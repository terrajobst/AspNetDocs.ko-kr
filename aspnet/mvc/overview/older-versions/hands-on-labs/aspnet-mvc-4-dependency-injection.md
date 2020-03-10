---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
title: ASP.NET MVC 4 종속성 주입 | Microsoft Docs
author: rick-anderson
description: 참고:이 실습 랩에서는 ASP.NET MVC 및 ASP.NET MVC 4 필터에 대 한 기본 지식이 있다고 가정 합니다. 이전에 ASP.NET MVC 4 필터를 사용 하지 않은 경우
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 84c7baca-1c54-4c44-8f52-4282122d6acb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 15c9d4dcb9e2c6b9f6adf54d65d15737b32cca3b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451823"
---
# <a name="aspnet-mvc-4-dependency-injection"></a>ASP.NET MVC 4 종속성 주입

[웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 교육 키트 다운로드](https://aka.ms/webcamps-training-kit)

이 실습 랩에서는 **ASP.NET mvc** 및 **ASP.NET mvc 4 필터**에 대 한 기본 지식이 있다고 가정 합니다. 이전에 **ASP.NET mvc 4 필터** 를 사용 하지 않은 경우에는 **ASP.NET Mvc 사용자 지정 작업 필터** 실습 실습을 사용 하는 것이 좋습니다.

> [!NOTE]
> 모든 샘플 코드와 코드 조각은 [Microsoft 웹/WebCampTrainingKit 릴리스에서](https://aka.ms/webcamps-training-kit)제공 되는 웹 캠프 교육 키트에 포함 되어 있습니다. 이 랩에서 관련 된 프로젝트는 [ASP.NET MVC 4 종속성 주입](https://github.com/Microsoft-Web/HOL-MVC4DependencyInjection)에서 사용할 수 있습니다.

**개체 지향 프로그래밍** 패러다임에서 개체는 기여자와 소비자가 있는 공동 작업 모델에서 함께 작동 합니다. 기본적으로이 통신 모델은 개체와 구성 요소 간의 종속성을 생성 하므로 복잡성이 증가 하면 관리가 어려워집니다.

![클래스 종속성 및 모델 복잡성](aspnet-mvc-4-dependency-injection/_static/image1.png "클래스 종속성 및 모델 복잡성")

*클래스 종속성 및 모델 복잡성*

클라이언트 개체가 서비스 위치를 주로 담당 하는 서비스를 사용 하 여 **팩터리 패턴** 및 인터페이스와 구현 간의 분리에 대해 들었습니다.

종속성 주입 패턴은 제어 반전의 특정 구현입니다. **IoC (제어 반전)** 는 개체에서 작업을 수행 하는 데 사용 하는 다른 개체를 만들지 않음을 의미 합니다. 대신 외부 소스에서 필요한 개체 (예: xml 구성 파일)를 가져옵니다.

**DI (종속성 주입)** 는 일반적으로 생성자 매개 변수를 전달 하 고 속성을 설정 하는 프레임 워크 구성 요소에서 개체 개입 없이이 작업을 수행 함을 의미 합니다.

<a id="The_Dependency_Injection_DI_Design_Pattern"></a>
### <a name="the-dependency-injection-di-design-pattern"></a>DI (종속성 주입) 디자인 패턴

높은 수준에서 종속성 주입의 목표는 클라이언트 클래스 (예: *골퍼*)가 인터페이스를 충족 하는 항목 (예: *iclub*)을 요구 하는 것입니다. 구체적 형식 (예: *WoodClub, IronClub, WedgeClub* 또는 *putterclub*)을 고려 하지 않고 다른 사람이이를 처리 하려고 합니다 (예: 좋은 *caddy*). ASP.NET MVC의 종속성 확인자를 사용 하 여 다른 곳에 종속성 논리를 등록할 수 있습니다 (예: 컨테이너 또는 *클럽 모음*).

![종속성 주입 다이어그램](aspnet-mvc-4-dependency-injection/_static/image2.png "종속성 주입 그림")

*종속성 주입-골프 비유*

종속성 주입 패턴 및 제어 반전을 사용 하면 다음과 같은 이점이 있습니다.

- 클래스 결합을 줄입니다.
- 코드 재사용 향상
- 코드 유지 관리 효율성 향상
- 응용 프로그램 테스트 향상

> [!NOTE]
> 종속성 주입은 추상 팩터리 디자인 패턴을 사용 하는 경우에 비해 약간 차이가 있지만 두 방법 간에는 약간의 차이가 있습니다. DI는 팩터리와 등록 된 서비스를 호출 하 여 종속성을 해결 하기 위한 프레임 워크를 사용 합니다.

이제 종속성 주입 패턴을 이해 했으므로이 랩에서 ASP.NET MVC 4에서 적용 하는 방법에 대해 알아봅니다. **컨트롤러** 에서 종속성 주입을 사용 하 여 데이터베이스 액세스 서비스를 포함 하기 시작 합니다. 다음에는 서비스를 사용 하 고 정보를 표시 하는 종속성 주입을 **뷰에** 적용 합니다. 마지막으로 DI를 ASP.NET MVC 4 필터로 확장 하 여 솔루션에 사용자 지정 작업 필터를 삽입 합니다.

이 실습 랩에서는 다음 방법에 대해 알아봅니다.

- NuGet 패키지를 사용 하 여 종속성 주입을 위해 ASP.NET MVC 4를 Unity와 통합
- ASP.NET MVC 컨트롤러 내에서 종속성 주입 사용
- ASP.NET MVC 뷰 내에서 종속성 주입 사용
- ASP.NET MVC 작업 필터 내에서 종속성 주입 사용

> [!NOTE]
> 이 랩에서는 종속성 확인을 위해 Mvc3 NuGet 패키지를 사용 하 고 있지만 ASP.NET MVC 4에서 작동 하는 종속성 주입 프레임 워크를 조정할 수 있습니다.

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

Visual Studio Code 코드 조각을 잘 모르는 경우이를 사용 하는 방법을 알아보려면이 문서의 부록 [B: 코드 조각&quot;사용](#AppendixB) &quot;부록을 참조 하세요.

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>실습

이 실습 랩은 다음 연습으로 구성 됩니다.

1. [연습 1: 컨트롤러 삽입](#Exercise1)
2. [연습 2: 보기 삽입](#Exercise2)
3. [연습 3: 필터 삽입](#Exercise3)

> [!NOTE]
> 각 연습에는 연습을 완료 한 후 얻게 되는 결과 솔루션을 포함 하는 **끝** 폴더가 함께 제공 됩니다. 연습을 진행 하는 데 도움이 필요한 경우이 솔루션을 지침으로 사용할 수 있습니다.

이 랩을 완료 하는 데 소요 되는 예상 시간: **30 분**

<a id="Exercise1"></a>

<a id="Exercise_1_Injecting_a_Controller"></a>
### <a name="exercise-1-injecting-a-controller"></a>연습 1: 컨트롤러 삽입

이 연습에서는 NuGet 패키지를 사용 하 여 Unity를 통합 하 여 ASP.NET MVC 컨트롤러에서 종속성 주입을 사용 하는 방법에 대해 설명 합니다. 이러한 이유로 MvcMusicStore 컨트롤러에 서비스를 포함 하 여 데이터 액세스와 논리를 구분 합니다. 서비스는 **Unity**의 도움으로 종속성 주입을 사용 하 여 확인 되는 컨트롤러 생성자에 새 종속성을 만듭니다.

이 방법은 더 유연 하 고 쉽게 유지 관리 하 고 테스트할 수 있는 더 작은 결합 응용 프로그램을 생성 하는 방법을 보여 줍니다. ASP.NET MVC를 Unity와 통합 하는 방법에 대해서도 알아봅니다.

<a id="About_StoreManager_Service"></a>
#### <a name="about-storemanager-service"></a>About StoreManager Service

이제 begin 솔루션에 제공 된 MVC Music 저장소에 **StoreService**이라는 저장소 컨트롤러 데이터를 관리 하는 서비스가 포함 되어 있습니다. 아래에서 매장 서비스 구현을 찾을 수 있습니다. 모든 메서드는 모델 엔터티를 반환 합니다.

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample1.cs)]

이제 시작 솔루션의 **StoreController** 가 **StoreService**을 소비 합니다. 모든 데이터 참조는 **StoreController**에서 제거 되었으므로 **StoreService**를 사용 하는 메서드를 변경 하지 않고 현재 데이터 액세스 공급자를 수정할 수 있습니다.

**StoreController** 구현이 클래스 생성자 내에서 **StoreService** 를 사용 하 여 종속성을 포함 한다는 것을 아래에서 찾을 수 있습니다.

> [!NOTE]
> 이 연습에서 소개 하는 종속성은 IoC ( **제어 반전** )와 관련이 있습니다.
> 
> **StoreController** 클래스 생성자는 클래스 내부에서 서비스 호출을 수행 하는 데 필수적인 **IStoreService** 형식 매개 변수를 받습니다. 그러나 **StoreController** 는 모든 컨트롤러가 ASP.NET MVC와 함께 사용 해야 하는 기본 생성자 (매개 변수 없음)를 구현 하지 않습니다.
> 
> 종속성을 확인 하려면 추상 팩터리 (지정 된 형식의 개체를 반환 하는 클래스)에 의해 컨트롤러를 만들어야 합니다.

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample2.cs)]

> [!NOTE]
> 매개 변수가 없는 생성자를 선언 하지 않았으므로 클래스에서 서비스 개체를 보내지 않고 StoreController를 만들려고 하면 오류가 발생 합니다.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Running_the_Application"></a>
#### <a name="task-1---running-the-application"></a>작업 1-응용 프로그램 실행

이 작업에서는 응용 프로그램 논리에서 데이터 액세스를 분리 하는 저장소 컨트롤러에 서비스를 포함 하는 Begin 응용 프로그램을 실행 합니다.

응용 프로그램을 실행할 때 컨트롤러 서비스가 기본적으로 매개 변수로 전달 되지 않기 때문에 예외를 수신 합니다.

1. **Source\ex01-injecting**에서 **시작** 솔루션을 엽니다.

   1. 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.
   2. **NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.
   3. 마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.

      > [!NOTE]
      > NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다. NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다. 이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.
2. **Ctrl + F5** 키를 눌러 디버깅 하지 않고 응용 프로그램을 실행 합니다. **이 개체&quot;에 대해 정의 된 매개 변수가 없는 생성자** &quot;오류 메시지가 표시 됩니다.

    ![ASP.NET MVC Begin 응용 프로그램을 실행 하는 동안 오류 발생](aspnet-mvc-4-dependency-injection/_static/image3.png "ASP.NET MVC Begin 응용 프로그램을 실행 하는 동안 오류 발생")

    *ASP.NET MVC Begin 응용 프로그램을 실행 하는 동안 오류 발생*
3. 브라우저를 닫습니다.

다음 단계에서는이 컨트롤러에 필요한 종속성을 삽입 하기 위해 Music Store 솔루션에 대해 작업을 수행 합니다.

<a id="Ex1Task2"></a>

<a id="Task_2_-_Including_Unity_into_MvcMusicStore_Solution"></a>
#### <a name="task-2---including-unity-into-mvcmusicstore-solution"></a>작업 2-Unity를 MvcMusicStore 솔루션으로 포함

이 작업에서는 솔루션에 **Mvc3** NuGet 패키지를 포함 합니다.

> [!NOTE]
> Mvc3 패키지는 ASP.NET MVC 3 용으로 설계 되었지만 ASP.NET MVC 4와 완전히 호환 됩니다.
> 
> Unity는 인스턴스 및 유형 가로채기에 대 한 선택적 지원을 포함 하는 간단 하 고 확장 가능한 종속성 주입 컨테이너입니다. 모든 형식의 .NET 응용 프로그램에서 사용할 수 있는 범용 컨테이너입니다. 이 클래스는 컨테이너에 대 한 구성 요소 구성을 지연 하 여 개체 만들기, 런타임에 종속성을 지정 하는 요구 사항 추상화, 요구 사항 추상화를 비롯 하 여 종속성 주입 메커니즘에 있는 모든 일반적인 기능을 제공 합니다.

1. **MvcMusicStore** 프로젝트에 **Mvc3** NuGet 패키지를 설치 합니다. 이렇게 하려면 **다른 창** | **보기** 에서 **패키지 관리자 콘솔** 을 엽니다.
2. 다음 명령을 실행합니다.

    PMC

    [!code-powershell[Main](aspnet-mvc-4-dependency-injection/samples/sample3.ps1)]

    ![Mvc3 NuGet 패키지를 설치 하는 중](aspnet-mvc-4-dependency-injection/_static/image4.png "Mvc3 NuGet 패키지를 설치 하는 중")

    *Mvc3 NuGet 패키지를 설치 하는 중*
3. **Mvc3** 패키지가 설치 되 면 unity 구성을 간소화 하기 위해 자동으로 추가 하는 파일 및 폴더를 탐색 합니다.

    ![Mvc3 패키지가 설치 됨](aspnet-mvc-4-dependency-injection/_static/image5.png "Mvc3 패키지가 설치 됨")

    *Mvc3 패키지가 설치 됨*

<a id="Ex1Task3"></a>

<a id="Task_3_-_Registering_Unity_in_Globalasaxcs_Application_Start"></a>
#### <a name="task-3---registering-unity-in-globalasaxcs-application_start"></a>작업 3-Global.asax.cs 응용 프로그램에서 Unity 등록\_시작

이 작업에서는 **Global.asax.cs** 에 있는 **응용 프로그램\_시작** 메서드를 업데이트 하 여 Unity 부트스트래퍼 이니셜라이저를 호출한 다음 종속성 주입에 사용할 서비스와 컨트롤러를 등록 하는 부트스트래퍼 파일을 업데이트 합니다.

1. 이제 Unity 컨테이너와 종속성 확인자를 초기화 하는 파일인 부트스트래퍼가 연결 됩니다. 이렇게 하려면 **Global.asax.cs** 를 열고 **응용 프로그램\_Start** 메서드 내에 다음 강조 표시 된 코드를 추가 합니다.

    (코드 조각- *ASP.NET 종속성 주입 랩-Ex01-Unity Unity*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample4.cs)]
2. **Bootstrapper.cs** 파일을 엽니다.
3. **MvcMusicStore** 및 **MusicStore**네임 스페이스를 포함 합니다.

    (코드 조각- *ASP.NET 종속성 주입 랩-Ex01-부트스트래퍼 네임 스페이스 추가*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample5.cs)]
4. **Buildunitycontainer** 메서드의 콘텐츠를 store Controller 및 store 서비스를 등록 하는 다음 코드로 바꿉니다.

    (코드 조각- *ASP.NET 종속성 주입 랩-Ex01-Register Store Controller And Service*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample6.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>작업 4-응용 프로그램 실행

이 작업에서는 응용 프로그램을 실행 하 여 Unity를 포함 한 후 응용 프로그램을 로드할 수 있는지 확인 합니다.

1. **F5** 키를 눌러 응용 프로그램을 실행 합니다. 그러면 응용 프로그램이 오류 메시지를 표시 하지 않고 로드 됩니다.

    ![종속성 주입을 사용 하 여 응용 프로그램 실행](aspnet-mvc-4-dependency-injection/_static/image6.png "종속성 주입을 사용 하 여 응용 프로그램 실행")

    *종속성 주입을 사용 하 여 응용 프로그램 실행*
2. **/Store**으로 이동 합니다. 이제 **Unity**를 사용 하 여 만든 **StoreController**이 호출 됩니다.

    ![MVC Music Store](aspnet-mvc-4-dependency-injection/_static/image7.png "MVC Music Store")

    *MVC Music Store*
3. 브라우저를 닫습니다.

다음 연습에서는 ASP.NET MVC 뷰 및 작업 필터 내에서 사용 하기 위해 종속성 주입 범위를 확장 하는 방법을 알아봅니다.

<a id="Exercise2"></a>

<a id="Exercise_2_Injecting_a_View"></a>
### <a name="exercise-2-injecting-a-view"></a>연습 2: 보기 삽입

이 연습에서는 ASP.NET MVC 4 for Unity 통합의 새로운 기능을 사용 하 여 뷰에서 종속성 주입을 사용 하는 방법에 대해 설명 합니다. 이렇게 하려면 저장소 찾아보기 보기 내에서 사용자 지정 서비스를 호출 합니다. 그러면 아래에 메시지와 이미지가 표시 됩니다.

그런 다음 프로젝트를 Unity와 통합 하 고 사용자 지정 종속성 해결 프로그램을 만들어 종속성을 삽입 합니다.

<a id="Ex2Task1"></a>

<a id="Task_1_-_Creating_a_View_that_Consumes_a_Service"></a>
#### <a name="task-1---creating-a-view-that-consumes-a-service"></a>작업 1-서비스를 사용 하는 뷰 만들기

이 태스크에서는 새 종속성을 생성 하기 위해 서비스 호출을 수행 하는 뷰를 만듭니다. 서비스는이 솔루션에 포함 된 간단한 메시징 서비스로 구성 됩니다.

1. **Source\ex02-injecting View\Begin** 폴더에 있는 **begin** 솔루션을 엽니다. 그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.

   1. 제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.
   2. **NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.
   3. 마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.

      > [!NOTE]
      > NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다. NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다. 이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.
      > 
      > 자세한 내용은 [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)문서를 참조 하세요.
2. **MessageService.cs** 및 **IMessageService.cs** 클래스를 **/서비스**의 **Source \assets** 폴더에 있습니다. 이렇게 하려면 **서비스** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **기존 항목 추가**를 선택 합니다. 파일의 위치를 찾아 포함 합니다.

    ![메시지 서비스 및 서비스 인터페이스 추가](aspnet-mvc-4-dependency-injection/_static/image8.png "메시지 서비스 및 서비스 인터페이스 추가")

    *메시지 서비스 및 서비스 인터페이스 추가*

    > [!NOTE]
    > **IMessageService** 인터페이스는 **MessageService** 클래스에서 구현 하는 두 가지 속성을 정의 합니다. 이러한 속성-**message** 및 **ImageUrl**-메시지와 표시할 이미지의 URL을 저장 합니다.
3. 프로젝트의 루트 폴더에 폴더 **/페이지** 를 만든 다음 **source\assets**에서 기존 클래스 **MyBasePage.cs** 를 추가 합니다. 상속 하는 기본 페이지의 구조는 다음과 같습니다.

    ![Pages 폴더](aspnet-mvc-4-dependency-injection/_static/image9.png "페이지 폴더")

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample7.cs)]
4. **/Views/Store** 폴더에서 **Browse. cshtml** 뷰를 열고 **MyBasePage.cs**에서 상속 하도록 합니다.

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample8.cshtml)]
5. **찾아보기** 보기에서 **MessageService** 에 대 한 호출을 추가 하 여 서비스에서 검색 한 이미지와 메시지를 표시 합니다.
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample9.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Including_a_Custom_Dependency_Resolver_and_a_Custom_View_Page_Activator"></a>
#### <a name="task-2---including-a-custom-dependency-resolver-and-a-custom-view-page-activator"></a>작업 2-사용자 지정 종속성 해결 프로그램 및 사용자 지정 뷰 페이지 활성기 포함

이전 작업에서는 뷰 내부에 새 종속성을 삽입 하 여 내부에서 서비스 호출을 수행 했습니다. 이제 ASP.NET MVC 종속성 주입 인터페이스 **Iviewpageactivator** 및 **되며 idependencyresolver**를 구현 하 여 해당 종속성을 해결 합니다. Unity를 사용 하 여 서비스 검색을 처리 하는 **되며 idependencyresolver** 의 구현을 솔루션에 포함 합니다. 그런 다음 뷰 만들기를 해결 하는 **Iviewpageactivator** 인터페이스의 또 다른 사용자 지정 구현을 포함 합니다.

> [!NOTE]
> ASP.NET MVC 3부터 종속성 주입에 대 한 구현이 서비스를 등록 하는 인터페이스를 간소화 했습니다. **되며 idependencyresolver** 및 **Iviewpageactivator** 는 종속성 주입에 대 한 ASP.NET MVC 3 기능의 일부입니다.
> 
> **-되며 idependencyresolver** interface는 이전 IMvcServiceLocator를 대체 합니다. 되며 idependencyresolver의 구현자는 서비스 또는 서비스 컬렉션의 인스턴스를 반환 해야 합니다.
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample10.cs)]
> 
> **-Iviewpageactivator** 인터페이스는 종속성 주입을 통해 뷰 페이지를 인스턴스화하는 방법을 보다 세밀 하 게 제어할 수 있도록 합니다. **Iviewpageactivator** 인터페이스를 구현 하는 클래스는 컨텍스트 정보를 사용 하 여 뷰 인스턴스를 만들 수 있습니다.
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample11.cs)]

1. 프로젝트의 루트 폴더에/**팩터리** 폴더를 만듭니다.
2. **/Sources/Assets/** 에서 **팩터리** 폴더로 솔루션에 **CustomViewPageActivator.cs** 를 포함 합니다. 이렇게 하려면 **/ss** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 기존 항목** 을 선택한 다음 **CustomViewPageActivator.cs**를 선택 합니다. 이 클래스는 Unity 컨테이너를 포함 하는 **Iviewpageactivator** 인터페이스를 구현 합니다.

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample12.cs)]

    > [!NOTE]
    > **Customviewpageactivator** 는 Unity 컨테이너를 사용 하 여 뷰 만들기를 관리 합니다.
3. **UnityDependencyResolver.cs** 파일을 **/source/pers** **폴더에 포함** 합니다. 이렇게 하려면 **/ss** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 기존 항목** 을 선택한 다음 **UnityDependencyResolver.cs** 파일을 선택 합니다.

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample13.cs)]

    > [!NOTE]
    > **UnityDependencyResolver** 클래스는 Unity의 사용자 지정 DependencyResolver입니다. Unity 컨테이너 내에서 서비스를 찾을 수 없는 경우 기본 해결 프로그램은 invocated입니다.

다음 태스크에서는 모델에서 서비스 및 뷰의 위치를 알 수 있도록 두 구현이 모두 등록 됩니다.

<a id="Ex2Task3"></a>

<a id="Task_3_-_Registering_for_Dependency_Injection_within_Unity_container"></a>
#### <a name="task-3---registering-for-dependency-injection-within-unity-container"></a>작업 3-Unity 컨테이너 내에서 종속성 주입에 등록

이 태스크에서는 종속성 주입 작업을 수행 하기 위해 모든 이전 항목을 함께 저장 합니다.

이제 솔루션에는 다음과 같은 요소가 있습니다.

- **MyBaseClass** 에서 상속 되 고 **MessageService**를 소비 하는 **찾아보기** 뷰입니다.
- 서비스 인터페이스에 대해 선언 된 종속성 주입을 포함 하는 중간 클래스-**MyBaseClass**-
- **MessageService** 및 **IMessageService**인터페이스를 지원 합니다.
- 서비스 검색을 처리 하는 **UnityDependencyResolver** -에 대 한 사용자 지정 종속성 해결 프로그램입니다.
- 페이지를 만드는 뷰 페이지 활성기- **Customviewpageactivator** -

**찾아보기** 보기를 삽입 하려면 이제 Unity 컨테이너에 사용자 지정 종속성 해결 프로그램을 등록 합니다.

1. **Bootstrapper.cs** 파일을 엽니다.
2. **MessageService** 의 인스턴스를 Unity 컨테이너에 등록 하 여 서비스를 초기화 합니다.

    (코드 조각- *ASP.NET 종속성 주입 랩-Ex02-Register Message Service*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample14.cs)]
3. **MvcMusicStore** 네임 스페이스에 대 한 참조를 추가 합니다.

    (코드 조각- *ASP.NET 종속성 주입 랩-Ex02 네임 스페이스*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample15.cs)]
4. **Customviewpageactivator** 를 Unity 컨테이너에 뷰 페이지 활성기로 등록 합니다.

    (코드 조각- *ASP.NET 종속성 주입 랩-Ex02-Register CustomViewPageActivator*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample16.cs)]
5. ASP.NET MVC 4 기본 종속성 해결 프로그램을 **UnityDependencyResolver**인스턴스로 바꿉니다. 이렇게 하려면 **Initialize** 메서드 콘텐츠를 다음 코드로 바꿉니다.

    (코드 조각- *ASP.NET 종속성 주입 랩-Ex02-종속성 확인자 업데이트*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample17.cs)]

    > [!NOTE]
    > ASP.NET MVC는 기본 종속성 확인자 클래스를 제공 합니다. Unity 용으로 만든 사용자 지정 종속성 해결 프로그램을 사용 하려면이 해결 프로그램을 바꾸어야 합니다.

<a id="Ex2Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>작업 4-응용 프로그램 실행

이 작업에서는 응용 프로그램을 실행 하 여 저장소 브라우저가 서비스를 사용 하는지 확인 하 고 검색 된 이미지와 메시지를 표시 합니다.

1. **F5** 키를 눌러 애플리케이션을 실행합니다.
2. 장르 메뉴 내에서 **바위** 를 클릭 하 고 **MessageService** 가 보기에 삽입 되 고 환영 메시지와 이미지를 로드 하는 방법을 확인 합니다. 이 예제에서는 &quot;**록**&quot;을 입력 합니다.

    ![MVC Music Store-뷰 삽입](aspnet-mvc-4-dependency-injection/_static/image10.png "MVC Music Store-뷰 삽입")

    *MVC Music Store-뷰 삽입*
3. 브라우저를 닫습니다.

<a id="Exercise3"></a>

<a id="Exercise_3_Injecting_Action_Filters"></a>
### <a name="exercise-3-injecting-action-filters"></a>연습 3: 작업 필터 삽입

이전 실습 랩 **사용자 지정 작업 필터** 에서 필터 사용자 지정 및 삽입으로 작업 했습니다. 이 연습에서는 Unity 컨테이너를 사용 하 여 종속성 주입으로 필터를 삽입 하는 방법에 대해 설명 합니다. 이렇게 하려면 사이트의 활동을 추적 하는 사용자 지정 작업 필터를 Music Store 솔루션에 추가 합니다.

<a id="Ex3Task1"></a>

<a id="Task_1_-_Including_the_Tracking_Filter_in_the_Solution"></a>
#### <a name="task-1---including-the-tracking-filter-in-the-solution"></a>작업 1-솔루션에 추적 필터 포함

이 작업에서는 추적 이벤트에 사용자 지정 작업 필터를 음악 저장소에 포함 합니다. 사용자 지정 작업 필터 개념은 이전 실습 &quot;사용자 지정 작업 필터&quot;이미 처리 되었으므로이 랩의 자산 폴더에 필터 클래스를 포함 한 다음 Unity 용 필터 공급자를 만듭니다.

1. **Source\ex03-삽입 작업 filter\begin** 폴더에 있는 **시작** 솔루션을 엽니다. 그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.

   1. 제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.
   2. **NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.
   3. 마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.

      > [!NOTE]
      > NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다. NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다. 이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.
      > 
      > 자세한 내용은 [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)문서를 참조 하세요.
2. **TraceActionFilter.cs** 파일을/ssource/cerui> **에 포함** 합니다.

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample18.cs)]

    > [!NOTE]
    > 이 사용자 지정 작업 필터는 ASP.NET 추적을 수행 합니다. 자세한 참조는 &quot;ASP.NET MVC 4 로컬 및 동적 작업 필터&quot; Lab을 확인할 수 있습니다.
3. **FilterProvider.cs** **폴더의** 프로젝트에 빈 클래스를 추가 합니다.
4. **FilterProvider.cs**에 **system.web** 및 **Microsoft** 의 system.xml 네임 스페이스를 추가 합니다.

    (코드 조각- *ASP.NET 종속성 주입 랩-Ex03-네임 스페이스를 추가 하는 필터 공급자*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample19.cs)]
5. 클래스가 **Ifilterprovider** 인터페이스에서 상속 하도록 합니다.

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample20.cs)]
6. **Filterprovider** 클래스에서 **Iunitycontainer** 속성을 추가한 다음 클래스 생성자를 만들어 컨테이너를 할당 합니다.

    (코드 조각- *ASP.NET 종속성 주입 랩-Ex03-필터 공급자 생성자*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample21.cs)]

    > [!NOTE]
    > 필터 공급자 클래스 생성자가 내부에 **새** 개체를 만들지 않습니다. 컨테이너는 매개 변수로 전달 되 고 종속성은 Unity에서 해결 됩니다.
7. **Filterprovider** 클래스에서 **ifilterprovider** 인터페이스에서 **getfilters** 메서드를 구현 합니다.

    (코드 조각- *ASP.NET 종속성 주입 랩-Ex03-필터 공급자 GetFilters*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample22.cs)]

<a id="Ex3Task2"></a>

<a id="Task_2_-_Registering_and_Enabling_the_Filter"></a>
#### <a name="task-2---registering-and-enabling-the-filter"></a>작업 2-필터 등록 및 사용

이 작업에서는 사이트 추적을 사용 하도록 설정 합니다. 이렇게 하려면 **Bootstrapper.cs BuildUnityContainer** 메서드에 필터를 등록 하 여 추적을 시작 합니다.

1. 프로젝트 루트에 있는 **web.config** 를 열고 system.web 그룹에서 추적 추적을 사용 하도록 설정 합니다.

    [!code-xml[Main](aspnet-mvc-4-dependency-injection/samples/sample23.xml)]
2. **Bootstrapper.cs** at 프로젝트 루트를 엽니다.
3. **MvcMusicStore** 네임 스페이스에 대 한 참조를 추가 합니다.

    (코드 조각- *ASP.NET 종속성 주입 랩-Ex03-부트스트래퍼 네임 스페이스 추가*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample24.cs)]
4. **Buildunitycontainer** 메서드를 선택 하 고 Unity 컨테이너에 필터를 등록 합니다. 필터 공급자 및 작업 필터를 등록 해야 합니다.

    (코드 조각- *ASP.NET 종속성 주입 랩-Ex03-Register FilterProvider 및 ActionFilter*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample25.cs)]

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>작업 3-응용 프로그램 실행

이 작업에서는 응용 프로그램을 실행 하 고 사용자 지정 작업 필터가 작업을 추적 하는지 테스트 합니다.

1. **F5** 키를 눌러 애플리케이션을 실행합니다.
2. 장르 메뉴에서 **바위** 를 클릭 합니다. 원하는 경우 더 많은 장르를 찾아볼 수 있습니다.

    ![Music Store](aspnet-mvc-4-dependency-injection/_static/image11.png "Music Store")

    *Music Store*
3. **/Trace.xml** 로 이동 하 여 응용 프로그램 추적 페이지를 표시 한 다음 **자세히 보기**를 클릭 합니다.

    ![응용 프로그램 추적 로그](aspnet-mvc-4-dependency-injection/_static/image12.png "응용 프로그램 추적 로그")

    *응용 프로그램 추적 로그*

    ![응용 프로그램 추적-요청 정보](aspnet-mvc-4-dependency-injection/_static/image13.png "응용 프로그램 추적-요청 정보")

    *응용 프로그램 추적-요청 정보*
4. 브라우저를 닫습니다.

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습 실습을 완료 하면 NuGet 패키지를 사용 하 여 Unity를 통합 하 여 ASP.NET MVC 4에서 종속성 주입을 사용 하는 방법을 배웠습니다. 이를 위해 컨트롤러, 뷰 및 작업 필터 내에서 종속성 주입을 사용 했습니다.

다음 개념을 설명 합니다.

- ASP.NET MVC 4 종속성 주입 기능
- Mvc3 NuGet 패키지를 사용 하 여 unity 통합
- 컨트롤러의 종속성 주입
- 뷰의 종속성 주입
- 작업 필터의 종속성 주입

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>부록 A: 웹에 대 한 Visual Studio Express 2012 설치

**[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)** 를 사용 하 여 웹 또는 다른 &quot;Express&quot; 버전 **에 대해 Microsoft Visual Studio Express 2012** 를 설치할 수 있습니다. 다음 지침에서는 *Microsoft 웹 플랫폼 설치 관리자*를 사용 하 여 *Visual studio Express 2012 for Web* 을 설치 하는 데 필요한 단계를 안내 합니다.

1. [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)로 이동합니다. 또는 웹 플랫폼 설치 관리자를 이미 설치한 경우에는 웹 플랫폼 설치 관리자를 열고 <em>Microsoft AZURE SDK&quot;를 사용 하 여 웹 용 2012 Visual Studio Express</em> &quot;제품을 검색할 수 있습니다.
2. **지금 설치**를 클릭 합니다. **웹 플랫폼 설치 관리자** 가 없으면 먼저이를 다운로드 하 여 설치 하도록 리디렉션됩니다.
3. **웹 플랫폼 설치 관리자** 가 열리면 **설치** 를 클릭 하 여 설치를 시작 합니다.

    ![Visual Studio Express 설치](aspnet-mvc-4-dependency-injection/_static/image14.png "Visual Studio Express 설치")

    *Visual Studio Express 설치*
4. 모든 제품의 라이선스 및 사용 조건을 읽고 **동의** 함을 클릭 하 여 계속 합니다.

    ![사용 조건 동의](aspnet-mvc-4-dependency-injection/_static/image15.png)

    *사용 조건 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](aspnet-mvc-4-dependency-injection/_static/image16.png)

    *설치 진행률*
6. 설치가 완료 되 면 **마침**을 클릭 합니다.

    ![설치 완료](aspnet-mvc-4-dependency-injection/_static/image17.png)

    *설치 완료*
7. **끝내기** 를 클릭 하 여 웹 플랫폼 설치 관리자를 닫습니다.
8. 웹에 대 한 Visual Studio Express를 열려면 **시작** 화면으로 이동 하 &quot;**VS Express**&quot;작성을 시작한 후 **VS Express for Web** 타일을 클릭 합니다.

    ![VS Express for Web 타일](aspnet-mvc-4-dependency-injection/_static/image18.png)

    *VS Express for Web 타일*

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a>부록 B: 코드 조각 사용

코드 조각을 사용 하면 필요한 모든 코드를 편리 하 게 사용할 수 있습니다. 랩 문서는 다음 그림에 표시 된 것 처럼 사용자가 사용할 수 있는 경우를 정확 하 게 알려줍니다.

![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입](aspnet-mvc-4-dependency-injection/_static/image19.png "Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입")

*Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입*

***키보드를 사용 하 여 코드 조각을 추가 하려면C# (만 해당)***

1. 코드를 삽입할 위치에 커서를 놓습니다.
2. 조각 이름 (공백 또는 하이픈 제외)을 입력 하기 시작 합니다.
3. IntelliSense는 일치 하는 코드 조각의 이름을 표시 합니다.
4. 올바른 코드 조각을 선택 하거나 전체 코드 조각 이름이 선택 될 때까지 계속 입력 합니다.
5. Tab 키를 두 번 눌러 커서 위치에 코드 조각을 삽입 합니다.

![코드 조각 이름 입력 시작](aspnet-mvc-4-dependency-injection/_static/image20.png "코드 조각 이름 입력 시작")

*코드 조각 이름 입력 시작*

![Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.](aspnet-mvc-4-dependency-injection/_static/image21.png "Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.")

*Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.*

![Tab 키를 다시 누르면 코드 조각이 확장 됩니다.](aspnet-mvc-4-dependency-injection/_static/image22.png "Tab 키를 다시 누르면 코드 조각이 확장 됩니다.")

*Tab 키를 다시 누르면 코드 조각이 확장 됩니다.*

***마우스C#(, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면*** 1(sp1). 코드 조각을 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭 합니다.

1. 코드 **조각 삽입** 을 선택한 다음 **내 코드 조각을**선택 합니다.
2. 목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.

![코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.](aspnet-mvc-4-dependency-injection/_static/image23.png "코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.")

*코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.*

![목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.](aspnet-mvc-4-dependency-injection/_static/image24.png "목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.")

*목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.*
