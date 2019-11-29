---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: ASP.NET MVC 응용 프로그램에서 Entity Framework로 상속 구현 (8/10) | Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다.
ms.author: riande
ms.date: 07/30/2013
ms.assetid: a5c3feff-5335-4cdd-a97d-f7a8785c2494
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9507cba71b976825257cc9948d54f2651355959d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595315"
---
# <a name="implementing-inheritance-with-the-entity-framework-in-an-aspnet-mvc-application-8-of-10"></a>ASP.NET MVC 응용 프로그램에서 Entity Framework로 상속 구현 (8/10)

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 5 Code First 및 Visual Studio 2012을 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요. [이 챕터의](building-the-ef5-mvc4-chapter-downloads.md) 시작 또는 시작 프로젝트 다운로드에서 자습서 시리즈를 시작 하 고 여기에서 시작할 수 있습니다.
> 
> > [!NOTE] 
> > 
> > 해결할 수 없는 문제가 발생 하는 경우 [완료 된 챕터를 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 하 여 문제를 재현해 보세요. 일반적으로 코드를 완성 된 코드와 비교 하 여 문제에 대 한 솔루션을 찾을 수 있습니다. 몇 가지 일반적인 오류 및 해결 방법에 대 한 자세한 내용은 [오류 및 해결](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors) 방법을 참조 하세요.

이전 자습서에서는 동시성 예외를 처리 했습니다. 이 자습서에서는 데이터 모델에서 상속을 구현하는 방법을 보여 줍니다.

개체 지향 프로그래밍에서는 상속을 사용 하 여 중복 코드를 제거할 수 있습니다. 이 자습서에서는 강사와 학생 모두에게 공통적인 속성(예: `LastName`)이 포함된 `Person` 기본 클래스에서 클래스가 파생되도록 `Instructor` 및 `Student` 클래스를 변경합니다. 웹 페이지를 추가하거나 변경하지는 않지만 일부 코드를 변경하고 이러한 변경 내용이 데이터베이스에 자동으로 반영됩니다.

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a>계층당 하나의 테이블 및 형식당 하나의 테이블 상속

개체 지향 프로그래밍에서는 상속을 사용 하 여 관련 클래스 작업을 보다 쉽게 수행할 수 있습니다. 예를 들어 `School` 데이터 모델의 `Instructor` 및 `Student` 클래스는 중복 된 코드를 생성 하는 여러 속성을 공유 합니다.

![Student_and_Instructor_classes](https://asp.net/media/2578113/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_e7a32f99-8bc4-48ce-aeaf-216a18071a8b.png)

`Instructor` 및 `Student` 엔터티에서 공유하는 속성에 대해 중복 코드를 제거하려고 한다고 가정해 보겠습니다. 다음 그림과 같이 해당 공유 속성만 포함 하는 `Person` 기본 클래스를 만든 다음 `Instructor` 및 `Student` 엔터티가 해당 기본 클래스에서 상속 하도록 할 수 있습니다.

![Student_and_Instructor_classes_deriving_from_Person_class](https://asp.net/media/2578119/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_deriving_from_Person_class_671d708c-cbb8-454a-a8f8-c2d99439acd9.png)

데이터베이스에 이 상속 구조를 여러 가지 방법으로 나타낼 수 있습니다. 학생 및 강사 모두에 대 한 정보를 단일 테이블에 포함 하는 `Person` 테이블이 있을 수 있습니다. 일부 열은 강사 (`HireDate`) 에게만 적용 되 고 일부는 학생 (`EnrollmentDate`)에만 적용 되 고 일부는 둘 다 (`LastName`, `FirstName`)에만 적용 될 수 있습니다. 일반적으로 각 행이 나타내는 형식을 나타내는 *판별자* 열이 있습니다. 예를 들어, 판별자 열은 강사에 대해 "Instructor"를, 학생에 대해 "Student"를 포함할 수 있습니다.

![테이블당 테이블 수 hierarchy_example](https://asp.net/media/2578125/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-hierarchy_example_244067cd-b451-4e9b-9595-793b9afca505.png)

단일 데이터베이스 테이블에서 엔터티 상속 구조를 생성 하는이 패턴은 TPH ( *계층당 하나의 테이블* ) 상속 이라고 합니다.

다른 방법은 데이터베이스를 상속 구조와 유사하게 만드는 것입니다. 예를 들어 `Person` 테이블에 이름 필드만 포함 하 고 날짜 필드를 사용 하 여 별도의 `Instructor` 및 `Student` 테이블을 가질 수 있습니다.

![테이블당 테이블 수 type_inheritance](https://asp.net/media/2578131/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-type_inheritance.png)

각 엔터티 클래스에 대 한 데이터베이스 테이블을 만드는이 패턴을 TPT (형식당 *하나의 테이블* ) 상속 이라고 합니다.

TPH 상속 패턴 Entity Framework은 일반적으로 TPT 상속 패턴 보다 더 나은 성능을 제공 합니다. TPT 패턴은 복잡 한 조인 쿼리를 발생 시킬 수 있기 때문입니다. 이 자습서에서는 TPH 상속을 구현하는 방법을 보여 줍니다. 이렇게 하려면 다음 단계를 수행 합니다.

- `Person` 클래스를 만들고 `Person`에서 파생 되도록 `Instructor` 및 `Student` 클래스를 변경 합니다.
- 데이터베이스 컨텍스트 클래스에 모델-데이터베이스 매핑 코드를 추가 합니다.
- 프로젝트 전체에서 `InstructorID` 및 `StudentID` 참조를 `PersonID`로 변경 합니다.

## <a name="creating-the-person-class"></a>Person 클래스 만들기

 참고: 이러한 클래스를 사용 하는 컨트롤러를 업데이트할 때까지 아래 클래스를 만든 후에는 프로젝트를 컴파일할 수 없습니다. 

*모델* 폴더에서 *Person.cs* 을 만들고 템플릿 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

*Instructor.cs*에서 `Person` 클래스의 `Instructor` 클래스를 파생 하 고 키 및 이름 필드를 제거 합니다. 해당 코드는 다음 예제와 같이 나타납니다.

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

*Student.cs*에 대 한 비슷한 변경을 수행 합니다. `Student` 클래스는 다음 예제와 같습니다.

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="adding-the-person-entity-type-to-the-model"></a>모델에 Person 엔터티 형식 추가

*SchoolContext.cs*에서 `Person` 엔터티 형식에 대 한 `DbSet` 속성을 추가 합니다.

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

계층당 하나의 테이블 상속을 구성하기 위해 Entity Framework에 필요한 모든 작업입니다. 여기서 볼 수 있듯이 데이터베이스를 다시 만들 때 `Student` 및 `Instructor` 테이블 대신 `Person` 테이블이 포함 됩니다.

## <a name="changing-instructorid-and-studentid-to-personid"></a>InstructorID 및 StudentID를 PersonID로 변경

*SchoolContext.cs*의 강사-강좌 매핑 문에서 `MapRightKey("InstructorID")`을 `MapRightKey("PersonID")`변경 합니다.

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=4)]

이러한 변경은 필요 하지 않습니다. 다대다 조인 테이블의 InstructorID 열 이름만 변경 합니다. 이름을 InstructorID로 남겨 둔 경우에도 응용 프로그램이 제대로 작동 합니다. 다음은 완료 된 *SchoolContext.cs*입니다.

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=15,24)]

다음으로 `InstructorID`를 `PersonID`으로 변경 하 고 *마이그레이션* 폴더의 타임 스탬프 마이그레이션 파일을 ***제외*** 하 고 프로젝트 전체에서 `PersonID` `StudentID` 해야 합니다. 이렇게 하려면 변경 해야 하는 파일만 찾고 연 다음 열린 파일에 대 한 전체 변경을 수행 합니다. 변경 해야 하는 *마이그레이션* 폴더의 유일한 파일은 *Migrations\Configuration.cs.* 입니다.

1. > [!IMPORTANT]
   > 먼저 Visual Studio에서 열려 있는 모든 파일을 닫습니다.
2. **편집** 메뉴에서 **찾기 및 바꾸기--모든 파일 찾기** 를 클릭 한 다음 프로젝트에서 `InstructorID`포함 된 모든 파일을 검색 합니다.  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. 각 파일에 대해 한 줄을 두 번 클릭 하 여 *마이그레이션 폴더에* &lt;타임 스탬프&gt; *\_.cs* 마이그레이션 파일을 ***제외 하*** 고 각 파일을 **찾기 결과** 창에서 엽니다.  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)
4. **파일에서 바꾸기** 대화 상자를 열고 열려 **있는** **모든 문서**를 확인 합니다.
5. **파일에서 바꾸기** 대화 상자를 사용 하 여 모든 `InstructorID`을 `PersonID.` 변경  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)
6. 프로젝트에서 `StudentID`를 포함 하는 모든 파일을 찾습니다.
7. 각 파일에 대해 한 줄을 두 번 클릭 하 여 &lt;타임 스탬프&gt;를 제외 하 고 *마이그레이션 폴더에* *\_\*.cs* 마이그레이션 파일을 ***제외 하*** 고 각 파일을 **찾기 결과** 창에서 엽니다.  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
8. **파일에서 바꾸기** 대화 상자를 열고 열려 **있는** **모든 문서**를 확인 합니다.
9. **파일에서 바꾸기** 대화 상자를 사용 하 여 모든 `StudentID`을 `PersonID`변경 합니다.   
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)
10. 프로젝트를 빌드합니다.

이는 기본 키의 이름을 지정 하는 `classnameID` 패턴의 *단점* 을 보여 줍니다. 클래스 이름 앞에 접두사를 지정 하지 않고 기본 키 ID의 이름을 지정한 경우에는 이름을 바꿀 필요가 *없습니다* .

## <a name="create-and-update-a-migrations-file"></a>마이그레이션 파일 만들기 및 업데이트

패키지 관리자 콘솔 (PMC)에서 다음 명령을 입력 합니다.

`Add-Migration Inheritance`

PMC에서 `Update-Database` 명령을 실행 합니다. 마이그레이션에서 처리 방법을 알지 못하는 기존 데이터가 있으므로이 시점에서 명령이 실패 합니다. 다음 오류가 발생 합니다.

*ALTER TABLE 문이 FOREIGN KEY 제약 조건 "FK\_dbo와 충돌 했습니다. 부서\_dbo. Person\_PersonID ". 데이터베이스 "ContosoUniversity", 테이블 "dbo .에서 충돌이 발생 했습니다. Person ", ' PersonID ' 열*

*마이그레이션\&l t; 타임 스탬프&gt;\_Inheritance.cs* 을 열고 `Up` 메서드를 다음 코드로 바꿉니다.

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=25,29-40)]

`update-database` 명령을 다시 실행 합니다.

> [!NOTE]
> 데이터를 마이그레이션하고 스키마를 변경 하는 경우 다른 오류가 발생할 수 있습니다. 해결할 수 없는 마이그레이션 오류가 발생 하면 *web.config 파일에서* 연결 문자열을 변경 하거나 데이터베이스를 삭제 하 여 자습서를 계속 진행할 수 있습니다. 가장 간단한 방법은 web.config 파일에서 데이터베이스 이름을 바꾸는 것 *입니다.* 예를 들어 다음 예제와 같이 데이터베이스 이름을 CU\_test로 변경 합니다.
> 
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.xml?highlight=1-2)]
> 
> 새 데이터베이스를 사용 하면 마이그레이션할 데이터가 없으며 `update-database` 명령이 오류 없이 완료 될 가능성이 훨씬 높습니다. 데이터베이스를 삭제 하는 방법에 대 한 지침은 [Visual Studio 2012에서 데이터베이스](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)를 삭제 하는 방법을 참조 하세요. 자습서를 계속 진행 하기 위해이 방법을 사용 하는 경우, 배포 된 사이트는 마이그레이션을 자동으로 실행 하는 경우 동일한 오류가 발생 하므로이 자습서의 끝에 있는 배포 단계를 건너뜁니다. 마이그레이션 오류를 해결 하려면 가장 적합 한 리소스는 Entity Framework 포럼 또는 StackOverflow.com 중 하나입니다.

## <a name="testing"></a>테스트

사이트를 실행 하 고 다양 한 페이지를 시도 합니다. 모든 항목이 이전과 같이 작동합니다.

**서버 탐색기** 에서 **schoolcontext.cs** 및 **Tables**를 확장 하 고 **Student** 및 **강사** 테이블이 **Person** 테이블로 대체 된 것을 확인할 수 있습니다. **Person** 테이블을 확장 하면 **Student** 및 **강사** 테이블에 사용 되는 모든 열이 포함 되어 있는 것을 볼 수 있습니다.

![Server_Explorer_showing_Person_table](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

Person 테이블을 마우스 오른쪽 단추로 클릭한 후 **테이블 데이터 표시**를 클릭하여 판별자 열을 표시합니다.

![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

다음 다이어그램에서는 새 School 데이터베이스의 구조를 보여 줍니다.

![School_database_diagram](https://asp.net/media/2578143/Windows-Live-Writer_58f5a93579b2_CC7B_School_database_diagram_6350a801-7199-413f-bbac-4a2009ed19d7.png)

## <a name="summary"></a>요약

이제 `Person`, `Student`및 `Instructor` 클래스에 대해 계층당 하나의 테이블 상속이 구현 되었습니다. 이 및 다른 상속 구조에 대 한 자세한 내용은 계승 Teza의 Avi의 블로그에서 [상속 매핑 전략](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx) 을 참조 하세요. 다음 자습서에서는 리포지토리 및 작업 단위 패턴을 구현 하는 몇 가지 방법을 알아봅니다.

[ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md)에서 다른 Entity Framework 리소스에 대 한 링크를 찾을 수 있습니다.

> [!div class="step-by-step"]
> [이전](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [다음](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)
