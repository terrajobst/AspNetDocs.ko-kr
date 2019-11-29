---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
title: DropShadow의 Z-인덱스 조정 (C#) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 DropShadow 컨트롤은 그림자가 있는 패널을 확장 합니다. 그러나이 그림자는 다른 컨트롤과 충돌 하는 경우가 있습니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 14133833-e518-4347-87b9-6b6f71f14a77
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
msc.type: authoredcontent
ms.openlocfilehash: 12bc7f0430f1f30ff964cd9547ee1e9b0aa7423c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74574274"
---
# <a name="adjusting-the-z-index-of-a-dropshadow-c"></a><span data-ttu-id="3f3ca-104">DropShadow의 Z-인덱스 조정(C#)</span><span class="sxs-lookup"><span data-stu-id="3f3ca-104">Adjusting the Z-Index of a DropShadow (C#)</span></span>

<span data-ttu-id="3f3ca-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="3f3ca-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="3f3ca-106">[코드 다운로드](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="3f3ca-106">[Download Code](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1CS.pdf)</span></span>

> <span data-ttu-id="3f3ca-107">AJAX 컨트롤 도구 키트의 DropShadow 컨트롤은 그림자가 있는 패널을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f3ca-107">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="3f3ca-108">그러나이 그림자는 ASP.NET Menu 컨트롤과 같은 다른 컨트롤과 충돌 하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f3ca-108">However this shadow sometimes conflicts with other controls, for instance the ASP.NET Menu control.</span></span> <span data-ttu-id="3f3ca-109">메뉴 항목이 표시 되 면 드롭 그림자 뒤에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f3ca-109">When a menu entry pops up, it appears behind the drop shadow.</span></span>

## <a name="overview"></a><span data-ttu-id="3f3ca-110">개요</span><span class="sxs-lookup"><span data-stu-id="3f3ca-110">Overview</span></span>

<span data-ttu-id="3f3ca-111">AJAX 컨트롤 도구 키트의 DropShadow 컨트롤은 그림자가 있는 패널을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f3ca-111">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="3f3ca-112">그러나이 그림자는 ASP.NET Menu 컨트롤과 같은 다른 컨트롤과 충돌 하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f3ca-112">However this shadow sometimes conflicts with other controls, for instance the ASP.NET Menu control.</span></span> <span data-ttu-id="3f3ca-113">메뉴 항목이 표시 되 면 드롭 그림자 뒤에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f3ca-113">When a menu entry pops up, it appears behind the drop shadow.</span></span>

## <a name="steps"></a><span data-ttu-id="3f3ca-114">단계</span><span class="sxs-lookup"><span data-stu-id="3f3ca-114">Steps</span></span>

<span data-ttu-id="3f3ca-115">코드는 패널 자체를 사용 하 여 시작 됩니다 효과를 표시 하는 데 충분 한 텍스트를 포함 하는 충분 한 텍스트를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f3ca-115">The code commences with the Panel itself, containing enough text so that the panel contains enough text for the effect to be visible:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample1.aspx)]

<span data-ttu-id="3f3ca-116">다른 패널은 `panelShadow` 패널 바로 앞에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f3ca-116">Another panel is placed directly before the `panelShadow` panel.</span></span> <span data-ttu-id="3f3ca-117">메뉴 항목이 가로 방향으로 표시 되는 메뉴를 포함 합니다. 즉, 메뉴 항목이 `dropShadow` 패널에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f3ca-117">It contains a menu with horizontal orientation so that menu entries appear over (or rather: under) the `dropShadow` panel):</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample2.aspx)]

<span data-ttu-id="3f3ca-118">그런 다음, 그림자 효과를 적용 하 여 `panelShadow` 패널을 확장 하기 위해 `DropShadowExtender` 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f3ca-118">Then, the `DropShadowExtender` is added to extend the `panelShadow` panel with a drop shadow effect:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample3.aspx)]

<span data-ttu-id="3f3ca-119">마지막으로 ASP.NET AJAX `ScriptManager` 컨트롤을 사용 하면 컨트롤 도구 키트가 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f3ca-119">Finally, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample4.aspx)]

<span data-ttu-id="3f3ca-120">이 스크립트를 실행 하면 패널 아래에 메뉴 항목이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f3ca-120">When you run this script, the menu entries appear underneath the panel.</span></span> <span data-ttu-id="3f3ca-121">그러나이 메뉴는 `panel` CSS 클래스를 사용 하 여 요소가 다른 패널 앞에 표시 되도록 하는 두 가지 작업을 정의 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f3ca-121">However the menu uses the CSS class `panel` where you just have to define two things to make elements appear in front of the other panel:</span></span>

- <span data-ttu-id="3f3ca-122">상대 위치 지정</span><span class="sxs-lookup"><span data-stu-id="3f3ca-122">Relative positioning</span></span>
- <span data-ttu-id="3f3ca-123">양의 z-인덱스</span><span class="sxs-lookup"><span data-stu-id="3f3ca-123">A positive z-index</span></span>

[!code-css[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample5.css)]

<span data-ttu-id="3f3ca-124">그러면 `DropShadowExtender` 컨트롤이 메뉴 컨트롤과 더 이상 충돌 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f3ca-124">Then, the `DropShadowExtender` control does not conflict any longer with the Menu control.</span></span>

<span data-ttu-id="3f3ca-125">[이전 ![: 메뉴 항목이 표시 되지 않습니다.](adjusting-the-z-index-of-a-dropshadow-cs/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3f3ca-125">[![Before: The menu entry is not visible](adjusting-the-z-index-of-a-dropshadow-cs/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image1.png)</span></span>

<span data-ttu-id="3f3ca-126">이전: 메뉴 항목이 표시 되지 않음 ([전체 크기 이미지를 보려면 클릭](adjusting-the-z-index-of-a-dropshadow-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="3f3ca-126">Before: The menu entry is not visible ([Click to view full-size image](adjusting-the-z-index-of-a-dropshadow-cs/_static/image3.png))</span></span>

<span data-ttu-id="3f3ca-127">[![후: 메뉴 항목이 표시 됩니다.](adjusting-the-z-index-of-a-dropshadow-cs/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="3f3ca-127">[![After: The menu entry appears](adjusting-the-z-index-of-a-dropshadow-cs/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image4.png)</span></span>

<span data-ttu-id="3f3ca-128">이후: 메뉴 항목이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](adjusting-the-z-index-of-a-dropshadow-cs/_static/image6.png)).</span><span class="sxs-lookup"><span data-stu-id="3f3ca-128">After: The menu entry appears ([Click to view full-size image](adjusting-the-z-index-of-a-dropshadow-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="3f3ca-129">다음</span><span class="sxs-lookup"><span data-stu-id="3f3ca-129">Next</span></span>](manipulating-dropshadow-properties-from-client-code-cs.md)
