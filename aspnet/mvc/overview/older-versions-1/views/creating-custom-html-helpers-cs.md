---
uid: aspnet/mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: 사용자 지정 HTML 도우미 만들기C#() | Microsoft Docs
author: microsoft
description: 이 자습서의 목표는 MVC 뷰 내에서 사용할 수 있는 사용자 지정 HTML 도우미를 만들 수 있는 방법을 보여 주는 것입니다. HTML 도우미를 활용 하 여 ...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 264ff9850bad397826b45649d52fbfefafc53a01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485789"
---
# <a name="creating-custom-html-helpers-c"></a><span data-ttu-id="4e1e6-104">사용자 지정 HTML 도우미 만들기(C#)</span><span class="sxs-lookup"><span data-stu-id="4e1e6-104">Creating Custom HTML Helpers (C#)</span></span>

<span data-ttu-id="4e1e6-105">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="4e1e6-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="4e1e6-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="4e1e6-106">Download PDF</span></span>](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> <span data-ttu-id="4e1e6-107">이 자습서의 목표는 MVC 뷰 내에서 사용할 수 있는 사용자 지정 HTML 도우미를 만들 수 있는 방법을 보여 주는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-107">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="4e1e6-108">HTML 도우미를 활용 하면 표준 HTML 페이지를 만들기 위해 수행 해야 하는 HTML 태그의 번거로운 입력 크기를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-108">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="4e1e6-109">이 자습서의 목표는 MVC 뷰 내에서 사용할 수 있는 사용자 지정 HTML 도우미를 만들 수 있는 방법을 보여 주는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-109">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="4e1e6-110">HTML 도우미를 활용 하면 표준 HTML 페이지를 만들기 위해 수행 해야 하는 HTML 태그의 번거로운 입력 크기를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-110">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="4e1e6-111">이 자습서의 첫 번째 부분에서는 ASP.NET MVC 프레임 워크에 포함 된 기존 HTML 도우미 중 일부를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-111">In the first part of this tutorial, I describe some of the existing HTML Helpers included with the ASP.NET MVC framework.</span></span> <span data-ttu-id="4e1e6-112">다음으로, 사용자 지정 HTML 도우미를 만드는 두 가지 방법에 대해 설명 합니다. 정적 메서드를 만들고 확장 메서드를 만들어 사용자 지정 HTML 도우미를 만드는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-112">Next, I describe two methods of creating custom HTML Helpers: I explain how to create custom HTML Helpers by creating a static method and by creating an extension method.</span></span>

## <a name="understanding-html-helpers"></a><span data-ttu-id="4e1e6-113">HTML 도우미 이해</span><span class="sxs-lookup"><span data-stu-id="4e1e6-113">Understanding HTML Helpers</span></span>

<span data-ttu-id="4e1e6-114">HTML 도우미는 문자열을 반환 하는 메서드 일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-114">An HTML Helper is just a method that returns a string.</span></span> <span data-ttu-id="4e1e6-115">문자열은 원하는 모든 형식의 콘텐츠를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-115">The string can represent any type of content that you want.</span></span> <span data-ttu-id="4e1e6-116">예를 들어 html 도우미를 사용 하 여 HTML `<input>` 및 `<img>` 태그와 같은 표준 HTML 태그를 렌더링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-116">For example, you can use HTML Helpers to render standard HTML tags like HTML `<input>` and `<img>` tags.</span></span> <span data-ttu-id="4e1e6-117">HTML 도우미를 사용 하 여 탭 스트립 또는 데이터베이스 데이터의 HTML 테이블과 같은 보다 복잡 한 콘텐츠를 렌더링할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-117">You also can use HTML Helpers to render more complex content such as a tab strip or an HTML table of database data.</span></span>

<span data-ttu-id="4e1e6-118">ASP.NET MVC 프레임 워크에는 다음과 같은 표준 HTML 도우미 집합이 포함 되어 있습니다 (완전 한 목록이 아님).</span><span class="sxs-lookup"><span data-stu-id="4e1e6-118">The ASP.NET MVC framework includes the following set of standard HTML Helpers (this is not a complete list):</span></span>

- <span data-ttu-id="4e1e6-119">Html.ActionLink()</span><span class="sxs-lookup"><span data-stu-id="4e1e6-119">Html.ActionLink()</span></span>
- <span data-ttu-id="4e1e6-120">Html.BeginForm()</span><span class="sxs-lookup"><span data-stu-id="4e1e6-120">Html.BeginForm()</span></span>
- <span data-ttu-id="4e1e6-121">Html.CheckBox()</span><span class="sxs-lookup"><span data-stu-id="4e1e6-121">Html.CheckBox()</span></span>
- <span data-ttu-id="4e1e6-122">Html.DropDownList()</span><span class="sxs-lookup"><span data-stu-id="4e1e6-122">Html.DropDownList()</span></span>
- <span data-ttu-id="4e1e6-123">Html.EndForm()</span><span class="sxs-lookup"><span data-stu-id="4e1e6-123">Html.EndForm()</span></span>
- <span data-ttu-id="4e1e6-124">Html.Hidden()</span><span class="sxs-lookup"><span data-stu-id="4e1e6-124">Html.Hidden()</span></span>
- <span data-ttu-id="4e1e6-125">Html.ListBox()</span><span class="sxs-lookup"><span data-stu-id="4e1e6-125">Html.ListBox()</span></span>
- <span data-ttu-id="4e1e6-126">Html.Password()</span><span class="sxs-lookup"><span data-stu-id="4e1e6-126">Html.Password()</span></span>
- <span data-ttu-id="4e1e6-127">Html.RadioButton()</span><span class="sxs-lookup"><span data-stu-id="4e1e6-127">Html.RadioButton()</span></span>
- <span data-ttu-id="4e1e6-128">Html.TextArea()</span><span class="sxs-lookup"><span data-stu-id="4e1e6-128">Html.TextArea()</span></span>
- <span data-ttu-id="4e1e6-129">Html.TextBox()</span><span class="sxs-lookup"><span data-stu-id="4e1e6-129">Html.TextBox()</span></span>

<span data-ttu-id="4e1e6-130">예를 들어 목록 1의 양식을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-130">For example, consider the form in Listing 1.</span></span> <span data-ttu-id="4e1e6-131">이 폼은 두 가지 표준 HTML 도우미의 도움으로 렌더링 됩니다 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="4e1e6-131">This form is rendered with the help of two of the standard HTML Helpers (see Figure 1).</span></span> <span data-ttu-id="4e1e6-132">이 폼에서는 `Html.BeginForm()` 및 `Html.TextBox()` 도우미 메서드를 사용 하 여 간단한 HTML 폼을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-132">This form uses the `Html.BeginForm()` and `Html.TextBox()` Helper methods to render a simple HTML form.</span></span>

<span data-ttu-id="4e1e6-133">[HTML 도우미를 사용 하 여 렌더링 된 ![페이지](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4e1e6-133">[![Page rendered with HTML Helpers](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span></span>

<span data-ttu-id="4e1e6-134">**그림 01**: HTML 도우미를 사용 하 여 렌더링 된 페이지 ([전체 크기 이미지를 보려면 클릭](creating-custom-html-helpers-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="4e1e6-134">**Figure 01**: Page rendered with HTML Helpers ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image3.png))</span></span>

<span data-ttu-id="4e1e6-135">**목록 1 – `Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="4e1e6-135">**Listing 1 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

<span data-ttu-id="4e1e6-136">Html.beginform () 도우미 메서드는 여는 태그와 닫는 HTML `<form>` 태그를 만드는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-136">The Html.BeginForm() Helper method is used to create the opening and closing HTML `<form>` tags.</span></span> <span data-ttu-id="4e1e6-137">`Html.BeginForm()` 메서드는 using 문 내에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-137">Notice that the `Html.BeginForm()` method is called within a using statement.</span></span> <span data-ttu-id="4e1e6-138">Using 문은 `<form>` 태그가 using 블록의 끝에서 닫히도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-138">The using statement ensures that the `<form>` tag gets closed at the end of the using block.</span></span>

<span data-ttu-id="4e1e6-139">Using 블록을 만드는 대신 Html. EndForm () 도우미 메서드를 호출 하 여 `<form>` 태그를 닫을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-139">If you prefer, instead of creating a using block, you can call the Html.EndForm() Helper method to close the `<form>` tag.</span></span> <span data-ttu-id="4e1e6-140">가장 직관적으로 보이는 여는 태그와 닫는 `<form>` 태그를 만드는 방법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-140">Use whichever approach to creating an opening and closing `<form>` tag that seems most intuitive to you.</span></span>

<span data-ttu-id="4e1e6-141">`Html.TextBox()` 도우미 메서드는 목록 1에서 HTML `<input>` 태그를 렌더링 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-141">The `Html.TextBox()` Helper methods are used in Listing 1 to render HTML `<input>` tags.</span></span> <span data-ttu-id="4e1e6-142">브라우저에서 소스 보기를 선택 하면 목록 2에 HTML 소스가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-142">If you select view source in your browser then you see the HTML source in Listing 2.</span></span> <span data-ttu-id="4e1e6-143">원본에는 표준 HTML 태그가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-143">Notice that the source contains standard HTML tags.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4e1e6-144">`Html.TextBox()`HTML 도우미는 `<% %>` 태그 대신 `<%= %>` 태그로 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-144">notice that the `Html.TextBox()`-HTML Helper is rendered with `<%= %>` tags instead of `<% %>` tags.</span></span> <span data-ttu-id="4e1e6-145">등호를 포함 하지 않으면 브라우저에 아무것도 렌더링 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-145">If you don't include the equal sign, then nothing gets rendered to the browser.</span></span>

<span data-ttu-id="4e1e6-146">ASP.NET MVC 프레임 워크에는 작은 도우미 집합이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-146">The ASP.NET MVC framework contains a small set of helpers.</span></span> <span data-ttu-id="4e1e6-147">사용자 지정 HTML 도우미를 사용 하 여 MVC 프레임 워크를 확장 해야 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-147">Most likely, you will need to extend the MVC framework with custom HTML Helpers.</span></span> <span data-ttu-id="4e1e6-148">이 자습서의 나머지 부분에서는 사용자 지정 HTML 도우미를 만드는 두 가지 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-148">In the remainder of this tutorial, you learn two methods of creating custom HTML Helpers.</span></span>

<span data-ttu-id="4e1e6-149">**목록 2 – `Index.aspx Source`**</span><span class="sxs-lookup"><span data-stu-id="4e1e6-149">**Listing 2 – `Index.aspx Source`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a><span data-ttu-id="4e1e6-150">정적 메서드를 사용 하 여 HTML 도우미 만들기</span><span class="sxs-lookup"><span data-stu-id="4e1e6-150">Creating HTML Helpers with Static Methods</span></span>

<span data-ttu-id="4e1e6-151">새 HTML 도우미를 만드는 가장 쉬운 방법은 문자열을 반환 하는 정적 메서드를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-151">The easiest way to create a new HTML Helper is to create a static method that returns a string.</span></span> <span data-ttu-id="4e1e6-152">예를 들어 HTML `<label>` 태그를 렌더링 하는 새 HTML 도우미를 만들도록 결정 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-152">Imagine, for example, that you decide to create a new HTML Helper that renders an HTML `<label>` tag.</span></span> <span data-ttu-id="4e1e6-153">목록 2에서 클래스를 사용 하 여 `<label>`를 렌더링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-153">You can use the class in Listing 2 to render a `<label>` .</span></span>

<span data-ttu-id="4e1e6-154">**목록 2 – `Helpers\LabelHelper.cs`**</span><span class="sxs-lookup"><span data-stu-id="4e1e6-154">**Listing 2 – `Helpers\LabelHelper.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

<span data-ttu-id="4e1e6-155">목록 2의 클래스에 대 한 특별 한 사항은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-155">There is nothing special about the class in Listing 2.</span></span> <span data-ttu-id="4e1e6-156">`Label()` 메서드는 단순히 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-156">The `Label()` method simply returns a string.</span></span>

<span data-ttu-id="4e1e6-157">목록 3의 수정 된 인덱스 뷰는 `LabelHelper`을 사용 하 여 HTML `<label>` 태그를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-157">The modified Index view in Listing 3 uses the `LabelHelper` to render HTML `<label>` tags.</span></span> <span data-ttu-id="4e1e6-158">뷰에는 `Application1.Helpers` 네임 스페이스를 가져오는 `<%@ imports %>` 지시문이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-158">Notice that the view includes an `<%@ imports %>` directive that imports the `Application1.Helpers` namespace.</span></span>

<span data-ttu-id="4e1e6-159">**목록 2 – `Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="4e1e6-159">**Listing 2 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a><span data-ttu-id="4e1e6-160">확장 메서드를 사용 하 여 HTML 도우미 만들기</span><span class="sxs-lookup"><span data-stu-id="4e1e6-160">Creating HTML Helpers with Extension Methods</span></span>

<span data-ttu-id="4e1e6-161">ASP.NET MVC 프레임 워크에 포함 된 표준 HTML 도우미와 같은 방식으로 작동 하는 HTML 도우미를 만들려는 경우에는 확장 메서드를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-161">If you want to create HTML Helpers that work just like the standard HTML Helpers included in the ASP.NET MVC framework then you need to create extension methods.</span></span> <span data-ttu-id="4e1e6-162">확장 메서드를 사용 하 여 기존 클래스에 새 메서드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-162">Extension methods enable you to add new methods to an existing class.</span></span> <span data-ttu-id="4e1e6-163">HTML 도우미 메서드를 만들 때 뷰의 Html 속성이 나타내는 HtmlHelper 클래스에 새 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-163">When creating an HTML Helper method, you add new methods to the HtmlHelper class represented by a view's Html property.</span></span>

<span data-ttu-id="4e1e6-164">목록 3의 클래스는 `Label()`이라는 `HtmlHelper` 클래스에 확장 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-164">The class in Listing 3 adds an extension method to the `HtmlHelper` class named `Label()`.</span></span> <span data-ttu-id="4e1e6-165">이 클래스에 대해 몇 가지 주의 해야 할 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-165">There are a couple of things that you should notice about this class.</span></span> <span data-ttu-id="4e1e6-166">먼저 클래스가 정적 클래스 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-166">First, notice that the class is a static class.</span></span> <span data-ttu-id="4e1e6-167">정적 클래스를 사용 하 여 확장 메서드를 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-167">You must define an extension method with a static class.</span></span>

<span data-ttu-id="4e1e6-168">둘째, `Label()` 메서드의 첫 번째 매개 변수가 `this`키워드 앞에와 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-168">Second, notice that the first parameter of the `Label()` method is preceded by the keyword `this`.</span></span> <span data-ttu-id="4e1e6-169">확장 메서드의 첫 번째 매개 변수는 확장 메서드가 확장 하는 클래스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-169">The first parameter of an extension method indicates the class that the extension method extends.</span></span>

<span data-ttu-id="4e1e6-170">**목록 3 – `Helpers\LabelExtensions.cs`**</span><span class="sxs-lookup"><span data-stu-id="4e1e6-170">**Listing 3 – `Helpers\LabelExtensions.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

<span data-ttu-id="4e1e6-171">확장 메서드를 만들고 응용 프로그램을 성공적으로 빌드한 후에는 Visual Studio Intellisense에 클래스의 다른 모든 메서드와 같은 확장 메서드가 표시 됩니다 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="4e1e6-171">After you create an extension method, and build your application successfully, the extension method appears in Visual Studio Intellisense like all of the other methods of a class (see Figure 2).</span></span> <span data-ttu-id="4e1e6-172">유일한 차이점은 확장 메서드가 해당 기호 옆에 특수 기호 (아래쪽 화살표 아이콘)와 함께 표시 된다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-172">The only difference is that extension methods appear with a special symbol next to them (an icon of a downward arrow).</span></span>

<span data-ttu-id="4e1e6-173">[Html. Label () 확장 메서드를 사용 하 여 ![](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="4e1e6-173">[![Using the Html.Label() extension method](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span></span>

<span data-ttu-id="4e1e6-174">**그림 02**: Html. Label () 확장 메서드 사용 ([전체 크기 이미지를 보려면 클릭](creating-custom-html-helpers-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="4e1e6-174">**Figure 02**: Using the Html.Label() extension method  ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image6.png))</span></span>

<span data-ttu-id="4e1e6-175">목록 4의 수정 된 인덱스 뷰는 Html. Label () 확장 메서드를 사용 하 여 모든 `<label>` 태그를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-175">The modified Index view in Listing 4 uses the Html.Label() extension method to render all of its `<label>` tags.</span></span>

<span data-ttu-id="4e1e6-176">**목록 4 – `Views\Home\Index3.aspx`**</span><span class="sxs-lookup"><span data-stu-id="4e1e6-176">**Listing 4 – `Views\Home\Index3.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a><span data-ttu-id="4e1e6-177">요약</span><span class="sxs-lookup"><span data-stu-id="4e1e6-177">Summary</span></span>

<span data-ttu-id="4e1e6-178">이 자습서에서는 사용자 지정 HTML 도우미를 만드는 두 가지 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-178">In this tutorial, you learned two methods of creating custom HTML Helpers.</span></span> <span data-ttu-id="4e1e6-179">먼저 문자열을 반환 하는 정적 메서드를 만들어 사용자 지정 `Label()` HTML 도우미를 만드는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-179">First, you learned how to create a custom `Label()` HTML Helper by creating a static method that returns a string.</span></span> <span data-ttu-id="4e1e6-180">다음으로 `HtmlHelper` 클래스에서 확장 메서드를 만들어 사용자 지정 `Label()` HTML 도우미 메서드를 만드는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-180">Next, you learned how to create a custom `Label()` HTML Helper method by creating an extension method on the `HtmlHelper` class.</span></span>

<span data-ttu-id="4e1e6-181">이 자습서에서는 매우 간단한 HTML 도우미 메서드를 작성 하는 데 초점을 두었습니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-181">In this tutorial, I focused on building an extremely simple HTML Helper method.</span></span> <span data-ttu-id="4e1e6-182">HTML 도우미는 원하는 대로 복잡할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-182">Realize that an HTML Helper can be as complicated as you want.</span></span> <span data-ttu-id="4e1e6-183">트리 뷰, 메뉴 또는 데이터베이스 데이터의 테이블과 같은 다양 한 콘텐츠를 렌더링 하는 HTML 도우미를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-183">You can build HTML Helpers that render rich content such as tree views, menus, or tables of database data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4e1e6-184">[이전](asp-net-mvc-views-overview-cs.md)
> [다음](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span><span class="sxs-lookup"><span data-stu-id="4e1e6-184">[Previous](asp-net-mvc-views-overview-cs.md)
[Next](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span></span>
