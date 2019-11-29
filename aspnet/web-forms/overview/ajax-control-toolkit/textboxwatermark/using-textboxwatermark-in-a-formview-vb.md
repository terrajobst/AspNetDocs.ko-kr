---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-vb
title: FormView에서 TextBoxWatermark 사용 (VB) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 TextBoxWatermark 컨트롤은 입력란 내에 텍스트가 표시 되도록 텍스트 상자를 확장 합니다. 사용자가 상자를 클릭 하면 ...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 41497361-7fba-4825-b36c-f58d79522a88
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-vb
msc.type: authoredcontent
ms.openlocfilehash: 1dd17ed57383680122c4ca613ca71f6682dec40e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598341"
---
# <a name="using-textboxwatermark-in-a-formview-vb"></a><span data-ttu-id="aab67-104">FormView에서 TextBoxWatermark 사용(VB)</span><span class="sxs-lookup"><span data-stu-id="aab67-104">Using TextBoxWatermark in a FormView (VB)</span></span>

<span data-ttu-id="aab67-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="aab67-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="aab67-106">[코드 다운로드](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark1.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="aab67-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark1VB.pdf)</span></span>

> <span data-ttu-id="aab67-107">AJAX 컨트롤 도구 키트의 TextBoxWatermark 컨트롤은 입력란 내에 텍스트가 표시 되도록 텍스트 상자를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="aab67-107">The TextBoxWatermark control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="aab67-108">사용자가 상자를 클릭 하면 해당 상자가 비워집니다.</span><span class="sxs-lookup"><span data-stu-id="aab67-108">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="aab67-109">사용자가 텍스트를 입력 하지 않고 상자를 벗어나면 미리 채워진 텍스트가 다시 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="aab67-109">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="aab67-110">이는 FormView 컨트롤 내 에서도 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="aab67-110">This is also possible within a FormView control.</span></span>

## <a name="overview"></a><span data-ttu-id="aab67-111">개요</span><span class="sxs-lookup"><span data-stu-id="aab67-111">Overview</span></span>

<span data-ttu-id="aab67-112">AJAX 컨트롤 도구 키트의 `TextBoxWatermark` 컨트롤은 입력란 내에 텍스트가 표시 되도록 텍스트 상자를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="aab67-112">The `TextBoxWatermark` control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="aab67-113">사용자가 상자를 클릭 하면 해당 상자가 비워집니다.</span><span class="sxs-lookup"><span data-stu-id="aab67-113">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="aab67-114">사용자가 텍스트를 입력 하지 않고 상자를 벗어나면 미리 채워진 텍스트가 다시 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="aab67-114">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="aab67-115">이는 `FormView` 컨트롤 내 에서도 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="aab67-115">This is also possible within a `FormView` control.</span></span>

## <a name="steps"></a><span data-ttu-id="aab67-116">단계</span><span class="sxs-lookup"><span data-stu-id="aab67-116">Steps</span></span>

<span data-ttu-id="aab67-117">먼저 데이터 원본이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="aab67-117">First of all, a data source is required.</span></span> <span data-ttu-id="aab67-118">이 샘플에서는 AdventureWorks 데이터베이스와 Microsoft SQL Server 2005 Express Edition을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aab67-118">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="aab67-119">데이터베이스는 Visual Studio 설치 (express edition 포함)의 선택적 부분이 며 [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)에서 별도의 다운로드로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aab67-119">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="aab67-120">AdventureWorks 데이터베이스는 SQL Server 2005 샘플 및 예제 데이터베이스 ( [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)에서 다운로드)의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="aab67-120">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="aab67-121">데이터베이스를 설정 하는 가장 쉬운 방법은 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en))를 사용 하 고 `AdventureWorks.mdf` 데이터베이스 파일을 연결 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="aab67-121">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="aab67-122">이 샘플에서는 SQL Server 2005 Express Edition 인스턴스가 `SQLEXPRESS` 호출 되 고 웹 서버와 같은 컴퓨터에 있는 것으로 가정 합니다. 이는 기본 설정 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="aab67-122">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="aab67-123">설정이 다른 경우 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aab67-123">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="aab67-124">ASP.NET AJAX 및 Control Toolkit의 기능을 활성화 하려면 페이지의 아무 곳에 나 `<form>` 요소 내에 `ScriptManager` 컨트롤을 배치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aab67-124">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample1.aspx)]

<span data-ttu-id="aab67-125">그런 다음 `DELETE`, `INSERT` 및 `UPDATE` SQL 문을 지 원하는 페이지에 데이터 원본을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="aab67-125">Then, add a data source to the page which supports the `DELETE`, `INSERT` and `UPDATE` SQL statements.</span></span> <span data-ttu-id="aab67-126">Visual Studio assistant를 사용 하 여 데이터 소스를 만드는 경우 현재 버전의 버그는 테이블 이름 (`Vendor`)에 `Purchasing`접두사로 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aab67-126">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="aab67-127">다음 태그는 올바른 구문을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aab67-127">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample2.aspx)]

<span data-ttu-id="aab67-128">`FormView` 컨트롤의 `DataSourceID` 속성에 사용 되므로 데이터 원본의 이름 (`ID`)을 명심 하십시오.</span><span class="sxs-lookup"><span data-stu-id="aab67-128">Remember the name (`ID`) of the data source, since it will be used in the `DataSourceID` property of the `FormView` control.</span></span> <span data-ttu-id="aab67-129">`FormView`의 `<InsertItemTemplate>` 섹션에는 `TextBoxWatermarkExtender` 컨트롤에 의해 확장 되는 텍스트 상자가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aab67-129">The `<InsertItemTemplate>` section of the `FormView` contains a textbox which is extended by the `TextBoxWatermarkExtender` control.</span></span> <span data-ttu-id="aab67-130">Extender가 외부가 아닌 템플릿 내에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="aab67-130">Make sure that the extender resides within the template and not outside of it.</span></span>

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample3.aspx)]

<span data-ttu-id="aab67-131">이제 사용자가 `FormView` 컨트롤의 삽입 모드로 변경 되 면 새 공급 업체에 대 한 텍스트 필드가 `TextBoxWatermarkExtender` 컨트롤로 미리 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="aab67-131">Now when the user changes into the insert mode of the `FormView` control, the text field for the new vendor is prefilled thanks to the `TextBoxWatermarkExtender` control.</span></span> <span data-ttu-id="aab67-132">텍스트 상자 내부를 클릭 하면 필러 텍스트가 사라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aab67-132">A click inside the textbox lets the filler text disappear.</span></span>

<span data-ttu-id="aab67-133">[extender에서 가져온 필드의 워터 마크 ![](using-textboxwatermark-in-a-formview-vb/_static/image2.png)](using-textboxwatermark-in-a-formview-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="aab67-133">[![The watermark in the field comes from the extender](using-textboxwatermark-in-a-formview-vb/_static/image2.png)](using-textboxwatermark-in-a-formview-vb/_static/image1.png)</span></span>

<span data-ttu-id="aab67-134">필드의 워터 마크는 extender에서 가져옵니다 ([전체 크기 이미지를 보려면 클릭](using-textboxwatermark-in-a-formview-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="aab67-134">The watermark in the field comes from the extender ([Click to view full-size image](using-textboxwatermark-in-a-formview-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="aab67-135">[이전](using-textboxwatermark-with-validation-controls-cs.md)
> [다음](using-textboxwatermark-with-validation-controls-vb.md)</span><span class="sxs-lookup"><span data-stu-id="aab67-135">[Previous](using-textboxwatermark-with-validation-controls-cs.md)
[Next](using-textboxwatermark-with-validation-controls-vb.md)</span></span>
