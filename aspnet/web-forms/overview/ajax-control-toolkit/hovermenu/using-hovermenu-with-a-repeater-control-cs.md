---
uid: web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
title: Repeater 컨트롤에서에 hovermenu 사용 (C#) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의에 hovermenu 컨트롤은 간단한 팝업 효과를 제공 합니다. 마우스 포인터를 요소 위로 가져가면 specifi에 팝업이 표시 됩니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e7700e7b-edc3-4183-a713-70e507cc7490
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 3e38b91d837c65191d4b3797fa31ef6112a1f070
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606707"
---
# <a name="using-hovermenu-with-a-repeater-control-c"></a><span data-ttu-id="6e9c4-103">반복기 컨트롤에 HoverMenu 사용(C#)</span><span class="sxs-lookup"><span data-stu-id="6e9c4-103">Using HoverMenu with a Repeater Control (C#)</span></span>

<span data-ttu-id="6e9c4-104">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="6e9c4-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="6e9c4-105">[코드 다운로드](https://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="6e9c4-105">[Download Code](https://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)</span></span>

> <span data-ttu-id="6e9c4-106">AJAX 컨트롤 도구 키트의에 hovermenu 컨트롤은 간단한 팝업 효과를 제공 합니다. 마우스 포인터를 요소 위로 가져가면 지정 된 위치에 팝업이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6e9c4-106">The HoverMenu control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="6e9c4-107">Repeater 내에서이 컨트롤을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e9c4-107">It is also possible to use this control within a repeater.</span></span>

## <a name="overview"></a><span data-ttu-id="6e9c4-108">개요</span><span class="sxs-lookup"><span data-stu-id="6e9c4-108">Overview</span></span>

<span data-ttu-id="6e9c4-109">AJAX 컨트롤 도구 키트의 `HoverMenu` 컨트롤은 간단한 팝업 효과를 제공 합니다. 마우스 포인터를 요소 위로 가져가면 지정 된 위치에 팝업이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6e9c4-109">The `HoverMenu` control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="6e9c4-110">Repeater 내에서이 컨트롤을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e9c4-110">It is also possible to use this control within a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="6e9c4-111">단계</span><span class="sxs-lookup"><span data-stu-id="6e9c4-111">Steps</span></span>

<span data-ttu-id="6e9c4-112">먼저 데이터 원본이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9c4-112">First of all, a data source is required.</span></span> <span data-ttu-id="6e9c4-113">이 샘플에서는 AdventureWorks 데이터베이스와 Microsoft SQL Server 2005 Express Edition을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9c4-113">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="6e9c4-114">데이터베이스는 Visual Studio 설치 (express edition 포함)의 선택적 부분이 며 [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)에서 별도의 다운로드로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e9c4-114">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="6e9c4-115">AdventureWorks 데이터베이스는 SQL Server 2005 샘플 및 예제 데이터베이스 ( [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)에서 다운로드)의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="6e9c4-115">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="6e9c4-116">데이터베이스를 설정 하는 가장 쉬운 방법은 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en))를 사용 하 고 `AdventureWorks.mdf` 데이터베이스 파일을 연결 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6e9c4-116">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="6e9c4-117">이 샘플에서는 SQL Server 2005 Express Edition 인스턴스가 `SQLEXPRESS` 호출 되 고 웹 서버와 같은 컴퓨터에 있는 것으로 가정 합니다. 이는 기본 설정 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9c4-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="6e9c4-118">설정이 다른 경우 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9c4-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="6e9c4-119">ASP.NET AJAX 및 Control Toolkit의 기능을 활성화 하려면 페이지의 아무 곳에 나 `<form>` 요소 내에 `ScriptManager` 컨트롤을 배치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9c4-119">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample1.aspx)]

<span data-ttu-id="6e9c4-120">그런 다음 페이지에 데이터 원본을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9c4-120">Then, add a data source to the page.</span></span> <span data-ttu-id="6e9c4-121">제한 된 양의 데이터를 사용 하기 위해 AdventureWorks 데이터베이스의 Vendor 테이블에서 처음 5 개 항목만 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9c4-121">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="6e9c4-122">Visual Studio assistant를 사용 하 여 데이터 소스를 만드는 경우 현재 버전의 버그는 테이블 이름 (`Vendor`)에 `Purchasing`접두사로 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6e9c4-122">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="6e9c4-123">다음 태그는 올바른 구문을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6e9c4-123">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample2.aspx)]

<span data-ttu-id="6e9c4-124">다음으로, 모달 popup으로 사용 되는 패널을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9c4-124">Next, add a panel which serves as the modal popup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample3.aspx)]

<span data-ttu-id="6e9c4-125">이제 `HoverMenuExtender`이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e9c4-125">Now, the `HoverMenuExtender` comes into play.</span></span> <span data-ttu-id="6e9c4-126">데이터 소스에 있는 모든 요소가 자체 팝업을 가져오기 위해 extender의 `<ItemTemplate>` 섹션 안에 extender를 넣어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e9c4-126">So that every element in the data source gets its own popup, the extender must be put within the repeater's `<ItemTemplate>` section.</span></span> <span data-ttu-id="6e9c4-127">다음은 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="6e9c4-127">Here is the markup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample4.aspx)]

<span data-ttu-id="6e9c4-128">이제 데이터 원본의 모든 항목에는 50 밀리초 (`PopDelay` 특성) 지연 후 오른쪽 (`PopupPosition` 특성)에 대 한 팝업이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e9c4-128">Now every item in the data source displays a popup to the right (`PopupPosition` attribute) after a delay of 50 milliseconds (`PopDelay` attribute).</span></span>

<span data-ttu-id="6e9c4-129">[가리키기 메뉴 ![repeater의 각 항목 옆에 표시 됩니다.](using-hovermenu-with-a-repeater-control-cs/_static/image2.png)](using-hovermenu-with-a-repeater-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6e9c4-129">[![The hover menu appears next to each item in the repeater](using-hovermenu-with-a-repeater-control-cs/_static/image2.png)](using-hovermenu-with-a-repeater-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="6e9c4-130">가리키기 메뉴가 repeater의 각 항목 옆에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](using-hovermenu-with-a-repeater-control-cs/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="6e9c4-130">The hover menu appears next to each item in the repeater ([Click to view full-size image](using-hovermenu-with-a-repeater-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="6e9c4-131">다음</span><span class="sxs-lookup"><span data-stu-id="6e9c4-131">Next</span></span>](using-hovermenu-with-a-repeater-control-vb.md)
