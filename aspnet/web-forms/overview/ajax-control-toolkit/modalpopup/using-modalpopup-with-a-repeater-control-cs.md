---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-cs
title: Repeater 컨트롤에서 ModalPopup 사용 (C#) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 ModalPopup 컨트롤은 클라이언트 쪽을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 이 항목을 사용 하는 것도 가능 합니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: d686d84a-1c58-492e-8a77-3eb5a0cfe918
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 980f023c9e8256ad5323aaa6cbb6918b04e18974
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598929"
---
# <a name="using-modalpopup-with-a-repeater-control-c"></a><span data-ttu-id="03dac-104">반복기 컨트롤에 ModalPopup사용(C#)</span><span class="sxs-lookup"><span data-stu-id="03dac-104">Using ModalPopup with a Repeater Control (C#)</span></span>

<span data-ttu-id="03dac-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="03dac-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="03dac-106">[코드 다운로드](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup2.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="03dac-106">[Download Code](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup2.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup2CS.pdf)</span></span>

> <span data-ttu-id="03dac-107">AJAX 컨트롤 도구 키트의 ModalPopup 컨트롤은 클라이언트 쪽을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="03dac-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="03dac-108">Repeater 내에서이 컨트롤을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03dac-108">It is also possible to use this control within a repeater.</span></span>

## <a name="overview"></a><span data-ttu-id="03dac-109">개요</span><span class="sxs-lookup"><span data-stu-id="03dac-109">Overview</span></span>

<span data-ttu-id="03dac-110">AJAX 컨트롤 도구 키트의 ModalPopup 컨트롤은 클라이언트 쪽을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="03dac-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="03dac-111">Repeater 내에서이 컨트롤을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03dac-111">It is also possible to use this control within a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="03dac-112">단계</span><span class="sxs-lookup"><span data-stu-id="03dac-112">Steps</span></span>

<span data-ttu-id="03dac-113">먼저 데이터 원본이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="03dac-113">First of all, a data source is required.</span></span> <span data-ttu-id="03dac-114">이 샘플에서는 AdventureWorks 데이터베이스와 Microsoft SQL Server 2005 Express Edition을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="03dac-114">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="03dac-115">데이터베이스는 Visual Studio 설치 (express edition 포함)의 선택적 부분이 며 [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)에서 별도의 다운로드로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03dac-115">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="03dac-116">AdventureWorks 데이터베이스는 SQL Server 2005 샘플 및 예제 데이터베이스 ( [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)에서 다운로드)의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="03dac-116">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="03dac-117">데이터베이스를 설정 하는 가장 쉬운 방법은 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en))를 사용 하 고 `AdventureWorks.mdf` 데이터베이스 파일을 연결 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="03dac-117">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span> <span data-ttu-id="03dac-118">이 샘플에서는 SQL Server 2005 Express Edition 인스턴스가 `SQLEXPRESS` 호출 되 고 웹 서버와 같은 컴퓨터에 있는 것으로 가정 합니다. 이는 기본 설정 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="03dac-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="03dac-119">설정이 다른 경우 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03dac-119">If your setup differs, you have to adapt the connection information for the database.</span></span> <span data-ttu-id="03dac-120">ASP.NET AJAX 및 Control Toolkit의 기능을 활성화 하려면 페이지의 아무 곳에 나 `<form>` 요소 내에 `ScriptManager` 컨트롤을 배치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03dac-120">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample1.aspx)]

<span data-ttu-id="03dac-121">그런 다음 페이지에 데이터 원본을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="03dac-121">Then, add a data source to the page.</span></span> <span data-ttu-id="03dac-122">제한 된 양의 데이터를 사용 하기 위해 AdventureWorks 데이터베이스의 Vendor 테이블에서 처음 5 개 항목만 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="03dac-122">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="03dac-123">Visual Studio assistant를 사용 하 여 데이터 소스를 만드는 경우 현재 버전의 버그는 테이블 이름 (`Vendor`)에 `Purchasing`접두사로 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="03dac-123">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="03dac-124">다음 태그는 올바른 구문을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="03dac-124">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample2.aspx)]

<span data-ttu-id="03dac-125">다음으로, 모달 popup으로 사용 되는 패널을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="03dac-125">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="03dac-126">팝업을 다시 닫기 위한 `Button` 컨트롤이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03dac-126">It contains a `Button` control to close the popup again:</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample3.aspx)]

<span data-ttu-id="03dac-127">Repeater 내에서 popup 작업을 수행 하려면 `ModalPopupExtender` 컨트롤을 repeater의 `<ItemTemplate>` 섹션에 배치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03dac-127">In order to make the popup work within the repeater, the `ModalPopupExtender` control must be put within the `<ItemTemplate>` section of the repeater.</span></span> <span data-ttu-id="03dac-128">패널이 repeater 외부에 있지만 extender는 안에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03dac-128">So the panel is outside the repeater, but the extender is inside.</span></span> <span data-ttu-id="03dac-129">다음은 repeater의 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="03dac-129">Here is the markup for the repeater:</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample4.aspx)]

<span data-ttu-id="03dac-130">그런 다음 데이터 원본의 모든 항목은 모달 팝업을 트리거하는 옆에 단추가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03dac-130">Then, every item in the data source is displayed with a button next to it that triggers the modal popup.</span></span>

<span data-ttu-id="03dac-131">[![모든 데이터 원본 항목에 대해 모달 팝업을 트리거할 수 있습니다.](using-modalpopup-with-a-repeater-control-cs/_static/image2.png)](using-modalpopup-with-a-repeater-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="03dac-131">[![The modal popup can be triggered for every data source entry](using-modalpopup-with-a-repeater-control-cs/_static/image2.png)](using-modalpopup-with-a-repeater-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="03dac-132">모든 데이터 원본 항목에 대해 모달 팝업을 트리거할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](using-modalpopup-with-a-repeater-control-cs/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="03dac-132">The modal popup can be triggered for every data source entry ([Click to view full-size image](using-modalpopup-with-a-repeater-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="03dac-133">[이전](launching-a-modal-popup-window-from-server-code-cs.md)
> [다음](handling-postbacks-from-a-modalpopup-cs.md)</span><span class="sxs-lookup"><span data-stu-id="03dac-133">[Previous](launching-a-modal-popup-window-from-server-code-cs.md)
[Next](handling-postbacks-from-a-modalpopup-cs.md)</span></span>
