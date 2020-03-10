---
uid: web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
title: '실습: ASP.NET Web API 및 node.js-ASP.NET 4.x를 사용 하 여 SPA (단일 페이지 응용 프로그램) 빌드'
author: rick-anderson
description: '단계별 코드: ASP.NET 4.x의 ASP.NET Web API 및 node.js를 사용 하 여 SPA (단일 페이지 응용 프로그램)를 빌드합니다.'
ms.author: riande
ms.date: 09/30/2015
ms.custom: seoapril2019
ms.assetid: 719727b7-bef3-45ad-bfe9-ba5bcdb2305f
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
msc.type: authoredcontent
ms.openlocfilehash: 86833a890da759e489dd11dc9afb128a9b7a75e3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448763"
---
# <a name="hands-on-lab-build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs"></a>실습: ASP.NET Web API 및 node.js를 사용 하 여 단일 페이지 응용 프로그램 (SPA) 빌드

[웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 교육 키트 다운로드](https://aka.ms/webcamps-training-kit)

이 랩에서는 ASP.NET 4.x의 ASP.NET Web API 및 node.js를 사용 하 여 SPA (단일 페이지 응용 프로그램)를 빌드하는 방법을 보여 줍니다.

이 실습에서는 이러한 기술을 활용 하 여 SPA 개념을 기반으로 하는 기타 정보 웹 사이트인 Geek of 퀴즈를 구현 합니다. 먼저 ASP.NET Web API를 사용 하 여 서비스 계층을 구현 하 여 퀴즈 질문을 검색 하는 데 필요한 끝점을 노출 하 고 답변을 저장 합니다. 그런 다음 AngularJS 및 CSS3 변환 효과를 사용 하 여 풍부 하 고 응답성이 뛰어난 UI를 빌드합니다.

기존 웹 응용 프로그램에서 클라이언트 (브라우저)는 페이지를 요청 하 여 서버와 통신을 시작 합니다. 그러면 서버에서 요청을 처리 하 고 페이지의 HTML을 클라이언트에 보냅니다. 이후 페이지와의 상호 작용에서 (예: 사용자가 링크로 이동 하거나 데이터를 사용 하 여 양식을 전송 – 새 요청이 서버에 전송 되 고 흐름이 다시 시작 됩니다. 서버는 요청을 처리 하 고 새 작업 요청에 대 한 응답으로 새 페이지를 브라우저로 보냅니다. 클라이언트에서 ed
> 
> SPAs (단일 페이지 응용 프로그램)에서는 초기 요청이 발생 한 후 전체 페이지가 브라우저에 로드 되지만 이후 상호 작용은 Ajax 요청을 통해 수행 됩니다. 즉, 브라우저에서 변경 된 페이지 부분만 업데이트 해야 합니다. 전체 페이지를 다시 로드할 필요가 없습니다. SPA 접근 방식을 사용 하면 응용 프로그램에서 사용자 작업에 응답 하는 데 걸리는 시간이 줄어들고,이로 인해 보다 유체 있는 환경이 제공 됩니다.
> 
> SPA의 아키텍처는 기존 웹 응용 프로그램에 존재 하지 않는 특정 문제를 포함 합니다. 그러나 ASP.NET Web API, AngularJS와 같은 JavaScript 프레임 워크, CSS3에서 제공 하는 새로운 스타일 기능 등의 새로운 기술을 통해 매우 쉽게 디자인 하 고 SPAs를 빌드할 수 있습니다.
> 
> 
> 모든 샘플 코드와 코드 조각은 [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)에서 사용할 수 있는 웹 캠프 교육 키트에 포함 되어 있습니다.

## <a name="overview"></a>개요

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서는 다음 방법에 대해 알아봅니다.

- JSON 데이터를 보내고 받을 ASP.NET Web API 서비스 만들기
- AngularJS를 사용 하 여 반응 형 UI 만들기
- CSS3 변환을 사용 하 여 UI 환경 향상

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>사전 요구 사항

이 실습 실습을 완료 하려면 다음이 필요 합니다.

- [웹 이상의 Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)

<a id="Setup"></a>
### <a name="setup"></a>설치 프로그램

이 실습 랩에서 연습을 실행 하려면 먼저 환경을 설정 해야 합니다.

1. Windows 탐색기를 열고 랩의 **원본** 폴더로 이동 합니다.
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

1. [Web API 만들기](#Exercise1)
2. [SPA 인터페이스 만들기](#Exercise2)

이 랩을 완료 하는 데 소요 되는 예상 시간: **60 분**

> [!NOTE]
> Visual Studio를 처음 시작 하는 경우 미리 정의 된 설정 컬렉션 중 하나를 선택 해야 합니다. 미리 정의 된 각 컬렉션은 특정 개발 스타일에 맞게 디자인 되 고 창 레이아웃, 편집기 동작, IntelliSense 코드 조각 및 대화 상자 옵션을 결정 합니다. 이 실습의 절차에서는 **일반 개발 설정** 컬렉션을 사용 하는 경우 Visual Studio에서 지정 된 작업을 수행 하는 데 필요한 작업을 설명 합니다. 개발 환경에 대해 다른 설정 컬렉션을 선택 하는 경우 고려해 야 하는 단계에 차이가 있을 수 있습니다.

<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-web-api"></a>연습 1: Web API 만들기

SPA의 주요 부분 중 하나는 서비스 계층입니다. UI에서 보낸 Ajax 호출을 처리 하 고 해당 호출에 대 한 응답으로 데이터를 반환 해야 합니다. 검색 된 데이터는 클라이언트에서 구문 분석 되 고 사용 하기 위해 컴퓨터에서 읽을 수 있는 형식으로 제공 되어야 합니다.

Web API 프레임 워크는 ASP.NET 스택의 일부 이며 일반적으로 RESTful API를 통해 JSON 또는 XML 형식의 데이터를 보내고 받는 HTTP 서비스를 쉽게 구현할 수 있도록 설계 되었습니다. 이 연습에서는 Geek of 퀴즈 응용 프로그램을 호스트 하는 웹 사이트를 만든 다음, ASP.NET Web API를 사용 하 여 퀴즈 데이터를 노출 하 고 유지 하기 위해 백 엔드 서비스를 구현 합니다.

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-the-initial-project-for-geek-quiz"></a>작업 1-Geek of 퀴즈를 위한 초기 프로젝트 만들기

이 작업에서는 Visual Studio와 함께 제공 되는 **One ASP.NET** 프로젝트 형식에 따라 ASP.NET Web API를 지 원하는 새 ASP.NET MVC 프로젝트 만들기를 시작 합니다. **한 ASP.NET** 는 모든 ASP.NET 기술을 통합 하 고 원하는 대로 혼합 하 고 일치 시킬 수 있는 옵션을 제공 합니다. 그런 다음 Entity Framework의 모델 클래스와 데이터베이스 이니셜라이저를 추가 하 여 퀴즈 질문을 삽입 합니다.

1. **웹에 대해 Visual Studio Express 2013** 을 열고 파일을 선택 합니다. **| 새 프로젝트** ... 새 솔루션을 시작 합니다.

    ![새 프로젝트 만들기](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image1.png "새 프로젝트 만들기")

    *새 프로젝트 만들기*
2. **새 프로젝트** 대화 상자의 시각적 개체  **C# 에서 ASP.NET 웹 응용 프로그램을 선택 합니다. 웹** 탭. **.NET Framework 4.5** 을 선택 했는지 확인 하 고 이름을 *GeekQuiz*로 지정 하 고 **위치** 를 선택한 다음 **확인**을 클릭 합니다.

    ![새 ASP.NET 웹 응용 프로그램 프로젝트 만들기](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image2.png "새 ASP.NET 웹 응용 프로그램 프로젝트 만들기")

    *새 ASP.NET 웹 응용 프로그램 프로젝트 만들기*
3. **새 ASP.NET 프로젝트** 대화 상자에서 **MVC** 템플릿을 선택 하 고 **Web API** 옵션을 선택 합니다. 또한 **인증** 옵션이 **개별 사용자 계정**으로 설정 되어 있는지 확인 합니다. 계속하려면 **확인** 을 클릭합니다.

    ![Web API 구성 요소를 포함 하 여 MVC 템플릿을 사용 하 여 새 프로젝트 만들기](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image3.png)

    *Web API 구성 요소를 포함 하 여 MVC 템플릿을 사용 하 여 새 프로젝트 만들기*
4. **솔루션 탐색기**에서 **GeekQuiz** 프로젝트의 **모델** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 기존 항목**...

    ![기존 항목 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image4.png "기존 항목 추가")

    *기존 항목 추가*
5. **기존 항목 추가** 대화 상자에서 **원본/자산/모델** 폴더로 이동 하 여 모든 파일을 선택 합니다. **추가**를 클릭합니다.

    ![모델 자산 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image5.png "모델 자산 추가")

    *모델 자산 추가*

    > [!NOTE]
    > 이러한 파일을 추가 하면 Geek of 퀴즈 응용 프로그램에 대 한 데이터 모델, Entity Framework 데이터베이스 컨텍스트 및 데이터베이스 이니셜라이저가 추가 됩니다.
    > 
    > **EF (Entity Framework** )는 관계형 저장소 스키마를 사용 하 여 직접 프로그래밍 하는 대신 개념적 응용 프로그램 모델을 사용 하 여 프로그래밍 하 여 데이터 액세스 응용 프로그램을 만들 수 있도록 하는 ORM (개체 관계형 매퍼)입니다. Entity Framework에 대 한 자세한 내용은 [여기](../../../entity-framework.md)를 참조 하세요.
    > 
    > 다음은 방금 추가한 클래스에 대 한 설명입니다.
    > 
    > - **Triviaoption:** 퀴즈 질문에 연결 된 단일 옵션을 나타냅니다.
    > - **Triviaquestion:** 퀴즈 질문을 나타내고 **options** 속성을 통해 관련 옵션을 노출 합니다.
    > - **Triviaanswer:** 퀴즈 질문에 대 한 응답으로 사용자가 선택한 옵션을 나타냅니다.
    > - **TriviaContext:** geek of 퀴즈 응용 프로그램의 Entity Framework 데이터베이스 컨텍스트를 나타냅니다. 이 클래스는 **Dcontext** 에서 파생 되며 위에서 설명한 엔터티의 컬렉션을 나타내는 **dbset** 속성을 노출 합니다.
    > - **TriviaDatabaseInitializer:** **Createdatabaseifnotexists**에서 상속 되는 **TriviaContext** 클래스에 대 한 Entity Framework 이니셜라이저의 구현입니다. 이 클래스의 기본 동작은 **시드** 메서드에 지정 된 엔터티를 삽입 하는 데이터베이스가 없는 경우에만 데이터베이스를 만드는 것입니다.
6. **Global.asax.cs** 파일을 열고 다음 using 문을 추가 합니다.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample1.cs)]
7. **응용 프로그램\_Start** 메서드의 시작 부분에 다음 코드를 추가 하 여 **TriviaDatabaseInitializer** 를 데이터베이스 이니셜라이저로 설정 합니다.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample2.cs)]
8. 인증 된 사용자에 대 한 액세스를 제한 하도록 **홈** 컨트롤러를 수정 합니다. 이렇게 하려면 **Controllers** 폴더에서 **HomeController.cs** 파일을 열고 **권한 부여** 특성을 **HomeController** 클래스 정의에 추가 합니다.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample3.cs)]

    > [!NOTE]
    > **권한 부여** 필터는 사용자가 인증 되었는지 확인 합니다. 사용자가 인증 되지 않은 경우 작업을 호출 하지 않고 HTTP 상태 코드 401 (권한 없음)을 반환 합니다. 전역, 컨트롤러 수준 또는 개별 작업 수준에서 필터를 적용할 수 있습니다.
9. 이제 웹 페이지와 브랜딩의 레이아웃을 사용자 지정 합니다. 이렇게 하려면 뷰 내에서 **\_Layout** 파일을 엽니다. *ASP.NET 응용 프로그램* 을 *geek of 퀴즈*로 바꿔서 **&lt;title&gt;** 요소의 콘텐츠를 업데이트 합니다.

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample4.cshtml)]
10. 동일한 파일에서 *정보* 및 *연락처* 링크를 제거 하 고 *홈* 링크의 이름을 *Play*로 바꿔서 탐색 모음을 업데이트 합니다. 또한 *응용 프로그램 이름* 링크의 이름을 *geek of 퀴즈*로 바꿉니다. 탐색 모음의 HTML은 다음 코드와 같습니다.

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample5.cshtml)]
11. *My ASP.NET Application* 을 *geek of 퀴즈*로 바꿔서 레이아웃 페이지의 바닥글을 업데이트 합니다. 이렇게 하려면 **&lt;바닥글&gt;** 요소의 내용을 다음 강조 표시 된 코드로 바꿉니다.

    [!code-html[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample6.html)]

<a id="Ex1Task2"></a>
#### <a name="task-2--creating-the-triviacontroller-web-api"></a>작업 2 – TriviaController 웹 API 만들기

이전 작업에서는 Geek of 퀴즈 웹 응용 프로그램의 초기 구조를 만들었습니다. 이제 퀴즈 데이터 모델과 상호 작용 하 고 다음과 같은 작업을 제공 하는 간단한 웹 API 서비스를 작성 합니다.

- **GET/api/trivia**: 인증 된 사용자가 대답할 수 있도록 퀴즈 목록에서 다음 질문을 검색 합니다.
- **POST/api/trivia**: 인증 된 사용자가 지정한 퀴즈 대답을 저장 합니다.

Visual Studio에서 제공 하는 ASP.NET 스 캐 폴딩 도구를 사용 하 여 Web API controller 클래스에 대 한 기준선을 만듭니다.

1. **앱\_시작** 폴더에서 **WebApiConfig.cs** 파일을 엽니다. 이 파일은 웹 api 서비스의 구성을 정의 합니다. 예를 들어, 웹 API 컨트롤러 작업에 경로를 매핑하는 방법입니다.
2. 파일의 시작 부분에 다음 using 문을 추가 합니다.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample7.cs)]
3. **Register** 메서드에 다음 강조 표시 된 코드를 추가 하 여 Web API 동작 메서드에서 검색 된 JSON 데이터에 대 한 포맷터를 전역적으로 구성 합니다.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample8.cs)]

    > [!NOTE]
    > **CamelCasePropertyNamesContractResolver** 는 속성 이름을 JavaScript의 속성 이름에 대 한 일반 규칙으로 자동으로 속성 이름을 *카멜식* case로 변환 합니다.
4. **솔루션 탐색기**에서 **GeekQuiz** 프로젝트의 **Controllers** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 새 스 캐 폴드 항목**....

    ![새 스 캐 폴드 항목 만들기](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image6.png "새 스 캐 폴드 항목 만들기")

    *새 스 캐 폴드 항목 만들기*
5. **스 캐 폴드 추가** 대화 상자에서 왼쪽 창에 **공통** 노드가 선택 되어 있는지 확인 합니다. 그런 다음 가운데 창에서 **WEB API 2 컨트롤러-비어** 있는 템플릿을 선택 하 고 **추가**를 클릭 합니다.

    ![Web API 2 컨트롤러 빈 템플릿 선택](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image7.png "Web API 2 컨트롤러 빈 템플릿 선택")

    *Web API 2 컨트롤러 빈 템플릿 선택*

    > [!NOTE]
    > **ASP.NET 스 캐 폴딩** 은 ASP.NET 웹 응용 프로그램에 대 한 코드 생성 프레임 워크입니다. Visual Studio 2013 MVC 및 Web API 프로젝트용으로 미리 설치 된 코드 생성기를 포함 합니다. 표준 데이터 작업을 개발 하는 데 필요한 시간을 줄이기 위해 데이터 모델과 상호 작용 하는 코드를 신속 하 게 추가 하려는 경우 프로젝트에서 스 캐 폴딩을 사용 해야 합니다.
    > 
    > 또한 스 캐 폴딩 프로세스에서는 모든 필수 종속성이 프로젝트에 설치 되어 있는지 확인 합니다. 예를 들어 빈 ASP.NET 프로젝트로 시작한 다음 스 캐 폴딩을 사용 하 여 Web API 컨트롤러를 추가 하는 경우 필요한 Web API NuGet 패키지와 참조가 프로젝트에 자동으로 추가 됩니다.
6. **컨트롤러 추가** 대화 상자에서 **컨트롤러 이름** 텍스트 상자에 *triviacontroller* 를 입력 하 고 **추가**를 클릭 합니다.

    ![기타 정보 컨트롤러 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image8.png "기타 정보 컨트롤러 추가")

    *기타 정보 컨트롤러 추가*
7. 그런 다음 **TriviaController.cs** 파일을 **GeekQuiz** 프로젝트의 **Controllers** 폴더에 추가 하 고 빈 **triviacontroller** 클래스를 포함 합니다. 파일의 시작 부분에 다음 using 문을 추가 합니다.

    (코드 조각- *AspNetWebApiSpa-Ex1-TriviaControllerUsings*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample9.cs)]
8. **Triviacontroller** 클래스의 시작 부분에 다음 코드를 추가 하 여 컨트롤러에서 **TriviaContext** 인스턴스를 정의, 초기화 및 삭제 합니다.

    (코드 조각- *AspNetWebApiSpa-Ex1-TriviaControllerContext*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample10.cs)]

    > [!NOTE]
    > **Triviacontroller** 의 **Dispose** 메서드는 **TriviaContext** 인스턴스의 **dispose** 메서드를 호출 하 여 **TriviaContext** 인스턴스가 삭제 되거나 가비지 수집 될 때 컨텍스트 개체에서 사용 하는 모든 리소스가 해제 되도록 합니다. 여기에는 Entity Framework에서 연 모든 데이터베이스 연결을 닫는 작업이 포함 됩니다.
9. **Triviacontroller** 클래스의 끝에 다음 도우미 메서드를 추가 합니다. 이 메서드는 지정 된 사용자가 응답할 수 있도록 데이터베이스에서 다음 퀴즈 질문을 검색 합니다.

    (코드 조각- *AspNetWebApiSpa-Ex1-TriviaControllerNextQuestion*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample11.cs)]
10. **Triviacontroller** 클래스에 다음 **Get** 작업 메서드를 추가 합니다. 이 작업 메서드는 이전 단계에서 정의 된 **NextQuestionAsync** 도우미 메서드를 호출 하 여 인증 된 사용자에 대 한 다음 질문을 검색 합니다.

    (코드 조각- *AspNetWebApiSpa-Ex1-TriviaControllerGetAction*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample12.cs)]
11. **Triviacontroller** 클래스의 끝에 다음 도우미 메서드를 추가 합니다. 이 메서드는 지정 된 대답을 데이터베이스에 저장 하 고 답변이 올바른지 여부를 나타내는 부울 값을 반환 합니다.

    (코드 조각- *AspNetWebApiSpa-Ex1-TriviaControllerStoreAsync*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample13.cs)]
12. **Triviacontroller** 클래스에 다음 **Post** 작업 메서드를 추가 합니다. 이 작업 메서드는 인증 된 사용자에 게 응답을 연결 하 고 **StoreAsync** helper 메서드를 호출 합니다. 그런 다음 도우미 메서드에서 반환 된 부울 값을 사용 하 여 응답을 보냅니다.

    (코드 조각- *AspNetWebApiSpa-Ex1-TriviaControllerPostAction*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample14.cs)]
13. **Triviacontroller** 클래스 정의에 **권한 부여** 특성을 추가 하 여 인증 된 사용자에 대 한 액세스를 제한 하도록 Web API 컨트롤러를 수정 합니다.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample15.cs)]

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a>작업 3 – 솔루션 실행

이 작업에서는 이전 작업에서 빌드한 Web API 서비스가 예상 대로 작동 하는지 확인 합니다. Internet Explorer **F12 개발자 도구** 를 사용 하 여 네트워크 트래픽을 캡처하고 웹 API 서비스에서 전체 응답을 검사 합니다.

> [!NOTE]
> Visual Studio 도구 모음에 있는 **시작** 단추에 **Internet Explorer** 가 선택 되어 있는지 확인 합니다.
> 
> ![Internet Explorer 옵션](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image9.png)

1. **F5** 키를 눌러 솔루션을 실행합니다. **로그인** 페이지가 브라우저에 표시 됩니다.

    > [!NOTE]
    > 응용 프로그램이 시작 되 면 기본 MVC 경로가 트리거되고, 기본적으로 **HomeController** 클래스의 **인덱스** 작업에 매핑됩니다. **HomeController** 는 인증 된 사용자로 제한 되므로 (연습 1의 **권한 부여** 특성을 사용 하 여 해당 클래스를 데코레이팅하는 경우) 사용자가 아직 인증 되지 않았으므로 응용 프로그램은 원래 요청을 로그인 페이지로 리디렉션합니다.

    ![솔루션 실행](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image10.png "솔루션 실행")

    *솔루션 실행*
2. **등록** 을 클릭 하 여 새 사용자를 만듭니다.

    ![새 사용자 등록](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image11.png "새 사용자 등록")

    *새 사용자 등록*
3. **등록** 페이지에서 **사용자 이름** 및 **암호**를 입력 한 다음 **등록**을 클릭 합니다.

    ![페이지 등록](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image12.png "페이지 등록")

    *페이지 등록*
4. 응용 프로그램이 새 계정을 등록 하 고 사용자가 인증 되 고 홈 페이지로 다시 리디렉션됩니다.

    ![사용자가 인증 됨](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image13.png "사용자 인증 됨")

    *사용자가 인증 됨*
5. 브라우저에서 **F12** 키를 눌러 **개발자 도구** 패널을 엽니다. **Ctrl + 4** 를 누르거나 **네트워크** 아이콘을 클릭 한 다음 녹색 화살표 단추를 클릭 하 여 네트워크 트래픽 캡처를 시작 합니다.

    ![Web API 네트워크 캡처 시작](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image14.png "Web API 네트워크 캡처 시작")

    *Web API 네트워크 캡처 시작*
6. 브라우저의 주소 표시줄에서 URL에 **api/기타 정보** 를 추가 합니다. 이제 **Triviacontroller**의 **Get** 작업 메서드에서 응답의 세부 정보를 검사 합니다.

    ![Web API를 통해 다음 질문 데이터 검색](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image15.png "Web API를 통해 다음 질문 데이터 검색")

    *Web API를 통해 다음 질문 데이터 검색*

    > [!NOTE]
    > 다운로드가 완료 되 면 다운로드 한 파일을 사용 하 여 작업을 수행 하 라는 메시지가 표시 됩니다. 개발자 도구 창을 통해 응답 콘텐츠를 볼 수 있으려면 대화 상자를 열어 둡니다.
7. 이제 응답의 본문을 검사 합니다. 이렇게 하려면 **세부 정보** 탭을 클릭 한 다음 **응답 본문**을 클릭 합니다. 다운로드 한 데이터가 속성 **옵션** ( **Triviaoption** 개체 목록), **Id** 및 **triviaoption** 클래스에 **해당 하는** 개체 인지 확인할 수 있습니다.

    ![Web API 응답 본문 보기](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image16.png "Web API 응답 본문 보기")

    *Web API 응답 본문 보기*
8. Visual Studio로 돌아가서 **SHIFT + f5** 키를 눌러 디버깅을 중지 합니다.

<a id="Exercise2"></a>
### <a name="exercise-2-creating-the-spa-interface"></a>연습 2: SPA 인터페이스 만들기

이 연습에서는 먼저 **AngularJS**를 사용 하 여 단일 페이지 응용 프로그램 상호 작용에 초점을 맞춘 geek of 퀴즈의 웹 프런트 엔드 부분을 빌드합니다. 그런 다음 CSS3를 사용 하 여 사용자 환경을 개선 하 여 다양 한 애니메이션을 수행 하 고 한 질문에서 다음 질문으로 전환할 때 컨텍스트 전환의 시각적 효과를 제공 합니다.

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-the-spa-interface-using-angularjs"></a>작업 1-AngularJS를 사용 하 여 SPA 인터페이스 만들기

이 태스크에서는 **AngularJS** 를 사용 하 여 geek of 퀴즈 응용 프로그램의 클라이언트측을 구현 합니다. **AngularJS** 는 MVC ( *모델-뷰-컨트롤러* ) 기능을 사용 하 여 브라우저 기반 응용 프로그램을 보강 하 여 개발과 테스트를 모두 용이 하 게 하는 오픈 소스 JavaScript 프레임 워크입니다.

Visual Studio의 패키지 관리자 콘솔에서 AngularJS를 설치 하 여 시작 합니다. 그런 다음 Geek of 퀴즈 앱의 동작과 AngularJS 템플릿 엔진을 사용 하 여 퀴즈 질문 및 답변을 렌더링 하는 뷰를 제공 하는 컨트롤러를 만듭니다.

> [!NOTE]
> AngularJS에 대 한 자세한 내용은 [[http://angularjs.org/](http://angularjs.org/)](http://angularjs.org/)를 참조 하세요.

1. **웹에 대해 Visual Studio Express 2013** 을 열고 **Source/Ex2-GeekQuiz Aspainterface/Begin** 폴더에 있는 솔루션을 엽니다. 또는 이전 연습에서 얻은 솔루션을 계속 사용할 수 있습니다.
2. **도구** > **NuGet 패키지 관리자**에서 **패키지 관리자 콘솔** 을 엽니다. 다음 명령을 입력 하 여 **AngularJS** NuGet 패키지를 설치 합니다.

    [!code-powershell[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample16.ps1)]
3. **솔루션 탐색기**에서 **GeekQuiz** 프로젝트의 **Scripts** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 새 폴더**. 폴더 이름을 **앱** 으로 입력 하 고 **enter**키를 누릅니다.
4. 방금 만든 **앱** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. JavaScript 파일**.

    ![새 JavaScript 파일 만들기](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image17.png)

    *새 JavaScript 파일 만들기*
5. **항목 이름 지정** 대화 상자에서 **항목 이름** 입력란에 *퀴즈-컨트롤러* 를 입력 하 고 **확인**을 클릭 합니다.

    ![새 JavaScript 파일 이름 지정](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image18.png)

    *새 JavaScript 파일 이름 지정*
6. **Quiz-controller** 파일에서 AngularJS **QuizCtrl** controller를 선언 하 고 초기화 하는 다음 코드를 추가 합니다.

    (코드 조각- *AspNetWebApiSpa-Ex2-AngularQuizController*)

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample17.js)]

    > [!NOTE]
    > **QuizCtrl** controller의 constructor 함수는 **$scope**라는 injectable 매개 변수를 필요로 합니다. **$Scope** 개체에 속성을 연결 하 여 생성자 함수에서 범위의 초기 상태를 설정 해야 합니다. 속성은 **뷰 모델**을 포함 하며, 컨트롤러가 등록 될 때 템플릿에 액세스할 수 있습니다.
    > 
    > **QuizCtrl** 컨트롤러는 **QuizApp**라는 모듈 내에서 정의 됩니다. 모듈은 응용 프로그램을 별도의 구성 요소로 나눌 수 있는 작업 단위입니다. 모듈을 사용 하는 경우의 주요 이점은 코드를 보다 쉽게 이해 하 고 단위 테스트, 재사용 및 유지 관리를 용이 하 게 하는 것입니다.
7. 이제 뷰에서 트리거된 이벤트에 반응 하기 위해 범위에 동작을 추가 합니다. **QuizCtrl** 컨트롤러의 끝에 다음 코드를 추가 하 여 **$Scope** 개체에 **nextquestion** 함수를 정의 합니다.

    (코드 조각- *AspNetWebApiSpa-Ex2-AngularQuizControllerNextQuestion*)

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample18.js)]

    > [!NOTE]
    > 이 함수는 이전 연습에서 만든 **기타 정보** 웹 API에서 다음 질문을 검색 하 고 질문 데이터를 **$scope** 개체에 연결 합니다.
8. **QuizCtrl** 컨트롤러의 끝에 다음 코드를 삽입 하 여 **$Scope** 개체에서 **sendanswer** 함수를 정의 합니다.

    (코드 조각- *AspNetWebApiSpa-Ex2-AngularQuizControllerSendAnswer*)

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample19.js)]

    > [!NOTE]
    > 이 함수는 사용자가 선택한 답변을 **기타 정보** Web API에 보내고 결과를 저장 합니다. 예를 들어 답변이 올바르면이 고, 그렇지 않으면 **$scope** 개체입니다.
    > 
    > 위의 **Nextquestion** 및 **Sendanswer** 함수는 AngularJS **$http** 개체를 사용 하 여 브라우저에서 XMLHTTPREQUEST JavaScript 개체를 통해 Web API와의 통신을 추상화 합니다. AngularJS는 RESTful Api를 통해 리소스에 대해 CRUD 작업을 수행 하기 위해 더 높은 수준의 추상화를 제공 하는 다른 서비스를 지원 합니다. AngularJS **$resource** 개체는 **$http** 개체와 상호 작용할 필요 없이 높은 수준의 동작을 제공 하는 동작 메서드를 포함 합니다. CRUD 모델이 필요한 시나리오에서 **$resource** 개체를 사용 하는 것이 좋습니다 (전경 정보, [$resource 설명서](https://docs.angularjs.org/api/ngResource/service/$resource)참조).
9. 다음 단계는 퀴즈에 대 한 뷰를 정의 하는 AngularJS 템플릿을 만드는 것입니다. 이렇게 하려면 뷰 내에서 파일의 인덱스를 엽니다 **.**  **Home** 폴더를 입력 하 고 내용을 다음 코드로 바꿉니다.

    (코드 조각- *AspNetWebApiSpa-Ex2-GeekQuizView*)

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample20.cshtml)]

    > [!NOTE]
    > AngularJS 템플릿은 모델 및 컨트롤러의 정보를 사용 하 여 사용자가 브라우저에서 볼 수 있는 동적 뷰로 정적 태그를 변환 하는 선언적 사양입니다. 다음은 템플릿에서 사용할 수 있는 AngularJS 요소 및 요소 특성의 예입니다.
    > 
    > - **앱** 지시문을 통해 응용 프로그램의 루트 요소를 나타내는 DOM 요소를 AngularJS에 지시할 것입니다.
    > - **컨트롤러** 지시문은 지시문이 선언 된 지점에서 DOM에 컨트롤러를 연결 합니다.
    > - 중괄호 표기법 **{{}}** 은 컨트롤러에 정의 된 범위 속성에 대 한 바인딩을 나타냅니다.
    > - 사용자 **클릭** 에 대 한 응답으로 범위에 정의 된 함수를 호출 하는 데는 클릭 광고 지시문이 사용 됩니다.
10. **Content** 폴더 내에서 **사이트 .css** 파일을 열고 파일 끝에 다음 강조 표시 된 스타일을 추가 하 여 퀴즈 보기에 대 한 모양과 느낌을 제공 합니다.

    (코드 조각- *AspNetWebApiSpa-Ex2-GeekQuizStyles*)

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample21.css)]

<a id="Ex2Task2"></a>
#### <a name="task-2--running-the-solution"></a>작업 2-솔루션 실행

이 작업에서는 AngularJS를 사용 하 여 빌드한 새 사용자 인터페이스를 사용 하 여 솔루션을 실행 하 여 일부 퀴즈 질문에 답변 합니다.

1. **F5** 키를 눌러 솔루션을 실행합니다.
2. 새 사용자 계정을 등록 합니다. 이렇게 하려면 연습 1, 작업 3에 설명 된 등록 단계를 따르세요.

    > [!NOTE]
    > 이전 연습에서 만든 솔루션을 사용 하는 경우 이전에 만든 사용자 계정으로 로그인 할 수 있습니다.
3. 퀴즈의 첫 번째 질문을 보여 주는 **홈** 페이지가 표시 됩니다. 옵션 중 하나를 클릭 하 여 질문에 대답 합니다. 이렇게 하면 이전에 정의 된 **Sendanswer** 함수를 트리거하여 선택한 옵션을 **기타 정보** Web API로 보냅니다.

    ![질문에 답변](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image19.png "질문에 답변")

    *질문에 답변*
4. 단추 중 하나를 클릭 하면 대답이 표시 됩니다. 다음 **질문** 을 클릭 하 여 다음 질문을 표시 합니다. 이렇게 하면 컨트롤러에 정의 된 **Nextquestion** 함수가 트리거됩니다.

    ![다음 질문 요청](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image20.png "다음 질문 요청")

    *다음 질문 요청*
5. 다음 질문이 표시 됩니다. 질문에 대 한 대답을 원하는 횟수 만큼 계속 합니다. 모든 질문을 완료 한 후에는 첫 번째 질문으로 돌아가야 합니다.

    ![다른 질문](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image21.png "다른 질문")

    *다음 질문*
6. Visual Studio로 돌아가서 **SHIFT + f5** 키를 눌러 디버깅을 중지 합니다.

<a id="Ex2Task3"></a>
#### <a name="task-3--creating-a-flip-animation-using-css3"></a>작업 3 – CSS3를 사용 하 여 대칭 이동 애니메이션 만들기

이 작업에서는 CSS3 속성을 사용 하 여 질문에 응답 하 고 다음 질문을 검색할 때 대칭 이동 효과를 추가 하 여 다양 한 애니메이션을 수행 합니다.

1. **솔루션 탐색기**에서 **GeekQuiz** 프로젝트의 **Content** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 기존 항목**...

    ![Content 폴더에 기존 항목 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image22.png "Content 폴더에 기존 항목 추가")

    *Content 폴더에 기존 항목 추가*
2. **기존 항목 추가** 대화 상자에서 **원본/자산** 폴더로 이동한 다음 **대칭 이동 .css**를 선택 합니다. **추가**를 클릭합니다.

    ![자산에서 대칭 .css 파일 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image23.png "자산에서 대칭 .css 파일 추가")

    *자산에서 대칭 .css 파일 추가*
3. 방금 추가한 **대칭 이동 .css** 파일을 열고 콘텐츠를 검사 합니다.
4. **대칭 이동 변환** 주석을 찾습니다. 주석 아래 스타일에서는 CSS **큐브 뷰** 및 **rotateY** 변환을 사용 하 여 &quot;카드 대칭&quot; 효과를 생성 합니다.

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample22.css)]
5. **대칭 이동 중 창 숨기기 창을** 찾습니다. 주석 아래 스타일은 **배경 표면 표시** CSS 속성을 *hidden*으로 설정 하 여 표면에서 반대쪽을 숨깁니다.

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample23.css)]
6. **앱\_시작** 폴더에서 **BundleConfig.cs** 파일을 열고 **&quot;~/content/css&quot;** 스타일 번들에서 **대칭 이동 .css** 파일에 참조를 추가 합니다.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample24.cs)]
7. **F5** 키를 눌러 솔루션을 실행 하 고 자격 증명을 사용 하 여 로그인 합니다.
8. 옵션 중 하나를 클릭 하 여 질문에 대답 합니다. 뷰 간에 전환할 때의 대칭 이동 효과를 확인 합니다.

    ![전환 효과를 사용 하 여 질문에 답변](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image24.png "전환 효과를 사용 하 여 질문에 답변")

    *전환 효과를 사용 하 여 질문에 답변*
9. 다음 **질문** 을 클릭 하 여 다음 질문을 검색 합니다. 대칭 이동 효과가 다시 표시 됩니다.

    ![플립 효과를 사용 하 여 다음 질문 검색](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image25.png "플립 효과를 사용 하 여 다음 질문 검색")

    *플립 효과를 사용 하 여 다음 질문 검색*

---

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습 실습을 완료 하면 다음 방법에 대해 알아보았습니다.

- ASP.NET 스 캐 폴딩을 사용 하 여 ASP.NET Web API 컨트롤러 만들기
- Web API Get 작업을 구현 하 여 다음 퀴즈 질문 검색
- 퀴즈 답변을 저장 하는 웹 API 게시 작업을 구현 합니다.
- Visual Studio 패키지 관리자 콘솔에서 AngularJS 설치
- AngularJS 템플릿 및 컨트롤러 구현
- CSS3 전환을 사용 하 여 애니메이션 효과 수행
