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
# <a name="introduction-to-scaleout-in-signalr-1x"></a><span data-ttu-id="90f2e-102">SignalR 1.x의 규모 확장 소개</span><span class="sxs-lookup"><span data-stu-id="90f2e-102">Introduction to Scaleout in SignalR 1.x</span></span>

<span data-ttu-id="90f2e-103">사람, [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="90f2e-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="90f2e-104">일반적으로 웹 응용 프로그램의 크기를 조정 하는 두 가지 방법이 있습니다 (강화 및 *규모*확장 *).*</span><span class="sxs-lookup"><span data-stu-id="90f2e-104">In general, there are two ways to scale a web application: *scale up* and *scale out*.</span></span>

- <span data-ttu-id="90f2e-105">강화는 더 큰 RAM, Cpu 등의 더 큰 규모의 서버 (또는 더 큰 VM)를 사용 하는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-105">Scale up means using a larger server (or a larger VM) with more RAM, CPUs, etc.</span></span>
- <span data-ttu-id="90f2e-106">규모 확장은 로드를 처리할 서버를 더 추가 하는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-106">Scale out means adding more servers to handle the load.</span></span>

<span data-ttu-id="90f2e-107">수직 확장의 문제는 컴퓨터 크기에 대 한 제한을 신속 하 게 적중 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-107">The problem with scaling up is that you quickly hit a limit on the size of the machine.</span></span> <span data-ttu-id="90f2e-108">그 외에도 규모를 확장 해야 합니다. 그러나 규모를 확장할 때 클라이언트는 다른 서버로 라우팅될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-108">Beyond that, you need to scale out. However, when you scale out, clients can get routed to different servers.</span></span> <span data-ttu-id="90f2e-109">한 서버에 연결 된 클라이언트는 다른 서버에서 보낸 메시지를 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-109">A client that is connected to one server will not receive messages sent from another server.</span></span>

![](scaleout-in-signalr/_static/image1.png)

<span data-ttu-id="90f2e-110">한 가지 해결 방법은 *후면판*이라는 구성 요소를 사용 하 여 서버 간에 메시지를 전달 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-110">One solution is to forward messages between servers, using a component called a *backplane*.</span></span> <span data-ttu-id="90f2e-111">후면판을 사용 하는 경우 각 응용 프로그램 인스턴스는 후면판으로 메시지를 보내고, 후면판은이를 다른 응용 프로그램 인스턴스로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-111">With a backplane enabled, each application instance sends messages to the backplane, and the backplane forwards them to the other application instances.</span></span> <span data-ttu-id="90f2e-112">(전자 제품에서 후면판은 병렬 커넥터 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-112">(In electronics, a backplane is a group of parallel connectors.</span></span> <span data-ttu-id="90f2e-113">SignalR 후면판은 여러 서버를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-113">By analogy, a SignalR backplane connects multiple servers.)</span></span>

![](scaleout-in-signalr/_static/image2.png)

<span data-ttu-id="90f2e-114">SignalR는 현재 다음 세 가지 백플레인을를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-114">SignalR currently provides three backplanes:</span></span>

- <span data-ttu-id="90f2e-115">**Azure Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="90f2e-115">**Azure Service Bus**.</span></span> <span data-ttu-id="90f2e-116">Service Bus는 구성 요소가 느슨하게 결합 된 방식으로 메시지를 보낼 수 있도록 하는 메시징 인프라입니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-116">Service Bus is a messaging infrastructure that allows components to send messages in a loosely coupled way.</span></span>
- <span data-ttu-id="90f2e-117">**Redis**.</span><span class="sxs-lookup"><span data-stu-id="90f2e-117">**Redis**.</span></span> <span data-ttu-id="90f2e-118">Redis는 메모리 내 키-값 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-118">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="90f2e-119">Redis는 메시지를 보내기 위한 게시/구독 ("pub/sub") 패턴을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-119">Redis supports a publish/subscribe ("pub/sub") pattern for sending messages.</span></span>
- <span data-ttu-id="90f2e-120">**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="90f2e-120">**SQL Server**.</span></span> <span data-ttu-id="90f2e-121">SQL Server 후면판은 메시지를 SQL 테이블에 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-121">The SQL Server backplane writes messages to SQL tables.</span></span> <span data-ttu-id="90f2e-122">후면판은 효율적인 메시징의 Service Broker를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-122">The backplane uses Service Broker for efficient messaging.</span></span> <span data-ttu-id="90f2e-123">그러나 Service Broker를 사용 하도록 설정 하지 않은 경우에도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-123">However, it also works if Service Broker is not enabled.</span></span>

<span data-ttu-id="90f2e-124">Azure에 응용 프로그램을 배포 하는 경우 Azure Service Bus 백플레인를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-124">If you deploy your application on Azure, consider using the Azure Service Bus backplane.</span></span> <span data-ttu-id="90f2e-125">사용자의 서버 팜에 배포 하는 경우 SQL Server 또는 Redis 백플레인을을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-125">If you are deploying to your own server farm, consider the SQL Server or Redis backplanes.</span></span>

<span data-ttu-id="90f2e-126">다음 항목에는 각 후면판에 대 한 단계별 자습서가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-126">The following topics contain step-by-step tutorials for each backplane:</span></span>

- [<span data-ttu-id="90f2e-127">Azure Service Bus로 SignalR 규모 확장</span><span class="sxs-lookup"><span data-stu-id="90f2e-127">SignalR Scaleout with Azure Service Bus</span></span>](scaleout-with-windows-azure-service-bus.md)
- [<span data-ttu-id="90f2e-128">Redis로 SignalR 규모 확장</span><span class="sxs-lookup"><span data-stu-id="90f2e-128">SignalR Scaleout with Redis</span></span>](scaleout-with-redis.md)
- [<span data-ttu-id="90f2e-129">SQL Server로 SignalR 규모 확장</span><span class="sxs-lookup"><span data-stu-id="90f2e-129">SignalR Scaleout with SQL Server</span></span>](scaleout-with-sql-server.md)

## <a name="implementation"></a><span data-ttu-id="90f2e-130">구현</span><span class="sxs-lookup"><span data-stu-id="90f2e-130">Implementation</span></span>

<span data-ttu-id="90f2e-131">SignalR에서 모든 메시지는 메시지 버스를 통해 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-131">In SignalR, every message is sent through a message bus.</span></span> <span data-ttu-id="90f2e-132">메시지 버스는 게시/구독 추상화를 제공 하는 [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) 인터페이스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-132">A message bus implements the [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) interface, which provides a publish/subscribe abstraction.</span></span> <span data-ttu-id="90f2e-133">백플레인을는 기본 **IMessageBus** 를 해당 후면판 용으로 설계 된 버스로 바꿔 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-133">The backplanes work by replacing the default **IMessageBus** with a bus designed for that backplane.</span></span> <span data-ttu-id="90f2e-134">예를 들어 Redis에 대 한 메시지 버스는 [Redismessagebus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.redis.redismessagebus(v=vs.100).aspx)이며, Redis [pub/sub](http://redis.io/topics/pubsub) 메커니즘을 사용 하 여 메시지를 보내고 받습니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-134">For example, the message bus for Redis is [RedisMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.redis.redismessagebus(v=vs.100).aspx), and it uses the Redis [pub/sub](http://redis.io/topics/pubsub) mechanism to send and receive messages.</span></span>

<span data-ttu-id="90f2e-135">각 서버 인스턴스는 버스를 통해 후면판에 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-135">Each server instance connects to the backplane through the bus.</span></span> <span data-ttu-id="90f2e-136">메시지가 전송 되 면 후면판으로 이동 하 여 후면판에서 모든 서버에 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-136">When a message is sent, it goes to the backplane, and the backplane sends it to every server.</span></span> <span data-ttu-id="90f2e-137">서버는 후면판에서 메시지를 가져오는 경우 해당 메시지를 로컬 캐시에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-137">When a server gets a message from the backplane, it puts the message in its local cache.</span></span> <span data-ttu-id="90f2e-138">그런 다음 서버는 로컬 캐시에서 클라이언트로 메시지를 배달 합니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-138">The server then delivers messages to clients from its local cache.</span></span>

<span data-ttu-id="90f2e-139">각 클라이언트 연결에 대해 메시지 스트림 읽기의 클라이언트 진행 상태는 커서를 사용 하 여 추적 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-139">For each client connection, the client's progress in reading the message stream is tracked using a cursor.</span></span> <span data-ttu-id="90f2e-140">커서는 메시지 스트림의 위치를 나타냅니다. 클라이언트에서 연결을 끊은 다음 다시 연결 하면 클라이언트의 커서 값 이후에 도착 한 모든 메시지에 대해 버스에 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-140">(A cursor represents a position in the message stream.) If a client disconnects and then reconnects, it asks the bus for any messages that arrived after the client's cursor value.</span></span> <span data-ttu-id="90f2e-141">연결에서 [긴 폴링을](../getting-started/introduction-to-signalr.md#transports)사용 하는 경우에도 동일한 작업이 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-141">The same thing happens when a connection uses [long polling](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="90f2e-142">긴 폴링 요청이 완료 된 후 클라이언트는 새 연결을 열고 커서 뒤에 도착 한 메시지를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-142">After a long poll request completes, the client opens a new connection and asks for messages that arrived after the cursor.</span></span>

<span data-ttu-id="90f2e-143">커서 메커니즘은 클라이언트가 다시 연결 시 다른 서버에 라우팅되는 경우에도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-143">The cursor mechanism works even if a client is routed to a different server on reconnect.</span></span> <span data-ttu-id="90f2e-144">후면판은 모든 서버를 인식 하며 클라이언트가 연결 하는 서버에 상관 없습니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-144">The backplane is aware of all the servers, and it doesn't matter which server a client connects to.</span></span>

## <a name="limitations"></a><span data-ttu-id="90f2e-145">제한 사항</span><span class="sxs-lookup"><span data-stu-id="90f2e-145">Limitations</span></span>

<span data-ttu-id="90f2e-146">후면판을 사용 하면 클라이언트가 단일 서버 노드에 직접 통신 하는 경우 최대 메시지 처리량은 보다 낮습니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-146">Using a backplane, the maximum message throughput is lower than it is when clients talk directly to a single server node.</span></span> <span data-ttu-id="90f2e-147">이는 후면판이 모든 메시지를 모든 노드에 전달 하므로 후면판이 병목 상태가 될 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-147">That's because the backplane forwards every message to every node, so the backplane can become a bottleneck.</span></span> <span data-ttu-id="90f2e-148">이 제한이 문제 인지 여부는 응용 프로그램에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-148">Whether this limitation is a problem depends on the application.</span></span> <span data-ttu-id="90f2e-149">예를 들어 몇 가지 일반적인 SignalR 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-149">For example, here are some typical SignalR scenarios:</span></span>

- <span data-ttu-id="90f2e-150">[서버 브로드캐스트](tutorial-server-broadcast-with-aspnet-signalr.md) (예: 주식 종목): 백플레인을 서버에서 메시지를 보내는 속도를 제어 하므로이 시나리오에 대해 잘 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-150">[Server broadcast](tutorial-server-broadcast-with-aspnet-signalr.md) (e.g., stock ticker): Backplanes work well for this scenario, because the server controls the rate at which messages are sent.</span></span>
- <span data-ttu-id="90f2e-151">[클라이언트-클라이언트](tutorial-getting-started-with-signalr.md) (예: 채팅):이 시나리오에서는 메시지 수가 클라이언트 수로 확장 되 면 후면판에서 병목 현상이 발생할 수 있습니다. 즉, 더 많은 클라이언트에 연결 될 때 메시지의 비율이 비례적으로 증가 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-151">[Client-to-client](tutorial-getting-started-with-signalr.md) (e.g., chat): In this scenario, the backplane might be a bottleneck if the number of messages scales with the number of clients; that is, if the rate of messages grows proportionally as more clients join.</span></span>
- <span data-ttu-id="90f2e-152">[높은 빈도 실시간](tutorial-high-frequency-realtime-with-signalr.md) (예: 실시간 게임):이 시나리오에는 후면판을 권장 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-152">[High-frequency realtime](tutorial-high-frequency-realtime-with-signalr.md) (e.g., real-time games): A backplane is not recommended for this scenario.</span></span>

## <a name="enabling-tracing-for-signalr-scaleout"></a><span data-ttu-id="90f2e-153">SignalR 확장에 대 한 추적 설정</span><span class="sxs-lookup"><span data-stu-id="90f2e-153">Enabling Tracing For SignalR Scaleout</span></span>

<span data-ttu-id="90f2e-154">백플레인을에 대 한 추적을 사용 하도록 설정 하려면 web.config 파일의 루트 **구성** 요소 아래에 다음 섹션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="90f2e-154">To enable tracing for the backplanes, add the following sections to the web.config file, under the root **configuration** element:</span></span>

[!code-html[Main](scaleout-in-signalr/samples/sample1.html)]
