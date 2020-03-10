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
# <a name="tutorial-update-related-data-with-ef-in-an-aspnet-mvc-app"></a>자습서: ASP.NET MVC 앱에서 EF를 사용 하 여 관련 데이터 업데이트

이전 자습서에서는 관련 데이터를 표시 했습니다. 이 자습서에서는 관련 데이터를 업데이트 합니다. 대부분의 관계에서는 외래 키 필드 또는 탐색 속성을 업데이트 하 여이 작업을 수행할 수 있습니다. 다대다 Entity Framework 관계의 경우 조인 테이블을 직접 노출 하지 않으므로 적절 한 탐색 속성에서 엔터티를 추가 및 제거 합니다.

다음 그림에서는 사용할 일부 페이지를 보여 줍니다.

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

![강사 편집 과정](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

이 자습서에서는 다음을 수행합니다.

> [!div class="checklist"]
> * 과정 페이지 사용자 지정
> * 강사 페이지에 office 추가
> * 강사 페이지에 과정 추가
> * DeleteConfirmed 업데이트
> * 만들기 페이지에 사무실 위치 및 강좌 추가

## <a name="prerequisites"></a>사전 요구 사항

* [관련 데이터 읽기](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="customize-courses-pages"></a>과정 페이지 사용자 지정

새 강좌 엔터티가 만들어질 때 기존 부서에 대한 관계가 있어야 합니다. 이를 수행하기 위해 스캐폴드 코드는 컨트롤러 메서드 및 부서를 선택하기 위한 드롭다운 목록을 포함하는 만들기 및 편집 보기를 포함합니다. 드롭다운 목록은 `Course.DepartmentID` 외래 키 속성을 설정 하며, 적절 한 `Department` 엔터티로 `Department` 탐색 속성을 로드 하는 데 필요한 Entity Framework입니다. 스캐폴드 코드를 사용하지만 오류 처리를 추가하고 드롭다운 목록을 정렬하도록 약간 변경합니다.

*CourseController.cs*에서 4 개의 `Create`와 `Edit` 메서드를 삭제 하 고 다음 코드로 바꿉니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,11-12,19-25,40,44,46,48-78)]

파일의 시작 부분에 다음 `using` 문을 추가 합니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

`PopulateDepartmentsDropDownList` 메서드는 이름별로 정렬 된 모든 부서의 목록을 가져오고, 드롭다운 목록에 대 한 `SelectList` 컬렉션을 만들고, 컬렉션을 `ViewBag` 속성의 뷰에 전달 합니다. 메서드는 호출 코드가 드롭다운 목록이 렌더링될 때 선택될 항목을 지정하도록 허용하는 선택적 `selectedDepartment` 매개 변수를 허용합니다. 뷰는 이름 `DepartmentID`를 [DropDownList](../../older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md) 도우미에 전달 하 고 도우미는 `DepartmentID`이라는 `SelectList`에 대 한 `ViewBag` 개체를 찾습니다.

`HttpGet` `Create` 메서드는 선택한 항목을 설정 하지 않고 `PopulateDepartmentsDropDownList` 메서드를 호출 합니다. 새 과정의 경우 부서가 아직 설정 되지 않았기 때문입니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

`HttpGet` `Edit` 메서드는 편집 중인 과정에 이미 할당 된 부서 ID를 기준으로 선택한 항목을 설정 합니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=12)]

`Create` 및 `Edit`에 대 한 `HttpPost` 메서드는 오류 발생 후 페이지를 다시 표시할 때 선택한 항목을 설정 하는 코드도 포함 합니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=6)]

이 코드는 페이지를 다시 표시 하 여 오류 메시지를 표시 하는 경우 선택한 부서를 선택 된 상태로 유지 합니다.

강좌 보기는 이미 부서 필드의 드롭다운 목록에 스 캐 폴드이 필드에 대 한 DepartmentID 캡션을 사용 하지 않으려는 경우, *Views\Course\Create.cshtml* 파일에 대해 다음과 같이 변경 내용을 적용 하 여 캡션을 변경 합니다.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml?highlight=43)]

*Views\Course\Edit.cshtml*에서 동일한 변경을 수행 합니다.

일반적으로 스 캐 폴더는 키 값이 데이터베이스에 의해 생성 되 고 변경할 수 없으며 사용자에 게 표시 되는 의미 있는 값이 아니기 때문에 기본 키를 스 캐 폴드 하지 않습니다. 스 캐 폴더에는 사용자가 기본 키 값을 입력할 수 있음을 의미 하는 `DatabaseGeneratedOption.None` 특성이 있음을 이해 하기 때문에에는 `CourseID` 필드의 텍스트 상자가 포함 되어 있습니다. 그러나이 숫자는 다른 보기에 표시 하려는 의미를 가지 므로이를 수동으로 추가 해야 한다는 것을 이해 하지 못합니다.

*Views\Course\Edit.cshtml*에서 **제목** 필드 앞에 강좌 번호 필드를 추가 합니다. 기본 키 이기 때문에 표시 되지만 변경할 수는 없습니다.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cshtml)]

편집 뷰에 강좌 번호에 대 한 숨겨진 필드 (`Html.HiddenFor` 도우미)가 이미 있습니다. 사용자가 편집 페이지에서 **저장** 을 클릭할 때 강좌 번호가 게시 된 데이터에 포함 되지 않기 때문에 도우미 *에 대 한 Html* 을 추가 하면 숨겨진 필드의 필요성이 제거 되지 않습니다.

*Views\Course\Delete.cshtml* 및 *Views\Course\Details.cshtml*에서 부서 이름 캡션을 "Name"에서 "부서"로 변경 하 고 **제목** 필드 앞에 강좌 번호 필드를 추가 합니다.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cshtml?highlight=2,9-15)]

**만들기** 페이지 (과정 인덱스 표시 페이지를 표시 하 고 **새로 만들기**를 클릭)를 실행 하 고 새 과정에 대 한 데이터를 입력 합니다.

| 값 | 설정 |
| ----- | ------- |
| Number | *1000*을 입력 합니다. |
| 제목 | *대 수*를 입력 합니다. |
| 크레딧 | *4*를 입력 합니다. |
|department | **수학**을 선택 합니다. |

**만들기**를 클릭합니다. 새 강좌가 목록에 추가 된 과정 인덱스 페이지가 표시 됩니다. 인덱스 페이지 목록의 부서 이름은 관계가 올바르게 설정되었음을 표시하는 탐색 속성에서 제공됩니다.

**편집** 페이지를 실행 합니다 (과정 인덱스 페이지를 표시 하 고 과정에서 **편집** 을 클릭).

페이지에서 데이터를 변경하고 **저장**을 클릭합니다. 업데이트 된 과정 데이터가 포함 된 과정 인덱스 페이지가 표시 됩니다.

## <a name="add-office-to-instructors-page"></a>강사 페이지에 office 추가

강사 레코드를 편집할 때 강사의 사무실 할당을 업데이트할 수 있습니다. `Instructor` 엔터티에는 `OfficeAssignment` 엔터티와 일 대 일 또는 일 관계가 있습니다. 즉, 다음과 같은 상황을 처리 해야 합니다.

- 사용자가 사무실 할당을 지우면 원래 값이 있는 경우 `OfficeAssignment` 엔터티를 제거 하 고 삭제 해야 합니다.
- 사용자가 office 할당 값을 입력 하 고 원래 값이 비어 있는 경우 새 `OfficeAssignment` 엔터티를 만들어야 합니다.
- 사용자가 사무실 할당 값을 변경 하는 경우 기존 `OfficeAssignment` 엔터티에서 값을 변경 해야 합니다.

*InstructorController.cs* 를 열고 `HttpGet` `Edit` 메서드를 확인 합니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

스 캐 폴드 코드는 원하는 항목이 아닙니다. 드롭다운 목록에 대 한 데이터를 설정 하 고 있지만 필요한 항목은 텍스트 상자입니다. 이 메서드를 다음 코드로 바꿉니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs?highlight=7-10)]

이 코드는 `ViewBag` 문을 삭제 하 고 연결 된 `OfficeAssignment` 엔터티에 대 한 즉시 로드를 추가 합니다. `Find` 메서드를 사용 하 여 즉시 로드를 수행할 수 없으므로 강사를 선택 하는 대신 `Where` 및 `Single` 메서드가 사용 됩니다.

`HttpPost` `Edit` 메서드를 다음 코드로 바꿉니다. office 할당 업데이트를 처리 하는:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

`RetryLimitExceededException`에 대 한 참조에는 `using` 문이 필요 합니다. 추가 하려면 마우스를 `RetryLimitExceededException`위로 가져갑니다. 다음 메시지가 표시 됩니다. 예외 메시지 다시 시도 ![](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)

**잠재적 수정 사항 표시**를 선택한 다음, **system.web을 사용** 합니다.

![다시 시도 예외 해결](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)

코드는 다음을 수행합니다.

- 는 현재 서명이 `HttpGet` 메서드와 동일 하기 때문에 메서드 이름을 `EditPost`로 변경 합니다. `ActionName` 특성은/Dv/URL이 계속 사용 됨을 지정 합니다.
- `Instructor` 탐색 속성에 대한 즉시 로드를 사용하여 데이터베이스에서 현재 `OfficeAssignment` 엔터티를 가져옵니다. 이는 `HttpGet` `Edit` 메서드에서 수행한 것과 동일 합니다.
- 모델 바인더의 값으로 검색된 `Instructor` 엔터티를 업데이트합니다. [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) 오버 로드를 사용 하면 포함 하려는 속성을 *허용 목록* 수 있습니다. 이렇게 하면 [두 번째 자습서](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)에 설명 된 대로 과도 한 게시를 방지할 수 있습니다.

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]
- 사무실 위치가 비어 있으면 `Instructor.OfficeAssignment` 속성을 null로 설정 하 여 `OfficeAssignment` 테이블의 관련 행이 삭제 되도록 합니다.

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]
- 변경 내용을 데이터베이스에 저장합니다.

*Views\Instructor\Edit.cshtml*의 **채용 날짜** 필드에 대 한 `div` 요소 뒤에 사무실 위치를 편집할 새 필드를 추가 합니다.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml)]

페이지를 실행 합니다 ( **강사** 탭을 선택 하 고 강사에서 **편집** 을 클릭). **사무실 위치**를 변경하고 **저장**을 클릭합니다.

## <a name="add-courses-to-instructors-page"></a>강사 페이지에 과정 추가

강사는 강좌 수에 관계 없이 가르칠 수 있습니다. 이제 확인란 그룹을 사용 하 여 강좌 할당을 변경 하는 기능을 추가 하 여 강사 편집 페이지를 개선 합니다.

`Course` 엔터티와 `Instructor` 엔터티 간의 관계는 다 대 다입니다. 즉, 조인 테이블에 있는 외래 키 속성에 직접 액세스할 수 없습니다. 대신 `Instructor.Courses` 탐색 속성에서 엔터티를 추가 하 고 제거 합니다.

강사에게 할당된 강좌를 변경할 수 있도록 하는 UI는 확인란의 그룹입니다. 데이터베이스의 모든 강좌에 대한 확인란이 표시되고 강사에게 현재 할당되어 있는 것이 선택됩니다. 사용자는 확인란을 선택하거나 선택 취소하여 강좌 할당을 변경할 수 있습니다. 강좌 수가 훨씬 많은 경우에는 뷰에서 데이터를 제공 하는 다른 방법을 사용 하는 것이 좋습니다. 그러나 관계를 만들거나 삭제 하기 위해 탐색 속성을 조작 하는 것과 동일한 방법을 사용 합니다.

확인란의 목록에 대한 보기에 데이터를 제공하려면 보기 모델 클래스를 사용합니다. *Viewmodels* 폴더에 *AssignedCourseData.cs* 를 만들고 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

*InstructorController.cs*에서 `HttpGet` `Edit` 메서드를 다음 코드로 바꿉니다. 변경 내용은 강조 표시되어 있습니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs?highlight=9,12,20-35)]

코드는 `Courses` 탐색 속성에 대해 즉시 로드를 추가하고 새 `PopulateAssignedCourseData` 메서드를 호출하여 `AssignedCourseData` 보기 모델 클래스를 사용하여 확인란 배열에 대한 정보를 제공합니다.

`PopulateAssignedCourseData` 메서드의 코드는 뷰 모델 클래스를 사용 하 여 과정 목록을 로드 하기 위해 모든 `Course` 엔터티를 읽습니다. 각 강좌의 경우 코드는 강좌가 강사의 `Courses` 탐색 속성에 있는지 여부를 확인합니다. 강좌가 강사에 게 할당 되었는지 여부를 확인할 때 효율적인 조회를 만들기 위해 강사에 게 할당 된 강좌는 [Hashset](https://msdn.microsoft.com/library/bb359438.aspx) 컬렉션에 저장 됩니다. `Assigned` 속성은 강사가 할당 된 과정에 대해 `true`로 설정 됩니다. 보기는 이 속성을 사용하여 선택된 것으로 표시되어야 하는 확인란을 결정합니다. 마지막으로 목록이 `ViewBag` 속성의 뷰에 전달 됩니다.

다음으로 사용자가 **저장**을 클릭할 때 실행되는 코드를 추가합니다. `EditPost` 메서드를 다음 코드로 바꿉니다 .이 코드는 `Instructor` 엔터티의 `Courses` 탐색 속성을 업데이트 하는 새 메서드를 호출 합니다. 변경 내용은 강조 표시되어 있습니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs?highlight=3,11,25,37,40-68)]

메서드 시그니처는 이제 `HttpGet` `Edit` 메서드와 다르므로 메서드 이름이 `EditPost`에서 `Edit`로 다시 변경 됩니다.

뷰에 `Course` 엔터티 컬렉션이 없으므로 모델 바인더는 `Courses` 탐색 속성을 자동으로 업데이트할 수 없습니다. 모델 바인더를 사용 하 여 `Courses` 탐색 속성을 업데이트 하는 대신 새 `UpdateInstructorCourses` 메서드에서이 작업을 수행 합니다. 따라서 모델 바인딩에서 `Courses` 속성을 제외해야 합니다. *허용 목록* 오버 로드를 사용 하 고 `Courses`는 포함 목록에 없으므로 [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) 를 호출 하는 코드를 변경할 필요가 없습니다.

확인란이 선택 되지 않은 경우 `UpdateInstructorCourses`의 코드는 빈 컬렉션을 사용 하 여 `Courses` 탐색 속성을 초기화 합니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

그런 다음, 코드는 데이터베이스의 모든 강좌를 반복하고 현재 강사에게 할당된 것과 보기에서 선택되었던 것에 대해 각 강좌를 확인합니다. 효율적인 조회를 수행하기 위해 후자의 두 컬렉션은 `HashSet` 개체에 저장됩니다.

강좌에 대한 확인란이 선택됐지만 강좌가 `Instructor.Courses` 탐색 속성에 없는 경우 강좌는 탐색 속성의 컬렉션에 추가됩니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

강좌에 대한 확인란이 선택되지 않았지만 강좌가 `Instructor.Courses` 탐색 속성에 있는 경우 강좌는 탐색 속성에서 제거됩니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs)]

*Views\Instructor\Edit.cshtml*에서 `OfficeAssignment` 필드의 `div` 요소 바로 뒤에 다음 코드를 추가 하 고 **저장** 단추의 `div` 요소 앞에 다음 코드를 추가 하 여 **코스** 필드를 확인란의 배열로 추가 합니다.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml)]

코드를 붙여넣은 후 줄 바꿈 및 들여쓰기가 여기에 표시 되지 않는 경우 여기에 표시 된 것 처럼 보이도록 모든 항목을 수동으로 수정 합니다. 들여쓰기는 완벽할 필요가 없지만 `@</tr><tr>`, `@:<td>`, `@:</td>` 및 `@</tr>` 줄은 표시된 것처럼 각각 한 줄에 있어야 합니다. 그렇지 않으면 런타임 오류가 발생합니다.

이 코드는 세 개의 열이 있는 HTML 테이블을 만듭니다. 각 열은 강좌 번호 및 제목으로 구성된 캡션이 뒤에 오는 확인란입니다. 확인란은 모두 동일한 이름 ("selectedCourses")을 가지 며,이는 모델 바인더에 그룹으로 처리 됨을 알립니다. 각 확인란의 `value` 특성은 페이지가 게시 될 때 `CourseID.` 값으로 설정 되며, 모델 바인더는 선택 된 확인란에 대해서만 `CourseID` 값으로 구성 된 배열을 컨트롤러에 전달 합니다.

확인란이 처음 렌더링 되는 경우 강사에 게 할당 된 강좌에 대 한 해당 항목은 `checked` 특성을가지고 있습니다 (선택 표시 됨).

강좌 할당을 변경한 후에는 사이트가 `Index` 페이지로 반환 될 때 변경 내용을 확인할 수 있습니다. 따라서 해당 페이지의 테이블에 열을 추가 해야 합니다. 이 경우 `ViewBag` 개체를 사용할 필요가 없습니다. 표시 하려는 정보가 해당 페이지로 페이지에 전달 하는 `Instructor` 엔터티의 `Courses` 탐색 속성에 이미 있기 때문입니다.

*Views\Instructor\Index.cshtml*에서 다음 예제와 같이 **Office** 제목 바로 뒤에 **강좌** 제목을 추가 합니다.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cshtml?highlight=6)]

그런 다음, 사무실 위치 정보 셀 바로 뒤에 새 정보 셀을 추가 합니다.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml?highlight=7-14)]

**강사 인덱스** 페이지를 실행 하 여 각 강사에 게 할당 된 강좌를 확인 합니다.

강사에서 **편집** 을 클릭 하 여 편집 페이지를 표시 합니다.

일부 강좌 할당을 변경 하 고 **저장**을 클릭 합니다. 변경 내용은 인덱스 페이지에 반영됩니다.

 참고: 강사 강좌 데이터를 편집 하는 데 사용 되는 방법은 제한 된 수의 강좌가 있는 경우에 잘 작동 합니다. 훨씬 큰 컬렉션의 경우 다른 UI 및 다른 업데이트 메서드가 필요합니다.

## <a name="update-deleteconfirmed"></a>DeleteConfirmed 업데이트

*InstructorController.cs*에서 `DeleteConfirmed` 메서드를 삭제 하 고 그 자리에 다음 코드를 삽입 합니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample24.cs?highlight=5-8,12-18)]

이 코드에서는 다음과 같이 변경 합니다.

- 강사가 모든 부서의 관리자로 할당 된 경우는 해당 부서에서 강사 할당을 제거 합니다. 이 코드가 없으면 부서에 관리자로 할당 된 강사를 삭제 하려고 하면 참조 무결성 오류가 발생 합니다.

이 코드는 여러 부서의 관리자로 할당 된 강사의 시나리오를 처리 하지 않습니다. 마지막 자습서에서는 해당 시나리오가 발생 하지 않도록 하는 코드를 추가 합니다.

## <a name="add-office-location-and-courses-to-the-create-page"></a>만들기 페이지에 사무실 위치 및 강좌 추가

*InstructorController.cs*에서 `HttpGet`를 삭제 하 고 `Create` 메서드를 `HttpPost` 다음 코드를 해당 위치에 추가 합니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample25.cs)]

이 코드는 처음에는 강좌를 선택 하지 않은 경우를 제외 하 고는 Edit 메서드에 대해 확인 된 코드와 비슷합니다. `HttpGet` `Create` 메서드는 선택한 강좌가 있지만 뷰의 `foreach` 루프에 대해 빈 컬렉션을 제공 하기 위해 `PopulateAssignedCourseData` 메서드를 호출 합니다 (그렇지 않은 경우 뷰 코드는 null 참조 예외를 throw 함).

HttpPost Create 메서드는 유효성 검사 오류를 확인 하 고 새 강사를 데이터베이스에 추가 하는 템플릿 코드 보다 먼저 선택한 강좌를 강좌 탐색 속성에 추가 합니다. 모델 오류가 있는 경우에도 강좌를 추가 하 여 모델 오류가 발생 한 경우 (예: 사용자에 게 잘못 된 날짜를 입력 한 경우), 페이지가 오류 메시지와 함께 다시 표시 될 때 수행 된 모든 강좌 선택이 자동으로 복원 되도록 합니다.

`Courses` 탐색 속성에 강좌를 추가할 수 있도록 빈 컬렉션으로 속성을 초기화해야 합니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample26.cs)]

컨트롤러 코드에서 이 작업을 수행하는 대안으로 다음 예제와 같이 존재하지 않는 경우 자동으로 컬렉션을 만들도록 getter 속성을 변경하여 강사 모델에서 해당 작업을 수행할 수 있습니다.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample27.cs)]

이러한 방식으로 `Courses` 속성을 수정하는 경우 컨트롤러에서 명시적 속성 초기화 코드를 제거할 수 있습니다.

*Views\Instructor\Create.cshtml*에서 채용 날짜 필드와 **제출** 단추 앞에 사무실 위치 텍스트 상자와 코스 확인란을 추가 합니다.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample28.cshtml)]

코드를 붙여넣은 후에는 편집 페이지에 대해 이전 처럼 줄 바꿈 및 들여쓰기를 수정 합니다.

만들기 페이지를 실행 하 고 강사를 추가 합니다.

<a id="transactions"></a>

## <a name="handling-transactions"></a>트랜잭션 처리

기본 [CRUD 기능 자습서](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)에서 설명 했 듯이 기본적으로 Entity Framework는 트랜잭션을 암시적으로 구현 합니다. 더 많은 제어가 필요한 시나리오의 경우 (예: 트랜잭션에 Entity Framework 외부에서 수행 된 작업을 포함 하려는 경우 MSDN에서 [트랜잭션 작업](https://msdn.microsoft.com/data/dn456843) 을 참조 하세요.

## <a name="get-the-code"></a>코드 가져오기

[완료 된 프로젝트 다운로드](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>추가 리소스

[ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)에서 다른 Entity Framework 리소스에 대 한 링크를 찾을 수 있습니다.

## <a name="next-step"></a>다음 단계

이 자습서에서는 다음을 수행합니다.

> [!div class="checklist"]
> * 사용자 지정 된 과정 페이지
> * 강사 페이지에 office를 추가 했습니다.
> * 강사 페이지에 과정 추가
> * 업데이트 된 DeleteConfirmed
> * 만들기 페이지에 office 위치 및 코스 추가

비동기 프로그래밍 모델을 구현 하는 방법에 대해 알아보려면 다음 문서로 이동 합니다.
> [!div class="nextstepaction"]
> [비동기 프로그래밍 모델](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application.md)
