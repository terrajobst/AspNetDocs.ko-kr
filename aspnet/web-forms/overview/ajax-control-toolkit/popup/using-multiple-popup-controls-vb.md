---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
title: 여러 Popup 컨트롤 사용 (VB) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 PopupControl extender는 다른 컨트롤이 활성화 될 때 팝업을 쉽게 트리거하는 방법을 제공 합니다. M ...을 사용 하는 것도 가능 합니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4da43d77-f6c4-43a8-9124-f1e8e1c8f0a2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: e1f4ff64e9fdf48ea63b75c97acd53a64b5ab5ce
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496325"
---
# <a name="using-multiple-popup-controls-vb"></a><span data-ttu-id="4c4bd-104">여러 팝업 컨트롤 사용(VB)</span><span class="sxs-lookup"><span data-stu-id="4c4bd-104">Using Multiple Popup Controls (VB)</span></span>

<span data-ttu-id="4c4bd-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="4c4bd-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="4c4bd-106">[코드 다운로드](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="4c4bd-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1VB.pdf)</span></span>

> <span data-ttu-id="4c4bd-107">AJAX 컨트롤 도구 키트의 PopupControl extender는 다른 컨트롤이 활성화 될 때 팝업을 쉽게 트리거하는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c4bd-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="4c4bd-108">또한 한 페이지에서 둘 이상의 popup 컨트롤을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c4bd-108">It is also possible to use more than one popup control on one page.</span></span>

## <a name="overview"></a><span data-ttu-id="4c4bd-109">개요</span><span class="sxs-lookup"><span data-stu-id="4c4bd-109">Overview</span></span>

<span data-ttu-id="4c4bd-110">AJAX 컨트롤 도구 키트의 PopupControl extender는 다른 컨트롤이 활성화 될 때 팝업을 쉽게 트리거하는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c4bd-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="4c4bd-111">또한 한 페이지에서 둘 이상의 popup 컨트롤을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c4bd-111">It is also possible to use more than one popup control on one page.</span></span>

## <a name="steps"></a><span data-ttu-id="4c4bd-112">단계</span><span class="sxs-lookup"><span data-stu-id="4c4bd-112">Steps</span></span>

<span data-ttu-id="4c4bd-113">ASP.NET AJAX 및 Control Toolkit의 기능을 활성화 하려면 페이지의 아무 곳에 나 `<form>` 요소 내에 `ScriptManager` 컨트롤을 배치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c4bd-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample1.aspx)]

<span data-ttu-id="4c4bd-114">다음으로 팝업으로 사용 되는 패널을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c4bd-114">Next, add a panel which serves as the popup.</span></span> <span data-ttu-id="4c4bd-115">현재 시나리오에서 패널은 `Calendar` 컨트롤을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c4bd-115">In the current scenario, the panel contains a `Calendar` control.</span></span> <span data-ttu-id="4c4bd-116">달력의 포스트백으로 인 한 페이지 새로 고침을 방지 하기 위해 패널은 `UpdatePanel` 컨트롤 내에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c4bd-116">In order to avoid the page refreshes caused by the Calendar's postbacks, the panel is put within an `UpdatePanel` control:</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample2.aspx)]

<span data-ttu-id="4c4bd-117">페이지에는 두 개의 텍스트 상자도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c4bd-117">The page also contains two text boxes.</span></span> <span data-ttu-id="4c4bd-118">텍스트 상자를 활성화 한 후에는 각 입력란에 대 한 달력 팝업이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c4bd-118">For each text box, the calendar popup shall appear once the text box is activated.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample3.aspx)]

<span data-ttu-id="4c4bd-119">이제 `PopupControlExtender`를 사용 하 여 두 개의 텍스트 상자를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c4bd-119">Now extend each of the two text boxes with a `PopupControlExtender`.</span></span> <span data-ttu-id="4c4bd-120">`TargetControlID` 특성은 extender에 연결 된 컨트롤의 ID를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c4bd-120">The `TargetControlID` attribute provides the ID of the control tied to the extender.</span></span> <span data-ttu-id="4c4bd-121">`PopupControlID` 특성에는 팝업 패널의 ID가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c4bd-121">The `PopupControlID` attribute contains the ID of the popup panel.</span></span> <span data-ttu-id="4c4bd-122">이 경우 두 extender는 동일한 패널을 표시 하지만 다른 패널도 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c4bd-122">In this case, both extenders show the same panel, but different panels are possible, as well.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample4.aspx)]

<span data-ttu-id="4c4bd-123">이제 텍스트 필드를 클릭할 때마다 필드 아래에 달력이 표시 되어 날짜를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c4bd-123">Now whenever you click within a text field, a calendar appears below the field, allowing you to select a date.</span></span> <span data-ttu-id="4c4bd-124">선택한 날짜를 텍스트 상자에 다시 가져오는 것은 다른 자습서에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c4bd-124">(Getting the selected date back into the text boxes will be covered in a different tutorial.)</span></span>

<span data-ttu-id="4c4bd-125">[사용자가 텍스트 상자를 클릭할 때 달력이 표시 되는 ![](using-multiple-popup-controls-vb/_static/image2.png)](using-multiple-popup-controls-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4c4bd-125">[![The Calendar appears when the user clicks into the textbox](using-multiple-popup-controls-vb/_static/image2.png)](using-multiple-popup-controls-vb/_static/image1.png)</span></span>

<span data-ttu-id="4c4bd-126">사용자가 텍스트 상자를 클릭 하면 달력이 나타납니다 ([전체 크기 이미지를 보려면 클릭](using-multiple-popup-controls-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="4c4bd-126">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](using-multiple-popup-controls-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4c4bd-127">[이전](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
> [다음](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)</span><span class="sxs-lookup"><span data-stu-id="4c4bd-127">[Previous](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
[Next](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)</span></span>
