---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: '자습서: ASP.NET MVC 앱에서 EF를 사용 하 여 관련 데이터 업데이트'
description: 이 자습서에서는 관련 데이터를 업데이트 합니다. 대부분의 관계에서는 외래 키 필드 또는 탐색 속성을 업데이트 하 여이 작업을 수행할 수 있습니다.
author: tdykstra
ms.author: riande
ms.date: 01/19/2019
ms.topic: tutorial
ms.assetid: 7ba88418-5d0a-437d-b6dc-7c3816d4ec07
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 4d5f6447fdccefdcdf9497a9e94f23243302a0e1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499301"
---
# <a name="tutorial-update-related-data-with-ef-in-an-aspnet-mvc-app"></a><span data-ttu-id="37ced-104">자습서: ASP.NET MVC 앱에서 EF를 사용 하 여 관련 데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="37ced-104">Tutorial: Update related data with EF in an ASP.NET MVC app</span></span>

<span data-ttu-id="37ced-105">이전 자습서에서는 관련 데이터를 표시 했습니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-105">In the previous tutorial you displayed related data.</span></span> <span data-ttu-id="37ced-106">이 자습서에서는 관련 데이터를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-106">In this tutorial you'll update related data.</span></span> <span data-ttu-id="37ced-107">대부분의 관계에서는 외래 키 필드 또는 탐색 속성을 업데이트 하 여이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-107">For most relationships, this can be done by updating either foreign key fields or navigation properties.</span></span> <span data-ttu-id="37ced-108">다대다 Entity Framework 관계의 경우 조인 테이블을 직접 노출 하지 않으므로 적절 한 탐색 속성에서 엔터티를 추가 및 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-108">For many-to-many relationships, the Entity Framework doesn't expose the join table directly, so you add and remove entities to and from the appropriate navigation properties.</span></span>

<span data-ttu-id="37ced-109">다음 그림에서는 사용할 일부 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-109">The following illustrations show some of the pages that you'll work with.</span></span>

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

![강사 편집 과정](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

<span data-ttu-id="37ced-113">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-113">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="37ced-114">과정 페이지 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="37ced-114">Customize courses pages</span></span>
> * <span data-ttu-id="37ced-115">강사 페이지에 office 추가</span><span class="sxs-lookup"><span data-stu-id="37ced-115">Add office to instructors page</span></span>
> * <span data-ttu-id="37ced-116">강사 페이지에 과정 추가</span><span class="sxs-lookup"><span data-stu-id="37ced-116">Add courses to instructors page</span></span>
> * <span data-ttu-id="37ced-117">DeleteConfirmed 업데이트</span><span class="sxs-lookup"><span data-stu-id="37ced-117">Update DeleteConfirmed</span></span>
> * <span data-ttu-id="37ced-118">만들기 페이지에 사무실 위치 및 강좌 추가</span><span class="sxs-lookup"><span data-stu-id="37ced-118">Add office location and courses to the Create page</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37ced-119">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="37ced-119">Prerequisites</span></span>

* [<span data-ttu-id="37ced-120">관련 데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="37ced-120">Reading Related Data</span></span>](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="customize-courses-pages"></a><span data-ttu-id="37ced-121">과정 페이지 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="37ced-121">Customize courses pages</span></span>

<span data-ttu-id="37ced-122">새 강좌 엔터티가 만들어질 때 기존 부서에 대한 관계가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-122">When a new course entity is created, it must have a relationship to an existing department.</span></span> <span data-ttu-id="37ced-123">이를 수행하기 위해 스캐폴드 코드는 컨트롤러 메서드 및 부서를 선택하기 위한 드롭다운 목록을 포함하는 만들기 및 편집 보기를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-123">To facilitate this, the scaffolded code includes controller methods and Create and Edit views that include a drop-down list for selecting the department.</span></span> <span data-ttu-id="37ced-124">드롭다운 목록은 `Course.DepartmentID` 외래 키 속성을 설정 하며, 적절 한 `Department` 엔터티로 `Department` 탐색 속성을 로드 하는 데 필요한 Entity Framework입니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-124">The drop-down list sets the `Course.DepartmentID` foreign key property, and that's all the Entity Framework needs in order to load the `Department` navigation property with the appropriate `Department` entity.</span></span> <span data-ttu-id="37ced-125">스캐폴드 코드를 사용하지만 오류 처리를 추가하고 드롭다운 목록을 정렬하도록 약간 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-125">You'll use the scaffolded code, but change it slightly to add error handling and sort the drop-down list.</span></span>

<span data-ttu-id="37ced-126">*CourseController.cs*에서 4 개의 `Create`와 `Edit` 메서드를 삭제 하 고 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-126">In *CourseController.cs*, delete the four `Create` and `Edit` methods and replace them with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,11-12,19-25,40,44,46,48-78)]

<span data-ttu-id="37ced-127">파일의 시작 부분에 다음 `using` 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-127">Add the following `using` statement at the beginning of the file:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="37ced-128">`PopulateDepartmentsDropDownList` 메서드는 이름별로 정렬 된 모든 부서의 목록을 가져오고, 드롭다운 목록에 대 한 `SelectList` 컬렉션을 만들고, 컬렉션을 `ViewBag` 속성의 뷰에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-128">The `PopulateDepartmentsDropDownList` method gets a list of all departments sorted by name, creates a `SelectList` collection for a drop-down list, and passes the collection to the view in a `ViewBag` property.</span></span> <span data-ttu-id="37ced-129">메서드는 호출 코드가 드롭다운 목록이 렌더링될 때 선택될 항목을 지정하도록 허용하는 선택적 `selectedDepartment` 매개 변수를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-129">The method accepts the optional `selectedDepartment` parameter that allows the calling code to specify the item that will be selected when the drop-down list is rendered.</span></span> <span data-ttu-id="37ced-130">뷰는 이름 `DepartmentID`를 [DropDownList](../../older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md) 도우미에 전달 하 고 도우미는 `DepartmentID`이라는 `SelectList`에 대 한 `ViewBag` 개체를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-130">The view will pass the name `DepartmentID` to the [DropDownList](../../older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md) helper, and the helper then knows to look in the `ViewBag` object for a `SelectList` named `DepartmentID`.</span></span>

<span data-ttu-id="37ced-131">`HttpGet` `Create` 메서드는 선택한 항목을 설정 하지 않고 `PopulateDepartmentsDropDownList` 메서드를 호출 합니다. 새 과정의 경우 부서가 아직 설정 되지 않았기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-131">The `HttpGet` `Create` method calls the `PopulateDepartmentsDropDownList` method without setting the selected item, because for a new course the department is not established yet:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

<span data-ttu-id="37ced-132">`HttpGet` `Edit` 메서드는 편집 중인 과정에 이미 할당 된 부서 ID를 기준으로 선택한 항목을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-132">The `HttpGet` `Edit` method sets the selected item, based on the ID of the department that is already assigned to the course being edited:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=12)]

<span data-ttu-id="37ced-133">`Create` 및 `Edit`에 대 한 `HttpPost` 메서드는 오류 발생 후 페이지를 다시 표시할 때 선택한 항목을 설정 하는 코드도 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-133">The `HttpPost` methods for both `Create` and `Edit` also include code that sets the selected item when they redisplay the page after an error:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=6)]

<span data-ttu-id="37ced-134">이 코드는 페이지를 다시 표시 하 여 오류 메시지를 표시 하는 경우 선택한 부서를 선택 된 상태로 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-134">This code ensures that when the page is redisplayed to show the error message, whatever department was selected stays selected.</span></span>

<span data-ttu-id="37ced-135">강좌 보기는 이미 부서 필드의 드롭다운 목록에 스 캐 폴드이 필드에 대 한 DepartmentID 캡션을 사용 하지 않으려는 경우, *Views\Course\Create.cshtml* 파일에 대해 다음과 같이 변경 내용을 적용 하 여 캡션을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-135">The Course views are already scaffolded with drop-down lists for the department field, but you don't want the DepartmentID caption for this field, so make the following highlighted change to the *Views\Course\Create.cshtml* file to change the caption.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml?highlight=43)]

<span data-ttu-id="37ced-136">*Views\Course\Edit.cshtml*에서 동일한 변경을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-136">Make the same change in *Views\Course\Edit.cshtml*.</span></span>

<span data-ttu-id="37ced-137">일반적으로 스 캐 폴더는 키 값이 데이터베이스에 의해 생성 되 고 변경할 수 없으며 사용자에 게 표시 되는 의미 있는 값이 아니기 때문에 기본 키를 스 캐 폴드 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-137">Normally the scaffolder doesn't scaffold a primary key because the key value is generated by the database and can't be changed and isn't a meaningful value to be displayed to users.</span></span> <span data-ttu-id="37ced-138">스 캐 폴더에는 사용자가 기본 키 값을 입력할 수 있음을 의미 하는 `DatabaseGeneratedOption.None` 특성이 있음을 이해 하기 때문에에는 `CourseID` 필드의 텍스트 상자가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-138">For Course entities the scaffolder does include an text box for the `CourseID` field because it understands that the `DatabaseGeneratedOption.None` attribute means the user should be able enter the primary key value.</span></span> <span data-ttu-id="37ced-139">그러나이 숫자는 다른 보기에 표시 하려는 의미를 가지 므로이를 수동으로 추가 해야 한다는 것을 이해 하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-139">But it doesn't understand that because the number is meaningful you want to see it in the other views, so you need to add it manually.</span></span>

<span data-ttu-id="37ced-140">*Views\Course\Edit.cshtml*에서 **제목** 필드 앞에 강좌 번호 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-140">In *Views\Course\Edit.cshtml*, add a course number field before the **Title** field.</span></span> <span data-ttu-id="37ced-141">기본 키 이기 때문에 표시 되지만 변경할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-141">Because it's the primary key, it's displayed, but it can't be changed.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cshtml)]

<span data-ttu-id="37ced-142">편집 뷰에 강좌 번호에 대 한 숨겨진 필드 (`Html.HiddenFor` 도우미)가 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-142">There's already a hidden field (`Html.HiddenFor` helper) for the course number in the Edit view.</span></span> <span data-ttu-id="37ced-143">사용자가 편집 페이지에서 **저장** 을 클릭할 때 강좌 번호가 게시 된 데이터에 포함 되지 않기 때문에 도우미 *에 대 한 Html* 을 추가 하면 숨겨진 필드의 필요성이 제거 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-143">Adding an *Html.LabelFor* helper doesn't eliminate the need for the hidden field because it doesn't cause the course number to be included in the posted data when the user clicks **Save** on the Edit page.</span></span>

<span data-ttu-id="37ced-144">*Views\Course\Delete.cshtml* 및 *Views\Course\Details.cshtml*에서 부서 이름 캡션을 "Name"에서 "부서"로 변경 하 고 **제목** 필드 앞에 강좌 번호 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-144">In *Views\Course\Delete.cshtml* and *Views\Course\Details.cshtml*, change the department name caption from "Name" to "Department" and add a course number field before the **Title** field.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cshtml?highlight=2,9-15)]

<span data-ttu-id="37ced-145">**만들기** 페이지 (과정 인덱스 표시 페이지를 표시 하 고 **새로 만들기**를 클릭)를 실행 하 고 새 과정에 대 한 데이터를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-145">Run the **Create** page (display the Course Index page and click **Create New**) and enter data for a new course:</span></span>

| <span data-ttu-id="37ced-146">값</span><span class="sxs-lookup"><span data-stu-id="37ced-146">Value</span></span> | <span data-ttu-id="37ced-147">설정</span><span class="sxs-lookup"><span data-stu-id="37ced-147">Setting</span></span> |
| ----- | ------- |
| <span data-ttu-id="37ced-148">Number</span><span class="sxs-lookup"><span data-stu-id="37ced-148">Number</span></span> | <span data-ttu-id="37ced-149">*1000*을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-149">Enter *1000*.</span></span> |
| <span data-ttu-id="37ced-150">제목</span><span class="sxs-lookup"><span data-stu-id="37ced-150">Title</span></span> | <span data-ttu-id="37ced-151">*대 수*를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-151">Enter *Algebra*.</span></span> |
| <span data-ttu-id="37ced-152">크레딧</span><span class="sxs-lookup"><span data-stu-id="37ced-152">Credits</span></span> | <span data-ttu-id="37ced-153">*4*를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-153">Enter *4*.</span></span> |
|<span data-ttu-id="37ced-154">department</span><span class="sxs-lookup"><span data-stu-id="37ced-154">Department</span></span> | <span data-ttu-id="37ced-155">**수학**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-155">Select **Mathematics**.</span></span> |

<span data-ttu-id="37ced-156">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-156">Click **Create**.</span></span> <span data-ttu-id="37ced-157">새 강좌가 목록에 추가 된 과정 인덱스 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-157">The Course Index page is displayed with the new course added to the list.</span></span> <span data-ttu-id="37ced-158">인덱스 페이지 목록의 부서 이름은 관계가 올바르게 설정되었음을 표시하는 탐색 속성에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-158">The department name in the Index page list comes from the navigation property, showing that the relationship was established correctly.</span></span>

<span data-ttu-id="37ced-159">**편집** 페이지를 실행 합니다 (과정 인덱스 페이지를 표시 하 고 과정에서 **편집** 을 클릭).</span><span class="sxs-lookup"><span data-stu-id="37ced-159">Run the **Edit** page (display the Course Index page and click **Edit** on a course).</span></span>

<span data-ttu-id="37ced-160">페이지에서 데이터를 변경하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-160">Change data on the page and click **Save**.</span></span> <span data-ttu-id="37ced-161">업데이트 된 과정 데이터가 포함 된 과정 인덱스 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-161">The Course Index page is displayed with the updated course data.</span></span>

## <a name="add-office-to-instructors-page"></a><span data-ttu-id="37ced-162">강사 페이지에 office 추가</span><span class="sxs-lookup"><span data-stu-id="37ced-162">Add office to instructors page</span></span>

<span data-ttu-id="37ced-163">강사 레코드를 편집할 때 강사의 사무실 할당을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-163">When you edit an instructor record, you want to be able to update the instructor's office assignment.</span></span> <span data-ttu-id="37ced-164">`Instructor` 엔터티에는 `OfficeAssignment` 엔터티와 일 대 일 또는 일 관계가 있습니다. 즉, 다음과 같은 상황을 처리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-164">The `Instructor` entity has a one-to-zero-or-one relationship with the `OfficeAssignment` entity, which means you must handle the following situations:</span></span>

- <span data-ttu-id="37ced-165">사용자가 사무실 할당을 지우면 원래 값이 있는 경우 `OfficeAssignment` 엔터티를 제거 하 고 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-165">If the user clears the office assignment and it originally had a value, you must remove and delete the `OfficeAssignment` entity.</span></span>
- <span data-ttu-id="37ced-166">사용자가 office 할당 값을 입력 하 고 원래 값이 비어 있는 경우 새 `OfficeAssignment` 엔터티를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-166">If the user enters an office assignment value and it originally was empty, you must create a new `OfficeAssignment` entity.</span></span>
- <span data-ttu-id="37ced-167">사용자가 사무실 할당 값을 변경 하는 경우 기존 `OfficeAssignment` 엔터티에서 값을 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-167">If the user changes the value of an office assignment, you must change the value in an existing `OfficeAssignment` entity.</span></span>

<span data-ttu-id="37ced-168">*InstructorController.cs* 를 열고 `HttpGet` `Edit` 메서드를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-168">Open *InstructorController.cs* and look at the `HttpGet` `Edit` method:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="37ced-169">스 캐 폴드 코드는 원하는 항목이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-169">The scaffolded code here isn't what you want.</span></span> <span data-ttu-id="37ced-170">드롭다운 목록에 대 한 데이터를 설정 하 고 있지만 필요한 항목은 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-170">It's setting up data for a drop-down list, but you what you need is a text box.</span></span> <span data-ttu-id="37ced-171">이 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-171">Replace this method with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs?highlight=7-10)]

<span data-ttu-id="37ced-172">이 코드는 `ViewBag` 문을 삭제 하 고 연결 된 `OfficeAssignment` 엔터티에 대 한 즉시 로드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-172">This code drops the `ViewBag` statement and adds eager loading for the associated `OfficeAssignment` entity.</span></span> <span data-ttu-id="37ced-173">`Find` 메서드를 사용 하 여 즉시 로드를 수행할 수 없으므로 강사를 선택 하는 대신 `Where` 및 `Single` 메서드가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-173">You can't perform eager loading with the `Find` method, so the `Where` and `Single` methods are used instead to select the instructor.</span></span>

<span data-ttu-id="37ced-174">`HttpPost` `Edit` 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-174">Replace the `HttpPost` `Edit` method with the following code.</span></span> <span data-ttu-id="37ced-175">office 할당 업데이트를 처리 하는:</span><span class="sxs-lookup"><span data-stu-id="37ced-175">which handles office assignment updates:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="37ced-176">`RetryLimitExceededException`에 대 한 참조에는 `using` 문이 필요 합니다. 추가 하려면 마우스를 `RetryLimitExceededException`위로 가져갑니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-176">The reference to `RetryLimitExceededException` requires a `using` statement; to add it - hover your mouse over `RetryLimitExceededException`.</span></span> <span data-ttu-id="37ced-177">다음 메시지가 표시 됩니다. 예외 메시지 다시 시도 ![](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="37ced-177">The following message appears: ![ Retry exception message](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)</span></span>

<span data-ttu-id="37ced-178">**잠재적 수정 사항 표시**를 선택한 다음, **system.web을 사용** 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-178">Select **Show potential fixes**, then **using System.Data.Entity.Infrastructure**</span></span>

![다시 시도 예외 해결](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)

<span data-ttu-id="37ced-180">코드는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-180">The code does the following:</span></span>

- <span data-ttu-id="37ced-181">는 현재 서명이 `HttpGet` 메서드와 동일 하기 때문에 메서드 이름을 `EditPost`로 변경 합니다. `ActionName` 특성은/Dv/URL이 계속 사용 됨을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-181">Changes the method name to `EditPost` because the signature is now the same as the `HttpGet` method (the `ActionName` attribute specifies that the /Edit/ URL is still used).</span></span>
- <span data-ttu-id="37ced-182">`Instructor` 탐색 속성에 대한 즉시 로드를 사용하여 데이터베이스에서 현재 `OfficeAssignment` 엔터티를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-182">Gets the current `Instructor` entity from the database using eager loading for the `OfficeAssignment` navigation property.</span></span> <span data-ttu-id="37ced-183">이는 `HttpGet` `Edit` 메서드에서 수행한 것과 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-183">This is the same as what you did in the `HttpGet` `Edit` method.</span></span>
- <span data-ttu-id="37ced-184">모델 바인더의 값으로 검색된 `Instructor` 엔터티를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-184">Updates the retrieved `Instructor` entity with values from the model binder.</span></span> <span data-ttu-id="37ced-185">[TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) 오버 로드를 사용 하면 포함 하려는 속성을 *허용 목록* 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-185">The [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) overload used enables you to *whitelist* the properties you want to include.</span></span> <span data-ttu-id="37ced-186">이렇게 하면 [두 번째 자습서](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)에 설명 된 대로 과도 한 게시를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-186">This prevents over-posting, as explained in [the second tutorial](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md).</span></span>

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]
- <span data-ttu-id="37ced-187">사무실 위치가 비어 있으면 `Instructor.OfficeAssignment` 속성을 null로 설정 하 여 `OfficeAssignment` 테이블의 관련 행이 삭제 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-187">If the office location is blank, sets the `Instructor.OfficeAssignment` property to null so that the related row in the `OfficeAssignment` table will be deleted.</span></span>

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]
- <span data-ttu-id="37ced-188">변경 내용을 데이터베이스에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-188">Saves the changes to the database.</span></span>

<span data-ttu-id="37ced-189">*Views\Instructor\Edit.cshtml*의 **채용 날짜** 필드에 대 한 `div` 요소 뒤에 사무실 위치를 편집할 새 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-189">In *Views\Instructor\Edit.cshtml*, after the `div` elements for the **Hire Date** field, add a new field for editing the office location:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml)]

<span data-ttu-id="37ced-190">페이지를 실행 합니다 ( **강사** 탭을 선택 하 고 강사에서 **편집** 을 클릭).</span><span class="sxs-lookup"><span data-stu-id="37ced-190">Run the page (select the **Instructors** tab and then click **Edit** on an instructor).</span></span> <span data-ttu-id="37ced-191">**사무실 위치**를 변경하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-191">Change the **Office Location** and click **Save**.</span></span>

## <a name="add-courses-to-instructors-page"></a><span data-ttu-id="37ced-192">강사 페이지에 과정 추가</span><span class="sxs-lookup"><span data-stu-id="37ced-192">Add courses to instructors page</span></span>

<span data-ttu-id="37ced-193">강사는 강좌 수에 관계 없이 가르칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-193">Instructors may teach any number of courses.</span></span> <span data-ttu-id="37ced-194">이제 확인란 그룹을 사용 하 여 강좌 할당을 변경 하는 기능을 추가 하 여 강사 편집 페이지를 개선 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-194">Now you'll enhance the Instructor Edit page by adding the ability to change course assignments using a group of check boxes.</span></span>

<span data-ttu-id="37ced-195">`Course` 엔터티와 `Instructor` 엔터티 간의 관계는 다 대 다입니다. 즉, 조인 테이블에 있는 외래 키 속성에 직접 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-195">The relationship between the `Course` and `Instructor` entities is many-to-many, which means you do not have direct access to the foreign key properties which are in the join table.</span></span> <span data-ttu-id="37ced-196">대신 `Instructor.Courses` 탐색 속성에서 엔터티를 추가 하 고 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-196">Instead, you add and remove entities to and from the `Instructor.Courses` navigation property.</span></span>

<span data-ttu-id="37ced-197">강사에게 할당된 강좌를 변경할 수 있도록 하는 UI는 확인란의 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-197">The UI that enables you to change which courses an instructor is assigned to is a group of check boxes.</span></span> <span data-ttu-id="37ced-198">데이터베이스의 모든 강좌에 대한 확인란이 표시되고 강사에게 현재 할당되어 있는 것이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-198">A check box for every course in the database is displayed, and the ones that the instructor is currently assigned to are selected.</span></span> <span data-ttu-id="37ced-199">사용자는 확인란을 선택하거나 선택 취소하여 강좌 할당을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-199">The user can select or clear check boxes to change course assignments.</span></span> <span data-ttu-id="37ced-200">강좌 수가 훨씬 많은 경우에는 뷰에서 데이터를 제공 하는 다른 방법을 사용 하는 것이 좋습니다. 그러나 관계를 만들거나 삭제 하기 위해 탐색 속성을 조작 하는 것과 동일한 방법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-200">If the number of courses were much greater, you would probably want to use a different method of presenting the data in the view, but you'd use the same method of manipulating navigation properties in order to create or delete relationships.</span></span>

<span data-ttu-id="37ced-201">확인란의 목록에 대한 보기에 데이터를 제공하려면 보기 모델 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-201">To provide data to the view for the list of check boxes, you'll use a view model class.</span></span> <span data-ttu-id="37ced-202">*Viewmodels* 폴더에 *AssignedCourseData.cs* 를 만들고 기존 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-202">Create *AssignedCourseData.cs* in the *ViewModels* folder and replace the existing code with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

<span data-ttu-id="37ced-203">*InstructorController.cs*에서 `HttpGet` `Edit` 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-203">In *InstructorController.cs*, replace the `HttpGet` `Edit` method with the following code.</span></span> <span data-ttu-id="37ced-204">변경 내용은 강조 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-204">The changes are highlighted.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs?highlight=9,12,20-35)]

<span data-ttu-id="37ced-205">코드는 `Courses` 탐색 속성에 대해 즉시 로드를 추가하고 새 `PopulateAssignedCourseData` 메서드를 호출하여 `AssignedCourseData` 보기 모델 클래스를 사용하여 확인란 배열에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-205">The code adds eager loading for the `Courses` navigation property and calls the new `PopulateAssignedCourseData` method to provide information for the check box array using the `AssignedCourseData` view model class.</span></span>

<span data-ttu-id="37ced-206">`PopulateAssignedCourseData` 메서드의 코드는 뷰 모델 클래스를 사용 하 여 과정 목록을 로드 하기 위해 모든 `Course` 엔터티를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-206">The code in the `PopulateAssignedCourseData` method reads through all `Course` entities in order to load a list of courses using the view model class.</span></span> <span data-ttu-id="37ced-207">각 강좌의 경우 코드는 강좌가 강사의 `Courses` 탐색 속성에 있는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-207">For each course, the code checks whether the course exists in the instructor's `Courses` navigation property.</span></span> <span data-ttu-id="37ced-208">강좌가 강사에 게 할당 되었는지 여부를 확인할 때 효율적인 조회를 만들기 위해 강사에 게 할당 된 강좌는 [Hashset](https://msdn.microsoft.com/library/bb359438.aspx) 컬렉션에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-208">To create efficient lookup when checking whether a course is assigned to the instructor, the courses assigned to the instructor are put into a [HashSet](https://msdn.microsoft.com/library/bb359438.aspx) collection.</span></span> <span data-ttu-id="37ced-209">`Assigned` 속성은 강사가 할당 된 과정에 대해 `true`로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-209">The `Assigned` property is set to `true` for courses the instructor is assigned.</span></span> <span data-ttu-id="37ced-210">보기는 이 속성을 사용하여 선택된 것으로 표시되어야 하는 확인란을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-210">The view will use this property to determine which check boxes must be displayed as selected.</span></span> <span data-ttu-id="37ced-211">마지막으로 목록이 `ViewBag` 속성의 뷰에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-211">Finally, the list is passed to the view in a `ViewBag` property.</span></span>

<span data-ttu-id="37ced-212">다음으로 사용자가 **저장**을 클릭할 때 실행되는 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-212">Next, add the code that's executed when the user clicks **Save**.</span></span> <span data-ttu-id="37ced-213">`EditPost` 메서드를 다음 코드로 바꿉니다 .이 코드는 `Instructor` 엔터티의 `Courses` 탐색 속성을 업데이트 하는 새 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-213">Replace the `EditPost` method with the following code, which calls a new method that updates the `Courses` navigation property of the `Instructor` entity.</span></span> <span data-ttu-id="37ced-214">변경 내용은 강조 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-214">The changes are highlighted.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs?highlight=3,11,25,37,40-68)]

<span data-ttu-id="37ced-215">메서드 시그니처는 이제 `HttpGet` `Edit` 메서드와 다르므로 메서드 이름이 `EditPost`에서 `Edit`로 다시 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-215">The method signature is now different from the `HttpGet` `Edit` method, so the method name changes from `EditPost` back to `Edit`.</span></span>

<span data-ttu-id="37ced-216">뷰에 `Course` 엔터티 컬렉션이 없으므로 모델 바인더는 `Courses` 탐색 속성을 자동으로 업데이트할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-216">Since the view doesn't have a collection of `Course` entities, the model binder can't automatically update the `Courses` navigation property.</span></span> <span data-ttu-id="37ced-217">모델 바인더를 사용 하 여 `Courses` 탐색 속성을 업데이트 하는 대신 새 `UpdateInstructorCourses` 메서드에서이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-217">Instead of using the model binder to update the `Courses` navigation property, you'll do that in the new `UpdateInstructorCourses` method.</span></span> <span data-ttu-id="37ced-218">따라서 모델 바인딩에서 `Courses` 속성을 제외해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-218">Therefore you need to exclude the `Courses` property from model binding.</span></span> <span data-ttu-id="37ced-219">*허용 목록* 오버 로드를 사용 하 고 `Courses`는 포함 목록에 없으므로 [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) 를 호출 하는 코드를 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-219">This doesn't require any change to the code that calls [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) because you're using the *whitelisting* overload and `Courses` isn't in the include list.</span></span>

<span data-ttu-id="37ced-220">확인란이 선택 되지 않은 경우 `UpdateInstructorCourses`의 코드는 빈 컬렉션을 사용 하 여 `Courses` 탐색 속성을 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-220">If no check boxes were selected, the code in `UpdateInstructorCourses` initializes the `Courses` navigation property with an empty collection:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

<span data-ttu-id="37ced-221">그런 다음, 코드는 데이터베이스의 모든 강좌를 반복하고 현재 강사에게 할당된 것과 보기에서 선택되었던 것에 대해 각 강좌를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-221">The code then loops through all courses in the database and checks each course against the ones currently assigned to the instructor versus the ones that were selected in the view.</span></span> <span data-ttu-id="37ced-222">효율적인 조회를 수행하기 위해 후자의 두 컬렉션은 `HashSet` 개체에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-222">To facilitate efficient lookups, the latter two collections are stored in `HashSet` objects.</span></span>

<span data-ttu-id="37ced-223">강좌에 대한 확인란이 선택됐지만 강좌가 `Instructor.Courses` 탐색 속성에 없는 경우 강좌는 탐색 속성의 컬렉션에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-223">If the check box for a course was selected but the course isn't in the `Instructor.Courses` navigation property, the course is added to the collection in the navigation property.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

<span data-ttu-id="37ced-224">강좌에 대한 확인란이 선택되지 않았지만 강좌가 `Instructor.Courses` 탐색 속성에 있는 경우 강좌는 탐색 속성에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-224">If the check box for a course wasn't selected, but the course is in the `Instructor.Courses` navigation property, the course is removed from the navigation property.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs)]

<span data-ttu-id="37ced-225">*Views\Instructor\Edit.cshtml*에서 `OfficeAssignment` 필드의 `div` 요소 바로 뒤에 다음 코드를 추가 하 고 **저장** 단추의 `div` 요소 앞에 다음 코드를 추가 하 여 **코스** 필드를 확인란의 배열로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-225">In *Views\Instructor\Edit.cshtml*, add a **Courses** field with an array of check boxes by adding the following code immediately after the `div` elements for the `OfficeAssignment` field and before the `div` element for the **Save** button:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml)]

<span data-ttu-id="37ced-226">코드를 붙여넣은 후 줄 바꿈 및 들여쓰기가 여기에 표시 되지 않는 경우 여기에 표시 된 것 처럼 보이도록 모든 항목을 수동으로 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-226">After you paste the code, if line breaks and indentation don't look like they do here, manually fix everything so that it looks like what you see here.</span></span> <span data-ttu-id="37ced-227">들여쓰기는 완벽할 필요가 없지만 `@</tr><tr>`, `@:<td>`, `@:</td>` 및 `@</tr>` 줄은 표시된 것처럼 각각 한 줄에 있어야 합니다. 그렇지 않으면 런타임 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-227">The indentation doesn't have to be perfect, but the `@</tr><tr>`, `@:<td>`, `@:</td>`, and `@</tr>` lines must each be on a single line as shown or you'll get a runtime error.</span></span>

<span data-ttu-id="37ced-228">이 코드는 세 개의 열이 있는 HTML 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-228">This code creates an HTML table that has three columns.</span></span> <span data-ttu-id="37ced-229">각 열은 강좌 번호 및 제목으로 구성된 캡션이 뒤에 오는 확인란입니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-229">In each column is a check box followed by a caption that consists of the course number and title.</span></span> <span data-ttu-id="37ced-230">확인란은 모두 동일한 이름 ("selectedCourses")을 가지 며,이는 모델 바인더에 그룹으로 처리 됨을 알립니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-230">The check boxes all have the same name ("selectedCourses"), which informs the model binder that they are to be treated as a group.</span></span> <span data-ttu-id="37ced-231">각 확인란의 `value` 특성은 페이지가 게시 될 때 `CourseID.` 값으로 설정 되며, 모델 바인더는 선택 된 확인란에 대해서만 `CourseID` 값으로 구성 된 배열을 컨트롤러에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-231">The `value` attribute of each check box is set to the value of `CourseID.` When the page is posted, the model binder passes an array to the controller that consists of the `CourseID` values for only the check boxes which are selected.</span></span>

<span data-ttu-id="37ced-232">확인란이 처음 렌더링 되는 경우 강사에 게 할당 된 강좌에 대 한 해당 항목은 `checked` 특성을가지고 있습니다 (선택 표시 됨).</span><span class="sxs-lookup"><span data-stu-id="37ced-232">When the check boxes are initially rendered, those that are for courses assigned to the instructor have `checked` attributes, which selects them (displays them checked).</span></span>

<span data-ttu-id="37ced-233">강좌 할당을 변경한 후에는 사이트가 `Index` 페이지로 반환 될 때 변경 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-233">After changing course assignments, you'll want to be able to verify the changes when the site returns to the `Index` page.</span></span> <span data-ttu-id="37ced-234">따라서 해당 페이지의 테이블에 열을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-234">Therefore, you need to add a column to the table in that page.</span></span> <span data-ttu-id="37ced-235">이 경우 `ViewBag` 개체를 사용할 필요가 없습니다. 표시 하려는 정보가 해당 페이지로 페이지에 전달 하는 `Instructor` 엔터티의 `Courses` 탐색 속성에 이미 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-235">In this case you don't need to use the `ViewBag` object, because the information you want to display is already in the `Courses` navigation property of the `Instructor` entity that you're passing to the page as the model.</span></span>

<span data-ttu-id="37ced-236">*Views\Instructor\Index.cshtml*에서 다음 예제와 같이 **Office** 제목 바로 뒤에 **강좌** 제목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-236">In *Views\Instructor\Index.cshtml*, add a **Courses** heading immediately following the **Office** heading, as shown in the following example:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cshtml?highlight=6)]

<span data-ttu-id="37ced-237">그런 다음, 사무실 위치 정보 셀 바로 뒤에 새 정보 셀을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-237">Then add a new detail cell immediately following the office location detail cell:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml?highlight=7-14)]

<span data-ttu-id="37ced-238">**강사 인덱스** 페이지를 실행 하 여 각 강사에 게 할당 된 강좌를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-238">Run the **Instructor Index** page to see the courses assigned to each instructor.</span></span>

<span data-ttu-id="37ced-239">강사에서 **편집** 을 클릭 하 여 편집 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-239">Click **Edit** on an instructor to see the Edit page.</span></span>

<span data-ttu-id="37ced-240">일부 강좌 할당을 변경 하 고 **저장**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-240">Change some course assignments and click **Save**.</span></span> <span data-ttu-id="37ced-241">변경 내용은 인덱스 페이지에 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-241">The changes you make are reflected on the Index page.</span></span>

 <span data-ttu-id="37ced-242">참고: 강사 강좌 데이터를 편집 하는 데 사용 되는 방법은 제한 된 수의 강좌가 있는 경우에 잘 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-242">Note: The approach taken here to edit instructor course data works well when there is a limited number of courses.</span></span> <span data-ttu-id="37ced-243">훨씬 큰 컬렉션의 경우 다른 UI 및 다른 업데이트 메서드가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-243">For collections that are much larger, a different UI and a different updating method would be required.</span></span>

## <a name="update-deleteconfirmed"></a><span data-ttu-id="37ced-244">DeleteConfirmed 업데이트</span><span class="sxs-lookup"><span data-stu-id="37ced-244">Update DeleteConfirmed</span></span>

<span data-ttu-id="37ced-245">*InstructorController.cs*에서 `DeleteConfirmed` 메서드를 삭제 하 고 그 자리에 다음 코드를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-245">In *InstructorController.cs*, delete the `DeleteConfirmed` method and insert the following code in its place.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample24.cs?highlight=5-8,12-18)]

<span data-ttu-id="37ced-246">이 코드에서는 다음과 같이 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-246">This code makes the following change:</span></span>

- <span data-ttu-id="37ced-247">강사가 모든 부서의 관리자로 할당 된 경우는 해당 부서에서 강사 할당을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-247">If the instructor is assigned as administrator of any department, removes the instructor assignment from that department.</span></span> <span data-ttu-id="37ced-248">이 코드가 없으면 부서에 관리자로 할당 된 강사를 삭제 하려고 하면 참조 무결성 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-248">Without this code, you would get a referential integrity error if you tried to delete an instructor who was assigned as administrator for a department.</span></span>

<span data-ttu-id="37ced-249">이 코드는 여러 부서의 관리자로 할당 된 강사의 시나리오를 처리 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-249">This code doesn't handle the scenario of one instructor assigned as administrator for multiple departments.</span></span> <span data-ttu-id="37ced-250">마지막 자습서에서는 해당 시나리오가 발생 하지 않도록 하는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-250">In the last tutorial you'll add code that prevents that scenario from happening.</span></span>

## <a name="add-office-location-and-courses-to-the-create-page"></a><span data-ttu-id="37ced-251">만들기 페이지에 사무실 위치 및 강좌 추가</span><span class="sxs-lookup"><span data-stu-id="37ced-251">Add office location and courses to the Create page</span></span>

<span data-ttu-id="37ced-252">*InstructorController.cs*에서 `HttpGet`를 삭제 하 고 `Create` 메서드를 `HttpPost` 다음 코드를 해당 위치에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-252">In *InstructorController.cs*, delete the `HttpGet` and `HttpPost` `Create` methods, and then add the following code in their place:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample25.cs)]

<span data-ttu-id="37ced-253">이 코드는 처음에는 강좌를 선택 하지 않은 경우를 제외 하 고는 Edit 메서드에 대해 확인 된 코드와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-253">This code is similar to what you saw for the Edit methods except that initially no courses are selected.</span></span> <span data-ttu-id="37ced-254">`HttpGet` `Create` 메서드는 선택한 강좌가 있지만 뷰의 `foreach` 루프에 대해 빈 컬렉션을 제공 하기 위해 `PopulateAssignedCourseData` 메서드를 호출 합니다 (그렇지 않은 경우 뷰 코드는 null 참조 예외를 throw 함).</span><span class="sxs-lookup"><span data-stu-id="37ced-254">The `HttpGet` `Create` method calls the `PopulateAssignedCourseData` method not because there might be courses selected but in order to provide an empty collection for the `foreach` loop in the view (otherwise the view code would throw a null reference exception).</span></span>

<span data-ttu-id="37ced-255">HttpPost Create 메서드는 유효성 검사 오류를 확인 하 고 새 강사를 데이터베이스에 추가 하는 템플릿 코드 보다 먼저 선택한 강좌를 강좌 탐색 속성에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-255">The HttpPost Create method adds each selected course to the Courses navigation property before the template code that checks for validation errors and adds the new instructor to the database.</span></span> <span data-ttu-id="37ced-256">모델 오류가 있는 경우에도 강좌를 추가 하 여 모델 오류가 발생 한 경우 (예: 사용자에 게 잘못 된 날짜를 입력 한 경우), 페이지가 오류 메시지와 함께 다시 표시 될 때 수행 된 모든 강좌 선택이 자동으로 복원 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-256">Courses are added even if there are model errors so that when there are model errors (for an example, the user keyed an invalid date) so that when the page is redisplayed with an error message, any course selections that were made are automatically restored.</span></span>

<span data-ttu-id="37ced-257">`Courses` 탐색 속성에 강좌를 추가할 수 있도록 빈 컬렉션으로 속성을 초기화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-257">Notice that in order to be able to add courses to the `Courses` navigation property you have to initialize the property as an empty collection:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample26.cs)]

<span data-ttu-id="37ced-258">컨트롤러 코드에서 이 작업을 수행하는 대안으로 다음 예제와 같이 존재하지 않는 경우 자동으로 컬렉션을 만들도록 getter 속성을 변경하여 강사 모델에서 해당 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-258">As an alternative to doing this in controller code, you could do it in the Instructor model by changing the property getter to automatically create the collection if it doesn't exist, as shown in the following example:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample27.cs)]

<span data-ttu-id="37ced-259">이러한 방식으로 `Courses` 속성을 수정하는 경우 컨트롤러에서 명시적 속성 초기화 코드를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-259">If you modify the `Courses` property in this way, you can remove the explicit property initialization code in the controller.</span></span>

<span data-ttu-id="37ced-260">*Views\Instructor\Create.cshtml*에서 채용 날짜 필드와 **제출** 단추 앞에 사무실 위치 텍스트 상자와 코스 확인란을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-260">In *Views\Instructor\Create.cshtml*, add an office location text box and course check boxes after the hire date field and before the **Submit** button.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample28.cshtml)]

<span data-ttu-id="37ced-261">코드를 붙여넣은 후에는 편집 페이지에 대해 이전 처럼 줄 바꿈 및 들여쓰기를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-261">After you paste the code, fix line breaks and indentation as you did earlier for the Edit page.</span></span>

<span data-ttu-id="37ced-262">만들기 페이지를 실행 하 고 강사를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-262">Run the Create page and add an instructor.</span></span>

<a id="transactions"></a>

## <a name="handling-transactions"></a><span data-ttu-id="37ced-263">트랜잭션 처리</span><span class="sxs-lookup"><span data-stu-id="37ced-263">Handling transactions</span></span>

<span data-ttu-id="37ced-264">기본 [CRUD 기능 자습서](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)에서 설명 했 듯이 기본적으로 Entity Framework는 트랜잭션을 암시적으로 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-264">As explained in the [Basic CRUD Functionality tutorial](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md), by default the Entity Framework implicitly implements transactions.</span></span> <span data-ttu-id="37ced-265">더 많은 제어가 필요한 시나리오의 경우 (예: 트랜잭션에 Entity Framework 외부에서 수행 된 작업을 포함 하려는 경우 MSDN에서 [트랜잭션 작업](https://msdn.microsoft.com/data/dn456843) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="37ced-265">For scenarios where you need more control -- for example, if you want to include operations done outside of Entity Framework in a transaction -- see [Working with Transactions](https://msdn.microsoft.com/data/dn456843) on MSDN.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="37ced-266">코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="37ced-266">Get the code</span></span>

[<span data-ttu-id="37ced-267">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="37ced-267">Download the Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="37ced-268">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="37ced-268">Additional resources</span></span>

<span data-ttu-id="37ced-269">[ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)에서 다른 Entity Framework 리소스에 대 한 링크를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-269">Links to other Entity Framework resources can be found in [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="37ced-270">다음 단계</span><span class="sxs-lookup"><span data-stu-id="37ced-270">Next step</span></span>

<span data-ttu-id="37ced-271">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-271">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="37ced-272">사용자 지정 된 과정 페이지</span><span class="sxs-lookup"><span data-stu-id="37ced-272">Customized courses pages</span></span>
> * <span data-ttu-id="37ced-273">강사 페이지에 office를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-273">Added office to instructors page</span></span>
> * <span data-ttu-id="37ced-274">강사 페이지에 과정 추가</span><span class="sxs-lookup"><span data-stu-id="37ced-274">Added courses to instructors page</span></span>
> * <span data-ttu-id="37ced-275">업데이트 된 DeleteConfirmed</span><span class="sxs-lookup"><span data-stu-id="37ced-275">Updated DeleteConfirmed</span></span>
> * <span data-ttu-id="37ced-276">만들기 페이지에 office 위치 및 코스 추가</span><span class="sxs-lookup"><span data-stu-id="37ced-276">Added office location and courses to the Create page</span></span>

<span data-ttu-id="37ced-277">비동기 프로그래밍 모델을 구현 하는 방법에 대해 알아보려면 다음 문서로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ced-277">Advance to the next article to learn how to implement an asynchronous programming model.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="37ced-278">비동기 프로그래밍 모델</span><span class="sxs-lookup"><span data-stu-id="37ced-278">Asynchronous programming model</span></span>](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application.md)
