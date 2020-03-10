---
uid: web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-vb
title: 목록에서 애니메이션 하나 선택 (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 프레임 워크도 허용 (.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 81ba9116-d485-40c0-8ff6-7e9ae23e0a0c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-vb
msc.type: authoredcontent
ms.openlocfilehash: 694416532b558291ff6ab57a442058b53d6167e0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430823"
---
# <a name="picking-one-animation-out-of-a-list-vb"></a><span data-ttu-id="8e6c2-104">목록에서 애니메이션 하나 선택(VB)</span><span class="sxs-lookup"><span data-stu-id="8e6c2-104">Picking One Animation Out Of a List (VB)</span></span>

<span data-ttu-id="8e6c2-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="8e6c2-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="8e6c2-106">[코드 다운로드](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="8e6c2-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5VB.pdf)</span></span>

> <span data-ttu-id="8e6c2-107">ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="8e6c2-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="8e6c2-108">또한 프레임 워크를 사용 하면 일부 JavaScript 코드의 평가에 따라 프로그래머가 애니메이션 목록에서 하나의 애니메이션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e6c2-108">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="8e6c2-109">개요</span><span class="sxs-lookup"><span data-stu-id="8e6c2-109">Overview</span></span>

<span data-ttu-id="8e6c2-110">ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="8e6c2-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="8e6c2-111">또한 프레임 워크를 사용 하면 일부 JavaScript 코드의 평가에 따라 프로그래머가 애니메이션 목록에서 하나의 애니메이션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e6c2-111">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="8e6c2-112">단계</span><span class="sxs-lookup"><span data-stu-id="8e6c2-112">Steps</span></span>

<span data-ttu-id="8e6c2-113">먼저 페이지에 `ScriptManager`를 포함 합니다. 그런 다음 ASP.NET AJAX 라이브러리가 로드 되어 컨트롤 도구 키트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e6c2-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample1.aspx)]

<span data-ttu-id="8e6c2-114">애니메이션은 다음과 같은 텍스트 패널에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e6c2-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample2.aspx)]

<span data-ttu-id="8e6c2-115">패널의 연결 된 CSS 클래스에서 좋은 배경색을 정의 하 고 패널의 고정 폭도 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e6c2-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](picking-one-animation-out-of-a-list-vb/samples/sample3.css)]

<span data-ttu-id="8e6c2-116">그런 다음 `ID`, `TargetControlID` 특성 및 obligatory을 제공 하 여 페이지에 `AnimationExtender`를 추가 `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="8e6c2-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample4.aspx)]

<span data-ttu-id="8e6c2-117">`<Animations>` 노드 내에서 `<OnLoad>`를 사용 하 여 페이지가 완전히 로드 되 면 애니메이션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e6c2-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="8e6c2-118">`<Case>` 요소는 일반적인 애니메이션 중 하나가 아니라 재생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e6c2-118">Instead of one of the regular animations, the `<Case>` element comes into play.</span></span> <span data-ttu-id="8e6c2-119">해당 SelectScript 특성의 값이 계산 됩니다. 반환 값은 숫자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e6c2-119">The value of its SelectScript attribute is evaluated; the return value must be numerical.</span></span> <span data-ttu-id="8e6c2-120">이 숫자에 따라 &lt;Case&gt; 내의 subanimations 중 하나가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e6c2-120">Depending on this number, one of the subanimations within &lt;Case&gt; is executed.</span></span> <span data-ttu-id="8e6c2-121">예를 들어 SelectScript가 2로 계산 되는 경우 컨트롤 도구 키트는 &lt;Case&gt; 내에서 세 번째 애니메이션을 실행 합니다 (계산은 0부터 시작).</span><span class="sxs-lookup"><span data-stu-id="8e6c2-121">For instance, if SelectScript evaluates to 2, the Control Toolkit runs the third animation within &lt;Case&gt; (counting starts at 0).</span></span>

<span data-ttu-id="8e6c2-122">다음 태그는 세 개의 하위 애니메이션 (너비 크기 조정, 높이 크기 조정 및 페이드 아웃)을 정의 합니다. JavaScript 코드 (`Math.floor(3 * Math.random())`)는 0과 2 사이의 숫자를 선택 하 여 세 가지 애니메이션 중 하나가 실행 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e6c2-122">The following markup defines three subanimations: Resizing the width, resizing the height, and fading out. The JavaScript code (`Math.floor(3 * Math.random())`) then picks a number between 0 and 2, so that one of the three animations is run:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample5.aspx)]

<span data-ttu-id="8e6c2-123">[가능한 세 가지 애니메이션 중 하나를 ![합니다. 즉, 패널은 더 넓어집니다.](picking-one-animation-out-of-a-list-vb/_static/image2.png)](picking-one-animation-out-of-a-list-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8e6c2-123">[![One of the possible three animations: The panel gets wider](picking-one-animation-out-of-a-list-vb/_static/image2.png)](picking-one-animation-out-of-a-list-vb/_static/image1.png)</span></span>

<span data-ttu-id="8e6c2-124">가능한 세 가지 애니메이션 중 하나: 패널이 더 넓게 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](picking-one-animation-out-of-a-list-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="8e6c2-124">One of the possible three animations: The panel gets wider ([Click to view full-size image](picking-one-animation-out-of-a-list-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8e6c2-125">[이전](animation-depending-on-a-condition-vb.md)
> [다음](animating-in-response-to-user-interaction-vb.md)</span><span class="sxs-lookup"><span data-stu-id="8e6c2-125">[Previous](animation-depending-on-a-condition-vb.md)
[Next](animating-in-response-to-user-interaction-vb.md)</span></span>
