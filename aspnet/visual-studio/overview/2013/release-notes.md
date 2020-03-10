---
uid: visual-studio/overview/2013/release-notes
title: Visual Studio 2013 릴리스 정보에 대 한 ASP.NET 및 Web Tools | Microsoft Docs
author: microsoft
description: 이 문서에서는 Visual Studio 2013의 ASP.NET 및 Web Tools 릴리스에 대해 설명 합니다.
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: d8af9c8e7ee1316a5eac90c5959d07c628154e09
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449525"
---
# <a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a>Visual Studio 2013용 ASP.NET 및 Web Tools 릴리스 정보

[Microsoft](https://github.com/microsoft) 에서

> 이 문서에서는 Visual Studio 2013의 ASP.NET 및 Web Tools 릴리스에 대해 설명 합니다.

## <a name="contents"></a>콘텐츠

- [설치 참고 사항](#TOC1)
- [설명서](#TOC2)
- [소프트웨어 요구 사항](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>Visual Studio 2013 ASP.NET 및 Web Tools의 새로운 기능

- [ASP.NET 1 개](#TOC6)
- [새 웹 프로젝트 환경](#newproj)
- [ASP.NET 스 캐 폴딩](#scaffold)
- [브라우저 링크](#browser-link)
- [Visual Studio 웹 편집기의 향상 된 기능](#web-editor)
- [Visual Studio에서 Web Apps 지원 Azure App Service](#waws)
- [웹 게시 향상](#publish)
- [NuGet 2.7](#nuget)
- [ASP.NET Web Forms](#TOC9)
- [ASP.NET MVC 5](#TOC10)
- [ASP.NET Web API 2](#TOC11)
- [ASP.NET SignalR](#TOC13)
- [ASP.NET Identity](#TOC8)
- [Microsoft OWIN 구성 요소](#TOC7)
- [Entity Framework 6](#ef6)
- [ASP.NET Razor 3](#TOC14)
- [ASP.NET 앱 일시 중단](#TOC15)
- [알려진 문제 및 주요 변경 내용](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a>설치 참고 사항

Visual Studio 2013에 대 한 ASP.NET 및 Web Tools는 기본 설치 관리자에 번들로 제공 되며 [여기](https://www.asp.net/downloads)에서 다운로드할 수 있습니다.

<a id="TOC2"></a>
## <a name="documentation"></a>문서화

Visual Studio 2013 ASP.NET 및 Web Tools에 대 한 자습서 및 기타 정보는 [ASP.NET 웹 사이트](https://www.asp.net/)에서 확인할 수 있습니다.

<a id="TOC4"></a>
## <a name="software-requirements"></a>소프트웨어 요구 사항

ASP.NET 및 Web Tools에는 Visual Studio 2013 필요 합니다.

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>Visual Studio 2013 ASP.NET 및 Web Tools의 새로운 기능

다음 섹션에서는 릴리스에 도입 된 기능에 대해 설명 합니다.

<a id="TOC6"></a>
## <a name="one-aspnet"></a>ASP.NET 1 개

Visual Studio 2013 릴리스에서는 ASP.NET 기술을 사용 하는 환경을 통합 하는 단계를 수행 하 여 원하는 것을 쉽게 조합 하 고 일치 시킬 수 있습니다. 예를 들어 MVC를 사용 하 여 프로젝트를 시작 하 고 나중에 Web Forms 페이지를 프로젝트에 쉽게 추가 하거나 Web Forms 프로젝트에서 웹 Api를 스 캐 폴드 수 있습니다. 한 가지 ASP.NET는 개발자가 ASP.NET에서 선호 하는 작업을 수행 하는 데 도움이 되는 것입니다. 선택한 기술에 관계 없이 하나의 ASP.NET 신뢰할 수 있는 기본 프레임 워크를 기반으로 하는 확신을 가질 수 있습니다.

<a id="newproj"></a>
## <a name="new-web-project-experience"></a>새 웹 프로젝트 환경

Visual Studio 2013에서 새 웹 프로젝트를 만드는 환경을 향상 시켰습니다. **새 ASP.NET 웹 프로젝트** 대화 상자에서 원하는 프로젝트 형식을 선택 하 고, 기술의 조합 (WEB FORMS, MVC, Web API)을 구성 하 고, 인증 옵션을 구성 하 고, 단위 테스트 프로젝트를 추가할 수 있습니다.

![새 ASP.NET 프로젝트](release-notes/_static/image1.png)

새 대화 상자를 사용 하 여 많은 템플릿에 대 한 기본 인증 옵션을 변경할 수 있습니다. 예를 들어 ASP.NET Web Forms 프로젝트를 만들 때 다음 옵션 중 하나를 선택할 수 있습니다.

- 인증 없음
- 개별 사용자 계정 (ASP.NET 멤버 자격 또는 소셜 공급자 로그인)
- 조직 계정 (인터넷 응용 프로그램의 Active Directory)
- Windows 인증 (인트라넷 응용 프로그램의 Active Directory)

![인증 옵션](release-notes/_static/image2.png)

웹 프로젝트를 만드는 새 프로세스에 대 한 자세한 내용은 [Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기](creating-web-projects-in-visual-studio.md)를 참조 하세요. 새 인증 옵션에 대 한 자세한 내용은이 문서의 뒷부분에 나오는 [ASP.NET Identity](#TOC8) 를 참조 하세요.

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a>ASP.NET 스 캐 폴딩

ASP.NET 스 캐 폴딩은 ASP.NET 웹 응용 프로그램에 대 한 코드 생성 프레임 워크입니다. 이를 통해 데이터 모델과 상호 작용 하는 상용구 코드를 프로젝트에 쉽게 추가할 수 있습니다.

이전 버전의 Visual Studio에서 스 캐 폴딩은 ASP.NET MVC 프로젝트로 제한 되었습니다. Visual Studio 2013를 사용 하 여 이제 Web Forms를 비롯 한 모든 ASP.NET 프로젝트에 스 캐 폴딩을 사용할 수 있습니다. Visual Studio 2013는 현재 Web Forms 프로젝트에 대 한 페이지 생성을 지원 하지 않지만 프로젝트에 MVC 종속성을 추가 하 여 Web Forms에서 스 캐 폴딩을 계속 사용할 수 있습니다. Web Forms에 대 한 페이지 생성 지원은 향후 업데이트에서 추가 될 예정입니다.

스 캐 폴딩을 사용 하는 경우 모든 필수 종속성이 프로젝트에 설치 되어 있는지 확인 합니다. 예를 들어 ASP.NET Web Forms 프로젝트로 시작한 다음 스 캐 폴딩을 사용 하 여 Web API 컨트롤러를 추가 하는 경우 필요한 NuGet 패키지와 참조가 프로젝트에 자동으로 추가 됩니다.

Web Forms 프로젝트에 MVC 스 캐 폴딩을 추가 하려면 **새 스 캐 폴드 항목** 을 추가 하 고 대화 상자 창에서 **mvc 5 종속성** 을 선택 합니다. MVC 스 캐 폴딩에 대 한 두 가지 옵션이 있습니다. 최소 및 전체. 최소를 선택 하면 ASP.NET MVC에 대 한 NuGet 패키지 및 참조만 프로젝트에 추가 됩니다. 전체 옵션을 선택 하는 경우 최소 종속성 뿐만 아니라 MVC 프로젝트에 필요한 콘텐츠 파일이 추가 됩니다.

비동기 컨트롤러 스 캐 폴딩에 대 한 지원은 Entity Framework 6의 새로운 비동기 기능을 사용 합니다.

자세한 내용 및 자습서는 [ASP.NET 스 캐 폴딩 개요](aspnet-scaffolding-overview.md)를 참조 하세요.

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a>브라우저 링크 – 브라우저와 Visual Studio 간 SignalR channel

새 [브라우저 링크](using-browser-link.md) 기능을 사용 하 여 여러 브라우저를 Visual Studio에 연결 하 고 도구 모음에서 단추를 클릭 하 여 모두 새로 고칠 수 있습니다. 모바일 에뮬레이터를 포함 하 여 여러 브라우저를 개발 사이트에 연결 하 고 새로 고침을 클릭 하 여 모든 브라우저를 동시에 새로 고칠 수 있습니다. 또한 브라우저 링크는 개발자가 브라우저 링크 확장을 작성할 수 있도록 API를 노출 합니다.

![](release-notes/_static/image3.png)

개발자가 브라우저 링크 API를 활용할 수 있도록 하 여 Visual Studio와 연결 된 브라우저 간에 경계를 교차 하는 매우 고급 시나리오를 만들 수 있습니다. Web Essentials는 API를 활용 하 여 Visual Studio와 브라우저의 개발자 도구 간에 통합 된 환경을 만듭니다. 원격으로 모바일 에뮬레이터를 제어 하 고 더 많은 작업을 수행 합니다.

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a>Visual Studio 웹 편집기의 향상 된 기능

Visual Studio 2013에는 웹 응용 프로그램의 Razor 파일 및 HTML 파일용 새 HTML 편집기가 포함 되어 있습니다. 새 HTML 편집기는 HTML5를 기반으로 하는 단일 통합 스키마를 제공 합니다. 자동 중괄호 완성, jQuery UI 및 AngularJS 특성 IntelliSense, 특성 IntelliSense 그룹화, ID 및 클래스 이름 Intellisense, 향상 된 성능, 형식 지정 및 스마트 태그를 비롯 한 기타 향상 된 기능을 포함 합니다.

다음 스크린샷에서는 HTML 편집기에서 부트스트랩 특성 IntelliSense를 사용 하는 방법을 보여 줍니다.

![HTML 편집기의 Intellisense](release-notes/_static/image4.png)

Visual Studio 2013는 CoffeeScript 및 LESS 편집기가 모두 내장 되어 제공 됩니다. LESS 편집기는 CSS 편집기의 모든 쿨 기능과 함께 제공 되며 @import 체인의 모든 LESS 문서에서 변수 및 mixin에 대 한 특정 Intellisense가 있습니다.

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a>Visual Studio에서 Web Apps 지원 Azure App Service

Azure SDK for .NET 2.2을 사용 하 Visual Studio 2013에서는 **서버 탐색기** 를 사용 하 여 원격 웹 앱과 직접 상호 작용할 수 있습니다. Azure 계정에 로그인 하 고, 새 웹 앱을 만들고, 앱을 구성 하 고, 실시간 로그를 볼 수 있습니다. SDK 2.2이 출시 된 후 곧 Azure에서 원격으로 디버그 모드에서 실행할 수 있습니다. Azure App Service Web Apps의 새로운 기능은 대부분 Azure SDK for .NET의 현재 릴리스를 설치할 때 Visual Studio 2012 에서도 작동 합니다.

자세한 내용은 다음 리소스를 참조하세요.

- [Azure App Service에서 ASP.NET 웹 앱 만들기](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [Visual Studio를 사용하여 Azure App Service의 웹앱 문제 해결](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a>웹 게시 향상

Visual Studio 2013에는 새롭고 향상 된 웹 게시 기능이 포함 되어 있습니다. 다음은 몇 가지 옵션입니다.

- [Web.config 파일 암호화](https://go.microsoft.com/fwlink/?LinkId=325529)를 쉽게 자동화 합니다. (이 링크와 다음 두 가지는 MSDN에 대 한 설명서를 참조 하 여 10/17 년에 출시 될 때까지 사용 하지 못할 수 있음)
- [배포 하는 동안 응용 프로그램을 오프 라인 상태로 만들기](https://go.microsoft.com/fwlink/?LinkId=325530)를 쉽게 자동화 합니다.
- 서버에 복사할 파일을 결정 하기 위해 [마지막으로 변경 된 날짜 대신 파일 체크섬을 사용](https://go.microsoft.com/fwlink/?LinkId=325531) 하도록 웹 배포를 구성 합니다.
- FTP 또는 파일 시스템 게시 방법과 웹 배포를 사용 하는 경우 선택한 개별 파일 (web.config 포함)을 신속 하 게 게시 합니다.

ASP.NET 웹 배포에 대 한 자세한 내용은 [ASP.NET 사이트](https://go.microsoft.com/fwlink/?LinkId=322027)를 참조 하세요.

<a id="nuget"></a>
## <a name="nuget-27"></a>NuGet 2.7

NuGet 2.7에는 [nuget 2.7 릴리스 정보](http://docs.nuget.org/docs/release-notes/nuget-2.7)에 자세히 설명 되어 있는 다양 한 새 기능 집합이 포함 되어 있습니다.

또한이 버전의 NuGet은 패키지를 다운로드 하기 위해 NuGet의 패키지 복원 기능에 대 한 명시적 동의를 제공 하지 않아도 됩니다. 이제 NuGet을 설치 하 여 승인 (및 NuGet의 기본 설정 대화 상자에서 관련 된 확인란)이 허용 됩니다. 이제 패키지 복원은 기본적으로 작동 합니다.

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a>ASP.NET 웹 양식

### <a name="one-aspnet"></a>ASP.NET 1 개

Web Forms 프로젝트 템플릿은 새로운 하나의 ASP.NET 환경과 원활 하 게 통합 됩니다. Web Forms 프로젝트에 MVC 및 Web API 지원을 추가할 수 있으며, 하나의 ASP.NET 프로젝트 만들기 마법사를 사용 하 여 인증을 구성할 수 있습니다. 자세한 내용은 [Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기](creating-web-projects-in-visual-studio.md)를 참조 하세요.

### <a name="aspnet-identity"></a>ASP.NET ID

Web Forms 프로젝트 템플릿은 새로운 ASP.NET Identity 프레임 워크를 지원 합니다. 또한 템플릿은 이제 Web Forms 인트라넷 프로젝트 만들기를 지원 합니다. 자세한 내용은 **Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기**의 [인증 방법](creating-web-projects-in-visual-studio.md#auth) 을 참조 하세요.

### <a name="bootstrap"></a>부트스트랩

Web Forms 템플릿은 [부트스트랩](http://twitter.github.io/bootstrap/) 을 사용 하 여 간단 하 고 응답성이 뛰어난 모양과 느낌을 제공 하 여 손쉽게 사용자 지정할 수 있습니다. 자세한 내용은 [Visual Studio 2013 웹 프로젝트 템플릿에서 부트스트랩](creating-web-projects-in-visual-studio.md#bootstrap)을 참조 하세요.

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a>ASP.NET MVC 5

### <a name="one-aspnet"></a>ASP.NET 1 개

웹 MVC 프로젝트 템플릿은 새로운 하나의 ASP.NET 환경과 원활 하 게 통합 됩니다. ASP.NET 프로젝트 만들기 마법사 하나를 사용 하 여 MVC 프로젝트를 사용자 지정 하 고 인증을 구성할 수 있습니다. ASP.NET MVC 5에 대 한 소개 자습서는 [ASP.NET mvc 5 시작](../../../mvc/overview/getting-started/introduction/getting-started.md)에서 찾을 수 있습니다.

MVC 4 프로젝트를 MVC 5로 업그레이드 하는 방법에 대 한 자세한 내용은 [ASP.NET mvc 4 및 WEB Api 프로젝트를 ASP.NET mvc 5 및 WEB api 2로 업그레이드 하는 방법](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)을 참조 하세요.

### <a name="aspnet-identity"></a>ASP.NET ID

MVC 프로젝트 템플릿은 인증 및 id 관리를 위해 ASP.NET Identity를 사용 하도록 업데이트 되었습니다. Facebook 및 Google 인증 및 새 멤버 자격 API를 사용 하는 자습서는 [facebook 및 Google OAuth2 및 Openid connect sign-on을 사용 하 여 ASP.NET mvc 5 앱 만들기](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 및 [인증 및 SQL DB를 사용 하 여 ASP.NET MVC 앱 만들기 및 Azure App Service에 배포](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)에서 찾을 수 있습니다.

### <a name="bootstrap"></a>부트스트랩

MVC 프로젝트 템플릿은 손쉽게 사용자 지정할 수 있는 슬림 하 고 응답성이 뛰어난 모양과 느낌을 제공 하기 위해 [부트스트랩](http://getbootstrap.com/) 을 사용 하도록 업데이트 되었습니다. 자세한 내용은 [Visual Studio 2013 웹 프로젝트 템플릿에서 부트스트랩](creating-web-projects-in-visual-studio.md#bootstrap)을 참조 하세요.

### <a name="authentication-filters"></a>인증 필터

인증 필터는 ASP.NET MVC 파이프라인에서 권한 부여 필터 전에 실행 되는 ASP.NET MVC의 새로운 종류의 필터 이며, 작업별, 컨트롤러당 또는 모든 컨트롤러에 대해 전역적으로 인증 논리를 지정할 수 있도록 합니다. 인증 필터는 요청에서 자격 증명을 처리 하 고 해당 보안 주체를 제공 합니다. 인증 필터는 권한이 없는 요청에 대 한 응답으로 인증 문제를 추가할 수도 있습니다.

### <a name="filter-overrides"></a>필터 재정의

이제 재정의 필터를 지정 하 여 지정 된 작업 메서드 또는 컨트롤러에 적용 되는 필터를 재정의할 수 있습니다. 재정의 필터는 지정 된 범위 (동작 또는 컨트롤러)에 대해 실행 하면 안 되는 필터 유형 집합을 지정 합니다. 이를 통해 전역적으로 적용 되는 필터를 구성한 다음 특정 작업 또는 컨트롤러에 적용 되는 특정 전역 필터를 제외할 수 있습니다.

### <a name="attribute-routing"></a>특성 라우팅

ASP.NET MVC는 이제 [http://attributerouting.net](http://attributerouting.net)작성자 인 Tim mccall의 기여로 인해 특성 라우팅을 지원 합니다. 특성 라우팅을 사용 하 여 작업 및 컨트롤러에 주석을 추가 하 여 경로를 지정할 수 있습니다.

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a>ASP.NET Web API 2

### <a name="attribute-routing"></a>특성 라우팅

이제 ASP.NET Web API은 [http://attributerouting.net](http://attributerouting.net)의 작성자 인 Tim mccall의 기여로 인해 특성 라우팅을 지원 합니다. 특성 라우팅을 사용 하 여 다음과 같이 작업 및 컨트롤러에 주석을 추가 하 여 Web API 경로를 지정할 수 있습니다.

[!code-csharp[Main](release-notes/samples/sample1.cs)]

특성 라우팅은 웹 API에서 Uri를 보다 강력 하 게 제어할 수 있도록 합니다. 예를 들어 단일 API 컨트롤러를 사용 하 여 리소스 계층을 쉽게 정의할 수 있습니다.

[!code-csharp[Main](release-notes/samples/sample2.cs)]

또한 특성 라우팅은 선택적 매개 변수, 기본값 및 경로 제약 조건을 지정 하는 편리한 구문을 제공 합니다.

[!code-csharp[Main](release-notes/samples/sample3.cs)]

특성 라우팅에 대 한 자세한 내용은 [WEB API 2에서 특성 라우팅](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md)을 참조 하세요.

### <a name="oauth-20"></a>OAuth 2.0

이제 Web API 및 단일 페이지 응용 프로그램 프로젝트 템플릿에서 OAuth 2.0을 사용한 권한 부여를 지원 합니다. OAuth 2.0은 보호 된 리소스에 대 한 클라이언트 액세스 권한을 부여 하기 위한 프레임 워크입니다. 브라우저 및 모바일 장치를 비롯 한 다양 한 클라이언트에서 작동 합니다.

OAuth 2.0에 대 한 지원은 전달자 인증 및 권한 부여 서버 역할 구현에 Microsoft OWIN 구성 요소에서 제공 하는 새로운 보안 미들웨어를 기반으로 합니다. 또는 Windows Server 2012 r 2에서 Azure Active Directory 또는 ADFS와 같은 조직 권한 부여 서버를 사용 하 여 클라이언트에 권한을 부여할 수 있습니다.

### <a name="odata-improvements"></a>OData 개선 사항

**$Select, $expand, $batch 및 $value에 대 한 지원**

ASP.NET Web API OData는 이제 $select, $expand 및 $value에 대 한 완전 한 지원을 제공 합니다. 또한 요청 일괄 처리 및 변경 집합 처리에 $batch를 사용할 수 있습니다.

$Select 및 $expand 옵션을 사용 하 여 OData 끝점에서 반환 되는 데이터의 모양을 변경할 수 있습니다. 자세한 내용은 [WEB API OData에서 $Select 소개 및 $expand 지원](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md)을 참조 하세요.

**향상 된 확장성**

이제 OData 포맷터를 확장할 수 있습니다. Atom 항목 메타 데이터를 추가 하 고 명명 된 스트림 및 미디어 링크 항목을 지원 하 고 인스턴스 주석을 추가 하 고 링크가 생성 되는 방법을 사용자 지정할 수 있습니다.

**지원 되지 않는 형식 지원**

이제 엔터티 형식에 대 한 CLR 형식을 정의할 필요 없이 OData 서비스를 빌드할 수 있습니다. 대신 OData 컨트롤러는 OData 포맷터 직렬화/deserialize 인 **IEdmObject**인스턴스를 사용 하거나 반환할 수 있습니다.

**기존 모델 다시 사용**

기존 EDM (엔터티 데이터 모델)이 이미 있는 경우 새 EDM (엔터티 데이터 모델)을 빌드하는 대신 직접 다시 사용할 수 있습니다. 예를 들어 Entity Framework를 사용 하는 경우 EF에서 작성 하는 EDM을 사용할 수 있습니다.

### <a name="request-batching"></a>일괄 처리 요청

요청 일괄 처리는 여러 작업을 단일 HTTP POST 요청으로 결합 하 여 네트워크 트래픽을 줄이고 더 부드럽고 번잡 사용자 인터페이스를 제공 합니다. ASP.NET Web API는 이제 요청 일괄 처리에 대 한 몇 가지 전략을 지원 합니다.

- OData 서비스의 $batch 끝점을 사용 합니다.
- 단일 MIME 다중 파트 요청에 여러 요청을 패키지 합니다.
- 사용자 지정 일괄 처리 형식을 사용 합니다.

요청 일괄 처리를 사용 하도록 설정 하려면 일괄 처리 처리기가 있는 경로를 웹 API 구성에 추가 하기만 하면 됩니다.

[!code-csharp[Main](release-notes/samples/sample4.cs)]

요청을 또는 순서에 관계 없이 실행할지 또는 실행할지를 제어할 수도 있습니다.

### <a name="portable-aspnet-web-api-client"></a>이식 가능한 ASP.NET Web API 클라이언트

이제 ASP.NET Web API 클라이언트를 사용 하 여 Windows 스토어 및 Windows Phone 8 응용 프로그램에서 작동 하는 이식 가능한 클래스 라이브러리를 만들 수 있습니다. 또한 클라이언트와 서버에서 공유할 수 있는 이식 가능한 포맷터를 만들 수 있습니다.

### <a name="improved-testability"></a>향상 된 테스트 용이성

Web API 2를 사용 하면 API 컨트롤러를 더 쉽게 단위 테스트할 수 있습니다. 요청 메시지 및 구성을 사용 하 여 API 컨트롤러를 인스턴스화한 다음 테스트할 동작 메서드를 호출 하면 됩니다. 링크 생성을 수행 하는 작업 메서드에 대해서는 **Urlhelper** 클래스를 쉽게 모의으로 만들 수 있습니다.

### <a name="ihttpactionresult"></a>IHttpActionResult

이제 IHttpActionResult을 구현 하 여 Web API 작업 메서드의 결과를 캡슐화 할 수 있습니다. 웹 API 동작 메서드에서 반환 되는 IHttpActionResult는 ASP.NET Web API 런타임에 의해 실행 되어 결과 응답 메시지를 생성 합니다. Web api 작업에서 IHttpActionResult를 반환 하 여 Web API 구현에 대 한 단위 테스트를 간소화할 수 있습니다. 편의를 위해 특정 상태 코드, 서식이 지정 된 콘텐츠 또는 콘텐츠 협상 된 응답을 반환 하는 결과를 포함 하 여 다양 한 IHttpActionResult 구현이 기본적으로 제공 됩니다.

### <a name="httprequestcontext"></a>HttpRequestContext

새 **Httprequestcontext** 는 요청에 연결 되었지만 요청에서 즉시 사용할 수 없는 상태를 추적 합니다. 예를 들어 **Httprequestcontext** 를 사용 하 여 경로 데이터, 요청에 연결 된 보안 주체, 클라이언트 인증서, **urlhelper** 및 가상 경로 루트를 가져올 수 있습니다. 단위 테스트를 위해 **Httprequestcontext** 를 쉽게 만들 수 있습니다.

요청에 대 한 보안 주체는 **system.threading.thread.currentprincipal**을 사용 하는 대신 요청으로 전달 되기 때문에 이제 웹 API 파이프라인에 있는 동안 요청 수명 내내 보안 주체를 사용할 수 있습니다.

### <a name="cors"></a>CORS

Brock Allen에서 좋은 다른 기여 덕분에 이제 ASP.NET는 CORS (원본 간 요청 공유)를 완벽 하 게 지원 합니다.

브라우저 보안은 웹 페이지에서 다른 도메인으로 AJAX 요청을 수행하지 못하도록 방지합니다. [CORS](http://www.w3.org/TR/cors/) 는 서버에서 동일한 원본 정책을 완화할 수 있게 해 주는 W3C 표준입니다. CORS를 사용하면 서버에서 명시적으로 일부 원본 간 요청을 허용하는 한편 다른 요청은 거부할 수 있습니다.

이제 Web API 2는 실행 전 요청의 자동 처리를 비롯 한 CORS를 지원 합니다. 자세한 내용은 [ASP.NET 웹 API에서 크로스-원본 리소스 요청 사용](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md)을 참조하세요.

### <a name="authentication-filters"></a>인증 필터

인증 필터는 ASP.NET Web API 파이프라인의 권한 부여 필터 전에 실행 되는 ASP.NET Web API의 새로운 종류의 필터 이며, 모든 컨트롤러에 대해 작업당, 컨트롤러당 또는 전역 인증 논리를 지정할 수 있도록 합니다. 인증 필터는 요청에서 자격 증명을 처리 하 고 해당 보안 주체를 제공 합니다. 인증 필터는 권한이 없는 요청에 대 한 응답으로 인증 문제를 추가할 수도 있습니다.

### <a name="filter-overrides"></a>필터 재정의

이제 재정의 필터를 지정 하 여 지정 된 작업 메서드 또는 컨트롤러에 적용 되는 필터를 재정의할 수 있습니다. 재정의 필터는 지정 된 범위 (동작 또는 컨트롤러)에 대해 실행 하면 안 되는 필터 유형 집합을 지정 합니다. 이렇게 하면 전역 필터를 추가할 수 있지만 특정 작업 또는 컨트롤러에서 제외할 수 있습니다.

### <a name="owin-integration"></a>OWIN 통합

ASP.NET Web API은 이제 OWIN을 완벽 하 게 지원 하며 모든 OWIN 지원 호스트에서 실행할 수 있습니다. OWIN 인증 시스템과의 통합을 제공 하는 **Hostauthenticationfilter** 도 포함 되어 있습니다.

OWIN 통합을 사용 하면 SignalR와 같은 다른 OWIN 미들웨어와 함께 자체 프로세스에서 Web API를 자체 호스트할 수 있습니다. 자세한 내용은 [OWIN를 사용 하 여 자체 호스트 ASP.NET Web API를](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)참조 하세요.

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a>ASP.NET SignalR 2.0

다음 섹션에서는 SignalR 2.0의 기능에 대해 설명 합니다.

- [OWIN 기반](#builtonowin)
- [이제 MapHubs 및 Maphubs이 MapSignalR](#MapSignalR)
- [도메인 간 지원](#crossdomain)
- [Monotouch.dialog 및 MonoDroid을 통한 iOS 및 Android 지원](#mobile)
- [이식 가능한 .NET 클라이언트](#portable)
- [새 자체 호스트 패키지](#selfhost)
- [이전 버전과 호환 되는 서버 지원](#backwardcompat)
- [.NET 4.0에 대 한 서버 지원이 제거 되었습니다.](#remove40)
- [클라이언트 및 그룹 목록에 메시지 보내기](#messagelist)
- [특정 사용자에 게 메시지 보내기](#sendtouser)
- [오류 처리 지원 향상](#errorhandling)
- [허브의 손쉬운 유닛 테스트](#unittesting)
- [JavaScript 오류 처리](#javascripterror)

기존 1.x 프로젝트를 SignalR 2.0로 업그레이드 하는 방법에 대 한 예제는 SignalR 1.x [프로젝트 업그레이드](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md)를 참조 하세요.

<a id="builtonowin"></a>
### <a name="built-on-owin"></a>OWIN 기반

SignalR 2.0는 완전히 [OWIN (.net 용 개방형 웹 인터페이스)](http://owin.org/)에서 빌드됩니다. 이러한 변경으로 인해 SignalR는 웹 호스팅 및 자체 호스팅 SignalR 응용 프로그램 간에 훨씬 더 일관 되 게 설치할 수 있지만 많은 API 변경도 필요 합니다.

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a>이제 MapHubs 및 Maphubs이 MapSignalR

OWIN 표준과의 호환성을 위해 이러한 메서드의 이름이 `MapSignalR`로 바뀌었습니다. 매개 변수 없이 호출 되는 `MapSignalR` 모든 허브를 매핑합니다 (`MapHubs` 버전 1.x에서). 개별 **PersistentConnection** 개체를 매핑하려면 연결 유형을 형식 매개 변수로 지정 하 고 연결에 대 한 URL 확장을 첫 번째 인수로 지정 합니다.

`MapSignalR` 메서드는 Owin startup 클래스에서 호출 됩니다. Visual Studio 2013 Owin startup 클래스에 대 한 새 템플릿이 포함 되어 있습니다. 이 템플릿을 사용 하려면 다음을 수행 합니다.

1. 프로젝트를 마우스 오른쪽 단추로 클릭 합니다.
2. **추가**, **새 항목** ...을 선택 합니다.
3. **Owin 시작 클래스**를 선택 합니다. 새 클래스의 이름을 **Startup.cs**로 합니다.

**웹 응용 프로그램** 에서 `MapSignalR` 메서드를 포함 하는 Owin startup 클래스는 아래와 같이 web.config 파일의 응용 프로그램 설정 노드의 항목을 사용 하 여 Owin의 시작 프로세스에 추가 됩니다.

**자체 호스팅 응용 프로그램**에서 Startup 클래스는 `WebApp.Start` 메서드의 형식 매개 변수로 전달 됩니다.

**SignalR 1.x (웹 응용 프로그램의 전역 응용 프로그램 파일)에서 허브 및 연결 매핑:** 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

**SignalR 2.0 (Owin 시작 클래스 파일에서)의 허브 및 연결 매핑:** 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

**자체 호스팅 응용 프로그램**에서 Startup 클래스는 아래와 같이 `WebApp.Start` 메서드에 대 한 형식 매개 변수로 전달 됩니다.

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a>도메인 간 지원

SignalR 1.x에서 도메인 간 요청은 단일 EnableCrossDomain 플래그에 의해 제어 됩니다. 이 플래그는 JSONP 및 CORS 요청을 모두 제어 합니다. 유연성을 높이기 위해 SignalR의 서버 구성 요소에서 모든 CORS 지원이 제거 되었습니다. JavaScript 클라이언트는 여전히 CORS를 사용 하 여 브라우저에서 지 원하는 경우에는 CORS를 정상적으로 사용 하 고, 이러한 시나리오를 지원 하기 위해 새로운 OWIN 미들웨어를 사용할 수 있게 되었습니다.

SignalR 2.0에서 클라이언트에 JSONP가 필요한 경우 (이전 브라우저에서 도메인 간 요청을 지원 하려면 아래와 같이 `HubConfiguration` `true`개체에 대 한 `EnableJSONP`를 설정 하 여 명시적으로 사용 하도록 설정 해야 합니다. JSONP는 CORS 보다 안전 하지 않으므로 기본적으로 사용 하지 않도록 설정 되어 있습니다.

SignalR 2.0에 새 CORS 미들웨어를 추가 하려면 프로젝트에 `Microsoft.Owin.Cors` 라이브러리를 추가 하 고 아래 섹션과 같이 SignalR 미들웨어 앞에 `UseCors`를 호출 합니다.

**Owin을 프로젝트에 추가**:이 라이브러리를 설치 하려면 패키지 관리자 콘솔에서 다음 명령을 실행 합니다.

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

이 명령은 2.0.0 버전의 패키지를 프로젝트에 추가 합니다.

**UseCors 호출**

다음 코드 조각에서는 SignalR 1.x 및 2.0에서 도메인 간 연결을 구현 하는 방법을 보여 줍니다.

**SignalR 1.x (전역 응용 프로그램 파일)에서 도메인 간 요청 구현**

[!code-csharp[Main](release-notes/samples/sample9.cs)]

**SignalR 2.0에서 도메인 간 요청 구현 ( C# 코드 파일에서)**

다음 코드에서는 SignalR 2.0 프로젝트에서 CORS 또는 JSONP를 사용 하도록 설정 하는 방법을 보여 줍니다. 이 코드 샘플은 `MapSignalR`대신 `Map` 및 `RunSignalR`를 사용 하므로 CORS 미들웨어는 `MapSignalR`에 지정 된 경로의 모든 트래픽이 아닌 CORS를 지원 해야 하는 SignalR 요청에 대해서만 실행 됩니다. `Map`는 전체 응용 프로그램이 아닌 특정 URL 접두사에 대해 실행 해야 하는 다른 미들웨어에도 사용할 수 있습니다.

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a>Monotouch.dialog 및 MonoDroid을 통한 iOS 및 Android 지원

[Xamarin 라이브러리](https://xamarin.com/)에서 Monotouch.dialog 및 MonoDroid 구성 요소를 사용 하 여 IOS 및 Android 클라이언트에 대 한 지원이 추가 되었습니다. 사용 방법에 대 한 자세한 내용은 [Xamarin 구성 요소 사용](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln)을 참조 하세요. 이러한 구성 요소는 SignalR RTW 릴리스를 사용할 수 있을 때 [Xamarin 스토어](https://store.xamarin.com/) 에서 사용할 수 있습니다.

<a id="portable"></a># # # 이식 가능한 .NET 클라이언트

플랫폼 간 개발을 보다 효율적으로 수행할 수 있도록 Silverlight, WinRT 및 Windows Phone 클라이언트는 다음 플랫폼을 지 원하는 단일 휴대용 .NET 클라이언트로 대체 되었습니다.

- NET 4.5
- Silverlight 5
- WinRT (Windows 스토어 앱 용 .NET)
- Windows Phone 8

<a id="selfhost"></a>

### <a name="new-self-host-package"></a>새 자체 호스트 패키지

이제 NuGet 패키지를 사용 하면 웹 서버에서 호스트 되는 것이 아니라 프로세스 또는 다른 응용 프로그램에서 호스트 되는 SignalR 응용 프로그램을 SignalR 하 여 쉽게 시작할 수 있습니다. SignalR 1.x를 사용 하 여 빌드된 자체 호스트 프로젝트를 업그레이드 하려면 SignalR 패키지를 제거 하 고 SignalR 패키지를 추가 합니다. 자체 호스트 패키지를 시작 하는 방법에 대 한 자세한 내용은 [자습서: SignalR](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)를 참조 하세요.

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a>이전 버전과 호환 되는 서버 지원

이전 버전의 SignalR에서는 클라이언트와 서버에서 사용 되는 SignalR 패키지의 버전이 동일 해야 합니다. 업데이트 하기 어려운 굵고 클라이언트 응용 프로그램을 지원 하기 위해 SignalR 2.0는 이제 이전 클라이언트에서 최신 서버 버전을 사용할 수 있도록 지원 합니다. **참고: SignalR 2.0는 최신 클라이언트를 사용 하 여 이전 버전으로 빌드된 서버를 지원 하지 않습니다.**

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a>.NET 4.0에 대 한 서버 지원이 제거 되었습니다.

SignalR 2.0은 .NET 4.0과의 서버 상호 운용성에 대 한 지원을 삭제 했습니다. .NET 4.5은 SignalR 2.0 서버와 함께 사용 해야 합니다. SignalR 2.0 용 .NET 4.0 클라이언트가 여전히 있습니다.

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a>클라이언트 및 그룹 목록에 메시지 보내기

SignalR 2.0에서는 클라이언트 및 그룹 Id 목록을 사용 하 여 메시지를 보낼 수 있습니다. 다음 코드 조각에서는이 작업을 수행 하는 방법을 보여 줍니다.

**PersistentConnection를 사용 하 여 클라이언트 및 그룹의 목록에 메시지 보내기**

[!code-csharp[Main](release-notes/samples/sample11.cs)]

**허브를 사용 하 여 클라이언트 및 그룹 목록에 메시지 보내기**

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a>특정 사용자에 게 메시지 보내기

이 기능을 사용 하면 사용자가 새 인터페이스 IUserIdProvider를 통해 IRequest를 기반으로 하는 사용자 Id를 지정할 수 있습니다.

**IUserIdProvider 인터페이스**

[!code-csharp[Main](release-notes/samples/sample13.cs)]

기본적으로 사용자의 IPrincipal.Identity.Name를 사용자 이름으로 사용 하는 구현이 있습니다.

허브에서는 새 API를 통해 이러한 사용자에 게 메시지를 보낼 수 있습니다.

**클라이언트 사용자 API 사용**

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a>오류 처리 지원 향상

이제 사용자가 모든 허브 호출에서 **HubException** 을 throw 할 수 있습니다. **HubException** 의 생성자는 문자열 메시지와 개체 추가 오류 데이터를 사용할 수 있습니다. SignalR는 예외를 자동으로 직렬화 하 고 허브 메서드 호출을 거부/실패 하는 데 사용 되는 클라이언트에 게 보냅니다.

**자세한 허브 예외 표시** 설정은 클라이언트로 다시 전송 되는 **HubException** 에는 영향을 미치지 않습니다. 항상 전송 됩니다.

**클라이언트에 HubException를 보내는 방법을 보여 주는 서버 쪽 코드**

[!code-csharp[Main](release-notes/samples/sample15.cs)]

**서버에서 보낸 HubException 응답을 보여 주는 JavaScript 클라이언트 코드**

[!code-html[Main](release-notes/samples/sample16.html)]

**서버에서 보낸 HubException 응답을 보여 주는 .NET 클라이언트 코드**

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a>허브의 손쉬운 유닛 테스트

SignalR 2.0에는 모의 클라이언트 쪽 호출을 보다 쉽게 만들 수 있도록 하는 허브에 `IHubCallerConnectionContext` 라는 인터페이스가 포함 되어 있습니다. 다음 코드 조각은 인기 있는 테스트 장비 [xUnit.net](https://github.com/xunit/xunit) 및 [moq](https://code.google.com/p/moq/)로이 인터페이스를 사용 하는 방법을 보여 줍니다.

**XUnit.net를 사용 하 여 SignalR 유닛 테스트**

[!code-csharp[Main](release-notes/samples/sample18.cs)]

**Moq로 SignalR 유닛 테스트**

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a>JavaScript 오류 처리

SignalR 2.0에서 모든 JavaScript 오류 처리 콜백은 원시 문자열 대신 JavaScript 오류 개체를 반환 합니다. 이렇게 하면 SignalR에서 오류 처리기에 대 한 다양 한 정보를 전달할 수 있습니다. 오류의 `source` 속성에서 내부 예외를 가져올 수 있습니다.

**Start. Fail 예외를 처리 하는 JavaScript 클라이언트 코드**

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a>ASP.NET ID

### <a name="new-aspnet-membership-system"></a>새 ASP.NET 멤버 자격 시스템

ASP.NET Identity ASP.NET 응용 프로그램에 대 한 새 멤버 자격 시스템입니다. ASP.NET Identity를 사용 하면 사용자 관련 프로필 데이터를 응용 프로그램 데이터와 쉽게 통합할 수 있습니다. ASP.NET Identity를 사용 하 여 응용 프로그램의 사용자 프로필에 대 한 지 속성 모델을 선택할 수도 있습니다. Azure Storage 테이블과 같은 NoSQL 데이터 저장소를 포함 하 여 SQL Server 데이터베이스 또는 다른 데이터 저장소에 데이터를 저장할 수 있습니다. 자세한 내용은 **Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기**의 [개별 사용자 계정](creating-web-projects-in-visual-studio.md#indauth) 을 참조 하세요.

### <a name="claims-based-authentication"></a>클레임 기반 인증

이제 ASP.NET는 클레임 기반 인증을 지원 합니다. 여기서 사용자의 id는 신뢰할 수 있는 발급자의 클레임 집합으로 표시 됩니다. 사용자는 응용 프로그램 데이터베이스에서 유지 관리 되는 사용자 이름 및 암호를 사용 하거나, 소셜 id 공급자 (예: Microsoft 계정, Facebook, Google, Twitter)를 사용 하거나, Azure Active Directory 또는을 통해 조직 계정을 사용 하 여 인증할 수 있습니다. Active Directory Federation Services (ADFS).

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a>Azure Active Directory 및 Windows Server Active Directory와 통합

이제 인증을 위해 Azure Active Directory 또는 Windows Server Active Directory (AD)를 사용 하는 ASP.NET 프로젝트를 만들 수 있습니다. 자세한 내용은 **Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기**의 [조직 계정](creating-web-projects-in-visual-studio.md#orgauth) 을 참조 하세요.

### <a name="owin-integration"></a>OWIN 통합

ASP.NET 인증은 이제 모든 OWIN 기반 호스트에서 사용할 수 있는 OWIN 미들웨어를 기반으로 합니다. OWIN에 대 한 자세한 내용은 다음 [MICROSOFT OWIN 구성 요소](#TOC7) 섹션을 참조 하세요.

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a>Microsoft OWIN 구성 요소

OWIN ( [Open Web Interface for .net](http://owin.org/) )는 .net 웹 서버와 웹 응용 프로그램 간의 추상화를 정의 합니다. OWIN는 서버에서 웹 응용 프로그램을 분리 하 여 웹 응용 프로그램을 호스트 독립적으로 만듭니다. 예를 들어 IIS에서 OWIN 기반 웹 응용 프로그램을 호스트 하거나 사용자 지정 프로세스에서 자체 호스트할 수 있습니다.

Microsoft OWIN 구성 요소 (Katana 프로젝트 라고도 함)에 도입 된 변경 내용에는 새로운 서버 및 호스트 구성 요소, 새 도우미 라이브러리 및 미들웨어, 새 인증 미들웨어가 포함 됩니다.

OWIN 및 Katana에 대 한 자세한 내용은 [OWIN 및 Katana의 새로운 기능](../../../aspnet/overview/owin-and-katana/index.md)을 참조 하세요.

**참고: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) 응용 프로그램은 IIS 클래식 모드에서 실행할 수 없습니다. 통합 모드로 실행 해야 합니다.**

**참고: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) 응용 프로그램은 완전 신뢰로 실행 해야 합니다.**

### <a name="new-servers-and-hosts"></a>새 서버 및 호스트

이 릴리스에서는 자체 호스트 시나리오를 사용할 수 있도록 새로운 구성 요소가 추가 되었습니다. 이러한 구성 요소에는 다음과 같은 NuGet 패키지가 포함 됩니다.

- **Owin. HttpListener**. **HttpListener** 를 사용 하 여 HTTP 요청을 수신 하 고이를 OWIN 파이프라인으로 전달 하는 OWIN 서버를 제공 합니다.
- **Owin** 는 콘솔 응용 프로그램 또는 Windows 서비스와 같은 사용자 지정 프로세스에서 Owin 파이프라인을 자체 호스트 하려는 개발자를 위한 라이브러리를 제공 합니다.
- **Owinhost**. `Microsoft.Owin.Hosting`를 래핑하는 독립 실행형 실행 파일을 제공 하며, 사용자 지정 호스트 응용 프로그램을 작성 하지 않고도 OWIN 파이프라인을 직접 호스팅할 수 있도록 합니다.

또한 `Microsoft.Owin.Host.SystemWeb` 패키지를 사용 하면 미들웨어가 **Systemweb** 서버에 힌트를 제공 하 여 특정 ASP.NET 파이프라인 단계에서 미들웨어를 호출 해야 함을 나타낼 수 있습니다. 이 기능은 ASP.NET 파이프라인의 초기에 실행 해야 하는 인증 미들웨어에 특히 유용 합니다.

### <a name="helper-libraries-and-middleware"></a>도우미 라이브러리 및 미들웨어

OWIN 사양의 함수 및 유형 정의만 사용 하 여 OWIN 구성 요소를 작성할 수 있지만, 새 `Microsoft.Owin` 패키지는 보다 사용자에 게 친숙 한 추상화 집합을 제공 합니다. 이 패키지는 여러 이전 패키지 (예: `Owin.Extensions`, `Owin.Types`)를 잘 구성 된 단일 개체 모델로 결합 하 여 다른 OWIN 구성 요소에서 쉽게 사용할 수 있게 합니다. 실제로 대부분의 Microsoft OWIN 구성 요소는이 패키지를 사용 합니다.

> [!NOTE]
> [OWIN](http://www.owin.org) 응용 프로그램은 IIS 클래식 모드에서 실행할 수 없습니다. 통합 모드로 실행 해야 합니다.

> [!NOTE]
> [OWIN](http://www.owin.org) 응용 프로그램은 완전 신뢰로 실행 해야 합니다.

이 릴리스에는 실행 중인 OWIN 응용 프로그램의 유효성을 검사 하는 미들웨어와 오류를 조사 하는 데 도움이 되는 오류 페이지 미들웨어를 포함 하는 Owin 패키지도 포함 되어 있습니다.

### <a name="authentication-components"></a>인증 구성 요소

다음 인증 구성 요소를 사용할 수 있습니다.

- **Owin. ActiveDirectory**. 온-프레미스 또는 클라우드 기반 디렉터리 서비스를 사용 하 여 인증을 사용 하도록 설정 합니다.
- **Owin** 쿠키를 사용 하 여 인증을 사용 하도록 설정 합니다. 이 패키지는 이전에 `Microsoft.Owin.Security.Forms`이름이 지정 되었습니다.
- **Owin** Facebook의 OAuth 기반 서비스를 사용 하 여 인증을 사용 하도록 설정 합니다.
- **Owin** Google의 openid connect 기반 서비스를 사용 하 여 인증을 사용 하도록 설정 합니다.
- **Owin** 를 사용 하면 jwt 토큰을 사용 하 여 인증할 수 있습니다.
- **Owin. MicrosoftAccount** 는 microsoft 계정을 사용 하 여 인증을 활성화 합니다.
- **Owin**입니다. 전달자 토큰을 인증 하는 데 필요한 미들웨어 뿐만 아니라 OAuth 권한 부여 서버를 제공 합니다.
- **Owin** 를 사용 하면 Twitter의 OAuth 기반 서비스를 사용 하 여 인증할 수 있습니다.

이 릴리스에는 크로스-원본 HTTP 요청을 처리 하기 위한 미들웨어를 포함 하는 `Microsoft.Owin.Cors` 패키지도 포함 되어 있습니다.

> [!NOTE]
> Visual Studio 2013의 최종 버전에서 JWT 서명 지원이 제거 되었습니다.

<a id="ef6"></a>
## <a name="entity-framework-6"></a>Entity Framework 6

Entity Framework 6의 새로운 기능 및 기타 변경 사항 목록은 [Entity Framework 버전 기록](https://msdn.com/data/jj574253)을 참조 하세요.

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a>ASP.NET Razor 3

ASP.NET Razor 3에는 다음과 같은 새로운 기능이 포함 되어 있습니다.

- 탭 편집 지원. 이전에는 **탭 유지** 옵션을 사용 하는 경우 Visual Studio에서 **문서 서식 지정** 명령, 자동 들여쓰기 및 자동 서식 지정이 제대로 작동 하지 않았습니다. 이 변경 내용은 탭 서식 지정을 위한 Razor 코드의 Visual Studio 서식 지정을 수정 합니다.
- 링크를 생성할 때 URL 다시 쓰기 규칙을 지원 합니다.
- 보안 투명 특성을 제거 합니다.
  > [!NOTE]
  > 이는 주요 변경 내용으로, razor 3은 MVC4 및 이전 버전과 호환 되지 않지만 Razor 2는 MVC5에 대해 컴파일된 MVC5 또는 어셈블리와 호환 되지 않습니다.

시험판 버전에서 Visual Studio 2013에서 해결 된 Razor 3 문제는 [여기](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0)에서 확인할 수 있습니다.

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a>ASP.NET 앱 일시 중단

ASP.NET 앱 일시 중단은 단일 컴퓨터에서 많은 수의 ASP.NET 사이트를 호스트 하기 위한 사용자 환경 및 경제 모델을 완전히 변경 하는 .NET Framework 4.5.1의 게임 변경 기능입니다. 자세한 내용은 [ASP.NET App Suspend – 응답성이 뛰어난 공유 .net 웹 호스팅](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx)을 참조 하세요.

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a>알려진 문제 및 주요 변경 내용

이 섹션에서는 Visual Studio 2013에 대 한 ASP.NET 및 Web Tools의 알려진 문제 및 주요 변경 사항을 설명 합니다.

### <a name="nuget"></a>NuGet

- [새 패키지 복원이 SLN 파일을 사용 하는 경우 Mono에서 작동 하지 않음](https://nuget.codeplex.com/workitem/3596) – 예정 된 nuget.exe 다운로드 및 [nuget 명령줄 패키지](http://www.nuget.org/packages/NuGet.CommandLine/) 업데이트에서 수정 됩니다.
- [새 패키지 복원은 Wix 프로젝트에서 작동 하지 않습니다](https://nuget.codeplex.com/workitem/3598) . 예정 된 nuget.exe 다운로드 및 [nuget 명령줄 패키지](http://www.nuget.org/packages/NuGet.CommandLine/) 업데이트에서 수정 됩니다.
- [자동 패키지 복원은 솔루션 폴더의 프로젝트에 대해 작동 하지 않습니다](https://nuget.codeplex.com/workitem/3625) . NuGet 2.8에서 수정 됩니다.

### <a name="aspnet-web-api"></a>ASP.NET Web API

1. `$select` 및 `$expand`에 대 한 지원을 추가 했으므로 `ODataQueryOptions<T>.ApplyTo(IQueryable)` `IQueryable<T>` 항상 반환 하지 않습니다.

    `ODataQueryOptions<T>`에 대 한 이전 예제는 항상 `ApplyTo`의 반환 값을 `IQueryable<T>`로 캐스트 했습니다. 앞에서 설명한 쿼리 옵션 (`$filter`, `$orderby`, `$skip`, `$top`)은 쿼리 형태를 변경 하지 않으므로 앞에서 작업 했습니다. 이제 `$select`를 지원 하 고 `ApplyTo`의 반환 값 `$expand` 항상 `IQueryable<T>` 되지 않습니다.

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    이전에 나온 샘플 코드를 사용 하는 경우 클라이언트가 `$select`를 전송 하지 않고 `$expand`경우 계속 작동 합니다. 그러나 `$select` 및 `$expand`를 지원 하려는 경우 해당 코드를로 변경 해야 합니다.

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. **요청. Url 또는 RequestContext. 일괄 처리 요청 중 Url이 null입니다.**

    일괄 처리 시나리오에서는 **요청 url** 또는 **RequestContext**에서 액세스할 때 **urlhelper** 가 null입니다.

    이 문제는 현재 Batchrequestcontext에서 추적 됩니다. [일괄 처리 요청에 대 한 Url은 null](http://aspnetwebstack.codeplex.com/workitem/1301)입니다.

    이 문제에 대 한 해결 방법은 다음 예제와 같이 **Urlhelper**의 새 인스턴스를 만드는 것입니다.

    **UrlHelper의 새 인스턴스 만들기**

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a>ASP.NET MVC

1. MVC5 및 OrgAuth를 사용 하는 경우 AntiForgerToken 유효성 검사를 수행 하는 보기가 있는 경우 뷰에 데이터를 게시할 때 다음 오류가 발생할 수 있습니다.

    **오류**:

    *'/' 응용 프로그램에서 서버 오류가 발생 했습니다.*

    <em>'<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>' 또는 '<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>' 형식의 클레임이 제공 된 ClaimsIdentity에 없습니다. 클레임 기반 인증을 사용 하 여 위조 방지 토큰 지원을 사용 하도록 설정 하려면 구성 된 클레임 공급자가 생성 하는 ClaimsIdentity 인스턴스에 대해 이러한 클레임을 모두 제공 하는지 확인 하세요. 구성 된 클레임 공급자에서 다른 클레임 유형을 고유 식별자로 사용 하는 경우에는 정적 속성인 AntiForgeryConfig를 설정 하 여 구성할 수 있습니다.</em>

    **해결 방법**:

    Global.asax에 다음 줄을 추가 하 여 문제를 해결 합니다.

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    이 문제는 다음 릴리스에 대해 수정 될 예정입니다.
2. MVC4 앱을 MVC5로 업그레이드 한 후 솔루션을 빌드하고 시작 합니다. 다음 오류가 표시 됩니다.

    은 [B] system.web. HostSection hostsection은 [B] System.web. HostSection HostSection으로 캐스트할 수 없습니다. 위치 ' C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35 \ '에 있는 ' Default ' 컨텍스트에서 ' 31bf3856ad364e35, Version = 2.0.0.0, Culture = 중립적인, PublicKeyToken = m A t i o n '을 입력 합니다. 형식 B는 ' 31bf3856ad364e35 ', ' 3.0.0.0, Version =, Culture = 중립, PublicKeyToken = '의 ' Default ' 컨텍스트 (위치 ' C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_273ce1\ ')에서 생성 됩니다.

    위의 오류를 해결 하려면 프로젝트에서 *모든* web.config 파일 (Views 폴더의 항목 포함)을 열고 다음을 수행 합니다.

   1. "4.0.0.0"의 모든 버전 ""를 "5.0.0.0"로 업데이트 합니다.
   2. "3.0.0.0"의 모든 버전 "2.0.0.0"을 업데이트 &quot;하 고, system.web. 웹 페이지&quot; 및 &quot;System.web. m i m&quot;를 ""으로 업데이트 합니다.

      예를 들어 위의 내용을 변경 하 고 나면 어셈블리 바인딩이 다음과 같이 표시 됩니다.

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      MVC 4 프로젝트를 MVC 5로 업그레이드 하는 방법에 대 한 자세한 내용은 [ASP.NET mvc 4 및 WEB Api 프로젝트를 ASP.NET mvc 5 및 WEB api 2로 업그레이드 하는 방법](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)을 참조 하세요.
3. JQuery가 맞지 않는 유효성 검사를 사용 하 여 클라이언트 쪽 유효성 검사를 사용 하는 경우 유효성 검사 메시지는 경우에 따라 형식이 ' number ' 인 HTML input 요소에 대해 올바르지 않습니다. 유효한 값이 필요한 올바른 메시지 대신 잘못 된 숫자를 입력 하는 경우에는 필요한 값에 대 한 유효성 검사 오류 ("Age 필드는 필수입니다.")가 표시 됩니다.

    이 문제는 일반적으로 Create 및 Edit 뷰에서 정수 속성이 있는 모델에 대 한 스 캐 폴드 코드에 있습니다.

    이 문제를 해결 하려면 편집기 도우미를 다음과 같이 변경 합니다.

    `@Html.EditorFor(person => person.Age)`

    아래와 같이 변경합니다.

    `@Html.TextBoxFor(person => person.Age)`
4. ASP.NET MVC 5는 더 이상 부분 신뢰를 지원 하지 않습니다. MVC 또는 WebAPI 이진 파일에 연결 하는 프로젝트는 [Securitytransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) 특성 및 [AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) 특성을 제거 해야 합니다. 이러한 특성을 제거 하면 다음과 같은 컴파일러 오류가 발생 하지 않습니다.

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > 이에 대 한 부작용으로 동일한 응용 프로그램에서 4.0 및 5.0 어셈블리를 사용할 수 없습니다. 모든 항목을 5.0로 업데이트 해야 합니다.

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a>웹 사이트가 인트라넷 영역에서 호스트 되는 동안 Facebook 권한 부여를 사용 하는 SPA 템플릿이 IE를 불안정 해질 수 있음

SPA 템플릿에서는 Facebook을 사용 하 여 외부 로그인을 제공 합니다. 템플릿을 사용 하 여 만든 프로젝트를 로컬로 실행 하는 경우 로그인 하면 IE의 작동이 중단 될 수 있습니다.

해결 방법:

1. 인터넷 영역에서 웹 사이트를 호스팅합니다. 디스크나

2. IE 이외의 브라우저에서 시나리오를 테스트 합니다.

### <a name="web-forms-scaffolding"></a>Web Forms 스캐폴딩

Web Forms 스 캐 폴딩은 VS2013에서 제거 되었으며 Visual Studio에 대 한 향후 업데이트에서 사용할 수 있습니다. 그러나 mvc 종속성을 추가 하 고 MVC에 대 한 스 캐 폴딩을 생성 하 여 Web Forms 프로젝트 내에서 스 캐 폴딩을 계속 사용할 수 있습니다. 프로젝트에 Web Forms 및 MVC의 조합이 포함 됩니다.

Web Forms 프로젝트에 MVC를 추가 하려면 새 스 캐 폴드 항목을 추가 하 고 **mvc 5 종속성**을 선택 합니다. 스크립트와 같은 모든 콘텐츠 파일이 필요한 지 여부에 따라 최소 또는 전체를 선택 합니다. 그런 다음 프로젝트에서 뷰와 컨트롤러를 만드는 MVC에 대 한 스 캐 폴드 항목을 추가 합니다.

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC 및 Web API 스 캐 폴딩-HTTP 404, 찾을 수 없음 오류

프로젝트에 스 캐 폴드 항목을 추가할 때 오류가 발생 하는 경우 프로젝트가 일관 되지 않은 상태로 남아 있을 수 있습니다. 스 캐 폴딩의 변경 내용 중 일부는 롤백되고, 설치 된 NuGet 패키지와 같은 다른 변경 내용은 롤백되지 않습니다. 라우팅 구성 변경 내용이 롤백되면 사용자는 스 캐 폴드 항목으로 이동할 때 HTTP 404 오류를 받게 됩니다.

해결 방법:

- MVC에 대 한이 오류를 해결 하려면 새 스 캐 폴드 항목을 추가 하 고 MVC 5 종속성 (최소 또는 전체)을 선택 합니다. 이 프로세스는 프로젝트에 필요한 모든 변경 내용을 추가 합니다.
- Web API에 대해이 오류를 해결 하려면:

  1. WebApiConfig 클래스를 프로젝트에 추가 합니다.

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. 다음과 같이 Global.asax의 응용 프로그램\_Start 메서드에서 WebApiConfig을 구성 합니다.

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]
