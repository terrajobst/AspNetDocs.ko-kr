---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs
title: ASP.NET MVC 라우팅 개요 (C#) | Microsoft Docs
author: StephenWalther
description: 이 자습서에서 Stephen Walther는 ASP.NET MVC 프레임 워크에서 브라우저 요청을 컨트롤러 작업에 매핑하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 5b39d2d5-4bf9-4d04-94c7-81b84dfeeb31
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs
msc.type: authoredcontent
ms.openlocfilehash: 5e1155ca676e7a25b5bfc63e251c6387a010eb34
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437705"
---
# <a name="aspnet-mvc-routing-overview-c"></a><span data-ttu-id="c3274-103">ASP.NET MVC 라우팅 개요(C#)</span><span class="sxs-lookup"><span data-stu-id="c3274-103">ASP.NET MVC Routing Overview (C#)</span></span>

<span data-ttu-id="c3274-104">[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="c3274-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="c3274-105">이 자습서에서 Stephen Walther는 ASP.NET MVC 프레임 워크에서 브라우저 요청을 컨트롤러 작업에 매핑하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-105">In this tutorial, Stephen Walther shows how the ASP.NET MVC framework maps browser requests to controller actions.</span></span>

<span data-ttu-id="c3274-106">이 자습서에서는 *ASP.NET Routing*이라는 모든 ASP.NET MVC 응용 프로그램의 중요 한 기능을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-106">In this tutorial, you are introduced to an important feature of every ASP.NET MVC application called *ASP.NET Routing*.</span></span> <span data-ttu-id="c3274-107">ASP.NET 라우팅 모듈은 들어오는 브라우저 요청을 특정 MVC 컨트롤러 작업에 매핑하는 작업을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-107">The ASP.NET Routing module is responsible for mapping incoming browser requests to particular MVC controller actions.</span></span> <span data-ttu-id="c3274-108">이 자습서를 마치면 표준 경로 테이블에서 컨트롤러 작업에 요청을 매핑하는 방법이 이해 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-108">By the end of this tutorial, you will understand how the standard route table maps requests to controller actions.</span></span>

## <a name="using-the-default-route-table"></a><span data-ttu-id="c3274-109">기본 경로 테이블 사용</span><span class="sxs-lookup"><span data-stu-id="c3274-109">Using the Default Route Table</span></span>

<span data-ttu-id="c3274-110">새 ASP.NET MVC 응용 프로그램을 만들 때 응용 프로그램은 이미 ASP.NET 라우팅을 사용 하도록 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-110">When you create a new ASP.NET MVC application, the application is already configured to use ASP.NET Routing.</span></span> <span data-ttu-id="c3274-111">ASP.NET 라우팅은 두 위치에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-111">ASP.NET Routing is setup in two places.</span></span>

<span data-ttu-id="c3274-112">먼저 ASP.NET 라우팅은 응용 프로그램의 웹 구성 파일 (web.config 파일)에서 사용 하도록 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-112">First, ASP.NET Routing is enabled in your application's Web configuration file (Web.config file).</span></span> <span data-ttu-id="c3274-113">구성 파일에는 경로와 관련 된 4 개의 섹션, 즉 system.web. httpModules 섹션, system.web. httpHandlers 섹션, system.webserver 섹션 및 system.webserver와 같은 4 개의 섹션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-113">There are four sections in the configuration file that are relevant to routing: the system.web.httpModules section, the system.web.httpHandlers section, the system.webserver.modules section, and the system.webserver.handlers section.</span></span> <span data-ttu-id="c3274-114">이러한 섹션을 사용 하지 않으면 라우팅이 더 이상 작동 하지 않으므로 이러한 섹션을 삭제 하지 않도록 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-114">Be careful not to delete these sections because without these sections routing will no longer work.</span></span>

<span data-ttu-id="c3274-115">둘째, 더 중요 한 점은 응용 프로그램의 Global.asax 파일에 경로 테이블이 생성 되는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-115">Second, and more importantly, a route table is created in the application's Global.asax file.</span></span> <span data-ttu-id="c3274-116">Global.asax 파일은 ASP.NET 응용 프로그램 수명 주기 이벤트에 대 한 이벤트 처리기를 포함 하는 특수 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-116">The Global.asax file is a special file that contains event handlers for ASP.NET application lifecycle events.</span></span> <span data-ttu-id="c3274-117">경로 테이블은 응용 프로그램 시작 이벤트 중에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-117">The route table is created during the Application Start event.</span></span>

<span data-ttu-id="c3274-118">목록 1의 파일에는 ASP.NET MVC 응용 프로그램에 대 한 기본 global.asax 파일이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-118">The file in Listing 1 contains the default Global.asax file for an ASP.NET MVC application.</span></span>

<span data-ttu-id="c3274-119">**목록 1-Global.asax.cs**</span><span class="sxs-lookup"><span data-stu-id="c3274-119">**Listing 1 - Global.asax.cs**</span></span>

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample1.cs)]

<span data-ttu-id="c3274-120">MVC 응용 프로그램이 처음 시작 될 때 응용 프로그램\_Start () 메서드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-120">When an MVC application first starts, the Application\_Start() method is called.</span></span> <span data-ttu-id="c3274-121">이 메서드는 RegisterRoutes () 메서드를 차례로 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-121">This method, in turn, calls the RegisterRoutes() method.</span></span> <span data-ttu-id="c3274-122">RegisterRoutes () 메서드는 경로 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-122">The RegisterRoutes() method creates the route table.</span></span>

<span data-ttu-id="c3274-123">기본 경로 테이블에는 단일 경로 (기본값)가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-123">The default route table contains a single route (named Default).</span></span> <span data-ttu-id="c3274-124">기본 경로는 URL의 첫 번째 세그먼트를 컨트롤러 이름에 매핑하고, URL의 두 번째 세그먼트를 컨트롤러 작업에 매핑하고, 세 번째 세그먼트는 **id**라는 매개 변수에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-124">The Default route maps the first segment of a URL to a controller name, the second segment of a URL to a controller action, and the third segment to a parameter named **id**.</span></span>

<span data-ttu-id="c3274-125">웹 브라우저의 주소 표시줄에 다음 URL을 입력 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-125">Imagine that you enter the following URL into your web browser's address bar:</span></span>

<span data-ttu-id="c3274-126">/Home/Index/3</span><span class="sxs-lookup"><span data-stu-id="c3274-126">/Home/Index/3</span></span>

<span data-ttu-id="c3274-127">기본 경로는이 URL을 다음 매개 변수에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-127">The Default route maps this URL to the following parameters:</span></span>

- <span data-ttu-id="c3274-128">컨트롤러 = 홈</span><span class="sxs-lookup"><span data-stu-id="c3274-128">controller = Home</span></span>

- <span data-ttu-id="c3274-129">작업 = 인덱스</span><span class="sxs-lookup"><span data-stu-id="c3274-129">action = Index</span></span>

- <span data-ttu-id="c3274-130">id = 3</span><span class="sxs-lookup"><span data-stu-id="c3274-130">id = 3</span></span>

<span data-ttu-id="c3274-131">URL/Home/Index/3를 요청 하면 다음 코드가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-131">When you request the URL /Home/Index/3, the following code is executed:</span></span>

<span data-ttu-id="c3274-132">HomeController.Index(3)</span><span class="sxs-lookup"><span data-stu-id="c3274-132">HomeController.Index(3)</span></span>

<span data-ttu-id="c3274-133">기본 경로에는 세 매개 변수 모두에 대 한 기본값이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-133">The Default route includes defaults for all three parameters.</span></span> <span data-ttu-id="c3274-134">컨트롤러를 제공 하지 않으면 컨트롤러 매개 변수의 기본값은 **Home**입니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-134">If you don't supply a controller, then the controller parameter defaults to the value **Home**.</span></span> <span data-ttu-id="c3274-135">동작을 제공 하지 않으면 action 매개 변수의 기본값은 value **Index**로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-135">If you don't supply an action, the action parameter defaults to the value **Index**.</span></span> <span data-ttu-id="c3274-136">마지막으로 id를 제공 하지 않으면 id 매개 변수의 기본값은 빈 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-136">Finally, if you don't supply an id, the id parameter defaults to an empty string.</span></span>

<span data-ttu-id="c3274-137">기본 경로에서 Url을 컨트롤러 작업에 매핑하는 방법에 대 한 몇 가지 예를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-137">Let's look at a few examples of how the Default route maps URLs to controller actions.</span></span> <span data-ttu-id="c3274-138">브라우저 주소 표시줄에 다음 URL을 입력 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-138">Imagine that you enter the following URL into your browser address bar:</span></span>

<span data-ttu-id="c3274-139">/Home</span><span class="sxs-lookup"><span data-stu-id="c3274-139">/Home</span></span>

<span data-ttu-id="c3274-140">기본 경로 매개 변수 기본값으로 인해이 URL을 입력 하면 목록 2에서 HomeController 클래스의 Index () 메서드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-140">Because of the Default route parameter defaults, entering this URL will cause the Index() method of the HomeController class in Listing 2 to be called.</span></span>

<span data-ttu-id="c3274-141">**목록 2-HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="c3274-141">**Listing 2 - HomeController.cs**</span></span>

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample2.cs)]

<span data-ttu-id="c3274-142">목록 2에서 HomeController 클래스에는 Id 라는 단일 매개 변수를 허용 하는 Index () 라는 메서드가 포함 되어 있습니다. URL/Home를 사용 하면 Index () 메서드가 Id 매개 변수의 값으로 빈 문자열을 사용 하 여 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-142">In Listing 2, the HomeController class includes a method named Index() that accepts a single parameter named Id. The URL /Home causes the Index() method to be called with an empty string as the value of the Id parameter.</span></span>

<span data-ttu-id="c3274-143">MVC 프레임 워크는 컨트롤러 작업을 호출 하는 방식 때문에 URL/Home는 목록 3에 있는 HomeController 클래스의 Index () 메서드와도 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-143">Because of the way that the MVC framework invokes controller actions, the URL /Home also matches the Index() method of the HomeController class in Listing 3.</span></span>

<span data-ttu-id="c3274-144">**목록 3-HomeController.cs (매개 변수가 없는 인덱스 동작)**</span><span class="sxs-lookup"><span data-stu-id="c3274-144">**Listing 3 - HomeController.cs (Index action with no parameter)**</span></span>

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample3.cs)]

<span data-ttu-id="c3274-145">목록 3의 Index () 메서드는 매개 변수를 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-145">The Index() method in Listing 3 does not accept any parameters.</span></span> <span data-ttu-id="c3274-146">URL/Home는이 Index () 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-146">The URL /Home will cause this Index() method to be called.</span></span> <span data-ttu-id="c3274-147">또한 URL/Home/Index/3는이 메서드를 호출 합니다 (Id는 무시 됨).</span><span class="sxs-lookup"><span data-stu-id="c3274-147">The URL /Home/Index/3 also invokes this method (the Id is ignored).</span></span>

<span data-ttu-id="c3274-148">URL/Home는 목록 4에 있는 HomeController 클래스의 Index () 메서드와도 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-148">The URL /Home also matches the Index() method of the HomeController class in Listing 4.</span></span>

<span data-ttu-id="c3274-149">**목록 4-HomeController.cs (nullable 매개 변수가 있는 인덱스 동작)**</span><span class="sxs-lookup"><span data-stu-id="c3274-149">**Listing 4 - HomeController.cs (Index action with nullable parameter)**</span></span>

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample4.cs)]

<span data-ttu-id="c3274-150">목록 4에서 Index () 메서드에 하나의 정수 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-150">In Listing 4, the Index() method has one Integer parameter.</span></span> <span data-ttu-id="c3274-151">매개 변수가 Null을 허용 하는 매개 변수 이므로 Null 값을 가질 수 있으므로 오류를 발생 시 키 지 않고 인덱스 ()를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-151">Because the parameter is a nullable parameter (can have the value Null), the Index() can be called without raising an error.</span></span>

<span data-ttu-id="c3274-152">마지막으로, URL/Home를 사용 하 여 5 목록에서 Index () 메서드를 호출 하면 Id 매개 변수가 null을 허용 하는 매개 변수가 *아니기* 때문에 예외가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-152">Finally, invoking the Index() method in Listing 5 with the URL /Home causes an exception since the Id parameter *is not* a nullable parameter.</span></span> <span data-ttu-id="c3274-153">Index () 메서드를 호출 하려고 하면 그림 1에 표시 된 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-153">If you attempt to invoke the Index() method then you get the error displayed in Figure 1.</span></span>

<span data-ttu-id="c3274-154">**목록 5-HomeController.cs (Id 매개 변수가 있는 인덱스 작업)**</span><span class="sxs-lookup"><span data-stu-id="c3274-154">**Listing 5 - HomeController.cs (Index action with Id parameter)**</span></span>

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample5.cs)]

<span data-ttu-id="c3274-155">[매개 변수 값을 필요로 하는 컨트롤러 작업 호출 ![](asp-net-mvc-routing-overview-cs/_static/image1.jpg)](asp-net-mvc-routing-overview-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c3274-155">[![Invoking a controller action that expects a parameter value](asp-net-mvc-routing-overview-cs/_static/image1.jpg)](asp-net-mvc-routing-overview-cs/_static/image1.png)</span></span>

<span data-ttu-id="c3274-156">**그림 01**: 매개 변수 값을 필요로 하는 컨트롤러 작업 호출 ([전체 크기 이미지를 보려면 클릭](asp-net-mvc-routing-overview-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="c3274-156">**Figure 01**: Invoking a controller action that expects a parameter value ([Click to view full-size image](asp-net-mvc-routing-overview-cs/_static/image2.png))</span></span>

<span data-ttu-id="c3274-157">반면에 URL/Home/Index/3는 목록 5의 인덱스 컨트롤러 작업에만 제대로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-157">The URL /Home/Index/3, on the other hand, works just fine with the Index controller action in Listing 5.</span></span> <span data-ttu-id="c3274-158">Request/Home/Index/3를 사용 하면 값이 3 인 Id 매개 변수를 사용 하 여 Index () 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-158">The request /Home/Index/3 causes the Index() method to be called with an Id parameter that has the value 3.</span></span>

## <a name="summary"></a><span data-ttu-id="c3274-159">요약</span><span class="sxs-lookup"><span data-stu-id="c3274-159">Summary</span></span>

<span data-ttu-id="c3274-160">이 자습서의 목표는 ASP.NET 라우팅에 대 한 간략 한 소개를 제공 하는 것 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-160">The goal of this tutorial was to provide you with a brief introduction to ASP.NET Routing.</span></span> <span data-ttu-id="c3274-161">새 ASP.NET MVC 응용 프로그램을 사용 하 여 얻을 수 있는 기본 경로 테이블을 검사 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-161">We examined the default route table that you get with a new ASP.NET MVC application.</span></span> <span data-ttu-id="c3274-162">기본 경로에서 Url을 컨트롤러 작업에 매핑하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="c3274-162">You learned how the default route maps URLs to controller actions.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="c3274-163">다음</span><span class="sxs-lookup"><span data-stu-id="c3274-163">Next</span></span>](understanding-action-filters-cs.md)
