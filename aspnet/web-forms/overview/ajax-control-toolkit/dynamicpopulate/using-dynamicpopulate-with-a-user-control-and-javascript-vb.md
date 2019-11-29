---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
title: 사용자 컨트롤 및 JavaScript에서 DynamicPopulate 사용 (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 DynamicPopulate 컨트롤은 웹 서비스 (또는 페이지 메서드)를 호출 하 고 결과 값을 t ...의 대상 컨트롤로 채웁니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 778b9009-76f2-4665-940e-afc0e35bc917
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
msc.type: authoredcontent
ms.openlocfilehash: ee5923ad6d8b101f689a0564aef8b1e0e00a7639
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599135"
---
# <a name="using-dynamicpopulate-with-a-user-control-and-javascript-vb"></a><span data-ttu-id="2dff5-103">사용자 정의 컨트롤 및 JavaScript에 DynamicPopulate 사용(VB)</span><span class="sxs-lookup"><span data-stu-id="2dff5-103">Using DynamicPopulate with a User Control And JavaScript (VB)</span></span>

<span data-ttu-id="2dff5-104">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="2dff5-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="2dff5-105">[코드 다운로드](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="2dff5-105">[Download Code](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2VB.pdf)</span></span>

> <span data-ttu-id="2dff5-106">ASP.NET AJAX 컨트롤 도구 키트의 DynamicPopulate 컨트롤은 웹 서비스 (또는 페이지 메서드)를 호출 하 고 페이지를 새로 고치지 않고 결과 값을 페이지의 대상 컨트롤로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="2dff5-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="2dff5-107">사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 채우기를 트리거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dff5-107">It is also possible to trigger the population using custom client-side JavaScript code.</span></span> <span data-ttu-id="2dff5-108">그러나 extender가 사용자 정의 컨트롤에 있는 경우 특별 한 주의를 기울여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dff5-108">However special care has to be taken when the extender resides in a user control.</span></span>

## <a name="overview"></a><span data-ttu-id="2dff5-109">개요</span><span class="sxs-lookup"><span data-stu-id="2dff5-109">Overview</span></span>

<span data-ttu-id="2dff5-110">ASP.NET AJAX 컨트롤 도구 키트의 `DynamicPopulate` 컨트롤은 웹 서비스 (또는 페이지 메서드)를 호출 하 고 페이지를 새로 고치지 않고 결과 값을 페이지의 대상 컨트롤로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="2dff5-110">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="2dff5-111">사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 채우기를 트리거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dff5-111">It is also possible to trigger the population using custom client-side JavaScript code.</span></span> <span data-ttu-id="2dff5-112">그러나 extender가 사용자 정의 컨트롤에 있는 경우 특별 한 주의를 기울여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dff5-112">However special care has to be taken when the extender resides in a user control.</span></span>

## <a name="steps"></a><span data-ttu-id="2dff5-113">단계</span><span class="sxs-lookup"><span data-stu-id="2dff5-113">Steps</span></span>

<span data-ttu-id="2dff5-114">먼저 `DynamicPopulateExtender` 컨트롤에 의해 호출 되는 메서드를 구현 하는 ASP.NET 웹 서비스가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dff5-114">First of all, you need an ASP.NET Web Service which implements the method to be called by the `DynamicPopulateExtender` control.</span></span> <span data-ttu-id="2dff5-115">`DynamicPopulate` 컨트롤이 각 웹 서비스 호출을 사용 하 여 하나의 컨텍스트 정보를 보내기 때문에 웹 서비스는 `contextKey`라는 문자열 형식의 인수 하나를 예상 하는 `getDate()` 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dff5-115">The web service implements the method `getDate()` that expects one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="2dff5-116">다음은 세 가지 형식 중 하나로 현재 날짜를 검색 하는 코드 (파일 `DynamicPopulate.vb.asmx`)입니다.</span><span class="sxs-lookup"><span data-stu-id="2dff5-116">Here is the code (files `DynamicPopulate.vb.asmx`) which retrieves the current date in one of three formats:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample1.aspx)]

<span data-ttu-id="2dff5-117">다음 단계에서 첫 번째 줄에서 다음 선언으로 표시 되는 새 사용자 정의 컨트롤 (`.ascx` 파일)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2dff5-117">In the next step, create a new user control (`.ascx` file), denoted by the following declaration in its first line:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample2.aspx)]

<span data-ttu-id="2dff5-118">&lt;`label`&gt; 요소는 서버에서 들어오는 데이터를 표시 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dff5-118">A &lt;`label`&gt; element will be used to display the data coming from the server.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample3.aspx)]

<span data-ttu-id="2dff5-119">또한 사용자 정의 컨트롤 파일에는 웹 서비스에서 지 원하는 세 가지 날짜 형식 중 하나를 나타내는 세 개의 라디오 단추가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dff5-119">Also in the user control file, we will use three radio buttons, each one representing one of the three possible date formats supported by the web service.</span></span> <span data-ttu-id="2dff5-120">사용자가 라디오 단추 중 하나를 클릭 하면 브라우저에서 다음과 같은 JavaScript 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dff5-120">When the user clicks on one of the radio buttons, the browser will execute JavaScript code which looks like this:</span></span>

[!code-powershell[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample4.ps1)]

<span data-ttu-id="2dff5-121">이 코드는 `DynamicPopulateExtender`에 액세스 합니다 (이상한 ID에 대해서는 걱정할 필요가 없으며,이 내용은 나중에 설명 됨), 데이터를 사용 하 여 동적 채우기를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="2dff5-121">This code accesses the `DynamicPopulateExtender` (do not worry about the strange ID yet, this will be covered later on) and triggers the dynamic population with data.</span></span> <span data-ttu-id="2dff5-122">현재 라디오 단추의 컨텍스트에서 `this.value`는 `format1`, `format2` 또는 `format3` 웹 메서드에 필요한 것과 같은 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2dff5-122">In the context of the current radio button, `this.value` refers to its value which is `format1`, `format2` or `format3` exactly what the web method expects.</span></span>

<span data-ttu-id="2dff5-123">사용자 정의 컨트롤에서 아직 누락 된 것은 웹 서비스에 라디오 단추를 연결 하는 `DynamicPopulateExtender` 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="2dff5-123">The only thing missing in the user control yet is the `DynamicPopulateExtender` control which links the radio buttons to the web service.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample5.aspx)]

<span data-ttu-id="2dff5-124">이 경우에도 컨트롤에서 사용 되는 이상한 ID를 `myDate`대신 `mcd1$myDate` 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dff5-124">Again you may note the strange ID used in the control: `mcd1$myDate` instead of `myDate`.</span></span> <span data-ttu-id="2dff5-125">이전에는 JavaScript 코드를 사용 하 여 `dpe1`대신 `DynamicPopulateExtender`에 액세스 `mcd1_dpe1` 했습니다. 이 명명 전략은 사용자 정의 컨트롤 내에서 `DynamicPopulateExtender`를 사용할 때 특별 한 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="2dff5-125">Previously, the JavaScript code used `mcd1_dpe1` to access the `DynamicPopulateExtender` instead of `dpe1`.This naming strategy is a special requirement when using `DynamicPopulateExtender` within a user control.</span></span> <span data-ttu-id="2dff5-126">또한 모든 작업을 수행 하기 위해 특정 방법으로 사용자 정의 컨트롤을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dff5-126">Furthermore, you have to embed the user control in a specific way to make it all work.</span></span> <span data-ttu-id="2dff5-127">새 ASP.NET 페이지를 만들고 방금 구현한 사용자 정의 컨트롤에 대 한 태그 접두사를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dff5-127">Create a new ASP.NET page and register a tag prefix for the user control you have just implemented:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample6.aspx)]

<span data-ttu-id="2dff5-128">그런 다음 새 페이지에 ASP.NET AJAX `ScriptManager` 컨트롤을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dff5-128">Then, include the ASP.NET AJAX `ScriptManager` control on the new page:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample7.aspx)]

<span data-ttu-id="2dff5-129">마지막으로 페이지에 사용자 정의 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dff5-129">Finally, add the user control to the page.</span></span> <span data-ttu-id="2dff5-130">`ID` 특성 (및 `runat="server"`)만 설정 해야 하지만,이를 특정 이름으로 설정 해야 합니다 .이는 JavaScript를 사용 하 여 액세스 하기 위해 사용자 정의 컨트롤 내에서 사용 되는 접두사 이므로 `mcd1`.</span><span class="sxs-lookup"><span data-stu-id="2dff5-130">You only have to set its `ID` attribute (and `runat="server"`, of course), but you also have to set it to a specific name: `mcd1` since this is the prefix used within the user control to access it using JavaScript.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample8.aspx)]

<span data-ttu-id="2dff5-131">됐습니다!</span><span class="sxs-lookup"><span data-stu-id="2dff5-131">And that's it!</span></span> <span data-ttu-id="2dff5-132">페이지가 예상 대로 동작 합니다. 사용자가 라디오 단추 중 하나를 클릭 하면 도구 키트의 컨트롤이 웹 서비스를 호출 하 고 원하는 형식으로 현재 날짜를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dff5-132">The page behaves as expected: A user clicks on one of the radio buttons, the control in the Toolkit calls the web service and displays the current date in the desired format.</span></span>

<span data-ttu-id="2dff5-133">[사용자 정의 컨트롤에 있는 라디오 단추 ![](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2dff5-133">[![The radio buttons reside in a user control](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image1.png)</span></span>

<span data-ttu-id="2dff5-134">라디오 단추는 사용자 정의 컨트롤에 있습니다 ([전체 크기 이미지를 보려면 클릭](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="2dff5-134">The radio buttons reside in a user control ([Click to view full-size image](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="2dff5-135">이전</span><span class="sxs-lookup"><span data-stu-id="2dff5-135">Previous</span></span>](dynamically-populating-a-control-using-javascript-code-vb.md)
