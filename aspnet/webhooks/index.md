---
uid: webhooks/index
title: ASP.NET 웹 후크 개요 | Microsoft Docs
author: rick-anderson
description: ASP.NET 웹 후크에 대 한 소개입니다.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5e2843f0-f499-448f-a712-33d4e9858321
ms.openlocfilehash: 1e21c92e950893c0ff87c63f03f4710a158441fd
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/07/2020
ms.locfileid: "77075088"
---
# <a name="aspnet-webhooks-overview"></a><span data-ttu-id="f794f-103">ASP.NET 웹 후크 개요</span><span class="sxs-lookup"><span data-stu-id="f794f-103">ASP.NET WebHooks overview</span></span>

<span data-ttu-id="f794f-104">WebHook는 Web API와 SaaS 서비스를 연결하는 간단한 pub/sub 모델을 제공하는 가벼운 HTTP 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-104">WebHooks is a lightweight HTTP pattern providing a simple pub/sub model for wiring together Web APIs and SaaS services.</span></span> <span data-ttu-id="f794f-105">서비스에서 이벤트가 발생하면 등록된 구독자에게 HTTP POST 요청의 형태로 알림이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-105">When an event happens in a service, a notification is sent in the form of an HTTP POST request to registered subscribers.</span></span> <span data-ttu-id="f794f-106">POST 요청에는 수신자가 적절하게 대처할 수 있도록 이벤트에 대한 정보를 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-106">The POST request contains information about the event which makes it possible for the receiver to act accordingly.</span></span>

<span data-ttu-id="f794f-107">편의상 웹 후크는 [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [여유](http://www.slack.com), [스트라이프](http://www.stripe.com), [Trello](http://www.trello.com/)등의 많은 서비스에 의해 이미 노출 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-107">Because of their simplicity, WebHooks are already exposed by a large number of services including [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/), and many more.</span></span> <span data-ttu-id="f794f-108">예를 들어 웹 후크는 [Dropbox](http://dropbox.com/)에서 파일이 변경 되었거나, GitHub에서 코드 변경이 커밋되거나, [PayPal](http://www.paypal.com/)에서 지불이 시작 되었거나 [Trello](http://www.trello.com/)에서 카드가 만들어진 것을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-108">For example, a WebHook can indicate that a file has changed in [Dropbox](http://dropbox.com/), or a code change has been committed in GitHub, or a payment has been initiated in [PayPal](http://www.paypal.com/), or a card has been created in [Trello](http://www.trello.com/).</span></span> <span data-ttu-id="f794f-109">가능성은 무한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-109">The possibilities are endless!</span></span>

<span data-ttu-id="f794f-110">Microsoft ASP.NET Webhook를 사용 하면 웹 후크를 ASP.NET 응용 프로그램의 일부로 쉽게 보내고 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-110">Microsoft ASP.NET WebHooks makes it easier to both send and receive WebHooks as part of your ASP.NET application:</span></span>

* <span data-ttu-id="f794f-111">수신 측에서는 여러 WebHook 공급자에서 웹 후크를 받고 처리 하기 위한 공통 모델을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-111">On the receiving side, it provides a common model for receiving and processing WebHooks from any number of WebHook providers.</span></span> <span data-ttu-id="f794f-112">[Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [pusher](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [여유 시간](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/),[WordPress](http://www.wordpress.com) 및 [Zendesk](https://www.zendesk.com/) 에 대 한 지원 기능이 제공 되지만 더 많은 지원을 추가 하는 것이 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-112">It comes out of the box with support for [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Pusher](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/),[WordPress](http://www.wordpress.com) and [Zendesk](https://www.zendesk.com/) but it is easy to add support for more.</span></span>

* <span data-ttu-id="f794f-113">보내는 쪽에서는 구독을 관리 및 저장 하는 것 뿐만 아니라 올바른 구독자 집합에 이벤트 알림을 보내는 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-113">On the sending side it provides support for managing and storing subscriptions as well as for sending event notifications to the right set of subscribers.</span></span> <span data-ttu-id="f794f-114">이렇게 하면 구독자가 구독할 수 있는 사용자 고유의 이벤트 집합을 정의 하 고 발생 하는 경우이를 알릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-114">This allows you to define your own set of events that subscribers can subscribe to and notify them when things happens.</span></span>

<span data-ttu-id="f794f-115">시나리오에 따라 두 부분을 함께 또는 별도로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-115">The two parts can be used together or apart depending on your scenario.</span></span> <span data-ttu-id="f794f-116">다른 서비스에서 Webhook를 수신 해야 하는 경우에는 받는 사람 부분만 사용할 수 있습니다. 다른 사용자가 사용할 수 있도록 웹 후크를 표시 하려는 경우에만이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-116">If you only need to receive WebHooks from other services then you can use just the receiver part; if you only want to expose WebHooks for others to consume, then you can do just that.</span></span>

<span data-ttu-id="f794f-117">코드는 ASP.NET Web API 2 및 ASP.NET MVC 5를 대상으로 하며 [GitHub에서 OSS](https://github.com/aspnet/WebHooks)로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-117">The code targets ASP.NET Web API 2 and ASP.NET MVC 5 and is available as [OSS on GitHub](https://github.com/aspnet/WebHooks).</span></span>

## <a name="webhooks-overview"></a><span data-ttu-id="f794f-118">웹 후크 개요</span><span class="sxs-lookup"><span data-stu-id="f794f-118">WebHooks Overview</span></span>

<span data-ttu-id="f794f-119">웹 후크는 서비스에서 서비스에 사용 되는 방식을 다르지만 기본 개념은 동일 함을 의미 하는 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-119">WebHooks is a pattern which means that it varies how it is used from service to service but the basic idea is the same.</span></span> <span data-ttu-id="f794f-120">사용자가 다른 위치에서 발생 하는 이벤트를 구독할 수 있는 간단한 pub/sub 모델로 웹 후크를 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-120">You can think of WebHooks as a simple pub/sub model where a user can subscribe to events happening elsewhere.</span></span> <span data-ttu-id="f794f-121">이벤트 알림은 이벤트 자체에 대 한 정보를 포함 하는 HTTP POST 요청으로 전파 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-121">The event notifications are propagated as HTTP POST requests containing information about the event itself.</span></span>

<span data-ttu-id="f794f-122">일반적으로 HTTP POST 요청은 webhook을 트리거하는 이벤트에 대 한 정보를 포함 하 여 웹 후크 발신자가 결정 한 JSON 개체 또는 HTML 양식 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-122">Typically the HTTP POST request contains a JSON object or HTML form data determined by the WebHook sender including information about the event causing the WebHook to trigger.</span></span> <span data-ttu-id="f794f-123">예를 들어 [GitHub](https://www.github.com/) 의 WebHook POST 요청 본문은 특정 리포지토리에서 새 문제가 열리는 경우 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-123">For example, a WebHook POST request body from [GitHub](https://www.github.com/) looks like this as a result of a new issue being opened in a particular repository:</span></span>

```json
{
  "action": "opened",
  "issue": {
      "url": "https://api.github.com/repos/octocat/Hello-World/issues/1347",
      "number": 1347,
      ...
  },
  "repository": {
      "id": 1296269,
      "full_name": "octocat/Hello-World",
      "owner": {
          "login": "octocat",
          "id": 1
          ...
      },
      ...
  },
  "sender": {
      "login": "octocat",
      "id": 1,
      ...
  }
}
```

<span data-ttu-id="f794f-124">WebHook가 의도 된 보낸 사람 으로부터 실제로 제공 되는지 확인 하기 위해 POST 요청은 어떤 방식으로든 보안 된 후 수신자가 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-124">To ensure that the WebHook is indeed from the intended sender, the POST request is secured in some way and then verified by the receiver.</span></span> <span data-ttu-id="f794f-125">예를 들어 [GitHub webhook](https://developer.github.com/webhooks/) 에는 수신기 구현에 의해 확인 되는 요청 본문의 해시가 있는 *X 허브 서명* HTTP 헤더가 포함 되어 있으므로 걱정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-125">For example, [GitHub WebHooks](https://developer.github.com/webhooks/) includes an *X-Hub-Signature* HTTP header with a hash of the request body which is checked by the receiver implementation so you don't have to worry about it.</span></span>

<span data-ttu-id="f794f-126">WebHook 흐름은 일반적으로 다음과 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-126">The WebHook flow generally goes something like this:</span></span>

* <span data-ttu-id="f794f-127">웹 후크 발신자는 클라이언트에서 구독할 수 있는 이벤트를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-127">The WebHook sender exposes events that a client can subscribe to.</span></span> <span data-ttu-id="f794f-128">이 이벤트는 시스템의 관찰 가능한 변경 내용 (예: 새 데이터 항목이 삽입 되었거나 프로세스가 완료 되었거나 다른 항목)을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-128">The events describe observable changes to the system, for example that a new data item has been inserted, that a process has completed, or something else.</span></span>

* <span data-ttu-id="f794f-129">웹 후크 수신기는 다음 네 가지 항목으로 구성 된 WebHook를 등록 하 여 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-129">The WebHook receiver subscribes by registering a WebHook consisting of four things:</span></span>

     1. <span data-ttu-id="f794f-130">HTTP POST 요청 형식으로 이벤트 알림이 게시 되어야 하는 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-130">A URI for where the event notification should be posted in the form of an HTTP POST request;</span></span>

     2. <span data-ttu-id="f794f-131">WebHook를 발생 시킬 특정 이벤트를 설명 하는 필터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-131">A set of filters describing the particular events for which the WebHook should be fired;</span></span>

     3. <span data-ttu-id="f794f-132">HTTP POST 요청에 서명 하는 데 사용 되는 비밀 키입니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-132">A secret key which is used to sign the HTTP POST request;</span></span>

     4. <span data-ttu-id="f794f-133">HTTP POST 요청에 포함할 추가 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-133">Additional data which is to be included in the HTTP POST request.</span></span> <span data-ttu-id="f794f-134">예를 들어 HTTP POST 요청 본문에 포함 된 추가 HTTP 헤더 필드 또는 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-134">This can for example be additional HTTP header fields or properties included in the HTTP POST request body.</span></span>

* <span data-ttu-id="f794f-135">이벤트가 발생 하면 일치 하는 WebHook 등록이 검색 되 고 HTTP POST 요청이 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-135">Once an event happens, the matching WebHook registrations are found and HTTP POST requests are submitted.</span></span> <span data-ttu-id="f794f-136">일반적으로 수신자가 응답 하지 않거나 HTTP POST 요청으로 인해 오류 응답이 발생 하는 경우 HTTP POST 요청 생성은 여러 번 다시 시도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-136">Typically, the generation of the HTTP POST requests are retried several times if for some reason the recipient is not responding or the HTTP POST request results in an error response.</span></span>

## <a name="webhooks-processing-pipeline"></a><span data-ttu-id="f794f-137">WebHooks 처리 파이프라인</span><span class="sxs-lookup"><span data-stu-id="f794f-137">WebHooks Processing Pipeline</span></span>

<span data-ttu-id="f794f-138">들어오는 웹 후크에 대 한 Microsoft ASP.NET 웹 후크 처리 파이프라인은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-138">The Microsoft ASP.NET WebHooks processing pipeline for incoming WebHooks looks like this:</span></span>

![ASP.NET 웹 후크 처리 파이프라인](_static/WebHookReceivers.png)

<span data-ttu-id="f794f-140">다음 두 가지 주요 개념은 *수신자* 및 *처리기*입니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-140">The two key concepts here are *Receivers* and *Handlers*:</span></span>

* <span data-ttu-id="f794f-141">*수신자* 는 지정 된 발신자 로부터 특정 버전의 webhook를 처리 하 고, 웹 후크 요청이 의도 된 발신자와 동일한 지 확인 하기 위해 보안 검사를 적용 하는 일을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-141">*Receivers* are responsible for handling the particular flavor of WebHook from a given sender and for enforcing security checks to ensure that the WebHook request indeed is from the intended sender.</span></span>

* <span data-ttu-id="f794f-142">*처리기* 는 일반적으로 사용자 코드가 특정 WebHook 처리를 실행 하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="f794f-142">*Handlers* are typically where user code runs processing the particular WebHook.</span></span>

<span data-ttu-id="f794f-143">다음 노드에서 이러한 개념에 대 한 자세한 내용은을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="f794f-143">In the following nodes these concepts are described in more details.</span></span>
