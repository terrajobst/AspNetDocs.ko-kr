---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: ASP.NET Web API에서 라우팅 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/29/2018
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 85862c094cc54365267b1f21e68d235a15519cda
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449249"
---
# <a name="routing-in-aspnet-web-api"></a><span data-ttu-id="8c38a-102">ASP.NET Web API의 라우팅</span><span class="sxs-lookup"><span data-stu-id="8c38a-102">Routing in ASP.NET Web API</span></span>

<span data-ttu-id="8c38a-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="8c38a-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="8c38a-104">이 문서에서는 ASP.NET Web API는 컨트롤러에 HTTP 요청을 라우팅하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-104">This article describes how ASP.NET Web API routes HTTP requests to controllers.</span></span>

> [!NOTE]
> <span data-ttu-id="8c38a-105">ASP.NET MVC에 익숙한 경우 Web API 라우팅은 MVC 라우팅과 매우 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-105">If you are familiar with ASP.NET MVC, Web API routing is very similar to MVC routing.</span></span> <span data-ttu-id="8c38a-106">주요 차이점은 Web API는 URI 경로가 아니라 HTTP 동사를 사용 하 여 작업을 선택 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-106">The main difference is that Web API uses the HTTP verb, not the URI path, to select the action.</span></span> <span data-ttu-id="8c38a-107">Web API에서 MVC 스타일 라우팅을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-107">You can also use MVC-style routing in Web API.</span></span> <span data-ttu-id="8c38a-108">이 문서에서는 ASP.NET MVC에 대 한 지식이 있다고 가정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-108">This article does not assume any knowledge of ASP.NET MVC.</span></span>

## <a name="routing-tables"></a><span data-ttu-id="8c38a-109">라우팅 테이블</span><span class="sxs-lookup"><span data-stu-id="8c38a-109">Routing Tables</span></span>

<span data-ttu-id="8c38a-110">ASP.NET Web API에서 *컨트롤러* 는 HTTP 요청을 처리 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-110">In ASP.NET Web API, a *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="8c38a-111">컨트롤러의 공용 메서드를 *작업 메서드* 또는 간단히 *동작*이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-111">The public methods of the controller are called *action methods* or simply *actions*.</span></span> <span data-ttu-id="8c38a-112">웹 API 프레임 워크에서 요청을 받으면 요청을 작업으로 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-112">When the Web API framework receives a request, it routes the request to an action.</span></span>

<span data-ttu-id="8c38a-113">호출할 동작을 결정 하기 위해 프레임 워크는 *라우팅 테이블*을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-113">To determine which action to invoke, the framework uses a *routing table*.</span></span> <span data-ttu-id="8c38a-114">Web API 용 Visual Studio 프로젝트 템플릿은 기본 경로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-114">The Visual Studio project template for Web API creates a default route:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="8c38a-115">이 경로는 *WebApiConfig.cs* 파일에 정의 됩니다 .이 파일은 *앱\_시작* 디렉터리에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-115">This route is defined in the *WebApiConfig.cs* file, which is placed in the *App\_Start* directory:</span></span>

![](routing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="8c38a-116">`WebApiConfig` 클래스에 대 한 자세한 내용은 [ASP.NET Web API 구성](../advanced/configuring-aspnet-web-api.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="8c38a-116">For more information about the `WebApiConfig` class, see [Configuring ASP.NET Web API](../advanced/configuring-aspnet-web-api.md).</span></span>

<span data-ttu-id="8c38a-117">Web API를 자체 호스트 하는 경우에는 `HttpSelfHostConfiguration` 개체에서 직접 라우팅 테이블을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-117">If you self-host Web API, you must set the routing table directly on the `HttpSelfHostConfiguration` object.</span></span> <span data-ttu-id="8c38a-118">자세한 내용은 [웹 API 자체 호스팅](../older-versions/self-host-a-web-api.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="8c38a-118">For more information, see [Self-Host a Web API](../older-versions/self-host-a-web-api.md).</span></span>

<span data-ttu-id="8c38a-119">라우팅 테이블의 각 항목에는 *경로 템플릿이*포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-119">Each entry in the routing table contains a *route template*.</span></span> <span data-ttu-id="8c38a-120">Web API에 대 한 기본 경로 템플릿은 &quot;API/{controller}/{id}&quot;입니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-120">The default route template for Web API is &quot;api/{controller}/{id}&quot;.</span></span> <span data-ttu-id="8c38a-121">이 템플릿에서 &quot;api&quot;는 리터럴 경로 세그먼트이 고 {controller} 및 {id}는 자리 표시자 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-121">In this template, &quot;api&quot; is a literal path segment, and {controller} and {id} are placeholder variables.</span></span>

<span data-ttu-id="8c38a-122">웹 API 프레임 워크는 HTTP 요청을 받으면 라우팅 테이블의 경로 템플릿 중 하나에 대해 URI를 일치 시 키 려 고 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-122">When the Web API framework receives an HTTP request, it tries to match the URI against one of the route templates in the routing table.</span></span> <span data-ttu-id="8c38a-123">경로가 일치 하지 않으면 클라이언트에서 404 오류를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-123">If no route matches, the client receives a 404 error.</span></span> <span data-ttu-id="8c38a-124">예를 들어 다음 Uri는 기본 경로와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-124">For example, the following URIs match the default route:</span></span>

- <span data-ttu-id="8c38a-125">/api/연락처</span><span class="sxs-lookup"><span data-stu-id="8c38a-125">/api/contacts</span></span>
- <span data-ttu-id="8c38a-126">/api/contacts/1</span><span class="sxs-lookup"><span data-stu-id="8c38a-126">/api/contacts/1</span></span>
- <span data-ttu-id="8c38a-127">/api/products/gizmo1</span><span class="sxs-lookup"><span data-stu-id="8c38a-127">/api/products/gizmo1</span></span>

<span data-ttu-id="8c38a-128">그러나 다음 URI는 &quot;api&quot; 세그먼트가 없으므로 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-128">However, the following URI does not match, because it lacks the &quot;api&quot; segment:</span></span>

- <span data-ttu-id="8c38a-129">/contacts/1</span><span class="sxs-lookup"><span data-stu-id="8c38a-129">/contacts/1</span></span>

> [!NOTE]
> <span data-ttu-id="8c38a-130">경로에서 "api"를 사용 하는 이유는 ASP.NET MVC 라우팅과의 충돌을 방지 하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-130">The reason for using "api" in the route is to avoid collisions with ASP.NET MVC routing.</span></span> <span data-ttu-id="8c38a-131">이렇게 하면 &quot;/연락처를&quot; 하 여 MVC 컨트롤러로 이동 하 고 &quot;/s i o n t i m e&quot;를 웹 API 컨트롤러로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-131">That way, you can have &quot;/contacts&quot; go to an MVC controller, and &quot;/api/contacts&quot; go to a Web API controller.</span></span> <span data-ttu-id="8c38a-132">물론이 규칙을 원하지 않는 경우 기본 경로 테이블을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-132">Of course, if you don't like this convention, you can change the default route table.</span></span>

<span data-ttu-id="8c38a-133">일치 하는 경로가 발견 되 면 Web API는 컨트롤러 및 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-133">Once a matching route is found, Web API selects the controller and the action:</span></span>

- <span data-ttu-id="8c38a-134">컨트롤러를 찾기 위해 Web API는 &quot;컨트롤러&quot;를 *{controller}* 변수 값에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-134">To find the controller, Web API adds &quot;Controller&quot; to the value of the *{controller}* variable.</span></span>
- <span data-ttu-id="8c38a-135">동작을 찾기 위해 Web API는 HTTP 동사를 찾은 다음 이름이 해당 HTTP 동사 이름으로 시작 하는 작업을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-135">To find the action, Web API looks at the HTTP verb, and then looks for an action whose name begins with that HTTP verb name.</span></span> <span data-ttu-id="8c38a-136">예를 들어 GET 요청을 사용 하는 경우 Web API는 &quot;GetContact&quot; 또는 &quot;GetAllContacts&quot;와 같은 &quot;Get&quot;접두사로 시작 하는 작업을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-136">For example, with a GET request, Web API looks for an action prefixed with &quot;Get&quot;, such as &quot;GetContact&quot; or &quot;GetAllContacts&quot;.</span></span> <span data-ttu-id="8c38a-137">이 규칙은 GET, POST, PUT, DELETE, HEAD, OPTIONS 및 PATCH 동사에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-137">This convention applies only to GET, POST, PUT, DELETE, HEAD, OPTIONS, and PATCH verbs.</span></span> <span data-ttu-id="8c38a-138">컨트롤러에서 특성을 사용 하 여 다른 HTTP 동사를 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-138">You can enable other HTTP verbs by using attributes on your controller.</span></span> <span data-ttu-id="8c38a-139">이에 대 한 예제는 나중에 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-139">We'll see an example of that later.</span></span>
- <span data-ttu-id="8c38a-140">경로 템플릿의 다른 자리 표시자 변수 (예: *{id}* )는 동작 매개 변수에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-140">Other placeholder variables in the route template, such as *{id},* are mapped to action parameters.</span></span>

<span data-ttu-id="8c38a-141">예제를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-141">Let's look at an example.</span></span> <span data-ttu-id="8c38a-142">다음 컨트롤러를 정의 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-142">Suppose that you define the following controller:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="8c38a-143">다음은 각각에 대해 호출 되는 작업과 함께 가능한 몇 가지 HTTP 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-143">Here are some possible HTTP requests, along with the action that gets invoked for each:</span></span>

| <span data-ttu-id="8c38a-144">HTTP 동사</span><span class="sxs-lookup"><span data-stu-id="8c38a-144">HTTP Verb</span></span> | <span data-ttu-id="8c38a-145">URI 경로</span><span class="sxs-lookup"><span data-stu-id="8c38a-145">URI Path</span></span> | <span data-ttu-id="8c38a-146">작업</span><span class="sxs-lookup"><span data-stu-id="8c38a-146">Action</span></span> | <span data-ttu-id="8c38a-147">매개 변수</span><span class="sxs-lookup"><span data-stu-id="8c38a-147">Parameter</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8c38a-148">GET</span><span class="sxs-lookup"><span data-stu-id="8c38a-148">GET</span></span> | <span data-ttu-id="8c38a-149">a p i/제품</span><span class="sxs-lookup"><span data-stu-id="8c38a-149">api/products</span></span> | <span data-ttu-id="8c38a-150">GetAllProducts</span><span class="sxs-lookup"><span data-stu-id="8c38a-150">GetAllProducts</span></span> | <span data-ttu-id="8c38a-151">*없음을*</span><span class="sxs-lookup"><span data-stu-id="8c38a-151">*(none)*</span></span> |
| <span data-ttu-id="8c38a-152">GET</span><span class="sxs-lookup"><span data-stu-id="8c38a-152">GET</span></span> | <span data-ttu-id="8c38a-153">a p i/제품/4</span><span class="sxs-lookup"><span data-stu-id="8c38a-153">api/products/4</span></span> | <span data-ttu-id="8c38a-154">GetProductById</span><span class="sxs-lookup"><span data-stu-id="8c38a-154">GetProductById</span></span> | <span data-ttu-id="8c38a-155">4</span><span class="sxs-lookup"><span data-stu-id="8c38a-155">4</span></span> |
| <span data-ttu-id="8c38a-156">Delete</span><span class="sxs-lookup"><span data-stu-id="8c38a-156">DELETE</span></span> | <span data-ttu-id="8c38a-157">a p i/제품/4</span><span class="sxs-lookup"><span data-stu-id="8c38a-157">api/products/4</span></span> | <span data-ttu-id="8c38a-158">DeleteProduct</span><span class="sxs-lookup"><span data-stu-id="8c38a-158">DeleteProduct</span></span> | <span data-ttu-id="8c38a-159">4</span><span class="sxs-lookup"><span data-stu-id="8c38a-159">4</span></span> |
| <span data-ttu-id="8c38a-160">POST</span><span class="sxs-lookup"><span data-stu-id="8c38a-160">POST</span></span> | <span data-ttu-id="8c38a-161">a p i/제품</span><span class="sxs-lookup"><span data-stu-id="8c38a-161">api/products</span></span> | <span data-ttu-id="8c38a-162">*(일치 항목 없음)*</span><span class="sxs-lookup"><span data-stu-id="8c38a-162">*(no match)*</span></span> |  |

<span data-ttu-id="8c38a-163">URI의 *{id}* 세그먼트 (있는 경우)가 동작의 *id* 매개 변수에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-163">Notice that the *{id}* segment of the URI, if present, is mapped to the *id* parameter of the action.</span></span> <span data-ttu-id="8c38a-164">이 예제에서 컨트롤러는 두 개의 GET 메서드를 정의 합니다. 하나는 *id* 매개 변수를 사용 하 고 다른 하나는 매개 변수를 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-164">In this example, the controller defines two GET methods, one with an *id* parameter and one with no parameters.</span></span>

<span data-ttu-id="8c38a-165">또한 컨트롤러에서 &quot;Post ...&quot; 메서드를 정의 하지 않으므로 POST 요청은 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-165">Also, note that the POST request will fail, because the controller does not define a &quot;Post...&quot; method.</span></span>

## <a name="routing-variations"></a><span data-ttu-id="8c38a-166">라우팅 변형</span><span class="sxs-lookup"><span data-stu-id="8c38a-166">Routing Variations</span></span>

<span data-ttu-id="8c38a-167">이전 섹션에서는 ASP.NET Web API에 대 한 기본 라우팅 메커니즘에 대해 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-167">The previous section described the basic routing mechanism for ASP.NET Web API.</span></span> <span data-ttu-id="8c38a-168">이 섹션에서는 몇 가지 변형에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-168">This section describes some variations.</span></span>

### <a name="http-verbs"></a><span data-ttu-id="8c38a-169">HTTP 동사</span><span class="sxs-lookup"><span data-stu-id="8c38a-169">HTTP verbs</span></span>

<span data-ttu-id="8c38a-170">HTTP 동사에 대 한 명명 규칙을 사용 하는 대신 작업 메서드를 다음 특성 중 하나로 데코레이팅 하 여 동작에 대 한 HTTP 동사를 명시적으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-170">Instead of using the naming convention for HTTP verbs, you can explicitly specify the HTTP verb for an action by decorating the action method with one of the following attributes:</span></span>

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

<span data-ttu-id="8c38a-171">다음 예제에서 `FindProduct` 메서드는 GET 요청에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-171">In the following example, the `FindProduct` method is mapped to GET requests:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="8c38a-172">작업에 대해 여러 HTTP 동사를 허용 하거나 GET, PUT, POST, DELETE, HEAD, OPTIONS 및 PATCH 이외의 HTTP 동사를 허용 하려면 HTTP 동사 목록을 사용 하는 `[AcceptVerbs]` 특성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-172">To allow multiple HTTP verbs for an action, or to allow HTTP verbs other than GET, PUT, POST, DELETE, HEAD, OPTIONS, and PATCH, use the `[AcceptVerbs]` attribute, which takes a list of HTTP verbs.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a><span data-ttu-id="8c38a-173">작업 이름별 라우팅</span><span class="sxs-lookup"><span data-stu-id="8c38a-173">Routing by Action Name</span></span>

<span data-ttu-id="8c38a-174">기본 라우팅 템플릿을 사용 하는 경우 Web API는 HTTP 동사를 사용 하 여 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-174">With the default routing template, Web API uses the HTTP verb to select the action.</span></span> <span data-ttu-id="8c38a-175">그러나 URI에 작업 이름이 포함 된 경로를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-175">However, you can also create a route where the action name is included in the URI:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="8c38a-176">이 경로 템플릿에서 *{action}* 매개 변수는 컨트롤러의 동작 메서드 이름을로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-176">In this route template, the *{action}* parameter names the action method on the controller.</span></span> <span data-ttu-id="8c38a-177">이 스타일의 라우팅을 사용 하 여 특성을 사용 하 여 허용 되는 HTTP 동사를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-177">With this style of routing, use attributes to specify the allowed HTTP verbs.</span></span> <span data-ttu-id="8c38a-178">예를 들어 컨트롤러에 다음 메서드가 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-178">For example, suppose your controller has the following method:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="8c38a-179">이 경우 "api/products/details/1"에 대 한 GET 요청은 `Details` 메서드에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-179">In this case, a GET request for "api/products/details/1" would map to the `Details` method.</span></span> <span data-ttu-id="8c38a-180">이 라우팅 스타일은 ASP.NET MVC와 비슷하며 RPC 스타일 API에 적합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-180">This style of routing is similar to ASP.NET MVC, and may be appropriate for an RPC-style API.</span></span>

<span data-ttu-id="8c38a-181">`[ActionName]` 특성을 사용 하 여 작업 이름을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-181">You can override the action name by using the `[ActionName]` attribute.</span></span> <span data-ttu-id="8c38a-182">다음 예제에는 &quot;s p 2에 매핑되는 두 가지 작업이*있습니다.* 하나는 GET을 지원 하 고 다른 하나는 POST를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-182">In the following example, there are two actions that map to &quot;api/products/thumbnail/*id*. One supports GET and the other supports POST:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a><span data-ttu-id="8c38a-183">비 작업</span><span class="sxs-lookup"><span data-stu-id="8c38a-183">Non-Actions</span></span>

<span data-ttu-id="8c38a-184">메서드가 동작으로 호출 되는 것을 방지 하려면 `[NonAction]` 특성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-184">To prevent a method from getting invoked as an action, use the `[NonAction]` attribute.</span></span> <span data-ttu-id="8c38a-185">이는 다른 방법으로 라우팅 규칙과 일치 하는 경우에도 메서드가 동작이 아니라는 프레임 워크에 신호를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-185">This signals to the framework that the method is not an action, even if it would otherwise match the routing rules.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a><span data-ttu-id="8c38a-186">추가 참고 자료</span><span class="sxs-lookup"><span data-stu-id="8c38a-186">Further Reading</span></span>

<span data-ttu-id="8c38a-187">이 항목에서는 라우팅에 대 한 개략적인 보기를 제공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8c38a-187">This topic provided a high-level view of routing.</span></span> <span data-ttu-id="8c38a-188">자세한 내용은 [라우팅 및 작업 선택](routing-and-action-selection.md), 프레임 워크가 경로에 대 한 URI를 정확히 일치 하는 방식에 대해 설명 하 고, 컨트롤러를 선택한 다음 호출할 작업을 선택 하는 방법을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="8c38a-188">For more detail, see [Routing and Action Selection](routing-and-action-selection.md), which describes exactly how the framework matches a URI to a route, selects a controller, and then selects the action to invoke.</span></span>
