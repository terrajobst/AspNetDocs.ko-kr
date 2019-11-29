---
uid: web-pages/overview/getting-started/introducing-razor-syntax-c
title: Razor 구문 (C#)을 사용 하는 ASP.NET 웹 프로그래밍 소개 | Microsoft Docs
author: Rick-Anderson
description: 이 장에서는 Razor 구문를 사용 하 ASP.NET 웹 페이지 프로그래밍에 대 한 개요를 제공 합니다. ASP.NET는 동적 웹 pa를 실행 하는 Microsoft 기술입니다 ...
ms.author: riande
ms.date: 02/07/2014
ms.assetid: aa67d304-583b-4bf8-a231-195656cfb587
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-c
msc.type: authoredcontent
ms.openlocfilehash: c2f420bb7c2f7d2e31654c20fb9ec7497a30a9f7
ms.sourcegitcommit: 6f0e10e4ca61a1e5534b09c655fd35cdc6886c8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2019
ms.locfileid: "74564882"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-c"></a><span data-ttu-id="05e9f-104">Razor 구문 (C#)을 사용 하는 ASP.NET 웹 프로그래밍 소개</span><span class="sxs-lookup"><span data-stu-id="05e9f-104">Introduction to ASP.NET Web Programming Using the Razor Syntax (C#)</span></span>

<span data-ttu-id="05e9f-105">만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="05e9f-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="05e9f-106">이 문서에서는 Razor 구문를 사용 하 여 ASP.NET 웹 페이지 프로그래밍에 대 한 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-106">This article gives you an overview of programming with ASP.NET Web Pages using the Razor syntax.</span></span> <span data-ttu-id="05e9f-107">ASP.NET는 웹 서버에서 동적 웹 페이지를 실행 하기 위한 Microsoft 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-107">ASP.NET is Microsoft's technology for running dynamic web pages on web servers.</span></span> <span data-ttu-id="05e9f-108">이 문서에서는 프로그래밍 언어를 C# 사용 하는 방법을 중점적으로 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-108">This articles focuses on using the C# programming language.</span></span>
> 
> <span data-ttu-id="05e9f-109">**학습 내용**:</span><span class="sxs-lookup"><span data-stu-id="05e9f-109">**What you'll learn**:</span></span>
> 
> - <span data-ttu-id="05e9f-110">Razor 구문를 사용 하 여 프로그래밍 ASP.NET 웹 페이지 시작 하기 위한 상위 8 개 프로그래밍 팁.</span><span class="sxs-lookup"><span data-stu-id="05e9f-110">The top 8 programming tips for getting started with programming ASP.NET Web Pages using Razor syntax.</span></span>
> - <span data-ttu-id="05e9f-111">필요한 기본 프로그래밍 개념.</span><span class="sxs-lookup"><span data-stu-id="05e9f-111">Basic programming concepts you'll need.</span></span>
> - <span data-ttu-id="05e9f-112">ASP.NET 서버 코드 및 Razor 구문은 무엇 인가요?</span><span class="sxs-lookup"><span data-stu-id="05e9f-112">What ASP.NET server code and the Razor syntax is all about.</span></span>
>   
> 
> ## <a name="software-versions"></a><span data-ttu-id="05e9f-113">소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="05e9f-113">Software versions</span></span>
> 
> 
> - <span data-ttu-id="05e9f-114">ASP.NET 웹 페이지 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="05e9f-114">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="05e9f-115">이 자습서는 ASP.NET 웹 페이지 2 에서도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-115">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="the-top-8-programming-tips"></a><span data-ttu-id="05e9f-116">상위 8 개 프로그래밍 팁</span><span class="sxs-lookup"><span data-stu-id="05e9f-116">The Top 8 Programming Tips</span></span>

<span data-ttu-id="05e9f-117">이 섹션에는 Razor 구문를 사용 하 여 ASP.NET 서버 코드 작성을 시작할 때 알아야 할 몇 가지 팁이 나열 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-117">This section lists a few tips that you absolutely need to know as you start writing ASP.NET server code using the Razor syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="05e9f-118">Razor 구문은 C# 프로그래밍 언어를 기반으로 하며,이는 ASP.NET 웹 페이지에서 가장 자주 사용 되는 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-118">The Razor syntax is based on the C# programming language, and that's the language that's used most often with ASP.NET Web Pages.</span></span> <span data-ttu-id="05e9f-119">그러나이 Razor 구문는 Visual Basic 언어도 지원 하 고 모든 사용자가 Visual Basic에서 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-119">However, the Razor syntax also supports the Visual Basic language, and everything you see you can also do in Visual Basic.</span></span> <span data-ttu-id="05e9f-120">자세한 내용은 부록 [Visual Basic 언어 및 구문](https://go.microsoft.com/fwlink/?LinkId=202908)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="05e9f-120">For details, see the appendix [Visual Basic Language and Syntax](https://go.microsoft.com/fwlink/?LinkId=202908).</span></span>

<span data-ttu-id="05e9f-121">이러한 프로그래밍 기술에 대 한 자세한 내용은이 문서의 뒷부분에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-121">You can find more details about most of these programming techniques later in the article.</span></span>

### <a name="1-you-add-code-to-a-page-using-the--character"></a><span data-ttu-id="05e9f-122">1. @ 문자를 사용 하 여 페이지에 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-122">1. You add code to a page using the @ character</span></span>

<span data-ttu-id="05e9f-123">`@` 문자는 인라인 식, 단일 문 블록 및 다중 문 블록을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-123">The `@` character starts inline expressions, single statement blocks, and multi-statement blocks:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample1.html)]

<span data-ttu-id="05e9f-124">이는 페이지가 브라우저에서 실행 될 때 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-124">This is what these statements look like when the page runs in a browser:</span></span>

![Razor-.Img1](introducing-razor-syntax-c/_static/image1.jpg)

> [!TIP] 
> 
> <span data-ttu-id="05e9f-126">**HTML 인코딩**</span><span class="sxs-lookup"><span data-stu-id="05e9f-126">**HTML Encoding**</span></span>
> 
> <span data-ttu-id="05e9f-127">앞의 예제와 같이 `@` 문자를 사용 하 여 페이지에 콘텐츠를 표시 하는 경우 ASP.NET은 출력을 HTML로 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-127">When you display content in a page using the `@` character, as in the preceding examples, ASP.NET HTML-encodes the output.</span></span> <span data-ttu-id="05e9f-128">이렇게 하면 예약 된 HTML 문자 (예: `<`, `>` 및 `&`)가 HTML 태그나 엔터티로 해석 되지 않고 웹 페이지에서 문자로 표시 될 수 있도록 하는 코드와 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-128">This replaces reserved HTML characters (such as `<` and `>` and `&`) with codes that enable the characters to be displayed as characters in a web page instead of being interpreted as HTML tags or entities.</span></span> <span data-ttu-id="05e9f-129">HTML 인코딩이 없으면 서버 코드의 출력이 올바르게 표시 되지 않을 수 있으며, 페이지를 보안 위험에 노출 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-129">Without HTML encoding, the output from your server code might not display correctly, and could expose a page to security risks.</span></span>
> 
> <span data-ttu-id="05e9f-130">태그를 태그로 렌더링 하는 HTML 태그를 출력 하는 경우 (`<p></p>` 예: 단락이 나 텍스트를 강조 하는 `<em></em>`)에는이 문서의 뒷부분에 나오는 [코드 블록의 텍스트, 태그 및 코드 결합](#BM_CombiningTextMarkupAndCode) 단원을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="05e9f-130">If your goal is to output HTML markup that renders tags as markup (for example `<p></p>` for a paragraph or `<em></em>` to emphasize text), see the section [Combining Text, Markup, and Code in Code Blocks](#BM_CombiningTextMarkupAndCode) later in this article.</span></span>
> 
> <span data-ttu-id="05e9f-131">[양식 작업](https://go.microsoft.com/fwlink/?LinkId=202892)에서 HTML 인코딩에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-131">You can read more about HTML encoding in [Working with Forms](https://go.microsoft.com/fwlink/?LinkId=202892).</span></span>

### <a name="2-you-enclose-code-blocks-in-braces"></a><span data-ttu-id="05e9f-132">2. 코드 블록을 중괄호로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-132">2. You enclose code blocks in braces</span></span>

<span data-ttu-id="05e9f-133">*코드 블록* 에는 하나 이상의 코드 문이 포함 되 고 중괄호로 묶여 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-133">A *code block* includes one or more code statements and is enclosed in braces.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample2.html)]

<span data-ttu-id="05e9f-134">브라우저에 표시 되는 결과는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-134">The result displayed in a browser:</span></span>

![Razor-Img2](introducing-razor-syntax-c/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-semicolon"></a><span data-ttu-id="05e9f-136">3. 블록 내에서 각 코드 문은 세미콜론으로 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-136">3. Inside a block, you end each code statement with a semicolon</span></span>

<span data-ttu-id="05e9f-137">코드 블록 내에서 각 완성 된 코드 문은 세미콜론으로 끝나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-137">Inside a code block, each complete code statement must end with a semicolon.</span></span> <span data-ttu-id="05e9f-138">인라인 식은 세미콜론으로 끝나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-138">Inline expressions don't end with a semicolon.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample3.html)]

### <a name="4-you-use-variables-to-store-values"></a><span data-ttu-id="05e9f-139">4. 변수를 사용 하 여 값 저장</span><span class="sxs-lookup"><span data-stu-id="05e9f-139">4. You use variables to store values</span></span>

<span data-ttu-id="05e9f-140">문자열, 숫자, 날짜 등을 포함 하 여 *변수에*값을 저장할 수 있습니다. `var` 키워드를 사용 하 여 새 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-140">You can store values in a *variable*, including strings, numbers, and dates, etc. You create a new variable using the `var` keyword.</span></span> <span data-ttu-id="05e9f-141">`@`를 사용 하 여 페이지에 직접 변수 값을 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-141">You can insert variable values directly in a page using `@`.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample4.html)]

<span data-ttu-id="05e9f-142">브라우저에 표시 되는 결과는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-142">The result displayed in a browser:</span></span>

![Razor-Img3](introducing-razor-syntax-c/_static/image3.jpg)

<a id="ID_StringLiterals"></a>
### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a><span data-ttu-id="05e9f-144">5. 리터럴 문자열 값을 큰따옴표로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-144">5. You enclose literal string values in double quotation marks</span></span>

<span data-ttu-id="05e9f-145">*문자열* 은 텍스트로 처리 되는 문자 시퀀스입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-145">A *string* is a sequence of characters that are treated as text.</span></span> <span data-ttu-id="05e9f-146">문자열을 지정 하려면 큰따옴표로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-146">To specify a string, you enclose it in double quotation marks:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample5.cshtml)]

<span data-ttu-id="05e9f-147">표시 하려는 문자열에 백슬래시 문자 (`\`) 또는 큰따옴표 (`"`)가 포함 된 경우에는 `@` 연산자 접두사가 붙은 *축 자 문자열 리터럴을* 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-147">If the string that you want to display contains a backslash character ( `\` ) or double quotation marks ( `"` ), use a *verbatim string literal* that's prefixed with the `@` operator.</span></span> <span data-ttu-id="05e9f-148">에서 C#\ 문자는 축 자 문자열 리터럴을 사용 하지 않는 한 특별 한 의미를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-148">(In C#, the \ character has special meaning unless you use a verbatim string literal.)</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample6.html)]

<span data-ttu-id="05e9f-149">큰따옴표를 포함 하려면 축 자 문자열 리터럴을 사용 하 고 따옴표를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-149">To embed double quotation marks, use a verbatim string literal and repeat the quotation marks:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample7.html)]

<span data-ttu-id="05e9f-150">다음은 페이지에서 두 예제를 모두 사용 하는 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-150">Here's the result of using both of these examples in a page:</span></span>

![Razor-Img4](introducing-razor-syntax-c/_static/image4.jpg)

> [!NOTE]
> <span data-ttu-id="05e9f-152">`@` 문자는 및의 C# 축 자 문자열 리터럴을 표시 하 고 ASP.NET 페이지에 코드를 표시 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-152">Notice that the `@` character is used both to mark verbatim string literals in C# and to mark code in ASP.NET pages.</span></span>

### <a name="6-code-is-case-sensitive"></a><span data-ttu-id="05e9f-153">6. 코드는 대/소문자를 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-153">6. Code is case sensitive</span></span>

<span data-ttu-id="05e9f-154">에서 C#키워드 (예: `var`, `true`, `if`) 및 변수 이름은 대/소문자를 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-154">In C#, keywords (like `var`, `true`, and `if`) and variable names are case sensitive.</span></span> <span data-ttu-id="05e9f-155">다음 코드 줄에서는 두 개의 서로 다른 변수 `lastName` 및 `LastName.`를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-155">The following lines of code create two different variables, `lastName` and `LastName.`</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample8.cshtml)]

<span data-ttu-id="05e9f-156">변수를 `var lastName = "Smith";` 선언 하 고 페이지에서 `@LastName`으로 해당 변수를 참조 하려고 하면 `"Smith"`대신 `"Jones"` 값이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-156">If you declare a variable as `var lastName = "Smith";` and try to reference that variable in your page as `@LastName`, you would get the value `"Jones"` instead of `"Smith"`.</span></span>

> [!NOTE]
> <span data-ttu-id="05e9f-157">Visual Basic 키워드와 변수는 대/소문자를 구분 *하지 않습니다* .</span><span class="sxs-lookup"><span data-stu-id="05e9f-157">In Visual Basic, keywords and variables are *not* case sensitive.</span></span>

### <a name="7-much-of-your-coding-involves-objects"></a><span data-ttu-id="05e9f-158">7. 대부분의 코딩에는 개체가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-158">7. Much of your coding involves objects</span></span>

<span data-ttu-id="05e9f-159">*개체* 는 페이지, 텍스트 상자, 파일, 이미지 &#8212; , 웹 요청, 전자 메일 메시지, 고객 레코드 (데이터베이스 행) 등을 사용 하 여 프로그래밍할 수 있는 작업을 나타냅니다. 개체에는 특성을 설명 하는 속성이 있으며, 텍스트 상자 개체 &#8212; 에 `Text` 속성이 있는지 여부를 읽거나 변경할 수 있습니다. 즉, 요청 개체에는 `Url` 속성이 있고, 메일 메시지에는 `From` 속성이 있으며, 고객 개체에는 `FirstName` 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-159">An *object* represents a thing that you can program with &#8212; a page, a text box, a file, an image, a web request, an email message, a customer record (database row), etc. Objects have properties that describe their characteristics and that you can read or change &#8212; a text box object has a `Text` property (among others), a request object has a `Url` property, an email message has a `From` property, and a customer object has a `FirstName` property.</span></span> <span data-ttu-id="05e9f-160">개체에는 수행할 수&quot; &quot;동사 인 메서드도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-160">Objects also have methods that are the &quot;verbs&quot; they can perform.</span></span> <span data-ttu-id="05e9f-161">예제에는 파일 개체의 `Save` 메서드, 이미지 개체의 `Rotate` 메서드 및 전자 메일 개체의 `Send` 메서드가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-161">Examples include a file object's `Save` method, an image object's `Rotate` method, and an email object's `Send` method.</span></span>

<span data-ttu-id="05e9f-162">페이지의 텍스트 상자 (양식 필드) 값, 요청을 만든 브라우저의 유형, 페이지 URL, 사용자 id 등의 정보를 제공 하는 `Request` 개체로 작업 하는 경우가 많습니다. 다음 예제에서는 `Request` 개체의 속성에 액세스 하는 방법과 서버에서 페이지의 절대 경로를 제공 하는 `Request` 개체의 `MapPath` 메서드를 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-162">You'll often work with the `Request` object, which gives you information like the values of text boxes (form fields) on the page, what type of browser made the request, the URL of the page, the user identity, etc. The following example shows how to access properties of the `Request` object and how to call the `MapPath` method of the `Request` object, which gives you the absolute path of the page on the server:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample9.html)]

<span data-ttu-id="05e9f-163">브라우저에 표시 되는 결과는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-163">The result displayed in a browser:</span></span>

![Razor-Img5](introducing-razor-syntax-c/_static/image5.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a><span data-ttu-id="05e9f-165">8. 결정을 내리는 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-165">8. You can write code that makes decisions</span></span>

<span data-ttu-id="05e9f-166">동적 웹 페이지의 핵심 기능은 조건에 따라 수행할 작업을 결정할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-166">A key feature of dynamic web pages is that you can determine what to do based on conditions.</span></span> <span data-ttu-id="05e9f-167">이 작업을 수행 하는 가장 일반적인 방법은 `if` 문 (및 선택적 `else` 문)을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-167">The most common way to do this is with the `if` statement (and optional `else` statement).</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample10.cshtml)]

<span data-ttu-id="05e9f-168">`if(IsPost)` 문은 `if(IsPost == true)`를 작성 하는 간단한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-168">The statement `if(IsPost)` is a shorthand way of writing `if(IsPost == true)`.</span></span> <span data-ttu-id="05e9f-169">`if` 문과 함께 조건을 테스트 하 고, 코드 블록을 반복 하 고,이 문서의 뒷부분에서 설명 하는 다양 한 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-169">Along with `if` statements, there are a variety of ways to test conditions, repeat blocks of code, and so on, which are described later in this article.</span></span>

<span data-ttu-id="05e9f-170">브라우저에 표시 되는 결과 ( **Submit**를 클릭 한 후):</span><span class="sxs-lookup"><span data-stu-id="05e9f-170">The result displayed in a browser (after clicking **Submit**):</span></span>

![Razor-Img6](introducing-razor-syntax-c/_static/image6.jpg)

> [!TIP] 
> 
> <a id="SB_HttpGetPost"></a>
> ### <a name="http-get-and-post-methods-and-the-ispost-property"></a><span data-ttu-id="05e9f-172">HTTP GET 및 POST 메서드 및 IsPost 속성</span><span class="sxs-lookup"><span data-stu-id="05e9f-172">HTTP GET and POST Methods and the IsPost Property</span></span>
> 
> <span data-ttu-id="05e9f-173">웹 페이지 (HTTP)에 사용 되는 프로토콜은 서버에 대 한 요청을 수행 하는 데 사용 되는 매우 제한 된 수의 메서드 (동사)를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-173">The protocol used for web pages (HTTP) supports a very limited number of methods (verbs) that are used to make requests to the server.</span></span> <span data-ttu-id="05e9f-174">가장 일반적인 두 가지는 페이지를 읽는 데 사용 되는 GET과 페이지를 전송 하는 데 사용 되는 게시물입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-174">The two most common ones are GET, which is used to read a page, and POST, which is used to submit a page.</span></span> <span data-ttu-id="05e9f-175">일반적으로 사용자가 페이지를 처음 요청할 때 페이지는 GET을 사용 하 여 요청 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-175">In general, the first time a user requests a page, the page is requested using GET.</span></span> <span data-ttu-id="05e9f-176">사용자가 양식을 채운 다음 제출 단추를 클릭 하면 브라우저에서 서버에 대 한 POST 요청을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-176">If the user fills in a form and then clicks a submit button, the browser makes a POST request to the server.</span></span>
> 
> <span data-ttu-id="05e9f-177">웹 프로그래밍에서 페이지를 처리 하는 방법을 알 수 있도록 페이지를 GET 또는 POST로 요청 하 고 있는지 여부를 확인 하는 것이 유용한 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-177">In web programming, it's often useful to know whether a page is being requested as a GET or as a POST so that you know how to process the page.</span></span> <span data-ttu-id="05e9f-178">ASP.NET 웹 페이지에서 `IsPost` 속성을 사용 하 여 요청이 GET 또는 POST 인지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-178">In ASP.NET Web Pages, you can use the `IsPost` property to see whether a request is a GET or a POST.</span></span> <span data-ttu-id="05e9f-179">요청이 POST 인 경우 `IsPost` 속성은 true를 반환 하 고 폼에서 텍스트 상자의 값을 읽는 등의 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-179">If the request is a POST, the `IsPost` property will return true, and you can do things like read the values of text boxes on a form.</span></span> <span data-ttu-id="05e9f-180">`IsPost`값에 따라 페이지를 다르게 처리 하는 방법을 보여 주는 많은 예제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-180">Many examples you'll see show you how to process the page differently depending on the value of `IsPost`.</span></span>

## <a name="a-simple-code-example"></a><span data-ttu-id="05e9f-181">간단한 코드 예제</span><span class="sxs-lookup"><span data-stu-id="05e9f-181">A Simple Code Example</span></span>

<span data-ttu-id="05e9f-182">이 절차에서는 기본 프로그래밍 기술을 보여 주는 페이지를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-182">This procedure shows you how to create a page that illustrates basic programming techniques.</span></span> <span data-ttu-id="05e9f-183">이 예제에서는 사용자가 두 개의 숫자를 입력 하 고 그 결과를 추가 하 고 결과를 표시할 수 있는 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-183">In the example, you create a page that lets users enter two numbers, then it adds them and displays the result.</span></span>

1. <span data-ttu-id="05e9f-184">편집기에서 새 파일을 만들고 이름을 *Addnumbers. cshtml*로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-184">In your editor, create a new file and name it *AddNumbers.cshtml*.</span></span>
2. <span data-ttu-id="05e9f-185">페이지에 이미 있는 항목을 대체 하 여 다음 코드와 태그를 페이지에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-185">Copy the following code and markup into the page, replacing anything already in the page.</span></span>  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample11.cshtml)]

    <span data-ttu-id="05e9f-186">유의 해야 할 몇 가지 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-186">Here are some things for you to note:</span></span>

    - <span data-ttu-id="05e9f-187">`@` 문자는 페이지에서 코드의 첫 번째 블록을 시작 하 고 페이지 아래쪽에 포함 된 `totalMessage` 변수 앞에 옵니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-187">The `@` character starts the first block of code in the page, and it precedes the `totalMessage` variable that's embedded near the bottom of the page.</span></span>
    - <span data-ttu-id="05e9f-188">페이지 맨 위에 있는 블록은 중괄호로 묶여 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-188">The block at the top of the page is enclosed in braces.</span></span>
    - <span data-ttu-id="05e9f-189">위쪽의 블록에서 모든 줄은 세미콜론으로 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-189">In the block at the top, all lines end with a semicolon.</span></span>
    - <span data-ttu-id="05e9f-190">변수 `total`, `num1`, `num2`및 `totalMessage`에는 여러 숫자와 문자열이 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-190">The variables `total`, `num1`, `num2`, and `totalMessage` store several numbers and a string.</span></span>
    - <span data-ttu-id="05e9f-191">`totalMessage` 변수에 할당 된 리터럴 문자열 값이 큰따옴표로 묶여 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-191">The literal string value assigned to the `totalMessage` variable is in double quotation marks.</span></span>
    - <span data-ttu-id="05e9f-192">코드는 대/소문자를 구분 하므로 `totalMessage` 변수를 페이지의 아래쪽 근처에 사용 하는 경우 해당 이름이 위쪽의 변수와 정확히 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-192">Because the code is case-sensitive, when the `totalMessage` variable is used near the bottom of the page, its name must match the variable at the top exactly.</span></span>
    - <span data-ttu-id="05e9f-193">식 `num1.AsInt() + num2.AsInt()`는 개체 및 메서드를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-193">The expression `num1.AsInt() + num2.AsInt()` shows how to work with objects and methods.</span></span> <span data-ttu-id="05e9f-194">각 변수의 `AsInt` 메서드는 사용자가 입력 한 문자열을 숫자 (정수)로 변환 하 여 산술 연산을 수행할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-194">The `AsInt` method on each variable converts the string entered by a user to a number (an integer) so that you can perform arithmetic on it.</span></span>
    - <span data-ttu-id="05e9f-195">`<form>` 태그는 `method="post"` 특성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-195">The `<form>` tag includes a `method="post"` attribute.</span></span> <span data-ttu-id="05e9f-196">이렇게 하면 사용자가 **추가**를 클릭 하면 HTTP POST 메서드를 사용 하 여 페이지가 서버에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-196">This specifies that when the user clicks **Add**, the page will be sent to the server using the HTTP POST method.</span></span> <span data-ttu-id="05e9f-197">페이지가 제출 되 면 `if(IsPost)` 테스트가 true로 평가 되 고 조건부 코드가 실행 되어 숫자를 더한 결과를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-197">When the page is submitted, the `if(IsPost)` test evaluates to true and the conditional code runs, displaying the result of adding the numbers.</span></span>
3. <span data-ttu-id="05e9f-198">페이지를 저장 하 고 브라우저에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-198">Save the page and run it in a browser.</span></span> <span data-ttu-id="05e9f-199">(파일을 실행 하기 전에 해당 페이지가 **파일** 작업 영역에서 선택 되어 있는지 확인 합니다.) 두 개의 정수를 입력 한 다음 **추가** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-199">(Make sure the page is selected in the **Files** workspace before you run it.) Enter two whole numbers and then click the **Add** button.</span></span> 

    ![Razor-Img7](introducing-razor-syntax-c/_static/image7.jpg)

## <a name="basic-programming-concepts"></a><span data-ttu-id="05e9f-201">기본 프로그래밍 개념</span><span class="sxs-lookup"><span data-stu-id="05e9f-201">Basic Programming Concepts</span></span>

<span data-ttu-id="05e9f-202">이 문서에서는 ASP.NET 웹 프로그래밍에 대 한 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-202">This article provides you with an overview of ASP.NET web programming.</span></span> <span data-ttu-id="05e9f-203">가장 자주 사용 하는 프로그래밍 개념을 간략히 살펴보고 철저 하 게 조사 하는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-203">It isn't an exhaustive examination, just a quick tour through the programming concepts you'll use most often.</span></span> <span data-ttu-id="05e9f-204">심지어는 ASP.NET 웹 페이지을 시작 하는 데 필요한 거의 모든 것을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-204">Even so, it covers almost everything you'll need to get started with ASP.NET Web Pages.</span></span>

<span data-ttu-id="05e9f-205">하지만 첫 번째는 약간 기술적인 배경입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-205">But first, a little technical background.</span></span>

### <a name="the-razor-syntax-server-code-and-aspnet"></a><span data-ttu-id="05e9f-206">Razor 구문, 서버 코드 및 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="05e9f-206">The Razor Syntax, Server Code, and ASP.NET</span></span>

<span data-ttu-id="05e9f-207">Razor 구문는 웹 페이지에 서버 기반 코드를 포함 하는 간단한 프로그래밍 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-207">Razor syntax is a simple programming syntax for embedding server-based code in a web page.</span></span> <span data-ttu-id="05e9f-208">Razor 구문를 사용 하는 웹 페이지에는 두 가지 종류의 콘텐츠, 즉 클라이언트 콘텐츠와 서버 코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-208">In a web page that uses the Razor syntax, there are two kinds of content: client content and server code.</span></span> <span data-ttu-id="05e9f-209">클라이언트 콘텐츠는 HTML 태그 (요소), CSS와 같은 스타일 정보, JavaScript와 같은 일부 클라이언트 스크립트, 일반 텍스트 등의 웹 페이지에서 사용 하는 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-209">Client content is the stuff you're used to in web pages: HTML markup (elements), style information such as CSS, maybe some client script such as JavaScript, and plain text.</span></span>

<span data-ttu-id="05e9f-210">Razor 구문를 사용 하 여이 클라이언트 콘텐츠에 서버 코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-210">Razor syntax lets you add server code to this client content.</span></span> <span data-ttu-id="05e9f-211">페이지에 서버 코드가 있으면 서버는 해당 코드를 먼저 실행 한 다음 페이지를 브라우저로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-211">If there's server code in the page, the server runs that code first, before it sends the page to the browser.</span></span> <span data-ttu-id="05e9f-212">서버에서를 실행 하는 경우 코드에서 서버 기반 데이터베이스에 액세스 하는 것과 같이 클라이언트 콘텐츠를 사용 하는 것 보다 복잡 한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-212">By running on the server, the code can perform tasks that can be a lot more complex to do using client content alone, like accessing server-based databases.</span></span> <span data-ttu-id="05e9f-213">가장 중요 한 점은 서버 코드에서 동적으로 클라이언트 &#8212; 콘텐츠를 만들 수 있으며, 즉석에서 HTML 태그나 기타 콘텐츠를 생성 한 다음 페이지에 포함 될 수 있는 정적 HTML과 함께 브라우저에 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-213">Most importantly, server code can dynamically create client content &#8212; it can generate HTML markup or other content on the fly and then send it to the browser along with any static HTML that the page might contain.</span></span> <span data-ttu-id="05e9f-214">브라우저의 관점에서 보면 서버 코드에서 생성 되는 클라이언트 콘텐츠는 다른 클라이언트 콘텐츠와 다르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-214">From the browser's perspective, client content that's generated by your server code is no different than any other client content.</span></span> <span data-ttu-id="05e9f-215">앞서 살펴본 것 처럼 필요한 서버 코드는 매우 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-215">As you've already seen, the server code that's required is quite simple.</span></span>

<span data-ttu-id="05e9f-216">Razor 구문를 포함 하는 ASP.NET 웹 페이지에는 특수 한 파일 확장명 (cshtml *또는*)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-216">ASP.NET web pages that include the Razor syntax have a special file extension (*.cshtml* or *.vbhtml*).</span></span> <span data-ttu-id="05e9f-217">서버는 이러한 확장을 인식 하 고 Razor 구문 표시 된 코드를 실행 한 다음 페이지를 브라우저로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-217">The server recognizes these extensions, runs the code that's marked with Razor syntax, and then sends the page to the browser.</span></span>

### <a name="where-does-aspnet-fit-in"></a><span data-ttu-id="05e9f-218">ASP.NET는 어디에 있나요?</span><span class="sxs-lookup"><span data-stu-id="05e9f-218">Where does ASP.NET fit in?</span></span>

<span data-ttu-id="05e9f-219">Razor 구문는 Microsoft에서 ASP.NET 이라는 기술을 기반으로 하며,이는 차례로 Microsoft .NET 프레임 워크를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-219">Razor syntax is based on a technology from Microsoft called ASP.NET, which in turn is based on the Microsoft .NET Framework.</span></span> <span data-ttu-id="05e9f-220">The.NET Framework는 거의 모든 종류의 컴퓨터 응용 프로그램을 개발 하기 위한 Microsoft의 대규모의 포괄적인 프로그래밍 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-220">The.NET Framework is a big, comprehensive programming framework from Microsoft for developing virtually any type of computer application.</span></span> <span data-ttu-id="05e9f-221">ASP.NET는 웹 응용 프로그램을 만들기 위해 특별히 설계 된 .NET Framework의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-221">ASP.NET is the part of the .NET Framework that's specifically designed for creating web applications.</span></span> <span data-ttu-id="05e9f-222">개발자는 ASP.NET를 사용 하 여 전 세계에서 가장 크고 트래픽이 많은 웹 사이트를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-222">Developers have used ASP.NET to create many of the largest and highest-traffic websites in the world.</span></span> <span data-ttu-id="05e9f-223">사이트에서 URL의 일부로 파일 이름 확장명 *.aspx* 가 표시 될 때마다 ASP.NET를 사용 하 여 사이트를 작성 한 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-223">(Any time you see the file-name extension *.aspx* as part of the URL in a site, you'll know that the site was written using ASP.NET.)</span></span>

<span data-ttu-id="05e9f-224">Razor 구문는 ASP.NET의 모든 기능을 제공 하지만 초보자 인 경우 더 쉽게 배울 수 있는 간소화 된 구문을 사용 하 여 생산성을 높여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-224">The Razor syntax gives you all the power of ASP.NET, but using a simplified syntax that's easier to learn if you're a beginner and that makes you more productive if you're an expert.</span></span> <span data-ttu-id="05e9f-225">이 구문을 사용 하는 것은 간단 하지만 ASP.NET 및 .NET Framework에 대 한 패밀리 관계는 웹 사이트가 더 정교 해지면 사용할 수 있는 더 큰 프레임 워크의 강력한 기능을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-225">Even though this syntax is simple to use, its family relationship to ASP.NET and the .NET Framework means that as your websites become more sophisticated, you have the power of the larger frameworks available to you.</span></span>

![Razor-Img8](introducing-razor-syntax-c/_static/image8.jpg)

> [!TIP] 
> 
> <span data-ttu-id="05e9f-227">**클래스 및 인스턴스**</span><span class="sxs-lookup"><span data-stu-id="05e9f-227">**Classes and Instances**</span></span>
> 
> <span data-ttu-id="05e9f-228">ASP.NET 서버 코드는 개체를 사용 하며,이는 클래스 개념을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-228">ASP.NET server code uses objects, which are in turn built on the idea of classes.</span></span> <span data-ttu-id="05e9f-229">클래스는 개체에 대 한 정의 또는 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-229">The class is the definition or template for an object.</span></span> <span data-ttu-id="05e9f-230">예를 들어 응용 프로그램에는 고객 개체가 필요로 하는 속성과 메서드를 정의 하는 `Customer` 클래스가 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-230">For example, an application might contain a `Customer` class that defines the properties and methods that any customer object needs.</span></span>
> 
> <span data-ttu-id="05e9f-231">응용 프로그램이 실제 고객 정보를 사용 해야 하는 경우 고객 개체의 인스턴스를 만듭니다 (또는 *인스턴스화*).</span><span class="sxs-lookup"><span data-stu-id="05e9f-231">When the application needs to work with actual customer information, it creates an instance of (or *instantiates*) a customer object.</span></span> <span data-ttu-id="05e9f-232">각 개별 고객은 `Customer` 클래스의 개별 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-232">Each individual customer is a separate instance of the `Customer` class.</span></span> <span data-ttu-id="05e9f-233">모든 인스턴스는 동일한 속성 및 메서드를 지원 하지만 각 고객 개체는 고유 하기 때문에 각 인스턴스에 대 한 속성 값은 일반적으로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-233">Every instance supports the same properties and methods, but the property values for each instance are typically different, because each customer object is unique.</span></span> <span data-ttu-id="05e9f-234">한 고객 개체에서 `LastName` 속성은 "Smith" 일 수 있습니다. 다른 customer 개체에서 `LastName` 속성은 "Jones" 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-234">In one customer object, the `LastName` property might be "Smith"; in another customer object, the `LastName` property might be "Jones."</span></span>
> 
> <span data-ttu-id="05e9f-235">마찬가지로, 사이트의 개별 웹 페이지는 `Page` 클래스 인스턴스인 `Page` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-235">Similarly, any individual web page in your site is a `Page` object that's an instance of the `Page` class.</span></span> <span data-ttu-id="05e9f-236">페이지의 단추는 `Button` 클래스의 인스턴스인 `Button` 개체 등입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-236">A button on the page is a `Button` object that is an instance of the `Button` class, and so on.</span></span> <span data-ttu-id="05e9f-237">각 인스턴스에는 고유한 특징이 있지만 모두 개체의 클래스 정의에 지정 된 항목을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-237">Each instance has its own characteristics, but they all are based on what's specified in the object's class definition.</span></span>

## <a name="basic-syntax"></a><span data-ttu-id="05e9f-238">기본 구문</span><span class="sxs-lookup"><span data-stu-id="05e9f-238">Basic Syntax</span></span>

<span data-ttu-id="05e9f-239">앞서 ASP.NET 웹 페이지 페이지를 만드는 방법의 기본 예제와 HTML 태그에 서버 코드를 추가 하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-239">Earlier you saw a basic example of how to create an ASP.NET Web Pages page, and how you can add server code to HTML markup.</span></span> <span data-ttu-id="05e9f-240">여기서는 Razor 구문 &#8212; 프로그래밍 언어 규칙을 사용 하 여 ASP.NET 서버 코드를 작성 하는 기본 사항을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-240">Here you'll learn the basics of writing ASP.NET server code using the Razor syntax &#8212; that is, the programming language rules.</span></span>

<span data-ttu-id="05e9f-241">프로그래밍 경험이 있는 경우 (특히 C, C++, C#, Visual Basic 또는 JavaScript를 사용 하는 경우) 여기에서 읽는 많은 내용이 익숙할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-241">If you're experienced with programming (especially if you've used C, C++, C#, Visual Basic, or JavaScript), much of what you read here will be familiar.</span></span> <span data-ttu-id="05e9f-242">서버 코드를 *. cshtml* 파일의 태그에 추가 하는 방법만 숙지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-242">You'll probably need to familiarize yourself only with how server code is added to markup in *.cshtml* files.</span></span>

<a id="BM_CombiningTextMarkupAndCode"></a>
### <a name="combining-text-markup-and-code-in-code-blocks"></a><span data-ttu-id="05e9f-243">코드 블록에서 텍스트, 태그 및 코드 결합</span><span class="sxs-lookup"><span data-stu-id="05e9f-243">Combining Text, Markup, and Code in Code Blocks</span></span>

<span data-ttu-id="05e9f-244">서버 코드 블록에서 텍스트 또는 태그 (또는 둘 다)를 페이지에 출력 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-244">In server code blocks, you often want to output text or markup (or both) to the page.</span></span> <span data-ttu-id="05e9f-245">서버 코드 블록에 코드가 아닌 텍스트가 포함 되어 있는 경우 해당 텍스트를 그대로 렌더링 해야 하는 경우 ASP.NET는 해당 텍스트를 코드와 구별할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-245">If a server code block contains text that's not code and that instead should be rendered as is, ASP.NET needs to be able to distinguish that text from code.</span></span> <span data-ttu-id="05e9f-246">다음과 같은 여러 가지 방법으로 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-246">There are several ways to do this.</span></span>

- <span data-ttu-id="05e9f-247">`<p></p>` 또는 `<em></em>`같은 HTML 요소로 텍스트를 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-247">Enclose the text in an HTML element like `<p></p>` or `<em></em>`:</span></span>   

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample12.cshtml)]

    <span data-ttu-id="05e9f-248">HTML 요소에는 텍스트, 추가 HTML 요소 및 서버 코드 식이 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-248">The HTML element can include text, additional HTML elements, and server-code expressions.</span></span> <span data-ttu-id="05e9f-249">ASP.NET 여는 HTML 태그 (예: `<p>`)를 볼 때 요소와 해당 콘텐츠를 포함 하는 모든 항목을 브라우저에 그대로 렌더링 하 여 서버 코드 식이 이동 하는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-249">When ASP.NET sees the opening HTML tag (for example, `<p>`), it renders everything including the element and its content as is to the browser, resolving server-code expressions as it goes.</span></span>
- <span data-ttu-id="05e9f-250">`@:` 연산자 또는 `<text>` 요소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-250">Use the `@:` operator or the `<text>` element.</span></span> <span data-ttu-id="05e9f-251">`@:`는 일반 텍스트 또는 일치 하지 않는 HTML 태그를 포함 하는 단일 내용의 줄을 출력 합니다. `<text>` 요소는 여러 줄을 출력으로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-251">The `@:` outputs a single line of content containing plain text or unmatched HTML tags; the `<text>` element encloses multiple lines to output.</span></span> <span data-ttu-id="05e9f-252">이러한 옵션은 HTML 요소를 출력의 일부로 렌더링 하지 않으려는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-252">These options are useful when you don't want to render an HTML element as part of the output.</span></span>  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample13.cshtml)]

    <span data-ttu-id="05e9f-253">여러 줄의 텍스트 또는 일치 하지 않는 HTML 태그를 출력 하려면 각 줄 앞에 `@:`를 사용 하거나 `<text>` 요소에 줄을 묶을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-253">If you want to output multiple lines of text or unmatched HTML tags, you can precede each line with `@:`, or you can enclose the line in a `<text>` element.</span></span> <span data-ttu-id="05e9f-254">`@:` 연산자와 마찬가지로`<text>` 태그는 ASP.NET에서 텍스트 콘텐츠를 식별 하는 데 사용 되며 페이지 출력에서 렌더링 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-254">Like the `@:` operator,`<text>` tags are used by ASP.NET to identify text content and are never rendered in the page output.</span></span>

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample14.cshtml)]

    <span data-ttu-id="05e9f-255">첫 번째 예제에서는 이전 예제를 반복 하지만 단일 쌍의 `<text>` 태그를 사용 하 여 렌더링할 텍스트를 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-255">The first example repeats the previous example but uses a single pair of `<text>` tags to enclose the text to render.</span></span> <span data-ttu-id="05e9f-256">두 번째 예제에서 `<text>` 및 `</text>` 태그는 세 줄을 포함 하며, 모든 줄에는 포함 되지 않은 텍스트와 일치 하지 않는 HTML 태그 (`<br />`)가 서버 코드 및 일치 하는 HTML 태그와 함께 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-256">In the second example, the `<text>` and `</text>` tags enclose three lines, all of which have some uncontained text and unmatched HTML tags (`<br />`), along with server code and matched HTML tags.</span></span> <span data-ttu-id="05e9f-257">또한 각 줄 앞에 `@:` 연산자를 사용 하 여 개별적으로 추가할 수 있습니다. 어떤 방법이 든 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-257">Again, you could also precede each line individually with the `@:` operator; either way works.</span></span>

    > [!NOTE]
    > <span data-ttu-id="05e9f-258">HTML 요소를 사용 하 여이 섹션 &#8212; 에 표시 된 대로 텍스트를 출력 하는 경우 `@:` 연산자 또는 `<text>` &#8212; 요소 ASP.NET은 출력을 html로 인코딩하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-258">When you output text as shown in this section &#8212; using an HTML element, the `@:` operator, or the `<text>` element &#8212; ASP.NET doesn't HTML-encode the output.</span></span> <span data-ttu-id="05e9f-259">앞에서 설명한 것 처럼 ASP.NET는이 섹션에 설명 된 특수 한 사례를 제외 하 고 `@`뒤에 오는 서버 코드 식과 서버 코드 블록의 출력을 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-259">(As noted earlier, ASP.NET does encode the output of server code expressions and server code blocks that are preceded by `@`, except in the special cases noted in this section.)</span></span>

### <a name="whitespace"></a><span data-ttu-id="05e9f-260">Whitespace</span><span class="sxs-lookup"><span data-stu-id="05e9f-260">Whitespace</span></span>

<span data-ttu-id="05e9f-261">문 (및 문자열 리터럴 외부)의 추가 공백은 문에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-261">Extra spaces in a statement (and outside of a string literal) don't affect the statement:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample15.cshtml)]

<span data-ttu-id="05e9f-262">문의 줄 바꿈은 문에 영향을 주지 않으며 가독성을 위해 문을 래핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-262">A line break in a statement has no effect on the statement, and you can wrap statements for readability.</span></span> <span data-ttu-id="05e9f-263">다음 문은 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-263">The following statements are the same:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample16.cshtml)]

<span data-ttu-id="05e9f-264">그러나 문자열 리터럴 중간에 줄을 줄 바꿈할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-264">However, you can't wrap a line in the middle of a string literal.</span></span> <span data-ttu-id="05e9f-265">다음 예는 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-265">The following example doesn't work:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample17.cshtml)]

<span data-ttu-id="05e9f-266">위의 코드와 같이 여러 줄로 래핑하는 긴 문자열을 결합 하려면 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-266">To combine a long string that wraps to multiple lines like the above code, there are two options.</span></span> <span data-ttu-id="05e9f-267">연결 연산자 (`+`)를 사용할 수 있습니다 .이에 대해서는이 문서의 뒷부분에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-267">You can use the concatenation operator (`+`), which you'll see later in this article.</span></span> <span data-ttu-id="05e9f-268">이 문서의 앞부분에서 살펴본 것 처럼 `@` 문자를 사용 하 여 축 자 문자열 리터럴을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-268">You can also use the `@` character to create a verbatim string literal, as you saw earlier in this article.</span></span> <span data-ttu-id="05e9f-269">약어 문자열 리터럴은 줄 전체로 나눌 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-269">You can break verbatim string literals across lines:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample18.cshtml)]

### <a name="code-and-markup-comments"></a><span data-ttu-id="05e9f-270">코드 및 태그 설명</span><span class="sxs-lookup"><span data-stu-id="05e9f-270">Code (and Markup) Comments</span></span>

<span data-ttu-id="05e9f-271">주석을 사용 하 여 자신에 게 메모를 남길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-271">Comments let you leave notes for yourself or others.</span></span> <span data-ttu-id="05e9f-272">또한 실행 하지 않으려는 코드 또는 태그 섹션을 사용 하지 않도록 설정 (*주석으로 처리*) 할 수 있지만 페이지에 유지 하려는 경우</span><span class="sxs-lookup"><span data-stu-id="05e9f-272">They also allow you to disable (*comment out*) a section of code or markup that you don't want to run but want to keep in your page for the time being.</span></span>

<span data-ttu-id="05e9f-273">Razor 코드 및 HTML 태그에 대 한 다양 한 주석 달기 구문이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-273">There's different commenting syntax for Razor code and for HTML markup.</span></span> <span data-ttu-id="05e9f-274">모든 Razor 코드와 마찬가지로 페이지가 브라우저에 전송 되기 전에 서버에서 Razor 주석이 처리 된 후 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-274">As with all Razor code, Razor comments are processed (and then removed) on the server before the page is sent to the browser.</span></span> <span data-ttu-id="05e9f-275">따라서 Razor 주석 구문을 사용 하면 파일을 편집할 때 볼 수 있는 코드 또는 태그에 주석을 추가할 수 있지만, 페이지 소스에도 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-275">Therefore, the Razor commenting syntax lets you put comments into the code (or even into the markup) that you can see when you edit the file, but that users don't see, even in the page source.</span></span>

<span data-ttu-id="05e9f-276">ASP.NET Razor 주석의 경우 `@*`를 사용 하 여 주석을 시작 하 고 `*@`로 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-276">For ASP.NET Razor comments, you start the comment with `@*` and end it with `*@`.</span></span> <span data-ttu-id="05e9f-277">주석은 한 줄 또는 여러 줄에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-277">The comment can be on one line or multiple lines:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample19.cshtml)]

<span data-ttu-id="05e9f-278">다음은 코드 블록 내의 주석입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-278">Here is a comment within a code block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample20.cshtml)]

<span data-ttu-id="05e9f-279">다음은 코드 줄을 주석으로 처리 하 여 실행 되지 않도록 코드를 주석으로 처리 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-279">Here is the same block of code, with the line of code commented out so that it won't run:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample21.cshtml)]

<span data-ttu-id="05e9f-280">코드 블록 내에서 Razor 주석 구문을 사용 하는 대신 사용 중인 프로그래밍 언어의 주석 구문 (예 C#:)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-280">Inside a code block, as an alternative to using Razor comment syntax, you can use the commenting syntax of the programming language you're using, such as C#:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample22.cshtml)]

<span data-ttu-id="05e9f-281">에서 C#한 줄로 된 주석에는 `//` 문자가 오고, 여러 줄 주석은 `/*`로 시작 하 고 `*/`로 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-281">In C#, single-line comments are preceded by the `//` characters, and multi-line comments begin with `/*` and end with `*/`.</span></span> <span data-ttu-id="05e9f-282">Razor 주석과 마찬가지로 C# 주석은 브라우저에 렌더링 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-282">(As with Razor comments, C# comments are not rendered to the browser.)</span></span>

<span data-ttu-id="05e9f-283">태그에 대해 아시다시피 HTML 주석을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-283">For markup, as you probably know, you can create an HTML comment:</span></span>

[!code-xml[Main](introducing-razor-syntax-c/samples/sample23.xml)]

<span data-ttu-id="05e9f-284">HTML 주석은 `<!--` 문자로 시작 하 고 `-->`로 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-284">HTML comments start with `<!--` characters and end with `-->`.</span></span> <span data-ttu-id="05e9f-285">HTML 주석을 사용 하 여 텍스트 뿐만 아니라 페이지에 유지 하지만 렌더링 하지 않으려는 HTML 태그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-285">You can use HTML comments to surround not only text, but also any HTML markup that you may want to keep in the page but don't want to render.</span></span> <span data-ttu-id="05e9f-286">이 HTML 주석은 태그의 전체 내용과 여기에 포함 되는 텍스트를 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-286">This HTML comment will hide the entire content of the tags and the text they contain:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample24.html)]

<span data-ttu-id="05e9f-287">Razor 주석과 달리 HTML 주석은 페이지 *에 렌더링 되며* 사용자는 페이지 소스를 확인 하 여 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-287">Unlike Razor comments, HTML comments *are* rendered to the page and the user can see them by viewing the page source.</span></span>

<span data-ttu-id="05e9f-288">Razor에는의 C#중첩 된 블록에 대 한 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-288">Razor has limitations on nested blocks of C#.</span></span> <span data-ttu-id="05e9f-289">자세한 내용은 [명명 된 변수 C# 및 중첩 블록에서 손상 된 코드 생성을](http://aspnetwebstack.codeplex.com/workitem/1914) 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="05e9f-289">For more information see [Named C# Variables and Nested Blocks Generate Broken Code](http://aspnetwebstack.codeplex.com/workitem/1914)</span></span>

## <a name="variables"></a><span data-ttu-id="05e9f-290">변수</span><span class="sxs-lookup"><span data-stu-id="05e9f-290">Variables</span></span>

<span data-ttu-id="05e9f-291">변수는 데이터를 저장 하는 데 사용 하는 명명 된 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-291">A variable is a named object that you use to store data.</span></span> <span data-ttu-id="05e9f-292">변수 이름을 지정할 수 있지만 이름은 영문자로 시작 해야 하며 공백 또는 예약 문자를 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-292">You can name variables anything, but the name must begin with an alphabetic character and it cannot contain whitespace or reserved characters.</span></span>

### <a name="variables-and-data-types"></a><span data-ttu-id="05e9f-293">변수 및 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="05e9f-293">Variables and Data Types</span></span>

<span data-ttu-id="05e9f-294">변수에는 변수에 저장 되는 데이터의 종류를 나타내는 특정 데이터 형식이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-294">A variable can have a specific data type, which indicates what kind of data is stored in the variable.</span></span> <span data-ttu-id="05e9f-295">문자열 값 (&quot;예: Hello 세계&quot;), 정수 값 (예: 3 또는 79)을 저장 하는 정수 변수, 날짜 값을 다양 한 형식 (예: 4/12/2012 또는 3 월 2009)으로 저장 하는 날짜 변수를 저장 하는 문자열 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-295">You can have string variables that store string values (like &quot;Hello world&quot;), integer variables that store whole-number values (like 3 or 79), and date variables that store date values in a variety of formats (like 4/12/2012 or March 2009).</span></span> <span data-ttu-id="05e9f-296">사용할 수 있는 다른 많은 데이터 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-296">And there are many other data types you can use.</span></span>

<span data-ttu-id="05e9f-297">그러나 일반적으로 변수의 형식을 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-297">However, you generally don't have to specify a type for a variable.</span></span> <span data-ttu-id="05e9f-298">대부분의 경우 ASP.NET는 변수의 데이터를 사용 하는 방법에 따라 형식을 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-298">Most of the time, ASP.NET can figure out the type based on how the data in the variable is being used.</span></span> <span data-ttu-id="05e9f-299">때로는 형식을 지정 해야 합니다 .이 경우에는 예제가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-299">(Occasionally you must specify a type; you'll see examples where this is true.)</span></span>

<span data-ttu-id="05e9f-300">`var` 키워드 (형식을 지정 하지 않을 경우)를 사용 하거나 형식의 이름을 사용 하 여 변수를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-300">You declare a variable using the `var` keyword (if you don't want to specify a type) or by using the name of the type:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample25.cshtml)]

<span data-ttu-id="05e9f-301">다음 예제에서는 웹 페이지에서 일반적으로 사용 되는 변수의 몇 가지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-301">The following example shows some typical uses of variables in a web page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample26.cshtml)]

<span data-ttu-id="05e9f-302">페이지에서 이전 예제를 결합 하는 경우 브라우저에 표시 되는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-302">If you combine the previous examples in a page, you see this displayed in a browser:</span></span>

![Razor-Img9](introducing-razor-syntax-c/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a><span data-ttu-id="05e9f-304">데이터 형식 변환 및 테스트</span><span class="sxs-lookup"><span data-stu-id="05e9f-304">Converting and Testing Data Types</span></span>

<span data-ttu-id="05e9f-305">ASP.NET는 일반적으로 데이터 형식을 자동으로 결정할 수 있지만 경우에 따라 자동으로 데이터 형식을 결정할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-305">Although ASP.NET can usually determine a data type automatically, sometimes it can't.</span></span> <span data-ttu-id="05e9f-306">따라서 명시적 변환을 수행 하 여 ASP.NET를 지원 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-306">Therefore, you might need to help ASP.NET out by performing an explicit conversion.</span></span> <span data-ttu-id="05e9f-307">형식을 변환 하지 않아도 되는 경우에도 사용할 수 있는 데이터 형식을 테스트 하는 것이 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-307">Even if you don't have to convert types, sometimes it's helpful to test to see what type of data you might be working with.</span></span>

<span data-ttu-id="05e9f-308">가장 일반적인 경우는 문자열을 정수 또는 날짜와 같은 다른 형식으로 변환 해야 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-308">The most common case is that you have to convert a string to another type, such as to an integer or date.</span></span> <span data-ttu-id="05e9f-309">다음 예에서는 문자열을 숫자로 변환 해야 하는 일반적인 경우를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-309">The following example shows a typical case where you must convert a string to a number.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample27.cshtml)]

<span data-ttu-id="05e9f-310">사용자 입력은 사용자가 문자열로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-310">As a rule, user input comes to you as strings.</span></span> <span data-ttu-id="05e9f-311">사용자에 게 숫자를 입력 하 라는 메시지가 표시 되 고 숫자를 입력 한 경우에도 사용자 입력이 제출 되 고 코드에서이를 읽으면 데이터는 문자열 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-311">Even if you've prompted users to enter a number, and even if they've entered a digit, when user input is submitted and you read it in code, the data is in string format.</span></span> <span data-ttu-id="05e9f-312">따라서 문자열을 숫자로 변환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-312">Therefore, you must convert the string to a number.</span></span> <span data-ttu-id="05e9f-313">예를 들어 값을 변환 하지 않고 값에 대해 산술 연산을 수행 하려고 하면 ASP.NET에서 두 개의 문자열을 추가할 수 없기 때문에 다음과 같은 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-313">In the example, if you try to perform arithmetic on the values without converting them, the following error results, because ASP.NET cannot add two strings:</span></span>

<span data-ttu-id="05e9f-314">*' String ' 형식을 ' i n t '로 암시적으로 변환할 수 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="05e9f-314">*Cannot implicitly convert type 'string' to 'int'.*</span></span>

<span data-ttu-id="05e9f-315">값을 정수로 변환 하려면 `AsInt` 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-315">To convert the values to integers, you call the `AsInt` method.</span></span> <span data-ttu-id="05e9f-316">성공적으로 변환 되 면 숫자를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-316">If the conversion is successful, you can then add the numbers.</span></span>

<span data-ttu-id="05e9f-317">다음 표에서는 변수에 대 한 몇 가지 일반적인 변환과 테스트 메서드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-317">The following table lists some common conversion and test methods for variables.</span></span>

:::row:::
    :::column:::
    <span data-ttu-id="05e9f-318"><strong>메서드</strong></span><span class="sxs-lookup"><span data-stu-id="05e9f-318"><strong>Method</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="05e9f-319"><strong>설명</strong></span><span class="sxs-lookup"><span data-stu-id="05e9f-319"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="05e9f-320"><strong>예</strong></span><span class="sxs-lookup"><span data-stu-id="05e9f-320"><strong>Example</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="05e9f-321">정수 값 (예: "593")을 나타내는 문자열을 정수로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-321">Converts a string that represents a whole number (like "593") to an integer.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample28.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsBool(), IsBool()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="05e9f-322">&quot;true&quot; 또는 &quot;false&quot; 같은 문자열을 부울 형식으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-322">Converts a string like &quot;true&quot; or &quot;false&quot; to a Boolean type.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample29.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsFloat(), IsFloat()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="05e9f-323">&quot;1.3&quot; 또는 &quot;7.439&quot; 같은 10 진수 값을 포함 하는 문자열을 부동 소수점 숫자로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-323">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a floating-point number.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample30.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDecimal(), IsDecimal()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="05e9f-324">&quot;1.3&quot; 또는 &quot;7.439&quot; 같은 10 진수 값이 있는 문자열을 10 진수로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-324">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a decimal number.</span></span> <span data-ttu-id="05e9f-325">ASP.NET에서 10 진수는 부동 소수점 숫자 보다 더 정확 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-325">(In ASP.NET, a decimal number is more precise than a floating-point number.)</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample31.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDateTime(), IsDateTime()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="05e9f-326">날짜 및 시간 값을 나타내는 문자열을 ASP.NET `DateTime` 형식으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-326">Converts a string that represents a date and time value to the ASP.NET `DateTime` type.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample32.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `ToString()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="05e9f-327">다른 모든 데이터 형식을 문자열로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-327">Converts any other data type to a string.</span></span>
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample33.js)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a><span data-ttu-id="05e9f-328">연산자</span><span class="sxs-lookup"><span data-stu-id="05e9f-328">Operators</span></span>

<span data-ttu-id="05e9f-329">연산자는 식에서 수행할 명령의 종류를 ASP.NET 알려 주는 키워드 또는 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-329">An operator is a keyword or character that tells ASP.NET what kind of command to perform in an expression.</span></span> <span data-ttu-id="05e9f-330">언어 C# (및이를 기반으로 하는 Razor 구문)는 많은 연산자를 지원 하지만 시작 하기 위해 몇 가지를 인식 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-330">The C# language (and the Razor syntax that's based on it) supports many operators, but you only need to recognize a few to get started.</span></span> <span data-ttu-id="05e9f-331">다음 표에서는 가장 일반적인 연산자를 요약 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-331">The following table summarizes the most common operators.</span></span>

:::row:::
    :::column:::
    <span data-ttu-id="05e9f-332"><strong>Operator</strong></span><span class="sxs-lookup"><span data-stu-id="05e9f-332"><strong>Operator</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="05e9f-333"><strong>설명</strong></span><span class="sxs-lookup"><span data-stu-id="05e9f-333"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="05e9f-334"><strong>예제</strong></span><span class="sxs-lookup"><span data-stu-id="05e9f-334"><strong>Examples</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        <span data-ttu-id="05e9f-335">`+` `-` `*` `/`</span><span class="sxs-lookup"><span data-stu-id="05e9f-335">`+` `-` `*` `/`</span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="05e9f-336">숫자 식에 사용 되는 수학 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-336">Math operators used in numerical expressions.</span></span>
    :::column-end:::
    :::column:::
        [!code-css[Main](introducing-razor-syntax-c/samples/sample34.css)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="05e9f-337">할당.</span><span class="sxs-lookup"><span data-stu-id="05e9f-337">Assignment.</span></span> <span data-ttu-id="05e9f-338">문의 오른쪽에 있는 값을 좌 변에 있는 개체에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-338">Assigns the value on the right side of a statement to the object on the left side.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample35.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `==`
    :::column-end:::
    :::column:::
    <span data-ttu-id="05e9f-339">같음</span><span class="sxs-lookup"><span data-stu-id="05e9f-339">Equality.</span></span> <span data-ttu-id="05e9f-340">값이 같으면 `true`을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-340">Returns `true` if the values are equal.</span></span> <span data-ttu-id="05e9f-341">`=` 연산자와 `==` 연산자의 차이를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-341">(Notice the distinction between the `=` operator and the `==` operator.)</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample36.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="05e9f-342">같지 않음</span><span class="sxs-lookup"><span data-stu-id="05e9f-342">Inequality.</span></span> <span data-ttu-id="05e9f-343">값이 같지 않으면 `true`을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-343">Returns `true` if the values are not equal.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample37.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="05e9f-344">보다 작음, 보다 큼, 보다 작음, 작거나 같음, 크거나 같음.</span><span class="sxs-lookup"><span data-stu-id="05e9f-344">Less-than, greater-than, less-than-or-equal, and greater-than-or-equal.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample38.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+`
    :::column-end:::
    :::column:::
    <span data-ttu-id="05e9f-345">연결-문자열을 조인 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-345">Concatenation, which is used to join strings.</span></span> <span data-ttu-id="05e9f-346">ASP.NET는이 연산자와 식의 데이터 형식에 따라 더하기 연산자의 차이를 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-346">ASP.NET knows the difference between this operator and the addition operator based on the data type of the expression.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample39.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        <span data-ttu-id="05e9f-347">`+=` `-=`</span><span class="sxs-lookup"><span data-stu-id="05e9f-347">`+=` `-=`</span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="05e9f-348">증가 및 감소 연산자-변수에서 1 (각각)을 더하거나 뺍니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-348">The increment and decrement operators, which add and subtract 1 (respectively) from a variable.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample40.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `.`
    :::column-end:::
    :::column:::
    <span data-ttu-id="05e9f-349">점과.</span><span class="sxs-lookup"><span data-stu-id="05e9f-349">Dot.</span></span> <span data-ttu-id="05e9f-350">개체와 해당 속성 및 메서드를 구분 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-350">Used to distinguish objects and their properties and methods.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample41.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="05e9f-351">괄호.</span><span class="sxs-lookup"><span data-stu-id="05e9f-351">Parentheses.</span></span> <span data-ttu-id="05e9f-352">식을 그룹화 하 고 메서드에 매개 변수를 전달 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-352">Used to group expressions and to pass parameters to methods.</span></span>
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample42.js)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `[]`
    :::column-end:::
    :::column:::
    <span data-ttu-id="05e9f-353">각괄호.</span><span class="sxs-lookup"><span data-stu-id="05e9f-353">Brackets.</span></span> <span data-ttu-id="05e9f-354">배열 또는 컬렉션의 값에 액세스 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-354">Used for accessing values in arrays or collections.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample43.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!`
    :::column-end:::
    :::column:::
    <span data-ttu-id="05e9f-355">나타내지.</span><span class="sxs-lookup"><span data-stu-id="05e9f-355">Not.</span></span> <span data-ttu-id="05e9f-356">`true` 값을 반대로 `false` 하 고 그 반대의 경우도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-356">Reverses a `true` value to `false` and vice versa.</span></span> <span data-ttu-id="05e9f-357">일반적으로 `false` (즉, `true`)을 테스트 하는 간단한 방법으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-357">Typically used as a shorthand way to test for `false` (that is, for not `true`).</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample44.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        <span data-ttu-id="05e9f-358">`&&` `||`</span><span class="sxs-lookup"><span data-stu-id="05e9f-358">`&&` `||`</span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="05e9f-359">논리적 AND 및 OR 이며 조건을 함께 연결 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-359">Logical AND and OR, which are used to link conditions together.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample45.cs)]
    :::column-end:::
:::row-end:::

<a id="ID_WorkingWithFileAndFolderPaths"></a>
## <a name="working-with-file-and-folder-paths-in-code"></a><span data-ttu-id="05e9f-360">코드에서 파일 및 폴더 경로 작업</span><span class="sxs-lookup"><span data-stu-id="05e9f-360">Working with File and Folder Paths in Code</span></span>

<span data-ttu-id="05e9f-361">코드에서 파일 및 폴더 경로를 사용 하 여 작업 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-361">You'll often work with file and folder paths in your code.</span></span> <span data-ttu-id="05e9f-362">다음은 개발 컴퓨터에 표시 될 수 있는 웹 사이트의 물리적 폴더 구조에 대 한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-362">Here is an example of physical folder structure for a website as it might appear on your development computer:</span></span>

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

<span data-ttu-id="05e9f-363">Url 및 경로에 대 한 몇 가지 필수 정보는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-363">Here are some essential details about URLs and paths:</span></span>

- <span data-ttu-id="05e9f-364">URL은 도메인 이름 (`http://www.example.com`) 또는 서버 이름 (`http://localhost`, `http://mycomputer`)으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-364">A URL begins with either a domain name (`http://www.example.com`) or a server name (`http://localhost`, `http://mycomputer`).</span></span>
- <span data-ttu-id="05e9f-365">URL은 호스트 컴퓨터의 실제 경로에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-365">A URL corresponds to a physical path on a host computer.</span></span> <span data-ttu-id="05e9f-366">예를 들어 `http://myserver` 서버의 *C:\websites\mywebsite* 폴더에 해당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-366">For example, `http://myserver` might correspond to the folder *C:\websites\mywebsite* on the server.</span></span>
- <span data-ttu-id="05e9f-367">가상 경로는 전체 경로를 지정 하지 않고도 코드에서 경로를 나타내는 축약형입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-367">A virtual path is shorthand to represent paths in code without having to specify the full path.</span></span> <span data-ttu-id="05e9f-368">도메인 또는 서버 이름 뒤에 오는 URL의 부분을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-368">It includes the portion of a URL that follows the domain or server name.</span></span> <span data-ttu-id="05e9f-369">가상 경로를 사용 하는 경우 경로를 업데이트 하지 않고도 다른 도메인 이나 서버로 코드를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-369">When you use virtual paths, you can move your code to a different domain or server without having to update the paths.</span></span>

<span data-ttu-id="05e9f-370">차이점을 이해 하는 데 도움이 되는 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-370">Here's an example to help you understand the differences:</span></span>

| <span data-ttu-id="05e9f-371">전체 URL</span><span class="sxs-lookup"><span data-stu-id="05e9f-371">Complete URL</span></span> | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| <span data-ttu-id="05e9f-372">서버 이름</span><span class="sxs-lookup"><span data-stu-id="05e9f-372">Server name</span></span> | <span data-ttu-id="05e9f-373">*mycompanyserver*</span><span class="sxs-lookup"><span data-stu-id="05e9f-373">*mycompanyserver*</span></span> |
| <span data-ttu-id="05e9f-374">가상 경로</span><span class="sxs-lookup"><span data-stu-id="05e9f-374">Virtual path</span></span> | <span data-ttu-id="05e9f-375">*/humanresources/CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="05e9f-375">*/humanresources/CompanyPolicy.htm*</span></span> |
| <span data-ttu-id="05e9f-376">실제 경로</span><span class="sxs-lookup"><span data-stu-id="05e9f-376">Physical path</span></span> | <span data-ttu-id="05e9f-377">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="05e9f-377">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span></span> |

<span data-ttu-id="05e9f-378">C: 드라이브의 루트가 \ 인 것 처럼 가상 루트는/입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-378">The virtual root is /, just like the root of your C: drive is \.</span></span> <span data-ttu-id="05e9f-379">가상 폴더 경로는 항상 슬래시를 사용 합니다. 폴더의 가상 경로에는 물리적 폴더와 동일한 이름을 사용할 수 없습니다. 별칭 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-379">(Virtual folder paths always use forward slashes.) The virtual path of a folder doesn't have to have the same name as the physical folder; it can be an alias.</span></span> <span data-ttu-id="05e9f-380">프로덕션 서버에서 가상 경로는 정확히 실제 경로와 거의 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-380">(On production servers, the virtual path rarely matches an exact physical path.)</span></span>

<span data-ttu-id="05e9f-381">코드에서 파일 및 폴더를 사용할 때 사용 하는 개체에 따라 실제 경로와 때때로 가상 경로를 참조 해야 하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-381">When you work with files and folders in code, sometimes you need to reference the physical path and sometimes a virtual path, depending on what objects you're working with.</span></span> <span data-ttu-id="05e9f-382">ASP.NET는 코드에서 파일 및 폴더 경로를 사용 하기 위한 다음과 같은 도구를 제공 합니다. `Server.MapPath` 메서드 및 `~` 연산자 및 `Href` 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-382">ASP.NET gives you these tools for working with file and folder paths in code: the `Server.MapPath` method, and the `~` operator and `Href` method.</span></span>

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a><span data-ttu-id="05e9f-383">가상에서 실제 경로로 변환: Server. MapPath 메서드</span><span class="sxs-lookup"><span data-stu-id="05e9f-383">Converting virtual to physical paths: the Server.MapPath method</span></span>

<span data-ttu-id="05e9f-384">`Server.MapPath` 메서드는 가상 경로 (예: */default.cshtml*)를 절대 실제 경로 (예: *C:\WebSites\MyWebSiteFolder\default.cshtml*)로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-384">The `Server.MapPath` method converts a virtual path (like */default.cshtml*) to an absolute physical path (like *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span></span> <span data-ttu-id="05e9f-385">이 메서드는 전체 실제 경로가 필요할 때마다 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-385">You use this method any time you need a complete physical path.</span></span> <span data-ttu-id="05e9f-386">일반적인 예로 웹 서버에서 텍스트 파일 또는 이미지 파일을 읽거나 쓰는 경우를 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-386">A typical example is when you're reading or writing a text file or image file on the web server.</span></span>

<span data-ttu-id="05e9f-387">일반적으로 호스팅 사이트 서버에서 사이트의 절대 실제 경로를 알 수 없으므로이 메서드는 사용자가 알고 있는 경로 (가상 경로)를 서버의 해당 경로로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-387">You typically don't know the absolute physical path of your site on a hosting site's server, so this method can convert the path you do know — the virtual path — to the corresponding path on the server for you.</span></span> <span data-ttu-id="05e9f-388">파일이 나 폴더에 대 한 가상 경로를 메서드에 전달 하 고 실제 경로를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-388">You pass the virtual path to a file or folder to the method, and it returns the physical path:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample46.cshtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a><span data-ttu-id="05e9f-389">가상 루트 참조: ~ operator 및 Href 메서드</span><span class="sxs-lookup"><span data-stu-id="05e9f-389">Referencing the virtual root: the ~ operator and Href method</span></span>

<span data-ttu-id="05e9f-390">*Cshtml* 또는 *vbhtml* 파일에서 `~` 연산자를 사용 하 여 가상 루트 경로를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-390">In a *.cshtml* or *.vbhtml* file, you can reference the virtual root path using the `~` operator.</span></span> <span data-ttu-id="05e9f-391">이는 사이트에서 페이지를 이동할 수 있으며 다른 페이지에 포함 된 모든 링크가 손상 되지 않도록 하기 때문에 매우 편리 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-391">This is very handy because you can move pages around in a site, and any links they contain to other pages won't be broken.</span></span> <span data-ttu-id="05e9f-392">웹 사이트를 다른 위치로 이동 하는 경우에도 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-392">It's also handy in case you ever move your website to a different location.</span></span> <span data-ttu-id="05e9f-393">다음은 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-393">Here are some examples:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample47.cshtml)]

<span data-ttu-id="05e9f-394">웹 사이트가 `http://myserver/myapp`경우 페이지가 실행 될 때 ASP.NET에서 이러한 경로를 처리 하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-394">If the website is `http://myserver/myapp`, here's how ASP.NET will treat these paths when the page runs:</span></span>

- <span data-ttu-id="05e9f-395">`myImagesFolder`: `http://myserver/myapp/images`</span><span class="sxs-lookup"><span data-stu-id="05e9f-395">`myImagesFolder`: `http://myserver/myapp/images`</span></span>
- <span data-ttu-id="05e9f-396">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span><span class="sxs-lookup"><span data-stu-id="05e9f-396">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span></span>

<span data-ttu-id="05e9f-397">이러한 경로는 변수의 값으로 실제로 표시 되지 않지만 ASP.NET는 경로를 해당 하는 것 처럼 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-397">(You won't actually see these paths as the values of the variable, but ASP.NET will treat the paths as if that's what they were.)</span></span>

<span data-ttu-id="05e9f-398">다음과 같이 서버 코드와 태그에서 모두 `~` 연산자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-398">You can use the `~` operator both in server code (as above) and in markup, like this:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample48.html)]

<span data-ttu-id="05e9f-399">태그에서 `~` 연산자를 사용 하 여 이미지 파일, 다른 웹 페이지 및 CSS 파일과 같은 리소스에 대 한 경로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-399">In markup, you use the `~` operator to create paths to resources like image files, other web pages, and CSS files.</span></span> <span data-ttu-id="05e9f-400">페이지가 실행 될 때 ASP.NET는 페이지 (코드 및 태그 모두)를 살펴보고 적절 한 경로에 대 한 모든 `~` 참조를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-400">When the page runs, ASP.NET looks through the page (both code and markup) and resolves all the `~` references to the appropriate path.</span></span>

## <a name="conditional-logic-and-loops"></a><span data-ttu-id="05e9f-401">조건부 논리 및 루프</span><span class="sxs-lookup"><span data-stu-id="05e9f-401">Conditional Logic and Loops</span></span>

<span data-ttu-id="05e9f-402">ASP.NET 서버 코드를 사용 하면 조건에 따라 작업을 수행 하 고 특정 횟수 (즉, 루프를 실행 하는 코드)에 문을 반복 하는 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-402">ASP.NET server code lets you perform tasks based on conditions and write code that repeats statements a specific number of times (that is, code that runs a loop).</span></span>

### <a name="testing-conditions"></a><span data-ttu-id="05e9f-403">테스트 조건</span><span class="sxs-lookup"><span data-stu-id="05e9f-403">Testing Conditions</span></span>

<span data-ttu-id="05e9f-404">간단한 조건을 테스트 하려면 지정 하는 테스트에 따라 true 또는 false를 반환 하는 `if` 문을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-404">To test a simple condition you use the `if` statement, which returns true or false based on a test you specify:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample49.cshtml)]

<span data-ttu-id="05e9f-405">`if` 키워드는 블록을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-405">The `if` keyword starts a block.</span></span> <span data-ttu-id="05e9f-406">실제 테스트 (조건)는 괄호 안에 있으며 true 또는 false를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-406">The actual test (condition) is in parentheses and returns true or false.</span></span> <span data-ttu-id="05e9f-407">테스트를 true로 설정 하는 경우 실행 되는 문은 중괄호로 묶여 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-407">The statements that run if the test is true are enclosed in braces.</span></span> <span data-ttu-id="05e9f-408">`if` 문은 조건이 false 인 경우 실행할 문을 지정 하는 `else` 블록을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-408">An `if` statement can include an `else` block that specifies statements to run if the condition is false:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample50.cshtml)]

<span data-ttu-id="05e9f-409">`else if` 블록을 사용 하 여 여러 조건을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-409">You can add multiple conditions using an `else if` block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample51.cshtml)]

<span data-ttu-id="05e9f-410">이 예에서는 if 블록의 첫 번째 조건이 true가 아닌 경우 `else if` 조건이 검사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-410">In this example, if the first condition in the if block is not true, the `else if` condition is checked.</span></span> <span data-ttu-id="05e9f-411">이러한 조건이 충족 되 면 `else if` 블록의 문이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-411">If that condition is met, the statements in the `else if` block are executed.</span></span> <span data-ttu-id="05e9f-412">조건을 충족 하는 조건이 없으면 `else` 블록의 문이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-412">If none of the conditions are met, the statements in the `else` block are executed.</span></span> <span data-ttu-id="05e9f-413">원하는 수의 else if 블록을 추가한 다음 `else` 블록을 사용 하 여 다른 모든 항목을&quot; 조건에 &quot;수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-413">You can add any number of else if blocks, and then close with an `else` block as the &quot;everything else&quot; condition.</span></span>

<span data-ttu-id="05e9f-414">많은 수의 조건을 테스트 하려면 `switch` 블록을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-414">To test a large number of conditions, use a `switch` block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample52.cshtml)]

<span data-ttu-id="05e9f-415">테스트할 값은 괄호 안에 있습니다 (예: `weekday` 변수).</span><span class="sxs-lookup"><span data-stu-id="05e9f-415">The value to test is in parentheses (in the example, the `weekday` variable).</span></span> <span data-ttu-id="05e9f-416">각 개별 테스트는 콜론으로 끝나는 `case` 문 (:)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-416">Each individual test uses a `case` statement that ends with a colon (:).</span></span> <span data-ttu-id="05e9f-417">`case` 문의 값이 테스트 값과 일치 하면 해당 case 블록의 코드가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-417">If the value of a `case` statement matches the test value, the code in that case block is executed.</span></span> <span data-ttu-id="05e9f-418">`break` 문을 사용 하 여 각 case 문을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-418">You close each case statement with a `break` statement.</span></span> <span data-ttu-id="05e9f-419">(각 `case` 블록에 중단을 포함 하는 것을 잊은 경우 다음 `case` 문의 코드도 실행 됩니다.) `switch` 블록에는 다른 모든 사례에 해당 하지 않는 경우 실행 되는 다른 모든 항목&quot; 옵션 &quot;에 대 한 마지막 사례로 `default` 문이 있는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-419">(If you forget to include break in each `case` block, the code from the next `case` statement will run also.) A `switch` block often has a `default` statement as the last case for an &quot;everything else&quot; option that runs if none of the other cases are true.</span></span>

<span data-ttu-id="05e9f-420">브라우저에 표시 되는 마지막 두 조건부 블록의 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-420">The result of the last two conditional blocks displayed in a browser:</span></span>

![Razor-Img10](introducing-razor-syntax-c/_static/image10.jpg)

### <a name="looping-code"></a><span data-ttu-id="05e9f-422">반복 코드</span><span class="sxs-lookup"><span data-stu-id="05e9f-422">Looping Code</span></span>

<span data-ttu-id="05e9f-423">동일한 문을 반복적으로 실행 해야 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-423">You often need to run the same statements repeatedly.</span></span> <span data-ttu-id="05e9f-424">이렇게 하려면 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-424">You do this by looping.</span></span> <span data-ttu-id="05e9f-425">예를 들어 데이터 컬렉션의 각 항목에 대해 동일한 문을 실행 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-425">For example, you often run the same statements for each item in a collection of data.</span></span> <span data-ttu-id="05e9f-426">반복 하려는 횟수를 정확히 알고 있는 경우 `for` 루프를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-426">If you know exactly how many times you want to loop, you can use a `for` loop.</span></span> <span data-ttu-id="05e9f-427">이러한 종류의 루프는 계산 하거나 계산 하는 데 특히 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-427">This kind of loop is especially useful for counting up or counting down:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample53.html)]

<span data-ttu-id="05e9f-428">루프는 `for` 키워드를 사용 하 여 시작 하 고, 괄호로 묶인 세 개의 문을 세미콜론으로 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-428">The loop begins with the `for` keyword, followed by three statements in parentheses, each terminated with a semicolon.</span></span>

- <span data-ttu-id="05e9f-429">괄호 안에 첫 번째 문 (`var i=10;`)은 카운터를 만들고 10으로 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-429">Inside the parentheses, the first statement (`var i=10;`) creates a counter and initializes it to 10.</span></span> <span data-ttu-id="05e9f-430">모든 변수를 사용할 수 `i` &#8212; 카운터의 이름을 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-430">You don't have to name the counter `i` &#8212; you can use any variable.</span></span> <span data-ttu-id="05e9f-431">`for` 루프가 실행 되 면 카운터가 자동으로 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-431">When the `for` loop runs, the counter is automatically incremented.</span></span>
- <span data-ttu-id="05e9f-432">두 번째 문 (`i < 21;`)은 계산 하려는 시간에 대 한 조건을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-432">The second statement (`i < 21;`) sets the condition for how far you want to count.</span></span> <span data-ttu-id="05e9f-433">이 경우에는이 값을 최대 20 개까지 이동 하려고 합니다. 즉, 카운터가 21 보다 작은 경우 계속 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-433">In this case, you want it to go to a maximum of 20 (that is, keep going while the counter is less than 21).</span></span>
- <span data-ttu-id="05e9f-434">세 번째 문 (`i++`)은 루프가 실행 될 때마다 카운터가 1을 추가 하도록 지정 하는 증분 연산자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-434">The third statement (`i++` ) uses an increment operator, which simply specifies that the counter should have 1 added to it each time the loop runs.</span></span>

<span data-ttu-id="05e9f-435">중괄호 안에는 루프가 반복 될 때마다 실행 되는 코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-435">Inside the braces is the code that will run for each iteration of the loop.</span></span> <span data-ttu-id="05e9f-436">태그는 매번 새 단락 (`<p>` 요소)을 만들고 출력에 줄을 추가 하 여 `i` (카운터)의 값을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-436">The markup creates a new paragraph (`<p>` element) each time and adds a line to the output, displaying the value of `i` (the counter).</span></span> <span data-ttu-id="05e9f-437">이 페이지를 실행 하는 경우이 예제에서는 출력을 표시 하는 11 개의 줄을 만들며 각 줄의 텍스트는 항목 번호를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-437">When you run this page, the example creates 11 lines displaying the output, with the text in each line indicating the item number.</span></span>

![Razor-Img11](introducing-razor-syntax-c/_static/image11.jpg)

<span data-ttu-id="05e9f-439">컬렉션 또는 배열에 대 한 작업을 수행 하는 경우에는 종종 `foreach` 루프를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-439">If you're working with a collection or array, you often use a `foreach` loop.</span></span> <span data-ttu-id="05e9f-440">컬렉션은 유사한 개체의 그룹 이며, `foreach` 루프를 사용 하 여 컬렉션의 각 항목에 대 한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-440">A collection is a group of similar objects, and the `foreach` loop lets you carry out a task on each item in the collection.</span></span> <span data-ttu-id="05e9f-441">이 유형의 루프는 `for` 루프와 달리 카운터를 증가 시키거나 제한을 설정할 필요가 없기 때문에 컬렉션에 편리 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-441">This type of loop is convenient for collections, because unlike a `for` loop, you don't have to increment the counter or set a limit.</span></span> <span data-ttu-id="05e9f-442">대신 `foreach` 루프 코드는 완료 될 때까지 컬렉션을 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-442">Instead, the `foreach` loop code simply proceeds through the collection until it's finished.</span></span>

<span data-ttu-id="05e9f-443">예를 들어 다음 코드는 웹 서버에 대 한 정보를 포함 하는 개체인 `Request.ServerVariables` 컬렉션의 항목을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-443">For example, the following code returns the items in the `Request.ServerVariables` collection, which is an object that contains information about your web server.</span></span> <span data-ttu-id="05e9f-444">`foreac` h 루프를 사용 하 여 HTML 글머리 기호 목록에 새 `<li>` 요소를 만들어 각 항목의 이름을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-444">It uses a `foreac` h loop to display the name of each item by creating a new `<li>` element in an HTML bulleted list.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample54.html)]

<span data-ttu-id="05e9f-445">`foreach` 키워드 뒤에는 컬렉션의 단일 항목을 나타내는 변수를 선언 하는 괄호 (예: `var item`)가 오고 그 뒤에 `in` 키워드가 오고 그 뒤에 반복 하려는 컬렉션이 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-445">The `foreach` keyword is followed by parentheses where you declare a variable that represents a single item in the collection (in the example, `var item`), followed by the `in` keyword, followed by the collection you want to loop through.</span></span> <span data-ttu-id="05e9f-446">`foreach` 루프의 본문에서 이전에 선언한 변수를 사용 하 여 현재 항목에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-446">In the body of the `foreach` loop, you can access the current item using the variable that you declared earlier.</span></span>

![Razor-Img12](introducing-razor-syntax-c/_static/image12.jpg)

<span data-ttu-id="05e9f-448">보다 일반적인 용도의 루프를 만들려면 `while` 문을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-448">To create a more general-purpose loop, use the `while` statement:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample55.cshtml)]

<span data-ttu-id="05e9f-449">`while` 루프는 `while` 키워드로 시작 하 여 루프가 계속 되는 기간을 지정 하는 괄호 (`countNum`가 50 보다 작은 경우)로 시작 하 여 반복할 블록을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-449">A `while` loop begins with the `while` keyword, followed by parentheses where you specify how long the loop continues (here, for as long as `countNum` is less than 50), then the block to repeat.</span></span> <span data-ttu-id="05e9f-450">루프는 일반적으로 계산에 사용 되는 변수 또는 개체를 증가 (추가) 또는 감소 (빼기) 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-450">Loops typically increment (add to) or decrement (subtract from) a variable or object used for counting.</span></span> <span data-ttu-id="05e9f-451">예제에서 `+=` 연산자는 루프가 실행 될 때마다 `countNum`에 1을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-451">In the example, the `+=` operator adds 1 to `countNum` each time the loop runs.</span></span> <span data-ttu-id="05e9f-452">(에서 계산 되는 루프의 변수를 감소 시키려면 감소 연산자 `-=`)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-452">(To decrement a variable in a loop that counts down, you would use the decrement operator `-=`).</span></span>

## <a name="objects-and-collections"></a><span data-ttu-id="05e9f-453">개체 및 컬렉션</span><span class="sxs-lookup"><span data-stu-id="05e9f-453">Objects and Collections</span></span>

<span data-ttu-id="05e9f-454">ASP.NET 웹 사이트의 거의 모든 항목은 웹 페이지를 포함 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-454">Nearly everything in an ASP.NET website is an object, including the web page itself.</span></span> <span data-ttu-id="05e9f-455">이 섹션에서는 코드에서 자주 사용 하는 몇 가지 중요 한 개체에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-455">This section discusses some important objects you'll work with frequently in your code.</span></span>

### <a name="page-objects"></a><span data-ttu-id="05e9f-456">Page 개체</span><span class="sxs-lookup"><span data-stu-id="05e9f-456">Page Objects</span></span>

<span data-ttu-id="05e9f-457">ASP.NET의 가장 기본적인 개체는 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-457">The most basic object in ASP.NET is the page.</span></span> <span data-ttu-id="05e9f-458">정규화 된 개체 없이 페이지 개체의 속성에 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-458">You can access properties of the page object directly without any qualifying object.</span></span> <span data-ttu-id="05e9f-459">다음 코드에서는 페이지의 `Request` 개체를 사용 하 여 페이지의 파일 경로를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-459">The following code gets the page's file path, using the `Request` object of the page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample56.cshtml)]

<span data-ttu-id="05e9f-460">현재 페이지 개체의 속성 및 메서드를 참조 하 고 있음을 명확 하 게 하기 위해 선택적으로 `this` 키워드를 사용 하 여 코드의 페이지 개체를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-460">To make it clear that you're referencing properties and methods on the current page object, you can optionally use the keyword `this` to represent the page object in your code.</span></span> <span data-ttu-id="05e9f-461">다음은 페이지를 나타내는 `this` 추가 된 이전 코드 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-461">Here is the previous code example, with `this` added to represent the page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample57.cshtml)]

<span data-ttu-id="05e9f-462">`Page` 개체의 속성을 사용 하 여 다음과 같은 많은 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-462">You can use properties of the `Page` object to get a lot of information, such as:</span></span>

- <span data-ttu-id="05e9f-463">`Request`.</span><span class="sxs-lookup"><span data-stu-id="05e9f-463">`Request`.</span></span> <span data-ttu-id="05e9f-464">앞서 살펴본 것 처럼, 요청을 만든 브라우저의 유형, 페이지 URL, 사용자 id 등을 포함 하 여 현재 요청에 대 한 정보 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-464">As you've already seen, this is a collection of information about the current request, including what type of browser made the request, the URL of the page, the user identity, etc.</span></span>
- <span data-ttu-id="05e9f-465">`Response`.</span><span class="sxs-lookup"><span data-stu-id="05e9f-465">`Response`.</span></span> <span data-ttu-id="05e9f-466">서버 코드의 실행이 완료 되 면 브라우저로 전송 되는 응답 (페이지)에 대 한 정보 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-466">This is a collection of information about the response (page) that will be sent to the browser when the server code has finished running.</span></span> <span data-ttu-id="05e9f-467">예를 들어이 속성을 사용 하 여 응답에 정보를 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-467">For example, you can use this property to write information into the response.</span></span> 

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample58.cshtml)]

<a id="ID_CollectionsAndObjects"></a>
### <a name="collection-objects-arrays-and-dictionaries"></a><span data-ttu-id="05e9f-468">컬렉션 개체 (배열 및 사전)</span><span class="sxs-lookup"><span data-stu-id="05e9f-468">Collection Objects (Arrays and Dictionaries)</span></span>

<span data-ttu-id="05e9f-469">*컬렉션* 은 데이터베이스의 `Customer` 개체 컬렉션과 같이 동일한 유형의 개체 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-469">A *collection* is a group of objects of the same type, such as a collection of `Customer` objects from a database.</span></span> <span data-ttu-id="05e9f-470">ASP.NET에는 `Request.Files` 컬렉션과 같은 여러 기본 제공 컬렉션이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-470">ASP.NET contains many built-in collections, like the `Request.Files` collection.</span></span>

<span data-ttu-id="05e9f-471">컬렉션의 데이터로 작업 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-471">You'll often work with data in collections.</span></span> <span data-ttu-id="05e9f-472">두 가지 일반적인 컬렉션 형식은 *배열* 및 *사전*입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-472">Two common collection types are the *array* and the *dictionary*.</span></span> <span data-ttu-id="05e9f-473">배열은 비슷한 항목의 컬렉션을 저장 하지만 각 항목을 저장할 별도의 변수를 만들지 않으려는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-473">An array is useful when you want to store a collection of similar items but don't want to create a separate variable to hold each item:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample59.cshtml)]

<span data-ttu-id="05e9f-474">배열을 사용 하 여 `string`, `int`또는 `DateTime`와 같은 특정 데이터 형식을 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-474">With arrays, you declare a specific data type, such as `string`, `int`, or `DateTime`.</span></span> <span data-ttu-id="05e9f-475">변수에 배열이 포함 될 수 있음을 나타내려면 괄호를 선언에 추가 합니다 (예: `string[]` 또는 `int[]`).</span><span class="sxs-lookup"><span data-stu-id="05e9f-475">To indicate that the variable can contain an array, you add brackets to the declaration (such as `string[]` or `int[]`).</span></span> <span data-ttu-id="05e9f-476">해당 위치 (인덱스)를 사용 하거나 `foreach` 문을 사용 하 여 배열의 항목에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-476">You can access items in an array using their position (index) or by using the `foreach` statement.</span></span> <span data-ttu-id="05e9f-477">배열 인덱스는 0부터 시작 &#8212; 합니다. 즉, 첫 번째 항목의 위치는 0이 고, 두 번째 항목은 위치 1에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-477">Array indexes are zero-based &#8212; that is, the first item is at position 0, the second item is at position 1, and so on.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample60.cshtml)]

<span data-ttu-id="05e9f-478">`Length` 속성을 가져와서 배열의 항목 수를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-478">You can determine the number of items in an array by getting its `Length` property.</span></span> <span data-ttu-id="05e9f-479">배열에서 특정 항목의 위치를 가져오려면 (배열을 검색 하려면) `Array.IndexOf` 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-479">To get the position of a specific item in the array (to search the array), use the `Array.IndexOf` method.</span></span> <span data-ttu-id="05e9f-480">배열의 콘텐츠를 반전 (`Array.Reverse` 메서드) 하거나 내용을 정렬 (`Array.Sort` 메서드) 하는 등의 작업을 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-480">You can also do things like reverse the contents of an array (the `Array.Reverse` method) or sort the contents (the `Array.Sort` method).</span></span>

<span data-ttu-id="05e9f-481">브라우저에 표시 되는 문자열 배열 코드의 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-481">The output of the string array code displayed in a browser:</span></span>

![Razor-Img13](introducing-razor-syntax-c/_static/image13.jpg)

<span data-ttu-id="05e9f-483">사전은 키 (또는 이름)를 제공 하 여 해당 값을 설정 하거나 검색할 수 있는 키/값 쌍의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-483">A dictionary is a collection of key/value pairs, where you provide the key (or name) to set or retrieve the corresponding value:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample61.cshtml)]

<span data-ttu-id="05e9f-484">사전을 만들려면 `new` 키워드를 사용 하 여 새 사전 개체를 만들도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-484">To create a dictionary, you use the `new` keyword to indicate that you're creating a new dictionary object.</span></span> <span data-ttu-id="05e9f-485">`var` 키워드를 사용 하 여 변수에 사전을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-485">You can assign a dictionary to a variable using the `var` keyword.</span></span> <span data-ttu-id="05e9f-486">꺾쇠 괄호 (`< >`)를 사용 하 여 사전에 있는 항목의 데이터 형식을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-486">You indicate the data types of the items in the dictionary using angle brackets ( `< >` ).</span></span> <span data-ttu-id="05e9f-487">선언 끝에 괄호 쌍을 추가 해야 합니다 .이는 실제로 새 사전을 만드는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-487">At the end of the declaration, you must add a pair of parentheses, because this is actually a method that creates a new dictionary.</span></span>

<span data-ttu-id="05e9f-488">사전에 항목을 추가 하려면 사전 변수의 `Add` 메서드 (이 경우`myScores`)를 호출한 다음 키와 값을 지정 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-488">To add items to the dictionary, you can call the `Add` method of the dictionary variable (`myScores` in this case), and then specify a key and a value.</span></span> <span data-ttu-id="05e9f-489">또는 다음 예제와 같이 대괄호를 사용 하 여 키를 나타내고 단순 할당을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-489">Alternatively, you can use square brackets to indicate the key and do a simple assignment, as in the following example:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample62.cs)]

<span data-ttu-id="05e9f-490">사전에서 값을 가져오려면 대괄호 안에 키를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-490">To get a value from the dictionary, you specify the key in brackets:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample63.cs)]

## <a name="calling-methods-with-parameters"></a><span data-ttu-id="05e9f-491">매개 변수를 사용 하 여 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="05e9f-491">Calling Methods with Parameters</span></span>

<span data-ttu-id="05e9f-492">이 문서 앞부분에서 읽은 것 처럼를 사용 하 여 프로그래밍 하는 개체에는 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-492">As you read earlier in this article, the objects that you program with can have methods.</span></span> <span data-ttu-id="05e9f-493">예를 들어 `Database` 개체에는 `Database.Connect` 메서드가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-493">For example, a `Database` object might have a `Database.Connect` method.</span></span> <span data-ttu-id="05e9f-494">또한 많은 메서드에 하나 이상의 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-494">Many methods also have one or more parameters.</span></span> <span data-ttu-id="05e9f-495">*매개 변수* 는 메서드가 해당 작업을 완료할 수 있도록 메서드에 전달 하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-495">A *parameter* is a value that you pass to a method to enable the method to complete its task.</span></span> <span data-ttu-id="05e9f-496">예를 들어 다음 세 개의 매개 변수를 사용 하는 `Request.MapPath` 메서드에 대 한 선언을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="05e9f-496">For example, look at a declaration for the `Request.MapPath` method, which takes three parameters:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample64.cs)]

<span data-ttu-id="05e9f-497">(줄은 더 쉽게 읽을 수 있도록 래핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-497">(The line has been wrapped to make it more readable.</span></span> <span data-ttu-id="05e9f-498">따옴표로 묶인 문자열 내부를 제외 하 고 거의 모든 위치에 줄 바꿈을 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-498">Remember that you can put line breaks almost any place except inside strings that are enclosed in quotation marks.)</span></span>

<span data-ttu-id="05e9f-499">이 메서드는 지정 된 가상 경로에 해당 하는 서버의 실제 경로를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-499">This method returns the physical path on the server that corresponds to a specified virtual path.</span></span> <span data-ttu-id="05e9f-500">메서드에 대 한 세 가지 매개 변수는 `virtualPath`, `baseVirtualDir`및 `allowCrossAppMapping`입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-500">The three parameters for the method are `virtualPath`, `baseVirtualDir`, and `allowCrossAppMapping`.</span></span> <span data-ttu-id="05e9f-501">선언에서 매개 변수는 허용 되는 데이터의 데이터 형식과 함께 나열 됩니다. 이 메서드를 호출 하는 경우 세 매개 변수 모두에 대 한 값을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-501">(Notice that in the declaration, the parameters are listed with the data types of the data that they'll accept.) When you call this method, you must supply values for all three parameters.</span></span>

<span data-ttu-id="05e9f-502">Razor 구문는 매개 변수를 메서드에 전달 하는 두 가지 옵션 ( *위치 매개 변수* 및 *명명 된 매개*변수)을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-502">The Razor syntax gives you two options for passing parameters to a method: *positional parameters* and *named parameters*.</span></span> <span data-ttu-id="05e9f-503">위치 매개 변수를 사용 하 여 메서드를 호출 하려면 메서드 선언에 지정 된 엄격한 순서로 매개 변수를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-503">To call a method using positional parameters, you pass the parameters in a strict order that's specified in the method declaration.</span></span> <span data-ttu-id="05e9f-504">(일반적으로 메서드의 설명서를 읽어이 순서를 확인 합니다.) 순서를 따라야 하 고 필요한 경우 매개 변수 &#8212; 를 건너뛸 수 없습니다. 값이 없는 위치 매개 변수에 대해 빈 문자열 (`""`) 또는 `null`를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-504">(You would typically know this order by reading documentation for the method.) You must follow the order, and you can't skip any of the parameters &#8212; if necessary, you pass an empty string (`""`) or `null` for a positional parameter that you don't have a value for.</span></span>

<span data-ttu-id="05e9f-505">다음 예제에서는 웹 사이트에 *scripts* 라는 폴더가 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-505">The following example assumes you have a folder named *scripts* on your website.</span></span> <span data-ttu-id="05e9f-506">이 코드는 `Request.MapPath` 메서드를 호출 하 고 세 개의 매개 변수에 대 한 값을 올바른 순서로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-506">The code calls the `Request.MapPath` method and passes values for the three parameters in the correct order.</span></span> <span data-ttu-id="05e9f-507">그런 다음 결과 매핑된 경로를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-507">It then displays the resulting mapped path.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample65.cshtml)]

<span data-ttu-id="05e9f-508">메서드에 매개 변수가 많은 경우 명명 된 매개 변수를 사용 하 여 코드를 더 읽기 쉽게 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-508">When a method has many parameters, you can keep your code more readable by using named parameters.</span></span> <span data-ttu-id="05e9f-509">명명 된 매개 변수를 사용 하 여 메서드를 호출 하려면 매개 변수 이름 뒤에 콜론 (:), 값을 차례로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-509">To call a method using named parameters, you specify the parameter name followed by a colon (:), and then the value.</span></span> <span data-ttu-id="05e9f-510">명명 된 매개 변수의 장점은 원하는 순서로 전달할 수 있다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-510">The advantage of named parameters is that you can pass them in any order you want.</span></span> <span data-ttu-id="05e9f-511">이는 메서드 호출이 압축 되지 않는다는 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-511">(A disadvantage is that the method call is not as compact.)</span></span>

<span data-ttu-id="05e9f-512">다음 예제에서는 위와 동일한 메서드를 호출 하지만 명명 된 매개 변수를 사용 하 여 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-512">The following example calls the same method as above, but uses named parameters to supply the values:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample66.cshtml)]

<span data-ttu-id="05e9f-513">여기에서 볼 수 있듯이 매개 변수는 다른 순서로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-513">As you can see, the parameters are passed in a different order.</span></span> <span data-ttu-id="05e9f-514">그러나 이전 예제와이 예제를 실행 하면 동일한 값이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-514">However, if you run the previous example and this example, they'll return the same value.</span></span>

<a id="ID_HandlingErrors"></a>
## <a name="handling-errors"></a><span data-ttu-id="05e9f-515">오류 처리</span><span class="sxs-lookup"><span data-stu-id="05e9f-515">Handling Errors</span></span>

### <a name="try-catch-statements"></a><span data-ttu-id="05e9f-516">Try-catch 문</span><span class="sxs-lookup"><span data-stu-id="05e9f-516">Try-Catch Statements</span></span>

<span data-ttu-id="05e9f-517">코드에 컨트롤 외부의 이유로 실패할 수 있는 문이 종종 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-517">You'll often have statements in your code that might fail for reasons outside your control.</span></span> <span data-ttu-id="05e9f-518">예를 들면 다음과 같습니다.:</span><span class="sxs-lookup"><span data-stu-id="05e9f-518">For example:</span></span>

- <span data-ttu-id="05e9f-519">코드에서 파일을 만들거나 액세스 하려고 하면 모든 종류의 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-519">If your code tries to create or access a file, all sorts of errors might occur.</span></span> <span data-ttu-id="05e9f-520">필요한 파일이 없거나, 잠겨 있거나, 코드에 권한이 없을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-520">The file you want might not exist, it might be locked, the code might not have permissions, and so on.</span></span>
- <span data-ttu-id="05e9f-521">마찬가지로, 코드에서 데이터베이스의 레코드를 업데이트 하려고 시도 하는 경우에는 사용 권한 문제가 있을 수 있습니다. 데이터베이스에 대 한 연결이 삭제 될 수 있습니다. 저장할 데이터가 유효 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-521">Similarly, if your code tries to update records in a database, there can be permissions issues, the connection to the database might be dropped, the data to save might be invalid, and so on.</span></span>

<span data-ttu-id="05e9f-522">프로그래밍 측면에서 이러한 상황을 *예외*라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-522">In programming terms, these situations are called *exceptions*.</span></span> <span data-ttu-id="05e9f-523">코드에서 예외가 발생 하는 경우 사용자에 게 가장 잘 방해가 되는 오류 메시지를 생성 (throw) 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-523">If your code encounters an exception, it generates (throws) an error message that's, at best, annoying to users:</span></span>

![Razor-Img14](introducing-razor-syntax-c/_static/image14.jpg)

<span data-ttu-id="05e9f-525">코드에 예외가 발생할 수 있는 상황에서이 유형의 오류 메시지를 방지 하기 위해 `try/catch` 문을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-525">In situations where your code might encounter exceptions, and in order to avoid error messages of this type, you can use `try/catch` statements.</span></span> <span data-ttu-id="05e9f-526">`try` 문에서 확인 중인 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-526">In the `try` statement, you run the code that you're checking.</span></span> <span data-ttu-id="05e9f-527">하나 이상의 `catch` 문에서 발생 했을 수 있는 특정 오류 (특정 유형의 예외)를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-527">In one or more `catch` statements, you can look for specific errors (specific types of exceptions) that might have occurred.</span></span> <span data-ttu-id="05e9f-528">예상 되는 오류를 찾기 위해 필요한 만큼 `catch` 문을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-528">You can include as many `catch` statements as you need to look for errors that you are anticipating.</span></span>

> [!NOTE]
> <span data-ttu-id="05e9f-529">`try/catch` 문에서는 `Response.Redirect` 메서드를 사용 하지 않는 것이 좋습니다 .이는 페이지에서 예외를 발생 시킬 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-529">We recommend that you avoid using the `Response.Redirect` method in `try/catch` statements, because it can cause an exception in your page.</span></span>

<span data-ttu-id="05e9f-530">다음 예에서는 첫 번째 요청에서 텍스트 파일을 만든 다음 사용자가 파일을 열 수 있도록 하는 단추를 표시 하는 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-530">The following example shows a page that creates a text file on the first request and then displays a button that lets the user open the file.</span></span> <span data-ttu-id="05e9f-531">이 예제에서는 예외를 발생 시 키 지 않도록 의도적으로 잘못 된 파일 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-531">The example deliberately uses a bad file name so that it will cause an exception.</span></span> <span data-ttu-id="05e9f-532">이 코드에는 두 가지 예외에 대 한 `catch` 문이 포함 되어 있습니다. `FileNotFoundException`는 파일 이름이 잘못 된 경우에 발생 하는 것이 고, ASP.NET에서 폴더를 찾을 수 없는 경우에 발생 하는 `DirectoryNotFoundException`입니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-532">The code includes `catch` statements for two possible exceptions: `FileNotFoundException`, which occurs if the file name is bad, and `DirectoryNotFoundException`, which occurs if ASP.NET can't even find the folder.</span></span> <span data-ttu-id="05e9f-533">(모든 것이 제대로 작동 하는 경우 실행 되는 방식을 확인 하기 위해 예제에서 문의 주석 처리를 제거할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="05e9f-533">(You can uncomment a statement in the example in order to see how it runs when everything works properly.)</span></span>

<span data-ttu-id="05e9f-534">코드에서 예외를 처리 하지 않은 경우 이전 스크린샷과 같은 오류 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-534">If your code didn't handle the exception, you would see an error page like the previous screen shot.</span></span> <span data-ttu-id="05e9f-535">그러나 `try/catch` 섹션을 사용 하면 사용자가 이러한 유형의 오류를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05e9f-535">However, the `try/catch` section helps prevent the user from seeing these types of errors.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample67.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="05e9f-536">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="05e9f-536">Additional Resources</span></span>

<span data-ttu-id="05e9f-537">**Visual Basic를 사용한 프로그래밍**</span><span class="sxs-lookup"><span data-stu-id="05e9f-537">**Programming with Visual Basic**</span></span>

[<span data-ttu-id="05e9f-538">부록: Visual Basic 언어 및 구문</span><span class="sxs-lookup"><span data-stu-id="05e9f-538">Appendix: Visual Basic Language and Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkId=202908)

<span data-ttu-id="05e9f-539">**참조 설명서**</span><span class="sxs-lookup"><span data-stu-id="05e9f-539">**Reference Documentation**</span></span>

[<span data-ttu-id="05e9f-540">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="05e9f-540">ASP.NET</span></span>](https://msdn.microsoft.com/library/ee532866.aspx)

[<span data-ttu-id="05e9f-541">C#언어도</span><span class="sxs-lookup"><span data-stu-id="05e9f-541">C# Language</span></span>](https://msdn.microsoft.com/library/kx37x362.aspx)
