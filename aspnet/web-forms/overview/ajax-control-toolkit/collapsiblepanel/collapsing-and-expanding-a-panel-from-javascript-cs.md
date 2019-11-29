---
uid: web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-cs
title: JavaScript에서 패널 축소 및 확장 (C#) | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 CollapsiblePanel 컨트롤은 패널을 확장 하 고 콘텐츠를 축소 하 고 확장 하는 기능을 제공 합니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: de5500be-75e5-461a-8064-b70ae52ea6a4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-cs
msc.type: authoredcontent
ms.openlocfilehash: bed14d82394d28336493bec10e31ddb4d411a192
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599450"
---
# <a name="collapsing-and-expanding-a-panel-from-javascript-c"></a><span data-ttu-id="883b1-103">JavaScript에서 패널 축소 및 확장(C#)</span><span class="sxs-lookup"><span data-stu-id="883b1-103">Collapsing and Expanding a Panel from JavaScript (C#)</span></span>

<span data-ttu-id="883b1-104">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="883b1-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="883b1-105">[코드 다운로드](https://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="883b1-105">[Download Code](https://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1CS.pdf)</span></span>

> <span data-ttu-id="883b1-106">ASP.NET AJAX 컨트롤 도구 키트의 CollapsiblePanel 컨트롤은 패널을 확장 하 고 콘텐츠를 축소 하 고 다시 확장할 수 있는 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="883b1-106">The CollapsiblePanel control in the ASP.NET AJAX Control Toolkit extends a panel and provides it with the capability to collapse its contents and expand it again.</span></span> <span data-ttu-id="883b1-107">이러한 두 작업은 사용자 지정 JavaScript 코드에서 트리거될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="883b1-107">These two actions can also be triggered from custom JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="883b1-108">개요</span><span class="sxs-lookup"><span data-stu-id="883b1-108">Overview</span></span>

<span data-ttu-id="883b1-109">ASP.NET AJAX 컨트롤 도구 키트의 CollapsiblePanel 컨트롤은 패널을 확장 하 고 콘텐츠를 축소 하 고 다시 확장할 수 있는 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="883b1-109">The CollapsiblePanel control in the ASP.NET AJAX Control Toolkit extends a panel and provides it with the capability to collapse its contents and expand it again.</span></span> <span data-ttu-id="883b1-110">이러한 두 작업은 사용자 지정 JavaScript 코드에서 트리거될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="883b1-110">These two actions can also be triggered from custom JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="883b1-111">단계</span><span class="sxs-lookup"><span data-stu-id="883b1-111">Steps</span></span>

<span data-ttu-id="883b1-112">먼저 새 ASP.NET 페이지를 만들고 하나의 `<form>` 요소 내에 `ScriptManager`를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="883b1-112">First of all, create a new ASP.NET page and include the `ScriptManager` within the one `<form>` element.</span></span> <span data-ttu-id="883b1-113">그러면 컨트롤 도구 키트에 필요한 ASP.NET AJAX 라이브러리가 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="883b1-113">This loads the ASP.NET AJAX library which is required by the Control Toolkit:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample1.aspx)]

<span data-ttu-id="883b1-114">그런 다음 축소/확장 효과를 볼 수 있도록 몇 가지 텍스트가 포함 된 패널을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="883b1-114">Then, create a panel with some text so that the collapse/expand effect can be seen:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample2.aspx)]

<span data-ttu-id="883b1-115">여기에서 볼 수 있듯이 패널은 여기에 표시 되는 CSS 클래스를 참조 합니다. 기본적으로 배경색과 패널의 너비를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="883b1-115">As you can see, the panel references a CSS class which is shown here (and basically defines a background color and the panel's width):</span></span>

[!code-css[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample3.css)]

<span data-ttu-id="883b1-116">`CollapsiblePanelExtender` 컨트롤에는 `TargetControlID` 특성이 필요 하므로 toolkit에서 요청 시 축소 하거나 확장할 패널을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="883b1-116">The `CollapsiblePanelExtender` control requires the `TargetControlID` attribute so that the toolkit knows which panel to collapse or expand upon request:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample4.aspx)]

<span data-ttu-id="883b1-117">아쉽게도 extender는 현재 패널을 축소 하거나 확장 하기 위한 특정 API를 노출 하지 않지만 일부 문서화 되지 않은 메서드는이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="883b1-117">Unfortunately, the extender currently does not expose a specific API for collapsing or expanding the panel, but some undocumented methods will do.</span></span> <span data-ttu-id="883b1-118">먼저 페이지에 세 개의 HTML 단추를 추가 합니다. 그러면이 페이지에 클라이언트 쪽 JavaScript를 트리거하여 패널의 내용을 축소 하거나 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="883b1-118">First of all, add three HTML buttons to the page which will then trigger the client-side JavaScript to collapse or expand the panel's contents:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample5.aspx)]

<span data-ttu-id="883b1-119">클라이언트 쪽 JavaScript 코드 (`<script type="text/javascript">`시작)에서는 `$find()` 메서드를 사용 하 여 `CollapsiblePanelExtender`에 액세스 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="883b1-119">In the client-side JavaScript code (started with `<script type="text/javascript">`), the `$find()` method needs to be used to access the `CollapsiblePanelExtender`.</span></span> <span data-ttu-id="883b1-120">`$find("cpe")`은이에 대 한 참조를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="883b1-120">`$find("cpe")` will return a reference to it.</span></span> <span data-ttu-id="883b1-121">여기서 특정 메서드는 현재 작업을 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="883b1-121">From there on, specific methods will solve the task at hand.</span></span>

<span data-ttu-id="883b1-122">패널을 열기 (확장) 하는 메서드를 `_doOpen()`이라고 합니다. 다음 코드는 첫 번째 단추를 클릭할 때 호출 되는 `doOpen()` 함수를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="883b1-122">The method for opening (expanding) the panel is called `_doOpen()`; the following code implements the `doOpen()` function called when the first button is clicked:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample6.js)]

<span data-ttu-id="883b1-123">패널을 닫거나 축소 하려면 `_doClose()` 메서드를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="883b1-123">For closing, or collapsing the panel, the `_doClose()` method needs to be executed.</span></span> <span data-ttu-id="883b1-124">따라서 사용자가 두 번째 단추를 클릭 하면 다음 JavaScript 코드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="883b1-124">So when the user clicks on the second button, the following JavaScript code is called:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample7.js)]

<span data-ttu-id="883b1-125">세 번째 단추는 패널의 상태를 축소 됨에서 확장 됨으로 전환 하 고 그 반대의 경우도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="883b1-125">The third button toggles the state of the panel: from collapsed to expanded, and vice versa.</span></span> <span data-ttu-id="883b1-126">`CollapsiblePanelExtender`는이 패널의 상태를 반대로 하는 `toggle()` 메서드를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="883b1-126">The `CollapsiblePanelExtender` exposes the `toggle()` method which does exactly that: reverses the state of the panel.</span></span> <span data-ttu-id="883b1-127">그러나 `toggle()` 메서드에서 내부적으로 사용 하는 다른 방법도 있습니다. `CollapsiblePanelExtender()`의 `get_Collapsed()` 메서드는 패널이 축소 되었는지 여부를 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="883b1-127">However there is also another approach (which is internally used by the `toggle()` method): The `get_Collapsed()` method of the `CollapsiblePanelExtender()` tells us whether the panel is collapsed or not.</span></span> <span data-ttu-id="883b1-128">이 함수의 반환 값에 따라 패널은 확장 (`_doOpen()` 메서드) 또는 축소 (`_doClose()`) 메서드 중 하나가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="883b1-128">Depending on the return value of this function, the panel is then either expanded (`_doOpen()` method) or collapsed (`_doClose()`) method:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample8.js)]

<span data-ttu-id="883b1-129">[세 번째 단추가 ![패널의 상태를 축소 됨에서 확장 후 뒤로 변경 합니다.](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="883b1-129">[![The third button changes the state of the panel: from collapsed to expanded and back](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image1.png)</span></span>

<span data-ttu-id="883b1-130">세 번째 단추는 패널의 상태를 축소 됨에서 확장 됨과 뒤로 변경 ([전체 크기 이미지를 보려면 클릭](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image3.png)) 합니다.</span><span class="sxs-lookup"><span data-stu-id="883b1-130">The third button changes the state of the panel: from collapsed to expanded and back ([Click to view full-size image](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="883b1-131">다음</span><span class="sxs-lookup"><span data-stu-id="883b1-131">Next</span></span>](collapsing-and-expanding-a-panel-from-javascript-vb.md)
