---
uid: web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
title: ASP.NET 웹 페이지 (Razor) 사이트에서 사용자 입력 유효성 검사 | Microsoft Docs
author: Rick-Anderson
description: 이 문서에서는 사용자에 게 제공 되는 &mdash; 정보를 확인 하는 방법에 대해 설명 합니다. 즉, 사용자가의 HTML 양식에 올바른 정보를 입력 하는 것을 확인 하려면 ...
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 4eb060cc-cf14-41ae-bab1-14a2c15332d0
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: e6f8e1051d09d11f1756bfada44a73ba7c2a1db2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454301"
---
# <a name="validating-user-input-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="40c43-103">ASP.NET 웹 페이지 (Razor) 사이트에서 사용자 입력 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="40c43-103">Validating User Input in ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="40c43-104">만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="40c43-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="40c43-105">이 문서에서는 사용자가 &mdash; 하는 정보를 확인 하는 방법에 대해 설명 합니다. 즉, 사용자가 Razor (ASP.NET 웹 페이지) 사이트의 HTML 양식으로 유효한 정보를 입력 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-105">This article discusses how to validate information you get from users &mdash; that is, to make sure that users enter valid information in HTML forms in an ASP.NET Web Pages (Razor) site.</span></span>
> 
> <span data-ttu-id="40c43-106">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="40c43-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="40c43-107">사용자의 입력이 정의 하는 유효성 검사 조건과 일치 하는지 확인 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-107">How to check that a user's input matches validation criteria that you define.</span></span>
> - <span data-ttu-id="40c43-108">모든 유효성 검사 테스트가 통과 했는지 여부를 확인 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-108">How to determine whether all validation tests have passed.</span></span>
> - <span data-ttu-id="40c43-109">유효성 검사 오류를 표시 하는 방법 및 형식을 지정 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-109">How to display validation errors (and how to format them).</span></span>
> - <span data-ttu-id="40c43-110">사용자에 게 직접 제공 되지 않는 데이터의 유효성을 검사 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-110">How to validate data that doesn't come directly from users.</span></span>
> 
> <span data-ttu-id="40c43-111">다음은이 문서에서 소개 하는 ASP.NET 프로그래밍 개념입니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-111">These are the ASP.NET programming concepts introduced in the article:</span></span>
> 
> - <span data-ttu-id="40c43-112">`Validation` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-112">The `Validation` helper.</span></span>
> - <span data-ttu-id="40c43-113">`Html.ValidationSummary` 및 `Html.ValidationMessage` 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-113">The `Html.ValidationSummary` and `Html.ValidationMessage` methods.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="40c43-114">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="40c43-114">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="40c43-115">ASP.NET 웹 페이지 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="40c43-115">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="40c43-116">이 자습서는 ASP.NET 웹 페이지 2 에서도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-116">This tutorial also works with ASP.NET Web Pages 2.</span></span>

<span data-ttu-id="40c43-117">이 문서에는 다음과 같은 섹션이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-117">This article contains the following sections:</span></span>

- [<span data-ttu-id="40c43-118">사용자 입력 유효성 검사 개요</span><span class="sxs-lookup"><span data-stu-id="40c43-118">Overview of User Input Validation</span></span>](#Overview_of_User_Input_Validation)
- [<span data-ttu-id="40c43-119">사용자 입력 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="40c43-119">Validating User Input</span></span>](#Validating_User_Input)
- [<span data-ttu-id="40c43-120">클라이언트 쪽 유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="40c43-120">Adding Client-Side Validation</span></span>](#Adding_Client-Side_Validation)
- [<span data-ttu-id="40c43-121">유효성 검사 오류 서식 지정</span><span class="sxs-lookup"><span data-stu-id="40c43-121">Formatting Validation Errors</span></span>](#Formatting_Validation_Errors)
- [<span data-ttu-id="40c43-122">사용자에 게 직접 제공 되지 않는 데이터 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="40c43-122">Validating Data That Doesn't Come Directly from Users</span></span>](#Validating_Data_That_Doesnt_Come_Directly_from_Users)

<a id="Overview_of_User_Input_Validation"></a>
## <a name="overview-of-user-input-validation"></a><span data-ttu-id="40c43-123">사용자 입력 유효성 검사 개요</span><span class="sxs-lookup"><span data-stu-id="40c43-123">Overview of User Input Validation</span></span>

<span data-ttu-id="40c43-124">사용자에 게 페이지에 정보를 입력 하도록 요청 하는 경우 (예: 양식) 입력 하는 값이 유효한 지 확인 하는 것이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-124">If you ask users to enter information in a page — for example, into a form — it's important to make sure that the values that they enter are valid.</span></span> <span data-ttu-id="40c43-125">예를 들어 중요 한 정보가 없는 폼을 처리 하지 않으려는 경우</span><span class="sxs-lookup"><span data-stu-id="40c43-125">For example, you don't want to process a form that's missing critical information.</span></span>

<span data-ttu-id="40c43-126">사용자가 HTML 양식에 값을 입력 하는 경우 입력 하는 값은 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-126">When users enter values into an HTML form, the values that they enter are strings.</span></span> <span data-ttu-id="40c43-127">많은 경우에 필요한 값은 정수 또는 날짜와 같은 다른 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-127">In many cases, the values you need are some other data types, like integers or dates.</span></span> <span data-ttu-id="40c43-128">따라서 사용자가 입력 하는 값을 적절 한 데이터 형식으로 올바르게 변환할 수 있는지도 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-128">Therefore, you also have to make sure that the values that users enter can be correctly converted to the appropriate data types.</span></span>

<span data-ttu-id="40c43-129">값에 대 한 특정 제한이 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-129">You might also have certain restrictions on the values.</span></span> <span data-ttu-id="40c43-130">예를 들어 사용자가 정수를 올바르게 입력 하는 경우에도 값이 특정 범위 내에 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-130">Even if users correctly enter an integer, for example, you might need to make sure that the value falls within a certain range.</span></span>

![CSS 스타일 클래스를 사용 하는 유효성 검사 오류](validating-user-input-in-aspnet-web-pages-sites/_static/image1.png)

> [!NOTE] 
> 
> <span data-ttu-id="40c43-132">**중요** 사용자 입력의 유효성을 검사 하는 것도 보안을 위해 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-132">**Important** Validating user input is also important for security.</span></span> <span data-ttu-id="40c43-133">사용자가 양식에 입력할 수 있는 값을 제한 하는 경우 사용자가 사이트의 보안을 손상 시킬 수 있는 값을 입력할 수 있는 기회가 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-133">When you restrict the values that users can enter in forms, you reduce the chance that someone can enter a value that can compromise the security of your site.</span></span>

<a id="Validating_User_Input"></a>
## <a name="validating-user-input"></a><span data-ttu-id="40c43-134">사용자 입력 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="40c43-134">Validating User Input</span></span>

<span data-ttu-id="40c43-135">ASP.NET 웹 페이지 2에서는 `Validator` 도우미를 사용 하 여 사용자 입력을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-135">In ASP.NET Web Pages 2, you can use the `Validator` helper to test user input.</span></span> <span data-ttu-id="40c43-136">기본적인 방법은 다음을 수행 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-136">The basic approach is to do the following:</span></span>

1. <span data-ttu-id="40c43-137">유효성을 검사할 입력 요소 (필드)를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-137">Determine which input elements (fields) you want to validate.</span></span>

    <span data-ttu-id="40c43-138">일반적으로 폼의 `<input>` 요소에 있는 값의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-138">You typically validate values in `<input>` elements in a form.</span></span> <span data-ttu-id="40c43-139">그러나 `<select>` 목록과 같이 제한 된 요소에서 제공 되는 입력을 비롯 하 여 모든 입력의 유효성을 검사 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-139">However, it's a good practice to validate all input, even input that comes from a constrained element like a `<select>` list.</span></span> <span data-ttu-id="40c43-140">이렇게 하면 사용자가 페이지에서 컨트롤을 우회 하 고 양식을 전송 하지 않도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-140">This helps to make sure that users don't bypass the controls on a page and submit a form.</span></span>
2. <span data-ttu-id="40c43-141">페이지 코드에서 `Validation` 도우미의 메서드를 사용 하 여 각 입력 요소에 대 한 개별 유효성 검사를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-141">In the page code, add individual validation checks for each input element by using methods of the `Validation` helper.</span></span>

    <span data-ttu-id="40c43-142">필수 필드를 확인 하려면 `Validation.RequireField(field, [error message])` (개별 필드의 경우) 또는 `Validation.RequireFields(field1, field2, ...))` (필드 목록의 경우)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-142">To check for required fields, use `Validation.RequireField(field, [error message])` (for an individual field) or `Validation.RequireFields(field1, field2, ...))` (for a list of fields).</span></span> <span data-ttu-id="40c43-143">다른 형식의 유효성 검사를 수행 하려면 `Validation.Add(field, ValidationType)`을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-143">For other types of validation, use `Validation.Add(field, ValidationType)`.</span></span> <span data-ttu-id="40c43-144">`ValidationType`의 경우 다음 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-144">For `ValidationType`, you can use these options:</span></span>

    `Validator.DateTime ([error message])`  
   `Validator.Decimal([error message])`  
   `Validator.EqualsTo(otherField [, error message])`  
   `Validator.Float([error message])`  
   `Validator.Integer([error message])`  
   `Validator.Range(min, max [, error message])`  
   `Validator.RegEx(pattern [, error message])`  
   `Validator.Required([error message])`  
   `Validator.StringLength(length)`  
   `Validator.Url([error message])`
3. <span data-ttu-id="40c43-145">페이지가 제출 되 면 유효성 검사를 `Validation.IsValid`확인 하 여 통과 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-145">When the page is submitted, check whether validation has passed by checking `Validation.IsValid`:</span></span>

    [!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample1.cs)]

    <span data-ttu-id="40c43-146">유효성 검사 오류가 있는 경우 일반 페이지 처리를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-146">If there are any validation errors, you skip normal page processing.</span></span> <span data-ttu-id="40c43-147">예를 들어, 페이지의 목적이 데이터베이스를 업데이트 하는 경우 모든 유효성 검사 오류가 해결 될 때까지이 작업을 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-147">For example, if the purpose of the page is to update a database, you don't do that until all validation errors have been fixed.</span></span>
4. <span data-ttu-id="40c43-148">유효성 검사 오류가 있는 경우 `Html.ValidationSummary` 또는 `Html.ValidationMessage`또는 둘 다를 사용 하 여 페이지의 태그에 오류 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-148">If there are validation errors, display error messages in the page's markup by using `Html.ValidationSummary` or `Html.ValidationMessage`, or both.</span></span>

<span data-ttu-id="40c43-149">다음 예에서는 이러한 단계를 보여 주는 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-149">The following example shows a page that illustrates these steps.</span></span>

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample2.cshtml)]

<span data-ttu-id="40c43-150">유효성 검사가 작동 하는 방식을 확인 하려면이 페이지를 실행 하 고 의도적으로 실수를 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-150">To see how validation works, run this page and deliberately make mistakes.</span></span> <span data-ttu-id="40c43-151">예를 들어 강좌 이름을 입력 하 고,를 입력 하 고, 잘못 된 날짜를 입력 하는 경우 페이지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-151">For example, here's what the page looks like if you forget to enter a course name, if you enter an, and if you enter an invalid date:</span></span>

![렌더링 된 페이지의 유효성 검사 오류](validating-user-input-in-aspnet-web-pages-sites/_static/image2.png)

<a id="Adding_Client-Side_Validation"></a>
## <a name="adding-client-side-validation"></a><span data-ttu-id="40c43-153">클라이언트측 유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="40c43-153">Adding Client-Side Validation</span></span>

<span data-ttu-id="40c43-154">기본적으로 사용자 입력은 사용자가 페이지를 전송한 후 유효성 검사가 수행 됩니다. 즉, 서버 코드에서 유효성 검사가 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-154">By default, user input is validated after users submit the page — that is, the validation is performed in server code.</span></span> <span data-ttu-id="40c43-155">이 방법의 단점은 사용자가 페이지를 제출할 때까지 오류가 발생 한 것을 사용자가 알지 못하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-155">A disadvantage of this approach is that users don't know that they've made an error until after they submit the page.</span></span> <span data-ttu-id="40c43-156">폼이 길거나 복잡 한 경우에는 사용자가 페이지를 전송한 후에만 오류를 보고 하는 것이 불편할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-156">If a form is long or complex, reporting errors only after the page is submitted can be inconvenient to the user.</span></span>

<span data-ttu-id="40c43-157">클라이언트 스크립트에서 유효성 검사를 수행 하는 지원을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-157">You can add support to perform validation in client script.</span></span> <span data-ttu-id="40c43-158">이 경우 사용자가 브라우저에서 작업할 때 유효성 검사가 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-158">In that case, the validation is performed as users work in the browser.</span></span> <span data-ttu-id="40c43-159">예를 들어 값을 정수로 지정 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-159">For example, suppose you specify that a value should be an integer.</span></span> <span data-ttu-id="40c43-160">사용자가 정수가 아닌 값을 입력 하는 경우 사용자가 입력 필드를 벗어나면 오류가 즉시 보고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-160">If a user enters a non-integer value, the error is reported as soon as the user leaves the entry field.</span></span> <span data-ttu-id="40c43-161">사용자는 즉각적인 피드백을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-161">Users get immediate feedback, which is convenient for them.</span></span> <span data-ttu-id="40c43-162">클라이언트 기반 유효성 검사를 사용 하면 사용자가 여러 오류를 수정 하기 위해 양식을 제출 해야 하는 횟수를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-162">Client-based validation can also reduce the number of times that the user has to submit the form to correct multiple errors.</span></span>

> [!NOTE]
> <span data-ttu-id="40c43-163">클라이언트 쪽 유효성 검사를 사용 하더라도 유효성 검사는 항상 서버 코드 에서도 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-163">Even if you use client-side validation, validation is always also performed in server code.</span></span> <span data-ttu-id="40c43-164">사용자가 클라이언트 기반 유효성 검사를 우회 하는 경우 서버 코드에서 유효성 검사를 수행 하는 것이 보안 조치입니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-164">Performing validation in server code is a security measure, in case users bypass client-based validation.</span></span>

1. <span data-ttu-id="40c43-165">페이지에 다음 JavaScript 라이브러리를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-165">Register the following JavaScript libraries in the page:</span></span>  

    [!code-html[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample3.html)]

   <span data-ttu-id="40c43-166">라이브러리 중 두 개는 CDN (content delivery network)에서 로드할 수 있으므로 컴퓨터 또는 서버에 반드시 있어야 하는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-166">Two of the libraries are loadable from a content delivery network (CDN), so you don't necessarily have to have them on your computer or server.</span></span> <span data-ttu-id="40c43-167">그러나 사용자에 게는 jquery의 로컬 복사본이 있어야 합니다 *.*</span><span class="sxs-lookup"><span data-stu-id="40c43-167">However, you must have a local copy of *jquery.validate.unobtrusive.js*.</span></span> <span data-ttu-id="40c43-168">라이브러리를 포함 하는 WebMatrix 템플릿 (예: **스타터 사이트** )을 아직 사용 하지 않는 경우 **스타터 사이트**를 기반으로 하는 웹 페이지 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-168">If you are not already working with a WebMatrix template (like **Starter Site** ) that includes the library, create a Web Pages site that's based on **Starter Site**.</span></span> <span data-ttu-id="40c43-169">그런 다음, *.js* 파일을 현재 사이트에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-169">Then copy the *.js* file to your current site.</span></span>
2. <span data-ttu-id="40c43-170">태그에서 유효성을 검사 하는 각 요소에 대해 `Validation.For(field)`에 대 한 호출을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-170">In markup, for each element that you're validating, add a call to `Validation.For(field)`.</span></span> <span data-ttu-id="40c43-171">이 메서드는 클라이언트 쪽 유효성 검사에 사용 되는 특성을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-171">This method emits attributes that are used by client-side validation.</span></span> <span data-ttu-id="40c43-172">메서드는 실제 JavaScript 코드를 내보내는 대신 `data-val-...`와 같은 특성을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-172">(Rather than emitting actual JavaScript code, the method emits attributes like `data-val-...`.</span></span> <span data-ttu-id="40c43-173">이러한 특성은 jQuery를 사용 하 여 작업을 수행 하는 클라이언트의 유효성 검사를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-173">These attributes support unobtrusive client validation that uses jQuery to do the work.)</span></span>

<span data-ttu-id="40c43-174">다음 페이지에서는 앞에 나온 예제에 클라이언트 유효성 검사 기능을 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-174">The following page shows how to add client validation features to the example shown earlier.</span></span>

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample4.cshtml?highlight=35-39,51,61,71)]

<span data-ttu-id="40c43-175">일부 유효성 검사는 클라이언트에서 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-175">Not all validation checks run on the client.</span></span> <span data-ttu-id="40c43-176">특히 데이터 형식 유효성 검사 (정수, 날짜 등)는 클라이언트에서 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-176">In particular, data-type validation (integer, date, and so on) don't run on the client.</span></span> <span data-ttu-id="40c43-177">클라이언트와 서버 모두에서 다음 검사를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-177">The following checks work on both the client and server:</span></span>

- `Required`
- `Range(minValue, maxValue)`
- `StringLength(maxLength[, minLength])`
- `Regex(pattern)`
- `EqualsTo(otherField)`

<span data-ttu-id="40c43-178">이 예제에서 유효한 날짜에 대 한 테스트는 클라이언트 코드에서 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-178">In this example, the test for a valid date won't work in client code.</span></span> <span data-ttu-id="40c43-179">그러나 테스트는 서버 코드에서 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-179">However, the test will be performed in server code.</span></span>

<a id="Formatting_Validation_Errors"></a>
## <a name="formatting-validation-errors"></a><span data-ttu-id="40c43-180">유효성 검사 오류 서식 지정</span><span class="sxs-lookup"><span data-stu-id="40c43-180">Formatting Validation Errors</span></span>

<span data-ttu-id="40c43-181">다음 예약 된 이름이 있는 CSS 클래스를 정의 하 여 유효성 검사 오류를 표시 하는 방법을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-181">You can control how validation errors are displayed by defining CSS classes that have the following reserved names:</span></span>

- <span data-ttu-id="40c43-182">`field-validation-error`입니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-182">`field-validation-error`.</span></span> <span data-ttu-id="40c43-183">오류가 표시 될 때 `Html.ValidationMessage` 메서드의 출력을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-183">Defines the output of the `Html.ValidationMessage` method when it's displaying an error.</span></span>
- <span data-ttu-id="40c43-184">`field-validation-valid`입니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-184">`field-validation-valid`.</span></span> <span data-ttu-id="40c43-185">오류가 없을 때 `Html.ValidationMessage` 메서드의 출력을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-185">Defines the output of the `Html.ValidationMessage` method when there is no error.</span></span>
- <span data-ttu-id="40c43-186">`input-validation-error`입니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-186">`input-validation-error`.</span></span> <span data-ttu-id="40c43-187">오류가 있을 때 `<input>` 요소가 렌더링 되는 방식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-187">Defines how `<input>` elements are rendered when there's an error.</span></span> <span data-ttu-id="40c43-188">예를 들어이 클래스를 사용 하 여 &lt;입력&gt; 요소의 배경색을 다른 색으로 설정할 수 있습니다 (해당 값이 유효 하지 않은 경우). 이 CSS 클래스는 클라이언트 유효성 검사 (ASP.NET 웹 페이지 2의 경우) 중에만 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-188">(For example, you can use this class to set the background color of an &lt;input&gt; element to a different color if its value is invalid.) This CSS class is used only during client validation (in ASP.NET Web Pages 2).</span></span>
- <span data-ttu-id="40c43-189">`input-validation-valid`입니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-189">`input-validation-valid`.</span></span> <span data-ttu-id="40c43-190">오류가 없을 때 `<input>` 요소의 모양을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-190">Defines the appearance of `<input>` elements when there is no error.</span></span>
- <span data-ttu-id="40c43-191">`validation-summary-errors`입니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-191">`validation-summary-errors`.</span></span> <span data-ttu-id="40c43-192">오류 목록을 표시 하는 `Html.ValidationSummary` 메서드의 출력을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-192">Defines the output of the `Html.ValidationSummary` method it's displaying a list of errors.</span></span>
- <span data-ttu-id="40c43-193">`validation-summary-valid`입니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-193">`validation-summary-valid`.</span></span> <span data-ttu-id="40c43-194">오류가 없을 때 `Html.ValidationSummary` 메서드의 출력을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-194">Defines the output of the `Html.ValidationSummary` method when there is no error.</span></span>

<span data-ttu-id="40c43-195">다음 `<style>` 블록에서는 오류 조건에 대 한 규칙을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-195">The following `<style>` block shows rules for error conditions.</span></span>

[!code-css[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample5.css)]

<span data-ttu-id="40c43-196">이 문서 앞부분의 예제 페이지에이 스타일 블록을 포함 하는 경우 오류 표시는 다음 그림과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-196">If you include this style block in the example pages from earlier in the article, the error display will look like the following illustration:</span></span>

![CSS 스타일 클래스를 사용 하는 유효성 검사 오류](validating-user-input-in-aspnet-web-pages-sites/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="40c43-198">ASP.NET 웹 페이지 2에서 클라이언트 유효성 검사를 사용 하지 않는 경우 `<input>` 요소에 대 한 CSS 클래스 (`input-validation-error` 및 `input-validation-valid`는 아무런 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-198">If you're not using client validation in ASP.NET Web Pages 2, the CSS classes for the `<input>` elements (`input-validation-error` and `input-validation-valid` don't have any effect.</span></span>

### <a name="static-and-dynamic-error-display"></a><span data-ttu-id="40c43-199">정적 및 동적 오류 표시</span><span class="sxs-lookup"><span data-stu-id="40c43-199">Static and Dynamic Error Display</span></span>

<span data-ttu-id="40c43-200">CSS 규칙은 `validation-summary-errors` 및 `validation-summary-valid`와 같이 쌍으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-200">The CSS rules come in pairs, such as `validation-summary-errors` and `validation-summary-valid`.</span></span> <span data-ttu-id="40c43-201">이러한 쌍을 통해 오류 조건 및 "일반" (오류 아님) 조건에 대 한 규칙을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-201">These pairs let you define rules for both conditions: an error condition and a "normal" (non-error) condition.</span></span> <span data-ttu-id="40c43-202">오류 표시에 대 한 태그는 오류가 없더라도 항상 렌더링 된다는 것을 이해 하는 것이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-202">It's important to understand that the markup for the error display is always rendered, even if there are no errors.</span></span> <span data-ttu-id="40c43-203">예를 들어 페이지의 태그에 `Html.ValidationSummary` 메서드가 있는 경우 페이지를 처음 요청 하는 경우에도 페이지 소스에는 다음 태그가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-203">For example, if a page has an `Html.ValidationSummary` method in the markup, the page source will contain the following markup even when the page is requested for the first time:</span></span>

`<div class="validation-summary-valid" data-valmsg-summary="true"><ul></ul></div>`

<span data-ttu-id="40c43-204">즉, `Html.ValidationSummary` 메서드는 오류 목록이 비어 있는 경우에도 항상 `<div>` 요소와 목록을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-204">In other words, the `Html.ValidationSummary` method always renders a `<div>` element and a list, even if the error list is empty.</span></span> <span data-ttu-id="40c43-205">마찬가지로 `Html.ValidationMessage` 메서드는 오류가 없더라도 항상 개별 필드 오류에 대 한 자리 표시자로 `<span>` 요소를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-205">Similarly, the `Html.ValidationMessage` method always renders a `<span>` element as a placeholder for an individual field error, even if there is no error.</span></span>

<span data-ttu-id="40c43-206">경우에 따라 오류 메시지를 표시 하면 페이지를 리플로우 하 여 페이지의 요소가 이동 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-206">In some situations, displaying an error message can cause the page to reflow and can cause elements on the page to move around.</span></span> <span data-ttu-id="40c43-207">`-valid` 종료 되는 CSS 규칙을 사용 하면이 문제를 방지 하는 데 도움이 되는 레이아웃을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-207">The CSS rules that end in `-valid` let you define a layout that can help prevent this problem.</span></span> <span data-ttu-id="40c43-208">예를 들어 `field-validation-error`를 정의 하 고 둘 다의 고정 크기를 `field-validation-valid` 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-208">For example, you can define `field-validation-error` and `field-validation-valid` to both have the same fixed size.</span></span> <span data-ttu-id="40c43-209">이렇게 하면 필드의 표시 영역이 정적이 고 오류 메시지가 표시 되 면 페이지 흐름이 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-209">That way, the display area for the field is static and won't change the page flow if an error message is displayed.</span></span>

<a id="Validating_Data_That_Doesnt_Come_Directly_from_Users"></a>
## <a name="validating-data-that-doesnt-come-directly-from-users"></a><span data-ttu-id="40c43-210">사용자에 게 직접 제공 되지 않는 데이터 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="40c43-210">Validating Data That Doesn't Come Directly from Users</span></span>

<span data-ttu-id="40c43-211">HTML 양식에서 직접 제공 하지 않는 정보의 유효성을 검사 해야 하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-211">Sometimes you have to validate information that doesn't come directly from an HTML form.</span></span> <span data-ttu-id="40c43-212">일반적인 예는 다음 예제와 같이 쿼리 문자열에서 값이 전달 되는 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-212">A typical example is a page where a value is passed in a query string, as in the following example:</span></span>

`http://server/myapp/EditClassInformation?classid=1022`

<span data-ttu-id="40c43-213">이 경우 페이지에 전달 된 값 (여기서는 `classid`값의 1022)이 유효한 지 확인 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-213">In this case, you want to make sure that the value that's passed to the page (here, 1022 for the value of `classid`) is valid.</span></span> <span data-ttu-id="40c43-214">`Validation` 도우미를 직접 사용 하 여이 유효성 검사를 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-214">You can't directly use the `Validation` helper to perform this validation.</span></span> <span data-ttu-id="40c43-215">그러나 유효성 검사 오류 메시지를 표시 하는 기능과 같은 유효성 검사 시스템의 다른 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-215">However, you can use other features of the validation system, like the ability to display validation error messages.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="40c43-216">**중요** 양식 필드 값, 쿼리 문자열 값 및 쿠키 값을 포함 하 여 *모든* 원본에서 가져온 값의 유효성을 항상 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-216">**Important** Always validate values that you get from *any* source, including form-field values, query-string values, and cookie values.</span></span> <span data-ttu-id="40c43-217">사용자는 이러한 값을 쉽게 변경할 수 있습니다 (악의적인 목적을 위해).</span><span class="sxs-lookup"><span data-stu-id="40c43-217">It's easy for people to change these values (perhaps for malicious purposes).</span></span> <span data-ttu-id="40c43-218">따라서 응용 프로그램을 보호 하기 위해 이러한 값을 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-218">So you must check these values in order to protect your application.</span></span>

<span data-ttu-id="40c43-219">다음 예에서는 쿼리 문자열에 전달 된 값의 유효성을 검사 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-219">The following example shows how you might validate a value that's passed in a query string.</span></span> <span data-ttu-id="40c43-220">이 코드는 값이 비어 있지 않고 정수 인지 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-220">The code tests that the value is not empty and that it's an integer.</span></span>

[!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample6.cs)]

<span data-ttu-id="40c43-221">요청이 양식 전송 (`if(!IsPost)`)이 아닌 경우 테스트가 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-221">Notice that the test is performed when the request is not a form submission (`if(!IsPost)`).</span></span> <span data-ttu-id="40c43-222">이 테스트는 페이지가 처음 요청 될 때를 전달 하지만 요청이 양식 전송 인 경우에는 전달 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-222">This test would pass the first time that the page is requested, but not when the request is a form submission.</span></span>

<span data-ttu-id="40c43-223">이 오류를 표시 하려면 `Validation.AddFormError("message")`를 호출 하 여 유효성 검사 오류 목록에 오류를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-223">To display this error, you can add the error to the list of validation errors by calling `Validation.AddFormError("message")`.</span></span> <span data-ttu-id="40c43-224">페이지에 `Html.ValidationSummary` 메서드에 대 한 호출이 포함 된 경우 사용자 입력 유효성 검사 오류와 마찬가지로 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40c43-224">If the page contains a call to the `Html.ValidationSummary` method, the error is displayed there, just like a user-input validation error.</span></span>

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a><span data-ttu-id="40c43-225">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="40c43-225">Additional Resources</span></span>

[<span data-ttu-id="40c43-226">ASP.NET 웹 페이지 사이트에서 HTML 양식 사용</span><span class="sxs-lookup"><span data-stu-id="40c43-226">Working with HTML Forms in ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkID=202892)
