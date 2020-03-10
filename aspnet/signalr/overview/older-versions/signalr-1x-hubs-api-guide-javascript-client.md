---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-javascript-client
title: SignalR 1.x Hubs API 가이드-JavaScript 클라이언트 | Microsoft Docs
author: bradygaster
description: '이 문서에서는 JavaScript 클라이언트에서 SignalR 버전 1.1 용 Hubs API를 사용 하는 방법을 소개 합니다 (예: 브라우저 및 Windows 스토어 (WinJS).'
ms.author: bradyg
ms.date: 04/17/2013
ms.assetid: dcd4593b-1118-418a-af71-d12ff33fb36d
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 24850fe5229490bf600e09ad4718abb575a845fa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431105"
---
# <a name="signalr-1x-hubs-api-guide---javascript-client"></a><span data-ttu-id="5fea7-103">SignalR 1.x 허브 API 가이드 - JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="5fea7-103">SignalR 1.x Hubs API Guide - JavaScript Client</span></span>

<span data-ttu-id="5fea7-104">[Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="5fea7-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="5fea7-105">이 문서에서는 브라우저 및 WinJS (Windows 스토어) 응용 프로그램과 같은 JavaScript 클라이언트에서 SignalR 버전 1.1 용 허브 API를 사용 하는 방법을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-105">This document provides an introduction to using the Hubs API for SignalR version 1.1 in JavaScript clients, such as browsers and Windows Store (WinJS) applications.</span></span>
> 
> <span data-ttu-id="5fea7-106">SignalR Hubs API를 사용 하면 서버에서 연결 된 클라이언트로 또는 클라이언트에서 서버로 Rpc (원격 프로시저 호출)를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="5fea7-107">서버 코드에서는 클라이언트에서 호출할 수 있는 메서드를 정의 하 고 클라이언트에서 실행 되는 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="5fea7-108">클라이언트 코드에서는 서버에서 호출할 수 있는 메서드를 정의 하 고 서버에서 실행 되는 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="5fea7-109">SignalR는 모든 클라이언트에서 서버로의 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="5fea7-110">또한 SignalR는 영구 연결 이라고 하는 하위 수준 API를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="5fea7-111">SignalR, 허브 및 영구 연결에 대 한 소개 나 전체 SignalR 응용 프로그램을 빌드하는 방법을 보여 주는 자습서는 [SignalR-시작](../getting-started/index.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5fea7-111">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>

## <a name="overview"></a><span data-ttu-id="5fea7-112">개요</span><span class="sxs-lookup"><span data-stu-id="5fea7-112">Overview</span></span>

<span data-ttu-id="5fea7-113">이 문서는 다음 섹션으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-113">This document contains the following sections:</span></span>

- [<span data-ttu-id="5fea7-114">생성 된 프록시와 사용자를 위해 수행 하는 작업</span><span class="sxs-lookup"><span data-stu-id="5fea7-114">The generated proxy and what it does for you</span></span>](#genproxy)

    - [<span data-ttu-id="5fea7-115">생성 된 프록시를 사용 하는 경우</span><span class="sxs-lookup"><span data-stu-id="5fea7-115">When to use the generated proxy</span></span>](#cantusegenproxy)
- [<span data-ttu-id="5fea7-116">클라이언트 설정</span><span class="sxs-lookup"><span data-stu-id="5fea7-116">Client Setup</span></span>](#clientsetup)

    - [<span data-ttu-id="5fea7-117">동적으로 생성 된 프록시를 참조 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5fea7-117">How to reference the dynamically generated proxy</span></span>](#dynamicproxy)
    - [<span data-ttu-id="5fea7-118">SignalR 생성 프록시에 대 한 물리적 파일을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="5fea7-118">How to create a physical file for the SignalR generated proxy</span></span>](#manualproxy)
- [<span data-ttu-id="5fea7-119">연결을 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5fea7-119">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="5fea7-120">$. hubConnection ()에서 생성 하는 것과 동일한 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-120">$.connection.hub is the same object that $.hubConnection() creates</span></span>](#connequivalence)
    - [<span data-ttu-id="5fea7-121">시작 메서드의 비동기 실행</span><span class="sxs-lookup"><span data-stu-id="5fea7-121">Asynchronous execution of the start method</span></span>](#asyncstart)
- [<span data-ttu-id="5fea7-122">도메인 간 연결을 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5fea7-122">How to establish a cross-domain connection</span></span>](#crossdomain)
- [<span data-ttu-id="5fea7-123">연결을 구성 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5fea7-123">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="5fea7-124">쿼리 문자열 매개 변수를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5fea7-124">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="5fea7-125">전송 방법을 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5fea7-125">How to specify the transport method</span></span>](#transport)
- [<span data-ttu-id="5fea7-126">허브 클래스에 대 한 프록시를 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="5fea7-126">How to get a proxy for a Hub class</span></span>](#getproxy)
- [<span data-ttu-id="5fea7-127">서버에서 호출할 수 있는 클라이언트에서 메서드를 정의 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5fea7-127">How to define methods on the client that the server can call</span></span>](#callclient)
- [<span data-ttu-id="5fea7-128">클라이언트에서 서버 메서드를 호출 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5fea7-128">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="5fea7-129">연결 수명 이벤트를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5fea7-129">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="5fea7-130">오류를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5fea7-130">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="5fea7-131">클라이언트 쪽 로깅을 사용 하도록 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5fea7-131">How to enable client-side logging</span></span>](#logging)

<span data-ttu-id="5fea7-132">서버 또는 .NET 클라이언트를 프로그래밍 하는 방법에 대 한 설명서는 다음 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5fea7-132">For documentation on how to program the server or .NET clients, see the following resources:</span></span>

- [<span data-ttu-id="5fea7-133">SignalR Hubs API 가이드-서버</span><span class="sxs-lookup"><span data-stu-id="5fea7-133">SignalR Hubs API Guide - Server</span></span>](../guide-to-the-api/hubs-api-guide-server.md)
- [<span data-ttu-id="5fea7-134">SignalR Hubs API 가이드-.NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="5fea7-134">SignalR Hubs API Guide - .NET Client</span></span>](../guide-to-the-api/hubs-api-guide-net-client.md)

<span data-ttu-id="5fea7-135">API 참조 항목에 대 한 링크는 .NET 4.5 버전의 API에 대 한 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-135">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="5fea7-136">.NET 4를 사용 하 [는 경우 .net 4 버전의 API 항목](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5fea7-136">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a><span data-ttu-id="5fea7-137">생성 된 프록시와 사용자를 위해 수행 하는 작업</span><span class="sxs-lookup"><span data-stu-id="5fea7-137">The generated proxy and what it does for you</span></span>

<span data-ttu-id="5fea7-138">SignalR에서 생성 하는 프록시를 사용 하거나 사용 하지 않고 SignalR 서비스와 통신 하도록 JavaScript 클라이언트를 프로그래밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-138">You can program a JavaScript client to communicate with a SignalR service with or without a proxy that SignalR generates for you.</span></span> <span data-ttu-id="5fea7-139">프록시는 사용자가 연결 하는 데 사용 하는 코드의 구문을 간소화 하 고, 서버에서 호출 하는 메서드를 작성 하 고, 서버에서 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-139">What the proxy does for you is simplify the syntax of the code you use to connect, write methods that the server calls, and call methods on the server.</span></span>

<span data-ttu-id="5fea7-140">서버 메서드를 호출 하는 코드를 작성할 때 생성 된 프록시를 사용 하면 로컬 함수를 실행 하는 것 처럼 보이는 구문을 사용할 수 있습니다. `invoke('serverMethod', arg1, arg2)`대신 `serverMethod(arg1, arg2)`를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-140">When you write code to call server methods, the generated proxy enables you to use syntax that looks as though you were executing a local function: you can write `serverMethod(arg1, arg2)` instead of `invoke('serverMethod', arg1, arg2)`.</span></span> <span data-ttu-id="5fea7-141">서버 메서드 이름을 잘못 입력 한 경우에는 생성 된 프록시 구문을 사용 하 여 즉각적인 있는 클라이언트 쪽 오류가 발생할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-141">The generated proxy syntax also enables an immediate and intelligible client-side error if you mistype a server method name.</span></span> <span data-ttu-id="5fea7-142">또한 프록시를 정의 하는 파일을 수동으로 만드는 경우 서버 메서드를 호출 하는 코드를 작성할 수 있도록 IntelliSense 지원을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-142">And if you manually create the file that defines the proxies, you can also get IntelliSense support for writing code that calls server methods.</span></span>

<span data-ttu-id="5fea7-143">예를 들어 서버에 다음과 같은 허브 클래스가 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-143">For example, suppose you have the following Hub class on the server:</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

<span data-ttu-id="5fea7-144">다음 코드 예제에서는 서버에서 `NewContosoChatMessage` 메서드를 호출 하 고 서버에서 `addContosoChatMessageToPage` 메서드의 호출을 수신 하는 JavaScript 코드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-144">The following code examples show what JavaScript code looks like for invoking the `NewContosoChatMessage` method on the server and receiving invocations of the `addContosoChatMessageToPage` method from the server.</span></span>

<span data-ttu-id="5fea7-145">**생성 된 프록시 사용**</span><span class="sxs-lookup"><span data-stu-id="5fea7-145">**With the generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

<span data-ttu-id="5fea7-146">**생성 된 프록시 제외**</span><span class="sxs-lookup"><span data-stu-id="5fea7-146">**Without the generated proxy**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a><span data-ttu-id="5fea7-147">생성 된 프록시를 사용 하는 경우</span><span class="sxs-lookup"><span data-stu-id="5fea7-147">When to use the generated proxy</span></span>

<span data-ttu-id="5fea7-148">서버에서 호출 하는 클라이언트 메서드에 대해 여러 이벤트 처리기를 등록 하려는 경우에는 생성 된 프록시를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-148">If you want to register multiple event handlers for a client method that the server calls, you can't use the generated proxy.</span></span> <span data-ttu-id="5fea7-149">그렇지 않으면 코딩 기본 설정에 따라 생성 된 프록시를 사용 하거나 사용 하지 않도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-149">Otherwise, you can choose to use the generated proxy or not based on your coding preference.</span></span> <span data-ttu-id="5fea7-150">사용 하지 않도록 선택 하는 경우 클라이언트 코드의 `script` 요소에서 "signalr/hubs" URL을 참조할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-150">If you choose not to use it, you don't have to reference the "signalr/hubs" URL in a `script` element in your client code.</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="5fea7-151">클라이언트 설치</span><span class="sxs-lookup"><span data-stu-id="5fea7-151">Client setup</span></span>

<span data-ttu-id="5fea7-152">JavaScript 클라이언트에는 jQuery 및 SignalR core JavaScript 파일에 대 한 참조가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-152">A JavaScript client requires references to jQuery and the SignalR core JavaScript file.</span></span> <span data-ttu-id="5fea7-153">JQuery 버전은 1.7.2, 1.8.2 또는 1.9.1와 같은 1.6.4 또는 주 이후 버전 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-153">The jQuery version must be 1.6.4 or major later versions, such as 1.7.2, 1.8.2, or 1.9.1.</span></span> <span data-ttu-id="5fea7-154">생성 된 프록시를 사용 하기로 결정 한 경우 SignalR 생성 된 프록시 JavaScript 파일에 대 한 참조도 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-154">If you decide to use the generated proxy, you also need a reference to the SignalR generated proxy JavaScript file.</span></span> <span data-ttu-id="5fea7-155">다음 예제에서는 생성 된 프록시를 사용 하는 HTML 페이지에서 참조의 모양을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-155">The following example shows what the references might look like in an HTML page that uses the generated proxy.</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample4.html)]

<span data-ttu-id="5fea7-156">이러한 참조는 jQuery first, SignalR core 이후, SignalR 프록시가 마지막 순서로 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-156">These references must be included in this order: jQuery first, SignalR core after that, and SignalR proxies last.</span></span>

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a><span data-ttu-id="5fea7-157">동적으로 생성 된 프록시를 참조 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5fea7-157">How to reference the dynamically generated proxy</span></span>

<span data-ttu-id="5fea7-158">앞의 예제에서 SignalR 생성 된 프록시에 대 한 참조는 물리적 파일이 아니라 동적으로 생성 되는 JavaScript 코드에 대 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-158">In the preceding example, the reference to the SignalR generated proxy is to dynamically generated JavaScript code, not to a physical file.</span></span> <span data-ttu-id="5fea7-159">SignalR는 프록시에 대 한 JavaScript 코드를 즉석에서 만들고 "/signalr/hubs" URL에 대 한 응답으로 클라이언트에 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-159">SignalR creates the JavaScript code for the proxy on the fly and serves it to the client in response to the "/signalr/hubs" URL.</span></span> <span data-ttu-id="5fea7-160">`MapHubs` 메서드의 서버에서 SignalR 연결에 대해 다른 기준 URL을 지정한 경우 동적으로 생성 된 프록시 파일의 URL은 "/hubs"가 추가 된 사용자 지정 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-160">If you specified a different base URL for SignalR connections on the server in your `MapHubs` method, the URL for the dynamically generated proxy file is your custom URL with "/hubs" appended to it.</span></span>

> [!NOTE]
> <span data-ttu-id="5fea7-161">Windows 8 (Windows 스토어) JavaScript 클라이언트의 경우 동적으로 생성 되는 것이 아니라 실제 프록시 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-161">For Windows 8 (Windows Store) JavaScript clients, use the physical proxy file instead of the dynamically generated one.</span></span> <span data-ttu-id="5fea7-162">자세한 내용은이 항목의 뒷부분에 나오는 [SignalR 생성 된 프록시에 대 한 물리적 파일을 만드는 방법](#manualproxy) 을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="5fea7-162">For more information, see [How to create a physical file for the SignalR generated proxy](#manualproxy) later in this topic.</span></span>

<span data-ttu-id="5fea7-163">ASP.NET MVC 4 Razor 뷰에서 물결표를 사용 하 여 프록시 파일 참조의 응용 프로그램 루트를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-163">In an ASP.NET MVC 4 Razor view, use the tilde to refer to the application root in your proxy file reference:</span></span>

[!code-html[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample5.html)]

<span data-ttu-id="5fea7-164">MVC 4에서 SignalR를 사용 하는 방법에 대 한 자세한 내용은 [SignalR 및 mvc 4 시작](tutorial-getting-started-with-signalr-and-mvc-4.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5fea7-164">For more information about using SignalR in MVC 4, see [Getting Started with SignalR and MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md).</span></span>

<span data-ttu-id="5fea7-165">ASP.NET MVC 3 Razor 뷰에서 프록시 파일 참조에 `Url.Content`를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-165">In an ASP.NET MVC 3 Razor view, use `Url.Content` for your proxy file reference:</span></span>

[!code-cshtml[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample6.cshtml)]

<span data-ttu-id="5fea7-166">ASP.NET Web Forms 응용 프로그램에서 프록시 파일 참조에 `ResolveClientUrl`를 사용 하거나, 앱 루트 상대 경로 (물결표로 시작)를 사용 하 여 ScriptManager를 통해 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-166">In an ASP.NET Web Forms application, use `ResolveClientUrl` for your proxies file reference or register it via the ScriptManager using an app root relative path (starting with a tilde):</span></span>

[!code-aspx[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample7.aspx)]

<span data-ttu-id="5fea7-167">일반적인 규칙으로, CSS 또는 JavaScript 파일에 사용 하는 "/signalr/hubs" URL을 지정 하는 데 동일한 방법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-167">As a general rule, use the same method for specifying the "/signalr/hubs" URL that you use for CSS or JavaScript files.</span></span> <span data-ttu-id="5fea7-168">물결표를 사용 하지 않고 URL을 지정 하는 경우 일부 시나리오에서는 IIS Express를 사용 하 여 Visual Studio에서 테스트 하는 경우 응용 프로그램이 올바르게 작동 하지만 전체 IIS에 배포할 때 404 오류가 발생 하 고 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-168">If you specify a URL without using a tilde, in some scenarios your application will work correctly when you test in Visual Studio using IIS Express but will fail with a 404 error when you deploy to full IIS.</span></span> <span data-ttu-id="5fea7-169">자세한 내용은 MSDN 사이트에서 [Visual Studio for ASP.NET 웹 프로젝트의 웹 서버](https://msdn.microsoft.com/library/58wxa9w5.aspx) 에서 **루트 수준 리소스에 대 한 참조 확인** 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5fea7-169">For more information, see **Resolving References to Root-Level Resources** in [Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx) on the MSDN site.</span></span>

<span data-ttu-id="5fea7-170">디버그 모드에서 Visual Studio 2012을 사용 하 여 웹 프로젝트를 실행 하 고 Internet Explorer를 브라우저로 사용 하는 경우 다음 그림과 같이 **스크립트 문서**아래 **솔루션 탐색기** 에서 프록시 파일을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-170">When you run a web project in Visual Studio 2012 in debug mode, and if you use Internet Explorer as your browser, you can see the proxy file in **Solution Explorer** under **Script Documents**, as shown in the following illustration.</span></span>

![솔루션 탐색기에서 JavaScript 생성 프록시 파일](signalr-1x-hubs-api-guide-javascript-client/_static/image1.png)

<span data-ttu-id="5fea7-172">파일의 내용을 보려면 **허브**를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-172">To see the contents of the file, double-click **hubs**.</span></span> <span data-ttu-id="5fea7-173">Visual Studio 2012 및 Internet Explorer를 사용 하지 않거나 디버그 모드가 아닌 경우 "/signalR/hubs" URL로 이동 하 여 파일의 내용을 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-173">If you are not using Visual Studio 2012 and Internet Explorer, or if you are not in debug mode, you can also get the contents of the file by browsing to the "/signalR/hubs" URL.</span></span> <span data-ttu-id="5fea7-174">예를 들어 사이트가 `http://localhost:56699`에서 실행 되는 경우 브라우저에서 `http://localhost:56699/SignalR/hubs`로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-174">For example, if your site is running at `http://localhost:56699`, go to `http://localhost:56699/SignalR/hubs` in your browser.</span></span>

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a><span data-ttu-id="5fea7-175">SignalR 생성 프록시에 대 한 물리적 파일을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="5fea7-175">How to create a physical file for the SignalR generated proxy</span></span>

<span data-ttu-id="5fea7-176">동적으로 생성 된 프록시에 대 한 대 안으로 프록시 코드를 포함 하는 물리적 파일을 만들고 해당 파일을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-176">As an alternative to the dynamically generated proxy, you can create a physical file that has the proxy code and reference that file.</span></span> <span data-ttu-id="5fea7-177">이러한 작업을 수행 하 여 캐싱 또는 번들 동작을 제어 하거나 서버 메서드를 코딩 하는 경우 IntelliSense를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-177">You might want to do that for control over caching or bundling behavior, or to get IntelliSense when you are coding calls to server methods.</span></span>

<span data-ttu-id="5fea7-178">프록시 파일을 만들려면 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-178">To create a proxy file, perform the following steps:</span></span>

1. <span data-ttu-id="5fea7-179">[SignalR 유틸리티](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-179">Install the [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet package.</span></span>
2. <span data-ttu-id="5fea7-180">명령 프롬프트를 열고 SignalR 파일이 포함 된 *tools* 폴더로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-180">Open a command prompt and browse to the *tools* folder that contains the SignalR.exe file.</span></span> <span data-ttu-id="5fea7-181">Tools 폴더는 다음 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-181">The tools folder is at the following location:</span></span>

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.1.0.1\tools`
3. <span data-ttu-id="5fea7-182">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-182">Enter the following command:</span></span>

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    <span data-ttu-id="5fea7-183">*.Dll* 의 경로는 일반적으로 프로젝트 폴더의 *bin* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-183">The path to your *.dll* is typically the *bin* folder in your project folder.</span></span>

    <span data-ttu-id="5fea7-184">이 명령은 *signalr*와 동일한 폴더에 *node.js* 라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-184">This command creates a file named *server.js* in the same folder as *signalr.exe*.</span></span>
4. <span data-ttu-id="5fea7-185">*서버 .js* 파일을 프로젝트의 적절 한 폴더에 배치 하 고 응용 프로그램에 적절 하 게 이름을 바꾼 다음 "signalr/hubs" 참조 대신 해당 폴더에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-185">Put the *server.js* file in an appropriate folder in your project, rename it as appropriate for your application, and add a reference to it in place of the "signalr/hubs" reference.</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="5fea7-186">연결을 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5fea7-186">How to establish a connection</span></span>

<span data-ttu-id="5fea7-187">연결을 설정 하려면 먼저 연결 개체를 만들고 프록시를 만든 다음 서버에서 호출할 수 있는 메서드에 대 한 이벤트 처리기를 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-187">Before you can establish a connection, you have to create a connection object, create a proxy, and register event handlers for methods that can be called from the server.</span></span> <span data-ttu-id="5fea7-188">프록시 및 이벤트 처리기를 설정 하는 경우 `start` 메서드를 호출 하 여 연결을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-188">When the proxy and event handlers are set up, establish the connection by calling the `start` method.</span></span>

<span data-ttu-id="5fea7-189">생성 된 프록시를 사용 하는 경우 생성 된 프록시 코드가 사용자에 게이를 수행 하므로 연결 개체를 직접 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-189">If you are using the generated proxy, you don't have to create the connection object in your own code because the generated proxy code does it for you.</span></span>

<a id="nogenconnection"></a>

<span data-ttu-id="5fea7-190">**생성 된 프록시를 사용 하 여 연결 설정**</span><span class="sxs-lookup"><span data-stu-id="5fea7-190">**Establish a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

<span data-ttu-id="5fea7-191">**생성 된 프록시를 사용 하지 않고 연결 설정**</span><span class="sxs-lookup"><span data-stu-id="5fea7-191">**Establish a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

<span data-ttu-id="5fea7-192">샘플 코드는 기본 "/signalr" URL을 사용 하 여 SignalR 서비스에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-192">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="5fea7-193">다른 기준 URL을 지정 하는 방법에 대 한 자세한 내용은 [ASP.NET SignalR HUBS API Guide-Server-/SIGNALR URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5fea7-193">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span></span>

> [!NOTE]
> <span data-ttu-id="5fea7-194">일반적으로 `start` 메서드를 호출 하 여 연결을 설정 하기 전에 이벤트 처리기를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-194">Normally you register event handlers before calling the `start` method to establish the connection.</span></span> <span data-ttu-id="5fea7-195">연결을 설정한 후 일부 이벤트 처리기를 등록 하려는 경우에는이 작업을 수행할 수 있지만 `start` 메서드를 호출 하기 전에 이벤트 처리기를 하나 이상 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-195">If you want to register some event handlers after establishing the connection, you can do that, but you must register at least one of your event handler(s) before calling the `start` method.</span></span> <span data-ttu-id="5fea7-196">한 가지 이유는 응용 프로그램에 많은 허브가 있을 수 있지만,이 중 하나에만 사용 하려는 경우 모든 허브에서 `OnConnected` 이벤트를 트리거하지 않으려는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-196">One reason for this is that there can be many Hubs in an application, but you wouldn't want to trigger the `OnConnected` event on every Hub if you are only going to use to one of them.</span></span> <span data-ttu-id="5fea7-197">연결이 설정 되 면 허브의 프록시에 클라이언트 메서드가 있으면 `OnConnected` 이벤트를 SignalR 알려 주는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-197">When the connection is established, the presence of a client method on a Hub's proxy is what tells SignalR to trigger the `OnConnected` event.</span></span> <span data-ttu-id="5fea7-198">`start` 메서드를 호출 하기 전에 이벤트 처리기를 등록 하지 않으면 허브에서 메서드를 호출할 수 있지만 허브의 `OnConnected` 메서드가 호출 되지 않으며 서버에서 클라이언트 메서드가 호출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-198">If you don't register any event handlers before calling the `start` method, you will be able to invoke methods on the Hub, but the Hub's `OnConnected` method won't be called and no client methods will be invoked from the server.</span></span>

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a><span data-ttu-id="5fea7-199">$. hubConnection ()에서 생성 하는 것과 동일한 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-199">$.connection.hub is the same object that $.hubConnection() creates</span></span>

<span data-ttu-id="5fea7-200">예제에서 볼 수 있듯이 생성 된 프록시를 사용 하는 경우 `$.connection.hub` 연결 개체를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-200">As you can see from the examples, when you use the generated proxy, `$.connection.hub` refers to the connection object.</span></span> <span data-ttu-id="5fea7-201">이는 생성 된 프록시를 사용 하지 않는 경우 `$.hubConnection()`를 호출 하 여 가져오는 것과 동일한 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-201">This is the same object that you get by calling `$.hubConnection()` when you aren't using the generated proxy.</span></span> <span data-ttu-id="5fea7-202">생성 된 프록시 코드는 다음 문을 실행 하 여 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-202">The generated proxy code creates the connection for you by executing the following statement:</span></span>

![생성 된 프록시 파일에서 연결 만들기](signalr-1x-hubs-api-guide-javascript-client/_static/image3.png)

<span data-ttu-id="5fea7-204">생성 된 프록시를 사용 하는 경우 생성 된 프록시를 사용 하지 않을 때 연결 개체를 사용 하 여 수행할 수 있는 `$.connection.hub` 모든 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-204">When you're using the generated proxy, you can do anything with `$.connection.hub` that you can do with a connection object when you're not using the generated proxy.</span></span>

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a><span data-ttu-id="5fea7-205">시작 메서드의 비동기 실행</span><span class="sxs-lookup"><span data-stu-id="5fea7-205">Asynchronous execution of the start method</span></span>

<span data-ttu-id="5fea7-206">`start` 메서드는 비동기적으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-206">The `start` method executes asynchronously.</span></span> <span data-ttu-id="5fea7-207">[JQuery 지연 개체](http://api.jquery.com/category/deferred-object/)를 반환 합니다. 즉, `pipe`, `done`및 `fail`와 같은 메서드를 호출 하 여 콜백 함수를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-207">It returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/), which means that you can add callback functions by calling methods such as `pipe`, `done`, and `fail`.</span></span> <span data-ttu-id="5fea7-208">서버 메서드 호출과 같이 연결이 설정 된 후에 실행 하려는 코드가 있는 경우 해당 코드를 콜백 함수에 넣거나 콜백 함수에서 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-208">If you have code that you want to execute after the connection is established, such as a call to a server method, put that code in a callback function or call it from a callback function.</span></span> <span data-ttu-id="5fea7-209">`.done` 콜백 메서드는 연결이 설정 된 후, 서버의 `OnConnected` 이벤트 처리기 메서드에 있는 코드의 실행이 완료 된 후에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-209">The `.done` callback method is executed after the connection has been established, and after any code that you have in your `OnConnected` event handler method on the server finishes executing.</span></span>

<span data-ttu-id="5fea7-210">앞의 예제에서 `.done` 콜백이 아닌 `start` 메서드 호출 후에 다음 코드 줄로 "Now connected" 문을 입력 하면 다음 예제와 같이 연결이 설정 되기 전에 `console.log` 줄이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-210">If you put the "Now connected" statement from the preceding example as the next line of code after the `start` method call (not in a `.done` callback), the `console.log` line will execute before the connection is established, as shown in the following example:</span></span>

![연결이 설정 된 후 실행 되는 코드를 작성 하는 잘못 된 방법](signalr-1x-hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a><span data-ttu-id="5fea7-212">도메인 간 연결을 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5fea7-212">How to establish a cross-domain connection</span></span>

<span data-ttu-id="5fea7-213">일반적으로 브라우저에서 `http://contoso.com`의 페이지를 로드 하는 경우에는 `http://contoso.com/signalr`에서 SignalR 연결이 동일한 도메인에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-213">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="5fea7-214">`http://contoso.com` 페이지에서 `http://fabrikam.com/signalr`에 연결 하는 경우에는 도메인 간 연결을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-214">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="5fea7-215">보안상의 이유로 도메인 간 연결은 기본적으로 사용 하지 않도록 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-215">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="5fea7-216">도메인 간 연결을 설정 하려면 서버에서 도메인 간 연결을 사용 하도록 설정 하 고 연결 개체를 만들 때 연결 URL을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-216">To establish a cross-domain connection, make sure that cross-domain connections are enabled on the server, and specify the connection URL when you create the connection object.</span></span> <span data-ttu-id="5fea7-217">SignalR는 [JSONP](http://en.wikipedia.org/wiki/JSONP) 또는 [CORS](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing)와 같은 도메인 간 연결에 대 한 적절 한 기술을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-217">SignalR will use the appropriate technology for cross-domain connections, such as [JSONP](http://en.wikipedia.org/wiki/JSONP) or [CORS](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span></span>

<span data-ttu-id="5fea7-218">서버에서 `MapHubs` 메서드를 호출할 때 해당 옵션을 선택 하 여 도메인 간 연결을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-218">On the server, enable cross-domain connections by selecting that option when you call the `MapHubs` method.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample10.cs?highlight=2)]

<span data-ttu-id="5fea7-219">클라이언트에서 생성 된 프록시를 사용 하지 않고 연결 개체를 만들 때 또는 생성 된 프록시를 사용 하 여 시작 메서드를 호출 하기 전에 URL을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-219">On the client, specify the URL when you create the connection object (without the generated proxy) or before you call the start method (with the generated proxy).</span></span>

<span data-ttu-id="5fea7-220">**생성 된 프록시를 사용 하 여 도메인 간 연결을 지정 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="5fea7-220">**Client code that specifies a cross-domain connection (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample11.js?highlight=1)]

<span data-ttu-id="5fea7-221">**생성 된 프록시를 사용 하지 않고 도메인 간 연결을 지정 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="5fea7-221">**Client code that specifies a cross-domain connection (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

<span data-ttu-id="5fea7-222">`$.hubConnection` 생성자를 사용 하는 경우 `useDefaultUrl`를 `false`로 지정 하지 않으면 URL에 `signalr`를 포함할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-222">When you use the `$.hubConnection` constructor, you don't have to include `signalr` in the URL because it is added automatically (unless you specify `useDefaultUrl` as `false`).</span></span>

<span data-ttu-id="5fea7-223">서로 다른 끝점에 대 한 여러 연결을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-223">You can create multiple connections to different endpoints.</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample13.js)]

> [!NOTE] 
> 
> - <span data-ttu-id="5fea7-224">코드에서 `jQuery.support.cors` true로 설정 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="5fea7-224">Don't set `jQuery.support.cors` to true in your code.</span></span>
> 
>     ![JQuery를 true로 설정 하지 마세요.](signalr-1x-hubs-api-guide-javascript-client/_static/image7.png)
> 
>     <span data-ttu-id="5fea7-226">SignalR는 JSONP 또는 CORS 사용을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-226">SignalR handles the use of JSONP or CORS.</span></span> <span data-ttu-id="5fea7-227">`jQuery.support.cors`를 true로 설정 하면 SignalR에서 브라우저가 CORS를 지원 한다고 가정 하기 때문에 JSONP를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-227">Setting `jQuery.support.cors` to true disables JSONP because it causes SignalR to assume the browser supports CORS.</span></span>
> - <span data-ttu-id="5fea7-228">Localhost URL에 연결 하는 경우 Internet Explorer 10은 도메인 간 연결을 고려 하지 않으므로 서버에서 도메인 간 연결을 사용 하도록 설정 하지 않은 경우에도 응용 프로그램은 IE 10에서 로컬로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-228">When you're connecting to a localhost URL, Internet Explorer 10 won't consider it a cross-domain connection, so the application will work locally with IE 10 even if you haven't enabled cross-domain connections on the server.</span></span>
> - <span data-ttu-id="5fea7-229">Internet Explorer 9에서 도메인 간 연결을 사용 하는 방법에 대 한 자세한 내용은 [이 StackOverflow 스레드](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5fea7-229">For information about using cross-domain connections with Internet Explorer 9, see [this StackOverflow thread](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).</span></span>
> - <span data-ttu-id="5fea7-230">Chrome에서 도메인 간 연결을 사용 하는 방법에 대 한 자세한 내용은 [이 StackOverflow 스레드](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5fea7-230">For information about using cross-domain connections with Chrome, see [this StackOverflow thread](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).</span></span>
> - <span data-ttu-id="5fea7-231">샘플 코드는 기본 "/signalr" URL을 사용 하 여 SignalR 서비스에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-231">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="5fea7-232">다른 기준 URL을 지정 하는 방법에 대 한 자세한 내용은 [ASP.NET SignalR HUBS API Guide-Server-/SIGNALR URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5fea7-232">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="5fea7-233">연결을 구성 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5fea7-233">How to configure the connection</span></span>

<span data-ttu-id="5fea7-234">연결을 설정 하기 전에 쿼리 문자열 매개 변수를 지정 하거나 전송 방법을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-234">Before you establish a connection, you can specify query string parameters or specify the transport method.</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="5fea7-235">쿼리 문자열 매개 변수를 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5fea7-235">How to specify query string parameters</span></span>

<span data-ttu-id="5fea7-236">클라이언트에서 연결할 때 서버에 데이터를 전송 하려는 경우 연결 개체에 쿼리 문자열 매개 변수를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-236">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="5fea7-237">다음 예에서는 클라이언트 코드에서 쿼리 문자열 매개 변수를 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-237">The following examples show how to set a query string parameter in client code.</span></span>

<span data-ttu-id="5fea7-238">**생성 된 프록시를 사용 하 여 시작 메서드를 호출 하기 전에 쿼리 문자열 값을 설정 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5fea7-238">**Set a query string value before calling the start method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample14.js?highlight=1)]

<span data-ttu-id="5fea7-239">**생성 된 프록시 없이 start 메서드를 호출 하기 전에 쿼리 문자열 값을 설정 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5fea7-239">**Set a query string value before calling the start method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample15.js?highlight=2)]

<span data-ttu-id="5fea7-240">다음 예에서는 서버 코드에서 쿼리 문자열 매개 변수를 읽는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-240">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample16.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="5fea7-241">전송 방법을 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5fea7-241">How to specify the transport method</span></span>

<span data-ttu-id="5fea7-242">연결 프로세스의 일부로 SignalR 클라이언트는 서버와 클라이언트 모두에서 지원 되는 최상의 전송을 결정 하기 위해 일반적으로 서버와 협상 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-242">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="5fea7-243">사용 하려는 전송을 이미 알고 있는 경우 `start` 메서드를 호출할 때 전송 방법을 지정 하 여이 협상 프로세스를 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-243">If you already know which transport you want to use, you can bypass this negotiation process by specifying the transport method when you call the `start` method.</span></span>

<span data-ttu-id="5fea7-244">**전송 메서드를 지정 하는 클라이언트 코드 (생성 된 프록시 포함)**</span><span class="sxs-lookup"><span data-stu-id="5fea7-244">**Client code that specifies the transport method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

<span data-ttu-id="5fea7-245">**전송 메서드를 지정 하는 클라이언트 코드 (생성 된 프록시 제외)**</span><span class="sxs-lookup"><span data-stu-id="5fea7-245">**Client code that specifies the transport method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

<span data-ttu-id="5fea7-246">또는 SignalR에서 시도 하는 순서 대로 여러 전송 방법을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-246">As an alternative, you can specify multiple transport methods in the order in which you want SignalR to try them:</span></span>

<span data-ttu-id="5fea7-247">**생성 된 프록시를 사용 하 여 사용자 지정 전송 대체 (fallback) 체계를 지정 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="5fea7-247">**Client code that specifies a custom transport fallback scheme (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample19.js?highlight=1)]

<span data-ttu-id="5fea7-248">**생성 된 프록시를 사용 하지 않고 사용자 지정 전송 대체 (fallback) 체계를 지정 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="5fea7-248">**Client code that specifies a custom transport fallback scheme (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample20.js?highlight=2)]

<span data-ttu-id="5fea7-249">전송 방법 지정에 다음 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-249">You can use the following values for specifying the transport method:</span></span>

- <span data-ttu-id="5fea7-250">"webSockets"</span><span class="sxs-lookup"><span data-stu-id="5fea7-250">"webSockets"</span></span>
- <span data-ttu-id="5fea7-251">"foreverFrame"</span><span class="sxs-lookup"><span data-stu-id="5fea7-251">"foreverFrame"</span></span>
- <span data-ttu-id="5fea7-252">"serverSentEvents"</span><span class="sxs-lookup"><span data-stu-id="5fea7-252">"serverSentEvents"</span></span>
- <span data-ttu-id="5fea7-253">"longPolling"</span><span class="sxs-lookup"><span data-stu-id="5fea7-253">"longPolling"</span></span>

<span data-ttu-id="5fea7-254">다음 예에서는 연결에서 사용 되는 전송 방법을 확인 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-254">The following examples show how to find out which transport method is being used by a connection.</span></span>

<span data-ttu-id="5fea7-255">**연결에서 사용 하는 전송 방법 (생성 된 프록시 포함)을 표시 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="5fea7-255">**Client code that displays the transport method used by a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample21.js?highlight=2)]

<span data-ttu-id="5fea7-256">**생성 된 프록시를 사용 하지 않고 연결에서 사용 되는 전송 방법을 표시 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="5fea7-256">**Client code that displays the transport method used by a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample22.js?highlight=3)]

<span data-ttu-id="5fea7-257">서버 코드에서 전송 방법을 확인 하는 방법에 대 한 자세한 내용은 [ASP.NET SignalR HUBS API 가이드-서버-컨텍스트 속성에서 클라이언트에 대 한 정보를 가져오는 방법](../guide-to-the-api/hubs-api-guide-server.md#contextproperty)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5fea7-257">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](../guide-to-the-api/hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="5fea7-258">전송 및 대체에 대 한 자세한 내용은 [SignalR에 대 한 소개-전송 및 대체](../getting-started/introduction-to-signalr.md#transports)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5fea7-258">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a><span data-ttu-id="5fea7-259">허브 클래스에 대 한 프록시를 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="5fea7-259">How to get a proxy for a Hub class</span></span>

<span data-ttu-id="5fea7-260">사용자가 만드는 각 연결 개체는 하나 이상의 허브 클래스를 포함 하는 SignalR 서비스에 대 한 연결 정보를 캡슐화 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-260">Each connection object that you create encapsulates information about a connection to a SignalR service that contains one or more Hub classes.</span></span> <span data-ttu-id="5fea7-261">허브 클래스와 통신 하려면 직접 만든 프록시 개체 (생성 된 프록시를 사용 하지 않는 경우) 또는 사용자를 위해 생성 된 프록시 개체를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-261">To communicate with a Hub class, you use a proxy object which you create yourself (if you're not using the generated proxy) or which is generated for you.</span></span>

<span data-ttu-id="5fea7-262">클라이언트에서 프록시 이름은 카멜식 대/소문자를 구분 하는 허브 클래스 이름 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-262">On the client the proxy name is a camel-cased version of the Hub class name.</span></span> <span data-ttu-id="5fea7-263">SignalR는 JavaScript 코드가 JavaScript 규칙을 준수할 수 있도록 이러한 변경을 자동으로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-263">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="5fea7-264">**서버의 허브 클래스**</span><span class="sxs-lookup"><span data-stu-id="5fea7-264">**Hub class on server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

<span data-ttu-id="5fea7-265">**허브에 대해 생성 된 클라이언트 프록시에 대 한 참조 가져오기**</span><span class="sxs-lookup"><span data-stu-id="5fea7-265">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample24.js?highlight=1)]

<span data-ttu-id="5fea7-266">**프록시를 생성 하지 않고 허브 클래스에 대 한 클라이언트 프록시를 만듭니다.**</span><span class="sxs-lookup"><span data-stu-id="5fea7-266">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="5fea7-267">`HubName` 특성을 사용 하 여 허브 클래스를 데코레이팅하는 경우 대/소문자를 변경 하지 않고 정확한 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-267">If you decorate your Hub class with a `HubName` attribute, use the exact name without changing case.</span></span>

<span data-ttu-id="5fea7-268">**HubName 특성이 있는 서버의 허브 클래스**</span><span class="sxs-lookup"><span data-stu-id="5fea7-268">**Hub class on server with HubName attribute**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="5fea7-269">**허브에 대해 생성 된 클라이언트 프록시에 대 한 참조 가져오기**</span><span class="sxs-lookup"><span data-stu-id="5fea7-269">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample27.js?highlight=1)]

<span data-ttu-id="5fea7-270">**프록시를 생성 하지 않고 허브 클래스에 대 한 클라이언트 프록시를 만듭니다.**</span><span class="sxs-lookup"><span data-stu-id="5fea7-270">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample28.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="5fea7-271">서버에서 호출할 수 있는 클라이언트에서 메서드를 정의 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5fea7-271">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="5fea7-272">서버에서 허브를 통해 호출할 수 있는 메서드를 정의 하려면 생성 된 프록시의 `client` 속성을 사용 하 여 허브 프록시에 이벤트 처리기를 추가 하거나 생성 된 프록시를 사용 하지 않는 경우 `on` 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-272">To define a method that the server can call from a Hub, add an event handler to the Hub proxy by using the `client` property of the generated proxy, or call the `on` method if you aren't using the generated proxy.</span></span> <span data-ttu-id="5fea7-273">매개 변수는 복잡 한 개체 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-273">The parameters can be complex objects.</span></span>

<span data-ttu-id="5fea7-274">`start` 메서드를 호출 하기 전에 이벤트 처리기를 추가 하 여 연결을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-274">Add the event handler before you call the `start` method to establish the connection.</span></span> <span data-ttu-id="5fea7-275">`start` 메서드를 호출한 후 이벤트 처리기를 추가 하려면이 문서의 앞부분에서 [연결을 설정](#establishconnection) 하는 방법의 참고를 참조 하 고, 생성 된 프록시를 사용 하지 않고 메서드를 정의 하는 데 표시 된 구문을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-275">(If you want to add event handlers after calling the `start` method, see the note in [How to establish a connection](#establishconnection) earlier in this document, and use the syntax shown for defining a method without using the generated proxy.)</span></span>

<span data-ttu-id="5fea7-276">메서드 이름 일치는 대/소문자를 구분 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-276">Method name matching is case-insensitive.</span></span> <span data-ttu-id="5fea7-277">예를 들어 서버의 `Clients.All.addContosoChatMessageToPage`은 클라이언트에서 `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`또는 `addcontosochatmessagetopage`를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-277">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`, or `addcontosochatmessagetopage` on the client.</span></span>

<span data-ttu-id="5fea7-278">**클라이언트에서 메서드 정의 (생성 된 프록시 포함)**</span><span class="sxs-lookup"><span data-stu-id="5fea7-278">**Define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample29.js?highlight=2)]

<span data-ttu-id="5fea7-279">**클라이언트에서 메서드를 정의 하는 다른 방법 (생성 된 프록시 포함)**</span><span class="sxs-lookup"><span data-stu-id="5fea7-279">**Alternate way to define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample30.js?highlight=1-2)]

<span data-ttu-id="5fea7-280">**클라이언트에서 메서드를 정의 합니다 (생성 된 프록시를 사용 하지 않거나 시작 메서드를 호출한 후 추가 하는 경우).**</span><span class="sxs-lookup"><span data-stu-id="5fea7-280">**Define method on client (without the generated proxy, or when adding after calling the start method)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample31.js?highlight=3)]

<span data-ttu-id="5fea7-281">**클라이언트 메서드를 호출 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="5fea7-281">**Server code that calls the client method**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample32.cs?highlight=5)]

<span data-ttu-id="5fea7-282">다음 예제에서는 복합 개체를 메서드 매개 변수로 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-282">The following examples include a complex object as a method parameter.</span></span>

<span data-ttu-id="5fea7-283">**클라이언트에서 생성 된 프록시를 사용 하 여 복잡 한 개체를 사용 하는 메서드를 정의 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5fea7-283">**Define method on client that takes a complex object (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample33.js?highlight=2-3)]

<span data-ttu-id="5fea7-284">**클라이언트에서 생성 된 프록시 없이 복잡 한 개체를 사용 하는 메서드를 정의 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5fea7-284">**Define method on client that takes a complex object (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample34.js?highlight=3-4)]

<span data-ttu-id="5fea7-285">**복합 개체를 정의 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="5fea7-285">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="5fea7-286">**복합 개체를 사용 하 여 클라이언트 메서드를 호출 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="5fea7-286">**Server code that calls the client method using a complex object**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample36.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="5fea7-287">클라이언트에서 서버 메서드를 호출 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5fea7-287">How to call server methods from the client</span></span>

<span data-ttu-id="5fea7-288">클라이언트에서 서버 메서드를 호출 하려면 생성 된 프록시를 사용 하지 않는 경우 생성 된 프록시의 `server` 속성 또는 허브 프록시의 `invoke` 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-288">To call a server method from the client, use the `server` property of the generated proxy or the `invoke` method on the Hub proxy if you aren't using the generated proxy.</span></span> <span data-ttu-id="5fea7-289">반환 값 또는 매개 변수는 복잡 한 개체 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-289">The return value or parameters can be complex objects.</span></span>

<span data-ttu-id="5fea7-290">허브에 있는 메서드 이름의 카멜식 대/소문자 버전을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-290">Pass in a camel-case version of the method name on the Hub.</span></span> <span data-ttu-id="5fea7-291">SignalR는 JavaScript 코드가 JavaScript 규칙을 준수할 수 있도록 이러한 변경을 자동으로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-291">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="5fea7-292">다음 예에서는 반환 값이 없는 서버 메서드를 호출 하는 방법과 반환 값이 있는 서버 메서드를 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-292">The following examples show how to call a server method that doesn't have a return value and how to call a server method that does have a return value.</span></span>

<span data-ttu-id="5fea7-293">**HubMethodName 특성이 없는 서버 메서드**</span><span class="sxs-lookup"><span data-stu-id="5fea7-293">**Server method with no HubMethodName attribute**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample37.cs?highlight=3)]

<span data-ttu-id="5fea7-294">**매개 변수에 전달 된 복합 개체를 정의 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="5fea7-294">**Server code that defines the complex object passed in a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample38.cs)]

<span data-ttu-id="5fea7-295">**생성 된 프록시를 사용 하 여 서버 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="5fea7-295">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample39.js?highlight=1)]

<span data-ttu-id="5fea7-296">**생성 된 프록시를 사용 하지 않고 서버 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="5fea7-296">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

<span data-ttu-id="5fea7-297">`HubMethodName` 특성을 사용 하 여 허브 메서드를 데코레이팅하는 경우에는 대/소문자를 변경 하지 않고 해당 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-297">If you decorated the Hub method with a `HubMethodName` attribute, use that name without changing case.</span></span>

<span data-ttu-id="5fea7-298">HubMethodName 특성이 있는 **서버 메서드**</span><span class="sxs-lookup"><span data-stu-id="5fea7-298">**Server method** with a HubMethodName attribute</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample41.cs?highlight=3)]

<span data-ttu-id="5fea7-299">**생성 된 프록시를 사용 하 여 서버 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="5fea7-299">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample42.js?highlight=1)]

<span data-ttu-id="5fea7-300">**생성 된 프록시를 사용 하지 않고 서버 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="5fea7-300">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample43.js?highlight=1)]

<span data-ttu-id="5fea7-301">앞의 예제에서는 반환 값이 없는 서버 메서드를 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-301">The preceding examples show how to call a server method that has no return value.</span></span> <span data-ttu-id="5fea7-302">다음 예에서는 반환 값이 있는 서버 메서드를 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-302">The following examples show how to call a server method that has a return value.</span></span>

<span data-ttu-id="5fea7-303">**반환 값을 포함 하는 메서드의 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="5fea7-303">**Server code for a method that has a return value**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample44.cs?highlight=3)]

<span data-ttu-id="5fea7-304">반환 값 **에 사용 되는 스톡 클래스입니다** .</span><span class="sxs-lookup"><span data-stu-id="5fea7-304">**The Stock class used for the** return value</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample45.cs?highlight=1)]

<span data-ttu-id="5fea7-305">**생성 된 프록시를 사용 하 여 서버 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="5fea7-305">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample46.js?highlight=2,4-5)]

<span data-ttu-id="5fea7-306">**생성 된 프록시를 사용 하지 않고 서버 메서드를 호출 하는 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="5fea7-306">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample47.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="5fea7-307">연결 수명 이벤트를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5fea7-307">How to handle connection lifetime events</span></span>

<span data-ttu-id="5fea7-308">SignalR는 처리할 수 있는 다음 연결 수명 이벤트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-308">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="5fea7-309">`starting`: 연결을 통해 데이터를 보내기 전에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-309">`starting`: Raised before any data is sent over the connection.</span></span>
- <span data-ttu-id="5fea7-310">`received`: 연결에서 데이터를 받을 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-310">`received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="5fea7-311">받은 데이터를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-311">Provides the received data.</span></span>
- <span data-ttu-id="5fea7-312">`connectionSlow`: 클라이언트에서 느리거나 자주 삭제 되는 연결을 검색할 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-312">`connectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="5fea7-313">`reconnecting`: 기본 전송에서 다시 연결을 시작할 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-313">`reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="5fea7-314">`reconnected`: 기본 전송이 다시 연결 되었을 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-314">`reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="5fea7-315">`stateChanged`: 연결 상태가 변경 될 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-315">`stateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="5fea7-316">이전 상태와 새 상태 (연결, 연결, 다시 연결 또는 연결 끊김)를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-316">Provides the old state and the new state (Connecting, Connected, Reconnecting, or Disconnected).</span></span>
- <span data-ttu-id="5fea7-317">`disconnected`: 연결의 연결이 끊어지면 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-317">`disconnected`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="5fea7-318">예를 들어, 눈에 띄는 지연을 일으킬 수 있는 연결 문제가 있을 때 경고 메시지를 표시 하려면 `connectionSlow` 이벤트를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-318">For example, if you want to display warning messages when there are connection problems that might cause noticeable delays, handle the `connectionSlow` event.</span></span>

<span data-ttu-id="5fea7-319">**생성 된 프록시를 사용 하 여 connectionSlow 이벤트를 처리 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5fea7-319">**Handle the connectionSlow event (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample48.js?highlight=1)]

<span data-ttu-id="5fea7-320">**생성 된 프록시를 사용 하지 않고 connectionSlow 이벤트를 처리 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5fea7-320">**Handle the connectionSlow event (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample49.js?highlight=2)]

<span data-ttu-id="5fea7-321">자세한 내용은 [SignalR의 연결 수명 이벤트 이해 및 처리](index.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5fea7-321">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](index.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="5fea7-322">오류를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5fea7-322">How to handle errors</span></span>

<span data-ttu-id="5fea7-323">SignalR JavaScript 클라이언트는에 대 한 처리기를 추가할 수 있는 `error` 이벤트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-323">The SignalR JavaScript client provides an `error` event that you can add a handler for.</span></span> <span data-ttu-id="5fea7-324">또한 fail 메서드를 사용 하 여 서버 메서드 호출로 인해 발생 하는 오류에 대 한 처리기를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-324">You can also use the fail method to add a handler for errors that result from a server method invocation.</span></span>

<span data-ttu-id="5fea7-325">서버에서 자세한 오류 메시지를 명시적으로 사용 하도록 설정 하지 않은 경우 오류 발생 후 SignalR에서 반환 하는 예외 개체는 오류에 대 한 최소 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-325">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="5fea7-326">예를`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`들어 `newContosoChatMessage`에 대 한 호출이 실패 하면 오류 개체의 오류 메시지에는 보안을 위해 프로덕션 환경에서 클라이언트에 자세한 오류 메시지를 보내는 것이 권장 되지 않습니다. 그러나 문제 해결을 위해 자세한 오류 메시지를 사용 하려면 서버에서 다음 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-326">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample50.cs?highlight=2)]

<span data-ttu-id="5fea7-327">다음 예제에서는 오류 이벤트에 대 한 처리기를 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-327">The following example shows how to add a handler for the error event.</span></span>

<span data-ttu-id="5fea7-328">**생성 된 프록시를 사용 하 여 오류 처리기 추가**</span><span class="sxs-lookup"><span data-stu-id="5fea7-328">**Add an error handler (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample51.js?highlight=1)]

<span data-ttu-id="5fea7-329">**생성 된 프록시를 사용 하지 않고 오류 처리기 추가**</span><span class="sxs-lookup"><span data-stu-id="5fea7-329">**Add an error handler (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

<span data-ttu-id="5fea7-330">다음 예제에서는 메서드 호출에서 오류를 처리 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-330">The following example shows how to handle an error from a method invocation.</span></span>

<span data-ttu-id="5fea7-331">**생성 된 프록시를 사용 하 여 메서드 호출에서 오류를 처리 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5fea7-331">**Handle an error from a method invocation (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample53.js?highlight=2)]

<span data-ttu-id="5fea7-332">**생성 된 프록시를 사용 하지 않고 메서드 호출에서 오류를 처리 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5fea7-332">**Handle an error from a method invocation (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

<span data-ttu-id="5fea7-333">메서드 호출에 실패 하면 `error` 이벤트도 발생 하므로 `error` 메서드 처리기 및 `.fail` 메서드 콜백에서 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-333">If a method invocation fails, the `error` event is also raised, so your code in the `error` method handler and in the `.fail` method callback would execute.</span></span>

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="5fea7-334">클라이언트 쪽 로깅을 사용 하도록 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5fea7-334">How to enable client-side logging</span></span>

<span data-ttu-id="5fea7-335">연결에 대 한 클라이언트 쪽 로깅을 사용 하도록 설정 하려면 연결 개체에 대 한 `logging` 속성을 설정 하 여 연결을 설정 하기 전에 `start` 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea7-335">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="5fea7-336">**생성 된 프록시를 사용 하 여 로깅 사용**</span><span class="sxs-lookup"><span data-stu-id="5fea7-336">**Enable logging (with the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample55.js?highlight=1)]

<span data-ttu-id="5fea7-337">**로깅 사용 (생성 된 프록시 제외)**</span><span class="sxs-lookup"><span data-stu-id="5fea7-337">**Enable logging (without the generated proxy)**</span></span>

[!code-javascript[Main](signalr-1x-hubs-api-guide-javascript-client/samples/sample56.js?highlight=2)]

<span data-ttu-id="5fea7-338">로그를 보려면 브라우저의 개발자 도구를 열고 콘솔 탭으로 이동 합니다. 이 작업을 수행 하는 방법을 보여 주는 단계별 지침 및 스크린 샷을 보여 주는 자습서는 ASP.NET Signalr를 사용 하 [여 서버 브로드캐스트-로깅 사용](index.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5fea7-338">To see the logs, open your browser's developer tools and go to the Console tab. For a tutorial that shows step-by-step instructions and screen shots that show how to do this, see [Server Broadcast with ASP.NET Signalr - Enable Logging](index.md).</span></span>
