---
uid: signalr/overview/older-versions/troubleshooting
title: SignalR 문제 해결 (SignalR 1.x) | Microsoft Docs
author: bradygaster
description: 이 문서에서는 SignalR 응용 프로그램 개발과 관련 된 일반적인 문제를 설명 합니다.
ms.author: bradyg
ms.date: 06/05/2013
ms.assetid: 347210ba-c452-4feb-886f-b51d89f58971
msc.legacyurl: /signalr/overview/older-versions/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: 3dbf091ac2daa4da477b405852bb4d1316584fcd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468101"
---
# <a name="signalr-troubleshooting-signalr-1x"></a><span data-ttu-id="5726c-103">SignalR 문제 해결(SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="5726c-103">SignalR Troubleshooting (SignalR 1.x)</span></span>

<span data-ttu-id="5726c-104">[Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="5726c-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="5726c-105">이 문서에서는 SignalR 관련 된 일반적인 문제 해결에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-105">This document describes common troubleshooting issues with SignalR.</span></span>

<span data-ttu-id="5726c-106">이 문서에는 다음과 같은 섹션이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-106">This document contains the following sections.</span></span>

- [<span data-ttu-id="5726c-107">클라이언트와 서버 간에 메서드를 자동으로 호출 하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-107">Calling methods between the client and server silently fails</span></span>](#connection)
- [<span data-ttu-id="5726c-108">기타 연결 문제</span><span class="sxs-lookup"><span data-stu-id="5726c-108">Other connection issues</span></span>](#other)
- [<span data-ttu-id="5726c-109">컴파일 및 서버 쪽 오류</span><span class="sxs-lookup"><span data-stu-id="5726c-109">Compilation and server-side errors</span></span>](#server)
- [<span data-ttu-id="5726c-110">Visual Studio 문제</span><span class="sxs-lookup"><span data-stu-id="5726c-110">Visual Studio issues</span></span>](#vs)
- [<span data-ttu-id="5726c-111">인터넷 정보 서비스 문제</span><span class="sxs-lookup"><span data-stu-id="5726c-111">Internet Information Services issues</span></span>](#iis)
- [<span data-ttu-id="5726c-112">Azure 문제</span><span class="sxs-lookup"><span data-stu-id="5726c-112">Azure issues</span></span>](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a><span data-ttu-id="5726c-113">클라이언트와 서버 간에 메서드를 자동으로 호출 하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-113">Calling methods between the client and server silently fails</span></span>

<span data-ttu-id="5726c-114">이 섹션에서는 클라이언트와 서버 간의 메서드 호출이 의미 있는 오류 메시지 없이 실패할 수 있는 원인을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-114">This section describes possible causes for a method call between client and server to fail without a meaningful error message.</span></span> <span data-ttu-id="5726c-115">SignalR 응용 프로그램에서 서버는 클라이언트가 구현 하는 메서드에 대 한 정보를 포함 하지 않습니다. 서버에서 클라이언트 메서드를 호출 하면 메서드 이름 및 매개 변수 데이터가 클라이언트에 전송 되 고 메서드가 지정 된 형식으로 존재 하는 경우에만 메서드가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-115">In a SignalR application, the server has no information about the methods that the client implements; when the server invokes a client method, the method name and parameter data are sent to the client, and the method is executed only if it exists in the format that the server specified.</span></span> <span data-ttu-id="5726c-116">클라이언트에서 일치 하는 메서드가 없는 경우 아무 일도 발생 하지 않으며 서버에서 오류 메시지가 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-116">If no matching method is found on the client, nothing happens, and no error message is raised on the server.</span></span>

<span data-ttu-id="5726c-117">호출 되지 않는 클라이언트 메서드를 추가로 조사 하기 위해 허브에서 시작 메서드를 호출 하기 전에 로깅을 설정 하 여 서버에서 들어오는 호출을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-117">To further investigate client methods not getting called, you can turn on logging before the calling the start method on the hub to see what calls are coming from the server.</span></span> <span data-ttu-id="5726c-118">JavaScript 응용 프로그램에서 로깅을 사용 하도록 설정 하려면 [클라이언트 쪽 로깅을 사용 하도록 설정 하는 방법 (javascript 클라이언트 버전)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5726c-118">To enable logging in a JavaScript application, see [How to enable client-side logging (JavaScript client version)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging).</span></span> <span data-ttu-id="5726c-119">.NET 클라이언트 응용 프로그램에서 로깅을 사용 하도록 설정 하려면 [클라이언트 쪽 로깅을 사용 하도록 설정 하는 방법 (.Net 클라이언트 버전)](../guide-to-the-api/hubs-api-guide-net-client.md#logging)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5726c-119">To enable logging in a .NET client application, see [How to enable client-side logging (.NET Client version)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).</span></span>

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a><span data-ttu-id="5726c-120">철자가 잘못 된 메서드, 잘못 된 메서드 서명 또는 잘못 된 허브 이름</span><span class="sxs-lookup"><span data-stu-id="5726c-120">Misspelled method, incorrect method signature, or incorrect hub name</span></span>

<span data-ttu-id="5726c-121">호출 된 메서드의 이름 또는 시그니처가 클라이언트의 적절 한 메서드와 정확 하 게 일치 하지 않으면 호출이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-121">If the name or signature of a called method does not exactly match an appropriate method on the client, the call will fail.</span></span> <span data-ttu-id="5726c-122">서버에 의해 호출 된 메서드 이름이 클라이언트의 메서드 이름과 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-122">Verify that the method name called by the server matches the name of the method on the client.</span></span> <span data-ttu-id="5726c-123">또한 SignalR는 JavaScript에서와 같이 카멜식 대/소문자를 사용 하는 메서드를 사용 하 여 허브 프록시를 만들기 때문에 서버에서 `SendMessage` 호출 된 메서드를 클라이언트 프록시에서 `sendMessage` 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-123">Also, SignalR creates the hub proxy using camel-cased methods, as is appropriate in JavaScript, so a method called `SendMessage` on the server would be called `sendMessage` in the client proxy.</span></span> <span data-ttu-id="5726c-124">서버 쪽 코드에서 `HubName` 특성을 사용 하는 경우 사용 된 이름이 클라이언트에서 허브를 만드는 데 사용 된 이름과 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-124">If you use the `HubName` attribute in your server-side code, verify that the name used matches the name used to create the hub on the client.</span></span> <span data-ttu-id="5726c-125">`HubName` 특성을 사용 하지 않는 경우 JavaScript 클라이언트의 허브 이름이 ChatHub 대신 chatHub와 같은 카멜식 대/소문자를 사용 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-125">If you do not use the `HubName` attribute, verify that the name of the hub in a JavaScript client is camel-cased, such as chatHub instead of ChatHub.</span></span>

### <a name="duplicate-method-name-on-client"></a><span data-ttu-id="5726c-126">클라이언트에서 중복 된 메서드 이름</span><span class="sxs-lookup"><span data-stu-id="5726c-126">Duplicate method name on client</span></span>

<span data-ttu-id="5726c-127">클라이언트에서 대/소문자만 다른 중복 메서드가 없는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-127">Verify that you do not have a duplicate method on the client that differs only by case.</span></span> <span data-ttu-id="5726c-128">클라이언트 응용 프로그램에 `sendMessage`이라는 메서드가 있는 경우에는 `SendMessage` 메서드도 없다는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-128">If your client application has a method called `sendMessage`, verify that there isn't also a method called `SendMessage` as well.</span></span>

### <a name="missing-json-parser-on-the-client"></a><span data-ttu-id="5726c-129">클라이언트에 JSON 파서가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-129">Missing JSON parser on the client</span></span>

<span data-ttu-id="5726c-130">SignalR에는 서버와 클라이언트 간의 호출을 serialize 하기 위해 JSON 파서가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-130">SignalR requires a JSON parser to be present to serialize calls between the server and the client.</span></span> <span data-ttu-id="5726c-131">클라이언트에 기본 제공 JSON 파서 (예: Internet Explorer 7)가 없는 경우 응용 프로그램에 하나를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-131">If your client doesn't have a built-in JSON parser (such as Internet Explorer 7), you'll need to include one in your application.</span></span> <span data-ttu-id="5726c-132">JSON 파서는 [여기](http://nuget.org/packages/json2)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-132">You can download the JSON parser [here](http://nuget.org/packages/json2).</span></span>

### <a name="mixing-hub-and-persistentconnection-syntax"></a><span data-ttu-id="5726c-133">Hub 및 PersistentConnection 구문 혼합</span><span class="sxs-lookup"><span data-stu-id="5726c-133">Mixing Hub and PersistentConnection syntax</span></span>

<span data-ttu-id="5726c-134">SignalR는 허브와 PersistentConnections의 두 가지 통신 모델을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-134">SignalR uses two communication models: Hubs and PersistentConnections.</span></span> <span data-ttu-id="5726c-135">이러한 두 통신 모델을 호출 하는 구문은 클라이언트 코드에서 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-135">The syntax for calling these two communication models is different in the client code.</span></span> <span data-ttu-id="5726c-136">서버 코드에 허브를 추가한 경우 모든 클라이언트 코드에서 적절 한 허브 구문을 사용 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-136">If you have added a hub in your server code, verify that all of your client code uses the proper hub syntax.</span></span>

<span data-ttu-id="5726c-137">**JavaScript 클라이언트에 PersistentConnection를 만드는 JavaScript 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="5726c-137">**JavaScript client code that creates a PersistentConnection in a JavaScript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

<span data-ttu-id="5726c-138">**Javascript 클라이언트에서 허브 프록시를 만드는 JavaScript 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="5726c-138">**JavaScript client code that creates a Hub Proxy in a Javascript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

<span data-ttu-id="5726c-139">**C#PersistentConnection에 경로를 매핑하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="5726c-139">**C# server code that maps a route to a PersistentConnection**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

<span data-ttu-id="5726c-140">**C#여러 응용 프로그램이 있는 경우 허브 또는 여러 허브에 경로를 매핑하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="5726c-140">**C# server code that maps a route to a Hub, or to multiple hubs if you have multiple applications**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample4.cs)]

### <a name="connection-started-before-subscriptions-are-added"></a><span data-ttu-id="5726c-141">구독을 추가 하기 전에 연결을 시작 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-141">Connection started before subscriptions are added</span></span>

<span data-ttu-id="5726c-142">서버에서 호출할 수 있는 메서드가 프록시에 추가 되기 전에 허브의 연결이 시작 되 면 메시지가 수신 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-142">If the Hub's connection is started before methods that can be called from the server are added to the proxy, messages will not be received.</span></span> <span data-ttu-id="5726c-143">다음 JavaScript 코드는 허브를 제대로 시작 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-143">The following JavaScript code will not start the hub properly:</span></span>

<span data-ttu-id="5726c-144">**허브 메시지를 수신 하지 못하게 하는 잘못 된 JavaScript 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="5726c-144">**Incorrect JavaScript client code that will not allow Hubs messages to be received**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

<span data-ttu-id="5726c-145">대신 Start를 호출 하기 전에 메서드 구독을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-145">Instead, add the method subscriptions before calling Start:</span></span>

<span data-ttu-id="5726c-146">**허브에 구독을 올바르게 추가 하는 JavaScript 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="5726c-146">**JavaScript client code that correctly adds subscriptions to a hub**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a><span data-ttu-id="5726c-147">허브 프록시에 메서드 이름이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-147">Missing method name on the hub proxy</span></span>

<span data-ttu-id="5726c-148">서버에 정의 된 메서드가 클라이언트에서 구독 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-148">Verify that the method defined on the server is subscribed to on the client.</span></span> <span data-ttu-id="5726c-149">서버에서 메서드를 정의 하는 경우에도 여전히 클라이언트 프록시에 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-149">Even though the server defines the method, it must still be added to the client proxy.</span></span> <span data-ttu-id="5726c-150">메서드는 다음과 같은 방법으로 클라이언트 프록시에 추가할 수 있습니다. 메서드는 허브가 아닌 허브의 `client` 멤버에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-150">Methods can be added to the client proxy in the following ways (Note that the method is added to the `client` member of the hub, not the hub directly):</span></span>

<span data-ttu-id="5726c-151">**허브 프록시에 메서드를 추가 하는 JavaScript 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="5726c-151">**JavaScript client code that adds methods to a hub proxy**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a><span data-ttu-id="5726c-152">허브 또는 허브 메서드가 Public으로 선언 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-152">Hub or hub methods not declared as Public</span></span>

<span data-ttu-id="5726c-153">클라이언트에서 볼 수 있도록 허브 구현 및 메서드를 `public`으로 선언 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-153">To be visible on the client, the hub implementation and methods must be declared as `public`.</span></span>

### <a name="accessing-hub-from-a-different-application"></a><span data-ttu-id="5726c-154">다른 응용 프로그램에서 허브 액세스</span><span class="sxs-lookup"><span data-stu-id="5726c-154">Accessing hub from a different application</span></span>

<span data-ttu-id="5726c-155">SignalR 허브는 SignalR 클라이언트를 구현 하는 응용 프로그램을 통해서만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-155">SignalR Hubs can only be accessed through applications that implement SignalR clients.</span></span> <span data-ttu-id="5726c-156">SignalR는 다른 통신 라이브러리 (예: SOAP 또는 WCF 웹 서비스)와 상호 운용할 수 없습니다. 대상 플랫폼에 사용할 수 있는 SignalR 클라이언트가 없는 경우 서버 끝점에 직접 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-156">SignalR cannot interoperate with other communication libraries (like SOAP or WCF web services.) If there is no SignalR client available for your target platform, you cannot access the server's endpoint directly.</span></span>

### <a name="manually-serializing-data"></a><span data-ttu-id="5726c-157">수동으로 데이터 직렬화</span><span class="sxs-lookup"><span data-stu-id="5726c-157">Manually serializing data</span></span>

<span data-ttu-id="5726c-158">SignalR는 자동으로 JSON을 사용 하 여 메서드 매개 변수를 직렬화 합니다 .이 작업은 직접 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-158">SignalR will automatically use JSON to serialize your method parameters- there's no need to do it yourself.</span></span>

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a><span data-ttu-id="5726c-159">원격 허브 메서드가 OnDisconnected 함수의 클라이언트에서 실행 되지 않음</span><span class="sxs-lookup"><span data-stu-id="5726c-159">Remote Hub method not executed on client in OnDisconnected function</span></span>

<span data-ttu-id="5726c-160">이 동작은 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-160">This behavior is by design.</span></span> <span data-ttu-id="5726c-161">`OnDisconnected`를 호출 하면 허브는 추가 허브 메서드 호출을 허용 하지 않는 `Disconnected` 상태를 이미 입력 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-161">When `OnDisconnected` is called, the hub has already entered the `Disconnected` state, which does not allow further hub methods to be called.</span></span>

<span data-ttu-id="5726c-162">**C#OnDisconnected 이벤트에서 코드를 올바르게 실행 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="5726c-162">**C# server code that correctly executes code in the OnDisconnected event**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="connection-limit-reached"></a><span data-ttu-id="5726c-163">연결 제한에 도달 함</span><span class="sxs-lookup"><span data-stu-id="5726c-163">Connection limit reached</span></span>

<span data-ttu-id="5726c-164">Windows 7과 같은 클라이언트 운영 체제에서 전체 버전의 IIS를 사용 하는 경우 10 개의 연결 제한이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-164">When using the full version of IIS on a client operating system like Windows 7, a 10-connection limit is imposed.</span></span> <span data-ttu-id="5726c-165">클라이언트 OS를 사용 하는 경우이 제한을 방지 하기 위해 IIS Express를 대신 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-165">When using a client OS, use IIS Express instead to avoid this limit.</span></span>

### <a name="cross-domain-connection-not-set-up-properly"></a><span data-ttu-id="5726c-166">도메인 간 연결이 제대로 설정 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-166">Cross-domain connection not set up properly</span></span>

<span data-ttu-id="5726c-167">도메인 간 연결 (SignalR URL이 호스팅 페이지와 동일한 도메인에 있지 않은 연결)이 올바르게 설정 되지 않은 경우 오류 메시지 없이 연결이 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-167">If a cross-domain connection (a connection for which the SignalR URL is not in the same domain as the hosting page) is not set up correctly, the connection may fail without an error message.</span></span> <span data-ttu-id="5726c-168">도메인 간 통신을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 [도메인 간 연결을 설정](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)하는 방법을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5726c-168">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a><span data-ttu-id="5726c-169">NTLM을 사용 하는 연결 (Active Directory)이 .NET 클라이언트에서 작동 하지 않음</span><span class="sxs-lookup"><span data-stu-id="5726c-169">Connection using NTLM (Active Directory) not working in .NET client</span></span>

<span data-ttu-id="5726c-170">연결이 제대로 구성 되지 않은 경우 도메인 보안을 사용 하는 .NET 클라이언트 응용 프로그램의 연결이 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-170">A connection in a .NET client application that uses Domain security may fail if the connection is not configured properly.</span></span> <span data-ttu-id="5726c-171">도메인 환경에서 SignalR를 사용 하려면 다음과 같이 필수 연결 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-171">To use SignalR in a domain environment, set the requisite connection property as follows:</span></span>

<span data-ttu-id="5726c-172">**C#연결 자격 증명을 구현 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="5726c-172">**C# client code that implements connection credentials**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="other"></a>

## <a name="other-connection-issues"></a><span data-ttu-id="5726c-173">기타 연결 문제</span><span class="sxs-lookup"><span data-stu-id="5726c-173">Other connection issues</span></span>

<span data-ttu-id="5726c-174">이 섹션에서는 연결 중에 발생 하는 특정 증상 또는 오류 메시지에 대 한 원인과 해결 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-174">This section describes the causes and solutions for specific symptoms or error messages that occur during a connection.</span></span>

### <a name="start-must-be-called-before-data-can-be-sent-error"></a><span data-ttu-id="5726c-175">"데이터를 전송 하려면 먼저 Start를 호출 해야 합니다." 오류</span><span class="sxs-lookup"><span data-stu-id="5726c-175">"Start must be called before data can be sent" error</span></span>

<span data-ttu-id="5726c-176">이 오류는 코드에서 연결을 시작 하기 전에 SignalR 개체를 참조 하는 경우에 일반적으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-176">This error is commonly seen if code references SignalR objects before the connection is started.</span></span> <span data-ttu-id="5726c-177">서버에 정의 된 메서드를 호출 하는 처리기 및 이와 같은 wireup는 연결이 완료 된 후에 추가 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-177">The wireup for handlers and the like that will call methods defined on the server must be added after the connection completes.</span></span> <span data-ttu-id="5726c-178">`Start`에 대 한 호출은 비동기 이므로 호출 후의 코드가 완료 되기 전에 실행 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-178">Note that the call to `Start` is asynchronous, so code after the call may be executed before it completes.</span></span> <span data-ttu-id="5726c-179">연결을 완전히 시작한 후 처리기를 추가 하는 가장 좋은 방법은 시작 메서드에 매개 변수로 전달 되는 콜백 함수에 추가 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-179">The best way to add handlers after a connection starts completely is to put them into a callback function that is passed as a parameter to the start method:</span></span>

<span data-ttu-id="5726c-180">**SignalR 개체를 참조 하는 이벤트 처리기를 올바르게 추가 하는 JavaScript 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="5726c-180">**JavaScript client code that correctly adds event handlers that reference SignalR objects**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

<span data-ttu-id="5726c-181">SignalR 개체가 여전히 참조 되는 동안 연결이 중지 되는 경우에도이 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-181">This error will also be seen if a connection stops while SignalR objects are still being referenced.</span></span>

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a><span data-ttu-id="5726c-182">"301을 영구적으로 이동" 또는 "302" 일시적으로 이동 "오류</span><span class="sxs-lookup"><span data-stu-id="5726c-182">"301 Moved Permanently" or "302 Moved Temporarily" error</span></span>

<span data-ttu-id="5726c-183">이 오류는 프로젝트가 자동으로 생성 된 프록시를 방해 하는 SignalR 라는 폴더를 포함 하는 경우에 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-183">This error may be seen if the project contains a folder called SignalR, which will interfere with the automatically-created proxy.</span></span> <span data-ttu-id="5726c-184">이 오류를 방지 하려면 응용 프로그램에서 `SignalR` 라는 폴더를 사용 하지 않거나 자동 프록시 생성을 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-184">To avoid this error, do not use a folder called `SignalR` in your application, or turn automatic proxy generation off.</span></span> <span data-ttu-id="5726c-185">자세한 내용은 [생성 된 프록시 및 수행 하는 작업](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5726c-185">See [The Generated Proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) for more details.</span></span>

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a><span data-ttu-id="5726c-186">.NET 또는 Silverlight 클라이언트에서 "403 사용할 수 없음" 오류 발생</span><span class="sxs-lookup"><span data-stu-id="5726c-186">"403 Forbidden" error in .NET or Silverlight client</span></span>

<span data-ttu-id="5726c-187">도메인 간 통신이 제대로 사용 하도록 설정 되지 않은 도메인 간 환경에서이 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-187">This error may occur in cross-domain environments where cross-domain communication is not properly enabled.</span></span> <span data-ttu-id="5726c-188">도메인 간 통신을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 [도메인 간 연결을 설정](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)하는 방법을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5726c-188">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span> <span data-ttu-id="5726c-189">Silverlight 클라이언트에서 도메인 간 연결을 설정 하려면 [silverlight 클라이언트에서 도메인 간](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain)연결을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5726c-189">To establish a cross-domain connection in a Silverlight client, see [Cross-domain connections from Silverlight clients](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).</span></span>

### <a name="404-not-found-error"></a><span data-ttu-id="5726c-190">"404를 찾을 수 없음" 오류</span><span class="sxs-lookup"><span data-stu-id="5726c-190">"404 Not Found" error</span></span>

<span data-ttu-id="5726c-191">이 문제에 대 한 여러 원인이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-191">There are several causes for this issue.</span></span> <span data-ttu-id="5726c-192">다음을 모두 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-192">Verify all of the following:</span></span>

- <span data-ttu-id="5726c-193">**허브 프록시 주소 참조의 형식이 잘못 되었습니다.** 이 오류는 생성 된 허브 프록시 주소에 대 한 참조의 형식이 잘못 된 경우에 일반적으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-193">**Hub proxy address reference not formatted correctly:** This error is commonly seen if the reference to the generated hub proxy address is not formatted correctly.</span></span> <span data-ttu-id="5726c-194">허브 주소에 대 한 참조가 올바르게 설정 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-194">Verify that the reference to the hub address is made properly.</span></span> <span data-ttu-id="5726c-195">자세한 내용은 [동적으로 생성 된 프록시를 참조 하는 방법을](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5726c-195">See [How to reference the dynamically generated proxy](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) for details.</span></span>
- <span data-ttu-id="5726c-196">**허브 경로를 추가 하기 전에 응용 프로그램에 경로를 추가 합니다.** 응용 프로그램에서 다른 경로를 사용 하는 경우 추가 된 첫 번째 경로가 `MapHubs`에 대 한 호출 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-196">**Adding routes to application before adding the hub route:** If your application uses other routes, verify that the first route added is the call to `MapHubs`.</span></span>

### <a name="500-internal-server-error"></a><span data-ttu-id="5726c-197">"500 내부 서버 오류"</span><span class="sxs-lookup"><span data-stu-id="5726c-197">"500 Internal Server Error"</span></span>

<span data-ttu-id="5726c-198">이는 매우 일반적인 오류 이며 다양 한 원인이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-198">This is a very generic error that could have a wide variety of causes.</span></span> <span data-ttu-id="5726c-199">오류의 세부 정보는 서버의 이벤트 로그에 표시 되거나 서버 디버깅을 통해 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-199">The details of the error should appear in the server's event log, or can be found through debugging the server.</span></span> <span data-ttu-id="5726c-200">서버에서 자세한 오류를 설정 하 여 자세한 오류 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-200">More detailed error information may be obtained by turning on detailed errors on the server.</span></span> <span data-ttu-id="5726c-201">자세한 내용은 [허브 클래스에서 오류를 처리 하는 방법](../guide-to-the-api/hubs-api-guide-server.md#handleErrors)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5726c-201">For more information, see [How to handle errors in the Hub class](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).</span></span>

### <a name="typeerror-lthubtypegt-is-undefined-error"></a><span data-ttu-id="5726c-202">"TypeError: &lt;hubType&gt;이 (가) 정의 되어 있지 않습니다." 오류</span><span class="sxs-lookup"><span data-stu-id="5726c-202">"TypeError: &lt;hubType&gt; is undefined" error</span></span>

<span data-ttu-id="5726c-203">`MapHubs`에 대 한 호출이 제대로 수행 되지 않으면이 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-203">This error will result if the call to `MapHubs` is not made properly.</span></span> <span data-ttu-id="5726c-204">자세한 내용은 [SignalR 경로를 등록 하 고 SignalR 옵션을 구성 하는 방법을](../guide-to-the-api/hubs-api-guide-server.md#route) 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5726c-204">See [How to register the SignalR route and configure SignalR options](../guide-to-the-api/hubs-api-guide-server.md#route) for more information.</span></span>

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a><span data-ttu-id="5726c-205">JsonSerializationException가 사용자 코드에서 처리 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-205">JsonSerializationException was unhandled by user code</span></span>

<span data-ttu-id="5726c-206">메서드에 보내는 매개 변수에 직렬화 할 수 없는 형식 (예: 파일 핸들 또는 데이터베이스 연결)이 포함 되어 있지 않은지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-206">Verify that the parameters you send to your methods do not include non-serializable types (like file handles or database connections).</span></span> <span data-ttu-id="5726c-207">클라이언트에 보내지 않으려는 서버 쪽 개체의 멤버를 사용 해야 하는 경우 (보안 또는 serialization의 이유로) `JSONIgnore` 특성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-207">If you need to use members on a server-side object that you don't want to be sent to the client (either for security or for reasons of serialization), use the `JSONIgnore` attribute.</span></span>

### <a name="protocol-error-unknown-transport-error"></a><span data-ttu-id="5726c-208">"프로토콜 오류: 알 수 없는 전송" 오류</span><span class="sxs-lookup"><span data-stu-id="5726c-208">"Protocol error: Unknown transport" error</span></span>

<span data-ttu-id="5726c-209">이 오류는 클라이언트가 SignalR에서 사용 하는 전송을 지원 하지 않는 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-209">This error may occur if the client does not support the transports that SignalR uses.</span></span> <span data-ttu-id="5726c-210">SignalR와 함께 사용할 수 있는 브라우저에 대 한 자세한 내용은 [전송 및 대체](../getting-started/introduction-to-signalr.md#transports) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5726c-210">See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for information on which browsers can be used with SignalR.</span></span>

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a><span data-ttu-id="5726c-211">"JavaScript 허브 프록시 생성을 사용할 수 없습니다."</span><span class="sxs-lookup"><span data-stu-id="5726c-211">"JavaScript Hub proxy generation has been disabled."</span></span>

<span data-ttu-id="5726c-212">`signalr/hubs`에서 동적으로 생성 된 프록시에 대 한 참조를 포함 하는 동시에 `DisableJavaScriptProxies` 설정 된 경우이 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-212">This error will occur if `DisableJavaScriptProxies` is set while also including a reference to the dynamically generated proxy at `signalr/hubs`.</span></span> <span data-ttu-id="5726c-213">프록시를 수동으로 만드는 방법에 대 한 자세한 내용은 [생성 된 프록시와 사용자의 역할](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5726c-213">For more information on creating the proxy manually, see [The generated proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span></span>

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a><span data-ttu-id="5726c-214">"연결 ID의 형식이 잘못 되었습니다." 또는 "활성 SignalR 연결 중에 사용자 id가 변경 될 수 없습니다." 오류</span><span class="sxs-lookup"><span data-stu-id="5726c-214">"The connection ID is in the incorrect format" or "The user identity cannot change during an active SignalR connection" error</span></span>

<span data-ttu-id="5726c-215">이 오류는 인증을 사용 하는 경우 연결을 중지 하기 전에 클라이언트를 로그 아웃할 때 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-215">This error may be seen if authentication is being used, and the client is logged out before the connection is stopped.</span></span> <span data-ttu-id="5726c-216">이 솔루션은 클라이언트를 로그 아웃 하기 전에 SignalR 연결을 중지 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-216">The solution is to stop the SignalR connection before logging the client out.</span></span>

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a><span data-ttu-id="5726c-217">"Catch 되지 않은 오류: SignalR: jQuery를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-217">"Uncaught Error: SignalR: jQuery not found.</span></span> <span data-ttu-id="5726c-218">JQuery가 SignalR 파일 앞에서 참조 되는지 확인 하세요. "오류</span><span class="sxs-lookup"><span data-stu-id="5726c-218">Please ensure jQuery is referenced before the SignalR.js file" error</span></span>

<span data-ttu-id="5726c-219">SignalR JavaScript 클라이언트를 실행 하려면 jQuery를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-219">The SignalR JavaScript client requires jQuery to run.</span></span> <span data-ttu-id="5726c-220">JQuery에 대 한 참조가 올바른지, 사용 된 경로가 올바른지, jQuery에 대 한 참조가 SignalR에 대 한 참조 보다 이전 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-220">Verify that your reference to jQuery is correct, that the path used is valid, and that the reference to jQuery is before the reference to SignalR.</span></span>

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a><span data-ttu-id="5726c-221">"Catch 되지 않은 TypeError: 속성 '&lt;속성&gt;' 정의 되지 않음" 오류를 읽을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-221">"Uncaught TypeError: Cannot read property '&lt;property&gt;' of undefined" error</span></span>

<span data-ttu-id="5726c-222">이 오류는 jQuery를 갖지 않거나 허브 프록시가 제대로 참조 되지 않았기 때문에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-222">This error results from not having jQuery or the hubs proxy referenced properly.</span></span> <span data-ttu-id="5726c-223">JQuery 및 허브 프록시에 대 한 참조가 올바른지, 사용 된 경로가 올바른지, jQuery에 대 한 참조가 허브 프록시에 대 한 참조 보다 이전 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-223">Verify that your reference to jQuery and the hubs proxy is correct, that the path used is valid, and that the reference to jQuery is before the reference to the hubs proxy.</span></span> <span data-ttu-id="5726c-224">허브 프록시에 대 한 기본 참조는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-224">The default reference to the hubs proxy should look like the following:</span></span>

<span data-ttu-id="5726c-225">**허브 프록시를 올바르게 참조 하는 HTML 클라이언트 쪽 코드**</span><span class="sxs-lookup"><span data-stu-id="5726c-225">**HTML client-side code that correctly references the Hubs proxy**</span></span>

[!code-html[Main](troubleshooting/samples/sample11.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a><span data-ttu-id="5726c-226">"RuntimeBinderException이 사용자 코드에서 처리 되지 않았습니다." 오류</span><span class="sxs-lookup"><span data-stu-id="5726c-226">"RuntimeBinderException was unhandled by user code" error</span></span>

<span data-ttu-id="5726c-227">이 오류는 `Hub.On`의 잘못 된 오버 로드를 사용 하는 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-227">This error may occur when the incorrect overload of `Hub.On` is used.</span></span> <span data-ttu-id="5726c-228">메서드에 반환 값이 있는 경우 반환 형식을 제네릭 형식 매개 변수로 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-228">If the method has a return value, the return type must be specified as a generic type parameter:</span></span>

<span data-ttu-id="5726c-229">**프록시를 생성 하지 않고 클라이언트에 정의 된 메서드**</span><span class="sxs-lookup"><span data-stu-id="5726c-229">**Method defined on the client (without generated proxy)**</span></span>

[!code-html[Main](troubleshooting/samples/sample12.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a><span data-ttu-id="5726c-230">연결 ID가 일치 하지 않거나 페이지 로드 간의 연결 끊김</span><span class="sxs-lookup"><span data-stu-id="5726c-230">Connection ID is inconsistent or connection breaks between page loads</span></span>

<span data-ttu-id="5726c-231">이 동작은 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-231">This behavior is by design.</span></span> <span data-ttu-id="5726c-232">허브 개체는 페이지 개체에서 호스트 되므로 페이지가 새로 고쳐질 때 허브가 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-232">Since the hub object is hosted in the page object, the hub is destroyed when the page refreshes.</span></span> <span data-ttu-id="5726c-233">다중 페이지 응용 프로그램은 페이지 로드 간에 일관 되도록 사용자와 연결 Id 간의 연결을 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-233">A multi-page application needs to maintain the association between users and connection IDs so that they will be consistent between page loads.</span></span> <span data-ttu-id="5726c-234">연결 Id는 `ConcurrentDictionary` 개체 또는 데이터베이스의 서버에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-234">The connection IDs can be stored on the server in either a `ConcurrentDictionary` object or a database.</span></span>

### <a name="value-cannot-be-null-error"></a><span data-ttu-id="5726c-235">"값이 null 일 수 없습니다." 오류</span><span class="sxs-lookup"><span data-stu-id="5726c-235">"Value cannot be null" error</span></span>

<span data-ttu-id="5726c-236">선택적 매개 변수가 있는 서버 쪽 메서드는 현재 지원 되지 않습니다. 선택적 매개 변수를 생략 하면 메서드가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-236">Server-side methods with optional parameters are not currently supported; if the optional parameter is omitted, the method will fail.</span></span> <span data-ttu-id="5726c-237">자세한 내용은 [선택적 매개 변수](https://github.com/SignalR/SignalR/issues/324)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5726c-237">For more information, see [Optional Parameters](https://github.com/SignalR/SignalR/issues/324).</span></span>

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a><span data-ttu-id="5726c-238">"Firefox에서 Firebug의 &lt;서버에 대 한 연결을 설정할 수 없습니다&gt;" 오류</span><span class="sxs-lookup"><span data-stu-id="5726c-238">"Firefox can't establish a connection to the server at &lt;address&gt;" error in Firebug</span></span>

<span data-ttu-id="5726c-239">이 오류 메시지는 WebSocket 전송에 대 한 협상이 실패 하 고 다른 전송이 대신 사용 되는 경우 Firebug에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-239">This error message can be seen in Firebug if negotiation of the WebSocket transport fails and another transport is used instead.</span></span> <span data-ttu-id="5726c-240">이 동작은 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-240">This behavior is by design.</span></span>

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a><span data-ttu-id="5726c-241">".NET 클라이언트 응용 프로그램에서" 유효성 검사 절차에 따르면 원격 인증서가 유효 하지 않습니다. "오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-241">"The remote certificate is invalid according to the validation procedure" error in .NET client application</span></span>

<span data-ttu-id="5726c-242">서버에 사용자 지정 클라이언트 인증서가 필요한 경우 요청이 만들어지기 전에 x509certificate를 연결에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-242">If your server requires custom client certificates, then you can add an x509certificate to the connection before the request is made.</span></span> <span data-ttu-id="5726c-243">`Connection.AddClientCertificate`를 사용 하 여 연결에 인증서를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-243">Add the certificate to the connection using `Connection.AddClientCertificate`.</span></span>

### <a name="connection-drops-after-authentication-times-out"></a><span data-ttu-id="5726c-244">인증 시간이 초과 된 후 연결이 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-244">Connection drops after authentication times out</span></span>

<span data-ttu-id="5726c-245">이 동작은 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-245">This behavior is by design.</span></span> <span data-ttu-id="5726c-246">연결이 활성화 되어 있는 동안에는 인증 자격 증명을 수정할 수 없습니다. 자격 증명을 새로 고치려면 연결을 중지 했다가 다시 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-246">Authentication credentials cannot be modified while a connection is active; to refresh credentials, the connection must be stopped and restarted.</span></span>

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a><span data-ttu-id="5726c-247">JQuery Mobile을 사용 하면 OnConnected가 두 번 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-247">OnConnected gets called twice when using jQuery Mobile</span></span>

<span data-ttu-id="5726c-248">jQuery Mobile의 `initializePage` 함수는 각 페이지의 스크립트를 강제로 다시 실행 하 여 두 번째 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-248">jQuery Mobile's `initializePage` function forces the scripts in each page to be re-executed, thus creating a second connection.</span></span> <span data-ttu-id="5726c-249">이 문제에 대 한 해결 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-249">Solutions for this issue include:</span></span>

- <span data-ttu-id="5726c-250">JavaScript 파일 앞에 jQuery Mobile에 대 한 참조를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-250">Include the reference to jQuery Mobile before your JavaScript file.</span></span>
- <span data-ttu-id="5726c-251">`$.mobile.autoInitializePage = false`을 설정 하 여 `initializePage` 함수를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-251">Disable the `initializePage` function by setting `$.mobile.autoInitializePage = false`.</span></span>
- <span data-ttu-id="5726c-252">연결을 시작 하기 전에 페이지 초기화가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-252">Wait for the page to finish initializing before starting the connection.</span></span>

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a><span data-ttu-id="5726c-253">서버에서 보낸 이벤트를 사용 하 여 Silverlight 응용 프로그램에서 메시지가 지연 됨</span><span class="sxs-lookup"><span data-stu-id="5726c-253">Messages are delayed in Silverlight applications using Server Sent Events</span></span>

<span data-ttu-id="5726c-254">Silverlight에서 서버에서 보낸 이벤트를 사용할 때 메시지가 지연 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-254">Messages are delayed when using server sent events on Silverlight.</span></span> <span data-ttu-id="5726c-255">대신 긴 폴링을 강제로 사용 하려면 연결을 시작할 때 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-255">To force long polling to be used instead, use the following when starting the connection:</span></span>

[!code-css[Main](troubleshooting/samples/sample13.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a><span data-ttu-id="5726c-256">영구 프레임 프로토콜을 사용 하는 "사용 권한이 거부 되었습니다."</span><span class="sxs-lookup"><span data-stu-id="5726c-256">"Permission Denied" using Forever Frame protocol</span></span>

<span data-ttu-id="5726c-257">이 문제는 [여기](https://github.com/SignalR/SignalR/issues/1963)에서 설명 하는 알려진 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-257">This is a known issue, described [here](https://github.com/SignalR/SignalR/issues/1963).</span></span> <span data-ttu-id="5726c-258">이 증상은 최신 JQuery 라이브러리를 사용 하 여 볼 수 있습니다. 해결 방법은 응용 프로그램을 JQuery 1.8.2으로 다운 그레이드 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-258">This symptom may be seen using the latest JQuery library; the workaround is to downgrade your application to JQuery 1.8.2.</span></span>

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a><span data-ttu-id="5726c-259">컴파일 및 서버 쪽 오류</span><span class="sxs-lookup"><span data-stu-id="5726c-259">Compilation and server-side errors</span></span>

 <span data-ttu-id="5726c-260">다음 섹션에는 컴파일러 및 서버 쪽 런타임 오류에 대 한 가능한 해결 방법이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-260">The following section contains possible solutions to compiler and server-side runtime errors.</span></span> 

### <a name="reference-to-hub-instance-is-null"></a><span data-ttu-id="5726c-261">허브 인스턴스에 대 한 참조가 null입니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-261">Reference to Hub instance is null</span></span>

<span data-ttu-id="5726c-262">허브 인스턴스는 각 연결에 대해 만들어지므로 코드에서 직접 허브 인스턴스를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-262">Since a hub instance is created for each connection, you can't create an instance of a hub in your code yourself.</span></span> <span data-ttu-id="5726c-263">허브 자체 외부에서 허브의 메서드를 호출 하려면 허브 컨텍스트에 대 한 참조를 얻는 방법에 대해 [허브 클래스 외부에서 클라이언트 메서드를 호출 하 고 그룹을 관리 하는 방법](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5726c-263">To call methods on a hub from outside the hub itself, see [How to call client methods and manage groups from outside the Hub class](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) for how to obtain a reference to the hub context.</span></span>

### <a name="httpcontextcurrentsession-is-null"></a><span data-ttu-id="5726c-264">HTTPContext. 세션이 null입니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-264">HTTPContext.Current.Session is null</span></span>

<span data-ttu-id="5726c-265">이 동작은 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-265">This behavior is by design.</span></span> <span data-ttu-id="5726c-266">SignalR는 세션 상태를 사용 하도록 설정 하면 이중 메시징을 중단 하므로 ASP.NET 세션 상태를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-266">SignalR does not support the ASP.NET session state, since enabling the session state would break duplex messaging.</span></span>

### <a name="no-suitable-method-to-override"></a><span data-ttu-id="5726c-267">재정의할 적절 한 메서드가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-267">No suitable method to override</span></span>

<span data-ttu-id="5726c-268">이전 문서 또는 블로그의 코드를 사용 하는 경우이 오류가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-268">You may see this error if you are using code from older documentation or blogs.</span></span> <span data-ttu-id="5726c-269">변경 되었거나 더 이상 사용 되지 않는 메서드 (예: `OnConnectedAsync`)의 이름을 참조 하 고 있지 않은지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-269">Verify that you are not referencing names of methods that have been changed or deprecated (like `OnConnectedAsync`).</span></span>

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a><span data-ttu-id="5726c-270">HostContextExtensions. WebSocketServerUrl가 null입니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-270">HostContextExtensions.WebSocketServerUrl is null</span></span>

<span data-ttu-id="5726c-271">이 동작은 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-271">This behavior is by design.</span></span> <span data-ttu-id="5726c-272">이 멤버는 더 이상 사용 되지 않으므로 사용 하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-272">This member is deprecated and should not be used.</span></span>

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a><span data-ttu-id="5726c-273">"이름이 ' signalr ' 인 경로가 경로 컬렉션에 이미 있습니다." 오류</span><span class="sxs-lookup"><span data-stu-id="5726c-273">"A route named 'signalr.hubs' is already in the route collection" error</span></span>

<span data-ttu-id="5726c-274">응용 프로그램에서 `MapHubs`를 두 번 호출 하는 경우이 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-274">This error will be seen if `MapHubs` is called twice by your application.</span></span> <span data-ttu-id="5726c-275">일부 예제 응용 프로그램은 전역 응용 프로그램 파일에서 직접 `MapHubs`를 호출 합니다. 다른 클래스는 래퍼 클래스에서 호출을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-275">Some example applications call `MapHubs` directly in the global application file; others make the call in a wrapper class.</span></span> <span data-ttu-id="5726c-276">응용 프로그램에서 두 가지 모두를 수행 하지 않는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-276">Ensure that your application does not do both.</span></span>

<a id="vs"></a>

## <a name="visual-studio-issues"></a><span data-ttu-id="5726c-277">Visual Studio 문제</span><span class="sxs-lookup"><span data-stu-id="5726c-277">Visual Studio issues</span></span>

<span data-ttu-id="5726c-278">이 단원에서는 Visual Studio에서 발생 하는 문제에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-278">This section describes issues encountered in Visual Studio.</span></span>

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a><span data-ttu-id="5726c-279">스크립트 문서 노드가 솔루션 탐색기에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-279">Script Documents node does not appear in Solution Explorer</span></span>

<span data-ttu-id="5726c-280">일부 자습서에서는 디버그 하는 동안 솔루션 탐색기의 "스크립트 문서" 노드로 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-280">Some of our tutorials direct you to the "Script Documents" node in Solution Explorer while debugging.</span></span> <span data-ttu-id="5726c-281">이 노드는 JavaScript 디버거에서 생성 되며 Internet Explorer에서 브라우저 클라이언트를 디버그 하는 동안에만 표시 됩니다. Chrome 또는 Firefox를 사용 하는 경우에는 노드가 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-281">This node is produced by the JavaScript debugger, and will only appear while debugging browser clients in Internet Explorer; the node will not appear if Chrome or Firefox are used.</span></span> <span data-ttu-id="5726c-282">다른 클라이언트 디버거가 실행 중인 경우 (예: Silverlight 디버거) JavaScript 디버거도 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-282">The JavaScript debugger will also not run if another client debugger is running, such as the Silverlight debugger.</span></span>

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a><span data-ttu-id="5726c-283">SignalR가 Visual Studio 2008 이전 버전에서 작동 하지 않음</span><span class="sxs-lookup"><span data-stu-id="5726c-283">SignalR does not work on Visual Studio 2008 or earlier</span></span>

<span data-ttu-id="5726c-284">이 동작은 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-284">This behavior is by design.</span></span> <span data-ttu-id="5726c-285">SignalR에 .NET Framework 4 이상이 필요 합니다. 이렇게 하려면 Visual Studio 2010 이상에서 SignalR 응용 프로그램을 개발 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-285">SignalR requires .NET Framework 4 or later; this requires that SignalR applications be developed in Visual Studio 2010 or later.</span></span>

<a id="iis"></a>

## <a name="iis-issues"></a><span data-ttu-id="5726c-286">IIS 문제</span><span class="sxs-lookup"><span data-stu-id="5726c-286">IIS issues</span></span>

<span data-ttu-id="5726c-287">이 섹션에는 인터넷 정보 서비스 관련 된 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-287">This section contains issues with Internet Information Services.</span></span>

### <a name="web-site-crashes-after-maphubs-call"></a><span data-ttu-id="5726c-288">MapHubs 호출 후 웹 사이트 충돌</span><span class="sxs-lookup"><span data-stu-id="5726c-288">Web site crashes after MapHubs call</span></span>

<span data-ttu-id="5726c-289">최신 버전의 SignalR에서이 문제가 해결 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-289">This issue has been fixed in the latest version of SignalR.</span></span> <span data-ttu-id="5726c-290">NuGet을 사용 하 여 설치를 업데이트 하 여 최신 릴리스 버전의 SignalR를 사용 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-290">Verify that you are using the latest released version of SignalR by updating your installation using NuGet.</span></span>

<a id="azure"></a>

## <a name="azure-issues"></a><span data-ttu-id="5726c-291">Azure 문제</span><span class="sxs-lookup"><span data-stu-id="5726c-291">Azure issues</span></span>

<span data-ttu-id="5726c-292">이 섹션에는 Microsoft Azure 관련 된 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-292">This section contains issues with Microsoft Azure.</span></span>

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a><span data-ttu-id="5726c-293">항목 이름을 변경한 후에 Azure 후면판을 통해 메시지를 받지 않음</span><span class="sxs-lookup"><span data-stu-id="5726c-293">Messages are not received through the Azure backplane after altering topic names</span></span>

<span data-ttu-id="5726c-294">Azure 후면판에서 사용 하는 토픽은 사용자가 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5726c-294">The topics used by the Azure backplane are not intended to be user-configurable.</span></span>
