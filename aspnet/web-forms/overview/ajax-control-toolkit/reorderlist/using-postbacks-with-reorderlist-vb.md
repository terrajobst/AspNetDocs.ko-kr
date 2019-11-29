---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
title: ReorderList와 함께 다시 게시 사용 (VB) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 ReorderList 컨트롤은 끌어서 놓기를 통해 사용자가 다시 정렬할 수 있는 목록을 제공 합니다. 목록이 다시 정렬 될 때마다 po ...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e5b6ed70-19ed-4024-ba4f-6d78e8acdc0f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 5d6075e40df2c32df6c0d801243eff98fa7790b2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611369"
---
# <a name="using-postbacks-with-reorderlist-vb"></a><span data-ttu-id="8e4ee-104">ReorderList에 포스트백 사용(VB)</span><span class="sxs-lookup"><span data-stu-id="8e4ee-104">Using Postbacks with ReorderList (VB)</span></span>

<span data-ttu-id="8e4ee-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="8e4ee-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="8e4ee-106">[코드 다운로드](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="8e4ee-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)</span></span>

> <span data-ttu-id="8e4ee-107">AJAX 컨트롤 도구 키트의 ReorderList 컨트롤은 끌어서 놓기를 통해 사용자가 다시 정렬할 수 있는 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4ee-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="8e4ee-108">목록이 다시 정렬 될 때마다 포스트백은 서버에 변경 내용을 알립니다.</span><span class="sxs-lookup"><span data-stu-id="8e4ee-108">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>

## <a name="overview"></a><span data-ttu-id="8e4ee-109">개요</span><span class="sxs-lookup"><span data-stu-id="8e4ee-109">Overview</span></span>

<span data-ttu-id="8e4ee-110">AJAX 컨트롤 도구 키트의 `ReorderList` 컨트롤은 끌어서 놓기를 통해 사용자가 다시 정렬할 수 있는 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4ee-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="8e4ee-111">목록이 다시 정렬 될 때마다 포스트백은 서버에 변경 내용을 알립니다.</span><span class="sxs-lookup"><span data-stu-id="8e4ee-111">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>

## <a name="steps"></a><span data-ttu-id="8e4ee-112">단계</span><span class="sxs-lookup"><span data-stu-id="8e4ee-112">Steps</span></span>

<span data-ttu-id="8e4ee-113">`ReorderList` 컨트롤에 사용할 수 있는 데이터 소스는 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4ee-113">There are several possible data sources for the `ReorderList` control.</span></span> <span data-ttu-id="8e4ee-114">하나는 `XmlDataSource` 컨트롤을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8e4ee-114">One is to use an `XmlDataSource` control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample1.aspx)]

<span data-ttu-id="8e4ee-115">이 XML을 `ReorderList` 컨트롤에 바인딩하고 다시 게시를 사용 하도록 설정 하려면 다음 특성을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4ee-115">In order to bind this XML to a `ReorderList` control and enable postbacks, the following attributes must be set:</span></span>

- <span data-ttu-id="8e4ee-116">`DataSourceID`: 데이터 원본의 ID</span><span class="sxs-lookup"><span data-stu-id="8e4ee-116">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="8e4ee-117">`SortOrderField`: 정렬할 속성</span><span class="sxs-lookup"><span data-stu-id="8e4ee-117">`SortOrderField`: The property to sort by</span></span>
- <span data-ttu-id="8e4ee-118">`AllowReorder`: 사용자가 목록 요소를 다시 정렬할 수 있는지 여부</span><span class="sxs-lookup"><span data-stu-id="8e4ee-118">`AllowReorder`: Whether to allow the user to reorder the list elements</span></span>
- <span data-ttu-id="8e4ee-119">`PostBackOnReorder`: 목록이 다시 정렬 될 때마다 다시 게시를 만들지 여부</span><span class="sxs-lookup"><span data-stu-id="8e4ee-119">`PostBackOnReorder`: Whether to create a postback whenever the list is rearranged</span></span>

<span data-ttu-id="8e4ee-120">다음은 컨트롤에 대 한 적절 한 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="8e4ee-120">Here is the appropriate markup for the control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample2.aspx)]

<span data-ttu-id="8e4ee-121">`ReorderList` 컨트롤 내에서 `Eval()` 메서드를 사용 하 여 데이터 소스의 특정 데이터를 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4ee-121">Within the `ReorderList` control, specific data from the data source may be bound using the `Eval()` method:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample3.aspx)]

<span data-ttu-id="8e4ee-122">페이지의 임의 위치에서 마지막으로 다시 정렬 하는 동안 레이블이 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4ee-122">At an arbitrary position on the page, a label will hold the information when the last reordering occurred:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample4.aspx)]

<span data-ttu-id="8e4ee-123">이 레이블은 서버 쪽 코드의 텍스트로 채워지고 다시 게시를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4ee-123">This label is filled with text in the server-side code, handling the postback:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample5.aspx)]

<span data-ttu-id="8e4ee-124">마지막으로 ASP.NET AJAX 및 Control Toolkit의 기능을 활성화 하기 위해 페이지에 `ScriptManager` 컨트롤을 넣어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4ee-124">Finally, in order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put on the page:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample6.aspx)]

<span data-ttu-id="8e4ee-125">[각 다시 정렬을 ![포스트백이 트리거됩니다.](using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8e4ee-125">[![Each reordering triggers a postback](using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)</span></span>

<span data-ttu-id="8e4ee-126">다시 정렬 하면 다시 게시가 트리거됩니다 ([전체 크기 이미지를 보려면 클릭](using-postbacks-with-reorderlist-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="8e4ee-126">Each reordering triggers a postback ([Click to view full-size image](using-postbacks-with-reorderlist-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8e4ee-127">[이전](drag-and-drop-via-reorderlist-cs.md)
> [다음](drag-and-drop-via-reorderlist-vb.md)</span><span class="sxs-lookup"><span data-stu-id="8e4ee-127">[Previous](drag-and-drop-via-reorderlist-cs.md)
[Next](drag-and-drop-via-reorderlist-vb.md)</span></span>
