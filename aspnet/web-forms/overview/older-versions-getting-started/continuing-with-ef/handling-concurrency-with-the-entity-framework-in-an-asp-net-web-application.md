---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application
title: ASP.NET 4 웹 응용 프로그램에서 Entity Framework 4.0를 사용 하 여 동시성 처리 | Microsoft Docs
author: tdykstra
description: 이 자습서 시리즈는 Entity Framework 4.0 자습서 시리즈 시작에서 만든 Contoso 대학 웹 응용 프로그램을 기반으로 합니다. I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: a5aa22a6-fb7f-4f41-9c7f-addda151940b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application
msc.type: authoredcontent
ms.openlocfilehash: 3df5f7d9c8fb22e1ea34fe16560bdb9a1309bb56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78513503"
---
# <a name="handling-concurrency-with-the-entity-framework-40-in-an-aspnet-4-web-application"></a>ASP.NET 4 웹 응용 프로그램에서 Entity Framework 4.0를 사용 하 여 동시성 처리

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

> 이 자습서 시리즈는 [Entity Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started) 자습서 시리즈 시작에서 만든 Contoso 대학 웹 응용 프로그램을 기반으로 합니다. 이전 자습서를 완료 하지 않은 경우이 자습서의 시작 점으로, 만든 [응용 프로그램을 다운로드할](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) 수 있습니다. 전체 자습서 시리즈에서 만든 [응용 프로그램을 다운로드할](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) 수도 있습니다. 자습서에 대 한 질문이 있는 경우 [ASP.NET Entity Framework 포럼](https://forums.asp.net/1227.aspx)에 게시할 수 있습니다.

이전 자습서에서는 `ObjectDataSource` 컨트롤과 Entity Framework를 사용 하 여 데이터를 정렬 하 고 필터링 하는 방법을 배웠습니다. 이 자습서에서는 Entity Framework를 사용 하는 ASP.NET 웹 응용 프로그램에서 동시성을 처리 하는 옵션을 보여 줍니다. 강사 office 할당을 업데이트 하는 전용 웹 페이지를 새로 만듭니다. 해당 페이지와 앞에서 만든 부서 페이지에서 동시성 문제를 처리 합니다.

[![Image06](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image2.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image1.png)

[![Image01](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image4.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image3.png)

## <a name="concurrency-conflicts"></a>동시성 충돌

동시성 충돌은 한 사용자가 레코드를 편집 하 고 첫 번째 사용자의 변경 내용이 데이터베이스에 기록 되기 전에 다른 사용자가 동일한 레코드를 편집할 때 발생 합니다. 이러한 충돌을 검색 하도록 Entity Framework를 설정 하지 않으면 데이터베이스를 마지막으로 업데이트 하 여 다른 사용자의 변경 내용을 덮어씁니다. 많은 응용 프로그램에서이 위험이 허용 되며, 가능한 동시성 충돌을 처리 하도록 응용 프로그램을 구성할 필요가 없습니다. (사용자가 거의 없거나 업데이트가 많지 않은 경우 또는 일부 변경 내용을 덮어쓰는 경우에는 중요 하지 않은 경우에는 동시성 프로그래밍의 비용이 이점 보다 클 수 있습니다.) 동시성 충돌에 대해 걱정 하지 않아도 되는 경우이 자습서를 건너뛸 수 있습니다. 시리즈의 나머지 두 자습서는이 자습서에서 작성 한 항목에 종속 되지 않습니다.

### <a name="pessimistic-concurrency-locking"></a>비관적 동시성 (잠금)

애플리케이션에서 동시성 시나리오에서 실수로 인한 데이터 손실을 방지할 필요가 있는 경우 해당 작업을 수행하는 한 가지 방법은 데이터베이스 잠금을 사용하는 것입니다. 이를 *비관적 동시성*이라고 합니다. 예를 들어 데이터베이스에서 행을 읽기 전에 읽기 전용 또는 업데이트 액세스에 대한 잠금을 요청합니다. 업데이트 액세스에 대한 행을 잠그는 경우 변경 중인 데이터의 복사본을 가져오기 때문에 다른 사용자는 읽기 전용 또는 업데이트 액세스에 대한 행을 잠그도록 허용되지 않습니다. 읽기 전용 액세스에 대한 행을 잠그는 경우 다른 사용자도 읽기 전용에 대해 잠글 수 있지만 업데이트에 대해서는 잠글 수 없습니다.

잠금 관리에는 몇 가지 단점이 있습니다. 프로그램을 설정하는 데 복잡할 수 있습니다. 중요 한 데이터베이스 관리 리소스가 필요 하며, 응용 프로그램의 사용자 수가 증가 함에 따라 성능 문제가 발생할 수 있습니다 (즉, 크기를 조정 하지 않음). 이러한 이유로 모든 데이터베이스 관리 시스템은 비관적 동시성을 지원하지 않습니다. Entity Framework는이에 대 한 기본 제공 지원을 제공 하지 않으며이 자습서에서 구현 방법을 보여 주지 않습니다.

### <a name="optimistic-concurrency"></a>낙관적 동시성

비관적 동시성 대신 *낙관적 동시성*을 사용할 수 있습니다. 낙관적 동시성은 동시성 충돌 발생을 허용한 다음, 그럴 경우 적절하게 반응하는 것을 의미합니다. 예를 들어, John은 *학과* 페이지를 실행 하 고, History 부서에 대 한 **편집** 링크를 클릭 하 고, **예산** 크기를 $1000000.00에서 $125000.00으로 줄입니다. (John은 경쟁 부서를 관리 하 고 자신의 부서에 대 한 비용을 확보 하려고 합니다.)

[![Image07](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image6.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image5.png)

John이 **업데이트**를 클릭 하기 전에 Jane은 같은 페이지를 실행 하 고, History 부서에 대 한 **편집** 링크를 클릭 한 다음 **시작 날짜** 필드를 1/10/2011에서 1/1/1999로 변경 합니다. Jane은 기록 부서를 관리 하 고 더 seniority를 제공 하려고 합니다.

[![Image08](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image8.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image7.png)

먼저 **업데이트** 를 클릭 한 다음 Jane은 **업데이트**를 클릭 합니다. Jane의 브라우저는 이제 $1000000.00으로 **예산** 금액을 나열 하지만, 크기가 John에서 $125000.00로 변경 되었기 때문에 잘못 되었습니다.

이 시나리오에서 수행할 수 있는 작업에는 다음이 포함 됩니다.

- 사용자가 수정한 속성의 추적을 유지하고 데이터베이스에서 해당하는 열만 업데이트할 수 있습니다. 예제 시나리오에서 서로 다른 속성이 두 사용자에 의해 업데이트되었기 때문에 데이터가 손실되지 않습니다. 다음에 누군가가 기록 부서를 탐색할 때 1/1/1999 및 $125000.00이 표시 됩니다. 

    이는 Entity Framework의 기본 동작으로, 데이터 손실이 발생할 수 있는 충돌 수를 크게 줄일 수 있습니다. 그러나 엔터티의 같은 속성을 변경 하는 경우에는 이러한 동작으로 인해 데이터 손실이 발생 하지 않습니다. 또한이 동작은 항상 가능 하지는 않습니다. 저장 프로시저를 엔터티 형식에 매핑하면 엔터티에 대 한 변경 내용이 데이터베이스에 적용 될 때 엔터티의 속성이 모두 업데이트 됩니다.
- Jane의 변경 내용이 John의 변경 내용을 덮어쓰는 것을 허용할 수 있습니다. Jane이 **업데이트**를 클릭 하면 **예산** 금액이 $1000000.00로 돌아갑니다. 이를 *클라이언트 우선* 또는 *최종 우선* 시나리오라고 합니다. (클라이언트의 값은 데이터 저장소에 있는 것 보다 우선 적용 됩니다.)
- Jane의 변경 내용이 데이터베이스에서 업데이트 되는 것을 방지할 수 있습니다. 일반적으로 오류 메시지를 표시 하 고, 데이터의 현재 상태를 표시 하 고, 변경 하려는 경우 변경 내용을 다시 입력할 수 있습니다. 사용자의 입력을 저장 하 고 다시 입력 하지 않고 다시 적용할 수 있는 기회를 제공 하 여 프로세스를 추가로 자동화할 수 있습니다. 이를 *저장소 우선* 시나리오라고 합니다. (데이터 저장소 값은 클라이언트에서 전송한 값에 우선합니다.)

### <a name="detecting-concurrency-conflicts"></a>동시성 충돌 감지

Entity Framework에서 Entity Framework throw 하는 `OptimisticConcurrencyException` 예외를 처리 하 여 충돌을 해결할 수 있습니다. 이러한 예외를 throw하는 시기를 확인하기 위해 Entity Framework에서 충돌을 검색할 수 있어야 합니다. 따라서 데이터베이스와 데이터 모델을 적절하게 구성해야 합니다. 충돌 검색을 활성화하기 위한 몇 가지 옵션은 다음과 같습니다.

- 데이터베이스에 행이 변경 된 시기를 결정 하는 데 사용할 수 있는 테이블 열을 포함 합니다. 그런 다음 SQL `Update` 또는 `Delete` 명령의 `Where` 절에 해당 열을 포함 하도록 Entity Framework를 구성할 수 있습니다.

    이는 `OfficeAssignment` 테이블의 `Timestamp` 열 용도입니다.

    [![Image09](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image10.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image9.png)

    `Timestamp` 열의 데이터 형식을 `Timestamp`라고도 합니다. 그러나 열에는 실제로 날짜 또는 시간 값이 포함 되지 않습니다. 대신이 값은 행이 업데이트 될 때마다 증가 하는 일련 번호입니다. `Update` 또는 `Delete` 명령에서 `Where` 절은 원래 `Timestamp` 값을 포함 합니다. 업데이트 되는 행이 다른 사용자에 의해 변경 된 경우 `Timestamp`의 값은 원래 값과 다르므로 `Where` 절은 업데이트할 행을 반환 하지 않습니다. Entity Framework 현재 `Update` 또는 `Delete` 명령에 의해 업데이트 된 행이 없는 것을 발견 하는 경우 (즉, 영향을 받는 행의 수가 0 인 경우)이는 동시성 충돌로 해석 합니다.
- `Update` 및 `Delete` 명령의 `Where` 절에서 테이블에 있는 모든 열의 원래 값을 포함 하도록 Entity Framework를 구성 합니다.

    첫 번째 옵션에서와 같이 행을 처음 읽은 후 행의 내용이 변경 된 경우에는 `Where` 절이 업데이트할 행을 반환 하지 않습니다 .이는 Entity Framework에서 동시성 충돌로 해석 합니다. 이 메서드는 `Timestamp` 필드를 사용 하는 것과 효과적 이지만 비효율적 일 수 있습니다. 많은 열이 있는 데이터베이스 테이블의 경우 `Where` 절이 매우 클 수 있으며, 웹 응용 프로그램에서는 많은 양의 상태를 유지 관리 해야 할 수 있습니다. 많은 양의 상태를 유지 관리 하는 것은 서버 리소스 (예: 세션 상태)가 필요 하거나 웹 페이지 자체 (예: 보기 상태)에 포함 되어야 하므로 응용 프로그램 성능에 영향을 줄 수 있습니다.

이 자습서에서는 추적 속성이 없는 엔터티 (`Department` 엔터티)와 추적 속성 (`OfficeAssignment` 엔터티)이 있는 엔터티에 대 한 낙관적 동시성 충돌에 대 한 오류 처리를 추가 합니다.

## <a name="handling-optimistic-concurrency-without-a-tracking-property"></a>추적 속성 없이 낙관적 동시성 처리

추적 (`Timestamp`) 속성이 없는 `Department` 엔터티에 대해 낙관적 동시성을 구현 하려면 다음 작업을 완료 합니다.

- `Department` 엔터티에 대해 동시성 추적을 사용 하도록 데이터 모델을 변경 합니다.
- `SchoolRepository` 클래스에서 `SaveChanges` 메서드의 동시성 예외를 처리 합니다.
- 학과 페이지 *에서* 시도 된 변경이 실패 했음을 사용자 경고에 표시 하 여 동시성 예외를 처리 합니다. 사용자는 현재 값을 확인 하 고 필요한 경우 변경 내용을 다시 시도할 수 있습니다.

### <a name="enabling-concurrency-tracking-in-the-data-model"></a>데이터 모델에서 동시성 추적 사용

Visual Studio에서이 시리즈의 이전 자습서에서 작업 중인 Contoso 대학 웹 응용 프로그램을 엽니다.

*SchoolModel*를 열고 데이터 모델 디자이너에서 `Department` 엔터티의 `Name` 속성을 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다. **속성** 창에서 `ConcurrencyMode` 속성을 `Fixed`로 변경 합니다.

[![Image16](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image12.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image11.png)

기본 키가 아닌 다른 스칼라 속성 (`Budget`, `StartDate`및 `Administrator`에 대해 동일한 작업을 수행 합니다. 탐색 속성에 대해서는이 작업을 수행할 수 없습니다. 이는 Entity Framework에서 `Update`을 생성 하거나 SQL 명령을 `Delete` 여 데이터베이스의 `Department` 엔터티를 업데이트할 때마다 원래 값이 있는 열을 `Where` 절에 포함 하도록 지정 합니다. `Update` 또는 `Delete` 명령이 실행 될 때 행을 찾을 수 없는 경우 Entity Framework는 낙관적 동시성 예외를 throw 합니다.

데이터 모델을 저장 하 고 닫습니다.

### <a name="handling-concurrency-exceptions-in-the-dal"></a>DAL에서 동시성 예외 처리

*SchoolRepository.cs* 를 열고 `System.Data` 네임 스페이스에 대해 다음 `using` 문을 추가 합니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample1.cs)]

낙관적 동시성 예외를 처리 하는 다음과 같은 새 `SaveChanges` 메서드를 추가 합니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample2.cs)]

이 메서드가 호출 될 때 동시성 오류가 발생 하면 메모리에 있는 엔터티의 속성 값이 현재 데이터베이스의 값으로 바뀝니다. 웹 페이지에서 처리할 수 있도록 동시성 예외가 다시 throw 됩니다.

`DeleteDepartment` 및 `UpdateDepartment` 메서드에서 새 메서드를 호출 하기 위해 기존 `context.SaveChanges()` 호출을 `SaveChanges()`에 대 한 호출로 바꿉니다.

### <a name="handling-concurrency-exceptions-in-the-presentation-layer"></a>프레젠테이션 계층에서 동시성 예외 처리

학과 *.aspx* 를 열고 `DepartmentsObjectDataSource` 컨트롤에 `OnDeleted="DepartmentsObjectDataSource_Deleted"` 특성을 추가 합니다. 이제 컨트롤의 여는 태그는 다음 예제와 유사 하 게 됩니다.

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample3.aspx)]

다음 예제와 같이 `DepartmentsGridView` 컨트롤에서 `DataKeyNames` 특성의 모든 테이블 열을 지정 합니다. 이렇게 하면 매우 큰 뷰 상태 필드가 생성 됩니다 .이는 추적 필드를 사용 하는 것이 일반적으로 동시성 충돌을 추적 하는 기본 방법입니다.

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample4.aspx)]

*Departments.aspx.cs* 를 열고 `System.Data` 네임 스페이스에 대해 다음 `using` 문을 추가 합니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample5.cs)]

다음 새 메서드를 추가 합니다 .이 메서드는 데이터 소스 컨트롤의 `Updated`에서 호출 하 고 동시성 예외를 처리 하기 위한 이벤트 처리기를 `Deleted` 합니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample6.cs)]

이 코드는 예외 형식을 확인 하 고, 동시성 예외인 경우 코드는 `ValidationSummary` 컨트롤에 메시지를 표시 하는 `CustomValidator` 컨트롤을 동적으로 만듭니다.

이전에 추가한 `Updated` 이벤트 처리기에서 새 메서드를 호출 합니다. 또한 동일한 메서드를 호출 하지만 다른 작업은 수행 하지 않는 새 `Deleted` 이벤트 처리기를 만듭니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample7.cs)]

### <a name="testing-optimistic-concurrency-in-the-departments-page"></a>부서 페이지에서 낙관적 동시성 테스트

*부서 .aspx* 페이지를 실행 합니다.

[![Image17](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image14.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image13.png)

행에서 **편집** 을 클릭 하 고 **예산** 열에서 값을 변경 합니다. 기존 `School` 데이터베이스 레코드에 잘못 된 데이터가 포함 되어 있으므로이 자습서에 대해 만든 레코드만 편집할 수 있습니다. 경제성 부서에 대 한 레코드는 시험해 볼 수 있는 것이 안전 합니다.

[![Image18](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image16.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image15.png)

새 브라우저 창을 열고 페이지를 다시 실행 합니다. 첫 번째 브라우저 창의 주소 상자에서 두 번째 브라우저 창으로 URL을 복사 합니다.

[![Image17](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image18.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image17.png)

이전에 편집한 동일한 행에서 **편집** 을 클릭 하 고 **예산** 값을 다른 값으로 변경 합니다.

[![Image19](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image20.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image19.png)

두 번째 브라우저 창에서 **업데이트**를 클릭 합니다. **예산** 금액이이 새 값으로 변경 되었습니다.

[![Image20](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image22.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image21.png)

첫 번째 브라우저 창에서 **업데이트**를 클릭 합니다. 업데이트가 실패 합니다. 두 번째 브라우저 창에서 설정한 값을 사용 하 여 **예산** 금액이 다시 표시 되 고 오류 메시지가 표시 됩니다.

[![Image21](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image24.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image23.png)

## <a name="handling-optimistic-concurrency-using-a-tracking-property"></a>추적 속성을 사용 하 여 낙관적 동시성 처리

추적 속성이 있는 엔터티에 대 한 낙관적 동시성을 처리 하려면 다음 작업을 완료 합니다.

- 데이터 모델에 저장 프로시저를 추가 하 여 `OfficeAssignment` 엔터티를 관리 합니다. (추적 속성 및 저장 프로시저는 함께 사용할 필요가 없습니다. 여기에 설명 된 대로 함께 그룹화 됩니다.)
- DAL에서 낙관적 동시성 예외를 처리 하는 코드를 비롯 하 여 `OfficeAssignment` 엔터티에 대 한 CRUD 및 BLL에 CRUD 메서드를 추가 합니다.
- Office 할당 웹 페이지를 만듭니다.
- 새 웹 페이지에서 낙관적 동시성을 테스트 합니다.

### <a name="adding-officeassignment-stored-procedures-to-the-data-model"></a>데이터 모델에 OfficeAssignment 저장 프로시저 추가

모델 디자이너에서 *SchoolModel* 파일을 열고 디자인 화면을 마우스 오른쪽 단추로 클릭 한 다음 **데이터베이스에서 모델 업데이트**를 클릭 합니다. **데이터베이스 개체 선택** 대화 상자의 **추가** 탭에서 **저장 프로시저** 를 확장 하 고 세 개의 `OfficeAssignment` 저장 프로시저 (다음 스크린샷 참조)를 선택한 다음 **마침**을 클릭 합니다. 이러한 저장 프로시저는 스크립트를 사용 하 여 다운로드 하거나 만들 때 데이터베이스에 이미 있습니다.

[![Image02](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image26.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image25.png)

`OfficeAssignment` 엔터티를 마우스 오른쪽 단추로 클릭 하 고 **저장 프로시저 매핑**을 선택 합니다.

[![Image03](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image28.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image27.png)

해당 저장 프로시저를 사용 하도록 **Insert**, **Update**및 **Delete** 함수를 설정 합니다. `Update` 함수의 `OrigTimestamp` 매개 변수에 대해 **속성** 을 `Timestamp`로 설정 하 고 **원래 값 사용** 옵션을 선택 합니다.

[![Image04](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image30.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image29.png)

Entity Framework `UpdateOfficeAssignment` 저장 프로시저를 호출 하면 `OrigTimestamp` 매개 변수에 `Timestamp` 열의 원래 값이 전달 됩니다. 저장 프로시저는 `Where` 절에서이 매개 변수를 사용 합니다.

[!code-sql[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample8.sql)]

또한 저장 프로시저는 업데이트 후에 `Timestamp` 열의 새 값을 선택 하 여 Entity Framework 메모리에 있는 `OfficeAssignment` 엔터티를 해당 데이터베이스 행과 동기화 상태로 유지할 수 있도록 합니다.

사무실 할당을 삭제 하는 저장 프로시저에는 `OrigTimestamp` 매개 변수가 없습니다. 따라서 Entity Framework 엔터티를 삭제 하기 전에 변경 되지 않은 것으로 확인할 수 없습니다.)

데이터 모델을 저장 하 고 닫습니다.

### <a name="adding-officeassignment-methods-to-the-dal"></a>DAL에 OfficeAssignment 메서드 추가

*ISchoolRepository.cs* 를 열고 `OfficeAssignment` 엔터티 집합에 대해 다음과 같은 CRUD 메서드를 추가 합니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample9.cs)]

*SchoolRepository.cs*에 다음과 같은 새 메서드를 추가 합니다. `UpdateOfficeAssignment` 메서드에서는 `context.SaveChanges`대신 로컬 `SaveChanges` 메서드를 호출 합니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample10.cs)]

테스트 프로젝트에서 *MockSchoolRepository.cs* 를 열고 다음 `OfficeAssignment` COLLECTION 및 CRUD 메서드를 추가 합니다. (모의 리포지토리는 리포지토리 인터페이스를 구현 해야 합니다. 그렇지 않으면 솔루션이 컴파일되지 않습니다.)

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample11.cs)]

### <a name="adding-officeassignment-methods-to-the-bll"></a>OfficeAssignment 메서드를 BLL에 추가

주 프로젝트에서 *SchoolBL.cs* 를 열고 `OfficeAssignment` 엔터티 집합에 대해 다음과 같은 CRUD 메서드를 추가 합니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample12.cs)]

## <a name="creating-an-officeassignments-web-page"></a>OfficeAssignments 웹 페이지 만들기

*Site.master* 마스터 페이지를 사용 하는 새 웹 페이지를 만들고 이름을 *OfficeAssignments*로 다시 만듭니다. `Content2`이라는 `Content` 컨트롤에 다음 태그를 추가 합니다.

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample13.aspx)]

`DataKeyNames` 특성에서 태그는 `Timestamp` 속성 뿐만 아니라 레코드 키 (`InstructorID`)를 지정 합니다. `DataKeyNames` 특성에 속성을 지정 하면 컨트롤이 다시 게시 처리 중에 원래 값을 사용할 수 있도록 컨트롤 상태 (뷰 상태와 유사)로 저장 됩니다.

`Timestamp` 값을 저장 하지 않은 경우 Entity Framework는 SQL `Update` 명령의 `Where` 절에 대해이 값을 포함 하지 않습니다. 따라서 업데이트할 항목이 없습니다. 따라서 Entity Framework `OfficeAssignment` 엔터티가 업데이트 될 때마다 낙관적 동시성 예외를 throw 합니다.

*OfficeAssignments.aspx.cs* 를 열고 데이터 액세스 계층에 대해 다음 `using` 문을 추가 합니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample14.cs)]

Dynamic Data 기능을 사용할 수 있는 다음 `Page_Init` 메서드를 추가 합니다. 또한 동시성 오류를 확인 하기 위해 `ObjectDataSource` 컨트롤의 `Updated` 이벤트에 대해 다음 처리기를 추가 합니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample15.cs)]

### <a name="testing-optimistic-concurrency-in-the-officeassignments-page"></a>OfficeAssignments 페이지에서 낙관적 동시성 테스트

*OfficeAssignments* 페이지를 실행 합니다.

[![Image10](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image32.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image31.png)

행에서 **편집** 을 클릭 하 고 **위치** 열에서 값을 변경 합니다.

[![Image11](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image34.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image33.png)

새 브라우저 창을 열고 페이지를 다시 실행 합니다. 첫 번째 브라우저 창에서 두 번째 브라우저 창으로 URL을 복사 합니다.

[![Image10](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image36.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image35.png)

이전에 편집한 동일한 행에서 **편집** 을 클릭 하 고 **위치** 값을 다른 값으로 변경 합니다.

[![Image12](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image38.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image37.png)

두 번째 브라우저 창에서 **업데이트**를 클릭 합니다.

[![Image13](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image40.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image39.png)

첫 번째 브라우저 창으로 전환 하 고 **업데이트**를 클릭 합니다.

[![Image15](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image42.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image41.png)

오류 메시지가 표시 되 고 **위치** 값이 업데이트 되어 두 번째 브라우저 창에서 변경한 값을 표시 합니다.

## <a name="handling-concurrency-with-the-entitydatasource-control"></a>EntityDataSource 컨트롤을 사용 하 여 동시성 처리

`EntityDataSource` 컨트롤은 데이터 모델의 동시성 설정을 인식 하 고 업데이트 및 삭제 작업을 적절 하 게 처리 하는 기본 제공 논리를 포함 합니다. 그러나 모든 예외와 마찬가지로 사용자에 게 친숙 한 오류 메시지를 제공 하기 위해 `OptimisticConcurrencyException` 예외를 직접 처리 해야 합니다.

다음으로 `EntityDataSource` 컨트롤을 사용 하는 *강의* 페이지를 구성 하 여 업데이트 및 삭제 작업을 허용 하 고 동시성 충돌이 발생 하는 경우 오류 메시지를 표시 합니다. `Course` 엔터티에는 동시성 추적 열이 없으므로 `Department` 엔터티를 사용 하 여 수행한 것과 동일한 메서드를 사용 합니다. 키가 아닌 모든 속성의 값을 추적 합니다.

*SchoolModel* 파일을 엽니다. `Course` 엔터티의 키가 아닌 속성 (`Title`, `Credits`및 `DepartmentID`)에 대해 **동시성 모드** 속성을 `Fixed`로 설정 합니다. 그런 다음 데이터 모델을 저장 하 고 닫습니다.

*Default.aspx* 페이지를 열고 다음과 같이 변경 합니다.

- `CoursesEntityDataSource` 컨트롤에서 `EnableUpdate="true"` 및 `EnableDelete="true"` 특성을 추가 합니다. 이제 해당 컨트롤의 여는 태그는 다음 예제와 유사 합니다.

    [!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample16.aspx)]
- `CoursesGridView` 컨트롤에서 `DataKeyNames` 특성 값을 `"CourseID,Title,Credits,DepartmentID"`로 변경 합니다. 그런 다음 **편집** 및 **삭제** 단추 (`<asp:CommandField ShowEditButton="True" ShowDeleteButton="True" />`)를 표시 하는 `Columns` 요소에 `CommandField` 요소를 추가 합니다. 이제 `GridView` 컨트롤은 다음 예제와 유사 합니다.

    [!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample17.aspx)]

페이지를 실행 하 고 부서 페이지에서 수행한 것과 같은 충돌 상황을 만듭니다. 두 브라우저 창에서 페이지를 실행 하 고, 각 창의 같은 줄에서 **편집** 을 클릭 하 고, 각 창에서 다른 변경을 수행 합니다. 한 창에서 **업데이트** 를 클릭 한 다음 다른 창에서 **업데이트** 를 클릭 합니다. **업데이트** 를 두 번 클릭 하면 처리 되지 않은 동시성 예외로 인해 발생 하는 오류 페이지가 표시 됩니다.

[![Image22](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image44.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image43.png)

이 오류는 `ObjectDataSource` 컨트롤에 대해 처리 하는 방법과 매우 비슷한 방식으로 처리 됩니다. *Default.aspx* 페이지를 열고 `CoursesEntityDataSource` 컨트롤에서 `Deleted` 및 `Updated` 이벤트에 대 한 처리기를 지정 합니다. 이제 컨트롤의 여는 태그는 다음 예제와 유사 합니다.

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample18.aspx)]

`CoursesGridView` 컨트롤 전에 다음 `ValidationSummary` 컨트롤을 추가 합니다.

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample19.aspx)]

*Courses.aspx.cs*에서 `System.Data` 네임 스페이스에 대 한 `using` 문을 추가 하 고, 동시성 예외를 확인 하는 메서드를 추가 하 고, `EntityDataSource` 컨트롤의 `Updated` 및 `Deleted` 처리기에 대 한 처리기를 추가 합니다. 코드는 다음과 같습니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample20.cs)]

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample21.cs)]

이 코드와 `ObjectDataSource` 컨트롤에 대해 수행한 작업의 차이점은이 경우 동시성 예외는 해당 예외의 `InnerException` 속성이 아닌 이벤트 인수 개체의 `Exception` 속성에 있다는 것입니다.

페이지를 실행 하 고 동시성 충돌을 다시 만듭니다. 이번에는 다음과 같은 오류 메시지가 표시 됩니다.

[![Image23](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image46.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image45.png)

동시성 충돌 처리에 대한 소개를 완료합니다. 다음 자습서에서는 Entity Framework를 사용 하는 웹 응용 프로그램의 성능을 향상 시키는 방법에 대 한 지침을 제공 합니다.

> [!div class="step-by-step"]
> [이전](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering.md)
> [다음](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)
