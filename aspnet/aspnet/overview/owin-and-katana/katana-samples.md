---
uid: aspnet/overview/owin-and-katana/katana-samples
title: Katana 샘플 | Microsoft Docs
author: microsoft
description: ''
ms.author: riande
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: 1238f7d09492a6856d49dece5de75184ccfa4838
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78472349"
---
# <a name="katana-samples"></a><span data-ttu-id="7ef8d-102">Katana 샘플</span><span class="sxs-lookup"><span data-stu-id="7ef8d-102">Katana Samples</span></span>

<span data-ttu-id="7ef8d-103">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="7ef8d-103">by [Microsoft](https://github.com/microsoft)</span></span>

## <a name="katana-samples"></a><span data-ttu-id="7ef8d-104">Katana 샘플</span><span class="sxs-lookup"><span data-stu-id="7ef8d-104">Katana Samples</span></span>

<span data-ttu-id="7ef8d-105">**ASP.NET 경로 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span><span class="sxs-lookup"><span data-stu-id="7ef8d-105">**ASP.NET Routes Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span></span>  
<span data-ttu-id="7ef8d-106">일부 응용 프로그램에서는 Asp.Net 경로 테이블의 OWIN 구성 요소를 비 OWIN 구성 요소와 나란히 후크 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef8d-106">In some applications you will want to hook up OWIN components in the Asp.Net route table side by side with non-OWIN components.</span></span> <span data-ttu-id="7ef8d-107">이 샘플에서는 Owin 웹에서 제공 하는 RouteCollection 확장 메서드 MapOwinPath 및 MapOwinRoute를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7ef8d-107">This sample shows how to use the RouteCollection extension methods MapOwinPath and MapOwinRoute provided by Microsoft.Owin.Host.SystemWeb.</span></span>

<span data-ttu-id="7ef8d-108">**파이프라인 분기 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span><span class="sxs-lookup"><span data-stu-id="7ef8d-108">**Branching Pipelines Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span></span>  
<span data-ttu-id="7ef8d-109">OWIN 요청 처리 파이프라인은 선형 일 필요가 없으며 다른 방법으로 요청을 처리 하도록 분기할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ef8d-109">OWIN request processing pipelines do not need to be linear, they can be branched to process requests in different ways.</span></span> <span data-ttu-id="7ef8d-110">이 샘플에서는 요청 경로 또는 헤더와 같은 다른 요청 데이터를 기반으로 분기 파이프라인을 생성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7ef8d-110">This sample shows how to construct a branching pipeline based on request paths or other request data such as headers.</span></span> <span data-ttu-id="7ef8d-111">이러한 구성 요소는 Owin nuget 패키지에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ef8d-111">These components are available in the Microsoft.Owin.Mapping nuget package.</span></span>

<span data-ttu-id="7ef8d-112">**사용자 지정 서버 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span><span class="sxs-lookup"><span data-stu-id="7ef8d-112">**Custom Server Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span></span>  
<span data-ttu-id="7ef8d-113">자체 호스팅 OWIN 때 사용자 지정 OWIN 서버를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7ef8d-113">Shows how to use a custom OWIN server when self-hosting OWIN.</span></span>

<span data-ttu-id="7ef8d-114">**포함 된 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span><span class="sxs-lookup"><span data-stu-id="7ef8d-114">**Embedded Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span></span>  
<span data-ttu-id="7ef8d-115">일부 OWIN 서버는 자체 프로세스 (&quot;자체 호스팅&quot;) 내에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ef8d-115">Some OWIN servers can be run inside of your own process (&quot;self-hosted&quot;).</span></span> <span data-ttu-id="7ef8d-116">이 샘플에서는 Owin nuget 패키지에서 제공 하는 도구를 사용 하 여 OWIN 응용 프로그램을 시작 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7ef8d-116">This sample shows how to start an OWIN application using the tools provided by the Microsoft.Owin.Hosting nuget package.</span></span>

<span data-ttu-id="7ef8d-117">**HelloWorld 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span><span class="sxs-lookup"><span data-stu-id="7ef8d-117">**HelloWorld Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span></span>  
<span data-ttu-id="7ef8d-118">OWIN는 다양 한 서버에서 응용 프로그램 이식성을 가능 하 게 하는 HTTP 서버 API 추상화입니다.</span><span class="sxs-lookup"><span data-stu-id="7ef8d-118">OWIN is a HTTP server API abstraction that enables application portability across various servers.</span></span> <span data-ttu-id="7ef8d-119">이 샘플에서는 원시 OWIN 추상화 주위에 몇 가지 **간단한 래퍼** 를 사용 하 여 Hello World 응용 프로그램을 작성 하 고 ASP.NET와 같은 웹 서버에서 실행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7ef8d-119">This sample demonstrates how to write a Hello World application using some **simple wrappers** around the raw OWIN abstraction and run it on a web server like ASP.NET.</span></span>

<span data-ttu-id="7ef8d-120">**Hello World RAW OWIN 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span><span class="sxs-lookup"><span data-stu-id="7ef8d-120">**Hello World Raw OWIN Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span></span>  
<span data-ttu-id="7ef8d-121">이 샘플에서는 **raw** OWIN 추상화를 사용 하 여 Hello World 응용 프로그램을 작성 하 고 Asp.Net와 같은 웹 서버에서 실행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7ef8d-121">This sample demonstrates how to write a Hello World application using the **raw** OWIN abstraction and run it on a web server like Asp.Net.</span></span>

<span data-ttu-id="7ef8d-122">**SignalR 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span><span class="sxs-lookup"><span data-stu-id="7ef8d-122">**SignalR Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span></span>  
<span data-ttu-id="7ef8d-123">OWIN/Katana를 사용 하 여 SignalR를 자체 호스트 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7ef8d-123">Shows how to self-host SignalR using OWIN / Katana.</span></span> <span data-ttu-id="7ef8d-124">자체 호스팅 SignalR에 대 한 자세한 내용은 [자습서: SignalR 셀프 호스트](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7ef8d-124">For more info about self-hosting SignalR, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<span data-ttu-id="7ef8d-125">**정적 파일 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span><span class="sxs-lookup"><span data-stu-id="7ef8d-125">**Static Files Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span></span>  
<span data-ttu-id="7ef8d-126">OWIN/Katana를 사용 하 여 정적 파일에 대 한 HTTP 요청을 지 원하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7ef8d-126">Shows how to support HTTP requests for static files using OWIN / Katana.</span></span>

<span data-ttu-id="7ef8d-127">**웹 API** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span><span class="sxs-lookup"><span data-stu-id="7ef8d-127">**Web API** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span></span>  
<span data-ttu-id="7ef8d-128">이 샘플에서는 IIS에서 OWIN를 호스팅하고 웹 API를 OWIN 파이프라인에 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7ef8d-128">This sample shows how to host OWIN in IIS and add Web API to the OWIN pipeline.</span></span>

<span data-ttu-id="7ef8d-129">**웹 소켓 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span><span class="sxs-lookup"><span data-stu-id="7ef8d-129">**Web Socket Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span></span>  
<span data-ttu-id="7ef8d-130">OWIN 클래스를 사용 하 여 웹 소켓을 지 원하는 방법을 보여 [줍니다.](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="7ef8d-130">Shows how to support Web Sockets in OWIN by using the [System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) class.</span></span>
