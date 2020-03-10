---
uid: mvc/mvc3
title: ASP.NET MVC 3
author: rick-anderson
description: (4 월 2011 도구 업데이트 포함) ASP.NET MVC 3은 잘 구성 된 디자인 패턴을 사용 하 여 확장성 있는 표준 기반 웹 응용 프로그램을 빌드하기 위한 프레임 워크입니다.
ms.author: riande
ms.date: 10/05/2010
ms.assetid: dddc8812-a0bc-49f9-aafb-caf2064c2b8c
msc.legacyurl: /mvc/mvc3
msc.type: content
ms.openlocfilehash: 421a06c89d4dbcb05d4080033813cc6558b7c698
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499649"
---
# <a name="aspnet-mvc-3"></a>ASP.NET MVC 3

> *(4 월 2011 도구 업데이트 포함)*
> 
> ASP.NET MVC 3은 잘 구성 된 디자인 패턴을 사용 하 고 ASP.NET 및 .NET Framework의 기능을 사용 하 여 확장성 있는 표준 기반 웹 응용 프로그램을 빌드하기 위한 프레임 워크입니다.
> 
> ASP.NET MVC 2와 나란히 설치 되므로 지금 사용을 시작 하세요!
> 
> 여기에서 [설치 프로그램](https://go.microsoft.com/fwlink/?LinkID=208140) 다운로드

## <a name="top-features"></a>주요 기능

- NuGet을 통해 확장 가능한 통합 스 캐 폴딩 시스템
- HTML 5 사용 프로젝트 템플릿
- 새 Razor 뷰 엔진을 포함 하는 표현 뷰
- 종속성 주입 및 전역 작업 필터를 사용 하는 강력한 후크
- JavaScript, jQuery 유효성 검사 및 JSON 바인딩을 사용 하 여 풍부한 JavaScript 지원
- *[아래의](#overview) 전체 기능 목록 읽기*

## <a name="top-links"></a>상위 링크

ASP.NET MVC 3의 새로운 기능

- Phil Haack: [ASP.NET MVC 3 출시](http://haacked.com/archive/2011/01/13/aspnetmvc3-released.aspx)
- Scott Hanselman: [ASP.NET MVC3, WebMatrix, NuGet, IIS Express 및 과수원 릴리스-컨텍스트의 Microsoft 1 월 웹 릴리스](http://www.hanselman.com/blog/ASPNETMVC3WebMatrixNuGetIISExpressAndOrchardReleasedTheMicrosoftJanuaryWebReleaseInContext.aspx)
- Scott Guthrie: [ASP.NET MVC 3, IIS Express, SQL CE 4, 웹 팜 프레임 워크, 과수원, WebMatrix 릴리스 발표](https://weblogs.asp.net/scottgu/archive/2011/01/13/announcing-release-of-asp-net-mvc-3-iis-express-sql-ce-4-web-farm-framework-orchard-webmatrix.aspx)
- [ASP.NET MVC 3에 대 한 릴리스 정보](../whitepapers/mvc3-release-notes.md)

설치 및 도움말

- [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MVC3) 를 사용 하 여 ASP.NET MVC 3 설치 (권장)
- [설치 관리자 실행 파일](https://go.microsoft.com/fwlink/?LinkID=208140) 을 사용 하 여 ASP.NET MVC 3 설치
- [Visual Studio 11 Developer Preview 용 ASP.NET MVC 3](https://go.microsoft.com/fwlink/?LinkID=208140) 설치
- [ASP.NET MVC 3 소개 자습서를](overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 참조 하십시오.
- [포럼](https://forums.asp.net/1146.aspx) 의 ASP.NET MVC 3에 대 한 도움말 보기 및 논의

<a id="overview"></a>
## <a name="aspnet-mvc-3-overview"></a>ASP.NET MVC 3 Overview

ASP.NET MVC 3은 ASP.NET MVC 1 및 2를 기반으로 하며, 코드를 단순화 하 고 더 심층적인 확장성을 허용 하는 뛰어난 기능을 추가 합니다. 이 항목에서는 다음 섹션으로 구성 된이 릴리스에 포함 된 여러 가지 새로운 기능에 대 한 개요를 제공 합니다.

- [MvcScaffold 통합으로 확장 가능한 스 캐 폴딩](#BM_MvcScaffolding)
- [HTML 5 사용 프로젝트 템플릿](#BM_HTML5)
- [Razor 뷰 엔진](#BM_TheRazorViewEngine)
- [다중 뷰 엔진 지원](#BM_Support_for_Multiple_View_Engines)
- [컨트롤러 개선](#BM_Controller_Improvements)
- [JavaScript 및 Ajax](#BM_JavaScript_and_Ajax_Improvements)
- [모델 유효성 검사 개선](#BM_Model_Validation_Improvements)
- [종속성 주입 향상](#BM_Dependency_Injection_Improvements)
- [기타 새 기능](#BM_Other_New_Features)

<a id="BM_MvcScaffolding"></a>

## <a name="extensible-scaffolding-with-mvcscaffold-integration"></a>MvcScaffold 통합으로 확장 가능한 스 캐 폴딩

새 스 캐 폴딩 시스템을 사용 하면 프레임 워크를 완전히 처음 접하는 경우 생산적인 사용을 보다 쉽게 선택 하 여 시작 하 고, 숙련 된 작업을 이미 알고 있는 경우 일반적인 개발 작업을 자동화할 수 있습니다.

이는 **Mvcscaffolding 캐 폴딩**이라는 새 NuGet *스 캐 폴딩* 패키지에서 지원 됩니다. "스 캐 폴딩" 이라는 용어는 소프트웨어의 기본 개요를 빠르게 생성 하 여 편집 하 고 사용자 지정할 수 있는 소프트웨어 기술에 사용 됩니다. ASP.NET MVC에 대해 만드는 스 캐 폴딩 패키지는 여러 시나리오에서 매우 유용 합니다.

- **ASP.NET MVC를 처음으로 학습**하는 경우에는 사용자의 요구에 따라 편집 하 고 조정할 수 있는 유용한 작업 코드를 신속 하 게 가져올 수 있는 방법을 제공 합니다. 이를 통해 빈 페이지를 trauma 하 고 시작 하는 위치를 알 수 없습니다.
- ASP.NET MVC가 잘 알고 있고 이제 개체 관계형 매퍼, 뷰 엔진, 테스트 라이브러리 등의 **몇 가지 새로운 추가 기능 기술을 탐색** 하는 경우 해당 기술의 작성자가 스 캐 폴딩 패키지를 만들었을 수도 있기 때문입니다.
- **작업에 일부 정렬의 유사한 클래스 또는 파일을 반복적으로 만드는 작업이 포함 된 경우**테스트 설비, 배포 스크립트 또는 필요한 다른 항목을 출력 하는 사용자 지정 scaffolders를 만들 수 있기 때문입니다. 팀의 모든 사용자가 사용자 지정 scaffolders를 사용할 수 있습니다.

MvcScaffolding 캐 폴딩의 다른 기능은 다음과 같습니다.

- 및 VB C# 프로젝트에 대 한 지원
- Razor 및 ASPX 뷰 엔진 지원
- ASP.NET MVC 영역으로 스 캐 폴딩을 지원 하 고 사용자 지정 보기 레이아웃/마스터를 사용 합니다.
- T4 템플릿을 편집 하 여 출력을 쉽게 사용자 지정할 수 있습니다.
- 사용자 지정 PowerShell 논리 및 사용자 지정 T4 템플릿을 사용 하 여 완전히 새로운 scaffolders를 추가할 수 있습니다. 이러한 매개 변수 (및 사용자 지정 매개 변수)는 콘솔 탭 완성 목록에 자동으로 표시 됩니다.
- 다른 기술에 대 한 추가 scaffolders 포함 된 NuGet 패키지를 가져올 수 있습니다 (예: 현재 LINQ to SQL에 대 한 개념 증명). 그리고 조합 하 고 일치

ASP.NET MVC 3 Tools 업데이트에는 다음과 같은이 스 캐 폴딩 시스템에 대 한 뛰어난 Visual Studio 지원 기능이 포함 되어 있습니다.

- 이제 컨트롤러 추가 대화 상자에서 컨트롤러 작업 및 해당 보기의 만들기, 읽기, 업데이트 및 삭제에 대 한 완전 한 자동 스 캐 폴딩을 지원 합니다. 기본적으로이 스 캐 폴드는 EF Code First를 사용 하 여 데이터 액세스 코드를 합니다.
- 컨트롤러 추가 대화 상자는 *Mvcscaffolding 캐 폴딩*과 같은 NuGet 패키지를 통해 *확장 가능한 스 캐 폴드* 을 지원 합니다. 이렇게 하면 사용자 지정 스 캐 폴드를 대화에 연결할 수 있습니다 .이 대화 상자에는 NHibernate 절전 모드 또는 다른 데이터 액세스 기술 (예: 스 캐 폴드)을 사용 하 여 다른 데이터 액세스 기술에 대 한을 만들 수 있습니다.

ASP.NET MVC 3에서 스 캐 폴딩에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- 다음을 포함 한 Steve Sanderson의 게시물 시리즈 

    1. [소개: MvcScaffolding 캐 폴딩 패키지를 사용 하 여 ASP.NET MVC 3 프로젝트 스 캐 폴드](http://blog.stevensanderson.com/2011/01/13/scaffold-your-aspnet-mvc-3-project-with-the-mvcscaffolding-package/)
    2. [표준 사용: 일반적인 사용 사례 및 옵션](http://blog.stevensanderson.com/2011/01/13/mvcscaffolding-standard-usage/)
    3. [일 대 다 관계](http://blog.stevensanderson.com/2011/01/28/mvcscaffolding-one-to-many-relationships/)
    4. [스 캐 폴딩 작업 및 단위 테스트](http://blog.stevensanderson.com/2011/03/28/scaffolding-actions-and-unit-tests-with-mvcscaffolding/)
    5. [T4 템플릿 재정의](http://blog.stevensanderson.com/2011/04/06/mvcscaffolding-overriding-the-t4-templates/)
    6. [이 게시물: 사용자 지정 scaffolders 만들기](http://blog.stevensanderson.com/2011/04/07/mvcscaffolding-creating-custom-scaffolders/)
- Scott Hanselman의 PDC 2010 세션에서 [Microsoft "명명 되지 않은 웹 패키지 패키지"를 사용 하 여 블로그 빌드](http://www.hanselman.com/blog/PDC10BuildingABlogWithMicrosoftUnnamedPackageOfWebLove.aspx)
- [MVC 3 릴리스 정보](../whitepapers/mvc3-release-notes.md)

<a id="BM_HTML5"></a>

## <a name="html-5-project-templates"></a>HTML 5 프로젝트 템플릿

새 프로젝트 대화 상자에는 HTML 5 버전의 프로젝트 템플릿을 사용 하도록 설정 하는 확인란이 포함 되어 있습니다. 이러한 템플릿은 Modernizr 1.7를 활용 하 여 하위 수준 브라우저에서 HTML 5 및 CSS 3에 대 한 호환성 지원을 제공 합니다.

<a id="BM_TheRazorViewEngine"></a>

## <a name="the-razor-view-engine"></a>Razor 뷰 엔진

ASP.NET MVC 3에는 다음과 같은 이점을 제공 하는 Razor 라는 새로운 뷰 엔진이 제공 됩니다.

- Razor 구문은 깨끗 하 고 간결 하므로 최소한의 키 입력이 필요 합니다.
- Razor는 및 Visual Basic와 같은 C# 기존 언어를 기반으로 하기 때문에 쉽게 학습할 수 있습니다.
- Visual Studio에는 Razor 구문에 대 한 IntelliSense 및 코드 색 지정이 포함 되어 있습니다.
- 응용 프로그램을 실행 하거나 웹 서버를 시작할 필요 없이 Razor 보기를 단위 테스트할 수 있습니다.

몇 가지 새로운 Razor 기능에는 다음이 포함 됩니다.

- 뷰에 전달 되는 형식을 지정 하는 `@model` 구문입니다.
- 주석 구문을 `@* *@` 합니다.
- 전체 사이트에 대해 기본값 (예: `layoutpage`)을 한 번 지정 하는 기능입니다.
- HTML로 인코딩하지 않고 텍스트를 표시 하는 `Html.Raw` 메서드입니다.
- 여러 뷰 ( *\_viewstart. cshtml* 또는 *\_viewstart. vbhtml* 파일) 간에 코드를 공유할 수 있도록 지원 합니다.

Razor는 다음과 같은 새로운 HTML 도우미도 포함 합니다.

- `Chart`입니다. ASP.NET 4에서 차트 컨트롤과 동일한 기능을 제공 하 여 차트를 렌더링 합니다.
- `WebGrid`입니다. 페이징 및 정렬 기능을 사용 하 여 데이터 표를 렌더링 합니다.
- `Crypto`입니다. 는 해싱 알고리즘을 사용 하 여 적절 한 솔트된 및 해시 된 암호를 만듭니다.
- `WebImage`입니다. 이미지를 렌더링 합니다.
- `WebMail`입니다. 메일 메시지를 전송합니다.

Razor에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [Razor를 소개 하는 Scott Guthrie의 블로그 게시물](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)
- [@model 키워드를 소개 하는 Scott Guthrie의 블로그 게시물](https://weblogs.asp.net/scottgu/archive/2010/10/19/asp-net-mvc-3-new-model-directive-support-in-razor.aspx)
- [Razor 레이아웃을 소개 하는 Scott Guthrie의 블로그 게시물](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)
- [Razor API 빠른 참조](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)
- [MVC 3 릴리스 정보](../whitepapers/mvc3-release-notes.md)

<a id="BM_Support_for_Multiple_View_Engines"></a>

## <a name="support-for-multiple-view-engines"></a>다중 뷰 엔진 지원

ASP.NET MVC 3의 **뷰 추가** 대화 상자를 사용 하 여 작업 하려는 뷰 엔진을 선택 하 고 **새 프로젝트** 대화 상자에서 프로젝트에 대 한 기본 뷰 엔진을 지정할 수 있습니다. 사용자는 ASPX (Web Forms 뷰 엔진), Razor 또는 [Spark](http://sparkviewengine.com/), [Nhaml](https://code.google.com/p/nhaml/)또는 [ndjango](http://ndjango.org/)와 같은 오픈 소스 뷰 엔진을 선택할 수 있습니다.

<a id="BM_Controller_Improvements"></a>

## <a name="controller-improvements"></a>컨트롤러 개선

### <a name="global-action-filters"></a>전역 작업 필터

작업 메서드가 실행 되기 전이나 동작 메서드가 실행 된 후에 논리를 수행 하려는 경우가 있습니다. 이를 지원 하기 위해 ASP.NET MVC 2에서 작업 필터를 제공 합니다. 작업 필터는 사전 작업 및 작업 후 동작을 특정 컨트롤러 작업 메서드에 추가 하는 선언적 방법을 제공 하는 사용자 지정 특성입니다. 그러나 일부 경우에는 모든 작업 메서드에 적용 되는 사전 작업 또는 사후 작업 동작을 지정 해야 할 수 있습니다. MVC 3에서는 전역 필터를 `GlobalFilters` 컬렉션에 추가 하 여 지정할 수 있습니다. 전역 작업 필터에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [MVC 3 Preview의 Scott Guthrie의 블로그](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)
- [ASP.NET MVC에서 필터링](https://msdn.microsoft.com/library/gg416513(VS.98).aspx)

### <a name="new-viewbag-property"></a>새 "ViewBag" 속성

MVC 2 컨트롤러는 런타임에 바인딩된 사전 API를 사용 하 여 뷰 템플릿에 데이터를 전달할 수 있도록 하는 `ViewData` 속성을 지원 합니다. MVC 3에서는 `ViewBag` 속성과 함께 약간 간단한 구문을 사용 하 여 동일한 용도를 달성할 수도 있습니다. 예를 들어 `ViewData["Message"]="text"`을 작성 하는 대신 `ViewBag.Message="text"`를 작성할 수 있습니다. `ViewBag` 속성을 사용 하기 위해 강력한 형식의 클래스를 정의할 필요는 없습니다. 동적 속성 이므로 속성을 가져오거나 설정 하기만 하면 런타임에 동적으로 해결 됩니다. 내부적으로 `ViewBag` 속성은 `ViewData` 사전에 이름/값 쌍으로 저장 됩니다. (참고: 대부분의 MVC 3 시험판 버전에서 `ViewBag` 속성의 이름은 `ViewModel` 속성입니다.)

### <a name="new-actionresult-types"></a>새 "ActionResult" 형식

다음 `ActionResult` 형식 및 해당 도우미 메서드는 MVC 3에서 새롭게 향상 되거나 향상 되었습니다.

- [HttpNotFoundResult](https://msdn.microsoft.com/library/system.web.mvc.httpnotfoundresult(v=vs.98).aspx). 404 HTTP 상태 코드를 클라이언트에 반환 합니다.
- [Redirectresult](https://msdn.microsoft.com/library/system.web.mvc.redirectresult(v=VS.98).aspx). 부울 매개 변수에 따라 임시 리디렉션 (HTTP 302 상태 코드) 또는 영구 리디렉션 (HTTP 301 상태 코드)을 반환 합니다. 이러한 변경과 함께 [컨트롤러](https://msdn.microsoft.com/library/system.web.mvc.controller(v=VS.98).aspx) 클래스에는 `RedirectPermanent`, `RedirectToRoutePermanent`및 `RedirectToActionPermanent`의 영구 리디렉션을 수행 하는 세 가지 메서드가 있습니다. 이러한 메서드는 `Permanent` 속성이 `true`로 설정 된 `RedirectResult`의 인스턴스를 반환 합니다.
- [HttpStatusCodeResult](https://msdn.microsoft.com/library/system.web.mvc.httpstatuscoderesult(v=VS.98).aspx). 사용자가 지정한 HTTP 상태 코드를 반환 합니다.

<a id="BM_JavaScript_and_Ajax_Improvements"></a>

## <a name="javascript-and-ajax-improvements"></a>JavaScript 및 Ajax 개선 사항

기본적으로 MVC 3의 Ajax 및 유효성 검사 도우미는 방해가 되지 않는 JavaScript 방법을 사용 합니다. JavaScript가 없는 JavaScript는 인라인 JavaScript를 HTML로 삽입 하지 않도록 방지 합니다. 이렇게 하면 HTML이 작고 복잡 하지 않으므로 JavaScript 라이브러리를 쉽게 교체 하거나 사용자 지정할 수 있습니다. MVC 3의 유효성 검사 도우미는 기본적으로 `jQueryValidate` 플러그 인도 사용 합니다. MVC 2 동작을 원하는 경우 *web.config* 파일 설정을 사용 하 여 문제가 없는 JavaScript를 사용 하지 않도록 설정할 수 있습니다. JavaScript 및 Ajax 개선 사항에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [위키백과 사이트의 기본 JavaScript에 대 한 기본 소개](http://en.wikipedia.org/wiki/Unobtrusive_JavaScript)
- [Brad Wilson의 JavaScript Post](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-ajax.html)
- [Brad Wilson의 JavaScript 유효성 검사 게시물](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)
- [Razor 및 비-JavaScript를 사용 하 여 MVC 3 응용 프로그램 만들기](overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript.md) (ASP.NET 사이트의 자습서)
- [MVC 3 릴리스 정보](../whitepapers/mvc3-release-notes.md)

### <a name="client-side-validation-enabled-by-default"></a>기본적으로 클라이언트 쪽 유효성 검사 사용

이전 버전의 MVC에서는 클라이언트 쪽 유효성 검사를 사용 하기 위해 뷰에서 `Html.EnableClientValidation` 메서드를 명시적으로 호출 해야 합니다. MVC 3에서 클라이언트 쪽 유효성 검사는 기본적으로 사용 하도록 설정 되어 있기 때문에 더 이상 필요 하지 않습니다. *Web.config 파일의* 설정을 사용 하 여이 기능을 사용 하지 않도록 설정할 수 있습니다.

클라이언트 쪽 유효성 검사가 작동 하려면 여전히 사이트에서 적절 한 jQuery 및 jQuery 유효성 검사 라이브러리를 참조 해야 합니다. 사용자의 서버에서 해당 라이브러리를 호스팅하거나 Microsoft 또는 Google의 CDNs와 같은 CDN (content delivery network)에서 해당 라이브러리를 참조할 수 있습니다.

### <a name="remote-validator"></a>원격 유효성 검사기

ASP.NET MVC 3은 jQuery 유효성 검사 플러그 인의 원격 유효성 검사기 지원을 활용할 수 있도록 하는 새로운 [Remoteattribute](https://msdn.microsoft.com/library/system.web.mvc.remoteattribute(v=VS.98).aspx) 클래스를 지원 합니다. 이렇게 하면 클라이언트 쪽 유효성 검사 라이브러리가 서버에서 정의한 사용자 지정 메서드를 자동으로 호출 하 여 서버 쪽만 수행할 수 있는 유효성 검사 논리를 수행할 수 있습니다.

다음 예제에서 `Remote` 특성은 `UserName` 필드의 유효성을 검사 하기 위해 클라이언트 유효성 검사에서 `UsersController` 클래스의 `UserNameAvailable` 라는 동작을 호출 하도록 지정 합니다.

[!code-csharp[Main](mvc3/samples/sample1.cs)]

다음 예에서는 해당 하는 컨트롤러를 보여 줍니다.

[!code-csharp[Main](mvc3/samples/sample2.cs)]

`Remote` 특성을 사용 하는 방법에 대 한 자세한 내용은 MSDN library의 [방법: ASP.NET MVC에서 원격 유효성 검사 구현](https://msdn.microsoft.com/library/gg508808(VS.98).aspx) 을 참조 하세요.

### <a name="json-binding-support"></a>JSON 바인딩 지원

ASP.NET MVC 3에는 작업 메서드가 JSON으로 인코딩된 데이터를 수신 하 고 작업 메서드 매개 변수에 모델 바인딩할 수 있도록 하는 기본 제공 JSON 바인딩 지원이 포함 되어 있습니다. 이 기능은 클라이언트 템플릿 및 데이터 바인딩과 관련 된 시나리오에서 유용 합니다. 클라이언트 템플릿을 사용 하면 클라이언트에서 실행 되는 템플릿을 사용 하 여 단일 데이터 항목 또는 데이터 항목 집합을 서식 지정 하 고 표시할 수 있습니다. MVC 3에서는 JSON 데이터를 보내고 받는 서버의 작업 메서드와 클라이언트 템플릿을 쉽게 연결할 수 있습니다. JSON 바인딩 지원에 대 한 자세한 내용은 [Scott Guthrie의 MVC 3 Preview 블로그 게시물](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)의 **JavaScript 및 AJAX 개선 사항** 섹션을 참조 하세요.

<a id="BM_Model_Validation_Improvements"></a>

## <a name="model-validation-improvements"></a>모델 유효성 검사 개선

### <a name="dataannotations-metadata-attributes"></a>"DataAnnotations" 메타 데이터 특성

ASP.NET MVC 3은 `DisplayAttribute`와 같은 `DataAnnotations` 메타 데이터 특성을 지원 합니다.

### <a name="validationattribute-class"></a>"ValidationAttribute" 클래스

`ValidationAttribute` 클래스는 유효성을 검사 하는 개체와 같은 현재 유효성 검사 컨텍스트에 대 한 추가 정보를 제공 하는 새로운 `IsValid` 오버 로드를 지원 하기 위해 .NET Framework 4에서 향상 되었습니다. 이를 통해 모델의 다른 속성을 기반으로 현재 값의 유효성을 검사할 수 있는 더 다양 한 시나리오를 사용할 수 있습니다. 예를 들어 새 `CompareAttribute` 특성을 사용 하면 모델의 두 속성 값을 비교할 수 있습니다. 다음 예제에서 `ComparePassword` 속성은 유효 하기 위해 `Password` 필드와 일치 해야 합니다.

[!code-csharp[Main](mvc3/samples/sample3.cs)]

### <a name="validation-interfaces"></a>유효성 검사 인터페이스

[IValidatableObject](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.ivalidatableobject.aspx) 인터페이스를 사용 하면 모델 수준 유효성 검사를 수행할 수 있으며,이를 통해 전체 모델의 상태 또는 모델 내 두 속성 간의 유효성 검사 오류 메시지를 제공할 수 있습니다. 이제 MVC 3은 모델 바인딩 시 `IValidatableObject` 인터페이스에서 오류를 검색 하 고 기본 제공 HTML 폼 도우미를 사용 하 여 뷰 내에서 영향을 받는 필드를 자동으로 플래그를 표시 하거나 강조 표시 합니다.

[Iclientvalidatable](https://msdn.microsoft.com/library/system.web.mvc.iclientvalidatable(v=VS.98).aspx) 인터페이스를 사용 하면 ASP.NET MVC에서 유효성 검사기가 클라이언트 유효성 검사를 지원 하는지 여부를 런타임에 검색할 수 있습니다. 이 인터페이스는 다양 한 유효성 검사 프레임 워크와 통합할 수 있도록 설계 되었습니다.

유효성 검사 인터페이스에 대 한 자세한 내용은 [Scott Guthrie의 MVC 3 Preview 블로그 게시물](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)의 **모델 유효성 검사 개선 사항** 섹션을 참조 하세요. 그러나 블로그의 "IValidateObject"에 대 한 참조는 "IValidatableObject" 여야 합니다.

<a id="BM_Dependency_Injection_Improvements"></a>

## <a name="dependency-injection-improvements"></a>종속성 주입 향상

ASP.NET MVC 3에서는 DI (종속성 주입) 적용 및 종속성 주입 또는 IOC (제어의 반전) 컨테이너와의 통합에 대 한 향상 된 지원을 제공 합니다. 다음 영역에서 DI에 대 한 지원이 추가 되었습니다.

- 컨트롤러 (컨트롤러 팩터리 등록 및 삽입, 컨트롤러 삽입).
- 뷰 (뷰 엔진을 등록 및 삽입 하 고, 종속성을 뷰 페이지에 삽입)
- 작업 필터 (필터를 찾고 삽입)
- 모델 바인더 (등록 및 삽입)
- 모델 유효성 검사 공급자 (등록 및 삽입)
- 모델 메타 데이터 공급자 (등록 및 삽입)
- 값 공급자 (등록 및 삽입)

MVC 3은 [공용 서비스 로케이터](https://github.com/unitycontainer/commonservicelocator) 라이브러리 및 해당 라이브러리의 `IServiceLocator` 인터페이스를 지 원하는 모든 DI 컨테이너를 지원 합니다. 또한 DI 프레임 워크를 쉽게 통합할 수 있도록 해 주는 새로운 `IDependencyResolver` 인터페이스를 지원 합니다.

MVC 3의 DI에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [서비스 위치에 대 한 Brad Wilson의 블로그 게시물 시리즈](http://bradwilson.typepad.com/blog/2010/07/service-location-pt1-introduction.html)
- [MVC 3 릴리스 정보](../whitepapers/mvc3-release-notes.md)

<a id="BM_Other_New_Features"></a>

## <a name="other-new-features"></a>기타 새 기능

### <a name="nuget-integration"></a>NuGet 통합

ASP.NET MVC 3은 설치의 일부로 NuGet을 자동으로 설치 하 고 사용 하도록 설정 합니다. NuGet은 프로젝트에서 .NET 라이브러리 및 도구를 쉽게 찾고 설치 하 고 사용할 수 있게 해 주는 무료 오픈 소스 패키지 관리자입니다. ASP.NET Web Forms 및 ASP.NET MVC를 비롯 한 모든 Visual Studio 프로젝트 형식에서 작동 합니다.

NuGet을 통해 오픈 소스 프로젝트를 유지 관리 하는 개발자 (예: Moq, NHibernate 절전 모드, Ninject, StructureMap, NUnit, Windsor, RhinoMocks 및 Elmah)를 사용 하 여 라이브러리를 패키지 하 고 온라인 갤러리에 등록할 수 있습니다. 이러한 라이브러리 중 하나를 사용 하 여 패키지를 찾고 작업 중인 프로젝트에 설치 하려는 .NET 개발자의 경우에는이 작업을 쉽게 수행할 수 있습니다.

ASP.NET 3 Tools 업데이트를 사용 하면 프로젝트 템플릿에 JavaScript 라이브러리가 사전 설치 된 NuGet 패키지를 포함 하므로 NuGet을 통해 업데이트할 수 있습니다. Entity Framework Code First도 NuGet 패키지로 미리 설치 됩니다.

NuGet에 대한 자세한 내용은 [NuGet 설명서](https://docs.microsoft.com/nuget/)를 참조하세요.

### <a name="partial-page-output-caching"></a>부분 페이지 출력 캐싱

ASP.NET MVC는 버전 1부터 전체 페이지 응답의 출력 캐싱을 지원 합니다. MVC 3에서는 부분 페이지 출력 캐싱도 지원 하므로 지역 또는 응답의 조각을 쉽게 캐시할 수 있습니다. 캐싱에 대 한 자세한 내용은 mvc 3 릴리스 [정보](../whitepapers/mvc3-release-notes.md)및 mvc 3 릴리스 정보의 **자식 작업 출력 캐싱** 섹션 [에서 Scott Guthrie의 블로그 게시물](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx) 의 **부분 페이지 출력 캐싱** 섹션을 참조 하십시오.

### <a name="granular-control-over-request-validation"></a>요청 유효성 검사에 대 한 세부적인 제어

ASP.NET MVC에는 XSS 및 HTML 삽입 공격 으로부터 자동으로 보호 하는 데 도움이 되는 기본 제공 요청 유효성 검사가 포함 되어 있습니다. 그러나 경우에 따라 사용자가 HTML 콘텐츠 (예: 블로그 항목 또는 CMS 콘텐츠)를 게시할 수 있도록 하려는 경우와 같이 요청 유효성 검사를 명시적으로 사용 하지 않도록 설정할 수 있습니다. 이제 모델 또는 모델에 [AllowHtml](https://msdn.microsoft.com/library/system.web.mvc.allowhtmlattribute(v=VS.98).aspx) 특성을 추가 하 여 모델 바인딩 중에 속성 별로 요청 유효성 검사를 사용 하지 않도록 설정할 수 있습니다. 요청 유효성 검사에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [Scott Guthrie의 블로그 게시물](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx)에 있는 **JavaScript 및 유효성 검사** 에 대 한 자세한 부분은 MVC 3 릴리스 후보에 있습니다.
- [MVC 3 릴리스 정보](../whitepapers/mvc3-release-notes.md)

### <a name="extensible-new-project-dialog-box"></a>확장 가능한 "새 프로젝트" 대화 상자

ASP.NET MVC 3에서 프로젝트 템플릿, 뷰 엔진 및 단위 테스트 프로젝트 프레임 워크를 **새 프로젝트** 대화 상자에 추가할 수 있습니다.

### <a name="template-scaffolding-improvements"></a>템플릿 스 캐 폴딩 기능 향상

ASP.NET MVC 3 스 캐 폴딩 템플릿에서는 모델에 대 한 기본 키 속성을 식별 하 고 이전 버전의 MVC 보다 적절 하 게 처리 하는 작업을 더 효율적으로 수행 합니다. 예를 들어 스 캐 폴딩 템플릿에서는 기본 키가 편집 가능한 폼 필드로 스 캐 폴드 되지 않도록 합니다.

기본적으로 Create 및 Edit 스 캐 폴드는 이제 `Html.TextBoxFor` 도우미 대신 `Html.EditorFor` 도우미를 사용 합니다. 이렇게 하면 **뷰 추가** 대화 상자에서 뷰를 생성할 때 데이터 주석 특성의 형태로 모델의 메타 데이터에 대 한 지원이 향상 됩니다.

### <a name="new-overloads-for-htmllabelfor-and-htmllabelformodel"></a>"Html. LabelFor" 및 "Html. LabelForModel"의 새 오버 로드

`LabelFor` 및 `LabelForModel` 도우미 메서드에 대 한 새 메서드 오버 로드가 추가 되었습니다. 새 오버 로드를 사용 하 여 레이블 텍스트를 지정 하거나 재정의할 수 있습니다.

### <a name="sessionless-controller-support"></a>Sessionless 컨트롤러 지원

ASP.NET MVC 3에서는 컨트롤러 클래스에서 세션 상태를 사용 하도록 할지 여부를 지정할 수 있으며,이 경우 세션 상태를 읽기/쓰기 또는 읽기 전용으로 설정할지 여부를 지정할 수 있습니다. 세션 없는 컨트롤러 지원에 대 한 자세한 내용은 [MVC 3 릴리스 정보](../whitepapers/mvc3-release-notes.md)를 참조 하세요.

### <a name="new-additionalmetadataattribute-class"></a>새 "AdditionalMetadataAttribute" 클래스

[Additionalmetadata](https://msdn.microsoft.com/library/system.web.mvc.additionalmetadataattribute(v=VS.98).aspx) 특성을 사용 하 여 모델 속성에 대 한 `ModelMetadata.AdditionalValues` 사전을 채울 수 있습니다. 예를 들어 뷰 모델에 관리자 에게만 표시 되어야 하는 속성이 있는 경우 다음 예제와 같이 해당 속성에 주석을 달 수 있습니다.

[!code-csharp[Main](mvc3/samples/sample4.cs)]

이 메타 데이터는 제품 뷰 모델을 렌더링할 때 모든 표시 또는 편집기 템플릿에서 사용할 수 있습니다. 메타 데이터 정보를 해석할 수 있습니다.

### <a name="accountcontroller-improvements"></a>AccountController 기능 향상

인터넷 프로젝트 템플릿의 AccountController가 크게 향상 되었습니다.

### <a name="new-intranet-project-template"></a>새 인트라넷 프로젝트 템플릿

Windows 인증을 사용 하 고 AccountController를 제거 하는 새 인트라넷 프로젝트 템플릿이 포함 되어 있습니다.
