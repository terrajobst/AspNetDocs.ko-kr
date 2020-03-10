---
uid: web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
title: Visual Studio 2012에서 제공 되는 ASP.NET 및 웹 개발의 새로운 기능 | Microsoft Docs
author: rick-anderson
description: 새 버전의 Visual Studio에는 웹 기술을 사용 하는 경우 환경 및 성능을 개선 하는 데 초점을 맞춘 많은 향상 된 기능이 도입 되었습니다.
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 6d40d276-1642-4a77-b6c9-02ac914f6805
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 80c77ec65ed86b06e417d3f6ba608e404c46768b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422099"
---
# <a name="whats-new-in-aspnet-and-web-development-in-visual-studio-2012"></a>Visual Studio 2012의 새로운 ASP.NET 및 웹 개발 기능

[웹 캠프 팀](https://twitter.com/webcamps)

> 새 버전의 Visual Studio에는 웹 기술로 작업할 때 경험 및 성능을 개선 하는 데 초점을 맞춘 많은 향상 된 기능이 도입 되었습니다. CSS, JavaScript 및 HTML 용 Visual Studio 편집기는 IntelliSense 및 자동 들여쓰기와 같은 대부분의 주문형 코드 지원 기능을 포함 하도록 완전히 개선 된 되었습니다. 이제 성능, 묶음 및 축소 기능이 기본 제공 기능으로 통합 되어 페이지 로드 시간을 쉽게 줄일 수 있습니다.
> 
> Visual Studio를 사용 하면 최신 웹 사이트 기술로 작업할 수 있습니다. 브라우저 간 CSS3 코드 조각을 사용 하 여 새 HTML5 요소와 기능을 활용 하면서 클라이언트 플랫폼에 관계 없이 사이트가 작동 하는지 확인할 수 있습니다.
> 
> 이 Visual Studio 버전에서는 JavaScript 코드를 작성 하 고 프로 파일링 하는 것이 더 쉬워졌습니다. IntelliSense 목록, 통합 XML 설명서 및 탐색 기능을 이제 JavaScript 코드에서 사용할 수 있습니다. 이제 JavaScript 카탈로그를 편리 하 게 사용할 수 있습니다. 또한 스크립트를 사용 하 여 ECMAScript5 준수를 확인 하 고 초기 단계에서 구문 오류를 검색할 수 있습니다.
> 
> 마지막으로,이 Visual Studio 버전은 기본 제공 묶음 및 축소를 구현 합니다. 사이트를 더 빠르게 수행 하도록 스크립트 파일 및 스타일 시트를 압축 하 고 압축 합니다.
> 
> 이 랩에서는 원본 폴더에 제공 된 샘플 웹 응용 프로그램에 사소한 변경 사항을 적용 하 여 앞에서 설명한 향상 된 기능 및 새로운 기능을 안내 합니다.
> 
> 모든 샘플 코드와 코드 조각은 [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)에서 사용할 수 있는 웹 캠프 교육 키트에 포함 되어 있습니다.

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 연습에서는 다음을 수행 하는 방법에 대해 설명 합니다.

- CSS 편집기의 새로운 기능 및 향상 된 기능 사용
- HTML 편집기의 새로운 기능 및 향상 된 기능 사용
- JavaScript 편집기의 새로운 기능 및 향상 된 기능 사용
- 묶음 및 축소 구성 및 사용

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>사전 요구 사항

- [웹 또는 고급의 경우 2012 Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (설치 방법에 대 한 지침은 [부록 a를](#AppendixA) 참조 하세요.)
- [Windows PowerShell](https://support.microsoft.com/kb/968930/) (설치 스크립트의 경우-windows 8 및 windows Server 2008 r 2에 이미 설치 됨)
- [Internet Explorer 10](https://windows.microsoft.com/internet-explorer/products/ie/home) 또는 HTML5 호환 브라우저

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>실습

이 실습 랩에서는 다음 연습이 포함 되어 있습니다.

1. [연습 1: CSS 편집기의 새로운 기능](#Exercise1)
2. [연습 2: HTML 편집기의 새로운 기능](#Exercise2)
3. [연습 3: JavaScript 편집기의 새로운 기능](#Exercise3)
4. [연습 4: 묶음 및 축소](#Exercise4)

이 랩을 완료 하는 데 소요 되는 예상 시간: **60 분**

<a id="Exercise1"></a>

<a id="Exercise_1_Whats_New_in_the_CSS_Editor"></a>
### <a name="exercise-1-whats-new-in-the-css-editor"></a>연습 1: CSS 편집기의 새로운 기능

웹 개발자는 CSS 편집과 관련 된 많은 문제에 대해 잘 알고 있어야 합니다. CSS 스타일의 가장 큰 문제 중 하나는 브라우저 간 호환성입니다. 사이트에 스타일을 적용 한 후에는 다른 브라우저나 장치에서 열 때 다르게 표시 되는 경우가 많습니다. 따라서 이러한 시각적 문제를 해결 하는 데 상당한 시간을 할애 하 여 한 브라우저에서 작업을 수행 하는 경우 다른 브라우저에서 분리 될 수 있다는 점을 알 수 있습니다.

이제 Visual Studio에는 개발자가 CSS 스타일 시트를 효과적으로 액세스, 작업 및 구성 하는 데 도움이 되는 기능이 포함 됩니다. 이 연습을 진행 하는 동안에는 유효한 조직과 버전의 새로운 기능 뿐만 아니라 브라우저 간 호환성을 위한 CSS3 코드 조각이 제공 됩니다.

<a id="Ex1Task1"></a>

<a id="Task_1_-_New_Editor_Features"></a>
#### <a name="task-1---new-editor-features"></a>작업 1-새 편집기 기능

이 태스크에서는 CSS 편집기의 새 기능을 검색 합니다. 이 새로운 편집기는 새로운 스마트 들여쓰기, 향상 된 코드 주석 및 향상 된 IntelliSense 목록을 활용 하 여 생산성을 높이는 데 도움이 됩니다.

1. **Visual Studio** 를 시작 하 고이 랩의 **Source\WhatsNewASPNET** 폴더에 있는 **WhatsNewASPNET** 솔루션을 엽니다.
2. 솔루션 탐색기에서 **스타일** 폴더 아래에 있는 **사이트 .css** 파일을 엽니다. **텍스트 편집기** 도구가 도구 모음에 표시 되는지 확인 합니다. 이렇게 하려면 | **도구 모음** **보기** 메뉴 옵션을 선택 하 고 **텍스트 편집기** 옵션을 선택 합니다. 이 새 버전을 사용 하는 경우 **주석** 단추![(주석 단추](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image1.png))와 주석 **제거** 단추 (![주석 제거 단추](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image2.png))도 CSS 편집기에 대해 사용 하도록 설정 된 것을 알 수 있습니다.

    ![편집기 및 CSS 도구 사용](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image3.png "편집기 및 CSS 도구 사용")

    *편집기 및 CSS 도구 사용*
3. 코드를 스크롤하고 CSS 클래스 정의를 선택 합니다. **주석 (![** 주석 단추](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image4.png)) 단추를 클릭 하 여 선택한 줄을 주석 처리 합니다. 그런 다음 **주석 처리 제거** (![](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image5.png) 제거) 단추를 클릭 하 여 변경 내용을 취소 합니다.
4. **축소** (![](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image6.png) 축소)를 클릭 하 고 텍스트의 왼쪽 여백에 있는 확장 (![](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image7.png)) 단추를 **확장** 합니다. 이제 사용 하지 않는 스타일을 더 이상 사용 하지 않는 스타일을 숨길 수 있습니다.

    ![CSS 클래스 축소](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image8.png "CSS 클래스 축소")

    *CSS 클래스 축소*
5. 스마트 들여쓰기 기능이 사용 되도록 설정 되어 있는지 확인 합니다. **도구** | **옵션** 메뉴 옵션을 선택한 다음 화면의 왼쪽 창에서 **텍스트 편집기** | **CSS** | **서식 지정** 페이지를 선택 합니다. **계층적 들여쓰기** 옵션을 선택 합니다.

    ![계층적 들여쓰기 사용](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image9.png "계층적 들여쓰기 사용")

    *계층적 들여쓰기 사용*
6. 주 클래스 정의 (main)를 찾아 div 요소에 스타일을 추가 합니다. 코드가 자동으로 정렬 되어 사용자가 부모 클래스를 한눈에 찾을 수 있도록 도와줍니다.

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample1.css)]

    ![CSS의 계층적 맞춤](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image10.png "CSS의 계층적 맞춤")

    *CSS의 계층적 맞춤*
7. **Main div** 클래스 내에서 **border** 의 끝에 있는 커서를 찾고 **enter** 키를 눌러 IntelliSense 목록을 표시 합니다. **Top** 입력을 시작 하 고 입력할 때 목록이 필터링 되는 방법을 확인 합니다. 이 목록에는 word의 모든 부분에서 **위쪽** 을 포함 하는 요소가 표시 됩니다 (이전 버전의 Visual Studio에서이 목록은 용어로 *시작* 하는 항목을 기준으로 필터링 됨).

    ![CSS의 향상 된 IntelliSense](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image11.png "CSS의 향상 된 IntelliSense")

    *CSS의 향상 된 IntelliSense*

<a id="Ex1Task2"></a>

<a id="Task_2_-_The_Color_Picker"></a>
#### <a name="task-2---the-color-picker"></a>작업 2-색 선택

이 작업에서는 Visual Studio IntelliSense에 통합 된 새 CSS 색 선택을 검색 합니다.

1. **사이트 .css** 에서 헤더 클래스 정의 (. header)를 찾은 다음 **해당 코드 줄** 에서 &quot;:&quot;와 &quot;#&quot; 문자 사이의 **배경 색** 특성 옆에 커서를 놓습니다.

    ![커서 찾기](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image12.png "커서 찾기")

    *커서 찾기*
2. **콜론** (:)을 삭제 합니다. 다시 작성 하 여 색 선택기를 표시 합니다. 표시 되는 첫 번째 색은 사이트의 가장 자주 발생 하는 색입니다. 흰색을 클릭 하면 해당 HTML 색 코드 (#fff)가 스타일 시트의 현재 색 코드를 대체 합니다.

    ![색 선택](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image13.png "색 선택")

    *색 선택*
3. 색 선택에서 **확장**![(com](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image14.png)) 단추를 눌러 색 그라데이션을 표시 한 다음 그라데이션 커서를 끌어 다른 색을 선택 합니다. 그런 다음 **스 포 이트** 단추를 클릭 하 고 화면에서 색을 선택 합니다. 커서를 이동 하는 동안에는 배경 색 값이 동적으로 변경 됩니다.

    ![색 선택 그라데이션](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image15.png "색 선택 그라데이션")

    *색 선택 그라데이션*
4. **불투명도** 슬라이더에서 선택기를 막대의 가운데로 이동 하 여 불투명도를 줄입니다. 이제 배경 색 값이 RGBA로 크기를 변경 하 고 있습니다.

    ![색 선택 불투명도](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image16.png "색 선택 불투명도")

    *색 선택 불투명도*

    > [!NOTE]
    > CSS3의 RGBA (빨강, 녹색, 파랑, 알파) 색 정의를 사용 하면 단일 항목에 대 한 색 불투명도 값을 정의할 수 있습니다. **불투명** 과 달리, RGBA 색 **-** 유사한 CSS 특성도 최신 브라우저와 호환 됩니다.

<a id="Ex1Task3"></a>

<a id="Task_3_-_CSS_Compatible_Code_Snippets"></a>
#### <a name="task-3---css-compatible-code-snippets"></a>작업 3-CSS 호환 코드 조각

이 작업에서는 브라우저 간 호환 CSS3 코드 조각을 사용 하 여 웹 사이트에서 일부 기능을 구현 하는 방법에 대해 설명 합니다.

1. **사이트 .css** 파일에서 **헤더** css 클래스 정의 (. header)를 찾고 커서를 **/\*테두리 반경\*/** 자리 표시자에 배치 하 여 새 조각을 추가 합니다. **Enter** 키를 눌러 IntelliSense 목록을 표시 하 고 **radius** 를 입력 하 여 목록을 필터링 합니다. 두 번 클릭 하 여 목록에서 **테두리-반경** 옵션을 선택한 다음 **tab** 키를 눌러 코드 조각을 삽입 합니다. 그런 다음 반경 크기를 픽셀 단위로 입력 하 고 **enter**키를 누릅니다. 예를 들어 **15px**를 입력 합니다.

    이 코드 조각에서 추가 된 CSS3 특성은 Mozilla 및 WebKit 기반 브라우저를 포함 하 여 대부분의 HTML5 규정 준수 브라우저에서 둥근 테두리를 렌더링 합니다.

    ![테두리-반지름 코드 조각 사용](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image17.png "테두리-반지름 코드 조각 사용")

    *테두리-반지름 코드 조각 사용*
2. 페이지 스타일 (페이지)에 같은 **테두리** 조각을 적용 합니다.

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample2.css)]
3. **F5** 키를 눌러 솔루션을 실행합니다. 이제 각 페이지의 테두리가 둥근 모양입니다.

    ![모퉁이가 둥근 모퉁이](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image18.png "모퉁이가 둥근 모퉁이")

    *모퉁이가 둥근 모퉁이*
4. 브라우저를 닫고 Visual Studio로 돌아갑니다.
5. **Styles** 폴더 아래에 있는 **사용자 지정 .css** 파일을 열고 **div. images ul imimg** 클래스 정의에 커서를 놓습니다.
6. Enter 키를 눌러 IntelliSense 목록을 표시 하 고 **box-shadow** 를 입력 한 다음 **tab** 키를 두 번 눌러 클래스 정의 내부에 기본 그림자 코드 조각을 삽입 합니다. 그림자 값을 **10px 10px 5px #888**로 설정 합니다. 그런 다음 **border-radius** 를 입력 하 고 코드 조각을 삽입 합니다. 반경 크기를 설정 하려면 **15px** 를 입력 하 **고 enter 키를 누릅니다.**

    ![그림자가 있는 둥근 모퉁이](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image19.png "그림자가 있는 둥근 모퉁이")

    *그림자가 있는 둥근 모퉁이*

    > [!NOTE]
    > 지금은 Mozilla 및 Webkit (Chrome, Safari, Konkeror) 브라우저를 지원 하기 위해 해당 접두사 (moz, webkit, o)를 사용 하 여 섀도 특성이 삽입 됩니다.
7. 새 클래스 div를 만듭니다 **. 이미지 ul li img: div를 마우스로 가리키면** **ul li img** 클래스 정의가 중괄호 안에 커서를 놓습니다 **.**

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample3.css)]
8. Transform **을 입력 하** 고 **tab** 키를 두 번 눌러 변환 코드 조각을 삽입 합니다. 그런 다음 **회전 (-15deg)** 을 입력 하 여 이미지를 가리킬 때 회전 각도 값을 변경 합니다.

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample4.css)]
9. **F5** 키를 눌러 솔루션을 실행 하 고 CSS3 페이지로 이동 합니다. 이미지에 모퉁이가 둥근 모퉁이 및 상자 그림자가 있습니다. 이미지 위로 마우스를 가져가면 회전을 시청 합니다.

    ![이미지를 회전 하는 조각 변환](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image20.png "이미지를 회전 하는 조각 변환")

    *이미지를 회전 하는 조각 변환*

    > [!NOTE]
    > Internet Explorer 10을 사용 하 고 그림자를 볼 수 없는 경우 문서 모드가 IE10 표준으로 설정 되어 있는지 확인 합니다. **F12** 키를 눌러 Internet Explorer 개발자 도구를 열고 **문서 모드** 를 클릭 하 여 IE10 표준으로 변경 합니다.

    ![about-us](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image21.png)

<a id="Exercise2"></a>

<a id="Exercise_2_Whats_New_in_the_HTML_Editor"></a>
### <a name="exercise-2-whats-new-in-the-html-editor"></a>연습 2: HTML 편집기의 새로운 기능

Visual Studio에는 향상 된 HTML 편집기가 있습니다. 이 버전에 포함 된 향상 된 기능 중 일부는 HTML 문서, HTML5 조각, HTML 시작 및 끝 태그 일치 및 HTML 유효성 검사에서 스마트 들여쓰기입니다. 이 연습을 수행 하는 동안 웹 사이트 태그에서 작업 하는 경우 이러한 변경 내용이 능숙를 어떻게 개선 하는지 확인할 수 있습니다.

CSS 편집기와 마찬가지로 HTML 편집기도 개선 되었습니다. 이러한 향상 된 기능 중 대부분은 웹 개발자의 작업을 용이 하 게 하는 작은 규모입니다. HTML 문서 DOCTYPE을 대상으로 하는 편집 및 유효성 검사를 수행할 때 HTML5, 스마트 들여쓰기, 일치 하는 시작 및 끝 태그에 대 한 추가 코드 조각 같은 항목은 이러한 향상 된 기능 중 일부입니다

<a id="Ex2Task1"></a>

<a id="Task_1_-_Improved_DOCTYPE_Validation"></a>
#### <a name="task-1---improved-doctype-validation"></a>작업 1-향상 된 DOCTYPE 유효성 검사

이제 HTML 편집기는 마스터 페이지에 정의 되어 있는 경우에도 페이지의 DOCTYPE을 확인할 수 있습니다. 페이지의 DOCTYPE에 따라 HTML 편집기는 올바른 규칙 집합을 사용 하 여 유효성을 검사 하 고 DOCTYPE 요소를 고려 하 여 IntelliSense 목록을 필터링 합니다.

이 태스크에서는 페이지의 DOCTYPE을 변경 하 여 HTML 편집기 동작을 적절 하 게 변경 하는 방법을 확인 합니다.

1. 아직 열지 않은 경우 **Visual Studio** 를 시작 하 고이 랩의 **Source\WhatsNewASPNET** 폴더에 있는 **WhatsNewASPNET** 솔루션을 엽니다.
2. **사이트 마스터** 페이지를 엽니다.
3. 유효성 검사 도구 모음에 대 한 대상 스키마를 확인 합니다. HTML 편집기의 동작 (유효성 검사, IntelliSense 등)이 선택한 Doctype에 맞게 올바르게 변경 됩니다.

    ![HTML 소스 편집 도구 모음에서 Doctype 사용](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image22.png "HTML 소스 편집 도구 모음에서 Doctype 사용")

    *HTML 소스 편집 도구 모음에서 Doctype 사용*
4. 대상 스키마를 HTML 4.01로 변경 합니다.

    ![HTML 소스 편집 도구 모음의 Doctype 변경](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image23.png "HTML 소스 편집 도구 모음의 Doctype 변경")

    *HTML 소스 편집 도구 모음의 Doctype 변경*
5. **Body** 요소 아래에 커서를 놓고 HTML5 요소의 이름 (예: **비디오**)을 입력 합니다. IntelliSense 목록에서 요소를 사용할 수 없습니다.

    ![나열 되지 않은 HTML5 요소](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image24.png "나열 되지 않은 HTML5 요소")

    *나열 되지 않은 HTML5 요소*
6. 유효성 검사 도구 모음의 대상 스키마에 대 한 변경 내용을 취소 하 고 드롭다운 목록에서 DOCTYPE: XHTML5를 선택 합니다.

    ![HTML 소스 편집 도구 모음에서 Doctype 사용](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image25.png "HTML 소스 편집 도구 모음에서 Doctype 사용")

    *HTML 원본 편집 도구 모음의 Doctype 다시 설정*
7. **Body** 요소 아래에 커서를 놓고 HTML5 요소를 다시 입력 하기 시작 합니다 (예: **비디오**). 이제는 HTML5 요소를 IntelliSense 목록에서 사용할 수 있습니다.

    ![표시 되는 HTML5 요소](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image26.png "표시 되는 HTML5 요소")

    *표시 되는 HTML5 요소*

<a id="Ex2Task2"></a>

<a id="Task_2_-_StartEnd_Tags_Automatic_Update"></a>
#### <a name="task-2---startend-tags-automatic-update"></a>작업 2-시작/끝 태그 자동 업데이트

이제 Visual Studio는 편집 중인 요소의 HTML 여는 태그 또는 닫는 태그를 서로 일치 하도록 업데이트 합니다. 이 새로운 기능을 통해 HTML 태그를 편집할 때 생산성을 향상 시킬 수 있습니다.

1. **Default.aspx 페이지에서** 제목이 있는 **H3** 요소를 추가 합니다 (예: Visual Studio 2012 암석 지 어!).

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample5.aspx)]
2. **H3** 태그를 변경 하 고 **H2** 또는 **H1을 입력 합니다.**

    끝 태그가 자동으로 업데이트 됩니다. 또한 끝 태그를 수정 하 여 시작 태그가 그에 따라 업데이트 되는 것을 볼 수 있습니다.

    ![끝 태그의 자동 업데이트](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image27.png "끝 태그의 자동 업데이트")

    *끝 태그의 자동 업데이트*

<a id="Ex2Task3"></a>

<a id="Task_3_-_New_HTML5_Code_Snippets"></a>
#### <a name="task-3---new-html5-code-snippets"></a>작업 3-새 HTML5 코드 조각

이제 Visual Studio에는 여러 HTML5 코드 조각이 포함 되어 있습니다. 이 작업에서는 다음 코드 조각 중 일부를 사용 합니다.

1. 이름이 **audio** 인 새 폴더를 웹 사이트 폴더의 루트에 추가 합니다. Windows 탐색기를 열고 오디오 파일을 **WhatsNewASPNET** 솔루션의 **audio** 폴더에 복사 합니다.
2. **Default.aspx 페이지에서** Web11 암석 지에서 커서를 찾습니다. 헤더. **Audio** 를 입력 하 고 tab 키를 누릅니다.

    새 HTML 편집기에는 HTML5 콘텐츠에 대 한 코드 조각이 포함 되어 있습니다. HTML5 코드 조각을 사용 하도록 설정 하려면 적절 한 DOCTYPE 정의를 사용 해야 합니다.

    ![HTML5 코드 조각 삽입](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image28.png "HTML5 코드 조각 삽입")

    *HTML5 코드 조각 삽입*
3. 기존 오디오 파일을 가리키도록 오디오 소스를 업데이트 합니다.

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample6.aspx)]

    > [!NOTE]
    > 오디오 파일을 솔루션에 추가 해야 합니다.
4. **F5** 키를 눌러 사이트를 실행 하 고 오디오를 재생 합니다.

    ![오디오 컨트롤 실행](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image29.png "오디오 컨트롤 실행")

    *오디오 컨트롤 실행*

    > [!NOTE]
    > 비디오, 그림 등 Visual Studio에 포함 된 추가 코드 조각을 사용해 볼 수도 있습니다.
5. 이제 페이지의 일부에 컨트롤을 삽입 해 봅니다. 예를 들어 **GridView** 컨트롤을 삽입 하려고 하지만 **&lt;눈금선를** 입력 하는 대신 **&lt;GV**를 입력 하기 시작 합니다. IntelliSense 목록에 **asp: GridView** 컨트롤이 표시 됩니다.

    HTML 편집기의 IntelliSense는 이제 부분 일치 (용어를 포함 하는 모든 요소 검색) 뿐만 아니라 부분 일치 검색을 제공 합니다.

    ![IntelliSense 목록을 사용 하 여 GridView 삽입](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image30.png "IntelliSense 목록을 사용 하 여 GridView 삽입")

    *IntelliSense 목록을 사용 하 여 GridView 삽입*

    **&lt;grid** 를 입력 하면 용어와 일치 하는 항목이 모두 표시 되지만 Visual Studio에서 **gridview** 컨트롤을 제안 합니다.

    ![IntelliSense 목록과 부분 일치를 사용 하 여 GridView 삽입](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image31.png "IntelliSense 목록과 부분 일치를 사용 하 여 GridView 삽입")

    *IntelliSense 목록과 부분 일치를 사용 하 여 GridView 삽입*

<a id="Ex2Task4"></a>

<a id="Task_4_-_HTML_Editor_Smart_Tags"></a>
#### <a name="task-4---html-editor-smart-tags"></a>작업 4-HTML 편집기 스마트 태그

HTML 편집기의 또 다른 개선 사항은 스마트 태그 기능입니다. 스마트 태그를 사용 하면 컨트롤 단위로 일반적인 개발 작업 또는 반복적인 개발 작업을 쉽게 수행할 수 있습니다. Html 디자이너에서는이 기능을 이미 사용할 수 있었지만 HTML 편집기에서는 사용할 수 없습니다.

1. **Site.master** 를 열고 **asp: Menu** 요소를 찾습니다. 시작 태그에 커서를 놓고 요소의 아래쪽에 작은 문자 모양이 표시 되는지 확인 하 고 클릭 하 여 스마트 작업 메뉴를 엽니다. 메뉴 컨트롤과 관련 된 일부 작업에 빠르게 액세스할 수 있습니다.

    ![메뉴 컨트롤에 대 한 스마트 작업](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image32.png "메뉴 컨트롤에 대 한 스마트 작업")

    *메뉴 컨트롤에 대 한 스마트 작업*

<a id="Ex2Task5"></a>

<a id="Task_5_-_Smart_Indentation"></a>
#### <a name="task-5---smart-indentation"></a>작업 5-스마트 들여쓰기

HTML의 모범 사례 중 하나는 코드를 읽을 수 있도록 중첩 된 요소를 들여쓰는 것입니다. Visual Studio 2012에서는 코드를 작성 하는 동안 편집기에서 요소를 자동으로 들여씁니다.

> [!NOTE]
> 이전 버전의 Visual Studio에서는 스마트 들여쓰기가 XML 편집기에서 사용할 수 있지만 HTML 편집기에서는 사용할 수 없습니다.

1. HTML 편집기의 들여쓰기 구성이 스마트 들여쓰기로 설정 되었는지 확인 합니다. 이렇게 하려면 도구를 선택 합니다. **| 옵션** 메뉴 옵션을 선택 하 고 **텍스트 편집기를 선택 합니다. HTML |** 화면의 왼쪽 창에 있는 탭 페이지 스마트 들여쓰기 옵션을 선택 합니다.

    ![HTML 편집기 설정](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image33.png "HTML 편집기 설정")

    *HTML 편집기 설정*
2. **Default.aspx 페이지에서** audio 요소 아래의 모든 콘텐츠를 제거 합니다.
3. 열린 **오디오** 요소의 끝에 커서를 놓고 **enter 키**를 누릅니다.

    커서의 새 위치에는 추가 들여쓰기 수준이 있습니다.

    ![HTML 편집기의 스마트 들여쓰기](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image34.png "HTML 편집기의 스마트 들여쓰기")

    *HTML 편집기의 스마트 들여쓰기*
4. 제거한 콘텐츠를 사용 하 여 audio 태그를 복원 하거나 변경 내용을 저장 하지 않고 default.aspx를 닫습니다 **.**

<a id="Ex2Task6"></a>

<a id="Task_6_-_Extract_to_User_Control"></a>
#### <a name="task-6---extract-to-user-control"></a>작업 6-사용자 정의 컨트롤로 추출

코드의 일부를 함수로 추출 하는 것과 같이 Visual Studio에 포함 된 리팩터링 도구는 향상 된 기능을 활용 하 고 기존 코드를 리팩터링할 수 있는 훌륭한 기능입니다. ASP.NET 페이지에 해당 하는는 사용자 정의 컨트롤에 대 한 HTML 코드를 추출 하는 것입니다. 수동으로 작업을 수행 하는 경우 새 사용자 정의 컨트롤을 만들고, 코드 섹션을 사용자 컨트롤로 이동 하 고, 사용자 정의 컨트롤에 대 한 태그 접두사를 등록 하 고, 마지막으로 페이지에서 사용자 정의 컨트롤을 인스턴스화하는 것과 같은 여러 단계가 필요 합니다. 이제 새 *사용자 정의 컨트롤로 추출* 도구가 자동으로 이러한 단계를 모두 수행 합니다.

이 태스크에서는 새 사용자 정의 컨트롤을 사용 하 여 새 사용자 정의 컨트롤 컨텍스트 작업을 사용 하 여 선택한 코드에서 새 사용자 정의 컨트롤을 생성 합니다.

1. **Default.aspx 페이지에서** **H2** 및 **audio** 요소를 선택 합니다.
2. 마우스 오른쪽 단추를 클릭 하 고 **사용자 정의 컨트롤로 추출을**선택 합니다.

    ![사용자 정의 컨트롤로 추출 메뉴 옵션](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image35.png "사용자 정의 컨트롤로 추출 메뉴 옵션")

    *사용자 정의 컨트롤로 추출 메뉴 옵션*
3. 새 사용자 정의 컨트롤의 이름을 입력 합니다. 예를 들어, **주크박스**를 클릭 한 다음 **확인**을 클릭 합니다.

    ![추출한 사용자 정의 컨트롤 저장](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image36.png "추출한 사용자 정의 컨트롤 저장")

    *추출한 사용자 정의 컨트롤 저장*
4. 선택한 코드를 사용자 정의 컨트롤로 추출 하 고 선택한 코드의 원래 위치가 새 사용자 정의 컨트롤의 인스턴스로 대체 되었음을 확인 합니다.

    ![새 사용자 정의 컨트롤을 사용 하도록 페이지가 자동으로 업데이트 됩니다.](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image37.png "새 사용자 정의 컨트롤을 사용 하도록 페이지가 자동으로 업데이트 됩니다.")

    *새 사용자 정의 컨트롤을 사용 하도록 페이지가 자동으로 업데이트 됩니다.*
5. **F5** 키를 눌러 페이지를 실행 하 고 컨트롤이 작동 하는지 확인 합니다.

<a id="Exercise3"></a>

<a id="Exercise_3_Whats_New_in_the_JavaScript_Editor"></a>
### <a name="exercise-3-whats-new-in-the-javascript-editor"></a>연습 3: JavaScript 편집기의 새로운 기능

JavaScript 코드를 작성 하거나 편집 하는 작업은 간단한 작업이 아닙니다. 특히 응용 프로그램 크기가 증가 하기 시작 하 고 긴 파일 및 수백 개의 함수를 처리 하는 것이 좋습니다. 스크립트 개발자는 일반적으로 코드 가독성을 유지 하 고 여러 파일을 탐색 하기 위해 몇 가지 추가 작업을 수행 해야 합니다. JQuery와 같은 JavaScript 라이브러리를 포함 하 여 스크립트 탐색은 코드 길이 때문에 챌린지 자체가 됩니다.

Visual Studio는 코드 모드에 액세스 하 고 구성할 수 있도록 하 여 JavaScript 편집기를 갱신 했습니다. 또는 VB 편집기에 C# 이미 있던 많은 Visual Studio 기능이 JavaScript 편집기에서 구현 됩니다. 정의로 이동, 자동 들여쓰기, 설명서 및 작성 중에 유효성 검사를 수행 합니다. 갱신 된 IntelliSense 목록에서 JavaScript 함수 카탈로그를 편리 하 게 사용할 수 있습니다.

이 연습에서는 JavaScript 편집기의 새로운 기능 및 향상 된 기능 중 일부를 배웁니다. 샘플 파일을 탐색 하 고 Visual Studio 2012 내에서 JavaScript 프로그래밍의 효율성을 높일 수 있는 새로운 특성을 각각 검색 합니다.

<a id="Ex3Task1"></a>

<a id="Task_1_-_JavaScript_Editor_New_Features"></a>
#### <a name="task-1---javascript-editor-new-features"></a>작업 1-JavaScript 편집기의 새로운 기능

이 작업에서는 코드를 구성 하 고 더 나은 사용자 환경을 제공 하는 데 초점을 맞춘 새로운 JavaScript 편집기 기능 중 일부를 소개 합니다.

1. 아직 열지 않은 경우 **Visual Studio** 를 시작 하 고이 랩의 **Source\WhatsNewASPNET** 폴더에 있는 **WhatsNewASPNET** 솔루션을 엽니다.
2. **F5** 키를 눌러 응용 프로그램을 실행 한 다음 탐색 모음에서 JavaScript 링크를 클릭 합니다. 페이지를 여러 번 새로 고치고 카운터가 증가 하는 방식을 확인 합니다.

    ![페이지 카운터](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image38.png "페이지 카운터")

    *페이지 카운터*
3. 브라우저를 닫고 Visual Studio로 돌아갑니다.
4. **JavaScript .aspx** 페이지를 열고 아래에 표시 된 **&lt;스크립트&gt;** 블록을 찾습니다.

    다음 코드는 HTML5 로컬 저장소를 사용 하 여 현재 사용자가 페이지를 방문한 횟수를 저장 하는 *Pageloadcount* 변수를 저장 합니다. 로컬 저장소는 HTML5 표준에 도입 된 클라이언트 쪽 키-값 데이터베이스입니다. 데이터는 사용자의 브라우저 내에서 로컬 컴퓨터에 저장 됩니다.

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample7.html)]

    > [!NOTE]
    > 다음 단계를 진행 하기 전에 DOCTYPE이 XHTML5로 설정 되었는지 확인 합니다.
5. 코드를 편집 하 고 JavaScript 용 IntelliSense는 로컬 저장소와 같은 HTML5 기능과 내부 메서드를 포함 하 고 있는지 확인 합니다.

    ![JavaScript의 HTML5 JavaScript 기능](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image39.png "JavaScript의 HTML5 JavaScript 기능")

    *JavaScript의 HTML5 JavaScript 기능*
6. 스크립팅 코드에서 여는 대괄호 ( **{** )를 클릭 하면 대괄호가 강조 표시 됩니다.

    ![대괄호가 강조 표시 됩니다.](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image40.png "대괄호가 강조 표시 됩니다.")

    *대괄호가 강조 표시 됩니다.*
7. **Testautoalign ()** 함수의 주석 처리를 제거 합니다 (3 개의 줄을 선택 하 고 **CTRL** + **K**를 사용할 수 있음). **CTRL** + **U**)를 누르고 함수 코드 내에서 커서를 찾습니다. Enter 키를 눌러 두 번째 줄을 추가 합니다. 이제 코드가 **정렬** 되 고 **자동으로 들여쓰기**됩니다.

    ![JavaScript 코드가 자동으로 정렬 됨](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image41.png "JavaScript 코드가 자동으로 정렬 됨")

    *JavaScript 코드가 자동으로 정렬 됨*

<a id="Ex3Task2"></a>

<a id="Task_2_-_Validating_JavaScript"></a>
#### <a name="task-2---validating-javascript"></a>작업 2-JavaScript 유효성 검사

이 작업에서는 ECMAScript5 표준에 대 한 새 JavaScript 유효성 검사를 검색 합니다. 이 기능을 통해 호환 되는 JavaScript 코드를 작성 하는 데 도움이 되지만 사이트 배포 이전에는 스크립팅 문제가 방지 됩니다.

> [!NOTE]
> Visual studio 2010은 ECMAStript3 준수를 구현 했지만 Visual studio 2012은 ECMAScript5 규정 준수를 제공 합니다.

1. **Scripts\custom** 프로젝트 폴더 아래에 있는 **ECMA5script5** 을 엽니다. 이제 ECMAScript5 표준에 대 한 유효성 검사를 테스트 합니다.

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample8.html)]

    파일의 첫 번째 줄에서 **엄격한** &quot; 방향을 사용 하 &quot;를 체크 아웃할 수 있습니다. 그러면 ECMAScript5 **strict 모드**를 사용할 수 있습니다. 이 모드는 이전 버전의 모호성을 명확 하 게 하는 언어의 하위 집합으로 구성 되며 getter 및 setter와 같은 몇 가지 새로운 기능, JSON에 대 한 라이브러리 지원 및 개체 속성에 대 한 보다 완전 한 반사를 추가 합니다.
2. 아직 열지 않은 경우 **오류 목록** 열기 (**보기** 메뉴 | **오류 목록**). **함수** 선언에는 밑줄이 그어집니다. 이는 ECMA5 표준 함수를 언어 구조 안에 중첩할 수 없기 때문입니다. 아래 오류 목록에 경고 세부 정보가 표시 됩니다.

    ![JavaScript 유효성 검사 오류 메시지](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image42.png "JavaScript 유효성 검사 오류 메시지")

    *JavaScript 유효성 검사 오류 메시지*
3. **엄격한&quot;방향을 사용 하&quot;** 를 주석으로 처리 하 고 오류가 사라지지만 경고는 남아 있는지 확인 합니다.
4. 파일의 마지막 줄에서 **&quot;테스트&quot;** 와 같은 문자열을 작성 합니다 (따옴표를 포함 하 여 문자열 임을 나타냄). 문자열 옆에 마침표를 쓰고 IntelliSense 목록을 표시 한 다음 **trim** 옵션을 선택 합니다.

    ECMAScript5 standard에서 문자열 값 및 변수에는 trim, 대문자, 검색 및 바꾸기와 같은 문자열 메서드도 정의 되어 있습니다.

    ![JavaScript의 IntelliSense 목록](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image43.png "JavaScript의 IntelliSense 목록")

    *JavaScript의 IntelliSense 목록*

<a id="Ex3Task3"></a>

<a id="Task_3_-_XML_Documentation_for_JavaScript"></a>
#### <a name="task-3---xml-documentation-for-javascript"></a>작업 3-JavaScript에 대 한 XML 문서

이 작업에서는 JavaScript에서 XML 문서에 대 한 Visual Studio 기능을 탐색 합니다. 이제 JavaScript IntelliSense 목록에 각 함수의 XML 문서가 표시 됩니다. 또한 JavaScript에서 탐색 기능을 검색 합니다.

1. **스크립트/사용자 지정** 프로젝트 폴더에 있는 **xmldoc 주석의** 파일을 엽니다. 이 파일에는 각 JavaScript 함수에 대 한 XML 문서가 포함 되어 있습니다.

    ![IntelliSense에 통합 되는 JavaScript XML 문서](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image44.png "IntelliSense에 통합 되는 JavaScript XML 문서")

    *IntelliSense에 통합 되는 JavaScript XML 문서*
2. **Xmldoc 주석의** 파일의 **add** 함수 아래에 **test**라는 새 함수를 만듭니다.
3. **테스트** 함수에서 두 개의 매개 변수를 받는 **곱하기** 함수를 호출 합니다. 도구 설명 상자는 **곱하기** 함수 설명서를 표시 합니다.

    [!code-javascript[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample9.js)]

    ![JavaScript 함수에 대 한 XML 문서](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image45.png "JavaScript 함수에 대 한 XML 문서")

    *JavaScript 함수에 대 한 XML 문서*
4. 함수 호출 문을 완료 하 고 *점을* 입력 하 여 반환 된 값에 대 한 IntelliSense 목록을 엽니다. Visual Studio는 설명서에서 **반환** 값을 검색 하 여 값을 숫자로 처리 합니다.

    ![반환 형식에 대 한 XML 문서](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image46.png "반환 형식에 대 한 XML 문서")

    *반환 형식에 대 한 XML 문서*
5. 이제 함수 추가에 대 한 호출을 삽입 합니다. JavaScript 편집기는 이제 함수 오버 로드를 지원 합니다. 함수 이름을 작성 하면 설명서에 지정 된 사용 가능한 오버 로드를 선택할 수 있습니다.

    ![오버 로드에 대 한 XML 문서](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image47.png "오버 로드에 대 한 XML 문서")

    *오버 로드에 대 한 XML 문서*
6. **GotoDefinition** 파일을 열고 **$ () .html ()** 함수 호출을 찾습니다. **Html**에서 커서를 찾습니다.
7. **F12** 키를 누르고 정의로 이동 합니다. 이제 **찾기** 도구를 사용 하지 않고 JavaScript 코드를 액세스 하 고 찾아볼 수 있습니다.
8. 코드 파일의 맨 아래에 있는 서명 블록 앞에서 jQuery 명령의 커서를 찾습니다. **F12**키를 누릅니다. JQuery 라이브러리 파일로 이동 합니다. **F12**키를 사용 하 여 jQuery 파일을 탐색할 수도 있습니다.

    ![JQuery 정의로 이동](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image48.png "JQuery 정의로 이동")

    *JQuery 정의로 이동*

> [!NOTE]
> GotoDefinition에 파일을 저장 하기 전에 구문 오류가 없는지 확인 합니다.

<a id="Exercise4"></a>

<a id="Exercise_4_Bundling_and_Minification"></a>
### <a name="exercise-4-bundling-and-minification"></a>연습 4: 묶음 및 축소

웹 사이트에 JavaScript 또는 CSS 파일이 둘 이상 포함 되는 횟수는 몇 개입니까? 이는 번들 및 축소를 사용 하 여 파일 크기를 줄이고 사이트를 더 빠르게 수행 하는 데 도움이 되는 매우 일반적인 시나리오입니다. ASP.NET 4.5의 새로운 번들 기능은 JS 또는 CSS 파일 집합을 단일 요소로 압축 하 고, 콘텐츠를 축소 하 여 크기를 줄입니다 (즉, 필요 하지 않은 빈 공간 제거, 주석 제거, 식별자 감소).

ASP.NET 4.5의 묶음 및 축소는 런타임에 수행 되어 사용자 에이전트 (예: IE, Mozilla 등)를 식별할 수 있습니다. 따라서 사용자 브라우저를 대상으로 지정 하 여 압축을 향상 시킵니다 (예: Mozilla 관련 된 콘텐츠 제거). 요청이 IE에서 제공 되는 경우).

이 연습에서는 ASP.NET 4.5에서 다양 한 종류의 묶음 및 축소를 사용 하도록 설정 하 고 사용 하는 방법에 대해 설명 합니다.

<a id="Ex4Task1"></a>

<a id="Task_1_-_Installing_the_Bundling_and_Minification_Package_from_NuGet"></a>
#### <a name="task-1---installing-the-bundling-and-minification-package-from-nuget"></a>작업 1-NuGet에서 번들 및 축소 패키지 설치

1. 아직 열지 않은 경우 **Visual Studio** 를 시작 하 고이 랩의 **Source\WhatsNewASPNET** 폴더에 있는 **WhatsNewASPNET** 솔루션을 엽니다.
2. NuGet 패키지 관리자 콘솔을 엽니다. 이렇게 하려면 **다른 Windows** | **패키지 관리자 콘솔** | 메뉴 **뷰** 를 사용 합니다.

    ![패키지 관리자 file:///C:/Users/User/AppData/Local/Temp/Marker3744//media/44462/Multiple-Stylesheets-and-JavaScript-files-in-the-application.pngconsole 열기](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image49.png "패키지 관리자 콘솔 열기")

    *패키지 관리자 콘솔 열기*
3. **패키지 관리자 콘솔** 에서 **설치 패키지** 를 입력 하 고 **enter**키를 누릅니다.

<a id="Ex4Task2"></a>

<a id="Task_2_-_Default_Bundles"></a>
#### <a name="task-2---default-bundles"></a>작업 2-기본 번들

묶음 및 축소를 사용 하는 가장 간단한 방법은 기본 번들을 사용 하는 것입니다. 이 메서드는 규칙을 사용 하 여 폴더의 JS 및 CSS 파일에 대해 제공 된 버전과 표시 되지 않은 버전을 참조할 수 있도록 합니다.

이 태스크에서는 함께 제공 된 JS 및 CSS 파일을 사용 하도록 설정 하 고 참조 하 고 결과 출력을 확인 하는 방법에 대해 설명 합니다.

1. 아직 열지 않은 경우 **Visual Studio** 를 시작 하 고이 랩의 **Source\WhatsNewASPNET** 폴더에 있는 **WhatsNewASPNET** 솔루션을 엽니다.
2. **솔루션 탐색기**에서 **scripts\custom** 및 **scripts\custom** 폴더 **스타일**을 확장 합니다.

    응용 프로그램에서 둘 이상의 CSS 및 JS 파일을 사용 하 고 있습니다.

    ![응용 프로그램의 여러 스타일 시트 및 JavaScript 파일](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image50.png "응용 프로그램의 여러 스타일 시트 및 JavaScript 파일")

    *응용 프로그램의 여러 스타일 시트 및 JavaScript 파일*
3. **Global.asax.cs** 파일을 엽니다.

    새 **Microsoft** 네임 스페이스는 파일의 시작 부분에서 주석으로 처리 됩니다. Using 지시문의 주석 처리를 제거 하 여 묶음 및 축소 기능을 포함 합니다.

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample10.cs)]
4. **응용 프로그램\_Start** 메서드를 찾습니다.

    이 메서드에서는 아래 코드 조각과 같이 EnableDefaultBundles 호출의 주석 처리를 제거 합니다. 이렇게 하면 해당 폴더에 대 한 경로를 사용 하 여 폴더에 있는 CSS 파일의 번들 컬렉션을 참조할 수 있으며 &quot;CSS&quot; 또는 &quot;JS&quot; 접미사를 사용할 수 있습니다.

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample11.cs)]
5. **최적화 .aspx** 파일을 열고 **헤드 콘텐츠의**콘텐츠 컨트롤을 찾습니다.

    CSS 파일 및 JS 파일에는 참조 된 단일 태그가 있습니다.

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample12.aspx)]

    > [!NOTE]
    > 이 코드는 데모용입니다. 이상적으로는 사이트 .Master 파일에서 번들을 참조 합니다. 이 샘플 코드에서는 일부 번들 파일이 Site.master 파일에 의해 참조 되는 것을 확인 하 여 마지막 참조를 중복 합니다.
6. 링크는 **href** 특성의 묶음 규칙을 사용 하 여 각각 Styles 및 Scripts\custom 폴더에서 모든 CSS 또는 JS 파일을 가져옵니다.

    아래 표시 된 것 처럼 **스크립트/사용자 지정/js** 경로를 사용 하 여 **스크립트/사용자 지정** 폴더 내의 모든 JS 파일을 번들로 묶어 지정할 수 있습니다. 기본 번들의 기본 동작입니다.

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample13.aspx)]
7. **Styles\Site.css** 파일을 엽니다.

    원래 CSS 파일에는 들여쓰기 된 코드, 공백 및 파일을 확장 하는 주석이 포함 되어 있습니다. (또한 JavaScript 파일에는 공백 및 주석이 포함 되어 있습니다.)

    ![Scripts 폴더의 원본 CSS 파일 중 하나](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image51.png "Scripts 폴더의 원본 CSS 파일 중 하나")

    *Scripts 폴더의 원본 CSS 파일 중 하나*
8. **F5** 키를 눌러 응용 프로그램을 실행 하 고 **최적화** 페이지로 이동 합니다.
9. **CSS 번들** 링크를 클릭 하 여 파일을 다운로드 하 고 엽니다.

    함께 제공 되는 파일을 체크 아웃 합니다. 모든 공백, 주석 및 들여쓰기 문자가 제거 되어 더 작은 파일을 생성 하는 것을 알 수 있습니다.

    ![번들로 제공 되는 CSS 파일](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image52.png "번들로 제공 되는 CSS 파일")

    *번들로 제공 되는 CSS 파일*
10. 이제 **JS 번들** 링크를 클릭 하 여 JavaScript 번들 파일을 엽니다. 탐색기 경고는 무시 해도 됩니다. **사용자 지정** 폴더 아래의 JavaScript 파일도 번들로 표시 되 고 확인 되지 않습니다.

    ![번들로 제공 되는 JavaScript 파일](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image53.png "번들로 제공 되는 JavaScript 파일")

    *번들로 제공 되는 JavaScript 파일*

    이전 ASP.NET 버전에서는 CSS 또는 JS 파일에 대해 압축을 사용 하는 것이 훨씬 더 복잡 합니다. 이제 *global.asax* 파일에 한 줄을 추가 하 여 번들을 사용 하도록 설정한 다음 사이트에서 번들로 제공 되는 파일을 참조 하기만 하면 됩니다.

<a id="Ex4Task3"></a>

<a id="Task_3_-_Static_Bundles"></a>
#### <a name="task-3---static-bundles"></a>작업 3-정적 번들

정적 번들 방식을 사용 하면 사용할 파일 집합, 참조 및 사용 되는 축소 메서드를 사용자 지정할 수 있습니다.

이 작업에서는 번들로 지정 된 특정 파일 집합을 정의 하도록 정적 번들을 구성 합니다.

1. 브라우저를 닫습니다.
2. **Global.asax.cs** 파일을 열고 **응용 프로그램\_Start** 메서드를 찾습니다.
3. 아래 코드에 표시 된 것 처럼 정적 번들 코드의 주석 처리를 제거 합니다.

    &quot; **~/Staticbundle**&quot; 가상 경로를 사용 하 여 참조 되는 정적 번들을 정의 하 고 **AddFile** 메서드를 사용 하 여 지정 된 모든 파일의 축소에 **JsMinify** 를 사용 합니다. 마지막으로 **bundletable.enableoptimization** 에 정적 번들을 추가 하 고 사용 하도록 설정 합니다.

    파일이 동일한 위치에 있지 않은 것을 알 수 있습니다. 이는 기본 묶음의 또 다른 장점입니다.

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample14.cs)]
4. **최적화 .aspx** 파일을 엽니다.

    **정적 JS 번들** 에 대 한 링크는 Global.asax.cs 파일에서 정적 번들을 구성할 때 선언 된 경로를 사용 하 고 있습니다. **/staticbundle**.

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample15.aspx)]
5. **F5** 키를 눌러 응용 프로그램을 실행 한 다음 **최적화** 페이지로 이동 합니다.
6. **정적 JS 번들** 링크를 클릭 하 여 파일을 엽니다.

    함께 제공 된 모든 JavaScript 파일의 출력은 고정 번들 파일에서 구성 된 모든 JavaScript 파일의 출력으로, &quot;/StaticBundle&quot;경로 아래에 있습니다.

    ![정적 JavaScript 파일 번들](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image54.png "정적 JavaScript 파일 번들")

    *정적 JavaScript 파일 번들*
7. 브라우저를 닫고 Visual Studio로 돌아갑니다.

<a id="Ex4Task4"></a>

<a id="Task_4_-_Dynamic_Folder_Bundles"></a>
#### <a name="task-4---dynamic-folder-bundles"></a>작업 4-동적 폴더 번들

이 작업에서는 동적 폴더 번들을 구성 하는 방법을 알아봅니다. 동적 번들의 기능은 정적 JavaScript와 JavaScript로 컴파일되는 언어의 다른 파일을 포함할 수 있으므로 번들이 실행 되기 전에 약간의 처리가 필요 하다는 것입니다.

이 예제에서는 **Dynamicfolderbundle** 클래스를 사용 하 여 CofeeScript로 작성 된 파일에 대 한 동적 번들을 만드는 방법에 대해 설명 합니다. CofeeScript는 javascript로 컴파일되고 javascript 코드를 작성 하는 간단한 구문을 제공 하 여 JavaScript의 간결 하 고 가독성이 향상 되는 프로그래밍 언어입니다.

1. **Global.asax.cs** 파일을 열고 **응용 프로그램\_Start** 메서드를 찾습니다.
2. 아래 코드에 표시 된 것 처럼 동적 번들 코드의 주석 처리를 제거 합니다.

    &quot; **. 커피**&quot; 확장 (CoffeeScript 파일)을 사용 하 여 파일에만 적용 되는 **CoffeeMinify** 사용자 지정 축소 프로세서를 사용 하는 동적 폴더 번들을 정의 합니다. 검색 패턴을 사용 하 여 폴더 내에서 묶을 파일을 선택할 수 있습니다 (예: '\*. 커피 ').

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample16.cs)]
3. NuGet 패키지 관리자 콘솔을 엽니다. 이렇게 하려면 **다른 Windows** | **패키지 관리자 콘솔** | 메뉴 **뷰** 를 사용 합니다.
4. **패키지 관리자 콘솔** 에서 **Install CoffeeSharp** **을 입력 하 고 enter 키를**누릅니다.
5. **솔루션 탐색기** 창에서 **모든 파일 표시** 단추를 클릭 합니다.

    ![모든 파일 표시](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image55.png "모든 파일 표시")

    *모든 파일 표시*
6. **솔루션 탐색기** 에서 **CoffeeMinify.cs** 파일을 마우스 오른쪽 단추로 클릭 하 고 **프로젝트에 포함** 을 선택 합니다.

    ![프로젝트에 CoffeeMinify.cs 파일 포함](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image56.png "프로젝트에 CoffeeMinify.cs 파일 포함")

    *프로젝트에 CoffeeMinify.cs 파일 포함*
7. **CoffeeMinify.cs** 파일을 엽니다.

    이 클래스는 CoffeeScript 코드 컴파일에서 생성 된 JavaScript 출력을 JsMinify에서 미니로 상속 합니다. CoffeeScript 컴파일러를 호출 하 여 JavaScript 코드를 먼저 생성 한 다음 JsMinify 메서드로 보내 결과 코드를 축소 합니다.

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample17.cs)]
8. **Scripts/번들** 폴더에서 **Script1** 및 **Script2** 파일을 엽니다.

    이러한 파일에는 CoffeeMinify 클래스를 사용 하 여 번들을 수행 하는 동안 컴파일될 CoffeScript 코드가 포함 됩니다.

    간단한 설명을 위해 제공 된 CoffeeScript 파일은 CoffeeScript 샘플 코드를 포함 합니다. 주석은 JsMinify 프로세스에 의해 제외 됩니다.

    ![CoffeeScript 파일](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image57.png "CoffeeScript 파일")

    *CoffeeScript 파일*

    > [!NOTE]
    > [CofeeScript](https://github.com/jashkenas/coffeescript/) 는 javascript 코드를 작성 하는 간단한 구문을 제공 하 여 javascript의 간결 하 고 가독성이 향상 되 고 배열 이해 및 패턴 일치와 같은 다른 기능을 추가 합니다.
9. **최적화 .aspx** 파일을 열고 번들 링크를 찾습니다.

    **동적 JS 번들** 에 대 한 링크는 동적 폴더 번들에 대해 구성한 **/coffee** 접미사를 사용 하 여 **스크립트/번들** 폴더를 참조 하 고 있습니다.

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample18.aspx)]
10. **F5** 키를 눌러 응용 프로그램을 실행 한 다음 **최적화** 페이지로 이동 합니다.
11. **동적 JS 번들** 링크를 클릭 하 여 생성 된 파일을 엽니다.

    이 번들에 포함 된 콘텐츠는 커피 파일만 포함 하 고 있습니다 **.** CoffeeScript 코드를 JavaScript로 컴파일 했 고 주석 처리 된 줄이 제거 되었음을 확인할 수도 있습니다.

    ![동적 JS 파일 번들](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image58.png "동적 JS 파일 번들")

    *동적 JS 파일 번들*

> [!NOTE]
> 또한 [부록 B: 웹 배포을 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시](#AppendixB)를 수행 하는 Windows Azure 웹 사이트에이 응용 프로그램을 배포할 수 있습니다.

<a id="Summary"></a>
## <a name="summary"></a>요약

이 랩을 통해 Visual Studio 2012에서 ASP.NET 및 웹 개발의 새로운 기능 및 Visual Studio 2012의 다양 한 향상 된 기능을 활용 하는 방법을 이해할 수 있습니다.

이 실습 실습을 완료 하면 Visual Studio 2012 편집기에서 CSS, JavaScript 및 HTML에 대 한 새로운 기능 및 향상 된 기능을 사용 하는 방법을 학습 수 있습니다. 또한 Visual Studio 2012에서 기본 제공 번들 및 축소를 구현 하는 방법도 학습 있습니다.

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>부록 A: 웹에 대 한 Visual Studio Express 2012 설치

**[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)** 를 사용 하 여 웹 또는 다른 &quot;Express&quot; 버전 **에 대해 Microsoft Visual Studio Express 2012** 를 설치할 수 있습니다. 다음 지침에서는 *Microsoft 웹 플랫폼 설치 관리자*를 사용 하 여 *Visual studio Express 2012 for Web* 을 설치 하는 데 필요한 단계를 안내 합니다.

1. [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)로 이동 합니다. 또는 웹 플랫폼 설치 관리자를 이미 설치한 경우에는 웹 플랫폼 설치 관리자를 열고 <em>Microsoft AZURE SDK&quot;를 사용 하 여 웹 용 2012 Visual Studio Express</em> &quot;제품을 검색할 수 있습니다.
2. **지금 설치**를 클릭 합니다. **웹 플랫폼 설치 관리자** 가 없으면 먼저이를 다운로드 하 여 설치 하도록 리디렉션됩니다.
3. **웹 플랫폼 설치 관리자** 가 열리면 **설치** 를 클릭 하 여 설치를 시작 합니다.

    ![Visual Studio Express 설치](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image59.png "Visual Studio Express 설치")

    *Visual Studio Express 설치*
4. 모든 제품의 라이선스 및 사용 조건을 읽고 **동의** 함을 클릭 하 여 계속 합니다.

    ![사용 조건 동의](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image60.png)

    *사용 조건 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image61.png)

    *설치 진행률*
6. 설치가 완료 되 면 **마침**을 클릭 합니다.

    ![설치 완료](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image62.png)

    *설치 완료*
7. **끝내기** 를 클릭 하 여 웹 플랫폼 설치 관리자를 닫습니다.
8. 웹에 대 한 Visual Studio Express를 열려면 **시작** 화면으로 이동 하 &quot;**VS Express**&quot;작성을 시작한 후 **VS Express for Web** 타일을 클릭 합니다.

    ![VS Express for Web 타일](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image63.png)

    *VS Express for Web 타일*

---

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>부록 B: 웹 배포을 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시

이 부록에서는 windows azure 관리 포털에서 새 웹 사이트를 만들고 랩에 따라 가져온 응용 프로그램을 게시 하 여 Windows Azure에서 제공 하는 웹 배포 게시 기능을 활용 하는 방법을 보여 줍니다.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a>작업 1-Windows Azure 포털에서 새 웹 사이트 만들기

1. [Windows Azure 관리 포털](https://manage.windowsazure.com/) 로 이동 하 고 구독과 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.

    > [!NOTE]
    > Windows Azure를 사용 하면 10 개의 ASP.NET 웹 사이트를 무료로 호스팅한 후 트래픽 증가에 따라 크기를 조정할 수 있습니다. [여기](https://aka.ms/aspnet-hol-azure)에서 등록할 수 있습니다.

    ![Windows Azure Portal에 로그온 합니다.](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image64.png "Windows Azure Portal에 로그온 합니다.")

    *Windows Azure 관리 포털에 로그온 합니다.*
2. 명령 모음에서 **새로 만들기** 를 클릭 합니다.

    ![새 웹 사이트 만들기](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image65.png "새 웹 사이트 만들기")

    *새 웹 사이트 만들기*
3. **Compute** | **웹 사이트**를 클릭 합니다. 그런 다음 **빠른 생성** 옵션을 선택 합니다. 새 웹 사이트에 사용할 수 있는 URL을 제공 하 고 **웹 사이트 만들기**를 클릭 합니다.

    > [!NOTE]
    > Microsoft Azure 웹 사이트는 사용자가 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램에 대 한 호스트입니다. 빠른 생성 옵션을 사용 하면 포털 외부에서 Windows Azure 웹 사이트에 완료 된 웹 응용 프로그램을 배포할 수 있습니다. 데이터베이스를 설정 하는 단계는 포함 되지 않습니다.

    ![빠른 생성을 사용 하 여 새 웹 사이트 만들기](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image66.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")

    *빠른 생성을 사용 하 여 새 웹 사이트 만들기*
4. 새 **웹 사이트가** 만들어질 때까지 기다립니다.
5. 웹 사이트를 만든 후 **URL** 열 아래의 링크를 클릭 합니다. 새 웹 사이트가 작동 하는지 확인 합니다.

    ![새 웹 사이트로 이동](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image67.png "새 웹 사이트로 이동")

    *새 웹 사이트로 이동*

    ![웹 사이트 실행 중](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image68.png "웹 사이트 실행 중")

    *웹 사이트 실행 중*
6. 포털로 돌아가서 **이름** 열 아래에 있는 웹 사이트의 이름을 클릭 하 여 관리 페이지를 표시 합니다.

    ![웹 사이트 관리 페이지 열기](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image69.png "웹 사이트 관리 페이지 열기")

    *웹 사이트 관리 페이지 열기*
7. **대시보드** 페이지의 **빠른** 보기 섹션에서 **게시 프로필 다운로드** 링크를 클릭 합니다.

    > [!NOTE]
    > *게시 프로필* 에는 사용 하도록 설정 된 각 게시 방법에 대해 웹 응용 프로그램을 Windows Azure 웹 사이트에 게시 하는 데 필요한 모든 정보가 포함 되어 있습니다. 게시 프로필에는 게시 방법이 사용 설정된 각 엔드포인트에 연결하고 이에 대해 인증하는 데 필요한 URL, 사용자 자격 증명 및 데이터베이스 문자열이 포함되어 있습니다. **Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** 및 **Microsoft Visual Studio 2012** 는 게시 프로필 읽기를 지원 하 여 웹 응용 프로그램을 Windows Azure 웹 사이트에 게시 하기 위해 이러한 프로그램의 구성을 자동화 합니다.

    ![웹 사이트 게시 프로필을 다운로드 하는 중](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image70.png "웹 사이트 게시 프로필을 다운로드 하는 중")

    *웹 사이트 게시 프로필을 다운로드 하는 중*
8. 알려진 위치에 게시 프로필 파일을 다운로드 합니다. 이 연습을 통해이 파일을 사용 하 여 Visual Studio에서 Windows Azure 웹 사이트에 웹 응용 프로그램을 게시 하는 방법을 확인할 수 있습니다.

    ![게시 프로필 파일을 저장 하는 중](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image71.png "게시 프로필을 저장 하는 중")

    *게시 프로필 파일을 저장 하는 중*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>작업 2-데이터베이스 서버 구성

응용 프로그램에서 SQL Server 데이터베이스를 사용 하는 경우 SQL Database 서버를 만들어야 합니다. SQL Server 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 작업을 건너뛸 수 있습니다.

1. 응용 프로그램 데이터베이스를 저장 하기 위한 SQL Database 서버가 필요 합니다. Microsoft Azure 관리 포털의 구독에서 SQL Database 서버를 볼 수는 **SQL 데이터베이스** | **서버** | **서버의 대시보드**. 만든 서버가 없는 경우 명령 모음에서 **추가** 단추를 사용 하 여 만들 수 있습니다. 다음 작업에서 사용할 **서버 이름과 URL, 관리자 로그인 이름 및 암호**를 기록해 둡니다. 이후 단계에서 생성 되므로 아직 데이터베이스를 만들지 마십시오.

    ![SQL Database 서버 대시보드](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image72.png "SQL Database 서버 대시보드")

    *SQL Database 서버 대시보드*
2. 다음 작업에서는 Visual Studio에서 데이터베이스 연결을 테스트 합니다. 따라서 서버에서 **허용 되는 Ip 주소**목록에 로컬 IP 주소를 포함 해야 합니다. 이렇게 하려면 **구성**을 클릭 하 고 **현재 클라이언트 IP 주소** 에서 ip 주소를 선택한 후 **시작 Ip 주소** 및 **끝 ip 주소** 텍스트 상자에 붙여넣습니다. 규칙의 이름을 입력 하 고 ![-](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image73.png)---------------------------

    ![클라이언트 IP 주소를 추가 하는 중](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image74.png)

    *클라이언트 IP 주소를 추가 하는 중*
3. **클라이언트 Ip 주소가** 허용 된 ip 주소 목록에 추가 되 면 **저장** 을 클릭 하 여 변경 내용을 확인 합니다.

    ![변경 내용 확인](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image75.png)

    *변경 내용 확인*

<a id="Ex1Task3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시

1. ASP.NET MVC 4 솔루션으로 돌아갑니다. **솔루션 탐색기**에서 웹 사이트 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 선택 합니다.

    ![응용 프로그램 게시](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image76.png "응용 프로그램 게시")

    *웹 사이트 게시*
2. 첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.

    ![게시 프로필을 가져오는 중](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image77.png "게시 프로필을 가져오는 중")

    *게시 프로필을 가져오는 중*
3. **연결 유효성 검사**를 클릭 합니다. 유효성 검사가 완료 되 면 **다음**을 클릭 합니다.

    > [!NOTE]
    > 유효성 검사는 연결 유효성 검사 단추 옆에 녹색 확인 표시가 표시 되 면 완료 됩니다.

    ![연결 유효성 검사](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image78.png "연결 유효성 검사")

    *연결 유효성 검사*
4. **설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆에 있는 단추 (즉, **defaultconnection**)를 클릭 합니다.

    ![웹 배포 구성](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image79.png "웹 배포 구성")

    *웹 배포 구성*
5. 데이터베이스 연결을 다음과 같이 구성 합니다.

   - **서버 이름** 에 *tcp:* 접두사를 사용 하 여 SQL Database 서버 URL을 입력 합니다.
   - **사용자 이름** 에 서버 관리자 로그인 이름을 입력 합니다.
   - **암호** 에 서버 관리자 로그인 암호를 입력 합니다.
   - 새 데이터베이스 이름 (예: *MVC4SampleDB*)을 입력 합니다.

     ![대상 연결 문자열 구성](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image80.png "대상 연결 문자열 구성")

     *대상 연결 문자열 구성*
6. 그런 후 **OK**를 클릭합니다. 데이터베이스를 만들 것인지 묻는 메시지가 표시 되 면 **예**를 클릭 합니다.

    ![데이터베이스 만들기](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image81.png "데이터베이스 문자열 만들기")

    *데이터베이스 만들기*
7. Windows Azure에서 SQL Database에 연결 하는 데 사용할 연결 문자열은 기본 연결 텍스트 상자 내에 표시 됩니다. 그런 후 **Next** 를 클릭합니다.

    ![SQL Database를 가리키는 연결 문자열](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image82.png "SQL Database를 가리키는 연결 문자열")

    *SQL Database를 가리키는 연결 문자열*
8. **미리 보기** 페이지에서 **게시**를 클릭 합니다.

    ![웹 응용 프로그램 게시](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image83.png "웹 응용 프로그램 게시")

    *웹 응용 프로그램 게시*
9. 게시 프로세스가 완료 되 면 기본 브라우저가 게시 된 웹 사이트를 엽니다.

    ![Windows Azure에 게시 된 응용 프로그램](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image84.png "Windows Azure에 게시 된 응용 프로그램")

    *Windows Azure에 게시 된 응용 프로그램*
