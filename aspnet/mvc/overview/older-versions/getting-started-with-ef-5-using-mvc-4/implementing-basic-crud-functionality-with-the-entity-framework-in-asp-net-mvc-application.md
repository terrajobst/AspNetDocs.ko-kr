---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
title: ASP.NET MVC 응용 프로그램에서 Entity Framework를 사용 하 여 기본 CRUD 기능 구현 (2/10) | Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다.
ms.author: riande
ms.date: 07/30/2013
ms.assetid: f7bace3f-b85a-47ff-b5fe-49e81441cdf9
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: eba146d2975e0dcf243facf7c205c4acfe40b6f6
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595336"
---
# <a name="implementing-basic-crud-functionality-with-the-entity-framework-in-aspnet-mvc-application-2-of-10"></a>ASP.NET MVC 응용 프로그램에서 Entity Framework를 사용 하 여 기본 CRUD 기능 구현 (2/10)

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 5 Code First 및 Visual Studio 2012을 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요. [이 챕터의](building-the-ef5-mvc4-chapter-downloads.md) 시작 또는 시작 프로젝트 다운로드에서 자습서 시리즈를 시작 하 고 여기에서 시작할 수 있습니다.
> 
> > [!NOTE] 
> > 
> > 해결할 수 없는 문제가 발생 하는 경우 [완료 된 챕터를 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 하 여 문제를 재현해 보세요. 일반적으로 코드를 완성 된 코드와 비교 하 여 문제에 대 한 솔루션을 찾을 수 있습니다. 몇 가지 일반적인 오류 및 해결 방법에 대 한 자세한 내용은 [오류 및 해결](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors) 방법을 참조 하세요.

이전 자습서에서는 Entity Framework 및 SQL Server LocalDB를 사용 하 여 데이터를 저장 하 고 표시 하는 MVC 응용 프로그램을 만들었습니다. 이 자습서에서는 MVC 스 캐 폴딩이 컨트롤러 및 보기에서 자동으로 만드는 CRUD (만들기, 읽기, 업데이트, 삭제) 코드를 검토 하 고 사용자 지정 합니다.

> [!NOTE]
> 컨트롤러와 데이터 액세스 계층 간에 추상화 계층을 만들기 위해 리포지토리 패턴을 구현하는 일반적인 사례입니다. 이러한 자습서를 간단 하 게 유지 하기 위해이 시리즈의 이후 자습서 까지는 리포지토리를 구현 하지 않습니다.

이 자습서에서는 다음과 같은 웹 페이지를 만듭니다.

![Student_Details_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image1.png)

![Student_Edit_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image2.png)

![Student_Create_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image3.png)

![Student_delete_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image4.png)

## <a name="creating-a-details-page"></a>세부 정보 페이지 만들기

학생 `Index` 페이지에 대 한 스 캐 폴드 코드는 컬렉션을 포함 하므로 `Enrollments` 속성을 그대로 유지 합니다. `Details` 페이지에서 컬렉션의 내용을 HTML 테이블에 표시 합니다.

 *Controllers\StudentController.cs*에서 `Details` 뷰의 동작 메서드는 `Find` 메서드를 사용 하 여 단일 `Student` 엔터티를 검색 합니다. 

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample1.cs)]

 키 값은 메서드에 `id` 매개 변수로 전달 되 고 인덱스 페이지의 **세부 정보** 하이퍼링크에 있는 경로 데이터에서 가져옵니다. 

1. *Views\Student\Details.cshtml*를 엽니다. 다음 예제와 같이 각 필드는 `DisplayFor` 도우미를 사용 하 여 표시 됩니다. 

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample2.cshtml)]
2. `EnrollmentDate` 필드 뒤와 closing `fieldset` 태그 바로 앞에 다음 예제와 같이 등록 목록을 표시 하는 코드를 추가 합니다.

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample3.cshtml?highlight=4-22)]

    이 코드는 `Enrollments` 탐색 속성의 엔터티를 통해 반복됩니다. 속성의 각 `Enrollment` 엔터티에 대해 강좌 제목 및 등급을 표시 합니다. 과정 제목은 `Enrollments` 엔터티의 `Course` 탐색 속성에 저장 된 `Course` 엔터티에서 검색 됩니다. 이러한 모든 데이터는 필요할 때 데이터베이스에서 자동으로 검색 됩니다. 즉, 여기서 지연 로드를 사용 합니다. `Courses` 탐색 속성에 대해 *즉시 로드* 를 지정 하지 않았으므로 해당 속성에 처음으로 액세스 하려고 할 때 쿼리를 데이터베이스에 전송 하 여 데이터를 검색 합니다. 이 시리즈의 뒷부분에 나오는 [관련 데이터 읽기](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) 자습서에서 지연 로드 및 즉시 로드에 대해 자세히 알아볼 수 있습니다.
3. **학생** 탭을 선택 하 고 Alexander carson에 대 한 **세부 정보** 링크를 클릭 하 여 페이지를 실행 합니다. 선택한 학생에 대한 강좌 및 등급의 목록이 표시됩니다.

    ![Student_Details_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image5.png)

## <a name="updating-the-create-page"></a>만들기 페이지를 업데이트 하는 중

1. *Controllers\StudentController.cs*에서 `HttpPost``Create` 작업 메서드를 다음 코드로 바꿔 `try-catch` 블록 및 [Bind 특성](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx) 을 스 캐 폴드 메서드에 추가 합니다. 

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample4.cs?highlight=4,7-8,14-20)]

    이 코드는 ASP.NET MVC 모델 바인더에서 만든 `Student` 엔터티를 `Students` 엔터티 집합에 추가한 다음 변경 내용을 데이터베이스에 저장 합니다. (*모델 바인더* 는 폼에서 제출한 데이터를 보다 쉽게 사용할 수 있도록 하는 ASP.NET MVC 기능을 말합니다. 모델 바인더는 게시 된 양식 값을 CLR 형식으로 변환 하 고 매개 변수에서 작업 메서드에 전달 합니다. 이 경우 모델 바인더는 `Form` 컬렉션의 속성 값을 사용 하 여 `Student` 엔터티를 인스턴스화합니다.)

    `ValidateAntiForgeryToken` 특성은 [교차 사이트 요청 위조](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) 공격을 방지 하는 데 도움이 됩니다.

<a id="overpost"></a>

    > [!WARNING]
    > Security - The `Bind` attribute is added to protect against *over-posting*. For example, suppose the `Student` entity includes a `Secret` property that you don't want this web page to update.
    > 
    > [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample5.cs?highlight=7)]
    > 
    > Even if you don't have a `Secret` field on the web page, a hacker could use a tool such as [fiddler](http://fiddler2.com/home), or write some JavaScript, to post a `Secret` form value. Without the [Bind](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx) attribute limiting the fields that the model binder uses when it creates a `Student` instance*,* the model binder would pick up that `Secret` form value and use it to update the `Student` entity instance. Then whatever value the hacker specified for the `Secret` form field would be updated in your database. The following image shows the fiddler tool adding the `Secret` field (with the value "OverPost") to the posted form values.
    > 
    > ![](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image6.png)  
    > 
    > The value "OverPost" would then be successfully added to the `Secret` property of the inserted row, although you never intended that the web page be able to update that property.
    > 
    > It's a security best practice to use the `Include` parameter with the `Bind` attribute to *whitelist* fields. It's also possible to use the `Exclude` parameter to *blacklist* fields you want to exclude. The reason `Include` is more secure is that when you add a new property to the entity, the new field is not automatically protected by an `Exclude` list.
    > 
    > Another alternative approach, and one preferred by many, is to use only view models with model binding. The view model contains only the properties you want to bind. Once the MVC model binder has finished, you copy the view model properties to the entity instance.

    Other than the `Bind` attribute, the `try-catch` block is the only change you've made to the scaffolded code. If an exception that derives from [DataException](https://msdn.microsoft.com/library/system.data.dataexception.aspx) is caught while the changes are being saved, a generic error message is displayed. [DataException](https://msdn.microsoft.com/library/system.data.dataexception.aspx) exceptions are sometimes caused by something external to the application rather than a programming error, so the user is advised to try again. Although not implemented in this sample, a production quality application would log the exception (and non-null inner exceptions ) with a logging mechanism such as [ELMAH](https://code.google.com/p/elmah/).

    The code in *Views\Student\Create.cshtml* is similar to what you saw in *Details.cshtml*, except that `EditorFor` and `ValidationMessageFor` helpers are used for each field instead of `DisplayFor`. The following example shows the relevant code:

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample6.cshtml)]

    *Create.cshtml* also includes `@Html.AntiForgeryToken()`, which works with the `ValidateAntiForgeryToken` attribute in the controller to help prevent [cross-site request forgery](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) attacks.

    No changes are required in *Create.cshtml*.
2. **학생** 탭을 선택 하 고 **새로 만들기**를 클릭 하 여 페이지를 실행 합니다.

    ![Student_Create_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image7.png)

    일부 데이터 유효성 검사는 기본적으로 작동 합니다. 이름 및 잘못 된 날짜를 입력 하 고 **만들기** 를 클릭 하 여 오류 메시지를 표시 합니다.

    ![Students_Create_page_error_message](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image8.png)

    다음 강조 표시 된 코드는 모델 유효성 검사를 보여 줍니다.

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample7.cs?highlight=5)]

    날짜를 9/1/2005 같은 유효한 값으로 변경 하 고 **만들기** 를 클릭 하 여 새 학생이 **인덱스** 페이지에 표시 되는지 확인 합니다.

    ![Students_Index_page_with_new_student](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image9.png)

## <a name="updating-the-edit-post-page"></a>사후 편집 페이지를 업데이트 하는 중

*Controllers\StudentController.cs*에서 `HttpGet` `Edit` 메서드 (`HttpPost` 특성이 없는 메서드)는 `Find` 메서드를 사용 하 여 `Student` 메서드에서 확인 한 것 처럼 메서드를 사용 하 여 선택한 `Details` 엔터티를 검색 합니다. 이 메서드를 변경할 필요가 없습니다.

그러나 `HttpPost` `Edit` 동작 메서드를 다음 코드로 바꿔 `try-catch` 블록과 [바인드 특성](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx)을 추가 합니다.

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample8.cs)]

이 코드는 `HttpPost` `Create` 메서드에서 본 것과 비슷합니다. 그러나 모델 바인더에서 만든 엔터티를 엔터티 집합에 추가 하는 대신이 코드에서는 엔터티가 변경 되었음을 나타내는 플래그를 설정 합니다. [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) 메서드가 호출 되 면 [수정](https://msdn.microsoft.com/library/system.data.entitystate.aspx) 된 플래그를 통해 Entity Framework는 SQL 문을 만들어 데이터베이스 행을 업데이트 합니다. 사용자가 변경 하지 않은 열을 포함 하 여 데이터베이스 행의 모든 열이 업데이트 되며 동시성 충돌은 무시 됩니다. 이 시리즈의 이후 자습서에서 동시성을 처리 하는 방법을 배웁니다.

### <a name="entity-states-and-the-attach-and-savechanges-methods"></a>엔터티 상태 및 연결 및 SaveChanges 메서드

데이터베이스 컨텍스트는 메모리의 엔터티가 데이터베이스의 해당 열과 동기화 상태인지 여부의 추적을 유지하고 이 정보는 `SaveChanges` 메서드를 호출할 때 발생하는 작업을 결정합니다. 예를 들어 새 엔터티를 [Add](https://msdn.microsoft.com/library/system.data.entity.dbset.add(v=vs.103).aspx) 메서드에 전달 하는 경우 해당 엔터티의 상태가 `Added`로 설정 됩니다. 그런 다음 [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) 메서드를 호출 하면 데이터베이스 컨텍스트는 SQL `INSERT` 명령을 실행 합니다.

엔터티는[다음 상태](https://msdn.microsoft.com/library/system.data.entitystate.aspx)중 하나일 수 있습니다.

- `Added`. 엔터티가 데이터베이스에 아직 없습니다. `SaveChanges` 메서드는 `INSERT` 문을 실행 해야 합니다.
- `Unchanged`. `SaveChanges` 메서드에서 이 엔터티로 아무 작업도 수행할 필요가 없습니다. 데이터베이스에서 엔터티를 읽을 때 엔터티는 이 상태로 시작합니다.
- `Modified`. 일부 또는 모든 엔터티의 속성 값이 수정되었습니다. `SaveChanges` 메서드는 `UPDATE` 문을 실행 해야 합니다.
- `Deleted`. 엔터티가 삭제되도록 표시되었습니다. `SaveChanges` 메서드는 `DELETE` 문을 실행 해야 합니다.
- `Detached`. 엔터티가 데이터베이스 컨텍스트에 의해 추적되지 않습니다.

데스크톱 애플리케이션에서는 일반적으로 상태 변경 내용이 자동으로 설정됩니다. 응용 프로그램의 데스크톱 유형에 서 엔터티를 읽고 일부 속성 값을 변경 합니다. 이렇게 하면 해당 엔터티 상태가 자동으로 `Modified`로 변경됩니다. 그런 다음 `SaveChanges`를 호출 하면 Entity Framework는 변경한 실제 속성만 업데이트 하는 SQL `UPDATE` 문을 생성 합니다.

웹 앱의 연결 되지 않은 특성은이 연속 시퀀스를 허용 하지 않습니다. 엔터티를 읽는 [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx) 는 페이지가 렌더링 된 후 삭제 됩니다. `HttpPost` `Edit` 동작 메서드가 호출 되 면 새 요청이 수행 되 고 [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx)의 새 인스턴스가 있는 것 이므로 엔터티 `Modified.` 상태를 수동으로 설정 해야 합니다. 그러면 `SaveChanges`를 호출할 때 컨텍스트는 변경한 속성을 알 수 없기 때문에 Entity Framework가 데이터베이스 행의 모든 열을 업데이트 합니다.

사용자가 실제로 변경한 필드만 SQL `Update` 문으로 업데이트 하려는 경우에는 `HttpPost` `Edit` 메서드를 호출할 때 사용할 수 있도록 원래 값을 특정 방식 (예: 숨겨진 필드)으로 저장할 수 있습니다. 그런 다음 원래 값을 사용 하 여 `Student` 엔터티를 만들고, 해당 원래 버전의 엔터티를 사용 하 여 `Attach` 메서드를 호출 하 고, 엔터티의 값을 새 값으로 업데이트 한 다음 `SaveChanges.`를 호출할 수 있습니다. 자세한 내용은 MSDN 데이터 개발자 센터에서 [엔터티 상태 및 SaveChanges](https://msdn.microsoft.com/data/jj592676) 및 [로컬 데이터](https://msdn.microsoft.com/data/jj592872) 를 참조 하세요.

*Views\Student\Edit.cshtml* 의 코드는 *Create. cshtml*에서 확인 한 것과 비슷하며, 변경할 필요가 없습니다.

**학생** 탭을 선택 하 고 **편집** 하이퍼링크를 클릭 하 여 페이지를 실행 합니다.

![Student_Edit_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image10.png)

데이터의 일부를 변경하고 **저장**을 클릭합니다. 인덱스 페이지에 변경 된 데이터가 표시 됩니다.

![Students_Index_page_after_edit](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image11.png)

## <a name="updating-the-delete-page"></a>삭제 페이지를 업데이트 하는 중

*Controllers\StudentController.cs*의 `HttpGet` `Delete` 메서드에 대 한 템플릿 코드는 `Details` 및 `Edit` 메서드에서 살펴본 대로 `Find` 메서드를 사용 하 여 선택한 `Student` 엔터티를 검색 합니다. 그러나 `SaveChanges`에 대한 호출이 실패하는 경우 사용자 지정 오류 메시지를 구현하려면 이 메서드 및 해당 보기에 일부 기능을 추가합니다.

업데이트 및 만들기 작업에 대해 본 것과 같이 삭제 작업에는 두 개의 작업 메서드가 필요합니다. GET 요청에 대 한 응답으로 호출 되는 메서드는 사용자에 게 삭제 작업을 승인 하거나 취소할 수 있는 뷰를 표시 합니다. 사용자가 승인하는 경우 POST 요청이 생성됩니다. 이 경우 `HttpPost` `Delete` 메서드가 호출 되 고이 메서드는 실제로 삭제 작업을 수행 합니다.

`HttpPost` `Delete` 메서드에 `try-catch` 블록을 추가 하 여 데이터베이스를 업데이트할 때 발생할 수 있는 오류를 처리 합니다. 오류가 발생 하면 `HttpPost` `Delete` 메서드가 `HttpGet` `Delete` 메서드를 호출 하 여 오류가 발생 했음을 나타내는 매개 변수를 전달 합니다. 그런 다음 `HttpGet Delete` 메서드는 오류 메시지와 함께 확인 페이지를 다시 지정 하 여 사용자에 게 취소 하거나 다시 시도할 수 있는 기회를 제공 합니다.

1. `HttpGet` `Delete` 작업 메서드를 오류 보고를 관리 하는 다음 코드로 바꿉니다. 

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample9.cs)]

    이 코드는 변경 내용을 저장 하지 못한 후에 호출 되었는지 여부를 나타내는 [선택적](https://msdn.microsoft.com/library/dd264739.aspx) 부울 매개 변수를 허용 합니다. 이 매개 변수는 이전 오류 없이 `HttpGet` `Delete` 메서드를 호출 하는 경우에 `false` 됩니다. 데이터베이스 업데이트 오류에 대 한 응답으로 `HttpPost` `Delete` 메서드에서 호출 하는 경우 매개 변수가 `true` 되 고 오류 메시지가 뷰에 전달 됩니다.
2. `HttpPost` `Delete` 작업 메서드 (이름이 `DeleteConfirmed`)를 다음 코드로 바꿉니다 .이 코드는 실제 삭제 작업을 수행 하 고 모든 데이터베이스 업데이트 오류를 catch 합니다.

     [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample10.cs)]

     이 코드는 선택한 엔터티를 검색 한 다음 [Remove](https://msdn.microsoft.com/library/system.data.entity.dbset.remove(v=vs.103).aspx) 메서드를 호출 하 여 엔터티의 상태를 `Deleted`설정 합니다. `SaveChanges`를 호출 하면 SQL `DELETE` 명령이 생성 됩니다. 또한 `DeleteConfirmed`에서 `Delete`로 작업 메서드 이름을 변경했습니다. `HttpPost` `Delete` 메서드 라는 스 캐 폴드 코드는 `HttpPost` 메서드에 고유한 서명을 제공 `DeleteConfirmed`. CLR에는 오버 로드 된 메서드가 다른 메서드 매개 변수를 포함 해야 합니다. 이제 서명이 고유 하므로 MVC 규칙을 사용 하 고 `HttpPost`에 동일한 이름을 사용 하 고 delete 메서드를 `HttpGet` 수 있습니다.

     고용량 응용 프로그램의 성능 향상이 우선 순위 인 경우에는 `Find`를 호출 하는 코드 줄을 대체 하 고 노란색 강조 표시와 같이 `Remove` 메서드를 다음 코드로 대체 하 여 불필요 한 SQL 쿼리가 행을 검색 하지 않도록 할 수 있습니다.

     [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample11.cs)]

     이 코드는 기본 키 값만 사용 하 여 `Student` 엔터티를 인스턴스화한 다음 엔터티 상태를 `Deleted`로 설정 합니다. Entity Framework에서 엔터티를 삭제하기 위해 필요한 모든 것입니다.

     앞서 설명한 것 처럼 `HttpGet` `Delete` 메서드는 데이터를 삭제 하지 않습니다. GET 요청에 대 한 응답으로 삭제 작업을 수행 하는 경우 (또는 편집 작업 수행, 만들기 작업 또는 데이터를 변경 하는 다른 작업을 수행 하는 경우) 보안 위험이 발생 합니다. 자세한 내용은 [ASP.NET MVC Tip #46-Stephen Walther의 블로그에서 보안 허점을 만들기 때문에 Delete 링크를 사용 하지 마세요](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx) .
3. *Views\Student\Delete.cshtml*에서 다음 예제와 같이 `h2` 머리글과 `h3` 제목 사이에 오류 메시지를 추가 합니다.

     [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample12.cshtml?highlight=2)]

     **학생** 탭을 선택 하 고 **삭제** 하이퍼링크를 클릭 하 여 페이지를 실행 합니다.

     ![Student_Delete_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image12.png)
4. **삭제**를 클릭합니다. 삭제된 학생 없이 인덱스 페이지가 표시됩니다. (이 시리즈의 뒷부분에 나오는 [동시성 처리](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) 자습서에서 수행 되는 오류 처리 코드의 예제를 확인할 수 있습니다.)

## <a name="ensuring-that-database-connections-are-not-left-open"></a>데이터베이스 연결이 열려 있지 않은지 확인

데이터베이스 연결이 제대로 닫혀 있고 보유 한 리소스가 해제 되었는지 확인 하려면 컨텍스트 인스턴스가 삭제 된 것을 확인 해야 합니다. 따라서 스 캐 폴드 코드는 다음 예제와 같이 *StudentController.cs*의 `StudentController` 클래스 끝에 [Dispose](https://msdn.microsoft.com/library/system.idisposable.dispose(v=vs.110).aspx) 메서드를 제공 합니다.

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample13.cs)]

기본 `Controller` 클래스는 이미 `IDisposable` 인터페이스를 구현 하므로이 코드는 `Dispose(bool)` 메서드에 재정의를 추가 하 여 컨텍스트 인스턴스를 명시적으로 삭제 합니다.

## <a name="summary"></a>요약

이제 `Student` 엔터티에 대 한 간단한 CRUD 작업을 수행 하는 전체 페이지 집합이 있습니다. MVC 도우미를 사용 하 여 데이터 필드에 대 한 UI 요소를 생성 했습니다. MVC 도우미에 대 한 자세한 내용은 [HTML 도우미를 사용 하 여 폼 렌더링](https://msdn.microsoft.com/library/dd410596(v=VS.98).aspx) (페이지는 mvc 3에 대 한 것 이지만 여전히 mvc 4와 관련 됨)을 참조 하세요.

다음 자습서에서는 정렬과 페이징을 추가 하 여 인덱스 페이지의 기능을 확장 합니다.

[ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md)에서 다른 Entity Framework 리소스에 대 한 링크를 찾을 수 있습니다.

> [!div class="step-by-step"]
> [이전](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)
> [다음](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
