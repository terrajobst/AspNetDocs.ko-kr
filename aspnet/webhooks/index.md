---
uid: webhooks/index
title: ASP.NET 웹 후크 개요 | Microsoft Docs
author: rick-anderson
description: ASP.NET 웹 후크에 대 한 소개입니다.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5e2843f0-f499-448f-a712-33d4e9858321
ms.openlocfilehash: 1e21c92e950893c0ff87c63f03f4710a158441fd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517535"
---
# <a name="aspnet-webhooks-overview"></a>ASP.NET 웹 후크 개요

WebHook는 Web API와 SaaS 서비스를 연결하는 간단한 pub/sub 모델을 제공하는 가벼운 HTTP 패턴입니다. 서비스에서 이벤트가 발생하면 등록된 구독자에게 HTTP POST 요청의 형태로 알림이 전송됩니다. POST 요청에는 수신자가 적절하게 대처할 수 있도록 이벤트에 대한 정보를 포함되어 있습니다.

편의상 웹 후크는 [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [여유](http://www.slack.com), [스트라이프](http://www.stripe.com), [Trello](http://www.trello.com/)등의 많은 서비스에 의해 이미 노출 되어 있습니다. 예를 들어 웹 후크는 [Dropbox](http://dropbox.com/)에서 파일이 변경 되었거나, GitHub에서 코드 변경이 커밋되거나, [PayPal](http://www.paypal.com/)에서 지불이 시작 되었거나 [Trello](http://www.trello.com/)에서 카드가 만들어진 것을 나타낼 수 있습니다. 가능성은 무한 합니다.

Microsoft ASP.NET Webhook를 사용 하면 웹 후크를 ASP.NET 응용 프로그램의 일부로 쉽게 보내고 받을 수 있습니다.

* 수신 측에서는 여러 WebHook 공급자에서 웹 후크를 받고 처리 하기 위한 공통 모델을 제공 합니다. [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [pusher](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [여유 시간](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/),[WordPress](http://www.wordpress.com) 및 [Zendesk](https://www.zendesk.com/) 에 대 한 지원 기능이 제공 되지만 더 많은 지원을 추가 하는 것이 쉽습니다.

* 보내는 쪽에서는 구독을 관리 및 저장 하는 것 뿐만 아니라 올바른 구독자 집합에 이벤트 알림을 보내는 기능을 제공 합니다. 이렇게 하면 구독자가 구독할 수 있는 사용자 고유의 이벤트 집합을 정의 하 고 발생 하는 경우이를 알릴 수 있습니다.

시나리오에 따라 두 부분을 함께 또는 별도로 사용할 수 있습니다. 다른 서비스에서 Webhook를 수신 해야 하는 경우에는 받는 사람 부분만 사용할 수 있습니다. 다른 사용자가 사용할 수 있도록 웹 후크를 표시 하려는 경우에만이 작업을 수행할 수 있습니다.

코드는 ASP.NET Web API 2 및 ASP.NET MVC 5를 대상으로 하며 [GitHub에서 OSS](https://github.com/aspnet/WebHooks)로 사용할 수 있습니다.

## <a name="webhooks-overview"></a>웹 후크 개요

웹 후크는 서비스에서 서비스에 사용 되는 방식을 다르지만 기본 개념은 동일 함을 의미 하는 패턴입니다. 사용자가 다른 위치에서 발생 하는 이벤트를 구독할 수 있는 간단한 pub/sub 모델로 웹 후크를 생각할 수 있습니다. 이벤트 알림은 이벤트 자체에 대 한 정보를 포함 하는 HTTP POST 요청으로 전파 됩니다.

일반적으로 HTTP POST 요청은 webhook을 트리거하는 이벤트에 대 한 정보를 포함 하 여 웹 후크 발신자가 결정 한 JSON 개체 또는 HTML 양식 데이터를 포함 합니다. 예를 들어 [GitHub](https://www.github.com/) 의 WebHook POST 요청 본문은 특정 리포지토리에서 새 문제가 열리는 경우 다음과 같이 표시 됩니다.

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

WebHook가 의도 된 보낸 사람 으로부터 실제로 제공 되는지 확인 하기 위해 POST 요청은 어떤 방식으로든 보안 된 후 수신자가 확인 합니다. 예를 들어 [GitHub webhook](https://developer.github.com/webhooks/) 에는 수신기 구현에 의해 확인 되는 요청 본문의 해시가 있는 *X 허브 서명* HTTP 헤더가 포함 되어 있으므로 걱정할 필요가 없습니다.

WebHook 흐름은 일반적으로 다음과 같이 나타납니다.

* 웹 후크 발신자는 클라이언트에서 구독할 수 있는 이벤트를 노출 합니다. 이 이벤트는 시스템의 관찰 가능한 변경 내용 (예: 새 데이터 항목이 삽입 되었거나 프로세스가 완료 되었거나 다른 항목)을 설명 합니다.

* 웹 후크 수신기는 다음 네 가지 항목으로 구성 된 WebHook를 등록 하 여 구독 합니다.

     1. HTTP POST 요청 형식으로 이벤트 알림이 게시 되어야 하는 URI입니다.

     2. WebHook를 발생 시킬 특정 이벤트를 설명 하는 필터 집합입니다.

     3. HTTP POST 요청에 서명 하는 데 사용 되는 비밀 키입니다.

     4. HTTP POST 요청에 포함할 추가 데이터입니다. 예를 들어 HTTP POST 요청 본문에 포함 된 추가 HTTP 헤더 필드 또는 속성을 사용할 수 있습니다.

* 이벤트가 발생 하면 일치 하는 WebHook 등록이 검색 되 고 HTTP POST 요청이 전송 됩니다. 일반적으로 수신자가 응답 하지 않거나 HTTP POST 요청으로 인해 오류 응답이 발생 하는 경우 HTTP POST 요청 생성은 여러 번 다시 시도 됩니다.

## <a name="webhooks-processing-pipeline"></a>WebHooks 처리 파이프라인

들어오는 웹 후크에 대 한 Microsoft ASP.NET 웹 후크 처리 파이프라인은 다음과 같습니다.

![ASP.NET 웹 후크 처리 파이프라인](_static/WebHookReceivers.png)

다음 두 가지 주요 개념은 *수신자* 및 *처리기*입니다.

* *수신자* 는 지정 된 발신자 로부터 특정 버전의 webhook를 처리 하 고, 웹 후크 요청이 의도 된 발신자와 동일한 지 확인 하기 위해 보안 검사를 적용 하는 일을 담당 합니다.

* *처리기* 는 일반적으로 사용자 코드가 특정 WebHook 처리를 실행 하는 위치입니다.

다음 노드에서 이러한 개념에 대 한 자세한 내용은을 참조 하십시오.
