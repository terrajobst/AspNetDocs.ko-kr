---
uid: web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
title: ASP.NET Web API-ASP.NET 4.x를 사용 하 여 RESTful Api 빌드
author: rick-anderson
description: '실습: ASP.NET 4.x의 Web API를 사용 하 여 연락처 관리자 응용 프로그램에 대 한 간단한 REST API을 빌드합니다.'
ms.author: riande
ms.date: 02/18/2013
ms.custom: seoapril2019
ms.assetid: 87daa99f-3810-407e-b969-dd28a192959d
msc.legacyurl: /web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 35b115d6b4f84084e78e429bbb4842670e57bba4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504269"
---
# <a name="build-restful-apis-with-aspnet-web-api"></a><span data-ttu-id="cc703-103">ASP.NET Web API를 사용 하 여 RESTful Api 빌드</span><span class="sxs-lookup"><span data-stu-id="cc703-103">Build RESTful APIs with ASP.NET Web API</span></span>

<span data-ttu-id="cc703-104">[웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="cc703-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="cc703-105">실습: ASP.NET 4.x의 Web API를 사용 하 여 연락처 관리자 응용 프로그램에 대 한 간단한 REST API을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-105">Hands on lab: Use Web API in ASP.NET 4.x to build a simple REST API for a contact manager application.</span></span> <span data-ttu-id="cc703-106">API를 사용 하는 클라이언트도 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-106">You will also build a client to consume the API.</span></span>

<span data-ttu-id="cc703-107">최근 몇 년 동안 HTTP는 HTML 페이지를 제공 하는 것이 아니라는 것이 분명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-107">In recent years, it has become clear that HTTP is not just for serving up HTML pages.</span></span> <span data-ttu-id="cc703-108">또한 몇 가지 동사 (GET, POST 등) 뿐만 아니라 *uri* 및 *헤더*와 같은 몇 가지 간단한 개념을 사용 하 여 웹 api를 빌드하기 위한 강력한 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-108">It is also a powerful platform for building Web APIs, using a handful of verbs (GET, POST, and so forth) plus a few simple concepts such as *URIs* and *headers*.</span></span> <span data-ttu-id="cc703-109">ASP.NET Web API은 HTTP 프로그래밍을 간소화 하는 구성 요소 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-109">ASP.NET Web API is a set of components that simplify HTTP programming.</span></span> <span data-ttu-id="cc703-110">ASP.NET MVC 런타임 위에 빌드되기 때문에 Web API는 HTTP의 하위 수준 전송 세부 정보를 자동으로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-110">Because it is built on top of the ASP.NET MVC runtime, Web API automatically handles the low-level transport details of HTTP.</span></span> <span data-ttu-id="cc703-111">동시에 Web API는 HTTP 프로그래밍 모델을 자연스럽 게 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-111">At the same time, Web API naturally exposes the HTTP programming model.</span></span> <span data-ttu-id="cc703-112">사실 웹 API의 한 가지 목표는 HTTP의 현실에서 추상화 *하지 않는* 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-112">In fact, one goal of Web API is to *not* abstract away the reality of HTTP.</span></span> <span data-ttu-id="cc703-113">따라서 Web API는 유연 하 고 쉽게 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-113">As a result, Web API is both flexible and easy to extend.</span></span>  <span data-ttu-id="cc703-114">REST 아키텍처 스타일은 http에 대 한 유일한 유효한 방법이 아니라 HTTP를 활용 하는 효과적인 방법으로 입증 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-114">The REST architectural style has proven to be an effective way to leverage HTTP - although it is certainly not the only valid approach to HTTP.</span></span> <span data-ttu-id="cc703-115">연락처 관리자는 연락처를 나열, 추가 및 제거 하는 RESTful를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-115">The contact manager will expose the RESTful for listing, adding and removing contacts, among others.</span></span> 

<span data-ttu-id="cc703-116">이 랩에서는 HTTP, REST에 대 한 기본적인 이해가 필요 하며, HTML, JavaScript 및 jQuery에 대 한 기본적인 작업 지식이 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-116">This lab requires a basic understanding of HTTP, REST, and assumes you have a basic working knowledge of HTML, JavaScript, and jQuery.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="cc703-117">ASP.NET 웹 사이트에는 [https://asp.net/web-api](https://asp.net/web-api)ASP.NET Web API 프레임 워크 전용 영역이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-117">The ASP.NET Web site has an area dedicated to the ASP.NET Web API framework at [https://asp.net/web-api](https://asp.net/web-api).</span></span> <span data-ttu-id="cc703-118">이 사이트는 Web API와 관련 된 최신 정보, 샘플 및 뉴스를 계속 제공 하므로, 거의 모든 장치 또는 개발 프레임 워크에서 사용할 수 있는 사용자 지정 웹 Api를 만드는 데 더 자세히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-118">This site will continue to provide late-breaking information, samples, and news related to Web API, so check it frequently if you'd like to delve deeper into the art of creating custom Web APIs available to virtually any device or development framework.</span></span>
> > 
> > <span data-ttu-id="cc703-119">ASP.NET MVC 4와 마찬가지로, 사용 가능한 종속성 주입 프레임 워크를 매우 쉽게 사용할 수 있도록 컨트롤러에서 서비스 계층을 분리 하는 측면에서 상당한 유연성을 제공 합니다. ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="cc703-119">ASP.NET Web API, similar to ASP.NET MVC 4, has great flexibility in terms of separating the service layer from the controllers allowing you to use several of the available Dependency Injection frameworks fairly easy.</span></span> <span data-ttu-id="cc703-120">MSDN에는 [여기](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7)에서 다운로드할 수 있는 ASP.NET Web API 프로젝트에서 종속성 주입에 대 한 Ninject를 사용 하는 방법을 보여 주는 유용한 샘플이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-120">There is a good sample in MSDN that shows how to use Ninject for dependency injection in an ASP.NET Web API project that you can download it from [here](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7).</span></span>
> 
> 
> <span data-ttu-id="cc703-121">모든 샘플 코드와 코드 조각은 [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)에서 사용할 수 있는 웹 캠프 교육 키트에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-121">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="cc703-122">목표</span><span class="sxs-lookup"><span data-stu-id="cc703-122">Objectives</span></span>

<span data-ttu-id="cc703-123">이 실습 랩에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-123">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="cc703-124">RESTful Web API 구현</span><span class="sxs-lookup"><span data-stu-id="cc703-124">Implement a RESTful Web API</span></span>
- <span data-ttu-id="cc703-125">HTML 클라이언트에서 API 호출</span><span class="sxs-lookup"><span data-stu-id="cc703-125">Call the API from an HTML client</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="cc703-126">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="cc703-126">Prerequisites</span></span>

<span data-ttu-id="cc703-127">이 실습 실습을 완료 하려면 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-127">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="cc703-128">[웹 또는 고급의 경우 2012 Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (설치 방법에 대 한 지침은 [부록 B](#AppendixB) 를 참조 하세요.)</span><span class="sxs-lookup"><span data-stu-id="cc703-128">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix B](#AppendixB) for instructions on how to install it).</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="cc703-129">설치 프로그램</span><span class="sxs-lookup"><span data-stu-id="cc703-129">Setup</span></span>

<span data-ttu-id="cc703-130">**코드 조각 설치**</span><span class="sxs-lookup"><span data-stu-id="cc703-130">**Installing Code Snippets**</span></span>

<span data-ttu-id="cc703-131">편의를 위해이 랩에서 관리 하는 대부분의 코드는 Visual Studio 코드 조각으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-131">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="cc703-132">코드 조각을 설치 하려면 **.\Source\Setup\CodeSnippets.vsi** 파일을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-132">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="cc703-133">Visual Studio Code 코드 조각에 익숙하지 않은 경우이를 사용 하는 방법을 알아보려면 [부록 A: &quot;코드 조각&quot;사용](#AppendixA) 문서에서 부록을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-133">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix A: Using Code Snippets](#AppendixA)&quot;.</span></span>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="cc703-134">실습</span><span class="sxs-lookup"><span data-stu-id="cc703-134">Exercises</span></span>

<span data-ttu-id="cc703-135">이 실습 랩에는 다음 연습이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-135">This hands-on lab includes the following exercise:</span></span>

1. [<span data-ttu-id="cc703-136">연습 1: 읽기 전용 웹 API 만들기</span><span class="sxs-lookup"><span data-stu-id="cc703-136">Exercise 1: Create a Read-Only Web API</span></span>](#Exercise1)
2. [<span data-ttu-id="cc703-137">연습 2: 읽기/쓰기 웹 API 만들기</span><span class="sxs-lookup"><span data-stu-id="cc703-137">Exercise 2: Create a Read/Write Web API</span></span>](#Exercise2)
3. [<span data-ttu-id="cc703-138">연습 3: HTML 클라이언트에서 Web API 사용</span><span class="sxs-lookup"><span data-stu-id="cc703-138">Exercise 3: Consume the Web API from an HTML Client</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="cc703-139">각 연습에는 연습을 완료 한 후 얻게 되는 결과 솔루션을 포함 하는 **끝** 폴더가 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-139">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="cc703-140">연습을 진행 하는 데 도움이 필요한 경우이 솔루션을 지침으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-140">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="cc703-141">이 랩을 완료 하는 데 소요 되는 예상 시간: **60 분**</span><span class="sxs-lookup"><span data-stu-id="cc703-141">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Create_a_Read-Only_Web_API"></a>
### <a name="exercise-1-create-a-read-only-web-api"></a><span data-ttu-id="cc703-142">연습 1: 읽기 전용 웹 API 만들기</span><span class="sxs-lookup"><span data-stu-id="cc703-142">Exercise 1: Create a Read-Only Web API</span></span>

<span data-ttu-id="cc703-143">이 연습에서는 연락처 관리자에 대 한 읽기 전용 GET 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-143">In this exercise, you will implement the read-only GET methods for the contact manager.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_API_Project"></a>
#### <a name="task-1---creating-the-api-project"></a><span data-ttu-id="cc703-144">작업 1-API 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="cc703-144">Task 1 - Creating the API Project</span></span>

<span data-ttu-id="cc703-145">이 작업에서는 새로운 ASP.NET 웹 프로젝트 템플릿을 사용 하 여 Web API 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-145">In this task, you will use the new ASP.NET web project templates to create a Web API web application.</span></span>

1. <span data-ttu-id="cc703-146">**Visual Studio 2012 Express For Web**을 실행 하 여 **시작** 으로 이동 하 **VS Express for Web** 입력 한 다음 **enter**키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-146">Run **Visual Studio 2012 Express for Web**, to do this go to **Start** and type **VS Express for Web** then press **Enter**.</span></span>
2. <span data-ttu-id="cc703-147">**파일** 메뉴에서 **새 프로젝트**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-147">From the **File** menu, select **New Project**.</span></span> <span data-ttu-id="cc703-148">**시각적 개체 C# 를 선택 합니다. | 웹** 프로젝트 형식 트리 뷰에서 **ASP.NET MVC 4 웹 응용 프로그램** 프로젝트 형식을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-148">Select the **Visual C# | Web** project type from the project type tree view, then select the **ASP.NET MVC 4 Web Application** project type.</span></span> <span data-ttu-id="cc703-149">프로젝트의 **이름을** " *연락처 관리자* "로 설정 하 고 **솔루션 이름을** *시작*으로 설정한 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-149">Set the project's **Name** to *ContactManager* and the **Solution name** to *Begin*, then click **OK**.</span></span>

    <span data-ttu-id="cc703-150">![새 ASP.NET MVC 4.0 웹 응용 프로그램 프로젝트 만들기](build-restful-apis-with-aspnet-web-api/_static/image1.png "새 ASP.NET MVC 4.0 웹 응용 프로그램 프로젝트 만들기")</span><span class="sxs-lookup"><span data-stu-id="cc703-150">![Creating a new ASP.NET MVC 4.0 Web Application Project](build-restful-apis-with-aspnet-web-api/_static/image1.png "Creating a new ASP.NET MVC 4.0 Web Application Project")</span></span>

    <span data-ttu-id="cc703-151">*새 ASP.NET MVC 4.0 웹 응용 프로그램 프로젝트 만들기*</span><span class="sxs-lookup"><span data-stu-id="cc703-151">*Creating a new ASP.NET MVC 4.0 Web Application Project*</span></span>
3. <span data-ttu-id="cc703-152">ASP.NET MVC 4 프로젝트 형식 대화 상자에서 **WEB API** 프로젝트 형식을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-152">In the ASP.NET MVC 4 project type dialog, select the **Web API** project type.</span></span> <span data-ttu-id="cc703-153">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-153">Click **OK**.</span></span>

    <span data-ttu-id="cc703-154">![웹 API 프로젝트 형식 지정](build-restful-apis-with-aspnet-web-api/_static/image2.png "웹 API 프로젝트 형식 지정")</span><span class="sxs-lookup"><span data-stu-id="cc703-154">![Specifying the Web API project type](build-restful-apis-with-aspnet-web-api/_static/image2.png "Specifying the Web API project type")</span></span>

    <span data-ttu-id="cc703-155">*웹 API 프로젝트 형식 지정*</span><span class="sxs-lookup"><span data-stu-id="cc703-155">*Specifying the Web API project type*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_the_Contact_Manager_API_Controllers"></a>
#### <a name="task-2---creating-the-contact-manager-api-controllers"></a><span data-ttu-id="cc703-156">작업 2-연락처 관리자 API 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="cc703-156">Task 2 - Creating the Contact Manager API Controllers</span></span>

<span data-ttu-id="cc703-157">이 작업에서는 API 메서드가 상주할 컨트롤러 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-157">In this task, you will create the controller classes in which API methods will reside.</span></span>

1. <span data-ttu-id="cc703-158">프로젝트에서 **Controllers** 폴더에 있는 **ValuesController.cs** 라는 파일을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-158">Delete the file named **ValuesController.cs** within **Controllers** folder from the project.</span></span>
2. <span data-ttu-id="cc703-159">프로젝트의 **Controllers** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 컨트롤러** 를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-159">Right-click the **Controllers** folder in the project and select **Add | Controller** from the context menu.</span></span>

    <span data-ttu-id="cc703-160">![프로젝트에 새 컨트롤러 추가](build-restful-apis-with-aspnet-web-api/_static/image3.png "프로젝트에 새 컨트롤러 추가")</span><span class="sxs-lookup"><span data-stu-id="cc703-160">![Adding a new controller to the project](build-restful-apis-with-aspnet-web-api/_static/image3.png "Adding a new controller to the project")</span></span>

    <span data-ttu-id="cc703-161">*프로젝트에 새 컨트롤러 추가*</span><span class="sxs-lookup"><span data-stu-id="cc703-161">*Adding a new controller to the project*</span></span>
3. <span data-ttu-id="cc703-162">표시 되는 **컨트롤러 추가** 대화 상자의 템플릿 메뉴에서 **빈 API 컨트롤러** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-162">In the **Add Controller** dialog that appears, select **Empty API Controller** from the Template menu.</span></span> <span data-ttu-id="cc703-163">**Controller 클래스의**이름을 함께로 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-163">Name the controller class **ContactController**.</span></span> <span data-ttu-id="cc703-164">그런 다음 추가를 클릭 **합니다.**</span><span class="sxs-lookup"><span data-stu-id="cc703-164">Then, click **Add.**</span></span>

    <span data-ttu-id="cc703-165">![컨트롤러 추가 대화 상자를 사용 하 여 새 Web API 컨트롤러 만들기](build-restful-apis-with-aspnet-web-api/_static/image4.png "컨트롤러 추가 대화 상자를 사용 하 여 새 Web API 컨트롤러 만들기")</span><span class="sxs-lookup"><span data-stu-id="cc703-165">![Using the Add Controller dialog to create a new Web API controller](build-restful-apis-with-aspnet-web-api/_static/image4.png "Using the Add Controller dialog to create a new Web API controller")</span></span>

    <span data-ttu-id="cc703-166">*컨트롤러 추가 대화 상자를 사용 하 여 새 Web API 컨트롤러 만들기*</span><span class="sxs-lookup"><span data-stu-id="cc703-166">*Using the Add Controller dialog to create a new Web API controller*</span></span>
4. <span data-ttu-id="cc703-167">다음 코드를 **연락처 컨트롤러**에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-167">Add the following code to the **ContactController**.</span></span>

    <span data-ttu-id="cc703-168">(코드 조각- *WEB Api Lab-Ex01-Api 메서드 가져오기*)</span><span class="sxs-lookup"><span data-stu-id="cc703-168">(Code Snippet - *Web API Lab - Ex01 - Get API Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample1.cs)]
5. <span data-ttu-id="cc703-169">**F5** 키를 눌러 애플리케이션을 디버그합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-169">Press **F5** to debug the application.</span></span> <span data-ttu-id="cc703-170">웹 API 프로젝트에 대 한 기본 홈 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-170">The default home page for a Web API project should appear.</span></span>

    <span data-ttu-id="cc703-171">![ASP.NET Web API 응용 프로그램의 기본 홈 페이지](build-restful-apis-with-aspnet-web-api/_static/image5.png "ASP.NET Web API 응용 프로그램의 기본 홈 페이지")</span><span class="sxs-lookup"><span data-stu-id="cc703-171">![The default home page of an ASP.NET Web API application](build-restful-apis-with-aspnet-web-api/_static/image5.png "The default home page of an ASP.NET Web API application")</span></span>

    <span data-ttu-id="cc703-172">*ASP.NET Web API 응용 프로그램의 기본 홈 페이지*</span><span class="sxs-lookup"><span data-stu-id="cc703-172">*The default home page of an ASP.NET Web API application*</span></span>
6. <span data-ttu-id="cc703-173">Internet Explorer 창에서 **F12** 키를 눌러 **개발자 도구** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-173">In the Internet Explorer window, press the **F12** key to open the **Developer Tools** window.</span></span> <span data-ttu-id="cc703-174">**네트워크** 탭을 클릭 한 다음 **캡처 시작** 단추를 클릭 하 여 창으로의 네트워크 트래픽 캡처를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-174">Click the **Network** tab, and then click the **Start Capturing** button to begin capturing network traffic into the window.</span></span>

    <span data-ttu-id="cc703-175">![네트워크 탭을 열고 네트워크 캡처 시작](build-restful-apis-with-aspnet-web-api/_static/image6.png "네트워크 탭을 열고 네트워크 캡처 시작")</span><span class="sxs-lookup"><span data-stu-id="cc703-175">![Opening the network tab and initiating network capture](build-restful-apis-with-aspnet-web-api/_static/image6.png "Opening the network tab and initiating network capture")</span></span>

    <span data-ttu-id="cc703-176">*네트워크 탭을 열고 네트워크 캡처 시작*</span><span class="sxs-lookup"><span data-stu-id="cc703-176">*Opening the network tab and initiating network capture*</span></span>
7. <span data-ttu-id="cc703-177">URL을 브라우저의 주소 표시줄에 **/ci/cer&gt** 에 추가 하 고 enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-177">Append the URL in the browser's address bar with **/api/contact** and press enter.</span></span> <span data-ttu-id="cc703-178">전송 세부 정보는 네트워크 캡처 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-178">The transmission details will appear in the network capture window.</span></span> <span data-ttu-id="cc703-179">응답의 MIME 형식은 **application/json**입니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-179">Note that the response's MIME type is **application/json**.</span></span> <span data-ttu-id="cc703-180">기본 출력 형식이 JSON 인 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-180">This demonstrates how the default output format is JSON.</span></span>

    <span data-ttu-id="cc703-181">![네트워크 보기에서 Web API 요청 출력 보기](build-restful-apis-with-aspnet-web-api/_static/image7.png "네트워크 보기에서 Web API 요청 출력 보기")</span><span class="sxs-lookup"><span data-stu-id="cc703-181">![Viewing the output of the Web API request in the Network view](build-restful-apis-with-aspnet-web-api/_static/image7.png "Viewing the output of the Web API request in the Network view")</span></span>

    <span data-ttu-id="cc703-182">*네트워크 보기에서 Web API 요청 출력 보기*</span><span class="sxs-lookup"><span data-stu-id="cc703-182">*Viewing the output of the Web API request in the Network view*</span></span>

    > [!NOTE]
    > <span data-ttu-id="cc703-183">이 시점에서 Internet Explorer 10의 기본 동작은 사용자가 웹 API 호출로 인해 발생 하는 스트림을 저장 하거나 열지를 요청 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-183">Internet Explorer 10's default behavior at this point will be to ask if the user would like to save or open the stream resulting from the Web API call.</span></span> <span data-ttu-id="cc703-184">출력은 Web API URL 호출의 JSON 결과가 포함 된 텍스트 파일이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-184">The output will be a text file containing the JSON result of the Web API URL call.</span></span> <span data-ttu-id="cc703-185">개발자 도구 창을 통해 응답 콘텐츠를 볼 수 있으려면 대화 상자를 취소 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="cc703-185">Do not cancel the dialog in order to be able to watch the response's content through Developers Tool window.</span></span>
8. <span data-ttu-id="cc703-186">이 API 호출의 응답에 대 한 자세한 내용을 보려면 **자세히 보기로 이동** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-186">Click the **Go to detailed view** button to see more details about the response of this API call.</span></span>

    <span data-ttu-id="cc703-187">![자세히 보기로 전환](build-restful-apis-with-aspnet-web-api/_static/image8.png "자세히 보기로 전환")</span><span class="sxs-lookup"><span data-stu-id="cc703-187">![Switch to Detailed View](build-restful-apis-with-aspnet-web-api/_static/image8.png "Switch to Details View")</span></span>

    <span data-ttu-id="cc703-188">*자세히 보기로 전환*</span><span class="sxs-lookup"><span data-stu-id="cc703-188">*Switch to Detailed View*</span></span>
9. <span data-ttu-id="cc703-189">**응답 본문** 탭을 클릭 하 여 실제 JSON 응답 텍스트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-189">Click the **Response body** tab to view the actual JSON response text.</span></span>

    <span data-ttu-id="cc703-190">![네트워크 모니터에서 JSON 출력 텍스트 보기](build-restful-apis-with-aspnet-web-api/_static/image9.png "네트워크 모니터에서 JSON 출력 텍스트 보기")</span><span class="sxs-lookup"><span data-stu-id="cc703-190">![Viewing the JSON output text in the network monitor](build-restful-apis-with-aspnet-web-api/_static/image9.png "Viewing the JSON output text in the network monitor")</span></span>

    <span data-ttu-id="cc703-191">*네트워크 모니터에서 JSON 출력 텍스트 보기*</span><span class="sxs-lookup"><span data-stu-id="cc703-191">*Viewing the JSON output text in the network monitor*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Creating_the_Contact_Models_and_Augment_the_Contact_Controller"></a>
#### <a name="task-3---creating-the-contact-models-and-augment-the-contact-controller"></a><span data-ttu-id="cc703-192">작업 3-연락처 모델 만들기 및 연락처 컨트롤러 보강</span><span class="sxs-lookup"><span data-stu-id="cc703-192">Task 3 - Creating the Contact Models and Augment the Contact Controller</span></span>

<span data-ttu-id="cc703-193">이 작업에서는 API 메서드가 상주할 컨트롤러 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-193">In this task, you will create the controller classes in which API methods will reside.</span></span>

1. <span data-ttu-id="cc703-194">**모델** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 클래스 ...** 상황에 맞는 메뉴에서.</span><span class="sxs-lookup"><span data-stu-id="cc703-194">Right-click the **Models** folder and select **Add | Class...** from the context menu.</span></span>

    <span data-ttu-id="cc703-195">![웹 응용 프로그램에 새 모델 추가](build-restful-apis-with-aspnet-web-api/_static/image10.png "웹 응용 프로그램에 새 모델 추가")</span><span class="sxs-lookup"><span data-stu-id="cc703-195">![Adding a new model to the web application](build-restful-apis-with-aspnet-web-api/_static/image10.png "Adding a new model to the web application")</span></span>

    <span data-ttu-id="cc703-196">*웹 응용 프로그램에 새 모델 추가*</span><span class="sxs-lookup"><span data-stu-id="cc703-196">*Adding a new model to the web application*</span></span>
2. <span data-ttu-id="cc703-197">**새 항목 추가** 대화 상자에서 새 파일의 이름을 **Contact.cs** 로 하 고 **추가를 클릭 합니다.**</span><span class="sxs-lookup"><span data-stu-id="cc703-197">In the **Add New Item** dialog, name the new file **Contact.cs** and click **Add.**</span></span>

    <span data-ttu-id="cc703-198">![새 연락처 클래스 파일 만들기](build-restful-apis-with-aspnet-web-api/_static/image11.png "새 연락처 클래스 파일 만들기")</span><span class="sxs-lookup"><span data-stu-id="cc703-198">![Creating the new Contact class file](build-restful-apis-with-aspnet-web-api/_static/image11.png "Creating the new Contact class file")</span></span>

    <span data-ttu-id="cc703-199">*새 연락처 클래스 파일 만들기*</span><span class="sxs-lookup"><span data-stu-id="cc703-199">*Creating the new Contact class file*</span></span>
3. <span data-ttu-id="cc703-200">**Contact** 클래스에 다음 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-200">Add the following highlighted code to the **Contact** class.</span></span>

    <span data-ttu-id="cc703-201">(코드 조각- *WEB API Lab-Ex01 클래스*)</span><span class="sxs-lookup"><span data-stu-id="cc703-201">(Code Snippet - *Web API Lab - Ex01 - Contact Class*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample2.cs)]
4. <span data-ttu-id="cc703-202">연락처 **컨트롤러** 클래스에서 **Get** 메서드의 메서드 정의에 있는 단어 **문자열** 을 선택 하 고 *Contact*라는 단어를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-202">In the **ContactController** class, select the word **string** in method definition of the **Get** method, and type the word *Contact*.</span></span> <span data-ttu-id="cc703-203">단어가 입력 되 면 **연락처**의 시작 부분에 표시기가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-203">Once the word is typed in, an indicator will appear at the beginning of the word **Contact**.</span></span> <span data-ttu-id="cc703-204">**Ctrl** 키를 누른 채 마침표 (.) 키를 누르거나 마우스를 사용 하 여 아이콘을 클릭 하 여 코드 편집기에서 지원 대화 상자를 열고 모델 네임 스페이스에 대 한 **using** 지시문을 자동으로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-204">Either hold down the **Ctrl** key and press the period (.) key or click the icon using your mouse to open up the assistance dialog in the code editor, to automatically fill in the **using** directive for the Models namespace.</span></span>

    ![네임 스페이스 선언에 Intellisense 지원 사용](build-restful-apis-with-aspnet-web-api/_static/image12.png)

    <span data-ttu-id="cc703-206">*네임 스페이스 선언에 Intellisense 지원 사용*</span><span class="sxs-lookup"><span data-stu-id="cc703-206">*Using Intellisense assistance for namespace declarations*</span></span>
5. <span data-ttu-id="cc703-207">**Get** 메서드에 대 한 코드를 수정 하 여 Contact model 인스턴스의 배열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-207">Modify the code for the **Get** method so that it returns an array of Contact model instances.</span></span>

    <span data-ttu-id="cc703-208">(코드 조각- *웹 API 랩-Ex01-연락처 목록 반환*)</span><span class="sxs-lookup"><span data-stu-id="cc703-208">(Code Snippet - *Web API Lab - Ex01 - Returning a list of contacts*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample3.cs)]
6. <span data-ttu-id="cc703-209">**F5** 키를 눌러 브라우저에서 웹 응용 프로그램을 디버깅 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-209">Press **F5** to debug the web application in the browser.</span></span> <span data-ttu-id="cc703-210">API의 응답 출력에 대 한 변경 내용을 보려면 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-210">To view the changes made to the response output of the API, perform the following steps.</span></span>

   1. <span data-ttu-id="cc703-211">브라우저가 열리면 **F12** 키를 누른 상태로 개발자 도구가 아직 열리지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-211">Once the browser opens, press **F12** if the developer tools are not open yet.</span></span>
   2. <span data-ttu-id="cc703-212">**네트워크** 탭을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-212">Click the **Network** tab.</span></span>
   3. <span data-ttu-id="cc703-213">**캡처 시작** 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-213">Press the **Start Capturing** button.</span></span>
   4. <span data-ttu-id="cc703-214">주소 표시줄의 URL에 URL 접미사/s a l i o n/ **연락처** 를 추가 하 고 **enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-214">Add the URL suffix **/api/contact** to the URL in the address bar and press the **Enter** key.</span></span>
   5. <span data-ttu-id="cc703-215">**자세히 보기로 이동** 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-215">Press the **Go to detailed view** button.</span></span>
   6. <span data-ttu-id="cc703-216">**응답 본문** 탭을 선택 합니다. 연락처 인스턴스 배열의 serialize 된 형식을 나타내는 JSON 문자열이 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-216">Select the **Response body** tab. You should see a JSON string representing the serialized form of an array of Contact instances.</span></span>

      <span data-ttu-id="cc703-217">![복합 웹 API 메서드 호출의 JSON 직렬화 된 출력](build-restful-apis-with-aspnet-web-api/_static/image13.png "복합 웹 API 메서드 호출의 JSON 직렬화 된 출력")</span><span class="sxs-lookup"><span data-stu-id="cc703-217">![JSON serialized output of a complex Web API method call](build-restful-apis-with-aspnet-web-api/_static/image13.png "JSON serialized output of a complex Web API method call")</span></span>

      <span data-ttu-id="cc703-218">*복합 웹 API 메서드 호출의 JSON 직렬화 된 출력*</span><span class="sxs-lookup"><span data-stu-id="cc703-218">*JSON serialized output of a complex Web API method call*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Extracting_Functionality_into_a_Service_Layer"></a>
#### <a name="task-4---extracting-functionality-into-a-service-layer"></a><span data-ttu-id="cc703-219">작업 4-서비스 계층으로 기능 압축 풀기</span><span class="sxs-lookup"><span data-stu-id="cc703-219">Task 4 - Extracting Functionality into a Service Layer</span></span>

<span data-ttu-id="cc703-220">이 작업에서는 개발자가 서비스 기능을 컨트롤러 계층에서 분리 하 여 실제로 작업을 수행 하는 서비스의 재사용을 가능 하 게 하는 서비스 계층으로 기능을 추출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-220">This task will demonstrate how to extract functionality into a Service layer to make it easy for developers to separate their service functionality from the controller layer, thereby allowing reusability of the services that actually do the work.</span></span>

1. <span data-ttu-id="cc703-221">솔루션 루트에서 새 폴더를 만들고 이름을 **Services**로 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-221">Create a new folder in the solution root and name it **Services**.</span></span> <span data-ttu-id="cc703-222">이렇게 하려면 프로젝트 **관리자** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가** | **새 폴더**를 선택한 다음 이름으로 *서비스*를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-222">To do this, right-click **ContactManager** project, select **Add** | **New Folder**, name it *Services*.</span></span>

    <span data-ttu-id="cc703-223">![서비스 폴더를 만드는 중](build-restful-apis-with-aspnet-web-api/_static/image14.png "서비스 폴더를 만드는 중")</span><span class="sxs-lookup"><span data-stu-id="cc703-223">![Creating Services folder](build-restful-apis-with-aspnet-web-api/_static/image14.png "Creating Services folder")</span></span>

    <span data-ttu-id="cc703-224">*서비스 폴더를 만드는 중*</span><span class="sxs-lookup"><span data-stu-id="cc703-224">*Creating Services folder*</span></span>
2. <span data-ttu-id="cc703-225">**서비스** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 클래스 ...** 상황에 맞는 메뉴에서.</span><span class="sxs-lookup"><span data-stu-id="cc703-225">Right-click the **Services** folder and select **Add | Class...** from the context menu.</span></span>

    <span data-ttu-id="cc703-226">![서비스 폴더에 새 클래스 추가](build-restful-apis-with-aspnet-web-api/_static/image15.png "서비스 폴더에 새 클래스 추가")</span><span class="sxs-lookup"><span data-stu-id="cc703-226">![Adding a new class to the Services folder](build-restful-apis-with-aspnet-web-api/_static/image15.png "Adding a new class to the Services folder")</span></span>

    <span data-ttu-id="cc703-227">*서비스 폴더에 새 클래스 추가*</span><span class="sxs-lookup"><span data-stu-id="cc703-227">*Adding a new class to the Services folder*</span></span>
3. <span data-ttu-id="cc703-228">**새 항목 추가** 대화 상자가 나타나면 **새 클래스의** 이름을 같은 이름으로 만들고 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-228">When the **Add New Item** dialog appears, name the new class **ContactRepository** and click **Add**.</span></span>

    <span data-ttu-id="cc703-229">![연락처 리포지토리 서비스 계층에 대 한 코드를 포함 하는 클래스 파일 만들기](build-restful-apis-with-aspnet-web-api/_static/image16.png "연락처 리포지토리 서비스 계층에 대 한 코드를 포함 하는 클래스 파일 만들기")</span><span class="sxs-lookup"><span data-stu-id="cc703-229">![Creating a class file to contain the code for the Contact Repository service layer](build-restful-apis-with-aspnet-web-api/_static/image16.png "Creating a class file to contain the code for the Contact Repository service layer")</span></span>

    <span data-ttu-id="cc703-230">*연락처 리포지토리 서비스 계층에 대 한 코드를 포함 하는 클래스 파일 만들기*</span><span class="sxs-lookup"><span data-stu-id="cc703-230">*Creating a class file to contain the code for the Contact Repository service layer*</span></span>
4. <span data-ttu-id="cc703-231">**ContactRepository.cs** 파일에 using 지시문을 추가 하 여 모델 네임 스페이스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-231">Add a using directive to the **ContactRepository.cs** file to include the models namespace.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample4.cs)]
5. <span data-ttu-id="cc703-232">**ContactRepository.cs** 파일에 다음 강조 표시 된 코드를 추가 하 여 GetAllContacts 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-232">Add the following highlighted code to the **ContactRepository.cs** file to implement GetAllContacts method.</span></span>

    <span data-ttu-id="cc703-233">(코드 조각- *웹 API 랩-Ex01-연락처 리포지토리*)</span><span class="sxs-lookup"><span data-stu-id="cc703-233">(Code Snippet - *Web API Lab - Ex01 - Contact Repository*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample5.cs)]
6. <span data-ttu-id="cc703-234">**ContactController.cs** 파일이 아직 열려 있지 않으면 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-234">Open the **ContactController.cs** file if it is not already open.</span></span>
7. <span data-ttu-id="cc703-235">다음 using 문을 파일의 네임 스페이스 선언 섹션에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-235">Add the following using statement to the namespace declaration section of the file.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample6.cs)]
8. <span data-ttu-id="cc703-236">**ContactController.cs** 클래스에 다음 강조 표시 된 코드를 추가 하 여 나머지 클래스 멤버가 서비스 구현을 사용할 수 있도록 전용 필드를 리포지토리의 인스턴스를 나타내는 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-236">Add the following highlighted code to the **ContactController.cs** class to add a private field to represent the instance of the repository, so that the rest of the class members can make use of the service implementation.</span></span>

    <span data-ttu-id="cc703-237">(코드 조각- *WEB API Lab-Ex01-Contact Controller*)</span><span class="sxs-lookup"><span data-stu-id="cc703-237">(Code Snippet - *Web API Lab - Ex01 - Contact Controller*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample7.cs)]
9. <span data-ttu-id="cc703-238">연락처 리포지토리 서비스를 사용 하도록 **Get** 메서드를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-238">Change the **Get** method so that it makes use of the contact repository service.</span></span>

    <span data-ttu-id="cc703-239">(코드 조각- *WEB API Lab-Ex01-리포지토리를 통해 연락처 목록 반환*)</span><span class="sxs-lookup"><span data-stu-id="cc703-239">(Code Snippet - *Web API Lab - Ex01 - Returning a list of contacts via the repository*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample8.cs)]
10. <span data-ttu-id="cc703-240">**연락처 컨트롤러**의 **Get** 메서드 정의에 중단점을 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-240">Put a breakpoint on the **ContactController**'s **Get** method definition.</span></span>

   <span data-ttu-id="cc703-241">![Contact controller에 중단점 추가](build-restful-apis-with-aspnet-web-api/_static/image17.png "Contact controller에 중단점 추가")</span><span class="sxs-lookup"><span data-stu-id="cc703-241">![Adding breakpoints to the contact controller](build-restful-apis-with-aspnet-web-api/_static/image17.png "Adding breakpoints to the contact controller")</span></span>

   <span data-ttu-id="cc703-242">*Contact controller에 중단점 추가*</span><span class="sxs-lookup"><span data-stu-id="cc703-242">*Adding breakpoints to the contact controller*</span></span>
11. <span data-ttu-id="cc703-243">**F5** 키를 눌러 애플리케이션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-243">Press **F5** to run the application.</span></span>
12. <span data-ttu-id="cc703-244">브라우저가 열리면 **F12** 키를 눌러 개발자 도구를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-244">When the browser opens, press **F12** to open the developer tools.</span></span>
13. <span data-ttu-id="cc703-245">**네트워크** 탭을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-245">Click the **Network** tab.</span></span>
14. <span data-ttu-id="cc703-246">**캡처 시작** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-246">Click the **Start Capturing** button.</span></span>
15. <span data-ttu-id="cc703-247">주소 표시줄에 URL을 suffix **/api/contact** 와 함께 추가 하 고 **enter** 키를 눌러 api 컨트롤러를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-247">Append the URL in the address bar with the suffix **/api/contact** and press **Enter** to load the API controller.</span></span>
16. <span data-ttu-id="cc703-248">**Get** 메서드가 실행을 시작 하면 Visual Studio 2012가 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-248">Visual Studio 2012 should break once **Get** method begins execution.</span></span>

   <span data-ttu-id="cc703-249">![Get 메서드 내에서 중단](build-restful-apis-with-aspnet-web-api/_static/image18.png "Get 메서드 내에서 중단")</span><span class="sxs-lookup"><span data-stu-id="cc703-249">![Breaking within the Get method](build-restful-apis-with-aspnet-web-api/_static/image18.png "Breaking within the Get method")</span></span>

   <span data-ttu-id="cc703-250">*Get 메서드 내에서 중단*</span><span class="sxs-lookup"><span data-stu-id="cc703-250">*Breaking within the Get method*</span></span>
17. <span data-ttu-id="cc703-251">계속하려면 **F5** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-251">Press **F5** to continue.</span></span>
18. <span data-ttu-id="cc703-252">아직 포커스가 없는 경우 Internet Explorer로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-252">Go back to Internet Explorer if it is not already in focus.</span></span> <span data-ttu-id="cc703-253">네트워크 캡처 창을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-253">Note the network capture window.</span></span>

    <span data-ttu-id="cc703-254">![웹 API 호출의 결과를 표시 하는 Internet Explorer의 네트워크 보기](build-restful-apis-with-aspnet-web-api/_static/image19.png "웹 API 호출의 결과를 표시 하는 Internet Explorer의 네트워크 보기")</span><span class="sxs-lookup"><span data-stu-id="cc703-254">![Network view in Internet Explorer showing results of the Web API call](build-restful-apis-with-aspnet-web-api/_static/image19.png "Network view in Internet Explorer showing results of the Web API call")</span></span>

    <span data-ttu-id="cc703-255">*웹 API 호출의 결과를 표시 하는 Internet Explorer의 네트워크 보기*</span><span class="sxs-lookup"><span data-stu-id="cc703-255">*Network view in Internet Explorer showing results of the Web API call*</span></span>
19. <span data-ttu-id="cc703-256">**자세히 보기로 이동** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-256">Click the **Go to detailed view** button.</span></span>
20. <span data-ttu-id="cc703-257">**응답 본문** 탭을 클릭 합니다. API 호출의 JSON 출력과 서비스 계층에서 검색 된 두 개의 연락처를 나타내는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-257">Click the **Response body** tab. Note the JSON output of the API call, and how it represents the two contacts retrieved by the service layer.</span></span>

    <span data-ttu-id="cc703-258">![개발자 도구 창에서 Web API의 JSON 출력 보기](build-restful-apis-with-aspnet-web-api/_static/image20.png "개발자 도구 창에서 Web API의 JSON 출력 보기")</span><span class="sxs-lookup"><span data-stu-id="cc703-258">![Viewing the JSON output from the Web API in the developer tools window](build-restful-apis-with-aspnet-web-api/_static/image20.png "Viewing the JSON output from the Web API in the developer tools window")</span></span>

    <span data-ttu-id="cc703-259">*개발자 도구 창에서 Web API의 JSON 출력 보기*</span><span class="sxs-lookup"><span data-stu-id="cc703-259">*Viewing the JSON output from the Web API in the developer tools window*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Create_a_ReadWrite_Web_API"></a>
### <a name="exercise-2-create-a-readwrite-web-api"></a><span data-ttu-id="cc703-260">연습 2: 읽기/쓰기 웹 API 만들기</span><span class="sxs-lookup"><span data-stu-id="cc703-260">Exercise 2: Create a Read/Write Web API</span></span>

<span data-ttu-id="cc703-261">이 연습에서는 데이터 편집 기능을 사용 하도록 설정 하기 위해 contact manager의 POST 및 PUT 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-261">In this exercise, you will implement POST and PUT methods for the contact manager to enable it with data-editing features.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Opening_the_Web_API_Project"></a>
#### <a name="task-1---opening-the-web-api-project"></a><span data-ttu-id="cc703-262">작업 1-웹 API 프로젝트 열기</span><span class="sxs-lookup"><span data-stu-id="cc703-262">Task 1 - Opening the Web API Project</span></span>

<span data-ttu-id="cc703-263">이 작업에서는 사용자 입력을 허용할 수 있도록 실습 1에서 만든 웹 API 프로젝트를 향상 시킬 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-263">In this task, you will prepare to enhance the Web API project created in Exercise 1 so that it can accept user input.</span></span>

1. <span data-ttu-id="cc703-264">**Visual Studio 2012 Express For Web**을 실행 하 여 **시작** 으로 이동 하 **VS Express for Web** 입력 한 다음 **enter**키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-264">Run **Visual Studio 2012 Express for Web**, to do this go to **Start** and type **VS Express for Web** then press **Enter**.</span></span>
2. <span data-ttu-id="cc703-265">**Source/Ex02-ReadWriteWebAPI/begin/** 폴더에 있는 **시작** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-265">Open the **Begin** solution located at **Source/Ex02-ReadWriteWebAPI/Begin/** folder.</span></span> <span data-ttu-id="cc703-266">그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-266">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="cc703-267">제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-267">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="cc703-268">이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-268">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="cc703-269">**NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-269">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="cc703-270">마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-270">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="cc703-271">NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-271">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="cc703-272">NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-272">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="cc703-273">이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-273">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="cc703-274">**서비스/연락처 리포지토리의 .cs** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-274">Open the **Services/ContactRepository.cs** file.</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Adding_Data-Persistence_Features_to_the_Contact_Repository_Implementation"></a>
#### <a name="task-2---adding-data-persistence-features-to-the-contact-repository-implementation"></a><span data-ttu-id="cc703-275">작업 2-연락처 리포지토리 구현에 데이터 지 속성 기능 추가</span><span class="sxs-lookup"><span data-stu-id="cc703-275">Task 2 - Adding Data-Persistence Features to the Contact Repository Implementation</span></span>

<span data-ttu-id="cc703-276">이 작업에서는 사용자 입력 및 새 연락처 인스턴스를 유지 하 고 허용할 수 있도록 연습 1에서 만든 Web API 프로젝트의 지 수 리포지토리 클래스를 확대 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-276">In this task, you will augment the ContactRepository class of the Web API project created in Exercise 1 so that it can persist and accept user input and new Contact instances.</span></span>

1. <span data-ttu-id="cc703-277">이 연습 뒷부분의 웹 서버 캐시 항목 키 이름 이름을 나타내는 다음 상수를 **연락처 리포지토리** 클래스에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-277">Add the following constant to the **ContactRepository** class to represent the name of the web server cache item key name later in this exercise.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample9.cs)]
2. <span data-ttu-id="cc703-278">다음 코드를 포함 하는 **연락처 리포지토리에** 생성자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-278">Add a constructor to the **ContactRepository** containing the following code.</span></span>

    <span data-ttu-id="cc703-279">(코드 조각- *WEB API Lab-Ex02 리포지토리 생성자*)</span><span class="sxs-lookup"><span data-stu-id="cc703-279">(Code Snippet - *Web API Lab - Ex02 - Contact Repository Constructor*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample10.cs)]
3. <span data-ttu-id="cc703-280">아래와 같이 **Getallcontacts** 메서드에 대 한 코드를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-280">Modify the code for the **GetAllContacts** method as demonstrated below.</span></span>

    <span data-ttu-id="cc703-281">(코드 조각- *WEB API Lab-Ex02-모든 연락처 가져오기*)</span><span class="sxs-lookup"><span data-stu-id="cc703-281">(Code Snippet - *Web API Lab - Ex02 - Get All Contacts*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample11.cs)]

    > [!NOTE]
    > <span data-ttu-id="cc703-282">이 예제는 데모용 이며, 웹 서버의 캐시를 저장 미디어로 사용 하므로 세션 저장소 메커니즘 또는 요청 저장소 수명을 사용 하지 않고 여러 클라이언트에서 동시에 값을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-282">This example is for demonstration purposes and will use the web server's cache as a storage medium, so that the values will be available to multiple clients simultaneously, rather than use a Session storage mechanism or a Request storage lifetime.</span></span> <span data-ttu-id="cc703-283">Entity Framework, XML 저장소 또는 웹 서버 캐시를 사용 하는 기타 다양 한 항목을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-283">One could use Entity Framework, XML storage, or any other variety in place of the web server cache.</span></span>
4. <span data-ttu-id="cc703-284">연락처를 저장 하는 작업을 수행 하려면 **SaveContact** 이라는 새 메서드를 지 수 **리포지토리** 클래스에 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-284">Implement a new method named **SaveContact** to the **ContactRepository** class to do the work of saving a contact.</span></span> <span data-ttu-id="cc703-285">**SaveContact** 메서드는 단일 **연락** 매개 변수를 사용 하 고 성공 또는 실패를 나타내는 부울 값을 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-285">The **SaveContact** method should take a single **Contact** parameter and return a Boolean value indicating success or failure.</span></span>

    <span data-ttu-id="cc703-286">(코드 조각- *WEB API Lab-Ex02-SaveContact 메서드 구현*)</span><span class="sxs-lookup"><span data-stu-id="cc703-286">(Code Snippet - *Web API Lab - Ex02 - Implementing the SaveContact Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample12.cs)]

<a id="Exercise3"></a>

<a id="Exercise_3_Consume_the_Web_API_from_an_HTML_Client"></a>
### <a name="exercise-3-consume-the-web-api-from-an-html-client"></a><span data-ttu-id="cc703-287">연습 3: HTML 클라이언트에서 Web API 사용</span><span class="sxs-lookup"><span data-stu-id="cc703-287">Exercise 3: Consume the Web API from an HTML Client</span></span>

<span data-ttu-id="cc703-288">이 연습에서는 Web API를 호출 하는 HTML 클라이언트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-288">In this exercise, you will create an HTML client to call the Web API.</span></span> <span data-ttu-id="cc703-289">이 클라이언트는 JavaScript를 사용 하 여 Web API와의 데이터 교환을 용이 하 게 하 고 HTML 태그를 사용 하 여 웹 브라우저에 결과를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-289">This client will facilitate data exchange with the Web API using JavaScript and will display the results in a web browser using HTML markup.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Displaying_Contacts"></a>
#### <a name="task-1---modifying-the-index-view-to-provide-a-gui-for-displaying-contacts"></a><span data-ttu-id="cc703-290">작업 1-연락처 표시를 위한 GUI를 제공 하도록 인덱스 뷰 수정</span><span class="sxs-lookup"><span data-stu-id="cc703-290">Task 1 - Modifying the Index View to Provide a GUI for Displaying Contacts</span></span>

<span data-ttu-id="cc703-291">이 태스크에서는 HTML 브라우저에서 기존 연락처 목록을 표시 하기 위한 요구 사항을 지원 하도록 웹 응용 프로그램의 기본 인덱스 뷰를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-291">In this task, you will modify the default Index view of the web application to support the requirement of displaying the list of existing contacts in an HTML browser.</span></span>

1. <span data-ttu-id="cc703-292">아직 열려 있지 않은 경우 **Visual Studio 2012 Express For Web을** 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-292">Open **Visual Studio 2012 Express for Web** if it is not already open.</span></span>
2. <span data-ttu-id="cc703-293">**Source/Ex03-ConsumingWebAPI/begin/** 폴더에 있는 **시작** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-293">Open the **Begin** solution located at **Source/Ex03-ConsumingWebAPI/Begin/** folder.</span></span> <span data-ttu-id="cc703-294">그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-294">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="cc703-295">제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-295">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="cc703-296">이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-296">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="cc703-297">**NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-297">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="cc703-298">마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-298">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="cc703-299">NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-299">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="cc703-300">NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-300">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="cc703-301">이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-301">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="cc703-302">**뷰/홈** 폴더에 있는 **인덱스 cshtml** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-302">Open the **Index.cshtml** file located at **Views/Home** folder.</span></span>
4. <span data-ttu-id="cc703-303">Div 요소 내에 있는 HTML 코드를 다음 코드와 같이 id **본문** 으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-303">Replace the HTML code within the div element with id **body** so that it looks like the following code.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample13.html)]
5. <span data-ttu-id="cc703-304">다음 Javascript 코드를 파일의 맨 아래에 추가 하 여 웹 API에 대 한 HTTP 요청을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-304">Add the following Javascript code at the bottom of the file to perform the HTTP request to the Web API.</span></span>

    [!code-cshtml[Main](build-restful-apis-with-aspnet-web-api/samples/sample14.cshtml)]
6. <span data-ttu-id="cc703-305">**ContactController.cs** 파일이 아직 열려 있지 않으면 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-305">Open the **ContactController.cs** file if it is not already open.</span></span>
7. <span data-ttu-id="cc703-306">**연락처 컨트롤러** 클래스의 **Get** 메서드에 중단점을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-306">Place a breakpoint on the **Get** method of the **ContactController** class.</span></span>

    <span data-ttu-id="cc703-307">![API 컨트롤러의 Get 메서드에 중단점 배치](build-restful-apis-with-aspnet-web-api/_static/image21.png "API 컨트롤러의 Get 메서드에 중단점 배치")</span><span class="sxs-lookup"><span data-stu-id="cc703-307">![Placing a breakpoint on the Get method of the API controller](build-restful-apis-with-aspnet-web-api/_static/image21.png "Placing a breakpoint on the Get method of the API controller")</span></span>

    <span data-ttu-id="cc703-308">*API 컨트롤러의 Get 메서드에 중단점 배치*</span><span class="sxs-lookup"><span data-stu-id="cc703-308">*Placing a breakpoint on the Get method of the API controller*</span></span>
8. <span data-ttu-id="cc703-309">**F5** 키를 눌러 프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-309">Press **F5** to run the project.</span></span> <span data-ttu-id="cc703-310">브라우저에서 HTML 문서를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-310">The browser will load the HTML document.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cc703-311">응용 프로그램의 루트 URL을 탐색 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-311">Ensure that you are browsing to the root URL of your application.</span></span>
9. <span data-ttu-id="cc703-312">페이지가 로드 되 고 JavaScript가 실행 되 면 중단점에 도달 하 고 컨트롤러에서 코드 실행이 일시 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-312">Once the page loads and the JavaScript executes, the breakpoint will be hit and the code execution will pause in the controller.</span></span>

    <span data-ttu-id="cc703-313">![VS Express for Web를 사용 하 여 웹 API 호출 디버깅](build-restful-apis-with-aspnet-web-api/_static/image22.png "VS Express for Web를 사용 하 여 웹 API 호출 디버깅")</span><span class="sxs-lookup"><span data-stu-id="cc703-313">![Debugging into the Web API calls using VS Express for Web](build-restful-apis-with-aspnet-web-api/_static/image22.png "Debugging into the Web API calls using VS Express for Web")</span></span>

    <span data-ttu-id="cc703-314">*Visual Studio 2012 Express for Web을 사용 하 여 웹 API 호출로 디버깅*</span><span class="sxs-lookup"><span data-stu-id="cc703-314">*Debugging into the Web API call using Visual Studio 2012 Express for Web*</span></span>
10. <span data-ttu-id="cc703-315">중단점을 제거 하 고 **F5** 키를 누르거나 디버그 도구 모음의 **계속** 단추를 클릭 하 여 브라우저에서 보기를 계속 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-315">Remove the breakpoint and press **F5** or the debugging toolbar's **Continue** button to continue loading the view in the browser.</span></span> <span data-ttu-id="cc703-316">웹 API 호출이 완료 되 면 브라우저에서 목록 항목으로 표시 되는 웹 API 호출에서 반환 된 연락처가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-316">Once the Web API call completes you should see the contacts returned from the Web API call displayed as list items in the browser.</span></span>

    <span data-ttu-id="cc703-317">![브라우저에 목록 항목으로 표시 되는 API 호출의 결과](build-restful-apis-with-aspnet-web-api/_static/image23.png "브라우저에 목록 항목으로 표시 되는 API 호출의 결과")</span><span class="sxs-lookup"><span data-stu-id="cc703-317">![Results of the API call displayed in the browser as list items](build-restful-apis-with-aspnet-web-api/_static/image23.png "Results of the API call displayed in the browser as list items")</span></span>

    <span data-ttu-id="cc703-318">*브라우저에 목록 항목으로 표시 되는 API 호출의 결과*</span><span class="sxs-lookup"><span data-stu-id="cc703-318">*Results of the API call displayed in the browser as list items*</span></span>
11. <span data-ttu-id="cc703-319">디버깅을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-319">Stop debugging.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Creating_Contacts"></a>
#### <a name="task-2---modifying-the-index-view-to-provide-a-gui-for-creating-contacts"></a><span data-ttu-id="cc703-320">작업 2-연락처를 만들기 위한 GUI를 제공 하도록 인덱스 보기 수정</span><span class="sxs-lookup"><span data-stu-id="cc703-320">Task 2 - Modifying the Index View to Provide a GUI for Creating Contacts</span></span>

<span data-ttu-id="cc703-321">이 태스크에서는 MVC 응용 프로그램의 인덱스 뷰를 계속 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-321">In this task, you will continue to modify the Index view of the MVC application.</span></span> <span data-ttu-id="cc703-322">사용자 입력을 캡처하고 웹 API로 보내서 새 연락처를 만드는 양식이 HTML 페이지에 추가 되 고, GUI에서 날짜를 수집 하기 위해 새 Web API 컨트롤러 메서드가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-322">A form will be added to the HTML page that will capture user input and send it to the Web API to create a new Contact, and a new Web API controller method will be created to collect date from the GUI.</span></span>

1. <span data-ttu-id="cc703-323">**ContactController.cs** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-323">Open the **ContactController.cs** file.</span></span>
2. <span data-ttu-id="cc703-324">다음 코드와 같이 **Post** 라는 컨트롤러 클래스에 새 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-324">Add a new method to the controller class named **Post** as shown in the following code.</span></span>

    <span data-ttu-id="cc703-325">(코드 조각- *WEB API 랩-Ex03-Post 메서드*)</span><span class="sxs-lookup"><span data-stu-id="cc703-325">(Code Snippet - *Web API Lab - Ex03 - Post Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample15.cs)]
3. <span data-ttu-id="cc703-326">아직 열려 있지 않은 경우 Visual Studio에서 **이 파일을 엽니다.**</span><span class="sxs-lookup"><span data-stu-id="cc703-326">Open the **Index.cshtml** file in Visual Studio if it is not already open.</span></span>
4. <span data-ttu-id="cc703-327">이전 작업에서 추가한 순서가 지정 되지 않은 목록 바로 뒤의 파일에 아래 HTML 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-327">Add the HTML code below to the file just after the unordered list you added in the previous task.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample16.html)]
5. <span data-ttu-id="cc703-328">문서 아래쪽의 script 요소 내에서 다음 강조 표시 된 코드를 추가 하 여 단추 클릭 이벤트를 처리 합니다. 그러면 HTTP POST 호출을 사용 하 여 Web API에 데이터를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-328">Within the script element at the bottom of the document, add the following highlighted code to handle button-click events, which will post the data to the Web API using an HTTP POST call.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample17.html)]
6. <span data-ttu-id="cc703-329">**ContactController.cs**에서 **Post** 메서드에 중단점을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-329">In **ContactController.cs**, place a breakpoint on the **Post** method.</span></span>
7. <span data-ttu-id="cc703-330">브라우저에서 응용 프로그램을 실행 하려면 **f5** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-330">Press **F5** to run the application in the browser.</span></span>
8. <span data-ttu-id="cc703-331">페이지가 브라우저에 로드 되 면 새 연락처 이름 및 Id를 입력 하 고 **저장** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-331">Once the page is loaded in the browser, type in a new contact name and Id and click the **Save** button.</span></span>

    <span data-ttu-id="cc703-332">![브라우저에 로드 된 클라이언트 HTML 문서](build-restful-apis-with-aspnet-web-api/_static/image24.png "브라우저에 로드 된 클라이언트 HTML 문서")</span><span class="sxs-lookup"><span data-stu-id="cc703-332">![The client HTML document loaded in the browser](build-restful-apis-with-aspnet-web-api/_static/image24.png "The client HTML document loaded in the browser")</span></span>

    <span data-ttu-id="cc703-333">*브라우저에 로드 된 클라이언트 HTML 문서*</span><span class="sxs-lookup"><span data-stu-id="cc703-333">*The client HTML document loaded in the browser*</span></span>
9. <span data-ttu-id="cc703-334">**Post** 메서드에서 디버거 창이 중단 되 면 **contact** 매개 변수의 속성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-334">When the debugger window breaks in the **Post** method, take a look at the properties of the **contact** parameter.</span></span> <span data-ttu-id="cc703-335">값은 폼에 입력 한 데이터와 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-335">The values should match the data you entered in the form.</span></span>

    <span data-ttu-id="cc703-336">![클라이언트에서 Web API로 전송 되는 Contact 개체입니다.](build-restful-apis-with-aspnet-web-api/_static/image25.png "클라이언트에서 Web API로 전송 되는 Contact 개체입니다.")</span><span class="sxs-lookup"><span data-stu-id="cc703-336">![The Contact object being sent to the Web API from the client](build-restful-apis-with-aspnet-web-api/_static/image25.png "The Contact object being sent to the Web API from the client")</span></span>

    <span data-ttu-id="cc703-337">*클라이언트에서 Web API로 전송 되는 Contact 개체입니다.*</span><span class="sxs-lookup"><span data-stu-id="cc703-337">*The Contact object being sent to the Web API from the client*</span></span>
10. <span data-ttu-id="cc703-338">**응답** 변수를 만들 때까지 디버거의 메서드를 단계별로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-338">Step through the method in the debugger until the **response** variable has been created.</span></span> <span data-ttu-id="cc703-339">디버거의 **지역** 창에서 검사 하면 모든 속성이 설정 된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-339">Upon inspection in the **Locals** window in the debugger, you'll see that all the properties have been set.</span></span>

   <span data-ttu-id="cc703-340">![디버거에서 만든 다음 응답](build-restful-apis-with-aspnet-web-api/_static/image26.png "디버거에서 만든 다음 응답")</span><span class="sxs-lookup"><span data-stu-id="cc703-340">![The response following creation in the debugger](build-restful-apis-with-aspnet-web-api/_static/image26.png "The response following creation in the debugger")</span></span>

   <span data-ttu-id="cc703-341">*디버거에서 만든 다음 응답*</span><span class="sxs-lookup"><span data-stu-id="cc703-341">*The response following creation in the debugger*</span></span>
11. <span data-ttu-id="cc703-342">**F5** 키를 누르거나 디버거에서 **계속** 을 클릭 하면 요청이 완료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-342">If you press **F5** or click **Continue** in the debugger the request will complete.</span></span> <span data-ttu-id="cc703-343">브라우저로 다시 전환 하면 새 연락처가 연락처 **리포지토리** 구현에 의해 저장 된 연락처 목록에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-343">Once you switch back to the browser, the new contact has been added to the list of contacts stored by the **ContactRepository** implementation.</span></span>

   <span data-ttu-id="cc703-344">![브라우저에서 새 연락처 인스턴스가 성공적으로 생성 된 것을 반영 합니다.](build-restful-apis-with-aspnet-web-api/_static/image27.png "브라우저에서 새 연락처 인스턴스가 성공적으로 생성 된 것을 반영 합니다.")</span><span class="sxs-lookup"><span data-stu-id="cc703-344">![The browser reflects successful creation of the new contact instance](build-restful-apis-with-aspnet-web-api/_static/image27.png "The browser reflects successful creation of the new contact instance")</span></span>

   <span data-ttu-id="cc703-345">*브라우저에서 새 연락처 인스턴스가 성공적으로 생성 된 것을 반영 합니다.*</span><span class="sxs-lookup"><span data-stu-id="cc703-345">*The browser reflects successful creation of the new contact instance*</span></span>

> [!NOTE]
> <span data-ttu-id="cc703-346">또한 웹 배포를 사용 하 여이 응용 프로그램을 Azure에 배포할 수 있습니다 [. 부록 C: ASP.NET MVC 4 응용 프로그램 게시.](#AppendixC)</span><span class="sxs-lookup"><span data-stu-id="cc703-346">Additionally, you can deploy this application to Azure following [Appendix C: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixC).</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="cc703-347">요약</span><span class="sxs-lookup"><span data-stu-id="cc703-347">Summary</span></span>

<span data-ttu-id="cc703-348">이 랩에서는 새로운 ASP.NET Web API 프레임 워크 및 프레임 워크를 사용 하 여 RESTful Web Api의 구현에 대해 소개 했습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-348">This lab has introduced you to the new ASP.NET Web API framework and to the implementation of RESTful Web APIs using the framework.</span></span> <span data-ttu-id="cc703-349">여기에서 다양 한 메커니즘을 사용 하 여 데이터 지 속성을 용이 하 게 하 고이 랩에서 예제로 제공 되는 간단한 것이 아니라 서비스를 제공 하는 새 리포지토리를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-349">From here, you could create a new repository that facilitates data persistence using any number of mechanisms and wire that service up rather than the simple one provided as an example in this lab.</span></span> <span data-ttu-id="cc703-350">Web API는 HTTP 및 JSON 또는 XML을 지 원하는 언어로 작성 된 비 HTML 클라이언트 로부터의 통신을 사용 하도록 설정 하는 등의 다양 한 추가 기능을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-350">Web API supports a number of additional features, such as enabling communication from non-HTML clients written in any language that supports HTTP and JSON or XML.</span></span> <span data-ttu-id="cc703-351">일반적인 웹 응용 프로그램 외부에서 Web API를 호스트 하는 기능을 사용할 수도 있으며 사용자 고유의 serialization 형식을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-351">The ability to host a Web API outside of a typical web application is also possible, as well as is the ability to create your own serialization formats.</span></span>

<span data-ttu-id="cc703-352">ASP.NET 웹 사이트에는 [[https://asp.net/web-api](https://asp.net/web-api)](https://asp.net/web-api)ASP.NET Web API 프레임 워크 전용 영역이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-352">The ASP.NET Web site has an area dedicated to the ASP.NET Web API framework at [[https://asp.net/web-api](https://asp.net/web-api)](https://asp.net/web-api).</span></span> <span data-ttu-id="cc703-353">이 사이트는 Web API와 관련 된 최신 정보, 샘플 및 뉴스를 계속 제공 하므로, 거의 모든 장치 또는 개발 프레임 워크에서 사용할 수 있는 사용자 지정 웹 Api를 만드는 데 더 자세히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-353">This site will continue to provide late-breaking information, samples, and news related to Web API, so check it frequently if you'd like to delve deeper into the art of creating custom Web APIs available to virtually any device or development framework.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a><span data-ttu-id="cc703-354">부록 A: 코드 조각 사용</span><span class="sxs-lookup"><span data-stu-id="cc703-354">Appendix A: Using Code Snippets</span></span>

<span data-ttu-id="cc703-355">코드 조각을 사용 하면 필요한 모든 코드를 편리 하 게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-355">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="cc703-356">랩 문서는 다음 그림에 표시 된 것 처럼 사용자가 사용할 수 있는 경우를 정확 하 게 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-356">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="cc703-357">![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입](build-restful-apis-with-aspnet-web-api/_static/image28.png "Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입")</span><span class="sxs-lookup"><span data-stu-id="cc703-357">![Using Visual Studio code snippets to insert code into your project](build-restful-apis-with-aspnet-web-api/_static/image28.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="cc703-358">*Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입*</span><span class="sxs-lookup"><span data-stu-id="cc703-358">*Using Visual Studio code snippets to insert code into your project*</span></span>

<a id="CodeSnippetUsingKeyBoard"></a>

<a id="To_add_a_code_snippet_using_the_keyboard_C_only"></a>
### <a name="to-add-a-code-snippet-using-the-keyboard-c-only"></a><span data-ttu-id="cc703-359">키보드를 사용 하 여 코드 조각을 추가 하려면C# (만 해당)</span><span class="sxs-lookup"><span data-stu-id="cc703-359">To add a code snippet using the keyboard (C# only)</span></span>

1. <span data-ttu-id="cc703-360">코드를 삽입할 위치에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-360">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="cc703-361">조각 이름 (공백 또는 하이픈 제외)을 입력 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-361">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="cc703-362">IntelliSense는 일치 하는 코드 조각의 이름을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-362">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="cc703-363">올바른 코드 조각을 선택 하거나 전체 코드 조각 이름이 선택 될 때까지 계속 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-363">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="cc703-364">Tab 키를 두 번 눌러 커서 위치에 코드 조각을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-364">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

    <span data-ttu-id="cc703-365">![코드 조각 이름 입력 시작](build-restful-apis-with-aspnet-web-api/_static/image29.png "코드 조각 이름 입력 시작")</span><span class="sxs-lookup"><span data-stu-id="cc703-365">![Start typing the snippet name](build-restful-apis-with-aspnet-web-api/_static/image29.png "Start typing the snippet name")</span></span>

    <span data-ttu-id="cc703-366">*코드 조각 이름 입력 시작*</span><span class="sxs-lookup"><span data-stu-id="cc703-366">*Start typing the snippet name*</span></span>

    <span data-ttu-id="cc703-367">![Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.](build-restful-apis-with-aspnet-web-api/_static/image30.png "Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="cc703-367">![Press Tab to select the highlighted snippet](build-restful-apis-with-aspnet-web-api/_static/image30.png "Press Tab to select the highlighted snippet")</span></span>

    <span data-ttu-id="cc703-368">*Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="cc703-368">*Press Tab to select the highlighted snippet*</span></span>

    <span data-ttu-id="cc703-369">![Tab 키를 다시 누르면 코드 조각이 확장 됩니다.](build-restful-apis-with-aspnet-web-api/_static/image31.png "Tab 키를 다시 누르면 코드 조각이 확장 됩니다.")</span><span class="sxs-lookup"><span data-stu-id="cc703-369">![Press Tab again and the snippet will expand](build-restful-apis-with-aspnet-web-api/_static/image31.png "Press Tab again and the snippet will expand")</span></span>

    <span data-ttu-id="cc703-370">*Tab 키를 다시 누르면 코드 조각이 확장 됩니다.*</span><span class="sxs-lookup"><span data-stu-id="cc703-370">*Press Tab again and the snippet will expand*</span></span>

<a id="CodeSnippetUsingMouse"></a>

<a id="To_add_a_code_snippet_using_the_mouse_C_Visual_Basic_and_XML"></a>
### <a name="to-add-a-code-snippet-using-the-mouse-c-visual-basic-and-xml"></a><span data-ttu-id="cc703-371">마우스 (C#, VISUAL BASIC 및 XML)를 사용 하 여 코드 조각을 추가 하려면</span><span class="sxs-lookup"><span data-stu-id="cc703-371">To add a code snippet using the mouse (C#, Visual Basic and XML)</span></span>

1. <span data-ttu-id="cc703-372">코드 조각을 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-372">Right-click where you want to insert the code snippet.</span></span>
2. <span data-ttu-id="cc703-373">코드 **조각 삽입** 을 선택한 다음 **내 코드 조각을**선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-373">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
3. <span data-ttu-id="cc703-374">목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-374">Pick the relevant snippet from the list, by clicking on it.</span></span>

    <span data-ttu-id="cc703-375">![코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.](build-restful-apis-with-aspnet-web-api/_static/image32.png "코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="cc703-375">![Right-click where you want to insert the code snippet and select Insert Snippet](build-restful-apis-with-aspnet-web-api/_static/image32.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

    <span data-ttu-id="cc703-376">*코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="cc703-376">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

    <span data-ttu-id="cc703-377">![목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.](build-restful-apis-with-aspnet-web-api/_static/image33.png "목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="cc703-377">![Pick the relevant snippet from the list, by clicking on it](build-restful-apis-with-aspnet-web-api/_static/image33.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

    <span data-ttu-id="cc703-378">*목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="cc703-378">*Pick the relevant snippet from the list, by clicking on it*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="cc703-379">부록 B: 웹에 대 한 Visual Studio Express 2012 설치</span><span class="sxs-lookup"><span data-stu-id="cc703-379">Appendix B: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="cc703-380">**[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)** 를 사용 하 여 웹 또는 다른 &quot;Express&quot; 버전 **에 대해 Microsoft Visual Studio Express 2012** 를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-380">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="cc703-381">다음 지침에서는 *Microsoft 웹 플랫폼 설치 관리자*를 사용 하 여 *Visual studio Express 2012 for Web* 을 설치 하는 데 필요한 단계를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-381">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="cc703-382">[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-382">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="cc703-383">또는 웹 플랫폼 설치 관리자를 이미 설치한 경우에는 웹 플랫폼 설치 관리자를 열고 <em>AZURE SDK&quot;를 사용 하 여 웹 용 2012 Visual Studio Express</em> 제품 &quot;검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-383">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="cc703-384">**지금 설치**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-384">Click on **Install Now**.</span></span> <span data-ttu-id="cc703-385">**웹 플랫폼 설치 관리자** 가 없으면 먼저이를 다운로드 하 여 설치 하도록 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-385">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="cc703-386">**웹 플랫폼 설치 관리자** 가 열리면 **설치** 를 클릭 하 여 설치를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-386">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="cc703-387">![Visual Studio Express 설치](build-restful-apis-with-aspnet-web-api/_static/image34.png "Visual Studio Express 설치")</span><span class="sxs-lookup"><span data-stu-id="cc703-387">![Install Visual Studio Express](build-restful-apis-with-aspnet-web-api/_static/image34.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="cc703-388">*Visual Studio Express 설치*</span><span class="sxs-lookup"><span data-stu-id="cc703-388">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="cc703-389">모든 제품의 라이선스 및 사용 조건을 읽고 **동의** 함을 클릭 하 여 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-389">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![사용 조건 동의](build-restful-apis-with-aspnet-web-api/_static/image35.png)

    <span data-ttu-id="cc703-391">*사용 조건 동의*</span><span class="sxs-lookup"><span data-stu-id="cc703-391">*Accepting the license terms*</span></span>
5. <span data-ttu-id="cc703-392">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-392">Wait until the downloading and installation process completes.</span></span>

    ![설치 진행률](build-restful-apis-with-aspnet-web-api/_static/image36.png)

    <span data-ttu-id="cc703-394">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="cc703-394">*Installation progress*</span></span>
6. <span data-ttu-id="cc703-395">설치가 완료 되 면 **마침**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-395">When the installation completes, click **Finish**.</span></span>

    ![설치 완료](build-restful-apis-with-aspnet-web-api/_static/image37.png)

    <span data-ttu-id="cc703-397">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="cc703-397">*Installation completed*</span></span>
7. <span data-ttu-id="cc703-398">**끝내기** 를 클릭 하 여 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-398">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="cc703-399">웹에 대 한 Visual Studio Express를 열려면 **시작** 화면으로 이동 하 &quot;**VS Express**&quot;작성을 시작한 후 **VS Express for Web** 타일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-399">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 타일](build-restful-apis-with-aspnet-web-api/_static/image38.png)

    <span data-ttu-id="cc703-401">*VS Express for Web 타일*</span><span class="sxs-lookup"><span data-stu-id="cc703-401">*VS Express for Web tile*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-c-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="cc703-402">부록 C: 웹 배포을 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="cc703-402">Appendix C: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="cc703-403">이 부록에서는 azure Portal에서 새 웹 사이트를 만들고 랩에 따라 얻은 응용 프로그램을 게시 하 여 Azure에서 제공 하는 웹 배포 게시 기능을 활용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-403">This appendix will show you how to create a new web site from the Azure Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Azure.</span></span>

<a id="ApxCTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a><span data-ttu-id="cc703-404">작업 1-Azure 포털에서 새 웹 사이트 만들기</span><span class="sxs-lookup"><span data-stu-id="cc703-404">Task 1 - Creating a New Web Site from the Azure Portal</span></span>

1. <span data-ttu-id="cc703-405">[Azure 관리 포털](https://manage.windowsazure.com/) 로 이동 하 고 구독과 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-405">Go to the [Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cc703-406">Azure를 사용 하면 10 개의 ASP.NET 웹 사이트를 무료로 호스팅한 다음 트래픽이 증가 함에 따라 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-406">With Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="cc703-407">[여기](https://aka.ms/aspnet-hol-azure)에서 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-407">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="cc703-408">![Windows Azure Portal에 로그온 합니다.](build-restful-apis-with-aspnet-web-api/_static/image39.png "Windows Azure Portal에 로그온 합니다.")</span><span class="sxs-lookup"><span data-stu-id="cc703-408">![Log on to Windows Azure portal](build-restful-apis-with-aspnet-web-api/_static/image39.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="cc703-409">*포털에 로그온*</span><span class="sxs-lookup"><span data-stu-id="cc703-409">*Log on to Portal*</span></span>
2. <span data-ttu-id="cc703-410">명령 모음에서 **새로 만들기** 를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-410">Click **New** on the command bar.</span></span>

    <span data-ttu-id="cc703-411">![새 웹 사이트 만들기](build-restful-apis-with-aspnet-web-api/_static/image40.png "새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="cc703-411">![Creating a new Web Site](build-restful-apis-with-aspnet-web-api/_static/image40.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="cc703-412">*새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="cc703-412">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="cc703-413">**Compute** | **웹 사이트**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-413">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="cc703-414">그런 다음 **빠른 생성** 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-414">Then select **Quick Create** option.</span></span> <span data-ttu-id="cc703-415">새 웹 사이트에 사용할 수 있는 URL을 제공 하 고 **웹 사이트 만들기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-415">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cc703-416">Azure는 사용자가 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램에 대 한 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-416">Azure is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="cc703-417">빠른 생성 옵션을 사용 하면 포털 외부에서 완료 된 웹 응용 프로그램을 Azure에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-417">The Quick Create option allows you to deploy a completed web application to the Azure from outside the portal.</span></span> <span data-ttu-id="cc703-418">데이터베이스를 설정 하는 단계는 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-418">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="cc703-419">![빠른 생성을 사용 하 여 새 웹 사이트 만들기](build-restful-apis-with-aspnet-web-api/_static/image41.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="cc703-419">![Creating a new Web Site using Quick Create](build-restful-apis-with-aspnet-web-api/_static/image41.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="cc703-420">*빠른 생성을 사용 하 여 새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="cc703-420">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="cc703-421">새 **웹 사이트가** 만들어질 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-421">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="cc703-422">웹 사이트를 만든 후 **URL** 열 아래의 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-422">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="cc703-423">새 웹 사이트가 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-423">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="cc703-424">![새 웹 사이트로 이동](build-restful-apis-with-aspnet-web-api/_static/image42.png "새 웹 사이트로 이동")</span><span class="sxs-lookup"><span data-stu-id="cc703-424">![Browsing to the new web site](build-restful-apis-with-aspnet-web-api/_static/image42.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="cc703-425">*새 웹 사이트로 이동*</span><span class="sxs-lookup"><span data-stu-id="cc703-425">*Browsing to the new web site*</span></span>

    <span data-ttu-id="cc703-426">![웹 사이트 실행 중](build-restful-apis-with-aspnet-web-api/_static/image43.png "웹 사이트 실행 중")</span><span class="sxs-lookup"><span data-stu-id="cc703-426">![Web site running](build-restful-apis-with-aspnet-web-api/_static/image43.png "Web site running")</span></span>

    <span data-ttu-id="cc703-427">*웹 사이트 실행 중*</span><span class="sxs-lookup"><span data-stu-id="cc703-427">*Web site running*</span></span>
6. <span data-ttu-id="cc703-428">포털로 돌아가서 **이름** 열 아래에 있는 웹 사이트의 이름을 클릭 하 여 관리 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-428">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="cc703-429">![웹 사이트 관리 페이지 열기](build-restful-apis-with-aspnet-web-api/_static/image44.png "웹 사이트 관리 페이지 열기")</span><span class="sxs-lookup"><span data-stu-id="cc703-429">![Opening the web site management pages](build-restful-apis-with-aspnet-web-api/_static/image44.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="cc703-430">*웹 사이트 관리 페이지 열기*</span><span class="sxs-lookup"><span data-stu-id="cc703-430">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="cc703-431">**대시보드** 페이지의 **빠른** 보기 섹션에서 **게시 프로필 다운로드** 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-431">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cc703-432">*게시 프로필* 에는 사용 하도록 설정 된 각 게시 방법에 대해 웹 응용 프로그램을 Azure에 게시 하는 데 필요한 모든 정보가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-432">The *publish profile* contains all of the information required to publish a web application to a Azure for each enabled publication method.</span></span> <span data-ttu-id="cc703-433">게시 프로필에는 게시 방법이 사용 설정된 각 엔드포인트에 연결하고 이에 대해 인증하는 데 필요한 URL, 사용자 자격 증명 및 데이터베이스 문자열이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-433">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="cc703-434">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** 및 **Microsoft Visual Studio 2012** 는 Azure에 웹 응용 프로그램을 게시 하기 위해 이러한 프로그램의 구성을 자동화 하는 게시 프로필 읽기를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-434">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Azure.</span></span>

    <span data-ttu-id="cc703-435">![웹 사이트 게시 프로필을 다운로드 하는 중](build-restful-apis-with-aspnet-web-api/_static/image45.png "웹 사이트 게시 프로필을 다운로드 하는 중")</span><span class="sxs-lookup"><span data-stu-id="cc703-435">![Downloading the web site publish profile](build-restful-apis-with-aspnet-web-api/_static/image45.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="cc703-436">*웹 사이트 게시 프로필을 다운로드 하는 중*</span><span class="sxs-lookup"><span data-stu-id="cc703-436">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="cc703-437">알려진 위치에 게시 프로필 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-437">Download the publish profile file to a known location.</span></span> <span data-ttu-id="cc703-438">이 연습을 통해이 파일을 사용 하 여 Visual Studio에서 Azure에 웹 응용 프로그램을 게시 하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-438">Further in this exercise you will see how to use this file to publish a web application to Azure from Visual Studio.</span></span>

    <span data-ttu-id="cc703-439">![게시 프로필 파일을 저장 하는 중](build-restful-apis-with-aspnet-web-api/_static/image46.png "게시 프로필을 저장 하는 중")</span><span class="sxs-lookup"><span data-stu-id="cc703-439">![Saving the publish profile file](build-restful-apis-with-aspnet-web-api/_static/image46.png "Saving the publish profile")</span></span>

    <span data-ttu-id="cc703-440">*게시 프로필 파일을 저장 하는 중*</span><span class="sxs-lookup"><span data-stu-id="cc703-440">*Saving the publish profile file*</span></span>

<a id="ApxCTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="cc703-441">작업 2-데이터베이스 서버 구성</span><span class="sxs-lookup"><span data-stu-id="cc703-441">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="cc703-442">응용 프로그램에서 SQL Server 데이터베이스를 사용 하는 경우 SQL Database 서버를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-442">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="cc703-443">SQL Server 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 작업을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-443">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="cc703-444">응용 프로그램 데이터베이스를 저장 하기 위한 SQL Database 서버가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-444">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="cc703-445">Azure 관리 포털의 구독에서 SQL Database 서버를 볼 수는 **SQL database** | **Servers** | **서버 대시보드**.</span><span class="sxs-lookup"><span data-stu-id="cc703-445">You can view the SQL Database servers from your subscription in the Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="cc703-446">만든 서버가 없는 경우 명령 모음에서 **추가** 단추를 사용 하 여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-446">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="cc703-447">다음 작업에서 사용할 **서버 이름과 URL, 관리자 로그인 이름 및 암호**를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-447">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="cc703-448">이후 단계에서 생성 되므로 아직 데이터베이스를 만들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="cc703-448">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="cc703-449">![SQL Database 서버 대시보드](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL Database 서버 대시보드")</span><span class="sxs-lookup"><span data-stu-id="cc703-449">![SQL Database Server Dashboard](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="cc703-450">*SQL Database 서버 대시보드*</span><span class="sxs-lookup"><span data-stu-id="cc703-450">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="cc703-451">다음 작업에서는 Visual Studio에서 데이터베이스 연결을 테스트 합니다. 따라서 서버에서 **허용 되는 Ip 주소**목록에 로컬 IP 주소를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-451">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="cc703-452">이렇게 하려면 **구성**을 클릭 하 고, **현재 클라이언트 IP 주소** 에서 ip 주소를 선택 하 고, **시작 Ip 주소** 및 **끝 ip 주소** 텍스트 상자에 붙여 넣고, ![추가-클라이언트-ip 주소-확인 단추](build-restful-apis-with-aspnet-web-api/_static/image48.png) 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-452">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](build-restful-apis-with-aspnet-web-api/_static/image48.png) button.</span></span>

    ![클라이언트 IP 주소를 추가 하는 중](build-restful-apis-with-aspnet-web-api/_static/image49.png)

    <span data-ttu-id="cc703-454">*클라이언트 IP 주소를 추가 하는 중*</span><span class="sxs-lookup"><span data-stu-id="cc703-454">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="cc703-455">**클라이언트 Ip 주소가** 허용 된 ip 주소 목록에 추가 되 면 **저장** 을 클릭 하 여 변경 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-455">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![변경 내용 확인](build-restful-apis-with-aspnet-web-api/_static/image50.png)

    <span data-ttu-id="cc703-457">*변경 내용 확인*</span><span class="sxs-lookup"><span data-stu-id="cc703-457">*Confirm Changes*</span></span>

<a id="ApxCTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="cc703-458">작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="cc703-458">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="cc703-459">ASP.NET MVC 4 솔루션으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-459">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="cc703-460">**솔루션 탐색기**에서 웹 사이트 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-460">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="cc703-461">![응용 프로그램 게시](build-restful-apis-with-aspnet-web-api/_static/image51.png "응용 프로그램 게시")</span><span class="sxs-lookup"><span data-stu-id="cc703-461">![Publishing the Application](build-restful-apis-with-aspnet-web-api/_static/image51.png "Publishing the Application")</span></span>

    <span data-ttu-id="cc703-462">*웹 사이트 게시*</span><span class="sxs-lookup"><span data-stu-id="cc703-462">*Publishing the web site*</span></span>
2. <span data-ttu-id="cc703-463">첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-463">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="cc703-464">![게시 프로필을 가져오는 중](build-restful-apis-with-aspnet-web-api/_static/image52.png "게시 프로필을 가져오는 중")</span><span class="sxs-lookup"><span data-stu-id="cc703-464">![Importing the publish profile](build-restful-apis-with-aspnet-web-api/_static/image52.png "Importing the publish profile")</span></span>

    <span data-ttu-id="cc703-465">*게시 프로필을 가져오는 중*</span><span class="sxs-lookup"><span data-stu-id="cc703-465">*Importing publish profile*</span></span>
3. <span data-ttu-id="cc703-466">**연결 유효성 검사**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-466">Click **Validate Connection**.</span></span> <span data-ttu-id="cc703-467">유효성 검사가 완료 되 면 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-467">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cc703-468">유효성 검사는 연결 유효성 검사 단추 옆에 녹색 확인 표시가 표시 되 면 완료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-468">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="cc703-469">![연결 유효성 검사](build-restful-apis-with-aspnet-web-api/_static/image53.png "연결 유효성 검사")</span><span class="sxs-lookup"><span data-stu-id="cc703-469">![Validating connection](build-restful-apis-with-aspnet-web-api/_static/image53.png "Validating connection")</span></span>

    <span data-ttu-id="cc703-470">*연결 유효성 검사*</span><span class="sxs-lookup"><span data-stu-id="cc703-470">*Validating connection*</span></span>
4. <span data-ttu-id="cc703-471">**설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆에 있는 단추 (즉, **defaultconnection**)를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-471">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="cc703-472">![웹 배포 구성](build-restful-apis-with-aspnet-web-api/_static/image54.png "웹 배포 구성")</span><span class="sxs-lookup"><span data-stu-id="cc703-472">![Web deploy configuration](build-restful-apis-with-aspnet-web-api/_static/image54.png "Web deploy configuration")</span></span>

    <span data-ttu-id="cc703-473">*웹 배포 구성*</span><span class="sxs-lookup"><span data-stu-id="cc703-473">*Web deploy configuration*</span></span>
5. <span data-ttu-id="cc703-474">데이터베이스 연결을 다음과 같이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-474">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="cc703-475">**서버 이름** 에 *tcp:* 접두사를 사용 하 여 SQL Database 서버 URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-475">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="cc703-476">**사용자 이름** 에 서버 관리자 로그인 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-476">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="cc703-477">**암호** 에 서버 관리자 로그인 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-477">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="cc703-478">새 데이터베이스 이름 (예: *MVC4SampleDB*)을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-478">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="cc703-479">![대상 연결 문자열 구성](build-restful-apis-with-aspnet-web-api/_static/image55.png "대상 연결 문자열 구성")</span><span class="sxs-lookup"><span data-stu-id="cc703-479">![Configuring destination connection string](build-restful-apis-with-aspnet-web-api/_static/image55.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="cc703-480">*대상 연결 문자열 구성*</span><span class="sxs-lookup"><span data-stu-id="cc703-480">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="cc703-481">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-481">Then click **OK**.</span></span> <span data-ttu-id="cc703-482">데이터베이스를 만들 것인지 묻는 메시지가 표시 되 면 **예**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-482">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="cc703-483">![데이터베이스 만들기](build-restful-apis-with-aspnet-web-api/_static/image56.png "데이터베이스 문자열 만들기")</span><span class="sxs-lookup"><span data-stu-id="cc703-483">![Creating the database](build-restful-apis-with-aspnet-web-api/_static/image56.png "Creating the database string")</span></span>

    <span data-ttu-id="cc703-484">*데이터베이스 만들기*</span><span class="sxs-lookup"><span data-stu-id="cc703-484">*Creating the database*</span></span>
7. <span data-ttu-id="cc703-485">Windows Azure에서 SQL Database에 연결 하는 데 사용할 연결 문자열은 기본 연결 텍스트 상자 내에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-485">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="cc703-486">그런 후 **Next** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-486">Then click **Next**.</span></span>

    <span data-ttu-id="cc703-487">![SQL Database를 가리키는 연결 문자열](build-restful-apis-with-aspnet-web-api/_static/image57.png "SQL Database를 가리키는 연결 문자열")</span><span class="sxs-lookup"><span data-stu-id="cc703-487">![Connection string pointing to SQL Database](build-restful-apis-with-aspnet-web-api/_static/image57.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="cc703-488">*SQL Database를 가리키는 연결 문자열*</span><span class="sxs-lookup"><span data-stu-id="cc703-488">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="cc703-489">**미리 보기** 페이지에서 **게시**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-489">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="cc703-490">![웹 응용 프로그램 게시](build-restful-apis-with-aspnet-web-api/_static/image58.png "웹 응용 프로그램 게시")</span><span class="sxs-lookup"><span data-stu-id="cc703-490">![Publishing the web application](build-restful-apis-with-aspnet-web-api/_static/image58.png "Publishing the web application")</span></span>

    <span data-ttu-id="cc703-491">*웹 응용 프로그램 게시*</span><span class="sxs-lookup"><span data-stu-id="cc703-491">*Publishing the web application*</span></span>
9. <span data-ttu-id="cc703-492">게시 프로세스가 완료 되 면 기본 브라우저가 게시 된 웹 사이트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cc703-492">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="cc703-493">![Windows Azure에 게시 된 응용 프로그램](build-restful-apis-with-aspnet-web-api/_static/image59.png "Windows Azure에 게시 된 응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="cc703-493">![Application published to Windows Azure](build-restful-apis-with-aspnet-web-api/_static/image59.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="cc703-494">*Azure에 게시 된 응용 프로그램*</span><span class="sxs-lookup"><span data-stu-id="cc703-494">*Application published to Azure*</span></span>
