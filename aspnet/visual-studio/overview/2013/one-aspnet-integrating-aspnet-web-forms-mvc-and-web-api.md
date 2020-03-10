---
uid: visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
title: '실습: One ASP.NET: ASP.NET Web Forms, MVC 및 Web API 통합 | Microsoft Docs'
author: rick-anderson
description: ASP.NET는 MVC, Web API 등의 전문 기술을 사용 하 여 웹 사이트, 앱 및 서비스를 빌드하기 위한 프레임 워크입니다. 확장 ASP.NET h ...
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 4fe2558d-67cc-4d12-a5c1-6fb9f6f16137
msc.legacyurl: /visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
msc.type: authoredcontent
ms.openlocfilehash: 165d104b5d3ef3281af449cc8673ad96f531d628
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505457"
---
# <a name="hands-on-lab-one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api"></a>실습: One ASP.NET: ASP.NET Web Forms, MVC 및 Web API 통합

[웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 교육 키트 다운로드](https://aka.ms/webcamps-training-kit)

> ASP.NET는 MVC, Web API 등의 전문 기술을 사용 하 여 웹 사이트, 앱 및 서비스를 빌드하기 위한 프레임 워크입니다. 확장 ASP.NET이 생성 된 후에는 이러한 기술이 통합 되어야 하 **는 것으로 나타났습니다.**
> 
> Visual Studio 2013에는 응용 프로그램을 빌드하고 한 프로젝트의 모든 ASP.NET 기술을 사용할 수 있도록 하는 통합 프로젝트 시스템이 새로 도입 되었습니다. 이 기능을 사용 하면 프로젝트를 시작할 때 한 기술을 선택 하 여 함께 사용할 필요가 없으며, 대신 한 프로젝트 내에서 여러 ASP.NET 프레임 워크를 사용 하는 것이 좋습니다.
> 
> 모든 샘플 코드와 코드 조각은 [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)에서 사용할 수 있는 웹 캠프 교육 키트에 포함 되어 있습니다.

<a id="Overview"></a>
## <a name="overview"></a>개요

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서는 다음 방법에 대해 알아봅니다.

- ASP.NET 프로젝트 형식 **하나** 를 기반으로 웹 사이트 만들기
- 동일한 프로젝트에서 **MVC** 및 **Web API** 와 같은 다른 **ASP.NET** 프레임 워크 사용
- **ASP.NET** 응용 프로그램의 주요 구성 요소를 식별 합니다.
- **ASP.NET 스 캐 폴딩** 프레임 워크를 활용 하 여 모델 클래스를 기반으로 CRUD 작업을 수행 하는 컨트롤러 및 뷰를 자동으로 만듭니다.
- 각 작업에 적합 한 도구를 사용 하 여 컴퓨터 및 사람이 읽을 수 있는 형식으로 동일한 정보 집합을 노출 합니다.

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>사전 요구 사항

이 실습 실습을 완료 하려면 다음이 필요 합니다.

- [웹 이상의 Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)
- [Visual Studio 2013 업데이트 1](https://go.microsoft.com/fwlink/?LinkId=301714)

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

1. [새 Web Forms 프로젝트 만들기](#Exercise1)
2. [스 캐 폴딩을 사용 하 여 MVC 컨트롤러 만들기](#Exercise2)
3. [스 캐 폴딩을 사용 하 여 Web API 컨트롤러 만들기](#Exercise3)

이 랩을 완료 하는 데 소요 되는 예상 시간: **60 분**

> [!NOTE]
> Visual Studio를 처음 시작 하는 경우 미리 정의 된 설정 컬렉션 중 하나를 선택 해야 합니다. 미리 정의 된 각 컬렉션은 특정 개발 스타일에 맞게 디자인 되 고 창 레이아웃, 편집기 동작, IntelliSense 코드 조각 및 대화 상자 옵션을 결정 합니다. 이 실습의 절차에서는 **일반 개발 설정** 컬렉션을 사용 하는 경우 Visual Studio에서 지정 된 작업을 수행 하는 데 필요한 작업을 설명 합니다. 개발 환경에 대해 다른 설정 컬렉션을 선택 하는 경우 고려해 야 하는 단계에 차이가 있을 수 있습니다.

<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-new-web-forms-project"></a>연습 1: 새 Web Forms 프로젝트 만들기

이 연습에서는 **하나의 ASP.NET** 통합 프로젝트 환경을 사용 하 여 Visual Studio 2013에 새 Web Forms 사이트를 만듭니다 .이를 통해 동일한 응용 프로그램에서 WEB FORMS, MVC 및 Web API 구성 요소를 쉽게 통합할 수 있습니다. 그런 다음 생성 된 솔루션을 탐색 하 고 파트를 식별 하 고 마지막으로 웹 사이트를 작동 하는 것을 볼 수 있습니다.

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-a-new-site-using-the-one-aspnet-experience"></a>작업 1-하나의 ASP.NET 환경을 사용 하 여 새 사이트 만들기

이 작업에서는 Visual Studio에서 ASP.NET 프로젝트 형식 **하나** 를 기반으로 새 웹 사이트 만들기를 시작 합니다. **한 ASP.NET** 는 모든 ASP.NET 기술을 통합 하 고 원하는 대로 혼합 하 고 일치 시킬 수 있는 옵션을 제공 합니다. 그런 다음 응용 프로그램 내에서 나란히 있는 Web Forms, MVC 및 Web API의 여러 구성 요소를 인식 합니다.

1. **웹에 대해 Visual Studio Express 2013** 을 열고 파일을 선택 합니다. **| 새 프로젝트** ... 새 솔루션을 시작 합니다.

    ![새 프로젝트 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image1.png)

    *새 프로젝트 만들기*
2. **새 프로젝트** 대화 상자의 시각적 개체  **C# 에서 ASP.NET 웹 응용 프로그램을 선택 합니다. 웹** 탭을 선택 하 고 **.NET Framework 4.5** 을 선택 했는지 확인 합니다. 프로젝트 이름을 *MyHybridSite*로, **위치** 를 선택 하 고 **확인**을 클릭 합니다.

    ![새 ASP.NET 웹 응용 프로그램 프로젝트](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image2.png)

    *새 ASP.NET 웹 응용 프로그램 프로젝트 만들기*
3. **새 ASP.NET 프로젝트** 대화 상자에서 **Web Forms** 템플릿을 선택 하 고 **MVC** 및 **Web API** 옵션을 선택 합니다. 또한 **인증** 옵션이 **개별 사용자 계정**으로 설정 되어 있는지 확인 합니다. 계속하려면 **확인** 을 클릭합니다.

    ![Web API 및 MVC 구성 요소를 포함 하 여 Web Forms 템플릿을 사용 하 여 새 프로젝트 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image3.png)

    *Web API 및 MVC 구성 요소를 포함 하 여 Web Forms 템플릿을 사용 하 여 새 프로젝트 만들기*
4. 이제 생성 된 솔루션의 구조를 탐색할 수 있습니다.

    ![생성 된 솔루션 살펴보기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image4.png)

    *생성 된 솔루션 살펴보기*

    1. **계정:** 이 폴더에는 응용 프로그램의 사용자 계정을 등록 하 고, 로그인 하 고, 관리할 웹 폼 페이지가 포함 되어 있습니다. 이 폴더는 Web Forms 프로젝트 템플릿을 구성 하는 동안 **개별 사용자 계정** 인증 옵션을 선택한 경우에 추가 됩니다.
    2. **모델:** 이 폴더에는 응용 프로그램 데이터를 나타내는 클래스가 포함 됩니다.
    3. **컨트롤러** 및 **뷰**: 이러한 폴더는 **ASP.NET MVC** 및 **ASP.NET Web API** 구성 요소에 필요 합니다. 다음 연습에서 MVC 및 Web API 기술을 살펴볼 것입니다.
    4. **Default.aspx 및** **.Aspx 파일에 대 한 정보** **는 응용**프로그램과 관련 된 페이지를 빌드하기 위한 시작 점으로 사용할 수 있는 미리 정의 된 웹 폼 페이지입니다. 이러한 파일의 프로그래밍 논리는 사용 되는 언어에 따라 &quot;.aspx&quot; 또는 &quot;aspx.cs&quot; 확장명을 포함 하는 &quot;코드 숨김이&quot; 파일 이라고 하는 별도의 파일에 있습니다. 코드 숨겨진 논리는 서버에서 실행 되 고 페이지에 대 한 HTML 출력을 동적으로 생성 합니다.
    5. **Site.master** 및 **site.master 페이지는** 응용 프로그램의 모든 페이지에 대 한 모양과 느낌 및 표준 동작을 정의 합니다.
5. **Default.aspx 파일을** 두 번 클릭 하 여 페이지의 내용을 탐색 합니다.

    ![Default.aspx 페이지 살펴보기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image5.png)

    *Default.aspx 페이지 살펴보기*

    > [!NOTE]
    > 파일 맨 위에 있는 **page** 지시어는 Web Forms 페이지의 특성을 정의 합니다. 예를 들어 **MasterPageFile** 특성은 마스터 페이지에 대 한 경로를 지정 합니다 *.* 이 경우에는 site.master 페이지와 **Inherits** 특성이 상속할 페이지의 코드 숨김이 클래스를 정의 합니다. 이 클래스는 **CodeBehind** 특성에 의해 결정 되는 파일에 있습니다.
    > 
    > **Asp: Content** 컨트롤은 페이지의 실제 콘텐츠 (텍스트, 태그 및 컨트롤)를 저장 하 고 마스터 페이지의 **asp: ContentPlaceHolder** 컨트롤에 매핑됩니다. 이 경우 페이지 콘텐츠는 *site.master* 페이지에 정의 된 *MainContent* 컨트롤 내에서 렌더링 됩니다.
6. **앱\_시작** 폴더를 확장 하 고 **WebApiConfig.cs** 파일을 확인 합니다. ASP.NET 템플릿 하나를 사용 하 여 프로젝트를 구성 하는 경우 Web API를 포함 했기 때문에 Visual Studio에서는 생성 된 솔루션에 해당 파일을 포함 했습니다.
7. **WebApiConfig.cs** 파일을 엽니다. *Webapiconfig* 클래스에서 web api에 연결 된 구성을 찾을 수 있으며,이는 HTTP 경로를 **웹 api 컨트롤러**에 매핑합니다.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample1.cs)]
8. **RouteConfig.cs** 파일을 엽니다. *RegisterRoutes* 메서드 내에서 mvc와 관련 된 구성을 찾을 수 있으며,이는 HTTP 경로를 **mvc 컨트롤러**에 매핑합니다.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample2.cs)]

<a id="Ex1Task2"></a>
#### <a name="task-2--running-the-solution"></a>작업 2-솔루션 실행

이 작업에서는 생성 된 솔루션을 실행 하 고 앱 및 URL 재작성 및 기본 제공 인증과 같은 일부 기능을 탐색 합니다.

1. 솔루션을 실행 하려면 **F5** 키를 누르거나 도구 모음에 있는 **시작** 단추를 클릭 합니다. 응용 프로그램 홈 페이지가 브라우저에서 열립니다.

    ![솔루션 실행](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image6.png)
2. Web Forms 페이지가 호출 되는지 확인 합니다. 이렇게 하려면 주소 표시줄의 URL에 **/contact.aspx** 를 추가 하 고 **enter**키를 누릅니다.

    ![친숙한 URL](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image7.png)

    *친숙 한 Url*

    > [!NOTE]
    > 여기에서 볼 수 있듯이 URL은 **/contact**로 변경 됩니다. **ASP.NET 4**부터 url 라우팅 기능이 Web Forms에 추가 되었으므로 *[http://www.mysite.com/products.aspx?category=software](http://www.mysite.com/products.aspx?category=software)* 대신 *[http://www.mysite.com/products/software](http://www.mysite.com/products/software)* 와 같은 url을 작성할 수 있습니다. 자세한 내용은 [URL 라우팅](../../../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing.md)을 참조 하세요.
3. 이제 응용 프로그램에 통합 된 인증 흐름이 탐색 됩니다. 이렇게 하려면 페이지의 오른쪽 위 모퉁이에 있는 **등록** 을 클릭 합니다.

    ![새 사용자 등록](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image8.png)

    *새 사용자 등록*
4. **등록** 페이지에서 **사용자 이름** 및 **암호**를 입력 한 다음 **등록**을 클릭 합니다.

    ![페이지 등록](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image9.png)

    *페이지 등록*
5. 응용 프로그램이 새 계정을 등록 하 고 사용자가 인증 됩니다.

    ![사용자 인증 됨](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image10.png)

    *사용자 인증 됨*
6. Visual Studio로 돌아가서 **SHIFT + f5** 키를 눌러 디버깅을 중지 합니다.

<a id="Exercise2"></a>
### <a name="exercise-2-creating-an-mvc-controller-using-scaffolding"></a>연습 2: 스 캐 폴딩을 사용 하 여 MVC 컨트롤러 만들기

이 연습에서는 Visual Studio에서 제공 하는 ASP.NET 스 캐 폴딩 프레임 워크를 활용 하 여 코드를 한 줄도 작성 하지 않고도 CRUD 작업을 수행 하는 작업 및 Razor 뷰로 ASP.NET MVC 5 컨트롤러를 만듭니다. 스 캐 폴딩 프로세스에서는 Entity Framework Code First를 사용 하 여 SQL database에 데이터 컨텍스트와 데이터베이스 스키마를 생성 합니다.

**Entity Framework Code First 정보**

EF (Entity Framework)는 관계형 저장소 스키마를 사용 하 여 직접 프로그래밍 하는 대신 개념적 응용 프로그램 모델을 사용 하 여 프로그래밍 하 여 데이터 액세스 응용 프로그램을 만들 수 있도록 하는 ORM (개체 관계형 매퍼)입니다.

Entity Framework Code First 모델링 워크플로를 사용 하면 사용자 고유의 도메인 클래스를 사용 하 여 쿼리, 변경 내용 추적 및 업데이트 기능을 수행할 때 EF에서 사용 하는 모델을 나타낼 수 있습니다. Code First 개발 워크플로를 사용 하 여 데이터베이스를 만들거나 스키마를 지정 하 여 응용 프로그램을 시작할 필요가 없습니다. 대신 응용 프로그램에 가장 적합 한 도메인 모델 개체를 정의 하는 표준 .NET 클래스를 작성할 수 있으며, Entity Framework는 데이터베이스를 만듭니다.

> [!NOTE]
> Entity Framework에 대 한 자세한 내용은 [여기](../../../entity-framework.md)를 참조 하세요.

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-new-model"></a>작업 1-새 모델 만들기

이제 **사용자** 클래스를 정의 합니다 .이는 스 캐 폴딩 프로세스에서 MVC 컨트롤러 및 뷰를 만드는 데 사용 하는 모델입니다. 먼저 **Person** 모델 클래스를 만들고, 컨트롤러의 CRUD 작업은 스 캐 폴딩 기능을 사용 하 여 자동으로 생성 됩니다.

1. **웹에 대해 Visual Studio Express 2013** 을 열고 **Source/Ex2-mvcscaffolding 캐 폴딩/Begin** 폴더에 있는 **MyHybridSite** 솔루션을 엽니다. 또는 이전 연습에서 얻은 솔루션을 계속 사용할 수 있습니다.
2. **솔루션 탐색기**에서 **MyHybridSite** 프로젝트의 **모델** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 클래스 ...** .

    ![Person 모델 클래스 추가](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image11.png)

    *Person 모델 클래스 추가*
3. **새 항목 추가** 대화 상자에서 파일 이름을 *Person.cs* 로 하 고 **추가**를 클릭 합니다.

    ![Person 모델 클래스 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image12.png)

    *Person 모델 클래스 만들기*
4. **Person.cs** 파일의 내용을 다음 코드로 바꿉니다. **Ctrl + S** 를 눌러 변경 내용을 저장 합니다.

    (코드 조각- *BringingTogetherOneAspNet-Ex2-PersonClass*)

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample3.cs)]
5. **솔루션 탐색기**에서 **MyHybridSite** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **빌드**를 선택 하거나 **ctrl + SHIFT + B** 를 눌러 프로젝트를 빌드합니다.

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-an-mvc-controller"></a>작업 2-MVC 컨트롤러 만들기

이제 **person** 모델을 만들었으므로 ASP.NET MVC 스 캐 폴딩을 Entity Framework와 함께 사용 하 여 **사용자**를 위한 CRUD 컨트롤러 작업 및 보기를 만듭니다.

1. **솔루션 탐색기**에서 **MyHybridSite** 프로젝트의 **Controllers** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 새 스 캐 폴드 항목**....

    ![새 스 캐 폴드 컨트롤러 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image13.png)

    *새 스 캐 폴드 컨트롤러 만들기*
2. **스 캐 폴드 추가** 대화 상자에서 **Entity Framework를 사용 하 여 MVC 5 컨트롤러 (뷰 포함)를** 선택 하 고 추가를 클릭 **합니다.**

    ![뷰 및 Entity Framework를 사용 하 여 MVC 5 컨트롤러 선택](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image14.png)

    *뷰 및 Entity Framework를 사용 하 여 MVC 5 컨트롤러 선택*
3. *MvcPersonController* 을 **컨트롤러 이름**으로 설정 하 고, **비동기 컨트롤러 작업 사용** 옵션을 선택 하 고, **모델 클래스로** **Person (MyHybridSite)** 을 선택 합니다.

    ![스 캐 폴딩을 사용 하 여 MVC 컨트롤러 추가](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image15.png)

    *스 캐 폴딩을 사용 하 여 MVC 컨트롤러 추가*
4. **데이터 컨텍스트 클래스**에서 **새 데이터 컨텍스트**...를 클릭 합니다.

    ![새 데이터 컨텍스트 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image16.png)

    *새 데이터 컨텍스트 만들기*
5. **새 데이터 컨텍스트** 대화 상자에서 새 데이터 컨텍스트의 이름을 *PersonContext* 하 고 **추가**를 클릭 합니다.

    ![새 PersonContext 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image17.png)

    *새 PersonContext 형식 만들기*
6. **추가** 를 클릭 하 여 스 캐 폴딩이 있는 **사용자** 에 대 한 새 컨트롤러를 만듭니다. 그런 다음 Visual Studio는 컨트롤러 작업, Person 데이터 컨텍스트 및 Razor 뷰를 생성 합니다.

    ![스 캐 폴딩을 사용 하 여 MVC 컨트롤러를 만든 후](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image18.png)

    *스 캐 폴딩을 사용 하 여 MVC 컨트롤러를 만든 후*
7. **Controllers** 폴더에서 **MvcPersonController.cs** 파일을 엽니다. CRUD 작업 메서드가 자동으로 생성 되었는지 확인 합니다.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample4.cs)]

    > [!NOTE]
    > 이전 단계에서 스 캐 폴딩 옵션의 비동기 **컨트롤러 작업 사용** 확인란을 선택 하면 Visual Studio는 Person 데이터 컨텍스트에 대 한 액세스를 포함 하는 모든 작업에 대해 비동기 작업 메서드를 생성 합니다. 요청이 처리 되는 동안 웹 서버에서 작업을 수행 하지 못하도록 차단 하지 않도록 장기 실행 CPU 바운드 요청에 대해 비동기 작업 메서드를 사용 하는 것이 좋습니다.

<a id="Ex2Task3"></a>
#### <a name="task-3--running-the-solution"></a>작업 3 – 솔루션 실행

이 작업에서는 솔루션을 다시 실행 하 여 **사용자** 의 뷰가 예상 대로 작동 하는지 확인 합니다. 새 사용자를 추가 하 여 데이터베이스에 성공적으로 저장 되었는지 확인 합니다.

1. **F5** 키를 눌러 솔루션을 실행합니다.
2. **/MvcPerson**로 이동 합니다. 사용자 목록이 표시 되는 스 캐 폴드 뷰가 표시 됩니다.
3. 새 사용자를 추가 하려면 **새로 만들기** 를 클릭 합니다.

    ![스 캐 폴드 MVC 뷰로 이동](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image19.png)

    *스 캐 폴드 MVC 뷰로 이동*
4. **만들기** 보기에서 사용자의 **이름과** **나** 이를 입력 하 고 **만들기**를 클릭 합니다.

    ![새 사용자 추가](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image20.png)

    *새 사용자 추가*
5. 새 사용자가 목록에 추가 됩니다. 요소 목록에서 **세부** 정보를 클릭 하 여 사용자의 세부 정보 보기를 표시 합니다. 그런 다음 **자세히** 보기에서 **목록으로** 돌아가기를 클릭 하 여 목록 보기로 돌아갑니다.

    ![사용자의 세부 정보 보기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image21.png)

    *사용자의 세부 정보 보기*
6. 사용자를 삭제 하려면 **삭제** 링크를 클릭 합니다. **삭제** 보기에서 **삭제** 를 클릭 하 여 작업을 확인 합니다.

    ![사람 삭제](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image22.png)

    *사람 삭제*
7. Visual Studio로 돌아가서 **SHIFT + f5** 키를 눌러 디버깅을 중지 합니다.

<a id="Exercise3"></a>
### <a name="exercise-3-creating-a-web-api-controller-using-scaffolding"></a>연습 3: 스 캐 폴딩을 사용 하 여 Web API 컨트롤러 만들기

Web API 프레임 워크는 ASP.NET 스택의 일부 이며 일반적으로 RESTful API를 통해 JSON 또는 XML 형식의 데이터를 보내고 받는 HTTP 서비스를 보다 쉽게 구현할 수 있도록 설계 되었습니다.

이 연습에서는 ASP.NET 스 캐 폴딩을 다시 사용 하 여 Web API 컨트롤러를 생성 합니다. 이전 연습에서 동일한 **person** 및 **PersonContext** 클래스를 사용 하 여 JSON 형식의 동일한 사람 데이터를 제공 합니다. 동일한 ASP.NET 응용 프로그램 내에서 여러 가지 방법으로 동일한 리소스를 노출 하는 방법을 확인할 수 있습니다.

<a id="Ex3Task1"></a>
#### <a name="task-1--creating-a-web-api-controller"></a>작업 1-Web API 컨트롤러 만들기

이 작업에서는 JSON과 같은 컴퓨터를 사용할 수 있는 형식으로 개인 데이터를 노출 하는 새 **WEB API 컨트롤러** 를 만듭니다.

1. 아직 열지 않은 경우 **웹에 대해 Visual Studio Express 2013** 을 열고 **Source/Ex3-WebAPI/Begin** 폴더에 있는 **MyHybridSite** 솔루션을 엽니다. 또는 이전 연습에서 얻은 솔루션을 계속 사용할 수 있습니다.

    > [!NOTE]
    > 연습 3에서 시작 솔루션으로 시작 하는 경우 **ctrl + SHIFT + B** 를 눌러 솔루션을 빌드합니다.
2. **솔루션 탐색기**에서 **MyHybridSite** 프로젝트의 **Controllers** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 새 스 캐 폴드 항목**....

    ![새 스 캐 폴드 컨트롤러 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image23.png)

    *새 스 캐 폴드 컨트롤러 만들기*
3. **스 캐 폴드 추가** 대화 상자의 왼쪽 창에서 **web api** 를 선택한 다음 가운데 창에서 **Entity Framework를 사용 하 여 동작을 포함 하는 web api 2 컨트롤러** 를 선택 하 고 추가를 클릭 **합니다.**

    ![작업 및 Entity Framework 웹 API 2 컨트롤러 선택](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image24.png "작업 및 Entity Framework 웹 API 2 컨트롤러 선택")

    *작업 및 Entity Framework 웹 API 2 컨트롤러 선택*
4. *ApiPersonController* 을 **컨트롤러 이름**으로 설정 하 고, **비동기 컨트롤러 작업 사용** 옵션을 선택 하 고, **모델** 및 **데이터 컨텍스트** 클래스로 각각 **Person (MyHybridSite)** 및 **PersonContext (MyHybridSite)** 를 선택 합니다. 그런 다음, **추가**를 클릭합니다.

    ![스 캐 폴딩을 사용 하 여 Web API 컨트롤러 추가](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image25.png "스 캐 폴딩을 사용 하 여 Web API 컨트롤러 추가")

    *스 캐 폴딩을 사용 하 여 Web API 컨트롤러 추가*
5. 그러면 Visual Studio에서 데이터를 사용할 수 있도록 네 가지 CRUD 작업을 사용 하 여 **ApiPersonController** 클래스를 생성 합니다.

    ![스 캐 폴딩을 사용 하 여 Web API 컨트롤러를 만든 후](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image26.png "스 캐 폴딩을 사용 하 여 Web API 컨트롤러를 만든 후")

    *스 캐 폴딩을 사용 하 여 Web API 컨트롤러를 만든 후*
6. **ApiPersonController.cs** 파일을 열고 *getpeople* 작업 메서드를 검사 합니다. 이 메서드는 사용자 데이터를 가져오기 위해 **PersonContext** 형식의 db 필드를 쿼리 합니다.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample5.cs)]
7. 이제 메서드 정의 위의 주석을 확인 합니다. 다음 작업에서 사용할이 작업을 노출 하는 URI를 제공 합니다.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample6.cs)]

    > [!NOTE]
    > 기본적으로 Web API는 */api* 경로에 대 한 쿼리를 catch 하 여 MVC 컨트롤러와의 충돌을 방지 하도록 구성 됩니다. 이 설정을 변경 해야 하는 경우 [ASP.NET Web API에서 라우팅](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md)을 참조 하세요.

<a id="Ex3Task2"></a>
#### <a name="task-2--running-the-solution"></a>작업 2-솔루션 실행

이 작업에서는 Internet Explorer **F12 개발자 도구** 를 사용 하 여 Web API 컨트롤러에서 전체 응답을 검사 합니다. 응용 프로그램 데이터에 대 한 자세한 정보를 얻기 위해 네트워크 트래픽을 캡처하는 방법을 확인할 수 있습니다.

> [!NOTE]
> Visual Studio 도구 모음에 있는 **시작** 단추에 **Internet Explorer** 가 선택 되어 있는지 확인 합니다.
> 
> ![Internet Explorer 옵션](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image27.png)
> 
> **F12 개발자 도구** 에는이 실습 실습에서 다루지 않는 다양 한 기능이 포함 되어 있습니다. 자세히 알아보려면 [F12 개발자 도구 사용](https://msdn.microsoft.com/library/ie/bg182326(v=vs.85))을 참조 하세요.

1. **F5** 키를 눌러 솔루션을 실행합니다.

    > [!NOTE]
    > 이 작업을 올바르게 수행 하려면 응용 프로그램에 데이터가 있어야 합니다. 데이터베이스가 비어 있는 경우 실습 2의 작업 3으로 돌아가서 MVC 뷰를 사용 하 여 새 사용자를 만드는 방법에 대 한 단계를 수행할 수 있습니다.
2. 브라우저에서 **F12** 키를 눌러 **개발자 도구** 패널을 엽니다. **Ctrl** + **4** 를 누르거나 **네트워크** 아이콘을 클릭 한 다음 녹색 화살표 단추를 클릭 하 여 네트워크 트래픽 캡처를 시작 합니다.

    ![Web API 네트워크 캡처 시작](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image28.png "Web API 네트워크 캡처 시작")

    *Web API 네트워크 캡처 시작*
3. 브라우저의 주소 표시줄에서 URL에 **api/ApiPerson** 을 추가 합니다. 이제 **ApiPersonController**응답의 세부 정보를 검사 합니다.

    ![Web API를 통해 개인 데이터 검색](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image29.png "Web API를 통해 개인 데이터 검색")

    *Web API를 통해 개인 데이터 검색*

    > [!NOTE]
    > 다운로드가 완료 되 면 다운로드 한 파일을 사용 하 여 작업을 수행 하 라는 메시지가 표시 됩니다. 개발자 도구 창을 통해 응답 콘텐츠를 볼 수 있으려면 대화 상자를 열어 둡니다.
4. 이제 응답의 본문을 검사 합니다. 이렇게 하려면 **세부 정보** 탭을 클릭 한 다음 **응답 본문**을 클릭 합니다. 다운로드 한 데이터가 **Person** 클래스에 해당 하는 속성 **Id**, **이름** 및 **기간** 을 가진 개체 목록 인지 확인할 수 있습니다.

    ![Web API 응답 본문 보기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image30.png "Web API 응답 본문 보기")

    *Web API 응답 본문 보기*

<a id="Ex3Task3"></a>
#### <a name="task-3--adding-web-api-help-pages"></a>작업 3 – Web API 도움말 페이지 추가

Web API를 만들 때 다른 개발자가 API를 호출 하는 방법을 알 수 있도록 도움말 페이지를 만드는 것이 유용 합니다. 설명서 페이지를 수동으로 만들고 업데이트할 수 있지만 유지 관리 작업을 수행 하지 않도록 하기 위해 자동으로 생성 하는 것이 좋습니다. 이 작업에서는 Nuget 패키지를 사용 하 여 웹 API 도움말 페이지를 솔루션에 자동으로 생성 합니다.

1. Visual Studio의 **도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 클릭 합니다.
2. **패키지 관리자 콘솔** 창에서 다음 명령을 실행 합니다.

    [!code-powershell[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample7.ps1)]

    > [!NOTE]
    > **WebApi** 패키지는 필요한 어셈블리를 설치 하 고 **영역/도움말 페이지** 폴더 아래에 도움말 페이지에 대 한 MVC 뷰를 추가 합니다.

    ![HelpPage 영역](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image31.png "HelpPage 영역")

    *HelpPage 영역*
3. 기본적으로 도움말 페이지에는 설명서에 대 한 자리 표시자 문자열이 있습니다. XML 문서 주석을 사용 하 여 설명서를 만들 수 있습니다. 이 기능을 사용 하도록 설정 하려면 **영역/도움말 페이지/앱\_시작** 폴더에 있는 **HelpPageConfig.cs** 파일을 열고 다음 줄의 주석 처리를 제거 합니다.

    [!code-javascript[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample8.js)]
4. **솔루션 탐색기**에서 **MyHybridSite**프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **속성** 을 선택한 다음 **빌드** 탭을 클릭 합니다.

    ![빌드 탭](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image32.png "빌드 섹션")

    *빌드 탭*
5. **출력**에서 **XML 문서 파일**을 선택 합니다. 편집 상자에 **App\_Data/XmlDocument**를 입력 합니다.

    ![빌드 탭의 출력 섹션](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image33.png "빌드 탭의 출력 섹션")

    *빌드 탭의 출력 섹션*
6. **Ctrl** + **S** 키를 눌러 변경 내용을 저장 합니다.
7. **Controllers** 폴더에서 **ApiPersonController.cs** 파일을 엽니다.
8. *Getpeople* 메서드 시그니처와 *//GET api/apiperson* 설명 사이에 새 줄을 입력 하 고 세 개의 슬래시를 입력 합니다.

    > [!NOTE]
    > Visual Studio는 메서드 설명서를 정의 하는 XML 요소를 자동으로 삽입 합니다.
9. *Getpeople* 메서드에 대 한 요약 텍스트 및 반환 값을 추가 합니다. 다음과 같이 표시 됩니다.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample9.cs)]
10. **F5** 키를 눌러 솔루션을 실행합니다.
11. 주소 표시줄의 URL에 **/help** 를 추가 하 여 도움말 페이지로 이동 합니다.

    ![ASP.NET Web API 도움말 페이지](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image34.png "ASP.NET Web API 도움말 페이지")

    *ASP.NET Web API 도움말 페이지*

    > [!NOTE]
    > 페이지의 기본 콘텐츠는 컨트롤러 별로 그룹화 된 Api의 테이블입니다. Table 항목은 **Iapiexplorer** 인터페이스를 사용 하 여 동적으로 생성 됩니다. API 컨트롤러를 추가 하거나 업데이트 하는 경우 다음에 응용 프로그램을 빌드할 때 테이블이 자동으로 업데이트 됩니다.
    > 
    > **API** 열에는 HTTP 메서드 및 상대 URI가 나열 됩니다. **설명** 열에는 메서드의 설명서에서 추출 된 정보가 포함 되어 있습니다.
12. 메서드 정의 위에 추가한 설명이 설명 열에 표시 됩니다.

    ![API 메서드 설명](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image35.png "API 메서드 설명")

    *API 메서드 설명*
13. API 메서드 중 하나를 클릭 하 여 샘플 응답 본문을 포함 하 여 더 자세한 정보가 포함 된 페이지로 이동 합니다.

    ![세부 정보 페이지](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image36.png "세부 정보 페이지")

    *세부 정보 페이지*

---

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습 실습을 완료 하면 다음 방법에 대해 알아보았습니다.

- Visual Studio 2013에서 하나의 ASP.NET 환경을 사용 하 여 새 웹 응용 프로그램을 만듭니다.
- 여러 ASP.NET 기술을 하나의 단일 프로젝트로 통합
- ASP.NET 스 캐 폴딩을 사용 하 여 모델 클래스에서 MVC 컨트롤러 및 뷰 생성
- 비동기 프로그래밍 및 데이터 액세스와 같은 기능을 사용 하는 웹 API 컨트롤러를 생성 Entity Framework
- 컨트롤러에 대 한 Web API 도움말 페이지를 자동으로 생성
