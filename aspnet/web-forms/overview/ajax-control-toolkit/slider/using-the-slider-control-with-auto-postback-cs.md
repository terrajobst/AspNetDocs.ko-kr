---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
title: 자동 포스트백에 슬라이더 컨트롤 사용 (C#) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 슬라이더 컨트롤은 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다. 슬라이더를 autopost 하 게 만들 수 있습니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4d85e9fb-91e6-41f2-9c13-754549b19c27
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
msc.type: authoredcontent
ms.openlocfilehash: 785d62108667fddac42994344cde265e82aca8f4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598371"
---
# <a name="using-the-slider-control-with-auto-postback-c"></a><span data-ttu-id="0eaa8-104">자동 포스트백에 슬라이더 컨트롤 사용 (C#)</span><span class="sxs-lookup"><span data-stu-id="0eaa8-104">Using the Slider Control With Auto-Postback (C#)</span></span>

<span data-ttu-id="0eaa8-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="0eaa8-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="0eaa8-106">[코드 다운로드](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="0eaa8-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)</span></span>

> <span data-ttu-id="0eaa8-107">AJAX 컨트롤 도구 키트의 슬라이더 컨트롤은 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaa8-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="0eaa8-108">값이 변경 되 면 슬라이더를 autopostback 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaa8-108">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="overview"></a><span data-ttu-id="0eaa8-109">개요</span><span class="sxs-lookup"><span data-stu-id="0eaa8-109">Overview</span></span>

<span data-ttu-id="0eaa8-110">AJAX 컨트롤 도구 키트의 슬라이더 컨트롤은 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaa8-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="0eaa8-111">값이 변경 되 면 슬라이더를 autopostback 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaa8-111">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="steps"></a><span data-ttu-id="0eaa8-112">단계</span><span class="sxs-lookup"><span data-stu-id="0eaa8-112">Steps</span></span>

<span data-ttu-id="0eaa8-113">변경 시 슬라이더가 자동으로 다시 게시 되도록 하기 위해 두 텍스트 상자에는 `AutoPostBack="true"`특성이 필요 합니다. 슬라이더 자체가 될 텍스트 상자와 슬라이더의 위치를 포함 하는 텍스트 상자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaa8-113">In order to make the slider automatically postback upon a change, both text boxes need the attribute `AutoPostBack="true"`: The text box that will become the slider itself, and the text box that holds the slider's position.</span></span> <span data-ttu-id="0eaa8-114">이에 대 한 필수 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaa8-114">Here is the required markup for that:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample1.aspx)]

<span data-ttu-id="0eaa8-115">ASP.NET AJAX 컨트롤 도구 키트의 `SliderExtender` 컨트롤은 슬라이더 기능을 두 개의 텍스트 상자에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaa8-115">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit assigns the slider functionality to the two text boxes:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample2.aspx)]

<span data-ttu-id="0eaa8-116">추가 레이블 요소는 나중에 다시 게시를 사용자에 게 알리는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaa8-116">An additional label element will later be used to inform the user of a postback:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample3.aspx)]

<span data-ttu-id="0eaa8-117">마지막으로 ASP.NET AJAX의 `ScriptManager` 제어는 컨트롤 Toolkit이 작동 하는 데 필요한 JavaScript를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaa8-117">Finally, the `ScriptManager` control of ASP.NET AJAX loads the required JavaScript for the Control Toolkit to work:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample4.aspx)]

<span data-ttu-id="0eaa8-118">이제 슬라이더가 다시 게시 됩니다. 서버 쪽에서이 이벤트를 catch 하 고 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaa8-118">Now the slider is posting back; on the server-side, this event may be caught and acted upon:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample5.aspx)]

<span data-ttu-id="0eaa8-119">[슬라이더를 이동 ![포스트백이 트리거됩니다.](using-the-slider-control-with-auto-postback-cs/_static/image2.png)](using-the-slider-control-with-auto-postback-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0eaa8-119">[![Moving the slider triggers a postback](using-the-slider-control-with-auto-postback-cs/_static/image2.png)](using-the-slider-control-with-auto-postback-cs/_static/image1.png)</span></span>

<span data-ttu-id="0eaa8-120">슬라이더를 이동 하면 다시 게시가 트리거됩니다 ([전체 크기 이미지를 보려면 클릭](using-the-slider-control-with-auto-postback-cs/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="0eaa8-120">Moving the slider triggers a postback ([Click to view full-size image](using-the-slider-control-with-auto-postback-cs/_static/image3.png))</span></span>

<span data-ttu-id="0eaa8-121">[이후에 ![이 변경 날짜는 레이블에 기록 됩니다.](using-the-slider-control-with-auto-postback-cs/_static/image5.png)](using-the-slider-control-with-auto-postback-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="0eaa8-121">[![Afterwards, the date of this change is written in the label](using-the-slider-control-with-auto-postback-cs/_static/image5.png)](using-the-slider-control-with-auto-postback-cs/_static/image4.png)</span></span>

<span data-ttu-id="0eaa8-122">그런 다음이 변경 날짜는 레이블에 기록 됩니다 ([전체 크기 이미지를 보려면 클릭](using-the-slider-control-with-auto-postback-cs/_static/image6.png)).</span><span class="sxs-lookup"><span data-stu-id="0eaa8-122">Afterwards, the date of this change is written in the label ([Click to view full-size image](using-the-slider-control-with-auto-postback-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="0eaa8-123">다음</span><span class="sxs-lookup"><span data-stu-id="0eaa8-123">Next</span></span>](databinding-the-slider-control-cs.md)
