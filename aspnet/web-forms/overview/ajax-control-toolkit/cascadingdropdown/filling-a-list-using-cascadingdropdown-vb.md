---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
title: CascadingDropDown를 사용 하 여 목록 채우기 (VB) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 CascadingDropDown 컨트롤은 dropdownlist 컨트롤을 확장 하 여 한 DropDownList의 변경 내용이 anoth에 연결 된 값을 로드 하도록 합니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 5236695e-5c70-4887-baee-0bfb0afb3448
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 8dd9ef8a4bdf705ba4451b7fd240e4de8618221c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430733"
---
# <a name="filling-a-list-using-cascadingdropdown-vb"></a><span data-ttu-id="a04b7-103">CascadingDropDown을 사용하여 목록 채우기(VB)</span><span class="sxs-lookup"><span data-stu-id="a04b7-103">Filling a List Using CascadingDropDown (VB)</span></span>

<span data-ttu-id="a04b7-104">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="a04b7-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a04b7-105">[코드 다운로드](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="a04b7-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)</span></span>

> <span data-ttu-id="a04b7-106">AJAX 컨트롤 도구 키트의 CascadingDropDown 컨트롤은 dropdownlist 컨트롤을 확장 하 여 한 DropDownList의 변경 내용이 다른 DropDownList의 관련 값을 로드 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a04b7-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="a04b7-107">예를 들어, 한 목록에는 미국 주 목록이 제공 되며 다음 목록에는 해당 상태의 주 도시가 채워집니다. 가장 먼저 해결 해야 하는 문제는이 컨트롤을 사용 하 여 드롭다운 목록을 실제로 채우는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a04b7-107">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="overview"></a><span data-ttu-id="a04b7-108">개요</span><span class="sxs-lookup"><span data-stu-id="a04b7-108">Overview</span></span>

<span data-ttu-id="a04b7-109">AJAX 컨트롤 도구 키트의 CascadingDropDown 컨트롤은 dropdownlist 컨트롤을 확장 하 여 한 DropDownList의 변경 내용이 다른 DropDownList의 관련 값을 로드 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a04b7-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="a04b7-110">예를 들어, 한 목록에는 미국 주 목록이 제공 되며 다음 목록에는 해당 상태의 주 도시가 채워집니다. 가장 먼저 해결 해야 하는 문제는이 컨트롤을 사용 하 여 드롭다운 목록을 실제로 채우는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a04b7-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="steps"></a><span data-ttu-id="a04b7-111">단계</span><span class="sxs-lookup"><span data-stu-id="a04b7-111">Steps</span></span>

<span data-ttu-id="a04b7-112">ASP.NET AJAX 및 Control Toolkit의 기능을 활성화 하려면 페이지의 아무 곳에 나 `<form>` 요소 내에 `ScriptManager` 컨트롤을 배치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a04b7-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample1.aspx)]

<span data-ttu-id="a04b7-113">그런 다음, DropDownList 컨트롤이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a04b7-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample2.aspx)]

<span data-ttu-id="a04b7-114">이 목록에는 CascadingDropDown extender가 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a04b7-114">For this list, a CascadingDropDown extender is added.</span></span> <span data-ttu-id="a04b7-115">웹 서비스에 대 한 비동기 요청을 보냅니다. 그러면 목록에 표시 될 항목의 목록이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a04b7-115">It will send an asynchronous request to a web service which will then return a list of entries to be displayed in the list.</span></span> <span data-ttu-id="a04b7-116">이 작업을 수행 하려면 다음 CascadingDropDown 특성을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a04b7-116">For this to work, the following CascadingDropDown attributes need to be set:</span></span>

- <span data-ttu-id="a04b7-117">`ServicePath`: 목록 항목을 제공 하는 웹 서비스의 URL</span><span class="sxs-lookup"><span data-stu-id="a04b7-117">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="a04b7-118">`ServiceMethod`: 목록 항목을 전달 하는 웹 메서드</span><span class="sxs-lookup"><span data-stu-id="a04b7-118">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="a04b7-119">`TargetControlID`: 드롭다운 목록의 ID</span><span class="sxs-lookup"><span data-stu-id="a04b7-119">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="a04b7-120">`Category`: 호출 시 웹 메서드에 제출 되는 범주 정보</span><span class="sxs-lookup"><span data-stu-id="a04b7-120">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="a04b7-121">`PromptText`: 서버에서 목록 데이터를 비동기적으로 로드할 때 표시 되는 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="a04b7-121">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>

<span data-ttu-id="a04b7-122">`CascadingDropDown` 요소에 대 한 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a04b7-122">Here is the markup for the `CascadingDropDown` element.</span></span> <span data-ttu-id="a04b7-123">C# 와 VB의 유일한 차이점은 연결 된 웹 서비스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a04b7-123">The only difference between C# and VB is the name of the associated web service:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample3.aspx)]

<span data-ttu-id="a04b7-124">`CascadingDropDown` extender에서 들어오는 JavaScript 코드는 다음 서명을 사용 하 여 웹 서비스 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="a04b7-124">The JavaScript code coming from the `CascadingDropDown` extender calls a web service method with the following signature:</span></span>

[!code-vb[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample4.vb)]

<span data-ttu-id="a04b7-125">따라서 중요 한 점은 메서드가 `CascadingDropDownNameValue` 형식의 배열을 반환 해야 한다는 것입니다 (ASP.NET AJAX 컨트롤 Toolkit에 정의 됨).</span><span class="sxs-lookup"><span data-stu-id="a04b7-125">So the important aspect is that the method needs to return an array of type `CascadingDropDownNameValue` (defined by the ASP.NET AJAX Control Toolkit).</span></span> <span data-ttu-id="a04b7-126">`CascadingDropDownNameValue` 생성자에서 목록 항목의 텍스트를 먼저 입력 한 다음 HTML로 `<option value="VALUE">NAME</option>` 하는 것과 마찬가지로 해당 값을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a04b7-126">In the `CascadingDropDownNameValue` constructor, first the list entry's text and then its value must be provided, just as `<option value="VALUE">NAME</option>` would do in HTML.</span></span> <span data-ttu-id="a04b7-127">다음은 몇 가지 샘플 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="a04b7-127">Here is some sample data:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample5.aspx)]

<span data-ttu-id="a04b7-128">브라우저에서 페이지를 로드 하면 3 개의 공급 업체가 채워질 목록이 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="a04b7-128">Loading the page in the browser will trigger the list to be filled with three vendors.</span></span>

<span data-ttu-id="a04b7-129">[목록이 자동으로 채워질 ![](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a04b7-129">[![The list is filled automatically](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)</span></span>

<span data-ttu-id="a04b7-130">목록이 자동으로 채워집니다 ([전체 크기 이미지를 보려면 클릭](filling-a-list-using-cascadingdropdown-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="a04b7-130">The list is filled automatically ([Click to view full-size image](filling-a-list-using-cascadingdropdown-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a04b7-131">[이전](using-auto-postback-with-cascadingdropdown-cs.md)
> [다음](using-cascadingdropdown-with-a-database-vb.md)</span><span class="sxs-lookup"><span data-stu-id="a04b7-131">[Previous](using-auto-postback-with-cascadingdropdown-cs.md)
[Next](using-cascadingdropdown-with-a-database-vb.md)</span></span>
