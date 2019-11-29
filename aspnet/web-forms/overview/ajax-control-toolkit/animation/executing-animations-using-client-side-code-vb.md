---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-vb
title: 클라이언트 쪽 코드를 사용 하 여 애니메이션 실행 (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 애니메이션 실행 ...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f7073f50-d765-456d-9957-926ce60f35f6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 7ef36900d20d8d07c3c6f3b63ce96568a377a0ed
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575506"
---
# <a name="executing-animations-using-client-side-code-vb"></a><span data-ttu-id="0424e-104">클라이언트 쪽 코드를 사용하여 애니메이션 실행(VB)</span><span class="sxs-lookup"><span data-stu-id="0424e-104">Executing Animations Using Client-Side Code (VB)</span></span>

<span data-ttu-id="0424e-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="0424e-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="0424e-106">[코드 다운로드](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="0424e-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10VB.pdf)</span></span>

> <span data-ttu-id="0424e-107">ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="0424e-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="0424e-108">사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 애니메이션 실행을 트리거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0424e-108">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="0424e-109">개요</span><span class="sxs-lookup"><span data-stu-id="0424e-109">Overview</span></span>

<span data-ttu-id="0424e-110">ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="0424e-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="0424e-111">사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 애니메이션 실행을 트리거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0424e-111">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="0424e-112">단계</span><span class="sxs-lookup"><span data-stu-id="0424e-112">Steps</span></span>

<span data-ttu-id="0424e-113">먼저 페이지에 `ScriptManager`를 포함 합니다. 그런 다음 ASP.NET AJAX 라이브러리가 로드 되어 컨트롤 도구 키트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0424e-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample1.aspx)]

<span data-ttu-id="0424e-114">애니메이션은 다음과 같은 텍스트 패널에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0424e-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample2.aspx)]

<span data-ttu-id="0424e-115">패널의 연결 된 CSS 클래스에서 좋은 배경색을 정의 하 고 패널의 고정 폭도 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0424e-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-animations-using-client-side-code-vb/samples/sample3.css)]

<span data-ttu-id="0424e-116">그런 다음 `ID`, `TargetControlID` 특성 및 obligatory `runat="server"`를 제공 하 여 페이지에 `AnimationExtender`를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0424e-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample4.aspx)]

<span data-ttu-id="0424e-117">`<Animations>` 노드 내에서 `<OnClick>`를 사용 하 여 사용자가 패널을 클릭 하면 애니메이션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0424e-117">Within the `<Animations>` node, use `<OnClick>` to run the animations once the user clicks on the panel.</span></span> <span data-ttu-id="0424e-118">병렬로 실행 되는 두 개의 애니메이션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0424e-118">Add two animations to be executed in parallel:</span></span>

[!code-xml[Main](executing-animations-using-client-side-code-vb/samples/sample5.xml)]

<span data-ttu-id="0424e-119">데모용으로이 애니메이션 및 컨트롤 도구 키트를 사용 하 여 만든 다른 모든 애니메이션은 페이지가 실행 되 면 JavaScript 코드를 사용 하 여 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0424e-119">For the sake of demonstration, this animation (and any other animation created using the Control Toolkit) is executed using JavaScript code, once the page runs.</span></span> <span data-ttu-id="0424e-120">먼저 `AnimationExtender` 컨트롤에 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0424e-120">First of all we need access to the `AnimationExtender` control.</span></span> <span data-ttu-id="0424e-121">ASP.NET AJAX 라이브러리는이 작업에 대 한 `$find()` 함수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0424e-121">The ASP.NET AJAX library provides the `$find()` function for this task:</span></span>

[!code-csharp[Main](executing-animations-using-client-side-code-vb/samples/sample6.cs)]

<span data-ttu-id="0424e-122">`AnimationExtender` 컨트롤은 XML 태그에 사용 되는 이벤트 처리기와 동일한 이름을 가진 메서드 (`OnClick()`, `OnLoad()`등)를 포함 하 여 다양 한 API를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="0424e-122">The `AnimationExtender` control exposes a rich API, including methods with names identical to the event handlers used in the XML markup: `OnClick()`, `OnLoad()`, and so on.</span></span> <span data-ttu-id="0424e-123">예를 들어 `OnClick()` 메서드 호출은 `AnimationExtender` 컨트롤의 `<OnClick>` 요소 내에서 애니메이션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0424e-123">For instance, a call of the `OnClick()` method executes the animation within the `<OnClick>` element of the `AnimationExtender` control:</span></span>

[!code-javascript[Main](executing-animations-using-client-side-code-vb/samples/sample7.js)]

<span data-ttu-id="0424e-124">페이지가 완전히 로드 된 후 패널의 클릭을 에뮬레이트하는 전체 클라이언트 쪽 JavaScript 코드는 페이지와 포함 된 모든 JavaScript 라이브러리가 로드 된 후 ASP.NET AJAX에 의해 호출 되는 `pageLoad()` 함수 이름이 사용 됨을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0424e-124">Here is the complete client-side JavaScript code that emulates the click on the panel once the page has been fully loaded note that the `pageLoad()` function name is used which is called by ASP.NET AJAX once the page and all included JavaScript libraries have been loaded.</span></span>

[!code-html[Main](executing-animations-using-client-side-code-vb/samples/sample8.html)]

<span data-ttu-id="0424e-125">[마우스를 클릭 하지 않고 애니메이션이 즉시 실행 ![](executing-animations-using-client-side-code-vb/_static/image2.png)](executing-animations-using-client-side-code-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0424e-125">[![The animation runs immediately, without a mouse click](executing-animations-using-client-side-code-vb/_static/image2.png)](executing-animations-using-client-side-code-vb/_static/image1.png)</span></span>

<span data-ttu-id="0424e-126">마우스 클릭 없이 애니메이션이 즉시 실행 됩니다 ([전체 크기 이미지를 보려면 클릭](executing-animations-using-client-side-code-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="0424e-126">The animation runs immediately, without a mouse click ([Click to view full-size image](executing-animations-using-client-side-code-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0424e-127">[이전](modifying-animations-from-the-server-side-vb.md)
> [다음](changing-an-animation-using-client-side-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="0424e-127">[Previous](modifying-animations-from-the-server-side-vb.md)
[Next](changing-an-animation-using-client-side-code-vb.md)</span></span>
