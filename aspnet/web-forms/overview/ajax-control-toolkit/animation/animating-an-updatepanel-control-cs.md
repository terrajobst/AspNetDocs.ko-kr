---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
title: UpdatePanel 컨트롤에 애니메이션 효과C#주기 () | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 의 내용에 대 한
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e57f8c7c-3940-4bc0-9468-3a0ca69158ea
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 8875d750d57c5f4e362bdf461826130a881ab1d4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431051"
---
# <a name="animating-an-updatepanel-control-c"></a><span data-ttu-id="e6650-104">UpdatePanel 컨트롤 애니메이션(C#)</span><span class="sxs-lookup"><span data-stu-id="e6650-104">Animating an UpdatePanel Control (C#)</span></span>

<span data-ttu-id="e6650-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="e6650-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="e6650-106">[코드 다운로드](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="e6650-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)</span></span>

> <span data-ttu-id="e6650-107">ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="e6650-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="e6650-108">UpdatePanel의 콘텐츠에는 애니메이션 프레임 워크 (UpdatePanelAnimation)에 크게 의존 하는 특수 extender가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6650-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="e6650-109">이 자습서에서는 UpdatePanel에 대해 이러한 애니메이션을 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6650-109">This tutorial shows how to set up such an animation for an UpdatePanel.</span></span>

## <a name="overview"></a><span data-ttu-id="e6650-110">개요</span><span class="sxs-lookup"><span data-stu-id="e6650-110">Overview</span></span>

<span data-ttu-id="e6650-111">ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="e6650-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="e6650-112">`UpdatePanel`콘텐츠의 경우 애니메이션 프레임 워크 (`UpdatePanelAnimation`)를 많이 사용 하는 특수 extender가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6650-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="e6650-113">이 자습서에서는 `UpdatePanel`에 대 한 애니메이션을 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6650-113">This tutorial shows how to set up such an animation for an `UpdatePanel`.</span></span>

## <a name="steps"></a><span data-ttu-id="e6650-114">단계</span><span class="sxs-lookup"><span data-stu-id="e6650-114">Steps</span></span>

<span data-ttu-id="e6650-115">첫 번째 단계는 ASP.NET AJAX 라이브러리가 로드 되 고 Control Toolkit를 사용할 수 있도록 페이지에 `ScriptManager`를 포함 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e6650-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample1.aspx)]

<span data-ttu-id="e6650-116">이 시나리오의 애니메이션은 `UpdatePanel`에 있는 ASP.NET `Wizard` 웹 컨트롤에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6650-116">The animation in this scenario will be applied to an ASP.NET `Wizard` web control residing in an `UpdatePanel`.</span></span> <span data-ttu-id="e6650-117">다시 게시를 트리거하기 위한 충분 한 옵션을 제공 하는 세 가지 (임의) 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6650-117">Three (arbitrary) steps provide enough options to trigger postbacks:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample2.aspx)]

<span data-ttu-id="e6650-118">`UpdatePanelAnimationExtender` 컨트롤에 필요한 태그는 `AnimationExtender`에 사용 되는 태그와 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="e6650-118">The markup necessary for the `UpdatePanelAnimationExtender` control is quite similar to the markup used for the `AnimationExtender`.</span></span> <span data-ttu-id="e6650-119">`TargetControlID` 특성에서 애니메이션 효과를 주는 `UpdatePanel`의 `ID`를 제공 합니다. `UpdatePanelAnimationExtender` 컨트롤 내에서 `<Animations>` 요소는 애니메이션에 대 한 XML 태그를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6650-119">In the `TargetControlID` attribute we provide the `ID` of the `UpdatePanel` to animate; within the `UpdatePanelAnimationExtender` control, the `<Animations>` element holds XML markup for the animation(s).</span></span> <span data-ttu-id="e6650-120">그러나 `AnimationExtender`에 비해 이벤트 및 이벤트 처리기의 양은 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6650-120">However there is one difference: The amount of events and event handlers is limited in comparison to `AnimationExtender`.</span></span> <span data-ttu-id="e6650-121">`UpdatePanels`의 경우 두 가지 중 하나만 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6650-121">For `UpdatePanels`, only two of them exist:</span></span>

- <span data-ttu-id="e6650-122">UpdatePanel이 업데이트 된 경우 `<OnUpdated>`</span><span class="sxs-lookup"><span data-stu-id="e6650-122">`<OnUpdated>` when the UpdatePanel has been updated</span></span>
- <span data-ttu-id="e6650-123">UpdatePanel 업데이트를 시작 하는 `<OnUpdating>`</span><span class="sxs-lookup"><span data-stu-id="e6650-123">`<OnUpdating>` when the UpdatePanel starts updating</span></span>

<span data-ttu-id="e6650-124">이 시나리오에서는 다시 게시 후 `UpdatePanel`의 새 콘텐츠가 페이드 인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6650-124">In this scenario, the new content of the `UpdatePanel` (after the postback) shall fade in.</span></span> <span data-ttu-id="e6650-125">이에 대 한 필수 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e6650-125">This is the necessary markup for that:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample3.aspx)]

<span data-ttu-id="e6650-126">이제 UpdatePanel 내에서 포스트백이 발생할 때마다 패널의 새 내용이 매끄럽게 페이드 인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6650-126">Now whenever a postback occurs within the UpdatePanel, the new contents of the panel fade in smoothly.</span></span>

<span data-ttu-id="e6650-127">[![다음 마법사 단계가 페이드 인 됩니다.](animating-an-updatepanel-control-cs/_static/image2.png)](animating-an-updatepanel-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e6650-127">[![The next wizard step is fading in](animating-an-updatepanel-control-cs/_static/image2.png)](animating-an-updatepanel-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="e6650-128">다음 마법사 단계가 페이드 인 됩니다 ([전체 크기 이미지를 보려면 클릭](animating-an-updatepanel-control-cs/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="e6650-128">The next wizard step is fading in ([Click to view full-size image](animating-an-updatepanel-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e6650-129">[이전](changing-an-animation-using-client-side-code-cs.md)
> [다음](dynamically-controlling-updatepanel-animations-cs.md)</span><span class="sxs-lookup"><span data-stu-id="e6650-129">[Previous](changing-an-animation-using-client-side-code-cs.md)
[Next](dynamically-controlling-updatepanel-animations-cs.md)</span></span>
