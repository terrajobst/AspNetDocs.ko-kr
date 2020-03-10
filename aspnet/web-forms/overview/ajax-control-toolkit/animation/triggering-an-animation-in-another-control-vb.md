---
uid: web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
title: 다른 컨트롤에서 애니메이션 트리거 (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 일반적으로 시작 하는 중 ...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 25ebaf1f-5a9f-423d-98c7-1d694e93664f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 6a4af2324afab7519170c123b6ea7c57ab3e03fb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430787"
---
# <a name="triggering-an-animation-in-another-control-vb"></a><span data-ttu-id="2f322-104">다른 컨트롤에서 애니메이션 트리거(VB)</span><span class="sxs-lookup"><span data-stu-id="2f322-104">Triggering an Animation in another Control (VB)</span></span>

<span data-ttu-id="2f322-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="2f322-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="2f322-106">[코드 다운로드](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="2f322-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8VB.pdf)</span></span>

> <span data-ttu-id="2f322-107">ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="2f322-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="2f322-108">일반적으로 애니메이션 시작은 동일한 컨트롤의 사용자 상호 작용에 의해 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f322-108">Generally, launching an animation is triggered by user interaction with the same control.</span></span> <span data-ttu-id="2f322-109">그러나 한 컨트롤과 상호 작용 한 다음 다른 컨트롤을 애니메이션으로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f322-109">It is however also possible to interact with one control and then animation another control.</span></span>

## <a name="overview"></a><span data-ttu-id="2f322-110">개요</span><span class="sxs-lookup"><span data-stu-id="2f322-110">Overview</span></span>

<span data-ttu-id="2f322-111">ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="2f322-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="2f322-112">일반적으로 애니메이션 시작은 동일한 컨트롤의 사용자 상호 작용에 의해 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f322-112">Generally, launching an animation is triggered by user interaction with the same control.</span></span> <span data-ttu-id="2f322-113">그러나 한 컨트롤과 상호 작용 한 다음 다른 컨트롤을 애니메이션으로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f322-113">It is however also possible to interact with one control and then animation another control.</span></span>

## <a name="steps"></a><span data-ttu-id="2f322-114">단계</span><span class="sxs-lookup"><span data-stu-id="2f322-114">Steps</span></span>

<span data-ttu-id="2f322-115">먼저 페이지에 `ScriptManager`를 포함 합니다. 그런 다음 ASP.NET AJAX 라이브러리가 로드 되어 컨트롤 도구 키트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f322-115">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample1.aspx)]

<span data-ttu-id="2f322-116">애니메이션은 다음과 같은 텍스트 패널에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f322-116">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample2.aspx)]

<span data-ttu-id="2f322-117">패널의 연결 된 CSS 클래스에서 좋은 배경색을 정의 하 고 패널의 고정 폭도 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f322-117">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](triggering-an-animation-in-another-control-vb/samples/sample3.css)]

<span data-ttu-id="2f322-118">패널에 대 한 애니메이션 효과를 시작 하기 위해 HTML 단추가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f322-118">In order to start animating the panel, an HTML button is used.</span></span> <span data-ttu-id="2f322-119">사용자가 해당 단추를 클릭할 때 포스트백을 원하지 않으므로 `<input type="button" />`는 `<asp:Button />`를 통해 favoured 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f322-119">Note that `<input type="button" />` is favoured over `<asp:Button />` since we do not want a postback when the user clicks on that button.</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample4.aspx)]

<span data-ttu-id="2f322-120">그런 다음 `ID`, `TargetControlID` 특성 및 obligatory `runat="server"`를 제공 하 여 페이지에 `AnimationExtender`를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f322-120">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`.</span></span> <span data-ttu-id="2f322-121">패널의 ID (애니메이션 효과를 주는 요소)가 아니라 단추 ID (애니메이션을 트리거하는 요소)로 `TargetControlID`를 설정 하는 것이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f322-121">It is important to set `TargetControlID` to the ID of the button (the element triggering the animation), not to the ID of the panel (the element being animated)</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample5.aspx)]

<span data-ttu-id="2f322-122">`<Animations>` 노드 내에서 애니메이션을 평소와 같이 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f322-122">Within the `<Animations>` node, place animations as usual.</span></span> <span data-ttu-id="2f322-123">단추가 아니라 패널을 변경 하기 위해 `AnimationExtender`내의 모든 애니메이션 요소에 대해 `AnimationTarget` 특성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f322-123">In order to make them change the panel, not the button, set the `AnimationTarget` attribute for every animation element within `AnimationExtender`.</span></span> <span data-ttu-id="2f322-124">`AnimationTarget`의 값은 패널의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="2f322-124">The value for `AnimationTarget` is the ID of the panel, of course.</span></span> <span data-ttu-id="2f322-125">이렇게 하면 애니메이션은 트리거 단추가 아니라 패널에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f322-125">That way, the animations happen with the panel, not with the triggering button.</span></span> <span data-ttu-id="2f322-126">이 시나리오에 대 한 `AnimationExtender` 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2f322-126">Here is the `AnimationExtender` markup for this scenario:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample6.aspx)]

<span data-ttu-id="2f322-127">개별 애니메이션이 표시 되는 특별 한 순서를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f322-127">Note the special order in which the individual animations appear.</span></span> <span data-ttu-id="2f322-128">먼저 애니메이션을 실행 하면 단추가 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f322-128">First of all, the button gets deactivated once the animation runs.</span></span> <span data-ttu-id="2f322-129">`<EnableAction>` 요소에 `AnimationTarget` 특성이 없으므로이 애니메이션은 원래 컨트롤 (단추)에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f322-129">Since there is no `AnimationTarget` attribute in the `<EnableAction>` element, this animation is applied to the originating control: the button.</span></span> <span data-ttu-id="2f322-130">다음 두 애니메이션 단계는 병렬로 수행 해야 합니다 (`<Parallel>` 요소).</span><span class="sxs-lookup"><span data-stu-id="2f322-130">The next two animation steps shall be carried out in parallel (`<Parallel>` element).</span></span> <span data-ttu-id="2f322-131">둘 다 `AnimationTarget` 특성이 `"Panel1"`로 설정 되어 있으므로 패널에 애니메이션을 적용 하는 것은 단추가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="2f322-131">Both have their `AnimationTarget` attributes set to `"Panel1"`, thus animating the panel, not the button.</span></span>

<span data-ttu-id="2f322-132">[단추를 마우스 클릭 ![하면 패널 애니메이션이 시작 됩니다.](triggering-an-animation-in-another-control-vb/_static/image2.png)](triggering-an-animation-in-another-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2f322-132">[![A mouse click on the button starts the panel animation](triggering-an-animation-in-another-control-vb/_static/image2.png)](triggering-an-animation-in-another-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="2f322-133">단추를 마우스 클릭 하면 패널 애니메이션이 시작 됩니다 ([전체 크기 이미지를 보려면 클릭](triggering-an-animation-in-another-control-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="2f322-133">A mouse click on the button starts the panel animation ([Click to view full-size image](triggering-an-animation-in-another-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2f322-134">[이전](disabling-actions-during-animation-vb.md)
> [다음](modifying-animations-from-the-server-side-vb.md)</span><span class="sxs-lookup"><span data-stu-id="2f322-134">[Previous](disabling-actions-during-animation-vb.md)
[Next](modifying-animations-from-the-server-side-vb.md)</span></span>
