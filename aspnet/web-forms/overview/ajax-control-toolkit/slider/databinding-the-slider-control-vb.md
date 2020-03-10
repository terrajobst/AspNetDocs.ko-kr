---
uid: web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
title: 슬라이더 컨트롤 데이터 바인딩 (VB) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 슬라이더 컨트롤은 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다. 현재 positio를 바인딩할 수 있습니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4f3ba53f-d166-422d-b29c-403348057836
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 9c14373bdfdead9916950b8a1cf61f427f7ba50b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78508901"
---
# <a name="databinding-the-slider-control-vb"></a><span data-ttu-id="6cbfa-104">슬라이더 컨트롤 데이터 바인딩(VB)</span><span class="sxs-lookup"><span data-stu-id="6cbfa-104">Databinding the Slider Control (VB)</span></span>

<span data-ttu-id="6cbfa-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="6cbfa-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="6cbfa-106">[코드 다운로드](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="6cbfa-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0VB.pdf)</span></span>

> <span data-ttu-id="6cbfa-107">AJAX 컨트롤 도구 키트의 슬라이더 컨트롤은 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="6cbfa-108">슬라이더의 현재 위치를 다른 ASP.NET 컨트롤에 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-108">It is possible to bind the current position of the slider to another ASP.NET control.</span></span>

## <a name="overview"></a><span data-ttu-id="6cbfa-109">개요</span><span class="sxs-lookup"><span data-stu-id="6cbfa-109">Overview</span></span>

<span data-ttu-id="6cbfa-110">AJAX 컨트롤 도구 키트의 슬라이더 컨트롤은 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="6cbfa-111">슬라이더의 현재 위치를 다른 ASP.NET 컨트롤에 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-111">It is possible to bind the current position of the slider to another ASP.NET control.</span></span>

## <a name="steps"></a><span data-ttu-id="6cbfa-112">단계</span><span class="sxs-lookup"><span data-stu-id="6cbfa-112">Steps</span></span>

<span data-ttu-id="6cbfa-113">ASP.NET AJAX 및 Control Toolkit의 기능을 활성화 하려면 페이지의 아무 곳에 나 `<form>` 요소 내에 `ScriptManager` 컨트롤을 배치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample1.aspx)]

<span data-ttu-id="6cbfa-114">그런 다음 페이지에 두 개의 `TextBox` 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-114">Next, add two `TextBox` controls to the page.</span></span> <span data-ttu-id="6cbfa-115">하나는 그래픽 슬라이더로 변환 되 고 다른 하나는 슬라이더의 위치를 보유 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-115">One will be transformed into a graphical slider, and the other one will hold the position of the slider.</span></span>

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample2.aspx)]

<span data-ttu-id="6cbfa-116">다음 단계는 이미 마지막 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-116">The next step is already the final step.</span></span> <span data-ttu-id="6cbfa-117">ASP.NET AJAX 컨트롤 도구 키트의 `SliderExtender` 컨트롤은 첫 번째 텍스트 상자 밖의 슬라이더를 만들고 슬라이더 위치가 변경 될 때 두 번째 텍스트 상자를 자동으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-117">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit makes a slider out of the first text box and automatically updates the second text box when the slider position changes.</span></span> <span data-ttu-id="6cbfa-118">이 작업을 수행 하려면 `SliderExtender`의 `TargetControlID` 특성을 첫 번째 텍스트 상자의 ID로 설정 해야 합니다. `BoundControlID` 특성을 두 번째 텍스트 상자의 ID로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-118">In order for that to work, The `SliderExtender`'s `TargetControlID` attribute must be set to the ID of the first text box; the `BoundControlID` attribute must be set to the ID of the second text box.</span></span>

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample3.aspx)]

<span data-ttu-id="6cbfa-119">브라우저에서 볼 수 있듯이 데이터 바인딩은 양방향으로 작동 합니다. 텍스트 상자에 새 값을 입력 하면 슬라이더의 위치가 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-119">As you can see in the browser, the data binding works in both directions: entering a new value in the text box updates the slider's position.</span></span> <span data-ttu-id="6cbfa-120">두 번째 텍스트 상자를 읽기 전용으로 설정 하는 경우 사용자가 해당 값을 수동으로 업데이트 하는 것이 더 어려워질 수 있도록 텍스트 필드에 weak 보호를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cbfa-120">If you make the second text box read only, you may add a weak protection to the text field so that it is harder for the user to manually update the value in there.</span></span>

<span data-ttu-id="6cbfa-121">[![슬라이더와 텍스트 상자가 동기화 되어 있습니다.](databinding-the-slider-control-vb/_static/image2.png)](databinding-the-slider-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6cbfa-121">[![Slider and text box are in sync](databinding-the-slider-control-vb/_static/image2.png)](databinding-the-slider-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="6cbfa-122">슬라이더와 텍스트 상자가 동기화 되어 있습니다 ([전체 크기 이미지를 보려면 클릭](databinding-the-slider-control-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="6cbfa-122">Slider and text box are in sync ([Click to view full-size image](databinding-the-slider-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="6cbfa-123">이전</span><span class="sxs-lookup"><span data-stu-id="6cbfa-123">Previous</span></span>](using-the-slider-control-with-auto-postback-vb.md)
