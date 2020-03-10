---
uid: signalr/overview/older-versions/scaleout-in-signalr
title: SignalR 1.x의 확장 소개 | Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 04/29/2013
ms.assetid: 3fd9f11c-799b-4001-bd60-1e70cfc61c19
msc.legacyurl: /signalr/overview/older-versions/scaleout-in-signalr
msc.type: authoredcontent
ms.openlocfilehash: 9bad72d31a0ebc491910ebb128b3b3a7fb537958
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431213"
---
# <a name="introduction-to-scaleout-in-signalr-1x"></a>SignalR 1.x의 규모 확장 소개

사람, [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

일반적으로 웹 응용 프로그램의 크기를 조정 하는 두 가지 방법이 있습니다 (강화 및 *규모*확장 *).*

- 강화는 더 큰 RAM, Cpu 등의 더 큰 규모의 서버 (또는 더 큰 VM)를 사용 하는 것을 의미 합니다.
- 규모 확장은 로드를 처리할 서버를 더 추가 하는 것을 의미 합니다.

수직 확장의 문제는 컴퓨터 크기에 대 한 제한을 신속 하 게 적중 하는 것입니다. 그 외에도 규모를 확장 해야 합니다. 그러나 규모를 확장할 때 클라이언트는 다른 서버로 라우팅될 수 있습니다. 한 서버에 연결 된 클라이언트는 다른 서버에서 보낸 메시지를 받지 않습니다.

![](scaleout-in-signalr/_static/image1.png)

한 가지 해결 방법은 *후면판*이라는 구성 요소를 사용 하 여 서버 간에 메시지를 전달 하는 것입니다. 후면판을 사용 하는 경우 각 응용 프로그램 인스턴스는 후면판으로 메시지를 보내고, 후면판은이를 다른 응용 프로그램 인스턴스로 전달 합니다. (전자 제품에서 후면판은 병렬 커넥터 그룹입니다. SignalR 후면판은 여러 서버를 연결 합니다.

![](scaleout-in-signalr/_static/image2.png)

SignalR는 현재 다음 세 가지 백플레인을를 제공 합니다.

- **Azure Service Bus**. Service Bus는 구성 요소가 느슨하게 결합 된 방식으로 메시지를 보낼 수 있도록 하는 메시징 인프라입니다.
- **Redis**. Redis는 메모리 내 키-값 저장소입니다. Redis는 메시지를 보내기 위한 게시/구독 ("pub/sub") 패턴을 지원 합니다.
- **SQL Server**. SQL Server 후면판은 메시지를 SQL 테이블에 기록 합니다. 후면판은 효율적인 메시징의 Service Broker를 사용 합니다. 그러나 Service Broker를 사용 하도록 설정 하지 않은 경우에도 작동 합니다.

Azure에 응용 프로그램을 배포 하는 경우 Azure Service Bus 백플레인를 사용 하는 것이 좋습니다. 사용자의 서버 팜에 배포 하는 경우 SQL Server 또는 Redis 백플레인을을 고려 합니다.

다음 항목에는 각 후면판에 대 한 단계별 자습서가 포함 되어 있습니다.

- [Azure Service Bus로 SignalR 규모 확장](scaleout-with-windows-azure-service-bus.md)
- [Redis로 SignalR 규모 확장](scaleout-with-redis.md)
- [SQL Server로 SignalR 규모 확장](scaleout-with-sql-server.md)

## <a name="implementation"></a>구현

SignalR에서 모든 메시지는 메시지 버스를 통해 전송 됩니다. 메시지 버스는 게시/구독 추상화를 제공 하는 [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) 인터페이스를 구현 합니다. 백플레인을는 기본 **IMessageBus** 를 해당 후면판 용으로 설계 된 버스로 바꿔 작동 합니다. 예를 들어 Redis에 대 한 메시지 버스는 [Redismessagebus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.redis.redismessagebus(v=vs.100).aspx)이며, Redis [pub/sub](http://redis.io/topics/pubsub) 메커니즘을 사용 하 여 메시지를 보내고 받습니다.

각 서버 인스턴스는 버스를 통해 후면판에 연결 됩니다. 메시지가 전송 되 면 후면판으로 이동 하 여 후면판에서 모든 서버에 전송 합니다. 서버는 후면판에서 메시지를 가져오는 경우 해당 메시지를 로컬 캐시에 저장 합니다. 그런 다음 서버는 로컬 캐시에서 클라이언트로 메시지를 배달 합니다.

각 클라이언트 연결에 대해 메시지 스트림 읽기의 클라이언트 진행 상태는 커서를 사용 하 여 추적 됩니다. 커서는 메시지 스트림의 위치를 나타냅니다. 클라이언트에서 연결을 끊은 다음 다시 연결 하면 클라이언트의 커서 값 이후에 도착 한 모든 메시지에 대해 버스에 요청 합니다. 연결에서 [긴 폴링을](../getting-started/introduction-to-signalr.md#transports)사용 하는 경우에도 동일한 작업이 수행 됩니다. 긴 폴링 요청이 완료 된 후 클라이언트는 새 연결을 열고 커서 뒤에 도착 한 메시지를 요청 합니다.

커서 메커니즘은 클라이언트가 다시 연결 시 다른 서버에 라우팅되는 경우에도 작동 합니다. 후면판은 모든 서버를 인식 하며 클라이언트가 연결 하는 서버에 상관 없습니다.

## <a name="limitations"></a>제한 사항

후면판을 사용 하면 클라이언트가 단일 서버 노드에 직접 통신 하는 경우 최대 메시지 처리량은 보다 낮습니다. 이는 후면판이 모든 메시지를 모든 노드에 전달 하므로 후면판이 병목 상태가 될 수 있기 때문입니다. 이 제한이 문제 인지 여부는 응용 프로그램에 따라 달라 집니다. 예를 들어 몇 가지 일반적인 SignalR 시나리오는 다음과 같습니다.

- [서버 브로드캐스트](tutorial-server-broadcast-with-aspnet-signalr.md) (예: 주식 종목): 백플레인을 서버에서 메시지를 보내는 속도를 제어 하므로이 시나리오에 대해 잘 작동 합니다.
- [클라이언트-클라이언트](tutorial-getting-started-with-signalr.md) (예: 채팅):이 시나리오에서는 메시지 수가 클라이언트 수로 확장 되 면 후면판에서 병목 현상이 발생할 수 있습니다. 즉, 더 많은 클라이언트에 연결 될 때 메시지의 비율이 비례적으로 증가 하는 경우입니다.
- [높은 빈도 실시간](tutorial-high-frequency-realtime-with-signalr.md) (예: 실시간 게임):이 시나리오에는 후면판을 권장 하지 않습니다.

## <a name="enabling-tracing-for-signalr-scaleout"></a>SignalR 확장에 대 한 추적 설정

백플레인을에 대 한 추적을 사용 하도록 설정 하려면 web.config 파일의 루트 **구성** 요소 아래에 다음 섹션을 추가 합니다.

[!code-html[Main](scaleout-in-signalr/samples/sample1.html)]
