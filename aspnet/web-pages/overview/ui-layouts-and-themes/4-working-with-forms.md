---
uid: web-pages/overview/ui-layouts-and-themes/4-working-with-forms
title: ASP.NET 웹 페이지 (Razor) 사이트에서 HTML 양식 사용 | Microsoft Docs
author: Rick-Anderson
description: 양식은 텍스트 상자, 확인란, 라디오 단추 및 풀 다운 목록과 같은 사용자 입력 컨트롤을 배치 하는 HTML 문서의 섹션입니다. 호환성이 폼을 사용 합니다.
ms.author: riande
ms.date: 02/10/2014
ms.assetid: f3f4b8c8-e8f6-4474-ad94-69228a6c01ee
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/4-working-with-forms
msc.type: authoredcontent
ms.openlocfilehash: c7d4802063c8610a246afe67bd15eea429f7304a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519605"
---
# <a name="working-with-html-forms-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="6ab7c-104">ASP.NET 웹 페이지 (Razor) 사이트에서 HTML 양식 사용</span><span class="sxs-lookup"><span data-stu-id="6ab7c-104">Working with HTML Forms in ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="6ab7c-105">만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="6ab7c-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="6ab7c-106">이 문서에서는 Razor (ASP.NET 웹 페이지) 웹 사이트에서 작업할 때 텍스트 상자와 단추를 사용 하 여 HTML 폼을 처리 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-106">This article describes how to process an HTML form (with text boxes and buttons) when you are working in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="6ab7c-107">**학습 내용:**</span><span class="sxs-lookup"><span data-stu-id="6ab7c-107">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="6ab7c-108">HTML 폼을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="6ab7c-108">How to create an HTML form.</span></span>
> - <span data-ttu-id="6ab7c-109">양식에서 사용자 입력을 읽는 방법</span><span class="sxs-lookup"><span data-stu-id="6ab7c-109">How to read user input from the form.</span></span>
> - <span data-ttu-id="6ab7c-110">사용자 입력의 유효성을 검사 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-110">How to validate user input.</span></span>
> - <span data-ttu-id="6ab7c-111">페이지가 제출 된 후 양식 값을 복원 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-111">How to restore form values after the page is submitted.</span></span>
> 
> <span data-ttu-id="6ab7c-112">다음은이 문서에서 소개 하는 ASP.NET 프로그래밍 개념입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-112">These are the ASP.NET programming concepts introduced in the article:</span></span>
> 
> - <span data-ttu-id="6ab7c-113">`Request` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-113">The `Request` object.</span></span>
> - <span data-ttu-id="6ab7c-114">입력 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="6ab7c-114">Input validation.</span></span>
> - <span data-ttu-id="6ab7c-115">HTML 인코딩입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-115">HTML encoding.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="6ab7c-116">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="6ab7c-116">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="6ab7c-117">ASP.NET 웹 페이지 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="6ab7c-117">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="6ab7c-118">이 자습서는 ASP.NET 웹 페이지 2 에서도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-118">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="creating-a-simple-html-form"></a><span data-ttu-id="6ab7c-119">간단한 HTML 폼 만들기</span><span class="sxs-lookup"><span data-stu-id="6ab7c-119">Creating a Simple HTML Form</span></span>

1. <span data-ttu-id="6ab7c-120">새 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-120">Create a new website.</span></span>
2. <span data-ttu-id="6ab7c-121">루트 폴더에서 이름이 *Form* 인 웹 페이지를 만들고 다음 태그를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-121">In the root folder, create a web page named *Form.cshtml* and enter the following markup:</span></span>

    [!code-html[Main](4-working-with-forms/samples/sample1.html)]
3. <span data-ttu-id="6ab7c-122">브라우저에서 페이지를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-122">Launch the page in your browser.</span></span> <span data-ttu-id="6ab7c-123">(WebMatrix의 **파일** 작업 영역에서 파일을 마우스 오른쪽 단추로 클릭 한 다음 **브라우저에서 시작**을 선택 합니다.) 3 개의 입력 필드와 **제출** 단추가 있는 간단한 양식이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-123">(In WebMatrix, in the **Files** workspace, right-click the file and then select **Launch in browser**.) A simple form with three input fields and a **Submit** button is displayed.</span></span>

    ![3 개의 입력란이 있는 폼의 스크린샷](4-working-with-forms/_static/image1.png)

    <span data-ttu-id="6ab7c-125">이 시점에서 **제출** 단추를 클릭 하면 아무 일도 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-125">At this point, if you click the **Submit** button, nothing happens.</span></span> <span data-ttu-id="6ab7c-126">폼을 유용 하 게 만들려면 서버에서 실행 되는 일부 코드를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-126">To make the form useful, you have to add some code that will run on the server.</span></span>

## <a name="reading-user-input-from-the-form"></a><span data-ttu-id="6ab7c-127">양식에서 사용자 입력 읽기</span><span class="sxs-lookup"><span data-stu-id="6ab7c-127">Reading User Input from the Form</span></span>

<span data-ttu-id="6ab7c-128">폼을 처리 하려면 전송 된 필드 값을 읽고이를 사용 하 여 작업을 수행 하는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-128">To process the form, you add code that reads the submitted field values and does something with them.</span></span> <span data-ttu-id="6ab7c-129">이 절차에서는 필드를 읽고 페이지에서 사용자 입력을 표시 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-129">This procedure shows you how to read the fields and display the user input on the page.</span></span> <span data-ttu-id="6ab7c-130">프로덕션 응용 프로그램에서는 일반적으로 사용자 입력을 통해 더 흥미로운 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-130">(In a production application, you generally do more interesting things with user input.</span></span> <span data-ttu-id="6ab7c-131">데이터베이스 사용에 대 한 문서에서이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-131">You'll do that in the article about working with databases.)</span></span>

1. <span data-ttu-id="6ab7c-132">*Cshtml* 파일의 맨 위에 다음 코드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-132">At the top of the *Form.cshtml* file, enter the following code:</span></span>

    [!code-cshtml[Main](4-working-with-forms/samples/sample2.cshtml)]

    <span data-ttu-id="6ab7c-133">사용자가 페이지를 처음 요청 하면 빈 양식만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-133">When the user first requests the page, only the empty form is displayed.</span></span> <span data-ttu-id="6ab7c-134">사용자가 폼을 채운 다음 **제출**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-134">The user (which will be you) fills in the form and then clicks **Submit**.</span></span> <span data-ttu-id="6ab7c-135">사용자 입력을 서버에 제출 (게시) 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-135">This submits (posts) the user input to the server.</span></span> <span data-ttu-id="6ab7c-136">기본적으로이 요청은 동일한 페이지 (예를 들어, *폼. cshtml*)로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-136">By default, the request goes to the same page (namely, *Form.cshtml*).</span></span>

    <span data-ttu-id="6ab7c-137">이번에 페이지를 제출 하면 입력 한 값이 폼 바로 위에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-137">When you submit the page this time, the values you entered are displayed just above the form:</span></span>

    ![사용자가 페이지에 표시 한 값을 보여 주는 스크린샷](4-working-with-forms/_static/image2.png)

    <span data-ttu-id="6ab7c-139">페이지의 코드를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-139">Look at the code for the page.</span></span> <span data-ttu-id="6ab7c-140">먼저 `IsPost` 메서드를 사용 하 여 페이지가 게시 &#8212; 되었는지 여부, 즉 사용자가 **제출** 단추를 클릭 했는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-140">You first use the `IsPost` method to determine whether the page is being posted &#8212; that is, whether a user clicked the **Submit** button.</span></span> <span data-ttu-id="6ab7c-141">Post 인 경우 `IsPost` true를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-141">If this is a post, `IsPost` returns true.</span></span> <span data-ttu-id="6ab7c-142">이는 초기 요청 (GET 요청)을 사용 하는지 아니면 포스트백 (POST 요청)을 사용 하 고 있는지를 확인 하는 ASP.NET 웹 페이지 표준 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-142">This is the standard way in ASP.NET Web Pages to determine whether you're working with an initial request (a GET request) or a postback (a POST request).</span></span> <span data-ttu-id="6ab7c-143">GET 및 POST에 대 한 자세한 내용은 [Razor 구문을 사용 하는 ASP.NET 웹 페이지 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkId=202890#SB_HttpGetPost)의 "HTTP GET 및 Post 및 IsPost 속성"을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-143">(For more information about GET and POST, see the sidebar "HTTP GET and POST and the IsPost Property" in [Introduction to ASP.NET Web Pages Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=202890#SB_HttpGetPost).)</span></span>

    <span data-ttu-id="6ab7c-144">그런 다음 사용자가 `Request.Form` 개체에서 채운 값을 가져와 나중에 사용할 수 있도록 변수에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-144">Next, you get the values that the user filled in from the `Request.Form` object, and you put them in variables for later.</span></span> <span data-ttu-id="6ab7c-145">`Request.Form` 개체는 페이지를 사용 하 여 제출 된 모든 값을 포함 하며, 각 값은 키로 식별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-145">The `Request.Form` object contains all the values that were submitted with the page, each identified by a key.</span></span> <span data-ttu-id="6ab7c-146">키는 읽을 폼 필드의 `name` 특성과 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-146">The key is the equivalent to the `name` attribute of the form field that you want to read.</span></span> <span data-ttu-id="6ab7c-147">예를 들어 `companyname` 필드 (텍스트 상자)를 읽으려면 `Request.Form["companyname"]`를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-147">For example, to read the `companyname` field (text box), you use `Request.Form["companyname"]`.</span></span>

    <span data-ttu-id="6ab7c-148">양식 값은 `Request.Form` 개체에 문자열로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-148">Form values are stored in the `Request.Form` object as strings.</span></span> <span data-ttu-id="6ab7c-149">따라서 값을 숫자 또는 날짜 또는 다른 형식으로 사용 해야 하는 경우 문자열에서 해당 형식으로 변환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-149">Therefore, when you have to work with a value as a number or a date or some other type, you have to convert it from a string to that type.</span></span> <span data-ttu-id="6ab7c-150">이 예제에서 `Request.Form`의 `AsInt` 메서드는 직원 수를 포함 하는 employees 필드의 값을 정수로 변환 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-150">In the example, the `AsInt` method of the `Request.Form` is used to convert the value of the employees field (which contains an employee count) to an integer.</span></span>
2. <span data-ttu-id="6ab7c-151">브라우저에서 페이지를 시작 하 고 양식 필드를 입력 한 다음 **제출**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-151">Launch the page in your browser, fill in the form fields, and click **Submit**.</span></span> <span data-ttu-id="6ab7c-152">이 페이지에는 사용자가 입력 한 값이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-152">The page displays the values you entered.</span></span>

> [!TIP] 
> 
> <a id="SB_HTMLEncoding"></a>
> ### <a name="html-encoding-for-appearance-and-security"></a><span data-ttu-id="6ab7c-153">모양 및 보안을 위한 HTML 인코딩</span><span class="sxs-lookup"><span data-stu-id="6ab7c-153">HTML Encoding for Appearance and Security</span></span>
> 
> <span data-ttu-id="6ab7c-154">HTML에는 `<`, `>`및 `&`와 같은 문자에 대 한 특별 한 사용이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-154">HTML has special uses for characters like `<`, `>`, and `&`.</span></span> <span data-ttu-id="6ab7c-155">이러한 특수 문자가 필요 하지 않은 위치에 표시 되는 경우 웹 페이지의 모양과 기능을 ruin 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-155">If these special characters appear where they're not expected, they can ruin the appearance and functionality of your web page.</span></span> <span data-ttu-id="6ab7c-156">예를 들어 브라우저는 `<b>` 또는 `<input ...>`와 같이 HTML 요소의 시작으로 `<` 문자 (공백이 뒤에 오지 않는 경우)를 해석 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-156">For example, the browser interprets the `<` character (unless it's followed by a space) as the beginning of an HTML element, like `<b>` or `<input ...>`.</span></span> <span data-ttu-id="6ab7c-157">브라우저에서 요소를 인식 하지 못하는 경우 다시 인식 되는 항목에 도달할 때까지 `<`로 시작 하는 문자열을 삭제 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-157">If the browser doesn't recognize the element, it simply discards the string that begins with `<` until it reaches something that it again recognizes.</span></span> <span data-ttu-id="6ab7c-158">이로 인해 페이지에서 이상한 렌더링이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-158">Obviously, this can result in some weird rendering in the page.</span></span>
> 
> <span data-ttu-id="6ab7c-159">HTML 인코딩은 이러한 예약 문자를 브라우저에서 올바른 기호로 해석 하는 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-159">HTML encoding replaces these reserved characters with a code that browsers interpret as the correct symbol.</span></span> <span data-ttu-id="6ab7c-160">예를 들어 `<` 문자는 `&lt;`로 바뀌고 `>` 문자는 `&gt;`로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-160">For example, the `<` character is replaced with `&lt;` and the `>` character is replaced with `&gt;`.</span></span> <span data-ttu-id="6ab7c-161">브라우저는 이러한 대체 문자열을 확인 하려는 문자로 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-161">The browser renders these replacement strings as the characters that you want to see.</span></span>
> 
> <span data-ttu-id="6ab7c-162">사용자가 가져온 문자열 (입력)을 표시할 때마다 HTML 인코딩을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-162">It's a good idea to use HTML encoding any time you display strings (input) that you got from a user.</span></span> <span data-ttu-id="6ab7c-163">그렇지 않으면 사용자가 웹 페이지에서 악의적인 스크립트를 실행 하거나 사이트 보안을 손상 시키는 다른 작업을 수행 하거나 의도 한 것이 아닌 다른 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-163">If you don't, a user can try to get your web page to run a malicious script or do something else that compromises your site security or that's just not what you intend.</span></span> <span data-ttu-id="6ab7c-164">사용자 입력을 사용 하 고 원하는 대로 저장 한 다음 나중 &#8212; 에 예를 들어 블로그 주석, 사용자 검토 또는 이와 같은 항목으로 표시 하는 경우에 특히 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-164">(This is particularly important if you take user input, store it someplace, and then display it later &#8212; for example, as a blog comment, user review, or something like that.)</span></span>
> 
> <span data-ttu-id="6ab7c-165">이러한 문제를 방지 하기 위해 ASP.NET 웹 페이지 코드에서 출력 하는 텍스트 콘텐츠를 자동으로 HTML로 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-165">To help prevent these problems, ASP.NET Web Pages automatically HTML-encodes any text content that you output from your code.</span></span> <span data-ttu-id="6ab7c-166">예를 들어 `@MyVar`와 같은 코드를 사용 하 여 변수 또는 식의 내용을 표시 하는 경우 ASP.NET 웹 페이지 출력을 자동으로 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-166">For example, when you display the content of a variable or an expression using code such as `@MyVar`, ASP.NET Web Pages automatically encodes the output.</span></span>

## <a name="validating-user-input"></a><span data-ttu-id="6ab7c-167">사용자 입력 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="6ab7c-167">Validating User Input</span></span>

<span data-ttu-id="6ab7c-168">사용자에 게 실수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-168">Users make mistakes.</span></span> <span data-ttu-id="6ab7c-169">사용자가 필드를 채우도록 요청 하 고, 직원 수를 입력 하 라는 메시지를 표시 하거나 대신 이름을 입력 하도록 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-169">You ask them to fill in a field, and they forget to, or you ask them to enter the number of employees and they type a name instead.</span></span> <span data-ttu-id="6ab7c-170">처리 하기 전에 양식이 올바르게 입력 되었는지 확인 하려면 사용자 입력의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-170">To make sure that a form has been filled in correctly before you process it, you validate the user's input.</span></span>

<span data-ttu-id="6ab7c-171">이 절차에서는 세 가지 양식 필드의 유효성을 검사 하 여 사용자가 비워 두지 않았는지 확인 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-171">This procedure shows how to validate all three form fields to make sure the user didn't leave them blank.</span></span> <span data-ttu-id="6ab7c-172">또한 employee count 값이 숫자 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-172">You also check that the employee count value is a number.</span></span> <span data-ttu-id="6ab7c-173">오류가 있는 경우 유효성 검사를 통과 하지 못한 값을 사용자에 게 알리는 오류 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-173">If there are errors, you'll display an error message that tells the user what values didn't pass validation.</span></span>

1. <span data-ttu-id="6ab7c-174">*Cshtml* 파일에서 첫 번째 코드 블록을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-174">In the *Form.cshtml* file, replace the first block of code with the following code:</span></span> 

    [!code-cshtml[Main](4-working-with-forms/samples/sample3.cshtml)]

    <span data-ttu-id="6ab7c-175">사용자 입력의 유효성을 검사 하려면 `Validation` 도우미를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-175">To validate user input, you use the `Validation` helper.</span></span> <span data-ttu-id="6ab7c-176">`Validation.RequireField`를 호출 하 여 필수 필드를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-176">You register required fields by calling `Validation.RequireField`.</span></span> <span data-ttu-id="6ab7c-177">`Validation.Add`를 호출 하 고 유효성을 검사할 필드와 수행할 유효성 검사 유형을 지정 하 여 다른 유형의 유효성 검사를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-177">You register other types of validation by calling `Validation.Add` and specifying the field to validate and the type of validation to perform.</span></span>

    <span data-ttu-id="6ab7c-178">페이지가 실행 될 때 ASP.NET는 모든 유효성 검사를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-178">When the page runs, ASP.NET does all the validation for you.</span></span> <span data-ttu-id="6ab7c-179">`Validation.IsValid`를 호출 하 여 결과를 확인할 수 있습니다 .이는 모두 성공 하면 true를 반환 하 고, 필드의 유효성 검사에 실패 하면 false를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-179">You can check the results by calling `Validation.IsValid`, which returns true if everything passed and false if any field failed validation.</span></span> <span data-ttu-id="6ab7c-180">일반적으로 사용자 입력에 대 한 처리를 수행 하기 전에 `Validation.IsValid`를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-180">Typically, you call `Validation.IsValid` before you perform any processing on the user input.</span></span>
2. <span data-ttu-id="6ab7c-181">다음과 같이 `Html.ValidationMessage` 메서드에 세 개의 호출을 추가 하 여 `<body>` 요소를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-181">Update the `<body>` element by adding three calls to the `Html.ValidationMessage` method, like this:</span></span>

    [!code-cshtml[Main](4-working-with-forms/samples/sample4.cshtml?highlight=8,13,18)]

    <span data-ttu-id="6ab7c-182">유효성 검사 오류 메시지를 표시 하려면 Html.`ValidationMessage`를 호출 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-182">To display validation error messages, you can call Html.`ValidationMessage`</span></span> <span data-ttu-id="6ab7c-183">메시지에 사용할 필드의 이름을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-183">and pass it the name of the field that you want the message for.</span></span>
3. <span data-ttu-id="6ab7c-184">페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-184">Run the page.</span></span> <span data-ttu-id="6ab7c-185">필드를 비워 두고 **전송**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-185">Leave the fields blank and click **Submit**.</span></span> <span data-ttu-id="6ab7c-186">오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-186">You see error messages.</span></span>

    ![사용자 입력이 유효성 검사를 통과 하지 못한 경우 표시 되는 오류 메시지를 보여 주는 스크린샷](4-working-with-forms/_static/image3.jpg)
4. <span data-ttu-id="6ab7c-188">**직원 수** 필드에 문자열 (예: "ABC")을 추가 하 고 **제출을** 다시 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-188">Add a string (for example, "ABC") to the **Employee Count** field and click **Submit** again.</span></span> <span data-ttu-id="6ab7c-189">이번에는 문자열이 올바른 형식 (예를 들어, 정수)이 아님을 나타내는 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-189">This time you see an error that indicates that the string isn't in the right format, namely, an integer.</span></span>

    ![사용자가 직원 필드에 대 한 문자열을 입력 하는 경우 표시 되는 오류 메시지를 보여 주는 스크린샷](4-working-with-forms/_static/image4.jpg)

<span data-ttu-id="6ab7c-191">ASP.NET 웹 페이지은 사용자가 브라우저에서 즉각적인 피드백을 받을 수 있도록 클라이언트 스크립트를 사용 하 여 자동으로 유효성 검사를 수행 하는 기능을 포함 하 여 사용자 입력의 유효성을 검사 하는 옵션을</span><span class="sxs-lookup"><span data-stu-id="6ab7c-191">ASP.NET Web Pages provides more options for validating user input, including the ability to automatically perform validation using client script, so that users get immediate feedback in the browser.</span></span> <span data-ttu-id="6ab7c-192">자세한 내용은 나중에 [추가 리소스](#Additional_Resources) 섹션을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-192">See the [Additional Resources](#Additional_Resources) section later for more information.</span></span>

## <a name="restoring-form-values-after-postbacks"></a><span data-ttu-id="6ab7c-193">다시 게시 후 양식 값 복원</span><span class="sxs-lookup"><span data-stu-id="6ab7c-193">Restoring Form Values After Postbacks</span></span>

<span data-ttu-id="6ab7c-194">이전 섹션에서 페이지를 테스트 하는 경우 유효성 검사 오류가 발생 하 고 입력 한 모든 항목 (잘못 된 데이터만 아님)이 없어졌으므로 모든 필드에 대 한 값을 다시 입력 해야 하는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-194">When you tested the page in the previous section, you might have noticed that if you had a validation error, everything you entered (not just the invalid data) was gone, and you had to re-enter values for all the fields.</span></span> <span data-ttu-id="6ab7c-195">이는 중요 한 점을 보여 줍니다. 페이지를 제출 하 고 처리 한 다음 페이지를 다시 렌더링 하면 페이지가 처음부터 다시 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-195">This illustrates an important point: when you submit a page, process it, and then render the page again, the page is re-created from scratch.</span></span> <span data-ttu-id="6ab7c-196">이는 표시 된 것 처럼 페이지에서 제출 된 모든 값이 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-196">As you saw, this means that any values that were in the page when it was submitted are lost.</span></span>

<span data-ttu-id="6ab7c-197">그러나이 문제는 쉽게 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-197">You can fix this easily, however.</span></span> <span data-ttu-id="6ab7c-198">전송 된 값에 액세스할 수 있습니다 (`Request.Form` 개체에서 페이지가 렌더링 될 때 이러한 값을 양식 필드에 다시 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-198">You have access to the values that were submitted (in the `Request.Form` object, so you can fill those values back into the form fields when the page is rendered.</span></span>

1. <span data-ttu-id="6ab7c-199">*형식. cshtml* 파일에서 `value` 특성을 사용 하 여 `<input>` 요소의 `value` 특성을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-199">In the *Form.cshtml* file, replace the `value` attributes of the `<input>` elements using the `value` attribute.:</span></span> 

    [!code-cshtml[Main](4-working-with-forms/samples/sample5.cshtml?highlight=13,19,25)]

    <span data-ttu-id="6ab7c-200">`<input>` 요소의 `value` 특성이 `Request.Form` 개체에서 필드 값을 동적으로 읽도록 설정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-200">The `value` attribute of the `<input>` elements has been set to dynamically read the field value out of the `Request.Form` object.</span></span> <span data-ttu-id="6ab7c-201">페이지가 처음 요청 될 때 `Request.Form` 개체의 값은 모두 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-201">The first time that the page is requested, the values in the `Request.Form` object are all empty.</span></span> <span data-ttu-id="6ab7c-202">이 방법은 폼이 비어 있기 때문에 문제가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-202">This is fine, because that way the form is blank.</span></span>
2. <span data-ttu-id="6ab7c-203">브라우저에서 페이지를 시작 하 고 양식 필드를 입력 하거나 비워 두고 **전송**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-203">Launch the page in your browser, fill in the form fields or leave them blank, and click **Submit**.</span></span> <span data-ttu-id="6ab7c-204">전송 된 값을 표시 하는 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ab7c-204">A page that shows the submitted values is displayed.</span></span>

    ![양식-5](4-working-with-forms/_static/image5.jpg)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="6ab7c-206">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="6ab7c-206">Additional Resources</span></span>

- [<span data-ttu-id="6ab7c-207">1001 웹 사용자의 입력을 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="6ab7c-207">1,001 Ways to Get Input from Web Users</span></span>](https://msdn.microsoft.com/library/ms971057.aspx)
- <span data-ttu-id="6ab7c-208">[양식 사용 및 사용자 입력 처리](https://msdn.microsoft.com/library/ms525182(VS.90).aspx)</span><span class="sxs-lookup"><span data-stu-id="6ab7c-208">[Using Forms and Processing User Input](https://msdn.microsoft.com/library/ms525182(VS.90).aspx)</span></span>
- [<span data-ttu-id="6ab7c-209">ASP.NET 웹 페이지 사이트에서 사용자 입력 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="6ab7c-209">Validating User Input in ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=253002)
- <span data-ttu-id="6ab7c-210">[HTML 양식에서 자동 완성 사용](https://msdn.microsoft.com/library/ms533032(VS.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="6ab7c-210">[Using AutoComplete in HTML Forms](https://msdn.microsoft.com/library/ms533032(VS.85).aspx)</span></span>
