---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-vb
title: 동시에 여러 애니메이션 실행 (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. Severa을 실행할 수 있습니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2469f7ea-1489-42fb-a8e1-414c90141ce9
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-vb
msc.type: authoredcontent
ms.openlocfilehash: fc11debd06c897c29db56d42167d483f5608cdf8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575335"
---
# <a name="executing-several-animations-at-the-same-time-vb"></a><span data-ttu-id="c60bd-104">동시에 여러 애니메이션 실행 (VB)</span><span class="sxs-lookup"><span data-stu-id="c60bd-104">Executing Several Animations at The Same Time (VB)</span></span>

<span data-ttu-id="c60bd-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="c60bd-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="c60bd-106">[코드 다운로드](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="c60bd-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2VB.pdf)</span></span>

> <span data-ttu-id="c60bd-107">ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="c60bd-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="c60bd-108">이를 통해 여러 애니메이션을 병렬 방식으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c60bd-108">It allows to run several animations in a parallel fashion.</span></span>

## <a name="overview"></a><span data-ttu-id="c60bd-109">개요</span><span class="sxs-lookup"><span data-stu-id="c60bd-109">Overview</span></span>

<span data-ttu-id="c60bd-110">ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="c60bd-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="c60bd-111">이를 통해 여러 애니메이션을 병렬 방식으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c60bd-111">It allows to run several animations in a parallel fashion.</span></span>

## <a name="steps"></a><span data-ttu-id="c60bd-112">단계</span><span class="sxs-lookup"><span data-stu-id="c60bd-112">Steps</span></span>

<span data-ttu-id="c60bd-113">먼저 페이지에 `ScriptManager`를 포함 합니다. 그런 다음 ASP.NET AJAX 라이브러리가 로드 되어 컨트롤 도구 키트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c60bd-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample1.aspx)]

<span data-ttu-id="c60bd-114">애니메이션은 다음과 같은 텍스트 패널에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c60bd-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample2.aspx)]

<span data-ttu-id="c60bd-115">패널의 연결 된 CSS 클래스에서 좋은 배경색을 정의 하 고 패널의 고정 폭도 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c60bd-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-at-the-same-time-vb/samples/sample3.css)]

<span data-ttu-id="c60bd-116">그런 다음 `ID`, `TargetControlID` 특성 및 obligatory `runat="server"`를 제공 하 여 페이지에 `AnimationExtender`를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c60bd-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample4.aspx)]

<span data-ttu-id="c60bd-117">`<Animations>` 노드 내에서 `<OnLoad>`를 사용 하 여 페이지가 완전히 로드 되 면 애니메이션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c60bd-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="c60bd-118">일반적으로 `<OnLoad>`는 하나의 애니메이션만 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c60bd-118">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="c60bd-119">애니메이션 프레임 워크를 사용 하면 `<Parallel>` 요소를 사용 하 여 여러 애니메이션을 하나로 조인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c60bd-119">The Animation framework allows you to join several animations into one using the `<Parallel>` element.</span></span> <span data-ttu-id="c60bd-120">`<Parallel>` 내의 모든 애니메이션은 동시에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c60bd-120">All animations within `<Parallel>` are executed at the same time.</span></span>

<span data-ttu-id="c60bd-121">다음은 `AnimationExtender` 컨트롤에 사용할 수 있는 태그 이며, 동시에 패널을 페이드 아웃 하 고 크기를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c60bd-121">Here is the a possible markup for the `AnimationExtender` control, fading out and resizing the panel at the same time:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample5.aspx)]

<span data-ttu-id="c60bd-122">그리고 실제로이 스크립트를 실행 하면 패널이 표시 되 고 크기를 조정 하 여 (너비를 tripling 하 고 높이를 나누어) 동시에 페이드 아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="c60bd-122">And indeed: when you run this script, the panel is displayed, then resizes (more than tripling its width and halving its height) and fades out at the same time.</span></span>

<span data-ttu-id="c60bd-123">[패널을 페이드 아웃 하 고 크기를 조정 하는 ![(브라우저의 렌더링 엔진 덕분에 콘텐츠 포함)](executing-several-animations-at-the-same-time-vb/_static/image2.png)](executing-several-animations-at-the-same-time-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c60bd-123">[![The panel is fading out and resizing (including its content, thanks to the browser's rendering engine)](executing-several-animations-at-the-same-time-vb/_static/image2.png)](executing-several-animations-at-the-same-time-vb/_static/image1.png)</span></span>

<span data-ttu-id="c60bd-124">패널을 페이드 아웃 하 고 크기를 조정 합니다 (브라우저의 렌더링 엔진 덕분에 콘텐츠 포함). ([전체 이미지를 보려면 클릭](executing-several-animations-at-the-same-time-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="c60bd-124">The panel is fading out and resizing (including its content, thanks to the browser's rendering engine) ([Click to view full-size image](executing-several-animations-at-the-same-time-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c60bd-125">[이전](adding-animation-to-a-control-vb.md)
> [다음](executing-several-animations-after-each-other-vb.md)</span><span class="sxs-lookup"><span data-stu-id="c60bd-125">[Previous](adding-animation-to-a-control-vb.md)
[Next](executing-several-animations-after-each-other-vb.md)</span></span>
