---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
title: Entity Framework 4.0 Database First 및 ASP.NET 4 Web Forms 시작-4 부 | Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 응용 프로그램 샘플은 ...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: ceb9e60f-957c-4d25-9331-cc527de96a33
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
msc.type: authoredcontent
ms.openlocfilehash: eb75a76038466bf30738387ed4739687de1df944
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518285"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-4"></a><span data-ttu-id="dde2e-104">Entity Framework 4.0 Database First 및 ASP.NET 4 Web Forms 시작-4 부</span><span class="sxs-lookup"><span data-stu-id="dde2e-104">Getting Started with Entity Framework 4.0 Database First and ASP.NET 4 Web Forms - Part 4</span></span>

<span data-ttu-id="dde2e-105">만든 사람 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="dde2e-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="dde2e-106">Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 4.0 및 Visual Studio 2010를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-106">The Contoso University sample web application demonstrates how to create ASP.NET Web Forms applications using the Entity Framework 4.0 and Visual Studio 2010.</span></span> <span data-ttu-id="dde2e-107">자습서 시리즈에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](the-entity-framework-and-aspnet-getting-started-part-1.md) 를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="dde2e-107">For information about the tutorial series, see [the first tutorial in the series](the-entity-framework-and-aspnet-getting-started-part-1.md)</span></span>

## <a name="working-with-related-data"></a><span data-ttu-id="dde2e-108">관련 데이터 작업</span><span class="sxs-lookup"><span data-stu-id="dde2e-108">Working with Related Data</span></span>

<span data-ttu-id="dde2e-109">이전 자습서에서는 데이터를 필터링, 정렬 및 그룹화 하는 `EntityDataSource` 컨트롤을 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-109">In the previous tutorial you used the `EntityDataSource` control to filter, sort, and group data.</span></span> <span data-ttu-id="dde2e-110">이 자습서에서는 관련 데이터를 표시 하 고 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-110">In this tutorial you'll display and update related data.</span></span>

<span data-ttu-id="dde2e-111">강사 목록을 보여 주는 강사 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-111">You'll create the Instructors page that shows a list of instructors.</span></span> <span data-ttu-id="dde2e-112">강사를 선택 하면 해당 강사가 학습 한 과정의 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-112">When you select an instructor, you see a list of courses taught by that instructor.</span></span> <span data-ttu-id="dde2e-113">강좌를 선택 하면 과정에 대 한 세부 정보와 강좌에 등록 된 학생 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-113">When you select a course, you see details for the course and a list of students enrolled in the course.</span></span> <span data-ttu-id="dde2e-114">강사 이름, 채용 날짜 및 사무실 할당을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-114">You can edit the instructor name, hire date, and office assignment.</span></span> <span data-ttu-id="dde2e-115">사무실 할당은 탐색 속성을 통해 액세스 하는 별도의 엔터티 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-115">The office assignment is a separate entity set that you access through a navigation property.</span></span>

<span data-ttu-id="dde2e-116">태그 또는 코드에서 마스터 데이터를 정보 데이터에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-116">You can link master data to detail data in markup or in code.</span></span> <span data-ttu-id="dde2e-117">자습서의이 부분에서는 두 가지 방법을 모두 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-117">In this part of the tutorial, you'll use both methods.</span></span>

<span data-ttu-id="dde2e-118">[![Image01](the-entity-framework-and-aspnet-getting-started-part-4/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="dde2e-118">[![Image01](the-entity-framework-and-aspnet-getting-started-part-4/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image1.png)</span></span>

## <a name="displaying-and-updating-related-entities-in-a-gridview-control"></a><span data-ttu-id="dde2e-119">GridView 컨트롤에서 관련 엔터티 표시 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="dde2e-119">Displaying and Updating Related Entities in a GridView Control</span></span>

<span data-ttu-id="dde2e-120">*Site.master* 마스터 페이지를 사용 하는 *강사 .aspx* 라는 새 웹 페이지를 만들고 `Content2`이라는 `Content` 컨트롤에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-120">Create a new web page named *Instructors.aspx* that uses the *Site.Master* master page, and add the following markup to the `Content` control named `Content2`:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample1.aspx)]

<span data-ttu-id="dde2e-121">이 태그는 강사를 선택 하 고 업데이트를 사용 하도록 설정 하는 `EntityDataSource` 컨트롤을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-121">This markup creates an `EntityDataSource` control that selects instructors and enables updates.</span></span> <span data-ttu-id="dde2e-122">`div` 요소는 왼쪽에 렌더링할 태그를 구성 하므로 나중에 열을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-122">The `div` element configures markup to render on the left so that you can add a column on the right later.</span></span>

<span data-ttu-id="dde2e-123">`EntityDataSource` 태그와 closing `</div>` 태그 사이에 오류 메시지에 사용할 `GridView` 컨트롤 및 `Label` 컨트롤을 만드는 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-123">Between the `EntityDataSource` markup and the closing `</div>` tag, add the following markup that creates a `GridView` control and a `Label` control that you'll use for error messages:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample2.aspx)]

<span data-ttu-id="dde2e-124">이 `GridView` 컨트롤은 행 선택을 가능 하 게 하 고, 선택한 행을 밝은 회색 배경색으로 강조 표시 하 고, `SelectedIndexChanged` 및 `Updating` 이벤트에 대해 나중에 만들 처리기를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-124">This `GridView` control enables row selection, highlights the selected row with a light gray background color, and specifies handlers (which you'll create later) for the `SelectedIndexChanged` and `Updating` events.</span></span> <span data-ttu-id="dde2e-125">또한 선택한 행의 키 값을 나중에 추가할 다른 컨트롤에 전달할 수 있도록 `DataKeyNames` 속성에 대 한 `PersonID`를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-125">It also specifies `PersonID` for the `DataKeyNames` property, so that the key value of the selected row can be passed to another control that you'll add later.</span></span>

<span data-ttu-id="dde2e-126">마지막 열에는 연결 된 엔터티에서 제공 되기 때문에 `Person` 엔터티의 탐색 속성에 저장 되는 강사의 사무실 할당이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-126">The last column contains the instructor's office assignment, which is stored in a navigation property of the `Person` entity because it comes from an associated entity.</span></span> <span data-ttu-id="dde2e-127">`GridView` 컨트롤이 업데이트를 위해 탐색 속성에 직접 바인딩할 수 없기 때문에 `EditItemTemplate` 요소는 `Bind`대신 `Eval`를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-127">Notice that the `EditItemTemplate` element specifies `Eval` instead of `Bind`, because the `GridView` control cannot directly bind to navigation properties in order to update them.</span></span> <span data-ttu-id="dde2e-128">코드에서 office 할당을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-128">You'll update the office assignment in code.</span></span> <span data-ttu-id="dde2e-129">이렇게 하려면 `TextBox` 컨트롤에 대 한 참조가 필요 하며, `TextBox` 컨트롤의 `Init` 이벤트에서 가져오고 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-129">To do that, you'll need a reference to the `TextBox` control, and you'll get and save that in the `TextBox` control's `Init` event.</span></span>

<span data-ttu-id="dde2e-130">`GridView` 컨트롤 다음에는 오류 메시지에 사용 되는 `Label` 컨트롤이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-130">Following the `GridView` control is a `Label` control that's used for error messages.</span></span> <span data-ttu-id="dde2e-131">컨트롤의 `Visible` 속성이 `false`되 고 뷰 상태가 해제 되어 코드에서 오류에 대 한 응답으로 표시 되는 경우에만 레이블이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-131">The control's `Visible` property is `false`, and view state is turned off, so that the label will appear only when code makes it visible in response to an error.</span></span>

<span data-ttu-id="dde2e-132">*Instructors.aspx.cs* 파일을 열고 다음 `using` 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-132">Open the *Instructors.aspx.cs* file and add the following `using` statement:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample3.cs)]

<span data-ttu-id="dde2e-133">부분 클래스 이름 선언 바로 뒤에 개인 클래스 필드를 추가 하 여 office 할당 텍스트 상자에 대 한 참조를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-133">Add a private class field immediately after the partial-class name declaration to hold a reference to the office assignment text box.</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample4.cs)]

<span data-ttu-id="dde2e-134">나중에 코드를 추가할 `SelectedIndexChanged` 이벤트 처리기에 대 한 스텁을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-134">Add a stub for the `SelectedIndexChanged` event handler that you'll add code for later.</span></span> <span data-ttu-id="dde2e-135">또한 `TextBox` 컨트롤에 대 한 참조를 저장할 수 있도록 office 할당 `TextBox` 컨트롤의 `Init` 이벤트에 대 한 처리기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-135">Also add a handler for the office assignment `TextBox` control's `Init` event so that you can store a reference to the `TextBox` control.</span></span> <span data-ttu-id="dde2e-136">이 참조를 사용 하 여 탐색 속성과 연결 된 엔터티를 업데이트 하기 위해 사용자가 입력 한 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-136">You'll use this reference to get the value the user entered in order to update the entity associated with the navigation property.</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample5.cs)]

<span data-ttu-id="dde2e-137">`GridView` 컨트롤의 `Updating` 이벤트를 사용 하 여 연결 된 `OfficeAssignment` 엔터티의 `Location` 속성을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-137">You'll use the `GridView` control's `Updating` event to update the `Location` property of the associated `OfficeAssignment` entity.</span></span> <span data-ttu-id="dde2e-138">`Updating` 이벤트에 대 한 다음 처리기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-138">Add the following handler for the `Updating` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample6.cs)]

<span data-ttu-id="dde2e-139">이 코드는 사용자가 `GridView` 행에서 **업데이트** 를 클릭 하면 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-139">This code is run when the user clicks **Update** in a `GridView` row.</span></span> <span data-ttu-id="dde2e-140">이 코드는 LINQ to Entities를 사용 하 여 이벤트 인수에서 선택한 행의 `PersonID`를 사용 하 여 현재 `Person` 엔터티와 연결 된 `OfficeAssignment` 엔터티를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-140">The code uses LINQ to Entities to retrieve the `OfficeAssignment` entity that's associated with the current `Person` entity, using the `PersonID` of the selected row from the event argument.</span></span>

<span data-ttu-id="dde2e-141">그런 다음 `InstructorOfficeTextBox` 컨트롤의 값에 따라 코드에서 다음 작업 중 하나를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-141">The code then takes one of the following actions depending on the value in the `InstructorOfficeTextBox` control:</span></span>

- <span data-ttu-id="dde2e-142">텍스트 상자에 값이 있고 업데이트할 `OfficeAssignment` 엔터티가 없으면 하나를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-142">If the text box has a value and there's no `OfficeAssignment` entity to update, it creates one.</span></span>
- <span data-ttu-id="dde2e-143">입력란에 값이 있고 `OfficeAssignment` 엔터티가 있으면 `Location` 속성 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-143">If the text box has a value and there's an `OfficeAssignment` entity, it updates the `Location` property value.</span></span>
- <span data-ttu-id="dde2e-144">입력란이 비어 있고 `OfficeAssignment` 엔터티가 있으면 해당 엔터티를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-144">If the text box is empty and an `OfficeAssignment` entity exists, it deletes the entity.</span></span>

<span data-ttu-id="dde2e-145">그 후에는 변경 내용을 데이터베이스에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-145">After this, it saves the changes to the database.</span></span> <span data-ttu-id="dde2e-146">예외가 발생 하면 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-146">If an exception occurs, it displays an error message.</span></span>

<span data-ttu-id="dde2e-147">페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-147">Run the page.</span></span>

<span data-ttu-id="dde2e-148">[![Image02](the-entity-framework-and-aspnet-getting-started-part-4/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="dde2e-148">[![Image02](the-entity-framework-and-aspnet-getting-started-part-4/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image3.png)</span></span>

<span data-ttu-id="dde2e-149">**편집** 을 클릭 하면 모든 필드가 텍스트 상자로 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-149">Click **Edit** and all fields change to text boxes.</span></span>

<span data-ttu-id="dde2e-150">[![Image03](the-entity-framework-and-aspnet-getting-started-part-4/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="dde2e-150">[![Image03](the-entity-framework-and-aspnet-getting-started-part-4/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image5.png)</span></span>

<span data-ttu-id="dde2e-151">**사무실 할당**을 포함 하 여 이러한 값을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-151">Change any of these values, including **Office Assignment**.</span></span> <span data-ttu-id="dde2e-152">**업데이트** 를 클릭 하면 목록에 반영 된 변경 내용이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-152">Click **Update** and you'll see the changes reflected in the list.</span></span>

## <a name="displaying-related-entities-in-a-separate-control"></a><span data-ttu-id="dde2e-153">별도의 컨트롤에 관련 엔터티 표시</span><span class="sxs-lookup"><span data-stu-id="dde2e-153">Displaying Related Entities in a Separate Control</span></span>

<span data-ttu-id="dde2e-154">각 강사는 하나 이상의 과정을 학습할 수 있으므로 강사 `GridView` 컨트롤에서 선택한 강사와 관련 된 과정을 나열 하는 `EntityDataSource` 컨트롤과 `GridView` 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-154">Each instructor can teach one or more courses, so you'll add an `EntityDataSource` control and a `GridView` control to list the courses associated with whichever instructor is selected in the instructors `GridView` control.</span></span> <span data-ttu-id="dde2e-155">코스 엔터티에 대 한 머리글 및 `EntityDataSource` 컨트롤을 만들려면 오류 메시지 `Label` 컨트롤과 닫는 `</div>` 태그 사이에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-155">To create a heading and the `EntityDataSource` control for courses entities, add the following markup between the error message `Label` control and the closing `</div>` tag:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample7.aspx)]

<span data-ttu-id="dde2e-156">`Where` 매개 변수에는 `InstructorsGridView` 컨트롤에서 해당 행이 선택 된 강사의 `PersonID` 값이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-156">The `Where` parameter contains the value of the `PersonID` of the instructor whose row is selected in the `InstructorsGridView` control.</span></span> <span data-ttu-id="dde2e-157">`Where` 속성에는 `Course` 엔터티의 `People` 탐색 속성에서 연결 된 모든 `Person` 엔터티를 가져오고, 연결 된 `Course` 엔터티 중 하나에 선택한 `Person` 값이 포함 된 경우에만 `PersonID` 엔터티를 선택 하는 하위 select 명령이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-157">The `Where` property contains a subselect command that gets all associated `Person` entities from a `Course` entity's `People` navigation property and selects the `Course` entity only if one of the associated `Person` entities contains the selected `PersonID` value.</span></span>

<span data-ttu-id="dde2e-158">`GridView` 컨트롤을 만들려면 `CoursesEntityDataSource` 컨트롤 바로 뒤에 다음 태그를 추가 합니다 (닫는 `</div>` 태그 앞).</span><span class="sxs-lookup"><span data-stu-id="dde2e-158">To create the `GridView` control., add the following markup immediately following the `CoursesEntityDataSource` control (before the closing `</div>` tag):</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample8.aspx)]

<span data-ttu-id="dde2e-159">강사를 선택 하지 않은 경우에는 코스가 표시 되지 않으므로 `EmptyDataTemplate` 요소가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-159">Because no courses will be displayed if no instructor is selected, an `EmptyDataTemplate` element is included.</span></span>

<span data-ttu-id="dde2e-160">페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-160">Run the page.</span></span>

<span data-ttu-id="dde2e-161">[![Image04](the-entity-framework-and-aspnet-getting-started-part-4/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="dde2e-161">[![Image04](the-entity-framework-and-aspnet-getting-started-part-4/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image7.png)</span></span>

<span data-ttu-id="dde2e-162">하나 이상의 강좌가 할당 된 강사를 선택 하면 목록에 강좌 또는 강좌가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-162">Select an instructor who has one or more courses assigned, and the course or courses appear in the list.</span></span> <span data-ttu-id="dde2e-163">(참고: 데이터베이스 스키마는 여러 과정을 허용 하지만, 데이터베이스에 제공 된 테스트 데이터에는 실제로 두 개 이상의 강좌가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-163">(Note: although the database schema allows multiple courses, in the test data supplied with the database no instructor actually has more than one course.</span></span> <span data-ttu-id="dde2e-164">**서버 탐색기** 창이 나 이후 자습서에서 추가할 *CoursesAdd* 페이지를 사용 하 여 데이터베이스에 과정을 직접 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-164">You can add courses to the database yourself using the **Server Explorer** window or the *CoursesAdd.aspx* page, which you'll add in a later tutorial.)</span></span>

<span data-ttu-id="dde2e-165">[![Image05](the-entity-framework-and-aspnet-getting-started-part-4/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="dde2e-165">[![Image05](the-entity-framework-and-aspnet-getting-started-part-4/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image9.png)</span></span>

<span data-ttu-id="dde2e-166">`CoursesGridView` 컨트롤은 몇 가지 과정 필드만 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-166">The `CoursesGridView` control shows only a few course fields.</span></span> <span data-ttu-id="dde2e-167">강좌에 대 한 모든 세부 정보를 표시 하려면 사용자가 선택 하는 과정에 대 한 `DetailsView` 컨트롤을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-167">To display all the details for a course, you'll use a `DetailsView` control for the course that the user selects.</span></span> <span data-ttu-id="dde2e-168">*강사 .aspx*에서 닫는 `</div>` 태그 뒤에 다음 태그를 추가 합니다 .이 태그는 앞에 있지 않고 닫는 div 태그 **뒤** 에 위치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-168">In *Instructors.aspx*, add the following markup after the closing `</div>` tag (make sure you place this markup **after** the closing div tag, not before it):</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample9.aspx)]

<span data-ttu-id="dde2e-169">이 태그는 `Courses` 엔터티 집합에 바인딩된 `EntityDataSource` 컨트롤을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-169">This markup creates an `EntityDataSource` control that's bound to the `Courses` entity set.</span></span> <span data-ttu-id="dde2e-170">`Where` 속성은 과정 `GridView` 컨트롤에서 선택 된 행의 `CourseID` 값을 사용 하 여 과정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-170">The `Where` property selects a course using the `CourseID` value of the selected row in the courses `GridView` control.</span></span> <span data-ttu-id="dde2e-171">태그는 나중에 학생 등급을 표시 하는 데 사용 하는 `Selected` 이벤트에 대 한 처리기를 지정 합니다 .이 이벤트는 계층 구조의 다른 수준 보다 낮습니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-171">The markup specifies a handler for the `Selected` event, which you'll use later for displaying student grades, which is another level lower in the hierarchy.</span></span>

<span data-ttu-id="dde2e-172">*Instructors.aspx.cs*에서 `CourseDetailsEntityDataSource_Selected` 메서드에 대 한 다음 스텁을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-172">In *Instructors.aspx.cs*, create the following stub for the `CourseDetailsEntityDataSource_Selected` method.</span></span> <span data-ttu-id="dde2e-173">이 스텁은 자습서의 뒷부분에서 자세히 설명 합니다. 지금은 페이지를 컴파일하고 실행 하는 데 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-173">(You'll fill this stub out later in the tutorial; for now, you need it so that the page will compile and run.)</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample10.cs)]

<span data-ttu-id="dde2e-174">페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-174">Run the page.</span></span>

<span data-ttu-id="dde2e-175">[![Image06](the-entity-framework-and-aspnet-getting-started-part-4/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="dde2e-175">[![Image06](the-entity-framework-and-aspnet-getting-started-part-4/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image11.png)</span></span>

<span data-ttu-id="dde2e-176">처음에는 강좌를 선택 하지 않았으므로 강좌 정보가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-176">Initially there are no course details because no course is selected.</span></span> <span data-ttu-id="dde2e-177">코스가 할당 된 강사를 선택 하 고 세부 정보를 볼 수 있는 과정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-177">Select an instructor who has a course assigned, and then select a course to see the details.</span></span>

<span data-ttu-id="dde2e-178">[![Image07](the-entity-framework-and-aspnet-getting-started-part-4/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="dde2e-178">[![Image07](the-entity-framework-and-aspnet-getting-started-part-4/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image13.png)</span></span>

## <a name="using-the-entitydatasource-selected-event-to-display-related-data"></a><span data-ttu-id="dde2e-179">EntityDataSource "Selected" 이벤트를 사용 하 여 관련 데이터 표시</span><span class="sxs-lookup"><span data-stu-id="dde2e-179">Using the EntityDataSource "Selected" Event to Display Related Data</span></span>

<span data-ttu-id="dde2e-180">마지막으로, 선택한 과정에 대해 등록 된 학생 및 해당 등급을 모두 표시 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-180">Finally, you want to show all of the enrolled students and their grades for the selected course.</span></span> <span data-ttu-id="dde2e-181">이렇게 하려면 과정 `DetailsView`에 바인딩된 `EntityDataSource` 컨트롤의 `Selected` 이벤트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-181">To do this, you'll use the `Selected` event of the `EntityDataSource` control bound to the course `DetailsView`.</span></span>

<span data-ttu-id="dde2e-182">*강사 .aspx*에서 `DetailsView` 컨트롤 뒤에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-182">In *Instructors.aspx*, add the following markup after the `DetailsView` control:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample11.aspx)]

<span data-ttu-id="dde2e-183">이 태그는 학생 목록과 선택한 과정의 등급을 표시 하는 `ListView` 컨트롤을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-183">This markup creates a `ListView` control that displays a list of students and their grades for the selected course.</span></span> <span data-ttu-id="dde2e-184">컨트롤을 코드에 데이터 바인딩할 수 있기 때문에 데이터 소스를 지정 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-184">No data source is specified because you'll databind the control in code.</span></span> <span data-ttu-id="dde2e-185">`EmptyDataTemplate` 요소는 강좌를 선택 하지 않은 경우 표시할 메시지를 제공 합니다 .이 경우에는 표시할 학생이 없는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-185">The `EmptyDataTemplate` element provides a message to display when no course is selected—in that case, there are no students to display.</span></span> <span data-ttu-id="dde2e-186">`LayoutTemplate` 요소는 목록을 표시 하는 HTML 테이블을 만들고 `ItemTemplate`는 표시할 열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-186">The `LayoutTemplate` element creates an HTML table to display the list, and the `ItemTemplate` specifies the columns to display.</span></span> <span data-ttu-id="dde2e-187">학생 ID와 학생 등급은 `StudentGrade` 엔터티에서 가져온 것 이며, 학생 이름은 Entity Framework에서 `StudentGrade` 엔터티의 `Person` 탐색 속성에 사용할 수 있도록 하는 `Person` 엔터티에서 가져온 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-187">The student ID and the student grade are from the `StudentGrade` entity, and the student name is from the `Person` entity that the Entity Framework makes available in the `Person` navigation property of the `StudentGrade` entity.</span></span>

<span data-ttu-id="dde2e-188">*Instructors.aspx.cs*에서 스텁 `CourseDetailsEntityDataSource_Selected` 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-188">In *Instructors.aspx.cs*, replace the stubbed-out `CourseDetailsEntityDataSource_Selected` method with the following code:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample12.cs)]

<span data-ttu-id="dde2e-189">이 이벤트에 대 한 이벤트 인수는 선택한 데이터를 컬렉션 형식으로 제공 합니다 .이는 선택 된 항목이 없는 경우에는 0이 고, `Course` 엔터티가 선택 되어 있으면 항목이 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-189">The event argument for this event provides the selected data in the form of a collection, which will have zero items if nothing is selected or one item if a `Course` entity is selected.</span></span> <span data-ttu-id="dde2e-190">`Course` 엔터티를 선택 하는 경우 코드는 `First` 메서드를 사용 하 여 컬렉션을 단일 개체로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-190">If a `Course` entity is selected, the code uses the `First` method to convert the collection to a single object.</span></span> <span data-ttu-id="dde2e-191">그런 다음 탐색 속성에서 `StudentGrade` 엔터티를 가져와 컬렉션으로 변환한 다음 `GradesListView` 컨트롤을 컬렉션에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-191">It then gets `StudentGrade` entities from the navigation property, converts them to a collection, and binds the `GradesListView` control to the collection.</span></span>

<span data-ttu-id="dde2e-192">이는 점수를 표시 하는 데 충분 하지만 페이지가 처음 표시 될 때 그리고 강좌를 선택 하지 않은 경우에는 빈 데이터 템플릿의 메시지가 표시 되도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-192">This is sufficient to display grades, but you want to make sure that the message in the empty data template is displayed the first time the page is displayed and whenever a course is not selected.</span></span> <span data-ttu-id="dde2e-193">이렇게 하려면 다음 메서드를 만듭니다 .이 메서드는 다음 두 위치에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-193">To do that, create the following method, which you'll call from two places:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample13.cs)]

<span data-ttu-id="dde2e-194">페이지가 처음 표시 될 때 빈 데이터 템플릿을 표시 하려면 `Page_Load` 메서드에서이 새 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-194">Call this new method from the `Page_Load` method to display the empty data template the first time the page is displayed.</span></span> <span data-ttu-id="dde2e-195">`InstructorsGridView_SelectedIndexChanged` 메서드에서이 메서드를 호출 합니다 .이 이벤트는 강사를 선택할 때 발생 합니다. 즉, 새 강좌가 과정 `GridView` 컨트롤에 로드 되 고 없음이 아직 선택 되지 않았음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-195">And call it from the `InstructorsGridView_SelectedIndexChanged` method because that event is raised when an instructor is selected, which means new courses are loaded into the courses `GridView` control and none is selected yet.</span></span> <span data-ttu-id="dde2e-196">다음은 두 호출입니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-196">Here are the two calls:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample14.cs)]

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample15.cs)]

<span data-ttu-id="dde2e-197">페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-197">Run the page.</span></span>

<span data-ttu-id="dde2e-198">[![Image08](the-entity-framework-and-aspnet-getting-started-part-4/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="dde2e-198">[![Image08](the-entity-framework-and-aspnet-getting-started-part-4/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image15.png)</span></span>

<span data-ttu-id="dde2e-199">코스가 할당 된 강사를 선택 하 고 강좌를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-199">Select an instructor that has a course assigned, and then select the course.</span></span>

<span data-ttu-id="dde2e-200">[![Image09](the-entity-framework-and-aspnet-getting-started-part-4/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="dde2e-200">[![Image09](the-entity-framework-and-aspnet-getting-started-part-4/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image17.png)</span></span>

<span data-ttu-id="dde2e-201">이제 관련 데이터로 작업 하는 몇 가지 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-201">You have now seen a few ways to work with related data.</span></span> <span data-ttu-id="dde2e-202">다음 자습서에서는 기존 엔터티 간에 관계를 추가 하는 방법, 관계를 제거 하는 방법 및 기존 엔터티에 대 한 관계를 포함 하는 새 엔터티를 추가 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="dde2e-202">In the following tutorial, you'll learn how to add relationships between existing entities, how to remove relationships, and how to add a new entity that has a relationship to an existing entity.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="dde2e-203">[이전](the-entity-framework-and-aspnet-getting-started-part-3.md)
> [다음](the-entity-framework-and-aspnet-getting-started-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="dde2e-203">[Previous](the-entity-framework-and-aspnet-getting-started-part-3.md)
[Next](the-entity-framework-and-aspnet-getting-started-part-5.md)</span></span>
