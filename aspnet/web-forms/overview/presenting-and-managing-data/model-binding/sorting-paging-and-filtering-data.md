---
uid: web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
title: 모델 바인딩 및 web forms를 사용 하 여 데이터 정렬, 페이징 및 필터링 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서 시리즈에서는 ASP.NET Web Forms 프로젝트를 사용 하 여 모델 바인딩을 사용 하는 기본적인 측면을 보여 줍니다. 모델 바인딩을 사용 하면 데이터 상호 작용이 더 간편 하 게-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 266e7866-e327-4687-b29d-627a0925e87d
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
msc.type: authoredcontent
ms.openlocfilehash: f8e64392af6110f36c6af98c4e4e9481c94a0d82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78441065"
---
# <a name="sorting-paging-and-filtering-data-with-model-binding-and-web-forms"></a><span data-ttu-id="ace92-104">모델 바인딩 및 web forms를 사용 하 여 데이터 정렬, 페이징 및 필터링</span><span class="sxs-lookup"><span data-stu-id="ace92-104">Sorting, paging, and filtering data with model binding and web forms</span></span>

<span data-ttu-id="ace92-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="ace92-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="ace92-106">이 자습서 시리즈에서는 ASP.NET Web Forms 프로젝트를 사용 하 여 모델 바인딩을 사용 하는 기본적인 측면을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="ace92-107">모델 바인딩을 사용 하면 데이터 원본 개체 (예: ObjectDataSource 또는 SqlDataSource)를 처리 하는 것 보다 데이터 상호 작용이 보다 간단 하 게 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="ace92-108">이 시리즈는 소개 자료로 시작 하 고 이후 자습서에서 보다 고급 개념으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="ace92-109">이 자습서에서는 모델 바인딩을 통해 데이터의 정렬, 페이징 및 필터링을 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-109">This tutorial shows how to add sorting, paging, and filtering of the data through model binding.</span></span>
> 
> <span data-ttu-id="ace92-110">이 자습서는 계열의 첫 번째 [부분](retrieving-data.md) 에서 만든 프로젝트를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-110">This tutorial builds on the project created in the first [part](retrieving-data.md) of the series.</span></span>
> 
> <span data-ttu-id="ace92-111">또는 VB 에서 C# 전체 프로젝트를 [다운로드](https://go.microsoft.com/fwlink/?LinkId=286116)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-111">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="ace92-112">다운로드 가능한 코드는 Visual Studio 2012 또는 Visual Studio 2013와 함께 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-112">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="ace92-113">이 자습서에서는이 자습서에 표시 된 Visual Studio 2013 템플릿과 약간 다른 Visual Studio 2012 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-113">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="ace92-114">빌드할 내용</span><span class="sxs-lookup"><span data-stu-id="ace92-114">What you'll build</span></span>

<span data-ttu-id="ace92-115">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-115">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="ace92-116">데이터 정렬 및 페이징 사용</span><span class="sxs-lookup"><span data-stu-id="ace92-116">Enable sorting and paging of the data</span></span>
2. <span data-ttu-id="ace92-117">사용자가 선택한 항목을 기준으로 데이터 필터링 사용</span><span class="sxs-lookup"><span data-stu-id="ace92-117">Enable filtering of the data based on a selection by the user</span></span>

## <a name="add-sorting"></a><span data-ttu-id="ace92-118">정렬 추가</span><span class="sxs-lookup"><span data-stu-id="ace92-118">Add sorting</span></span>

<span data-ttu-id="ace92-119">GridView에서 정렬을 사용 하는 것은 매우 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-119">Enabling sorting in the GridView is very easy.</span></span> <span data-ttu-id="ace92-120">학생용 .aspx 파일에서 GridView의 **Allowsorting** **true** 로 설정 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-120">In the Student.aspx file, simply set **AllowSorting** to **true** in the GridView.</span></span> <span data-ttu-id="ace92-121">DataField가 자동으로 사용 되기 때문에 각 열에 대해 **SortExpression** 값을 설정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-121">You do not need to set a **SortExpression** value for each column as the DataField is automatically used.</span></span> <span data-ttu-id="ace92-122">GridView는 선택한 값을 기준으로 데이터 순서 지정을 포함 하도록 쿼리를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-122">The GridView modifies the query to include ordering the data by the selected value.</span></span> <span data-ttu-id="ace92-123">아래 강조 표시 된 코드는 정렬을 사용 하도록 설정 하는 데 필요한 추가 작업을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-123">The highlighted code below shows the addition you need to make to enable sorting.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample1.aspx?highlight=5)]

<span data-ttu-id="ace92-124">웹 응용 프로그램을 실행 하 고 여러 열의 값을 기준으로 학생 레코드 정렬을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-124">Run the web application, and test sorting student records by the values in different columns.</span></span>

![학생 정렬](sorting-paging-and-filtering-data/_static/image2.png)

## <a name="add-paging"></a><span data-ttu-id="ace92-126">페이징 추가</span><span class="sxs-lookup"><span data-stu-id="ace92-126">Add paging</span></span>

<span data-ttu-id="ace92-127">페이징을 사용 하는 것도 매우 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-127">Enabling paging is also very easy.</span></span> <span data-ttu-id="ace92-128">GridView에서 **AllowPaging** 속성을 **true** 로 설정 하 고 **PageSize** 속성을 각 페이지에 표시할 레코드 수로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-128">In the GridView, set the **AllowPaging** property to **true** and set the **PageSize** property to the number of records you wish to display on each page.</span></span> <span data-ttu-id="ace92-129">이 자습서에서는 4로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-129">In this tutorial, you can set it to 4.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample2.aspx?highlight=5)]

<span data-ttu-id="ace92-130">웹 응용 프로그램을 실행 합니다. 이제 레코드는 단일 페이지에 표시 되는 레코드가 4 개이 하를 포함 하는 여러 페이지로 나뉘어 있음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-130">Run the web application, and notice that now the records are divided over multiple pages with no more than 4 records displayed on a single page.</span></span>

![페이징 추가](sorting-paging-and-filtering-data/_static/image4.png)

<span data-ttu-id="ace92-132">지연 된 쿼리 실행은 응용 프로그램의 효율성을 향상 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-132">Deferred query execution improves the application efficiency.</span></span> <span data-ttu-id="ace92-133">GridView는 전체 데이터 집합을 검색 하는 대신 현재 페이지에 대 한 레코드만 검색 하도록 쿼리를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-133">Instead of retrieving the entire data set, the GridView modifies the query to retrieve only the records for the current page.</span></span>

## <a name="filter-records-by-user-selection"></a><span data-ttu-id="ace92-134">사용자 선택에 따라 레코드 필터링</span><span class="sxs-lookup"><span data-stu-id="ace92-134">Filter records by user selection</span></span>

<span data-ttu-id="ace92-135">모델 바인딩은 모델 바인딩 메서드에서 매개 변수의 값을 설정 하는 방법을 지정할 수 있는 여러 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-135">Model binding adds several attributes which enable you to designate how to set the value for a parameter in a model binding method.</span></span> <span data-ttu-id="ace92-136">이러한 특성은 **system.web. ModelBinding** 네임 스페이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-136">These attributes are in the **System.Web.ModelBinding** namespace.</span></span> <span data-ttu-id="ace92-137">다음과 같은 변경 내용이 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-137">They include:</span></span>

- <span data-ttu-id="ace92-138">컨트롤</span><span class="sxs-lookup"><span data-stu-id="ace92-138">Control</span></span>
- <span data-ttu-id="ace92-139">쿠키</span><span class="sxs-lookup"><span data-stu-id="ace92-139">Cookie</span></span>
- <span data-ttu-id="ace92-140">Form</span><span class="sxs-lookup"><span data-stu-id="ace92-140">Form</span></span>
- <span data-ttu-id="ace92-141">프로필</span><span class="sxs-lookup"><span data-stu-id="ace92-141">Profile</span></span>
- <span data-ttu-id="ace92-142">QueryString</span><span class="sxs-lookup"><span data-stu-id="ace92-142">QueryString</span></span>
- <span data-ttu-id="ace92-143">RouteData</span><span class="sxs-lookup"><span data-stu-id="ace92-143">RouteData</span></span>
- <span data-ttu-id="ace92-144">세션</span><span class="sxs-lookup"><span data-stu-id="ace92-144">Session</span></span>
- <span data-ttu-id="ace92-145">UserProfile</span><span class="sxs-lookup"><span data-stu-id="ace92-145">UserProfile</span></span>
- <span data-ttu-id="ace92-146">ViewState</span><span class="sxs-lookup"><span data-stu-id="ace92-146">ViewState</span></span>

<span data-ttu-id="ace92-147">이 자습서에서는 컨트롤의 값을 사용 하 여 GridView에 표시 되는 레코드를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-147">In this tutorial, you will use a control's value to filter which records are displayed in the GridView.</span></span> <span data-ttu-id="ace92-148">이전에 만든 쿼리 메서드에 **컨트롤** 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-148">You will add the **Control** attribute to the query method you had created earlier.</span></span> <span data-ttu-id="ace92-149">[이후](using-query-string-values-to-retrieve-data.md) 자습서에서는 매개 변수 값이 쿼리 문자열 값에서 제공 되도록 지정 하기 위해 **QueryString** 특성을 매개 변수에 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-149">In a [later](using-query-string-values-to-retrieve-data.md) tutorial, you will apply the **QueryString** attribute to a parameter to specify that the parameter value comes from a query string value.</span></span>

<span data-ttu-id="ace92-150">먼저 ValidationSummary 위에서 표시 되는 학생을 필터링 하기 위한 드롭다운 목록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-150">First, above the ValidationSummary, add a drop down list for filtering which students are shown.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample3.aspx?highlight=3-11)]

<span data-ttu-id="ace92-151">코드 숨김이 파일에서 컨트롤의 값을 받도록 select 메서드를 수정 하 고, 매개 변수의 이름을 값을 제공 하는 컨트롤의 이름으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-151">In the code-behind file, modify the select method to receive a value from the control, and set the name of the parameter to the name of the control that provides the value.</span></span>

<span data-ttu-id="ace92-152">컨트롤 특성을 확인 하려면 system.web **. ModelBinding** 네임 스페이스에 대 한 **using** 문을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-152">You must add a **using** statement for the **System.Web.ModelBinding** namespace to resolve the Control attribute.</span></span>

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample4.cs)]

<span data-ttu-id="ace92-153">다음 코드는 드롭다운 목록의 값을 기준으로 반환 된 데이터를 필터링 하기 위해 다시 작동 하는 select 메서드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-153">The following code shows the select method re-worked to filter the returned data based on the value of the drop down list.</span></span> <span data-ttu-id="ace92-154">매개 변수 앞에 컨트롤 특성을 추가 하면이 매개 변수의 값이 같은 이름의 컨트롤에서 오는 것으로 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-154">Adding a control attribute before a parameter specifies that the value for this parameter comes from a control with the same name.</span></span>

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample5.cs)]

<span data-ttu-id="ace92-155">웹 응용 프로그램을 실행 하 고 드롭다운 목록에서 다른 값을 선택 하 여 학생 목록을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-155">Run the web application and select different values from the drop down list to filter the list of students.</span></span>

![학생 필터링](sorting-paging-and-filtering-data/_static/image6.png)

## <a name="conclusion"></a><span data-ttu-id="ace92-157">결론</span><span class="sxs-lookup"><span data-stu-id="ace92-157">Conclusion</span></span>

<span data-ttu-id="ace92-158">이 자습서에서는 데이터의 정렬과 페이징을 사용 하도록 설정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-158">In this tutorial, you enabled sorting and paging of the data.</span></span> <span data-ttu-id="ace92-159">또한 컨트롤의 값을 기준으로 데이터를 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-159">You also enabled filtering the data by the value of a control.</span></span>

<span data-ttu-id="ace92-160">다음 [자습서](integrating-jquery-ui.md) 에서는 JQuery ui 위젯을 동적 데이터 템플릿에 통합 하 여 ui를 향상 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="ace92-160">In the next [tutorial](integrating-jquery-ui.md) you will enhance the UI by integrating a JQuery UI widget into the dynamic data template.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ace92-161">[이전](updating-deleting-and-creating-data.md)
> [다음](integrating-jquery-ui.md)</span><span class="sxs-lookup"><span data-stu-id="ace92-161">[Previous](updating-deleting-and-creating-data.md)
[Next](integrating-jquery-ui.md)</span></span>
