---
uid: webhooks/receiving/handlers
title: ASP.NET 웹 후크 처리기 | Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook에서 요청을 처리 하는 방법입니다.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: a55b0d20-9c90-4bd3-a471-20da6f569f0c
ms.openlocfilehash: 01c9a283d105c4a0973ff88c8de646c5f49a34db
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518033"
---
# <a name="aspnet-webhooks-handlers"></a><span data-ttu-id="359b4-103">ASP.NET 웹 후크 처리기</span><span class="sxs-lookup"><span data-stu-id="359b4-103">ASP.NET WebHooks handlers</span></span>

<span data-ttu-id="359b4-104">WebHook 수신기에서 WebHook 요청의 유효성을 검사 한 후에는 사용자 코드에서 처리할 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="359b4-104">Once WebHooks requests has been validated by a WebHook receiver, it is ready to be processed by user code.</span></span> <span data-ttu-id="359b4-105">여기에는 *처리기* 가 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="359b4-105">This is where *handlers* come in.</span></span> <span data-ttu-id="359b4-106">처리기는 [IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) 인터페이스에서 파생 되지만 일반적으로 인터페이스에서 직접 파생 하는 대신 [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="359b4-106">Handlers derive from the [IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) interface but typically uses the [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) class instead of deriving directly from the interface.</span></span>

<span data-ttu-id="359b4-107">하나 이상의 처리기에서 WebHook 요청을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="359b4-107">A WebHook request can be processed by one or more handlers.</span></span> <span data-ttu-id="359b4-108">처리기는 가장 낮은 값에서 가장 높은 값으로 이동 하 *는 순서에* 따라 순서 대로 호출 됩니다. 여기서 order는 단순 정수입니다 (1에서 100 사이에서 제안 됨).</span><span class="sxs-lookup"><span data-stu-id="359b4-108">Handlers are called in order based on their respective *Order* property going from lowest to highest where Order is a simple integer (suggested to be between 1 and 100):</span></span>

![WebHook 처리기 순서 속성 다이어그램](_static/Handlers.png)

<span data-ttu-id="359b4-110">처리기는 필요에 따라 WebHookHandlerContext에 대 한 *응답* 속성을 설정 하 여 처리를 중지 하 고 응답을 다시 웹 후크에 HTTP 응답으로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="359b4-110">A handler can optionally set the *Response* property on the WebHookHandlerContext which will lead the processing to stop and the response to be sent back as the HTTP response to the WebHook.</span></span> <span data-ttu-id="359b4-111">위의 경우 처리기 C는 B 보다 높은 순서를 포함 하 고 B는 응답을 설정 하므로 호출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="359b4-111">In the case above, Handler C won't get called because it has a higher order than B and B sets the response.</span></span>

<span data-ttu-id="359b4-112">응답을 설정 하는 것은 일반적으로 응답이 원래 API로 정보를 다시 전달할 수 있는 웹 후크에만 해당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="359b4-112">Setting the response is typically only relevant for WebHooks where the response can carry information back to the originating API.</span></span> <span data-ttu-id="359b4-113">이는 응답이 있는 채널에 응답을 다시 게시 하는 여유 시간 webhook을 사용 하는 경우를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="359b4-113">This is for example the case with Slack WebHooks where the response is posted back to the channel where the WebHook came from.</span></span> <span data-ttu-id="359b4-114">처리기는 해당 특정 수신기에서 웹 후크를 수신 하려는 경우에만 받는 사람 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="359b4-114">Handlers can set the Receiver property if they only want to receive WebHooks from that particular receiver.</span></span> <span data-ttu-id="359b4-115">수신기를 설정 하지 않으면 모든 수신기에 대해 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="359b4-115">If they don't set the receiver they are called for all of them.</span></span>

<span data-ttu-id="359b4-116">응답의 또 다른 일반적인 용도는 *410 사라진* 응답을 사용 하 여 WebHook가 더 이상 활성 상태가 없고 추가 요청을 제출 하지 않음을 나타내는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="359b4-116">One other common use of a response is to use a *410 Gone* response to indicate that the WebHook no longer is active and no further requests should be submitted.</span></span>

<span data-ttu-id="359b4-117">기본적으로 처리기는 모든 WebHook 수신자에 의해 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="359b4-117">By default a handler will be called by all WebHook receivers.</span></span> <span data-ttu-id="359b4-118">그러나 *받는 사람* 속성이 처리기의 이름으로 설정 된 경우 해당 처리기는 해당 수신자의 WebHook 요청을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="359b4-118">However, if the *Receiver* property is set to the name of a handler then that handler will only receive WebHook requests from that receiver.</span></span>

## <a name="processing-a-webhook"></a><span data-ttu-id="359b4-119">WebHook 처리</span><span class="sxs-lookup"><span data-stu-id="359b4-119">Processing a WebHook</span></span>

<span data-ttu-id="359b4-120">처리기가 호출 되 면 WebHook 요청에 대 한 정보를 포함 하는 [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) 을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="359b4-120">When a handler is called, it gets a [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) containing information about the WebHook request.</span></span> <span data-ttu-id="359b4-121">데이터 (일반적으로 HTTP 요청 본문)는 *데이터* 속성에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="359b4-121">The data, typically the HTTP request body, is available from the *Data* property.</span></span>

<span data-ttu-id="359b4-122">데이터 형식은 일반적으로 JSON 또는 HTML 양식 데이터 이지만 원하는 경우 보다 구체적인 형식으로 캐스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="359b4-122">The type of the data is typically JSON or HTML form data, but it is possible to cast to a more specific type if desired.</span></span> <span data-ttu-id="359b4-123">예를 들어 ASP.NET WebHooks 의해 생성 된 사용자 지정 웹 후크를 다음과 같이 형식 [Customnotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) 로 캐스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="359b4-123">For example, the custom WebHooks generated by ASP.NET WebHooks can be cast to the type [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) as follows:</span></span>

```csharp
public class MyWebHookHandler : WebHookHandler
{
    public MyWebHookHandler()
    {
        this.Receiver = "custom";
    }

    public override Task ExecuteAsync(string generator, WebHookHandlerContext context)
    {
        CustomNotifications notifications = context.GetDataOrDefault<CustomNotifications>();
        foreach (var notification in notifications.Notifications)
        {
            ...
        }
        return Task.FromResult(true);
    }
}
```

  ## <a name="queued-processing"></a><span data-ttu-id="359b4-124">대기 중인 처리</span><span class="sxs-lookup"><span data-stu-id="359b4-124">Queued Processing</span></span>

<span data-ttu-id="359b4-125">대부분의 WebHook 발신자는 몇 초 내에 응답이 생성 되지 않으면 WebHook를 다시 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="359b4-125">Most WebHook senders will resend a WebHook if a response is not generated within a handful of seconds.</span></span> <span data-ttu-id="359b4-126">즉, 처리기가 다시 호출 되지 않도록 해당 시간 프레임 내에서 처리를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="359b4-126">This means that your handler must complete the processing within that time frame in order not for it to be called again.</span></span>

<span data-ttu-id="359b4-127">처리가 더 길거나 별도로 처리 되는 경우 [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) 를 사용 하 여 큐에 WebHook 요청을 제출할 수 있습니다 (예: [Azure Storage 큐](https://msdn.microsoft.com/library/azure/dd179353.aspx)).</span><span class="sxs-lookup"><span data-stu-id="359b4-127">If the processing takes longer, or is better handled separately then the [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) can be used to submit the WebHook request to a queue, for example [Azure Storage Queue](https://msdn.microsoft.com/library/azure/dd179353.aspx).</span></span>

<span data-ttu-id="359b4-128">[WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) 구현에 대 한 개요는 다음에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="359b4-128">An outline of a [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) implementation is provided here:</span></span>

```csharp
public class QueueHandler : WebHookQueueHandler
{
    public override Task EnqueueAsync(WebHookQueueContext context)
    {

        // Enqueue WebHookQueueContext to your queuing system of choice

        return Task.FromResult(true);
    }
}
```
