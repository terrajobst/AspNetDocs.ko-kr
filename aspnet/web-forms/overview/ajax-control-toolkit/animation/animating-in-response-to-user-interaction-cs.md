---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
title: 사용자 상호 작용에 대 한 응답C#으로 애니메이션 효과 주기 () | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 애니메이션은 별이 될 수 있습니다 ...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ea26549d-fbbf-4973-a108-b14cd1d6de26
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
msc.type: authoredcontent
ms.openlocfilehash: d04fa680d0cd4f7fb54521ac6fbb47a2cf9a83cf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497903"
---
# <a name="animating-in-response-to-user-interaction-c"></a><span data-ttu-id="8cf16-104">사용자 상호 작용에 대한 응답으로 애니메이션(C#)</span><span class="sxs-lookup"><span data-stu-id="8cf16-104">Animating in Response To User Interaction (C#)</span></span>

<span data-ttu-id="8cf16-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="8cf16-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="8cf16-106">[코드 다운로드](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="8cf16-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6CS.pdf)</span></span>

> <span data-ttu-id="8cf16-107">ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="8cf16-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="8cf16-108">애니메이션은 자동으로 시작 되거나 사용자 상호 작용 (예: 마우스로 클릭)에 의해 트리거될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cf16-108">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="overview"></a><span data-ttu-id="8cf16-109">개요</span><span class="sxs-lookup"><span data-stu-id="8cf16-109">Overview</span></span>

<span data-ttu-id="8cf16-110">ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="8cf16-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="8cf16-111">애니메이션은 자동으로 시작 되거나 사용자 상호 작용 (예: 마우스로 클릭)에 의해 트리거될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cf16-111">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="steps"></a><span data-ttu-id="8cf16-112">단계</span><span class="sxs-lookup"><span data-stu-id="8cf16-112">Steps</span></span>

<span data-ttu-id="8cf16-113">먼저 페이지에 `ScriptManager`를 포함 합니다. 그런 다음 ASP.NET AJAX 라이브러리가 로드 되어 컨트롤 도구 키트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cf16-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample1.aspx)]

<span data-ttu-id="8cf16-114">애니메이션은 다음과 같은 텍스트 패널에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cf16-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample2.aspx)]

<span data-ttu-id="8cf16-115">패널의 연결 된 CSS 클래스에서 좋은 배경색을 정의 하 고 패널의 고정 폭도 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cf16-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animating-in-response-to-user-interaction-cs/samples/sample3.css)]

<span data-ttu-id="8cf16-116">그런 다음 `ID`, `TargetControlID` 특성 및 obligatory `runat="server"`를 제공 하 여 페이지에 `AnimationExtender`를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cf16-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample4.aspx)]

<span data-ttu-id="8cf16-117">`<Animations>` 노드 내에는 사용자 상호 작용을 통해 애니메이션을 시작 하는 5 가지 방법이 있습니다. 누락 된 요소는 전체 페이지가 완전히 로드 된 후 실행 되는 `<OnLoad>`입니다.</span><span class="sxs-lookup"><span data-stu-id="8cf16-117">Within the `<Animations>` node, there are five ways to start the animation via user interaction (the missing element is `<OnLoad>` which is executed once the whole page has been fully loaded):</span></span>

- <span data-ttu-id="8cf16-118">`<OnClick>` (컨트롤에서 마우스 클릭)</span><span class="sxs-lookup"><span data-stu-id="8cf16-118">`<OnClick>` (mouse click on the control)</span></span>
- <span data-ttu-id="8cf16-119">`<OnHoverOut>` (마우스가 컨트롤을 벗어납니다.)</span><span class="sxs-lookup"><span data-stu-id="8cf16-119">`<OnHoverOut>` (mouse leaves the control)</span></span>
- <span data-ttu-id="8cf16-120">`<OnHoverOver>` (마우스 마우스로 컨트롤 가리키기, `<OnHoverOut>` 애니메이션 중지)</span><span class="sxs-lookup"><span data-stu-id="8cf16-120">`<OnHoverOver>` (mouse hovers over a control, stopping the `<OnHoverOut>` animation)</span></span>
- <span data-ttu-id="8cf16-121">`<OnMouseOut>` (마우스가 컨트롤을 벗어나면)</span><span class="sxs-lookup"><span data-stu-id="8cf16-121">`<OnMouseOut>` (mouse leaves a control)</span></span>
- <span data-ttu-id="8cf16-122">`<OnMouseOver>` (`<OnMouseOut>` 애니메이션을 중지 하지 않고 컨트롤을 마우스로 가리키기)</span><span class="sxs-lookup"><span data-stu-id="8cf16-122">`<OnMouseOver>` (mouse hovers over a control, not stopping the `<OnMouseOut>` animation)</span></span>

<span data-ttu-id="8cf16-123">이 시나리오에서는 `<OnClick>` 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cf16-123">In this scenario, `<OnClick>` is used.</span></span> <span data-ttu-id="8cf16-124">사용자가 패널을 클릭 하면 크기가 조정 되 고 동시에 페이드 아웃 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cf16-124">When the user clicks on the panel, it is resized and fades out at the same time.</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample5.aspx)]

<span data-ttu-id="8cf16-125">[마우스 클릭 ![애니메이션 시작](animating-in-response-to-user-interaction-cs/_static/image2.png)](animating-in-response-to-user-interaction-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8cf16-125">[![A mouse click starts the animation](animating-in-response-to-user-interaction-cs/_static/image2.png)](animating-in-response-to-user-interaction-cs/_static/image1.png)</span></span>

<span data-ttu-id="8cf16-126">마우스 클릭으로 애니메이션 시작 ([전체 크기 이미지를 보려면 클릭](animating-in-response-to-user-interaction-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="8cf16-126">A mouse click starts the animation ([Click to view full-size image](animating-in-response-to-user-interaction-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8cf16-127">[이전](picking-one-animation-out-of-a-list-cs.md)
> [다음](disabling-actions-during-animation-cs.md)</span><span class="sxs-lookup"><span data-stu-id="8cf16-127">[Previous](picking-one-animation-out-of-a-list-cs.md)
[Next](disabling-actions-during-animation-cs.md)</span></span>
