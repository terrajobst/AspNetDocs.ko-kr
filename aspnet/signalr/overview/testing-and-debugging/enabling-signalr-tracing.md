---
uid: signalr/overview/testing-and-debugging/enabling-signalr-tracing
title: SignalR 추적 사용 | Microsoft Docs
author: bradygaster
description: 이 문서에서는 SignalR 서버 및 클라이언트에 대 한 추적을 사용 하도록 설정 하 고 구성 하는 방법을 설명 합니다. 추적을 사용 하 여 이벤트에 대 한 진단 정보를 볼 수 있습니다 ...
ms.author: bradyg
ms.date: 08/08/2014
ms.assetid: 30060acb-be3e-4347-996f-3870f0c37829
msc.legacyurl: /signalr/overview/testing-and-debugging/enabling-signalr-tracing
msc.type: authoredcontent
ms.openlocfilehash: 34fe2cdb10c4b41a6e8cac7fb1741d53c02dfc80
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467441"
---
# <a name="enabling-signalr-tracing"></a><span data-ttu-id="2cf91-104">SignalR 추적 사용</span><span class="sxs-lookup"><span data-stu-id="2cf91-104">Enabling SignalR Tracing</span></span>

<span data-ttu-id="2cf91-105">만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="2cf91-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="2cf91-106">이 문서에서는 SignalR 서버 및 클라이언트에 대 한 추적을 사용 하도록 설정 하 고 구성 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-106">This document describes how to enable and configure tracing for SignalR servers and clients.</span></span> <span data-ttu-id="2cf91-107">추적을 사용 하면 SignalR 응용 프로그램에서 이벤트에 대 한 진단 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-107">Tracing enables you to view diagnostic information about events in your SignalR application.</span></span>
>
> <span data-ttu-id="2cf91-108">이 항목은 원래 Patrick Fletcher에 의해 작성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-108">This topic was originally written by Patrick Fletcher.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="2cf91-109">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="2cf91-109">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="2cf91-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="2cf91-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="2cf91-111">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="2cf91-111">.NET Framework 4.5</span></span>
> - <span data-ttu-id="2cf91-112">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="2cf91-112">SignalR version 2</span></span>
>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="2cf91-113">질문 및 설명</span><span class="sxs-lookup"><span data-stu-id="2cf91-113">Questions and comments</span></span>
>
> <span data-ttu-id="2cf91-114">이 자습서와 페이지 맨 아래에 있는 의견에서 개선할 수 있는 방법에 대 한 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="2cf91-114">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="2cf91-115">자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-115">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="2cf91-116">추적을 사용 하는 경우 SignalR 응용 프로그램에서 이벤트에 대 한 로그 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-116">When tracing is enabled, a SignalR application creates log entries for events.</span></span> <span data-ttu-id="2cf91-117">클라이언트와 서버 모두에서 이벤트를 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-117">You can log events from both the client and the server.</span></span> <span data-ttu-id="2cf91-118">서버에 대 한 추적은 연결, 확장 공급자 및 메시지 버스 이벤트를 로깅합니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-118">Tracing on the server logs connection, scaleout provider, and message bus events.</span></span> <span data-ttu-id="2cf91-119">클라이언트의 추적은 연결 이벤트를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-119">Tracing on the client logs connection events.</span></span> <span data-ttu-id="2cf91-120">SignalR 2.1 이상에서 클라이언트에 대 한 추적은 허브 호출 메시지의 전체 콘텐츠를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-120">In SignalR 2.1 and later, tracing on the client logs the full content of hub invocation messages.</span></span>

## <a name="contents"></a><span data-ttu-id="2cf91-121">콘텐츠</span><span class="sxs-lookup"><span data-stu-id="2cf91-121">Contents</span></span>

- [<span data-ttu-id="2cf91-122">서버에서 추적 사용</span><span class="sxs-lookup"><span data-stu-id="2cf91-122">Enabling tracing on the server</span></span>](#server)

    - [<span data-ttu-id="2cf91-123">텍스트 파일에 서버 이벤트 로깅</span><span class="sxs-lookup"><span data-stu-id="2cf91-123">Logging server events to text files</span></span>](#server_text)
    - [<span data-ttu-id="2cf91-124">이벤트 로그에 서버 이벤트 로깅</span><span class="sxs-lookup"><span data-stu-id="2cf91-124">Logging server events to the event log</span></span>](#server_eventlog)
- [<span data-ttu-id="2cf91-125">.NET 클라이언트에서 추적 사용 (Windows 데스크톱 응용 프로그램)</span><span class="sxs-lookup"><span data-stu-id="2cf91-125">Enabling tracing in the .NET client (Windows Desktop apps)</span></span>](#net_client)

    - [<span data-ttu-id="2cf91-126">데스크톱 클라이언트 이벤트를 콘솔에 기록</span><span class="sxs-lookup"><span data-stu-id="2cf91-126">Logging Desktop client events to the console</span></span>](#desktop_console)
    - [<span data-ttu-id="2cf91-127">텍스트 파일에 데스크톱 클라이언트 이벤트 로깅</span><span class="sxs-lookup"><span data-stu-id="2cf91-127">Logging Desktop client events to a text file</span></span>](#desktop_text)
- [<span data-ttu-id="2cf91-128">Windows Phone 8 클라이언트에서 추적 사용</span><span class="sxs-lookup"><span data-stu-id="2cf91-128">Enabling tracing in Windows Phone 8 clients</span></span>](#phone)

    - [<span data-ttu-id="2cf91-129">UI에 Windows Phone 클라이언트 이벤트 로깅</span><span class="sxs-lookup"><span data-stu-id="2cf91-129">Logging Windows Phone client events to the UI</span></span>](#phone_ui)
    - [<span data-ttu-id="2cf91-130">디버그 콘솔에 Windows Phone 클라이언트 이벤트 로깅</span><span class="sxs-lookup"><span data-stu-id="2cf91-130">Logging Windows Phone client events to the debug console</span></span>](#phone_debug)
- [<span data-ttu-id="2cf91-131">JavaScript 클라이언트에서 추적 사용</span><span class="sxs-lookup"><span data-stu-id="2cf91-131">Enabling tracing in the JavaScript client</span></span>](#javascript)

<a id="server"></a>
## <a name="enabling-tracing-on-the-server"></a><span data-ttu-id="2cf91-132">서버에서 추적 사용</span><span class="sxs-lookup"><span data-stu-id="2cf91-132">Enabling tracing on the server</span></span>

<span data-ttu-id="2cf91-133">응용 프로그램의 구성 파일 (프로젝트의 형식에 따라 app.config 또는 web.config) 내의 서버에서 추적을 사용 하도록 설정 합니다. 로깅할 이벤트 범주를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-133">You enable tracing on the server within the application's configuration file (either App.config or Web.config depending on the type of project.) You specify which categories of events you want to log.</span></span> <span data-ttu-id="2cf91-134">구성 파일에서 [TraceListener](https://msdn.microsoft.com/library/system.diagnostics.tracelistener(v=vs.110).aspx)의 구현을 사용 하 여 텍스트 파일, Windows 이벤트 로그 또는 사용자 지정 로그에 이벤트를 기록할지 여부도 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-134">In the configuration file, you also specify whether to log the events to a text file, the Windows event log, or a custom log using an implementation of [TraceListener](https://msdn.microsoft.com/library/system.diagnostics.tracelistener(v=vs.110).aspx).</span></span>

<span data-ttu-id="2cf91-135">서버 이벤트 범주는 다음과 같은 종류의 메시지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-135">The server event categories include the following sorts of messages:</span></span>

| <span data-ttu-id="2cf91-136">원본</span><span class="sxs-lookup"><span data-stu-id="2cf91-136">Source</span></span> | <span data-ttu-id="2cf91-137">메시지</span><span class="sxs-lookup"><span data-stu-id="2cf91-137">Messages</span></span> |
| --- | --- |
| <span data-ttu-id="2cf91-138">SignalR.SqlMessageBus</span><span class="sxs-lookup"><span data-stu-id="2cf91-138">SignalR.SqlMessageBus</span></span> | <span data-ttu-id="2cf91-139">SQL 메시지 버스 확장 공급자 설치, 데이터베이스 작업, 오류 및 시간 제한 이벤트</span><span class="sxs-lookup"><span data-stu-id="2cf91-139">SQL Message Bus scaleout provider setup, database operation, error, and timeout events</span></span> |
| <span data-ttu-id="2cf91-140">SignalR.ServiceBusMessageBus</span><span class="sxs-lookup"><span data-stu-id="2cf91-140">SignalR.ServiceBusMessageBus</span></span> | <span data-ttu-id="2cf91-141">Service bus 확장 공급자 토픽 만들기 및 구독, 오류 및 메시징 이벤트</span><span class="sxs-lookup"><span data-stu-id="2cf91-141">Service bus scaleout provider topic creation and subscription, error, and messaging events</span></span> |
| <span data-ttu-id="2cf91-142">SignalR.RedisMessageBus</span><span class="sxs-lookup"><span data-stu-id="2cf91-142">SignalR.RedisMessageBus</span></span> | <span data-ttu-id="2cf91-143">Redis 확장 공급자 연결, 연결 끊기 및 오류 이벤트</span><span class="sxs-lookup"><span data-stu-id="2cf91-143">Redis scaleout provider connection, disconnection, and error events</span></span> |
| <span data-ttu-id="2cf91-144">SignalR.ScaleoutMessageBus</span><span class="sxs-lookup"><span data-stu-id="2cf91-144">SignalR.ScaleoutMessageBus</span></span> | <span data-ttu-id="2cf91-145">확장 messaging 이벤트</span><span class="sxs-lookup"><span data-stu-id="2cf91-145">Scaleout messaging events</span></span> |
| <span data-ttu-id="2cf91-146">SignalR.Transports.WebSocketTransport</span><span class="sxs-lookup"><span data-stu-id="2cf91-146">SignalR.Transports.WebSocketTransport</span></span> | <span data-ttu-id="2cf91-147">WebSocket 전송 연결, 연결 끊기, 메시징 및 오류 이벤트</span><span class="sxs-lookup"><span data-stu-id="2cf91-147">WebSocket transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="2cf91-148">SignalR.Transports.ServerSentEventsTransport</span><span class="sxs-lookup"><span data-stu-id="2cf91-148">SignalR.Transports.ServerSentEventsTransport</span></span> | <span data-ttu-id="2cf91-149">ServerSentEvents 전송 연결, 연결 끊기, 메시징 및 오류 이벤트</span><span class="sxs-lookup"><span data-stu-id="2cf91-149">ServerSentEvents transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="2cf91-150">SignalR.Transports.ForeverFrameTransport</span><span class="sxs-lookup"><span data-stu-id="2cf91-150">SignalR.Transports.ForeverFrameTransport</span></span> | <span data-ttu-id="2cf91-151">ForeverFrame 전송 연결, 연결 끊기, 메시징 및 오류 이벤트</span><span class="sxs-lookup"><span data-stu-id="2cf91-151">ForeverFrame transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="2cf91-152">SignalR.Transports.LongPollingTransport</span><span class="sxs-lookup"><span data-stu-id="2cf91-152">SignalR.Transports.LongPollingTransport</span></span> | <span data-ttu-id="2cf91-153">이상 폴링 전송 연결, 연결 끊기, 메시징 및 오류 이벤트</span><span class="sxs-lookup"><span data-stu-id="2cf91-153">LongPolling transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="2cf91-154">SignalR.Transports.TransportHeartBeat</span><span class="sxs-lookup"><span data-stu-id="2cf91-154">SignalR.Transports.TransportHeartBeat</span></span> | <span data-ttu-id="2cf91-155">전송 연결, 연결 끊기 및 keepalive 이벤트</span><span class="sxs-lookup"><span data-stu-id="2cf91-155">Transport connection, disconnection, and keepalive events</span></span> |
| <span data-ttu-id="2cf91-156">SignalR.ReflectedHubDescriptorProvider</span><span class="sxs-lookup"><span data-stu-id="2cf91-156">SignalR.ReflectedHubDescriptorProvider</span></span> | <span data-ttu-id="2cf91-157">허브 검색 이벤트</span><span class="sxs-lookup"><span data-stu-id="2cf91-157">Hub discovery events</span></span> |

<a id="server_text"></a>
### <a name="logging-server-events-to-text-files"></a><span data-ttu-id="2cf91-158">텍스트 파일에 서버 이벤트 로깅</span><span class="sxs-lookup"><span data-stu-id="2cf91-158">Logging server events to text files</span></span>

<span data-ttu-id="2cf91-159">다음 코드에서는 각 이벤트 범주에 대해 추적을 사용 하도록 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-159">The following code shows how to enable tracing for each category of event.</span></span> <span data-ttu-id="2cf91-160">이 샘플에서는 텍스트 파일에 이벤트를 기록 하도록 응용 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-160">This sample configures the application to log events to text files.</span></span>

<span data-ttu-id="2cf91-161">**추적 사용을 위한 XML 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="2cf91-161">**XML server code for enabling tracing**</span></span>

[!code-html[Main](enabling-signalr-tracing/samples/sample1.html)]

<span data-ttu-id="2cf91-162">위의 코드에서 `SignalRSwitch` 항목은 지정 된 로그로 전송 된 이벤트에 사용 되는 [TraceLevel](https://msdn.microsoft.com/library/system.diagnostics.tracelevel(v=vs.110).aspx) 를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-162">In the code above, the `SignalRSwitch` entry specifies the [TraceLevel](https://msdn.microsoft.com/library/system.diagnostics.tracelevel(v=vs.110).aspx) used for events sent to the specified log.</span></span> <span data-ttu-id="2cf91-163">이 경우 모든 디버깅 및 추적 메시지가 기록 됨을 의미 하는 `Verbose`로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-163">In this case, it is set to `Verbose` which means all debugging and tracing messages are logged.</span></span>

<span data-ttu-id="2cf91-164">다음 출력은 위의 구성 파일을 사용 하는 응용 프로그램에 대 한 `transports.log.txt` 파일의 항목을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-164">The following output shows entries from the `transports.log.txt` file for an application using the above configuration file.</span></span> <span data-ttu-id="2cf91-165">새 연결, 제거 된 연결 및 전송 하트 비트 이벤트를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-165">It shows a new connection, a removed connection, and transport heartbeat events.</span></span>

[!code-console[Main](enabling-signalr-tracing/samples/sample2.cmd)]

<a id="server_eventlog"></a>
### <a name="logging-server-events-to-the-event-log"></a><span data-ttu-id="2cf91-166">이벤트 로그에 서버 이벤트 로깅</span><span class="sxs-lookup"><span data-stu-id="2cf91-166">Logging server events to the event log</span></span>

<span data-ttu-id="2cf91-167">텍스트 파일이 아닌 이벤트 로그에 이벤트를 기록 하려면 `sharedListeners` 노드의 항목에 대 한 값을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-167">To log events to the event log rather than a text file, change the values for the entries in the `sharedListeners` node.</span></span> <span data-ttu-id="2cf91-168">다음 코드에서는 이벤트 로그에 서버 이벤트를 기록 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-168">The following code shows how to log server events to the event log:</span></span>

<span data-ttu-id="2cf91-169">**이벤트 로그에 이벤트를 기록 하기 위한 XML 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="2cf91-169">**XML server code for logging events to the event log**</span></span>

[!code-xml[Main](enabling-signalr-tracing/samples/sample3.xml)]

<span data-ttu-id="2cf91-170">이벤트는 응용 프로그램 로그에 기록 되 고 아래와 같이 이벤트 뷰어를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-170">The events are logged in the Application log, and are available through the Event Viewer, as shown below:</span></span>

![SignalR 로그를 보여 주는 이벤트 뷰어](enabling-signalr-tracing/_static/image1.png)

> [!NOTE]
> <span data-ttu-id="2cf91-172">이벤트 로그를 사용 하는 경우 **TraceLevel** 를 **Error** 로 설정 하 여 메시지 수를 관리 가능 하 게 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-172">When using the event log, set the **TraceLevel** to **Error** to keep the number of messages manageable.</span></span>

<a id="net_client"></a>
## <a name="enabling-tracing-in-the-net-client-windows-desktop-apps"></a><span data-ttu-id="2cf91-173">.NET 클라이언트에서 추적 사용 (Windows 데스크톱 응용 프로그램)</span><span class="sxs-lookup"><span data-stu-id="2cf91-173">Enabling tracing in the .NET client (Windows Desktop apps)</span></span>

<span data-ttu-id="2cf91-174">.NET 클라이언트는 [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx)의 구현을 사용 하 여 콘솔, 텍스트 파일 또는 사용자 지정 로그에 이벤트를 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-174">The .NET client can log events to the console, a text file, or to a custom log using an implementation of [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx).</span></span>

<span data-ttu-id="2cf91-175">.NET 클라이언트에서 로깅을 사용 하도록 설정 하려면 연결의 `TraceLevel` 속성을 [TraceLevels](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.tracelevels(v=vs.118).aspx) 값으로 설정 하 고 `TraceWriter` 속성을 올바른 [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) 인스턴스로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-175">To enable logging in the .NET client, set the connection's `TraceLevel` property to a [TraceLevels](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.tracelevels(v=vs.118).aspx) value, and the `TraceWriter` property to a valid [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) instance.</span></span>

<a id="desktop_console"></a>
### <a name="logging-desktop-client-events-to-the-console"></a><span data-ttu-id="2cf91-176">데스크톱 클라이언트 이벤트를 콘솔에 기록</span><span class="sxs-lookup"><span data-stu-id="2cf91-176">Logging Desktop client events to the console</span></span>

<span data-ttu-id="2cf91-177">다음 C# 코드에서는 .net 클라이언트의 이벤트를 콘솔에 기록 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-177">The following C# code shows how to log events in the .NET client to the console:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample4.cs?highlight=2-3)]

<a id="desktop_text"></a>
### <a name="logging-desktop-client-events-to-a-text-file"></a><span data-ttu-id="2cf91-178">텍스트 파일에 데스크톱 클라이언트 이벤트 로깅</span><span class="sxs-lookup"><span data-stu-id="2cf91-178">Logging Desktop client events to a text file</span></span>

<span data-ttu-id="2cf91-179">다음 C# 코드에서는 .net 클라이언트의 이벤트를 텍스트 파일에 기록 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-179">The following C# code shows how to log events in the .NET client to a text file:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample5.cs?highlight=4-5)]

<span data-ttu-id="2cf91-180">다음 출력은 위의 구성 파일을 사용 하는 응용 프로그램에 대 한 `ClientLog.txt` 파일의 항목을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-180">The following output shows entries from the `ClientLog.txt` file for an application using the above configuration file.</span></span> <span data-ttu-id="2cf91-181">서버에 연결 하는 클라이언트와 `addMessage`이라는 클라이언트 메서드를 호출 하는 허브를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-181">It shows the client connecting to the server, and the hub invoking a client method called `addMessage`:</span></span>

[!code-console[Main](enabling-signalr-tracing/samples/sample6.cmd)]

<a id="phone"></a>
## <a name="enabling-tracing-in-windows-phone-8-clients"></a><span data-ttu-id="2cf91-182">Windows Phone 8 클라이언트에서 추적 사용</span><span class="sxs-lookup"><span data-stu-id="2cf91-182">Enabling tracing in Windows Phone 8 clients</span></span>

<span data-ttu-id="2cf91-183">Windows Phone apps 용 SignalR 응용 프로그램은 데스크톱 앱과 동일한 .NET 클라이언트를 사용 하지만 [콘솔](https://msdn.microsoft.com/library/system.console.out(v=vs.110).aspx) 을 사용 하 고 [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) 를 사용 하 여 파일에 쓰는 것은 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-183">SignalR applications for Windows Phone apps use the same .NET client as desktop apps, but [Console.Out](https://msdn.microsoft.com/library/system.console.out(v=vs.110).aspx) and writing to a file with [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) are not available.</span></span> <span data-ttu-id="2cf91-184">대신, 추적을 위해 [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) 의 사용자 지정 구현을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-184">Instead, you need to create a custom implementation of [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) for tracing.</span></span>

<a id="phone_ui"></a>
### <a name="logging-windows-phone-client-events-to-the-ui"></a><span data-ttu-id="2cf91-185">UI에 Windows Phone 클라이언트 이벤트 로깅</span><span class="sxs-lookup"><span data-stu-id="2cf91-185">Logging Windows Phone client events to the UI</span></span>

<span data-ttu-id="2cf91-186">[SignalR 코드 베이스](https://github.com/SignalR/SignalR/archive/master.zip) 에는 `TextBlockWriter`이라는 사용자 지정 [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) 구현을 사용 하 여 [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) 에 추적 출력을 기록 하는 Windows Phone 샘플이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-186">The [SignalR codebase](https://github.com/SignalR/SignalR/archive/master.zip) includes a Windows Phone sample that writes trace output to a [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) using a custom [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) implementation called `TextBlockWriter`.</span></span> <span data-ttu-id="2cf91-187">이 클래스는 **samples/SignalR. WP8** 프로젝트에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-187">This class can be found in the **samples/Microsoft.AspNet.SignalR.Client.WP8.Samples** project.</span></span> <span data-ttu-id="2cf91-188">`TextBlockWriter`인스턴스를 만들 때 현재 [SynchronizationContext](https://msdn.microsoft.com/library/system.threading.synchronizationcontext(v=vs.110).aspx)를 전달 하 고 추적 출력에 사용할 [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) 을 만들 [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) 을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-188">When creating an instance of `TextBlockWriter`, pass in the current [SynchronizationContext](https://msdn.microsoft.com/library/system.threading.synchronizationcontext(v=vs.110).aspx), and a [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) where it will create a [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) to use for trace output:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample7.cs)]

<span data-ttu-id="2cf91-189">그러면 전달 된 [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) 에서 만든 새 [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) 에 추적 출력이 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-189">The trace output will then be written to a new [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) created in the [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) you passed in:</span></span>

![](enabling-signalr-tracing/_static/image2.png)

<a id="phone_debug"></a>
### <a name="logging-windows-phone-client-events-to-the-debug-console"></a><span data-ttu-id="2cf91-190">디버그 콘솔에 Windows Phone 클라이언트 이벤트 로깅</span><span class="sxs-lookup"><span data-stu-id="2cf91-190">Logging Windows Phone client events to the debug console</span></span>

<span data-ttu-id="2cf91-191">출력을 UI 대신 디버그 콘솔로 보내려면 디버그 창에 쓰는 [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) 의 구현을 만들고 연결의 [tracewriter](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connection.tracewriter(v=vs.118).aspx) 속성에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-191">To send output to the debug console rather than the UI, create an implementation of [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) that writes to the debug window, and assign it to your connection's [TraceWriter](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connection.tracewriter(v=vs.118).aspx) property:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample8.cs)]

<span data-ttu-id="2cf91-192">그러면 Visual Studio의 디버그 창에 추적 정보가 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-192">Trace information will then be written to the debug window in Visual Studio:</span></span>

![](enabling-signalr-tracing/_static/image3.png)

<a id="javascript"></a>
## <a name="enabling-tracing-in-the-javascript-client"></a><span data-ttu-id="2cf91-193">JavaScript 클라이언트에서 추적 사용</span><span class="sxs-lookup"><span data-stu-id="2cf91-193">Enabling tracing in the JavaScript client</span></span>

<span data-ttu-id="2cf91-194">연결에 대 한 클라이언트 쪽 로깅을 사용 하도록 설정 하려면 연결 개체에 대 한 `logging` 속성을 설정 하 여 연결을 설정 하기 전에 `start` 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-194">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="2cf91-195">**생성 된 프록시를 사용 하 여 브라우저 콘솔에 추적을 사용 하도록 설정 하는 클라이언트 JavaScript 코드**</span><span class="sxs-lookup"><span data-stu-id="2cf91-195">**Client JavaScript code for enabling tracing to the browser console (with the generated proxy)**</span></span>

[!code-javascript[Main](enabling-signalr-tracing/samples/sample9.js?highlight=1)]

<span data-ttu-id="2cf91-196">**브라우저 콘솔에 대 한 추적을 사용 하도록 설정 하는 클라이언트 JavaScript 코드 (생성 된 프록시 제외)**</span><span class="sxs-lookup"><span data-stu-id="2cf91-196">**Client JavaScript code for enabling tracing to the browser console (without the generated proxy)**</span></span>

[!code-javascript[Main](enabling-signalr-tracing/samples/sample10.js?highlight=2)]

<span data-ttu-id="2cf91-197">추적을 사용 하는 경우 JavaScript 클라이언트는 브라우저 콘솔에 이벤트를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-197">When tracing is enabled, the JavaScript client logs events to the browser console.</span></span> <span data-ttu-id="2cf91-198">브라우저 콘솔에 액세스 하려면 [전송 모니터링](../getting-started/introduction-to-signalr.md#MonitoringTransports)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="2cf91-198">To access the browser console, see [Monitoring Transports](../getting-started/introduction-to-signalr.md#MonitoringTransports).</span></span>

<span data-ttu-id="2cf91-199">다음 스크린샷에서는 추적을 사용 하는 SignalR JavaScript 클라이언트를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-199">The following screenshot shows a SignalR JavaScript client with tracing enabled.</span></span> <span data-ttu-id="2cf91-200">브라우저 콘솔에 연결 및 허브 호출 이벤트를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cf91-200">It shows connection and hub invocation events in the browser console:</span></span>

![브라우저 콘솔의 SignalR 추적 이벤트](enabling-signalr-tracing/_static/image4.png)
