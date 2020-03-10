---
uid: mvc/overview/older-versions-1/models-data/performing-simple-validation-vb
title: 간단한 유효성 검사 수행 (VB) | Microsoft Docs
author: StephenWalther
description: ASP.NET MVC 응용 프로그램에서 유효성 검사를 수행 하는 방법에 대해 알아봅니다. 이 자습서에서 Stephen Walther는 모델 상태와 유효성 검사 HTML 도우미를 소개 합니다.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: df6cf4b7-0bb3-4c4e-b17a-bd78a759a6bc
msc.legacyurl: /mvc/overview/older-versions-1/models-data/performing-simple-validation-vb
msc.type: authoredcontent
ms.openlocfilehash: 46925f22b7dfc23f2bb89b8d2fff0cbd8ae49062
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78436667"
---
# <a name="performing-simple-validation-vb"></a><span data-ttu-id="f74a5-104">간단한 유효성 검사 수행(VB)</span><span class="sxs-lookup"><span data-stu-id="f74a5-104">Performing Simple Validation (VB)</span></span>

<span data-ttu-id="f74a5-105">[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="f74a5-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="f74a5-106">ASP.NET MVC 응용 프로그램에서 유효성 검사를 수행 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-106">Learn how to perform validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="f74a5-107">이 자습서에서 Stephen Walther는 모델 상태 및 유효성 검사 HTML 도우미를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-107">In this tutorial, Stephen Walther introduces you to model state and the validation HTML helpers.</span></span>

<span data-ttu-id="f74a5-108">이 자습서의 목표는 ASP.NET MVC 응용 프로그램 내에서 유효성 검사를 수행 하는 방법을 설명 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-108">The goal of this tutorial is to explain how you can perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="f74a5-109">예를 들어 사용자가 필수 필드에 대 한 값을 포함 하지 않는 양식을 전송 하지 못하도록 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-109">For example, you learn how to prevent someone from submitting a form that does not contain a value for a required field.</span></span> <span data-ttu-id="f74a5-110">모델 상태와 유효성 검사 HTML 도우미를 사용 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-110">You learn how to use model state and the validation HTML helpers.</span></span>

## <a name="understanding-model-state"></a><span data-ttu-id="f74a5-111">모델 상태 이해</span><span class="sxs-lookup"><span data-stu-id="f74a5-111">Understanding Model State</span></span>

<span data-ttu-id="f74a5-112">모델 상태 (모델 상태 사전)를 사용 하 여 유효성 검사 오류를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-112">You use model state - or more accurately, the model state dictionary - to represent validation errors.</span></span> <span data-ttu-id="f74a5-113">예를 들어 목록 1의 Create () 동작은 product 클래스를 데이터베이스에 추가 하기 전에 Product 클래스의 속성에 대 한 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-113">For example, the Create() action in Listing 1 validates the properties of a Product class before adding the Product class to a database.</span></span>

<span data-ttu-id="f74a5-114">컨트롤러에 유효성 검사 또는 데이터베이스 논리를 추가 하는 것을 권장 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-114">I'm not recommending that you add your validation or database logic to a controller.</span></span> <span data-ttu-id="f74a5-115">컨트롤러는 응용 프로그램 흐름 제어와 관련 된 논리를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-115">A controller should contain only logic related to application flow control.</span></span> <span data-ttu-id="f74a5-116">작업을 단순하게 유지 하기 위한 바로 가기를 작성 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-116">We are taking a shortcut to keep things simple.</span></span>

<span data-ttu-id="f74a5-117">**목록 1-Controller\entstomom.xml**</span><span class="sxs-lookup"><span data-stu-id="f74a5-117">**Listing 1 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](performing-simple-validation-vb/samples/sample1.vb)]

<span data-ttu-id="f74a5-118">목록 1에서 Product 클래스의 Name, Description 및 UnitsInStock 속성에 대 한 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-118">In Listing 1, the Name, Description, and UnitsInStock properties of the Product class are validated.</span></span> <span data-ttu-id="f74a5-119">이러한 속성 중 하나라도 유효성 검사 테스트에 실패 하면 모델 상태 사전 (컨트롤러 클래스의 ModelState 속성으로 표시 됨)에 오류가 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-119">If any of these properties fail a validation test then an error is added to the model state dictionary (represented by the ModelState property of the Controller class).</span></span>

<span data-ttu-id="f74a5-120">모델 상태에 오류가 있으면 ModelState. IsValid 속성은 false를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-120">If there are any errors in model state then the ModelState.IsValid property returns false.</span></span> <span data-ttu-id="f74a5-121">이 경우 새 제품을 만들기 위한 HTML 양식이 다시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-121">In that case, the HTML form for creating a new product is redisplayed.</span></span> <span data-ttu-id="f74a5-122">그렇지 않으면 유효성 검사 오류가 없는 경우 새 제품이 데이터베이스에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-122">Otherwise, if there are no validation errors, the new Product is added to the database.</span></span>

## <a name="using-the-validation-helpers"></a><span data-ttu-id="f74a5-123">유효성 검사 도우미 사용</span><span class="sxs-lookup"><span data-stu-id="f74a5-123">Using the Validation Helpers</span></span>

<span data-ttu-id="f74a5-124">ASP.NET MVC 프레임 워크에는 Html. ValidationMessage () 도우미와 ValidationSummary () 도우미 라는 두 가지 유효성 검사 도우미가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-124">The ASP.NET MVC framework includes two validation helpers: the Html.ValidationMessage() helper and the Html.ValidationSummary() helper.</span></span> <span data-ttu-id="f74a5-125">뷰에 이러한 두 도우미를 사용 하 여 유효성 검사 오류 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-125">You use these two helpers in a view to display validation error messages.</span></span>

<span data-ttu-id="f74a5-126">Html ValidationMessage () 및 ValidationSummary () 도우미는 ASP.NET MVC 스 캐 폴딩에 의해 자동으로 생성 되는 만들기 및 편집 뷰에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-126">The Html.ValidationMessage() and Html.ValidationSummary() helpers are used in the Create and Edit views that are generated automatically by the ASP.NET MVC scaffolding.</span></span> <span data-ttu-id="f74a5-127">Create view를 생성 하려면 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-127">Follow these steps to generate the Create view:</span></span>

1. <span data-ttu-id="f74a5-128">제품 컨트롤러에서 만들기 () 작업을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **보기 추가** 를 선택 합니다 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="f74a5-128">Right-click the Create() action in the Product controller and select the menu option **Add View** (see Figure 1).</span></span>
2. <span data-ttu-id="f74a5-129">**보기 추가** 대화 상자에서 **강력한 형식의 뷰 만들기** 확인란을 선택 합니다 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="f74a5-129">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view** (see Figure 2).</span></span>
3. <span data-ttu-id="f74a5-130">**데이터 클래스 보기** 드롭다운 목록에서 Product 클래스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-130">From the **View data class** dropdown list, select the Product class.</span></span>
4. <span data-ttu-id="f74a5-131">**콘텐츠 보기** 드롭다운 목록에서 만들기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-131">From the **View content** dropdown list, select Create.</span></span>
5. <span data-ttu-id="f74a5-132">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-132">Click the **Add** button.</span></span>

<span data-ttu-id="f74a5-133">뷰를 추가 하기 전에 응용 프로그램을 빌드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-133">Make sure that you build your application before adding a view.</span></span> <span data-ttu-id="f74a5-134">그렇지 않으면 클래스 목록이 **데이터 클래스 보기** 드롭다운 목록에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-134">Otherwise, the list of classes won't appear in the **View data class** dropdown list.</span></span>

<span data-ttu-id="f74a5-135">[새 프로젝트 대화 상자 ![](performing-simple-validation-vb/_static/image1.jpg)](performing-simple-validation-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f74a5-135">[![The New Project dialog box](performing-simple-validation-vb/_static/image1.jpg)](performing-simple-validation-vb/_static/image1.png)</span></span>

<span data-ttu-id="f74a5-136">**그림 01**: 보기 추가 ([전체 크기 이미지를 보려면 클릭](performing-simple-validation-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="f74a5-136">**Figure 01**: Adding a view([Click to view full-size image](performing-simple-validation-vb/_static/image2.png))</span></span>

<span data-ttu-id="f74a5-137">[새 프로젝트 대화 상자 ![](performing-simple-validation-vb/_static/image2.jpg)](performing-simple-validation-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="f74a5-137">[![The New Project dialog box](performing-simple-validation-vb/_static/image2.jpg)](performing-simple-validation-vb/_static/image3.png)</span></span>

<span data-ttu-id="f74a5-138">**그림 02**: 강력한 형식의 뷰 만들기 ([전체 크기 이미지를 보려면 클릭](performing-simple-validation-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="f74a5-138">**Figure 02**: Creating a strongly-typed view ([Click to view full-size image](performing-simple-validation-vb/_static/image4.png))</span></span>

<span data-ttu-id="f74a5-139">이러한 단계를 완료 한 후 목록 2에서 만들기 보기를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-139">After you complete these steps, you get the Create view in Listing 2.</span></span>

<span data-ttu-id="f74a5-140">**목록 2-Views\Product\Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="f74a5-140">**Listing 2 - Views\Product\Create.aspx**</span></span>

[!code-aspx[Main](performing-simple-validation-vb/samples/sample2.aspx)]

<span data-ttu-id="f74a5-141">목록 2에서는 html 양식 바로 위에 ValidationSummary () 도우미가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-141">In Listing 2, the Html.ValidationSummary() helper is called immediately above the HTML form.</span></span> <span data-ttu-id="f74a5-142">이 도우미는 유효성 검사 오류 메시지 목록을 표시 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-142">This helper is used to display a list of validation error messages.</span></span> <span data-ttu-id="f74a5-143">ValidationSummary () 도우미는 오류를 글머리 기호 목록으로 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-143">The Html.ValidationSummary() helper renders the errors in a bulleted list.</span></span>

<span data-ttu-id="f74a5-144">Html 양식 필드 옆에 Html. ValidationMessage () 도우미가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-144">The Html.ValidationMessage() helper is called next to each of the HTML form fields.</span></span> <span data-ttu-id="f74a5-145">이 도우미는 폼 필드 바로 옆에 오류 메시지를 표시 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-145">This helper is used to display an error message right next to a form field.</span></span> <span data-ttu-id="f74a5-146">목록 2의 경우 오류가 발생 하면 Html. ValidationMessage () 도우미에 별표가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-146">In the case of Listing 2, the Html.ValidationMessage() helper displays an asterisk when there is an error.</span></span>

<span data-ttu-id="f74a5-147">그림 3의 페이지는 양식이 누락 된 필드와 잘못 된 값으로 제출 될 때 유효성 검사 도우미에서 렌더링 하는 오류 메시지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-147">The page in Figure 3 illustrates the error messages rendered by the validation helpers when the form is submitted with missing fields and invalid values.</span></span>

<span data-ttu-id="f74a5-148">[새 프로젝트 대화 상자 ![](performing-simple-validation-vb/_static/image3.jpg)](performing-simple-validation-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="f74a5-148">[![The New Project dialog box](performing-simple-validation-vb/_static/image3.jpg)](performing-simple-validation-vb/_static/image5.png)</span></span>

<span data-ttu-id="f74a5-149">**그림 03**: 문제가 있는 생성 된 Create view ([전체 크기 이미지를 보려면 클릭](performing-simple-validation-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="f74a5-149">**Figure 03**: The Create view submitted with problems ([Click to view full-size image](performing-simple-validation-vb/_static/image6.png))</span></span>

<span data-ttu-id="f74a5-150">유효성 검사 오류가 있는 경우에도 HTML 입력 필드의 모양이 수정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-150">Notice that the appearance of the HTML input fields are also modified when there is a validation error.</span></span> <span data-ttu-id="f74a5-151">Html. textbox () 도우미는 Html. TextBox () 도우미에 의해 렌더링 된 속성과 관련 된 유효성 검사 오류가 있을 때 *class = "입력-오류"* 특성을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-151">The Html.TextBox() helper renders a *class="input-validation-error"* attribute when there is a validation error associated with the property rendered by the Html.TextBox() helper.</span></span>

<span data-ttu-id="f74a5-152">유효성 검사 오류의 모양을 제어 하는 데 사용 되는 세 가지 css 스타일 시트 클래스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-152">There are three cascading style sheet classes used to control the appearance of validation errors:</span></span>

- <span data-ttu-id="f74a5-153">입력-유효성 검사-오류-Html. TextBox () 도우미에 의해 렌더링 된 &lt;입력&gt; 태그에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-153">input-validation-error - Applied to the &lt;input&gt; tag rendered by Html.TextBox() helper.</span></span>
- <span data-ttu-id="f74a5-154">필드-유효성 검사-오류-Html. ValidationMessage () 도우미에 의해 렌더링 된 &lt;범위&gt; 태그에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-154">field-validation-error - Applied to the &lt;span&gt; tag rendered by the Html.ValidationMessage() helper.</span></span>
- <span data-ttu-id="f74a5-155">유효성 검사-요약-오류-ValidationSummary () 도우미에 의해 렌더링 된 &lt;ul&gt; 태그에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-155">validation-summary-errors - Applied to the &lt;ul&gt; tag rendered by the Html.ValidationSummary() helper.</span></span>

<span data-ttu-id="f74a5-156">이러한 css 스타일 시트 클래스를 수정할 수 있으므로 Content 폴더에 있는 사이트 .css 파일을 수정 하 여 유효성 검사 오류의 모양을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-156">You can modify these cascading style sheet classes, and therefore modify the appearance of the validation errors, by modifying the Site.css file located in the Content folder.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="f74a5-157">HtmlHelper 클래스는 유효성 검사 관련 CSS 클래스의 이름을 검색 하기 위한 읽기 전용 정적 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-157">The HtmlHelper class includes read-only static properties for retrieving the names of the validation related CSS classes.</span></span> <span data-ttu-id="f74a5-158">이러한 정적 속성의 이름은 ValidationInputCssClassName, ValidationFieldCssClassName 및 ValidationSummaryCssClassName입니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-158">These static properties are named ValidationInputCssClassName, ValidationFieldCssClassName, and ValidationSummaryCssClassName.</span></span>

## <a name="prebinding-validation-and-postbinding-validation"></a><span data-ttu-id="f74a5-159">Prebinding 유효성 검사 및 사후 바인딩 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="f74a5-159">Prebinding Validation and Postbinding Validation</span></span>

<span data-ttu-id="f74a5-160">제품을 만들기 위한 HTML 양식을 제출 하 고 price 필드에 대해 잘못 된 값을 입력 하 고 UnitsInStock 필드에 값을 입력 하지 않은 경우 그림 4에 표시 된 유효성 검사 메시지를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-160">If you submit the HTML form for creating a Product, and you enter an invalid value for the price field and no value for the UnitsInStock field, then you'll get the validation messages displayed in Figure 4.</span></span> <span data-ttu-id="f74a5-161">이러한 유효성 검사 오류 메시지는 어디에서 제공 되나요?</span><span class="sxs-lookup"><span data-stu-id="f74a5-161">Where do these validation error messages come from?</span></span>

<span data-ttu-id="f74a5-162">[새 프로젝트 대화 상자 ![](performing-simple-validation-vb/_static/image4.jpg)](performing-simple-validation-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="f74a5-162">[![The New Project dialog box](performing-simple-validation-vb/_static/image4.jpg)](performing-simple-validation-vb/_static/image7.png)</span></span>

<span data-ttu-id="f74a5-163">**그림 04**: 사전 바인딩 유효성 검사 오류 ([전체 크기 이미지를 보려면 클릭](performing-simple-validation-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="f74a5-163">**Figure 04**: Prebinding Validation Errors([Click to view full-size image](performing-simple-validation-vb/_static/image8.png))</span></span>

<span data-ttu-id="f74a5-164">실제로는 HTML 양식 필드가 클래스에 바인딩되고 폼 필드가 클래스에 바인딩된 후에 생성 된 유효성 검사 오류 메시지의 두 가지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-164">There are actually two types of validation error messages - those generated before the HTML form fields are bound to a class and those generated after the form fields are bound to the class.</span></span> <span data-ttu-id="f74a5-165">즉, prebinding 유효성 검사 오류와 postbinding 유효성 검사 오류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-165">In other words, there are prebinding validation errors and postbinding validation errors.</span></span>

<span data-ttu-id="f74a5-166">목록 1에서 제품 컨트롤러에 의해 노출 되는 만들기 () 작업은 Product 클래스의 인스턴스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-166">The Create() action exposed by the Product controller in Listing 1 accepts an instance of the Product class.</span></span> <span data-ttu-id="f74a5-167">Create 메서드의 시그니처는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-167">The signature of the Create method looks like this:</span></span>

[!code-vb[Main](performing-simple-validation-vb/samples/sample3.vb)]

<span data-ttu-id="f74a5-168">만들기 양식의 HTML 양식 필드 값은 모델 바인더 라는 항목에 따라 제품 Tocreate 클래스에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-168">The values of the HTML form fields from the Create form are bound to the productToCreate class by something called a model binder.</span></span> <span data-ttu-id="f74a5-169">기본 모델 바인더는 양식 필드를 폼 속성에 바인딩할 수 없는 경우 자동으로 모델 상태에 오류 메시지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-169">The default model binder adds an error message to model state automatically when it cannot bind a form field to a form property.</span></span>

<span data-ttu-id="f74a5-170">기본 모델 바인더는 "apple" 문자열을 Product 클래스의 Price 속성에 바인딩할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-170">The default model binder cannot bind the string "apple" to the Price property of the Product class.</span></span> <span data-ttu-id="f74a5-171">Decimal 속성에는 문자열을 할당할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-171">You can't assign a string to a decimal property.</span></span> <span data-ttu-id="f74a5-172">따라서 모델 바인더는 모델 상태에 오류를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-172">Therefore, the model binder adds an error to model state.</span></span>

<span data-ttu-id="f74a5-173">또한 기본 모델 바인더는 nothing 값을 허용 하지 않는 속성에 Nothing 값을 할당할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-173">The default model binder also cannot assign the value Nothing to a property that does not accept the value Nothing.</span></span> <span data-ttu-id="f74a5-174">특히 모델 바인더는 UnitsInStock 속성에 Nothing 값을 할당할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-174">In particular, the model binder cannot assign the value Nothing to the UnitsInStock property.</span></span> <span data-ttu-id="f74a5-175">다시 한 번 모델 바인더는이를 제공 하 고 모델 상태에 오류 메시지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-175">Once again, the model binder gives up and adds an error message to model state.</span></span>

<span data-ttu-id="f74a5-176">이러한 prebinding 오류 메시지의 모양을 사용자 지정 하려면 이러한 메시지에 대 한 리소스 문자열을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-176">If you want to customize the appearance of these prebinding error messages then you need to create resource strings for these messages.</span></span>

## <a name="summary"></a><span data-ttu-id="f74a5-177">요약</span><span class="sxs-lookup"><span data-stu-id="f74a5-177">Summary</span></span>

<span data-ttu-id="f74a5-178">이 자습서의 목표는 ASP.NET MVC 프레임 워크에서 유효성 검사의 기본 메커니즘을 설명 하는 것 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-178">The goal of this tutorial was to describe the basic mechanics of validation in the ASP.NET MVC framework.</span></span> <span data-ttu-id="f74a5-179">모델 상태와 유효성 검사 HTML 도우미를 사용 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-179">You learned how to use model state and the validation HTML helpers.</span></span> <span data-ttu-id="f74a5-180">또한 prebinding과 postbinding 유효성 검사의 차이점에 대해 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-180">We also discussed the distinction between prebinding and postbinding validation.</span></span> <span data-ttu-id="f74a5-181">다른 자습서에서는 컨트롤러 및 모델 클래스에서 유효성 검사 코드를 이동 하는 다양 한 전략에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f74a5-181">In other tutorials, we'll discuss various strategies for moving your validation code out of your controllers and into your model classes.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f74a5-182">[이전](displaying-a-table-of-database-data-vb.md)
> [다음](validating-with-the-idataerrorinfo-interface-vb.md)</span><span class="sxs-lookup"><span data-stu-id="f74a5-182">[Previous](displaying-a-table-of-database-data-vb.md)
[Next](validating-with-the-idataerrorinfo-interface-vb.md)</span></span>
