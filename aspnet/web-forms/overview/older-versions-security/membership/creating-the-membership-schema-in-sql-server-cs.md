---
uid: web-forms/overview/older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs
title: SQL Server에서 멤버 자격 스키마 만들기 (C#) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 먼저 SqlMembershipProvider를 사용 하기 위해 필요한 스키마를 데이터베이스에 추가 하는 방법을 검토 합니다. 그 후에는 다음을 수행 합니다.
ms.author: riande
ms.date: 01/18/2008
ms.assetid: b4ac129d-1b8e-41ca-a38f-9b19d7c7bb0e
msc.legacyurl: /web-forms/overview/older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs
msc.type: authoredcontent
ms.openlocfilehash: 97623e7c13ab7799b9dadbb8e52be8e0cd99e252
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78464441"
---
# <a name="creating-the-membership-schema-in-sql-server-c"></a>SQL Server에서 멤버 자격 스키마 만들기(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_04_CS.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial04_MembershipSetup_cs.pdf)

> 이 자습서에서는 먼저 SqlMembershipProvider를 사용 하기 위해 필요한 스키마를 데이터베이스에 추가 하는 방법을 검토 합니다. 다음에는 스키마의 키 테이블을 살펴보고 목적과 중요도에 대해 설명 합니다. 이 자습서에서는 멤버 프레임 워크에서 사용 해야 하는 공급자를 ASP.NET 응용 프로그램에 알리는 방법에 대해 살펴봅니다.

## <a name="introduction"></a>소개

이전 두 자습서에서는 폼 인증을 사용 하 여 웹 사이트 방문자를 식별 하는 방법을 살펴보았습니다. 개발자는 폼 인증 프레임 워크를 사용 하 여 사용자를 웹 사이트에 쉽게 로그인 하 고 인증 티켓을 사용 하 여 페이지를 방문할 때마다 기억할 수 있습니다. `FormsAuthentication` 클래스에는 티켓을 생성 하 고 방문자의 쿠키에 추가 하는 메서드가 포함 되어 있습니다. `FormsAuthenticationModule`는 들어오는 모든 요청을 검사 하 고, 유효한 인증 티켓이 있는 요청에 대해 `GenericPrincipal` 및 `FormsIdentity` 개체를 만들어 현재 요청과 연결 합니다. 폼 인증은 단순히 로그인 할 때 방문자에 게 인증 티켓을 부여 하는 메커니즘이 며 후속 요청에서 사용자의 id를 확인 하기 위해 해당 티켓을 구문 분석 합니다. 사용자 계정을 지원 하기 위한 웹 응용 프로그램의 경우 여전히 사용자 저장소를 구현 하 고 자격 증명의 유효성을 검사 하 고, 새 사용자를 등록 하 고, 다른 사용자 계정 관련 작업을 등록 하는 기능을 추가 해야 합니다.

ASP.NET 2.0 이전에는 개발자가 이러한 모든 사용자 계정 관련 작업을 구현 하기 위한 후크 였습니다. 다행히 ASP.NET 팀은 이러한 단점을 인식 하 고 ASP.NET 2.0를 사용 하 여 멤버 자격 프레임 워크를 도입 했습니다. 멤버 프레임 프레임 워크는 핵심 사용자 계정 관련 작업을 수행 하기 위한 프로그래밍 인터페이스를 제공 하는 .NET Framework의 클래스 집합입니다. 이 프레임 워크는 개발자가 사용자 지정 된 구현을 표준화 된 API에 연결할 수 있도록 하는 [공급자 모델](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)위에 빌드됩니다.

<a id="Tutorial1"> </a> [*보안 기본 및 ASP.NET 지원*](../introduction/security-basics-and-asp-net-support-cs.md) 자습서에 설명 된 대로 .NET Framework에는 [`ActiveDirectoryMembershipProvider`](https://msdn.microsoft.com/library/system.web.security.activedirectorymembershipprovider.aspx) 및 [`SqlMembershipProvider`](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx)의 두 가지 기본 제공 멤버 자격 공급자가 제공 됩니다. 이름에서 알 때 `SqlMembershipProvider`는 Microsoft SQL Server 데이터베이스를 사용자 저장소로 사용 합니다. 응용 프로그램에서이 공급자를 사용 하려면 저장소로 사용할 데이터베이스를 공급자에 게 알려 주어 야 합니다. 짐작할 수 있듯이 `SqlMembershipProvider`에는 사용자 저장소 데이터베이스에 특정 데이터베이스 테이블, 뷰 및 저장 프로시저가 포함 될 것으로 예상 됩니다. 이 예상 스키마를 선택한 데이터베이스에 추가 해야 합니다.

이 자습서에서는 먼저 `SqlMembershipProvider`를 사용 하기 위해 필요한 스키마를 데이터베이스에 추가 하는 기술에 대해 검토 합니다. 다음에는 스키마의 키 테이블을 살펴보고 목적과 중요도에 대해 설명 합니다. 이 자습서에서는 멤버 프레임 워크에서 사용 해야 하는 공급자를 ASP.NET 응용 프로그램에 알리는 방법에 대해 살펴봅니다.

이제 시작하겠습니다.

## <a name="step-1-deciding-where-to-place-the-user-store"></a>1 단계: 사용자 저장소를 보관할 위치 결정

ASP.NET 응용 프로그램의 데이터는 일반적으로 데이터베이스의 여러 테이블에 저장 됩니다. `SqlMembershipProvider` 데이터베이스 스키마를 구현 하는 경우에는 멤버 자격 스키마를 응용 프로그램 데이터와 같은 데이터베이스 또는 대체 데이터베이스에 배치할지 여부를 결정 해야 합니다.

다음과 같은 이유로 응용 프로그램 데이터와 동일한 데이터베이스에서 멤버 자격 스키마를 찾는 것이 좋습니다.

- **유지 관리** 데이터를 하나의 데이터베이스에 캡슐화 하는 응용 프로그램은 별도의 데이터베이스가 두 개인 응용 프로그램 보다 더 쉽게 이해 하 고 유지 관리 하 고 배포할 수 있습니다.
- **관계형 무결성** 응용 프로그램 테이블과 동일한 데이터베이스에 멤버 자격 관련 테이블을 배치 하 여 멤버 자격 관련 테이블 및 관련 응용 프로그램 테이블의 기본 키 사이에 [foreign key 제약 조건을](http://en.wikipedia.org/wiki/Foreign_key) 설정할 수 있습니다.

사용자 저장소와 응용 프로그램 데이터를 개별 데이터베이스로 분리 하는 것은 각각 별도의 데이터베이스를 사용 하지만 공통 사용자 저장소를 공유 해야 하는 여러 응용 프로그램이 있는 경우에만 적합 합니다.

### <a name="creating-a-database"></a>데이터베이스 만들기

두 번째 자습서에서 작성 한 응용 프로그램은 아직 데이터베이스를 필요로 하지 않았습니다. 그러나 사용자 저장소에 대 한 현재이 (가) 필요 합니다. 하나를 만든 다음 `SqlMembershipProvider` 공급자에 필요한 스키마 (2 단계 참조)에 추가 해 보겠습니다.

> [!NOTE]
> 이 자습서 시리즈 전체에서는 [Microsoft SQL Server 2005 Express Edition](https://msdn.microsoft.com/sql/Aa336346.aspx) 데이터베이스를 사용 하 여 응용 프로그램 테이블과 `SqlMembershipProvider` 스키마를 저장 합니다. 이러한 결정은 두 가지 이유로 수행 되었습니다. 첫 번째는 비용 없이 무료로 제공 됩니다. Express Edition은 SQL Server 2005의 가장 readably 액세스 가능한 버전입니다. 두 번째로 SQL Server 2005 Express Edition 데이터베이스를 웹 응용 프로그램의 `App_Data` 폴더에 직접 배치 하 여 하나의 ZIP 파일에 데이터베이스 및 웹 응용 프로그램을 cinch 하 고 특별 한 설치 지침 또는 구성 옵션 없이 다시 배포할 수 있습니다. Express Edition 버전의 SQL Server을 사용 하 여 수행 하는 것을 선호 하는 경우 무료로 사용할 수 있습니다. 단계는 사실상 동일 합니다. `SqlMembershipProvider` 스키마는 Microsoft SQL Server 2000 이상 버전에서 작동 합니다.

솔루션 탐색기에서 `App_Data` 폴더를 마우스 오른쪽 단추로 클릭 하 고 새 항목 추가를 선택 합니다. 프로젝트에 `App_Data` 폴더가 표시 되지 않으면 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 ASP.NET 폴더 추가를 선택 하 고 `App_Data`를 선택 합니다. 새 항목 추가 대화 상자에서 `SecurityTutorials.mdf`라는 새 SQL Database을 추가 하도록 선택 합니다. 이 자습서에서는이 데이터베이스에 `SqlMembershipProvider` 스키마를 추가 합니다. 이후 자습서에서는 응용 프로그램 데이터를 캡처하기 위해 추가 테이블을 만듭니다.

[![새 SQL Database를 App_Data 폴더에 추가 합니다.](creating-the-membership-schema-in-sql-server-cs/_static/image2.png)](creating-the-membership-schema-in-sql-server-cs/_static/image1.png)

**그림 1**: `App_Data` 폴더에 `SecurityTutorials.mdf` 데이터베이스 라는 새 SQL Database 추가 ([전체 크기 이미지를 보려면 클릭](creating-the-membership-schema-in-sql-server-cs/_static/image3.png))

`App_Data` 폴더에 데이터베이스를 추가 하면 데이터베이스 탐색기 뷰에 자동으로 포함 됩니다. Express Edition 버전의 Visual Studio에서는 데이터베이스 탐색기를 서버 탐색기 이라고 합니다. 데이터베이스 탐색기로 이동 하 여 바로 추가 된 `SecurityTutorials` 데이터베이스를 확장 합니다. 화면에 데이터베이스 탐색기 표시 되지 않으면 보기 메뉴로 이동 하 여 데이터베이스 탐색기를 선택 하거나 Ctrl + Alt + S를 누릅니다. 그림 2에 나와 있는 것 처럼 `SecurityTutorials` 데이터베이스는 비어 있습니다. 즉, 테이블, 뷰 및 저장 프로시저는 포함 되지 않습니다.

[SecurityTutorials 데이터베이스가 현재 비어 ![](creating-the-membership-schema-in-sql-server-cs/_static/image5.png)](creating-the-membership-schema-in-sql-server-cs/_static/image4.png)

**그림 2**: `SecurityTutorials` 데이터베이스가 현재 비어 있습니다 ([전체 크기 이미지를 보려면 클릭](creating-the-membership-schema-in-sql-server-cs/_static/image6.png)).

## <a name="step-2-adding-thesqlmembershipproviderschema-to-the-database"></a>2 단계: 데이터베이스에`SqlMembershipProvider`스키마 추가

`SqlMembershipProvider`를 사용 하려면 특정 테이블, 뷰 및 저장 프로시저 집합을 사용자 저장소 데이터베이스에 설치 해야 합니다. 이러한 필수 데이터베이스 개체는 [`aspnet_regsql.exe` 도구](https://msdn.microsoft.com/library/ms229862.aspx)를 사용 하 여 추가할 수 있습니다. 이 파일은 `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\` 폴더에 있습니다.

> [!NOTE]
> `aspnet_regsql.exe` 도구는 명령줄 기능과 그래픽 사용자 인터페이스를 모두 제공 합니다. 그래픽 인터페이스는 보다 사용자에 게 친숙 하며이 자습서에서 살펴볼 것입니다. 명령줄 인터페이스는 빌드 스크립트 또는 자동화 된 테스트 시나리오에서와 같이 `SqlMembershipProvider` 스키마의 추가를 자동화 해야 하는 경우에 유용 합니다.

`aspnet_regsql.exe` 도구는 지정 된 SQL Server 데이터베이스에 *ASP.NET 응용 프로그램 서비스* 를 추가 하거나 제거 하는 데 사용 됩니다. ASP.NET 응용 프로그램 서비스는 기타 ASP.NET 2.0 프레임 워크에 대 한 SQL 기반 공급자의 스키마와 함께 `SqlMembershipProvider` 및 `SqlRoleProvider`에 대 한 스키마를 포함 합니다. `aspnet_regsql.exe` 도구에 두 가지 비트 정보를 제공 해야 합니다.

- 응용 프로그램 서비스를 추가 하거나 제거할지 여부를 지정 합니다.
- 응용 프로그램 서비스 스키마를 추가 하거나 제거할 데이터베이스입니다.

사용할 데이터베이스에 대 한 프롬프트에서 `aspnet_regsql.exe` 도구는 데이터베이스가 있는 서버의 이름, 데이터베이스에 연결 하기 위한 보안 자격 증명 및 데이터베이스 이름을 제공 하도록 요청 합니다. SQL Server Express Edition 이외의 버전을 사용 하는 경우이 정보는 ASP.NET 웹 페이지를 통해 데이터베이스를 사용할 때 연결 문자열을 통해 제공 해야 하는 정보 이기 때문에 이미 알고 있어야 합니다. 그러나 `App_Data` 폴더에 SQL Server 2005 Express Edition 데이터베이스를 사용 하는 경우 서버와 데이터베이스 이름을 결정 하는 것은 더 많은 관련이 있습니다.

다음 섹션에서는 `App_Data` 폴더의 SQL Server 2005 Express Edition 데이터베이스에 대 한 서버 및 데이터베이스 이름을 지정 하는 간단한 방법을 검사 합니다. SQL Server 2005 Express Edition 사용 하지 않는 경우 애플리케이션 서비스 섹션 설치로 건너뛸 수 있습니다.

### <a name="determining-the-server-and-database-name-for-a-sql-server-2005-express-edition-database-in-theapp_datafolder"></a>`App_Data`폴더의 SQL Server 2005 Express Edition 데이터베이스에 대 한 서버 및 데이터베이스 이름 확인

`aspnet_regsql.exe` 도구를 사용 하려면 서버 및 데이터베이스 이름을 알아야 합니다. 서버 이름이 `localhost\InstanceName`입니다. *인스턴스* 이름이 (가) `SQLExpress`될 가능성이 높습니다. 그러나 SQL Server 2005 Express Edition를 수동으로 설치한 경우 (즉, Visual Studio를 설치 하는 동안 자동으로 설치 하지 않은 경우) 다른 인스턴스 이름을 선택할 수 있습니다.

데이터베이스 이름을 확인 하는 것이 다소 까다롭습니다. `App_Data` 폴더의 데이터베이스에는 일반적으로 데이터베이스 파일에 대 한 경로와 함께 [전역 고유 식별자](http://en.wikipedia.org/wiki/Globally_Unique_Identifier) 가 포함 된 데이터베이스 이름이 있습니다. `aspnet_regsql.exe`를 통해 응용 프로그램 서비스 스키마를 추가 하려면이 데이터베이스 이름을 결정 해야 합니다.

데이터베이스 이름을 확인 하는 가장 쉬운 방법은 SQL Server Management Studio을 통해 확인 하는 것입니다. SQL Server Management Studio는 SQL Server 2005 데이터베이스를 관리 하기 위한 그래픽 인터페이스를 제공 하지만 SQL Server 2005 Express 버전에는 제공 되지 않습니다. SQL Server Management Studio 무료 Express 버전을 [다운로드할 수](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en) 있는 것이 좋습니다.

> [!NOTE]
> SQL Server 2005의 Express 버전이 아닌 버전이 바탕 화면에 설치 되어 있는 경우 Management Studio의 전체 버전이 설치 될 가능성이 높습니다. Express Edition에 대해 아래에 설명 된 것과 동일한 단계에 따라 전체 버전을 사용 하 여 데이터베이스 이름을 결정할 수 있습니다.

Visual Studio를 닫아 시작 하 여 데이터베이스 파일에서 Visual Studio에 적용 되는 모든 잠금이 닫혀 있는지 확인 합니다. 그런 다음 SQL Server Management Studio를 시작 하 고 SQL Server 2005 Express Edition에 대 한 `localhost\InstanceName` 데이터베이스에 연결 합니다. 앞에서 설명한 것 처럼 인스턴스 이름이 `SQLExpress`될 가능성이 있습니다. 인증 옵션에 대해 Windows 인증을 선택 합니다.

[SQL Server 2005 Express Edition 인스턴스에 연결 ![](creating-the-membership-schema-in-sql-server-cs/_static/image8.png)](creating-the-membership-schema-in-sql-server-cs/_static/image7.png)

**그림 3**: SQL Server 2005 Express Edition 인스턴스에 연결 ([전체 크기 이미지를 보려면 클릭](creating-the-membership-schema-in-sql-server-cs/_static/image9.png))

SQL Server 2005 Express Edition 인스턴스에 연결한 후 Management Studio는 데이터베이스, 보안 설정, 서버 개체 등에 대 한 폴더를 표시 합니다. 데이터베이스 탭을 확장 하면 `SecurityTutorials.mdf` 데이터베이스가 데이터베이스 인스턴스에 등록 *되지* 않은 것을 확인할 수 있습니다. 먼저 데이터베이스를 연결 해야 합니다.

데이터베이스 폴더를 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 연결을 선택 합니다. 그러면 데이터베이스 연결 대화 상자가 표시 됩니다. 여기에서 추가 단추를 클릭 하 고 `SecurityTutorials.mdf` 데이터베이스를 찾은 다음 확인을 클릭 합니다. 그림 4에서는 `SecurityTutorials.mdf` 데이터베이스를 선택한 후 데이터베이스 연결 대화 상자를 보여 줍니다. 그림 5는 데이터베이스가 성공적으로 연결 된 후의 개체 탐색기 Management Studio 보여 줍니다.

[SecurityTutorials .mdf 데이터베이스를 연결 ![](creating-the-membership-schema-in-sql-server-cs/_static/image11.png)](creating-the-membership-schema-in-sql-server-cs/_static/image10.png)

**그림 4**: `SecurityTutorials.mdf` 데이터베이스 연결 ([전체 크기 이미지를 보려면 클릭](creating-the-membership-schema-in-sql-server-cs/_static/image12.png))

[SecurityTutorials를 ![데이터베이스 폴더에 .mdf 데이터베이스가 표시 됩니다.](creating-the-membership-schema-in-sql-server-cs/_static/image14.png)](creating-the-membership-schema-in-sql-server-cs/_static/image13.png)

**그림 5**: 데이터베이스 폴더에 `SecurityTutorials.mdf` 데이터베이스 표시 ([전체 크기 이미지를 보려면 클릭](creating-the-membership-schema-in-sql-server-cs/_static/image15.png))

그림 5와 같이 `SecurityTutorials.mdf` 데이터베이스에는 대신 abstruse 이름이 있습니다. 더 기억 하기 쉬운 (형식) 이름으로 변경해 보겠습니다. 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 이름 바꾸기를 선택한 다음 이름을 `SecurityTutorialsDatabase`로 바꿉니다. 이는 파일 이름을 변경 하지 않습니다. 데이터베이스에서 SQL Server를 식별 하는 데 사용 하는 이름입니다.

[SecurityTutorialsDatabase로 데이터베이스 이름 바꾸기 ![](creating-the-membership-schema-in-sql-server-cs/_static/image17.png)](creating-the-membership-schema-in-sql-server-cs/_static/image16.png)

**그림 6**: `SecurityTutorialsDatabase`로 데이터베이스 이름 바꾸기 ([전체 크기 이미지를 보려면 클릭](creating-the-membership-schema-in-sql-server-cs/_static/image18.png))

이 시점에서 `SecurityTutorials.mdf` 데이터베이스 파일에 대 한 서버 및 데이터베이스 이름 (각각 `localhost\InstanceName` 및 `SecurityTutorialsDatabase`)을 알 수 있습니다. 이제 `aspnet_regsql.exe` 도구를 통해 응용 프로그램 서비스를 설치할 준비가 되었습니다.

### <a name="installing-the-application-services"></a>애플리케이션 서비스 설치

`aspnet_regsql.exe` 도구를 시작 하려면 시작 메뉴로 이동 하 여 실행을 선택 합니다. 텍스트 상자에 `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\aspnet_regsql.exe`를 입력 하 고 확인을 클릭 합니다. 또는 Windows 탐색기를 사용 하 여 적절 한 폴더로 드릴 다운 하 고 `aspnet_regsql.exe` 파일을 두 번 클릭 합니다. 두 방법 모두 동일한 결과를 발생 합니다.

명령줄 인수 없이 `aspnet_regsql.exe` 도구를 실행 하면 ASP.NET SQL Server 설치 마법사 그래픽 사용자 인터페이스가 시작 됩니다. 이 마법사를 사용 하면 지정 된 데이터베이스에서 ASP.NET 응용 프로그램 서비스를 쉽게 추가 하거나 제거할 수 있습니다. 그림 7에 표시 된 마법사의 첫 번째 화면에서는 도구의 용도를 설명 합니다.

[ASP.NET SQL Server 설치 마법사 ![사용 하 여 멤버 자격 스키마를 추가 합니다.](creating-the-membership-schema-in-sql-server-cs/_static/image20.png)](creating-the-membership-schema-in-sql-server-cs/_static/image19.png)

**그림 7**: ASP.NET SQL Server 설치 마법사를 사용 하 여 멤버 자격 스키마 추가 ([전체 크기 이미지를 보려면 클릭](creating-the-membership-schema-in-sql-server-cs/_static/image21.png))

마법사의 두 번째 단계에서는 응용 프로그램 서비스를 추가할지 아니면 제거할지를 묻는 메시지를 표시 합니다. `SqlMembershipProvider`에 필요한 테이블, 뷰 및 저장 프로시저를 추가 하려고 하므로 응용 프로그램 서비스에 대 한 SQL Server 구성 옵션을 선택 합니다. 나중에이 스키마를 데이터베이스에서 제거 하려면이 마법사를 다시 실행 하 고, 대신 기존 데이터베이스에서 응용 프로그램 서비스 정보 제거 옵션을 선택 합니다.

[![애플리케이션 서비스에 대 한 SQL Server 구성 옵션을 선택 합니다.](creating-the-membership-schema-in-sql-server-cs/_static/image23.png)](creating-the-membership-schema-in-sql-server-cs/_static/image22.png)

**그림 8**: 애플리케이션 서비스에 대 한 SQL Server 구성 옵션 선택 ([전체 크기 이미지를 보려면 클릭](creating-the-membership-schema-in-sql-server-cs/_static/image24.png))

세 번째 단계에서는 데이터베이스 정보 (서버 이름, 인증 정보 및 데이터베이스 이름)를 묻는 메시지를 표시 합니다. 이 자습서와 함께 다음을 수행 하 여 `App_Data`에 `SecurityTutorials.mdf` 데이터베이스를 추가 하 고 `localhost\InstanceName`에 연결한 후 `SecurityTutorialsDatabase`로 이름을 바꾼 후에는 다음 값을 사용 합니다.

- 서버: `localhost\InstanceName`
- Windows 인증
- 데이터베이스: `SecurityTutorialsDatabase`

[데이터베이스 정보를 입력 ![](creating-the-membership-schema-in-sql-server-cs/_static/image26.png)](creating-the-membership-schema-in-sql-server-cs/_static/image25.png)

**그림 9**: 데이터베이스 정보 입력 ([전체 크기 이미지를 보려면 클릭](creating-the-membership-schema-in-sql-server-cs/_static/image27.png))

데이터베이스 정보를 입력 한 후 다음을 클릭 합니다. 마지막 단계에서는 수행 되는 단계를 요약 합니다. 다음을 클릭 하 여 응용 프로그램 서비스를 설치한 후 마침을 클릭 하 여 마법사를 완료 합니다.

> [!NOTE]
> Management Studio를 사용 하 여 데이터베이스를 연결 하 고 데이터베이스 파일의 이름을 바꾼 경우에는 데이터베이스를 분리 하 고 Visual Studio를 다시 열기 전에 Management Studio를 닫아야 합니다. `SecurityTutorialsDatabase` 데이터베이스를 분리 하려면 데이터베이스 이름을 마우스 오른쪽 단추로 클릭 하 고 작업 메뉴에서 분리를 선택 합니다.

마법사가 완료 되 면 Visual Studio로 돌아가서 데이터베이스 탐색기로 이동 합니다. 테이블 폴더를 확장합니다. 이름이 `aspnet_`접두사로 시작 하는 일련의 테이블이 표시 됩니다. 마찬가지로 뷰 및 저장 프로시저 폴더 아래에서 다양 한 뷰 및 저장 프로시저를 찾을 수 있습니다. 이러한 데이터베이스 개체는 응용 프로그램 서비스 스키마를 구성 합니다. 3 단계에서 멤버 자격 및 역할 관련 데이터베이스 개체를 살펴보겠습니다.

[여러 테이블, 뷰 및 저장 프로시저가 데이터베이스에 추가 ![](creating-the-membership-schema-in-sql-server-cs/_static/image29.png)](creating-the-membership-schema-in-sql-server-cs/_static/image28.png)

**그림 10**: 다양 한 테이블, 뷰 및 저장 프로시저가 데이터베이스에 추가 되었습니다 ([전체 크기 이미지를 보려면 클릭](creating-the-membership-schema-in-sql-server-cs/_static/image30.png)).

> [!NOTE]
> `aspnet_regsql.exe` 도구의 그래픽 사용자 인터페이스는 전체 응용 프로그램 서비스 스키마를 설치 합니다. 그러나 명령줄에서 `aspnet_regsql.exe`를 실행 하는 경우 설치 하거나 제거할 특정 응용 프로그램 서비스 구성 요소를 지정할 수 있습니다. 따라서 `SqlMembershipProvider` 및 `SqlRoleProvider` 공급자에 필요한 테이블, 뷰 및 저장 프로시저만 추가 하려면 명령줄에서 `aspnet_regsql.exe`를 실행 합니다. 또는 `aspnet_regsql.exe`에서 사용 하는 T-sql 만들기 스크립트의 적절 한 하위 집합을 수동으로 실행할 수 있습니다. 이러한 스크립트는 `InstallCommon.sql`,`InstallMembership.sql`,`InstallRoles.sql`, `InstallProfile.sql`,`InstallSqlState.sql`등과 같은 이름을 가진 `WINDIR%\Microsoft.Net\Framework\v2.0.50727\` 폴더에 있습니다.

이 시점에서 `SqlMembershipProvider`에 필요한 데이터베이스 개체를 만들었습니다. 그러나 `SqlMembershipProvider` (`ActiveDirectoryMembershipProvider`)를 사용 해야 하 고 `SqlMembershipProvider` `SecurityTutorials` 데이터베이스를 사용 해야 한다는 것을 멤버 자격 프레임 워크에 지시 해야 합니다. 사용할 공급자를 지정 하는 방법 및 4 단계에서 선택한 공급자의 설정을 사용자 지정 하는 방법을 살펴보겠습니다. 하지만 먼저 방금 만든 데이터베이스 개체를 자세히 살펴보겠습니다.

## <a name="step-3-a-look-at-the-schemas-core-tables"></a>3 단계: 스키마의 핵심 테이블 살펴보기

ASP.NET 응용 프로그램의 멤버 자격 및 역할 프레임 워크를 사용 하는 경우 구현 세부 정보는 공급자에 의해 캡슐화 됩니다. 이후 자습서에서는 .NET Framework의 `Membership` 및 `Roles` 클래스를 통해 이러한 프레임 워크와 상호 작용 합니다. 이러한 높은 수준의 Api를 사용 하는 경우 실행 되는 쿼리, `SqlMembershipProvider`에서 수정 되는 테이블 및 `SqlRoleProvider`와 같은 하위 수준 세부 정보를 고려 하지 않아도 됩니다.

이를 고려 하 여 2 단계에서 만든 데이터베이스 스키마를 탐색 하지 않고도 멤버 자격과 역할 프레임 워크를 안전 하 게 사용할 수 있습니다. 그러나 응용 프로그램 데이터를 저장 하는 테이블을 만들 때 사용자 또는 역할과 관련 된 엔터티를 만들어야 할 수 있습니다. 응용 프로그램 데이터 테이블과 2 단계에서 만든 테이블 사이에 foreign key 제약 조건을 설정할 때 `SqlMembershipProvider` 및 `SqlRoleProvider` 스키마를 잘 이해 하는 데 도움이 됩니다. 또한 드문 경우 지만 사용자 및 역할 저장소와 `Membership` 또는 `Roles` 클래스 대신 데이터베이스 수준에서 직접 인터페이스를 사용 해야 할 수도 있습니다.

### <a name="partitioning-the-user-store-into-applications"></a>사용자 저장소를 응용 프로그램으로 분할

멤버 자격 및 역할 프레임 워크는 여러 응용 프로그램 간에 단일 사용자 및 역할 저장소를 공유할 수 있도록 설계 되었습니다. 멤버 자격 또는 역할 프레임 워크를 사용 하는 ASP.NET 응용 프로그램은 사용할 응용 프로그램 파티션을 지정 해야 합니다. 간단히 말해서 여러 웹 응용 프로그램에서 동일한 사용자 및 역할 저장소를 사용할 수 있습니다. 그림 11에서는 HRSite, CustomerSite 및 SalesSite의 세 가지 응용 프로그램으로 분할 된 사용자 및 역할 저장소를 보여 줍니다. 이러한 세 웹 응용 프로그램은 각각 고유한 사용자 및 역할을 포함 하지만 모두 동일한 데이터베이스 테이블에 사용자 계정 및 역할 정보를 실제로 저장 합니다.

[![사용자 계정이 여러 응용 프로그램에서 분할 될 수 있습니다.](creating-the-membership-schema-in-sql-server-cs/_static/image32.png)](creating-the-membership-schema-in-sql-server-cs/_static/image31.png)

**그림 11**: 사용자 계정이 여러 응용 프로그램에서 분할 될 수 있습니다 ([전체 크기 이미지를 보려면 클릭](creating-the-membership-schema-in-sql-server-cs/_static/image33.png)).

`aspnet_Applications` 테이블은 이러한 파티션을 정의 하는 것입니다. 데이터베이스를 사용 하 여 사용자 계정 정보를 저장 하는 각 응용 프로그램은이 테이블의 행으로 표시 됩니다. `aspnet_Applications` 테이블에는 `ApplicationId`, `ApplicationName`, `LoweredApplicationName`및 `Description`이라는 4 개의 열이 있습니다. `ApplicationId`은 [`uniqueidentifier`](https://msdn.microsoft.com/library/ms187942.aspx) 유형이 며 테이블의 기본 키입니다. `ApplicationName`은 각 응용 프로그램에 대 한 고유한 이름을 제공 합니다.

다른 멤버 자격 및 역할 관련 테이블은 `aspnet_Applications`의 `ApplicationId` 필드로 다시 연결 됩니다. 예를 들어 각 사용자 계정에 대 한 레코드를 포함 하는 `aspnet_Users` 테이블에는 `ApplicationId` 외래 키 필드가 있습니다. `aspnet_Roles` 테이블에 대 한 ditto입니다. 이러한 테이블의 `ApplicationId` 필드는 사용자 계정 또는 역할이 속한 응용 프로그램 파티션을 지정 합니다.

### <a name="storing-user-account-information"></a>사용자 계정 정보 저장

사용자 계정 정보는 `aspnet_Users` 및 `aspnet_Membership`의 두 테이블에 있습니다. `aspnet_Users` 테이블에는 필수 사용자 계정 정보를 저장 하는 필드가 포함 되어 있습니다. 가장 관련성이 높은 세 열은 다음과 같습니다.

- `UserId`
- `UserName`
- `ApplicationId`

`UserId`은 기본 키 (`uniqueidentifier`형식)입니다. `UserName` `nvarchar(256)` 형식이 며, 암호와 함께 사용자의 자격 증명을 구성 합니다. 사용자의 암호는 `aspnet_Membership` 테이블에 저장 됩니다. `ApplicationId` 사용자 계정을 `aspnet_Applications`의 특정 응용 프로그램에 연결 합니다. `UserName` 및 `ApplicationId` 열에는 복합 [`UNIQUE` 제약 조건이](https://msdn.microsoft.com/library/ms191166.aspx) 있습니다. 이렇게 하면 지정 된 응용 프로그램에서 각 사용자 이름이 고유 하지만 다른 응용 프로그램에서 동일한 `UserName`를 사용할 수 있습니다.

`aspnet_Membership` 테이블에는 사용자의 암호, 전자 메일 주소, 마지막 로그인 날짜 및 시간과 같은 추가 사용자 계정 정보가 포함 되어 있습니다. `aspnet_Users`와 `aspnet_Membership` 테이블의 레코드 간에는 일 대 일 관계가 있습니다. 이 관계는 테이블의 기본 키로 사용 되는 `aspnet_Membership``UserId` 필드에 의해 보장 됩니다. `aspnet_Users` 테이블과 마찬가지로 `aspnet_Membership`에는이 정보를 특정 응용 프로그램 파티션에 연결 하는 `ApplicationId` 필드가 포함 됩니다.

### <a name="securing-passwords"></a>암호 보안

암호 정보는 `aspnet_Membership` 테이블에 저장 됩니다. `SqlMembershipProvider`를 사용 하 여 다음 세 가지 방법 중 하나를 사용 하 여 데이터베이스에 암호를 저장할 수 있습니다.

- **Clear** -암호가 데이터베이스에 일반 텍스트로 저장 됩니다. 이 옵션을 사용 하지 않는 것이 좋습니다. 데이터베이스가 손상 된 경우, 백 도어를 검색 하는 해커 또는 데이터베이스 액세스 권한이 있는 불만 직원에 의해 it를 받을 수 있습니다. 모든 단일 사용자의 자격 증명이 사용 됩니다.
- **해시** 된 암호는 단방향 해시 알고리즘 및 임의로 생성 된 솔트 값을 사용 하 여 해시 됩니다. 이 해시 된 값 (솔트와 함께)은 데이터베이스에 저장 됩니다.
- **암호화** 됨-암호화 된 버전의 암호가 데이터베이스에 저장 됩니다.

사용 되는 암호 저장소 기술은 `Web.config`에 지정 된 `SqlMembershipProvider` 설정에 따라 달라 집니다. 4 단계에서 `SqlMembershipProvider` 설정을 사용자 지정 하는 방법을 살펴보겠습니다. 기본 동작은 암호의 해시를 저장 하는 것입니다.

암호 저장을 담당 하는 열은 `Password`, `PasswordFormat`및 `PasswordSalt`입니다. `PasswordFormat`은 암호를 저장 하는 데 사용 되는 기술을 나타내는 값을 갖는 `int` 형식의 필드입니다. 0은 암호를 저장 하는 데 사용 됩니다. 1은 해시 됩니다. 2는 암호화 됩니다. 사용 된 암호 저장소 기술에 관계 없이 임의로 생성 된 문자열이 `PasswordSalt`에 할당 됩니다. `PasswordSalt` 값은 암호의 해시를 계산 하는 경우에만 사용 됩니다. 마지막으로, `Password` 열에는 실제 암호 데이터, 일반 텍스트 암호, 암호 해시 또는 암호화 된 암호가 포함 됩니다.

표 1에서는 암호 MySecret을 저장할 때 다양 한 저장소 기술에 대해 이러한 세 개의 열이 어떻게 표시 될 수 있는지를 보여 줍니다. .

| **저장소 기술&lt;\_o3a\_p/&gt;** | **암호&lt;\_o3a\_p/&gt;** | **PasswordFormat&lt;\_o3a\_p/&gt;** | **PasswordSalt&lt;\_o3a\_p/&gt;** |
| --- | --- | --- | --- |
| 지우기 | MySecret! | 0 | tTnkPlesqissc2y2SMEygA== |
| 된 | 2oXm6sZHWbTHFgjgkGQsc2Ec9ZM= | 1 | wFgjUfhdUFOCKQiI61vtiQ== |
| 암호화 | 62RZgDvhxykkqsMchZ0Yly7HS6onhpaoCYaRxV8g0F4CW56OXUU3e7Inza9j9BKp | 2 | LSRzhGS/aa/oqAXGLHJNBw== |

**표 1**: 암호 Mysecret을 저장할 때 암호 관련 필드에 대 한 예제 값

> [!NOTE]
> `SqlMembershipProvider`에서 사용 하는 특정 암호화 또는 해시 알고리즘은 `<machineKey>` 요소의 설정에 따라 결정 됩니다. <a id="Tutorial3"> </a> [*폼 인증 구성 및 고급 항목*](../introduction/forms-authentication-configuration-and-advanced-topics-cs.md) 자습서의 3 단계에서이 구성 요소에 대해 설명 했습니다.

### <a name="storing-roles-and-role-associations"></a>역할 및 역할 연결 저장

개발자는 역할 프레임 워크를 사용 하 여 역할 집합을 정의 하 고 역할에 속하는 사용자를 지정할 수 있습니다. 이 정보는 `aspnet_Roles` 및 `aspnet_UsersInRoles`테이블을 통해 데이터베이스에 캡처됩니다. `aspnet_Roles` 테이블의 각 레코드는 특정 응용 프로그램에 대 한 역할을 나타냅니다. `aspnet_Users` 테이블과 매우 유사 하 게 `aspnet_Roles` 테이블에는 토론에 관련 된 세 개의 열이 있습니다.

- `RoleId`
- `RoleName`
- `ApplicationId`

`RoleId`은 기본 키 (`uniqueidentifier`형식)입니다. `RoleName`는 `nvarchar(256)` 형식입니다. 및 `ApplicationId` 사용자 계정을 `aspnet_Applications`의 특정 응용 프로그램에 연결 합니다. `RoleName` 및 `ApplicationId` 열에 복합 `UNIQUE` 제약 조건이 있으므로 지정 된 응용 프로그램에서 각 역할 이름이 고유한 지 확인 합니다.

`aspnet_UsersInRoles` 테이블은 사용자와 역할 간의 매핑으로 사용 됩니다. `UserId`와 `RoleId` 열이 두 개 뿐 이며 함께 복합 기본 키를 구성 합니다.

## <a name="step-4-specifying-the-provider-and-customizing-its-settings"></a>4 단계: 공급자 지정 및 해당 설정 사용자 지정

멤버 자격 및 역할 프레임 워크와 같이 공급자 모델을 지 원하는 모든 프레임 워크는 구현에 대 한 세부 정보를 제공 하 고 대신 해당 역할을 공급자 클래스에 위임 합니다. 멤버 프레임 프레임 워크의 경우 `Membership` 클래스는 사용자 계정을 관리 하기 위한 API를 정의 하지만 사용자 저장소와 직접 상호 작용 하지는 않습니다. 대신, `Membership` 클래스의 메서드는 구성 된 공급자에 게 요청을 전달 합니다. `SqlMembershipProvider`사용 됩니다. `Membership` 클래스의 메서드 중 하나를 호출할 때 멤버 프레임 워크에서 `SqlMembershipProvider`호출을 위임 하는 방법을 어떻게 알 수 있나요?

`Membership` 클래스에는 멤버 자격 프레임 워크에서 사용할 수 있는 등록 된 모든 공급자 클래스에 대 한 참조를 포함 하는 [`Providers` 속성이](https://msdn.microsoft.com/library/system.web.security.membership.providers.aspx) 있습니다. 등록 된 각 공급자에는 연결 된 이름 및 유형이 있습니다. 이 이름은 `Providers` 컬렉션에서 특정 공급자를 참조 하는 사용자에 게 친숙 한 방법을 제공 하는 반면 형식은 공급자 클래스를 식별 합니다. 또한 등록 된 각 공급자에는 구성 설정이 포함 될 수 있습니다. 멤버 자격 프레임 워크에 대 한 구성 설정에는 `passwordFormat` 및 `requiresUniqueEmail`가 포함 됩니다. `SqlMembershipProvider`에서 사용 하는 구성 설정의 전체 목록은 표 2를 참조 하세요.

`Providers` 속성의 내용은 웹 응용 프로그램의 구성 설정을 통해 지정 됩니다. 기본적으로 모든 웹 응용 프로그램에는 `SqlMembershipProvider`형식의 `AspNetSqlMembershipProvider` 라는 공급자가 있습니다. 이 기본 멤버 자격 공급자는 `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG)`에 있는 `machine.config`에 등록 됩니다.

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample1.xml)]

위의 태그가 보여 주는 것 처럼 [`<membership>` 요소](https://msdn.microsoft.com/library/1b9hw62f.aspx) 는 [`<providers>` 자식 요소가](https://msdn.microsoft.com/library/6d4936ht.aspx) 등록 된 공급자를 지정 하는 동안 멤버 자격 프레임 워크에 대 한 구성 설정을 정의 합니다. [`<add>`](https://msdn.microsoft.com/library/whae3t94.aspx) 또는 [`<remove>`](https://msdn.microsoft.com/library/aykw9a6d.aspx) 요소를 사용 하 여 공급자를 추가 하거나 제거할 수 있습니다. [`<clear>`](https://msdn.microsoft.com/library/t062y6yc.aspx) 요소를 사용 하 여 현재 등록 된 공급자를 모두 제거 합니다. 위의 태그에서 보여 주는 것 처럼 `machine.config` `SqlMembershipProvider`형식의 `AspNetSqlMembershipProvider` 라는 공급자를 추가 합니다.

`name` 및 `type` 특성 외에도 `<add>` 요소는 다양 한 구성 설정의 값을 정의 하는 특성을 포함 합니다. 표 2에는 사용 가능한 `SqlMembershipProvider`관련 구성 설정과 각 설정에 대 한 설명이 나와 있습니다.

> [!NOTE]
> 표 2에 명시 된 기본값은 `SqlMembershipProvider` 클래스에 정의 된 기본값을 참조 합니다. `AspNetSqlMembershipProvider`의 일부 구성 설정은 `SqlMembershipProvider` 클래스의 기본값과 일치 하지 않습니다. 예를 들어 멤버 자격 공급자에 지정 되지 않은 경우 `requiresUniqueEmail` 설정의 기본값은 true입니다. 그러나 `AspNetSqlMembershipProvider`는 `false`값을 명시적으로 지정 하 여이 기본값을 재정의 합니다.

| **설정&lt;\_o3a\_p/&gt;** | **설명&lt;\_o3a\_p/&gt;** |
| --- | --- |
| `ApplicationName` | Membership framework는 단일 사용자 저장소가 여러 응용 프로그램에 걸쳐 분할 될 수 있도록 합니다. 이 설정은 멤버 자격 공급자가 사용 하는 응용 프로그램 파티션의 이름을 나타냅니다. 이 값을 명시적으로 지정 하지 않으면 런타임에 응용 프로그램의 가상 루트 경로 값으로 설정 됩니다. |
| `commandTimeout` | SQL 명령 제한 시간 값 (초)을 지정 합니다. 기본값은 30입니다. |
| `connectionStringName` | 사용자 저장소 데이터베이스에 연결 하는 데 사용할 `<connectionStrings>` 요소에 있는 연결 문자열의 이름입니다. 이 값은 필수입니다. |
| `description` | 등록 된 공급자에 대 한 사용자에 게 친숙 한 설명을 제공 합니다. |
| `enablePasswordRetrieval` | 사용자가 잊어버린 암호를 검색할 수 있는지 여부를 지정 합니다. 기본값은 `false`입니다. |
| `enablePasswordReset` | 사용자가 자신의 암호를 재설정할 수 있는지 여부를 나타냅니다. 기본값은 `true`입니다. |
| `maxInvalidPasswordAttempts` | 사용자가 잠기기 전에 `passwordAttemptWindow` 지정 된 사용자가 지정 된 사용자에 대해 발생할 수 있는 최대 로그인 실패 횟수입니다. 기본값은 5입니다. |
| `minRequiredNonalphanumericCharacters` | 사용자의 암호에 표시 되어야 하는 영숫자가 아닌 최소 문자 수입니다. 이 값은 0에서 128 사이 여야 합니다. 기본값은 1입니다. |
| `minRequiredPasswordLength` | 암호에 필요한 최소 문자 수입니다. 이 값은 0에서 128 사이 여야 합니다. 기본값은 7입니다. |
| `name` | 등록 된 공급자의 이름입니다. 이 값은 필수입니다. |
| `passwordAttemptWindow` | 실패 한 로그인 시도가 추적 되는 시간 (분)입니다. 사용자가 지정 된 기간 내에 잘못 된 로그인 자격 `maxInvalidPasswordAttempts` 증명을 제공 하는 경우에는 잠금이 잠깁니다. 기본값은 10입니다. |
| `PasswordFormat` | 암호 저장소 형식: `Clear`, `Hashed`또는 `Encrypted`. 기본값은 `Hashed`입니다. |
| `passwordStrengthRegularExpression` | 제공 되는 경우이 정규식은 새 계정을 만들 때 또는 암호를 변경할 때 사용자가 선택한 암호의 강도를 평가 하는 데 사용 됩니다. 기본값은 빈 문자열입니다. |
| `requiresQuestionAndAnswer` | 사용자가 암호를 검색 하거나 다시 설정 하는 경우 보안 질문에 답변해 야 하는지 여부를 지정 합니다. 기본값은 `true`입니다. |
| `requiresUniqueEmail` | 지정 된 응용 프로그램 파티션의 모든 사용자 계정에 고유한 전자 메일 주소가 있어야 하는지 여부를 나타냅니다. 기본값은 `true`입니다. |
| `type` | 공급자의 유형을 지정 합니다. 이 값은 필수입니다. |

**표 2**: 멤버 자격 및 `SqlMembershipProvider` 구성 설정

`AspNetSqlMembershipProvider`외에도 `Web.config` 파일에 비슷한 태그를 추가 하 여 응용 프로그램 별로 다른 멤버 자격 공급자를 등록할 수 있습니다.

> [!NOTE]
> 역할 프레임 워크는 거의 동일한 방식으로 작동 합니다. `machine.config`에 등록 된 기본 역할 공급자가 있으며 등록 된 공급자는 `Web.config`에서 응용 프로그램 별로 사용자 지정 될 수 있습니다. 이후 자습서에서는 역할 프레임 워크 및 해당 구성 마크업에 대해 자세히 살펴보겠습니다.

### <a name="customizing-thesqlmembershipprovidersettings"></a>`SqlMembershipProvider`설정 사용자 지정

기본 `SqlMembershipProvider` (`AspNetSqlMembershipProvider`) `connectionStringName` 특성은 `LocalSqlServer`로 설정 됩니다. `AspNetSqlMembershipProvider` 공급자와 마찬가지로 연결 문자열 이름 `LocalSqlServer` `machine.config`에 정의 되어 있습니다.

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample2.xml)]

여기에서 볼 수 있듯이이 연결 문자열은 |에 있는 SQL 2005 Express Edition 데이터베이스를 정의 합니다. DataDirectory | aspnetdb.mdf. 문자열 | DataDirectory | `~/App_Data/` 디렉터리를 가리키도록 런타임에 변환 되므로 데이터베이스 경로 | DataDirectory | aspnetdb.mdf는 `~/App_Data`/`aspnet.mdf`로 변환 됩니다.

응용 프로그램의 `Web.config` 파일에 멤버 자격 공급자 정보를 지정 하지 않은 경우 응용 프로그램은 등록 된 기본 멤버 자격 공급자 인 `AspNetSqlMembershipProvider`를 사용 합니다. `~/App_Data/aspnet.mdf` 데이터베이스가 없으면 ASP.NET 런타임은 자동으로이를 만들고 응용 프로그램 서비스 스키마를 추가 합니다. 그러나 `aspnet.mdf` 데이터베이스를 사용 하지 않으려고 합니다. 대신 2 단계에서 만든 `SecurityTutorials.mdf` 데이터베이스를 사용 하려고 합니다. 이 수정 작업은 다음 두 가지 방법 중 하나로 수행할 수 있습니다.

- <strong>`Web.config`</strong>에서<strong>`LocalSqlServer`</strong> <strong>연결 문자열 이름</strong> <strong>에 대 한 값을 지정</strong> 합니다 <strong>.</strong> `Web.config`에서 `LocalSqlServer` 연결 문자열 이름 값을 덮어써서 등록 된 기본 멤버 자격 공급자 (`AspNetSqlMembershipProvider`)를 사용 하 고 `SecurityTutorials.mdf` 데이터베이스에서 올바르게 작동 하도록 할 수 있습니다. `AspNetSqlMembershipProvider`에 지정 된 구성 설정을 사용 하는 경우이 방법은 적절 하지 않습니다. 이 기술에 대 한 자세한 내용은 [Scott Guthrie](https://weblogs.asp.net/scottgu/)의 블로그 게시물, [SQL Server 2000 또는 SQL Server 2005를 사용 하도록 ASP.NET 2.0 애플리케이션 서비스 구성](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx)을 참조 하세요.
- <strong>`SqlMembershipProvider`</strong> <strong>형식의 등록 된 새 공급자를 추가</strong> 하 고<strong>`SecurityTutorials.mdf`</strong>데이터베이스 <strong>를 가리키도록</strong> <strong>`connectionStringName`</strong>설정을 <strong>구성</strong> <strong>합니다.</strong> 이 방법은 데이터베이스 연결 문자열 외에 다른 구성 속성을 사용자 지정 하려는 경우에 유용 합니다. 내 프로젝트에서는 유연성과 가독성 때문에 항상이 방법을 사용 합니다.

`SecurityTutorials.mdf` 데이터베이스를 참조 하는 등록 된 새 공급자를 추가 하려면 먼저 `Web.config`의 `<connectionStrings>` 섹션에서 적절 한 연결 문자열 값을 추가 해야 합니다. 다음 태그는 `App_Data` 폴더에서 SQL Server 2005 Express Edition `SecurityTutorials.mdf` 데이터베이스를 참조 하 `SecurityTutorialsConnectionString` 라는 새 연결 문자열을 추가 합니다.

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample3.xml)]

> [!NOTE]
> 대체 데이터베이스 파일을 사용 하는 경우 필요에 따라 연결 문자열을 업데이트 합니다. 올바른 연결 문자열을 형성 하는 방법에 대 한 자세한 내용은 [ConnectionStrings.com](http://www.connectionstrings.com/)를 참조 하세요.

다음으로 `Web.config` 파일에 다음 멤버 자격 구성 태그를 추가 합니다. 이 태그는 `SecurityTutorialsSqlMembershipProvider`라는 새 공급자를 등록 합니다.

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample4.xml)]

`SecurityTutorialsSqlMembershipProvider` 공급자를 등록 하는 것 외에도 위의 태그는 `SecurityTutorialsSqlMembershipProvider`를 기본 공급자로 정의 합니다 (`<membership>` 요소의 `defaultProvider` 특성을 통해). 멤버 자격 프레임 워크에는 등록 된 공급자가 여러 개 있을 수 있습니다. `AspNetSqlMembershipProvider`은 `machine.config`의 첫 번째 공급자로 등록 되므로 달리 지정 하지 않는 한 기본 공급자로 사용 됩니다.

현재 응용 프로그램에는 두 개의 등록 된 공급자 인 `AspNetSqlMembershipProvider` 및 `SecurityTutorialsSqlMembershipProvider`있습니다. 그러나 `SecurityTutorialsSqlMembershipProvider` 공급자를 등록 하기 전에 `<add>` 요소 바로 앞에 [`<clear />` 요소](https://msdn.microsoft.com/library/t062y6yc.aspx) 를 추가 하 여 이전에 등록 된 공급자를 모두 지울 수 있습니다. 이렇게 하면 등록 된 공급자 목록에서 `AspNetSqlMembershipProvider`을 지울 수 있습니다. 즉, `SecurityTutorialsSqlMembershipProvider` 등록 된 유일한 멤버 자격 공급자가 됩니다. 이 접근 방식을 사용 하는 경우 등록 된 유일한 멤버 자격 공급자 이기 때문에 `SecurityTutorialsSqlMembershipProvider`를 기본 공급자로 표시할 필요가 없습니다. `<clear />`사용에 대 한 자세한 내용은 [공급자를 추가할 때 `<clear />` 사용](https://weblogs.asp.net/scottgu/archive/2006/11/20/common-gotcha-don-t-forget-to-clear-when-adding-providers.aspx)을 참조 하세요.

`SecurityTutorialsSqlMembershipProvider`의 `connectionStringName` 설정은 방금 추가 된 `SecurityTutorialsConnectionString` 연결 문자열 이름을 참조 하 고 `applicationName` 설정이 SecurityTutorials의 값으로 설정 되어 있는지 확인 합니다. 또한 `requiresUniqueEmail` 설정이 `true`로 설정 되었습니다. 다른 모든 구성 옵션은 `AspNetSqlMembershipProvider`의 값과 동일 합니다. 원하는 경우 언제 든 지 모든 구성을 수정할 수 있습니다. 예를 들어, 하나 대신 영숫자가 아닌 문자를 두 개 이상 요구 하거나 암호 길이를 7이 아닌 8 자로 늘려서 암호 강도를 강화할 수 있습니다.

> [!NOTE]
> Membership framework는 단일 사용자 저장소가 여러 응용 프로그램에 걸쳐 분할 될 수 있도록 합니다. 멤버 자격 공급자의 `applicationName` 설정은 사용자 저장소를 사용할 때 공급자가 사용 하는 응용 프로그램을 나타냅니다. `applicationName` 구성 설정에 대 한 값을 명시적으로 설정 하는 것이 중요 합니다. `applicationName`을 명시적으로 설정 하지 않은 경우 런타임에 웹 응용 프로그램의 가상 루트 경로에 할당 됩니다. 응용 프로그램의 가상 루트 경로가 변경 되지 않은 경우에는 잘 작동 하지만 응용 프로그램을 다른 경로로 이동 하면 `applicationName` 설정도 변경 됩니다. 이 경우 멤버 자격 공급자는 이전에 사용 된 것과 다른 응용 프로그램 파티션으로 작업을 시작 합니다. 이동 전에 만든 사용자 계정은 다른 응용 프로그램 파티션에 상주 하 고 해당 사용자는 더 이상 사이트에 로그인 할 수 없습니다. 이러한 문제에 대 한 자세한 내용은 [ASP.NET 2.0 멤버 자격 및 기타 공급자를 구성할 때 항상 `applicationName` 속성 설정](https://weblogs.asp.net/scottgu/443634)을 참조 하세요.

## <a name="summary"></a>요약

이 시점에서`SecurityTutorials.mdf`(구성 된 응용 프로그램 서비스)가 포함 된 데이터베이스가 있고, 멤버 자격 프레임 워크에서 방금 등록 한 `SecurityTutorialsSqlMembershipProvider` 공급자를 사용 하도록 웹 응용 프로그램을 구성 했습니다. 이 등록 된 공급자는 `SqlMembershipProvider` 유형이 며 해당 `connectionStringName`를 적절 한 연결 문자열 (`SecurityTutorialsConnectionString`)로 설정 하 고 해당 `applicationName` 값을 명시적으로 설정 합니다.

이제 응용 프로그램에서 멤버 자격 프레임 워크를 사용할 준비가 되었습니다. 다음 자습서에서는 새 사용자 계정을 만드는 방법을 살펴봅니다. 다음에는 사용자 인증, 사용자 기반 권한 부여 수행, 데이터베이스에 추가 사용자 관련 정보 저장에 대해 설명 합니다.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 참고 자료

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 2.0 멤버 자격과 기타 공급자를 구성할 때 항상 `applicationName` 속성을 설정 합니다.](https://weblogs.asp.net/scottgu/443634)
- [SQL Server 2000 또는 SQL Server 2005를 사용 하도록 ASP.NET 2.0 애플리케이션 서비스 구성](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx)
- [Express Edition 다운로드 SQL Server Management Studio](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en)
- [ASP.NET 2.0 s 멤버 자격, 역할 및 프로필 검사](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [멤버 자격에 대 한 공급자의 `<add>` 요소](https://msdn.microsoft.com/library/whae3t94.aspx)
- [`<membership>` 요소](https://msdn.microsoft.com/library/1b9hw62f.aspx)
- [멤버 자격에 대 한 `<providers>` 요소](https://msdn.microsoft.com/library/6d4936ht.aspx)
- [공급자를 추가할 때 `<clear />` 사용](https://weblogs.asp.net/scottgu/archive/2006/11/20/common-gotcha-don-t-forget-to-clear-when-adding-providers.aspx)
- [`SqlMembershipProvider` 직접 작업](http://aspnet.4guysfromrolla.com/articles/091207-1.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>이 자습서에 포함 된 항목에 대 한 비디오 학습

- [ASP.NET 멤버 자격 이해](../../../videos/authentication/understanding-aspnet-memberships.md)
- [멤버 자격 스키마와 함께 작동하도록 SQL 구성](../../../videos/authentication/configuring-sql-to-work-with-membership-schemas.md)
- [기본 멤버 자격 스키마에서 멤버 자격 설정 변경](../../../videos/authentication/changing-membership-settings-in-the-default-membership-schema.md)

### <a name="about-the-author"></a>저자 정보

Scott Mitchell는 여러 ASP/ASP. NET books의 작성자와 4GuysFromRolla.com의 창립자가 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 *[24 시간 이내에 ASP.NET 2.0을 sams teach yourself](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 것입니다. Scott은 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) 또는 [http://ScottOnWriting.NET](http://scottonwriting.net/)의 블로그를 통해 연결할 수 있습니다.

### <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Alicja Maziarz입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면 [mitchell@4GuysFromRolla.com](mailto:mitchell@4guysfromrolla.com)에서 줄을 삭제 합니다.

> [!div class="step-by-step"]
> [다음](creating-user-accounts-cs.md)
