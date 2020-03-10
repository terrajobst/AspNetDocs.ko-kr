---
uid: whitepapers/mvc4-beta-release-notes
title: ASP.NET MVC 4 | Microsoft Docs
author: rick-anderson
description: 이 문서에서는 Visual Studio 2010 용 ASP.NET MVC 4 Beta 릴리스에 대해 설명 합니다.
ms.author: riande
ms.date: 09/09/2011
ms.assetid: 666407bb-81de-4319-89ba-0302c382a208
msc.legacyurl: /whitepapers/mvc4-beta-release-notes
msc.type: content
ms.openlocfilehash: 17800dfe091bbb7afb25f7f41e3bd885b882edb0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78419843"
---
# <a name="aspnet-mvc-4"></a>ASP.NET MVC 4

> 이 문서에서는 Visual Studio 2010 용 ASP.NET MVC 4 Beta 릴리스에 대해 설명 합니다.
> 
> > [!NOTE]
> > 이는 최신 릴리스가 아닙니다. ASP.NET MVC 4 RC 릴리스 정보는 [여기](mvc4-release-notes.md)에서 확인할 수 있습니다.

- [설치 참고 사항](#_Toc303253802)
- [설명서](#_Toc303253803)
- [지원](#_Toc303253804)
- [소프트웨어 요구 사항](#_Toc303253805)
- [ASP.NET MVC 3 프로젝트를 ASP.NET MVC 4로 업그레이드](#_Toc303253806)
- [ASP.NET MVC 4 Beta의 새로운 기능](#_Toc303253807)

    - [ASP.NET Web API](#_Toc317096197)
    - [ASP.NET 단일 페이지 응용 프로그램](#_Toc317096198)
    - [기본 프로젝트 템플릿에 대 한 향상 된 기능](#_Toc303253808)
    - [모바일 프로젝트 템플릿](#_Toc303253809)
    - [디스플레이 모드](#_Toc303253810)
    - [jQuery Mobile, 뷰 전환기 및 브라우저 재정의](#_Toc303253811)
    - [Visual Studio에서 코드 생성을 위한 조리법](#_Toc303253812)
    - [비동기 컨트롤러에 대 한 작업 지원](#_Toc303253813)
    - [Azure SDK](#_Toc303253814)
    - [알려진 문제 및 주요 변경 내용](#_Toc303253815)

<a id="_Toc303253802"></a>
## <a name="installation-notes"></a>설치 참고 사항

ASP.NET MVC 4 Beta for Visual Studio 2010는 웹 플랫폼 설치 관리자를 사용 하 여 [ASP.NET mvc 4 홈 페이지](../mvc/mvc4.md) 에서 설치할 수 있습니다.

ASP.NET MVC 4 Beta를 설치 하기 전에 ASP.NET MVC 4의 이전에 설치 된 미리 보기를 제거 해야 합니다.

이 릴리스는 .NET Framework 4.5 Developer Preview와 호환 되지 않습니다. ASP.NET MVC 4 Beta를 설치 하기 전에 .NET 4.5 Developer Preview를 제거 해야 합니다.

ASP.NET MVC 4는 설치 될 수 있으며 ASP.NET MVC 3과 함께 실행할 수 있습니다.

<a id="_Toc303253803"></a>
## <a name="documentation"></a>문서화

ASP.NET MVC 문서는 다음 URL의 MSDN 웹사이트에서 제공됩니다.

[https://go.microsoft.com/fwlink/?LinkID=243043](https://go.microsoft.com/fwlink/?LinkID=243043)

ASP.NET MVC에 대 한 자습서 및 기타 정보는[https://www.asp.net/mvc/mvc4](../mvc/mvc4.md)(ASP.NET) 웹 사이트의 MVC 4 페이지 (영문)에서 사용할 수 있습니다.

<a id="_Toc303253804"></a>
## <a name="support"></a>지원

이 릴리스는 미리 보기 릴리스 이며 공식적으로 지원 되지 않습니다. 이 릴리스를 사용 하는 방법에 대 한 질문이 있는 경우 ASP.NET MVC 포럼 ([https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx))에 게시 합니다. ASP.NET 커뮤니티의 구성원이 비공식적 지원을 제공할 수 있는 경우가 많습니다.

<a id="_Toc303253805"></a>
## <a name="software-requirements"></a>소프트웨어 요구 사항

Visual Studio 용 ASP.NET MVC 4 구성 요소에는 PowerShell 2.0 및 Visual Studio 2010 서비스 팩 1 또는 Visual Web Developer Express 2010 서비스 팩 1이 필요 합니다.

<a id="_Toc303253806"></a>
## <a name="upgrading-an-aspnet-mvc-3-project-to-aspnet-mvc-4"></a>ASP.NET MVC 3 프로젝트를 ASP.NET MVC 4로 업그레이드

ASP.NET MVC 4는 동일한 컴퓨터에 ASP.NET MVC 3과 함께 설치할 수 있습니다. 그러면 ASP.NET MVC 3 응용 프로그램을 ASP.NET MVC 4로 업그레이드할 시기를 유연 하 게 선택할 수 있습니다.

가장 간단한 업그레이드 방법은 새 ASP.NET MVC 4 프로젝트를 만들고 기존 MVC 3 프로젝트의 모든 뷰, 컨트롤러, 코드 및 콘텐츠 파일을 새 프로젝트에 복사한 다음 새 프로젝트의 어셈블리 참조를 이전 프로젝트와 일치 하도록 업데이트 하는 것입니다. MVC 3 프로젝트에서 web.config 파일을 변경한 경우 이러한 변경 내용을 MVC 4 프로젝트의 web.config 파일에 병합 해야 합니다.

기존 ASP.NET MVC 3 응용 프로그램을 버전 4로 수동으로 업그레이드 하려면 다음을 수행 합니다.

1. 프로젝트의 모든 Web.config 파일 (프로젝트의 루트에 있고, Views 폴더에 있고, 프로젝트의 각 영역에 대 한 Views 폴더에 있는 프로젝트)에서 다음 텍스트의 모든 인스턴스를 바꿉니다.

    [!code-console[Main](mvc4-beta-release-notes/samples/sample1.cmd)]

    다음 텍스트를 사용 합니다.

    [!code-console[Main](mvc4-beta-release-notes/samples/sample2.cmd)]
2. 루트 Web.config 파일에서 *웹 페이지: 버전* 요소를 "2.0.0.0"으로 업데이트 하 고 값이 "true" 인 새 *PreserveLoginUrl* 키를 추가 합니다.

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample3.xml)]
3. 솔루션 탐색기에서 버전 3 DLL을 가리키는 *system.web* 에 대 한 참조를 삭제 합니다. 그런 다음, *system.web* (v 4.0.0.0)에 대 한 참조를 추가 합니다. 특히, 어셈블리 참조를 업데이트 하려면 다음과 같이 변경 해야 합니다. 세부 정보는 다음과 같습니다.

    1. 솔루션 탐색기에서 다음 어셈블리에 대 한 참조를 삭제 합니다. 

        - *System.web*(v 3.0.0.0)
        - *System.web. 웹 페이지*(v 1.0.0.0)
        - *System.web. Razor*(v 1.0.0.0)
        - *System.web. 배포*(v 1.0.0.0)
        - *System.web. 웹 페이지. Razor*(v 1.0.0.0)
    2. 다음 어셈블리에 대 한 참조를 추가 합니다. 

        - *System.web*(v 4.0.0.0)
        - *System.web. 웹 페이지*(v 2.0.0.0)
        - *System.web*(v 2.0.0.0)
        - *System.web. 배포*(v 2.0.0.0)
        - *System.web. 웹 페이지. Razor*(v 2.0.0.0)
4. 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 한 다음 프로젝트 언로드를 선택 합니다. 그런 다음 이름을 다시 마우스 오른쪽 단추로 클릭 하 고 *ProjectName*.csproj 편집을 선택 합니다.
5. *Projecttypeguids* 요소를 찾아서 {E53F8FEA-EAE0-44A6-8774-FFD645390401}을 {E3E379DF-F4C6-4180-9B81-6769533ABE47}로 바꿉니다.
6. 변경 내용을 저장 하 고 편집 중인 프로젝트 (.csproj) 파일을 닫은 다음 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 프로젝트 다시 로드를 선택 합니다.
7. 프로젝트가 이전 버전의 ASP.NET MVC를 사용 하 여 컴파일된 타사 라이브러리를 참조 하는 경우 루트 Web.config 파일을 열고 *구성* 섹션 아래에 다음 세 가지 *bindingRedirect* 요소를 추가 합니다. 

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample4.xml)]

<a id="_Toc303253807"></a>
## <a name="new-features-in-aspnet-mvc-4-beta"></a>ASP.NET MVC 4 Beta의 새로운 기능

이 섹션에서는 ASP.NET MVC 4 베타 릴리스에 도입 된 기능을 설명 합니다.

<a id="_Toc317096197"></a>
### <a name="aspnet-web-api"></a>ASP.NET Web API

이제 ASP.NET MVC 4에는 브라우저 및 모바일 장치를 비롯 한 광범위 한 클라이언트에 연결할 수 있는 HTTP 서비스를 만들기 위한 새로운 프레임 워크인 ASP.NET Web API 포함 되어 있습니다. 또한 ASP.NET Web API는 RESTful services를 빌드하기 위한 이상적인 플랫폼입니다.

ASP.NET Web API에는 다음 기능에 대 한 지원이 포함 됩니다.

- **최신 HTTP 프로그래밍 모델:** 강력한 형식의 새 HTTP 개체 모델을 사용 하 여 웹 Api에서 HTTP 요청 및 응답을 직접 액세스 하 고 조작 합니다. 동일한 프로그래밍 모델 및 HTTP 파이프라인은 새 HttpClient 형식을 통해 클라이언트에서 대칭적으로 사용할 수 있습니다.
- **경로에 대 한 완전 한 지원**: 이제 웹 api는 경로 매개 변수 및 제약 조건을 포함 하 여 항상 웹 스택의 일부가 되는 전체 경로 기능 집합을 지원 합니다. 또한 작업에 대 한 매핑에는 규칙에 대 한 모든 지원이 있으므로 클래스 및 메서드에 [HttpPost]와 같은 특성을 더 이상 적용할 필요가 없습니다.
- **콘텐츠 협상**: 클라이언트와 서버가 함께 작동 하 여 API에서 반환 되는 데이터의 올바른 형식을 결정할 수 있습니다. XML, JSON 및 폼 URL로 인코딩된 형식에 대 한 기본 지원을 제공 하며, 사용자 고유의 포맷터를 추가 하거나 기본 콘텐츠 협상 전략을 대체 하 여이 지원을 확장할 수 있습니다.
- **모델 바인딩 및 유효성 검사:** 모델 바인더는 HTTP 요청의 다양 한 부분에서 데이터를 추출 하 고 이러한 메시지 부분을 웹 API 작업에서 사용할 수 있는 .NET 개체로 변환 하는 쉬운 방법을 제공 합니다.
- **필터:** 이제 Web Api는 [권한 부여] 특성과 같은 잘 알려진 필터를 포함 하 여 필터를 지원 합니다. 작업, 권한 부여 및 예외 처리에 대 한 사용자 고유의 필터를 작성 하 고 연결할 수 있습니다.
- **쿼리 컴퍼지션:** IQueryable&lt;T&gt;반환 하기만 하면 Web API는 OData URL 규칙을 통한 쿼리를 지원 합니다.
- **향상 된 HTTP 정보 테스트:** 정적 컨텍스트 개체에서 HTTP 세부 정보를 설정 하는 대신, 이제 HttpRequestMessage 및 HttpResponseMessage의 인스턴스를 사용 하 여 Web API 작업을 수행할 수 있습니다. 이러한 개체의 제네릭 버전은 HTTP 형식 외에 사용자 지정 형식으로 작업 하는 데에도 존재 합니다.
- **DependencyResolver를 통한 제어 반전 (IoC) 향상:** Web API는 이제 MVC의 종속성 확인자에서 구현 된 서비스 로케이터 패턴을 사용 하 여 다양 한 기능에 대 한 인스턴스를 가져옵니다.
- **코드 기반 구성:** 웹 API 구성은 코드를 통해서만 수행 되며 구성 파일이 깨끗 하 게 유지 됩니다.
- **자체 호스트:** 웹 api는 전체 경로 및 Web API의 다른 기능을 계속 사용 하면서 IIS 외에도 자체 프로세스에서 호스팅될 수 있습니다.

ASP.NET Web API에 대 한 자세한 내용은 [https://www.asp.net/web-api](../web-api/index.md)를 참조 하세요.

<a id="_Toc317096198"></a>
### <a name="aspnet-single-page-application"></a>ASP.NET 단일 페이지 응용 프로그램

ASP.NET MVC 4에는 이제 JavaScript 및 Web Api를 사용 하 여 중요 한 클라이언트 쪽 상호 작용으로 단일 페이지 응용 프로그램을 빌드하는 환경에 대 한 초기 미리 보기가 포함 되어 있습니다. 이 지원에는 다음이 포함 됩니다.

- 캐시 된 데이터와의 더 많은 로컬 상호 작용을 위한 JavaScript 라이브러리 집합
- 작업 단위 및 DAL 지원에 대 한 추가 웹 API 구성 요소
- 신속 하 게 시작 하기 위해 스 캐 폴딩이 포함 된 MVC 프로젝트 템플릿

ASP.NET MVC 4의 단일 페이지 응용 프로그램 지원에 대 한 자세한 내용은 [https://www.asp.net/single-page-application](../single-page-application/index.md)를 참조 하세요.

<a id="_Toc303253808"></a>
### <a name="enhancements-to-default-project-templates"></a>기본 프로젝트 템플릿에 대 한 향상 된 기능

새 ASP.NET MVC 4 프로젝트를 만드는 데 사용 되는 템플릿이 최신 웹 사이트를 만들기 위해 업데이트 되었습니다.

![](mvc4-beta-release-notes/_static/image1.png)

외관 향상 외에도 새 템플릿에서 향상 된 기능이 있습니다. 템플릿에서는 적응 렌더링 이라는 기술을 사용 하 여 사용자 지정 없이 데스크톱 브라우저와 모바일 브라우저 모두에 적합 합니다.

![](mvc4-beta-release-notes/_static/image2.png)

작동 중인 적응 렌더링을 보려면 모바일 에뮬레이터를 사용 하거나 데스크톱 브라우저 창의 크기를 작게 조정 하면 됩니다. 브라우저 창이 충분히 작으면 페이지 레이아웃이 변경 됩니다.

기본 프로젝트 템플릿에 대 한 또 다른 향상 된 기능은 JavaScript를 사용 하 여 보다 풍부한 UI를 제공 하는 것입니다. 템플릿에 사용 되는 로그인 및 등록 링크는 jQuery UI 대화 상자를 사용 하 여 다양 한 로그인 화면을 표시 하는 방법의 예입니다.

![](mvc4-beta-release-notes/_static/image3.png)

<a id="_Toc303253809"></a>
### <a name="mobile-project-template"></a>모바일 프로젝트 템플릿

새 프로젝트를 시작 하 고 모바일 및 태블릿 브라우저용으로 특정 사이트를 만들려는 경우 새 모바일 응용 프로그램 프로젝트 템플릿을 사용할 수 있습니다. 이는 터치 최적화 UI를 빌드하기 위한 오픈 소스 라이브러리인 jQuery Mobile을 기반으로 합니다.

![](mvc4-beta-release-notes/_static/image4.png)

이 템플릿은 인터넷 응용 프로그램 템플릿과 동일한 응용 프로그램 구조를 포함 하 고 컨트롤러 코드는 거의 동일 하지만, jQuery Mobile을 사용 하 여 양호한 것으로 확인 하 고 터치 기반 모바일 장치에서 잘 작동 합니다. 모바일 UI를 구조화 하 고 스타일을 만드는 방법에 대 한 자세한 내용은 [JQuery mobile project 웹 사이트](http://jquerymobile.com/)를 참조 하세요.

모바일에 최적화 된 보기를 추가할 데스크톱 기반 사이트가 이미 있는 경우 또는 데스크톱 및 모바일 브라우저에 대해 다르게 스타일 지정 된 보기를 제공 하는 단일 사이트를 만들려는 경우에는 새 디스플레이 모드 기능을 사용할 수 있습니다. (다음 섹션을 참조하십시오.)

<a id="_Toc303253810"></a>
### <a name="display-modes"></a>디스플레이 모드

새 디스플레이 모드 기능을 사용 하면 응용 프로그램에서 요청을 수행 하는 브라우저에 따라 보기를 선택할 수 있습니다. 예를 들어 데스크톱 브라우저에서 홈 페이지를 요청 하는 경우 응용 프로그램은 Views\Home\Index.cshtml 템플릿을 사용할 수 있습니다. 모바일 브라우저에서 홈 페이지를 요청 하는 경우 응용 프로그램에서 Views\Home\Index.mobile.cshtml 템플릿이 반환 될 수 있습니다.

레이아웃 및 부분 특정 브라우저 유형에 대해 재정의할 수도 있습니다. 다음은 그 예입니다.

- Views\Shared 폴더에 \_\_레이아웃을 모두 포함 하는 경우에는 기본적으로 응용 프로그램에서 \_Layout을 사용 합니다. 모바일 브라우저 및 \_레이아웃에서 요청 하는 동안에는 응용 프로그램에서 Layout을 사용 합니다.
- 폴더에 \_MyPartial 및 \_MyPartial이 모두 포함 되어 있으면 명령 @Html.Partial("\_MyPartial")는 모바일 브라우저에서 요청 하는 동안 MyPartial를 렌더링 하 고 다른 요청 중에는 \_MyPartial를 렌더링 합니다.\_

다른 장치에 대 한 보기, 레이아웃 또는 부분 보기를 더 많이 만들려는 경우 새 *DefaultDisplayMode* 인스턴스를 등록 하 여 요청이 특정 조건에 부합 될 때 검색할 이름을 지정할 수 있습니다. 예를 들어, Global.asax 파일의 *응용 프로그램\_Start* 메서드에 다음 코드를 추가 하 여 Apple iPhone 브라우저가 요청할 때 적용 되는 표시 모드로 문자열 "iPhone"을 등록할 수 있습니다.

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample5.cs)]

이 코드가 실행 된 후 Apple iPhone 브라우저가 요청을 만들면 응용 프로그램은 Views\Shared\\_Layout (있는 경우)을 사용 합니다.

<a id="_Toc303253811"></a>
### <a name="jquery-mobile-the-view-switcher-and-browser-overriding"></a>jQuery Mobile, 뷰 전환기 및 브라우저 재정의

jQuery Mobile은 터치에 최적화 된 웹 UI를 빌드하기 위한 오픈 소스 라이브러리입니다. ASP.NET MVC 4 응용 프로그램에서 jQuery Mobile을 사용 하려는 경우 시작 하는 데 도움이 되는 NuGet 패키지를 다운로드 하 여 설치할 수 있습니다. Visual Studio 패키지 관리자 콘솔에서 설치 하려면 다음 명령을 입력 합니다.

[!code-powershell[Main](mvc4-beta-release-notes/samples/sample6.ps1)]

다음을 포함 하 여 jQuery Mobile 및 일부 도우미 파일을 설치 합니다.

- Views/Shared/\_레이아웃. Mobile. cshtml는 jQuery 모바일 기반 레이아웃입니다.
- Views/Shared/\_ViewSwitcher로 구성 된 뷰-전환기 구성 요소입니다. cshtml 부분 뷰와 ViewSwitcherController.cs controller.

패키지를 설치한 후 모바일 브라우저를 사용 하 여 응용 프로그램을 실행 하거나 (예: Firefox [사용자 에이전트 전환기](http://chrispederick.com/work/user-agent-switcher/) 추가 기능) 해당 응용 프로그램을 실행 합니다. JQuery Mobile은 레이아웃 및 스타일을 처리 하므로 페이지가 크게 달라 보입니다. 이를 활용 하려면 다음을 수행할 수 있습니다.

- 이전 [표시 모드](#_Toc303253810) (예: 모바일 브라우저용 Views\Home\Index.cshtml를 재정의 하는 Views\Home\Index.mobile.cshtml 만들기)에 설명 된 대로 모바일 관련 뷰 재정의를 만듭니다.
- [JQuery 모바일 설명서](http://jquerymobile.com/) 를 읽고 모바일 보기에서 터치 최적화 UI 요소를 추가 하는 방법에 대해 자세히 알아보세요.

모바일 최적화 웹 페이지의 규칙은 사용자가 페이지의 데스크톱 버전으로 전환할 수 있는 바탕 화면 보기 또는 전체 사이트 모드와 같은 텍스트를 포함 하는 링크를 추가 하는 것입니다. JQuery. Mobile. i n a. i n a. 이는 기본 Views\Shared\\_Layout에 사용 되며 페이지가 렌더링 될 때 다음과 같이 표시 됩니다.

![](mvc4-beta-release-notes/_static/image5.png)

방문자가 링크를 클릭 하면 동일한 페이지의 데스크톱 버전으로 전환 됩니다.

바탕 화면 레이아웃에는 기본적으로 보기 전환기가 포함 되어 있지 않으므로 방문자는 모바일 모드로 전환 하는 방법을 사용할 수 없습니다. 이를 사용 하도록 설정 하려면 *ViewSwitcher\_* 에 대 한 다음 참조를 *&lt;body&gt;* 요소 내에서 바탕 화면 레이아웃에 추가 합니다.

[!code-cshtml[Main](mvc4-beta-release-notes/samples/sample7.cshtml)]

뷰 전환기는 브라우저 재정의 라는 새로운 기능을 사용 합니다. 이 기능을 통해 응용 프로그램은 요청을 실제로 사용 하는 것과 다른 브라우저 (사용자 에이전트)에서 가져온 것 처럼 처리할 수 있습니다. 다음 표에서는 브라우저 재정의에서 제공 하는 메서드를 보여 줍니다.

| `HttpContext.SetOverriddenBrowser(userAgentString)` | 지정된 사용자 에이전트를 사용하여 요청의 실제 사용자 에이전트 값을 재정의합니다. |
| --- | --- |
| `HttpContext.GetOverriddenUserAgent()` | 요청의 사용자 에이전트 재정의 값 또는 재정의가 지정 되지 않은 경우 실제 사용자 에이전트 문자열을 반환 합니다. |
| `HttpContext.GetOverriddenBrowser()` | 현재 요청에 대해 설정 된 (실제 또는 재정의) 사용자 에이전트에 해당 하는 *HttpBrowserCapabilitiesBase* 인스턴스를 반환 합니다. 이 값을 사용 하 여 *IsMobileDevice*등의 속성을 가져올 수 있습니다. |
| `HttpContext.ClearOverriddenBrowser()` | 현재 요청에 대해 재정의된 사용자 에이전트를 제거합니다. |

브라우저 재정의는 ASP.NET MVC 4의 핵심 기능이 며, jQuery를 설치 하지 않은 경우에도 사용할 수 있습니다. 그러나 뷰, 레이아웃 및 부분 뷰 선택에만 영향을 *줍니다. ASP.NET 개체에* 종속 되는 다른 모든 기능에는 영향을 주지 않습니다.

기본적으로 사용자 에이전트 재정의는 쿠키를 사용 하 여 저장 됩니다. 데이터베이스의 경우와 같이 다른 곳에서 재정의를 저장 하려는 경우 기본 공급자 (*Browseroverridestores. Current*)를 바꿀 수 있습니다. 이 공급자에 대 한 설명서는 이후 버전의 ASP.NET MVC와 함께 제공 될 예정입니다.

<a id="_Toc303253812"></a>
### <a name="recipes-for-code-generation-in-visual-studio"></a>Visual Studio에서 코드 생성을 위한 조리법

새로운 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 여 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 피가 프레임 워크 조리법은 NuGet 패키지로 배포 되기 때문에 쉽게 소스 제어에 체크 인하고 프로젝트의 모든 개발자와 자동으로 공유 될 수 있습니다. 솔루션 별로 사용할 수도 있습니다.

<a id="_Toc303253813"></a>
### <a name="task-support-for-asynchronous-controllers"></a>비동기 컨트롤러에 대 한 작업 지원

이제 비동기 작업 메서드를 *task* 또는 task 형식의 개체를 반환 하는 단일 메서드 *&lt;actionresult&gt;* 에 쓸 수 있습니다.

예를 들어, Visual C# 5를 사용 하는 경우 (또는 [비동기 CTP](https://msdn.microsoft.com/vstudio/async.aspx)를 사용 하는 경우) 다음과 같은 비동기 작업 메서드를 만들 수 있습니다.

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample8.cs)]

이전 동작 메서드에서 *newsService* 에 *대 한 호출* 은 비동기적으로 호출 되며 스레드 풀에서 스레드를 차단 하지 않습니다.

*작업* 인스턴스를 반환 하는 비동기 작업 메서드는 시간 제한을 지원할 수도 있습니다. 작업 메서드를 취소 가능한 하려면 *CancellationToken* 형식의 매개 변수를 동작 메서드 시그니처에 추가 합니다. 다음 예제에서는 시간 제한이 2500 밀리초이 고 시간 제한이 발생 하는 경우 클라이언트에 *TimedOut* 뷰를 표시 하는 비동기 작업 메서드를 보여 줍니다.

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample9.cs)]

<a id="_Toc303253814"></a>
### <a name="azure-sdk"></a>Azure SDK

ASP.NET MVC 4 Beta는 Microsoft Azure SDK의 9 월 2011 1.5 릴리스를 지원 합니다.

<a id="_Toc303253815"></a>
## <a name="known-issues-and-breaking-changes"></a>알려진 문제 및 주요 변경 내용

- **ASP.NET MVC 4 Beta를 설치한 후에는 코드 조각 또는 형식 파일에 코드 조각 또는 JavaScript를 입력 한 후 Visual Studio 2010 서비스 팩 1 CSHTML/VBHTML 편집기의 CSHTML/VBHTML editor가 오랫동안 일시 중지 될 수 있습니다.** 이는 생성 되었으며 아직 컴파일되지 않은 ASP.NET MVC 4 응용 프로그램 에서만 발생 합니다.

    해결 방법은 프로젝트를 컴파일하여 bin 폴더의 어셈블리를 가져오는 것입니다. Bin 폴더에서 어셈블리를 제거 하는 프로젝트를 정리 하면 편집기 문제가 다시 표시 됩니다.

    이는 다음 릴리스에서 수정 될 예정입니다.
- **C#Visual Studio 11 Beta 용 프로젝트 템플릿의 Global.asax.cs에 잘못 된 연결 문자열이 포함 되어 있습니다.** Visual Studio 11 Beta에서 만든 프로젝트에 대 한 응용 프로그램\_Start 메서드에 지정 된 기본 연결에는 이스케이프 되지 않은 백슬래시 (\) 문자를 포함 하는 LocalDB 연결 문자열이 포함 되어 있습니다. 이로 인해 SqlException을 생성 하는 Entity Framework DbContext에 대 한 액세스를 시도할 때 연결 오류가 발생 합니다.

    이 문제를 해결 하려면 Global.asax.cs의 App\_Start 메서드에서 백슬래시 문자를 이스케이프 하 여 다음과 같이 읽습니다.

    [!code-csharp[Main](mvc4-beta-release-notes/samples/sample10.cs)]
- **.Net 4.5를 대상으로 하는 ASP.NET MVC 4 응용 프로그램은 .NET 4.0에서 실행 될 때 FileLoadException 어셈블리에 액세스 하려고 할 때을 throw 합니다.** .NET 4.5에서 만든 ASP.NET MVC 4 응용 프로그램에는 "파일 또는 어셈블리를 로드할 수 없습니다. Http ' 또는 해당 종속성 중 하나를 로드할 수 없습니다." 라는 FileLoadException를 생성 하는 바인딩 리디렉션이 포함 됩니다. 응용 프로그램이 .NET 4.0이 설치 된 시스템에서 실행 되는 경우 이 문제를 해결 하려면 web.config에서 다음 바인딩 리디렉션을 제거 합니다.

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample11.xml)]

    수정 된 web.config의 어셈블리 바인딩 요소는 다음과 같이 표시 됩니다.

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample12.xml)]
- <strong>Visual Basic 프로젝트의 "컨트롤러 추가" 항목 템플릿은</strong><strong>영역 내부에서</strong> 호출 될 때 잘못 된 네임 스페이스를 생성 합니다. Visual Basic를 사용 하는 ASP.NET MVC 프로젝트의 영역에 컨트롤러를 추가 하면 항목 템플릿에서 잘못 된 네임 스페이스를 컨트롤러에 삽입 합니다. 컨트롤러에서 작업으로 이동할 때 결과는 "파일을 찾을 수 없습니다" 라는 오류가 발생 합니다.  
  
  생성 된 네임 스페이스는 루트 네임 스페이스 이후의 모든 항목을 생략 합니다. 예를 들어 생성 된 네임 스페이스는 *RootNamespace* 이지만 *RootNamespace AreaName* 여야 합니다.
- **Razor 뷰 엔진의 주요 변경 내용입니다.** Razor 파서를 다시 작성 하는 과정에서 다음과 같은 형식이 *system.web*에서 제거 되었습니다. 

    - *ModelSpan*
    - *MvcVBRazorCodeGenerator*
    - *MvcCSharpRazorCodeGenerator*
    - *MvcVBRazorCodeParser*

  다음 메서드도 제거 되었습니다. 

    - *MvcCSharpRazorCodeParser (ParseInheritsStatement) ((System.web.*
    - *MvcWebPageRazorHost (DecorateCodeGenerator) (RazorCodeGenerator)*
    - *MvcVBRazorCodeParser (System.web. CodeBlockInfo)*
- **ASP.NET MVC 4 앱의 WebData 디렉터리에 WebMatrix를 포함 하는 경우 폼 인증에 대 한 URL을 사용 합니다.** 응용 프로그램에 WebData 어셈블리를 추가 하는 경우 (예를 들어, 배포 가능 종속성 추가 대화 상자를 사용할 때 "Razor 구문을 사용 하 여 ASP.NET 웹 페이지"을 선택 하는 경우)에는 기본 ASP.NET MVC 계정 컨트롤러에서 예상 하는/account/pvrn이 아닌/t r i n s/logon으로의 인증 로그인 리디렉션이 재정의 됩니다. 이 동작을 방지 하 고 web.config의 인증 섹션에 이미 지정 된 URL을 사용 하려면 PreserveLoginUrl 라는 appSetting를 추가 하 고 true로 설정 하면 됩니다. 

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample13.xml)]
- **Visual Studio 2010 및 Visual Web Developer 2010의 side-by-side 설치를 위해 ASP.NET MVC 4를 설치 하려고 하면 NuGet 패키지 관리자가 설치 되지 않습니다.** ASP.NET MVC 4를 사용 하 여 Visual Studio 2010 및 Visual Web Developer 2010을 함께 실행 하려면 두 버전의 Visual Studio가 이미 설치 된 후 ASP.NET MVC 4를 설치 해야 합니다.
- **필수 구성 요소가 이미 제거 된 경우 ASP.NET MVC 4를 제거 하는 작업이 실패 합니다.** ASP.NET MVC 4를 완전히 제거 하려면 Visual Studio를 제거 하기 전에 ASP.NET MVC 4를 제거 해야 합니다.
- **기본 Web API 프로젝트를 실행 하면 사용자가 존재 하지 않는 RegisterApis 메서드를 사용 하 여 경로를 추가 하도록 잘못 지시 하는 명령이 표시 됩니다.** ASP.NET 경로 테이블을 사용 하 여 RegisterRoutes 메서드에서 경로를 추가 해야 합니다.
- **ASP.NET MVC 4 Beta를 설치 하면 ASP.NET MVC 3 RTM 응용 프로그램이 중단 됩니다.** RTM 릴리스로 만든 ASP.NET MVC 3 응용 프로그램 (ASP.NET MVC 3 도구 업데이트 릴리스를 사용 하지 않음)은 ASP.NET MVC 4 Beta와 함께 작동 하기 위해 다음과 같이 변경 해야 합니다. 이러한 업데이트를 수행 하지 않고 프로젝트를 빌드하면 컴파일 오류가 발생 합니다. 

    **필수 업데이트**

  1. 루트 Web.config 파일에서 키 *웹 페이지: 버전* 및 값 *1.0.0.0*을 사용 하 여 새 *&lt;appSettings&gt;* 항목을 추가 합니다.

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample14.xml)]
  2. 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 한 다음 프로젝트 언로드를 선택 합니다. 그런 다음 이름을 다시 마우스 오른쪽 단추로 클릭 하 고 *ProjectName*.csproj 편집을 선택 합니다.
  3. 다음 어셈블리 참조를 찾습니다. 

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample15.xml)]

      다음으로 바꿉니다.

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample16.xml)]
  4. 변경 내용을 저장 하 고 편집 중인 프로젝트 (.csproj) 파일을 닫은 다음 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 다시 로드를 선택 합니다.
