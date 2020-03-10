---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
title: ASP.NET 웹 페이지 소개-일관 된 레이아웃 만들기 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 레이아웃을 사용 하 여 ASP.NET 웹 페이지를 사용 하는 사이트의 페이지에 대해 일관 된 모양을 만드는 방법을 보여 줍니다. 다음을 완료 했다고 가정 합니다.
ms.author: riande
ms.date: 05/28/2015
ms.assetid: c85ec591-f8d7-4882-b763-de6ab9f3df7a
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
msc.type: authoredcontent
ms.openlocfilehash: 678eb7089e95e3d221d6b2d82034a62aefa75757
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422747"
---
# <a name="introducing-aspnet-web-pages---creating-a-consistent-layout"></a>ASP.NET 웹 페이지 소개-일관적인 레이아웃 만들기

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서에서는 *레이아웃* 을 사용 하 여 ASP.NET 웹 페이지를 사용 하는 사이트의 페이지에 대해 일관 된 모양을 만드는 방법을 보여 줍니다. [ASP.NET 웹 페이지에서 데이터베이스 데이터를 삭제](https://go.microsoft.com/fwlink/?LinkId=251584)하 여 계열을 완료 했다고 가정 합니다.
> 
> 학습할 내용:
> 
> - 레이아웃 페이지는 무엇 인가요?
> - 레이아웃 페이지를 동적 콘텐츠와 결합 하는 방법입니다.
> - 레이아웃 페이지에 값을 전달 하는 방법입니다.

## <a name="about-layouts"></a>레이아웃 정보

지금까지 만든 페이지는 모두 완전 한 독립 실행형 페이지입니다. 모두 동일한 사이트에 속하지만 공통 요소나 표준 모양을 갖지 않습니다.

대부분의 사이트에는 일관 된 모양과 레이아웃이 있습니다. 예를 들어 [Microsoft.com/web](https://www.microsoft.com/web/) 사이트로 이동 하 여이를 살펴보면 페이지가 모두 전체 레이아웃 및 시각적 테마를 준수 하는 것을 볼 수 있습니다.

![머리글, 탐색 영역, 콘텐츠 영역 및 바닥글의 레이아웃을 표시 하는 Microsoft.com/web 사이트 페이지](layouts/_static/image1.png)

이 레이아웃을 만드는 *비효율적인* 방법은 각 페이지에 개별적으로 머리글, 탐색 모음 및 바닥글을 정의 하는 것입니다. 매번 동일한 태그를 복제 합니다. 바닥글 업데이트와 같은 항목을 변경 하려면 각 페이지를 별도로 변경 해야 합니다.

*레이아웃 페이지가* 제공 되는 위치입니다. ASP.NET 웹 페이지에서 사이트의 페이지에 대 한 전체 컨테이너를 제공 하는 레이아웃 페이지를 정의할 수 있습니다. 예를 들어 레이아웃 페이지에는 머리글, 탐색 영역 및 바닥글을 포함할 수 있습니다. 레이아웃 페이지에는 주 콘텐츠가 이동 하는 자리 표시 자가 포함 되어 있습니다.

그런 다음 해당 페이지에 대 한 코드와 태그를 포함 하는 개별 콘텐츠 페이지를 정의할 수 있습니다. 콘텐츠 페이지가 완전 한 HTML 페이지가 될 필요는 없습니다. `<body>` 요소가 없어도 됩니다. 또한 콘텐츠를 표시 하려는 레이아웃 페이지를 ASP.NET 알려 주는 코드 줄이 있습니다. 이 관계가 작동 하는 방식을 대략적으로 보여 주는 그림은 다음과 같습니다.

![두 콘텐츠 페이지와 이러한 페이지에 맞는 레이아웃 페이지가 표시 된 개념적 다이어그램](layouts/_static/image2.png)

이러한 상호 작용은 동작에서 볼 때 쉽게 이해할 수 있습니다. 이 자습서에서는 레이아웃을 사용 하도록 동영상 페이지를 변경 합니다.

## <a name="adding-a-layout-page"></a>레이아웃 페이지 추가

먼저 머리글, 바닥글 및 주 콘텐츠에 대 한 영역을 사용 하 여 일반적인 페이지 레이아웃을 정의 하는 레이아웃 페이지를 만듭니다. *\_* web\ststststststststststststststststststststststststst

선행 밑줄 (`_`) 문자는 중요 합니다. 페이지 이름이 밑줄로 시작 하는 경우 ASP.NET는 해당 페이지를 브라우저에 직접 보내지 않습니다. 이 규칙을 사용 하면 사이트에 필요한 페이지를 정의할 수 있지만 사용자가 직접 요청할 수는 없습니다.

페이지의 내용을 다음과 같이 바꿉니다.

[!code-html[Main](layouts/samples/sample1.html)]

여기에서 볼 수 있듯이이 태그는 `<div>` 요소를 사용 하 여 페이지에 세 개의 섹션을 정의 하는 HTML 뿐 이며 세 개의 섹션을 저장할 `<div>` 요소가 하나 더 있습니다. 바닥글에는 약간의 Razor 코드 (`@DateTime.Now.Year`)가 포함 되어 있습니다 .이 코드는 페이지의 해당 위치에서 현재 연도를 렌더링 합니다.

*동영상 .css*이라는 스타일 시트에 대 한 링크가 있습니다. 스타일 시트는 요소의 물리적 레이아웃에 대 한 세부 정보를 정의 합니다. 잠시 후에 만듭니다.

이 *\_레이아웃* 에서 유일 하지 않은 기능은 `@Render.Body()` 줄입니다. 이 레이아웃을 다른 페이지와 병합할 때 콘텐츠가 이동 하는 자리 표시자입니다.

## <a name="adding-a-css-file"></a>.Css 파일 추가

페이지에서 요소의 실제 정렬 (즉, 모양)을 정의 하는 기본 방법은 CSS (css 스타일 시트) 규칙을 사용 하는 것입니다. 따라서 새 레이아웃에 대 한 규칙이 있는 *.css* 파일을 만듭니다.

WebMatrix에서 사이트의 루트를 선택 합니다. 그런 다음 리본의 **파일** 탭에서 **새로 만들기** 단추 아래의 화살표를 클릭 한 다음 **새 폴더**를 클릭 합니다.

![리본 메뉴의 새로 만들기 아래에 있는 ' 새 폴더 ' 옵션입니다.](layouts/_static/image3.png)

새 폴더의 이름을 *스타일*로 합니다.

![새 폴더 ' 스타일 ' 이름 지정](layouts/_static/image4.png)

새 *스타일* 폴더 내에서 *동영상이 .css*인 파일을 만듭니다.

![새 동영상 .css 파일 만들기](layouts/_static/image5.png)

새 *.css* 파일의 내용을 다음으로 바꿉니다.

[!code-css[Main](layouts/samples/sample2.css)]

이러한 CSS 규칙에 대해서는 두 가지를 제외 하 고는 다루지 않습니다. 하나는 글꼴과 크기를 설정 하는 것 외에도 규칙에서 절대 위치를 사용 하 여 머리글, 바닥글 및 주 콘텐츠 영역의 위치를 설정 하는 것입니다. CSS에 위치를 처음 접하는 경우 W3Schools 사이트에서 [Css 위치 지정](http://www.w3schools.com/css/css_positioning.asp) 자습서를 읽을 수 있습니다.

그 밖의 다른 점은 원래 *동영상. cshtml* 파일에 개별적으로 정의 된 스타일 규칙을 복사 했다는 것입니다. 이러한 규칙은 ASP.NET 웹 페이지 자습서를 [사용 하 여 데이터를 표시 하](https://go.microsoft.com/fwlink/?LinkId=251580) 는 방법을 소개 하 여 테이블에 줄무늬를 추가한 `WebGrid` 도우미 렌더링 태그를 만드는 데 사용 되었습니다. 스타일 정의에 *.css* 파일을 사용 하려는 경우 전체 사이트에 대 한 스타일 규칙을 배치할 수 있습니다.

## <a name="updating-the-movies-file-to-use-the-layout"></a>레이아웃을 사용 하도록 동영상 파일 업데이트

이제 사이트에서 기존 파일을 업데이트 하 여 새 레이아웃을 사용할 수 있습니다. *영화 cshtml* 파일을 엽니다. 맨 위에 있는 코드의 첫 번째 줄에 다음을 추가 합니다.

[!code-csharp[Main](layouts/samples/sample3.cs)]

이제 페이지는 다음과 같은 방식으로 시작 됩니다.

[!code-cshtml[Main](layouts/samples/sample4.cshtml?highlight=2)]

이 한 줄의 코드는 *동영상* 페이지가 실행 될 때 *\_Layout. cshtml* 파일과 병합 되어야 한다는 것을 ASP.NET에 지시 합니다.

이제 *동영상과* 파일은 레이아웃 페이지를 사용 하므로 *\_layout* 파일에 의해 처리 되는 *동영상. cshtml* 페이지에서 태그를 제거할 수 있습니다. `<!DOCTYPE>`, `<html>`및 `<body>` 여는 태그와 닫는 태그를 사용 합니다. 이제 *.css* 파일에 해당 규칙이 있기 때문에 표의 스타일 규칙을 포함 하는 전체 `<head>` 요소 및 해당 내용을 가져옵니다. 현재 `<h1>` 요소를 `<h2>` 요소로 변경 합니다. 레이아웃 페이지에 `<h1>` 요소가 이미 있습니다. `<h2>` 텍스트를 "동영상 나열"으로 변경 합니다.

일반적으로 콘텐츠 페이지에서 이러한 종류의 변경 작업을 수행 하지 않아도 됩니다. 레이아웃 페이지를 사용 하 여 사이트를 시작 하는 경우 이러한 모든 요소를 시작 하지 않고 콘텐츠 페이지를 만듭니다. 그러나이 경우에는 독립 실행형 페이지를 레이아웃을 사용 하는 것으로 변환 하는 것이 좋습니다. 따라서 정리가 약간 있습니다.

작업이 완료 되 면 *동영상과* 페이지는 다음과 같이 표시 됩니다.

[!code-cshtml[Main](layouts/samples/sample5.cshtml)]

### <a name="testing-the-layout"></a>레이아웃 테스트

이제 레이아웃이 어떻게 표시 되는지 확인할 수 있습니다. WebMatrix에서 *동영상과* 페이지를 마우스 오른쪽 단추로 클릭 하 고 **브라우저에서 시작**을 선택 합니다. 브라우저에 페이지가 표시 되 면 페이지는 다음과 같습니다.

![레이아웃을 사용 하 여 렌더링 된 동영상 페이지](layouts/_static/image6.png)

ASP.NET가 영화의 콘텐츠를 *\_레이아웃* 에 병합 했습니다 .이 페이지는 `RenderBody` 메서드가 인 위치에 있습니다. 물론 *\_레이아웃* 은 페이지의 모양을 정의 하는 *.css* 파일을 참조 합니다.

## <a name="updating-the-addmovie-page-to-use-the-layout"></a>레이아웃을 사용 하도록 AddMovie 페이지 업데이트

레이아웃의 실제 혜택은 사이트의 모든 페이지에 사용할 수 있다는 것입니다. *Addmovie. cshtml* 페이지를 엽니다.

*Addmovie* 페이지에는 유효성 검사 오류 메시지의 모양을 정의 하는 CSS 규칙이 원래 있던 것을 기억할 수 있습니다. 이제 사이트에 대 한 *.css* 파일이 있으므로 해당 규칙을 *.css* 파일로 이동할 수 있습니다. *Addmovie* 파일에서 제거 하 고 *동영상 .css* 파일의 아래쪽에 추가 합니다. 다음 규칙을 이동 하 고 있습니다.

[!code-css[Main](layouts/samples/sample6.css)]

이제는 *Addmovie* 에서 동일한 종류의 변경 내용을 적용 합니다. cshtml를 사용 하는 *경우, 이제* 는 `Layout="~/_Layout.cshtml;` 추가 하 고 HTML 태그는 불필요 하 게 제거 합니다. `<h1>` 요소를 `<h2>`변경 합니다. 완료 되 면 페이지는 다음 예와 같이 표시 됩니다.

[!code-cshtml[Main](layouts/samples/sample7.cshtml)]

페이지를 실행 합니다. 이제 다음 그림과 같습니다.

![레이아웃을 사용 하 여 렌더링 된 ' 동영상 추가 ' 페이지](layouts/_static/image7.png)

사이트의 페이지 ( *Editmovie. cshtml* 및 *DeleteMovie*)에 대해 비슷한 변경을 수행 하려고 합니다. 그러나 이렇게 하기 전에 레이아웃에 대 한 다른 변경을 수행 하 여 좀 더 유연 하 게 만들 수 있습니다.

## <a name="passing-title-information-to-the-layout-page"></a>레이아웃 페이지에 제목 정보 전달

사용자가 만든 *\_레이아웃. cshtml* 페이지에는 "My Movie Site"로 설정 된 `<title>` 요소가 있습니다. 대부분의 브라우저는이 요소의 내용을 탭의 텍스트로 표시 합니다.

![브라우저 탭에 표시 되는 페이지의 &lt;제목&gt; 요소](layouts/_static/image8.png)

이 제목 정보는 일반 정보입니다. 제목 텍스트를 현재 페이지에 더 구체적으로 지정 하려고 한다고 가정 합니다. (제목 텍스트는 페이지에 대 한 정보를 확인 하기 위해 검색 엔진 에서도 사용 됩니다.) *동영상과* 같은 콘텐츠 페이지에서 정보를 전달 하 고, 레이아웃 페이지로 이동한 다음 해당 정보를 사용 하 여 레이아웃 페이지에서 렌더링 되는 항목을 사용자 지정할 수 있습니다 *.*

*동영상. cshtml* 페이지를 다시 엽니다. 위쪽의 코드에서 다음 줄을 추가 합니다.

[!code-csharp[Main](layouts/samples/sample8.cs)]

`Page` 개체는 모든 *cshtml* 페이지에서 사용할 수 있으며,이 목적을 위해 페이지와 레이아웃 간에 정보를 공유 합니다.

*\_레이아웃. cshtml* 페이지를 엽니다. 이 태그와 같이 `<title>` 요소를 변경 합니다.

[!code-html[Main](layouts/samples/sample9.html)]

이 코드는 `Page.Title` 속성에 있는 모든 항목을 페이지의 해당 위치에서 렌더링 합니다.

*동영상. cshtml* 페이지를 실행 합니다. 이번에는 브라우저 탭에 `Page.Title`값으로 전달 된 내용이 표시 됩니다.

![동적으로 생성 된 제목을 보여 주는 브라우저 탭](layouts/_static/image9.png)

원하는 경우 브라우저에서 페이지 소스를 봅니다. `<title>` 요소가 `<title>List Movies</title>`으로 렌더링 되는 것을 볼 수 있습니다.

> [!TIP] 
> 
> **Page 개체입니다.**
> 
> `Page`의 유용한 기능은 동적 개체입니다. 즉, `Title` 속성이 고정 또는 예약 된 이름이 아닙니다. `Page` 개체의 값으로 *임의의* 이름을 사용할 수 있습니다. 예를 들어 `Page.CurrentName` 또는 `Page.MyPage`라는 속성을 사용 하 여 제목을 쉽게 전달할 수 있습니다. 유일한 제한 사항은 이름을 지정할 수 있는 속성에 대 한 일반 규칙을 따라야 한다는 것입니다. (예를 들어 이름에는 공백이 포함 될 수 없습니다.)
> 
> `Page` 개체를 사용 하 여 원하는 수의 값을 전달할 수 있습니다. 레이아웃 페이지에 영화 정보를 전달 하려는 경우 `Page.MovieTitle`, `Page.Genre` 및 `Page.MovieYear`와 같은 항목을 사용 하 여 값을 전달할 수 있습니다. (또는 정보를 저장 하기 위해 만든 다른 모든 이름) 매우 명백한 요구 사항은 콘텐츠 페이지 및 레이아웃 페이지에서 동일한 이름을 사용 해야 한다는 것입니다.
> 
> `Page` 개체를 사용 하 여 전달 하는 정보는 레이아웃 페이지에 표시할 텍스트로만 제한 되지 않습니다. 레이아웃 페이지에 값을 전달할 수 있습니다. 그러면 레이아웃 페이지의 코드에서 값을 사용 하 여 페이지의 섹션을 표시할지 여부를 결정 하 고 사용할 *.css* 파일 등을 지정할 수 있습니다. `Page` 개체에서 전달 하는 값은 코드에서 사용 하는 다른 값과 유사 합니다. 콘텐츠 페이지에서 값이 시작 되 고 레이아웃 페이지에 전달 되는 것입니다.

*Addmovie* 페이지를 열고 코드 맨 위에 addmovie의 제목을 제공 하는 줄을 추가 합니다 *. cshtml* 페이지:

[!code-csharp[Main](layouts/samples/sample10.cs)]

*Addmovie. cshtml* 페이지를 실행 합니다. 새 제목 표시:

![동적으로 만들어진 ' 동영상 추가 ' 제목을 보여 주는 브라우저 탭](layouts/_static/image10.png)

## <a name="updating-the-remaining-pages-to-use-the-layout"></a>나머지 페이지를 업데이트 하 여 레이아웃 사용

이제 새 레이아웃을 사용 하도록 사이트의 나머지 페이지를 완료할 수 있습니다. *Editmovie. cshtml* 및 *DeleteMovie* 를 차례로 열고 각에서 동일한 변경을 수행 합니다.

레이아웃 페이지에 연결 되는 코드 줄을 추가 합니다.

[!code-csharp[Main](layouts/samples/sample11.cs)]

페이지 제목을 설정 하는 선을 추가 합니다.

[!code-csharp[Main](layouts/samples/sample12.cs)]

또는:

[!code-csharp[Main](layouts/samples/sample13.cs)]

모든 불필요 한 HTML 태그를 제거 합니다. 기본적으로 `<body>` 요소 내에 있는 비트만 그대로 둡니다 (맨 위에 있는 코드 블록).

`<h1>` 요소를 `<h2>` 요소가 되도록 변경 합니다.

이러한 변경을 수행한 후에는 각 테스트를 테스트 하 여 제대로 표시 되 고 제목이 올바른지 확인 합니다.

## <a name="parting-thoughts-about-layout-pages"></a>레이아웃 페이지에 대 한 파팅 고가

이 자습서에서는 *\_레이아웃* 을 만들고 `RenderBody` 메서드를 사용 하 여 다른 페이지에서 콘텐츠를 병합 했습니다. 이 패턴은 웹 페이지에서 레이아웃을 사용 하는 기본 패턴입니다.

레이아웃 페이지에는 여기에 포함 되지 않은 추가 기능이 있습니다. 예를 들어 레이아웃 페이지를 중첩할 수 있습니다. 즉, 한 레이아웃 페이지에서 다른 레이아웃 페이지를 참조할 수 있습니다. 중첩 된 레이아웃은 다른 레이아웃이 필요한 사이트의 하위 섹션으로 작업 하는 경우 유용할 수 있습니다. 추가 메서드 (예: `RenderSection`)를 사용 하 여 레이아웃 페이지에서 명명 된 섹션을 설정할 수도 있습니다.

레이아웃 페이지와 *.css* 파일의 조합은 강력 합니다. 다음 자습서 시리즈에서 볼 수 있듯이, WebMatrix에서 *템플릿을*기반으로 사이트를 만들 수 있으며,이를 통해 미리 빌드된 기능이 있는 사이트를 제공 합니다. 이 템플릿은 레이아웃 페이지와 CSS를 사용 하 여 메뉴와 같은 기능을 제공 하는 사이트를 만드는 데 유용 합니다. 다음은 레이아웃 페이지와 CSS를 사용 하는 기능을 보여 주는 템플릿을 기반으로 하는 사이트의 홈 페이지 스크린샷입니다.

![헤더, 탐색 영역, 콘텐츠 영역, 옵션 섹션 및 로그인 링크를 표시 하는 WebMatrix 사이트 템플릿에서 만든 레이아웃](layouts/_static/image11.png)

## <a name="complete-listing-for-movie-page-updated-to-use-a-layout-page"></a>동영상에 대 한 목록 완료 페이지 (레이아웃 페이지를 사용 하도록 업데이트 됨)

[!code-cshtml[Main](layouts/samples/sample14.cshtml)]

## <a name="complete-page-listing-for-add-movie-page-updated-for-layout"></a>동영상 추가 페이지의 전체 페이지 목록 (레이아웃으로 업데이트 됨)

[!code-cshtml[Main](layouts/samples/sample15.cshtml)]

## <a name="complete-page-listing-for-delete-movie-page-updated-for-layout"></a>동영상 삭제 페이지에 대 한 전체 페이지 목록 (레이아웃으로 업데이트 됨)

[!code-cshtml[Main](layouts/samples/sample16.cshtml)]

## <a name="complete-page-listing-for-edit-movie-page-updated-for-layout"></a>동영상 편집 페이지의 전체 페이지 목록 (레이아웃으로 업데이트 됨)

[!code-cshtml[Main](layouts/samples/sample17.cshtml)]

## <a name="coming-up-next"></a>다음에서 시작

다음 자습서에서는 모든 사용자가 볼 수 있도록 인터넷에 사이트를 게시 하는 방법을 알아봅니다.

## <a name="additional-resources"></a>추가 리소스

- [일관적인 모양 만들기](https://go.microsoft.com/fwlink/?LinkID=202891) -레이아웃 사용에 대 한 자세한 정보를 제공 하는 문서입니다. 또한 일부 콘텐츠를 표시 하거나 숨기는 레이아웃 페이지에 값을 전달 하는 방법을 설명 합니다.
- [Razor를 사용 하는 중첩 레이아웃 페이지](http://www.mikesdotnetting.com/Article/164/Nested-Layout-Pages-with-Razor) -레이아웃 페이지를 중첩 하는 방법에 대 한 예제는 Mike brind 블로그입니다. (페이지 다운로드 포함)

> [!div class="step-by-step"]
> [이전](deleting-data.md)
> [다음](publishing.md)
