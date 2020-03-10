---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
title: '자습서: MVC 5를 사용 하 여 Entity Framework 6 Code First 시작 | Microsoft Docs'
description: 이 일련의 자습서에서는 데이터 액세스에 Entity Framework 6을 사용 하는 ASP.NET MVC 5 응용 프로그램을 빌드하는 방법에 대해 알아봅니다.
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: 00bc8b51-32ed-4fd3-9745-be4c2a9c1eaf
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: a00a5a3aa295c2584b90abbf931c258c9e1b58ca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499409"
---
# <a name="tutorial-get-started-with-entity-framework-6-code-first-using-mvc-5"></a>자습서: MVC 5를 사용 하 여 Entity Framework 6 Code First 시작 하기

> [!NOTE]
> 새 개발을 위해 ASP.NET MVC 컨트롤러 및 뷰를 [Razor Pages ASP.NET Core](/aspnet/core/razor-pages) 하는 것이 좋습니다. Razor Pages 사용 하는 것과 비슷한 자습서 시리즈는 [자습서: ASP.NET Core에서 Razor Pages 시작](/aspnet/core/tutorials/razor-pages/razor-pages-start)을 참조 하세요. 새 자습서:
> * 자습서 내용을 좀 더 쉽게 진행할 수 있습니다.
> * 더 많은 EF Core 모범 사례를 제공합니다.
> * 더 효율적인 쿼리를 사용합니다.
> * 최신 API가 탑재되어 최신 상태입니다.
> * 더 많은 기능을 다룹니다.
> * 새 애플리케이션 개발을 위해 선호되는 방법입니다.

이 일련의 자습서에서는 데이터 액세스에 Entity Framework 6을 사용 하는 ASP.NET MVC 5 응용 프로그램을 빌드하는 방법에 대해 알아봅니다. 이 자습서에서는 Code First 워크플로를 사용 합니다. Code First, Database First 및 Model First 중 하나를 선택 하는 방법에 대 한 자세한 내용은 [모델 만들기](/ef/ef6/modeling/)를 참조 하세요.

이 자습서 시리즈에서는 Contoso 대학 샘플 응용 프로그램을 빌드하는 방법을 설명 합니다. 샘플 응용 프로그램은 간단한 대학 웹 사이트입니다. 이를 통해 학생, 강좌 및 강사 정보를 보고 업데이트할 수 있습니다. 다음은 사용자가 만드는 화면 중 두 가지입니다.

![Students_Index_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image1.png)

![학생 편집](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image2.png)

이 자습서에서는 다음을 수행합니다.

> [!div class="checklist"]
> * MVC 웹 앱 만들기
> * 사이트 스타일 설정
> * Entity Framework 6 설치
> * 데이터 모델 만들기
> * 데이터베이스 컨텍스트 만들기
> * 테스트 데이터로 DB 초기화
> * LocalDB를 사용 하도록 EF 6 설정
> * 컨트롤러 및 뷰 만들기
> * 데이터베이스 보기

## <a name="prerequisites"></a>사전 요구 사항

* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)

## <a name="create-an-mvc-web-app"></a>MVC 웹 앱 만들기

1. C# **ASP.NET 웹 응용 프로그램 (.NET Framework)** 템플릿을 사용 하 여 Visual Studio를 열고 웹 프로젝트를 만듭니다. 프로젝트 이름을 *ContosoUniversity* 로 선택 하 고 **확인을**선택 합니다.

   ![Visual Studio의 새 프로젝트 대화 상자](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/new-project-dialog.png)

1. **New ASP.NET 웹 응용 프로그램-ContosoUniversity**에서 **MVC**를 선택 합니다.

   ![Visual Studio의 새 웹 앱 대화 상자](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/new-web-app-dialog.png)

    > [!NOTE]
    > 기본적으로 **인증** 옵션은 **인증 안 함**으로 설정 됩니다. 이 자습서에서 웹 앱은 사용자가 로그인 할 필요가 없습니다. 또한 로그인 한 사용자에 따라 액세스를 제한 하지 않습니다.

1. **확인**을 선택하여 프로젝트를 만듭니다.

## <a name="set-up-the-site-style"></a>사이트 스타일 설정

몇 가지 간단한 변경 내용으로 사이트 메뉴, 레이아웃 및 홈 페이지를 설정합니다.

1. *Views\Shared\\_Layout*를 열고 다음과 같이 변경 합니다.

   - "My ASP.NET Application" 및 "Application name"의 각 항목을 "Contoso 대학"으로 변경 합니다.
   - 학생, 강의, 강사 및 부서에 대 한 메뉴 항목을 추가 하 고 연락처 항목을 삭제 합니다.

   다음 코드 조각에서 변경 내용이 강조 표시 됩니다.

   [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample1.cshtml?highlight=6,19,24-27,38)]

2. *Views\Home\Index.cshtml*에서 파일의 내용을 다음 코드로 바꾸어 ASP.NET 및 MVC에 대 한 텍스트를이 응용 프로그램에 대 한 텍스트로 바꿉니다.

   [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample2.cshtml)]

3. Ctrl + F5 키를 눌러 웹 사이트를 실행 합니다. 주 메뉴가 표시 된 홈 페이지가 표시 됩니다.

## <a name="install-entity-framework-6"></a>Entity Framework 6 설치

1. **도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다.

2. **패키지 관리자 콘솔** 창에서 다음 명령을 입력합니다.

   ```text
   Install-Package EntityFramework
   ```

이 단계는이 자습서에서 수동으로 수행 하는 몇 가지 단계 중 하나 이지만 ASP.NET MVC 스 캐 폴딩 기능을 통해 자동으로 수행 될 수 있습니다. EF (Entity Framework)를 사용 하는 데 필요한 단계를 확인할 수 있도록 수동으로 수행 하 고 있습니다. 나중에 스 캐 폴딩을 사용 하 여 MVC 컨트롤러 및 뷰를 만듭니다. 대안은 자동으로 EF NuGet 패키지를 설치 하 고, 데이터베이스 컨텍스트 클래스를 만들고, 연결 문자열을 만들 수 있도록 하는 것입니다. 이러한 방식으로 수행할 준비가 되 면 이러한 단계를 건너뛰고 엔터티 클래스를 만든 후 MVC 컨트롤러를 스 캐 폴드 합니다.

## <a name="create-the-data-model"></a>데이터 모델 만들기

다음으로 Contoso University 애플리케이션에 대한 엔터티 클래스를 만듭니다. 다음 세 가지 엔터티로 시작 합니다.

**강좌** <-> **등록** <-> **학생**

| 엔터티 | 관계 |
| -------- | ------------ |
| 등록 과정 | 일대다 |
| 등록할 학생 | 일대다 |

`Student` 및 `Enrollment` 엔터티 간에 일대다 관계가 있으며 `Course` 및 `Enrollment` 엔터티 간에 일대다 관계가 있습니다. 즉, 학생은 개수에 관계 없이 강좌에 등록될 수 있으며 강좌는 등록된 학생이 여러 명일 수 있습니다.

다음 섹션에서는 이러한 엔터티 중 하나에 대 한 클래스를 만듭니다.

> [!NOTE]
> 이러한 모든 엔터티 클래스 만들기를 완료 하기 전에 프로젝트를 컴파일하려고 하면 컴파일러 오류가 발생 합니다.

### <a name="the-student-entity"></a>학생 엔터티

- *모델* 폴더에서 **솔루션 탐색기** 의 폴더를 마우스 오른쪽 단추로 클릭 하 고 > **클래스** **추가** 를 선택 하 여 *Student.cs* 라는 클래스 파일을 만듭니다. 템플릿 코드를 다음 코드로 바꿉니다.

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample3.cs)]

`ID` 속성은 이 클래스에 해당하는 데이터베이스 테이블의 기본 키 열이 됩니다. 기본적으로 Entity Framework는 이름이 `ID` 또는 *classname* `ID` 인 속성을 기본 키로 해석 합니다.

`Enrollments` 속성은 *탐색 속성*입니다. 탐색 속성은 이 엔터티와 관련된 다른 엔터티를 포함합니다. 이 경우 `Student` 엔터티의 `Enrollments` 속성은 해당 `Student` 엔터티와 관련 된 모든 `Enrollment` 엔터티를 포함 합니다. 즉, 데이터베이스의 지정 된 `Student` 행에 두 개의 관련 된 `Enrollment` 행 (`StudentID` 외래 키 열에 해당 학생의 기본 키 값을 포함 하는 행)이 있는 경우 해당 `Student` 엔터티의 `Enrollments` 탐색 속성은 해당 두 개의 `Enrollment` 엔터티를 포함 합니다.

일반적으로 탐색 속성은 *지연 로드*와 같은 특정 Entity Framework 기능을 활용할 수 있도록 `virtual`로 정의 됩니다. 지연 로드는 나중에이 시리즈 뒷부분에 나오는 [관련 데이터 읽기](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) 자습서에서 설명 합니다.

탐색 속성이 여러 엔터티를 포함할 수 있는 경우(다대다 또는 일대다 관계로), 해당 형식은 `ICollection`와 같이 항목이 추가, 삭제 및 업데이트될 수 있는 목록이어야 합니다.

### <a name="the-enrollment-entity"></a>등록 엔터티

- *Models* 폴더에서*Enrollment.cs*를 만들고 기존 코드를 다음 코드로 바꿉니다.

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample4.cs)]

`EnrollmentID` 속성은 기본 키가 됩니다. 이 엔터티는 `Student` 엔터티에서 확인 한 대로 `ID` 대신 *classname* `ID` 패턴을 사용 합니다. 일반적으로 하나의 패턴을 선택하고 이를 데이터 모델 전체에서 사용합니다. 여기에서 변형은 패턴 중 하나를 사용할 수 있음을 보여 줍니다. 이후 자습서에서는 `classname` 없이 `ID`를 사용 하 여 데이터 모델에서 상속을 보다 쉽게 구현할 수 있도록 하는 방법을 알아봅니다.

`Grade` 속성은 [열거형](/ef/ef6/modeling/code-first/data-types/enums)입니다. `Grade` 형식 선언 뒤에 있는 물음표는 `Grade` 속성이 [nullable](/dotnet/csharp/programming-guide/nullable-types/using-nullable-types)이라는 것을 나타냅니다. 값이 null 인 등급은 0 등급과 다릅니다. null은 등급이 알려져 있지 않거나 아직 할당 되지 않았음을 의미 합니다.

`StudentID` 속성은 외래 키로, 해당 탐색 속성은 `Student`입니다. `Enrollment` 엔터티는 하나의 `Student` 엔터티와 연결되어 있으므로 속성은 단일 `Student` 엔터티만 포함할 수 있습니다(이전에 살펴본 여러 `Student.Enrollments` 엔터티를 포함할 수 있는 `Enrollment` 탐색 속성과 달리).

`CourseID` 속성은 외래 키로, 해당 탐색 속성은 `Course`입니다. `Enrollment` 엔터티는 하나의 `Course` 엔터티와 연결됩니다.

속성을 외래 키 속성으로 해석 하는 Entity Framework *&lt;탐색 속성 이름&gt;&lt;기본 키 속성 이름&gt;* (예: `StudentID` 엔터티의 기본 키가 `Student` 되기 때문에 `Student` 탐색 속성의 `ID`). 외래 키 속성의 이름은 단순히 *&lt;기본 키 속성 이름&gt;* (예: `Course` 엔터티의 기본 키가 `CourseID`되기 때문에 `CourseID`)으로도 지정할 수 있습니다.

### <a name="the-course-entity"></a>강좌 엔터티

- *모델* 폴더에서 *Course.cs*을 만들고 템플릿 코드를 다음 코드로 바꿉니다.

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample5.cs)]

`Enrollments` 속성은 탐색 속성입니다. `Course` 엔터티는 `Enrollment` 엔터티의 개수와 관련이 있을 수 있습니다.

이 시리즈의 이후 자습서에서는 <xref:System.ComponentModel.DataAnnotations.Schema.DatabaseGeneratedAttribute> 특성에 대해 자세히 설명 합니다. 기본적으로 이 특성을 통해 생성하는 데이터베이스를 갖는 대신 강좌에 대한 기본 키를 입력할 수 있습니다.

## <a name="create-the-database-context"></a>데이터베이스 컨텍스트 만들기

지정 된 데이터 모델에 대 한 Entity Framework 기능을 조정 하는 주 클래스는 *데이터베이스 컨텍스트* 클래스입니다. 이 클래스는 [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.113).aspx) 클래스에서 파생 하 여 만듭니다. 코드에서 데이터 모델에 포함 되는 엔터티를 지정 합니다. 특정 Entity Framework 동작을 사용자 지정할 수도 있습니다. 이 프로젝트에서 클래스 이름은 `SchoolContext`로 지정됩니다.

- ContosoUniversity 프로젝트에서 폴더를 만들려면 **솔루션 탐색기** 에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 클릭 한 다음 **새 폴더**를 클릭 합니다. 새 폴더의 이름을 *DAL* (데이터 액세스 계층의 경우)으로 합니다. 해당 폴더에서 *SchoolContext.cs*이라는 새 클래스 파일을 만들고 템플릿 코드를 다음 코드로 바꿉니다.

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample6.cs)]

### <a name="specify-entity-sets"></a>엔터티 집합 지정

이 코드는 각 엔터티 집합에 대해 [dbset](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.113).aspx) 속성을 만듭니다. Entity Framework 용어에서 *엔터티 집합* 은 일반적으로 데이터베이스 테이블에 해당 하며 *엔터티* 는 테이블의 행에 해당 합니다.

> [!NOTE]
>
> `DbSet<Enrollment>` 및 `DbSet<Course>` 문을 생략할 수 있으며 동일한 작업을 수행 합니다. `Student` 엔터티는 `Enrollment` 엔터티를 참조 하 고 `Enrollment` 엔터티는 `Course` 엔터티를 참조 하기 때문에 Entity Framework은 암시적으로 포함 됩니다.

### <a name="specify-the-connection-string"></a>연결 문자열 지정

나중에 Web.config 파일에 추가 하는 연결 문자열의 이름이 생성자에 전달 됩니다.

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample7.cs?highlight=1)]

Web.config 파일에 저장 된 이름 대신 연결 문자열 자체를 전달할 수도 있습니다. 사용할 데이터베이스를 지정 하는 옵션에 대 한 자세한 내용은 [연결 문자열 및 모델](/ef/ef6/fundamentals/configuring/connection-strings)을 참조 하세요.

연결 문자열 또는 이름을 명시적으로 지정 하지 않으면 Entity Framework 연결 문자열 이름이 클래스 이름과 같다고 가정 합니다. 이 예의 기본 연결 문자열 이름은 명시적으로 지정 하는 것과 같은 `SchoolContext`됩니다.

### <a name="specify-singular-table-names"></a>단일 테이블 이름 지정

[Onmodelcreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) 메서드의 `modelBuilder.Conventions.Remove` 문은 테이블 이름이 되지 않도록 방지 합니다. 이 작업을 수행 하지 않은 경우 데이터베이스에서 생성 된 테이블의 이름은 `Students`, `Courses`및 `Enrollments`입니다. 대신 테이블 이름이 `Student`, `Course`및 `Enrollment`됩니다. 개발자는 테이블 이름을 복수화할지 여부에 대해 동의하지 않습니다. 이 자습서에서는 단 수 형태를 사용 하지만 중요 한 점은이 코드 줄을 포함 하거나 생략 하 여 원하는 임의의 양식을 선택할 수 있다는 것입니다.

## <a name="initialize-db-with-test-data"></a>테스트 데이터로 DB 초기화

응용 프로그램을 실행할 때 자동으로 데이터베이스를 만들거나 삭제 하 고 다시 만들 수 Entity Framework. 응용 프로그램이 실행 될 때마다 또는 모델이 기존 데이터베이스와 동기화 되지 않은 경우에만이 작업이 수행 되도록 지정할 수 있습니다. 또한 데이터베이스를 만든 후에 테스트 데이터로 채우기 위해 자동으로 호출 Entity Framework는 `Seed` 메서드를 작성할 수 있습니다.

기본 동작은 데이터베이스가 없는 경우에만 데이터베이스를 만드는 것이 고, 모델이 변경 되 고 데이터베이스가 이미 있는 경우에는 예외를 throw 하는 것입니다. 이 섹션에서는 모델이 변경 될 때마다 데이터베이스를 삭제 하 고 다시 만들도록 지정 합니다. 데이터베이스를 삭제 하면 모든 데이터가 손실 됩니다. 이는 데이터베이스를 다시 만들고 테스트 데이터를 다시 만들 때 `Seed` 메서드가 실행 되기 때문에 일반적으로 개발 중에 유용 합니다. 그러나 프로덕션 환경에서는 일반적으로 데이터베이스 스키마를 변경 해야 할 때마다 모든 데이터가 손실 되는 것을 원하지 않습니다. 나중에 데이터베이스를 삭제 하 고 다시 만드는 대신 Code First 마이그레이션를 사용 하 여 데이터베이스 스키마를 변경 하는 방법으로 모델 변경을 처리 하는 방법을 확인할 수 있습니다.

1. DAL 폴더에서 *SchoolInitializer.cs* 라는 새 클래스 파일을 만들고 템플릿 코드를 다음 코드로 바꿉니다. 그러면 필요한 경우 데이터베이스가 만들어지고 테스트 데이터를 새 데이터베이스에 로드할 수 있습니다.

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample8.cs)]

   `Seed` 메서드는 데이터베이스 컨텍스트 개체를 입력 매개 변수로 사용 하 고 메서드의 코드는 해당 개체를 사용 하 여 데이터베이스에 새 엔터티를 추가 합니다. 각 엔터티 형식에 대해 코드는 새 엔터티 컬렉션을 만들고 해당 `DbSet` 속성에 추가한 다음 변경 내용을 데이터베이스에 저장 합니다. 각 엔터티 그룹 뒤에 `SaveChanges` 메서드를 호출 하는 것은 필요 하지 않지만,이 작업을 수행 하면 코드에서 데이터베이스에 쓰는 동안 예외가 발생 하는 경우 문제의 원인을 찾을 수 있습니다.

2. 이니셜라이저 클래스를 사용 하도록 Entity Framework를 지시 하려면 다음 예제와 같이 응용 프로그램 *web.config* 파일의 `entityFramework` 요소 (루트 프로젝트 폴더의 파일)에 요소를 추가 합니다.

   [!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample9.xml?highlight=2-6)]

   `context type`는 정규화 된 컨텍스트 클래스 이름과 어셈블리를 지정 하 고, `databaseinitializer type` 이니셜라이저 클래스의 정규화 된 이름과 해당 어셈블리를 지정 합니다. EF를 사용 하지 않으려는 경우 `context` 요소에 대 한 특성을 설정할 수 있습니다. `disableDatabaseInitialization="true"`.) 자세한 내용은 [구성 파일 설정](/ef/ef6/fundamentals/configuring/config-file)을 참조 하세요.

   *Web.config 파일에서* 이니셜라이저를 설정 하는 다른 방법은 *Global.asax.cs* 파일의 `Application_Start` 메서드에 `Database.SetInitializer` 문을 추가 하 여 코드에서 수행 하는 것입니다. 자세한 내용은 [Entity Framework Code First의 데이터베이스 이니셜라이저 이해](http://www.codeguru.com/csharp/article.php/c19999/Understanding-Database-Initializers-in-Entity-Framework-Code-First.htm)를 참조 하세요.

응용 프로그램은 이제 지정 된 응용 Entity Framework 프로그램 실행 시 데이터베이스에 처음으로 액세스 하는 경우 데이터베이스를 모델 (`SchoolContext` 및 엔터티 클래스)과 비교 하도록 설정 됩니다. 차이점이 있으면 응용 프로그램은 데이터베이스를 삭제 하 고 다시 만듭니다.

> [!NOTE]
> 프로덕션 웹 서버에 응용 프로그램을 배포 하는 경우 데이터베이스를 삭제 하 고 다시 만드는 코드를 제거 하거나 사용 하지 않도록 설정 해야 합니다. 이 시리즈의 이후 자습서에서이 작업을 수행 합니다.

## <a name="set-up-ef-6-to-use-localdb"></a>LocalDB를 사용 하도록 EF 6 설정

[LocalDB](/sql/database-engine/configure-windows/sql-server-2016-express-localdb?view=sql-server-2017) 는 SQL Server Express 데이터베이스 엔진의 경량 버전입니다. 설치 및 구성 하 고, 요청 시 시작 하 고, 사용자 모드에서 실행 하는 것이 쉽습니다. LocalDB는 데이터베이스를 *.mdf* 파일로 사용할 수 있도록 하는 SQL Server Express의 특수 실행 모드로 실행 됩니다. 프로젝트를 사용 하 여 데이터베이스를 복사할 수 있도록 하려면 웹 프로젝트의 *App\_Data* 폴더에 LocalDB 데이터베이스 파일을 넣을 수 있습니다. SQL Server Express의 사용자 인스턴스 기능을 사용 하면 *.mdf* 파일을 사용할 수도 있지만 사용자 인스턴스 기능은 사용 되지 않습니다. 따라서 *.mdf* 파일을 사용 하는 경우에는 LocalDB를 사용 하는 것이 좋습니다. LocalDB는 Visual Studio와 함께 기본적으로 설치 됩니다.

일반적으로 SQL Server Express는 프로덕션 웹 응용 프로그램에 사용 되지 않습니다. 특히 LocalDB는 IIS에서 작동 하도록 설계 되지 않았기 때문에 웹 응용 프로그램에서 프로덕션 용도로 사용 하지 않는 것이 좋습니다.

- 이 자습서에서는 LocalDB를 사용 합니다. 다음 예제와 같이 응용 프로그램 *web.config* 파일을 열고 `appSettings` 요소 앞에 `connectionStrings` 요소를 추가 합니다. 루트 프로젝트 폴더에 있는 web.config *파일을 업데이트 해야 합니다.* 업데이트 하지 않아도 되는 *Views* 하위 *폴더에도 web.config 파일이 있습니다* .

   [!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample10.xml?highlight=1-3)]

추가 된 연결 문자열은 Entity Framework에서 *ContosoUniversity1*라는 LocalDB 데이터베이스를 사용 하도록 지정 합니다. (데이터베이스는 아직 존재 하지 않지만 EF에서 만듭니다.) *응용 프로그램\_데이터* 폴더에 데이터베이스를 만들려는 경우 연결 문자열에 `AttachDBFilename=|DataDirectory|\ContosoUniversity1.mdf`를 추가할 수 있습니다. 연결 문자열에 대 한 자세한 내용은 [SQL Server ASP.NET 웹 응용 프로그램에 대 한 연결 문자열](/previous-versions/aspnet/jj653752(v=vs.110))을 참조 하세요.

실제로 *web.config* 파일에는 연결 문자열이 필요 하지 않습니다. 연결 문자열을 제공 하지 않을 경우 Entity Framework는 컨텍스트 클래스에 기반 하 여 기본 연결 문자열을 사용 합니다. 자세한 내용은 [새 데이터베이스에 Code First를](/ef/ef6/modeling/code-first/workflows/new-database)참조 하세요.

## <a name="create-controller-and-views"></a>컨트롤러 및 뷰 만들기

이제 데이터를 표시 하는 웹 페이지를 만듭니다. 데이터를 요청 하는 프로세스는 데이터베이스 생성을 자동으로 트리거합니다. 먼저 새 컨트롤러를 만듭니다. 그러나이 작업을 수행 하기 전에 프로젝트를 빌드하여 MVC 컨트롤러 스 캐 폴딩에서 모델 및 컨텍스트 클래스를 사용할 수 있도록 합니다.

1. **솔루션 탐색기**의 **컨트롤러** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 선택한 다음 **새 스 캐 폴드 항목**을 클릭 합니다.
2. **스 캐 폴드 추가** 대화 상자에서 **MVC 5 컨트롤러 (뷰 포함), Entity Framework 사용**을 선택 하 고 **추가**를 선택 합니다.

     ![Visual Studio에서 스 캐 폴드 대화 상자 추가](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/add-scaffold.png)

3. **컨트롤러 추가** 대화 상자에서 다음 항목을 선택 하 고 **추가**를 선택 합니다.

   - 모델 클래스: **Student (ContosoUniversity)** . 드롭다운 목록에서이 옵션이 표시 되지 않으면 프로젝트를 빌드하고 다시 시도 합니다.
   - 데이터 컨텍스트 클래스: **schoolcontext.cs (ContosoUniversity)** .
   - 컨트롤러 이름: **StudentController** (studentscontroller.cs 아님).
   - 다른 필드의 기본값을 그대로 둡니다.

     **추가**를 클릭 하면 스 캐 폴더는 컨트롤러와 함께 작동 하는 *StudentController.cs* 파일 및 뷰 (*cshtml* 파일) 집합을 만듭니다. 나중에 Entity Framework를 사용 하는 프로젝트를 만들 때 스 캐 폴더의 몇 가지 추가 기능을 활용할 수 있습니다. 첫 번째 모델 클래스를 만들고 연결 문자열을 만든 다음 **컨트롤러 추가** 상자에서 **데이터 컨텍스트 클래스**옆의 **+** 단추를 선택 하 여 **새 데이터 컨텍스트** 를 지정 합니다. 스 캐 폴더는 컨트롤러 및 뷰 뿐만 아니라 `DbContext` 클래스와 연결 문자열을 만듭니다.
4. Visual Studio에서 *Controllers\StudentController.cs* 파일을 엽니다. 데이터베이스 컨텍스트 개체를 인스턴스화하는 클래스 변수가 생성 된 것을 확인할 수 있습니다.

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

     `Index` 작업 메서드는 데이터베이스 컨텍스트 인스턴스의 `Students` 속성을 읽어 *학생* 엔터티 집합에서 학생 목록을 가져옵니다.

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

     *Student\Index.cshtml* 뷰는 테이블에이 목록을 표시 합니다.

     [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample13.cshtml)]
5. Ctrl+F5를 눌러 프로젝트를 실행합니다. "섀도 복사본을 만들 수 없습니다." 오류가 표시 되 면 브라우저를 닫고 다시 시도 합니다.

     **학생** 탭을 클릭 하 여 `Seed` 메서드가 삽입 한 테스트 데이터를 확인 합니다. 브라우저 창의 범위에 따라 위쪽 주소 표시줄에 학생 탭 링크가 표시 됩니다. 링크를 표시 하려면 오른쪽 위 모서리를 클릭 해야 합니다.

     ![메뉴 단추](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image14.png)

## <a name="view-the-database"></a>데이터베이스 보기

학생 페이지를 실행 하 고 응용 프로그램에서 데이터베이스에 액세스 하려고 하면 EF는 데이터베이스가 없는 것을 발견 하 고 하나를 만들었습니다. 그러면 EF가 시드 메서드를 실행 하 여 데이터베이스를 데이터로 채웁니다.

**서버 탐색기** 또는 **SQL Server 개체 탐색기** (SSOX)를 사용 하 여 Visual Studio에서 데이터베이스를 볼 수 있습니다. 이 자습서에서는 **서버 탐색기**을 사용 합니다.

1. 브라우저를 닫습니다.
2. **서버 탐색기**에서 **데이터 연결** (먼저 새로 고침 단추를 선택 해야 할 수 있음)을 확장 하 고 **School Context (ContosoUniversity)** 를 확장 한 다음 **테이블** 을 확장 하 여 새 데이터베이스의 테이블을 확인 합니다.

3. **학생** 테이블을 마우스 오른쪽 단추로 클릭 하 고 **테이블 데이터 표시** 를 클릭 하 여 생성 된 열과 테이블에 삽입 된 행을 표시 합니다.

4. **서버 탐색기** 연결을 닫습니다.

*ContosoUniversity1* 및 *.ldf* 데이터베이스 파일은 *% USERPROFILE%* 폴더에 있습니다.

`DropCreateDatabaseIfModelChanges` 이니셜라이저를 사용 하기 때문에 이제 `Student` 클래스를 변경 하 고, 응용 프로그램을 다시 실행 하 고, 변경 내용과 일치 하도록 데이터베이스를 자동으로 다시 만들 수 있습니다. 예를 들어 `EmailAddress` 속성을 `Student` 클래스에 추가 하 고 학생 페이지를 다시 실행 한 다음 테이블을 다시 살펴보면 새 `EmailAddress` 열이 표시 됩니다.

## <a name="conventions"></a>규칙

Entity Framework 전체 데이터베이스를 만들 수 있도록 하기 위해 작성 해야 하는 코드의 양은 *규칙*또는 Entity Framework에 대 한 가정 때문에 최소입니다. 그 중 일부는 이미 표시 되었거나 사용자가 인식 하지 않고도 사용 되었습니다.

- 엔터티 클래스 이름의 복수화 형식은 테이블 이름으로 사용 됩니다.
- 엔터티 속성 이름은 열 이름에 사용됩니다.
- `ID` 또는 *classname* `ID` 라는 엔터티 속성은 기본 키 속성으로 인식 됩니다.
- 속성은 이름이 *&lt;탐색 속성 이름 &lt;&gt;* 이름이 지정 된 경우 외래 키 속성으로 해석 됩니다. 예를 들어 `StudentID` 엔터티의 기본 키가 `Student` 되기 때문에 `Student` 탐색 속성의 `ID`&gt;. 외래 키 속성의 이름은 단순히 &lt;기본 키 속성 이름&gt; (예: `Enrollment` 엔터티의 기본 키가 `EnrollmentID`되기 때문에 `EnrollmentID`)으로도 지정할 수 있습니다.

규칙을 재정의할 수 있습니다. 예를 들어 테이블 이름을 복수화로 지정 하 고 나중에 속성을 외래 키 속성으로 명시적으로 표시 하는 방법을 확인할 수 있습니다.

## <a name="get-the-code"></a>코드 가져오기

[완료 된 프로젝트 다운로드](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>추가 리소스

EF 6에 대 한 자세한 내용은 다음 문서를 참조 하세요.

* [ASP.NET 데이터 액세스 - 권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)

* [Code First 규칙](/ef/ef6/modeling/code-first/conventions/built-in)

* [좀 더 복잡한 데이터 모델 만들기](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음을 수행합니다.

> [!div class="checklist"]
> * MVC 웹 앱 만들기
> * 사이트 스타일 설정
> * 설치 된 Entity Framework 6
> * 데이터 모델 만들기
> * 데이터베이스 컨텍스트 만들기
> * 테스트 데이터로 DB 초기화
> * LocalDB를 사용 하도록 EF 6 설정
> * 컨트롤러 및 뷰 만들기
> * 데이터베이스 보기

다음 문서로 이동 하 여 컨트롤러 및 보기에서 CRUD (만들기, 읽기, 업데이트, 삭제) 코드를 검토 하 고 사용자 지정 하는 방법을 알아보세요.
> [!div class="nextstepaction"]
> [기본 CRUD 기능 구현](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)