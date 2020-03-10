---
uid: web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
title: 컨트롤에 애니메이션 추가 (C#) | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 이 자습서에서는 다음 방법을 보여 줍니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0f1fc1f5-9dbd-44e7-931e-387d42f0342b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
msc.type: authoredcontent
ms.openlocfilehash: dd63157fe616c5f6874b7cca11f4ede15018df04
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497969"
---
# <a name="adding-animation-to-a-control-c"></a><span data-ttu-id="d9665-104">컨트롤에 애니메이션 추가(C#)</span><span class="sxs-lookup"><span data-stu-id="d9665-104">Adding Animation to a Control (C#)</span></span>

<span data-ttu-id="d9665-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="d9665-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="d9665-106">[코드 다운로드](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="d9665-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1CS.pdf)</span></span>

> <span data-ttu-id="d9665-107">ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="d9665-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="d9665-108">이 자습서에서는 이러한 애니메이션을 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d9665-108">This tutorial shows how to set up such an animation.</span></span>

## <a name="overview"></a><span data-ttu-id="d9665-109">개요</span><span class="sxs-lookup"><span data-stu-id="d9665-109">Overview</span></span>

<span data-ttu-id="d9665-110">ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="d9665-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="d9665-111">이 자습서에서는 이러한 애니메이션을 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d9665-111">This tutorial shows how to set up such an animation.</span></span>

## <a name="steps"></a><span data-ttu-id="d9665-112">단계</span><span class="sxs-lookup"><span data-stu-id="d9665-112">Steps</span></span>

<span data-ttu-id="d9665-113">첫 번째 단계는 ASP.NET AJAX 라이브러리가 로드 되 고 Control Toolkit를 사용할 수 있도록 페이지에 `ScriptManager`를 포함 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d9665-113">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample1.aspx)]

<span data-ttu-id="d9665-114">이 시나리오의 애니메이션은 다음과 같은 텍스트 패널에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9665-114">The animation in this scenario will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample2.aspx)]

<span data-ttu-id="d9665-115">패널의 연결 된 CSS 클래스는 배경색 및 너비를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9665-115">The associated CSS class for the panel defines a background color and a width:</span></span>

[!code-css[Main](adding-animation-to-a-control-cs/samples/sample3.css)]

<span data-ttu-id="d9665-116">다음으로 `AnimationExtender`필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9665-116">Next up, we need the `AnimationExtender`.</span></span> <span data-ttu-id="d9665-117">`ID` 및 일반적인 `runat="server"`를 제공한 후에는 패널에서 애니메이션 효과를 적용할 컨트롤에 `TargetControlID` 특성을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9665-117">After providing an `ID` and the usual `runat="server"`, the `TargetControlID` attribute must be set to the control to animate in our case, the panel:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample4.aspx)]

<span data-ttu-id="d9665-118">전체 애니메이션은 현재 Visual Studio의 IntelliSense에서 완전히 지원 되지 않는 XML 구문을 사용 하 여 선언적으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9665-118">The whole animation is applied declaratively, using an XML syntax, unfortunately currently not fully supported by Visual Studio's IntelliSense.</span></span> <span data-ttu-id="d9665-119">루트 노드는이 노드 내에 `<Animations>;` 되며, 몇 가지 이벤트를 사용 하 여 애니메이션이 적용 되는 시기를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9665-119">The root node is `<Animations>;` within this node, several events are allowed which determine when the animation(s) take(s) place:</span></span>

- <span data-ttu-id="d9665-120">`OnClick` (마우스 클릭)</span><span class="sxs-lookup"><span data-stu-id="d9665-120">`OnClick` (mouse click)</span></span>
- <span data-ttu-id="d9665-121">`OnHoverOut` (마우스가 컨트롤을 벗어나면)</span><span class="sxs-lookup"><span data-stu-id="d9665-121">`OnHoverOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="d9665-122">`OnHoverOver` (마우스로 컨트롤을 가리킬 때 `OnHoverOut` 애니메이션 중지)</span><span class="sxs-lookup"><span data-stu-id="d9665-122">`OnHoverOver` (when the mouse hovers over a control, stopping the `OnHoverOut` animation)</span></span>
- <span data-ttu-id="d9665-123">`OnLoad` (페이지가 로드 된 경우)</span><span class="sxs-lookup"><span data-stu-id="d9665-123">`OnLoad` (when the page has been loaded)</span></span>
- <span data-ttu-id="d9665-124">`OnMouseOut` (마우스가 컨트롤을 벗어나면)</span><span class="sxs-lookup"><span data-stu-id="d9665-124">`OnMouseOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="d9665-125">`OnMouseOver` (마우스로 컨트롤을 가리킬 때 `OnMouseOut` 애니메이션을 중지 하지 않음)</span><span class="sxs-lookup"><span data-stu-id="d9665-125">`OnMouseOver` (when the mouse hovers over a control, not stopping the `OnMouseOut` animation)</span></span>

<span data-ttu-id="d9665-126">프레임 워크는 각각 자체 XML 요소로 표시 되는 애니메이션 집합과 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9665-126">The framework comes with a set of animations, each one represented by its own XML element.</span></span> <span data-ttu-id="d9665-127">선택 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d9665-127">Here is a selection:</span></span>

- <span data-ttu-id="d9665-128">`<Color>` (색 변경)</span><span class="sxs-lookup"><span data-stu-id="d9665-128">`<Color>` (changing a color)</span></span>
- <span data-ttu-id="d9665-129">`<FadeIn>` (페이딩)</span><span class="sxs-lookup"><span data-stu-id="d9665-129">`<FadeIn>` (fading in)</span></span>
- <span data-ttu-id="d9665-130">`<FadeOut>` (페이드 아웃)</span><span class="sxs-lookup"><span data-stu-id="d9665-130">`<FadeOut>` (fading out)</span></span>
- <span data-ttu-id="d9665-131">`<Property>` (컨트롤의 속성 변경)</span><span class="sxs-lookup"><span data-stu-id="d9665-131">`<Property>` (changing a control's property)</span></span>
- <span data-ttu-id="d9665-132">`<Pulse>` (pulsating)</span><span class="sxs-lookup"><span data-stu-id="d9665-132">`<Pulse>` (pulsating)</span></span>
- <span data-ttu-id="d9665-133">`<Resize>` (크기 변경)</span><span class="sxs-lookup"><span data-stu-id="d9665-133">`<Resize>` (changing the size)</span></span>
- <span data-ttu-id="d9665-134">`<Scale>` (크기를 비례적으로 변경)</span><span class="sxs-lookup"><span data-stu-id="d9665-134">`<Scale>` (proportionally changing the size)</span></span>

<span data-ttu-id="d9665-135">이 예제에서는 패널이 페이드 아웃 됩니다. 애니메이션은 1.5 초 (`Duration` 특성)를 사용 하 여 24 개의 프레임 (애니메이션 단계)/초 (`Fps` 특성)를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9665-135">In this example, the panel shall fade out. The animation shall take 1.5 seconds (`Duration` attribute), displaying 24 frames (animation steps) per second (`Fps` attribute).</span></span> <span data-ttu-id="d9665-136">`AnimationExtender` 컨트롤의 전체 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d9665-136">Here is the complete markup for the `AnimationExtender` control:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample5.aspx)]

<span data-ttu-id="d9665-137">이 스크립트를 실행 하면 패널이 표시 되 고 1 ~ 50 초 안에 페이드 아웃 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9665-137">When you run this script, the panel is displayed and fades out in one and a half seconds.</span></span>

<span data-ttu-id="d9665-138">[패널이 페이드 아웃 된 ![](adding-animation-to-a-control-cs/_static/image2.png)](adding-animation-to-a-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d9665-138">[![The panel is fading out](adding-animation-to-a-control-cs/_static/image2.png)](adding-animation-to-a-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="d9665-139">패널이 페이드 아웃 됩니다 ([전체 크기 이미지를 보려면 클릭](adding-animation-to-a-control-cs/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="d9665-139">The panel is fading out ([Click to view full-size image](adding-animation-to-a-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="d9665-140">다음</span><span class="sxs-lookup"><span data-stu-id="d9665-140">Next</span></span>](executing-several-animations-at-the-same-time-cs.md)
