---
uid: signalr/overview/getting-started/supported-platforms
title: 지원 되는 플랫폼 | Microsoft Docs
author: bradygaster
description: 이 문서에서는 SignalR에서 지원 되는 클라이언트 및 서버에 대해 설명 합니다.
ms.author: bradyg
ms.date: 04/18/2018
ms.assetid: eac31beb-0f46-4afa-9def-e80904dea4f0
msc.legacyurl: /signalr/overview/getting-started/supported-platforms
msc.type: authoredcontent
ms.openlocfilehash: 89730e591bb94022d16fe1a78a4350b38e0bf7a4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450125"
---
# <a name="supported-platforms"></a>지원되는 플랫폼

[Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 문서에서는 SignalR에서 지원 되는 클라이언트 및 서버에 대해 설명 합니다. 
> 
> ## <a name="questions-and-comments"></a>질문 및 설명
> 
> 이 자습서와 페이지 맨 아래에 있는 의견에서 개선할 수 있는 방법에 대 한 의견을 남겨 주세요. 자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)에 게시할 수 있습니다.

SignalR는 다양 한 서버 및 클라이언트 구성에서 지원 됩니다. 또한 각 전송 옵션에는 자체 요구 사항 집합이 있습니다. 전송에 대 한 시스템 요구 사항을 사용할 수 없는 경우 SignalR는 다른 전송으로 정상적으로 장애 조치 (failover)를 수행할 수 있습니다. SignalR에서 지 원하는 전송에 대 한 자세한 내용은 [전송 및 대체](introduction-to-signalr.md#transports)를 참조 하세요.

## <a name="server-system-requirements"></a>서버 시스템 요구 사항

SignalR 서버 구성 요소는 다양 한 서버 구성에서 호스팅될 수 있습니다. 이 섹션에서는 지원 되는 운영 체제 버전, .NET framework, 인터넷 정보 서버 및 기타 구성 요소에 대해 설명 합니다.

### <a name="supported-server-operating-systems"></a>지원 되는 서버 운영 체제

SignalR 서버 구성 요소는 다음 서버 또는 클라이언트 운영 체제에서 호스팅될 수 있습니다. SignalR에서 Websocket을 사용 하려면 windows Server 2012, Windows Server 2016 또는 Windows 8이 필요 합니다. (WebSocket은 Windows Azure 웹 사이트에서 사용할 수 있습니다. 사이트의 .NET framework 버전이 4.5로 설정 되 고 사이트에서 웹 소켓이 사용 하도록 설정 된 경우) 구성 페이지).

- Windows Server 2016
- Windows Server 2012
- Windows Server 2008 r2
- 윈도우 10
- Windows 8
- Windows 7
- Windows Azure

### <a name="supported-server-net-framework-version"></a>지원 되는 서버 .NET Framework 버전

SignalR 2는 .NET Framework 4.5 에서만 지원 됩니다. 안정성, 호환성, 안정성 및 성능을 향상 시키는 업데이트는 [권장 업데이트](#updates) 섹션을 참조 하세요.

### <a name="supported-server-iis-versions"></a>지원 되는 서버 IIS 버전

SignalR가 IIS에서 호스팅되는 경우 지원 되는 버전은 다음과 같습니다. 개발 (Windows 8 또는 Windows 7) 등의 클라이언트 운영 체제를 사용 하는 경우에는 전체 버전의 IIS 또는 Cassini를 사용 하면 안 됩니다 .이 경우 연결 된 후에 매우 빠르게 도달할 수 있는 동시 연결 수가 10 개로 제한 되기 때문입니다. 일시적으로 다시 설정 되 고 더 이상 사용 되지 않을 때 즉시 삭제 되지 않습니다. IIS Express은 클라이언트 운영 체제에서 사용 해야 합니다.

또한 SignalR에서 WebSocket을 사용 하려면 IIS 8 또는 IIS 8 Express를 사용 하 고 서버에서 Windows 8, Windows Server 2012 이상을 사용 해야 하며 IIS에서 WebSocket을 사용 하도록 설정 해야 합니다. IIS에서 WebSocket을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 [iis 8.0 Websocket 프로토콜 지원](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support)을 참조 하세요.

- IIS 8 또는 IIS 8 Express
- IIS 7 및 7.5. [확장명 없는 url](https://support.microsoft.com/kb/980368) 에 대 한 지원이 필요 합니다.
- IIS는 통합 모드로 실행 해야 합니다. 클래식 모드는 지원 되지 않습니다. 서버에서 보낸 이벤트 전송을 사용 하 여 클래식 모드에서 IIS를 실행 하는 경우 최대 30 초의 메시지 지연이 발생할 수 있습니다.
- 호스팅 응용 프로그램은 완전 신뢰 모드로 실행 되어야 합니다.

## <a name="client-system-requirements"></a>클라이언트 시스템 요구 사항

SignalR는 다양 한 클라이언트 플랫폼에서 사용할 수 있습니다. 이 섹션에서는 웹 브라우저, Windows 데스크톱 응용 프로그램, Silverlight 응용 프로그램 및 모바일 장치에서 SignalR를 사용 하기 위한 시스템 요구 사항에 대해 설명 합니다.

### <a name="web-browsers"></a>웹 브라우저

SignalR는 다양 한 웹 브라우저에서 사용할 수 있지만 일반적으로 최신 두 버전만 지원 됩니다.

브라우저에서 SignalR를 사용 하는 응용 프로그램은 jQuery 버전 1.6.4 또는 최신 버전 (예: 1.7.2, 1.8.2 또는 1.9.1)을 사용 해야 합니다.

SignalR는 다음 브라우저에서 사용할 수 있습니다.

- Microsoft Internet Explorer 버전 8, 9, 10 및 11. 최신, 데스크톱 및 모바일 버전이 지원 됩니다.
- Mozilla Firefox: Windows 및 Mac 버전 모두 최신 버전-1.
- Google Chrome: Windows 및 Mac 버전의 최신 버전-1.
- Safari: 현재 버전-1, Mac 및 iOS 버전 모두.
- Opera: 현재 버전-1, Windows만 해당 합니다.
- Android 브라우저

특정 브라우저를 요구 하는 것 외에도 SignalR에서 사용 하는 다양 한 전송에는 고유한 요구 사항이 있습니다. 다음 구성에서는 다음과 같은 전송 작업을 지원 합니다.

<a id="browser"></a>

**웹 브라우저 전송 요구 사항**

| 전송 | Internet Explorer | Chrome (Windows 또는 iOS) | Firefox | Safari (OSX 또는 iOS) | Android |
| --- | --- | --- | --- | --- | --- |
| WebSockets | 10+ | 현재-1 | 현재-1 | 현재-1 | 해당 없음 |
| 서버에서 보낸 이벤트 | 해당 없음 | 현재-1 | 현재-1 | 현재-1 | 해당 없음 |
| ForeverFrame | 8+ | 해당 없음 | 해당 없음 | 해당 없음 | 4.1 |
| 긴 폴링 | 8+ | 현재-1 | 현재-1 | 현재-1 | 4.1 |

\*: 6 + 전체 기능에 필요 합니다.

#### <a name="unsupported-browsers"></a>지원 되지 않는 브라우저

SignalR는 이전 브라우저 버전에서 중요 한 문제 없이 실행 *될 수* 있지만, SignalR를 적극적으로 테스트 하지 않으며 일반적으로이에 나타날 수 있는 버그를 수정 하지 않습니다.

### <a name="windows-desktop-and-silverlight-applications"></a>Windows 데스크톱 및 Silverlight 응용 프로그램

웹 브라우저에서 실행 하는 것 외에도 SignalR를 독립 실행형 Windows 클라이언트 또는 Silverlight 응용 프로그램에서 호스팅할 수 있습니다. Windows Desktop 및 Silverlight SignalR 응용 프로그램에는 다음과 같은 시스템 요구 사항이 있습니다.

- .NET 4를 사용 하는 응용 프로그램은 Windows XP SP3 이상에서 지원 됩니다.
- .NET Framework 4.5를 사용 하는 응용 프로그램은 Windows Vista 이상에서 지원 됩니다.

운영 체제 및 .NET framework 요구 사항 외에도 SignalR에서 사용할 수 있는 전송에는 고유한 요구 사항이 있습니다. 다음 구성에서는 다음과 같은 전송 작업을 지원 합니다.

**Windows 데스크톱 및 Silverlight 전송 요구 사항**

| 전송 | .NET 애플리케이션 | Silverlight |
| --- | --- | --- |
| 웹 소켓 | Windows 8 이상 및 .NET 4.5 이상 | 해당 없음 |
| 영원히 프레임 | 해당 없음 | 해당 없음 |
| 서버에서 보낸 이벤트 | .NET 4+ | 5+ |
| 긴 폴링 | .NET 4+ | 5+ |

<a id="android"></a>

### <a name="windows-store-and-windows-phone-applications"></a>Windows 스토어 및 Windows Phone 응용 프로그램

SignalR는 Windows 스토어 응용 프로그램 및 Windows Phone 8 응용 프로그램에서 사용할 수 있습니다. 다음 구성에서는 다음과 같은 전송 작업을 지원 합니다.

**Windows 스토어 및 Windows Phone 전송 요구 사항**

| 전송 | Windows 스토어/.NET | Windows 스토어/JavaScript | Windows Phone/IE | Windows Phone/ .NET |
| --- | --- | --- | --- | --- |
| WebSockets | 해당 없음 | Win8 + | 8+ | 해당 없음 |
| 영원히 프레임 | 해당 없음 | Win8 + | 7.5+ | 해당 없음 |
| 서버에서 보낸 이벤트 | Win8 + | 해당 없음 | 해당 없음 | 8+ |
| 긴 폴링 | Win8 + | Win8 + | 7.5+ | 8+ |

<a id="updates"></a>

## <a name="recommended-updates"></a>권장 업데이트

SignalR 서버에 권장 되는 업데이트는 다음과 같습니다.

- .NET Framework 4.5에 대 한 업데이트는 [여기](https://support.microsoft.com/kb/2750149)에서 사용할 수 있습니다.
- Microsoft는 ASP.NET 용 Qfe를 주기적으로 릴리스 합니다. 사용 가능한 것으로 적용 해야 합니다.
