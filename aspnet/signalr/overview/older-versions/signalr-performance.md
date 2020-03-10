---
uid: signalr/overview/older-versions/signalr-performance
title: SignalR 성능 (SignalR 1.x) | Microsoft Docs
author: bradygaster
description: SignalR 성능
ms.author: bradyg
ms.date: 07/03/2013
ms.assetid: 9594d644-66b6-4223-acdd-23e29a6e4c46
msc.legacyurl: /signalr/overview/older-versions/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: 915fd822caae9bbcb0a688c6dd7a5b2bda12c9df
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468107"
---
# <a name="signalr-performance-signalr-1x"></a>SignalR 성능(SignalR 1.x)

[Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 항목에서는 SignalR 응용 프로그램의 성능을 설계, 측정 및 개선 하는 방법에 대해 설명 합니다.

SignalR 성능 및 크기 조정에 대 한 최근 프레젠테이션은 [ASP.NET SignalR를 사용 하 여 실시간 웹 크기 조정](https://channel9.msdn.com/Events/Build/2013/3-502)을 참조 하세요.

이 항목에는 다음과 같은 섹션이 포함되어 있습니다.

- [디자인 고려 사항](#design)
- [성능을 위해 SignalR 서버 튜닝](#tuning)
- [성능 문제 해결](#troubleshooting)
- [SignalR 성능 카운터 사용](#perfcounters)
- [다른 성능 카운터 사용](#othercounters)
- [기타 참고 자료](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a>디자인 고려 사항

이 섹션에서는 SignalR 응용 프로그램을 디자인 하는 동안 구현할 수 있는 패턴을 설명 하 여 불필요 한 네트워크 트래픽을 생성 하 여 성능이 저하 되지 않도록 합니다.

### <a name="throttling-message-frequency"></a>메시지 빈도 조정

실시간 게임 응용 프로그램과 같은 높은 빈도로 메시지를 전송 하는 응용 프로그램 에서도 대부분의 응용 프로그램은 몇 초 이상의 메시지를 보낼 필요가 없습니다. 각 클라이언트에서 생성 하는 트래픽 양을 줄이기 위해 메시지 루프를 구현 하 여 고정 된 속도 보다 더 자주 메시지를 전송 하지 않습니다. 즉, 해당 시간에 메시지가 있는 경우 몇 초 마다 전송 됩니다. 전송 될 terval). 클라이언트와 서버 모두에서 메시지를 특정 속도로 제한 하는 예제 응용 프로그램은 SignalR를 사용 하는 [빈도가 높은 실시간](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)을 참조 하세요.

### <a name="reducing-message-size"></a>메시지 크기 줄이기

Serialize 된 개체의 크기를 줄여 SignalR 메시지의 크기를 줄일 수 있습니다. 서버 코드에서 전송 하지 않아도 되는 속성을 포함 하는 개체를 전송 하는 경우 `JsonIgnore` 특성을 사용 하 여 이러한 속성이 serialize 되지 않도록 합니다. 속성의 이름도 메시지에 저장 됩니다. `JsonProperty` 특성을 사용 하 여 속성의 이름을 줄일 수 있습니다. 다음 코드 샘플에서는 클라이언트에 전송 되는 속성을 제외 하는 방법과 속성 이름을 단축 하는 방법을 보여 줍니다.

**클라이언트에 전송 되는 데이터를 제외 하는 JsonIgnore 특성을 보여 주는 .NET server 코드와 메시지 크기를 줄이기 위해 Jsonpropery 특성**

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

클라이언트 코드에서 가독성/유지 관리를 유지 하기 위해 메시지를 받은 후 축약 된 속성 이름을 사용자에 게 친숙 한 이름으로 다시 매핑할 수 있습니다. 다음 코드 샘플에서는 메시지 계약 (매핑)을 정의 하 고 `reMap` 함수를 사용 하 여 최적화 된 메시지 클래스에 계약을 적용 하는 방법을 보여 줍니다.

**사용자가 읽을 수 있는 이름에 축약 된 속성 이름을 다시 매핑하는 클라이언트 쪽 JavaScript 코드**

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

동일한 방법을 사용 하 여 클라이언트에서 서버로의 메시지 에서도 이름을 줄일 수 있습니다.

메시지 개체의 메모리 공간 (즉, 메시지에 사용 되는 메모리 양)을 줄이면 성능도 향상 될 수 있습니다. 예를 들어 `int`의 전체 범위가 필요 하지 않은 경우 `short` 또는 `byte`를 대신 사용할 수 있습니다.

메시지는 서버 메모리의 메시지 버스에 저장 되므로 메시지 크기를 줄이면 서버 메모리 문제를 해결할 수도 있습니다.

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a>성능을 위해 SignalR 서버 튜닝

다음 구성 설정을 사용 하 여 SignalR 응용 프로그램의 성능을 향상 시키기 위해 서버를 튜닝할 수 있습니다. ASP.NET 응용 프로그램의 성능을 향상 시키는 방법에 대 한 일반적인 내용은 [ASP.NET 성능 향상](https://msdn.microsoft.com/library/ff647787.aspx)을 참조 하세요.

**SignalR 구성 설정**

- **Defaultmessagebuffersize**: 기본적으로 SignalR는 연결 당 허브 당 1000 메시지를 메모리에 보관 합니다. 많은 메시지를 사용 하는 경우이 값을 줄이면 메모리 문제가 발생할 수 있습니다. 이 설정은 ASP.NET 응용 프로그램의 `Application_Start` 이벤트 처리기 또는 자체 호스팅 응용 프로그램에서 OWIN startup 클래스의 `Configuration` 메서드에서 설정할 수 있습니다. 다음 샘플에서는 사용 되는 서버 메모리 양을 줄이기 위해 응용 프로그램의 메모리 사용 공간을 줄이기 위해이 값을 줄이는 방법을 보여 줍니다.

    **기본 메시지 버퍼 크기를 줄이기 위한 Global.asax의 .NET 서버 코드**

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

**IIS 구성 설정**

- **응용 프로그램당 최대 동시 요청**수: 동시 IIS 요청 수를 늘리면 요청을 처리 하는 데 사용할 수 있는 서버 리소스가 늘어납니다. 기본값은 5000입니다. 이 설정을 늘리려면 관리자 권한 명령 프롬프트에서 다음 명령을 실행 합니다.

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]

**ASP.NET 구성 설정**

이 섹션에는 `aspnet.config` 파일에서 설정할 수 있는 구성 설정이 포함 되어 있습니다. 이 파일은 플랫폼에 따라 다음 두 위치 중 하나에 있습니다.

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

SignalR 성능을 향상 시킬 수 있는 ASP.NET 설정에는 다음이 포함 됩니다.

- **CPU 당 최대 동시 요청**수:이 설정을 높이면 성능 병목 현상이 발생할 수 있습니다. 이 설정을 늘리려면 `aspnet.config` 파일에 다음 구성 설정을 추가 합니다.

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- **요청 큐 제한**: 연결의 총 수가 `maxConcurrentRequestsPerCPU` 설정을 초과 하는 경우 ASP.NET는 큐를 사용 하 여 요청을 조정 하기 시작 합니다. 큐 크기를 늘리려면 `requestQueueLimit` 설정을 늘릴 수 있습니다. 이렇게 하려면 `aspnet.config`아닌 `config/machine.config`의 `processModel` 노드에 다음 구성 설정을 추가 합니다.

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a>성능 문제 해결

이 섹션에서는 응용 프로그램에서 성능 병목 지점을 찾는 방법에 대해 설명 합니다.

### <a name="verifying-that-websocket-is-being-used"></a>WebSocket이 사용 되 고 있는지 확인 하는 중

SignalR는 클라이언트와 서버 간의 통신에 다양 한 전송을 사용할 수 있는 반면 WebSocket은 상당한 성능상의 이점을 제공 하며 클라이언트와 서버에서 지 원하는 경우 사용 해야 합니다. 클라이언트와 서버가 WebSocket에 대 한 요구 사항을 충족 하는지 확인 하려면 [전송 및 대체](../getting-started/introduction-to-signalr.md#transports)를 참조 하세요. 응용 프로그램에서 사용 되는 전송을 확인 하기 위해 브라우저 개발자 도구를 사용 하 고 로그를 검토 하 여 연결에 사용 되는 전송을 확인할 수 있습니다. Internet Explorer 및 Chrome에서 브라우저 개발 도구를 사용 하는 방법에 대 한 자세한 내용은 [전송 및 대체](../getting-started/introduction-to-signalr.md#transports)를 참조 하세요.

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a>SignalR 성능 카운터 사용

이 섹션에서는 `Microsoft.AspNet.SignalR.Utils` 패키지에 있는 SignalR 성능 카운터를 사용 하도록 설정 하 고 사용 하는 방법을 설명 합니다.

### <a name="installing-signalrexe"></a>Signalr를 설치 하는 중

SignalR 이라는 유틸리티를 사용 하 여 성능 카운터를 서버에 추가할 수 있습니다. 이 유틸리티를 설치 하려면 다음 단계를 수행 합니다.

1. Visual Studio에서 **도구** > **nuget 패키지 관리자** > **솔루션에 대 한 nuget 패키지 관리** 를 선택 합니다.
2. **Signalr. 유틸리티**를 검색 하 고 설치를 선택 합니다.

    ![](signalr-performance/_static/image1.png)
3. 사용권 계약에 동의 하 여 패키지를 설치 합니다.
4. SignalR가 `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`에 설치 됩니다.

### <a name="installing-performance-counters-with-signalrexe"></a>SignalR를 사용 하 여 성능 카운터 설치

SignalR 성능 카운터를 설치 하려면 다음 매개 변수를 사용 하 여 관리자 권한 명령 프롬프트에서 SignalR를 실행 합니다.

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

SignalR 성능 카운터를 제거 하려면 다음 매개 변수를 사용 하 여 관리자 권한 명령 프롬프트에서 SignalR를 실행 합니다.

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a>SignalR 성능 카운터

유틸리티 패키지는 다음 성능 카운터를 설치 합니다. "Total" 카운터는 마지막 응용 프로그램 풀 또는 서버 다시 시작 이후의 이벤트 수를 측정 합니다.

**연결 메트릭**

다음 메트릭은 발생 하는 연결 수명 이벤트를 측정 합니다. 자세한 내용은 [연결 수명 이벤트 이해 및 처리](../guide-to-the-api/handling-connection-lifetime-events.md)를 참조 하세요.

- **연결 된 연결**
- **연결이 다시 연결 되었습니다.**
- **연결 끊김**
- **현재 연결**

**메시지 메트릭**

다음 메트릭은 SignalR에서 생성 된 메시지 트래픽을 측정 합니다.

- **총 받은 연결 메시지**
- **총 보낸 연결 메시지**
- **받은 연결 메시지/초**
- **전송 되는 연결 메시지/초**

**메시지 버스 메트릭**

다음 메트릭은 내부 SignalR 메시지 버스, 들어오고 나가는 모든 SignalR 메시지가 배치 되는 큐를 통해 트래픽을 측정 합니다. 메시지는 보내거나 브로드캐스트할 때 **게시** 됩니다. 이 컨텍스트의 **구독자** 는 메시지 버스에 대 한 구독입니다. 이는 클라이언트 수와 서버 자체의 수와 같아야 합니다. **할당 된 작업자** 는 활성 연결에 데이터를 전송 하는 구성 요소입니다. **사용 중인 작업자** 는 메시지를 전송 하는 작업자입니다.

- **메시지 버스 총 수신 메시지**
- **메시지 버스 받은 메시지/초**
- **메시지 버스 총 게시 된 메시지**
- **게시 된 메시지 버스 메시지/초**
- **메시지 버스 구독자 최신**
- **메시지 버스 구독자 합계**
- **메시지 버스 구독자/초**
- **메시지 버스 할당 된 작업자**
- **메시지 버스 작업 중인 작업자**
- **메시지 버스 항목 현재**

**오류 메트릭**

다음 메트릭은 SignalR 메시지 트래픽에 의해 생성 된 오류를 측정 합니다. 허브 **확인** 오류는 허브 또는 허브 메서드를 확인할 수 없을 때 발생 합니다. 허브 **호출** 오류는 허브 메서드를 호출 하는 동안 throw 되는 예외입니다. **전송** 오류는 HTTP 요청 또는 응답 중에 throw 된 연결 오류입니다.

- **오류: 전체**
- **오류: 모두/초**
- **오류: 총 허브 해상도**
- **오류: 허브 확인/초**
- **오류: 총 허브 호출**
- **오류: 허브 호출/초**
- **오류: 총 전송**
- **오류: Transport/Sec**

**확장 메트릭**

다음 메트릭은 확장 공급자에 의해 생성 된 트래픽 및 오류를 측정 합니다. 이 컨텍스트의 **스트림은** 확장 공급자에서 사용 되는 배율 단위입니다. 이는 SQL Server 사용 되는 경우 테이블이 고 Service Bus 사용 되는 경우 토픽 이며 Redis가 사용 되는 경우 구독입니다. 기본적으로 하나의 스트림만 사용 되지만 SQL Server 및 Service Bus에 대 한 구성을 통해이를 늘릴 수 있습니다. **버퍼링** 스트림은 오류가 발생 한 상태로 입력 된 스트림입니다. 스트림이 오류가 발생 한 경우에는 스트림이 더 이상 오류가 발생 하지 않을 때까지 후면판에 전송 된 모든 메시지가 즉시 실패 합니다. **송신 큐 길이** 는 게시 되었지만 아직 보내지 않은 메시지 수입니다.

- **확장 메시지 버스 수신 메시지/초**
- **총 확장 스트림**
- **확장 스트림 열기**
- **확장 스트림 버퍼링**
- **총 확장 오류**
- **확장 오류/초**
- **확장 송신 큐 길이**

이러한 카운터를 측정 하는 방법에 대 한 자세한 내용은 [SignalR 확장 with Azure Service Bus](scaleout-with-windows-azure-service-bus.md)를 참조 하세요.

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a>다른 성능 카운터 사용

다음 성능 카운터는 응용 프로그램의 성능을 모니터링 하는 데 유용할 수도 있습니다.

**메모리**

- .NET CLR 메모리 # 모든 힙의 바이트 수 (w3wp.exe의 경우)

**ASP.NET**

- ASP.NET\Requests Current
- ASP.NET\Queued
- ASP.NET\Rejected

**CPU**

- 프로세서 Information\Processor Time

**TCP/IP**

- TCPv6/연결 설정
- TCPv4/연결 설정

**웹 서비스**

- 웹 서비스 \ 현재 연결
- 웹 서비스 \ 최대 연결

**스레딩**

- 현재 논리 스레드의 .NET CLR LocksAndThreads\#
- 현재 실제 스레드\# .NET CLR LocksAnd 스레드

<a id="otherresources"></a>

## <a name="other-resources"></a>관련 자료

ASP.NET 성능 모니터링 및 튜닝에 대 한 자세한 내용은 다음 항목을 참조 하세요.

- [ASP.NET 성능 개요](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)
- [IIS 7.5, IIS 7.0 및 IIS 6.0의 ASP.NET 스레드 사용](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [&lt;applicationPool&gt; 요소 (웹 설정)](https://msdn.microsoft.com/library/dd560842.aspx)
