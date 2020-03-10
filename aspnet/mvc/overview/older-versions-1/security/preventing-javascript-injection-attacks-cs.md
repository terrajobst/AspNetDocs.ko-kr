---
uid: mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-cs
title: JavaScript 삽입 공격 방지 (C#) | Microsoft Docs
author: StephenWalther
description: JavaScript 삽입 공격 및 사이트 간 스크립팅 공격이 발생 하지 않도록 합니다. 이 자습서에서 Stephen Walther는 쉽게 제거할 수 있는 방법을 설명 합니다.
ms.author: riande
ms.date: 08/19/2008
ms.assetid: d0136da6-81a4-4815-b002-baa84744c09e
msc.legacyurl: /mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-cs
msc.type: authoredcontent
ms.openlocfilehash: fb00ee8a7e3d678e824052060eb5d9fd5d4b6a42
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485933"
---
# <a name="preventing-javascript-injection-attacks-c"></a><span data-ttu-id="c660d-104">JavaScript 삽입 공격 방지(C#)</span><span class="sxs-lookup"><span data-stu-id="c660d-104">Preventing JavaScript Injection Attacks (C#)</span></span>

<span data-ttu-id="c660d-105">[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="c660d-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

[<span data-ttu-id="c660d-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="c660d-106">Download PDF</span></span>](https://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_06_CS.pdf)

> <span data-ttu-id="c660d-107">JavaScript 삽입 공격 및 사이트 간 스크립팅 공격이 발생 하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-107">Prevent JavaScript Injection Attacks and Cross-Site Scripting Attacks from happening to you.</span></span> <span data-ttu-id="c660d-108">이 자습서에서 Stephen Walther는 콘텐츠를 HTML 인코딩하여 이러한 유형의 공격을 쉽게 방지할 수 있는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-108">In this tutorial, Stephen Walther explains how you can easily defeat these types of attacks by HTML encoding your content.</span></span>

<span data-ttu-id="c660d-109">이 자습서의 목표는 ASP.NET MVC 응용 프로그램에서 JavaScript 삽입 공격을 방지 하는 방법을 설명 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-109">The goal of this tutorial is to explain how you can prevent JavaScript injection attacks in your ASP.NET MVC applications.</span></span> <span data-ttu-id="c660d-110">이 자습서에서는 JavaScript 삽입 공격 으로부터 웹 사이트를 방어 하는 두 가지 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-110">This tutorial discusses two approaches to defending your website against a JavaScript injection attack.</span></span> <span data-ttu-id="c660d-111">표시 되는 데이터를 인코딩하여 JavaScript 삽입 공격을 방지 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-111">You learn how to prevent JavaScript injection attacks by encoding the data that you display.</span></span> <span data-ttu-id="c660d-112">또한 사용자가 수락한 데이터를 인코딩하여 JavaScript 삽입 공격을 방지 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-112">You also learn how to prevent JavaScript injection attacks by encoding the data that you accept.</span></span>

## <a name="what-is-a-javascript-injection-attack"></a><span data-ttu-id="c660d-113">JavaScript 삽입 공격 이란?</span><span class="sxs-lookup"><span data-stu-id="c660d-113">What is a JavaScript Injection Attack?</span></span>

<span data-ttu-id="c660d-114">사용자 입력을 수락 하 고 사용자 입력을 다시 표시할 때마다 JavaScript 삽입 공격에 대해 웹 사이트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-114">Whenever you accept user input and redisplay the user input, you open your website to JavaScript injection attacks.</span></span> <span data-ttu-id="c660d-115">JavaScript 삽입 공격에 공개 된 구체적인 응용 프로그램을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-115">Let's examine a concrete application that is open to JavaScript injection attacks.</span></span>

<span data-ttu-id="c660d-116">사용자 의견 웹 사이트를 만들었다고 가정 합니다 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="c660d-116">Imagine that you have created a customer feedback website (see Figure 1).</span></span> <span data-ttu-id="c660d-117">고객은 웹 사이트를 방문 하 여 제품 사용 경험에 대 한 피드백을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-117">Customers can visit the website and enter feedback on their experience using your products.</span></span> <span data-ttu-id="c660d-118">고객이 피드백을 제출 하면 피드백 페이지에 피드백이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-118">When a customer submits their feedback, the feedback is redisplayed on the feedback page.</span></span>

<span data-ttu-id="c660d-119">[사용자 의견 웹 사이트 ![](preventing-javascript-injection-attacks-cs/_static/image2.png)](preventing-javascript-injection-attacks-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c660d-119">[![Customer Feedback Website](preventing-javascript-injection-attacks-cs/_static/image2.png)](preventing-javascript-injection-attacks-cs/_static/image1.png)</span></span>

<span data-ttu-id="c660d-120">**그림 01**: 사용자 의견 웹 사이트 ([전체 크기 이미지를 보려면 클릭](preventing-javascript-injection-attacks-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="c660d-120">**Figure 01**: Customer Feedback Website ([Click to view full-size image](preventing-javascript-injection-attacks-cs/_static/image3.png))</span></span>

<span data-ttu-id="c660d-121">사용자 의견 웹 사이트는 목록 1에 `controller`를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-121">The customer feedback website uses the `controller` in Listing 1.</span></span> <span data-ttu-id="c660d-122">이 `controller`에는 `Index()` 및 `Create()`라는 두 개의 작업이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-122">This `controller` contains two actions named `Index()` and `Create()`.</span></span>

<span data-ttu-id="c660d-123">**목록 1 – `HomeController.cs`**</span><span class="sxs-lookup"><span data-stu-id="c660d-123">**Listing 1 – `HomeController.cs`**</span></span>

[!code-csharp[Main](preventing-javascript-injection-attacks-cs/samples/sample1.cs)]

<span data-ttu-id="c660d-124">`Index()` 메서드는 `Index` 뷰를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-124">The `Index()` method displays the `Index` view.</span></span> <span data-ttu-id="c660d-125">이 메서드는 LINQ to SQL 쿼리를 사용 하 여 데이터베이스에서 피드백을 검색 하 여 모든 이전 사용자 의견을 `Index` 보기에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-125">This method passes all of the previous customer feedback to the `Index` view by retrieving the feedback from the database (using a LINQ to SQL query).</span></span>

<span data-ttu-id="c660d-126">`Create()` 메서드는 새 피드백 항목을 만들어 데이터베이스에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-126">The `Create()` method creates a new Feedback item and adds it to the database.</span></span> <span data-ttu-id="c660d-127">고객이 양식에 입력 하는 메시지는 메시지 매개 변수에서 `Create()` 메서드에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-127">The message that the customer enters in the form is passed to the `Create()` method in the message parameter.</span></span> <span data-ttu-id="c660d-128">피드백 항목이 만들어지고 메시지가 피드백 항목의 `Message` 속성에 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-128">A Feedback item is created and the message is assigned to the Feedback item's `Message` property.</span></span> <span data-ttu-id="c660d-129">사용자 의견 항목이 `DataContext.SubmitChanges()` 메서드 호출로 데이터베이스에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-129">The Feedback item is submitted to the database with the `DataContext.SubmitChanges()` method call.</span></span> <span data-ttu-id="c660d-130">마지막으로 방문자는 모든 피드백이 표시 되는 `Index` 보기로 다시 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-130">Finally, the visitor is redirected back to the `Index` view where all of the feedback is displayed.</span></span>

<span data-ttu-id="c660d-131">`Index` 보기는 목록 2에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-131">The `Index` view is contained in Listing 2.</span></span>

<span data-ttu-id="c660d-132">**목록 2 – `Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="c660d-132">**Listing 2 – `Index.aspx`**</span></span>

[!code-aspx[Main](preventing-javascript-injection-attacks-cs/samples/sample2.aspx)]

<span data-ttu-id="c660d-133">`Index` 보기에는 두 개의 섹션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-133">The `Index` view has two sections.</span></span> <span data-ttu-id="c660d-134">위쪽 섹션에는 실제 사용자 의견 양식이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-134">The top section contains the actual customer feedback form.</span></span> <span data-ttu-id="c660d-135">아래쪽 섹션에는에 대 한이 포함 되어 있습니다. 모든 이전 사용자 의견 항목을 반복 하 고 각 피드백 항목의 EntryDate 및 Message 속성을 표시 하는 각 루프</span><span class="sxs-lookup"><span data-stu-id="c660d-135">The bottom section contains a For..Each loop that loops through all of the previous customer feedback items and displays the EntryDate and Message properties for each feedback item.</span></span>

<span data-ttu-id="c660d-136">사용자 의견 웹 사이트는 간단한 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-136">The customer feedback website is a simple website.</span></span> <span data-ttu-id="c660d-137">불행 하 게도 웹 사이트는 JavaScript 삽입 공격에 공개 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-137">Unfortunately, the website is open to JavaScript injection attacks.</span></span>

<span data-ttu-id="c660d-138">사용자 의견 양식에 다음 텍스트를 입력 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-138">Imagine that you enter the following text into the customer feedback form:</span></span>

[!code-html[Main](preventing-javascript-injection-attacks-cs/samples/sample3.html)]

<span data-ttu-id="c660d-139">이 텍스트는 경고 메시지 상자를 표시 하는 JavaScript 스크립트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-139">This text represents a JavaScript script that displays an alert message box.</span></span> <span data-ttu-id="c660d-140">사용자가이 스크립트를 사용자 의견 양식에 제출한 후 메시지는 <em>Boo!</em> 나중에 누구나 고객 피드백 웹 사이트를 방문할 때마다 표시 됩니다 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="c660d-140">After someone submits this script into the feedback form, the message <em>Boo!</em>will appear whenever anyone visits the customer feedback website in the future (see Figure 2).</span></span>

<span data-ttu-id="c660d-141">[JavaScript 삽입 ![](preventing-javascript-injection-attacks-cs/_static/image5.png)](preventing-javascript-injection-attacks-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="c660d-141">[![JavaScript Injection](preventing-javascript-injection-attacks-cs/_static/image5.png)](preventing-javascript-injection-attacks-cs/_static/image4.png)</span></span>

<span data-ttu-id="c660d-142">**그림 02**: JavaScript 삽입 ([전체 크기 이미지를 보려면 클릭](preventing-javascript-injection-attacks-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="c660d-142">**Figure 02**: JavaScript Injection ([Click to view full-size image](preventing-javascript-injection-attacks-cs/_static/image6.png))</span></span>

<span data-ttu-id="c660d-143">이제 JavaScript 삽입 공격에 대 한 초기 응답이 apathy 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-143">Now, your initial response to JavaScript injection attacks might be apathy.</span></span> <span data-ttu-id="c660d-144">JavaScript 삽입 공격은 단순히 *파손* 공격의 유형 이라고 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-144">You might think that JavaScript injection attacks are simply a type of *defacement* attack.</span></span> <span data-ttu-id="c660d-145">JavaScript 삽입 공격을 커밋하여 어떤 것도 진정한 영향을 주지 않는 것으로 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-145">You might believe that no one can do anything truly evil by committing a JavaScript injection attack.</span></span>

<span data-ttu-id="c660d-146">불행 하 게도 해커는 JavaScript를 웹 사이트에 삽입 하 여 정말 나쁜 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-146">Unfortunately, a hacker can do some really, really evil things by injecting JavaScript into a website.</span></span> <span data-ttu-id="c660d-147">JavaScript 삽입 공격을 사용 하 여 XSS (사이트 간 스크립팅) 공격을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-147">You can use a JavaScript injection attack to perform a Cross-Site Scripting (XSS) attack.</span></span> <span data-ttu-id="c660d-148">사이트 간 스크립팅 공격에서는 기밀 사용자 정보를 도용 하 고 다른 웹 사이트로 정보를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-148">In a Cross-Site Scripting attack, you steal confidential user information and send the information to another website.</span></span>

<span data-ttu-id="c660d-149">예를 들어 해커가 JavaScript 삽입 공격을 사용 하 여 다른 사용자의 브라우저 쿠키 값을 도용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-149">For example, a hacker can use a JavaScript injection attack to steal the values of browser cookies from other users.</span></span> <span data-ttu-id="c660d-150">암호, 신용 카드 번호 또는 주민 등록 번호와 같은 중요 한 정보가 브라우저 쿠키에 저장 된 경우 해커가 JavaScript 삽입 공격을 사용 하 여이 정보를 도용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-150">If sensitive information -- such as passwords, credit card numbers, or social security numbers – is stored in the browser cookies, then a hacker can use a JavaScript injection attack to steal this information.</span></span> <span data-ttu-id="c660d-151">또는 JavaScript 공격으로 손상 된 페이지에 포함 된 양식 필드에 중요 한 정보를 입력 하는 경우 해커가 삽입 된 JavaScript를 사용 하 여 양식 데이터를 가져와서 다른 웹 사이트로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-151">Or, if a user enters sensitive information in a form field contained in a page that has been compromised with a JavaScript attack, then the hacker can use the injected JavaScript to grab the form data and send it to another website.</span></span>

<span data-ttu-id="c660d-152">*무서 워 하세요*.</span><span class="sxs-lookup"><span data-stu-id="c660d-152">*Please be scared*.</span></span> <span data-ttu-id="c660d-153">JavaScript 주입 공격을 심각 하 게 수행 하 고 사용자의 기밀 정보를 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-153">Take JavaScript injection attacks seriously and protect your user's confidential information.</span></span> <span data-ttu-id="c660d-154">다음 두 섹션에서는 JavaScript 삽입 공격 으로부터 ASP.NET MVC 응용 프로그램을 보호 하는 데 사용할 수 있는 두 가지 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-154">In the next two sections, we discuss two techniques that you can use to defend your ASP.NET MVC applications from JavaScript injection attacks.</span></span>

## <a name="approach-1-html-encode-in-the-view"></a><span data-ttu-id="c660d-155">#1 방식: 뷰에서 HTML 인코드</span><span class="sxs-lookup"><span data-stu-id="c660d-155">Approach #1: HTML Encode in the View</span></span>

<span data-ttu-id="c660d-156">JavaScript 삽입 공격을 방지 하는 한 가지 쉬운 방법은 뷰에서 데이터를 다시 표시할 때 웹 사이트 사용자가 입력 한 데이터를 HTML 인코딩하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-156">One easy method of preventing JavaScript injection attacks is to HTML encode any data entered by website users when you redisplay the data in a view.</span></span> <span data-ttu-id="c660d-157">목록 3의 업데이트 된 `Index` 보기는이 접근 방식을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-157">The updated `Index` view in Listing 3 follows this approach.</span></span>

<span data-ttu-id="c660d-158">**목록 3 – `Index.aspx` (HTML 인코딩)**</span><span class="sxs-lookup"><span data-stu-id="c660d-158">**Listing 3 – `Index.aspx` (HTML Encoded)**</span></span>

[!code-aspx[Main](preventing-javascript-injection-attacks-cs/samples/sample4.aspx)]

<span data-ttu-id="c660d-159">값이 다음 코드와 함께 표시 되기 전에 `feedback.Message` 값이 HTML로 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-159">Notice that the value of `feedback.Message` is HTML encoded before the value is displayed with the following code:</span></span>

[!code-aspx[Main](preventing-javascript-injection-attacks-cs/samples/sample5.aspx)]

<span data-ttu-id="c660d-160">HTML 인코딩 이란 무엇을 의미 하나요?</span><span class="sxs-lookup"><span data-stu-id="c660d-160">What does it mean to HTML encode a string?</span></span> <span data-ttu-id="c660d-161">문자열을 HTML로 인코딩하면 `<` 및 `>`와 같은 위험한 문자가 `&lt;` 및 `&gt;`같은 HTML 엔터티 참조로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-161">When you HTML encode a string, dangerous characters such as `<` and `>` are replaced by HTML entity references such as `&lt;` and `&gt;`.</span></span> <span data-ttu-id="c660d-162">따라서 `<script>alert("Boo!")</script>` 문자열을 HTML로 인코딩하면 `&lt;script&gt;alert(&quot;Boo!&quot;)&lt;/script&gt;`으로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-162">So when the string `<script>alert("Boo!")</script>` is HTML encoded, it gets converted to `&lt;script&gt;alert(&quot;Boo!&quot;)&lt;/script&gt;`.</span></span> <span data-ttu-id="c660d-163">인코딩된 문자열은 브라우저에서 해석 될 때 더 이상 JavaScript 스크립트로 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-163">The encoded string no longer executes as a JavaScript script when interpreted by a browser.</span></span> <span data-ttu-id="c660d-164">대신 그림 3의 무해 한 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-164">Instead, you get the harmless page in Figure 3.</span></span>

<span data-ttu-id="c660d-165">[![JavaScript 공격 공격](preventing-javascript-injection-attacks-cs/_static/image8.png)](preventing-javascript-injection-attacks-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="c660d-165">[![Defeated JavaScript Attack](preventing-javascript-injection-attacks-cs/_static/image8.png)](preventing-javascript-injection-attacks-cs/_static/image7.png)</span></span>

<span data-ttu-id="c660d-166">**그림 03**: JavaScript 공격 거부 ([전체 크기 이미지를 보려면 클릭](preventing-javascript-injection-attacks-cs/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="c660d-166">**Figure 03**: Defeated JavaScript Attack ([Click to view full-size image](preventing-javascript-injection-attacks-cs/_static/image9.png))</span></span>

<span data-ttu-id="c660d-167">목록 3의 `Index` 뷰에서는 `feedback.Message` 값만 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-167">Notice that in the `Index` view in Listing 3 only the value of `feedback.Message` is encoded.</span></span> <span data-ttu-id="c660d-168">`feedback.EntryDate`의 값은 인코딩되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-168">The value of `feedback.EntryDate` is not encoded.</span></span> <span data-ttu-id="c660d-169">사용자가 입력 한 데이터만 인코딩해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-169">You only need to encode data entered by a user.</span></span> <span data-ttu-id="c660d-170">EntryDate의 값이 컨트롤러에서 생성 되었기 때문에이 값을 HTML로 인코딩할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-170">Because the value of EntryDate was generated in the controller, you don't need to HTML encode this value.</span></span>

## <a name="approach-2-html-encode-in-the-controller"></a><span data-ttu-id="c660d-171">방법 #2: 컨트롤러에서 HTML 인코드</span><span class="sxs-lookup"><span data-stu-id="c660d-171">Approach #2: HTML Encode in the Controller</span></span>

<span data-ttu-id="c660d-172">데이터를 뷰에 표시할 때 HTML 인코딩 데이터 대신 데이터를 데이터베이스로 전송 하기 바로 전에 데이터를 HTML로 인코딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-172">Instead of HTML encoding data when you display the data in a view, you can HTML encode the data just before you submit the data to the database.</span></span> <span data-ttu-id="c660d-173">이 두 번째 방법은 목록 4의 `controller` 경우에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-173">This second approach is taken in the case of the `controller` in Listing 4.</span></span>

<span data-ttu-id="c660d-174">**목록 4 – `HomeController.cs` (HTML 인코딩)**</span><span class="sxs-lookup"><span data-stu-id="c660d-174">**Listing 4 – `HomeController.cs` (HTML Encoded)**</span></span>

[!code-csharp[Main](preventing-javascript-injection-attacks-cs/samples/sample6.cs)]

<span data-ttu-id="c660d-175">메시지의 값이 `Create()` 작업 내에서 데이터베이스로 전송 되기 전에 HTML로 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-175">Notice that the value of Message is HTML encoded before the value is submitted to the database within the `Create()` action.</span></span> <span data-ttu-id="c660d-176">메시지가 뷰에서 다시 표시 되 면 메시지는 HTML로 인코딩되고 메시지에 삽입 된 모든 JavaScript는 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-176">When the Message is redisplayed in the view, the Message is HTML encoded and any JavaScript injected in the Message is not executed.</span></span>

<span data-ttu-id="c660d-177">일반적으로이 자습서에서 설명 하는 첫 번째 방법에는이 두 번째 방법을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-177">Typically, you should favor the first approach discussed in this tutorial over this second approach.</span></span> <span data-ttu-id="c660d-178">이 두 번째 방법의 문제는 데이터베이스에서 HTML로 인코딩된 데이터를 종료 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-178">The problem with this second approach is that you end up with HTML encoded data in your database.</span></span> <span data-ttu-id="c660d-179">즉, 데이터베이스 데이터는 재미 있는 문자를 사용 하 여 변경 된 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-179">In other words, your database data is dirtied with funny looking characters.</span></span>

<span data-ttu-id="c660d-180">이것이 왜 바람직하지 않나요?</span><span class="sxs-lookup"><span data-stu-id="c660d-180">Why is this bad?</span></span> <span data-ttu-id="c660d-181">웹 페이지가 아닌 다른 항목에 데이터베이스 데이터를 표시 해야 하는 경우에는 문제가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-181">If you ever need to display the database data in something other than a web page, then you will have problems.</span></span> <span data-ttu-id="c660d-182">예를 들어 Windows Forms 응용 프로그램에서 더 이상 데이터를 더 이상 표시 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-182">For example, you can no longer easily display the data in a Windows Forms application.</span></span>

## <a name="summary"></a><span data-ttu-id="c660d-183">요약</span><span class="sxs-lookup"><span data-stu-id="c660d-183">Summary</span></span>

<span data-ttu-id="c660d-184">이 자습서의 목적은 JavaScript 삽입 공격의 잠재 고객을 부담 하는 것 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-184">The purpose of this tutorial was to scare you about the prospect of a JavaScript injection attack.</span></span> <span data-ttu-id="c660d-185">이 자습서에서는 JavaScript 삽입 공격 으로부터 ASP.NET MVC 응용 프로그램을 보호 하는 두 가지 방법에 대해 설명 했습니다. 뷰에서 사용자가 제출한 데이터를 HTML로 인코딩하거나 컨트롤러에서 사용자가 제출한 데이터를 HTML 인코딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c660d-185">This tutorial discussed two approaches for defending your ASP.NET MVC applications against JavaScript injection attacks: you can either HTML encode user submitted data in the view or you can HTML encode user submitted data in the controller.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c660d-186">[이전](authenticating-users-with-windows-authentication-cs.md)
> [다음](authenticating-users-with-forms-authentication-vb.md)</span><span class="sxs-lookup"><span data-stu-id="c660d-186">[Previous](authenticating-users-with-windows-authentication-cs.md)
[Next](authenticating-users-with-forms-authentication-vb.md)</span></span>
