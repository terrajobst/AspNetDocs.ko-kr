---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
title: ASP.NET MVC 4 기본 사항 | Microsoft Docs
author: rick-anderson
description: 이 실습 랩에서는 MVC (모델 뷰 컨트롤러) 음악 저장소, ASP.NET MV를 사용 하는 방법을 단계별로 설명 하는 자습서 응용 프로그램을 기반으로 합니다.
ms.author: riande
ms.date: 02/18/2013
ms.assetid: b7dba543-73c3-4534-a9a0-ba70fa2c6a8a
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
msc.type: authoredcontent
ms.openlocfilehash: 95e9b9f55b2080c0ed01dc34e3a32f9f1c905644
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484571"
---
# <a name="aspnet-mvc-4-fundamentals"></a>ASP.NET MVC 4 기본 사항

[웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 교육 키트 다운로드](https://aka.ms/webcamps-training-kit)

이 실습 랩은 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 소개 하 고 설명 하는 자습서 응용 프로그램 인 MVC (모델 뷰 컨트롤러) 음악 저장소를 기반으로 합니다. 랩 전체에서 이러한 기술을 함께 사용 하는 것이 더 간단 하지만, 간단한 응용 프로그램으로 시작 하 여 완벽 하 게 작동 하는 ASP.NET MVC 4 웹 응용 프로그램을 만들 때까지 빌드를 시작 합니다.

이 랩은 ASP.NET MVC 4와 함께 작동 합니다.

ASP.NET MVC 3 버전의 자습서 응용 프로그램을 탐색 하려는 경우이를 [mvc-음악 저장소](https://github.com/evilDave/MVC-Music-Store)에서 찾을 수 있습니다.

이 실습 랩에서는 개발자가 HTML 및 JavaScript와 같은 웹 개발 기술을 경험 하 고 있다고 가정 합니다.

> [!NOTE]
> 모든 샘플 코드와 코드 조각은 [Microsoft 웹/WebCampTrainingKit 릴리스에서](https://aka.ms/webcamps-training-kit)제공 되는 웹 캠프 교육 키트에 포함 되어 있습니다. 이 랩에서 관련 된 프로젝트는 [ASP.NET MVC 4 기본 사항](https://github.com/Microsoft-Web/HOL-MVC4Fundamentals)에서 제공 됩니다.

<a id="The_Music_Store_application"></a>
### <a name="the-music-store-application"></a>Music Store 응용 프로그램

이 랩에서 구축할 Music Store 웹 응용 프로그램은 쇼핑, 구매 및 관리의 세 가지 주요 부분으로 구성 됩니다. 방문자는 장르별로 앨범을 탐색 하 고, 바구니에 앨범을 추가 하 고, 선택 항목을 검토 하 고, 마지막으로 체크 아웃으로 이동 하 여 주문을 완료할 수 있습니다. 또한 저장소 관리자는 사용 가능한 앨범 뿐만 아니라 주 속성도 관리할 수 있습니다.

![뮤직 저장소 화면](aspnet-mvc-4-fundamentals/_static/image1.png "뮤직 저장소 화면")

*뮤직 저장소 화면*

<a id="ASPNET_MVC_4_Essentials"></a>
### <a name="aspnet-mvc-4-essentials"></a>ASP.NET MVC 4 Essentials

Music Store 응용 프로그램은 응용 프로그램을 세 가지 주요 구성 요소로 구분 하는 아키텍처 패턴 인 **MVC (모델 뷰 컨트롤러)** 를 사용 하 여 빌드됩니다.

- **모델**: 모델 개체는 도메인 논리를 구현 하는 응용 프로그램의 일부입니다. 모델 개체는 또한 데이터베이스에서 모델 상태를 검색 하 고 저장 하는 경우가 많습니다.
- **보기:** 보기는 응용 프로그램 UI (사용자 인터페이스)를 표시 하는 구성 요소입니다. 일반적으로 이 UI는 모델 데이터에서 만들어집니다. 예를 들어 앨범 개체의 현재 상태를 기반으로 하는 드롭다운 목록과 텍스트 상자를 표시 하는 앨범의 편집 뷰가 있습니다.
- **컨트롤러:** 컨트롤러는 사용자 상호 작용을 처리 하 고, 모델을 조작 하 고, 궁극적으로 UI를 렌더링 하는 뷰를 선택 하는 구성 요소입니다. MVC 응용 프로그램에서 뷰는 정보만 표시하고 컨트롤러는 사용자 입력에 대한 응답 및 상호 작용을 처리합니다.

MVC 패턴을 사용 하면 응용 프로그램의 다양 한 측면 (입력 논리, 비즈니스 논리 및 UI 논리)을 분리 하는 동시에 이러한 요소 간의 느슨한 결합을 제공 하는 응용 프로그램을 만들 수 있습니다. 이러한 분리를 통해 응용 프로그램을 빌드할 때 복잡성을 관리할 수 있습니다 .이를 통해 한 번에 하나의 구현 측면에 집중할 수 있습니다. 또한 MVC 패턴을 사용 하면 응용 프로그램을 쉽게 테스트할 수 있으며, 응용 프로그램을 만들기 위해 TDD (테스트 기반 개발)를 사용 하는 것도 좋습니다.

**ASP.NET mvc** 프레임 워크는 ASP.NET Mvc 기반 웹 응용 프로그램을 만들기 위한 ASP.NET Web Forms 패턴의 대안을 제공 합니다. **ASP.NET MVC** 프레임 워크는 웹 폼 기반 응용 프로그램과 마찬가지로 마스터 페이지 및 멤버 기반 인증과 같은 기존 ASP.NET 기능과 통합 되어 핵심 .net framework의 모든 기능을 활용할 수 있는 간단 하 고 테스트 하기 용이한 프레젠테이션 프레임 워크입니다. 이미 사용 하 고 있는 모든 라이브러리를 ASP.NET MVC 4에서 사용할 수 있기 때문에 ASP.NET Web Forms에 이미 익숙한 경우에 유용 합니다.

또한 MVC 응용 프로그램의 세 가지 주요 구성 요소 간의 느슨한 결합은 병렬 개발을 촉진 합니다. 예를 들어 한 개발자가 보기에서 작업 하 고, 두 번째 개발자는 컨트롤러 논리에 대해 작업을 수행할 수 있으며, 세 번째 개발자는 모델의 비즈니스 논리에 집중할 수 있습니다.

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서는 다음 방법에 대해 알아봅니다.

- Music Store 응용 프로그램 자습서를 기반으로 하 여 처음부터 ASP.NET MVC 응용 프로그램 만들기
- 사이트의 홈 페이지에 대 한 Url을 처리 하 고 주 기능을 검색 하는 컨트롤러 추가
- 보기를 추가 하 여 스타일과 함께 표시 되는 콘텐츠를 사용자 지정 합니다.
- 데이터 및 도메인 논리를 포함 하 고 관리 하는 모델 클래스 추가
- 모델 패턴 보기를 사용 하 여 컨트롤러 작업에서 보기 템플릿으로 정보를 전달 합니다.
- 인터넷 응용 프로그램에 대 한 ASP.NET MVC 4 새 템플릿 살펴보기

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>사전 요구 사항

이 랩을 완료 하려면 다음 항목이 있어야 합니다.

- [Visual Studio 2012 Express For Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (설치 방법에 대 한 지침은 [부록 a](#AppendixA) 참조)

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>설치 프로그램

**코드 조각 설치**

편의를 위해이 랩에서 관리 하는 대부분의 코드는 Visual Studio 코드 조각으로 사용할 수 있습니다. 코드 조각을 설치 하려면 **.\Source\Setup\CodeSnippets.vsi** 파일을 실행 합니다.

Visual Studio Code 코드 조각에 대해 잘 모르는 경우이를 사용 하는 방법을 알아보려면이 문서의 부록 [C: 코드 조각&quot;사용](#AppendixC) &quot;부록을 참조할 수 있습니다.

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>실습

이 실습 랩은 다음 연습으로 구성 됩니다.

1. [연습 1: MusicStore ASP.NET MVC 웹 응용 프로그램 프로젝트 만들기](#Exercise1)
2. [연습 2: 컨트롤러 만들기](#Exercise2)
3. [연습 3: 컨트롤러에 매개 변수 전달](#Exercise3)
4. [연습 4: 보기 만들기](#Exercise4)
5. [연습 5: 뷰 모델 만들기](#Exercise5)
6. [연습 6: 뷰에서 매개 변수 사용](#Exercise6)
7. [연습 7: ASP.NET MVC 4 새 템플릿 살펴보기](#Exercise7)

> [!NOTE]
> 각 연습에는 연습을 완료 한 후 얻게 되는 결과 솔루션을 포함 하는 **끝** 폴더가 함께 제공 됩니다. 연습을 진행 하는 데 도움이 필요한 경우이 솔루션을 지침으로 사용할 수 있습니다.

이 랩을 완료 하는 데 소요 되는 예상 시간: **60 분**

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_MusicStore_ASPNET_MVC_Web_Application_Project"></a>
### <a name="exercise-1-creating-musicstore-aspnet-mvc-web-application-project"></a>연습 1: MusicStore ASP.NET MVC 웹 응용 프로그램 프로젝트 만들기

이 연습에서는 Visual Studio 2012 Express for Web 및 기본 폴더 구성에서 ASP.NET MVC 응용 프로그램을 만드는 방법에 대해 설명 합니다. 또한 새 컨트롤러를 추가 하 고 응용 프로그램의 홈 페이지에 간단한 문자열을 표시 하는 방법을 배웁니다.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_ASPNET_MVC_Web_Application_Project"></a>
#### <a name="task-1---creating-the-aspnet-mvc-web-application-project"></a>작업 1-ASP.NET MVC 웹 응용 프로그램 프로젝트 만들기

1. 이 작업에서는 MVC Visual Studio 템플릿을 사용 하 여 빈 ASP.NET MVC 응용 프로그램 프로젝트를 만듭니다. **VS Express for Web**를 시작 합니다.
2. **파일** 메뉴에서 **새 프로젝트**를 클릭합니다.
3. **새 프로젝트** 대화 상자에서 **시각적 개체 C#,** **웹** 템플릿 목록 아래에 있는 **ASP.NET MVC 4 웹 응용 프로그램** 프로젝트 형식을 선택 합니다.
4. **이름** 을 *MvcMusicStore*로 변경 합니다.
5. 이 연습의 원본 폴더에 있는 새 **시작** 폴더 (예: **[\Source\Ex01-CreatingMusicStoreProject\Begin]** ) 내에 솔루션의 위치를 설정 합니다. **확인**을 클릭합니다.

    ![새 프로젝트 만들기 대화 상자](aspnet-mvc-4-fundamentals/_static/image2.png "새 프로젝트 만들기 대화 상자")

    *새 프로젝트 만들기 대화 상자*
6. **새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **기본** 템플릿을 선택 하 고 선택 된 **뷰 엔진이** **Razor**인지 확인 합니다. **확인**을 클릭합니다.

    ![New ASP.NET MVC 4 프로젝트 대화 상자](aspnet-mvc-4-fundamentals/_static/image3.png "New ASP.NET MVC 4 프로젝트 대화 상자")

    *New ASP.NET MVC 4 프로젝트 대화 상자*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Exploring_the_Solution_Structure"></a>
#### <a name="task-2---exploring-the-solution-structure"></a>작업 2-솔루션 구조 탐색

ASP.NET MVC 프레임 워크에는 MVC 패턴을 지 원하는 웹 응용 프로그램을 만드는 데 도움이 되는 Visual Studio 프로젝트 템플릿이 포함 되어 있습니다. 이 템플릿은 필수 폴더, 항목 템플릿 및 구성 파일 항목을 사용 하 여 새 ASP.NET MVC 웹 응용 프로그램을 만듭니다.

이 작업에서는 솔루션 구조를 검사 하 여 관련 된 요소 및 해당 관계를 이해 합니다. ASP.NET MVC 프레임 워크는 기본적으로 구성&quot; 접근 방법에 &quot;규칙을 사용 하 고 폴더 명명 규칙에 따라 몇 가지 기본 가정을 만들기 때문에 모든 ASP.NET MVC 응용 프로그램에는 다음 폴더가 포함 되어 있습니다.

1. 프로젝트를 만든 후에는 오른쪽 솔루션 탐색기에서 생성 된 폴더 구조를 검토 합니다.

    ![솔루션 탐색기 ASP.NET MVC 폴더 구조](aspnet-mvc-4-fundamentals/_static/image4.png "솔루션 탐색기 ASP.NET MVC 폴더 구조")

    *솔루션 탐색기 ASP.NET MVC 폴더 구조*

   1. **컨트롤러**. 이 폴더에는 컨트롤러 클래스가 포함 됩니다. MVC 기반 응용 프로그램에서 컨트롤러는 최종 사용자 상호 작용을 처리 하 고, 모델을 조작 하 고, 궁극적으로 UI를 렌더링 하기 위해 뷰를 선택 하는 일을 담당 합니다.

       > [!NOTE]
       > MVC 프레임 워크에는 모든 컨트롤러의 이름이 &quot;Controller&quot;(예: HomeController, LoginController 또는 제품 컨트롤러)로 끝나야 합니다.
   2. **모델**. 이 폴더는 MVC 웹 응용 프로그램에 대 한 응용 프로그램 모델을 나타내는 클래스에 대해 제공 됩니다. 일반적으로 개체를 정의 하는 코드와 데이터 저장소와 상호 작용 하는 논리를 포함 합니다. 실제 모델 개체의 일반적 위치는 이 폴더가 아니라 별도의 클래스 라이브러리입니다. 그러나 새 응용 프로그램을 만들 때 클래스를 포함 한 다음 개발 주기의 이후 시점에서 별도의 클래스 라이브러리로 이동할 수 있습니다.
   3. **뷰입니다**. 이 폴더는 응용 프로그램의 사용자 인터페이스 표시를 담당 하는 구성 요소인 보기의 권장 위치입니다. 뷰 렌더링 뷰와 관련 된 다른 모든 파일 뿐만 아니라 .aspx, .ascx, cshtml 및 .master 파일을 사용 합니다. Views 폴더에는 각 컨트롤러에 대 한 폴더가 포함 됩니다. 폴더 이름은 컨트롤러 이름 접두사로 지정 됩니다. 예를 들어 **HomeController**라는 컨트롤러가 있는 경우 Views 폴더에 Home 이라는 폴더가 포함 됩니다. 기본적으로 ASP.NET MVC 프레임 워크는 뷰를 로드할 때 Views\controllerName 폴더 (**뷰 [controllerName] [action] .aspx**) 또는 (뷰 **[ControllerName] [action]. cshtml**)에서 요청 된 뷰 이름을 사용 하 여 .aspx 파일을 찾습니다.

      > [!NOTE]
      > 이전에 나열 된 폴더 외에도 MVC 웹 응용 **프로그램은 global.asax 파일을** 사용 하 여 전역 URL 라우팅 기본값을 설정 하 고 **web.config** 파일을 사용 하 여 응용 프로그램을 구성 합니다.

<a id="Ex1Task3"></a>

<a id="Task_3_-_Adding_a_HomeController"></a>
#### <a name="task-3---adding-a-homecontroller"></a>작업 3-HomeController 추가

MVC 프레임 워크를 사용 하지 않는 ASP.NET 응용 프로그램에서 사용자 상호 작용은 페이지를 중심으로 구성 되며 해당 페이지에서 발생 하는 이벤트를 처리 하 고 처리 합니다. 이와 대조적으로 ASP.NET MVC 응용 프로그램과의 사용자 상호 작용은 컨트롤러와 해당 작업 메서드를 중심으로 구성 됩니다.

반면에 ASP.NET MVC 프레임 워크는 컨트롤러 라고 하는 클래스에 Url을 매핑합니다. 컨트롤러는 들어오는 요청을 처리 하 고, 사용자 입력 및 상호 작용을 처리 하 고, 적절 한 응용 프로그램 논리를 실행 하 고, 클라이언트에 다시 전송 하는 응답 (HTML 표시, 파일 다운로드, 다른 URL로 리디렉션 등)을 결정 합니다. HTML을 표시 하는 경우 컨트롤러 클래스는 일반적으로 별도의 뷰 구성 요소를 호출 하 여 요청에 대 한 HTML 태그를 생성 합니다. MVC 응용 프로그램에서 뷰는 정보만 표시하고 컨트롤러는 사용자 입력에 대한 응답 및 상호 작용을 처리합니다.

이 작업에서는 Url을 처리 하는 컨트롤러 클래스를 Music Store 사이트의 홈 페이지에 추가 합니다.

1. 솔루션 탐색기 내의 **Controllers** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** 를 선택한 다음 **컨트롤러** 명령을 선택 합니다.

    ![컨트롤러 명령 추가](aspnet-mvc-4-fundamentals/_static/image5.png "컨트롤러 명령 추가")

    *컨트롤러 추가 명령*
2. **컨트롤러 추가** 대화 상자가 나타납니다. 컨트롤러 이름을 *HomeController* 로 하 고 **추가**를 누릅니다.

    ![컨트롤러 추가 대화 상자](aspnet-mvc-4-fundamentals/_static/image6.png "컨트롤러 추가 대화 상자")

    *컨트롤러 추가 대화 상자*
3. **HomeController.cs** 파일이 **Controllers** 폴더에 만들어집니다. **HomeController** 가 인덱스 작업에서 문자열을 반환 하도록 하려면 **index** 메서드를 다음 코드로 바꿉니다.

    (코드 조각- *ASP.NET MVC 4 기본-Ex1 HomeController Index*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample1.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>작업 4-응용 프로그램 실행

이 작업에서는 웹 브라우저에서 응용 프로그램을 사용해 봅니다.

1. **F5** 키를 눌러 응용 프로그램을 실행 합니다. 프로젝트가 컴파일되고 로컬 IIS 웹 서버가 시작 됩니다. 로컬 IIS 웹 서버에서 웹 서버의 URL을 가리키는 웹 브라우저가 자동으로 열립니다.

    ![웹 브라우저에서 실행 되는 응용 프로그램](aspnet-mvc-4-fundamentals/_static/image7.png "웹 브라우저에서 실행 되는 응용 프로그램")

    *웹 브라우저에서 실행 되는 응용 프로그램*

    > [!NOTE]
    > 로컬 IIS 웹 서버는 사용 가능한 임의의 포트 번호를 사용 하 여 웹 사이트를 실행 합니다. 위의 그림에서 사이트는 `http://localhost:50103/`에서 실행 되므로 포트 50103를 사용 합니다. 포트 번호는 다를 수 있습니다.
2. 브라우저를 닫습니다.

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Controller"></a>
### <a name="exercise-2-creating-a-controller"></a>연습 2: 컨트롤러 만들기

이 연습에서는 Music Store 응용 프로그램의 간단한 기능을 구현 하도록 컨트롤러를 업데이트 하는 방법을 알아봅니다. 해당 컨트롤러는 다음의 각 특정 요청을 처리 하는 작업 메서드를 정의 합니다.

- Music Store의 음악 장르 목록 페이지
- 특정 장르에 대 한 모든 음악 앨범을 나열 하는 찾아보기 페이지
- 특정 음악 앨범에 대 한 정보를 표시 하는 세부 정보 페이지

이 연습의 범위에서 이러한 작업은 단순히 문자열을 반환 합니다.

<a id="Ex2Task1"></a>

<a id="Task_1_-_Adding_a_New_StoreController_Class"></a>
#### <a name="task-1---adding-a-new-storecontroller-class"></a>작업 1-새 StoreController 클래스 추가

이 작업에서는 새 컨트롤러를 추가 합니다.

1. 아직 열려 있지 않으면 **2012 VS Express for Web**시작 합니다.
2. **파일** 메뉴에서 **프로젝트 열기**를 선택 합니다. 프로젝트 열기 대화 상자에서 **Source\Ex02-CreatingAController\Begin**로 이동 하 고 **시작** 을 선택 하 고 **열기**를 클릭 합니다. 또는 이전 연습을 완료 한 후 얻은 솔루션을 계속 사용할 수 있습니다.

   1. 제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.
   2. **NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.
   3. 마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.

      > [!NOTE]
      > NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다. NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다. 이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.
3. 새 컨트롤러를 추가 합니다. 이렇게 하려면 솔루션 탐색기 내의 **Controllers** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** 를 선택한 다음 **컨트롤러** 명령을 클릭 합니다. **컨트롤러 이름을** *StoreController*로 변경 하 고 **추가**를 클릭 합니다.

    ![컨트롤러 추가 대화 상자](aspnet-mvc-4-fundamentals/_static/image8.png "컨트롤러 추가 대화 상자")

    *컨트롤러 추가 대화 상자*

<a id="Ex2Task2"></a>

<a id="Task_2_-_Modifying_the_StoreControllers_Actions"></a>
#### <a name="task-2---modifying-the-storecontrollers-actions"></a>작업 2-StoreController의 작업 수정

이 작업에서는 **작업**이라고 하는 컨트롤러 메서드를 수정 합니다. 작업은 URL 요청을 처리 하 고 브라우저 또는 URL을 호출한 사용자에 게 다시 보내야 하는 콘텐츠를 결정 하는 작업을 담당 합니다.

1. **StoreController** 클래스에는 이미 **인덱스** 메서드가 있습니다. 이 랩에서 나중에 사용 하 여 음악 상점의 모든 장르를 나열 하는 페이지를 구현 합니다. 지금은 **index** 메서드를 Store. index ()&quot;에서 &quot;Hello 문자열을 반환 하는 다음 코드로 바꿉니다.

    (코드 조각- *ASP.NET MVC 4 기본-Ex2 StoreController Index*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample2.cs)]
2. **찾아보기** 및 **세부 정보** 메서드를 추가 합니다. 이렇게 하려면 **StoreController**에 다음 코드를 추가 합니다.

    (코드 조각- *ASP.NET MVC 4 기본-Ex2 StoreController BrowseAndDetails*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample3.cs)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>작업 3-응용 프로그램 실행

이 작업에서는 웹 브라우저에서 응용 프로그램을 사용해 봅니다.

1. **F5** 키를 눌러 응용 프로그램을 실행 합니다.
2. 프로젝트가 **홈** 페이지에서 시작 됩니다. URL을 변경 하 여 각 작업의 구현을 확인 합니다.

    1. **/Store**. **Store. Index ()&quot;에서&quot;Hello** 가 표시 됩니다.
    2. **/Svers를 찾습니다**. **Store. Browse ()&quot;에서&quot;Hello** 가 표시 됩니다.
    3. **/Sv/ds/자세히**입니다. **Store. Details ()&quot;에서&quot;Hello** 가 표시 됩니다.

        ![검색 방법 찾아보기](aspnet-mvc-4-fundamentals/_static/image9.png "검색 방법 찾아보기")

        *검색/이동/찾아보기*
3. 브라우저를 닫습니다.

<a id="Exercise3"></a>

<a id="Exercise_3_Passing_parameters_to_a_Controller"></a>
### <a name="exercise-3-passing-parameters-to-a-controller"></a>연습 3: 컨트롤러에 매개 변수 전달

지금까지 컨트롤러에서 상수 문자열을 반환 했습니다. 이 연습에서는 URL 및 querystring을 사용 하 여 매개 변수를 컨트롤러에 전달한 다음 메서드 작업이 텍스트를 사용 하 여 브라우저에 응답 하 게 하는 방법을 설명 합니다.

<a id="Ex3Task1"></a>

<a id="Task_1_-_Adding_Genre_Parameter_to_StoreController"></a>
#### <a name="task-1---adding-genre-parameter-to-storecontroller"></a>작업 1-StoreController에 장르 매개 변수 추가

이 태스크에서는 **querystring** 을 사용 하 여 **StoreController**의 **Browse** 동작 메서드에 매개 변수를 보냅니다.

1. 아직 열려 있지 않은 경우 **VS Express for Web**를 시작 합니다.
2. **파일** 메뉴에서 **프로젝트 열기**를 선택 합니다. 프로젝트 열기 대화 상자에서 **Source\Ex03-PassingParametersToAController\Begin**로 이동 하 고 **시작** 을 선택 하 고 **열기**를 클릭 합니다. 또는 이전 연습을 완료 한 후 얻은 솔루션을 계속 사용할 수 있습니다.

   1. 제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.
   2. **NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.
   3. 마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.

      > [!NOTE]
      > NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다. NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다. 이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.
3. **StoreController** 클래스를 엽니다. 이렇게 하려면 **솔루션 탐색기**에서 **Controllers** 폴더를 확장 하 고 **StoreController.cs**를 두 번 클릭 합니다.
4. **찾아보기** 메서드를 변경 하 여 특정 장르를 요청 하는 문자열 매개 변수를 추가 합니다. ASP.NET MVC는 호출 될 때 **장르** 라는 모든 querystring 또는 폼 post 매개 변수를이 작업 메서드에 자동으로 전달 합니다. 이렇게 하려면 **Browse** 메서드를 다음 코드로 바꿉니다.

    (코드 조각- *ASP.NET MVC 4 기본-Ex3 StoreController BrowseMethod*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample4.cs)]

> [!NOTE]
> 사용자가 **HtmlEncode** 유틸리티 메서드를 사용 하 여 사용자가/sv/dherer>와 같은 링크를 사용 하 여 Javascript를 뷰에 삽입 하지 못하도록 합니다.  **장르 =&lt;스크립트&gt;창. location = '[http://hackersite.com](http://hackersite.com)'&lt;/script&gt;** .
> 
> 자세한 설명은 [이 msdn 문서](https://msdn.microsoft.com/library/a2a4yykt(v=VS.80).aspx)를 참조 하세요.

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>작업 2-응용 프로그램 실행

이 작업에서는 웹 브라우저에서 응용 프로그램을 사용해 보고 **장르** 매개 변수를 사용 합니다.

1. **F5** 키를 눌러 응용 프로그램을 실행 합니다.
2. 프로젝트가 **홈** 페이지에서 시작 됩니다. URL을/Svs\hers로 변경 *하 시겠습니까? 장르 = Disco* 작업에서 장르 매개 변수를 수신 하는지 확인 합니다.

    ![StoreBrowseGenre = Disco 찾아보기](aspnet-mvc-4-fundamentals/_static/image10.png "StoreBrowseGenre = Disco 찾아보기")

    *검색/선택/찾아보기 장르 = Disco*
3. 브라우저를 닫습니다.

<a id="Ex3Task3"></a>

<a id="Task_3_-_Adding_an_Id_Parameter_Embedded_in_the_URL"></a>
#### <a name="task-3---adding-an-id-parameter-embedded-in-the-url"></a>작업 3-URL에 포함 된 Id 매개 변수 추가

이 태스크에서는 **URL** 을 사용 하 여 **StoreController**의 **Details** action 메서드에 **Id** 매개 변수를 전달 합니다. ASP.NET MVC의 기본 라우팅 규칙은 작업 메서드 이름 뒤에 있는 URL의 세그먼트를 **Id**라는 매개 변수로 처리 하는 것입니다. 작업 메서드에 이름이 Id 인 매개 변수가 있는 경우 ASP.NET MVC는 자동으로 URL 세그먼트를 매개 변수로 전달 합니다. URL **저장소/세부 정보/5**에서 **Id** 는 **5**로 해석 됩니다.

1. **Id**라는 **int** 매개 변수를 추가 하 여 **StoreController**의 **세부 정보** 메서드를 변경 합니다. 이렇게 하려면 **Details** 메서드를 다음 코드로 바꿉니다.

    (코드 조각- *ASP.NET MVC 4 기본-Ex3 StoreController DetailsMethod*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample5.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>작업 4-응용 프로그램 실행

이 작업에서는 웹 브라우저에서 응용 프로그램을 사용해 보고 **Id** 매개 변수를 사용 합니다.

1. **F5** 키를 눌러 응용 프로그램을 실행 합니다.
2. 프로젝트가 **홈** 페이지에서 시작 됩니다. URL을 */Store/Details/5* 로 변경 하 여 동작에서 id 매개 변수를 수신 하는지 확인 합니다.

    ![StoreDetails5 찾아보기](aspnet-mvc-4-fundamentals/_static/image11.png "StoreDetails5 찾아보기")

    */Store/Details/5 찾아보기*

<a id="Exercise4"></a>

<a id="Exercise_4_Creating_a_View"></a>
### <a name="exercise-4-creating-a-view"></a>연습 4: 보기 만들기

지금까지 컨트롤러 작업에서 문자열을 반환 했습니다. 이는 컨트롤러의 작동 방식을 이해 하는 데 유용한 방법 이지만 실제 웹 응용 프로그램을 빌드하는 방법은 아닙니다. 뷰는 템플릿 파일을 사용 하 여 브라우저에 다시 HTML을 생성 하는 더 나은 방법을 제공 하는 구성 요소입니다.

이 연습에서는 사이트의 모양과 느낌을 개선 하는 스타일 시트를 사용 하 여 공용 HTML 콘텐츠에 대 한 템플릿을 설정 하는 레이아웃 마스터 페이지를 추가 하는 방법과 HomeController에서 HTML을 반환 하도록 하는 뷰 템플릿을 설정 하는 방법에 대해 설명 합니다.

<a id="Ex4Task1"></a>

<a id="Task_1_-_Modifying_the_file__layoutcshtml"></a>
#### <a name="task-1---modifying-the-file-_layoutcshtml"></a>작업 1-파일 \_레이아웃 수정. cshtml

File **~/Views/Shared/\_layout. cshtml** 를 사용 하면 전체 웹 사이트에서 사용할 공통 HTML 용 템플릿을 설정할 수 있습니다. 이 작업에서는 홈 페이지 및 상점 영역에 대 한 링크가 포함 된 공통 머리글을 사용 하 여 레이아웃 마스터 페이지를 추가 합니다.

1. 아직 열려 있지 않은 경우 **VS Express for Web**를 시작 합니다.
2. **파일** 메뉴에서 **프로젝트 열기**를 선택 합니다. 프로젝트 열기 대화 상자에서 **Source\ex04-creatingaview\begin**으로 이동 하 여 **begin .sln** 을 선택 하 고 **열기**를 클릭 합니다. 또는 이전 연습을 완료 한 후 얻은 솔루션을 계속 사용할 수 있습니다.

   1. 제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.
   2. **NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.
   3. 마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.

      > [!NOTE]
      > NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다. NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다. 이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.
3. 파일 <strong>\_레이아웃. cshtml</strong> 에는 사이트의 모든 페이지에 대 한 HTML 컨테이너 레이아웃이 포함 되어 있습니다. HTML 응답에 대 한 <strong>&lt;html&gt;</strong> 요소 뿐만 아니라 <strong>&lt;head&gt;</strong> 및 <strong>&lt;body&gt;</strong> 요소를 포함 합니다. HTML 본문 내의 <strong>@RenderBody()</strong> 는 보기 템플릿을 통해 동적 콘텐츠로 채울 수 있는 영역을 식별 합니다.
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample6.cshtml)]
4. 홈 페이지에 대 한 링크가 포함 된 공통 헤더를 추가 하 고 사이트의 모든 페이지에 저장 영역을 추가 합니다. 이 작업을 수행 하려면 &lt;body&gt; 문 아래에 다음 코드를 추가 합니다.
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample7.cshtml)]
5. 각 페이지의 본문 구역을 렌더링 하려면 div를 포함 합니다. <strong>@RenderBody()</strong> 를 강조 표시 된 다음 코드로 바꿉니다.C#()

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample8.cshtml)]

    > [!NOTE]
    > 알고 계십니까? Visual Studio 2012에는 HTML, 코드 파일 등에서 자주 사용 되는 코드를 쉽게 추가할 수 있도록 하는 코드 조각이 있습니다. **&lt;div&gt;** 를 입력 하 고 **tab** 키를 두 번 눌러서 전체 **div** 태그를 삽입 합니다.

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_CSS_Stylesheet"></a>
#### <a name="task-2---adding-css-stylesheet"></a>작업 2-CSS 스타일 시트 추가

빈 프로젝트 템플릿에는 기본 폼 및 유효성 검사 메시지를 표시 하는 데 사용 되는 스타일을 포함 하는 매우 간소화 된 CSS 파일이 포함 되어 있습니다. 사이트의 모양과 느낌을 향상 시키기 위해 디자이너에서 제공 하는 추가 CSS 및 이미지를 사용 합니다.

이 태스크에서는 CSS 스타일 시트를 추가 하 여 사이트의 스타일을 정의 합니다.

1. CSS 파일 및 이미지는이 랩의 **Source\assets\content** 폴더에 포함 되어 있습니다. 응용 프로그램에 추가 하려면 아래와 같이 **Windows 탐색기** 창에서 웹에 대 한 Visual Studio Express의 **솔루션 탐색기** 로 해당 콘텐츠를 끌어 옵니다.

    ![스타일 내용 끌기](aspnet-mvc-4-fundamentals/_static/image12.png "스타일 내용 끌기")

    *스타일 내용 끌기*
2. **사이트 .css** 파일 및 일부 기존 이미지를 바꾸도록 확인 하는 경고 대화 상자가 표시 됩니다. **모든 항목에 적용을** 선택 하 고 **예**를 클릭 합니다.

<a id="Ex4Task3"></a>

<a id="Task_3_-_Adding_a_View_Template"></a>
#### <a name="task-3---adding-a-view-template"></a>작업 3-보기 템플릿 추가

이 작업에서는 뷰 템플릿을 추가 하 여이 연습에서 추가 된 레이아웃 마스터 페이지 및 CSS를 사용 하는 HTML 응답을 생성 합니다.

1. 사이트의 홈 페이지를 검색할 때 보기 템플릿을 사용 하려면 먼저 문자열을 반환 하는 대신 **HomeController Index** 메서드를 사용 하 여 **뷰**를 반환 하도록 지정 해야 합니다. **HomeController** 클래스를 열고 **Index** 메서드를 변경 하 여 **Actionresult**를 반환 하 고 **View ()** 를 반환 하도록 합니다.

    (코드 조각- *ASP.NET MVC 4 기본-Ex4 HomeController Index*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample9.cs)]
2. 이제 적절 한 뷰 템플릿을 추가 해야 합니다. 이렇게 하려면 **인덱스** 동작 메서드 내부를 **마우스 오른쪽 단추로 클릭** 하 고 **뷰 추가**를 선택 합니다. 그러면 **보기 추가** 대화 상자가 표시 됩니다.

    ![Index 메서드 내에서 뷰 추가](aspnet-mvc-4-fundamentals/_static/image13.png "Index 메서드 내에서 뷰 추가")

    *Index 메서드 내에서 뷰 추가*
3. 뷰 **추가** 대화 상자가 표시 되 면 뷰 템플릿 파일을 생성 합니다. 기본적으로이 대화 상자는 뷰 템플릿의 이름을 미리 채워이를 사용 하는 작업 메서드와 일치 시킵니다. HomeController 내의 **index** 동작 메서드 내에서 **뷰 추가** 상황에 맞는 메뉴를 사용 했기 때문에 **뷰 추가** 대화 상자에는 기본 뷰 이름으로 인덱스가 있습니다. **추가**를 클릭합니다.

    ![뷰 추가 대화 상자](aspnet-mvc-4-fundamentals/_static/image14.png "뷰 추가 대화 상자")

    *뷰 추가 대화 상자*
4. Visual Studio는 **Views\Home** 폴더 안에 **Index. cshtml** 뷰 템플릿을 생성 한 다음 엽니다.

    ![만든 홈 인덱스 보기](aspnet-mvc-4-fundamentals/_static/image15.png "만든 홈 인덱스 보기")

    *만든 홈 인덱스 보기*

    > [!NOTE]
    > 인덱스의 이름 및 위치입니다 **. cshtml** 파일은 관련 되며 기본 ASP.NET MVC 명명 규칙을 따릅니다.
    > 
    > \Views\**홈** 폴더는 컨트롤러 이름 (**홈** 컨트롤러)과 일치 합니다. 뷰 템플릿 이름 (**인덱스**)은 뷰를 표시 하는 컨트롤러 작업 메서드와 일치 합니다.
    > 
    > 이러한 방식으로 ASP.NET MVC는이 명명 규칙을 사용 하 여 뷰를 반환할 때 뷰 템플릿의 이름이 나 위치를 명시적으로 지정 하지 않아도 됩니다.
5. 생성 된 뷰 템플릿은\_레이아웃을 기반으로 **합니다. cshtml** 템플릿 이전에 정의 되었습니다. 아래 코드에 표시 된 것 처럼 ViewBag 속성을 **home**으로 업데이트 하 고, 기본 콘텐츠를 **이 홈 페이지**로 변경 합니다.

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample10.cshtml)]
6. 솔루션 탐색기에서 **MvcMusicStore** 프로젝트를 선택 하 고 **F5** 키를 눌러 응용 프로그램을 실행 합니다.

<a id="Ex4Task4"></a>

<a id="Task_4_Verification"></a>
#### <a name="task-4-verification"></a>작업 4: 확인

이전 연습에서 모든 단계를 올바르게 수행 했는지 확인 하려면 다음과 같이 진행 합니다.

응용 프로그램이 브라우저에서 열리면 다음 사항을 확인 해야 합니다.

1. 뷰 템플릿이 표준 명명 규칙을 준수 하기 때문에 HomeController의 인덱스 작업 메서드가 **반환 뷰 ()** 를 호출 하는 경우에도 **\Views\Home\Index.cshtml** view 템플릿을 찾아 표시 합니다.
2. 홈 페이지에는 **\Views\Home\Index.cshtml** view 템플릿 내에 정의 된 환영 메시지가 표시 됩니다.
3. 홈 페이지는 **\_레이아웃** 을 사용 하 고 있으므로 시작 메시지는 표준 사이트 HTML 레이아웃에 포함 됩니다.

    ![정의 된 LayoutPage 및 style을 사용 하는 홈 인덱스 보기](aspnet-mvc-4-fundamentals/_static/image16.png "정의 된 LayoutPage 및 style을 사용 하는 홈 인덱스 보기")

    *정의 된 LayoutPage 및 style을 사용 하는 홈 인덱스 보기*

<a id="Exercise5"></a>

<a id="Exercise_5_Creating_a_View_Model"></a>
### <a name="exercise-5-creating-a-view-model"></a>연습 5: 뷰 모델 만들기

지금 까지는 뷰가 하드 코드 된 HTML을 표시 하지만 동적 웹 응용 프로그램을 만들기 위해 뷰 템플릿이 컨트롤러에서 정보를 받아야 합니다. 이러한 목적으로 사용 되는 일반적인 방법 중 하나는 컨트롤러에서 적절 한 HTML 응답을 생성 하는 데 필요한 모든 정보를 패키지할 수 있도록 하는 **ViewModel** 패턴입니다.

이 연습에서는 ViewModel 클래스를 만들고 필요한 속성을 추가 하는 방법에 대해 알아봅니다. 스토어의 장르 수와 해당 장르 목록입니다. 또한 생성 된 ViewModel을 사용 하도록 StoreController을 업데이트 하 고, 마지막으로 페이지에 언급 된 속성을 표시 하는 새 뷰 템플릿을 만듭니다.

<a id="Ex5Task1"></a>

<a id="Task_1_-_Creating_a_ViewModel_Class"></a>
#### <a name="task-1---creating-a-viewmodel-class"></a>작업 1-ViewModel 클래스 만들기

이 작업에서는 스토어 장르 목록 시나리오를 구현 하는 ViewModel 클래스를 만듭니다.

1. 아직 열려 있지 않은 경우 **VS Express for Web**를 시작 합니다.
2. **파일** 메뉴에서 **프로젝트 열기**를 선택 합니다. 프로젝트 열기 대화 상자에서 **Source\ex05-creatingaviewmodel\begin**으로 이동 하 여 **begin .sln** 을 선택 하 고 **열기**를 클릭 합니다. 또는 이전 연습을 완료 한 후 얻은 솔루션을 계속 사용할 수 있습니다.

   1. 제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.
   2. **NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.
   3. 마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.

      > [!NOTE]
      > NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다. NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다. 이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.
3. ViewModel을 보관할 **Viewmodels** 폴더를 만듭니다. 이렇게 하려면 최상위 **MvcMusicStore** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가** 를 선택한 다음 **새 폴더**를 선택 합니다.

    ![새 폴더 추가](aspnet-mvc-4-fundamentals/_static/image17.png "새 폴더 추가")

    *새 폴더 추가*
4. 폴더 이름을 *Viewmodels*으로 합니다.

    ![솔루션 탐색기의 ViewModels 폴더](aspnet-mvc-4-fundamentals/_static/image18.png "솔루션 탐색기의 ViewModels 폴더")

    *솔루션 탐색기의 ViewModels 폴더*
5. **ViewModel** 클래스를 만듭니다. 이렇게 하려면 최근에 만든 **Viewmodels** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** , **새 항목**을 차례로 선택 합니다. **코드**에서 **클래스** 항목을 선택 하 고 파일 이름을 *StoreIndexViewModel.cs*으로 지정한 다음 **추가**를 클릭 합니다.

    ![새 클래스 추가](aspnet-mvc-4-fundamentals/_static/image19.png "새 클래스 추가")

    *새 클래스 추가*

    ![이 클래스 만들기](aspnet-mvc-4-fundamentals/_static/image20.png "이 클래스 만들기")

    *이 클래스 만들기*

<a id="Ex5Task2"></a>

<a id="Task_2_-_Adding_Properties_to_the_ViewModel_class"></a>
#### <a name="task-2---adding-properties-to-the-viewmodel-class"></a>작업 2-ViewModel 클래스에 속성 추가

예상 되는 HTML 응답을 생성 하기 위해 StoreController에서 뷰 템플릿으로 전달 되는 두 개의 매개 변수 (매장의 장르 수와 해당 장르 목록)가 있습니다.

이 태스크에서는 해당 2 개의 속성을 **사용자의 사용자** 속성: **numberofgenres** (정수) 및 **장르** (문자열 목록)에 추가 합니다.

1. 이 클래스에 **numberofgenres** 및 **장르** 속성을 **추가 합니다.** 이렇게 하려면 클래스 정의에 다음 두 줄을 추가 합니다.

    (코드 조각- *ASP.NET MVC 4 기본-Ex5 StoreIndexViewModel 속성*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample11.cs)]

> [!NOTE]
> **{Get; set;}** 표기법은의 자동 구현 C#속성 기능을 사용 합니다. 지원 필드를 선언 하지 않고도 속성의 이점을 제공 합니다.

<a id="Ex5Task3"></a>

<a id="Task_3_-_Updating_StoreController_to_use_the_StoreIndexViewModel"></a>
#### <a name="task-3---updating-storecontroller-to-use-the-storeindexviewmodel"></a>작업 3-StoreController Indexviewmodel을 사용 하도록 업데이트

StoreController **Indexviewmodel** 클래스는 응답을 생성 하기 위해의 **인덱스** 메서드를 뷰 템플릿으로 전달 하는 데 필요한 정보를 캡슐화 합니다.

이 작업에서는 **StoreController** **인덱스 viewmodel**을 사용 하도록 해당 사용자를 업데이트 합니다.

1. **StoreController** 클래스를 엽니다.

    ![StoreController 클래스 열기](aspnet-mvc-4-fundamentals/_static/image21.png "StoreController 클래스 열기")

    *StoreController 클래스 열기*
2. **StoreController에서** **indexviewmodel** 클래스를 사용 하려면 **StoreController** 코드의 맨 위에 다음 네임 스페이스를 추가 합니다.

    (코드 조각- *ASP.NET MVC 4 기본 사항-ViewModels을 사용 하 여 Ex5 StoreIndexViewModel*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample12.cs)]
3. **StoreController**의 **Index** 동작 메서드를 변경 하 여이 개체를 만들고이 **개체를 뷰** 템플릿에 전달 하 여 HTML 응답을 생성 합니다.

    > [!NOTE]
    > Lab &quot;ASP.NET MVC 모델 및 데이터 액세스&quot; 데이터베이스에서 스토어 장르 목록을 검색 하는 코드를 작성 합니다. 다음 코드에서는 복사본 **인덱스 viewmodel**을 채울 더미 데이터 장르 **목록을** 만듭니다.
    > 
    > 이 개체를 만들고 설정 하면 **해당 개체는** **뷰** 메서드에 인수로 전달 됩니다. 이는 뷰 템플릿에서 해당 개체를 사용 하 여 HTML 응답을 생성 한다는 것을 나타냅니다.
4. **Index** 메서드를 다음 코드로 바꿉니다.

    (코드 조각- *ASP.NET MVC 4 기본-Ex5 StoreController Index 메서드*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample13.cs)]

> [!NOTE]
> 에 C#익숙하지 않은 경우 **var** 을 사용 한다고 해 서 **viewModel** 변수가 런타임에 바인딩되어 있다고 가정할 수 있습니다. 올바르지 **않습니다. 컴파일러**는 C# 변수에 할당 된 항목을 기반으로 하는 형식 유추를 사용 하 여 **viewModel** 이 복사본 형식 인지 여부를 확인 합니다. 또한 로컬 **viewModel** **변수를 기능 코드 형식으로** 컴파일하면 컴파일 시간 검사 및 Visual Studio 코드 편집기를 사용할 수 있습니다.

<a id="Ex5Task4"></a>

<a id="Task_4_-_Creating_a_View_Template_that_Uses_StoreIndexViewModel"></a>
#### <a name="task-4---creating-a-view-template-that-uses-storeindexviewmodel"></a>작업 4-기능을 사용 하는 뷰 템플릿 만들기

이 태스크에서는 컨트롤러에서 전달 된 복사본 인덱스 Viewmodel 개체를 사용 하 여 장르 목록을 표시 하는 보기 템플릿을 만듭니다.

1. 새 뷰 템플릿을 만들기 전에 **보기 추가 대화 상자** 에서 자동으로 파일 **인덱스 viewmodel** 클래스를 인식할 수 있도록 프로젝트를 빌드합니다. **빌드** 메뉴 항목을 선택한 다음 **MvcMusicStore 빌드**를 선택 하 여 프로젝트를 빌드합니다.

    ![프로젝트 빌드](aspnet-mvc-4-fundamentals/_static/image22.png "프로젝트 빌드")

    *프로젝트 빌드*
2. 새 뷰 템플릿을 만듭니다. 이렇게 하려면 **Index** 메서드 내부를 마우스 오른쪽 단추로 클릭 하 고 **뷰 추가**를 선택 합니다.

    ![보기 추가](aspnet-mvc-4-fundamentals/_static/image23.png "보기 추가")

    *보기 추가*
3. **뷰 추가 대화 상자** 는 **StoreController**에서 호출 되기 때문에 기본적으로 **\Views\Store\Index.cshtml** 파일에 뷰 템플릿이 추가 됩니다. 강력한 형식의 **뷰 만들기** 확인란을 선택 하 고 **모델 클래스로**이 클래스 **이름 지정** 을 선택 합니다. 또한 선택 된 뷰 엔진이 **Razor**인지 확인 합니다. **추가**를 클릭합니다.

    ![뷰 추가 대화 상자](aspnet-mvc-4-fundamentals/_static/image24.png "뷰 추가 대화 상자")

    *뷰 추가 대화 상자*

    **\Views\Store\Index.cshtml** View 템플릿 파일을 만들고 엽니다. 보기 템플릿은 마지막 단계에서 **보기 추가** 대화 상자에 제공 된 정보를 기준으로 HTML **응답을 생성** 하는 데 사용할 데이터를 데이터로 사용 합니다. 템플릿이에서 C#`ViewPage<musicstore.viewmodels.storeindexviewmodel>`를 상속 하는 것을 알 수 있습니다.

<a id="Ex5Task5"></a>

<a id="Task_5_-_Updating_the_View_Template"></a>
#### <a name="task-5---updating-the-view-template"></a>작업 5-보기 템플릿 업데이트

이 태스크에서는 마지막 작업에서 만든 보기 템플릿을 업데이트 하 여 장르 수와 페이지 내에서의 해당 이름을 검색 합니다.

> [!NOTE]
> @ 구문 (&quot;code 너 깃&quot;라고도 함)을 사용 하 여 뷰 템플릿 내에서 코드를 실행 합니다.

1. **인덱스 cshtml** 파일의 **Store** 폴더 내에서 해당 코드를 다음 코드로 바꿉니다.

[!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample14.cshtml)]

    > [!NOTE]
    > As soon as you finish typing the period after the word **Model**, Visual Studio's Intellisense will show a list of possible properties and methods to choose from.
    > 
    > ![](aspnet-mvc-4-fundamentals/_static/image25.png)
    > 
    > *Getting Model properties and methods with Visual Studio's IntelliSense*
    > 
    > The **Model** property references the **StoreIndexViewModel** object that the Controller passed to the View template. This means that you can access all of the data passed from the Controller to the View template via the **Model** property, and format it into an appropriate HTML response within the View template.
    > 
    > You can just select the **NumberOfGenres** property from the Intellisense list rather than typing it in and then it will auto-complete it by pressing the **tab key**.
2. 을 (를) 사용 하 여에 있는 장르 목록에 대해 루프를 **실행 하 고** **foreach** 루프를 사용 하 여 HTML **&lt;ul&gt;** 목록을 만듭니다.
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample15.cshtml)]
3. **F5** 키를 눌러 응용 프로그램을 실행 하 고 **/Store**를 검색 합니다. **StoreController** 에서 보기 템플릿에 전달 된 장르 목록이 표시 됩니다. **이 개체는 해당 개체** 에 전달 됩니다.

    ![장르 목록을 표시 하는 보기](aspnet-mvc-4-fundamentals/_static/image26.png "장르 목록을 표시 하는 보기")

    *장르 목록을 표시 하는 보기*
4. 브라우저를 닫습니다.

<a id="Exercise6"></a>

<a id="Exercise_6_Using_Parameters_in_View"></a>
### <a name="exercise-6-using-parameters-in-view"></a>연습 6: 뷰에서 매개 변수 사용

연습 3에서는 매개 변수를 컨트롤러에 전달 하는 방법을 배웠습니다. 이 연습에서는 보기 템플릿에서 해당 매개 변수를 사용 하는 방법을 배웁니다. 이러한 목적을 위해 데이터 및 도메인 논리를 관리 하는 데 도움이 되는 모델 클래스를 먼저 소개 합니다. 또한 URL 경로 인코딩과 같은 항목을 걱정 하지 않고 ASP.NET MVC 응용 프로그램 내에서 페이지에 대 한 링크를 만드는 방법을 배웁니다.

<a id="Ex6Task1"></a>

<a id="Task_1_-_Adding_Model_Classes"></a>
#### <a name="task-1---adding-model-classes"></a>작업 1-모델 클래스 추가

컨트롤러에서 뷰로 정보를 전달 하기 위해 만들어진 ViewModels과 달리 모델 클래스는 데이터 및 도메인 논리를 포함 하 고 관리 하기 위해 빌드됩니다. 이 작업에서는 **장르** 및 **앨범**이라는 두 가지 모델 클래스를 추가 하 여 이러한 개념을 나타냅니다.

1. 아직 열려 있지 않은 경우 시작 **VS Express for Web**
2. **파일** 메뉴에서 **프로젝트 열기**를 선택 합니다. 프로젝트 열기 대화 상자에서 **Source\Ex06-UsingParametersInView\Begin**로 이동 하 고 **시작** 을 선택 하 고 **열기**를 클릭 합니다. 또는 이전 연습을 완료 한 후 얻은 솔루션을 계속 사용할 수 있습니다.

   1. 제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.
   2. **NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.
   3. 마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.

      > [!NOTE]
      > NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다. NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다. 이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.
3. **장르** 모델 클래스를 추가 합니다. 이렇게 하려면 **솔루션 탐색기**의 **모델** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** 를 선택한 다음 **새 항목** 옵션을 선택 합니다. **코드**에서 **클래스** 항목을 선택 하 고 파일 이름을 *Genre.cs*으로 지정한 다음 **추가**를 클릭 합니다.

    ![클래스 추가](aspnet-mvc-4-fundamentals/_static/image27.png "클래스 추가")

    *새 항목 추가*

    ![장르 모델 클래스 추가](aspnet-mvc-4-fundamentals/_static/image28.png "장르 모델 클래스 추가")

    *장르 모델 클래스 추가*
4. 장르 클래스에 **이름** 속성을 추가 합니다. 이렇게 하려면 다음 코드를 추가 합니다.

    (코드 조각- *ASP.NET MVC 4 기본-Ex6 장르*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample16.cs)]
5. 이전과 동일한 절차를 수행 하 여 **앨범** 클래스를 추가 합니다. 이렇게 하려면 **솔루션 탐색기**의 **모델** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** 를 선택한 다음 **새 항목** 옵션을 선택 합니다. **코드**에서 **클래스** 항목을 선택 하 고 파일 이름을 *Album.cs*으로 지정한 다음 **추가**를 클릭 합니다.
6. 앨범 클래스에 **장르** 및 **제목**이라는 두 가지 속성을 추가 합니다. 이렇게 하려면 다음 코드를 추가 합니다.

    (코드 조각- *ASP.NET MVC 4 기본-Ex6 앨범*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample17.cs)]

<a id="Ex6Task2"></a>

<a id="Task_2_-_Adding_a_StoreBrowseViewModel"></a>
#### <a name="task-2---adding-a-storebrowseviewmodel"></a>작업 2-StoreBrowseViewModel 추가

**StoreBrowseViewModel** 은이 작업에서 선택 된 장르와 일치 하는 앨범을 표시 하는 데 사용 됩니다. 이 작업에서는이 클래스를 만든 후 **장르** 및 해당 **앨범**목록을 처리 하는 두 개의 속성을 추가 합니다.

1. **StoreBrowseViewModel** 클래스를 추가 합니다. 이렇게 하려면 **솔루션 탐색기**의 **viewmodels** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** 를 선택한 다음 **새 항목** 옵션을 선택 합니다. **코드**에서 **클래스** 항목을 선택 하 고 파일 이름을 *StoreBrowseViewModel.cs*으로 지정한 다음 **추가**를 클릭 합니다.
2. **StoreBrowseViewModel** 클래스에서 모델에 대 한 참조를 추가 합니다. 이렇게 하려면 네임 스페이스를 사용 하 여 다음을 추가 합니다.

    (코드 조각- *ASP.NET MVC 4 기본-Ex6 UsingModel*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample18.cs)]
3. **StoreBrowseViewModel** 클래스: **장르** 및 **앨범**에 두 개의 속성을 추가 합니다. 이렇게 하려면 다음 코드를 추가 합니다.

    (코드 조각- *ASP.NET MVC 4 기본-Ex6 ModelProperties*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample19.cs)]

> [!NOTE]
> **List&lt;앨범&gt;** ?:이 정의는 **list&lt;t&gt;** 형식을 사용 합니다. 여기서 **t** 는이 **목록의** 요소가 속하는 형식 ( **이 경우에** 는 해당 항목 또는 해당 하위 항목)에 대 한 형식을 제한 합니다.
> 
> 클래스 또는 메서드를 클라이언트 코드에서 선언 하 고 인스턴스화할 때까지 하나 이상의 형식에 대 한 사양을 지연 하는 클래스 및 메서드를 디자인 하는 기능은 **제네릭**이라는 C# 언어의 기능입니다.
> 
> **List&lt;t&gt;** 는 **ArrayList** 형식에 해당 하는 제네릭 이며 **system.object** 네임 스페이스에서 사용할 수 있습니다. **제네릭을** 사용 하는 경우의 이점 중 하나는 형식이 지정 된 경우에는 **ArrayList**를 사용 하는 것 처럼 요소를 **앨범** 으로 캐스팅 하는 것과 같은 형식 검사 작업을 처리할 필요가 없다는 것입니다.

<a id="Ex6Task3"></a>

<a id="Task_3_-_Using_the_New_ViewModel_in_the_StoreController"></a>
#### <a name="task-3---using-the-new-viewmodel-in-the-storecontroller"></a>작업 3-StoreController에서 새 ViewModel 사용

이 작업에서는 새 **StoreBrowseViewModel**를 사용 하도록 **StoreController**의 **Browse** 및 **Details** 작업 메서드를 수정 합니다.

1. **StoreController** 클래스의 모델 폴더에 대 한 참조를 추가 합니다. 이렇게 하려면 **솔루션 탐색기** 의 **컨트롤러** 폴더를 확장 하 고 **StoreController** 클래스를 엽니다. 그런 후에 다음 코드를 추가 합니다.

    (코드 조각- *ASP.NET MVC 4 기본-Ex6 UsingModelInController*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample20.cs)]
2. **StoreViewBrowseController** 클래스를 사용 하도록 **Browse** action 메서드를 대체 합니다. 더미 데이터를 사용 하 여 장르와 두 개의 새 앨범 개체를 만듭니다. 다음 실습 랩에서는 데이터베이스의 실제 데이터를 사용 합니다. 이렇게 하려면 **Browse** 메서드를 다음 코드로 바꿉니다.

    (코드 조각- *ASP.NET MVC 4 기본-Ex6 BrowseMethod*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample21.cs)]
3. **StoreViewBrowseController** 클래스를 사용 하도록 **Details** 작업 메서드를 대체 합니다. **뷰에**반환 될 새 **앨범** 개체를 만듭니다. 이렇게 하려면 **Details** 메서드를 다음 코드로 바꿉니다.

    (코드 조각- *ASP.NET MVC 4 기본-Ex6 DetailsMethod*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample22.cs)]

<a id="Ex6Task4"></a>

<a id="Task_4_-_Adding_a_Browse_View_Template"></a>
#### <a name="task-4---adding-a-browse-view-template"></a>작업 4-찾아보기 보기 템플릿 추가

이 작업에서는 특정 장르에 대해 찾은 앨범을 표시 하는 **찾아보기** 보기를 추가 합니다.

1. 새 뷰 템플릿을 만들기 전에 **보기 추가** 대화 상자에서 사용할 **ViewModel** 클래스에 대해 알 수 있도록 프로젝트를 빌드해야 합니다. **빌드** 메뉴 항목을 선택한 다음 **MvcMusicStore 빌드**를 선택 하 여 프로젝트를 빌드합니다.
2. **찾아보기** 보기를 추가 합니다. 이렇게 하려면 **StoreController** 의 **찾아보기** 동작 메서드를 마우스 오른쪽 단추로 클릭 하 고 **뷰 추가**를 클릭 합니다.
3. **보기 추가** 대화 상자에서 보기 이름이 **찾아보기**인지 확인 합니다. **강력한 형식의 뷰 만들기** 확인란을 선택 하 고 **모델 클래스** 드롭다운에서 **StoreBrowseViewModel** 를 선택 합니다. 다른 필드는 기본값으로 둡니다. 그런 다음, **추가**를 클릭합니다.

    ![찾아보기 보기 추가](aspnet-mvc-4-fundamentals/_static/image29.png "찾아보기 보기 추가")

    *찾아보기 보기 추가*
4. StoreBrowseViewModel를 **수정 하 여** 장르 정보를 표시 하 고 뷰 템플릿에 전달 되는 개체에 액세스 합니다. 이렇게 하려면 콘텐츠를 다음으로 바꿉니다. (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample23.cshtml)]

<a id="Ex6Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>작업 5-응용 프로그램 실행

이 작업에서는 browse 메서드가 **browse** **메서드 작업** 에서 앨범을 검색 하도록 테스트 합니다.

1. **F5** 키를 눌러 응용 프로그램을 실행 합니다.
2. 프로젝트가 홈 페이지에서 시작 됩니다. URL을/Svs\hers로 변경 **하 시겠습니까? 장르 = Disco** 작업에서 두 개의 앨범이 반환 되는지 확인 합니다.

    ![저장소 검색 Disco 앨범](aspnet-mvc-4-fundamentals/_static/image30.png "저장소 검색 Disco 앨범")

    *저장소 검색 Disco 앨범*

<a id="Ex6Task6"></a>

<a id="Task_6_-_Displaying_information_About_a_Specific_Album"></a>
#### <a name="task-6---displaying-information-about-a-specific-album"></a>작업 6-특정 앨범에 대 한 정보 표시

이 태스크에서는 **저장소/세부 정보** 보기를 구현 하 여 특정 앨범에 대 한 정보를 표시 합니다. 이 실습 랩에서는 앨범에 대해 표시 되는 모든 항목이 **보기** 템플릿에 이미 포함 되어 있습니다. 따라서 **StoreDetailsViewModel** 클래스를 만드는 대신 현재 **StoreBrowseViewModel** 템플릿을 사용 하 여 앨범을 전달 합니다.

1. 필요한 경우 브라우저를 닫고 Visual Studio 창으로 돌아갑니다. **StoreController**의 **details** 작업 메서드에 대 한 새 **세부 정보** 보기를 추가 합니다. 이렇게 하려면 **StoreController** 클래스에서 **Details** 메서드를 마우스 오른쪽 단추로 클릭 하 고 **뷰 추가**를 클릭 합니다.
2. **보기 추가** 대화 상자에서 **보기 이름이** **Details**인지 확인 합니다. **강력한 형식의 뷰 만들기** 확인란을 선택 하 고 **모델 클래스** 드롭다운에서 **앨범** 을 선택 합니다. 다른 필드는 기본값으로 둡니다. 그런 다음, **추가**를 클릭합니다. 그러면 **\Views\Store\Details.cshtml** 파일이 생성 되 고 열립니다.

    ![세부 정보 보기 추가](aspnet-mvc-4-fundamentals/_static/image31.png "세부 정보 보기 추가")

    *세부 정보 보기 추가*
3. **세부** 정보를 수정 하 여 앨범 정보를 표시 하 고 보기 템플릿에 전달 된 **앨범** 개체에 액세스 합니다. 이렇게 하려면 콘텐츠를 다음으로 바꿉니다. (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample24.cshtml)]

<a id="Ex6Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a>작업 7-응용 프로그램 실행

이 작업에서는 details **작업** 메서드에서 앨범 정보를 검색 하는 **세부** 정보 보기를 테스트 합니다.

1. **F5** 키를 눌러 응용 프로그램을 실행 합니다.
2. 프로젝트가 **홈** 페이지에서 시작 됩니다. URL을 **/Store/Details/5** 로 변경 하 여 앨범 정보를 확인 합니다.

    ![앨범 탐색 세부 정보](aspnet-mvc-4-fundamentals/_static/image32.png "앨범 탐색 세부 정보")

    *탐색 앨범의 세부 정보*

<a id="Ex6Task8"></a>

<a id="Task_8_-_Adding_Links_Between_Pages"></a>
#### <a name="task-8---adding-links-between-pages"></a>작업 8-페이지 간 링크 추가

이 작업에서는 스토어 보기의 링크를 추가 하 여 모든 장르 이름에 적절 한 **/Sv/svhurl** 에 대 한 링크를 추가 합니다. 이러한 방식으로, 예를 들어, 장르를 클릭 하면 **disco**로 이동 하 여 **/Source= Disco** URL로 이동 합니다.

1. 필요한 경우 브라우저를 닫고 Visual Studio 창으로 돌아갑니다. **인덱스** 페이지를 업데이트 하 여 **찾아보기** 페이지에 링크를 추가 합니다. 이렇게 하려면 **솔루션 탐색기** 에서 **Views** 폴더를 확장 한 다음 **저장소** 폴더를 확장 하 고, **Index. cshtml** 페이지를 두 번 클릭 합니다.
2. 선택 된 장르를 나타내는 찾아보기 보기에 링크를 추가 합니다. 이렇게 하려면 **&lt;li&gt;** 태그에서 다음 강조 표시 된 코드를 바꿉니다. (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample25.cshtml)]

   > [!NOTE]
   > 또 다른 방법은 다음과 같은 코드를 사용 하 여 페이지에 직접 연결 하는 것입니다.
   > 
   > &lt;href =&quot;/svs\hhhhher? 장르 =@genreName&quot;&gt;@genreName&lt;/a&gt;
   > 
   > 이 방법이 작동 하지만 하드 코드 된 문자열에 따라 다릅니다. 나중에 컨트롤러의 이름을 바꾸는 경우에는이 명령을 수동으로 변경 해야 합니다. 더 나은 대안은 **HTML 도우미** 메서드를 사용 하는 것입니다. ASP.NET MVC에는 이러한 작업에 사용할 수 있는 HTML 도우미 메서드가 포함 되어 있습니다. Html.actionlink **()** 도우미 메서드를 사용 하면 **&gt;링크&lt;** html을 쉽게 빌드할 수 있으므로 url 경로가 적절 하 게 url로 인코딩됩니다.
   > 
   > Html.actionlink에는 여러 오버 로드가 있습니다. 이 연습에서는 다음 3 개의 매개 변수를 사용 하는 매개 변수를 사용 합니다.
   > 
   > 1. 장르 이름을 표시 하는 링크 텍스트
   > 2. 컨트롤러 작업 이름 (**찾아보기**)
   > 3. 이름 (**장르**) 및 값 (**장르 이름**)을 모두 지정 하는 경로 매개 변수 값

<a id="Ex6Task9"></a>

<a id="Task_9_-_Running_the_Application"></a>
#### <a name="task-9---running-the-application"></a>작업 9-응용 프로그램 실행

이 작업에서는 각 장르가 적절 한 **/Sv/svhurl** 에 대 한 링크와 함께 표시 되는지 테스트 합니다.

1. **F5** 키를 눌러 응용 프로그램을 실행 합니다.
2. 프로젝트가 홈 페이지에서 시작 됩니다. **/Store** 에 대 한 url을 변경 하 여 각 장르가 적절 한 **/sv/dvurl** 에 링크 되는지 확인 합니다.

    ![찾아보기 페이지로 이동 하는 링크를 사용 하 여 장르 검색](aspnet-mvc-4-fundamentals/_static/image33.png "찾아보기 페이지로 이동 하는 링크를 사용 하 여 장르 검색")

    *찾아보기 페이지로 이동 하는 링크를 사용 하 여 장르 검색*

<a id="Ex6Task10"></a>

<a id="Task_10_-_Using_Dynamic_ViewModel_Collection_to_Pass_Values"></a>
#### <a name="task-10---using-dynamic-viewmodel-collection-to-pass-values"></a>작업 10-동적 ViewModel 컬렉션을 사용 하 여 값 전달

이 태스크에서는 모델을 변경 하지 않고 컨트롤러와 뷰 간에 값을 전달 하는 간단 하 고 강력한 메서드를 학습 합니다. ASP.NET MVC 4는 &quot;ViewModel&quot;컬렉션을 제공 합니다 .이 컬렉션은 동적 값에 할당 하 고 컨트롤러 및 뷰 내에서 액세스할 수 있습니다.

이제 ViewBag 동적 컬렉션을 사용 하 여 컨트롤러에서 뷰로 &quot;**별표 표시 장르**&quot; 목록을 전달 합니다. 저장소 인덱스 보기는 **ViewModel** 에 액세스 하 고 정보를 표시 합니다.

1. 필요한 경우 브라우저를 닫고 Visual Studio 창으로 돌아갑니다. **StoreController.cs** 를 열고 **Index** 메서드를 수정 하 여 ViewModel 컬렉션에 별표 표시 장르 목록을 만듭니다.

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample26.cs)]

    > [!NOTE]
    > **Viewbag [&quot;별표 표시&quot;]** 구문을 사용 하 여 속성에 액세스할 수도 있습니다.
2. **별표 표시&quot;별&quot;** 아이콘이이 랩의 **Source\assets\images** 폴더에 포함 되어 있습니다. 응용 프로그램에 추가 하려면 아래와 같이 **Windows 탐색기** 창에서 Visual Web Developer Express의 **솔루션 탐색기** 로 해당 콘텐츠를 끌어 옵니다.

    ![솔루션에 별모양 이미지 추가](aspnet-mvc-4-fundamentals/_static/image34.png "솔루션에 별모양 이미지 추가")

    *솔루션에 별모양 이미지 추가*
3. **저장소/인덱스** 를 열고 내용을 수정 합니다. **Viewbag** 컬렉션에서 &quot;별표 표시&quot; 속성을 읽고 현재 장르 이름이 목록에 있는지 확인 합니다. 이 경우에는 장르 링크에 바로 별 아이콘이 표시 됩니다.
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample27.cshtml)]

<a id="Ex6Task11"></a>

<a id="Task_11_-_Running_the_Application"></a>
#### <a name="task-11---running-the-application"></a>작업 11-응용 프로그램 실행

이 작업에서는 별표 표시 장르에 별 아이콘이 표시 되는 것을 테스트 합니다.

1. **F5** 키를 눌러 응용 프로그램을 실행 합니다.
2. 프로젝트가 **홈** 페이지에서 시작 됩니다. URL을 **/Store** 로 변경 하 여 각 주요 장르에 준수 레이블이 있는지 확인 합니다.

    ![별표 표시 요소를 사용 하 여 장르 검색](aspnet-mvc-4-fundamentals/_static/image35.png "별표 표시 요소를 사용 하 여 장르 검색")

    *별표 표시 요소를 사용 하 여 장르 검색*

<a id="Exercise7"></a>

<a id="Exercise_7_A_lap_around_ASPNET_MVC_4_new_template"></a>
### <a name="exercise-7-a-lap-around-aspnet-mvc-4-new-template"></a>연습 7: ASP.NET MVC 4 새 템플릿 살펴보기

이 연습에서는 ASP.NET MVC 4 프로젝트 템플릿의 향상 된 기능을 살펴보고 새 템플릿의 가장 관련성이 높은 기능을 살펴봅니다.

<a id="Ex7Task1"></a>

<a id="Task_1_Exploring_the_ASPNET_MVC_4_Internet_Application_Template"></a>
#### <a name="task-1-exploring-the-aspnet-mvc-4-internet-application-template"></a>작업 1: ASP.NET MVC 4 인터넷 응용 프로그램 템플릿 탐색

1. 아직 열려 있지 않은 경우 시작 **VS Express for Web**
2. 파일을 선택 합니다. **| 새로 만들기 | 프로젝트** 메뉴 명령입니다. **새 프로젝트** 대화 상자에서 **시각적 개체 C#| 웹** 템플릿을 선택 하 고 **ASP.NET MVC 4 웹 응용 프로그램**을 선택 합니다. 프로젝트 **이름을** *MusicStore* 로 지정 하 고 **솔루션 이름을** *시작*으로 업데이트 한 다음 위치를 선택 하거나 기본값을 그대로 유지 하 고 **확인**을 클릭 합니다.

    ![새 ASP.NET MVC 4 프로젝트 만들기](aspnet-mvc-4-fundamentals/_static/image36.png "새 ASP.NET MVC 4 프로젝트 만들기")

    *새 ASP.NET MVC 4 프로젝트 만들기*
3. **새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **인터넷 응용 프로그램** 프로젝트 템플릿을 선택 하 고 **확인**을 클릭 합니다. 보기 엔진으로 Razor 또는 ASPX를 선택할 수 있습니다.

    ![새 ASP.NET MVC 4 인터넷 응용 프로그램 만들기](aspnet-mvc-4-fundamentals/_static/image37.png "새 ASP.NET MVC 4 인터넷 응용 프로그램 만들기")

    *새 ASP.NET MVC 4 인터넷 응용 프로그램 만들기*

    > [!NOTE]
    > Razor 구문는 ASP.NET MVC 3에서 도입 되었습니다. 이는 파일에 필요한 문자 및 키 입력 수를 최소화 하 여 빠르고 유체 코딩 워크플로를 사용 하도록 설정 하는 것입니다. Razor는 기존 C#/vb (또는 기타) 언어 기술을 활용 하 고 멋진 HTML 생성 워크플로를 활성화 하는 템플릿 태그 구문을 제공 합니다.
4. **F5** 키를 눌러 솔루션을 실행 하 고 갱신 된 템플릿을 확인 합니다. 다음 기능을 확인할 수 있습니다.

    1. **최신 스타일 템플릿**

        템플릿이 갱신 되어 최신 스타일을 제공 합니다.

        ![ASP.NET MVC 4 스타일 지정 템플릿](aspnet-mvc-4-fundamentals/_static/image38.png "ASP.NET MVC 4 스타일 지정 템플릿")

        *ASP.NET MVC 4 스타일 지정 템플릿*
    2. **적응 렌더링**

        브라우저 창의 크기를 조정 하 고 페이지 레이아웃이 새 창 크기에 동적으로 적응 하는 방식을 확인 합니다. 이러한 템플릿은 적응 렌더링 기술을 사용 하 여 사용자 지정 없이 데스크톱과 모바일 플랫폼 모두에서 적절히 렌더링 합니다.

        ![다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿](aspnet-mvc-4-fundamentals/_static/image39.png "다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿")

        *다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿*
5. 디버거를 중지 하 고 Visual Studio로 돌아가려면 브라우저를 닫습니다.
6. 이제 솔루션을 탐색 하 고 프로젝트 템플릿에서 ASP.NET MVC 4에서 도입 된 새로운 기능 중 일부를 확인할 수 있습니다.

    ![ASP.NET (MVC4)-프로젝트 템플릿](aspnet-mvc-4-fundamentals/_static/image40.png "ASP.NET MVC 4 인터넷 응용 프로그램 프로젝트 템플릿")

    *ASP.NET MVC 4 인터넷 응용 프로그램 프로젝트 템플릿*

   1. **HTML5 태그**

       템플릿 뷰를 탐색 하 여 새 테마 태그를 찾습니다. 예를 들어 **Home** 폴더 내에서 열기 **About. cshtml** 보기를 찾습니다.

       ![새 템플릿, Razor 및 HTML5 태그 사용](aspnet-mvc-4-fundamentals/_static/image41.png "새 템플릿, Razor 및 HTML5 태그 사용")

       *새 템플릿, Razor 및 HTML5 태그 사용*
   2. **포함 된 JavaScript 라이브러리**

      1. **jquery**: JQUERY는 HTML 문서 트래버스, 이벤트 처리, 애니메이션 및 Ajax 상호 작용을 간소화 합니다.
      2. **JQUERY UI**:이 라이브러리는 Jquery JavaScript 라이브러리를 기반으로 구축 된 낮은 수준의 상호 작용 및 애니메이션, 고급 효과 및 themeable 위젯에 대 한 추상화를 제공 합니다.

         > [!NOTE]
         > [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/)에서 jQuery 및 jquery UI에 대해 알아볼 수 있습니다.
      3. **KnockoutJS**: ASP.NET MVC 4 기본 템플릿에는 JAVASCRIPT 및 HTML을 사용 하 여 풍부 하 고 응답성이 뛰어난 웹 응용 프로그램을 만들 수 있는 javascript MVVM 프레임 워크인 **KnockoutJS**가 포함 되어 있습니다. ASP.NET MVC 3의 경우와 마찬가지로 jQuery 및 jQuery UI 라이브러리도 ASP.NET MVC 4에 포함 되어 있습니다.

          > [!NOTE]
          > 이 링크에서 KnockOutJS library에 대 한 자세한 내용은 [http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)를 확인 하세요.
      4. **Modernizr**:이 라이브러리는 HTML5 및 CSS3 기술을 사용 하는 경우 사이트가 이전 브라우저와 호환 되도록 자동으로 실행 됩니다.

          > [!NOTE]
          > 이 링크에서 Modernizr library에 대 한 자세한 내용은 [http://www.modernizr.com/](http://www.modernizr.com/)를 확인 하세요.
   3. **솔루션에 포함 된 SimpleMembership**

       SimpleMembership는 이전 ASP.NET 역할 및 멤버 자격 공급자 시스템에 대 한 대체로 설계 되었습니다. 개발자가 보다 유연 하 게 웹 페이지를 보다 쉽게 보호할 수 있도록 하는 여러 가지 새로운 기능이 포함 되어 있습니다.

       인터넷 템플릿에서 SimpleMembership를 통합 하기 위한 몇 가지 작업을 이미 설정 했습니다. 예를 들어 AccountController는 OAuthWebSecurity (OAuth 계정 등록, 로그인, 관리 등) 및 웹 보안을 사용할 준비를 합니다.

       ![솔루션에 포함 된 SimpleMembership](aspnet-mvc-4-fundamentals/_static/image42.png "솔루션에 포함 된 SimpleMembership")

       *솔루션에 포함 된 SimpleMembership*

       > [!NOTE]
       > MSDN의 [Oauthwebsecurity](https://msdn.microsoft.com/library/jj158393(v=vs.111).aspx) 에 대 한 자세한 내용을 확인 하세요.

> [!NOTE]
> 또한 [부록 B: 웹 배포을 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시](#AppendixB)를 수행 하는 Windows Azure 웹 사이트에이 응용 프로그램을 배포할 수 있습니다.

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습 실습을 완료 하면 ASP.NET MVC의 기본 사항에 대해 알아보았습니다.

- MVC 응용 프로그램의 핵심 요소 및 상호 작용 방법
- ASP.NET MVC 응용 프로그램을 만드는 방법
- URL 및 querystring을 통해 전달 되는 매개 변수를 처리 하는 컨트롤러를 추가 및 구성 하는 방법
- 일반 HTML 콘텐츠에 대 한 템플릿을 설정 하는 레이아웃 마스터 페이지를 추가 하는 방법, 모양과 느낌을 개선 하는 스타일 시트 및 HTML 콘텐츠를 표시 하는 보기 템플릿
- 동적 정보를 표시 하기 위해 뷰 템플릿에 속성을 전달 하는 데 ViewModel 패턴을 사용 하는 방법
- 뷰 템플릿에서 컨트롤러에 전달 된 매개 변수를 사용 하는 방법
- ASP.NET MVC 응용 프로그램 내 페이지에 대 한 링크를 추가 하는 방법
- 뷰에서 동적 속성을 추가 하 고 사용 하는 방법
- ASP.NET MVC 4 프로젝트 템플릿의 향상 된 기능

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>부록 A: 웹에 대 한 Visual Studio Express 2012 설치

**[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)** 를 사용 하 여 웹 또는 다른 &quot;Express&quot; 버전 **에 대해 Microsoft Visual Studio Express 2012** 를 설치할 수 있습니다. 다음 지침에서는 *Microsoft 웹 플랫폼 설치 관리자*를 사용 하 여 *Visual studio Express 2012 for Web* 을 설치 하는 데 필요한 단계를 안내 합니다.

1. [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)로 이동 합니다. 또는 웹 플랫폼 설치 관리자를 이미 설치한 경우에는 웹 플랫폼 설치 관리자를 열고 <em>Microsoft AZURE SDK&quot;를 사용 하 여 웹 용 2012 Visual Studio Express</em> &quot;제품을 검색할 수 있습니다.
2. **지금 설치**를 클릭 합니다. **웹 플랫폼 설치 관리자** 가 없으면 먼저이를 다운로드 하 여 설치 하도록 리디렉션됩니다.
3. **웹 플랫폼 설치 관리자** 가 열리면 **설치** 를 클릭 하 여 설치를 시작 합니다.

    ![Visual Studio Express 설치](aspnet-mvc-4-fundamentals/_static/image43.png "Visual Studio Express 설치")

    *Visual Studio Express 설치*
4. 모든 제품의 라이선스 및 사용 조건을 읽고 **동의** 함을 클릭 하 여 계속 합니다.

    ![사용 조건 동의](aspnet-mvc-4-fundamentals/_static/image44.png)

    *사용 조건 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](aspnet-mvc-4-fundamentals/_static/image45.png)

    *설치 진행률*
6. 설치가 완료 되 면 **마침**을 클릭 합니다.

    ![설치 완료](aspnet-mvc-4-fundamentals/_static/image46.png)

    *설치 완료*
7. **끝내기** 를 클릭 하 여 웹 플랫폼 설치 관리자를 닫습니다.
8. 웹에 대 한 Visual Studio Express를 열려면 **시작** 화면으로 이동 하 &quot;**VS Express**&quot;작성을 시작한 후 **VS Express for Web** 타일을 클릭 합니다.

    ![VS Express for Web 타일](aspnet-mvc-4-fundamentals/_static/image47.png)

    *VS Express for Web 타일*

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>부록 B: 웹 배포을 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시

이 부록에서는 windows azure 관리 포털에서 새 웹 사이트를 만들고 랩에 따라 가져온 응용 프로그램을 게시 하 여 Windows Azure에서 제공 하는 웹 배포 게시 기능을 활용 하는 방법을 보여 줍니다.

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a>작업 1-Windows Azure 포털에서 새 웹 사이트 만들기

1. [Windows Azure 관리 포털](https://manage.windowsazure.com/) 로 이동 하 고 구독과 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.

    > [!NOTE]
    > Windows Azure를 사용 하면 10 개의 ASP.NET 웹 사이트를 무료로 호스팅한 후 트래픽 증가에 따라 크기를 조정할 수 있습니다. [여기](https://aka.ms/aspnet-hol-azure)에서 등록할 수 있습니다.

    ![Windows Azure Portal에 로그온 합니다.](aspnet-mvc-4-fundamentals/_static/image48.png "Windows Azure Portal에 로그온 합니다.")

    *Windows Azure 관리 포털에 로그온 합니다.*
2. 명령 모음에서 **새로 만들기** 를 클릭 합니다.

    ![새 웹 사이트 만들기](aspnet-mvc-4-fundamentals/_static/image49.png "새 웹 사이트 만들기")

    *새 웹 사이트 만들기*
3. **Compute** | **웹 사이트**를 클릭 합니다. 그런 다음 **빠른 생성** 옵션을 선택 합니다. 새 웹 사이트에 사용할 수 있는 URL을 제공 하 고 **웹 사이트 만들기**를 클릭 합니다.

    > [!NOTE]
    > Microsoft Azure 웹 사이트는 사용자가 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램에 대 한 호스트입니다. 빠른 생성 옵션을 사용 하면 포털 외부에서 Windows Azure 웹 사이트에 완료 된 웹 응용 프로그램을 배포할 수 있습니다. 데이터베이스를 설정 하는 단계는 포함 되지 않습니다.

    ![빠른 생성을 사용 하 여 새 웹 사이트 만들기](aspnet-mvc-4-fundamentals/_static/image50.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")

    *빠른 생성을 사용 하 여 새 웹 사이트 만들기*
4. 새 **웹 사이트가** 만들어질 때까지 기다립니다.
5. 웹 사이트를 만든 후 **URL** 열 아래의 링크를 클릭 합니다. 새 웹 사이트가 작동 하는지 확인 합니다.

    ![새 웹 사이트로 이동](aspnet-mvc-4-fundamentals/_static/image51.png "새 웹 사이트로 이동")

    *새 웹 사이트로 이동*

    ![웹 사이트 실행 중](aspnet-mvc-4-fundamentals/_static/image52.png "웹 사이트 실행 중")

    *웹 사이트 실행 중*
6. 포털로 돌아가서 **이름** 열 아래에 있는 웹 사이트의 이름을 클릭 하 여 관리 페이지를 표시 합니다.

    ![웹 사이트 관리 페이지 열기](aspnet-mvc-4-fundamentals/_static/image53.png "웹 사이트 관리 페이지 열기")

    *웹 사이트 관리 페이지 열기*
7. **대시보드** 페이지의 **빠른** 보기 섹션에서 **게시 프로필 다운로드** 링크를 클릭 합니다.

    > [!NOTE]
    > *게시 프로필* 에는 사용 하도록 설정 된 각 게시 방법에 대해 웹 응용 프로그램을 Windows Azure 웹 사이트에 게시 하는 데 필요한 모든 정보가 포함 되어 있습니다. 게시 프로필에는 게시 방법이 사용 설정된 각 엔드포인트에 연결하고 이에 대해 인증하는 데 필요한 URL, 사용자 자격 증명 및 데이터베이스 문자열이 포함되어 있습니다. **Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** 및 **Microsoft Visual Studio 2012** 는 게시 프로필 읽기를 지원 하 여 웹 응용 프로그램을 Windows Azure 웹 사이트에 게시 하기 위해 이러한 프로그램의 구성을 자동화 합니다.

    ![웹 사이트 게시 프로필을 다운로드 하는 중](aspnet-mvc-4-fundamentals/_static/image54.png "웹 사이트 게시 프로필을 다운로드 하는 중")

    *웹 사이트 게시 프로필을 다운로드 하는 중*
8. 알려진 위치에 게시 프로필 파일을 다운로드 합니다. 이 연습을 통해이 파일을 사용 하 여 Visual Studio에서 Windows Azure 웹 사이트에 웹 응용 프로그램을 게시 하는 방법을 확인할 수 있습니다.

    ![게시 프로필 파일을 저장 하는 중](aspnet-mvc-4-fundamentals/_static/image55.png "게시 프로필을 저장 하는 중")

    *게시 프로필 파일을 저장 하는 중*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>작업 2-데이터베이스 서버 구성

응용 프로그램에서 SQL Server 데이터베이스를 사용 하는 경우 SQL Database 서버를 만들어야 합니다. SQL Server 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 작업을 건너뛸 수 있습니다.

1. 응용 프로그램 데이터베이스를 저장 하기 위한 SQL Database 서버가 필요 합니다. Microsoft Azure 관리 포털의 구독에서 SQL Database 서버를 볼 수는 **SQL 데이터베이스** | **서버** | **서버의 대시보드**. 만든 서버가 없는 경우 명령 모음에서 **추가** 단추를 사용 하 여 만들 수 있습니다. 다음 작업에서 사용할 **서버 이름과 URL, 관리자 로그인 이름 및 암호**를 기록해 둡니다. 이후 단계에서 생성 되므로 아직 데이터베이스를 만들지 마십시오.

    ![SQL Database 서버 대시보드](aspnet-mvc-4-fundamentals/_static/image56.png "SQL Database 서버 대시보드")

    *SQL Database 서버 대시보드*
2. 다음 작업에서는 Visual Studio에서 데이터베이스 연결을 테스트 합니다. 따라서 서버에서 **허용 되는 Ip 주소**목록에 로컬 IP 주소를 포함 해야 합니다. 이렇게 하려면 **구성**을 클릭 하 고, **현재 클라이언트 IP 주소** 에서 ip 주소를 선택 하 고, **시작 Ip 주소** 및 **끝 ip 주소** 텍스트 상자에 붙여 넣고, ![추가-클라이언트-ip 주소-확인 단추](aspnet-mvc-4-fundamentals/_static/image57.png) 단추를 클릭 합니다.

    ![클라이언트 IP 주소를 추가 하는 중](aspnet-mvc-4-fundamentals/_static/image58.png)

    *클라이언트 IP 주소를 추가 하는 중*
3. **클라이언트 Ip 주소가** 허용 된 ip 주소 목록에 추가 되 면 **저장** 을 클릭 하 여 변경 내용을 확인 합니다.

    ![변경 내용 확인](aspnet-mvc-4-fundamentals/_static/image59.png)

    *변경 내용 확인*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시

1. ASP.NET MVC 4 솔루션으로 돌아갑니다. **솔루션 탐색기**에서 웹 사이트 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 선택 합니다.

    ![응용 프로그램 게시](aspnet-mvc-4-fundamentals/_static/image60.png "응용 프로그램 게시")

    *웹 사이트 게시*
2. 첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.

    ![게시 프로필을 가져오는 중](aspnet-mvc-4-fundamentals/_static/image61.png "게시 프로필을 가져오는 중")

    *게시 프로필을 가져오는 중*
3. **연결 유효성 검사**를 클릭 합니다. 유효성 검사가 완료 되 면 **다음**을 클릭 합니다.

    > [!NOTE]
    > 유효성 검사는 연결 유효성 검사 단추 옆에 녹색 확인 표시가 표시 되 면 완료 됩니다.

    ![연결 유효성 검사](aspnet-mvc-4-fundamentals/_static/image62.png "연결 유효성 검사")

    *연결 유효성 검사*
4. **설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆에 있는 단추 (즉, **defaultconnection**)를 클릭 합니다.

    ![웹 배포 구성](aspnet-mvc-4-fundamentals/_static/image63.png "웹 배포 구성")

    *웹 배포 구성*
5. 데이터베이스 연결을 다음과 같이 구성 합니다.

   - **서버 이름** 에 *tcp:* 접두사를 사용 하 여 SQL Database 서버 URL을 입력 합니다.
   - **사용자 이름** 에 서버 관리자 로그인 이름을 입력 합니다.
   - **암호** 에 서버 관리자 로그인 암호를 입력 합니다.
   - 새 데이터베이스 이름 (예: *MVC4SampleDB*)을 입력 합니다.

     ![대상 연결 문자열 구성](aspnet-mvc-4-fundamentals/_static/image64.png "대상 연결 문자열 구성")

     *대상 연결 문자열 구성*
6. 그런 후 **OK**를 클릭합니다. 데이터베이스를 만들 것인지 묻는 메시지가 표시 되 면 **예**를 클릭 합니다.

    ![데이터베이스 만들기](aspnet-mvc-4-fundamentals/_static/image65.png "데이터베이스 문자열 만들기")

    *데이터베이스 만들기*
7. Windows Azure에서 SQL Database에 연결 하는 데 사용할 연결 문자열은 기본 연결 텍스트 상자 내에 표시 됩니다. 그런 후 **Next** 를 클릭합니다.

    ![SQL Database를 가리키는 연결 문자열](aspnet-mvc-4-fundamentals/_static/image66.png "SQL Database를 가리키는 연결 문자열")

    *SQL Database를 가리키는 연결 문자열*
8. **미리 보기** 페이지에서 **게시**를 클릭 합니다.

    ![웹 응용 프로그램 게시](aspnet-mvc-4-fundamentals/_static/image67.png "웹 응용 프로그램 게시")

    *웹 응용 프로그램 게시*
9. 게시 프로세스가 완료 되 면 기본 브라우저가 게시 된 웹 사이트를 엽니다.

    ![Windows Azure에 게시 된 응용 프로그램](aspnet-mvc-4-fundamentals/_static/image68.png "Windows Azure에 게시 된 응용 프로그램")

    *Windows Azure에 게시 된 응용 프로그램*

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>부록 C: 코드 조각 사용

코드 조각을 사용 하면 필요한 모든 코드를 편리 하 게 사용할 수 있습니다. 랩 문서는 다음 그림에 표시 된 것 처럼 사용자가 사용할 수 있는 경우를 정확 하 게 알려줍니다.

![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입](aspnet-mvc-4-fundamentals/_static/image69.png "Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입")

*Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입*

***키보드를 사용 하 여 코드 조각을 추가 하려면C# (만 해당)***

1. 코드를 삽입할 위치에 커서를 놓습니다.
2. 조각 이름 (공백 또는 하이픈 제외)을 입력 하기 시작 합니다.
3. IntelliSense는 일치 하는 코드 조각의 이름을 표시 합니다.
4. 올바른 코드 조각을 선택 하거나 전체 코드 조각 이름이 선택 될 때까지 계속 입력 합니다.
5. Tab 키를 두 번 눌러 커서 위치에 코드 조각을 삽입 합니다.

![코드 조각 이름 입력 시작](aspnet-mvc-4-fundamentals/_static/image70.png "코드 조각 이름 입력 시작")

*코드 조각 이름 입력 시작*

![Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.](aspnet-mvc-4-fundamentals/_static/image71.png "Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.")

*Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.*

![Tab 키를 다시 누르면 코드 조각이 확장 됩니다.](aspnet-mvc-4-fundamentals/_static/image72.png "Tab 키를 다시 누르면 코드 조각이 확장 됩니다.")

*Tab 키를 다시 누르면 코드 조각이 확장 됩니다.*

***마우스C#(, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면*** 1(sp1). 코드 조각을 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭 합니다.

1. 코드 **조각 삽입** 을 선택한 다음 **내 코드 조각을**선택 합니다.
2. 목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.

![코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.](aspnet-mvc-4-fundamentals/_static/image73.png "코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.")

*코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.*

![목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.](aspnet-mvc-4-fundamentals/_static/image74.png "목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.")

*목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.*
