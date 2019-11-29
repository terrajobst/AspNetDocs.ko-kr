---
uid: web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-vb
title: 아코디언에 데이터 바인딩 (VB) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 아코디언 컨트롤은 여러 창을 제공 하 고 사용자가 한 번에 하나씩 표시할 수 있도록 합니다. 패널은 일반적으로 ...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b19f0875-7d3e-4ecf-baa1-a0c693c765b3
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-vb
msc.type: authoredcontent
ms.openlocfilehash: bfb31940c0395c7ed1d5d471fb8fb686b66c59ad
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599977"
---
# <a name="databinding-to-an-accordion-vb"></a><span data-ttu-id="34461-104">Accordion에 데이터 바인딩(VB)</span><span class="sxs-lookup"><span data-stu-id="34461-104">Databinding to an Accordion (VB)</span></span>

<span data-ttu-id="34461-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="34461-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="34461-106">[코드 다운로드](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="34461-106">[Download Code](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1VB.pdf)</span></span>

> <span data-ttu-id="34461-107">AJAX 컨트롤 도구 키트의 아코디언 컨트롤은 여러 창을 제공 하 고 사용자가 한 번에 하나씩 표시할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="34461-107">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="34461-108">패널은 일반적으로 페이지 자체 내에서 선언 되지만 데이터 원본에 바인딩하면 더 많은 유연성이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34461-108">Panels are usually declared within the page itself, but binding to a data source offers more flexibility.</span></span>

## <a name="overview"></a><span data-ttu-id="34461-109">개요</span><span class="sxs-lookup"><span data-stu-id="34461-109">Overview</span></span>

<span data-ttu-id="34461-110">AJAX 컨트롤 도구 키트의 아코디언 컨트롤은 여러 창을 제공 하 고 사용자가 한 번에 하나씩 표시할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="34461-110">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="34461-111">패널은 일반적으로 페이지 자체 내에서 선언 되지만 데이터 원본에 바인딩하면 더 많은 유연성이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34461-111">Panels are usually declared within the page itself, but binding to a data source offers more flexibility.</span></span>

## <a name="steps"></a><span data-ttu-id="34461-112">단계</span><span class="sxs-lookup"><span data-stu-id="34461-112">Steps</span></span>

<span data-ttu-id="34461-113">먼저 데이터 원본이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="34461-113">First of all, a data source is required.</span></span> <span data-ttu-id="34461-114">이 샘플에서는 AdventureWorks 데이터베이스와 Microsoft SQL Server 2005 Express Edition을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="34461-114">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="34461-115">데이터베이스는 Visual Studio 설치 (express edition 포함)의 선택적 부분이 며 [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)에서 별도의 다운로드로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34461-115">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="34461-116">AdventureWorks 데이터베이스는 SQL Server 2005 샘플 및 예제 데이터베이스 ( [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)에서 다운로드)의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="34461-116">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="34461-117">데이터베이스를 설정 하는 가장 쉬운 방법은 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en))를 사용 하 고 `AdventureWorks.mdf` 데이터베이스 파일을 연결 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="34461-117">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="34461-118">이 샘플에서는 SQL Server 2005 Express Edition 인스턴스가 `SQLEXPRESS` 호출 되 고 웹 서버와 같은 컴퓨터에 있는 것으로 가정 합니다. 이는 기본 설정 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="34461-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="34461-119">설정이 다른 경우 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34461-119">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="34461-120">ASP.NET AJAX 및 Control Toolkit의 기능을 활성화 하려면 페이지의 아무 곳에 나 `<form>` 요소 내에 `ScriptManager` 컨트롤을 배치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34461-120">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample1.aspx)]

<span data-ttu-id="34461-121">그런 다음 페이지에 데이터 원본을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="34461-121">Then, add a data source to the page.</span></span> <span data-ttu-id="34461-122">제한 된 양의 데이터를 사용 하기 위해 AdventureWorks 데이터베이스의 Vendor 테이블에서 처음 5 개 항목만 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="34461-122">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="34461-123">Visual Studio assistant를 사용 하 여 데이터 소스를 만드는 경우 현재 버전의 버그는 테이블 이름 (`Vendor`)에 `Purchasing`접두사로 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="34461-123">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="34461-124">다음 태그는 올바른 구문을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="34461-124">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample2.aspx)]

<span data-ttu-id="34461-125">데이터 원본의 이름 (ID)을 유념 하십시오.</span><span class="sxs-lookup"><span data-stu-id="34461-125">Remember the name (ID) of the data source.</span></span> <span data-ttu-id="34461-126">이 id는 다음과 같이 아코디언 컨트롤의 `DataSourceID` 속성에서 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34461-126">This very identification must then be used in the `DataSourceID` property of the Accordion control:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample3.aspx)]

<span data-ttu-id="34461-127">아코디언 컨트롤 내에서 헤더 (`<HeaderTemplate>`) 및 콘텐츠 (`<ContentTemplate>`)를 포함 하 여 컨트롤의 다양 한 부분에 대 한 템플릿을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34461-127">Within the Accordion control, you can provide templates for various parts of the control, including the header (`<HeaderTemplate>`) and the content (`<ContentTemplate>`).</span></span> <span data-ttu-id="34461-128">이러한 요소 내에서 `DataBinder.Eval()` 메서드를 사용 하 여 데이터 소스에서 데이터를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="34461-128">Within these elements, just output the data from the data source, using the `DataBinder.Eval()` method:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample4.aspx)]

<span data-ttu-id="34461-129">페이지가 로드 되 면 데이터 원본은이 서버 쪽 코드를 사용 하 여 아코디언에 바인딩되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34461-129">When the page is loaded, the data source must be bound to the accordion with this server-side code:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample5.aspx)]

<span data-ttu-id="34461-130">이 샘플을 종료 하려면 아코디언 컨트롤에서 참조 되는 두 개의 CSS 클래스 (속성 `HeaderCssClass` 및 `ContentCssClass`)를 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34461-130">To conclude this sample, you need to define the two CSS classes that are referenced in the Accordion control (in its properties `HeaderCssClass` and `ContentCssClass`).</span></span> <span data-ttu-id="34461-131">페이지의 `<head>` 섹션에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="34461-131">Put the following markup in the `<head>` section of the page:</span></span>

[!code-css[Main](databinding-to-an-accordion-vb/samples/sample6.css)]

<span data-ttu-id="34461-132">[아코디언의 데이터가 데이터 원본에서 직접 제공 ![](databinding-to-an-accordion-vb/_static/image2.png)](databinding-to-an-accordion-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="34461-132">[![The data in the accordion comes directly from the data source](databinding-to-an-accordion-vb/_static/image2.png)](databinding-to-an-accordion-vb/_static/image1.png)</span></span>

<span data-ttu-id="34461-133">아코디언의 데이터는 데이터 원본에서 직접 제공 됩니다 ([전체 크기 이미지를 보려면 클릭](databinding-to-an-accordion-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="34461-133">The data in the accordion comes directly from the data source ([Click to view full-size image](databinding-to-an-accordion-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="34461-134">[이전](dynamically-adding-an-accordion-pane-cs.md)
> [다음](dynamically-adding-an-accordion-pane-vb.md)</span><span class="sxs-lookup"><span data-stu-id="34461-134">[Previous](dynamically-adding-an-accordion-pane-cs.md)
[Next](dynamically-adding-an-accordion-pane-vb.md)</span></span>
