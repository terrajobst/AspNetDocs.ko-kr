---
uid: mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
title: ASP.NET MVC 응용 프로그램에 대 한 단위C#테스트 만들기 () | Microsoft Docs
author: StephenWalther
description: 컨트롤러 작업에 대 한 단위 테스트를 만드는 방법에 대해 알아봅니다. 이 자습서에서 Stephen Walther는 컨트롤러 작업에서 parti를 반환 하는지 여부를 테스트 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 08/19/2008
ms.assetid: d3a270b9-d7b1-47f2-8775-fc3beb518b5c
msc.legacyurl: /mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
msc.type: authoredcontent
ms.openlocfilehash: 35fd0d85c63e5bd196394ce11b851c822a6405d9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506093"
---
# <a name="creating-unit-tests-for-aspnet-mvc-applications-c"></a><span data-ttu-id="ca497-104">ASP.NET MVC 애플리케이션에 대한 단위 테스트 만들기(C#)</span><span class="sxs-lookup"><span data-stu-id="ca497-104">Creating Unit Tests for ASP.NET MVC Applications (C#)</span></span>

<span data-ttu-id="ca497-105">[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="ca497-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

[<span data-ttu-id="ca497-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="ca497-106">Download PDF</span></span>](https://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_07_CS.pdf)

> <span data-ttu-id="ca497-107">컨트롤러 작업에 대 한 단위 테스트를 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-107">Learn how to create unit tests for controller actions.</span></span> <span data-ttu-id="ca497-108">이 자습서에서 Stephen Walther는 컨트롤러 작업이 특정 뷰를 반환 하는지, 특정 데이터 집합을 반환 하는지 또는 다른 유형의 작업 결과를 반환 하는지를 테스트 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-108">In this tutorial, Stephen Walther demonstrates how to test whether a controller action returns a particular view, returns a particular set of data, or returns a different type of action result.</span></span>

<span data-ttu-id="ca497-109">이 자습서의 목표는 ASP.NET MVC 응용 프로그램에서 컨트롤러에 대 한 단위 테스트를 작성 하는 방법을 보여 주는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-109">The goal of this tutorial is to demonstrate how you can write unit tests for the controllers in your ASP.NET MVC applications.</span></span> <span data-ttu-id="ca497-110">3 가지 유형의 단위 테스트를 빌드하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-110">We discuss how to build three different types of unit tests.</span></span> <span data-ttu-id="ca497-111">컨트롤러 작업에서 반환 하는 뷰를 테스트 하는 방법, 컨트롤러 작업에서 반환 된 뷰 데이터를 테스트 하는 방법, 한 컨트롤러 작업이 두 번째 컨트롤러 작업으로 리디렉션하는 지 여부를 테스트 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-111">You learn how to test the view returned by a controller action, how to test the View Data returned by a controller action, and how to test whether or not one controller action redirects you to a second controller action.</span></span>

## <a name="creating-the-controller-under-test"></a><span data-ttu-id="ca497-112">테스트 중인 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="ca497-112">Creating the Controller under Test</span></span>

<span data-ttu-id="ca497-113">먼저 테스트 하려는 컨트롤러를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-113">Let's start by creating the controller that we intend to test.</span></span> <span data-ttu-id="ca497-114">`ProductController`이라는 컨트롤러는 목록 1에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-114">The controller, named the `ProductController`, is contained in Listing 1.</span></span>

<span data-ttu-id="ca497-115">**목록 1 – `ProductController.cs`**</span><span class="sxs-lookup"><span data-stu-id="ca497-115">**Listing 1 – `ProductController.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample1.cs)]

<span data-ttu-id="ca497-116">`ProductController`에는 `Index()` 및 `Details()`라는 두 개의 작업 메서드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-116">The `ProductController` contains two action methods named `Index()` and `Details()`.</span></span> <span data-ttu-id="ca497-117">두 작업 메서드는 모두 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-117">Both action methods return a view.</span></span> <span data-ttu-id="ca497-118">`Details()` 작업은 Id 라는 매개 변수를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-118">Notice that the `Details()` action accepts a parameter named Id.</span></span>

## <a name="testing-the-view-returned-by-a-controller"></a><span data-ttu-id="ca497-119">컨트롤러에서 반환 된 뷰 테스트</span><span class="sxs-lookup"><span data-stu-id="ca497-119">Testing the View returned by a Controller</span></span>

<span data-ttu-id="ca497-120">`ProductController`에서 올바른 뷰를 반환 하는지 여부를 테스트 하려고 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-120">Imagine that we want to test whether or not the `ProductController` returns the right view.</span></span> <span data-ttu-id="ca497-121">`ProductController.Details()` 작업이 호출 될 때 세부 정보 뷰가 반환 되는지 확인 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-121">We want to make sure that when the `ProductController.Details()` action is invoked, the Details view is returned.</span></span> <span data-ttu-id="ca497-122">목록 2의 테스트 클래스에는 `ProductController.Details()` 작업에서 반환 된 뷰를 테스트 하기 위한 단위 테스트가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-122">The test class in Listing 2 contains a unit test for testing the view returned by the `ProductController.Details()` action.</span></span>

<span data-ttu-id="ca497-123">**목록 2 – `ProductControllerTest.cs`**</span><span class="sxs-lookup"><span data-stu-id="ca497-123">**Listing 2 – `ProductControllerTest.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample2.cs)]

<span data-ttu-id="ca497-124">목록 2의 클래스에는 `TestDetailsView()`이라는 테스트 메서드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-124">The class in Listing 2 includes a test method named `TestDetailsView()`.</span></span> <span data-ttu-id="ca497-125">이 메서드에는 세 줄의 코드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-125">This method contains three lines of code.</span></span> <span data-ttu-id="ca497-126">코드의 첫 번째 줄은 `ProductController` 클래스의 새 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-126">The first line of code creates a new instance of the `ProductController` class.</span></span> <span data-ttu-id="ca497-127">코드의 두 번째 줄은 컨트롤러의 `Details()` 작업 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-127">The second line of code invokes the controller's `Details()` action method.</span></span> <span data-ttu-id="ca497-128">마지막으로, 코드의 마지막 줄은 `Details()` 동작에서 반환 된 뷰가 자세히 뷰 인지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-128">Finally, the last line of code checks whether or not the view returned by the `Details()` action is the Details view.</span></span>

<span data-ttu-id="ca497-129">`ViewResult.ViewName` 속성은 컨트롤러에서 반환 된 뷰의 이름을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-129">The `ViewResult.ViewName` property represents the name of the view returned by a controller.</span></span> <span data-ttu-id="ca497-130">이 속성 테스트에 대 한 한 가지 큰 경고입니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-130">One big warning about testing this property.</span></span> <span data-ttu-id="ca497-131">컨트롤러에서 뷰를 반환 하는 방법에는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-131">There are two ways that a controller can return a view.</span></span> <span data-ttu-id="ca497-132">컨트롤러는 다음과 같이 명시적으로 뷰를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-132">A controller can explicitly return a view like this:</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample3.cs)]

<span data-ttu-id="ca497-133">또는 다음과 같이 컨트롤러 작업의 이름에서 뷰 이름을 유추할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-133">Alternatively, the name of the view can be inferred from the name of the controller action like this:</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample4.cs)]

<span data-ttu-id="ca497-134">또한이 컨트롤러 작업은 `Details`라는 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-134">This controller action also returns a view named `Details`.</span></span> <span data-ttu-id="ca497-135">그러나 뷰의 이름은 동작 이름에서 유추 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-135">However, the name of the view is inferred from the action name.</span></span> <span data-ttu-id="ca497-136">뷰 이름을 테스트 하려면 컨트롤러 작업에서 뷰 이름을 명시적으로 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-136">If you want to test the view name, then you must explicitly return the view name from the controller action.</span></span>

<span data-ttu-id="ca497-137">목록 2에서 키보드 조합 **Ctrl + R, A** 를 입력 하거나 **솔루션의 모든 테스트 실행** 단추를 클릭 하 여 단위 테스트를 실행할 수 있습니다 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="ca497-137">You can run the unit test in Listing 2 by either entering the keyboard combination **Ctrl-R, A** or by clicking the **Run All Tests in Solution** button (see Figure 1).</span></span> <span data-ttu-id="ca497-138">테스트가 통과 되 면 그림 2에 테스트 결과 창이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-138">If the test passes, you'll see the Test Results window in Figure 2.</span></span>

<span data-ttu-id="ca497-139">[![솔루션의 모든 테스트 실행](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ca497-139">[![Run All Tests in Solution](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image1.png)</span></span>

<span data-ttu-id="ca497-140">**그림 01**: 솔루션에서 모든 테스트 실행 ([전체 크기 이미지를 보려면 클릭](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="ca497-140">**Figure 01**: Run All Tests in Solution ([Click to view full-size image](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image3.png))</span></span>

<span data-ttu-id="ca497-141">[성공 ![](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="ca497-141">[![Success!](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image4.png)</span></span>

<span data-ttu-id="ca497-142">**그림 02**: 성공!</span><span class="sxs-lookup"><span data-stu-id="ca497-142">**Figure 02**: Success!</span></span> <span data-ttu-id="ca497-143">([전체 크기 이미지를 보려면 클릭](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="ca497-143">([Click to view full-size image](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image6.png))</span></span>

## <a name="testing-the-view-data-returned-by-a-controller"></a><span data-ttu-id="ca497-144">컨트롤러에서 반환 된 뷰 데이터 테스트</span><span class="sxs-lookup"><span data-stu-id="ca497-144">Testing the View Data returned by a Controller</span></span>

<span data-ttu-id="ca497-145">MVC 컨트롤러는 *`View Data`* 이라는 항목을 사용 하 여 뷰에 데이터를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-145">An MVC controller passes data to a view by using something called *`View Data`*.</span></span> <span data-ttu-id="ca497-146">예를 들어 `ProductController Details()` 작업을 호출할 때 특정 제품에 대 한 세부 정보를 표시 하려는 경우를 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-146">For example, imagine that you want to display the details for a particular product when you invoke the `ProductController Details()` action.</span></span> <span data-ttu-id="ca497-147">이 경우 모델에 정의 된 `Product` 클래스의 인스턴스를 만들고 `View Data`를 활용 하 여 `Details` 뷰에 인스턴스를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-147">In that case, you can create an instance of a `Product` class (defined in your model) and pass the instance to the `Details` view by taking advantage of `View Data`.</span></span>

<span data-ttu-id="ca497-148">목록 3의 수정 된 `ProductController`에는 제품을 반환 하는 업데이트 된 `Details()` 작업이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-148">The modified `ProductController` in Listing 3 includes an updated `Details()` action that returns a Product.</span></span>

<span data-ttu-id="ca497-149">**목록 3 – `ProductController.cs`**</span><span class="sxs-lookup"><span data-stu-id="ca497-149">**Listing 3 – `ProductController.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample5.cs)]

<span data-ttu-id="ca497-150">먼저 `Details()` 작업은 랩톱 컴퓨터를 나타내는 `Product` 클래스의 새 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-150">First, the `Details()` action creates a new instance of the `Product` class that represents a laptop computer.</span></span> <span data-ttu-id="ca497-151">그런 다음 `Product` 클래스의 인스턴스가 `View()` 메서드에 두 번째 매개 변수로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-151">Next, the instance of the `Product` class is passed as the second parameter to the `View()` method.</span></span>

<span data-ttu-id="ca497-152">필요한 데이터가 뷰 데이터에 포함 되어 있는지 여부를 테스트 하는 단위 테스트를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-152">You can write unit tests to test whether the expected data is contained in view data.</span></span> <span data-ttu-id="ca497-153">목록 4에서 단위 테스트는 `ProductController Details()` 작업 메서드를 호출할 때 랩톱 컴퓨터를 나타내는 제품이 반환 되는지 여부를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-153">The unit test in Listing 4 tests whether or not a Product representing a laptop computer is returned when you call the `ProductController Details()` action method.</span></span>

<span data-ttu-id="ca497-154">**목록 4 – `ProductControllerTest.cs`**</span><span class="sxs-lookup"><span data-stu-id="ca497-154">**Listing 4 – `ProductControllerTest.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample6.cs)]

<span data-ttu-id="ca497-155">목록 4에서 `TestDetailsView()` 메서드는 `Details()` 메서드를 호출 하 여 반환 된 뷰 데이터를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-155">In Listing 4, the `TestDetailsView()` method tests the View Data returned by invoking the `Details()` method.</span></span> <span data-ttu-id="ca497-156">`ViewData`은 `Details()` 메서드를 호출 하 여 반환 되는 `ViewResult` 속성으로 노출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-156">The `ViewData` is exposed as a property on the `ViewResult` returned by invoking the `Details()` method.</span></span> <span data-ttu-id="ca497-157">`ViewData.Model` 속성은 뷰에 전달 된 제품을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-157">The `ViewData.Model` property contains the product passed to the view.</span></span> <span data-ttu-id="ca497-158">테스트는 보기 데이터에 포함 된 제품의 이름이 랩톱 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-158">The test simply verifies that the product contained in the View Data has the name Laptop.</span></span>

## <a name="testing-the-action-result-returned-by-a-controller"></a><span data-ttu-id="ca497-159">컨트롤러에서 반환 하는 작업 결과 테스트</span><span class="sxs-lookup"><span data-stu-id="ca497-159">Testing the Action Result returned by a Controller</span></span>

<span data-ttu-id="ca497-160">더 복잡 한 컨트롤러 작업은 컨트롤러 작업에 전달 되는 매개 변수의 값에 따라 다른 유형의 작업 결과를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-160">A more complex controller action might return different types of action results depending on the values of the parameters passed to the controller action.</span></span> <span data-ttu-id="ca497-161">컨트롤러 작업은 `ViewResult`, `RedirectToRouteResult`또는 `JsonResult`를 포함 하 여 다양 한 유형의 작업 결과를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-161">A controller action can return a variety of types of action results including a `ViewResult`, `RedirectToRouteResult`, or `JsonResult`.</span></span>

<span data-ttu-id="ca497-162">예를 들어 목록 5에서 수정 된 `Details()` 작업은 올바른 제품 Id를 작업에 전달할 때 `Details` 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-162">For example, the modified `Details()` action in Listing 5 returns the `Details` view when you pass a valid product Id to the action.</span></span> <span data-ttu-id="ca497-163">1 보다 작은 값이 포함 된 Id로 잘못 된 제품 Id를 전달 하면 `Index()` 작업으로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-163">If you pass an invalid product Id -- an Id with a value less than 1 -- then you are redirected to the `Index()` action.</span></span>

<span data-ttu-id="ca497-164">**목록 5 – `ProductController.cs`**</span><span class="sxs-lookup"><span data-stu-id="ca497-164">**Listing 5 – `ProductController.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample7.cs)]

<span data-ttu-id="ca497-165">목록 6에서 단위 테스트를 사용 하 여 `Details()` 작업의 동작을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-165">You can test the behavior of the `Details()` action with the unit test in Listing 6.</span></span> <span data-ttu-id="ca497-166">목록 6의 단위 테스트는 값이-1 인 Id가 `Details()` 메서드에 전달 될 때 `Index` 뷰로 리디렉션되도록 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-166">The unit test in Listing 6 verifies that you are redirected to the `Index` view when an Id with the value -1 is passed to the `Details()` method.</span></span>

<span data-ttu-id="ca497-167">**목록 6 – `ProductControllerTest.cs`**</span><span class="sxs-lookup"><span data-stu-id="ca497-167">**Listing 6 – `ProductControllerTest.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample8.cs)]

<span data-ttu-id="ca497-168">컨트롤러 작업에서 `RedirectToAction()` 메서드를 호출 하면 컨트롤러 작업에서 `RedirectToRouteResult`을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-168">When you call the `RedirectToAction()` method in a controller action, the controller action returns a `RedirectToRouteResult`.</span></span> <span data-ttu-id="ca497-169">테스트는 `RedirectToRouteResult` 사용자를 `Index`라는 컨트롤러 작업으로 리디렉션할지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-169">The test checks whether the `RedirectToRouteResult` will redirect the user to a controller action named `Index`.</span></span>

## <a name="summary"></a><span data-ttu-id="ca497-170">요약</span><span class="sxs-lookup"><span data-stu-id="ca497-170">Summary</span></span>

<span data-ttu-id="ca497-171">이 자습서에서는 MVC 컨트롤러 작업에 대 한 단위 테스트를 작성 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-171">In this tutorial, you learned how to build unit tests for MVC controller actions.</span></span> <span data-ttu-id="ca497-172">먼저 컨트롤러 작업에서 올바른 뷰가 반환 되는지 여부를 확인 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-172">First, you learned how to verify whether the right view is returned by a controller action.</span></span> <span data-ttu-id="ca497-173">`ViewResult.ViewName` 속성을 사용 하 여 뷰의 이름을 확인 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-173">You learned how to use the `ViewResult.ViewName` property to verify the name of a view.</span></span>

<span data-ttu-id="ca497-174">다음으로 `View Data`의 콘텐츠를 테스트할 수 있는 방법을 검토 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-174">Next, we examined how you can test the contents of `View Data`.</span></span> <span data-ttu-id="ca497-175">컨트롤러 작업을 호출한 후 `View Data`에서 올바른 제품이 반환 되었는지 여부를 확인 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-175">You learned how to check whether the right product was returned in `View Data` after calling a controller action.</span></span>

<span data-ttu-id="ca497-176">마지막으로 컨트롤러 작업에서 다른 유형의 작업 결과가 반환 되는지 여부를 테스트 하는 방법에 대해 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-176">Finally, we discussed how you can test whether different types of action results are returned from a controller action.</span></span> <span data-ttu-id="ca497-177">컨트롤러에서 `ViewResult` 또는 `RedirectToRouteResult`를 반환 하는지 여부를 테스트 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="ca497-177">You learned how to test whether a controller returns a `ViewResult` or a `RedirectToRouteResult`.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="ca497-178">다음</span><span class="sxs-lookup"><span data-stu-id="ca497-178">Next</span></span>](creating-unit-tests-for-asp-net-mvc-applications-vb.md)
