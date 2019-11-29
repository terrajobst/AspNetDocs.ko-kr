---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 테스트에 배포 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 ASP.NET 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자 (usin ...)에 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 01/16/2019
ms.assetid: 8bf2c4fb-4ee5-4841-bfc2-03462c1f7a7a
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
msc.type: authoredcontent
ms.openlocfilehash: 738318cce442fdc5d58dd1e4c992d4941be2487e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74591252"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-to-test"></a>Visual Studio를 사용 하 여 ASP.NET 웹 배포: 테스트에 배포

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

이 자습서 시리즈에서는 Visual Studio 2017을 사용 하 여 Azure App Service Web Apps 또는 타사 호스팅 공급자에 ASP.NET 웹 응용 프로그램을 배포 (게시) 하는 방법을 보여 줍니다. 계열에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)를 참조 하십시오.

최신 버전의 Azure에 배포 하는 경우 [azure에서 ASP.NET Core 웹 앱 만들기](/azure/app-service/app-service-web-get-started-dotnet)를 참조 하세요.

## <a name="overview"></a>개요

이 자습서에서는 로컬 컴퓨터의 인터넷 정보 서버 (IIS)에 ASP.NET 웹 응용 프로그램을 배포 합니다.

일반적으로 응용 프로그램을 개발 하는 경우 응용 프로그램을 실행 하 고 Visual Studio에서 테스트 합니다. 기본적으로 Visual Studio 2017의 웹 응용 프로그램 프로젝트는 IIS Express를 개발 웹 서버로 사용 합니다. IIS Express은 기본적으로 Visual Studio 2017에서 사용 하는 Visual Studio 개발 서버 (Cassini 라고도 함) 보다 전체 IIS와 같은 방식으로 작동 합니다. 하지만 개발 웹 서버는 IIS와 똑같이 작동 하지 않습니다. 따라서 앱이 Visual Studio에서 제대로 실행 되 고 테스트 되지만 IIS에 배포 되는 경우 실패 합니다.

다음 두 가지 방법으로 응용 프로그램을 안정적으로 테스트할 수 있습니다.

1. 나중에 프로덕션 환경에 배포 하는 데 사용 하는 것과 동일한 프로세스를 사용 하 여 개발 컴퓨터의 IIS에 응용 프로그램을 배포 합니다.

   웹 프로젝트를 실행할 때 IIS를 사용 하도록 Visual Studio를 구성할 수 있지만 배포 프로세스를 테스트 하지는 않습니다. 이 메서드는 배포 프로세스의 유효성을 검사 하 고 IIS에서 응용 프로그램이 올바르게 실행 되는지 확인 합니다.

2. 프로덕션 환경과 유사한 테스트 환경에 응용 프로그램을 배포 합니다. 
 
   이러한 자습서에 대 한 프로덕션 환경은 Azure App Service Web Apps 됩니다. 이상적인 테스트 환경은 Azure 서비스에서 만들어지는 추가 웹 앱입니다. 프로덕션 웹 앱과 동일한 방식으로 설정 되지만 테스트에만 사용 됩니다.

옵션 2는 가장 안정적으로 테스트할 수 있는 방법입니다. 옵션 2를 사용 하는 경우 옵션 1을 반드시 사용할 필요는 없습니다. 그러나 타사 호스팅 공급자에 배포 하는 경우에는 옵션 2를 사용할 수 없거나 비용이 많이 들 수 있습니다 .이 자습서 시리즈에서는 두 가지 방법을 모두 보여 줍니다. 옵션 2에 대 한 지침은 [프로덕션 환경에 배포](deploying-to-production.md) 자습서에서 제공 됩니다.

Visual Studio에서 웹 서버를 사용 하는 방법에 대 한 자세한 내용은 [ASP.NET 웹 프로젝트용 Visual studio의 웹 서버](https://msdn.microsoft.com/library/58wxa9w5.aspx)를 참조 하세요.

미리 알림: 자습서를 진행할 때 오류 메시지가 표시 되거나 문제가 해결 되지 않으면 [문제 해결 페이지](troubleshooting.md)를 확인 해야 합니다.

## <a name="download-the-contoso-university-starter-project"></a>Contoso 대학 스타터 프로젝트 다운로드

Contoso 대학 Visual Studio 시작 솔루션 및 프로젝트를 다운로드 하 여 설치 합니다. 이 솔루션에는 완료 된 자습서가 포함 되어 있습니다. 

[시작 프로젝트 다운로드](https://go.microsoft.com/fwlink/p/?LinkId=282627)

## <a name="install-iis"></a>IIS 설치

개발 컴퓨터에서 IIS에 배포 하려면 IIS 및 웹 배포 설치 되어 있는지 확인 합니다. 기본적으로 Visual Studio는 웹 배포를 설치 하지만 IIS는 기본 Windows 10, Windows 8 또는 Windows 7 구성에 포함 되지 않습니다. IIS를 이미 설치 했 고 기본 응용 프로그램 풀이 이미 .NET 4로 설정 되어 있는 경우 [다음 섹션](#sqlexpress)으로 건너뜁니다.

1. [WPI (웹 플랫폼 설치 관리자)](https://www.microsoft.com/web/downloads/platform.aspx) 를 사용 하 여 IIS를 설치 하 고 웹 배포 하는 것이 좋습니다. WPI은 IIS를 포함 하는 권장 IIS 구성과 필요한 경우 필수 구성 요소 웹 배포 설치 합니다.

   IIS, 웹 배포 또는 필수 구성 요소 중 하나를 이미 설치한 경우 WPI는 누락 된 항목만 설치 합니다.

   * 웹 플랫폼 설치 관리자를 사용 하 여 IIS 및 웹 배포를 설치 합니다.
    
     ![WPI를 사용 하 여 IIS 설치](deploying-to-iis/_static/image30.png)

     ![WPI를 사용 하 여 웹 배포 설치](deploying-to-iis/_static/image31.png)

     IIS 7이 설치 됨을 나타내는 메시지가 표시 됩니다. 이 링크는 Windows 8에서 IIS 8에 대해 작동 합니다. 그러나 Windows 8 이상에서는 다음 단계를 수행 하 여 ASP.NET 4.7가 설치 되어 있는지 확인 합니다.

   * **제어판** **을 열고 프로그램 및 기능** ** > ** **Windows 기능을 설정 하거나 해제** >  > 합니다.

   * **인터넷 정보 서비스**, **World Wide Web 서비스**및 **응용 프로그램 개발 기능**을 확장 합니다.
   
   * **ASP.NET 4.7** 이 선택 되어 있는지 확인 합니다.

     ![ASP.NET 4.7 선택](deploying-to-iis/_static/image1a.png)

   * **World Wide Web Services** 및 **IIS 관리 콘솔이** 선택 되어 있는지 확인 합니다. 그러면 IIS 및 IIS 관리자가 설치 됩니다.
    
     ![World Wide Web 서비스 선택](deploying-to-iis/_static/image24.png)    
  
   * **확인**을 선택합니다. 설치가 진행 중임을 나타내는 대화 상자 메시지가 표시 됩니다.

IIS를 설치한 후 **Iis 관리자** 를 실행 하 여 .NET Framework 버전 4가 기본 응용 프로그램 풀에 할당 되었는지 확인 합니다.

1. WINDOWS + R을 눌러 **실행** 대화 상자를 엽니다.

   Windows 8 이상에서는 **시작** 페이지에 "실행"을 입력 합니다. Windows 7의 경우 **시작** 메뉴에서 **실행** 을 선택 합니다. **시작** 메뉴에 **실행** 이 없으면 작업 표시줄을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택한 다음 **시작 메뉴** 탭을 선택 하 고 **사용자 지정**을 선택 하 고 **명령 실행**을 선택 합니다.

2. "Inetmgr"을 입력 하 고 **확인을**선택 합니다.

3. **연결** 창에서 서버 노드를 확장 하 고 **응용 프로그램 풀**을 선택 합니다. 다음 그림과 같이 **DefaultAppPool** 이 .net framework 버전 4에 할당 된 경우 **응용 프로그램 풀** 창에서 다음 섹션으로 건너뜁니다.

   ![Inetmgr_showing_4 0_app_pools](deploying-to-iis/_static/image5a.png)

4. 응용 프로그램 풀이 두 개만 표시 되 고 둘 다 .NET Framework 2.0로 설정 된 경우 IIS에 ASP.NET 4를 설치 합니다.

   Windows 8 이상에서는 ASP.NET 4.7가 설치 되어 있는지 확인 하는 방법에 대 한 이전 섹션의 지침을 참조 하거나 [windows 8 및 Windows Server 2012에 ASP.NET 4.5을 설치 하는 방법](https://support.microsoft.com/kb/2736284)을 참조 하세요. Windows 7의 경우 Windows **시작** 메뉴에서 **명령 프롬프트** 를 마우스 오른쪽 단추로 클릭 하 고 **관리자 권한으로 실행**을 선택 하 여 명령 프롬프트 창을 엽니다. 다음 명령을 사용 하 여 IIS에 ASP.NET 4를 설치 하려면 다음과 같이 [aspnet\_](https://msdn.microsoft.com/library/k6h9cz8h.aspx) 를 실행 합니다. 32 비트 시스템에서는 "Framework64"를 "Framework"로 바꿉니다.

   [!code-console[Main](deploying-to-iis/samples/sample1.cmd)]

   이 명령은 .NET Framework 4에 대해 새 응용 프로그램 풀을 만들지만 기본 응용 프로그램 풀은 2.0로 설정 된 상태를 유지 합니다. .NET 4를 대상으로 하는 응용 프로그램을 해당 응용 프로그램 풀에 배포 하는 중 이므로 응용 프로그램 풀을 .NET 4로 변경 합니다.

5. **IIS 관리자**를 닫은 경우 다시 실행 하 고 서버 노드를 확장 한 다음 **응용 프로그램 풀**을 선택 합니다.

6. **응용 프로그램 풀** 창에서 **DefaultAppPool**을 선택 합니다. **작업** 창에서 **기본 설정**을 선택 합니다.

   ![Inetmgr_selecting_Basic_Settings_for_app_pool](deploying-to-iis/_static/image25.png)

7. **응용 프로그램 풀 편집** 대화 상자에서 **.net clr 버전** 을 **.net clr v 4.0.30319**로 변경 합니다. **확인**을 선택합니다.

   ![Selecting_ NET_4_for_DefaultAppPool](deploying-to-iis/_static/image6a.png)

이제 웹 응용 프로그램을 IIS에 게시할 준비가 되었습니다. 그러나 먼저 테스트를 위한 데이터베이스를 만듭니다.

<a id="sqlexpress"></a>

## <a name="install-sql-server-express"></a>SQL Server Express 설치

LocalDB는 IIS에서 작동 하도록 설계 되지 않았으므로 테스트 환경에 SQL Server Express 설치 되어 있어야 합니다. Visual Studio 2010 SQL Server Express를 사용 하는 경우 이미 기본적으로 설치 되어 있습니다. Visual Studio 2012 이상 버전을 사용 하는 경우 SQL Server Express를 설치 합니다.

SQL Server Express를 설치 하려면 [다운로드 센터: Microsoft SQL Server 2017 Express edition](https://www.microsoft.com/sql-server/sql-server-editions-express)에서 다운로드 하 여 설치 합니다. 

SQL Server 설치 센터의 첫 페이지에서 **새로 만들기 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가** 를 선택 하 고 지침에 따라 기본 선택 항목을 적용 합니다. 설치 마법사에서 기본 설정을 적용 합니다. 설치 옵션에 대 한 자세한 내용은 설치 [마법사에서 SQL Server 설치 (설치 프로그램)](https://msdn.microsoft.com/library/ms143219.aspx)를 참조 하세요.

## <a name="create-sql-server-express-databases-for-the-test-environment"></a>테스트 환경에 대 한 SQL Server Express 데이터베이스 만들기

Contoso 대학 응용 프로그램에는 두 개의 데이터베이스가 있습니다. 

1. 멤버 자격 데이터베이스 
2. 응용 프로그램 데이터베이스 

이러한 데이터베이스를 두 개의 개별 데이터베이스나 단일 데이터베이스에 배포할 수 있습니다. 이러한 항목을 결합 하면 데이터베이스 간 조인이 쉬워집니다. 

타사 호스팅 공급자에 배포 하는 경우 호스팅 계획에서 결합 해야 할 수도 있습니다. 예를 들어 공급자가 여러 데이터베이스에 대해 더 많은 요금을 청구 하거나 둘 이상의 데이터베이스를 허용 하지 않을 수도 있습니다.

이 자습서에서는 테스트 환경의 두 데이터베이스와 스테이징 및 프로덕션 환경에 있는 하나의 데이터베이스에 배포 합니다.

Visual Studio의 **보기** 메뉴에서 **서버 탐색기** (visual Web Developer의**데이터베이스 탐색기** )를 선택 합니다. **데이터 연결** 을 마우스 오른쪽 단추로 클릭 하 고 **새 SQL Server 데이터베이스 만들기**를 선택 합니다.

![Selecting_Create_New_SQL_Server_Database](deploying-to-iis/_static/image8.png)

**새 SQL Server 데이터베이스 만들기** 대화 상자에서 **서버 이름** 상자에 ".\SQLExpress"를 입력 하 고 **새 데이터베이스 이름** 상자에 "ContosoUniversity"을 입력 합니다. **확인**을 선택합니다.

![Aspnet-ContosoUniversity 만들기](deploying-to-iis/_static/image9.png)

동일한 절차에 따라 `ContosoUniversity`라는 새 SQL Server Express School 데이터베이스를 만듭니다.

**서버 탐색기** 는 두 개의 새 데이터베이스를 보여 줍니다.

![서버 탐색기의 새 데이터베이스](deploying-to-iis/_static/image10.png)

## <a name="create-a-grant-script-for-the-new-databases"></a>새 데이터베이스에 대 한 grant 스크립트 만들기

응용 프로그램이 개발 컴퓨터의 IIS에서 실행 되는 경우 응용 프로그램은 기본 응용 프로그램 풀의 자격 증명을 사용 하 여 데이터베이스에 액세스 합니다. 그러나 기본적으로 응용 프로그램 풀에는 데이터베이스를 열 수 있는 권한이 없습니다. 이는 해당 사용 권한을 부여 하기 위해 스크립트를 실행 해야 함을 의미 합니다. 이 섹션에서는 해당 스크립트를 만들고 나중에 실행 하 여 응용 프로그램이 IIS에서 실행 될 때 데이터베이스를 열 수 있는지 확인 합니다.

텍스트 편집기에서 다음 SQL 명령을 새 파일에 복사 하 고 *Grant .sql*로 저장 합니다. 

[!code-sql[Main](deploying-to-iis/samples/sample2.sql)]

Visual Studio에서 Contoso 대학 솔루션을 엽니다. 프로젝트 중 하나가 아닌 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **추가**를 선택 합니다. **기존 항목**을 선택 하 고 *Grant .sql*로 이동 하 여 엽니다.

> [!NOTE]
> 이 스크립트는이 자습서에 지정 된 대로 2012 이상 및 Windows 10, Windows 8 또는 Windows 7의 IIS 설정에서 SQL Server Express 사용할 수 있도록 설계 되었습니다. 다른 버전의 SQL Server 또는 Windows를 사용 하는 경우 또는 컴퓨터에 IIS를 다르게 설정 하는 경우이 스크립트를 변경 해야 할 수 있습니다. SQL Server 스크립트에 대 한 자세한 내용은 [SQL Server 온라인 설명서](https://go.microsoft.com/fwlink/?LinkId=132511)을 참조 하십시오.

> [!NOTE] 
> **보안 정보** 이 스크립트는 런타임에 데이터베이스에 액세스 하는 사용자에 게 `db_owner` 권한을 제공 하며,이는 프로덕션 환경에 포함 됩니다. 일부 시나리오에서는 배포에 대해서만 전체 데이터베이스 스키마 업데이트 권한이 있는 사용자를 지정 하 고 데이터를 읽고 쓸 수 있는 권한만 있는 다른 사용자를 런타임에 지정할 수 있습니다. 자세한 내용은이 자습서의 뒷부분에 나오는 [Code First 마이그레이션의 자동 Web.config 변경 내용 검토](#reviewingmigrations) 를 참조 하세요.

<a id="publish"></a>

## <a name="run-the-grant-script-in-the-application-database"></a>응용 프로그램 데이터베이스에서 grant 스크립트 실행

데이터베이스 배포에서 [dbDacFx](https://docs.microsoft.com/iis/publish/using-web-deploy/dbdacfx-provider-for-incremental-database-publishing) 공급자를 사용 하므로 배포 중에 멤버 자격 데이터베이스에서 grant 스크립트를 실행 하도록 게시 프로필을 구성할 수 있습니다. 응용 프로그램 데이터베이스를 배포 하는 방법 인 Code First 마이그레이션 배포 중에는 스크립트를 실행할 수 없습니다. 즉, 응용 프로그램 데이터베이스에서 배포 하기 전에 스크립트를 수동으로 실행 해야 합니다.

1. Visual Studio에서 이전에 만든 *Grant .sql* 파일을 엽니다.

2. **연결**을 선택 합니다. 

    ![연결 단추](deploying-to-iis/_static/image11.png)

3. **서버에 연결** 대화 상자에서 **서버 이름**으로 *.\SQLExpress* 을 입력 합니다. **연결**을 선택 합니다.

4. 데이터베이스 드롭다운 목록에서 **ContosoUniversity**를 선택 합니다. **실행**을 선택 합니다. 

   ![](deploying-to-iis/_static/image12.png)

이제 응용 프로그램을 실행할 때 데이터베이스 테이블을 만들 수 있도록 응용 프로그램 데이터베이스에서 기본 응용 프로그램 풀 id에 충분 한 권한이 Code First 마이그레이션.

## <a name="publish-to-iis"></a>IIS에 게시

Visual Studio 및 웹 배포를 사용 하 여 IIS에 배포 하는 방법에는 여러 가지가 있습니다.

* Visual Studio one 클릭 게시를 사용 합니다.
* 명령줄에서 게시 합니다.
* 배포 패키지를 만들고 IIS 관리자를 사용 하 여 설치 합니다. 패키지에는 IIS에 사이트를 설치 하는 데 필요한 모든 파일 및 메타 데이터를 포함 하는 .zip 파일이 있습니다.
* 배포 패키지를 만들고 명령줄을 사용 하 여 설치 합니다.

배포 작업을 자동화 하기 위해 Visual Studio를 설정 하는 이전 자습서에서 수행한 프로세스는 이러한 모든 메서드에 적용 됩니다. 이러한 자습서에서는 처음 두 가지 방법을 사용 합니다. 배포 패키지를 사용 하는 방법에 대 한 자세한 내용은 Visual Studio 및 ASP.NET 용 웹 배포 콘텐츠 맵에서 [웹 배포 패키지를 만들고 설치 하 여 웹 응용 프로그램 배포](https://go.microsoft.com/fwlink/p/?LinkId=282413#package) 를 참조 하세요.

게시 하기 전에 관리자 모드에서 Visual Studio를 실행 하 고 있는지 확인 합니다. 제목 표시줄에 **(관리자)** 가 표시 되지 않으면 Visual Studio를 닫습니다. Windows 8 이상 **시작** 페이지 또는 Windows 7 **시작** 메뉴에서 Visual Studio 아이콘을 마우스 오른쪽 단추로 클릭 하 고 **관리자 권한으로 실행**을 선택 합니다. 관리자 모드는 로컬 컴퓨터의 IIS에 게시 하는 경우에만 게시 해야 합니다.

### <a name="create-the-publish-profile"></a>게시 프로필 만들기

1. **솔루션 탐색기**에서 **ContosoUniversity** 프로젝트가 아닌 **ContosoUniversity** 프로젝트를 마우스 오른쪽 단추로 클릭 합니다. **게시**를 선택합니다. **게시** 페이지가 나타납니다.

2. **새 프로필**을 선택 합니다. **게시 대상 선택** 대화 상자가 나타납니다.

3. **IIS, FTP 등을**선택 합니다. **프로필 만들기**를 선택 합니다. **게시** 마법사가 나타납니다.

   ![웹 게시 마법사 프로필 탭](deploying-to-iis/_static/image26.png)

4. **게시 방법** 드롭다운 메뉴에서 **웹 배포**를 선택 합니다.

5. **서버**에 *localhost*를 입력 합니다.

6. **사이트 이름**에는 *기본 웹 사이트/ContosoUniversity*를 입력 합니다.

7. **대상 URL**에 *http://localhost/ContosoUniversity* 을 입력 합니다.

   **대상 URL** 설정은 필요 하지 않습니다. Visual Studio에서 응용 프로그램 배포를 마치면이 URL에 대 한 기본 브라우저가 자동으로 열립니다. 배포 후 브라우저를 자동으로 열지 않으려면이 상자를 비워 둡니다.

8. **연결 유효성 검사** 를 선택 하 여 설정이 올바른지 확인 하 고 로컬 컴퓨터의 IIS에 연결할 수 있습니다.

   녹색 확인 표시는 연결에 성공 했는지 확인 합니다.

   ![웹 게시 마법사 연결 탭](deploying-to-iis/_static/image27.png)

9. **다음** 을 선택 하 여 **설정** 탭으로 이동 합니다.

10. **구성** 드롭다운 상자는 배포할 빌드 구성을 지정 합니다. 기본값인 **Release**로 설정 된 상태로 둡니다. 이 자습서에서는 디버그 빌드를 배포 하지 않습니다.

11. **파일 게시 옵션**을 확장 합니다. **앱\_데이터 폴더에서 파일 제외를**선택 합니다.

    테스트 환경에서 응용 프로그램은 응용 프로그램 *\_Data* 폴더의 .mdf 파일이 아니라 로컬 SQL Server Express 인스턴스에서 만든 데이터베이스에 액세스 합니다.

12. 게시 하 **는 동안 미리 컴파일** 을 그대로 두고 **대상에서 추가 파일 제거** 확인란의 선택을 취소 합니다.

    ![설정 탭의 파일 게시 옵션](deploying-to-iis/_static/image15a.png)

    미리 컴파일하면 주로 규모가 많은 사이트에 유용한 옵션입니다. 사이트가 게시 된 후 페이지가 처음으로 요청 될 때 시작 시간을 줄일 수 있습니다.

    첫 번째 배포이 고 대상 폴더에 아직 파일이 없기 때문에 추가 파일을 제거할 필요가 없습니다.

    > [!NOTE] 
    > 동일한 사이트에 대 한 후속 배포를 위해 **대상에서 추가 파일 제거** 를 선택 하는 경우 미리 보기 기능을 사용 하 여를 배포 하기 전에 파일이 삭제 되는 것을 미리 확인할 수 있도록 해야 합니다. 예상 되는 동작은 웹 배포가 프로젝트에서 삭제 한 대상 서버에서 파일을 삭제 하는 것입니다. 그러나 원본 및 대상 폴더 아래의 전체 폴더 구조는 비교 됩니다. 일부 시나리오에서는 삭제 하지 않을 파일을 웹 배포 삭제할 수 있습니다.
    > 
    > 예를 들어 루트 폴더에 프로젝트를 배포할 때 서버의 하위 폴더에 웹 응용 프로그램이 있는 경우 하위 폴더가 삭제 됩니다. Contoso.com에 기본 사이트에 대 한 프로젝트가 하나 있고 contoso.com/blog에 블로그의 다른 프로젝트가 있을 수 있습니다. 블로그 응용 프로그램은 하위 폴더에 있습니다. 기본 사이트를 배포할 때 **대상에서 추가 파일 제거** 를 선택 하면 블로그 응용 프로그램이 삭제 됩니다.
    > 
    > 또 다른 예로, 응용 프로그램\_데이터 폴더는 예기치 않게 삭제 될 수 있습니다. SQL Server Compact와 같은 특정 데이터베이스는 응용 프로그램\_데이터 폴더에 데이터베이스 파일을 저장 합니다. 초기 배포 후에 후속 배포에서 데이터베이스 파일을 복사 하는 것을 원하지 않으므로 패키지/웹 게시 탭에서 **앱\_데이터 제외** 를 선택 합니다. 선택한 **대상에서 추가 파일을 제거** 하는 경우 다음에 게시할 때 데이터베이스 파일과 앱\_데이터 폴더 자체가 삭제 됩니다.

### <a name="configure-deployment-for-the-membership-database"></a>멤버 자격 데이터베이스에 대 한 배포 구성

다음 단계는 대화 상자의 **데이터베이스** 섹션에서 **defaultconnection** 데이터베이스에 적용 됩니다.

1. **원격 연결 문자열** 상자에 새 SQL Server Express 멤버 자격 데이터베이스를 가리키는 다음 연결 문자열을 입력 합니다.

   [!code-console[Main](deploying-to-iis/samples/sample3.cmd)]

   **런타임에이 연결 문자열 사용** 을 선택 했기 때문에 배포 프로세스는 배포 된 web.config 파일에이 연결 문자열을 넣습니다.

    **서버 탐색기**에서 연결 문자열을 가져올 수도 있습니다. **서버 탐색기**에서 **데이터 연결** 을 확장 하 고 **&lt;machinename&gt;\Sqlexpress.aspnet-ContosoUniversity** 데이터베이스를 선택한 다음 **속성** 창에서 **연결 문자열** 값을 복사 합니다. 이 연결 문자열에는 `Pooling=False`삭제할 수 있는 추가 설정이 하나 있습니다.

2. **데이터베이스 업데이트**를 선택 합니다.

   이로 인해 배포 중에 대상 데이터베이스에 데이터베이스 스키마가 생성 됩니다. 다음 단계에서는 실행 해야 하는 추가 스크립트를 지정 합니다. 하나는 기본 응용 프로그램 풀에 대 한 데이터베이스 액세스 권한을 부여 하 고 다른 하나는 데이터를 배포 합니다.

3. **데이터베이스 업데이트 구성**을 선택 합니다.
 
4. **데이터베이스 업데이트 구성** 대화 상자에서 **SQL 스크립트 추가**를 선택 합니다. 이전에 솔루션 폴더에 저장 한 *Grant .sql* 스크립트로 이동 합니다.

5. 프로세스를 반복 하 여 *aspnet-data-dev* 스크립트를 추가 합니다.

   ![멤버 자격 데이터베이스에 대 한 데이터베이스 업데이트 구성](deploying-to-iis/_static/image16.png)

6. **닫기**를 선택합니다.

### <a name="configure-deployment-for-the-application-database"></a>응용 프로그램 데이터베이스에 대 한 배포 구성

Visual Studio는 Entity Framework `DbContext` 클래스를 검색 하면 **데이터베이스 업데이트** 확인란 대신 **Code First 마이그레이션 실행** 확인란이 있는 **데이터베이스** 섹션에 항목을 만듭니다. 이 자습서에서는이 확인란을 사용 하 여 Code First 마이그레이션 배포를 지정 합니다.

일부 시나리오에서는 `DbContext` 데이터베이스를 사용 하 고 있지만 마이그레이션 대신 dbDacFx 공급자를 사용 하 여 데이터베이스를 배포 하려는 경우가 있습니다. 이 경우 MSDN의 ASP.NET 웹 배포 FAQ에서 [마이그레이션을 사용 하지 않고 Code First 데이터베이스 배포를 어떻게 할까요?](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) 참조 하세요.

다음 단계는 대화 상자의 **데이터베이스** 섹션에 있는 **schoolcontext.cs** 데이터베이스에 적용 됩니다.

1. **원격 연결 문자열** 상자에 새 SQL Server Express 응용 프로그램 데이터베이스를 가리키는 다음 연결 문자열을 입력 합니다.

   [!code-console[Main](deploying-to-iis/samples/sample4.cmd)]

   **런타임에이 연결 문자열 사용** 을 선택 했기 때문에 배포 프로세스는 배포 된 web.config 파일에이 연결 문자열을 넣습니다.

   또한 멤버 자격 데이터베이스 연결 문자열을 가져오는 것과 같은 방법으로 **서버 탐색기** 에서 응용 프로그램 데이터베이스 연결 문자열을 가져올 수 있습니다.

2. **Code First 마이그레이션 실행 (응용 프로그램 시작 시 실행)** 을 선택 합니다.

   이 옵션을 선택 하면 배포 프로세스에서 배포 된 Web.config 파일을 구성 하 여 `MigrateDatabaseToLatestVersion` 이니셜라이저를 지정 합니다. 이 이니셜라이저는 응용 프로그램이 배포 후 처음으로 데이터베이스에 액세스 하는 경우 데이터베이스를 최신 버전으로 자동으로 업데이트 합니다.

### <a name="configure-publish-profile-transforms"></a>게시 프로필 변환 구성

1. **닫기**를 선택합니다. 변경 내용을 저장할 것인지 묻는 메시지가 표시 되 면 **예** 를 선택 합니다.

2. **솔루션 탐색기**에서 **속성**, 기타 **프로필**을 차례로 확장 합니다.

3. *Customprofile. pubxml* 을 마우스 오른쪽 단추로 클릭 하 고 이름을 *Test. pubxml*로 바꿉니다.

4. *테스트 pubxml*을 마우스 오른쪽 단추로 클릭 합니다. **구성 변환 추가**를 선택 합니다.

   ![구성 변환 메뉴 추가](deploying-to-iis/_static/image17.png)

   Visual Studio에서 web.config *변환 파일을 만들고* 엽니다.

5. *Web.config* 변환 파일에서 열기 구성 태그 바로 뒤에 다음 코드를 삽입 합니다.

   [!code-xml[Main](deploying-to-iis/samples/sample5.xml)]

    테스트 게시 프로필을 사용 하는 경우이 변환은 환경 표시기를 "Test"로 설정 합니다. 배포 된 사이트에 "Contoso 대학" H1 제목 뒤에 "(테스트)"가 표시 됩니다.

6. 파일을 저장한 후 닫습니다.

7. *Web.config* 파일을 마우스 오른쪽 단추로 클릭 하 고 **변환 미리 보기** 를 선택 하 여 코딩 된 변환이 필요한 변경 내용을 생성 하는지 확인 합니다.

    Web.config **미리 보기** 창에는 *web.config 변환과 web.config* 변환을 모두 적용 한 결과가 표시 *됩니다.*

### <a name="preview-the-deployment-updates"></a>배포 업데이트 미리 보기

1. **웹 게시** 마법사를 다시 엽니다. ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**, **미리 보기**를 차례로 선택 합니다.

2. **미리** 보기 대화 상자에서 **미리 보기 시작** 을 선택 하 여 복사할 파일의 목록을 표시 합니다. 

   ![게시 미리 보기](deploying-to-iis/_static/image29.png)

   **데이터베이스 미리 보기** 링크를 선택 하 여 멤버 자격 데이터베이스에서 실행할 스크립트를 볼 수도 있습니다. Code First 마이그레이션 배포에 대해 스크립트가 실행 되지 않으므로 응용 프로그램 데이터베이스에 대 한 미리 보기는 없습니다.

3. **게시**를 선택합니다.

   Visual Studio가 관리자 모드가 아니면 사용 권한 오류 메시지가 나타날 수 있습니다. 이 경우 Visual Studio를 닫고 관리자 모드에서 연 다음 다시 게시 해 보세요.

   Visual Studio가 관리자 모드에 있으면 **출력** 창에서 성공한 빌드 및 게시를 보고 합니다.

   ![Output_window_publish_Test](deploying-to-iis/_static/image20.png)

   게시 프로필 **연결** 탭의 **대상 URL** 상자에 URL을 입력 한 경우 브라우저는 컴퓨터의 IIS에서 실행 되는 Contoso 대학 홈 페이지에 자동으로 열립니다.

## <a name="test-in-the-test-environment"></a>테스트 환경에서 테스트

환경 표시기는 환경 표시기에 대 한 *web.config 변환이 성공* 했음을 보여 주는 "(Dev)" 대신 "(테스트)"를 표시 합니다.

**강사 페이지를** 실행 하 여 Code First가 강사 데이터로 데이터베이스를 시드 하는지 확인 합니다. Code First 데이터베이스를 만든 다음 `Seed` 메서드를 실행 하기 때문에이 페이지를 선택 하면 로드 하는 데 몇 분 정도 걸릴 수 있습니다. 응용 프로그램이 아직 데이터베이스에 액세스를 시도 하지 않았기 때문에 홈 페이지에 있는 경우에는이 작업을 수행 하지 않습니다.

**학생** 탭을 선택 하 여 배포 된 데이터베이스에 학생이 없는 경우를 확인 합니다.

**학생** 메뉴에서 **학생 추가** 를 선택 합니다. 학생을 추가한 다음 **학생** 페이지에서 새 학생을 봅니다. 이는 데이터베이스에 성공적으로 쓸 수 있는지 확인 합니다.

**과정** 메뉴에서 **크레딧 업데이트**를 선택 합니다. [ **크레딧 업데이트** ] 페이지에는 관리자 권한이 필요 하므로 **로그인** 페이지가 표시 됩니다. 이전에 만든 관리자 계정 자격 증명 ("admin" 및 "devpwd")을 입력 합니다. [ **크레딧 업데이트** ] 페이지가 표시 됩니다. 이렇게 하면 이전 자습서에서 만든 관리자 계정이 테스트 환경에 올바르게 배포 되었는지 확인 합니다.

*C:\inetpub\wwwroot\ContosoUniversity* 폴더에 해당 하는 자리 표시자 파일만 포함 된 *ELMAH* 폴더가 있는지 확인 합니다.

<a id="reviewingmigrations"></a>

## <a name="review-the-automatic-webconfig-changes-for-code-first-migrations"></a>Code First 마이그레이션에 대 한 자동 web.config 변경 내용 검토

*C:\inetpub\wwwroot\ContosoUniversity* 에서 배포 된 응용 프로그램의 *web.config* 파일을 열고 배포 프로세스가 Code First 마이그레이션 구성 된 위치를 확인 하 여 데이터베이스를 최신 버전으로 자동으로 업데이트할 수 있습니다.

![](deploying-to-iis/_static/image21.png)

또한 배포 프로세스에서는 데이터베이스 스키마를 업데이트 하는 데 독점적으로 사용할 Code First 마이그레이션에 대 한 새 연결 문자열을 만들었습니다.

![연결 문자열 Database_Publish](deploying-to-iis/_static/image22.png)

이 추가 연결 문자열을 사용 하 여 데이터베이스 스키마 업데이트에 대 한 사용자 계정과 응용 프로그램 데이터 액세스에 대 한 다른 사용자 계정을 지정할 수 있습니다. 예를 들어 db **\_소유자** 역할을 **db\_datawriter 여부** 역할을 사용 하 여 응용 프로그램에 Code First 마이그레이션 및 **db\_datareader** 에 할당할 수 있습니다. 응용 프로그램의 잠재적으로 악의적인 코드가 데이터베이스 스키마를 변경 하지 못하도록 하는 일반적인 심층 방어 패턴입니다. 예를 들어이 문제는 SQL 삽입 공격이 성공할 때 발생할 수 있습니다. 이러한 자습서에서는이 패턴을 사용 하지 않습니다. 시나리오에서이 패턴을 구현 하려면 다음 단계를 수행 합니다.

1. **웹 게시** 마법사의 **설정** 탭에서 전체 데이터베이스 스키마 업데이트 권한을 가진 사용자를 지정 하는 연결 문자열을 입력 합니다. **런타임에이 연결 문자열 사용** 확인란의 선택을 취소 합니다. 배포 된 web.config 파일에서는 `DatabasePublish` 연결 문자열이 됩니다.

2. 응용 프로그램에서 런타임에 사용 하려는 연결 문자열에 대 한 web.config 파일 변환을 만듭니다.

## <a name="summary"></a>요약

이제 개발 컴퓨터의 IIS에 응용 프로그램을 배포 하 고 테스트 했습니다.

![테스트의 홈 페이지](deploying-to-iis/_static/image23.png)

이렇게 하면 배포 프로세스가 응용 프로그램의 콘텐츠를 올바른 위치 (배포 하지 않으려는 파일 제외)에 복사 하 고 배포 중에 IIS를 올바르게 구성 웹 배포 확인 됩니다. 다음 자습서에서는 아직 수행 되지 않은 배포 작업을 찾는 테스트를 하나 더 실행 합니다. *느릅나무 ah* 폴더에 대 한 폴더 사용 권한을 설정 합니다.

## <a name="more-information"></a>추가 정보

Visual Studio에서 IIS 또는 IIS Express를 실행 하는 방법에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- IIS.net 사이트에 대 한 [개요를 IIS Express](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) 합니다.
- Scott Guthrie의 블로그에서 [IIS Express 소개](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) .
- [Visual Studio에서 ASP.NET 웹 프로젝트용 웹 서버](https://msdn.microsoft.com/library/58wxa9w5.aspx).
- [IIS와](../../older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md) ASP.NET 사이트의 ASP.NET 개발 서버의 핵심 차이점

응용 프로그램이 보통 신뢰 수준으로 실행 될 때 발생할 수 있는 문제에 대 한 자세한 내용은 Rolla 사이트에서 4 명의 회사에서 [ASP.NET 응용 프로그램을 Medium trust로 호스팅](http://www.4guysfromrolla.com/articles/100307-1.aspx) 을 참조 하세요.

> [!div class="step-by-step"]
> [이전](project-properties.md)
> [다음](setting-folder-permissions.md)
