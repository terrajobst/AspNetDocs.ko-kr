---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-cs
title: 사용자 지정 경로 제약 조건 만들기C#() | Microsoft Docs
author: StephenWalther
description: Stephen Walther는 사용자 지정 경로 제약 조건을 만드는 방법을 보여 줍니다. 경로가 일치 하는 것을 방지 하는 간단한 사용자 지정 제약 조건을 구현 합니다.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: a4f4bf4e-abcc-4650-8f43-527e48b52fe6
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-cs
msc.type: authoredcontent
ms.openlocfilehash: 98d5839e3d2623665770ccc5689c28f9eb29c8f6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486827"
---
# <a name="creating-a-custom-route-constraint-c"></a><span data-ttu-id="22350-104">사용자 지정 경로 제약 조건 만들기(C#)</span><span class="sxs-lookup"><span data-stu-id="22350-104">Creating a Custom Route Constraint (C#)</span></span>

<span data-ttu-id="22350-105">[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="22350-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="22350-106">Stephen Walther는 사용자 지정 경로 제약 조건을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="22350-106">Stephen Walther demonstrates how you can create a custom route constraint.</span></span> <span data-ttu-id="22350-107">원격 컴퓨터에서 브라우저 요청을 수행할 때 경로가 일치 하지 않도록 하는 간단한 사용자 지정 제약 조건을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="22350-107">We implement a simple custom constraint that prevents a route from being matched when a browser request is made from a remote computer.</span></span>

<span data-ttu-id="22350-108">이 자습서의 목표는 사용자 지정 경로 제약 조건을 만드는 방법을 보여 주는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="22350-108">The goal of this tutorial is to demonstrate how you can create a custom route constraint.</span></span> <span data-ttu-id="22350-109">사용자 지정 경로 제약 조건을 사용 하면 일부 사용자 지정 조건이 일치 하지 않는 한 경로가 일치 하지 않도록 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22350-109">A custom route constraint enables you to prevent a route from being matched unless some custom condition is matched.</span></span>

<span data-ttu-id="22350-110">이 자습서에서는 Localhost 경로 제약 조건을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22350-110">In this tutorial, we create a Localhost route constraint.</span></span> <span data-ttu-id="22350-111">Localhost 경로 제약 조건은 로컬 컴퓨터에서 수행 된 요청만 일치 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="22350-111">The Localhost route constraint only matches requests made from the local computer.</span></span> <span data-ttu-id="22350-112">인터넷을 통한 원격 요청이 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22350-112">Remote requests from across the Internet are not matched.</span></span>

<span data-ttu-id="22350-113">IRouteConstraint 인터페이스를 구현 하 여 사용자 지정 경로 제약 조건을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="22350-113">You implement a custom route constraint by implementing the IRouteConstraint interface.</span></span> <span data-ttu-id="22350-114">이는 단일 메서드를 설명 하는 매우 간단한 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="22350-114">This is an extremely simple interface which describes a single method:</span></span>

[!code-csharp[Main](creating-a-custom-route-constraint-cs/samples/sample1.cs)]

<span data-ttu-id="22350-115">메서드는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="22350-115">The method returns a Boolean value.</span></span> <span data-ttu-id="22350-116">False를 반환 하는 경우 제약 조건과 연결 된 경로가 브라우저 요청과 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22350-116">If you return false, the route associated with the constraint won't match the browser request.</span></span>

<span data-ttu-id="22350-117">Localhost 제약 조건은 목록 1에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22350-117">The Localhost constraint is contained in Listing 1.</span></span>

<span data-ttu-id="22350-118">**목록 1-LocalhostConstraint.cs**</span><span class="sxs-lookup"><span data-stu-id="22350-118">**Listing 1 - LocalhostConstraint.cs**</span></span>

[!code-csharp[Main](creating-a-custom-route-constraint-cs/samples/sample2.cs)]

<span data-ttu-id="22350-119">목록 1의 제약 조건은 HttpRequest 클래스에 의해 노출 된 IsLocal 속성을 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="22350-119">The constraint in Listing 1 takes advantage of the IsLocal property exposed by the HttpRequest class.</span></span> <span data-ttu-id="22350-120">요청의 IP 주소가 127.0.0.1 이거나 요청의 IP가 서버의 IP 주소와 동일한 경우이 속성은 true를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="22350-120">This property returns true when the IP address of the request is either 127.0.0.1 or when the IP of the request is the same as the server's IP address.</span></span>

<span data-ttu-id="22350-121">Global.asax 파일에 정의 된 경로 내에서 사용자 지정 제약 조건을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="22350-121">You use a custom constraint within a route defined in the Global.asax file.</span></span> <span data-ttu-id="22350-122">목록 2의 Global.asax 파일은 Localhost 제약 조건을 사용 하 여 로컬 서버에서 요청을 수행 하지 않는 한 관리 페이지를 요청 하지 못하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="22350-122">The Global.asax file in Listing 2 uses the Localhost constraint to prevent anyone from requesting an Admin page unless they make the request from the local server.</span></span> <span data-ttu-id="22350-123">예를 들어 원격 서버에서/Admin/DeleteAll에 대 한 요청을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="22350-123">For example, a request for /Admin/DeleteAll will fail when made from a remote server.</span></span>

<span data-ttu-id="22350-124">**목록 2-global.asax**</span><span class="sxs-lookup"><span data-stu-id="22350-124">**Listing 2 - Global.asax**</span></span>

[!code-csharp[Main](creating-a-custom-route-constraint-cs/samples/sample3.cs)]

<span data-ttu-id="22350-125">Localhost 제약 조건은 관리자 경로 정의에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22350-125">The Localhost constraint is used in the definition of the Admin route.</span></span> <span data-ttu-id="22350-126">이 경로는 원격 브라우저 요청과 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22350-126">This route won't be matched by a remote browser request.</span></span> <span data-ttu-id="22350-127">그러나 Global.asax에 정의 된 다른 경로는 동일한 요청과 일치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22350-127">Realize, however, that other routes defined in Global.asax might match the same request.</span></span> <span data-ttu-id="22350-128">제약 조건으로 인해 특정 경로는 Global.asax 파일에 정의 된 모든 경로가 아니라 요청과 일치 하지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22350-128">It is important to understand that a constraint prevents a particular route from matching a request and not all routes defined in the Global.asax file.</span></span>

<span data-ttu-id="22350-129">기본 경로는 목록 2의 Global.asax 파일에서 주석으로 처리 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="22350-129">Notice that the Default route has been commented out from the Global.asax file in Listing 2.</span></span> <span data-ttu-id="22350-130">기본 경로를 포함 하는 경우 기본 경로는 관리 컨트롤러에 대 한 요청과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="22350-130">If you include the Default route, then the Default route would match requests for the Admin controller.</span></span> <span data-ttu-id="22350-131">이 경우에는 요청이 관리자 경로와 일치 하지 않더라도 원격 사용자는 여전히 관리 컨트롤러의 작업을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22350-131">In that case, remote users could still invoke actions of the Admin controller even though their requests wouldn't match the Admin route.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="22350-132">[이전](creating-a-route-constraint-cs.md)
> [다음](asp-net-mvc-controller-overview-vb.md)</span><span class="sxs-lookup"><span data-stu-id="22350-132">[Previous](creating-a-route-constraint-cs.md)
[Next](asp-net-mvc-controller-overview-vb.md)</span></span>
