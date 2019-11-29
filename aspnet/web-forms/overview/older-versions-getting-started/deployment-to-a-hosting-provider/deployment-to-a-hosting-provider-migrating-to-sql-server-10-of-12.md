---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12
title: 'Visual Studio 또는 Visual Web Developer를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: SQL Server로 마이그레이션 (12/10) Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 Visual Stu ...를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 11/17/2011
ms.assetid: a89d6f32-b71b-4036-8ff7-5f8ac2a6eca8
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12
msc.type: authoredcontent
ms.openlocfilehash: c5281a42596d95e725b32e652c75785abe0fd64e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74640636"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-migrating-to-sql-server---10-of-12"></a>Visual Studio 또는 Visual Web Developer를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: SQL Server로 마이그레이션 (12/10)

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 이 자습서 시리즈에서는 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC for Web을 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다. 웹 게시 업데이트를 설치 하는 경우 Visual Studio 2010을 사용할 수도 있습니다. 시리즈에 대 한 소개는 [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)를 참조 하십시오.
> 
> Visual Studio 2012의 RC 릴리스 후에 도입 된 배포 기능을 보여 주는 자습서는 SQL Server Compact 이외의 SQL Server 버전을 배포 하는 방법을 보여 주고 Azure App Service Web Apps에 배포 하는 방법을 보여 줍니다. [Visual Studio를 사용 하 여 ASP.NET 웹 배포](../../deployment/visual-studio-web-deployment/introduction.md)를 참조 하세요.

## <a name="overview"></a>개요

이 자습서에서는 SQL Server Compact에서 SQL Server로 마이그레이션하는 방법을 보여 줍니다. 이 작업을 수행 하는 한 가지 이유는 저장 프로시저, 트리거, 뷰, 복제 등 SQL Server Compact 지원 하지 않는 SQL Server 기능을 활용 하는 것입니다. SQL Server Compact와 SQL Server 간의 차이점에 대 한 자세한 내용은 [SQL Server Compact 배포](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) 자습서를 참조 하십시오.

### <a name="sql-server-express-versus-full-sql-server-for-development"></a>개발을 위한 전체 SQL Server SQL Server Express

SQL Server로 업그레이드 하기로 결정 한 후에는 개발 및 테스트 환경에서 SQL Server 또는 SQL Server Express를 사용 하는 것이 좋습니다. 도구 지원과 데이터베이스 엔진 기능의 차이점 외에도 공급자 구현에 SQL Server Compact와 다른 SQL Server 버전 간의 차이가 있습니다. 이러한 차이로 인해 동일한 코드가 다른 결과를 생성할 수 있습니다. 따라서 SQL Server Compact를 개발 데이터베이스로 유지 하기로 결정 한 경우 프로덕션에 배포 하기 전에 테스트 환경에서 SQL Server 또는 SQL Server Express에서 사이트를 철저히 테스트 해야 합니다.

SQL Server Compact와 달리 SQL Server Express은 기본적으로 동일한 데이터베이스 엔진 이며 전체 SQL Server 동일한 .NET 공급자를 사용 합니다. SQL Server Express를 사용 하 여 테스트 하는 경우 SQL Server와 동일한 결과를 얻을 수 있습니다. SQL Server Express와 함께 사용할 수 있는 대부분의 동일한 데이터베이스 도구를 사용 하 여 SQL Server ( [SQL Server Profiler](https://msdn.microsoft.com/library/ms181091.aspx)하는 주목할 만한 예외)를 사용할 수 있으며, 저장 프로시저, 뷰, 트리거 및 복제와 같은 SQL Server의 다른 기능을 지원 합니다. 그러나 일반적으로 프로덕션 웹 사이트에서는 전체 SQL Server를 사용 해야 합니다. SQL Server Express은 공유 호스팅 환경에서 실행할 수 있지만이를 위해 설계 되지 않았으므로 많은 호스팅 공급자가이를 지원 하지 않습니다.)

Visual Studio 2012을 사용 하는 경우 일반적으로 Visual Studio에서 기본적으로 설치 되는 것 이기 때문에 개발 환경에 대 한 SQL Server Express LocalDB를 선택 합니다. 그러나 LocalDB는 IIS에서 작동 하지 않으므로 테스트 환경에 SQL Server 또는 SQL Server Express를 사용 해야 합니다.

### <a name="combining-databases-versus-keeping-them-separate"></a>데이터베이스 조합 및 분리

Contoso 대학 응용 프로그램에는 두 개의 SQL Server Compact 데이터베이스, 즉 멤버 자격 데이터베이스 (*aspnet .sdf*)와 응용 프로그램 데이터베이스 (*School*)가 있습니다. 마이그레이션할 때 이러한 데이터베이스를 두 개의 개별 데이터베이스나 단일 데이터베이스로 마이그레이션할 수 있습니다. 응용 프로그램 데이터베이스와 멤버 자격 데이터베이스 간의 데이터베이스 조인을 용이 하 게 하기 위해 결합 하는 것이 좋습니다. 호스팅 계획을 결합 하는 이유가 제공 될 수도 있습니다. 예를 들어 호스팅 공급자는 여러 데이터베이스에 대해 더 많은 요금을 청구 하거나 둘 이상의 데이터베이스를 허용 하지 않을 수 있습니다. 단일 SQL Server 데이터베이스만 허용 하는이 자습서에 사용 되는 Cytanium Lite 호스팅 계정을 사용 하는 경우입니다.

이 자습서에서는 다음과 같은 방법으로 두 개의 데이터베이스를 마이그레이션합니다.

- 개발 환경에서 두 개의 LocalDB 데이터베이스로 마이그레이션합니다.
- 테스트 환경에서 두 개의 SQL Server Express 데이터베이스로 마이그레이션합니다.
- 프로덕션 환경에서 결합 된 전체 SQL Server 데이터베이스 하나로 마이그레이션합니다.

미리 알림: 자습서를 진행할 때 오류 메시지가 표시 되거나 문제가 해결 되지 않으면 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)를 확인 해야 합니다.

## <a name="installing-sql-server-express"></a>SQL Server Express 설치

SQL Server Express는 기본적으로 Visual Studio 2010와 함께 자동으로 설치 되지만, 기본적으로 Visual Studio 2012과 함께 설치 되지 않습니다. SQL Server 2012 Express를 설치 하려면 다음 링크를 클릭 하십시오.

- [SQL Server Express 2012](https://www.microsoft.com/download/details.aspx?id=29062)

*한국어/x64/sqlexpr\_x64\_enu* 또는 *enu/X86/sqlexpr\_x86\_enu*를 선택 하 고 설치 마법사에서 기본 설정을 적용 합니다. 설치 옵션에 대 한 자세한 내용은 설치 [마법사에서 SQL Server 2012 설치 (설치 프로그램)](https://msdn.microsoft.com/library/ms143219.aspx)를 참조 하세요.

## <a name="creating-sql-server-express-databases-for-the-test-environment"></a>테스트 환경에 대 한 SQL Server Express 데이터베이스 만들기

다음 단계는 ASP.NET 멤버 자격과 School 데이터베이스를 만드는 것입니다.

**보기** 메뉴에서 **서버 탐색기** (Visual Web Developer에서**데이터베이스 탐색기** )를 선택 하 고 **데이터 연결** 을 마우스 오른쪽 단추로 클릭 한 다음 **새 SQL Server 데이터베이스 만들기**를 선택 합니다.

![Selecting_Create_New_SQL_Server_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image1.png)

**새 SQL Server 데이터베이스 만들기** 대화 상자에서 **서버 이름** 상자에 ".\SQLExpress"를 입력 하 고 **새 데이터베이스 이름** 상자에 "aspnet-Test"를 입력 한 다음 **확인**을 클릭 합니다.

![Create_New_SQL_Server_Database_aspnet](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image2.png)

동일한 절차에 따라 "School-Test" 라는 새 SQL Server Express School 데이터베이스를 만듭니다.

나중에 개발 환경에 대 한 각 데이터베이스의 추가 인스턴스를 만들고 두 데이터베이스 집합을 구분할 수 있어야 하므로 이러한 데이터베이스 이름에 "Test"를 추가 하는 것입니다.

이제 **서버 탐색기** 에 두 개의 새 데이터베이스가 표시 됩니다.

![New_databases_in_Server_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image3.png)

## <a name="creating-a-grant-script-for-the-new-databases"></a>새 데이터베이스에 대 한 Grant 스크립트 만들기

응용 프로그램이 개발 컴퓨터의 IIS에서 실행 되는 경우 응용 프로그램은 기본 응용 프로그램 풀의 자격 증명을 사용 하 여 데이터베이스에 액세스 합니다. 그러나 기본적으로 응용 프로그램 풀 id에는 데이터베이스를 열 수 있는 권한이 없습니다. 따라서 해당 사용 권한을 부여 하는 스크립트를 실행 해야 합니다. 이 섹션에서는 응용 프로그램이 IIS에서 실행 될 때 데이터베이스를 열 수 있도록 나중에 실행할 스크립트를 만듭니다.

[프로덕션 환경에 배포](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) 자습서에서 만든 솔루션의 *솔루션의 솔루션 폴더에서* *Grant .sql*이라는 새 SQL 파일을 만듭니다. 다음 SQL 명령을 파일에 복사 하 고 파일을 저장 한 후 닫습니다.

[!code-sql[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample1.sql)]

> [!NOTE]
> 이 스크립트는이 자습서에 지정 된 대로 SQL Server 2008 및 Windows 7의 IIS 설정에서 작동 하도록 설계 되었습니다. 다른 버전의 SQL Server 또는 Windows를 사용 하는 경우 또는 컴퓨터에 IIS를 다르게 설정 하는 경우이 스크립트를 변경 해야 할 수 있습니다. SQL Server 스크립트에 대 한 자세한 내용은 [SQL Server 온라인 설명서](https://go.microsoft.com/fwlink/?LinkId=132511)을 참조 하십시오.

> [!NOTE] 
> 
> **보안 정보** 이 스크립트는 런타임에 데이터베이스에 액세스 하는 사용자에 게 db\_소유자 권한을 제공 합니다 .이 권한은 프로덕션 환경에서 사용할 수 있습니다. 일부 시나리오에서는 배포에 대 한 전체 데이터베이스 스키마 업데이트 권한만 있는 사용자를 지정 하 고 데이터를 읽고 쓸 수 있는 권한만 있는 다른 사용자를 런타임에 지정할 수 있습니다. 자세한 내용은 [IIS에 테스트 환경으로 배포 하](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) **는 Code First 마이그레이션에 대 한 자동 Web.config 변경 내용 검토** 를 참조 하세요.

## <a name="configuring-database-deployment-for-the-test-environment"></a>테스트 환경에 대 한 데이터베이스 배포 구성

다음에는 각 데이터베이스에 대해 다음 작업을 수행할 수 있도록 Visual Studio를 구성 합니다.

- 대상 데이터베이스의 원본 데이터베이스 구조 (테이블, 열, 제약 조건 등)를 만드는 SQL 스크립트를 생성 합니다.
- 원본 데이터베이스의 데이터를 대상 데이터베이스의 테이블에 삽입 하는 SQL 스크립트를 생성 합니다.
- 생성 된 스크립트와 사용자가 만든 Grant 스크립트를 대상 데이터베이스에서 실행 합니다.

**프로젝트 속성** 창을 열고 **SQL 패키지 및 게시** 탭을 선택 합니다.

**구성** 드롭다운 목록에서 **활성 (릴리스)** 또는 **릴리스** 가 선택 되어 있는지 확인 합니다.

**이 페이지 사용**을 클릭 합니다.

![Package_Publish_SQL_tab_Enable_This_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image4.png)

**SQL 패키지 및 게시** 탭은 레거시 배포 방법을 지정 하므로 일반적으로 비활성화 되어 있습니다. 대부분의 시나리오의 경우 **웹 게시** 마법사에서 데이터베이스 배포를 구성 해야 합니다. SQL Server Compact에서 SQL Server 또는 SQL Server Express으로 마이그레이션하는 것은이 방법을 선택 하는 것이 좋은 특수 한 경우입니다.

**Web.config에서 가져오기를**클릭 합니다.

![Selecting_Import_from_Web .config](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image5.png)

Visual Studio는 web.config 파일에서 연결 문자열을 찾고, 멤버 자격 데이터베이스와 School 데이터베이스에 대해 하나를 찾고, **데이터베이스 항목** 테이블의 각 연결 문자열에 해당 하는 행을 *추가 합니다.* 기존 SQL Server Compact 데이터베이스에 대 한 연결 문자열을 찾은 후 다음 단계는 이러한 데이터베이스를 배포할 방법 및 위치를 구성 하는 것입니다.

데이터베이스 항목 **세부 정보** 섹션 **의 데이터베이스 항목 테이블 아래** 에 데이터베이스 배포 설정을 입력 합니다. **데이터베이스 항목 세부 정보** 섹션에 표시 된 설정은 다음 그림에 표시 된 것 처럼 **데이터베이스 항목** 테이블의 어떤 행이 선택 되었는지와 관련이 있습니다.

![Database_Entry_Details_section_of_Package_Publish_SQL_tab](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image6.png)

### <a name="configuring-deployment-settings-for-the-membership-database"></a>멤버 자격 데이터베이스에 대 한 배포 설정 구성

멤버 자격 데이터베이스에 적용 되는 설정을 구성 하기 위해 **데이터베이스 항목** 테이블에서 **Defaultconnection-Deployment** 행을 선택 합니다.

**대상 데이터베이스에 대 한 연결 문자열**에 새 SQL Server Express 멤버 자격 데이터베이스를 가리키는 연결 문자열을 입력 합니다. **서버 탐색기**에서 필요한 연결 문자열을 가져올 수 있습니다. **서버 탐색기**에서 **데이터 연결** 을 확장 하 고 **AspnetTest** 데이터베이스를 선택한 다음 **속성** 창에서 **연결 문자열** 값을 복사 합니다.

![aspnet_connection_string_in_Server_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image7.png)

동일한 연결 문자열이 다음과 같이 재현 됩니다.

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample2.cmd)]

**SQL 패키지 및 게시** 탭에서 **대상 데이터베이스에 대 한 연결 문자열** 에이 연결 문자열을 복사 하 여 붙여 넣습니다.

**기존 데이터베이스에서 데이터 및/또는 스키마 끌어오기** 가 선택 되어 있는지 확인 합니다. 이로 인해 SQL 스크립트가 자동으로 생성 되 고 대상 데이터베이스에서 실행 됩니다.

**원본 데이터베이스 값에 대 한 연결 문자열** 을 *web.config 파일에서* 추출 하 고 개발 SQL Server Compact 데이터베이스를 가리킵니다. 이는 대상 데이터베이스에서 나중에 실행 될 스크립트를 생성 하는 데 사용 되는 원본 데이터베이스입니다. 프로덕션 버전의 데이터베이스를 배포 하려는 경우 "aspnet-Dev"을 "aspnet-Prod"로 변경 합니다.

데이터베이스 구조 뿐만 아니라 데이터 (사용자 계정 및 역할)를 복사 하려는 경우에 **만 스키마** 에서 스키마 **및 데이터로** **데이터베이스 스크립팅 옵션** 을 변경 합니다.

이전에 만든 grant 스크립트를 실행 하도록 배포를 구성 하려면 **데이터베이스 스크립트** 섹션에 해당 스크립트를 추가 해야 합니다. **스크립트 추가**를 클릭 하 고 **SQL 스크립트 추가** 대화 상자에서 grant 스크립트를 저장 한 폴더로 이동 합니다 .이 폴더는 솔루션 파일이 들어 있는 폴더입니다. *Grant .sql*이라는 파일을 선택 하 고 **열기**를 클릭 합니다.

[![Select_File_dialog_box_grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image9.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image8.png)

**데이터베이스 항목** 에서 **defaultconnection 배포** 행의 설정은 이제 다음 그림과 같습니다.

![Database_Entry_Details_for_DefaultConnection_Test](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image10.png)

### <a name="configuring-deployment-settings-for-the-school-database"></a>School 데이터베이스에 대 한 배포 설정 구성

그런 다음 School 데이터베이스에 대 한 배포 설정을 구성 하기 위해 **데이터베이스 항목** 테이블에서 **schoolcontext.cs** 행을 선택 합니다.

이전에 사용한 것과 동일한 방법을 사용 하 여 새 SQL Server Express 데이터베이스에 대 한 연결 문자열을 가져올 수 있습니다. **SQL 패키지 및 게시** 탭에서 **대상 데이터베이스에 대 한 연결 문자열** 에이 연결 문자열을 복사 합니다.

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample3.cmd)]

**기존 데이터베이스에서 데이터 및/또는 스키마 끌어오기** 가 선택 되어 있는지 확인 합니다.

**원본 데이터베이스 값에 대 한 연결 문자열** 을 *web.config 파일에서* 추출 하 고 개발 SQL Server Compact 데이터베이스를 가리킵니다. "School-Dev"을 "School-Prod"로 변경 하 여 데이터베이스의 프로덕션 버전을 배포 합니다. 응용 프로그램\_Data 폴더에 School-Prod 파일을 만들지 않았기 때문에이 파일을 테스트 환경에서 나중에 ContosoUniversity 프로젝트 폴더의 App\_Data 폴더에 복사 합니다.

**스키마 및 데이터**에 대 한 **데이터베이스 스크립팅 옵션** 을 변경 합니다.

또한 스크립트를 실행 하 여이 데이터베이스에 대 한 읽기 및 쓰기 권한을 응용 프로그램 풀 id에 부여 하는 것 이므로 *grant .sql* 스크립트 파일을 멤버 자격 데이터베이스에 대해 수행한 그대로 추가 합니다.

완료 되 면 **데이터베이스 항목** 에서 **schoolcontext.cs-Deployment** 행의 설정은 다음 그림과 같이 표시 됩니다.

![Database_Entry_Details_for_SchoolContext_Test](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image11.png)

**SQL 패키지 및 게시** 탭에 변경 내용을 저장 합니다.

*C:\inetpub\wwwroot\ContosoUniversity\App\_Data* 폴더에서 ContosoUniversity 프로젝트의 *App\_data* 폴더로 *School-Prod* 파일을 복사 합니다.

### <a name="specifying-transacted-mode-for-the-grant-script"></a>Grant 스크립트의 트랜잭션 모드 지정

배포 프로세스에서는 데이터베이스 스키마 및 데이터를 배포 하는 스크립트를 생성 합니다. 기본적으로 이러한 스크립트는 트랜잭션에서 실행 됩니다. 그러나 기본적으로 사용자 지정 스크립트 (예: grant 스크립트)는 트랜잭션에서 실행 되지 않습니다. 배포 프로세스에서 트랜잭션 모드를 혼합 하는 경우 배포 중에 스크립트를 실행할 때 시간 초과 오류가 발생할 수 있습니다. 이 섹션에서는 트랜잭션에서 실행 되도록 사용자 지정 스크립트를 구성 하기 위해 프로젝트 파일을 편집 합니다.

**솔루션 탐색기**에서 **ContosoUniversity** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **프로젝트 언로드**를 선택 합니다.

![Unload_Project_in_Solution_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image12.png)

그런 다음 프로젝트를 다시 마우스 오른쪽 단추로 클릭 하 고 **ContosoUniversity 편집**을 선택 합니다.

![Edit_Project_in_Solution_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image13.png)

Visual Studio 편집기에는 프로젝트 파일의 XML 콘텐츠가 표시 됩니다. 몇 가지 `PropertyGroup` 요소가 있습니다. 이미지에서 `PropertyGroup` 요소의 콘텐츠가 생략 되었습니다.

![프로젝트 파일 편집기 창](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image15.png)

`Condition` 특성이 없는 첫 번째 항목은 빌드 구성과 상관 없이 적용 되는 설정에 대 한 것입니다. 하나의 `PropertyGroup` 요소는 디버그 빌드 `Condition` 구성에만 적용 되 고, 하나는 릴리스 빌드 구성에만 적용 되며, 하나는 테스트 빌드 구성에만 적용 됩니다. 릴리스 빌드 구성에 대 한 `PropertyGroup` 요소 내에서 **SQL 패키지 및 게시** 탭에서 입력 한 설정이 포함 된 `PublishDatabaseSettings` 요소가 표시 됩니다. 지정한 각 grant 스크립트에 해당 하는 `Object` 요소가 있습니다. "Grant .sql"의 두 인스턴스를 확인 합니다. 기본적으로 각 grant 스크립트에 대 한 `Source` 요소의 `Transacted` 특성은 `False`됩니다.

![Transacted_false](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image16.png)

`Source` 요소의 `Transacted` 특성 값을 `True`로 변경 합니다.

![Transacted_true](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image17.png)

프로젝트 파일을 저장 하 고 닫은 다음 **솔루션 탐색기** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **프로젝트 다시 로드**를 선택 합니다.

![Reload_project](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image18.png)

## <a name="setting-up-webconfig-transformations-for-the-connection-strings"></a>연결 문자열에 대 한 Web.config 변환 설정

**Sql 패키지 및 게시** 탭에 입력 한 새 SQL Express 데이터베이스의 연결 문자열은 배포 중에 대상 데이터베이스를 업데이트 하는 경우에만 웹 배포에서 사용 됩니다. *배포 된 web.config 파일* 의 연결 문자열이 새 SQL Server Express 데이터베이스를 가리키도록 *web.config* 변환을 설정 해야 합니다. **SQL 패키지 및 게시** 탭을 사용 하는 경우 게시 프로필에서 연결 문자열을 구성할 수 없습니다.

*Web.config* 를 열고 다음 예제에서 `connectionStrings` 요소를 `connectionStrings` 요소로 바꿉니다. (컨텍스트를 제공 하기 위해 여기에 표시 된 주변 코드가 아닌 connectionStrings 요소만 복사 해야 합니다.)

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample4.xml?highlight=2-11)]

이 코드는 배포 된 *web.config* 파일에서 각 `add` 요소의 `connectionString` 및 `providerName` 특성을 대체 합니다. 이러한 연결 문자열은 **SQL 패키지 및 게시** 탭에 입력 한 문자열과 동일 하지 않습니다. Entity Framework 및 Universal Providers에 필요 하기 때문에 "MultipleActiveResultSets = True" 설정이 추가 되었습니다.

## <a name="installing-sql-server-compact"></a>SQL Server Compact 설치

SqlServerCompact NuGet 패키지는 Contoso 대학 응용 프로그램에 대 한 SQL Server Compact 데이터베이스 엔진 어셈블리를 제공 합니다. 그러나 이제는 응용 프로그램이 아니지만 SQL Server 데이터베이스에서 실행할 스크립트를 만들기 위해 SQL Server Compact 데이터베이스를 읽을 수 있어야 하는 웹 배포. 웹 배포 SQL Server Compact 데이터베이스를 읽도록 설정 하려면 [Microsoft SQL Server Compact 4.0](https://www.microsoft.com/downloads/details.aspx?FamilyID=15F7C9B3-A150-4AD2-823E-E4E0DCF85DF6)링크를 사용 하 여 개발 컴퓨터에 SQL Server Compact을 설치 합니다.

## <a name="deploying-to-the-test-environment"></a>테스트 환경에 배포

테스트 환경에 게시 하려면 게시 프로필 데이터베이스 설정 대신 데이터베이스 게시에 대 한 **SQL 패키지 및 게시** 탭을 사용 하도록 구성 된 게시 프로필을 만들어야 합니다.

먼저 기존 테스트 프로필을 삭제 합니다.

**솔루션 탐색기**에서 ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 클릭 합니다.

**프로필** 탭을 선택 합니다.

**프로필 관리**를 클릭 합니다.

**테스트**를 선택 하 고 **제거**를 클릭 한 다음 **닫기**를 클릭 합니다.

이 변경 내용을 저장 하려면 **웹 게시** 마법사를 닫습니다.

그런 다음 새 테스트 프로필을 만들어 프로젝트를 게시 하는 데 사용 합니다.

**솔루션 탐색기**에서 ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 클릭 합니다.

**프로필** 탭을 선택 합니다.

드롭다운 목록에서 **&lt;새로 만들기 ...&gt;** 를 선택 하 고 프로필 이름으로 "Test"를 입력 합니다.

**서비스 URL** 상자에 *localhost*를 입력 합니다.

**사이트/응용 프로그램** 상자에서 *기본 웹 사이트/ContosoUniversity*를 입력 합니다.

**대상 URL** 상자에 `http://localhost/ContosoUniversity/`을 입력 합니다.

**다음**을 클릭합니다.

**설정** 탭에서는 **SQL 패키지 및 게시** 탭이 구성 되었다는 경고를 표시 하 고 새 데이터베이스 게시 기능 사용을 클릭 하 여 재정의할 수 있습니다. 이 배포의 경우 **SQL 패키지 및 게시** 탭 설정을 재정의 하지 말고 **다음**을 클릭 하면 됩니다.

![Publish_Web_wizard_Settings_tab_Migrate](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image19.png)

**미리 보기** 탭의 메시지는 **게시할 데이터베이스가 선택**되지 않았음을 나타냅니다. 하지만이는 게시 프로필에서 데이터베이스 게시가 구성 되지 않았음을 의미 합니다.

**게시**를 클릭합니다.

![Publish_Web_wizard_Preview_tab_Migrate](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image20.png)

Visual Studio에서 응용 프로그램을 배포 하 고 테스트 환경에서 사이트의 홈 페이지로 브라우저를 엽니다. 강사 페이지를 실행 하 여 앞에서 살펴본 것과 동일한 데이터가 표시 되는지 확인 합니다. **학생 추가** 페이지를 실행 하 고, 새 학생을 추가한 다음, **학생** 페이지에서 새 학생을 봅니다. 이렇게 하면 데이터베이스를 업데이트할 수 있는지 확인 됩니다. 멤버 자격 데이터베이스를 배포 하 고 해당 데이터베이스에 액세스할 수 있는지 확인 하려면 **크레딧 업데이트** 페이지를 선택 합니다 (로그인 해야 함).

## <a name="creating-a-sql-server-database-for-the-production-environment"></a>프로덕션 환경에 대 한 SQL Server 데이터베이스 만들기

이제 테스트 환경에 배포 했으므로 프로덕션에 배포를 설정할 준비가 되었습니다. 배포할 데이터베이스를 만들어 테스트 환경에서 수행한 것 처럼 시작 합니다. 개요에서 Cytanium Lite 호스팅 요금제는 단일 SQL Server 데이터베이스만 허용 하므로 두 개의 데이터베이스를 하나만 설정 합니다. 멤버 자격과 School SQL Server Compact 데이터베이스의 모든 테이블 및 데이터는 프로덕션 환경에서 하나의 SQL Server 데이터베이스에 배포 됩니다.

[http://panel.cytanium.com](http://panel.cytanium.com)에서 Cytanium 컨트롤 패널로 이동 합니다. **데이터베이스** 위에 마우스를 놓고 **SQL Server 2008**을 클릭 합니다.

[![Selecting_Databases_in_Control_Panel](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image22.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image21.png)

**SQL Server 2008** 페이지에서 **데이터베이스 만들기**를 클릭 합니다.

[![Selecting_Create_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image24.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image23.png)

데이터베이스 이름을 "School"으로 선택 하 고 **저장**을 클릭 합니다. 페이지에 "contosouSchool" 접두사가 자동으로 추가 되므로 유효 이름이 ""이 됩니다.

[![Naming_the_database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image26.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image25.png)

동일한 페이지에서 **사용자 만들기**를 클릭 합니다. Cytanium 서버에서 Windows 통합 보안을 사용 하 고 응용 프로그램 풀 id를 사용 하 여 데이터베이스를 열도록 허용 하는 대신 데이터베이스를 열 수 있는 권한이 있는 사용자를 만듭니다. 프로덕션 *web.config* 파일에 있는 연결 문자열에 사용자의 자격 증명을 추가 합니다. 이 단계에서는 이러한 자격 증명을 만듭니다.

[![Creating_a_database_user](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image28.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image27.png)

**SQL 사용자 속성** 페이지에서 필수 필드를 입력 합니다.

- 이름으로 "다음으로"를 입력 합니다.
- 암호를 입력 하십시오.
- 기본 데이터베이스로 **contosouSchool** 를 선택 합니다.
- **ContosouSchool** 확인란을 선택 합니다.

[![SQL_User_Properties_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image30.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image29.png)

## <a name="configuring-database-deployment-for-the-production-environment"></a>프로덕션 환경에 대 한 데이터베이스 배포 구성

이제 테스트 환경에 대해 이전에 수행한 것 처럼 **SQL 패키지 및 게시** 탭에서 데이터베이스 배포 설정을 설정할 준비가 완료 되었습니다.

**프로젝트 속성** 창을 열고 **SQL 패키지 및 게시** 탭을 선택한 후 **구성** 드롭다운 목록에서 **활성 (릴리스)** 또는 **릴리스** 가 선택 되어 있는지 확인 합니다.

각 데이터베이스에 대 한 배포 설정을 구성 하는 경우, 프로덕션 및 테스트 환경에서 수행 하는 작업 간의 주요 차이점은 연결 문자열을 구성 하는 방법에 있습니다. 테스트 환경에서 다른 대상 데이터베이스 연결 문자열을 입력 했지만 프로덕션 환경의 경우 대상 연결 문자열은 두 데이터베이스에 대해 동일 합니다. 이는 프로덕션 환경의 한 데이터베이스에 두 데이터베이스를 배포 하기 때문입니다.

### <a name="configuring-deployment-settings-for-the-membership-database"></a>멤버 자격 데이터베이스에 대 한 배포 설정 구성

멤버 자격 데이터베이스에 적용 되는 설정을 구성 하려면 **데이터베이스 항목** 테이블에서 **Defaultconnection-Deployment** 행을 선택 합니다.

**대상 데이터베이스에 대 한 연결 문자열**에서 방금 만든 새 프로덕션 SQL Server 데이터베이스를 가리키는 연결 문자열을 입력 합니다. 환영 전자 메일에서 연결 문자열을 가져올 수 있습니다. 전자 메일의 관련 부분에는 다음과 같은 샘플 연결 문자열이 포함 되어 있습니다.

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample5.cmd)]

세 개의 변수를 바꾼 후 필요한 연결 문자열은 다음 예제와 같습니다.

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample6.cmd)]

**SQL 패키지 및 게시** 탭에서 **대상 데이터베이스에 대 한 연결 문자열** 에이 연결 문자열을 복사 하 여 붙여 넣습니다.

**기존 데이터베이스에서 데이터 및/또는 스키마 끌어오기** 를 선택 하 고 **데이터베이스 스크립팅 옵션** 은 여전히 **스키마와 데이터**인지 확인 합니다.

**데이터베이스 스크립트** 상자에서 Grant. sql 스크립트 옆에 있는 확인란의 선택을 취소 합니다.

![Disable_Grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image31.png)

### <a name="configuring-deployment-settings-for-the-school-database"></a>School 데이터베이스에 대 한 배포 설정 구성

그런 다음, School 데이터베이스 설정을 구성 하기 위해 **데이터베이스 항목** 테이블에서 **schoolcontext.cs** 행을 선택 합니다.

멤버 자격 데이터베이스의 해당 필드에 복사한 **대상 데이터베이스의 연결 문자열** 에 동일한 연결 문자열을 복사 합니다.

**기존 데이터베이스에서 데이터 및/또는 스키마 끌어오기** 를 선택 하 고 **데이터베이스 스크립팅 옵션** 은 여전히 **스키마와 데이터**인지 확인 합니다.

**데이터베이스 스크립트** 상자에서 Grant. sql 스크립트 옆에 있는 확인란의 선택을 취소 합니다.

**SQL 패키지 및 게시** 탭에 변경 내용을 저장 합니다.

## <a name="setting-up-webconfig-transforms-for-the-connection-strings-to-production-databases"></a>프로덕션 데이터베이스에 대 한 연결 문자열에 대 한 Web.config 변환 설정

다음으로 *, 배포 된 web.config 파일* 의 연결 문자열이 새 프로덕션 데이터베이스를 가리키도록 *web.config* 변환을 설정 합니다. `MultipleResultSets` 옵션을 추가 하는 경우를 제외 하 고는 **SQL 패키지 및 게시** 탭에 입력 한 연결 문자열이 응용 프로그램에서 사용 해야 하는 것과 웹 배포 합니다.

*Web.config* 를 열고 `connectionStrings` 요소를 다음 예제와 같은 `connectionStrings` 요소로 바꿉니다. 컨텍스트를 표시 하기 위해 제공 된 주변 태그가 아닌 `connectionStrings` 요소만 복사 합니다.

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample7.xml?highlight=2-11)]

경우에 따라 *web.config 파일에서* 연결 문자열을 항상 암호화 하도록 알려 주는 조언이 표시 될 수 있습니다. 이는 회사의 네트워크에 있는 서버에 배포 하는 경우에 적합할 수 있습니다. 그러나 공유 호스팅 환경에 배포 하는 경우 호스팅 공급자의 보안 사례를 신뢰 하 고, 연결 문자열을 암호화 하는 것은 필요 하지 않습니다.

## <a name="deploying-to-the-production-environment"></a>프로덕션 환경에 배포

이제 프로덕션 환경에 배포할 준비가 되었습니다. 웹 배포는 프로젝트의 *App\_데이터* 폴더에 있는 SQL Server Compact 데이터베이스를 읽고 프로덕션 SQL Server 데이터베이스에 있는 모든 테이블 및 데이터를 다시 만듭니다. **웹 패키지 및 게시** 탭 설정을 사용 하 여 게시 하려면 프로덕션을 위한 새 게시 프로필을 만들어야 합니다.

먼저 이전에 테스트 프로필을 수행한 것 처럼 기존 프로덕션 프로필을 삭제 합니다.

**솔루션 탐색기**에서 ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 클릭 합니다.

**프로필** 탭을 선택 합니다.

**프로필 관리**를 클릭 합니다.

**프로덕션**을 선택 하 고 **제거**를 클릭 한 다음 **닫기**를 클릭 합니다.

이 변경 내용을 저장 하려면 **웹 게시** 마법사를 닫습니다.

그런 다음 새 프로덕션 프로필을 만들고이를 사용 하 여 프로젝트를 게시 합니다.

**솔루션 탐색기**에서 ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 클릭 합니다.

**프로필** 탭을 선택 합니다.

**가져오기**를 클릭 하 고 앞에서 다운로드 한 publishsettings 파일을 선택 합니다.

**연결** 탭에서 **대상 url** 을 올바른 임시 url로 변경 합니다 .이 예제에서는 http://contosouniversity.com.vserver01.cytanium.com 합니다.

프로필의 이름을 Production로 바꿉니다. ( **프로필** 탭을 선택 하 고 **프로필 관리** 를 클릭 하 여 해당 작업을 수행 합니다.)

**웹 게시** 마법사를 닫고 변경 내용을 저장 합니다.

프로덕션에서 데이터베이스를 업데이트 하는 실제 응용 프로그램에서는 게시 하기 전에 다음과 같은 두 가지 추가 단계를 수행 합니다.

1. [프로덕션 환경에 배포](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) 자습서에 표시 된 대로 *앱\_오프 라인*으로 업로드 합니다.
2. Cytanium 제어판의 **파일 관리자** 기능을 사용 하 여 프로덕션 사이트에서 ContosoUniversity 프로젝트의 *App\_Data* 폴더로 *aspnet-Prod* 및 *School-Prod* 파일을 복사 합니다. 이렇게 하면 새 SQL Server 데이터베이스에 배포 하는 데이터에 프로덕션 웹 사이트에서 수행 하는 최신 업데이트가 포함 됩니다.

웹에서 **게시** 도구 모음을 클릭 한 다음 **프로덕션** 프로필을 선택 했는지 확인 하 고 **게시**를 클릭 합니다.

게시 하기 전에 <em>오프 라인으로\_앱</em> 을 업로드 한 경우 Cytanium 제어판의 <strong>파일 관리자</strong> 유틸리티를 사용 하 여 <em>오프 라인에서 앱\_</em> 를 삭제 해야 합니다. 테스트 하기 전에 htm. 또한 <em>앱\_데이터</em> 폴더에서 <em>.sdf</em> 파일을 삭제할 수도 있습니다.

이제 브라우저를 열고 공용 사이트의 URL로 이동 하 여 테스트 환경에 배포한 후와 동일한 방식으로 응용 프로그램을 테스트할 수 있습니다.

## <a name="switching-to-sql-server-express-localdb-in-development"></a>개발 중인 LocalDB SQL Server Express로 전환

개요에 설명 된 대로 일반적으로 테스트 및 프로덕션 환경에서 사용 하는 것과 동일한 데이터베이스 엔진을 개발에 사용 하는 것이 좋습니다. 개발에 SQL Server Express를 사용 하는 이점은 데이터베이스가 개발, 테스트 및 프로덕션 환경에서 동일 하 게 작동 한다는 것을 명심 해야 합니다. 이 섹션에서는 Visual Studio에서 응용 프로그램을 실행할 때 SQL Server Express LocalDB를 사용 하도록 ContosoUniversity 프로젝트를 설정 합니다.

이 마이그레이션을 수행 하는 가장 간단한 방법은 Code First 하 고 멤버 자격 시스템에서 새로운 개발 데이터베이스를 모두 만드는 것입니다. 이 방법을 사용 하려면 다음 세 단계가 필요 합니다.

1. 새 SQL Express LocalDB 데이터베이스를 지정 하도록 연결 문자열을 변경 합니다.
2. 웹 사이트 관리 도구를 실행 하 여 관리자 사용자를 만듭니다. 그러면 멤버 자격 데이터베이스가 만들어집니다.
3. Code First 마이그레이션 update-database 명령을 사용 하 여 응용 프로그램 데이터베이스를 만들고 초기값을 적용 합니다.

### <a name="updating-connection-strings-in-the-webconfig-file"></a>Web.config 파일에서 연결 문자열 업데이트

*Web.config* 파일을 열고 `connectionStrings` 요소를 다음 코드로 바꿉니다.

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample8.xml)]

### <a name="creating-the-membership-database"></a>멤버 자격 데이터베이스 만들기

**솔루션 탐색기**에서 ContosoUniversity 프로젝트를 선택한 다음 **프로젝트** 메뉴에서 **ASP.NET 구성** 을 클릭 합니다.

보안 탭을 선택합니다.

**역할 만들기 또는 관리**를 클릭 한 다음 **관리자** 역할을 만듭니다.

보안 탭으로 돌아갑니다.

**사용자 만들기**를 클릭 한 다음 **관리자** 확인란을 선택 하 고 admin 이라는 사용자를 만듭니다.

**웹 사이트 관리 도구**를 닫습니다.

### <a name="creating-the-school-database"></a>School 데이터베이스 만들기

패키지 관리자 콘솔 창을 엽니다.

**기본 프로젝트** 드롭다운 목록에서 ContosoUniversity 프로젝트를 선택 합니다.

명령을 입력하십시오.

[!code-powershell[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample9.ps1)]

Code First 마이그레이션는 데이터베이스를 만드는 초기 마이그레이션을 적용 한 다음 AddBirthDate 마이그레이션을 적용 한 후 초기값 메서드를 실행 합니다.

Ctrl 키를 눌러 사이트를 실행 합니다. 테스트 및 프로덕션 환경에서 수행한 것 처럼 **학생 추가** 페이지를 실행 하 고 새 학생을 추가한 다음 **학생** 페이지에서 새 학생을 봅니다. 이렇게 하면 School 데이터베이스가 만들어지고 초기화 되었으며 여기에 대 한 읽기 및 쓰기 권한이 있는지 확인 됩니다.

**크레딧 업데이트** 페이지를 선택 하 고 로그인 하 여 멤버 자격 데이터베이스가 배포 되어 있고 액세스 권한이 있는지 확인 합니다. 사용자 계정을 마이그레이션하지 않은 경우 관리자 계정을 만든 다음, **크레딧 업데이트** 페이지를 선택 하 여 작동 하는지 확인 합니다.

## <a name="cleaning-up-sql-server-compact-files"></a>SQL Server Compact 파일 정리

SQL Server Compact를 지원 하기 위해 포함 된 파일 및 NuGet 패키지는 더 이상 필요 하지 않습니다. 원하는 경우 (이 단계는 필요 하지 않음) 불필요 한 파일 및 참조를 정리할 수 있습니다.

**솔루션 탐색기**에서 *응용 프로그램\_Data* 폴더의 *.sdf* 파일과 *bin* 폴더의 *amd64* 및 *x86* 폴더를 삭제 합니다.

**솔루션 탐색기**에서 솔루션 (프로젝트 중 하나가 아님)을 마우스 오른쪽 단추로 클릭 한 다음 **솔루션에 대 한 NuGet 패키지 관리**를 클릭 합니다.

**NuGet 패키지 관리** 대화 상자의 왼쪽 창에서 **설치 된 패키지**를 선택 합니다.

**SqlServerCompact** 패키지를 선택 하 고 **관리**를 클릭 합니다.

**프로젝트 선택** 대화 상자에서 두 프로젝트를 모두 선택 합니다. 두 프로젝트 모두에서 패키지를 제거 하려면 두 확인란의 선택을 취소 한 다음 **확인**을 클릭 합니다.

종속 패키지를 제거할지 묻는 대화 상자에서 아니요를 클릭 합니다. 다음 중 하나는 유지 해야 하는 Entity Framework 패키지입니다.

동일한 절차에 따라 **SqlServerCompact** 패키지를 제거 합니다. **SqlServerCompact** 패키지는 **SqlServerCompact** 패키지에 종속 되므로이 순서로 패키지를 제거 해야 합니다.

이제 SQL Server Express 및 전체 SQL Server 성공적으로 마이그레이션 되었습니다. 다음 자습서에서는 다른 데이터베이스를 변경 하 고 테스트 및 프로덕션 데이터베이스에서 SQL Server Express 및 전체 SQL Server를 사용 하는 경우 데이터베이스 변경 내용을 배포 하는 방법을 알아봅니다.

> [!div class="step-by-step"]
> [이전](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
> [다음](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)
