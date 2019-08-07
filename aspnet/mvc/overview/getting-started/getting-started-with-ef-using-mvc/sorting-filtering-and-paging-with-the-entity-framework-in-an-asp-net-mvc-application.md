---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: '자습서: ASP.NET MVC 응용 프로그램에서 Entity Framework를 사용 하 여 정렬, 필터링 및 페이징 추가 | Microsoft Docs'
author: tdykstra
description: 이 자습서에서는 **학생** 인덱스 페이지에 정렬, 필터링 및 페이징 기능을 추가 합니다. 간단한 그룹화 페이지도 만들 수 있습니다.
ms.author: riande
ms.date: 01/14/2019
ms.assetid: d5723e46-41fe-4d09-850a-e03b9e285bfa
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: d9fadc12aa83a8095f364cf39e5376243a7d0670
ms.sourcegitcommit: f774732a3960fca079438a88a5472c37cf7be08a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2019
ms.locfileid: "68810757"
---
# <a name="tutorial-add-sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application"></a>자습서: ASP.NET MVC 응용 프로그램에서 Entity Framework를 사용 하 여 정렬, 필터링 및 페이징 추가

[이전 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)에서는 엔터티에 대 한 `Student` 기본 CRUD 작업을 위한 일련의 웹 페이지를 구현 했습니다. 이 자습서에서는 **학생** 인덱스 페이지에 정렬, 필터링 및 페이징 기능을 추가 합니다. 간단한 그룹화 페이지도 만들 수 있습니다.

다음 이미지는 완료 될 때 페이지가 표시 되는 모양을 보여 줍니다. 열 제목은 해당 열로 정렬하기 위해 사용자가 클릭할 수 있는 링크입니다. 열 제목을 반복해서 클릭하면 오름차순 및 내림차순으로 정렬 순서가 토글됩니다.

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * 열 정렬 링크 추가
> * 검색 상자 추가
> * 페이징 추가
> * 정보 페이지 만들기

## <a name="prerequisites"></a>필수 구성 요소

* [기본 CRUD 기능 구현](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)

## <a name="add-column-sort-links"></a>열 정렬 링크 추가

학생 인덱스 페이지에 정렬을 추가 하려면 `Index` `Student` 컨트롤러의 메서드를 변경 하 `Student` 고 인덱스 뷰에 코드를 추가 합니다.

### <a name="add-sorting-functionality-to-the-index-method"></a>인덱스 메서드에 정렬 기능 추가

- *Controllers\StudentController.cs*에서 `Index` 메서드를 다음 코드로 바꿉니다.

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

이 코드는 URL의 쿼리 문자열에서 `sortOrder` 매개 변수를 받습니다. 쿼리 문자열 값은 ASP.NET MVC에서 작업 메서드에 대 한 매개 변수로 제공 됩니다. 매개 변수는 "Name" 또는 "Date" 이며, 선택적으로 밑줄을 지정 하 고 문자열 "desc"를 내림차순으로 지정 하는 문자열입니다. 기본 정렬 순서는 오름차순입니다.

인덱스 페이지를 처음 요청하면 쿼리 문자열은 없습니다. 학습자는 `switch` 문에 대 한 제어에 의해 `LastName`설정 된 기본값 인 오름차순으로 표시 됩니다. 사용자가 열 제목 하이퍼링크를 클릭하면 쿼리 문자열에 해당 `sortOrder` 값이 제공됩니다.

뷰가 적절 `ViewBag` 한 쿼리 문자열 값을 사용 하 여 열 머리글 하이퍼링크를 구성할 수 있도록 두 개의 변수가 사용 됩니다.

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

이것은 3개로 구성된 문입니다. 첫 번째 `sortOrder` 매개 변수는 매개 변수가 null 이거나 `ViewBag.NameSortParm` 비어 있는 경우 "이름\_desc"로 설정 해야 함을 지정 하 고, 그렇지 않은 경우에는 빈 문자열로 설정 해야 합니다. 이러한 두 명령문을 사용하면 뷰에서 다음과 같이 열 제목 하이퍼링크를 설정할 수 있습니다.

| 현재 정렬 순서 | 성 하이퍼링크 | 날짜 하이퍼링크 |
| --- | --- | --- |
| 성 오름차순 | descending | ascending |
| 성 내림차순 | ascending | ascending |
| 날짜 오름차순 | ascending | descending |
| 날짜 내림차순 | ascending | ascending |

메서드는 [LINQ to Entities](/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities) 을 사용 하 여 정렬 기준으로 사용할 열을 지정 합니다. 이 코드는 `switch` 문 <xref:System.Linq.IQueryable%601> 앞에 변수 `switch` 를 만들고, `switch` 문에서이를 수정 하 고, 문 `ToList` 다음에 메서드를 호출 합니다. `IQueryable` 변수를 작성하고 수정하면 데이터베이스에 쿼리가 보내지지 않습니다. `IQueryable` 와`ToList`같은 메서드를 호출 하 여 개체를 컬렉션으로 변환할 때까지 쿼리가 실행 되지 않습니다. 따라서이 코드는 `return View` 문까지 실행 되지 않는 단일 쿼리를 생성 합니다.

각 정렬 순서에 대해 서로 다른 LINQ 문을 작성 하는 대신 LINQ 문을 동적으로 만들 수 있습니다. 동적 LINQ에 대 한 자세한 내용은 [동적 linq](https://go.microsoft.com/fwlink/?LinkID=323957)를 참조 하세요.

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a>학생 인덱스 뷰에 열 제목 하이퍼링크 추가

1. *Views\Student\Index.cshtml*에서 제목 행의 `<tr>` 및 `<th>` 요소를 강조 표시 된 코드로 바꿉니다.

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

   이 코드는 `ViewBag` 속성의 정보를 사용 하 여 적절 한 쿼리 문자열 값으로 하이퍼링크를 설정 합니다.

2. 페이지를 실행 하 고 **Last Name** 및 **등록 날짜** 열 제목을 클릭 하 여 정렬이 작동 하는지 확인 합니다.

   **성** 머리글을 클릭 하면 학생이 내림차순 성 순서로 표시 됩니다.

## <a name="add-a-search-box"></a>검색 상자 추가

학생 인덱스 페이지에 필터링을 추가 하려면 보기에 텍스트 상자와 제출 단추를 추가 하 고 `Index` 메서드에서 해당 내용을 변경 합니다. 텍스트 상자를 사용 하 여 이름 및 성 필드에서 검색할 문자열을 입력할 수 있습니다.

### <a name="add-filtering-functionality-to-the-index-method"></a>인덱스 메서드에 필터링 기능 추가

- *Controllers\StudentController.cs*에서 `Index` 메서드를 다음 코드로 바꿉니다 (변경 내용이 강조 표시 됨).

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

이 코드는 매개 `searchString` 변수 `Index` 를 메서드에 추가 합니다. 검색 문자열 값은 Index 뷰에 추가할 텍스트 상자에서 가져옵니다. 또한 첫 번째 이름 `where` 또는 성이 검색 문자열을 포함 하는 학생만 선택 하는 LINQ 문에 절을 추가 합니다. 절을 <xref:System.Linq.Queryable.Where%2A> 추가 하는 문은 검색할 값이 있는 경우에만 실행 됩니다.

> [!NOTE]
> 대부분의 경우 Entity Framework 엔터티 집합에 대해 동일한 메서드를 호출 하거나 메모리 내 컬렉션에서 확장 메서드로 호출할 수 있습니다. 결과는 일반적으로 동일 하지만 경우에 따라 다를 수 있습니다.
>
> 예를 들어 `Contains` 메서드의 .NET Framework 구현은 빈 문자열을 전달할 때 모든 행을 반환 하지만 SQL Server Compact 4.0에 대 한 Entity Framework 공급자는 빈 문자열에 대해 0 개의 행을 반환 합니다. 따라서이 예제의 코드 (문 `Where` `if` 내에 문을 배치)는 모든 버전의 SQL Server에 대해 동일한 결과를 얻을 수 있도록 합니다. 또한 `Contains` 메서드의 .NET Framework 구현은 기본적으로 대/소문자를 구분 하는 비교를 수행 하지만 Entity Framework SQL Server 공급자는 기본적으로 대/소문자를 구분 하지 않는 비교를 수행 합니다. 따라서 메서드를 `ToUpper` 호출 하 여 테스트를 명시적으로 대/소문자를 구분 하지 않도록 설정 하면 나중에 리포지토리를 사용 하도록 코드를 변경할 때 결과가 변경 되지 않습니다. `IEnumerable` 그러면 `IQueryable` 개체가 아닌 컬렉션이 반환 됩니다. (`IEnumerable` 컬렉션에서 `Contains` 메서드를 호출하면 .NET Framework 구현을 가져오고 `IQueryable` 개체에서 호출하면 데이터베이스 공급자 구현을 가져옵니다.)
>
> 또한 Null 처리는 데이터베이스 공급자 마다 다르거나 `IQueryable` `IEnumerable` 컬렉션을 사용 하는 경우와 비교 하 여 개체를 사용 하는 경우 다를 수 있습니다. 예를 들어 일부 시나리오 `Where` 에서는와 `table.Column != 0` 같은 조건이 값 `null` 으로의 열을 반환 하지 않을 수 있습니다. 기본적으로 EF는 메모리에서 작동 하는 것 처럼 데이터베이스에서 null 값이 일치 하도록 추가 SQL 연산자를 생성 하지만 EF6에서 [Usedatabasenullsemantics](https://docs.microsoft.com/dotnet/api/system.data.entity.infrastructure.dbcontextconfiguration.usedatabasenullsemantics) 플래그를 설정 하거나 EF Core의 [UseRelationalNulls](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.infrastructure.relationaldbcontextoptionsbuilder-2.userelationalnulls) 메서드를 호출할 수 있습니다. 이 동작을 구성 합니다.

### <a name="add-a-search-box-to-the-student-index-view"></a>학생 인덱스 뷰에 검색 상자 추가

1. *Views\Student\Index.cshtml*에서 캡션, 텍스트 상자 및 **검색** 단추를 만들기 `table` 위해 강조 표시 된 코드를 여는 태그 바로 앞에 추가 합니다.

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=4-11)]

2. 페이지를 실행 하 고 검색 문자열을 입력 한 다음 **검색** 을 클릭 하 여 필터링이 작동 하는지 확인 합니다.

   URL에 "a" 검색 문자열이 포함 되어 있지 않습니다. 즉,이 페이지를 책갈피로 만들면 책갈피를 사용할 때 필터링 된 목록을 가져올 수 없습니다. 이는 전체 목록을 정렬 하기 때문에 열 정렬 링크에도 적용 됩니다. **검색** 단추를 변경 하 여 자습서의 뒷부분에서 필터 조건에 대 한 쿼리 문자열을 사용 합니다.

## <a name="add-paging"></a>페이징 추가

학생 인덱스 페이지에 페이징을 추가 하려면 **PagedList** NuGet 패키지를 설치 하는 것으로 시작 합니다. 그런 다음 `Index` 메서드를 추가로 변경 하 고 `Index` 뷰에 페이징 링크를 추가 합니다. **PagedList** 는 ASP.NET Mvc에 대 한 다양 한 페이징 및 정렬 패키지 중 하나 이며, 여기에서 사용 하는 것은 다른 옵션에 대 한 권장 사항이 아닌 예제로만 사용 됩니다.

### <a name="install-the-pagedlistmvc-nuget-package"></a>PagedList NuGet 패키지를 설치 합니다.

NuGet **PagedList** 패키지는 자동으로 **PagedList** 패키지를 종속성으로 설치 합니다. **PagedList** 패키지는 및 `PagedList` `IQueryable` 컬렉션`IEnumerable` 에 대 한 컬렉션 형식 및 확장 메서드를 설치 합니다. `PagedList` 확장 메서드는 또는 `IQueryable` `IEnumerable`에서 컬렉션에 데이터의 단일 페이지를 만들며, 컬렉션은 `PagedList` 페이징을 용이 하 게 하는 여러 속성과 메서드를 제공 합니다. **PagedList** 패키지는 페이징 단추를 표시 하는 페이징 도우미를 설치 합니다.

1. **도구** 메뉴에서 **NuGet 패키지 관리자** , **패키지 관리자 콘솔**을 차례로 선택 합니다.

2. **패키지 관리자 콘솔** 창에서 **패키지 원본이** **Nuget.org** 이 고 **기본 프로젝트가** **ContosoUniversity**인지 확인 하 고 다음 명령을 입력 합니다.

   ```text
   Install-Package PagedList.Mvc
   ```

3. 프로젝트를 빌드합니다.

### <a name="add-paging-functionality-to-the-index-method"></a>인덱스 메서드에 페이징 기능 추가

1. *Controllers\StudentController.cs*에서 `PagedList` 네임 스페이스에 `using` 대 한 문을 추가 합니다.

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

2. `Index` 메서드를 다음 코드로 바꿉니다.

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=1,3,7-16,41-43)]

   이 코드는 `page` 매개 변수, 현재 정렬 순서 매개 변수 및 현재 필터 매개 변수를 메서드 시그니처에 추가 합니다.

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

   페이지가 처음 표시 될 때 또는 사용자가 페이징 또는 정렬 링크를 클릭 하지 않은 경우 모든 매개 변수가 null입니다. 페이징 링크를 클릭 `page` 하면 표시할 페이지 번호가 변수에 포함 됩니다.

   속성 `ViewBag` 은 뷰를 현재 정렬 순서와 함께 제공 합니다 .이는 페이징 링크에 포함 되어야 합니다.

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

   또 다른 속성인 `ViewBag.CurrentFilter`는 현재 필터 문자열을 사용 하 여 뷰를 제공 합니다. 이 값은 페이징 중 필터 설정을 유지하기 위해 페이징 링크에 포함되어야 하며 페이지를 다시 표시할 때 텍스트 상자에 복원되어야 합니다. 페이징 중에 검색 문자열이 변경되면 새 필터로 인해 다른 데이터가 표시될 수 있으므로 페이지는 1로 재설정되어야 합니다. 텍스트 상자에 값을 입력 하 고 제출 단추를 누르면 검색 문자열이 변경 됩니다. 이 경우 `searchString` 매개 변수는 null이 아닙니다.

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

   메서드 끝에서 학생 `ToPagedList` `IQueryable` 개체의 확장 메서드는 학생 쿼리를 페이징을 지 원하는 컬렉션 형식으로 학생의 단일 페이지로 변환 합니다. 그런 다음 학생의 단일 페이지가 보기에 전달 됩니다.

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

   `ToPagedList` 메서드는 페이지 번호를 사용합니다. 두 물음표는 [null 병합 연산자](/dotnet/csharp/language-reference/operators/null-coalescing-operator)를 나타냅니다. Null 병합 연산자는 nullable 형식의 기본값을 정의합니다. `(page ?? 1)` 식은 값이 있는 경우 `page` 값을 반환하고 `page`가 Null이면 1일 반환합니다.

### <a name="add-paging-links-to-the-student-index-view"></a>학생 인덱스 뷰에 페이징 링크 추가

1. *Views\Student\Index.cshtml*에서 기존 코드를 다음 코드로 바꿉니다. 변경 내용은 강조 표시되어 있습니다.

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=1-3,6,9,14,17,24,30,55-56,58-59)]

   페이지 맨 위에 `@model` 문은 뷰가 `List` 개체 대신 `PagedList` 개체를 가져오는 것을 지정합니다.

   에 대 한 `PagedList.Mvc` 문은페이징단추의MVC도우미에대한액세스를제공합니다.`using`

   코드는 [Formmethod. Get](/previous-versions/aspnet/dd460179(v=vs.100))을 지정할 수 있는 [html.beginform](/previous-versions/aspnet/dd492719(v=vs.108)) 의 오버 로드를 사용 합니다.

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

   기본 [HTML.BEGINFORM](/previous-versions/aspnet/dd492719(v=vs.108)) POST를 사용 하 여 폼 데이터를 전송 합니다. 즉, 매개 변수가 HTTP 메시지 본문에 전달 되 고 URL에 쿼리 문자열로 전달 되지 않습니다. HTTP GET을 지정하면 폼 데이터가 URL에 쿼리 문자열로 전달되고 이를 통해 사용자는 URL을 책갈피로 지정할 수 있습니다. [HTTP get 사용에 대 한 W3C 지침은](http://www.w3.org/2001/tag/doc/whenToUseGet.html) 동작으로 인해 업데이트가 발생 하지 않을 때 get을 사용 해야 한다는 것입니다.

   텍스트 상자는 현재 검색 문자열로 초기화 되므로 새 페이지를 클릭 하면 현재 검색 문자열을 볼 수 있습니다.

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml?highlight=1)]

   열 머리글 링크는 쿼리 문자열을 사용하여 현재 검색 문자열을 컨트롤러에 전달하므로 사용자가 필터 결과 내에서 정렬할 수 있습니다.

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1)]

   현재 페이지와 총 페이지 수가 표시 됩니다.

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]

   표시할 페이지가 없으면 "0/0 페이지"가 표시 됩니다. 이 경우 페이지 번호는가 1이 고 `Model.PageNumber` `Model.PageCount` 가 0 이므로 페이지 수는 페이지 수보다 큽니다.

   `PagedListPager` 도우미는 페이징 단추를 표시 합니다.

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

   도우미 `PagedListPager` 는 url 및 스타일을 포함 하 여 사용자 지정할 수 있는 다양 한 옵션을 제공 합니다. 자세한 내용은 GitHub 사이트에서 [TroyGoode/PagedList](https://github.com/TroyGoode/PagedList) 를 참조 하세요.

2. 페이지를 실행 합니다.

   다른 정렬 순서의 페이징 링크를 클릭하여 페이징이 작동하는지 확인합니다. 그런 다음, 검색 문자열을 입력하고 페이징을 다시 시도하여 정렬 및 필터링을 통해 페이징이 제대로 작동하는지 확인합니다.

## <a name="create-an-about-page"></a>정보 페이지 만들기

Contoso 대학 웹 사이트의 정보 페이지에서 각 등록 날짜에 대해 등록 한 학생 수를 표시 합니다. 여기에는 그룹화와 그룹에 대한 간단한 계산이 필요합니다. 이 작업을 수행하기 위해 다음을 수행합니다.

- 뷰에 전달해야 하는 데이터에 대해 뷰 모델 클래스를 만듭니다.
- 컨트롤러에서 메서드를 `About` 수정 합니다. `Home`
- 뷰를 `About` 수정 합니다.

### <a name="create-the-view-model"></a>뷰 모델 만들기

프로젝트 폴더에 *Viewmodels* 폴더를 만듭니다. 해당 폴더에서 *EnrollmentDateGroup.cs* 클래스를 추가 하 고 템플릿 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a>홈 컨트롤러 수정

1. *HomeController.cs*에서 파일 맨 위에 다음 `using` 문을 추가 합니다.

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

2. 클래스에 대 한 여는 중괄호 바로 뒤에 데이터베이스 컨텍스트에 대 한 클래스 변수를 추가 합니다.

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

3. `About` 메서드를 다음 코드로 바꿉니다.

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

   LINQ 문은 등록 날짜별로 학생 엔터티를 그룹화하고 각 그룹의 엔터티 수를 계산하며 결과를 `EnrollmentDateGroup` 뷰 모델 개체의 컬렉션에 저장합니다.

4. 메서드를 `Dispose` 추가 합니다.

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a>정보 뷰 수정

1. *Views\Home\About.cshtml* 파일의 코드를 다음 코드로 바꿉니다.

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

2. 앱을 실행 하 고 **정보** 링크를 클릭 합니다.

   각 등록 날짜에 대 한 학생 수가 테이블에 표시 됩니다.

   ![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="get-the-code"></a>코드 가져오기

[완료 된 프로젝트 다운로드](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>추가 자료

[ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)에서 다른 Entity Framework 리소스에 대 한 링크를 찾을 수 있습니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * 열 정렬 링크 추가
> * 검색 상자 추가
> * 페이징 추가
> * 정보 페이지 만들기

다음 문서로 이동 하 여 연결 복원 력 및 명령 가로채기를 사용 하는 방법을 알아보세요.
> [!div class="nextstepaction"]
> [연결 복원 력 및 명령 가로채기](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)
