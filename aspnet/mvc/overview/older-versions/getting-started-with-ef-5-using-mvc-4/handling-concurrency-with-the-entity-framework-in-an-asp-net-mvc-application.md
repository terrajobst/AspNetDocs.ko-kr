---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
title: ASP.NET MVC 응용 프로그램에서 Entity Framework를 사용 하 여 동시성 처리 (7/10) | Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다.
ms.author: riande
ms.date: 07/30/2013
ms.assetid: b83f47c4-8521-4d0a-8644-e8f77e39733e
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9800a313879477f36a730e6a70c79bc06d403ae3
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/07/2020
ms.locfileid: "77074958"
---
# <a name="handling-concurrency-with-the-entity-framework-in-an-aspnet-mvc-application-7-of-10"></a>ASP.NET MVC 응용 프로그램에서 Entity Framework를 사용 하 여 동시성 처리 (7/10)

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 5 Code First 및 Visual Studio 2012을 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요. [이 챕터의](building-the-ef5-mvc4-chapter-downloads.md) 시작 또는 시작 프로젝트 다운로드에서 자습서 시리즈를 시작 하 고 여기에서 시작할 수 있습니다.
> 
> > [!NOTE] 
> > 
> > 해결할 수 없는 문제가 발생 하는 경우 [완료 된 챕터를 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 하 여 문제를 재현해 보세요. 일반적으로 코드를 완성 된 코드와 비교 하 여 문제에 대 한 솔루션을 찾을 수 있습니다. 몇 가지 일반적인 오류 및 해결 방법에 대 한 자세한 내용은 [오류 및 해결](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors) 방법을 참조 하세요.

이전 두 자습서에서는 관련 데이터로 작업 했습니다. 이 자습서에서는 동시성을 처리 하는 방법을 보여 줍니다. `Department` 엔터티를 사용 하 여 작업 하는 웹 페이지를 만들고 `Department` 엔터티를 편집 및 삭제 하는 페이지가 동시성 오류를 처리 합니다. 다음 그림에서는 동시성 충돌이 발생 하는 경우 표시 되는 일부 메시지를 포함 하 여 인덱스 및 삭제 페이지를 보여 줍니다.

![Department_Index_page_before_edits](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="concurrency-conflicts"></a>동시성 충돌

한 명의 사용자가 편집하기 위해 엔터티의 데이터를 표시한 다음, 다른 사용자가 첫 번째 사용자의 변경 내용이 데이터베이스에 기록되기 전에 동일한 엔터티의 데이터를 업데이트하는 경우 동시성 충돌이 발생합니다. 이러한 충돌의 감지를 활성화하지 않는 경우 누구든지 데이터베이스를 마지막으로 업데이트하면 다른 사용자의 변경 내용을 덮어씁니다. 많은 애플리케이션에서 이 위험은 허용 가능합니다. 적은 수의 사용자 또는 적은 업데이트가 있거나 일부 변경 내용이 덮어쓰여지는지 여부가 실제로 중요하지 않은 경우 동시성에 대한 프로그래밍의 비용은 이점보다 클 수 있습니다. 이 경우 동시성 충돌을 처리하도록 애플리케이션을 구성할 필요가 없습니다.

### <a name="pessimistic-concurrency-locking"></a>비관적 동시성 (잠금)

애플리케이션에서 동시성 시나리오에서 실수로 인한 데이터 손실을 방지할 필요가 있는 경우 해당 작업을 수행하는 한 가지 방법은 데이터베이스 잠금을 사용하는 것입니다. 이를 *비관적 동시성*이라고 합니다. 예를 들어 데이터베이스에서 행을 읽기 전에 읽기 전용 또는 업데이트 액세스에 대한 잠금을 요청합니다. 업데이트 액세스에 대한 행을 잠그는 경우 변경 중인 데이터의 복사본을 가져오기 때문에 다른 사용자는 읽기 전용 또는 업데이트 액세스에 대한 행을 잠그도록 허용되지 않습니다. 읽기 전용 액세스에 대한 행을 잠그는 경우 다른 사용자도 읽기 전용에 대해 잠글 수 있지만 업데이트에 대해서는 잠글 수 없습니다.

잠금 관리에는 단점이 있습니다. 프로그램을 설정하는 데 복잡할 수 있습니다. 중요 한 데이터베이스 관리 리소스가 필요 하며, 응용 프로그램의 사용자 수가 증가 함에 따라 성능 문제가 발생할 수 있습니다 (즉, 크기를 조정 하지 않음). 이러한 이유로 모든 데이터베이스 관리 시스템은 비관적 동시성을 지원하지 않습니다. Entity Framework는이에 대 한 기본 제공 지원을 제공 하지 않으며이 자습서에서 구현 방법을 보여 주지 않습니다.

### <a name="optimistic-concurrency"></a>낙관적 동시성

비관적 동시성 대신 *낙관적 동시성*을 사용할 수 있습니다. 낙관적 동시성은 동시성 충돌 발생을 허용한 다음, 그럴 경우 적절하게 반응하는 것을 의미합니다. 예를 들어, John은 부서 편집 페이지를 실행 하 고, 영어 부서에 대 한 **예산** 금액을 $350000.00에서 $0.00로 변경 합니다.

![Changing_English_dept_budget_to_100000](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

John이 **Save**를 클릭 하기 전에 Jane은 같은 페이지를 실행 하 고 **시작 날짜** 필드를 9/1/2007에서 8/8/2013로 변경 합니다.

![Changing_English_dept_start_date_to_1999](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

John이 먼저 **저장** 을 클릭 하 고 브라우저가 인덱스 페이지로 반환 될 때 해당 변경 내용을 확인 한 다음 Jane은 **저장**을 클릭 합니다. 다음 작업은 동시성 충돌을 처리하는 방법에 따라 결정됩니다. 몇 가지 옵션에는 다음이 포함됩니다.

- 사용자가 수정한 속성의 추적을 유지하고 데이터베이스에서 해당하는 열만 업데이트할 수 있습니다. 예제 시나리오에서 서로 다른 속성이 두 사용자에 의해 업데이트되었기 때문에 데이터가 손실되지 않습니다. 다음에 누군가가 영어 부서를 찾아볼 때 John의 변경 내용 (8/8/2013의 시작 날짜 및 0 달러의 예산)이 표시 됩니다.

    이 업데이트의 메서드는 데이터 손실이 발생할 수 있는 충돌 수를 줄일 수 있지만 경쟁하는 변경 내용이 동일한 엔터티의 속성에 만들어지는 경우 데이터 손실을 방지할 수 없습니다. Entity Framework가 이 방식으로 작동하는지 여부는 업데이트 코드를 구현하는 방법에 따라 달라집니다. 엔터티에 대한 모든 기존 속성 값 뿐만 아니라 새 값의 추적을 유지하기 위해 많은 양의 상태를 유지 관리해야 하므로 웹 애플리케이션에서는 종종 실용적이지 않습니다. 많은 양의 상태를 유지 관리 하는 것은 서버 리소스가 필요 하거나 웹 페이지 자체 (예: 숨겨진 필드)에 포함 되어야 하므로 응용 프로그램 성능에 영향을 줄 수 있습니다.
- Jane의 변경 내용이 John의 변경 내용을 덮어쓰는 것을 허용할 수 있습니다. 다음에 누군가가 영어 부서를 찾아볼 때 8/8/2013 및 복원 된 $350000.00 값이 표시 됩니다. 이를 *클라이언트 우선* 또는 *최종 우선* 시나리오라고 합니다. (클라이언트의 값은 데이터 저장소에 있는 것 보다 우선 적용 됩니다.) 이 섹션 소개에서 설명한 것 처럼 동시성 처리를 위한 코딩을 수행 하지 않으면 자동으로 수행 됩니다.
- Jane의 변경 내용이 데이터베이스에서 업데이트 되는 것을 방지할 수 있습니다. 일반적으로 오류 메시지를 표시 하 고, 데이터의 현재 상태를 표시 하 고, 변경 하려는 경우 변경 내용을 다시 적용 하도록 할 수 있습니다. 이를 *저장소 우선* 시나리오라고 합니다. (데이터 저장소 값은 클라이언트에서 전송 된 값 보다 우선 적용 됩니다.) 이 자습서에서는 저장소 우선 시나리오를 구현 합니다. 이 메서드는 상황에 대한 경고를 받는 사용자 없이 변경 내용을 덮어쓰지 않도록 합니다.

### <a name="detecting-concurrency-conflicts"></a>동시성 충돌 감지

Entity Framework throw 되는 [OptimisticConcurrencyException](https://msdn.microsoft.com/library/system.data.optimisticconcurrencyexception.aspx) 예외를 처리 하 여 충돌을 해결할 수 있습니다. 이러한 예외를 throw하는 시기를 확인하기 위해 Entity Framework에서 충돌을 검색할 수 있어야 합니다. 따라서 데이터베이스와 데이터 모델을 적절하게 구성해야 합니다. 충돌 검색을 활성화하기 위한 몇 가지 옵션은 다음과 같습니다.

- 데이터베이스 테이블에서 행이 변경된 시기를 확인하는 데 사용될 수 있는 추적 열을 포함합니다. 그런 다음 SQL `Update` 또는 `Delete` 명령의 `Where` 절에 해당 열을 포함 하도록 Entity Framework를 구성할 수 있습니다.

    추적 열의 데이터 형식은 일반적으로 [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)입니다. [Rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) 값은 행이 업데이트 될 때마다 증가 하는 일련 번호입니다. `Update` 또는 `Delete` 명령에서 `Where` 절에는 추적 열의 원래 값 (원래 행 버전)이 포함 됩니다. 업데이트 되는 행이 다른 사용자에 의해 변경 된 경우 `rowversion` 열의 값이 원래 값과 다르므로 `Update` 또는 `Delete` 문이 `Where` 절 때문에 업데이트할 행을 찾을 수 없습니다. Entity Framework `Update` 또는 `Delete` 명령에 의해 업데이트 된 행이 없는 것을 발견 하면 (즉, 영향을 받는 행의 수가 0 인 경우) 동시성 충돌로 해석 합니다.
- `Update` 및 `Delete` 명령의 `Where` 절에서 테이블에 있는 모든 열의 원래 값을 포함 하도록 Entity Framework를 구성 합니다.

    첫 번째 옵션에서와 같이 행을 처음 읽은 후 행의 내용이 변경 된 경우에는 `Where` 절이 업데이트할 행을 반환 하지 않습니다 .이는 Entity Framework에서 동시성 충돌로 해석 합니다. 많은 열이 있는 데이터베이스 테이블의 경우이 방법을 사용 하면 `Where` 절이 매우 클 수 있으며 많은 양의 상태를 유지 관리 해야 할 수 있습니다. 앞에서 설명한 것 처럼 많은 양의 상태를 유지 관리 하는 것은 서버 리소스가 필요 하거나 웹 페이지 자체에 포함 되어야 하므로 응용 프로그램 성능에 영향을 줄 수 있습니다. 따라서이 방법은 일반적으로 권장 되지 않으며이 자습서에서 사용 되는 방법이 아닙니다.

    동시성에 대해이 방법을 구현 하려면 [ConcurrencyCheck](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.concurrencycheckattribute.aspx) 특성을 추가 하 여 동시성을 추적 하려는 엔터티의 기본 키가 아닌 모든 속성을 표시 해야 합니다. 이렇게 변경 하면 Entity Framework에서 `UPDATE` 문의 SQL `WHERE` 절에 있는 모든 열을 포함할 수 있습니다.

이 자습서의 나머지 부분에서는 [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) 추적 속성을 `Department` 엔터티에 추가 하 고 컨트롤러 및 뷰를 만든 다음 테스트 하 여 모든 것이 제대로 작동 하는지 확인 합니다.

## <a name="add-an-optimistic-concurrency-property-to-the-department-entity"></a>부서 엔터티에 낙관적 동시성 속성 추가

*Models\Department.cs*에서 `RowVersion`이라는 추적 속성을 추가 합니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=18-19)]

[Timestamp](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx) 특성은이 열이 `Update`의 `Where` 절에 포함 되 고 `Delete` 명령이 데이터베이스로 전송 됨을 지정 합니다. 이전 버전의 SQL Server sql [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) 에서 sql [타임 스탬프](https://msdn.microsoft.com/library/ms182776(v=SQL.90).aspx) 데이터 형식을 사용 하기 때문에 특성을 [timestamp](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx) 라고 합니다. `rowversion`에 대 한 .Net 형식은 바이트 배열입니다. 흐름 API를 사용 하려는 경우 다음 예제와 같이 [IsConcurrencyToken](https://msdn.microsoft.com/library/gg679501(v=VS.103).aspx) 메서드를 사용 하 여 추적 속성을 지정할 수 있습니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

GitHub 문제 [Replace IsConcurrencyToken By IsRowVersion](https://github.com/aspnet/AspNetDocs/issues/302)를 참조 하세요.

속성을 추가하여 데이터베이스 모델을 변경했으므로 다른 마이그레이션을 수행해야 합니다. PMC(패키지 관리자 콘솔)에서 다음 명령을 입력합니다.

[!code-console[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cmd)]

## <a name="create-a-department-controller"></a>부서 컨트롤러 만들기

다음 설정을 사용 하 여 다른 컨트롤러와 동일한 방식으로 `Department` 컨트롤러 및 뷰를 만듭니다.

![Add_Controller_dialog_box_for_Department_controller](https://asp.net/media/2578041/Windows-Live-Writer_Handling-C.NET-MVC-Application-7-of-10h1_AFDC_Add_Controller_dialog_box_for_Department_controller_d1d9c788-f970-4d6a-9f5a-1eddc84330b7.png)

*Controllers\DepartmentController.cs*에서 `using` 문을 추가 합니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

부서 관리자 드롭다운 목록에 성이 아닌 강사의 전체 이름이 포함 되도록 "LastName"을이 파일의 모든 위치에서 "FullName"으로 변경 합니다 (4 회).

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=1)]

`HttpPost` `Edit` 메서드의 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

뷰에 원래 `RowVersion` 값이 숨겨진 필드에 저장 됩니다. 모델 바인더는 `department` 인스턴스를 만들 때 편집 페이지에서 사용자가 입력 한 대로 원래 `RowVersion` 속성 값과 다른 속성의 새 값을 갖게 됩니다. 그런 다음 Entity Framework SQL `UPDATE` 명령을 만들 때 해당 명령은 원래 `RowVersion` 값이 있는 행을 찾는 `WHERE` 절을 포함 합니다.

`UPDATE` 명령의 영향을 받는 행이 없는 경우 (행에 원래 `RowVersion` 값이 없는 경우) Entity Framework는 `DbUpdateConcurrencyException` 예외를 throw 하 고 `catch` 블록의 코드는 예외 개체에서 영향을 받는 `Department` 엔터티를 가져옵니다. 이 엔터티에는 데이터베이스에서 읽은 값과 사용자가 입력 한 새 값이 모두 있습니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

다음으로,이 코드는 사용자가 편집 페이지에서 입력 한 것과 다른 데이터베이스 값이 있는 각 열에 대해 사용자 지정 오류 메시지를 추가 합니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

더 긴 오류 메시지는 발생 한 내용과 그에 대해 수행할 작업을 설명 합니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

마지막으로,이 코드는 `Department` 개체의 `RowVersion` 값을 데이터베이스에서 검색 된 새 값으로 설정 합니다. 이 새로운 `RowVersion` 값은 편집 페이지가 다시 표시되고, 다음 번에 사용자가 **저장**을 클릭할 때 숨겨진 필드에 저장되고, 편집 페이지의 다시 표시로 인해 발생하는 동시성 오류만 catch됩니다.

*Views\Department\Edit.cshtml*에서 숨겨진 필드를 추가 하 여 `DepartmentID` 속성에 대 한 숨겨진 필드 바로 뒤에 `RowVersion` 속성 값을 저장 합니다.

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cshtml?highlight=17)]

*Views\Department\Index.cshtml*에서 기존 코드를 다음 코드로 바꾸어 행 링크를 왼쪽으로 이동 하 고 페이지 제목 및 열 머리글을 변경 하 여 **관리자** 열에 `LastName` 대신 `FullName` 표시 합니다.

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cshtml)]

## <a name="testing-optimistic-concurrency-handling"></a>낙관적 동시성 처리 테스트

사이트를 실행 하 고 **부서**를 클릭 합니다.

![Department_Index_page_before_edits](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

최 차장 Abercrombie에 대 한 **편집** 하이퍼링크를 마우스 오른쪽 단추로 클릭 하 고 **새 탭에서 열기를** 선택한 다음 최 차장 Abercrombie에 대 한 **편집** 하이퍼링크를 클릭 합니다. 두 창에 동일한 정보가 표시 됩니다.

![Department_Edit_page_before_changes](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

첫 번째 브라우저 창에서 필드를 변경 하 고 **저장**을 클릭 합니다.

![Department_Edit_page_1_after_change](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

브라우저에 변경된 값과 인덱스 페이지가 표시됩니다.

![Departments_Index_page_after_first_budget_edit](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

두 번째 브라우저 창에서 모든 필드를 변경 하 고 **저장**을 클릭 합니다.

![Department_Edit_page_2_after_change](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

두 번째 브라우저 창에서 **저장** 을 클릭 합니다. 오류 메시지가 표시됩니다.

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

**저장**을 다시 클릭합니다. 두 번째 브라우저에서 입력 한 값은 첫 번째 브라우저에서 변경한 데이터의 원래 값과 함께 저장 됩니다. 인덱스 페이지가 나타날 때 저장된 값이 표시됩니다.

![Department_Index_page_with_change_from_second_browser](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image11.png)

## <a name="updating-the-delete-page"></a>삭제 페이지를 업데이트 하는 중

삭제 페이지의 경우 Entity Framework는 비슷한 방식으로 부서를 편집하는 사용자에 의해 발생한 동시성 충돌을 감지합니다. `HttpGet` `Delete` 메서드가 확인 보기를 표시 하는 경우 뷰는 숨겨진 필드에 원래 `RowVersion` 값을 포함 합니다. 그런 다음 사용자가 삭제를 확인 하는 경우 호출 되는 `HttpPost` `Delete` 메서드에서 해당 값을 사용할 수 있습니다. Entity Framework SQL `DELETE` 명령을 만들 때 원래 `RowVersion` 값을 포함 하는 `WHERE` 절이 포함 됩니다. 명령으로 인해 영향을 받지 않는 행이 있으면 (삭제 확인 페이지가 표시 된 후 행이 변경 된 것을 의미 함) 동시성 예외가 throw 되 고 확인 페이지를 오류 메시지와 함께 다시 표시 하기 위해 오류 플래그가 `true`로 설정 된 상태에서 `HttpGet Delete` 메서드가 호출 됩니다. 또한 다른 사용자가 행을 삭제 했기 때문에 0 개의 행이 영향을 받을 수 있으므로이 경우 다른 오류 메시지가 표시 됩니다.

*DepartmentController.cs*에서 `HttpGet` `Delete` 메서드를 다음 코드로 바꿉니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]

메서드는 동시성 오류가 발생한 후 페이지가 다시 표시되고 있는지 여부를 나타내는 선택적 매개 변수를 허용합니다. 이 플래그가 `true`된 경우 `ViewBag` 속성을 사용 하 여 오류 메시지를 뷰로 보냅니다.

`HttpPost` `Delete` 메서드 (이름이 `DeleteConfirmed`)의 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

방금 바꾼 스캐폴드된 코드에서 이 메서드는 레코드 ID만 허용했습니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

이 매개 변수를 모델 바인더에서 만든 `Department` 엔터티 인스턴스로 변경 했습니다. 이를 통해 레코드 키 외에도 `RowVersion` 속성 값에 액세스할 수 있습니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

또한 `DeleteConfirmed`에서 `Delete`로 작업 메서드 이름을 변경했습니다. `HttpPost` `Delete` 메서드 라는 스 캐 폴드 코드는 `HttpPost` 메서드에 고유한 서명을 제공 `DeleteConfirmed`. CLR에는 오버 로드 된 메서드가 다른 메서드 매개 변수를 포함 해야 합니다. 이제 서명이 고유 하므로 MVC 규칙을 사용 하 고 `HttpPost`에 동일한 이름을 사용 하 고 delete 메서드를 `HttpGet` 수 있습니다.

동시성 오류가 catch되는 경우 코드는 삭제 확인 페이지를 다시 표시하고 동시성 오류 메시지를 표시해야 함을 나타내는 플래그를 제공합니다.

*Views\Department\Delete.cshtml*에서 스 캐 폴드 코드를 서식을 변경 하 고 오류 메시지 필드를 추가 하는 다음 코드로 바꿉니다. 변경 내용은 강조 표시되어 있습니다.

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml?highlight=9,37,40,45-46)]

이 코드는 `h2` 및 `h3` 머리글 사이에 오류 메시지를 추가 합니다.

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

`LastName`를 `Administrator` 필드의 `FullName`으로 바꿉니다.

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

마지막으로 `Html.BeginForm` 문 뒤에 `DepartmentID` 및 `RowVersion` 속성에 대 한 숨겨진 필드를 추가 합니다.

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

부서 인덱스 페이지를 실행 합니다. 영어 부서에 대 한 **삭제** 하이퍼링크를 마우스 오른쪽 단추로 클릭 하 고 **새 창에서 열기를** 선택한 다음 첫 번째 창에서 영어 부서에 대 한 **편집** 하이퍼링크를 클릭 합니다.

첫 번째 창에서 값 중 하나를 변경 하 고 **저장** 을 클릭 합니다.

![Department_Edit_page_after_change_before_delete](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image12.png)

인덱스 페이지에서 변경 내용을 확인 합니다.

![Departments_Index_page_after_budget_edit_before_delete](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)

두 번째 창에서 **삭제**를 클릭 합니다.

![Department_Delete_confirmation_page_before_concurrency_error](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)

동시성 오류 메시지가 표시되며 부서 값은 데이터베이스의 현재 값으로 새로 고쳐집니다.

![Department_Delete_confirmation_page_with_concurrency_error](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)

**삭제**를 다시 클릭하면 부서가 삭제되었음을 보여 주는 인덱스 페이지로 리디렉션됩니다.

## <a name="summary"></a>요약

동시성 충돌 처리에 대한 소개를 완료합니다. 다양 한 동시성 시나리오를 처리 하는 다른 방법에 대 한 자세한 내용은 [낙관적 동시성 패턴](https://blogs.msdn.com/b/adonet/archive/2011/02/03/using-dbcontext-in-ef-feature-ctp5-part-9-optimistic-concurrency-patterns.aspx) 및 Entity Framework 팀 블로그에서 [속성 값 작업](https://blogs.msdn.com/b/adonet/archive/2011/01/30/using-dbcontext-in-ef-feature-ctp5-part-5-working-with-property-values.aspx) 을 참조 하세요. 다음 자습서에서는 `Instructor` 및 `Student` 엔터티에 대해 계층당 하나의 테이블 상속을 구현 하는 방법을 보여 줍니다.

[ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md)에서 다른 Entity Framework 리소스에 대 한 링크를 찾을 수 있습니다.

> [!div class="step-by-step"]
> [이전](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [다음](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
