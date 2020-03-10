---
uid: webhooks/receiving/receivers
title: ASP.NET WebHooks 수신자 | Microsoft Docs
author: rick-anderson
description: ASP.NET 웹 후크 수신기
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 6cdea089-15b2-4732-8c68-921ca561a8f1
ms.openlocfilehash: d771a588b23abcd7b1b33e694af17b219683fc48
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78463463"
---
# <a name="aspnet-webhooks-receivers"></a><span data-ttu-id="51d38-103">ASP.NET 웹 후크 수신기</span><span class="sxs-lookup"><span data-stu-id="51d38-103">ASP.NET WebHooks receivers</span></span>

<span data-ttu-id="51d38-104">웹 후크 수신은 발신자가 누구 인지에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="51d38-104">Receiving WebHooks depends on who the sender is.</span></span> <span data-ttu-id="51d38-105">구독자가 정말로 수신 대기 중인지 확인 하는 추가 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d38-105">Sometimes there are additional steps registering a WebHook verifying that the subscriber is really listening.</span></span> <span data-ttu-id="51d38-106">일부 Webhook는 HTTP POST 요청에 이벤트 정보에 대 한 참조만 포함 된 후 독립적으로 검색 되는 푸시-끌어오기 모델을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="51d38-106">Some WebHooks provide a push-to-pull model where the HTTP POST request only contains a reference to the event information which is then to be retrieved independently.</span></span> <span data-ttu-id="51d38-107">보안 모델은 약간의 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d38-107">Often the security model varies quite a bit.</span></span>

<span data-ttu-id="51d38-108">웹 후크에 Microsoft ASP.NET 하는 목적은 웹 후크에 대 한 특정 변형을 처리 하는 방법을 파악 하는 데 많은 시간을 소비 하지 않고 API를 연결 하는 것이 더 간단 하 고 일관 되도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="51d38-108">The purpose of Microsoft ASP.NET WebHooks is to make it both simpler and more consistent to wire up your API without spending a lot of time figuring out how to handle any particular variant of WebHooks.</span></span>

<span data-ttu-id="51d38-109">웹 후크 수신기는 특정 발신자의 webhook를 수락 하 고 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="51d38-109">A WebHook receiver is responsible for accepting and verifying WebHooks from a particular sender.</span></span> <span data-ttu-id="51d38-110">웹 후크 수신기는 각각 고유한 구성을 사용 하 여 원하는 수의 웹 후크를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d38-110">A WebHook receiver can support any number of WebHooks, each with their own configuration.</span></span> <span data-ttu-id="51d38-111">예를 들어 GitHub WebHook 수신기는 다 수의 GitHub 리포지토리에서 웹 후크를 수락할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d38-111">For example, the GitHub WebHook receiver can accept WebHooks from any number of GitHub repositories.</span></span>

## <a name="webhook-receiver-uris"></a><span data-ttu-id="51d38-112">WebHook 수신기 Uri</span><span class="sxs-lookup"><span data-stu-id="51d38-112">WebHook Receiver URIs</span></span>

<span data-ttu-id="51d38-113">Microsoft ASP.NET 웹 후크를 설치 하면 개방형 서비스의 서비스에서 WebHook 요청을 수락 하는 일반 웹 후크 컨트롤러를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d38-113">By installing Microsoft ASP.NET WebHooks you get a general WebHook controller which accepts WebHook requests from an open-ended number of services.</span></span> <span data-ttu-id="51d38-114">요청이 도착 하면 특정 WebHook 발신자를 처리 하기 위해 설치한 적절 한 수신기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="51d38-114">When a request arrives, it picks the appropriate receiver that you have installed for handling a particular WebHook sender.</span></span>

<span data-ttu-id="51d38-115">이 컨트롤러의 URI는 서비스에 등록 하 고 형식이 인 WebHook URI입니다.</span><span class="sxs-lookup"><span data-stu-id="51d38-115">The URI of this controller is the WebHook URI that you register with the service and is of the form:</span></span>

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

<span data-ttu-id="51d38-116">보안상의 이유로, 대부분의 WebHook 수신기는 URI를 *https* uri로 사용 해야 하며, 경우에 따라 의도 된 당사자만이 위의 URI로 webhook를 보낼 수 있도록 하는 데 사용 되는 추가 쿼리 매개 변수도 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51d38-116">For security reasons, many WebHook receivers require that the URI is an *https* URI and in some cases it must also contain an additional query parameter which is used to enforce that only the intended party can send WebHooks to the URI above.</span></span>

<span data-ttu-id="51d38-117">`<receiver>` 구성 요소는 수신기의 이름 (예: `github` 또는 `slack`입니다.</span><span class="sxs-lookup"><span data-stu-id="51d38-117">The `<receiver>` component is the name of the receiver, for example `github` or `slack`.</span></span>

<span data-ttu-id="51d38-118">*{Id}* 는 특정 WebHook 수신기 구성을 식별 하는 데 사용할 수 있는 선택적 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="51d38-118">The *{id}* is an optional identifier which can be used to identify a particular WebHook receiver configuration.</span></span> <span data-ttu-id="51d38-119">이를 사용 하 여 N 개의 WebHooks를 특정 수신기에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d38-119">This can be used to register N WebHooks with a particular receiver.</span></span> <span data-ttu-id="51d38-120">예를 들어 다음 세 개의 Uri를 사용 하 여 세 개의 독립 웹 후크를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d38-120">For example, the following three URIs can be used to register for three independent WebHooks:</span></span>

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a><span data-ttu-id="51d38-121">WebHook 수신기 설치</span><span class="sxs-lookup"><span data-stu-id="51d38-121">Installing a WebHook Receiver</span></span>

<span data-ttu-id="51d38-122">Microsoft ASP.NET webhook를 사용 하 여 웹 후크를 수신 하려면 먼저 WebHook 공급자에 대 한 Nuget 패키지를 설치 하거나 웹 후크를 수신 하려는 공급자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="51d38-122">To receive WebHooks using Microsoft ASP.NET WebHooks, you first install the Nuget package for the WebHook provider or providers you want to receive WebHooks from.</span></span> <span data-ttu-id="51d38-123">Nuget 패키지의 이름은 Microsoft. m p. m. [수신자](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) .</span><span class="sxs-lookup"><span data-stu-id="51d38-123">The Nuget packages are named [Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) where the last part indicates the service supported.</span></span> <span data-ttu-id="51d38-124">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="51d38-124">For example</span></span>

<span data-ttu-id="51d38-125">ASP.NET는 GitHub 및 Microsoft의 webhook에서 웹 후크를 수신 하도록 지원 합니다. [사용자 지정](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) [은](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) 웹 후크에 의해 생성 된 웹 후크를 수신 하도록 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="51d38-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) provides support for receiving WebHooks from GitHub and [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) provides support for receiving WebHooks generated by ASP.NET WebHooks.</span></span>

<span data-ttu-id="51d38-126">기본적으로 Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, 여유 시간, Stripe, Trello 및 WordPress에 대 한 지원을 확인할 수 있지만, 원하는 수의 다른 공급자를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d38-126">Out of the box you can find support for Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello, and WordPress but it is possible to support any number of other providers.</span></span>

## <a name="configuring-a-webhook-receiver"></a><span data-ttu-id="51d38-127">WebHook 수신기 구성</span><span class="sxs-lookup"><span data-stu-id="51d38-127">Configuring a WebHook Receiver</span></span>

<span data-ttu-id="51d38-128">웹 후크 수신기는 [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) 인터페이스을 통해 구성 되며, 해당 인터페이스의 특정 구현을 종속성 주입 모델을 사용 하 여 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d38-128">WebHook Receivers are configured through the [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) inteface and particular implementations of that interface can be registered using any dependency injection model.</span></span> <span data-ttu-id="51d38-129">기본 구현에서는 web.config 파일에 설정 하거나 Azure Web Apps를 사용 하는 경우 [Azure Portal](https://portal.azure.com/)을 통해 설정할 수 있는 응용 프로그램 설정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="51d38-129">The default implementation uses Application Settings which can either be set in the Web.config file, or, if using Azure Web Apps, can be set through the [Azure Portal](https://portal.azure.com/).</span></span>

![Azure 앱 설정](_static/AzureAppSettings.png)

<span data-ttu-id="51d38-131">응용 프로그램 설정 키에 대 한 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="51d38-131">The format for Application Setting keys is as follows:</span></span>

```
MS_WebHookReceiverSecret_<receiver>
```

<span data-ttu-id="51d38-132">값은 WebHooks 등록 된 *{id}* 값과 일치 하는 값의 쉼표로 구분 된 목록입니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="51d38-132">The value is a comma-separated list of values matching the *{id}* values for which WebHooks have been registered, for example:</span></span>

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a><span data-ttu-id="51d38-133">WebHook 수신기 초기화</span><span class="sxs-lookup"><span data-stu-id="51d38-133">Initializing a WebHook Receiver</span></span>

<span data-ttu-id="51d38-134">WebHook 수신기는 일반적으로 *Webapiconfig* 정적 클래스에 등록 하 여 초기화 됩니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="51d38-134">WebHook Receivers are initialized by registering them, typically in the *WebApiConfig* static class, for example:</span></span>

```csharp
namespace WebHookReceivers
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            // Load receivers
            config.InitializeReceiveGitHubWebHooks();
        }
    }
}
```
