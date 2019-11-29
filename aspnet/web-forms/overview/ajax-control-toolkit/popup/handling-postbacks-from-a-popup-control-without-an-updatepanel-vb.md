---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
title: UpdatePanel을 사용 하지 않고 Popup 컨트롤에서 포스트백 처리 (VB) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 PopupControl extender는 다른 컨트롤이 활성화 될 때 팝업을 쉽게 트리거하는 방법을 제공 합니다. Su에서 포스트백이 발생 하는 경우 ...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a0b9186c-0912-4fff-916a-6d17e696a50b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: aaecf77c1d25f2c99ef4e9948d79fc01b837169b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611724"
---
# <a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-vb"></a><span data-ttu-id="f27f2-104">UpdatePanel을 사용하지 않고 팝업 컨트롤에서 포스트백 처리(VB)</span><span class="sxs-lookup"><span data-stu-id="f27f2-104">Handling Postbacks from A Popup Control Without an UpdatePanel (VB)</span></span>

<span data-ttu-id="f27f2-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="f27f2-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f27f2-106">[코드 다운로드](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="f27f2-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3VB.pdf)</span></span>

> <span data-ttu-id="f27f2-107">AJAX 컨트롤 도구 키트의 PopupControl extender는 다른 컨트롤이 활성화 될 때 팝업을 쉽게 트리거하는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f27f2-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="f27f2-108">이러한 패널에서 포스트백이 발생 하 고 페이지에 여러 패널이 있으면 클릭 한 패널을 확인 하기가 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="f27f2-108">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="overview"></a><span data-ttu-id="f27f2-109">개요</span><span class="sxs-lookup"><span data-stu-id="f27f2-109">Overview</span></span>

<span data-ttu-id="f27f2-110">AJAX 컨트롤 도구 키트의 PopupControl extender는 다른 컨트롤이 활성화 될 때 팝업을 쉽게 트리거하는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f27f2-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="f27f2-111">이러한 패널에서 포스트백이 발생 하 고 페이지에 여러 패널이 있으면 클릭 한 패널을 확인 하기가 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="f27f2-111">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="steps"></a><span data-ttu-id="f27f2-112">단계</span><span class="sxs-lookup"><span data-stu-id="f27f2-112">Steps</span></span>

<span data-ttu-id="f27f2-113">포스트백과 함께 `PopupControl`를 사용할 때 페이지에 `UpdatePanel` 없는 경우, 컨트롤 도구 키트는 팝업을 트리거한 클라이언트 요소를 확인 하는 방법을 제공 하지 않습니다 .이는 다시 게시를 발생 시킨 클라이언트 요소를 확인 하는 방법을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f27f2-113">When using a `PopupControl` with a postback, but without having an `UpdatePanel` on the page, the Control Toolkit does not offer a way to determine which client element has triggered the popup which in turn caused the postback.</span></span> <span data-ttu-id="f27f2-114">그러나 작은 트릭은이 시나리오에 대 한 해결 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f27f2-114">However a small trick provides a workaround for this scenario.</span></span>

<span data-ttu-id="f27f2-115">먼저, 다음은 기본 설정입니다. 두 텍스트 상자는 동일한 팝업 인 달력을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="f27f2-115">First of all, here is the basic setup: two text boxes which both trigger the same popup, a calendar.</span></span> <span data-ttu-id="f27f2-116">텍스트 상자와 팝업을 함께 표시 하는 두 가지 `PopupControlExtenders`입니다.</span><span class="sxs-lookup"><span data-stu-id="f27f2-116">Two `PopupControlExtenders` bring text boxes and popup together.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample1.aspx)]

<span data-ttu-id="f27f2-117">기본적인 개념은 popup을 시작한 텍스트 상자를 포함 하는 &lt;`form`&gt; 요소에 숨겨진 양식 필드를 추가 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f27f2-117">The basic idea is to add a hidden form field in the &lt;`form`&gt; element that holds the text box which launched the popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample2.aspx)]

<span data-ttu-id="f27f2-118">페이지가 로드 되 면 JavaScript 코드는 두 텍스트 상자 모두에 이벤트 처리기를 추가 합니다. 사용자가 텍스트 상자를 클릭할 때마다 숨겨진 폼 필드에 해당 이름이 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f27f2-118">When the page is loaded, JavaScript code adds an event handler to both text boxes: Whenever the user clicks on a text box, its name is written into the hidden form field:</span></span>

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample3.html)]

<span data-ttu-id="f27f2-119">서버 쪽 코드에서 숨김 필드의 값을 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f27f2-119">In the server-side code, the value of the hidden field must be read.</span></span> <span data-ttu-id="f27f2-120">숨겨진 양식 필드는 조작 하기는 쉽지 않으므로 숨겨진 값의 유효성을 검사 하는 허용 목록 접근 방식이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f27f2-120">Since hidden form fields are trivial to manipulate, a whitelist approach to validate the hidden value is required.</span></span> <span data-ttu-id="f27f2-121">올바른 텍스트 상자를 확인 한 후에는 달력의 날짜가 해당 텍스트 상자에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f27f2-121">Once the correct text box has been identified, the date from the calendar is written into it.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample4.aspx)]

<span data-ttu-id="f27f2-122">[사용자가 텍스트 상자를 클릭할 때 달력이 표시 되는 ![](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f27f2-122">[![The Calendar appears when the user clicks into the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image1.png)</span></span>

<span data-ttu-id="f27f2-123">사용자가 텍스트 상자를 클릭 하면 달력이 나타납니다 ([전체 크기 이미지를 보려면 클릭](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="f27f2-123">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image3.png))</span></span>

<span data-ttu-id="f27f2-124">[날짜를 클릭 ![텍스트 상자에 배치 됩니다.](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="f27f2-124">[![Clicking on a date puts it in the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image4.png)</span></span>

<span data-ttu-id="f27f2-125">날짜를 클릭 하면 텍스트 상자에 배치 됩니다 ([전체 크기 이미지를 보려면 클릭](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image6.png)).</span><span class="sxs-lookup"><span data-stu-id="f27f2-125">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="f27f2-126">이전</span><span class="sxs-lookup"><span data-stu-id="f27f2-126">Previous</span></span>](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)
