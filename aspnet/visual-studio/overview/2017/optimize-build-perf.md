---
uid: visual-studio/overview/2017/optimize-build-perf
title: 솔루션에 대한 빌드 성능 최적화
author: AngelosP
description: 솔루션에 대한 빌드 성능 최적화
ms.author: riande
ms.date: 08/29/2018
msc.type: authoredcontent
ms.openlocfilehash: c1a5cf5e59374b4c0dd7150c5dd62fbde42af555
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504977"
---
# <a name="optimize-build-performance-for-solution"></a><span data-ttu-id="ca275-103">솔루션에 대한 빌드 성능 최적화</span><span class="sxs-lookup"><span data-stu-id="ca275-103">Optimize build performance for solution</span></span>

<span data-ttu-id="ca275-104">Visual Studio 2017 15.8 이상에는 메뉴 항목이 포함 되어 있습니다. **빌드** > **ASP.NET 컴파일** > **솔루션에 대 한 빌드 성능 최적화**.</span><span class="sxs-lookup"><span data-stu-id="ca275-104">Visual Studio 2017 15.8 or later include a menu item: **Build** > **ASP.NET Compilation** > **Optimize Build Performance for Solution**.</span></span>

![새 메뉴 항목의 스크린샷](optimize-build-perf/_static/optimize-build-performance-for-solution.png)

<span data-ttu-id="ca275-106">ASP.NET는 런타임에 뷰를 컴파일합니다. 즉, ASP.NET 프로젝트가 컴파일러의 복사본과 함께 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca275-106">ASP.NET compiles its views at runtime, which means that an ASP.NET project carries with it a copy of the compiler.</span></span> <span data-ttu-id="ca275-107">그러나 컴파일러의 복사본이 Visual Studio의 복사본과 일치 하지 않는 개발자 컴퓨터에서는 빌드 성능이 증분 빌드 당 1-3 초 순서로 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="ca275-107">However on a developer machine when the copy of the compiler doesn't match Visual Studio's copy, build performance is impacted on the order of 1-3 seconds per incremental build.</span></span> <span data-ttu-id="ca275-108">이 기능은 Visual Studio의 프로젝트 복사본을 업데이트 하 여 일반적으로 증분 빌드의 속도를 향상 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="ca275-108">This feature updates your project's copy of the compiler to match Visual Studio's, which usually speeds up incremental builds.</span></span>

<span data-ttu-id="ca275-109">**ASP.NET Framework 4.7.1 이상 프로젝트에만 적용 되 고 ASP.NET Core에는 적용 되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="ca275-109">**This is applicable to ASP.NET Framework 4.7.1 or later projects only, it does not apply to ASP.NET Core.**</span></span>
