---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: ASP.NET MVC 응용 프로그램에서 Entity Framework를 사용 하 여 관련 데이터 읽기 (5/10) | Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다.
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 0d6fb83b-71f7-425d-8dec-981197d7ec42
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: e1752022b66952783039fbea0c2880e2f9be6ef8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595217"
---
# <a name="reading-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-5-of-10"></a>ASP.NET MVC 응용 프로그램에서 Entity Framework를 사용 하 여 관련 데이터 읽기 (5/10)

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 5 Code First 및 Visual Studio 2012을 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요. [이 챕터의](building-the-ef5-mvc4-chapter-downloads.md) 시작 또는 시작 프로젝트 다운로드에서 자습서 시리즈를 시작 하 고 여기에서 시작할 수 있습니다.
> 
> > [!NOTE] 
> > 
> > 해결할 수 없는 문제가 발생 하는 경우 [완료 된 챕터를 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 하 여 문제를 재현해 보세요. 일반적으로 코드를 완성 된 코드와 비교 하 여 문제에 대 한 솔루션을 찾을 수 있습니다. 몇 가지 일반적인 오류 및 해결 방법에 대 한 자세한 내용은 [오류 및 해결](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors) 방법을 참조 하세요.

이전 자습서에서는 School 데이터 모델을 완료 했습니다. 이 자습서에서는 관련 데이터 (즉, Entity Framework에서 탐색 속성으로 로드 하는 데이터)를 읽고 표시 합니다.

다음 그림에서는 사용할 페이지를 보여 줍니다.

![](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="lazy-eager-and-explicit-loading-of-related-data"></a>관련 데이터의 지연, 즉시 및 명시적 로드

Entity Framework는 엔터티의 탐색 속성에 관련 데이터를 로드할 수 있는 여러 가지 방법이 있습니다.

- *지연 로드*. 엔터티를 처음 읽을 때 관련된 데이터가 검색되지 않습니다. 그러나 탐색 속성에 처음으로 액세스하려고 할 때 해당 탐색 속성에 필요한 데이터가 자동으로 검색됩니다. 이렇게 하면 여러 개의 쿼리가 데이터베이스에 전송 됩니다. 하나는 엔터티 자체를 위한 것이 고 다른 하나는 엔터티에 대 한 관련 데이터를 검색 해야 하는 경우입니다. 

    ![Lazy_loading_example](https://asp.net/media/2577850/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Lazy_loading_example_2c44eabb-5fd3-485a-837d-8e3d053f2c0c.png)
- *즉시 로드*. 엔터티를 읽을 때 관련된 데이터가 함께 검색됩니다. 이는 일반적으로 필요한 데이터를 모두 검색하는 단일 조인 쿼리를 발생시킵니다. `Include` 메서드를 사용 하 여 즉시 로드를 지정 합니다.

    ![Eager_loading_example](https://asp.net/media/2577856/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Eager_loading_example_33f907ff-f0b0-4057-8e75-05a8cacac807.png)
- *명시적 로드*. 코드에서 관련 데이터를 명시적으로 검색 하는 경우를 제외 하 고는 지연 로드와 비슷합니다. 탐색 속성에 액세스 하는 경우 자동으로 발생 하지 않습니다. 엔터티에 대 한 개체 상태 관리자 항목을 가져오고 단일 엔터티를 포함 하는 속성에 대 한 `Reference.Load` 메서드 또는 컬렉션에 대 한 `Collection.Load` 메서드를 호출 하 여 관련 데이터를 수동으로 로드 합니다. (다음 예제에서는 관리자 탐색 속성을 로드 하려는 경우 `Collection(x => x.Courses)`를 `Reference(x => x.Administrator)`으로 바꿉니다.)

    ![Explicit_loading_example](https://asp.net/media/2577862/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Explicit_loading_example_79d8c368-6d82-426f-be9a-2b443644ab15.png)

속성 값을 즉시 검색 하지 않으므로 지연 로드 및 명시적 로드도 모두 *지연 된 로드*라고도 합니다.

일반적으로 검색 되는 모든 엔터티에 대 한 관련 데이터가 필요 하다는 것을 알고 있는 경우 데이터베이스에 전송 되는 단일 쿼리가 검색 된 각 엔터티에 대 한 별도의 쿼리 보다 더 효율적 이기 때문에 즉시 로드는 최상의 성능을 제공 합니다. 예를 들어 위의 예제에서 각 부서에는 10 개의 관련 된 강좌가 있다고 가정 합니다. 즉시 로드 예제에서는 단일 (조인) 쿼리와 데이터베이스에 대 한 단일 왕복만 발생 합니다. 지연 로드 및 명시적 로드 예제는 모두 11 개의 쿼리를 생성 하 고 데이터베이스에 대해 11 번 왕복 합니다. 데이터베이스에 대한 추가 왕복은 대기 시간이 길 때 성능에 특히 악영향을 줍니다.

반면에 일부 시나리오에서는 지연 로드가 더 효율적입니다. 즉시 로드 하면 매우 복잡 한 조인이 생성 될 수 있으며,이로 인해 SQL Server 효율적으로 처리할 수 없습니다. 또는 처리 중인 엔터티 집합의 하위 집합에 대해서만 엔터티의 탐색 속성에 액세스 해야 하는 경우 즉시 로드에서 필요한 것 보다 더 많은 데이터를 검색 하기 때문에 지연 로드 성능이 향상 될 수 있습니다. 성능이 중요한 경우 최상의 선택을 위해 두 가지 방식으로 성능을 테스트하는 것이 가장 좋습니다.

일반적으로는 지연 로드를 해제 한 경우에만 명시적 로드를 사용 합니다. 지연 로드를 해제 해야 하는 한 가지 시나리오는 serialization 중입니다. 지연 로드와 serialization은 함께 사용할 수 없으며, 지연 로드를 사용 하는 경우 의도 한 것 보다 훨씬 더 많은 데이터를 쿼리할 수 있습니다. Serialization은 일반적으로 형식의 인스턴스에서 각 속성에 액세스 하는 방식으로 작동 합니다. 속성 액세스는 지연 로드를 트리거하고 지연 로드 된 엔터티는 serialize 됩니다. 그러면 serialization 프로세스가 지연 로드 된 엔터티의 각 속성에 액세스 하 여 더 많은 지연 로드 및 serialization을 발생 시킬 수 있습니다. 이 실행 체인 반응을 방지 하려면 엔터티를 serialize 하기 전에 지연 로드를 해제 합니다.

데이터베이스 컨텍스트 클래스는 기본적으로 지연 로드를 수행 합니다. 지연 로드를 사용 하지 않도록 설정 하는 방법에는 다음 두 가지가 있습니다.

- 특정 탐색 속성의 경우 속성을 선언할 때 `virtual` 키워드를 생략 합니다.
- 모든 탐색 속성에 대해 `LazyLoadingEnabled`를 `false`로 설정 합니다. 예를 들어 컨텍스트 클래스의 생성자에 다음 코드를 넣을 수 있습니다. 

    [!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

지연 로드는 성능 문제를 발생 시키는 코드를 마스킹할 수 있습니다. 예를 들어 선행 또는 명시적 로드를 지정 하지는 않지만 많은 엔터티를 처리 하 고 각 반복에서 여러 탐색 속성을 사용 하는 코드는 데이터베이스에 대 한 많은 왕복으로 인해 매우 비효율적입니다. 온-프레미스 SQL server를 사용 하 여 개발을 원활 하 게 수행 하는 응용 프로그램은 대기 시간이 늘어나고 지연 로드로 인해 Azure SQL Database으로 이동할 때 성능 문제가 발생할 수 있습니다. 현실적인 테스트 로드를 사용 하 여 데이터베이스 쿼리를 프로 파일링 하면 지연 로드가 적절 한지 여부를 확인 하는 데 도움이 됩니다. 자세한 내용은 [전문가가 제공 자세히 Entity Framework 전략을 참조 하세요. ](https://msdn.microsoft.com/magazine/hh205756.aspx) 관련 된 데이터를 로드 하 고 [Entity Framework를 사용 하 여 네트워크 대기 시간을 SQL Azure으로 줄입니다](https://msdn.microsoft.com/magazine/gg309181.aspx).

## <a name="create-a-courses-index-page-that-displays-department-name"></a>부서 이름을 표시 하는 과정 인덱스 페이지 만들기

`Course` 엔터티에는 코스가 할당 된 부서의 `Department` 엔터티를 포함 하는 탐색 속성이 포함 되어 있습니다. 과정 목록에 할당 된 학과의 이름을 표시 하려면 `Course.Department` 탐색 속성에 있는 `Department` 엔터티에서 `Name` 속성을 가져와야 합니다.

다음 그림에 나와 있는 것 처럼 `Student` 컨트롤러에 대해 이전에 수행한 것과 동일한 옵션을 사용 하 여 `Course` 엔터티 형식에 대 한 `CourseController` 라는 컨트롤러를 만듭니다. 이미지와는 달리 모델 네임 스페이스가 아닌 DAL 네임 스페이스에 컨텍스트 클래스가 있습니다.

![Add_Controller_dialog_box_for_Course_controller](https://asp.net/media/2577868/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Add_Controller_dialog_box_for_Course_controller_c167c11e-2d3e-4b64-a2b9-a0b368b8041d.png)

*Controllers\CourseController.cs* 를 열고 `Index` 메서드를 확인 합니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

자동 스캐폴딩은 `Include` 메서드를 사용하여 `Department` 탐색 속성에 대해 즉시 로드를 지정했습니다.

*Views\Course\Index.cshtml* 를 열고 기존 코드를 다음 코드로 바꿉니다. 변경 내용이 강조 표시되어 있습니다.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=4,15,18,28-30)]

스캐폴드 코드에 다음 변경 내용을 만들었습니다.

- 머리글을 **인덱스** 에서 **과정**으로 변경 했습니다.
- 행 링크를 왼쪽으로 이동 했습니다.
- `CourseID` 속성 값을 표시 하는 머리글 **번호** 아래에 열을 추가 했습니다. 기본적으로 기본 키는 최종 사용자에 게는 의미가 없기 때문에 스 캐 폴드 되지 않습니다. 그러나이 경우 기본 키는 의미가 있으며 표시 하려고 합니다.
- 마지막 열 머리글이 **DepartmentID** (외래 `Department` 키의 이름)에서 **학과**로 변경 되었습니다.

마지막 열에 대해 스 캐 폴드 코드는 `Department` 탐색 속성에 로드 된 `Department` 엔터티의 `Name` 속성을 표시 합니다.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml)]

페이지를 실행 하 여 (Contoso 대학 홈 페이지에서 **과정** 탭 선택) 부서 이름이 있는 목록을 표시 합니다.

![Courses_index_page_with_department_names](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="create-an-instructors-index-page-that-shows-courses-and-enrollments"></a>강좌 및 등록을 보여 주는 강사 인덱스 페이지 만들기

이 섹션에서는 강사 인덱스 페이지를 표시 하기 위해 `Instructor` 엔터티에 대 한 컨트롤러 및 뷰를 만듭니다.

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

이 페이지는 다음과 같은 방법으로 관련된 데이터를 읽고 표시합니다.

- 강사 목록은 `OfficeAssignment` 엔터티에서 관련 된 데이터를 표시 합니다. `Instructor` 및 `OfficeAssignment` 엔터티는 일대영 또는 일 관계에 있습니다. `OfficeAssignment` 엔터티에 대해 즉시 로드를 사용 합니다. 이전에 설명한 대로 기본 테이블의 검색된 모든 행에 관련된 데이터가 필요한 경우 즉시 로드는 일반적으로 더 효율적입니다. 이 경우 표시된 모든 강사에 대한 사무실 할당을 표시하길 원합니다.
- 사용자가 강사를 선택하면 관련된 `Course` 엔터티가 표시됩니다. `Instructor` 및 `Course` 엔터티는 다대다 관계에 있습니다. `Course` 엔터티 및 관련 `Department` 엔터티에 대해 즉시 로드를 사용 합니다. 이 경우 선택한 강사에 대해서만 강좌가 필요 하므로 지연 로드가 더 효율적일 수 있습니다. 그러나 이 예제에서는 탐색 속성에 있는 엔터티 내에서 탐색 속성에 대한 즉시 로드를 사용하는 방법을 보여 줍니다.
- 사용자가 강좌를 선택 하면 `Enrollments` 엔터티 집합의 관련 데이터가 표시 됩니다. `Course` 및 `Enrollment` 엔터티는 일대다 관계에 있습니다. `Enrollment` 엔터티 및 관련 `Student` 엔터티에 대 한 명시적 로드를 추가 합니다. 지연 로드를 사용 하도록 설정 되어 있지만 명시적 로드를 수행 하는 방법을 보여 주는 명시적 로드는 필요 하지 않습니다.

### <a name="create-a-view-model-for-the-instructor-index-view"></a>강사 인덱스 뷰에 대 한 뷰 모델 만들기

강사 인덱스 페이지에는 세 개의 다른 테이블이 표시 됩니다. 따라서 각각이 테이블 중 하나에 대한 데이터를 보유하는 세 가지 속성을 포함하는 보기 모델을 만듭니다.

*Viewmodels* 폴더에서 *InstructorIndexData.cs* 을 만들고 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

### <a name="adding-a-style-for-selected-rows"></a>선택한 행에 대 한 스타일 추가

선택한 행을 표시 하려면 다른 배경색이 필요 합니다. 이 UI에 대 한 스타일을 제공 하려면 아래와 같이 *Content\site.css*의 `/* info and errors */` 섹션에 다음 강조 표시 된 코드를 추가 합니다.

[!code-css[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.css?highlight=2-5)]

### <a name="creating-the-instructor-controller-and-views"></a>강사 컨트롤러 및 보기 만들기

다음 그림에 표시 된 것 처럼 `InstructorController` 컨트롤러를 만듭니다.

![Add_Controller_dialog_box_for_Instructor_controller](https://asp.net/media/2577909/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Add_Controller_dialog_box_for_Instructor_controller_f99c10aa-1efd-49d6-af1d-b00461616107.png)

*Controllers\InstructorController.cs* 를 열고 `ViewModels` 네임 스페이스에 대 한 `using` 문을 추가 합니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

`Index` 메서드의 스 캐 폴드 코드는 `OfficeAssignment` 탐색 속성에 대해서만 즉시 로드를 지정 합니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

추가 관련 데이터를 로드 하 고 뷰 모델에 배치 하려면 `Index` 메서드를 다음 코드로 바꿉니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

이 메서드는 선택적 경로 데이터 (`id`) 및 선택한 강사와 선택한 과정의 ID 값을 제공 하는 쿼리 문자열 매개 변수 (`courseID`)를 허용 하 고 모든 필요한 데이터를 뷰에 전달 합니다. 매개 변수는 페이지의 **선택** 하이퍼링크에서 제공됩니다.

> [!TIP]
> 
> **경로 데이터**
> 
> 경로 데이터는 모델 바인더가 라우팅 테이블에 지정 된 URL 세그먼트에서 발견 한 데이터입니다. 예를 들어 기본 경로 `controller`, `action`및 `id` 세그먼트를 지정 합니다.
> 
> ```csharp
> routes.MapRoute(  
>  name: "Default",  
>  url: "{controller}/{action}/{id}",  
>  defaults: new { controller = "Home", action = "Index", id = UrlParameter.Optional }  
> );
> ```
> 
> 다음 URL에서 기본 경로는 `Instructor` `controller`, `Index` `action` 및 1을 `id`으로 매핑합니다. 이러한 값은 경로 데이터 값입니다.
> 
> `http://localhost:1230/Instructor/Index/1?courseID=2021`
> 
> "? courseID = 2021"는 쿼리 문자열 값입니다. 모델 바인더는 `id` 쿼리 문자열 값으로 전달 하는 경우에도 작동 합니다.
> 
> `http://localhost:1230/Instructor/Index?id=1&CourseID=2021`
> 
> Url은 Razor 뷰에서 `ActionLink` 문으로 생성 됩니다. 다음 코드에서 `id` 매개 변수는 기본 경로와 일치 하므로 `id` 경로 데이터에 추가 됩니다.
> 
> [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cshtml)]
> 
> 다음 코드에서 `courseID`는 기본 경로에 있는 매개 변수와 일치 하지 않으므로 쿼리 문자열로 추가 됩니다.
> 
> [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cshtml)]

코드는 보기 모델의 인스턴스를 만들고 강사 목록에 배치하여 시작합니다. 코드는 `Instructor.OfficeAssignment` 및 `Instructor.Courses` 탐색 속성에 대 한 즉시 로드를 지정 합니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs?highlight=3-4)]

두 번째 `Include` 메서드는 코스를 로드 하 고 로드 된 각 과정에 대해 `Course.Department` 탐색 속성에 대해 즉시 로드 합니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

앞서 언급 했 듯이 즉시 로드는 필요 하지 않지만 성능을 향상 시키기 위해 수행 됩니다. 뷰에는 항상 `OfficeAssignment` 엔터티가 필요 하므로 동일한 쿼리에서 가져오는 것이 더 효율적입니다. 웹 페이지에서 강사를 선택 하는 경우에는 `Course` 엔터티가 필요 합니다 .이를 제외 하 고는 페이지가 더 자주 표시 되는 경우를 제외 하 고 페이지가 더 자주 표시 되는 경우에만 시간이 지연 로드 보다 좋습니다.

강사 ID를 선택한 경우 선택한 강사는 보기 모델의 강사 목록에서 검색 됩니다. 그런 다음 해당 강사의 `Courses` 탐색 속성에서 `Course` 엔터티를 사용 하 여 뷰 모델의 `Courses` 속성을 로드 합니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

`Where` 메서드는 컬렉션을 반환 하지만이 경우 해당 메서드에 전달 된 조건으로 인해 단일 `Instructor` 엔터티만 반환 됩니다. `Single` 메서드는 컬렉션을 단일 `Instructor` 엔터티로 변환 합니다. 그러면 해당 엔터티의 `Courses` 속성에 액세스할 수 있습니다.

컬렉션에 항목이 하나만 있음을 알고 있는 경우 컬렉션에 대해 [단일](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx) 메서드를 사용 합니다. `Single` 메서드는 전달 된 컬렉션이 비어 있거나 둘 이상의 항목이 있는 경우 예외를 throw 합니다. [SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx)는 컬렉션이 비어 있는 경우 기본값 (이 경우 `null`)을 반환 하는 입니다. 그러나이 경우에는 예외를 발생 시킵니다 (`null` 참조에서 `Courses` 속성을 찾으려고 시도). 예외 메시지는 문제의 원인을 명확 하 게 나타내는 것이 아닙니다. `Single` 메서드를 호출 하는 경우 `Where` 메서드를 별도로 호출 하는 대신 `Where` 조건을 전달할 수도 있습니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

다음 문자열 대신에

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

다음으로 강좌를 선택한 경우 선택한 강좌가 보기 모델의 강좌 목록에서 검색됩니다. 그런 다음 뷰 모델의 `Enrollments` 속성은 해당 과정의 `Enrollments` 탐색 속성의 `Enrollment` 엔터티를 사용 하 여 로드 됩니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

### <a name="modifying-the-instructor-index-view"></a>강사 인덱스 보기 수정

*Views\Instructor\Index.cshtml*에서 기존 코드를 다음 코드로 바꿉니다. 변경 내용이 강조 표시되어 있습니다.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml?highlight=1,4,18,22-27,29,43-48)]

기존 코드에 다음 변경 내용을 만들었습니다.

- 모델 클래스를 `InstructorIndexData`로 변경했습니다.
- 페이지 제목을 **인덱스**에서 **강사**로 변경했습니다.
- 행 링크 열을 왼쪽으로 이동 했습니다.
- **FullName** 열을 제거 했습니다.
- `item.OfficeAssignment`가 null이 아닌 경우에만 `item.OfficeAssignment.Location` 표시 하는 **Office** 열을 추가 했습니다. 이는 일 대 영 또는 일 관계 이므로 관련 `OfficeAssignment` 엔터티가 아닐 수 있습니다. 

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]
- 선택한 강사의 `tr` 요소에 `class="selectedrow"`를 동적으로 추가 하는 코드를 추가 했습니다. 이렇게 하면 이전에 만든 CSS 클래스를 사용 하 여 선택 된 행의 배경색을 설정 합니다. `valign` 특성은 테이블에 다중 행 열을 추가할 때 다음 자습서에서 유용 합니다. 

    [!code-html[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html)]
- 각 행의 다른 링크 바로 앞에 **선택** 레이블이 지정 된 새 `ActionLink`을 추가 하 여 선택한 강사 ID가 `Index` 메서드로 전송 되도록 합니다.

응용 프로그램을 실행 하 고 **강사** 탭을 선택 합니다. 이 페이지에는 관련 된 `OfficeAssignment` 엔터티의 `Location` 속성이 표시 되 고 관련 된 `OfficeAssignment` 엔터티가 없으면 빈 테이블 셀이 표시 됩니다.

![Instructors_index_page_with_nothing_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

*Views\Instructor\Index.cshtml* 파일에서 파일의 끝 부분에 있는 closing `table` 요소 뒤에 다음 강조 표시 된 코드를 추가 합니다. 강사가 선택 된 경우 강사와 관련 된 과정의 목록이 표시 됩니다.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=11-46)]

이 코드는 보기 모델의 `Courses` 속성을 읽어 강좌의 목록을 표시합니다. 또한 `Index` 작업 메서드로 선택한 과정의 ID를 전송 하는 `Select` 하이퍼링크를 제공 합니다.

> [!NOTE]
> *.Css* 파일은 브라우저에 의해 캐시 됩니다. 응용 프로그램을 실행할 때 변경 내용이 표시 되지 않으면 하드 새로 고침을 수행 합니다. CTRL 키를 누른 채 **새로 고침** 단추를 클릭 하거나 Ctrl + F5 키를 누릅니다.

페이지를 실행 하 고 강사를 선택 합니다. 이제 선택된 강사에 할당된 강좌를 표시하는 표가 표시되고 각 강좌에 대해 할당된 부서의 이름이 표시됩니다.

![Instructors_index_page_with_instructor_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

방금 추가한 코드 블록 뒤에 다음 코드를 추가합니다. 해당 강좌가 선택된 경우에 강좌에 등록된 학생의 목록을 표시합니다.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cshtml)]

이 코드는 과정에 등록 된 학생의 목록을 표시 하기 위해 뷰 모델의 `Enrollments` 속성을 읽습니다.

페이지를 실행 하 고 강사를 선택 합니다. 그런 다음, 강좌를 선택하여 등록된 학생 및 해당 등급의 목록을 봅니다.

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

### <a name="adding-explicit-loading"></a>명시적 로드 추가

*InstructorController.cs* 를 열고 `Index` 메서드가 선택한 과정에 대 한 등록 목록을 가져오는 방법을 확인 합니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cs)]

강사 목록을 검색할 때 `Courses` 탐색 속성에 대해 즉시 로드를 지정 하 고 각 과정의 `Department` 속성에 대해 즉시 로드를 지정 했습니다. 그런 다음 뷰 모델에 `Courses` 컬렉션을 배치 하면 이제 해당 컬렉션의 한 엔터티에서 `Enrollments` 탐색 속성에 액세스 하 게 됩니다. `Course.Enrollments` 탐색 속성에 대해 즉시 로드를 지정 하지 않았으므로 지연 로드의 결과로 해당 속성의 데이터가 페이지에 표시 됩니다.

다른 방법으로 코드를 변경 하지 않고 지연 로드를 사용 하지 않도록 설정한 경우 `Enrollments` 속성은 실제로 실제로 보유 한 등록 수에 관계 없이 null이 됩니다. 이 경우 `Enrollments` 속성을 로드 하려면 즉시 로드를 지정 하거나 명시적 로드를 지정 해야 합니다. 즉시 로드를 수행 하는 방법을 이미 살펴보았습니다. 명시적 로드의 예제를 보려면 `Index` 메서드를 다음 코드로 바꿉니다 .이 코드는 `Enrollments` 속성을 명시적으로 로드 합니다. 변경 된 코드는 강조 표시 됩니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample24.cs?highlight=20-27)]

선택한 `Course` 엔터티를 가져온 후 새 코드는 해당 강좌의 `Enrollments` 탐색 속성을 명시적으로 로드 합니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample25.cs)]

그런 다음 각 `Enrollment` 엔터티의 관련 `Student` 엔터티를 명시적으로 로드 합니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample26.cs)]

`Collection` 메서드를 사용 하 여 컬렉션 속성을 로드 하지만 하나의 엔터티만 포함 하는 속성의 경우 `Reference` 메서드를 사용 합니다. 이제 강사 인덱스 페이지를 실행할 수 있으며, 데이터를 검색 하는 방법을 변경 했더라도 페이지에 표시 되는 차이점이 표시 되지 않습니다.

## <a name="summary"></a>요약

이제 세 가지 방법 (lazy, 선행 및 명시적)을 모두 사용 하 여 관련 데이터를 탐색 속성에 로드 했습니다. 다음 자습서에서는 관련된 데이터를 업데이트하는 방법을 설명합니다.

[ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md)에서 다른 Entity Framework 리소스에 대 한 링크를 찾을 수 있습니다.

> [!div class="step-by-step"]
> [이전](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
> [다음](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
