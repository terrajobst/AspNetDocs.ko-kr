---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
title: 'Entity Framework 4.0 및 ObjectDataSource 컨트롤 사용, 3 부: 정렬 및 필터링 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈는 Entity Framework 4.0 자습서 시리즈 시작에서 만든 Contoso 대학 웹 응용 프로그램을 기반으로 합니다. I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 2990bd10-590d-43d5-9529-6b503ce5455d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
msc.type: authoredcontent
ms.openlocfilehash: 603120864528b9a5ff81214270eb9a7f1b68b347
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78512717"
---
# <a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-3-sorting-and-filtering"></a><span data-ttu-id="cf744-104">Entity Framework 4.0 및 ObjectDataSource 컨트롤 사용, 3 부: 정렬 및 필터링</span><span class="sxs-lookup"><span data-stu-id="cf744-104">Using the Entity Framework 4.0 and the ObjectDataSource Control, Part 3: Sorting and Filtering</span></span>

<span data-ttu-id="cf744-105">만든 사람 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="cf744-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="cf744-106">이 자습서 시리즈는 [Entity Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started) 자습서 시리즈 시작에서 만든 Contoso 대학 웹 응용 프로그램을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-106">This tutorial series builds on the Contoso University web application that is created by the [Getting Started with the Entity Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started) tutorial series.</span></span> <span data-ttu-id="cf744-107">이전 자습서를 완료 하지 않은 경우이 자습서의 시작 점으로, 만든 [응용 프로그램을 다운로드할](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-107">If you didn't complete the earlier tutorials, as a starting point for this tutorial you can [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) that you would have created.</span></span> <span data-ttu-id="cf744-108">전체 자습서 시리즈에서 만든 [응용 프로그램을 다운로드할](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-108">You can also [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) that is created by the complete tutorial series.</span></span> <span data-ttu-id="cf744-109">자습서에 대 한 질문이 있는 경우 [ASP.NET Entity Framework 포럼](https://forums.asp.net/1227.aspx)에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-109">If you have questions about the tutorials, you can post them to the [ASP.NET Entity Framework forum](https://forums.asp.net/1227.aspx).</span></span>

<span data-ttu-id="cf744-110">이전 자습서에서는 Entity Framework 및 `ObjectDataSource` 컨트롤을 사용 하는 n 계층 웹 응용 프로그램에서 리포지토리 패턴을 구현 했습니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-110">In the previous tutorial you implemented the repository pattern in an n-tier web application that uses the Entity Framework and the `ObjectDataSource` control.</span></span> <span data-ttu-id="cf744-111">이 자습서에서는 마스터-세부 시나리오를 정렬 및 필터링 하 고 처리 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-111">This tutorial shows how to do sorting and filtering and handle master-detail scenarios.</span></span> <span data-ttu-id="cf744-112">다음과 같은 향상 된 기능을 *학과 페이지에 추가 합니다.*</span><span class="sxs-lookup"><span data-stu-id="cf744-112">You'll add the following enhancements to the *Departments.aspx* page:</span></span>

- <span data-ttu-id="cf744-113">사용자가 이름을 기준으로 부서를 선택할 수 있는 입력란입니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-113">A text box to allow users to select departments by name.</span></span>
- <span data-ttu-id="cf744-114">표에 표시 된 각 학과의 과정 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-114">A list of courses for each department that's shown in the grid.</span></span>
- <span data-ttu-id="cf744-115">열 머리글을 클릭 하 여 정렬할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-115">The ability to sort by clicking column headings.</span></span>

<span data-ttu-id="cf744-116">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="cf744-116">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)</span></span>

## <a name="adding-the-ability-to-sort-gridview-columns"></a><span data-ttu-id="cf744-117">GridView 열을 정렬 하는 기능 추가</span><span class="sxs-lookup"><span data-stu-id="cf744-117">Adding the Ability to Sort GridView Columns</span></span>

<span data-ttu-id="cf744-118">학과 페이지 *를* 열고 `DepartmentsObjectDataSource`이라는 `ObjectDataSource` 컨트롤에 `SortParameterName="sortExpression"` 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-118">Open the *Departments.aspx* page and add a `SortParameterName="sortExpression"` attribute to the `ObjectDataSource` control named `DepartmentsObjectDataSource`.</span></span> <span data-ttu-id="cf744-119">나중에 `sortExpression`이라는 매개 변수를 사용 하는 `GetDepartments` 메서드를 만듭니다. 이제 컨트롤의 여는 태그에 대 한 태그는 다음 예제와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-119">(Later you'll create a `GetDepartments` method that takes a parameter named `sortExpression`.) The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample1.aspx)]

<span data-ttu-id="cf744-120">`GridView` 컨트롤의 여는 태그에 `AllowSorting="true"` 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-120">Add the `AllowSorting="true"` attribute to the opening tag of the `GridView` control.</span></span> <span data-ttu-id="cf744-121">이제 컨트롤의 여는 태그에 대 한 태그는 다음 예제와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-121">The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample2.aspx)]

<span data-ttu-id="cf744-122">*Departments.aspx.cs*에서 `Page_Load` 메서드에서 `GridView` 컨트롤의 `Sort` 메서드를 호출 하 여 기본 정렬 순서를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-122">In *Departments.aspx.cs*, set the default sort order by calling the `GridView` control's `Sort` method from the `Page_Load` method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample3.cs)]

<span data-ttu-id="cf744-123">비즈니스 논리 클래스 또는 리포지토리 클래스에서 또는 필터를 정렬 하는 코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-123">You can add code that sorts or filters in either the business logic class or the repository class.</span></span> <span data-ttu-id="cf744-124">비즈니스 논리 클래스에서 수행 하는 경우 데이터를 데이터베이스에서 검색 한 후 정렬 또는 필터링 작업이 수행 됩니다. 비즈니스 논리 클래스가 리포지토리에서 반환 된 `IEnumerable` 개체를 사용 하 고 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-124">If you do it in the business logic class, the sorting or filtering work will be done after the data is retrieved from the database, because the business logic class is working with an `IEnumerable` object returned by the repository.</span></span> <span data-ttu-id="cf744-125">리포지토리 클래스에서 정렬 및 필터링 코드를 추가 하 고 LINQ 식 또는 개체 쿼리가 `IEnumerable` 개체로 변환 되기 전에 수행 하는 경우, 처리를 위해 명령이 데이터베이스로 전달 되며이는 일반적으로 더 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-125">If you add sorting and filtering code in the repository class and you do it before a LINQ expression or object query has been converted to an `IEnumerable` object, your commands will be passed through to the database for processing, which is typically more efficient.</span></span> <span data-ttu-id="cf744-126">이 자습서에서는 데이터베이스에서 처리를 수행 하는 방식으로 (즉, 리포지토리에서) 정렬과 필터링을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-126">In this tutorial you'll implement sorting and filtering in a way that causes the processing to be done by the database — that is, in the repository.</span></span>

<span data-ttu-id="cf744-127">정렬 기능을 추가 하려면 리포지토리 인터페이스 및 리포지토리 클래스 뿐만 아니라 비즈니스 논리 클래스에 새 메서드를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-127">To add sorting capability, you must add a new method to the repository interface and repository classes as well as to the business logic class.</span></span> <span data-ttu-id="cf744-128">*ISchoolRepository.cs* 파일에서 반환 되는 부서 목록을 정렬 하는 데 사용 되는 `sortExpression` 매개 변수를 사용 하는 새 `GetDepartments` 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-128">In the *ISchoolRepository.cs* file, add a new `GetDepartments` method that takes a `sortExpression` parameter that will be used to sort the list of departments that's returned:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample4.cs)]

<span data-ttu-id="cf744-129">`sortExpression` 매개 변수는 정렬 기준이 되는 열과 정렬 방향을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-129">The `sortExpression` parameter will specify the column to sort on and the sort direction.</span></span>

<span data-ttu-id="cf744-130">새 메서드에 대 한 코드를 *SchoolRepository.cs* 파일에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-130">Add code for the new method to the *SchoolRepository.cs* file:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample5.cs)]

<span data-ttu-id="cf744-131">매개 변수가 없는 기존 `GetDepartments` 메서드를 변경 하 여 새 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-131">Change the existing parameterless `GetDepartments` method to call the new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample6.cs)]

<span data-ttu-id="cf744-132">테스트 프로젝트에서 *MockSchoolRepository.cs*에 다음 새 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-132">In the test project, add the following new method to *MockSchoolRepository.cs*:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample7.cs)]

<span data-ttu-id="cf744-133">정렬 된 목록을 반환 하는이 메서드에 종속 된 단위 테스트를 만들려는 경우에는 반환 하기 전에 목록을 정렬 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-133">If you were going to create any unit tests that depended on this method returning a sorted list, you would need to sort the list before returning it.</span></span> <span data-ttu-id="cf744-134">이 자습서에서와 같은 테스트를 만들 수 없으므로 메서드는 정렬 되지 않은 부서 목록만 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-134">You won't be creating tests like that in this tutorial, so the method can just return the unsorted list of departments.</span></span>

<span data-ttu-id="cf744-135">*SchoolBL.cs* 파일에서 비즈니스 논리 클래스에 다음과 같은 새 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-135">In the *SchoolBL.cs* file, add the following new method to the business logic class:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample8.cs)]

<span data-ttu-id="cf744-136">이 코드는 sort 매개 변수를 리포지토리 메서드에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-136">This code passes the sort parameter to the repository method.</span></span>

<span data-ttu-id="cf744-137">*부서 .aspx* 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-137">Run the *Departments.aspx* page.</span></span>

<span data-ttu-id="cf744-138">[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="cf744-138">[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)</span></span>

<span data-ttu-id="cf744-139">이제 열 머리글을 클릭 하 여 해당 열을 기준으로 정렬할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-139">You can now click any column heading to sort by that column.</span></span> <span data-ttu-id="cf744-140">열이 이미 정렬 된 경우 머리글을 클릭 하면 정렬 방향이 반전 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-140">If the column is already sorted, clicking the heading reverses the sort direction.</span></span>

## <a name="adding-a-search-box"></a><span data-ttu-id="cf744-141">검색 상자 추가</span><span class="sxs-lookup"><span data-stu-id="cf744-141">Adding a Search Box</span></span>

<span data-ttu-id="cf744-142">이 섹션에서는 검색 텍스트 상자를 추가 하 고, 컨트롤 매개 변수를 사용 하 여 `ObjectDataSource` 컨트롤에 연결 하 고, 필터링을 지원 하기 위해 비즈니스 논리 클래스에 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-142">In this section you'll add a search text box, link it to the `ObjectDataSource` control using a control parameter, and add a method to the business logic class to support filtering.</span></span>

<span data-ttu-id="cf744-143">학과 페이지 *를* 열고 머리글과 첫 번째 `ObjectDataSource` 컨트롤 사이에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-143">Open the *Departments.aspx* page and add the following markup between the heading and the first `ObjectDataSource` control:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample9.aspx)]

<span data-ttu-id="cf744-144">`DepartmentsObjectDataSource`이라는 `ObjectDataSource` 컨트롤에서 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-144">In the `ObjectDataSource` control named `DepartmentsObjectDataSource`, do the following:</span></span>

- <span data-ttu-id="cf744-145">`SearchTextBox` 컨트롤에 입력 한 값을 가져오는 `nameSearchString` 이라는 매개 변수에 대 한 `SelectParameters` 요소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-145">Add a `SelectParameters` element for a parameter named `nameSearchString` that gets the value entered in the `SearchTextBox` control.</span></span>
- <span data-ttu-id="cf744-146">`SelectMethod` 특성 값을 `GetDepartmentsByName`로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-146">Change the `SelectMethod` attribute value to `GetDepartmentsByName`.</span></span> <span data-ttu-id="cf744-147">이 메서드는 나중에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-147">(You'll create this method later.)</span></span>

<span data-ttu-id="cf744-148">이제 `ObjectDataSource` 컨트롤의 태그는 다음 예제와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-148">The markup for the `ObjectDataSource` control now resembles the following example:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample10.aspx)]

<span data-ttu-id="cf744-149">*ISchoolRepository.cs*에서 `sortExpression` 및 `nameSearchString` 매개 변수를 모두 사용 하는 `GetDepartmentsByName` 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-149">In *ISchoolRepository.cs*, add a `GetDepartmentsByName` method that takes both `sortExpression` and `nameSearchString` parameters:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample11.cs)]

<span data-ttu-id="cf744-150">*SchoolRepository.cs*에 다음과 같은 새 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-150">In *SchoolRepository.cs*, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample12.cs)]

<span data-ttu-id="cf744-151">이 코드는 `Where` 메서드를 사용 하 여 검색 문자열이 포함 된 항목을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-151">This code uses a `Where` method to select items that contain the search string.</span></span> <span data-ttu-id="cf744-152">검색 문자열이 비어 있으면 모든 레코드가 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-152">If the search string is empty, all records will be selected.</span></span> <span data-ttu-id="cf744-153">예 `Where``OrderBy`를 들어`Include`와 같은 한 문에 메서드 호출을 함께 지정 하는 경우 `Where` 메서드는 항상 마지막 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-153">Note that when you specify method calls together in one statement like this (`Include`, then `OrderBy`, then `Where`), the `Where` method must always be last.</span></span>

<span data-ttu-id="cf744-154">`sortExpression` 매개 변수를 사용 하 여 새 메서드를 호출 하는 기존 `GetDepartments` 메서드를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-154">Change the existing `GetDepartments` method that takes a `sortExpression` parameter to call the new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample13.cs)]

<span data-ttu-id="cf744-155">테스트 프로젝트의 *MockSchoolRepository.cs* 에 다음과 같은 새 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-155">In *MockSchoolRepository.cs* in the test project, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample14.cs)]

<span data-ttu-id="cf744-156">*SchoolBL.cs*에 다음과 같은 새 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-156">In *SchoolBL.cs*, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample15.cs)]

<span data-ttu-id="cf744-157">학과 페이지 *를* 실행 하 고 검색 문자열을 입력 하 여 선택 논리가 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-157">Run the *Departments.aspx* page and enter a search string to make sure that the selection logic works.</span></span> <span data-ttu-id="cf744-158">텍스트 상자를 비워 두고 검색을 시도 하 여 모든 레코드가 반환 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-158">Leave the text box empty and try a search to make sure that all records are returned.</span></span>

<span data-ttu-id="cf744-159">[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="cf744-159">[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)</span></span>

## <a name="adding-a-details-column-for-each-grid-row"></a><span data-ttu-id="cf744-160">각 표 형태 창의 행에 대 한 세부 정보 열 추가</span><span class="sxs-lookup"><span data-stu-id="cf744-160">Adding a Details Column for Each Grid Row</span></span>

<span data-ttu-id="cf744-161">다음으로 표의 오른쪽 셀에 표시 되는 각 학과의 모든 과정을 확인 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-161">Next, you want to see all of the courses for each department displayed in the right-hand cell of the grid.</span></span> <span data-ttu-id="cf744-162">이렇게 하려면 중첩 된 `GridView` 컨트롤을 사용 하 고이를 `Department` 엔터티의 `Courses` 탐색 속성의 데이터에 데이터 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-162">To do this, you'll use a nested `GridView` control and databind it to data from the `Courses` navigation property of the `Department` entity.</span></span>

<span data-ttu-id="cf744-163">학과 *.aspx* 를 열고 `GridView` 컨트롤에 대 한 태그에서 `RowDataBound` 이벤트에 대 한 처리기를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-163">Open *Departments.aspx* and in the markup for the `GridView` control, specify a handler for the `RowDataBound` event.</span></span> <span data-ttu-id="cf744-164">이제 컨트롤의 여는 태그에 대 한 태그는 다음 예제와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-164">The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample16.aspx)]

<span data-ttu-id="cf744-165">`Administrator` 템플릿 필드 뒤에 새 `TemplateField` 요소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-165">Add a new `TemplateField` element after the `Administrator` template field:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample17.aspx)]

<span data-ttu-id="cf744-166">이 태그는 과정 번호와 코스 목록의 제목을 표시 하는 중첩 된 `GridView` 컨트롤을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-166">This markup creates a nested `GridView` control that shows the course number and title of a list of courses.</span></span> <span data-ttu-id="cf744-167">`RowDataBound` 처리기에서 코드에 데이터를 바인딩할 수 있기 때문에 데이터 소스를 지정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-167">It does not specify a data source because you'll databind it in code in the `RowDataBound` handler.</span></span>

<span data-ttu-id="cf744-168">*Departments.aspx.cs* 를 열고 `RowDataBound` 이벤트에 대 한 다음 처리기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-168">Open *Departments.aspx.cs* and add the following handler for the `RowDataBound` event:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample18.cs)]

<span data-ttu-id="cf744-169">이 코드는 이벤트 인수에서 `Department` 엔터티를 가져오고 `Courses` 탐색 속성을 `List` 컬렉션으로 변환한 다음 중첩 된 `GridView`를 컬렉션에 열의.</span><span class="sxs-lookup"><span data-stu-id="cf744-169">This code gets the `Department` entity from the event arguments, converts the `Courses` navigation property to a `List` collection, and databinds the nested `GridView` to the collection.</span></span>

<span data-ttu-id="cf744-170">*SchoolRepository.cs* 파일을 열고 `GetDepartmentsByName` 메서드에서 만든 개체 쿼리에서 `Include` 메서드를 호출 하 여 `Courses` 탐색 속성에 대해 즉시 로드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-170">Open the *SchoolRepository.cs* file and specify eager loading for the `Courses` navigation property by calling the `Include` method in the object query that you create in the `GetDepartmentsByName` method.</span></span> <span data-ttu-id="cf744-171">이제 `GetDepartmentsByName` 메서드의 `return` 문은 다음 예제와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-171">The `return` statement in the `GetDepartmentsByName` method now resembles the following example.</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample19.cs)]

<span data-ttu-id="cf744-172">페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-172">Run the page.</span></span> <span data-ttu-id="cf744-173">이전에 추가한 정렬 및 필터링 기능 외에도 GridView 컨트롤에는 각 부서에 대 한 중첩 된 과정 세부 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-173">In addition to the sorting and filtering capability that you added earlier, the GridView control now shows nested course details for each department.</span></span>

<span data-ttu-id="cf744-174">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="cf744-174">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)</span></span>

<span data-ttu-id="cf744-175">이렇게 하면 정렬, 필터링 및 마스터-세부 시나리오에 대 한 소개를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-175">This completes the introduction to sorting, filtering, and master-detail scenarios.</span></span> <span data-ttu-id="cf744-176">다음 자습서에서는 동시성을 처리 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cf744-176">In the next tutorial, you'll see how to handle concurrency.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="cf744-177">[이전](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
> [다음](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)</span><span class="sxs-lookup"><span data-stu-id="cf744-177">[Previous](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
[Next](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)</span></span>
