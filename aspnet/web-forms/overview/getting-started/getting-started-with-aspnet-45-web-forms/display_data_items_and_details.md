---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
title: 데이터 항목 및 세부 정보 표시 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈는 ASP.NET 4.7 및 Microsoft Visual Studio 2017를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 보여줍니다.
ms.author: riande
ms.date: 1/04/2019
ms.assetid: 64a491a8-0ed6-4c2f-9c1c-412962eb6006
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
msc.type: authoredcontent
ms.openlocfilehash: 130c9ffd29df612dac5bb954830a2eb9b738aaf0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520811"
---
# <a name="display-data-items-and-details"></a><span data-ttu-id="8a348-103">데이터 항목 및 세부 정보 표시</span><span class="sxs-lookup"><span data-stu-id="8a348-103">Display data items and details</span></span>

<span data-ttu-id="8a348-104">[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="8a348-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

> <span data-ttu-id="8a348-105">이 자습서 시리즈에서는 ASP.NET 4.7 및 Microsoft Visual Studio 2017를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 구축 하는 기본 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-105">This tutorial series teaches you the basics of building an ASP.NET Web Forms application with ASP.NET 4.7 and Microsoft Visual Studio 2017.</span></span>

<span data-ttu-id="8a348-106">이 자습서에서는 ASP.NET Web Forms를 사용 하 여 데이터 항목 및 데이터 항목 정보를 표시 하 고 Code First Entity Framework 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-106">In this tutorial, you'll learn how to display data items and data item details with ASP.NET Web Forms and Entity Framework Code First.</span></span> <span data-ttu-id="8a348-107">이 자습서는 정문 장난감 스토어 자습서 시리즈의 일부로 이전 "UI 및 탐색" 자습서를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-107">This tutorial builds on the previous "UI and Navigation" tutorial as part of the Wingtip Toy Store tutorial series.</span></span> <span data-ttu-id="8a348-108">이 자습서를 완료 한 후에는 *ProductsList* 페이지의 제품 및 제품 *세부 정보 .aspx* 페이지에 대 한 제품 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-108">After completing this tutorial, you'll see products on the *ProductsList.aspx* page and a product's details on the *ProductDetails.aspx* page.</span></span>

## <a name="youll-learn-how-to"></a><span data-ttu-id="8a348-109">이 문서에서 배울 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-109">You'll learn how to:</span></span>

- <span data-ttu-id="8a348-110">데이터 컨트롤을 추가 하 여 데이터베이스의 제품 표시</span><span class="sxs-lookup"><span data-stu-id="8a348-110">Add a data control to display products from the database</span></span>
- <span data-ttu-id="8a348-111">선택한 데이터에 데이터 컨트롤 연결</span><span class="sxs-lookup"><span data-stu-id="8a348-111">Connect a data control to the selected data</span></span>
- <span data-ttu-id="8a348-112">데이터베이스의 제품 정보를 표시 하는 데이터 컨트롤 추가</span><span class="sxs-lookup"><span data-stu-id="8a348-112">Add a data control to display product details from the database</span></span>
- <span data-ttu-id="8a348-113">쿼리 문자열에서 값을 검색 하 고 해당 값을 사용 하 여 데이터베이스에서 검색 되는 데이터를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-113">Retrieve a value from the query string and use that value to limit the data that's retrieved from the database</span></span>

### <a name="features-introduced-in-this-tutorial"></a><span data-ttu-id="8a348-114">이 자습서에 도입 된 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-114">Features introduced in this tutorial:</span></span>

- <span data-ttu-id="8a348-115">모델 바인딩</span><span class="sxs-lookup"><span data-stu-id="8a348-115">Model binding</span></span>
- <span data-ttu-id="8a348-116">값 공급자</span><span class="sxs-lookup"><span data-stu-id="8a348-116">Value providers</span></span>

## <a name="add-a-data-control"></a><span data-ttu-id="8a348-117">데이터 컨트롤 추가</span><span class="sxs-lookup"><span data-stu-id="8a348-117">Add a data control</span></span>

<span data-ttu-id="8a348-118">몇 가지 다른 옵션을 사용 하 여 데이터를 서버 컨트롤에 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-118">You can use a few different options to bind data to a server control.</span></span> <span data-ttu-id="8a348-119">가장 일반적인 경우는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-119">The most common include:</span></span>

* <span data-ttu-id="8a348-120">데이터 소스 컨트롤 추가</span><span class="sxs-lookup"><span data-stu-id="8a348-120">Adding a data source control</span></span>
* <span data-ttu-id="8a348-121">코드를 직접 추가</span><span class="sxs-lookup"><span data-stu-id="8a348-121">Adding code by hand</span></span>
* <span data-ttu-id="8a348-122">모델 바인딩 사용</span><span class="sxs-lookup"><span data-stu-id="8a348-122">Using model binding</span></span>

### <a name="use-a-data-source-control-to-bind-data"></a><span data-ttu-id="8a348-123">데이터 소스 컨트롤을 사용 하 여 데이터 바인딩</span><span class="sxs-lookup"><span data-stu-id="8a348-123">Use a data source control to bind data</span></span>

<span data-ttu-id="8a348-124">데이터 소스 컨트롤을 추가 하면 데이터 소스 컨트롤을 데이터를 표시 하는 컨트롤에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-124">Adding a data source control allows you to link the data source control to the control that displays the data.</span></span> <span data-ttu-id="8a348-125">이 방법을 사용 하면 프로그래밍 방식으로 서버 쪽 컨트롤을 데이터 원본에 연결 하는 대신 선언적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-125">With this approach, you can declaratively,  rather than programmatically, connect server-side controls to data sources.</span></span>

### <a name="code-by-hand-to-bind-data"></a><span data-ttu-id="8a348-126">데이터를 바인딩하기 위한 코딩</span><span class="sxs-lookup"><span data-stu-id="8a348-126">Code by hand to bind data</span></span>

<span data-ttu-id="8a348-127">직접 코딩에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-127">Coding by hand involves:</span></span>

1. <span data-ttu-id="8a348-128">값 읽기</span><span class="sxs-lookup"><span data-stu-id="8a348-128">Reading a value</span></span>
2. <span data-ttu-id="8a348-129">Null 인지 확인</span><span class="sxs-lookup"><span data-stu-id="8a348-129">Checking if it's null</span></span>
3. <span data-ttu-id="8a348-130">적절 한 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="8a348-130">Converting it to an appropriate type</span></span>
4. <span data-ttu-id="8a348-131">변환 성공 확인 중</span><span class="sxs-lookup"><span data-stu-id="8a348-131">Checking conversion success</span></span>
5. <span data-ttu-id="8a348-132">쿼리에서 값 사용</span><span class="sxs-lookup"><span data-stu-id="8a348-132">Using the value in the query</span></span> 

<span data-ttu-id="8a348-133">이 방법을 사용 하면 데이터 액세스 논리를 완전히 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-133">This approach lets you have full control over your data-access logic.</span></span>

### <a name="use-model-binding-to-bind-data"></a><span data-ttu-id="8a348-134">모델 바인딩을 사용 하 여 데이터 바인딩</span><span class="sxs-lookup"><span data-stu-id="8a348-134">Use model binding to bind data</span></span>

<span data-ttu-id="8a348-135">모델 바인딩을 사용 하면 훨씬 더 작은 코드를 사용 하 여 결과를 바인딩하고 응용 프로그램 전체에서 기능을 재사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-135">Model binding lets you bind results with far less code and gives you the ability to reuse the functionality throughout your application.</span></span> <span data-ttu-id="8a348-136">풍부한 데이터 바인딩 프레임 워크를 제공 하는 동시에 코드 중심 데이터 액세스 논리를 사용 하는 작업을 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-136">It simplifies working with code-focused data-access logic while still providing a rich, data-binding framework.</span></span>

## <a name="display-products"></a><span data-ttu-id="8a348-137">제품 표시</span><span class="sxs-lookup"><span data-stu-id="8a348-137">Display products</span></span>

<span data-ttu-id="8a348-138">이 자습서에서는 모델 바인딩을 사용 하 여 데이터를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-138">In this tutorial, you'll use model binding to bind data.</span></span> <span data-ttu-id="8a348-139">모델 바인딩을 사용 하 여 데이터를 선택 하도록 데이터 컨트롤을 구성 하려면 컨트롤의 `SelectMethod` 속성을 페이지 코드의 메서드 이름으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-139">To configure a data control to use model binding to select data, you set the control's `SelectMethod` property to a method name in the page's code.</span></span> <span data-ttu-id="8a348-140">데이터 컨트롤은 페이지 수명 주기에서 적절 한 시간에 메서드를 호출 하 고 반환 된 데이터를 자동으로 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-140">The data control calls the method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="8a348-141">`DataBind` 메서드를 명시적으로 호출할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-141">There's no need to explicitly call the `DataBind` method.</span></span>

1. <span data-ttu-id="8a348-142">**솔루션 탐색기**에서 *ProductList*을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-142">In **Solution Explorer**, open *ProductList.aspx*.</span></span>
2. <span data-ttu-id="8a348-143">기존 태그를 다음 태그로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-143">Replace the existing markup with this markup:</span></span>   

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample1.aspx)]

<span data-ttu-id="8a348-144">이 코드는 `productList` 이라는 **ListView** 컨트롤을 사용 하 여 제품을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-144">This code uses a **ListView** control named `productList` to display products.</span></span>

[!code-aspx-csharp[Main](display_data_items_and_details/samples/sample2.aspx)]

<span data-ttu-id="8a348-145">템플릿과 스타일을 사용 하 여 **ListView** 컨트롤에서 데이터를 표시 하는 방법을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-145">With templates and styles, you define how the **ListView** control displays data.</span></span> <span data-ttu-id="8a348-146">반복 구조의 데이터에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-146">It's useful for data in any repeating structure.</span></span> <span data-ttu-id="8a348-147">이 **ListView** 예제는 단순히 데이터베이스 데이터를 표시 하지만, 코드를 사용 하지 않고도 사용자가 데이터를 편집, 삽입 및 삭제 하 고 데이터를 정렬 하 고 페이지를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-147">Though this **ListView** example simply displays database data, you can also, without code, enable users to edit, insert, and delete data, and to sort and page data.</span></span>

<span data-ttu-id="8a348-148">**ListView** 컨트롤에서 `ItemType` 속성을 설정 하 여 데이터 바인딩 식 `Item`를 사용할 수 있으며 컨트롤이 강력한 형식으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-148">By setting the `ItemType` property in the **ListView** control, the data-binding expression `Item` is available and the control becomes strongly typed.</span></span> <span data-ttu-id="8a348-149">이전 자습서에서 설명한 대로 IntelliSense를 사용 하 여 항목 개체 세부 정보를 선택할 수 있습니다 (예: `ProductName`지정).</span><span class="sxs-lookup"><span data-stu-id="8a348-149">As mentioned in the previous tutorial, you can select Item object details with IntelliSense, such as specifying the `ProductName`:</span></span>

![데이터 항목 및 세부 정보 표시-IntelliSense](display_data_items_and_details/_static/image1.png)

<span data-ttu-id="8a348-151">모델 바인딩을 사용 하 여 `SelectMethod` 값을 지정 하는 것도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-151">You're also using model binding to specify a `SelectMethod` value.</span></span> <span data-ttu-id="8a348-152">이 값 (`GetProducts`)은 다음 단계에서 제품을 표시 하기 위해 코드 숨김으로 추가 하는 방법에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-152">This value (`GetProducts`) corresponds to the method you'll add to the code behind to display products in the next step.</span></span>

### <a name="add-code-to-display-products"></a><span data-ttu-id="8a348-153">제품을 표시 하는 코드 추가</span><span class="sxs-lookup"><span data-stu-id="8a348-153">Add code to display products</span></span>

<span data-ttu-id="8a348-154">이 단계에서는 **ListView** 컨트롤을 데이터베이스의 제품 데이터로 채우는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-154">In this step, you'll add code to populate the **ListView** control with product data from the database.</span></span> <span data-ttu-id="8a348-155">이 코드는 모든 제품 및 개별 범주 제품 표시를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-155">The code supports showing all products and  individual category products.</span></span>

1. <span data-ttu-id="8a348-156">**솔루션 탐색기**에서 *ProductList* 를 마우스 오른쪽 단추로 클릭 한 다음 **코드 보기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-156">In **Solution Explorer**, right-click *ProductList.aspx* and then select **View Code**.</span></span>
2. <span data-ttu-id="8a348-157">*ProductList.aspx.cs* 파일의 기존 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-157">Replace the existing code in the *ProductList.aspx.cs* file with this:</span></span>   

    [!code-csharp[Main](display_data_items_and_details/samples/sample3.cs)]

<span data-ttu-id="8a348-158">이 코드는 *ProductList* 페이지에서 **ListView** 컨트롤의 `ItemType` 속성이 참조 하는 `GetProducts` 메서드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-158">This code shows the `GetProducts` method that the **ListView** control's `ItemType` property references in the *ProductList.aspx* page.</span></span> <span data-ttu-id="8a348-159">특정 데이터베이스 범주에 대 한 결과를 제한 하기 위해 코드는 *ProductList* 페이지를 탐색할 때 *ProductList* 페이지에 전달 된 쿼리 문자열 값에서 `categoryId` 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-159">To limit the results to a specific database category, the code sets the `categoryId` value from the query string value passed to the *ProductList.aspx* page when the *ProductList.aspx* page is navigated to.</span></span> <span data-ttu-id="8a348-160">`System.Web.ModelBinding` 네임 스페이스의 `QueryStringAttribute` 클래스는 `id`쿼리 문자열 변수의 값을 검색 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-160">The `QueryStringAttribute` class in the `System.Web.ModelBinding` namespace is used to retrieve the value of the query string variable `id`.</span></span> <span data-ttu-id="8a348-161">이렇게 하면 런타임에 쿼리 문자열의 값을 `categoryId` 매개 변수에 바인딩하기 위해 모델 바인딩이 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-161">This instructs model binding to try to bind a value from the query string to the `categoryId` parameter at run time.</span></span>

<span data-ttu-id="8a348-162">유효한 범주가 페이지에 쿼리 문자열로 전달 되는 경우 쿼리 결과는 데이터베이스에서 `categoryId` 값과 일치 하는 제품으로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-162">When a valid category is passed as a query string to the page, the results of the query are limited to those products in the database that match the `categoryId` value.</span></span> <span data-ttu-id="8a348-163">예를 들어, *ProductsList* 페이지 URL은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-163">For instance, if the *ProductsList.aspx* page URL is this:</span></span>

[!code-console[Main](display_data_items_and_details/samples/sample4.cmd)]

<span data-ttu-id="8a348-164">이 페이지에는 `categoryId` `1`와 같은 제품만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-164">The page displays only the products where the `categoryId` equals `1`.</span></span>

<span data-ttu-id="8a348-165">*ProductList* 페이지가 호출 될 때 쿼리 문자열이 포함 되지 않은 경우 모든 제품이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-165">All products are displayed if no query string is included when the *ProductList.aspx* page is called.</span></span>

<span data-ttu-id="8a348-166">이러한 메서드에 대 한 값의 소스를 *값 공급자* (예: *QueryString*) 라고 하며 사용할 값 공급자를 나타내는 매개 변수 특성을 *값 공급자 특성* (예: `id`) 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-166">The sources of values for these methods are referred to as *value providers* (such as *QueryString*), and the parameter attributes that indicate which value provider to use are referred to as *value provider attributes* (such as `id`).</span></span> <span data-ttu-id="8a348-167">ASP.NET에는 쿼리 문자열, 쿠키, 폼 값, 컨트롤, 뷰 상태, 세션 상태 및 프로필 속성과 같은 Web Forms 응용 프로그램에서 사용자 입력의 일반적인 모든 원본에 대 한 값 공급자 및 해당 특성이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-167">ASP.NET includes value providers and corresponding attributes for all of the typical sources of user input in a Web Forms application such as the query string, cookies, form values, controls, view state, session state, and profile properties.</span></span> <span data-ttu-id="8a348-168">사용자 지정 값 공급자를 작성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-168">You can also write custom value providers.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="8a348-169">애플리케이션 실행</span><span class="sxs-lookup"><span data-stu-id="8a348-169">Run the application</span></span>

<span data-ttu-id="8a348-170">이제 응용 프로그램을 실행 하 여 모든 제품 또는 범주의 제품을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-170">Run the application now to view all products or a category's products.</span></span>

1. <span data-ttu-id="8a348-171">Visual Studio에서 **f5** 키를 눌러 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-171">Press **F5** while in Visual Studio to run the application.</span></span>  
   <span data-ttu-id="8a348-172">브라우저가 열리고 *default.aspx 페이지가 표시 됩니다.*</span><span class="sxs-lookup"><span data-stu-id="8a348-172">The browser opens and shows the *Default.aspx* page.</span></span>

2. <span data-ttu-id="8a348-173">제품 범주 탐색 메뉴에서 **자동차** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-173">Select **Cars** from the product category navigation menu.</span></span>  
   <span data-ttu-id="8a348-174">*ProductList* 페이지에는 **자동차** 범주 제품만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-174">The *ProductList.aspx* page displays showing only **Cars** category products.</span></span> <span data-ttu-id="8a348-175">이 자습서의 뒷부분에서는 제품 세부 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-175">Later in this tutorial, you'll display product details.</span></span>  

    ![데이터 항목 및 세부 정보 표시-자동차](display_data_items_and_details/_static/image2.png)

3. <span data-ttu-id="8a348-177">위쪽의 탐색 메뉴에서 **제품** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-177">Select **Products** from the navigation menu at the top.</span></span>  
   <span data-ttu-id="8a348-178">*ProductList* 페이지가 표시 되지만 이번에는 전체 제품 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-178">Again, the *ProductList.aspx* page is displayed, however this time it shows the entire list of products.</span></span>   

    ![데이터 항목 및 세부 정보 표시-제품](display_data_items_and_details/_static/image3.png)

4. <span data-ttu-id="8a348-180">브라우저를 닫고 Visual Studio로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-180">Close the browser and return to Visual Studio.</span></span>

### <a name="add-a-data-control-to-display-product-details"></a><span data-ttu-id="8a348-181">제품 정보를 표시 하는 데이터 컨트롤 추가</span><span class="sxs-lookup"><span data-stu-id="8a348-181">Add a data control to display product details</span></span>

<span data-ttu-id="8a348-182">다음으로, 이전 자습서에서 추가한 제품 *세부 정보 .aspx* 페이지의 태그를 수정 하 여 특정 제품 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-182">Next, you'll modify the markup in the *ProductDetails.aspx* page that you added in the previous tutorial to display specific product information.</span></span>

1. <span data-ttu-id="8a348-183">**솔루션 탐색기**에서 *제품 세부 정보 .aspx*를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-183">In **Solution Explorer**, open *ProductDetails.aspx*.</span></span>

2. <span data-ttu-id="8a348-184">기존 태그를 다음 태그로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-184">Replace the existing markup with this markup:</span></span>

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample5.aspx)] 

    <span data-ttu-id="8a348-185">이 코드는 **FormView** 컨트롤을 사용 하 여 특정 제품 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-185">This code uses a **FormView** control to display specific product details.</span></span> <span data-ttu-id="8a348-186">이 태그는 *ProductList* 페이지에 데이터를 표시 하는 데 사용 되는 메서드와 같은 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-186">This markup uses methods like the methods used to display data in the *ProductList.aspx* page.</span></span> <span data-ttu-id="8a348-187">**FormView** 컨트롤은 데이터 소스에서 한 번에 하나의 레코드를 표시 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-187">The **FormView** control is used to display a single record at a time from a data source.</span></span> <span data-ttu-id="8a348-188">**FormView** 컨트롤을 사용 하는 경우 데이터 바인딩된 값을 표시 하 고 편집 하는 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-188">When you use the **FormView** control, you create templates to display and edit data-bound values.</span></span> <span data-ttu-id="8a348-189">이러한 템플릿에는 폼의 모양과 기능을 정의 하는 컨트롤, 바인딩 식 및 형식이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-189">These templates contain controls, binding expressions, and formatting that define the form's look and functionality.</span></span>

<span data-ttu-id="8a348-190">이전 태그를 데이터베이스에 연결 하려면 추가 코드가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-190">Connecting the previous markup to the database requires additional code.</span></span>

1. <span data-ttu-id="8a348-191">**솔루션 탐색기**에서 *제품 세부 정보 .aspx* 를 마우스 오른쪽 단추로 클릭 한 다음 **코드 보기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-191">In **Solution Explorer**, right-click *ProductDetails.aspx* and then click **View Code**.</span></span>  
   <span data-ttu-id="8a348-192">*ProductDetails.aspx.cs* 파일이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-192">The *ProductDetails.aspx.cs* file is displayed.</span></span>

2. <span data-ttu-id="8a348-193">기존 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-193">Replace the existing code with this code:</span></span>   

    [!code-csharp[Main](display_data_items_and_details/samples/sample6.cs)]

<span data-ttu-id="8a348-194">이 코드는 "`productID`" 쿼리 문자열 값을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-194">This code checks for a "`productID`" query-string value.</span></span> <span data-ttu-id="8a348-195">올바른 쿼리 문자열 값이 발견 되 면 일치 하는 제품이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-195">If a valid query-string value is found, the matching product is displayed.</span></span> <span data-ttu-id="8a348-196">쿼리 문자열을 찾을 수 없거나 해당 값이 유효 하지 않으면 제품이 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-196">If the query-string isn't found, or its value isn't valid, no product is displayed.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="8a348-197">애플리케이션 실행</span><span class="sxs-lookup"><span data-stu-id="8a348-197">Run the application</span></span>

<span data-ttu-id="8a348-198">이제 응용 프로그램을 실행 하 여 제품 ID에 따라 표시 된 개별 제품을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-198">Now you can run the application to see an individual product displayed based on product ID.</span></span>

1. <span data-ttu-id="8a348-199">Visual Studio에서 **f5** 키를 눌러 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-199">Press **F5** while in Visual Studio to run the application.</span></span>  
   <span data-ttu-id="8a348-200">브라우저가 열리고 *default.aspx 페이지가 표시 됩니다.*</span><span class="sxs-lookup"><span data-stu-id="8a348-200">The browser opens and shows the *Default.aspx* page.</span></span>

2. <span data-ttu-id="8a348-201">범주 탐색 메뉴에서 **배** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-201">Select **Boats** from the category navigation menu.</span></span>  
   <span data-ttu-id="8a348-202">*ProductList* 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-202">The *ProductList.aspx* page is displayed.</span></span>

3. <span data-ttu-id="8a348-203">제품 목록에서 **Paper 보트** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-203">Select **Paper Boat** from the product list.</span></span>
   <span data-ttu-id="8a348-204">*제품 세부 정보 .aspx* 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-204">The *ProductDetails.aspx* page is displayed.</span></span>

    ![데이터 항목 및 세부 정보 표시-제품](display_data_items_and_details/_static/image4.png)
    
4. <span data-ttu-id="8a348-206">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-206">Close the browser.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8a348-207">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="8a348-207">Additional resources</span></span>

[<span data-ttu-id="8a348-208">모델 바인딩 및 web forms를 사용 하 여 데이터 검색 및 표시</span><span class="sxs-lookup"><span data-stu-id="8a348-208">Retrieving and displaying data with model binding and web forms</span></span>](../../presenting-and-managing-data/model-binding/retrieving-data.md)

## <a name="next-steps"></a><span data-ttu-id="8a348-209">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8a348-209">Next steps</span></span>

<span data-ttu-id="8a348-210">이 자습서에서는 제품 및 제품 세부 정보를 표시 하는 태그와 코드를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-210">In this tutorial, you added markup and code to display products and product details.</span></span> <span data-ttu-id="8a348-211">강력한 형식의 데이터 컨트롤, 모델 바인딩 및 값 공급자에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-211">You learned about strongly typed data controls, model binding, and value providers.</span></span> <span data-ttu-id="8a348-212">다음 자습서에서는 정문 장난감 샘플 응용 프로그램에 쇼핑 카트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a348-212">In the next tutorial, you'll add a shopping cart to the Wingtip Toys sample application.</span></span> 

> [!div class="step-by-step"]
> <span data-ttu-id="8a348-213">[이전](ui_and_navigation.md)
> [다음](shopping-cart.md)</span><span class="sxs-lookup"><span data-stu-id="8a348-213">[Previous](ui_and_navigation.md)
[Next](shopping-cart.md)</span></span>
