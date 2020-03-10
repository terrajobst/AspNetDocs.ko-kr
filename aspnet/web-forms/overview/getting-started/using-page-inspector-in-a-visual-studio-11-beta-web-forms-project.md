---
uid: web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
title: ASP.NET Web Forms에서 Visual Studio 2012에 페이지 검사기 사용 | Microsoft Docs
author: rick-anderson
description: Visual Studio 2012 페이지 검사기은 통합 브라우저를 사용 하는 웹 개발 도구입니다. 통합 브라우저에서 요소를 선택 하 고 페이지 검사기 ...
ms.author: riande
ms.date: 08/15/2012
ms.assetid: 2ece0bf4-aae5-4ff4-8f62-28e0819d4f86
msc.legacyurl: /web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
msc.type: authoredcontent
ms.openlocfilehash: c165bbea505b4cb8eae1312cdd587f4ed36541a0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78464945"
---
# <a name="using-page-inspector-for-visual-studio-2012-in-aspnet-web-forms"></a>ASP.NET Web Forms에서 Visual Studio 2012용 페이지 검사기 사용

사람, Tim Am마나트 n

> Visual Studio 2012 페이지 검사기은 통합 브라우저를 사용 하는 웹 개발 도구입니다. 통합 브라우저에서 요소를 선택 하 고 페이지 검사기 요소의 원본 및 CSS를 즉시 강조 표시 합니다. 응용 프로그램의 모든 페이지를 찾아보고, 렌더링 된 태그의 소스를 빠르게 찾고, Visual Studio 환경 내에서 브라우저 도구를 바로 사용할 수 있습니다.
> 
> 이 자습서에서는 검사 모드을 사용 하도록 설정한 다음 웹 프로젝트 내에서 CSS 규칙과 텍스트를 빠르게 찾고 편집 하는 방법을 보여 줍니다. 이 자습서에서는 Web Forms 응용 프로그램 프로젝트를 사용 하지만 웹 사이트 프로젝트 및 [MVC](https://go.microsoft.com/?linkid=9802002) 응용 프로그램에 페이지 검사기를 사용할 수도 있습니다.
> 
> 이 자습서에는 다음과 같은 섹션이 있습니다.
> 
> [필수 구성 요소](#_1_prerequisites)
> 
> [웹 응용 프로그램 만들기](#_2_creating_a)
> 
> [페이지 검사기를 사용 하 여 응용 프로그램 보기](#_3_using_page)
> 
> [검사 모드 사용](#_4_inspection_mode)
> 
> [페이지 검사기를 사용 하 여 태그 변경](#_5_using_page)
> 
> [검사 모드 및 HTML 창](#_6_inspection_mode)
> 
> [스타일 창에서 CSS 변경 내용 미리 보기](#_7_previewing_css)
> 
> [CSS 자동 동기화](#css_auto_sync)
> 
> [CSS 색 선택 사용](#css_color_picker)

<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a>사전 요구 사항

- 웹 용 [Visual Studio 2012](https://www.microsoft.com/visualstudio/11) 또는 [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/downloads#express-web)

> [!NOTE]
> 최신 버전의 페이지 검사기을 다운로드 하려면 [웹 플랫폼 설치 관리자](https://go.microsoft.com/fwlink/?LinkId=255386) 를 사용 하 여 Azure SDK for .net 2.0을 설치 합니다.

페이지 검사기 Microsoft Web 개발자 도구와 함께 제공 됩니다. 최신 버전은 1.3입니다. 보유 한 버전을 확인 하려면 Visual Studio를 실행 하 고 **도움말** 메뉴에서 **정보 Microsoft Visual Studio** 를 선택 합니다.

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a>웹 응용 프로그램 만들기

먼저 페이지 검사기 사용할 웹 응용 프로그램을 만듭니다. Visual Studio에서 **파일** &gt; **새 프로젝트**를 선택 합니다. 왼쪽에서 **시각적 C#개체** 를 확장 하 고 **웹**을 선택한 다음 **ASP.NET Web Forms 응용 프로그램**을 선택 합니다.

![새 Web Forms 응용 프로그램](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image1.png)

**확인**을 클릭합니다.

응용 프로그램이 **소스** 뷰에서 열립니다.

![소스 뷰의 새 Web Forms 응용 프로그램](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image2.png)

이제 작업할 응용 프로그램이 있으므로 페이지 검사기를 사용 하 여 검사 하 고 수정할 수 있습니다.

<a id="_starting_page_inspector"></a><a id="_3_starting_page"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-view-the-application"></a>페이지 검사기를 사용 하 여 응용 프로그램 보기

다음에는 페이지 검사기를 사용 하 여 응용 프로그램을 봅니다. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 **페이지 검사기에서 보기**를 선택 합니다.

![페이지 검사기에서 보기](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image3.png)

기본적으로 페이지 검사기 처음 시작 하는 경우 Visual Studio 환경의 왼쪽에 좁은 창으로 도킹 됩니다. 왼쪽에 도킹 된 상태로 두고 사용자에 게 친숙 한 너비로 설정 하거나 위쪽, 아래쪽 또는 오른쪽의 도구 영역 중 하나에 도킹 합니다.

![페이지 검사기 도킹 위치](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image4.png)

페이지 검사기 창의 도킹을 해제 하는 경우 Visual Studio 외부 또는 두 번째 모니터 (있는 경우)에도 놓을 수 있습니다. 그러나 페이지 검사기 창이 도킹 해제 될 때 페이지 검사기와 Visual Studio 사이에서 ALT + TAB을 실행 하려면 **도구** &gt; **옵션** &gt; **환경** &gt; **탭 및 창**으로 이동 하 고, **탭 웰**에서 **부동 도구 창**이라는 확인란의 선택을 취소 합니다.

![부동 도구 창 확인란의 선택을 취소 하 고 Visual Studio와 도킹 되지 않은 페이지 검사기 창 사이에서 ALT + TAB을 선택 합니다.](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image5.png)

페이지 검사기 창의 위쪽 창에는 브라우저 창의 현재 페이지가 표시 됩니다. 아래쪽 창에는 왼쪽의 HTML 태그에 페이지가 표시 되 고 오른쪽에는 페이지의 다양 한 측면을 검사할 수 있는 탭이 표시 됩니다. 아래쪽 창은 Internet Explorer의 [F12 개발자 도구](https://msdn.microsoft.com/ie/aa740478) 와 비슷합니다. 그러나 개발자 도구와 달리 Visual Studio 내에서 페이지 검사기를 사용할 수 있습니다.

![페이지 검사기](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image6.png)

이 자습서에서는 응용 프로그램을 신속 하 게 탐색 하 고 변경 하는 데 도움이 되는 페이지 검사기 브라우저 창과 **HTML** 및 **스타일** 탭을 사용 합니다.

<a id="_4_inspection_mode"></a>
## <a name="enable-inspection-mode"></a>검사 모드 사용

다음으로 페이지 검사기 검사 모드 작동 하는 방법을 확인 합니다. 페이지 검사기 창에서 **검사** 단추를 클릭 합니다.

![요소 검사](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image7.png)

작동 중인 검사 모드를 확인 하려면 페이지 검사기 브라우저 창 내에서 페이지의 다른 부분으로 마우스를 이동 합니다. 이렇게 하면 마우스 포인터가 큼 더하기 기호로 바뀌고 아래 요소가 강조 표시 됩니다.

![Div를 마우스로 가리킵니다. 콘텐츠-래퍼](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image8.png)

마우스 포인터를 이동할 때 다음 사항에 유의 하십시오.

- **소스** 뷰의 콘텐츠가 변경 되어 페이지에서 선택한 요소에 해당 하는 태그가 표시 됩니다. 관련 태그가 강조 표시 됩니다. 소스가 다른 파일에 있는 경우 해당 파일은 관련 태그가 강조 표시 된 소스 뷰에서 열립니다.

- 페이지 검사기의 **HTML** 탭에 표시 되는 마크업도 페이지에서 선택한 요소에 해당 하는로 변경 됩니다. **HTML** 탭에서 관련 태그에 대해 간략하게 설명 합니다.

- **스타일** 탭에는 현재 선택 영역과 관련 된 CSS 규칙이 표시 됩니다.

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a>페이지 검사기를 사용 하 여 태그 변경

이제 페이지 검사기를 사용 하 여 위치가 즉시 명확 하지 않을 수 있는 태그 또는 텍스트를 찾고 변경 하는 방법을 확인할 수 있습니다.

페이지 검사기를 검사 모드에 넣고 홈 페이지의 아래쪽으로 스크롤합니다.

바닥글 영역을 입력 하는 즉시 페이지 검사기 다른 탭의 오른쪽에 있는 임시 탭의 **원본** 뷰에서 *사이트 .master* 레이아웃 파일을 열고 선택한 마스터 페이지의 섹션을 강조 표시 합니다. 이 항목에서는 처음에 열었던 것과 다른 파일에서 실제로 제공 될 수 있는 페이지에서 콘텐츠를 찾고 표시할 수 페이지 검사기 방법을 보여 줍니다.

![검사 모드에서 바닥글 강조 표시](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image9.png)

페이지 검사기 브라우저 창에서 저작권 <a id="a"> </a>표시를 사용 하 여 줄 위로 마우스 포인터를 이동 합니다.

*Site.master* 페이지에서 해당 줄이 강조 표시 됩니다.

![바닥글 저작권 선이 강조 표시 됨](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image10.png)

*사이트 마스터* 파일의 줄 끝에 일부 텍스트를 추가 합니다.

&lt;p&gt;&amp;복사 &lt;%: DateTime. Year%&gt;-My ASP.NET Application 암석 지.&lt;/p&gt;

이제 Ctrl + Alt + Enter를 누르거나 업데이트 표시줄을 클릭 하 여 페이지 검사기 브라우저 창에 결과를 표시 합니다.

![내 ASP.NET 응용 프로그램 돌!](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image11.png)

바닥글은 default.aspx 페이지에 있었지만 마스터 레이아웃 페이지에 표시 되는 것으로 확인 했을 수 있습니다. *이 페이지에서* 이를 찾을 페이지 검사기.

<a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a>검사 모드 및 HTML 창

다음으로 HTML 창 및이 창에서 요소를 매핑하는 방법에 대해 간략히 살펴봅니다.

검사 모드에 페이지 검사기을 배치 합니다.

![요소 검사](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image12.png)

"여기에 로고가 있습니다." 라는 페이지의 위쪽 부분을 클릭 합니다. 특정 요소를 자세히 검사 하 고 있으므로 마우스 포인터를 이동할 때 브라우저 창에 표시 되는 내용이 더 이상 표시 되지 않습니다.

이제 마우스 포인터를 **HTML** 창으로 이동 합니다. 마우스 포인터를 움직이면 페이지 검사기 **HTML** 창에서 요소를 윤곽선으로 표시 하 고 브라우저 창에서 해당 요소를 강조 표시 합니다.

![HTML 창](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image13.png)

이전 처럼 페이지 검사기 임시 탭에서 *site.master* 파일을 엽니다. 사이트. 마스터 탭을 클릭 하면 &lt;헤더&gt; 섹션에서 해당 태그가 강조 표시 됩니다.

![강조 표시 된 태그](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image14.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a>스타일 창에서 CSS 변경 내용 미리 보기

다음으로 페이지 검사기 **스타일** 창을 사용 하 여 CSS에 대 한 변경 내용을 미리 볼 수 있는 방법을 확인 합니다.

**검사** 단추를 클릭 하 여 검사 모드 페이지 검사기을 입력 합니다.

페이지 검사기 브라우저 창에서 **div. 콘텐츠-래퍼** 레이블이 나타날 때까지 마우스 포인터를 "홈 페이지" 섹션으로 이동 합니다.

![요소 가리키기](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image15.png)

Div. 콘텐츠-래퍼 섹션 내에서 한 번 클릭 한 다음 마우스 포인터를 **스타일** 창으로 이동 합니다. 주요. 콘텐츠-래퍼 클래스 선택기에서 배경색 속성의 확인란을 선택 취소 하 고 선택 합니다.

![배경색 지우기](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image16.png)

페이지 검사기 브라우저 창에서 변경 내용이 즉시 미리 보기를 확인 합니다.

확인란을 다시 선택 하 고 속성 값을 두 번 클릭 한 다음 `red`로 변경 합니다. 변경 내용이 즉시 표시 됩니다.

![빨강 배경색](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image17.png)

스타일 **창을 사용** 하면 스타일 시트 자체에 변경 내용을 커밋하기 전에 CSS 변경을 쉽게 테스트 하 고 미리 볼 수 있습니다.

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a>CSS Auto Sync

> [!NOTE]
> 이 기능을 사용 하려면 1.3 버전의 페이지 검사기 필요 합니다.

CSS 자동 동기화 기능을 사용 하면 CSS 파일을 직접 편집 하 고 페이지 검사기 브라우저에서 즉시 변경 내용을 볼 수 있습니다.

**검사** 를 클릭 하 여 검사 모드에 페이지 검사기을 배치 합니다.

페이지 검사기 브라우저에서 ' 홈 페이지 ' 섹션 위로 마우스 포인터를 이동 합니다. **콘텐츠-래퍼** 레이블이 나타날 때까지 이동 합니다. 한 번 클릭 하 여이 요소를 선택 합니다.

**스타일** 창에는이 요소에 대 한 모든 CSS 규칙이 표시 됩니다. 아래로 스크롤하여, 주요. 콘텐츠-래퍼 클래스 선택기를 찾습니다. "주요. 콘텐츠-래퍼"를 클릭 합니다. 페이지 검사기이 스타일 (.css)을 정의 하는 CSS 파일을 열고 해당 CSS 스타일을 강조 표시 합니다.

![CSS 파일](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image18.png)

이제 `background-color`의 값을 "red"로 변경 합니다. 변경 내용은 페이지 검사기 브라우저에 즉시 표시 됩니다.

![페이지 검사기 브라우저](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image19.png)

<a id="css_color_picker"></a>

## <a name="using-the-css-color-picker"></a>CSS 색 선택 사용

다음으로 페이지 검사기를 사용 하 여 기본 응용 프로그램에서 강조 표시 된 텍스트에 대 한 CSS를 빠르게 찾고 변경 하는 방법을 배웁니다. 이 예제에서는 파란색 강조 표시와 다른 색으로 변경 하는 것을 원하지 않기로 결정 했습니다.

**검사** 단추를 클릭 합니다.

![요소 검사](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image20.png)

페이지 검사기 브라우저 창에서 강조 표시 된 "비디오, 자습서 및 샘플" 텍스트 위로 마우스 포인터를 이동 하 여 CSS "표시" 레이블이 표시 되도록 합니다.

![Mark 요소 가리키기](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image21.png)

텍스트를 클릭 하 여 선택 합니다. 해당 CSS 표시 선택기는 **스타일** 창의 아래쪽에 표시 됩니다.

![스타일 창의 표시 선택기](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image22.png)

표시 선택기를 클릭 합니다. 그러면 웹 응용 프로그램에 대 한 *사이트 .css* 파일이 열립니다. 사이트 .css 탭을 클릭 하면 선택기의 해당 CSS가 강조 표시 됩니다.

![스타일 시트의 표시 선택기](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image23.png)

배경 색 속성을 사용 하 여 줄을 선택 하 고 제거 합니다.

이제 새 Visual Studio 2012 CSS 색 선택기를 사용 하 여 배경색 **표시** 속성의 새 색을 선택 합니다.

<a id="_using_the_visual"></a>

### <a name="using-the-visual-studio-2012-css-color-picker"></a>Visual Studio 2012 CSS 색 선택 사용

Visual Studio 2012의 CSS 편집기에는 색을 쉽게 선택 하 고 삽입할 수 있는 색 선택이 있습니다. 간단한 색 막대와 "팝업" 선택기를 통해 더욱 세밀 하 게 제어할 수 있습니다.

색 선택기는 색의 표준 색상표를 포함 하 고, 표준 색 이름, 해시 코드, RGB, RGBA, HSL 및 HSLA 색을 지원 하며, 문서에서 가장 최근에 사용한 색의 목록을 유지 관리 합니다.

배경 색 속성이 있었던 줄에서 "bc"를 입력 하 고 아래쪽 화살표를 한 번 누릅니다.

하이픈으로 구분 된 속성 (예: "배경색")에서 각 단어의 첫 번째 문자를 입력 하면 IntelliSense는 일치 하는 속성만 표시 하도록 목록을 필터링 합니다.

![Intellisense 필터링 된 값](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image24.png)

이제 콜론을 입력 합니다. 이렇게 하면 전체 배경색 속성 이름이 삽입 됩니다. **#** 또는 **rgb (** 를 입력 합니다. 그러면 색 선택 막대가 나타납니다.

![CSS 색 선택 막대입니다.](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image25.png)

색 선택 막대가 어떻게 작동 하는지 확인 하려면 마우스 포인터로 색을 클릭 하거나 아래쪽 화살표 키를 누른 다음 왼쪽 및 오른쪽 화살표 키를 사용 하 여 색을 트래버스 합니다. 색을 방문할 때 배경 색 속성에 해당 하는 값을 미리 봅니다.

![배경 색 속성 값 미리 보기](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image26.png)

이 시점에서 Enter 키를 눌러 값을 선택 하 고 세미콜론 (;) CSS 항목을 완료 합니다. 지금은 색 선택 팝업이 작동 하는 방식을 확인할 수 있도록 다음 섹션으로 이동 합니다.

#### <a name="using-the-color-picker-pop-down"></a>색 선택 팝업 사용

색 막대에 원하는 정확한 색이 없으면 색 선택 팝업을 사용할 수 있습니다.

이를 열려면 색 막대의 오른쪽 끝에 있는 이중 갈매기형 펼침 단추를 클릭 하거나 키보드에서 아래쪽 화살표를 한 번 또는 두 번 누릅니다.

![CSS 색 선택 팝업](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image27.png)

오른쪽의 세로 막대에서 색을 클릭 합니다. 이렇게 하면 주 창에 해당 색의 그라데이션이 표시 됩니다. Enter 키를 눌러 세로 막대에서 색을 직접 선택 하거나 주 창에서 아무 점이 나 클릭 하 여 더 높은 정밀도로 선택 합니다.

사용 하려는 컴퓨터 화면에 색이 있는 경우 (Visual Studio 사용자 인터페이스 내부에 있을 필요가 없음) 오른쪽 아래에 있는 스 포 이트 도구를 사용 하 여 해당 값을 캡처할 수 있습니다.

색 선택 아래쪽의 슬라이더를 움직여 색의 불투명도를 변경할 수도 있습니다. 이렇게 하면 RGBA 형식이 불투명을 나타낼 수 있기 때문에 색 값이 RGBA 값으로 변경 됩니다.

색을 선택한 후 Enter 키를 누른 후 세미콜론을 입력 하 여 *사이트 .css* 파일의 배경색 항목을 완성 합니다.

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a>페이지 검사기 업데이트 표시줄

페이지 검사기는 *사이트 .css* 파일 (또는 응용 프로그램의 모든 파일)에 대 한 변경 내용을 즉시 검색 하 고 업데이트 표시줄에 경고를 표시 합니다.

![업데이트 표시줄](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image28.png)

모든 파일을 저장 하 고 페이지 검사기 브라우저를 새로 고치려면 Ctrl + Alt + Enter를 누르거나 업데이트 표시줄을 클릭 합니다. 강조 표시 색의 변경 내용이 브라우저에 나타납니다.

![강조 색이 변경 됨](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image29.png)

<a id="_using_page_inspector_1"></a>Visual Studio 환경 내에서 바로 페이지 검사기 브라우저를 새로 고쳤습니다. 외부 브라우저 대신 페이지 검사기를 사용 하면 웹 응용 프로그램을 개발할 때 편집기를 그대로 유지할 수 있습니다.

## <a name="see-also"></a>참고 항목

[페이지 검사기 소개](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector) (Channel 9 비디오)

[페이지 검사기 오류 메시지](https://go.microsoft.com/?linkid=9813062) (MSDN)
