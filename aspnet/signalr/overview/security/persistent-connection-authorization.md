---
uid: signalr/overview/security/persistent-connection-authorization
title: SignalR 영구 연결에 대 한 인증 및 권한 부여 | Microsoft Docs
author: bradygaster
description: 이 항목에서는 영구 연결에 대 한 권한 부여를 적용 하는 방법에 대해 설명 합니다. 보안을 SignalR 응용 프로그램에 통합 하는 방법에 대 한 일반적인 정보는,...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: e264677b-9c01-47ec-94f9-3cd8f08f94af
msc.legacyurl: /signalr/overview/security/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: 7e69d3c1a18f1239142891734ba58cd2b0078f84
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467477"
---
# <a name="authentication-and-authorization-for-signalr-persistent-connections"></a><span data-ttu-id="80430-104">SignalR 영구 연결에 대한 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="80430-104">Authentication and Authorization for SignalR Persistent Connections</span></span>

<span data-ttu-id="80430-105">[Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="80430-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="80430-106">이 항목에서는 영구 연결에 대 한 권한 부여를 적용 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="80430-106">This topic describes how to enforce authorization on a persistent connection.</span></span> <span data-ttu-id="80430-107">보안을 SignalR 응용 프로그램에 통합 하는 방법에 대 한 일반적인 내용은 [보안 소개](introduction-to-security.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="80430-107">For general information about integrating security into a SignalR application, see [Introduction to Security](introduction-to-security.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="80430-108">이 항목에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="80430-108">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="80430-109">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="80430-109">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="80430-110">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="80430-110">.NET 4.5</span></span>
> - <span data-ttu-id="80430-111">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="80430-111">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="80430-112">이 항목의 이전 버전</span><span class="sxs-lookup"><span data-stu-id="80430-112">Previous versions of this topic</span></span>
>
> <span data-ttu-id="80430-113">이전 버전의 SignalR에 대 한 자세한 내용은 [SignalR 이전 버전](../older-versions/index.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="80430-113">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="80430-114">질문 및 설명</span><span class="sxs-lookup"><span data-stu-id="80430-114">Questions and comments</span></span>
>
> <span data-ttu-id="80430-115">이 자습서와 페이지 맨 아래에 있는 의견에서 개선할 수 있는 방법에 대 한 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="80430-115">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="80430-116">자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80430-116">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="enforce-authorization"></a><span data-ttu-id="80430-117">권한 부여 적용</span><span class="sxs-lookup"><span data-stu-id="80430-117">Enforce authorization</span></span>

<span data-ttu-id="80430-118">[PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) 를 사용할 때 권한 부여 규칙을 적용 하려면 `AuthorizeRequest` 메서드를 재정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80430-118">To enforce authorization rules when using a [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) you must override the `AuthorizeRequest` method.</span></span> <span data-ttu-id="80430-119">영구 연결에는 `Authorize` 특성을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="80430-119">You cannot use the `Authorize` attribute with persistent connections.</span></span> <span data-ttu-id="80430-120">`AuthorizeRequest` 메서드는 요청 된 작업을 수행할 수 있는 권한이 사용자에 게 있는지 확인 하기 위해 모든 요청 이전에 SignalR 프레임 워크에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80430-120">The `AuthorizeRequest` method is called by the SignalR Framework before every request to verify that the user is authorized to perform the requested action.</span></span> <span data-ttu-id="80430-121">`AuthorizeRequest` 메서드가 클라이언트에서 호출 되지 않습니다. 대신 응용 프로그램의 표준 인증 메커니즘을 통해 사용자를 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="80430-121">The `AuthorizeRequest` method is not called from the client; instead, you authenticate the user through your application's standard authentication mechanism.</span></span>

<span data-ttu-id="80430-122">아래 예제에서는 요청을 인증 된 사용자로 제한 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="80430-122">The example below shows how to limit requests to authenticated users.</span></span>

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

<span data-ttu-id="80430-123">AuthorizeRequest 메서드에서 사용자 지정 된 권한 부여 논리를 추가할 수 있습니다. 예를 들어 사용자가 특정 역할에 속하는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="80430-123">You can add any customized authorization logic in the AuthorizeRequest method; such as, checking whether a user belongs to a particular role.</span></span>
