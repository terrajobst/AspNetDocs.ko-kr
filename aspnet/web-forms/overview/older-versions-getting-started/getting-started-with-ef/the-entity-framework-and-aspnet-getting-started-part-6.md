---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-6
title: Entity Framework 4.0 Database First 및 ASP.NET 4 Web Forms 시작-6 단계 | Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 응용 프로그램 샘플은 ...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: 994a5496-c648-4830-b03c-55bb43f325d2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-6
msc.type: authoredcontent
ms.openlocfilehash: 8bfbe74f90eb03ea9aab7610842ef2578e80d113
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454919"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-6"></a>Entity Framework 4.0 Database First 및 ASP.NET 4 Web Forms 시작-6 단계

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

> Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 4.0 및 Visual Studio 2010를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](the-entity-framework-and-aspnet-getting-started-part-1.md) 를 참조 하십시오.

## <a name="implementing-table-per-hierarchy-inheritance"></a>계층당 하나의 테이블 상속 구현

이전 자습서에서는 관계를 추가 및 삭제 하 고 기존 엔터티에 대 한 관계가 있는 새 엔터티를 추가 하 여 관련 데이터로 작업 했습니다. 이 자습서에서는 데이터 모델에서 상속을 구현하는 방법을 보여 줍니다.

개체 지향 프로그래밍에서는 상속을 사용 하 여 관련 클래스 작업을 보다 쉽게 수행할 수 있습니다. 예를 들어 `Person` 기본 클래스에서 파생 되는 `Instructor` 및 `Student` 클래스를 만들 수 있습니다. Entity Framework 엔터티 간에 동일한 종류의 상속 구조를 만들 수 있습니다.

자습서의이 부분에서는 새 웹 페이지를 만들지 않습니다. 대신, 파생 엔터티를 데이터 모델에 추가 하 고 기존 페이지를 수정 하 여 새 엔터티를 사용 합니다.

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a>계층당 하나의 테이블 및 형식당 하나의 테이블 상속

데이터베이스는 관련 개체에 대 한 정보를 하나의 테이블 또는 여러 테이블에 저장할 수 있습니다. 예를 들어 `School` 데이터베이스의 `Person` 테이블에는 단일 테이블의 학생과 강사 모두에 대 한 정보가 포함 되어 있습니다. 일부 열은 강사 (`HireDate`)에만 적용 되 고 일부는 학생 (`EnrollmentDate`)에만 적용 되 고 일부는 (`LastName`, `FirstName`)에만 적용 됩니다.

[![image11](the-entity-framework-and-aspnet-getting-started-part-6/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image1.png)

Entity Framework를 구성 하 여 `Person` 엔터티에서 상속 하는 `Instructor` 및 `Student` 엔터티를 만들 수 있습니다. 단일 데이터베이스 테이블에서 엔터티 상속 구조를 생성 하는이 패턴은 TPH ( *계층당 하나의 테이블* ) 상속 이라고 합니다.

과정에서 `School` 데이터베이스는 다른 패턴을 사용 합니다. 온라인 과정 및 온사이트 과정은 각각 `Course` 테이블을 가리키는 외래 키를 포함 하는 별도의 테이블에 저장 됩니다. 두 과정 유형에 공통적인 정보는 `Course` 테이블에만 저장 됩니다.

[![image12](the-entity-framework-and-aspnet-getting-started-part-6/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image3.png)

`OnlineCourse` 및 `OnsiteCourse` 엔터티가 `Course` 엔터티에서 상속 하도록 Entity Framework 데이터 모델을 구성할 수 있습니다. 각 형식에 대 한 별도의 테이블에서 엔터티 상속 구조를 생성 하는이 패턴은 모든 형식에 공통 된 데이터를 저장 하는 테이블을 다시 참조 하는 각 테이블을 TPT (형식당 *하나의 테이블* ) 상속 이라고 합니다.

TPH 상속 패턴 Entity Framework은 일반적으로 TPT 상속 패턴 보다 더 나은 성능을 제공 합니다. TPT 패턴은 복잡 한 조인 쿼리를 발생 시킬 수 있기 때문입니다. 이 연습에서는 TPH 상속을 구현 하는 방법을 보여 줍니다. 이렇게 하려면 다음 단계를 수행 합니다.

- `Person`에서 파생 되는 엔터티 형식 `Instructor` 및 `Student` 만듭니다.
- 파생 엔터티와 관련 된 속성을 `Person` 엔터티에서 파생 엔터티로 이동 합니다.
- 파생 형식의 속성에 제약 조건을 설정 합니다.
- `Person` 엔터티를 추상 엔터티로 만듭니다.
- `Person` 행이 파생 형식을 나타내는지 여부를 확인 하는 방법을 지정 하는 조건을 사용 하 여 각 파생 엔터티를 `Person` 테이블에 매핑합니다.

## <a name="adding-instructor-and-student-entities"></a>강사 및 학생 엔터티 추가

<em>SchoolModel</em> 파일을 열고 디자이너에서 빈 영역을 마우스 오른쪽 단추로 클릭 한 다음 <strong>추가</strong>를 선택 하 고 <strong>엔터티</strong>를 선택<em>합니다.</em>

[![image01](the-entity-framework-and-aspnet-getting-started-part-6/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image5.png)

**엔터티 추가** 대화 상자에서 엔터티 이름을 `Instructor`로 설정 하 고 해당 **기본 형식** 옵션을 `Person`로 설정 합니다.

[![image02](the-entity-framework-and-aspnet-getting-started-part-6/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image7.png)

**확인**을 클릭합니다. 디자이너는 `Person` 엔터티에서 파생 되는 `Instructor` 엔터티를 만듭니다. 새 엔터티에 아직 속성이 없습니다.

[![image03](the-entity-framework-and-aspnet-getting-started-part-6/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image9.png)

프로시저를 반복 하 여 `Person`에서도 파생 되는 `Student` 엔터티를 만듭니다.

강사만 고용 날짜를 가지 므로 `Person` 엔터티에서 해당 속성을 `Instructor` 엔터티로 이동 해야 합니다. `Person` 엔터티에서 `HireDate` 속성을 마우스 오른쪽 단추로 클릭 하 고 **잘라내기**를 클릭 합니다. 그런 다음 `Instructor` 엔터티에서 **속성** 을 마우스 오른쪽 단추로 클릭 하 고 **붙여넣기**를 클릭 합니다.

[![image04](the-entity-framework-and-aspnet-getting-started-part-6/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image11.png)

`Instructor` 엔터티의 채용 날짜는 null 일 수 없습니다. `HireDate` 속성을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 클릭 한 다음 **속성** 창에서 `Nullable` `False`변경 합니다.

[![image05](the-entity-framework-and-aspnet-getting-started-part-6/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image13.png)

이 절차를 반복 하 여 `Person` 엔터티에서 `EnrollmentDate` 속성을 `Student` 엔터티로 이동 합니다. `EnrollmentDate` 속성에 대해 `Nullable`를 `False`으로 설정 해야 합니다.

이제 `Person` 엔터티에 `Instructor` 및 `Student` 엔터티에 공통 된 속성만 있으므로 (이동 하지 않는 탐색 속성 외에) 엔터티는 상속 구조에서 기본 엔터티로만 사용할 수 있습니다. 따라서 독립적인 엔터티로 처리 되지 않도록 해야 합니다. `Person` 엔터티를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택한 다음 **속성** 창에서 **Abstract** 속성의 값을 **True**로 변경 합니다.

[![image06](the-entity-framework-and-aspnet-getting-started-part-6/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image15.png)

## <a name="mapping-instructor-and-student-entities-to-the-person-table"></a>Person 테이블에 강사 및 학생 엔터티 매핑

이제 데이터베이스에서 `Instructor`와 `Student` 엔터티를 구분 하는 방법을 Entity Framework에 게 알려 주어 야 합니다.

`Instructor` 엔터티를 마우스 오른쪽 단추로 클릭 하 고 **테이블 매핑**을 선택 합니다. **매핑 정보** 창에서 **테이블 또는 뷰 추가** 를 클릭 하 고 **Person**을 선택 합니다.

[![image07](the-entity-framework-and-aspnet-getting-started-part-6/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image17.png)

**조건 추가**를 클릭 한 다음 **HireDate**를 선택 합니다.

[![image09](the-entity-framework-and-aspnet-getting-started-part-6/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image19.png)

**연산자** 를 **Is** 로 변경 하 고 **값/속성** 을 **not Null**로 변경 합니다.

[![image10](the-entity-framework-and-aspnet-getting-started-part-6/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image21.png)

`EnrollmentDate` 열이 null이 아닌 경우이 엔터티가 `Person` 테이블에 매핑되도록 지정 하 `Students` 엔터티에 대해이 절차를 반복 합니다. 그런 다음 데이터 모델을 저장 하 고 닫습니다.

새 엔터티를 클래스로 만들고 디자이너에서 사용할 수 있게 하려면 프로젝트를 빌드합니다.

## <a name="using-the-instructor-and-student-entities"></a>강사 및 학생 엔터티 사용

학생 및 강사 데이터를 사용 하는 웹 페이지를 만들 때이를 `Person` 엔터티 집합에 데이터 바인딩된 다음 `HireDate` 또는 `EnrollmentDate` 속성을 필터링 하 여 반환 된 데이터를 학생 또는 강사에 게 제한 합니다. 그러나 이제 `Person` 엔터티 집합에 각 데이터 소스 컨트롤을 바인딩할 때 `Student` 또는 `Instructor` 엔터티 유형만 선택 하도록 지정할 수 있습니다. Entity Framework는 `Person` 엔터티 집합에서 학생 및 강사를 구분 하는 방법을 알고 있으므로 수동으로 입력 한 `Where` 속성 설정을 제거할 수 있습니다.

Visual Studio 디자이너에서 다음 예제와 같이 `Configure Data Source` 마법사의 **EntityTypeFilter** 드롭다운 상자에서 `EntityDataSource` 컨트롤이 선택 해야 하는 엔터티 형식을 지정할 수 있습니다.

[![image13](the-entity-framework-and-aspnet-getting-started-part-6/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image23.png)

그리고 **속성** 창에서 다음 예제와 같이 더 이상 필요 하지 않은 `Where` 절 값을 제거할 수 있습니다.

[![image14](the-entity-framework-and-aspnet-getting-started-part-6/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image25.png)

그러나 `EntityDataSource` 컨트롤에 대 한 태그를 변경 하 여 `ContextTypeName` 특성을 사용 하기 때문에 이미 만든 `EntityDataSource` 컨트롤에 대해 **데이터 소스 구성** 마법사를 실행할 수 없습니다. 따라서 태그를 변경 하 여 필요한 변경을 수행 합니다.

*학생과 .aspx* 페이지를 엽니다. `StudentsEntityDataSource` 컨트롤에서 `Where` 특성을 제거 하 고 `EntityTypeFilter="Student"` 특성을 추가 합니다. 이제 태그는 다음 예제와 유사 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample1.aspx)]

`EntityTypeFilter` 특성을 설정 하면 `EntityDataSource` 컨트롤이 지정 된 엔터티 형식만 선택 하 게 됩니다. `Student` 및 `Instructor` 엔터티 형식을 모두 검색 하려는 경우에는이 특성을 설정 하지 않습니다. (읽기 전용 데이터 액세스에 대해 컨트롤을 사용 하는 경우에만 `EntityDataSource` 컨트롤 하나를 사용 하 여 여러 엔터티 형식을 검색 하는 옵션을 사용할 수 있습니다. `EntityDataSource` 컨트롤을 사용 하 여 엔터티를 삽입, 업데이트 또는 삭제 하 고, 바인딩된 엔터티 집합에 여러 형식이 포함 될 수 있는 경우 하나의 엔터티 형식만 사용할 수 있으며이 특성을 설정 해야 합니다.

`SearchEntityDataSource` 컨트롤에 대해이 절차를 반복 합니다. 단, 속성을 완전히 제거 하는 대신 `Student` 엔터티를 선택 하는 `Where` 특성 부분만 제거 합니다. 이제 컨트롤의 여는 태그는 다음 예제와 유사 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample2.aspx)]

페이지를 실행 하 여 이전과 동일한 방식으로 작동 하는지 확인 합니다.

[![image15](the-entity-framework-and-aspnet-getting-started-part-6/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image27.png)

이전 자습서에서 만든 다음 페이지를 업데이트 하 여 엔터티를 `Person` 하는 대신 새 `Student` 및 `Instructor` 엔터티를 사용 하 고이를 실행 하 여 이전 처럼 작동 하는지 확인 합니다.

- *StudentsAdd*에서 `StudentsEntityDataSource` 컨트롤에 `EntityTypeFilter="Student"`를 추가 합니다. 이제 태그는 다음 예제와 유사 합니다. 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample3.aspx)]

    [![image16](the-entity-framework-and-aspnet-getting-started-part-6/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image29.png)
- *About .aspx*에서 `StudentStatisticsEntityDataSource` 컨트롤에 `EntityTypeFilter="Student"`를 추가 하 고 `Where="it.EnrollmentDate is not null"`를 제거 합니다. 이제 태그는 다음 예제와 유사 합니다. 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample4.aspx)]

    [![image17](the-entity-framework-and-aspnet-getting-started-part-6/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image31.png)
- *강사* 와 *InstructorsCourses*에서 `InstructorsEntityDataSource` 컨트롤에 `EntityTypeFilter="Instructor"`를 추가 하 고 `Where="it.HireDate is not null"`를 제거 합니다. 이제 *강사 .aspx* 의 태그는 다음 예제와 유사 합니다. 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample5.aspx)]

    [![image18](the-entity-framework-and-aspnet-getting-started-part-6/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image33.png)

    이제 *InstructorsCourses* 의 태그는 다음 예제와 유사 합니다.

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample6.aspx)]

    [![image19](the-entity-framework-and-aspnet-getting-started-part-6/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image35.png)

이러한 변경으로 인해 Contoso 대학 응용 프로그램의 유지 관리를 여러 가지 방법으로 향상 시켰습니다. UI 계층 ( *.aspx* 태그)에서 선택 및 유효성 검사 논리를 이동 하 여 데이터 액세스 계층의 필수적인 부분으로 만들었습니다. 이렇게 하면 나중에 데이터베이스 스키마 또는 데이터 모델에 대해 수행할 수 있는 변경 내용 으로부터 응용 프로그램 코드를 격리할 수 있습니다. 예를 들어 학생이 교사 지원으로 고용 될 수 있으므로 고용 날짜를 얻을 수 있습니다. 그런 다음 새 속성을 추가 하 여 강사와 학생을 차별화 하 고 데이터 모델을 업데이트할 수 있습니다. 학생의 고용 날짜를 표시 하려는 경우를 제외 하 고 웹 응용 프로그램의 코드는 변경 하지 않아도 됩니다. `Instructor` 및 `Student` 엔터티를 추가 하는 또 다른 장점으로는 실제로 학생 또는 강사 인 개체를 `Person` 하는 것 보다 코드를 보다 쉽게 이해할 수 있습니다.

이제 Entity Framework에서 상속 패턴을 구현 하는 한 가지 방법을 살펴보았습니다. 다음 자습서에서는 저장 프로시저를 사용 하 여 Entity Framework에서 데이터베이스에 액세스 하는 방법을 보다 세밀 하 게 제어 하는 방법을 알아봅니다.

> [!div class="step-by-step"]
> [이전](the-entity-framework-and-aspnet-getting-started-part-5.md)
> [다음](the-entity-framework-and-aspnet-getting-started-part-7.md)
