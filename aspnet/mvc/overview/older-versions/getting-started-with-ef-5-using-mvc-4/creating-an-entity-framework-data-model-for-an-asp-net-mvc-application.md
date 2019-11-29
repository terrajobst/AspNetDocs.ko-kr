---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
title: ASP.NET MVC 응용 프로그램에 대 한 Entity Framework 데이터 모델 만들기 (1/10) | Microsoft Docs
author: tdykstra
description: Visual Studio 2013, Entity Framework 6 및 MVC 5에 대 한이 자습서 시리즈의 최신 버전을 사용할 수 있습니다. Contoso 대학 샘플 웹 응용 프로그램을 제거 하는 방법 ...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 4ba029b6-ee7c-4e45-a0e7-b703c37e5d9a
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 8ee5aa22b6b2329b01d41437f30508e28a2288b2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595965"
---
# <a name="creating-an-entity-framework-data-model-for-an-aspnet-mvc-application-1-of-10"></a>ASP.NET MVC 응용 프로그램에 대 한 Entity Framework 데이터 모델 만들기 (1/10)

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> > [!NOTE] 
> > 
> > Visual Studio 2013, Entity Framework 6 및 MVC 5에 대 한 [이 자습서 시리즈의 최신 버전](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) 을 사용할 수 있습니다.
> 
> 
> Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 5 및 Visual Studio 2012을 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다. 샘플 애플리케이션은 가상 Contoso University의 웹 사이트입니다. 학생 입학, 강좌 개설 및 강사 할당과 같은 기능이 있습니다. 이 자습서 시리즈에서는 Contoso 대학 샘플 응용 프로그램을 빌드하는 방법을 설명 합니다. [완성 된 응용 프로그램을 다운로드할](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)수 있습니다.
> 
> ## <a name="code-first"></a>Code First
> 
> Entity Framework에서 데이터를 사용할 수 있는 방법에는 *Database First*, *Model First*및 *Code First*의 세 가지가 있습니다. 이 자습서는 Code First에 대 한 것입니다. 이러한 워크플로의 차이점과 시나리오에 가장 적합 한 지침을 선택 하는 방법에 대 한 자세한 내용은 [Entity Framework 개발 워크플로](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)를 참조 하세요.
> 
> ## <a name="mvc"></a>MVC
> 
> 샘플 응용 프로그램은 [ASP.NET MVC](../../../index.md)를 기반으로 합니다. ASP.NET Web Forms 모델을 사용 하는 것을 선호 하는 경우 [모델 바인딩 및 Web Forms](../../../../web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data.md) 자습서 시리즈 및 [ASP.NET 데이터 액세스 콘텐츠 맵을](../../../../whitepapers/aspnet-data-access-content-map.md)참조 하세요.
> 
> ## <a name="software-versions"></a>소프트웨어 버전
> 
> | **자습서에 표시 됨** | **또한와 함께 작동 합니다.** |
> | --- | --- |
> | Windows 8 | Windows 7 |
> | Visual Studio 2012 | Visual Studio 2012 Express for Web. 이는 VS 2012 또는 VS 2012 Express for Web이 아직 없는 경우 Microsoft Azure SDK에 의해 자동으로 설치 됩니다. Visual Studio 2013 작동 하지만 자습서가 테스트 되지 않았으며 일부 메뉴 선택 및 대화 상자가 다릅니다. Microsoft Azure 배포에는 [VS 2013 버전의 Windows AZURE SDK](https://go.microsoft.com/fwlink/p/?linkid=323510) 가 필요 합니다. |
> | .NET 4.5 | 표시 되는 대부분의 기능은 .NET 4에서 작동 하지만 일부는 그렇지 않습니다. 예를 들어 EF에서 열거형을 지원 하려면 .NET 4.5이 필요 합니다. |
> | Entity Framework 5 |  |
> | [Microsoft Azure SDK 2.1](https://go.microsoft.com/fwlink/p/?linkid=323511) | Microsoft Azure 배포 단계를 건너뛰는 경우 SDK가 필요 하지 않습니다. 새 버전의 SDK가 출시 되 면 링크를 통해 최신 버전이 설치 됩니다. 이 경우 몇 가지 지침을 새로운 UI 및 기능에 맞게 조정 해야 할 수 있습니다. |
> 
> ## <a name="questions"></a>질문
> 
> 자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET Entity Framework 포럼](https://forums.asp.net/1227.aspx), [Entity Framework 및 LINQ to Entities 포럼](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/)또는 [StackOverflow.com](http://stackoverflow.com/)에 게시할 수 있습니다.
> 
> ## <a name="acknowledgments"></a>감사의 글
> 
> 승인에 대 한 시리즈의 마지막 자습서 [및 VB에 대 한 메모를](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#acknowledgments)참조 하세요.
> 
> ## <a name="original-version-of-the-tutorial"></a>자습서의 원래 버전
> 
> 자습서의 원래 버전은 [EF 4.1/MVC 3 e-서적](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#GettingStartedwiththeEntityFramework4.1usingASP.NETMVC)에서 사용할 수 있습니다.

## <a name="the-contoso-university-web-application"></a>Contoso 대학 웹 응용 프로그램

이 자습서에서 빌드하는 애플리케이션은 간단한 대학 웹 사이트입니다.

사용자는 학생, 강좌 및 강사 정보를 보고 업데이트할 수 있습니다. 다음은 만들 몇 가지 화면입니다.

![Students_Index_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image1.png)

![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image2.png)

자습서가 Entity Framework를 사용하는 방법에 주로 초점을 맞출 수 있도록 이 사이트의 UI 스타일은 기본 제공 템플릿에서 생성된 내용에 가깝게 유지되었습니다.

## <a name="prerequisites"></a>Prerequisites

이 자습서의 지침 및 스크린샷은 [Visual studio 2012](https://www.microsoft.com/visualstudio/eng/downloads) 또는 [Visual studio 2012 Express for Web](https://go.microsoft.com/fwlink/?LinkID=275131)을 사용 하는 것으로 가정 합니다. 여기에는 최신 업데이트 및 Azure SDK for .net을 사용 하 여 7 월, 2013로 설치 됩니다. 다음 링크를 사용 하 여이를 모두 가져올 수 있습니다.

[.NET 용 Azure SDK (Visual Studio 2012)](https://go.microsoft.com/fwlink/?LinkId=254364)

Visual Studio가 설치 되어 있는 경우 위의 링크를 누르면 누락 된 구성 요소가 모두 설치 됩니다. Visual Studio가 없는 경우 링크를 누르면 Visual Studio 2012 Express for Web이 설치 됩니다. Visual Studio 2013를 사용할 수 있지만 필요한 절차와 화면 중 일부는 다를 수 있습니다.

## <a name="create-an-mvc-web-application"></a>MVC 웹 응용 프로그램 만들기

Visual Studio를 열고 C# **ASP.NET MVC 4 웹 응용 프로그램** 템플릿을 사용 하 여 "ContosoUniversity" 라는 새 프로젝트를 만듭니다. **.NET Framework 4.5** 를 대상으로 하는지 확인 합니다. ( [`enum` 속성](https://msdn.microsoft.com/data/hh859576.aspx)을 사용 하며, .net 4.5이 필요 합니다.)

![New_project_dialog_box](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image3.png)

**새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **인터넷 응용 프로그램** 템플릿을 선택 합니다.

**Razor** 뷰 엔진을 선택 된 채로 두고 **단위 테스트 프로젝트 만들기** 확인란의 선택을 취소 합니다.

**확인**을 클릭합니다.

![Project_template_options](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image4.png)

## <a name="set-up-the-site-style"></a>사이트 스타일 설정

몇 가지 간단한 변경 내용으로 사이트 메뉴, 레이아웃 및 홈 페이지를 설정합니다.

*Views\Shared\\_Layout*를 열고 파일 내용을 다음 코드로 바꿉니다. 변경 내용은 강조 표시되어 있습니다.

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample1.cshtml?highlight=5,15,25-28,43)]

이 코드로 다음이 변경됩니다.

- "My ASP.NET MVC Application" 및 "your your here" 템플릿 인스턴스를 "Contoso 대학"으로 바꿉니다.
- 자습서의 뒷부분에서 사용할 여러 작업 링크를 추가 합니다.

*Views\Home\Index.cshtml*에서 파일의 내용을 다음 코드로 바꿔서 ASP.NET 및 MVC에 대 한 템플릿 단락을 제거 합니다.

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample2.cshtml)]

*Controllers\ homecontroller.cs*에서 다음 예제와 같이 `Index` 동작 메서드에서 `ViewBag.Message`의 값을 "시작 Contoso 대학!"로 변경 합니다.

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=3)]

CTRL + F5 키를 눌러 사이트를 실행 합니다. 주 메뉴가 표시 된 홈 페이지가 표시 됩니다.

![Contoso_University_home_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image5.png)

## <a name="create-the-data-model"></a>데이터 모델 만들기

다음으로 Contoso University 애플리케이션에 대한 엔터티 클래스를 만듭니다. 다음 세 가지 엔터티로 시작 합니다.

![Class_diagram](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image6.png)

`Student` 및 `Enrollment` 엔터티 간에 일대다 관계가 있으며 `Course` 및 `Enrollment` 엔터티 간에 일대다 관계가 있습니다. 즉, 학생은 개수에 관계 없이 강좌에 등록될 수 있으며 강좌는 등록된 학생이 여러 명일 수 있습니다.

다음 섹션에서 이러한 엔터티 각각에 대한 클래스를 만듭니다.

> [!NOTE]
> 이러한 모든 엔터티 클래스 만들기를 완료 하기 전에 프로젝트를 컴파일하려고 하면 컴파일러 오류가 발생 합니다.

### <a name="the-student-entity"></a>학생 엔터티

![Student_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image7.png)

*모델* 폴더에서 *Student.cs* 을 만들고 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample4.cs)]

`StudentID` 속성은 이 클래스에 해당하는 데이터베이스 테이블의 기본 키 열이 됩니다. 기본적으로 Entity Framework는 이름이 `ID` 또는 *classname* `ID` 인 속성을 기본 키로 해석 합니다.

`Enrollments` 속성은 *탐색 속성*입니다. 탐색 속성은 이 엔터티와 관련된 다른 엔터티를 포함합니다. 이 경우 `Student` 엔터티의 `Enrollments` 속성은 해당 `Student` 엔터티와 관련 된 모든 `Enrollment` 엔터티를 포함 합니다. 즉, 데이터베이스의 지정 된 `Student` 행에 두 개의 관련 된 `Enrollment` 행 (`StudentID` 외래 키 열에 해당 학생의 기본 키 값을 포함 하는 행)이 있는 경우 해당 `Student` 엔터티의 `Enrollments` 탐색 속성은 해당 두 개의 `Enrollment` 엔터티를 포함 합니다.

일반적으로 탐색 속성은 *지연 로드*와 같은 특정 Entity Framework 기능을 활용할 수 있도록 `virtual`로 정의 됩니다. 지연 로드는 나중에이 시리즈 뒷부분의 [관련 데이터 읽기](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) 자습서에서 설명 합니다.

탐색 속성이 여러 엔터티를 포함할 수 있는 경우(다대다 또는 일대다 관계로), 해당 형식은 `ICollection`와 같이 항목이 추가, 삭제 및 업데이트될 수 있는 목록이어야 합니다.

### <a name="the-enrollment-entity"></a>등록 엔터티

![Enrollment_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image8.png)

*Models* 폴더에서*Enrollment.cs*를 만들고 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample5.cs)]

Grade 속성은 [열거형](https://msdn.microsoft.com/data/hh859576.aspx)입니다. `Grade` 형식 선언 뒤에 있는 물음표는 `Grade` 속성이 [nullable](https://msdn.microsoft.com/library/2cf62fcy.aspx)이라는 것을 나타냅니다. 값이 null 인 등급은 0 등급과 다릅니다. null은 등급이 알려져 있지 않거나 아직 할당 되지 않았음을 의미 합니다.

`StudentID` 속성은 외래 키로, 해당 탐색 속성은 `Student`입니다. `Enrollment` 엔터티는 하나의 `Student` 엔터티와 연결되어 있으므로 속성은 단일 `Student` 엔터티만 포함할 수 있습니다(이전에 살펴본 여러 `Enrollment` 엔터티를 포함할 수 있는 `Student.Enrollments` 탐색 속성과 달리).

`CourseID` 속성은 외래 키로, 해당 탐색 속성은 `Course`입니다. `Enrollment` 엔터티는 하나의 `Course` 엔터티와 연결됩니다.

### <a name="the-course-entity"></a>Course 엔터티

![Course_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image9.png)

*모델* 폴더에서 *Course.cs*을 만들고 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample6.cs)]

`Enrollments` 속성은 탐색 속성입니다. `Course` 엔터티는 `Enrollment` 엔터티의 개수와 관련이 있을 수 있습니다.

[[Databasegenerated](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute(v=vs.110).aspx)([DatabaseGeneratedOption](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.95).aspx). None)] 특성을 통해 다음 자습서를 진행 합니다. 기본적으로 이 특성을 통해 생성하는 데이터베이스를 갖는 대신 강좌에 대한 기본 키를 입력할 수 있습니다.

## <a name="create-the-database-context"></a>데이터베이스 컨텍스트 만들기

지정 된 데이터 모델에 대 한 Entity Framework 기능을 조정 하는 주 클래스는 *데이터베이스 컨텍스트* 클래스입니다. 이 클래스는 [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx) 클래스에서 파생 하 여 만듭니다. 코드에서 데이터 모델에 포함되는 엔터티를 지정합니다. 특정 Entity Framework 동작을 사용자 지정할 수도 있습니다. 이 프로젝트에서 클래스 이름은 `SchoolContext`로 지정됩니다.

*DAL* (데이터 액세스 계층의 경우) 이라는 폴더를 만듭니다. 해당 폴더에서 *SchoolContext.cs*이라는 새 클래스 파일을 만들고 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample7.cs)]

이 코드는 각 엔터티 집합에 대해 [dbset](https://msdn.microsoft.com/library/system.data.entity.dbset(v=VS.103).aspx) 속성을 만듭니다. Entity Framework 용어에서 *엔터티 집합* 은 일반적으로 데이터베이스 테이블에 해당 하며 *엔터티* 는 테이블의 행에 해당 합니다.

[Onmodelcreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) 메서드의 `modelBuilder.Conventions.Remove` 문은 테이블 이름이 되지 않도록 방지 합니다. 이 작업을 수행 하지 않은 경우 생성 된 테이블의 이름은 `Students`, `Courses`및 `Enrollments`입니다. 대신 테이블 이름이 `Student`, `Course`및 `Enrollment`됩니다. 개발자는 테이블 이름을 복수화할지 여부에 대해 동의하지 않습니다. 이 자습서에서는 단 수 형태를 사용 하지만 중요 한 점은이 코드 줄을 포함 하거나 생략 하 여 원하는 임의의 양식을 선택할 수 있다는 것입니다.

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

[LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx) 는 요청 시 시작 하 고 사용자 모드에서 실행 되는 SQL Server Express 데이터베이스 엔진의 경량 버전입니다. LocalDB는 데이터베이스를 *.mdf* 파일로 사용할 수 있도록 하는 SQL Server Express의 특수 실행 모드로 실행 됩니다. 일반적으로 LocalDB 데이터베이스 파일은 웹 프로젝트의 *App\_Data* 폴더에 저장 됩니다. SQL Server Express의 사용자 인스턴스 기능을 사용 하면 *.mdf* 파일을 사용할 수도 있지만 사용자 인스턴스 기능은 사용 되지 않습니다. 따라서 *.mdf* 파일을 사용 하는 경우에는 LocalDB를 사용 하는 것이 좋습니다.

일반적으로 SQL Server Express는 프로덕션 웹 응용 프로그램에 사용 되지 않습니다. 특히 LocalDB는 IIS에서 작동 하도록 설계 되지 않았기 때문에 웹 응용 프로그램에서 프로덕션 용도로 사용 하지 않는 것이 좋습니다.

Visual Studio 2012 이상 버전에서 LocalDB는 기본적으로 Visual Studio와 함께 설치 됩니다. Visual Studio 2010 이전 버전에서는 SQL Server Express (LocalDB 제외)가 Visual Studio에서 기본적으로 설치 됩니다. Visual Studio 2010을 사용 하는 경우 수동으로 설치 해야 합니다.

이 자습서에서는 데이터베이스를 *응용 프로그램\_Data* 폴더에 *.mdf* 파일로 저장할 수 있도록 LocalDB를 사용 합니다. 다음 예제와 같이 루트 *web.config* 파일을 열고 `connectionStrings` 컬렉션에 새 연결 문자열을 추가 합니다. 루트 프로젝트 폴더에 있는 web.config *파일을 업데이트 해야 합니다.* 또한 web.config 파일은 업데이트 하지 않아도 되는 *Views* 하위 *폴더에 있습니다* .

[!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample8.xml)]

기본적으로 Entity Framework는 `DbContext` 클래스 (이 프로젝트에 대 한`SchoolContext`)와 같은 이름으로 명명 된 연결 문자열을 찾습니다. 추가한 연결 문자열은 *App\_Data* 폴더에 있는 *ContosoUniversity* 라는 LocalDB 데이터베이스를 지정 합니다. 자세한 내용은 [SQL Server ASP.NET 웹 응용 프로그램에 대 한 연결 문자열](https://msdn.microsoft.com/library/jj653752.aspx)을 참조 하세요.

실제로는 연결 문자열을 지정할 필요가 없습니다. 연결 문자열을 제공 하지 않을 경우 Entity Framework는 연결 문자열을 하나씩 만듭니다. 그러나 응용 프로그램의 *app\_data* 폴더에 데이터베이스가 없을 수 있습니다. 데이터베이스가 생성 되는 위치에 대 한 자세한 내용은 [새 데이터베이스에 Code First를](https://msdn.microsoft.com/data/jj193542)참조 하세요.

`connectionStrings` 컬렉션에는 멤버 자격 데이터베이스에 사용 되는 `DefaultConnection` 라는 연결 문자열도 있습니다. 이 자습서에서는 멤버 자격 데이터베이스를 사용 하지 않습니다. 두 연결 문자열 간의 유일한 차이점은 데이터베이스 이름과 name 특성 값입니다.

## <a name="set-up-and-execute-a-code-first-migration"></a>Code First 마이그레이션 설정 및 실행

처음으로 응용 프로그램 개발을 시작 하면 데이터 모델이 자주 변경 되며 모델이 변경 될 때마다 데이터베이스와 동기화 되지 않습니다. 데이터 모델을 변경할 때마다 데이터베이스를 자동으로 삭제 하 고 다시 만들기 위해 Entity Framework를 구성할 수 있습니다. 이는 테스트 데이터를 쉽게 다시 만들 수 있기 때문에 개발 초기에는 문제가 되지 않지만 프로덕션에 배포 된 후에는 일반적으로 데이터베이스를 삭제 하지 않고 데이터베이스 스키마를 업데이트 하려고 합니다. 마이그레이션 기능을 사용 하면 Code First는 데이터베이스를 삭제 하 고 다시 만들지 않고 데이터베이스를 업데이트할 수 있습니다. 새 프로젝트의 개발 주기 초반에는 [Dropcreatedatabaseifmodelchanges](https://msdn.microsoft.com/library/gg679604(v=vs.103).aspx) 를 사용 하 여 모델이 변경 될 때마다 데이터베이스를 삭제 하 고 다시 만든 다음 다시 초기값을 설정할 수 있습니다. 응용 프로그램을 배포할 준비가 되 면 마이그레이션 방법으로 변환할 수 있습니다. 이 자습서에서는 마이그레이션을 사용 합니다. 자세한 내용은 [Code First 마이그레이션](https://msdn.microsoft.com/data/jj591621) 및 [마이그레이션 동영상 가이드 시리즈](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx)를 참조 하세요.

### <a name="enable-code-first-migrations"></a>Code First 마이그레이션 사용

1. **도구** 메뉴에서 **NuGet 패키지 관리자** , **패키지 관리자 콘솔**을 차례로 클릭 합니다.

    ![Selecting_Package_Manager_Console](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image10.png)
2. `PM>` 프롬프트에서 다음 명령을 입력 합니다.

    [!code-powershell[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample9.ps1)]

    ![사용-마이그레이션 명령](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image11.png)

    이 명령은 ContosoUniversity 프로젝트에 *마이그레이션* 폴더를 만들고 해당 폴더에 *Configuration.cs* 파일을 저장 합니다 .이 파일을 편집 하 여 마이그레이션을 구성할 수 있습니다.

    ![마이그레이션 폴더](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image12.png)

    `Configuration` 클래스에는 데이터베이스를 만들 때와 데이터 모델이 변경 된 후 업데이트 될 때마다 호출 되는 `Seed` 메서드가 포함 되어 있습니다.

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

    이 `Seed` 방법은 Code First 만든 후 테스트 데이터를 데이터베이스에 삽입 하거나 업데이트 하는 데 사용 됩니다.

### <a name="set-up-the-seed-method"></a>초기값 설정

[시드](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) 메서드는 Code First 마이그레이션 데이터베이스를 만들 때와 데이터베이스를 최신 마이그레이션으로 업데이트할 때마다 실행 됩니다. 초기값 방법의 목적은 응용 프로그램이 데이터베이스에 처음으로 액세스 하기 전에 데이터를 테이블에 삽입할 수 있도록 하는 것입니다.

이전 버전의 Code First에서는 마이그레이션이 해제 되기 전에 테스트 데이터를 삽입 하는 `Seed` 방법이 일반적 이었습니다. 개발 중에 모든 모델이 변경 되 면 데이터베이스를 완전히 삭제 하 고 처음부터 다시 만들어야 하기 때문입니다. Code First 마이그레이션를 사용 하면 데이터베이스 변경 후에 테스트 데이터가 유지 되므로 [시드](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) 메서드에 테스트 데이터를 포함 하는 것은 일반적으로 필요 하지 않습니다. 실제로는 `Seed` 메서드가 프로덕션 환경에서 실행 되므로 마이그레이션을 사용 하 여 데이터베이스를 프로덕션 환경에 배포 하는 경우에는 `Seed` 메서드에서 테스트 데이터를 삽입 하지 않으려고 합니다. 이 경우 `Seed` 메서드가 프로덕션에 삽입 하려는 데이터만 데이터베이스에 삽입 하려고 합니다. 예를 들어 응용 프로그램을 프로덕션 환경에서 사용할 수 있게 되 면 데이터베이스에 `Department` 테이블에 실제 부서 이름이 포함 되도록 할 수 있습니다.

이 자습서에서는 배포에 대해 마이그레이션을 사용 하지만, 많은 데이터를 수동으로 삽입 하지 않고도 응용 프로그램 기능이 작동 하는 방식을 쉽게 확인할 수 있도록 `Seed` 메서드가 테스트 데이터를 삽입 합니다.

1. *Configuration.cs* 파일의 내용을 새 데이터베이스에 테스트 데이터를 로드 하는 다음 코드로 바꿉니다. 

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

    [초기값](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) 메서드는 데이터베이스 컨텍스트 개체를 입력 매개 변수로 사용 하 고 메서드의 코드는 해당 개체를 사용 하 여 데이터베이스에 새 엔터티를 추가 합니다. 각 엔터티 형식에 대해 코드는 새 엔터티 컬렉션을 만들고 적절 한 [Dbset](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) 속성에 추가한 다음 변경 내용을 데이터베이스에 저장 합니다. 여기에서 수행 하는 것 처럼 각 엔터티 그룹 다음에 [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) 메서드를 호출할 필요는 없지만, 이렇게 하면 코드에서 데이터베이스에 쓰는 동안 예외가 발생 하는 경우 문제의 원인을 찾을 수 있습니다.

    데이터를 삽입 하는 문 중 일부는 [Addorupdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 메서드를 사용 하 여 "upsert" 작업을 수행 합니다. `Seed` 메서드는 마이그레이션할 때마다 실행 되기 때문에 데이터를 삽입 하기만 하면 됩니다. 추가 하려는 행은 데이터베이스를 만드는 첫 번째 마이그레이션 후에 이미 있기 때문입니다. "Upsert" 작업은 이미 있는 행을 삽입 하려고 할 때 발생 하는 오류를 방지 하지만 응용 프로그램을 테스트 하는 동안 수행 된 데이터의 변경 내용을 ***재정의*** 합니다. 일부 테이블에서 테스트 데이터를 사용 하는 경우 이러한 상황이 발생 하지 않을 수 있습니다. 테스트 하는 동안 데이터를 변경 하는 경우 데이터베이스 업데이트 후에 변경 내용을 유지 하려는 경우도 있습니다. 조건부 삽입 작업을 수행 하려는 경우: 행이 아직 없는 경우에만 행을 삽입 합니다. 초기값 메서드는 두 가지 방법을 모두 사용 합니다.

    [Addorupdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 메서드에 전달 된 첫 번째 매개 변수는 행이 이미 있는지 여부를 확인 하는 데 사용할 속성을 지정 합니다. 제공 하는 테스트 학생 데이터의 경우 목록의 각 성이 고유 하기 때문에 `LastName` 속성을이 용도로 사용할 수 있습니다.

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

    이 코드에서는 성이 고유한 것으로 가정 합니다. 중복 성이 있는 학생을 수동으로 추가 하는 경우 다음에 마이그레이션을 수행할 때 다음과 같은 예외가 발생 합니다.

    시퀀스에 둘 이상의 요소가 포함 되어 있습니다.

    `AddOrUpdate` 방법에 대 한 자세한 내용은 Julie Lerman의 블로그에서 [EF 4.3 AddOrUpdate 메서드를 사용](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/) 하는 방법을 참조 하세요.

    `Enrollment` 엔터티를 추가 하는 코드는 `AddOrUpdate` 메서드를 사용 하지 않습니다. 엔터티가 이미 있는지 확인 하 고 존재 하지 않는 경우 엔터티를 삽입 합니다. 이 방법은 마이그레이션이 실행 될 때 등록 등급에 대 한 변경 내용을 유지 합니다. 이 코드는 `Enrollment`[목록의](https://msdn.microsoft.com/library/6sh2ey19.aspx) 각 멤버를 반복 하 고, 등록을 데이터베이스에서 찾을 수 없는 경우 데이터베이스에 등록을 추가 합니다. 처음으로 데이터베이스를 업데이트할 때 데이터베이스는 비어 있으므로 각 등록을 추가 합니다.

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

    `Seed` 메서드를 디버깅 하는 방법과 "Alexander Carson" 이라는 두 학생 같은 중복 데이터를 처리 하는 방법에 대 한 자세한 내용은 Rick Anderson의 블로그에서 [EF (시드 및 디버깅 Entity Framework) db](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) 를 참조 하세요.
2. 프로젝트를 빌드합니다.

### <a name="create-and-execute-the-first-migration"></a>첫 번째 마이그레이션 만들기 및 실행

1. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다. 

    [!code-powershell[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample14.ps1)]

    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image13.png)

    `add-migration` 명령은 데이터베이스를 만드는 코드가 포함 된 *[Datestamp]\_InitialCreate.cs* 파일을 마이그레이션 폴더에 추가 합니다. 첫 번째 매개 변수 (`InitialCreate)`는 파일 이름에 사용 되 고 원하는 대로 지정할 수 있습니다. 일반적으로 마이그레이션에서 수행 되는 작업을 요약 하는 단어나 구를 선택 합니다. 예를 들어 AddDepartmentTable&quot;&quot;나중에 마이그레이션하는 이름을로 할 수 있습니다.

    ![초기 마이그레이션을 사용 하는 마이그레이션 폴더](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image14.png)

    `InitialCreate` 클래스의 `Up` 메서드는 데이터 모델 엔터티 집합에 해당 하는 데이터베이스 테이블을 만들고 `Down` 메서드에서 해당 테이블을 삭제 합니다. 마이그레이션에서는 마이그레이션을 위한 데이터 모델 변경을 구현하기 위해 `Up` 메서드를 호출합니다. 업데이트를 롤백하는 명령을 입력하면 마이그레이션에서 `Down` 메서드를 호출합니다. 다음 코드는 `InitialCreate` 파일의 내용을 보여 줍니다.

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample15.cs)]

    `update-database` 명령은 `Up` 메서드를 실행 하 여 데이터베이스를 만든 다음 `Seed` 메서드를 실행 하 여 데이터베이스를 채웁니다.

이제 데이터 모델에 대 한 SQL Server 데이터베이스가 만들어졌습니다. 데이터베이스의 이름은 *ContosoUniversity*이 고 .mdf 파일은 연결 문자열에 지정 된 것 이기 때문에 프로젝트의 *앱\_데이터* 폴더에 *있습니다.*

**서버 탐색기** 또는 **SQL Server 개체 탐색기** (SSOX)를 사용 하 여 Visual Studio에서 데이터베이스를 볼 수 있습니다. 이 자습서에서는 **서버 탐색기**을 사용 합니다. 웹의 Visual Studio Express 2012에서 **서버 탐색기** **데이터베이스 탐색기**이라고 합니다.

1. **보기** 메뉴에서 **서버 탐색기**를 클릭 합니다.
2. **연결 추가** 아이콘을 클릭 합니다.

    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image15.png)
3. **데이터 원본 선택** 대화 상자가 표시 되 면 **Microsoft SQL Server**를 클릭 한 다음 **계속**을 클릭 합니다.  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image16.png)
4. **연결 추가** 대화 상자에서 **서버 이름**으로 **(localdb) \v11.0** 을 입력 합니다. **데이터베이스 이름 선택 또는 입력**에서 ContosoUniversity를 선택 **합니다.**  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image17.png)
5. **확인**을 클릭합니다.
6. **Schoolcontext.cs** 를 확장 한 다음 **테이블**을 확장 합니다.  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image18.png)
7. **학생** 테이블을 마우스 오른쪽 단추로 클릭 하 고 **테이블 데이터 표시** 를 클릭 하 여 생성 된 열과 테이블에 삽입 된 행을 표시 합니다.

    ![학생 테이블](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image19.png)

## <a name="creating-a-student-controller-and-views"></a>학생 컨트롤러 및 뷰 만들기

다음 단계는 이러한 테이블 중 하나를 사용할 수 있는 ASP.NET MVC 컨트롤러 및 뷰를 응용 프로그램에 만드는 것입니다.

1. `Student` 컨트롤러를 만들려면 **솔루션 탐색기**의 **컨트롤러** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 선택한 후 **컨트롤러**를 클릭 합니다. **컨트롤러 추가** 대화 상자에서 다음 항목을 선택 하 고 **추가**를 클릭 합니다. 

   - 컨트롤러 이름: **StudentController**.
   - Template: **Entity Framework을 사용 하 여 읽기/쓰기 동작 및 뷰가 포함 된 MVC 컨트롤러**입니다.
   - 모델 클래스: **Student (ContosoUniversity)** . 드롭다운 목록에서이 옵션이 표시 되지 않으면 프로젝트를 빌드하고 다시 시도 합니다.
   - 데이터 컨텍스트 클래스: **schoolcontext.cs (ContosoUniversity)** .
   - 뷰: **Razor (CSHTML)** . 기본값은입니다.

     ![Add_Controller_dialog_box_for_Student_controller](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image20.png)
2. Visual Studio에서 *Controllers\StudentController.cs* 파일을 엽니다. 데이터베이스 컨텍스트 개체를 인스턴스화하는 클래스 변수가 생성 된 것을 볼 수 있습니다.

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample16.cs)]

     `Index` 작업 메서드는 데이터베이스 컨텍스트 인스턴스의 `Students` 속성을 읽어 *학생* 엔터티 집합에서 학생 목록을 가져옵니다.

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample17.cs)]

     *Student\Index.cshtml* 뷰는 테이블에이 목록을 표시 합니다.

     [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample18.cshtml)]
3. Ctrl+F5를 눌러 프로젝트를 실행합니다.

     **학생** 탭을 클릭 하 여 `Seed` 메서드가 삽입 한 테스트 데이터를 확인 합니다.

     ![학생 인덱스 페이지](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image21.png)

## <a name="conventions"></a>표기 규칙

Entity Framework에서 전체 데이터베이스를 만들 수 있도록 하기 위해 작성 해야 하는 코드의 양은 *규칙*의 사용 또는 Entity Framework에 대 한 가정 때문에 최소입니다. 그 중 일부는 이미 명시 되어 있습니다.

- 엔터티 클래스 이름의 복수화 형식은 테이블 이름으로 사용 됩니다.
- 엔터티 속성 이름은 열 이름에 사용됩니다.
- `ID` 또는 *classname* `ID` 라는 엔터티 속성은 기본 키 속성으로 인식 됩니다.

규칙을 재정의할 수 있습니다 (예: 테이블 이름이 복수화 되지 않도록 지정). 규칙 및 규칙을 재정의 하는 방법에 대 한 자세한 내용은이 시리즈의 뒷부분에 있는 [더 복잡 한 데이터 모델 만들기](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md) 자습서에서 확인할 수 있습니다. 자세한 내용은 [Code First 규칙](https://msdn.microsoft.com/data/jj679962)을 참조 하세요.

## <a name="summary"></a>요약

이제 Entity Framework 및 SQL Server Express를 사용 하 여 데이터를 저장 하 고 표시 하는 간단한 응용 프로그램을 만들었습니다. 다음 자습서에서는 기본 CRUD (만들기, 읽기, 업데이트, 삭제) 작업을 수행 하는 방법을 배웁니다. 이 페이지의 맨 아래에 의견을 남길 수 있습니다. 자습서의이 부분과이를 개선할 수 있는 방법을 알려 주세요.

[ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md)에서 다른 Entity Framework 리소스에 대 한 링크를 찾을 수 있습니다.

> [!div class="step-by-step"]
> [다음](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
