---
uid: web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-cs
title: 텍스트 상자에 특정 문자만 허용 (C#) | Microsoft Docs
author: wenz
description: ASP.NET 유효성 검사 컨트롤을 사용 하면 사용자 입력에 특정 문자만 허용 되도록 할 수 있습니다. 그러나이 경우 사용자가 잘못 된 형식을 입력 하는 것을 방지할 수 없습니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: fd2a1c52-d717-44af-8a61-67c8279bb26e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-cs
msc.type: authoredcontent
ms.openlocfilehash: d1e367becd574e31d24fca8545f76b1ed3c4d85e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446357"
---
# <a name="allowing-only-certain-characters-in-a-text-box-c"></a><span data-ttu-id="f8cae-104">텍스트 상자에 특정 문자만 허용(C#)</span><span class="sxs-lookup"><span data-stu-id="f8cae-104">Allowing Only Certain Characters in a Text Box (C#)</span></span>

<span data-ttu-id="f8cae-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="f8cae-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f8cae-106">[코드 다운로드](https://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="f8cae-106">[Download Code](https://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0CS.pdf)</span></span>

> <span data-ttu-id="f8cae-107">ASP.NET 유효성 검사 컨트롤을 사용 하면 사용자 입력에 특정 문자만 허용 되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8cae-107">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="f8cae-108">그러나이 경우에도 사용자는 잘못 된 문자를 입력 하 고 양식을 전송 하는 것을 방지할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f8cae-108">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>

## <a name="overview"></a><span data-ttu-id="f8cae-109">개요</span><span class="sxs-lookup"><span data-stu-id="f8cae-109">Overview</span></span>

<span data-ttu-id="f8cae-110">ASP.NET 유효성 검사 컨트롤을 사용 하면 사용자 입력에 특정 문자만 허용 되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8cae-110">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="f8cae-111">그러나이 경우에도 사용자는 잘못 된 문자를 입력 하 고 양식을 전송 하는 것을 방지할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f8cae-111">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>

## <a name="steps"></a><span data-ttu-id="f8cae-112">단계</span><span class="sxs-lookup"><span data-stu-id="f8cae-112">Steps</span></span>

<span data-ttu-id="f8cae-113">ASP.NET AJAX 컨트롤 도구 키트는 텍스트 상자를 확장 하는 `FilteredTextBox` 컨트롤을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8cae-113">The ASP.NET AJAX Control Toolkit contains the `FilteredTextBox` control which extends a text box.</span></span> <span data-ttu-id="f8cae-114">활성화 된 후에는 특정 문자 집합만 필드에 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8cae-114">Once activated, only a certain set of characters may be entered into the field.</span></span>

<span data-ttu-id="f8cae-115">이 작업을 수행 하려면 먼저 ASP.NET AJAX 컨트롤 Toolkit 에서도 사용 되는 JavaScript 라이브러리를 로드 하는 ASP.NET AJAX `ScriptManager` 일반적으로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8cae-115">For this to work, we first need as usual the ASP.NET AJAX `ScriptManager` which loads the JavaScript libraries which are also used by the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample1.aspx)]

<span data-ttu-id="f8cae-116">그런 다음 텍스트 상자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8cae-116">Then, we need a text box:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample2.aspx)]

<span data-ttu-id="f8cae-117">마지막으로, `FilteredTextBoxExtender` 컨트롤은 사용자가 입력할 수 있는 문자를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8cae-117">Finally, the `FilteredTextBoxExtender` control takes care of restricting the characters the user is allowed to type.</span></span> <span data-ttu-id="f8cae-118">먼저 `TargetControlID` 특성을 `TextBox` 컨트롤의 `ID` 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8cae-118">First, set the `TargetControlID` attribute to the `ID` of the `TextBox` control.</span></span> <span data-ttu-id="f8cae-119">그런 다음 사용 가능한 `FilterType` 값 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8cae-119">Then, choose one of the available `FilterType` values:</span></span>

- <span data-ttu-id="f8cae-120">`Custom` 기본값 유효한 문자 목록을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8cae-120">`Custom` default; you have to provide a list of valid chars</span></span>
- <span data-ttu-id="f8cae-121">`LowercaseLetters` 소문자만</span><span class="sxs-lookup"><span data-stu-id="f8cae-121">`LowercaseLetters` lowercase letters only</span></span>
- <span data-ttu-id="f8cae-122">`Numbers` 숫자만</span><span class="sxs-lookup"><span data-stu-id="f8cae-122">`Numbers` digits only</span></span>
- <span data-ttu-id="f8cae-123">대문자 `UppercaseLetters`</span><span class="sxs-lookup"><span data-stu-id="f8cae-123">`UppercaseLetters` uppercase letters only</span></span>

<span data-ttu-id="f8cae-124">`Custom FilterType`를 사용 하는 경우 `ValidChars` 속성을 설정 하 고 입력 될 수 있는 문자 목록을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8cae-124">If the `Custom FilterType` is used, the `ValidChars` property must be set and provide a list of characters that may be typed.</span></span> <span data-ttu-id="f8cae-125">텍스트 상자에 텍스트를 붙여 넣으려고 하면 잘못 된 모든 문자가 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8cae-125">By the way: if you try to paste text into the text box, all invalid chars are removed.</span></span>

<span data-ttu-id="f8cae-126">숫자만 허용 하는 `FilteredTextBoxExtender` 컨트롤에 대 한 태그는 다음과 같습니다 (`FilterType="Numbers"`에서도 가능한 항목).</span><span class="sxs-lookup"><span data-stu-id="f8cae-126">Here is the markup for the `FilteredTextBoxExtender` control that only allows digits (something that would also have been possible with `FilterType="Numbers"`):</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample3.aspx)]

<span data-ttu-id="f8cae-127">페이지를 실행 하 고 JavaScript를 사용 하는 경우 문자를 입력 하 여 작업을 수행 하지 않습니다. 그러나 숫자는 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8cae-127">Run the page and try to enter a letter if JavaScript is enabled, it will not work; digits however appear on the page.</span></span> <span data-ttu-id="f8cae-128">그러나 제공 되는 보호 `FilteredTextBox`는 글머리 기호가 아닙니다. JavaScript를 사용 하는 경우 텍스트 상자에 데이터를 입력할 수 있으므로 추가 유효성 검사 (예: ASP)를 사용 해야 합니다. NET의 유효성 검사 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="f8cae-128">However note that the protection `FilteredTextBox` provides is not bullet-proof: If JavaScript is enabled, any data may be entered in the text box, so you have to use additional validation means, i.e. ASP.NET's validation controls.</span></span>

<span data-ttu-id="f8cae-129">[![숫자만 입력할 수 있습니다.](allowing-only-certain-characters-in-a-text-box-cs/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f8cae-129">[![Only digits may be entered](allowing-only-certain-characters-in-a-text-box-cs/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-cs/_static/image1.png)</span></span>

<span data-ttu-id="f8cae-130">숫자만 입력할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](allowing-only-certain-characters-in-a-text-box-cs/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="f8cae-130">Only digits may be entered ([Click to view full-size image](allowing-only-certain-characters-in-a-text-box-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="f8cae-131">다음</span><span class="sxs-lookup"><span data-stu-id="f8cae-131">Next</span></span>](allowing-only-certain-characters-in-a-text-box-vb.md)
