---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-3
title: Entity Framework 4.0 Database First 및 ASP.NET 4 Web Forms 시작-3 단계 | Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 응용 프로그램 샘플은 ...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: ccdc3f8c-2568-40a7-8f8b-3c23d2e05388
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-3
msc.type: authoredcontent
ms.openlocfilehash: 88debb11a9157dce9ff000b1cb459b876dbceaf3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78522641"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-3"></a>Entity Framework 4.0 Database First 및 ASP.NET 4 Web Forms 시작-3 부

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

> Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 4.0 및 Visual Studio 2010를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](the-entity-framework-and-aspnet-getting-started-part-1.md) 를 참조 하십시오.

## <a name="filtering-ordering-and-grouping-data"></a>데이터 필터링, 정렬 및 그룹화

이전 자습서에서는 데이터를 표시 하 고 편집 하는 `EntityDataSource` 컨트롤을 사용 했습니다. 이 자습서에서는 데이터를 필터링, 정렬 및 그룹화 합니다. `EntityDataSource` 컨트롤의 속성을 설정 하 여이 작업을 수행 하는 경우 구문은 다른 데이터 소스 컨트롤과 다릅니다. 그러나 이러한 차이를 최소화 하기 위해 `QueryExtender` 컨트롤을 사용할 수 있습니다.

학생을 필터링 하 고 이름을 기준으로 정렬 하 고 이름으로 검색 하려면 *학습자* 페이지를 변경 합니다. 또한 코스 *.aspx* 페이지를 변경 하 여 선택한 부서에 대 한 과정을 표시 하 고 이름으로 과정을 검색 합니다. 마지막으로 *About .aspx* 페이지에 학생 통계를 추가 합니다.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-3/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image1.png)

[![Image11](the-entity-framework-and-aspnet-getting-started-part-3/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image3.png)

[![Image10](the-entity-framework-and-aspnet-getting-started-part-3/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image5.png)

[![Image14](the-entity-framework-and-aspnet-getting-started-part-3/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image7.png)

## <a name="using-the-entitydatasource-where-property-to-filter-data"></a>EntityDataSource "Where" 속성을 사용 하 여 데이터 필터링

이전 자습서에서 만든 *학생용 .aspx* 페이지를 엽니다. 현재 구성 된 대로 페이지의 `GridView` 컨트롤에 `People` 엔터티 집합의 모든 이름이 표시 됩니다. 그러나 null이 아닌 등록 날짜가 있는 엔터티 `Person` 선택 하 여 찾을 수 있는 학생만 표시 하려고 합니다.

**디자인** 뷰로 전환 하 고 `EntityDataSource` 컨트롤을 선택 합니다. **속성** 창에서 `Where` 속성을 `it.EnrollmentDate is not null`로 설정합니다.

[![Image01](the-entity-framework-and-aspnet-getting-started-part-3/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image9.png)

`EntityDataSource` 컨트롤의 `Where` 속성에서 사용 하는 구문은 Entity SQL입니다. Entity SQL는 Transact-sql과 유사 하지만 데이터베이스 개체가 아닌 엔터티에서 사용 하도록 사용자 지정 됩니다. 식 `it.EnrollmentDate is not null`에서 `it` 단어는 쿼리에서 반환 되는 엔터티에 대 한 참조를 나타냅니다. 따라서 `it.EnrollmentDate`는 `EntityDataSource` 컨트롤이 반환 하는 `Person` 엔터티의 `EnrollmentDate` 속성을 참조 합니다.

페이지를 실행 합니다. 학생 목록에는 이제 학생만 포함 됩니다. 등록 날짜를 표시 하지 않는 행은 표시 되지 않습니다.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-3/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image11.png)

## <a name="using-the-entitydatasource-orderby-property-to-order-data"></a>EntityDataSource "OrderBy" 속성을 사용 하 여 데이터 정렬

또한이 목록이 처음 표시 될 때 이름 순서로 표시 되도록 합니다. *학습자* 페이지가 **디자인** 뷰에서 열려 있는 상태에서 `EntityDataSource` 컨트롤을 선택한 상태로 **속성** 창에서 **OrderBy** 속성을 `it.LastName`로 설정 합니다.

[![Image05](the-entity-framework-and-aspnet-getting-started-part-3/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image13.png)

페이지를 실행 합니다. 학생 목록은 이제 성을 기준으로 정렬 됩니다.

[![Image04](the-entity-framework-and-aspnet-getting-started-part-3/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image15.png)

## <a name="using-a-control-parameter-to-set-the-where-property"></a>컨트롤 매개 변수를 사용 하 여 "Where" 속성 설정

다른 데이터 소스 컨트롤과 마찬가지로 `Where` 속성에 매개 변수 값을 전달할 수 있습니다. 자습서의 2 부에서 만든 *과정 .aspx* 페이지에서이 방법을 사용 하 여 사용자가 드롭다운 목록에서 선택한 부서와 관련 된 과정을 표시할 수 있습니다.

*코스 .aspx* 를 열고 **디자인** 뷰로 전환 합니다. 페이지에 두 번째 `EntityDataSource` 컨트롤을 추가 하 고 이름을 `CoursesEntityDataSource`에 추가 합니다. `SchoolEntities` 모델에 연결 하 고 **EntitySetName** 값으로 `Courses`를 선택 합니다.

**속성** 창의 **Where** 속성 상자에서 줄임표를 클릭 합니다. **속성** 창을 사용 하기 전에 `CoursesEntityDataSource` 컨트롤이 계속 선택 되어 있는지 확인 합니다.

[![Image06](the-entity-framework-and-aspnet-getting-started-part-3/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image17.png)

**식 편집기** 대화 상자가 표시 됩니다. 이 대화 상자에서 **제공 된 매개 변수를 기반으로 Where 식 자동 생성**을 선택 하 고 **매개 변수 추가**를 클릭 합니다. 매개 변수의 이름을 `DepartmentID`하 고 **Control** 을 **매개 변수 원본** 값으로 선택 하 고 **DepartmentsDropDownList** 를 **ControlID** 값으로 선택 합니다.

[![Image07](the-entity-framework-and-aspnet-getting-started-part-3/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image19.png)

**고급 속성 표시**를 클릭 하 고 **식 편집기** 대화 상자의 **속성** 창에서 `Type` 속성을 `Int32`로 변경 합니다.

[![Image15](the-entity-framework-and-aspnet-getting-started-part-3/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image21.png)

완료되면 **확인**을 클릭합니다.

드롭다운 목록 아래에서 페이지에 `GridView` 컨트롤을 추가 하 고 이름을 `CoursesGridView`로 표시 합니다. `CoursesEntityDataSource` 데이터 소스 컨트롤에 연결 하 고, **스키마 새로 고침**을 클릭 하 고, **열 편집**을 클릭 하 고, `DepartmentID` 열을 제거 합니다. `GridView` 컨트롤 태그는 다음 예제와 유사 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample1.aspx)]

사용자가 드롭다운 목록에서 선택한 부서를 변경 하는 경우 관련 과정 목록이 자동으로 변경 되는 것을 볼 수 있습니다. 이렇게 하려면 드롭다운 목록을 선택 하 고 **속성** 창에서 `AutoPostBack` 속성을 `True`로 설정 합니다.

[![Image08](the-entity-framework-and-aspnet-getting-started-part-3/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image23.png)

이제 디자이너 사용을 완료 했으므로 **원본** 뷰로 전환 하 고 `CoursesEntityDataSource` 컨트롤의 `ConnectionString` 및 `DefaultContainer` name 속성을 `ContextTypeName="ContosoUniversity.DAL.SchoolEntities"` 특성으로 바꿉니다. 완료 되 면 컨트롤의 태그는 다음 예제와 같이 표시 됩니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample2.aspx)]

페이지를 실행 하 고 드롭다운 목록을 사용 하 여 다른 부서를 선택 합니다. 선택한 부서에서 제공 하는 강좌가 `GridView` 컨트롤에 표시 됩니다.

[![Image09](the-entity-framework-and-aspnet-getting-started-part-3/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image25.png)

## <a name="using-the-entitydatasource-groupby-property-to-group-data"></a>EntityDataSource "GroupBy" 속성을 사용 하 여 데이터 그룹화

Contoso 대학이 정보 페이지에 몇 가지 학생 통계를 추가 하려고 한다고 가정 합니다. 특히 등록 된 날짜별로 학생 수의 분석을 표시 하려고 합니다.

*Default.aspx*를 열고 **소스** 뷰에서 `BodyContent` 컨트롤의 기존 내용을 `h2` 태그 간에 "학생 본문 통계"로 바꿉니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample3.aspx)]

제목 뒤에 `EntityDataSource` 컨트롤을 추가 하 고 이름을 `StudentStatisticsEntityDataSource`로 이름을로 합니다. `SchoolEntities`에 연결 하 고, `People` 엔터티 집합을 선택 하 고, 마법사에서 **선택** 상자를 변경 되지 않은 상태로 둡니다. **속성** 창에서 다음 속성을 설정 합니다.

- 학생용 으로만 필터링 하려면 `Where` 속성을 `it.EnrollmentDate is not null`로 설정 합니다.
- 등록 날짜를 기준으로 결과를 그룹화 하려면 `GroupBy` 속성을 `it.EnrollmentDate`로 설정 합니다.
- 등록 날짜와 학생 수를 선택 하려면 `Select` 속성을 `it.EnrollmentDate, Count(it.EnrollmentDate) AS NumberOfStudents`로 설정 합니다.
- 등록 날짜를 기준으로 결과를 정렬 하려면 `OrderBy` 속성을 `it.EnrollmentDate`로 설정 합니다.

**소스** 뷰에서 `ConnectionString` 및 `DefaultContainer` name 속성을 `ContextTypeName` 속성으로 바꿉니다. 이제 `EntityDataSource` 컨트롤 태그는 다음 예제와 유사 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample4.aspx)]

`Select`, `GroupBy`및 `Where` 속성의 구문은 현재 엔터티를 지정 하는 `it` 키워드를 제외 하 고 Transact-sql과 비슷합니다.

다음 태그를 추가 하 여 데이터를 표시 하는 `GridView` 컨트롤을 만듭니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample5.aspx)]

페이지를 실행 하 여 등록 날짜별 학생 수를 보여 주는 목록을 표시 합니다.

[![Image10](the-entity-framework-and-aspnet-getting-started-part-3/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image27.png)

## <a name="using-the-queryextender-control-for-filtering-and-ordering"></a>필터링 및 정렬에 QueryExtender 컨트롤 사용

`QueryExtender` 컨트롤은 태그에서 필터링 및 정렬을 지정 하는 방법을 제공 합니다. 구문은 사용 중인 DBMS (데이터베이스 관리 시스템)와는 독립적입니다. 또한 일반적으로 Entity Framework와는 독립적 이며 탐색 속성에 사용 하는 구문이 Entity Framework에 고유 합니다.

자습서의이 부분에서는 `QueryExtender` 컨트롤을 사용 하 여 데이터를 필터링 하 고 정렬 하며, order by 필드 중 하나가 탐색 속성이 됩니다.

(태그 대신 코드를 사용 하 여 `EntityDataSource` 컨트롤에 의해 자동으로 생성 되는 쿼리를 확장 하려는 경우 `QueryCreated` 이벤트를 처리 하 여 수행할 수 있습니다. `QueryExtender` 컨트롤이 `EntityDataSource` 컨트롤 쿼리도 확장 하는 방법입니다.)

*Default.aspx* 페이지를 열고 이전에 추가한 태그 아래에서 다음 태그를 삽입 하 여 머리글, 검색 문자열을 입력할 수 있는 텍스트 상자, 검색 단추 및 `Courses` 엔터티 집합에 바인딩된 `EntityDataSource` 컨트롤을 삽입 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample6.aspx)]

`EntityDataSource` 컨트롤의 `Include` 속성이 `Department`으로 설정 되어 있는지 확인 합니다. 데이터베이스에서 `Course` 테이블에는 부서 이름이 포함 되지 않습니다. `DepartmentID` 외래 키 열이 포함 되어 있습니다. 데이터베이스를 직접 쿼리 하는 경우 과정 데이터와 함께 부서 이름을 가져오려면 `Course` 및 `Department` 테이블에 조인 해야 합니다. `Include` 속성을 `Department`로 설정 하면 Entity Framework에서 `Course` 엔터티를 가져올 때 관련 `Department` 엔터티를 가져오는 작업을 수행 하도록 지정 합니다. 그런 다음 `Department` 엔터티는 `Course` 엔터티의 `Department` 탐색 속성에 저장 됩니다. 기본적으로 데이터 모델 디자이너에 의해 생성 된 `SchoolEntities` 클래스는 필요한 경우 관련 데이터를 검색 하 고, 데이터 소스 컨트롤을 해당 클래스에 바인딩한 후에는 `Include` 속성을 설정 하지 않아도 됩니다. 그러나이 메서드를 설정 하면 페이지의 성능이 향상 됩니다. 그렇지 않으면 Entity Framework는 데이터베이스에 대 한 별도의 호출을 수행 하 여 `Course` 엔터티 및 관련 된 `Department` 엔터티에 대 한 데이터를 검색 합니다.

방금 만든 `EntityDataSource` 컨트롤 뒤에 다음 태그를 삽입 하 여 해당 `EntityDataSource` 컨트롤에 바인딩되는 `QueryExtender` 컨트롤을 만듭니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample7.aspx)]

`SearchExpression` 요소는 제목이 텍스트 상자에 입력 한 값과 일치 하는 과정을 선택 하도록 지정 합니다. `SearchType` 속성이 `StartsWith`를 지정 하기 때문에 텍스트 상자에 입력 된 문자 수만 비교 됩니다.

`OrderByExpression` 요소는 결과 집합을 부서 이름 내의 과정 제목별로 정렬 하도록 지정 합니다. 부서 이름 지정 방법: `Department.Name`. `Course` 엔터티와 `Department` 엔터티 간의 연결은 일 대 일 이므로 `Department` 탐색 속성은 `Department` 엔터티를 포함 합니다. 이 관계가 일 대 다 관계인 경우 속성은 컬렉션을 포함 합니다. 부서 이름을 가져오려면 `Department` 엔터티의 `Name` 속성을 지정 해야 합니다.

마지막으로, `GridView` 컨트롤을 추가 하 여 과정 목록을 표시 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample8.aspx)]

첫 번째 열은 부서 이름을 표시 하는 템플릿 필드입니다. 데이터 바인딩 식은 `QueryExtender` 컨트롤에서 살펴본 것 처럼 `Department.Name`를 지정 합니다.

페이지를 실행 합니다. 초기 표시에서는 부서별로 모든 과정의 목록을 표시 한 다음 코스 제목별로 표시 됩니다.

[![Image11](the-entity-framework-and-aspnet-getting-started-part-3/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image29.png)

"M"을 입력 하 고 **검색** 을 클릭 하 여 제목이 "m"으로 시작 하는 모든 과정을 확인 합니다 (검색은 대/소문자를 구분 하지 않음).

[![Image12](the-entity-framework-and-aspnet-getting-started-part-3/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image31.png)

## <a name="using-the-like-operator-to-filter-data"></a>"Like" 연산자를 사용 하 여 데이터 필터링

`Like` 컨트롤의 `EntityDataSource` 속성에서 `Where` 연산자를 사용 하 여 `QueryExtender` 컨트롤의 `StartsWith`, `Contains`및 `EndsWith` 검색 형식과 비슷한 효과를 달성할 수 있습니다. 자습서의이 부분에서는 `Like` 연산자를 사용 하 여 이름별로 학생을 검색 하는 방법을 알아봅니다.

**소스** 뷰에서 *학습자* 를 엽니다. `GridView` 컨트롤 뒤에 다음 태그를 추가 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample9.aspx)]

이 태그는 `Where` 속성 값을 제외 하 고 앞에서 살펴본 것과 비슷합니다. `Where` 식의 두 번째 부분에서는 텍스트 상자에 입력 된 항목에 대해 성과 이름을 모두 검색 하는 부분 문자열 검색 (`LIKE %FirstMidName% or LIKE %LastName%`)을 정의 합니다.

페이지를 실행 합니다. `StudentName` 매개 변수의 기본값은 "%" 이므로 처음에는 모든 학생이 표시 됩니다.

[![Image13](the-entity-framework-and-aspnet-getting-started-part-3/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image33.png)

텍스트 상자에 문자 "g"를 입력 하 고 **검색**을 클릭 합니다. 첫 번째 또는 마지막 이름에 "g"가 있는 학생의 목록이 표시 됩니다.

[![Image14](the-entity-framework-and-aspnet-getting-started-part-3/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image35.png)

이제 개별 테이블에서 데이터를 표시, 업데이트, 필터링, 정렬 및 그룹화 했습니다. 다음 자습서에서는 관련 데이터를 사용 하 여 작업을 시작 합니다 (마스터-세부 시나리오).

> [!div class="step-by-step"]
> [이전](the-entity-framework-and-aspnet-getting-started-part-2.md)
> [다음](the-entity-framework-and-aspnet-getting-started-part-4.md)
