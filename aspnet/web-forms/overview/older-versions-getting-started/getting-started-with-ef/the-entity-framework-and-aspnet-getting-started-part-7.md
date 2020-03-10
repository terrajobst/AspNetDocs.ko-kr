---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-7
title: Entity Framework 4.0 Database First 및 ASP.NET 4 Web Forms 시작-7 부 | Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 응용 프로그램 샘플은 ...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: f8afb245-b705-419c-8790-0b295e90d5e2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-7
msc.type: authoredcontent
ms.openlocfilehash: 18d4b44c5e23fd6942c3adf48a33a5602e6df6d0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78488525"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-7"></a>Entity Framework 4.0 Database First 및 ASP.NET 4 Web Forms 시작-7 부

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

> Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 4.0 및 Visual Studio 2010를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](the-entity-framework-and-aspnet-getting-started-part-1.md) 를 참조 하십시오.

## <a name="using-stored-procedures"></a>저장 프로시저 사용

이전 자습서에서는 계층당 하나의 테이블 상속 패턴을 구현 했습니다. 이 자습서에서는 저장 프로시저를 사용 하 여 데이터베이스 액세스를 보다 효과적으로 제어 하는 방법을 보여 줍니다.

Entity Framework를 사용 하 여 데이터베이스 액세스를 위해 저장 프로시저를 사용 하도록 지정할 수 있습니다. 모든 엔터티 형식에 대해 해당 형식의 엔터티를 생성, 업데이트 또는 삭제 하는 데 사용할 저장 프로시저를 지정할 수 있습니다. 그런 다음 데이터 모델에서 엔터티 집합을 검색 하는 등의 작업을 수행 하는 데 사용할 수 있는 저장 프로시저에 대 한 참조를 추가할 수 있습니다.

저장 프로시저를 사용 하는 것은 데이터베이스 액세스에 대 한 일반적인 요구 사항입니다. 경우에 따라 데이터베이스 관리자는 보안상의 이유로 모든 데이터베이스 액세스에서 저장 프로시저를 통과 하도록 요구할 수 있습니다. 다른 경우에는 데이터베이스를 업데이트할 때 Entity Framework에서 사용 하는 프로세스 중 일부에 비즈니스 논리를 작성 하는 것이 좋습니다. 예를 들어 엔터티가 삭제 될 때마다 보관 데이터베이스에 복사 하는 것이 좋습니다. 또는 행이 업데이트 될 때마다 변경 내용을 기록한 기록 테이블에 행을 기록 하는 것이 좋습니다. Entity Framework에서 엔터티를 삭제 하거나 엔터티를 업데이트할 때마다 호출 되는 저장 프로시저에서 이러한 종류의 작업을 수행할 수 있습니다.

이전 자습서에서와 같이 새 페이지를 만들지 않습니다. 대신, 이미 만든 페이지 중 일부에 대 한 Entity Framework 데이터베이스에 액세스 하는 방식을 변경 합니다.

이 자습서에서는 `Student` 및 `Instructor` 엔터티 삽입을 위해 데이터베이스에 저장 프로시저를 만듭니다. 데이터 모델에 추가 하 고 데이터베이스에 `Student` 및 `Instructor` 엔터티를 추가 하는 데 Entity Framework를 사용 하도록 지정 합니다. 또한 `Course` 엔터티를 검색 하는 데 사용할 수 있는 저장 프로시저를 만듭니다.

## <a name="creating-stored-procedures-in-the-database"></a>데이터베이스에 저장 프로시저 만들기

이 자습서를 사용 하 여 다운로드할 수 있는 프로젝트의 *School .mdf* 파일을 사용 하는 경우 저장 프로시저가 이미 존재 하기 때문에이 섹션을 건너뛸 수 있습니다.

**서버 탐색기**에서 *School*을 확장 하 고 **저장 프로시저**를 마우스 오른쪽 단추로 클릭 한 다음 **새 저장 프로시저 추가**를 선택 합니다.

[![image15](the-entity-framework-and-aspnet-getting-started-part-7/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image1.png)

다음 SQL 문을 복사 하 여 저장 프로시저 창에 붙여넣어 기초 저장 프로시저를 대체 합니다.

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample1.sql)]

[![image14](the-entity-framework-and-aspnet-getting-started-part-7/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image3.png)

`Student` 엔터티에는 `PersonID`, `LastName`, `FirstName`및 `EnrollmentDate`의 네 가지 속성이 있습니다. 데이터베이스는 ID 값을 자동으로 생성 하 고 저장 프로시저는 세 번째 매개 변수에 대 한 매개 변수를 허용 합니다. 저장 프로시저는 새 행의 레코드 키 값을 반환 하므로 Entity Framework는 메모리에 유지 되는 엔터티 버전의 레코드를 추적할 수 있습니다.

저장 프로시저 창을 저장 하 고 닫습니다.

다음 SQL 문을 사용 하 여 동일한 방식으로 `InsertInstructor` 저장 프로시저를 만듭니다.

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample2.sql)]

`Student` 및 `Instructor` 엔터티에 대 한 `Update` 저장 프로시저를 만듭니다. 데이터베이스는 `Instructor` 및 `Student` 엔터티 모두에 대해 작동 하는 `DeletePerson` 저장 프로시저를 이미 포함 하 고 있습니다.

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample3.sql)]

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample4.sql)]

이 자습서에서는 각 엔터티 형식에 대해 삽입, 업데이트 및 삭제 라는 세 함수를 모두 매핑합니다. Entity Framework 버전 4에서는 다른 함수를 매핑하지 않고 저장 프로시저에 이러한 함수 중 하나 또는 두 개만 매핑할 수 있습니다. 단, 업데이트 함수를 매핑하고 delete Entity Framework 함수가 아닌 경우에는 예외를 throw 합니다. 엔터티를 삭제 하려고 합니다. Entity Framework 버전 3.5에서는 저장 프로시저를 매핑하는 데 그다지 유연성이 없었습니다. 함수 하나를 매핑한 경우 세 가지를 모두 매핑해야 합니다.

업데이트 데이터가 아닌를 읽는 저장 프로시저를 만들려면 다음 SQL 문을 사용 하 여 모든 `Course` 엔터티를 선택 하는 저장 프로시저를 만듭니다.

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample5.sql)]

## <a name="adding-the-stored-procedures-to-the-data-model"></a>데이터 모델에 저장 프로시저 추가

이제 저장 프로시저가 데이터베이스에 정의 되어 있지만 Entity Framework에서 사용할 수 있도록 데이터 모델에 추가 되어야 합니다. *SchoolModel*을 열고 디자인 화면을 마우스 오른쪽 단추로 클릭 한 다음 **데이터베이스에서 모델 업데이트**를 선택 합니다. **데이터베이스 개체 선택** 대화 상자의 **추가** 탭에서 **저장 프로시저**를 확장 하 고 새로 만든 저장 프로시저와 `DeletePerson` 저장 프로시저를 선택한 다음 **마침**을 클릭 합니다.

[![image20](the-entity-framework-and-aspnet-getting-started-part-7/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image5.png)

## <a name="mapping-the-stored-procedures"></a>저장 프로시저 매핑

데이터 모델 디자이너에서 `Student` 엔터티를 마우스 오른쪽 단추로 클릭 하 고 **저장 프로시저 매핑**을 선택 합니다.

[![image21](the-entity-framework-and-aspnet-getting-started-part-7/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image7.png)

**매핑 정보** 창이 표시 됩니다. 여기에서 Entity Framework이 형식의 엔터티를 삽입, 업데이트 및 삭제 하는 데 사용 해야 하는 저장 프로시저를 지정할 수 있습니다.

[![image22](the-entity-framework-and-aspnet-getting-started-part-7/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image9.png)

**Insert** 함수를 **insertstudent**로 설정 합니다. 창에는 저장 프로시저 매개 변수 목록이 표시 되며, 각 매개 변수는 엔터티 속성에 매핑되어야 합니다. 이러한 두 가지는 이름이 동일 하기 때문에 자동으로 매핑됩니다. `FirstName`라는 엔터티 속성이 없으므로 사용 가능한 엔터티 속성을 표시 하는 드롭다운 목록에서 `FirstMidName`을 수동으로 선택 해야 합니다. 이는 `FirstName` 속성의 이름을 첫 번째 자습서에서 `FirstMidName`로 변경 했기 때문입니다.

[![image23](the-entity-framework-and-aspnet-getting-started-part-7/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image11.png)

동일한 **매핑 정보** 창에서 `Update` 함수를 `UpdateStudent` 저장 프로시저에 매핑합니다 (`Insert` 저장 프로시저의 경우와 같이 `FirstName`에 대 한 매개 변수 값으로 `FirstMidName`을 지정 하 고 `Delete` 저장 프로시저에 `DeletePerson` 함수를 지정 해야 합니다.

[![image01](the-entity-framework-and-aspnet-getting-started-part-7/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image13.png)

동일한 절차에 따라 강사의 삽입, 업데이트 및 삭제 저장 프로시저를 `Instructor` 엔터티에 매핑합니다.

[![image02](the-entity-framework-and-aspnet-getting-started-part-7/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image15.png)

데이터를 업데이트 하는 대신 읽을 수 있는 저장 프로시저의 경우 **모델 브라우저** 창을 사용 하 여 저장 프로시저를 반환 하는 엔터티 형식에 매핑합니다. 데이터 모델 디자이너에서 디자인 화면을 마우스 오른쪽 단추로 클릭 하 고 **모델 브라우저**를 선택 합니다. **SchoolModel** 노드를 연 다음 **저장 프로시저** 노드를 엽니다. 그런 다음 `GetCourses` 저장 프로시저를 마우스 오른쪽 단추로 클릭 하 고 **Function Import 추가**를 선택 합니다.

[![image24](the-entity-framework-and-aspnet-getting-started-part-7/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image17.png)

**함수 가져오기 추가** 대화 상자의 아래에서 Select 엔터티의 **컬렉션을** 반환한 다음 반환된 엔터티 형식으로 `Course`를 선택 합니다. 완료되면 **확인**을 클릭합니다. *.Edmx* 파일을 저장 하 고 닫습니다.

[![image25](the-entity-framework-and-aspnet-getting-started-part-7/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image19.png)

## <a name="using-insert-update-and-delete-stored-procedures"></a>Insert, Update 및 Delete 저장 프로시저 사용

데이터를 삽입, 업데이트 및 삭제 하는 저장 프로시저는 데이터 모델에 추가 하 고 적절 한 엔터티에 매핑한 후 Entity Framework에서 자동으로 사용 됩니다. 이제 *StudentsAdd* 페이지를 실행할 수 있으며, 새 학생을 만들 때마다 Entity Framework `InsertStudent` 저장 프로시저를 사용 하 여 `Student` 테이블에 새 행을 추가 합니다.

[![image03](the-entity-framework-and-aspnet-getting-started-part-7/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image21.png)

*학생과 .aspx* 페이지를 실행 하 고 목록에 새 학생을 표시 합니다.

[![image04](the-entity-framework-and-aspnet-getting-started-part-7/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image23.png)

이름을 변경 하 여 업데이트 함수가 작동 하는지 확인 한 다음 학생을 삭제 하 여 delete 함수가 작동 하는지 확인 합니다.

[![image05](the-entity-framework-and-aspnet-getting-started-part-7/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image25.png)

## <a name="using-select-stored-procedures"></a>Select 저장 프로시저 사용

Entity Framework는 `GetCourses`와 같은 저장 프로시저를 자동으로 실행 하지 않으며 `EntityDataSource` 컨트롤과 함께 사용할 수 없습니다. 이를 사용 하려면 코드에서 호출 합니다.

*InstructorsCourses.aspx.cs* 파일을 엽니다. `PopulateDropDownLists` 메서드는 LINQ to entities 쿼리를 사용 하 여 모든 강좌 엔터티를 검색 하 여 목록을 반복 하 고 강사가 할당 된 항목과 할당 되지 않은 항목을 확인할 수 있습니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample6.cs)]

다음 코드로 바꿉니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample7.cs)]

이제 페이지에서 `GetCourses` 저장 프로시저를 사용 하 여 모든 과정 목록을 검색 합니다. 페이지를 실행 하 여 이전과 동일한 방식으로 작동 하는지 확인 합니다.

저장 프로시저에 의해 검색 되는 엔터티의 탐색 속성은 `ObjectContext` 기본 설정에 따라 해당 엔터티와 관련 된 데이터로 자동으로 채워지지 않을 수 있습니다. 자세한 내용은 MSDN Library에서 [관련 개체 로드](https://msdn.microsoft.com/library/bb896272.aspx) 를 참조 하세요.

다음 자습서에서는 Dynamic Data 기능을 사용 하 여 데이터 형식 및 유효성 검사 규칙을 쉽게 프로그래밍 하 고 테스트 하는 방법을 배웁니다. 데이터 형식 문자열 및 필드의 필요 여부와 같은 각 웹 페이지 규칙을 지정 하는 대신 데이터 모델 메타 데이터에서 이러한 규칙을 지정할 수 있습니다. 이러한 규칙은 모든 페이지에 자동으로 적용 됩니다.

> [!div class="step-by-step"]
> [이전](the-entity-framework-and-aspnet-getting-started-part-6.md)
> [다음](the-entity-framework-and-aspnet-getting-started-part-8.md)
