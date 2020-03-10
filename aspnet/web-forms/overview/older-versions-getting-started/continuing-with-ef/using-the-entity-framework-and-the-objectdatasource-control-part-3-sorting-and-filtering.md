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
# <a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-3-sorting-and-filtering"></a>Entity Framework 4.0 및 ObjectDataSource 컨트롤 사용, 3 부: 정렬 및 필터링

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

> 이 자습서 시리즈는 [Entity Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started) 자습서 시리즈 시작에서 만든 Contoso 대학 웹 응용 프로그램을 기반으로 합니다. 이전 자습서를 완료 하지 않은 경우이 자습서의 시작 점으로, 만든 [응용 프로그램을 다운로드할](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) 수 있습니다. 전체 자습서 시리즈에서 만든 [응용 프로그램을 다운로드할](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) 수도 있습니다. 자습서에 대 한 질문이 있는 경우 [ASP.NET Entity Framework 포럼](https://forums.asp.net/1227.aspx)에 게시할 수 있습니다.

이전 자습서에서는 Entity Framework 및 `ObjectDataSource` 컨트롤을 사용 하는 n 계층 웹 응용 프로그램에서 리포지토리 패턴을 구현 했습니다. 이 자습서에서는 마스터-세부 시나리오를 정렬 및 필터링 하 고 처리 하는 방법을 보여 줍니다. 다음과 같은 향상 된 기능을 *학과 페이지에 추가 합니다.*

- 사용자가 이름을 기준으로 부서를 선택할 수 있는 입력란입니다.
- 표에 표시 된 각 학과의 과정 목록입니다.
- 열 머리글을 클릭 하 여 정렬할 수 있습니다.

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)

## <a name="adding-the-ability-to-sort-gridview-columns"></a>GridView 열을 정렬 하는 기능 추가

학과 페이지 *를* 열고 `DepartmentsObjectDataSource`이라는 `ObjectDataSource` 컨트롤에 `SortParameterName="sortExpression"` 특성을 추가 합니다. 나중에 `sortExpression`이라는 매개 변수를 사용 하는 `GetDepartments` 메서드를 만듭니다. 이제 컨트롤의 여는 태그에 대 한 태그는 다음 예제와 유사 합니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample1.aspx)]

`GridView` 컨트롤의 여는 태그에 `AllowSorting="true"` 특성을 추가 합니다. 이제 컨트롤의 여는 태그에 대 한 태그는 다음 예제와 유사 합니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample2.aspx)]

*Departments.aspx.cs*에서 `Page_Load` 메서드에서 `GridView` 컨트롤의 `Sort` 메서드를 호출 하 여 기본 정렬 순서를 설정 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample3.cs)]

비즈니스 논리 클래스 또는 리포지토리 클래스에서 또는 필터를 정렬 하는 코드를 추가할 수 있습니다. 비즈니스 논리 클래스에서 수행 하는 경우 데이터를 데이터베이스에서 검색 한 후 정렬 또는 필터링 작업이 수행 됩니다. 비즈니스 논리 클래스가 리포지토리에서 반환 된 `IEnumerable` 개체를 사용 하 고 있기 때문입니다. 리포지토리 클래스에서 정렬 및 필터링 코드를 추가 하 고 LINQ 식 또는 개체 쿼리가 `IEnumerable` 개체로 변환 되기 전에 수행 하는 경우, 처리를 위해 명령이 데이터베이스로 전달 되며이는 일반적으로 더 효율적입니다. 이 자습서에서는 데이터베이스에서 처리를 수행 하는 방식으로 (즉, 리포지토리에서) 정렬과 필터링을 구현 합니다.

정렬 기능을 추가 하려면 리포지토리 인터페이스 및 리포지토리 클래스 뿐만 아니라 비즈니스 논리 클래스에 새 메서드를 추가 해야 합니다. *ISchoolRepository.cs* 파일에서 반환 되는 부서 목록을 정렬 하는 데 사용 되는 `sortExpression` 매개 변수를 사용 하는 새 `GetDepartments` 메서드를 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample4.cs)]

`sortExpression` 매개 변수는 정렬 기준이 되는 열과 정렬 방향을 지정 합니다.

새 메서드에 대 한 코드를 *SchoolRepository.cs* 파일에 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample5.cs)]

매개 변수가 없는 기존 `GetDepartments` 메서드를 변경 하 여 새 메서드를 호출 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample6.cs)]

테스트 프로젝트에서 *MockSchoolRepository.cs*에 다음 새 메서드를 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample7.cs)]

정렬 된 목록을 반환 하는이 메서드에 종속 된 단위 테스트를 만들려는 경우에는 반환 하기 전에 목록을 정렬 해야 합니다. 이 자습서에서와 같은 테스트를 만들 수 없으므로 메서드는 정렬 되지 않은 부서 목록만 반환할 수 있습니다.

*SchoolBL.cs* 파일에서 비즈니스 논리 클래스에 다음과 같은 새 메서드를 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample8.cs)]

이 코드는 sort 매개 변수를 리포지토리 메서드에 전달 합니다.

*부서 .aspx* 페이지를 실행 합니다.

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)

이제 열 머리글을 클릭 하 여 해당 열을 기준으로 정렬할 수 있습니다. 열이 이미 정렬 된 경우 머리글을 클릭 하면 정렬 방향이 반전 됩니다.

## <a name="adding-a-search-box"></a>검색 상자 추가

이 섹션에서는 검색 텍스트 상자를 추가 하 고, 컨트롤 매개 변수를 사용 하 여 `ObjectDataSource` 컨트롤에 연결 하 고, 필터링을 지원 하기 위해 비즈니스 논리 클래스에 메서드를 추가 합니다.

학과 페이지 *를* 열고 머리글과 첫 번째 `ObjectDataSource` 컨트롤 사이에 다음 태그를 추가 합니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample9.aspx)]

`DepartmentsObjectDataSource`이라는 `ObjectDataSource` 컨트롤에서 다음을 수행 합니다.

- `SearchTextBox` 컨트롤에 입력 한 값을 가져오는 `nameSearchString` 이라는 매개 변수에 대 한 `SelectParameters` 요소를 추가 합니다.
- `SelectMethod` 특성 값을 `GetDepartmentsByName`로 변경 합니다. 이 메서드는 나중에 만듭니다.

이제 `ObjectDataSource` 컨트롤의 태그는 다음 예제와 유사 합니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample10.aspx)]

*ISchoolRepository.cs*에서 `sortExpression` 및 `nameSearchString` 매개 변수를 모두 사용 하는 `GetDepartmentsByName` 메서드를 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample11.cs)]

*SchoolRepository.cs*에 다음과 같은 새 메서드를 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample12.cs)]

이 코드는 `Where` 메서드를 사용 하 여 검색 문자열이 포함 된 항목을 선택 합니다. 검색 문자열이 비어 있으면 모든 레코드가 선택 됩니다. 예 `Where``OrderBy`를 들어`Include`와 같은 한 문에 메서드 호출을 함께 지정 하는 경우 `Where` 메서드는 항상 마지막 이어야 합니다.

`sortExpression` 매개 변수를 사용 하 여 새 메서드를 호출 하는 기존 `GetDepartments` 메서드를 변경 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample13.cs)]

테스트 프로젝트의 *MockSchoolRepository.cs* 에 다음과 같은 새 메서드를 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample14.cs)]

*SchoolBL.cs*에 다음과 같은 새 메서드를 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample15.cs)]

학과 페이지 *를* 실행 하 고 검색 문자열을 입력 하 여 선택 논리가 작동 하는지 확인 합니다. 텍스트 상자를 비워 두고 검색을 시도 하 여 모든 레코드가 반환 되는지 확인 합니다.

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)

## <a name="adding-a-details-column-for-each-grid-row"></a>각 표 형태 창의 행에 대 한 세부 정보 열 추가

다음으로 표의 오른쪽 셀에 표시 되는 각 학과의 모든 과정을 확인 하려고 합니다. 이렇게 하려면 중첩 된 `GridView` 컨트롤을 사용 하 고이를 `Department` 엔터티의 `Courses` 탐색 속성의 데이터에 데이터 바인딩할 수 있습니다.

학과 *.aspx* 를 열고 `GridView` 컨트롤에 대 한 태그에서 `RowDataBound` 이벤트에 대 한 처리기를 지정 합니다. 이제 컨트롤의 여는 태그에 대 한 태그는 다음 예제와 유사 합니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample16.aspx)]

`Administrator` 템플릿 필드 뒤에 새 `TemplateField` 요소를 추가 합니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample17.aspx)]

이 태그는 과정 번호와 코스 목록의 제목을 표시 하는 중첩 된 `GridView` 컨트롤을 만듭니다. `RowDataBound` 처리기에서 코드에 데이터를 바인딩할 수 있기 때문에 데이터 소스를 지정 하지 않습니다.

*Departments.aspx.cs* 를 열고 `RowDataBound` 이벤트에 대 한 다음 처리기를 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample18.cs)]

이 코드는 이벤트 인수에서 `Department` 엔터티를 가져오고 `Courses` 탐색 속성을 `List` 컬렉션으로 변환한 다음 중첩 된 `GridView`를 컬렉션에 열의.

*SchoolRepository.cs* 파일을 열고 `GetDepartmentsByName` 메서드에서 만든 개체 쿼리에서 `Include` 메서드를 호출 하 여 `Courses` 탐색 속성에 대해 즉시 로드를 지정 합니다. 이제 `GetDepartmentsByName` 메서드의 `return` 문은 다음 예제와 유사 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample19.cs)]

페이지를 실행 합니다. 이전에 추가한 정렬 및 필터링 기능 외에도 GridView 컨트롤에는 각 부서에 대 한 중첩 된 과정 세부 정보가 표시 됩니다.

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)

이렇게 하면 정렬, 필터링 및 마스터-세부 시나리오에 대 한 소개를 완료 합니다. 다음 자습서에서는 동시성을 처리 하는 방법을 알아봅니다.

> [!div class="step-by-step"]
> [이전](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
> [다음](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)
