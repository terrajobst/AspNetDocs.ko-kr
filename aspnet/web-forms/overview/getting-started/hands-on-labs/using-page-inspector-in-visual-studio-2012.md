---
uid: web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
title: Visual Studio 2012에서 페이지 검사기 사용 | Microsoft Docs
author: rick-anderson
description: 이 실습 랩에서는 Visual Studio에서 웹 페이지 문제를 검색 하 고 수정 하는 새 도구인 페이지 검사기를 검색 합니다. 페이지 검사기는 새로운 도구인
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 73232292-a5fe-4720-82a1-8f6553effd1f
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: f42b1be2697ba7d1145b3e334fe8f4ebf019cd12
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78473801"
---
# <a name="using-page-inspector-in-visual-studio-2012"></a>Visual Studio 2012에서 페이지 검사기 사용

[웹 캠프 팀](https://twitter.com/webcamps)

> 이 실습 랩에서는 Visual Studio에서 웹 페이지 문제를 검색 하 고 수정 하는 새 도구인 페이지 검사기를 검색 합니다.
> 
> 페이지 검사기는 브라우저 진단 도구를 Visual Studio에 제공 하 고 브라우저, ASP.NET 및 소스 코드 간에 통합 된 환경을 제공 하는 새로운 도구입니다. Visual Studio IDE 내에서 직접 웹 페이지 (HTML, Web Forms, ASP.NET MVC 또는 웹 페이지)를 렌더링 하 고 소스 코드와 결과 출력을 모두 검사할 수 있습니다. 페이지 검사기를 사용 하면 웹 사이트를 쉽게 분해 하 고, 처음부터 빠르게 페이지를 작성 하 고, 문제를 신속 하 게 진단할 수 있습니다.
> 
> 오늘날 ASP.NET MVC 및 WebForms와 같이 적시에 유연 하 고 확장 가능한 웹 사이트를 만드는 다양 한 웹 프레임 워크가 있습니다. 반면에 IDE는 템플릿 기반 페이지와 동적 콘텐츠에서 디자이너 뷰를 지원 하지 않기 때문에 페이지에서 발생 하는 문제를 찾는 것이 더 어려워집니다. 따라서 이러한 웹 사이트를 브라우저에서 열어 사용자에 게 표시 되는 방식을 확인 해야 합니다.
> 
> 웹 개발자는 외부 도구를 사용 하 여 브라우저에서 정기적으로 실행 되는 문제를 찾습니다. 그런 다음 IDE로 돌아가서 수정을 시작 합니다. IDE, 브라우저 및 프로 파일링 도구 사이에서 이와 같은 작업을 수행 하는 것은 비효율적일 수 있으며, 경우에 따라 문제를 재현할 때마다 새로 배포 하 고 캐시를 정리 해야 합니다.
> 
> 페이지 검사기는 결합 된 기능 집합을 사용 하 여 두 분야의 장점을 모두 제공 함으로써 클라이언트 (브라우저 도구)와 서버 (ASP.NET 및 소스 코드) 사이에서 웹 개발의 격차를 통합 합니다.
> 
> 페이지 검사기를 사용 하 여 브라우저에서 렌더링 될 HTML 태그를 생성 한 소스 파일 (서버 쪽 코드 포함)의 요소를 확인할 수 있습니다. 또한 페이지 검사기를 사용 하면 CSS 속성 및 DOM 요소 특성을 수정 하 여 브라우저에 즉시 반영 된 변경 내용을 볼 수 있습니다.
> 
> 이 실습 랩에서는 페이지 검사기 기능을 안내 하 고 이러한 기능을 사용 하 여 웹 응용 프로그램의 문제를 해결 하는 방법을 보여 줍니다. **이 랩에서는 비슷한 흐름을 사용 하지만 다른 기술을 대상으로 하는 두 개의 연습이 포함 되어 있습니다. ASP.NET MVC 개발자 인 경우 연습 1을 따르세요. WebForms 개발자 인 경우 연습 2를 따릅니다**.
> 
> 이 랩에서는 원본 폴더에 제공 된 샘플 웹 응용 프로그램에 사소한 변경 사항을 적용 하 여 앞에서 설명한 향상 된 기능 및 새로운 기능을 안내 합니다.
> 
> 모든 샘플 코드와 코드 조각은 [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)에서 사용할 수 있는 웹 캠프 교육 키트에 포함 되어 있습니다.

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서는 다음 방법에 대해 알아봅니다.

- 페이지 검사기를 사용 하 여 웹 사이트 분해
- 페이지 검사기를 사용 하 여 CSS 스타일 변경 검사 및 미리 보기
- 페이지 검사기를 사용 하 여 웹 페이지의 문제 검색 및 해결

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>사전 요구 사항

이 랩을 완료 하려면 다음 항목이 있어야 합니다.

- [웹 또는 고급의 경우 2012 Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (설치 방법에 대 한 지침은 [부록 a를](#AppendixA) 참조 하세요.)
- Internet Explorer 9 이상

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>실습

이 실습 랩에는 다음 연습이 포함 되어 있습니다.

1. [연습 1: ASP.NET MVC 프로젝트에서 페이지 검사기 사용](#Exercise1)
2. [연습 2: WebForms 프로젝트에서 페이지 검사기 사용](#Exercise2)

> [!NOTE]
> 각 연습은 연습 시작 폴더에 있는 시작 솔루션과 함께 사용 하 여 각 연습을 서로 독립적으로 수행할 수 있습니다. 연습에 대 한 소스 코드 내에서 해당 연습의 단계를 완료 하 여 생성 된 코드를 포함 하는 Visual Studio 솔루션을 포함 하는 끝 폴더를 찾을 수도 있습니다. 이 실습 랩을 통해 작업할 때 추가 도움이 필요한 경우 이러한 솔루션을 지침으로 사용할 수 있습니다.

이 랩을 완료 하는 데 소요 되는 예상 시간: **30 분**

<a id="Exercise1"></a>

<a id="Exercise_1_Using_Page_Inspector_in_ASPNET_MVC_Projects"></a>
### <a name="exercise-1-using-page-inspector-in-aspnet-mvc-projects"></a>연습 1: ASP.NET MVC 프로젝트에서 페이지 검사기 사용

이 연습에서는 **페이지 검사기**를 사용 하 여 **ASP.NET MVC 4** 솔루션을 미리 보고 디버그 하는 방법을 알아봅니다. 먼저, 웹 디버깅 프로세스를 용이 하 게 하는 기능을 배울 수 있도록 도구를 간략히 살펴봅니다. 그런 다음 스타일 문제가 있는 웹 페이지에서 작업 합니다. 페이지 검사기를 사용 하 여 문제를 생성 하는 소스 코드를 찾고 수정 하는 방법을 배웁니다.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a>작업 1-페이지 검사기 탐색

이 작업에서는 사진 갤러리를 표시 하는 ASP.NET MVC 4 프로젝트의 컨텍스트에서 페이지 검사기를 사용 하는 방법에 대해 설명 합니다.

1. **Source/Ex1-MVC4/begin/** 폴더에 있는 **시작** 솔루션을 엽니다.

   1. 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.
   2. **NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.
   3. 마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.

      > [!NOTE]
      > NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다. NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다. 이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.
2. 솔루션 탐색기 **/Views/Home** 프로젝트 폴더 아래에서 **Index. cshtml** 뷰를 찾아 마우스 오른쪽 단추로 클릭 한 다음 **페이지 검사기에서 보기**를 선택 합니다.

    ![페이지 검사기 미리 볼 파일 선택](using-page-inspector-in-visual-studio-2012/_static/image1.png "페이지 검사기 미리 볼 파일 선택")

    *페이지 검사기 미리 볼 파일 선택*
3. 페이지 검사기 창에는 선택한 원본 뷰에 매핑된 */Home/Index* URL이 표시 됩니다.

    ![PageInspector의 첫 번째 연락처](using-page-inspector-in-visual-studio-2012/_static/image2.png)

    *페이지 검사기에 대 한 첫 번째 연락처*

    페이지 검사기 도구는 Visual Studio 환경에 통합 되어 있습니다. 검사기에는 강력한 HTML 프로파일러와 함께 포함 된 브라우저가 포함 되어 있습니다. 페이지의 모양을 확인 하기 위해 솔루션을 실행할 필요는 없습니다.

    > [!NOTE]
    > 페이지 검사기 브라우저의 너비가 열린 페이지의 너비 보다 적으면 페이지가 제대로 표시 되지 않습니다. 이 경우 페이지 검사기의 너비를 조정 합니다.
4. 페이지 검사기에서 **파일** 탭을 클릭 합니다.

    인덱스 페이지를 작성 하는 모든 원본 파일이 표시 됩니다. 이 기능을 사용 하면 특히 부분 뷰 및 템플릿으로 작업 하는 경우 모든 요소를 한눈에 식별할 수 있습니다. 링크를 클릭 하면 각 파일을 열 수도 있습니다.

    ![-파일-탭](using-page-inspector-in-visual-studio-2012/_static/image3.png)

    *파일 탭*
5. 탭의 왼쪽에 있는 **토글 검사 모드** 단추를 클릭 합니다.

    이 도구를 사용 하 여 페이지의 요소를 선택 하 고 HTML 및 Razor 코드를 볼 수 있습니다.

    ![전환-검사 모드-단추](using-page-inspector-in-visual-studio-2012/_static/image4.png)

    *검사 모드 토글 단추*
6. 페이지 검사기 브라우저에서 마우스 포인터를 페이지 요소 위로 이동 합니다. 마우스 포인터를 렌더링 된 페이지의 특정 부분으로 이동 하는 동안 요소 형식이 표시 되 고 Visual Studio 편집기에서 해당 소스 태그나 코드가 강조 표시 됩니다.

    ![검사 모드 실행](using-page-inspector-in-visual-studio-2012/_static/image5.png)

    *검사 모드 실행*

    > [!NOTE]
    > 페이지 검사기 창을 최대화 하지 마십시오. 그렇지 않으면 소스 코드를 표시 하는 미리 보기 탭을 볼 수 없습니다. 최대화 된 페이지 검사기의 요소를 클릭 하면 선택의 소스 코드가 표시 되지만 페이지 검사기 창이 숨겨집니다.

    **인덱스 cshtml** 파일에 주의를 기울여야 하는 경우 선택한 요소를 생성 하는 소스 코드의 일부가 강조 표시 된 것을 알 수 있습니다. 이 기능을 사용 하면 긴 소스 파일을 쉽게 편집할 수 있으므로 코드에 직접 액세스 하는 방법과 빠른 방법을 제공 합니다.

    ![요소 검사](using-page-inspector-in-visual-studio-2012/_static/image6.png)

    *요소 검사*
7. **검사 모드 설정/해제** 단추를 클릭 합니다 (![Html 탭을 선택 하 여 페이지 검사기 브라우저에 렌더링 된 html 코드를 표시 합니다.](using-page-inspector-in-visual-studio-2012/_static/image7.png "HTML 탭을 선택 하 여 페이지 검사기 브라우저에서 렌더링 된 HTML 코드를 표시 합니다.") )를 사용 하지 않도록 설정 합니다.
8. **Html** 탭을 선택 하 여 페이지 검사기 브라우저에서 렌더링 된 html 코드를 표시 합니다.
9. HTML 태그에서 Koala 링크를 사용 하 여 목록 항목을 찾아 선택 합니다.

    코드를 선택 하면 브라우저에서 해당 출력이 자동으로 강조 표시 됩니다. 이 기능은 HTML 블록이 페이지에서 렌더링 되는 방법을 확인 하는 데 유용 합니다.

    ![페이지에서 HTML 요소 선택](using-page-inspector-in-visual-studio-2012/_static/image8.png "페이지에서 HTML 요소 선택")

    *페이지에서 HTML 요소 선택*
10. 검사 모드 설정 **/해제** 단추를 클릭 하 여 *검사 모드* 를 사용 하도록 설정 하 고 탐색 모음을 클릭 합니다. HTML 코드의 오른쪽에 있는 스타일 창에 선택한 요소에 CSS 스타일이 적용 된 목록이 표시 됩니다.

    > [!NOTE]
    > 헤더가 사이트 레이아웃의 일부 이기 때문에 페이지 검사기 \_Layout 파일이 열리고 영향을 받는 코드의 세그먼트가 강조 표시 됩니다.

    ![스타일 검색](using-page-inspector-in-visual-studio-2012/_static/image9.png)

    *선택한 요소의 스타일 및 소스 파일 검색*
11. 검사 설정/해제 포인터가 활성화 된 상태에서 마우스 포인터를 파란색 추천 막대 아래로 이동 하 고 절반 원을 클릭 합니다.

    ![요소 선택](using-page-inspector-in-visual-studio-2012/_static/image10.png "요소 선택")

    *요소 선택*
12. 스타일 창의 **. 주-콘텐츠** 그룹에서 **배경 이미지** 항목을 찾습니다. **배경 이미지** 를 **선택 취소** 하 고 어떻게 되는지 확인 합니다. 그러면 브라우저에 변경 내용이 즉시 반영 되 고 원이 숨겨집니다.

    > [!NOTE]
    > 페이지 검사기 스타일 탭에서 적용 하는 변경 내용은 원래 스타일 시트에 영향을 주지 않습니다. 스타일을 선택 취소 하거나 값을 원하는 횟수 만큼 변경할 수 있지만 페이지를 새로 고치면 복원 됩니다.

    ![CSS 스타일 사용 및 사용 안 함](using-page-inspector-in-visual-studio-2012/_static/image11.png "CSS 스타일 사용 및 사용 안 함")

    *CSS 스타일 사용 및 사용 안 함*
13. 이제 검사 모드를 사용 하 여 헤더의 '**여기에서 로고**' 텍스트를 클릭 합니다.
14. **스타일** 탭의 **. 사이트 제목** 그룹에서 **font-size** CSS 특성을 찾습니다. 특성 값을 두 번 클릭 하 고 2.3 em 값을 **3 em**으로 바꾼 다음 **enter**키를 누릅니다. 제목이 클수록 보입니다.

    ![페이지 검사기에서 CSS 값 변경](using-page-inspector-in-visual-studio-2012/_static/image12.png "페이지 검사기에서 CSS 값 변경")

    *페이지 검사기에서 CSS 값 변경*
15. 페이지 검사기의 오른쪽 창에 있는 **추적 스타일** 탭을 클릭 합니다. 이 방법은 선택 항목에 적용 된 모든 스타일을 특성 이름별로 정렬 하 여 표시 하는 대체 방법입니다.

    ![CSS 스타일 추적](using-page-inspector-in-visual-studio-2012/_static/image13.png)

    *선택한 요소의 CSS 스타일 추적*
16. 페이지 검사기의 또 다른 기능은 레이아웃 창입니다. 검사 모드를 사용 하 여 탐색 모음을 선택 하 고 오른쪽 창에서 **레이아웃** 탭을 클릭 합니다. 선택한 요소의 정확한 크기와 해당 오프셋, 여백, 안쪽 여백 및 테두리 크기가 표시 됩니다. 이 보기에서 값을 수정할 수도 있습니다.

    ![페이지 검사기의 요소 레이아웃](using-page-inspector-in-visual-studio-2012/_static/image14.png "페이지 검사기의 요소 레이아웃")

    *페이지 검사기의 요소 레이아웃*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a>작업 2-사진 갤러리에서 스타일 문제 찾기 및 수정

이전 버전의 Visual Studio에서 웹 페이지 문제를 진단 하려면 어떻게 해야 하나요? Internet Explorer 개발자 도구 또는 Firebug와 같이 Visual Studio IDE 외부에서 실행 되는 웹 디버깅 도구에 대해 잘 알고 있을 것입니다. 브라우저는 HTML, 스크립팅 및 스타일만 이해 하는 반면 기본 프레임 워크는 렌더링 될 HTML을 생성 합니다. 따라서 웹 페이지의 모양을 확인 하려면 전체 사이트를 배포 해야 하는 경우가 많습니다.

웹 사이트에서 문제를 검색 하 고 수정 하려는 경우 다음 단계를 수행 했을 수 있습니다.

1. Visual Studio에서 솔루션을 실행 하거나 웹 서버에 페이지를 배포 합니다.
2. 브라우저에서 사용 하는 개발자 도구를 열거나 소스 코드와 스타일을 열고 문제를 찾습니다. 관련 파일을 찾으려면 스타일 클래스의 이름을 사용 하 여 &quot;검색&quot; 또는 파일에서 검색&quot; 기능을 &quot;합니다.
3. 오류가 검색 되 면 웹 브라우저 및 서버를 중지 합니다.
4. 브라우저 캐시를 지웁니다.
5. 수정 사항을 적용 하려면 Visual Studio로 돌아갑니다. 테스트 하는 모든 단계를 반복 합니다.

ASP.NET MVC 4에는 실제 WYSIWYG가 없으므로 이후 단계에서 웹 응용 프로그램을 실행 하거나 배포한 후에 대부분의 스타일 문제가 감지 됩니다. 이제 페이지 검사기를 사용 하 여 솔루션을 실행 하지 않고 모든 페이지를 미리 볼 수 있습니다.

이 작업에서는 페이지 검사기를 사용 하 여 사진 갤러리 응용 프로그램의 일부 문제를 해결 합니다.

1. 페이지 검사기를 사용 하 여 헤더의 왼쪽에 있는 **레지스터** 와 **로그인** 링크를 찾습니다.

    링크는 오른쪽의 예상 위치에 표시 되지 않으며 글머리 기호 목록과 같이 표시 됩니다. 이제 링크를 오른쪽에 맞추고 그에 따라 스타일을 조정 합니다.

    ![등록 및 로그인 링크 찾기](using-page-inspector-in-visual-studio-2012/_static/image15.png "등록 및 로그인 링크 찾기")

    *등록 및 로그인 링크 찾기*
2. 토글 검사 모드 선택 된 상태에서 등록 링크를 클릭 하 여 해당 코드를 엽니다.

    링크의 소스 코드는 **loginpartial.cshtml 파일\_** 에 있으며, 첫 번째 위치에서 찾을 수 있는 위치에 해당 하는 및 \_레이아웃이 아닙니다. 올바른 소스 파일에 직접 배치 되었습니다.
3. **스타일** 탭에서 이러한 링크의 HTML 컨테이너인 **\<섹션 > #login** 항목을 찾아 클릭 합니다.

    **#Login** 스타일은를 클릭 한 후에 자동으로 **사이트 .css** 에 배치 됩니다. 코드도 이제 강조 표시 됩니다.

    ![CSS 스타일 선택](using-page-inspector-in-visual-studio-2012/_static/image16.png "CSS 스타일 선택")

    *CSS 스타일 선택*
4. 열기 및 닫기 문자를 제거 하 여 강조 표시 된 코드에서 **텍스트 맞춤** 특성의 주석 처리를 제거 하 고 **사이트 .css** 파일을 저장 합니다.

    페이지 검사기는 현재 페이지를 구성 하는 다른 모든 파일을 인식 하 고 이러한 파일이 변경 되 면이를 감지할 수 있습니다. 브라우저의 현재 페이지가 원본 파일과 동기화 되지 않을 때마다 경고를 표시 합니다.
5. 페이지 검사기 브라우저에서 주소 표시줄 아래에 있는 막대를 클릭 하 여 페이지를 다시 로드 합니다.

    ![페이지 다시 로드](using-page-inspector-in-visual-studio-2012/_static/image17.png)

    *페이지 다시 로드*

    링크는 이제 오른쪽에 있지만 여전히 글머리 기호 목록과 같습니다. 이제 글머리 기호를 제거 하 고 링크를 가로로 정렬 합니다.

    ![업데이트 된 페이지](using-page-inspector-in-visual-studio-2012/_static/image18.png)

    *업데이트 된 페이지*
6. 검사 모드를 사용 하 여 &quot;등록&quot;를 포함 하는 **&lt;li&gt;** 항목을 선택 하 고 &quot;링크를&quot; 합니다. 그런 다음 **&lt;섹션&gt; #login** 항목을 클릭 하 여 **스타일 css** 코드에 액세스 합니다.

    ![스타일 찾기](using-page-inspector-in-visual-studio-2012/_static/image19.png "스타일 찾기")

    *스타일 찾기*
7. **스타일 .css**에서 **#login li** 항목에 대 한 코드의 주석 처리를 제거 합니다. 추가 하는 스타일은 글머리 기호를 숨기고 항목이 가로로 표시 됩니다.

    ![로그인 링크의 스타일 다시 지정](using-page-inspector-in-visual-studio-2012/_static/image20.png "로그인 링크의 스타일 다시 지정")

    *로그인 링크의 스타일 다시 지정*
8. **스타일 .css** 파일을 저장 하 고 주소 아래에 있는 막대에서 한 번을 클릭 하 여 페이지를 다시 로드 합니다. 링크가 올바르게 표시 되는지 확인 합니다.

    ![오른쪽에 정렬 된 링크](using-page-inspector-in-visual-studio-2012/_static/image21.png "오른쪽에 정렬 된 링크")

    *오른쪽에 정렬 된 링크*
9. 마지막으로 헤더 제목을 변경 합니다. 검사 모드를 사용 하 여 **여기에서 로고** 를 클릭 하 고 해당 텍스트를 생성 하는 소스 코드를 가져옵니다.
10. 이제 **\_레이아웃**을 사용 하 고 있습니다. cshtml에서 '**로고를 여기**로 ' 텍스트를 '**사진 갤러리**'로 바꿉니다. 페이지 검사기 브라우저를 저장 하 고 업데이트 합니다.

    ![새 제목 할당](using-page-inspector-in-visual-studio-2012/_static/image22.png "새 제목 할당")

    *새 제목 할당*

    ![사진 갤러리 페이지](using-page-inspector-in-visual-studio-2012/_static/image23.png)

    *사진 갤러리 페이지가 업데이트 됨*
11. 마지막으로, **사진 갤러리** 프로젝트를 선택 하 고 **f5** 키를 눌러 앱을 실행 합니다. 모든 변경 내용이 예상 대로 작동 하는지 확인 합니다.

---

<a id="Exercise2"></a>

<a id="Exercise_2_Using_Page_Inspector_in_WebForms_Projects"></a>
### <a name="exercise-2-using-page-inspector-in-webforms-projects"></a>연습 2: WebForms 프로젝트에서 페이지 검사기 사용

이 연습에서는 페이지 검사기를 사용 하 여 WebForms 솔루션을 미리 보고 디버그 하는 방법을 알아봅니다. 웹 디버깅 프로세스를 용이 하 게 하는 페이지 검사기 기능에 대 한 자세한 내용은 도구에 대 한 간략 한 랩을 먼저 수행 합니다. 그런 다음 스타일 문제가 있는 웹 페이지에서 작업 합니다. 페이지 검사기를 사용 하 여 문제를 생성 하는 소스 코드를 찾고 수정 하는 방법을 배웁니다.

<a id="Ex2Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a>작업 1-페이지 검사기 탐색

이 작업에서는 사진 갤러리를 표시 하는 WebForms 프로젝트의 컨텍스트에서 페이지 검사기 기능을 사용 하는 방법에 대해 설명 합니다.

1. **Source/Ex2-WebForms/begin/** 폴더에 있는 **시작** 솔루션을 엽니다.

   1. 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.
   2. **NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.
   3. 마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.

      > [!NOTE]
      > NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다. NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다. 이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.
2. 솔루션 탐색기 **default.aspx 페이지를** 찾아 마우스 오른쪽 단추로 클릭 하 고 **페이지 검사기에서 보기**를 선택 합니다.

    ![페이지 검사기를 사용 하 여 default.aspx 열기](using-page-inspector-in-visual-studio-2012/_static/image24.png "페이지 검사기를 사용 하 여 default.aspx 열기")

    *페이지 검사기를 사용 하 여 default.aspx 열기*
3. 페이지 검사기 창은 Default.aspx를 표시 합니다.

    ![페이지 검사기에서 default.aspx 보기](using-page-inspector-in-visual-studio-2012/_static/image25.png "페이지 검사기에서 default.aspx 보기")

    *페이지 검사기에서 default.aspx 보기*

    페이지 검사기 도구는 Visual Studio 환경에 통합 되어 있습니다. 검사기에는 선택한 코드를 표시 하는 강력한 HTML 프로파일러와 함께 포함 된 브라우저가 포함 되어 있습니다. 페이지의 모양을 확인 하기 위해 솔루션을 실행할 필요는 없습니다.

    > [!NOTE]
    > 페이지 검사기 브라우저의 너비가 열린 페이지의 너비 보다 적으면 페이지가 제대로 표시 되지 않습니다. 이 경우 페이지 검사기의 너비를 조정 합니다.
4. 페이지 검사기에서 **파일** 탭을 클릭 합니다.

    렌더링 된 기본 페이지를 작성 하는 모든 원본 파일이 표시 됩니다. 이 기능은 특히 사용자 컨트롤 및 마스터 페이지를 사용 하 여 작업 하는 경우 모든 요소를 한눈에 식별 하는 데 유용 합니다. 각 파일을 탐색할 수도 있습니다.

    ![파일 탭](using-page-inspector-in-visual-studio-2012/_static/image26.png "파일 탭")

    *파일 탭*
5. 탭의 왼쪽에 있는 **토글 검사 모드** 단추를 클릭 합니다.

    이 도구를 사용 하 여 페이지의 요소를 선택 하 고 HTML 코드 및 .aspx 소스를 볼 수 있습니다.

    ![검사 모드 토글 단추](using-page-inspector-in-visual-studio-2012/_static/image27.png "검사 모드 토글 단추")

    *검사 모드 토글 단추*
6. 페이지 검사기 브라우저에서 페이지 요소 위로 마우스를 이동 합니다. 마우스 포인터를 렌더링 된 페이지의 특정 부분으로 이동 하는 동안 요소 형식이 표시 되 고 Visual Studio 편집기에서 해당 소스 태그나 코드가 강조 표시 됩니다.

    ![검사 모드 실행](using-page-inspector-in-visual-studio-2012/_static/image28.png "검사 모드 실행")

    *검사 모드 실행*

    > [!NOTE]
    > 페이지 검사기 창을 최대화 하지 마십시오. 그렇지 않으면 소스 코드를 표시 하는 미리 보기 탭을 볼 수 없습니다. 최대화 된 페이지 검사기의 요소를 클릭 하면 선택의 소스 코드가 표시 되지만 페이지 검사기 창이 숨겨집니다.

    **Default.aspx 파일에** 주의를 기울여야 하는 경우 선택한 요소를 생성 하는 소스 코드 부분이 강조 표시 됩니다. 이 기능은 긴 소스 파일의 버전을 용이 하 게 하 여 코드에 직접적이 고 빠르게 액세스할 수 있는 방법을 제공 합니다.

    ![요소 검사](using-page-inspector-in-visual-studio-2012/_static/image29.png "요소 검사")

    *요소 검사*
7. **설정/해제** 단추를 클릭 합니다 (html-html-검사 모드-html-![코드에서 렌더링-탐색기-브라우저-탐색기-브라우저에서).](using-page-inspector-in-visual-studio-2012/_static/image30.png "-Html-html-코드-렌더링-페이지-탐색-탐색기-브라우저를 선택 합니다.") )를 사용 하 여 커서를 사용 하지 않도록 설정 페이지 검사기.
8. **Html** 탭을 선택 하 여 페이지 검사기 브라우저에서 렌더링 된 html 코드를 표시 합니다.
9. HTML 코드에서 Koala 링크를 사용 하 여 목록 항목을 찾아 선택 합니다.

    코드를 선택 하면 해당 출력이 자동으로 브라우저에 강조 표시 됩니다. 이 기능은 HTML 블록이 페이지에서 렌더링 되는 방법을 확인 하는 데 유용 합니다.

    ![페이지에서 HTML 요소 선택](using-page-inspector-in-visual-studio-2012/_static/image31.png "페이지에서 HTML 요소 선택")

    *페이지에서 HTML 요소 선택*
10. 검사 모드 설정 **/해제** 단추를 클릭 하 여 *검사 모드* 를 사용 하도록 설정 하 고 탐색 모음을 클릭 합니다. HTML 코드의 오른쪽에 있는 스타일 창에 선택한 요소에 CSS 스타일이 적용 된 목록이 표시 됩니다.

    > [!NOTE]
    > 헤더가 사이트 레이아웃의 일부 이기 때문에 페이지 검사기는 사이트 .Master 파일도 열고 영향을 받는 코드의 세그먼트를 강조 표시 합니다.

    ![스타일 검색 WebForms](using-page-inspector-in-visual-studio-2012/_static/image32.png "선택한 요소의 스타일 및 소스 파일 검색")

    *선택한 요소의 스타일 및 소스 파일 검색*
11. 검사 설정/해제 포인터가 활성화 된 상태에서 마우스 포인터를 메뉴 모음 아래로 이동 하 고 빈 절반 원을 클릭 합니다.

    ![요소 선택](using-page-inspector-in-visual-studio-2012/_static/image33.png "요소 선택")

    *요소 선택*
12. 스타일 창의 **. 주-콘텐츠** 그룹에서 **배경 이미지** 항목을 찾습니다. **배경 이미지** 를 **선택 취소** 하 고 어떻게 되는지 확인 합니다. 그러면 브라우저에 변경 내용이 즉시 반영 되 고 원이 숨겨집니다.

    > [!NOTE]
    > 페이지 검사기 스타일 탭에서 적용 하는 변경 내용은 원래 스타일 시트에 영향을 주지 않습니다. 스타일을 선택 취소 하거나 값을 원하는 횟수 만큼 변경할 수 있지만 페이지를 새로 고치면 복원 됩니다.

    ![CSS styles2 사용 및 사용 안 함](using-page-inspector-in-visual-studio-2012/_static/image34.png "CSS 스타일 사용 및 사용 안 함")

    *CSS 스타일 사용 및 사용 안 함*
13. 이제 검사 모드를 사용 하 여 헤더**의 '** **여기에서 로고** ' 텍스트를 클릭 합니다.
14. **스타일** 탭의 **. 사이트 제목** 그룹에서 **font-size** CSS 특성을 찾습니다. 특성을 두 번 클릭 하 여 해당 값을 편집 합니다. 2\.3 em 값을 **3em**으로 바꾸고 enter 키를 누릅니다. 제목이 클수록 보입니다.

    ![Inspector2 페이지에서 CSS 값 변경](using-page-inspector-in-visual-studio-2012/_static/image35.png "페이지 검사기에서 CSS 값 변경")

    *페이지 검사기에서 CSS 값 변경*
15. 페이지 검사기의 오른쪽 창에 있는 **추적 스타일** 탭을 클릭 합니다. 이 방법은 선택 항목에 적용 된 모든 스타일을 특성 이름별로 정렬 하 여 표시 하는 대체 방법입니다.

    ![선택한 요소의 CSS 스타일 추적](using-page-inspector-in-visual-studio-2012/_static/image36.png "선택한 요소의 CSS 스타일 추적")

    *선택한 요소의 CSS 스타일 추적*
16. 페이지 검사기의 또 다른 기능은 레이아웃 창입니다. 검사 모드를 사용 하 여 탐색 모음을 선택 하 고 오른쪽 창에서 **레이아웃** 탭을 클릭 합니다. 선택한 요소의 정확한 크기와 해당 오프셋, 여백, 안쪽 여백 및 테두리 크기가 표시 됩니다. 이 보기에서 값을 수정할 수도 있습니다.

    ![페이지 검사기의 요소 레이아웃](using-page-inspector-in-visual-studio-2012/_static/image37.png "페이지 검사기의 요소 레이아웃")

    *페이지 검사기의 요소 레이아웃*

<a id="Ex2Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a>작업 2-사진 갤러리에서 스타일 문제 찾기 및 수정

이전 버전의 Visual Studio에서 웹 페이지 문제를 진단 하려면 어떻게 해야 하나요? Internet Explorer 개발자 도구 또는 Firebug와 같이 Visual Studio IDE 외부에서 실행 되는 웹 디버깅 도구에 대해 잘 알고 있을 것입니다. 브라우저는 HTML, 스크립팅 및 스타일만 이해 하는 반면 기본 프레임 워크는 렌더링 될 HTML을 생성 합니다. 따라서 웹 페이지의 모양을 확인 하려면 전체 사이트를 배포 해야 하는 경우가 많습니다.

웹 사이트에서 문제를 검색 하 고 수정 하려는 경우 다음 단계를 수행 했을 수 있습니다.

1. Visual Studio에서 솔루션을 실행 하거나 웹 서버에 페이지를 배포 합니다.
2. 브라우저에서 사용 하는 개발자 도구를 열거나 소스 코드와 스타일을 열고 문제를 찾습니다. 관련 파일을 찾으려면 스타일 클래스의 이름을 사용 하 여 &quot;검색&quot; 또는 파일에서 검색&quot; 기능을 &quot;합니다.
3. 오류가 검색 되 면 웹 브라우저 및 서버를 중지 합니다.
4. 브라우저 캐시를 지웁니다.
5. 수정 사항을 적용 하려면 Visual Studio로 돌아갑니다. 테스트 하는 모든 단계를 반복 합니다.

ASP.NET WebForms에는 실제 WYSIWYG가 없으므로 이후 단계에서 (실행 또는 배포 후) 일부 스타일 문제가 감지 됩니다. 이제 페이지 검사기를 사용 하 여 솔루션을 실행 하지 않고 모든 페이지를 미리 볼 수 있습니다.

이 작업에서는 사진 갤러리 응용 프로그램의 일부 문제를 해결 하는 데 페이지 검사기를 사용 합니다. 다음 단계에서는 헤더에서 몇 가지 간단한 스타일 지정 문제를 검색 하 고 신속 하 게 해결 합니다.

1. 페이지 검사를 사용 하 여 헤더의 왼쪽에 있는 **레지스터** 및 **로그인** 링크를 찾습니다.

    오른쪽의 예상 위치에는 링크가 표시 되지 않습니다. 이제 링크를 오른쪽에 맞추고 그에 맞게 스타일을 다시 조정 합니다.

    ![왼쪽에 위치 하는 로그인 링크](using-page-inspector-in-visual-studio-2012/_static/image38.png "왼쪽에 위치 하는 로그인 링크")

    *왼쪽에 위치 하는 로그인 링크*
2. 토글 검사 모드 선택 하 고 로그인 링크를 선택 하 여 해당 코드를 엽니다.

    링크 소스 코드는 첫 번째 위치에 있는 default.aspx 페이지가 아닌 **site.master** 파일에 위치 하는 것을 볼 수 있습니다. 올바른 소스 파일에 직접 배치 되었습니다.
3. **스타일** 탭에서 이러한 링크의 HTML 컨테이너인 **&lt;섹션&gt; #login** 항목을 찾아 클릭 합니다.

    **#Login** 스타일은를 클릭 한 후에 자동으로 **사이트 .css** 에 배치 됩니다. 코드도 이제 강조 표시 됩니다.

    ![CSS 스타일 선택](using-page-inspector-in-visual-studio-2012/_static/image39.png "CSS 스타일 선택")

    *CSS 스타일 선택*
4. 열기 및 닫기 문자를 제거 하 여 강조 표시 된 코드에서 **텍스트 맞춤** 특성의 주석 처리를 제거 하 고 **사이트 .css** 파일을 저장 합니다.

    페이지 검사기는 현재 페이지를 구성 하는 다른 모든 파일을 인식 하 고 이러한 파일이 변경 되 면이를 감지할 수 있습니다. 브라우저의 현재 페이지가 원본 파일과 동기화 되지 않을 때마다 경고를 표시 합니다.
5. 페이지 검사기 브라우저에서 주소 표시줄 아래에 있는 막대를 클릭 하 여 변경 내용을 저장 하 고 페이지를 다시 로드 합니다.

    ![페이지 다시 로드](using-page-inspector-in-visual-studio-2012/_static/image40.png)

    *페이지 다시 로드*

    링크는 이제 오른쪽에 있지만 여전히 글머리 기호 목록과 같습니다. 이제 글머리 기호를 제거 하 고 링크를 가로로 정렬 합니다.

    ![업데이트 된 페이지](using-page-inspector-in-visual-studio-2012/_static/image41.png)

    *업데이트 된 페이지*
6. 검사 모드를 사용 하 여 &quot;등록&quot;를 포함 하는 **&lt;li&gt;** 항목을 선택 하 고 &quot;링크를&quot; 합니다. 그런 다음 **&lt;섹션&gt; #login** 항목을 클릭 하 여 **스타일 css** 코드에 액세스 합니다.

    ![스타일 찾기](using-page-inspector-in-visual-studio-2012/_static/image42.png "스타일 찾기")

    *스타일 찾기*
7. **스타일 .css**에서 **#login li** 항목에 대 한 코드의 주석 처리를 제거 합니다. 추가 하는 스타일은 글머리 기호를 숨기고 항목이 가로로 표시 됩니다.

    ![로그인 링크의 스타일 다시 지정](using-page-inspector-in-visual-studio-2012/_static/image43.png "로그인 링크의 스타일 다시 지정")

    *로그인 링크의 스타일 다시 지정*
8. **스타일 .css** 파일을 저장 하 고 주소 아래에 있는 막대에서 한 번을 클릭 하 여 페이지를 다시 로드 합니다. 링크가 올바르게 표시 되는지 확인 합니다.

    ![오른쪽에 정렬 된 링크](using-page-inspector-in-visual-studio-2012/_static/image44.png "오른쪽에 정렬 된 링크")

    *오른쪽에 정렬 된 링크*
9. 마지막으로 헤더 제목을 변경 합니다. 모든 파일에서 '**로고 위치 '** 텍스트를 검색 하는 대신 검사 모드를 사용 하 여 텍스트를 클릭 하 고이를 생성 하는 소스 코드를 가져옵니다.

    ![사이트 제목 찾기](using-page-inspector-in-visual-studio-2012/_static/image45.png "사이트 제목 찾기")

    *사이트 제목 찾기*
10. 이제 **site.master**에서 '**로고를 여기**' 텍스트를 '**사진 갤러리**'로 바꿉니다. 페이지 검사기 브라우저를 저장 하 고 업데이트 합니다.

    ![사진 갤러리 페이지가 업데이트 됨](using-page-inspector-in-visual-studio-2012/_static/image46.png "사진 갤러리 페이지가 업데이트 됨")

    *사진 갤러리 페이지가 업데이트 됨*
11. 마지막으로 **f5** 키를 눌러 앱을 실행 합니다. 모든 변경 내용이 예상 대로 작동 합니다.

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습 실습을 완료 하면 브라우저에서 웹 사이트를 다시 빌드하고 실행할 필요 없이 페이지 검사기를 사용 하 여 웹 응용 프로그램을 미리 보는 방법을 학습 수 있습니다. 또한 렌더링 된 출력에서 소스 코드에 직접 액세스 하 여 버그를 신속 하 게 찾아 수정 하는 방법을 학습 있습니다.

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>부록 A: 웹에 대 한 Visual Studio Express 2012 설치

**[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)** 를 사용 하 여 웹 또는 다른 &quot;Express&quot; 버전 **에 대해 Microsoft Visual Studio Express 2012** 를 설치할 수 있습니다. 다음 지침에서는 *Microsoft 웹 플랫폼 설치 관리자*를 사용 하 여 *Visual studio Express 2012 for Web* 을 설치 하는 데 필요한 단계를 안내 합니다.

1. [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)로 이동 합니다. 또는 웹 플랫폼 설치 관리자를 이미 설치한 경우에는 웹 플랫폼 설치 관리자를 열고 <em>Microsoft AZURE SDK&quot;를 사용 하 여 웹 용 2012 Visual Studio Express</em> &quot;제품을 검색할 수 있습니다.
2. **지금 설치**를 클릭 합니다. **웹 플랫폼 설치 관리자** 가 없으면 먼저이를 다운로드 하 여 설치 하도록 리디렉션됩니다.
3. **웹 플랫폼 설치 관리자** 가 열리면 **설치** 를 클릭 하 여 설치를 시작 합니다.

    ![Visual Studio Express 설치](using-page-inspector-in-visual-studio-2012/_static/image47.png "Visual Studio Express 설치")

    *Visual Studio Express 설치*
4. 모든 제품의 라이선스 및 사용 조건을 읽고 **동의** 함을 클릭 하 여 계속 합니다.

    ![사용 조건 동의](using-page-inspector-in-visual-studio-2012/_static/image48.png)

    *사용 조건 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](using-page-inspector-in-visual-studio-2012/_static/image49.png)

    *설치 진행률*
6. 설치가 완료 되 면 **마침**을 클릭 합니다.

    ![설치 완료](using-page-inspector-in-visual-studio-2012/_static/image50.png)

    *설치 완료*
7. **끝내기** 를 클릭 하 여 웹 플랫폼 설치 관리자를 닫습니다.
8. 웹에 대 한 Visual Studio Express를 열려면 **시작** 화면으로 이동 하 &quot;**VS Express**&quot;작성을 시작한 후 **VS Express for Web** 타일을 클릭 합니다.

    ![VS Express for Web 타일](using-page-inspector-in-visual-studio-2012/_static/image51.png)

    *VS Express for Web 타일*
