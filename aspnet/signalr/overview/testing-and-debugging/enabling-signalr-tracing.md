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
# <a name="enabling-signalr-tracing"></a>SignalR 추적 사용

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 문서에서는 SignalR 서버 및 클라이언트에 대 한 추적을 사용 하도록 설정 하 고 구성 하는 방법을 설명 합니다. 추적을 사용 하면 SignalR 응용 프로그램에서 이벤트에 대 한 진단 정보를 볼 수 있습니다.
>
> 이 항목은 원래 Patrick Fletcher에 의해 작성 되었습니다.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET Framework 4.5
> - SignalR 버전 2
>
>
>
> ## <a name="questions-and-comments"></a>질문 및 설명
>
> 이 자습서와 페이지 맨 아래에 있는 의견에서 개선할 수 있는 방법에 대 한 의견을 남겨 주세요. 자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)에 게시할 수 있습니다.

추적을 사용 하는 경우 SignalR 응용 프로그램에서 이벤트에 대 한 로그 항목을 만듭니다. 클라이언트와 서버 모두에서 이벤트를 기록할 수 있습니다. 서버에 대 한 추적은 연결, 확장 공급자 및 메시지 버스 이벤트를 로깅합니다. 클라이언트의 추적은 연결 이벤트를 기록 합니다. SignalR 2.1 이상에서 클라이언트에 대 한 추적은 허브 호출 메시지의 전체 콘텐츠를 기록 합니다.

## <a name="contents"></a>콘텐츠

- [서버에서 추적 사용](#server)

    - [텍스트 파일에 서버 이벤트 로깅](#server_text)
    - [이벤트 로그에 서버 이벤트 로깅](#server_eventlog)
- [.NET 클라이언트에서 추적 사용 (Windows 데스크톱 응용 프로그램)](#net_client)

    - [데스크톱 클라이언트 이벤트를 콘솔에 기록](#desktop_console)
    - [텍스트 파일에 데스크톱 클라이언트 이벤트 로깅](#desktop_text)
- [Windows Phone 8 클라이언트에서 추적 사용](#phone)

    - [UI에 Windows Phone 클라이언트 이벤트 로깅](#phone_ui)
    - [디버그 콘솔에 Windows Phone 클라이언트 이벤트 로깅](#phone_debug)
- [JavaScript 클라이언트에서 추적 사용](#javascript)

<a id="server"></a>
## <a name="enabling-tracing-on-the-server"></a>서버에서 추적 사용

응용 프로그램의 구성 파일 (프로젝트의 형식에 따라 app.config 또는 web.config) 내의 서버에서 추적을 사용 하도록 설정 합니다. 로깅할 이벤트 범주를 지정 합니다. 구성 파일에서 [TraceListener](https://msdn.microsoft.com/library/system.diagnostics.tracelistener(v=vs.110).aspx)의 구현을 사용 하 여 텍스트 파일, Windows 이벤트 로그 또는 사용자 지정 로그에 이벤트를 기록할지 여부도 지정 합니다.

서버 이벤트 범주는 다음과 같은 종류의 메시지를 포함 합니다.

| 원본 | 메시지 |
| --- | --- |
| SignalR.SqlMessageBus | SQL 메시지 버스 확장 공급자 설치, 데이터베이스 작업, 오류 및 시간 제한 이벤트 |
| SignalR.ServiceBusMessageBus | Service bus 확장 공급자 토픽 만들기 및 구독, 오류 및 메시징 이벤트 |
| SignalR.RedisMessageBus | Redis 확장 공급자 연결, 연결 끊기 및 오류 이벤트 |
| SignalR.ScaleoutMessageBus | 확장 messaging 이벤트 |
| SignalR.Transports.WebSocketTransport | WebSocket 전송 연결, 연결 끊기, 메시징 및 오류 이벤트 |
| SignalR.Transports.ServerSentEventsTransport | ServerSentEvents 전송 연결, 연결 끊기, 메시징 및 오류 이벤트 |
| SignalR.Transports.ForeverFrameTransport | ForeverFrame 전송 연결, 연결 끊기, 메시징 및 오류 이벤트 |
| SignalR.Transports.LongPollingTransport | 이상 폴링 전송 연결, 연결 끊기, 메시징 및 오류 이벤트 |
| SignalR.Transports.TransportHeartBeat | 전송 연결, 연결 끊기 및 keepalive 이벤트 |
| SignalR.ReflectedHubDescriptorProvider | 허브 검색 이벤트 |

<a id="server_text"></a>
### <a name="logging-server-events-to-text-files"></a>텍스트 파일에 서버 이벤트 로깅

다음 코드에서는 각 이벤트 범주에 대해 추적을 사용 하도록 설정 하는 방법을 보여 줍니다. 이 샘플에서는 텍스트 파일에 이벤트를 기록 하도록 응용 프로그램을 구성 합니다.

**추적 사용을 위한 XML 서버 코드**

[!code-html[Main](enabling-signalr-tracing/samples/sample1.html)]

위의 코드에서 `SignalRSwitch` 항목은 지정 된 로그로 전송 된 이벤트에 사용 되는 [TraceLevel](https://msdn.microsoft.com/library/system.diagnostics.tracelevel(v=vs.110).aspx) 를 지정 합니다. 이 경우 모든 디버깅 및 추적 메시지가 기록 됨을 의미 하는 `Verbose`로 설정 됩니다.

다음 출력은 위의 구성 파일을 사용 하는 응용 프로그램에 대 한 `transports.log.txt` 파일의 항목을 보여 줍니다. 새 연결, 제거 된 연결 및 전송 하트 비트 이벤트를 표시 합니다.

[!code-console[Main](enabling-signalr-tracing/samples/sample2.cmd)]

<a id="server_eventlog"></a>
### <a name="logging-server-events-to-the-event-log"></a>이벤트 로그에 서버 이벤트 로깅

텍스트 파일이 아닌 이벤트 로그에 이벤트를 기록 하려면 `sharedListeners` 노드의 항목에 대 한 값을 변경 합니다. 다음 코드에서는 이벤트 로그에 서버 이벤트를 기록 하는 방법을 보여 줍니다.

**이벤트 로그에 이벤트를 기록 하기 위한 XML 서버 코드**

[!code-xml[Main](enabling-signalr-tracing/samples/sample3.xml)]

이벤트는 응용 프로그램 로그에 기록 되 고 아래와 같이 이벤트 뷰어를 통해 사용할 수 있습니다.

![SignalR 로그를 보여 주는 이벤트 뷰어](enabling-signalr-tracing/_static/image1.png)

> [!NOTE]
> 이벤트 로그를 사용 하는 경우 **TraceLevel** 를 **Error** 로 설정 하 여 메시지 수를 관리 가능 하 게 유지 합니다.

<a id="net_client"></a>
## <a name="enabling-tracing-in-the-net-client-windows-desktop-apps"></a>.NET 클라이언트에서 추적 사용 (Windows 데스크톱 응용 프로그램)

.NET 클라이언트는 [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx)의 구현을 사용 하 여 콘솔, 텍스트 파일 또는 사용자 지정 로그에 이벤트를 기록할 수 있습니다.

.NET 클라이언트에서 로깅을 사용 하도록 설정 하려면 연결의 `TraceLevel` 속성을 [TraceLevels](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.tracelevels(v=vs.118).aspx) 값으로 설정 하 고 `TraceWriter` 속성을 올바른 [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) 인스턴스로 설정 합니다.

<a id="desktop_console"></a>
### <a name="logging-desktop-client-events-to-the-console"></a>데스크톱 클라이언트 이벤트를 콘솔에 기록

다음 C# 코드에서는 .net 클라이언트의 이벤트를 콘솔에 기록 하는 방법을 보여 줍니다.

[!code-csharp[Main](enabling-signalr-tracing/samples/sample4.cs?highlight=2-3)]

<a id="desktop_text"></a>
### <a name="logging-desktop-client-events-to-a-text-file"></a>텍스트 파일에 데스크톱 클라이언트 이벤트 로깅

다음 C# 코드에서는 .net 클라이언트의 이벤트를 텍스트 파일에 기록 하는 방법을 보여 줍니다.

[!code-csharp[Main](enabling-signalr-tracing/samples/sample5.cs?highlight=4-5)]

다음 출력은 위의 구성 파일을 사용 하는 응용 프로그램에 대 한 `ClientLog.txt` 파일의 항목을 보여 줍니다. 서버에 연결 하는 클라이언트와 `addMessage`이라는 클라이언트 메서드를 호출 하는 허브를 표시 합니다.

[!code-console[Main](enabling-signalr-tracing/samples/sample6.cmd)]

<a id="phone"></a>
## <a name="enabling-tracing-in-windows-phone-8-clients"></a>Windows Phone 8 클라이언트에서 추적 사용

Windows Phone apps 용 SignalR 응용 프로그램은 데스크톱 앱과 동일한 .NET 클라이언트를 사용 하지만 [콘솔](https://msdn.microsoft.com/library/system.console.out(v=vs.110).aspx) 을 사용 하 고 [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) 를 사용 하 여 파일에 쓰는 것은 사용할 수 없습니다. 대신, 추적을 위해 [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) 의 사용자 지정 구현을 만들어야 합니다.

<a id="phone_ui"></a>
### <a name="logging-windows-phone-client-events-to-the-ui"></a>UI에 Windows Phone 클라이언트 이벤트 로깅

[SignalR 코드 베이스](https://github.com/SignalR/SignalR/archive/master.zip) 에는 `TextBlockWriter`이라는 사용자 지정 [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) 구현을 사용 하 여 [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) 에 추적 출력을 기록 하는 Windows Phone 샘플이 포함 되어 있습니다. 이 클래스는 **samples/SignalR. WP8** 프로젝트에서 찾을 수 있습니다. `TextBlockWriter`인스턴스를 만들 때 현재 [SynchronizationContext](https://msdn.microsoft.com/library/system.threading.synchronizationcontext(v=vs.110).aspx)를 전달 하 고 추적 출력에 사용할 [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) 을 만들 [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) 을 전달 합니다.

[!code-csharp[Main](enabling-signalr-tracing/samples/sample7.cs)]

그러면 전달 된 [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) 에서 만든 새 [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) 에 추적 출력이 기록 됩니다.

![](enabling-signalr-tracing/_static/image2.png)

<a id="phone_debug"></a>
### <a name="logging-windows-phone-client-events-to-the-debug-console"></a>디버그 콘솔에 Windows Phone 클라이언트 이벤트 로깅

출력을 UI 대신 디버그 콘솔로 보내려면 디버그 창에 쓰는 [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) 의 구현을 만들고 연결의 [tracewriter](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connection.tracewriter(v=vs.118).aspx) 속성에 할당 합니다.

[!code-csharp[Main](enabling-signalr-tracing/samples/sample8.cs)]

그러면 Visual Studio의 디버그 창에 추적 정보가 기록 됩니다.

![](enabling-signalr-tracing/_static/image3.png)

<a id="javascript"></a>
## <a name="enabling-tracing-in-the-javascript-client"></a>JavaScript 클라이언트에서 추적 사용

연결에 대 한 클라이언트 쪽 로깅을 사용 하도록 설정 하려면 연결 개체에 대 한 `logging` 속성을 설정 하 여 연결을 설정 하기 전에 `start` 메서드를 호출 합니다.

**생성 된 프록시를 사용 하 여 브라우저 콘솔에 추적을 사용 하도록 설정 하는 클라이언트 JavaScript 코드**

[!code-javascript[Main](enabling-signalr-tracing/samples/sample9.js?highlight=1)]

**브라우저 콘솔에 대 한 추적을 사용 하도록 설정 하는 클라이언트 JavaScript 코드 (생성 된 프록시 제외)**

[!code-javascript[Main](enabling-signalr-tracing/samples/sample10.js?highlight=2)]

추적을 사용 하는 경우 JavaScript 클라이언트는 브라우저 콘솔에 이벤트를 기록 합니다. 브라우저 콘솔에 액세스 하려면 [전송 모니터링](../getting-started/introduction-to-signalr.md#MonitoringTransports)을 참조 하세요.

다음 스크린샷에서는 추적을 사용 하는 SignalR JavaScript 클라이언트를 보여 줍니다. 브라우저 콘솔에 연결 및 허브 호출 이벤트를 표시 합니다.

![브라우저 콘솔의 SignalR 추적 이벤트](enabling-signalr-tracing/_static/image4.png)
