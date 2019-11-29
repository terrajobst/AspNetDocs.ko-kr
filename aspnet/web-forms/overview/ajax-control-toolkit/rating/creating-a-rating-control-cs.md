---
uid: web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
title: 등급 컨트롤 만들기 (C#) | Microsoft Docs
author: wenz
description: 전자 상거래에서 커뮤니티 사이트로의 많은 websites는 사용자에 게 문서 또는 항목의 등급을 제공 합니다. 일반적으로 몇 가지 코딩 작업이 필요 하지만 ...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 969fb28f-2bff-4fc4-b24a-27f5e2534a37
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
msc.type: authoredcontent
ms.openlocfilehash: c0bf793406e378321f54f0460031c526a0b41a02
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611566"
---
# <a name="creating-a-rating-control-c"></a><span data-ttu-id="0f8f5-104">등급 컨트롤 만들기(C#)</span><span class="sxs-lookup"><span data-stu-id="0f8f5-104">Creating a Rating Control (C#)</span></span>

<span data-ttu-id="0f8f5-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="0f8f5-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="0f8f5-106">[코드 다운로드](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="0f8f5-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)</span></span>

> <span data-ttu-id="0f8f5-107">전자 상거래에서 커뮤니티 사이트로의 많은 websites는 사용자에 게 문서 또는 항목의 등급을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f5-107">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="0f8f5-108">이 경우 일반적으로 몇 가지 코딩 노력이 필요 하지만, 제어 도구 키트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f5-108">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>

## <a name="overview"></a><span data-ttu-id="0f8f5-109">개요</span><span class="sxs-lookup"><span data-stu-id="0f8f5-109">Overview</span></span>

<span data-ttu-id="0f8f5-110">전자 상거래에서 커뮤니티 사이트로의 많은 websites는 사용자에 게 문서 또는 항목의 등급을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f5-110">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="0f8f5-111">이 경우 일반적으로 몇 가지 코딩 노력이 필요 하지만, 제어 도구 키트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f5-111">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>

## <a name="steps"></a><span data-ttu-id="0f8f5-112">단계</span><span class="sxs-lookup"><span data-stu-id="0f8f5-112">Steps</span></span>

<span data-ttu-id="0f8f5-113">먼저 (적어도) 두 종류의 이미지가 표시 됩니다. 하나는 입력 된 등급 항목을 위한 것이 고 다른 하나는 빈 등급 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f5-113">First of all, you need (at least) two kinds of images: one for a filled out rating item, and one for an empty rating item.</span></span> <span data-ttu-id="0f8f5-114">등급 항목은 일반적으로 별 이거나 웃는 얼굴입니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f5-114">A rating item is usually a star or a smiley.</span></span> <span data-ttu-id="0f8f5-115">이 시나리오의 경우이 자습서에 대 한 소스 코드 다운로드의 일부로 smiley-done 및 빈 .png 및의 세 가지 파일을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f5-115">For this scenario, you find three files, smiley.png and empty.png and smiley-done.png as part of the source code downloads for this tutorial.</span></span>

<span data-ttu-id="0f8f5-116">그런 다음 새 ASP.NET 파일을 만들고이 파일에 `ScriptManager` 컨트롤을 추가 하는 것으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f5-116">Then, create a new ASP.NET file and start with adding a `ScriptManager` control to it:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample1.aspx)]

<span data-ttu-id="0f8f5-117">그런 다음 ASP.NET AJAX 컨트롤 도구 키트의 `Rating` 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f5-117">Then, add the `Rating` control from the ASP.NET AJAX Control Toolkit.</span></span> <span data-ttu-id="0f8f5-118">이 예제에 대해 다음 특성을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f5-118">The following attributes need to be set for this example:</span></span>

- <span data-ttu-id="0f8f5-119">사용할 초기 등급을 `CurrentRating` 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f5-119">`CurrentRating` the initial rating to be used</span></span>
- <span data-ttu-id="0f8f5-120">최대 등급 `MaxRating`</span><span class="sxs-lookup"><span data-stu-id="0f8f5-120">`MaxRating` the maximum rating</span></span>
- <span data-ttu-id="0f8f5-121">등급 항목 (star)이 비어 있을 때 사용할 CSS 클래스를 `EmptyStarCssClass` 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f5-121">`EmptyStarCssClass` the CSS class to use when a rating item ( star ) is empty</span></span>
- <span data-ttu-id="0f8f5-122">등급 항목 (별모양)이 채워질 때 사용할 CSS 클래스를 `FilledStarCssClass` 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f5-122">`FilledStarCssClass` the CSS class to use when a rating item ( star ) is filled out</span></span>
- <span data-ttu-id="0f8f5-123">표시 되는 통계에 사용할 CSS 클래스를 `StarCssClass` 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f5-123">`StarCssClass` the CSS class to use for a visible stat</span></span>
- <span data-ttu-id="0f8f5-124">스타 등급이 서버로 다시 전송 되는 동안 사용할 CSS 클래스를 `WaitingStarCssClass` 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f5-124">`WaitingStarCssClass` the CSS class to use while a star rating is sent back to the server</span></span>

<span data-ttu-id="0f8f5-125">다음은 처음에 아무것도 채워지지 않은 5 개 항목 (smileys)을 사용 하는 등급 컨트롤을 만드는 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f5-125">And here is the markup which creates a rating control with five items (smileys) of which none is filled out initially:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample2.aspx)]

<span data-ttu-id="0f8f5-126">이제 세 개의 참조 된 CSS 클래스는 CSS를 사용 하 여 쉽게 수행할 수 있는 적절 한 이미지 파일을 표시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f5-126">The three referenced CSS classes now need to show the appropriate image files, which is easy to do using CSS:</span></span>

[!code-css[Main](creating-a-rating-control-cs/samples/sample3.css)]

<span data-ttu-id="0f8f5-127">3 개 이미지의 너비와 높이를 제공 해야 합니다. 그렇지 않으면 디스플레이에서 비트 문제가 발생 한 보일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f5-127">Make sure that you provide the width and height of the three images, otherwise the display may look a bit messed up.</span></span>

<span data-ttu-id="0f8f5-128">마지막으로 등급의 결과가 사용자에 게 표시 되어야 합니다 (또는 적어도 데이터베이스에 저장 됨).</span><span class="sxs-lookup"><span data-stu-id="0f8f5-128">Finally, the result of the rating should be displayed to the user (or, at least saved in a database).</span></span> <span data-ttu-id="0f8f5-129">따라서 문자 메시지의 출력에 대 한 레이블을 추가 하 고 제출 단추를 추가 하 여 등급 양식을 서버에 다시 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f5-129">So add a label for the output of a text message and a submit button to post back the rating form to the server:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample4.aspx)]

<span data-ttu-id="0f8f5-130">서버 쪽 코드에서 `ID`를 통해 등급 컨트롤에 액세스 한 다음 선택 된 등급 항목의 수 인 `CurrentRating` 속성에 액세스 합니다. 예를 들어 0에서 5 사이의 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f5-130">In the server-side code, access the Rating control via its `ID` and then access its `CurrentRating` property which is the number of the selected rating items, in our example a value between 0 and 5.</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample5.aspx)]

<span data-ttu-id="0f8f5-131">페이지를 저장 하 고 브라우저에 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f5-131">Save the page and load it into your browser.</span></span> <span data-ttu-id="0f8f5-132">(처음에는 비어 있음) 등급 항목을 마우스로 가리키면 JavaScript 효과가 발생 합니다. 등급은 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f5-132">When you hover over the (initially empty) rating items, a JavaScript effect occurs: The rating changes.</span></span> <span data-ttu-id="0f8f5-133">별 집합을 클릭 하면 현재 등급은 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f5-133">When you click on the set of stars, the current rating is retained.</span></span> <span data-ttu-id="0f8f5-134">마지막으로 폼을 제출할 때 서버 쪽 코드는 선택한 등급을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f5-134">Finally, when you submit the form, the server-side code outputs the selected rating.</span></span>

<span data-ttu-id="0f8f5-135">[최소한의 코드로 등급 시스템을 만드는 ![](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0f8f5-135">[![Creating a rating system with minimal code](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="0f8f5-136">최소 코드로 등급 시스템 만들기 ([전체 크기 이미지를 보려면 클릭](creating-a-rating-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="0f8f5-136">Creating a rating system with minimal code ([Click to view full-size image](creating-a-rating-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="0f8f5-137">다음</span><span class="sxs-lookup"><span data-stu-id="0f8f5-137">Next</span></span>](creating-a-rating-control-vb.md)
