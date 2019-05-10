---
uid: web-api/overview/advanced/http-message-handlers
title: HTTP 메시지 처리기에서 ASP.NET Web API-ASP.NET 4.x
author: MikeWasson
description: ASP.NET에 대 한 ASP.NET Web API의 HTTP 메시지 처리기 개요 4.x
ms.author: riande
ms.date: 02/13/2012
ms.custom: seoapril2019
ms.assetid: 9002018b-3aa3-4358-bb1c-fbb5bc751d01
msc.legacyurl: /web-api/overview/advanced/http-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: a8e6f1da8df4802e1acf7779a2fc75bfe8ab876f
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65115541"
---
# <a name="http-message-handlers-in-aspnet-web-api"></a><span data-ttu-id="49ee8-103">ASP.NET Web API의에서 HTTP 메시지 처리기</span><span class="sxs-lookup"><span data-stu-id="49ee8-103">HTTP Message Handlers in ASP.NET Web API</span></span>

<span data-ttu-id="49ee8-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="49ee8-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="49ee8-105">A *메시지 처리기* 는 HTTP 요청을 수신 하 고 HTTP 응답을 반환 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-105">A *message handler* is a class that receives an HTTP request and returns an HTTP response.</span></span> <span data-ttu-id="49ee8-106">추상에서 파생 되는 메시지 처리기 **HttpMessageHandler** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-106">Message handlers derive from the abstract **HttpMessageHandler** class.</span></span>

<span data-ttu-id="49ee8-107">일반적으로 일련의 메시지 처리기를 함께 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-107">Typically, a series of message handlers are chained together.</span></span> <span data-ttu-id="49ee8-108">HTTP 요청을 받고 일부 처리를 요청 다음 처리기를 제공 하는 첫 번째 처리기 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-108">The first handler receives an HTTP request, does some processing, and gives the request to the next handler.</span></span> <span data-ttu-id="49ee8-109">어느 시점에서 응답 생성 되 고 체인 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-109">At some point, the response is created and goes back up the chain.</span></span> <span data-ttu-id="49ee8-110">이 패턴은 호출을 *위임* 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-110">This pattern is called a *delegating* handler.</span></span>

![](http-message-handlers/_static/image1.png)

## <a name="server-side-message-handlers"></a><span data-ttu-id="49ee8-111">서버 쪽 메시지 처리기</span><span class="sxs-lookup"><span data-stu-id="49ee8-111">Server-Side Message Handlers</span></span>

<span data-ttu-id="49ee8-112">서버 쪽에서 Web API 파이프라인을 몇 가지 기본 제공 메시지 처리기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-112">On the server side, the Web API pipeline uses some built-in message handlers:</span></span>

- <span data-ttu-id="49ee8-113">**HttpServer** 호스트에서 요청을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-113">**HttpServer** gets the request from the host.</span></span>
- <span data-ttu-id="49ee8-114">**HttpRoutingDispatcher** 경로 따라 요청을 발송 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-114">**HttpRoutingDispatcher** dispatches the request based on the route.</span></span>
- <span data-ttu-id="49ee8-115">**HttpControllerDispatcher** Web API 컨트롤러에 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-115">**HttpControllerDispatcher** sends the request to a Web API controller.</span></span>

<span data-ttu-id="49ee8-116">파이프라인에 사용자 지정 처리기를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-116">You can add custom handlers to the pipeline.</span></span> <span data-ttu-id="49ee8-117">메시지 처리기는 HTTP 메시지 대신 컨트롤러 작업 수준에서 작동 하는 교차 편집 문제에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-117">Message handlers are good for cross-cutting concerns that operate at the level of HTTP messages (rather than controller actions).</span></span> <span data-ttu-id="49ee8-118">예를 들어, 메시지 처리기를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-118">For example, a message handler might:</span></span>

- <span data-ttu-id="49ee8-119">읽기 또는 요청 헤더를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-119">Read or modify request headers.</span></span>
- <span data-ttu-id="49ee8-120">응답 헤더를 응답에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-120">Add a response header to responses.</span></span>
- <span data-ttu-id="49ee8-121">컨트롤러에 도달 하기 전에 요청을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-121">Validate requests before they reach the controller.</span></span>

<span data-ttu-id="49ee8-122">이 다이어그램에서는 파이프라인에 삽입 하는 두 명의 사용자 지정 처리기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-122">This diagram shows two custom handlers inserted into the pipeline:</span></span>

![](http-message-handlers/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="49ee8-123">클라이언트 쪽에서는 HttpClient 메시지 처리기도 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-123">On the client side, HttpClient also uses message handlers.</span></span> <span data-ttu-id="49ee8-124">자세한 내용은 [HttpClient 메시지 처리기](httpclient-message-handlers.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-124">For more information, see [HttpClient Message Handlers](httpclient-message-handlers.md).</span></span>

## <a name="custom-message-handlers"></a><span data-ttu-id="49ee8-125">사용자 지정 메시지 처리기</span><span class="sxs-lookup"><span data-stu-id="49ee8-125">Custom Message Handlers</span></span>

<span data-ttu-id="49ee8-126">파생 되는 사용자 지정 메시지 처리기를 작성 하려면 **System.Net.Http.DelegatingHandler** 재정의 **SendAsync** 메서드.</span><span class="sxs-lookup"><span data-stu-id="49ee8-126">To write a custom message handler, derive from **System.Net.Http.DelegatingHandler** and override the **SendAsync** method.</span></span> <span data-ttu-id="49ee8-127">이 메서드의 서명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-127">This method has the following signature:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample1.cs)]

<span data-ttu-id="49ee8-128">메서드는 **HttpRequestMessage** 입력 하 고 비동기적으로 반환은 **HttpResponseMessage**합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-128">The method takes an **HttpRequestMessage** as input and asynchronously returns an **HttpResponseMessage**.</span></span> <span data-ttu-id="49ee8-129">일반적인 구현은 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-129">A typical implementation does the following:</span></span>

1. <span data-ttu-id="49ee8-130">요청 메시지를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-130">Process the request message.</span></span>
2. <span data-ttu-id="49ee8-131">호출 `base.SendAsync` 내부 처리기에는 요청을 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-131">Call `base.SendAsync` to send the request to the inner handler.</span></span>
3. <span data-ttu-id="49ee8-132">내부 처리기는 응답 메시지를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-132">The inner handler returns a response message.</span></span> <span data-ttu-id="49ee8-133">(이 단계는 비동기입니다.)</span><span class="sxs-lookup"><span data-stu-id="49ee8-133">(This step is asynchronous.)</span></span>
4. <span data-ttu-id="49ee8-134">응답을 처리 하 고 호출자에 게 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-134">Process the response and return it to the caller.</span></span>

<span data-ttu-id="49ee8-135">간단한 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-135">Here is a trivial example:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="49ee8-136">에 대 한 호출 `base.SendAsync` 은 비동기입니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-136">The call to `base.SendAsync` is asynchronous.</span></span> <span data-ttu-id="49ee8-137">이 호출 후에 모든 작업 수행 하는 처리기를 사용 합니다 **await** 키워드를 표시 된 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-137">If the handler does any work after this call, use the **await** keyword, as shown.</span></span>

<span data-ttu-id="49ee8-138">위임 처리기는 내부 처리기를 건너뛸 수도 하 고 응답을 직접 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-138">A delegating handler can also skip the inner handler and directly create the response:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample3.cs)]

<span data-ttu-id="49ee8-139">처리기를 호출 하지 않고 응답 만듭니다를 위임 하는 경우 `base.SendAsync`를 요청 파이프라인의 나머지 부분을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-139">If a delegating handler creates the response without calling `base.SendAsync`, the request skips the rest of the pipeline.</span></span> <span data-ttu-id="49ee8-140">이 (오류 응답이 생성) 요청의 유효성을 검사 하는 처리기에 대 한 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-140">This can be useful for a handler that validates the request (creating an error response).</span></span>

![](http-message-handlers/_static/image3.png)

## <a name="adding-a-handler-to-the-pipeline"></a><span data-ttu-id="49ee8-141">파이프라인에 처리기를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-141">Adding a Handler to the Pipeline</span></span>

<span data-ttu-id="49ee8-142">서버 쪽에서 메시지 처리기를 추가할 처리기를 추가 합니다 **HttpConfiguration.MessageHandlers** 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-142">To add a message handler on the server side, add the handler to the **HttpConfiguration.MessageHandlers** collection.</span></span> <span data-ttu-id="49ee8-143">"ASP.NET MVC 4 웹 응용 프로그램" 템플릿을 사용 하는 프로젝트를 만든 경우에이 내부를 수행할 수 있습니다 합니다 **WebApiConfig** 클래스:</span><span class="sxs-lookup"><span data-stu-id="49ee8-143">If you used the "ASP.NET MVC 4 Web Application" template to create the project, you can do this inside the **WebApiConfig** class:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample4.cs)]

<span data-ttu-id="49ee8-144">에 표시 되는 순서 대로 메시지 처리기가 호출 **MessageHandlers** 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-144">Message handlers are called in the same order that they appear in **MessageHandlers** collection.</span></span> <span data-ttu-id="49ee8-145">중첩 되어 있으므로 응답 메시지는 반대 방향으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-145">Because they are nested, the response message travels in the other direction.</span></span> <span data-ttu-id="49ee8-146">마지막 처리기 즉, 첫 번째 응답 메시지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-146">That is, the last handler is the first to get the response message.</span></span>

<span data-ttu-id="49ee8-147">내부 처리기; 설정할 필요가 없습니다 알 수 있습니다. Web API 프레임 워크의 메시지 처리기를 자동으로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-147">Notice that you don't need to set the inner handlers; the Web API framework automatically connects the message handlers.</span></span>

<span data-ttu-id="49ee8-148">있다면 [자체 호스팅](../older-versions/self-host-a-web-api.md)의 인스턴스를 만듭니다를 **HttpSelfHostConfiguration** 클래스 및 처리기를 추가 합니다 **MessageHandlers** 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-148">If you are [self-hosting](../older-versions/self-host-a-web-api.md), create an instance of the **HttpSelfHostConfiguration** class and add the handlers to the **MessageHandlers** collection.</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample5.cs)]

<span data-ttu-id="49ee8-149">이제 사용자 지정 메시지 처리기의 몇 가지 예를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-149">Now let's look at some examples of custom message handlers.</span></span>

## <a name="example-x-http-method-override"></a><span data-ttu-id="49ee8-150">예제: X-HTTP-메서드-재정</span><span class="sxs-lookup"><span data-stu-id="49ee8-150">Example: X-HTTP-Method-Override</span></span>

<span data-ttu-id="49ee8-151">HTTP 메서드 재정의 X는 비표준 HTTP 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-151">X-HTTP-Method-Override is a non-standard HTTP header.</span></span> <span data-ttu-id="49ee8-152">PUT 또는 DELETE 같은 HTTP 요청 형식을 특정를 보낼 수 없는 클라이언트에 대 한 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-152">It is designed for clients that cannot send certain HTTP request types, such as PUT or DELETE.</span></span> <span data-ttu-id="49ee8-153">대신 클라이언트 POST 요청을 보내고 HTTP 메서드 재정의 X 헤더 원하는 메서드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-153">Instead, the client sends a POST request and sets the X-HTTP-Method-Override header to the desired method.</span></span> <span data-ttu-id="49ee8-154">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="49ee8-154">For example:</span></span>

[!code-console[Main](http-message-handlers/samples/sample6.cmd)]

<span data-ttu-id="49ee8-155">HTTP 메서드 재정의 X에 대 한 지원을 추가 하는 메시지 처리기는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-155">Here is a message handler that adds support for X-HTTP-Method-Override:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample7.cs)]

<span data-ttu-id="49ee8-156">에 **SendAsync** 요청 메시지는 POST 요청 인지 여부 및 HTTP 메서드 재정의 X 헤더 포함 여부 메서드를 처리기를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-156">In the **SendAsync** method, the handler checks whether the request message is a POST request, and whether it contains the X-HTTP-Method-Override header.</span></span> <span data-ttu-id="49ee8-157">그렇다면 헤더 값의 유효성을 검사 하 고 요청 메서드를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-157">If so, it validates the header value, and then modifies the request method.</span></span> <span data-ttu-id="49ee8-158">처리기를 호출 하는 마지막으로, `base.SendAsync` 다음 처리기에 메시지를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-158">Finally, the handler calls `base.SendAsync` to pass the message to the next handler.</span></span>

<span data-ttu-id="49ee8-159">요청에 도달 하면 합니다 **HttpControllerDispatcher** 클래스 **HttpControllerDispatcher** 는 업데이트 요청 방법에 따라 요청을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-159">When the request reaches the **HttpControllerDispatcher** class, **HttpControllerDispatcher** will route the request based on the updated request method.</span></span>

## <a name="example-adding-a-custom-response-header"></a><span data-ttu-id="49ee8-160">예제: 사용자 지정 응답 헤더를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-160">Example: Adding a Custom Response Header</span></span>

<span data-ttu-id="49ee8-161">모든 응답 메시지를 사용자 지정 헤더를 추가 하는 메시지 처리기는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-161">Here is a message handler that adds a custom header to every response message:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample8.cs)]

<span data-ttu-id="49ee8-162">처리기를 호출 하는 먼저 `base.SendAsync` 내부 메시지 처리기는 요청을 전달 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-162">First, the handler calls `base.SendAsync` to pass the request to the inner message handler.</span></span> <span data-ttu-id="49ee8-163">내부 처리기를 응답 메시지를 반환 하지만 비동기적으로 사용 하는 **태스크&lt;T&gt;**  개체입니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-163">The inner handler returns a response message, but it does so asynchronously using a **Task&lt;T&gt;** object.</span></span> <span data-ttu-id="49ee8-164">응답 메시지를 때까지 사용할 수 없는 `base.SendAsync` 비동기적으로 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-164">The response message is not available until `base.SendAsync` completes asynchronously.</span></span>

<span data-ttu-id="49ee8-165">이 예제에서는 합니다 **await** 작업을 수행 하는 키워드 후 비동기적으로 `SendAsync` 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-165">This example uses the **await** keyword to perform work asynchronously after `SendAsync` completes.</span></span> <span data-ttu-id="49ee8-166">.NET Framework 4.0을 대상으로 하는 경우 사용 합니다 **태스크**&lt;T&gt;**합니다. ContinueWith** 메서드:</span><span class="sxs-lookup"><span data-stu-id="49ee8-166">If you are targeting .NET Framework 4.0, use the **Task**&lt;T&gt;**.ContinueWith** method:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample9.cs)]

## <a name="example-checking-for-an-api-key"></a><span data-ttu-id="49ee8-167">예제: API 키에 대 한 확인</span><span class="sxs-lookup"><span data-stu-id="49ee8-167">Example: Checking for an API Key</span></span>

<span data-ttu-id="49ee8-168">일부 웹 서비스 요청에 API 키를 포함 하는 클라이언트가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-168">Some web services require clients to include an API key in their request.</span></span> <span data-ttu-id="49ee8-169">다음 예제에서는 메시지 처리기 유효한 API 키에 대 한 요청을 확인할 수 있습니다 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-169">The following example shows how a message handler can check requests for a valid API key:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample10.cs)]

<span data-ttu-id="49ee8-170">이 처리기는 URI 쿼리 문자열에 API 키를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-170">This handler looks for the API key in the URI query string.</span></span> <span data-ttu-id="49ee8-171">(이 예를 들어 가정 정적 문자열로 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-171">(For this example, we assume that the key is a static string.</span></span> <span data-ttu-id="49ee8-172">실제 구현이 아마도 더 복잡 한 유효성 검사를 사용 합니다.) 쿼리 문자열에 키를 포함 하는 경우 처리기는 내부 처리기에 요청을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-172">A real implementation would probably use more complex validation.) If the query string contains the key, the handler passes the request to the inner handler.</span></span>

<span data-ttu-id="49ee8-173">처리기 상태 403 사용 하 여 응답 메시지를 만듭니다 요청에 유효한 키를 찾을 수 없는 경우 사용할 수 없음.</span><span class="sxs-lookup"><span data-stu-id="49ee8-173">If the request does not have a valid key, the handler creates a response message with status 403, Forbidden.</span></span> <span data-ttu-id="49ee8-174">이 경우 처리기를 호출 하지 않습니다 `base.SendAsync`, 내부 처리기가 받지 요청 하므로 컨트롤러를 않습니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-174">In this case, the handler does not call `base.SendAsync`, so the inner handler never receives the request, nor does the controller.</span></span> <span data-ttu-id="49ee8-175">따라서 컨트롤러를 사용 하 들어오는 모든 요청에 유효한 API 키를 있다고 가정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-175">Therefore, the controller can assume that all incoming requests have a valid API key.</span></span>

> [!NOTE]
> <span data-ttu-id="49ee8-176">API 키를 특정 컨트롤러 작업에만 적용 되는 경우에 작업 필터를 사용 하 여 메시지 처리기를 대신 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-176">If the API key applies only to certain controller actions, consider using an action filter instead of a message handler.</span></span> <span data-ttu-id="49ee8-177">작업 필터 URI 라우팅 수행 된 후 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-177">Action filters run after URI routing is performed.</span></span>

## <a name="per-route-message-handlers"></a><span data-ttu-id="49ee8-178">경로 당 메시지 처리기</span><span class="sxs-lookup"><span data-stu-id="49ee8-178">Per-Route Message Handlers</span></span>

<span data-ttu-id="49ee8-179">처리기는 **HttpConfiguration.MessageHandlers** 컬렉션 전체적으로 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-179">Handlers in the **HttpConfiguration.MessageHandlers** collection apply globally.</span></span>

<span data-ttu-id="49ee8-180">또는 경로 정의 하는 경우 특정 경로에 메시지 처리기를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-180">Alternatively, you can add a message handler to a specific route when you define the route:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample11.cs?highlight=16)]

<span data-ttu-id="49ee8-181">이 예제에서는 요청 URI에 "Route2" 일치 하는 경우 요청에 디스패치 됩니다 `MessageHandler2`합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-181">In this example, if the request URI matches "Route2", the request is dispatched to `MessageHandler2`.</span></span> <span data-ttu-id="49ee8-182">다음 다이어그램은 이러한 두 경로 대 한 파이프라인을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-182">The following diagram shows the pipeline for these two routes:</span></span>

![](http-message-handlers/_static/image4.png)

<span data-ttu-id="49ee8-183">있음을 `MessageHandler2` 기본값을 바꾸는 **HttpControllerDispatcher**합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-183">Notice that `MessageHandler2` replaces the default **HttpControllerDispatcher**.</span></span> <span data-ttu-id="49ee8-184">이 예제에서는 `MessageHandler2` 응답을 만들고 "Route2" 컨트롤러에 절대로 일치 하는 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-184">In this example, `MessageHandler2` creates the response, and requests that match "Route2" never go to a controller.</span></span> <span data-ttu-id="49ee8-185">이 방법으로 사용자 고유의 사용자 지정 끝점을 사용 하 여 전체 Web API 컨트롤러 메커니즘을 교체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-185">This lets you replace the entire Web API controller mechanism with your own custom endpoint.</span></span>

<span data-ttu-id="49ee8-186">또는 경로 당 메시지 처리기에 게 위임할 수 **HttpControllerDispatcher**, 그러면 컨트롤러에 디스패치합니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-186">Alternatively, a per-route message handler can delegate to **HttpControllerDispatcher**, which then dispatches to a controller.</span></span>

![](http-message-handlers/_static/image5.png)

<span data-ttu-id="49ee8-187">다음 코드에는이 경로 구성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="49ee8-187">The following code shows how to configure this route:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample12.cs)]
