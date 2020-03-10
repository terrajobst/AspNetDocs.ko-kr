---
uid: mvc/overview/older-versions/aspnet-mvc-4-mobile-features
title: ASP.NET MVC 4 모바일 기능 | Microsoft Docs
author: Rick-Anderson
description: 이제 Azure 웹 사이트에 ASP.NET MVC 5 모바일 웹 응용 프로그램 배포의 코드 샘플과 함께이 자습서의 MVC 5 버전이 있습니다.
ms.author: riande
ms.date: 08/15/2012
ms.assetid: 27dc4fc8-1b51-43b0-933f-fc1b52476523
msc.legacyurl: /mvc/overview/older-versions/aspnet-mvc-4-mobile-features
msc.type: authoredcontent
ms.openlocfilehash: 9716def069ca9f7115af32e16381f41bd4d13342
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468431"
---
# <a name="aspnet-mvc-4-mobile-features"></a>ASP.NET MVC 4 모바일 기능

[Rick Anderson](https://twitter.com/RickAndMSFT)

> 이제 [Azure 웹 사이트에 ASP.NET MVC 5 모바일 웹 응용 프로그램 배포](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/)의 코드 샘플과 함께이 자습서의 MVC 5 버전이 있습니다.

이 자습서에서는 ASP.NET MVC 4 웹 응용 프로그램에서 모바일 기능을 사용 하는 방법에 대 한 기본 사항을 학습 합니다. 이 자습서에서는 [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) 또는 Visual web Developer 2010 Express 서비스 팩 1 (&quot;Visual web DEVELOPER 또는 VWD&quot;)을 사용할 수 있습니다. 이미 있는 경우 Visual Studio의 professional 버전을 사용할 수 있습니다.

시작 하기 전에 아래 나열 된 필수 구성 요소를 설치 했는지 확인 합니다.

- [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) (권장) 또는 Visual Studio Web DEVELOPER Express SP1. Visual Studio 2012은 ASP.NET MVC 4를 포함 합니다. Visual Web Developer 2010를 사용 하는 경우 [ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392)를 설치 해야 합니다.

모바일 브라우저 에뮬레이터도 필요합니다. 다음을 사용할 수 있습니다.

- [Windows 7 Phone 에뮬레이터](https://msdn.microsoft.com/library/ff402563(VS.92).aspx). 이 에뮬레이터는이 자습서의 스크린 샷 대부분에서 사용 되는 에뮬레이터입니다.
- IPhone을 에뮬레이트 하도록 사용자 에이전트 문자열을 변경 합니다. [이](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) 블로그 항목을 참조 하세요.
- [Opera 모바일 에뮬레이터](http://www.opera.com/developer/tools/mobile/)
- 사용자 에이전트가 iPhone으로 설정 된 [Apple Safari](http://www.apple.com/safari/download/) . Safari의 사용자 에이전트를 "iPhone"으로 설정 하는 방법에 대 한 지침은 Alison의 블로그에서 [safari가 IE](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) 를 가장 하는 방법을 참조 하세요.

C# 소스 코드를 사용하는 Visual Studio 프로젝트를 다음 항목과 함께 사용할 수 있습니다.

- [시작 프로젝트 다운로드](https://go.microsoft.com/fwlink/?linkid=228307&amp;clcid=0x409)
- [완료 된 프로젝트 다운로드](https://go.microsoft.com/fwlink/?linkid=228306&amp;clcid=0x409)

### <a name="what-youll-build"></a>만들 내용

이 자습서에서는 [시작 프로젝트](https://go.microsoft.com/fwlink/?LinkId=228307)에 제공 된 간단한 회의 목록 응용 프로그램에 모바일 기능을 추가 합니다. 다음 스크린샷은 [Windows 7 Phone 에뮬레이터](https://msdn.microsoft.com/library/ff402563(VS.92).aspx)에 표시 된 대로 완료 된 응용 프로그램의 태그 페이지를 보여 줍니다. 키보드 입력을 단순화 하려면 [Windows Phone 에뮬레이터에 대 한 키보드 매핑](https://msdn.microsoft.com/library/ff754352(v=vs.92).aspx) 을 참조 하세요.

[![p1_Tags_CompletedProj](aspnet-mvc-4-mobile-features/_static/image2.png)](aspnet-mvc-4-mobile-features/_static/image1.png)

Internet Explorer 버전 9 또는 10, FireFox 또는 Chrome을 사용 하 여 [사용자 에이전트 문자열](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)을 설정 하 여 모바일 응용 프로그램을 개발할 수 있습니다. 다음 그림은 iPhone을 에뮬레이션 하는 Internet Explorer를 사용 하는 완료 된 자습서를 보여 줍니다. Internet Explorer F-12 개발자 도구 및 [Fiddler 도구](http://www.fiddler2.com/fiddler2/) 를 사용 하 여 응용 프로그램을 디버그할 수 있습니다.

![](aspnet-mvc-4-mobile-features/_static/image3.png)

### <a name="skills-youll-learn"></a>학습할 기술

다음 내용을 학습하게 됩니다.

- ASP.NET MVC 4 템플릿에서 HTML5 `viewport` 특성 및 적응형 렌더링을 사용 하 여 모바일 장치에서 디스플레이를 개선 하는 방법입니다.
- 모바일 관련 보기를 만드는 방법
- 사용자가 모바일 뷰와 응용 프로그램의 데스크톱 보기 간을 전환할 수 있도록 하는 보기 전환기를 만드는 방법입니다.

### <a name="getting-started"></a>시작하기

다음 링크를 사용 하 여 시작 프로젝트용 회의 목록 응용 프로그램을 다운로드 합니다. [다운로드](https://go.microsoft.com/fwlink/?LinkId=228307). 그런 다음 Windows 탐색기에서 *Mvcmobile .zip* 파일을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다. **Mvcmobile .Zip 속성** 대화 상자에서 **차단 해제** 단추를 선택 합니다. (차단 해제는 웹에서 다운로드한 *.zip* 파일을 사용하려고 할 때 발생하는 보안 경고를 막습니다.)

![p1_unBlock](aspnet-mvc-4-mobile-features/_static/image4.png)

*Mvcmobile .zip* 파일을 마우스 오른쪽 단추로 클릭 하 고 **압축 풀기** 를 선택 하 여 파일의 압축을 풉니다. Visual Studio에서 *Mvcmobile .sln* 파일을 엽니다.

CTRL + f 5를 눌러 응용 프로그램을 실행 하면 데스크톱 브라우저에 표시 됩니다. 모바일 브라우저 에뮬레이터를 시작 하 고, 회의 응용 프로그램의 URL을 에뮬레이터에 복사한 다음, **태그별로 찾아보기** 링크를 클릭 합니다. Windows Phone 에뮬레이터를 사용 하는 경우 URL 표시줄을 클릭 하 고 일시 중지 키를 눌러 키보드 액세스를 가져옵니다. 아래 이미지는 *Alltags* 뷰 ( **태그로 찾아보기**선택)를 보여 줍니다.

[![p1_browseTag](aspnet-mvc-4-mobile-features/_static/image6.png)](aspnet-mvc-4-mobile-features/_static/image5.png)

이 화면은 모바일 디바이스에서 가독성이 뛰어납니다. ASP.NET 링크를 선택 합니다.

[![p1_tagged_ASPNET](aspnet-mvc-4-mobile-features/_static/image8.png)](aspnet-mvc-4-mobile-features/_static/image7.png)

ASP.NET 태그 보기는 매우 복잡 합니다. 예를 들어 **날짜** 열은 읽기가 매우 어렵습니다. 이 자습서의 뒷부분에서는 모바일 브라우저용으로 특별히 표시 되 고 표시를 읽을 수 있도록 하는 *Alltags* 보기의 버전을 만듭니다.

참고: 현재 버그가 모바일 캐싱 엔진에 있습니다. 프로덕션 응용 프로그램의 경우 [고정 displaymodes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) nugget 패키지를 설치 해야 합니다. 해결 방법에 대 한 자세한 내용은 [ASP.NET MVC 4 Mobile 캐싱 버그 수정](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) 을 참조 하세요.

## <a name="css-media-queries"></a>CSS 미디어 쿼리

[Css 미디어 쿼리](http://www.w3.org/TR/css3-mediaqueries/) 는 미디어 유형의 css에 대 한 확장입니다. 이를 통해 특정 브라우저 (사용자 에이전트)에 대 한 기본 CSS 규칙을 재정의 하는 규칙을 만들 수 있습니다. 모바일 브라우저를 대상으로 하는 CSS에 대 한 일반적인 규칙은 최대 화면 크기를 정의 하는 것입니다. 새 ASP.NET MVC 4 인터넷 프로젝트를 만들 때 생성 된 *Content\site.xml* 파일에는 다음 미디어 쿼리가 포함 됩니다.

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample1.css)]

브라우저 창의 너비가 850 픽셀이 면이 미디어 블록 내에서 CSS 규칙을 사용 합니다. 이와 같은 CSS 미디어 쿼리를 사용 하 여 데스크톱 브라우저의 광범위 한 표시를 위해 디자인 된 기본 CSS 규칙 보다 작은 브라우저 (예: 모바일 브라우저)에서 HTML 콘텐츠를 더 잘 표시할 수 있습니다.

## <a name="the-viewport-meta-tag"></a>뷰포트 메타 태그

대부분의 모바일 브라우저는 모바일 장치의 실제 너비 보다 훨씬 큰 가상 브라우저 창 너비 ( *뷰포트*)를 정의 합니다. 이를 통해 모바일 브라우저는 전체 웹 페이지를 가상 디스플레이 안에 포함할 수 있습니다. 그러면 사용자가 관심 있는 콘텐츠를 확대할 수 있습니다. 그러나 뷰포트 너비를 실제 장치 너비로 설정 하면 콘텐츠가 모바일 브라우저에 맞게 조정 되지 않습니다.

ASP.NET MVC 4 레이아웃 파일의 뷰포트 `<meta>` 태그는 뷰포트를 장치 너비로 설정 합니다. 다음 줄에서는 ASP.NET MVC 4 레이아웃 파일의 뷰포트 `<meta>` 태그를 보여 줍니다.

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample2.html)]

## <a name="examining-the-effect-of-css-media-queries-and-the-viewport-meta-tag"></a>CSS 미디어 쿼리 및 뷰포트 메타 태그의 영향 검사

편집기에서 *Views\Shared\\_Layout* 파일을 열고 뷰포트 `<meta>` 태그를 주석으로 처리 합니다. 다음 태그는 주석 처리 된 줄을 보여 줍니다.

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample3.cshtml)]

편집기에서 *MvcMobile\Content\Site.css* 파일을 열고 미디어 쿼리의 최대 너비를 0 픽셀로 변경 합니다. 이렇게 하면 CSS 규칙이 모바일 브라우저에서 사용 되지 않습니다. 다음 줄은 수정 된 미디어 쿼리를 보여 줍니다.

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample4.css)]

변경 내용을 저장 하 고 모바일 브라우저 에뮬레이터에서 회의 응용 프로그램으로 이동 합니다. 다음 이미지에서 가장 작은 텍스트는 뷰포트 `<meta>` 태그를 제거 하는 결과입니다. Viewport `<meta>` 태그를 사용 하지 않으면 브라우저가 대부분의 모바일 브라우저에서 기본 뷰포트 너비 (850 픽셀 이상)로 확대 됩니다.

[![p1_noViewPort](aspnet-mvc-4-mobile-features/_static/image10.png)](aspnet-mvc-4-mobile-features/_static/image9.png)

변경 내용 실행 취소-레이아웃 파일에서 뷰포트 `<meta>` 태그의 주석 처리를 제거 하 고 *사이트 .css* 파일에서 미디어 쿼리를 850 픽셀로 복원 합니다. 변경 내용을 저장 하 고 모바일 브라우저를 새로 고쳐 모바일 친화적인 디스플레이가 복원 되었는지 확인 합니다.

Viewport `<meta>` 태그와 CSS 미디어 쿼리는 ASP.NET MVC 4와 관련이 없으며 모든 웹 응용 프로그램에서 이러한 기능을 활용할 수 있습니다. 그러나 이제 새 ASP.NET MVC 4 프로젝트를 만들 때 생성 되는 파일에 기본 제공 됩니다.

Viewport `<meta>` 태그에 대 한 자세한 내용은 두 개의 [뷰포트 (2 부) tale of two](http://www.quirksmode.org/mobile/viewports2.html)를 참조 하세요.

다음 섹션에서는 모바일 브라우저 전용 뷰를 제공하는 방법을 설명합니다.

## <a name="overriding-views-layouts-and-partial-views"></a>뷰, 레이아웃 및 부분 뷰 재정의

ASP.NET MVC 4의 중요 한 새로운 기능은 일반적으로, 개별 모바일 브라우저나 특정 브라우저에 대해 모바일 브라우저의 모든 보기 (레이아웃 및 부분 보기 포함)를 재정의할 수 있는 간단한 메커니즘입니다. 모바일 전용 뷰를 제공하기 위해 뷰 파일을 복사하여 파일 이름에 *.Mobile* 을 추가할 수 있습니다. 예를 들어, 모바일 *인덱스* 보기를 만들려면 *Views\Home\Index.cshtml* 을 *Views\Home\Index.Mobile.cshtml*에 복사 합니다.

이 섹션에서는 모바일 전용 레이아웃 파일을 만듭니다.

시작 하려면 *Views\Shared\\_Layout* 를 *Views\Shared\\_Layout*로 복사 합니다. *\_Layout* 을 열고 제목을 **MVC4 회의** 에서 **회의 (모바일)** 로 변경 합니다.

각 `Html.ActionLink` 호출에서 *각 링크의*"Browse by"를 제거 합니다. 다음 코드는 모바일 레이아웃 파일의 완료 된 본문 섹션을 보여 줍니다.

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample5.cshtml)]

*Views\Home\AllTags.cshtml* 파일을 *Views\Home\AllTags.Mobile.cshtml*에 복사 합니다. 새 파일을 열고 `<h2>` 요소를 "Tags"에서 "Tags (M)"으로 변경합니다.

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample6.html)]

데스크톱 브라우저와 모바일 브라우저 에뮬레이터를 사용하여 태그 페이지로 이동합니다. 모바일 브라우저 에뮬레이터에는 두 가지 변경 내용이 표시 됩니다.

[p2m_layoutTags ![](aspnet-mvc-4-mobile-features/_static/image12.png)](aspnet-mvc-4-mobile-features/_static/image11.png)

이와 달리 바탕 화면 표시는 변경 되지 않았습니다.

[![p2_layoutTagsDesktop](aspnet-mvc-4-mobile-features/_static/image14.png)](aspnet-mvc-4-mobile-features/_static/image13.png)

## <a name="browser-specific-views"></a>브라우저 관련 뷰

모바일 전용 및 데스크톱 전용 뷰 외에도 개별 브라우저를 위한 뷰를 만들 수 있습니다. 예를 들어 iPhone 브라우저 전용 보기를 만들 수 있습니다. 이 섹션에서는 iPhone 브라우저를 위한 레이아웃과 iPhone 버전의 *AllTags* 뷰를 만들어 봅니다.

*Global.asax* 파일을 열고 다음 코드를 `Application_Start` 메서드에 추가 합니다.

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample7.cs)]

이 코드는 각 수신 요청에 맞출 "iPhone"이라는 새로운 디스플레이 모드를 정의합니다. 수신 요청이 정의된 조건과 일치하는 경우(즉, 사용자 에이전트가 "iPhone" 문자열을 포함하는 경우) ASP.NET MVC는 이름에 "iPhone" 접미사가 들어 있는 뷰를 찾습니다.

코드에서 `DefaultDisplayMode`를 마우스 오른쪽 단추로 클릭하고 **확인**을 선택한 다음 `using System.Web.WebPages;`를 선택합니다. 그러면 `System.Web.WebPages` 네임스페이스에 참조가 추가되고, 여기에서 `DisplayModes` 및 `DefaultDisplayMode` 유형이 정의됩니다.

[![p2_resolve](aspnet-mvc-4-mobile-features/_static/image16.png)](aspnet-mvc-4-mobile-features/_static/image15.png)

또는 파일의 `using` 섹션에 다음 줄을 직접 추가할 수 있습니다.

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample8.cs)]

*Global.asax* 파일의 전체 내용이 아래에 나와 있습니다.

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample9.cs)]

변경 내용을 저장합니다. *MvcMobile\Views\Shared\\_Layout* 파일을 *MvcMobile\Views\Shared\\_Layout*에 복사 합니다. 새 파일을 열고 `h1` 제목을 `Conference (Mobile)`에서 `Conference (iPhone)`으로 변경 합니다.

*MvcMobile\Views\Home\AllTags.Mobile.cshtml* 파일을 *MvcMobile\Views\Home\AllTags.iPhone.cshtml*에 복사 합니다. 새 파일에서 `<h2>` 요소를 "Tags (M)"에서 "Tags (iPhone)"로 변경합니다.

애플리케이션을 실행합니다. 모바일 브라우저 에뮬레이터를 실행하고, 사용자 에이전트가 "iPhone"으로 설정되었는지 확인하고, *AllTags* 뷰로 이동합니다. 다음 스크린샷은 [Safari](http://www.apple.com/safari/download/) 브라우저에 렌더링 된 *alltags* 뷰를 보여 줍니다. [여기](https://support.apple.com/kb/DL1531)에서 Windows 용 Safari를 다운로드할 수 있습니다.

[![p2_iphoneView](aspnet-mvc-4-mobile-features/_static/image18.png)](aspnet-mvc-4-mobile-features/_static/image17.png)

이 섹션에서는 모바일 레이아웃 및 뷰를 만드는 방법과 iPhone과 같은 특정 디바이스용의 레이아웃 및 뷰를 만드는 방법을 살펴보았습니다. 다음 섹션에서는 더 강력한 모바일 보기를 위해 jQuery Mobile을 활용 하는 방법을 알아봅니다.

## <a name="using-jquery-mobile"></a>JQuery Mobile 사용

[JQuery mobile](http://jquerymobile.com/demos/1.0b3/#/demos/1.0b3/docs/about/intro.html) library는 모든 주요 모바일 브라우저에서 작동 하는 사용자 인터페이스 프레임 워크를 제공 합니다. jQuery Mobile은 CSS 및 JavaScript를 지 원하는 모바일 브라우저에 *점진적 향상 기능* 을 적용 합니다. 점진적 향상 기능을 사용 하면 모든 브라우저에서 웹 페이지의 기본 콘텐츠를 표시할 수 있을 뿐 아니라 더욱 강력한 브라우저와 장치에서 더 다양 한 디스플레이를 사용할 수 있습니다. JQuery Mobile 스타일에 포함 된 JavaScript 및 CSS 파일은 태그를 변경 하지 않고 모바일 브라우저에 맞는 많은 요소를 포함 합니다.

이 섹션에서는 jquery Mobile 및 뷰 전환기 위젯을 설치 하는 *jquery. mobile.* i n a. n a n 패키지를 설치 합니다.

시작 하려면 이전에 만든 *\\_Layout 공유* 된 *\\_Layout* 파일을 삭제 합니다.

*Views\Home\AllTags.Mobile.cshtml* 및 *Views\Home\AllTags.iPhone.cshtml* 파일의 이름을 *Views\Home\AllTags.iPhone.cshtml.hide* 및 *Views\Home\AllTags.Mobile.cshtml.hide*로 바꿉니다. 파일은 더 이상 확장명이 없습니다 *.* ASP.NET MVC 런타임에서 *alltags* 뷰를 렌더링 하는 데 사용 되지 않습니다.

다음을 수행 하 여 *jQuery. Mobile.* x NuGet 패키지를 설치 합니다.

1. **도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다.

    [![p3_packageMgr](aspnet-mvc-4-mobile-features/_static/image20.png)](aspnet-mvc-4-mobile-features/_static/image19.png)
2. **패키지 관리자 콘솔**에서 `Install-Package jQuery.Mobile.MVC -version 1.0.0`를 입력 합니다.

다음 이미지는 NuGet jQuery. Mobile. x 패키지를 통해 MvcMobile 프로젝트에 추가 되 고 변경 된 파일을 보여 줍니다. 추가 된 파일에는 파일 이름 뒤에 [추가]가 추가 됩니다. 이미지에는 *Content\images* 폴더에 추가 된 GIF 및 PNG 파일이 표시 되지 않습니다.

![](aspnet-mvc-4-mobile-features/_static/image21.png)

JQuery. Mobile. n a n.

- *응용 프로그램\_Start\BundleMobileConfig.cs* 파일은 jQuery JavaScript 및 추가 된 CSS 파일을 참조 하는 데 필요 합니다. 아래 지침을 따르고이 파일에 정의 된 모바일 번들을 참조 해야 합니다.
- jQuery 모바일 CSS 파일.
- `ViewSwitcher` 컨트롤러 위젯 (*Controllers\viewswitchercontroller.cs*).
- jQuery Mobile JavaScript 파일.
- JQuery 모바일 스타일의 레이아웃 파일 (*Views\Shared\\_Layout*).
- 각 페이지 맨 위에 있는 링크를 제공 하 여 데스크톱 보기에서 모바일 보기로 전환 하거나 그 반대로 전환 하는 MvcMobile\Views\Shared () 뷰-전환기 부분 보기 *(\\_ViewSwitcher*)입니다.
- <em>Content\images</em> 폴더의 여러<em>.png</em> 및 <em>.gif</em> 이미지 파일

*Global.asax* 파일을 열고 다음 코드를 `Application_Start` 메서드의 마지막 줄로 추가 합니다.

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample10.cs)]

다음 코드 *에서는 전체 global.asax 파일을* 보여 줍니다.

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample11.cs?highlight=26)]

> [!NOTE]
> Internet Explorer 9를 사용 하는 경우 위의 `BundleMobileConfig` 줄이 노란색 강조 표시 되지 않으면 IE의 호환성 보기 단추![(꺼짐)](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "호환성 보기 단추 (꺼짐)의 그림") 에 [있는 호환성 보기](https://windows.microsoft.com/windows7/How-to-use-Compatibility-View-in-Internet-Explorer-9)단추 그림을 클릭 하 여 호환성 보기 ![단추 (꺼짐)의 개요 그림](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "호환성 보기 단추 (꺼짐)의 그림") 에서 ![호환성 보기 단추 (설정)의 단색 그림](https://res1.windows.microsoft.com/resbox/en/Windows 7/main/156805ff-3130-481b-a12d-4d3a96470f36_14.jpg "호환성 보기 단추 (설정)의 그림")으로 아이콘을 변경 합니다. 또는 FireFox 또는 Chrome에서이 자습서를 볼 수 있습니다.

*MvcMobile\Views\Shared\\_Layout* 파일을 열고 `Html.Partial` 호출한 후에 다음 태그를 직접 추가 합니다.

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample12.cshtml)]

전체 *MvcMobile\Views\Shared\\_Layout* 파일은 다음과 같습니다.

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample13.cshtml)]

응용 프로그램을 빌드하고 모바일 브라우저 에뮬레이터에서 *Alltags* 뷰로 이동 합니다. 다음이 표시됩니다.

[![p3_afterNuGet](aspnet-mvc-4-mobile-features/_static/image23.png)](aspnet-mvc-4-mobile-features/_static/image22.png)

> [!NOTE]
> IE 또는 Chrome에 대 한 [사용자 에이전트 문자열을](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) iPhone으로 설정 하 고 F-12 개발자 도구를 사용 하 여 모바일 관련 코드를 디버그할 수 있습니다. 모바일 브라우저에서 **홈**, **스피커**, **태그**및 **날짜** 링크를 단추로 표시 하지 않는 경우 jQuery mobile 스크립트와 CSS 파일에 대 한 참조가 잘못 된 것일 수 있습니다.

스타일을 변경 하는 것 외에도 모바일 보기와 모바일 보기에서 바탕 화면 보기로 전환할 수 있는 링크가 **표시** 됩니다. **바탕 화면 보기** 링크를 선택 하면 바탕 화면 뷰가 표시 됩니다.

[![p3_desktopView](aspnet-mvc-4-mobile-features/_static/image25.png)](aspnet-mvc-4-mobile-features/_static/image24.png)

바탕 화면 보기는 모바일 보기로 직접 다시 이동 하는 방법을 제공 하지 않습니다. 이제이 문제를 해결 합니다. *Views\Shared\\_Layout* 파일을 엽니다. 페이지 `body` 요소 바로 아래에 다음 코드를 추가 합니다 .이 코드는 뷰 전환기 위젯을 렌더링 합니다.

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample14.cshtml)]

모바일 브라우저에서 *Alltags* 보기를 새로 고칩니다. 이제 데스크톱과 모바일 보기 사이를 탐색할 수 있습니다.

[![p3_desktopViewWithMobileLink](aspnet-mvc-4-mobile-features/_static/image27.png)](aspnet-mvc-4-mobile-features/_static/image26.png)

> [!NOTE]
> 디버그 참고: Views\Shared _ViewSwitcher\\의 끝에 다음 코드를 추가 하 여 브라우저를 사용 하는 경우 모바일 장치에 설정 된 사용자 에이전트 문자열을 사용 하 여 뷰를 디버그할 수 있습니다.
>
> [!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample15.cs)]
>
> *Views\Shared\\_Layout* 파일에 다음 제목을 추가 합니다.
>
> [!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample16.html)]

데스크톱 브라우저에서 *Alltags* 페이지로 이동 합니다. 뷰 전환기 위젯은 모바일 레이아웃 페이지에만 추가 되었으므로 데스크톱 브라우저에 표시 되지 않습니다. 자습서의 뒷부분에서 보기-전환기 위젯을 바탕 화면 보기에 추가 하는 방법을 확인할 수 있습니다.

[![p3_desktopBrowser](aspnet-mvc-4-mobile-features/_static/image29.png)](aspnet-mvc-4-mobile-features/_static/image28.png)

## <a name="improving-the-speakers-list"></a>발표자 목록 개선

모바일 브라우저에서 **Speakers** 링크를 선택합니다. 모바일 보기 (*Allspeakers*)가 없으므로 기본 발표자 표시 (*allspeakers*)는 모바일 레이아웃 보기 ( *\_layout.* cshtml)를 사용 하 여 렌더링 됩니다.

[![p3_speakersDeskTop](aspnet-mvc-4-mobile-features/_static/image31.png)](aspnet-mvc-4-mobile-features/_static/image30.png)

다음과 같이 *뷰\\_ViewStart* 의 `true`에 `RequireConsistentDisplayMode`를 설정 하 여 모바일 레이아웃 내에서 기본 (비모바일) 뷰를 전체적으로 렌더링 하지 않도록 설정할 수 있습니다.

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample17.cshtml)]

`RequireConsistentDisplayMode`을 `true`로 설정 하면 모바일 레이아웃 (<em>\_layout</em>)은 모바일 뷰에서만 사용 됩니다. 즉, 뷰 파일은 <em>* * ViewName</em>형식입니다<em>. 휴대폰과.)</em>모바일 레이아웃이 비모바일 보기에서 제대로 작동 하지 않는 경우 `RequireConsistentDisplayMode`를 `true` 설정 해야 할 수 있습니다. 아래 스크린샷은 `RequireConsistentDisplayMode`이 `true`으로 설정 된 경우 <em>스피커</em> 페이지가 어떻게 렌더링 되는지 보여 줍니다.

[![p3_speakersConsistent](aspnet-mvc-4-mobile-features/_static/image33.png)](aspnet-mvc-4-mobile-features/_static/image32.png)

보기 파일의 `false` `RequireConsistentDisplayMode`을 설정 하 여 뷰에서 일관 된 표시 모드를 사용 하지 않도록 설정할 수 있습니다. *Views\Home\AllSpeakers.cshtml* 파일의 다음 태그는 `false``RequireConsistentDisplayMode` 설정 합니다.

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample18.cshtml)]

## <a name="creating-a-mobile-speakers-view"></a>모바일 발표자 보기 만들기

방금 본 것처럼 *발표자* 보기는 가독성은 있지만 링크가 작고 모바일 디바이스에서 누르기 어렵습니다. 이 섹션에서는 최신 모바일 응용 프로그램 처럼 보이는 모바일 특정 *발표자* 보기를 만듭니다. 여기에는 크고 간편한 링크를 표시 하 고, 스피커를 빠르게 찾을 수 있는 검색 상자가 포함 되어 있습니다.

Allspeakers를 *allspeakers* *로 복사* 합니다. *Allspeakers* 파일을 열고 `<h2>` 제목 요소를 제거 합니다.

`<ul>` 태그에서 `data-role` 특성을 추가 하 고 해당 값을 `listview`로 설정 합니다. 다른 [`data-*` 특성과](http://html5doctor.com/html5-custom-data-attributes/)마찬가지로 `data-role="listview"`를 사용 하면 많은 목록 항목을 쉽게 탭 할 수 있습니다. 완성 된 태그는 다음과 같습니다.

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample19.cshtml)]

모바일 브라우저를 새로 고칩니다. 업데이트된 뷰는 다음과 같이 표시됩니다.

[![p3_updatedSpeakerView1](aspnet-mvc-4-mobile-features/_static/image35.png)](aspnet-mvc-4-mobile-features/_static/image34.png)

모바일 보기가 개선 되었지만 긴 스피커 목록을 탐색 하기가 어렵습니다. 이 문제를 해결 하려면 `<ul>` 태그에서 `data-filter` 특성을 추가 하 고 `true`로 설정 합니다. 아래 코드는 `ul` 태그를 보여 줍니다.

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample20.html)]

다음 그림은 페이지 맨 위에 `data-filter` 특성의 결과로 나타나는 검색 필터 상자를 보여 줍니다.

[![ps_Data_Filter](aspnet-mvc-4-mobile-features/_static/image37.png)](aspnet-mvc-4-mobile-features/_static/image36.png)

검색 상자에 각 문자를 입력 하면 jQuery Mobile에서 아래 이미지에 표시 된 것 처럼 표시 된 목록을 필터링 합니다.

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image39.png)](aspnet-mvc-4-mobile-features/_static/image38.png)

## <a name="improving-the-tags-list"></a>태그 목록 개선

기본 *발표자* 보기와 마찬가지로 *태그* 보기는 읽을 수 있지만 링크는 작고 모바일 장치에서 탭 하기 어렵습니다. 이 섹션에서는 *발표자* 보기를 수정 하는 것과 동일한 방식으로 *태그* 보기를 수정 합니다.

*Views\Home\AllTags.Mobile.cshtml.hide* 파일에 대 한 &quot;&quot; 접미사를 제거 하 여 이름을 *Views\Home\AllTags.Mobile.cshtml*로 표시 합니다. 이름을 바꾼 파일을 열고 `<h2>` 요소를 제거 합니다.

다음과 같이 `data-role` 및 `data-filter` 특성을 `<ul>` 태그에 추가 합니다.

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample21.html)]

아래 이미지는 `J`문자에 대 한 태그 페이지 필터링을 보여 줍니다.

[![p3_tags_J](aspnet-mvc-4-mobile-features/_static/image41.png)](aspnet-mvc-4-mobile-features/_static/image40.png)

## <a name="improving-the-dates-list"></a>날짜 목록 개선

*발표자* 및 *태그* 보기를 개선 한 것 처럼 *날짜* 뷰를 개선 하 여 모바일 장치에서 더 쉽게 사용할 수 있습니다.

*Views\Home\AllDates.cshtml* 파일을 *Views\Home\AllDates.Mobile.cshtml*에 복사 합니다. 새 파일을 열고 `<h2>` 요소를 제거 합니다.

다음과 같이 `<ul>` 태그에 `data-role="listview"`를 추가 합니다.

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample22.html)]

아래 이미지는 `data-role` 특성을 사용 하 여 **날짜** 페이지의 모양을 보여 줍니다.

[![p3_dates1](aspnet-mvc-4-mobile-features/_static/image43.png)](aspnet-mvc-4-mobile-features/_static/image42.png) *Views\Home\AllDates.Mobile.cshtml* 파일의 내용을 다음 코드로 바꿉니다.

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample23.cshtml)]

이 코드는 모든 세션을 일별로 그룹화 합니다. 새 날짜에 대 한 목록 구분선을 만들고 각 날짜에 대 한 모든 세션을 구분선 아래에 나열 합니다. 이 코드가 실행 될 때 표시 되는 모양은 다음과 같습니다.

[![p3_dates2](aspnet-mvc-4-mobile-features/_static/image45.png)](aspnet-mvc-4-mobile-features/_static/image44.png)

## <a name="improving-the-sessionstable-view"></a>SessionsTable 된 뷰 개선

이 섹션에서는 세션의 모바일 관련 뷰를 만듭니다. 변경 내용은 만든 다른 보기 보다 더 광범위 하 게 적용 됩니다.

모바일 브라우저에서 **스피커** 단추를 탭 한 다음 검색 상자에 `Sc`을 입력 합니다.

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image47.png)](aspnet-mvc-4-mobile-features/_static/image46.png)

**Scott Hanselman** 링크를 누릅니다.

[![p3_scottHa](aspnet-mvc-4-mobile-features/_static/image49.png)](aspnet-mvc-4-mobile-features/_static/image48.png)

여기에서 볼 수 있듯이 모바일 브라우저에서는 표시를 읽기가 어렵습니다. 날짜 열을 읽기 어려울 때 태그 열이 보기를 벗어났습니다. 이 문제를 해결 하려면 *Views\Home\SessionsTable.cshtml* 를 *Views\Home\SessionsTable.Mobile.cshtml*에 복사 하 고 파일의 내용을 다음 코드로 바꿉니다.

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample24.cshtml)]

이 코드는 대화방 및 태그 열을 제거 하 고 제목, 스피커 및 날짜를 세로로 서식 지정 하 여 모든 정보를 모바일 브라우저에서 읽을 수 있도록 합니다. 아래 이미지는 코드 변경 내용이 반영된 화면입니다.

[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image51.png)](aspnet-mvc-4-mobile-features/_static/image50.png)

## <a name="improving-the-sessionbycode-view"></a>SessionByCode 뷰 개선

마지막으로 *Sessionbycode* 뷰의 모바일 관련 뷰를 만듭니다. 모바일 브라우저에서 **스피커** 단추를 탭 한 다음 검색 상자에 `Sc`을 입력 합니다.

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image53.png)](aspnet-mvc-4-mobile-features/_static/image52.png)

**Scott Hanselman** 링크를 누릅니다. Scott Hanselman의 세션이 표시 됩니다.

[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image55.png)](aspnet-mvc-4-mobile-features/_static/image54.png)

웹 링크 **의 MS 웹 스택에 대 한 개요** 를 선택 합니다.

[![ps_love](aspnet-mvc-4-mobile-features/_static/image57.png)](aspnet-mvc-4-mobile-features/_static/image56.png)

기본 바탕 화면 보기는 문제가 없지만 향상 시킬 수 있습니다.

*Views\Home\SessionByCode.cshtml* 을 *Views\Home\SessionByCode.Mobile.cshtml* 에 복사 하 고 *Views\Home\SessionByCode.Mobile.cshtml* 파일의 내용을 다음 태그로 바꿉니다.

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample25.cshtml)]

새 태그는 `data-role` 특성을 사용 하 여 뷰의 레이아웃을 향상 시킵니다.

모바일 브라우저를 새로 고칩니다. 다음 이미지는 방금 변경한 코드가 반영된 화면입니다.

[![p3_love2](aspnet-mvc-4-mobile-features/_static/image59.png)](aspnet-mvc-4-mobile-features/_static/image58.png)

## <a name="wrapup-and-review"></a>Wrapup 및 검토

이 자습서에서는 ASP.NET MVC 4 Developer Preview의 새로운 모바일 기능을 소개 했습니다. 모바일 기능에는 다음이 포함 됩니다.

- 전역 및 개별 뷰에 대해 레이아웃, 뷰 및 부분 뷰를 재정의 하는 기능입니다.
- `RequireConsistentDisplayMode` 속성을 사용 하 여 레이아웃 및 부분 재정의 적용을 제어 합니다.
- 모바일 보기에 대 한 뷰 전환기 위젯을 바탕 화면 보기에 표시할 수도 있습니다.
- IPhone 브라우저와 같은 특정 브라우저 지원 지원

## <a name="see-also"></a>참고 항목

- [JQuery 모바일](http://jquerymobile.com) 사이트.
- [jQuery 모바일 개요](http://jquerymobile.com/demos/1.0b3/docs/about/intro.html)
- [W3C에서 권장하는 모바일 웹 애플리케이션 모범 사례](http://www.w3.org/TR/mwabp/)
- [미디어 쿼리에 대한 W3C 권장 사항](http://www.w3.org/TR/css3-mediaqueries/)
