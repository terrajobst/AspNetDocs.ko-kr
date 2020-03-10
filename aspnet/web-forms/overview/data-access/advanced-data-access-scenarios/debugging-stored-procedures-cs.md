---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/debugging-stored-procedures-cs
title: 저장 프로시저 디버깅 (C#) | Microsoft Docs
author: rick-anderson
description: Visual Studio Professional 및 Team System 버전을 사용 하면 중단점을 설정 하 고 SQL Server 내 저장 프로시저에 한 단계씩 실행 하 여 디버깅을 저장할 수 있습니다.
ms.author: riande
ms.date: 08/03/2007
ms.assetid: c655c324-2ffa-4c21-8265-a254d79a693d
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/debugging-stored-procedures-cs
msc.type: authoredcontent
ms.openlocfilehash: 12a8500b107345b9cc9ab457016fdef09ca1bb9d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78428393"
---
# <a name="debugging-stored-procedures-c"></a>저장 프로시저 디버그(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_74_CS.zip) 또는 [PDF 다운로드](debugging-stored-procedures-cs/_static/datatutorial74cs1.pdf)

> Visual Studio Professional 및 Team System 버전을 사용 하면 중단점을 설정 하 고 SQL Server 내의 저장 프로시저를 단계별로 실행 하 여 응용 프로그램 코드를 디버깅 하는 것 처럼 저장 프로시저를 쉽게 디버깅할 수 있습니다. 이 자습서에서는 데이터베이스를 직접 디버깅 하 고 저장 프로시저를 디버깅 하는 방법을 보여 줍니다.

## <a name="introduction"></a>소개

Visual Studio는 풍부한 디버깅 환경을 제공 합니다. 마우스를 몇 번의 키 입력 이나 클릭 하면 중단점을 사용 하 여 프로그램 실행을 중지 하 고 상태 및 제어 흐름을 검사할 수 있습니다. Visual Studio는 응용 프로그램 코드 디버깅과 함께 SQL Server 내에서 저장 프로시저를 디버깅 하는 기능을 제공 합니다. ASP.NET 코드 지향 클래스 또는 비즈니스 논리 계층 클래스의 코드 내에서 중단점을 설정 하는 것 처럼 저장 프로시저 내에 배치할 수 있습니다.

이 자습서에서는 실행 중인 ASP.NET 응용 프로그램에서 저장 프로시저를 호출할 때 적중 되는 중단점을 설정 하는 방법 뿐만 아니라 Visual Studio 내의 서버 탐색기에서 저장 프로시저를 단계별로 실행 하는 방법을 살펴봅니다.

> [!NOTE]
> 그러나 저장 프로시저는 Visual Studio Professional 및 Team Systems 버전을 통해서만 단계별로 실행할 수 있습니다. Visual Web Developer 또는 standard 버전의 Visual Studio를 사용 하는 경우 저장 프로시저를 디버깅 하는 데 필요한 단계를 진행 하면서 계속 읽을 수 있지만 이러한 단계를 컴퓨터에서 복제할 수는 없습니다.

## <a name="sql-server-debugging-concepts"></a>SQL Server 디버깅 개념

Microsoft SQL Server 2005는 모든 .NET 어셈블리에서 사용 되는 런타임 [CLR (공용 언어 런타임)](https://msdn.microsoft.com/netframework/aa497266.aspx)과의 통합을 제공 하도록 설계 되었습니다. 따라서 2005 SQL Server 관리 되는 데이터베이스 개체를 지원 합니다. 즉, 저장 프로시저 및 Udf (사용자 정의 함수)와 같은 데이터베이스 개체를 C# 클래스의 메서드로 만들 수 있습니다. 이렇게 하면 이러한 저장 프로시저 및 Udf를 사용 하 여 .NET Framework 및 사용자 고유의 사용자 지정 클래스의 기능을 활용할 수 있습니다. 물론 SQL Server 2005는 T-sql 데이터베이스 개체에 대 한 지원도 제공 합니다.

SQL Server 2005는 T-sql 및 관리 되는 데이터베이스 개체에 대 한 디버깅 지원을 제공 합니다. 그러나 이러한 개체는 Visual Studio 2005 Professional 및 Team Systems edition을 통해서만 디버그할 수 있습니다. 이 자습서에서는 T-sql 데이터베이스 개체 디버깅을 살펴보겠습니다. 이후 자습서에서는 관리 되는 데이터베이스 개체를 디버깅 하는 방법을 살펴봅니다.

[SQL Server 2005 CLR 통합 팀](https://blogs.msdn.com/sqlclr/default.aspx) 의 [SQL Server 2005 블로그 항목에서 T-sql 및 CLR 디버깅의 개요](https://blogs.msdn.com/sqlclr/archive/2006/06/29/651644.aspx) 는 Visual Studio에서 SQL Server 2005 개체를 디버깅 하는 세 가지 방법을 강조 표시 합니다.

- **DDD (직접 데이터베이스 디버깅)** -서버 탐색기에서 저장 프로시저 및 udf와 같은 t-sql 데이터베이스 개체를 한 단계씩 코드 실행 할 수 있습니다. 1 단계에서 DDD를 살펴보겠습니다.
- **응용 프로그램 디버깅** -데이터베이스 개체 내에 중단점을 설정한 다음 ASP.NET 응용 프로그램을 실행할 수 있습니다. 데이터베이스 개체가 실행 될 때 중단점에 도달 하 고 디버거로 제어가 설정 됩니다. 응용 프로그램 디버깅을 사용 하면 응용 프로그램 코드에서 데이터베이스 개체를 한 단계씩 실행할 수 없습니다. 디버거를 중지 하려는 저장 프로시저나 Udf에서 중단점을 명시적으로 설정 해야 합니다. 응용 프로그램 디버깅은 2 단계부터 검사 됩니다.
- **SQL Server 프로젝트** Visual Studio Professional 및 Team system Edition에서 디버깅에는 관리 되는 데이터베이스 개체를 만드는 데 일반적으로 사용 되는 SQL Server 프로젝트 형식이 포함 되어 있습니다. 다음 자습서에서 SQL Server 프로젝트를 사용 하 고 해당 콘텐츠를 디버그 하는 방법을 살펴보겠습니다.

Visual Studio는 로컬 및 원격 SQL Server 인스턴스에서 저장 프로시저를 디버그할 수 있습니다. 로컬 SQL Server 인스턴스는 Visual Studio와 같은 컴퓨터에 설치 되어 있습니다. 사용 중인 SQL Server 데이터베이스가 개발 컴퓨터에 없는 경우 원격 인스턴스로 간주 됩니다. 이러한 자습서에서는 로컬 SQL Server 인스턴스를 사용 했습니다. 원격 SQL server 인스턴스에서 저장 프로시저를 디버깅 하려면 로컬 인스턴스에서 저장 프로시저를 디버깅할 때 보다 더 많은 구성 단계가 필요 합니다.

로컬 SQL Server 인스턴스를 사용 하는 경우 1 단계부터 시작 하 여이 자습서를 마칠 수 있습니다. 그러나 원격 SQL Server 인스턴스를 사용 하는 경우에는 먼저 디버깅할 때 원격 인스턴스에 대 한 SQL Server 로그인이 있는 Windows 사용자 계정을 사용 하 여 개발 컴퓨터에 로그인 해야 합니다. 또한이 데이터베이스 로그인과 실행 중인 ASP.NET 응용 프로그램에서 데이터베이스에 연결 하는 데 사용 되는 데이터베이스 로그인은 모두 `sysadmin` 역할의 멤버 여야 합니다. Visual Studio를 구성 하 SQL Server 고 원격 인스턴스를 디버깅 하는 방법에 대 한 자세한 내용은이 자습서의 끝부분에 있는 원격 인스턴스에 대 한 T-SQL Database 개체 디버깅 섹션을 참조 하세요.

마지막으로, T-sql 데이터베이스 개체에 대 한 디버깅 지원이 .NET 응용 프로그램에 대 한 디버깅 지원으로 풍부한 기능으로 인식 되지 않습니다. 예를 들어 중단점 조건 및 필터는 지원 되지 않으며, 디버깅 창의 하위 집합만 사용할 수 있으며, 편집 하며 계속 하기를 사용할 수 없으며, 직접 실행 창이 쓸모 없게 렌더링 됩니다. 자세한 내용은 [디버거 명령 및 기능에 대 한 제한 사항](https://msdn.microsoft.com/library/ms165035(VS.80).aspx) 을 참조 하세요.

## <a name="step-1-directly-stepping-into-a-stored-procedure"></a>1 단계: 저장 프로시저 직접 한 단계씩 코드 실행

Visual Studio를 사용 하면 데이터베이스 개체를 쉽게 직접 디버그할 수 있습니다. DDD (직접 데이터베이스 디버깅) 기능을 사용 하 여 Northwind 데이터베이스의 `Products_SelectByCategoryID` 저장 프로시저를 한 단계씩 실행 하는 방법을 살펴보겠습니다. 이름에서 알 때 `Products_SelectByCategoryID`는 특정 범주에 대 한 제품 정보를 반환 합니다. [형식화 된 데이터 집합의 tableadapter 자습서에 대 한 기존 저장 프로시저를 사용 하](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) 여 생성 되었습니다. 먼저 서버 탐색기로 이동 하 여 Northwind 데이터베이스 노드를 확장 합니다. 그런 다음 저장 프로시저 폴더로 드릴 다운 하 고 `Products_SelectByCategoryID` 저장 프로시저를 마우스 오른쪽 단추로 클릭 한 다음 상황에 맞는 메뉴에서 저장 프로시저 한 단계씩 코드 실행 옵션을 선택 합니다. 그러면 디버거가 시작 됩니다.

`Products_SelectByCategoryID` 저장 프로시저에는 `@CategoryID` 입력 매개 변수가 필요 하므로이 값을 입력 하 라는 메시지가 표시 됩니다. 음료에 대 한 정보를 반환 하는 1을 입력 합니다.

![@CategoryID 매개 변수에 값 1을 사용 합니다.](debugging-stored-procedures-cs/_static/image1.png)

**그림 1**: `@CategoryID` 매개 변수에 값 1을 사용 합니다.

`@CategoryID` 매개 변수에 대 한 값을 제공 하면 저장 프로시저가 실행 됩니다. 그러나 실행이 완료 될 때까지 실행 되지 않고 디버거는 첫 번째 문에서 실행을 중단 합니다. 여백에 있는 노란색 화살표를 참고 하 여 저장 프로시저의 현재 위치를 나타냅니다. 조사식 창를 통해 또는 저장 프로시저에서 매개 변수 이름을 마우스로 가리키면 매개 변수 값을 보고 편집할 수 있습니다.

[저장 프로시저의 첫 번째 문에서 디버거가 중지 된 ![](debugging-stored-procedures-cs/_static/image3.png)](debugging-stored-procedures-cs/_static/image2.png)

**그림 2**: 디버거가 저장 프로시저의 첫 번째 문에서 중지 되었습니다 ([전체 크기 이미지를 보려면 클릭](debugging-stored-procedures-cs/_static/image4.png)).

저장 프로시저를 한 번에 하나씩 단계별로 실행 하려면 도구 모음에서 프로시저 단위 실행 단추를 클릭 하거나 F10 키를 누릅니다. `Products_SelectByCategoryID` 저장 프로시저에는 단일 `SELECT` 문이 포함 되어 있으므로 F10 키를 누르면 단일 문을 한 단계씩 실행 하 고 저장 프로시저의 실행을 완료 합니다. 저장 프로시저가 완료 된 후에는 해당 출력이 출력 창에 표시 되 고 디버거가 종료 됩니다.

> [!NOTE]
> T-sql 디버깅은 문 수준에서 발생 합니다. `SELECT` 문을 한 단계씩 실행할 수 없습니다.

## <a name="step-2-configuring-the-website-for-application-debugging"></a>2 단계: 응용 프로그램 디버깅을 위한 웹 사이트 구성

서버 탐색기에서 직접 저장 프로시저를 디버깅 하는 것이 편리 하지만 대부분의 시나리오에서는 ASP.NET 응용 프로그램에서 호출 될 때 저장 프로시저를 디버깅 하는 데 더 관심이 있습니다. Visual Studio 내에서 저장 프로시저에 중단점을 추가한 다음 ASP.NET 응용 프로그램의 디버깅을 시작할 수 있습니다. 응용 프로그램에서 중단점을 포함 하는 저장 프로시저를 호출 하면 실행이 중단점에서 중지 되 고 1 단계에서 수행한 것 처럼 저장 프로시저의 매개 변수 값을 보고 변경할 수 있으며 해당 문을 단계별로 실행할 수 있습니다.

응용 프로그램에서 호출 되는 저장 프로시저의 디버깅을 시작 하기 전에 ASP.NET 웹 응용 프로그램에 SQL Server 디버거와 통합 하도록 지시 해야 합니다. 솔루션 탐색기 (`ASPNET_Data_Tutorial_74_CS`)에서 웹 사이트 이름을 마우스 오른쪽 단추로 클릭 하 여 시작 합니다. 상황에 맞는 메뉴에서 속성 페이지 옵션을 선택 하 고, 왼쪽의 시작 옵션 항목을 선택 하 고, 디버거 섹션에서 SQL Server 확인란을 선택 합니다 (그림 3 참조).

[응용 프로그램 속성 페이지에서 SQL Server 확인란을 선택 ![.](debugging-stored-procedures-cs/_static/image6.png)](debugging-stored-procedures-cs/_static/image5.png)

**그림 3**: 응용 프로그램의 속성 페이지에서 SQL Server 확인란 확인 ([전체 크기 이미지를 보려면 클릭](debugging-stored-procedures-cs/_static/image7.png))

또한 연결 풀링을 사용 하지 않도록 설정 하기 위해 응용 프로그램에서 사용 하는 데이터베이스 연결 문자열을 업데이트 해야 합니다. 데이터베이스에 대 한 연결을 닫으면 해당 `SqlConnection` 개체가 사용 가능한 연결 풀에 배치 됩니다. 데이터베이스에 대 한 연결을 설정 하는 경우 새 연결을 만들고 설정 하지 않고이 풀에서 사용 가능한 연결 개체를 검색할 수 있습니다. 이러한 연결 개체 풀링은 성능 향상 이며 기본적으로 사용 하도록 설정 되어 있습니다. 그러나 디버깅 하는 경우에는 풀에서 가져온 연결을 사용할 때 디버깅 인프라가 올바르게 다시 설정 되지 않으므로 연결 풀링을 해제 하려고 합니다.

연결 풀링을 사용 하지 않도록 설정 하려면 `Pooling=false` 설정을 포함 하도록 `Web.config`에서 `NORTHWNDConnectionString`를 업데이트 합니다.

[!code-xml[Main](debugging-stored-procedures-cs/samples/sample1.xml)]

> [!NOTE]
> ASP.NET 응용 프로그램을 통해 SQL Server 디버깅을 완료 한 후에는 연결 문자열에서 `Pooling` 설정을 제거 하거나 `Pooling=true`으로 설정 하 여 연결 풀링을 복원 해야 합니다.

이 시점에서 ASP.NET 응용 프로그램은 Visual Studio에서 웹 응용 프로그램을 통해 호출 될 때 SQL Server 데이터베이스 개체를 디버깅할 수 있도록 구성 되었습니다. 이제 저장 프로시저에 중단점을 추가 하 고 디버깅을 시작 합니다.

## <a name="step-3-adding-a-breakpoint-and-debugging"></a>3 단계: 중단점 및 디버깅 추가

`Products_SelectByCategoryID` 저장 프로시저를 열고 적절 한 위치의 여백을 클릭 하거나 `SELECT` 문의 시작 부분에 커서를 놓고 F9를 눌러 `SELECT` 문의 시작 부분에 중단점을 설정 합니다. 그림 4에 나와 있는 것 처럼 중단점은 여백에 빨간색 원으로 표시 됩니다.

[Products_SelectByCategoryID 저장 프로시저에 중단점을 설정 ![](debugging-stored-procedures-cs/_static/image9.png)](debugging-stored-procedures-cs/_static/image8.png)

**그림 4**: `Products_SelectByCategoryID` 저장 프로시저에 중단점 설정 ([전체 크기 이미지를 보려면 클릭](debugging-stored-procedures-cs/_static/image10.png))

클라이언트 응용 프로그램을 통해 SQL database 개체를 디버깅 하려면 응용 프로그램 디버깅을 지원 하도록 데이터베이스를 구성 해야 합니다. 처음으로 중단점을 설정 하는 경우이 설정은 자동으로 전환 되지만 두 번 확인 하는 것이 좋습니다. 서버 탐색기에서 `NORTHWND.MDF` 노드를 마우스 오른쪽 단추로 클릭 합니다. 상황에 맞는 메뉴에는 응용 프로그램 디버깅 이라는 확인 된 메뉴 항목이 포함 되어야 합니다.

![응용 프로그램 디버깅 옵션이 활성화 되어 있는지 확인 합니다.](debugging-stored-procedures-cs/_static/image11.png)

**그림 5**: 응용 프로그램 디버깅 옵션이 설정 되어 있는지 확인

중단점을 설정 하 고 응용 프로그램 디버깅 옵션을 사용 하도록 설정 하면 ASP.NET 응용 프로그램에서 호출 될 때 저장 프로시저를 디버그할 준비가 됩니다. 디버그 메뉴로 이동 하 여 디버깅 시작을 선택 하거나, F5 키를 누르거나, 도구 모음에서 녹색 재생 아이콘을 클릭 하 여 디버거를 시작 합니다. 그러면 디버거가 시작 되 고 웹 사이트가 시작 됩니다.

[형식화 된 데이터 집합의 tableadapter 자습서에 대 한 기존 저장 프로시저를 사용 하](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) 여 `Products_SelectByCategoryID` 저장 프로시저를 만들었습니다. 해당 웹 페이지 (`~/AdvancedDAL/ExistingSprocs.aspx`)에는이 저장 프로시저가 반환 하는 결과를 표시 하는 GridView가 포함 되어 있습니다. 브라우저를 통해이 페이지를 방문 하세요. 페이지에 도달 하면 `Products_SelectByCategoryID` 저장 프로시저의 중단점이 적중 되 고 Visual Studio에 컨트롤이 반환 됩니다. 1 단계와 마찬가지로 저장 프로시저의 문을 단계별로 실행 하 고 매개 변수 값을 확인 하 고 수정할 수 있습니다.

[ExistingSprocs 페이지 ![는 먼저 음료를 표시 합니다.](debugging-stored-procedures-cs/_static/image13.png)](debugging-stored-procedures-cs/_static/image12.png)

**그림 6**: `ExistingSprocs.aspx` 페이지에는 먼저 음료 ([전체 크기 이미지를 보려면 클릭](debugging-stored-procedures-cs/_static/image14.png))가 표시 됩니다.

[저장 프로시저의 중단점에 도달 ![](debugging-stored-procedures-cs/_static/image16.png)](debugging-stored-procedures-cs/_static/image15.png)

**그림 7**: 저장 프로시저의 중단점에 도달 했습니다 ([전체 크기 이미지를 보려면 클릭](debugging-stored-procedures-cs/_static/image17.png)).

그림 7의 조사식 창에서 볼 수 있듯이 `@CategoryID` 매개 변수의 값은 1입니다. `ExistingSprocs.aspx` 페이지는 처음에 `CategoryID` 값이 1 인 음료 범주의 제품을 표시 하기 때문입니다. 드롭다운 목록에서 다른 범주를 선택 합니다. 이렇게 하면 다시 게시를 수행 하 고 `Products_SelectByCategoryID` 저장 프로시저를 다시 실행 합니다. 중단점은 다시 적중 되지만 이번에는 `@CategoryID` 매개 변수 s 값이 선택한 드롭다운 목록 항목인 s `CategoryID`를 반영 합니다.

[드롭다운 목록에서 다른 범주를 선택 ![](debugging-stored-procedures-cs/_static/image19.png)](debugging-stored-procedures-cs/_static/image18.png)

**그림 8**: 드롭다운 목록에서 다른 범주 선택 ([전체 크기 이미지를 보려면 클릭](debugging-stored-procedures-cs/_static/image20.png))

[![@CategoryID 매개 변수는 웹 페이지에서 선택한 범주를 반영 합니다.](debugging-stored-procedures-cs/_static/image22.png)](debugging-stored-procedures-cs/_static/image21.png)

**그림 9**: `@CategoryID` 매개 변수는 웹 페이지에서 선택한 범주를 반영 합니다 ([전체 크기 이미지를 보려면 클릭](debugging-stored-procedures-cs/_static/image23.png)).

> [!NOTE]
> `ExistingSprocs.aspx` 페이지를 방문할 때 `Products_SelectByCategoryID` 저장 프로시저의 중단점이 적중 되지 않는 경우 ASP.NET 응용 프로그램의 속성 페이지에 있는 디버거 섹션에서 SQL Server 확인란을 선택 했는지 확인 하 고, 연결 풀링이 비활성화 되었고, 데이터베이스 s 응용 프로그램 디버깅 옵션을 사용 하도록 설정 했는지 확인 합니다. 문제가 계속 되 면 Visual Studio를 다시 시작 하 고 다시 시도 하세요.

## <a name="debugging-t-sql-database-objects-on-remote-instances"></a>원격 인스턴스에서 T SQL Database 개체 디버깅

Visual Studio를 통해 데이터베이스 개체를 디버깅 하는 것은 SQL Server 데이터베이스 인스턴스가 Visual Studio와 같은 컴퓨터에 있는 경우에 매우 간단 합니다. 그러나 SQL Server와 Visual Studio가 서로 다른 컴퓨터에 있는 경우 모든 것이 제대로 작동 하려면 몇 가지 신중한 구성이 필요 합니다. 다음과 같은 두 가지 핵심 작업이 있습니다.

- ADO.NET을 통해 데이터베이스에 연결 하는 데 사용 되는 로그인이 `sysadmin` 역할에 속하는지 확인 합니다.
- 개발 컴퓨터에서 Visual Studio에 사용 되는 Windows 사용자 계정이 `sysadmin` 역할에 속하는 유효한 SQL Server 로그인 계정 인지 확인 합니다.

첫 번째 단계는 비교적 간단 합니다. 먼저 ASP.NET 응용 프로그램에서 데이터베이스에 연결 하는 데 사용 되는 사용자 계정을 확인 한 다음 SQL Server Management Studio에서 해당 로그인 계정을 `sysadmin` 역할에 추가 합니다.

두 번째 작업을 수행 하려면 응용 프로그램을 디버깅 하는 데 사용 하는 Windows 사용자 계정이 원격 데이터베이스에서 유효한 로그인 이어야 합니다. 그러나를 사용 하 여 워크스테이션에 로그온 한 Windows 계정이 SQL Server 올바른 로그인이 아닙니다. SQL Server에 특정 로그인 계정을 추가 하는 대신 일부 Windows 사용자 계정을 SQL Server 디버깅 계정으로 지정 하는 것이 더 좋습니다. 그런 다음 원격 SQL Server 인스턴스의 데이터베이스 개체를 디버깅 하려면 해당 Windows 로그인 계정의 자격 증명을 사용 하 여 Visual Studio를 실행 합니다.

예를 통해 항목을 명확 하 게 파악할 수 있습니다. Windows 도메인 내에 `SQLDebug` 이라는 Windows 계정이 있다고 가정 합니다. 이 계정은 원격 SQL Server 인스턴스에 유효한 로그인 및 `sysadmin` 역할의 멤버로 추가 해야 합니다. 그런 다음 Visual Studio에서 원격 SQL Server 인스턴스를 디버깅 하려면 `SQLDebug` 사용자로 Visual Studio를 실행 해야 합니다. 이 작업은 워크스테이션에서 로그 아웃 하 고, `SQLDebug`으로 다시 로그인 한 후 Visual Studio를 시작 하 여 수행할 수 있지만, 사용자의 자격 증명을 사용 하 여 워크스테이션에 로그인 한 다음 `runas.exe`를 사용 하 여 `SQLDebug` 사용자로 Visual Studio를 실행 하는 것이 더 간단 합니다. `runas.exe`를 사용 하면 다른 사용자 계정에서 특정 응용 프로그램을 실행할 수 있습니다. `SQLDebug`로 Visual Studio를 시작 하려면 명령줄에 다음 문을 입력 합니다.

[!code-console[Main](debugging-stored-procedures-cs/samples/sample2.cmd)]

이 프로세스에 대 한 자세한 설명은 [William R. Vaughn](http://betav.com/BLOG/billva/) s *Hitchhiker s Guide to Visual Studio 및 SQL Server, 7 번째 버전 및* [방법: 디버깅을 위한 SQL Server 권한 설정](https://msdn.microsoft.com/library/w1bhybwz(VS.80).aspx)을 참조 하세요.

> [!NOTE]
> 개발 컴퓨터에서 Windows XP 서비스 팩 2를 실행 하는 경우에는 원격 디버깅을 허용 하도록 인터넷 연결 방화벽을 구성 해야 합니다. [방법: SQL Server 2005 디버깅을 사용 하도록 설정](https://msdn.microsoft.com/library/s0fk6z6e(VS.80).aspx) 하는 방법에 대 한 자세한 내용은 Visual Studio 호스트 컴퓨터에서 (a) `Devenv.exe`를 예외 목록에 추가 하 고 TCP 135 포트를 열어야 합니다. 그리고 (b) 원격 (SQL) 컴퓨터에서 TCP 135 포트를 열고 예외 목록에 `sqlservr.exe`를 추가 해야 합니다. 도메인 정책에서 IPSec을 통해 네트워크 통신을 수행 해야 하는 경우 UDP 4500 및 UDP 500 포트를 열어야 합니다.

## <a name="summary"></a>요약

Visual Studio는 .NET 응용 프로그램 코드에 대 한 디버깅 지원을 제공 하는 것 외에도 SQL Server 2005에 대 한 다양 한 디버깅 옵션을 제공 합니다. 이 자습서에서는 직접 데이터베이스 디버깅 및 응용 프로그램 디버깅 이라는 두 가지 옵션을 살펴보았습니다. T-sql 데이터베이스 개체를 직접 디버깅 하려면 서버 탐색기을 통해 개체를 찾은 다음 마우스 오른쪽 단추로 클릭 하 고 한 단계씩 코드 실행을 선택 합니다. 그러면 디버거가 시작 되 고 데이터베이스 개체의 첫 번째 문에서 중단 됩니다. 이때 개체의 문을 단계별로 실행 하 고 매개 변수 값을 확인 하 고 수정할 수 있습니다. 1 단계에서는이 방법을 사용 하 여 `Products_SelectByCategoryID` 저장 프로시저를 한 단계씩 실행 했습니다.

응용 프로그램 디버깅을 사용 하면 데이터베이스 개체 내에서 직접 중단점을 설정할 수 있습니다. 중단점을 포함 하는 데이터베이스 개체가 클라이언트 응용 프로그램 (예: ASP.NET 웹 응용 프로그램)에서 호출 되 면 디버거가 실행 될 때 프로그램이 중단 됩니다. 응용 프로그램 디버깅은 특정 데이터베이스 개체의 호출을 발생 시키는 응용 프로그램 작업을 보다 명확 하 게 표시 하기 때문에 유용 합니다. 그러나 직접 데이터베이스 디버깅 보다 약간의 구성과 설정이 필요 합니다.

SQL Server 프로젝트를 통해 데이터베이스 개체를 디버그할 수도 있습니다. 다음 자습서에서 SQL Server 프로젝트를 사용 하 고이를 사용 하 여 관리 되는 데이터베이스 개체를 만들고 디버그 하는 방법을 살펴보겠습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

> [!div class="step-by-step"]
> [이전](protecting-connection-strings-and-other-configuration-information-cs.md)
> [다음](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs.md)
