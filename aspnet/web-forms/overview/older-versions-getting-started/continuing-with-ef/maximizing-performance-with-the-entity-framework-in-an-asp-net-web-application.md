---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application
title: ASP.NET 4 웹 응용 프로그램에서 Entity Framework 4.0를 사용 하 여 성능 최대화 | Microsoft Docs
author: tdykstra
description: 이 자습서 시리즈는 Entity Framework 4.0 자습서 시리즈 시작에서 만든 Contoso 대학 웹 응용 프로그램을 기반으로 합니다. I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 4e43455e-dfa1-42db-83cb-c987703f04b5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application
msc.type: authoredcontent
ms.openlocfilehash: 5630200a1ad1d30f6d89b38e15179f15b699fa9f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78439265"
---
# <a name="maximizing-performance-with-the-entity-framework-40-in-an-aspnet-4-web-application"></a>ASP.NET 4 웹 응용 프로그램에서 Entity Framework 4.0를 사용 하 여 성능 최대화

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

> 이 자습서 시리즈는 [Entity Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started) 자습서 시리즈 시작에서 만든 Contoso 대학 웹 응용 프로그램을 기반으로 합니다. 이전 자습서를 완료 하지 않은 경우이 자습서의 시작 점으로, 만든 [응용 프로그램을 다운로드할](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) 수 있습니다. 전체 자습서 시리즈에서 만든 [응용 프로그램을 다운로드할](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) 수도 있습니다. 자습서에 대 한 질문이 있는 경우 [ASP.NET Entity Framework 포럼](https://forums.asp.net/1227.aspx)에 게시할 수 있습니다.

이전 자습서에서 동시성 충돌을 처리 하는 방법을 살펴보았습니다. 이 자습서에서는 Entity Framework를 사용 하는 ASP.NET 웹 응용 프로그램의 성능을 향상 시키기 위한 옵션을 보여 줍니다. 성능을 최대화 하거나 성능 문제를 진단 하기 위한 몇 가지 방법을 알아봅니다.

다음 섹션에 나와 있는 정보는 다양 한 시나리오에서 유용할 수 있습니다.

- 관련 데이터를 효율적으로 로드 합니다.
- 뷰 상태를 관리 합니다.

다음 섹션에 나와 있는 정보는 성능 문제를 발생 시키는 개별 쿼리가 있는 경우에 유용할 수 있습니다.

- `NoTracking` 병합 옵션을 사용 합니다.
- LINQ 쿼리를 미리 컴파일합니다.
- 데이터베이스에 전송 된 쿼리 명령을 검사 합니다.

다음 섹션에 나와 있는 정보는 매우 큰 데이터 모델을 가진 응용 프로그램에 유용할 수 있습니다.

- 뷰를 미리 생성 합니다.

> [!NOTE]
> 웹 응용 프로그램 성능에는 요청 및 응답 데이터의 크기, 데이터베이스 쿼리의 속도, 서버에서 큐에 대기 시킬 수 있는 요청 수, 서비스의 효율성 등 여러 가지 요소가 영향을 받습니다. 클라이언트 스크립트 라이브러리를 사용 하 고 있을 수 있습니다. 응용 프로그램에서 성능이 중요 한 경우 또는 테스트 또는 환경에서 응용 프로그램 성능이 만족 스 럽 지 않은 것으로 표시 되는 경우 성능 조정을 위해 일반 프로토콜을 따라야 합니다. 측정 하 여 성능 병목 현상이 발생 하는 위치를 확인 한 다음 전체 응용 프로그램 성능에 가장 큰 영향을 줄 수 있는 영역을 해결 합니다.
> 
> 이 항목에서는 ASP.NET에서 특히 Entity Framework의 성능을 향상 시킬 수 있는 방법에 중점을 둘 수 있습니다. 이 제안 사항은 데이터 액세스가 응용 프로그램의 성능 병목 현상 중 하나 인지 확인 하는 경우에 유용 합니다. 설명 된 경우를 제외 하 고, 여기에 설명 된 메서드는 일반적으로&quot; &quot;모범 사례에 따라 고려 하지 않아야 합니다. 대부분은 예외적인 상황 에서만 적절 하거나 특정 유형의 성능 병목 현상을 해결할 수 있습니다.

자습서를 시작 하려면 Visual Studio를 시작 하 고 이전 자습서에서 작업 하 던 Contoso 대학 웹 응용 프로그램을 엽니다.

## <a name="efficiently-loading-related-data"></a>효율적으로 관련 데이터 로드

Entity Framework는 엔터티의 탐색 속성에 관련 데이터를 로드할 수 있는 여러 가지 방법이 있습니다.

- *지연 로드*. 엔터티를 처음 읽을 때 관련된 데이터가 검색되지 않습니다. 그러나 탐색 속성에 처음으로 액세스하려고 할 때 해당 탐색 속성에 필요한 데이터가 자동으로 검색됩니다. 이렇게 하면 여러 개의 쿼리가 데이터베이스에 전송 됩니다. 하나는 엔터티 자체를 위한 것이 고 다른 하나는 엔터티에 대 한 관련 데이터를 검색 해야 하는 경우입니다. 

    [![Image05](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image2.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image1.png)

*즉시 로드*. 엔터티를 읽을 때 관련된 데이터가 함께 검색됩니다. 이는 일반적으로 필요한 데이터를 모두 검색하는 단일 조인 쿼리를 발생시킵니다. 이러한 자습서에서 살펴본 것 처럼 `Include` 메서드를 사용 하 여 즉시 로드를 지정 합니다.

[![Image07](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image4.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image3.png)

- *명시적 로드*. 코드에서 관련 데이터를 명시적으로 검색 하는 경우를 제외 하 고는 지연 로드와 비슷합니다. 탐색 속성에 액세스 하는 경우 자동으로 발생 하지 않습니다. 컬렉션에 대 한 탐색 속성의 `Load` 메서드를 사용 하 여 관련 데이터를 수동으로 로드 하거나, 단일 개체를 포함 하는 속성에 대 한 참조 속성의 `Load` 메서드를 사용 합니다. 예를 들어 `PersonReference.Load` 메서드를 호출 하 여 `Department` 엔터티의 `Person` 탐색 속성을 로드 합니다.

    [![Image06](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image6.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image5.png)

속성 값을 즉시 검색 하지 않으므로 지연 로드 및 명시적 로드도 모두 *지연 된 로드*라고도 합니다.

지연 로드는 디자이너가 생성 한 개체 컨텍스트의 기본 동작입니다. 개체 컨텍스트 클래스를 정의 하는 *SchoolModel.Designer.cs* 파일을 여는 경우 세 가지 생성자 메서드를 찾을 수 있으며 각 메서드는 다음 문을 포함 합니다.

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample1.cs)]

일반적으로 검색 되는 모든 엔터티에 대 한 관련 데이터가 필요 하다는 것을 알고 있는 경우 데이터베이스에 전송 되는 단일 쿼리가 검색 된 각 엔터티에 대 한 별도의 쿼리 보다 더 효율적 이기 때문에 즉시 로드는 최상의 성능을 제공 합니다. 반면, 엔터티 탐색 속성에 자주 액세스 하거나 작은 엔터티 집합에 대해서만 액세스 해야 하는 경우 즉시 로드는 필요한 것 보다 더 많은 데이터를 검색 하기 때문에 지연 로드 또는 명시적 로드가 더 효율적일 수 있습니다.

웹 응용 프로그램에서는 페이지를 렌더링 하는 개체 컨텍스트에 대 한 연결이 없는 브라우저에서 관련 데이터의 필요성에 영향을 주는 사용자 작업이 발생 하기 때문에 지연 로드는 상대적으로 작은 값일 수 있습니다. 반면, 컨트롤의 데이터를 데이터 바인딩할 때 일반적으로 필요한 데이터를 알고 있으므로 일반적으로 각 시나리오의 적절 한 사항에 따라 즉시 로드 또는 지연 된 로드를 선택 하는 것이 좋습니다.

또한 개체 컨텍스트를 삭제 한 후에는 데이터 바인딩된 컨트롤이 엔터티 개체를 사용할 수 있습니다. 이 경우 탐색 속성을 지연 로드 하려는 시도가 실패 합니다. 표시 되는 오류 메시지는 다음과 같습니다. &quot;`The ObjectContext instance has been disposed and can no longer be used for operations that require a connection.`&quot;

`EntityDataSource` 컨트롤은 기본적으로 지연 로드를 사용 하지 않도록 설정 합니다. 현재 자습서에 사용 하는 `ObjectDataSource` 컨트롤 또는 페이지 코드에서 개체 컨텍스트에 액세스 하는 경우 여러 가지 방법으로 지연 로드를 기본적으로 사용 하지 않도록 설정할 수 있습니다. 개체 컨텍스트를 인스턴스화할 때 사용 하지 않도록 설정할 수 있습니다. 예를 들어 `SchoolRepository` 클래스의 생성자 메서드에 다음 줄을 추가할 수 있습니다.

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample2.cs)]

Contoso 대학 응용 프로그램의 경우 컨텍스트를 인스턴스화할 때마다이 속성을 설정할 필요가 없도록 개체 컨텍스트를 지연 로드를 자동으로 사용 하지 않도록 설정 합니다.

*SchoolModel* 데이터 모델을 열고 디자인 화면을 클릭 한 다음 속성 창에서 **지연 로드 설정** 속성을 `False`로 설정 합니다. 데이터 모델을 저장 하 고 닫습니다.

[![Image04](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image8.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image7.png)

## <a name="managing-view-state"></a>뷰 상태 관리

업데이트 기능을 제공 하기 위해 페이지를 렌더링할 때 ASP.NET 웹 페이지에서 엔터티의 원래 속성 값을 저장 해야 합니다. 포스트백 처리 중에 컨트롤은 엔터티의 원래 상태를 다시 만들고 변경 내용을 적용 하 고 `SaveChanges` 메서드를 호출 하기 전에 엔터티의 `Attach` 메서드를 호출할 수 있습니다. 기본적으로 ASP.NET Web Forms 데이터 컨트롤은 뷰 상태를 사용 하 여 원래 값을 저장 합니다. 그러나 뷰 상태는 브라우저에서 보내고 받는 페이지의 크기를 크게 늘릴 수 있는 숨겨진 필드에 저장 되기 때문에 성능에 영향을 줄 수 있습니다.

뷰 상태 또는 세션 상태와 같은 대안을 관리 하는 기술은 Entity Framework에 고유 하지 않으므로이 자습서에서는이 항목에 대해 자세히 설명 하지 않습니다. 자세한 내용은 자습서 끝에 있는 링크를 참조 하세요.

그러나 ASP.NET 버전 4는 모든 ASP.NET 응용 프로그램 개발자 Web Forms가 `ViewStateMode` 속성을 인식 해야 하는 뷰 상태를 사용 하는 새로운 방법을 제공 합니다. 이 새로운 속성은 페이지나 컨트롤 수준에서 설정 될 수 있으며, 페이지에 대해 기본적으로 뷰 상태를 사용 하지 않도록 설정 하 고 필요한 컨트롤에 대해서만 사용 하도록 설정할 수 있습니다.

성능이 중요 한 응용 프로그램의 경우 페이지 수준에서 항상 보기 상태를 사용 하지 않도록 설정 하 고이를 필요로 하는 컨트롤에 대해서만 사용 하도록 설정 하는 것이 좋습니다. Contoso 대학 페이지의 보기 상태 크기는이 방법으로 크게 감소 하지는 않지만 어떻게 작동 하는지 확인 하기 위해 *강사 .aspx* 페이지에 대해이 작업을 수행 합니다. 이 페이지에는 뷰 상태가 사용 하지 않도록 설정 된 `Label` 컨트롤을 포함 하 여 많은 컨트롤이 포함 되어 있습니다. 이 페이지의 컨트롤은 실제로 보기 상태를 사용 하도록 설정 하지 않아도 됩니다. `GridView` 컨트롤의 `DataKeyNames` 속성은 다시 게시 간에 유지 해야 하는 상태를 지정 하지만 이러한 값은 `ViewStateMode` 속성의 영향을 받지 않는 컨트롤 상태에 유지 됩니다.

현재 `Page` 지시문 및 `Label` 컨트롤 태그는 다음 예제와 비슷합니다.

[!code-aspx[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample3.aspx)]

다음과 같이 변경합니다.

- `Page` 지시문에 `ViewStateMode="Disabled"`를 추가 합니다.
- `Label` 컨트롤에서 `ViewStateMode="Disabled"`를 제거 합니다.

이제 태그는 다음 예제와 유사 합니다.

[!code-aspx[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample4.aspx)]

이제 모든 컨트롤에서 뷰 상태를 사용할 수 없습니다. 나중에 뷰 상태를 사용 해야 하는 컨트롤을 추가 하는 경우 해당 컨트롤에 대 한 `ViewStateMode="Enabled"` 특성만 포함 하기만 하면 됩니다.

## <a name="using-the-notracking-merge-option"></a>NoTracking Merge 옵션 사용

개체 컨텍스트가 데이터베이스 행을 검색 하 고이를 나타내는 엔터티 개체를 만드는 경우 기본적으로 해당 개체 상태 관리자를 사용 하 여 해당 엔터티 개체도 추적 합니다. 이 추적 데이터는 캐시 역할을 하며 엔터티를 업데이트할 때 사용 됩니다. 웹 응용 프로그램에는 일반적으로 수명이 짧은 개체 컨텍스트 인스턴스가 있기 때문에 쿼리는 추적 하지 않아도 되는 데이터를 반환 하는 경우가 많습니다. 이러한 데이터는이를 읽는 엔터티가 다시 사용 되거나 업데이트 되기 전에 삭제 됩니다.

Entity Framework에서 *병합 옵션*을 설정 하 여 개체 컨텍스트에서 엔터티 개체를 추적할지 여부를 지정할 수 있습니다. 개별 쿼리 또는 엔터티 집합에 대 한 병합 옵션을 설정할 수 있습니다. 엔터티 집합에 대해이 옵션을 설정 하는 경우 해당 엔터티 집합에 대해 생성 된 모든 쿼리에 대해 기본 병합 옵션을 설정 하는 것입니다.

Contoso 대학 응용 프로그램의 경우 리포지토리에 액세스 하는 엔터티 집합에는 추적이 필요 하지 않으므로 리포지토리 클래스에서 개체 컨텍스트를 인스턴스화할 때 이러한 엔터티 집합에 대 한 `NoTracking` 병합 옵션을 설정할 수 있습니다. 이 자습서에서는 병합 옵션을 설정 하는 것이 응용 프로그램의 성능에 크게 영향을 주지 않습니다. `NoTracking` 옵션은 특정 대량 볼륨 시나리오 에서만 예측 가능한 성능을 향상 시킬 수 있습니다.

DAL 폴더에서 *SchoolRepository.cs* 파일을 열고 리포지토리가 액세스 하는 엔터티 집합에 대 한 병합 옵션을 설정 하는 생성자 메서드를 추가 합니다.

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample5.cs)]

## <a name="pre-compiling-linq-queries"></a>LINQ 쿼리 미리 컴파일

Entity Framework에서 지정 된 `ObjectContext` 인스턴스 수명 내에 Entity SQL 쿼리를 처음 실행 하면 쿼리를 컴파일하는 데 약간의 시간이 걸립니다. 컴파일의 결과가 캐시 됩니다. 즉, 이후의 쿼리 실행이 훨씬 빨라집니다. LINQ 쿼리는 쿼리가 실행 될 때마다 쿼리를 컴파일하는 데 필요한 일부 작업을 수행 한다는 점을 제외 하 고 비슷한 패턴을 따릅니다. 즉, LINQ 쿼리의 경우에는 기본적으로 컴파일 결과가 모두 캐시 되지 않습니다.

개체 컨텍스트 수명 동안 반복적으로 실행 해야 하는 LINQ 쿼리가 있는 경우 LINQ 쿼리가 처음 실행 될 때 컴파일 결과가 모두 캐시 되도록 하는 코드를 작성할 수 있습니다.

이에 대 한 설명으로, `SchoolRepository` 클래스의 두 가지 `Get` 메서드에 대해이 작업을 수행 합니다. 그 중 하나는 매개 변수 (`GetInstructorNames` 메서드)를 사용 하지 않고 다른 하나는 매개 변수 (`GetDepartmentsByAdministrator` 메서드)를 필요로 합니다. 이러한 메서드는 이제는 LINQ 쿼리가 아니기 때문에 실제로 컴파일할 필요가 없습니다.

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample6.cs)]

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample7.cs)]

그러나 컴파일된 쿼리를 사용해 볼 수 있도록 다음 LINQ 쿼리로 작성 된 것 처럼 계속 진행 합니다.

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample8.cs)]

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample9.cs)]

이러한 메서드의 코드를 위에 표시 된 내용으로 변경 하 고 응용 프로그램을 실행 하 여 계속 하기 전에 작동 하는지 확인할 수 있습니다. 그러나 다음 지침에서는 미리 컴파일된 버전의를 직접 만듭니다.

*DAL* 폴더에 클래스 파일을 만들고 이름을 *SchoolEntities.cs*로 바꾸고 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample10.cs)]

이 코드는 자동으로 생성 된 개체 컨텍스트 클래스를 확장 하는 partial 클래스를 만듭니다. Partial 클래스는 `CompiledQuery` 클래스의 `Compile` 메서드를 사용 하 여 컴파일된 두 LINQ 쿼리를 포함 합니다. 또한 쿼리를 호출 하는 데 사용할 수 있는 메서드를 만듭니다. 이 파일을 저장 하 고 닫습니다.

그런 다음 *SchoolRepository.cs*에서 컴파일된 쿼리를 호출 하도록 리포지토리 클래스의 기존 `GetInstructorNames` 및 `GetDepartmentsByAdministrator` 메서드를 변경 합니다.

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample11.cs)]

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample12.cs)]

학과 페이지 *를 실행 하 여 이전과* 동일한 방식으로 작동 하는지 확인 합니다. `GetInstructorNames` 메서드는 관리자 드롭다운 목록을 채우기 위해 호출 되며, **업데이트** 를 클릭 하 여 두 개 이상의 부서에 대 한 관리자가 없는지 확인 하기 위해 `GetDepartmentsByAdministrator` 메서드가 호출 됩니다.

[![Image03](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image10.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image9.png)

이 작업을 수행 하는 방법을 확인 하기 위해 Contoso 대학 응용 프로그램의 쿼리는 미리 컴파일되어 성능이 크게 성능이 향상 되지 않습니다. LINQ 쿼리를 미리 컴파일하면 코드에 복잡성 수준이 추가 되므로 실제로 응용 프로그램에서 성능 병목 현상을 나타내는 쿼리에만이 작업을 수행 해야 합니다.

## <a name="examining-queries-sent-to-the-database"></a>데이터베이스로 전송 된 쿼리 검사

성능 문제를 조사할 때 Entity Framework는 데이터베이스에 전송 하는 정확한 SQL 명령을 파악 하는 것이 도움이 될 수 있습니다. `IQueryable` 개체로 작업 하는 경우이 작업을 수행 하는 한 가지 방법은 `ToTraceString` 메서드를 사용 하는 것입니다.

*SchoolRepository.cs*에서 다음 예제와 일치 하도록 `GetDepartmentsByName` 메서드의 코드를 변경 합니다.

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample13.cs)]

이전 줄의 끝에 있는 `Where` 메서드가 `IQueryable` 개체를 만들기 때문에 `departments` 변수를 `ObjectQuery` 형식으로 캐스팅 해야 합니다. `Where` 메서드가 없으면 캐스트가 필요 하지 않습니다.

`return` 줄에 중단점을 설정한 다음 디버거의 *.aspx* 페이지를 실행 합니다. 중단점에 도달 하면 **지역** 창에서 `commandText` 변수를 검사 하 고 텍스트 시각화 도우미 ( **값** 열의 돋보기)를 사용 하 여 **텍스트 시각화 도우미** 창에 해당 값을 표시 합니다. 이 코드의 결과로 생성 되는 전체 SQL 명령을 볼 수 있습니다.

[![Image08](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image12.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image11.png)

또는 Visual Studio Ultimate의 IntelliTrace 기능을 통해 코드를 변경 하거나 중단점을 설정 하지 않아도 되는 Entity Framework에서 생성 된 SQL 명령을 볼 수 있습니다.

> [!NOTE]
> Visual Studio Ultimate 경우에만 다음 절차를 수행할 수 있습니다.

`GetDepartmentsByName` 메서드에서 원래 코드를 복원한 다음 디버거의 *.aspx* 페이지를 실행 합니다.

Visual Studio에서 **디버그** 메뉴, **Intellitrace**, **intellitrace 이벤트**를 차례로 선택 합니다.

[![Image11](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image14.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image13.png)

**IntelliTrace** 창에서 **모두 중단**을 클릭 합니다.

[![Image12](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image16.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image15.png)

**IntelliTrace** 창에는 최근 이벤트의 목록이 표시 됩니다.

[![Image09](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image18.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image17.png)

**ADO.NET** 줄을 클릭 합니다. 확장 하 여 명령 텍스트를 표시 합니다.

[![Image10](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image20.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image19.png)

전체 명령 텍스트 문자열을 **로컬** 창에서 클립보드에 복사할 수 있습니다.

간단한 `School` 데이터베이스 보다 많은 테이블, 관계 및 열이 포함 된 데이터베이스를 사용 하 고 있다고 가정 합니다. 여러 `Join` 절을 포함 하는 단일 `Select` 문에 필요한 모든 정보를 수집 하는 쿼리가 너무 복잡 하 여 효율적으로 작업할 수 없는 경우가 있습니다. 이 경우 즉시 로드에서 명시적 로드로 전환 하 여 쿼리를 단순화할 수 있습니다.

예를 들어 *SchoolRepository.cs*의 `GetDepartmentsByName` 메서드에서 코드를 변경해 봅니다. 현재이 메서드는 `Person`에 대 한 `Include` 메서드와 탐색 속성을 `Courses` 하는 개체 쿼리가 있습니다. 다음 예제와 같이 `return` 문을 명시적 로드를 수행 하는 코드로 바꿉니다.

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample14.cs)]

디버거에서 학과 *페이지를* 실행 하 고 이전과 같은 방법으로 **IntelliTrace** 창을 다시 확인 합니다. 이전에는 단일 쿼리를 수행 하는 위치에 대 한 자세한 시퀀스가 표시 됩니다.

[![Image13](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image22.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image21.png)

첫 번째 **ADO.NET** 줄을 클릭 하 여 앞에서 본 복잡 한 쿼리에 대 한 변경 내용을 확인 합니다.

[![Image14](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image24.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image23.png)

부서에서 쿼리는 `Join` 절을 사용 하지 않는 간단한 `Select` 쿼리가 되었지만 그 다음에는 원래 쿼리에서 반환 된 각 부서에 대해 두 개의 쿼리 집합을 사용 하 여 관련 과정 및 관리자를 검색 하는 별도의 쿼리가 적용 됩니다.

> [!NOTE]
> 지연 로드를 사용 하는 경우 여기에 표시 되는 패턴은 동일한 쿼리를 여러 번 반복 하 여 지연 로드로 인해 발생할 수 있습니다. 일반적으로 사용 하지 않으려는 패턴은 기본 테이블의 모든 행에 대 한 지연 로드 관련 데이터입니다. 단일 조인 쿼리가 너무 복잡 한 것을 확인 하지 않은 경우에는 일반적으로 즉시 로드를 사용 하도록 기본 쿼리를 변경 하 여 성능을 향상 시킬 수 있습니다.

## <a name="pre-generating-views"></a>미리 생성 된 뷰

새 응용 프로그램 도메인에서 `ObjectContext` 개체를 처음 만들 때 Entity Framework는 데이터베이스에 액세스 하는 데 사용 하는 클래스 집합을 생성 합니다. 이러한 클래스를 *뷰*라고 하며, 데이터 모델이 매우 큰 경우 이러한 뷰를 생성 하면 새 응용 프로그램 도메인이 초기화 된 후에 페이지에 대 한 첫 번째 요청에 대 한 웹 사이트의 응답이 지연 될 수 있습니다. 런타임 대신 컴파일 시간에 뷰를 만들어이 첫 번째 요청 지연을 줄일 수 있습니다.

> [!NOTE]
> 응용 프로그램에 매우 큰 데이터 모델이 없거나 큰 데이터 모델이 있지만 IIS를 재활용 하 고 첫 번째 페이지 요청에만 영향을 주는 성능 문제를 걱정 하지 않는 경우이 섹션을 건너뛸 수 있습니다. 뷰가 응용 프로그램 도메인에 캐시 되기 때문에 `ObjectContext` 개체를 인스턴스화할 때마다 뷰 만들기가 발생 하지 않습니다. 따라서 IIS에서 응용 프로그램을 자주 재활용 하지 않는 한 페이지 요청 수가 너무 적으면 미리 생성 된 뷰에서 이점을 누릴 수 있습니다.

*Edmgen.exe* 명령줄 도구를 사용 하거나 *텍스트 템플릿 변환 도구 키트* (T4) 템플릿을 사용 하 여 뷰를 미리 생성할 수 있습니다. 이 자습서에서는 T4 템플릿을 사용 합니다.

*DAL* 폴더에서 **텍스트 템플릿** 템플릿을 사용 하 여 파일을 추가 하 고 ( **설치 된 템플릿** 목록의 **일반** 노드 아래에 있는) 이름을 *SchoolModel.Views.tt*로 표시 합니다. 파일의 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample15.cs)]

이 코드는 템플릿과 동일한 폴더에 있으며 템플릿 파일과 이름이 같은 *.edmx* 파일에 대 한 뷰를 생성 합니다. 예를 들어 템플릿 파일의 이름이 *SchoolModel.Views.tt*인 경우 *SchoolModel*라는 데이터 모델 파일이 검색 됩니다.

파일을 저장 한 다음 **솔루션 탐색기** 파일을 마우스 오른쪽 단추로 클릭 하 고 **사용자 지정 도구 실행**을 선택 합니다.

[![Image02](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image26.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image25.png)

Visual Studio는 템플릿을 기반으로 하는 *SchoolModel.Views.cs* 라는 뷰를 만드는 코드 파일을 생성 합니다. 템플릿 파일을 저장 하는 즉시 **사용자 지정 도구 실행**을 선택 하기 전에 코드 파일이 생성 되었다는 것을 알 수 있습니다.

[![Image01](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image28.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image27.png)

이제 응용 프로그램을 실행 하 고 이전과 같은 방식으로 작동 하는지 확인할 수 있습니다.

미리 생성 된 뷰에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- 방법: MSDN 웹 사이트에서 [뷰를 미리 생성 하 여 쿼리 성능 향상](https://msdn.microsoft.com/library/bb896240.aspx) `EdmGen.exe` 명령줄 도구를 사용 하 여 뷰를 미리 생성 하는 방법에 대해 설명 합니다.
- Windows Server AppFabric Customer Advise 팀 블로그의 [Entity Framework 4에서 미리 컴파일된/미리 생성 된 뷰로 성능을 격리](https://blogs.msdn.com/b/appfabriccat/archive/2010/08/06/isolating-performance-with-precompiled-pre-generated-views-in-the-entity-framework-4.aspx) 합니다.

이렇게 하면 Entity Framework를 사용 하는 ASP.NET 웹 응용 프로그램의 성능 향상에 대 한 소개를 완료 합니다. 자세한 내용은 다음 리소스를 참조하세요.

- MSDN 웹 사이트의 [성능 고려 사항 (Entity Framework)](https://msdn.microsoft.com/library/cc853327.aspx)
- [Entity Framework 팀 블로그의 성능 관련 게시물](https://blogs.msdn.com/b/adonet/archive/tags/performance/)입니다.
- [EF 병합 옵션 및 컴파일된 쿼리](https://blogs.msdn.com/b/dsimmons/archive/2010/01/12/ef-merge-options-and-compiled-queries.aspx) `NoTracking`와 같은 컴파일된 쿼리 및 병합 옵션의 예기치 않은 동작을 설명 하는 블로그 게시물입니다. 컴파일된 쿼리를 사용 하거나 응용 프로그램의 병합 옵션 설정을 조작 하려는 경우이를 먼저 읽어 보십시오.
- [데이터 및 모델링 고객 자문 팀 블로그의 Entity Framework 관련 게시물](https://blogs.msdn.com/b/dmcat/archive/tags/entity+framework/)입니다. 컴파일된 쿼리에 대 한 게시를 포함 하 고 Visual Studio 2010 Profiler를 사용 하 여 성능 문제를 검색 합니다.
- [매우 복잡 한 쿼리의 성능을 개선 하는 방법에 대 한 조언을 포함 하는 포럼 스레드를 Entity Framework](https://social.msdn.microsoft.com/Forums/adodotnetentityframework/thread/ffe8b2ab-c5b5-4331-8988-33a872d0b5f6)합니다.
- [ASP.NET 상태 관리 권장 사항](https://msdn.microsoft.com/library/z1hkazw7.aspx).
- [Entity Framework 및 ObjectDataSource: 사용자 지정 페이징 사용](http://geekswithblogs.net/Frez/articles/using-the-entity-framework-and-the-objectdatasource-custom-paging.aspx) 이 자습서에서 만든 ContosoUniversity 응용 프로그램을 기반으로 하는 블로그 게시물을 통해 *학과 페이지에서* 페이징을 구현 하는 방법을 설명 합니다.

다음 자습서에서는 버전 4의 새로운 기능에 Entity Framework 대 한 몇 가지 중요 한 향상 된 기능을 검토 합니다.

> [!div class="step-by-step"]
> [이전](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)
> [다음](what-s-new-in-the-entity-framework-4.md)
