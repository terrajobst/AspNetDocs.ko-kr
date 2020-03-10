---
uid: web-pages/overview/getting-started/introducing-razor-syntax-vb
title: Razor 구문을 사용한 ASP.NET 웹 프로그래밍 소개 (Visual Basic) | Microsoft Docs
author: Rick-Anderson
description: 이 부록에서는 Razor 구문를 사용 하 여 Visual Basic ASP.NET 웹 페이지를 사용한 프로그래밍에 대 한 개요를 제공 합니다.
ms.author: riande
ms.date: 02/07/2014
ms.assetid: 5da59646-e973-41cd-88a9-c6b2c0594027
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-vb
msc.type: authoredcontent
ms.openlocfilehash: 2be57655b8c9b76b94e1d9a7ae5fbee27545a0a9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422663"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-visual-basic"></a><span data-ttu-id="f0ece-103">Razor 구문(Visual Basic)을 사용하는 ASP.NET 웹 프로그래밍 소개</span><span class="sxs-lookup"><span data-stu-id="f0ece-103">Introduction to ASP.NET Web Programming Using the Razor Syntax (Visual Basic)</span></span>

<span data-ttu-id="f0ece-104">만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="f0ece-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="f0ece-105">이 문서에서는 Razor 구문 및 Visual Basic를 사용 하 여 ASP.NET 웹 페이지 프로그래밍에 대 한 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-105">This article gives you an overview of programming with ASP.NET Web Pages using the Razor syntax and Visual Basic.</span></span> <span data-ttu-id="f0ece-106">ASP.NET는 웹 서버에서 동적 웹 페이지를 실행 하기 위한 Microsoft 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-106">ASP.NET is Microsoft's technology for running dynamic web pages on web servers.</span></span>
> 
> <span data-ttu-id="f0ece-107">**학습 내용**:</span><span class="sxs-lookup"><span data-stu-id="f0ece-107">**What you'll learn**:</span></span>
> 
> - <span data-ttu-id="f0ece-108">Razor 구문를 사용 하 여 프로그래밍 ASP.NET 웹 페이지 시작 하기 위한 상위 8 개 프로그래밍 팁.</span><span class="sxs-lookup"><span data-stu-id="f0ece-108">The top 8 programming tips for getting started with programming ASP.NET Web Pages using Razor syntax.</span></span>
> - <span data-ttu-id="f0ece-109">필요한 기본 프로그래밍 개념.</span><span class="sxs-lookup"><span data-stu-id="f0ece-109">Basic programming concepts you'll need.</span></span>
> - <span data-ttu-id="f0ece-110">ASP.NET 서버 코드 및 Razor 구문은 무엇 인가요?</span><span class="sxs-lookup"><span data-stu-id="f0ece-110">What ASP.NET server code and the Razor syntax is all about.</span></span>
>   
> 
> ## <a name="software-versions"></a><span data-ttu-id="f0ece-111">소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="f0ece-111">Software versions</span></span>
> 
> 
> - <span data-ttu-id="f0ece-112">ASP.NET 웹 페이지 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="f0ece-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="f0ece-113">이 자습서는 ASP.NET 웹 페이지 2 에서도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>

<span data-ttu-id="f0ece-114">Razor 구문에서 ASP.NET 웹 페이지를 사용 하는 대부분 C#의 예제는를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-114">Most examples of using ASP.NET Web Pages with Razor syntax use C#.</span></span> <span data-ttu-id="f0ece-115">그러나 Razor 구문는 Visual Basic도 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-115">But the Razor syntax also supports Visual Basic.</span></span> <span data-ttu-id="f0ece-116">Visual Basic에서 ASP.NET 웹 페이지를 프로그래밍 *하려면 파일 이름* 확장명을 사용 하 여 웹 페이지를 만든 다음 Visual Basic 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-116">To program an ASP.NET web page in Visual Basic, you create a web page with a *.vbhtml* filename extension, and then add Visual Basic code.</span></span> <span data-ttu-id="f0ece-117">이 문서에서는 ASP.NET 웹 페이지를 만들기 위한 Visual Basic 언어 및 구문을 사용 하는 방법에 대 한 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-117">This article gives you an overview of working with the Visual Basic language and syntax to create ASP.NET Webpages.</span></span>

> [!NOTE]
> <span data-ttu-id="f0ece-118">Microsoft WebMatrix (**빵집**, **사진 갤러리**및 **스타터 사이트**등)의 기본 웹 사이트 템플릿은 및 Visual Basic 버전에서 C# 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-118">The default website templates for Microsoft WebMatrix (**Bakery**, **Photo Gallery**, and **Starter Site**, etc.) are available in C# and Visual Basic versions.</span></span> <span data-ttu-id="f0ece-119">NuGet 패키지로 Visual Basic 템플릿을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-119">You can install the Visual Basic templates by as NuGet packages.</span></span> <span data-ttu-id="f0ece-120">웹 사이트 템플릿은 *Microsoft templates*라는 폴더에 있는 사이트의 루트 폴더에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-120">Website templates are installed in the root folder of your site in a folder named *Microsoft Templates*.</span></span>

## <a name="the-top-8-programming-tips"></a><span data-ttu-id="f0ece-121">상위 8 개 프로그래밍 팁</span><span class="sxs-lookup"><span data-stu-id="f0ece-121">The Top 8 Programming Tips</span></span>

<span data-ttu-id="f0ece-122">이 섹션에는 Razor 구문를 사용 하 여 ASP.NET 서버 코드 작성을 시작할 때 알아야 할 몇 가지 팁이 나열 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-122">This section lists a few tips that you absolutely need to know as you start writing ASP.NET server code using the Razor syntax.</span></span>

### <a name="1-you-add-code-to-a-page-using-the--character"></a><span data-ttu-id="f0ece-123">1. @ 문자를 사용 하 여 페이지에 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-123">1. You add code to a page using the @ character</span></span>

<span data-ttu-id="f0ece-124">`@` 문자는 인라인 식, 단일 문 블록 및 다중 문 블록을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-124">The `@` character starts inline expressions, single-statement blocks, and multi-statement blocks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample1.vbhtml)]

<span data-ttu-id="f0ece-125">브라우저에 표시 되는 결과는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-125">The result displayed in a browser:</span></span>

![Razor-.Img1](introducing-razor-syntax-vb/_static/image1.jpg)

> [!TIP] 
> 
> <span data-ttu-id="f0ece-127">**HTML 인코딩**</span><span class="sxs-lookup"><span data-stu-id="f0ece-127">**HTML Encoding**</span></span>
> 
> <span data-ttu-id="f0ece-128">앞의 예제와 같이 `@` 문자를 사용 하 여 페이지에 콘텐츠를 표시 하는 경우 ASP.NET은 출력을 HTML로 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-128">When you display content in a page using the `@` character, as in the preceding examples, ASP.NET HTML-encodes the output.</span></span> <span data-ttu-id="f0ece-129">이렇게 하면 예약 된 HTML 문자 (예: `<`, `>` 및 `&`)가 HTML 태그나 엔터티로 해석 되지 않고 웹 페이지에서 문자로 표시 될 수 있도록 하는 코드와 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-129">This replaces reserved HTML characters (such as `<` and `>` and `&`) with codes that enable the characters to be displayed as characters in a web page instead of being interpreted as HTML tags or entities.</span></span> <span data-ttu-id="f0ece-130">HTML 인코딩이 없으면 서버 코드의 출력이 올바르게 표시 되지 않을 수 있으며, 페이지를 보안 위험에 노출 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-130">Without HTML encoding, the output from your server code might not display correctly, and could expose a page to security risks.</span></span>
> 
> <span data-ttu-id="f0ece-131">태그를 태그로 렌더링 하는 HTML 태그를 출력 하는 경우 (`<p></p>` 예: 단락이 나 텍스트를 강조 하는 `<em></em>`)에는이 문서의 뒷부분에 나오는 [코드 블록의 텍스트, 태그 및 코드 결합](#BM_CombiningTextMarkupAndCode) 단원을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f0ece-131">If your goal is to output HTML markup that renders tags as markup (for example `<p></p>` for a paragraph or `<em></em>` to emphasize text), see the section [Combining Text, Markup, and Code in Code Blocks](#BM_CombiningTextMarkupAndCode) later in this article.</span></span>
> 
> <span data-ttu-id="f0ece-132">[ASP.NET 웹 페이지 사이트에서 Html 양식 사용](https://go.microsoft.com/fwlink/?LinkId=202892)에 대 한 자세한 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-132">You can read more about HTML encoding in [Working with HTML Forms in ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=202892).</span></span>

### <a name="2-you-enclose-code-blocks-with-codeend-code"></a><span data-ttu-id="f0ece-133">2. 코드 블록을 코드로 묶습니다. 최종 코드</span><span class="sxs-lookup"><span data-stu-id="f0ece-133">2. You enclose code blocks with Code...End Code</span></span>

<span data-ttu-id="f0ece-134">코드 블록에는 하나 이상의 코드 문이 포함 되 고 `Code` 및 `End Code`키워드로 묶입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-134">A code block includes one or more code statements and is enclosed with the keywords `Code` and `End Code`.</span></span> <span data-ttu-id="f0ece-135">`@` 문자 &#8212; 바로 뒤에 여는 `Code` 키워드를 추가 합니다. 태그 사이에 공백이 있을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-135">Place the opening `Code` keyword immediately after the `@` character &#8212; there can't be whitespace between them.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample2.vbhtml)]

<span data-ttu-id="f0ece-136">브라우저에 표시 되는 결과는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-136">The result displayed in a browser:</span></span>

![Razor-Img2](introducing-razor-syntax-vb/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-line-break"></a><span data-ttu-id="f0ece-138">3. 블록 내에서 각 코드 문을 줄 바꿈으로 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-138">3. Inside a block, you end each code statement with a line break</span></span>

<span data-ttu-id="f0ece-139">Visual Basic 코드 블록에서 각 문은 줄 바꿈으로 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-139">In a Visual Basic code block, each statement ends with a line break.</span></span> <span data-ttu-id="f0ece-140">(필요에 따라 긴 코드 문을 여러 줄로 래핑하는 방법에 대해서는이 문서의 뒷부분에서 설명 합니다.)</span><span class="sxs-lookup"><span data-stu-id="f0ece-140">(Later in the article you'll see a way to wrap a long code statement into multiple lines if needed.)</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample3.vbhtml)]

### <a name="4-you-use-variables-to-store-values"></a><span data-ttu-id="f0ece-141">4. 변수를 사용 하 여 값 저장</span><span class="sxs-lookup"><span data-stu-id="f0ece-141">4. You use variables to store values</span></span>

<span data-ttu-id="f0ece-142">문자열, 숫자, 날짜 등을 포함 하 여 *변수에*값을 저장할 수 있습니다. `Dim` 키워드를 사용 하 여 새 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-142">You can store values in a *variable*, including strings, numbers, and dates, etc. You create a new variable using the `Dim` keyword.</span></span> <span data-ttu-id="f0ece-143">`@`를 사용 하 여 페이지에 직접 변수 값을 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-143">You can insert variable values directly in a page using `@`.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample4.vbhtml)]

<span data-ttu-id="f0ece-144">브라우저에 표시 되는 결과는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-144">The result displayed in a browser:</span></span>

![Razor-Img3](introducing-razor-syntax-vb/_static/image3.jpg)

### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a><span data-ttu-id="f0ece-146">5. 리터럴 문자열 값을 큰따옴표로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-146">5. You enclose literal string values in double quotation marks</span></span>

<span data-ttu-id="f0ece-147">*문자열* 은 텍스트로 처리 되는 문자 시퀀스입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-147">A *string* is a sequence of characters that are treated as text.</span></span> <span data-ttu-id="f0ece-148">문자열을 지정 하려면 큰따옴표로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-148">To specify a string, you enclose it in double quotation marks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample5.vbhtml)]

<span data-ttu-id="f0ece-149">문자열 값에 큰따옴표를 포함 하려면 두 개의 큰따옴표 문자를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-149">To embed double quotation marks within a string value, insert two double quotation mark characters.</span></span> <span data-ttu-id="f0ece-150">페이지 출력에 큰따옴표를 한 번 표시 하려면 따옴표 붙은 문자열 내에 `""`로 입력 하 고, 두 번째 문자를 두 번 표시 하려면 따옴표 붙은 문자열 내에 `""""`로 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-150">If you want the double quotation character to appear once in the page output, enter it as `""` within the quoted string, and if you want it to appear twice, enter it as `""""` within the quoted string.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample6.vbhtml)]

<span data-ttu-id="f0ece-151">브라우저에 표시 되는 결과는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-151">The result displayed in a browser:</span></span>

![Razor-Img4](introducing-razor-syntax-vb/_static/image4.jpg)

### <a name="6-visual-basic-code-is-not-case-sensitive"></a><span data-ttu-id="f0ece-153">6. Visual Basic 코드는 대/소문자를 구분 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-153">6. Visual Basic code is not case sensitive</span></span>

<span data-ttu-id="f0ece-154">Visual Basic 언어는 대/소문자를 구분 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-154">The Visual Basic language is not case sensitive.</span></span> <span data-ttu-id="f0ece-155">프로그래밍 키워드 (예: `Dim`, `If`, `True`) 및 변수 이름 (예: `myString`또는 `subTotal`)은 어떤 경우 든 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-155">Programming keywords (like `Dim`, `If`, and `True`) and variable names (like `myString`, or `subTotal`) can be written in any case.</span></span>

<span data-ttu-id="f0ece-156">다음 코드 줄에서는 소문자 이름을 사용 하 `lastname` 변수에 값을 할당 한 다음 대문자 이름을 사용 하 여 변수 값을 페이지에 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-156">The following lines of code assign a value to the variable `lastname` using a lowercase name, and then output the variable value to the page using an uppercase name.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample7.vbhtml)]

<span data-ttu-id="f0ece-157">브라우저에 표시 되는 결과는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-157">The result displayed in a browser:</span></span>

![vb-syntax-5](introducing-razor-syntax-vb/_static/image5.jpg)

### <a name="7-much-of-your-coding-involves-working-with-objects"></a><span data-ttu-id="f0ece-159">7. 코딩의 대부분이 개체 작업을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-159">7. Much of your coding involves working with objects</span></span>

<span data-ttu-id="f0ece-160">개체는 페이지, 텍스트 상자, 파일, 이미지 &#8212; , 웹 요청, 전자 메일 메시지, 고객 레코드 (데이터베이스 행) 등을 사용 하 여 프로그래밍할 수 있는 작업을 나타냅니다. 개체에는 텍스트 상자 개체에 &#8212; `Text` 속성이 있고, 요청 개체에 `Url` 속성이 있고, 메일 메시지에 `From` 속성이 있으며, customer 개체에 `FirstName` 속성이 있는 특성을 설명 하는 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-160">An object represents a thing that you can program with &#8212; a page, a text box, a file, an image, a web request, an email message, a customer record (database row), etc. Objects have properties that describe their characteristics &#8212; a text box object has a `Text` property, a request object has a `Url` property, an email message has a `From` property, and a customer object has a `FirstName` property.</span></span> <span data-ttu-id="f0ece-161">개체에는 수행할 수&quot; &quot;동사 인 메서드도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-161">Objects also have methods that are the &quot;verbs&quot; they can perform.</span></span> <span data-ttu-id="f0ece-162">예제에는 파일 개체의 `Save` 메서드, 이미지 개체의 `Rotate` 메서드 및 전자 메일 개체의 `Send` 메서드가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-162">Examples include a file object's `Save` method, an image object's `Rotate` method, and an email object's `Send` method.</span></span>

<span data-ttu-id="f0ece-163">페이지의 양식 필드 값 (입력란 등), 요청을 만든 브라우저의 유형, 페이지 URL, 사용자 id 등의 정보를 제공 하는 `Request` 개체를 사용 하는 경우가 많습니다. 이 예제에서는 `Request` 개체의 속성에 액세스 하는 방법과 서버에서 페이지의 절대 경로를 제공 하는 `Request` 개체의 `MapPath` 메서드를 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-163">You'll often work with the `Request` object, which gives you information like the values of form fields on the page (text boxes, etc.), what type of browser made the request, the URL of the page, the user identity, etc. This example shows how to access properties of the `Request` object and how to call the `MapPath` method of the `Request` object, which gives you the absolute path of the page on the server:</span></span>

[!code-html[Main](introducing-razor-syntax-vb/samples/sample8.html)]

<span data-ttu-id="f0ece-164">브라우저에 표시 되는 결과는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-164">The result displayed in a browser:</span></span>

![Razor-Img5](introducing-razor-syntax-vb/_static/image6.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a><span data-ttu-id="f0ece-166">8. 결정을 내리는 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-166">8. You can write code that makes decisions</span></span>

<span data-ttu-id="f0ece-167">동적 웹 페이지의 핵심 기능은 조건에 따라 수행할 작업을 결정할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-167">A key feature of dynamic web pages is that you can determine what to do based on conditions.</span></span> <span data-ttu-id="f0ece-168">이 작업을 수행 하는 가장 일반적인 방법은 `If` 문 (및 선택적 `Else` 문)을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-168">The most common way to do this is with the `If` statement (and optional `Else` statement).</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample9.vbhtml)]

<span data-ttu-id="f0ece-169">`If IsPost` 문은 `If IsPost = True`를 작성 하는 간단한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-169">The statement `If IsPost` is a shorthand way of writing `If IsPost = True`.</span></span> <span data-ttu-id="f0ece-170">`If` 문과 함께 조건을 테스트 하 고, 코드 블록을 반복 하 고,이 문서의 뒷부분에서 설명 하는 다양 한 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-170">Along with `If` statements, there are a variety of ways to test conditions, repeat blocks of code, and so on, which are described later in this article.</span></span>

<span data-ttu-id="f0ece-171">브라우저에 표시 되는 결과 ( **Submit**를 클릭 한 후):</span><span class="sxs-lookup"><span data-stu-id="f0ece-171">The result displayed in a browser (after clicking **Submit**):</span></span>

![Razor-Img6](introducing-razor-syntax-vb/_static/image7.jpg)

> [!TIP] 
> 
> <span data-ttu-id="f0ece-173">**HTTP GET 및 POST 메서드 및 IsPost 속성**</span><span class="sxs-lookup"><span data-stu-id="f0ece-173">**HTTP GET and POST Methods and the IsPost Property**</span></span>
> 
> <span data-ttu-id="f0ece-174">웹 페이지 (HTTP)에 사용 되는 프로토콜은 서버에 대 한 요청을 수행 하는 데 사용 되는 매우 제한 된 수의 메서드 (&quot;동사&quot;)를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-174">The protocol used for web pages (HTTP) supports a very limited number of methods (&quot;verbs&quot;) that are used to make requests to the server.</span></span> <span data-ttu-id="f0ece-175">가장 일반적인 두 가지는 페이지를 읽는 데 사용 되는 GET과 페이지를 전송 하는 데 사용 되는 게시물입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-175">The two most common ones are GET, which is used to read a page, and POST, which is used to submit a page.</span></span> <span data-ttu-id="f0ece-176">일반적으로 사용자가 페이지를 처음 요청할 때 페이지는 GET을 사용 하 여 요청 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-176">In general, the first time a user requests a page, the page is requested using GET.</span></span> <span data-ttu-id="f0ece-177">사용자가 양식을 채운 다음 **제출**을 클릭 하면 브라우저에서 서버에 대 한 POST 요청을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-177">If the user fills in a form and then clicks **Submit**, the browser makes a POST request to the server.</span></span>
> 
> <span data-ttu-id="f0ece-178">웹 프로그래밍에서 페이지를 처리 하는 방법을 알 수 있도록 페이지를 GET 또는 POST로 요청 하 고 있는지 여부를 확인 하는 것이 유용한 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-178">In web programming, it's often useful to know whether a page is being requested as a GET or as a POST so that you know how to process the page.</span></span> <span data-ttu-id="f0ece-179">ASP.NET 웹 페이지에서 `IsPost` 속성을 사용 하 여 요청이 GET 또는 POST 인지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-179">In ASP.NET Web Pages, you can use the `IsPost` property to see whether a request is a GET or a POST.</span></span> <span data-ttu-id="f0ece-180">요청이 POST 인 경우 `IsPost` 속성은 true를 반환 하 고 폼에서 텍스트 상자의 값을 읽는 등의 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-180">If the request is a POST, the `IsPost` property will return true, and you can do things like read the values of text boxes on a form.</span></span> <span data-ttu-id="f0ece-181">`IsPost`값에 따라 페이지를 다르게 처리 하는 방법을 보여 주는 많은 예제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-181">Many examples you'll see show you how to process the page differently depending on the value of `IsPost`.</span></span>

## <a name="a-simple-code-example"></a><span data-ttu-id="f0ece-182">간단한 코드 예제</span><span class="sxs-lookup"><span data-stu-id="f0ece-182">A Simple Code Example</span></span>

<span data-ttu-id="f0ece-183">이 절차에서는 기본 프로그래밍 기술을 보여 주는 페이지를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-183">This procedure shows you how to create a page that illustrates basic programming techniques.</span></span> <span data-ttu-id="f0ece-184">이 예제에서는 사용자가 두 개의 숫자를 입력 하 고 그 결과를 추가 하 고 결과를 표시할 수 있는 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-184">In the example, you create a page that lets users enter two numbers, then it adds them and displays the result.</span></span>

1. <span data-ttu-id="f0ece-185">편집기에서 새 파일을 만들고 이름을 *Addnumbers. vbhtml*로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-185">In your editor, create a new file and name it *AddNumbers.vbhtml*.</span></span>
2. <span data-ttu-id="f0ece-186">페이지에 이미 있는 항목을 대체 하 여 다음 코드와 태그를 페이지에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-186">Copy the following code and markup into the page, replacing anything already in the page.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample10.vbhtml)]

    <span data-ttu-id="f0ece-187">유의 해야 할 몇 가지 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-187">Here are some things for you to note:</span></span>

    - <span data-ttu-id="f0ece-188">`@` 문자는 페이지에서 첫 번째 코드 블록을 시작 하 고 맨 아래에 포함 된 `totalMessage` 변수 앞에 옵니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-188">The `@` character starts the first block of code in the page, and it precedes the `totalMessage` variable embedded near the bottom.</span></span>
    - <span data-ttu-id="f0ece-189">페이지 맨 위에 있는 블록은 `Code...End Code`로 묶여 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-189">The block at the top of the page is enclosed in `Code...End Code`.</span></span>
    - <span data-ttu-id="f0ece-190">변수 `total`, `num1`, `num2`및 `totalMessage`에는 여러 숫자와 문자열이 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-190">The variables `total`, `num1`, `num2`, and `totalMessage` store several numbers and a string.</span></span>
    - <span data-ttu-id="f0ece-191">`totalMessage` 변수에 할당 된 리터럴 문자열 값이 큰따옴표로 묶여 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-191">The literal string value assigned to the `totalMessage` variable is in double quotation marks.</span></span>
    - <span data-ttu-id="f0ece-192">Visual Basic 코드는 대/소문자를 구분 하지 않으므로 `totalMessage` 변수를 페이지의 아래쪽 근처에 사용 하는 경우 해당 이름은 페이지 맨 위에 있는 변수 선언의 철자와 일치 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-192">Because Visual Basic code is not case sensitive, when the `totalMessage` variable is used near the bottom of the page, its name only needs to match the spelling of the variable declaration at the top of the page.</span></span> <span data-ttu-id="f0ece-193">대/소문자 구분은 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-193">The casing doesn't matter.</span></span>
    - <span data-ttu-id="f0ece-194">식 `num1.AsInt()` + `num2.AsInt()` 개체 및 메서드로 작업 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-194">The expression `num1.AsInt()` + `num2.AsInt()` shows how to work with objects and methods.</span></span> <span data-ttu-id="f0ece-195">각 변수의 `AsInt` 메서드는 사용자가 입력 한 문자열을 추가할 수 있는 정수 (정수)로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-195">The `AsInt` method on each variable converts the string entered by a user to a whole number (an integer) that can be added.</span></span>
    - <span data-ttu-id="f0ece-196">`<form>` 태그는 `method="post"` 특성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-196">The `<form>` tag includes a `method="post"` attribute.</span></span> <span data-ttu-id="f0ece-197">이렇게 하면 사용자가 **추가**를 클릭 하면 HTTP POST 메서드를 사용 하 여 페이지가 서버에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-197">This specifies that when the user clicks **Add**, the page will be sent to the server using the HTTP POST method.</span></span> <span data-ttu-id="f0ece-198">페이지가 전송 되 면 코드 `If IsPost`이 true로 평가 되 고 조건부 코드가 실행 되어 숫자를 더한 결과를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-198">When the page is submitted, the code `If IsPost` evaluates to true and the conditional code runs, displaying the result of adding the numbers.</span></span>
3. <span data-ttu-id="f0ece-199">페이지를 저장 하 고 브라우저에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-199">Save the page and run it in a browser.</span></span> <span data-ttu-id="f0ece-200">(파일을 실행 하기 전에 해당 페이지가 **파일** 작업 영역에서 선택 되어 있는지 확인 합니다.) 두 개의 정수를 입력 한 다음 **추가** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-200">(Make sure the page is selected in the **Files** workspace before you run it.) Enter two whole numbers and then click the **Add** button.</span></span>

    ![Razor-Img7](introducing-razor-syntax-vb/_static/image8.jpg)

## <a name="visual-basic-language-and-syntax"></a><span data-ttu-id="f0ece-202">Visual Basic 언어 및 구문</span><span class="sxs-lookup"><span data-stu-id="f0ece-202">Visual Basic Language and Syntax</span></span>

<span data-ttu-id="f0ece-203">앞에서 ASP.NET 웹 페이지를 만드는 방법 및 HTML 태그에 서버 코드를 추가 하는 방법의 기본 예를 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-203">Earlier you saw a basic example of how to create an ASP.NET web page, and how you can add server code to HTML markup.</span></span> <span data-ttu-id="f0ece-204">여기서는 Visual Basic 사용 하 여 Razor 구문 &#8212; 프로그래밍 언어 규칙을 사용 하 여 ASP.NET 서버 코드를 작성 하는 기본 사항을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-204">Here you'll learn the basics of using Visual Basic to write ASP.NET server code using the Razor syntax &#8212; that is, the programming language rules.</span></span>

<span data-ttu-id="f0ece-205">프로그래밍 경험이 있는 경우 (특히 C, C++, C#, Visual Basic 또는 JavaScript를 사용 하는 경우) 여기에서 읽는 많은 내용이 익숙할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-205">If you're experienced with programming (especially if you've used C, C++, C#, Visual Basic, or JavaScript), much of what you read here will be familiar.</span></span> <span data-ttu-id="f0ece-206">사용자는 WebMatrix 코드를 *. vbhtml* 파일의 태그에 추가 하는 방법만 숙지 해야 할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-206">You'll probably need to familiarize yourself only with how WebMatrix code is added to markup in *.vbhtml* files.</span></span>

### <a id="BM_CombiningTextMarkupAndCode"></a><span data-ttu-id="f0ece-207">코드 블록에서 텍스트, 태그 및 코드 결합</span><span class="sxs-lookup"><span data-stu-id="f0ece-207">Combining text, markup, and code in code blocks</span></span>

<span data-ttu-id="f0ece-208">서버 코드 블록에서 텍스트 및 태그를 페이지에 출력 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-208">In server code blocks, you'll often want to output text and markup to the page.</span></span> <span data-ttu-id="f0ece-209">서버 코드 블록에 코드가 아닌 텍스트가 포함 되어 있는 경우 해당 텍스트를 그대로 렌더링 해야 하는 경우 ASP.NET는 해당 텍스트를 코드와 구별할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-209">If a server code block contains text that's not code and that instead should be rendered as is, ASP.NET needs to be able to distinguish that text from code.</span></span> <span data-ttu-id="f0ece-210">여러 가지 방법으로 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-210">There are several ways to do this.</span></span>

- <span data-ttu-id="f0ece-211">`<p></p>` 또는 `<em></em>`와 같은 HTML 블록 요소의 텍스트를 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-211">Enclose the text in an HTML block element like `<p></p>` or `<em></em>`:</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample11.vbhtml)]

    <span data-ttu-id="f0ece-212">HTML 요소에는 텍스트, 추가 HTML 요소 및 서버 코드 식이 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-212">The HTML element can include text, additional HTML elements, and server-code expressions.</span></span> <span data-ttu-id="f0ece-213">ASP.NET는 여는 HTML 태그 (예: `<p>`)를 볼 때 요소와 해당 콘텐츠를 브라우저에 그대로 렌더링 하 고 서버 코드 식을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-213">When ASP.NET sees the opening HTML tag (for example, `<p>`), it renders everything the element and its content as is to the browser (and resolves the server-code expressions).</span></span>

- <span data-ttu-id="f0ece-214">`@:` 연산자 또는 `<text>` 요소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-214">Use the `@:` operator or the `<text>` element.</span></span> <span data-ttu-id="f0ece-215">`@:`는 일반 텍스트 또는 일치 하지 않는 HTML 태그를 포함 하는 단일 내용의 줄을 출력 합니다. `<text>` 요소는 여러 줄을 출력으로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-215">The `@:` outputs a single line of content containing plain text or unmatched HTML tags; the `<text>` element encloses multiple lines to output.</span></span> <span data-ttu-id="f0ece-216">이러한 옵션은 HTML 요소를 출력의 일부로 렌더링 하지 않으려는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-216">These options are useful when you don't want to render an HTML element as part of the output.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample12.vbhtml)]

    <span data-ttu-id="f0ece-217">다음 예제에서는 이전 예제를 반복 하지만 단일 쌍의 `<text>` 태그를 사용 하 여 렌더링할 텍스트를 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-217">The following example repeats the previous example but uses a single pair of `<text>` tags to enclose the text to render.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample13.vbhtml)]

    <span data-ttu-id="f0ece-218">다음 예제에서 `<text>` 및 `</text>` 태그는 세 개의 줄을 포함 하며, 모든 줄에는 포함 되지 않은 텍스트와 일치 하지 않는 HTML 태그 (`<br />`)가 서버 코드 및 일치 하는 HTML 태그와 함께 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-218">In the following example, the `<text>` and `</text>` tags enclose three lines, all of which have some uncontained text and unmatched HTML tags (`<br />`), along with server code and matched HTML tags.</span></span> <span data-ttu-id="f0ece-219">또한 각 줄 앞에 `@:` 연산자를 사용 하 여 개별적으로 추가할 수 있습니다. 어떤 방법이 든 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-219">Again, you could also precede each line individually with the `@:` operator; either way works.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample14.vbhtml)]

    > [!NOTE]
    > <span data-ttu-id="f0ece-220">HTML 요소를 사용 하 여이 섹션 &#8212; 에 표시 된 대로 텍스트를 출력 하는 경우 `@:` 연산자 또는 `<text>` &#8212; 요소 ASP.NET은 출력을 html로 인코딩하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-220">When you output text as shown in this section &#8212; using an HTML element, the `@:` operator, or the `<text>` element &#8212; ASP.NET doesn't HTML-encode the output.</span></span> <span data-ttu-id="f0ece-221">앞에서 설명한 것 처럼 ASP.NET는이 섹션에 설명 된 특수 한 사례를 제외 하 고 `@`뒤에 오는 서버 코드 식과 서버 코드 블록의 출력을 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-221">(As noted earlier, ASP.NET does encode the output of server code expressions and server code blocks that are preceded by `@`, except in the special cases noted in this section.)</span></span>

### <a name="whitespace"></a><span data-ttu-id="f0ece-222">공백</span><span class="sxs-lookup"><span data-stu-id="f0ece-222">Whitespace</span></span>

<span data-ttu-id="f0ece-223">문 (및 문자열 리터럴 외부)의 추가 공백은 문에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-223">Extra spaces in a statement (and outside of a string literal) don't affect the statement:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample15.vbhtml)]

### <a name="breaking-long-statements-into-multiple-lines"></a><span data-ttu-id="f0ece-224">긴 문을 여러 줄로 분할</span><span class="sxs-lookup"><span data-stu-id="f0ece-224">Breaking long statements into multiple lines</span></span>

<span data-ttu-id="f0ece-225">코드의 각 줄 뒤에 밑줄 문자 `_` (Visual Basic를 *연속 문자*라고 함)를 사용 하 여 긴 코드 문을 여러 줄로 나눌 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-225">You can break a long code statement into multiple lines by using the underscore character `_` (which in Visual Basic is called the *continuation character*) after each line of code.</span></span> <span data-ttu-id="f0ece-226">문을 다음 줄로 나누려면 줄의 끝에 공백을 추가 하 고 연속 문자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-226">To break a statement onto the next line, at the end of the line add a space and then the continuation character.</span></span> <span data-ttu-id="f0ece-227">다음 줄에서 문을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-227">Continue the statement on the next line.</span></span> <span data-ttu-id="f0ece-228">가독성을 높이는 데 필요한 만큼의 줄로 문을 래핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-228">You can wrap statements onto as many lines as you need to improve readability.</span></span> <span data-ttu-id="f0ece-229">다음 문은 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-229">The following statements are the same:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample16.vbhtml)]

<span data-ttu-id="f0ece-230">그러나 문자열 리터럴 중간에 줄을 줄 바꿈할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-230">However, you can't wrap a line in the middle of a string literal.</span></span> <span data-ttu-id="f0ece-231">다음 예는 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-231">The following example doesn't work:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample17.vbhtml)]

<span data-ttu-id="f0ece-232">위의 코드와 같이 여러 줄로 래핑하는 긴 문자열을 결합 하려면이 문서의 뒷부분에 나오는 *연결 연산자* (`&`)를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-232">To combine a long string that wraps to multiple lines like the above code, you would need to use the *concatenation operator* (`&`), which you'll see later in this article.</span></span>

### <a name="code-comments"></a><span data-ttu-id="f0ece-233">코드 주석</span><span class="sxs-lookup"><span data-stu-id="f0ece-233">Code comments</span></span>

<span data-ttu-id="f0ece-234">주석을 사용 하 여 자신에 게 메모를 남길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-234">Comments let you leave notes for yourself or others.</span></span> <span data-ttu-id="f0ece-235">Razor 구문 주석은 접두사로 `@*` 하 고 `*@`로 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-235">Razor syntax comments are prefixed with `@*` and end with `*@`.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-vb/samples/sample18.cshtml)]

<span data-ttu-id="f0ece-236">코드 블록 내에서 Razor 구문 주석을 사용 하거나 각 줄 앞에 있는 작은따옴표 (`'`) 인 일반 Visual Basic 주석 문자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-236">Within code blocks you can use the Razor syntax comments, or you can use ordinary Visual Basic comment character, which is a single quote (`'`) prefixed to each line.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample19.vbhtml)]

## <a name="variables"></a><span data-ttu-id="f0ece-237">variables</span><span class="sxs-lookup"><span data-stu-id="f0ece-237">Variables</span></span>

<span data-ttu-id="f0ece-238">변수는 데이터를 저장 하는 데 사용 하는 명명 된 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-238">A variable is a named object that you use to store data.</span></span> <span data-ttu-id="f0ece-239">변수 이름을 지정할 수 있지만 이름은 영문자로 시작 해야 하며 공백 또는 예약 문자를 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-239">You can name variables anything, but the name must begin with an alphabetic character and it cannot contain whitespace or reserved characters.</span></span> <span data-ttu-id="f0ece-240">Visual Basic에서 앞서 살펴본 것 처럼 변수 이름에 있는 문자의 대/소문자는 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-240">In Visual Basic, as you saw earlier, the case of the letters in a variable name doesn't matter.</span></span>

### <a name="variables-and-data-types"></a><span data-ttu-id="f0ece-241">변수 및 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="f0ece-241">Variables and data types</span></span>

<span data-ttu-id="f0ece-242">변수에는 변수에 저장 되는 데이터의 종류를 나타내는 특정 데이터 형식이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-242">A variable can have a specific data type, which indicates what kind of data is stored in the variable.</span></span> <span data-ttu-id="f0ece-243">문자열 값 (&quot;예: Hello 세계&quot;), 정수 값 (예: 3 또는 79)을 저장 하는 정수 변수, 날짜 값을 다양 한 형식 (예: 4/12/2012 또는 3 월 2009)으로 저장 하는 날짜 변수를 저장 하는 문자열 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-243">You can have string variables that store string values (like &quot;Hello world&quot;), integer variables that store whole-number values (like 3 or 79), and date variables that store date values in a variety of formats (like 4/12/2012 or March 2009).</span></span> <span data-ttu-id="f0ece-244">사용할 수 있는 다른 많은 데이터 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-244">And there are many other data types you can use.</span></span>

<span data-ttu-id="f0ece-245">그러나 변수의 형식을 지정할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-245">However, you don't have to specify a type for a variable.</span></span> <span data-ttu-id="f0ece-246">대부분의 경우 ASP.NET는 변수의 데이터를 사용 하는 방법에 따라 형식을 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-246">In most cases ASP.NET can figure out the type based on how the data in the variable is being used.</span></span> <span data-ttu-id="f0ece-247">때로는 형식을 지정 해야 합니다 .이 경우에는 예제가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-247">(Occasionally you must specify a type; you'll see examples where this is true.)</span></span>

<span data-ttu-id="f0ece-248">형식을 지정 하지 않고 변수를 선언 하려면 `Dim` 및 변수 이름 (예 `Dim myVar`)을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-248">To declare a variable without specifying a type, use `Dim` plus the variable name (for instance, `Dim myVar`).</span></span> <span data-ttu-id="f0ece-249">형식을 사용 하 여 변수를 선언 하려면 `Dim`와 변수 이름을 차례로 사용 하 고 `As` 다음에 형식 이름 (예를 들어 `Dim myVar As String`)을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-249">To declare a variable with a type, use `Dim` plus the variable name, followed by `As` and then the type name (for instance, `Dim myVar As String`).</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample20.vbhtml)]

<span data-ttu-id="f0ece-250">다음 예제에서는 웹 페이지의 변수를 사용 하는 일부 인라인 식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-250">The following example shows some inline expressions that use the variables in a web page.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample21.vbhtml)]

<span data-ttu-id="f0ece-251">브라우저에 표시 되는 결과는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-251">The result displayed in a browser:</span></span>

![Razor-Img9](introducing-razor-syntax-vb/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a><span data-ttu-id="f0ece-253">데이터 형식 변환 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f0ece-253">Converting and testing data types</span></span>

<span data-ttu-id="f0ece-254">ASP.NET는 일반적으로 데이터 형식을 자동으로 결정할 수 있지만 경우에 따라 자동으로 데이터 형식을 결정할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-254">Although ASP.NET can usually determine a data type automatically, sometimes it can't.</span></span> <span data-ttu-id="f0ece-255">따라서 명시적 변환을 수행 하 여 ASP.NET를 지원 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-255">Therefore, you might need to help ASP.NET out by performing an explicit conversion.</span></span> <span data-ttu-id="f0ece-256">형식을 변환 하지 않아도 되는 경우에도 사용할 수 있는 데이터 형식을 테스트 하는 것이 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-256">Even if you don't have to convert types, sometimes it's helpful to test to see what type of data you might be working with.</span></span>

<span data-ttu-id="f0ece-257">가장 일반적인 경우는 문자열을 정수 또는 날짜와 같은 다른 형식으로 변환 해야 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-257">The most common case is that you have to convert a string to another type, such as to an integer or date.</span></span> <span data-ttu-id="f0ece-258">다음 예에서는 문자열을 숫자로 변환 해야 하는 일반적인 경우를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-258">The following example shows a typical case where you must convert a string to a number.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample22.vbhtml)]

<span data-ttu-id="f0ece-259">사용자 입력은 사용자가 문자열로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-259">As a rule, user input comes to you as strings.</span></span> <span data-ttu-id="f0ece-260">사용자에 게 숫자를 입력 하 라는 메시지가 표시 되 고 숫자를 입력 한 경우에도 사용자 입력이 제출 되 고 코드에서이를 읽으면 데이터는 문자열 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-260">Even if you've prompted the user to enter a number, and even if they've entered a digit, when user input is submitted and you read it in code, the data is in string format.</span></span> <span data-ttu-id="f0ece-261">따라서 문자열을 숫자로 변환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-261">Therefore, you must convert the string to a number.</span></span> <span data-ttu-id="f0ece-262">예를 들어 값을 변환 하지 않고 값에 대해 산술 연산을 수행 하려고 하면 ASP.NET에서 두 개의 문자열을 추가할 수 없기 때문에 다음과 같은 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-262">In the example, if you try to perform arithmetic on the values without converting them, the following error results, because ASP.NET cannot add two strings:</span></span>

`Cannot implicitly convert type 'string' to 'int'.`

<span data-ttu-id="f0ece-263">값을 정수로 변환 하려면 `AsInt` 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-263">To convert the values to integers, you call the `AsInt` method.</span></span> <span data-ttu-id="f0ece-264">성공적으로 변환 되 면 숫자를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-264">If the conversion is successful, you can then add the numbers.</span></span>

<span data-ttu-id="f0ece-265">다음 표에서는 변수에 대 한 몇 가지 일반적인 변환과 테스트 메서드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-265">The following table lists some common conversion and test methods for variables.</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="f0ece-266"><strong>메서드</strong></span><span class="sxs-lookup"><span data-stu-id="f0ece-266"><strong>Method</strong></span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="f0ece-267"><strong>설명</strong></span><span class="sxs-lookup"><span data-stu-id="f0ece-267"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="f0ece-268"><strong>예제</strong></span><span class="sxs-lookup"><span data-stu-id="f0ece-268"><strong>Example</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="f0ece-269">정수 (예: &quot;593&quot;)를 나타내는 문자열을 정수로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-269">Converts a string that represents a whole number (like &quot;593&quot;) to an integer.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample23.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsBool(), IsBool()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="f0ece-270">&quot;true&quot; 또는 &quot;false&quot; 같은 문자열을 부울 형식으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-270">Converts a string like &quot;true&quot; or &quot;false&quot; to a Boolean type.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample24.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsFloat(), IsFloat()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="f0ece-271">&quot;1.3&quot; 또는 &quot;7.439&quot; 같은 10 진수 값을 포함 하는 문자열을 부동 소수점 숫자로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-271">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a floating-point number.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample25.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDecimal(), IsDecimal()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="f0ece-272">&quot;1.3&quot; 또는 &quot;7.439&quot; 같은 10 진수 값이 있는 문자열을 10 진수로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-272">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a decimal number.</span></span> <span data-ttu-id="f0ece-273">ASP.NET에서 10 진수는 부동 소수점 숫자 보다 더 정확 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-273">(In ASP.NET, a decimal number is more precise than a floating-point number.)</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample26.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDateTime(), IsDateTime()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="f0ece-274">날짜 및 시간 값을 나타내는 문자열을 ASP.NET `DateTime` 형식으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-274">Converts a string that represents a date and time value to the ASP.NET `DateTime` type.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample27.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `ToString()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="f0ece-275">다른 모든 데이터 형식을 문자열로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-275">Converts any other data type to a string.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample28.vb)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a><span data-ttu-id="f0ece-276">연산자</span><span class="sxs-lookup"><span data-stu-id="f0ece-276">Operators</span></span>

<span data-ttu-id="f0ece-277">연산자는 식에서 수행할 명령의 종류를 ASP.NET 알려 주는 키워드 또는 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-277">An operator is a keyword or character that tells ASP.NET what kind of command to perform in an expression.</span></span> <span data-ttu-id="f0ece-278">Visual Basic는 많은 연산자를 지원 하지만 ASP.NET 웹 페이지 개발을 시작 하기 위해 몇 가지를 인식 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-278">Visual Basic supports many operators, but you only need to recognize a few to get started developing ASP.NET web pages.</span></span> <span data-ttu-id="f0ece-279">다음 표에서는 가장 일반적인 연산자를 요약 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-279">The following table summarizes the most common operators.</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="f0ece-280"><strong>연산자</strong></span><span class="sxs-lookup"><span data-stu-id="f0ece-280"><strong>Operator</strong></span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="f0ece-281"><strong>설명</strong></span><span class="sxs-lookup"><span data-stu-id="f0ece-281"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="f0ece-282"><strong>예</strong></span><span class="sxs-lookup"><span data-stu-id="f0ece-282"><strong>Examples</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+ - * /`
    :::column-end:::
    :::column:::
        <span data-ttu-id="f0ece-283">숫자 식에 사용 되는 수학 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-283">Math operators used in numerical expressions.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample29.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
        <span data-ttu-id="f0ece-284">할당 및 같음.</span><span class="sxs-lookup"><span data-stu-id="f0ece-284">Assignment and equality.</span></span> <span data-ttu-id="f0ece-285">컨텍스트에 따라 문의 오른쪽에 있는 값을 좌 변에 있는 개체에 할당 하거나 값이 같은지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-285">Depending on context, either assigns the value on the right side of a statement to the object on the left side, or checks the values for equality.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample30.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `<>`
    :::column-end:::
    :::column:::
        <span data-ttu-id="f0ece-286">같지 않음</span><span class="sxs-lookup"><span data-stu-id="f0ece-286">Inequality.</span></span> <span data-ttu-id="f0ece-287">값이 같지 않으면 `True`을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-287">Returns `True` if the values are not equal.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample31.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
        <span data-ttu-id="f0ece-288">보다 작음, 보다 큼, 작거나 같음, 보다 크거나 같음</span><span class="sxs-lookup"><span data-stu-id="f0ece-288">Less than, greater than, less than or equal, and greater than or equal.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample32.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `&`
    :::column-end:::
    :::column:::
        <span data-ttu-id="f0ece-289">연결-문자열을 조인 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-289">Concatenation, which is used to join strings.</span></span>
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample33.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+= -=`
    :::column-end:::
    :::column:::
        <span data-ttu-id="f0ece-290">증가 및 감소 연산자-변수에서 1 (각각)을 더하거나 뺍니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-290">The increment and decrement operators, which add and subtract 1 (respectively) from a variable.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample34.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `.`
    :::column-end:::
    :::column:::
        <span data-ttu-id="f0ece-291">점과.</span><span class="sxs-lookup"><span data-stu-id="f0ece-291">Dot.</span></span> <span data-ttu-id="f0ece-292">개체와 해당 속성 및 메서드를 구분 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-292">Used to distinguish objects and their properties and methods.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample35.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="f0ece-293">괄호.</span><span class="sxs-lookup"><span data-stu-id="f0ece-293">Parentheses.</span></span> <span data-ttu-id="f0ece-294">식을 그룹화 하 고, 매개 변수를 메서드에 전달 하 고, 배열 및 컬렉션의 멤버에 액세스 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-294">Used to group expressions, to pass parameters to methods, and to access members of arrays and collections.</span></span>
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample36.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `Not`
    :::column-end:::
    :::column:::
        <span data-ttu-id="f0ece-295">나타내지.</span><span class="sxs-lookup"><span data-stu-id="f0ece-295">Not.</span></span> <span data-ttu-id="f0ece-296">True 값을 false로 바꾸고 그 반대의 경우도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-296">Reverses a true value to false and vice versa.</span></span> <span data-ttu-id="f0ece-297">일반적으로 `False` (즉, `True`)을 테스트 하는 간단한 방법으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-297">Typically used as a shorthand way to test for `False` (that is, for not `True`).</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample37.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AndAlso OrElse`
    :::column-end:::
    :::column:::
        <span data-ttu-id="f0ece-298">논리적 AND 및 OR 이며 조건을 함께 연결 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-298">Logical AND and OR, which are used to link conditions together.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample38.vb)]
    :::column-end:::
:::row-end:::

## <a name="working-with-file-and-folder-paths-in-code"></a><span data-ttu-id="f0ece-299">코드에서 파일 및 폴더 경로 작업</span><span class="sxs-lookup"><span data-stu-id="f0ece-299">Working with File and Folder Paths in Code</span></span>

<span data-ttu-id="f0ece-300">코드에서 파일 및 폴더 경로를 사용 하 여 작업 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-300">You'll often work with file and folder paths in your code.</span></span> <span data-ttu-id="f0ece-301">다음은 개발 컴퓨터에 표시 될 수 있는 웹 사이트의 물리적 폴더 구조에 대 한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-301">Here is an example of physical folder structure for a website as it might appear on your development computer:</span></span>

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

<span data-ttu-id="f0ece-302">Url 및 경로에 대 한 몇 가지 필수 정보는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-302">Here are some essential details about URLs and paths:</span></span>

- <span data-ttu-id="f0ece-303">URL은 도메인 이름 (`http://www.example.com`) 또는 서버 이름 (`http://localhost`, `http://mycomputer`)으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-303">A URL begins with either a domain name (`http://www.example.com`) or a server name (`http://localhost`, `http://mycomputer`).</span></span>
- <span data-ttu-id="f0ece-304">URL은 호스트 컴퓨터의 실제 경로에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-304">A URL corresponds to a physical path on a host computer.</span></span> <span data-ttu-id="f0ece-305">예를 들어 `http://myserver` 서버의 *C:\websites\mywebsite* 폴더에 해당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-305">For example, `http://myserver` might correspond to the folder *C:\websites\mywebsite* on the server.</span></span>
- <span data-ttu-id="f0ece-306">가상 경로는 전체 경로를 지정 하지 않고도 코드에서 경로를 나타내는 축약형입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-306">A virtual path is shorthand to represent paths in code without having to specify the full path.</span></span> <span data-ttu-id="f0ece-307">도메인 또는 서버 이름 뒤에 오는 URL의 부분을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-307">It includes the portion of a URL that follows the domain or server name.</span></span> <span data-ttu-id="f0ece-308">가상 경로를 사용 하는 경우 경로를 업데이트 하지 않고도 다른 도메인 이나 서버로 코드를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-308">When you use virtual paths, you can move your code to a different domain or server without having to update the paths.</span></span>

<span data-ttu-id="f0ece-309">차이점을 이해 하는 데 도움이 되는 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-309">Here's an example to help you understand the differences:</span></span>

| <span data-ttu-id="f0ece-310">전체 URL</span><span class="sxs-lookup"><span data-stu-id="f0ece-310">Complete URL</span></span> | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| <span data-ttu-id="f0ece-311">서버 이름</span><span class="sxs-lookup"><span data-stu-id="f0ece-311">Server name</span></span> | <span data-ttu-id="f0ece-312">*mycompanyserver*</span><span class="sxs-lookup"><span data-stu-id="f0ece-312">*mycompanyserver*</span></span> |
| <span data-ttu-id="f0ece-313">가상 경로</span><span class="sxs-lookup"><span data-stu-id="f0ece-313">Virtual path</span></span> | <span data-ttu-id="f0ece-314">*/humanresources/CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="f0ece-314">*/humanresources/CompanyPolicy.htm*</span></span> |
| <span data-ttu-id="f0ece-315">실제 경로</span><span class="sxs-lookup"><span data-stu-id="f0ece-315">Physical path</span></span> | <span data-ttu-id="f0ece-316">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="f0ece-316">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span></span> |

<span data-ttu-id="f0ece-317">C: 드라이브의 루트가 \ 인 것 처럼 가상 루트는/입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-317">The virtual root is /, just like the root of your C: drive is \.</span></span> <span data-ttu-id="f0ece-318">가상 폴더 경로는 항상 슬래시를 사용 합니다. 폴더의 가상 경로에는 물리적 폴더와 동일한 이름을 사용할 수 없습니다. 별칭 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-318">(Virtual folder paths always use forward slashes.) The virtual path of a folder doesn't have to have the same name as the physical folder; it can be an alias.</span></span> <span data-ttu-id="f0ece-319">프로덕션 서버에서 가상 경로는 정확히 실제 경로와 거의 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-319">(On production servers, the virtual path rarely matches an exact physical path.)</span></span>

<span data-ttu-id="f0ece-320">코드에서 파일 및 폴더를 사용할 때 사용 하는 개체에 따라 실제 경로와 때때로 가상 경로를 참조 해야 하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-320">When you work with files and folders in code, sometimes you need to reference the physical path and sometimes a virtual path, depending on what objects you're working with.</span></span> <span data-ttu-id="f0ece-321">ASP.NET는 코드에서 파일 및 폴더 경로를 사용 하기 위한 다음과 같은 도구를 제공 합니다. `Server.MapPath` 메서드 및 `~` 연산자 및 `Href` 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-321">ASP.NET gives you these tools for working with file and folder paths in code: the `Server.MapPath` method, and the `~` operator and `Href` method.</span></span>

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a><span data-ttu-id="f0ece-322">가상에서 실제 경로로 변환: Server. MapPath 메서드</span><span class="sxs-lookup"><span data-stu-id="f0ece-322">Converting virtual to physical paths: the Server.MapPath method</span></span>

<span data-ttu-id="f0ece-323">`Server.MapPath` 메서드는 가상 경로 (예: */default.cshtml*)를 절대 실제 경로 (예: *C:\WebSites\MyWebSiteFolder\default.cshtml*)로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-323">The `Server.MapPath` method converts a virtual path (like */default.cshtml*) to an absolute physical path (like *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span></span> <span data-ttu-id="f0ece-324">이 메서드는 전체 실제 경로가 필요할 때마다 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-324">You use this method any time you need a complete physical path.</span></span> <span data-ttu-id="f0ece-325">일반적인 예로 웹 서버에서 텍스트 파일 또는 이미지 파일을 읽거나 쓰는 경우를 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-325">A typical example is when you're reading or writing a text file or image file on the web server.</span></span>

<span data-ttu-id="f0ece-326">일반적으로 호스팅 사이트 서버에서 사이트의 절대 실제 경로를 알 수 없으므로이 메서드는 사용자가 알고 있는 경로 (가상 경로)를 서버의 해당 경로로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-326">You typically don't know the absolute physical path of your site on a hosting site's server, so this method can convert the path you do know — the virtual path — to the corresponding path on the server for you.</span></span> <span data-ttu-id="f0ece-327">파일이 나 폴더에 대 한 가상 경로를 메서드에 전달 하 고 실제 경로를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-327">You pass the virtual path to a file or folder to the method, and it returns the physical path:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample39.vbhtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a><span data-ttu-id="f0ece-328">가상 루트 참조: ~ operator 및 Href 메서드</span><span class="sxs-lookup"><span data-stu-id="f0ece-328">Referencing the virtual root: the ~ operator and Href method</span></span>

<span data-ttu-id="f0ece-329">*Cshtml* 또는 *vbhtml* 파일에서 `~` 연산자를 사용 하 여 가상 루트 경로를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-329">In a *.cshtml* or *.vbhtml* file, you can reference the virtual root path using the `~` operator.</span></span> <span data-ttu-id="f0ece-330">이는 사이트에서 페이지를 이동할 수 있으며 다른 페이지에 포함 된 모든 링크가 손상 되지 않도록 하기 때문에 매우 편리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-330">This is very handy because you can move pages around in a site, and any links they contain to other pages won't be broken.</span></span> <span data-ttu-id="f0ece-331">웹 사이트를 다른 위치로 이동 하는 경우에도 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-331">It's also handy in case you ever move your website to a different location.</span></span> <span data-ttu-id="f0ece-332">예를 들어 다음과 같은 노래를 선택할 수 있다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-332">Here are some examples:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample40.vbhtml)]

<span data-ttu-id="f0ece-333">웹 사이트가 `http://myserver/myapp`경우 페이지가 실행 될 때 ASP.NET에서 이러한 경로를 처리 하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-333">If the website is `http://myserver/myapp`, here's how ASP.NET will treat these paths when the page runs:</span></span>

- <span data-ttu-id="f0ece-334">`myImagesFolder`: `http://myserver/myapp/images`</span><span class="sxs-lookup"><span data-stu-id="f0ece-334">`myImagesFolder`: `http://myserver/myapp/images`</span></span>
- <span data-ttu-id="f0ece-335">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span><span class="sxs-lookup"><span data-stu-id="f0ece-335">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span></span>

<span data-ttu-id="f0ece-336">이러한 경로는 변수의 값으로 실제로 표시 되지 않지만 ASP.NET는 경로를 해당 하는 것 처럼 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-336">(You won't actually see these paths as the values of the variable, but ASP.NET will treat the paths as if that's what they were.)</span></span>

<span data-ttu-id="f0ece-337">다음과 같이 서버 코드와 태그에서 모두 `~` 연산자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-337">You can use the `~` operator both in server code (as above) and in markup, like this:</span></span>

[!code-html[Main](introducing-razor-syntax-vb/samples/sample41.html)]

<span data-ttu-id="f0ece-338">태그에서 `~` 연산자를 사용 하 여 이미지 파일, 다른 웹 페이지 및 CSS 파일과 같은 리소스에 대 한 경로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-338">In markup, you use the `~` operator to create paths to resources like image files, other web pages, and CSS files.</span></span> <span data-ttu-id="f0ece-339">페이지가 실행 될 때 ASP.NET는 페이지 (코드 및 태그 모두)를 살펴보고 적절 한 경로에 대 한 모든 `~` 참조를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-339">When the page runs, ASP.NET looks through the page (both code and markup) and resolves all the `~` references to the appropriate path.</span></span>

## <a name="conditional-logic-and-loops"></a><span data-ttu-id="f0ece-340">조건부 논리 및 루프</span><span class="sxs-lookup"><span data-stu-id="f0ece-340">Conditional Logic and Loops</span></span>

<span data-ttu-id="f0ece-341">ASP.NET 서버 코드를 사용 하면 조건에 따라 작업을 수행 하 고 특정 횟수 (루프를 실행 하는 코드)로 문을 반복 하는 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-341">ASP.NET server code lets you perform tasks based on conditions and write code that repeats statements a specific number of times that is, code that runs a loop).</span></span>

### <a name="testing-conditions"></a><span data-ttu-id="f0ece-342">테스트 조건</span><span class="sxs-lookup"><span data-stu-id="f0ece-342">Testing conditions</span></span>

<span data-ttu-id="f0ece-343">간단한 조건을 테스트 하려면 지정 하는 테스트에 따라 `True` 또는 `False`를 반환 하는 `If...Then` 문을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-343">To test a simple condition you use the `If...Then` statement, which returns `True` or `False` based on a test you specify:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample42.vbhtml)]

<span data-ttu-id="f0ece-344">`If` 키워드는 블록을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-344">The `If` keyword starts a block.</span></span> <span data-ttu-id="f0ece-345">실제 테스트 (조건)는 `If` 키워드를 따르며 true 또는 false를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-345">The actual test (condition) follows the `If` keyword and returns true or false.</span></span> <span data-ttu-id="f0ece-346">`If` 문이 `Then`로 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-346">The `If` statement ends with `Then`.</span></span> <span data-ttu-id="f0ece-347">테스트를 true로 설정 하는 경우 실행 되는 문은 `If` 및 `End If`으로 묶입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-347">The statements that will run if the test is true are enclosed by `If` and `End If`.</span></span> <span data-ttu-id="f0ece-348">`If` 문은 조건이 false 인 경우 실행할 문을 지정 하는 `Else` 블록을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-348">An `If` statement can include an `Else` block that specifies statements to run if the condition is false:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample43.vbhtml)]

<span data-ttu-id="f0ece-349">`If` 문이 코드 블록을 시작 하는 경우 일반적인 `Code...End Code` 문을 사용 하 여 블록을 포함할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-349">If an `If` statement starts a code block, you don't have to use the normal `Code...End Code` statements to include the blocks.</span></span> <span data-ttu-id="f0ece-350">블록에 `@`를 추가 하기만 하면 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-350">You can just add `@` to the block, and it will work.</span></span> <span data-ttu-id="f0ece-351">이 방법은 `If`와 함께 사용할 수 있으며, `For`, `For Each`, `Do While`등의 코드 블록 뒤에 나오는 기타 Visual Basic 프로그래밍 키워드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-351">This approach works with `If` as well as other Visual Basic programming keywords that are followed by code blocks, including `For`, `For Each`, `Do While`, etc.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample44.vbhtml)]

<span data-ttu-id="f0ece-352">하나 이상의 `ElseIf` 블록을 사용 하 여 여러 조건을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-352">You can add multiple conditions using one or more `ElseIf` blocks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample45.vbhtml)]

<span data-ttu-id="f0ece-353">이 예에서는 `If` 블록의 첫 번째 조건이 true가 아니면 `ElseIf` 조건이 검사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-353">In this example, if the first condition in the `If` block is not true, the `ElseIf` condition is checked.</span></span> <span data-ttu-id="f0ece-354">이러한 조건이 충족 되 면 `ElseIf` 블록의 문이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-354">If that condition is met, the statements in the `ElseIf` block are executed.</span></span> <span data-ttu-id="f0ece-355">조건을 충족 하는 조건이 없으면 `Else` 블록의 문이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-355">If none of the conditions are met, the statements in the `Else` block are executed.</span></span> <span data-ttu-id="f0ece-356">개수에 관계 없이 `ElseIf` 블록을 추가한 다음 `Else` 블록을 사용 하 여 다른 모든&quot; 조건으로 &quot;수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-356">You can add any number of `ElseIf` blocks, and then close with an `Else` block as the &quot;everything else&quot; condition.</span></span>

<span data-ttu-id="f0ece-357">많은 수의 조건을 테스트 하려면 `Select Case` 블록을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-357">To test a large number of conditions, use a `Select Case` block:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample46.vbhtml)]

<span data-ttu-id="f0ece-358">테스트할 값이 괄호 안에 있습니다 (예: weekday 변수).</span><span class="sxs-lookup"><span data-stu-id="f0ece-358">The value to test is in parentheses (in the example, the weekday variable).</span></span> <span data-ttu-id="f0ece-359">각 개별 테스트는 값을 나열 하는 `Case` 문을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-359">Each individual test uses a `Case` statement that lists a value.</span></span> <span data-ttu-id="f0ece-360">`Case` 문의 값이 테스트 값과 일치 하면 해당 `Case` 블록의 코드가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-360">If the value of a `Case` statement matches the test value, the code in that `Case` block is executed.</span></span>

<span data-ttu-id="f0ece-361">브라우저에 표시 되는 마지막 두 조건부 블록의 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-361">The result of the last two conditional blocks displayed in a browser:</span></span>

![Razor-Img10](introducing-razor-syntax-vb/_static/image10.jpg)

### <a name="looping-code"></a><span data-ttu-id="f0ece-363">반복 코드</span><span class="sxs-lookup"><span data-stu-id="f0ece-363">Looping code</span></span>

<span data-ttu-id="f0ece-364">동일한 문을 반복적으로 실행 해야 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-364">You often need to run the same statements repeatedly.</span></span> <span data-ttu-id="f0ece-365">이렇게 하려면 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-365">You do this by looping.</span></span> <span data-ttu-id="f0ece-366">예를 들어 데이터 컬렉션의 각 항목에 대해 동일한 문을 실행 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-366">For example, you often run the same statements for each item in a collection of data.</span></span> <span data-ttu-id="f0ece-367">반복 하려는 횟수를 정확히 알고 있는 경우 `For` 루프를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-367">If you know exactly how many times you want to loop, you can use a `For` loop.</span></span> <span data-ttu-id="f0ece-368">이러한 종류의 루프는 계산 하거나 계산 하는 데 특히 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-368">This kind of loop is especially useful for counting up or counting down:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample47.vbhtml)]

<span data-ttu-id="f0ece-369">루프는 `For` 키워드로 시작 하 고 그 뒤에 세 개의 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-369">The loop begins with the `For` keyword, followed by three elements:</span></span>

- <span data-ttu-id="f0ece-370">`For` 문 바로 다음에는 카운터 변수를 선언 하 고 (`Dim`를 사용할 필요가 없음) `i = 10 to 20`에서와 같이 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-370">Immediately after the `For` statement, you declare a counter variable (you don't have to use `Dim`) and then indicate the range, as in `i = 10 to 20`.</span></span> <span data-ttu-id="f0ece-371">즉, `i` 변수는 10에서 계산을 시작 하 고 20 (포함)에 도달할 때까지 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-371">This means the variable `i` will start counting at 10 and continue until it reaches 20 (inclusive).</span></span>
- <span data-ttu-id="f0ece-372">`For` 문과 `Next` 문은 블록의 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-372">Between the `For` and `Next` statements is the content of the block.</span></span> <span data-ttu-id="f0ece-373">여기에는 각 루프에서 실행 되는 하나 이상의 코드 문이 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-373">This can contain one or more code statements that execute with each loop.</span></span>
- <span data-ttu-id="f0ece-374">`Next i` 문은 루프를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-374">The `Next i` statement ends the loop.</span></span> <span data-ttu-id="f0ece-375">카운터를 증가 시키고 루프의 다음 반복을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-375">It increments the counter and starts the next iteration of the loop.</span></span>

<span data-ttu-id="f0ece-376">`For`와 `Next` 줄 사이에 있는 코드 줄에는 루프가 반복 될 때마다 실행 되는 코드가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-376">The line of code between the `For` and `Next` lines contains the code that runs for each iteration of the loop.</span></span> <span data-ttu-id="f0ece-377">태그는 매번 새 단락 (`<p>` 요소)을 만들고 출력에 줄을 추가 하 여 i (카운터)의 값을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-377">The markup creates a new paragraph (`<p>` element) each time and adds a line to the output, displaying the value of i (the counter).</span></span> <span data-ttu-id="f0ece-378">이 페이지를 실행 하는 경우이 예제에서는 출력을 표시 하는 11 개의 줄을 만들며 각 줄의 텍스트는 항목 번호를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-378">When you run this page, the example creates 11 lines displaying the output, with the text in each line indicating the item number.</span></span>

![Razor-Img11](introducing-razor-syntax-vb/_static/image11.jpg)

<span data-ttu-id="f0ece-380">컬렉션 또는 배열에 대 한 작업을 수행 하는 경우에는 종종 `For Each` 루프를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-380">If you're working with a collection or array, you often use a `For Each` loop.</span></span> <span data-ttu-id="f0ece-381">컬렉션은 유사한 개체의 그룹 이며, `For Each` 루프를 사용 하 여 컬렉션의 각 항목에 대 한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-381">A collection is a group of similar objects, and the `For Each` loop lets you carry out a task on each item in the collection.</span></span> <span data-ttu-id="f0ece-382">이 유형의 루프는 `For` 루프와 달리 카운터를 증가 시키거나 제한을 설정할 필요가 없기 때문에 컬렉션에 편리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-382">This type of loop is convenient for collections, because unlike a `For` loop, you don't have to increment the counter or set a limit.</span></span> <span data-ttu-id="f0ece-383">대신 `For Each` 루프 코드는 완료 될 때까지 컬렉션을 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-383">Instead, the `For Each` loop code simply proceeds through the collection until it's finished.</span></span>

<span data-ttu-id="f0ece-384">이 예제에서는 웹 서버에 대 한 정보를 포함 하는 `Request.ServerVariables` 컬렉션의 항목을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-384">This example returns the items in the `Request.ServerVariables` collection (which contains information about your web server).</span></span> <span data-ttu-id="f0ece-385">`For Each` 루프를 사용 하 여 HTML 글머리 기호 목록에 새 `<li>` 요소를 만들어 각 항목의 이름을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-385">It uses a `For Each` loop to display the name of each item by creating a new `<li>` element in an HTML bulleted list.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample48.vbhtml)]

<span data-ttu-id="f0ece-386">`For Each` 키워드 뒤에는 컬렉션의 단일 항목을 나타내는 변수 (예: `myItem`)가 오고 그 뒤에 `In` 키워드가 오고 그 뒤에 반복 하려는 컬렉션이 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-386">The `For Each` keyword is followed by a variable that represents a single item in the collection (in the example, `myItem`), followed by the `In` keyword, followed by the collection you want to loop through.</span></span> <span data-ttu-id="f0ece-387">`For Each` 루프의 본문에서 이전에 선언한 변수를 사용 하 여 현재 항목에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-387">In the body of the `For Each` loop, you can access the current item using the variable that you declared earlier.</span></span>

![Razor-Img12](introducing-razor-syntax-vb/_static/image12.jpg)

<span data-ttu-id="f0ece-389">보다 일반적인 용도의 루프를 만들려면 `Do While` 문을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-389">To create a more general-purpose loop, use the `Do While` statement:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample49.vbhtml)]

<span data-ttu-id="f0ece-390">이 루프는 `Do While` 키워드와 조건, 반복 되는 블록 순서로 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-390">This loop begins with the `Do While` keyword, followed by a condition, followed by the block to repeat.</span></span> <span data-ttu-id="f0ece-391">루프는 일반적으로 계산에 사용 되는 변수 또는 개체를 증가 (추가) 또는 감소 (빼기) 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-391">Loops typically increment (add to) or decrement (subtract from) a variable or object used for counting.</span></span> <span data-ttu-id="f0ece-392">예제에서 `+=` 연산자는 루프가 실행 될 때마다 변수 값에 1을 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-392">In the example, the `+=` operator adds 1 to the value of a variable each time the loop runs.</span></span> <span data-ttu-id="f0ece-393">(에서 계산 되는 루프의 변수를 감소 시키려면 감소 연산자 `-=`를 사용 합니다.)</span><span class="sxs-lookup"><span data-stu-id="f0ece-393">(To decrement a variable in a loop that counts down, you would use the decrement operator `-=`.)</span></span>

## <a name="objects-and-collections"></a><span data-ttu-id="f0ece-394">개체 및 컬렉션</span><span class="sxs-lookup"><span data-stu-id="f0ece-394">Objects and Collections</span></span>

<span data-ttu-id="f0ece-395">ASP.NET 웹 사이트의 거의 모든 항목은 웹 페이지를 포함 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-395">Nearly everything in an ASP.NET website is an object, including the web page itself.</span></span> <span data-ttu-id="f0ece-396">이 섹션에서는 코드에서 자주 사용 하는 몇 가지 중요 한 개체에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-396">This section discusses some important objects you'll work with frequently in your code.</span></span>

### <a name="page-objects"></a><span data-ttu-id="f0ece-397">Page 개체</span><span class="sxs-lookup"><span data-stu-id="f0ece-397">Page objects</span></span>

<span data-ttu-id="f0ece-398">ASP.NET의 가장 기본적인 개체는 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-398">The most basic object in ASP.NET is the page.</span></span> <span data-ttu-id="f0ece-399">정규화 된 개체 없이 페이지 개체의 속성에 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-399">You can access properties of the page object directly without any qualifying object.</span></span> <span data-ttu-id="f0ece-400">다음 코드에서는 페이지의 `Request` 개체를 사용 하 여 페이지의 파일 경로를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-400">The following code gets the page's file path, using the `Request` object of the page:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample50.vbhtml)]

<span data-ttu-id="f0ece-401">`Page` 개체의 속성을 사용 하 여 다음과 같은 많은 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-401">You can use properties of the `Page` object to get a lot of information, such as:</span></span>

- <span data-ttu-id="f0ece-402">`Request`입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-402">`Request`.</span></span> <span data-ttu-id="f0ece-403">앞서 살펴본 것 처럼, 요청을 만든 브라우저의 유형, 페이지 URL, 사용자 id 등을 포함 하 여 현재 요청에 대 한 정보 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-403">As you've already seen, this is a collection of information about the current request, including what type of browser made the request, the URL of the page, the user identity, etc.</span></span>
- <span data-ttu-id="f0ece-404">`Response`입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-404">`Response`.</span></span> <span data-ttu-id="f0ece-405">서버 코드의 실행이 완료 되 면 브라우저로 전송 되는 응답 (페이지)에 대 한 정보 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-405">This is a collection of information about the response (page) that will be sent to the browser when the server code has finished running.</span></span> <span data-ttu-id="f0ece-406">예를 들어이 속성을 사용 하 여 응답에 정보를 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-406">For example, you can use this property to write information into the response.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample51.vbhtml)]

### <a name="collection-objects-arrays-and-dictionaries"></a><span data-ttu-id="f0ece-407">컬렉션 개체 (배열 및 사전)</span><span class="sxs-lookup"><span data-stu-id="f0ece-407">Collection objects (arrays and dictionaries)</span></span>

<span data-ttu-id="f0ece-408">컬렉션은 데이터베이스의 `Customer` 개체 컬렉션과 같이 동일한 유형의 개체 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-408">A collection is a group of objects of the same type, such as a collection of `Customer` objects from a database.</span></span> <span data-ttu-id="f0ece-409">ASP.NET에는 `Request.Files` 컬렉션과 같은 여러 기본 제공 컬렉션이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-409">ASP.NET contains many built-in collections, like the `Request.Files` collection.</span></span>

<span data-ttu-id="f0ece-410">컬렉션의 데이터로 작업 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-410">You'll often work with data in collections.</span></span> <span data-ttu-id="f0ece-411">두 가지 일반적인 컬렉션 형식은 *배열* 및 *사전*입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-411">Two common collection types are the *array* and the *dictionary*.</span></span> <span data-ttu-id="f0ece-412">배열은 비슷한 항목의 컬렉션을 저장 하지만 각 항목을 저장할 별도의 변수를 만들지 않으려는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-412">An array is useful when you want to store a collection of similar items but don't want to create a separate variable to hold each item:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample52.vbhtml)]

<span data-ttu-id="f0ece-413">배열을 사용 하 여 `String`, `Integer`또는 `DateTime`와 같은 특정 데이터 형식을 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-413">With arrays, you declare a specific data type, such as `String`, `Integer`, or `DateTime`.</span></span> <span data-ttu-id="f0ece-414">변수에 배열이 포함 될 수 있음을 나타내려면 선언에서 변수 이름에 괄호를 추가 합니다 (예: `Dim myVar() As String`).</span><span class="sxs-lookup"><span data-stu-id="f0ece-414">To indicate that the variable can contain an array, you add parentheses to the variable name in the declaration (such as `Dim myVar() As String`).</span></span> <span data-ttu-id="f0ece-415">해당 위치 (인덱스)를 사용 하거나 `For Each` 문을 사용 하 여 배열의 항목에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-415">You can access items in an array using their position (index) or by using the `For Each` statement.</span></span> <span data-ttu-id="f0ece-416">배열 인덱스는 0부터 시작 &#8212; 합니다. 즉, 첫 번째 항목의 위치는 0이 고, 두 번째 항목은 위치 1에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-416">Array indexes are zero-based &#8212; that is, the first item is at position 0, the second item is at position 1, and so on.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample53.vbhtml)]

<span data-ttu-id="f0ece-417">`Length` 속성을 가져와서 배열의 항목 수를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-417">You can determine the number of items in an array by getting its `Length` property.</span></span> <span data-ttu-id="f0ece-418">배열에서 특정 항목의 위치를 가져오려면 (즉, 배열 검색) `Array.IndexOf` 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-418">To get the position of a specific item in the array (that is, to search the array), use the `Array.IndexOf` method.</span></span> <span data-ttu-id="f0ece-419">배열의 콘텐츠를 반전 (`Array.Reverse` 메서드) 하거나 내용을 정렬 (`Array.Sort` 메서드) 하는 등의 작업을 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-419">You can also do things like reverse the contents of an array (the `Array.Reverse` method) or sort the contents (the `Array.Sort` method).</span></span>

<span data-ttu-id="f0ece-420">브라우저에 표시 되는 문자열 배열 코드의 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-420">The output of the string array code displayed in a browser:</span></span>

![Razor-Img13](introducing-razor-syntax-vb/_static/image13.jpg)

<span data-ttu-id="f0ece-422">사전은 키 (또는 이름)를 제공 하 여 해당 값을 설정 하거나 검색할 수 있는 키/값 쌍의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-422">A dictionary is a collection of key/value pairs, where you provide the key (or name) to set or retrieve the corresponding value:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample54.vbhtml)]

<span data-ttu-id="f0ece-423">사전을 만들려면 `New` 키워드를 사용 하 여 새 `Dictionary` 개체를 만들고 있음을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-423">To create a dictionary, you use the `New` keyword to indicate that you're creating a new `Dictionary` object.</span></span> <span data-ttu-id="f0ece-424">`Dim` 키워드를 사용 하 여 변수에 사전을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-424">You can assign a dictionary to a variable using the `Dim` keyword.</span></span> <span data-ttu-id="f0ece-425">괄호 (`( )`)를 사용 하 여 사전에 있는 항목의 데이터 형식을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-425">You indicate the data types of the items in the dictionary using parentheses ( `( )` ).</span></span> <span data-ttu-id="f0ece-426">선언 끝에서 다른 괄호 쌍을 추가 해야 합니다 .이는 실제로 새 사전을 만드는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-426">At the end of the declaration, you must add another pair of parentheses, because this is actually a method that creates a new dictionary.</span></span>

<span data-ttu-id="f0ece-427">사전에 항목을 추가 하려면 사전 변수의 `Add` 메서드 (이 경우`myScores`)를 호출한 다음 키와 값을 지정 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-427">To add items to the dictionary, you can call the `Add` method of the dictionary variable (`myScores` in this case), and then specify a key and a value.</span></span> <span data-ttu-id="f0ece-428">또는 다음 예제와 같이 괄호를 사용 하 여 키를 나타내고 간단한 할당을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-428">Alternatively, you can use parentheses to indicate the key and do a simple assignment, as in the following example:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample55.vbhtml)]

<span data-ttu-id="f0ece-429">사전에서 값을 가져오려면 괄호 안에 키를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-429">To get a value from the dictionary, you specify the key in parentheses:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample56.vbhtml)]

## <a name="calling-methods-with-parameters"></a><span data-ttu-id="f0ece-430">매개 변수를 사용 하 여 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="f0ece-430">Calling Methods with Parameters</span></span>

<span data-ttu-id="f0ece-431">이 문서 앞부분에서 살펴본 것 처럼를 사용 하 여 프로그래밍 하는 개체에는 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-431">As you saw earlier in this article, the objects that you program with have methods.</span></span> <span data-ttu-id="f0ece-432">예를 들어 `Database` 개체에는 `Database.Connect` 메서드가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-432">For example, a `Database` object might have a `Database.Connect` method.</span></span> <span data-ttu-id="f0ece-433">또한 많은 메서드에 하나 이상의 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-433">Many methods also have one or more parameters.</span></span> <span data-ttu-id="f0ece-434">*매개 변수* 는 메서드가 해당 작업을 완료할 수 있도록 메서드에 전달 하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-434">A *parameter* is a value that you pass to a method to enable the method to complete its task.</span></span> <span data-ttu-id="f0ece-435">예를 들어 다음 세 개의 매개 변수를 사용 하는 `Request.MapPath` 메서드에 대 한 선언을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="f0ece-435">For example, look at a declaration for the `Request.MapPath` method, which takes three parameters:</span></span>

[!code-vb[Main](introducing-razor-syntax-vb/samples/sample57.vb)]

<span data-ttu-id="f0ece-436">이 메서드는 지정 된 가상 경로에 해당 하는 서버의 실제 경로를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-436">This method returns the physical path on the server that corresponds to a specified virtual path.</span></span> <span data-ttu-id="f0ece-437">메서드에 대 한 세 가지 매개 변수는 `virtualPath`, `baseVirtualDir`및 `allowCrossAppMapping`입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-437">The three parameters for the method are `virtualPath`, `baseVirtualDir`, and `allowCrossAppMapping`.</span></span> <span data-ttu-id="f0ece-438">선언에서 매개 변수는 허용 되는 데이터의 데이터 형식과 함께 나열 됩니다. 이 메서드를 호출 하는 경우 세 매개 변수 모두에 대 한 값을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-438">(Notice that in the declaration, the parameters are listed with the data types of the data that they'll accept.) When you call this method, you must supply values for all three parameters.</span></span>

<span data-ttu-id="f0ece-439">Razor 구문와 함께 Visual Basic를 사용 하는 경우 메서드에 매개 변수를 전달 하는 두 가지 옵션 ( *위치 매개 변수* 또는 *명명 된 매개*변수)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-439">When you're using Visual Basic with the Razor syntax, you have two options for passing parameters to a method: *positional parameters* or *named parameters*.</span></span> <span data-ttu-id="f0ece-440">위치 매개 변수를 사용 하 여 메서드를 호출 하려면 메서드 선언에 지정 된 엄격한 순서로 매개 변수를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-440">To call a method using positional parameters, you pass the parameters in a strict order that's specified in the method declaration.</span></span> <span data-ttu-id="f0ece-441">(일반적으로 메서드의 설명서를 읽어이 순서를 확인 합니다.) 순서를 따라야 하며 필요한 경우 매개 변수 &#8212; 를 건너뛸 수 없습니다. 값이 없는 위치 매개 변수에 대해 빈 문자열 (`""`) 또는 null을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-441">(You would typically know this order by reading documentation for the method.) You must follow the order, and you can't skip any of the parameters &#8212; if necessary, you pass an empty string (`""`) or null for a positional parameter that you don't have a value for.</span></span>

<span data-ttu-id="f0ece-442">다음 예제에서는 웹 사이트에 *scripts* 라는 폴더가 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-442">The following example assumes you have a folder named *scripts* on your website.</span></span> <span data-ttu-id="f0ece-443">이 코드는 `Request.MapPath` 메서드를 호출 하 고 세 개의 매개 변수에 대 한 값을 올바른 순서로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-443">The code calls the `Request.MapPath` method and passes values for the three parameters in the correct order.</span></span> <span data-ttu-id="f0ece-444">그런 다음 결과 매핑된 경로를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-444">It then displays the resulting mapped path.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample58.vbhtml)]

<span data-ttu-id="f0ece-445">메서드에 대 한 매개 변수가 많은 경우 명명 된 매개 변수를 사용 하 여 코드를 더 간결 하 고 읽기 쉽게 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-445">When there are many parameters for a method, you can keep your code cleaner and more readable by using named parameters.</span></span> <span data-ttu-id="f0ece-446">명명 된 매개 변수를 사용 하 여 메서드를 호출 하려면 매개 변수 이름 뒤에 `:=`를 지정 하 고 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-446">To call a method using named parameters, specify the parameter name followed by `:=` and then provide the value.</span></span> <span data-ttu-id="f0ece-447">명명 된 매개 변수의 장점은 원하는 순서로 추가할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-447">An advantage of named parameters is that you can add them in any order you want.</span></span> <span data-ttu-id="f0ece-448">이는 메서드 호출이 압축 되지 않는다는 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-448">(A disadvantage is that the method call is not as compact.)</span></span>

<span data-ttu-id="f0ece-449">다음 예제에서는 위와 동일한 메서드를 호출 하지만 명명 된 매개 변수를 사용 하 여 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-449">The following example calls the same method as above, but uses named parameters to supply the values:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample59.vbhtml)]

<span data-ttu-id="f0ece-450">여기에서 볼 수 있듯이 매개 변수는 다른 순서로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-450">As you can see, the parameters are passed in a different order.</span></span> <span data-ttu-id="f0ece-451">그러나 이전 예제와이 예제를 실행 하면 동일한 값이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-451">However, if you run the previous example and this example, they'll return the same value.</span></span>

## <a name="handling-errors"></a><span data-ttu-id="f0ece-452">오류 처리</span><span class="sxs-lookup"><span data-stu-id="f0ece-452">Handling Errors</span></span>

### <a name="try-catch-statements"></a><span data-ttu-id="f0ece-453">Try-catch 문</span><span class="sxs-lookup"><span data-stu-id="f0ece-453">Try-Catch statements</span></span>

<span data-ttu-id="f0ece-454">코드에 컨트롤 외부의 이유로 실패할 수 있는 문이 종종 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-454">You'll often have statements in your code that might fail for reasons outside your control.</span></span> <span data-ttu-id="f0ece-455">다음은 그 예입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-455">For example:</span></span>

- <span data-ttu-id="f0ece-456">코드에서 파일 열기, 만들기, 읽기 또는 쓰기를 시도 하는 경우 모든 종류의 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-456">If your code tries to open, create, read, or write a file, all sorts of errors might occur.</span></span> <span data-ttu-id="f0ece-457">필요한 파일이 없거나, 잠겨 있거나, 코드에 권한이 없을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-457">The file you want might not exist, it might be locked, the code might not have permissions, and so on.</span></span>
- <span data-ttu-id="f0ece-458">마찬가지로, 코드에서 데이터베이스의 레코드를 업데이트 하려고 시도 하는 경우에는 사용 권한 문제가 있을 수 있습니다. 데이터베이스에 대 한 연결이 삭제 될 수 있습니다. 저장할 데이터가 유효 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-458">Similarly, if your code tries to update records in a database, there can be permissions issues, the connection to the database might be dropped, the data to save might be invalid, and so on.</span></span>

<span data-ttu-id="f0ece-459">프로그래밍 측면에서 이러한 상황을 *예외*라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-459">In programming terms, these situations are called *exceptions*.</span></span> <span data-ttu-id="f0ece-460">코드에서 예외가 발생 하는 경우 사용자에 게 가장 잘 방해가 되는 오류 메시지를 생성 (throw) 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-460">If your code encounters an exception, it generates (throws) an error message that is, at best, annoying to users.</span></span>

![Razor-Img14](introducing-razor-syntax-vb/_static/image14.jpg)

<span data-ttu-id="f0ece-462">코드에 예외가 발생할 수 있는 상황에서이 유형의 오류 메시지를 방지 하기 위해 `Try/Catch` 문을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-462">In situations where your code might encounter exceptions, and in order to avoid error messages of this type, you can use `Try/Catch` statements.</span></span> <span data-ttu-id="f0ece-463">`Try` 문에서 확인 중인 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-463">In the `Try` statement, you run the code that you're checking.</span></span> <span data-ttu-id="f0ece-464">하나 이상의 `Catch` 문에서 발생 했을 수 있는 특정 오류 (특정 유형의 예외)를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-464">In one or more `Catch` statements, you can look for specific errors (specific types of exceptions) that might have occurred.</span></span> <span data-ttu-id="f0ece-465">예상 되는 오류를 찾기 위해 필요한 만큼 `Catch` 문을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-465">You can include as many `Catch` statements as you need to look for errors that you're anticipating.</span></span>

> [!NOTE]
> <span data-ttu-id="f0ece-466">`Try/Catch` 문에서는 `Response.Redirect` 메서드를 사용 하지 않는 것이 좋습니다 .이는 페이지에서 예외를 발생 시킬 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-466">We recommend that you avoid using the `Response.Redirect` method in `Try/Catch` statements, because it can cause an exception in your page.</span></span>

<span data-ttu-id="f0ece-467">다음 예에서는 첫 번째 요청에서 텍스트 파일을 만든 다음 사용자가 파일을 열 수 있도록 하는 단추를 표시 하는 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-467">The following example shows a page that creates a text file on the first request and then displays a button that lets the user open the file.</span></span> <span data-ttu-id="f0ece-468">이 예제에서는 예외를 발생 시 키 지 않도록 의도적으로 잘못 된 파일 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-468">The example deliberately uses a bad file name so that it will cause an exception.</span></span> <span data-ttu-id="f0ece-469">이 코드에는 두 가지 예외에 대 한 `Catch` 문이 포함 되어 있습니다. `FileNotFoundException`는 파일 이름이 잘못 된 경우에 발생 하는 것이 고, ASP.NET에서 폴더를 찾을 수 없는 경우에 발생 하는 `DirectoryNotFoundException`입니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-469">The code includes `Catch` statements for two possible exceptions: `FileNotFoundException`, which occurs if the file name is bad, and `DirectoryNotFoundException`, which occurs if ASP.NET can't even find the folder.</span></span> <span data-ttu-id="f0ece-470">(모든 것이 제대로 작동 하는 경우 실행 되는 방식을 확인 하기 위해 예제에서 문의 주석 처리를 제거할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="f0ece-470">(You can uncomment a statement in the example in order to see how it runs when everything works properly.)</span></span>

<span data-ttu-id="f0ece-471">코드에서 예외를 처리 하지 않은 경우 이전 스크린샷과 같은 오류 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-471">If your code didn't handle the exception, you would see an error page like the previous screen shot.</span></span> <span data-ttu-id="f0ece-472">그러나 `Try/Catch` 섹션을 사용 하면 사용자가 이러한 유형의 오류를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0ece-472">However, the `Try/Catch` section helps prevent the user from seeing these types of errors.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample60.vbhtml)]

## <a name="additional-resources"></a><span data-ttu-id="f0ece-473">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f0ece-473">Additional Resources</span></span>

### <a name="reference-documentation"></a><span data-ttu-id="f0ece-474">참조 설명서</span><span class="sxs-lookup"><span data-stu-id="f0ece-474">Reference Documentation</span></span>

- [<span data-ttu-id="f0ece-475">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f0ece-475">ASP.NET</span></span>](https://msdn.microsoft.com/library/ee532866.aspx)
- [<span data-ttu-id="f0ece-476">Visual Basic 언어</span><span class="sxs-lookup"><span data-stu-id="f0ece-476">Visual Basic Language</span></span>](https://msdn.microsoft.com/library/2x7h1hfk.aspx)
