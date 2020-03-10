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
# <a name="httpclient-message-handlers-in-aspnet-web-api"></a>ASP.NET Web API의 HttpClient 메시지 처리기

[Mike Wasson](https://github.com/MikeWasson)

*메시지 처리기* 는 http 요청을 수신 하 고 http 응답을 반환 하는 클래스입니다.

일반적으로 일련의 메시지 처리기가 함께 연결 됩니다. 첫 번째 처리기는 HTTP 요청을 수신 하 고, 일부 처리를 수행 하 고, 다음 처리기에 요청을 제공 합니다. 어느 시점에서 응답이 만들어지고 체인을 백업 합니다. 이 패턴을 *위임* 처리기 라고 합니다.

![](httpclient-message-handlers/_static/image1.png)

클라이언트 쪽에서는 **Httpclient** 클래스가 메시지 처리기를 사용 하 여 요청을 처리 합니다. 기본 처리기는 **Httpclienthandler**로, 네트워크를 통해 요청을 보내고 서버에서 응답을 가져옵니다. 사용자 지정 메시지 처리기를 클라이언트 파이프라인에 삽입할 수 있습니다.

![](httpclient-message-handlers/_static/image2.png)

> [!NOTE]
> 또한 ASP.NET Web API 서버 쪽의 메시지 처리기를 사용 합니다. 자세한 내용은 [HTTP 메시지 처리기](http-message-handlers.md)를 참조 하세요.

## <a name="custom-message-handlers"></a>사용자 지정 메시지 처리기

사용자 지정 메시지 처리기를 쓰려면 **DelegatingHandler** 에서 파생 하 고 **SendAsync** 메서드를 재정의 합니다. 메서드 서명은 다음과 같습니다.

[!code-csharp[Main](httpclient-message-handlers/samples/sample1.cs)]

메서드는 **HttpRequestMessage** 를 입력으로 사용 하 고 **HttpResponseMessage**를 비동기적으로 반환 합니다. 일반적인 구현에서는 다음을 수행 합니다.

1. 요청 메시지를 처리 합니다.
2. `base.SendAsync`를 호출 하 여 요청을 내부 처리기에 보냅니다.
3. 내부 처리기는 응답 메시지를 반환 합니다. 이 단계는 비동기입니다.
4. 응답을 처리 하 고 호출자에 게 반환 합니다.

다음 예제에서는 보내는 요청에 사용자 지정 헤더를 추가 하는 메시지 처리기를 보여 줍니다.

[!code-csharp[Main](httpclient-message-handlers/samples/sample2.cs)]

`base.SendAsync`에 대한 호출은 비동기입니다. 이 호출 후 처리기에서 작업을 수행 하는 경우에는 **wait** 키워드를 사용 하 여 메서드가 완료 된 후 실행을 다시 시작 합니다. 다음 예제에서는 오류 코드를 기록 하는 처리기를 보여 줍니다. 로깅 자체는 그다지 흥미로운 것은 아니지만이 예제에서는 처리기 내에서 응답을 가져오는 방법을 보여 줍니다.

[!code-csharp[Main](httpclient-message-handlers/samples/sample3.cs?highlight=10,13)]

## <a name="adding-message-handlers-to-the-client-pipeline"></a>클라이언트 파이프라인에 메시지 처리기 추가

**Httpclient**에 사용자 지정 처리기를 추가 하려면 **Httpclientfactory. 만들기** 메서드를 사용 합니다.

[!code-csharp[Main](httpclient-message-handlers/samples/sample4.cs)]

메시지 처리기는 **Create** 메서드에 전달 하는 순서 대로 호출 됩니다. 처리기가 중첩 되기 때문에 응답 메시지는 다른 방향으로 이동 합니다. 즉, 마지막 처리기가 응답 메시지를 가져오기 위한 첫 번째 처리기입니다.
