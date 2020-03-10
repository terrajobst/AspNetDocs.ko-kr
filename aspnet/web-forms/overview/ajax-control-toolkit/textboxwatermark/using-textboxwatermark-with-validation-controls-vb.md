---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-vb
title: 유효성 검사 컨트롤에 TextBoxWatermark 사용 (VB) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 TextBoxWatermark 컨트롤은 입력란 내에 텍스트가 표시 되도록 텍스트 상자를 확장 합니다. 사용자가 상자를 클릭 하면 ...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e6c2cb98-f745-4bc8-973a-813879c8a891
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 141cae26c9e52be510e2a5a8f816cbac977dcf3d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78508751"
---
# <a name="using-textboxwatermark-with-validation-controls-vb"></a><span data-ttu-id="76e5f-104">유효성 검사 컨트롤에 TextBoxWatermark 사용(VB)</span><span class="sxs-lookup"><span data-stu-id="76e5f-104">Using TextBoxWatermark With Validation Controls (VB)</span></span>

<span data-ttu-id="76e5f-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="76e5f-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="76e5f-106">[코드 다운로드](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="76e5f-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2VB.pdf)</span></span>

> <span data-ttu-id="76e5f-107">AJAX 컨트롤 도구 키트의 TextBoxWatermark 컨트롤은 입력란 내에 텍스트가 표시 되도록 텍스트 상자를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="76e5f-107">The TextBoxWatermark control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="76e5f-108">사용자가 상자를 클릭 하면 해당 상자가 비워집니다.</span><span class="sxs-lookup"><span data-stu-id="76e5f-108">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="76e5f-109">사용자가 텍스트를 입력 하지 않고 상자를 벗어나면 미리 채워진 텍스트가 다시 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="76e5f-109">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="76e5f-110">이는 동일한 페이지에서 ASP.NET 유효성 검사 컨트롤과 충돌할 수 있지만 이러한 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76e5f-110">This may collide with ASP.NET Validation Controls on the same page, but these issues may be overcome.</span></span>

## <a name="overview"></a><span data-ttu-id="76e5f-111">개요</span><span class="sxs-lookup"><span data-stu-id="76e5f-111">Overview</span></span>

<span data-ttu-id="76e5f-112">AJAX 컨트롤 도구 키트의 `TextBoxWatermark` 컨트롤은 입력란 내에 텍스트가 표시 되도록 텍스트 상자를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="76e5f-112">The `TextBoxWatermark` control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="76e5f-113">사용자가 상자를 클릭 하면 해당 상자가 비워집니다.</span><span class="sxs-lookup"><span data-stu-id="76e5f-113">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="76e5f-114">사용자가 텍스트를 입력 하지 않고 상자를 벗어나면 미리 채워진 텍스트가 다시 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="76e5f-114">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="76e5f-115">이는 동일한 페이지에서 ASP.NET 유효성 검사 컨트롤과 충돌할 수 있지만 이러한 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76e5f-115">This may collide with ASP.NET Validation Controls on the same page, but these issues may be overcome.</span></span>

## <a name="steps"></a><span data-ttu-id="76e5f-116">단계</span><span class="sxs-lookup"><span data-stu-id="76e5f-116">Steps</span></span>

<span data-ttu-id="76e5f-117">샘플의 기본 설정은 다음과 같습니다. `TextBox` 컨트롤은 `TextBoxWatermarkExtender` 컨트롤을 사용 하 여 워터 마크 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76e5f-117">The basic setup of the sample is the following: a `TextBox` control is watermarked using a `TextBoxWatermarkExtender` control.</span></span> <span data-ttu-id="76e5f-118">단추는 포스트백을 트리거하고 나중에 페이지에서 유효성 검사 컨트롤을 트리거하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76e5f-118">A button triggers a postback and will later be used to trigger the validation controls on the page.</span></span> <span data-ttu-id="76e5f-119">또한 ASP.NET AJAX를 초기화 하려면 `ScriptManager` 컨트롤이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="76e5f-119">Also, a `ScriptManager` control is required to initialize ASP.NET AJAX:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample1.aspx)]

<span data-ttu-id="76e5f-120">이제 양식이 전송 될 때 필드에 텍스트가 있는지 여부를 확인 하는 `RequiredFieldValidator` 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="76e5f-120">Now add a `RequiredFieldValidator` control that checks whether there is text in the field when the form is submitted.</span></span> <span data-ttu-id="76e5f-121">유효성 검사기의 `InitialValue` 속성은 `TextBoxWatermarkExtender` 컨트롤에 사용 되는 것과 동일한 값으로 설정 해야 합니다. 폼이 제출 될 때 변경 되지 않은 텍스트 상자의 값은 그 안에 있는 워터 마크 값입니다.</span><span class="sxs-lookup"><span data-stu-id="76e5f-121">The `InitialValue` property of the validator must be set to the same value that is used in the `TextBoxWatermarkExtender` control: When the form is submitted, the value of an unchanged textbox is the watermark value within it:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample2.aspx)]

<span data-ttu-id="76e5f-122">그러나이 방법에는 한 가지 문제가 있습니다. 클라이언트가 JavaScript를 사용 하지 않도록 설정 하는 경우 텍스트 필드가 워터 마크 텍스트로 미리 채워지지 않으므로 `RequiredFieldValidator`는 오류 메시지를 트리거하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76e5f-122">However there is one problem with this approach: If the client disables JavaScript, the text field is not prefilled with the watermark text, therefore the `RequiredFieldValidator` does not trigger an error message.</span></span> <span data-ttu-id="76e5f-123">따라서 `InitialValue` 특성을 생략 하 고 빈 텍스트 상자를 확인 하는 두 번째 `RequiredFieldValidator` 컨트롤이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="76e5f-123">Therefore, a second `RequiredFieldValidator` control is required which checks for an empty text box (omitting the `InitialValue` attribute).</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample3.aspx)]

<span data-ttu-id="76e5f-124">두 유효성 검사기는 `Display`=`"Dynamic"`를 사용 하므로 최종 사용자는 두 가지 유효성 검사기의 시각적 모양을 구별할 수 없습니다. 그 중 하나만 있는 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="76e5f-124">Since both validators use `Display`=`"Dynamic"`, the end user cannot distinguish from the visual appearance which of the two validators was fired; instead, it looks like there was only one of them.</span></span>

<span data-ttu-id="76e5f-125">마지막으로, 유효성 검사기에서 오류 메시지를 발행 하지 않은 경우 필드의 텍스트를 출력 하는 서버 쪽 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="76e5f-125">Finally, add some server-side code to output the text in the field if no validator issued an error message:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-vb/samples/sample4.aspx)]

<span data-ttu-id="76e5f-126">[필드에 텍스트가 불만 유효성 검사기를 ![합니다.](using-textboxwatermark-with-validation-controls-vb/_static/image2.png)](using-textboxwatermark-with-validation-controls-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="76e5f-126">[![The validator complains that there is no text in the field](using-textboxwatermark-with-validation-controls-vb/_static/image2.png)](using-textboxwatermark-with-validation-controls-vb/_static/image1.png)</span></span>

<span data-ttu-id="76e5f-127">유효성 검사기에서 필드에 텍스트가 불만 ([전체 크기 이미지를 보려면 클릭](using-textboxwatermark-with-validation-controls-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="76e5f-127">The validator complains that there is no text in the field ([Click to view full-size image](using-textboxwatermark-with-validation-controls-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="76e5f-128">이전</span><span class="sxs-lookup"><span data-stu-id="76e5f-128">Previous</span></span>](using-textboxwatermark-in-a-formview-vb.md)
