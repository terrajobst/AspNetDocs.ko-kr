---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: '자습서: ASP.NET MVC 5 앱에서 EF로 상속 구현'
description: 이 자습서에서는 데이터 모델에서 상속을 구현하는 방법을 보여 줍니다.
author: tdykstra
ms.author: riande
ms.date: 01/21/2019
ms.topic: tutorial
ms.assetid: 08834147-77ec-454a-bb7a-d931d2a40dab
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 73a01ed47b0935a1a9734c197377470defb1fe36
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519390"
---
# <a name="tutorial-implement-inheritance-with-ef-in-an-aspnet-mvc-5-app"></a>자습서: ASP.NET MVC 5 앱에서 EF로 상속 구현

이전 자습서에서는 동시성 예외를 처리 했습니다. 이 자습서에서는 데이터 모델에서 상속을 구현하는 방법을 보여 줍니다.

개체 지향 프로그래밍에서는 [상속](http://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming)) 을 사용 하 여 코드를 쉽게 [재사용할](http://en.wikipedia.org/wiki/Code_reuse)수 있습니다. 이 자습서에서는 강사와 학생 모두에게 공통적인 속성(예: `LastName`)이 포함된 `Person` 기본 클래스에서 클래스가 파생되도록 `Instructor` 및 `Student` 클래스를 변경합니다. 웹 페이지를 추가하거나 변경하지는 않지만 일부 코드를 변경하고 이러한 변경 내용이 데이터베이스에 자동으로 반영됩니다.

이 자습서에서는 다음과 같은 작업을 수행합니다.

> [!div class="checklist"]
> * 데이터베이스에 상속 매핑 방법 알아보기
> * Person 클래스 만들기
> * 강사 및 학생 업데이트
> * 모델에 사람 추가
> * 마이그레이션 만들기 및 업데이트
> * 구현 테스트
> * Azure에 배포

## <a name="prerequisites"></a>전제 조건

* [동시성 처리](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="map-inheritance-to-database"></a>데이터베이스에 상속 매핑

`School` 데이터 모델의 `Instructor` 및 `Student` 클래스에는 동일한 여러 속성이 있습니다.

![Student_and_Instructor_classes](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

`Instructor` 및 `Student` 엔터티에서 공유하는 속성에 대해 중복 코드를 제거하려고 한다고 가정해 보겠습니다. 또는 강사 또는 학생의 이름인지 여부를 신경쓰지 않고 이름의 형식을 지정할 수 있는 서비스를 작성하려고 합니다. 다음 그림과 같이 해당 공유 속성만 포함 하는 `Person` 기본 클래스를 만든 다음 `Instructor` 및 `Student` 엔터티가 해당 기본 클래스에서 상속 하도록 할 수 있습니다.

![Student_and_Instructor_classes_deriving_from_Person_class](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

데이터베이스에 이 상속 구조를 여러 가지 방법으로 나타낼 수 있습니다. 학생 및 강사 모두에 대 한 정보를 단일 테이블에 포함 하는 `Person` 테이블이 있을 수 있습니다. 일부 열은 강사 (`HireDate`) 에게만 적용 되 고 일부는 학생 (`EnrollmentDate`)에만 적용 되 고 일부는 둘 다 (`LastName`, `FirstName`)에만 적용 될 수 있습니다. 일반적으로 각 행이 나타내는 형식을 나타내는 *판별자* 열이 있습니다. 예를 들어, 판별자 열은 강사에 대해 "Instructor"를, 학생에 대해 "Student"를 포함할 수 있습니다.

![테이블당 테이블 수 hierarchy_example](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

단일 데이터베이스 테이블에서 엔터티 상속 구조를 생성 하는이 패턴은 TPH ( *계층당 하나의 테이블* ) 상속 이라고 합니다.

다른 방법은 데이터베이스를 상속 구조와 유사하게 만드는 것입니다. 예를 들어 `Person` 테이블에 이름 필드만 포함 하 고 날짜 필드를 사용 하 여 별도의 `Instructor` 및 `Student` 테이블을 가질 수 있습니다.

![Table-per-type_inheritance](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

각 엔터티 클래스에 대 한 데이터베이스 테이블을 만드는이 패턴을 TPT (형식당 *하나의 테이블* ) 상속 이라고 합니다.

또 다른 옵션은 모든 비추상 형식을 개별 테이블에 매핑하는 것입니다. 상속된 속성을 포함한 모든 클래스 속성을 해당 테이블의 열에 매핑합니다. 이 패턴을 TPC(구체적 클래스당 하나의 테이블) 상속이라고 합니다. 앞에서 설명한 것 처럼 `Person`, `Student`및 `Instructor` 클래스에 대해 TPC 상속을 구현 하는 경우 `Student` 및 `Instructor` 테이블은 이전에 수행한 것 보다 상속을 구현한 후에는 다르게 보입니다.

일반적으로 TPT 패턴은 복잡 한 조인 쿼리를 발생 시킬 수 있기 때문에 TPC 및 TPH 상속 패턴 Entity Framework은 TPT 상속 패턴 보다 더 나은 성능을 제공 합니다.

이 자습서에서는 TPH 상속을 구현하는 방법을 보여 줍니다. TPH는 Entity Framework의 기본 상속 패턴 이므로 `Person` 클래스를 만들고, `Instructor` 및 `Student` 클래스를 `Person`에서 파생 되도록 변경 하 고, 새 클래스를 `DbContext`에 추가 하 고, 마이그레이션을 만듭니다. 다른 상속 패턴을 구현 하는 방법에 대 한 자세한 내용은 MSDN Entity Framework 설명서에서 형식당 [하나의 테이블 상속 매핑](https://msdn.microsoft.com/data/jj591617#2.5) 및 TPC ( [비추상 클래스) 상속 매핑](https://msdn.microsoft.com/data/jj591617#2.6) 을 참조 하세요.

## <a name="create-the-person-class"></a>Person 클래스 만들기

*모델* 폴더에서 *Person.cs* 을 만들고 템플릿 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

## <a name="update-instructor-and-student"></a>강사 및 학생 업데이트

이제 *Instructor.cs* 및 *Student.cs* 를 업데이트 하 여 *Person.sc*에서 값을 상속 합니다.

*Instructor.cs*에서 `Person` 클래스의 `Instructor` 클래스를 파생 하 고 키 및 이름 필드를 제거 합니다. 해당 코드는 다음 예제와 같이 나타납니다.

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

*Student.cs*에 대 한 비슷한 변경을 수행 합니다. `Student` 클래스는 다음 예제와 같습니다.

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="add-person-to-the-model"></a>모델에 사람 추가

*SchoolContext.cs*에서 `Person` 엔터티 형식에 대 한 `DbSet` 속성을 추가 합니다.

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

계층당 하나의 테이블 상속을 구성하기 위해 Entity Framework에 필요한 모든 작업입니다. 여기서 볼 수 있듯이 데이터베이스를 업데이트 하면 `Student` 및 `Instructor` 테이블 대신 `Person` 테이블이 포함 됩니다.

## <a name="create-and-update-migrations"></a>마이그레이션 만들기 및 업데이트

패키지 관리자 콘솔 (PMC)에서 다음 명령을 입력 합니다.

`Add-Migration Inheritance`

PMC에서 `Update-Database` 명령을 실행 합니다. 마이그레이션에서 처리 방법을 알지 못하는 기존 데이터가 있으므로이 시점에서 명령이 실패 합니다. 다음과 같은 오류 메시지가 표시 됩니다.

> *개체 ' dbo '를 삭제할 수 없습니다. 강사 '는 FOREIGN KEY 제약 조건에 의해 참조 되므로*

*마이그레이션\&l t; 타임 스탬프&gt;\_Inheritance.cs* 을 열고 `Up` 메서드를 다음 코드로 바꿉니다.

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

이 코드는 다음과 같은 데이터베이스 업데이트 작업을 처리합니다.

- Student 테이블을 가리키는 외래 키 제약 조건 및 인덱스를 제거합니다.
- Instructor 테이블 이름을 Person으로 바꾸고 Student 데이터를 저장하기 위해 필요한 변경을 수행합니다.

    - 학생에 대한 Nullable EnrollmentDate를 추가합니다.
    - 행이 학생용인지, 강사용인지 나타내는 판별자 열을 추가합니다.
    - 학생 행은 고용 날짜를 포함하지 않으므로 HireDate를 Nullable로 설정합니다.
    - 학생을 가리키는 외래 키를 업데이트하는 데 사용할 임시 필드를 추가합니다. Person 테이블에 학생을 복사 하면 새 기본 키 값이 얻게 됩니다.
- Student 테이블에서 Person 테이블로 데이터를 복사합니다. 그러면 학생에게 새 기본 키 값이 할당됩니다.
- 학생을 가리키는 외래 키 값을 수정합니다.
- 이제 Person 테이블을 가리키도록 외래 키 제약 조건 및 인덱스를 다시 만듭니다.

(기본 키 형식으로 정수 대신 GUID를 사용한 경우, 학생 기본 키 값을 변경할 필요가 없으며 이 단계 중 일부가 생략되었을 수 있습니다.)

`update-database` 명령을 다시 실행합니다.

프로덕션 시스템에서는 이전 데이터베이스 버전으로 다시 이동 하는 데 사용 해야 하는 경우에는 Down 메서드를 변경 해야 합니다. 이 자습서에서는 Down 메서드를 사용 하지 않습니다.

> [!NOTE]
> 데이터를 마이그레이션하고 스키마를 변경 하는 경우 다른 오류가 발생할 수 있습니다. 해결할 수 없는 마이그레이션 오류가 발생 하면 *web.config 파일에서* 연결 문자열을 변경 하거나 데이터베이스를 삭제 하 여 자습서를 계속 진행할 수 있습니다. 가장 간단한 방법은 web.config 파일에서 데이터베이스 이름을 바꾸는 것 *입니다.* 예를 들어 다음 예제와 같이 데이터베이스 이름을 ContosoUniversity2로 변경 합니다.
>
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.xml?highlight=2)]
>
> 새 데이터베이스를 사용 하면 마이그레이션할 데이터가 없으며 `update-database` 명령이 오류 없이 완료 될 가능성이 훨씬 높습니다. 데이터베이스를 삭제 하는 방법에 대 한 지침은 [Visual Studio 2012에서 데이터베이스](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)를 삭제 하는 방법을 참조 하세요. 자습서를 계속 진행 하기 위해이 방법을 사용 하는 경우이 자습서의 끝에 있는 배포 단계를 건너뛰거나 새 사이트 및 데이터베이스에 배포 합니다. 이미 배포 하는 동일한 사이트에 업데이트를 배포 하는 경우, 자동으로 마이그레이션을 실행 하면 EF가 동일한 오류를 받게 됩니다. 마이그레이션 오류를 해결 하려면 가장 적합 한 리소스는 Entity Framework 포럼 또는 StackOverflow.com 중 하나입니다.

## <a name="test-the-implementation"></a>구현 테스트

사이트를 실행 하 고 다양 한 페이지를 시도 합니다. 모든 항목이 이전과 같이 작동합니다.

**서버 탐색기** 에서 **Data Connections\SchoolContext** 및 **Tables**를 확장 하면 **Student** 및 **강사** 테이블이 **Person** 테이블로 대체 된 것을 볼 수 있습니다. **Person** 테이블을 확장 하면 **Student** 및 **강사** 테이블에 사용 되는 모든 열이 포함 되어 있는 것을 볼 수 있습니다.

Person 테이블을 마우스 오른쪽 단추로 클릭한 후 **테이블 데이터 표시**를 클릭하여 판별자 열을 표시합니다.

다음 다이어그램에서는 새 School 데이터베이스의 구조를 보여 줍니다.

![School_database_diagram](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

## <a name="deploy-to-azure"></a>Azure에 배포

이 섹션에서는이 자습서 시리즈의 [3 부, 정렬, 필터링 및 페이징](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md) 에서 선택적으로 **Azure에 앱 배포** 섹션을 완료 해야 합니다. 로컬 프로젝트에서 데이터베이스를 삭제 하 여 마이그레이션 오류가 해결 된 경우에는이 단계를 건너뜁니다. 또는 새 사이트 및 데이터베이스를 만들고 새 환경에 배포 합니다.

1. Visual Studio의 **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **게시**를 선택합니다.

2. **게시**를 클릭합니다.

    웹 앱이 기본 브라우저에서 열립니다.

3. 응용 프로그램을 테스트 하 여 작동 하는지 확인 합니다.

    데이터베이스에 액세스 하는 페이지를 처음 실행 하는 경우 Entity Framework는 현재 데이터 모델을 사용 하 여 데이터베이스를 최신 상태로 만드는 데 필요한 모든 마이그레이션 `Up` 메서드를 실행 합니다.

## <a name="get-the-code"></a>코드 가져오기

[완료 된 프로젝트 다운로드](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>추가 자료

[ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)에서 다른 Entity Framework 리소스에 대 한 링크를 찾을 수 있습니다.

이 및 다른 상속 구조에 대 한 자세한 내용은 MSDN의 [TPT 상속 패턴](https://msdn.microsoft.com/data/jj618293) 및 [TPH 상속 패턴](https://msdn.microsoft.com/data/jj618292) 을 참조 하세요. 다음 자습서에서는 다양한 고급 Entity Framework 시나리오를 처리하는 방법을 살펴봅니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음과 같은 작업을 수행합니다.

> [!div class="checklist"]
> * 상속을 데이터베이스로 매핑하기 위해 배웠습니다.
> * Person 클래스 만들기
> * 강사 및 학생 업데이트
> * 모델에 개인 추가
> * 마이그레이션 생성 및 업데이트
> * 구현 테스트
> * Azure에 배포

Entity Framework Code First를 사용 하는 ASP.NET 웹 응용 프로그램을 개발 하는 기본 사항을 벗어날 때 알아두어야 하는 유용한 항목에 대해 알아보려면 다음 문서로 이동 합니다.
> [!div class="nextstepaction"]
> [고급 Entity Framework 시나리오](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
