---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-vb
title: ReorderList를 통해 끌어서 놓기 (VB) | Microsoft Docs
author: wenz
description: /data-access/tutorials/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 848e6bcf-4c3f-4d14-974d-e45b9444ab79
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 3f7c5749053d8bf587467fb1939fca05ce2872a4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598678"
---
# <a name="drag-and-drop-via-reorderlist-vb"></a><span data-ttu-id="63a5f-103">ReorderList를 통해 끌어서 놓기(VB)</span><span class="sxs-lookup"><span data-stu-id="63a5f-103">Drag and Drop via ReorderList (VB)</span></span>

<span data-ttu-id="63a5f-104">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="63a5f-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="63a5f-105">[코드 다운로드](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="63a5f-105">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5VB.pdf)</span></span>

> <span data-ttu-id="63a5f-106">AJAX 컨트롤 도구 키트의 ReorderList 컨트롤은 끌어서 놓기를 통해 사용자가 다시 정렬할 수 있는 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="63a5f-106">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="63a5f-107">목록의 현재 순서는 서버에 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63a5f-107">The current order of the list shall be persisted on the server.</span></span>

## <a name="overview"></a><span data-ttu-id="63a5f-108">개요</span><span class="sxs-lookup"><span data-stu-id="63a5f-108">Overview</span></span>

<span data-ttu-id="63a5f-109">AJAX 컨트롤 도구 키트의 `ReorderList` 컨트롤은 끌어서 놓기를 통해 사용자가 다시 정렬할 수 있는 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="63a5f-109">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="63a5f-110">목록의 현재 순서는 서버에 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63a5f-110">The current order of the list shall be persisted on the server.</span></span>

## <a name="steps"></a><span data-ttu-id="63a5f-111">단계</span><span class="sxs-lookup"><span data-stu-id="63a5f-111">Steps</span></span>

<span data-ttu-id="63a5f-112">`ReorderList` 컨트롤은 데이터베이스의 데이터를 목록에 바인딩하는 것을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="63a5f-112">The `ReorderList` control supports binding data from a database to the list.</span></span> <span data-ttu-id="63a5f-113">무엇 보다도, 목록 요소 순서에 대 한 변경 내용을 데이터 저장소에 다시 쓸 수 있도록 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="63a5f-113">Best of all, it also supports writing changes to the order of the list element back to the data store.</span></span>

<span data-ttu-id="63a5f-114">이 샘플에서는 Microsoft SQL Server 2005 Express Edition을 데이터 저장소로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="63a5f-114">This sample uses Microsoft SQL Server 2005 Express Edition as the data store.</span></span> <span data-ttu-id="63a5f-115">데이터베이스는 express edition을 포함 하 여 Visual Studio 설치의 선택적 (및 무료) 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="63a5f-115">The database is an optional (and free) part of a Visual Studio installation, including express edition.</span></span> <span data-ttu-id="63a5f-116">[https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)에서 별도의 다운로드로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63a5f-116">It is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="63a5f-117">이 샘플에서는 SQL Server 2005 Express Edition 인스턴스가 `SQLEXPRESS` 호출 되 고 웹 서버와 같은 컴퓨터에 있는 것으로 가정 합니다. 이는 기본 설정 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="63a5f-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="63a5f-118">설정이 다른 경우 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63a5f-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="63a5f-119">데이터베이스를 설정 하는 가장 쉬운 방법은 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) )를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="63a5f-119">The easiest way to set up the database is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span></span> <span data-ttu-id="63a5f-120">서버에 연결 하 여 `Databases`를 두 번 클릭 하 고 새 데이터베이스를 만듭니다 (마우스 오른쪽 단추를 클릭 하 고 `New Database`를 선택) `Tutorials`.</span><span class="sxs-lookup"><span data-stu-id="63a5f-120">Connect to the server, double-click on `Databases` and create a new database (right-click and choose `New Database`) called `Tutorials`.</span></span>

<span data-ttu-id="63a5f-121">이 데이터베이스에서 다음 네 개의 열을 사용 하 여 `AJAX` 라는 새 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="63a5f-121">In this database, create a new table called `AJAX` with the following four columns:</span></span>

- <span data-ttu-id="63a5f-122">`id` (기본 키, 정수, id, NULL 아님)</span><span class="sxs-lookup"><span data-stu-id="63a5f-122">`id` (primary key, integer, identity, not NULL)</span></span>
- <span data-ttu-id="63a5f-123">`char` (char (1), NULL)</span><span class="sxs-lookup"><span data-stu-id="63a5f-123">`char` (char(1), NULL)</span></span>
- <span data-ttu-id="63a5f-124">`description` (varchar (50), NULL)</span><span class="sxs-lookup"><span data-stu-id="63a5f-124">`description` (varchar(50), NULL)</span></span>
- <span data-ttu-id="63a5f-125">`position` (int, NULL)</span><span class="sxs-lookup"><span data-stu-id="63a5f-125">`position` (int, NULL)</span></span>

<span data-ttu-id="63a5f-126">[AJAX 테이블의 레이아웃 ![](drag-and-drop-via-reorderlist-vb/_static/image2.png)](drag-and-drop-via-reorderlist-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="63a5f-126">[![The layout of the AJAX table](drag-and-drop-via-reorderlist-vb/_static/image2.png)](drag-and-drop-via-reorderlist-vb/_static/image1.png)</span></span>

<span data-ttu-id="63a5f-127">AJAX 테이블의 레이아웃 ([전체 크기 이미지를 보려면 클릭](drag-and-drop-via-reorderlist-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="63a5f-127">The layout of the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-vb/_static/image3.png))</span></span>

<span data-ttu-id="63a5f-128">그런 다음 두 개의 값으로 테이블을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="63a5f-128">Next, fill the table with a couple of values.</span></span> <span data-ttu-id="63a5f-129">`position` 열에는 요소의 정렬 순서가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63a5f-129">Note that the `position` column holds the sort order of the elements.</span></span>

<span data-ttu-id="63a5f-130">[AJAX 테이블의 초기 데이터 ![](drag-and-drop-via-reorderlist-vb/_static/image5.png)](drag-and-drop-via-reorderlist-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="63a5f-130">[![The initial data in the AJAX table](drag-and-drop-via-reorderlist-vb/_static/image5.png)](drag-and-drop-via-reorderlist-vb/_static/image4.png)</span></span>

<span data-ttu-id="63a5f-131">AJAX 테이블의 초기 데이터 ([전체 크기 이미지를 보려면 클릭](drag-and-drop-via-reorderlist-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="63a5f-131">The initial data in the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-vb/_static/image6.png))</span></span>

<span data-ttu-id="63a5f-132">다음 단계에서는 새 데이터베이스와 해당 테이블과 통신 하는 `SqlDataSource` 컨트롤을 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63a5f-132">The next step requires to generate an `SqlDataSource` control to communicate with the new database and its table.</span></span> <span data-ttu-id="63a5f-133">데이터 원본은 `SELECT` 및 `UPDATE` SQL 명령을 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63a5f-133">The data source must support the `SELECT` and `UPDATE` SQL commands.</span></span> <span data-ttu-id="63a5f-134">목록 요소의 순서가 나중에 변경 되는 경우 `ReorderList` 컨트롤은 데이터 원본의 `Update` 명령에 새 위치와 요소의 ID로 두 값을 자동으로 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="63a5f-134">When the order of the list elements is later changed, the `ReorderList` control automatically submits two values to the data source's `Update` command: the new position and the ID of the element.</span></span> <span data-ttu-id="63a5f-135">따라서 데이터 원본에는 다음 두 값에 대 한 `<UpdateParameters>` 섹션이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="63a5f-135">Therefore, the data source needs an `<UpdateParameters>` section for these two values:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample1.aspx)]

<span data-ttu-id="63a5f-136">`ReorderList` 컨트롤은 다음 특성을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63a5f-136">The `ReorderList` control needs to set the following attributes:</span></span>

- <span data-ttu-id="63a5f-137">`AllowReorder`: 목록 항목을 다시 정렬할 수 있는지 여부</span><span class="sxs-lookup"><span data-stu-id="63a5f-137">`AllowReorder`: Whether the list items may be rearranged</span></span>
- <span data-ttu-id="63a5f-138">`DataSourceID`: 데이터 원본의 ID</span><span class="sxs-lookup"><span data-stu-id="63a5f-138">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="63a5f-139">`DataKeyField`: 데이터 원본에 있는 기본 키 열의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="63a5f-139">`DataKeyField`: The name of the primary key column in the data source</span></span>
- <span data-ttu-id="63a5f-140">`SortOrderField`: 목록 항목에 대 한 정렬 순서를 제공 하는 데이터 원본 열입니다.</span><span class="sxs-lookup"><span data-stu-id="63a5f-140">`SortOrderField`: The data source column that provides the sort order for the list items</span></span>

<span data-ttu-id="63a5f-141">`<DragHandleTemplate>` 및 `<ItemTemplate>` 섹션에서 목록의 레이아웃을 세밀 하 게 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63a5f-141">In the `<DragHandleTemplate>` and `<ItemTemplate>` sections, the layout of the list can be fine-tuned.</span></span> <span data-ttu-id="63a5f-142">또한 다음과 같이 `Eval()` 메서드를 사용 하 여 데이터 바인딩을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63a5f-142">Also, databinding is possible using the `Eval()` method, as seen here:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample2.aspx)]

<span data-ttu-id="63a5f-143">다음 CSS 스타일 정보 (`ReorderList` 컨트롤의 `<DragHandleTemplate>` 섹션에서 참조 됨)는 끌기 핸들을 가리킬 때 마우스 포인터가 적절 하 게 변경 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="63a5f-143">The following CSS style information (referenced in the `<DragHandleTemplate>` section of the `ReorderList` control) makes sure that the mouse pointer changes appropriately when it hovers over the drag handle:</span></span>

[!code-css[Main](drag-and-drop-via-reorderlist-vb/samples/sample3.css)]

<span data-ttu-id="63a5f-144">마지막으로 `ScriptManager` 컨트롤은 페이지에 대 한 ASP.NET AJAX를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="63a5f-144">Finally, a `ScriptManager` control initializes ASP.NET AJAX for the page:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample4.aspx)]

<span data-ttu-id="63a5f-145">브라우저에서이 예제를 실행 하 고 목록 항목을 약간 다시 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="63a5f-145">Run this example in the browser and rearrange the list items a bit.</span></span> <span data-ttu-id="63a5f-146">그런 다음 페이지를 다시 로드 하거나 데이터베이스를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="63a5f-146">Then, reload the page and/or have a look at the database.</span></span> <span data-ttu-id="63a5f-147">변경 된 위치는 유지 관리 되 고 데이터베이스의 `position` 열 값 및 태그를 사용 하 여 코드 없이 모두 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63a5f-147">The altered positions have been maintained and are also reflected by the values in the `position` column in the database and that all without any code, just by using markup.</span></span>

<span data-ttu-id="63a5f-148">[새 목록 항목 순서에 따라 데이터베이스의 데이터 변경 내용 ![](drag-and-drop-via-reorderlist-vb/_static/image8.png)](drag-and-drop-via-reorderlist-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="63a5f-148">[![The data in the database changes according to the new list item order](drag-and-drop-via-reorderlist-vb/_static/image8.png)](drag-and-drop-via-reorderlist-vb/_static/image7.png)</span></span>

<span data-ttu-id="63a5f-149">데이터베이스의 데이터는 새 목록 항목 순서에 따라 변경 됩니다 ([전체 크기 이미지를 보려면 클릭](drag-and-drop-via-reorderlist-vb/_static/image9.png)).</span><span class="sxs-lookup"><span data-stu-id="63a5f-149">The data in the database changes according to the new list item order ([Click to view full-size image](drag-and-drop-via-reorderlist-vb/_static/image9.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="63a5f-150">이전</span><span class="sxs-lookup"><span data-stu-id="63a5f-150">Previous</span></span>](using-postbacks-with-reorderlist-vb.md)
