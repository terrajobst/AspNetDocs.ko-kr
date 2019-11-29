---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
title: 자동 포스트백에 슬라이더 컨트롤 사용 (VB) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 슬라이더 컨트롤은 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다. 슬라이더를 autopost 하 게 만들 수 있습니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 41d1abba-97a5-4a45-9b44-d05624c19777
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
msc.type: authoredcontent
ms.openlocfilehash: e7a3286bcf7ca844f5dcfa4848c15e0bd4767c0f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598536"
---
# <a name="using-the-slider-control-with-auto-postback-vb"></a><span data-ttu-id="84ed6-104">자동 포스트백에 슬라이더 컨트롤 사용 (VB)</span><span class="sxs-lookup"><span data-stu-id="84ed6-104">Using the Slider Control With Auto-Postback (VB)</span></span>

<span data-ttu-id="84ed6-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="84ed6-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="84ed6-106">[코드 다운로드](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="84ed6-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1VB.pdf)</span></span>

> <span data-ttu-id="84ed6-107">AJAX 컨트롤 도구 키트의 슬라이더 컨트롤은 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="84ed6-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="84ed6-108">값이 변경 되 면 슬라이더를 autopostback 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ed6-108">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="overview"></a><span data-ttu-id="84ed6-109">개요</span><span class="sxs-lookup"><span data-stu-id="84ed6-109">Overview</span></span>

<span data-ttu-id="84ed6-110">AJAX 컨트롤 도구 키트의 슬라이더 컨트롤은 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="84ed6-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="84ed6-111">값이 변경 되 면 슬라이더를 autopostback 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ed6-111">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="steps"></a><span data-ttu-id="84ed6-112">단계</span><span class="sxs-lookup"><span data-stu-id="84ed6-112">Steps</span></span>

<span data-ttu-id="84ed6-113">변경 시 슬라이더가 자동으로 다시 게시 되도록 하기 위해 두 텍스트 상자에는 `AutoPostBack="true"`특성이 필요 합니다. 슬라이더 자체가 될 텍스트 상자와 슬라이더의 위치를 포함 하는 텍스트 상자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="84ed6-113">In order to make the slider automatically postback upon a change, both text boxes need the attribute `AutoPostBack="true"`: The text box that will become the slider itself, and the text box that holds the slider's position.</span></span> <span data-ttu-id="84ed6-114">이에 대 한 필수 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="84ed6-114">Here is the required markup for that:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample1.aspx)]

<span data-ttu-id="84ed6-115">ASP.NET AJAX 컨트롤 도구 키트의 `SliderExtender` 컨트롤은 슬라이더 기능을 두 개의 텍스트 상자에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="84ed6-115">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit assigns the slider functionality to the two text boxes:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample2.aspx)]

<span data-ttu-id="84ed6-116">추가 레이블 요소는 나중에 다시 게시를 사용자에 게 알리는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84ed6-116">An additional label element will later be used to inform the user of a postback:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample3.aspx)]

<span data-ttu-id="84ed6-117">마지막으로 ASP.NET AJAX의 `ScriptManager` 제어는 컨트롤 Toolkit이 작동 하는 데 필요한 JavaScript를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="84ed6-117">Finally, the `ScriptManager` control of ASP.NET AJAX loads the required JavaScript for the Control Toolkit to work:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample4.aspx)]

<span data-ttu-id="84ed6-118">이제 슬라이더가 다시 게시 됩니다. 서버 쪽에서이 이벤트를 catch 하 고 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ed6-118">Now the slider is posting back; on the server-side, this event may be caught and acted upon:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample5.aspx)]

<span data-ttu-id="84ed6-119">[슬라이더를 이동 ![포스트백이 트리거됩니다.](using-the-slider-control-with-auto-postback-vb/_static/image2.png)](using-the-slider-control-with-auto-postback-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="84ed6-119">[![Moving the slider triggers a postback](using-the-slider-control-with-auto-postback-vb/_static/image2.png)](using-the-slider-control-with-auto-postback-vb/_static/image1.png)</span></span>

<span data-ttu-id="84ed6-120">슬라이더를 이동 하면 다시 게시가 트리거됩니다 ([전체 크기 이미지를 보려면 클릭](using-the-slider-control-with-auto-postback-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="84ed6-120">Moving the slider triggers a postback ([Click to view full-size image](using-the-slider-control-with-auto-postback-vb/_static/image3.png))</span></span>

<span data-ttu-id="84ed6-121">[이후에 ![이 변경 날짜는 레이블에 기록 됩니다.](using-the-slider-control-with-auto-postback-vb/_static/image5.png)](using-the-slider-control-with-auto-postback-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="84ed6-121">[![Afterwards, the date of this change is written in the label](using-the-slider-control-with-auto-postback-vb/_static/image5.png)](using-the-slider-control-with-auto-postback-vb/_static/image4.png)</span></span>

<span data-ttu-id="84ed6-122">그런 다음이 변경 날짜는 레이블에 기록 됩니다 ([전체 크기 이미지를 보려면 클릭](using-the-slider-control-with-auto-postback-vb/_static/image6.png)).</span><span class="sxs-lookup"><span data-stu-id="84ed6-122">Afterwards, the date of this change is written in the label ([Click to view full-size image](using-the-slider-control-with-auto-postback-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="84ed6-123">[이전](databinding-the-slider-control-cs.md)
> [다음](databinding-the-slider-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="84ed6-123">[Previous](databinding-the-slider-control-cs.md)
[Next](databinding-the-slider-control-vb.md)</span></span>
