---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: ASP.NET MVC 응용 프로그램에서 Entity Framework를 사용 하 여 관련 데이터 업데이트 (6/10) | Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다.
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 7871dc05-2750-470f-8b4c-3a52511949bc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: d29cb172d642b67947b461d1a7e55d01872bb8c2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468287"
---
# <a name="updating-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-6-of-10"></a>ASP.NET MVC 응용 프로그램에서 Entity Framework를 사용 하 여 관련 데이터 업데이트 (6/10)

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 5 Code First 및 Visual Studio 2012을 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요. [이 챕터의](building-the-ef5-mvc4-chapter-downloads.md) 시작 또는 시작 프로젝트 다운로드에서 자습서 시리즈를 시작 하 고 여기에서 시작할 수 있습니다.
> 
> > [!NOTE] 
> > 
> > 해결할 수 없는 문제가 발생 하는 경우 [완료 된 챕터를 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 하 여 문제를 재현해 보세요. 일반적으로 코드를 완성 된 코드와 비교 하 여 문제에 대 한 솔루션을 찾을 수 있습니다. 몇 가지 일반적인 오류 및 해결 방법에 대 한 자세한 내용은 [오류 및 해결](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors) 방법을 참조 하세요.

이전 자습서에서는 관련 데이터를 표시 합니다. 이 자습서에서는 관련 데이터를 업데이트 합니다. 대부분의 관계에 대해 적절 한 외래 키 필드를 업데이트 하 여이 작업을 수행할 수 있습니다. 다 대 다 관계의 경우 Entity Framework는 조인 테이블을 직접 노출 하지 않으므로 적절 한 탐색 속성에서 엔터티를 명시적으로 추가 하 고 제거 해야 합니다.

다음 그림에서는 사용할 페이지를 보여 줍니다.

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="customize-the-create-and-edit-pages-for-courses"></a>강좌에 대한 만들기 및 편집 페이지 사용자 지정

새 강좌 엔터티가 만들어질 때 기존 부서에 대한 관계가 있어야 합니다. 이를 수행하기 위해 스캐폴드 코드는 컨트롤러 메서드 및 부서를 선택하기 위한 드롭다운 목록을 포함하는 만들기 및 편집 보기를 포함합니다. 드롭다운 목록은 `Course.DepartmentID` 외래 키 속성을 설정 하며, 적절 한 `Department` 엔터티로 `Department` 탐색 속성을 로드 하는 데 필요한 Entity Framework입니다. 스캐폴드 코드를 사용하지만 오류 처리를 추가하고 드롭다운 목록을 정렬하도록 약간 변경합니다.

*CourseController.cs*에서 4 개의 `Edit`와 `Create` 메서드를 삭제 하 고 다음 코드로 바꿉니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,10,13-14,21-27,34,41,44-45,52-58,62-68)]

`PopulateDepartmentsDropDownList` 메서드는 이름별로 정렬 된 모든 부서의 목록을 가져오고, 드롭다운 목록에 대 한 `SelectList` 컬렉션을 만들고, 컬렉션을 `ViewBag` 속성의 뷰에 전달 합니다. 메서드는 호출 코드가 드롭다운 목록이 렌더링될 때 선택될 항목을 지정하도록 허용하는 선택적 `selectedDepartment` 매개 변수를 허용합니다. 뷰는 `DepartmentID` 이름 [`DropDownList` 도우미](../working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md)에 전달 하 고 도우미는 `DepartmentID`이라는 `SelectList`에 대 한 `ViewBag` 개체를 확인 합니다.

`HttpGet` `Create` 메서드는 선택한 항목을 설정 하지 않고 `PopulateDepartmentsDropDownList` 메서드를 호출 합니다. 새 과정의 경우 부서가 아직 설정 되지 않았기 때문입니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

`HttpGet` `Edit` 메서드는 편집 중인 과정에 이미 할당 된 부서 ID를 기준으로 선택한 항목을 설정 합니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

`Create` 및 `Edit`에 대 한 `HttpPost` 메서드는 오류 발생 후 페이지를 다시 표시할 때 선택한 항목을 설정 하는 코드도 포함 합니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

이 코드는 페이지를 다시 표시 하 여 오류 메시지를 표시 하는 경우 선택한 부서를 선택 된 상태로 유지 합니다.

*Views\Course\Create.cshtml*에서 강조 표시 된 코드를 추가 하 여 **제목** 필드 앞에 새 강좌 번호 필드를 만듭니다. 이전 자습서에서 설명한 대로 기본 키 필드는 기본적으로 스 캐 폴드 되지 않지만이 기본 키는 의미가 있으므로 사용자가 키 값을 입력할 수 있도록 하려고 합니다.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=17-23)]

*Views\Course\Edit.cshtml*, *Views\Course\Delete.cshtml*및 *Views\Course\Details.cshtml*에서 **제목** 필드 앞에 강좌 번호 필드를 추가 합니다. 기본 키 이기 때문에 표시 되지만 변경할 수는 없습니다.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

**만들기** 페이지 (과정 인덱스 표시 페이지를 표시 하 고 **새로 만들기**를 클릭)를 실행 하 고 새 과정에 대 한 데이터를 입력 합니다.

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

**만들기**를 클릭합니다. 새 강좌가 목록에 추가 된 과정 인덱스 페이지가 표시 됩니다. 인덱스 페이지 목록의 부서 이름은 관계가 올바르게 설정되었음을 표시하는 탐색 속성에서 제공됩니다.

![Course_Index_page_showing_new_course](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

**편집** 페이지를 실행 합니다 (과정 인덱스 페이지를 표시 하 고 과정에서 **편집** 을 클릭).

![Course_edit_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

페이지에서 데이터를 변경하고 **저장**을 클릭합니다. 업데이트 된 과정 데이터가 포함 된 과정 인덱스 페이지가 표시 됩니다.

## <a name="adding-an-edit-page-for-instructors"></a>강사를 위한 편집 페이지 추가

강사 레코드를 편집할 때 강사의 사무실 할당을 업데이트할 수 있습니다. `Instructor` 엔터티에는 `OfficeAssignment` 엔터티와 일 대 일 또는 일 관계가 있습니다. 즉, 다음과 같은 상황을 처리 해야 합니다.

- 사용자가 사무실 할당을 지우면 원래 값이 있는 경우 `OfficeAssignment` 엔터티를 제거 하 고 삭제 해야 합니다.
- 사용자가 office 할당 값을 입력 하 고 원래 값이 비어 있는 경우 새 `OfficeAssignment` 엔터티를 만들어야 합니다.
- 사용자가 사무실 할당 값을 변경 하는 경우 기존 `OfficeAssignment` 엔터티에서 값을 변경 해야 합니다.

*InstructorController.cs* 를 열고 `HttpGet` `Edit` 메서드를 확인 합니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

스 캐 폴드 코드는 원하는 항목이 아닙니다. 드롭다운 목록에 대 한 데이터를 설정 하 고 있지만 필요한 항목은 텍스트 상자입니다. 이 메서드를 다음 코드로 바꿉니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

이 코드는 `ViewBag` 문을 삭제 하 고 연결 된 `OfficeAssignment` 엔터티에 대 한 즉시 로드를 추가 합니다. `Find` 메서드를 사용 하 여 즉시 로드를 수행할 수 없으므로 강사를 선택 하는 대신 `Where` 및 `Single` 메서드가 사용 됩니다.

`HttpPost` `Edit` 메서드를 다음 코드로 바꿉니다. office 할당 업데이트를 처리 하는:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

코드는 다음을 수행합니다.

- `Instructor` 탐색 속성에 대한 즉시 로드를 사용하여 데이터베이스에서 현재 `OfficeAssignment` 엔터티를 가져옵니다. 이는 `HttpGet` `Edit` 메서드에서 수행한 것과 동일 합니다.
- 모델 바인더의 값으로 검색된 `Instructor` 엔터티를 업데이트합니다. [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) 오버 로드를 사용 하면 포함 하려는 속성을 *허용 목록* 수 있습니다. 이렇게 하면 [두 번째 자습서](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)에 설명 된 대로 과도 한 게시를 방지할 수 있습니다.

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]
- 사무실 위치가 비어 있으면 `Instructor.OfficeAssignment` 속성을 null로 설정 하 여 `OfficeAssignment` 테이블의 관련 행이 삭제 되도록 합니다.

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]
- 변경 내용을 데이터베이스에 저장합니다.

*Views\Instructor\Edit.cshtml*의 **채용 날짜** 필드에 대 한 `div` 요소 뒤에 사무실 위치를 편집할 새 필드를 추가 합니다.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml)]

페이지를 실행 합니다 ( **강사** 탭을 선택 하 고 강사에서 **편집** 을 클릭). **사무실 위치**를 변경하고 **저장**을 클릭합니다.

![Changing_the_office_location](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

## <a name="adding-course-assignments-to-the-instructor-edit-page"></a>강사 편집 페이지에 강좌 할당 추가

강사는 강좌 수에 관계 없이 가르칠 수 있습니다. 이제 다음 스크린샷에 표시된 것처럼 확인란 그룹을 사용하여 강좌 할당을 변경하는 기능을 추가하여 강사 편집 페이지를 향상시킵니다.

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

`Course` 엔터티와 `Instructor` 엔터티 간의 관계는 다 대 다입니다. 즉, 조인 테이블에 직접 액세스할 수 없습니다. 대신 `Instructor.Courses` 탐색 속성에서 엔터티를 추가 및 제거 합니다.

강사에게 할당된 강좌를 변경할 수 있도록 하는 UI는 확인란의 그룹입니다. 데이터베이스의 모든 강좌에 대한 확인란이 표시되고 강사에게 현재 할당되어 있는 것이 선택됩니다. 사용자는 확인란을 선택하거나 선택 취소하여 강좌 할당을 변경할 수 있습니다. 강좌 수가 훨씬 많은 경우에는 뷰에서 데이터를 제공 하는 다른 방법을 사용 하는 것이 좋습니다. 그러나 관계를 만들거나 삭제 하기 위해 탐색 속성을 조작 하는 것과 동일한 방법을 사용 합니다.

확인란의 목록에 대한 보기에 데이터를 제공하려면 보기 모델 클래스를 사용합니다. *Viewmodels* 폴더에 *AssignedCourseData.cs* 를 만들고 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

*InstructorController.cs*에서 `HttpGet` `Edit` 메서드를 다음 코드로 바꿉니다. 변경 내용은 강조 표시되어 있습니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=5,8,12-27)]

코드는 `Courses` 탐색 속성에 대해 즉시 로드를 추가하고 새 `PopulateAssignedCourseData` 메서드를 호출하여 `AssignedCourseData` 보기 모델 클래스를 사용하여 확인란 배열에 대한 정보를 제공합니다.

`PopulateAssignedCourseData` 메서드의 코드는 뷰 모델 클래스를 사용 하 여 과정 목록을 로드 하기 위해 모든 `Course` 엔터티를 읽습니다. 각 강좌의 경우 코드는 강좌가 강사의 `Courses` 탐색 속성에 있는지 여부를 확인합니다. 강좌가 강사에 게 할당 되었는지 여부를 확인할 때 효율적인 조회를 만들기 위해 강사에 게 할당 된 강좌는 [Hashset](https://msdn.microsoft.com/library/bb359438.aspx) 컬렉션에 저장 됩니다. `Assigned` 속성은 강사가 할당 된 과정에 대해 `true`로 설정 됩니다. 보기는 이 속성을 사용하여 선택된 것으로 표시되어야 하는 확인란을 결정합니다. 마지막으로 목록이 `ViewBag` 속성의 뷰에 전달 됩니다.

다음으로 사용자가 **저장**을 클릭할 때 실행되는 코드를 추가합니다. `HttpPost` `Edit` 메서드를 다음 코드로 바꿉니다 .이 코드는 `Instructor` 엔터티의 `Courses` 탐색 속성을 업데이트 하는 새 메서드를 호출 합니다. 변경 내용은 강조 표시되어 있습니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs?highlight=3,7,20,33,37-65)]

뷰에 `Course` 엔터티 컬렉션이 없으므로 모델 바인더는 `Courses` 탐색 속성을 자동으로 업데이트할 수 없습니다. 모델 바인더를 사용 하 여 강좌 탐색 속성을 업데이트 하는 대신 새 `UpdateInstructorCourses` 메서드에서이 작업을 수행 합니다. 따라서 모델 바인딩에서 `Courses` 속성을 제외해야 합니다. *허용 목록* 오버 로드를 사용 하 고 `Courses`는 포함 목록에 없으므로 [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) 를 호출 하는 코드를 변경할 필요가 없습니다.

확인란이 선택 되지 않은 경우 `UpdateInstructorCourses`의 코드는 빈 컬렉션을 사용 하 여 `Courses` 탐색 속성을 초기화 합니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

그런 다음, 코드는 데이터베이스의 모든 강좌를 반복하고 현재 강사에게 할당된 것과 보기에서 선택되었던 것에 대해 각 강좌를 확인합니다. 효율적인 조회를 수행하기 위해 후자의 두 컬렉션은 `HashSet` 개체에 저장됩니다.

강좌에 대한 확인란이 선택됐지만 강좌가 `Instructor.Courses` 탐색 속성에 없는 경우 강좌는 탐색 속성의 컬렉션에 추가됩니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

강좌에 대한 확인란이 선택되지 않았지만 강좌가 `Instructor.Courses` 탐색 속성에 있는 경우 강좌는 탐색 속성에서 제거됩니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

*Views\Instructor\Edit.cshtml*에서 `OfficeAssignment` 필드의 `div` 요소 바로 뒤에 다음 강조 표시 된 코드를 추가 하 여 일련의 확인란을 사용 하 여 **코스** 필드를 추가 합니다.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml?highlight=51-73)]

이 코드는 세 개의 열이 있는 HTML 테이블을 만듭니다. 각 열은 강좌 번호 및 제목으로 구성된 캡션이 뒤에 오는 확인란입니다. 확인란은 모두 동일한 이름 ("selectedCourses")을 가지 며,이는 모델 바인더에 그룹으로 처리 됨을 알립니다. 각 확인란의 `value` 특성은 페이지가 게시 될 때 `CourseID.` 값으로 설정 되며, 모델 바인더는 선택 된 확인란에 대해서만 `CourseID` 값으로 구성 된 배열을 컨트롤러에 전달 합니다.

확인란이 처음 렌더링 되는 경우 강사에 게 할당 된 강좌에 대 한 해당 항목은 `checked` 특성을가지고 있습니다 (선택 표시 됨).

강좌 할당을 변경한 후에는 사이트가 `Index` 페이지로 반환 될 때 변경 내용을 확인할 수 있습니다. 따라서 해당 페이지의 테이블에 열을 추가 해야 합니다. 이 경우 `ViewBag` 개체를 사용할 필요가 없습니다. 표시 하려는 정보가 해당 페이지로 페이지에 전달 하는 `Instructor` 엔터티의 `Courses` 탐색 속성에 이미 있기 때문입니다.

*Views\Instructor\Index.cshtml*에서 다음 예제와 같이 **Office** 제목 바로 뒤에 **강좌** 제목을 추가 합니다.

[!code-html[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html?highlight=7)]

그런 다음, 사무실 위치 정보 셀 바로 뒤에 새 정보 셀을 추가 합니다.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=19,50-57)]

**강사 인덱스** 페이지를 실행 하 여 각 강사에 게 할당 된 강좌를 확인 합니다.

![Instructor_index_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

강사에서 **편집** 을 클릭 하 여 편집 페이지를 표시 합니다.

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

일부 강좌 할당을 변경 하 고 **저장**을 클릭 합니다. 변경 내용은 인덱스 페이지에 반영됩니다.

 참고: 강사 강좌 데이터를 편집 하는 방법은 제한 된 수의 강좌가 있는 경우에 잘 작동 합니다. 훨씬 큰 컬렉션의 경우 다른 UI 및 다른 업데이트 메서드가 필요합니다.  

## <a name="update-the-delete-method"></a>Delete 메서드를 업데이트 합니다.

HttpPost Delete 메서드의 코드를 변경 하 여 강사가 삭제 될 때 office 할당 레코드 (있는 경우)가 삭제 되도록 합니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs?highlight=6,10)]

관리자 권한으로 부서에 할당 된 강사를 삭제 하려고 하면 참조 무결성 오류가 발생 합니다. 강사가 관리자로 할당 된 모든 부서에서 강사가 자동으로 제거 되는 추가 코드는 [이 자습서의 현재 버전](../../getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) 을 참조 하세요.

## <a name="summary"></a>요약

이제 관련 된 데이터를 사용 하는 방법을 소개 했습니다. 지금까지 이러한 자습서에서는 전체 CRUD 작업을 수행 했지만 동시성 문제를 처리 하지 않았습니다. 다음 자습서에서는 동시성 항목을 소개 하 고,이를 처리 하는 옵션을 설명 하 고, 하나의 엔터티 형식에 대해 이미 작성 한 CRUD 코드에 동시성 처리를 추가 합니다.

[이 시리즈의 마지막 자습서](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)끝에 있는 다른 Entity Framework 리소스에 대 한 링크를 찾을 수 있습니다.

> [!div class="step-by-step"]
> [이전](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [다음](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
