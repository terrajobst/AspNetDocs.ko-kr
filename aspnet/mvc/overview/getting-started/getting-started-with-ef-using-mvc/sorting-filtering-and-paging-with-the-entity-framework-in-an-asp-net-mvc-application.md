---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: '자습서: ASP.NET MVC 응용 프로그램에서 Entity Framework를 사용 하 여 정렬, 필터링 및 페이징 추가 | Microsoft Docs'
author: tdykstra
description: 이 자습서에서는 **학생** 인덱스 페이지에 정렬, 필터링 및 페이징 기능을 추가 합니다. 간단한 그룹화 페이지도 만들 수 있습니다.
ms.author: riande
ms.date: 01/14/2019
ms.assetid: d5723e46-41fe-4d09-850a-e03b9e285bfa
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: d9fadc12aa83a8095f364cf39e5376243a7d0670
ms.sourcegitcommit: f774732a3960fca079438a88a5472c37cf7be08a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2019
ms.locfileid: "68810757"
---
# <a name="tutorial-add-sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application"></a><span data-ttu-id="1e46b-104">자습서: ASP.NET MVC 응용 프로그램에서 Entity Framework를 사용 하 여 정렬, 필터링 및 페이징 추가</span><span class="sxs-lookup"><span data-stu-id="1e46b-104">Tutorial: Add sorting, filtering, and paging with the Entity Framework in an ASP.NET MVC application</span></span>

<span data-ttu-id="1e46b-105">[이전 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)에서는 엔터티에 대 한 `Student` 기본 CRUD 작업을 위한 일련의 웹 페이지를 구현 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-105">In the [previous tutorial](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md), you implemented a set of web pages for basic CRUD operations for `Student` entities.</span></span> <span data-ttu-id="1e46b-106">이 자습서에서는 **학생** 인덱스 페이지에 정렬, 필터링 및 페이징 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-106">In this tutorial you add sorting, filtering, and paging functionality to the **Students** Index page.</span></span> <span data-ttu-id="1e46b-107">간단한 그룹화 페이지도 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-107">You also create a simple grouping page.</span></span>

<span data-ttu-id="1e46b-108">다음 이미지는 완료 될 때 페이지가 표시 되는 모양을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-108">The following image shows what the page will look like when you're done.</span></span> <span data-ttu-id="1e46b-109">열 제목은 해당 열로 정렬하기 위해 사용자가 클릭할 수 있는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-109">The column headings are links that the user can click to sort by that column.</span></span> <span data-ttu-id="1e46b-110">열 제목을 반복해서 클릭하면 오름차순 및 내림차순으로 정렬 순서가 토글됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-110">Clicking a column heading repeatedly toggles between ascending and descending sort order.</span></span>

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

<span data-ttu-id="1e46b-112">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-112">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1e46b-113">열 정렬 링크 추가</span><span class="sxs-lookup"><span data-stu-id="1e46b-113">Add column sort links</span></span>
> * <span data-ttu-id="1e46b-114">검색 상자 추가</span><span class="sxs-lookup"><span data-stu-id="1e46b-114">Add a Search box</span></span>
> * <span data-ttu-id="1e46b-115">페이징 추가</span><span class="sxs-lookup"><span data-stu-id="1e46b-115">Add paging</span></span>
> * <span data-ttu-id="1e46b-116">정보 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="1e46b-116">Create an About page</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e46b-117">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="1e46b-117">Prerequisites</span></span>

* [<span data-ttu-id="1e46b-118">기본 CRUD 기능 구현</span><span class="sxs-lookup"><span data-stu-id="1e46b-118">Implementing Basic CRUD Functionality</span></span>](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)

## <a name="add-column-sort-links"></a><span data-ttu-id="1e46b-119">열 정렬 링크 추가</span><span class="sxs-lookup"><span data-stu-id="1e46b-119">Add column sort links</span></span>

<span data-ttu-id="1e46b-120">학생 인덱스 페이지에 정렬을 추가 하려면 `Index` `Student` 컨트롤러의 메서드를 변경 하 `Student` 고 인덱스 뷰에 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-120">To add sorting to the Student Index page, you'll change the `Index` method of the `Student` controller and add code to the `Student` Index view.</span></span>

### <a name="add-sorting-functionality-to-the-index-method"></a><span data-ttu-id="1e46b-121">인덱스 메서드에 정렬 기능 추가</span><span class="sxs-lookup"><span data-stu-id="1e46b-121">Add sorting functionality to the Index method</span></span>

- <span data-ttu-id="1e46b-122">*Controllers\StudentController.cs*에서 `Index` 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-122">In *Controllers\StudentController.cs*, replace the `Index` method with the following code:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="1e46b-123">이 코드는 URL의 쿼리 문자열에서 `sortOrder` 매개 변수를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-123">This code receives a `sortOrder` parameter from the query string in the URL.</span></span> <span data-ttu-id="1e46b-124">쿼리 문자열 값은 ASP.NET MVC에서 작업 메서드에 대 한 매개 변수로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-124">The query string value is provided by ASP.NET MVC as a parameter to the action method.</span></span> <span data-ttu-id="1e46b-125">매개 변수는 "Name" 또는 "Date" 이며, 선택적으로 밑줄을 지정 하 고 문자열 "desc"를 내림차순으로 지정 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-125">The parameter is a string that's either "Name" or "Date", optionally followed by an underscore and the string "desc" to specify descending order.</span></span> <span data-ttu-id="1e46b-126">기본 정렬 순서는 오름차순입니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-126">The default sort order is ascending.</span></span>

<span data-ttu-id="1e46b-127">인덱스 페이지를 처음 요청하면 쿼리 문자열은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-127">The first time the Index page is requested, there's no query string.</span></span> <span data-ttu-id="1e46b-128">학습자는 `switch` 문에 대 한 제어에 의해 `LastName`설정 된 기본값 인 오름차순으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-128">The students are displayed in ascending order by `LastName`, which is the default as established by the fall-through case in the `switch` statement.</span></span> <span data-ttu-id="1e46b-129">사용자가 열 제목 하이퍼링크를 클릭하면 쿼리 문자열에 해당 `sortOrder` 값이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-129">When the user clicks a column heading hyperlink, the appropriate `sortOrder` value is provided in the query string.</span></span>

<span data-ttu-id="1e46b-130">뷰가 적절 `ViewBag` 한 쿼리 문자열 값을 사용 하 여 열 머리글 하이퍼링크를 구성할 수 있도록 두 개의 변수가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-130">The two `ViewBag` variables are used so that the view can configure the column heading hyperlinks with the appropriate query string values:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="1e46b-131">이것은 3개로 구성된 문입니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-131">These are ternary statements.</span></span> <span data-ttu-id="1e46b-132">첫 번째 `sortOrder` 매개 변수는 매개 변수가 null 이거나 `ViewBag.NameSortParm` 비어 있는 경우 "이름\_desc"로 설정 해야 함을 지정 하 고, 그렇지 않은 경우에는 빈 문자열로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-132">The first one specifies that if the `sortOrder` parameter is null or empty, `ViewBag.NameSortParm` should be set to "name\_desc"; otherwise, it should be set to an empty string.</span></span> <span data-ttu-id="1e46b-133">이러한 두 명령문을 사용하면 뷰에서 다음과 같이 열 제목 하이퍼링크를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-133">These two statements enable the view to set the column heading hyperlinks as follows:</span></span>

| <span data-ttu-id="1e46b-134">현재 정렬 순서</span><span class="sxs-lookup"><span data-stu-id="1e46b-134">Current sort order</span></span> | <span data-ttu-id="1e46b-135">성 하이퍼링크</span><span class="sxs-lookup"><span data-stu-id="1e46b-135">Last Name Hyperlink</span></span> | <span data-ttu-id="1e46b-136">날짜 하이퍼링크</span><span class="sxs-lookup"><span data-stu-id="1e46b-136">Date Hyperlink</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1e46b-137">성 오름차순</span><span class="sxs-lookup"><span data-stu-id="1e46b-137">Last Name ascending</span></span> | <span data-ttu-id="1e46b-138">descending</span><span class="sxs-lookup"><span data-stu-id="1e46b-138">descending</span></span> | <span data-ttu-id="1e46b-139">ascending</span><span class="sxs-lookup"><span data-stu-id="1e46b-139">ascending</span></span> |
| <span data-ttu-id="1e46b-140">성 내림차순</span><span class="sxs-lookup"><span data-stu-id="1e46b-140">Last Name descending</span></span> | <span data-ttu-id="1e46b-141">ascending</span><span class="sxs-lookup"><span data-stu-id="1e46b-141">ascending</span></span> | <span data-ttu-id="1e46b-142">ascending</span><span class="sxs-lookup"><span data-stu-id="1e46b-142">ascending</span></span> |
| <span data-ttu-id="1e46b-143">날짜 오름차순</span><span class="sxs-lookup"><span data-stu-id="1e46b-143">Date ascending</span></span> | <span data-ttu-id="1e46b-144">ascending</span><span class="sxs-lookup"><span data-stu-id="1e46b-144">ascending</span></span> | <span data-ttu-id="1e46b-145">descending</span><span class="sxs-lookup"><span data-stu-id="1e46b-145">descending</span></span> |
| <span data-ttu-id="1e46b-146">날짜 내림차순</span><span class="sxs-lookup"><span data-stu-id="1e46b-146">Date descending</span></span> | <span data-ttu-id="1e46b-147">ascending</span><span class="sxs-lookup"><span data-stu-id="1e46b-147">ascending</span></span> | <span data-ttu-id="1e46b-148">ascending</span><span class="sxs-lookup"><span data-stu-id="1e46b-148">ascending</span></span> |

<span data-ttu-id="1e46b-149">메서드는 [LINQ to Entities](/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities) 을 사용 하 여 정렬 기준으로 사용할 열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-149">The method uses [LINQ to Entities](/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities) to specify the column to sort by.</span></span> <span data-ttu-id="1e46b-150">이 코드는 `switch` 문 <xref:System.Linq.IQueryable%601> 앞에 변수 `switch` 를 만들고, `switch` 문에서이를 수정 하 고, 문 `ToList` 다음에 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-150">The code creates an <xref:System.Linq.IQueryable%601> variable before the `switch` statement, modifies it in the `switch` statement, and calls the `ToList` method after the `switch` statement.</span></span> <span data-ttu-id="1e46b-151">`IQueryable` 변수를 작성하고 수정하면 데이터베이스에 쿼리가 보내지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-151">When you create and modify `IQueryable` variables, no query is sent to the database.</span></span> <span data-ttu-id="1e46b-152">`IQueryable` 와`ToList`같은 메서드를 호출 하 여 개체를 컬렉션으로 변환할 때까지 쿼리가 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-152">The query is not executed until you convert the `IQueryable` object into a collection by calling a method such as `ToList`.</span></span> <span data-ttu-id="1e46b-153">따라서이 코드는 `return View` 문까지 실행 되지 않는 단일 쿼리를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-153">Therefore, this code results in a single query that is not executed until the `return View` statement.</span></span>

<span data-ttu-id="1e46b-154">각 정렬 순서에 대해 서로 다른 LINQ 문을 작성 하는 대신 LINQ 문을 동적으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-154">As an alternative to writing different LINQ statements for each sort order, you can dynamically create a LINQ statement.</span></span> <span data-ttu-id="1e46b-155">동적 LINQ에 대 한 자세한 내용은 [동적 linq](https://go.microsoft.com/fwlink/?LinkID=323957)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="1e46b-155">For information about dynamic LINQ, see [Dynamic LINQ](https://go.microsoft.com/fwlink/?LinkID=323957).</span></span>

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a><span data-ttu-id="1e46b-156">학생 인덱스 뷰에 열 제목 하이퍼링크 추가</span><span class="sxs-lookup"><span data-stu-id="1e46b-156">Add column heading hyperlinks to the Student index view</span></span>

1. <span data-ttu-id="1e46b-157">*Views\Student\Index.cshtml*에서 제목 행의 `<tr>` 및 `<th>` 요소를 강조 표시 된 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-157">In *Views\Student\Index.cshtml*, replace the `<tr>` and `<th>` elements for the heading row with the highlighted code:</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

   <span data-ttu-id="1e46b-158">이 코드는 `ViewBag` 속성의 정보를 사용 하 여 적절 한 쿼리 문자열 값으로 하이퍼링크를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-158">This code uses the information in the `ViewBag` properties to set up hyperlinks with the appropriate query string values.</span></span>

2. <span data-ttu-id="1e46b-159">페이지를 실행 하 고 **Last Name** 및 **등록 날짜** 열 제목을 클릭 하 여 정렬이 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-159">Run the page and click the **Last Name** and **Enrollment Date** column headings to verify that sorting works.</span></span>

   <span data-ttu-id="1e46b-160">**성** 머리글을 클릭 하면 학생이 내림차순 성 순서로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-160">After you click the **Last Name** heading, students are displayed in descending last name order.</span></span>

## <a name="add-a-search-box"></a><span data-ttu-id="1e46b-161">검색 상자 추가</span><span class="sxs-lookup"><span data-stu-id="1e46b-161">Add a Search box</span></span>

<span data-ttu-id="1e46b-162">학생 인덱스 페이지에 필터링을 추가 하려면 보기에 텍스트 상자와 제출 단추를 추가 하 고 `Index` 메서드에서 해당 내용을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-162">To add filtering to the Students index page, you'll add a text box and a submit button to the view and make corresponding changes in the `Index` method.</span></span> <span data-ttu-id="1e46b-163">텍스트 상자를 사용 하 여 이름 및 성 필드에서 검색할 문자열을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-163">The text box lets you enter a string to search for in the first name and last name fields.</span></span>

### <a name="add-filtering-functionality-to-the-index-method"></a><span data-ttu-id="1e46b-164">인덱스 메서드에 필터링 기능 추가</span><span class="sxs-lookup"><span data-stu-id="1e46b-164">Add filtering functionality to the Index method</span></span>

- <span data-ttu-id="1e46b-165">*Controllers\StudentController.cs*에서 `Index` 메서드를 다음 코드로 바꿉니다 (변경 내용이 강조 표시 됨).</span><span class="sxs-lookup"><span data-stu-id="1e46b-165">In *Controllers\StudentController.cs*, replace the `Index` method with the following code (the changes are highlighted):</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

<span data-ttu-id="1e46b-166">이 코드는 매개 `searchString` 변수 `Index` 를 메서드에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-166">The code adds a `searchString` parameter to the `Index` method.</span></span> <span data-ttu-id="1e46b-167">검색 문자열 값은 Index 뷰에 추가할 텍스트 상자에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-167">The search string value is received from a text box that you'll add to the Index view.</span></span> <span data-ttu-id="1e46b-168">또한 첫 번째 이름 `where` 또는 성이 검색 문자열을 포함 하는 학생만 선택 하는 LINQ 문에 절을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-168">It also adds a `where` clause to the LINQ statement that selects only students whose first name or last name contains the search string.</span></span> <span data-ttu-id="1e46b-169">절을 <xref:System.Linq.Queryable.Where%2A> 추가 하는 문은 검색할 값이 있는 경우에만 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-169">The statement that adds the <xref:System.Linq.Queryable.Where%2A> clause executes only if there's a value to search for.</span></span>

> [!NOTE]
> <span data-ttu-id="1e46b-170">대부분의 경우 Entity Framework 엔터티 집합에 대해 동일한 메서드를 호출 하거나 메모리 내 컬렉션에서 확장 메서드로 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-170">In many cases you can call the same method either on an Entity Framework entity set or as an extension method on an in-memory collection.</span></span> <span data-ttu-id="1e46b-171">결과는 일반적으로 동일 하지만 경우에 따라 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-171">The results are normally the same but in some cases may be different.</span></span>
>
> <span data-ttu-id="1e46b-172">예를 들어 `Contains` 메서드의 .NET Framework 구현은 빈 문자열을 전달할 때 모든 행을 반환 하지만 SQL Server Compact 4.0에 대 한 Entity Framework 공급자는 빈 문자열에 대해 0 개의 행을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-172">For example, the .NET Framework implementation of the `Contains` method returns all rows when you pass an empty string to it, but the Entity Framework provider for SQL Server Compact 4.0 returns zero rows for empty strings.</span></span> <span data-ttu-id="1e46b-173">따라서이 예제의 코드 (문 `Where` `if` 내에 문을 배치)는 모든 버전의 SQL Server에 대해 동일한 결과를 얻을 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-173">Therefore the code in the example (putting the `Where` statement inside an `if` statement) makes sure that you get the same results for all versions of SQL Server.</span></span> <span data-ttu-id="1e46b-174">또한 `Contains` 메서드의 .NET Framework 구현은 기본적으로 대/소문자를 구분 하는 비교를 수행 하지만 Entity Framework SQL Server 공급자는 기본적으로 대/소문자를 구분 하지 않는 비교를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-174">Also, the .NET Framework implementation of the `Contains` method performs a case-sensitive comparison by default, but Entity Framework SQL Server providers perform case-insensitive comparisons by default.</span></span> <span data-ttu-id="1e46b-175">따라서 메서드를 `ToUpper` 호출 하 여 테스트를 명시적으로 대/소문자를 구분 하지 않도록 설정 하면 나중에 리포지토리를 사용 하도록 코드를 변경할 때 결과가 변경 되지 않습니다. `IEnumerable` 그러면 `IQueryable` 개체가 아닌 컬렉션이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-175">Therefore, calling the `ToUpper` method to make the test explicitly case-insensitive ensures that results do not change when you change the code later to use a repository, which will return an `IEnumerable` collection instead of an `IQueryable` object.</span></span> <span data-ttu-id="1e46b-176">(`IEnumerable` 컬렉션에서 `Contains` 메서드를 호출하면 .NET Framework 구현을 가져오고 `IQueryable` 개체에서 호출하면 데이터베이스 공급자 구현을 가져옵니다.)</span><span class="sxs-lookup"><span data-stu-id="1e46b-176">(When you call the `Contains` method on an `IEnumerable` collection, you get the .NET Framework implementation; when you call it on an `IQueryable` object, you get the database provider implementation.)</span></span>
>
> <span data-ttu-id="1e46b-177">또한 Null 처리는 데이터베이스 공급자 마다 다르거나 `IQueryable` `IEnumerable` 컬렉션을 사용 하는 경우와 비교 하 여 개체를 사용 하는 경우 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-177">Null handling may also be different for different database providers or when you use an `IQueryable` object compared to when you use an `IEnumerable` collection.</span></span> <span data-ttu-id="1e46b-178">예를 들어 일부 시나리오 `Where` 에서는와 `table.Column != 0` 같은 조건이 값 `null` 으로의 열을 반환 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-178">For example, in some scenarios a `Where` condition such as `table.Column != 0` may not return columns that have `null` as the value.</span></span> <span data-ttu-id="1e46b-179">기본적으로 EF는 메모리에서 작동 하는 것 처럼 데이터베이스에서 null 값이 일치 하도록 추가 SQL 연산자를 생성 하지만 EF6에서 [Usedatabasenullsemantics](https://docs.microsoft.com/dotnet/api/system.data.entity.infrastructure.dbcontextconfiguration.usedatabasenullsemantics) 플래그를 설정 하거나 EF Core의 [UseRelationalNulls](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.infrastructure.relationaldbcontextoptionsbuilder-2.userelationalnulls) 메서드를 호출할 수 있습니다. 이 동작을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-179">By default, EF generates additional SQL operators to make equality between null values work in the database like it works in memory, but you can set the [UseDatabaseNullSemantics](https://docs.microsoft.com/dotnet/api/system.data.entity.infrastructure.dbcontextconfiguration.usedatabasenullsemantics) flag in EF6 or call the [UseRelationalNulls](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.infrastructure.relationaldbcontextoptionsbuilder-2.userelationalnulls) method in EF Core to configure this behavior.</span></span>

### <a name="add-a-search-box-to-the-student-index-view"></a><span data-ttu-id="1e46b-180">학생 인덱스 뷰에 검색 상자 추가</span><span class="sxs-lookup"><span data-stu-id="1e46b-180">Add a search box to the Student index view</span></span>

1. <span data-ttu-id="1e46b-181">*Views\Student\Index.cshtml*에서 캡션, 텍스트 상자 및 **검색** 단추를 만들기 `table` 위해 강조 표시 된 코드를 여는 태그 바로 앞에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-181">In *Views\Student\Index.cshtml*, add the highlighted code immediately before the opening `table` tag in order to create a caption, a text box, and a **Search** button.</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=4-11)]

2. <span data-ttu-id="1e46b-182">페이지를 실행 하 고 검색 문자열을 입력 한 다음 **검색** 을 클릭 하 여 필터링이 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-182">Run the page, enter a search string, and click **Search** to verify that filtering is working.</span></span>

   <span data-ttu-id="1e46b-183">URL에 "a" 검색 문자열이 포함 되어 있지 않습니다. 즉,이 페이지를 책갈피로 만들면 책갈피를 사용할 때 필터링 된 목록을 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-183">Notice the URL doesn't contain the "an" search string, which means that if you bookmark this page, you won't get the filtered list when you use the bookmark.</span></span> <span data-ttu-id="1e46b-184">이는 전체 목록을 정렬 하기 때문에 열 정렬 링크에도 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-184">This applies also to the column sort links, as they will sort the whole list.</span></span> <span data-ttu-id="1e46b-185">**검색** 단추를 변경 하 여 자습서의 뒷부분에서 필터 조건에 대 한 쿼리 문자열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-185">You'll change the **Search** button to use query strings for filter criteria later in the tutorial.</span></span>

## <a name="add-paging"></a><span data-ttu-id="1e46b-186">페이징 추가</span><span class="sxs-lookup"><span data-stu-id="1e46b-186">Add paging</span></span>

<span data-ttu-id="1e46b-187">학생 인덱스 페이지에 페이징을 추가 하려면 **PagedList** NuGet 패키지를 설치 하는 것으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-187">To add paging to the Students index page, you'll start by installing the **PagedList.Mvc** NuGet package.</span></span> <span data-ttu-id="1e46b-188">그런 다음 `Index` 메서드를 추가로 변경 하 고 `Index` 뷰에 페이징 링크를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-188">Then you'll make additional changes in the `Index` method and add paging links to the `Index` view.</span></span> <span data-ttu-id="1e46b-189">**PagedList** 는 ASP.NET Mvc에 대 한 다양 한 페이징 및 정렬 패키지 중 하나 이며, 여기에서 사용 하는 것은 다른 옵션에 대 한 권장 사항이 아닌 예제로만 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-189">**PagedList.Mvc** is one of many good paging and sorting packages for ASP.NET MVC, and its use here is intended only as an example, not as a recommendation for it over other options.</span></span>

### <a name="install-the-pagedlistmvc-nuget-package"></a><span data-ttu-id="1e46b-190">PagedList NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-190">Install the PagedList.MVC NuGet package</span></span>

<span data-ttu-id="1e46b-191">NuGet **PagedList** 패키지는 자동으로 **PagedList** 패키지를 종속성으로 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-191">The NuGet **PagedList.Mvc** package automatically installs the **PagedList** package as a dependency.</span></span> <span data-ttu-id="1e46b-192">**PagedList** 패키지는 및 `PagedList` `IQueryable` 컬렉션`IEnumerable` 에 대 한 컬렉션 형식 및 확장 메서드를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-192">The **PagedList** package installs a `PagedList` collection type and extension methods for `IQueryable` and `IEnumerable` collections.</span></span> <span data-ttu-id="1e46b-193">`PagedList` 확장 메서드는 또는 `IQueryable` `IEnumerable`에서 컬렉션에 데이터의 단일 페이지를 만들며, 컬렉션은 `PagedList` 페이징을 용이 하 게 하는 여러 속성과 메서드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-193">The extension methods create a single page of data in a `PagedList` collection out of your `IQueryable` or `IEnumerable`, and the `PagedList` collection provides several properties and methods that facilitate paging.</span></span> <span data-ttu-id="1e46b-194">**PagedList** 패키지는 페이징 단추를 표시 하는 페이징 도우미를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-194">The **PagedList.Mvc** package installs a paging helper that displays the paging buttons.</span></span>

1. <span data-ttu-id="1e46b-195">**도구** 메뉴에서 **NuGet 패키지 관리자** , **패키지 관리자 콘솔**을 차례로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-195">From the **Tools** menu, select **NuGet Package Manager** and then **Package Manager Console**.</span></span>

2. <span data-ttu-id="1e46b-196">**패키지 관리자 콘솔** 창에서 **패키지 원본이** **Nuget.org** 이 고 **기본 프로젝트가** **ContosoUniversity**인지 확인 하 고 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-196">In the **Package Manager Console** window, make sure the **Package source** is **nuget.org** and the **Default project** is **ContosoUniversity**, and then enter the following command:</span></span>

   ```text
   Install-Package PagedList.Mvc
   ```

3. <span data-ttu-id="1e46b-197">프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-197">Build the project.</span></span>

### <a name="add-paging-functionality-to-the-index-method"></a><span data-ttu-id="1e46b-198">인덱스 메서드에 페이징 기능 추가</span><span class="sxs-lookup"><span data-stu-id="1e46b-198">Add paging functionality to the Index method</span></span>

1. <span data-ttu-id="1e46b-199">*Controllers\StudentController.cs*에서 `PagedList` 네임 스페이스에 `using` 대 한 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-199">In *Controllers\StudentController.cs*, add a `using` statement for the `PagedList` namespace:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

2. <span data-ttu-id="1e46b-200">`Index` 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-200">Replace the `Index` method with the following code:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=1,3,7-16,41-43)]

   <span data-ttu-id="1e46b-201">이 코드는 `page` 매개 변수, 현재 정렬 순서 매개 변수 및 현재 필터 매개 변수를 메서드 시그니처에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-201">This code adds a `page` parameter, a current sort order parameter, and a current filter parameter to the method signature:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

   <span data-ttu-id="1e46b-202">페이지가 처음 표시 될 때 또는 사용자가 페이징 또는 정렬 링크를 클릭 하지 않은 경우 모든 매개 변수가 null입니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-202">The first time the page is displayed, or if the user hasn't clicked a paging or sorting link, all the parameters are null.</span></span> <span data-ttu-id="1e46b-203">페이징 링크를 클릭 `page` 하면 표시할 페이지 번호가 변수에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-203">If a paging link is clicked, the `page` variable contains the page number to display.</span></span>

   <span data-ttu-id="1e46b-204">속성 `ViewBag` 은 뷰를 현재 정렬 순서와 함께 제공 합니다 .이는 페이징 링크에 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-204">A `ViewBag` property provides the view with the current sort order, because this must be included in the paging links in order to keep the sort order the same while paging:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

   <span data-ttu-id="1e46b-205">또 다른 속성인 `ViewBag.CurrentFilter`는 현재 필터 문자열을 사용 하 여 뷰를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-205">Another property, `ViewBag.CurrentFilter`, provides the view with the current filter string.</span></span> <span data-ttu-id="1e46b-206">이 값은 페이징 중 필터 설정을 유지하기 위해 페이징 링크에 포함되어야 하며 페이지를 다시 표시할 때 텍스트 상자에 복원되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-206">This value must be included in the paging links in order to maintain the filter settings during paging, and it must be restored to the text box when the page is redisplayed.</span></span> <span data-ttu-id="1e46b-207">페이징 중에 검색 문자열이 변경되면 새 필터로 인해 다른 데이터가 표시될 수 있으므로 페이지는 1로 재설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-207">If the search string is changed during paging, the page has to be reset to 1, because the new filter can result in different data to display.</span></span> <span data-ttu-id="1e46b-208">텍스트 상자에 값을 입력 하 고 제출 단추를 누르면 검색 문자열이 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-208">The search string is changed when a value is entered in the text box and the submit button is pressed.</span></span> <span data-ttu-id="1e46b-209">이 경우 `searchString` 매개 변수는 null이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-209">In that case, the `searchString` parameter is not null.</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

   <span data-ttu-id="1e46b-210">메서드 끝에서 학생 `ToPagedList` `IQueryable` 개체의 확장 메서드는 학생 쿼리를 페이징을 지 원하는 컬렉션 형식으로 학생의 단일 페이지로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-210">At the end of the method, the `ToPagedList` extension method on the students `IQueryable` object converts the student query to a single page of students in a collection type that supports paging.</span></span> <span data-ttu-id="1e46b-211">그런 다음 학생의 단일 페이지가 보기에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-211">That single page of students is then passed to the view:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

   <span data-ttu-id="1e46b-212">`ToPagedList` 메서드는 페이지 번호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-212">The `ToPagedList` method takes a page number.</span></span> <span data-ttu-id="1e46b-213">두 물음표는 [null 병합 연산자](/dotnet/csharp/language-reference/operators/null-coalescing-operator)를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-213">The two question marks represent the [null-coalescing operator](/dotnet/csharp/language-reference/operators/null-coalescing-operator).</span></span> <span data-ttu-id="1e46b-214">Null 병합 연산자는 nullable 형식의 기본값을 정의합니다. `(page ?? 1)` 식은 값이 있는 경우 `page` 값을 반환하고 `page`가 Null이면 1일 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-214">The null-coalescing operator defines a default value for a nullable type; the expression `(page ?? 1)` means return the value of `page` if it has a value, or return 1 if `page` is null.</span></span>

### <a name="add-paging-links-to-the-student-index-view"></a><span data-ttu-id="1e46b-215">학생 인덱스 뷰에 페이징 링크 추가</span><span class="sxs-lookup"><span data-stu-id="1e46b-215">Add paging links to the Student index view</span></span>

1. <span data-ttu-id="1e46b-216">*Views\Student\Index.cshtml*에서 기존 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-216">In *Views\Student\Index.cshtml*, replace the existing code with the following code.</span></span> <span data-ttu-id="1e46b-217">변경 내용은 강조 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-217">The changes are highlighted.</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=1-3,6,9,14,17,24,30,55-56,58-59)]

   <span data-ttu-id="1e46b-218">페이지 맨 위에 `@model` 문은 뷰가 `List` 개체 대신 `PagedList` 개체를 가져오는 것을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-218">The `@model` statement at the top of the page specifies that the view now gets a `PagedList` object instead of a `List` object.</span></span>

   <span data-ttu-id="1e46b-219">에 대 한 `PagedList.Mvc` 문은페이징단추의MVC도우미에대한액세스를제공합니다.`using`</span><span class="sxs-lookup"><span data-stu-id="1e46b-219">The `using` statement for `PagedList.Mvc` gives access to the MVC helper for the paging buttons.</span></span>

   <span data-ttu-id="1e46b-220">코드는 [Formmethod. Get](/previous-versions/aspnet/dd460179(v=vs.100))을 지정할 수 있는 [html.beginform](/previous-versions/aspnet/dd492719(v=vs.108)) 의 오버 로드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-220">The code uses an overload of [BeginForm](/previous-versions/aspnet/dd492719(v=vs.108)) that allows it to specify [FormMethod.Get](/previous-versions/aspnet/dd460179(v=vs.100)).</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

   <span data-ttu-id="1e46b-221">기본 [HTML.BEGINFORM](/previous-versions/aspnet/dd492719(v=vs.108)) POST를 사용 하 여 폼 데이터를 전송 합니다. 즉, 매개 변수가 HTTP 메시지 본문에 전달 되 고 URL에 쿼리 문자열로 전달 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-221">The default [BeginForm](/previous-versions/aspnet/dd492719(v=vs.108)) submits form data with a POST, which means that parameters are passed in the HTTP message body and not in the URL as query strings.</span></span> <span data-ttu-id="1e46b-222">HTTP GET을 지정하면 폼 데이터가 URL에 쿼리 문자열로 전달되고 이를 통해 사용자는 URL을 책갈피로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-222">When you specify HTTP GET, the form data is passed in the URL as query strings, which enables users to bookmark the URL.</span></span> <span data-ttu-id="1e46b-223">[HTTP get 사용에 대 한 W3C 지침은](http://www.w3.org/2001/tag/doc/whenToUseGet.html) 동작으로 인해 업데이트가 발생 하지 않을 때 get을 사용 해야 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-223">The [W3C guidelines for the use of HTTP GET](http://www.w3.org/2001/tag/doc/whenToUseGet.html) recommend that you should use GET when the action does not result in an update.</span></span>

   <span data-ttu-id="1e46b-224">텍스트 상자는 현재 검색 문자열로 초기화 되므로 새 페이지를 클릭 하면 현재 검색 문자열을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-224">The text box is initialized with the current search string so when you click a new page you can see the current search string.</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml?highlight=1)]

   <span data-ttu-id="1e46b-225">열 머리글 링크는 쿼리 문자열을 사용하여 현재 검색 문자열을 컨트롤러에 전달하므로 사용자가 필터 결과 내에서 정렬할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-225">The column header links use the query string to pass the current search string to the controller so that the user can sort within filter results:</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1)]

   <span data-ttu-id="1e46b-226">현재 페이지와 총 페이지 수가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-226">The current page and total number of pages are displayed.</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]

   <span data-ttu-id="1e46b-227">표시할 페이지가 없으면 "0/0 페이지"가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-227">If there are no pages to display, "Page 0 of 0" is shown.</span></span> <span data-ttu-id="1e46b-228">이 경우 페이지 번호는가 1이 고 `Model.PageNumber` `Model.PageCount` 가 0 이므로 페이지 수는 페이지 수보다 큽니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-228">(In that case the page number is greater than the page count because `Model.PageNumber` is 1, and `Model.PageCount` is 0.)</span></span>

   <span data-ttu-id="1e46b-229">`PagedListPager` 도우미는 페이징 단추를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-229">The paging buttons are displayed by the `PagedListPager` helper:</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

   <span data-ttu-id="1e46b-230">도우미 `PagedListPager` 는 url 및 스타일을 포함 하 여 사용자 지정할 수 있는 다양 한 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-230">The `PagedListPager` helper provides a number of options that you can customize, including URLs and styling.</span></span> <span data-ttu-id="1e46b-231">자세한 내용은 GitHub 사이트에서 [TroyGoode/PagedList](https://github.com/TroyGoode/PagedList) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="1e46b-231">For more information, see [TroyGoode / PagedList](https://github.com/TroyGoode/PagedList) on the GitHub site.</span></span>

2. <span data-ttu-id="1e46b-232">페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-232">Run the page.</span></span>

   <span data-ttu-id="1e46b-233">다른 정렬 순서의 페이징 링크를 클릭하여 페이징이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-233">Click the paging links in different sort orders to make sure paging works.</span></span> <span data-ttu-id="1e46b-234">그런 다음, 검색 문자열을 입력하고 페이징을 다시 시도하여 정렬 및 필터링을 통해 페이징이 제대로 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-234">Then enter a search string and try paging again to verify that paging also works correctly with sorting and filtering.</span></span>

## <a name="create-an-about-page"></a><span data-ttu-id="1e46b-235">정보 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="1e46b-235">Create an About page</span></span>

<span data-ttu-id="1e46b-236">Contoso 대학 웹 사이트의 정보 페이지에서 각 등록 날짜에 대해 등록 한 학생 수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-236">For the Contoso University website's About page, you'll display how many students have enrolled for each enrollment date.</span></span> <span data-ttu-id="1e46b-237">여기에는 그룹화와 그룹에 대한 간단한 계산이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-237">This requires grouping and simple calculations on the groups.</span></span> <span data-ttu-id="1e46b-238">이 작업을 수행하기 위해 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-238">To accomplish this, you'll do the following:</span></span>

- <span data-ttu-id="1e46b-239">뷰에 전달해야 하는 데이터에 대해 뷰 모델 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-239">Create a view model class for the data that you need to pass to the view.</span></span>
- <span data-ttu-id="1e46b-240">컨트롤러에서 메서드를 `About` 수정 합니다. `Home`</span><span class="sxs-lookup"><span data-stu-id="1e46b-240">Modify the `About` method in the `Home` controller.</span></span>
- <span data-ttu-id="1e46b-241">뷰를 `About` 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-241">Modify the `About` view.</span></span>

### <a name="create-the-view-model"></a><span data-ttu-id="1e46b-242">뷰 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="1e46b-242">Create the View Model</span></span>

<span data-ttu-id="1e46b-243">프로젝트 폴더에 *Viewmodels* 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-243">Create a *ViewModels* folder in the project folder.</span></span> <span data-ttu-id="1e46b-244">해당 폴더에서 *EnrollmentDateGroup.cs* 클래스를 추가 하 고 템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-244">In that folder, add a class file *EnrollmentDateGroup.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a><span data-ttu-id="1e46b-245">홈 컨트롤러 수정</span><span class="sxs-lookup"><span data-stu-id="1e46b-245">Modify the Home Controller</span></span>

1. <span data-ttu-id="1e46b-246">*HomeController.cs*에서 파일 맨 위에 다음 `using` 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-246">In *HomeController.cs*, add the following `using` statements at the top of the file:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

2. <span data-ttu-id="1e46b-247">클래스에 대 한 여는 중괄호 바로 뒤에 데이터베이스 컨텍스트에 대 한 클래스 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-247">Add a class variable for the database context immediately after the opening curly brace for the class:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

3. <span data-ttu-id="1e46b-248">`About` 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-248">Replace the `About` method with the following code:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

   <span data-ttu-id="1e46b-249">LINQ 문은 등록 날짜별로 학생 엔터티를 그룹화하고 각 그룹의 엔터티 수를 계산하며 결과를 `EnrollmentDateGroup` 뷰 모델 개체의 컬렉션에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-249">The LINQ statement groups the student entities by enrollment date, calculates the number of entities in each group, and stores the results in a collection of `EnrollmentDateGroup` view model objects.</span></span>

4. <span data-ttu-id="1e46b-250">메서드를 `Dispose` 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-250">Add a `Dispose` method:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a><span data-ttu-id="1e46b-251">정보 뷰 수정</span><span class="sxs-lookup"><span data-stu-id="1e46b-251">Modify the About View</span></span>

1. <span data-ttu-id="1e46b-252">*Views\Home\About.cshtml* 파일의 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-252">Replace the code in the *Views\Home\About.cshtml* file with the following code:</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

2. <span data-ttu-id="1e46b-253">앱을 실행 하 고 **정보** 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-253">Run the app and click the **About** link.</span></span>

   <span data-ttu-id="1e46b-254">각 등록 날짜에 대 한 학생 수가 테이블에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-254">The count of students for each enrollment date displays in a table.</span></span>

   ![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="get-the-code"></a><span data-ttu-id="1e46b-256">코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="1e46b-256">Get the code</span></span>

[<span data-ttu-id="1e46b-257">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="1e46b-257">Download the Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="1e46b-258">추가 자료</span><span class="sxs-lookup"><span data-stu-id="1e46b-258">Additional resources</span></span>

<span data-ttu-id="1e46b-259">[ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)에서 다른 Entity Framework 리소스에 대 한 링크를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-259">Links to other Entity Framework resources can be found in [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e46b-260">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1e46b-260">Next steps</span></span>

<span data-ttu-id="1e46b-261">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="1e46b-261">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1e46b-262">열 정렬 링크 추가</span><span class="sxs-lookup"><span data-stu-id="1e46b-262">Add column sort links</span></span>
> * <span data-ttu-id="1e46b-263">검색 상자 추가</span><span class="sxs-lookup"><span data-stu-id="1e46b-263">Add a Search box</span></span>
> * <span data-ttu-id="1e46b-264">페이징 추가</span><span class="sxs-lookup"><span data-stu-id="1e46b-264">Add paging</span></span>
> * <span data-ttu-id="1e46b-265">정보 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="1e46b-265">Create an About page</span></span>

<span data-ttu-id="1e46b-266">다음 문서로 이동 하 여 연결 복원 력 및 명령 가로채기를 사용 하는 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="1e46b-266">Advance to the next article to learn how to use connection resiliency and command interception.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="1e46b-267">연결 복원 력 및 명령 가로채기</span><span class="sxs-lookup"><span data-stu-id="1e46b-267">Connection resiliency and command interception</span></span>](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)
