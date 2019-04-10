---
uid: mvc/overview/older-versions-1/controllers-and-routing/index
title: 컨트롤러 및 라우팅 | Microsoft Docs
author: rick-anderson
description: 이 자습서 집합에 알아봅니다 ASP.NET 라우팅에 대 한 브라우저 요청을 ASP.NET MVC 컨트롤러 작업에 매핑하는 합니다.
ms.author: riande
ms.date: 09/28/2011
ms.assetid: 124df537-428c-4861-b6c2-4830c094fe0c
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing
msc.type: chapter
ms.openlocfilehash: 1a994b37faefe0e20c99a6991768898185e51b43
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59417223"
---
# <a name="controllers-and-routing"></a><span data-ttu-id="0e665-103">컨트롤러 및 라우팅</span><span class="sxs-lookup"><span data-stu-id="0e665-103">Controllers and Routing</span></span>

> <span data-ttu-id="0e665-104">이 자습서 집합에 알아봅니다 ASP.NET 라우팅에 대 한 브라우저 요청을 ASP.NET MVC 컨트롤러 작업에 매핑하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e665-104">In this tutorial set, you learn about ASP.NET routing, which maps browser requests to ASP.NET MVC controller actions.</span></span>


- [<span data-ttu-id="0e665-105">ASP.NET MVC 라우팅 개요(C#)</span><span class="sxs-lookup"><span data-stu-id="0e665-105">ASP.NET MVC Routing Overview (C#)</span></span>](asp-net-mvc-routing-overview-cs.md)
- [<span data-ttu-id="0e665-106">작업 필터 이해(C#)</span><span class="sxs-lookup"><span data-stu-id="0e665-106">Understanding Action Filters (C#)</span></span>](understanding-action-filters-cs.md)
- [<span data-ttu-id="0e665-107">출력 캐싱을 통한 성능 향상(C#)</span><span class="sxs-lookup"><span data-stu-id="0e665-107">Improving Performance with Output Caching (C#)</span></span>](improving-performance-with-output-caching-cs.md)
- [<span data-ttu-id="0e665-108">캐시된 페이지에 동적 콘텐츠 추가(C#)</span><span class="sxs-lookup"><span data-stu-id="0e665-108">Adding Dynamic Content to a Cached Page (C#)</span></span>](adding-dynamic-content-to-a-cached-page-cs.md)
- [<span data-ttu-id="0e665-109">컨트롤러 만들기(C#)</span><span class="sxs-lookup"><span data-stu-id="0e665-109">Creating a Controller (C#)</span></span>](creating-a-controller-cs.md)
- [<span data-ttu-id="0e665-110">작업 만들기(C#)</span><span class="sxs-lookup"><span data-stu-id="0e665-110">Creating an Action (C#)</span></span>](creating-an-action-cs.md)
- [<span data-ttu-id="0e665-111">ASP.NET MVC 라우팅 개요(VB)</span><span class="sxs-lookup"><span data-stu-id="0e665-111">ASP.NET MVC Routing Overview (VB)</span></span>](asp-net-mvc-routing-overview-vb.md)
- [<span data-ttu-id="0e665-112">작업 필터 이해(VB)</span><span class="sxs-lookup"><span data-stu-id="0e665-112">Understanding Action Filters (VB)</span></span>](understanding-action-filters-vb.md)
- [<span data-ttu-id="0e665-113">출력 캐싱을 통한 성능 향상(VB)</span><span class="sxs-lookup"><span data-stu-id="0e665-113">Improving Performance with Output Caching (VB)</span></span>](improving-performance-with-output-caching-vb.md)
- [<span data-ttu-id="0e665-114">캐시된 페이지에 동적 콘텐츠 추가(VB)</span><span class="sxs-lookup"><span data-stu-id="0e665-114">Adding Dynamic Content to a Cached Page (VB)</span></span>](adding-dynamic-content-to-a-cached-page-vb.md)
- [<span data-ttu-id="0e665-115">컨트롤러 만들기(VB)</span><span class="sxs-lookup"><span data-stu-id="0e665-115">Creating a Controller (VB)</span></span>](creating-a-controller-vb.md)
- [<span data-ttu-id="0e665-116">작업 만들기(VB)</span><span class="sxs-lookup"><span data-stu-id="0e665-116">Creating an Action (VB)</span></span>](creating-an-action-vb.md)
- [<span data-ttu-id="0e665-117">ASP.NET MVC 컨트롤러 개요(C#)</span><span class="sxs-lookup"><span data-stu-id="0e665-117">ASP.NET MVC Controller Overview (C#)</span></span>](aspnet-mvc-controllers-overview-cs.md)
- [<span data-ttu-id="0e665-118">사용자 지정 경로 만들기(C#)</span><span class="sxs-lookup"><span data-stu-id="0e665-118">Creating Custom Routes (C#)</span></span>](creating-custom-routes-cs.md)
- [<span data-ttu-id="0e665-119">경로 제약 조건 만들기(C#)</span><span class="sxs-lookup"><span data-stu-id="0e665-119">Creating a Route Constraint (C#)</span></span>](creating-a-route-constraint-cs.md)
- [<span data-ttu-id="0e665-120">사용자 지정 경로 제약 조건 만들기(C#)</span><span class="sxs-lookup"><span data-stu-id="0e665-120">Creating a Custom Route Constraint (C#)</span></span>](creating-a-custom-route-constraint-cs.md)
- [<span data-ttu-id="0e665-121">ASP.NET MVC 컨트롤러 개요(VB)</span><span class="sxs-lookup"><span data-stu-id="0e665-121">ASP.NET MVC Controller Overview (VB)</span></span>](asp-net-mvc-controller-overview-vb.md)
- [<span data-ttu-id="0e665-122">사용자 지정 경로 만들기(VB)</span><span class="sxs-lookup"><span data-stu-id="0e665-122">Creating Custom Routes (VB)</span></span>](creating-custom-routes-vb.md)
- [<span data-ttu-id="0e665-123">경로 제약 조건 만들기(VB)</span><span class="sxs-lookup"><span data-stu-id="0e665-123">Creating a Route Constraint (VB)</span></span>](creating-a-route-constraint-vb.md)
- [<span data-ttu-id="0e665-124">사용자 지정 경로 제약 조건 만들기(VB)</span><span class="sxs-lookup"><span data-stu-id="0e665-124">Creating a Custom Route Constraint (VB)</span></span>](creating-a-custom-route-constraint-vb.md)
