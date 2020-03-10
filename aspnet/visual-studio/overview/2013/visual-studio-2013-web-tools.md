---
uid: visual-studio/overview/2013/visual-studio-2013-web-tools
title: '실습: 웹 도구 Visual Studio 2013 | Microsoft Docs'
author: rick-anderson
description: Visual Studio는의 뛰어난 개발 환경입니다. NET 기반 Windows 및 웹 프로젝트. 여기에는 쉽게 사용할 수 있는 강력한 텍스트 편집기가 포함 되어 있습니다.
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 09e82351-816b-402d-acd1-0f9ac6901d16
msc.legacyurl: /visual-studio/overview/2013/visual-studio-2013-web-tools
msc.type: authoredcontent
ms.openlocfilehash: 2fb987dd9b26ad9f0e8a88fd881bde4505ec4148
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505007"
---
# <a name="hands-on-lab-visual-studio-2013-web-tools"></a>실습: 웹 도구 Visual Studio 2013

[웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 교육 키트 다운로드](https://aka.ms/webcamps-training-kit)

> Visual Studio는의 뛰어난 개발 환경입니다. NET 기반 Windows 및 웹 프로젝트. 여기에는 프로젝트 없이 독립 실행형 파일을 쉽게 편집할 수 있는 강력한 텍스트 편집기가 포함 되어 있습니다.
> 
> Visual Studio는 각 파일을 편집할 때 전체 기능을 갖춘 구문 분석 트리를 유지 관리 합니다. 이를 통해 Visual Studio에서 뛰어난 자동 완성 및 문서 기반 작업을 제공 하 고 개발 환경을 훨씬 빠르고 즐겁게 만들 수 있습니다. 이러한 기능은 HTML 및 CSS 문서에서 특히 강력한 기능입니다.
> 
> 이러한 모든 기능을 확장에 사용할 수 있으므로 요구 사항에 맞게 강력한 새 기능으로 편집기를 쉽게 확장할 수 있습니다. Web Essentials는 Visual Studio에 대 한 대부분의 웹 관련 향상 된 기능 모음입니다. 여기에는 많은 새 IntelliSense 완성 (특히 CSS의 경우), 새로운 브라우저 링크 기능, JavaScript 파일용 자동 JSHint, HTML 및 CSS에 대 한 새로운 경고, 최신 웹 개발에 필수적인 기타 많은 기능이 포함 되어 있습니다.
> 
> 모든 샘플 코드와 코드 조각은 [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)에서 사용할 수 있는 웹 캠프 교육 키트에 포함 되어 있습니다.

<a id="Overview"></a>
## <a name="overview"></a>개요

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서는 다음 방법에 대해 알아봅니다.

- 풍부한 HTML5 코드 조각 및 Zen 코딩 등 Web Essentials에 포함 된 새 HTML 편집기 기능 사용
- 색 선택 및 브라우저 매트릭스 도구 설명과 같은 웹 Essentials에 포함 된 새 CSS 편집기 기능 사용
- 모든 HTML 요소에 대 한 파일 및 IntelliSense에 압축 풀기와 같은 웹 Essentials에 포함 된 새 JavaScript 편집기 기능을 사용 합니다.
- 브라우저 링크를 사용 하 여 브라우저와 Visual Studio 간 데이터 교환

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>사전 요구 사항

이 실습 실습을 완료 하려면 다음이 필요 합니다.

- [Microsoft Visual Studio Professional 2013](https://www.microsoft.com/visualstudio/) 이상
- [웹 Essentials 2013](http://vswebessentials.com/)
- [Google Chrome](https://www.google.com/chrome/)

<a id="Setup"></a>
### <a name="setup"></a>설치 프로그램

이 실습 랩에서 연습을 실행 하려면 먼저 환경을 설정 해야 합니다.

1. Windows 탐색기 창을 열고 랩의 **원본** 폴더로 이동 합니다.
2. **Setup.exe** 를 마우스 오른쪽 단추로 클릭 하 고 **관리자 권한으로 실행** 을 선택 하 여 환경을 구성 하는 설치 프로세스를 시작 하 고이 랩에 대 한 Visual Studio 코드 조각을 설치 합니다.
3. 사용자 계정 컨트롤 대화 상자가 표시 되 면 계속 하려면 작업을 확인 합니다.

> [!NOTE]
> 설치 프로그램을 실행 하기 전에이 랩에 대 한 모든 종속성을 확인 했는지 확인 합니다.

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>코드 조각 사용

랩 문서 전체에서 코드 블록을 삽입 하 라는 지침이 표시 됩니다. 사용자 편의를 위해이 코드의 대부분은 Visual Studio 2013 내에서 액세스할 수 있는 Visual Studio Code 코드 조각으로 제공 되며,이를 수동으로 추가 하지 않아도 됩니다.

> [!NOTE]
> 각 연습에는 각 연습을 서로 독립적으로 수행할 수 있는 연습 **시작** 폴더에 있는 시작 솔루션이 있습니다. 연습 중에 추가 된 코드 조각은 이러한 시작 솔루션에서 누락 되었으며, 연습을 완료할 때까지 작동 하지 않을 수 있습니다. 연습에 대 한 소스 코드 내에서 해당 연습의 단계를 완료 하 여 생성 된 코드를 포함 하는 Visual Studio 솔루션을 포함 하는 **끝** 폴더를 찾을 수도 있습니다. 이 실습 랩을 통해 작업할 때 추가 도움이 필요한 경우 이러한 솔루션을 지침으로 사용할 수 있습니다.

---

<a id="Exercises"></a>
## <a name="exercises"></a>실습

이 실습 랩에는 다음 연습이 포함 되어 있습니다.

1. [브라우저 링크 및 Web Essentials 작업](#Exercise1)
2. [코드 조각 및 IntelliSense를 활용 합니다.](#Exercise2)

> [!NOTE]
> Visual Studio를 처음 시작 하는 경우 미리 정의 된 설정 컬렉션 중 하나를 선택 해야 합니다. 미리 정의 된 각 컬렉션은 특정 개발 스타일에 맞게 디자인 되 고 창 레이아웃, 편집기 동작, IntelliSense 코드 조각 및 대화 상자 옵션을 결정 합니다. 이 실습의 절차에서는 **일반 개발 설정** 컬렉션을 사용 하는 경우 Visual Studio에서 지정 된 작업을 수행 하는 데 필요한 작업을 설명 합니다. 개발 환경에 대해 다른 설정 컬렉션을 선택 하는 경우 고려해 야 하는 단계에 차이가 있을 수 있습니다.

<a id="Exercise1"></a>
### <a name="exercise-1-working-with-browser-link-and-web-essentials"></a>연습 1: 브라우저 링크 및 Web Essentials 작업

**Web Essentials** 는 최신 웹 개발을 위한 다양 한 유용한 기능을 추가 하는 Visual Studio 확장으로, 대부분 웹 개발 환경을 훨씬 빠르고 편리 하 게 만드는 데 주력 합니다. Visual Studio의 확장 갤러리에서 Web Essentials를 설치할 수 있습니다.

**브라우저 링크** 는 VISUAL studio IDE와 웹 응용 프로그램 및 visual studio 간에 데이터를 교환 하기 위해 열려 있는 모든 브라우저 사이에 채널을 제공 하는 Visual Studio 2013에 포함 된 새로운 기능입니다. 웹 Essentials는 브라우저 링크를 도구로 확장 하 여 브라우저에서 직접 웹 페이지의 CSS 스타일과 DOM 개체 모델을 조작 합니다.

이 연습에서는 간단한 퀴즈 페이지를 개선 하기 위해 **Web Essentials** 및 **브라우저 링크** 에서 지 원하는 기능 중 일부를 살펴보겠습니다.

<a id="Ex1Task1"></a>
#### <a name="task-1---running-the-project-in-multiple-browsers"></a>작업 1-여러 브라우저에서 프로젝트 실행

이 태스크에서는 여러 브라우저에서 한 번에 실행 되도록 웹 응용 프로그램을 구성 하며,이는 브라우저 간 테스트에 유용 합니다.

1. **Microsoft Visual Studio**를 엽니다.
2. **파일** 메뉴에서 열기를 선택 합니다.  **프로젝트/솔루션** ... 랩의 **원본** 폴더 (C:\WebCampsTK\HOL\VSWebTooling\Source)에서 **Ex1-WorkingwithBrowserLinkandWebEssentials\Begin** 로 이동 합니다. **시작 .sln** 을 선택 하 고 **열기**를 클릭 합니다.
3. Visual Studio 도구 모음에서 브라우저 메뉴를 확장 하 고 **찾아보기**...를 선택 합니다.

    ![메뉴 옵션으로 찾아보기](visual-studio-2013-web-tools/_static/image1.png "찾아보기 ... 브라우저 메뉴")

    *메뉴 옵션으로 찾아보기*
4. **브라우저** 선택 대화 상자에서 **CTRL** 키를 누른 상태에서 **Google Chrome** 및 **Internet Explorer** 를 모두 선택 하 고 **기본값으로 설정**을 클릭 합니다.

    ![찾아보기 대화 상자](visual-studio-2013-web-tools/_static/image2.png "찾아보기 대화 상자")

    *여러 기본 브라우저 선택*
5. 이제 Google Chrome과 Internet Explorer가 모두 기본 브라우저로 표시 되어야 합니다. **취소**를 클릭하여 대화 상자를 닫습니다.

    ![Google Chrome 및 Internet Explorer를 기본 브라우저로](visual-studio-2013-web-tools/_static/image3.png "Google Chrome 및 Internet Explorer 기본 브라우저")

    *Google Chrome 및 Internet Explorer를 기본 브라우저로*

    > [!NOTE]
    > 기본 브라우저를 구성한 후 브라우저 메뉴에서 **다중 브라우저** 옵션이 선택 됩니다.
    > 
    > ![여러 브라우저](visual-studio-2013-web-tools/_static/image4.png "여러 브라우저")
6. **Ctrl** + **f5** 키를 눌러 디버깅 하지 않고 응용 프로그램을 실행 합니다.
7. 두 브라우저 창이 모두 열려 있는 경우 두 브라우저의 업데이트를 동시에 표시 하기 위해 둘 중 하나를 다른 창 위에 놓습니다. 브라우저는 밝은 파란색 사각형이 있는 웹 페이지를 표시 합니다.

    ![브라우저 하나에 다른 브라우저 배치](visual-studio-2013-web-tools/_static/image5.png "브라우저 하나에 다른 브라우저 배치")

    *브라우저 하나에 다른 브라우저 배치*
8. 브라우저를 닫지 마세요. 이러한 작업은 다음 작업에서 사용 합니다.

<a id="Ex1Task2"></a>
#### <a name="task-2---using-zen-coding-to-create-html-elements"></a>작업 2-Zen 코딩을 사용 하 여 HTML 요소 만들기

**Zen 코딩** 은 고속 HTML, XML, XSL (또는 기타 구조화 된 코드 형식) 코딩 및 편집을 위한 편집기 플러그 인입니다. 이 플러그 인의 핵심은 CSS 선택기와 유사한 식 (HTML 코드)을 확장 하는 데 사용할 수 있는 강력한 약어 엔진입니다. Zen 코딩은 CSS 스타일 선택기 구문을 사용 하 여 HTML을 신속 하 게 작성 하는 방법입니다.

이 연습에서는 Web Essentials에서 제공 하는 Zen 코딩 기능을 사용 하 여 질문의 옵션을 나타내는 HTML 단추를 생성 합니다.

1. Visual Studio로 다시 전환 합니다.
2. **보기** | **홈** 폴더에 있는 **인덱스 cshtml** 파일을 엽니다.
3. **&lt;!--TODO:** 다음 코드를 사용 하 여 주석&gt;하 고 **tab**키를 누릅니다.

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample1.css)]
4. HTML로 코드를 확장 해야 합니다.

    ![확장 된 HTML](visual-studio-2013-web-tools/_static/image6.png "확장 된 HTML")

    *확장 된 HTML*

    > [!NOTE]
    > Zen 코딩 구문에 대해 자세히 알아보려면 다음 [문서](http://www.johnpapa.net/zen-coding-in-visual-studio-2012/)를 참조 하세요.
5. 두 브라우저를 모두 업데이트 하려면 **연결 된 브라우저 새로 고침** 단추를 클릭 합니다.

    ![연결 된 브라우저 새로 고침](visual-studio-2013-web-tools/_static/image7.png "연결 된 브라우저 새로 고침")

    *연결 된 브라우저 새로 고침*

    ![Internet Explorer-4 개의 단추로 업데이트 된 페이지](visual-studio-2013-web-tools/_static/image8.png "Internet Explorer-4 개의 단추로 업데이트 된 페이지")

    *Internet Explorer-4 개의 단추로 업데이트 된 페이지*

    ![Google Chrome-4 개의 단추로 업데이트 된 페이지](visual-studio-2013-web-tools/_static/image9.png "Google Chrome-4 개의 단추로 업데이트 된 페이지")

    *Google Chrome-4 개의 단추로 업데이트 된 페이지*
6. Visual Studio로 다시 전환 합니다.
7. 페이지에 단추를 추가 했지만 여전히 템플릿 질문을 추가 해야 합니다. 이렇게 하려면 **Lorem Ipsum generator**라는 웹 Essentials의 새로운 기능을 사용 합니다. **클래스** 특성이 **front**인 **div** 요소를 찾습니다.
8. 다음 코드를 **div**의 첫 번째 자식 요소로 추가 하 고 **tab**키를 누릅니다.

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample2.css)]
9. HTML로 코드를 확장 해야 합니다.

    ![Lorem Ipsum 자동 생성](visual-studio-2013-web-tools/_static/image10.png "Lorem Ipsum 자동 생성")

    *Lorem Ipsum 자동 생성*

    > [!NOTE]
    > Zen 코딩의 일부로 이제 HTML 편집기에서 직접 Lorem Ipsum 코드를 생성할 수 있습니다. **Lorem** 를 입력 하 고 **TAB** 키를 누르면 30 단어 lorem Ipsum 텍스트가 삽입 됩니다. 예를 들어 *lorem10* 는 10 개의 Lorem Ipsum 단어를 삽입 합니다.
10. **Lorem Pixel generator**라는 웹 Essentials의 또 다른 새로운 기능을 사용 하 여 질문의 맨 위에 로고를 추가 합니다. **컨테이너** 를 **클래스** 값으로 사용 하 여 다음 코드를 **div** 요소의 첫 번째 자식 요소로 추가 하 고 **tab**키를 누릅니다.

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample3.css)]
11. 코드가 HTML로 확장 됩니다.

    ![자동 생성 되는 Lorem 픽셀](visual-studio-2013-web-tools/_static/image11.png "자동 생성 되는 Lorem 픽셀")

    *자동 생성 되는 Lorem 픽셀*

    > [!NOTE]
    > Zen 코딩의 일부로 HTML 편집기에서 직접 Lorem 픽셀 코드를 생성할 수도 있습니다. **200 x 200-동물** 및 적중 **탭** 을 입력 하면 동물의 200 x 200 이미지가 포함 된 **img** 태그가 삽입 됩니다. 자세한 내용은 [Lorem 픽셀](http://www.lorempixel.com)을 참조 하세요.
12. 두 브라우저를 모두 업데이트 하려면 **연결 된 브라우저 새로 고침** 단추를 클릭 합니다.

    ![Internet Explorer-자동으로 생성 되는 이미지 및 텍스트](visual-studio-2013-web-tools/_static/image12.png "Internet Explorer-자동으로 생성 되는 이미지 및 텍스트")

    *Internet Explorer-자동으로 생성 되는 이미지 및 텍스트*

    ![Google Chrome-자동으로 생성 되는 이미지 및 텍스트](visual-studio-2013-web-tools/_static/image13.png "Google Chrome-자동으로 생성 되는 이미지 및 텍스트")

    *Google Chrome-자동으로 생성 되는 이미지 및 텍스트*

    > [!NOTE]
    > 코드 조각을 추가할 때 이미지를 임의로 선택 하므로 브라우저에 표시 되는 이미지는 다를 수 있습니다.
13. 브라우저를 닫지 마세요. 이러한 작업은 다음 작업에서 사용 합니다.

<a id="Ex1Task3"></a>
#### <a name="task-3---updating-a-style-property"></a>작업 3-스타일 속성 업데이트

이 작업에서는 브라우저 링크의 **검사 모드** 기능을 사용 하 여 특정 DOM 요소가 생성 되는 정확한 위치를 검색 한 다음 Web Essentials에서 제공 하는 색 선택기를 사용 하 여 해당 요소의 color 속성을 업데이트 합니다.

1. Internet Explorer 브라우저에서 Alt **키를 눌러 검사** 모드를 **사용 하도록 설정 하려면** **ALT** +  + 합니다.
2. 연한 파란색 테두리 위로 포인터를 이동 하 고를 클릭 합니다.

    ![연한 파란색 테두리 위로 포인터 이동](visual-studio-2013-web-tools/_static/image14.png "연한 파란색 테두리 위로 포인터 이동")

    *연한 파란색 테두리 위로 포인터 이동*
3. Visual Studio로 다시 전환 합니다. 브라우저에서 선택한 HTML 요소가 Visual Studio HTML 편집기 에서도 선택 되어 있는지 확인 합니다.

    ![Visual Studio HTML 편집기에서 선택 된 HTML 요소](visual-studio-2013-web-tools/_static/image15.png "Visual Studio HTML 편집기에서 선택 된 HTML 요소")

    *Visual Studio HTML 편집기에서 선택 된 HTML 요소*
4. 이제 선택한 요소의 스타일을 변경 하기 위해 **front** CSS 클래스를 업데이트 합니다. 이렇게 하려면 **CTRL** + **를** 눌러 검색 **탐색** 상자를 엽니다. **Site .css** 를 입력 하 고 **enter** 키를 눌러 파일을 엽니다.

    ![파일 사이트 .css를 여는 경우](visual-studio-2013-web-tools/_static/image16.png "파일 사이트 .css를 여는 경우")

    *파일 사이트 .css를 여는 경우*
5. **Ctrl** + **F** 를 누르고 **. 대칭 이동-container.** 를 입력 하 여 CSS 선택기를 찾습니다.
6. 클래스의 border 속성에서 연한 파란색 사각형을 클릭 하 여 색 선택기를 엽니다.

    ![색 선택 열기](visual-studio-2013-web-tools/_static/image17.png "색 선택 열기")

    *색 선택 열기*
7. 펼침 단추를 클릭 하 여 색 선택기를 확장 하 고 새 색을 선택 합니다.

    ![색 선택 확장](visual-studio-2013-web-tools/_static/image18.png "색 선택 확장")

    *색 선택 확장*
8. **Ctrl** + **alt** ** + 를** 눌러 연결 된 브라우저를 새로 고칩니다.
9. Internet Explorer로 전환 하 고 테두리 색이 변경 된 방식을 확인 합니다.

    ![Internet Explorer-테두리 색이 업데이트 됨](visual-studio-2013-web-tools/_static/image19.png "Internet Explorer-테두리 색이 업데이트 됨")

    *Internet Explorer-테두리 색이 업데이트 됨*
10. Google Chrome으로 전환 하 고 테두리 색이 변경 된 방식을 확인 합니다.

    ![Google Chrome-테두리 색이 업데이트 됨](visual-studio-2013-web-tools/_static/image20.png "Google Chrome-테두리 색이 업데이트 됨")

    *Google Chrome-테두리 색이 업데이트 됨*
11. Visual Studio로 다시 전환 합니다.
12. **Btn** 선택기를 찾으려면 **Site .css** 파일의 끝으로 이동 하 고 **CTRL** + **F** 를 누릅니다.
13. **-Webkit** 속성은 녹색으로 밑줄이 그어집니다.

    ![-webkit-btn selector의 radius 속성](visual-studio-2013-web-tools/_static/image21.png "-webkit-btn selector의 radius 속성")

    *-webkit-btn selector의 radius 속성*
14. **-Webkit** 속성에 캐럿을 추가 합니다. 속성의 첫 번째 단어의 첫 문자 아래에 파란색 선이 표시 됩니다. **스마트 태그**입니다.
15. **Ctrl** + 를 누릅니다 **.** 제안 메뉴를 열고 **누락 된 표준 속성 추가 (테두리-반경)** 를 클릭 합니다.

    ![누락 된 표준 속성 제안 추가](visual-studio-2013-web-tools/_static/image22.png "누락 된 표준 속성 제안 추가")

    *누락 된 표준 속성 제안 추가*
16. **테두리-반경** 속성은 CSS 규칙에 자동으로 추가 됩니다.

    ![누락 된 표준 속성 추가 됨](visual-studio-2013-web-tools/_static/image23.png "누락 된 표준 속성 추가 됨")

    *누락 된 표준 속성 추가 됨*
17. 포인터를 **테두리-radius** 속성 위로 이동 하 여 **브라우저 매트릭스 도구 설명을**표시 합니다. **브라우저 매트릭스 도구 설명** 에는 각 브라우저에서 속성의 가용성이 표시 됩니다.

    ![브라우저 매트릭스 도구 설명](visual-studio-2013-web-tools/_static/image24.png "브라우저 매트릭스 도구 설명")

    *브라우저 매트릭스 도구 설명*
18. **테두리-반경** 속성의 값은 여전히 밑줄이 그어집니다. 포인터를 값 위로 이동 하 여 경고 메시지를 표시 합니다.

    ![테두리-반지름 속성 값 경고](visual-studio-2013-web-tools/_static/image25.png "테두리-반지름 속성 값 경고")

    *테두리-반지름 속성 값 경고*
19. 도구 설명에서 제안 하는 대로 **테두리-반지름** 속성 값의 단위를 제거 합니다.
20. **테두리 반경** 은 테두리 모퉁이가 둥근 정도를 정의 하는 표준 속성입니다. CSS 규칙에서 **-webkit** 속성 및 값을 제거할 수 있습니다.
21. **단어 줄 바꿈** 속성에 캐럿을 배치 하 고 스마트 태그가 아래에도 표시 되는지 확인 합니다.
22. 메뉴를 열고 누락 된 **공급 업체 특성 추가**를 클릭 합니다.

    ![누락 된 공급 업체 세부 제안 추가](visual-studio-2013-web-tools/_static/image26.png "누락 된 공급 업체 세부 제안 추가")

    *누락 된 공급 업체 세부 제안 추가*
23. **---단어 래핑** 속성은 CSS 규칙에 자동으로 추가 됩니다.

    ![공급 업체별 속성 추가 됨](visual-studio-2013-web-tools/_static/image27.png "공급 업체별 속성 추가 됨")

    *공급 업체별 속성 추가 됨*

<a id="Ex1Task4"></a>
#### <a name="task-4---updating-the-html-code-from-the-browser"></a>작업 4-브라우저에서 HTML 코드 업데이트

이 작업에서는 브라우저 링크의 **디자인 모드** 기능을 사용 하 여 브라우저에서 DOM 개체를 편집 하 고 Visual STUDIO의 HTML 소스 파일에 변경 내용을 전송 합니다.

1. Google Chrome에서 **ctrl** + **alt** + **D** 를 눌러 디자인 모드를 사용 하도록 설정 합니다.
2. 포인터를 **Lorem Ipsum dolor sit amet** 레이블 위로 이동 하 고를 클릭 합니다.

    ![질문 편집](visual-studio-2013-web-tools/_static/image28.png "질문 편집")

    *질문 편집*
3. 커서가 표시 됩니다. *더 긴 질문을 작성할 때*원래 텍스트를 어떻게 표시 되는지 바꾸고 **ESC** 키를 눌러 디자인 모드를 종료 합니다.

    ![수정한 질문](visual-studio-2013-web-tools/_static/image29.png "수정한 질문")

    *수정한 질문*
4. 아직 열지 않은 경우 Visual Studio로 다시 전환 하 고, **Index. cshtml**를 엽니다. **&lt;p&gt;** 요소의 내부 텍스트가 업데이트 된 것을 확인할 수 있습니다.

    ![HTML 페이지의 업데이트 된 질문](visual-studio-2013-web-tools/_static/image30.png "HTML 페이지의 업데이트 된 질문")

    *HTML 페이지의 업데이트 된 질문*

<a id="Ex1Task5"></a>
#### <a name="task-5---reviewing-seo-related-warnings"></a>작업 5-SEO 관련 경고 검토

SEO ( **검색 엔진 최적화** )는 검색 엔진의 결과 목록에서 웹 사이트 순위를 높게 만드는 프로세스입니다. 사이트 순위가 높을수록 더 일관 되 게 표시 되는 사이트의 방문자가 검색 엔진에서 얻을 수 있습니다. Web Essentials는 HTML을 검사 하 고 발견 된 문제를 보고 하 고 문제를 해결 하기 위한 지원을 제공 하는 분석 도구를 통합 합니다.

1. **보기** 메뉴로 이동 하 고 **오류 목록** 를 클릭 하 여 **오류 목록** 창을 엽니다.

    ![보기 메뉴의 오류 목록](visual-studio-2013-web-tools/_static/image31.png "보기 메뉴의 오류 목록")

    *보기 메뉴의 오류 목록*
2. 페이지 설명에 대 한 **&lt;meta&gt;** 태그가 없음을 알리는 SEO 경고가 발생 합니다. SEO 경고 항목을 두 번 클릭 하 여 수정 합니다.

    ![오류 목록 창](visual-studio-2013-web-tools/_static/image32.png "오류 목록 창")

    *오류 목록 창*
3. **Web Essentials** 대화 상자에서 **예** 를 클릭 하 여 메타&gt; 태그 &lt;설명을 삽입 합니다.

    ![Web Essentials 대화 상자](visual-studio-2013-web-tools/_static/image33.png "Web Essentials 대화 상자")

    *Web Essentials 대화 상자*
4. **\_레이아웃** 에 대 한 편집기가 열리고 **&lt;META&gt;** 태그가 HTML 파일의 **head** 섹션에 자동으로 추가 됩니다.

    ![_Layout 페이지에 자동으로 추가 되는 메타 태그](visual-studio-2013-web-tools/_static/image34.png "_Layout 페이지에 자동으로 추가 되는 메타 태그")

    *\_레이아웃 페이지에 메타 태그가 자동으로 추가 됨*
5. **Content** 특성의 값을 *GeekQuiz* 로 변경 하 고 파일을 저장 합니다.

<a id="Exercise2"></a>
### <a name="exercise-2-taking-advantage-of-code-snippets-and-intellisense"></a>연습 2: 코드 조각 및 IntelliSense 활용

Web Essentials를 사용 하 여 HTML 편집기는 추가 기능으로 확장 되었습니다. 이 연습에서는 웹 응용 프로그램을 개발할 때 도움이 되는 몇 가지 새로운 기능을 확인할 수 있습니다.

<a id="Ex2Task1"></a>
#### <a name="task-1---using-intellisense-in-html-documents"></a>작업 1-HTML 문서에서 IntelliSense 사용

이 작업에 표시 되는 첫 번째 새 기능은 **동적 IntelliSense**라고 합니다. 동적 IntelliSense는 다른 태그 및 특성을 읽어 사용할 수 있는 id를 유추 합니다.

이 작업에서는 레이블과 입력 필드를 포함 하는 새 HTML 폼 요소를 만듭니다. 그런 다음 레이블에 **대 한** 특성을 추가 하 여 입력에 바인딩합니다. 범위에 있는 입력의 id를 기반으로 IntelliSense 제안이 표시 됩니다.

1. **웹에 대해 Visual Studio Express 2013** 을 열고 **Source/Ex2-TakingAdvantageofCodeSnippetsandIntelliSense/begin** 폴더에 있는 **시작 .sln** 솔루션을 엽니다. 또는 이전 연습에서 얻은 솔루션을 계속 사용할 수 있습니다.
2. **솔루션 탐색기**에서 **보기** | **홈** 폴더에 있는 **인덱스 cshtml** 파일을 엽니다.
3. **&lt;section&gt;** 요소 안에 다음 폼을 추가 합니다.

    (코드 조각- *VisualStudio2013WebTooling* - *Ex2* - *양식*)

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample4.html)]
4. 입력 태그 앞에는 필드에 대 한 설명이 포함 된 레이블 앞에와 야 합니다. 입력 태그 앞에 다음 레이블을 추가 합니다.

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample5.html)]
5. **&lt;레이블의** **for** 특성&gt;레이블이 바인딩되는 폼 요소를 지정 합니다. 특성의 값은 관련 된 요소의 id와 같아야 합니다. **For** 특성을 **&lt;label&gt;** 요소에 추가 합니다. 다음 그림에 표시 된 것 처럼 &quot;이름&quot; 값은 동일한 범위 (바깥쪽 **&lt;폼&gt;** ) 내의 요소 id를 기준으로 IntelliSense 상자에 표시 됩니다.

    ![IntelliSense에서 id 표시](visual-studio-2013-web-tools/_static/image35.png "IntelliSense에서 id 표시")

    *IntelliSense에서 id 표시*
6. 최근 추가 된 **&lt;폼&gt;** 요소 및 해당 콘텐츠를 삭제 합니다.

<a id="Ex2Task2"></a>
#### <a name="task-2---using-html-code-snippets"></a>작업 2-HTML 코드 조각 사용

HTML5에는 25 개가 넘는 새 의미 태그가 도입 되었습니다. Visual Studio에는 이러한 태그에 대 한 IntelliSense 지원이 이미 있지만 Visual Studio 2013 새 코드 조각을 추가 하 여 더 빠르고 쉽게 태그를 작성할 수 있습니다. 이러한 태그는 복잡 하지 않지만 *오디오* 태그에 대 한 올바른 코덱 대체를 추가 하는 것과 같이 몇 가지 사소한 미묘한와 함께 제공 됩니다. 이 작업에서는 audio 태그에 대 한 HTML 코드 조각이 표시 됩니다.

1. Aud 파일에서 다음 그림에 표시 된 것 처럼 **&lt;섹션&gt;** 요소 내부에 **&lt;** 을 **입력 합니다.**

    ![Audio 요소 삽입](visual-studio-2013-web-tools/_static/image36.png "Audio 요소 삽입")

    *Audio 요소 삽입*
2. **Tab** 키를 두 번 눌러 다음 코드가 페이지에 추가 되 고 커서가 첫 번째 소스의 **src** 특성에 배치 되는 방식을 확인 합니다.

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample6.html)]

    > [!NOTE]
    > **TAB** 키를 두 번 누르면 코드 조각이 삽입 됩니다. 오디오 조각은 지원 향상을 위한 두 개의 소스 파일과 함께 *오디오* 태그의 표준 사용을 보여 줍니다.
3. WebCampsTV Katana show: [http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3](http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3)에 대 한 다음 링크를 사용 하 여 두 번째 줄을 삭제 하 고 첫 번째 줄의 소스를 업데이트 합니다. 결과 코드는 다음과 같습니다.

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample7.html)]

    > [!NOTE]
    > 원본 파일 *KatanaProject. mp3* 를 예로 사용 합니다. 원하는 경우 다른 원본을 사용할 수 있습니다.
4. **Ctrl** + **S** 를 눌러 파일을 저장 합니다.
5. **Ctrl** + **f5** 키를 눌러 응용 프로그램을 시작 합니다.
6. 오디오 플레이어가 응용 프로그램에 추가 되었음을 확인 합니다.

    ![Internet Explorer의 오디오 플레이어](visual-studio-2013-web-tools/_static/image37.png "Internet Explorer의 오디오 플레이어")

    *Internet Explorer의 오디오 플레이어*

    ![Google Chrome의 오디오 플레이어](visual-studio-2013-web-tools/_static/image38.png "Google Chrome의 오디오 플레이어")

    *Google Chrome의 오디오 플레이어*
7. 브라우저를 닫지 마세요. 이러한 작업은 다음 작업에서 사용 합니다.

<a id="Ex2Task3"></a>
#### <a name="task-3---using-intellisense-in-javascript-documents"></a>작업 3-JavaScript 문서에서 IntelliSense 사용

Web Essentials 2013를 사용 하는 경우 스타일 시트와 HTML 페이지는 Id 및 클래스 이름 목록을 생성 합니다. 이 작업에서는 이러한 목록이 Web Essentials 2013에서 JavaScript IntelliSense 지원을 개선 하는 방법에 대해 설명 합니다.

1. **Index cshtml** 파일에서 다음 코드를 추가 하 여 JavaScript 코드에 대 한 **스크립트** 태그를 정의 합니다.

    [!code-cshtml[Main](visual-studio-2013-web-tools/samples/sample8.cshtml)]
2. **스크립트** 태그 내에 다음 코드를 추가 하 여 준비 된 콜백 함수를 정의 합니다.

    (코드 조각- *VisualStudio2013WebTooling* - *Ex2* - *ReadyFunction*)

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample9.js)]
3. **스크립트** 태그에 캐럿을 추가 하 고 **ctrl** + 를 누릅니다 **.** 제안 메뉴를 엽니다.
4. **파일 추출을**클릭 합니다.

    ![JavaScript 파일에 대 한 추출 제안](visual-studio-2013-web-tools/_static/image39.png "JavaScript 파일에 대 한 추출 제안")

    *JavaScript 파일에 대 한 추출 제안*
5. 다른 이름 **으로 저장** 창에서 **Scripts** 폴더를 선택 하 고 파일 이름을 **init** 로 하 고 **저장**을 클릭 합니다.

    ![창으로 저장](visual-studio-2013-web-tools/_static/image40.png "창으로 저장")

    *창으로 저장*

    > [!NOTE]
    > **Init .js** 파일이 만들어지고 스크립트의 내용이 파일로 이동 합니다.
    > 
    > ![포함 된 콘텐츠를 사용 하 여 생성 된 초기화 .js 파일](visual-studio-2013-web-tools/_static/image41.png "포함 된 콘텐츠를 사용 하 여 생성 된 초기화 .js 파일")
    > 
    > *포함 된 콘텐츠를 사용 하 여 생성 된 초기화 .js 파일*
6. **인덱스 cshtml** 파일을 열고 스크립트 태그가 **init .js** 파일에 대 한 참조로 대체 되었는지 확인 합니다.

    ![Init .js html 참조](visual-studio-2013-web-tools/_static/image42.png "Init .js html 참조")

    *Init .js html 참조*
7. **솔루션 탐색기** 로 이동 하 여 **init .js** 파일이 솔루션에 자동으로 포함 되어 있는지 확인 합니다.

    ![솔루션에 포함 된 초기화 .js 파일](visual-studio-2013-web-tools/_static/image43.png "솔루션에 포함 된 초기화 .js 파일")

    *솔루션에 포함 된 초기화 .js 파일*
8. **Init .js** 파일로 다시 전환 하 여 **준비** 함수 콜백을 업데이트 합니다.
9. *준비*에 전달 된 함수 콜백 정의 내에서 다음 코드를 추가 하 여 특정 클래스 특성에 따라 모든 요소를 가져옵니다.

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample10.js)]
10. **GetElementsByClassName** 함수 호출 내의 따옴표 사이에 있는 **ctrl** + **공백을** 누릅니다.

    ![GetElementsByClassName 함수에 대 한 IntelliSense 표시](visual-studio-2013-web-tools/_static/image44.png "GetElementsByClassName 함수에 대 한 IntelliSense 표시")

    *GetElementsByClassName 함수에 대 한 IntelliSense 표시*

    > [!NOTE]
    > IntelliSense가 프로젝트 스타일 시트에 정의 된 클래스를 표시 합니다.
11. 만든 줄을 다음 코드로 바꿉니다.

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample11.js)]
12. **GetElementsByTagName** 함수의 따옴표 안에 있는 **au** 뒤에 커서를 놓고 **CTRL** + **Space**를 누릅니다.

    ![GetElementByTagName 메서드에 대 한 IntelliSense 표시](visual-studio-2013-web-tools/_static/image45.png "GetElementByTagName 메서드에 대 한 IntelliSense 표시")

    *GetElementsByTagName 메서드에 대 한 IntelliSense 표시*
13. 목록에서 **&quot;오디오&quot;** 를 선택 하 고 **enter**키를 누릅니다. 결과는 다음 그림에 나와 있습니다.

    ![오디오 요소 검색](visual-studio-2013-web-tools/_static/image46.png "오디오 요소 검색")

    *오디오 요소 검색*
14. **솔루션 탐색기**에서 **Scripts** 폴더의 **init .js** 파일을 마우스 오른쪽 단추로 클릭 하 고 **Web Essentials** 메뉴에서 파일을 선택 하지 않은 **JavaScript 파일** 을 선택 합니다.

    ![JavaScript 파일 (s)](visual-studio-2013-web-tools/_static/image47.png "JavaScript 파일")

    *JavaScript 파일 (s)*
15. 원본 파일이 변경 될 때 자동 축소를 사용 하도록 설정 하 라는 메시지가 표시 되 면 **예**를 클릭 합니다.

    ![자동 축소 경고 사용](visual-studio-2013-web-tools/_static/image48.png "자동 축소 경고 사용")

    *자동 축소 경고 사용*

    > [!NOTE]
    > **Init.** m a m. m a. m **a.**
    > 
    > ![초기화 되는 최소 .js 파일](visual-studio-2013-web-tools/_static/image49.png "초기화 되는 최소 .js 파일")
    > 
    > *초기화 되는 최소 .js 파일*
16. **Init. 최소 .js** 파일을 열고 파일의 표시를 확인 합니다.

    ![Init. 최소 .js 파일 콘텐츠](visual-studio-2013-web-tools/_static/image50.png "Init. 최소 .js 파일 콘텐츠")

    *Init. 최소 .js 파일 콘텐츠*
17. **Init .js** 파일에서 **getElementsByTagName** 함수 호출 아래에 다음 코드를 추가 하 여 모든 오디오 요소를 재생 합니다.

    (코드 조각- *VisualStudio2013WebTooling* - *Ex2* - *play오디오 요소*)

    [!code-csharp[Main](visual-studio-2013-web-tools/samples/sample12.cs)]
18. **CTRL** + **S** 를 클릭 하 여 파일을 저장 합니다. 파일이 이미 열려 있으므로 파일이 소스 편집기 외부에서 수정 되었다는 대화 상자가 표시 됩니다. **예**를 클릭합니다.

    ![Microsoft Visual Studio 경고](visual-studio-2013-web-tools/_static/image51.png "Microsoft Visual Studio 경고")

    *Microsoft Visual Studio 경고*
19. **Init.** m a m 파일로 다시 전환 하 여 파일이 새 코드로 업데이트 되었는지 확인 합니다.

    ![초기화 된 최소 .js 파일](visual-studio-2013-web-tools/_static/image52.png "초기화 된 최소 .js 파일")

    *초기화 된 최소 .js 파일*
20. **브라우저 링크 새로 고침** 단추를 클릭 합니다.
21. 두 브라우저를 새로 고치면 이전 작업에서 본 오디오 플레이어가 자동으로 재생 되기 시작 합니다.

    ![보기에 포함 된 오디오 플레이어](visual-studio-2013-web-tools/_static/image53.png "보기에 포함 된 오디오 플레이어")

    *보기에 포함 된 오디오 플레이어*

---

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습 실습을 완료 하면 다음 방법에 대해 알아보았습니다.

- 풍부한 HTML5 코드 조각 및 Zen 코딩 등 Web Essentials에 포함 된 새 HTML 편집기 기능 사용
- 색 선택 및 브라우저 매트릭스 도구 설명과 같은 웹 Essentials에 포함 된 새 CSS 편집기 기능 사용
- 모든 HTML 요소에 대 한 파일 및 IntelliSense에 압축 풀기와 같은 웹 Essentials에 포함 된 새 JavaScript 편집기 기능을 사용 합니다.
- 브라우저 링크를 사용 하 여 브라우저와 Visual Studio 간 데이터 교환
