---
uid: web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-cs
title: UpdatePanel 애니메이션을 동적으로C#제어 () | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 의 내용에 대 한
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 5138b8fe-98ff-4e73-a00b-e263fc3ff11d
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-cs
msc.type: authoredcontent
ms.openlocfilehash: 183974564764aab9c0d8a4e577995f3c444bf2d3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430901"
---
# <a name="dynamically-controlling-updatepanel-animations-c"></a><span data-ttu-id="5c3a5-104">UpdatePanel 애니메이션을 동적으로 제어(C#)</span><span class="sxs-lookup"><span data-stu-id="5c3a5-104">Dynamically Controlling UpdatePanel Animations (C#)</span></span>

<span data-ttu-id="5c3a5-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="5c3a5-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="5c3a5-106">[코드 다운로드](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="5c3a5-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2CS.pdf)</span></span>

> <span data-ttu-id="5c3a5-107">ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a5-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="5c3a5-108">UpdatePanel의 콘텐츠에는 애니메이션 프레임 워크 (UpdatePanelAnimation)에 크게 의존 하는 특수 extender가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a5-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="5c3a5-109">또한 UpdatePanel 트리거와 함께 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a5-109">It can also work together with UpdatePanel triggers.</span></span>

## <a name="overview"></a><span data-ttu-id="5c3a5-110">개요</span><span class="sxs-lookup"><span data-stu-id="5c3a5-110">Overview</span></span>

<span data-ttu-id="5c3a5-111">ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a5-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="5c3a5-112">`UpdatePanel`콘텐츠의 경우 애니메이션 프레임 워크 (`UpdatePanelAnimation`)를 많이 사용 하는 특수 extender가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a5-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="5c3a5-113">또한 `UpdatePanel` 트리거와 함께 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a5-113">It can also work together with `UpdatePanel` triggers.</span></span>

## <a name="steps"></a><span data-ttu-id="5c3a5-114">단계</span><span class="sxs-lookup"><span data-stu-id="5c3a5-114">Steps</span></span>

<span data-ttu-id="5c3a5-115">첫 번째 단계는 ASP.NET AJAX 라이브러리가 로드 되 고 Control Toolkit를 사용할 수 있도록 페이지에 `ScriptManager`를 포함 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a5-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample1.aspx)]

<span data-ttu-id="5c3a5-116">이 시나리오의 애니메이션은 현재 시간을 표시 하는 데 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a5-116">The animation in this scenario will be applied to a display of the current time.</span></span> <span data-ttu-id="5c3a5-117">이 정보는 `Page_Load()` 메서드를 사용 하 여 레이블에 기록 하거나 간단 하 게 사용할 수 있도록 다음과 같은 인라인 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a5-117">This information can be written into a label using the `Page_Load()` method, or (for the sake of simplicity) the following inline code is used:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample2.aspx)]

<span data-ttu-id="5c3a5-118">또한 시간 업데이트를 트리거하는 단추도 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a5-118">Also, a button to trigger updating the time is created:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample3.aspx)]

<span data-ttu-id="5c3a5-119">그런 다음이 코드는 `UpdatePanel` 요소의 `<ContentTemplate>` 섹션에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a5-119">This code is then put into the `<ContentTemplate>` section of an `UpdatePanel` element.</span></span> <span data-ttu-id="5c3a5-120">트리거로 패널의 내용을 업데이트할 수 있으므로 패널의 `UpdateMode` 특성은 `"Conditional"`으로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a5-120">The panel's `UpdateMode` attribute must be set to `"Conditional"`, since only triggers may update the panel's contents.</span></span> <span data-ttu-id="5c3a5-121">`UpdatePanel`의 `<Triggers>` 섹션에서 비동기 포스트백 트리거를 만들고 단추의 `Click` 이벤트에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a5-121">In the `<Triggers>` section of the `UpdatePanel`, an asynchronous postback trigger is created and tied to the `Click` event of the button.</span></span> <span data-ttu-id="5c3a5-122">따라서 사용자가 단추를 클릭 하면 `UpdatePanel` 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a5-122">Thus, if the user clicks on the button, the `UpdatePanel` is refreshed.</span></span> <span data-ttu-id="5c3a5-123">`UpdatePanel` 컨트롤에 대 한 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a5-123">Here is the markup for the `UpdatePanel` control:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample4.aspx)]

<span data-ttu-id="5c3a5-124">마지막으로 `UpdatePanelAnimationExtender`를 구성 해야 합니다. `TargetControlID` 특성을 패널의 ID로 설정 하 고 extender 내에서 애니메이션을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a5-124">Finally, the `UpdatePanelAnimationExtender` must be configured: Set the `TargetControlID` attribute to the ID of the panel, and define an animation within the extender.</span></span> <span data-ttu-id="5c3a5-125">페이드 인을 사용 하면 업데이트 된 시간에 대 한 시각적인 강조 효과를 쉽게 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a5-125">Fading in makes sense, which creates a nice visual emphasis on the updated time.</span></span> <span data-ttu-id="5c3a5-126">Extender 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a5-126">Your extender markup may then look like this:</span></span>

[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample5.aspx)]

<span data-ttu-id="5c3a5-127">브라우저에서 파일을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a5-127">Run the file in the browser.</span></span> <span data-ttu-id="5c3a5-128">단추를 클릭할 때마다 현재 시간이 패널에 표시 되며, 항상 1 초 동안 페이드 인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a5-128">Whenever you click on the button, the current time is shown in the panel, always fading in for the duration of one second.</span></span>

<span data-ttu-id="5c3a5-129">[현재 시간이 페이딩 ![](dynamically-controlling-updatepanel-animations-cs/_static/image2.png)](dynamically-controlling-updatepanel-animations-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5c3a5-129">[![The current time is fading in](dynamically-controlling-updatepanel-animations-cs/_static/image2.png)](dynamically-controlling-updatepanel-animations-cs/_static/image1.png)</span></span>

<span data-ttu-id="5c3a5-130">현재 시간이 페이딩 ([전체 크기 이미지를 보려면 클릭](dynamically-controlling-updatepanel-animations-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="5c3a5-130">The current time is fading in ([Click to view full-size image](dynamically-controlling-updatepanel-animations-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5c3a5-131">[이전](animating-an-updatepanel-control-cs.md)
> [다음](adding-animation-to-a-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="5c3a5-131">[Previous](animating-an-updatepanel-control-cs.md)
[Next](adding-animation-to-a-control-vb.md)</span></span>
