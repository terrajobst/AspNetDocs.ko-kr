---
uid: web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
title: 애니메이션 중 작업 비활성화 (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 또한 작업을 지원 합니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a86c0276-6481-46ee-8b4f-8c2009399ee9
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
msc.type: authoredcontent
ms.openlocfilehash: 4924d4f70099255b930d53f6a72e810be7a47485
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430931"
---
# <a name="disabling-actions-during-animation-vb"></a><span data-ttu-id="7d2ad-104">애니메이션 중에 작업 사용 안 함(VB)</span><span class="sxs-lookup"><span data-stu-id="7d2ad-104">Disabling Actions during Animation (VB)</span></span>

<span data-ttu-id="7d2ad-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="7d2ad-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="7d2ad-106">[코드 다운로드](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="7d2ad-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7VB.pdf)</span></span>

> <span data-ttu-id="7d2ad-107">ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="7d2ad-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="7d2ad-108">또한 마우스 클릭과 같은 동작을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2ad-108">It also supports actions, like mouse clicks.</span></span> <span data-ttu-id="7d2ad-109">그러나 마우스 클릭으로 애니메이션을 시작 하는 경우 애니메이션 중 마우스 클릭을 사용 하지 않도록 설정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7d2ad-109">However when a mouse click starts an animation, it is desirable to disable mouse clicks during the animation.</span></span>

## <a name="overview"></a><span data-ttu-id="7d2ad-110">개요</span><span class="sxs-lookup"><span data-stu-id="7d2ad-110">Overview</span></span>

<span data-ttu-id="7d2ad-111">ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="7d2ad-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="7d2ad-112">또한 마우스 클릭과 같은 동작을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2ad-112">It also supports actions, like mouse clicks.</span></span> <span data-ttu-id="7d2ad-113">그러나 마우스 클릭으로 애니메이션을 시작 하는 경우 애니메이션 중 마우스 클릭을 사용 하지 않도록 설정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7d2ad-113">However when a mouse click starts an animation, it is desirable to disable mouse clicks during the animation.</span></span>

## <a name="steps"></a><span data-ttu-id="7d2ad-114">단계</span><span class="sxs-lookup"><span data-stu-id="7d2ad-114">Steps</span></span>

<span data-ttu-id="7d2ad-115">먼저 페이지에 `ScriptManager`를 포함 합니다. 그런 다음 ASP.NET AJAX 라이브러리가 로드 되어 컨트롤 도구 키트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d2ad-115">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample1.aspx)]

<span data-ttu-id="7d2ad-116">애니메이션은 다음과 같은 HTML 단추에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d2ad-116">The animation will be applied to an HTML button like this:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample2.aspx)]

<span data-ttu-id="7d2ad-117">단추를 사용 하 여 포스트백을 만들지 않기 때문에 웹 컨트롤 대신 HTML 컨트롤을 사용 합니다. 클라이언트 쪽 애니메이션을 시작 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d2ad-117">Note that an HTML Control is used instead of a Web Control since we do not want the button to create a postback; it shall just launch the client-side animation for us.</span></span>

<span data-ttu-id="7d2ad-118">그런 다음 `ID`, `TargetControlID` 특성 및 obligatory `runat="server"`를 제공 하 여 페이지에 `AnimationExtender`를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2ad-118">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample3.aspx)]

<span data-ttu-id="7d2ad-119">`<Animations>` 노드 내에서 `<OnClick>` 마우스 클릭을 처리할 올바른 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="7d2ad-119">Within the `<Animations>` node, `<OnClick>` is the right element to handle the mouse click.</span></span> <span data-ttu-id="7d2ad-120">그러나 애니메이션을 수행 하는 동안에도 단추를 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d2ad-120">However, the button could be clicked during the animation, as well.</span></span> <span data-ttu-id="7d2ad-121">`<EnableAction>` 요소는이를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d2ad-121">The `<EnableAction>` element can take care of that.</span></span> <span data-ttu-id="7d2ad-122">`Enabled="false"`를 설정 하면 애니메이션의 일부로 단추가 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7d2ad-122">Setting `Enabled="false"` disables the button as part of the animation.</span></span> <span data-ttu-id="7d2ad-123">여러 개별 애니메이션 (단추 및 실제 애니메이션 사용 안 함)을 사용 하 고 있으므로 단일 애니메이션을 하나로 붙이려면 `<Parallel>` 요소가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2ad-123">Since we are using several individual animations (disabling the button and the actual animations), the `<Parallel>` element is required to glue the single animations together into one.</span></span> <span data-ttu-id="7d2ad-124">`AnimationExtender`에 대 한 전체 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7d2ad-124">Here is the complete markup for `AnimationExtender`:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample4.aspx)]

<span data-ttu-id="7d2ad-125">목록의 끝에 있는 다음 XML 요소를 사용 하 여 애니메이션 뒤에 단추를 다시 사용 하도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d2ad-125">It would also be possible to re-enable to button after the animation, using the following XML element at the end of the list:</span></span>

[!code-xml[Main](disabling-actions-during-animation-vb/samples/sample5.xml)]

<span data-ttu-id="7d2ad-126">그러나 지정 된 시나리오에서는 단추가 페이드 아웃 되어 애니메이션의 끝에 표시 되지 않으므로이는 쓸모가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7d2ad-126">However in the given scenario this would be useless since the button fades out and is not visible at the end of the animation.</span></span>

<span data-ttu-id="7d2ad-127">[![애니메이션이 실행 되는 즉시 단추를 사용할 수 없습니다.](disabling-actions-during-animation-vb/_static/image2.png)](disabling-actions-during-animation-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7d2ad-127">[![The button is disabled as soon as the animation runs](disabling-actions-during-animation-vb/_static/image2.png)](disabling-actions-during-animation-vb/_static/image1.png)</span></span>

<span data-ttu-id="7d2ad-128">애니메이션을 실행 하는 즉시 단추를 사용할 수 없습니다 ([전체 크기 이미지를 보려면 클릭](disabling-actions-during-animation-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="7d2ad-128">The button is disabled as soon as the animation runs ([Click to view full-size image](disabling-actions-during-animation-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7d2ad-129">[이전](animating-in-response-to-user-interaction-vb.md)
> [다음](triggering-an-animation-in-another-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="7d2ad-129">[Previous](animating-in-response-to-user-interaction-vb.md)
[Next](triggering-an-animation-in-another-control-vb.md)</span></span>
