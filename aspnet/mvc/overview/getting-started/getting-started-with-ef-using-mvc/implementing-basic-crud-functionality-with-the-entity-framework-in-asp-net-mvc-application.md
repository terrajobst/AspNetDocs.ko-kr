---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
title: '자습서: ASP.NET MVC에서 Entity Framework를 사용 하 여 CRUD 기능 구현 | Microsoft Docs'
description: MVC 스 캐 폴딩이 컨트롤러 및 뷰에서 자동으로 만드는 CRUD (만들기, 읽기, 업데이트, 삭제) 코드를 검토 하 고 사용자 지정 합니다.
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: a2f70ba4-83d1-4002-9255-24732726c4f2
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9ed388543dd54d209ff2a0b92df4f7659962582c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471149"
---
# <a name="tutorial-implement-crud-functionality-with-the-entity-framework-in-aspnet-mvc"></a>자습서: ASP.NET MVC의 Entity Framework를 사용 하 여 CRUD 기능 구현

[이전 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)에서는 EF (Entity Framework) 6 및 SQL Server LocalDB를 사용 하 여 데이터를 저장 하 고 표시 하는 MVC 응용 프로그램을 만들었습니다. 이 자습서에서는 MVC 스 캐 폴딩이 컨트롤러 및 보기에서 자동으로 만드는 CRUD (만들기, 읽기, 업데이트, 삭제) 코드를 검토 하 고 사용자 지정 합니다.

> [!NOTE]
> 컨트롤러와 데이터 액세스 계층 간에 추상화 계층을 만들기 위해 리포지토리 패턴을 구현하는 일반적인 사례입니다. 이러한 자습서를 간단 하 고 사용 하는 방법에 중점을 두고 EF 6 자체를 사용 하는 방법은 리포지토리를 사용 하지 않습니다. 리포지토리를 구현 하는 방법에 대 한 정보는 [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md)을 참조 하십시오.

만든 웹 페이지의 예는 다음과 같습니다.

![학생 정보 페이지의 스크린샷](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image1.png)

![학생 만들기 페이지의 스크린샷](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image2.png)

![학생 삭제 페이지에 있는 스크린샷.](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image3.png)

이 자습서에서는 다음을 수행합니다.

> [!div class="checklist"]
> * 세부 정보 페이지 만들기
> * 만들기 페이지 업데이트
> * HttpPost Edit 메서드를 업데이트 합니다.
> * 삭제 페이지 업데이트
> * 데이터베이스 연결 닫기
> * 트랜잭션 처리

## <a name="prerequisites"></a>사전 요구 사항

* [Entity Framework 데이터 모델 만들기](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)

## <a name="create-a-details-page"></a>세부 정보 페이지 만들기

학생 `Index` 페이지에 대 한 스 캐 폴드 코드는 컬렉션을 포함 하므로 `Enrollments` 속성을 그대로 유지 합니다. `Details` 페이지에서 컬렉션의 내용을 HTML 테이블에 표시 합니다.

*Controllers\StudentController.cs*에서 `Details` 뷰의 동작 메서드는 [Find](https://msdn.microsoft.com/library/gg696418(v=VS.103).aspx) 메서드를 사용 하 여 단일 `Student` 엔터티를 검색 합니다.

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample1.cs)]

키 값은 메서드에 `id` 매개 변수로 전달 되 고 인덱스 페이지의 **세부 정보** 하이퍼링크에 있는 *경로 데이터* 에서 가져옵니다.

### <a name="tip-route-data"></a>팁: **경로 데이터**

경로 데이터는 모델 바인더가 라우팅 테이블에 지정 된 URL 세그먼트에서 발견 한 데이터입니다. 예를 들어 기본 경로 `controller`, `action`및 `id` 세그먼트를 지정 합니다.

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample2.cs?highlight=3)]

다음 URL에서 기본 경로는 `Instructor` `controller`, `Index` `action` 및 1을 `id`으로 매핑합니다. 이러한 값은 경로 데이터 값입니다.

`http://localhost:1230/Instructor/Index/1?courseID=2021`

`?courseID=2021`는 쿼리 문자열 값입니다. 모델 바인더는 `id` 쿼리 문자열 값으로 전달 하는 경우에도 작동 합니다.

`http://localhost:1230/Instructor/Index?id=1&CourseID=2021`

Url은 Razor 뷰에서 `ActionLink` 문으로 생성 됩니다. 다음 코드에서 `id` 매개 변수는 기본 경로와 일치 하므로 `id` 경로 데이터에 추가 됩니다.

[!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample3.cshtml)]

다음 코드에서 `courseID`는 기본 경로에 있는 매개 변수와 일치 하지 않으므로 쿼리 문자열로 추가 됩니다.

[!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample4.cshtml)]

### <a name="to-create-the-details-page"></a>세부 정보 페이지를 만들려면

1. *Views\Student\Details.cshtml*를 엽니다.

   다음 예제와 같이 각 필드는 `DisplayFor` 도우미를 사용 하 여 표시 됩니다.

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample5.cshtml)]

2. `EnrollmentDate` 필드 뒤와 closing `</dl>` 태그 바로 앞에 다음 예제와 같이 강조 표시 된 코드를 추가 하 여 등록 목록을 표시 합니다.

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample6.cshtml?highlight=8-29)]

    코드를 붙여넣은 후 코드 들여쓰기가 잘못 된 경우 **ctrl**+**K**, **ctrl**+**D** 를 눌러 서식을 지정 합니다.

    이 코드는 `Enrollments` 탐색 속성의 엔터티를 통해 반복됩니다. 속성의 각 `Enrollment` 엔터티에 대해 강좌 제목 및 등급을 표시 합니다. 과정 제목은 `Enrollments` 엔터티의 `Course` 탐색 속성에 저장 된 `Course` 엔터티에서 검색 됩니다. 이러한 모든 데이터는 필요할 때 데이터베이스에서 자동으로 검색 됩니다. 즉, 여기서 지연 로드를 사용 합니다. `Courses` 탐색 속성에 대해 *즉시 로드* 를 지정 하지 않았으므로 학습자를 받은 동일한 쿼리에서 등록가 검색 되지 않았습니다. 대신 `Enrollments` 탐색 속성에 처음으로 액세스 하려고 할 때 새 쿼리가 데이터베이스로 전송 되어 데이터를 검색 합니다. 이 시리즈의 뒷부분에 나오는 [관련 데이터 읽기](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) 자습서에서 지연 로드 및 즉시 로드에 대해 자세히 알아볼 수 있습니다.

3. 프로그램을 시작 하 고 (**Ctrl**+**F5**) **학생** 탭을 선택한 다음 Alexander carson에 대 한 **세부 정보** 링크를 클릭 하 여 세부 정보 페이지를 엽니다. ( *자세한 정보. cshtml* 파일이 열려 있는 동안 **Ctrl**+**f5** 키를 누르면 HTTP 400 오류가 발생 합니다. Visual Studio가 세부 정보 페이지를 실행 하려고 하지만 표시할 학생을 지정 하는 링크에서 도달 하지 않았기 때문입니다. 이 경우 URL에서 "Student/Details"를 제거 하 고 다시 시도 하거나, 브라우저를 닫고 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 **브라우저에서** **보기** > 보기를 클릭 합니다.)

    선택한 학생에 대 한 과정 및 등급의 목록이 표시 됩니다.

4. 브라우저를 닫습니다.

## <a name="update-the-create-page"></a>만들기 페이지 업데이트

1. *Controllers\StudentController.cs*에서 <xref:System.Web.Mvc.HttpPostAttribute> `Create` 동작 메서드를 다음 코드로 바꿉니다. 이 코드는 `try-catch` 블록을 추가 하 고 스 캐 폴드 메서드에 대 한 <xref:System.Web.Mvc.BindAttribute> 특성에서 `ID`를 제거 합니다.

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample7.cs?highlight=3,5-6,13-18)]

    이 코드는 ASP.NET MVC 모델 바인더에서 만든 `Student` 엔터티를 `Students` 엔터티 집합에 추가한 다음 변경 내용을 데이터베이스에 저장 합니다. *모델 바인더* 는 폼에서 제출한 데이터를 보다 쉽게 사용할 수 있도록 하는 ASP.NET MVC 기능을 나타냅니다. 모델 바인더는 게시 된 양식 값을 CLR 형식으로 변환 하 고 매개 변수에서 작업 메서드에 전달 합니다. 이 경우 모델 바인더는 `Form` 컬렉션의 속성 값을 사용 하 여 `Student` 엔터티를 인스턴스화합니다.

    `ID`은 행이 삽입 될 때 SQL Server 자동으로 설정 되는 기본 키 값 이므로 Bind 특성에서 `ID` 제거 했습니다. 사용자 입력은 `ID` 값을 설정 하지 않습니다.

    <a id="overpost"></a>

    ### <a name="security-warning---the-validateantiforgerytoken-attribute-helps-prevent-cross-site-request-forgery-attacks-it-requires-a-corresponding-htmlantiforgerytoken-statement-in-the-view-which-youll-see-later"></a>보안 경고-`ValidateAntiForgeryToken` 특성은 [교차 사이트 요청 위조](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) 공격을 방지 하는 데 도움이 됩니다. 뷰에 해당 하는 `Html.AntiForgeryToken()` 문이 필요 하며,이는 나중에 볼 수 있습니다.

    `Bind` 특성은 만들기 시나리오에서 *과도 한 게시* 를 방지 하는 한 가지 방법입니다. 예를 들어 `Student` 엔터티에이 웹 페이지를 설정 하지 않으려는 `Secret` 속성이 포함 되어 있다고 가정 합니다.

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample8.cs?highlight=7)]

    웹 페이지에 `Secret` 필드가 없더라도 해커가 [fiddler](http://fiddler2.com/home)와 같은 도구를 사용 하거나 일부 JavaScript를 작성 하 여 `Secret` 양식 값을 게시할 수 있습니다. `Student` 인스턴스를 만들 때 모델 바인더가 사용 하는 필드를 제한 하는 <xref:System.Web.Mvc.BindAttribute> 특성이 없으면 모델<em>바인더는 해당</em> `Secret` 형식 값을 선택 하 고이를 사용 하 여 `Student` 엔터티 인스턴스를 만듭니다. 그런 다음, 해커가 `Secret` 양식 필드에 대해 지정한 모든 값은 데이터베이스에서 업데이트됩니다. 다음 이미지는 게시 된 폼 값에 `Secret` 필드를 추가 하는 fiddler 도구를 보여 줍니다 (값 "과잉 게시").

    ![](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image5.png)

    값 "OverPost"는 웹 페이지가 속성을 설정할 수 있도록 의도하지 않았지만 삽입된 행의 `Secret` 속성에 성공적으로 추가됩니다.

    `Bind` 특성과 함께 `Include` 매개 변수를 사용 하 여 필드를 *허용 목록* 하는 것이 가장 좋습니다. 또한 `Exclude` 매개 변수를 사용 하 여 제외할 필드를 *블랙 리스트* 에 추가할 수 있습니다. `Include` 하는 것이 더 안전 하기 때문에 엔터티에 새 속성을 추가할 때 새 필드는 `Exclude` 목록에 의해 자동으로 보호 되지 않습니다.

    편집 시나리오에서의 과도 한 게시는 먼저 데이터베이스에서 엔터티를 읽은 다음 `TryUpdateModel`를 호출 하 여 명시적으로 허용 되는 속성 목록을 전달 하는 것입니다. 이는 이러한 자습서에서 사용 되는 방법입니다.

    많은 개발자가 선호 하는 과도 한 게시를 방지 하는 또 다른 방법은 모델 바인딩을 사용 하는 엔터티 클래스 대신 뷰 모델을 사용 하는 것입니다. 보기 모델에서 업데이트하려는 속성만 포함합니다. MVC 모델 바인더가 완료 되 면 필요에 따라 [Automapper](http://automapper.org/)와 같은 도구를 사용 하 여 엔터티 인스턴스에 뷰 모델 속성을 복사 합니다. Db를 사용 합니다. 상태를 변경 되지 않은 상태로 설정할 엔터티 인스턴스의 항목을 입력 한 다음 속성 ("PropertyName")을 설정 합니다. 보기 모델에 포함 된 각 엔터티 속성에 대해 IsModified가 true로 수정 되었습니다. 이 방법은 편집 및 만들기 시나리오에서 모두 작동합니다.

    `Bind` 특성 외에 `try-catch` 블록은 스 캐 폴드 코드에 대해 수행한 유일한 변경 내용입니다. <xref:System.Data.DataException>에서 파생되는 예외가 변경 내용이 저장되는 동안 발견되는 경우 일반 오류 메시지가 표시됩니다. <xref:System.Data.DataException> 예외는 경우에 따라 프로그래밍 오류가 아니라 애플리케이션에 대한 외부적인 문제로 발생하므로 사용자는 다시 시도하는 것이 좋습니다. 이 샘플에서 구현되지 않지만 프로덕션 품질 애플리케이션은 예외를 기록합니다. 자세한 내용은 **모니터링 및 원격 분석(Azure로 실제 클라우드 앱 빌드)** 에서 [정보에 대한 로그](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry.md#log) 섹션을 참조하세요.

    *Views\Student\Create.cshtml* 의 코드는 `DisplayFor`아닌 각 필드에 대해 `EditorFor` 및 `ValidationMessageFor` 도우미가 사용 된다는 점을 제외 하 고는 자세히에서 살펴본 것과 비슷합니다 *.* 관련 코드는 다음과 같습니다.

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample9.cshtml)]

    *Create. cshtml* 에는 [사이트 간 요청 위조](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) 공격을 방지 하기 위해 컨트롤러의 `ValidateAntiForgeryToken` 특성에서 작동 하는 `@Html.AntiForgeryToken()`포함 되어 있습니다.

    *Create. cshtml*에는 변경이 필요 하지 않습니다.

2. 프로그램을 시작 하 고 **학생** 탭을 선택한 다음 **새로 만들기**를 클릭 하 여 페이지를 실행 합니다.

3. 이름 및 잘못 된 날짜를 입력 하 고 **만들기** 를 클릭 하 여 오류 메시지를 표시 합니다.

    이는 기본적으로 가져오는 서버 쪽 유효성 검사입니다. 이후 자습서에서는 클라이언트 쪽 유효성 검사에 대 한 코드를 생성 하는 특성을 추가 하는 방법에 대해 알아봅니다. 다음 강조 표시 된 코드는 **Create** 메서드의 모델 유효성 검사를 보여 줍니다.

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample10.cs?highlight=1)]

4. 유효한 값으로 날짜를 변경하고 **만들기**를 클릭하여 **인덱스** 페이지에 표시되는 새 학생을 봅니다.

5. 브라우저를 닫습니다.

## <a name="update-httppost-edit-method"></a>HttpPost Edit 메서드 업데이트

1. <xref:System.Web.Mvc.HttpPostAttribute> `Edit` 동작 메서드를 다음 코드로 바꿉니다.

   [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample11.cs)]

   > [!NOTE]
   > *Controllers\StudentController.cs*에서 `HttpGet Edit` 메서드 (`HttpPost` 특성이 없는 메서드)는 `Find` 메서드를 사용 하 여 `Details` 메서드에서 본 것 처럼 선택한 `Student` 엔터티를 검색 합니다. 이 메서드를 변경할 필요가 없습니다.

   이러한 변경 내용은 [과도 한 게시](#overpost)를 방지 하는 보안 모범 사례를 구현 합니다. 스 캐 폴더는 `Bind` 특성을 생성 하 고 모델 바인더에서 만든 엔터티를 수정 된 플래그를 사용 하 여 엔터티 집합에 추가 했습니다. `Bind` 특성은 `Include` 매개 변수에 나열 되지 않은 필드의 기존 데이터를 모두 제거 하므로 해당 코드를 더 이상 권장 하지 않습니다. 나중에 편집 메서드에 대 한 `Bind` 특성을 생성 하지 않도록 MVC 컨트롤러 스 캐 폴더 업데이트 됩니다.

   새 코드는 기존 엔터티를 읽고 <xref:System.Web.Mvc.Controller.TryUpdateModel%2A>를 호출 하 여 게시 된 양식 데이터의 사용자 입력에서 필드를 업데이트 합니다. Entity Framework의 자동 변경 내용 추적은 엔터티의 [EntityState](<xref:System.Data.EntityState.Modified>) 플래그를 설정 합니다. [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) 메서드가 호출 되 면 <xref:System.Data.EntityState.Modified> 플래그를 통해 Entity Framework SQL 문을 만들어 데이터베이스 행을 업데이트 합니다. [동시성 충돌](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) 은 무시 되 고 사용자가 변경 하지 않은 데이터베이스를 포함 하 여 데이터베이스 행의 모든 열이 업데이트 됩니다. (이후 자습서에서는 동시성 충돌을 처리 하는 방법을 보여 줍니다. 데이터베이스에서 개별 필드만 업데이트 하려면 엔터티를 [EntityState](<xref:System.Data.EntityState.Unchanged>) 로 설정 하 고 개별 필드를 [EntityState](<xref:System.Data.EntityState.Modified>)로 설정 하면 됩니다.)

   과도 한 게시를 방지 하기 위해 편집 페이지에서 업데이트할 수 있는 필드는 `TryUpdateModel` 매개 변수에 허용 목록 됩니다. 현재 보호하는 추가 필드가 없지만 모델 바인더에서 바인딩하길 원하는 필드를 나열하는 것은 향후에 데이터 모델에 필드를 추가하는지 확인하며, 여기에서 명시적으로 추가할 때까지 자동으로 보호됩니다.

   이러한 변경의 결과로 HttpPost Edit 메서드의 메서드 시그니처는 HttpGet edit 메서드와 동일 합니다. 따라서 메서드 편집 게시의 이름을 바꿨습니다.

   > [!TIP]
   >
   > **엔터티 상태 및 연결 및 SaveChanges 메서드**
   >
   > 데이터베이스 컨텍스트는 메모리의 엔터티가 데이터베이스의 해당 열과 동기화 상태인지 여부의 추적을 유지하고 이 정보는 `SaveChanges` 메서드를 호출할 때 발생하는 작업을 결정합니다. 예를 들어 새 엔터티를 [Add](https://msdn.microsoft.com/library/system.data.entity.dbset.add(v=vs.103).aspx) 메서드에 전달 하는 경우 해당 엔터티의 상태가 `Added`로 설정 됩니다. 그런 다음 [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) 메서드를 호출 하면 데이터베이스 컨텍스트는 SQL `INSERT` 명령을 실행 합니다.
   >
   > 엔터티는 다음 [상태](xref:System.Data.EntityState)중 하나일 수 있습니다.
   >
   > - `Added`입니다. 엔터티가 데이터베이스에 아직 없습니다. `SaveChanges` 메서드는 `INSERT` 문을 실행 해야 합니다.
   > - `Unchanged`입니다. `SaveChanges` 메서드에서 이 엔터티로 아무 작업도 수행할 필요가 없습니다. 데이터베이스에서 엔터티를 읽을 때 엔터티는 이 상태로 시작합니다.
   > - `Modified`입니다. 일부 또는 모든 엔터티의 속성 값이 수정되었습니다. `SaveChanges` 메서드는 `UPDATE` 문을 실행 해야 합니다.
   > - `Deleted`입니다. 엔터티가 삭제되도록 표시되었습니다. `SaveChanges` 메서드는 `DELETE` 문을 실행 해야 합니다.
   > - `Detached`입니다. 엔터티가 데이터베이스 컨텍스트에 의해 추적되지 않습니다.
   >
   > 데스크톱 애플리케이션에서는 일반적으로 상태 변경 내용이 자동으로 설정됩니다. 응용 프로그램의 데스크톱 유형에 서 엔터티를 읽고 일부 속성 값을 변경 합니다. 이렇게 하면 해당 엔터티 상태가 자동으로 `Modified`로 변경됩니다. 그런 다음 `SaveChanges`를 호출 하면 Entity Framework는 변경한 실제 속성만 업데이트 하는 SQL `UPDATE` 문을 생성 합니다.
   >
   > 웹 앱의 연결 되지 않은 특성은이 연속 시퀀스를 허용 하지 않습니다. 엔터티를 읽는 [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx) 는 페이지가 렌더링 된 후 삭제 됩니다. `HttpPost` `Edit` 동작 메서드가 호출 되 면 새 요청이 수행 되 고 [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx)의 새 인스턴스가 있는 것 이므로 엔터티 `Modified.` 상태를 수동으로 설정 해야 합니다. 그러면 `SaveChanges`를 호출할 때 컨텍스트는 변경한 속성을 알 수 없기 때문에 Entity Framework가 데이터베이스 행의 모든 열을 업데이트 합니다.
   >
   > 사용자가 실제로 변경한 필드만 SQL `Update` 문으로 업데이트 하려는 경우에는 `HttpPost` `Edit` 메서드를 호출할 때 사용할 수 있도록 원래 값을 특정 방식 (예: 숨겨진 필드)으로 저장할 수 있습니다. 그런 다음 원래 값을 사용 하 여 `Student` 엔터티를 만들고, 해당 원래 버전의 엔터티를 사용 하 여 `Attach` 메서드를 호출 하 고, 엔터티의 값을 새 값으로 업데이트 한 다음 `SaveChanges.`를 호출할 수 있습니다. 자세한 내용은 [엔터티 상태 및 SaveChanges](/ef/ef6/saving/change-tracking/entity-state) 및 [로컬 데이터](/ef/ef6/querying/local-data)를 참조 하세요.

   *Views\Student\Edit.cshtml* 의 HTML 및 Razor 코드는 *Create. cshtml*에서 확인 한 것과 비슷하며 변경이 필요 하지 않습니다.

2. 프로그램을 시작 하 고 **학생** 탭을 선택한 다음 **편집** 하이퍼링크를 클릭 하 여 페이지를 실행 합니다.

3. 데이터의 일부를 변경하고 **저장**을 클릭합니다. 인덱스 페이지에 변경 된 데이터가 표시 됩니다.

4. 브라우저를 닫습니다.

## <a name="update-the-delete-page"></a>삭제 페이지 업데이트

*Controllers\StudentController.cs*의 <xref:System.Web.Mvc.HttpGetAttribute> `Delete` 메서드에 대 한 템플릿 코드는 `Details` 및 `Edit` 메서드에서 살펴본 대로 `Find` 메서드를 사용 하 여 선택한 `Student` 엔터티를 검색 합니다. 그러나 `SaveChanges`에 대한 호출이 실패하는 경우 사용자 지정 오류 메시지를 구현하려면 이 메서드 및 해당 보기에 일부 기능을 추가합니다.

업데이트 및 만들기 작업에 대해 본 것과 같이 삭제 작업에는 두 개의 작업 메서드가 필요합니다. GET 요청에 대 한 응답으로 호출 되는 메서드는 사용자에 게 삭제 작업을 승인 하거나 취소할 수 있는 뷰를 표시 합니다. 사용자가 승인하는 경우 POST 요청이 생성됩니다. 이 경우 `HttpPost` `Delete` 메서드가 호출 되 고이 메서드는 실제로 삭제 작업을 수행 합니다.

<xref:System.Web.Mvc.HttpPostAttribute> `Delete` 메서드에 `try-catch` 블록을 추가 하 여 데이터베이스를 업데이트할 때 발생할 수 있는 오류를 처리 합니다. 오류가 발생 하면 <xref:System.Web.Mvc.HttpPostAttribute> `Delete` 메서드가 <xref:System.Web.Mvc.HttpGetAttribute> `Delete` 메서드를 호출 하 여 오류가 발생 했음을 나타내는 매개 변수를 전달 합니다. 그런 다음 <xref:System.Web.Mvc.HttpGetAttribute> `Delete` 메서드는 오류 메시지와 함께 확인 페이지를 다시 지정 하 여 사용자에 게 취소 하거나 다시 시도할 수 있는 기회를 제공 합니다.

1. <xref:System.Web.Mvc.HttpGetAttribute> `Delete` 작업 메서드를 오류 보고를 관리 하는 다음 코드로 바꿉니다.

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample12.cs?highlight=1,7-10)]

    이 코드는 변경 내용을 저장 하는 데 실패 한 후 메서드가 호출 되었는지 여부를 나타내는 [선택적 매개 변수](https://msdn.microsoft.com/library/dd264739.aspx) 를 허용 합니다. 이 매개 변수는 이전 오류 없이 `HttpGet` `Delete` 메서드를 호출 하는 경우에 `false` 됩니다. 데이터베이스 업데이트 오류에 대 한 응답으로 `HttpPost` `Delete` 메서드에서 호출 하는 경우 매개 변수가 `true` 되 고 오류 메시지가 뷰에 전달 됩니다.

2. <xref:System.Web.Mvc.HttpPostAttribute> `Delete` 작업 메서드 (이름이 `DeleteConfirmed`)를 다음 코드로 바꿉니다 .이 코드는 실제 삭제 작업을 수행 하 고 모든 데이터베이스 업데이트 오류를 catch 합니다.

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample13.cs)]

    이 코드는 선택한 엔터티를 검색 한 다음 [Remove](https://msdn.microsoft.com/library/system.data.entity.dbset.remove(v=vs.103).aspx) 메서드를 호출 하 여 엔터티의 상태를 `Deleted`설정 합니다. `SaveChanges`를 호출 하면 SQL `DELETE` 명령이 생성 됩니다. 또한 `DeleteConfirmed`에서 `Delete`로 작업 메서드 이름을 변경했습니다. `HttpPost` `Delete` 메서드 라는 스 캐 폴드 코드는 `HttpPost` 메서드에 고유한 서명을 제공 `DeleteConfirmed`. CLR에는 오버 로드 된 메서드가 다른 메서드 매개 변수를 포함 해야 합니다. 이제 서명이 고유 하므로 MVC 규칙을 사용 하 고 `HttpPost`에 동일한 이름을 사용 하 고 delete 메서드를 `HttpGet` 수 있습니다.

    고용량 응용 프로그램의 성능 향상이 우선 순위가 면 `Find`를 호출 하는 코드 줄을 바꾸고 `Remove` 메서드를 다음 코드로 바꿔서 불필요 한 SQL 쿼리가 행을 검색 하는 것을 방지할 수 있습니다.

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample14.cs)]

    이 코드는 기본 키 값만 사용 하 여 `Student` 엔터티를 인스턴스화한 다음 엔터티 상태를 `Deleted`로 설정 합니다. Entity Framework에서 엔터티를 삭제하기 위해 필요한 모든 것입니다.

    앞서 설명한 것 처럼 `HttpGet` `Delete` 메서드는 데이터를 삭제 하지 않습니다. GET 요청에 대 한 응답으로 삭제 작업을 수행 하는 경우 (또는 편집 작업 수행, 만들기 작업 또는 데이터를 변경 하는 다른 작업을 수행 하는 경우) 보안 위험이 발생 합니다. 자세한 내용은 [ASP.NET MVC Tip #46-Stephen Walther의 블로그에서 보안 허점을 만들기 때문에 Delete 링크를 사용 하지 마세요](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx) .

3. *Views\Student\Delete.cshtml*에서 다음 예제와 같이 `h2` 머리글과 `h3` 제목 사이에 오류 메시지를 추가 합니다.

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample15.cshtml?highlight=2)]

4. 프로그램을 시작 하 고, **학생** 탭을 선택 하 고, **삭제** 하이퍼링크를 클릭 하 여 페이지를 실행 합니다.

5. 페이지에서 **삭제** 를 선택 하 시겠습니까 **?** 라는 메시지가 표시 되 면 삭제를 선택 합니다.

    삭제 된 학생이 없으면 인덱스 페이지가 표시 됩니다. ( [동시성 자습서](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)의 작업에서 오류 처리 코드의 예제를 확인할 수 있습니다.)

## <a name="close-database-connections"></a>데이터베이스 연결 닫기

데이터베이스 연결을 닫고 최대한 빨리 보유 하 고 있는 리소스를 확보 하려면 작업을 완료할 때 컨텍스트 인스턴스를 삭제 합니다. 따라서 스 캐 폴드 코드는 다음 예제와 같이 *StudentController.cs*의 `StudentController` 클래스 끝에 [Dispose](https://msdn.microsoft.com/library/system.idisposable.dispose(v=vs.110).aspx) 메서드를 제공 합니다.

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample16.cs)]

기본 `Controller` 클래스는 이미 `IDisposable` 인터페이스를 구현 하므로이 코드는 `Dispose(bool)` 메서드에 재정의를 추가 하 여 컨텍스트 인스턴스를 명시적으로 삭제 합니다.

## <a name="handle-transactions"></a>트랜잭션 처리

기본적으로 Entity Framework는 트랜잭션을 암시적으로 구현합니다. 여러 행 또는 테이블을 변경한 다음 `SaveChanges`를 호출 하는 시나리오에서 Entity Framework는 모든 변경 내용이 성공 하거나 모두 실패 하도록 자동으로 설정 합니다. 일부 변경 내용이 먼저 완료된 다음, 오류가 발생하는 경우 해당 변경 내용이 자동으로 롤백됩니다. 예를 들어&mdash;더 많은 제어가 필요한 시나리오의 경우 트랜잭션에서 Entity Framework 외부에서 수행 되는 작업을 포함 하려는 경우 트랜잭션 [작업](/ef/ef6/saving/transactions)을 참조&mdash;.

## <a name="get-the-code"></a>코드 가져오기

[완료 된 프로젝트 다운로드](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>추가 리소스

이제 `Student` 엔터티에 대 한 간단한 CRUD 작업을 수행 하는 전체 페이지 집합이 있습니다. MVC 도우미를 사용 하 여 데이터 필드에 대 한 UI 요소를 생성 했습니다. MVC 도우미에 대 한 자세한 내용은 [HTML 도우미를 사용 하 여 폼 렌더링](/previous-versions/aspnet/dd410596(v=vs.98)) (문서는 mvc 3에 대 한 것 이지만 여전히 mvc 5와 관련 됨)을 참조 하세요.

다른 EF 6 리소스에 대 한 링크는 [ASP.NET Data Access-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)에서 찾을 수 있습니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음을 수행합니다.

> [!div class="checklist"]
> * 세부 정보 페이지를 만듦
> * 만들기 페이지 업데이트
> * HttpPost Edit 메서드를 업데이트 했습니다.
> * 삭제 페이지 업데이트
> * 데이터베이스 연결 닫기
> * 처리 한 트랜잭션

다음 문서로 이동 하 여 프로젝트에 정렬, 필터링 및 페이징을 추가 하는 방법에 대해 알아보세요.
> [!div class="nextstepaction"]
> [정렬, 필터링 및 페이징](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
