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
# <a name="supported-platforms"></a><span data-ttu-id="5a6a8-103">지원되는 플랫폼</span><span class="sxs-lookup"><span data-stu-id="5a6a8-103">Supported Platforms</span></span>

<span data-ttu-id="5a6a8-104">[Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="5a6a8-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="5a6a8-105">이 문서에서는 SignalR에서 지원 되는 클라이언트 및 서버에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-105">This article describes what clients and servers are supported by SignalR.</span></span> 
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="5a6a8-106">질문 및 설명</span><span class="sxs-lookup"><span data-stu-id="5a6a8-106">Questions and comments</span></span>
> 
> <span data-ttu-id="5a6a8-107">이 자습서와 페이지 맨 아래에 있는 의견에서 개선할 수 있는 방법에 대 한 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-107">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="5a6a8-108">자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-108">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="5a6a8-109">SignalR는 다양 한 서버 및 클라이언트 구성에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-109">SignalR is supported under a variety of server and client configurations.</span></span> <span data-ttu-id="5a6a8-110">또한 각 전송 옵션에는 자체 요구 사항 집합이 있습니다. 전송에 대 한 시스템 요구 사항을 사용할 수 없는 경우 SignalR는 다른 전송으로 정상적으로 장애 조치 (failover)를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-110">In addition, each transport option has a set of requirements of its own; if the system requirements for a transport are not available, SignalR will gracefully failover to other transports.</span></span> <span data-ttu-id="5a6a8-111">SignalR에서 지 원하는 전송에 대 한 자세한 내용은 [전송 및 대체](introduction-to-signalr.md#transports)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-111">For more information on the transports that SignalR supports, see [Transports and Fallbacks](introduction-to-signalr.md#transports).</span></span>

## <a name="server-system-requirements"></a><span data-ttu-id="5a6a8-112">서버 시스템 요구 사항</span><span class="sxs-lookup"><span data-stu-id="5a6a8-112">Server system requirements</span></span>

<span data-ttu-id="5a6a8-113">SignalR 서버 구성 요소는 다양 한 서버 구성에서 호스팅될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-113">The SignalR server component can be hosted on a variety of server configurations.</span></span> <span data-ttu-id="5a6a8-114">이 섹션에서는 지원 되는 운영 체제 버전, .NET framework, 인터넷 정보 서버 및 기타 구성 요소에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-114">This section describes the supported versions of operating systems, .NET framework, Internet Information Server, and other components.</span></span>

### <a name="supported-server-operating-systems"></a><span data-ttu-id="5a6a8-115">지원 되는 서버 운영 체제</span><span class="sxs-lookup"><span data-stu-id="5a6a8-115">Supported server operating systems</span></span>

<span data-ttu-id="5a6a8-116">SignalR 서버 구성 요소는 다음 서버 또는 클라이언트 운영 체제에서 호스팅될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-116">The SignalR server component can be hosted in the following server or client operating systems.</span></span> <span data-ttu-id="5a6a8-117">SignalR에서 Websocket을 사용 하려면 windows Server 2012, Windows Server 2016 또는 Windows 8이 필요 합니다. (WebSocket은 Windows Azure 웹 사이트에서 사용할 수 있습니다. 사이트의 .NET framework 버전이 4.5로 설정 되 고 사이트에서 웹 소켓이 사용 하도록 설정 된 경우) 구성 페이지).</span><span class="sxs-lookup"><span data-stu-id="5a6a8-117">Note that for SignalR to use WebSockets, Windows Server 2012, Windows Server 2016, or Windows 8 is required (WebSocket can be used on Windows Azure Web Sites, as long as the site's .NET framework version is set to 4.5, and Web Sockets is enabled in the site's Configuration page).</span></span>

- <span data-ttu-id="5a6a8-118">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="5a6a8-118">Windows Server 2016</span></span>
- <span data-ttu-id="5a6a8-119">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="5a6a8-119">Windows Server 2012</span></span>
- <span data-ttu-id="5a6a8-120">Windows Server 2008 r2</span><span class="sxs-lookup"><span data-stu-id="5a6a8-120">Windows Server 2008 r2</span></span>
- <span data-ttu-id="5a6a8-121">윈도우 10</span><span class="sxs-lookup"><span data-stu-id="5a6a8-121">Windows 10</span></span>
- <span data-ttu-id="5a6a8-122">Windows 8</span><span class="sxs-lookup"><span data-stu-id="5a6a8-122">Windows 8</span></span>
- <span data-ttu-id="5a6a8-123">Windows 7</span><span class="sxs-lookup"><span data-stu-id="5a6a8-123">Windows 7</span></span>
- <span data-ttu-id="5a6a8-124">Windows Azure</span><span class="sxs-lookup"><span data-stu-id="5a6a8-124">Windows Azure</span></span>

### <a name="supported-server-net-framework-version"></a><span data-ttu-id="5a6a8-125">지원 되는 서버 .NET Framework 버전</span><span class="sxs-lookup"><span data-stu-id="5a6a8-125">Supported server .NET Framework version</span></span>

<span data-ttu-id="5a6a8-126">SignalR 2는 .NET Framework 4.5 에서만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-126">SignalR 2 is only supported on .NET Framework 4.5.</span></span> <span data-ttu-id="5a6a8-127">안정성, 호환성, 안정성 및 성능을 향상 시키는 업데이트는 [권장 업데이트](#updates) 섹션을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-127">See the [Recommended Updates](#updates) section for updates that enhance reliability, compatibility, stability, and performance.</span></span>

### <a name="supported-server-iis-versions"></a><span data-ttu-id="5a6a8-128">지원 되는 서버 IIS 버전</span><span class="sxs-lookup"><span data-stu-id="5a6a8-128">Supported server IIS versions</span></span>

<span data-ttu-id="5a6a8-129">SignalR가 IIS에서 호스팅되는 경우 지원 되는 버전은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-129">When SignalR is hosted in IIS, the following versions are supported.</span></span> <span data-ttu-id="5a6a8-130">개발 (Windows 8 또는 Windows 7) 등의 클라이언트 운영 체제를 사용 하는 경우에는 전체 버전의 IIS 또는 Cassini를 사용 하면 안 됩니다 .이 경우 연결 된 후에 매우 빠르게 도달할 수 있는 동시 연결 수가 10 개로 제한 되기 때문입니다. 일시적으로 다시 설정 되 고 더 이상 사용 되지 않을 때 즉시 삭제 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-130">Note that if a client operating system is used, such as for development (Windows 8 or Windows 7), full versions of IIS or Cassini should not be used, since there will be a limit of 10 simultaneous connections imposed, which will be reached very quickly since connections are transient, frequently re-established, and are not disposed immediately upon no longer being used.</span></span> <span data-ttu-id="5a6a8-131">IIS Express은 클라이언트 운영 체제에서 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-131">IIS Express should be used on client operating systems.</span></span>

<span data-ttu-id="5a6a8-132">또한 SignalR에서 WebSocket을 사용 하려면 IIS 8 또는 IIS 8 Express를 사용 하 고 서버에서 Windows 8, Windows Server 2012 이상을 사용 해야 하며 IIS에서 WebSocket을 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-132">Also note that for SignalR to use WebSocket, IIS 8 or IIS 8 Express must be used, the server must be using Windows 8, Windows Server 2012, or later, and WebSocket must be enabled in IIS.</span></span> <span data-ttu-id="5a6a8-133">IIS에서 WebSocket을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 [iis 8.0 Websocket 프로토콜 지원](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-133">For information on how to enable WebSocket in IIS, see [IIS 8.0 WebSocket Protocol Support](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support).</span></span>

- <span data-ttu-id="5a6a8-134">IIS 8 또는 IIS 8 Express</span><span class="sxs-lookup"><span data-stu-id="5a6a8-134">IIS 8 or IIS 8 Express.</span></span>
- <span data-ttu-id="5a6a8-135">IIS 7 및 7.5.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-135">IIS 7 and 7.5.</span></span> <span data-ttu-id="5a6a8-136">[확장명 없는 url](https://support.microsoft.com/kb/980368) 에 대 한 지원이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-136">Support for [extensionless URLs](https://support.microsoft.com/kb/980368) is required.</span></span>
- <span data-ttu-id="5a6a8-137">IIS는 통합 모드로 실행 해야 합니다. 클래식 모드는 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-137">IIS must be running in integrated mode; classic mode is not supported.</span></span> <span data-ttu-id="5a6a8-138">서버에서 보낸 이벤트 전송을 사용 하 여 클래식 모드에서 IIS를 실행 하는 경우 최대 30 초의 메시지 지연이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-138">Message delays of up to 30 seconds may be experienced if IIS is run in classic mode using the Server-Sent Events transport.</span></span>
- <span data-ttu-id="5a6a8-139">호스팅 응용 프로그램은 완전 신뢰 모드로 실행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-139">The hosting application must be running in full trust mode.</span></span>

## <a name="client-system-requirements"></a><span data-ttu-id="5a6a8-140">클라이언트 시스템 요구 사항</span><span class="sxs-lookup"><span data-stu-id="5a6a8-140">Client system requirements</span></span>

<span data-ttu-id="5a6a8-141">SignalR는 다양 한 클라이언트 플랫폼에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-141">SignalR can be used in a variety of client platforms.</span></span> <span data-ttu-id="5a6a8-142">이 섹션에서는 웹 브라우저, Windows 데스크톱 응용 프로그램, Silverlight 응용 프로그램 및 모바일 장치에서 SignalR를 사용 하기 위한 시스템 요구 사항에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-142">This section describes the system requirements for using SignalR in web browsers, Windows desktop applications, Silverlight applications, and mobile devices.</span></span>

### <a name="web-browsers"></a><span data-ttu-id="5a6a8-143">웹 브라우저</span><span class="sxs-lookup"><span data-stu-id="5a6a8-143">Web browsers</span></span>

<span data-ttu-id="5a6a8-144">SignalR는 다양 한 웹 브라우저에서 사용할 수 있지만 일반적으로 최신 두 버전만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-144">SignalR can be used in a variety of web browsers, but typically, only the latest two versions are supported.</span></span>

<span data-ttu-id="5a6a8-145">브라우저에서 SignalR를 사용 하는 응용 프로그램은 jQuery 버전 1.6.4 또는 최신 버전 (예: 1.7.2, 1.8.2 또는 1.9.1)을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-145">Applications that use SignalR in browsers must use jQuery version 1.6.4 or major later versions (such as 1.7.2, 1.8.2, or 1.9.1).</span></span>

<span data-ttu-id="5a6a8-146">SignalR는 다음 브라우저에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-146">SignalR can be used in the following browsers:</span></span>

- <span data-ttu-id="5a6a8-147">Microsoft Internet Explorer 버전 8, 9, 10 및 11.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-147">Microsoft Internet Explorer versions 8, 9, 10, and 11.</span></span> <span data-ttu-id="5a6a8-148">최신, 데스크톱 및 모바일 버전이 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-148">Modern, Desktop, and Mobile versions are supported.</span></span>
- <span data-ttu-id="5a6a8-149">Mozilla Firefox: Windows 및 Mac 버전 모두 최신 버전-1.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-149">Mozilla Firefox: current version - 1, both Windows and Mac versions.</span></span>
- <span data-ttu-id="5a6a8-150">Google Chrome: Windows 및 Mac 버전의 최신 버전-1.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-150">Google Chrome: current version - 1, both Windows and Mac versions.</span></span>
- <span data-ttu-id="5a6a8-151">Safari: 현재 버전-1, Mac 및 iOS 버전 모두.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-151">Safari: current version - 1, both Mac and iOS versions.</span></span>
- <span data-ttu-id="5a6a8-152">Opera: 현재 버전-1, Windows만 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-152">Opera: current version - 1, Windows only.</span></span>
- <span data-ttu-id="5a6a8-153">Android 브라우저</span><span class="sxs-lookup"><span data-stu-id="5a6a8-153">Android browser</span></span>

<span data-ttu-id="5a6a8-154">특정 브라우저를 요구 하는 것 외에도 SignalR에서 사용 하는 다양 한 전송에는 고유한 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-154">In addition to requiring certain browsers, the various transports that SignalR uses have requirements of their own.</span></span> <span data-ttu-id="5a6a8-155">다음 구성에서는 다음과 같은 전송 작업을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-155">The following transports are supported under the following configurations:</span></span>

<a id="browser"></a>

<span data-ttu-id="5a6a8-156">**웹 브라우저 전송 요구 사항**</span><span class="sxs-lookup"><span data-stu-id="5a6a8-156">**Web Browser Transport Requirements**</span></span>

| <span data-ttu-id="5a6a8-157">전송</span><span class="sxs-lookup"><span data-stu-id="5a6a8-157">Transport</span></span> | <span data-ttu-id="5a6a8-158">Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="5a6a8-158">Internet Explorer</span></span> | <span data-ttu-id="5a6a8-159">Chrome (Windows 또는 iOS)</span><span class="sxs-lookup"><span data-stu-id="5a6a8-159">Chrome (Windows or iOS)</span></span> | <span data-ttu-id="5a6a8-160">Firefox</span><span class="sxs-lookup"><span data-stu-id="5a6a8-160">Firefox</span></span> | <span data-ttu-id="5a6a8-161">Safari (OSX 또는 iOS)</span><span class="sxs-lookup"><span data-stu-id="5a6a8-161">Safari (OSX or iOS)</span></span> | <span data-ttu-id="5a6a8-162">Android</span><span class="sxs-lookup"><span data-stu-id="5a6a8-162">Android</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="5a6a8-163">WebSockets</span><span class="sxs-lookup"><span data-stu-id="5a6a8-163">WebSockets</span></span> | <span data-ttu-id="5a6a8-164">10+</span><span class="sxs-lookup"><span data-stu-id="5a6a8-164">10+</span></span> | <span data-ttu-id="5a6a8-165">현재-1</span><span class="sxs-lookup"><span data-stu-id="5a6a8-165">current - 1</span></span> | <span data-ttu-id="5a6a8-166">현재-1</span><span class="sxs-lookup"><span data-stu-id="5a6a8-166">current - 1</span></span> | <span data-ttu-id="5a6a8-167">현재-1</span><span class="sxs-lookup"><span data-stu-id="5a6a8-167">current - 1</span></span> | <span data-ttu-id="5a6a8-168">해당 없음</span><span class="sxs-lookup"><span data-stu-id="5a6a8-168">N/A</span></span> |
| <span data-ttu-id="5a6a8-169">서버에서 보낸 이벤트</span><span class="sxs-lookup"><span data-stu-id="5a6a8-169">Server-Sent Events</span></span> | <span data-ttu-id="5a6a8-170">해당 없음</span><span class="sxs-lookup"><span data-stu-id="5a6a8-170">N/A</span></span> | <span data-ttu-id="5a6a8-171">현재-1</span><span class="sxs-lookup"><span data-stu-id="5a6a8-171">current - 1</span></span> | <span data-ttu-id="5a6a8-172">현재-1</span><span class="sxs-lookup"><span data-stu-id="5a6a8-172">current - 1</span></span> | <span data-ttu-id="5a6a8-173">현재-1</span><span class="sxs-lookup"><span data-stu-id="5a6a8-173">current - 1</span></span> | <span data-ttu-id="5a6a8-174">해당 없음</span><span class="sxs-lookup"><span data-stu-id="5a6a8-174">N/A</span></span> |
| <span data-ttu-id="5a6a8-175">ForeverFrame</span><span class="sxs-lookup"><span data-stu-id="5a6a8-175">ForeverFrame</span></span> | <span data-ttu-id="5a6a8-176">8+</span><span class="sxs-lookup"><span data-stu-id="5a6a8-176">8+</span></span> | <span data-ttu-id="5a6a8-177">해당 없음</span><span class="sxs-lookup"><span data-stu-id="5a6a8-177">N/A</span></span> | <span data-ttu-id="5a6a8-178">해당 없음</span><span class="sxs-lookup"><span data-stu-id="5a6a8-178">N/A</span></span> | <span data-ttu-id="5a6a8-179">해당 없음</span><span class="sxs-lookup"><span data-stu-id="5a6a8-179">N/A</span></span> | <span data-ttu-id="5a6a8-180">4.1</span><span class="sxs-lookup"><span data-stu-id="5a6a8-180">4.1</span></span> |
| <span data-ttu-id="5a6a8-181">긴 폴링</span><span class="sxs-lookup"><span data-stu-id="5a6a8-181">Long Polling</span></span> | <span data-ttu-id="5a6a8-182">8+</span><span class="sxs-lookup"><span data-stu-id="5a6a8-182">8+</span></span> | <span data-ttu-id="5a6a8-183">현재-1</span><span class="sxs-lookup"><span data-stu-id="5a6a8-183">current - 1</span></span> | <span data-ttu-id="5a6a8-184">현재-1</span><span class="sxs-lookup"><span data-stu-id="5a6a8-184">current - 1</span></span> | <span data-ttu-id="5a6a8-185">현재-1</span><span class="sxs-lookup"><span data-stu-id="5a6a8-185">current - 1</span></span> | <span data-ttu-id="5a6a8-186">4.1</span><span class="sxs-lookup"><span data-stu-id="5a6a8-186">4.1</span></span> |

<span data-ttu-id="5a6a8-187">\*: 6 + 전체 기능에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-187">\*: 6+ required for full functionality.</span></span>

#### <a name="unsupported-browsers"></a><span data-ttu-id="5a6a8-188">지원 되지 않는 브라우저</span><span class="sxs-lookup"><span data-stu-id="5a6a8-188">Unsupported Browsers</span></span>

<span data-ttu-id="5a6a8-189">SignalR는 이전 브라우저 버전에서 중요 한 문제 없이 실행 *될 수* 있지만, SignalR를 적극적으로 테스트 하지 않으며 일반적으로이에 나타날 수 있는 버그를 수정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-189">While SignalR *may* run without major issues in older browser versions, we do not actively test SignalR in them and generally do not fix bugs that may appear in them.</span></span>

### <a name="windows-desktop-and-silverlight-applications"></a><span data-ttu-id="5a6a8-190">Windows 데스크톱 및 Silverlight 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="5a6a8-190">Windows Desktop and Silverlight Applications</span></span>

<span data-ttu-id="5a6a8-191">웹 브라우저에서 실행 하는 것 외에도 SignalR를 독립 실행형 Windows 클라이언트 또는 Silverlight 응용 프로그램에서 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-191">In addition to running in a web browser, SignalR can be hosted in standalone Windows client or Silverlight applications.</span></span> <span data-ttu-id="5a6a8-192">Windows Desktop 및 Silverlight SignalR 응용 프로그램에는 다음과 같은 시스템 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-192">Windows Desktop and Silverlight SignalR applications have the following system requirements.</span></span>

- <span data-ttu-id="5a6a8-193">.NET 4를 사용 하는 응용 프로그램은 Windows XP SP3 이상에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-193">Applications using .NET 4 are supported on Windows XP SP3 or later.</span></span>
- <span data-ttu-id="5a6a8-194">.NET Framework 4.5를 사용 하는 응용 프로그램은 Windows Vista 이상에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-194">Applications using .NET Framework 4.5 are supported on Windows Vista or later.</span></span>

<span data-ttu-id="5a6a8-195">운영 체제 및 .NET framework 요구 사항 외에도 SignalR에서 사용할 수 있는 전송에는 고유한 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-195">In addition to operating system and .NET framework requirements, the transports available to SignalR have requirements of their own.</span></span> <span data-ttu-id="5a6a8-196">다음 구성에서는 다음과 같은 전송 작업을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-196">The following transports are supported under the following configurations:</span></span>

<span data-ttu-id="5a6a8-197">**Windows 데스크톱 및 Silverlight 전송 요구 사항**</span><span class="sxs-lookup"><span data-stu-id="5a6a8-197">**Windows Desktop and Silverlight Transport Requirements**</span></span>

| <span data-ttu-id="5a6a8-198">전송</span><span class="sxs-lookup"><span data-stu-id="5a6a8-198">Transport</span></span> | <span data-ttu-id="5a6a8-199">.NET 애플리케이션</span><span class="sxs-lookup"><span data-stu-id="5a6a8-199">.NET application</span></span> | <span data-ttu-id="5a6a8-200">Silverlight</span><span class="sxs-lookup"><span data-stu-id="5a6a8-200">Silverlight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5a6a8-201">웹 소켓</span><span class="sxs-lookup"><span data-stu-id="5a6a8-201">Web Sockets</span></span> | <span data-ttu-id="5a6a8-202">Windows 8 이상 및 .NET 4.5 이상</span><span class="sxs-lookup"><span data-stu-id="5a6a8-202">Windows 8+ and .NET 4.5+</span></span> | <span data-ttu-id="5a6a8-203">해당 없음</span><span class="sxs-lookup"><span data-stu-id="5a6a8-203">N/A</span></span> |
| <span data-ttu-id="5a6a8-204">영원히 프레임</span><span class="sxs-lookup"><span data-stu-id="5a6a8-204">Forever Frame</span></span> | <span data-ttu-id="5a6a8-205">해당 없음</span><span class="sxs-lookup"><span data-stu-id="5a6a8-205">N/A</span></span> | <span data-ttu-id="5a6a8-206">해당 없음</span><span class="sxs-lookup"><span data-stu-id="5a6a8-206">N/A</span></span> |
| <span data-ttu-id="5a6a8-207">서버에서 보낸 이벤트</span><span class="sxs-lookup"><span data-stu-id="5a6a8-207">Server-Sent Events</span></span> | <span data-ttu-id="5a6a8-208">.NET 4+</span><span class="sxs-lookup"><span data-stu-id="5a6a8-208">.NET 4+</span></span> | <span data-ttu-id="5a6a8-209">5+</span><span class="sxs-lookup"><span data-stu-id="5a6a8-209">5+</span></span> |
| <span data-ttu-id="5a6a8-210">긴 폴링</span><span class="sxs-lookup"><span data-stu-id="5a6a8-210">Long Polling</span></span> | <span data-ttu-id="5a6a8-211">.NET 4+</span><span class="sxs-lookup"><span data-stu-id="5a6a8-211">.NET 4+</span></span> | <span data-ttu-id="5a6a8-212">5+</span><span class="sxs-lookup"><span data-stu-id="5a6a8-212">5+</span></span> |

<a id="android"></a>

### <a name="windows-store-and-windows-phone-applications"></a><span data-ttu-id="5a6a8-213">Windows 스토어 및 Windows Phone 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="5a6a8-213">Windows Store and Windows Phone Applications</span></span>

<span data-ttu-id="5a6a8-214">SignalR는 Windows 스토어 응용 프로그램 및 Windows Phone 8 응용 프로그램에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-214">SignalR can be used in Windows Store applications and Windows Phone 8 applications.</span></span> <span data-ttu-id="5a6a8-215">다음 구성에서는 다음과 같은 전송 작업을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-215">The following transports are supported under the following configurations:</span></span>

<span data-ttu-id="5a6a8-216">**Windows 스토어 및 Windows Phone 전송 요구 사항**</span><span class="sxs-lookup"><span data-stu-id="5a6a8-216">**Windows Store and Windows Phone Transport Requirements**</span></span>

| <span data-ttu-id="5a6a8-217">전송</span><span class="sxs-lookup"><span data-stu-id="5a6a8-217">Transport</span></span> | <span data-ttu-id="5a6a8-218">Windows 스토어/.NET</span><span class="sxs-lookup"><span data-stu-id="5a6a8-218">Windows Store/ .NET</span></span> | <span data-ttu-id="5a6a8-219">Windows 스토어/JavaScript</span><span class="sxs-lookup"><span data-stu-id="5a6a8-219">Windows Store/ JavaScript</span></span> | <span data-ttu-id="5a6a8-220">Windows Phone/IE</span><span class="sxs-lookup"><span data-stu-id="5a6a8-220">Windows Phone/ IE</span></span> | <span data-ttu-id="5a6a8-221">Windows Phone/ .NET</span><span class="sxs-lookup"><span data-stu-id="5a6a8-221">Windows Phone/ .NET</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="5a6a8-222">WebSockets</span><span class="sxs-lookup"><span data-stu-id="5a6a8-222">WebSockets</span></span> | <span data-ttu-id="5a6a8-223">해당 없음</span><span class="sxs-lookup"><span data-stu-id="5a6a8-223">N/A</span></span> | <span data-ttu-id="5a6a8-224">Win8 +</span><span class="sxs-lookup"><span data-stu-id="5a6a8-224">Win8+</span></span> | <span data-ttu-id="5a6a8-225">8+</span><span class="sxs-lookup"><span data-stu-id="5a6a8-225">8+</span></span> | <span data-ttu-id="5a6a8-226">해당 없음</span><span class="sxs-lookup"><span data-stu-id="5a6a8-226">N/A</span></span> |
| <span data-ttu-id="5a6a8-227">영원히 프레임</span><span class="sxs-lookup"><span data-stu-id="5a6a8-227">Forever Frame</span></span> | <span data-ttu-id="5a6a8-228">해당 없음</span><span class="sxs-lookup"><span data-stu-id="5a6a8-228">N/A</span></span> | <span data-ttu-id="5a6a8-229">Win8 +</span><span class="sxs-lookup"><span data-stu-id="5a6a8-229">Win8+</span></span> | <span data-ttu-id="5a6a8-230">7.5+</span><span class="sxs-lookup"><span data-stu-id="5a6a8-230">7.5+</span></span> | <span data-ttu-id="5a6a8-231">해당 없음</span><span class="sxs-lookup"><span data-stu-id="5a6a8-231">N/A</span></span> |
| <span data-ttu-id="5a6a8-232">서버에서 보낸 이벤트</span><span class="sxs-lookup"><span data-stu-id="5a6a8-232">Server-Sent Events</span></span> | <span data-ttu-id="5a6a8-233">Win8 +</span><span class="sxs-lookup"><span data-stu-id="5a6a8-233">Win8+</span></span> | <span data-ttu-id="5a6a8-234">해당 없음</span><span class="sxs-lookup"><span data-stu-id="5a6a8-234">N/A</span></span> | <span data-ttu-id="5a6a8-235">해당 없음</span><span class="sxs-lookup"><span data-stu-id="5a6a8-235">N/A</span></span> | <span data-ttu-id="5a6a8-236">8+</span><span class="sxs-lookup"><span data-stu-id="5a6a8-236">8+</span></span> |
| <span data-ttu-id="5a6a8-237">긴 폴링</span><span class="sxs-lookup"><span data-stu-id="5a6a8-237">Long Polling</span></span> | <span data-ttu-id="5a6a8-238">Win8 +</span><span class="sxs-lookup"><span data-stu-id="5a6a8-238">Win8+</span></span> | <span data-ttu-id="5a6a8-239">Win8 +</span><span class="sxs-lookup"><span data-stu-id="5a6a8-239">Win8+</span></span> | <span data-ttu-id="5a6a8-240">7.5+</span><span class="sxs-lookup"><span data-stu-id="5a6a8-240">7.5+</span></span> | <span data-ttu-id="5a6a8-241">8+</span><span class="sxs-lookup"><span data-stu-id="5a6a8-241">8+</span></span> |

<a id="updates"></a>

## <a name="recommended-updates"></a><span data-ttu-id="5a6a8-242">권장 업데이트</span><span class="sxs-lookup"><span data-stu-id="5a6a8-242">Recommended Updates</span></span>

<span data-ttu-id="5a6a8-243">SignalR 서버에 권장 되는 업데이트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-243">The following updates are recommended for SignalR servers:</span></span>

- <span data-ttu-id="5a6a8-244">.NET Framework 4.5에 대 한 업데이트는 [여기](https://support.microsoft.com/kb/2750149)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-244">An update for .NET Framework 4.5 is available [here](https://support.microsoft.com/kb/2750149).</span></span>
- <span data-ttu-id="5a6a8-245">Microsoft는 ASP.NET 용 Qfe를 주기적으로 릴리스 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-245">Microsoft will periodically release QFEs for ASP.NET.</span></span> <span data-ttu-id="5a6a8-246">사용 가능한 것으로 적용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6a8-246">These should be applied as available.</span></span>
