---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: ASP.NET Web API 2에서 특성 라우팅 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 7da1805d8a7066e82743dc9bd7e024cc9813ee89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446999"
---
# <a name="attribute-routing-in-aspnet-web-api-2"></a><span data-ttu-id="5c81d-102">ASP.NET Web API 2에서 특성 라우팅</span><span class="sxs-lookup"><span data-stu-id="5c81d-102">Attribute Routing in ASP.NET Web API 2</span></span>

<span data-ttu-id="5c81d-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="5c81d-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="5c81d-104">*라우팅은* 웹 API가 작업에 대 한 URI와 일치 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-104">*Routing* is how Web API matches a URI to an action.</span></span> <span data-ttu-id="5c81d-105">Web API 2는 *특성 라우팅*이라는 새로운 유형의 라우팅을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-105">Web API 2 supports a new type of routing, called *attribute routing*.</span></span> <span data-ttu-id="5c81d-106">이름에서 알 수 있듯이 특성 라우팅은 경로를 정의 하는 특성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-106">As the name implies, attribute routing uses attributes to define routes.</span></span> <span data-ttu-id="5c81d-107">특성 라우팅은 웹 API에서 Uri를 보다 강력 하 게 제어할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-107">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="5c81d-108">예를 들어 리소스 계층 구조를 설명 하는 Uri를 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-108">For example, you can easily create URIs that describe hierarchies of resources.</span></span>

<span data-ttu-id="5c81d-109">규칙 기반 라우팅 이라고 하는 이전 라우팅 스타일은 여전히 완전 하 게 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-109">The earlier style of routing, called convention-based routing, is still fully supported.</span></span> <span data-ttu-id="5c81d-110">실제로 동일한 프로젝트에서 두 기법을 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-110">In fact, you can combine both techniques in the same project.</span></span>

<span data-ttu-id="5c81d-111">이 항목에서는 특성 라우팅을 사용 하도록 설정 하 고 특성 라우팅에 대 한 다양 한 옵션을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-111">This topic shows how to enable attribute routing and describes the various options for attribute routing.</span></span> <span data-ttu-id="5c81d-112">특성 라우팅을 사용 하는 종단 간 자습서는 [WEB API 2에서 특성 라우팅을 사용 하 여 REST API 만들기](create-a-rest-api-with-attribute-routing.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5c81d-112">For an end-to-end tutorial that uses attribute routing, see [Create a REST API with Attribute Routing in Web API 2](create-a-rest-api-with-attribute-routing.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c81d-113">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="5c81d-113">Prerequisites</span></span>

<span data-ttu-id="5c81d-114">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional 또는 Enterprise edition</span><span class="sxs-lookup"><span data-stu-id="5c81d-114">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional, or Enterprise edition</span></span>

<span data-ttu-id="5c81d-115">또는 NuGet 패키지 관리자를 사용 하 여 필요한 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-115">Alternatively, use NuGet Package Manager to install the necessary packages.</span></span> <span data-ttu-id="5c81d-116">Visual Studio의 **도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-116">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="5c81d-117">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-117">Enter the following command in the Package Manager Console window:</span></span>

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a><span data-ttu-id="5c81d-118">특성을 라우팅하는 이유</span><span class="sxs-lookup"><span data-stu-id="5c81d-118">Why Attribute Routing?</span></span>

<span data-ttu-id="5c81d-119">Web API의 첫 번째 릴리스는 *규칙 기반* 라우팅을 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-119">The first release of Web API used *convention-based* routing.</span></span> <span data-ttu-id="5c81d-120">해당 라우팅 형식에서 기본적으로 매개 변수가 있는 문자열인 경로 템플릿을 하나 이상 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-120">In that type of routing, you define one or more route templates, which are basically parameterized strings.</span></span> <span data-ttu-id="5c81d-121">프레임 워크는 요청을 받으면 경로 템플릿과 URI를 일치 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-121">When the framework receives a request, it matches the URI against the route template.</span></span> <span data-ttu-id="5c81d-122">규칙 기반 라우팅에 대 한 자세한 내용은 [ASP.NET Web API 라우팅](routing-in-aspnet-web-api.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5c81d-122">(For more information about convention-based routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>

<span data-ttu-id="5c81d-123">규칙 기반 라우팅의 이점 중 하나는 템플릿이 단일 장소에서 정의 되 고 라우팅 규칙이 모든 컨트롤러에서 일관 되 게 적용 된다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-123">One advantage of convention-based routing is that templates are defined in a single place, and the routing rules are applied consistently across all controllers.</span></span> <span data-ttu-id="5c81d-124">불행 하 게도 규칙 기반 라우팅은 RESTful Api에서 공통적으로 사용 되는 특정 URI 패턴을 지원 하기 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-124">Unfortunately, convention-based routing makes it hard to support certain URI patterns that are common in RESTful APIs.</span></span> <span data-ttu-id="5c81d-125">예를 들어, 리소스에는 고객에 게 주문이 있고, 영화에는 행위자가 있으며, 책은 저자와 같은 하위 리소스가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-125">For example, resources often contain child resources: Customers have orders, movies have actors, books have authors, and so forth.</span></span> <span data-ttu-id="5c81d-126">이러한 관계를 반영 하는 Uri를 만드는 것은 자연스럽 게 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-126">It's natural to create URIs that reflect these relations:</span></span>

`/customers/1/orders`

<span data-ttu-id="5c81d-127">이러한 유형의 URI는 규칙 기반 라우팅을 사용 하 여 만드는 것이 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-127">This type of URI is difficult to create using convention-based routing.</span></span> <span data-ttu-id="5c81d-128">이 작업을 수행할 수 있지만 컨트롤러 또는 리소스 종류가 많은 경우 결과가 제대로 확장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-128">Although it can be done, the results don't scale well if you have many controllers or resource types.</span></span>

<span data-ttu-id="5c81d-129">특성 라우팅을 사용 하 여이 URI에 대 한 경로를 정의 하는 것은 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-129">With attribute routing, it's trivial to define a route for this URI.</span></span> <span data-ttu-id="5c81d-130">단순히 컨트롤러 작업에 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-130">You simply add an attribute to the controller action:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

<span data-ttu-id="5c81d-131">특성 라우팅이 용이 하 게 하는 몇 가지 다른 패턴은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-131">Here are some other patterns that attribute routing makes easy.</span></span>

<span data-ttu-id="5c81d-132">**API 버전 관리**</span><span class="sxs-lookup"><span data-stu-id="5c81d-132">**API versioning**</span></span>

<span data-ttu-id="5c81d-133">이 예제에서 "/api/v1/products"는 "/api/v2/products"가 아닌 다른 컨트롤러로 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-133">In this example, "/api/v1/products" would be routed to a different controller than "/api/v2/products".</span></span>

`/api/v1/products`
`/api/v2/products`

<span data-ttu-id="5c81d-134">**오버 로드 된 URI 세그먼트**</span><span class="sxs-lookup"><span data-stu-id="5c81d-134">**Overloaded URI segments**</span></span>

<span data-ttu-id="5c81d-135">이 예제에서 "1"은 주문 번호 이지만 "보류 중"은 컬렉션에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-135">In this example, "1" is an order number, but "pending" maps to a collection.</span></span>

`/orders/1`
`/orders/pending`

<span data-ttu-id="5c81d-136">**여러 매개 변수 형식**</span><span class="sxs-lookup"><span data-stu-id="5c81d-136">**Multiple parameter types**</span></span>

<span data-ttu-id="5c81d-137">이 예에서 "1"은 주문 번호 이지만 "2013/06/16"은 날짜를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-137">In this example, "1" is an order number, but "2013/06/16" specifies a date.</span></span>

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a><span data-ttu-id="5c81d-138">특성 라우팅 사용</span><span class="sxs-lookup"><span data-stu-id="5c81d-138">Enabling Attribute Routing</span></span>

<span data-ttu-id="5c81d-139">특성 라우팅을 사용 하도록 설정 하려면 구성 하는 동안 **Maphttpattributeroutes** 를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-139">To enable attribute routing, call **MapHttpAttributeRoutes** during configuration.</span></span> <span data-ttu-id="5c81d-140">이 확장 메서드는 **system.web. HttpConfigurationExtensions** 클래스에서 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-140">This extension method is defined in the **System.Web.Http.HttpConfigurationExtensions** class.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

<span data-ttu-id="5c81d-141">특성 라우팅은 [규칙 기반](routing-in-aspnet-web-api.md) 라우팅과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-141">Attribute routing can be combined with [convention-based](routing-in-aspnet-web-api.md) routing.</span></span> <span data-ttu-id="5c81d-142">규칙 기반 경로를 정의 하려면 **MapHttpRoute** 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-142">To define convention-based routes, call the **MapHttpRoute** method.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

<span data-ttu-id="5c81d-143">Web API를 구성 하는 방법에 대 한 자세한 내용은 [ASP.NET Web API 2 구성](../advanced/configuring-aspnet-web-api.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5c81d-143">For more information about configuring Web API, see [Configuring ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md).</span></span>

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a><span data-ttu-id="5c81d-144">참고: Web API 1에서 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="5c81d-144">Note: Migrating From Web API 1</span></span>

<span data-ttu-id="5c81d-145">Web API 2 이전에 웹 API 프로젝트 템플릿은 다음과 같은 코드를 생성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-145">Prior to Web API 2, the Web API project templates generated code like this:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

<span data-ttu-id="5c81d-146">특성 라우팅이 사용 되는 경우이 코드는 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-146">If attribute routing is enabled, this code will throw an exception.</span></span> <span data-ttu-id="5c81d-147">특성 라우팅을 사용 하도록 기존 Web API 프로젝트를 업그레이드 하는 경우이 구성 코드를 다음으로 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-147">If you upgrade an existing Web API project to use attribute routing, make sure to update this configuration code to the following:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> <span data-ttu-id="5c81d-148">자세한 내용은 [ASP.NET 호스팅을 사용 하 여 WEB API 구성](../advanced/configuring-aspnet-web-api.md#webhost)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5c81d-148">For more information, see [Configuring Web API with ASP.NET Hosting](../advanced/configuring-aspnet-web-api.md#webhost).</span></span>

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a><span data-ttu-id="5c81d-149">경로 특성 추가</span><span class="sxs-lookup"><span data-stu-id="5c81d-149">Adding Route Attributes</span></span>

<span data-ttu-id="5c81d-150">특성을 사용 하 여 정의 된 경로의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-150">Here is an example of a route defined using an attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

<span data-ttu-id="5c81d-151">&quot;customers/{customerId}/orders&quot; 문자열은 경로에 대 한 URI 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-151">The string &quot;customers/{customerId}/orders&quot; is the URI template for the route.</span></span> <span data-ttu-id="5c81d-152">Web API는 요청 URI를 템플릿에 일치 시 키 려 고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-152">Web API tries to match the request URI to the template.</span></span> <span data-ttu-id="5c81d-153">이 예에서 "customers" 및 "orders"는 리터럴 세그먼트 이며 "{customerId}"는 변수 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-153">In this example, "customers" and "orders" are literal segments, and "{customerId}" is a variable parameter.</span></span> <span data-ttu-id="5c81d-154">다음 Uri는이 템플릿과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-154">The following URIs would match this template:</span></span>

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

<span data-ttu-id="5c81d-155">이 항목의 뒷부분에서 설명 하는 [제약 조건을](#constraints)사용 하 여 일치를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-155">You can restrict the matching by using [constraints](#constraints), described later in this topic.</span></span>

<span data-ttu-id="5c81d-156">경로 템플릿의 &quot;{customerId}&quot; 매개 변수가 메서드의 *customerId* 매개 변수 이름과 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-156">Notice that the &quot;{customerId}&quot; parameter in the route template matches the name of the *customerId* parameter in the method.</span></span> <span data-ttu-id="5c81d-157">Web API는 컨트롤러 작업을 호출할 때 경로 매개 변수를 바인딩하려 려 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-157">When Web API invokes the controller action, it tries to bind the route parameters.</span></span> <span data-ttu-id="5c81d-158">예를 들어 URI가 `http://example.com/customers/1/orders`되는 경우 Web API는 동작의 *customerId* 매개 변수에 "1" 값을 바인딩하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-158">For example, if the URI is `http://example.com/customers/1/orders`, Web API tries to bind the value "1" to the *customerId* parameter in the action.</span></span>

<span data-ttu-id="5c81d-159">URI 템플릿에는 여러 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-159">A URI template can have several parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

<span data-ttu-id="5c81d-160">경로 특성이 없는 컨트롤러 메서드는 규칙 기반 라우팅을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-160">Any controller methods that do not have a route attribute use convention-based routing.</span></span> <span data-ttu-id="5c81d-161">이런 방식으로 동일한 프로젝트에서 두 가지 유형의 라우팅을 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-161">That way, you can combine both types of routing in the same project.</span></span>

## <a name="http-methods"></a><span data-ttu-id="5c81d-162">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="5c81d-162">HTTP Methods</span></span>

<span data-ttu-id="5c81d-163">웹 API는 또한 요청의 HTTP 메서드 (GET, POST 등)를 기반으로 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-163">Web API also selects actions based on the HTTP method of the request (GET, POST, etc).</span></span> <span data-ttu-id="5c81d-164">기본적으로 웹 API는 컨트롤러 메서드 이름의 시작과 함께 대/소문자를 구분 하지 않는 일치 항목을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-164">By default, Web API looks for a case-insensitive match with the start of the controller method name.</span></span> <span data-ttu-id="5c81d-165">예를 들어 `PutCustomers` 라는 컨트롤러 메서드는 HTTP PUT 요청과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-165">For example, a controller method named `PutCustomers` matches an HTTP PUT request.</span></span>

<span data-ttu-id="5c81d-166">메서드를 다음 특성으로 데코레이팅 하 여이 규칙을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-166">You can override this convention by decorating the method with any the following attributes:</span></span>

- <span data-ttu-id="5c81d-167">**HttpDelete**</span><span class="sxs-lookup"><span data-stu-id="5c81d-167">**[HttpDelete]**</span></span>
- <span data-ttu-id="5c81d-168">**[HttpGet]**</span><span class="sxs-lookup"><span data-stu-id="5c81d-168">**[HttpGet]**</span></span>
- <span data-ttu-id="5c81d-169">**[HttpHead]**</span><span class="sxs-lookup"><span data-stu-id="5c81d-169">**[HttpHead]**</span></span>
- <span data-ttu-id="5c81d-170">**[HttpOptions]**</span><span class="sxs-lookup"><span data-stu-id="5c81d-170">**[HttpOptions]**</span></span>
- <span data-ttu-id="5c81d-171">**[HttpPatch]**</span><span class="sxs-lookup"><span data-stu-id="5c81d-171">**[HttpPatch]**</span></span>
- <span data-ttu-id="5c81d-172">**HttpPost**</span><span class="sxs-lookup"><span data-stu-id="5c81d-172">**[HttpPost]**</span></span>
- <span data-ttu-id="5c81d-173">**HttpPut**</span><span class="sxs-lookup"><span data-stu-id="5c81d-173">**[HttpPut]**</span></span>

<span data-ttu-id="5c81d-174">다음 예제에서는 CreateBook 메서드를 HTTP POST 요청에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-174">The following example maps the CreateBook method to HTTP POST requests.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

<span data-ttu-id="5c81d-175">비표준 메서드를 비롯 한 다른 모든 HTTP 메서드의 경우 HTTP 메서드 목록을 사용 하는 **Acceptverbs** 특성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-175">For all other HTTP methods, including non-standard methods, use the **AcceptVerbs** attribute, which takes a list of HTTP methods.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a><span data-ttu-id="5c81d-176">경로 접두사</span><span class="sxs-lookup"><span data-stu-id="5c81d-176">Route Prefixes</span></span>

<span data-ttu-id="5c81d-177">컨트롤러의 경로는 모두 동일한 접두사로 시작 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-177">Often, the routes in a controller all start with the same prefix.</span></span> <span data-ttu-id="5c81d-178">다음은 그 예입니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-178">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

<span data-ttu-id="5c81d-179">**[RoutePrefix]** 특성을 사용 하 여 전체 컨트롤러에 대 한 공통 접두사를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-179">You can set a common prefix for an entire controller by using the **[RoutePrefix]** attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

<span data-ttu-id="5c81d-180">메서드 특성에 물결표 (~)를 사용 하 여 경로 접두사를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-180">Use a tilde (~) on the method attribute to override the route prefix:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

<span data-ttu-id="5c81d-181">경로 접두사는 매개 변수를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-181">The route prefix can include parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a><span data-ttu-id="5c81d-182">경로 제약 조건</span><span class="sxs-lookup"><span data-stu-id="5c81d-182">Route Constraints</span></span>

<span data-ttu-id="5c81d-183">경로 제약 조건을 사용 하면 경로 템플릿의 매개 변수가 일치 하는 방식을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-183">Route constraints let you restrict how the parameters in the route template are matched.</span></span> <span data-ttu-id="5c81d-184">일반적인 구문은 &quot;{parameter: constraint}&quot;입니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-184">The general syntax is &quot;{parameter:constraint}&quot;.</span></span> <span data-ttu-id="5c81d-185">다음은 그 예입니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-185">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

<span data-ttu-id="5c81d-186">여기서 첫 번째 경로는 URI의 &quot;id&quot; 세그먼트가 정수인 경우에만 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-186">Here, the first route will only be selected if the &quot;id&quot; segment of the URI is an integer.</span></span> <span data-ttu-id="5c81d-187">그렇지 않으면 두 번째 경로가 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-187">Otherwise, the second route will be chosen.</span></span>

<span data-ttu-id="5c81d-188">다음 표에서는 지원 되는 제약 조건을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-188">The following table lists the constraints that are supported.</span></span>

| <span data-ttu-id="5c81d-189">제약 조건</span><span class="sxs-lookup"><span data-stu-id="5c81d-189">Constraint</span></span> | <span data-ttu-id="5c81d-190">Description</span><span class="sxs-lookup"><span data-stu-id="5c81d-190">Description</span></span> | <span data-ttu-id="5c81d-191">예제</span><span class="sxs-lookup"><span data-stu-id="5c81d-191">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5c81d-192">알파</span><span class="sxs-lookup"><span data-stu-id="5c81d-192">alpha</span></span> | <span data-ttu-id="5c81d-193">대문자 또는 소문자 라틴 알파벳 문자 (a-z, a-z)를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-193">Matches uppercase or lowercase Latin alphabet characters (a-z, A-Z)</span></span> | <span data-ttu-id="5c81d-194">{x:alpha}</span><span class="sxs-lookup"><span data-stu-id="5c81d-194">{x:alpha}</span></span> |
| <span data-ttu-id="5c81d-195">bool</span><span class="sxs-lookup"><span data-stu-id="5c81d-195">bool</span></span> | <span data-ttu-id="5c81d-196">부울 값을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-196">Matches a Boolean value.</span></span> | <span data-ttu-id="5c81d-197">{x:bool}</span><span class="sxs-lookup"><span data-stu-id="5c81d-197">{x:bool}</span></span> |
| <span data-ttu-id="5c81d-198">Datetime</span><span class="sxs-lookup"><span data-stu-id="5c81d-198">datetime</span></span> | <span data-ttu-id="5c81d-199">**DateTime** 값과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-199">Matches a **DateTime** value.</span></span> | <span data-ttu-id="5c81d-200">{x:datetime}</span><span class="sxs-lookup"><span data-stu-id="5c81d-200">{x:datetime}</span></span> |
| <span data-ttu-id="5c81d-201">decimal</span><span class="sxs-lookup"><span data-stu-id="5c81d-201">decimal</span></span> | <span data-ttu-id="5c81d-202">10 진수 값을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-202">Matches a decimal value.</span></span> | <span data-ttu-id="5c81d-203">{x:decimal}</span><span class="sxs-lookup"><span data-stu-id="5c81d-203">{x:decimal}</span></span> |
| <span data-ttu-id="5c81d-204">double</span><span class="sxs-lookup"><span data-stu-id="5c81d-204">double</span></span> | <span data-ttu-id="5c81d-205">64 비트 부동 소수점 값을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-205">Matches a 64-bit floating-point value.</span></span> | <span data-ttu-id="5c81d-206">{x:double}</span><span class="sxs-lookup"><span data-stu-id="5c81d-206">{x:double}</span></span> |
| <span data-ttu-id="5c81d-207">float</span><span class="sxs-lookup"><span data-stu-id="5c81d-207">float</span></span> | <span data-ttu-id="5c81d-208">32 비트 부동 소수점 값을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-208">Matches a 32-bit floating-point value.</span></span> | <span data-ttu-id="5c81d-209">{x:float}</span><span class="sxs-lookup"><span data-stu-id="5c81d-209">{x:float}</span></span> |
| <span data-ttu-id="5c81d-210">guid</span><span class="sxs-lookup"><span data-stu-id="5c81d-210">guid</span></span> | <span data-ttu-id="5c81d-211">GUID 값과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-211">Matches a GUID value.</span></span> | <span data-ttu-id="5c81d-212">{x:guid}</span><span class="sxs-lookup"><span data-stu-id="5c81d-212">{x:guid}</span></span> |
| <span data-ttu-id="5c81d-213">int</span><span class="sxs-lookup"><span data-stu-id="5c81d-213">int</span></span> | <span data-ttu-id="5c81d-214">32 비트 정수 값을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-214">Matches a 32-bit integer value.</span></span> | <span data-ttu-id="5c81d-215">{x:int}</span><span class="sxs-lookup"><span data-stu-id="5c81d-215">{x:int}</span></span> |
| <span data-ttu-id="5c81d-216">length</span><span class="sxs-lookup"><span data-stu-id="5c81d-216">length</span></span> | <span data-ttu-id="5c81d-217">지정 된 길이 또는 지정 된 길이 범위 내에서 문자열을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-217">Matches a string with the specified length or within a specified range of lengths.</span></span> | <span data-ttu-id="5c81d-218">{x:length(6)} {x:length(1,20)}</span><span class="sxs-lookup"><span data-stu-id="5c81d-218">{x:length(6)} {x:length(1,20)}</span></span> |
| <span data-ttu-id="5c81d-219">long</span><span class="sxs-lookup"><span data-stu-id="5c81d-219">long</span></span> | <span data-ttu-id="5c81d-220">64 비트 정수 값을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-220">Matches a 64-bit integer value.</span></span> | <span data-ttu-id="5c81d-221">{x:long}</span><span class="sxs-lookup"><span data-stu-id="5c81d-221">{x:long}</span></span> |
| <span data-ttu-id="5c81d-222">max</span><span class="sxs-lookup"><span data-stu-id="5c81d-222">max</span></span> | <span data-ttu-id="5c81d-223">최대값과 정수를 일치 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-223">Matches an integer with a maximum value.</span></span> | <span data-ttu-id="5c81d-224">{x:max(10)}</span><span class="sxs-lookup"><span data-stu-id="5c81d-224">{x:max(10)}</span></span> |
| <span data-ttu-id="5c81d-225">maxlength</span><span class="sxs-lookup"><span data-stu-id="5c81d-225">maxlength</span></span> | <span data-ttu-id="5c81d-226">최대 길이가 인 문자열을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-226">Matches a string with a maximum length.</span></span> | <span data-ttu-id="5c81d-227">{x:maxlength(10)}</span><span class="sxs-lookup"><span data-stu-id="5c81d-227">{x:maxlength(10)}</span></span> |
| <span data-ttu-id="5c81d-228">min</span><span class="sxs-lookup"><span data-stu-id="5c81d-228">min</span></span> | <span data-ttu-id="5c81d-229">최소값을 가진 정수를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-229">Matches an integer with a minimum value.</span></span> | <span data-ttu-id="5c81d-230">{x:min(10)}</span><span class="sxs-lookup"><span data-stu-id="5c81d-230">{x:min(10)}</span></span> |
| <span data-ttu-id="5c81d-231">minlength</span><span class="sxs-lookup"><span data-stu-id="5c81d-231">minlength</span></span> | <span data-ttu-id="5c81d-232">최소 길이가 인 문자열을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-232">Matches a string with a minimum length.</span></span> | <span data-ttu-id="5c81d-233">{x:minlength(10)}</span><span class="sxs-lookup"><span data-stu-id="5c81d-233">{x:minlength(10)}</span></span> |
| <span data-ttu-id="5c81d-234">range</span><span class="sxs-lookup"><span data-stu-id="5c81d-234">range</span></span> | <span data-ttu-id="5c81d-235">값 범위 내에서 정수를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-235">Matches an integer within a range of values.</span></span> | <span data-ttu-id="5c81d-236">{x:range(10,50)}</span><span class="sxs-lookup"><span data-stu-id="5c81d-236">{x:range(10,50)}</span></span> |
| <span data-ttu-id="5c81d-237">regex</span><span class="sxs-lookup"><span data-stu-id="5c81d-237">regex</span></span> | <span data-ttu-id="5c81d-238">정규식과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-238">Matches a regular expression.</span></span> | <span data-ttu-id="5c81d-239">{x:regex (^ \d{3}-\d{3}-\d{4}$)}</span><span class="sxs-lookup"><span data-stu-id="5c81d-239">{x:regex(^\d{3}-\d{3}-\d{4}$)}</span></span> |

<span data-ttu-id="5c81d-240">&quot;min&quot;와 같은 일부 제약 조건은 괄호 안에 인수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-240">Notice that some of the constraints, such as &quot;min&quot;, take arguments in parentheses.</span></span> <span data-ttu-id="5c81d-241">콜론으로 구분 된 매개 변수에 여러 제약 조건을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-241">You can apply multiple constraints to a parameter, separated by a colon.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a><span data-ttu-id="5c81d-242">사용자 지정 경로 제약 조건</span><span class="sxs-lookup"><span data-stu-id="5c81d-242">Custom Route Constraints</span></span>

<span data-ttu-id="5c81d-243">**IHttpRouteConstraint** 인터페이스를 구현 하 여 사용자 지정 경로 제약 조건을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-243">You can create custom route constraints by implementing the **IHttpRouteConstraint** interface.</span></span> <span data-ttu-id="5c81d-244">예를 들어 다음 제약 조건은 매개 변수를 0이 아닌 정수 값으로 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-244">For example, the following constraint restricts a parameter to a non-zero integer value.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

<span data-ttu-id="5c81d-245">다음 코드에서는 제약 조건을 등록 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-245">The following code shows how to register the constraint:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

<span data-ttu-id="5c81d-246">이제 경로에 제약 조건을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-246">Now you can apply the constraint in your routes:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

<span data-ttu-id="5c81d-247">**IInlineConstraintResolver** 인터페이스를 구현 하 여 전체 **DefaultInlineConstraintResolver** 클래스를 대체할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-247">You can also replace the entire **DefaultInlineConstraintResolver** class by implementing the **IInlineConstraintResolver** interface.</span></span> <span data-ttu-id="5c81d-248">이렇게 하면 **IInlineConstraintResolver** 구현에서 특별히 추가 하지 않는 한 기본 제공 제약 조건이 모두 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-248">Doing so will replace all of the built-in constraints, unless your implementation of **IInlineConstraintResolver** specifically adds them.</span></span>

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a><span data-ttu-id="5c81d-249">선택적 URI 매개 변수 및 기본값</span><span class="sxs-lookup"><span data-stu-id="5c81d-249">Optional URI Parameters and Default Values</span></span>

<span data-ttu-id="5c81d-250">경로 매개 변수에 물음표를 추가 하 여 URI 매개 변수를 선택적으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-250">You can make a URI parameter optional by adding a question mark to the route parameter.</span></span> <span data-ttu-id="5c81d-251">경로 매개 변수가 선택 사항인 경우에는 메서드 매개 변수의 기본값을 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-251">If a route parameter is optional, you must define a default value for the method parameter.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

<span data-ttu-id="5c81d-252">이 예제에서 `/api/books/locale/1033` 및 `/api/books/locale`는 동일한 리소스를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-252">In this example, `/api/books/locale/1033` and `/api/books/locale` return the same resource.</span></span>

<span data-ttu-id="5c81d-253">또는 다음과 같이 경로 템플릿 내에 기본값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-253">Alternatively, you can specify a default value inside the route template, as follows:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

<span data-ttu-id="5c81d-254">이는 이전 예제와 거의 동일 하지만 기본값이 적용 될 때 동작의 약간 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-254">This is almost the same as the previous example, but there is a slight difference of behavior when the default value is applied.</span></span>

- <span data-ttu-id="5c81d-255">첫 번째 예제 ("{lcid: int?}")에서 1033의 기본값은 메서드 매개 변수에 직접 할당 되므로 매개 변수의 값이 정확 하 게 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-255">In the first example ("{lcid:int?}"), the default value of 1033 is assigned directly to the method parameter, so the parameter will have this exact value.</span></span>
- <span data-ttu-id="5c81d-256">두 번째 예 ("{lcid: int = 1033}")에서 "1033"의 기본값은 모델 바인딩 프로세스를 거칩니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-256">In the second example ("{lcid:int=1033}"), the default value of "1033" goes through the model-binding process.</span></span> <span data-ttu-id="5c81d-257">기본 모델 바인더는 "1033"을 숫자 값 1033로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-257">The default model-binder will convert "1033" to the numeric value 1033.</span></span> <span data-ttu-id="5c81d-258">그러나 다른 작업을 수행 하는 사용자 지정 모델 바인더를 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-258">However, you could plug in a custom model binder, which might do something different.</span></span>

<span data-ttu-id="5c81d-259">파이프라인에 사용자 지정 모델 바인더를 포함 하지 않는 한 대부분의 경우 두 가지 형태는 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-259">(In most cases, unless you have custom model binders in your pipeline, the two forms will be equivalent.)</span></span>

<a id="route-names"></a>
## <a name="route-names"></a><span data-ttu-id="5c81d-260">경로 이름</span><span class="sxs-lookup"><span data-stu-id="5c81d-260">Route Names</span></span>

<span data-ttu-id="5c81d-261">Web API에서 모든 경로에는 이름이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-261">In Web API, every route has a name.</span></span> <span data-ttu-id="5c81d-262">경로 이름은 링크를 생성 하는 데 유용 하므로 HTTP 응답에 링크를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-262">Route names are useful for generating links, so that you can include a link in an HTTP response.</span></span>

<span data-ttu-id="5c81d-263">경로 이름을 지정 하려면 특성의 **이름** 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-263">To specify the route name, set the **Name** property on the attribute.</span></span> <span data-ttu-id="5c81d-264">다음 예에서는 경로 이름을 설정 하는 방법과 링크를 생성할 때 경로 이름을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-264">The following example shows how to set the route name, and also how to use the route name when generating a link.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a><span data-ttu-id="5c81d-265">경로 순서</span><span class="sxs-lookup"><span data-stu-id="5c81d-265">Route Order</span></span>

<span data-ttu-id="5c81d-266">프레임 워크는 URI를 경로와 일치 시 키 려 고 할 때 특정 순서로 경로를 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-266">When the framework tries to match a URI with a route, it evaluates the routes in a particular order.</span></span> <span data-ttu-id="5c81d-267">순서를 지정 하려면 경로 특성에서 **order** 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-267">To specify the order, set the **Order** property on the route attribute.</span></span> <span data-ttu-id="5c81d-268">낮은 값이 먼저 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-268">Lower values are evaluated first.</span></span> <span data-ttu-id="5c81d-269">기본 순서 값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-269">The default order value is zero.</span></span>

<span data-ttu-id="5c81d-270">다음은 전체 순서가 결정 되는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-270">Here is how the total ordering is determined:</span></span>

1. <span data-ttu-id="5c81d-271">경로 특성의 **Order** 속성을 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-271">Compare the **Order** property of the route attribute.</span></span>
2. <span data-ttu-id="5c81d-272">경로 템플릿에서 각 URI 세그먼트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-272">Look at each URI segment in the route template.</span></span> <span data-ttu-id="5c81d-273">각 세그먼트에 대해 다음과 같이 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-273">For each segment, order as follows:</span></span>

    1. <span data-ttu-id="5c81d-274">리터럴 세그먼트.</span><span class="sxs-lookup"><span data-stu-id="5c81d-274">Literal segments.</span></span>
    2. <span data-ttu-id="5c81d-275">제약 조건이 포함 된 경로 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-275">Route parameters with constraints.</span></span>
    3. <span data-ttu-id="5c81d-276">제약 조건이 없는 경로 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-276">Route parameters without constraints.</span></span>
    4. <span data-ttu-id="5c81d-277">제약 조건이 있는 와일드 카드 매개 변수 세그먼트입니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-277">Wildcard parameter segments with constraints.</span></span>
    5. <span data-ttu-id="5c81d-278">제약 조건이 없는 와일드 카드 매개 변수 세그먼트입니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-278">Wildcard parameter segments without constraints.</span></span>
3. <span data-ttu-id="5c81d-279">연결의 경우 경로는 대/소문자를 구분 하지 않는 경로 템플릿의[stringcomparison.ordinalignorecase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)(서 수 문자열 비교)를 기준으로 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-279">In the case of a tie, routes are ordered by a case-insensitive ordinal string comparison ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) of the route template.</span></span>

<span data-ttu-id="5c81d-280">다음 예를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c81d-280">Here is an example.</span></span> <span data-ttu-id="5c81d-281">다음 컨트롤러를 정의 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-281">Suppose you define the following controller:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

<span data-ttu-id="5c81d-282">이러한 경로는 다음과 같이 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-282">These routes are ordered as follows.</span></span>

1. <span data-ttu-id="5c81d-283">주문/세부 정보</span><span class="sxs-lookup"><span data-stu-id="5c81d-283">orders/details</span></span>
2. <span data-ttu-id="5c81d-284">orders/{id}</span><span class="sxs-lookup"><span data-stu-id="5c81d-284">orders/{id}</span></span>
3. <span data-ttu-id="5c81d-285">orders/{customerName}</span><span class="sxs-lookup"><span data-stu-id="5c81d-285">orders/{customerName}</span></span>
4. <span data-ttu-id="5c81d-286">orders/{\*date}</span><span class="sxs-lookup"><span data-stu-id="5c81d-286">orders/{\*date}</span></span>
5. <span data-ttu-id="5c81d-287">orders/pending</span><span class="sxs-lookup"><span data-stu-id="5c81d-287">orders/pending</span></span>

<span data-ttu-id="5c81d-288">"Details"는 리터럴 세그먼트 이며 "{id}" 앞에 나타나지만 **Order** 속성은 1 이기 때문에 "보류 중"으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-288">Notice that "details" is a literal segment and appears before "{id}", but "pending" appears last because the **Order** property is 1.</span></span> <span data-ttu-id="5c81d-289">이 예에서는 "details" 또는 "pending" 이라는 고객이 없는 것으로 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-289">(This example assumes there are no customers named "details" or "pending".</span></span> <span data-ttu-id="5c81d-290">일반적으로 모호한 경로를 방지 하십시오.</span><span class="sxs-lookup"><span data-stu-id="5c81d-290">In general, try to avoid ambiguous routes.</span></span> <span data-ttu-id="5c81d-291">이 예제에서 `GetByCustomer`에 대 한 더 나은 경로 템플릿은 "customers/{customerName}"입니다.</span><span class="sxs-lookup"><span data-stu-id="5c81d-291">In this example, a better route template for `GetByCustomer` is "customers/{customerName}" )</span></span>
