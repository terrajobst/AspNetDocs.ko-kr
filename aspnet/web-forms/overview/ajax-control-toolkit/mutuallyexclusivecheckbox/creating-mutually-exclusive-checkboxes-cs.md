---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-cs
title: 상호 배타적인 확인란 만들기 (C#) | Microsoft Docs
author: wenz
description: 옵션 집합 중 하나만 선택할 수 있는 경우 라디오 단추가 일반적으로 사용 됩니다. 그러나 그룹에서 하나의 라디오 단추를 선택 하면 단점이 있습니다,...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 8e11b813-ba0d-4c29-b0f8-f65db6dbef1e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-cs
msc.type: authoredcontent
ms.openlocfilehash: ddc154601752cc856f00dd4f3207952ab7e0e3e0
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606529"
---
# <a name="creating-mutually-exclusive-checkboxes-c"></a><span data-ttu-id="b9e59-104">상호 배타적인 확인란 만들기(C#)</span><span class="sxs-lookup"><span data-stu-id="b9e59-104">Creating Mutually Exclusive Checkboxes (C#)</span></span>

<span data-ttu-id="b9e59-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="b9e59-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="b9e59-106">[코드 다운로드](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="b9e59-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0CS.pdf)</span></span>

> <span data-ttu-id="b9e59-107">옵션 집합 중 하나만 선택할 수 있는 경우 라디오 단추가 일반적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9e59-107">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="b9e59-108">하지만 그룹에서 하나의 라디오 단추를 선택한 후에는 모든 라디오 단추를 선택 취소할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b9e59-108">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="b9e59-109">확인란은 언제 든 지 선택 취소할 수 있지만 함께 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b9e59-109">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="b9e59-110">이 자습서에서는 두 가지 방법, 즉 함께 사용할 수 없는 확인란을 모두 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9e59-110">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>

## <a name="overview"></a><span data-ttu-id="b9e59-111">개요</span><span class="sxs-lookup"><span data-stu-id="b9e59-111">Overview</span></span>

<span data-ttu-id="b9e59-112">옵션 집합 중 하나만 선택할 수 있는 경우 라디오 단추가 일반적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9e59-112">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="b9e59-113">하지만 그룹에서 하나의 라디오 단추를 선택한 후에는 모든 라디오 단추를 선택 취소할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b9e59-113">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="b9e59-114">확인란은 언제 든 지 선택 취소할 수 있지만 함께 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b9e59-114">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="b9e59-115">이 자습서에서는 두 가지 방법, 즉 함께 사용할 수 없는 확인란을 모두 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9e59-115">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>

## <a name="steps"></a><span data-ttu-id="b9e59-116">단계</span><span class="sxs-lookup"><span data-stu-id="b9e59-116">Steps</span></span>

<span data-ttu-id="b9e59-117">ASP.NET AJAX 컨트롤 도구 키트는 MutuallyExclusiveCheckBox extender를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9e59-117">The ASP.NET AJAX Control Toolkit contains the MutuallyExclusiveCheckBox extender.</span></span> <span data-ttu-id="b9e59-118">이를 통해 프로그래머는 모든 확인란을 그룹 이름 (`Key` 특성)에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9e59-118">This enables programmers to assign any checkbox to a group name (`Key` attribute).</span></span> <span data-ttu-id="b9e59-119">동일한 그룹 내의 모든 확인란은 한 번에 하나만 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9e59-119">From all check boxes within the same group, only one may be selected at one time.</span></span>

<span data-ttu-id="b9e59-120">새 ASP.NET 페이지에 두 개의 확인란을 추가 하는 것부터 시작 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b9e59-120">Let's start with putting two check boxes on a new ASP.NET page.</span></span> <span data-ttu-id="b9e59-121">더 많은 작업을 수행할 수 있지만 두 가지 모두 원칙을 보여 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9e59-121">There can be more, but two of them suffice to demonstrate the principle:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample1.aspx)]

<span data-ttu-id="b9e59-122">두 확인란 모두 MutuallyExclusiveCheckBoxExtender 컨트롤을 페이지에 배치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9e59-122">For both checkboxes, a MutuallyExclusiveCheckBoxExtender control must be put on the page.</span></span> <span data-ttu-id="b9e59-123">HTML 라디오 단추 요소의 값 특성이 자신이 속한 그룹을 표시 하는 것과 동일한 경우 두 키 특성의 값은 동일 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9e59-123">Both Key attributes need to have the same value, just as the value attributes of HTML radio button elements must be identical to denote the group they belong to.</span></span> <span data-ttu-id="b9e59-124">Extender의 TargetControlID 속성은 확인란의 ID를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="b9e59-124">The TargetControlID property of the extender points to the ID of the check box.</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample2.aspx)]

<span data-ttu-id="b9e59-125">마지막으로 ASP.NET AJAX 컨트롤 Toolkit의 모든 요소에 필요한 ASP.NET AJAX `ScriptManager`를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9e59-125">Finally, include the ASP.NET AJAX `ScriptManager` which is required by all elements of the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample3.aspx)]

<span data-ttu-id="b9e59-126">페이지를 저장 하 고 실행 합니다. 확인란을 선택 하 고 선택 취소할 수 있지만 두 확인란을 모두 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9e59-126">Save and run the page: You can check and uncheck both check boxes, however at no time can both check boxes be checked.</span></span>

<span data-ttu-id="b9e59-127">[한 번에 하나의 확인란을 확인할 수 ![.](creating-mutually-exclusive-checkboxes-cs/_static/image2.png)](creating-mutually-exclusive-checkboxes-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b9e59-127">[![Only one checkbox can be checked at a time](creating-mutually-exclusive-checkboxes-cs/_static/image2.png)](creating-mutually-exclusive-checkboxes-cs/_static/image1.png)</span></span>

<span data-ttu-id="b9e59-128">한 번에 하나의 확인란만 확인할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](creating-mutually-exclusive-checkboxes-cs/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="b9e59-128">Only one checkbox can be checked at a time ([Click to view full-size image](creating-mutually-exclusive-checkboxes-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="b9e59-129">다음</span><span class="sxs-lookup"><span data-stu-id="b9e59-129">Next</span></span>](creating-mutually-exclusive-checkboxes-vb.md)
