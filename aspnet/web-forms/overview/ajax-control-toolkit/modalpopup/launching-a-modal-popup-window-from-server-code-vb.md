---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-vb
title: 서버 코드에서 모달 팝업 창 시작 (VB) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 ModalPopup 컨트롤은 클라이언트 쪽을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 그러나 일부 시나리오에서는
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 36ca81d7-906d-4db2-952b-add18a4ff421
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 1368a78d35ac6461bbc2e852e468f42eef2c0d2c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606586"
---
# <a name="launching-a-modal-popup-window-from-server-code-vb"></a><span data-ttu-id="92697-104">서버 코드에서 모달 팝업 창 시작(VB)</span><span class="sxs-lookup"><span data-stu-id="92697-104">Launching a Modal Popup Window from Server Code (VB)</span></span>

<span data-ttu-id="92697-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="92697-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="92697-106">[코드 다운로드](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="92697-106">[Download Code](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1VB.pdf)</span></span>

> <span data-ttu-id="92697-107">AJAX 컨트롤 도구 키트의 ModalPopup 컨트롤은 클라이언트 쪽을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="92697-108">그러나 일부 시나리오의 경우에는 서버 쪽에서 모달 팝업을 여는 것이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-108">However some scenarios require that the opening of the modal popup is triggered on the server-side.</span></span>

## <a name="overview"></a><span data-ttu-id="92697-109">개요</span><span class="sxs-lookup"><span data-stu-id="92697-109">Overview</span></span>

<span data-ttu-id="92697-110">AJAX 컨트롤 도구 키트의 ModalPopup 컨트롤은 클라이언트 쪽을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="92697-111">그러나 일부 시나리오의 경우에는 서버 쪽에서 모달 팝업을 여는 것이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-111">However some scenarios require that the opening of the modal popup is triggered on the server-side.</span></span>

## <a name="steps"></a><span data-ttu-id="92697-112">단계</span><span class="sxs-lookup"><span data-stu-id="92697-112">Steps</span></span>

<span data-ttu-id="92697-113">먼저, ModalPopup 컨트롤이 작동 하는 방법을 보여 주기 위해 ASP.NET Button 웹 컨트롤이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-113">First of all, an ASP.NET Button web control is required to demonstrate how the ModalPopup control works.</span></span> <span data-ttu-id="92697-114">새 페이지의 &lt;폼&gt; 요소에 이러한 단추를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-114">Add such a button within the &lt;form&gt; element on a new page:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample1.aspx)]

<span data-ttu-id="92697-115">그런 다음 만들려는 팝업에 대 한 태그가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-115">Then, you need the markup for the popup you want to create.</span></span> <span data-ttu-id="92697-116">`<asp:Panel>` 컨트롤로 정의 하 고 단추 컨트롤이 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-116">Define it as an `<asp:Panel>` control and make sure that it includes a Button control.</span></span> <span data-ttu-id="92697-117">ModalPopup 컨트롤은 이러한 단추를 팝업을 닫기 위한 기능을 제공 합니다. 그렇지 않은 경우에는 쉽게 사라질 수 있는 방법이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="92697-117">The ModalPopup control offers the functionality to make such a button close the popup; otherwise there is no easy way to let it vanish.</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample2.aspx)]

<span data-ttu-id="92697-118">그런 다음 ASP.NET AJAX Toolkit의 ModalPopup 컨트롤을 페이지에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-118">Next add the ModalPopup control from the ASP.NET AJAX Toolkit to the page.</span></span> <span data-ttu-id="92697-119">컨트롤을 로드 하는 단추에 대 한 속성을 설정 하 고 단추를 사라지게 하는 단추와 실제 팝업의 ID를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-119">Set properties for the button which loads the control, the button which makes it disappear, and the ID of the actual popup.</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample3.aspx)]

<span data-ttu-id="92697-120">ASP.NET AJAX를 기반으로 하는 모든 웹 페이지와 마찬가지로 스크립트 관리자는 다음과 같은 다양 한 대상 브라우저에 필요한 JavaScript 라이브러리를 로드 하는 데 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-120">As with all web pages based on ASP.NET AJAX; the Script Manager is required to load the necessary JavaScript libraries for the different target browsers:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample4.aspx)]

<span data-ttu-id="92697-121">브라우저에서 예제를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-121">Run the example in the browser.</span></span> <span data-ttu-id="92697-122">단추를 클릭 하면 모달 팝업이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="92697-122">When you click on the button, the modal popup appears.</span></span> <span data-ttu-id="92697-123">서버 쪽 코드를 사용 하 여 동일한 결과를 얻기 위해 새 단추가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-123">In order to achieve the same effect using server-side code, a new button is required:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample5.aspx)]

<span data-ttu-id="92697-124">여기에서 볼 수 있듯이 단추를 클릭 하면 포스트백이 생성 되 고 서버에서 `ServerButton_Click()` 메서드가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92697-124">As you can see, a click on the button generates a postback and executes the `ServerButton_Click()` method on the server.</span></span> <span data-ttu-id="92697-125">이 메서드에서 `launchModal()` 이라는 JavaScript 함수는 정확 하 게 실행 됩니다. 페이지가 로드 되 면 JavaScript 함수가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92697-125">In this method, a JavaScript function called `launchModal()` is executed to be exact, the JavaScript function will be executed once the page has been loaded:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample6.aspx)]

<span data-ttu-id="92697-126">`launchModal()` 작업은 ModalPopup을 표시 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="92697-126">The job of `launchModal()` is to display the ModalPopup.</span></span> <span data-ttu-id="92697-127">`launchModal()` 함수는 전체 HTML 페이지가 로드 된 후에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92697-127">The `launchModal()` function is executed once the complete HTML page has been loaded.</span></span> <span data-ttu-id="92697-128">그러나이 시점에서 ASP.NET AJAX 프레임 워크는 아직 완전히 로드 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="92697-128">At that moment, however, the ASP.NET AJAX framework has not been fully loaded yet.</span></span> <span data-ttu-id="92697-129">따라서 `launchModal()` 함수는 ModalPopup 컨트롤이 나중에 표시 되어야 하는 변수만 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-129">Therefore, the `launchModal()` function just sets a variable that the ModalPopup control must be shown later on:</span></span>

[!code-html[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample7.html)]

<span data-ttu-id="92697-130">`pageLoad()` JavaScript 함수는 ASP.NET AJAX가 완전히 로드 된 후 실행 되는 특수 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="92697-130">The `pageLoad()` JavaScript function is a special function that gets executed once ASP.NET AJAX has been fully loaded.</span></span> <span data-ttu-id="92697-131">따라서이 함수에 코드를 추가 하 여 ModalPopup 컨트롤을 표시 하지만 `launchModal()` 이전에 호출 된 경우에만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92697-131">Therefore we add code to this function to show the ModalPopup control, but only if `launchModal()` has been called before:</span></span>

[!code-javascript[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample8.js)]

<span data-ttu-id="92697-132">`$find()` 함수는 페이지에서 명명 된 요소를 찾고 서버측 ID를 매개 변수로 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="92697-132">The `$find()` function is looking for a named element on the page and expects the server-side ID as a parameter.</span></span> <span data-ttu-id="92697-133">따라서 `$find("mpe")`는 ModalPopup 컨트롤의 클라이언트 표현을 반환 합니다. 해당 `show()` 메서드를 사용 하면 팝업이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92697-133">Therefore, `$find("mpe")` returns the client representation of the ModalPopup control; its `show()` method lets the popup appear.</span></span>

<span data-ttu-id="92697-134">[단추 중 하나를 클릭 하면 모달 팝업이 나타납니다 ![](launching-a-modal-popup-window-from-server-code-vb/_static/image2.png)](launching-a-modal-popup-window-from-server-code-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="92697-134">[![The modal popup appears when either of the buttons is clicked](launching-a-modal-popup-window-from-server-code-vb/_static/image2.png)](launching-a-modal-popup-window-from-server-code-vb/_static/image1.png)</span></span>

<span data-ttu-id="92697-135">단추 중 하나를 클릭 하면 모달 팝업이 나타납니다 ([전체 크기 이미지를 보려면 클릭](launching-a-modal-popup-window-from-server-code-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="92697-135">The modal popup appears when either of the buttons is clicked ([Click to view full-size image](launching-a-modal-popup-window-from-server-code-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="92697-136">[이전](positioning-a-modalpopup-cs.md)
> [다음](using-modalpopup-with-a-repeater-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="92697-136">[Previous](positioning-a-modalpopup-cs.md)
[Next](using-modalpopup-with-a-repeater-control-vb.md)</span></span>
