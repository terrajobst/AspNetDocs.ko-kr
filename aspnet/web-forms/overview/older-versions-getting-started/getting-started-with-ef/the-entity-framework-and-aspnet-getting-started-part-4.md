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
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-4"></a>Entity Framework 4.0 Database First 및 ASP.NET 4 Web Forms 시작-4 부

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

> Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 4.0 및 Visual Studio 2010를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](the-entity-framework-and-aspnet-getting-started-part-1.md) 를 참조 하십시오.

## <a name="working-with-related-data"></a>관련 데이터 작업

이전 자습서에서는 데이터를 필터링, 정렬 및 그룹화 하는 `EntityDataSource` 컨트롤을 사용 했습니다. 이 자습서에서는 관련 데이터를 표시 하 고 업데이트 합니다.

강사 목록을 보여 주는 강사 페이지를 만듭니다. 강사를 선택 하면 해당 강사가 학습 한 과정의 목록이 표시 됩니다. 강좌를 선택 하면 과정에 대 한 세부 정보와 강좌에 등록 된 학생 목록이 표시 됩니다. 강사 이름, 채용 날짜 및 사무실 할당을 편집할 수 있습니다. 사무실 할당은 탐색 속성을 통해 액세스 하는 별도의 엔터티 집합입니다.

태그 또는 코드에서 마스터 데이터를 정보 데이터에 연결할 수 있습니다. 자습서의이 부분에서는 두 가지 방법을 모두 사용 합니다.

[![Image01](the-entity-framework-and-aspnet-getting-started-part-4/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image1.png)

## <a name="displaying-and-updating-related-entities-in-a-gridview-control"></a>GridView 컨트롤에서 관련 엔터티 표시 및 업데이트

*Site.master* 마스터 페이지를 사용 하는 *강사 .aspx* 라는 새 웹 페이지를 만들고 `Content2`이라는 `Content` 컨트롤에 다음 태그를 추가 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample1.aspx)]

이 태그는 강사를 선택 하 고 업데이트를 사용 하도록 설정 하는 `EntityDataSource` 컨트롤을 만듭니다. `div` 요소는 왼쪽에 렌더링할 태그를 구성 하므로 나중에 열을 추가할 수 있습니다.

`EntityDataSource` 태그와 closing `</div>` 태그 사이에 오류 메시지에 사용할 `GridView` 컨트롤 및 `Label` 컨트롤을 만드는 다음 태그를 추가 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample2.aspx)]

이 `GridView` 컨트롤은 행 선택을 가능 하 게 하 고, 선택한 행을 밝은 회색 배경색으로 강조 표시 하 고, `SelectedIndexChanged` 및 `Updating` 이벤트에 대해 나중에 만들 처리기를 지정 합니다. 또한 선택한 행의 키 값을 나중에 추가할 다른 컨트롤에 전달할 수 있도록 `DataKeyNames` 속성에 대 한 `PersonID`를 지정 합니다.

마지막 열에는 연결 된 엔터티에서 제공 되기 때문에 `Person` 엔터티의 탐색 속성에 저장 되는 강사의 사무실 할당이 포함 됩니다. `GridView` 컨트롤이 업데이트를 위해 탐색 속성에 직접 바인딩할 수 없기 때문에 `EditItemTemplate` 요소는 `Bind`대신 `Eval`를 지정 합니다. 코드에서 office 할당을 업데이트 합니다. 이렇게 하려면 `TextBox` 컨트롤에 대 한 참조가 필요 하며, `TextBox` 컨트롤의 `Init` 이벤트에서 가져오고 저장 합니다.

`GridView` 컨트롤 다음에는 오류 메시지에 사용 되는 `Label` 컨트롤이 있습니다. 컨트롤의 `Visible` 속성이 `false`되 고 뷰 상태가 해제 되어 코드에서 오류에 대 한 응답으로 표시 되는 경우에만 레이블이 표시 됩니다.

*Instructors.aspx.cs* 파일을 열고 다음 `using` 문을 추가 합니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample3.cs)]

부분 클래스 이름 선언 바로 뒤에 개인 클래스 필드를 추가 하 여 office 할당 텍스트 상자에 대 한 참조를 저장 합니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample4.cs)]

나중에 코드를 추가할 `SelectedIndexChanged` 이벤트 처리기에 대 한 스텁을 추가 합니다. 또한 `TextBox` 컨트롤에 대 한 참조를 저장할 수 있도록 office 할당 `TextBox` 컨트롤의 `Init` 이벤트에 대 한 처리기를 추가 합니다. 이 참조를 사용 하 여 탐색 속성과 연결 된 엔터티를 업데이트 하기 위해 사용자가 입력 한 값을 가져옵니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample5.cs)]

`GridView` 컨트롤의 `Updating` 이벤트를 사용 하 여 연결 된 `OfficeAssignment` 엔터티의 `Location` 속성을 업데이트 합니다. `Updating` 이벤트에 대 한 다음 처리기를 추가 합니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample6.cs)]

이 코드는 사용자가 `GridView` 행에서 **업데이트** 를 클릭 하면 실행 됩니다. 이 코드는 LINQ to Entities를 사용 하 여 이벤트 인수에서 선택한 행의 `PersonID`를 사용 하 여 현재 `Person` 엔터티와 연결 된 `OfficeAssignment` 엔터티를 검색 합니다.

그런 다음 `InstructorOfficeTextBox` 컨트롤의 값에 따라 코드에서 다음 작업 중 하나를 수행 합니다.

- 텍스트 상자에 값이 있고 업데이트할 `OfficeAssignment` 엔터티가 없으면 하나를 만듭니다.
- 입력란에 값이 있고 `OfficeAssignment` 엔터티가 있으면 `Location` 속성 값을 업데이트 합니다.
- 입력란이 비어 있고 `OfficeAssignment` 엔터티가 있으면 해당 엔터티를 삭제 합니다.

그 후에는 변경 내용을 데이터베이스에 저장 합니다. 예외가 발생 하면 오류 메시지가 표시 됩니다.

페이지를 실행 합니다.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-4/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image3.png)

**편집** 을 클릭 하면 모든 필드가 텍스트 상자로 변경 됩니다.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-4/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image5.png)

**사무실 할당**을 포함 하 여 이러한 값을 변경 합니다. **업데이트** 를 클릭 하면 목록에 반영 된 변경 내용이 표시 됩니다.

## <a name="displaying-related-entities-in-a-separate-control"></a>별도의 컨트롤에 관련 엔터티 표시

각 강사는 하나 이상의 과정을 학습할 수 있으므로 강사 `GridView` 컨트롤에서 선택한 강사와 관련 된 과정을 나열 하는 `EntityDataSource` 컨트롤과 `GridView` 컨트롤을 추가 합니다. 코스 엔터티에 대 한 머리글 및 `EntityDataSource` 컨트롤을 만들려면 오류 메시지 `Label` 컨트롤과 닫는 `</div>` 태그 사이에 다음 태그를 추가 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample7.aspx)]

`Where` 매개 변수에는 `InstructorsGridView` 컨트롤에서 해당 행이 선택 된 강사의 `PersonID` 값이 포함 됩니다. `Where` 속성에는 `Course` 엔터티의 `People` 탐색 속성에서 연결 된 모든 `Person` 엔터티를 가져오고, 연결 된 `Course` 엔터티 중 하나에 선택한 `Person` 값이 포함 된 경우에만 `PersonID` 엔터티를 선택 하는 하위 select 명령이 포함 되어 있습니다.

`GridView` 컨트롤을 만들려면 `CoursesEntityDataSource` 컨트롤 바로 뒤에 다음 태그를 추가 합니다 (닫는 `</div>` 태그 앞).

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample8.aspx)]

강사를 선택 하지 않은 경우에는 코스가 표시 되지 않으므로 `EmptyDataTemplate` 요소가 포함 됩니다.

페이지를 실행 합니다.

[![Image04](the-entity-framework-and-aspnet-getting-started-part-4/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image7.png)

하나 이상의 강좌가 할당 된 강사를 선택 하면 목록에 강좌 또는 강좌가 표시 됩니다. (참고: 데이터베이스 스키마는 여러 과정을 허용 하지만, 데이터베이스에 제공 된 테스트 데이터에는 실제로 두 개 이상의 강좌가 있습니다. **서버 탐색기** 창이 나 이후 자습서에서 추가할 *CoursesAdd* 페이지를 사용 하 여 데이터베이스에 과정을 직접 추가할 수 있습니다.

[![Image05](the-entity-framework-and-aspnet-getting-started-part-4/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image9.png)

`CoursesGridView` 컨트롤은 몇 가지 과정 필드만 표시 합니다. 강좌에 대 한 모든 세부 정보를 표시 하려면 사용자가 선택 하는 과정에 대 한 `DetailsView` 컨트롤을 사용 합니다. *강사 .aspx*에서 닫는 `</div>` 태그 뒤에 다음 태그를 추가 합니다 .이 태그는 앞에 있지 않고 닫는 div 태그 **뒤** 에 위치 해야 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample9.aspx)]

이 태그는 `Courses` 엔터티 집합에 바인딩된 `EntityDataSource` 컨트롤을 만듭니다. `Where` 속성은 과정 `GridView` 컨트롤에서 선택 된 행의 `CourseID` 값을 사용 하 여 과정을 선택 합니다. 태그는 나중에 학생 등급을 표시 하는 데 사용 하는 `Selected` 이벤트에 대 한 처리기를 지정 합니다 .이 이벤트는 계층 구조의 다른 수준 보다 낮습니다.

*Instructors.aspx.cs*에서 `CourseDetailsEntityDataSource_Selected` 메서드에 대 한 다음 스텁을 만듭니다. 이 스텁은 자습서의 뒷부분에서 자세히 설명 합니다. 지금은 페이지를 컴파일하고 실행 하는 데 필요 합니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample10.cs)]

페이지를 실행 합니다.

[![Image06](the-entity-framework-and-aspnet-getting-started-part-4/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image11.png)

처음에는 강좌를 선택 하지 않았으므로 강좌 정보가 없습니다. 코스가 할당 된 강사를 선택 하 고 세부 정보를 볼 수 있는 과정을 선택 합니다.

[![Image07](the-entity-framework-and-aspnet-getting-started-part-4/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image13.png)

## <a name="using-the-entitydatasource-selected-event-to-display-related-data"></a>EntityDataSource "Selected" 이벤트를 사용 하 여 관련 데이터 표시

마지막으로, 선택한 과정에 대해 등록 된 학생 및 해당 등급을 모두 표시 하려고 합니다. 이렇게 하려면 과정 `DetailsView`에 바인딩된 `EntityDataSource` 컨트롤의 `Selected` 이벤트를 사용 합니다.

*강사 .aspx*에서 `DetailsView` 컨트롤 뒤에 다음 태그를 추가 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample11.aspx)]

이 태그는 학생 목록과 선택한 과정의 등급을 표시 하는 `ListView` 컨트롤을 만듭니다. 컨트롤을 코드에 데이터 바인딩할 수 있기 때문에 데이터 소스를 지정 하지 않았습니다. `EmptyDataTemplate` 요소는 강좌를 선택 하지 않은 경우 표시할 메시지를 제공 합니다 .이 경우에는 표시할 학생이 없는 것입니다. `LayoutTemplate` 요소는 목록을 표시 하는 HTML 테이블을 만들고 `ItemTemplate`는 표시할 열을 지정 합니다. 학생 ID와 학생 등급은 `StudentGrade` 엔터티에서 가져온 것 이며, 학생 이름은 Entity Framework에서 `StudentGrade` 엔터티의 `Person` 탐색 속성에 사용할 수 있도록 하는 `Person` 엔터티에서 가져온 것입니다.

*Instructors.aspx.cs*에서 스텁 `CourseDetailsEntityDataSource_Selected` 메서드를 다음 코드로 바꿉니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample12.cs)]

이 이벤트에 대 한 이벤트 인수는 선택한 데이터를 컬렉션 형식으로 제공 합니다 .이는 선택 된 항목이 없는 경우에는 0이 고, `Course` 엔터티가 선택 되어 있으면 항목이 하나 있습니다. `Course` 엔터티를 선택 하는 경우 코드는 `First` 메서드를 사용 하 여 컬렉션을 단일 개체로 변환 합니다. 그런 다음 탐색 속성에서 `StudentGrade` 엔터티를 가져와 컬렉션으로 변환한 다음 `GradesListView` 컨트롤을 컬렉션에 바인딩합니다.

이는 점수를 표시 하는 데 충분 하지만 페이지가 처음 표시 될 때 그리고 강좌를 선택 하지 않은 경우에는 빈 데이터 템플릿의 메시지가 표시 되도록 해야 합니다. 이렇게 하려면 다음 메서드를 만듭니다 .이 메서드는 다음 두 위치에서 호출 됩니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample13.cs)]

페이지가 처음 표시 될 때 빈 데이터 템플릿을 표시 하려면 `Page_Load` 메서드에서이 새 메서드를 호출 합니다. `InstructorsGridView_SelectedIndexChanged` 메서드에서이 메서드를 호출 합니다 .이 이벤트는 강사를 선택할 때 발생 합니다. 즉, 새 강좌가 과정 `GridView` 컨트롤에 로드 되 고 없음이 아직 선택 되지 않았음을 의미 합니다. 다음은 두 호출입니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample14.cs)]

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample15.cs)]

페이지를 실행 합니다.

[![Image08](the-entity-framework-and-aspnet-getting-started-part-4/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image15.png)

코스가 할당 된 강사를 선택 하 고 강좌를 선택 합니다.

[![Image09](the-entity-framework-and-aspnet-getting-started-part-4/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image17.png)

이제 관련 데이터로 작업 하는 몇 가지 방법을 살펴보았습니다. 다음 자습서에서는 기존 엔터티 간에 관계를 추가 하는 방법, 관계를 제거 하는 방법 및 기존 엔터티에 대 한 관계를 포함 하는 새 엔터티를 추가 하는 방법에 대해 알아봅니다.

> [!div class="step-by-step"]
> [이전](the-entity-framework-and-aspnet-getting-started-part-3.md)
> [다음](the-entity-framework-and-aspnet-getting-started-part-5.md)
