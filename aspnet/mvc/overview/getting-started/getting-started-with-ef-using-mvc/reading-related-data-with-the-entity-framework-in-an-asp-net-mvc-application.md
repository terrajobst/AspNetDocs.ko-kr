---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: '자습서: ASP.NET MVC 앱에서 EF를 사용 하 여 관련 데이터 읽기'
description: 이 자습서에서는 관련 데이터 (즉, Entity Framework에서 탐색 속성으로 로드 하는 데이터)를 읽고 표시 합니다.
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: 18cdd896-8ed9-4547-b143-114711e3eafb
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: d804c8dd45ad131949260c85d9d9c6683bfe9646
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445653"
---
# <a name="tutorial-read-related-data-with-ef-in-an-aspnet-mvc-app"></a>자습서: ASP.NET MVC 앱에서 EF를 사용 하 여 관련 데이터 읽기

이전 자습서에서는 School 데이터 모델을 완료 했습니다. 이 자습서에서는 관련 데이터 (즉, Entity Framework에서 탐색 속성으로 로드 하는 데이터)를 읽고 표시 합니다.

다음 그림에서는 사용할 페이지를 보여 줍니다.

![](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)

> Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 6 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요.

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * 관련 데이터를 로드하는 방법 알아보기
> * 강좌 페이지 만들기
> * 강사 페이지 만들기

## <a name="prerequisites"></a>전제 조건

* [더 복잡 한 데이터 모델 만들기](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)

## <a name="learn-how-to-load-related-data"></a>관련 데이터를 로드하는 방법 알아보기

Entity Framework는 엔터티의 탐색 속성에 관련 데이터를 로드할 수 있는 여러 가지 방법이 있습니다.

- *지연 로드*. 엔터티를 처음 읽을 때 관련된 데이터가 검색되지 않습니다. 그러나 탐색 속성에 처음으로 액세스하려고 할 때 해당 탐색 속성에 필요한 데이터가 자동으로 검색됩니다. 이렇게 하면 여러 개의 쿼리가 데이터베이스에 전송 됩니다. 하나는 엔터티 자체를 위한 것이 고 다른 하나는 엔터티에 대 한 관련 데이터를 검색 해야 하는 경우입니다. `DbContext` 클래스는 기본적으로 지연 로드를 사용 하도록 설정 합니다.

    ![Lazy_loading_example](https://asp.net/media/2577850/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Lazy_loading_example_2c44eabb-5fd3-485a-837d-8e3d053f2c0c.png)
- *즉시 로드*. 엔터티를 읽을 때 관련된 데이터가 함께 검색됩니다. 이는 일반적으로 필요한 데이터를 모두 검색하는 단일 조인 쿼리를 발생시킵니다. `Include` 메서드를 사용 하 여 즉시 로드를 지정 합니다.

    ![Eager_loading_example](https://asp.net/media/2577856/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Eager_loading_example_33f907ff-f0b0-4057-8e75-05a8cacac807.png)
- *명시적 로드*. 코드에서 관련 데이터를 명시적으로 검색 하는 경우를 제외 하 고는 지연 로드와 비슷합니다. 탐색 속성에 액세스 하는 경우 자동으로 발생 하지 않습니다. 엔터티에 대 한 개체 상태 관리자 항목을 가져오고 컬렉션에 대 한 [컬렉션. load](https://msdn.microsoft.com/library/gg696220(v=vs.103).aspx) 메서드를 호출 하거나 단일 엔터티를 포함 하는 속성에 대 한 [Reference. load](https://msdn.microsoft.com/library/gg679166(v=vs.103).aspx) 메서드를 호출 하 여 관련 데이터를 수동으로 로드 합니다. (다음 예제에서는 관리자 탐색 속성을 로드 하려는 경우 `Collection(x => x.Courses)`를 `Reference(x => x.Administrator)`으로 바꿉니다.) 일반적으로는 지연 로드를 해제 한 경우에만 명시적 로드를 사용 합니다.

    ![Explicit_loading_example](https://asp.net/media/2577862/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Explicit_loading_example_79d8c368-6d82-426f-be9a-2b443644ab15.png)

속성 값을 즉시 검색 하지 않으므로 지연 로드 및 명시적 로드도 모두 *지연 된 로드*라고도 합니다.

### <a name="performance-considerations"></a>성능 고려 사항

검색된 모든 엔터티에 대해 관련된 데이터가 필요한 경우 데이터베이스에 전송된 단일 쿼리는 검색된 각 엔터티에 대한 별도 쿼리보다 일반적으로 더 효율적이므로 즉시 로드는 종종 최상의 성능을 제공합니다. 예를 들어 위의 예제에서 각 부서에는 10 개의 관련 된 강좌가 있다고 가정 합니다. 즉시 로드 예제에서는 단일 (조인) 쿼리와 데이터베이스에 대 한 단일 왕복만 발생 합니다. 지연 로드 및 명시적 로드 예제는 모두 11 개의 쿼리를 생성 하 고 데이터베이스에 대해 11 번 왕복 합니다. 데이터베이스에 대한 추가 왕복은 대기 시간이 길 때 성능에 특히 악영향을 줍니다.

반면에 일부 시나리오에서는 지연 로드가 더 효율적입니다. 즉시 로드 하면 매우 복잡 한 조인이 생성 될 수 있으며,이로 인해 SQL Server 효율적으로 처리할 수 없습니다. 또는 처리 중인 엔터티 집합의 하위 집합에 대해서만 엔터티의 탐색 속성에 액세스 해야 하는 경우 즉시 로드에서 필요한 것 보다 더 많은 데이터를 검색 하기 때문에 지연 로드 성능이 향상 될 수 있습니다. 성능이 중요한 경우 최상의 선택을 위해 두 가지 방식으로 성능을 테스트하는 것이 가장 좋습니다.

지연 로드는 성능 문제를 발생 시키는 코드를 마스킹할 수 있습니다. 예를 들어 선행 또는 명시적 로드를 지정 하지는 않지만 많은 엔터티를 처리 하 고 각 반복에서 여러 탐색 속성을 사용 하는 코드는 데이터베이스에 대 한 많은 왕복으로 인해 매우 비효율적입니다. 온-프레미스 SQL server를 사용 하 여 개발을 원활 하 게 수행 하는 응용 프로그램은 대기 시간이 늘어나고 지연 로드로 인해 Azure SQL Database으로 이동할 때 성능 문제가 발생할 수 있습니다. 현실적인 테스트 로드를 사용 하 여 데이터베이스 쿼리를 프로 파일링 하면 지연 로드가 적절 한지 여부를 확인 하는 데 도움이 됩니다. 자세한 내용은 [전문가가 제공 자세히 Entity Framework 전략: 관련 데이터 로드](https://msdn.microsoft.com/magazine/hh205756.aspx) 및 Entity Framework를 [사용 하 여 SQL Azure에 대 한 네트워크 대기 시간 줄이기를](https://msdn.microsoft.com/magazine/gg309181.aspx)참조 하세요.

### <a name="disable-lazy-loading-before-serialization"></a>Serialization 전 지연 로드 사용 안 함

Serialization 중에 지연 로드를 사용 하도록 설정 하는 경우 의도 한 것 보다 훨씬 더 많은 데이터를 쿼리할 수 있습니다. Serialization은 일반적으로 형식의 인스턴스에서 각 속성에 액세스 하는 방식으로 작동 합니다. 속성 액세스는 지연 로드를 트리거하고 지연 로드 된 엔터티는 serialize 됩니다. 그러면 serialization 프로세스가 지연 로드 된 엔터티의 각 속성에 액세스 하 여 더 많은 지연 로드 및 serialization을 발생 시킬 수 있습니다. 이 실행 체인 반응을 방지 하려면 엔터티를 serialize 하기 전에 지연 로드를 해제 합니다.

[고급 시나리오 자습서](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#proxies)에 설명 된 대로 Entity Framework에서 사용 하는 프록시 클래스를 사용 하 여 Serialization을 복잡할 수도 있습니다.

Serialization 문제를 방지 하는 한 가지 방법은 [Entity Framework 웹 API 사용](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-5.md) 자습서에 표시 된 것 처럼 엔터티 개체 대신 dto (데이터 전송 개체)를 serialize 하는 것입니다.

Dto를 사용 하지 않는 경우 지연 로드를 사용 하지 않도록 설정 하 고 프록시를 [만들지 않도록 설정](https://msdn.microsoft.com/data/jj592886.aspx)하 여 프록시 문제를 방지할 수 있습니다.

[지연 로드를 사용 하지 않도록 설정 하](https://msdn.microsoft.com/data/jj574232)는 다른 몇 가지 방법은 다음과 같습니다.

- 특정 탐색 속성의 경우 속성을 선언할 때 `virtual` 키워드를 생략 합니다.
- 모든 탐색 속성에 대해 `LazyLoadingEnabled`를 `false`로 설정 하 고 컨텍스트 클래스의 생성자에 다음 코드를 입력 합니다.

    [!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

## <a name="create-a-courses-page"></a>강좌 페이지 만들기

`Course` 엔터티에는 코스가 할당 된 부서의 `Department` 엔터티를 포함 하는 탐색 속성이 포함 되어 있습니다. 과정 목록에 할당 된 학과의 이름을 표시 하려면 `Course.Department` 탐색 속성에 있는 `Department` 엔터티에서 `Name` 속성을 가져와야 합니다.

`Student` 컨트롤러에 대해 이전에 수행한 Entity Framework 스 캐 폴더를 **사용 하 여 뷰가 포함 된 MVC 5 컨트롤러** 에 대해 동일한 옵션을 사용 하 여 `Course` 엔터티 형식에 대해 `CourseController` (not CoursesController) 라는 컨트롤러를 만듭니다.

| 설정 | 값 |
| ------- | ----- |
| 모델 클래스 | **과정 (ContosoUniversity)** 을 선택 합니다. |
| 데이터 컨텍스트 클래스 | **Schoolcontext.cs (ContosoUniversity)** 를 선택 합니다. |
| 컨트롤러 이름 | *CourseController*를 입력 합니다. 다시, *s*로 *CoursesController* 하지 않습니다. **강좌 (ContosoUniversity)** 를 선택 하면 **컨트롤러 이름** 값이 자동으로 채워집니다. 값을 변경 해야 합니다. |

다른 기본값을 그대로 두고 컨트롤러를 추가 합니다.

*Controllers\CourseController.cs* 를 열고 `Index` 메서드를 확인 합니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

자동 스캐폴딩은 `Department` 메서드를 사용하여 `Include` 탐색 속성에 대해 즉시 로드를 지정했습니다.

*Views\Course\Index.cshtml* 를 열고 템플릿 코드를 다음 코드로 바꿉니다. 변경 내용은 강조 표시되어 있습니다.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=4,7,14-16,23-25,31-33,40-42)]

스캐폴드 코드에 다음 변경 내용을 만들었습니다.

- 머리글을 **인덱스** 에서 **과정**으로 변경 했습니다.
- **속성 값을 보여 주는**Number`CourseID` 열을 추가했습니다. 기본적으로 기본 키는 일반적으로 최종 사용자에 게 의미가 없기 때문에 스 캐 폴드 되지 않습니다. 그러나 이 경우 기본 키는 의미가 있으며 표시하길 원합니다.
- **부서** 열을 오른쪽으로 이동 하 고 머리글을 변경 했습니다. 스 캐 폴더가 `Department` 엔터티에서 `Name` 속성을 표시 하도록 올바르게 선택 되어 있지만 과정 페이지에서 열 머리글은 **이름이**아니라 **부서** 여야 합니다.

부서 열에 대해 스 캐 폴드 코드는 `Department` 탐색 속성에 로드 된 `Department` 엔터티의 `Name` 속성을 표시 합니다.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=2)]

페이지를 실행 하 여 (Contoso 대학 홈 페이지에서 **과정** 탭 선택) 부서 이름이 있는 목록을 표시 합니다.

## <a name="create-an-instructors-page"></a>강사 페이지 만들기

이 섹션에서는 강사 페이지를 표시 하기 위해 `Instructor` 엔터티에 대 한 컨트롤러 및 뷰를 만듭니다. 이 페이지는 다음과 같은 방법으로 관련된 데이터를 읽고 표시합니다.

- 강사 목록은 `OfficeAssignment` 엔터티에서 관련 된 데이터를 표시 합니다. `Instructor` 및 `OfficeAssignment` 엔터티는 일대영 또는 일 관계에 있습니다. `OfficeAssignment` 엔터티에 대해 즉시 로드를 사용 합니다. 이전에 설명한 대로 기본 테이블의 검색된 모든 행에 관련된 데이터가 필요한 경우 즉시 로드는 일반적으로 더 효율적입니다. 이 경우 표시된 모든 강사에 대한 사무실 할당을 표시하길 원합니다.
- 사용자가 강사를 선택하면 관련된 `Course` 엔터티가 표시됩니다. `Instructor` 및 `Course` 엔터티는 다대다 관계에 있습니다. `Course` 엔터티 및 관련 `Department` 엔터티에 대해 즉시 로드를 사용 합니다. 이 경우 선택한 강사에 대해서만 강좌가 필요 하므로 지연 로드가 더 효율적일 수 있습니다. 그러나 이 예제에서는 탐색 속성에 있는 엔터티 내에서 탐색 속성에 대한 즉시 로드를 사용하는 방법을 보여 줍니다.
- 사용자가 강좌를 선택 하면 `Enrollments` 엔터티 집합의 관련 데이터가 표시 됩니다. `Course` 및 `Enrollment` 엔터티는 일대다 관계에 있습니다. `Enrollment` 엔터티 및 관련 `Student` 엔터티에 대 한 명시적 로드를 추가 합니다. 지연 로드를 사용 하도록 설정 되어 있지만 명시적 로드를 수행 하는 방법을 보여 주는 명시적 로드는 필요 하지 않습니다.

### <a name="create-a-view-model-for-the-instructor-index-view"></a>강사 인덱스 뷰에 대 한 뷰 모델 만들기

강사 페이지에는 세 개의 다른 테이블이 표시 됩니다. 따라서 각각이 테이블 중 하나에 대한 데이터를 보유하는 세 가지 속성을 포함하는 보기 모델을 만듭니다.

*Viewmodels* 폴더에서 *InstructorIndexData.cs* 을 만들고 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

### <a name="create-the-instructor-controller-and-views"></a>강사 컨트롤러 및 보기 만들기

EF 읽기/쓰기 작업을 사용 하 여 `InstructorController` (InstructorsController 아님) 컨트롤러를 만듭니다.

| 설정 | 값 |
| ------- | ----- |
| 모델 클래스 | **강사 (ContosoUniversity)** 를 선택 합니다. |
| 데이터 컨텍스트 클래스 | **Schoolcontext.cs (ContosoUniversity)** 를 선택 합니다. |
| 컨트롤러 이름 | *InstructorController*를 입력 합니다. 다시, *s*로 *InstructorsController* 하지 않습니다. **강좌 (ContosoUniversity)** 를 선택 하면 **컨트롤러 이름** 값이 자동으로 채워집니다. 값을 변경 해야 합니다. |

다른 기본값을 그대로 두고 컨트롤러를 추가 합니다.

*Controllers\InstructorController.cs* 를 열고 `ViewModels` 네임 스페이스에 대 한 `using` 문을 추가 합니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

`Index` 메서드의 스 캐 폴드 코드는 `OfficeAssignment` 탐색 속성에 대해서만 즉시 로드를 지정 합니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

추가 관련 데이터를 로드 하 고 뷰 모델에 배치 하려면 `Index` 메서드를 다음 코드로 바꿉니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

이 메서드는 선택적 경로 데이터 (`id`) 및 선택한 강사와 선택한 과정의 ID 값을 제공 하는 쿼리 문자열 매개 변수 (`courseID`)를 허용 하 고 모든 필요한 데이터를 뷰에 전달 합니다. 매개 변수는 페이지의 **선택** 하이퍼링크에서 제공됩니다.

코드는 보기 모델의 인스턴스를 만들고 강사 목록에 배치하여 시작합니다. 코드는 `Instructor.OfficeAssignment` 및 `Instructor.Courses` 탐색 속성에 대 한 즉시 로드를 지정 합니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs?highlight=3-4)]

두 번째 `Include` 메서드는 코스를 로드 하 고 로드 된 각 과정에 대해 `Course.Department` 탐색 속성에 대해 즉시 로드 합니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

앞서 언급 했 듯이 즉시 로드는 필요 하지 않지만 성능을 향상 시키기 위해 수행 됩니다. 뷰에는 항상 `OfficeAssignment` 엔터티가 필요 하므로 동일한 쿼리에서 가져오는 것이 더 효율적입니다. 웹 페이지에서 강사를 선택 하는 경우에는 `Course` 엔터티가 필요 합니다 .이를 제외 하 고는 페이지가 더 자주 표시 되는 경우를 제외 하 고 페이지가 더 자주 표시 되는 경우에만 시간이 지연 로드 보다 좋습니다.

강사 ID를 선택한 경우 선택한 강사는 보기 모델의 강사 목록에서 검색 됩니다. 그런 다음 해당 강사의 `Courses` 탐색 속성에서 `Course` 엔터티를 사용 하 여 뷰 모델의 `Courses` 속성을 로드 합니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

`Where` 메서드는 컬렉션을 반환 하지만이 경우 해당 메서드에 전달 된 조건으로 인해 단일 `Instructor` 엔터티만 반환 됩니다. `Single` 메서드는 컬렉션을 단일 `Instructor` 엔터티로 변환 합니다. 그러면 해당 엔터티의 `Courses` 속성에 액세스할 수 있습니다.

컬렉션에 항목이 하나만 있음을 알고 있는 경우 컬렉션에 대해 [단일](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx) 메서드를 사용 합니다. `Single` 메서드는 전달 된 컬렉션이 비어 있거나 둘 이상의 항목이 있는 경우 예외를 throw 합니다. [SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx)는 컬렉션이 비어 있는 경우 기본값 (이 경우 `null`)을 반환 하는 입니다. 그러나이 경우에는 예외를 발생 시킵니다 (`null` 참조에서 `Courses` 속성을 찾으려고 시도). 예외 메시지는 문제의 원인을 명확 하 게 나타내는 것이 아닙니다. `Single` 메서드를 호출 하는 경우 `Where` 메서드를 별도로 호출 하는 대신 `Where` 조건을 전달할 수도 있습니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]

위 코드를 아래 코드 대신 사용합니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

다음으로 강좌를 선택한 경우 선택한 강좌가 보기 모델의 강좌 목록에서 검색됩니다. 그런 다음 뷰 모델의 `Enrollments` 속성은 해당 과정의 `Enrollments` 탐색 속성의 `Enrollment` 엔터티를 사용 하 여 로드 됩니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

### <a name="modify-the-instructor-index-view"></a>강사 인덱스 보기 수정

*Views\Instructor\Index.cshtml*에서 템플릿 코드를 다음 코드로 바꿉니다. 변경 내용은 강조 표시되어 있습니다.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1,4,14-18,21,23-28,38-43,45)]

기존 코드에 다음 변경 내용을 만들었습니다.

- 모델 클래스를 `InstructorIndexData`로 변경했습니다.
- 페이지 제목을 **인덱스**에서 **강사**로 변경했습니다.
- `item.OfficeAssignment`가 null이 아닌 경우에만 `item.OfficeAssignment.Location` 표시 하는 **Office** 열을 추가 했습니다. 이는 일 대 영 또는 일 관계 이므로 관련 `OfficeAssignment` 엔터티가 아닐 수 있습니다.

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]
- 선택한 강사의 `tr` 요소에 `class="success"`를 동적으로 추가 하는 코드를 추가 했습니다. [부트스트랩](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap) 클래스를 사용 하 여 선택 된 행의 배경색을 설정 합니다.

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]
- 각 행의 다른 링크 바로 앞에 **선택** 레이블이 지정 된 새 `ActionLink`을 추가 하 여 선택한 강사 ID가 `Index` 메서드로 전송 되도록 합니다.

응용 프로그램을 실행 하 고 **강사** 탭을 선택 합니다. 이 페이지에는 관련 된 `OfficeAssignment` 엔터티의 `Location` 속성이 표시 되 고 관련 된 `OfficeAssignment` 엔터티가 없으면 빈 테이블 셀이 표시 됩니다.

*Views\Instructor\Index.cshtml* 파일에서 파일의 끝에 있는 closing `table` 요소 뒤에 다음 코드를 추가 합니다. 이 코드는 강사가 선택된 경우 강사와 관련된 강좌의 목록을 표시합니다.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

이 코드는 보기 모델의 `Courses` 속성을 읽어 강좌의 목록을 표시합니다. 또한 `Index` 작업 메서드로 선택한 과정의 ID를 전송 하는 `Select` 하이퍼링크를 제공 합니다.

페이지를 실행 하 고 강사를 선택 합니다. 이제 선택된 강사에 할당된 강좌를 표시하는 표가 표시되고 각 강좌에 대해 할당된 부서의 이름이 표시됩니다.

방금 추가한 코드 블록 뒤에 다음 코드를 추가합니다. 해당 강좌가 선택된 경우에 강좌에 등록된 학생의 목록을 표시합니다.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

이 코드는 과정에 등록 된 학생의 목록을 표시 하기 위해 뷰 모델의 `Enrollments` 속성을 읽습니다.

페이지를 실행 하 고 강사를 선택 합니다. 그런 다음, 강좌를 선택하여 등록된 학생 및 해당 등급의 목록을 봅니다.

### <a name="adding-explicit-loading"></a>명시적 로드 추가

*InstructorController.cs* 를 열고 `Index` 메서드가 선택한 과정에 대 한 등록 목록을 가져오는 방법을 확인 합니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs)]

강사 목록을 검색할 때 `Courses` 탐색 속성에 대해 즉시 로드를 지정 하 고 각 과정의 `Department` 속성에 대해 즉시 로드를 지정 했습니다. 그런 다음 뷰 모델에 `Courses` 컬렉션을 배치 하면 이제 해당 컬렉션의 한 엔터티에서 `Enrollments` 탐색 속성에 액세스 하 게 됩니다. `Course.Enrollments` 탐색 속성에 대해 즉시 로드를 지정 하지 않았으므로 지연 로드의 결과로 해당 속성의 데이터가 페이지에 표시 됩니다.

다른 방법으로 코드를 변경 하지 않고 지연 로드를 사용 하지 않도록 설정한 경우 `Enrollments` 속성은 실제로 실제로 보유 한 등록 수에 관계 없이 null이 됩니다. 이 경우 `Enrollments` 속성을 로드 하려면 즉시 로드를 지정 하거나 명시적 로드를 지정 해야 합니다. 즉시 로드를 수행 하는 방법을 이미 살펴보았습니다. 명시적 로드의 예제를 보려면 `Index` 메서드를 다음 코드로 바꿉니다 .이 코드는 `Enrollments` 속성을 명시적으로 로드 합니다. 변경 된 코드는 강조 표시 됩니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs?highlight=20-31)]

선택한 `Course` 엔터티를 가져온 후 새 코드는 해당 강좌의 `Enrollments` 탐색 속성을 명시적으로 로드 합니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

그런 다음 각 `Enrollment` 엔터티의 관련 `Student` 엔터티를 명시적으로 로드 합니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cs)]

`Collection` 메서드를 사용 하 여 컬렉션 속성을 로드 하지만 하나의 엔터티만 포함 하는 속성의 경우 `Reference` 메서드를 사용 합니다.

이제 강사 인덱스 페이지를 실행 하면 데이터 검색 방법을 변경 했더라도 페이지에 표시 되는 내용에 차이가 없다는 것을 알 수 있습니다.

## <a name="get-the-code"></a>코드 가져오기

[완료 된 프로젝트 다운로드](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>추가 자료

[ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)에서 다른 Entity Framework 리소스에 대 한 링크를 찾을 수 있습니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * 관련 데이터를 로드하는 방법 알아보기
> * 강좌 페이지 만들기
> * 강사 페이지 만들기

관련 데이터를 업데이트하는 방법을 알아보려면 다음 문서로 진행합니다.

> [!div class="nextstepaction"]
> [관련 데이터 업데이트](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
