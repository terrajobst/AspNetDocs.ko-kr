---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
title: ASP.NET MVC 응용 프로그램에서 리포지토리 및 작업 단위 패턴 구현 (9/10) | Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다.
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 44761193-04ba-4990-9f90-145d3c10a716
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 18de9b125ee5d10795b9ce1a366918dadf4fc4e3
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595236"
---
# <a name="implementing-the-repository-and-unit-of-work-patterns-in-an-aspnet-mvc-application-9-of-10"></a>ASP.NET MVC 응용 프로그램에서 리포지토리 및 작업 단위 패턴 구현 (9/10)

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 5 Code First 및 Visual Studio 2012을 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요. [이 챕터의](building-the-ef5-mvc4-chapter-downloads.md) 시작 또는 시작 프로젝트 다운로드에서 자습서 시리즈를 시작 하 고 여기에서 시작할 수 있습니다.
> 
> > [!NOTE] 
> > 
> > 해결할 수 없는 문제가 발생 하는 경우 [완료 된 챕터를 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 하 여 문제를 재현해 보세요. 일반적으로 코드를 완성 된 코드와 비교 하 여 문제에 대 한 솔루션을 찾을 수 있습니다. 몇 가지 일반적인 오류 및 해결 방법에 대 한 자세한 내용은 [오류 및 해결](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors) 방법을 참조 하세요.

이전 자습서에서는 상속을 사용 하 여 `Student` 및 `Instructor` 엔터티 클래스에서 중복 코드를 줄이고 있습니다. 이 자습서에서는 CRUD 작업에 대 한 작업 패턴의 리포지토리 및 단위를 사용 하는 몇 가지 방법을 알아봅니다. 이전 자습서에서와 같이이 자습서에서는 새 페이지를 만드는 대신 이미 만든 페이지에서 코드가 작동 하는 방식을 변경 합니다.

## <a name="the-repository-and-unit-of-work-patterns"></a>리포지토리 및 작업 단위 패턴

리포지토리 및 작업 단위 패턴은 응용 프로그램의 비즈니스 논리 계층 및 데이터 액세스 계층 간에 추상화 계층을 만들기 위한 것입니다. 이러한 패턴을 구현하면 데이터 저장소의 변경 내용으로부터 애플리케이션을 격리할 수 있으며 자동화된 단위 테스트 또는 TDD(테스트 중심 개발)를 용이하게 수행할 수 있습니다.

이 자습서에서는 각 엔터티 형식에 대 한 리포지토리 클래스를 구현 합니다. 엔터티 형식 `Student` 리포지토리 인터페이스와 리포지토리 클래스를 만듭니다. 컨트롤러에서 리포지토리를 인스턴스화하면 컨트롤러에서 리포지토리 인터페이스를 구현 하는 개체에 대 한 참조를 허용 하도록 인터페이스를 사용 합니다. 컨트롤러는 웹 서버에서 실행 될 때 Entity Framework 작동 하는 리포지토리를 수신 합니다. 컨트롤러는 단위 테스트 클래스에서 실행 될 때 메모리 내 컬렉션과 같이 테스트를 위해 쉽게 조작할 수 있는 방식으로 저장 된 데이터와 함께 작동 하는 리포지토리를 수신 합니다.

자습서의 뒷부분에서는 `Course`에 대 한 여러 리포지토리와 작업 단위 클래스를 사용 하 고 `Course` 컨트롤러에서 엔터티 형식을 `Department` 합니다. 작업 단위 클래스는 모두 공유 하는 단일 데이터베이스 컨텍스트 클래스를 만들어 여러 리포지토리의 작업을 조정 합니다. 자동화 된 단위 테스트를 수행 하려면 `Student` 리포지토리에 대해 수행한 것과 동일한 방식으로 이러한 클래스에 대 한 인터페이스를 만들고 사용 합니다. 그러나 자습서를 단순하게 유지 하기 위해 인터페이스 없이 이러한 클래스를 만들고 사용 합니다.

다음 그림에서는 리포지토리 또는 작업 단위 패턴을 사용 하지 않는 것과 비교 하 여 컨트롤러와 컨텍스트 클래스 간의 관계를 설명 하는 한 가지 방법을 보여 줍니다.

![Repository_pattern_diagram](https://asp.net/media/2578149/Windows-Live-Writer_8c4963ba1fa3_CE3B_Repository_pattern_diagram_1df790d3-bdf2-4c11-9098-946ddd9cd884.png)

이 자습서 시리즈에서는 단위 테스트를 만들지 않습니다. 리포지토리 패턴을 사용 하는 MVC 응용 프로그램의 TDD에 대 한 소개는 [연습: ASP.NET MVC와 함께 Tdd 사용](https://msdn.microsoft.com/library/ff847525.aspx)을 참조 하세요. 리포지토리 패턴에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- MSDN의 [리포지토리 패턴](https://msdn.microsoft.com/library/ff649690.aspx)
- Entity Framework 팀 블로그에서 [Entity Framework 4.0를 사용 하 여 리포지토리 및 작업 단위 패턴을 사용](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx) 합니다.
- [Agile Entity Framework 4 리포지토리](http://thedatafarm.com/blog/data-access/agile-entity-framework-4-repository-part-1-model-and-poco-classes/) 시리즈 Julie Lerman의 블로그 시리즈
- Dan Wahlin의 블로그에서 [잠깐의 HTML5/JQuery 응용 프로그램에서 계정을 작성](https://weblogs.asp.net/dwahlin/archive/2011/08/15/building-the-account-at-a-glance-html5-jquery-application.aspx) 합니다.

> [!NOTE]
> 리포지토리 및 작업 패턴 단위를 구현 하는 방법에는 여러 가지가 있습니다. 작업 단위 클래스를 포함 하거나 포함 하지 않고 리포지토리 클래스를 사용할 수 있습니다. 모든 엔터티 형식 또는 각 형식에 대해 하나의 리포지토리를 구현할 수 있습니다. 각 형식에 대해 하나를 구현 하는 경우 별도의 클래스, 제네릭 기본 클래스 및 파생 클래스, 추상 기본 클래스 및 파생 클래스를 사용할 수 있습니다. 저장소에 비즈니스 논리를 포함 하거나 데이터 액세스 논리로 제한할 수 있습니다. 엔터티 집합에 대해 [Dbset](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) 형식 대신 [IDbSet](https://msdn.microsoft.com/library/gg679233(v=vs.103).aspx) 인터페이스를 사용 하 여 데이터베이스 컨텍스트 클래스에 추상 계층을 빌드할 수도 있습니다. 이 자습서에 표시 된 추상화 계층을 구현 하는 방법은 모든 시나리오와 환경에 대 한 권장 사항은 아니라 고려해 야 할 한 가지 옵션입니다.

## <a name="creating-the-student-repository-class"></a>학생 리포지토리 클래스 만들기

*DAL* 폴더에서 *IStudentRepository.cs* 라는 클래스 파일을 만들고 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample1.cs)]

이 코드는 두 개의 읽기 메서드를 포함 하는 일반적인 CRUD 메서드 집합을 선언 합니다. 하나는 모든 `Student` 엔터티를 반환 하 고 다른 하나는 ID로 단일 `Student` 엔터티를 찾습니다.

*DAL* 폴더에서 *StudentRepository.cs* file 이라는 클래스 파일을 만듭니다. 기존 코드를 `IStudentRepository` 인터페이스를 구현 하는 다음 코드로 바꿉니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample2.cs)]

데이터베이스 컨텍스트는 클래스 변수에 정의 되 고 생성자는 호출 하는 개체가 컨텍스트의 인스턴스를 전달 하는 것으로 예상 합니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample3.cs)]

리포지토리에서 새 컨텍스트를 인스턴스화할 수 있지만 한 컨트롤러에서 여러 리포지토리를 사용 하는 경우 각각은 별도의 컨텍스트로 종료 됩니다. 나중에 `Course` 컨트롤러에서 여러 리포지토리를 사용 하 고 작업 단위 클래스에서 모든 리포지토리가 동일한 컨텍스트를 사용 하도록 하는 방법을 확인할 수 있습니다.

리포지토리는 [IDisposable](https://msdn.microsoft.com/library/system.idisposable.aspx) 을 구현 하 고 컨트롤러에서 앞서 살펴본 것 처럼 데이터베이스 컨텍스트를 삭제 하며, CRUD 메서드는 앞에서 살펴본 것과 같은 방식으로 데이터베이스 컨텍스트를 호출 합니다.

## <a name="change-the-student-controller-to-use-the-repository"></a>리포지토리를 사용 하도록 학생 컨트롤러 변경

*StudentController.cs*에서 클래스의 현재 코드를 다음 코드로 바꿉니다. 변경 내용은 강조 표시되어 있습니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=13-18,44,75,77,102-103,120,137-138,159,172-174,186)]

이제 컨트롤러는 컨텍스트 클래스 대신 `IStudentRepository` 인터페이스를 구현 하는 개체에 대 한 클래스 변수를 선언 합니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample5.cs)]

기본 (매개 변수가 없는) 생성자는 새 컨텍스트 인스턴스를 만들고 선택적 생성자를 사용 하면 호출자가 컨텍스트 인스턴스를 전달할 수 있습니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample6.cs)]

( *종속성 주입*또는 di를 사용 하는 경우 di 소프트웨어에서 올바른 리포지토리 개체가 항상 제공 되도록 하기 때문에 기본 생성자가 필요 하지 않습니다.)

CRUD 메서드에서는 이제 컨텍스트 대신 리포지토리가 호출 됩니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample7.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample8.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample9.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample10.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample11.cs)]

그리고 `Dispose` 메서드는 이제 컨텍스트 대신 리포지토리를 삭제 합니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample12.cs)]

사이트를 실행 하 고 **학생** 탭을 클릭 합니다.

![Students_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image1.png)

이 페이지는 리포지토리를 사용 하기 위해 코드를 변경 하기 전과 동일 하 게 작동 하며 다른 학생 페이지도 동일 하 게 작동 합니다. 그러나 컨트롤러의 `Index` 메서드가 필터링 하 고 순서를 지정 하는 방법에는 중요 한 차이점이 있습니다. 이 메서드의 원래 버전에는 다음 코드가 포함 되어 있습니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample13.cs?highlight=1)]

업데이트 된 `Index` 메서드는 다음 코드를 포함 합니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=1)]

강조 표시 된 코드만 변경 되었습니다.

코드의 원래 버전에서 `students`은 `IQueryable` 개체로 형식화 됩니다. 쿼리가 `ToList`와 같은 메서드를 사용 하 여 컬렉션으로 변환 될 때까지 데이터베이스에 전송 되지 않습니다 .이는 인덱스 뷰가 학생 모델에 액세스할 때까지 발생 하지 않습니다. 위의 원래 코드에서 `Where` 메서드는 데이터베이스로 전송 된 SQL 쿼리의 `WHERE` 절이 됩니다. 그러면 선택한 엔터티만 데이터베이스에서 반환 됩니다. 그러나 `context.Students` `studentRepository.GetStudents()`변경 된 결과로이 문 다음에 오는 `students` 변수는 데이터베이스의 모든 학생을 포함 하는 `IEnumerable` 컬렉션입니다. `Where` 메서드를 적용 하는 최종 결과는 동일 하지만 이제는 데이터베이스가 아니라 웹 서버의 메모리에서 작업을 수행 합니다. 대용량의 데이터를 반환 하는 쿼리의 경우 비효율적 일 수 있습니다.

> [!TIP]
> 
> **IQueryable 및 IEnumerable 비교**
> 
> 여기에 표시 된 대로 리포지토리를 구현한 후에는 검색 상자에 항목을 입력 하는 경우에 **도 검색 상자** 에 항목을 입력 해도 검색 조건이 포함 되지 않기 때문에 모든 학생 행이 반환 SQL Server.
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image2.png)
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample15.sql)]
> 
> 이 쿼리는 리포지토리에서 검색 조건에 대해 알지 못해도 쿼리를 실행 했기 때문에 모든 학생 데이터를 반환 합니다. 검색 조건을 적용 하 고, 검색 조건을 적용 하 고, 페이징에 대 한 데이터의 하위 집합을 선택 하는 프로세스 (이 경우에는 3 개의 행만 표시)는 나중에 `IEnumerable` 컬렉션에서 `ToPagedList` 메서드가 호출 될 때 메모리에서 수행 됩니다.
> 
> 이전 버전의 코드에서 (리포지토리를 구현 하기 전에), `IQueryable` 개체에서 `ToPagedList`가 호출 되 면 검색 조건을 적용할 때 까지는 쿼리가 데이터베이스로 전송 되지 않습니다.
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image3.png)
> 
> `IQueryable` 개체에 대해 ToPagedList가 호출 되 면 검색 문자열을 지정 하 SQL Server에 전송 된 쿼리는 검색 조건을 충족 하는 행만 반환 되 고 메모리에서 필터링을 수행 하지 않아도 됩니다.
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample16.sql)]
> 
> 다음 자습서에서는 SQL Server에 전송 된 쿼리를 검사 하는 방법을 설명 합니다.

다음 섹션에서는 데이터베이스에서이 작업을 수행 하도록 지정할 수 있는 리포지토리 메서드를 구현 하는 방법을 보여 줍니다.

이제 컨트롤러와 Entity Framework 데이터베이스 컨텍스트 간에 추상화 계층을 만들었습니다. 이 응용 프로그램을 사용 하 여 자동화 된 단위 테스트를 수행 하려는 경우 `IStudentRepository`를 구현 하는 단위 테스트 프로젝트에 대체 리포지토리 클래스를 만들 수 있습니다 *.* 데이터 읽기 및 쓰기를 위해 컨텍스트를 호출 하는 대신이 모의 리포지토리 클래스는 컨트롤러 함수를 테스트 하기 위해 메모리 내 컬렉션을 조작할 수 있습니다.

## <a name="implement-a-generic-repository-and-a-unit-of-work-class"></a>제네릭 리포지토리 및 작업 단위 클래스 구현

각 엔터티 형식에 대 한 리포지토리 클래스를 만들면 중복 코드가 많이 발생 하 고 부분 업데이트가 발생할 수 있습니다. 예를 들어 동일한 트랜잭션의 일부로 두 개의 다른 엔터티 유형을 업데이트 해야 한다고 가정 합니다. 각각 별도의 데이터베이스 컨텍스트 인스턴스를 사용 하는 경우 하나는 성공 하 고 다른 하나는 실패할 수 있습니다. 중복 코드를 최소화 하는 한 가지 방법은 일반 리포지토리를 사용 하는 것입니다. 즉, 모든 리포지토리에서 동일한 데이터베이스 컨텍스트를 사용 하 고 모든 업데이트를 조정 하는 한 가지 방법은 작업 단위 클래스를 사용 하는 것입니다.

자습서의이 섹션에서는 `GenericRepository` 클래스 및 `UnitOfWork` 클래스를 만들고 `Course` 컨트롤러에서이 클래스를 사용 하 여 `Department` 및 `Course` 엔터티 집합 모두에 액세스 합니다. 앞에서 설명한 대로 자습서의이 부분을 간단 하 게 유지 하기 위해 이러한 클래스에 대 한 인터페이스를 만들지는 않습니다. 그러나이를 사용 하 여 TDD를 용이 하 게 하는 경우 일반적으로 `Student` 리포지토리를 사용 하는 것과 동일한 방식으로 인터페이스를 사용 하 여 구현 합니다.

### <a name="create-a-generic-repository"></a>제네릭 리포지토리 만들기

*DAL* 폴더에서 *GenericRepository.cs* 을 만들고 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample17.cs)]

클래스 변수는 데이터베이스 컨텍스트 및 리포지토리가 인스턴스화된 엔터티 집합에 대해 선언 됩니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample18.cs)]

생성자는 데이터베이스 컨텍스트 인스턴스를 수락 하 고 엔터티 집합 변수를 초기화 합니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample19.cs)]

`Get` 메서드는 람다 식을 사용 하 여 호출 코드에서 필터 조건 및 결과의 순서를 지정 하는 열을 지정 하 고, 문자열 매개 변수를 사용 하 여 호출자는 즉시 로드를 위한 탐색 속성의 쉼표로 구분 된 목록을 제공할 수 있도록 합니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample20.cs)]

코드 `Expression<Func<TEntity, bool>> filter`는 호출자가 `TEntity` 형식을 기반으로 람다 식을 제공 한다는 것을 의미 하며,이 식은 부울 값을 반환 합니다. 예를 들어 `Student` 엔터티 형식에 대해 리포지토리가 인스턴스화된 경우 호출 하는 메서드의 코드는 `filter` 매개 변수에 대 한 `student => student.LastName == "Smith`&quot;를 지정할 수 있습니다.

코드 `Func<IQueryable<TEntity>, IOrderedQueryable<TEntity>> orderBy`는 호출자가 람다 식을 제공 한다는 것을 의미 하기도 합니다. 그러나이 경우 식에 대 한 입력은 `TEntity` 형식에 대 한 `IQueryable` 개체입니다. 이 식은 `IQueryable` 개체의 정렬 된 버전을 반환 합니다. 예를 들어 `Student` 엔터티 형식에 대해 리포지토리가 인스턴스화된 경우 호출 하는 메서드의 코드는 `orderBy` 매개 변수에 대 한 `q => q.OrderBy(s => s.LastName)`를 지정할 수 있습니다.

`Get` 메서드의 코드는 `IQueryable` 개체를 만든 다음 필터 식을 적용 합니다 (있는 경우).

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample21.cs)]

다음은 쉼표로 구분 된 목록을 구문 분석 한 후 즉시 로드 하는 식을 적용 합니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample22.cs)]

마지막으로 `orderBy` 식이 있으면이를 적용 하 고 결과를 반환 합니다. 그렇지 않으면 순서가 지정 되지 않은 쿼리에서 결과를 반환 합니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample23.cs)]

`Get` 메서드를 호출 하는 경우 이러한 함수에 대 한 매개 변수를 제공 하는 대신 메서드에서 반환 된 `IEnumerable` 컬렉션을 필터링 하 고 정렬할 수 있습니다. 그러나 정렬 및 필터링 작업은 웹 서버의 메모리에서 수행 됩니다. 이러한 매개 변수를 사용 하 여 웹 서버가 아닌 데이터베이스에서 작업을 수행 하는지 확인 합니다. 다른 방법은 특정 엔터티 형식에 대 한 파생 클래스를 만들고 `GetStudentsInNameOrder` 또는 `GetStudentsByName`와 같은 특수 한 `Get` 메서드를 추가 하는 것입니다. 그러나 복잡 한 응용 프로그램에서는 이러한 파생 클래스와 특수 메서드를 많이 사용할 수 있으며,이로 인해 더 많은 작업을 유지 관리할 수 있습니다.

`GetByID`, `Insert`및 `Update` 메서드의 코드는 제네릭이 아닌 리포지토리에서 보았던 코드와 비슷합니다. `Find` 메서드를 사용 하 여 즉시 로드할 수 없기 때문에 `GetByID` 시그니처에서 즉시 로드 매개 변수를 제공 하지 않습니다.

`Delete` 메서드에는 두 개의 오버 로드가 제공 됩니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample24.cs)]

이 중 하나를 사용 하 여 삭제할 엔터티의 ID만 전달할 수 있으며, 엔터티 인스턴스를 사용 합니다. [동시성](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) 처리 자습서에서 살펴본 것 처럼 동시성 처리를 위해 추적 속성의 원래 값을 포함 하는 엔터티 인스턴스를 사용 하는 `Delete` 메서드가 필요 합니다.

이 일반 리포지토리는 일반적인 CRUD 요구 사항을 처리 합니다. 특정 엔터티 형식에 더 복잡 한 필터링 또는 정렬과 같은 특수 요구 사항이 있는 경우 해당 형식에 대 한 추가 메서드가 있는 파생 클래스를 만들 수 있습니다.

## <a name="creating-the-unit-of-work-class"></a>작업 단위 클래스 만들기

작업 단위 클래스는 한 가지 용도로 사용 됩니다. 여러 리포지토리를 사용 하는 경우 단일 데이터베이스 컨텍스트를 공유 하는지 확인 합니다. 이렇게 하면 작업 단위가 완료 되 면 컨텍스트의 해당 인스턴스에서 `SaveChanges` 메서드를 호출 하 고 모든 관련 변경 내용이 조정 되도록 보장할 수 있습니다. 클래스가 필요로 하는 모든 것은 `Save` 메서드와 각 리포지토리의 속성입니다. 각 리포지토리 속성은 다른 리포지토리 인스턴스와 동일한 데이터베이스 컨텍스트 인스턴스를 사용 하 여 인스턴스화된 리포지토리 인스턴스를 반환 합니다.

*DAL* 폴더에서 *UnitOfWork.cs* 라는 클래스 파일을 만들고 템플릿 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample25.cs)]

이 코드는 데이터베이스 컨텍스트와 각 리포지토리에 대 한 클래스 변수를 만듭니다. `context` 변수의 경우 새 컨텍스트가 인스턴스화됩니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample26.cs)]

각 리포지토리 속성은 리포지토리가 이미 있는지 여부를 확인 합니다. 그렇지 않으면 리포지토리를 인스턴스화하고 컨텍스트 인스턴스를 전달 합니다. 따라서 모든 리포지토리는 동일한 컨텍스트 인스턴스를 공유 합니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample27.cs)]

`Save` 메서드는 데이터베이스 컨텍스트에서 `SaveChanges`를 호출 합니다.

클래스 변수에 데이터베이스 컨텍스트를 인스턴스화하는 클래스와 마찬가지로 `UnitOfWork` 클래스는 `IDisposable`를 구현 하 고 컨텍스트를 삭제 합니다.

### <a name="changing-the-course-controller-to-use-the-unitofwork-class-and-repositories"></a>클라우드 클래스 및 리포지토리를 사용 하도록 강좌 컨트롤러 변경

현재 *CourseController.cs* 에 있는 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample28.cs?highlight=15,20,22,31,54-55,70,85-86,101-102,122-124,130)]

이 코드는 `UnitOfWork` 클래스에 대 한 클래스 변수를 추가 합니다. 여기에서 인터페이스를 사용 하는 경우 여기에서 변수를 초기화 하지 않아도 됩니다. 대신 `Student` 리포지토리에 대해 수행한 것과 동일한 방식으로 두 생성자의 패턴을 구현 합니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample29.cs)]

클래스의 나머지 부분에서 데이터베이스 컨텍스트에 대 한 모든 참조는 리포지토리에 액세스 하는 `UnitOfWork` 속성을 사용 하 여 적절 한 리포지토리에 대 한 참조로 대체 됩니다. `Dispose` 메서드는 `UnitOfWork` 인스턴스를 삭제 합니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample30.cs)]

사이트를 실행 하 고 **강좌** 탭을 클릭 합니다.

![Courses_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image4.png)

페이지는 변경 전과 동일 하 게 표시 되 고 다른 과정 페이지도 동일 하 게 작동 합니다.

## <a name="summary"></a>요약

이제 리포지토리 및 작업 단위 패턴을 모두 구현 했습니다. 람다 식을 제네릭 리포지토리에서 메서드 매개 변수로 사용 했습니다. `IQueryable` 개체에서 이러한 식을 사용 하는 방법에 대 한 자세한 내용은 MSDN Library의 [IQueryable (t) 인터페이스 (system.string)](https://msdn.microsoft.com/library/bb351562.aspx) 를 참조 하세요. 다음 자습서에서는 몇 가지 고급 시나리오를 처리 하는 방법을 배웁니다.

[ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md)에서 다른 Entity Framework 리소스에 대 한 링크를 찾을 수 있습니다.

> [!div class="step-by-step"]
> [이전](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [다음](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
