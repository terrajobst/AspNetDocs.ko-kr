---
uid: web-pages/readme/beta3
title: 웹 행렬 및 ASP.NET 웹 페이지 (Razor) Beta 3 릴리스 추가 정보 | Microsoft Docs
author: rick-anderson
description: WebMatrix 및 ASP.NET 웹 페이지(Razor) 베타 3 릴리스 추가 정보
ms.author: riande
ms.date: 01/10/2011
ms.assetid: ffa3d5c9-91e5-4da3-b409-560b0c7fbbf0
msc.legacyurl: /web-pages/readme/beta3
msc.type: content
ms.openlocfilehash: dc1d9237c04a7fcdbf4db6ccc8c36d255f6de003
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510341"
---
# <a name="web-matrix-and-aspnet-web-pages-razor-beta-3-release-readme"></a>WebMatrix 및 ASP.NET 웹 페이지(Razor) 베타 3 릴리스 추가 정보

> WebMatrix 및 ASP.NET 웹 페이지(Razor) 베타 3 릴리스 추가 정보

9 11 월 2010

## <a name="contents"></a>콘텐츠

- [개요](#Overview)
- [설치](#Installation_Notes)
- [베타 3 릴리스의 새로운 기능, 변경 사항 및 알려진 문제](#Known_Issues)

    - [WebMatrix 설치 문제](#Known_Issues_Installation)
    - [ASP.NET 웹 페이지 2](#Known_Issues_ASPNET)
    - [SQL Server Compact](#Known_Issues_SQL_Server_Compact)
    - [응용 프로그램 설치](#Known_Issues_Installing_Applications)
    - [응용 프로그램 게시](#Known_Issues_Publishing_Applications)
    - [기타 문제](#Known_Issues_Other_Issues)
- [자세한 내용](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a>개요

> Microsoft WebMatrix Beta는 몇 분 안에 설치 되는 무료 웹 개발 스택입니다. 웹 서버를 데이터베이스 및 프로그래밍 프레임 워크와 통합 하 여 통합 된 단일 환경을 만듭니다. WebMatrix Beta를 사용 하 여 사용자 고유의 ASP.NET 또는 PHP 웹 사이트를 코딩, 테스트 및 게시 하는 방법을 간소화 하거나 WebMatrix Beta를 사용 하 여 DotNetNuke, Umbraco, WordPress 또는 Joomla와 같은 인기 있는 오픈 소스 앱을 사용 하 여 새 웹 사이트를 시작할 수 있습니다. WebMatrix 베타는 인터넷에서 웹 사이트를 실행 하는 동일한 강력한 웹 서버, 데이터베이스 엔진 및 프레임 워크 환경을 사용 하며,이를 통해 개발 환경에서 프로덕션 환경으로 원활 하 고 원활 하 게 전환할 수 있습니다.

<a id="Installation_Notes"></a>

## <a name="installation"></a>설치

> WebMatrix 베타 3을 설치 하려면 [Microsoft 웹 플랫폼 설치 관리자 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)를 사용 합니다. 웹 플랫폼 설치 관리자를 설치한 후 WebMatrix 베타 3을 설치 하는 데 사용할 수 있습니다.
> 
> 설치 하는 동안 문제가 발생 하는 경우 [Microsoft 웹 플랫폼 설치 관리자 문제 해결](https://go.microsoft.com/fwlink/?LinkId=196212)을 참조 하세요.

<a id="Installation_Notes0"></a>

## <a name="instructions-for-publishing-applications"></a>응용 프로그램 게시에 대 한 지침

> [응용 프로그램 게시에 대 한 단계별 지침](https://go.microsoft.com/fwlink/?LinkID=196149) 을 참조 하세요.

<a id="Known_Issues"></a>

## <a name="new-features-changes-andknown-issues"></a>새로운 기능, 변경 사항 및 알려진 문제

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-beta-3-installation"></a>WebMatrix 베타 3 설치

#### <a name="issue-webmatrix-beta-3-is-only-available-on-platforms-that-support-microsoft-net-framework-4"></a>문제: WebMatrix 베타 3은 Microsoft .NET Framework 4를 지 원하는 플랫폼 에서만 사용할 수 있습니다.

> WebMatrix 베타에 .NET Framework 버전 4가 필요 합니다. 경우에 따라 WebMatrix 베타 설치 관리자를 사용 하 여 지원 되는 구성 집합의 일부가 아닌 플랫폼에을 설치할 수 있습니다. 특히 SP1 업데이트가 설치 되지 않은 Windows Vista에서는 WebMatrix 베타 설치를 시작할 수 있지만 .NET Framework 4 구성 요소는 실패 하 고 설치를 차단 합니다.
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

#### <a name="issue-cannot-install-webmatrix-beta-3-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a>문제: Microsoft Visual Studio 2008 s p 1 없이 Microsoft Visual Studio 2008가 설치 된 경우 WebMatrix 베타 3을 설치할 수 없습니다.

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

이 문서의 섹션에서는 Razor 구문와 함께 ASP.NET 웹 페이지 베타 3 릴리스의 새로운 기능, 변경 사항 및 알려진 문제에 대해 설명 합니다.

- [새로운 기능](#NewFeatures)
- [변경](#Changes)
- [문제](#Issues)

<a id="NewFeatures"></a>

#### <a name="new-features-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a>Razor 구문을 사용 하는 ASP.NET 웹 페이지에 대 한 Beta 3의 새로운 기능

#### <a name="new-htmlraw-method-renders-unencoded-markup"></a>New: "Html.actionlink" 메서드는 인코딩되지 않은 태그를 렌더링 합니다.

> 새 `Html.Raw` 메서드를 사용 하면 인코딩된 출력을 렌더링 하는 대신 HTML 태그를 태그로 렌더링할 수 있습니다. 기본적으로 ASP.NET Razor는 렌더링 하기 전에 문자열을 인코딩합니다. 구문은 다음과 같습니다.
> 
> `Html.Raw(value)`
> 
> 다음 예제에서는 `Html.Raw`을 사용하는 방법을 보여 줍니다.
> 
> [!code-cshtml[Main](beta3/samples/sample1.cshtml)]

<a id="Changes"></a>

#### <a name="changes-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a>Razor 구문을 사용 하는 ASP.NET 웹 페이지에 대 한 베타 3의 변경 내용

#### <a name="change-hrefattribute-method-removed"></a>변경: "HrefAttribute" 메서드가 제거 되었습니다.

> `WebPage` 클래스의 `HrefAttribute` 메서드가 제거 되었습니다. 이 도우미는 Url에서 안전 하지 않은 문자를 인코딩하는 데 사용 되었습니다. ASP.NET Razor는 문자열을 자동으로 인코드 하므로 더 이상 필요 하지 않습니다. 새 `Html.Raw` 메서드를 사용 하 여 인코딩되지 않은 문자열을 렌더링 합니다.

#### <a name="change-syntax-for-declarative-helper-helpers-changed"></a>Change: 선언적 "@helper" 도우미의 구문이 변경 되었습니다.

> Beta 3 릴리스에서 ASP.NET는 `@helper` 구문을 사용 하 여 만든 도우미를 구문 분석 하는 방법을 변경 합니다. 기본적으로 `@helper` 구문은 이제 코드를 포함할 수 있는 태그 블록이 아니라 코드 블록으로 구문 분석 됩니다. 따라서 도우미 내의 코드는 `@{ }` 블록으로 묶을 필요가 없습니다. 반대로 도우미 내부의 태그는 HTML 요소나 ASP.NET Razor `<text></text>` 태그에 명시적으로 포함 되어야 합니다.
> 
> 예를 들어 베타 3 릴리스에서는 다음과 같은 `@helper` 구문이 작동 합니다.
> 
> [!code-cshtml[Main](beta3/samples/sample2.cshtml)]
> 
> 베타 3 릴리스에서는 다음 예와 같이이 도우미를 변경 해야 합니다.
> 
> [!code-cshtml[Main](beta3/samples/sample3.cshtml)]
> 
> 도우미에서 초기 코드 주위의 `@{ }` 문자는 더 이상 사용 되지 않습니다. 이는 도우미의 내용이 기본적으로 코드 블록으로 처리 되기 때문입니다. 도우미는 여는 `<a>` 태그로 시작 하는 태그를 렌더링 합니다. 도우미가 닫는 태그 (예: `<meta>` 태그)를 포함 하지 않는 일반 텍스트 또는 태그를 렌더링 해야 하는 경우 렌더링할 콘텐츠가 `<text></text>` 태그에 있어야 합니다.

#### <a name="change-webpagecontexthttpcontext-removed"></a>변경: "WebPageContext" 제거 됨

> `WebPageContext.HttpContext` 속성이 제거되었습니다. 대신 `HttpContext.Current`를 사용하세요. `WebPageContext.HttpContext` 속성은 간단히이를 래핑 했습니다.

#### <a name="change-facebook-helper-moved-to-new-package"></a>변경: "Facebook" 도우미가 새 패키지로 이동 됨

> `Facebook` 도우미가 `Facebook` 도우미 및 추가 기능을 포함 하는 *Facebook* 라이브러리로 이동 되었습니다. [ASP.NET 시작 페이지](https://go.microsoft.com/fwlink/?LinkId=202889)의 "패키지 관리자를 사용 하 여 도우미 설치"에 설명 된 대로이 라이브러리를 별도의 패키지로 설치 해야 합니다.

#### <a name="change-membership-role-and-security-types-moves-to-new-assembly"></a>변경: 멤버 자격, 역할 및 보안 유형이 새 어셈블리로 이동 합니다.

> 다음 형식이 `WebMatrix.WebData` 어셈블리로 이동 되었습니다.
> 
> - `ExtendedMembershipProvider`
> - `SimpleMembershipProvider`
> - `SimpleRoleProvider`
> - `WebSecurity`

#### <a name="change-tagbuilder-class-moved-to-systemwebwebpagesdll-assembly"></a>Change: "빌드하는 tagbuilder" 클래스가 System.object로 이동 되었습니다.

> `TagBuilde` r 클래스가 System.web. 웹 페이지 .dll 어셈블리로 이동 되었습니다. 이전에는 ASP.NET MVC의 일부인 어셈블리에 있었습니다. 이 변경은 `TagBuilder` 클래스를 사용 하기 위해 ASP.NET MVC를 설치할 필요가 없음을 의미 합니다.
> 
> 그러나 클래스는 여전히 `System.Web.Mvc` 네임 스페이스에 있습니다. 사용자 지정 ASP.NET Razor 도우미와 같은 `TagBuilder` 클래스를 사용 하려면 네임 스페이스를 참조 해야 합니다. 예를 들어 코드에 `@using System.Web.Mvc`를 추가 합니다.

#### <a name="change-request-validation-syntax-changed-validation-class-removed"></a>변경: 요청 유효성 검사 구문이 변경 되었습니다. "유효성 검사" 클래스 제거 됨

> 베타 3 릴리스에서 개별 필드 또는 필드 집합에 대 한 유효성 검사를 사용 하지 않도록 설정 하려면 `Validation.Exclude` 메서드를 호출 하 여 유효성 검사에서 제외할 필드의 이름 또는 이름을 전달 합니다. 베타 3 릴리스에서는 유효성 검사를 무시 하는 새 구문을 사용할 수 있습니다. Beta 3에서 사용 되는 `Validation` 메서드가 제거 되었습니다.
> 
> > [!NOTE]
> > 요청 유효성 검사를 사용 하지 않도록 설정 하지 않으면 사용자가 HTML 태그를 업로드 하려고 할 때 (예: 페이지에서 서식 있는 텍스트 편집기 사용) 웹 사이트에서 잠재적으로 위험한 요청 등의 오류를 보고 *합니다. 클라이언트에서 양식 값이 검색* 되 고 사용자 입력이 허용 되지 않습니다. 요청 유효성 검사를 사용 하지 않도록 설정 하는 경우 사용자 입력을 수동으로 확인 하 여 [Microsoft 사이트 간 스크립팅 라이브러리 v 4.0](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651)과 같은 기능을 사용 하는 잠재적으로 위험한 태그나 스크립트가 포함 되지 않았는지 확인 해야 합니다.
> 
> 
> 자동 요청 유효성 검사를 사용 하지 않도록 설정 하려면 `Request.Unvalidated` 메서드를 호출 하 여 요청 유효성 검사를 무시 하려는 필드 또는 다른 게시 개체의 이름을 전달 합니다. 이 메서드를 사용 하 여 `Form`, `QueryString`, `Cookies`및 `ServerVariables` 컬렉션에 있는 항목에 대 한 유효성 검사를 건너뛸 수 있습니다. 다음 예에서는 `Unvalidated` 메서드를 사용 하는 방법을 보여 줍니다.
> 
> [!code-csharp[Main](beta3/samples/sample4.cs)]

<a id="Issues"></a>

#### <a name="known-issues-for-aspnet-web-pages-with-razor-syntax"></a>Razor 구문을 사용한 ASP.NET 웹 페이지의 알려진 문제

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a>문제: 멤버 자격에 사용자 지정 사용자 테이블을 사용할 때 예기치 않은 동작이 발생 합니다.

> ASP.NET Razor 웹 사이트의 멤버 자격 공급자를 초기화 하려면 `WebSecurity.InitializeDatabaseConnection` 메서드를 호출 합니다. (WebMatrix에서 스타터 사이트 템플릿은 *\_AppStart* 파일에이 메서드에 대 한 호출을 포함 합니다.) 이 메서드의 `autoCreateTables` 매개 변수가 true로 설정 되어 있으면 (기본적으로 시작 사이트 템플릿에서 true로 설정 됨) 인식할 수 없는 테이블 이름이 메서드에 전달 되는 경우 (두 번째 매개 변수) 메서드는 오류를 throw 하지 않습니다. 대신 테이블을 자동으로 만듭니다.
> 
> 멤버 자격에 사용자 지정 사용자 테이블을 사용 하지만 잘못 된 테이블 이름을 `WebSecurity.InitializeDatabaseConnection` 메서드에 전달 하려는 경우에이 문제가 발생할 수 있습니다. 사용자가 지정 하는 테이블이 존재 하지 않는 경우 메서드는 기본적으로 오류를 발생 시 키 지 않으며 대신 새 테이블을 만드는 경우 응용 프로그램이 작동 하는 것 처럼 보일 수 있습니다. 그러나 사용자 지정 사용자 테이블을 사용 하는 응용 프로그램 코드 (및 그 안에 포함 된 필드)는 결국 예기치 않은 오류로 인해 실패할 수 있습니다.
> 
> **해결 방법**  
> `InitializeDatabaseConnection` 메서드에 전달 된 이름이 멤버 자격 데이터베이스의 사용자 프로필 테이블과 일치 하는지 확인 하거나 `autoCreateTables` 매개 변수가 false로 설정 되어 있는지 확인 합니다.

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a>문제: "SQL Server 사용자 인스턴스를 생성 하지 못했습니다." 오류

> WebMatrix 웹 응용 프로그램이 SQL Server Express를 사용 하 고 Windows 7 또는 Windows Server 2008 r 2에서 IIS 7.5를 실행 하는 경우 SQL Server에서 사용자의 로컬 응용 프로그램 경로를 런타임에 검색할 수 없음을 나타내는 오류가 표시 될 수 있습니다.
> 
> **해결 방법** 응용 프로그램이 실행 되는 Windows 계정 (일반적으로 NETWORK SERVICE)에 응용 프로그램의 루트 폴더와 *앱\_데이터*와 같은 하위 폴더에 대 한 읽기/쓰기 권한이 있는지 확인 합니다. 자세한 내용은 기술 자료 문서 [SQL Server Express 사용자 인스턴스 및 ASP.net 웹 응용 프로그램 프로젝트 문제](https://support.microsoft.com/kb/2002980)에서 확인할 수 있습니다.

#### <a name="issue-in-visual-studio-namespaces-for-custom-assemblies-dlls-are-not-imported-automatically"></a>문제: Visual Studio에서 사용자 지정 어셈블리 (Dll)의 네임 스페이스를 자동으로 가져오지 않습니다.

> Visual Studio의 프로젝트에서 사용자 지정 어셈블리를 사용 하는 경우 해당 어셈블리에 선언 된 네임 스페이스는 디자인 타임에 자동으로 가져오지 않습니다. 따라서 사용자 지정 형식에 대 한 참조가 디자인 타임에 인식 되지 않을 수 있으며 Visual Studio에서 인식 되지 않는 것으로 표시 됩니다 ("물결선" 사용). 이 문제는 Visual Studio의 디자인 타임에만 발생 합니다. 응용 프로그램 자체는 정상적으로 실행 됩니다.
> 
> **해결 방법**  
> 디자인 타임에 인식 되지 않는 엔터티를 참조 하는 `using` 문 (Visual Basic의`imports`)을 포함 합니다.

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a>문제: Visual Studio IntelliSense 및 프로젝트 템플릿은 ASP.NET MVC 버전 3 에서만 사용할 수 있습니다.

> ASP.NET 웹 페이지를 설치 해도 ASP.NET 웹 페이지 응용 프로그램용 IntelliSense 및 프로젝트 템플릿과 같은 Visual Studio 용 도구도 설치 되지 않습니다.
> 
> **해결 방법** Visual Studio에서 ASP.NET 웹 페이지 응용 프로그램에 대 한 IntelliSense 및 프로젝트 템플릿을 사용 하려면 웹 플랫폼 설치 관리자 또는 [독립 실행형 설치 관리자](https://go.microsoft.com/fwlink/?LinkID=191797)를 통해 ASP.NET MVC 3 RC를 설치 합니다.

#### <a name="issue-lthelpergt-class-cannot-be-found-error"></a>문제: "&lt;도우미&gt; 클래스를 찾을 수 없습니다." 오류

> 베타 3으로 업그레이드 한 후에는 도우미 클래스 (예: `Facebook` 클래스)를 찾을 수 없다는 오류가 표시 될 수 있습니다. Beta 2부터 시작 하 여 베타 3에서 계속 하면 도우미가 명시적으로 설치 해야 하는 패키지로 이동 했습니다. 기존 사이트는 이러한 패키지를 포함 하도록 업그레이드 되지 않습니다. 여기에는 *\My Documents\IISExpress* 또는 *\My Documents\My 웹 사이트* 폴더의 사이트가 포함 됩니다. 특히 `Twitter` 도우미에 대 한 참조를 포함 하는 *내 사이트* (WebSite1)에서 기본 사이트를 사용 하는 경우이 오류가 표시 됩니다.
> 
> **해결 방법**  
> 사이트의 모든 도우미에 대 한 호출을 주석으로 처리 하 고 *\_관리* 페이지를 실행 한 다음 사용 하려는 도우미가 포함 된 패키지를 설치 합니다. 패키지를 설치한 후에는 도우미를 참조 하는 줄의 주석 처리를 제거 하면 됩니다.

#### <a name="issue-deploying-beta-3-aspnet-razor-assemblies-to-the-bin-folder-might-not-work-on-hosting-sites"></a>문제: 호스트 사이트에서 베타 3 ASP.NET Razor 어셈블리를 Bin 폴더에 배포 하는 작업이 작동 하지 않을 수 있음

> 호스팅 사이트에 ASP.NET 웹 페이지 웹 사이트를 배포 하 고 사이트의 *Bin* 폴더에 ASP.NET Razor Beta 3 어셈블리를 배포 하는 경우 다음과 같은 오류가 발생할 수 있습니다.
> 
> `Could not load type 'Microsoft.Web.Infrastructure.DynamicModuleHelper.DynamicModuleUtility' from assembly 'Microsoft.Web.Infrastructure, Version=1.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`
> 
> 이 문제는 호스팅 공급자가 서버의 GAC (전역 응용 프로그램 캐시)에 ASP.NET 웹 페이지 Beta 1 어셈블리를 설치한 경우에 발생할 수 있습니다. GAC의 어셈블리는 *Bin* 폴더에 로컬로 설치 된 어셈블리 보다 우선적으로 적용 됩니다.
> 
> **해결 방법** 호스팅 공급자에 게 문의 하 여 발생 한 오류가 공급자의 어셈블리 버전과 사용자의 어셈블리 버전 간 충돌로 인 한 것인지 확인 합니다. 이 경우 호스팅 공급자가 서버의 GAC에서 어셈블리를 업데이트 하도록 요청 합니다.

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a>문제: 프록시 서버를 통해 피드 또는 기타 외부 데이터 읽기

> 사이트를 실행 하는 서버가 프록시 서버 뒤에 있는 경우 사이트 외부에서 제공 되는 정보를 읽을 수 있도록 *web.config 파일에서* 프록시 정보를 구성 해야 할 수 있습니다. 예를 들어 `ReCaptcha` 도우미를 사용 하는 경우 도우미가 reCAPTCHA 서비스와 통신 하지만 프록시 서버에 의해 차단 될 수 있습니다. 마찬가지로 패키지 관리자에서 사용 하는 피드와 같이 ASP.NET 웹 페이지에 사용 되는 피드에는 프록시 구성이 필요할 수 있습니다.
> 
> 외부 서비스를 사용 하거나 패키지 피드를 사용 하 여 작업 하는 데 문제가 발생 하는 경우 응용 프로그램의 루트 web.config 파일에 다음 요소를 *추가 합니다.*
> 
> [!code-xml[Main](beta3/samples/sample5.xml)]
> 
> 프록시 서버를 구성 하는 방법에 대 한 자세한 내용은 MSDN 웹 사이트에서 [&lt;프록시&gt; 요소 (네트워크 설정)](https://msdn.microsoft.com/library/sa91de1e.aspx) 를 참조 하십시오.

#### <a name="issue-microsoftwebinfrastructuredll-cannot-be-loaded-error"></a>문제: "Microsoft web.config .dll을 로드할 수 없습니다." 오류

> 이전에 Razor 구문를 사용 하 여 ASP.NET 웹 페이지 베타 1 버전을 설치 하 고 베타 3 버전을 설치 하는 경우에는 해당 하는 모든 어셈블리가 *Microsoft web.config*를 제외 하 고 GAC에 설치 됩니다. 결과적으로 ASP.NET Razor 페이지를 실행할 때 *Microsoft web.config .dll* 을 로드할 수 없음을 나타내는 오류가 표시 됩니다.
> 
> 클린 컴퓨터에서 베타 3 릴리스를 로드 한 경우에는이 문제가 발생 하지 않습니다.
> 
> **해결 방법**  
> 제어판에서 ASP.NET 웹 페이지를 제거 합니다. 그런 다음 베타 3 릴리스를 다시 설치 합니다.

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a>문제: .NET Framework 버전 4를 제거 하면 Razor 구문을 사용 하 여 ASP.NET 웹 페이지 사용 하지 않도록 설정 됩니다.

> .NET Framework 버전 4를 제거한 후 다시 설치 하는 경우 Razor 구문 사용 하지 않도록 설정 된 ASP.NET 웹 페이지. 확장명이 *cshtml* 인 페이지는 올바르게 실행 되지 않습니다. ASP.NET 웹 페이지는 컴퓨터 루트 *web.config* 파일에 어셈블리를 등록 하 고 .NET Framework 제거 하면 해당 파일이 제거 됩니다. .NET Framework를 다시 설치 하면 새 버전의 구성 파일이 설치 되지만 ASP.NET 웹 페이지 어셈블리에 대 한 참조는 추가 되지 않습니다.
> 
> **해결 방법** .NET Framework를 다시 설치한 후 Razor 구문를 사용 하 여 ASP.NET 웹 페이지를 다시 설치 합니다. 그러면 다음 요소가 컴퓨터 루트의 web.config *파일에* 추가 됩니다 .이 파일은 일반적으로 다음 위치에 있습니다.  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> 
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](beta3/samples/sample6.xml)]

#### <a name="issue-applications-previously-deployed-with-aspnet-assemblies-in-the-bin-folder-experience-errors"></a>문제: Bin 폴더에 ASP.NET 어셈블리를 사용 하 여 이전에 배포한 응용 프로그램에서 오류가 발생 합니다.

> 배포 하는 동안 ASP.NET 웹 페이지 어셈블리 (예: *Microsoft. 웹 페이지*)의 복사본은 서버에 있는 웹 사이트의 *Bin* 폴더에 복사 됩니다. 이는 배포 중에 자동으로 발생 하거나 개발자가 어셈블리를 명시적으로 복사한 경우에 발생할 수 있습니다. 그러나 베타 3 릴리스가 설치 될 때 특정 유형을 찾을 수 없다는 오류와 같은 오류가 발생 합니다. 이는 여러 ASP.NET 웹 페이지 형식이 Beta 3 릴리스에 대 한 다른 네임 스페이스로 이동 되었기 때문에 발생 합니다.
> 
> **해결 방법**   
> 배포 된 응용 프로그램의 *Bin* 폴더를 지우고 새 어셈블리를 폴더에 복사 하거나 응용 프로그램을 다시 배포 하 고 응용 프로그램을 다시 시작 합니다.

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
> 
> [!code-xml[Main](beta3/samples/sample7.xml)]

#### <a name="issue-using-web-application-project-or-aspnet-mvc-and-aspnet-web-pages-in-the-same-application"></a>문제: 웹 응용 프로그램 프로젝트 또는 ASP.NET MVC를 사용 하 고 동일한 응용 프로그램에서 웹 페이지 ASP.NET

> 웹 응용 프로그램 프로젝트 또는 ASP.NET MVC 응용 프로그램에서 ASP.NET 웹 페이지를 사용 하는 경우 *WebPageHttpApplication* 를 찾을 수 없다는 오류가 표시 될 수 있습니다.
> 
> **해결 방법**  
> 이 오류가 발생 하는 경우 응용 프로그램이 파생 되는 기본 클래스를 변경 합니다. *Global.asax* 파일에서 다음 줄을 변경 합니다.
> 
> [!code-csharp[Main](beta3/samples/sample8.cs)]
> 
> 값:
> 
> [!code-csharp[Main](beta3/samples/sample9.cs)]
> 
> 이는 Razor 구문와 ASP.NET 웹 페이지 베타 1 릴리스에 대해 도입 된 변경 내용을 취소 합니다.

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a>문제: SQL Server Compact 설치 되지 않은 컴퓨터에 응용 프로그램 배포

> SQL Server Compact 데이터베이스를 포함 하는 응용 프로그램은 SQL Server Compact가 설치 되지 않은 컴퓨터에서 실행할 수 있습니다. Microsoft WebMatrix 베타 3은 이러한 이진 파일을 자동으로 복사 하 고 *적절 한* web.config 파일 변환을 수행 합니다.
> 
> **해결 방법** 이러한 파일을 복사 하 고 *web.config 파일을* 수동으로 변경 하려면 다음을 수행 합니다.
> 
> 1. 대상 컴퓨터에 있는 응용 프로그램의 *Bin* 폴더 (및 하위 폴더)에 데이터베이스 엔진 어셈블리를 복사 합니다. 
> 
>     - *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* **를** *\bin* 에 복사 합니다.
>     - *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* * **를** *\Bin\x86* 에 복사 합니다.
>     - *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\* * **를** *\Bin\amd64* 에 복사 합니다.
> 2. *웹* 사이트의 루트 폴더에서 web.config 파일을 만들거나 엽니다. (WebMatrix 베타 3에서는 **파일 형식 선택** 대화 상자에서 **모두** 를 클릭 하는 경우이 파일 형식을 사용할 수 있습니다.)
> 3. 다음 요소를 **&lt;system.web&gt;** 요소 내부가 아닌 **&lt;구성&gt;** 요소의 자식으로 추가 합니다.
> 
> 
> [!code-xml[Main](beta3/samples/sample10.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a>문제: 데이터베이스 및 WebGrid 도우미가 Visual Basic의 보통 신뢰에서 작동 하지 않음

> Visual Basic를 사용 하는 경우 ( *vbhtml* 파일 만들기) 응용 프로그램이 보통 신뢰를 사용 하도록 설정 된 경우 `Database` 및 `WebGrid` 도우미가 작동 하지 않습니다.
> 
> **해결 방법**  
> 완전 신뢰를 사용 하도록 응용 프로그램을 일시적으로 설정 합니다.

<a id="Known_Issues_SQL_Server_Compact"></a>
### <a name="sql-server-compact"></a>SQL Server Compact

#### <a name="issue-encrypt-property-is-not-recognized"></a>문제: "Encrypt" 속성이 인식 되지 않습니다.

> SQL Server Compact 4.0는 `SqlCeConnection` 클래스의 `Encrypt` 속성을 인식 하지 못합니다. 데이터베이스 파일을 암호화 하는 데이 속성을 사용 하면 안 됩니다. `Encrypt` 속성은 SQL Server Compact 3.5 릴리스에서 사용 되지 않으며 이전 버전과의 호환성을 위해서만 유지 되었습니다. 
> 
> **해결 방법**  
> `SqlCeConnection` 클래스의 `Encryption Mode` 속성을 사용 하 여 SQL Server Compact 4.0 데이터베이스 파일을 암호화 합니다. 다음 예에서는 `Encryption Mode` 속성을 사용 하 여 암호화 된 SQL Server Compact 4.0 데이터베이스를 만드는 방법을 보여 줍니다.
> 
> [!code-csharp[Main](beta3/samples/sample11.cs)]
> 
> [!code-vb[Main](beta3/samples/sample12.vb)]
> 
> 기존 SQL Server Compact 4.0 데이터베이스의 암호화 모드를 변경 하려면 다음을 수행 합니다.
> 
> [!code-csharp[Main](beta3/samples/sample13.cs)]
> 
> [!code-vb[Main](beta3/samples/sample14.vb)]
> 
> 암호화 되지 않은 SQL Server Compact 4.0 데이터베이스를 암호화 하려면 다음을 수행 합니다.
> 
> [!code-csharp[Main](beta3/samples/sample15.cs)]
> 
> [!code-vb[Main](beta3/samples/sample16.vb)]

#### <a name="issue-microsoft-visual-c-2008-runtime-libraries-are-required"></a>문제: Microsoft Visual C++ 2008 런타임 라이브러리가 필요 합니다.

> SQL Server Compact 4.0의 네이티브 Dll에는 Microsoft Visual C++ 2008 런타임 라이브러리 (X86, IA64 및 X64) 서비스 팩 1이 필요 합니다.
> 
> **해결 방법**  
> .NET Framework 3.5 SP1을 설치 합니다. 또한 Visual C++ 2008 런타임 라이브러리 s p 1을 설치 합니다. 다음 위치에서 라이브러리를 다운로드할 수 있습니다.   
>   
> [Microsoft Visual C++ 2008 서비스 팩 1 재배포 가능 패키지 ATL 보안 업데이트](https://go.microsoft.com/fwlink/?LinkId=194827)
> 
> [!NOTE]
> 2\.0, 3.0 또는 4 .NET Framework 설치 하는 경우 Visual C++ 2008 런타임 라이브러리 s p 1이 설치 *되지* 않습니다.

#### <a name="issue-if-sql-server-compact-is-installed-prior-to-installing-net-framework-on-the-computer-its-provider-invariant-name-is-not-registered-in-the-net-framework-machineconfig-file"></a>문제: 컴퓨터에 .NET Framework를 설치 하기 전에 SQL Server Compact 설치 된 경우 공급자 고정 이름이 .NET Framework machine.config 파일에 등록 되지 않습니다.

> SQL Server Compact에는 .NET Framework가 필요 하기 때문에 .NET Framework가 설치 되지 않은 컴퓨터에 SQL Server Compact를 설치할 수 있습니다. SQL Server Compact를 설치 하기 전에 .NET Framework 버전 3.5 또는 4를 모두 설치 하지 않은 경우에는 SQL Server Compact 설치 프로그램이 *machine.config 파일에* 공급자 고정 이름을 등록 하지 않습니다. *Machine.config 파일의* SQL Server Compact 항목에 의존 하는 모든 응용 프로그램은 실패 합니다. *Machine.config의 고정* 이름 등록 항목은 다음 예제와 같습니다.
> 
> [!code-xml[Main](beta3/samples/sample17.xml)]
> 
> **해결 방법**  
> SQL Server Compact 4.0 CTP1을 제거 합니다. 다음 위치에서 .NET Framework의 전체 버전을 다운로드 하 여 설치 합니다.
> 
> [Microsoft .NET Framework 3.5 서비스 팩 1 (전체 패키지)](https://go.microsoft.com/fwlink/?LinkId=194828)  
> [Microsoft .NET Framework 4.0 릴리스 (전체 패키지)](https://www.microsoft.com/downloads/details.aspx?FamilyID=9cfb2d51-5ff4-4491-b0e5-b386f32c0992&amp;displaylang=en)
> 
> 그런 다음 [SQL Server Compact 4.0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en)를 다시 설치 합니다.

<a id="Known_Issues_Installing_Applications"></a>

### <a name="installing-applications"></a>애플리케이션 설치

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a>문제: 사용자의 내 문서 폴더가 네트워크 공유로 리디렉션되는 경우 응용 프로그램을 설치 하는 데 시간이 오래 걸릴 수 있습니다.

> **해결 방법**  
> 없음 응용 프로그램을 설치 하는 데 약간의 시간이 걸릴 수 있지만 제대로 설치 됩니다.

<a id="Known_Issues_Publishing_Applications"></a>

### <a name="publishing-applications"></a>응용 프로그램 게시

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

<a id="Known_Issues_Other_Issues"></a>

### <a name="other-issues"></a>기타 이슈

#### <a name="issue-searchfilter-does-not-work-in-reports-for-group-by-issue-type"></a>문제: 검색/필터가 Group By에 대 한 보고서: 문제 유형에서 작동 하지 않음

> 사이트에 대 한 보고서를 실행할 때 *URL로 필터링* 상자에 텍스트를 입력 하 고 *검색*을 클릭 하면 아무 일도 발생 하지 않습니다. 이는 보고서의 *Group By* 상태가 *Issue 유형*(기본값)으로 설정 되어 있는 동안이 컨트롤이 작동 하지 않기 때문입니다.
> 
> **해결 방법** 리본 메뉴의 *그룹화* 방법 탭에서 *url* 을 클릭 하 여 원본 url로 항목을 그룹화 합니다. 이 상태에서 항목을 필터링 하는 텍스트 상자와 단추가 작동 합니다.

#### <a name="issue-wcf-applications-fail-to-run-with-iis-express"></a>문제: IIS Express 사용 하 여 WCF 응용 프로그램을 실행 하지 못함

> WCF 응용 프로그램을 탐색 하면 다음과 같은 오류가 발생 합니다.
> 
> *파일이 나 어셈블리 ' 7.0.0.0, Version =, Culture = 중립, PublicKeyToken = 31bf3856ad364e35 ' 또는 해당 종속성 중 하나를 로드할 수 없습니다. 시스템에서 지정 된 파일을 찾을 수 없습니다.*
> 
> 이는 IIS Express 베타 버전이 기본적으로 WCF를 지원 하지 않기 때문에 발생 합니다.
> 
> **해결 방법** 다음 해결 방법 중 하나를 사용 합니다 (해결 방법 #2 Microsoft Windows Vista 이상이 필요 함).
> 
> 
> 1. WebMatrix 설치 위치에서 WCF 응용 프로그램의 *bin* 디렉터리에 *Microsoft Web.config* 및 *microsoft web.config .dll* 어셈블리를 복사 합니다. 기본적으로 WebMatrix는 시스템의 *Program Files* 폴더 아래에 있는 *Microsoft webmatrix* 하위 폴더에 설치 됩니다.
> 2. Microsoft Windows Vista 이상에서 다음 명령을 사용 하 여 *bin* 디렉터리의 어셈블리에 대 한 symlink를 만듭니다. 이 방법은 어셈블리의 복사본을 만들지 않는다는 장점이 있습니다.
> 
>     [!code-console[Main](beta3/samples/sample18.cmd)]
> 3. GAC에 두 어셈블리를 설치 합니다. 관리자 권한 프롬프트에서 다음 명령을 실행 합니다.
> 
>     [!code-console[Main](beta3/samples/sample19.cmd)]

#### <a name="issue-webmatrix-beta-3-is-unable-to-perform-certain-tasks-that-require-elevation"></a>문제: WebMatrix 베타 3은 권한 상승이 필요한 특정 작업을 수행할 수 없습니다.

> WebMatrix 베타 3은 다음과 같은 상황에서 추가 구성 요소를 설치 하는 등 권한 상승이 필요한 특정 작업을 수행할 수 없습니다.
> 
> - Windows Vista 또는 Windows 7에서 관리 권한이 없고 UAC (사용자 계정 컨트롤)를 사용할 수 없는 계정으로 로그인 합니다.
> - Microsoft Windows XP 또는 Microsoft Windows Server 2003를 사용 하 고 있습니다.
> 
> **해결 방법**  
> WebMatrix 베타 3의 모든 작업에는 관리 권한이 필요 하지 않습니다. 이렇게 하려면 관리자 권한으로 작업을 수행 하거나 다음 단계를 수행 하면 됩니다.
> 
> - Windows Vista 또는 Windows 7에서 UAC를 사용 하도록 설정 합니다.
> - Windows XP에서 관리자 보안 그룹에 사용자를 추가 합니다.

#### <a name="issue-site-from-web-gallery-is-disabled"></a>문제: "웹 갤러리에서 사이트"를 사용할 수 없습니다.

> 웹 플랫폼 설치 관리자 3.0가 설치 되어 있지 않으면 **웹 갤러리에서 사이트** 옵션을 사용할 수 없습니다.
> 
> **해결 방법**  
> [Microsoft 웹 플랫폼 설치 관리자 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)을 설치 합니다.

#### <a name="issue-on-windows-server-2003-iis-express-does-not-start-for-a-non-administrative-user"></a>문제: Windows Server 2003에서 관리자가 아닌 사용자에 대 한 IIS Express 시작 되지 않음

> Windows Server 2003에서 페이지를 시작 하거나 IIS Express를 시작 하면 IIS Express 시작 되지 않습니다. 웹 페이지의 경우 관리자가 아닌 사용자가 응용 프로그램을 시작 했음을 나타내는 오류가 표시 됩니다.
> 
> **해결 방법**  
> 관리자가 WebMatrix 베타 3를 시작 합니다. 자세한 내용은 다음 기술 자료 문서를 참조 하십시오.  
>   
> [관리자가 아닌 사용자가 시작한 응용 프로그램은 Windows Vista, Windows Server 2003 또는 Windows XP에서 응용 프로그램이 실행 되 고 있는 컴퓨터의 HTTP 트래픽을 수신할 수 없습니다.](https://support.microsoft.com/kb/939786)

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

#### <a name="issue-the-relationships-button-is-disabled"></a>문제: "관계" 단추를 사용할 수 없습니다.

> **데이터베이스** 작업 영역의 **테이블** 탭에 있는 **관계** 단추는 SQL Server Compact 데이터베이스에서 사용할 수 없습니다.
> 
> **해결 방법**  
> 없음 SQL Server Compact은 테이블 간의 관계를 지원 하지 않습니다.

#### <a name="issue-parameterized-sql-queries-throw-exceptions"></a>문제: 매개 변수가 있는 SQL 쿼리가 예외를 throw 합니다.

> SQL Server Compact 4.0에서 매개 변수가 있는 쿼리의 매개 변수에 대해 `SqlDbType` 또는 `DbType` 같은 데이터 형식을 지정 하지 않으면 쿼리가 실행 될 때 예외가 throw 됩니다.
> 
> **해결 방법**  
> `SqlDbType` 또는 `DbType`와 같은 매개 변수의 데이터 형식을 명시적으로 설정 합니다. BLOB 데이터 형식 (`image` 및 `ntext`)의 경우이는 중요 합니다. 다음과 같은 코드를 사용 합니다.
> 
> [!code-sql[Main](beta3/samples/sample20.sql)]
> 
> [!code-vb[Main](beta3/samples/sample21.vb)]

<a id="More_Info"></a>

## <a name="for-more-information"></a>참조 항목

WebMatrix 베타 3에 대 한 자세한 내용은 다음 웹 사이트를 참조 하세요.

- [IIS.net](http://iis.net/)
- [ASP.NET](https://asp.net/webmatrix)
- [Microsoft.com/web](https://www.microsoft.com/web)

---

© 2010 Microsoft Corporation. All Rights Reserved. [사용 약관](https://msdn.microsoft.cos/cc300389.aspx).
