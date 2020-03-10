---
uid: web-api/overview/advanced/httpclient-message-handlers
title: ASP.NET Web API의 HttpClient 메시지 처리기-ASP.NET 4.x
author: MikeWasson
description: ASP.NET 4.x의 ASP.NET Web API에 대 한 사용자 지정 메시지 처리기 만들기
ms.author: riande
ms.date: 10/01/2012
ms.custom: seoapril2019
ms.assetid: 5a4b6c80-b2e9-4710-8969-d5076f7f82b8
msc.legacyurl: /web-api/overview/advanced/httpclient-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: 265bd9b2f48ed7d1e955f3c4947d10fd589b3e17
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449279"
---
# <a name="httpclient-message-handlers-in-aspnet-web-api"></a><span data-ttu-id="1afd4-103">ASP.NET Web API의 HttpClient 메시지 처리기</span><span class="sxs-lookup"><span data-stu-id="1afd4-103">HttpClient Message Handlers in ASP.NET Web API</span></span>

<span data-ttu-id="1afd4-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="1afd4-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="1afd4-105">*메시지 처리기* 는 http 요청을 수신 하 고 http 응답을 반환 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1afd4-105">A *message handler* is a class that receives an HTTP request and returns an HTTP response.</span></span>

<span data-ttu-id="1afd4-106">일반적으로 일련의 메시지 처리기가 함께 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1afd4-106">Typically, a series of message handlers are chained together.</span></span> <span data-ttu-id="1afd4-107">첫 번째 처리기는 HTTP 요청을 수신 하 고, 일부 처리를 수행 하 고, 다음 처리기에 요청을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1afd4-107">The first handler receives an HTTP request, does some processing, and gives the request to the next handler.</span></span> <span data-ttu-id="1afd4-108">어느 시점에서 응답이 만들어지고 체인을 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="1afd4-108">At some point, the response is created and goes back up the chain.</span></span> <span data-ttu-id="1afd4-109">이 패턴을 *위임* 처리기 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1afd4-109">This pattern is called a *delegating* handler.</span></span>

![](httpclient-message-handlers/_static/image1.png)

<span data-ttu-id="1afd4-110">클라이언트 쪽에서는 **Httpclient** 클래스가 메시지 처리기를 사용 하 여 요청을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="1afd4-110">On the client side, the **HttpClient** class uses a message handler to process requests.</span></span> <span data-ttu-id="1afd4-111">기본 처리기는 **Httpclienthandler**로, 네트워크를 통해 요청을 보내고 서버에서 응답을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1afd4-111">The default handler is **HttpClientHandler**, which sends the request over the network and gets the response from the server.</span></span> <span data-ttu-id="1afd4-112">사용자 지정 메시지 처리기를 클라이언트 파이프라인에 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1afd4-112">You can insert custom message handlers into the client pipeline:</span></span>

![](httpclient-message-handlers/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="1afd4-113">또한 ASP.NET Web API 서버 쪽의 메시지 처리기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1afd4-113">ASP.NET Web API also uses message handlers on the server side.</span></span> <span data-ttu-id="1afd4-114">자세한 내용은 [HTTP 메시지 처리기](http-message-handlers.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="1afd4-114">For more information, see [HTTP Message Handlers](http-message-handlers.md).</span></span>

## <a name="custom-message-handlers"></a><span data-ttu-id="1afd4-115">사용자 지정 메시지 처리기</span><span class="sxs-lookup"><span data-stu-id="1afd4-115">Custom Message Handlers</span></span>

<span data-ttu-id="1afd4-116">사용자 지정 메시지 처리기를 쓰려면 **DelegatingHandler** 에서 파생 하 고 **SendAsync** 메서드를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1afd4-116">To write a custom message handler, derive from **System.Net.Http.DelegatingHandler** and override the **SendAsync** method.</span></span> <span data-ttu-id="1afd4-117">메서드 서명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1afd4-117">Here is the method signature:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample1.cs)]

<span data-ttu-id="1afd4-118">메서드는 **HttpRequestMessage** 를 입력으로 사용 하 고 **HttpResponseMessage**를 비동기적으로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1afd4-118">The method takes an **HttpRequestMessage** as input and asynchronously returns an **HttpResponseMessage**.</span></span> <span data-ttu-id="1afd4-119">일반적인 구현에서는 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1afd4-119">A typical implementation does the following:</span></span>

1. <span data-ttu-id="1afd4-120">요청 메시지를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="1afd4-120">Process the request message.</span></span>
2. <span data-ttu-id="1afd4-121">`base.SendAsync`를 호출 하 여 요청을 내부 처리기에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1afd4-121">Call `base.SendAsync` to send the request to the inner handler.</span></span>
3. <span data-ttu-id="1afd4-122">내부 처리기는 응답 메시지를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1afd4-122">The inner handler returns a response message.</span></span> <span data-ttu-id="1afd4-123">이 단계는 비동기입니다.</span><span class="sxs-lookup"><span data-stu-id="1afd4-123">(This step is asynchronous.)</span></span>
4. <span data-ttu-id="1afd4-124">응답을 처리 하 고 호출자에 게 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1afd4-124">Process the response and return it to the caller.</span></span>

<span data-ttu-id="1afd4-125">다음 예제에서는 보내는 요청에 사용자 지정 헤더를 추가 하는 메시지 처리기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1afd4-125">The following example shows a message handler that adds a custom header to the outgoing request:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample2.cs)]

<span data-ttu-id="1afd4-126">`base.SendAsync`에 대한 호출은 비동기입니다.</span><span class="sxs-lookup"><span data-stu-id="1afd4-126">The call to `base.SendAsync` is asynchronous.</span></span> <span data-ttu-id="1afd4-127">이 호출 후 처리기에서 작업을 수행 하는 경우에는 **wait** 키워드를 사용 하 여 메서드가 완료 된 후 실행을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1afd4-127">If the handler does any work after this call, use the **await** keyword to resume execution after the method completes.</span></span> <span data-ttu-id="1afd4-128">다음 예제에서는 오류 코드를 기록 하는 처리기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1afd4-128">The following example shows a handler that logs error codes.</span></span> <span data-ttu-id="1afd4-129">로깅 자체는 그다지 흥미로운 것은 아니지만이 예제에서는 처리기 내에서 응답을 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1afd4-129">The logging itself is not very interesting, but the example shows how to get at the response inside the handler.</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample3.cs?highlight=10,13)]

## <a name="adding-message-handlers-to-the-client-pipeline"></a><span data-ttu-id="1afd4-130">클라이언트 파이프라인에 메시지 처리기 추가</span><span class="sxs-lookup"><span data-stu-id="1afd4-130">Adding Message Handlers to the Client Pipeline</span></span>

<span data-ttu-id="1afd4-131">**Httpclient**에 사용자 지정 처리기를 추가 하려면 **Httpclientfactory. 만들기** 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1afd4-131">To add custom handlers to **HttpClient**, use the **HttpClientFactory.Create** method:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample4.cs)]

<span data-ttu-id="1afd4-132">메시지 처리기는 **Create** 메서드에 전달 하는 순서 대로 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1afd4-132">Message handlers are called in the order that you pass them into the **Create** method.</span></span> <span data-ttu-id="1afd4-133">처리기가 중첩 되기 때문에 응답 메시지는 다른 방향으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="1afd4-133">Because handlers are nested, the response message travels in the other direction.</span></span> <span data-ttu-id="1afd4-134">즉, 마지막 처리기가 응답 메시지를 가져오기 위한 첫 번째 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="1afd4-134">That is, the last handler is the first to get the response message.</span></span>
