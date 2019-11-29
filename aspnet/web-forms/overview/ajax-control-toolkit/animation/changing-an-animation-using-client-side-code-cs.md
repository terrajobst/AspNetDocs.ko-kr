---
uid: web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
title: 클라이언트 쪽 코드를 사용 하 여 애니메이션 변경C#() | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 애니메이션을 사용할 수도 있습니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2bfbc5cc-f942-44b7-a62d-a29520f1da9a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 84fc2d6646b89cfabb2193cdfca59462d6d7ef16
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606974"
---
# <a name="changing-an-animation-using-client-side-code-c"></a><span data-ttu-id="35c28-104">클라이언트 쪽 코드를 사용하여 애니메이션 변경(C#)</span><span class="sxs-lookup"><span data-stu-id="35c28-104">Changing an Animation Using Client-Side Code (C#)</span></span>

<span data-ttu-id="35c28-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="35c28-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="35c28-106">[코드 다운로드](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="35c28-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11CS.pdf)</span></span>

> <span data-ttu-id="35c28-107">ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="35c28-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="35c28-108">사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 애니메이션을 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35c28-108">The animation can also be changed using custom client-side JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="35c28-109">개요</span><span class="sxs-lookup"><span data-stu-id="35c28-109">Overview</span></span>

<span data-ttu-id="35c28-110">ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="35c28-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="35c28-111">사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 애니메이션을 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35c28-111">The animation can also be changed using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="35c28-112">단계</span><span class="sxs-lookup"><span data-stu-id="35c28-112">Steps</span></span>

<span data-ttu-id="35c28-113">먼저 페이지에 `ScriptManager`를 포함 합니다. 그런 다음 ASP.NET AJAX 라이브러리가 로드 되어 컨트롤 도구 키트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35c28-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample1.aspx)]

<span data-ttu-id="35c28-114">애니메이션은 다음과 같은 텍스트 패널에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35c28-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample2.aspx)]

<span data-ttu-id="35c28-115">패널의 연결 된 CSS 클래스에서 좋은 배경색을 정의 하 고 패널의 고정 폭도 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="35c28-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](changing-an-animation-using-client-side-code-cs/samples/sample3.css)]

<span data-ttu-id="35c28-116">실제 애니메이션은 HTML 단추를 통해 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35c28-116">The actual animation is launched by an HTML button:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample4.aspx)]

<span data-ttu-id="35c28-117">그런 다음 `ID`, `TargetControlID` 특성 및 obligatory `runat="server"`를 제공 하 여 페이지에 `AnimationExtender`를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="35c28-117">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample5.aspx)]

<span data-ttu-id="35c28-118">`AnimationExtender` 컨트롤 내에 `<Animations>` 노드가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="35c28-118">Note that there is no `<Animations>` node within the `AnimationExtender` control.</span></span> <span data-ttu-id="35c28-119">사용자 지정 JavaScript 코드는 컨트롤과 함께 사용 되는 애니메이션을 제공 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35c28-119">Custom JavaScript code is used to provide the animations to be used with the control.</span></span>

<span data-ttu-id="35c28-120">`AnimationExtender`의 서버 API와 마찬가지로 extender에 아직 애니메이션을 할당 하는 쉬운 방법은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="35c28-120">As with the server API of `AnimationExtender`, there is no easy way to assign an animation to the extender yet.</span></span> <span data-ttu-id="35c28-121">그러나 extender는 다양 한 이벤트 (`OnClick`, `OnLoad`등)에 등록 된 애니메이션을 읽고 쓰는 여러 메서드를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="35c28-121">However the extender does expose several methods to read and write animations registered with the various events (`OnClick`, `OnLoad`, and so on).</span></span> <span data-ttu-id="35c28-122">다음은 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="35c28-122">Here are some examples:</span></span>

- `get_OnClick()`
- `set_OnClick()`
- `get_OnLoad()`
- `set_OnLoad()`
- `...`

<span data-ttu-id="35c28-123">`get_*()` 함수의 반환 값 형식 및 `set_*()` 함수에 대 한 인수 형식은 JSON 문자열이 며 XML 태그가 무엇 인지에 대 한 개체 표현을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="35c28-123">The format of the return value of the `get_*()` functions and the format of the argument for the `set_*()` functions is a JSON string, providing an object representation of what the XML markup would be.</span></span> <span data-ttu-id="35c28-124">현재에서는 개체를 전달할 방법이 없지만 지정 된 애니메이션 (`get_OnXXXBehavior()` 메서드)에서 개체를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35c28-124">Currently, there is no way to pass an object in, but it is possible to read an object from a given animation (`get_OnXXXBehavior()` methods).</span></span>

<span data-ttu-id="35c28-125">다음은 단추에 의해 트리거되는 애니메이션을 나타내는 JSON 문자열 (구분 기호를 사용 하 여 깔끔하게 형식이 지정 되지 않음)이 고, 패널 크기를 조정 하 여 패널에 애니메이션을 적용 하 고 동시에 페이드 아웃 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="35c28-125">Here is a JSON string (without the delimiting quotes and formatted nicely) representing an animation triggered by the button, but animating the panel by resizing it and fading it out at the same time:</span></span>

[!code-json[Main](changing-an-animation-using-client-side-code-cs/samples/sample6.json)]

<span data-ttu-id="35c28-126">다음 JavaScript 코드는이 JSON descripting을 현재 extender의 `OnClick` 애니메이션에 할당 하 고 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="35c28-126">The following JavaScript code assigns this JSON descripting to the `OnClick` animation of the current extender and runs it:</span></span>

[!code-html[Main](changing-an-animation-using-client-side-code-cs/samples/sample7.html)]

<span data-ttu-id="35c28-127">[마우스를 클릭 하지 않고 매우 작은 태그를 사용 하 여 애니메이션이 즉시 실행 ![](changing-an-animation-using-client-side-code-cs/_static/image2.png)](changing-an-animation-using-client-side-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="35c28-127">[![The animation runs immediately, without a mouse click (and with very little markup)](changing-an-animation-using-client-side-code-cs/_static/image2.png)](changing-an-animation-using-client-side-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="35c28-128">애니메이션은 마우스 클릭 없이 (또는 매우 작은 태그를 사용 하 여) 즉시 실행 됩니다 ([전체 크기 이미지를 보려면 클릭](changing-an-animation-using-client-side-code-cs/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="35c28-128">The animation runs immediately, without a mouse click (and with very little markup) ([Click to view full-size image](changing-an-animation-using-client-side-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="35c28-129">[이전](executing-animations-using-client-side-code-cs.md)
> [다음](animating-an-updatepanel-control-cs.md)</span><span class="sxs-lookup"><span data-stu-id="35c28-129">[Previous](executing-animations-using-client-side-code-cs.md)
[Next](animating-an-updatepanel-control-cs.md)</span></span>
