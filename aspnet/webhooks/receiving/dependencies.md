---
uid: webhooks/receiving/dependencies
title: ASP.NET WebHooks 수신기 종속성 | Microsoft Docs
author: rick-anderson
description: ASP.NET 웹 후크에 받는 사람 종속성 및 종속성 주입.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.openlocfilehash: 477b8828209d0da1d485ef883b0f99b4e1b9b5bf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517529"
---
# <a name="aspnet-webhooks-receiver-dependencies"></a><span data-ttu-id="0a8a7-103">ASP.NET WebHooks 수신기 종속성</span><span class="sxs-lookup"><span data-stu-id="0a8a7-103">ASP.NET WebHooks receiver dependencies</span></span>

<span data-ttu-id="0a8a7-104">Microsoft ASP.NET 웹 후크는 종속성 주입을 염두에 두면 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0a8a7-104">Microsoft ASP.NET WebHooks is designed with dependency injection in mind.</span></span> <span data-ttu-id="0a8a7-105">시스템의 대부분 종속성은 종속성 주입 엔진을 사용 하 여 대체 구현으로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a8a7-105">Most dependencies in the system can be replaced with alternative implementations using a dependency injection engine.</span></span>

<span data-ttu-id="0a8a7-106">수신자 종속성 목록은 [DependencyScopeExtensions](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0a8a7-106">See [DependencyScopeExtensions](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) for a list of receiver dependencies.</span></span> <span data-ttu-id="0a8a7-107">종속성이 등록 되지 않은 경우 기본 구현이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a8a7-107">If no dependency has been registered, a default implementation is used.</span></span> <span data-ttu-id="0a8a7-108">기본 구현 목록은 [ReceiverServices](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0a8a7-108">See [ReceiverServices](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) for a list of default implementations.</span></span>
