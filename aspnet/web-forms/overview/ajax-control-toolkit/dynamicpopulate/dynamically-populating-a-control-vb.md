---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-vb
title: 동적으로 컨트롤 채우기 (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 DynamicPopulate 컨트롤은 웹 서비스 (또는 페이지 메서드)를 호출 하 고 결과 값을 t ...의 대상 컨트롤로 채웁니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 27305347-7b5d-4519-97b7-197a357e7f6e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-vb
msc.type: authoredcontent
ms.openlocfilehash: d11320f1f89bb69afe5f62751574079716124da0
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599388"
---
# <a name="dynamically-populating-a-control-vb"></a><span data-ttu-id="7600b-103">동적으로 컨트롤 채우기(VB)</span><span class="sxs-lookup"><span data-stu-id="7600b-103">Dynamically Populating a Control (VB)</span></span>

<span data-ttu-id="7600b-104">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="7600b-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="7600b-105">[코드 다운로드](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="7600b-105">[Download Code](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0VB.pdf)</span></span>

> <span data-ttu-id="7600b-106">ASP.NET AJAX 컨트롤 도구 키트의 DynamicPopulate 컨트롤은 웹 서비스 (또는 페이지 메서드)를 호출 하 고 페이지를 새로 고치지 않고 결과 값을 페이지의 대상 컨트롤로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="7600b-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span>

## <a name="overview"></a><span data-ttu-id="7600b-107">개요</span><span class="sxs-lookup"><span data-stu-id="7600b-107">Overview</span></span>

<span data-ttu-id="7600b-108">ASP.NET AJAX 컨트롤 도구 키트의 `DynamicPopulate` 컨트롤은 웹 서비스 (또는 페이지 메서드)를 호출 하 고 페이지를 새로 고치지 않고 결과 값을 페이지의 대상 컨트롤로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="7600b-108">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="7600b-109">이 자습서에서는이를 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7600b-109">This tutorial shows how to set this up.</span></span>

## <a name="steps"></a><span data-ttu-id="7600b-110">단계</span><span class="sxs-lookup"><span data-stu-id="7600b-110">Steps</span></span>

<span data-ttu-id="7600b-111">먼저 `DynamicPopulate`에 의해 호출 되는 메서드를 구현 하는 ASP.NET 웹 서비스가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7600b-111">First of all, you need an ASP.NET Web Service which implements the method to be called by `DynamicPopulate`.</span></span> <span data-ttu-id="7600b-112">웹 서비스 클래스에는 `Microsoft.Web.Script.Services`내에 정의 된 `ScriptService` 특성이 필요 합니다. 그렇지 않으면 ASP.NET AJAX는 웹 서비스에 대 한 클라이언트 쪽 JavaScript 프록시를 만들 수 없으며,이 프록시는 `DynamicPopulate`에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7600b-112">The web service class requires the `ScriptService` attribute which is defined within `Microsoft.Web.Script.Services`; otherwise ASP.NET AJAX cannot create the client-side JavaScript proxy for the web service which in turn is required by `DynamicPopulate`.</span></span>

<span data-ttu-id="7600b-113">`DynamicPopulate` 컨트롤은 각 웹 서비스 호출을 사용 하 여 하나의 컨텍스트 정보를 보내기 때문에 웹 메서드는 `contextKey`라는 문자열 형식의 인수를 하나 이상 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7600b-113">The web method must expect one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="7600b-114">다음 웹 서비스는 `contextKey` 인수로 표시 되는 형식으로 현재 날짜를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7600b-114">The following web service returns the current date in a format represented by the `contextKey` argument:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample1.aspx)]

<span data-ttu-id="7600b-115">그런 다음 웹 서비스는 `DynamicPopulate.vb.asmx`로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7600b-115">The web service is then saved as `DynamicPopulate.vb.asmx`.</span></span> <span data-ttu-id="7600b-116">또는 `DynamicPopulate` 컨트롤을 사용 하 여 실제 ASP.NET 페이지 내에서 `getDate()` 메서드를 페이지 메서드로 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7600b-116">Alternatively, you could implement the `getDate()` method as a page method within the actual ASP.NET page with the `DynamicPopulate` control.</span></span>

<span data-ttu-id="7600b-117">다음 단계에서 새 ASP.NET 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7600b-117">In the next step, create a new ASP.NET file.</span></span> <span data-ttu-id="7600b-118">항상 첫 번째 단계는 현재 페이지에 `ScriptManager`를 포함 하 여 ASP.NET AJAX 라이브러리를 로드 하 고 컨트롤 도구 키트의 작업을 수행 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7600b-118">As always, the first step is to include the `ScriptManager` in the current page to load the ASP.NET AJAX library and to make the Control Toolkit work:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample2.aspx)]

<span data-ttu-id="7600b-119">그런 다음 나중에 웹 서비스 호출의 결과를 표시 하는 동일한 이름의 HTML 컨트롤이 나 &gt; 웹 컨트롤  /`asp:Label`&lt;을 사용 하 여 레이블 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7600b-119">Then, add a label control (for instance using the HTML control of the same name, or the &lt;`asp:Label` /&gt; web control) which will later show the result of the web service call.</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample3.aspx)]

<span data-ttu-id="7600b-120">HTML 단추 (서버에 대 한 포스트백을 요구 하지 않으므로 HTML 컨트롤)는 동적 채우기를 트리거하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7600b-120">An HTML button (as an HTML control, since we do not require a postback to the server) will then be used to trigger the dynamic population:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample4.aspx)]

<span data-ttu-id="7600b-121">마지막으로, 항목을 연결 하는 `DynamicPopulateExtender` 컨트롤이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7600b-121">Finally, we need the `DynamicPopulateExtender` control to wire things up.</span></span> <span data-ttu-id="7600b-122">다음 특성이 설정 됩니다 (분명 한 것은 `ID`, `runat`=`"server"`).</span><span class="sxs-lookup"><span data-stu-id="7600b-122">The following attributes will be set (apart from the obvious ones, `ID` and `runat`=`"server"`):</span></span>

- <span data-ttu-id="7600b-123">웹 서비스 호출에서 결과를 넣을 위치를 `TargetControlID` 합니다.</span><span class="sxs-lookup"><span data-stu-id="7600b-123">`TargetControlID` where to put the result from the web service call</span></span>
- <span data-ttu-id="7600b-124">웹 서비스의 `ServicePath` 경로 (페이지 메서드를 사용 하려는 경우 생략)</span><span class="sxs-lookup"><span data-stu-id="7600b-124">`ServicePath` path to the web service (omit if you want to use a page method)</span></span>
- <span data-ttu-id="7600b-125">웹 메서드 또는 페이지 메서드의 `ServiceMethod` 이름</span><span class="sxs-lookup"><span data-stu-id="7600b-125">`ServiceMethod` name of the web method or page method</span></span>
- <span data-ttu-id="7600b-126">웹 서비스로 보낼 컨텍스트 정보를 `ContextKey` 합니다.</span><span class="sxs-lookup"><span data-stu-id="7600b-126">`ContextKey` context information to be sent to the web service</span></span>
- <span data-ttu-id="7600b-127">웹 서비스 호출을 트리거하는 `PopulateTriggerControlID` 요소</span><span class="sxs-lookup"><span data-stu-id="7600b-127">`PopulateTriggerControlID` element which triggers the web service call</span></span>
- <span data-ttu-id="7600b-128">웹 서비스 호출 중에 대상 요소를 비울 지 여부를 `ClearContentsDuringUpdate` 합니다.</span><span class="sxs-lookup"><span data-stu-id="7600b-128">`ClearContentsDuringUpdate` whether to empty the target element during the web service call</span></span>

<span data-ttu-id="7600b-129">여기에서 볼 수 있듯이, 컨트롤에는 일부 정보가 필요 하지만 모든 항목을 제자리에 배치 하는 것은 매우 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="7600b-129">As you can see, the control requires some information but putting everything into place is quite straight-forward.</span></span> <span data-ttu-id="7600b-130">현재 시나리오의 `DynamicPopulateExtender` 컨트롤에 대 한 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7600b-130">Here is the markup for the `DynamicPopulateExtender` control in the current scenario:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample5.aspx)]

<span data-ttu-id="7600b-131">브라우저에서 ASP.NET 페이지를 실행 하 고 단추를 클릭 합니다. 월-일-연도 형식으로 현재 날짜를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7600b-131">Run the ASP.NET page in the browser and click on the button; you will receive the current date in month-day-year format.</span></span>

<span data-ttu-id="7600b-132">[![단추를 클릭 하면 서버에서 날짜가 검색 됩니다.](dynamically-populating-a-control-vb/_static/image2.png)](dynamically-populating-a-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7600b-132">[![A click on the button retrieves the date from the server](dynamically-populating-a-control-vb/_static/image2.png)](dynamically-populating-a-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="7600b-133">단추를 클릭 하면 서버에서 날짜가 검색 됩니다 ([전체 크기 이미지를 보려면 클릭](dynamically-populating-a-control-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="7600b-133">A click on the button retrieves the date from the server ([Click to view full-size image](dynamically-populating-a-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7600b-134">[이전](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)
> [다음](dynamically-populating-a-control-using-javascript-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="7600b-134">[Previous](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)
[Next](dynamically-populating-a-control-using-javascript-code-vb.md)</span></span>
