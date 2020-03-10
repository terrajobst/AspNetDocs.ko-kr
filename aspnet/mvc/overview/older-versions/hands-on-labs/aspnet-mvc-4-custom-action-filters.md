---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
title: ASP.NET MVC 4 사용자 지정 작업 필터 | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC는 작업 메서드를 호출 하기 전이나 후에 필터링 논리를 실행 하기 위한 작업 필터를 제공 합니다. 작업 필터는 사용자 지정 특성 tha
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 969ab824-1b98-4552-81fe-b60ef5fc6887
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
msc.type: authoredcontent
ms.openlocfilehash: eaeb32180f79fabf557cbc38ff067eb26b47fea7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468179"
---
# <a name="aspnet-mvc-4-custom-action-filters"></a>ASP.NET MVC 4 사용자 지정 작업 필터

[웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 교육 키트 다운로드](https://aka.ms/webcamps-training-kit)

ASP.NET MVC는 작업 메서드를 호출 하기 전이나 후에 필터링 논리를 실행 하기 위한 작업 필터를 제공 합니다. 작업 필터는 사전 작업 및 작업 후 동작을 컨트롤러의 작업 메서드에 추가 하는 선언적 방법을 제공 하는 사용자 지정 특성입니다.

이 실습 랩에서는 MvcMusicStore 솔루션에 사용자 지정 작업 필터 특성을 만들어 컨트롤러의 요청을 catch 하 고 사이트의 활동을 데이터베이스 테이블에 기록 합니다. 모든 컨트롤러 또는 작업에 대 한 삽입으로 로깅 필터를 추가할 수 있습니다. 마지막으로 방문자 목록을 표시 하는 로그 보기가 표시 됩니다.

이 실습 랩에서는 **ASP.NET MVC**에 대 한 기본 지식이 있다고 가정 합니다. 이전에 **ASP.NET mvc** 를 사용 하지 않은 경우 **ASP.NET mvc 4 기본** 실습 실습을 사용 하는 것이 좋습니다.

> [!NOTE]
> 모든 샘플 코드와 코드 조각은 [Microsoft 웹/WebCampTrainingKit 릴리스에서](https://aka.ms/webcamps-training-kit)제공 되는 웹 캠프 교육 키트에 포함 되어 있습니다. 이 랩에서 관련 된 프로젝트는 [ASP.NET MVC 4 사용자 지정 작업 필터](https://github.com/Microsoft-Web/HOL-MVC4CustomActionFilters)에서 사용할 수 있습니다.

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서는 다음 방법에 대해 알아봅니다.

- 사용자 지정 작업 필터 특성을 만들어 필터링 기능 확장
- 특정 수준에 주입 별 사용자 지정 필터 특성 적용
- 사용자 지정 작업 필터를 전역적으로 등록

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>사전 요구 사항

이 랩을 완료 하려면 다음 항목이 있어야 합니다.

- [웹 또는 고급의 경우 2012 Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (설치 방법에 대 한 지침은 [부록 a를](#AppendixA) 참조 하세요.)

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>설치 프로그램

**코드 조각 설치**

편의를 위해이 랩에서 관리 하는 대부분의 코드는 Visual Studio 코드 조각으로 사용할 수 있습니다. 코드 조각을 설치 하려면 **.\Source\Setup\CodeSnippets.vsi** 파일을 실행 합니다.

Visual Studio Code 코드 조각에 대해 잘 모르는 경우이를 사용 하는 방법을 알아보려면이 문서의 부록 [C: 코드 조각&quot;사용](#AppendixC) &quot;부록을 참조할 수 있습니다.

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>실습

이 실습 랩은 다음 연습으로 구성 됩니다.

1. [연습 1: 로깅 작업](#Exercise1)
2. [연습 2: 여러 작업 필터 관리](#Exercise2)

이 랩을 완료 하는 데 소요 되는 예상 시간: **30 분**

> [!NOTE]
> 각 연습에는 연습을 완료 한 후 얻게 되는 결과 솔루션을 포함 하는 **끝** 폴더가 함께 제공 됩니다. 연습을 진행 하는 데 도움이 필요한 경우이 솔루션을 지침으로 사용할 수 있습니다.

<a id="Exercise1"></a>

<a id="Exercise_1_Logging_Actions"></a>
### <a name="exercise-1-logging-actions"></a>연습 1: 로깅 작업

이 연습에서는 ASP.NET MVC 4 필터 공급자를 사용 하 여 사용자 지정 작업 로그 필터를 만드는 방법에 대해 설명 합니다. 이렇게 하려면 선택한 컨트롤러의 모든 활동을 기록 하는 로깅 필터를 MusicStore 사이트에 적용 합니다.

이 필터는 **Actionfilterattributeclass** 를 확장 하 고 **onactionexecuting** 메서드를 재정의 하 여 각 요청을 catch 한 다음 로깅 동작을 수행 합니다. HTTP 요청, 실행 메서드, 결과 및 매개 변수에 대 한 컨텍스트 정보는 ASP.NET MVC **ActionExecutingContext** 클래스에서 제공 됩니다 **.**

> [!NOTE]
> ASP.NET MVC 4에는 사용자 지정 필터를 만들지 않고 사용할 수 있는 기본 필터 공급자도 있습니다. ASP.NET MVC 4는 다음과 같은 유형의 필터를 제공 합니다.
> 
> - **권한 부여** 필터-인증 수행 또는 요청 속성의 유효성 검사 등의 동작 메서드 실행 여부에 대 한 보안 결정을 내립니다.
> - **작업 필터-** 작업 메서드 실행을 래핑합니다. 이 필터는 작업 메서드에 추가 데이터를 제공 하거나 반환 값을 검사 하거나 작업 메서드의 실행을 취소 하는 등의 추가 처리 작업을 수행할 수 있습니다.
> - **결과** 필터-actionresult 개체의 실행을 래핑합니다. 이 필터는 HTTP 응답 수정과 같은 결과의 추가 처리를 수행할 수 있습니다.
> - **예외** 필터-권한 부여 필터부터 시작 하 여 결과 실행으로 끝나는 동작 메서드에서 처리 되지 않은 예외가 throw 되는 경우에 실행 됩니다. 예외 필터는 로깅 또는 오류 페이지 표시 등의 작업에 사용될 수 있습니다.
> 
> 필터 공급자에 대 한 자세한 내용은 MSDN 링크 ([https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx))를 참조 하세요.

<a id="AboutLoggingFeature"></a>

<a id="About_MVC_Music_Store_Application_logging_feature"></a>
#### <a name="about-mvc-music-store-application-logging-feature"></a>MVC Music Store 응용 프로그램 로깅 기능 정보

이 Music Store 솔루션에는 사이트 로깅, **Actionlog**에 대 한 새 데이터 모델 테이블이 있습니다 .이 테이블에는 요청을 수신 하는 컨트롤러의 이름 (작업, 클라이언트 IP 및 타임 스탬프) 필드가 있습니다.

![데이터 모델. ActionLog 테이블입니다.](aspnet-mvc-4-custom-action-filters/_static/image1.png "데이터 모델. ActionLog 테이블입니다.")

*데이터 모델-ActionLog 테이블*

이 솔루션은 **MvcMusicStores/Views/ActionLog**에서 찾을 수 있는 작업 로그에 대 한 ASP.NET MVC 뷰를 제공 합니다.

![작업 로그 보기](aspnet-mvc-4-custom-action-filters/_static/image2.png "작업 로그 보기")

*작업 로그 보기*

이 지정 된 구조를 사용 하 여 모든 작업은 컨트롤러의 요청을 중단 하 고 사용자 지정 필터링을 사용 하 여 로깅을 수행 하는 데 집중 됩니다.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_Custom_Filter_to_Catch_a_Controllers_Request"></a>
#### <a name="task-1---creating-a-custom-filter-to-catch-a-controllers-request"></a>작업 1-컨트롤러의 요청을 Catch 하는 사용자 지정 필터 만들기

이 작업에서는 로깅 논리를 포함 하는 사용자 지정 필터 특성 클래스를 만듭니다. 이 목적을 위해 ASP.NET MVC **Actionfilterattribute** 클래스를 확장 하 고 **iactionfilter**인터페이스를 구현 합니다.

> [!NOTE]
> **Actionfilterattribute** 는 모든 특성 필터에 대 한 기본 클래스입니다. 이 클래스는 다음 메서드를 제공 하 여 컨트롤러 작업의 실행 전후에 특정 논리를 실행 합니다.
> 
> - **Onactionexecuting**(ActionExecutingContext filtercontext): 동작 메서드가 호출 되기 직전입니다.
> - **Onactionexecuted**됨 (actionexecutedcontext filtercontext): 동작 메서드가 호출 되 고 결과가 실행 되기 전에 (뷰 렌더링 전)
> - **Onresultexecuting**(ResultExecutingContext filtercontext): 결과가 실행 되기 직전 (뷰 렌더링 전).
> - **Onresultexecuted**(resultexecutedcontext filtercontext): 뷰가 렌더링 된 후 결과가 실행 된 후
> 
> 이러한 메서드를 파생 클래스로 재정의 하 여 사용자 고유의 필터링 코드를 실행할 수 있습니다.

1. **\Source\Ex01-LoggingActions\Begin** 폴더에 있는 **시작** 솔루션을 엽니다.

   1. 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.
   2. **NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.
   3. 마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.

      > [!NOTE]
      > NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다. NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다. 이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.
      > 
      > 자세한 내용은 [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)문서를 참조 하세요.
2. Filters 폴더에 C# 새 클래스를 추가 하 고 이름을 *CustomActionFilter.cs*로 만듭니다. 이 폴더에는 모든 사용자 지정 필터가 저장 됩니다.
3. **CustomActionFilter.cs** 및 **MvcMusicStore** 네임 **스페이스에 대** 한 참조를 추가 합니다.

    (코드 조각- *ASP.NET MVC 4 사용자 지정 작업 필터-Ex1-CustomActionFilterNamespaces*)

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample1.cs)]
4. **Actionfilterattribute** 에서 **CustomActionFilter** 클래스를 상속한 다음 **CustomActionFilter** 클래스가 **iactionfilter** 인터페이스를 구현 하도록 합니다.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample2.cs)]
5. **CustomActionFilter** 클래스가 **onactionexecuting** 메서드를 재정의 하 고 필터 실행을 기록 하는 데 필요한 논리를 추가 합니다. 이렇게 하려면 **CustomActionFilter** 클래스 내에서 다음 강조 표시 된 코드를 추가 합니다.

    (코드 조각- *ASP.NET MVC 4 사용자 지정 작업 필터-Ex1-LoggingActions*)

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample3.cs#Highlight)]

    > [!NOTE]
    > **Onactionexecuting** 메서드는 **Entity Framework** 을 사용 하 여 새 actionlog 레지스터를 추가 합니다. **Filtercontext**의 컨텍스트 정보를 사용 하 여 새 엔터티 인스턴스를 만들고 채웁니다.
    > 
    > **Controllercontext** 클래스에 대 한 자세한 내용은 [msdn](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx)에서 읽을 수 있습니다.

<a id="Ex1Task2"></a>

<a id="Task_2_-_Injecting_a_Code_Interceptor_into_the_Store_Controller_Class"></a>
#### <a name="task-2---injecting-a-code-interceptor-into-the-store-controller-class"></a>작업 2-저장소 컨트롤러 클래스에 코드 인터셉터 삽입

이 태스크에서는 사용자 지정 필터를 기록 하는 모든 컨트롤러 클래스 및 컨트롤러 작업에 삽입 하 여 해당 필터를 추가 합니다. 이 연습에서는 저장소 컨트롤러 클래스에 로그가 포함 됩니다.

**Actionlogfilterattribute** 사용자 지정 필터에서 **onactionexecuting** 메서드는 삽입 된 요소가 호출 될 때 실행 됩니다.

특정 컨트롤러 메서드를 가로챌 수도 있습니다.

1. **StoreController** 에서 **MvcMusicStore\Controllers** 를 열고 **필터** 네임 스페이스에 대 한 참조를 추가 합니다.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample4.cs)]
2. 클래스 선언 앞에 **[CustomActionFilter]** 특성을 추가 하 여 사용자 지정 필터 **CustomActionFilter** 에 **StoreController** 클래스를 삽입 합니다.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample5.cs)]

   > [!NOTE]
   > 필터가 컨트롤러 클래스에 삽입 되 면 모든 작업도 삽입 됩니다. 작업 집합에 대해서만 필터를 적용 하려면 각 항목에 **[CustomActionFilter]** 을 삽입 해야 합니다.
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample6.cs)]

<a id="Ex1Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>작업 3-응용 프로그램 실행

이 작업에서 로깅 필터가 작동 하는지 테스트 합니다. 응용 프로그램을 시작 하 고 스토어를 방문 하 고 기록 된 작업을 확인 합니다.

1. **F5** 키를 눌러 애플리케이션을 실행합니다.
2. **/Clog** 로 이동 하 여 로그 뷰 초기 상태를 확인 합니다.

    ![페이지 작업 전 로그 추적기 상태](aspnet-mvc-4-custom-action-filters/_static/image3.png "페이지 작업 전 로그 추적기 상태")

    *페이지 작업 전 로그 추적기 상태*

   > [!NOTE]
   > 기본적으로 메뉴에 대 한 기존 장르를 검색할 때 생성 되는 하나의 항목이 항상 표시 됩니다.
   > 
   > 간단 하 게 하기 위해 응용 프로그램이 실행 될 때마다 **Actionlog** 테이블을 정리 하므로 각 특정 작업의 확인에 대 한 로그만 표시 됩니다.
   > 
   > 저장소 컨트롤러 내에서 실행 되는 모든 작업에 대 한 기록 로그를 저장 하려면 **Session\_Start** 메서드 ( **global.asax 클래스)** 에서 다음 코드를 제거 해야 할 수 있습니다.
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample7.cs)]
3. 메뉴에서 **장르** 중 하나를 클릭 하 고 사용 가능한 앨범 탐색과 같은 몇 가지 작업을 수행 합니다.
4. **/Actionlog** 로 이동 하 여 로그가 비어 있으면 **F5** 키를 눌러 페이지를 새로 고칩니다. 방문이 추적 되었는지 확인 합니다.

    ![작업이 기록 된 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image4.png "작업이 기록 된 작업 로그")

    *작업이 기록 된 작업 로그*

<a id="Exercise2"></a>

<a id="Exercise_2_Managing_Multiple_Action_Filters"></a>
### <a name="exercise-2-managing-multiple-action-filters"></a>연습 2: 여러 작업 필터 관리

이 연습에서는 StoreController 클래스에 두 번째 사용자 지정 작업 필터를 추가 하 고 두 필터를 실행할 특정 순서를 정의 합니다. 그런 다음 코드를 업데이트 하 여 전역으로 필터를 등록 합니다.

필터 실행 순서를 정의할 때 고려할 다른 옵션이 있습니다. 예를 들어 Order 속성 및 필터 범위는 다음과 같습니다.

각 필터의 **범위** 를 정의할 수 있습니다. 예를 들어 **컨트롤러 범위**내에서 실행 되는 모든 작업 필터의 범위를 지정 하 고 모든 권한 부여 필터를 **전역 범위**에서 실행할 수 있습니다. 범위는 실행 순서를 정의 합니다.

또한 각 작업 필터에는 필터 범위에서 실행 순서를 결정 하는 데 사용 되는 Order 속성이 있습니다.

사용자 지정 작업 필터 실행 순서에 대 한 자세한 내용은 MSDN 문서 ([https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx))를 참조 하세요.

<a id="Ex2Task1"></a>

<a id="Task_1_Creating_a_new_Custom_Action_Filter"></a>
#### <a name="task-1-creating-a-new-custom-action-filter"></a>작업 1: 새 사용자 지정 작업 필터 만들기

이 작업에서는 StoreController 클래스에 삽입할 새 사용자 지정 작업 필터를 만들어 필터 실행 순서를 관리 하는 방법을 배웁니다.

1. **\Source\Ex02-ManagingMultipleActionFilters\Begin** 폴더에 있는 **시작** 솔루션을 엽니다. 그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.

    1. 제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.
    2. **NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.
    3. 마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.

        > [!NOTE]
        > NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다. NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다. 이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.
        > 
        > 자세한 내용은 [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)문서를 참조 하세요.
2. Filters 폴더에 C# 새 클래스를 추가 하 고 이름을 *MyNewCustomActionFilter.cs* 로 추가 합니다.
3. **MyNewCustomActionFilter.cs** 을 열고 **system.web** 및 **MvcMusicStore** 네임 스페이스에 대 한 참조를 추가 합니다.

    (코드 조각- *ASP.NET MVC 4 사용자 지정 작업 필터-Ex2-MyNewCustomActionFilterNamespaces*)

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample8.cs)]
4. 기본 클래스 선언을 다음 코드로 바꿉니다.

    (코드 조각- *ASP.NET MVC 4 사용자 지정 작업 필터-Ex2-MyNewCustomActionFilterClass*)

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample9.cs)]

    > [!NOTE]
    > 이 사용자 지정 작업 필터는 이전 연습에서 만든 것과 거의 동일 합니다. 주요 차이점은 로그에 등록 된 필터를 식별 하기 위해이 새 클래스의 이름을 사용 하 여&quot;특성을 업데이트 *한&quot;* 를 포함 한다는 것입니다.

<a id="Ex2Task2"></a>

<a id="Task_2_Injecting_a_new_Code_Interceptor_into_the_StoreController_Class"></a>
#### <a name="task-2-injecting-a-new-code-interceptor-into-the-storecontroller-class"></a>작업 2: StoreController 클래스에 새 코드 인터셉터 삽입

이 작업에서는 StoreController 클래스에 새 사용자 지정 필터를 추가 하 고 솔루션을 실행 하 여 두 필터가 함께 작동 하는 방식을 확인 합니다.

1. **MvcMusicStore\Controllers** 에 있는 **StoreController** 클래스를 열고 다음 코드에 표시 된 것 처럼 **StoreController** 클래스에 새 사용자 지정 필터 **MyNewCustomActionFilter** 을 삽입 합니다.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample10.cs)]
2. 이제 응용 프로그램을 실행 하 여 이러한 두 사용자 지정 작업 필터가 작동 하는 방식을 확인 합니다. 이렇게 하려면 **F5** 키를 누르고 응용 프로그램이 시작 될 때까지 기다립니다.
3. **/Clog** 로 이동 하 여 로그 뷰 초기 상태를 확인 합니다.

    ![페이지 작업 전 로그 추적기 상태](aspnet-mvc-4-custom-action-filters/_static/image5.png "페이지 작업 전 로그 추적기 상태")

    *페이지 작업 전 로그 추적기 상태*
4. 메뉴에서 **장르** 중 하나를 클릭 하 고 사용 가능한 앨범 탐색과 같은 몇 가지 작업을 수행 합니다.
5. 이 시간이 있는지 확인 합니다. **StorageController** 클래스에 추가한 사용자 지정 작업 필터 각각에 대해 한 번씩, 두 번 방문이 추적 되었습니다.

    ![작업이 기록 된 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image6.png "작업이 기록 된 작업 로그")

    *작업이 기록 된 작업 로그*
6. 브라우저를 닫습니다.

<a id="Ex2Task3"></a>

<a id="Task_3_Managing_Filter_Ordering"></a>
#### <a name="task-3-managing-filter-ordering"></a>작업 3: 필터 순서 관리

이 태스크에서는 Order 속성을 사용 하 여 필터 실행 순서를 관리 하는 방법을 알아봅니다.

1. **MvcMusicStore\Controllers** 에 있는 **StoreController** 클래스를 열고 아래와 같이 두 필터 모두에 **Order** 속성을 지정 합니다.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample11.cs)]
2. 이제 Order 속성의 값에 따라 필터를 실행 하는 방법을 확인 합니다. 순서 값이 가장 작은 필터 (**CustomActionFilter**)가 가장 먼저 실행 되는 것을 알 수 있습니다. **F5** 키를 누르고 응용 프로그램이 시작 될 때까지 기다립니다.
3. **/Clog** 로 이동 하 여 로그 뷰 초기 상태를 확인 합니다.

    ![페이지 작업 전 로그 추적기 상태](aspnet-mvc-4-custom-action-filters/_static/image7.png "페이지 작업 전 로그 추적기 상태")

    *페이지 작업 전 로그 추적기 상태*
4. 메뉴에서 **장르** 중 하나를 클릭 하 고 사용 가능한 앨범 탐색과 같은 몇 가지 작업을 수행 합니다.
5. 이번에는 ' Order value: **CustomActionFilter** logs ' 필터를 기준으로 방문 시간이 먼저 추적 되었는지 확인 합니다.

    ![작업이 기록 된 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image8.png "작업이 기록 된 작업 로그")

    *작업이 기록 된 작업 로그*
6. 이제 필터의 순서 값을 업데이트 하 고 로깅 순서가 변경 되는 방식을 확인 합니다. **StoreController** 클래스에서 아래와 같이 필터의 순서 값을 업데이트 합니다.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample12.cs)]
7. **F5**키를 눌러 응용 프로그램을 다시 실행 합니다.
8. 메뉴에서 **장르** 중 하나를 클릭 하 고 사용 가능한 앨범 탐색과 같은 몇 가지 작업을 수행 합니다.
9. 이번에는 **MyNewCustomActionFilter** 필터로 만든 로그가 먼저 표시 되는지 확인 합니다.

    ![작업이 기록 된 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image9.png "작업이 기록 된 작업 로그")

    *작업이 기록 된 작업 로그*

<a id="Ex2Task4"></a>

<a id="Task_4_Registering_Filters_Globally"></a>
#### <a name="task-4-registering-filters-globally"></a>작업 4: 전역으로 필터 등록

이 태스크에서는 새 필터 (**MyNewCustomActionFilter**)를 전역 필터로 등록 하도록 솔루션을 업데이트 합니다. 이 작업을 수행 하면 응용 프로그램에서 수행 되는 모든 작업에 의해 트리거되고 이전 작업의 경우와 마찬가지로 StoreController에서 수행 됩니다.

1. **StoreController** 클래스에서 [ **MyNewCustomActionFilter]** 특성과 Order 속성을 **[CustomActionFilter]** 에서 제거 합니다. 다음과 같아야 합니다.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample13.cs)]
2. **Global.asax** 파일을 열고 **응용 프로그램\_Start** 메서드를 찾습니다. 응용 프로그램이 시작 될 때마다 **Filterconfig** 클래스 내에서 **registerglobalfilters** 메서드를 호출 하 여 전역 필터를 등록 하는 것입니다.

    ![Global.asax에 전역 필터를 등록 하는 중](aspnet-mvc-4-custom-action-filters/_static/image10.png "Global.asax에 전역 필터를 등록 하는 중")

    *Global.asax에 전역 필터를 등록 하는 중*
3. **앱\_시작** 폴더에서 **FilterConfig.cs** 파일을 엽니다.
4. System.web를 사용 하 여에 대 한 참조 추가 MvcMusicStore 사용 공간.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample14.cs)]
5. **Registerglobalfilters** 메서드를 업데이트 하 여 사용자 지정 필터를 추가 합니다. 이렇게 하려면 강조 표시 된 코드를 추가 합니다.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample15.cs)]
6. **F5**를 눌러 애플리케이션을 실행합니다.
7. 메뉴에서 **장르** 중 하나를 클릭 하 고 사용 가능한 앨범 탐색과 같은 몇 가지 작업을 수행 합니다.
8. 이제 **[MyNewCustomActionFilter]** 가 HomeController 및 ActionLogController에 삽입 되는지 확인 합니다.

    ![작업이 기록 된 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image11.png "작업이 기록 된 작업 로그")

    *글로벌 활동이 기록 된 작업 로그*

> [!NOTE]
> 또한 [부록 B: 웹 배포을 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시](#AppendixB)를 수행 하는 Windows Azure 웹 사이트에이 응용 프로그램을 배포할 수 있습니다.

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습 실습을 완료 하면 작업 필터를 확장 하 여 사용자 지정 작업을 실행 하는 방법을 알아보았습니다. 또한 페이지 컨트롤러에 필터를 삽입 하는 방법도 알아보았습니다. 사용 되는 개념은 다음과 같습니다.

- ASP.NET MVC ActionFilterAttribute 클래스를 사용 하 여 사용자 지정 작업 필터를 만드는 방법
- ASP.NET MVC 컨트롤러에 필터를 삽입 하는 방법
- Order 속성을 사용 하 여 필터 순서를 관리 하는 방법
- 전역으로 필터를 등록 하는 방법

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>부록 A: 웹에 대 한 Visual Studio Express 2012 설치

**[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)** 를 사용 하 여 웹 또는 다른 &quot;Express&quot; 버전 **에 대해 Microsoft Visual Studio Express 2012** 를 설치할 수 있습니다. 다음 지침에서는 *Microsoft 웹 플랫폼 설치 관리자*를 사용 하 여 *Visual studio Express 2012 for Web* 을 설치 하는 데 필요한 단계를 안내 합니다.

1. [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)로 이동합니다. 또는 웹 플랫폼 설치 관리자를 이미 설치한 경우에는 웹 플랫폼 설치 관리자를 열고 <em>Microsoft AZURE SDK&quot;를 사용 하 여 웹 용 2012 Visual Studio Express</em> &quot;제품을 검색할 수 있습니다.
2. **지금 설치**를 클릭 합니다. **웹 플랫폼 설치 관리자** 가 없으면 먼저이를 다운로드 하 여 설치 하도록 리디렉션됩니다.
3. **웹 플랫폼 설치 관리자** 가 열리면 **설치** 를 클릭 하 여 설치를 시작 합니다.

    ![Visual Studio Express 설치](aspnet-mvc-4-custom-action-filters/_static/image12.png "Visual Studio Express 설치")

    *Visual Studio Express 설치*
4. 모든 제품의 라이선스 및 사용 조건을 읽고 **동의** 함을 클릭 하 여 계속 합니다.

    ![사용 조건 동의](aspnet-mvc-4-custom-action-filters/_static/image13.png)

    *사용 조건 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](aspnet-mvc-4-custom-action-filters/_static/image14.png)

    *설치 진행률*
6. 설치가 완료 되 면 **마침**을 클릭 합니다.

    ![설치 완료](aspnet-mvc-4-custom-action-filters/_static/image15.png)

    *설치 완료*
7. **끝내기** 를 클릭 하 여 웹 플랫폼 설치 관리자를 닫습니다.
8. 웹에 대 한 Visual Studio Express를 열려면 **시작** 화면으로 이동 하 &quot;**VS Express**&quot;작성을 시작한 후 **VS Express for Web** 타일을 클릭 합니다.

    ![VS Express for Web 타일](aspnet-mvc-4-custom-action-filters/_static/image16.png)

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

    ![Windows Azure Portal에 로그온 합니다.](aspnet-mvc-4-custom-action-filters/_static/image17.png "Windows Azure Portal에 로그온 합니다.")

    *Windows Azure 관리 포털에 로그온 합니다.*
2. 명령 모음에서 **새로 만들기** 를 클릭 합니다.

    ![새 웹 사이트 만들기](aspnet-mvc-4-custom-action-filters/_static/image18.png "새 웹 사이트 만들기")

    *새 웹 사이트 만들기*
3. **Compute** | **웹 사이트**를 클릭 합니다. 그런 다음 **빠른 생성** 옵션을 선택 합니다. 새 웹 사이트에 사용할 수 있는 URL을 제공 하 고 **웹 사이트 만들기**를 클릭 합니다.

    > [!NOTE]
    > Microsoft Azure 웹 사이트는 사용자가 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램에 대 한 호스트입니다. 빠른 생성 옵션을 사용 하면 포털 외부에서 Windows Azure 웹 사이트에 완료 된 웹 응용 프로그램을 배포할 수 있습니다. 데이터베이스를 설정 하는 단계는 포함 되지 않습니다.

    ![빠른 생성을 사용 하 여 새 웹 사이트 만들기](aspnet-mvc-4-custom-action-filters/_static/image19.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")

    *빠른 생성을 사용 하 여 새 웹 사이트 만들기*
4. 새 **웹 사이트가** 만들어질 때까지 기다립니다.
5. 웹 사이트를 만든 후 **URL** 열 아래의 링크를 클릭 합니다. 새 웹 사이트가 작동 하는지 확인 합니다.

    ![새 웹 사이트로 이동](aspnet-mvc-4-custom-action-filters/_static/image20.png "새 웹 사이트로 이동")

    *새 웹 사이트로 이동*

    ![웹 사이트 실행 중](aspnet-mvc-4-custom-action-filters/_static/image21.png "웹 사이트 실행 중")

    *웹 사이트 실행 중*
6. 포털로 돌아가서 **이름** 열 아래에 있는 웹 사이트의 이름을 클릭 하 여 관리 페이지를 표시 합니다.

    ![웹 사이트 관리 페이지 열기](aspnet-mvc-4-custom-action-filters/_static/image22.png "웹 사이트 관리 페이지 열기")

    *웹 사이트 관리 페이지 열기*
7. **대시보드** 페이지의 **빠른** 보기 섹션에서 **게시 프로필 다운로드** 링크를 클릭 합니다.

    > [!NOTE]
    > *게시 프로필* 에는 사용 하도록 설정 된 각 게시 방법에 대해 웹 응용 프로그램을 Windows Azure 웹 사이트에 게시 하는 데 필요한 모든 정보가 포함 되어 있습니다. 게시 프로필에는 게시 방법이 사용 설정된 각 엔드포인트에 연결하고 이에 대해 인증하는 데 필요한 URL, 사용자 자격 증명 및 데이터베이스 문자열이 포함되어 있습니다. **Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** 및 **Microsoft Visual Studio 2012** 는 게시 프로필 읽기를 지원 하 여 웹 응용 프로그램을 Windows Azure 웹 사이트에 게시 하기 위해 이러한 프로그램의 구성을 자동화 합니다.

    ![웹 사이트 게시 프로필을 다운로드 하는 중](aspnet-mvc-4-custom-action-filters/_static/image23.png "웹 사이트 게시 프로필을 다운로드 하는 중")

    *웹 사이트 게시 프로필을 다운로드 하는 중*
8. 알려진 위치에 게시 프로필 파일을 다운로드 합니다. 이 연습을 통해이 파일을 사용 하 여 Visual Studio에서 Windows Azure 웹 사이트에 웹 응용 프로그램을 게시 하는 방법을 확인할 수 있습니다.

    ![게시 프로필 파일을 저장 하는 중](aspnet-mvc-4-custom-action-filters/_static/image24.png "게시 프로필을 저장 하는 중")

    *게시 프로필 파일을 저장 하는 중*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>작업 2-데이터베이스 서버 구성

응용 프로그램에서 SQL Server 데이터베이스를 사용 하는 경우 SQL Database 서버를 만들어야 합니다. SQL Server 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 작업을 건너뛸 수 있습니다.

1. 응용 프로그램 데이터베이스를 저장 하기 위한 SQL Database 서버가 필요 합니다. Microsoft Azure 관리 포털의 구독에서 SQL Database 서버를 볼 수는 **SQL 데이터베이스** | **서버** | **서버의 대시보드**. 만든 서버가 없는 경우 명령 모음에서 **추가** 단추를 사용 하 여 만들 수 있습니다. 다음 작업에서 사용할 **서버 이름과 URL, 관리자 로그인 이름 및 암호**를 기록해 둡니다. 이후 단계에서 생성 되므로 아직 데이터베이스를 만들지 마십시오.

    ![SQL Database 서버 대시보드](aspnet-mvc-4-custom-action-filters/_static/image25.png "SQL Database 서버 대시보드")

    *SQL Database 서버 대시보드*
2. 다음 작업에서는 Visual Studio에서 데이터베이스 연결을 테스트 합니다. 따라서 서버에서 **허용 되는 Ip 주소**목록에 로컬 IP 주소를 포함 해야 합니다. 이렇게 하려면 **구성**을 클릭 하 고, **현재 클라이언트 IP 주소** 에서 ip 주소를 선택 하 고, **시작 Ip 주소** 및 **끝 ip 주소** 텍스트 상자에 붙여 넣고, ![추가-클라이언트-ip 주소-확인 단추](aspnet-mvc-4-custom-action-filters/_static/image26.png) 단추를 클릭 합니다.

    ![클라이언트 IP 주소를 추가 하는 중](aspnet-mvc-4-custom-action-filters/_static/image27.png)

    *클라이언트 IP 주소를 추가 하는 중*
3. **클라이언트 Ip 주소가** 허용 된 ip 주소 목록에 추가 되 면 **저장** 을 클릭 하 여 변경 내용을 확인 합니다.

    ![변경 내용 확인](aspnet-mvc-4-custom-action-filters/_static/image28.png)

    *변경 내용 확인*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시

1. ASP.NET MVC 4 솔루션으로 돌아갑니다. **솔루션 탐색기**에서 웹 사이트 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 선택 합니다.

    ![응용 프로그램 게시](aspnet-mvc-4-custom-action-filters/_static/image29.png "응용 프로그램 게시")

    *웹 사이트 게시*
2. 첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.

    ![게시 프로필을 가져오는 중](aspnet-mvc-4-custom-action-filters/_static/image30.png "게시 프로필을 가져오는 중")

    *게시 프로필을 가져오는 중*
3. **연결 유효성 검사**를 클릭 합니다. 유효성 검사가 완료 되 면 **다음**을 클릭 합니다.

    > [!NOTE]
    > 유효성 검사는 연결 유효성 검사 단추 옆에 녹색 확인 표시가 표시 되 면 완료 됩니다.

    ![연결 유효성 검사](aspnet-mvc-4-custom-action-filters/_static/image31.png "연결 유효성 검사")

    *연결 유효성 검사*
4. **설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆에 있는 단추 (즉, **defaultconnection**)를 클릭 합니다.

    ![웹 배포 구성](aspnet-mvc-4-custom-action-filters/_static/image32.png "웹 배포 구성")

    *웹 배포 구성*
5. 데이터베이스 연결을 다음과 같이 구성 합니다.

   - **서버 이름** 에 *tcp:* 접두사를 사용 하 여 SQL Database 서버 URL을 입력 합니다.
   - **사용자 이름** 에 서버 관리자 로그인 이름을 입력 합니다.
   - **암호** 에 서버 관리자 로그인 암호를 입력 합니다.
   - 새 데이터베이스 이름을 입력 합니다.

     ![대상 연결 문자열 구성](aspnet-mvc-4-custom-action-filters/_static/image33.png "대상 연결 문자열 구성")

     *대상 연결 문자열 구성*
6. 그런 후 **OK**를 클릭합니다. 데이터베이스를 만들 것인지 묻는 메시지가 표시 되 면 **예**를 클릭 합니다.

    ![데이터베이스 만들기](aspnet-mvc-4-custom-action-filters/_static/image34.png "데이터베이스 문자열 만들기")

    *데이터베이스 만들기*
7. Windows Azure에서 SQL Database에 연결 하는 데 사용할 연결 문자열은 기본 연결 텍스트 상자 내에 표시 됩니다. 그런 후 **Next** 를 클릭합니다.

    ![SQL Database를 가리키는 연결 문자열](aspnet-mvc-4-custom-action-filters/_static/image35.png "SQL Database를 가리키는 연결 문자열")

    *SQL Database를 가리키는 연결 문자열*
8. **미리 보기** 페이지에서 **게시**를 클릭 합니다.

    ![웹 응용 프로그램 게시](aspnet-mvc-4-custom-action-filters/_static/image36.png "웹 응용 프로그램 게시")

    *웹 응용 프로그램 게시*
9. 게시 프로세스가 완료 되 면 기본 브라우저가 게시 된 웹 사이트를 엽니다.

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>부록 C: 코드 조각 사용

코드 조각을 사용 하면 필요한 모든 코드를 편리 하 게 사용할 수 있습니다. 랩 문서는 다음 그림에 표시 된 것 처럼 사용자가 사용할 수 있는 경우를 정확 하 게 알려줍니다.

![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입](aspnet-mvc-4-custom-action-filters/_static/image37.png "Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입")

*Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입*

***키보드를 사용 하 여 코드 조각을 추가 하려면C# (만 해당)***

1. 코드를 삽입할 위치에 커서를 놓습니다.
2. 조각 이름 (공백 또는 하이픈 제외)을 입력 하기 시작 합니다.
3. IntelliSense는 일치 하는 코드 조각의 이름을 표시 합니다.
4. 올바른 코드 조각을 선택 하거나 전체 코드 조각 이름이 선택 될 때까지 계속 입력 합니다.
5. Tab 키를 두 번 눌러 커서 위치에 코드 조각을 삽입 합니다.

![코드 조각 이름 입력 시작](aspnet-mvc-4-custom-action-filters/_static/image38.png "코드 조각 이름 입력 시작")

*코드 조각 이름 입력 시작*

![Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.](aspnet-mvc-4-custom-action-filters/_static/image39.png "Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.")

*Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.*

![Tab 키를 다시 누르면 코드 조각이 확장 됩니다.](aspnet-mvc-4-custom-action-filters/_static/image40.png "Tab 키를 다시 누르면 코드 조각이 확장 됩니다.")

*Tab 키를 다시 누르면 코드 조각이 확장 됩니다.*

***마우스C#(, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면*** 1(sp1). 코드 조각을 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭 합니다.

1. 코드 **조각 삽입** 을 선택한 다음 **내 코드 조각을**선택 합니다.
2. 목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.

![코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.](aspnet-mvc-4-custom-action-filters/_static/image41.png "코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.")

*코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.*

![목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.](aspnet-mvc-4-custom-action-filters/_static/image42.png "목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.")

*목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.*
