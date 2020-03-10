---
uid: web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
title: 조건에 따른 애니메이션 (C#) | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 애니메이션의 여부입니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b7a28c0d-efb9-443a-80a4-1a5ee54671cd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
msc.type: authoredcontent
ms.openlocfilehash: 476b0cf80fa7c04cd8b8f9a92060ddabb9d14c13
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484169"
---
# <a name="animation-depending-on-a-condition-c"></a><span data-ttu-id="00ff4-104">조건에 따른 애니메이션(C#)</span><span class="sxs-lookup"><span data-stu-id="00ff4-104">Animation Depending On a Condition (C#)</span></span>

<span data-ttu-id="00ff4-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="00ff4-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="00ff4-106">[코드 다운로드](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="00ff4-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4CS.pdf)</span></span>

> <span data-ttu-id="00ff4-107">ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="00ff4-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="00ff4-108">애니메이션의 실행 여부는 일부 JavaScript 코드 형식의 조건에 따라서도 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00ff4-108">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="00ff4-109">개요</span><span class="sxs-lookup"><span data-stu-id="00ff4-109">Overview</span></span>

<span data-ttu-id="00ff4-110">ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="00ff4-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="00ff4-111">애니메이션의 실행 여부는 일부 JavaScript 코드 형식의 조건에 따라서도 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00ff4-111">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="00ff4-112">단계</span><span class="sxs-lookup"><span data-stu-id="00ff4-112">Steps</span></span>

<span data-ttu-id="00ff4-113">먼저 페이지에 `ScriptManager`를 포함 합니다. 그런 다음 ASP.NET AJAX 라이브러리가 로드 되어 컨트롤 도구 키트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00ff4-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample1.aspx)]

<span data-ttu-id="00ff4-114">애니메이션은 다음과 같은 텍스트 패널에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00ff4-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample2.aspx)]

<span data-ttu-id="00ff4-115">패널의 연결 된 CSS 클래스에서 좋은 배경색을 정의 하 고 패널의 고정 폭도 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ff4-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animation-depending-on-a-condition-cs/samples/sample3.css)]

<span data-ttu-id="00ff4-116">그런 다음 `ID`, `TargetControlID` 특성 및 obligatory을 제공 하 여 페이지에 `AnimationExtender`를 추가 `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="00ff4-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample4.aspx)]

<span data-ttu-id="00ff4-117">`<Animations>` 노드 내에서 `<OnLoad>`를 사용 하 여 페이지가 완전히 로드 되 면 애니메이션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ff4-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="00ff4-118">`<Condition>` 요소는 일반적인 애니메이션 중 하나가 아니라 재생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00ff4-118">Instead of one of the regular animations, the `<Condition>` element comes into play.</span></span> <span data-ttu-id="00ff4-119">`ConditionScript` 특성의 값으로 제공 되는 JavaScript 코드는 런타임에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00ff4-119">The JavaScript code provided as the value of the `ConditionScript` attribute is executed at runtime.</span></span> <span data-ttu-id="00ff4-120">True로 평가 되 면 애니메이션이 실행 되 고, 그렇지 않으면가 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00ff4-120">If it evaluates to true, the animation is executed, otherwise not.</span></span> <span data-ttu-id="00ff4-121">다음 태그는 두 개의 애니메이션을 제공 하며, 각 애니메이션은 무작위으로 50%의 사례에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00ff4-121">The following markup provides two animations, each of them being executed in 50% of cases upon random.</span></span> <span data-ttu-id="00ff4-122">`<OnLoad>`내에는 애니메이션이 하나만 있을 수 있으므로 `<Sequence>` 요소를 사용 하 여 두 `<Condition>` 애니메이션이 함께 조인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00ff4-122">Since there may only be one animation within `<OnLoad>`, the two `<Condition>` animations are joined together using the `<Sequence>` element:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample5.aspx)]

<span data-ttu-id="00ff4-123">`ConditionScript` 특성에서 보다 작음 부호 (`<`)는 이스케이프 되어야 합니다 ().</span><span class="sxs-lookup"><span data-stu-id="00ff4-123">Note that the less than sign (`<`) in the `ConditionScript` attribute must be escaped ().</span></span> <span data-ttu-id="00ff4-124">이 스크립트를 실행 하는 경우 애니메이션을 실행 하지 않거나 둘 중 하나 또는 둘 다 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="00ff4-124">When you run this script, either no animation runs, or one of the two does, or both do.</span></span>

<span data-ttu-id="00ff4-125">[패널의 크기를 조정 하지 않고 페이드 아웃 하면 두 번째 애니메이션이 실행 되므로 첫 번째 애니메이션이 실행 되지 않는 ![](animation-depending-on-a-condition-cs/_static/image2.png)](animation-depending-on-a-condition-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="00ff4-125">[![The panel is fading out without resizing, so the second animation runs, the first one didn't](animation-depending-on-a-condition-cs/_static/image2.png)](animation-depending-on-a-condition-cs/_static/image1.png)</span></span>

<span data-ttu-id="00ff4-126">패널은 크기를 조정 하지 않고 페이드 아웃 되기 때문에 첫 번째 애니메이션이 실행 됩니다 ([전체 크기 이미지를 보려면 클릭](animation-depending-on-a-condition-cs/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="00ff4-126">The panel is fading out without resizing, so the second animation runs, the first one didn't ([Click to view full-size image](animation-depending-on-a-condition-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="00ff4-127">[이전](executing-several-animations-after-each-other-cs.md)
> [다음](picking-one-animation-out-of-a-list-cs.md)</span><span class="sxs-lookup"><span data-stu-id="00ff4-127">[Previous](executing-several-animations-after-each-other-cs.md)
[Next](picking-one-animation-out-of-a-list-cs.md)</span></span>
