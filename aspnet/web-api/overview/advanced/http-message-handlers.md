---
uid: web-api/overview/advanced/http-message-handlers
title: ASP.NET Web API의 HTTP 메시지 처리기-ASP.NET 4.x
author: MikeWasson
description: ASP.NET 4.x 용 ASP.NET Web API의 HTTP 메시지 처리기 개요
ms.author: riande
ms.date: 02/13/2012
ms.custom: seoapril2019
ms.assetid: 9002018b-3aa3-4358-bb1c-fbb5bc751d01
msc.legacyurl: /web-api/overview/advanced/http-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: a8e6f1da8df4802e1acf7779a2fc75bfe8ab876f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504929"
---
# <a name="http-message-handlers-in-aspnet-web-api"></a><span data-ttu-id="847fb-103">ASP.NET Web API의 HTTP 메시지 처리기</span><span class="sxs-lookup"><span data-stu-id="847fb-103">HTTP Message Handlers in ASP.NET Web API</span></span>

<span data-ttu-id="847fb-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="847fb-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="847fb-105">*메시지 처리기* 는 http 요청을 수신 하 고 http 응답을 반환 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-105">A *message handler* is a class that receives an HTTP request and returns an HTTP response.</span></span> <span data-ttu-id="847fb-106">메시지 처리기는 추상 **Httpmessagehandler** 클래스에서 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-106">Message handlers derive from the abstract **HttpMessageHandler** class.</span></span>

<span data-ttu-id="847fb-107">일반적으로 일련의 메시지 처리기가 함께 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-107">Typically, a series of message handlers are chained together.</span></span> <span data-ttu-id="847fb-108">첫 번째 처리기는 HTTP 요청을 수신 하 고, 일부 처리를 수행 하 고, 다음 처리기에 요청을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-108">The first handler receives an HTTP request, does some processing, and gives the request to the next handler.</span></span> <span data-ttu-id="847fb-109">어느 시점에서 응답이 만들어지고 체인을 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-109">At some point, the response is created and goes back up the chain.</span></span> <span data-ttu-id="847fb-110">이 패턴을 *위임* 처리기 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-110">This pattern is called a *delegating* handler.</span></span>

![](http-message-handlers/_static/image1.png)

## <a name="server-side-message-handlers"></a><span data-ttu-id="847fb-111">서버 쪽 메시지 처리기</span><span class="sxs-lookup"><span data-stu-id="847fb-111">Server-Side Message Handlers</span></span>

<span data-ttu-id="847fb-112">서버 쪽에서 Web API 파이프라인은 몇 가지 기본 제공 메시지 처리기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-112">On the server side, the Web API pipeline uses some built-in message handlers:</span></span>

- <span data-ttu-id="847fb-113">**HttpServer** 는 호스트에서 요청을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-113">**HttpServer** gets the request from the host.</span></span>
- <span data-ttu-id="847fb-114">**HttpRoutingDispatcher** 는 경로에 따라 요청을 디스패치합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-114">**HttpRoutingDispatcher** dispatches the request based on the route.</span></span>
- <span data-ttu-id="847fb-115">**Httpcontrollerdispatcher** 웹 API 컨트롤러에 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-115">**HttpControllerDispatcher** sends the request to a Web API controller.</span></span>

<span data-ttu-id="847fb-116">파이프라인에 사용자 지정 처리기를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-116">You can add custom handlers to the pipeline.</span></span> <span data-ttu-id="847fb-117">메시지 처리기는 컨트롤러 작업 대신 HTTP 메시지 수준에서 작동 하는 크로스 절삭 문제에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-117">Message handlers are good for cross-cutting concerns that operate at the level of HTTP messages (rather than controller actions).</span></span> <span data-ttu-id="847fb-118">예를 들어 메시지 처리기는 다음과 같은 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-118">For example, a message handler might:</span></span>

- <span data-ttu-id="847fb-119">요청 헤더를 읽거나 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-119">Read or modify request headers.</span></span>
- <span data-ttu-id="847fb-120">응답에 응답 헤더를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-120">Add a response header to responses.</span></span>
- <span data-ttu-id="847fb-121">컨트롤러에 도달 하기 전에 요청의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-121">Validate requests before they reach the controller.</span></span>

<span data-ttu-id="847fb-122">이 다이어그램은 파이프라인에 삽입 된 두 개의 사용자 지정 처리기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-122">This diagram shows two custom handlers inserted into the pipeline:</span></span>

![](http-message-handlers/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="847fb-123">클라이언트 쪽에서 HttpClient는 메시지 처리기도 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-123">On the client side, HttpClient also uses message handlers.</span></span> <span data-ttu-id="847fb-124">자세한 내용은 [Httpclient 메시지 처리기](httpclient-message-handlers.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="847fb-124">For more information, see [HttpClient Message Handlers](httpclient-message-handlers.md).</span></span>

## <a name="custom-message-handlers"></a><span data-ttu-id="847fb-125">사용자 지정 메시지 처리기</span><span class="sxs-lookup"><span data-stu-id="847fb-125">Custom Message Handlers</span></span>

<span data-ttu-id="847fb-126">사용자 지정 메시지 처리기를 쓰려면 **DelegatingHandler** 에서 파생 하 고 **SendAsync** 메서드를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-126">To write a custom message handler, derive from **System.Net.Http.DelegatingHandler** and override the **SendAsync** method.</span></span> <span data-ttu-id="847fb-127">이 메서드의 서명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-127">This method has the following signature:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample1.cs)]

<span data-ttu-id="847fb-128">메서드는 **HttpRequestMessage** 를 입력으로 사용 하 고 **HttpResponseMessage**를 비동기적으로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-128">The method takes an **HttpRequestMessage** as input and asynchronously returns an **HttpResponseMessage**.</span></span> <span data-ttu-id="847fb-129">일반적인 구현에서는 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-129">A typical implementation does the following:</span></span>

1. <span data-ttu-id="847fb-130">요청 메시지를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-130">Process the request message.</span></span>
2. <span data-ttu-id="847fb-131">`base.SendAsync`를 호출 하 여 요청을 내부 처리기에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-131">Call `base.SendAsync` to send the request to the inner handler.</span></span>
3. <span data-ttu-id="847fb-132">내부 처리기는 응답 메시지를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-132">The inner handler returns a response message.</span></span> <span data-ttu-id="847fb-133">이 단계는 비동기입니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-133">(This step is asynchronous.)</span></span>
4. <span data-ttu-id="847fb-134">응답을 처리 하 고 호출자에 게 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-134">Process the response and return it to the caller.</span></span>

<span data-ttu-id="847fb-135">다음은 간단한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-135">Here is a trivial example:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="847fb-136">`base.SendAsync`에 대한 호출은 비동기입니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-136">The call to `base.SendAsync` is asynchronous.</span></span> <span data-ttu-id="847fb-137">이 호출 후 처리기에서 작업을 수행 하는 경우 표시 된 것 처럼 **wait** 키워드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-137">If the handler does any work after this call, use the **await** keyword, as shown.</span></span>

<span data-ttu-id="847fb-138">위임 처리기는 내부 처리기를 건너뛰고 직접 응답을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-138">A delegating handler can also skip the inner handler and directly create the response:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample3.cs)]

<span data-ttu-id="847fb-139">위임 처리기가 `base.SendAsync`를 호출 하지 않고 응답을 만드는 경우 요청은 파이프라인의 나머지 부분을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-139">If a delegating handler creates the response without calling `base.SendAsync`, the request skips the rest of the pipeline.</span></span> <span data-ttu-id="847fb-140">이는 요청의 유효성을 검사 하는 처리기 (오류 응답 생성)에 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-140">This can be useful for a handler that validates the request (creating an error response).</span></span>

![](http-message-handlers/_static/image3.png)

## <a name="adding-a-handler-to-the-pipeline"></a><span data-ttu-id="847fb-141">파이프라인에 처리기 추가</span><span class="sxs-lookup"><span data-stu-id="847fb-141">Adding a Handler to the Pipeline</span></span>

<span data-ttu-id="847fb-142">서버 쪽에서 메시지 처리기를 추가 하려면 **Httpconfiguration. messagehandlers** 컬렉션에 처리기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-142">To add a message handler on the server side, add the handler to the **HttpConfiguration.MessageHandlers** collection.</span></span> <span data-ttu-id="847fb-143">"ASP.NET MVC 4 웹 응용 프로그램" 템플릿을 사용 하 여 프로젝트를 만든 경우 **Webapiconfig** 클래스 내에서이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-143">If you used the "ASP.NET MVC 4 Web Application" template to create the project, you can do this inside the **WebApiConfig** class:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample4.cs)]

<span data-ttu-id="847fb-144">메시지 처리기는 **messagehandlers** collection에 표시 되는 순서와 동일한 순서로 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-144">Message handlers are called in the same order that they appear in **MessageHandlers** collection.</span></span> <span data-ttu-id="847fb-145">중첩 되기 때문에 응답 메시지는 다른 방향으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-145">Because they are nested, the response message travels in the other direction.</span></span> <span data-ttu-id="847fb-146">즉, 마지막 처리기가 응답 메시지를 가져오기 위한 첫 번째 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-146">That is, the last handler is the first to get the response message.</span></span>

<span data-ttu-id="847fb-147">내부 처리기를 설정할 필요가 없습니다. Web API 프레임 워크는 메시지 처리기를 자동으로 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-147">Notice that you don't need to set the inner handlers; the Web API framework automatically connects the message handlers.</span></span>

<span data-ttu-id="847fb-148">[자체 호스팅](../older-versions/self-host-a-web-api.md)인 경우 **HttpSelfHostConfiguration** 클래스의 인스턴스를 만들고이 처리기를 **messagehandlers** collection에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-148">If you are [self-hosting](../older-versions/self-host-a-web-api.md), create an instance of the **HttpSelfHostConfiguration** class and add the handlers to the **MessageHandlers** collection.</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample5.cs)]

<span data-ttu-id="847fb-149">이제 사용자 지정 메시지 처리기의 몇 가지 예를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-149">Now let's look at some examples of custom message handlers.</span></span>

## <a name="example-x-http-method-override"></a><span data-ttu-id="847fb-150">예: X-HTTP 메서드-재정의</span><span class="sxs-lookup"><span data-stu-id="847fb-150">Example: X-HTTP-Method-Override</span></span>

<span data-ttu-id="847fb-151">X-HTTP 메서드-재정의는 비표준 HTTP 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-151">X-HTTP-Method-Override is a non-standard HTTP header.</span></span> <span data-ttu-id="847fb-152">PUT 또는 DELETE와 같은 특정 HTTP 요청 형식을 전송할 수 없는 클라이언트를 위해 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-152">It is designed for clients that cannot send certain HTTP request types, such as PUT or DELETE.</span></span> <span data-ttu-id="847fb-153">대신, 클라이언트는 POST 요청을 전송 하 고, HTTP 메서드 재정의 헤더를 원하는 메서드로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-153">Instead, the client sends a POST request and sets the X-HTTP-Method-Override header to the desired method.</span></span> <span data-ttu-id="847fb-154">다음은 그 예입니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-154">For example:</span></span>

[!code-console[Main](http-message-handlers/samples/sample6.cmd)]

<span data-ttu-id="847fb-155">다음은 X-HTTP 메서드 재정의에 대 한 지원을 추가 하는 메시지 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-155">Here is a message handler that adds support for X-HTTP-Method-Override:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample7.cs)]

<span data-ttu-id="847fb-156">SendAsync 메서드에서 처리기는 요청 메시지가 POST 요청 인지 여부와 해당 요청 메시지가 헤더를 포함 하는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-156">In the **SendAsync** method, the handler checks whether the request message is a POST request, and whether it contains the X-HTTP-Method-Override header.</span></span> <span data-ttu-id="847fb-157">이 경우 헤더 값의 유효성을 검사 한 다음 요청 메서드를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-157">If so, it validates the header value, and then modifies the request method.</span></span> <span data-ttu-id="847fb-158">마지막으로 처리기는 `base.SendAsync`를 호출 하 여 메시지를 다음 처리기로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-158">Finally, the handler calls `base.SendAsync` to pass the message to the next handler.</span></span>

<span data-ttu-id="847fb-159">요청이 **httpcontrollerdispatcher** 클래스에 도달 하면 **httpcontrollerdispatcher** 는 업데이트 된 요청 메서드를 기반으로 요청을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-159">When the request reaches the **HttpControllerDispatcher** class, **HttpControllerDispatcher** will route the request based on the updated request method.</span></span>

## <a name="example-adding-a-custom-response-header"></a><span data-ttu-id="847fb-160">예: 사용자 지정 응답 헤더 추가</span><span class="sxs-lookup"><span data-stu-id="847fb-160">Example: Adding a Custom Response Header</span></span>

<span data-ttu-id="847fb-161">모든 응답 메시지에 사용자 지정 헤더를 추가 하는 메시지 처리기는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-161">Here is a message handler that adds a custom header to every response message:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample8.cs)]

<span data-ttu-id="847fb-162">먼저 처리기는 `base.SendAsync`를 호출 하 여 내부 메시지 처리기에 요청을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-162">First, the handler calls `base.SendAsync` to pass the request to the inner message handler.</span></span> <span data-ttu-id="847fb-163">내부 처리기는 응답 메시지를 반환 하지만 **&lt;t&gt;** 개체를 사용 하 여 비동기적으로 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-163">The inner handler returns a response message, but it does so asynchronously using a **Task&lt;T&gt;** object.</span></span> <span data-ttu-id="847fb-164">`base.SendAsync` 비동기식으로 완료 될 때까지 응답 메시지를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-164">The response message is not available until `base.SendAsync` completes asynchronously.</span></span>

<span data-ttu-id="847fb-165">이 예제에서는 **wait** 키워드를 사용 하 여 `SendAsync` 완료 된 후 비동기적으로 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-165">This example uses the **await** keyword to perform work asynchronously after `SendAsync` completes.</span></span> <span data-ttu-id="847fb-166">.NET Framework 4.0를 대상으로 하는 경우에는&gt;&lt;**태스크** 를 사용 **합니다. System.threading.tasks.task.continuewith** 메서드:</span><span class="sxs-lookup"><span data-stu-id="847fb-166">If you are targeting .NET Framework 4.0, use the **Task**&lt;T&gt;**.ContinueWith** method:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample9.cs)]

## <a name="example-checking-for-an-api-key"></a><span data-ttu-id="847fb-167">예: API 키 확인</span><span class="sxs-lookup"><span data-stu-id="847fb-167">Example: Checking for an API Key</span></span>

<span data-ttu-id="847fb-168">일부 웹 서비스에서는 클라이언트가 요청에 API 키를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-168">Some web services require clients to include an API key in their request.</span></span> <span data-ttu-id="847fb-169">다음 예제에서는 메시지 처리기가 유효한 API 키에 대 한 요청을 확인 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-169">The following example shows how a message handler can check requests for a valid API key:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample10.cs)]

<span data-ttu-id="847fb-170">이 처리기는 URI 쿼리 문자열에서 API 키를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-170">This handler looks for the API key in the URI query string.</span></span> <span data-ttu-id="847fb-171">이 예에서는 키가 정적 문자열 이라고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-171">(For this example, we assume that the key is a static string.</span></span> <span data-ttu-id="847fb-172">실제 구현에서는 더 복잡 한 유효성 검사를 사용할 수 있습니다. 쿼리 문자열에 키가 포함 된 경우 처리기는 내부 처리기에 요청을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-172">A real implementation would probably use more complex validation.) If the query string contains the key, the handler passes the request to the inner handler.</span></span>

<span data-ttu-id="847fb-173">요청에 유효한 키가 없으면 처리기는 상태 403, 사용 권한 없음 응답 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-173">If the request does not have a valid key, the handler creates a response message with status 403, Forbidden.</span></span> <span data-ttu-id="847fb-174">이 경우 처리기는 `base.SendAsync`를 호출 하지 않으므로 내부 처리기가 요청을 수신 하지 않으며 컨트롤러도 수신 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-174">In this case, the handler does not call `base.SendAsync`, so the inner handler never receives the request, nor does the controller.</span></span> <span data-ttu-id="847fb-175">따라서 컨트롤러는 들어오는 모든 요청에 유효한 API 키가 있다고 가정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-175">Therefore, the controller can assume that all incoming requests have a valid API key.</span></span>

> [!NOTE]
> <span data-ttu-id="847fb-176">API 키가 특정 컨트롤러 작업에만 적용 되는 경우 메시지 처리기 대신 작업 필터를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-176">If the API key applies only to certain controller actions, consider using an action filter instead of a message handler.</span></span> <span data-ttu-id="847fb-177">URI 라우팅이 수행 된 후에 실행 되는 작업 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-177">Action filters run after URI routing is performed.</span></span>

## <a name="per-route-message-handlers"></a><span data-ttu-id="847fb-178">경로 당 메시지 처리기</span><span class="sxs-lookup"><span data-stu-id="847fb-178">Per-Route Message Handlers</span></span>

<span data-ttu-id="847fb-179">**Httpconfiguration의 처리기입니다. messagehandlers** collection은 전역적으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-179">Handlers in the **HttpConfiguration.MessageHandlers** collection apply globally.</span></span>

<span data-ttu-id="847fb-180">또는 경로를 정의할 때 메시지 처리기를 특정 경로에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-180">Alternatively, you can add a message handler to a specific route when you define the route:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample11.cs?highlight=16)]

<span data-ttu-id="847fb-181">이 예제에서 요청 URI가 "Route2"와 일치 하는 경우 요청이 `MessageHandler2`디스패치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-181">In this example, if the request URI matches "Route2", the request is dispatched to `MessageHandler2`.</span></span> <span data-ttu-id="847fb-182">다음 다이어그램에서는 이러한 두 경로에 대 한 파이프라인을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-182">The following diagram shows the pipeline for these two routes:</span></span>

![](http-message-handlers/_static/image4.png)

<span data-ttu-id="847fb-183">`MessageHandler2`는 기본 **Httpcontrollerdispatcher**를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-183">Notice that `MessageHandler2` replaces the default **HttpControllerDispatcher**.</span></span> <span data-ttu-id="847fb-184">이 예제에서 `MessageHandler2`는 응답을 만들고 "Route2"와 일치 하는 요청은 컨트롤러로 이동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-184">In this example, `MessageHandler2` creates the response, and requests that match "Route2" never go to a controller.</span></span> <span data-ttu-id="847fb-185">이렇게 하면 전체 Web API 컨트롤러 메커니즘을 사용자 지정 끝점으로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-185">This lets you replace the entire Web API controller mechanism with your own custom endpoint.</span></span>

<span data-ttu-id="847fb-186">또는 경로 당 메시지 처리기가 **Httpcontrollerdispatcher**로 위임한 후이를 컨트롤러에 디스패치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-186">Alternatively, a per-route message handler can delegate to **HttpControllerDispatcher**, which then dispatches to a controller.</span></span>

![](http-message-handlers/_static/image5.png)

<span data-ttu-id="847fb-187">다음 코드에서는이 경로를 구성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="847fb-187">The following code shows how to configure this route:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample12.cs)]
