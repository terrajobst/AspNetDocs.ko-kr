---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-net-client
title: ASP.NET SignalR Hubs API 가이드-.NET 클라이언트 (SignalR 1.x) | Microsoft Docs
author: bradygaster
description: 이 문서에서는 Windows 스토어 (WinRT), WPF, Silverlight, 단점 등 .NET 클라이언트에서 SignalR 버전 2 용 허브 API를 사용 하는 방법을 소개 합니다.
ms.author: bradyg
ms.date: 04/17/2013
ms.assetid: c334adc3-d6dc-44f3-9f06-f7634475aad3
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: 2b22b53c405a865f91b04e677f60b82dd46dbf9b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505973"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-signalr-1x"></a>ASP.NET SignalR Hubs API 가이드-.NET 클라이언트 (SignalR 1.x)

[Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 문서에서는 Windows 스토어 (WinRT), WPF, Silverlight, 콘솔 응용 프로그램 등의 .NET 클라이언트에서 SignalR 버전 2 용 허브 API를 사용 하는 방법을 소개 합니다.
> 
> SignalR Hubs API를 사용 하면 서버에서 연결 된 클라이언트로 또는 클라이언트에서 서버로 Rpc (원격 프로시저 호출)를 수행할 수 있습니다. 서버 코드에서는 클라이언트에서 호출할 수 있는 메서드를 정의 하 고 클라이언트에서 실행 되는 메서드를 호출 합니다. 클라이언트 코드에서는 서버에서 호출할 수 있는 메서드를 정의 하 고 서버에서 실행 되는 메서드를 호출 합니다. SignalR는 모든 클라이언트에서 서버로의 작업을 수행 합니다.
> 
> 또한 SignalR는 영구 연결 이라고 하는 하위 수준 API를 제공 합니다. SignalR, 허브 및 영구 연결에 대 한 소개 나 전체 SignalR 응용 프로그램을 빌드하는 방법을 보여 주는 자습서는 [SignalR-시작](../getting-started/index.md)을 참조 하세요.

## <a name="overview"></a>개요

이 문서는 다음 섹션으로 구성됩니다.

- [클라이언트 설정](#clientsetup)
- [연결을 설정 하는 방법](#establishconnection)

    - [Silverlight 클라이언트에서 도메인 간 연결](#slcrossdomain)
- [연결을 구성 하는 방법](#configureconnection)

    - [WPF 클라이언트에서 동시 연결의 최대 수를 설정 하는 방법](#maxconnections)
    - [쿼리 문자열 매개 변수를 지정 하는 방법](#querystring)
    - [전송 방법을 지정 하는 방법](#transport)
    - [HTTP 헤더를 지정 하는 방법](#httpheaders)
    - [클라이언트 인증서를 지정 하는 방법](#clientcertificate)
- [허브 프록시를 만드는 방법](#proxy)
- [서버에서 호출할 수 있는 클라이언트에서 메서드를 정의 하는 방법](#callclient)

    - [매개 변수가 없는 메서드](#clientmethodswithoutparms)
    - [매개 변수가 있는 메서드, 매개 변수 형식 지정](#clientmethodswithparmtypes)
    - [매개 변수가 있는 메서드, 매개 변수에 대 한 동적 개체 지정](#clientmethodswithdynamparms)
    - [처리기를 제거 하는 방법](#removehandler)
- [클라이언트에서 서버 메서드를 호출 하는 방법](#callserver)
- [연결 수명 이벤트를 처리 하는 방법](#connectionlifetime)
- [오류를 처리 하는 방법](#handleerrors)
- [클라이언트 쪽 로깅을 사용 하도록 설정 하는 방법](#logging)
- [서버에서 호출할 수 있는 클라이언트 메서드에 대 한 WPF, Silverlight 및 콘솔 응용 프로그램 코드 샘플](#wpfsl)

샘플 .NET 클라이언트 프로젝트는 다음 리소스를 참조 하세요.

- [gustavo-armenta/SignalR-](https://github.com/gustavo-armenta/SignalR-Samples) GitHub.com의 샘플 (WinRT, Silverlight, 콘솔 앱 예제).
- GitHub.com의 [DamianEdwards/SignalR-MoveShapeDemo/MoveShape](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) (WPF 예제).
- [SignalR/SignalR](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) 의 GitHub.com (콘솔 앱 예제).

서버 또는 JavaScript 클라이언트를 프로그래밍 하는 방법에 대 한 설명서는 다음 리소스를 참조 하세요.

- [SignalR Hubs API 가이드-서버](../guide-to-the-api/hubs-api-guide-server.md)
- [SignalR Hubs API 가이드-JavaScript 클라이언트](../guide-to-the-api/hubs-api-guide-javascript-client.md)

API 참조 항목에 대 한 링크는 .NET 4.5 버전의 API에 대 한 링크입니다. .NET 4를 사용 하 [는 경우 .net 4 버전의 API 항목](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)을 참조 하세요.

<a id="clientsetup"></a>

## <a name="client-setup"></a>클라이언트 설치

[SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet 패키지를 설치 합니다 ( [SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) 패키지는 아님). 이 패키지는 .NET 4와 .NET 4.5 모두에 대해 WinRT, Silverlight, WPF, 콘솔 응용 프로그램 및 Windows Phone 클라이언트를 지원 합니다.

클라이언트에 있는 SignalR 버전이 서버에 있는 버전과 다른 경우 SignalR는 종종 차이점에 맞게 조정할 수 있습니다. 예를 들어 SignalR 버전 2.0이 출시 되 고 서버에 설치 하면 서버에서 1.1. x가 설치 된 클라이언트와 2.0이 설치 된 클라이언트를 지원 합니다. 서버 버전과 클라이언트 버전의 차이가 너무 SignalR 클라이언트에서 연결을 설정 하려고 할 때 `InvalidOperationException` 예외가 throw 됩니다. 오류 메시지는 "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`"입니다.

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>연결을 설정 하는 방법

연결을 설정 하려면 `HubConnection` 개체를 만들고 프록시를 만들어야 합니다. 연결을 설정 하려면 `HubConnection` 개체에 대해 `Start` 메서드를 호출 합니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample1.cs?highlight=1,4)]

> [!NOTE]
> JavaScript 클라이언트의 경우 연결을 설정 하기 위해 `Start` 메서드를 호출 하기 전에 이벤트 처리기를 하나 이상 등록 해야 합니다. .NET 클라이언트에는이 작업이 필요 하지 않습니다. JavaScript 클라이언트의 경우 생성 된 프록시 코드는 서버에 있는 모든 허브에 대 한 프록시를 자동으로 만들고, 처리기를 등록 하면 클라이언트가 사용할 허브를 표시 하는 방법이 됩니다. 그러나 .NET 클라이언트의 경우에는 허브 프록시를 수동으로 만들 수 있으므로 SignalR은 사용자가 프록시를 만드는 허브를 사용 한다고 가정 합니다.

샘플 코드는 기본 "/signalr" URL을 사용 하 여 SignalR 서비스에 연결 합니다. 다른 기준 URL을 지정 하는 방법에 대 한 자세한 내용은 [ASP.NET SignalR HUBS API Guide-Server-/SIGNALR URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl)을 참조 하세요.

`Start` 메서드는 비동기적으로 실행 됩니다. 연결이 설정 될 때까지 후속 코드 줄이 실행 되지 않도록 하려면 ASP.NET 4.5 비동기 메서드에서 `await`를 사용 하거나 동기 메서드에서 `.Wait()` 합니다. WinRT 클라이언트에서는 `.Wait()`을 사용 하지 마세요.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](signalr-1x-hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

`HubConnection` 클래스는 스레드로부터 안전합니다.

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a>Silverlight 클라이언트에서 도메인 간 연결

Silverlight 클라이언트에서 도메인 간 연결을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 [도메인 경계에서 서비스를 사용할 수 있도록](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx)설정을 참조 하세요.

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>연결을 구성 하는 방법

연결을 설정 하기 전에 다음 옵션 중 하나를 지정할 수 있습니다.

- 동시 연결 제한.
- 쿼리 문자열 매개 변수입니다.
- 전송 방법입니다.
- HTTP 헤더입니다.
- 클라이언트 인증서.

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a>WPF 클라이언트에서 동시 연결의 최대 수를 설정 하는 방법

WPF 클라이언트에서는 기본값 2에서 동시 연결의 최대 수를 늘려야 할 수 있습니다. 권장 값은 10입니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample4.cs?highlight=4)]

자세한 내용은 [Servicepointmanager. DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx)를 참조 하세요.

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>쿼리 문자열 매개 변수를 지정 하는 방법

클라이언트에서 연결할 때 서버에 데이터를 전송 하려는 경우 연결 개체에 쿼리 문자열 매개 변수를 추가할 수 있습니다. 다음 예제에서는 클라이언트 코드에서 쿼리 문자열 매개 변수를 설정 하는 방법을 보여 줍니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample5.cs)]

다음 예에서는 서버 코드에서 쿼리 문자열 매개 변수를 읽는 방법을 보여 줍니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>전송 방법을 지정 하는 방법

연결 프로세스의 일부로 SignalR 클라이언트는 서버와 클라이언트 모두에서 지원 되는 최상의 전송을 결정 하기 위해 일반적으로 서버와 협상 합니다. 사용 하려는 전송을 이미 알고 있는 경우이 협상 프로세스를 무시할 수 있습니다. 전송 방법을 지정 하려면 전송 개체를 Start 메서드로 전달 합니다. 다음 예제에서는 클라이언트 코드에서 전송 메서드를 지정 하는 방법을 보여 줍니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample7.cs?highlight=4)]

[SignalR](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) 네임 스페이스에는 전송을 지정 하는 데 사용할 수 있는 다음과 같은 클래스가 포함 되어 있습니다.

- [LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)
- [ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)
- [WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (서버와 클라이언트가 모두 .net 4.5을 사용 하는 경우에만 사용 가능)
- [Autotransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (클라이언트와 서버 모두에서 지원 되는 최상의 전송을 자동으로 선택 합니다. 이는 기본 전송입니다. 이를 `Start` 메서드에 전달 하는 것은 아무 것도 전달 하지 않는 것과 같은 효과를 갖습니다.)

ForeverFrame 전송은 브라우저 에서만 사용 되므로이 목록에 포함 되지 않습니다.

서버 코드에서 전송 방법을 확인 하는 방법에 대 한 자세한 내용은 [ASP.NET SignalR HUBS API 가이드-서버-컨텍스트 속성에서 클라이언트에 대 한 정보를 가져오는 방법](../guide-to-the-api/hubs-api-guide-server.md#contextproperty)을 참조 하세요. 전송 및 대체에 대 한 자세한 내용은 [SignalR에 대 한 소개-전송 및 대체](../getting-started/introduction-to-signalr.md#transports)를 참조 하세요.

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a>HTTP 헤더를 지정 하는 방법

HTTP 헤더를 설정 하려면 연결 개체에 대 한 `Headers` 속성을 사용 합니다. 다음 예제에서는 HTTP 헤더를 추가 하는 방법을 보여 줍니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a>클라이언트 인증서를 지정 하는 방법

클라이언트 인증서를 추가 하려면 연결 개체에 대해 `AddClientCertificate` 메서드를 사용 합니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a>허브 프록시를 만드는 방법

클라이언트에서 허브가 서버에서 호출할 수 있는 메서드를 정의 하 고 서버의 허브에서 메서드를 호출 하려면 연결 개체에 대해 `CreateHubProxy`를 호출 하 여 허브에 대 한 프록시를 만듭니다. `CreateHubProxy`에 전달 하는 문자열은 허브 클래스의 이름 이거나 서버에서 사용 되는 경우 `HubName` 특성에 지정 된 이름입니다. 이름 일치 시 대/소문자는 구분하지 않습니다.

**서버의 허브 클래스**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

**허브 클래스에 대 한 클라이언트 프록시 만들기**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample11.cs?highlight=2)]

`HubName` 특성을 사용 하 여 허브 클래스를 데코레이팅하는 경우 해당 이름을 사용 합니다.

**서버의 허브 클래스**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample12.cs)]

**허브 클래스에 대 한 클라이언트 프록시 만들기**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample13.cs?highlight=2)]

프록시 개체는 스레드로부터 안전 합니다. 실제로 동일한 `hubName`를 사용 하 여 `HubConnection.CreateHubProxy`을 여러 번 호출 하는 경우 동일한 캐시 된 `IHubProxy` 개체를 가져옵니다.

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>서버에서 호출할 수 있는 클라이언트에서 메서드를 정의 하는 방법

서버에서 호출할 수 있는 메서드를 정의 하려면 프록시의 `On` 메서드를 사용 하 여 이벤트 처리기를 등록 합니다.

메서드 이름 일치는 대/소문자를 구분 하지 않습니다. 예를 들어 서버의 `Clients.All.UpdateStockPrice`은 클라이언트에서 `updateStockPrice`, `updatestockprice`또는 `UpdateStockPrice`를 실행 합니다.

클라이언트 플랫폼 마다 UI를 업데이트 하는 메서드 코드를 작성 하는 방법에 대 한 요구 사항이 다릅니다. 표시 된 예제는 WinRT (Windows 스토어 .NET) 클라이언트를 위한 것입니다. WPF, Silverlight 및 콘솔 응용 프로그램 예제는 [이 항목의 뒷부분](#wpfsl)에 나오는 별도의 섹션에서 제공 됩니다.

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a>매개 변수가 없는 메서드

처리 중인 메서드에 매개 변수가 없는 경우 `On` 메서드의 제네릭이 아닌 오버 로드를 사용 합니다.

**매개 변수 없이 클라이언트 메서드를 호출 하는 서버 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

**매개 변수 없이 서버에서 호출 되는 메서드에 대 한 WinRT 클라이언트 코드 ([이 항목의 뒷부분에 나오는 WPF 및 Silverlight 예제 참조](#wpfsl))**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>매개 변수가 있는 메서드, 매개 변수 형식 지정

처리 중인 메서드에 매개 변수가 있는 경우 매개 변수의 형식을 `On` 메서드의 제네릭 형식으로 지정 합니다. 최대 8 개의 매개 변수를 지정할 수 있도록 하는 `On` 메서드의 제네릭 오버 로드가 있습니다 (Windows Phone 7에서 4). 다음 예제에서는 하나의 매개 변수가 `UpdateStockPrice` 메서드로 전송 됩니다.

**매개 변수를 사용 하 여 클라이언트 메서드를 호출 하는 서버 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

**매개 변수에 사용 되는 스톡 클래스입니다.**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample17.cs)]

**매개 변수를 사용 하 여 서버에서 호출 된 메서드에 대 한 WinRT 클라이언트 코드 ([이 항목의 뒷부분에 나오는 WPF 및 Silverlight 예제 참조](#wpfsl))**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>매개 변수가 있는 메서드, 매개 변수에 대 한 동적 개체 지정

매개 변수를 `On` 메서드의 제네릭 형식으로 지정 하는 대신 매개 변수를 동적 개체로 지정할 수 있습니다.

**매개 변수를 사용 하 여 클라이언트 메서드를 호출 하는 서버 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

**매개 변수에 사용 되는 스톡 클래스입니다.**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample20.cs)]

**매개 변수에 대 한 동적 개체를 사용 하 여 매개 변수를 사용 하 여 서버에서 호출 된 메서드에 대 한 WinRT 클라이언트 코드 ([이 항목의 뒷부분에 나오는 WPF 및 Silverlight 예제 참조](#wpfsl))**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a>처리기를 제거 하는 방법

처리기를 제거 하려면 해당 `Dispose` 메서드를 호출 합니다.

**서버에서 호출 된 메서드에 대 한 클라이언트 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

**처리기를 제거 하는 클라이언트 코드**

[!code-css[Main](signalr-1x-hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>클라이언트에서 서버 메서드를 호출 하는 방법

서버에서 메서드를 호출 하려면 허브 프록시에서 `Invoke` 메서드를 사용 합니다.

서버 메서드에 반환 값이 없는 경우 `Invoke` 메서드의 제네릭이 아닌 오버 로드를 사용 합니다.

**반환 값이 없는 메서드에 대 한 서버 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

**반환 값이 없는 메서드를 호출 하는 클라이언트 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

서버 메서드에 반환 값이 있는 경우 반환 형식을 `Invoke` 메서드의 제네릭 형식으로 지정 합니다.

**반환 값을 가지 며 복합 형식 매개 변수를 사용 하는 메서드의 서버 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

**매개 변수 및 반환 값에 사용 되는 스톡 클래스입니다.**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample27.cs)]

**ASP.NET 4.5 async 메서드에서 반환 값을 가지 며 복합 형식 매개 변수를 사용 하는 메서드를 호출 하는 클라이언트 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

**동기 메서드에서 반환 값을 포함 하 고 복합 형식 매개 변수를 사용 하는 메서드를 호출 하는 클라이언트 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

`Invoke` 메서드는 비동기적으로 실행 되 고 `Task` 개체를 반환 합니다. `await` 또는 `.Wait()`을 지정 하지 않으면 호출 하는 메서드의 실행이 완료 되기 전에 다음 코드 줄이 실행 됩니다.

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>연결 수명 이벤트를 처리 하는 방법

SignalR는 처리할 수 있는 다음 연결 수명 이벤트를 제공 합니다.

- `Received`: 연결에서 데이터를 받을 때 발생 합니다. 받은 데이터를 제공 합니다.
- `ConnectionSlow`: 클라이언트에서 느리거나 자주 삭제 되는 연결을 검색할 때 발생 합니다.
- `Reconnecting`: 기본 전송에서 다시 연결을 시작할 때 발생 합니다.
- `Reconnected`: 기본 전송이 다시 연결 되었을 때 발생 합니다.
- `StateChanged`: 연결 상태가 변경 될 때 발생 합니다. 이전 상태와 새 상태를 제공 합니다. 연결 상태 값에 대 한 자세한 내용은 [Connectionstate 열거](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx)를 참조 하세요.
- `Closed`: 연결의 연결이 끊어지면 발생 합니다.

예를 들어 치명적이 지 않은 오류에 대 한 경고 메시지를 표시 하 고 연결을 속도 저하 하거나 자주 삭제 하는 등의 일시적인 연결 문제를 발생 시키려면 `ConnectionSlow` 이벤트를 처리 합니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample30.cs)]

자세한 내용은 [SignalR의 연결 수명 이벤트 이해 및 처리](../guide-to-the-api/handling-connection-lifetime-events.md)를 참조 하세요.

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>오류를 처리 하는 방법

서버에서 자세한 오류 메시지를 명시적으로 사용 하도록 설정 하지 않은 경우 오류 발생 후 SignalR에서 반환 하는 예외 개체는 오류에 대 한 최소 정보를 포함 합니다. 예를`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`들어 `newContosoChatMessage`에 대 한 호출이 실패 하면 오류 개체의 오류 메시지에는 보안을 위해 프로덕션 환경에서 클라이언트에 자세한 오류 메시지를 보내는 것이 권장 되지 않습니다. 그러나 문제 해결을 위해 자세한 오류 메시지를 사용 하려면 서버에서 다음 코드를 사용 합니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

SignalR에서 발생 하는 오류를 처리 하기 위해 connection 개체의 `Error` 이벤트에 대 한 처리기를 추가할 수 있습니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample32.cs)]

메서드 호출에서 발생 하는 오류를 처리 하려면 try-catch 블록에 코드를 래핑합니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>클라이언트 쪽 로깅을 사용 하도록 설정 하는 방법

클라이언트 쪽 로깅을 사용 하도록 설정 하려면 연결 개체에 대 한 `TraceLevel` 및 `TraceWriter` 속성을 설정 합니다.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample34.cs?highlight=2-3)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a>서버에서 호출할 수 있는 클라이언트 메서드에 대 한 WPF, Silverlight 및 콘솔 응용 프로그램 코드 샘플

서버에서 호출할 수 있는 클라이언트 메서드를 정의 하기 위해 앞에서 보여 준 코드 샘플은 WinRT 클라이언트에 적용 됩니다. 다음 샘플에서는 WPF, Silverlight 및 콘솔 응용 프로그램 클라이언트에 해당 하는 코드를 보여 줍니다.

### <a name="methods-without-parameters"></a>매개 변수가 없는 메서드

**매개 변수 없이 서버에서 호출 되는 메서드의 WPF 클라이언트 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

**매개 변수 없이 서버에서 호출 되는 메서드에 대 한 Silverlight 클라이언트 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

**매개 변수가 없는 서버에서 호출 되는 메서드에 대 한 콘솔 응용 프로그램 클라이언트 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>매개 변수가 있는 메서드, 매개 변수 형식 지정

**매개 변수를 사용 하 여 서버에서 호출 된 메서드의 WPF 클라이언트 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

**매개 변수를 사용 하 여 서버에서 호출 된 메서드에 대 한 Silverlight 클라이언트 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

**매개 변수를 사용 하 여 서버에서 호출 된 메서드에 대 한 콘솔 응용 프로그램 클라이언트 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>매개 변수가 있는 메서드, 매개 변수에 대 한 동적 개체 지정

**매개 변수에 대 한 동적 개체를 사용 하 여 매개 변수를 사용 하는 서버에서 호출 된 메서드의 WPF 클라이언트 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

**매개 변수에 대 한 동적 개체를 사용 하 여 매개 변수를 사용 하 여 서버에서 호출 된 메서드에 대 한 Silverlight 클라이언트 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

**매개 변수에 대 한 동적 개체를 사용 하 여 매개 변수를 사용 하 여 서버에서 호출 된 메서드에 대 한 콘솔 응용 프로그램 클라이언트 코드**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
