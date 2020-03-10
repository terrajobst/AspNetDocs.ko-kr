---
uid: web-pages/readme/overview
title: WebMatrix 추가 정보 | Microsoft Docs
author: rick-anderson
description: WebMatrix 및 ASP.NET 웹 페이지 (Razor) 1.0 릴리스 정보
ms.author: riande
ms.date: 01/06/2011
ms.assetid: 36c5beeb-45a7-48a0-9c30-f82cdf5c5f5f
msc.legacyurl: /web-pages/readme
msc.type: content
ms.openlocfilehash: fac53e935860a90d8f2aa96699d56d66ade3a40f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454271"
---
# <a name="webmatrix-readme"></a>WebMatrix 추가 정보

13 월 13 일 2011

## <a name="contents"></a>콘텐츠

> [!NOTE]
> 이 추가 정보는 WebMatrix의 1.0 릴리스에 적용 됩니다.

- [개요](#Overview)
- [설치](#Installation_Notes)
- [응용 프로그램을 게시 하는 방법](#InstructionsForPublishingApplications)
- [변경 내용 및 문제](#ChangesAndIssues)

    - [WebMatrix 1.0 설치](#Known_Issues_Installation)
    - [ASP.NET 웹 페이지 2](#Known_Issues_ASPNET)
    - [WebMatrix](#Known_Issues_WebMatrix)
    - [IIS Express](#Known_Issues_IISExpress)
    - [SQL Server Compact](#Known_Issues_SQLServerCompact)
    - [응용 프로그램 설치](#Known_Issues_Installing_Applications)
    - [응용 프로그램 게시](#Known_Issues_Publishing_Applications)
- [자세한 내용](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a>개요

> Microsoft WebMatrix 1.0은 몇 분 안에 설치 되는 무료 웹 개발 스택입니다. 웹 서버를 데이터베이스 및 프로그래밍 프레임 워크와 통합 하 여 통합 된 단일 환경을 만듭니다. WebMatrix를 사용 하 여 사용자 고유의 ASP.NET 또는 PHP 웹 사이트를 코딩, 테스트 및 게시 하는 방법을 간소화 하거나 WebMatrix를 사용 하 여 DotNetNuke, Umbraco, WordPress 또는 Joomla와 같은 인기 있는 오픈 소스 앱을 사용 하 여 새 웹 사이트를 시작할 수 있습니다. WebMatrix는 인터넷에서 웹 사이트를 실행 하는 동일한 강력한 웹 서버, 데이터베이스 엔진 및 프레임 워크 환경을 사용 하며,이를 통해 개발 환경에서 프로덕션 환경으로 원활 하 고 원활 하 게 전환할 수 있습니다.

<a id="Installation_Notes"></a>

## <a name="installation"></a>설치

> WebMatrix 1.0을 설치 하려면 [Microsoft 웹 플랫폼 설치 관리자 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)를 먼저 설치 해야 합니다. 웹 플랫폼 설치 관리자를 설치한 후 WebMatrix를 설치 하는 데 사용할 수 있습니다.
> 
> 설치 하는 동안 문제가 발생 하는 경우 [Microsoft 웹 플랫폼 설치 관리자 문제 해결](https://go.microsoft.com/fwlink/?LinkId=196212)을 참조 하세요.

<a id="InstructionsForPublishingApplications"></a>
## <a name="how-to-publish-applications"></a>응용 프로그램을 게시 하는 방법

> [응용 프로그램 게시에 대 한 단계별 지침](https://go.microsoft.com/fwlink/?LinkID=196149) 을 참조 하세요.

<a id="ChangesAndIssues"></a>

## <a name="changes-and-issues"></a>변경 내용 및 문제

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-10-installation-issues"></a>WebMatrix 1.0 설치 문제

#### <a name="issue-webmatrix-10-is-available-only-on-platforms-that-support-microsoft-net-framework-4"></a>문제: WebMatrix 1.0은 Microsoft .NET Framework 4를 지 원하는 플랫폼 에서만 사용할 수 있습니다.

> WebMatrix에는 .NET Framework 버전 4가 필요 합니다. 경우에 따라 WebMatrix 1.0 설치 관리자를 사용 하 여 지원 되는 구성 집합의 일부가 아닌 플랫폼에을 설치할 수 있습니다. 특히 SP1 업데이트가 설치 되지 않은 Windows Vista에서는 WebMatrix 설치를 시작할 수 있지만 .NET Framework 4 구성 요소는 실패 하 고 설치를 차단 합니다.
> 
> **해결 방법**  
> 지원 되는 플랫폼에을 설치 합니다. 여기에는 다음이 포함 됩니다.
> 
> - Windows 7
> - Windows Server 2008
> - Windows Server 2008 R2
> - Windows Vista SP1 이상
> - Windows XP SP3
> - Windows Server 2003 SP2

#### <a name="issue-cannot-install-webmatrix-10-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a>문제: Microsoft Visual Studio 2008 s p 1 없이 Microsoft Visual Studio 2008이 설치 된 경우 WebMatrix 1.0를 설치할 수 없음

> **해결 방법**  
> Microsoft 다운로드 센터에서 [Microsoft Visual Studio 2008](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) s p 1을 설치 합니다.

#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a>문제: SQL Server Compact 4.0에 대 한 일부 어셈블리가 GAC에 설치 되어 있지 않습니다.

> SQL Server Compact 4.0에 대 한 관리 되는 어셈블리는 64 비트 컴퓨터에 SQL Server Compact 4.0를 설치할 때 GAC (전역 어셈블리 캐시)에 배치 되지 않고 컴퓨터에 .NET Framework 3.5 SP1 클라이언트 프로필만 설치 되어 있습니다. GAC에 설치 되지 않은 관리 되는 어셈블리는 다음과 같습니다.
> 
> - *System.data.sqlserverce* (ADO.NET provider)
> - *System.data.sqlserverce* (ADO.NET Entity Framework).
> 
> **해결 방법**  
> SQL Server Compact 4.0를 제거 합니다. 다음 위치에서 .NET Framework 3.5 s p 1의 전체 버전을 다운로드 하 여 설치 합니다.  
>   
> [Microsoft .NET Framework 3.5 서비스 팩 1 (전체 패키지)](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> 그런 다음 SQL Server Compact 4.0을 다시 설치 합니다.

#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a>문제: 명령줄을 사용 하 여 SQL Server Compact를 제거할 수 없습니다.

> 명령줄 옵션을 사용 하는 SQL Server Compact 제거는이 릴리스에서 작동 하지 않습니다.
> 
> **해결 방법**  
> Windows 제어판의 *프로그램 및 기능* 을 사용 하 여 Microsoft SQL Server Compact 4.0를 제거 합니다.

<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a>ASP.NET 웹 페이지

이 문서의 섹션에서는 Razor 구문와 ASP.NET 웹 페이지의 1.0 릴리스와 관련 된 새로운 기능, 변경 사항 및 알려진 문제에 대해 설명 합니다.

- [새로운 기능](#NewFeatures)
- [변경](#Changes)
- [문제](#Issues)

#### <a id="NewFeatures"></a>새 기능

#### <a name="new-configuration-setting-added-to-disable-the-package-manager"></a>새: 패키지 관리자를 사용 하지 않도록 설정 하는 구성 설정이 추가 됨

> *Web.config* 파일의 `<appSettings>` 요소에 대해 새 `asp:AdminManagerEnabled` 키를 사용할 수 있으며이를 통해 패키지 관리자를 완전히 사용 하지 않도록 설정할 수 있습니다. 이 요소의 기본값은 true *입니다. 즉, web.config 파일에* 포함 되어 있지 않으면 패키지 관리자를 사용할 수 있습니다. 패키지 관리자를 사용 하지 않도록 설정 하려면 *웹* 사이트의 루트에 있는 web.config 파일에 다음 요소를 추가 합니다.
> 
> [!code-xml[Main](overview/samples/sample1.xml)]

#### <a id="Changes"></a>변경

#### <a name="change-webpagesadminfoldervirtualpath-key-renamed-to-aspadminfoldervirtualpath"></a>변경: "웹 페이지: AdminFolderVirtualPath" 키 이름이 "asp: AdminFolderVirtualPath"로 바뀜

> 패키지 관리자의 위치를 지정 하기 위해 web.config *파일에* 추가할 수 있는 `webPages:AdminFolderVirtualPath` 키가 `webPages` 네임 스페이스 대신 `asp:` 네임 스페이스를 사용 하도록 이름이 바뀌었습니다. 이 요소를 사용한 경우 구성 파일에서 이름을 바꾸어야 합니다.

#### <a id="Issues"></a>  알려진 문제

#### <a name="issue-passwords-for-membership-users-no-longer-recognized"></a>문제: 멤버 자격 사용자의 암호가 더 이상 인식 되지 않습니다.

> 멤버 자격 (로그인) 암호를 만들고 저장 하는 알고리즘이 더 안전 하 게 변경 되었습니다. 따라서 ASP.NET Razor의 베타 버전에서 만든 구성원 (사용자)에 대해 저장 된 암호는 인식 되지 않습니다. 
> 
> **해결 방법** 사이트가 아직 프로덕션에 배치 되지 않은 경우 멤버 자격 데이터베이스에서 사용자 레코드를 제거 합니다. 데이터베이스가 라이브 인 경우 멤버 자격 데이터베이스에서 프로그래밍 방식으로 기존 암호를 다시 생성 합니다.

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a>문제: 멤버 자격에 사용자 지정 사용자 테이블을 사용할 때 예기치 않은 동작이 발생 합니다.

> ASP.NET Razor 웹 사이트의 멤버 자격 공급자를 초기화 하려면 `WebSecurity.InitializeDatabaseConnection` 메서드를 호출 합니다. (WebMatrix에서 스타터 사이트 템플릿은 *\_AppStart* 파일에이 메서드에 대 한 호출을 포함 합니다.) 이 메서드의 `autoCreateTables` 매개 변수가 true로 설정 되어 있으면 (기본적으로 시작 사이트 템플릿에서 true로 설정 됨) 인식할 수 없는 테이블 이름이 메서드에 전달 되는 경우 (두 번째 매개 변수) 메서드는 오류를 throw 하지 않습니다. 대신 테이블을 자동으로 만듭니다.
> 
> 멤버 자격에 사용자 지정 사용자 테이블을 사용 하지만 잘못 된 테이블 이름을 `WebSecurity.InitializeDatabaseConnection` 메서드에 전달 하려는 경우에이 문제가 발생할 수 있습니다. 사용자가 지정 하는 테이블이 존재 하지 않는 경우 메서드는 기본적으로 오류를 발생 시 키 지 않으며 대신 새 테이블을 만드는 경우 응용 프로그램이 작동 하는 것 처럼 보일 수 있습니다. 그러나 사용자 지정 사용자 테이블을 사용 하는 응용 프로그램 코드 (및 그 안에 포함 된 필드)는 결국 예기치 않은 오류로 인해 실패할 수 있습니다.
> 
> **해결 방법**  
> `InitializeDatabaseConnection` 메서드에 전달 된 이름이 멤버 자격 데이터베이스의 사용자 프로필 테이블과 일치 하는지 확인 하거나 `autoCreateTables` 매개 변수가 false로 설정 되어 있는지 확인 합니다.

#### <a name="issue-error-message-the-admin-module-requires-access-to-app_data"></a>문제: "관리자 모듈에서 ~/App\_데이터에 액세스 해야 합니다." 오류 메시지

> 경우에 따라 사용자를 만들거나 ASP.NET 멤버 자격 시스템을 사용 하 여 작업 하려는 경우에는 *관리자 모듈에서 ~/App\_데이터에 액세스 해야*하는 오류가 표시 될 수 있습니다. 이는 IIS 또는 IIS Express가 실행 중인 계정에 웹 사이트 루트 아래에 있는 *앱\_데이터* 폴더를 만들고 쓸 수 있는 권한이 없는 경우에 발생 합니다. 
> 
> **해결 방법** 웹 사이트에 대 한 *앱\_데이터* 폴더를 수동으로 만듭니다. 그런 다음 응용 프로그램이 실행 되는 Windows 계정 (일반적으로 NETWORK SERVICE)이 응용 프로그램의 루트 폴더와 앱\_데이터와 같은 하위 폴더에 대 한 읽기/쓰기 권한을 갖고 있는지 확인 합니다. 자세한 내용은 기술 자료 문서 [SQL Server Express 사용자 인스턴스 및 ASP.net 웹 응용 프로그램 프로젝트 문제](https://support.microsoft.com/kb/2002980)에서 확인할 수 있습니다.

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a>문제: "SQL Server 사용자 인스턴스를 생성 하지 못했습니다." 오류

> WebMatrix 웹 응용 프로그램이 SQL Server Express를 사용 하 고 Windows 7 또는 Windows Server 2008 r 2에서 IIS 7.5를 실행 하는 경우 SQL Server에서 사용자의 로컬 응용 프로그램 경로를 런타임에 검색할 수 없음을 나타내는 오류가 표시 될 수 있습니다.
> 
> **해결 방법** 응용 프로그램이 실행 되는 Windows 계정 (일반적으로 NETWORK SERVICE)에 응용 프로그램의 루트 폴더와 *앱\_데이터*와 같은 하위 폴더에 대 한 읽기/쓰기 권한이 있는지 확인 합니다. 자세한 내용은 기술 자료 문서 [SQL Server Express 사용자 인스턴스 및 ASP.net 웹 응용 프로그램 프로젝트 문제](https://support.microsoft.com/kb/2002980)에서 확인할 수 있습니다.

#### <a name="issue-files-that-contains-package-manager-resources-or-package-manager-passwords-are-servable-under-iis-60-and-earlier"></a>문제: 패키지 관리자 리소스 또는 패키지 관리자 암호를 포함 하는 파일은 IIS 6.0 및 이전 버전에서 사용할 수 있습니다.

> RC2 릴리스를 사용 하 여 빌드된 ASP.NET 웹 페이지 (Razor) 응용 프로그램을 배포 하는 경우 및 응용 프로그램의 */cm/App\_Data/admin*아래에 *암호 .txt* 또는 *packagesources* 파일이 포함 되어 있는 경우 IIS 6.0은 요청 될 경우 패키지 관리자 인스턴스에 대 한 암호를 노출 하는 파일을 제공 합니다. 
> 
> **해결 방법** *Password .txt* 또는 *packagesources* 파일의 이름을 *packagesources 또는*로 *바꿉니다* . 기본적으로 IIS 6.0는 확장명이 *.config* 인 파일을 제공 하지 않습니다. IIS 7에서는 *응용 프로그램\_데이터* 폴더의 파일이 제공 되지 않으므로 파일 이름을 바꿀 필요가 없습니다.

#### <a name="issue-uninstalling-packages-installed-using-the-beta-3-release-does-not-completely-remove-package-components"></a>문제: Beta 3 릴리스를 사용 하 여 설치 된 패키지를 제거 해도 패키지 구성 요소가 완전히 제거 되지 않음

> 베타 3 릴리스에서 패키지 관리자를 사용 하 여 패키지를 설치한 다음 현재 릴리스를 사용 하 여 패키지를 제거 하려고 하면 패키지가 완전히 제거 되지 않습니다. 패키지 관리자의 **제거** 단추를 사용 하면 일부 구성 요소가 제거 되지만 패키지의 라이브러리 코드는 그대로 유지 되 고 *패키지 .config* 파일은 업데이트 되지 않습니다.
> 
> **해결 방법**   
> 다음 단계를 수행 합니다.  
> 1. *앱\_Data\packages* 폴더를 삭제 합니다. 그러면 모든 패키지가 제거 됩니다.   
> 2. 웹 사이트의 루트에 있는 *패키지 .config* 파일을 삭제 합니다.

#### <a name="issue-in-visual-studio-invoking-the-web-based-package-manager-takes-the-application-offline"></a>문제: Visual Studio에서 웹 기반 패키지 관리자를 호출 하면 응용 프로그램이 오프 라인으로 전환 됩니다.

> WebMatrix가 아닌 Visual Studio에서 작업 중이 고 *\_관리자* 기능을 사용 하 여 패키지 관리자를 시작 하는 경우 visual studio는 응용 프로그램을 오프 라인으로 전환 하 고 웹 사이트 루트에 응용 프로그램을 *오프 라인\_* 게시 하 여 패키지 관리자를 사용 하는 기능을 중단 합니다.
> 
> [!NOTE]
> 일반적으로 웹 기반 패키지 관리자 인터페이스를 사용 하는 경우이 동작이 표시 되기는 하지만, *App\_Data* 폴더의 파일을 추가, 제거 또는 수정 하는 경우에도 동일한 동작이 발생 합니다.
> 
> **해결 방법**   
> Visual Studio에서 패키지를 사용 하려면 웹 기반 패키지 관리자 대신 NuGet 확장을 사용 합니다. 자세한 내용은 [NuGet 설명서](https://docs.microsoft.com/nuget/)를 참조 하세요. *App\_Data* 폴더의 다른 파일을 사용 하는 경우이 문제를 방지 하려면 다른 위치에 파일을 보관 하는 것이 좋습니다. 실용적이 지 않은 경우 *앱\_오프 라인 .htm* 파일을 수동으로 삭제 하거나 사이트가 자동으로 다시 온라인 상태가 될 때까지 기다립니다 (기본적으로 30 초 후).

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a>문제: Visual Studio IntelliSense 및 프로젝트 템플릿은 ASP.NET MVC 버전 3 에서만 사용할 수 있습니다.

> ASP.NET 웹 페이지를 설치 해도 ASP.NET 웹 페이지 응용 프로그램용 IntelliSense 및 프로젝트 템플릿과 같은 Visual Studio 용 도구도 설치 되지 않습니다.
> 
> **해결 방법** Visual Studio에서 ASP.NET 웹 페이지 응용 프로그램에 대 한 IntelliSense 및 프로젝트 템플릿을 사용 하려면 웹 플랫폼 설치 관리자 또는 [독립 실행형 설치 관리자](https://go.microsoft.com/fwlink/?LinkID=191797)를 통해 ASP.NET MVC 3 RC를 설치 합니다.

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a>문제: 프록시 서버를 통해 피드 또는 기타 외부 데이터 읽기

> 사이트를 실행 하는 서버가 프록시 서버 뒤에 있는 경우 사이트 외부에서 제공 되는 정보를 읽을 수 있도록 *web.config 파일에서* 프록시 정보를 구성 해야 할 수 있습니다. 예를 들어 `ReCaptcha` 도우미를 사용 하는 경우 도우미가 reCAPTCHA 서비스와 통신 하지만 프록시 서버에 의해 차단 될 수 있습니다. 마찬가지로 패키지 관리자에서 사용 하는 피드와 같이 ASP.NET 웹 페이지에 사용 되는 피드에는 프록시 구성이 필요할 수 있습니다.
> 
> 외부 서비스를 사용 하거나 패키지 피드를 사용 하 여 작업 하는 데 문제가 발생 하는 경우 응용 프로그램의 루트 web.config 파일에 다음 요소를 *추가 합니다.*
> 
> [!code-xml[Main](overview/samples/sample2.xml)]
> 
> 프록시 서버를 구성 하는 방법에 대 한 자세한 내용은 MSDN 웹 사이트에서 [&lt;프록시&gt; 요소 (네트워크 설정)](https://msdn.microsoft.com/library/sa91de1e.aspx) 를 참조 하십시오.

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a>문제: .NET Framework 버전 4를 제거 하면 Razor 구문을 사용 하 여 ASP.NET 웹 페이지 사용 하지 않도록 설정 됩니다.

> .NET Framework 버전 4를 제거한 후 다시 설치 하는 경우 Razor 구문 사용 하지 않도록 설정 된 ASP.NET 웹 페이지. 확장명이 *cshtml* 인 페이지는 올바르게 실행 되지 않습니다. ASP.NET 웹 페이지는 컴퓨터 루트 *web.config* 파일에 어셈블리를 등록 하 고 .NET Framework 제거 하면 해당 파일이 제거 됩니다. .NET Framework를 다시 설치 하면 새 버전의 구성 파일이 설치 되지만 ASP.NET 웹 페이지 어셈블리에 대 한 참조는 추가 되지 않습니다.
> 
> **해결 방법** .NET Framework를 다시 설치한 후 Razor 구문를 사용 하 여 ASP.NET 웹 페이지를 다시 설치 합니다. 그러면 다음 요소가 컴퓨터 루트의 web.config *파일에* 추가 됩니다 .이 파일은 일반적으로 다음 위치에 있습니다.  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](overview/samples/sample3.xml)]

#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a>문제: 확장명 없는 Url은 IIS 7 또는 IIS 7.5에 있는 cshtml/. a s d 파일을 찾지 못합니다.

> IIS 7 또는 IIS 7.5에서는 다음과 같은 URL을 사용 하는 요청이 *확장명이. n e t 또는* *.* n e t 인 페이지를 찾을 수 없습니다.  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> URL 다시 쓰기는 IIS 7 또는 IIS 7.5에 대해 기본적으로 사용 되지 않기 때문에 문제가 발생 합니다. Likeliest를 사용 하 IIS Express 여 로컬로 테스트 하는 경우에는 문제가 표시 되지 않지만 호스팅 웹 사이트에 웹 사이트를 배포할 때이 문제가 발생 합니다.
> 
> **해결 방법**
> 
> - 서버 컴퓨터를 제어 하는 경우 서버 컴퓨터에서 업데이트에 설명 된 업데이트를 설치할 수 있습니다. [그러면 특정 iis 7.0 또는 iis 7.5 처리기에서 url이 마침표로 끝나지 않는 요청을 처리할 수 있습니다](https://support.microsoft.com/kb/980368).
> - 서버 컴퓨터를 제어할 수 없는 경우 (예: 호스팅 웹 사이트에 배포 하는 경우) 웹 사이트의 *web.config* 파일에 다음을 추가 합니다. 
> 
>     [!code-xml[Main](overview/samples/sample4.xml)]

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a>문제: SQL Server Compact 설치 되지 않은 컴퓨터에 응용 프로그램 배포

> SQL Server Compact 데이터베이스를 포함 하는 응용 프로그램은 SQL Server Compact가 설치 되지 않은 컴퓨터에서 실행할 수 있습니다. Microsoft WebMatrix 1.0은 이러한 이진 파일을 자동으로 복사 하 고 *적절 한* web.config 파일 변환을 수행 합니다.
> 
> **해결 방법** 이러한 파일을 복사 하 고 *web.config 파일을* 수동으로 변경 하려면 다음을 수행 합니다.
> 
> 1. 대상 컴퓨터에 있는 응용 프로그램의 *Bin* 폴더 (및 하위 폴더)에 데이터베이스 엔진 어셈블리를 복사 합니다.  
> 
>    - *C:\Program Files\Microsoft SQL Server Edition\v4.0\Desktop\System.Data.SqlServerCe.dll*  복사  
>      *\bin*
>    - *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* **를** *\Bin\x86* 에 복사 합니다.
>    - *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\* * **를** *\Bin\amd64* 에 복사 합니다.
> 
> 2. *웹* 사이트의 루트 폴더에서 web.config 파일을 만들거나 엽니다. (WebMatrix 1.0에서는 **파일 형식 선택** 대화 상자에서 **모두** 를 클릭 하는 경우이 파일 형식을 사용할 수 있습니다.)
> 3. 다음 요소를 `<system.web>` 요소 내부가 아닌 `<configuration>` 요소의 자식으로 추가 합니다.
> 
>     [!code-xml[Main](overview/samples/sample5.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a>문제: "데이터베이스" 및 "WebGrid" 도우미가 Visual Basic의 보통 신뢰에서 작동 하지 않음

> Visual Basic를 사용 하는 경우 ( *vbhtml* 파일 만들기) 응용 프로그램이 보통 신뢰를 사용 하도록 설정 된 경우 `Database` 및 `WebGrid` 도우미가 작동 하지 않습니다.
> 
> **해결 방법**  
> Visual Studio 2010을 사용 하는 경우 서비스 팩 1 릴리스를 설치 하 여이 문제를 해결할 수 있습니다. 최신 버전의 SP1 릴리스를 사용할 수 있을 때 까지는 Microsoft 다운로드 센터의 [Microsoft Visual Studio 2010 서비스 팩 1 베타](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en) 페이지에서 베타 버전의 s p 1을 다운로드할 수 있습니다.   
>   
> 유용 하지 않거나 Visual Studio 2010을 사용 하지 않는 경우 일시적으로 응용 프로그램에 완전 신뢰를 사용 하도록 설정할 수 있습니다.

#### <a name="issue-applicationpart-resources-are-externally-accessible"></a>문제: "ApplicationPart" 리소스는 외부에서 액세스할 수 있습니다.

> 어셈블리가 `ApplicationPart` 클래스에서 파생 되는 개체를 포함 하는 경우 해당 어셈블리의 리소스는 `ResourceRouteHandler` 클래스에 의해 노출 됩니다. 예를 들어 다음 URL을 가정해 봅니다.  
>   
> `~/r.ashx/System.Web.WebPages.Administration/Resources/AdminResources.resources`  
>   
> 이 요청은 *system.web* 어셈블리의 모든 리소스 문자열을 다운로드 합니다. 모든 포함 된 리소스 (정적 콘텐츠로 제공 하지 않는 경우에도)가 다운로드 됩니다. 포함 된 리소스에 중요 한 정보가 포함 된 경우이는 보안 위험을 나타낼 수 있습니다. 
> 
> **해결 방법**   
> **Applicationpart** 개체를 만드는 경우 해당 **applicationpart** 개체의 어셈블리와 연결 된 포함 리소스에 중요 한 정보가 포함 되어 있지 않은지 확인 합니다.

<a id="Known_Issues_WebMatrix"></a>

### <a name="webmatrix"></a>WebMatrix

> [!NOTE]
> WebMatrix 설치 문제에 대 한 자세한 내용은이 문서의 앞부분에 있는 [Webmatrix 설치 문제](#Known_Issues_Installation) 를 참조 하세요.

문서의이 섹션에서는 WebMatrix 개발 환경에 대 한 알려진 문제를 설명 합니다.

#### <a name="issue-changes-in-the-username-or-password-of-a-database-connection-string-in-a-webconfig-file-are-not-reflected-in-the-databases-workspace"></a>문제: web.config 파일에서 데이터베이스 연결 문자열의 사용자 이름 또는 암호 변경 내용이 데이터베이스 작업 영역에 반영 되지 않습니다.

> **해결 방법**  
> 
> 1. *Web.config 파일에서* 연결 문자열의 데이터베이스 이름을 변경 합니다 (예: "1"을 여기에 추가).
> 2. *Web.config 파일을* 저장 합니다.
> 3. **데이터베이스** 및 새로 고침을 클릭 합니다.
> 4. *Web.config* 파일의 연결 문자열에 있는 데이터베이스 이름을 다시 원래 데이터베이스 이름으로 변경 합니다.
> 5. *Web.config 파일을* 저장 합니다.
> 6. **데이터베이스** 및 새로 고침을 클릭 합니다.

#### <a name="issue-folders-created-by-webmatrix-cannot-be-deleted"></a>문제: WebMatrix에서 만든 폴더를 삭제할 수 없습니다.

> Windows에서 **관리자 권한으로 실행** 옵션을 사용 하 여 webmatrix를 시작한 경우, webmatrix를 사용 하 여 webmatrix를 실행 하는 경우 windows 탐색기를 사용 하 여 webmatrix에서 만든 폴더를 삭제할 수 없습니다.
> 
> **해결 방법**  
> 승격 된 권한을 사용 하 여 Windows 탐색기를 실행 합니다. 다음 단계를 수행하세요.  
> 
> 1. Windows에서 **시작**을 클릭 합니다.
> 2. "Windows 탐색기"를 입력 하 고 **Windows 탐색기**의 항목을 마우스 오른쪽 단추로 클릭 합니다.
> 3. **관리자 권한으로 실행을**클릭 합니다. 그런 다음 폴더를 삭제할 수 있습니다.

#### <a name="issue-webmatrix-10-is-unable-to-perform-certain-tasks-that-require-elevation"></a>문제: WebMatrix 1.0는 권한 상승이 필요한 특정 작업을 수행할 수 없습니다.

> WebMatrix 1.0는 다음과 같은 상황에서 추가 구성 요소를 설치 하는 등 권한 상승이 필요한 특정 작업을 수행할 수 없습니다.
> 
> - Windows Vista 또는 Windows 7에서 관리 권한이 없고 UAC (사용자 계정 컨트롤)를 사용할 수 없는 계정으로 로그인 합니다.
> - Microsoft Windows XP 또는 Microsoft Windows Server 2003를 사용 하 고 있습니다.
> 
> **해결 방법**  
> WebMatrix 1.0에서 대부분의 작업에는 관리 권한이 필요 하지 않습니다. 이렇게 하려면 관리자 권한으로 작업을 수행 하거나 다음 단계를 수행 하면 됩니다.
> 
> - Windows Vista 또는 Windows 7에서 UAC를 사용 하도록 설정 합니다.
> - Windows XP에서 관리자 보안 그룹에 사용자를 추가 합니다.

#### <a name="issue-site-from-web-gallery-is-disabled"></a>문제: "웹 갤러리에서 사이트"를 사용할 수 없습니다.

> 웹 플랫폼 설치 관리자 3.0가 설치 되어 있지 않으면 **웹 갤러리에서 사이트** 옵션을 사용할 수 없습니다.
> 
> **해결 방법**  
> [Microsoft 웹 플랫폼 설치 관리자 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)을 설치 합니다.

#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a>문제: Google Chrome은 실행 옵션으로 사용할 수 없습니다.

> Google Chrome은 **홈** 탭에서 **실행** 중인 브라우저 목록에 표시 되지 않습니다.
> 
> **해결 방법**  
> 일부 Google Chrome 버전은 Windows의 기본 프로그램 기능을 사용 하 여 제대로 등록 되지 않습니다. 해결 방법으로 Google Chrome을 시작 하 *고 사용자 지정 및 제어 Google chrome* 메뉴를 클릭 한 다음 *옵션*을 클릭 하 고 *Google Chrome 내 기본 브라우저 만들기*를 클릭 합니다.

#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a>문제: "외래 키" 대화 상자에서 기본 키 입력을 허용 하지 않습니다.

> **외래 키** 대화 상자에서는 기본 키 테이블의 기본 키 이름을 입력할 수 없습니다.
> 
> **해결 방법**  
> 이것은 의도적인 것입니다. 기본 키 테이블에서 기본 키의 이름을 입력할 필요는 없습니다.

#### <a name="issue-intellisense-is-not-available-in-webmatrix-for-razor-syntax-c-or-visual-basic"></a>문제: Razor 구문, C#또는에 대해 WebMatrix에서 IntelliSense를 사용할 수 없습니다 Visual Basic

> IntelliSense는 HTML 및 CSS 용 WebMatrix에서 지원 됩니다. 그러나 다른 언어에 대해서는 사용할 수 없습니다. 
> 
> **해결 방법**   
> 없음

#### <a name="issue-intellisense-for-html-and-css-suggests-elements-that-are-not-contextually-appropriate"></a>문제: HTML 및 CSS 용 IntelliSense에서 적절 하 게 컨텍스트 않는 요소를 제안 합니다.

> WebMatrix의 태그에 대 한 IntelliSense는 [css 2.1 스키마](http://www.w3.org/TR/CSS2/)를 사용 하 여 [XHTML 1.0 전환 스키마](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional) 및 css를 사용 하는 HTML을 지원 합니다. IntelliSense는 이러한 특정 스키마를 기반으로 하기 때문에 현재 페이지나 스타일 정의에 적합 하지 않은 특정 태그, 특성 또는 속성이 제안 될 수 있습니다. HTML의 경우 잘못 된 형식의 XHTML (예: 태그가 닫히지 않은 경우)으로 해석 될 수 있는 콘텐츠에서 예기치 않은 제안을 발생 시킬 수도 있습니다. 삽입 지점이 불완전 한 태그 안에 있는 경우이 문제가 더 눈에 띄는 것일 수 있습니다. 이 경우 IntelliSense는 새로운 열기 태그를 제안 하거나 다른 잘못 된 제안을 제공할 수 있습니다. 
> 
> **해결 방법**   
> HTML의 경우 올바른 형식의 전체 XHTML 페이지 내에서 작업 하 고 있는지 확인 합니다. CSS의 경우 해결 방법이 없습니다.

#### <a name="issue-intellisense-is-not-invoked-while-you-type"></a>문제:를 입력 하는 동안 IntelliSense가 호출 되지 않습니다.

> HTML 또는 CSS를 편집기에 입력 하는 경우에는 IntelliSense가 호출 되지 않을 수 있습니다. 특히 삽입 지점이 다른 요소 바로 다음에 있거나 파일의 끝에 있는 경우이 문제가 발생할 수 있습니다. 
> 
> **해결 방법**   
> 삽입 지점 주위에 공백이 있고 삽입 지점이 파일의 끝에 있지 않은지 확인 합니다. Ctrl + Space를 눌러 IntelliSense를 수동으로 호출할 수도 있습니다.

#### <a name="issue-no-ui-is-available-for-disabling-intellisense"></a>문제: IntelliSense를 비활성화 하는 데 사용할 수 있는 UI가 없습니다.

> WebMatrix 1.0는 IntelliSense를 사용 하지 않도록 설정 하기 위한 UI 나 제스처를 제공 하지 않습니다. 
> 
> **해결 방법**   
> IntelliSense를 사용 하지 않도록 설정 하는 스위치를 포함 하는 다음 명령을 사용 하 여 WebMatrix를 시작 합니다.  
>   
> `WebMatrix.exe #ExecuteCommand# EditorIntelliSense off`

<a id="Known_Issues_IISExpress"></a>
### <a name="iis-express"></a>IIS Express

IIS Express에는 다음 URL에서 사용할 수 있는 고유한 추가 정보 파일이 있습니다.

[https://go.microsoft.com/fwlink/?LinkID=207675&amp; clcid = 0x409](https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409)

<a id="Known_Issues_SQLServerCompact"></a>

### <a name="sql-server-compact"></a>SQL Server Compact

SQL Server Compact에는 다음 URL에서 사용할 수 있는 고유한 추가 정보 파일이 있습니다.

[https://go.microsoft.com/fwlink/?LinkID=208545](https://go.microsoft.com/fwlink/?LinkID=208545&amp;clcid=0x409)

WebMatrix의 일부로 SQL Server Compact 설치와 관련 된 문제에 대 한 자세한 내용은이 문서의 앞부분에 있는 [Webmatrix 설치 문제](#Known_Issues_Installation) 를 참조 하세요.

### <a id="Known_Issues_Installing_Applications"></a>응용 프로그램 설치

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a>문제: 사용자의 내 문서 폴더가 네트워크 공유로 리디렉션되는 경우 응용 프로그램을 설치 하는 데 시간이 오래 걸릴 수 있습니다.

> **해결 방법**  
> 없음 응용 프로그램을 설치 하는 데 약간의 시간이 걸릴 수 있지만 제대로 설치 됩니다.

### <a id="Known_Issues_Publishing_Applications"></a>응용 프로그램 게시

#### <a name="issue-required-permissions-cannot-be-acquired-error-when-publishing-a-sql-compact-database"></a>문제: SQL Compact 데이터베이스를 게시할 때 "필요한 사용 권한을 얻을 수 없습니다." 오류가 발생 합니다.

> WebMatrix는 .NET Framework 버전 3.5을 실행 하는 서버에 대 한 SQL Server Compact 지원 이진 파일을 보통 신뢰 구성과 함께 배포 하는 것을 완벽 하 게 지원 하지 않습니다.
> 
> **해결 방법**  
> 권장 해결 방법은 서버에 .NET Framework 4를 설치 하는 것입니다. 또는 다음을 수행 합니다.
> 
> 1. *웹\_MediumTrust .config* 파일의 `SecurityClasses` 섹션에 다음 요소를 추가 합니다.
> 
>     [!code-html[Main](overview/samples/sample6.html)]
> 2. 다음 필수 권한으로 *웹\_MediumTrust .config* 파일에 새 권한 집합을 만듭니다.
> 
>     [!code-html[Main](overview/samples/sample7.html)]
> 3. *웹\_MediumTrust .config* 파일에 다음 요소를 배치 하 여 SQL Server Compact에 권한 집합을 적용 합니다.
> 
>     [!code-html[Main](overview/samples/sample8.html)]

#### <a name="issue-gallery-and-phpbb-web-applications-display-a-service-is-unavailable-error-after-publishing"></a>문제: 게시 후 갤러리 및 PhpBB 웹 응용 프로그램에서 "서비스를 사용할 수 없음" 오류를 표시 합니다.

> 경우에 따라 응용 프로그램을 게시 하면 "서비스를 사용할 수 없습니다." 오류가 발생 합니다.
> 
> **해결 방법**  
> WebMatrix에서, **게시 설정** 창에서 서버 이름의 끝에 백슬래시 (\)를 추가 하 고 응용 프로그램을 다시 게시 합니다.

#### <a name="issue-moodle-website-layout-and-links-are-broken-after-publishing"></a>문제: 게시 후 Moodle 웹 사이트 레이아웃 및 링크가 손상 되었습니다.

> Moodle 응용 프로그램을 게시 한 후에는 응용 프로그램이 제대로 작동 하지 않습니다.
> 
> **해결 방법**  
> WebMatrix에서 **게시 설정** 창에 있는 **사이트 이름** 필드의 끝에 슬래시 (/)를 추가한 다음 응용 프로그램을 다시 게시 합니다.

#### <a name="issue-publishing-nopcommerce-fails-with-a-database-error"></a>문제: 게시 nopCommerce이 데이터베이스 오류와 함께 실패 합니다.

> NopCommerce를 게시 하면 "nop\_로그 테이블에 삽입 하지 못했습니다."와 같은 데이터베이스 오류를 보고 합니다.
> 
> **해결 방법**  
> 
> 1. WebMatrix에서 **실행** 을 클릭 하 여 nopCommerce를 로컬로 시작 합니다.
> 2. 관리 페이지에 로그인 합니다.
> 3. **시스템** 메뉴를 클릭 합니다.
> 4. **로그** 옵션을 클릭 합니다.
> 5. **로그 지우기** 단추를 클릭합니다.
> 6. NopCommerce를 다시 게시 합니다.

#### <a name="issue-silverstripe-cms-displays-a-http-500-php-fcgi-error-when-you-download-a-published-site"></a>문제: 게시 된 사이트를 다운로드할 때 Silverstripe CMS에서 "HTTP 500 PHP FCGI 오류"를 표시 합니다.

> **해결 방법**  
> **게시 된 사이트 다운로드**를 클릭 한 후 **게시 미리 보기**에서 `silverstripe-cache/manifest_main`를 건너뜁니다. 이 파일은 캐싱에 사용 되며 각 컴퓨터에만 적용 됩니다.

#### <a name="issue-subtext-displays-server-error-in--application-when-you-download-a-published-site"></a>문제: 게시 된 사이트를 다운로드 하는 경우 Subtext가 "'/' 응용 프로그램에 서버 오류"를 표시 합니다.

> **해결 방법**  
> 사이트의 *web.config* 파일을 열고 데이터베이스 연결 문자열의 사용자 ID와 암호를 SQL Server 관리자 자격 증명 ("sa" 자격 증명)으로 바꿉니다.
> 
> 또는 `db_owner` 권한으로 로그인 한 사용자 계정을 제공 하기 위해 다음 단계를 수행 합니다.
> 
> 1. 웹 플랫폼 설치 관리자를 사용 하 여 SQL Server Management Studio를 설치 합니다.
> 2. 로컬 SQL Server Express 인스턴스에 연결 합니다 (기본적으로 `.\SQLEXPRESS`).
> 3. **데이터베이스** &gt; *[Localsubtextdatabase]* &gt; **Security** &gt; **Users** &gt; *[localsubtextdatabase*] (기본값은 `subtextuser`]를 클릭 하 고 마우스 오른쪽 단추를 클릭 한 다음 **속성**을 클릭 합니다.
> 4. 역할 멤버 자격 섹션에서 **db\_소유자** 를 선택 합니다.

#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a>문제: 사이트 "대상 URL" 필드는 http:// 또는 https:// 로 시작 하지 않는 경우 게시 한 후 작동 하지 않을 수 있습니다.

> **게시 설정** 대화 상자에서 대상 URL이 `http://` 또는 `https://`으로 시작 하지 않는 경우 배포 후 사이트가 작동 하지 않을 수 있습니다.
> 
> **해결 방법**  
> 사이트를 게시 하기 전에 **게시 설정** 대화 상자의 대상 URL은 `http://` 또는 `https://`으로 시작 해야 합니다.

#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a>문제: "데이터베이스를 게시 하지 못했습니다." 오류가 발생 하 여 MySQL 데이터베이스를 게시 하지 못했습니다. 이 문제는 원격 데이터베이스에서 스크립트를 실행할 수 없는 경우 발생할 수 있습니다. "

> 이 오류는 여러 가지 이유로 발생할 수 있습니다. 데이터베이스 스크립트에 작은따옴표 (')가 포함 되어 있고 대상 MySQL 데이터베이스의 기본 문자 집합이 u t f-8이 아닌 경우이 오류가 나타날 수 있습니다.
> 
> **해결 방법**  
> 원격 MySQL 데이터베이스의 기본 문자 집합을 u t f-8로 설정 합니다.

#### <a name="issue-some-links-are-not-visible-in-dotnetnuke-after-publishing-or-downloading-the-site"></a>문제: 일부 링크는 사이트 게시 또는 다운로드 후 DotNetNuke에 표시 되지 않습니다.

> DotNetNuke 사이트를 게시 하거나 다운로드 하는 경우 사이트에 새 링크를 표시 하려면 캐시를 지워야 할 수 있습니다.
> 
> **해결 방법**
> 
> 1. "Host"로 로그인 합니다.
> 2. 호스트 메뉴로 이동 하 여 **호스트 설정**을 선택 합니다.
> 3. 아래로 스크롤하고 **고급 설정**에서 **성능 설정**을 확장 합니다.
> 4. 페이지에 대 한 **캐시 지우기** 링크를 클릭 합니다.
> 5. 페이지 아래쪽으로 이동 하 여 응용 프로그램을 다시 시작 합니다.

#### <a name="issue-some-links-in-atomsite-are-broken-after-you-download-a-published-site"></a>문제: 게시 된 사이트를 다운로드 한 후 AtomSite의 일부 링크가 손상 되었습니다.

> **해결 방법**  
> *서비스 .config* 파일, *사용자 .config* 파일 및 모든 *.xml* 파일에서 URL 문자열 (예: `http://myhost.com/atomsite`)을 로컬 항목 (예: `http://localhost:1239`)으로 바꿉니다.

#### <a name="issue-mysql-based-applications-like-wordpress-fail-to-publish-and-report-a-database-error"></a>문제: WordPress와 같은 MySQL 기반 응용 프로그램에서 데이터베이스 오류를 게시 하 고 보고 하지 못했습니다.

> 기본적으로 WebMatrix는 UTF-8 문자 집합을 사용 하 여 MySQL을 설치 합니다. 자체에 MySQL을 설치 하 고 문자 집합이 u t f-8이 아닌 경우 (예: Latin1) 데이터베이스에 대 한 게시 프로세스가 실패할 수 있습니다.
> 
> **해결 방법**
> 
> 1. MySQL에 대 한 문자 집합을 u t f-8로 변경 합니다. 자세한 내용은 MySQL 웹 사이트의 [서버 문자 집합 및 데이터 정렬](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html) 을 참조 하세요.
> 2. 응용 프로그램을 다시 설치하십시오.
> 3. 응용 프로그램을 다시 게시 합니다.

#### <a name="issue-download-published-site-fails-for-applications-that-have-browser-based-setup"></a>문제: 브라우저 기반 설치를 사용 하는 응용 프로그램의 경우 "게시 된 사이트 다운로드"가 실패 함

> 일부 응용 프로그램 (예: Kentico CMS)에서는 데이터베이스를 만드는 등의 설치 후 설치를 수행 하기 위해 브라우저에서 해당 응용 프로그램을 시작 해야 합니다. 브라우저 기반 설치를 완료 하지 않고 이와 같은 응용 프로그램을 게시 하면 원격 서버에서 동일한 사이트를 다운로드 하는 데 실패 합니다.
> 
> **해결 방법**  
> 사이트를 게시 하기 전에 브라우저 기반 설치를 완료 합니다.

#### <a name="issue-download-published-site-fails-with-a-database-error-for-dotnetnuke-and-kooboo-cms"></a>문제: DotNetNuke 및 Kooboo CMS에 대해 데이터베이스 오류가 발생 하 여 "게시 된 사이트 다운로드"가 실패 함

> 서버에서 응용 프로그램을 다운로드 하려고 하는데 **게시 설정** 대화 상자의 데이터베이스 연결 문자열에 관리자 자격 증명이 있는 경우 게시 로그에 다음 오류가 표시 될 수 있습니다.
> 
> [!code-console[Main](overview/samples/sample9.cmd)]
> 
> **해결 방법**  
> 실용적 인 경우 데이터베이스에 대 한 비관리자 자격 증명을 사용 하 여 사이트를 다시 게시 하거나 게시 합니다.

<a id="More_Info"></a>

## <a name="for-more-information"></a>참조 항목

WebMatrix 1.0에 대 한 자세한 내용은 다음 웹 사이트를 참조 하세요.

- [IIS.net](http://iis.net/)
- [ASP.NET](https://asp.net/webmatrix)
- [Microsoft.com/web](https://www.microsoft.com/web)

© 2011 Microsoft Corporation. All Rights Reserved. [사용 약관](https://msdn.microsoft.cos/cc300389.aspx).
