---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-controller-overview-vb
title: ASP.NET MVC 컨트롤러 개요 (VB) | Microsoft Docs
author: StephenWalther
description: 이 자습서에서 Stephen Walther는 ASP.NET MVC 컨트롤러를 소개 합니다. 새 컨트롤러를 만들고 다양 한 유형의 작업을 반환 하는 방법에 대해 알아봅니다.
ms.author: riande
ms.date: 02/16/2008
ms.assetid: 94c3e5d9-a904-445e-a34e-d92fd1ca108a
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-controller-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: f19e7dd7fc025de2e0c387db898d36623e790e6a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486923"
---
# <a name="aspnet-mvc-controller-overview-vb"></a><span data-ttu-id="39002-104">ASP.NET MVC 컨트롤러 개요(VB)</span><span class="sxs-lookup"><span data-stu-id="39002-104">ASP.NET MVC Controller Overview (VB)</span></span>

<span data-ttu-id="39002-105">[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="39002-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="39002-106">이 자습서에서 Stephen Walther는 ASP.NET MVC 컨트롤러를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-106">In this tutorial, Stephen Walther introduces you to ASP.NET MVC controllers.</span></span> <span data-ttu-id="39002-107">새 컨트롤러를 만들고 다른 유형의 작업 결과를 반환 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="39002-107">You learn how to create new controllers and return different types of action results.</span></span>

<span data-ttu-id="39002-108">이 자습서에서는 ASP.NET MVC 컨트롤러, 컨트롤러 작업 및 작업 결과 항목을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="39002-108">This tutorial explores the topic of ASP.NET MVC controllers, controller actions, and action results.</span></span> <span data-ttu-id="39002-109">이 자습서를 완료 한 후에는 컨트롤러가 ASP.NET MVC 웹 사이트와 상호 작용 하는 방식을 제어 하는 데 컨트롤러를 사용 하는 방법을 이해 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39002-109">After you complete this tutorial, you will understand how controllers are used to control the way a visitor interacts with an ASP.NET MVC website.</span></span>

## <a name="understanding-controllers"></a><span data-ttu-id="39002-110">컨트롤러 이해</span><span class="sxs-lookup"><span data-stu-id="39002-110">Understanding Controllers</span></span>

<span data-ttu-id="39002-111">MVC 컨트롤러는 ASP.NET MVC 웹 사이트에 대 한 요청에 응답 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-111">MVC controllers are responsible for responding to requests made against an ASP.NET MVC website.</span></span> <span data-ttu-id="39002-112">각 브라우저 요청은 특정 컨트롤러에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="39002-112">Each browser request is mapped to a particular controller.</span></span> <span data-ttu-id="39002-113">예를 들어 브라우저의 주소 표시줄에 다음 URL을 입력 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-113">For example, imagine that you enter the following URL into the address bar of your browser:</span></span>

`http://localhost/Product/Index/3`

<span data-ttu-id="39002-114">이 경우에는 제품 컨트롤러 라는 컨트롤러가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39002-114">In this case, a controller named ProductController is invoked.</span></span> <span data-ttu-id="39002-115">제품 컨트롤러는 브라우저 요청에 대 한 응답을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-115">The ProductController is responsible for generating the response to the browser request.</span></span> <span data-ttu-id="39002-116">예를 들어 컨트롤러가 특정 뷰를 브라우저에 다시 반환 하거나 컨트롤러가 사용자를 다른 컨트롤러로 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39002-116">For example, the controller might return a particular view back to the browser or the controller might redirect the user to another controller.</span></span>

<span data-ttu-id="39002-117">목록 1은 제품 컨트롤러 라는 간단한 컨트롤러를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-117">Listing 1 contains a simple controller named ProductController.</span></span>

<span data-ttu-id="39002-118">**Listing1-Controllers\ProductController.vb**</span><span class="sxs-lookup"><span data-stu-id="39002-118">**Listing1 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample1.vb)]

<span data-ttu-id="39002-119">목록 1에서 볼 수 있듯이 컨트롤러는 단지 클래스 (Visual Basic .NET 또는 C# 클래스)입니다.</span><span class="sxs-lookup"><span data-stu-id="39002-119">As you can see from Listing 1, a controller is just a class (a Visual Basic .NET or C# class).</span></span> <span data-ttu-id="39002-120">컨트롤러는 기본 System.object 클래스에서 파생 되는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="39002-120">A controller is a class that derives from the base System.Web.Mvc.Controller class.</span></span> <span data-ttu-id="39002-121">컨트롤러가이 기본 클래스에서 상속 하기 때문에 컨트롤러는 몇 가지 유용한 메서드를 무료로 상속 합니다 (이 메서드에 대해 잠시 설명).</span><span class="sxs-lookup"><span data-stu-id="39002-121">Because a controller inherits from this base class, a controller inherits several useful methods for free (We discuss these methods in a moment).</span></span>

## <a name="understanding-controller-actions"></a><span data-ttu-id="39002-122">컨트롤러 작업 이해</span><span class="sxs-lookup"><span data-stu-id="39002-122">Understanding Controller Actions</span></span>

<span data-ttu-id="39002-123">컨트롤러는 컨트롤러 작업을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-123">A controller exposes controller actions.</span></span> <span data-ttu-id="39002-124">작업은 브라우저 주소 표시줄에 특정 URL을 입력할 때 호출 되는 컨트롤러의 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="39002-124">An action is a method on a controller that gets called when you enter a particular URL in your browser address bar.</span></span> <span data-ttu-id="39002-125">예를 들어 다음 URL에 대 한 요청을 수행 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="39002-125">For example, imagine that you make a request for the following URL:</span></span>

`http://localhost/Product/Index/3`

<span data-ttu-id="39002-126">이 경우에는 Index () 메서드가 제품 컨트롤러 클래스에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39002-126">In this case, the Index() method is called on the ProductController class.</span></span> <span data-ttu-id="39002-127">Index () 메서드는 컨트롤러 작업의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="39002-127">The Index() method is an example of a controller action.</span></span>

<span data-ttu-id="39002-128">컨트롤러 작업은 컨트롤러 클래스의 공용 메서드 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-128">A controller action must be a public method of a controller class.</span></span> <span data-ttu-id="39002-129">Visual Basic.NET 메서드는 기본적으로 공용 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="39002-129">Visual Basic.NET methods, by default, are public methods.</span></span> <span data-ttu-id="39002-130">컨트롤러 클래스에 추가 하는 공용 메서드는 컨트롤러 작업으로 자동으로 노출 됩니다. 예를 들어, 컨트롤러 작업은 간단 하 게 브라우저 주소 표시줄에 올바른 URL을 입력 하 여 universe의 모든 사용자가 호출할 수 있기 때문에 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-130">Realize that any public method that you add to a controller class is exposed as a controller action automatically (You must be careful about this since a controller action can be invoked by anyone in the universe simply by typing the right URL into a browser address bar).</span></span>

<span data-ttu-id="39002-131">컨트롤러 작업에서 충족 해야 하는 몇 가지 추가 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39002-131">There are some additional requirements that must be satisfied by a controller action.</span></span> <span data-ttu-id="39002-132">컨트롤러 작업으로 사용 되는 메서드는 오버 로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="39002-132">A method used as a controller action cannot be overloaded.</span></span> <span data-ttu-id="39002-133">또한 컨트롤러 작업은 정적 메서드가 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="39002-133">Furthermore, a controller action cannot be a static method.</span></span> <span data-ttu-id="39002-134">그 외에는 모든 메서드를 컨트롤러 작업으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39002-134">Other than that, you can use just about any method as a controller action.</span></span>

## <a name="understanding-action-results"></a><span data-ttu-id="39002-135">작업 결과 이해</span><span class="sxs-lookup"><span data-stu-id="39002-135">Understanding Action Results</span></span>

<span data-ttu-id="39002-136">컨트롤러 작업은 *작업 결과*라고 하는 항목을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-136">A controller action returns something called an *action result*.</span></span> <span data-ttu-id="39002-137">작업 결과는 브라우저 요청에 대 한 응답으로 컨트롤러 작업에서 반환 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="39002-137">An action result is what a controller action returns in response to a browser request.</span></span>

<span data-ttu-id="39002-138">ASP.NET MVC 프레임 워크는 다음과 같은 몇 가지 유형의 작업 결과를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-138">The ASP.NET MVC framework supports several types of action results including:</span></span>

1. <span data-ttu-id="39002-139">ViewResult-HTML 및 태그를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="39002-139">ViewResult - Represents HTML and markup.</span></span>
2. <span data-ttu-id="39002-140">EmptyResult-결과가 없음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="39002-140">EmptyResult - Represents no result.</span></span>
3. <span data-ttu-id="39002-141">RedirectResult-새 URL로의 리디렉션을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="39002-141">RedirectResult - Represents a redirection to a new URL.</span></span>
4. <span data-ttu-id="39002-142">JsonResult-AJAX 응용 프로그램에서 사용할 수 있는 JavaScript Object Notation 결과를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="39002-142">JsonResult - Represents a JavaScript Object Notation result that can be used in an AJAX application.</span></span>
5. <span data-ttu-id="39002-143">JavaScriptResult-JavaScript 스크립트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="39002-143">JavaScriptResult - Represents a JavaScript script.</span></span>
6. <span data-ttu-id="39002-144">ContentResult-텍스트 결과를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="39002-144">ContentResult - Represents a text result.</span></span>
7. <span data-ttu-id="39002-145">FileContentResult-다운로드 가능한 파일 (이진 콘텐츠 포함)을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="39002-145">FileContentResult - Represents a downloadable file (with the binary content).</span></span>
8. <span data-ttu-id="39002-146">FilePathResult-다운로드 가능한 파일 (경로 포함)을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="39002-146">FilePathResult - Represents a downloadable file (with a path).</span></span>
9. <span data-ttu-id="39002-147">FileStreamResult-다운로드 가능한 파일 (파일 스트림 포함)을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="39002-147">FileStreamResult - Represents a downloadable file (with a file stream).</span></span>

<span data-ttu-id="39002-148">이러한 모든 작업 결과는 기본 ActionResult 클래스에서 상속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39002-148">All of these action results inherit from the base ActionResult class.</span></span>

<span data-ttu-id="39002-149">대부분의 경우 컨트롤러 작업은 ViewResult를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-149">In most cases, a controller action returns a ViewResult.</span></span> <span data-ttu-id="39002-150">예를 들어 목록 2의 인덱스 컨트롤러 동작은 ViewResult를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-150">For example, the Index controller action in Listing 2 returns a ViewResult.</span></span>

<span data-ttu-id="39002-151">**목록 2-controllers\bookcontroller**</span><span class="sxs-lookup"><span data-stu-id="39002-151">**Listing 2 - Controllers\BookController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample2.vb)]

<span data-ttu-id="39002-152">작업에서 ViewResult를 반환 하면 HTML이 브라우저로 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39002-152">When an action returns a ViewResult, HTML is returned to the browser.</span></span> <span data-ttu-id="39002-153">목록 2의 Index () 메서드는 브라우저에 대 한 Index 라는 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-153">The Index() method in Listing 2 returns a view named Index to the browser.</span></span>

<span data-ttu-id="39002-154">목록 2의 Index () 동작은 ViewResult ()를 반환 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="39002-154">Notice that the Index() action in Listing 2 does not return a ViewResult().</span></span> <span data-ttu-id="39002-155">대신 컨트롤러 기본 클래스의 View () 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-155">Instead, the View() method of the Controller base class is called.</span></span> <span data-ttu-id="39002-156">일반적으로 작업 결과를 직접 반환 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="39002-156">Normally, you do not return an action result directly.</span></span> <span data-ttu-id="39002-157">대신 컨트롤러 기본 클래스의 다음 메서드 중 하나를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-157">Instead, you call one of the following methods of the Controller base class:</span></span>

1. <span data-ttu-id="39002-158">View-ViewResult 작업 결과를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-158">View - Returns a ViewResult action result.</span></span>
2. <span data-ttu-id="39002-159">리디렉션-RedirectResult 작업 결과를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-159">Redirect - Returns a RedirectResult action result.</span></span>
3. <span data-ttu-id="39002-160">RedirectToAction-RedirectToRouteResult 작업 결과를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-160">RedirectToAction - Returns a RedirectToRouteResult action result.</span></span>
4. <span data-ttu-id="39002-161">RedirectToRoute-RedirectToRouteResult 작업 결과를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-161">RedirectToRoute - Returns a RedirectToRouteResult action result.</span></span>
5. <span data-ttu-id="39002-162">Json-JsonResult 작업 결과를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-162">Json - Returns a JsonResult action result.</span></span>
6. <span data-ttu-id="39002-163">JavaScriptResult-JavaScriptResult을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-163">JavaScriptResult - Returns a JavaScriptResult.</span></span>
7. <span data-ttu-id="39002-164">콘텐츠-ContentResult 작업 결과를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-164">Content - Returns a ContentResult action result.</span></span>
8. <span data-ttu-id="39002-165">File-메서드에 전달 된 매개 변수에 따라 FileContentResult, FilePathResult 또는 FileStreamResult를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-165">File - Returns a FileContentResult, FilePathResult, or FileStreamResult depending on the parameters passed to the method.</span></span>

<span data-ttu-id="39002-166">따라서 브라우저에 뷰를 반환 하려는 경우 View () 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-166">So, if you want to return a View to the browser, you call the View() method.</span></span> <span data-ttu-id="39002-167">한 컨트롤러 동작에서 다른 컨트롤러로 사용자를 리디렉션하려면 RedirectToAction () 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-167">If you want to redirect the user from one controller action to another, you call the RedirectToAction() method.</span></span> <span data-ttu-id="39002-168">예를 들어 목록 3의 Details () 동작은 Id 매개 변수에 값이 있는지 여부에 따라 뷰를 표시 하거나 사용자를 Index () 동작으로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-168">For example, the Details() action in Listing 3 either displays a view or redirects the user to the Index() action depending on whether the Id parameter has a value.</span></span>

<span data-ttu-id="39002-169">**목록 3-CustomerController .vb**</span><span class="sxs-lookup"><span data-stu-id="39002-169">**Listing 3 - CustomerController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample3.vb)]

<span data-ttu-id="39002-170">ContentResult 작업 결과는 특수 합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-170">The ContentResult action result is special.</span></span> <span data-ttu-id="39002-171">ContentResult 작업 결과를 사용 하 여 일반 텍스트로 작업 결과를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39002-171">You can use the ContentResult action result to return an action result as plain text.</span></span> <span data-ttu-id="39002-172">예를 들어 4를 나열 하는 Index () 메서드는 메시지를 HTML이 아닌 일반 텍스트로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-172">For example, the Index() method in Listing 4 returns a message as plain text and not as HTML.</span></span>

<span data-ttu-id="39002-173">**목록 4-Controllers\StatusController.vb**</span><span class="sxs-lookup"><span data-stu-id="39002-173">**Listing 4 - Controllers\StatusController.vb**</span></span>

> <span data-ttu-id="39002-174">StatusController</span><span class="sxs-lookup"><span data-stu-id="39002-174">StatusController</span></span>
> 
> 
> <span data-ttu-id="39002-175">System.Web.Mvc.Controller</span><span class="sxs-lookup"><span data-stu-id="39002-175">System.Web.Mvc.Controller</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample4.vb)]

<span data-ttu-id="39002-176">StatusController. Index () 동작을 호출 하면 뷰가 반환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="39002-176">When the StatusController.Index() action is invoked, a view is not returned.</span></span> <span data-ttu-id="39002-177">대신 "Hello World!" 원시 텍스트가</span><span class="sxs-lookup"><span data-stu-id="39002-177">Instead, the raw text "Hello World!"</span></span> <span data-ttu-id="39002-178">이 브라우저에 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39002-178">is returned to the browser.</span></span>

<span data-ttu-id="39002-179">컨트롤러 작업이 작업 결과가 아닌 결과 (예: 날짜 또는 정수)를 반환 하는 경우 결과가 ContentResult에 자동으로 래핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="39002-179">If a controller action returns a result that is not an action result - for example, a date or an integer - then the result is wrapped in a ContentResult automatically.</span></span> <span data-ttu-id="39002-180">예를 들어 목록 5에서 작업 컨트롤러의 Index () 동작을 호출 하면 해당 날짜는 자동으로 ContentResult로 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39002-180">For example, when the Index() action of the WorkController in Listing 5 is invoked, the date is returned as a ContentResult automatically.</span></span>

<span data-ttu-id="39002-181">**목록 5-근무 컨트롤러 .vb**</span><span class="sxs-lookup"><span data-stu-id="39002-181">**Listing 5 - WorkController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample5.vb)]

<span data-ttu-id="39002-182">목록 5의 Index () 동작은 DateTime 개체를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-182">The Index() action in Listing 5 returns a DateTime object.</span></span> <span data-ttu-id="39002-183">ASP.NET MVC 프레임 워크는 DateTime 개체를 문자열로 변환 하 고 ContentResult의 DateTime 값을 자동으로 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-183">The ASP.NET MVC framework converts the DateTime object to a string and wraps the DateTime value in a ContentResult automatically.</span></span> <span data-ttu-id="39002-184">브라우저는 날짜와 시간을 일반 텍스트로 받습니다.</span><span class="sxs-lookup"><span data-stu-id="39002-184">The browser receives the date and time as plain text.</span></span>

## <a name="summary"></a><span data-ttu-id="39002-185">요약</span><span class="sxs-lookup"><span data-stu-id="39002-185">Summary</span></span>

<span data-ttu-id="39002-186">이 자습서에서는 ASP.NET MVC 컨트롤러, 컨트롤러 작업 및 컨트롤러 작업 결과에 대 한 개념을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="39002-186">The purpose of this tutorial was to introduce you to the concepts of ASP.NET MVC controllers, controller actions, and controller action results.</span></span> <span data-ttu-id="39002-187">첫 번째 섹션에서는 ASP.NET MVC 프로젝트에 새 컨트롤러를 추가 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="39002-187">In the first section, you learned how to add new controllers to an ASP.NET MVC project.</span></span> <span data-ttu-id="39002-188">다음으로 컨트롤러의 공용 메서드를 컨트롤러 작업으로 universe에 노출 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="39002-188">Next, you learned how public methods of a controller are exposed to the universe as controller actions.</span></span> <span data-ttu-id="39002-189">마지막으로, 컨트롤러 작업에서 반환 될 수 있는 다양 한 유형의 작업 결과에 대해 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="39002-189">Finally, we discussed the different types of action results that can be returned from a controller action.</span></span> <span data-ttu-id="39002-190">특히 컨트롤러 작업에서 ViewResult, RedirectToActionResult 및 ContentResult를 반환 하는 방법에 대해 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="39002-190">In particular, we discussed how to return a ViewResult, RedirectToActionResult, and ContentResult from a controller action.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="39002-191">[이전](creating-a-custom-route-constraint-cs.md)
> [다음](creating-custom-routes-vb.md)</span><span class="sxs-lookup"><span data-stu-id="39002-191">[Previous](creating-a-custom-route-constraint-cs.md)
[Next](creating-custom-routes-vb.md)</span></span>
