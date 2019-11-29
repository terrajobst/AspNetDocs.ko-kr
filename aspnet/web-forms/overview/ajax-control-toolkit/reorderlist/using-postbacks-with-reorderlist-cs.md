---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-cs
title: ReorderList (C#) |에서 다시 게시 사용 Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 ReorderList 컨트롤은 끌어서 놓기를 통해 사용자가 다시 정렬할 수 있는 목록을 제공 합니다. 목록이 다시 정렬 될 때마다 po ...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 70d5d106-b547-442c-a7fd-3492b3e3d646
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-cs
msc.type: authoredcontent
ms.openlocfilehash: f83201fc6fd458e730b6bb5ffee184d303b52e90
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611381"
---
# <a name="using-postbacks-with-reorderlist-c"></a><span data-ttu-id="91f94-104">ReorderList에 포스트백 사용(C#)</span><span class="sxs-lookup"><span data-stu-id="91f94-104">Using Postbacks with ReorderList (C#)</span></span>

<span data-ttu-id="91f94-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="91f94-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="91f94-106">[코드 다운로드](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="91f94-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4CS.pdf)</span></span>

> <span data-ttu-id="91f94-107">AJAX 컨트롤 도구 키트의 ReorderList 컨트롤은 끌어서 놓기를 통해 사용자가 다시 정렬할 수 있는 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="91f94-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="91f94-108">목록이 다시 정렬 될 때마다 포스트백은 서버에 변경 내용을 알립니다.</span><span class="sxs-lookup"><span data-stu-id="91f94-108">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>

## <a name="overview"></a><span data-ttu-id="91f94-109">개요</span><span class="sxs-lookup"><span data-stu-id="91f94-109">Overview</span></span>

<span data-ttu-id="91f94-110">AJAX 컨트롤 도구 키트의 `ReorderList` 컨트롤은 끌어서 놓기를 통해 사용자가 다시 정렬할 수 있는 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="91f94-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="91f94-111">목록이 다시 정렬 될 때마다 포스트백은 서버에 변경 내용을 알립니다.</span><span class="sxs-lookup"><span data-stu-id="91f94-111">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>

## <a name="steps"></a><span data-ttu-id="91f94-112">단계</span><span class="sxs-lookup"><span data-stu-id="91f94-112">Steps</span></span>

<span data-ttu-id="91f94-113">`ReorderList` 컨트롤에 사용할 수 있는 데이터 소스는 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91f94-113">There are several possible data sources for the `ReorderList` control.</span></span> <span data-ttu-id="91f94-114">하나는 `XmlDataSource` 컨트롤을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="91f94-114">One is to use an `XmlDataSource` control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample1.aspx)]

<span data-ttu-id="91f94-115">이 XML을 `ReorderList` 컨트롤에 바인딩하고 다시 게시를 사용 하도록 설정 하려면 다음 특성을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91f94-115">In order to bind this XML to a `ReorderList` control and enable postbacks, the following attributes must be set:</span></span>

- <span data-ttu-id="91f94-116">`DataSourceID`: 데이터 원본의 ID</span><span class="sxs-lookup"><span data-stu-id="91f94-116">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="91f94-117">`SortOrderField`: 정렬할 속성</span><span class="sxs-lookup"><span data-stu-id="91f94-117">`SortOrderField`: The property to sort by</span></span>
- <span data-ttu-id="91f94-118">`AllowReorder`: 사용자가 목록 요소를 다시 정렬할 수 있는지 여부</span><span class="sxs-lookup"><span data-stu-id="91f94-118">`AllowReorder`: Whether to allow the user to reorder the list elements</span></span>
- <span data-ttu-id="91f94-119">`PostBackOnReorder`: 목록이 다시 정렬 될 때마다 다시 게시를 만들지 여부</span><span class="sxs-lookup"><span data-stu-id="91f94-119">`PostBackOnReorder`: Whether to create a postback whenever the list is rearranged</span></span>

<span data-ttu-id="91f94-120">다음은 컨트롤에 대 한 적절 한 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="91f94-120">Here is the appropriate markup for the control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample2.aspx)]

<span data-ttu-id="91f94-121">`ReorderList` 컨트롤 내에서 `Eval()` 메서드를 사용 하 여 데이터 소스의 특정 데이터를 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91f94-121">Within the `ReorderList` control, specific data from the data source may be bound using the `Eval()` method:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample3.aspx)]

<span data-ttu-id="91f94-122">페이지의 임의 위치에서 마지막으로 다시 정렬 하는 동안 레이블이 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="91f94-122">At an arbitrary position on the page, a label will hold the information when the last reordering occurred:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample4.aspx)]

<span data-ttu-id="91f94-123">이 레이블은 서버 쪽 코드의 텍스트로 채워지고 다시 게시를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="91f94-123">This label is filled with text in the server-side code, handling the postback:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample5.aspx)]

<span data-ttu-id="91f94-124">마지막으로 ASP.NET AJAX 및 Control Toolkit의 기능을 활성화 하기 위해 페이지에 `ScriptManager` 컨트롤을 넣어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91f94-124">Finally, in order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put on the page:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample6.aspx)]

<span data-ttu-id="91f94-125">[각 다시 정렬을 ![포스트백이 트리거됩니다.](using-postbacks-with-reorderlist-cs/_static/image2.png)](using-postbacks-with-reorderlist-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="91f94-125">[![Each reordering triggers a postback](using-postbacks-with-reorderlist-cs/_static/image2.png)](using-postbacks-with-reorderlist-cs/_static/image1.png)</span></span>

<span data-ttu-id="91f94-126">다시 정렬 하면 다시 게시가 트리거됩니다 ([전체 크기 이미지를 보려면 클릭](using-postbacks-with-reorderlist-cs/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="91f94-126">Each reordering triggers a postback ([Click to view full-size image](using-postbacks-with-reorderlist-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="91f94-127">다음</span><span class="sxs-lookup"><span data-stu-id="91f94-127">Next</span></span>](drag-and-drop-via-reorderlist-cs.md)
