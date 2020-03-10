---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-vb
title: 경로 제약 조건 만들기 (VB) | Microsoft Docs
author: StephenWalther
description: 이 자습서에서 Stephen Walther은 정규식을 사용 하 여 경로 제약 조건을 만들어 브라우저에서 경로를 검색 하는 방식을 제어 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: b7cce113-c82c-45bf-b97b-357e5d9f7f56
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-vb
msc.type: authoredcontent
ms.openlocfilehash: 205742dd8f866c8828008c8aac7ab3f98b173ceb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486773"
---
# <a name="creating-a-route-constraint-vb"></a><span data-ttu-id="e1aaa-103">경로 제약 조건 만들기(VB)</span><span class="sxs-lookup"><span data-stu-id="e1aaa-103">Creating a Route Constraint (VB)</span></span>

<span data-ttu-id="e1aaa-104">[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="e1aaa-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="e1aaa-105">이 자습서에서 Stephen Walther은 정규식을 사용 하 여 경로 제약 조건을 만들어 브라우저에서 경로를 검색 하는 방식을 제어 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e1aaa-105">In this tutorial, Stephen Walther demonstrates how you can control how browser requests match routes by creating route constraints with regular expressions.</span></span>

<span data-ttu-id="e1aaa-106">경로 제약 조건을 사용 하 여 특정 경로와 일치 하는 브라우저 요청을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1aaa-106">You use route constraints to restrict the browser requests that match a particular route.</span></span> <span data-ttu-id="e1aaa-107">정규식을 사용 하 여 경로 제약 조건을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1aaa-107">You can use a regular expression to specify a route constraint.</span></span>

<span data-ttu-id="e1aaa-108">예를 들어 Global.asax 파일에서 목록 1에 경로를 정의 했다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e1aaa-108">For example, imagine that you have defined the route in Listing 1 in your Global.asax file.</span></span>

<span data-ttu-id="e1aaa-109">**목록 1-global.asax .vb**</span><span class="sxs-lookup"><span data-stu-id="e1aaa-109">**Listing 1 - Global.asax.vb**</span></span>

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample1.vb)]

<span data-ttu-id="e1aaa-110">목록 1에는 Product 라는 경로가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1aaa-110">Listing 1 contains a route named Product.</span></span> <span data-ttu-id="e1aaa-111">제품 경로를 사용 하 여 브라우저 요청을 목록 2에 포함 된 제품 컨트롤러에 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1aaa-111">You can use the Product route to map browser requests to the ProductController contained in Listing 2.</span></span>

<span data-ttu-id="e1aaa-112">**목록 2-Controllers\제품**</span><span class="sxs-lookup"><span data-stu-id="e1aaa-112">**Listing 2 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample2.vb)]

<span data-ttu-id="e1aaa-113">제품 컨트롤러에서 노출 하는 Details () 작업은 productId 라는 단일 매개 변수를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1aaa-113">Notice that the Details() action exposed by the Product controller accepts a single parameter named productId.</span></span> <span data-ttu-id="e1aaa-114">이 매개 변수는 정수 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="e1aaa-114">This parameter is an integer parameter.</span></span>

<span data-ttu-id="e1aaa-115">목록 1에 정의 된 경로는 다음 Url과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1aaa-115">The route defined in Listing 1 will match any of the following URLs:</span></span>

- <span data-ttu-id="e1aaa-116">/Cv3</span><span class="sxs-lookup"><span data-stu-id="e1aaa-116">/Product/23</span></span>
- <span data-ttu-id="e1aaa-117">/제품/7</span><span class="sxs-lookup"><span data-stu-id="e1aaa-117">/Product/7</span></span>

<span data-ttu-id="e1aaa-118">불행 하 게도 경로는 다음 Url과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1aaa-118">Unfortunately, the route will also match the following URLs:</span></span>

- <span data-ttu-id="e1aaa-119">/Product/blah</span><span class="sxs-lookup"><span data-stu-id="e1aaa-119">/Product/blah</span></span>
- <span data-ttu-id="e1aaa-120">/> Apple</span><span class="sxs-lookup"><span data-stu-id="e1aaa-120">/Product/apple</span></span>

<span data-ttu-id="e1aaa-121">Details () 작업에는 정수 매개 변수가 필요 하기 때문에 정수 값이 아닌 다른 항목을 포함 하는 요청을 수행 하면 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1aaa-121">Because the Details() action expects an integer parameter, making a request that contains something other than an integer value will cause an error.</span></span> <span data-ttu-id="e1aaa-122">예를 들어, 브라우저에 URL/Dva/>를 입력 하면 그림 1에 오류 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1aaa-122">For example, if you type the URL /Product/apple into your browser then you will get the error page in Figure 1.</span></span>

<span data-ttu-id="e1aaa-123">[새 프로젝트 대화 상자 ![](creating-a-route-constraint-vb/_static/image1.jpg)](creating-a-route-constraint-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e1aaa-123">[![The New Project dialog box](creating-a-route-constraint-vb/_static/image1.jpg)](creating-a-route-constraint-vb/_static/image1.png)</span></span>

<span data-ttu-id="e1aaa-124">**그림 01**: 페이지 분해[보기 (전체 크기 이미지를 보려면 클릭](creating-a-route-constraint-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="e1aaa-124">**Figure 01**: Seeing a page explode ([Click to view full-size image](creating-a-route-constraint-vb/_static/image2.png))</span></span>

<span data-ttu-id="e1aaa-125">원하는 것은 적절 한 정수 productId를 포함 하는 Url과 일치 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e1aaa-125">What you really want to do is only match URLs that contain a proper integer productId.</span></span> <span data-ttu-id="e1aaa-126">경로를 정의할 때 제약 조건을 사용 하 여 경로와 일치 하는 Url을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1aaa-126">You can use a constraint when defining a route to restrict the URLs that match the route.</span></span> <span data-ttu-id="e1aaa-127">목록 3의 수정 된 제품 경로에는 정수와 일치 하는 정규식 제약 조건이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1aaa-127">The modified Product route in Listing 3 contains a regular expression constraint that only matches integers.</span></span>

<span data-ttu-id="e1aaa-128">**목록 3-global.asax .vb**</span><span class="sxs-lookup"><span data-stu-id="e1aaa-128">**Listing 3 - Global.asax.vb**</span></span>

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample3.vb)]

<span data-ttu-id="e1aaa-129">정규식 \d +는 하나 이상의 정수와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1aaa-129">The regular expression \d+ matches one or more integers.</span></span> <span data-ttu-id="e1aaa-130">이 제약 조건으로 인해 제품 경로가 다음 Url과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1aaa-130">This constraint causes the Product route to match the following URLs:</span></span>

- <span data-ttu-id="e1aaa-131">/Product/3</span><span class="sxs-lookup"><span data-stu-id="e1aaa-131">/Product/3</span></span>
- <span data-ttu-id="e1aaa-132">/Cv99</span><span class="sxs-lookup"><span data-stu-id="e1aaa-132">/Product/8999</span></span>

<span data-ttu-id="e1aaa-133">그러나 다음 Url은 그렇지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e1aaa-133">But not the following URLs:</span></span>

- <span data-ttu-id="e1aaa-134">/> Apple</span><span class="sxs-lookup"><span data-stu-id="e1aaa-134">/Product/apple</span></span>
- <span data-ttu-id="e1aaa-135">/Product</span><span class="sxs-lookup"><span data-stu-id="e1aaa-135">/Product</span></span>

<span data-ttu-id="e1aaa-136">이러한 브라우저 요청은 다른 경로에 의해 처리 되거나, 일치 하는 경로가 없는 경우 리소스를 *찾을* 수 없습니다. 오류가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1aaa-136">These browser requests will be handled by another route or, if there are no matching routes, a *The resource could not be found* error will be returned.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e1aaa-137">[이전](creating-custom-routes-vb.md)
> [다음](creating-a-custom-route-constraint-vb.md)</span><span class="sxs-lookup"><span data-stu-id="e1aaa-137">[Previous](creating-custom-routes-vb.md)
[Next](creating-a-custom-route-constraint-vb.md)</span></span>
