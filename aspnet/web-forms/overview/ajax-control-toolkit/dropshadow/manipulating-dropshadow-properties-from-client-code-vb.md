---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
title: 클라이언트 코드에서 DropShadow 속성 조작 (VB) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 DropShadow 컨트롤은 그림자가 있는 패널을 확장 합니다. Client JavaScrip를 사용 하 여이 extender의 속성을 변경할 수도 있습니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 11be4211-2fb9-4e15-b6d4-2aa623d81f3e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
msc.type: authoredcontent
ms.openlocfilehash: a39adb9c06819f6f828add7d762effad430b8570
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497411"
---
# <a name="manipulating-dropshadow-properties-from-client-code-vb"></a><span data-ttu-id="c681c-104">클라이언트 코드에서 DropShadow 속성 조작(VB)</span><span class="sxs-lookup"><span data-stu-id="c681c-104">Manipulating DropShadow Properties from Client Code (VB)</span></span>

<span data-ttu-id="c681c-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="c681c-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="c681c-106">[코드 다운로드](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="c681c-106">[Download Code](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2VB.pdf)</span></span>

> <span data-ttu-id="c681c-107">AJAX 컨트롤 도구 키트의 DropShadow 컨트롤은 그림자가 있는 패널을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c681c-107">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="c681c-108">클라이언트 JavaScript 코드를 사용 하 여이 extender의 속성을 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c681c-108">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="c681c-109">개요</span><span class="sxs-lookup"><span data-stu-id="c681c-109">Overview</span></span>

<span data-ttu-id="c681c-110">AJAX 컨트롤 도구 키트의 DropShadow 컨트롤은 그림자가 있는 패널을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c681c-110">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="c681c-111">클라이언트 JavaScript 코드를 사용 하 여이 extender의 속성을 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c681c-111">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="c681c-112">단계</span><span class="sxs-lookup"><span data-stu-id="c681c-112">Steps</span></span>

<span data-ttu-id="c681c-113">코드는 일부 텍스트 줄이 포함 된 패널로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c681c-113">The code starts with a panel containing some lines of text:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample1.aspx)]

<span data-ttu-id="c681c-114">연결 된 CSS 클래스는 패널에 멋진 배경색을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c681c-114">The associated CSS class gives the panel a nice background color:</span></span>

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample2.css)]

<span data-ttu-id="c681c-115">그림자 효과, 불투명도가 50%로 설정 된 패널을 확장 하는 `DropShadowExtender` 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c681c-115">The `DropShadowExtender` is added to extend the panel with a drop shadow effect, opacity set to 50%:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample3.aspx)]

<span data-ttu-id="c681c-116">그런 다음 ASP.NET AJAX `ScriptManager` 컨트롤을 사용 하 여 컨트롤 도구 키트가 작동 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c681c-116">Then, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample4.aspx)]

<span data-ttu-id="c681c-117">다른 패널에는 그림자의 불투명도를 설정 하기 위한 두 가지 JavaScript 링크가 있습니다. 빼기 링크는 그림자의 불투명도를 줄이고 더하기 링크를 통해이를 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="c681c-117">Another panel contains two JavaScript links for setting the opacity of the drop shadow: the minus link decreases the shadow's opacity, the plus link increases it.</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample5.aspx)]

<span data-ttu-id="c681c-118">그러면 JavaScript 함수 `changeOpacity()` 먼저 페이지에서 `DropShadowExtender` 컨트롤을 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c681c-118">The JavaScript function `changeOpacity()` must then first find the `DropShadowExtender` control on the page.</span></span> <span data-ttu-id="c681c-119">ASP.NET AJAX는 정확히 해당 작업에 대 한 `$find()` 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c681c-119">ASP.NET AJAX defines the `$find()` method for exactly that task.</span></span> <span data-ttu-id="c681c-120">그런 다음 `get_Opacity()` 메서드는 현재 불투명도를 검색 하 고 `set_Opacity()` 메서드는이를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c681c-120">Then, the `get_Opacity()` method retrieves the current opacity, the `set_Opacity()` method sets it.</span></span> <span data-ttu-id="c681c-121">JavaScript 코드는 현재 불투명도 값을 `<label>` 요소에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c681c-121">The JavaScript code then puts the current opacity value in the `<label>` element:</span></span>

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample6.html)]

<span data-ttu-id="c681c-122">[클라이언트 쪽에서 불투명도가 변경 ![](manipulating-dropshadow-properties-from-client-code-vb/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c681c-122">[![The opacity is changed on the client side](manipulating-dropshadow-properties-from-client-code-vb/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-vb/_static/image1.png)</span></span>

<span data-ttu-id="c681c-123">클라이언트 쪽에서 불투명도가 변경 됩니다 ([전체 크기 이미지를 보려면 클릭](manipulating-dropshadow-properties-from-client-code-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="c681c-123">The opacity is changed on the client side ([Click to view full-size image](manipulating-dropshadow-properties-from-client-code-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="c681c-124">이전</span><span class="sxs-lookup"><span data-stu-id="c681c-124">Previous</span></span>](adjusting-the-z-index-of-a-dropshadow-vb.md)
