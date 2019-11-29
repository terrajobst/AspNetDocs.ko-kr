---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
title: 암호 강도 테스트 (C#) | Microsoft Docs
author: wenz
description: 암호는 거의 모든 위치에서 필요 하므로 지연 사용자가 쉽게 중단할 수 있는 간단한 암호를 선택 하는 경향이 있습니다. ASP의 PasswordStrength 컨트롤입니다. N ...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: cb4afbae-9b8f-483d-9729-476d4b9f85fc
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
msc.type: authoredcontent
ms.openlocfilehash: e55eab9feebc18f39dd40c59cfb423208296b6c5
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598840"
---
# <a name="testing-the-strength-of-a-password-c"></a><span data-ttu-id="05493-104">암호 강도 테스트(C#)</span><span class="sxs-lookup"><span data-stu-id="05493-104">Testing the Strength of a Password (C#)</span></span>

<span data-ttu-id="05493-105">[Christian Wenz](https://github.com/wenz) 별</span><span class="sxs-lookup"><span data-stu-id="05493-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="05493-106">[코드 다운로드](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="05493-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.cs.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0CS.pdf)</span></span>

> <span data-ttu-id="05493-107">암호는 거의 모든 위치에서 필요 하므로 지연 사용자가 쉽게 중단할 수 있는 간단한 암호를 선택 하는 경향이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05493-107">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="05493-108">ASP.NET AJAX 컨트롤 도구 키트의 PasswordStrength 컨트롤은 암호의 정상적인 정도를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05493-108">The PasswordStrength control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>

## <a name="overview"></a><span data-ttu-id="05493-109">개요</span><span class="sxs-lookup"><span data-stu-id="05493-109">Overview</span></span>

<span data-ttu-id="05493-110">암호는 거의 모든 위치에서 필요 하므로 지연 사용자가 쉽게 중단할 수 있는 간단한 암호를 선택 하는 경향이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05493-110">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="05493-111">ASP.NET AJAX 컨트롤 도구 키트의 `PasswordStrength` 컨트롤은 암호의 정상적인 정도를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05493-111">The `PasswordStrength` control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>

## <a name="steps"></a><span data-ttu-id="05493-112">단계</span><span class="sxs-lookup"><span data-stu-id="05493-112">Steps</span></span>

<span data-ttu-id="05493-113">`PasswordStrength` 컨트롤은 입력란을 확장 하 고 암호가 충분 한지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="05493-113">The `PasswordStrength` control extends a text box and checks whether the password in it is good enough.</span></span> <span data-ttu-id="05493-114">특성을 통해 다양 한 옵션을 제공 합니다. 다음은 몇 가지 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="05493-114">It offers a wealth of options via attributes; here are just some of them:</span></span>

- <span data-ttu-id="05493-115">암호에 필요한 최소 숫자 문자 수를 `MinimumNumericCharacters` 합니다.</span><span class="sxs-lookup"><span data-stu-id="05493-115">`MinimumNumericCharacters` minimum number of numeric characters required in the password</span></span>
- <span data-ttu-id="05493-116">암호에 필요한 최소 기호 문자 수 (문자와 숫자 아님) `MinimumSymbolCharacters`</span><span class="sxs-lookup"><span data-stu-id="05493-116">`MinimumSymbolCharacters` minimum number of symbol characters (not letters and digits) required in the password</span></span>
- <span data-ttu-id="05493-117">암호의 최소 길이를 `PreferredPasswordLength` 합니다.</span><span class="sxs-lookup"><span data-stu-id="05493-117">`PreferredPasswordLength` minimum length of the password</span></span>
- <span data-ttu-id="05493-118">암호에서 대 문자와 소문자를 모두 사용 해야 하는지 여부를 `RequiresUpperAndLowerCaseCharacters` 합니다.</span><span class="sxs-lookup"><span data-stu-id="05493-118">`RequiresUpperAndLowerCaseCharacters` whether the password needs to use both uppercase and lowercase characters</span></span>

<span data-ttu-id="05493-119">`StrengthIndicatorType`는 암호의 강도를 텍스트 (값 `"Text"`) 또는 종류의 진행률 표시줄 (값 `"BarIndicator"`)으로 표시 하는 방법에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="05493-119">The `StrengthIndicatorType` provides the information how to present the strength of the password, as text (value `"Text"`) or as a kind of progress bar (value `"BarIndicator"`).</span></span> <span data-ttu-id="05493-120">`DisplayPosition` 특성에서 정보가 표시 되는 위치를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="05493-120">In the `DisplayPosition` attribute, you configure where the information appears.</span></span> <span data-ttu-id="05493-121">다음은 사용자가 암호를 입력할 수 있는 텍스트 상자와 ASP.NET AJAX `ScriptManager` 컨트롤, `PasswordStrength` 컨트롤을 포함 하는 전체 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="05493-121">Here is a complete example, including the ASP.NET AJAX `ScriptManager` control, the `PasswordStrength` control and of course a text box where the user may enter a password.</span></span> <span data-ttu-id="05493-122">데모용으로, 후자 양식 필드는 암호 필드가 아니라 일반 텍스트 필드 이며, 입력 하는 항목을 개발 하는 동안 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05493-122">For the sake of demonstration, the latter form field is a regular text field and not a password field so that you can see during development what you are typing.</span></span>

[!code-aspx[Main](testing-the-strength-of-a-password-cs/samples/sample1.aspx)]

<span data-ttu-id="05493-123">페이지를 실행 하 고 입력: 소문자, 대문자, 숫자 및 기호를 입력 한 후에만 암호를 unbreakable로 간주 합니다.</span><span class="sxs-lookup"><span data-stu-id="05493-123">Run the page and type away: Only after you have entered lowercase letters, uppercase letters, digits and symbols, the password is deemed as unbreakable .</span></span>

<span data-ttu-id="05493-124">[이제 ![암호가 양호 합니다.](testing-the-strength-of-a-password-cs/_static/image2.png)](testing-the-strength-of-a-password-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="05493-124">[![Now the password is (quite) good](testing-the-strength-of-a-password-cs/_static/image2.png)](testing-the-strength-of-a-password-cs/_static/image1.png)</span></span>

<span data-ttu-id="05493-125">이제 암호가 매우 양호 합니다 ([전체 크기 이미지를 보려면 클릭](testing-the-strength-of-a-password-cs/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="05493-125">Now the password is (quite) good ([Click to view full-size image](testing-the-strength-of-a-password-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="05493-126">다음</span><span class="sxs-lookup"><span data-stu-id="05493-126">Next</span></span>](testing-the-strength-of-a-password-vb.md)
