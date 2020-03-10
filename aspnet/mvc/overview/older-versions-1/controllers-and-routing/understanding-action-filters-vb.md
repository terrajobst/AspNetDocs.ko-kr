---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-vb
title: 작업 필터 이해 (VB) | Microsoft Docs
author: microsoft
description: 이 자습서의 목표는 작업 필터를 설명 하는 것입니다. 작업 필터는 컨트롤러 작업 또는 전체 컨트롤러에 적용할 수 있는 특성입니다.
ms.author: riande
ms.date: 10/16/2008
ms.assetid: e83812f2-c53e-4a43-a7c1-d64c59ecf694
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-vb
msc.type: authoredcontent
ms.openlocfilehash: 263658231ccaa7863508c691a3570bc00b9e8039
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486587"
---
# <a name="understanding-action-filters-vb"></a><span data-ttu-id="b52fe-104">작업 필터 이해(VB)</span><span class="sxs-lookup"><span data-stu-id="b52fe-104">Understanding Action Filters (VB)</span></span>

<span data-ttu-id="b52fe-105">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="b52fe-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="b52fe-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="b52fe-106">Download PDF</span></span>](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_VB.pdf)

> <span data-ttu-id="b52fe-107">이 자습서의 목표는 작업 필터를 설명 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-107">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="b52fe-108">작업 필터는 컨트롤러 작업 (또는 전체 컨트롤러)에 적용할 수 있는 특성으로, 작업이 실행 되는 방식을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-108">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span>

## <a name="understanding-action-filters"></a><span data-ttu-id="b52fe-109">작업 필터 이해</span><span class="sxs-lookup"><span data-stu-id="b52fe-109">Understanding Action Filters</span></span>

<span data-ttu-id="b52fe-110">이 자습서의 목표는 작업 필터를 설명 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-110">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="b52fe-111">작업 필터는 컨트롤러 작업 (또는 전체 컨트롤러)에 적용할 수 있는 특성으로, 작업이 실행 되는 방식을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-111">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span> <span data-ttu-id="b52fe-112">ASP.NET MVC 프레임 워크에는 다음과 같은 몇 가지 작업 필터가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-112">The ASP.NET MVC framework includes several action filters:</span></span>

- <span data-ttu-id="b52fe-113">OutputCache –이 작업 필터는 지정 된 시간 동안 컨트롤러 작업의 출력을 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-113">OutputCache – This action filter caches the output of a controller action for a specified amount of time.</span></span>
- <span data-ttu-id="b52fe-114">HandleError –이 작업 필터는 컨트롤러 작업이 실행 될 때 발생 하는 오류를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-114">HandleError – This action filter handles errors raised when a controller action executes.</span></span>
- <span data-ttu-id="b52fe-115">권한 부여 –이 작업 필터를 사용 하면 특정 사용자 또는 역할에 대 한 액세스를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-115">Authorize – This action filter enables you to restrict access to a particular user or role.</span></span>

<span data-ttu-id="b52fe-116">사용자 지정 작업 필터를 직접 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-116">You also can create your own custom action filters.</span></span> <span data-ttu-id="b52fe-117">예를 들어 사용자 지정 인증 시스템을 구현 하기 위해 사용자 지정 작업 필터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-117">For example, you might want to create a custom action filter in order to implement a custom authentication system.</span></span> <span data-ttu-id="b52fe-118">또는 컨트롤러 동작에서 반환 된 뷰 데이터를 수정 하는 작업 필터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-118">Or, you might want to create an action filter that modifies the view data returned by a controller action.</span></span>

<span data-ttu-id="b52fe-119">이 자습서에서는 처음부터 작업 필터를 작성 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-119">In this tutorial, you learn how to build an action filter from the ground up.</span></span> <span data-ttu-id="b52fe-120">Visual Studio 출력 창에 작업 처리의 다양 한 단계를 기록 하는 로그 작업 필터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-120">We create a Log action filter that logs different stages of the processing of an action to the Visual Studio Output window.</span></span>

### <a name="using-an-action-filter"></a><span data-ttu-id="b52fe-121">작업 필터 사용</span><span class="sxs-lookup"><span data-stu-id="b52fe-121">Using an Action Filter</span></span>

<span data-ttu-id="b52fe-122">작업 필터는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-122">An action filter is an attribute.</span></span> <span data-ttu-id="b52fe-123">개별 컨트롤러 작업 또는 전체 컨트롤러에 대부분의 작업 필터를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-123">You can apply most action filters to either an individual controller action or an entire controller.</span></span>

<span data-ttu-id="b52fe-124">예를 들어 목록 1의 데이터 컨트롤러는 현재 시간을 반환 하는 `Index()` 이라는 동작을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-124">For example, the Data controller in Listing 1 exposes an action named `Index()` that returns the current time.</span></span> <span data-ttu-id="b52fe-125">이 작업은 `OutputCache` 작업 필터로 데코 레이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-125">This action is decorated with the `OutputCache` action filter.</span></span> <span data-ttu-id="b52fe-126">이 필터는 작업에서 반환 된 값이 10 초 동안 캐시 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-126">This filter causes the value returned by the action to be cached for 10 seconds.</span></span>

<span data-ttu-id="b52fe-127">**목록 1 – `Controllers\DataController.vb`**</span><span class="sxs-lookup"><span data-stu-id="b52fe-127">**Listing 1 – `Controllers\DataController.vb`**</span></span>

[!code-vb[Main](understanding-action-filters-vb/samples/sample1.vb)]

<span data-ttu-id="b52fe-128">브라우저의 주소 표시줄에 URL/Data/Index를 입력 하 고 새로 고침 단추를 여러 번 눌러 `Index()` 작업을 반복적으로 호출 하면 10 초 동안 동일한 시간이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-128">If you repeatedly invoke the `Index()` action by entering the URL /Data/Index into the address bar of your browser and hitting the Refresh button multiple times, then you will see the same time for 10 seconds.</span></span> <span data-ttu-id="b52fe-129">`Index()` 작업의 출력은 10 초 동안 캐시 됩니다 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="b52fe-129">The output of the `Index()` action is cached for 10 seconds (see Figure 1).</span></span>

<span data-ttu-id="b52fe-130">[![캐시 된 시간](understanding-action-filters-vb/_static/image2.png)](understanding-action-filters-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b52fe-130">[![Cached time](understanding-action-filters-vb/_static/image2.png)](understanding-action-filters-vb/_static/image1.png)</span></span>

<span data-ttu-id="b52fe-131">**그림 01**: 캐시 된 시간 ([전체 크기 이미지를 보려면 클릭](understanding-action-filters-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="b52fe-131">**Figure 01**: Cached time ([Click to view full-size image](understanding-action-filters-vb/_static/image3.png))</span></span>

<span data-ttu-id="b52fe-132">목록 1에서 `OutputCache` 작업 필터 – `Index()` 메서드에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-132">In Listing 1, a single action filter – the `OutputCache` action filter – is applied to the `Index()` method.</span></span> <span data-ttu-id="b52fe-133">필요한 경우 여러 작업 필터를 동일한 작업에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-133">If you need, you can apply multiple action filters to the same action.</span></span> <span data-ttu-id="b52fe-134">예를 들어 `OutputCache` 및 `HandleError` 작업 필터를 모두 동일한 작업에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-134">For example, you might want to apply both the `OutputCache` and `HandleError` action filters to the same action.</span></span>

<span data-ttu-id="b52fe-135">목록 1에서 `OutputCache` 작업 필터는 `Index()` 작업에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-135">In Listing 1, the `OutputCache` action filter is applied to the `Index()` action.</span></span> <span data-ttu-id="b52fe-136">또한 `DataController` 클래스 자체에이 특성을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-136">You also could apply this attribute to the `DataController` class itself.</span></span> <span data-ttu-id="b52fe-137">이 경우 컨트롤러에서 노출 하는 작업에서 반환 된 결과는 10 초 동안 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-137">In that case, the result returned by any action exposed by the controller would be cached for 10 seconds.</span></span>

### <a name="the-different-types-of-filters"></a><span data-ttu-id="b52fe-138">여러 유형의 필터</span><span class="sxs-lookup"><span data-stu-id="b52fe-138">The Different Types of Filters</span></span>

<span data-ttu-id="b52fe-139">ASP.NET MVC 프레임 워크는 다음과 같은 네 가지 유형의 필터를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-139">The ASP.NET MVC framework supports four different types of filters:</span></span>

1. <span data-ttu-id="b52fe-140">권한 부여 필터 – `IAuthorizationFilter` 특성을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-140">Authorization filters – Implements the `IAuthorizationFilter` attribute.</span></span>
2. <span data-ttu-id="b52fe-141">작업 필터 – `IActionFilter` 특성을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-141">Action filters – Implements the `IActionFilter` attribute.</span></span>
3. <span data-ttu-id="b52fe-142">결과 필터 – `IResultFilter` 특성을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-142">Result filters – Implements the `IResultFilter` attribute.</span></span>
4. <span data-ttu-id="b52fe-143">예외 필터 – `IExceptionFilter` 특성을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-143">Exception filters – Implements the `IExceptionFilter` attribute.</span></span>

<span data-ttu-id="b52fe-144">필터는 위에 나열 된 순서 대로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-144">Filters are executed in the order listed above.</span></span> <span data-ttu-id="b52fe-145">예를 들어 권한 부여 필터는 항상 다른 모든 유형의 필터 후에 작업 필터 및 예외 필터가 실행 되기 전에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-145">For example, authorization filters are always executed before action filters and exception filters are always executed after every other type of filter.</span></span>

<span data-ttu-id="b52fe-146">권한 부여 필터는 컨트롤러 작업에 대 한 인증 및 권한 부여를 구현 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-146">Authorization filters are used to implement authentication and authorization for controller actions.</span></span> <span data-ttu-id="b52fe-147">예를 들어 권한 부여 필터는 권한 부여 필터의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-147">For example, the Authorize filter is an example of an Authorization filter.</span></span>

<span data-ttu-id="b52fe-148">작업 필터는 컨트롤러 작업이 실행 되기 전후에 실행 되는 논리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-148">Action filters contain logic that is executed before and after a controller action executes.</span></span> <span data-ttu-id="b52fe-149">예를 들어 작업 필터를 사용 하 여 컨트롤러 작업에서 반환 하는 뷰 데이터를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-149">You can use an action filter, for instance, to modify the view data that a controller action returns.</span></span>

<span data-ttu-id="b52fe-150">결과 필터에는 뷰 결과가 실행 되기 전후에 실행 되는 논리가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-150">Result filters contain logic that is executed before and after a view result is executed.</span></span> <span data-ttu-id="b52fe-151">예를 들어 뷰가 브라우저에 렌더링 되기 바로 전에 뷰 결과를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-151">For example, you might want to modify a view result right before the view is rendered to the browser.</span></span>

<span data-ttu-id="b52fe-152">예외 필터는 실행할 필터의 마지막 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-152">Exception filters are the last type of filter to run.</span></span> <span data-ttu-id="b52fe-153">예외 필터를 사용 하 여 컨트롤러 작업 또는 컨트롤러 작업 결과에서 발생 한 오류를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-153">You can use an exception filter to handle errors raised by either your controller actions or controller action results.</span></span> <span data-ttu-id="b52fe-154">예외 필터를 사용 하 여 오류를 기록할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-154">You also can use exception filters to log errors.</span></span>

<span data-ttu-id="b52fe-155">각 유형의 필터는 특정 순서에 따라 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-155">Each different type of filter is executed in a particular order.</span></span> <span data-ttu-id="b52fe-156">동일한 형식의 필터를 실행 하는 순서를 제어 하려면 필터의 순서 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-156">If you want to control the order in which filters of the same type are executed then you can set a filter's Order property.</span></span>

<span data-ttu-id="b52fe-157">모든 작업 필터에 대 한 기본 클래스는 `System.Web.Mvc.FilterAttribute` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-157">The base class for all action filters is the `System.Web.Mvc.FilterAttribute` class.</span></span> <span data-ttu-id="b52fe-158">특정 형식의 필터를 구현 하려면 기본 필터 클래스에서 상속 하는 클래스를 만들고 하나 이상의 IAuthorizationFilter, IActionFilter, Iactionfilter 또는 ExceptionFilter 인터페이스를 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-158">If you want to implement a particular type of filter, then you need to create a class that inherits from the base Filter class and implements one or more of the IAuthorizationFilter, IActionFilter, IResultFilter, or ExceptionFilter interfaces.</span></span>

### <a name="the-base-actionfilterattribute-class"></a><span data-ttu-id="b52fe-159">기본 ActionFilterAttribute 클래스</span><span class="sxs-lookup"><span data-stu-id="b52fe-159">The Base ActionFilterAttribute Class</span></span>

<span data-ttu-id="b52fe-160">사용자 지정 작업 필터를 쉽게 구현할 수 있도록 ASP.NET MVC 프레임 워크에는 기본 `ActionFilterAttribute` 클래스가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-160">In order to make it easier for you to implement a custom action filter, the ASP.NET MVC framework includes a base `ActionFilterAttribute` class.</span></span> <span data-ttu-id="b52fe-161">이 클래스는 `IActionFilter` 및 `IResultFilter` 인터페이스를 모두 구현 하 고 `Filter` 클래스에서 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-161">This class implements both the `IActionFilter` and `IResultFilter` interfaces and inherits from the `Filter` class.</span></span>

<span data-ttu-id="b52fe-162">여기에 나와 있는 용어는 완전히 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-162">The terminology here is not entirely consistent.</span></span> <span data-ttu-id="b52fe-163">기술적으로 ActionFilterAttribute 클래스에서 상속 되는 클래스는 작업 필터와 결과 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-163">Technically, a class that inherits from the ActionFilterAttribute class is both an action filter and a result filter.</span></span> <span data-ttu-id="b52fe-164">그러나 ASP.NET MVC 프레임 워크에서 모든 종류의 필터를 참조 하는 데에는 word 작업 필터가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-164">However, in the loose sense, the word action filter is used to refer to any type of filter in the ASP.NET MVC framework.</span></span>

<span data-ttu-id="b52fe-165">기본 ActionFilterAttribute 클래스에는 재정의할 수 있는 다음 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-165">The base ActionFilterAttribute class has the following methods that you can override:</span></span>

- <span data-ttu-id="b52fe-166">OnActionExecuting –이 메서드는 컨트롤러 작업이 실행 되기 전에 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-166">OnActionExecuting – This method is called before a controller action is executed.</span></span>
- <span data-ttu-id="b52fe-167">OnActionExecuted –이 메서드는 컨트롤러 작업이 실행 된 후에 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-167">OnActionExecuted – This method is called after a controller action is executed.</span></span>
- <span data-ttu-id="b52fe-168">OnResultExecuting –이 메서드는 컨트롤러 작업 결과가 실행 되기 전에 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-168">OnResultExecuting – This method is called before a controller action result is executed.</span></span>
- <span data-ttu-id="b52fe-169">OnResultExecuted – 컨트롤러 작업 결과가 실행 된 후이 메서드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-169">OnResultExecuted – This method is called after a controller action result is executed.</span></span>

<span data-ttu-id="b52fe-170">다음 섹션에서는 이러한 여러 가지 방법을 구현 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-170">In the next section, we'll see how you can implement each of these different methods.</span></span>

### <a name="creating-a-log-action-filter"></a><span data-ttu-id="b52fe-171">로그 작업 필터 만들기</span><span class="sxs-lookup"><span data-stu-id="b52fe-171">Creating a Log Action Filter</span></span>

<span data-ttu-id="b52fe-172">사용자 지정 작업 필터를 작성 하는 방법을 보여 주기 위해 Visual Studio 출력 창에 컨트롤러 작업 처리 단계를 기록 하는 사용자 지정 작업 필터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-172">In order to illustrate how you can build a custom action filter, we'll create a custom action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span> <span data-ttu-id="b52fe-173">`LogActionFilter`은 목록 2에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-173">Our `LogActionFilter` is contained in Listing 2.</span></span>

<span data-ttu-id="b52fe-174">**목록 2 – `ActionFilters\LogActionFilter.vb`**</span><span class="sxs-lookup"><span data-stu-id="b52fe-174">**Listing 2 – `ActionFilters\LogActionFilter.vb`**</span></span>

[!code-vb[Main](understanding-action-filters-vb/samples/sample2.vb)]

<span data-ttu-id="b52fe-175">목록 2에서 `OnActionExecuting()`, `OnActionExecuted()`, `OnResultExecuting()`및 `OnResultExecuted()` 메서드는 모두 `Log()` 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-175">In Listing 2, the `OnActionExecuting()`, `OnActionExecuted()`, `OnResultExecuting()`, and `OnResultExecuted()` methods all call the `Log()` method.</span></span> <span data-ttu-id="b52fe-176">메서드 이름과 현재 경로 데이터는 `Log()` 메서드에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-176">The name of the method and the current route data is passed to the `Log()` method.</span></span> <span data-ttu-id="b52fe-177">`Log()` 메서드는 Visual Studio 출력 창에 메시지를 기록 합니다 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="b52fe-177">The `Log()` method writes a message to the Visual Studio Output window (see Figure 2).</span></span>

<span data-ttu-id="b52fe-178">[Visual Studio 출력 창에 쓰기 ![](understanding-action-filters-vb/_static/image5.png)](understanding-action-filters-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="b52fe-178">[![Writing to the Visual Studio Output window](understanding-action-filters-vb/_static/image5.png)](understanding-action-filters-vb/_static/image4.png)</span></span>

<span data-ttu-id="b52fe-179">**그림 02**: Visual Studio 출력 창에 쓰기 ([전체 크기 이미지를 보려면 클릭](understanding-action-filters-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="b52fe-179">**Figure 02**: Writing to the Visual Studio Output window ([Click to view full-size image](understanding-action-filters-vb/_static/image6.png))</span></span>

<span data-ttu-id="b52fe-180">목록 3의 홈 컨트롤러는 전체 컨트롤러 클래스에 로그 작업 필터를 적용할 수 있는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-180">The Home controller in Listing 3 illustrates how you can apply the Log action filter to an entire controller class.</span></span> <span data-ttu-id="b52fe-181">홈 컨트롤러에서 노출 하는 작업 (`Index()` 메서드 또는 `About()` 메서드)이 호출 될 때마다 작업 처리 단계는 Visual Studio 출력 창에 로깅됩니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-181">Whenever any of the actions exposed by the Home controller are invoked – either the `Index()` method or the `About()` method – the stages of processing the action are logged to the Visual Studio Output window.</span></span>

<span data-ttu-id="b52fe-182">**목록 3 – `Controllers\HomeController.vb`**</span><span class="sxs-lookup"><span data-stu-id="b52fe-182">**Listing 3 – `Controllers\HomeController.vb`**</span></span>

[!code-vb[Main](understanding-action-filters-vb/samples/sample3.vb)]

### <a name="summary"></a><span data-ttu-id="b52fe-183">요약</span><span class="sxs-lookup"><span data-stu-id="b52fe-183">Summary</span></span>

<span data-ttu-id="b52fe-184">이 자습서에서는 ASP.NET MVC 작업 필터를 소개 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-184">In this tutorial, you were introduced to ASP.NET MVC action filters.</span></span> <span data-ttu-id="b52fe-185">권한 부여 필터, 작업 필터, 결과 필터 및 예외 필터와 같은 네 가지 유형의 필터에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-185">You learned about the four different types of filters: authorization filters, action filters, result filters, and exception filters.</span></span> <span data-ttu-id="b52fe-186">또한 기본 `ActionFilterAttribute` 클래스에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-186">You also learned about the base `ActionFilterAttribute` class.</span></span>

<span data-ttu-id="b52fe-187">마지막으로 간단한 작업 필터를 구현 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-187">Finally, you learned how to implement a simple action filter.</span></span> <span data-ttu-id="b52fe-188">Visual Studio 출력 창에 컨트롤러 작업을 처리 하는 단계를 기록 하는 로그 작업 필터를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="b52fe-188">We created a Log action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b52fe-189">[이전](asp-net-mvc-routing-overview-vb.md)
> [다음](improving-performance-with-output-caching-vb.md)</span><span class="sxs-lookup"><span data-stu-id="b52fe-189">[Previous](asp-net-mvc-routing-overview-vb.md)
[Next](improving-performance-with-output-caching-vb.md)</span></span>
