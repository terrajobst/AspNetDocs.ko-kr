---
uid: web-api/overview/web-api-routing-and-actions/routing-and-action-selection
title: ASP.NET Web API에서 라우팅 및 작업 선택 Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 12/14/2018
ms.assetid: bcf2d223-cb7f-411e-be05-f43e96a14015
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-and-action-selection
msc.type: authoredcontent
ms.openlocfilehash: 62114e56fb29e80c93b82dcb78ce2bc2a123a83b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446915"
---
# <a name="routing-and-action-selection-in-aspnet-web-api"></a><span data-ttu-id="94a5b-102">ASP.NET Web API에서 라우팅 및 작업 선택</span><span class="sxs-lookup"><span data-stu-id="94a5b-102">Routing and Action Selection in ASP.NET Web API</span></span>

<span data-ttu-id="94a5b-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="94a5b-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="94a5b-104">이 문서에서는 ASP.NET Web API는 컨트롤러의 특정 작업에 HTTP 요청을 라우팅하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-104">This article describes how ASP.NET Web API routes an HTTP request to a particular action on a controller.</span></span>

> [!NOTE]
> <span data-ttu-id="94a5b-105">라우팅에 대 한 개략적인 개요는 [ASP.NET Web API에서 라우팅](routing-in-aspnet-web-api.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="94a5b-105">For a high-level overview of routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>

<span data-ttu-id="94a5b-106">이 문서에서는 라우팅 프로세스에 대 한 세부 정보를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-106">This article looks at the details of the routing process.</span></span> <span data-ttu-id="94a5b-107">Web API 프로젝트를 만들고 일부 요청이 원하는 방식으로 라우팅되지 않는 경우이 문서를 통해 도움을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-107">If you create a Web API project and find that some requests don't get routed the way you expect, hopefully this article will help.</span></span>

<span data-ttu-id="94a5b-108">라우팅에는 세 가지 주요 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-108">Routing has three main phases:</span></span>

1. <span data-ttu-id="94a5b-109">경로 템플릿에 대 한 URI 일치</span><span class="sxs-lookup"><span data-stu-id="94a5b-109">Matching the URI to a route template.</span></span>
2. <span data-ttu-id="94a5b-110">컨트롤러 선택</span><span class="sxs-lookup"><span data-stu-id="94a5b-110">Selecting a controller.</span></span>
3. <span data-ttu-id="94a5b-111">작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-111">Selecting an action.</span></span>

<span data-ttu-id="94a5b-112">프로세스의 일부를 사용자 지정 동작으로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-112">You can replace some parts of the process with your own custom behaviors.</span></span> <span data-ttu-id="94a5b-113">이 문서에서는 기본 동작을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-113">In this article, I describe the default behavior.</span></span> <span data-ttu-id="94a5b-114">마지막으로 동작을 사용자 지정할 수 있는 위치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-114">At the end, I note the places where you can customize the behavior.</span></span>

## <a name="route-templates"></a><span data-ttu-id="94a5b-115">경로 템플릿</span><span class="sxs-lookup"><span data-stu-id="94a5b-115">Route Templates</span></span>

<span data-ttu-id="94a5b-116">경로 템플릿은 URI 경로와 비슷하지만 중괄호를 사용 하 여 표시 되는 자리 표시자 값이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-116">A route template looks similar to a URI path, but it can have placeholder values, indicated with curly braces:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample1.ps1)]

<span data-ttu-id="94a5b-117">경로를 만들 때 일부 또는 모든 자리 표시자에 대 한 기본값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-117">When you create a route, you can provide default values for some or all of the placeholders:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample2.cs)]

<span data-ttu-id="94a5b-118">또한 URI 세그먼트가 자리 표시자와 일치 하는 방법을 제한 하는 제약 조건을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-118">You can also provide constraints, which restrict how a URI segment can match a placeholder:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample3.js)]

<span data-ttu-id="94a5b-119">프레임 워크는 URI 경로의 세그먼트를 템플릿에 일치 시 키 려 고 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-119">The framework tries to match the segments in the URI path to the template.</span></span> <span data-ttu-id="94a5b-120">템플릿의 리터럴은 정확히 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-120">Literals in the template must match exactly.</span></span> <span data-ttu-id="94a5b-121">제약 조건을 지정 하지 않으면 자리 표시자는 모든 값과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-121">A placeholder matches any value, unless you specify constraints.</span></span> <span data-ttu-id="94a5b-122">프레임 워크가 호스트 이름 또는 쿼리 매개 변수와 같은 URI의 다른 부분과 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-122">The framework does not match other parts of the URI, such as the host name or the query parameters.</span></span> <span data-ttu-id="94a5b-123">프레임 워크는 경로 테이블에서 URI와 일치 하는 첫 번째 경로를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-123">The framework selects the first route in the route table that matches the URI.</span></span>

<span data-ttu-id="94a5b-124">"{Controller}" 및 "{action}" 이라는 두 가지 특수 한 자리 표시 자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-124">There are two special placeholders: "{controller}" and "{action}".</span></span>

- <span data-ttu-id="94a5b-125">"{controller}"는 컨트롤러의 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-125">"{controller}" provides the name of the controller.</span></span>
- <span data-ttu-id="94a5b-126">"{action}"은 (는) 동작 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-126">"{action}" provides the name of the action.</span></span> <span data-ttu-id="94a5b-127">Web API에서 일반적인 규칙은 "{action}"을 생략 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-127">In Web API, the usual convention is to omit "{action}".</span></span>

### <a name="defaults"></a><span data-ttu-id="94a5b-128">기본값</span><span class="sxs-lookup"><span data-stu-id="94a5b-128">Defaults</span></span>

<span data-ttu-id="94a5b-129">기본값을 제공 하는 경우 경로는 해당 세그먼트가 없는 URI와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-129">If you provide defaults, the route will match a URI that is missing those segments.</span></span> <span data-ttu-id="94a5b-130">다음은 그 예입니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-130">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample4.cs)]

<span data-ttu-id="94a5b-131">Uri `http://localhost/api/products/all` 이전 경로와 일치 `http://localhost/api/products`.</span><span class="sxs-lookup"><span data-stu-id="94a5b-131">The URIs `http://localhost/api/products/all` and `http://localhost/api/products` match the preceding route.</span></span> <span data-ttu-id="94a5b-132">후자 URI에서 누락 된 `{category}` 세그먼트에는 `all`기본값이 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-132">In the latter URI, the missing `{category}` segment is assigned the default value `all`.</span></span>

### <a name="route-dictionary"></a><span data-ttu-id="94a5b-133">경로 사전</span><span class="sxs-lookup"><span data-stu-id="94a5b-133">Route Dictionary</span></span>

<span data-ttu-id="94a5b-134">프레임 워크가 URI에 대해 일치 하는 항목을 찾으면 각 자리 표시자에 대 한 값을 포함 하는 사전을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-134">If the framework finds a match for a URI, it creates a dictionary that contains the value for each placeholder.</span></span> <span data-ttu-id="94a5b-135">키는 중괄호를 포함 하지 않는 자리 표시자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-135">The keys are the placeholder names, not including the curly braces.</span></span> <span data-ttu-id="94a5b-136">값은 URI 경로 또는 기본값에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-136">The values are taken from the URI path or from the defaults.</span></span> <span data-ttu-id="94a5b-137">사전은 **IHttpRouteData** 개체에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-137">The dictionary is stored in the **IHttpRouteData** object.</span></span>

<span data-ttu-id="94a5b-138">이 경로 일치 단계에서 특수 한 "{controller}" 및 "{action}" 자리 표시자는 다른 자리 표시자와 동일 하 게 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-138">During this route-matching phase, the special "{controller}" and "{action}" placeholders are treated just like the other placeholders.</span></span> <span data-ttu-id="94a5b-139">단지 다른 값을 사용 하 여 사전에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-139">They are simply stored in the dictionary with the other values.</span></span>

<span data-ttu-id="94a5b-140">기본값은 RouteParameter 특수 값을 가질 수 있습니다 **.**</span><span class="sxs-lookup"><span data-stu-id="94a5b-140">A default can have the special value **RouteParameter.Optional**.</span></span> <span data-ttu-id="94a5b-141">자리 표시자에이 값이 할당 되 면 해당 값은 경로 사전에 추가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-141">If a placeholder gets assigned this value, the value is not added to the route dictionary.</span></span> <span data-ttu-id="94a5b-142">다음은 그 예입니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-142">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample5.cs)]

<span data-ttu-id="94a5b-143">URI 경로 "api/products"의 경우 경로 사전에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-143">For the URI path "api/products", the route dictionary will contain:</span></span>

- <span data-ttu-id="94a5b-144">컨트롤러: "제품"</span><span class="sxs-lookup"><span data-stu-id="94a5b-144">controller: "products"</span></span>
- <span data-ttu-id="94a5b-145">범주: "all"</span><span class="sxs-lookup"><span data-stu-id="94a5b-145">category: "all"</span></span>

<span data-ttu-id="94a5b-146">그러나 "api/products/장난감/123"의 경우 경로 사전에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-146">For "api/products/toys/123", however, the route dictionary will contain:</span></span>

- <span data-ttu-id="94a5b-147">컨트롤러: "제품"</span><span class="sxs-lookup"><span data-stu-id="94a5b-147">controller: "products"</span></span>
- <span data-ttu-id="94a5b-148">범주: "장난감"</span><span class="sxs-lookup"><span data-stu-id="94a5b-148">category: "toys"</span></span>
- <span data-ttu-id="94a5b-149">id: "123"</span><span class="sxs-lookup"><span data-stu-id="94a5b-149">id: "123"</span></span>

<span data-ttu-id="94a5b-150">기본값에는 경로 템플릿의 아무 곳에도 나타나지 않는 값이 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-150">The defaults can also include a value that does not appear anywhere in the route template.</span></span> <span data-ttu-id="94a5b-151">경로가 일치 하는 경우 해당 값이 사전에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-151">If the route matches, that value is stored in the dictionary.</span></span> <span data-ttu-id="94a5b-152">다음은 그 예입니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-152">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample6.cs)]

<span data-ttu-id="94a5b-153">URI 경로가 "api/root/8" 이면 사전에는 다음 두 값이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-153">If the URI path is "api/root/8", the dictionary will contain two values:</span></span>

- <span data-ttu-id="94a5b-154">컨트롤러: "고객"</span><span class="sxs-lookup"><span data-stu-id="94a5b-154">controller: "customers"</span></span>
- <span data-ttu-id="94a5b-155">id: "8"</span><span class="sxs-lookup"><span data-stu-id="94a5b-155">id: "8"</span></span>

## <a name="selecting-a-controller"></a><span data-ttu-id="94a5b-156">컨트롤러 선택</span><span class="sxs-lookup"><span data-stu-id="94a5b-156">Selecting a Controller</span></span>

<span data-ttu-id="94a5b-157">컨트롤러 선택은 **IHttpControllerSelector 컨트롤러** 메서드에서 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-157">Controller selection is handled by the **IHttpControllerSelector.SelectController** method.</span></span> <span data-ttu-id="94a5b-158">이 메서드는 **HttpRequestMessage** 인스턴스를 사용 하 여 **httpcontrollerdescriptor**를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-158">This method takes an **HttpRequestMessage** instance and returns an **HttpControllerDescriptor**.</span></span> <span data-ttu-id="94a5b-159">기본 구현은 **DefaultHttpControllerSelector** 클래스에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-159">The default implementation is provided by the **DefaultHttpControllerSelector** class.</span></span> <span data-ttu-id="94a5b-160">이 클래스는 간단한 알고리즘을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-160">This class uses a straightforward algorithm:</span></span>

1. <span data-ttu-id="94a5b-161">"컨트롤러" 키에 대 한 경로 사전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-161">Look in the route dictionary for the key "controller".</span></span>
2. <span data-ttu-id="94a5b-162">이 키의 값을 가져와 "Controller" 문자열을 추가 하 여 컨트롤러 유형 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-162">Take the value for this key and append the string "Controller" to get the controller type name.</span></span>
3. <span data-ttu-id="94a5b-163">이 형식 이름을 사용 하 여 Web API 컨트롤러를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-163">Look for a Web API controller with this type name.</span></span>

<span data-ttu-id="94a5b-164">예를 들어 경로 사전에 키-값 쌍 "controller" = "products"가 포함 되어 있으면 컨트롤러 유형은 "ProductsController"입니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-164">For example, if the route dictionary contains the key-value pair "controller" = "products", then the controller type is "ProductsController".</span></span> <span data-ttu-id="94a5b-165">일치 하는 형식 또는 여러 일치 항목이 없는 경우 프레임 워크는 클라이언트에 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-165">If there is no matching type, or multiple matches, the framework returns an error to the client.</span></span>

<span data-ttu-id="94a5b-166">3 단계에서 **DefaultHttpControllerSelector** 는 **IHttpControllerTypeResolver** 인터페이스를 사용 하 여 Web API 컨트롤러 유형 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-166">For step 3, **DefaultHttpControllerSelector** uses the **IHttpControllerTypeResolver** interface to get the list of Web API controller types.</span></span> <span data-ttu-id="94a5b-167">**IHttpControllerTypeResolver** 의 기본 구현에서는 (a) **IHttpController**를 구현 하는 모든 public 클래스 (b)가 abstract가 아니고 (c)에 "Controller"로 끝나는 모든 public 클래스를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-167">The default implementation of **IHttpControllerTypeResolver** returns all public classes that (a) implement **IHttpController**, (b) are not abstract, and (c) have a name that ends in "Controller".</span></span>

## <a name="action-selection"></a><span data-ttu-id="94a5b-168">작업 선택</span><span class="sxs-lookup"><span data-stu-id="94a5b-168">Action Selection</span></span>

<span data-ttu-id="94a5b-169">컨트롤러를 선택한 후 프레임 워크는 **IHttpActionSelector 작업** 메서드를 호출 하 여 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-169">After selecting the controller, the framework selects the action by calling the **IHttpActionSelector.SelectAction** method.</span></span> <span data-ttu-id="94a5b-170">이 메서드는 **Httpcontrollercontext** 를 사용 하 고 **httpcontrollercontext**를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-170">This method takes an **HttpControllerContext** and returns an **HttpActionDescriptor**.</span></span>

<span data-ttu-id="94a5b-171">기본 구현은 **ApiControllerActionSelector** 클래스에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-171">The default implementation is provided by the **ApiControllerActionSelector** class.</span></span> <span data-ttu-id="94a5b-172">작업을 선택 하려면 다음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-172">To select an action, it looks at the following:</span></span>

- <span data-ttu-id="94a5b-173">요청의 HTTP 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-173">The HTTP method of the request.</span></span>
- <span data-ttu-id="94a5b-174">경로 템플릿의 "{action}" 자리 표시자 (있는 경우)입니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-174">The "{action}" placeholder in the route template, if present.</span></span>
- <span data-ttu-id="94a5b-175">컨트롤러에 대 한 작업의 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-175">The parameters of the actions on the controller.</span></span>

<span data-ttu-id="94a5b-176">선택 알고리즘을 확인 하기 전에 컨트롤러 작업에 대 한 몇 가지 사항을 이해 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-176">Before looking at the selection algorithm, we need to understand some things about controller actions.</span></span>

<span data-ttu-id="94a5b-177">**"작업"으로 간주 되는 컨트롤러의 메서드는 무엇입니까?**</span><span class="sxs-lookup"><span data-stu-id="94a5b-177">**Which methods on the controller are considered "actions"?**</span></span> <span data-ttu-id="94a5b-178">작업을 선택 하는 경우 프레임 워크는 컨트롤러의 공용 인스턴스 메서드만 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-178">When selecting an action, the framework only looks at public instance methods on the controller.</span></span> <span data-ttu-id="94a5b-179">또한 ["특수 이름"](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname) 메서드 (생성자, 이벤트, 연산자 오버 로드 등) 및 **ApiController** 클래스에서 상속 된 메서드를 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-179">Also, it excludes ["special name"](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname) methods (constructors, events, operator overloads, and so forth), and methods inherited from the **ApiController** class.</span></span>

<span data-ttu-id="94a5b-180">**HTTP 메서드.**</span><span class="sxs-lookup"><span data-stu-id="94a5b-180">**HTTP Methods.**</span></span> <span data-ttu-id="94a5b-181">프레임 워크는 요청의 HTTP 메서드와 일치 하는 동작만 선택 하 고 다음과 같이 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-181">The framework only chooses actions that match the HTTP method of the request, determined as follows:</span></span>

1. <span data-ttu-id="94a5b-182">특성을 사용 하 여 HTTP 메서드 ( **Acceptverbs**, **httpdelete**, **HttpGet**, **httpdelete**, **Httpdelete**, **httpdelete**, **HttpPost**또는 **httpdelete**)를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-182">You can specify the HTTP method with an attribute: **AcceptVerbs**, **HttpDelete**, **HttpGet**, **HttpHead**, **HttpOptions**, **HttpPatch**, **HttpPost**, or **HttpPut**.</span></span>
2. <span data-ttu-id="94a5b-183">그렇지 않고 컨트롤러 메서드의 이름이 "Get", "Post", "Put", "Delete", "Head", "Options" 또는 "Patch"로 시작 하는 경우이 작업은 해당 HTTP 메서드를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-183">Otherwise, if the name of the controller method starts with "Get", "Post", "Put", "Delete", "Head", "Options", or "Patch", then by convention the action supports that HTTP method.</span></span>
3. <span data-ttu-id="94a5b-184">위의 항목이 없으면 메서드는 POST를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-184">If none of the above, the method supports POST.</span></span>

<span data-ttu-id="94a5b-185">**매개 변수 바인딩입니다.**</span><span class="sxs-lookup"><span data-stu-id="94a5b-185">**Parameter Bindings.**</span></span> <span data-ttu-id="94a5b-186">매개 변수 바인딩은 Web API가 매개 변수 값을 만드는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-186">A parameter binding is how Web API creates a value for a parameter.</span></span> <span data-ttu-id="94a5b-187">매개 변수 바인딩에 대 한 기본 규칙은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-187">Here is the default rule for parameter binding:</span></span>

- <span data-ttu-id="94a5b-188">단순 형식은 URI에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-188">Simple types are taken from the URI.</span></span>
- <span data-ttu-id="94a5b-189">복합 형식은 요청 본문에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-189">Complex types are taken from the request body.</span></span>

<span data-ttu-id="94a5b-190">단순 형식에는 모든 [.NET Framework 기본 형식](https://msdn.microsoft.com/library/system.type.isprimitive)및 **DateTime**, **Decimal**, **Guid**, **String**및 **TimeSpan**이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-190">Simple types include all of the [.NET Framework primitive types](https://msdn.microsoft.com/library/system.type.isprimitive), plus **DateTime**, **Decimal**, **Guid**, **String**, and **TimeSpan**.</span></span> <span data-ttu-id="94a5b-191">각 작업에 대해 최대 하나의 매개 변수는 요청 본문을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-191">For each action, at most one parameter can read the request body.</span></span>

> [!NOTE]
> <span data-ttu-id="94a5b-192">기본 바인딩 규칙을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-192">It is possible to override the default binding rules.</span></span> <span data-ttu-id="94a5b-193">[WebAPI 매개 변수 바인딩은 내부적으로](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="94a5b-193">See [WebAPI Parameter binding under the hood](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx).</span></span>

<span data-ttu-id="94a5b-194">이 배경에서 작업 선택 알고리즘은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-194">With that background, here is the action selection algorithm.</span></span>

1. <span data-ttu-id="94a5b-195">컨트롤러에서 HTTP 요청 메서드와 일치 하는 모든 작업의 목록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-195">Create a list of all actions on the controller that match the HTTP request method.</span></span>
2. <span data-ttu-id="94a5b-196">경로 사전에 "action" 항목이 있는 경우 이름이이 값과 일치 하지 않는 작업을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-196">If the route dictionary has an "action" entry, remove actions whose name does not match this value.</span></span>
3. <span data-ttu-id="94a5b-197">다음과 같이 작업 매개 변수를 URI에 일치 시 키 려 고 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-197">Try to match action parameters to the URI, as follows:</span></span> 

    1. <span data-ttu-id="94a5b-198">각 작업에 대해 단순 형식인 매개 변수 목록을 가져옵니다. 여기서 바인딩은 URI에서 매개 변수를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-198">For each action, get a list of the parameters that are a simple type, where the binding gets the parameter from the URI.</span></span> <span data-ttu-id="94a5b-199">선택적 매개 변수를 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-199">Exclude optional parameters.</span></span>
    2. <span data-ttu-id="94a5b-200">이 목록에서 경로 사전 또는 URI 쿼리 문자열에서 각 매개 변수 이름에 대 한 일치 항목 찾기를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-200">From this list, try to find a match for each parameter name, either in the route dictionary or in the URI query string.</span></span> <span data-ttu-id="94a5b-201">일치는 대/소문자를 구분 하지 않으며 매개 변수 순서에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-201">Matches are case insensitive and do not depend on the parameter order.</span></span>
    3. <span data-ttu-id="94a5b-202">목록의 모든 매개 변수가 URI에서 일치 하는 항목을 포함 하는 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-202">Select an action where every parameter in the list has a match in the URI.</span></span>
    4. <span data-ttu-id="94a5b-203">하나 이상의 작업이 이러한 조건을 충족 하는 경우 가장 많은 매개 변수 일치 항목을 사용 하 여 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-203">If more that one action meets these criteria, pick the one with the most parameter matches.</span></span>
4. <span data-ttu-id="94a5b-204">**[Nonaction]** 특성이 있는 동작을 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-204">Ignore actions with the **[NonAction]** attribute.</span></span>

<span data-ttu-id="94a5b-205">#3 단계가 가장 혼란 스 러 울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-205">Step #3 is probably the most confusing.</span></span> <span data-ttu-id="94a5b-206">기본 개념은 매개 변수가 URI, 요청 본문 또는 사용자 지정 바인딩에서 해당 값을 가져올 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-206">The basic idea is that a parameter can get its value either from the URI, from the request body, or from a custom binding.</span></span> <span data-ttu-id="94a5b-207">URI에서 제공 되는 매개 변수의 경우 URI에 실제로 경로 (경로 사전) 또는 쿼리 문자열의 해당 매개 변수에 대 한 값이 포함 되어 있는지 확인 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-207">For parameters that come from the URI, we want to ensure that the URI actually contains a value for that parameter, either in the path (via the route dictionary) or in the query string.</span></span>

<span data-ttu-id="94a5b-208">예를 들어 다음 작업을 고려 하십시오.</span><span class="sxs-lookup"><span data-stu-id="94a5b-208">For example, consider the following action:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample7.cs)]

<span data-ttu-id="94a5b-209">*Id* 매개 변수는 URI에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-209">The *id* parameter binds to the URI.</span></span> <span data-ttu-id="94a5b-210">따라서이 작업은 경로 사전 또는 쿼리 문자열에 "id"의 값을 포함 하는 URI만 일치 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-210">Therefore, this action can only match a URI that contains a value for "id", either in the route dictionary or in the query string.</span></span>

<span data-ttu-id="94a5b-211">선택적 매개 변수는 선택 사항 이므로 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-211">Optional parameters are an exception, because they are optional.</span></span> <span data-ttu-id="94a5b-212">선택적 매개 변수의 경우 바인딩이 URI에서 값을 가져올 수 없는 경우 정상입니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-212">For an optional parameter, it's OK if the binding can't get the value from the URI.</span></span>

<span data-ttu-id="94a5b-213">복합 형식은 다른 이유로 인 한 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-213">Complex types are an exception for a different reason.</span></span> <span data-ttu-id="94a5b-214">복합 형식은 사용자 지정 바인딩을 통해 URI에만 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-214">A complex type can only bind to the URI through a custom binding.</span></span> <span data-ttu-id="94a5b-215">그러나이 경우 프레임 워크는 매개 변수가 특정 URI에 바인딩 되었는지 여부를 미리 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-215">But in that case, the framework cannot know in advance whether the parameter would bind to a particular URI.</span></span> <span data-ttu-id="94a5b-216">이를 확인 하려면 바인딩을 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-216">To find out, it would need to invoke the binding.</span></span> <span data-ttu-id="94a5b-217">선택 알고리즘의 목표는 바인딩을 호출 하기 전에 정적 설명에서 작업을 선택 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-217">The goal of the selection algorithm is to select an action from the static description, before invoking any bindings.</span></span> <span data-ttu-id="94a5b-218">따라서 복합 형식은 일치 알고리즘에서 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-218">Therefore, complex types are excluded from the matching algorithm.</span></span>

<span data-ttu-id="94a5b-219">동작을 선택 하면 모든 매개 변수 바인딩이 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-219">After the action is selected, all parameter bindings are invoked.</span></span>

<span data-ttu-id="94a5b-220">요약:</span><span class="sxs-lookup"><span data-stu-id="94a5b-220">Summary:</span></span>

- <span data-ttu-id="94a5b-221">작업은 요청의 HTTP 메서드와 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-221">The action must match the HTTP method of the request.</span></span>
- <span data-ttu-id="94a5b-222">작업 이름은 경로 사전의 "action" 항목과 일치 해야 합니다 (있는 경우).</span><span class="sxs-lookup"><span data-stu-id="94a5b-222">The action name must match the "action" entry in the route dictionary, if present.</span></span>
- <span data-ttu-id="94a5b-223">작업의 모든 매개 변수에 대해 매개 변수를 URI에서 가져온 경우 매개 변수 이름은 경로 사전 또는 URI 쿼리 문자열에서 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-223">For every parameter of the action, if the parameter is taken from the URI, then the parameter name must be found either in the route dictionary or in the URI query string.</span></span> <span data-ttu-id="94a5b-224">복합 형식을 사용 하는 선택적 매개 변수 및 매개 변수는 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-224">(Optional parameters and parameters with complex types are excluded.)</span></span>
- <span data-ttu-id="94a5b-225">가장 많은 수의 매개 변수를 일치 시 키 려 고 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-225">Try to match the most number of parameters.</span></span> <span data-ttu-id="94a5b-226">가장 일치 하는 항목은 매개 변수가 없는 메서드 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-226">The best match might be a method with no parameters.</span></span>

## <a name="extended-example"></a><span data-ttu-id="94a5b-227">확장 된 예제</span><span class="sxs-lookup"><span data-stu-id="94a5b-227">Extended Example</span></span>

<span data-ttu-id="94a5b-228">라우트에</span><span class="sxs-lookup"><span data-stu-id="94a5b-228">Routes:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample8.cs)]

<span data-ttu-id="94a5b-229">컨트롤러:</span><span class="sxs-lookup"><span data-stu-id="94a5b-229">Controller:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample9.cs)]

<span data-ttu-id="94a5b-230">HTTP 요청:</span><span class="sxs-lookup"><span data-stu-id="94a5b-230">HTTP request:</span></span>

[!code-console[Main](routing-and-action-selection/samples/sample10.cmd)]

### <a name="route-matching"></a><span data-ttu-id="94a5b-231">경로 일치</span><span class="sxs-lookup"><span data-stu-id="94a5b-231">Route Matching</span></span>

<span data-ttu-id="94a5b-232">URI는 이름이 "DefaultApi" 인 경로와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-232">The URI matches the route named "DefaultApi".</span></span> <span data-ttu-id="94a5b-233">경로 사전에는 다음 항목이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-233">The route dictionary contains the following entries:</span></span>

- <span data-ttu-id="94a5b-234">컨트롤러: "제품"</span><span class="sxs-lookup"><span data-stu-id="94a5b-234">controller: "products"</span></span>
- <span data-ttu-id="94a5b-235">id: "1"</span><span class="sxs-lookup"><span data-stu-id="94a5b-235">id: "1"</span></span>

<span data-ttu-id="94a5b-236">경로 사전에 쿼리 문자열 매개 변수 "version" 및 "details"가 포함 되어 있지 않지만 작업을 선택 하는 동안에는이 매개 변수를 계속 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-236">The route dictionary does not contain the query string parameters, "version" and "details", but these will still be considered during action selection.</span></span>

### <a name="controller-selection"></a><span data-ttu-id="94a5b-237">컨트롤러 선택</span><span class="sxs-lookup"><span data-stu-id="94a5b-237">Controller Selection</span></span>

<span data-ttu-id="94a5b-238">경로 사전의 "컨트롤러" 항목에서 컨트롤러 유형이 `ProductsController`입니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-238">From the "controller" entry in the route dictionary, the controller type is `ProductsController`.</span></span>

### <a name="action-selection"></a><span data-ttu-id="94a5b-239">작업 선택</span><span class="sxs-lookup"><span data-stu-id="94a5b-239">Action Selection</span></span>

<span data-ttu-id="94a5b-240">HTTP 요청은 GET 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-240">The HTTP request is a GET request.</span></span> <span data-ttu-id="94a5b-241">GET을 지 원하는 컨트롤러 작업은 `GetAll`, `GetById`및 `FindProductsByName`입니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-241">The controller actions that support GET are `GetAll`, `GetById`, and `FindProductsByName`.</span></span> <span data-ttu-id="94a5b-242">경로 사전이 "action"에 대 한 항목을 포함 하지 않으므로 작업 이름과 일치 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-242">The route dictionary does not contain an entry for "action", so we don't need to match the action name.</span></span>

<span data-ttu-id="94a5b-243">다음으로 작업에 대 한 매개 변수 이름을 일치 시키고 GET 동작만 검색 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-243">Next, we try to match parameter names for the actions, looking only at the GET actions.</span></span>

| <span data-ttu-id="94a5b-244">작업</span><span class="sxs-lookup"><span data-stu-id="94a5b-244">Action</span></span> | <span data-ttu-id="94a5b-245">일치 시킬 매개 변수</span><span class="sxs-lookup"><span data-stu-id="94a5b-245">Parameters to Match</span></span> |
| --- | --- |
| `GetAll` | <span data-ttu-id="94a5b-246">none</span><span class="sxs-lookup"><span data-stu-id="94a5b-246">none</span></span> |
| `GetById` | <span data-ttu-id="94a5b-247">"id"</span><span class="sxs-lookup"><span data-stu-id="94a5b-247">"id"</span></span> |
| `FindProductsByName` | <span data-ttu-id="94a5b-248">이름의</span><span class="sxs-lookup"><span data-stu-id="94a5b-248">"name"</span></span> |

<span data-ttu-id="94a5b-249">`GetById`의 *version* 매개 변수는 선택적 매개 변수 이기 때문에 고려 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-249">Notice that the *version* parameter of `GetById` is not considered, because it is an optional parameter.</span></span>

<span data-ttu-id="94a5b-250">`GetAll` 메서드는 일반적으로와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-250">The `GetAll` method matches trivially.</span></span> <span data-ttu-id="94a5b-251">경로 사전이 "id"를 포함 하기 때문에 `GetById` 메서드도 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-251">The `GetById` method also matches, because the route dictionary contains "id".</span></span> <span data-ttu-id="94a5b-252">`FindProductsByName` 메서드가와 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-252">The `FindProductsByName` method does not match.</span></span>

<span data-ttu-id="94a5b-253">`GetById` 메서드는 `GetAll`에 대 한 매개 변수 및 매개 변수는 일치 하지 않으므로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-253">The `GetById` method wins, because it matches one parameter, versus no parameters for `GetAll`.</span></span> <span data-ttu-id="94a5b-254">메서드는 다음 매개 변수 값을 사용 하 여 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-254">The method is invoked with the following parameter values:</span></span>

- <span data-ttu-id="94a5b-255">*id* = 1</span><span class="sxs-lookup"><span data-stu-id="94a5b-255">*id* = 1</span></span>
- <span data-ttu-id="94a5b-256">*버전* = 1.5</span><span class="sxs-lookup"><span data-stu-id="94a5b-256">*version* = 1.5</span></span>

<span data-ttu-id="94a5b-257">선택 알고리즘에서 *버전* 을 사용 하지 않은 경우에도 매개 변수 값은 URI 쿼리 문자열에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-257">Notice that even though *version* was not used in the selection algorithm, the value of the parameter comes from the URI query string.</span></span>

## <a name="extension-points"></a><span data-ttu-id="94a5b-258">확장점</span><span class="sxs-lookup"><span data-stu-id="94a5b-258">Extension Points</span></span>

<span data-ttu-id="94a5b-259">Web API는 라우팅 프로세스의 일부에 대 한 확장 위치를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-259">Web API provides extension points for some parts of the routing process.</span></span>

| <span data-ttu-id="94a5b-260">인터페이스</span><span class="sxs-lookup"><span data-stu-id="94a5b-260">Interface</span></span> | <span data-ttu-id="94a5b-261">Description</span><span class="sxs-lookup"><span data-stu-id="94a5b-261">Description</span></span> |
| --- | --- |
| <span data-ttu-id="94a5b-262">**IHttpControllerSelector**</span><span class="sxs-lookup"><span data-stu-id="94a5b-262">**IHttpControllerSelector**</span></span> | <span data-ttu-id="94a5b-263">컨트롤러를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-263">Selects the controller.</span></span> |
| <span data-ttu-id="94a5b-264">**IHttpControllerTypeResolver**</span><span class="sxs-lookup"><span data-stu-id="94a5b-264">**IHttpControllerTypeResolver**</span></span> | <span data-ttu-id="94a5b-265">컨트롤러 유형 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-265">Gets the list of controller types.</span></span> <span data-ttu-id="94a5b-266">**DefaultHttpControllerSelector** 는이 목록에서 컨트롤러 유형을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-266">The **DefaultHttpControllerSelector** chooses the controller type from this list.</span></span> |
| <span data-ttu-id="94a5b-267">**IAssembliesResolver**</span><span class="sxs-lookup"><span data-stu-id="94a5b-267">**IAssembliesResolver**</span></span> | <span data-ttu-id="94a5b-268">프로젝트 어셈블리의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-268">Gets the list of project assemblies.</span></span> <span data-ttu-id="94a5b-269">**IHttpControllerTypeResolver** 인터페이스는이 목록을 사용 하 여 컨트롤러 유형을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-269">The **IHttpControllerTypeResolver** interface uses this list to find the controller types.</span></span> |
| <span data-ttu-id="94a5b-270">**IHttpControllerActivator**</span><span class="sxs-lookup"><span data-stu-id="94a5b-270">**IHttpControllerActivator**</span></span> | <span data-ttu-id="94a5b-271">새 컨트롤러 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-271">Creates new controller instances.</span></span> |
| <span data-ttu-id="94a5b-272">**IHttpActionSelector**</span><span class="sxs-lookup"><span data-stu-id="94a5b-272">**IHttpActionSelector**</span></span> | <span data-ttu-id="94a5b-273">작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-273">Selects the action.</span></span> |
| <span data-ttu-id="94a5b-274">**IHttpActionInvoker**</span><span class="sxs-lookup"><span data-stu-id="94a5b-274">**IHttpActionInvoker**</span></span> | <span data-ttu-id="94a5b-275">동작을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-275">Invokes the action.</span></span> |

<span data-ttu-id="94a5b-276">이러한 인터페이스에 대 한 고유한 구현을 제공 하려면 **Httpconfiguration** 개체에서 **서비스** 컬렉션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="94a5b-276">To provide your own implementation for any of these interfaces, use the **Services** collection on the **HttpConfiguration** object:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample11.cs)]
