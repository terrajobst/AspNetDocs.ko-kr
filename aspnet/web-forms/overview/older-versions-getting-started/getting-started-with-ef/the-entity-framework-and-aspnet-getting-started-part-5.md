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
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-5"></a>Entity Framework 4.0 Database First 및 ASP.NET 4 Web Forms 시작-5 부

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

> Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 4.0 및 Visual Studio 2010를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](the-entity-framework-and-aspnet-getting-started-part-1.md) 를 참조 하십시오.

## <a name="working-with-related-data-continued"></a>관련 데이터 작업, 계속

이전 자습서에서는 `EntityDataSource` 컨트롤을 사용 하 여 관련 데이터 작업을 시작 했습니다. 탐색 속성에서 여러 수준의 계층 및 편집 된 데이터를 표시 했습니다. 이 자습서에서는 관계를 추가 및 삭제 하 고 기존 엔터티에 대 한 관계를 포함 하는 새 엔터티를 추가 하 여 관련 데이터를 계속 해 서 사용할 수 있습니다.

부서에 할당 된 과정을 추가 하는 페이지를 만듭니다. 부서는 이미 존재 하 고 새 과정을 만들 때 동시에 기존 부서와 기존 부서 간의 관계를 설정 합니다.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image1.png)

강의를 강좌에 할당 하 여 다 대 다 관계에서 작동 하는 페이지를 만들 수도 있습니다. (선택한 두 엔터티 간의 관계를 추가 하거나) 강좌에서 강사를 제거 합니다 (두 엔터티 간의 관계 제거 을 선택 합니다. 데이터베이스에서 강사와 강좌 간에 관계를 추가 하면 `CourseInstructor` 연결 테이블에 새 행이 추가 됩니다. 관계를 제거 하려면 `CourseInstructor` 연결 테이블에서 행을 삭제 해야 합니다. 그러나 `CourseInstructor` 테이블을 명시적으로 참조 하지 않고 탐색 속성을 설정 하 여 Entity Framework에서이 작업을 수행 합니다.

[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image3.png)

## <a name="adding-an-entity-with-a-relationship-to-an-existing-entity"></a>관계를 사용 하 여 기존 엔터티에 엔터티 추가

*Site.master* 마스터 페이지를 사용 하는 *CoursesAdd* 라는 새 웹 페이지를 만들고 `Content2`이라는 `Content` 컨트롤에 다음 태그를 추가 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample1.aspx)]

이 태그는 삽입을 가능 하 게 하 고 `Inserting` 이벤트에 대 한 처리기를 지정 하는 과정을 선택 하는 `EntityDataSource` 컨트롤을 만듭니다. 새 `Course` 엔터티를 만들 때 처리기를 사용 하 여 `Department` 탐색 속성을 업데이트 합니다.

또한 태그는 새 `Course` 엔터티를 추가 하는 데 사용할 `DetailsView` 컨트롤을 만듭니다. 태그는 `Course` 엔터티 속성에 바인딩된 필드를 사용 합니다. 시스템 생성 ID 필드가 아니기 때문에 `CourseID` 값을 입력 해야 합니다. 대신 코스가 생성 될 때 수동으로 지정 해야 하는 과정 번호입니다.

탐색 속성은 `BoundField` 컨트롤과 함께 사용할 수 없으므로 `Department` 탐색 속성에 템플릿 필드를 사용 합니다. 템플릿 필드는 부서를 선택할 수 있는 드롭다운 목록을 제공 합니다. 드롭다운 목록은 `Bind`하는 대신 `Eval`를 사용 하 여 `Departments` 엔터티 집합에 바인딩되어 있습니다. 탐색 속성을 업데이트 하기 위해 직접 바인딩할 수 없기 때문입니다. `DepartmentID` 외래 키를 업데이트 하는 코드에서 사용할 수 있도록 컨트롤에 대 한 참조를 저장할 수 있도록 `DropDownList` 컨트롤의 `Init` 이벤트에 대 한 처리기를 지정 합니다.

Partial 클래스 선언 바로 뒤에 *CoursesAdd.aspx.cs* `DepartmentsDropDownList` 컨트롤에 대 한 참조를 보유 하는 클래스 필드를 추가 합니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample2.cs)]

컨트롤에 대 한 참조를 저장할 수 있도록 `DepartmentsDropDownList` 컨트롤의 `Init` 이벤트에 대 한 처리기를 추가 합니다. 이렇게 하면 사용자가 입력 한 값을 가져오고이를 사용 하 여 `Course` 엔터티의 `DepartmentID` 값을 업데이트할 수 있습니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample3.cs)]

`DetailsView` 컨트롤의 `Inserting` 이벤트에 대 한 처리기를 추가 합니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample4.cs)]

사용자가 `Insert`를 클릭 하면 새 레코드가 삽입 되기 전에 `Inserting` 이벤트가 발생 합니다. 처리기의 코드는 `DropDownList` 컨트롤에서 `DepartmentID`를 가져오고이를 사용 하 여 `Course` 엔터티의 `DepartmentID` 속성에 사용 될 값을 설정 합니다.

Entity Framework는이 과정을 관련 된 `Department` 엔터티의 `Courses` 탐색 속성에 추가 하는 과정을 처리 합니다. 또한 `Course` 엔터티의 `Department` 탐색 속성에 부서를 추가 합니다.

페이지를 실행 합니다.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image5.png)

ID, 제목, 크레딧 수를 입력 하 고 부서를 선택한 다음 **삽입**을 클릭 합니다.

*Default.aspx* 페이지를 실행 하 고 동일한 부서를 선택 하 여 새 강좌를 확인 합니다.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-5/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image7.png)

## <a name="working-with-many-to-many-relationships"></a>다 대 다 관계 작업

`Courses` 엔터티 집합과 `People` 엔터티 집합 간의 관계는 다 대 다 관계입니다. `Course` 엔터티에는 `People` 이라는 탐색 속성이 있습니다 .이 속성에는 해당 과정을 설명 하기 위해 할당 된 강사를 나타내는 0 개 이상의 관련 된 `Person` 엔터티가 포함 될 수 있습니다. 및 `Person` 엔터티에는 `Courses` 라는 탐색 속성이 있습니다 .이 속성은 0 개 이상의 관련 `Course` 엔터티 (강사가 학습에 할당 한 과정을 나타냄)를 포함할 수 있습니다. 한 강사는 여러 과정을 학습할 수 있으며, 한 강좌는 여러 강사가 배울 수 있습니다. 이 연습 섹션에서는 관련 엔터티의 탐색 속성을 업데이트 하 여 `Person`와 `Course` 엔터티 간의 관계를 추가 하 고 제거 합니다.

*Site.master* 마스터 페이지를 사용 하는 *InstructorsCourses* 라는 새 웹 페이지를 만들고 `Content2`이라는 `Content` 컨트롤에 다음 태그를 추가 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample5.aspx)]

이 태그는 강사를 위한 `Person` 엔터티의 이름과 `PersonID`를 검색 하는 `EntityDataSource` 컨트롤을 만듭니다. `DropDrownList` 컨트롤은 `EntityDataSource` 컨트롤에 바인딩됩니다. `DropDownList` 컨트롤은 `DataBound` 이벤트에 대 한 처리기를 지정 합니다. 이 처리기를 사용 하 여 코스를 표시 하는 두 개의 드롭다운 목록을 모두 바인딩할 수 있습니다.

태그는 또한 선택한 강사에 게 강좌를 할당 하는 데 사용할 다음 컨트롤 그룹을 만듭니다.

- 할당할 과정을 선택 하는 `DropDownList` 컨트롤입니다. 이 컨트롤은 현재 선택한 강사에 게 할당 되지 않은 과정으로 채워집니다.
- 할당을 시작 하는 `Button` 컨트롤입니다.
- 할당이 실패 하는 경우 오류 메시지를 표시 하는 `Label` 컨트롤입니다.

마지막으로, 태그는 선택한 강사 로부터 강좌를 제거 하는 데 사용할 컨트롤 그룹도 만듭니다.

*InstructorsCourses.aspx.cs*에서 using 문을 추가 합니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample6.cs)]

코스를 표시 하는 두 개의 드롭다운 목록을 채우는 메서드를 추가 합니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample7.cs)]

이 코드는 `Courses` 엔터티 집합에서 모든 과정을 가져오고 선택한 강사에 대 한 `Person` 엔터티의 `Courses` 탐색 속성에서 과정을 가져옵니다. 그런 다음 해당 강사에 게 할당 되는 과정을 결정 하 고 드롭다운 목록을 그에 따라 채웁니다.

`Assign` 단추의 `Click` 이벤트에 대 한 처리기를 추가 합니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample8.cs)]

이 코드는 선택한 강사의 `Person` 엔터티를 가져오고, 선택한 강좌에 대 한 `Course` 엔터티를 가져오고, 강사의 `Person` 엔터티의 `Courses` 탐색 속성에 선택한 과정을 추가 합니다. 그런 다음 변경 내용을 데이터베이스에 저장 하 고 드롭다운 목록을 다시 채웁니다. 그러면 결과가 즉시 표시 될 수 있습니다.

`Remove` 단추의 `Click` 이벤트에 대 한 처리기를 추가 합니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample9.cs)]

이 코드는 선택한 강사의 `Person` 엔터티를 가져오고, 선택한 강좌에 대 한 `Course` 엔터티를 가져오고, `Person` 엔터티의 `Courses` 탐색 속성에서 선택한 과정을 제거 합니다. 그런 다음 변경 내용을 데이터베이스에 저장 하 고 드롭다운 목록을 다시 채웁니다. 그러면 결과가 즉시 표시 될 수 있습니다.

보고할 오류가 없을 때 오류 메시지가 표시 되지 않도록 하는 `Page_Load` 메서드에 코드를 추가 하 고 `DataBound`에 대 한 처리기를 추가 하 고 강사 드롭다운 목록의 이벤트를 `SelectedIndexChanged` 하 여 강의 드롭다운 목록을 채웁니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample10.cs)]

페이지를 실행 합니다.

[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image9.png)

강사를 선택 합니다. <strong>강좌 할당</strong> 드롭다운 목록에는 강사가 학습 하지 않는 코스가 표시 되 고 <strong>강좌 제거</strong> 드롭다운 목록에는 강사가 이미 할당 된 강좌가 표시 됩니다. <strong>과정 할당</strong> 섹션에서 과정을 선택한 다음 <strong>할당</strong>을 클릭 합니다. 강좌는 <strong>과정 제거</strong> 드롭다운 목록으로 이동 합니다. <strong>강좌 제거</strong> 섹션에서 과정을 선택 하 고 <strong>제거</strong>를 클릭<em>합니다.</em> 강좌는 <strong>과정 할당</strong> 드롭다운 목록으로 이동 합니다.

이제 관련 데이터로 작업 하는 몇 가지 방법을 살펴보았습니다. 다음 자습서에서는 데이터 모델에서 상속을 사용 하 여 응용 프로그램의 유지 관리를 개선 하는 방법을 배웁니다.

> [!div class="step-by-step"]
> [이전](the-entity-framework-and-aspnet-getting-started-part-4.md)
> [다음](the-entity-framework-and-aspnet-getting-started-part-6.md)
