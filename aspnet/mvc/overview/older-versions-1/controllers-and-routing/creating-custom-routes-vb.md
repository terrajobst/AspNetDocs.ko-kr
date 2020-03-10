---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
title: 사용자 지정 경로 만들기 (VB) | Microsoft Docs
author: microsoft
description: ASP.NET MVC 응용 프로그램에 사용자 지정 경로를 추가 하는 방법에 대해 알아봅니다. 이 자습서에서는 global.asax 파일에서 기본 경로 테이블을 수정 하는 방법에 대해 알아봅니다.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 6ac5758b-6199-42af-adcb-21954b864951
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
msc.type: authoredcontent
ms.openlocfilehash: 22b44e9e575c9d404881a23ee735bb0c8b7109e1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486695"
---
# <a name="creating-custom-routes-vb"></a><span data-ttu-id="0b9e7-104">사용자 지정 경로 만들기(VB)</span><span class="sxs-lookup"><span data-stu-id="0b9e7-104">Creating Custom Routes (VB)</span></span>

<span data-ttu-id="0b9e7-105">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="0b9e7-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="0b9e7-106">ASP.NET MVC 응용 프로그램에 사용자 지정 경로를 추가 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0b9e7-106">Learn how to add custom routes to an ASP.NET MVC application.</span></span> <span data-ttu-id="0b9e7-107">이 자습서에서는 global.asax 파일에서 기본 경로 테이블을 수정 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0b9e7-107">In this tutorial, you learn how to modify the default route table in the Global.asax file.</span></span>

<span data-ttu-id="0b9e7-108">이 자습서에서는 ASP.NET MVC 응용 프로그램에 사용자 지정 경로를 추가 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0b9e7-108">In this tutorial, you learn how to add a custom route to an ASP.NET MVC application.</span></span> <span data-ttu-id="0b9e7-109">사용자 지정 경로를 사용 하 여 Global.asax 파일에서 기본 경로 테이블을 수정 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0b9e7-109">You learn how to modify the default route table in the Global.asax file with a custom route.</span></span>

<span data-ttu-id="0b9e7-110">ASP.NET MVC 응용 프로그램에서 기본 경로 테이블은 정상적으로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b9e7-110">In ASP.NET MVC applications, the default route table will work just fine.</span></span> <span data-ttu-id="0b9e7-111">그러나 특별 한 라우팅 요구 사항이 있다는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b9e7-111">However, you might discover that you have specialized routing needs.</span></span> <span data-ttu-id="0b9e7-112">이 경우 사용자 지정 경로를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b9e7-112">In that case, you can create a custom route.</span></span>

<span data-ttu-id="0b9e7-113">예를 들어, 블로그 응용 프로그램을 빌드하는 경우를 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0b9e7-113">Imagine, for example, that you are building a blog application.</span></span> <span data-ttu-id="0b9e7-114">다음과 같은 들어오는 요청을 처리 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0b9e7-114">You might want to handle incoming requests that look like this:</span></span>

<span data-ttu-id="0b9e7-115">/Archive/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="0b9e7-115">/Archive/12-25-2009</span></span>

<span data-ttu-id="0b9e7-116">사용자가이 요청을 입력 하면 날짜 12/25/2009에 해당 하는 블로그 항목을 반환 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b9e7-116">When a user enters this request, you want to return the blog entry that corresponds to the date 12/25/2009.</span></span> <span data-ttu-id="0b9e7-117">이러한 유형의 요청을 처리 하려면 사용자 지정 경로를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b9e7-117">In order to handle this type of request, you need to create a custom route.</span></span>

<span data-ttu-id="0b9e7-118">1을 나열 하는 Global.asax 파일에는/Archive/*entry date*와 같은 요청을 처리 하는 새 사용자 지정 경로 라는 이름이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b9e7-118">The Global.asax file in Listing 1 contains a new custom route, named Blog, which handles requests that look like /Archive/*entry date*.</span></span>

<span data-ttu-id="0b9e7-119">**목록 1-global.asax (사용자 지정 경로 사용)**</span><span class="sxs-lookup"><span data-stu-id="0b9e7-119">**Listing 1 - Global.asax (with custom route)**</span></span>

[!code-vb[Main](creating-custom-routes-vb/samples/sample1.vb)]

<span data-ttu-id="0b9e7-120">경로 테이블에 추가 하는 경로의 순서는 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b9e7-120">The order of the routes that you add to the route table is important.</span></span> <span data-ttu-id="0b9e7-121">새 사용자 지정 블로그 경로가 기존 기본 경로 앞에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b9e7-121">Our new custom Blog route is added before the existing Default route.</span></span> <span data-ttu-id="0b9e7-122">순서를 반대로 하면 기본 경로가 항상 사용자 지정 경로 대신 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b9e7-122">If you reversed the order, then the Default route always will get called instead of the custom route.</span></span>

<span data-ttu-id="0b9e7-123">사용자 지정 블로그 경로는/Archive/.로 시작 하는 모든 요청과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b9e7-123">The custom Blog route matches any request that starts with /Archive/.</span></span> <span data-ttu-id="0b9e7-124">따라서 다음 Url이 모두 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b9e7-124">So, it matches all of the following URLs:</span></span>

- <span data-ttu-id="0b9e7-125">/Archive/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="0b9e7-125">/Archive/12-25-2009</span></span>

- <span data-ttu-id="0b9e7-126">/Archive/10-6-2004</span><span class="sxs-lookup"><span data-stu-id="0b9e7-126">/Archive/10-6-2004</span></span>

- <span data-ttu-id="0b9e7-127">/Archive/apple</span><span class="sxs-lookup"><span data-stu-id="0b9e7-127">/Archive/apple</span></span>

<span data-ttu-id="0b9e7-128">사용자 지정 경로는 수신 된 요청을 Archive 컨트롤러에 매핑하고 Entry () 작업을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b9e7-128">The custom route maps the incoming request to a controller named Archive and invokes the Entry() action.</span></span> <span data-ttu-id="0b9e7-129">Entry () 메서드를 호출 하면 항목 날짜가 entryDate 라는 매개 변수로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b9e7-129">When the Entry() method is called, the entry date is passed as a parameter named entryDate.</span></span>

<span data-ttu-id="0b9e7-130">목록 2의 컨트롤러와 함께 블로그 사용자 지정 경로를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b9e7-130">You can use the Blog custom route with the controller in Listing 2.</span></span>

<span data-ttu-id="0b9e7-131">**목록 2-ArchiveController**</span><span class="sxs-lookup"><span data-stu-id="0b9e7-131">**Listing 2 - ArchiveController.vb**</span></span>

[!code-vb[Main](creating-custom-routes-vb/samples/sample2.vb)]

<span data-ttu-id="0b9e7-132">목록 2의 Entry () 메서드는 DateTime 형식의 매개 변수를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b9e7-132">Notice that the Entry() method in Listing 2 accepts a parameter of type DateTime.</span></span> <span data-ttu-id="0b9e7-133">MVC 프레임 워크는 URL의 항목 날짜를 자동으로 DateTime 값으로 변환할 수 있을 정도로 지능적입니다.</span><span class="sxs-lookup"><span data-stu-id="0b9e7-133">The MVC framework is smart enough to convert the entry date from the URL into a DateTime value automatically.</span></span> <span data-ttu-id="0b9e7-134">URL의 entry date 매개 변수를 DateTime으로 변환할 수 없는 경우 오류가 발생 합니다 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="0b9e7-134">If the entry date parameter from the URL cannot be converted to a DateTime, an error is raised (see Figure 1).</span></span>

<span data-ttu-id="0b9e7-135">**그림 1-변환 매개 변수 오류**</span><span class="sxs-lookup"><span data-stu-id="0b9e7-135">**Figure 1 - Error from converting parameter**</span></span>

<span data-ttu-id="0b9e7-136">[새 프로젝트 대화 상자 ![](creating-custom-routes-vb/_static/image1.jpg)](creating-custom-routes-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0b9e7-136">[![The New Project dialog box](creating-custom-routes-vb/_static/image1.jpg)](creating-custom-routes-vb/_static/image1.png)</span></span>

<span data-ttu-id="0b9e7-137">**그림 01**: 매개 변수 변환 오류 ([전체 크기 이미지를 보려면 클릭](creating-custom-routes-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="0b9e7-137">**Figure 01**: Error from converting parameter ([Click to view full-size image](creating-custom-routes-vb/_static/image2.png))</span></span>

## <a name="summary"></a><span data-ttu-id="0b9e7-138">요약</span><span class="sxs-lookup"><span data-stu-id="0b9e7-138">Summary</span></span>

<span data-ttu-id="0b9e7-139">이 자습서의 목표는 사용자 지정 경로를 만드는 방법을 설명 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0b9e7-139">The goal of this tutorial was to demonstrate how you can create a custom route.</span></span> <span data-ttu-id="0b9e7-140">블로그 항목을 나타내는 global.asax 파일의 경로 테이블에 사용자 지정 경로를 추가 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="0b9e7-140">You learned how to add a custom route to the route table in the Global.asax file that represents blog entries.</span></span> <span data-ttu-id="0b9e7-141">블로그 항목에 대 한 요청을 ArchiveController 이라는 컨트롤러에 매핑하는 방법과 Entry () 라는 컨트롤러 작업을 매핑하는 방법에 대해 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0b9e7-141">We discussed how to map requests for blog entries to a controller named ArchiveController and a controller action named Entry().</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0b9e7-142">[이전](asp-net-mvc-controller-overview-vb.md)
> [다음](creating-a-route-constraint-vb.md)</span><span class="sxs-lookup"><span data-stu-id="0b9e7-142">[Previous](asp-net-mvc-controller-overview-vb.md)
[Next](creating-a-route-constraint-vb.md)</span></span>
