---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12
title: 'Visual Studio 또는 Visual Web Developer를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: IIS에 테스트 환경으로 배포-5/12 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 Visual Stu ...를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 493b2a66-816c-485c-8315-952ed1085ccc
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12
msc.type: authoredcontent
ms.openlocfilehash: 5d85232ff2cb229d771d517db7173721c9e277bf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515681"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-to-iis-as-a-test-environment---5-of-12"></a>Visual Studio 또는 Visual Web Developer를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: IIS에 테스트 환경으로 배포-5/12

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 이 자습서 시리즈에서는 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC for Web을 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다. 웹 게시 업데이트를 설치 하는 경우 Visual Studio 2010을 사용할 수도 있습니다. 시리즈에 대 한 소개는 [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)를 참조 하십시오.
> 
> Visual Studio 2012의 RC 릴리스 후에 도입 된 배포 기능을 보여 주는 자습서는 SQL Server Compact 이외의 SQL Server 버전을 배포 하는 방법을 보여 주고 Azure App Service Web Apps에 배포 하는 방법을 보여 줍니다. [Visual Studio를 사용 하 여 ASP.NET 웹 배포](../../deployment/visual-studio-web-deployment/introduction.md)를 참조 하세요.

## <a name="overview"></a>개요

이 자습서에서는 로컬 컴퓨터의 IIS에 ASP.NET 웹 응용 프로그램을 배포 하는 방법을 보여 줍니다.

응용 프로그램을 개발 하는 경우 일반적으로 Visual Studio에서 실행 하 여 테스트 합니다. 기본적으로 Visual Studio 개발 서버 (Cassini 라고도 함)를 사용 하 고 있음을 의미 합니다. Visual Studio 개발 서버을 사용 하면 Visual Studio에서 개발 하는 동안 쉽게 테스트할 수 있지만 IIS와 똑같이 작동 하지 않습니다. 결과적으로, Visual Studio에서 테스트 하는 경우 응용 프로그램이 올바르게 실행 될 수 있지만 호스팅 환경에서 IIS에 배포 하면 실패 합니다.

다음과 같은 방법으로 응용 프로그램을 보다 안정적으로 테스트할 수 있습니다.

1. 개발 하는 동안 Visual Studio에서 테스트 하는 경우 Visual Studio 개발 서버 대신 IIS Express 또는 전체 IIS를 사용 합니다. 이 메서드는 일반적으로 IIS에서 사이트를 실행 하는 방법을 보다 정확 하 게 에뮬레이트합니다. 그러나이 방법은 배포 프로세스를 테스트 하거나 배포 프로세스의 결과가 올바르게 실행 되는지 확인 하지 않습니다.
2. 나중에 프로덕션 환경에 배포 하는 데 사용 하는 것과 동일한 프로세스를 사용 하 여 개발 컴퓨터의 IIS에 응용 프로그램을 배포 합니다. 이 메서드는 IIS에서 응용 프로그램이 올바르게 실행 되는지 확인 하는 것 외에도 배포 프로세스의 유효성을 검사 합니다.
3. 프로덕션 환경에 최대한 가까운 테스트 환경에 응용 프로그램을 배포 합니다. 이러한 자습서의 프로덕션 환경은 타사 호스팅 공급자 이므로 이상적인 테스트 환경은 호스팅 공급자를 사용 하는 두 번째 계정일 수 있습니다. 이 두 번째 계정은 테스트에만 사용 되지만 프로덕션 계정과 동일한 방식으로 설정 됩니다.

이 자습서에서는 옵션 2에 대 한 단계를 보여 줍니다. 옵션 3에 대 한 지침은 [프로덕션 환경에 배포](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) 자습서의 끝에 제공 되며이 자습서의 끝 부분에서는 옵션 1에 대 한 리소스 링크를 제공 합니다.

미리 알림: 자습서를 진행할 때 오류 메시지가 표시 되거나 문제가 해결 되지 않으면 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)를 확인 해야 합니다.

## <a name="configuring-the-application-to-run-in-medium-trust"></a>보통 신뢰 수준에서 실행 되도록 응용 프로그램 구성

IIS를 설치 하 고 배포 하기 전에 일반적으로 공유 되는 호스팅 환경에서와 같은 방식으로 사이트를 실행 하도록 web.config 파일 설정을 변경 합니다.

일반적으로 호스트 공급자는 *보통 신뢰 수준*에서 웹 사이트를 실행 합니다. 즉, 일부 작업은 허용 되지 않습니다. 예를 들어 응용 프로그램 코드는 Windows 레지스트리에 액세스할 수 없고 응용 프로그램의 폴더 계층 구조 외부에 있는 파일을 읽거나 쓸 수 없습니다. 기본적으로 응용 프로그램은 로컬 컴퓨터에서 *높은 신뢰 수준* 으로 실행 됩니다. 즉, 응용 프로그램이 프로덕션 환경에 배포할 때 실패 하는 작업을 수행할 수 있습니다. 따라서 테스트 환경에 프로덕션 환경이 더 정확 하 게 반영 되도록 하려면 보통 신뢰 수준에서 실행 되도록 응용 프로그램을 구성 합니다.

응용 프로그램 Web.config 파일에서 다음 예제와 같이 **system.web** 요소에 **trust** 요소를 추가 합니다.

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample1.xml?highlight=4)]

이제 응용 프로그램은 로컬 컴퓨터 에서도 IIS의 보통 신뢰 수준으로 실행 됩니다. 이 설정을 사용 하면 응용 프로그램 코드에서 프로덕션에 실패 하는 작업을 수행 하는 모든 시도를 가능한 한 빨리 파악할 수 있습니다.

> [!NOTE]
> Entity Framework Code First 마이그레이션를 사용 하는 경우 버전 5.0 이상을 설치 했는지 확인 합니다. Entity Framework 버전 4.3에서는 마이그레이션에 데이터베이스 스키마를 업데이트 하기 위해 완전 신뢰가 필요 합니다.

## <a name="installing-iis-and-web-deploy"></a>IIS 및 웹 배포 설치

개발 컴퓨터에서 IIS에 배포 하려면 IIS 및 웹 배포 설치 되어 있어야 합니다. 이러한 설정은 기본 Windows 7 구성에 포함 되지 않습니다. IIS와 웹 배포를 이미 설치한 경우 다음 섹션으로 건너뜁니다.

웹 플랫폼 설치 [관리자](https://www.microsoft.com/web/downloads/platform.aspx) 를 사용 하는 것이 iis 및 웹 배포를 설치 하는 기본 방법입니다. 웹 플랫폼 설치 관리자가 iis에 권장 구성을 설치 하 고 필요한 경우 iis 및 웹 배포에 대 한 필수 구성 요소를 자동으로 설치 하므로

웹 플랫폼 설치 관리자를 실행 하 여 IIS 및 웹 배포를 설치 하려면 다음 링크를 사용 합니다. IIS, 웹 배포 또는 필수 구성 요소를 이미 설치한 경우 웹 플랫폼 설치 관리자는 누락 된 항목만 설치 합니다.

- [WebPI를 사용 하 여 IIS 및 웹 배포 설치](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=IIS7;ASPNET;NETFramework4;WDeploy)

## <a name="setting-the-default-application-pool-to-net-4"></a>기본 응용 프로그램 풀을 .NET 4로 설정

IIS를 설치한 후 **Iis 관리자** 를 실행 하 여 .NET Framework 버전 4가 기본 응용 프로그램 풀에 할당 되었는지 확인 합니다.

Windows **시작** 메뉴에서 **실행**을 선택 하 고 "inetmgr"을 입력 한 다음 **확인**을 클릭 합니다. **실행** 명령이 **시작** 메뉴에 없으면 Windows 키와 R 키를 눌러 열 수 있습니다. 또는 작업 표시줄을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 클릭 한 다음 **시작 메뉴** 탭을 선택 하 고 **사용자 지정**을 클릭 한 다음 **명령 실행**을 선택 합니다.

**연결** 창에서 서버 노드를 확장 하 고 **응용 프로그램 풀**을 선택 합니다. **응용 프로그램 풀** 창에서 다음 그림과 같이 **DefaultAppPool** 이 .net framework 버전 4에 할당 된 경우 다음 섹션으로 건너뜁니다.

[Inetmgr_showing_4 ![0_app_pools](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image1.png)

응용 프로그램 풀이 두 개만 표시 되 고 둘 다 .NET Framework 2.0로 설정 된 경우 IIS에 ASP.NET 4를 설치 해야 합니다.

- Windows **시작** 메뉴에서 **명령 프롬프트** 를 마우스 오른쪽 단추로 클릭 하 고 **관리자 권한으로 실행**을 선택 하 여 명령 프롬프트 창을 엽니다. 그런 다음 [aspnet\_](https://msdn.microsoft.com/library/k6h9cz8h.aspx) 를 실행 하 여 iis에 ASP.NET 4를 설치 하 고 다음 명령을 사용 합니다. (64 비트 시스템에서 "Framework"를 "Framework64"로 바꿉니다.)

    [!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample2.cmd)]

    [aspnet_regiis_installing_ASP ![NET_4](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image3.png)

    이 명령은 .NET Framework 4에 대해 새 응용 프로그램 풀을 만들지만 기본 응용 프로그램 풀은 여전히 2.0로 설정 됩니다. .NET 4를 대상으로 하는 응용 프로그램을 해당 응용 프로그램 풀에 배포 하므로 응용 프로그램 풀을 .NET 4로 변경 해야 합니다.

**IIS 관리자**를 닫은 경우 다시 실행 하 고 서버 노드를 확장 한 다음 **응용** 프로그램 풀을 클릭 하 여 **응용 프로그램 풀** 창을 다시 표시 합니다.

**응용 프로그램 풀** 창에서 **DefaultAppPool**를 클릭 한 다음 **작업** 창에서 **기본 설정**을 클릭 합니다.

[![Inetmgr_selecting_Basic_Settings_for_app_pool](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image6.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image5.png)

**응용 프로그램 풀 편집** 대화 상자에서 **.NET Framework 버전** 을 **.NET Framework v 4.0.30319** 로 변경 하 고 **확인**을 클릭 합니다.

[Selecting_ ![NET_4_for_DefaultAppPool](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image7.png)

이제 IIS에 게시할 준비가 되었습니다.

## <a name="publishing-to-iis"></a>IIS에 게시

Visual Studio 2010 및 웹 배포를 사용 하 여 배포할 수 있는 몇 가지 방법이 있습니다.

- Visual Studio one 클릭 게시를 사용 합니다.
- *배포 패키지* 를 만들고 IIS 관리자 UI를 사용 하 여 설치 합니다. 배포 패키지는 IIS에 사이트를 설치 하는 데 필요한 모든 파일 및 메타 데이터를 포함 하는 *.zip* 파일로 구성 되어 있습니다.
- 배포 패키지를 만들고 명령줄을 사용 하 여 설치 합니다.

배포 작업을 자동화 하도록 Visual Studio를 설정 하기 위한 이전 자습서에서 수행한 프로세스는 이러한 세 가지 방법에 모두 적용 됩니다. 이러한 자습서에서는 이러한 메서드 중 첫 번째 방법을 사용 합니다. 배포 패키지를 사용 하는 방법에 대 한 자세한 내용은 [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521.aspx)을 참조 하십시오.

게시 하기 전에 관리자 모드에서 Visual Studio를 실행 하 고 있는지 확인 합니다. Windows 7 **시작** 메뉴에서 사용 중인 Visual Studio 버전의 아이콘을 마우스 오른쪽 단추로 클릭 하 고 **관리자 권한으로 실행**을 선택 합니다. 관리자 모드는 로컬 컴퓨터의 IIS에 게시 하는 경우에만 게시를 위해 필요 합니다.

**솔루션 탐색기**에서 ContosoUniversity 프로젝트가 아닌 ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 선택 합니다.

**웹 게시** 마법사가 나타납니다.

![Publish_Web_wizard_Profile_tab](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image9.png)

드롭다운 목록에서 **&lt;새로 만들기 ...&gt;** 를 선택 합니다.

**새 프로필** 대화 상자에서 "Test"를 입력 한 다음 **확인**을 클릭 합니다.

![New_Profile_dialog_box](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image10.png)

이 이름은 앞에서 만든 web.config 변환 파일의 중간 노드와 동일 합니다. 이로 인해이 프로필을 사용 하 여 게시할 때 web.config 변환이 적용 됩니다.

마법사가 자동으로 **연결** 탭으로 이동 합니다.

**서비스 URL** 상자에 *localhost*를 입력 합니다.

**사이트/응용 프로그램** 상자에서 *기본 웹 사이트/ContosoUniversity*를 입력 합니다.

**대상 URL** 상자에 `http://localhost/ContosoUniversity`을 입력 합니다.

**대상 URL** 설정은 필요 하지 않습니다. Visual Studio에서 응용 프로그램 배포를 마치면이 URL에 대 한 기본 브라우저가 자동으로 열립니다. 배포 후 브라우저를 자동으로 열지 않으려면이 상자를 비워 둡니다.

![Publish_Web_wizard_Connection_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image11.png)

**연결 유효성 검사** 를 클릭 하 여 설정이 올바른지 확인 하 고 로컬 컴퓨터의 IIS에 연결할 수 있습니다.

녹색 확인 표시는 연결에 성공 했는지 확인 합니다.

![Publish_Web_wizard_Connection_tab_validated](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image12.png)

**다음** 을 클릭 하 여 **설정** 탭으로 이동 합니다.

**구성** 드롭다운 상자는 배포할 빌드 구성을 지정 합니다. 기본값은 릴리스 이며 원하는 값입니다.

**대상에 추가 파일 제거** 확인란을 선택 취소 된 상태로 둡니다. 첫 번째 배포 이므로 대상 폴더에 아직 파일이 없습니다.

**데이터베이스** 섹션에서 **schoolcontext.cs**에 대 한 연결 문자열 상자에 다음 값을 입력 합니다.

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample3.cmd)]

**런타임에이 연결 문자열 사용** 을 선택 했기 때문에 배포 프로세스에서 배포 된 web.config 파일에이 연결 문자열을 넣습니다.

또한 **schoolcontext.cs**아래에서 **Code First 마이그레이션 적용**을 선택 합니다. 이 옵션을 선택 하면 배포 프로세스에서 배포 된 Web.config 파일을 구성 하 여 `MigrateDatabaseToLatestVersion` 이니셜라이저를 지정 합니다. 이 이니셜라이저는 응용 프로그램이 배포 후 처음으로 데이터베이스에 액세스 하는 경우 데이터베이스를 최신 버전으로 자동으로 업데이트 합니다.

**Defaultconnection**에 대 한 연결 문자열 상자에 다음 값을 입력 합니다.

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample4.cmd)]

**업데이트 데이터베이스** 를 지운 채로 둡니다. 앱\_데이터에서 .sdf 파일을 복사 하 여 멤버 자격 데이터베이스를 배포 하 고 배포 프로세스에서이 데이터베이스를 사용 하 여 다른 작업을 수행 하는 것을 원하지 않습니다.

![Publish_Web_wizard_Settings_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image13.png)

**다음** 을 클릭 하 여 **미리 보기** 탭으로 이동 합니다.

**미리 보기** 탭에서 **미리 보기 시작** 을 클릭 하 여 복사할 파일의 목록을 확인 합니다.

![Publish_Web_wizard_Preview_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image14.png)

![Publish_Web_wizard_Preview_tab_Test_with_file_list](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image15.png)

**게시**를 클릭합니다.

Visual Studio가 관리자 모드가 아니면 사용 권한 오류를 나타내는 오류 메시지가 나타날 수 있습니다. 이 경우 Visual Studio를 닫고 관리자 모드에서 연 다음 다시 게시 해 보세요.

Visual Studio가 관리자 모드에 있으면 **출력** 창에서 성공한 빌드 및 게시를 보고 합니다.

![Output_window_publish_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image16.png)

브라우저가 로컬 컴퓨터의 IIS에서 실행 되는 Contoso 대학 홈 페이지에 자동으로 열립니다.

[![Home_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image17.png)

## <a name="testing-in-the-test-environment"></a>테스트 환경에서 테스트

환경 표시기는 환경 표시기에 대 한 *web.config 변환이 성공* 했음을 보여 주는 "(Dev)" 대신 "(테스트)"를 표시 합니다.

[![Home_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image19.png)

**학생** 페이지를 실행 하 여 배포 된 데이터베이스에 학생이 없는 경우를 확인 합니다. Code First 데이터베이스를 만든 다음 `Seed` 메서드를 실행 하기 때문에이 페이지를 선택 하면 로드 하는 데 몇 분 정도 걸릴 수 있습니다. 응용 프로그램이 아직 데이터베이스에 액세스를 시도 하지 않았기 때문에 홈 페이지에 있는 경우에는이 작업을 수행 하지 않습니다.

[![Students_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image22.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image21.png)

**강사 페이지를** 실행 하 여 Code First가 강사 데이터로 데이터베이스를 시드 하는지 확인 합니다.

[![Instructors_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image24.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image23.png)

**학생** 메뉴에서 **학생 추가** 를 선택 하 고 학생을 추가한 다음 **학생** 페이지에서 새 학생을 보고 데이터베이스에 성공적으로 쓸 수 있는지 확인 합니다.

[![Add_Students_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image26.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image25.png)

[![Students_page_with_new_student_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image28.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image27.png)

**과정** 메뉴에서 **크레딧 업데이트**를 선택 합니다. [ **크레딧 업데이트** ] 페이지에는 관리자 권한이 필요 하므로 **로그인** 페이지가 표시 됩니다. 앞에서 만든 관리자 계정 자격 증명 ("admin" 및 "Pas $ w0rd")을 입력 합니다. 이전 자습서에서 만든 관리자 계정이 테스트 환경에 올바르게 배포 되었는지 확인 하는 **크레딧 업데이트** 페이지가 표시 됩니다.

[![Log_In_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image30.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image29.png)

[![Update_Credits_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image32.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image31.png)

*Elmah* 폴더에 자리 표시자 파일만 있는지 확인 합니다.

[![Elmah_folder_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image34.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image33.png)

<a id="efcfmigrations"></a>

## <a name="reviewing-the-automatic-webconfig-changes-for-code-first-migrations"></a>Code First 마이그레이션에 대 한 자동 web.config 변경 내용 검토

*C:\inetpub\wwwroot\ContosoUniversity* 에서 배포 된 응용 프로그램의 *web.config* 파일을 열고 배포 프로세스가 Code First 마이그레이션 구성 된 위치를 확인 하 여 데이터베이스를 최신 버전으로 자동으로 업데이트할 수 있습니다.

![](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image35.png)

또한 배포 프로세스에서는 데이터베이스 스키마를 업데이트 하는 데 독점적으로 사용할 Code First 마이그레이션에 대 한 새 연결 문자열을 만들었습니다.

![DatabasePublish_connection_string](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image36.png)

이 추가 연결 문자열을 사용 하 여 데이터베이스 스키마 업데이트에 대해 하나의 사용자 계정 및 응용 프로그램 데이터 액세스에 대 한 다른 사용자 계정을 지정할 수 있습니다. 예를 들어 db\_owner 역할을 Code First 마이그레이션에 할당 하 고, db\_datareader 및 db\_datawriter 여부 역할을 응용 프로그램에 할당할 수 있습니다. 응용 프로그램의 잠재적으로 악의적인 코드가 데이터베이스 스키마를 변경 하지 못하도록 하는 일반적인 심층 방어 패턴입니다. 예를 들어이 문제는 SQL 삽입 공격이 성공할 때 발생할 수 있습니다. 이 패턴은 이러한 자습서에서 사용 되지 않습니다. SQL Server Compact에는 적용 되지 않으며이 시리즈의 이후 자습서에서 SQL Server로 마이그레이션하면 적용 되지 않습니다. Cytanium 사이트는 Cytanium에서 만든 SQL Server 데이터베이스에 액세스 하기 위한 사용자 계정을 한 개만 제공 합니다. 시나리오에서이 패턴을 구현할 수 있는 경우 다음 단계를 수행 하 여 수행할 수 있습니다.

1. **웹 게시** 마법사의 **설정** 탭에서 전체 데이터베이스 스키마 업데이트 권한이 있는 사용자를 지정 하는 연결 문자열을 입력 하 고 **런타임에이 연결 문자열 사용** 확인란의 선택을 취소 합니다. 배포 된 web.config 파일에서는 `DatabasePublish` 연결 문자열이 됩니다.
2. 응용 프로그램에서 런타임에 사용 하려는 연결 문자열에 대 한 web.config 파일 변환을 만듭니다.

이제 개발 컴퓨터의 IIS에 응용 프로그램을 배포 하 고 테스트 했습니다. 이렇게 하면 배포 프로세스가 응용 프로그램의 콘텐츠를 올바른 위치 (배포 하지 않으려는 파일 제외)에 복사 하 고 배포 중에 IIS를 올바르게 구성 웹 배포 확인 됩니다. 다음 자습서에서는 아직 수행 되지 않은 배포 작업을 찾는 테스트를 하나 더 실행 합니다. *Elmah* 폴더에 대 한 폴더 사용 권한을 설정 합니다.

## <a name="more-information"></a>추가 정보

Visual Studio에서 IIS 또는 IIS Express를 실행 하는 방법에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- IIS.net 사이트에 대 한 [개요를 IIS Express](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) 합니다.
- Scott Guthrie의 블로그에서 [IIS Express 소개](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) .
- [방법: Visual Studio에서 웹 프로젝트용 웹 서버 지정](https://msdn.microsoft.com/library/ms178108.aspx)
- [IIS와](../deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md) ASP.NET 사이트의 ASP.NET 개발 서버의 핵심 차이점
- Rick Anderson의 블로그에서 [30 초 안에 IIS 7에서 ASP.NET MVC 또는 Web Forms 응용 프로그램을 테스트](https://blogs.msdn.com/b/rickandy/archive/2011/04/22/test-you-asp-net-mvc-or-webforms-application-on-iis-7-in-30-seconds.aspx) 합니다. 이 항목에서는 Visual Studio 개발 서버 (Cassini)를 사용한 테스트가 IIS Express 테스트 만큼 안정적이 지 않으며, IIS Express에서 테스트 하는 것이 IIS에서 테스트 하는 것 만큼 안정적이 지 않은 이유에 대 한 예를 제공 합니다.

응용 프로그램이 보통 신뢰 수준으로 실행 될 때 발생할 수 있는 문제에 대 한 자세한 내용은 Rolla 사이트의 4 개 사용자의 [ASP.NET 응용 프로그램을 Medium trust로 호스팅](http://www.4guysfromrolla.com/articles/100307-1.aspx) 을 참조 하세요.

> [!div class="step-by-step"]
> [이전](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md)
> [다음](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)
