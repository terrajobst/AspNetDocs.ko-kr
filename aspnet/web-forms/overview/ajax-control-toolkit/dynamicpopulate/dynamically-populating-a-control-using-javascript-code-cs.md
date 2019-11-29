---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-cs
title: JavaScript 코드를 사용 하 여 동적으로C#컨트롤 채우기 () | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 DynamicPopulate 컨트롤은 웹 서비스 (또는 페이지 메서드)를 호출 하 고 결과 값을 t ...의 대상 컨트롤로 채웁니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: cc4c2def-e88c-4456-ae8b-a6ae0ff8cc2d
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 24dc358427dec3ffcba16d00041c9a2db657e7e2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599255"
---
# <a name="dynamically-populating-a-control-using-javascript-code-c"></a><span data-ttu-id="5c74e-103">JavaScript 코드를 사용하여 동적으로 컨트롤 채우기(C#)</span><span class="sxs-lookup"><span data-stu-id="5c74e-103">Dynamically Populating a Control Using JavaScript Code (C#)</span></span>

<span data-ttu-id="5c74e-104">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="5c74e-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="5c74e-105">[코드 다운로드](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="5c74e-105">[Download Code](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1CS.pdf)</span></span>

> <span data-ttu-id="5c74e-106">ASP.NET AJAX 컨트롤 도구 키트의 DynamicPopulate 컨트롤은 웹 서비스 (또는 페이지 메서드)를 호출 하 고 페이지를 새로 고치지 않고 결과 값을 페이지의 대상 컨트롤로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="5c74e-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="5c74e-107">사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 채우기를 트리거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c74e-107">It is also possible to trigger the population using custom client-side JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="5c74e-108">개요</span><span class="sxs-lookup"><span data-stu-id="5c74e-108">Overview</span></span>

<span data-ttu-id="5c74e-109">ASP.NET AJAX 컨트롤 도구 키트의 `DynamicPopulate` 컨트롤은 웹 서비스 (또는 페이지 메서드)를 호출 하 고 페이지를 새로 고치지 않고 결과 값을 페이지의 대상 컨트롤로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="5c74e-109">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="5c74e-110">사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 채우기를 트리거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c74e-110">It is also possible to trigger the population using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="5c74e-111">단계</span><span class="sxs-lookup"><span data-stu-id="5c74e-111">Steps</span></span>

<span data-ttu-id="5c74e-112">먼저 `DynamicPopulateExtender` 컨트롤에 의해 호출 되는 메서드를 구현 하는 ASP.NET 웹 서비스가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c74e-112">First of all, you need an ASP.NET Web Service which implements the method to be called by the `DynamicPopulateExtender` control.</span></span> <span data-ttu-id="5c74e-113">`DynamicPopulate` 컨트롤이 각 웹 서비스 호출을 사용 하 여 하나의 컨텍스트 정보를 보내기 때문에 웹 서비스는 `contextKey`라는 문자열 형식의 인수 하나를 예상 하는 `getDate()` 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c74e-113">The web service implements the method `getDate()` that expects one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="5c74e-114">다음은 세 가지 형식 중 하나로 현재 날짜를 검색 하는 코드 (파일 `DynamicPopulate.cs.asmx`)입니다.</span><span class="sxs-lookup"><span data-stu-id="5c74e-114">Here is the code (file `DynamicPopulate.cs.asmx`) which retrieves the current date in one of three formats:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample1.aspx)]

<span data-ttu-id="5c74e-115">다음 단계에서는 새 ASP.NET 사이트를 만들고 ASP.NET AJAX ScriptManager 컨트롤을 사용 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c74e-115">In the next step, create a new ASP.NET site and start with the ASP.NET AJAX ScriptManager control:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample2.aspx)]

<span data-ttu-id="5c74e-116">그런 다음 나중에 웹 서비스 호출의 결과를 표시 하는 동일한 이름의 HTML 컨트롤이 나 `<asp:Label />` 웹 컨트롤을 사용 하 여 레이블 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c74e-116">Then, add a label control (for instance using the HTML control of the same name, or the `<asp:Label />` web control) which will later show the result of the web service call.</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample3.aspx)]

<span data-ttu-id="5c74e-117">그런 다음 `DynamicPopulateExtender` 컨트롤을 포함 하 고 웹 서비스 정보, 대상 제어를 제공 하지만, 채우기를 트리거하는 컨트롤의 이름은 나중에 사용자 지정 JavaScript를 사용 하 여 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c74e-117">Next, include a `DynamicPopulateExtender` control and provide web service information, target control, but not the name of the control which triggers the population this will be done later on, using custom JavaScript!</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample4.aspx)]

<span data-ttu-id="5c74e-118">이제 JavaScript 파트로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="5c74e-118">Now to the JavaScript part.</span></span> <span data-ttu-id="5c74e-119">ASP.NET AJAX 라이브러리에 의해 정의 되는 `$find()` 함수는 `DynamicPopulateExtender`와 같은 ASP.NET AJAX 컨트롤 도구 키트의 서버 쪽 개체에 대 한 참조를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c74e-119">The `$find()` function, defined by the ASP.NET AJAX library, returns a reference to server-side objects of the ASP.NET AJAX Control Toolkit such as `DynamicPopulateExtender`.</span></span> <span data-ttu-id="5c74e-120">현재 파일에서 `$find("dpe")`는 페이지의 한 `DynamicPopulateExtender` 컨트롤에 대 한 참조를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c74e-120">In the current file, `$find("dpe")` returns a reference to the one `DynamicPopulateExtender` control in the page.</span></span> <span data-ttu-id="5c74e-121">동적 채우기 프로세스를 트리거하는 `populate()` 이라는 메서드를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c74e-121">It exposes a method called `populate()` which triggers the dynamic population process.</span></span> <span data-ttu-id="5c74e-122">`populate()` 메서드는 하나의 인수를 사용 해야 합니다. 컨텍스트 키는 `getDate()` 웹 메서드에 대 한 인수로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c74e-122">The `populate()` method requires one argument: the context key which will serve as argument to the `getDate()` web method.</span></span> <span data-ttu-id="5c74e-123">예를 들어 `$find("dpe").populate("format1")`는 레이블을 월-일-연도 형식의 현재 날짜로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="5c74e-123">So for instance, `$find("dpe").populate("format1")` would populate the label with the current date in month-day-year format.</span></span>

<span data-ttu-id="5c74e-124">예제를 좀 더 유연 하 게 만들기 위해 이제 사용자가 여러 날짜 형식 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c74e-124">In order to make the sample a bit more flexible, the user may now choose between several date formats.</span></span> <span data-ttu-id="5c74e-125">이러한 각 항목에 대해 라디오 단추가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c74e-125">For each one of them, a radio button is displayed.</span></span> <span data-ttu-id="5c74e-126">사용자가 라디오 단추를 클릭 하면 JavaScript 코드가 자동으로 레이블을 선택한 날짜 형식으로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="5c74e-126">Once the user clicks on a radio button, JavaScript code dynamically populates the label with the selected date format.</span></span> <span data-ttu-id="5c74e-127">해당 라디오 단추는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5c74e-127">Here are those radio buttons:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample5.aspx)]

<span data-ttu-id="5c74e-128">라디오 단추의 컨텍스트 내에서 JavaScript 식 `this.value`는 현재 단추의 값을 참조 하며,이 값은 `getDate()` 메서드가 사용할 수 있는 것과 정확히 동일한 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c74e-128">Note that within the context of a radio button, the JavaScript expression `this.value` refers to the value of the current button, which happens to be exactly the same information the `getDate()` method can work with.</span></span>

<span data-ttu-id="5c74e-129">[![단추를 클릭 하면 지정 된 형식으로 서버에서 날짜를 검색 합니다.](dynamically-populating-a-control-using-javascript-code-cs/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5c74e-129">[![A click on the button retrieves the date from the server, in the format specified](dynamically-populating-a-control-using-javascript-code-cs/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="5c74e-130">단추를 클릭 하면 서버에서 지정 된 형식으로 날짜가 검색 됩니다 ([전체 크기 이미지를 보려면 클릭](dynamically-populating-a-control-using-javascript-code-cs/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="5c74e-130">A click on the button retrieves the date from the server, in the format specified ([Click to view full-size image](dynamically-populating-a-control-using-javascript-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5c74e-131">[이전](dynamically-populating-a-control-cs.md)
> [다음](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)</span><span class="sxs-lookup"><span data-stu-id="5c74e-131">[Previous](dynamically-populating-a-control-cs.md)
[Next](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)</span></span>
