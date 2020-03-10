---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
title: Entity Framework 4.0 Database First 및 ASP.NET 4 Web Forms 시작-5 부 | Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 응용 프로그램 샘플은 ...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: 24ad4379-3fb2-44dc-ba59-85fe0ffcb2ae
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
msc.type: authoredcontent
ms.openlocfilehash: 75328e67abb4295b619cac5423a9eb970942fff7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78423869"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-5"></a><span data-ttu-id="a6b14-104">Entity Framework 4.0 Database First 및 ASP.NET 4 Web Forms 시작-5 부</span><span class="sxs-lookup"><span data-stu-id="a6b14-104">Getting Started with Entity Framework 4.0 Database First and ASP.NET 4 Web Forms - Part 5</span></span>

<span data-ttu-id="a6b14-105">만든 사람 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="a6b14-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="a6b14-106">Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 4.0 및 Visual Studio 2010를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-106">The Contoso University sample web application demonstrates how to create ASP.NET Web Forms applications using the Entity Framework 4.0 and Visual Studio 2010.</span></span> <span data-ttu-id="a6b14-107">자습서 시리즈에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](the-entity-framework-and-aspnet-getting-started-part-1.md) 를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a6b14-107">For information about the tutorial series, see [the first tutorial in the series](the-entity-framework-and-aspnet-getting-started-part-1.md)</span></span>

## <a name="working-with-related-data-continued"></a><span data-ttu-id="a6b14-108">관련 데이터 작업, 계속</span><span class="sxs-lookup"><span data-stu-id="a6b14-108">Working with Related Data, Continued</span></span>

<span data-ttu-id="a6b14-109">이전 자습서에서는 `EntityDataSource` 컨트롤을 사용 하 여 관련 데이터 작업을 시작 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-109">In the previous tutorial you began to use the `EntityDataSource` control to work with related data.</span></span> <span data-ttu-id="a6b14-110">탐색 속성에서 여러 수준의 계층 및 편집 된 데이터를 표시 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-110">You displayed multiple levels of hierarchy and edited data in navigation properties.</span></span> <span data-ttu-id="a6b14-111">이 자습서에서는 관계를 추가 및 삭제 하 고 기존 엔터티에 대 한 관계를 포함 하는 새 엔터티를 추가 하 여 관련 데이터를 계속 해 서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-111">In this tutorial you'll continue to work with related data by adding and deleting relationships and by adding a new entity that has a relationship to an existing entity.</span></span>

<span data-ttu-id="a6b14-112">부서에 할당 된 과정을 추가 하는 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-112">You'll create a page that adds courses that are assigned to departments.</span></span> <span data-ttu-id="a6b14-113">부서는 이미 존재 하 고 새 과정을 만들 때 동시에 기존 부서와 기존 부서 간의 관계를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-113">The departments already exist, and when you create a new course, at the same time you'll establish a relationship between it and an existing department.</span></span>

<span data-ttu-id="a6b14-114">[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a6b14-114">[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image1.png)</span></span>

<span data-ttu-id="a6b14-115">강의를 강좌에 할당 하 여 다 대 다 관계에서 작동 하는 페이지를 만들 수도 있습니다. (선택한 두 엔터티 간의 관계를 추가 하거나) 강좌에서 강사를 제거 합니다 (두 엔터티 간의 관계 제거 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-115">You'll also create a page that works with a many-to-many relationship by assigning an instructor to a course (adding a relationship between two entities that you select) or removing an instructor from a course (removing a relationship between two entities that you select).</span></span> <span data-ttu-id="a6b14-116">데이터베이스에서 강사와 강좌 간에 관계를 추가 하면 `CourseInstructor` 연결 테이블에 새 행이 추가 됩니다. 관계를 제거 하려면 `CourseInstructor` 연결 테이블에서 행을 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-116">In the database, adding a relationship between an instructor and a course results in a new row being added to the `CourseInstructor` association table; removing a relationship involves deleting a row from the `CourseInstructor` association table.</span></span> <span data-ttu-id="a6b14-117">그러나 `CourseInstructor` 테이블을 명시적으로 참조 하지 않고 탐색 속성을 설정 하 여 Entity Framework에서이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-117">However, you do this in the Entity Framework by setting navigation properties, without referring to the `CourseInstructor` table explicitly.</span></span>

<span data-ttu-id="a6b14-118">[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="a6b14-118">[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image3.png)</span></span>

## <a name="adding-an-entity-with-a-relationship-to-an-existing-entity"></a><span data-ttu-id="a6b14-119">관계를 사용 하 여 기존 엔터티에 엔터티 추가</span><span class="sxs-lookup"><span data-stu-id="a6b14-119">Adding an Entity with a Relationship to an Existing Entity</span></span>

<span data-ttu-id="a6b14-120">*Site.master* 마스터 페이지를 사용 하는 *CoursesAdd* 라는 새 웹 페이지를 만들고 `Content2`이라는 `Content` 컨트롤에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-120">Create a new web page named *CoursesAdd.aspx* that uses the *Site.Master* master page, and add the following markup to the `Content` control named `Content2`:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample1.aspx)]

<span data-ttu-id="a6b14-121">이 태그는 삽입을 가능 하 게 하 고 `Inserting` 이벤트에 대 한 처리기를 지정 하는 과정을 선택 하는 `EntityDataSource` 컨트롤을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-121">This markup creates an `EntityDataSource` control that selects courses, that enables inserting, and that specifies a handler for the `Inserting` event.</span></span> <span data-ttu-id="a6b14-122">새 `Course` 엔터티를 만들 때 처리기를 사용 하 여 `Department` 탐색 속성을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-122">You'll use the handler to update the `Department` navigation property when a new `Course` entity is created.</span></span>

<span data-ttu-id="a6b14-123">또한 태그는 새 `Course` 엔터티를 추가 하는 데 사용할 `DetailsView` 컨트롤을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-123">The markup also creates a `DetailsView` control to use for adding new `Course` entities.</span></span> <span data-ttu-id="a6b14-124">태그는 `Course` 엔터티 속성에 바인딩된 필드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-124">The markup uses bound fields for `Course` entity properties.</span></span> <span data-ttu-id="a6b14-125">시스템 생성 ID 필드가 아니기 때문에 `CourseID` 값을 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-125">You have to enter the `CourseID` value because this is not a system-generated ID field.</span></span> <span data-ttu-id="a6b14-126">대신 코스가 생성 될 때 수동으로 지정 해야 하는 과정 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-126">Instead, it's a course number that must be specified manually when the course is created.</span></span>

<span data-ttu-id="a6b14-127">탐색 속성은 `BoundField` 컨트롤과 함께 사용할 수 없으므로 `Department` 탐색 속성에 템플릿 필드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-127">You use a template field for the `Department` navigation property because navigation properties cannot be used with `BoundField` controls.</span></span> <span data-ttu-id="a6b14-128">템플릿 필드는 부서를 선택할 수 있는 드롭다운 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-128">The template field provides a drop-down list to select the department.</span></span> <span data-ttu-id="a6b14-129">드롭다운 목록은 `Bind`하는 대신 `Eval`를 사용 하 여 `Departments` 엔터티 집합에 바인딩되어 있습니다. 탐색 속성을 업데이트 하기 위해 직접 바인딩할 수 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-129">The drop-down list is bound to the `Departments` entity set by using `Eval` rather than `Bind`, again because you cannot directly bind navigation properties in order to update them.</span></span> <span data-ttu-id="a6b14-130">`DepartmentID` 외래 키를 업데이트 하는 코드에서 사용할 수 있도록 컨트롤에 대 한 참조를 저장할 수 있도록 `DropDownList` 컨트롤의 `Init` 이벤트에 대 한 처리기를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-130">You specify a handler for the `DropDownList` control's `Init` event so that you can store a reference to the control for use by the code that updates the `DepartmentID` foreign key.</span></span>

<span data-ttu-id="a6b14-131">Partial 클래스 선언 바로 뒤에 *CoursesAdd.aspx.cs* `DepartmentsDropDownList` 컨트롤에 대 한 참조를 보유 하는 클래스 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-131">In *CoursesAdd.aspx.cs* just after the partial-class declaration, add a class field to hold a reference to the `DepartmentsDropDownList` control:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample2.cs)]

<span data-ttu-id="a6b14-132">컨트롤에 대 한 참조를 저장할 수 있도록 `DepartmentsDropDownList` 컨트롤의 `Init` 이벤트에 대 한 처리기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-132">Add a handler for the `DepartmentsDropDownList` control's `Init` event so that you can store a reference to the control.</span></span> <span data-ttu-id="a6b14-133">이렇게 하면 사용자가 입력 한 값을 가져오고이를 사용 하 여 `Course` 엔터티의 `DepartmentID` 값을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-133">This lets you get the value the user has entered and use it to update the `DepartmentID` value of the `Course` entity.</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample3.cs)]

<span data-ttu-id="a6b14-134">`DetailsView` 컨트롤의 `Inserting` 이벤트에 대 한 처리기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-134">Add a handler for the `DetailsView` control's `Inserting` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample4.cs)]

<span data-ttu-id="a6b14-135">사용자가 `Insert`를 클릭 하면 새 레코드가 삽입 되기 전에 `Inserting` 이벤트가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-135">When the user clicks `Insert`, the `Inserting` event is raised before the new record is inserted.</span></span> <span data-ttu-id="a6b14-136">처리기의 코드는 `DropDownList` 컨트롤에서 `DepartmentID`를 가져오고이를 사용 하 여 `Course` 엔터티의 `DepartmentID` 속성에 사용 될 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-136">The code in the handler gets the `DepartmentID` from the `DropDownList` control and uses it to set the value that will be used for the `DepartmentID` property of the `Course` entity.</span></span>

<span data-ttu-id="a6b14-137">Entity Framework는이 과정을 관련 된 `Department` 엔터티의 `Courses` 탐색 속성에 추가 하는 과정을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-137">The Entity Framework will take care of adding this course to the `Courses` navigation property of the associated `Department` entity.</span></span> <span data-ttu-id="a6b14-138">또한 `Course` 엔터티의 `Department` 탐색 속성에 부서를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-138">It also adds the department to the `Department` navigation property of the `Course` entity.</span></span>

<span data-ttu-id="a6b14-139">페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-139">Run the page.</span></span>

<span data-ttu-id="a6b14-140">[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="a6b14-140">[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image5.png)</span></span>

<span data-ttu-id="a6b14-141">ID, 제목, 크레딧 수를 입력 하 고 부서를 선택한 다음 **삽입**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-141">Enter an ID, a title, a number of credits, and select a department, then click **Insert**.</span></span>

<span data-ttu-id="a6b14-142">*Default.aspx* 페이지를 실행 하 고 동일한 부서를 선택 하 여 새 강좌를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-142">Run the *Courses.aspx* page, and select the same department to see the new course.</span></span>

<span data-ttu-id="a6b14-143">[![Image03](the-entity-framework-and-aspnet-getting-started-part-5/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="a6b14-143">[![Image03](the-entity-framework-and-aspnet-getting-started-part-5/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image7.png)</span></span>

## <a name="working-with-many-to-many-relationships"></a><span data-ttu-id="a6b14-144">다 대 다 관계 작업</span><span class="sxs-lookup"><span data-stu-id="a6b14-144">Working with Many-to-Many Relationships</span></span>

<span data-ttu-id="a6b14-145">`Courses` 엔터티 집합과 `People` 엔터티 집합 간의 관계는 다 대 다 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-145">The relationship between the `Courses` entity set and the `People` entity set is a many-to-many relationship.</span></span> <span data-ttu-id="a6b14-146">`Course` 엔터티에는 `People` 이라는 탐색 속성이 있습니다 .이 속성에는 해당 과정을 설명 하기 위해 할당 된 강사를 나타내는 0 개 이상의 관련 된 `Person` 엔터티가 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-146">A `Course` entity has a navigation property named `People` that can contain zero, one, or more related `Person` entities (representing instructors assigned to teach that course).</span></span> <span data-ttu-id="a6b14-147">및 `Person` 엔터티에는 `Courses` 라는 탐색 속성이 있습니다 .이 속성은 0 개 이상의 관련 `Course` 엔터티 (강사가 학습에 할당 한 과정을 나타냄)를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-147">And a `Person` entity has a navigation property named `Courses` that can contain zero, one, or more related `Course` entities (representing courses that instructor is assigned to teach).</span></span> <span data-ttu-id="a6b14-148">한 강사는 여러 과정을 학습할 수 있으며, 한 강좌는 여러 강사가 배울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-148">One instructor might teach multiple courses, and one course might be taught by multiple instructors.</span></span> <span data-ttu-id="a6b14-149">이 연습 섹션에서는 관련 엔터티의 탐색 속성을 업데이트 하 여 `Person`와 `Course` 엔터티 간의 관계를 추가 하 고 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-149">In this section of the walkthrough, you'll add and remove relationships between `Person` and `Course` entities by updating the navigation properties of the related entities.</span></span>

<span data-ttu-id="a6b14-150">*Site.master* 마스터 페이지를 사용 하는 *InstructorsCourses* 라는 새 웹 페이지를 만들고 `Content2`이라는 `Content` 컨트롤에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-150">Create a new web page named *InstructorsCourses.aspx* that uses the *Site.Master* master page, and add the following markup to the `Content` control named `Content2`:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample5.aspx)]

<span data-ttu-id="a6b14-151">이 태그는 강사를 위한 `Person` 엔터티의 이름과 `PersonID`를 검색 하는 `EntityDataSource` 컨트롤을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-151">This markup creates an `EntityDataSource` control that retrieves the name and `PersonID` of `Person` entities for instructors.</span></span> <span data-ttu-id="a6b14-152">`DropDrownList` 컨트롤은 `EntityDataSource` 컨트롤에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-152">A `DropDrownList` control is bound to the `EntityDataSource` control.</span></span> <span data-ttu-id="a6b14-153">`DropDownList` 컨트롤은 `DataBound` 이벤트에 대 한 처리기를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-153">The `DropDownList` control specifies a handler for the `DataBound` event.</span></span> <span data-ttu-id="a6b14-154">이 처리기를 사용 하 여 코스를 표시 하는 두 개의 드롭다운 목록을 모두 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-154">You'll use this handler to databind the two drop-down lists that display courses.</span></span>

<span data-ttu-id="a6b14-155">태그는 또한 선택한 강사에 게 강좌를 할당 하는 데 사용할 다음 컨트롤 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-155">The markup also creates the following group of controls to use for assigning a course to the selected instructor:</span></span>

- <span data-ttu-id="a6b14-156">할당할 과정을 선택 하는 `DropDownList` 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-156">A `DropDownList` control for selecting a course to assign.</span></span> <span data-ttu-id="a6b14-157">이 컨트롤은 현재 선택한 강사에 게 할당 되지 않은 과정으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-157">This control will be populated with courses that are currently not assigned to the selected instructor.</span></span>
- <span data-ttu-id="a6b14-158">할당을 시작 하는 `Button` 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-158">A `Button` control to initiate the assignment.</span></span>
- <span data-ttu-id="a6b14-159">할당이 실패 하는 경우 오류 메시지를 표시 하는 `Label` 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-159">A `Label` control to display an error message if the assignment fails.</span></span>

<span data-ttu-id="a6b14-160">마지막으로, 태그는 선택한 강사 로부터 강좌를 제거 하는 데 사용할 컨트롤 그룹도 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-160">Finally, the markup also creates a group of controls to use for removing a course from the selected instructor.</span></span>

<span data-ttu-id="a6b14-161">*InstructorsCourses.aspx.cs*에서 using 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-161">In *InstructorsCourses.aspx.cs*, add a using statement:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample6.cs)]

<span data-ttu-id="a6b14-162">코스를 표시 하는 두 개의 드롭다운 목록을 채우는 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-162">Add a method for populating the two drop-down lists that display courses:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample7.cs)]

<span data-ttu-id="a6b14-163">이 코드는 `Courses` 엔터티 집합에서 모든 과정을 가져오고 선택한 강사에 대 한 `Person` 엔터티의 `Courses` 탐색 속성에서 과정을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-163">This code gets all courses from the `Courses` entity set and gets the courses from the `Courses` navigation property of the `Person` entity for the selected instructor.</span></span> <span data-ttu-id="a6b14-164">그런 다음 해당 강사에 게 할당 되는 과정을 결정 하 고 드롭다운 목록을 그에 따라 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-164">It then determines which courses are assigned to that instructor and populates the drop-down lists accordingly.</span></span>

<span data-ttu-id="a6b14-165">`Assign` 단추의 `Click` 이벤트에 대 한 처리기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-165">Add a handler for the `Assign` button's `Click` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample8.cs)]

<span data-ttu-id="a6b14-166">이 코드는 선택한 강사의 `Person` 엔터티를 가져오고, 선택한 강좌에 대 한 `Course` 엔터티를 가져오고, 강사의 `Person` 엔터티의 `Courses` 탐색 속성에 선택한 과정을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-166">This code gets the `Person` entity for the selected instructor, gets the `Course` entity for the selected course, and adds the selected course to the `Courses` navigation property of the instructor's `Person` entity.</span></span> <span data-ttu-id="a6b14-167">그런 다음 변경 내용을 데이터베이스에 저장 하 고 드롭다운 목록을 다시 채웁니다. 그러면 결과가 즉시 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-167">It then saves the changes to the database and repopulates the drop-down lists so the results can be seen immediately.</span></span>

<span data-ttu-id="a6b14-168">`Remove` 단추의 `Click` 이벤트에 대 한 처리기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-168">Add a handler for the `Remove` button's `Click` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample9.cs)]

<span data-ttu-id="a6b14-169">이 코드는 선택한 강사의 `Person` 엔터티를 가져오고, 선택한 강좌에 대 한 `Course` 엔터티를 가져오고, `Person` 엔터티의 `Courses` 탐색 속성에서 선택한 과정을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-169">This code gets the `Person` entity for the selected instructor, gets the `Course` entity for the selected course, and removes the selected course from the `Person` entity's `Courses` navigation property.</span></span> <span data-ttu-id="a6b14-170">그런 다음 변경 내용을 데이터베이스에 저장 하 고 드롭다운 목록을 다시 채웁니다. 그러면 결과가 즉시 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-170">It then saves the changes to the database and repopulates the drop-down lists so the results can be seen immediately.</span></span>

<span data-ttu-id="a6b14-171">보고할 오류가 없을 때 오류 메시지가 표시 되지 않도록 하는 `Page_Load` 메서드에 코드를 추가 하 고 `DataBound`에 대 한 처리기를 추가 하 고 강사 드롭다운 목록의 이벤트를 `SelectedIndexChanged` 하 여 강의 드롭다운 목록을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-171">Add code to the `Page_Load` method that makes sure the error messages are not visible when there's no error to report, and add handlers for the `DataBound` and `SelectedIndexChanged` events of the instructors drop-down list to populate the courses drop-down lists:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample10.cs)]

<span data-ttu-id="a6b14-172">페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-172">Run the page.</span></span>

<span data-ttu-id="a6b14-173">[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="a6b14-173">[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image9.png)</span></span>

<span data-ttu-id="a6b14-174">강사를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-174">Select an instructor.</span></span> <span data-ttu-id="a6b14-175"><strong>강좌 할당</strong> 드롭다운 목록에는 강사가 학습 하지 않는 코스가 표시 되 고 <strong>강좌 제거</strong> 드롭다운 목록에는 강사가 이미 할당 된 강좌가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-175">The <strong>Assign a Course</strong> drop-down list displays the courses that the instructor doesn't teach, and the <strong>Remove a Course</strong> drop-down list displays the courses that the instructor is already assigned to.</span></span> <span data-ttu-id="a6b14-176"><strong>과정 할당</strong> 섹션에서 과정을 선택한 다음 <strong>할당</strong>을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-176">In the <strong>Assign a Course</strong> section, select a course and then click <strong>Assign</strong>.</span></span> <span data-ttu-id="a6b14-177">강좌는 <strong>과정 제거</strong> 드롭다운 목록으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-177">The course moves to the <strong>Remove a Course</strong> drop-down list.</span></span> <span data-ttu-id="a6b14-178"><strong>강좌 제거</strong> 섹션에서 과정을 선택 하 고 <strong>제거</strong>를 클릭<em>합니다.</em></span><span class="sxs-lookup"><span data-stu-id="a6b14-178">Select a course in the <strong>Remove a Course</strong> section and click <strong>Remove</strong><em>.</em></span></span> <span data-ttu-id="a6b14-179">강좌는 <strong>과정 할당</strong> 드롭다운 목록으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-179">The course moves to the <strong>Assign a Course</strong> drop-down list.</span></span>

<span data-ttu-id="a6b14-180">이제 관련 데이터로 작업 하는 몇 가지 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-180">You have now seen some more ways to work with related data.</span></span> <span data-ttu-id="a6b14-181">다음 자습서에서는 데이터 모델에서 상속을 사용 하 여 응용 프로그램의 유지 관리를 개선 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="a6b14-181">In the following tutorial, you'll learn how to use inheritance in the data model to improve the maintainability of your application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a6b14-182">[이전](the-entity-framework-and-aspnet-getting-started-part-4.md)
> [다음](the-entity-framework-and-aspnet-getting-started-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="a6b14-182">[Previous](the-entity-framework-and-aspnet-getting-started-part-4.md)
[Next](the-entity-framework-and-aspnet-getting-started-part-6.md)</span></span>
