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
# <a name="aspnet-webhooks-handlers"></a>ASP.NET 웹 후크 처리기

WebHook 수신기에서 WebHook 요청의 유효성을 검사 한 후에는 사용자 코드에서 처리할 준비가 된 것입니다. 여기에는 *처리기* 가 제공 됩니다. 처리기는 [IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) 인터페이스에서 파생 되지만 일반적으로 인터페이스에서 직접 파생 하는 대신 [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) 클래스를 사용 합니다.

하나 이상의 처리기에서 WebHook 요청을 처리할 수 있습니다. 처리기는 가장 낮은 값에서 가장 높은 값으로 이동 하 *는 순서에* 따라 순서 대로 호출 됩니다. 여기서 order는 단순 정수입니다 (1에서 100 사이에서 제안 됨).

![WebHook 처리기 순서 속성 다이어그램](_static/Handlers.png)

처리기는 필요에 따라 WebHookHandlerContext에 대 한 *응답* 속성을 설정 하 여 처리를 중지 하 고 응답을 다시 웹 후크에 HTTP 응답으로 보낼 수 있습니다. 위의 경우 처리기 C는 B 보다 높은 순서를 포함 하 고 B는 응답을 설정 하므로 호출 되지 않습니다.

응답을 설정 하는 것은 일반적으로 응답이 원래 API로 정보를 다시 전달할 수 있는 웹 후크에만 해당 됩니다. 이는 응답이 있는 채널에 응답을 다시 게시 하는 여유 시간 webhook을 사용 하는 경우를 예로 들 수 있습니다. 처리기는 해당 특정 수신기에서 웹 후크를 수신 하려는 경우에만 받는 사람 속성을 설정할 수 있습니다. 수신기를 설정 하지 않으면 모든 수신기에 대해 호출 됩니다.

응답의 또 다른 일반적인 용도는 *410 사라진* 응답을 사용 하 여 WebHook가 더 이상 활성 상태가 없고 추가 요청을 제출 하지 않음을 나타내는 것입니다.

기본적으로 처리기는 모든 WebHook 수신자에 의해 호출 됩니다. 그러나 *받는 사람* 속성이 처리기의 이름으로 설정 된 경우 해당 처리기는 해당 수신자의 WebHook 요청을 받습니다.

## <a name="processing-a-webhook"></a>WebHook 처리

처리기가 호출 되 면 WebHook 요청에 대 한 정보를 포함 하는 [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) 을 가져옵니다. 데이터 (일반적으로 HTTP 요청 본문)는 *데이터* 속성에서 사용할 수 있습니다.

데이터 형식은 일반적으로 JSON 또는 HTML 양식 데이터 이지만 원하는 경우 보다 구체적인 형식으로 캐스팅할 수 있습니다. 예를 들어 ASP.NET WebHooks 의해 생성 된 사용자 지정 웹 후크를 다음과 같이 형식 [Customnotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) 로 캐스팅할 수 있습니다.

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

  ## <a name="queued-processing"></a>대기 중인 처리

대부분의 WebHook 발신자는 몇 초 내에 응답이 생성 되지 않으면 WebHook를 다시 전송 합니다. 즉, 처리기가 다시 호출 되지 않도록 해당 시간 프레임 내에서 처리를 완료 해야 합니다.

처리가 더 길거나 별도로 처리 되는 경우 [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) 를 사용 하 여 큐에 WebHook 요청을 제출할 수 있습니다 (예: [Azure Storage 큐](https://msdn.microsoft.com/library/azure/dd179353.aspx)).

[WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) 구현에 대 한 개요는 다음에서 제공 됩니다.

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
