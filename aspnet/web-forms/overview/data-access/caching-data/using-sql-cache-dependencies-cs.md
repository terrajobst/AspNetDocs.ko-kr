---
uid: web-forms/overview/data-access/caching-data/using-sql-cache-dependencies-cs
title: SQL 캐시 종속성 사용 (C#) | Microsoft Docs
author: rick-anderson
description: 가장 간단한 캐싱 전략은 지정 된 기간 후에 캐시 된 데이터의 만료를 허용 하는 것입니다. 그러나이 간단한 방법은 캐시 된 데이터 maintai.
ms.author: riande
ms.date: 05/30/2007
ms.assetid: 0e91842c-7f10-4aed-8c23-4ee3e2774014
msc.legacyurl: /web-forms/overview/data-access/caching-data/using-sql-cache-dependencies-cs
msc.type: authoredcontent
ms.openlocfilehash: 5bc27a08e39606c25b8f99d6ea057d2a853f08a6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78443087"
---
# <a name="using-sql-cache-dependencies-c"></a>SQL 캐시 종속성 사용(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_61_CS.zip) 또는 [PDF 다운로드](using-sql-cache-dependencies-cs/_static/datatutorial61cs1.pdf)

> 가장 간단한 캐싱 전략은 지정 된 기간 후에 캐시 된 데이터의 만료를 허용 하는 것입니다. 그러나이 간단한 방법은 캐시 된 데이터가 기본 데이터 원본과의 연결을 유지 하지 않으므로 오래 된 데이터를 너무 오래 유지 하거나 너무 빨리 만료 되는 최신 데이터를 유지 하는 것을 의미 합니다. SqlCacheDependency 클래스를 사용 하 여 SQL 데이터베이스에서 기본 데이터가 수정 될 때까지 데이터가 캐시 된 상태로 유지 되도록 하는 것이 더 좋습니다. 이 자습서에서는 방법을 보여 줍니다.

## <a name="introduction"></a>소개

아키텍처 자습서에서 ObjectDataSource 및 [캐싱 데이터](caching-data-in-the-architecture-cs.md) 를 사용 하 여 [데이터 캐싱](caching-data-with-the-objectdatasource-cs.md) 에서 검사 한 캐싱 기술은 지정 된 기간 후에 캐시에서 데이터를 제거 하는 시간 기반 만료를 사용 했습니다. 이 방법은 데이터 부실에 대해 캐싱의 성능 향상을 분산 하는 가장 간단한 방법입니다. 시간 만료 시간 ( *x* 초)을 선택 하면 페이지 개발자가 *x* 초에 대 한 concedes의 성능 이점을 얻을 수 있지만, 해당 데이터는 최대 *x* 초 보다 오래 되지 않습니다. 물론 정적 데이터의 경우 [응용 프로그램 시작 시 데이터 캐싱](caching-data-at-application-startup-cs.md) 자습서에서 살펴본 대로 *x* 를 웹 응용 프로그램의 수명으로 확장할 수 있습니다.

데이터베이스 데이터를 캐시할 때 시간 기반 만료는 사용 편의성을 위해 선택 되는 경우가 많지만 종종 부적절 한 솔루션입니다. 데이터베이스 데이터는 기본 데이터가 데이터베이스에서 수정 될 때까지 캐시 된 상태로 유지 되는 것이 가장 좋습니다. 그 다음에만 캐시가 제거 됩니다. 이 방법은 캐시의 성능 이점을 극대화 하 고 오래 된 데이터의 기간을 최소화 합니다. 그러나 이러한 혜택을 이용 하려면 기본 데이터베이스 데이터가 수정 된 시기를 인식 하 고 캐시에서 해당 항목을 임의로 시스템을 준비 해야 합니다. ASP.NET 2.0 이전에는 페이지 개발자가이 시스템을 구현 해야 했습니다.

ASP.NET 2.0는 해당 하는 캐시 된 항목을 제거할 수 있도록 데이터베이스에서 변경이 발생 한 시기를 확인 하는 데 필요한 인프라와 [`SqlCacheDependency` 클래스](https://msdn.microsoft.com/library/system.web.caching.sqlcachedependency.aspx) 를 제공 합니다. 기본 데이터가 변경 된 시기를 결정 하는 두 가지 방법이 있습니다. 알림 및 폴링. 알림과 폴링 간의 차이점을 논의 한 후에는 폴링을 지 원하는 데 필요한 인프라를 만든 다음 선언적이 고 프로그래밍 방식의 시나리오에서 `SqlCacheDependency` 클래스를 사용 하는 방법을 탐색 합니다.

## <a name="understanding-notification-and-polling"></a>알림 및 폴링 이해

데이터베이스의 데이터가 수정 된 시기를 확인 하는 데 사용할 수 있는 두 가지 방법은 알림 및 폴링입니다. 알림을 사용 하면 쿼리가 마지막으로 실행 된 이후 특정 쿼리의 결과가 변경 된 경우 데이터베이스에서 ASP.NET 런타임에 자동으로 경고 합니다 .이 시점에서 쿼리와 연결 된 캐시 된 항목이 제거 됩니다. 폴링을 사용 하면 데이터베이스 서버는 특정 테이블이 마지막으로 업데이트 된 시간에 대 한 정보를 유지 관리 합니다. ASP.NET 런타임은 데이터베이스를 주기적으로 폴링하여 캐시에 입력 된 이후 변경 된 테이블을 확인 합니다. 데이터가 수정 된 테이블은 연결 된 캐시 항목을 제거 합니다.

알림 옵션은 폴링 보다 더 작은 설정이 필요 하며 테이블 수준이 아닌 쿼리 수준에서 변경 내용을 추적 하기 때문에 더 세분화 됩니다. 불행 하 게도 Microsoft SQL Server 2005 (예: Express 버전이 아닌 버전)의 전체 버전 에서만 알림을 사용할 수 있습니다. 그러나 폴링 옵션은 7.0에서 2005 까지의 모든 버전 Microsoft SQL Server에 사용할 수 있습니다. 이러한 자습서에서는 SQL Server 2005의 Express 버전을 사용 하므로 폴링 옵션을 설정 하 고 사용 하는 데 중점을 둡니다. SQL Server 2005 s 알림 기능에 대 한 추가 리소스는이 자습서의 끝부분에 있는 추가 정보 섹션을 참조 하세요.

폴링을 사용 하 여 데이터베이스는 `tableName`, `notificationCreated`및 `changeId`의 3 개 열이 있는 `AspNet_SqlCacheTablesForChangeNotification` 이라는 테이블을 포함 하도록 구성 되어야 합니다. 이 테이블에는 웹 응용 프로그램의 SQL 캐시 종속성에서 사용 해야 하는 데이터가 있는 각 테이블에 대 한 행이 포함 되어 있습니다. `tableName` 열은 테이블의 이름을 지정 하는 반면 `notificationCreated`는 행이 테이블에 추가 된 날짜와 시간을 나타냅니다. `changeId` 열은 `int` 형식이 며 초기 값이 0입니다. 해당 값은 테이블을 수정할 때마다 증가 합니다.

`AspNet_SqlCacheTablesForChangeNotification` 테이블 외에도 데이터베이스에 SQL 캐시 종속성에 나타날 수 있는 각 테이블에 대 한 트리거를 포함 해야 합니다. 이러한 트리거는 행이 삽입, 업데이트 또는 삭제 될 때마다 실행 되 고 `AspNet_SqlCacheTablesForChangeNotification`에서 테이블 s `changeId` 값을 증가 시킵니다.

ASP.NET 런타임은 `SqlCacheDependency` 개체를 사용 하 여 데이터를 캐시할 때 테이블의 현재 `changeId`를 추적 합니다. 데이터베이스는 주기적으로 확인 되 고 다른 `changeId` 값은 데이터가 캐시 된 이후 테이블에 변경 내용이 있음을 나타내므로 해당 `changeId`의 값과 다른 `SqlCacheDependency` 개체가 제거 됩니다.

## <a name="step-1-exploring-theaspnet_regsqlexecommand-line-program"></a>1 단계:`aspnet_regsql.exe`명령줄 프로그램 탐색

폴링 방법을 사용 하는 경우 데이터베이스는 위에서 설명한 인프라를 포함 하도록 설치 해야 합니다. 미리 정의 된 테이블 (`AspNet_SqlCacheTablesForChangeNotification`), 몇 가지 저장 프로시저, 웹 응용 프로그램의 SQL 캐시 종속성에 사용 될 수 있는 각 테이블에 대 한 트리거 등이 있습니다. 이러한 테이블, 저장 프로시저 및 트리거는 `$WINDOWS$\Microsoft.NET\Framework\version` 폴더에 있는 `aspnet_regsql.exe`명령줄 프로그램을 통해 만들 수 있습니다. `AspNet_SqlCacheTablesForChangeNotification` 테이블 및 연결 된 저장 프로시저를 만들려면 명령줄에서 다음을 실행 합니다.

[!code-console[Main](using-sql-cache-dependencies-cs/samples/sample1.cmd)]

> [!NOTE]
> 이러한 명령을 실행 하려면 지정 된 데이터베이스 로그인이 [`db_securityadmin`](https://msdn.microsoft.com/library/ms188685.aspx) 및 [`db_ddladmin`](https://msdn.microsoft.com/library/ms190667.aspx) 역할에 있어야 합니다. `aspnet_regsql.exe` 명령줄 프로그램에서 데이터베이스에 보낸 T-sql을 검사 하려면 [이 블로그 항목](http://scottonwriting.net/sowblog/posts/10709.aspx)을 참조 하세요.

예를 들어 Windows 인증을 사용 하 여 `ScottsServer` 라는 데이터베이스 서버에서 `pubs` 라는 Microsoft SQL Server 데이터베이스에 폴링을 위한 인프라를 추가 하려면 적절 한 디렉터리로 이동 하 여 명령줄에서 다음을 입력 합니다.

[!code-console[Main](using-sql-cache-dependencies-cs/samples/sample2.cmd)]

데이터베이스 수준 인프라를 추가한 후 SQL 캐시 종속성에 사용 될 테이블에 트리거를 추가 해야 합니다. `aspnet_regsql.exe` 명령줄 프로그램을 다시 사용 하지만 `-t` 스위치를 사용 하 여 테이블 이름을 지정 하 고 `-ed` 스위치를 사용 하는 대신 다음과 같이 `-et`를 사용 합니다.

[!code-html[Main](using-sql-cache-dependencies-cs/samples/sample3.html)]

`authors`에 트리거를 추가 하 고 `ScottsServer`의 `pubs` 데이터베이스에 `titles` 테이블을 추가 하려면 다음을 사용 합니다.

[!code-console[Main](using-sql-cache-dependencies-cs/samples/sample4.cmd)]

이 자습서에서는 `Products`, `Categories`및 `Suppliers` 테이블에 트리거를 추가 합니다. 3 단계의 특정 명령줄 구문을 살펴보겠습니다.

## <a name="step-2-referencing-a-microsoft-sql-server-2005-express-edition-database-inapp_data"></a>2 단계:`App_Data`에서 Microsoft SQL Server 2005 Express Edition 데이터베이스 참조

필요한 폴링 인프라를 추가 하려면 `aspnet_regsql.exe` 명령줄 프로그램에 데이터베이스 및 서버 이름이 필요 합니다. 그러나 `App_Data` 폴더에 있는 Microsoft SQL Server 2005 Express 데이터베이스의 데이터베이스 및 서버 이름은 무엇 인가요? 데이터베이스와 서버 이름을 검색 하는 대신 데이터베이스를 `localhost\SQLExpress` 데이터베이스 인스턴스에 연결 하 고 [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx)를 사용 하 여 데이터 이름을 바꾸는 것이 가장 간단한 방법입니다. 컴퓨터에 SQL Server 2005의 전체 버전 중 하나가 설치 되어 있으면 컴퓨터에 이미 SQL Server Management Studio 설치 되어 있을 가능성이 높습니다. Express edition만 있는 경우 [Express edition Management Studio 무료 Microsoft SQL Server](https://www.microsoft.com/downloads/details.aspx?displaylang=en&amp;FamilyID=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796)다운로드할 수 있습니다.

먼저 Visual Studio를 닫습니다. 그런 다음 SQL Server Management Studio 열고 Windows 인증을 사용 하 여 `localhost\SQLExpress` 서버에 연결 하도록 선택 합니다.

![Localhost\SQLExpress 서버에 연결](using-sql-cache-dependencies-cs/_static/image1.gif)

**그림 1**: `localhost\SQLExpress` 서버에 연결

서버에 연결한 후에는 서버를 표시 하 고 데이터베이스, 보안 등에 대 한 하위 폴더를 Management Studio 합니다. 데이터베이스 폴더를 마우스 오른쪽 단추로 클릭 하 고 연결 옵션을 선택 합니다. 그러면 데이터베이스 연결 대화 상자가 표시 됩니다 (그림 2 참조). 추가 단추를 클릭 하 고 웹 응용 프로그램 `App_Data` 폴더의 `NORTHWND.MDF` 데이터베이스 폴더를 선택 합니다.

[NORTHWND.MDF를 연결 ![합니다. App_Data 폴더의 MDF 데이터베이스](using-sql-cache-dependencies-cs/_static/image2.gif)](using-sql-cache-dependencies-cs/_static/image1.png)

**그림 2**: `App_Data` 폴더에서 `NORTHWND.MDF` 데이터베이스 연결 ([전체 크기 이미지를 보려면 클릭](using-sql-cache-dependencies-cs/_static/image2.png))

데이터베이스 폴더에 데이터베이스가 추가 됩니다. 데이터베이스 이름은 데이터베이스 파일의 전체 경로 또는 [GUID](http://en.wikipedia.org/wiki/Globally_Unique_Identifier)가 앞에 붙은 전체 경로일 수 있습니다. Aspnet\_regsql 명령줄 도구를 사용 하는 경우이 긴 데이터베이스 이름을 입력할 필요가 없도록 하려면 연결 된 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 이름 바꾸기를 선택 하 여 데이터베이스 이름을 보다 알기 쉬운 이름으로 바꿉니다. 내 데이터베이스 이름을 DataTutorials로 변경 했습니다.

![연결 된 데이터베이스의 이름을 보다 알기 쉬운 이름으로 바꿉니다.](using-sql-cache-dependencies-cs/_static/image3.gif)

**그림 3**: 사용자에 게 친숙 한 이름으로 연결 된 데이터베이스 이름 바꾸기

## <a name="step-3-adding-the-polling-infrastructure-to-the-northwind-database"></a>3 단계: Northwind 데이터베이스에 폴링 인프라 추가

이제 `App_Data` 폴더에서 `NORTHWND.MDF` 데이터베이스를 연결 했으므로 폴링 인프라를 추가할 준비가 되었습니다. 데이터베이스의 이름을 DataTutorials로 변경 했다고 가정 하 고 다음 네 가지 명령을 실행 합니다.

[!code-console[Main](using-sql-cache-dependencies-cs/samples/sample5.cmd)]

이러한 네 가지 명령을 실행 한 후 Management Studio에서 데이터베이스 이름을 마우스 오른쪽 단추로 클릭 하 고 작업 하위 메뉴로 이동한 다음 분리를 선택 합니다. 그런 다음 Management Studio 닫고 Visual Studio를 다시 엽니다.

Visual Studio를 다시 연 후 서버 탐색기를 통해 데이터베이스를 드릴 다운 합니다. 새 테이블 (`AspNet_SqlCacheTablesForChangeNotification`), 새 저장 프로시저 및 `Products`, `Categories`및 `Suppliers` 테이블의 트리거를 확인 합니다.

![이제 데이터베이스에 필요한 폴링 인프라가 포함 되어 있습니다.](using-sql-cache-dependencies-cs/_static/image4.gif)

**그림 4**: 이제 데이터베이스에 필요한 폴링 인프라가 포함 되어 있습니다.

## <a name="step-4-configuring-the-polling-service"></a>4 단계: 폴링 서비스 구성

데이터베이스에서 필요한 테이블, 트리거 및 저장 프로시저를 만든 후 마지막 단계는 사용할 데이터베이스와 폴링 빈도 (밀리초)를 지정 하 여 `Web.config`을 통해 수행 되는 폴링 서비스를 구성 하는 것입니다. 다음 태그는 1 초 마다 한 번씩 Northwind 데이터베이스를 폴링합니다.

[!code-xml[Main](using-sql-cache-dependencies-cs/samples/sample6.xml)]

`<add>` 요소 (NorthwindDB)의 `name` 값은 사람이 읽을 수 있는 이름을 특정 데이터베이스에 연결 합니다. SQL 캐시 종속성을 사용 하는 경우 여기에 정의 된 데이터베이스 이름 뿐만 아니라 캐시 된 데이터의 기반이 되는 테이블을 참조 해야 합니다. `SqlCacheDependency` 클래스를 사용 하 여 6 단계에서 SQL 캐시 종속성을 캐시 된 데이터와 프로그래밍 방식으로 연결 하는 방법을 알아봅니다.

SQL 캐시 종속성이 설정 되 면 폴링 시스템은 `pollTime` 밀리초 마다 `<databases>` 요소에 정의 된 데이터베이스에 연결 하 고 `AspNet_SqlCachePollingStoredProcedure` 저장 프로시저를 실행 합니다. `aspnet_regsql.exe` 명령줄 도구를 사용 하 여 3 단계에서 다시 추가 된이 저장 프로시저는 `AspNet_SqlCacheTablesForChangeNotification`의 각 레코드에 대 한 `tableName` 및 `changeId` 값을 반환 합니다. 오래 된 SQL 캐시 종속성은 캐시에서 제거 됩니다.

`pollTime` 설정에는 성능 및 데이터 부실 간에 균형을 유지 하는 기능이 도입 되었습니다. 작은 `pollTime` 값은 데이터베이스에 대 한 요청 수를 늘리고 캐시에서 오래 된 데이터를 더 빠르게 임의로 합니다. `pollTime` 값이 클수록 데이터베이스 요청 수가 줄어들지만 백 엔드 데이터를 변경 하는 시간과 관련 캐시 항목이 제거 될 때까지 지연 시간이 증가 합니다. 다행히 데이터베이스 요청은 단순 하 고 간단한 테이블에서 몇 개의 행만 반환 하는 간단한 저장 프로시저를 실행 합니다. 그러나 데이터베이스 액세스와 응용 프로그램에 대 한 데이터 부실 간에 이상적인 균형을 찾기 위해 다른 `pollTime` 값을 시험해 봅니다. 허용 되는 가장 작은 `pollTime` 값은 500입니다.

> [!NOTE]
> 위의 예에서는 `<sqlCacheDependency>` 요소에 단일 `pollTime` 값을 제공 하지만 필요에 따라 `<add>` 요소에 `pollTime` 값을 지정할 수 있습니다. 이는 여러 데이터베이스를 지정 하 고 데이터베이스당 폴링 빈도를 사용자 지정 하려는 경우에 유용 합니다.

## <a name="step-5-declaratively-working-with-sql-cache-dependencies"></a>5 단계: 선언적으로 SQL 캐시 종속성 작업

1 ~ 4 단계에서는 필요한 데이터베이스 인프라를 설정 하 고 폴링 시스템을 구성 하는 방법을 살펴보았습니다. 이제이 인프라를 사용 하 여 프로그래밍 방식 또는 선언적 기술을 사용 하 여 연결 된 SQL 캐시 종속성으로 데이터 캐시에 항목을 추가할 수 있습니다. 이 단계에서는 SQL 캐시 종속성을 선언적으로 사용 하는 방법을 살펴보겠습니다. 6 단계에서는 프로그래밍 방식으로 살펴보겠습니다.

[Objectdatasource를 사용 하 여 데이터 캐싱](caching-data-with-the-objectdatasource-cs.md) 자습서에서는 objectdatasource의 선언적 캐싱 기능을 탐색 했습니다. `EnableCaching` 속성을 `true`로 설정 하 고 `CacheDuration` 속성을 일정 시간 간격으로 설정 하면 ObjectDataSource가 지정 된 간격 동안 기본 개체에서 반환 된 데이터를 자동으로 캐시 합니다. ObjectDataSource는 하나 이상의 SQL 캐시 종속성을 사용할 수도 있습니다.

SQL 캐시 종속성을 선언적으로 사용 하는 방법을 보여 주려면 `Caching` 폴더에서 `SqlCacheDependencies.aspx` 페이지를 열고 GridView를 도구 상자에서 디자이너로 끌어 놓습니다. GridView s `ID`를 `ProductsDeclarative`로 설정 하 고 스마트 태그에서 `ProductsDataSourceDeclarative`라는 새 ObjectDataSource에 바인딩합니다.

[ProductsDataSourceDeclarative 라는 새 ObjectDataSource를 만들 ![](using-sql-cache-dependencies-cs/_static/image5.gif)](using-sql-cache-dependencies-cs/_static/image3.png)

**그림 5**: 이름이 `ProductsDataSourceDeclarative` 새 ObjectDataSource 만들기 ([전체 크기 이미지를 보려면 클릭](using-sql-cache-dependencies-cs/_static/image4.png))

`ProductsBLL` 클래스를 사용 하도록 ObjectDataSource를 구성 하 고 선택 탭의 드롭다운 목록을 `GetProducts()`로 설정 합니다. 업데이트 탭에서 `productName`, `unitPrice`및 `productID`의 세 가지 입력 매개 변수를 사용 하 여 `UpdateProduct` 오버 로드를 선택 합니다. 삽입 및 삭제 탭에서 드롭다운 목록을 (없음)으로 설정 합니다.

[3 개의 입력 매개 변수를 사용 하 여 UpdateProduct 오버 로드를 사용 ![](using-sql-cache-dependencies-cs/_static/image6.gif)](using-sql-cache-dependencies-cs/_static/image5.png)

**그림 6**: 3 개의 입력 매개 변수를 사용 하 여 Updateproduct 오버 로드 사용 ([전체 크기 이미지를 보려면 클릭](using-sql-cache-dependencies-cs/_static/image6.png))

[삽입 및 삭제 탭에 대 한 드롭다운 목록을 (없음)으로 설정 ![](using-sql-cache-dependencies-cs/_static/image7.gif)](using-sql-cache-dependencies-cs/_static/image7.png)

**그림 7**: 삽입 및 삭제 탭에 대 한 드롭다운 목록을 (없음)로 설정 ([전체 크기 이미지를 보려면 클릭](using-sql-cache-dependencies-cs/_static/image8.png))

데이터 소스 구성 마법사를 완료 한 후 Visual Studio에서 각 데이터 필드에 대해 GridView에 BoundFields 및 CheckBoxFields를 만듭니다. 모든 필드를 제거 하 고, `ProductName`, `CategoryName`및 `UnitPrice`하 고, 적절 하 게 표시 되는 필드의 서식을 지정 합니다. GridView s 스마트 태그에서 페이징 사용, 정렬 사용 및 편집 사용 확인란을 선택 합니다. 그러면 ObjectDataSource s `OldValuesParameterFormatString` 속성이 `original_{0}`로 설정 됩니다. GridView의 편집 기능이 제대로 작동 하려면 선언적 구문에서이 속성을 완전히 제거 하거나 `{0}`기본값으로 다시 설정 합니다.

마지막으로 GridView 위에 Label 웹 컨트롤을 추가 하 고 해당 `ID` 속성을 `ODSEvents`로 설정 하 고 `EnableViewState` 속성을 `false`로 설정 합니다. 이러한 변경을 수행한 후에는 페이지의 선언적 태그가 다음과 같이 표시 됩니다. SQL 캐시 종속성 기능을 설명 하는 데 필요 하지 않은 GridView 필드에 대해 많은 사용자 지정 항목을 미적 했습니다.

[!code-aspx[Main](using-sql-cache-dependencies-cs/samples/sample7.aspx)]

다음으로, ObjectDataSource s `Selecting` 이벤트에 대 한 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample8.cs)]

ObjectDataSource s `Selecting` 이벤트는 기본 개체에서 데이터를 검색 하는 경우에만 발생 합니다. ObjectDataSource가 자체 캐시에서 데이터에 액세스 하는 경우에는이 이벤트가 발생 하지 않습니다.

이제 브라우저를 통해이 페이지를 방문 하세요. 캐싱을 구현 하려고 하기 때문에, 표를 페이지, 정렬 또는 편집할 때마다 페이지에는 그림 8에 표시 된 것 처럼 이벤트가 발생 하는 것을 선택 하 여 텍스트를 표시 해야 합니다.

[GridView를 페이징 하거나, 편집 하거나, 정렬할 때마다 ObjectDataSource s를 선택 하는 이벤트가 발생 ![](using-sql-cache-dependencies-cs/_static/image8.gif)](using-sql-cache-dependencies-cs/_static/image9.png)

**그림 8**: ObjectDataSource s `Selecting` 이벤트는 GridView가 페이징, 편집 또는 정렬 될 때마다 발생 합니다 ([전체 크기 이미지를 보려면 클릭](using-sql-cache-dependencies-cs/_static/image10.png)).

ObjectDataSource를 사용 하 여 [데이터 캐싱](caching-data-with-the-objectdatasource-cs.md) 자습서에서 살펴본 것 처럼 `EnableCaching` 속성을 `true`로 설정 하면 objectdatasource가 `CacheDuration` 속성에 지정 된 기간 동안 해당 데이터를 캐시 합니다. ObjectDataSource에는 다음 패턴을 사용 하 여 캐시 된 데이터에 하나 이상의 SQL 캐시 종속성을 추가 하는 [`SqlCacheDependency` 속성도](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.sqlcachedependency.aspx)있습니다.

[!code-css[Main](using-sql-cache-dependencies-cs/samples/sample9.css)]

여기서 *databaseName* 은 `Web.config`에 있는 `<add>` 요소의 `name` 특성에 지정 된 데이터베이스의 이름이 고 *tableName* 은 데이터베이스 테이블의 이름입니다. 예를 들어 Northwind s `Products` 테이블에 대 한 SQL 캐시 종속성에 따라 무한정 데이터를 캐시 하는 ObjectDataSource를 만들려면 ObjectDataSource s `EnableCaching` 속성을 `true`로 설정 하 고 해당 `SqlCacheDependency` 속성을 NorthwindDB: Products로 설정 합니다.

> [!NOTE]
> `EnableCaching`을 `true`로 설정 하 고 시간 간격으로 `CacheDuration` 하 고 데이터베이스 및 테이블 이름에 `SqlCacheDependency`를 설정 하 여 SQL 캐시 종속성 *및* 시간 기반 만료를 사용할 수 있습니다. ObjectDataSource는 시간 기반 만료에 도달 하거나 폴링 시스템에서 기본 데이터베이스 데이터를 변경 하는 것이 먼저 발생 하는 경우 해당 데이터를 제거 합니다.

`SqlCacheDependencies.aspx` GridView는 `Products` 및 `Categories` 두 테이블의 데이터를 표시 합니다. 제품 `CategoryName` 필드는 `JOIN`의 `Categories`를 통해 검색 됩니다. 따라서 두 개의 SQL 캐시 종속성 (NorthwindDB: Products;)을 지정 하려고 합니다. NorthwindDB: 범주.

[제품 및 범주에 대 한 SQL 캐시 종속성을 사용 하 여 캐싱을 지원 하도록 ObjectDataSource 구성 ![](using-sql-cache-dependencies-cs/_static/image9.gif)](using-sql-cache-dependencies-cs/_static/image11.png)

**그림 9**: `Products` 및 `Categories`에서 SQL 캐시 종속성을 사용 하 여 캐싱을 지원 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](using-sql-cache-dependencies-cs/_static/image12.png))

캐싱을 지원 하도록 ObjectDataSource를 구성한 후 브라우저를 통해 페이지를 다시 방문 합니다. 이 경우에도 실행 되는 이벤트 선택 텍스트가 첫 번째 페이지에 표시 되어야 하지만 페이징, 정렬 또는 편집 또는 취소 단추를 클릭할 때 사라집니다. 이는 데이터를 ObjectDataSource 캐시에 로드 한 후 `Products` 또는 `Categories` 테이블이 수정 되거나 GridView를 통해 데이터가 업데이트 될 때까지 유지 되기 때문입니다.

표를 페이징 하 고 이벤트가 발생 하는 이벤트가 발생 하지 않은 경우에는 새 브라우저 창을 열고 편집, 삽입 및 삭제 섹션 (`~/EditInsertDelete/Basics.aspx`)의 기본 사항 자습서로 이동 합니다. 제품의 이름 또는 가격을 업데이트 합니다. 그런 다음, 첫 번째 브라우저 창에서 다른 데이터 페이지를 보거나, 표를 정렬 하거나, 행의 편집 단추를 클릭 합니다. 이번에는 기본 데이터베이스 데이터가 수정 되었기 때문에 발생 하는 선택 이벤트가 다시 나타납니다 (그림 10 참조). 텍스트가 표시 되지 않으면 잠시 기다린 후 다시 시도 하세요. 폴링 서비스는 `pollTime` 밀리초 마다 `Products` 테이블에 대 한 변경 내용을 확인 하 고 있으므로 기본 데이터가 업데이트 되는 시간과 캐시 된 데이터가 제거 될 때 사이에 지연이 발생 합니다.

[Products 테이블을 수정 하 ![임의로는 캐시 된 제품 데이터를](using-sql-cache-dependencies-cs/_static/image10.gif)](using-sql-cache-dependencies-cs/_static/image13.png)

**그림 10**: Products 테이블을 수정 하 여 캐시 된 제품 데이터 임의로 ([전체 크기 이미지를 보려면 클릭](using-sql-cache-dependencies-cs/_static/image14.png))

## <a name="step-6-programmatically-working-with-thesqlcachedependencyclass"></a>6 단계: 프로그래밍 방식으로`SqlCacheDependency`클래스 작업

[아키텍처의 데이터 캐싱](caching-data-in-the-architecture-cs.md) 자습서에서는 캐싱을 ObjectDataSource와 긴밀 하 게 결합 하는 것이 아니라 아키텍처에서 별도의 캐싱 계층을 사용 하는 이점을 살펴보았습니다. 이 자습서에서는 데이터 캐시를 프로그래밍 방식으로 사용 하는 방법을 보여 주기 위해 `ProductsCL` 클래스를 만들었습니다. 캐싱 계층에서 SQL 캐시 종속성을 활용 하려면 `SqlCacheDependency` 클래스를 사용 합니다.

폴링 시스템에서 `SqlCacheDependency` 개체는 특정 데이터베이스 및 테이블 쌍에 연결 되어야 합니다. 예를 들어 다음 코드는 Northwind 데이터베이스의 `Products` 테이블을 기반으로 `SqlCacheDependency` 개체를 만듭니다.

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample10.cs)]

`SqlCacheDependency` s 생성자에 대 한 두 개의 입력 매개 변수는 각각 데이터베이스 및 테이블 이름입니다. ObjectDataSource s `SqlCacheDependency` 속성과 마찬가지로, 사용 되는 데이터베이스 이름은 `Web.config`에 있는 `<add>` 요소의 `name` 특성에 지정 된 값과 동일 합니다. 테이블 이름은 데이터베이스 테이블의 실제 이름입니다.

`SqlCacheDependency`를 데이터 캐시에 추가 된 항목과 연결 하려면 종속성을 허용 하는 `Insert` 메서드 오버 로드 중 하나를 사용 합니다. 다음 코드는 무한 기간 동안 데이터 캐시에 *값* 을 추가 하지만 `Products` 테이블의 `SqlCacheDependency`와 연결 합니다. 즉, *값* 은 메모리 제약 조건으로 인해 제거 될 때까지 또는 캐시 된 이후에 `Products` 테이블이 변경 되었음을 검색 하기 전까지 캐시에 남아 있습니다.

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample11.cs)]

캐싱 계층 s `ProductsCL` 클래스는 현재 시간 기반 만료 60 초를 사용 하 여 `Products` 테이블의 데이터를 캐시 합니다. 대신 SQL 캐시 종속성을 사용 하도록이 클래스를 업데이트 해 보겠습니다. 캐시에 데이터를 추가 하는 `ProductsCL` 클래스 s `AddCacheItem` 메서드는 현재 다음 코드를 포함 합니다.

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample12.cs)]

`MasterCacheKeyArray` 캐시 종속성 대신 `SqlCacheDependency` 개체를 사용 하도록이 코드를 업데이트 합니다.

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample13.cs)]

이 기능을 테스트 하려면 GridView를 기존 `ProductsDeclarative` GridView 아래에 있는 페이지에 추가 합니다. 새 GridView s `ID`를 `ProductsProgrammatic`으로 설정 하 고 스마트 태그를 통해 `ProductsDataSourceProgrammatic`라는 새 ObjectDataSource에 바인딩합니다. `ProductsCL` 클래스를 사용 하도록 ObjectDataSource를 구성 하 고 선택 및 업데이트 탭의 드롭다운 목록을 각각 `GetProducts` 및 `UpdateProduct`로 설정 합니다.

[![하 여 제품 Scl 클래스를 사용 하도록 ObjectDataSource 구성](using-sql-cache-dependencies-cs/_static/image11.gif)](using-sql-cache-dependencies-cs/_static/image15.png)

**그림 11**: `ProductsCL` 클래스를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](using-sql-cache-dependencies-cs/_static/image16.png))

[SELECT Tab s 드롭다운 목록에서 GetProducts 메서드를 선택 ![](using-sql-cache-dependencies-cs/_static/image12.gif)](using-sql-cache-dependencies-cs/_static/image17.png)

**그림 12**: 탭 선택 드롭다운 목록에서 `GetProducts` 메서드 선택 ([전체 크기 이미지를 보려면 클릭](using-sql-cache-dependencies-cs/_static/image18.png))

[업데이트 탭의 드롭다운 목록에서 UpdateProduct 메서드를 선택 ![](using-sql-cache-dependencies-cs/_static/image13.gif)](using-sql-cache-dependencies-cs/_static/image19.png)

**그림 13**: 업데이트 탭의 드롭다운 목록에서 Updateproduct 메서드 선택 ([전체 크기 이미지를 보려면 클릭](using-sql-cache-dependencies-cs/_static/image20.png))

데이터 소스 구성 마법사를 완료 한 후 Visual Studio에서 각 데이터 필드에 대해 GridView에 BoundFields 및 CheckBoxFields를 만듭니다. 이 페이지에 첫 번째 GridView가 추가 된 것 처럼 모든 필드를 제거 하 고, `CategoryName`및 `UnitPrice``ProductName`하 고, 적절 하 게 표시 되는 필드의 서식을 지정 합니다. GridView s 스마트 태그에서 페이징 사용, 정렬 사용 및 편집 사용 확인란을 선택 합니다. `ProductsDataSourceDeclarative` ObjectDataSource와 마찬가지로 Visual Studio에서는 `ProductsDataSourceProgrammatic` ObjectDataSource s `OldValuesParameterFormatString` 속성을 `original_{0}`로 설정 합니다. GridView의 편집 기능이 제대로 작동 하려면이 속성을 다시 `{0}`로 설정 하거나 선언적 구문에서 속성 할당을 완전히 제거 합니다.

이러한 작업을 완료 한 후 결과 GridView 및 ObjectDataSource 선언 태그는 다음과 같습니다.

[!code-aspx[Main](using-sql-cache-dependencies-cs/samples/sample14.aspx)]

캐싱 계층에서 SQL 캐시 종속성을 테스트 하려면 `ProductCL` 클래스 s `AddCacheItem` 메서드에 중단점을 설정한 다음 디버깅을 시작 합니다. `SqlCacheDependencies.aspx`를 처음 방문 하는 경우 처음으로 데이터를 요청 하 고 캐시에 배치 하면 중단점이 적중 됩니다. 다음으로 GridView의 다른 페이지로 이동 하거나 열 중 하나를 정렬 합니다. 이로 인해 GridView가 해당 데이터를 다시 쿼리해야 하지만 `Products` 데이터베이스 테이블이 수정 되지 않았기 때문에 캐시에 데이터가 있습니다. 캐시에서 데이터를 반복적으로 찾을 수 없는 경우 컴퓨터에 사용할 수 있는 메모리가 충분 한지 확인 한 후 다시 시도 하십시오.

GridView의 일부 페이지를 페이징 한 후에 두 번째 브라우저 창을 열고 편집, 삽입 및 삭제 섹션 (`~/EditInsertDelete/Basics.aspx`)의 기본 사항 자습서로 이동 합니다. Products 테이블에서 레코드를 업데이트 한 다음 첫 번째 브라우저 창에서 새 페이지를 확인 하거나 정렬 헤더 중 하나를 클릭 합니다.

이 시나리오에서는 두 가지 중 하나가 표시 됩니다. 즉, 중단점에 도달 하 여 캐시 된 데이터가 데이터베이스의 변경으로 인해 제거 되었음을 나타냅니다. 또는 중단점에 도달 하지 않습니다. 즉, `SqlCacheDependencies.aspx`는 이제 부실 데이터를 표시 합니다. 중단점이 적중 되지 않으면 데이터가 변경 된 후에도 폴링 서비스가 아직 발생 하지 않았기 때문일 수 있습니다. 폴링 서비스는 `pollTime` 밀리초 마다 `Products` 테이블에 대 한 변경 내용을 확인 하 고 있으므로 기본 데이터가 업데이트 되는 시간과 캐시 된 데이터가 제거 될 때 사이에 지연이 발생 합니다.

> [!NOTE]
> 이러한 지연은 `SqlCacheDependencies.aspx`에서 GridView를 통해 제품 중 하나를 편집할 때 나타날 가능성이 높습니다. [아키텍처의 데이터 캐싱](caching-data-in-the-architecture-cs.md) 자습서에서는 `ProductsCL` 클래스 s `UpdateProduct` 메서드를 통해 편집 중인 데이터가 캐시에서 제거 되었는지 확인 하기 위해 `MasterCacheKeyArray` cache 종속성을 추가 했습니다. 그러나이 단계에서 이전에 `AddCacheItem` 메서드를 수정할 때이 캐시 종속성을 대체 했으므로 폴링 시스템에서 `Products` 테이블의 변경 내용을 확인할 때까지 `ProductsCL` 클래스는 캐시 된 데이터를 계속 표시 합니다. 7 단계에서 `MasterCacheKeyArray` cache 종속성을 이동 하는 방법을 알아봅니다.

## <a name="step-7-associating-multiple-dependencies-with-a-cached-item"></a>7 단계: 캐시 된 항목에 여러 종속성 연결

`MasterCacheKeyArray` 캐시 종속성은 관련 된 단일 항목이 업데이트 될 때 *모든* 제품 관련 데이터가 캐시에서 제거 되도록 하는 데 사용 됩니다. 예를 들어 `GetProductsByCategoryID(categoryID)` 메서드는 각 고유 *categoryID* 값에 대해 `ProductsDataTables` 인스턴스를 캐시 합니다. 이러한 개체 중 하나를 제거 하는 경우 캐시 종속성 `MasterCacheKeyArray` 다른 항목도 제거 됩니다. 이 캐시 종속성이 없는 경우 캐시 된 데이터를 수정 하면 캐시 된 다른 제품 데이터가 만료 될 가능성이 있습니다. 따라서 SQL 캐시 종속성을 사용할 때 `MasterCacheKeyArray` 캐시 종속성을 유지 관리 하는 것이 중요 합니다. 그러나 data cache s `Insert` 메서드는 단일 종속성 개체만 허용 합니다.

또한 SQL 캐시 종속성을 사용 하는 경우 여러 데이터베이스 테이블을 종속성으로 연결 해야 할 수 있습니다. 예를 들어 `ProductsCL` 클래스에 캐시 된 `ProductsDataTable`는 각 제품에 대 한 범주 및 공급자 이름을 포함 하지만 `AddCacheItem` 메서드는 `Products`에 대 한 종속성만 사용 합니다. 이 경우 사용자가 범주나 공급자의 이름을 업데이트 하면 캐시 된 제품 데이터가 캐시에 남아 있고 만료 되지 않습니다. 따라서 캐시 된 제품 데이터를 `Products` 테이블 뿐만 아니라 `Categories` 및 `Suppliers` 테이블에 종속 되도록 지정 하려고 합니다.

[`AggregateCacheDependency` 클래스](https://msdn.microsoft.com/library/system.web.caching.aggregatecachedependency.aspx) 는 여러 종속성을 캐시 항목과 연결 하기 위한 방법을 제공 합니다. `AggregateCacheDependency` 인스턴스를 만들어 시작 합니다. 다음으로 `AggregateCacheDependency` s `Add` 메서드를 사용 하 여 종속성 집합을 추가 합니다. 이후에 데이터 캐시에 항목을 삽입할 때 `AggregateCacheDependency` 인스턴스를 전달 합니다. `AggregateCacheDependency` 인스턴스 s 종속성이 변경 *되 면 캐시* 된 항목이 제거 됩니다.

다음은 `ProductsCL` 클래스 `AddCacheItem` 메서드의 업데이트 된 코드를 보여 줍니다. 메서드는 `Products`, `Categories`및 `Suppliers` 테이블의 `SqlCacheDependency` 개체와 함께 `MasterCacheKeyArray` cache 종속성을 만듭니다. 이러한 개체는 모두 `aggregateDependencies`라는 하나의 `AggregateCacheDependency` 개체로 결합 되며이 개체는 `Insert` 메서드로 전달 됩니다.

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample15.cs)]

이 새 코드를 테스트 합니다. 이제 `Products`, `Categories`또는 `Suppliers` 테이블로 변경 하면 캐시 된 데이터가 제거 됩니다. 또한 GridView를 통해 제품을 편집할 때 호출 되는 `ProductsCL` 클래스 `UpdateProduct` 메서드는 캐시 된 `ProductsDataTable`를 제거 하 고 다음 요청 시 데이터를 다시 검색 하는 `MasterCacheKeyArray` 캐시 종속성을 임의로 합니다.

> [!NOTE]
> SQL 캐시 종속성을 [출력 캐싱과](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/caching/output.aspx)함께 사용할 수도 있습니다. 이 기능에 대 한 데모는 SQL Server에서 [ASP.NET 출력 캐싱 사용](https://msdn.microsoft.com/library/e3w8402y(VS.80).aspx)을 참조 하세요.

## <a name="summary"></a>요약

데이터베이스 데이터를 캐시할 때 데이터는 데이터베이스에서 수정 될 때까지 캐시에 유지 됩니다. ASP.NET 2.0를 사용 하면 선언적 시나리오와 프로그래밍 방식 시나리오 모두에서 SQL 캐시 종속성을 만들고 사용할 수 있습니다. 이 방법의 문제 중 하나는 데이터가 수정 된 경우를 검색 하는 것입니다. Microsoft SQL Server 2005의 전체 버전에서는 쿼리 결과가 변경 될 때 응용 프로그램에 경고할 수 있는 알림 기능을 제공 합니다. Express Edition SQL Server 2005 및 이전 버전의 SQL Server의 경우 폴링 시스템을 대신 사용 해야 합니다. 다행히 필요한 폴링 인프라를 설정 하는 것은 매우 간단 합니다.

행복 한 프로그래밍

## <a name="further-reading"></a>추가 참고 자료

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [Microsoft SQL Server 2005에서 쿼리 알림 사용](https://msdn.microsoft.com/library/ms175110.aspx)
- [쿼리 알림 만들기](https://msdn.microsoft.com/library/ms188669.aspx)
- [`SqlCacheDependency` 클래스를 사용 하 여 ASP.NET에서 캐싱](https://msdn.microsoft.com/library/ms178604(VS.80).aspx)
- [ASP.NET SQL Server 등록 도구 (`aspnet_regsql.exe`)](https://msdn.microsoft.com/library/ms229862(vs.80).aspx)
- [`SqlCacheDependency` 개요](http://www.aspnetresources.com/blog/sql_cache_depedency_overview.aspx)

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서에 대 한 리드 검토자는 Marko Rangel, Teresa Murphy 및 Hilton Gid Esenow입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](caching-data-at-application-startup-cs.md)
> [다음](caching-data-with-the-objectdatasource-vb.md)
