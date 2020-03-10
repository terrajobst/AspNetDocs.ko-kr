---
uid: whitepapers/mvc4-release-notes
title: ASP.NET MVC 4 | Microsoft Docs
author: rick-anderson
description: 이 문서에서는 ASP.NET MVC 4의 릴리스에 대해 설명 합니다.
ms.author: riande
ms.date: 09/09/2011
ms.assetid: f014524f-25c0-4094-b8e1-886d99536f00
msc.legacyurl: /whitepapers/mvc4-release-notes
msc.type: content
ms.openlocfilehash: b57480bd0274fbb76c600dfb0dd09037bdcbf1e7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454235"
---
# <a name="aspnet-mvc-4"></a>ASP.NET MVC 4

> 이 문서에서는 ASP.NET MVC 4의 릴리스에 대해 설명 합니다.

- [설치 참고 사항](#_Toc303253802)
- [설명서](#_Toc303253803)
- [지원](#_Toc303253804)
- [소프트웨어 요구 사항](#_Toc303253805)
- [ASP.NET MVC 4의 새로운 기능](#_Toc303253807)

    - [ASP.NET Web API](#_Toc317096197)
    - [기본 프로젝트 템플릿에 대 한 향상 된 기능](#_Toc303253808)
    - [모바일 프로젝트 템플릿](#_Toc303253809)
    - [디스플레이 모드](#_Toc303253810)
    - [jQuery Mobile, 뷰 전환기 및 브라우저 재정의](#_Toc303253811)
    - [비동기 컨트롤러에 대 한 작업 지원](#_Toc303253813)
    - [Azure SDK](#_Toc303253814)
    - [데이터베이스 마이그레이션](#_Toc303253818)
    - [빈 프로젝트 템플릿](#_Toc303253819)
    - [모든 프로젝트 폴더에 컨트롤러 추가](#_Toc303253820)
    - [묶음 및 축소](#_Toc303253821)
    - [OAuth 및 Openid connect를 사용 하 여 Facebook 및 기타 사이트에서 로그인 사용](#_Toc303253822)
- [ASP.NET MVC 3 프로젝트를 ASP.NET MVC 4로 업그레이드](#_Toc303253806)
- [ASP.NET MVC 4 릴리스 후보의 변경 내용](#_Toc303253817)
- [알려진 문제 및 주요 변경 내용](#_Toc303253815)

<a id="_Toc303253802"></a>
## <a name="installation-notes"></a>설치 참고 사항

ASP.NET MVC 4 for Visual Studio 2010는 웹 플랫폼 설치 관리자를 사용 하 여 [ASP.NET mvc 4 홈 페이지](../mvc/mvc4.md) 에서 설치할 수 있습니다.

ASP.NET MVC 4를 설치 하기 전에 ASP.NET MVC 4의 이전에 설치 된 미리 보기를 제거 하는 것이 좋습니다. 을 (를) 제거 하지 않고 ASP.NET MVC 4 베타 및 릴리스 후보를 ASP.NET MVC 4로 업그레이드할 수 있습니다.

이 릴리스는 .NET Framework 4.5의 미리 보기 릴리스와 호환 되지 않습니다. ASP.NET MVC 4를 설치 하기 전에 .NET Framework 4.5의 설치 된 미리 보기 릴리스를 최종 버전으로 개별적으로 업그레이드 해야 합니다.

ASP.NET MVC 4는 ASP.NET MVC 3과 함께 설치 하 고 실행할 수 있습니다.

<a id="_Toc303253803"></a>
## <a name="documentation"></a>문서화

ASP.NET MVC 문서는 다음 URL의 MSDN 웹사이트에서 제공됩니다.

[https://go.microsoft.com/fwlink/?LinkID=243043](https://go.microsoft.com/fwlink/?LinkID=243043)

ASP.NET MVC에 대 한 자습서 및 기타 정보는[https://www.asp.net/mvc/mvc4](../mvc/mvc4.md)(ASP.NET) 웹 사이트의 MVC 4 페이지 (영문)에서 사용할 수 있습니다.

<a id="_Toc303253804"></a>
## <a name="support"></a>지원

ASP.NET MVC 4는 완벽 하 게 지원 됩니다. 이 릴리스를 사용 하는 방법에 대 한 질문이 있는 경우 ASP.NET MVC 포럼 ([https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx))에 게시할 수 있습니다. ASP.NET 커뮤니티의 멤버가 비공식적인 지원을 제공할 수 있는 경우가 많습니다.

<a id="_Toc303253805"></a>
## <a name="software-requirements"></a>소프트웨어 요구 사항

Visual Studio 용 ASP.NET MVC 4 구성 요소에는 PowerShell 2.0 및 Visual Studio 2010 서비스 팩 1 또는 Visual Web Developer Express 2010 서비스 팩 1이 필요 합니다.

<a id="_Toc303253807"></a>
## <a name="new-features-in-aspnet-mvc-4"></a>ASP.NET MVC 4의 새로운 기능

이 섹션에서는 ASP.NET MVC 4 릴리스에 도입 된 기능을 설명 합니다.

<a id="_Toc317096197"></a>
### <a name="aspnet-web-api"></a>ASP.NET Web API

ASP.NET MVC 4에는 브라우저 및 모바일 장치를 비롯 한 광범위 한 클라이언트에 연결할 수 있는 HTTP 서비스를 만들기 위한 새로운 프레임 워크인 ASP.NET Web API 포함 되어 있습니다. 또한 ASP.NET Web API는 RESTful services를 빌드하기 위한 이상적인 플랫폼입니다.

ASP.NET Web API에는 다음 기능에 대 한 지원이 포함 됩니다.

- **최신 HTTP 프로그래밍 모델:** 강력한 형식의 새 HTTP 개체 모델을 사용 하 여 웹 Api에서 HTTP 요청 및 응답을 직접 액세스 하 고 조작 합니다. 동일한 프로그래밍 모델 및 HTTP 파이프라인은 새 *httpclient* 형식을 통해 클라이언트에서 대칭적으로 사용할 수 있습니다.
- **경로에 대 한 완전 한 지원:** ASP.NET Web API는 경로 매개 변수 및 제약 조건을 포함 하 여 ASP.NET Routing의 전체 경로 기능 집합을 지원 합니다. 또한 간단한 규칙을 사용 하 여 작업을 HTTP 메서드에 매핑합니다.
- **콘텐츠 협상:** 클라이언트와 서버는 함께 작동 하 여 web API에서 반환 되는 데이터의 올바른 형식을 결정할 수 있습니다. ASP.NET Web API는 XML, JSON 및 폼 URL로 인코딩된 형식에 대 한 기본 지원을 제공 하며 사용자 고유의 포맷터를 추가 하거나 기본 콘텐츠 협상 전략을 대체 하 여이 지원을 확장할 수 있습니다.
- **모델 바인딩 및 유효성 검사:** 모델 바인더는 HTTP 요청의 다양 한 부분에서 데이터를 추출 하 고 이러한 메시지 부분을 웹 API 작업에서 사용할 수 있는 .NET 개체로 변환 하는 쉬운 방법을 제공 합니다. 유효성 검사는 데이터 주석을 기반으로 하는 작업 매개 변수에 대해서도 수행 됩니다.
- **필터:** ASP.NET Web API는 *[권한 부여]* 특성과 같이 잘 알려진 필터를 포함 하는 필터를 지원 합니다. 작업, 권한 부여 및 예외 처리에 대 한 사용자 고유의 필터를 작성 하 고 연결할 수 있습니다.
- **쿼리 컴퍼지션:** *IQueryable* 을 반환 하는 작업에 대해 *[쿼리 가능]* 필터 특성을 사용 하 여 OData 쿼리 규칙을 통해 web API 쿼리를 지원할 수 있습니다.
- **향상 된 테스트 용이성:** 정적 컨텍스트 개체에서 HTTP 정보를 설정 하는 대신 웹 API 작업은 *HttpRequestMessage* 및 *HttpResponseMessage*의 인스턴스에서 작동 합니다. Web api 프로젝트와 함께 단위 테스트 프로젝트를 만들어 웹 API 기능에 대 한 단위 테스트 작성을 빠르게 시작할 수 있습니다.
- **코드 기반 구성:** 구성 파일이 깨끗 하 게 유지 되 고 코드를 통해서만 ASP.NET Web API 구성이 수행 됩니다. 제공 된 서비스 로케이터 패턴을 사용 하 여 확장성 점수를 구성 합니다.
- **IoC (제어의 반전) 컨테이너에 대 한 지원이 향상 되었습니다.** ASP.NET Web API는 향상 된 종속성 확인자 추상화를 통해 IoC 컨테이너에 대해 뛰어난 지원을 제공 합니다.
- **자체 호스트:** 웹 api는 전체 경로 및 Web API의 다른 기능을 계속 사용 하면서 IIS 외에도 자체 프로세스에서 호스팅될 수 있습니다.
- **사용자 지정 도움말 및 테스트 페이지 만들기:** 이제 새 *Iapiexplorer* 서비스를 사용 하 여 web api에 대 한 전체 런타임 설명을 가져오는 웹 api에 대 한 사용자 지정 도움말 및 테스트 페이지를 쉽게 빌드할 수 있습니다.
- **모니터링 및 진단:** 이제 ASP.NET Web API은 시스템 진단, ETW 및 타사 로깅 프레임 워크와 같은 기존 로깅 솔루션과 쉽게 통합 될 수 있도록 하는 경량 추적 인프라를 제공 합니다. *ITraceWriter* 구현을 제공 하 고 web API 구성에 추가 하 여 추적을 사용 하도록 설정할 수 있습니다.
- **링크 생성:** ASP.NET Web API *Urlhelper* 를 사용 하 여 동일한 응용 프로그램에서 관련 리소스에 대 한 링크를 생성할 수 있습니다.
- **웹 API 프로젝트 템플릿:** 새 MVC 4 프로젝트 마법사에서 새 Web API 프로젝트를 선택 하 여 ASP.NET Web API를 빠르게 시작 하 고 실행 합니다.
- **스 캐 폴딩:** **컨트롤러 추가** 대화 상자를 사용 하 여 Entity Framework 기반 모델 유형에 따라 웹 API 컨트롤러를 빠르게 스 캐 폴드 수 있습니다.

ASP.NET Web API에 대 한 자세한 내용은 [https://www.asp.net/web-api](../web-api/index.md)를 참조 하세요.

<a id="_Toc303253808"></a>
### <a name="enhancements-to-default-project-templates"></a>기본 프로젝트 템플릿에 대 한 향상 된 기능

새 ASP.NET MVC 4 프로젝트를 만드는 데 사용 되는 템플릿이 최신 웹 사이트를 만들기 위해 업데이트 되었습니다.

![](mvc4-release-notes/_static/image1.png)

외관 향상 외에도 새 템플릿에서 향상 된 기능이 있습니다. 템플릿에서는 적응 렌더링 이라는 기술을 사용 하 여 사용자 지정 없이 데스크톱 브라우저와 모바일 브라우저 모두에 적합 합니다.

![](mvc4-release-notes/_static/image2.png)

작동 중인 적응 렌더링을 보려면 모바일 에뮬레이터를 사용 하거나 데스크톱 브라우저 창의 크기를 작게 조정 하면 됩니다. 브라우저 창이 충분히 작으면 페이지 레이아웃이 변경 됩니다.

<a id="_Toc303253809"></a>
### <a name="mobile-project-template"></a>모바일 프로젝트 템플릿

새 프로젝트를 시작 하 고 모바일 및 태블릿 브라우저용으로 특정 사이트를 만들려는 경우 새 모바일 응용 프로그램 프로젝트 템플릿을 사용할 수 있습니다. 이는 터치 최적화 UI를 빌드하기 위한 오픈 소스 라이브러리인 jQuery Mobile을 기반으로 합니다.

![](mvc4-release-notes/_static/image3.png)

이 템플릿은 인터넷 응용 프로그램 템플릿과 동일한 응용 프로그램 구조를 포함 하 고 컨트롤러 코드는 거의 동일 하지만, jQuery Mobile을 사용 하 여 양호한 것으로 확인 하 고 터치 기반 모바일 장치에서 잘 작동 합니다. 모바일 UI를 구조화 하 고 스타일을 만드는 방법에 대 한 자세한 내용은 [JQuery mobile project 웹 사이트](http://jquerymobile.com/)를 참조 하세요.

모바일에 최적화 된 보기를 추가할 데스크톱 기반 사이트가 이미 있는 경우 또는 데스크톱 및 모바일 브라우저에 대해 다르게 스타일 지정 된 보기를 제공 하는 단일 사이트를 만들려는 경우에는 새 디스플레이 모드 기능을 사용할 수 있습니다. (다음 섹션을 참조하십시오.)

<a id="_Toc303253810"></a>
### <a name="display-modes"></a>디스플레이 모드

새 디스플레이 모드 기능을 사용 하면 응용 프로그램에서 요청을 수행 하는 브라우저에 따라 보기를 선택할 수 있습니다. 예를 들어 데스크톱 브라우저에서 홈 페이지를 요청 하는 경우 응용 프로그램은 Views\Home\Index.cshtml 템플릿을 사용할 수 있습니다. 모바일 브라우저에서 홈 페이지를 요청 하는 경우 응용 프로그램에서 Views\Home\Index.mobile.cshtml 템플릿이 반환 될 수 있습니다.

레이아웃 및 부분 특정 브라우저 유형에 대해 재정의할 수도 있습니다. 다음은 그 예입니다.

- Views\Shared 폴더에 \_\_레이아웃을 모두 포함 하는 경우에는 기본적으로 응용 프로그램에서 \_Layout을 사용 합니다. 모바일 브라우저 및 \_레이아웃에서 요청 하는 동안에는 응용 프로그램에서 Layout을 사용 합니다.
- 폴더에 \_MyPartial 및 \_MyPartial이 모두 포함 되어 있으면 명령 @Html.Partial("\_MyPartial")는 모바일 브라우저에서 요청 하는 동안 MyPartial를 렌더링 하 고 다른 요청 중에는 \_MyPartial를 렌더링 합니다.\_

다른 장치에 대 한 보기, 레이아웃 또는 부분 보기를 더 많이 만들려는 경우 새 *DefaultDisplayMode* 인스턴스를 등록 하 여 요청이 특정 조건에 부합 될 때 검색할 이름을 지정할 수 있습니다. 예를 들어, Global.asax 파일의 *응용 프로그램\_Start* 메서드에 다음 코드를 추가 하 여 Apple iPhone 브라우저가 요청할 때 적용 되는 표시 모드로 문자열 "iPhone"을 등록할 수 있습니다.

[!code-csharp[Main](mvc4-release-notes/samples/sample1.cs)]

이 코드가 실행 된 후 Apple iPhone 브라우저가 요청을 만들면 응용 프로그램은 Views\Shared\\_Layout (있는 경우)을 사용 합니다. 표시 모드에 대 한 자세한 내용은 [ASP.NET MVC 4 Mobile Features](../mvc/overview/older-versions/aspnet-mvc-4-mobile-features.md)을 참조 하세요. DisplayModeProvider를 사용 하는 응용 프로그램은 [고정 displaymode](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) NuGet 패키지를 설치 해야 합니다. [ASP.NET 낙하 2012 업데이트](https://go.microsoft.com/fwlink/?LinkID=271322) 에는 새 프로젝트 템플릿에 [고정 된 displaymodes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) NuGet 패키지가 포함 됩니다. 해결 방법에 대 한 자세한 내용은 [ASP.NET MVC 4 Mobile 캐싱 버그 Fixedd](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) 를 참조 하세요.

<a id="_Toc303253811"></a>
### <a name="jquery-mobile-and-mobile-features"></a>jQuery Mobile 및 Mobile 기능

JQuery Mobile을 사용 하 여 ASP.NET MVC 4로 모바일 응용 프로그램을 빌드하는 방법에 대 한 자세한 내용은 자습서 [ASP.NET MVC 4 모바일 기능](../mvc/overview/older-versions/aspnet-mvc-4-mobile-features.md)을 참조 하세요.

<a id="_Toc303253813"></a>
### <a name="task-support-for-asynchronous-controllers"></a>비동기 컨트롤러에 대 한 작업 지원

이제 비동기 작업 메서드를 *task* 또는 task 형식의 개체를 반환 하는 단일 메서드 *&lt;actionresult&gt;* 에 쓸 수 있습니다.

 자세한 내용은 [ASP.NET MVC 4에서 비동기 메서드 사용](../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)을 참조 하세요.

<a id="_Toc303253814"></a>
### <a name="azure-sdk"></a>Azure SDK

ASP.NET MVC 4는 1.6 이상 버전의 Windows Azure SDK를 지원 합니다.

<a id="_Toc303253818"></a>
### <a name="database-migrations"></a>데이터베이스 마이그레이션

ASP.NET MVC 4 프로젝트에는 이제 Entity Framework 5가 포함 됩니다. Entity Framework 5의 유용한 기능 중 하나는 데이터베이스 마이그레이션을 지 원하는 것입니다. 이 기능을 사용 하면 데이터베이스의 데이터를 유지 하면서 코드 중심 마이그레이션을 사용 하 여 데이터베이스 스키마를 쉽게 개선할 수 있습니다. 데이터베이스 마이그레이션에 대 한 자세한 내용은 [ASP.NET MVC 4 소개 자습서](../mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)의 [동영상 모델 및 테이블에 새 필드 추가](../mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table.md) 를 참조 하세요.

<a id="_Toc303253819"></a>
### <a name="empty-project-template"></a>빈 프로젝트 템플릿

이제 완전히 정리 된 슬레이트에서 시작할 수 있도록 MVC 빈 프로젝트 템플릿이 실제로 비어 있습니다. 이전 버전의 빈 프로젝트 템플릿은 Basic으로 이름이 변경 되었습니다.

<a id="_Toc303253820"></a>
### <a name="add-controller-to-any-project-folder"></a>모든 프로젝트 폴더에 컨트롤러 추가

이제 마우스 오른쪽 단추를 클릭 하 고 MVC 프로젝트의 아무 폴더에서 나 **추가 컨트롤러** 를 선택할 수 있습니다. 이렇게 하면 MVC 및 Web API 컨트롤러를 별도의 폴더에 유지 하는 것을 포함 하 여 원하는 컨트롤러를 보다 유연 하 게 구성할 수 있습니다.

<a id="_Toc303253821"></a>
### <a name="bundling-and-minification"></a>묶음 및 축소

번들 및 축소 프레임 워크를 사용 하면 개별 파일을 스크립트와 CSS에 대 한 단일 번들 파일로 결합 하 여 웹 페이지에서 수행 해야 하는 HTTP 요청 수를 줄일 수 있습니다. 그런 다음 번들의 내용을 축소 하 여 해당 요청의 전체 크기를 줄일 수 있습니다. 축소에는 의미 체계에 따라 CSS 선택기를 축소 하기 위해 공백 제거와 같은 작업이 포함 될 수 있습니다. 번들은 코드에서 선언 및 구성 되며, 번들에 대 한 단일 링크를 생성 하거나 디버그할 때 번들의 개별 콘텐츠에 대 한 여러 링크를 생성할 수 있는 도우미 메서드를 통해 뷰에서 쉽게 참조할 수 있습니다. 자세한 내용은 [묶음 및 축소](../mvc/overview/performance/bundling-and-minification.md)를 참조 하세요.

<a id="_Toc303253822"></a>
### <a name="enabling-logins-from-facebook-and-other-sites-using-oauth-and-openid"></a>OAuth 및 Openid connect를 사용 하 여 Facebook 및 기타 사이트에서 로그인 사용

ASP.NET MVC 4 Internet 프로젝트 템플릿의 기본 템플릿에는 이제 DotNetOpenAuth 라이브러리를 사용 하는 OAuth 및 Openid connect 로그인에 대 한 지원이 포함 됩니다. OAuth 또는 Openid connect 공급자를 구성 하는 방법에 대 한 자세한 내용은 [WebForms, MVC 및 웹 페이지에 대 한 oauth/Openid connect 지원](https://blogs.msdn.com/b/webdev/archive/2012/08/15/oauth-openid-support-for-webforms-mvc-and-webpages.aspx) 및 [ASP.NET 웹 페이지의 oauth 및 openid connect 기능 설명서](../web-pages/overview/releases/top-features-in-web-pages-2.md#oauthsetup)를 참조 하세요.

<a id="_Toc303253806"></a>
## <a name="upgrading-an-aspnet-mvc-3-project-to-aspnet-mvc-4"></a>ASP.NET MVC 3 프로젝트를 ASP.NET MVC 4로 업그레이드

ASP.NET MVC 4는 동일한 컴퓨터에 ASP.NET MVC 3과 함께 설치할 수 있습니다. 그러면 ASP.NET MVC 3 응용 프로그램을 ASP.NET MVC 4로 업그레이드할 시기를 유연 하 게 선택할 수 있습니다.

가장 간단한 업그레이드 방법은 새 ASP.NET MVC 4 프로젝트를 만들고 기존 MVC 3 프로젝트의 모든 뷰, 컨트롤러, 코드 및 콘텐츠 파일을 새 프로젝트에 복사한 다음, 새 프로젝트의 어셈블리 참조가의 비 MVC 템플릿과 일치 하도록 업데이트 하는 것입니다. cluded assembiles를 사용 하 고 있습니다. MVC 3 프로젝트에서 web.config 파일을 변경한 경우 이러한 변경 내용을 MVC 4 프로젝트의 web.config 파일에 병합 해야 합니다.

기존 ASP.NET MVC 3 응용 프로그램을 버전 4로 수동으로 업그레이드 하려면 다음을 수행 합니다.

1. 프로젝트의 모든 Web.config 파일 (프로젝트의 루트에 있고, Views 폴더에 있고, 프로젝트의 각 영역에 대 한 Views 폴더에 있음)에서 다음 텍스트의 모든 인스턴스를 바꿉니다 (참고: System.web, Version = 1.0.0.0은에서 찾을 수 없음). Visual Studio 2012를 사용 하 여 만든 프로젝트: 

    [!code-console[Main](mvc4-release-notes/samples/sample2.cmd)]

    다음 텍스트를 사용 합니다.

    [!code-console[Main](mvc4-release-notes/samples/sample3.cmd)]
2. 루트 Web.config 파일에서 *웹 페이지: 버전* 요소를 "2.0.0.0"으로 업데이트 하 고 값이 "true" 인 새 *PreserveLoginUrl* 키를 추가 합니다. 

    [!code-xml[Main](mvc4-release-notes/samples/sample4.xml)]
3. 솔루션 탐색기에서 참조를 마우스 오른쪽 단추로 클릭 하 고 NuGet 패키지 관리를 선택 합니다. 왼쪽 창에서 **Online\NuGet 공식 패키지 원본**을 선택 하 고 다음을 업데이트 합니다.

    - ASP.NET MVC 4
    - (선택 사항) jQuery, jQuery 유효성 검사 및 jQuery UI
    - 필드 Entity Framework
    - (Optonal) Modernizr
4. 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 한 다음 프로젝트 언로드를 선택 합니다. 그런 다음 이름을 다시 마우스 오른쪽 단추로 클릭 하 고 *ProjectName*.csproj 편집을 선택 합니다.
5. *Projecttypeguids* 요소를 찾아서 {E53F8FEA-EAE0-44A6-8774-FFD645390401}을 {E3E379DF-F4C6-4180-9B81-6769533ABE47}로 바꿉니다.
6. 변경 내용을 저장 하 고 편집 중인 프로젝트 (.csproj) 파일을 닫은 다음 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 프로젝트 다시 로드를 선택 합니다.
7. 프로젝트가 이전 버전의 ASP.NET MVC를 사용 하 여 컴파일된 타사 라이브러리를 참조 하는 경우 루트 Web.config 파일을 열고 *구성* 섹션 아래에 다음 세 가지 *bindingRedirect* 요소를 추가 합니다. 

    [!code-xml[Main](mvc4-release-notes/samples/sample5.xml)]

<a id="_Toc303253817"></a>
## <a name="changes-from-aspnet-mvc-4-release-candidate"></a>ASP.NET MVC 4 릴리스 후보의 변경 내용

ASP.NET MVC 4 릴리스 후보의 릴리스 정보는 다음 위치에서 찾을 수 있습니다.

이 릴리스에서 ASP.NET MVC 4 릴리스 후보의 주요 변경 내용은 아래에 요약 되어 있습니다.

- **컨트롤러 단위 구성:** ASP.NET Web API 컨트롤러는 자체 포맷터, 작업 선택기 및 매개 변수 바인더를 설정 하기 위해 *IControllerConfiguration* 을 구현 하는 사용자 지정 특성을 사용 하 여 특성을 지정할 수 있습니다. *Httpcontrollerconfigurationattribute* 가 제거 되었습니다.
- **경로 메시지 처리기 당:** 이제 지정 된 경로에 대 한 요청 체인에서 최종 메시지 처리기를 지정할 수 있습니다. 이렇게 하면 전달 프레임 워크가 라우팅을 사용 하 여 자체 (비*IHttpController*) 끝점으로 디스패치할 수 있습니다.
- **진행률 알림:** *ProgressMessageHandler* 는 업로드 중인 요청 엔터티와 다운로드 중인 응답 엔터티 모두에 대 한 진행률 알림을 생성 합니다. 이 처리기를 사용 하 여 요청 본문을 업로드 하거나 응답 본문을 다운로드 하는 정도를 추적할 수 있습니다.
- **푸시 콘텐츠:** *Pushstreamcontent* 클래스를 사용 하면 데이터 공급자가 스트림을 사용 하 여 동기적 또는 비동기적으로 요청 또는 응답에 직접 쓰려는 시나리오를 사용할 수 있습니다. *Pushstreamcontent* 가 데이터를 수락할 준비가 되 면 출력 스트림을 사용 하 여 작업 대리자를 호출 합니다. 그러면 개발자는 필요한 기간 동안 스트림에 쓰고 쓰기가 완료 되 면 스트림을 닫을 수 있습니다. *Pushstreamcontent* 는 스트림 닫기를 검색 하 고 콘텐츠를 작성 하기 위한 기본 비동기 *작업* 을 완료 합니다.
- **오류 응답을 만드는 중:** *HttpError* 형식을 사용 하 여 유효성 검사 오류 및 예외와 같은 오류 정보를 일관 되 게 표시 하는 동시에 *IncludeErrorDetailPolicy*를 그대로 사용 합니다. 새 *Createerrorresponse* 확장 메서드를 사용 하 여 *HttpError* 를 콘텐츠로 쉽게 오류 응답을 만들 수 있습니다. *HttpError* 콘텐츠는 완전히 협상 된 콘텐츠입니다.
- **제거 MediaRangeMapping:** 미디어 유형 범위는 이제 기본 콘텐츠 negotiator 처리 됩니다.
- **이제 단순 형식 매개 변수에 대 한 기본 매개 변수 바인딩이 [FromUri]로 되어 있습니다.** ASP.NET Web API의 이전 릴리스에서는 단순 형식 매개 변수에 대 한 기본 매개 변수 바인딩이 모델 바인딩을 사용 했습니다. 이제 단순 형식 매개 변수에 대 한 기본 매개 변수 바인딩이 *[Fromuri]* 입니다.
- **작업 선택은 필수 매개 변수를** 준수 합니다. ASP.NET Web API의 작업 선택은 이제 URI에서 제공 되는 모든 필수 매개 변수가 제공 되는 경우에만 작업을 선택 합니다. 작업 메서드 시그니처의 인수에 기본값을 제공 하 여 매개 변수를 선택적으로 지정할 수 있습니다.
- **HTTP 매개 변수 바인딩 사용자 지정:** *Parameterbindingattribute* 를 사용 하 여 특정 작업 매개 변수에 대 한 매개 변수 바인딩을 사용자 지정 하거나 *Httpconfiguration* 의 *ParameterBindingRules* 를 사용 하 여 매개 변수 바인딩을 보다 폭넓게 사용자 지정 합니다.
- **향상 된 MediaTypeFormatter:** 포맷터는 이제 전체 *Httpcontent* 인스턴스에 액세스할 수 있습니다.
- **호스트 버퍼링 정책 선택:** ASP.NET Web API에서 *IHostBufferPolicySelector* 서비스를 구현 하 고 구성 하 여 호스트에서 버퍼링을 사용 하는 경우에 대 한 정책을 확인할 수 있도록 합니다.
- **호스트의 클라이언트 인증서에 대 한 액세스 권한 없는 방식:** *GetClientCertificate* 확장 메서드를 사용 하 여 요청 메시지에서 제공 된 클라이언트 인증서를 가져옵니다.
- **콘텐츠 협상 확장성:** *Defaultcontentnegotiator* 파생 하 고 원하는 콘텐츠 협상의 모든 측면을 재정의 하 여 콘텐츠 협상을 사용자 지정 합니다.
- **406 허용 되지 않는 응답 반환에 대 한 지원:** 이제 *Excludematchontypeonly* 매개 변수를 *true*로 설정 하 여 *defaultcontentnegotiator* 만들 때 적합 한 포맷터를 찾을 수 없는 경우 ASP.NET Web API에서 허용 되지 않는 406 응답을 반환할 수 있습니다.
- **양식 데이터를 NameValueCollection 또는 JToken으로 읽습니다.** 각각 *Parsequerystring* 및 *ReadAsFormDataAsync* extension 메서드를 사용 하 여 URI 쿼리 문자열 또는 요청 본문의 양식 데이터를 *NameValueCollection* 읽을 수 있습니다. 마찬가지로, 각&gt; 확장 *메서드를 사용* *하&lt;여* URI 쿼리 문자열 또는 요청 본문의 양식 데이터를 *jtoken* 로 읽을 수 있습니다.
- **다중 파트 기능 향상:** 이제 사용자에 게 최적의 방식으로 결과를 표시 하 고 읽을 수 있는 MIME 다중 파트 데이터의 형식에 완전히 맞는 *Multipartstreamprovider* 를 작성할 수 있습니다. 또한 구현이 MIME 다중 파트 본문 부분에서 원하는 post 처리를 수행할 수 있도록 하는 *Multipartstreamprovider* 에 사후 처리 단계를 후크 할 수 있습니다. 예를 들어 *Multipartformdatastreamprovider* 구현은 HTML 양식 데이터 파트를 읽고이를 *NameValueCollection* 에 추가 하므로 호출자가 쉽게 가져올 수 있습니다.
- **향상 된 링크 생성:** *Urlhelper* 는 더 이상 *httpcontrollercontext*에 의존 하지 않습니다. 이제 *HttpRequestMessage* 를 사용할 수 있는 모든 컨텍스트에서 *urlhelper* 에 액세스할 수 있습니다.
- **메시지 처리기 실행 순서 변경:** 이제 메시지 처리기가 역순으로 구성 된 순서 대로 실행 됩니다.
- **메시지 처리기를 연결 하기 위한 도우미입니다.** *DelegatingHandlers* 를 연결 하 고 원하는 파이프라인이 준비 된 *httpclient* 를 만들 수 있는 새 *httpclientfactory* 입니다. 또한 대체 내부 처리기 (기본값은 *Httpclienthandler*)를 연결 하는 기능을 제공 하 고, *httpmessage호출자* 를 사용 하는 경우 또는 *httpclient* 대신 *DelegatingHandler* 를 최상위 호출자로 사용 하는 경우 연결을 수행할 수 있습니다.
- **ASP.NET 웹 최적화의 CDNs 지원:** 이제 ASP.NET 웹 최적화는 CDN 대체 경로에 대 한 지원을 제공 하 여 각 번들에 대해 콘텐츠 배달 네트워크에서 동일한 리소스를 가리키는 추가 URL을 지정할 수 있도록 합니다. CDNs를 지원 하면 웹 응용 프로그램의 최종 소비자에 게 매우 가깝게 스크립트 및 스타일 번들을 얻을 수 있습니다. CDN을 사용할 수 없는 경우 프로덕션 앱에서 대체를 구현 해야 합니다. 대체 (fallback)를 테스트 합니다.
- **ASP.NET Web API 경로 및 구성이 *Webapiconfig.* 테스트 코드에서 사용할 수 있는 정적 메서드를 등록 합니다.** *RouteConfig RegisterRoutes* 에 이전에 ASP.NET Web API 경로가 표준 MVC 경로와 함께 추가 되었습니다. 이제 기본 ASP.NET Web API 경로 및 구성이 별도의 *Webapiconfig. Register* 메서드로 처리 되어 테스트를 용이 하 게 합니다.

<a id="_Toc303253815"></a>
## <a name="known-issues-and-breaking-changes"></a>알려진 문제 및 주요 변경 내용

- **ASP.NET MVC 4의 RC 및 RTM 버전은 모바일 뷰를 반환 해야 하는 경우 캐시 된 데스크톱 보기를 잘못 반환 합니다.**

    - 해결 방법에 대 한 자세한 내용은 [ASP.NET MVC 4 Mobile 캐싱 버그 수정](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) 을 참조 하세요. 수정은 [고정 displaymodes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) NuGet 패키지에서 설치할 수 있습니다.
- **Razor 뷰 엔진의 주요 변경 내용**입니다. 다음 형식이 *system.object*에서 제거 되었습니다. 

    - *ModelSpan*
    - *MvcVBRazorCodeGenerator*
    - *MvcCSharpRazorCodeGenerator*
    - *MvcVBRazorCodeParser*

  다음 메서드도 제거 되었습니다. 

    - *MvcCSharpRazorCodeParser (ParseInheritsStatement) ((System.web.*
    - *MvcWebPageRazorHost (DecorateCodeGenerator) (RazorCodeGenerator)*
    - *MvcVBRazorCodeParser (System.web. CodeBlockInfo)*
- **ASP.NET MVC 4 앱의 WebData 디렉터리에 WebMatrix를 포함 하는 경우 폼 인증에 대 한 URL을 사용 합니다.** 응용 프로그램에 WebData 어셈블리를 추가 하는 경우 (예를 들어, 배포 가능 종속성 추가 대화 상자를 사용할 때 "Razor 구문을 사용 하 여 ASP.NET 웹 페이지"을 선택 하는 경우)에는 기본 ASP.NET MVC 계정 컨트롤러에서 예상 하는/account/pvrn이 아닌/t r i n s/logon으로의 인증 로그인 리디렉션이 재정의 됩니다. 이 동작을 방지 하 고 web.config의 인증 섹션에 이미 지정 된 URL을 사용 하려면 PreserveLoginUrl 라는 appSetting를 추가 하 고 true로 설정 하면 됩니다. 

    [!code-xml[Main](mvc4-release-notes/samples/sample6.xml)]
- **Visual Studio 2010 및 Visual Web Developer 2010의 side-by-side 설치를 위해 ASP.NET MVC 4를 설치 하려고 하면 NuGet 패키지 관리자가 설치 되지 않습니다.** ASP.NET MVC 4를 사용 하 여 Visual Studio 2010 및 Visual Web Developer 2010을 함께 실행 하려면 두 버전의 Visual Studio가 이미 설치 된 후 ASP.NET MVC 4를 설치 해야 합니다.
- **필수 구성 요소가 이미 제거 된 경우 ASP.NET MVC 4를 제거 하는 작업이 실패 합니다.** ASP.NET MVC 4를 완전히 제거 하려면 Visual Studio를 제거 하기 전에 ASP.NET MVC 4를 제거 해야 합니다.
- **ASP.NET MVC 4를 설치 하면 ASP.NET MVC 3 RTM 응용 프로그램이 중단 됩니다.** RTM 릴리스로 만든 ASP.NET MVC 3 응용 프로그램 ( [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/download/details.aspx?id=1491) 릴리스를 사용 하지 않음)은 ASP.NET mvc 4와 함께 작동 하기 위해 다음과 같이 변경 해야 합니다. 이러한 업데이트를 수행 하지 않고 프로젝트를 빌드하면 컴파일 오류가 발생 합니다. 

    **필수 업데이트**

  1. 루트 Web.config 파일에서 키 *웹 페이지: 버전* 및 값 *1.0.0.0*을 사용 하 여 새 *&lt;appSettings&gt;* 항목을 추가 합니다. 

      [!code-xml[Main](mvc4-release-notes/samples/sample7.xml)]
  2. 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 한 다음 프로젝트 언로드를 선택 합니다. 그런 다음 이름을 다시 마우스 오른쪽 단추로 클릭 하 고 *ProjectName*.csproj 편집을 선택 합니다.
  3. 다음 어셈블리 참조를 찾습니다. 

      [!code-xml[Main](mvc4-release-notes/samples/sample8.xml)]

      다음으로 바꿉니다.

      [!code-xml[Main](mvc4-release-notes/samples/sample9.xml)]
  4. 변경 내용을 저장 하 고 편집 중인 프로젝트 (.csproj) 파일을 닫은 다음 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 다시 로드를 선택 합니다.

- **ASP.NET MVC 4 프로젝트를 4.5의 대상 4.0으로 변경 해도 EntityFramework 어셈블리 참조는 업데이트 되지 않습니다.** ASP.NET MVC 4 프로젝트를 대상 4.0 4.5 후 대상으로 변경 하는 경우 EntityFramework 어셈블리에 대 한 참조는 여전히 4.5 버전을 가리킵니다. 이 문제를 해결 하려면 EntityFramework NuGet 패키지를 제거 하 고 다시 설치 합니다.
- **403 4.5에서 대상 4.0로 변경한 후 Azure에서 ASP.NET MVC 4 응용 프로그램을 실행할 때 사용할 수 없음:** 4.5에 연결한 후 ASP.NET MVC 4 프로젝트를 대상 4.0으로 변경 하 고 Azure에 배포 하는 경우 런타임에 403 사용할 수 없음 오류가 표시 될 수 있습니다. 이 문제를 해결 하려면 web.config에 다음을 추가 합니다. `<modules runAllManagedModulesForAllRequests="true" />`
- **Razor 파일의 문자열 리터럴에 '\'를 입력 하면 Visual Studio 2012의 작동이 중단 됩니다.** 문제를 해결 하려면 먼저 문자열 리터럴의 닫는 따옴표를 입력 합니다.
- <strong>인터넷 템플릿에서 &quot;계정/관리&quot;를 검색 하면 CHS, 추적 및 CHT 언어에 대 한 런타임 오류가 발생 합니다.</strong> 문제를 해결 하려면 <em>&lt;강력한&gt;</em> 태그 내의 유일한 콘텐츠로 배치 하 여 <em>@User.Identity.Name</em> 를 분리 하도록 페이지를 수정 합니다.
- **Google 및 LinkedIn 공급자는 Azure 웹 사이트 내에서 지원 되지 않습니다.** Azure 웹 사이트에 배포 하는 경우 대체 인증 공급자를 사용 합니다.
- **IIS 8 Express/IIS에서 UriPathExtensionMapping을 사용 하는 경우 확장을 사용 하려고 할 때 404 찾을 수 없음 오류가 표시 됩니다.** 정적 파일 처리기는 *Uripathextensionmappings*를 사용 하는 웹 api에 대 한 요청을 방해 합니다. 문제를 해결 하려면 web.config에서 *runAllManagedModulesForAllRequests = true* 를 설정 합니다.
- **Controller. Execute 메서드는 더 이상 호출 되지 않습니다.** 이제 모든 MVC 컨트롤러는 항상 비동기적으로 실행 됩니다.
