---
uid: web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-vb
title: Repeater에서 단일 단추 사용 (VB) | Microsoft Docs
author: wenz
description: 사용자가 단추 (LinkButton 컨트롤 포함)를 클릭 하면 AJAX 컨트롤 Toolkit의 [사용자] 단추 extender가 예/아니요 팝업을 만듭니다. 예 인 경우에만 ...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 18c31709-3f9d-4d93-8b01-f1356bf610b4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-vb
msc.type: authoredcontent
ms.openlocfilehash: 001233d866d8a731d93d6900f714cd2060f3d08c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497543"
---
# <a name="using-a-confirmbutton-in-a-repeater-vb"></a><span data-ttu-id="05f5b-104">Repeater에 ConfirmButton 사용(VB)</span><span class="sxs-lookup"><span data-stu-id="05f5b-104">Using a ConfirmButton In a Repeater (VB)</span></span>

<span data-ttu-id="05f5b-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="05f5b-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="05f5b-106">[코드 다운로드](https://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="05f5b-106">[Download Code](https://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1VB.pdf)</span></span>

> <span data-ttu-id="05f5b-107">사용자가 단추 (LinkButton 컨트롤 포함)를 클릭 하면 AJAX 컨트롤 Toolkit의 [사용자] 단추 extender가 예/아니요 팝업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05f5b-107">The ConfirmButton extender in the AJAX Control Toolkit creates a Yes/No popup when the user clicks on a button (including LinkButton control).</span></span> <span data-ttu-id="05f5b-108">예를 클릭 한 경우에만 단추의 동작이 실행 되 고, 그렇지 않으면 취소 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05f5b-108">Only if Yes is clicked, the button's action is executed, otherwise cancelled.</span></span> <span data-ttu-id="05f5b-109">이는 리피터 에서도 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="05f5b-109">This is also possible in a repeater.</span></span>

## <a name="overview"></a><span data-ttu-id="05f5b-110">개요</span><span class="sxs-lookup"><span data-stu-id="05f5b-110">Overview</span></span>

<span data-ttu-id="05f5b-111">사용자가 단추 (LinkButton 컨트롤 포함)를 클릭 하면 AJAX 컨트롤 Toolkit의 [사용자] 단추 extender가 예/아니요 팝업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05f5b-111">The ConfirmButton extender in the AJAX Control Toolkit creates a Yes/No popup when the user clicks on a button (including LinkButton control).</span></span> <span data-ttu-id="05f5b-112">예를 클릭 한 경우에만 단추의 동작이 실행 되 고, 그렇지 않으면 취소 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05f5b-112">Only if Yes is clicked, the button's action is executed, otherwise cancelled.</span></span> <span data-ttu-id="05f5b-113">이는 리피터 에서도 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="05f5b-113">This is also possible in a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="05f5b-114">단계</span><span class="sxs-lookup"><span data-stu-id="05f5b-114">Steps</span></span>

<span data-ttu-id="05f5b-115">먼저 데이터 원본이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="05f5b-115">First of all, a data source is required.</span></span> <span data-ttu-id="05f5b-116">이 샘플에서는 AdventureWorks 데이터베이스와 Microsoft SQL Server 2005 Express Edition을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="05f5b-116">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="05f5b-117">데이터베이스는 Visual Studio 설치 (express edition 포함)의 선택적 부분이 며 [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)에서 별도의 다운로드로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05f5b-117">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="05f5b-118">AdventureWorks 데이터베이스는 SQL Server 2005 샘플 및 예제 데이터베이스 ( [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)에서 다운로드)의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="05f5b-118">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="05f5b-119">데이터베이스를 설정 하는 가장 쉬운 방법은 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en))를 사용 하 고 `AdventureWorks.mdf` 데이터베이스 파일을 연결 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="05f5b-119">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="05f5b-120">이 샘플에서는 SQL Server 2005 Express Edition 인스턴스가 `SQLEXPRESS` 호출 되 고 웹 서버와 같은 컴퓨터에 있는 것으로 가정 합니다. 이는 기본 설정 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="05f5b-120">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="05f5b-121">설정이 다른 경우 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05f5b-121">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="05f5b-122">ASP.NET AJAX 및 Control Toolkit의 기능을 활성화 하려면 페이지의 아무 곳에 나 `<form>` 요소 내에 `ScriptManager` 컨트롤을 배치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05f5b-122">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample1.aspx)]

<span data-ttu-id="05f5b-123">그런 다음 데이터 원본이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="05f5b-123">Then, a data source is required.</span></span> <span data-ttu-id="05f5b-124">편의상 AdventureWorks 공급 업체 테이블의 처음 5 개 항목만 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05f5b-124">For the sake of simplicity, only the first five entries in AdventureWorks' Vendors table are retrieved.</span></span> <span data-ttu-id="05f5b-125">Visual Studio 마법사를 사용 하 여 데이터 소스를 만들 때 현재 테이블 이름 (`Vendors`)에는 `Purchasing`접두사가 올바르게 붙지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05f5b-125">Note that when using the Visual Studio wizard to create the data source, the table name (`Vendors`) is currently not correctly prefixed with `Purchasing`.</span></span> <span data-ttu-id="05f5b-126">올바른 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="05f5b-126">The following markup is the correct one:</span></span>

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample2.aspx)]

<span data-ttu-id="05f5b-127">그러면이 데이터 원본을 repeater 내에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05f5b-127">This data source can then be used within a repeater.</span></span> <span data-ttu-id="05f5b-128">일반적으로 `DataBinder.Eval()` 메서드는 데이터 소스에서 데이터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="05f5b-128">As usual, the `DataBinder.Eval()` method retrieves data from the data source.</span></span> <span data-ttu-id="05f5b-129">그런 다음 데이터 원본의 모든 항목에 대해 표시 되도록 `ConfirmButtonExtender` 컨트롤을 repeater의 `<ItemTemplate>` 섹션에 배치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05f5b-129">The `ConfirmButtonExtender` control must then be placed within the `<ItemTemplate>` section of the repeater so that it appears for every entry in the data source.</span></span>

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample3.aspx)]

<span data-ttu-id="05f5b-130">[데이터 원본의 각 항목 옆에 확인 단추가 표시 ![](using-a-confirmbutton-in-a-repeater-vb/_static/image2.png)](using-a-confirmbutton-in-a-repeater-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="05f5b-130">[![The confirm button appears next to each entry from the data source](using-a-confirmbutton-in-a-repeater-vb/_static/image2.png)](using-a-confirmbutton-in-a-repeater-vb/_static/image1.png)</span></span>

<span data-ttu-id="05f5b-131">확인 단추는 데이터 원본의 각 항목 옆에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](using-a-confirmbutton-in-a-repeater-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="05f5b-131">The confirm button appears next to each entry from the data source ([Click to view full-size image](using-a-confirmbutton-in-a-repeater-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="05f5b-132">이전</span><span class="sxs-lookup"><span data-stu-id="05f5b-132">Previous</span></span>](using-a-confirmbutton-in-a-repeater-cs.md)
