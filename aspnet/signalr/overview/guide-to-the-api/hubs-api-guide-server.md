---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-server
title: ASP.NET SignalR Hubs API 가이드-Server (C#) | Microsoft Docs
author: bradygaster
description: 이 문서에서는 SignalR 버전 2 용 ASP.NET SignalR Hubs API의 서버 쪽 프로그래밍에 대해 소개 하 고, 코드 샘플을 보여 줍니다.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: b19913e5-cd8a-4e4b-a872-5ac7a858a934
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: c681b104b15bfc4a04587c7abf685dcf20def2ca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431369"
---
# <a name="aspnet-signalr-hubs-api-guide---server-c"></a><span data-ttu-id="bebbc-103">ASP.NET SignalR Hubs API 가이드-서버 (C#)</span><span class="sxs-lookup"><span data-stu-id="bebbc-103">ASP.NET SignalR Hubs API Guide - Server (C#)</span></span>

<span data-ttu-id="bebbc-104">[Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="bebbc-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="bebbc-105">이 문서에서는 일반적인 옵션을 보여 주는 코드 샘플을 사용 하 여 SignalR 버전 2 용 ASP.NET SignalR Hubs API의 서버 쪽 프로그래밍에 대 한 소개를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-105">This document provides an introduction to programming the server side of the ASP.NET SignalR Hubs API for SignalR version 2, with code samples demonstrating common options.</span></span>
> 
> <span data-ttu-id="bebbc-106">SignalR Hubs API를 사용 하면 서버에서 연결 된 클라이언트로 또는 클라이언트에서 서버로 Rpc (원격 프로시저 호출)를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="bebbc-107">서버 코드에서는 클라이언트에서 호출할 수 있는 메서드를 정의 하 고 클라이언트에서 실행 되는 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="bebbc-108">클라이언트 코드에서는 서버에서 호출할 수 있는 메서드를 정의 하 고 서버에서 실행 되는 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="bebbc-109">SignalR는 모든 클라이언트에서 서버로의 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="bebbc-110">또한 SignalR는 영구 연결 이라고 하는 하위 수준 API를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="bebbc-111">SignalR, 허브 및 영구 연결에 대 한 소개는 [SignalR 2 소개](../getting-started/introduction-to-signalr.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="bebbc-111">For an introduction to SignalR, Hubs, and Persistent Connections, see [Introduction to SignalR 2](../getting-started/introduction-to-signalr.md).</span></span>
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="bebbc-112">이 항목에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="bebbc-112">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="bebbc-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="bebbc-113">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="bebbc-114">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="bebbc-114">.NET 4.5</span></span>
> - <span data-ttu-id="bebbc-115">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="bebbc-115">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="topic-versions"></a><span data-ttu-id="bebbc-116">토픽 버전</span><span class="sxs-lookup"><span data-stu-id="bebbc-116">Topic versions</span></span>
> 
> <span data-ttu-id="bebbc-117">이전 버전의 SignalR에 대 한 자세한 내용은 [SignalR 이전 버전](../older-versions/index.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="bebbc-117">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="bebbc-118">질문 및 설명</span><span class="sxs-lookup"><span data-stu-id="bebbc-118">Questions and comments</span></span>
> 
> <span data-ttu-id="bebbc-119">이 자습서와 페이지 맨 아래에 있는 의견에서 개선할 수 있는 방법에 대 한 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="bebbc-119">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="bebbc-120">자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-120">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="bebbc-121">개요</span><span class="sxs-lookup"><span data-stu-id="bebbc-121">Overview</span></span>

<span data-ttu-id="bebbc-122">이 문서는 다음 섹션으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-122">This document contains the following sections:</span></span>

- [<span data-ttu-id="bebbc-123">SignalR 미들웨어를 등록 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bebbc-123">How to register SignalR middleware</span></span>](#route)

    - [<span data-ttu-id="bebbc-124">/Signalr URL</span><span class="sxs-lookup"><span data-stu-id="bebbc-124">The /signalr URL</span></span>](#signalrurl)
    - [<span data-ttu-id="bebbc-125">SignalR 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="bebbc-125">Configuring SignalR options</span></span>](#options)
- [<span data-ttu-id="bebbc-126">허브 클래스를 만들고 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bebbc-126">How to create and use Hub classes</span></span>](#hubclass)

    - [<span data-ttu-id="bebbc-127">허브 개체 수명</span><span class="sxs-lookup"><span data-stu-id="bebbc-127">Hub object lifetime</span></span>](#transience)
    - [<span data-ttu-id="bebbc-128">카멜식-JavaScript 클라이언트에서 허브 이름의 대/소문자 구분</span><span class="sxs-lookup"><span data-stu-id="bebbc-128">Camel-casing of Hub names in JavaScript clients</span></span>](#hubnames)
    - [<span data-ttu-id="bebbc-129">여러 허브</span><span class="sxs-lookup"><span data-stu-id="bebbc-129">Multiple Hubs</span></span>](#multiplehubs)
    - [<span data-ttu-id="bebbc-130">강력한 형식의 허브</span><span class="sxs-lookup"><span data-stu-id="bebbc-130">Strongly-Typed Hubs</span></span>](#stronglytypedhubs)
- [<span data-ttu-id="bebbc-131">클라이언트가 호출할 수 있는 허브 클래스에서 메서드를 정의 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bebbc-131">How to define methods in the Hub class that clients can call</span></span>](#hubmethods)

    - [<span data-ttu-id="bebbc-132">카멜식-JavaScript 클라이언트에서 메서드 이름의 대/소문자 구분</span><span class="sxs-lookup"><span data-stu-id="bebbc-132">Camel-casing of method names in JavaScript clients</span></span>](#methodnames)
    - [<span data-ttu-id="bebbc-133">비동기적으로 실행 하는 경우</span><span class="sxs-lookup"><span data-stu-id="bebbc-133">When to execute asynchronously</span></span>](#asyncmethods)
    - [<span data-ttu-id="bebbc-134">오버 로드 정의</span><span class="sxs-lookup"><span data-stu-id="bebbc-134">Defining overloads</span></span>](#overloads)
    - [<span data-ttu-id="bebbc-135">허브 메서드 호출의 진행률 보고</span><span class="sxs-lookup"><span data-stu-id="bebbc-135">Reporting progress from hub method invocations</span></span>](#progress)
- [<span data-ttu-id="bebbc-136">허브 클래스에서 클라이언트 메서드를 호출 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bebbc-136">How to call client methods from the Hub class</span></span>](#callfromhub)

    - [<span data-ttu-id="bebbc-137">RPC를 수신 하는 클라이언트 선택</span><span class="sxs-lookup"><span data-stu-id="bebbc-137">Selecting which clients will receive the RPC</span></span>](#selectingclients)
    - [<span data-ttu-id="bebbc-138">메서드 이름에 대 한 컴파일 타임 유효성 검사 없음</span><span class="sxs-lookup"><span data-stu-id="bebbc-138">No compile-time validation for method names</span></span>](#dynamicmethodnames)
    - [<span data-ttu-id="bebbc-139">대/소문자를 구분 하지 않는 메서드 이름 일치</span><span class="sxs-lookup"><span data-stu-id="bebbc-139">Case-insensitive method name matching</span></span>](#caseinsensitive)
    - [<span data-ttu-id="bebbc-140">비동기 실행</span><span class="sxs-lookup"><span data-stu-id="bebbc-140">Asynchronous execution</span></span>](#asyncclient)
- [<span data-ttu-id="bebbc-141">허브 클래스에서 그룹 멤버 자격을 관리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bebbc-141">How to manage group membership from the Hub class</span></span>](#groupsfromhub)

    - [<span data-ttu-id="bebbc-142">Add 및 Remove 메서드의 비동기 실행</span><span class="sxs-lookup"><span data-stu-id="bebbc-142">Asynchronous execution of Add and Remove methods</span></span>](#asyncgroupmethods)
    - [<span data-ttu-id="bebbc-143">그룹 멤버 자격 지 속성</span><span class="sxs-lookup"><span data-stu-id="bebbc-143">Group membership persistence</span></span>](#grouppersistence)
    - [<span data-ttu-id="bebbc-144">단일 사용자 그룹</span><span class="sxs-lookup"><span data-stu-id="bebbc-144">Single-user groups</span></span>](#singleusergroups)
- [<span data-ttu-id="bebbc-145">허브 클래스에서 연결 수명 이벤트를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bebbc-145">How to handle connection lifetime events in the Hub class</span></span>](#connectionlifetime)

    - [<span data-ttu-id="bebbc-146">OnConnected, Onconnected 및 Onconnected가 호출 되는 경우</span><span class="sxs-lookup"><span data-stu-id="bebbc-146">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>](#onreconnected)
    - [<span data-ttu-id="bebbc-147">호출자 상태가 채워지지 않음</span><span class="sxs-lookup"><span data-stu-id="bebbc-147">Caller state not populated</span></span>](#nocallerstate)
- [<span data-ttu-id="bebbc-148">컨텍스트 속성에서 클라이언트에 대 한 정보를 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="bebbc-148">How to get information about the client from the Context property</span></span>](#contextproperty)
- [<span data-ttu-id="bebbc-149">클라이언트와 허브 클래스 간의 상태를 전달 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bebbc-149">How to pass state between clients and the Hub class</span></span>](#passstate)
- [<span data-ttu-id="bebbc-150">허브 클래스에서 오류를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bebbc-150">How to handle errors in the Hub class</span></span>](#handleErrors)
- [<span data-ttu-id="bebbc-151">허브 클래스 외부에서 클라이언트 메서드를 호출 하 고 그룹을 관리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bebbc-151">How to call client methods and manage groups from outside the Hub class</span></span>](#callfromoutsidehub)

    - [<span data-ttu-id="bebbc-152">클라이언트 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="bebbc-152">Calling client methods</span></span>](#callingclientsoutsidehub)
    - [<span data-ttu-id="bebbc-153">그룹 멤버 자격 관리</span><span class="sxs-lookup"><span data-stu-id="bebbc-153">Managing group membership</span></span>](#managinggroupsoutsidehub)
- [<span data-ttu-id="bebbc-154">추적을 사용 하도록 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bebbc-154">How to enable tracing</span></span>](#tracing)
- [<span data-ttu-id="bebbc-155">허브 파이프라인을 사용자 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bebbc-155">How to customize the Hubs pipeline</span></span>](#hubpipeline)

<span data-ttu-id="bebbc-156">클라이언트를 프로그래밍 하는 방법에 대 한 설명서는 다음 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="bebbc-156">For documentation on how to program clients, see the following resources:</span></span>

- [<span data-ttu-id="bebbc-157">SignalR Hubs API 가이드-JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="bebbc-157">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)
- [<span data-ttu-id="bebbc-158">SignalR Hubs API 가이드-.NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="bebbc-158">SignalR Hubs API Guide - .NET Client</span></span>](hubs-api-guide-net-client.md)

<span data-ttu-id="bebbc-159">SignalR 2 용 서버 구성 요소는 .NET 4.5 에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-159">The server components for SignalR 2 are only available in .NET 4.5.</span></span> <span data-ttu-id="bebbc-160">.NET 4.0를 실행 하는 서버는 SignalR v1. x를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-160">Servers running .NET 4.0 must use SignalR v1.x.</span></span>

<a id="route"></a>

## <a name="how-to-register-signalr-middleware"></a><span data-ttu-id="bebbc-161">SignalR 미들웨어를 등록 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bebbc-161">How to register SignalR middleware</span></span>

<span data-ttu-id="bebbc-162">클라이언트가 허브에 연결 하는 데 사용 하는 경로를 정의 하려면 응용 프로그램이 시작 될 때 `MapSignalR` 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-162">To define the route that clients will use to connect to your Hub, call the `MapSignalR` method when the application starts.</span></span> <span data-ttu-id="bebbc-163">`MapSignalR`은 `OwinExtensions` 클래스에 대 한 [확장 메서드입니다](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) .</span><span class="sxs-lookup"><span data-stu-id="bebbc-163">`MapSignalR` is an [extension method](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) for the `OwinExtensions` class.</span></span> <span data-ttu-id="bebbc-164">다음 예제에서는 OWIN startup 클래스를 사용 하 여 SignalR Hubs 경로를 정의 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-164">The following example shows how to define the SignalR Hubs route using an OWIN startup class.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample1.cs)]

<span data-ttu-id="bebbc-165">SignalR 기능을 ASP.NET MVC 응용 프로그램에 추가 하는 경우 SignalR 경로가 다른 경로 앞에 추가 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-165">If you are adding SignalR functionality to an ASP.NET MVC application, make sure that the SignalR route is added before the other routes.</span></span> <span data-ttu-id="bebbc-166">자세한 내용은 [자습서: SignalR 2 및 MVC 5 시작](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="bebbc-166">For more information, see [Tutorial: Getting Started with SignalR 2 and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a><span data-ttu-id="bebbc-167">/Signalr URL</span><span class="sxs-lookup"><span data-stu-id="bebbc-167">The /signalr URL</span></span>

<span data-ttu-id="bebbc-168">기본적으로 클라이언트에서 허브에 연결 하는 데 사용할 경로 URL은 "/signalr"입니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-168">By default, the route URL which clients will use to connect to your Hub is "/signalr".</span></span> <span data-ttu-id="bebbc-169">이 URL은 자동으로 생성 된 JavaScript 파일에 대 한 "/signalr/hubs" URL과 혼동 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="bebbc-169">(Don't confuse this URL with the "/signalr/hubs" URL, which is for the automatically generated JavaScript file.</span></span> <span data-ttu-id="bebbc-170">생성 된 프록시에 대 한 자세한 내용은 [SignalR HUBS API 가이드-JavaScript 클라이언트-생성 된 프록시와 사용자를 위해 수행](hubs-api-guide-javascript-client.md#genproxy)하는 작업을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="bebbc-170">For more information about the generated proxy, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).)</span></span>

<span data-ttu-id="bebbc-171">SignalR에 대해이 기본 URL을 사용할 수 없도록 하는 특별 한 상황이 있을 수 있습니다. 예를 들어 프로젝트에 이름이 *signalr* 인 폴더가 있으며 이름을 변경 하지 않으려는 경우</span><span class="sxs-lookup"><span data-stu-id="bebbc-171">There might be extraordinary circumstances that make this base URL not usable for SignalR; for example, you have a folder in your project named *signalr* and you don't want to change the name.</span></span> <span data-ttu-id="bebbc-172">이 경우 다음 예제와 같이 기준 URL을 변경할 수 있습니다 (샘플 코드에서 "/signalr"을 원하는 URL로 바꿉니다).</span><span class="sxs-lookup"><span data-stu-id="bebbc-172">In that case, you can change the base URL, as shown in the following examples (replace "/signalr" in the sample code with your desired URL).</span></span>

<span data-ttu-id="bebbc-173">**URL을 지정 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="bebbc-173">**Server code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample2.cs?highlight=1)]

<span data-ttu-id="bebbc-174">**생성 된 프록시를 사용 하 여 URL을 지정 하는 JavaScript 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="bebbc-174">**JavaScript client code that specifies the URL (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample3.js?highlight=1)]

<span data-ttu-id="bebbc-175">**생성 된 프록시 없이 URL을 지정 하는 JavaScript 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="bebbc-175">**JavaScript client code that specifies the URL (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample4.js?highlight=1)]

<span data-ttu-id="bebbc-176">**URL을 지정 하는 .NET 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="bebbc-176">**.NET client code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample5.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a><span data-ttu-id="bebbc-177">SignalR 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="bebbc-177">Configuring SignalR Options</span></span>

<span data-ttu-id="bebbc-178">`MapSignalR` 메서드의 오버 로드를 사용 하 여 사용자 지정 URL, 사용자 지정 종속성 해결 프로그램 및 다음 옵션을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-178">Overloads of the `MapSignalR` method enable you to specify a custom URL, a custom dependency resolver, and the following options:</span></span>

- <span data-ttu-id="bebbc-179">브라우저 클라이언트에서 CORS 또는 JSONP를 사용 하 여 도메인 간 호출을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-179">Enable cross-domain calls using CORS or JSONP from browser clients.</span></span>

    <span data-ttu-id="bebbc-180">일반적으로 브라우저에서 `http://contoso.com`의 페이지를 로드 하는 경우에는 `http://contoso.com/signalr`에서 SignalR 연결이 동일한 도메인에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-180">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="bebbc-181">`http://contoso.com` 페이지에서 `http://fabrikam.com/signalr`에 연결 하는 경우에는 도메인 간 연결을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-181">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="bebbc-182">보안상의 이유로 도메인 간 연결은 기본적으로 사용 하지 않도록 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-182">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="bebbc-183">자세한 내용은 [ASP.NET SignalR HUBS API 가이드-JavaScript 클라이언트-도메인 간 연결을 설정 하는 방법](hubs-api-guide-javascript-client.md#crossdomain)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="bebbc-183">For more information, see [ASP.NET SignalR Hubs API Guide - JavaScript Client - How to establish a cross-domain connection](hubs-api-guide-javascript-client.md#crossdomain).</span></span>
- <span data-ttu-id="bebbc-184">자세한 오류 메시지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-184">Enable detailed error messages.</span></span>

    <span data-ttu-id="bebbc-185">오류가 발생 하는 경우 SignalR의 기본 동작은 클라이언트에 알림 메시지를 전송 하 여 발생 한 상황에 대 한 세부 정보를 제공 하지 않는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-185">When errors occur, the default behavior of SignalR is to send to clients a notification message without details about what happened.</span></span> <span data-ttu-id="bebbc-186">악의적인 사용자가 응용 프로그램에 대 한 공격 정보를 사용할 수 있기 때문에 클라이언트에 자세한 오류 정보를 보내는 것은 프로덕션 환경에서 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-186">Sending detailed error information to clients is not recommended in production, because malicious users might be able to use the information in attacks against your application.</span></span> <span data-ttu-id="bebbc-187">문제를 해결 하려면이 옵션을 사용 하 여 더 많은 정보를 제공 하는 오류 보고를 일시적으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-187">For troubleshooting, you can use this option to temporarily enable more informative error reporting.</span></span>
- <span data-ttu-id="bebbc-188">자동으로 생성 된 JavaScript 프록시 파일을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-188">Disable automatically generated JavaScript proxy files.</span></span>

    <span data-ttu-id="bebbc-189">기본적으로 허브 클래스에 대 한 프록시를 포함 하는 JavaScript 파일은 URL "/signalr/hubs"에 대 한 응답으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-189">By default, a JavaScript file with proxies for your Hub classes is generated in response to the URL "/signalr/hubs".</span></span> <span data-ttu-id="bebbc-190">JavaScript 프록시를 사용 하지 않으려는 경우 또는이 파일을 수동으로 생성 하 고 클라이언트의 물리적 파일을 참조 하려는 경우이 옵션을 사용 하 여 프록시 생성을 사용 하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-190">If you don't want to use the JavaScript proxies, or if you want to generate this file manually and refer to a physical file in your clients, you can use this option to disable proxy generation.</span></span> <span data-ttu-id="bebbc-191">자세한 내용은 [SignalR HUBS API 가이드-JavaScript 클라이언트-SignalR 생성 프록시에 대 한 물리적 파일을 만드는 방법](hubs-api-guide-javascript-client.md#manualproxy)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="bebbc-191">For more information, see [SignalR Hubs API Guide - JavaScript Client - How to create a physical file for the SignalR generated proxy](hubs-api-guide-javascript-client.md#manualproxy).</span></span>

<span data-ttu-id="bebbc-192">다음 예제에서는 `MapSignalR` 메서드에 대 한 호출에서 SignalR 연결 URL 및 이러한 옵션을 지정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-192">The following example shows how to specify the SignalR connection URL and these options in a call to the `MapSignalR` method.</span></span> <span data-ttu-id="bebbc-193">사용자 지정 URL을 지정 하려면 예의 "/signalr"를 사용 하려는 URL로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-193">To specify a custom URL, replace "/signalr" in the example with the URL that you want to use.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample6.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a><span data-ttu-id="bebbc-194">허브 클래스를 만들고 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bebbc-194">How to create and use Hub classes</span></span>

<span data-ttu-id="bebbc-195">허브를 만들려면 [Signalr](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)에서 파생 되는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-195">To create a Hub, create a class that derives from [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span></span> <span data-ttu-id="bebbc-196">다음 예제에서는 채팅 응용 프로그램에 대 한 간단한 허브 클래스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-196">The following example shows a simple Hub class for a chat application.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample7.cs)]

<span data-ttu-id="bebbc-197">이 예제에서 연결 된 클라이언트는 `NewContosoChatMessage` 메서드를 호출할 수 있으며, 수신 된 데이터는 연결 된 모든 클라이언트에 브로드캐스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-197">In this example, a connected client can call the `NewContosoChatMessage` method, and when it does, the data received is broadcasted to all connected clients.</span></span>

<a id="transience"></a>

### <a name="hub-object-lifetime"></a><span data-ttu-id="bebbc-198">허브 개체 수명</span><span class="sxs-lookup"><span data-stu-id="bebbc-198">Hub object lifetime</span></span>

<span data-ttu-id="bebbc-199">서버에서 허브 클래스를 인스턴스화하거나 사용자의 코드에서 해당 메서드를 호출 하지 않습니다. 모든 작업은 SignalR Hubs 파이프라인에서 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-199">You don't instantiate the Hub class or call its methods from your own code on the server; all that is done for you by the SignalR Hubs pipeline.</span></span> <span data-ttu-id="bebbc-200">SignalR는 클라이언트가 서버에 연결, 연결 끊기 또는 메서드 호출을 수행 하는 경우와 같은 허브 작업을 처리 해야 할 때마다 허브 클래스의 새 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-200">SignalR creates a new instance of your Hub class each time it needs to handle a Hub operation such as when a client connects, disconnects, or makes a method call to the server.</span></span>

<span data-ttu-id="bebbc-201">허브 클래스의 인스턴스는 일시적 이므로이를 사용 하 여 하나의 메서드 호출에서 다음으로 상태를 유지할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-201">Because instances of the Hub class are transient, you can't use them to maintain state from one method call to the next.</span></span> <span data-ttu-id="bebbc-202">서버가 클라이언트에서 메서드 호출을 받을 때마다 허브 클래스의 새 인스턴스가 메시지를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-202">Each time the server receives a method call from a client, a new instance of your Hub class processes the message.</span></span> <span data-ttu-id="bebbc-203">여러 연결 및 메서드 호출을 통해 상태를 유지 하려면 데이터베이스, 허브 클래스의 정적 변수 또는 `Hub`에서 파생 되지 않은 다른 클래스와 같은 다른 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-203">To maintain state through multiple connections and method calls, use some other method such as a database, or a static variable on the Hub class, or a different class that does not derive from `Hub`.</span></span> <span data-ttu-id="bebbc-204">허브 클래스에서 정적 변수와 같은 메서드를 사용 하 여 메모리에 데이터를 저장 하는 경우 응용 프로그램 도메인이 재활용 되 면 데이터가 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-204">If you persist data in memory, using a method such as a static variable on the Hub class, the data will be lost when the app domain recycles.</span></span>

<span data-ttu-id="bebbc-205">허브 클래스 외부에서 실행 되는 자체 코드에서 클라이언트에 메시지를 보내려는 경우 허브 클래스 인스턴스를 인스턴스화하여 수행할 수 없지만 허브 클래스의 SignalR context 개체에 대 한 참조를 가져오면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-205">If you want to send messages to clients from your own code that runs outside the Hub class, you can't do it by instantiating a Hub class instance, but you can do it by getting a reference to the SignalR context object for your Hub class.</span></span> <span data-ttu-id="bebbc-206">자세한 내용은이 항목의 뒷부분에 나오는 [클라이언트 메서드를 호출 하 고 허브 클래스 외부에서 그룹을 관리 하는 방법](#callfromoutsidehub) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="bebbc-206">For more information, see [How to call client methods and manage groups from outside the Hub class](#callfromoutsidehub) later in this topic.</span></span>

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a><span data-ttu-id="bebbc-207">카멜식-JavaScript 클라이언트에서 허브 이름의 대/소문자 구분</span><span class="sxs-lookup"><span data-stu-id="bebbc-207">Camel-casing of Hub names in JavaScript clients</span></span>

<span data-ttu-id="bebbc-208">기본적으로 JavaScript 클라이언트는 카멜식 대/소문자 버전의 클래스 이름을 사용 하 여 허브를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-208">By default, JavaScript clients refer to Hubs by using a camel-cased version of the class name.</span></span> <span data-ttu-id="bebbc-209">SignalR는 JavaScript 코드가 JavaScript 규칙을 준수할 수 있도록 이러한 변경을 자동으로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-209">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span> <span data-ttu-id="bebbc-210">이전 예제는 JavaScript 코드에서 `contosoChatHub` 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-210">The previous example would be referred to as `contosoChatHub` in JavaScript code.</span></span>

<span data-ttu-id="bebbc-211">**Server**</span><span class="sxs-lookup"><span data-stu-id="bebbc-211">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample8.cs?highlight=1)]

<span data-ttu-id="bebbc-212">**생성 된 프록시를 사용 하는 JavaScript 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="bebbc-212">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample9.js?highlight=1)]

<span data-ttu-id="bebbc-213">클라이언트에서 사용할 다른 이름을 지정 하려면 `HubName` 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-213">If you want to specify a different name for clients to use, add the `HubName` attribute.</span></span> <span data-ttu-id="bebbc-214">`HubName` 특성을 사용 하는 경우 JavaScript 클라이언트에서 카멜식 대/소문자로 이름이 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-214">When you use a `HubName` attribute, there is no name change to camel case on JavaScript clients.</span></span>

<span data-ttu-id="bebbc-215">**Server**</span><span class="sxs-lookup"><span data-stu-id="bebbc-215">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample10.cs?highlight=1)]

<span data-ttu-id="bebbc-216">**생성 된 프록시를 사용 하는 JavaScript 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="bebbc-216">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample11.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a><span data-ttu-id="bebbc-217">여러 허브</span><span class="sxs-lookup"><span data-stu-id="bebbc-217">Multiple Hubs</span></span>

<span data-ttu-id="bebbc-218">응용 프로그램에서 여러 허브 클래스를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-218">You can define multiple Hub classes in an application.</span></span> <span data-ttu-id="bebbc-219">이렇게 하면 연결이 공유 되지만 그룹은 다음과 같이 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-219">When you do that, the connection is shared but groups are separate:</span></span>

- <span data-ttu-id="bebbc-220">모든 클라이언트는 동일한 URL을 사용 하 여 서비스 ("/signalr") 또는 사용자 지정 URL (지정 된 경우)과 SignalR 연결을 설정 하 고, 해당 연결은 서비스에서 정의 된 모든 허브에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-220">All clients will use the same URL to establish a SignalR connection with your service ("/signalr" or your custom URL if you specified one), and that connection is used for all Hubs defined by the service.</span></span>

    <span data-ttu-id="bebbc-221">단일 클래스의 모든 허브 기능을 정의 하는 것과 비교 했을 때 여러 허브에 대 한 성능 차이는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-221">There is no performance difference for multiple Hubs compared to defining all Hub functionality in a single class.</span></span>
- <span data-ttu-id="bebbc-222">모든 허브는 동일한 HTTP 요청 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-222">All Hubs get the same HTTP request information.</span></span>

    <span data-ttu-id="bebbc-223">모든 허브가 동일한 연결을 공유 하므로 서버에서 발생 하는 HTTP 요청 정보는 SignalR 연결을 설정 하는 원래 HTTP 요청에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-223">Since all Hubs share the same connection, the only HTTP request information that the server gets is what comes in the original HTTP request that establishes the SignalR connection.</span></span> <span data-ttu-id="bebbc-224">쿼리 문자열을 지정 하 여 클라이언트에서 서버로 정보를 전달 하는 데 연결 요청을 사용 하는 경우 다른 허브에 다른 쿼리 문자열을 제공할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-224">If you use the connection request to pass information from the client to the server by specifying a query string, you can't provide different query strings to different Hubs.</span></span> <span data-ttu-id="bebbc-225">모든 허브는 동일한 정보를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-225">All Hubs will receive the same information.</span></span>
- <span data-ttu-id="bebbc-226">생성 된 JavaScript 프록시 파일은 한 파일의 모든 허브에 대 한 프록시를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-226">The generated JavaScript proxies file will contain proxies for all Hubs in one file.</span></span>

    <span data-ttu-id="bebbc-227">JavaScript 프록시에 대 한 자세한 내용은 [SignalR HUBS API 가이드-Javascript 클라이언트-생성 된 프록시와 사용자를 위해 수행 하는 작업](hubs-api-guide-javascript-client.md#genproxy)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="bebbc-227">For information about JavaScript proxies, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).</span></span>
- <span data-ttu-id="bebbc-228">그룹은 허브 내에서 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-228">Groups are defined within Hubs.</span></span>

    <span data-ttu-id="bebbc-229">SignalR에서 명명 된 그룹을 정의 하 여 연결 된 클라이언트의 하위 집합에 브로드캐스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-229">In SignalR you can define named groups to broadcast to subsets of connected clients.</span></span> <span data-ttu-id="bebbc-230">그룹은 각 허브에 대해 개별적으로 유지 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-230">Groups are maintained separately for each Hub.</span></span> <span data-ttu-id="bebbc-231">예를 들어 "Administrators" 라는 그룹에는 `ContosoChatHub` 클래스에 대 한 클라이언트 집합이 포함 되며 동일한 그룹 이름은 `StockTickerHub` 클래스에 대해 다른 클라이언트 집합을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-231">For example, a group named "Administrators" would include one set of clients for your `ContosoChatHub` class, and the same group name would refer to a different set of clients for your `StockTickerHub` class.</span></span>

<a id="stronglytypedhubs"></a>
### <a name="strongly-typed-hubs"></a><span data-ttu-id="bebbc-232">강력한 형식의 허브</span><span class="sxs-lookup"><span data-stu-id="bebbc-232">Strongly-Typed Hubs</span></span>

<span data-ttu-id="bebbc-233">클라이언트에서 참조할 수 있는 허브 메서드에 대 한 인터페이스를 정의 하 고 허브 메서드에서 Intellisense를 사용 하도록 설정 하려면 `Hub`이 아니라 `Hub<T>` (SignalR 2.1에 도입 됨)에서 허브를 파생 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-233">To define an interface for your hub methods that your client can reference (and enable Intellisense on your hub methods), derive your hub from `Hub<T>` (introduced in SignalR 2.1) rather than `Hub`:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample12.cs)]

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a><span data-ttu-id="bebbc-234">클라이언트가 호출할 수 있는 허브 클래스에서 메서드를 정의 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bebbc-234">How to define methods in the Hub class that clients can call</span></span>

<span data-ttu-id="bebbc-235">허브의 메서드를 클라이언트에서 호출할 수 있도록 하려면 다음 예제와 같이 public 메서드를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-235">To expose a method on the Hub that you want to be callable from the client, declare a public method, as shown in the following examples.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](hubs-api-guide-server/samples/sample14.cs?highlight=3)]

<span data-ttu-id="bebbc-236">일반적인 C# 메서드와 마찬가지로 복합 형식 및 배열 등을 사용해서 반환 형식과 매개 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-236">You can specify a return type and parameters, including complex types and arrays, as you would in any C# method.</span></span> <span data-ttu-id="bebbc-237">매개 변수로 받거나 호출자에 게 반환 되는 모든 데이터는 JSON을 사용 하 여 클라이언트와 서버 간에 전달 되며 SignalR는 복잡 한 개체의 바인딩과 개체의 배열을 자동으로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-237">Any data that you receive in parameters or return to the caller is communicated between the client and the server by using JSON, and SignalR handles the binding of complex objects and arrays of objects automatically.</span></span>

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a><span data-ttu-id="bebbc-238">카멜식-JavaScript 클라이언트에서 메서드 이름의 대/소문자 구분</span><span class="sxs-lookup"><span data-stu-id="bebbc-238">Camel-casing of method names in JavaScript clients</span></span>

<span data-ttu-id="bebbc-239">기본적으로 JavaScript 클라이언트는 카멜식 대/소문자를 사용 하는 메서드 이름 버전을 사용 하 여 허브 메서드를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-239">By default, JavaScript clients refer to Hub methods by using a camel-cased version of the method name.</span></span> <span data-ttu-id="bebbc-240">SignalR는 JavaScript 코드가 JavaScript 규칙을 준수할 수 있도록 이러한 변경을 자동으로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-240">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="bebbc-241">**Server**</span><span class="sxs-lookup"><span data-stu-id="bebbc-241">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample15.cs?highlight=1)]

<span data-ttu-id="bebbc-242">**생성 된 프록시를 사용 하는 JavaScript 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="bebbc-242">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample16.js?highlight=1)]

<span data-ttu-id="bebbc-243">클라이언트에서 사용할 다른 이름을 지정 하려면 `HubMethodName` 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-243">If you want to specify a different name for clients to use, add the `HubMethodName` attribute.</span></span>

<span data-ttu-id="bebbc-244">**Server**</span><span class="sxs-lookup"><span data-stu-id="bebbc-244">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample17.cs?highlight=1)]

<span data-ttu-id="bebbc-245">**생성 된 프록시를 사용 하는 JavaScript 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="bebbc-245">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a><span data-ttu-id="bebbc-246">비동기적으로 실행 하는 경우</span><span class="sxs-lookup"><span data-stu-id="bebbc-246">When to execute asynchronously</span></span>

<span data-ttu-id="bebbc-247">메서드가 장기 실행 되거나 데이터베이스 조회 또는 웹 서비스 호출과 같이 대기와 관련 된 작업을 수행 해야 하는 경우에는 `void` 반환 형식 대신 [작업](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) 을 반환 하거나 `T` 반환 형식 대신 작업 [&lt;t&gt;](https://msdn.microsoft.com/library/dd321424.aspx) 개체를 반환 하 여 허브 메서드를 비동기식으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-247">If the method will be long-running or has to do work that would involve waiting, such as a database lookup or a web service call, make the Hub method asynchronous by returning a [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (in place of `void` return) or [Task&lt;T&gt;](https://msdn.microsoft.com/library/dd321424.aspx) object (in place of `T` return type).</span></span> <span data-ttu-id="bebbc-248">메서드에서 `Task` 개체를 반환 하는 경우 SignalR는 `Task` 완료 될 때까지 대기한 다음 래핑 해제 된 결과를 클라이언트에 게 다시 보내면 클라이언트에서 메서드 호출을 코딩 하는 방법에는 차이가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-248">When you return a `Task` object from the method, SignalR waits for the `Task` to complete, and then it sends the unwrapped result back to the client, so there is no difference in how you code the method call in the client.</span></span>

<span data-ttu-id="bebbc-249">허브 메서드를 비동기적으로 만들면 WebSocket 전송을 사용할 때 연결 차단이 방지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-249">Making a Hub method asynchronous avoids blocking the connection when it uses the WebSocket transport.</span></span> <span data-ttu-id="bebbc-250">허브 메서드가 동기적으로 실행 되 고 전송이 WebSocket 인 경우 허브 메서드가 완료 될 때까지 동일한 클라이언트에서 허브에 있는 메서드를 이후에 호출 하는 것은 차단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-250">When a Hub method executes synchronously and the transport is WebSocket, subsequent invocations of methods on the Hub from the same client are blocked until the Hub method completes.</span></span>

<span data-ttu-id="bebbc-251">다음 예제에서는 동기적 또는 비동기적으로 실행 되도록 코딩 된 동일한 메서드를 보여 주고, 두 버전을 호출 하는 데 사용할 수 있는 JavaScript 클라이언트 코드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-251">The following example shows the same method coded to run synchronously or asynchronously, followed by JavaScript client code that works for calling either version.</span></span>

<span data-ttu-id="bebbc-252">**동기적인**</span><span class="sxs-lookup"><span data-stu-id="bebbc-252">**Synchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample19.cs)]

<span data-ttu-id="bebbc-253">**비동기로**</span><span class="sxs-lookup"><span data-stu-id="bebbc-253">**Asynchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

<span data-ttu-id="bebbc-254">**생성 된 프록시를 사용 하는 JavaScript 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="bebbc-254">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample21.js)]

<span data-ttu-id="bebbc-255">ASP.NET 4.5에서 비동기 메서드를 사용 하는 방법에 대 한 자세한 내용은 [ASP.NET MVC 4에서 비동기 메서드 사용](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="bebbc-255">For more information about how to use asynchronous methods in ASP.NET 4.5, see [Using Asynchronous Methods in ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span></span>

<a id="overloads"></a>

### <a name="defining-overloads"></a><span data-ttu-id="bebbc-256">오버 로드 정의</span><span class="sxs-lookup"><span data-stu-id="bebbc-256">Defining Overloads</span></span>

<span data-ttu-id="bebbc-257">메서드에 대 한 오버 로드를 정의 하려면 각 오버 로드의 매개 변수 수가 서로 달라 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-257">If you want to define overloads for a method, the number of parameters in each overload must be different.</span></span> <span data-ttu-id="bebbc-258">서로 다른 매개 변수 형식을 지정 하 여 오버 로드를 구분 하는 경우 허브 클래스가 컴파일되지만 SignalR 서비스는 클라이언트가 오버 로드 중 하나를 호출 하려고 할 때 런타임에 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-258">If you differentiate an overload just by specifying different parameter types, your Hub class will compile but the SignalR service will throw an exception at run time when clients try to call one of the overloads.</span></span>

<a id="progress"></a>
### <a name="reporting-progress-from-hub-method-invocations"></a><span data-ttu-id="bebbc-259">허브 메서드 호출의 진행률 보고</span><span class="sxs-lookup"><span data-stu-id="bebbc-259">Reporting progress from hub method invocations</span></span>

<span data-ttu-id="bebbc-260">SignalR 2.1에는 .NET 4.5에 도입 된 [진행률 보고 패턴](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) 에 대 한 지원이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-260">SignalR 2.1 adds support for the [progress reporting pattern](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) introduced in .NET 4.5.</span></span> <span data-ttu-id="bebbc-261">진행률 보고를 구현 하려면 클라이언트가 액세스할 수 있는 허브 방법에 대 한 `IProgress<T>` 매개 변수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-261">To implement progress reporting, define an `IProgress<T>` parameter for your hub method that your client can access:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample22.cs)]

<span data-ttu-id="bebbc-262">장기 실행 서버 메서드를 작성 하는 경우 허브 스레드를 차단 하는 대신 비동기/대기와 같은 비동기 프로그래밍 패턴을 사용 하는 것이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-262">When writing a long-running server method, it is important to use an asynchronous programming pattern like Async/ Await rather than blocking the hub thread.</span></span>

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a><span data-ttu-id="bebbc-263">허브 클래스에서 클라이언트 메서드를 호출 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bebbc-263">How to call client methods from the Hub class</span></span>

<span data-ttu-id="bebbc-264">서버에서 클라이언트 메서드를 호출 하려면 허브 클래스의 메서드에서 `Clients` 속성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-264">To call client methods from the server, use the `Clients` property in a method in your Hub class.</span></span> <span data-ttu-id="bebbc-265">다음 예제에서는 모든 연결 된 클라이언트에서 `addNewMessageToPage`를 호출 하는 서버 코드와 JavaScript 클라이언트에서 메서드를 정의 하는 클라이언트 코드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-265">The following example shows server code that calls `addNewMessageToPage` on all connected clients, and client code that defines the method in a JavaScript client.</span></span>

<span data-ttu-id="bebbc-266">**Server**</span><span class="sxs-lookup"><span data-stu-id="bebbc-266">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample23.cs?highlight=5)]

<span data-ttu-id="bebbc-267">클라이언트 메서드 호출은 비동기 작업이 며 `Task`을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-267">Invoking a client method is an asynchronous operation and returns a `Task`.</span></span> <span data-ttu-id="bebbc-268">`await`는 다음 용도로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-268">Use `await`:</span></span>

* <span data-ttu-id="bebbc-269">메시지를 오류 없이 보낼지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-269">To ensure the message is sent without error.</span></span> 
* <span data-ttu-id="bebbc-270">Try-catch 블록에서 오류를 catch 하 고 처리할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-270">To enable catching and handling errors in a try-catch block.</span></span>

<span data-ttu-id="bebbc-271">**생성 된 프록시를 사용 하는 JavaScript 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="bebbc-271">**JavaScript client using generated proxy**</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample24.html?highlight=1)]

<span data-ttu-id="bebbc-272">클라이언트 메서드에서 반환 값을 가져올 수 없습니다. `int x = Clients.All.add(1,1)`와 같은 구문은 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-272">You can't get a return value from a client method; syntax such as `int x = Clients.All.add(1,1)` does not work.</span></span>

<span data-ttu-id="bebbc-273">매개 변수에 대 한 복합 형식 및 배열을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-273">You can specify complex types and arrays for the parameters.</span></span> <span data-ttu-id="bebbc-274">다음 예제에서는 메서드 매개 변수에서 복합 형식을 클라이언트에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-274">The following example passes a complex type to the client in a method parameter.</span></span>

<span data-ttu-id="bebbc-275">**복합 개체를 사용 하 여 클라이언트 메서드를 호출 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="bebbc-275">**Server code that calls a client method using a complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample25.cs?highlight=3)]

<span data-ttu-id="bebbc-276">**복합 개체를 정의 하는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="bebbc-276">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample26.cs?highlight=1)]

<span data-ttu-id="bebbc-277">**생성 된 프록시를 사용 하는 JavaScript 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="bebbc-277">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample27.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a><span data-ttu-id="bebbc-278">RPC를 수신 하는 클라이언트 선택</span><span class="sxs-lookup"><span data-stu-id="bebbc-278">Selecting which clients will receive the RPC</span></span>

<span data-ttu-id="bebbc-279">Clients 속성은 RPC를 수신 하는 클라이언트를 지정 하는 여러 옵션을 제공 하는 [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) 개체를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-279">The Clients property returns a [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) object that provides several options for specifying which clients will receive the RPC:</span></span>

- <span data-ttu-id="bebbc-280">연결된 모든 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-280">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample28.cs)]
- <span data-ttu-id="bebbc-281">호출 클라이언트만</span><span class="sxs-lookup"><span data-stu-id="bebbc-281">Only the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample29.cs)]
- <span data-ttu-id="bebbc-282">호출 클라이언트를 제외한 모든 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-282">All clients except the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample30.cs)]
- <span data-ttu-id="bebbc-283">연결 ID로 식별 되는 특정 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-283">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample31.css)]

    <span data-ttu-id="bebbc-284">이 예제에서는 호출 클라이언트에 대 한 `addContosoChatMessageToPage`를 호출 하 고 `Clients.Caller`를 사용 하는 것과 동일한 효과를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-284">This example calls `addContosoChatMessageToPage` on the calling client and has the same effect as using `Clients.Caller`.</span></span>
- <span data-ttu-id="bebbc-285">지정 된 클라이언트를 제외한 연결 된 모든 클라이언트는 연결 ID로 식별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-285">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample32.cs)]
- <span data-ttu-id="bebbc-286">지정 된 그룹의 모든 연결 된 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-286">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample33.css)]
- <span data-ttu-id="bebbc-287">지정 된 그룹에서 연결 ID로 식별 된 지정 된 클라이언트를 제외한 모든 연결 된 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-287">All connected clients in a specified group except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample34.cs)]
- <span data-ttu-id="bebbc-288">호출 클라이언트를 제외한 지정 된 그룹에 있는 모든 연결 된 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-288">All connected clients in a specified group except the calling client.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample35.css)]
- <span data-ttu-id="bebbc-289">사용자 Id로 식별 되는 특정 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-289">A specific user, identified by userId.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample36.cs)]

    <span data-ttu-id="bebbc-290">기본적으로이는 `IPrincipal.Identity.Name`이지만 [IUserIdProvider의 구현을 전역 호스트에 등록](mapping-users-to-connections.md#IUserIdProvider)하 여 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-290">By default, this is `IPrincipal.Identity.Name`, but this can be changed by [registering an implementation of IUserIdProvider with the global host](mapping-users-to-connections.md#IUserIdProvider).</span></span>
- <span data-ttu-id="bebbc-291">연결 Id 목록의 모든 클라이언트 및 그룹</span><span class="sxs-lookup"><span data-stu-id="bebbc-291">All clients and groups in a list of connection IDs.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample37.css)]
- <span data-ttu-id="bebbc-292">그룹 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-292">A list of groups.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample38.css)]
- <span data-ttu-id="bebbc-293">이름으로 된 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-293">A user by name.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample39.cs)]
- <span data-ttu-id="bebbc-294">SignalR 2.1에 도입 된 사용자 이름 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-294">A list of user names (introduced in SignalR 2.1).</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample40.cs)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a><span data-ttu-id="bebbc-295">메서드 이름에 대 한 컴파일 타임 유효성 검사 없음</span><span class="sxs-lookup"><span data-stu-id="bebbc-295">No compile-time validation for method names</span></span>

<span data-ttu-id="bebbc-296">지정 하는 메서드 이름은 동적 개체로 해석 됩니다. 즉, IntelliSense 또는 컴파일 타임 유효성 검사를 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-296">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="bebbc-297">식은 런타임에 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-297">The expression is evaluated at run time.</span></span> <span data-ttu-id="bebbc-298">메서드 호출이 실행 되 면 SignalR는 메서드 이름 및 매개 변수 값을 클라이언트에 보내고, 클라이언트에 이름과 일치 하는 메서드가 있으면 해당 메서드가 호출 되 고 매개 변수 값이 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-298">When the method call executes, SignalR sends the method name and the parameter values to the client, and if the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="bebbc-299">클라이언트에서 일치 하는 메서드를 찾을 수 없는 경우 오류가 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-299">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="bebbc-300">클라이언트 메서드를 호출할 때 SignalR가 백그라운드에서 클라이언트로 전송 하는 데이터 형식에 대 한 자세한 내용은 [SignalR 소개](../getting-started/introduction-to-signalr.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="bebbc-300">For information about the format of the data that SignalR transmits to the client behind the scenes when you call a client method, see [Introduction to SignalR](../getting-started/introduction-to-signalr.md).</span></span>

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a><span data-ttu-id="bebbc-301">대/소문자를 구분 하지 않는 메서드 이름 일치</span><span class="sxs-lookup"><span data-stu-id="bebbc-301">Case-insensitive method name matching</span></span>

<span data-ttu-id="bebbc-302">메서드 이름 일치는 대/소문자를 구분 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-302">Method name matching is case-insensitive.</span></span> <span data-ttu-id="bebbc-303">예를 들어 서버의 `Clients.All.addContosoChatMessageToPage`은 클라이언트에서 `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`또는 `addContosoChatMessageToPage`를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-303">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`, or `addContosoChatMessageToPage` on the client.</span></span>

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a><span data-ttu-id="bebbc-304">비동기 실행</span><span class="sxs-lookup"><span data-stu-id="bebbc-304">Asynchronous execution</span></span>

<span data-ttu-id="bebbc-305">호출 하는 메서드는 비동기적으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-305">The method that you call executes asynchronously.</span></span> <span data-ttu-id="bebbc-306">클라이언트에 대 한 메서드 호출 후에 발생 하는 모든 코드는 다음 코드 줄이 메서드 완료를 기다리도록 지정 하지 않는 한 SignalR가 클라이언트에 데이터 전송을 완료할 때까지 기다리지 않고 즉시 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-306">Any code that comes after a method call to a client will execute immediately without waiting for SignalR to finish transmitting data to clients unless you specify that the subsequent lines of code should wait for method completion.</span></span> <span data-ttu-id="bebbc-307">다음 코드 예제에서는 두 개의 클라이언트 메서드를 순차적으로 실행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-307">The following code example shows how to execute two client methods sequentially.</span></span>

<span data-ttu-id="bebbc-308">**Wait 사용 (.NET 4.5)**</span><span class="sxs-lookup"><span data-stu-id="bebbc-308">**Using Await (.NET 4.5)**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

<span data-ttu-id="bebbc-309">`await`를 사용 하 여 다음 코드 줄이 실행 되기 전에 클라이언트 메서드가 완료 될 때까지 대기 하는 경우 클라이언트는 다음 코드 줄이 실행 되기 전에 실제로 메시지를 수신 하는 것을 의미 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-309">If you use `await` to wait until a client method finishes before the next line of code executes, that does not mean that clients will actually receive the message before the next line of code executes.</span></span> <span data-ttu-id="bebbc-310">클라이언트 메서드 호출의 "완료"는 SignalR 메시지를 보내는 데 필요한 모든 작업을 수행 했음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-310">"Completion" of a client method call only means that SignalR has done everything necessary to send the message.</span></span> <span data-ttu-id="bebbc-311">클라이언트에서 메시지를 받았는지 확인 해야 하는 경우 해당 메커니즘을 직접 프로그래밍 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-311">If you need verification that clients received the message, you have to program that mechanism yourself.</span></span> <span data-ttu-id="bebbc-312">예를 들어 허브에 `MessageReceived` 메서드를 코딩 하 고 클라이언트에서 수행 해야 하는 작업을 수행한 후 클라이언트의 `addContosoChatMessageToPage` 메서드에서 `MessageReceived`를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-312">For example, you could code a `MessageReceived` method on the Hub, and in the `addContosoChatMessageToPage` method on the client you could call `MessageReceived` after you do whatever work you need to do on the client.</span></span> <span data-ttu-id="bebbc-313">허브의 `MessageReceived`은 실제 클라이언트 수신 및 원래 메서드 호출 처리에 따라 달라 지는 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-313">In `MessageReceived` in the Hub you can do whatever work depends on actual client reception and processing of the original method call.</span></span>

### <a name="how-to-use-a-string-variable-as-the-method-name"></a><span data-ttu-id="bebbc-314">문자열 변수를 메서드 이름으로 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bebbc-314">How to use a string variable as the method name</span></span>

<span data-ttu-id="bebbc-315">문자열 변수를 메서드 이름으로 사용 하 여 클라이언트 메서드를 호출 하려면 `Clients.All` (또는 `Clients.Others`, `Clients.Caller`등)를 `IClientProxy`로 캐스팅 한 다음 [invoke (methodName, args ...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx)를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-315">If you want to invoke a client method by using a string variable as the method name, cast `Clients.All` (or `Clients.Others`, `Clients.Caller`, etc.) to `IClientProxy` and then call [Invoke(methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample42.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a><span data-ttu-id="bebbc-316">허브 클래스에서 그룹 멤버 자격을 관리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bebbc-316">How to manage group membership from the Hub class</span></span>

<span data-ttu-id="bebbc-317">SignalR의 그룹은 연결 된 클라이언트의 지정 된 하위 집합에 메시지를 브로드캐스팅하는 메서드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-317">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="bebbc-318">그룹에는 원하는 수의 클라이언트가 있을 수 있으며, 클라이언트는 원하는 수의 그룹의 구성원이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-318">A group can have any number of clients, and a client can be a member of any number of groups.</span></span>

<span data-ttu-id="bebbc-319">그룹 멤버 자격을 관리 하려면 허브 클래스의 `Groups` 속성에서 제공 하는 [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) 및 [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-319">To manage group membership, use the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) and [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods provided by the `Groups` property of the Hub class.</span></span> <span data-ttu-id="bebbc-320">다음 예제에서는 클라이언트 코드에서 호출 되는 허브 메서드에서 사용 되는 `Groups.Add` 및 `Groups.Remove` 메서드와이를 호출 하는 JavaScript 클라이언트 코드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-320">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods that are called by client code, followed by JavaScript client code that calls them.</span></span>

<span data-ttu-id="bebbc-321">**Server**</span><span class="sxs-lookup"><span data-stu-id="bebbc-321">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample43.cs?highlight=5,10)]

<span data-ttu-id="bebbc-322">**생성 된 프록시를 사용 하는 JavaScript 클라이언트**</span><span class="sxs-lookup"><span data-stu-id="bebbc-322">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample44.js)]

[!code-javascript[Main](hubs-api-guide-server/samples/sample45.js)]

<span data-ttu-id="bebbc-323">그룹을 명시적으로 만들 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-323">You don't have to explicitly create groups.</span></span> <span data-ttu-id="bebbc-324">실제로 그룹은 `Groups.Add`호출에서 처음으로 이름을 지정 하는 경우 자동으로 생성 되며, 해당 그룹의 멤버 자격에서 마지막 연결을 제거 하면 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-324">In effect a group is automatically created the first time you specify its name in a call to `Groups.Add`, and it is deleted when you remove the last connection from membership in it.</span></span>

<span data-ttu-id="bebbc-325">그룹 구성원 목록이 나 그룹 목록을 가져오기 위한 API는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-325">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="bebbc-326">SignalR는 [pub/sub 모델](http://en.wikipedia.org/wiki/Publish/subscribe)을 기반으로 클라이언트 및 그룹에 메시지를 보내고 서버는 그룹 또는 그룹 멤버 자격 목록을 유지 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-326">SignalR sends messages to clients and groups based on a [pub/sub model](http://en.wikipedia.org/wiki/Publish/subscribe), and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="bebbc-327">이를 통해 웹 팜에 노드를 추가할 때마다 SignalR가 유지 관리 하는 모든 상태를 새 노드에 전파 해야 하므로 확장성을 최대화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-327">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a><span data-ttu-id="bebbc-328">Add 및 Remove 메서드의 비동기 실행</span><span class="sxs-lookup"><span data-stu-id="bebbc-328">Asynchronous execution of Add and Remove methods</span></span>

<span data-ttu-id="bebbc-329">`Groups.Add` 및 `Groups.Remove` 메서드는 비동기적으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-329">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span> <span data-ttu-id="bebbc-330">그룹에 클라이언트를 추가 하 고 해당 그룹을 사용 하 여 클라이언트에 즉시 메시지를 보내려면 `Groups.Add` 메서드가 먼저 완료 되는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-330">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the `Groups.Add` method finishes first.</span></span> <span data-ttu-id="bebbc-331">다음 코드 예제에서는이 작업을 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-331">The following code example shows how to do that.</span></span>

<span data-ttu-id="bebbc-332">**클라이언트를 그룹에 추가한 다음 해당 클라이언트에 메시징**</span><span class="sxs-lookup"><span data-stu-id="bebbc-332">**Adding a client to a group and then messaging that client**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample46.cs?highlight=1,3)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a><span data-ttu-id="bebbc-333">그룹 멤버 자격 지 속성</span><span class="sxs-lookup"><span data-stu-id="bebbc-333">Group membership persistence</span></span>

<span data-ttu-id="bebbc-334">SignalR는 사용자가 아닌 연결을 추적 하므로 사용자가 연결을 설정할 때마다 사용자가 동일한 그룹에 포함 되도록 하려면 사용자가 새 연결을 설정할 때마다 `Groups.Add`를 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-334">SignalR tracks connections, not users, so if you want a user to be in the same group every time the user establishes a connection, you have to call `Groups.Add` every time the user establishes a new connection.</span></span>

<span data-ttu-id="bebbc-335">일시적으로 연결이 끊어지면 SignalR에서 자동으로 연결을 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-335">After a temporary loss of connectivity, sometimes SignalR can restore the connection automatically.</span></span> <span data-ttu-id="bebbc-336">이 경우 SignalR는 새 연결을 설정 하지 않고 동일한 연결을 복원 하므로 클라이언트의 그룹 멤버 자격은 자동으로 복원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-336">In that case, SignalR is restoring the same connection, not establishing a new connection, and so the client's group membership is automatically restored.</span></span> <span data-ttu-id="bebbc-337">이는 그룹 멤버 자격을 포함 하 여 각 클라이언트에 대 한 연결 상태가 클라이언트에 게 라운드트립 되기 때문에 일시적 중단이 서버 재부팅 또는 실패의 결과일 때에도 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-337">This is possible even when the temporary break is the result of a server reboot or failure, because connection state for each client, including group memberships, is round-tripped to the client.</span></span> <span data-ttu-id="bebbc-338">연결 시간이 초과 되기 전에 서버가 중단 되 고 새 서버로 교체 되는 경우 클라이언트는 새 서버에 자동으로 다시 연결 하 고 해당 그룹이 속한 그룹에 다시 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-338">If a server goes down and is replaced by a new server before the connection times out, a client can reconnect automatically to the new server and re-enroll in groups it is a member of.</span></span>

<span data-ttu-id="bebbc-339">연결 손실 후 자동으로 연결을 복원할 수 없거나 연결 시간이 초과 되거나 클라이언트가 연결을 끊을 때 (예: 브라우저가 새 페이지로 이동 하는 경우) 그룹 멤버 자격이 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-339">When a connection can't be restored automatically after a loss of connectivity, or when the connection times out, or when the client disconnects (for example, when a browser navigates to a new page), group memberships are lost.</span></span> <span data-ttu-id="bebbc-340">사용자가 다음에 연결할 때 새 연결이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-340">The next time the user connects will be a new connection.</span></span> <span data-ttu-id="bebbc-341">동일한 사용자가 새 연결을 설정할 때 그룹 멤버 자격을 유지 하려면 응용 프로그램에서 사용자와 그룹 간의 연결을 추적 하 고 사용자가 새 연결을 설정할 때마다 그룹 멤버 자격을 복원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-341">To maintain group memberships when the same user establishes a new connection, your application has to track the associations between users and groups, and restore group memberships each time a user establishes a new connection.</span></span>

<span data-ttu-id="bebbc-342">연결 및 횟수에 대 한 자세한 내용은이 항목의 뒷부분에 있는 [허브 클래스에서 연결 수명 이벤트를 처리 하는 방법](#connectionlifetime) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="bebbc-342">For more information about connections and reconnections, see [How to handle connection lifetime events in the Hub class](#connectionlifetime) later in this topic.</span></span>

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a><span data-ttu-id="bebbc-343">단일 사용자 그룹</span><span class="sxs-lookup"><span data-stu-id="bebbc-343">Single-user groups</span></span>

<span data-ttu-id="bebbc-344">SignalR를 사용 하는 응용 프로그램은 일반적으로 메시지를 보낸 사용자와 메시지를 수신 해야 하는 사용자를 확인 하기 위해 사용자와 연결 간의 연결을 추적 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-344">Applications that use SignalR typically have to keep track of the associations between users and connections in order to know which user has sent a message and which user(s) should be receiving a message.</span></span> <span data-ttu-id="bebbc-345">이러한 작업을 수행 하기 위해 일반적으로 사용 되는 두 패턴 중 하나에서 그룹이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-345">Groups are used in one of the two commonly used patterns for doing that.</span></span>

- <span data-ttu-id="bebbc-346">단일 사용자 그룹.</span><span class="sxs-lookup"><span data-stu-id="bebbc-346">Single-user groups.</span></span>

    <span data-ttu-id="bebbc-347">사용자 이름을 그룹 이름으로 지정 하 고 사용자가 연결 하거나 다시 연결할 때마다 현재 연결 ID를 그룹에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-347">You can specify the user name as the group name, and add the current connection ID to the group every time the user connects or reconnects.</span></span> <span data-ttu-id="bebbc-348">그룹에 보내는 사용자에 게 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-348">To send messages to the user you send to the group.</span></span> <span data-ttu-id="bebbc-349">이 방법의 단점은 그룹이 사용자를 온라인 또는 오프 라인 상태 인지 여부를 확인 하는 방법을 제공 하지 않는다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-349">A disadvantage of this method is that the group doesn't provide you with a way to find out if the user is online or offline.</span></span>
- <span data-ttu-id="bebbc-350">사용자 이름과 연결 Id 간의 연결을 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-350">Track associations between user names and connection IDs.</span></span>

    <span data-ttu-id="bebbc-351">사전 또는 데이터베이스에 각 사용자 이름과 하나 이상의 연결 Id 사이에 연결을 저장 하 고, 사용자가 연결 하거나 연결을 끊을 때마다 저장 된 데이터를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-351">You can store an association between each user name and one or more connection IDs in a dictionary or database, and update the stored data each time the user connects or disconnects.</span></span> <span data-ttu-id="bebbc-352">사용자에 게 메시지를 보내려면 연결 Id를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-352">To send messages to the user you specify the connection IDs.</span></span> <span data-ttu-id="bebbc-353">이 방법의 단점은 더 많은 메모리를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-353">A disadvantage of this method is that it takes more memory.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a><span data-ttu-id="bebbc-354">허브 클래스에서 연결 수명 이벤트를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bebbc-354">How to handle connection lifetime events in the Hub class</span></span>

<span data-ttu-id="bebbc-355">연결 수명 이벤트를 처리 하는 일반적인 이유는 사용자가 연결 되었는지 여부를 추적 하 고 사용자 이름과 연결 Id 간의 연결을 추적 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-355">Typical reasons for handling connection lifetime events are to keep track of whether a user is connected or not, and to keep track of the association between user names and connection IDs.</span></span> <span data-ttu-id="bebbc-356">클라이언트에서 연결 하거나 연결을 끊을 때 사용자 고유의 코드를 실행 하려면 다음 예제와 같이 허브 클래스의 `OnConnected`, `OnDisconnected`및 `OnReconnected` 가상 메서드를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-356">To run your own code when clients connect or disconnect, override the `OnConnected`, `OnDisconnected`, and `OnReconnected` virtual methods of the Hub class, as shown in the following example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample47.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a><span data-ttu-id="bebbc-357">OnConnected, Onconnected 및 Onconnected가 호출 되는 경우</span><span class="sxs-lookup"><span data-stu-id="bebbc-357">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>

<span data-ttu-id="bebbc-358">브라우저가 새 페이지로 이동할 때마다 새 연결을 설정 해야 합니다. 즉, SignalR는 `OnDisconnected` 메서드를 실행 한 다음 `OnConnected` 메서드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-358">Each time a browser navigates to a new page, a new connection has to be established, which means SignalR will execute the `OnDisconnected` method followed by the `OnConnected` method.</span></span> <span data-ttu-id="bebbc-359">SignalR는 새 연결이 설정 될 때 항상 새 연결 ID를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-359">SignalR always creates a new connection ID when a new connection is established.</span></span>

<span data-ttu-id="bebbc-360">`OnReconnected` 메서드는 연결 시간이 초과 되기 전에 케이블을 일시적으로 분리 하 고 다시 연결 하는 경우와 같이 SignalR에서 자동으로 복구할 수 있는 일시적인 연결이 있을 때 호출 됩니다. `OnDisconnected` 메서드는 브라우저가 새 페이지로 이동 하는 경우와 같이 클라이언트 연결이 끊어져 SignalR가 자동으로 다시 연결할 수 없는 경우에 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-360">The `OnReconnected` method is called when there has been a temporary break in connectivity that SignalR can automatically recover from, such as when a cable is temporarily disconnected and reconnected before the connection times out. The `OnDisconnected` method is called when the client is disconnected and SignalR can't automatically reconnect, such as when a browser navigates to a new page.</span></span> <span data-ttu-id="bebbc-361">따라서 지정 된 클라이언트에 대해 가능한 이벤트 시퀀스는 `OnConnected`, `OnReconnected`, `OnDisconnected`;입니다. 또는 `OnConnected``OnDisconnected`합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-361">Therefore, a possible sequence of events for a given client is `OnConnected`, `OnReconnected`, `OnDisconnected`; or `OnConnected`, `OnDisconnected`.</span></span> <span data-ttu-id="bebbc-362">지정 된 연결에 대 한 `OnConnected`, `OnDisconnected``OnReconnected` 시퀀스는 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-362">You won't see the sequence `OnConnected`, `OnDisconnected`, `OnReconnected` for a given connection.</span></span>

<span data-ttu-id="bebbc-363">서버 작동이 중단 되거나 응용 프로그램 도메인이 재활용 되는 등의 일부 시나리오에서는 `OnDisconnected` 메서드가 호출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-363">The `OnDisconnected` method doesn't get called in some scenarios, such as when a server goes down or the App Domain gets recycled.</span></span> <span data-ttu-id="bebbc-364">다른 서버를 온라인 상태로 만들거나 앱 도메인에서 재활용이 완료 되 면 일부 클라이언트는 `OnReconnected` 이벤트를 다시 연결 하 여 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-364">When another server comes on line or the App Domain completes its recycle, some clients may be able to reconnect and fire the `OnReconnected` event.</span></span>

<span data-ttu-id="bebbc-365">자세한 내용은 [SignalR의 연결 수명 이벤트 이해 및 처리](handling-connection-lifetime-events.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="bebbc-365">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a><span data-ttu-id="bebbc-366">호출자 상태가 채워지지 않음</span><span class="sxs-lookup"><span data-stu-id="bebbc-366">Caller state not populated</span></span>

<span data-ttu-id="bebbc-367">연결 수명 이벤트 처리기 메서드는 서버에서 호출 됩니다. 즉, 클라이언트의 `state` 개체에 넣는 모든 상태는 서버의 `Caller` 속성에 채워지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-367">The connection lifetime event handler methods are called from the server, which means that any state that you put in the `state` object on the client will not be populated in the `Caller` property on the server.</span></span> <span data-ttu-id="bebbc-368">`state` 개체 및 `Caller` 속성에 대 한 자세한 내용은이 항목의 뒷부분에 나오는 [클라이언트와 허브 클래스 간의 상태를 전달 하는 방법](#passstate) 을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="bebbc-368">For information about the `state` object and the `Caller` property, see [How to pass state between clients and the Hub class](#passstate) later in this topic.</span></span>

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a><span data-ttu-id="bebbc-369">컨텍스트 속성에서 클라이언트에 대 한 정보를 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="bebbc-369">How to get information about the client from the Context property</span></span>

<span data-ttu-id="bebbc-370">클라이언트에 대 한 정보를 가져오려면 허브 클래스의 `Context` 속성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-370">To get information about the client, use the `Context` property of the Hub class.</span></span> <span data-ttu-id="bebbc-371">`Context` 속성은 다음 정보에 대 한 액세스를 제공 하는 [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) 개체를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-371">The `Context` property returns a [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) object which provides access to the following information:</span></span>

- <span data-ttu-id="bebbc-372">호출 클라이언트의 연결 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-372">The connection ID of the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample48.cs?highlight=1)]

    <span data-ttu-id="bebbc-373">연결 ID는 SignalR에서 할당 한 GUID입니다 (사용자 고유의 코드에서 값을 지정할 수 없음).</span><span class="sxs-lookup"><span data-stu-id="bebbc-373">The connection ID is a GUID that is assigned by SignalR (you can't specify the value in your own code).</span></span> <span data-ttu-id="bebbc-374">각 연결에 대해 하나의 연결 ID가 있으며, 응용 프로그램에 허브가 여러 개 있는 경우 모든 허브에서 동일한 연결 ID를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-374">There is one connection ID for each connection, and the same connection ID is used by all Hubs if you have multiple Hubs in your application.</span></span>
- <span data-ttu-id="bebbc-375">HTTP 헤더 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-375">HTTP header data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    <span data-ttu-id="bebbc-376">`Context.Headers`에서 HTTP 헤더를 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-376">You can also get HTTP headers from `Context.Headers`.</span></span> <span data-ttu-id="bebbc-377">동일한 작업을 수행 하는 이유는 `Context.Headers`를 먼저 만들고 `Context.Request` 속성을 나중에 추가 하 고 `Context.Headers` 이전 버전과의 호환성을 위해 유지 했기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-377">The reason for multiple references to the same thing is that `Context.Headers` was created first, the `Context.Request` property was added later, and `Context.Headers` was retained for backward compatibility.</span></span>
- <span data-ttu-id="bebbc-378">쿼리 문자열 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-378">Query string data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample50.cs?highlight=1)]

    <span data-ttu-id="bebbc-379">`Context.QueryString`에서 쿼리 문자열 데이터를 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-379">You can also get query string data from `Context.QueryString`.</span></span>

    <span data-ttu-id="bebbc-380">이 속성에서 가져오는 쿼리 문자열은 SignalR 연결을 설정 하는 HTTP 요청에 사용 된 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-380">The query string that you get in this property is the one that was used with the HTTP request that established the SignalR connection.</span></span> <span data-ttu-id="bebbc-381">클라이언트에서 서버로 클라이언트에 대 한 데이터를 전달 하는 편리한 방법인 연결을 구성 하 여 클라이언트에서 쿼리 문자열 매개 변수를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-381">You can add query string parameters in the client by configuring the connection, which is a convenient way to pass data about the client from the client to the server.</span></span> <span data-ttu-id="bebbc-382">다음 예에서는 생성 된 프록시를 사용할 때 JavaScript 클라이언트에서 쿼리 문자열을 추가 하는 한 가지 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-382">The following example shows one way to add a query string in a JavaScript client when you use the generated proxy.</span></span>

    [!code-javascript[Main](hubs-api-guide-server/samples/sample51.js?highlight=1)]

    <span data-ttu-id="bebbc-383">쿼리 문자열 매개 변수를 설정 하는 방법에 대 한 자세한 내용은 [JavaScript](hubs-api-guide-javascript-client.md) 및 [.net](hubs-api-guide-net-client.md) 클라이언트에 대 한 API 가이드를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="bebbc-383">For more information about setting query string parameters, see the API guides for the [JavaScript](hubs-api-guide-javascript-client.md) and [.NET](hubs-api-guide-net-client.md) clients.</span></span>

    <span data-ttu-id="bebbc-384">SignalR에서 내부적으로 사용 되는 다른 값과 함께 쿼리 문자열 데이터에서 연결에 사용 되는 전송 방법을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-384">You can find the transport method used for the connection in the query string data, along with some other values used internally by SignalR:</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample52.cs)]

    <span data-ttu-id="bebbc-385">`transportMethod`의 값은 "Websocket", "serverSentEvents", "foreverFrame" 또는 ""입니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-385">The value of `transportMethod` will be "webSockets", "serverSentEvents", "foreverFrame" or "longPolling".</span></span> <span data-ttu-id="bebbc-386">`OnConnected` 이벤트 처리기 메서드에서이 값을 확인 하는 경우 일부 시나리오에서 처음에는 연결에 대해 협상 된 최종 전송 방법이 아닌 전송 값을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-386">Note that if you check this value in the `OnConnected` event handler method, in some scenarios you might initially get a transport value that is not the final negotiated transport method for the connection.</span></span> <span data-ttu-id="bebbc-387">이 경우 메서드는 예외를 throw 하 고 나중에 최종 전송 메서드가 설정 될 때 다시 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-387">In that case the method will throw an exception and will be called again later when the final transport method is established.</span></span>
- <span data-ttu-id="bebbc-388">쿠키입니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-388">Cookies.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample53.cs?highlight=1)]

    <span data-ttu-id="bebbc-389">`Context.RequestCookies`에서 쿠키를 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-389">You can also get cookies from `Context.RequestCookies`.</span></span>
- <span data-ttu-id="bebbc-390">사용자 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-390">User information.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample54.cs?highlight=1)]
- <span data-ttu-id="bebbc-391">요청에 대 한 HttpContext 개체:</span><span class="sxs-lookup"><span data-stu-id="bebbc-391">The HttpContext object for the request :</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample55.cs?highlight=1)]

    <span data-ttu-id="bebbc-392">SignalR 연결에 대 한 `HttpContext` 개체를 가져오는 `HttpContext.Current` 대신이 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-392">Use this method instead of getting `HttpContext.Current` to get the `HttpContext` object for the SignalR connection.</span></span>

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a><span data-ttu-id="bebbc-393">클라이언트와 허브 클래스 간의 상태를 전달 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bebbc-393">How to pass state between clients and the Hub class</span></span>

<span data-ttu-id="bebbc-394">클라이언트 프록시는 각 메서드 호출을 사용 하 여 서버로 전송 하려는 데이터를 저장할 수 있는 `state` 개체를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-394">The client proxy provides a `state` object in which you can store data that you want to be transmitted to the server with each method call.</span></span> <span data-ttu-id="bebbc-395">서버에서 클라이언트에 의해 호출 되는 허브 메서드의 `Clients.Caller` 속성에서이 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-395">On the server you can access this data in the `Clients.Caller` property in Hub methods that are called by clients.</span></span> <span data-ttu-id="bebbc-396">`Clients.Caller` 속성은 `OnConnected`, `OnDisconnected`및 `OnReconnected`연결 수명 이벤트 처리기 메서드에 대해 채워지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-396">The `Clients.Caller` property is not populated for the connection lifetime event handler methods `OnConnected`, `OnDisconnected`, and `OnReconnected`.</span></span>

<span data-ttu-id="bebbc-397">`state` 개체의 데이터를 만들거나 업데이트 하는 방법 및 `Clients.Caller` 속성은 양방향으로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-397">Creating or updating data in the `state` object and the `Clients.Caller` property works in both directions.</span></span> <span data-ttu-id="bebbc-398">서버에서 값을 업데이트할 수 있으며 클라이언트에 다시 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-398">You can update values in the server and they are passed back to the client.</span></span>

<span data-ttu-id="bebbc-399">다음 예제에서는 모든 메서드 호출을 통해 서버로 전송 되는 상태를 저장 하는 JavaScript 클라이언트 코드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-399">The following example shows JavaScript client code that stores state for transmission to the server with every method call.</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample56.js?highlight=1-2)]

<span data-ttu-id="bebbc-400">다음 예제에서는 .NET 클라이언트의 해당 코드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-400">The following example shows the equivalent code in a .NET client.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample57.cs?highlight=1-2)]

<span data-ttu-id="bebbc-401">허브 클래스의 `Clients.Caller` 속성에서이 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-401">In your Hub class, you can access this data in the `Clients.Caller` property.</span></span> <span data-ttu-id="bebbc-402">다음 예제에서는 이전 예제에서 참조 되는 상태를 검색 하는 코드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-402">The following example shows code that retrieves the state referred to in the previous example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample58.cs?highlight=3-4)]

> [!NOTE]
> <span data-ttu-id="bebbc-403">상태를 유지 하기 위한이 메커니즘은 많은 양의 데이터에는 사용할 수 없습니다 .이 메커니즘은 `state` 또는 `Clients.Caller` 속성에 입력 한 모든 항목이 모든 메서드 호출에서 라운드트립 되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-403">This mechanism for persisting state is not intended for large amounts of data, since everything you put in the `state` or `Clients.Caller` property is round-tripped with every method invocation.</span></span> <span data-ttu-id="bebbc-404">사용자 이름 또는 카운터와 같은 작은 항목에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-404">It's useful for smaller items such as user names or counters.</span></span>

<span data-ttu-id="bebbc-405">VB.NET 또는 강력한 형식의 허브에서 호출자 상태 개체는 `Clients.Caller`을 통해 액세스할 수 없습니다. 대신 `Clients.CallerState` (SignalR 2.1에 도입 됨)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-405">In VB.NET or in a strongly-typed hub, the caller state object can't be accessed through `Clients.Caller`; instead, use `Clients.CallerState` (introduced in SignalR 2.1):</span></span>

<span data-ttu-id="bebbc-406">**에서 CallerState 사용C#**</span><span class="sxs-lookup"><span data-stu-id="bebbc-406">**Using CallerState in C#**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample59.cs?highlight=3-4)]

<span data-ttu-id="bebbc-407">**Visual Basic에서 CallerState 사용**</span><span class="sxs-lookup"><span data-stu-id="bebbc-407">**Using CallerState in Visual Basic**</span></span>

[!code-vb[Main](hubs-api-guide-server/samples/sample60.vb)]

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a><span data-ttu-id="bebbc-408">허브 클래스에서 오류를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bebbc-408">How to handle errors in the Hub class</span></span>

<span data-ttu-id="bebbc-409">허브 클래스 메서드에서 발생 하는 오류를 처리 하려면 먼저 `await`를 사용 하 여 비동기 작업 (예: 클라이언트 메서드 호출)에서 발생 하는 모든 예외를 "관찰" 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-409">To handle errors that occur in your Hub class methods, first ensure you "observe" any exceptions from async operations (such as invoking client methods) by using `await`.</span></span> <span data-ttu-id="bebbc-410">다음 방법 중 하나 이상을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-410">Then use one or more of the following methods:</span></span>

- <span data-ttu-id="bebbc-411">Try-catch 블록에서 메서드 코드를 래핑하고 예외 개체를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-411">Wrap your method code in try-catch blocks and log the exception object.</span></span> <span data-ttu-id="bebbc-412">디버깅을 위해 클라이언트에 예외를 보낼 수 있지만, 보안상의 이유로 프로덕션 환경에서 클라이언트에 자세한 정보를 전송 하는 것은 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-412">For debugging purposes you can send the exception to the client, but for security reasons sending detailed information to clients in production is not recommended.</span></span>
- <span data-ttu-id="bebbc-413">[OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) 메서드를 처리 하는 허브 파이프라인 모듈을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-413">Create a Hubs pipeline module that handles the [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) method.</span></span> <span data-ttu-id="bebbc-414">다음 예제에서는 오류를 기록 하 고, 모듈을 허브 파이프라인에 삽입 하는 Startup.cs의 코드를 기록 하는 파이프라인 모듈을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-414">The following example shows a pipeline module that logs errors, followed by code in Startup.cs that injects the module into the Hubs pipeline.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample61.cs)]

    [!code-csharp[Main](hubs-api-guide-server/samples/sample62.cs?highlight=4)]
- <span data-ttu-id="bebbc-415">SignalR 2에 도입 된 `HubException` 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-415">Use the `HubException` class (introduced in SignalR 2).</span></span> <span data-ttu-id="bebbc-416">이 오류는 모든 허브 호출에서 throw 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-416">This error can be thrown from any hub invocation.</span></span> <span data-ttu-id="bebbc-417">`HubError` 생성자는 문자열 메시지를 사용 하 고 추가 오류 데이터를 저장 하기 위한 개체를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-417">The `HubError` constructor takes a string message, and an object for storing extra error data.</span></span> <span data-ttu-id="bebbc-418">SignalR는 예외를 자동으로 직렬화 하 고 클라이언트에 보냅니다. 그러면이 예외를 사용 하 여 허브 메서드 호출을 거부 하거나 실패 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-418">SignalR will auto-serialize the exception and send it to the client, where it will be used to reject or fail the hub method invocation.</span></span>

    <span data-ttu-id="bebbc-419">다음 코드 샘플에서는 허브 호출 중에 `HubException`을 throw 하는 방법과 JavaScript 및 .NET 클라이언트에서 예외를 처리 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-419">The following code samples demonstrate how to throw a `HubException` during a Hub invocation, and how to handle the exception on JavaScript and .NET clients.</span></span>

    <span data-ttu-id="bebbc-420">**HubException 클래스를 보여 주는 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="bebbc-420">**Server code demonstrating the HubException class**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample63.cs)]

    <span data-ttu-id="bebbc-421">**허브에서 HubException을 throw 하는 응답을 보여 주는 JavaScript 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="bebbc-421">**JavaScript client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-html[Main](hubs-api-guide-server/samples/sample64.html)]

    <span data-ttu-id="bebbc-422">**허브에서 HubException을 throw 하는 응답을 보여 주는 .NET 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="bebbc-422">**.NET client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample65.cs)]

<span data-ttu-id="bebbc-423">허브 파이프라인 모듈에 대 한 자세한 내용은이 항목의 뒷부분에 나오는 [허브 파이프라인을 사용자 지정 하는 방법](#hubpipeline) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="bebbc-423">For more information about Hub pipeline modules, see [How to customize the Hubs pipeline](#hubpipeline) later in this topic.</span></span>

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a><span data-ttu-id="bebbc-424">추적을 사용 하도록 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bebbc-424">How to enable tracing</span></span>

<span data-ttu-id="bebbc-425">서버 쪽 추적을 사용 하도록 설정 하려면 다음 예제와 같이 Web.config 파일에 시스템 진단 요소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-425">To enable server-side tracing, add a system.diagnostics element to your Web.config file, as shown in this example:</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample66.html?highlight=17-72)]

<span data-ttu-id="bebbc-426">Visual Studio에서 응용 프로그램을 실행 하면 **출력** 창에서 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-426">When you run the application in Visual Studio, you can view the logs in the **Output** window.</span></span>

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a><span data-ttu-id="bebbc-427">허브 클래스 외부에서 클라이언트 메서드를 호출 하 고 그룹을 관리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bebbc-427">How to call client methods and manage groups from outside the Hub class</span></span>

<span data-ttu-id="bebbc-428">허브 클래스와 다른 클래스에서 클라이언트 메서드를 호출 하려면 허브에 대 한 SignalR context 개체에 대 한 참조를 가져온 다음 클라이언트에서 메서드를 호출 하거나 그룹을 관리 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-428">To call client methods from a different class than your Hub class, get a reference to the SignalR context object for the Hub and use that to call methods on the client or manage groups.</span></span>

<span data-ttu-id="bebbc-429">다음 샘플 `StockTicker` 클래스는 컨텍스트 개체를 가져와 클래스의 인스턴스에 저장 하 고, 클래스 인스턴스를 정적 속성에 저장 하 고, singleton 클래스 인스턴스의 컨텍스트를 사용 하 여 `StockTickerHub`라는 허브에 연결 된 클라이언트에서 `updateStockPrice` 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-429">The following sample `StockTicker` class gets the context object, stores it in an instance of the class, stores the class instance in a static property, and uses the context from the singleton class instance to call the `updateStockPrice` method on clients that are connected to a Hub named `StockTickerHub`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample67.cs?highlight=8,24)]

<span data-ttu-id="bebbc-430">수명이 긴 개체에서 여러 번 컨텍스트를 사용 해야 하는 경우에는 참조를 한 번 가져온 다음 매번 다시 가져오는 대신 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-430">If you need to use the context multiple-times in a long-lived object, get the reference once and save it rather than getting it again each time.</span></span> <span data-ttu-id="bebbc-431">컨텍스트를 한 번 가져오면 SignalR에서 허브 메서드가 클라이언트 메서드 호출을 수행 하는 것과 동일한 순서로 메시지를 클라이언트에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-431">Getting the context once ensures that SignalR sends messages to clients in the same sequence in which your Hub methods make client method invocations.</span></span> <span data-ttu-id="bebbc-432">허브에 SignalR 컨텍스트를 사용 하는 방법을 보여 주는 자습서는 [ASP.NET SignalR를 사용 하 여 서버 브로드캐스트](../getting-started/tutorial-server-broadcast-with-signalr.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="bebbc-432">For a tutorial that shows how to use the SignalR context for a Hub, see [Server Broadcast with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).</span></span>

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a><span data-ttu-id="bebbc-433">클라이언트 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="bebbc-433">Calling client methods</span></span>

<span data-ttu-id="bebbc-434">RPC를 받을 클라이언트를 지정할 수 있지만 허브 클래스에서를 호출 하는 경우 보다 더 낮은 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-434">You can specify which clients will receive the RPC, but you have fewer options than when you call from a Hub class.</span></span> <span data-ttu-id="bebbc-435">이는 컨텍스트가 클라이언트의 특정 호출과 연결 되지 않기 때문에 `Clients.Others`, `Clients.Caller`또는 `Clients.OthersInGroup`와 같은 현재 연결 ID를 알고 있어야 하는 모든 메서드를 사용할 수 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-435">The reason for this is that the context is not associated with a particular call from a client, so any methods that require knowledge of the current connection ID, such as `Clients.Others`, or `Clients.Caller`, or `Clients.OthersInGroup`, are not available.</span></span> <span data-ttu-id="bebbc-436">다음 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-436">The following options are available:</span></span>

- <span data-ttu-id="bebbc-437">연결된 모든 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-437">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample68.cs)]
- <span data-ttu-id="bebbc-438">연결 ID로 식별 되는 특정 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-438">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample69.css)]
- <span data-ttu-id="bebbc-439">지정 된 클라이언트를 제외한 연결 된 모든 클라이언트는 연결 ID로 식별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-439">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample70.cs)]
- <span data-ttu-id="bebbc-440">지정 된 그룹의 모든 연결 된 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-440">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample71.css)]
- <span data-ttu-id="bebbc-441">지정 된 그룹에서 연결 ID로 식별 된 지정 된 클라이언트를 제외한 모든 연결 된 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-441">All connected clients in a specified group except specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample72.cs)]

<span data-ttu-id="bebbc-442">허브 클래스의 메서드를 사용 하 여 허브 클래스가 아닌 클래스를 호출 하는 경우 현재 연결 ID를 전달 하 고 `Clients.Client`, `Clients.AllExcept`또는 `Clients.Group`와 함께 사용 하 여 `Clients.Caller`, `Clients.Others`또는 `Clients.OthersInGroup`을 시뮬레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-442">If you are calling into your non-Hub class from methods in your Hub class, you can pass in the current connection ID and use that with `Clients.Client`, `Clients.AllExcept`, or `Clients.Group` to simulate `Clients.Caller`, `Clients.Others`, or `Clients.OthersInGroup`.</span></span> <span data-ttu-id="bebbc-443">다음 예제에서는 `Broadcaster` 클래스가 `Clients.Others`를 시뮬레이션할 수 있도록 `MoveShapeHub` 클래스가 연결 ID를 `Broadcaster` 클래스로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-443">In the following example, the `MoveShapeHub` class passes the connection ID to the `Broadcaster` class so that the `Broadcaster` class can simulate `Clients.Others`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample73.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a><span data-ttu-id="bebbc-444">그룹 멤버 자격 관리</span><span class="sxs-lookup"><span data-stu-id="bebbc-444">Managing group membership</span></span>

<span data-ttu-id="bebbc-445">그룹 관리의 경우 허브 클래스와 동일한 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-445">For managing groups you have the same options as you do in a Hub class.</span></span>

- <span data-ttu-id="bebbc-446">그룹에 클라이언트 추가</span><span class="sxs-lookup"><span data-stu-id="bebbc-446">Add a client to a group</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample74.cs)]
- <span data-ttu-id="bebbc-447">그룹에서 클라이언트 제거</span><span class="sxs-lookup"><span data-stu-id="bebbc-447">Remove a client from a group</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample75.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a><span data-ttu-id="bebbc-448">허브 파이프라인을 사용자 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bebbc-448">How to customize the Hubs pipeline</span></span>

<span data-ttu-id="bebbc-449">SignalR를 사용 하면 허브 파이프라인에 사용자 고유의 코드를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-449">SignalR enables you to inject your own code into the Hub pipeline.</span></span> <span data-ttu-id="bebbc-450">다음 예제에서는 클라이언트에서 수신 된 각 들어오는 메서드 호출 및 클라이언트에서 호출 된 나가는 메서드 호출을 기록 하는 사용자 지정 허브 파이프라인 모듈을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-450">The following example shows a custom Hub pipeline module that logs each incoming method call received from the client and outgoing method call invoked on the client:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample76.cs)]

<span data-ttu-id="bebbc-451">*Startup.cs* 파일의 다음 코드는 허브 파이프라인에서 실행 되도록 모듈을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-451">The following code in the *Startup.cs* file registers the module to run in the Hub pipeline:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample77.cs?highlight=3)]

<span data-ttu-id="bebbc-452">재정의할 수 있는 여러 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bebbc-452">There are many different methods that you can override.</span></span> <span data-ttu-id="bebbc-453">전체 목록은 [HubPipelineModule 메서드](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="bebbc-453">For a complete list, see [HubPipelineModule Methods](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span></span>
