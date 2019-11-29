---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-cs
title: CascadingDropDown (C#)에서 자동 포스트백 사용 Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 CascadingDropDown 컨트롤은 dropdownlist 컨트롤을 확장 하 여 한 DropDownList의 변경 내용이 anoth에 연결 된 값을 로드 하도록 합니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6755d8d9-14be-4a1d-86e5-1a6110f3dea8
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: 8bccd716814e7de544798010cecbc148ec50b5cd
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74574519"
---
# <a name="using-auto-postback-with-cascadingdropdown-c"></a><span data-ttu-id="e03da-103">CascadingDropDown으로 자동 포스트백 사용(C#)</span><span class="sxs-lookup"><span data-stu-id="e03da-103">Using Auto-Postback with CascadingDropDown (C#)</span></span>

<span data-ttu-id="e03da-104">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="e03da-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="e03da-105">[코드 다운로드](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="e03da-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3CS.pdf)</span></span>

> <span data-ttu-id="e03da-106">AJAX 컨트롤 도구 키트의 CascadingDropDown 컨트롤은 dropdownlist 컨트롤을 확장 하 여 한 DropDownList의 변경 내용이 다른 DropDownList의 관련 값을 로드 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03da-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="e03da-107">그러나 CascadingDropDown 컨트롤을 사용 하는 경우 ASP. 데이터를 목록에 비동기적으로 로드 하면 (불필요 한) 포스트백이 생성 되므로 NET의 DropDownList 컨트롤의 AutoPostBack 기능이 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e03da-107">However when using the CascadingDropDown control, ASP.NET's DropDownList control's AutoPostBack feature does not work, since asynchronously loading data into the list generates an (unnecessary) postback itself.</span></span> <span data-ttu-id="e03da-108">일부 JavaScript 코드를 사용 하면이 효과를 피할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e03da-108">With some JavaScript code, this effect can be avoided.</span></span>

## <a name="overview"></a><span data-ttu-id="e03da-109">개요</span><span class="sxs-lookup"><span data-stu-id="e03da-109">Overview</span></span>

<span data-ttu-id="e03da-110">AJAX 컨트롤 도구 키트의 CascadingDropDown 컨트롤은 dropdownlist 컨트롤을 확장 하 여 한 DropDownList의 변경 내용이 다른 DropDownList의 관련 값을 로드 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03da-110">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="e03da-111">예를 들어, 한 목록에는 미국 주 목록이 제공 되며 다음 목록에는 해당 상태의 주 도시가 채워집니다. 그러나 CascadingDropDown 컨트롤을 사용 하는 경우 ASP. 데이터를 목록에 비동기적으로 로드 하면 (불필요 한) 포스트백이 생성 되므로 NET의 DropDownList 컨트롤의 AutoPostBack 기능이 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e03da-111">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) However when using the CascadingDropDown control, ASP.NET's DropDownList control's AutoPostBack feature does not work, since asynchronously loading data into the list generates an (unnecessary) postback itself.</span></span> <span data-ttu-id="e03da-112">일부 JavaScript 코드를 사용 하면이 효과를 피할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e03da-112">With some JavaScript code, this effect can be avoided.</span></span>

## <a name="steps"></a><span data-ttu-id="e03da-113">단계</span><span class="sxs-lookup"><span data-stu-id="e03da-113">Steps</span></span>

<span data-ttu-id="e03da-114">ASP.NET AJAX 및 Control Toolkit의 기능을 활성화 하려면 페이지의 아무 곳에 나 `ScriptManager` 컨트롤을 배치 해야 합니다 (&lt;`form`&gt; 요소 내).</span><span class="sxs-lookup"><span data-stu-id="e03da-114">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the &lt;`form`&gt; element):</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample1.aspx)]

<span data-ttu-id="e03da-115">그런 다음, DropDownList 컨트롤이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03da-115">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample2.aspx)]

<span data-ttu-id="e03da-116">이 목록에 대해 웹 서비스 URL 및 메서드 정보를 제공 하는 CascadingDropDown extender가 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e03da-116">For this list, a CascadingDropDown extender is added, providing web service URL and method information:</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample3.aspx)]

<span data-ttu-id="e03da-117">그런 다음 CascadingDropDown extender는 다음 메서드 시그니처를 사용 하 여 웹 서비스를 비동기적으로 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03da-117">The CascadingDropDown extender then asynchronously calls a web service with the following method signature:</span></span>

[!code-csharp[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample4.cs)]

<span data-ttu-id="e03da-118">메서드는 CascadingDropDown value 형식의 배열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03da-118">The method returns an array of type CascadingDropDown value.</span></span> <span data-ttu-id="e03da-119">형식의 생성자는 먼저 목록 항목의 캡션과 값 (HTML `value` 특성)을 먼저 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03da-119">The type's constructor expects first the list entry's caption and then the value (HTML `value` attribute).</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample5.aspx)]

<span data-ttu-id="e03da-120">브라우저에서 페이지를 로드 하면 세 공급 업체가 세 번째로 미리 선택 된 상태로 드롭다운 목록을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="e03da-120">Loading the page in the browser will fill the dropdown list with three vendors, the second one being preselected.</span></span> <span data-ttu-id="e03da-121">또한 ASP.NET는 `__doPostBack()` JavaScript 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03da-121">Also, ASP.NET defines the `__doPostBack()` JavaScript method.</span></span> <span data-ttu-id="e03da-122">페이지가 로드 되 면이 JavaScript 호출은 드롭다운 목록에 추가 되지만 여기에는 요소가 있는 경우에만 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e03da-122">Once the page has been loaded, this JavaScript call is added to the dropdown list, but only if there are elements in it.</span></span> <span data-ttu-id="e03da-123">목록에 요소가 없으면 컨트롤 도구 키트가 현재 로드 하 고 있으므로 JavaScript 코드는 시간 제한을 사용 하 고 0.5 초 후에 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03da-123">If there are no elements in the list, the Control Toolkit is currently loading them, so the JavaScript code uses a timeout and tries again in a half second.</span></span>

[!code-html[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample6.html)]

<span data-ttu-id="e03da-124">이러한 방식으로, 목록에 실제로 요소가 있고 사용자가 항목을 선택 하는 경우에만 포스트백이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e03da-124">This way, a postback is only executed when there are actually elements in the list and the user selects an entry.</span></span>

<span data-ttu-id="e03da-125">[목록 요소를 선택 ![포스트백이 발생 합니다.](using-auto-postback-with-cascadingdropdown-cs/_static/image2.png)](using-auto-postback-with-cascadingdropdown-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e03da-125">[![Selecting a list element causes a postback](using-auto-postback-with-cascadingdropdown-cs/_static/image2.png)](using-auto-postback-with-cascadingdropdown-cs/_static/image1.png)</span></span>

<span data-ttu-id="e03da-126">목록 요소를 선택 하면 포스트백이 발생 합니다 ([전체 크기 이미지를 보려면 클릭](using-auto-postback-with-cascadingdropdown-cs/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="e03da-126">Selecting a list element causes a postback ([Click to view full-size image](using-auto-postback-with-cascadingdropdown-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e03da-127">[이전](presetting-list-entries-with-cascadingdropdown-cs.md)
> [다음](filling-a-list-using-cascadingdropdown-vb.md)</span><span class="sxs-lookup"><span data-stu-id="e03da-127">[Previous](presetting-list-entries-with-cascadingdropdown-cs.md)
[Next](filling-a-list-using-cascadingdropdown-vb.md)</span></span>
