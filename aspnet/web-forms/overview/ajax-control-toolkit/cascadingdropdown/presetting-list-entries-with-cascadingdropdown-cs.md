---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-cs
title: 미리 설정 목록 항목 CascadingDropDown (C#) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 CascadingDropDown 컨트롤은 dropdownlist 컨트롤을 확장 하 여 한 DropDownList의 변경 내용이 anoth에 연결 된 값을 로드 하도록 합니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 04c79748-0f21-4a3b-aba5-e1ce3161c32e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: 3bb4a51092534e6fddbd40f868c53c58d12eef2f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74574658"
---
# <a name="presetting-list-entries-with-cascadingdropdown-c"></a><span data-ttu-id="23509-103">CascadingDropDown으로 목록 항목 미리 설정(C#)</span><span class="sxs-lookup"><span data-stu-id="23509-103">Presetting List Entries with CascadingDropDown (C#)</span></span>

<span data-ttu-id="23509-104">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="23509-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="23509-105">[코드 다운로드](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingDropDown2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="23509-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingDropDown2CS.pdf)</span></span>

> <span data-ttu-id="23509-106">AJAX 컨트롤 도구 키트의 CascadingDropDown 컨트롤은 dropdownlist 컨트롤을 확장 하 여 한 DropDownList의 변경 내용이 다른 DropDownList의 관련 값을 로드 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="23509-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="23509-107">약간의 코드를 사용 하면 데이터가 동적으로 로드 된 후에 목록 요소가 미리 선택 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23509-107">With a little bit of code it is possible that a list element is preselected once the data has been dynamically loaded.</span></span>

## <a name="overview"></a><span data-ttu-id="23509-108">개요</span><span class="sxs-lookup"><span data-stu-id="23509-108">Overview</span></span>

<span data-ttu-id="23509-109">AJAX 컨트롤 도구 키트의 CascadingDropDown 컨트롤은 dropdownlist 컨트롤을 확장 하 여 한 DropDownList의 변경 내용이 다른 DropDownList의 관련 값을 로드 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="23509-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="23509-110">예를 들어, 한 목록에는 미국 주 목록이 제공 되며 다음 목록에는 해당 상태의 주 도시가 채워집니다. 약간의 코드를 사용 하면 데이터가 동적으로 로드 된 후에 목록 요소가 미리 선택 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23509-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) With a little bit of code it is possible that a list element is preselected once the data has been dynamically loaded.</span></span>

## <a name="steps"></a><span data-ttu-id="23509-111">단계</span><span class="sxs-lookup"><span data-stu-id="23509-111">Steps</span></span>

<span data-ttu-id="23509-112">ASP.NET AJAX 및 Control Toolkit의 기능을 활성화 하려면 페이지의 아무 곳에 나 `<form>` 요소 내에 `ScriptManager` 컨트롤을 배치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23509-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample1.aspx)]

<span data-ttu-id="23509-113">그런 다음, DropDownList 컨트롤이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="23509-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample2.aspx)]

<span data-ttu-id="23509-114">이 목록에 대해 웹 서비스 URL 및 메서드 정보를 제공 하는 CascadingDropDown extender가 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23509-114">For this list, a CascadingDropDown extender is added, providing web service URL and method information:</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample3.aspx)]

<span data-ttu-id="23509-115">그런 다음 CascadingDropDown extender는 다음 메서드 시그니처를 사용 하 여 웹 서비스를 비동기적으로 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="23509-115">The CascadingDropDown extender then asynchronously calls a web service with the following method signature:</span></span>

[!code-csharp[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample4.cs)]

<span data-ttu-id="23509-116">메서드는 CascadingDropDown value 형식의 배열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="23509-116">The method returns an array of type CascadingDropDown value.</span></span> <span data-ttu-id="23509-117">형식의 생성자는 먼저 목록 항목의 캡션과 값 (HTML `value` 특성)을 먼저 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="23509-117">The type's constructor expects first the list entry's caption and then the value (HTML `value` attribute).</span></span> <span data-ttu-id="23509-118">세 번째 인수를 true로 설정 하면 목록 요소가 브라우저에서 자동으로 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23509-118">If the third argument is set to true, the list element is automatically selected in the browser.</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample5.aspx)]

<span data-ttu-id="23509-119">브라우저에서 페이지를 로드 하면 세 공급 업체가 세 번째로 미리 선택 된 상태로 드롭다운 목록을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="23509-119">Loading the page in the browser will fill the dropdown list with three vendors, the second one being preselected.</span></span>

<span data-ttu-id="23509-120">[목록이 채워지고 자동으로 미리 선택 된 ![](presetting-list-entries-with-cascadingdropdown-cs/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="23509-120">[![The list is filled and preselected automatically](presetting-list-entries-with-cascadingdropdown-cs/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-cs/_static/image1.png)</span></span>

<span data-ttu-id="23509-121">목록이 자동으로 채워지고 미리 선택 됩니다 ([전체 크기 이미지를 보려면 클릭](presetting-list-entries-with-cascadingdropdown-cs/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="23509-121">The list is filled and preselected automatically ([Click to view full-size image](presetting-list-entries-with-cascadingdropdown-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="23509-122">[이전](using-cascadingdropdown-with-a-database-cs.md)
> [다음](using-auto-postback-with-cascadingdropdown-cs.md)</span><span class="sxs-lookup"><span data-stu-id="23509-122">[Previous](using-cascadingdropdown-with-a-database-cs.md)
[Next](using-auto-postback-with-cascadingdropdown-cs.md)</span></span>
