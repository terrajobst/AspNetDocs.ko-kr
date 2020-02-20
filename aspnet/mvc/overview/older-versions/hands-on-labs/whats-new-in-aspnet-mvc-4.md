---
uid: mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
title: ASP.NET MVC 4의 새로운 기능 | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4는 잘 구성 된 디자인 패턴과 ASP.NET의 기능을 사용 하 여 확장성 있는 표준 기반 웹 응용 프로그램을 빌드하기 위한 프레임 워크입니다.
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 48f7feb3-872f-485d-b96f-e30011ff8c4a
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 4235f4fe666cdeb7d0821127a2b349f2ff30cd6e
ms.sourcegitcommit: 295cf898a4c87e264b0c35c7254b0fa4169f2278
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2019
ms.locfileid: "74057038"
---
# <a name="whats-new-in-aspnet-mvc-4"></a>ASP.NET MVC 4의 새로운 기능

[웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 교육 키트 다운로드](https://aka.ms/webcamps-training-kit)

ASP.NET MVC 4는 잘 구성 된 디자인 패턴과 ASP.NET 및 .NET framework의 기능을 사용 하 여 확장성 있는 표준 기반 웹 응용 프로그램을 빌드하기 위한 프레임 워크입니다. 이 새로운 4 번째 버전의 프레임 워크는 모바일 웹 응용 프로그램 개발을 더 쉽게 만드는 데 중점을 둔 것입니다.

먼저 새 ASP.NET MVC 4 프로젝트를 만들 때 모바일 장치에 대해 특별히 독립 실행형 앱을 빌드하는 데 사용할 수 있는 모바일 응용 프로그램 프로젝트 템플릿이 있습니다. 또한 ASP.NET MVC 4는 jQuery 및 NuGet 패키지를 통해 jQuery Mobile과 통합 됩니다. jQuery Mobile은 Windows Phone, iPhone, Android 등을 비롯 한 널리 사용 되는 모든 모바일 장치 플랫폼과 호환 되는 웹 앱을 개발 하기 위한 HTML5 기반 프레임 워크입니다. 그러나 특수화가 필요한 경우에는 ASP.NET MVC 4를 사용 하 여 여러 장치에 대 한 다양 한 보기를 제공 하 고 장치별 최적화를 제공할 수도 있습니다.

이 실습 랩에서는 ASP.NET MVC 4 &quot;인터넷 응용 프로그램&quot; 프로젝트 템플릿으로 시작 하 여 사진 갤러리 응용 프로그램을 만듭니다. JQuery Mobile 및 ASP.NET MVC 4의 새로운 기능을 사용 하 여 앱을 점진적으로 개선 하 여 다양 한 모바일 장치 및 데스크톱 웹 브라우저와 호환 되도록 할 수 있습니다. 또한 코드 생성을 위한 새 코드 조리법 및 ASP.NET MVC 4를 사용 하 여 작업&lt;ActionResult&gt; 반환 형식을 지원 함으로써 비동기 작업 메서드를 보다 쉽게 작성할 수 있는 방법을 알아봅니다.

> [!NOTE]
> 모든 샘플 코드와 코드 조각은 [Microsoft 웹/WebCampTrainingKit 릴리스에서](https://aka.ms/webcamps-training-kit)제공 되는 웹 캠프 교육 키트에 포함 되어 있습니다. 이 랩에서 관련 된 프로젝트는 [ASP.NET 4.5의 Web Forms 새로운 기능](https://github.com/Microsoft-Web/HOL-ASPNETWebForms)에서 제공 됩니다.

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서는 다음 방법에 대해 알아봅니다.

- 새 모바일 응용 프로그램 프로젝트 템플릿을 포함 하 여 ASP.NET MVC 프로젝트 템플릿에 대 한 향상 된 기능 활용
- HTML5 뷰포트 특성 및 CSS 미디어 쿼리를 사용 하 여 모바일 장치에 대 한 디스플레이 개선
- 프로그레시브 기능 향상을 위해 jQuery Mobile 사용 및 터치 최적화 웹 UI 빌드
- 모바일 관련 보기 만들기
- 뷰-전환기 구성 요소를 사용 하 여 응용 프로그램에서 모바일 및 데스크톱 보기 사이를 전환 합니다.
- 작업 지원을 사용 하 여 비동기 컨트롤러 만들기

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>사전 요구 사항

이 랩을 완료 하려면 다음 항목이 있어야 합니다.

- [웹 또는 고급의 경우 2012 Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (설치 방법에 대 한 지침은 [부록 B](#AppendixB) 를 참조 하세요.)
- [ASP.NET MVC 4](../../../mvc4.md) (Microsoft Visual Studio 2012 설치에 포함 됨)
- Windows Phone 에뮬레이터 ( [Windows Phone 7.1.1 SDK](https://www.microsoft.com/download/details.aspx?id=29233)에 포함 됨)
- 선택 사항- [WebMatrix 2](https://www.microsoft.com/web/webmatrix/) ( **전기 Plum iphone 시뮬레이터** 확장 포함) (iphone 시뮬레이터를 사용 하 여 웹 응용 프로그램을 검색 하는 데 사용 되는 연습 3에만 해당)

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>설치 프로그램

랩 문서 전체에서 코드 블록을 삽입 하 라는 지침이 표시 됩니다. 사용자 편의를 위해 대부분의 코드는 Visual Studio 내에서 사용 하 여 수동으로 추가할 필요가 없도록 하는 Visual Studio Code 코드 조각으로 제공 됩니다.

코드 조각을 설치 하려면:

1. Windows 탐색기 창을 열고 랩의 **Source\Setup** 폴더로 이동 합니다.
2. 이 폴더에 있는 **setup.exe** 파일을 두 번 클릭 하 여 Visual Studio 코드 조각을 설치 합니다.

Visual Studio Code 코드 조각에 익숙하지 않은 경우이를 사용 하는 방법을 알아보려면 [부록 A: &quot;코드 조각&quot;사용](#AppendixA) 문서에서 부록을 참조할 수 있습니다.

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>실습

이 실습 랩에는 다음 연습이 포함 되어 있습니다.

1. [새 ASP.NET MVC 4 프로젝트 템플릿](#Exercise1)
2. [사진 갤러리 웹 응용 프로그램 만들기](#Exercise2)
3. [모바일 장치에 대 한 지원 추가](#Exercise3)
4. [비동기 컨트롤러 사용](#Exercise4)

> [!NOTE]
> 각 연습에는 연습을 완료 한 후 얻게 되는 결과 솔루션을 포함 하는 **끝** 폴더가 함께 제공 됩니다. 연습을 진행 하는 데 도움이 필요한 경우이 솔루션을 지침으로 사용할 수 있습니다.

이 랩을 완료 하는 데 소요 되는 예상 시간: **60 분**

<a id="Exercise1"></a>

<a id="Exercise_1_New_ASPNET_MVC_4_Project_Templates"></a>
### <a name="exercise-1-new-aspnet-mvc-4-project-templates"></a>연습 1: New ASP.NET MVC 4 프로젝트 템플릿

이 연습에서는 ASP.NET MVC 4 프로젝트 템플릿의 향상 된 기능을 살펴봅니다. 이제 MVC 3에 이미 있는 인터넷 응용 프로그램 템플릿 외에도이 버전에는 모바일 응용 프로그램에 대 한 별도의 템플릿이 포함 되어 있습니다. 먼저 각 템플릿의 관련 기능 중 일부를 살펴보겠습니다. 그런 다음 적절 한 방법을 사용 하 여 여러 플랫폼에서 페이지를 올바르게 렌더링 하는 작업을 수행 합니다.

<a id="Task_1_-_Exploring_the_Internet_Application_Template"></a>
#### <a name="task-1---exploring-the-internet-application-template"></a>작업 1-인터넷 응용 프로그램 템플릿 탐색

1. **Visual Studio**를 엽니다.
2. 파일을 선택 합니다. **| 새로 만들기 | 프로젝트** 메뉴 명령입니다. **새 프로젝트** 대화 상자에서 **시각적 개체 C# | 웹** 템플릿 왼쪽 창에서 **ASP.NET MVC 4 웹 응용 프로그램을 선택 합니다.** 프로젝트 이름을 **사진**으로 지정 하 고 위치를 선택 하거나 기본값을 그대로 두고 **확인**을 클릭 합니다.

    > [!NOTE]
    > 나중에 현재 만들고 있는 사진 갤러리 ASP.NET MVC 4 솔루션을 사용자 지정 합니다.

    ![새 프로젝트 만들기](whats-new-in-aspnet-mvc-4/_static/image1.png "새 프로젝트 만들기")

    *새 프로젝트 만들기*
3. **새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **인터넷 응용 프로그램** 프로젝트 템플릿을 선택 하 고 **확인**을 클릭 합니다. Razor를 뷰 엔진으로 선택 했는지 확인 합니다.

    ![새 ASP.NET MVC 4 인터넷 응용 프로그램 만들기](whats-new-in-aspnet-mvc-4/_static/image2.png "새 ASP.NET MVC 4 인터넷 응용 프로그램 만들기")

    *새 ASP.NET MVC 4 인터넷 응용 프로그램 만들기*

    > [!NOTE]
    > Razor 구문는 ASP.NET MVC 3에서 도입 되었습니다. 이는 파일에 필요한 문자 및 키 입력 수를 최소화 하 여 빠르고 유체 코딩 워크플로를 사용 하도록 설정 하는 것입니다. Razor는 기존 C# /VB (또는 기타) 언어 기술을 활용 하 고 멋진 HTML 생성 워크플로를 활성화 하는 템플릿 태그 구문을 제공 합니다.
4. **F5** 키를 눌러 솔루션을 실행 하 고 갱신 된 템플릿을 확인 합니다. 다음 기능을 확인할 수 있습니다.

    **최신 스타일 템플릿**

    템플릿이 갱신 되어 최신 스타일을 제공 합니다.

    ![ASP.NET MVC 4 스타일 지정 템플릿](whats-new-in-aspnet-mvc-4/_static/image3.png "MVC 4 스타일 지정 템플릿")

    *ASP.NET MVC 4 스타일 지정 템플릿*

    ![새 연락처 페이지](whats-new-in-aspnet-mvc-4/_static/image4.png "새 연락처 페이지")

    *새 연락처 페이지*

    **적응 렌더링**

    브라우저 창의 크기를 조정 하 고 페이지 레이아웃이 새 창 크기에 동적으로 적응 하는 방식을 확인 합니다. 이러한 템플릿은 적응 렌더링 기술을 사용 하 여 사용자 지정 없이 데스크톱과 모바일 플랫폼 모두에서 적절히 렌더링 합니다.

    ![다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿](whats-new-in-aspnet-mvc-4/_static/image5.png "다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿")

    *다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿*

    **JavaScript를 사용 하는 풍부한 UI**

    기본 프로젝트 템플릿에 대 한 또 다른 향상 된 기능은 JavaScript를 사용 하 여 더 대화형 JavaScript를 제공 하는 것입니다. 템플릿에 사용 되는 로그인 및 등록 링크는 jQuery 유효성 검사를 사용 하 여 클라이언트 쪽에서 입력 필드의 유효성을 검사 하는 방법을 exemplify 합니다.

    ![jQuery 유효성 검사](whats-new-in-aspnet-mvc-4/_static/image6.png)

    *jQuery 유효성 검사*

    > [!NOTE]
    > 두 개의 로그인 섹션, 첫 번째 섹션에서는 사이트에서 등록 된 계정을 사용 하 여 로그인 할 수 있으며, 두 번째 섹션에서는 google (기본적으로 사용 하지 않도록 설정 됨)과 같은 다른 인증 서비스를 사용 하 여 로그인 할 수 있습니다.
5. 디버거를 중지 하 고 Visual Studio로 돌아가려면 브라우저를 닫습니다.
6. **앱\_시작** 폴더 아래에 있는 **AuthConfig.cs** 파일을 엽니다.
7. 마지막 줄에서 의견을 제거 하 여 *OAuth* 인증에 Google 클라이언트를 등록 합니다.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample1.cs)]

    > [!NOTE]
    > Openid connect 또는 OAuth 서비스 (예: Facebook, Twitter, Microsoft 등)를 사용 하 여 인증을 쉽게 사용할 수 있습니다.
8. **F5** 키를 눌러 솔루션을 실행 하 고 로그인 페이지로 이동 합니다.
9. 로그인 하려면 **Google** service를 선택 합니다.

    ![로그인 서비스 선택](whats-new-in-aspnet-mvc-4/_static/image7.png)

    *로그인 서비스 선택*
10. Google 계정을 사용 하 여 로그인 합니다.
11. 사이트 (localhost)가 Google 계정에서 정보를 검색할 수 있도록 허용 합니다.
12. 마지막으로 Google 계정을 연결 하려면 사이트에 등록 해야 합니다.

   ![Google 계정 연결](whats-new-in-aspnet-mvc-4/_static/image8.png)

   *Google 계정 연결*
13. 디버거를 중지 하 고 Visual Studio로 돌아가려면 브라우저를 닫습니다.
14. 이제 솔루션을 탐색 하 여 프로젝트 템플릿에서 ASP.NET MVC 4에서 도입 된 몇 가지 다른 새로운 기능을 확인 하세요.

   ![ASP.NET MVC 4 인터넷 응용 프로그램 프로젝트 템플릿](whats-new-in-aspnet-mvc-4/_static/image9.png "ASP.NET MVC 4 인터넷 응용 프로그램 프로젝트 템플릿")

   *ASP.NET MVC 4 인터넷 응용 프로그램 프로젝트 템플릿*

    - **HTML 5 태그**

       템플릿 뷰를 탐색 하 여 새 테마 태그를 찾습니다.

       ![새 템플릿으로, Razor 및 HTML5 태그를 사용 합니다.](whats-new-in-aspnet-mvc-4/_static/image10.png "새 템플릿으로, Razor 및 HTML5 태그를 사용 합니다.")

       *Razor 및 HTML5 태그를 사용 하는 새 템플릿 (정보 cshtml)*
    - **업데이트 된 JavaScript 라이브러리**

       ASP.NET MVC 4 기본 템플릿에는 JavaScript 및 HTML을 사용 하 여 풍부 하 고 응답성이 뛰어난 웹 응용 프로그램을 만들 수 있는 JavaScript MVVM 프레임 워크인 KnockoutJS가 포함 되어 있습니다. MVC3에서와 마찬가지로 jQuery 및 jQuery UI 라이브러리도 ASP.NET MVC 4에 포함 되어 있습니다.

     > [!NOTE]
     > 이 링크에서 KnockOutJS library에 대 한 자세한 내용은 [[http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)](http://learn.knockoutjs.com/)를 확인 하세요. 또한 [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/)에서 jQuery 및 jquery UI에 대해 알아볼 수 있습니다.

<a id="Task_2_-_Exploring_the_Mobile_Application_Template"></a>
#### <a name="task-2---exploring-the-mobile-application-template"></a>작업 2-모바일 응용 프로그램 템플릿 탐색

ASP.NET MVC 4는 모바일 및 태블릿 브라우저용 웹 사이트 개발을 용이 하 게 합니다. 이 템플릿의 응용 프로그램 구조는 인터넷 응용 프로그램 템플릿과 동일 하지만 (컨트롤러 코드는 거의 동일 함) 터치 기반 모바일 장치에서 제대로 렌더링 되도록 스타일이 수정 되었습니다.

1. 파일을 선택 합니다. **| 새로 만들기 | 프로젝트** 메뉴 명령입니다. **새 프로젝트** 대화 상자에서 **시각적 개체 C# | 웹** 템플릿을 선택 하 고 **ASP.NET MVC 4 웹 응용 프로그램을 선택 합니다.** 프로젝트 이름을 **사진 갤러리**로 지정 하 고, 위치를 선택 하 고, 위치를 선택 하거나, &quot;솔루션&quot;에 추가를 선택 하 고 **확인**을 클릭 합니다.
2. **새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **모바일 응용 프로그램** 프로젝트 템플릿을 선택 하 고 **확인**을 클릭 합니다. Razor를 뷰 엔진으로 선택 했는지 확인 합니다.

    ![새 ASP.NET MVC 4 모바일 응용 프로그램 만들기](whats-new-in-aspnet-mvc-4/_static/image11.png "새 ASP.NET MVC 4 모바일 응용 프로그램 만들기")

    *새 ASP.NET MVC 4 모바일 응용 프로그램 만들기*
3. 이제 솔루션을 탐색 하 고 mobile 용 ASP.NET MVC 4 솔루션 템플릿에서 도입 된 새로운 기능 중 일부를 확인할 수 있습니다.

    - **jQuery 모바일 라이브러리**

        모바일 응용 프로그램 프로젝트 템플릿에는 모바일 브라우저 호환성을 위한 오픈 소스 라이브러리인 jQuery 모바일 라이브러리가 포함 되어 있습니다. jQuery Mobile은 CSS 및 JavaScript를 지 원하는 모바일 브라우저에 점진적 향상 기능을 적용 합니다. 점진적 향상 기능을 통해 모든 브라우저는 웹 페이지의 기본 콘텐츠를 표시할 수 있으며, 가장 강력한 브라우저 에서만 풍부한 콘텐츠를 표시할 수 있습니다. JQuery 모바일 스타일에 포함 된 JavaScript 및 CSS 파일은 페이지 태그를 변경 하지 않고 화면에 콘텐츠를 맞추는 데 도움이 됩니다.

        ![jQuery-mobile-library-included-in-the-template](whats-new-in-aspnet-mvc-4/_static/image12.png)

        *템플릿에 포함 된 jQuery mobile library*
    - **HTML5 기반 태그**

        ![모바일-응용 프로그램-템플릿 사용-HTML5-태그](whats-new-in-aspnet-mvc-4/_static/image13.png)

        *HTML5 태그를 사용 하는 모바일 응용 프로그램 템플릿 (Login/cshtml)*
4. **F5** 키를 눌러 솔루션을 실행합니다.
5. **Windows Phone 7 에뮬레이터**를 엽니다.
6. 휴대폰 시작 화면에서 Internet Explorer를 엽니다. 데스크톱 응용 프로그램이 시작 된 URL을 확인 하 고 휴대폰에서 해당 URL로 이동 합니다 (예: `http://localhost:[PortNumber]/`).
7. 이제 로그인 페이지를 입력 하거나 정보 페이지를 확인할 수 있습니다. 웹 사이트의 스타일은 모바일 용 새 Metro 앱을 기반으로 합니다. ASP.NET MVC 4 프로젝트 템플릿이 모바일 장치에 올바르게 표시 되므로 페이지의 모든 요소가 표시 되 고 사용 하도록 설정 됩니다. 헤더에 대 한 링크는 클릭 하거나 탭 할 만큼 충분히 큽니다.

    ![모바일 장치의 프로젝트 템플릿 페이지](whats-new-in-aspnet-mvc-4/_static/image14.png "모바일 장치의 프로젝트 템플릿 페이지")

    *모바일 장치의 프로젝트 템플릿 페이지*
8. 새 템플릿은 **뷰포트 메타 태그**도 사용 합니다. 대부분의 모바일 브라우저는 모바일 장치의 실제 너비 보다 큰 가상 브라우저 창 또는 &quot;뷰포트&quot;의 너비를 정의 합니다. 이렇게 하면 모바일 브라우저에서 전체 웹 페이지를 가상 표시 안에 표시할 수 있습니다. 웹 개발자는 **뷰포트 메타 태그** 를 사용 하 여 모바일 장치에서 브라우저 영역의 너비, 높이 및 크기를 설정할 수 있습니다 **.** 모바일 응용 프로그램에 대 한 ASP.NET MVC 4 템플릿에서는 레이아웃 템플릿 (*Views\Shared\_layout. cshtml*)의 장치 너비 (&quot;width = 장치 너비&quot;)로 뷰포트를 설정 하 여 모든 페이지의 뷰포트가 장치 화면 너비로 설정 되도록 합니다. 뷰포트 메타 태그는 기본 브라우저 보기를 변경 하지 않습니다.
9. 뷰에 있는 **\_Layout. cshtml**를 엽니다.  **공유** 폴더, 뷰포트 메타 태그 설명 응용 프로그램을 아직 열지 않은 경우 실행 하 고 차이점을 확인 합니다.

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample2.cshtml)]

![뷰포트 메타 태그를 주석으로 처리 한 후의 사이트입니다.](whats-new-in-aspnet-mvc-4/_static/image15.png "뷰포트 메타 태그를 주석으로 처리 한 후의 사이트입니다.")

*뷰포트 메타 태그를 주석으로 처리 한 후의 사이트입니다.*
10. Visual Studio에서 **SHIFT** + **f5** 키를 눌러 응용 프로그램 디버깅을 중지 합니다.
11. 뷰포트 메타 태그의 주석 처리를 제거 합니다.

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample3.cshtml)]

<a id="Task_3_-_Using_Adaptive_Rendering"></a>
#### <a name="task-3---using-adaptive-rendering"></a>작업 3-적응 렌더링 사용

이 작업에서는 사용자 지정 없이 모바일 장치 및 웹 브라우저에서 웹 페이지를 올바르게 렌더링 하는 다른 방법을 배웁니다. 이미 유사한 용도로 뷰포트 메타 태그를 사용 했습니다. 이제 다른 강력한 방법 ( *적응 렌더링*)을 충족 합니다.

적응 렌더링은 **CSS3 미디어 쿼리** 를 사용 하 여 페이지에 적용 되는 스타일을 사용자 지정 하는 기술입니다. 미디어 쿼리는 특정 조건에서 CSS 스타일을 그룹화 하 여 스타일 시트 내에서 조건을 정의 합니다. 조건이 true 인 경우에만 스타일이 선언 된 개체에 적용 됩니다.

적응 렌더링 기술에서 제공 하는 유연성을 통해 다른 장치에 사이트를 표시 하는 사용자 지정을 수행할 수 있습니다. 스타일을 선택 하는 논리 코드를 작성 하지 않고 단일 스타일 시트에서 원하는 만큼 스타일을 정의할 수 있습니다. 따라서 렌더링 용도로 중복 된 코드와 논리의 양이 줄어들기 때문에 페이지 스타일을 적용 하는 것이 매우 편리 합니다. 반면, CSS 파일의 크기는 매우 커질 수 있으므로 대역폭 소비가 증가 합니다.

적응 렌더링 기술을 사용 하 여 **브라우저에 관계 없이 사이트가 제대로 표시 됩니다.** 그러나 대역폭 추가 로드가 중요 한 경우를 고려해 야 합니다.

> [!NOTE]
> 미디어 쿼리의 기본 형식은 @media \[범위: 모두 | 핸드헬드 | 인쇄 | 프로젝션 | 화면\] ([속성: 값] 및 ... [속성: 값])

미디어 쿼리 예: &gt; **@media 모든 및 (최대 너비: 1000px) 및 (최소 너비: 700px) {}:** 00px와 1000px 사이의 모든 해상도

> **@media 화면 및 (최소 너비: 400px) 및 (최대 너비: 700px) {...}:** 화면에만 해당 합니다. 해상도는 400에서 700px 사이 여야 합니다.
> 
> **@media 핸드헬드 및 (최소 너비: 20em), 화면 및 (최소 너비: 20em) {...}:** -핸드헬드 (모바일 및 장치) 및 화면 최소 너비는 20em 보다 커야 합니다.
> 
> [W3C 사이트](http://www.w3.org/TR/css3-mediaqueries/)에서이에 대 한 자세한 정보를 찾을 수 있습니다.

이제 적응 렌더링의 작동 방식을 탐색 하 여 ASP.NET MVC 4 기본 웹 사이트 템플릿의 가독성을 향상 시킵니다.

1. 작업 1에서 만든 **사진 갤러리 .sln** 솔루션을 열고 **사진 갤러리** 프로젝트를 선택 합니다. **F5** 키를 눌러 솔루션을 실행합니다.
2. 브라우저의 너비 크기를 조정 하 여 windows를 원래 크기의 절반 또는 1/4 미만으로 설정 합니다. 헤더의 항목에 대 한 결과, 일부 요소는 머리글의 표시 영역에 표시 되지 않습니다.
3. **콘텐츠** 프로젝트 폴더에 있는 Visual Studio 솔루션 탐색기에서 **사이트 .css** 파일을 엽니다. **Ctrl + F** 를 눌러 Visual Studio 통합 검색을 열고 **CSS 미디어 쿼리**를 찾을 `@media`을 작성 합니다.

    이 템플릿에 정의 된 미디어 쿼리 조건은 다음과 같은 방식으로 작동 합니다. 브라우저의 창 크기가 **850 px**미만이 면 적용 되는 CSS 규칙이이 미디어 블록 내에서 정의 된 것입니다.

    ![미디어 쿼리 찾기](whats-new-in-aspnet-mvc-4/_static/image16.png "미디어 쿼리 찾기")

    *미디어 쿼리 찾기*
4. 적응 렌더링을 사용 하지 않도록 설정 하기 위해 850 px에 설정 된 최대 너비 특성 값을 **10px**로 바꾸고 **CTRL + S** 를 눌러 변경 내용을 저장 합니다. 브라우저로 돌아가서 **CTRL + F5** 키를 눌러 변경한 내용으로 페이지를 새로 고칩니다. 창의 너비를 조정할 때 두 페이지의 차이점을 확인 합니다.

    ![왼쪽의 페이지에 @media 스타일이 적용 됩니다. 오른쪽에는 스타일이 생략 됩니다.](whats-new-in-aspnet-mvc-4/_static/image17.png "왼쪽의 페이지에 @media 스타일이 적용 됩니다. 오른쪽에는 스타일이 생략 됩니다.")

    *왼쪽의 페이지에 @media 스타일이 적용 됩니다. 오른쪽에는 스타일이 생략 됩니다.*

    이제 모바일 장치에서 발생 하는 상황을 확인해 보겠습니다.

    ![왼쪽의 페이지에 @media 스타일이 적용 됩니다. 오른쪽에는 스타일이 생략 됩니다.](whats-new-in-aspnet-mvc-4/_static/image18.png "왼쪽의 페이지에 @media 스타일이 적용 됩니다. 오른쪽에는 스타일이 생략 됩니다.")

    *왼쪽의 페이지에 @media 스타일이 적용 됩니다. 오른쪽에는 스타일이 생략 됩니다.*

    웹 브라우저에서 페이지가 렌더링 되는 경우 변경 내용이 그다지 중요 하지 않지만 모바일 장치를 사용 하는 경우 차이가 더 분명해 집니다. 이미지의 왼쪽에서 사용자 지정 스타일의 가독성을 향상 시키는 것을 볼 수 있습니다.

    적응 렌더링은 다양 한 시나리오에서 사용 될 수 있으므로, 웹 사이트에 조건부 스타일을 보다 쉽게 적용 하 고 다양 한 방식으로 일반적인 스타일 문제를 해결할 수 있습니다.

    뷰포트 메타 태그 및 CSS 미디어 쿼리는 ASP.NET MVC 4에 한정 되지 않으므로 모든 웹 응용 프로그램에서 이러한 기능을 활용할 수 있습니다.
5. Visual Studio에서 **SHIFT** + **f5** 키를 눌러 응용 프로그램 디버깅을 중지 합니다.

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_the_Photo_Gallery_Web_Application"></a>
### <a name="exercise-2-creating-the-photo-gallery-web-application"></a>연습 2: 사진 갤러리 웹 응용 프로그램 만들기

이 연습에서는 사진 갤러리 응용 프로그램에 대 한 작업을 수행 하 여 사진을 표시 합니다. ASP.NET MVC 4 프로젝트 템플릿으로 시작 하 고 서비스에서 사진을 검색 하 고 홈 페이지에 표시 하는 기능을 추가 합니다.

다음 연습에서는이 솔루션을 업데이트 하 여 모바일 장치에 표시 되는 방법을 개선 합니다.

<a id="Task_1_-_Creating_a_Mock_Photo_Service"></a>
#### <a name="task-1---creating-a-mock-photo-service"></a>작업 1-모의 사진 서비스 만들기

이 작업에서는 갤러리에 표시 되는 콘텐츠를 검색 하는 사진 서비스의 모의를 만듭니다. 이렇게 하려면 각 사진의 데이터를 사용 하 여 JSON 파일을 단순히 반환 하는 새 컨트롤러를 추가 합니다.

1. 아직 열려 있지 않은 경우 **Visual Studio** 를 엽니다.
2. 파일을 선택 합니다. **| 새로 만들기 | 프로젝트** 메뉴 명령입니다. **새 프로젝트** 대화 상자에서 **시각적 개체 C# | 웹** 템플릿 왼쪽 창에서 **ASP.NET MVC 4 웹 응용 프로그램을 선택 합니다.** 프로젝트 이름을 **사진**으로 지정 하 고 위치를 선택 하거나 기본값을 그대로 두고 **확인**을 클릭 합니다. 또는 **실습 1** 에서 기존 ASP.NET MVC 4 **인터넷 응용 프로그램** 솔루션의 작업을 계속 진행 하 고 다음 단계를 건너뛸 수 있습니다.
3. **새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **인터넷 응용 프로그램** 프로젝트 템플릿을 선택 하 고 **확인**을 클릭 합니다. 뷰 엔진으로 Razor가 선택 되어 있는지 확인 합니다.
4. **솔루션 탐색기**에서 프로젝트의 **App\_Data** 폴더를 마우스 오른쪽 단추로 클릭 하 고 추가 |를 선택 합니다.  **기존 항목**입니다. 이 랩의 **Source\assets\app\_Data** 폴더로 이동 하 여 **사진의 json** 파일을 추가 합니다.
5. 이름으로 **사진 컨트롤러**를 사용 하 여 새 컨트롤러를 만듭니다. 이렇게 하려면 **Controllers** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** 로 이동한 후 컨트롤러를 선택 **합니다.** 컨트롤러 이름을 완료 하 고 **빈 MVC 컨트롤러** 템플릿을 그대로 두고 **추가**를 클릭 합니다.

    ![사진 컨트롤러 추가](whats-new-in-aspnet-mvc-4/_static/image19.png "사진 컨트롤러 추가")

    *사진 컨트롤러 추가*
6. **Index** 메서드를 다음 **갤러리** 작업으로 바꾸고 최근에 프로젝트에 추가한 JSON 파일의 콘텐츠를 반환 합니다.

    (코드 조각- *ASP.NET MVC 4 Lab-Ex02-갤러리 동작*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample4.cs)]
7. **F5** 키를 눌러 솔루션을 실행 하 고 모의 photo 서비스를 테스트 하기 위해 다음 URL로 이동 합니다. `http://localhost:[port]/photo/gallery` ([port] 값은 응용 프로그램이 시작 된 현재 포트에 따라 달라 짐) 이 URL에 대 한 요청은 **사진. json** 파일의 콘텐츠를 검색 해야 합니다.

    ![모의 photo 서비스 테스트](whats-new-in-aspnet-mvc-4/_static/image20.png "모의 photo 서비스 테스트")

    *모의 photo 서비스 테스트*

실제 구현에서는 [ASP.NET Web API](../../../../web-api/index.md) 를 사용 하 여 사진 갤러리 서비스를 구현할 수 있습니다. ASP.NET Web API는 브라우저와 모바일 장치 등 광범위한 클라이언트를 연결하는 HTTP 서비스를 쉽게 빌드할 수 있도록 해주는 프레임워크입니다. ASP.NET Web API는 .NET Framework에 RESTful 응용 프로그램을 빌딩하기에 이상적인 플랫폼입니다.

<a id="Task_2_-_Displaying_the_Photo_Gallery"></a>
#### <a name="task-2---displaying-the-photo-gallery"></a>작업 2-사진 갤러리 표시

이 작업에서는이 연습의 첫 번째 작업에서 만든 모의 서비스를 사용 하 여 사진 갤러리를 표시 하도록 홈 페이지를 업데이트 합니다. 모델 파일을 추가 하 고 갤러리 뷰를 업데이트 합니다.

1. Visual Studio에서 **SHIFT** + **f5** 키를 눌러 응용 프로그램 디버깅을 중지 합니다.
2. **모델** 폴더에서 **Photo** 클래스를 만듭니다. 이렇게 하려면 **모델** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** 를 선택한 다음 **클래스**를 클릭 합니다. 그런 다음 이름을 **Photo.cs** 로 설정 하 고 **추가**를 클릭 합니다.
3. **Photo** 클래스에 다음 멤버를 추가 합니다.

    (코드 조각- *ASP.NET MVC 4 Lab-Ex02-Photo model*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample5.cs)]
4. **컨트롤러** 폴더에서 **HomeController.cs** 파일을 엽니다.
5. 다음 using 문을 추가합니다.

    (코드 조각- *ASP.NET MVC 4 Lab-Ex02-HomeController using*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample6.cs)]
6. **Httpclient** 를 사용 하 여 갤러리 데이터를 검색 한 다음 **JavaScriptSerializer** 를 사용 하 여 뷰 모델로 deserialize 하는 **인덱스** 작업을 업데이트 합니다.

    (코드 조각- *ASP.NET MVC 4 Lab-Ex02 동작*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample7.cs)]
7. **Views\Home** 폴더 **아래에 있는 파일을** 열고 모든 내용을 다음 코드로 바꿉니다.

    이 코드는 서비스에서 검색 된 모든 사진을 반복 하 여 순서가 지정 되지 않은 목록으로 표시 합니다.

    (코드 조각- *ASP.NET MVC 4 Lab-Ex02-Photo List*)

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample8.cshtml)]
8. **솔루션 탐색기**에서 프로젝트의 **콘텐츠** 폴더를 마우스 오른쪽 단추로 클릭 하 고 추가 |를 선택 합니다.  **기존 항목**입니다. 이 랩의 **Source\assets\content** 폴더로 이동 하 여 **사이트 .css** 파일을 추가 합니다. 교체를 확인 해야 합니다. **사이트 .css** 파일이 열려 있는 경우에도 파일을 다시 로드 해야 합니다.
9. 파일 탐색기를 열고이 랩의 **Source\assets** 폴더 아래에 있는 전체 **사진** 폴더를 솔루션 탐색기 프로젝트의 루트 폴더에 복사 합니다.
10. 애플리케이션을 실행합니다. 이제 갤러리에 사진을 표시 하는 홈 페이지가 표시 됩니다.

    ![사진 갤러리](whats-new-in-aspnet-mvc-4/_static/image21.png "사진 갤러리")

    *사진 갤러리*
11. Visual Studio에서 **SHIFT** + **f5** 키를 눌러 응용 프로그램 디버깅을 중지 합니다.

<a id="Exercise3"></a>

<a id="Exercise_3_Adding_support_for_mobile_devices"></a>
### <a name="exercise-3-adding-support-for-mobile-devices"></a>연습 3: 모바일 장치에 대 한 지원 추가

ASP.NET MVC 4의 주요 업데이트 중 하나는 모바일 개발에 대 한 지원입니다. 이 연습에서는 이전 연습에서 만든 사진 갤러리 솔루션을 확장 하 여 모바일 응용 프로그램에 대 한 ASP.NET MVC 4 new 기능을 살펴봅니다.

<a id="Task_1_-_Installing_jQuery_Mobile_in_an_ASPNET_MVC_4_Application"></a>
#### <a name="task-1---installing-jquery-mobile-in-an-aspnet-mvc-4-application"></a>작업 1-ASP.NET MVC 4 응용 프로그램에 jQuery Mobile 설치

1. **Source/Ex3-MobileSupport/begin/** 폴더에 있는 **시작** 솔루션을 엽니다. 그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.

   1. 제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.
   2. **NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.
   3. 마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.

      > [!NOTE]
      > NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다. NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다. 이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.
2. **NuGet 패키지 관리자** > **패키지 관리자 콘솔** 메뉴 옵션 > **도구** 를 클릭 하 여 **패키지 관리자 콘솔** 을 엽니다.

    ![NuGet 패키지 관리자 콘솔 열기](whats-new-in-aspnet-mvc-4/_static/image22.png "NuGet 패키지 관리자 콘솔 열기")

    *NuGet 패키지 관리자 콘솔 열기*
3. 패키지 관리자 콘솔에서 다음 명령을 실행 하 여 **jQuery** 를 설치 합니다.

    jQuery Mobile은 터치에 최적화 된 웹 UI를 빌드하기 위한 오픈 소스 라이브러리입니다. ASP.NET MVC 4 응용 프로그램과 함께 jQuery Mobile을 사용 하는 도우미가 jQuery의 NuGet 패키지에 포함 되어 있습니다.

    > [!NOTE]
    > 다음 명령을 실행 하 여 Nuget에서 jQuery. MVC 라이브러리를 다운로드 합니다.

    PM

    [!code-powershell[Main](whats-new-in-aspnet-mvc-4/samples/sample9.ps1)]

    이 명령은 다음을 포함 하 여 jQuery Mobile 및 일부 도우미 파일을 설치 합니다.

    - **Views/Shared/\_layout. cshtml**: 더 작은 화면에 최적화 된 jQuery 모바일 기반 레이아웃입니다. 웹 사이트는 모바일 브라우저에서 요청을 받으면 원래 레이아웃 (\_레이아웃. cshtml)을이 항목으로 바꿉니다.
    - 뷰 전환기 구성 요소: **Views/Shared/\_ViewSwitcher** 로 구성 됩니다. cshtml 부분 뷰와 **ViewSwitcherController.cs** controller 이 구성 요소는 사용자가 페이지의 데스크톱 버전으로 전환 하는 데 사용할 수 있는 모바일 브라우저의 링크를 표시 합니다.  
        ![모바일 지원이 있는 사진 갤러리 프로젝트](whats-new-in-aspnet-mvc-4/_static/image23.png "Ph모바일 지원이 있는 o Gallery 프로젝트 ")

        *모바일 지원이 있는 사진 갤러리 프로젝트*
4. 모바일 번들을 등록 합니다. 이렇게 하려면 **Global.asax.cs** 파일을 열고 다음 줄을 추가 합니다.

    (코드 조각- *ASP.NET MVC 4 Lab-Ex03-Register Mobile 번들*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample10.cs)]
5. 데스크톱 웹 브라우저를 사용 하 여 응용 프로그램을 실행 합니다.
6. 시작 메뉴에 있는 **Windows Phone 7 에뮬레이터를** 엽니다. **| 모든 프로그램 | Windows Phone SDK 7.1 | 에뮬레이터를 Windows Phone 합니다.**
7. 휴대폰 시작 화면에서 Internet Explorer를 엽니다. 응용 프로그램이 시작 된 URL을 확인 하 고 휴대폰 브라우저 (예: `http://localhost:[PortNumber]/`)를 사용 하 여 해당 URL로 이동 합니다.

    응용 프로그램이 Windows Phone 에뮬레이터에서 다르게 표시 되는 것을 확인할 수 있습니다 .이는 응용 프로그램이 모바일 장치에 대해 최적화 된 보기를 표시 하는 프로젝트에서 새 자산을 만들었습니다.

    휴대폰의 위쪽에 있는 메시지를 확인 하 고 바탕 화면 보기로 전환 되는 링크를 표시 합니다. 또한 사용자가 설치한 패키지에서 만든 **\_레이아웃** 은 응용 프로그램에 다른 레이아웃을 포함 합니다.

    > [!NOTE]
    > 지금까지 모바일 보기로 돌아갈 수 있는 링크가 없습니다. 이후 버전에 포함 됩니다.

    ![사진 갤러리 홈 페이지의 모바일 보기](whats-new-in-aspnet-mvc-4/_static/image24.png "사진 갤러리 홈 페이지의 모바일 보기")

    *사진 갤러리 홈 페이지의 모바일 보기*
8. Visual Studio에서 **SHIFT** + **f5** 키를 눌러 응용 프로그램 디버깅을 중지 합니다.

<a id="Task_2_-_Creating_Mobile_Views"></a>
#### <a name="task-2---creating-mobile-views"></a>작업 2-모바일 보기 만들기

이 작업에서는 모바일 장치에서 더 나은 모양을 위해 콘텐츠를 조정 하 여 인덱스 보기의 모바일 버전을 만듭니다.

1. **Views\Home\Index.cshtml** view를 복사 하 여 붙여넣어 복사본을 만들고 새 파일의 이름을 **Index. Mobile. cshtml**로 바꿉니다.
2. 새로 만든 **Index. Mobile. cshtml** 뷰를 열고 기존 &lt;ul&gt; 태그를이 코드로 바꿉니다. 이 작업을 수행 하 여 jQuery의 모바일 테마를 사용 하도록 jQuery Mobile 데이터 주석과 &lt;ul&gt; 태그를 업데이트 합니다.

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample11.html)]

    > [!NOTE] 
    > 
    > 다음에 유의합니다.
    > 
    > - **Listview** 로 설정 된 **데이터 역할** 특성은 listview 스타일을 사용 하 여 목록을 렌더링 합니다.
    > 
    > - **데이터 인세트** 특성을 true로 설정 하면 모퉁이가 둥근 테두리와 여백이 있는 목록이 표시 됩니다.
    > 
    > - **데이터 필터** 특성을 **true** 로 설정 하면 검색 상자가 생성 됩니다.
    > 
    > 프로젝트 설명서에서 jQuery 모바일 규칙에 대해 자세히 알아볼 수 있습니다. [ [http://jquerymobile.com/demos/1.1.1/](http://jquerymobile.com/demos/1.1.1/)](http://jquerymobile.com/demos/1.1.1/)
3. **Ctrl + S** 를 눌러 변경 내용을 저장 합니다.
4. **Windows Phone Emulator** 로 전환 하 고 사이트를 새로 고칩니다. 갤러리 목록의 새로운 모양과 느낌 뿐만 아니라 맨 위에 있는 새 검색 상자가 표시 됩니다. 그런 다음 검색 상자 (예 **Tulips**)에 단어를 입력 하 여 사진 갤러리에서 검색을 시작 합니다.

    ![필터링과 함께 listview 스타일을 사용 하는 갤러리](whats-new-in-aspnet-mvc-4/_static/image25.png "필터링과 함께 listview 스타일을 사용 하는 갤러리")

    *필터링과 함께 listview 스타일을 사용 하는 갤러리*

    요약 하면 View Mobilizer 조리법을 사용 하 여 &quot;mobile&quot; 접미사로 인덱스 보기의 복사본을 만들었습니다. 이 접미사는 ASP.NET MVC 4를 나타냅니다. 모바일 장치에서 생성 된 모든 요청은이 인덱스 복사본을 사용 합니다. 또한 모바일 장치의 사이트 모양과 느낌을 향상 시키기 위해 jQuery Mobile을 사용 하도록 인덱스 뷰의 모바일 버전을 업데이트 했습니다.
5. Visual Studio로 돌아가서 **Content** 폴더 아래에 있는 **사이트별** 를 엽니다.
6. 사진 제목의 위치를 수정 하 여 이미지의 오른쪽에 표시 되도록 합니다. 이렇게 하려면 다음 코드를 **사이트. Mobile .css** 파일에 추가 합니다.

    CSS

    [!code-css[Main](whats-new-in-aspnet-mvc-4/samples/sample12.css)]
7. **Ctrl + S** 를 눌러 변경 내용을 저장 합니다.
8. **Windows Phone 에뮬레이터** 로 다시 전환 하 고 사이트를 새로 고칩니다. 이제 사진 제목을 올바른 위치에 배치 합니다.

    ![이미지 오른쪽에 배치 된 제목](whats-new-in-aspnet-mvc-4/_static/image26.png "이미지 오른쪽에 배치 된 제목")

    *이미지 오른쪽에 배치 된 제목*

<a id="Task_3_-_jQuery_Mobile_Themes"></a>
#### <a name="task-3---jquery-mobile-themes"></a>작업 3-jQuery 모바일 테마

JQuery Mobile의 모든 레이아웃 및 위젯은 새로운 개체 지향 CSS 프레임 워크를 중심으로 디자인 되어 사이트 및 응용 프로그램에 완전 한 통합 시각적 디자인 테마를 적용할 수 있습니다.

jQuery Mobile의 기본 테마는 빠른 참조를 위해 문자 (a, b, c, d, e)가 지정 된 5 개의 견본을 포함 합니다.

이 작업에서는 기본값과 다른 테마를 사용 하도록 모바일 레이아웃을 업데이트 합니다.

1. Visual Studio로 다시 전환 합니다.
2. Views\Shared에 있는 **\_Layout.** 파일을 엽니다.
3. &quot;페이지&quot;으로 설정 된 데이터 역할의 div 요소를 찾고 **데이터 테마** 를 &quot;**e**&quot;로 업데이트 합니다.

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample13.html)]
4. **Ctrl + S** 를 눌러 변경 내용을 저장 합니다.
5. **Windows Phone 에뮬레이터** 에서 사이트를 새로 고치고 새 색 구성표를 확인 합니다.

    ![다른 색 구성표를 사용 하는 모바일 레이아웃](whats-new-in-aspnet-mvc-4/_static/image27.png "다른 색 구성표를 사용 하는 모바일 레이아웃")

    *다른 색 구성표를 사용 하는 모바일 레이아웃*

<a id="Task_4_-_Using_the_View-Switcher_Component_and_the_Browser_Overriding_Features"></a>
#### <a name="task-4---using-the-view-switcher-component-and-the-browser-overriding-features"></a>작업 4-뷰 전환기 구성 요소 및 브라우저 재정의 기능 사용

모바일 최적화 웹 페이지의 규칙은 사용자가 페이지의 데스크톱 버전으로 전환할 수 있는 바탕 화면 보기 또는 전체 사이트 모드와 같은 텍스트를 포함 하는 링크를 추가 하는 것입니다. JQuery. Mobile. i n a. i n a. i n. i n **\_** a.

![바탕 화면 뷰로 전환 하기 위한 링크](whats-new-in-aspnet-mvc-4/_static/image28.png "바탕 화면 뷰로 전환 하기 위한 링크")

*바탕 화면 뷰로 전환 하기 위한 링크*

뷰 전환기는 **브라우저 재정의**라는 새로운 기능을 사용 합니다. 이 기능을 사용 하면 응용 프로그램이 실제로 제공 되는 것과 다른 브라우저 (사용자 에이전트)에서 오는 것 처럼 요청을 처리할 수 있습니다.

이 작업에서는 ASP.NET MVC 4의 기능을 재정의 하는 새 브라우저 및 jQuery에서 추가 된 뷰 전환기의 샘플 구현을 살펴봅니다.

1. Visual Studio로 다시 전환 합니다.
2. **Views\Shared** 폴더 아래에 있는 **\_Layout** 을 열고 뷰-전환기 구성 요소가 부분 뷰로 참조 되는지 확인 합니다.

    ![뷰 전환기 구성 요소를 사용 하는 모바일 레이아웃](whats-new-in-aspnet-mvc-4/_static/image29.png "뷰 전환기 구성 요소를 사용 하는 모바일 레이아웃")

    *뷰 전환기 구성 요소를 사용 하는 모바일 레이아웃*
3. **\_ViewSwitcher. cshtml** 부분 뷰를 엽니다.

    부분 뷰는 새로운 메서드인 **ViewContext ()** 를 사용 하 여 웹 요청의 원본을 확인 하 고 해당 링크를 표시 하 여 데스크톱 또는 모바일 보기로 전환 합니다.

    **GetOverriddenBrowser** 메서드는 요청에 대해 현재 설정 된 (실제 또는 재정의) 사용자 에이전트에 해당 하는 **HttpBrowserCapabilitiesBase** 인스턴스를 반환 합니다. 이 값을 사용 하 여 **IsMobileDevice**등의 속성을 가져올 수 있습니다.

    ![ViewSwitcher 부분 뷰](whats-new-in-aspnet-mvc-4/_static/image30.png "ViewSwitcher 부분 뷰")

    *ViewSwitcher 부분 뷰*
4. **Controllers** 폴더에 있는 **ViewSwitcherController.cs** 클래스를 엽니다. ViewSwitcher 구성 요소의 링크에 의해 SwitchView 작업이 호출 되는지 확인 하 고 새 HttpContext 메서드를 확인 합니다.

    - **ClearOverriddenBrowser ()** 메서드는 현재 요청에 대해 재정의 된 사용자 에이전트를 제거 합니다.
    - **SetOverriddenBrowser ()** 메서드는 지정 된 사용자 에이전트를 사용 하 여 요청의 실제 사용자 에이전트 값을 재정의 합니다.  
        ![ViewSwitcher 컨트롤러](whats-new-in-aspnet-mvc-4/_static/image31.png "ViewSwitcher 컨트롤러 ")  
*ViewSwitcher 컨트롤러*

        브라우저 재정의는 ASP.NET MVC 4의 핵심 기능이 며, jQuery 패키지를 설치 하지 않은 경우에도 사용할 수 있습니다. 그러나이 기능은 뷰, 레이아웃 및 부분 뷰에만 영향을 주며, Browser 개체에 종속 된 기능에는 영향을 주지 않습니다.

<a id="Task_5_-_Adding_the_View-Switcher_in_the_Desktop_View"></a>
#### <a name="task-5---adding-the-view-switcher-in-the-desktop-view"></a>작업 5-바탕 화면 보기에서 뷰-전환기 추가

이 작업에서는 뷰 전환기를 포함 하도록 바탕 화면 레이아웃을 업데이트 합니다. 이렇게 하면 모바일 사용자가 바탕 화면 보기를 탐색할 때 모바일 보기로 돌아갈 수 있습니다.

1. **Windows Phone 에뮬레이터**에서 사이트를 새로 고칩니다.
2. 갤러리 위쪽에서 **바탕 화면 보기** 링크를 클릭 합니다. 바탕 화면 보기에는 모바일 보기로 돌아갈 수 있는 뷰 전환기가 없습니다.
3. Visual Studio로 돌아가서 **\_Layout. cshtml** 뷰를 엽니다.
4. 로그인 섹션을 찾은 후 호출을 삽입 하 여 **\_logonpartial** 부분 보기 아래에 **\_viewswitcher** 부분 뷰를 렌더링 합니다. 그런 다음 **ctrl + S** 를 눌러 변경 내용을 저장 합니다.

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample14.cshtml)]
5. **Ctrl + S** 를 눌러 변경 내용을 저장 합니다.
6. Windows Phone 에뮬레이터에서 페이지를 새로 고치고 화면을 두 번 클릭 하 여 확대 합니다. 이제 홈 페이지에 모바일에서 바탕 화면 보기로 전환 하는 **모바일 보기** 링크가 표시 됩니다.

    ![데스크톱 보기에서 렌더링 된 뷰 전환기](whats-new-in-aspnet-mvc-4/_static/image32.png "데스크톱 보기에서 렌더링 된 뷰 전환기")

    *데스크톱 보기에서 렌더링 된 뷰 전환기*
7. 모바일 보기로 다시 전환 하 고 **정보** 페이지 (http://localhost[port]/Home/About)로 이동 합니다. About. Mobile. cshtml 뷰를 만들지 않은 경우에도 모바일 레이아웃을 사용 하 여 About 페이지가 표시 됩니다 (\_Layout. cshtml).

    ![정보 페이지](whats-new-in-aspnet-mvc-4/_static/image33.png "[정보] 페이지")

    *정보 페이지*
8. 마지막으로 데스크톱 웹 브라우저에서 사이트를 엽니다. 이전 업데이트가 바탕 화면 보기에 영향을 미치지 않습니다.

    ![사진 갤러리 바탕 화면 보기](whats-new-in-aspnet-mvc-4/_static/image34.png "사진 갤러리 바탕 화면 보기")

    *사진 갤러리 바탕 화면 보기*

<a id="Task_6_-_Creating_New_Display_Modes"></a>
#### <a name="task-6---creating-new-display-modes"></a>작업 6-새 디스플레이 모드 만들기

새 디스플레이 모드 기능을 사용 하면 응용 프로그램에서 요청을 생성 하는 브라우저에 따라 보기를 선택할 수 있습니다. 예를 들어 데스크톱 브라우저에서 홈 페이지를 요청 하는 경우 응용 프로그램은 **Views\Home\Index.cshtml** 템플릿을 반환 합니다. 그런 다음 모바일 브라우저에서 홈 페이지를 요청 하면 응용 프로그램은 **Views\Home\Index.mobile.cshtml** 템플릿을 반환 합니다.

이 작업에서는 iPhone 장치에 대 한 사용자 지정 레이아웃을 만들고 iPhone 장치에서 요청을 시뮬레이션 해야 합니다. 이렇게 하려면 iPhone 에뮬레이터/시뮬레이터 (예: [전기 모바일 시뮬레이터](http://www.electricplum.com/)) 또는 사용자 에이전트를 수정 하는 추가 기능을 사용 하는 브라우저를 사용할 수 있습니다. Safari 브라우저에서 iPhone을 에뮬레이트하는 사용자 에이전트 문자열을 설정 하는 방법에 대 한 지침은 Alison의 블로그에서 [safari를 사용](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) 하는 방법에 대 한 자세한 내용을 참조 하세요.

**이 태스크는 선택 사항이 며 랩에서 실행 하지 않고 계속 진행할 수 있습니다.**

1. Visual Studio에서 **SHIFT** + **f5** 키를 눌러 응용 프로그램 디버깅을 중지 합니다.
2. **Global.asax.cs** 를 열고 다음 using 문을 추가 합니다.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample15.cs)]
3. 응용 프로그램\_Start 메서드에 다음 강조 표시 된 코드를 추가 합니다.

    (코드 조각- *ASP.NET MVC 4 Lab-Ex03-IPhone DisplayMode*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample16.cs)]

들어오는 각 요청에 대해 일치 하는 정적 **Displaymodeprovider. Instance.** mode 정적 목록 내에 **&quot;iPhone&quot;라는 새 DefaultDisplayMode** 를 등록 했습니다. 들어오는 요청에 &quot;iPhone&quot;문자열이 포함 된 경우 ASP.NET MVC는 이름에 &quot;iPhone&quot; 접미사가 포함 된 뷰를 찾습니다. 0 매개 변수는 특정가 새 모드 인지 여부를 나타냅니다. 예를 들어이 보기는 모바일 장치의 요청과 일치 하는 일반 &quot;모바일&quot; 규칙 보다 더 구체적입니다.

이 코드를 실행 한 후 iPhone 브라우저가 요청을 생성할 때 응용 프로그램은 다음 단계에서 만들 **Views\Shared\\_Layout** 를 사용 합니다.

> [!NOTE]
> IPhone에 대 한 요청을 테스트 하는이 방법은 데모용으로 간소화 되었으며 모든 iPhone 사용자 에이전트 문자열에 대해 예상 대로 작동 하지 않을 수 있습니다 (예: 테스트는 대/소문자를 구분 함).

4. **Views\Shared** 폴더에 **\_layout** 파일의 복사본을 만들고 복사본의 이름을 &quot; **\_layout. cshtml**&quot;로 바꿉니다.
5. 이전 단계에서 만든 **\_Layout. cshtml** 를 엽니다.
6. 데이터 역할 특성이 **페이지** 로 설정 된 div 요소를 **찾고&quot;&quot;** **데이터 테마** 특성을 변경 합니다.

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample17.cshtml)]

이제 ASP.NET MVC 4 응용 프로그램에는 세 가지 레이아웃이 있습니다.

1. **\_레이아웃. cshtml**: 데스크톱 브라우저에 사용 되는 기본 레이아웃입니다.
2. **\_레이아웃. mobile. cshtml**: 모바일 장치에 사용 되는 기본 레이아웃입니다.
3. **\_레이아웃. iphone. cshtml**: 다른 색 구성표를 사용 하 여 \_레이아웃과 구별 하는 iphone 장치에 대 한 특정 레이아웃.
7. **F5** 키를 눌러 응용 프로그램을 실행 하 고 **Windows Phone 에뮬레이터**에서 사이트를 검색 합니다.
8. **Iphone 시뮬레이터** 를 열고 (iphone 시뮬레이터를 설치 및 구성 하는 방법에 대 한 지침은 [부록 C](#AppendixC) 참조) 사이트를 찾아봅니다. 각 휴대폰은 특정 템플릿을 사용 하 고 있습니다.

    ![Using-different-views-for-each-mobile-device2](whats-new-in-aspnet-mvc-4/_static/image35.png)

    *각 모바일 장치에 대해 서로 다른 보기 사용*

<a id="Exercise4"></a>

<a id="Exercise_4_Using_Asynchronous_Controllers"></a>
### <a name="exercise-4-using-asynchronous-controllers"></a>연습 4: 비동기 컨트롤러 사용

Microsoft .NET Framework 4.5에서는 및의 C# 새로운 언어 기능을 도입 하 여 .net 프로그래밍에 비동기에 대 한 새로운 토대를 제공 Visual Basic. 이 새로운 토대를 통해 비동기 프로그래밍은 및와 유사 하 게 동기 프로그래밍으로 만들 수 있습니다. 이제 **Asynccontroller** 클래스를 사용 하 여 ASP.NET MVC 4에서 비동기 작업 메서드를 작성할 수 있습니다. 비동기 작업 메서드는 CPU 바인딩되지 않은 장기 실행 요청에 대해 사용할 수 있습니다. 이렇게 하면 요청이 처리되는 동안 웹 서버의 작업 수행이 차단되지 않습니다. AsyncController 클래스는 일반적으로 장기 실행 웹 서비스 호출에 사용 됩니다.

이 연습에서는 ASP.NET MVC 4의 비동기 작업에 대 한 기본 사항을 설명 합니다. 자세히 알아보려면 다음 문서를 참조 하세요. [ [https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)

<a id="Task_1_-_Implementing_an_Asynchronous_Controller"></a>
#### <a name="task-1---implementing-an-asynchronous-controller"></a>작업 1-비동기 컨트롤러 구현

1. **원본/Ex4-Async/begin/** 폴더에 있는 **시작** 솔루션을 엽니다. 그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.

   1. 제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.
   2. **NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.
   3. 마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.

      > [!NOTE]
      > NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다. NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다. 이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.
2. **Controllers** 폴더에서 **HomeController.cs** 클래스를 엽니다.
3. 다음 using 문을 추가 합니다.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample18.cs)]
4. **Asynccontroller**에서 상속 하도록 **HomeController** 클래스를 업데이트 합니다. AsyncController에서 파생 되는 컨트롤러는 ASP.NET을 사용 하 여 비동기 요청을 처리 하 고 동기 작업 메서드를 여전히 처리할 수 있습니다.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample19.cs)]
5. **Index** 메서드에 **async** 키워드를 추가 하 고 **작업 형식&lt;actionresult&gt;** 반환 하도록 설정 합니다.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample20.cs)]

    > [!NOTE]
    > **Async** 키워드는 .NET Framework 4.5에서 제공 하는 새 키워드 중 하나입니다. 이 메서드에는 비동기 코드가 포함 되어 있음을 컴파일러에 알립니다. **작업** 개체는 나중에 완료 될 수 있는 비동기 작업을 나타냅니다.
6. 클라이언트를 바꿉니다 **.** 아래 표시 된 것 처럼 wait 키워드를 사용 하는 전체 비동기 버전의 getasync () 호출입니다.

    (코드 조각- *ASP.NET MVC 4 Lab-Ex04-GetAsync*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample21.cs)]

    > [!NOTE]
    > 이전 버전에서는 결과가 반환 될 때까지 (동기화 버전) **작업** 개체의 **result** 속성을 사용 하 여 스레드를 차단 했습니다.
    > 
    > **Wait** 키워드를 추가 하면 컴파일러는 메서드 호출에서 반환 된 작업을 비동기적으로 대기 합니다. 즉, 코드의 나머지 부분은 대기 메서드가 완료 된 후에만 콜백으로 실행 됩니다. 이 작업을 수행 하기 위해 try-catch 블록을 변경할 필요는 없습니다. 즉, 백그라운드에서 발생 하는 예외 나 전경에서 발생 하는 예외는 프레임 워크에서 제공 하는 처리기를 사용 하 여 추가 작업 없이 계속 catch 됩니다.
7. 아래와 같이 줄을 새 코드로 바꿔서 비동기 구현을 계속 하려면 코드를 변경 합니다.

    (코드 조각- *ASP.NET MVC 4 Lab-Ex04-ReadAsStringAsync*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample22.cs)]
8. 애플리케이션을 실행합니다. 중요 한 변경 사항은 없지만 코드는 스레드 풀의 스레드를 차단 하 여 서버 리소스를 더 효율적으로 사용 하 고 성능을 개선 하지는 않습니다.

    > [!NOTE]
    > Lab &quot;의 새로운 비동기 프로그래밍 기능에 대 한 자세한 내용은 Visual Studio 학습 키트에 포함 된 **.net C# 4.5의 .net 및 Visual Basic의 비동기 프로그래밍** 을&quot;.

<a id="Task_2_-_Handling_Time-Outs_with_Cancellation_Tokens"></a>
#### <a name="task-2---handling-time-outs-with-cancellation-tokens"></a>작업 2-취소 토큰으로 시간 제한 처리

작업 인스턴스를 반환 하는 비동기 작업 메서드는 제한 시간을 지원할 수도 있습니다. 이 작업에서는 취소 토큰을 사용 하 여 시간 제한 시나리오를 처리 하도록 인덱스 메서드 코드를 업데이트 합니다.

1. Visual Studio로 돌아가서 **SHIFT + f5** 키를 눌러 디버깅을 중지 합니다.
2. **HomeController.cs** 파일에 다음 using 문을 추가 합니다.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample23.cs)]
3. **CancellationToken** 인수를 수신 하도록 인덱스 작업을 업데이트 합니다.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample24.cs)]
4. **Getasync** 호출을 업데이트 하 여 취소 토큰을 전달 합니다.

    (코드 조각- *ASP.NET MVC 4 Lab-Ex04-SendAsync With CancellationToken*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample25.cs)]
5. **Asynctimeout** 특성을 500 밀리초로 설정 하 고 **TaskCanceledException** 를 처리 하도록 구성 된 **handleerror** 특성을 **TimedOut** 뷰로 리디렉션하여 *인덱스* 메서드를 장식 합니다.

    (코드 조각- *ASP.NET MVC 4 Lab-Ex04*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample26.cs)]
6. **사진 컨트롤러** 클래스를 열고 **갤러리** 메서드를 업데이트 하 여 장기 실행 작업을 시뮬레이션 하기 위해 1000 밀리초 (1 초)의 실행을 지연 시킵니다.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample27.cs)]
7. **Web.config** 파일을 열고 다음 요소를 추가 하 여 사용자 지정 오류를 사용 하도록 설정 합니다.

    [!code-xml[Main](whats-new-in-aspnet-mvc-4/samples/sample28.xml)]
8. **Views\Shared** 에 **TimedOut** 라는 새 뷰를 만들고 기본 레이아웃을 사용 합니다. 솔루션 탐색기에서 **Views\Shared** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 보기**.

    ![각 모바일 장치에 대해 서로 다른 보기 사용](whats-new-in-aspnet-mvc-4/_static/image36.png "각 모바일 장치에 대해 서로 다른 보기 사용")

    *각 모바일 장치에 대해 서로 다른 보기 사용*
9. 아래와 같이 **TimedOut** view 콘텐츠를 업데이트 합니다.

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample29.cshtml)]
10. 응용 프로그램을 실행 하 고 루트 URL로 이동 합니다. 스레드를 추가 했으므로 1000 밀리초의 절전 모드를 사용할 경우 **Asynctimeout** 특성에 의해 생성 되 고 **handleerror** 특성에 의해 catch 되는 시간 제한 오류가 발생 **합니다.**

    ![처리 시간 제한 예외](whats-new-in-aspnet-mvc-4/_static/image37.png "처리 시간 제한 예외")

    *처리 시간 제한 예외*

> [!NOTE]
> 또한 [부록 D: 웹 배포을 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시](#AppendixD)를 따라 Microsoft Azure 웹 사이트에이 응용 프로그램을 배포할 수 있습니다.

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습 실습에서는 ASP.NET MVC 4의 새로운 기능 중 일부를 살펴보았습니다. 다음 개념에 대해 설명 했습니다.

- 새 모바일 응용 프로그램 프로젝트 템플릿을 포함 하 여 ASP.NET MVC 프로젝트 템플릿에 대 한 향상 된 기능 활용
- HTML5 뷰포트 특성 및 CSS 미디어 쿼리를 사용 하 여 모바일 장치에 대 한 디스플레이 개선
- 프로그레시브 기능 향상을 위해 jQuery Mobile 사용 및 터치 최적화 웹 UI 빌드
- 모바일 관련 보기 만들기
- 뷰-전환기 구성 요소를 사용 하 여 응용 프로그램에서 모바일 및 데스크톱 보기 사이를 전환 합니다.
- 작업 지원을 사용 하 여 비동기 컨트롤러 만들기

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a>부록 A: 코드 조각 사용

코드 조각을 사용 하면 필요한 모든 코드를 편리 하 게 사용할 수 있습니다. 랩 문서는 다음 그림에 표시 된 것 처럼 사용자가 사용할 수 있는 경우를 정확 하 게 알려줍니다.

![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입](whats-new-in-aspnet-mvc-4/_static/image38.png "Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입")

*Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입*

***키보드를 사용 하 여 코드 조각을 추가 하려면C# (만 해당)***

1. 코드를 삽입할 위치에 커서를 놓습니다.
2. 조각 이름 (공백 또는 하이픈 제외)을 입력 하기 시작 합니다.
3. IntelliSense는 일치 하는 코드 조각의 이름을 표시 합니다.
4. 올바른 코드 조각을 선택 하거나 전체 코드 조각 이름이 선택 될 때까지 계속 입력 합니다.
5. Tab 키를 두 번 눌러 커서 위치에 코드 조각을 삽입 합니다.

![코드 조각 이름 입력 시작](whats-new-in-aspnet-mvc-4/_static/image39.png "코드 조각 이름 입력 시작")

*코드 조각 이름 입력 시작*

![Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.](whats-new-in-aspnet-mvc-4/_static/image40.png "Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.")

*Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.*

![Tab 키를 다시 누르면 코드 조각이 확장 됩니다.](whats-new-in-aspnet-mvc-4/_static/image41.png "Tab 키를 다시 누르면 코드 조각이 확장 됩니다.")

*Tab 키를 다시 누르면 코드 조각이 확장 됩니다.*

***마우스 (C#, VISUAL BASIC 및 XML)를 사용 하 여 코드 조각을 추가 하려면***

1. 코드 조각을 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭 합니다.
2. 코드 **조각 삽입** 을 선택한 다음 **내 코드 조각을**선택 합니다.
3. 목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.

![코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.](whats-new-in-aspnet-mvc-4/_static/image42.png "코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.")

*코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.*

![목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.](whats-new-in-aspnet-mvc-4/_static/image43.png "목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.")

*목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.*

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a>부록 B: 웹에 대 한 Visual Studio Express 2012 설치

**[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)** 를 사용 하 여 웹 또는 다른 &quot;Express&quot; 버전 **에 대해 Microsoft Visual Studio Express 2012** 를 설치할 수 있습니다. 다음 지침에서는 *Microsoft 웹 플랫폼 설치 관리자*를 사용 하 여 *Visual studio Express 2012 for Web* 을 설치 하는 데 필요한 단계를 안내 합니다.

1. [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)로 이동 합니다. 또는 웹 플랫폼 설치 관리자를 이미 설치한 경우에는 웹 플랫폼 설치 관리자를 열고 *Microsoft AZURE SDK&quot;를 사용 하 여 웹 용 2012 Visual Studio Express* &quot;제품을 검색할 수 있습니다.
2. **지금 설치**를 클릭 합니다. **웹 플랫폼 설치 관리자** 가 없으면 먼저이를 다운로드 하 여 설치 하도록 리디렉션됩니다.
3. **웹 플랫폼 설치 관리자** 가 열리면 **설치** 를 클릭 하 여 설치를 시작 합니다.

    ![Visual Studio Express 설치](whats-new-in-aspnet-mvc-4/_static/image44.png "Visual Studio Express 설치")

    *Visual Studio Express 설치*
4. 모든 제품의 라이선스 및 사용 조건을 읽고 **동의** 함을 클릭 하 여 계속 합니다.

    ![사용 조건 동의](whats-new-in-aspnet-mvc-4/_static/image45.png)

    *사용 조건 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](whats-new-in-aspnet-mvc-4/_static/image46.png)

    *설치 진행률*
6. 설치가 완료 되 면 **마침**을 클릭 합니다.

    ![설치 완료](whats-new-in-aspnet-mvc-4/_static/image47.png)

    *설치 완료*
7. **끝내기** 를 클릭 하 여 웹 플랫폼 설치 관리자를 닫습니다.
8. 웹에 대 한 Visual Studio Express를 열려면 **시작** 화면으로 이동 하 &quot;**VS Express**&quot;작성을 시작한 후 **VS Express for Web** 타일을 클릭 합니다.

    ![VS Express for Web 타일](whats-new-in-aspnet-mvc-4/_static/image48.png)

    *VS Express for Web 타일*

<a id="AppendixC"></a>

<a id="Appendix_C_Installing_WebMatrix_2_and_iPhone_Simulator"></a>
## <a name="appendix-c-installing-webmatrix-2-and-iphone-simulator"></a>부록 C: WebMatrix 2 및 iPhone 시뮬레이터 설치

시뮬레이션 된 iPhone 장치에서 사이트를 실행 하려면 iPhone&quot;에 대해 &quot;전자 Mobile 시뮬레이터를 사용 하 여 WebMatrix 확장을 사용할 수 있습니다. 또한 Visual Studio 2012에서 시뮬레이터를 실행 하도록 동일한 확장을 구성할 수 있습니다.

<a id="ApxCTask1"></a>

<a id="Task_1_-_Installing_WebMatrix_2"></a>
#### <a name="task-1---installing-webmatrix-2"></a>작업 1-WebMatrix 2 설치

1. [[https://go.microsoft.com/?linkid=9809776](https://go.microsoft.com/?linkid=9809776)](https://go.microsoft.com/?linkid=9810169)로 이동 합니다. 또는 웹 플랫폼 설치 관리자를 이미 설치한 경우이를 열고 &quot;*WebMatrix 2*&quot;제품을 검색할 수 있습니다.
2. **지금 설치**를 클릭 합니다. **웹 플랫폼 설치 관리자** 가 없으면 먼저이를 다운로드 하 여 설치 하도록 리디렉션됩니다.
3. **웹 플랫폼 설치 관리자** 가 열리면 **설치** 를 클릭 하 여 설치를 시작 합니다.

    ![WebMatrix 설치 2](whats-new-in-aspnet-mvc-4/_static/image49.png "WebMatrix 설치 2")

    *WebMatrix 설치 2*
4. 모든 제품의 라이선스 및 사용 조건을 읽고 **동의** 함을 클릭 하 여 계속 합니다.

    ![사용 조건 동의](whats-new-in-aspnet-mvc-4/_static/image50.png "사용 조건 동의")

    *사용 조건 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](whats-new-in-aspnet-mvc-4/_static/image51.png "설치 진행률")

    *설치 진행률*
6. 설치가 완료 되 면 **마침**을 클릭 합니다.

    ![설치 완료](whats-new-in-aspnet-mvc-4/_static/image52.png "설치 완료")

    *설치 완료*
7. **끝내기** 를 클릭 하 여 웹 플랫폼 설치 관리자를 닫습니다.

<a id="ApxCTask2"></a>

<a id="Task_2_-_Installing_the_iPhone_Simulator_Extension"></a>
#### <a name="task-2---installing-the-iphone-simulator-extension"></a>작업 2-iPhone 시뮬레이터 확장 설치

1. **WebMatrix** 를 실행 하 여 기존 웹 사이트를 열거나 새 사이트를 만듭니다.
2. **홈** 리본 메뉴에서 **실행** 단추를 클릭 하 고 **새로 추가**를 선택 합니다.

    ![새 WebMatrix 확장 추가](whats-new-in-aspnet-mvc-4/_static/image53.png "새 WebMatrix 확장 추가")

    *새 WebMatrix 확장 추가*
3. **IPhone 시뮬레이터** 를 선택 하 고 **설치**를 클릭 합니다.

    ![WebMatrix 확장 검색](whats-new-in-aspnet-mvc-4/_static/image54.png "WebMatrix 확장 검색")

    *WebMatrix 확장 검색*
4. 패키지 세부 정보에서 **설치** 를 클릭 하 여 확장 설치를 계속 합니다.

    ![iPhone 시뮬레이터 확장](whats-new-in-aspnet-mvc-4/_static/image55.png "iPhone 시뮬레이터 확장")

    *iPhone 시뮬레이터 확장*
5. 확장 EULA를 읽고 동의 합니다.

    ![WebMatrix 확장 EULA](whats-new-in-aspnet-mvc-4/_static/image56.png "WebMatrix 확장 EULA")

    *WebMatrix 확장 EULA*
6. 이제 iPhone 시뮬레이터 옵션을 사용 하 여 WebMatrix에서 웹 사이트를 실행할 수 있습니다.

    ![IPhone을 사용 하 여 실행](whats-new-in-aspnet-mvc-4/_static/image57.png "IPhone을 사용 하 여 실행")

    *IPhone을 사용 하 여 실행*

<a id="ApxCTask3"></a>

<a id="Task_3_-_Configuring_Visual_Studio_2012_to_run_iPhone_Simulator"></a>
#### <a name="task-3---configuring-visual-studio-2012-to-run-iphone-simulator"></a>작업 3-iPhone 시뮬레이터를 실행 하는 Visual Studio 2012 구성

1. **Visual Studio 2012** 을 열고 웹 사이트를 열거나 새 프로젝트를 만듭니다.
2. 실행 단추에서 아래쪽 화살표를 클릭 하 고 **찾아보기를**선택 합니다.

    ![찾아보기](whats-new-in-aspnet-mvc-4/_static/image58.png "찾아보기")

    *찾아보기*
3. &quot;&quot;로 찾아보기 대화 상자에서 **추가**를 클릭 합니다.
4. &quot;프로그램 추가&quot; 대화 상자에서 다음 값을 사용 합니다.

   - **프로그램**: C:\Users\*{CurrentUser} * \AppData\Local\Microsoft\WebMatrix\Extensions\20\iPhoneSimulator\ElectricMobileSim\ElectricMobileSim.exe *(그에 따라 경로 업데이트)*
   - **인수**: &quot;1&quot;
   - **이름**: iPhone 시뮬레이터

     ![프로그램 추가](whats-new-in-aspnet-mvc-4/_static/image59.png "프로그램 추가")

     *탐색할 프로그램 추가*
5. **확인** 을 클릭 하 고 대화 상자를 닫습니다.
6. 이제 Visual Studio 2012의 iPhone 시뮬레이터에서 웹 응용 프로그램을 실행할 수 있습니다.

    ![IPhone 시뮬레이터를 사용 하 여 찾아보기](whats-new-in-aspnet-mvc-4/_static/image60.png "IPhone 시뮬레이터를 사용 하 여 찾아보기")

    *IPhone 시뮬레이터를 사용 하 여 찾아보기*

<a id="AppendixD"></a>

<a id="Appendix_D_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-d-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>부록 D: 웹 배포을 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시

이 부록에서는 windows azure 관리 포털에서 새 웹 사이트를 만들고 랩에 따라 가져온 응용 프로그램을 게시 하 여 Windows Azure에서 제공 하는 웹 배포 게시 기능을 활용 하는 방법을 보여 줍니다.

<a id="ApxDTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a>작업 1-Windows Azure 포털에서 새 웹 사이트 만들기

1. [Windows Azure 관리 포털](https://manage.windowsazure.com/) 로 이동 하 고 구독과 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.

    > [!NOTE]
    > Windows Azure를 사용 하면 10 개의 ASP.NET 웹 사이트를 무료로 호스팅한 후 트래픽 증가에 따라 크기를 조정할 수 있습니다. [여기](https://aka.ms/aspnet-hol-azure)에서 등록할 수 있습니다.

    ![Windows Azure Portal에 로그온 합니다.](whats-new-in-aspnet-mvc-4/_static/image61.png "Windows Azure Portal에 로그온 합니다.")

    *Windows Azure 관리 포털에 로그온 합니다.*
2. 명령 모음에서 **새로 만들기** 를 클릭 합니다.

    ![새 웹 사이트 만들기](whats-new-in-aspnet-mvc-4/_static/image62.png "새 웹 사이트 만들기")

    *새 웹 사이트 만들기*
3. **Compute** | **웹 사이트**를 클릭 합니다. 그런 다음 **빠른 생성** 옵션을 선택 합니다. 새 웹 사이트에 사용할 수 있는 URL을 제공 하 고 **웹 사이트 만들기**를 클릭 합니다.

    > [!NOTE]
    > Microsoft Azure 웹 사이트는 사용자가 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램에 대 한 호스트입니다. 빠른 생성 옵션을 사용 하면 포털 외부에서 Windows Azure 웹 사이트에 완료 된 웹 응용 프로그램을 배포할 수 있습니다. 데이터베이스를 설정 하는 단계는 포함 되지 않습니다.

    ![빠른 생성을 사용 하 여 새 웹 사이트 만들기](whats-new-in-aspnet-mvc-4/_static/image63.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")

    *빠른 생성을 사용 하 여 새 웹 사이트 만들기*
4. 새 **웹 사이트가** 만들어질 때까지 기다립니다.
5. 웹 사이트를 만든 후 **URL** 열 아래의 링크를 클릭 합니다. 새 웹 사이트가 작동 하는지 확인 합니다.

    ![새 웹 사이트로 이동](whats-new-in-aspnet-mvc-4/_static/image64.png "새 웹 사이트로 이동")

    *새 웹 사이트로 이동*

    ![웹 사이트 실행 중](whats-new-in-aspnet-mvc-4/_static/image65.png "웹 사이트 실행 중")

    *웹 사이트 실행 중*
6. 포털로 돌아가서 **이름** 열 아래에 있는 웹 사이트의 이름을 클릭 하 여 관리 페이지를 표시 합니다.

    ![웹 사이트 관리 페이지 열기](whats-new-in-aspnet-mvc-4/_static/image66.png "웹 사이트 관리 페이지 열기")

    *웹 사이트 관리 페이지 열기*
7. **대시보드** 페이지의 **빠른** 보기 섹션에서 **게시 프로필 다운로드** 링크를 클릭 합니다.

    > [!NOTE]
    > *게시 프로필* 에는 사용 하도록 설정 된 각 게시 방법에 대해 웹 응용 프로그램을 Windows Azure 웹 사이트에 게시 하는 데 필요한 모든 정보가 포함 되어 있습니다. 게시 프로필에는 게시 방법이 사용 설정된 각 엔드포인트에 연결하고 이에 대해 인증하는 데 필요한 URL, 사용자 자격 증명 및 데이터베이스 문자열이 포함되어 있습니다. **Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** 및 **Microsoft Visual Studio 2012** 는 게시 프로필 읽기를 지원 하 여 웹 응용 프로그램을 Windows Azure 웹 사이트에 게시 하기 위해 이러한 프로그램의 구성을 자동화 합니다.

    ![웹 사이트 게시 프로필을 다운로드 하는 중](whats-new-in-aspnet-mvc-4/_static/image67.png "웹 사이트 게시 프로필을 다운로드 하는 중")

    *웹 사이트 게시 프로필을 다운로드 하는 중*
8. 알려진 위치에 게시 프로필 파일을 다운로드 합니다. 이 연습을 통해이 파일을 사용 하 여 Visual Studio에서 Windows Azure 웹 사이트에 웹 응용 프로그램을 게시 하는 방법을 확인할 수 있습니다.

    ![게시 프로필 파일을 저장 하는 중](whats-new-in-aspnet-mvc-4/_static/image68.png "게시 프로필을 저장 하는 중")

    *게시 프로필 파일을 저장 하는 중*

<a id="ApxDTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>작업 2-데이터베이스 서버 구성

응용 프로그램에서 SQL Server 데이터베이스를 사용 하는 경우 SQL Database 서버를 만들어야 합니다. SQL Server 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 작업을 건너뛸 수 있습니다.

1. 응용 프로그램 데이터베이스를 저장 하기 위한 SQL Database 서버가 필요 합니다. Microsoft Azure 관리 포털의 구독에서 SQL Database 서버를 볼 수는 **SQL 데이터베이스** | **서버** | **서버의 대시보드**. 만든 서버가 없는 경우 명령 모음에서 **추가** 단추를 사용 하 여 만들 수 있습니다. 다음 작업에서 사용할 **서버 이름과 URL, 관리자 로그인 이름 및 암호**를 기록해 둡니다. 이후 단계에서 생성 되므로 아직 데이터베이스를 만들지 마십시오.

    ![SQL Database 서버 대시보드](whats-new-in-aspnet-mvc-4/_static/image69.png "SQL Database 서버 대시보드")

    *SQL Database 서버 대시보드*
2. 다음 작업에서는 Visual Studio에서 데이터베이스 연결을 테스트 합니다. 따라서 서버에서 **허용 되는 Ip 주소**목록에 로컬 IP 주소를 포함 해야 합니다. 이렇게 하려면 **구성**을 클릭 하 고, **현재 클라이언트 IP 주소** 에서 ip 주소를 선택 하 고, **시작 Ip 주소** 및 **끝 ip 주소** 텍스트 상자에 붙여 넣고, ![추가-클라이언트-ip 주소-확인 단추](whats-new-in-aspnet-mvc-4/_static/image70.png) 단추를 클릭 합니다.

    ![클라이언트 IP 주소를 추가 하는 중](whats-new-in-aspnet-mvc-4/_static/image71.png)

    *클라이언트 IP 주소를 추가 하는 중*
3. **클라이언트 Ip 주소가** 허용 된 ip 주소 목록에 추가 되 면 **저장** 을 클릭 하 여 변경 내용을 확인 합니다.

    ![변경 내용 확인](whats-new-in-aspnet-mvc-4/_static/image72.png)

    *변경 내용 확인*

<a id="ApxDTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시

1. ASP.NET MVC 4 솔루션으로 돌아갑니다. **솔루션 탐색기**에서 웹 사이트 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 선택 합니다.

    ![응용 프로그램 게시](whats-new-in-aspnet-mvc-4/_static/image73.png "응용 프로그램 게시")

    *웹 사이트 게시*
2. 첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.

    ![게시 프로필을 가져오는 중](whats-new-in-aspnet-mvc-4/_static/image74.png "게시 프로필을 가져오는 중")

    *게시 프로필을 가져오는 중*
3. **연결 유효성 검사**를 클릭 합니다. 유효성 검사가 완료 되 면 **다음**을 클릭 합니다.

    > [!NOTE]
    > 유효성 검사는 연결 유효성 검사 단추 옆에 녹색 확인 표시가 표시 되 면 완료 됩니다.

    ![연결 유효성 검사](whats-new-in-aspnet-mvc-4/_static/image75.png "연결 유효성 검사")

    *연결 유효성 검사*
4. **설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆에 있는 단추 (즉, **defaultconnection**)를 클릭 합니다.

    ![웹 배포 구성](whats-new-in-aspnet-mvc-4/_static/image76.png "웹 배포 구성")

    *웹 배포 구성*
5. 데이터베이스 연결을 다음과 같이 구성 합니다.

   - **서버 이름** 에 *tcp:* 접두사를 사용 하 여 SQL Database 서버 URL을 입력 합니다.
   - **사용자 이름** 에 서버 관리자 로그인 이름을 입력 합니다.
   - **암호** 에 서버 관리자 로그인 암호를 입력 합니다.
   - 새 데이터베이스 이름 (예: *MVC4SampleDB*)을 입력 합니다.

     ![대상 연결 문자열 구성](whats-new-in-aspnet-mvc-4/_static/image77.png "대상 연결 문자열 구성")

     *대상 연결 문자열 구성*
6. 그런 후 **OK**를 클릭합니다. 데이터베이스를 만들 것인지 묻는 메시지가 표시 되 면 **예**를 클릭 합니다.

    ![데이터베이스 만들기](whats-new-in-aspnet-mvc-4/_static/image78.png "데이터베이스 문자열 만들기")

    *데이터베이스 만들기*
7. Windows Azure에서 SQL Database에 연결 하는 데 사용할 연결 문자열은 기본 연결 텍스트 상자 내에 표시 됩니다. 그런 후 **Next** 를 클릭합니다.

    ![SQL Database를 가리키는 연결 문자열](whats-new-in-aspnet-mvc-4/_static/image79.png "SQL Database를 가리키는 연결 문자열")

    *SQL Database를 가리키는 연결 문자열*
8. **미리 보기** 페이지에서 **게시**를 클릭 합니다.

    ![웹 응용 프로그램 게시](whats-new-in-aspnet-mvc-4/_static/image80.png "웹 응용 프로그램 게시")

    *웹 응용 프로그램 게시*
9. 게시 프로세스가 완료 되 면 기본 브라우저가 게시 된 웹 사이트를 엽니다.

    ![Windows Azure에 게시 된 응용 프로그램](whats-new-in-aspnet-mvc-4/_static/image81.png "Windows Azure에 게시 된 응용 프로그램")

    *Windows Azure에 게시 된 응용 프로그램*
