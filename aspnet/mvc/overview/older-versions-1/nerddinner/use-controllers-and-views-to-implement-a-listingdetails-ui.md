---
uid: mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
title: 컨트롤러 및 뷰를 사용 하 여 목록/세부 정보 UI 구현 | Microsoft Docs
author: microsoft
description: 4 단계에서는 모델을 활용 하는 응용 프로그램에 컨트롤러를 추가 하 여 사용자에 게 데이터 목록/세부 정보 탐색 환경을 제공 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 64116e56-1c9a-4f07-8097-bb36cbb6e57f
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
msc.type: authoredcontent
ms.openlocfilehash: 74319fe5ea4c79b50140834349e2fdf86420cfbb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486221"
---
# <a name="use-controllers-and-views-to-implement-a-listingdetails-ui"></a><span data-ttu-id="2948b-103">컨트롤러 및 보기를 사용하여 목록/세부 정보 UI 구현</span><span class="sxs-lookup"><span data-stu-id="2948b-103">Use Controllers and Views to Implement a Listing/Details UI</span></span>

<span data-ttu-id="2948b-104">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="2948b-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="2948b-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="2948b-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="2948b-106">ASP.NET MVC 1을 사용 하 여 작고 완전 한 웹 응용 프로그램을 빌드하는 방법을 안내 하는 무료 ["Nerddinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 의 4 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-106">This is step 4 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="2948b-107">4 단계에서는 모델을 활용 하 여 응용 프로그램에 컨트롤러를 추가 하는 방법을 보여 줍니다 .이 모델을 사용 하 여 사용자에 게 dinners에 대 한 데이터 목록/세부 정보 탐색 환경을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-107">Step 4 shows how to add a Controller to the application that takes advantage of our model to provide users with a data listing/details navigation experience for dinners on our NerdDinner site.</span></span>
> 
> <span data-ttu-id="2948b-108">ASP.NET MVC 3을 사용 하는 경우 [mvc 3 시작](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [mvc Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-4-controllers-and-views"></a><span data-ttu-id="2948b-109">Nerddinner Step 4: 컨트롤러 및 뷰</span><span class="sxs-lookup"><span data-stu-id="2948b-109">NerdDinner Step 4: Controllers and Views</span></span>

<span data-ttu-id="2948b-110">기존 웹 프레임 워크 (기존 ASP, PHP, ASP.NET Web Forms 등)를 사용 하 여 들어오는 Url은 일반적으로 디스크의 파일에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-110">With traditional web frameworks (classic ASP, PHP, ASP.NET Web Forms, etc), incoming URLs are typically mapped to files on disk.</span></span> <span data-ttu-id="2948b-111">예: "/Products.aspx" 또는 "/Products.php"와 같은 URL에 대 한 요청은 "" 또는 "" 파일에 의해 처리 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-111">For example: a request for a URL like "/Products.aspx" or "/Products.php" might be processed by a "Products.aspx" or "Products.php" file.</span></span>

<span data-ttu-id="2948b-112">웹 기반 MVC 프레임 워크는 Url을 서버 코드에 약간 다른 방식으로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-112">Web-based MVC frameworks map URLs to server code in a slightly different way.</span></span> <span data-ttu-id="2948b-113">들어오는 Url을 파일에 매핑하는 대신, 해당 url을 클래스의 메서드에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-113">Instead of mapping incoming URLs to files, they instead map URLs to methods on classes.</span></span> <span data-ttu-id="2948b-114">이러한 클래스를 "컨트롤러" 라고 하며, 들어오는 HTTP 요청을 처리 하 고, 사용자 입력을 처리 하 고, 데이터를 검색 및 저장 하 고, 클라이언트로 다시 보낼 응답을 결정 합니다 (HTML 표시, 파일 다운로드, 다른 위치로 리디렉션). URL 등).</span><span class="sxs-lookup"><span data-stu-id="2948b-114">These classes are called "Controllers" and they are responsible for processing incoming HTTP requests, handling user input, retrieving and saving data, and determining the response to send back to the client (display HTML, download a file, redirect to a different URL, etc).</span></span>

<span data-ttu-id="2948b-115">이제 동료 Ddinner 응용 프로그램에 대 한 기본 모델을 빌드 했으므로 다음 단계는 응용 프로그램에 컨트롤러를 추가 하 여 사용자에 게 사이트의 Dinners에 대 한 데이터 목록/세부 정보 탐색 환경을 제공 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-115">Now that we have built up a basic model for our NerdDinner application, our next step will be to add a Controller to the application that takes advantage of it to provide users with a data listing/details navigation experience for Dinners on our site.</span></span>

### <a name="adding-a-dinnerscontroller-controller"></a><span data-ttu-id="2948b-116">DinnersController 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="2948b-116">Adding a DinnersController Controller</span></span>

<span data-ttu-id="2948b-117">웹 프로젝트 내에서 "컨트롤러" 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가&gt;컨트롤러** 메뉴 명령을 선택 하 여 시작 합니다 (Ctrl + M, Ctrl + C를 입력 하 여이 명령을 실행할 수도 있음).</span><span class="sxs-lookup"><span data-stu-id="2948b-117">We'll begin by right-clicking on the "Controllers" folder within our web project, and then select the **Add-&gt;Controller** menu command (you can also execute this command by typing Ctrl-M, Ctrl-C):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image1.png)

<span data-ttu-id="2948b-118">그러면 "컨트롤러 추가" 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-118">This will bring up the "Add Controller" dialog:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image2.png)

<span data-ttu-id="2948b-119">새 컨트롤러의 이름을 "DinnersController"로 하 고 "추가" 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-119">We'll name the new controller "DinnersController" and click the "Add" button.</span></span> <span data-ttu-id="2948b-120">그러면 Visual Studio가 \Controllers 디렉터리 아래에 DinnersController.cs 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-120">Visual Studio will then add a DinnersController.cs file under our \Controllers directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image3.png)

<span data-ttu-id="2948b-121">또한 코드 편집기 내에서 새로운 DinnersController 클래스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-121">It will also open up the new DinnersController class within the code-editor.</span></span>

### <a name="adding-index-and-details-action-methods-to-the-dinnerscontroller-class"></a><span data-ttu-id="2948b-122">Index () 및 Details () 동작 메서드를 DinnersController 클래스에 추가</span><span class="sxs-lookup"><span data-stu-id="2948b-122">Adding Index() and Details() Action Methods to the DinnersController Class</span></span>

<span data-ttu-id="2948b-123">응용 프로그램을 사용 하 여 방문자가 예정 된 dinners 목록을 검색 하 고 목록에서 저녁을 클릭 하 여이에 대 한 특정 세부 정보를 볼 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-123">We want to enable visitors using our application to browse a list of upcoming dinners, and allow them to click on any Dinner in the list to see specific details about it.</span></span> <span data-ttu-id="2948b-124">응용 프로그램에서 다음 Url을 게시 하 여이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-124">We'll do this by publishing the following URLs from our application:</span></span>

| <span data-ttu-id="2948b-125">**URL**</span><span class="sxs-lookup"><span data-stu-id="2948b-125">**URL**</span></span> | <span data-ttu-id="2948b-126">**용도**</span><span class="sxs-lookup"><span data-stu-id="2948b-126">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="2948b-127">*/Dinners/*</span><span class="sxs-lookup"><span data-stu-id="2948b-127">*/Dinners/*</span></span> | <span data-ttu-id="2948b-128">예정 된 dinners의 HTML 목록 표시</span><span class="sxs-lookup"><span data-stu-id="2948b-128">Display an HTML list of upcoming dinners</span></span> |
| <span data-ttu-id="2948b-129">*/Dinners/Details/[id]*</span><span class="sxs-lookup"><span data-stu-id="2948b-129">*/Dinners/Details/[id]*</span></span> | <span data-ttu-id="2948b-130">URL에 포함 된 "id" 매개 변수로 표시 되는 특정 dinner a에 대 한 세부 정보를 표시 합니다 .이 매개 변수는 데이터베이스에 있는 dinner of의 DinnerID와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-130">Display details about a specific dinner indicated by an "id" parameter embedded within the URL – which will match the DinnerID of the dinner in the database.</span></span> <span data-ttu-id="2948b-131">예:/Dinners/Details/2는 해당 DinnerID 값이 2 인 Dinner a에 대 한 세부 정보가 포함 된 HTML 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-131">For example: /Dinners/Details/2 would display an HTML page with details about the Dinner whose DinnerID value is 2.</span></span> |

<span data-ttu-id="2948b-132">이러한 Url의 초기 구현은 아래와 같이 DinnersController 클래스에 두 개의 공용 "작업 메서드"를 추가 하 여 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-132">We will publish initial implementations of these URLs by adding two public "action methods" to our DinnersController class like below:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample1.cs)]

<span data-ttu-id="2948b-133">그런 다음,이 응용 프로그램을 호출 하는 데 브라우저를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-133">We'll then run the NerdDinner application and use our browser to invoke them.</span></span> <span data-ttu-id="2948b-134">*"/Dinners/"* URL에 입력 하면 *Index ()* 메서드가 실행 되 고 다음 응답이 다시 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-134">Typing in the *"/Dinners/"* URL will cause our *Index()* method to run, and it will send back the following response:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image4.png)

<span data-ttu-id="2948b-135">*"/Dinners/Details/2"* URL에 입력 하면 *Details ()* 메서드가 실행 되 고 다음 응답이 다시 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-135">Typing in the *"/Dinners/Details/2"* URL will cause our *Details()* method to run, and send back the following response:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image5.png)

<span data-ttu-id="2948b-136">ASP.NET MVC에서 사용자의 microsoft의 microsoft 차원 클래스를 만들고 해당 메서드를 호출 하는 방법을 궁금할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-136">You might be wondering - how did ASP.NET MVC know to create our DinnersController class and invoke those methods?</span></span> <span data-ttu-id="2948b-137">이를 이해 하기 위해 라우팅을 어떻게 작동 하는지 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-137">To understand that let's take a quick look at how routing works.</span></span>

### <a name="understanding-aspnet-mvc-routing"></a><span data-ttu-id="2948b-138">ASP.NET MVC 라우팅 이해</span><span class="sxs-lookup"><span data-stu-id="2948b-138">Understanding ASP.NET MVC Routing</span></span>

<span data-ttu-id="2948b-139">ASP.NET MVC에는 Url이 컨트롤러 클래스에 매핑되는 방식을 유연 하 게 제어할 수 있는 강력한 URL 라우팅 엔진이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-139">ASP.NET MVC includes a powerful URL routing engine that provides a lot of flexibility in controlling how URLs are mapped to controller classes.</span></span> <span data-ttu-id="2948b-140">ASP.NET MVC에서 만들 컨트롤러 클래스를 선택 하 고, 호출할 메서드를 선택 하 고, 변수를 URL/Querystring에서 자동으로 구문 분석 하 여 매개 변수 인수로 메서드에 전달할 수 있는 다양 한 방법을 구성 하는 방법을 완벽 하 게 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-140">It allows us to completely customize how ASP.NET MVC chooses which controller class to create, which method to invoke on it, as well as configure different ways that variables can be automatically parsed from the URL/Querystring and passed to the method as parameter arguments.</span></span> <span data-ttu-id="2948b-141">응용 프로그램에서 원하는 URL 구조를 게시할 뿐만 아니라 SEO (검색 엔진 최적화)를 위해 사이트를 완전히 최적화할 수 있는 유연성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-141">It delivers the flexibility to totally optimize a site for SEO (search engine optimization) as well as publish any URL structure we want from an application.</span></span>

<span data-ttu-id="2948b-142">기본적으로 새 ASP.NET MVC 프로젝트에는 미리 구성 된 URL 라우팅 규칙 집합이 이미 등록 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-142">By default, new ASP.NET MVC projects come with a preconfigured set of URL routing rules already registered.</span></span> <span data-ttu-id="2948b-143">이렇게 하면 명시적으로 아무것도 구성 하지 않고도 응용 프로그램을 쉽게 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-143">This enables us to easily get started on an application without having to explicitly configure anything.</span></span> <span data-ttu-id="2948b-144">기본 라우팅 규칙 등록은 프로젝트의 "응용 프로그램" 클래스 내에서 찾을 수 있습니다. 프로젝트의 루트에 있는 "global.asax" 파일을 두 번 클릭 하 여 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-144">The default routing rule registrations can be found within the "Application" class of our projects – which we can open by double-clicking the "Global.asax" file in the root of our project:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image6.png)

<span data-ttu-id="2948b-145">기본 ASP.NET MVC 라우팅 규칙은이 클래스의 "RegisterRoutes" 메서드 내에 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-145">The default ASP.NET MVC routing rules are registered within the "RegisterRoutes" method of this class:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample2.cs)]

<span data-ttu-id="2948b-146">"경로입니다. MapRoute () "메서드 호출은 URL 형식을 사용 하 여 들어오는 Url을 컨트롤러 클래스에 매핑하는 기본 라우팅 규칙을 등록 합니다."/{controller}/{action}/{id} "-여기서" controller "는 인스턴스화할 컨트롤러 클래스의 이름이 고," action "은 해당 클래스에 대해 호출할 public 메서드의 이름이 고," id "는 메서드에 인수로 전달 될 수 있는 URL 내에 포함 된 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-146">The "routes.MapRoute()" method call above registers a default routing rule that maps incoming URLs to controller classes using the URL format: "/{controller}/{action}/{id}" – where "controller" is the name of the controller class to instantiate, "action" is the name of a public method to invoke on it, and "id" is an optional parameter embedded within the URL that can be passed as an argument to the method.</span></span> <span data-ttu-id="2948b-147">"MapRoute ()" 메서드 호출에 전달 되는 세 번째 매개 변수는 URL (Controller = "Home", Action = "Index", Id = "")에 없는 이벤트의 컨트롤러/작업/id 값에 사용할 기본값 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-147">The third parameter passed to the "MapRoute()" method call is a set of default values to use for the controller/action/id values in the event that they are not present in the URL (Controller = "Home", Action="Index", Id="").</span></span>

<span data-ttu-id="2948b-148">다음은 기본 "<em>/{controllers}/{action}/{id}"</em>경로 규칙을 사용 하 여 다양 한 url이 매핑되는 방법을 보여 주는 표입니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-148">Below is a table that demonstrates how a variety of URLs are mapped using the default "<em>/{controllers}/{action}/{id}"</em>route rule:</span></span>

| <span data-ttu-id="2948b-149">**URL**</span><span class="sxs-lookup"><span data-stu-id="2948b-149">**URL**</span></span> | <span data-ttu-id="2948b-150">**Controller 클래스**</span><span class="sxs-lookup"><span data-stu-id="2948b-150">**Controller Class**</span></span> | <span data-ttu-id="2948b-151">**Action 메서드**</span><span class="sxs-lookup"><span data-stu-id="2948b-151">**Action Method**</span></span> | <span data-ttu-id="2948b-152">**매개 변수가 전달 되었습니다.**</span><span class="sxs-lookup"><span data-stu-id="2948b-152">**Parameters Passed**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2948b-153">*/Dinners/Details/2*</span><span class="sxs-lookup"><span data-stu-id="2948b-153">*/Dinners/Details/2*</span></span> | <span data-ttu-id="2948b-154">DinnersController</span><span class="sxs-lookup"><span data-stu-id="2948b-154">DinnersController</span></span> | <span data-ttu-id="2948b-155">세부 정보 (id)</span><span class="sxs-lookup"><span data-stu-id="2948b-155">Details(id)</span></span> | <span data-ttu-id="2948b-156">id=2</span><span class="sxs-lookup"><span data-stu-id="2948b-156">id=2</span></span> |
| <span data-ttu-id="2948b-157">*/Dinners/Edit/5*</span><span class="sxs-lookup"><span data-stu-id="2948b-157">*/Dinners/Edit/5*</span></span> | <span data-ttu-id="2948b-158">DinnersController</span><span class="sxs-lookup"><span data-stu-id="2948b-158">DinnersController</span></span> | <span data-ttu-id="2948b-159">Edit(id)</span><span class="sxs-lookup"><span data-stu-id="2948b-159">Edit(id)</span></span> | <span data-ttu-id="2948b-160">id=5</span><span class="sxs-lookup"><span data-stu-id="2948b-160">id=5</span></span> |
| <span data-ttu-id="2948b-161">*/Dinners/Create*</span><span class="sxs-lookup"><span data-stu-id="2948b-161">*/Dinners/Create*</span></span> | <span data-ttu-id="2948b-162">DinnersController</span><span class="sxs-lookup"><span data-stu-id="2948b-162">DinnersController</span></span> | <span data-ttu-id="2948b-163">Create()</span><span class="sxs-lookup"><span data-stu-id="2948b-163">Create()</span></span> | <span data-ttu-id="2948b-164">해당 없음</span><span class="sxs-lookup"><span data-stu-id="2948b-164">N/A</span></span> |
| <span data-ttu-id="2948b-165">*/Dinners*</span><span class="sxs-lookup"><span data-stu-id="2948b-165">*/Dinners*</span></span> | <span data-ttu-id="2948b-166">DinnersController</span><span class="sxs-lookup"><span data-stu-id="2948b-166">DinnersController</span></span> | <span data-ttu-id="2948b-167">Index ()</span><span class="sxs-lookup"><span data-stu-id="2948b-167">Index()</span></span> | <span data-ttu-id="2948b-168">해당 없음</span><span class="sxs-lookup"><span data-stu-id="2948b-168">N/A</span></span> |
| <span data-ttu-id="2948b-169">*/Home*</span><span class="sxs-lookup"><span data-stu-id="2948b-169">*/Home*</span></span> | <span data-ttu-id="2948b-170">HomeController</span><span class="sxs-lookup"><span data-stu-id="2948b-170">HomeController</span></span> | <span data-ttu-id="2948b-171">Index ()</span><span class="sxs-lookup"><span data-stu-id="2948b-171">Index()</span></span> | <span data-ttu-id="2948b-172">해당 없음</span><span class="sxs-lookup"><span data-stu-id="2948b-172">N/A</span></span> |
| */* | <span data-ttu-id="2948b-173">HomeController</span><span class="sxs-lookup"><span data-stu-id="2948b-173">HomeController</span></span> | <span data-ttu-id="2948b-174">Index ()</span><span class="sxs-lookup"><span data-stu-id="2948b-174">Index()</span></span> | <span data-ttu-id="2948b-175">해당 없음</span><span class="sxs-lookup"><span data-stu-id="2948b-175">N/A</span></span> |

<span data-ttu-id="2948b-176">마지막 세 행에는 사용 되는 기본값 (Controller = Home, Action = Index, Id = "")이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-176">The last three rows show the default values (Controller = Home, Action = Index, Id = "") being used.</span></span> <span data-ttu-id="2948b-177">"Index" 메서드가 지정 되지 않은 경우 기본 작업 이름으로 등록 되기 때문에 "/Dinners" 및 "/Home" Url을 지정 하면 해당 컨트롤러 클래스에서 Index () 작업 메서드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-177">Because the "Index" method is registered as the default action name if one isn't specified, the "/Dinners" and "/Home" URLs cause the Index() action method to be invoked on their Controller classes.</span></span> <span data-ttu-id="2948b-178">"홈" 컨트롤러가 지정 되지 않은 경우 기본 컨트롤러로 등록 되기 때문에 "/" URL을 통해 HomeController 생성 되 고 Index () 작업 메서드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-178">Because the "Home" controller is registered as the default controller if one isn't specified, the "/" URL causes the HomeController to be created, and the Index() action method on it to be invoked.</span></span>

<span data-ttu-id="2948b-179">이러한 기본 URL 라우팅 규칙을 원하지 않는 경우에는 위의 RegisterRoutes 메서드 내에서 간단히 변경 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-179">If you don't like these default URL routing rules, the good news is that they are easy to change - just edit them within the RegisterRoutes method above.</span></span> <span data-ttu-id="2948b-180">그러나 이러한 공동으로 사용 하는 Ddinner 응용 프로그램의 경우 기본 URL 라우팅 규칙을 변경 하지 않습니다. 대신 그대로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-180">For our NerdDinner application, though, we aren't going to change any of the default URL routing rules – instead we'll just use them as-is.</span></span>

### <a name="using-the-dinnerrepository-from-our-dinnerscontroller"></a><span data-ttu-id="2948b-181">Binnerscontroller의 DinnerRepository 사용</span><span class="sxs-lookup"><span data-stu-id="2948b-181">Using the DinnerRepository from our DinnersController</span></span>

<span data-ttu-id="2948b-182">이제 microsoft의 DinnersController Index () 및 Details () 작업 메서드의 현재 구현을 모델을 사용 하는 구현으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-182">Let's now replace our current implementation of the DinnersController's Index() and Details() action methods with implementations that use our model.</span></span>

<span data-ttu-id="2948b-183">이전에 빌드한 DinnerRepository 클래스를 사용 하 여 동작을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-183">We'll use the DinnerRepository class we built earlier to implement the behavior.</span></span> <span data-ttu-id="2948b-184">"NerdDinner. 모델" 네임 스페이스를 참조 하는 "using" 문을 추가한 다음 Dinnerrepository 클래스의 필드로 DinnerRepository의 인스턴스를 선언 하는 것으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-184">We'll begin by adding a "using" statement that references the "NerdDinner.Models" namespace, and then declare an instance of our DinnerRepository as a field on our DinnerController class.</span></span>

<span data-ttu-id="2948b-185">이 챕터의 뒷부분에서는 "종속성 주입"의 개념을 소개 하 고 컨트롤러에서 더 나은 단위 테스트를 가능 하 게 하는 다른 방법을 보여 줍니다. 그러나 이제는이에 대 한 올바른 단위 테스트를 제공 합니다. 아래와 같이 인라인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-185">Later in this chapter we'll introduce the concept of "Dependency Injection" and show another way for our Controllers to obtain a reference to a DinnerRepository that enables better unit testing – but for right now we'll just create an instance of our DinnerRepository inline like below.</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample3.cs)]

<span data-ttu-id="2948b-186">이제 검색 된 데이터 모델 개체를 사용 하 여 HTML 응답을 다시 생성할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-186">Now we are ready to generate a HTML response back using our retrieved data model objects.</span></span>

### <a name="using-views-with-our-controller"></a><span data-ttu-id="2948b-187">컨트롤러에서 보기 사용</span><span class="sxs-lookup"><span data-stu-id="2948b-187">Using Views with our Controller</span></span>

<span data-ttu-id="2948b-188">작업 메서드 내에 HTML을 조합 하는 코드를 작성 한 다음, *응답. write ()* 도우미 메서드를 사용 하 여 클라이언트에 다시 보낼 수 있지만, 이러한 접근 방식은 속도가 훨씬 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-188">While it is possible to write code within our action methods to assemble HTML and then use the *Response.Write()* helper method to send it back to the client, that approach becomes fairly unwieldy quickly.</span></span> <span data-ttu-id="2948b-189">훨씬 더 나은 방법은 microsoft의 경우에는 microsoft의 응용 프로그램 및 데이터 논리를 microsoft의 microsoft 응용 프로그램 및 데이터 논리를 수행 하 고 html 표현을 출력 하는 별도의 "뷰" 템플릿에 HTML 응답을 렌더링 하는 데 필요한 데이터를 전달 하는 것입니다. 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-189">A much better approach is for us to only perform application and data logic inside our DinnersController action methods, and to then pass the data needed to render a HTML response to a separate "view" template that is responsible for outputting the HTML representation of it.</span></span> <span data-ttu-id="2948b-190">잠시 후에 표시 되는 것 처럼 "뷰" 템플릿은 일반적으로 HTML 태그와 포함 된 렌더링 코드의 조합을 포함 하는 텍스트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-190">As we'll see in a moment, a "view" template is a text file that typically contains a combination of HTML markup and embedded rendering code.</span></span>

<span data-ttu-id="2948b-191">컨트롤러 논리를 뷰 렌더링에서 분리 하면 몇 가지 큰 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-191">Separating our controller logic from our view rendering brings several big benefits.</span></span> <span data-ttu-id="2948b-192">특히 응용 프로그램 코드와 UI 서식/렌더링 코드 간에 명확 하지 않은 "문제 분리"를 강제 적용 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-192">In particular it helps enforce a clear "separation of concerns" between the application code and UI formatting/rendering code.</span></span> <span data-ttu-id="2948b-193">이를 통해 UI 렌더링 논리와 격리 하는 단위 테스트 응용 프로그램 논리를 훨씬 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-193">This makes it much easier to unit-test application logic in isolation from UI rendering logic.</span></span> <span data-ttu-id="2948b-194">나중에 응용 프로그램 코드를 변경 하지 않고도 UI 렌더링 템플릿을 더 쉽게 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-194">It makes it easier to later modify the UI rendering templates without having to make application code changes.</span></span> <span data-ttu-id="2948b-195">개발자와 디자이너가 더 쉽게 프로젝트에서 공동 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-195">And it can make it easier for developers and designers to collaborate together on projects.</span></span>

<span data-ttu-id="2948b-196">' Void ' 반환 형식이 "ActionResult" 인 반환 형식을 대신 사용 하 여 두 작업 메서드의 메서드 시그니처를 변경 하 여 HTML UI 응답을 다시 보내도록 하기 위해이 클래스를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-196">We can update our DinnersController class to indicate that we want to use a view template to send back an HTML UI response by changing the method signatures of our two action methods from having a return type of "void" to instead have a return type of "ActionResult".</span></span> <span data-ttu-id="2948b-197">그런 다음 컨트롤러 기본 클래스에서 *View ()* 도우미 메서드를 호출 하 여 아래와 같이 "viewresult" 개체를 다시 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-197">We can then call the *View()* helper method on the Controller base class to return back a "ViewResult" object like below:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample4.cs)]

<span data-ttu-id="2948b-198">위에서 사용 하는 *View ()* 도우미 메서드의 시그니처는 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-198">The signature of the *View()* helper method we are using above looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image7.png)

<span data-ttu-id="2948b-199">*View ()* 도우미 메서드의 첫 번째 매개 변수는 HTML 응답을 렌더링 하는 데 사용 하려는 뷰 템플릿 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-199">The first parameter to the *View()* helper method is the name of the view template file we want to use to render the HTML response.</span></span> <span data-ttu-id="2948b-200">두 번째 매개 변수는 뷰 템플릿이 HTML 응답을 렌더링 하기 위해 필요로 하는 데이터를 포함 하는 모델 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-200">The second parameter is a model object that contains the data that the view template needs in order to render the HTML response.</span></span>

<span data-ttu-id="2948b-201">Index () 작업 메서드 내에서 *view ()* 도우미 메서드를 호출 하 고 "인덱스" 뷰 템플릿을 사용 하 여 DINNERS의 HTML 목록을 렌더링 하려고 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-201">Within our Index() action method we are calling the *View()* helper method and indicating that we want to render an HTML listing of dinners using an "Index" view template.</span></span> <span data-ttu-id="2948b-202">다음에서 목록을 생성 하기 위해 뷰 템플릿이 Dinner objects의 시퀀스를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-202">We are passing the view template a sequence of Dinner objects to generate the list from:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample5.cs)]

<span data-ttu-id="2948b-203">Details () 작업 메서드 내에서 URL에 제공 된 id를 사용 하 여 Dinner object를 검색 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-203">Within our Details() action method we attempt to retrieve a Dinner object using the id provided within the URL.</span></span> <span data-ttu-id="2948b-204">유효한 Dinner found가 발견 되 면 "Details" 뷰 템플릿을 사용 하 여 검색 된 Dinner object를 렌더링 함을 나타내는 *view ()* 도우미 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-204">If a valid Dinner is found we call the *View()* helper method, indicating we want to use a "Details" view template to render the retrieved Dinner object.</span></span> <span data-ttu-id="2948b-205">잘못 된 dinner를 요청 하는 경우 "NotFound" 뷰 템플릿 (그리고 템플릿 이름만 사용 하는 *뷰 ()* 도우미 메서드의 오버 로드 된 버전)을 사용 하 여 dinner is가 없다는 것을 나타내는 유용한 오류 메시지를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-205">If an invalid dinner is requested, we render a helpful error message that indicates that the Dinner doesn't exist using a "NotFound" view template (and an overloaded version of the *View()* helper method that just takes the template name):</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample6.cs)]

<span data-ttu-id="2948b-206">이제 "NotFound", "Details" 및 "Index" 뷰 템플릿을 구현 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-206">Let's now implement the "NotFound", "Details", and "Index" view templates.</span></span>

### <a name="implementing-the-notfound-view-template"></a><span data-ttu-id="2948b-207">"NotFound" 뷰 템플릿 구현</span><span class="sxs-lookup"><span data-stu-id="2948b-207">Implementing the "NotFound" View Template</span></span>

<span data-ttu-id="2948b-208">먼저 "NotFound" 보기 템플릿을 구현 하 여 요청 된 저녁을 찾을 수 없음을 나타내는 오류 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-208">We'll begin by implementing the "NotFound" view template – which displays a friendly error message indicating that the requested dinner can't be found.</span></span>

<span data-ttu-id="2948b-209">컨트롤러 작업 메서드 내에 텍스트 커서를 놓고 마우스 오른쪽 단추를 클릭 한 다음 "보기 추가" 메뉴 명령을 선택 하 여 새 보기 템플릿을 만든 다음 Ctrl + M, Ctrl + V를 입력 하 여이 명령을 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-209">We'll create a new view template by positioning our text cursor within a controller action method, and then right click and choose the "Add View" menu command (we can also execute this command by typing Ctrl-M, Ctrl-V):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image8.png)

<span data-ttu-id="2948b-210">그러면 아래와 같이 "뷰 추가" 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-210">This will bring up an "Add View" dialog like below.</span></span> <span data-ttu-id="2948b-211">기본적으로 대화 상자는 대화가 시작 될 때 커서가 있던 동작 메서드의 이름과 일치 하도록 만들 뷰의 이름을 미리 채웁니다 (이 경우 "Details").</span><span class="sxs-lookup"><span data-stu-id="2948b-211">By default the dialog will pre-populate the name of the view to create to match the name of the action method the cursor was in when the dialog was launched (in this case "Details").</span></span> <span data-ttu-id="2948b-212">"NotFound" 템플릿을 먼저 구현 하려고 하기 때문에이 뷰 이름을 재정의 하 고 대신 "NotFound"로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-212">Because we want to first implement the "NotFound" template, we'll override this view name and set it to instead be "NotFound":</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image9.png)

<span data-ttu-id="2948b-213">"추가" 단추를 클릭 하면 Visual Studio는 "\Views\Dinners" 디렉터리 내에 새 "NotFound .aspx" 보기 템플릿을 만듭니다 (디렉터리가 아직 없는 경우에도 생성 됨).</span><span class="sxs-lookup"><span data-stu-id="2948b-213">When we click the "Add" button, Visual Studio will create a new "NotFound.aspx" view template for us within the "\Views\Dinners" directory (which it will also create if the directory doesn't already exist):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image10.png)

<span data-ttu-id="2948b-214">또한 코드 편집기 내에서 새로운 "NotFound .aspx" 보기 템플릿을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-214">It will also open up our new "NotFound.aspx" view template within the code-editor:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image11.png)

<span data-ttu-id="2948b-215">기본적으로 템플릿 보기에는 콘텐츠와 코드를 추가할 수 있는 두 개의 "콘텐츠 영역"이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-215">View templates by default have two "content regions" where we can add content and code.</span></span> <span data-ttu-id="2948b-216">첫 번째 방법에서는 다시 보낸 HTML 페이지의 "제목"을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-216">The first allows us to customize the "title" of the HTML page sent back.</span></span> <span data-ttu-id="2948b-217">두 번째 방법을 사용 하면 다시 보낸 HTML 페이지의 "주 콘텐츠"를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-217">The second allows us to customize the "main content" of the HTML page sent back.</span></span>

<span data-ttu-id="2948b-218">"NotFound" 뷰 템플릿을 구현 하려면 몇 가지 기본 콘텐츠를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-218">To implement our "NotFound" view template we'll add some basic content:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample7.aspx)]

<span data-ttu-id="2948b-219">그런 다음 브라우저에서 사용해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-219">We can then try it out within the browser.</span></span> <span data-ttu-id="2948b-220">이렇게 하려면 *"/Dinners/Details/9999"* URL을 요청 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-220">To do this let's request the *"/Dinners/Details/9999"* URL.</span></span> <span data-ttu-id="2948b-221">이는 데이터베이스에 현재 존재 하지 않는 dinner to를 참조 하 고,이를 통해 "NotFound" 뷰 템플릿을 렌더링 하는 데에는 DinnersController. Details () 작업 메서드가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-221">This will refer to a dinner that doesn't currently exist in the database, and will cause our DinnersController.Details() action method to render our "NotFound" view template:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image12.png)

<span data-ttu-id="2948b-222">위의 스크린샷에서 볼 수 있는 한 가지 사항은 기본 보기 템플릿이 화면에서 주 콘텐츠를 둘러싸는 많은 HTML을 상속한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-222">One thing you'll notice in the screen-shot above is that our basic view template has inherited a bunch of HTML that surrounds the main content on the screen.</span></span> <span data-ttu-id="2948b-223">이는 보기 템플릿이 사이트의 모든 보기에서 일관적인 레이아웃을 적용할 수 있는 "마스터 페이지" 템플릿을 사용 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-223">This is because our view-template is using a "master page" template that enables us to apply a consistent layout across all views on the site.</span></span> <span data-ttu-id="2948b-224">이 자습서의 뒷부분에서 마스터 페이지의 작동 방식에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-224">We'll discuss how master pages work more in a later part of this tutorial.</span></span>

### <a name="implementing-the-details-view-template"></a><span data-ttu-id="2948b-225">"Details" 뷰 템플릿 구현</span><span class="sxs-lookup"><span data-stu-id="2948b-225">Implementing the "Details" View Template</span></span>

<span data-ttu-id="2948b-226">이제 단일 Dinner model에 대 한 HTML을 생성 하는 "Details" 뷰 템플릿을 구현 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-226">Let's now implement the "Details" view template – which will generate HTML for a single Dinner model.</span></span>

<span data-ttu-id="2948b-227">이렇게 하려면 세부 정보 작업 메서드 내에 텍스트 커서를 놓고 마우스 오른쪽 단추를 클릭 한 다음 "보기 추가" 메뉴 명령을 선택 하거나 Ctrl + M, Ctrl + V를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-227">We'll do this by positioning our text cursor within the Details action method, and then right click and choose the "Add View" menu command (or press Ctrl-M, Ctrl-V):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image13.png)

<span data-ttu-id="2948b-228">그러면 "보기 추가" 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-228">This will bring up the "Add View" dialog.</span></span> <span data-ttu-id="2948b-229">기본 보기 이름 ("Details")을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-229">We'll keep the default view name ("Details").</span></span> <span data-ttu-id="2948b-230">또한 대화 상자에서 "강력한 형식의 뷰 만들기" 확인란을 선택 하 고 컨트롤러에서 뷰로 전달할 모델 유형의 이름을 선택 합니다 (combobox 드롭다운 사용).</span><span class="sxs-lookup"><span data-stu-id="2948b-230">We'll also select the "Create a strongly-typed View" checkbox in the dialog and select (using the combobox dropdown) the name of the model type we are passing from the Controller to the View.</span></span> <span data-ttu-id="2948b-231">이 뷰에서는 Dinner object를 전달 합니다 .이 형식의 정규화 된 이름은 "NerdDinner. 모델인"입니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-231">For this view we are passing a Dinner object (the fully qualified name for this type is: "NerdDinner.Models.Dinner"):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image14.png)

<span data-ttu-id="2948b-232">"빈 뷰"를 만들도록 선택한 이전 템플릿과 달리 이번에는 "Details" 템플릿을 사용 하 여 보기를 자동으로 "스 캐 폴드" 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-232">Unlike the previous template, where we chose to create an "Empty View", this time we will choose to automatically "scaffold" the view using a "Details" template.</span></span> <span data-ttu-id="2948b-233">위의 대화 상자에서 "콘텐츠 보기" 드롭다운을 변경 하 여이를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-233">We can indicate this by changing the "View content" drop-down in the dialog above.</span></span>

<span data-ttu-id="2948b-234">"스 캐 폴딩"은 전달 하는 Dinner object를 기반으로 세부 정보 보기 템플릿의 초기 구현을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-234">"Scaffolding" will generate an initial implementation of our details view template based on the Dinner object we are passing to it.</span></span> <span data-ttu-id="2948b-235">이를 통해 보기 템플릿 구현을 신속 하 게 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-235">This provides an easy way for us to quickly get started on our view template implementation.</span></span>

<span data-ttu-id="2948b-236">"추가" 단추를 클릭 하면 Visual Studio에서 "\Views\Dinners" 디렉터리 내에 새 "Details .aspx" 보기 템플릿 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-236">When we click the "Add" button, Visual Studio will create a new "Details.aspx" view template file for us within our "\Views\Dinners" directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image15.png)

<span data-ttu-id="2948b-237">또한 코드 편집기 내에서 새로운 "Details .aspx" 보기 템플릿을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-237">It will also open up our new "Details.aspx" view template within the code-editor.</span></span> <span data-ttu-id="2948b-238">Dinner model을 기반으로 하는 세부 정보 보기의 초기 스 캐 폴드 구현을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-238">It will contain an initial scaffold implementation of a details view based on a Dinner model.</span></span> <span data-ttu-id="2948b-239">스 캐 폴딩 엔진은 .NET 리플렉션을 사용 하 여 전달 된 클래스에 노출 되는 공용 속성을 확인 하 고 찾은 각 형식에 따라 적절 한 콘텐츠를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-239">The scaffolding engine uses .NET reflection to look at the public properties exposed on the class passed it, and will add appropriate content based on each type it finds:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample8.aspx)]

<span data-ttu-id="2948b-240">*"/Dinners/Details/1"* URL을 요청 하 여 브라우저에서 "세부 정보" 스 캐 폴드 구현이 어떻게 표시 되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-240">We can request the *"/Dinners/Details/1"* URL to see what this "details" scaffold implementation looks like in the browser.</span></span> <span data-ttu-id="2948b-241">이 URL을 사용 하면 처음 만들 때 데이터베이스에 수동으로 추가 된 dinners 중 하나가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-241">Using this URL will display one of the dinners we manually added to our database when we first created it:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image16.png)

<span data-ttu-id="2948b-242">이를 통해 신속 하 게 실행 하 고 세부 정보 .aspx 보기의 초기 구현을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-242">This gets us up and running quickly, and provides us with an initial implementation of our Details.aspx view.</span></span> <span data-ttu-id="2948b-243">그런 다음이를 이동 하 고 조정 하 여 UI를 사용자의 만족도로 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-243">We can then go and tweak it to customize the UI to our satisfaction.</span></span>

<span data-ttu-id="2948b-244">세부 정보 .aspx 템플릿을 자세히 살펴보면 포함 된 렌더링 코드 뿐만 아니라 정적 HTML도 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-244">When we look at the Details.aspx template more closely, we'll find that it contains static HTML as well as embedded rendering code.</span></span> <span data-ttu-id="2948b-245">&lt;%%&gt; 코드 너 깃는 뷰 템플릿이 렌더링 될 때 코드를 실행 하 고, &lt;% =%&gt; 코드는 해당 코드 내에 포함 된 코드를 실행 한 다음 결과를 템플릿의 출력 스트림으로 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-245">&lt;% %&gt; code nuggets execute code when the view template renders, and &lt;%= %&gt; code nuggets execute the code contained within them and then render the result to the output stream of the template.</span></span>

<span data-ttu-id="2948b-246">강력한 형식의 "모델" 속성을 사용 하 여 컨트롤러에서 전달 된 "Dinner" 모델 개체에 액세스 하는 코드를 보기 내에 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-246">We can write code within our View that accesses the "Dinner" model object that was passed from our controller using a strongly-typed "Model" property.</span></span> <span data-ttu-id="2948b-247">Visual Studio는 편집기 내에서이 "모델" 속성에 액세스할 때 전체 코드 intellisense를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-247">Visual Studio provides us with full code-intellisense when accessing this "Model" property within the editor:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image17.png)

<span data-ttu-id="2948b-248">최종 세부 정보 보기 템플릿의 소스가 아래와 같이 약간의 작업을 수행해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-248">Let's make some tweaks so that the source for our final Details view template looks like below:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample9.aspx)]

<span data-ttu-id="2948b-249">*"/Dinners/Details/1"* URL에 다시 액세스 하면 이제 아래와 같이 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-249">When we access the *"/Dinners/Details/1"* URL again it will now render like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image18.png)

### <a name="implementing-the-index-view-template"></a><span data-ttu-id="2948b-250">"인덱스" 뷰 템플릿 구현</span><span class="sxs-lookup"><span data-stu-id="2948b-250">Implementing the "Index" View Template</span></span>

<span data-ttu-id="2948b-251">이제 "인덱스" 뷰 템플릿을 구현 하 여 예정 된 Dinners 목록을 생성 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-251">Let's now implement the "Index" view template – which will generate a listing of upcoming Dinners.</span></span> <span data-ttu-id="2948b-252">이렇게 하려면 인덱스 작업 메서드 내에 텍스트 커서를 놓고 마우스 오른쪽 단추를 클릭 한 다음 "보기 추가" 메뉴 명령을 선택 하거나 Ctrl + M, Ctrl + V를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-252">To-do this we'll position our text cursor within the Index action method, and then right click and choose the "Add View" menu command (or press Ctrl-M, Ctrl-V).</span></span>

<span data-ttu-id="2948b-253">"뷰 추가" 대화 상자 내에서 "Index" 라는 뷰 템플릿을 유지 하 고 "강력한 형식의 뷰 만들기" 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-253">Within the "Add View" dialog we'll keep the view template named "Index" and select the "Create a strongly-typed view" checkbox.</span></span> <span data-ttu-id="2948b-254">이번에는 "목록" 보기 템플릿을 자동으로 생성 하 고 뷰에 전달 되는 모델 형식으로 "스 캐 폴드"를 선택 합니다 .이 경우 "목록"을 만드는 것으로 표시 되었기 때문에 보기 추가 대화 상자에서 보기 추가 대화 상자를 표시 합니다. 컨트롤러에서 뷰로 Dinner objects 시퀀스 전달:</span><span class="sxs-lookup"><span data-stu-id="2948b-254">This time we will choose to automatically generate a "List" view template, and select "NerdDinner.Models.Dinner" as the model type passed to the view (which because we have indicated we are creating a "List" scaffold will cause the Add View dialog to assume we are passing a sequence of Dinner objects from our Controller to the View):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image19.png)

<span data-ttu-id="2948b-255">"추가" 단추를 클릭 하면 Visual Studio에서 "\Views\Dinners" 디렉터리 내에 새 "" 템플릿 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-255">When we click the "Add" button, Visual Studio will create a new "Index.aspx" view template file for us within our "\Views\Dinners" directory.</span></span> <span data-ttu-id="2948b-256">뷰에 전달 된 Dinners의 HTML 테이블 목록을 제공 하는 초기 구현을 "스 캐 폴드" 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-256">It will "scaffold" an initial implementation within it that provides an HTML table listing of the Dinners we pass to the view.</span></span>

<span data-ttu-id="2948b-257">응용 프로그램을 실행 하 고 *"/Dinners/"* URL에 액세스 하면 Dinners 목록이 다음과 같이 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-257">When we run the application and access the *"/Dinners/"* URL it will render our list of dinners like so:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image20.png)

<span data-ttu-id="2948b-258">위의 테이블 솔루션은 Dinner data의 그리드와 유사한 레이아웃을 제공 합니다 .이는 고객의 저녁 식사 목록에 대해 원하는 내용이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-258">The table solution above gives us a grid-like layout of our Dinner data – which isn't quite what we want for our consumer facing Dinner listing.</span></span> <span data-ttu-id="2948b-259">위의 코드를 사용 하 여 테이블 대신 열을 렌더링 하는 데&gt; &lt;사용할 수 있는 데이터 열을 나열 하 고이를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-259">We can update the Index.aspx view template and modify it to list fewer columns of data, and use a &lt;ul&gt; element to render them instead of a table using the code below:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample10.aspx)]

<span data-ttu-id="2948b-260">위의 foreach 문 내에서 "var" 키워드를 사용 하 여 모델의 각 dinner 루프를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-260">We are using the "var" keyword within the above foreach statement as we loop over each dinner in our Model.</span></span> <span data-ttu-id="2948b-261">3\.0에 C# 익숙하지 않은 것은 "var"을 사용 하면 dinner object가 런타임에 바인딩되어 있음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-261">Those unfamiliar with C# 3.0 might think that using "var" means that the dinner object is late-bound.</span></span> <span data-ttu-id="2948b-262">대신, 컴파일러에서 강력한 형식의 "모델" 속성 ("IEnumerable&lt;Dinner&gt;" 형식)에 대해 형식 유추를 사용 하 고 로컬 "dinner" 변수를 Dinner type으로 컴파일 했음을 의미 합니다. 즉, 코드 블록 내에서 전체 intellisense 및 컴파일 시간 검사를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-262">It instead means that the compiler is using type-inference against the strongly typed "Model" property (which is of type "IEnumerable&lt;Dinner&gt;") and compiling the local "dinner" variable as a Dinner type – which means we get full intellisense and compile-time checking for it within code blocks:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image21.png)

<span data-ttu-id="2948b-263">브라우저에서 */Dinners* URL에 대 한 새로 고침을 누르면 업데이트 된 보기가 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-263">When we hit refresh on the */Dinners* URL in our browser our updated view now looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image22.png)

<span data-ttu-id="2948b-264">이는 더 나은 방법 이지만 완전히 아직 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-264">This is looking better – but isn't entirely there yet.</span></span> <span data-ttu-id="2948b-265">마지막 단계는 최종 사용자가 목록에서 개별 Dinners를 클릭 하 고 세부 정보를 볼 수 있도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-265">Our last step is to enable end-users to click individual Dinners in the list and see details about them.</span></span> <span data-ttu-id="2948b-266">이를 구현 하는 것은 microsoft의 자세한 작업 메서드에 연결 하는 HTML 하이퍼링크 요소를</span><span class="sxs-lookup"><span data-stu-id="2948b-266">We'll implement this by rendering HTML hyperlink elements that link to the Details action method on our DinnersController.</span></span>

<span data-ttu-id="2948b-267">인덱스 보기 내에서 다음 두 가지 방법 중 하나로 이러한 하이퍼링크를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-267">We can generate these hyperlinks within our Index view in one of two ways.</span></span> <span data-ttu-id="2948b-268">첫 번째 방법은 &lt;HTML 요소&gt; 내에 &lt;%%&gt; 블록을 포함 하는 아래와 같은&gt; 요소에 HTML &lt;수동으로 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-268">The first is to manually create HTML &lt;a&gt; elements like below, where we embed &lt;% %&gt; blocks within the &lt;a&gt; HTML element:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image23.png)

<span data-ttu-id="2948b-269">사용할 수 있는 다른 방법은 컨트롤러의 다른 작업 메서드에 연결 되는&gt; 요소를 프로그래밍 방식으로 &lt;HTML을 지 원하는 ASP.NET MVC 내에서 기본 제공 "Html.actionlink ()" 도우미 메서드를 활용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-269">An alternative approach we can use is to take advantage of the built-in "Html.ActionLink()" helper method within ASP.NET MVC that supports programmatically creating an HTML &lt;a&gt; element that links to another action method on a Controller:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample11.aspx)]

<span data-ttu-id="2948b-270">Html에 대 한 첫 번째 매개 변수입니다. Html.actionlink () 도우미 메서드는 표시할 링크 텍스트 (이 경우 dinner of의 제목)이 고, 두 번째 매개 변수는 링크를 생성할 컨트롤러 작업 이름 (이 경우 Details 메서드)이 고, 세 번째 매개 변수는 작업에 보낼 매개 변수 집합입니다 (속성 이름/값을 사용 하 여 무명 형식으로 구현 됨).</span><span class="sxs-lookup"><span data-stu-id="2948b-270">The first parameter to the Html.ActionLink() helper method is the link-text to display (in this case the title of the dinner), the second parameter is the Controller action name we want to generate the link to (in this case the Details method), and the third parameter is a set of parameters to send to the action (implemented as an anonymous type with property name/values).</span></span> <span data-ttu-id="2948b-271">이 경우에는 연결 하려는 dinner a의 "id" 매개 변수를 지정 합니다. ASP.NET MVC의 기본 URL 라우팅 규칙은 "{Controller}/{Action}/{id}" 이므로 html.actionlink () 도우미 메서드는 다음과 같은 출력을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-271">In this case we are specifying the "id" parameter of the dinner we want to link to, and because the default URL routing rule in ASP.NET MVC is "{Controller}/{Action}/{id}" the Html.ActionLink() helper method will generate the following output:</span></span>

[!code-html[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample12.html)]

<span data-ttu-id="2948b-272">여기서는 Html.actionlink () 도우미 메서드를 사용 하 고 목록에 있는 각 dinner를 적절 한 세부 정보 URL에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-272">For our Index.aspx view we'll use the Html.ActionLink() helper method approach and have each dinner in the list link to the appropriate details URL:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample13.aspx)]

<span data-ttu-id="2948b-273">이제 */Dinners* URL에 도달 하면 dinner list는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-273">And now when we hit the */Dinners* URL our dinner list looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image24.png)

<span data-ttu-id="2948b-274">목록에서 Dinners를 클릭 하면이에 대 한 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-274">When we click any of the Dinners in the list we'll navigate to see details about it:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image25.png)

### <a name="convention-based-naming-and-the-views-directory-structure"></a><span data-ttu-id="2948b-275">규칙 기반 명명 및 \Views 디렉터리 구조</span><span class="sxs-lookup"><span data-stu-id="2948b-275">Convention-based naming and the \Views directory structure</span></span>

<span data-ttu-id="2948b-276">ASP.NET MVC 응용 프로그램은 기본적으로 보기 템플릿을 확인할 때 규칙 기반 디렉터리 명명 구조를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-276">ASP.NET MVC applications by default use a convention-based directory naming structure when resolving view templates.</span></span> <span data-ttu-id="2948b-277">이를 통해 개발자는 컨트롤러 클래스 내에서 뷰를 참조할 때 위치 경로를 정규화 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-277">This allows developers to avoid having to fully-qualify a location path when referencing views from within a Controller class.</span></span> <span data-ttu-id="2948b-278">기본적으로 ASP.NET MVC는 응용 프로그램 아래의 \* \Views\[ControllerName]\* 디렉터리에서 뷰 템플릿 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-278">By default ASP.NET MVC will look for the view template file within the \*\Views\[ControllerName]\* directory underneath the application.</span></span>

<span data-ttu-id="2948b-279">예를 들어, "Index", "Details" 및 "NotFound"와 같은 세 가지 뷰 템플릿을 명시적으로 참조 하는</span><span class="sxs-lookup"><span data-stu-id="2948b-279">For example, we've been working on the DinnersController class – which explicitly references three view templates: "Index", "Details" and "NotFound".</span></span> <span data-ttu-id="2948b-280">ASP.NET MVC는 응용 프로그램 루트 디렉터리 아래의 *\Views\Dinners* 디렉터리 내에서 이러한 뷰를 기본적으로 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-280">ASP.NET MVC will by default look for these views within the *\Views\Dinners* directory underneath our application root directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image26.png)

<span data-ttu-id="2948b-281">이전에는 프로젝트에 현재 세 개의 컨트롤러 클래스 (HomeController 및 AccountController – 프로젝트를 만들 때 마지막 2 개가 기본적으로 추가 됨) 및 세 개의 하위 디렉터리 (각각 하나씩)가 있습니다. controller)를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-281">Notice above how there are currently three controller classes within the project (DinnersController, HomeController and AccountController – the last two were added by default when we created the project), and there are three sub-directories (one for each controller) within the \Views directory.</span></span>

<span data-ttu-id="2948b-282">Home 및 Accounts 컨트롤러에서 참조 되는 뷰는 해당 *\Views\Home* 및 *\Views\Account* 디렉터리에서 해당 뷰 템플릿을 자동으로 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-282">Views referenced from the Home and Accounts controllers will automatically resolve their view templates from the respective *\Views\Home* and *\Views\Account* directories.</span></span> <span data-ttu-id="2948b-283">*\Views\Shared* 하위 디렉터리는 응용 프로그램 내의 여러 컨트롤러에서 다시 사용 되는 뷰 템플릿을 저장할 수 있는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-283">The *\Views\Shared* sub-directory provides a way to store view templates that are re-used across multiple controllers within the application.</span></span> <span data-ttu-id="2948b-284">ASP.NET MVC는 뷰 템플릿을 확인 하려고 할 때 먼저 *\Views\[Controller]* 특정 디렉터리 내에서 확인 하 고, 해당 디렉터리에서 뷰 템플릿을 찾을 수 없는 경우 *\Views\Shared* 디렉터리 내에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-284">When ASP.NET MVC attempts to resolve a view template, it will first check within the *\Views\[Controller]* specific directory, and if it can't find the view template there it will look within the *\Views\Shared* directory.</span></span>

<span data-ttu-id="2948b-285">개별 뷰 템플릿 이름을 지정 하는 것이 좋습니다. 뷰 템플릿이 렌더링을 유발한 동작 메서드와 동일한 이름을 공유 하도록 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-285">When it comes to naming individual view templates, the recommended guidance is to have the view template share the same name as the action method that caused it to render.</span></span> <span data-ttu-id="2948b-286">예를 들어 "Index" 동작 메서드에서는 "Index" 뷰를 사용 하 여 뷰 결과를 렌더링 하 고 "Details" 작업 메서드는 "Details" 뷰를 사용 하 여 결과를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-286">For example, above our "Index" action method is using the "Index" view to render the view result, and the "Details" action method is using the "Details" view to render its results.</span></span> <span data-ttu-id="2948b-287">이렇게 하면 각 작업에 연결 된 템플릿을 빠르게 쉽게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-287">This makes it easy to quickly see which template is associated with each action.</span></span>

<span data-ttu-id="2948b-288">개발자는 뷰 템플릿의 이름이 컨트롤러에서 호출 되는 작업 메서드와 같을 때 뷰 템플릿 이름을 명시적으로 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-288">Developers do not need to explicitly specify the view template name when the view template has the same name as the action method being invoked on the controller.</span></span> <span data-ttu-id="2948b-289">대신, 뷰 이름을 지정 하지 않고 "View ()" 도우미 메서드에 모델 개체를 전달할 수 있으며, ASP.NET MVC는 *\Views\[ControllerName]\[ActionName]* 를 사용 하 여 디스크에서이 템플릿을 렌더링 하려고 함을 자동으로 유추 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-289">We can instead just pass the model object to the "View()" helper method (without specifying the view name), and ASP.NET MVC will automatically infer that we want to use the *\Views\[ControllerName]\[ActionName]* view template on disk to render it.</span></span>

<span data-ttu-id="2948b-290">이를 통해 컨트롤러 코드를 약간 정리 하 고 코드에서 이름을 두 번 중복 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-290">This allows us to clean up our controller code a little, and avoid duplicating the name twice in our code:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample14.cs)]

<span data-ttu-id="2948b-291">위의 코드는 사이트에 대 한 훌륭한 저녁 목록/세부 경험을 구현 하는 데 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-291">The above code is all that is needed to implement a nice Dinner listing/details experience for the site.</span></span>

#### <a name="next-step"></a><span data-ttu-id="2948b-292">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2948b-292">Next Step</span></span>

<span data-ttu-id="2948b-293">이제 훌륭한 Dinner 브라우징 환경을 구축 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-293">We now have a nice Dinner browsing experience built.</span></span>

<span data-ttu-id="2948b-294">이제 CRUD (만들기, 읽기, 업데이트, 삭제) 데이터 폼 편집 지원을 사용 하도록 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2948b-294">Let's now enable CRUD (Create, Read, Update, Delete) data form editing support.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2948b-295">[이전](build-a-model-with-business-rule-validations.md)
> [다음](provide-crud-create-read-update-delete-data-form-entry-support.md)</span><span class="sxs-lookup"><span data-stu-id="2948b-295">[Previous](build-a-model-with-business-rule-validations.md)
[Next](provide-crud-create-read-update-delete-data-form-entry-support.md)</span></span>
