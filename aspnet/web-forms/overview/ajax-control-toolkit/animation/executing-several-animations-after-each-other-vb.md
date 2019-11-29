---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
title: 서로 다른 여러 애니메이션 실행 (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. Severa을 실행할 수 있습니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 21ece509-79cc-4d9d-892d-7b6e9c4d3502
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
msc.type: authoredcontent
ms.openlocfilehash: 5034fe905299d4559b713dd841cb166886179c39
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606900"
---
# <a name="executing-several-animations-after-each-other-vb"></a><span data-ttu-id="77210-104">여러 애니메이션을 순차적으로 실행(VB)</span><span class="sxs-lookup"><span data-stu-id="77210-104">Executing Several Animations after Each Other (VB)</span></span>

<span data-ttu-id="77210-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="77210-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="77210-106">[코드 다운로드](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="77210-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.vb.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3VB.pdf)</span></span>

> <span data-ttu-id="77210-107">ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="77210-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="77210-108">이를 통해 여러 애니메이션을 차례로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77210-108">It allows to run several animations one after the other.</span></span>

## <a name="overview"></a><span data-ttu-id="77210-109">개요</span><span class="sxs-lookup"><span data-stu-id="77210-109">Overview</span></span>

<span data-ttu-id="77210-110">ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="77210-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="77210-111">이를 통해 여러 애니메이션을 차례로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77210-111">It allows to run several animations one after the other.</span></span>

## <a name="steps"></a><span data-ttu-id="77210-112">단계</span><span class="sxs-lookup"><span data-stu-id="77210-112">Steps</span></span>

<span data-ttu-id="77210-113">먼저 페이지에 `ScriptManager`를 포함 합니다. 그런 다음 ASP.NET AJAX 라이브러리가 로드 되어 컨트롤 도구 키트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77210-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample1.aspx)]

<span data-ttu-id="77210-114">애니메이션은 다음과 같은 텍스트 패널에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77210-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample2.aspx)]

<span data-ttu-id="77210-115">패널의 연결 된 CSS 클래스에서 좋은 배경색을 정의 하 고 패널의 고정 폭도 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="77210-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-after-each-other-vb/samples/sample3.css)]

<span data-ttu-id="77210-116">그런 다음 `ID`, `TargetControlID` 특성 및 obligatory을 제공 하 여 페이지에 `AnimationExtender`를 추가 `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="77210-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample4.aspx)]

<span data-ttu-id="77210-117">`<Animations>` 노드 내에서 `<OnLoad>`를 사용 하 여 페이지가 완전히 로드 되 면 애니메이션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="77210-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="77210-118">일반적으로 `<OnLoad>`는 하나의 애니메이션만 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="77210-118">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="77210-119">애니메이션 프레임 워크를 사용 하면 `<Sequence>` 요소를 사용 하 여 여러 애니메이션을 하나로 조인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77210-119">The Animation framework allows you to join several animations into one using the `<Sequence>` element.</span></span> <span data-ttu-id="77210-120">`<Sequence>` 내의 모든 애니메이션은 그 다음에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77210-120">All animations within `<Sequence>` are executed one after the other.</span></span> <span data-ttu-id="77210-121">다음은 `AnimationExtender` 컨트롤에 사용할 수 있는 태그입니다. 먼저 패널의 너비를 높이 거 나 높이를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="77210-121">Here is the a possible markup for the `AnimationExtender` control, first making the panel wider and then decreasing its height:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample5.aspx)]

<span data-ttu-id="77210-122">이 스크립트를 실행 하면 패널의 크기가 더 넓어집니다.</span><span class="sxs-lookup"><span data-stu-id="77210-122">When you run this script, the panel first gets wider and then smaller.</span></span>

<span data-ttu-id="77210-123">[처음 ![너비가 증가 합니다.](executing-several-animations-after-each-other-vb/_static/image2.png)](executing-several-animations-after-each-other-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="77210-123">[![First the width is increased](executing-several-animations-after-each-other-vb/_static/image2.png)](executing-several-animations-after-each-other-vb/_static/image1.png)</span></span>

<span data-ttu-id="77210-124">먼저 너비가 증가 합니다 ([전체 크기 이미지를 보려면 클릭](executing-several-animations-after-each-other-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="77210-124">First the width is increased ([Click to view full-size image](executing-several-animations-after-each-other-vb/_static/image3.png))</span></span>

<span data-ttu-id="77210-125">[![높이가 감소 합니다.](executing-several-animations-after-each-other-vb/_static/image5.png)](executing-several-animations-after-each-other-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="77210-125">[![Then the height is decreased](executing-several-animations-after-each-other-vb/_static/image5.png)](executing-several-animations-after-each-other-vb/_static/image4.png)</span></span>

<span data-ttu-id="77210-126">그러면 높이가 줄어듭니다 ([전체 크기 이미지를 보려면 클릭](executing-several-animations-after-each-other-vb/_static/image6.png)).</span><span class="sxs-lookup"><span data-stu-id="77210-126">Then the height is decreased ([Click to view full-size image](executing-several-animations-after-each-other-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="77210-127">[이전](executing-several-animations-at-the-same-time-vb.md)
> [다음](animation-depending-on-a-condition-vb.md)</span><span class="sxs-lookup"><span data-stu-id="77210-127">[Previous](executing-several-animations-at-the-same-time-vb.md)
[Next](animation-depending-on-a-condition-vb.md)</span></span>
