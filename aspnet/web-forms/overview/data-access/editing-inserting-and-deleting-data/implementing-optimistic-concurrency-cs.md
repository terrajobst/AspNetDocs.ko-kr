---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs
title: 낙관적 동시성 구현 (C#) | Microsoft Docs
author: rick-anderson
description: 여러 사용자가 데이터를 편집할 수 있도록 허용 하는 웹 응용 프로그램의 경우 두 사용자가 동시에 동일한 데이터를 편집할 수 있습니다. 이 tutori
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 56e15b33-93b8-43ad-8e19-44c6647ea05c
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs
msc.type: authoredcontent
ms.openlocfilehash: 3cddb0efd28249ffc5708ece39c80581d078a5a2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74617479"
---
# <a name="implementing-optimistic-concurrency-c"></a>낙관적 동시성 구현(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_21_CS.exe) 또는 [PDF 다운로드](implementing-optimistic-concurrency-cs/_static/datatutorial21cs1.pdf)

> 여러 사용자가 데이터를 편집할 수 있도록 허용 하는 웹 응용 프로그램의 경우 두 사용자가 동시에 동일한 데이터를 편집할 수 있습니다. 이 자습서에서는이 위험을 처리 하는 낙관적 동시성 제어를 구현 합니다.

## <a name="introduction"></a>소개

사용자가 데이터를 볼 수 있도록 허용 하는 웹 응용 프로그램 또는 데이터를 수정할 수 있는 단일 사용자만 포함 된 웹 응용 프로그램의 경우 두 명의 동시 사용자가 다른 사용자의 변경 내용을 실수로 덮어쓰는 위협 요소가 없습니다. 그러나 여러 사용자가 데이터를 업데이트 하거나 삭제할 수 있도록 하는 웹 응용 프로그램의 경우 한 사용자가 다른 동시 사용자와 충돌 하도록 수정할 가능성이 있습니다. 동시성 정책을 적용 하지 않은 경우 두 사용자가 동시에 단일 레코드를 편집 하는 경우 해당 변경 내용을 마지막으로 커밋한 사용자가 첫 번째에서 변경한 내용을 재정의 합니다.

예를 들어 두 사용자가 모두 응용 프로그램의 페이지를 방문 하 여 방문자가 GridView 컨트롤을 통해 제품을 업데이트 하 고 삭제할 수 있다고 가정 합니다. 동시에 GridView에서 편집 단추를 클릭 합니다. Jisun은 제품 이름을 "Chai Tea"로 변경 하 고 업데이트 단추를 클릭 합니다. Net result는 데이터베이스로 전송 되는 `UPDATE` 문으로, *모든* 제품의 업데이트 가능한 필드 `ProductName`를 설정 합니다 (Jisun은 한 필드만 업데이트 된 경우에도). 이 시점에서 데이터베이스에는이 특정 제품에 대 한 "Chai Tea", 범주 음료, 공급자 Exotic Liquids 등의 값이 있습니다. 그러나 Sam 화면에서 GridView는 편집 가능한 GridView 행의 제품 이름을 "Chai"로 계속 표시 합니다. Jisun의 변경 내용이 커밋된 후 몇 초 후에 Sam이 범주를 조미료로 업데이트 하 고 업데이트를 클릭 합니다. 이렇게 하면 제품 이름을 "Chai"로 설정 하는 데이터베이스와 해당 음료 범주 ID로 `CategoryID` 전송 되는 `UPDATE` 문이 생성 됩니다. 제품 이름에 대 한 jisun 변경을 덮어썼습니다. 그림 1에서는 이러한 일련의 이벤트를 그래픽으로 보여 줍니다.

[두 사용자가 레코드를 동시에 업데이트 하는 경우 ![한 사용자가 다른 사용자의 변경 내용을 덮어쓸 가능성이 있습니다.](implementing-optimistic-concurrency-cs/_static/image2.png)](implementing-optimistic-concurrency-cs/_static/image1.png)

**그림 1**: 두 사용자가 동시에 레코드를 업데이트 하는 경우 한 사용자가 변경 하 여 다른를 덮어쓸 수 있습니다 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image3.png)).

마찬가지로, 두 사용자가 페이지를 방문 하는 경우 한 사용자가 다른 사용자에 의해 삭제 될 때 레코드를 업데이트 하 고 있을 수 있습니다. 또는 사용자가 페이지를 로드 하 고 삭제 단추를 클릭할 때 사이에 다른 사용자가 해당 레코드의 내용을 수정 했을 수 있습니다.

세 가지 [동시성 제어](http://en.wikipedia.org/wiki/Concurrency_control) 전략을 사용할 수 있습니다.

- **아무 작업도 수행 하지 않음** -동시 사용자가 동일한 레코드를 수정 하는 경우 마지막 커밋 (기본 동작)을 사용 합니다.
- [**낙관적 동시성**](http://en.wikipedia.org/wiki/Optimistic_concurrency_control) -현재 마다 동시성 충돌이 있을 수 있지만 이러한 충돌은 거의 발생 하지 않는 것으로 가정 합니다. 따라서 충돌이 발생 하는 경우 다른 사용자가 동일한 데이터를 수정 했기 때문에 변경 내용을 저장할 수 없다고 사용자에 게 알립니다.
- **비관적 동시성** -동시성 충돌이 일반적이 고 사용자가 다른 사용자의 동시 작업으로 인해 변경 내용이 저장 되지 않은 것으로 가정 합니다. 따라서 한 사용자가 레코드 업데이트를 시작 하면 해당 레코드를 잠가 사용자가 수정 내용을 커밋할 때까지 다른 사용자가 해당 레코드를 편집 하거나 삭제할 수 없게 됩니다.

지금까지 모든 자습서에서 기본 동시성 해결 전략을 사용 했습니다. 즉, 마지막 쓰기가 성공 하도록 합니다. 이 자습서에서는 낙관적 동시성 제어를 구현 하는 방법을 살펴보겠습니다.

> [!NOTE]
> 이 자습서 시리즈의 비관적 동시성 예는 확인 하지 않습니다. 비관적 동시성은 거의 사용 되지 않습니다. 이러한 잠금의 경우 적절 한 하므로 없는 경우 다른 사용자가 데이터를 업데이트 하지 못할 수 있습니다. 예를 들어 사용자가 편집을 위해 레코드를 잠근 다음 해당 날짜를 잠금 해제 하기 전에 남겨 둔 경우 원래 사용자가 업데이트를 반환 하 고 완료할 때까지 다른 사용자가 해당 레코드를 업데이트할 수 없습니다. 따라서 비관적 동시성을 사용 하는 경우 일반적으로 시간 제한이 발생 하 여 잠금을 취소 합니다. 사용자가 주문 프로세스를 완료 하는 동안 짧은 기간 동안 특정 좌석 위치를 잠그는 티켓 판매 websites는 비관적 동시성 제어의 한 예입니다.

## <a name="step-1-looking-at-how-optimistic-concurrency-is-implemented"></a>1 단계: 낙관적 동시성을 구현 하는 방법 보기

낙관적 동시성 제어는 업데이트 또는 삭제 하는 레코드의 값이 업데이트 또는 삭제 프로세스가 시작 된 것과 동일한 지 확인 하는 방식으로 작동 합니다. 예를 들어 편집 가능한 GridView에서 편집 단추를 클릭 하면 레코드의 값이 데이터베이스에서 읽어서 텍스트 상자와 다른 웹 컨트롤에 표시 됩니다. 이러한 원래 값은 GridView에 의해 저장 됩니다. 나중에 사용자가 변경 하 고 업데이트 단추를 클릭 하면 원래 값과 새 값이 비즈니스 논리 계층으로 전송 된 다음 데이터 액세스 계층으로 이동 됩니다. 데이터 액세스 계층은 사용자가 편집을 시작한 원래 값이 데이터베이스에 있는 값과 동일한 경우에만 레코드를 업데이트 하는 SQL 문을 실행 해야 합니다. 그림 2에서는 이러한 이벤트 시퀀스를 보여 줍니다.

[업데이트 또는 삭제에 대 한 ![성공 하려면 원래 값이 현재 데이터베이스 값과 같아야 합니다.](implementing-optimistic-concurrency-cs/_static/image5.png)](implementing-optimistic-concurrency-cs/_static/image4.png)

**그림 2**: 업데이트 또는 삭제가 성공 하려면 원래 값이 현재 데이터베이스 값과 같아야 합니다 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image6.png)).

낙관적 동시성을 구현 하는 방법에는 여러 가지가 있습니다 (여러 옵션에 대 한 간략 한 개요는 [Peter Bromberg](http://peterbromberg.net/)의 [낙관적 동시성 업데이트 논리](http://www.eggheadcafe.com/articles/20050719.asp) 참조). ADO.NET 형식화 된 데이터 집합은 확인란의 틱 으로만 구성할 수 있는 하나의 구현을 제공 합니다. 형식화 된 데이터 집합에서 TableAdapter에 대해 낙관적 동시성을 사용 하도록 설정 하면 TableAdapter의 `UPDATE` 및 `DELETE` 문을 보강 하 여 `WHERE` 절의 모든 원래 값에 대 한 비교를 포함 합니다. 예를 들어 다음 `UPDATE` 문은 현재 데이터베이스 값이 GridView의 레코드를 업데이트할 때 원래 검색 된 값과 동일한 경우에만 제품의 이름과 가격을 업데이트 합니다. `@ProductName` 및 `@UnitPrice` 매개 변수는 사용자가 입력 한 새 값을 포함 하는 반면 `@original_ProductName` 및 `@original_UnitPrice`에는 편집 단추를 클릭 했을 때 원래 GridView로 로드 된 값이 포함 됩니다.

[!code-sql[Main](implementing-optimistic-concurrency-cs/samples/sample1.sql)]

> [!NOTE]
> 이 `UPDATE` 문은 가독성을 위해 간소화 되었습니다. 실제로 `WHERE` 절의 `UnitPrice` 검사는 `NULL`를 포함 하 고 `NULL = NULL`에서 항상 False를 반환 하는지 여부를 확인 하기 `UnitPrice` 때문에 더 많은 관련이 있습니다 (대신 `IS NULL`를 사용 해야 함).

다른 기본 `UPDATE` 문을 사용 하는 것 외에도, 낙관적 동시성을 사용 하도록 TableAdapter를 구성 하는 것은 DB 직접 메서드의 서명을 수정 합니다. 첫 번째 자습서를 통해 [*데이터 액세스 계층을 만들고*](../introduction/creating-a-data-access-layer-cs.md), 해당 DB 직접 메서드는 스칼라 값 목록을 강력한 형식의 DataRow 또는 DataTable 인스턴스가 아닌 입력 매개 변수로 허용 하는 것입니다. 낙관적 동시성을 사용 하는 경우 DB direct `Update()` 및 `Delete()` 메서드에 원래 값에 대 한 입력 매개 변수도 포함 됩니다. 또한 batch 업데이트 패턴을 사용 하기 위한 BLL의 코드 `Update()` (스칼라 값이 아닌 Datarow 및 Datatable를 허용 하는 메서드 오버 로드)도 변경 해야 합니다.

낙관적 동시성을 사용 하기 위해 기존 DAL의 Tableadapter를 확장 하는 대신 낙관적 동시성을 사용 하도록 변경 하는 것이 좋습니다 .이는 낙관적 동시성을 사용 하는 `Products` TableAdapter를 추가할 `NorthwindOptimisticConcurrency`이라는 새 형식화 된 데이터 집합을 만드는 것입니다. 다음으로 낙관적 동시성 DAL을 지원 하기 위해 적절 한 수정이 있는 `ProductsOptimisticConcurrencyBLL` 비즈니스 논리 계층 클래스를 만듭니다. 이 기반이 배치 된 후에는 ASP.NET 페이지를 만들 준비가 되었습니다.

## <a name="step-2-creating-a-data-access-layer-that-supports-optimistic-concurrency"></a>2 단계: 낙관적 동시성을 지 원하는 데이터 액세스 계층 만들기

새 형식화 된 데이터 집합을 만들려면 `App_Code` 폴더 내의 `DAL` 폴더를 마우스 오른쪽 단추로 클릭 하 고 `NorthwindOptimisticConcurrency`라는 새 데이터 집합을 추가 합니다. 첫 번째 자습서에서 살펴본 것 처럼이 작업을 수행 하면 형식화 된 데이터 집합에 새 TableAdapter가 추가 되어 TableAdapter 구성 마법사가 자동으로 시작 됩니다. 첫 번째 화면에는 연결할 데이터베이스를 지정 하 라는 메시지가 표시 됩니다.-`Web.config`에서 `NORTHWNDConnectionString` 설정을 사용 하 여 동일한 Northwind 데이터베이스에 연결 합니다.

[동일한 Northwind 데이터베이스에 연결 ![](implementing-optimistic-concurrency-cs/_static/image8.png)](implementing-optimistic-concurrency-cs/_static/image7.png)

**그림 3**: 동일한 Northwind 데이터베이스에 연결 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image9.png))

다음으로, 임시 SQL 문, 새 저장 프로시저 또는 기존 저장 프로시저를 통해 데이터를 쿼리 하는 방법에 대 한 메시지가 표시 됩니다. 원래 DAL에서 임시 SQL 쿼리를 사용 했으므로 여기에서이 옵션을 사용 합니다.

[임시 SQL 문을 사용 하 여 검색할 데이터를 지정 ![](implementing-optimistic-concurrency-cs/_static/image11.png)](implementing-optimistic-concurrency-cs/_static/image10.png)

**그림 4**: 임시 SQL 문을 사용 하 여 검색할 데이터 지정 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image12.png))

다음 화면에서 제품 정보를 검색 하는 데 사용할 SQL 쿼리를 입력 합니다. 원래 DAL의 `Products` TableAdapter에 사용 되는 것과 정확히 동일한 SQL 쿼리를 사용 하 여 제품의 공급자 및 범주 이름과 함께 모든 `Product` 열을 반환 합니다.

[!code-sql[Main](implementing-optimistic-concurrency-cs/samples/sample2.sql)]

[원본 DAL의 TableAdapter 제품에서 동일한 SQL 쿼리를 사용 ![](implementing-optimistic-concurrency-cs/_static/image14.png)](implementing-optimistic-concurrency-cs/_static/image13.png)

**그림 5**: 원래 DAL에서 `Products` TableAdapter와 동일한 SQL 쿼리 사용 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image15.png))

다음 화면으로 이동 하기 전에 고급 옵션 단추를 클릭 합니다. 이 TableAdapter에서 낙관적 동시성 제어를 사용 하도록 하려면 "낙관적 동시성 사용" 확인란을 선택 하면 됩니다.

[낙관적 동시성 제어 사용 &quot;를 선택 하 여 낙관적 동시성 제어를 사용 하도록 설정 ![&quot; 확인란](implementing-optimistic-concurrency-cs/_static/image17.png)](implementing-optimistic-concurrency-cs/_static/image16.png)

**그림 6**: "낙관적 동시성 사용" 확인란을 선택 하 여 낙관적 동시성 제어 사용 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image18.png))

마지막으로 TableAdapter가 DataTable을 채우고 DataTable을 반환 하는 데이터 액세스 패턴을 사용 하도록 지정 합니다. 또한 DB 직접 메서드를 만들어야 함을 표시 합니다. 원래 DAL에서 사용한 명명 규칙을 미러 하기 위해 GetData에서 GetProducts로 DataTable 패턴을 반환 하도록 메서드 이름을 변경 합니다.

[TableAdapter가 모든 데이터 액세스 패턴을 활용 하는 ![](implementing-optimistic-concurrency-cs/_static/image20.png)](implementing-optimistic-concurrency-cs/_static/image19.png)

**그림 7**: TableAdapter에서 모든 데이터 액세스 패턴을 사용 하도록[하려면 (전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image21.png))

마법사를 완료 한 후 데이터 집합 디자이너에는 강력한 형식의 `Products` DataTable 및 TableAdapter가 포함 됩니다. Datatable의 제목 표시줄을 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 이름 바꾸기를 선택 하 여 DataTable의 이름을 `Products`에서 `ProductsOptimisticConcurrency`로 바꿀 수 있습니다.

[DataTable 및 TableAdapter가 형식화 된 데이터 집합에 추가 ![](implementing-optimistic-concurrency-cs/_static/image23.png)](implementing-optimistic-concurrency-cs/_static/image22.png)

**그림 8**: DataTable 및 TableAdapter가 형식화 된 데이터 집합에 추가 되었습니다 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image24.png)).

`UPDATE`와 `DELETE` 간의 차이점을 확인 하려면 tableadapter (낙관적 동시성을 사용 하는)와 Products (`ProductsOptimisticConcurrency`) 간의 차이점을 확인 하 고 tableadapter를 클릭 한 다음 속성 창로 이동 합니다. `DeleteCommand` 및 `UpdateCommand` 속성 `CommandText` 하위 속성에서 DAL의 업데이트 또는 삭제 관련 메서드가 호출 될 때 데이터베이스로 전송 되는 실제 SQL 구문을 볼 수 있습니다. `ProductsOptimisticConcurrency` TableAdapter의 경우 사용 되는 `DELETE` 문은 다음과 같습니다.

[!code-sql[Main](implementing-optimistic-concurrency-cs/samples/sample3.sql)]

원래 DAL의 제품 TableAdapter에 대 한 `DELETE` 문은 훨씬 간단 합니다.

[!code-sql[Main](implementing-optimistic-concurrency-cs/samples/sample4.sql)]

여기에서 볼 수 있듯이 낙관적 동시성을 사용 하는 TableAdapter에 대 한 `DELETE` 문의 `WHERE` 절에는 GridView (또는 DetailsView 또는 FormView)가 마지막으로 채워질 때의 원래 값과 `Product` 테이블의 기존 열 값을 비교 하는 작업이 포함 됩니다. `ProductID`, `ProductName`및 `Discontinued` 이외의 모든 필드에는 `NULL` 값이 있을 수 있으므로 `NULL` 절의 `WHERE` 값을 올바르게 비교 하기 위해 추가 매개 변수 및 검사가 포함 되어 있습니다.

ASP.NET 페이지는 제품 정보만 업데이트 하 고 삭제할 수 있으므로이 자습서의 낙관적 동시성 지원 데이터 집합에 추가 Datatable를 추가 하지 않습니다. 그러나 `ProductsOptimisticConcurrency` TableAdapter에 `GetProductByProductID(productID)` 메서드를 추가 해야 합니다.

이렇게 하려면 TableAdapter의 제목 표시줄을 마우스 오른쪽 단추로 클릭 하 고 `Fill` 바로 위의 영역 및 메서드 이름 `GetProducts` 하 고 상황에 맞는 메뉴에서 쿼리 추가를 선택 합니다. TableAdapter 쿼리 구성 마법사가 시작 됩니다. TableAdapter의 초기 구성과 마찬가지로 임시 SQL 문을 사용 하 여 `GetProductByProductID(productID)` 메서드를 만들도록 옵트인 합니다 (그림 4 참조). `GetProductByProductID(productID)` 메서드는 특정 제품에 대 한 정보를 반환 하므로이 쿼리가 행을 반환 하는 `SELECT` 쿼리 유형인 것으로 표시 합니다.

[행을 반환 하는 &quot;SELECT로 쿼리 유형을 표시 ![&quot;](implementing-optimistic-concurrency-cs/_static/image26.png)](implementing-optimistic-concurrency-cs/_static/image25.png)

**그림 9**: 쿼리 유형을 "행을 반환 하는`SELECT`"로 표시 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image27.png))

다음 화면에서 TableAdapter의 기본 쿼리를 미리 로드 하 여 사용할 SQL 쿼리를 묻는 메시지가 표시 됩니다. 그림 10에 표시 된 것 처럼 `WHERE ProductID = @ProductID`절을 포함 하도록 기존 쿼리를 보강 합니다.

[![특정 제품 레코드를 반환 하기 위해 미리 로드 된 쿼리에 WHERE 절을 추가 합니다.](implementing-optimistic-concurrency-cs/_static/image29.png)](implementing-optimistic-concurrency-cs/_static/image28.png)

**그림 10**: 미리 로드 된 쿼리에 `WHERE` 절을 추가 하 여 특정 제품 레코드 반환 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image30.png))

마지막으로 생성 된 메서드 이름을 `FillByProductID`로 변경 하 고 `GetProductByProductID`합니다.

[메서드의 이름을 FillByProductID 및 Getproductid Byproductid로 바꾸기 ![](implementing-optimistic-concurrency-cs/_static/image32.png)](implementing-optimistic-concurrency-cs/_static/image31.png)

**그림 11**: `FillByProductID` 및 `GetProductByProductID` 메서드 이름 바꾸기 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image33.png))

이 마법사를 완료 하면 TableAdapter에는 데이터를 검색 하는 두 가지 메서드인 `GetProducts()`이 포함 됩니다 .이는 *모든* 제품을 반환 합니다. 지정 된 제품을 반환 하는 및를 `GetProductByProductID(productID)`합니다.

## <a name="step-3-creating-a-business-logic-layer-for-the-optimistic-concurrency-enabled-dal"></a>3 단계: 낙관적 동시성 사용 DAL에 대 한 비즈니스 논리 계층 만들기

기존 `ProductsBLL` 클래스에는 batch 업데이트 및 DB 직접 패턴을 모두 사용 하는 예가 포함 되어 있습니다. `AddProduct` 메서드와 `UpdateProduct` 오버 로드는 모두 일괄 업데이트 패턴을 사용 하 여 `ProductRow` 인스턴스를 TableAdapter의 업데이트 메서드로 전달 합니다. 반면에 `DeleteProduct` 메서드는 DB direct 패턴을 사용 하 여 TableAdapter의 `Delete(productID)` 메서드를 호출 합니다.

새 `ProductsOptimisticConcurrency` TableAdapter를 사용 하는 경우 DB direct 메서드는 이제 원래 값도 전달 해야 합니다. 예를 들어 `Delete` 메서드는 이제 원래 `ProductID`, `ProductName`, `SupplierID`, `CategoryID`, `QuantityPerUnit`, `UnitPrice`, `UnitsInStock`, `UnitsOnOrder`, `ReorderLevel`의 입력 매개 변수를 예상 합니다. 데이터베이스에 전송 된 `DELETE` 문의 `WHERE` 절에 이러한 추가 입력 매개 변수의 값을 사용 하 고 데이터베이스의 현재 값이 원래 값으로 매핑되는 경우에만 지정 된 레코드만 삭제 합니다.

일괄 처리 업데이트 패턴에 사용 된 TableAdapter의 `Update` 메서드에 대 한 메서드 시그니처는 변경 되지 않지만 원래 값과 새 값을 기록 하는 데 필요한 코드는입니다. 따라서 기존 `ProductsBLL` 클래스에서 낙관적 동시성을 사용 하는 DAL을 사용 하는 대신 새 DAL 작업을 위한 새로운 비즈니스 논리 계층 클래스를 만들어 보겠습니다.

`ProductsOptimisticConcurrencyBLL` 라는 클래스를 `App_Code` 폴더 내의 `BLL` 폴더에 추가 합니다.

![ProductsOptimisticConcurrencyBLL 클래스를 BLL 폴더에 추가 합니다.](implementing-optimistic-concurrency-cs/_static/image34.png)

**그림 12**: BLL 폴더에 `ProductsOptimisticConcurrencyBLL` 클래스 추가

그런 다음 `ProductsOptimisticConcurrencyBLL` 클래스에 다음 코드를 추가 합니다.

[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample5.cs)]

클래스 선언 시작 부분 위에 using `NorthwindOptimisticConcurrencyTableAdapters` 문을 적어둡니다. `NorthwindOptimisticConcurrencyTableAdapters` 네임 스페이스는 DAL의 메서드를 제공 하는 `ProductsOptimisticConcurrencyTableAdapter` 클래스를 포함 합니다. 또한 클래스 선언 이전에는이 클래스를 ObjectDataSource 마법사의 드롭다운 목록에 포함 하도록 Visual Studio에 지시 하는 `System.ComponentModel.DataObject` 특성을 찾을 수 있습니다.

`ProductsOptimisticConcurrencyBLL`의 `Adapter` 속성은 `ProductsOptimisticConcurrencyTableAdapter` 클래스의 인스턴스에 대 한 빠른 액세스를 제공 하며 원래 BLL 클래스 (`ProductsBLL`, `CategoriesBLL`등)에서 사용 되는 패턴을 따릅니다. 마지막으로 `GetProducts()` 메서드는 DAL의 `GetProducts()` 메서드를 호출 하 고 데이터베이스의 각 제품 레코드에 대해 `ProductsOptimisticConcurrencyRow` 인스턴스로 채워진 `ProductsOptimisticConcurrencyDataTable` 개체를 반환 합니다.

## <a name="deleting-a-product-using-the-db-direct-pattern-with-optimistic-concurrency"></a>낙관적 동시성을 사용 하는 DB Direct 패턴을 사용 하 여 제품 삭제

낙관적 동시성을 사용 하는 DAL에 대해 DB direct 패턴을 사용 하는 경우 메서드에 새 값과 원래 값이 전달 되어야 합니다. 삭제의 경우 새 값이 없으므로 원래 값만 전달 해야 합니다. 그러면 BLL에서 모든 원래 매개 변수를 입력 매개 변수로 수락 해야 합니다. `ProductsOptimisticConcurrencyBLL` 클래스의 `DeleteProduct` 메서드가 DB direct 메서드를 사용 하 고 있습니다. 즉,이 메서드는 다음 코드에 표시 된 것 처럼 모든 10 개의 제품 데이터 필드를 입력 매개 변수로 사용 하 고 DAL에 전달 해야 합니다.

[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample6.cs)]

사용자가 삭제 단추를 클릭할 때 원래 값 (또는 DetailsView 또는 FormView)에 마지막으로 로드 된 값이 데이터베이스의 값과 다를 경우에는 `WHERE` 절이 데이터베이스 레코드와 일치 하지 않으며 레코드는 영향을 받지 않습니다. 따라서 TableAdapter의 `Delete` 메서드는 `0`를 반환 하 고 BLL의 `DeleteProduct` 메서드는 `false`을 반환 합니다.

## <a name="updating-a-product-using-the-batch-update-pattern-with-optimistic-concurrency"></a>낙관적 동시성을 사용 하 여 Batch 업데이트 패턴을 사용 하 여 제품 업데이트

앞에서 설명한 대로 일괄 처리 업데이트 패턴에 대 한 TableAdapter의 `Update` 메서드는 낙관적 동시성을 사용 하는지 여부에 관계 없이 동일한 메서드 시그니처를 가집니다. 즉, `Update` 메서드에는 DataRow, Datarow 배열, DataTable 또는 형식화 된 데이터 집합이 필요 합니다. 원래 값을 지정 하기 위한 추가 입력 매개 변수는 없습니다. DataTable은 해당 DataRow의 원래 값과 수정 된 값을 추적 하기 때문에 가능 합니다. DAL이 해당 `UPDATE` 문을 발급 하면 `@original_ColumnName` 매개 변수가 DataRow의 원래 값으로 채워지고, `@ColumnName` 매개 변수는 DataRow의 수정 된 값으로 채워집니다.

기존의 비 낙관적 동시성 DAL을 사용 하는 `ProductsBLL` 클래스에서 batch 업데이트 패턴을 사용 하 여 제품 정보를 업데이트 하는 경우 코드에서 다음과 같은 이벤트 시퀀스를 수행 합니다.

1. TableAdapter의 `GetProductByProductID(productID)` 메서드를 사용 하 여 `ProductRow` 인스턴스로 현재 데이터베이스 제품 정보를 읽습니다.
2. 1 단계의 `ProductRow` 인스턴스에 새 값을 할당 합니다.
3. TableAdapter의 `Update` 메서드를 호출 하 여 `ProductRow` 인스턴스를 전달 합니다.

그러나이 일련의 단계는 1 단계에서 채운 `ProductRow` 데이터베이스에서 직접 채워지기 때문에 낙관적 동시성을 올바르게 지원 하지 않습니다. 즉, DataRow에서 사용 되는 원래 값이 데이터베이스에 현재 존재 하는 값이 고 편집 프로세스 시작 시 GridView에 바인딩된 값이 아닌 경우에는 낙관적 동시성을 올바르게 지원 하지 않습니다. 대신 낙관적 동시성을 사용 하는 DAL을 사용 하는 경우 다음 단계를 사용 하도록 `UpdateProduct` 메서드 오버 로드를 변경 해야 합니다.

1. TableAdapter의 `GetProductByProductID(productID)` 메서드를 사용 하 여 `ProductsOptimisticConcurrencyRow` 인스턴스로 현재 데이터베이스 제품 정보를 읽습니다.
2. 1 단계의 `ProductsOptimisticConcurrencyRow` 인스턴스에 *원래* 값을 할당 합니다.
3. `ProductsOptimisticConcurrencyRow` 인스턴스의 `AcceptChanges()` 메서드를 호출 합니다 .이 메서드는 DataRow에 현재 값이 "원본" 임을 지시 합니다.
4. `ProductsOptimisticConcurrencyRow` 인스턴스에 *새* 값을 할당 합니다.
5. TableAdapter의 `Update` 메서드를 호출 하 여 `ProductsOptimisticConcurrencyRow` 인스턴스를 전달 합니다.

1 단계는 지정 된 제품 레코드에 대 한 모든 현재 데이터베이스 값을 읽습니다. 이 단계는 2 단계에서 이러한 값을 덮어쓸 때 *모든* 제품 열을 업데이트 하는 `UpdateProduct` 오버 로드에서 불필요 하지만 열 값의 하위 집합만 입력 매개 변수로 전달 되는 경우에는 이러한 오버 로드에 반드시 필요 합니다. `ProductsOptimisticConcurrencyRow` 인스턴스에 원래 값이 할당 되 면 `AcceptChanges()` 메서드가 호출 됩니다 .이 메서드는 현재 DataRow 값을 `UPDATE` 문의 `@original_ColumnName` 매개 변수에 사용할 원래 값으로 표시 합니다. 그런 다음 `ProductsOptimisticConcurrencyRow`에 새 매개 변수 값을 할당 하 고 마지막으로 `Update` 메서드를 호출 하 여 DataRow를 전달 합니다.

다음 코드에서는 모든 제품 데이터 필드를 입력 매개 변수로 허용 하는 `UpdateProduct` 오버 로드를 보여 줍니다. 여기에 표시 되지 않은 경우이 자습서에 대 한 다운로드에 포함 된 `ProductsOptimisticConcurrencyBLL` 클래스에는 제품의 이름과 가격만 입력 매개 변수로 허용 하는 `UpdateProduct` 오버 로드가 포함 됩니다.

[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample7.cs)]

## <a name="step-4-passing-the-original-and-new-values-from-the-aspnet-page-to-the-bll-methods"></a>4 단계: ASP.NET 페이지의 원래 값과 새 값을 BLL 메서드로 전달

DAL 및 BLL이 완료 되 면 시스템에 기본 제공 되는 낙관적 동시성 논리를 활용할 수 있는 ASP.NET 페이지를 만들 수 있습니다. 특히 데이터 웹 컨트롤 (GridView, DetailsView 또는 FormView)은 원래 값을 명심 해야 하며 ObjectDataSource는 두 값 집합을 모두 비즈니스 논리 계층에 전달 해야 합니다. 또한 동시성 위반을 정상적으로 처리 하도록 ASP.NET 페이지를 구성 해야 합니다.

먼저 `EditInsertDelete` 폴더에서 `OptimisticConcurrency.aspx` 페이지를 열고 GridView를 디자이너에 추가 하 여 `ID` 속성을 `ProductsGrid`로 설정 합니다. GridView의 스마트 태그에서 `ProductsOptimisticConcurrencyDataSource`라는 새 ObjectDataSource를 만들도록 옵트인 합니다. 이 ObjectDataSource에서 낙관적 동시성을 지 원하는 DAL을 사용 하려고 하므로 `ProductsOptimisticConcurrencyBLL` 개체를 사용 하도록 구성 해야 합니다.

[ObjectDataSource에서 ProductsOptimisticConcurrencyBLL 개체를 사용 ![](implementing-optimistic-concurrency-cs/_static/image36.png)](implementing-optimistic-concurrency-cs/_static/image35.png)

**그림 13**: ObjectDataSource에서 `ProductsOptimisticConcurrencyBLL` 개체 사용 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image37.png))

마법사의 드롭다운 목록에서 `GetProducts`, `UpdateProduct`및 `DeleteProduct` 메서드를 선택 합니다. UpdateProduct 메서드의 경우 모든 제품의 데이터 필드를 허용 하는 오버 로드를 사용 합니다.

## <a name="configuring-the-objectdatasource-controls-properties"></a>ObjectDataSource 컨트롤의 속성 구성

마법사를 완료 한 후 ObjectDataSource의 선언 태그는 다음과 같습니다.

[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample8.aspx)]

여기에서 볼 수 있듯이 `DeleteParameters` 컬렉션에는 `ProductsOptimisticConcurrencyBLL` 클래스의 `DeleteProduct` 메서드에서 각각의 10 개의 입력 매개 변수에 대 한 `Parameter` 인스턴스가 포함 됩니다. 마찬가지로 `UpdateParameters` 컬렉션에는 `UpdateProduct`의 각 입력 매개 변수에 대 한 `Parameter` 인스턴스가 포함 되어 있습니다.

데이터 수정과 관련 된 이전 자습서의 경우,이 속성은이 시점에서 ObjectDataSource의 `OldValuesParameterFormatString` 속성을 제거 합니다 .이 속성은 BLL 메서드에 이전 (또는 원래) 값이 전달 될 것으로 예상 하 고 새 값을 전달 한다는 것을 나타냅니다. 또한이 속성 값은 원래 값에 대 한 입력 매개 변수 이름을 나타냅니다. 원래 값을 BLL에 전달 하기 때문에이 속성을 제거 *하지* 마십시오.

> [!NOTE]
> `OldValuesParameterFormatString` 속성의 값은 원래 값이 필요한 BLL의 입력 매개 변수 이름에 매핑되어야 합니다. 이러한 매개 변수를 `original_productName`, `original_supplierID`등으로 명명 했으므로 `OldValuesParameterFormatString` 속성 값을 `original_{0}`로 유지할 수 있습니다. 그러나 BLL 메서드의 입력 매개 변수에 `old_productName`, `old_supplierID`등과 같은 이름이 있는 경우 `OldValuesParameterFormatString` 속성을 `old_{0}`로 업데이트 해야 합니다.

ObjectDataSource가 원래 값을 BLL 메서드에 올바르게 전달 하기 위해 수행 해야 하는 최종 속성 설정이 하나 있습니다. ObjectDataSource에는 다음 [두 값 중 하나](https://msdn.microsoft.com/library/system.web.ui.conflictoptions.aspx)에 할당할 수 있는 [ConflictDetection 속성이](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.conflictdetection.aspx) 있습니다.

- `OverwriteChanges`-기본값입니다. 는 원래 값을 BLL 메서드의 원래 입력 매개 변수로 보내지 않습니다.
- `CompareAllValues`-원래 값을 BLL 메서드로 보냅니다. 낙관적 동시성을 사용 하는 경우이 옵션을 선택 합니다.

잠시 시간을 사용 하 여 `ConflictDetection` 속성을 `CompareAllValues`로 설정 합니다.

## <a name="configuring-the-gridviews-properties-and-fields"></a>GridView의 속성 및 필드 구성

ObjectDataSource의 속성이 제대로 구성 된 상태에서 GridView를 설정 하는 데 주의를 기울여야 합니다. 먼저 GridView에서 편집 및 삭제를 지원 하기 때문에 GridView의 스마트 태그에서 편집 사용 및 삭제할 수 있습니다 확인란을 클릭 합니다. 그러면 `ShowEditButton`와 `ShowDeleteButton` 모두 `true`으로 설정 된 CommandField가 추가 됩니다.

`ProductsOptimisticConcurrencyDataSource` ObjectDataSource에 바인딩되는 경우 GridView는 각 제품의 데이터 필드에 대 한 필드를 포함 합니다. 이러한 GridView를 편집할 수 있지만 사용자 환경에는 무엇이 든 사용할 수 있습니다. `CategoryID` 및 `SupplierID` BoundFields는 입력란으로 렌더링 되므로 사용자가 적절 한 범주와 공급 업체를 ID 번호로 입력 해야 합니다. 숫자 필드에 대 한 서식은 없으며, 제품 이름을 제공 하 고 단가, 재고 단위, 주문 단위 및 다시 정렬 수준 값을 모두 적절 한 숫자 값으로 지정 하 고, 보다 크거나 같은지 확인 하는 유효성 검사 컨트롤은 없습니다. 0입니다.

*편집 및 삽입 인터페이스에 유효성 검사 컨트롤 추가* 및 *데이터 수정 인터페이스* 자습서 사용자 지정에서 설명한 대로 BoundFields를 템플릿 필드로 바꿔 사용자 인터페이스를 사용자 지정할 수 있습니다. 다음 방법으로이 GridView 및 편집 인터페이스를 수정 했습니다.

- `ProductID`, `SupplierName`및 `CategoryName` BoundFields 제거 됨
- `ProductName` BoundField를 Templatefield로 변환로 변환 하 고 RequiredFieldValidation 컨트롤을 추가 했습니다.
- `CategoryID` 및 `SupplierID`를 템플릿 필드로 변환 하 고 텍스트 상자 대신 Dropdownlist를 사용 하도록 편집 인터페이스를 조정 했습니다. 이러한 템플릿 필드의 `ItemTemplates`에는 `CategoryName` 및 `SupplierName` 데이터 필드가 표시 됩니다.
- `UnitPrice`, `UnitsInStock`, `UnitsOnOrder`및 `ReorderLevel` BoundFields를 템플릿 필드로 변환 하 고 CompareValidator 컨트롤을 추가 했습니다.

이전 자습서에서 이러한 작업을 수행 하는 방법을 이미 검토 했으므로 여기에서 최종 선언 구문을 나열 하 고 구현 방법을 그대로 둡니다.

[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample9.aspx)]

완전히 작동 하는 예제는 매우 가깝습니다. 그러나 몇 가지 미묘한 문제로 인해 문제가 발생할 수 있습니다. 또한 동시성 위반이 발생 했을 때 사용자에 게 경고 하는 인터페이스가 여전히 필요 합니다.

> [!NOTE]
> 데이터 웹 컨트롤에서 원래 값을 ObjectDataSource (BLL에 전달 됨)에 올바르게 전달 하려면 GridView의 `EnableViewState` 속성이 `true` (기본값)로 설정 되어 있는 것이 중요 합니다. 뷰 상태를 사용 하지 않도록 설정 하면 다시 게시할 때 원래 값이 손실 됩니다.

## <a name="passing-the-correct-original-values-to-the-objectdatasource"></a>ObjectDataSource에 올바른 원래 값 전달

GridView가 구성 된 방법과 관련 된 몇 가지 문제가 있습니다. ObjectDataSource의 `ConflictDetection` 속성이 `CompareAllValues`으로 설정 된 경우 (예를 들어) objectdatasource의 `Update()` 또는 `Delete()` 메서드가 GridView (또는 DetailsView 또는 FormView)에 의해 호출 되 면 ObjectDataSource에서 GridView의 원래 값을 적절 한 `Parameter` 인스턴스로 복사 하려고 시도 합니다. 이 프로세스를 그래픽으로 표시 하려면 그림 2를 다시 참조 하세요.

특히 GridView의 원래 값에는 데이터가 GridView에 바인딩될 때마다 양방향 데이터 바인딩 문에서 값이 할당 됩니다. 따라서 필수적인 원래 값은 모두 양방향 데이터 바인딩을 통해 캡처되고 변환 가능한 형식으로 제공 되어야 합니다.

이 사항이 중요 한 이유를 확인 하려면 잠시 시간을 들 여 브라우저에서 페이지를 방문 하세요. 예상 대로 GridView는 맨 왼쪽 열에 편집 및 삭제 단추가 있는 각 제품을 나열 합니다.

[GridView에 제품이 나열 ![](implementing-optimistic-concurrency-cs/_static/image39.png)](implementing-optimistic-concurrency-cs/_static/image38.png)

**그림 14**: 제품이 GridView에 나열 되어 있습니다 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image40.png)).

모든 제품에 대 한 삭제 단추를 클릭 하면 `FormatException` throw 됩니다.

[FormatException에서 제품 결과를 삭제 하는 ![](implementing-optimistic-concurrency-cs/_static/image42.png)](implementing-optimistic-concurrency-cs/_static/image41.png)

**그림 15**: `FormatException` ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image43.png))에서 제품을 삭제 하려고 합니다.

ObjectDataSource가 원래 `UnitPrice` 값에서 읽으려고 할 때 `FormatException` 발생 합니다. `ItemTemplate`에는 통화 (`<%# Bind("UnitPrice", "{0:C}") %>`)로 서식이 지정 된 `UnitPrice` 있으므로 $19.95와 같은 통화 기호가 포함 됩니다. `FormatException`은 ObjectDataSource가이 문자열을 `decimal`변환 하려고 할 때 발생 합니다. 이 문제를 방지 하기 위해 다음과 같은 다양 한 옵션을 사용할 수 있습니다.

- `ItemTemplate`에서 통화 서식을 제거 합니다. 즉, `<%# Bind("UnitPrice", "{0:C}") %>`를 사용 하는 대신 `<%# Bind("UnitPrice") %>`를 사용 하기만 하면 됩니다. 이로 인해 가격은 더 이상 서식이 지정 되지 않습니다.
- `ItemTemplate`통화로 형식이 지정 된 `UnitPrice` 표시 하지만 `Eval` 키워드를 사용 하 여이를 수행 합니다. `Eval`는 단방향 데이터 바인딩을 수행 합니다. 여전히 원래 값에 대 한 `UnitPrice` 값을 제공 해야 하기 때문에 `ItemTemplate`에 양방향 데이터 바인딩 문이 필요 하지만 `Visible` 속성이 `false`로 설정 된 레이블 웹 컨트롤에 배치 될 수 있습니다. ItemTemplate에서 다음 태그를 사용할 수 있습니다.

[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample10.aspx)]

- `<%# Bind("UnitPrice") %>`를 사용 하 여 `ItemTemplate`에서 통화 서식을 제거 합니다. GridView의 `RowDataBound` 이벤트 처리기에서 `UnitPrice` 값이 표시 되는 Label 웹 컨트롤에 프로그래밍 방식으로 액세스 하 고 `Text` 속성을 형식이 지정 된 버전으로 설정 합니다.
- `UnitPrice` 서식을 통화로 그대로 둡니다. GridView의 `RowDeleting` 이벤트 처리기에서 `Decimal.Parse`을 사용 하 여 기존의 원래 `UnitPrice` 값 ($19.95)을 실제 10 진수 값으로 바꿉니다. [*ASP.NET 페이지 자습서의 BLL 및 DAL 수준 예외 처리*](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md) 에서 `RowUpdating` 이벤트 처리기와 유사한 작업을 수행 하는 방법을 살펴보았습니다.

다음 예제에서는 두 번째 방법을 사용 하 여 `Text` 속성이 형식이 지정 되지 않은 `UnitPrice` 값에 바인딩된 양방향 데이터 인 숨겨진 Label 웹 컨트롤을 추가 했습니다.

이 문제를 해결 한 후에는 모든 제품에 대 한 삭제 단추를 다시 클릭 하십시오. 이번에는 ObjectDataSource가 BLL의 `UpdateProduct` 메서드를 호출 하려고 할 때 `InvalidOperationException`을 받게 됩니다.

[![ObjectDataSource에서 전송 하려는 입력 매개 변수가 있는 메서드를 찾을 수 없습니다.](implementing-optimistic-concurrency-cs/_static/image45.png)](implementing-optimistic-concurrency-cs/_static/image44.png)

**그림 16**: ObjectDataSource에서 보내려고 하는 입력 매개 변수가 있는 메서드를 찾을 수 없음 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image46.png))

예외의 메시지를 살펴보면 ObjectDataSource가 `original_CategoryName` 및 `original_SupplierName` 입력 매개 변수를 포함 하는 BLL `DeleteProduct` 메서드를 호출 하려고 한다는 것을 알 수 있습니다. `CategoryID` 및 `SupplierID` 템플릿 필드의 `ItemTemplate`에는 현재 `CategoryName` 및 `SupplierName` 데이터 필드를 포함 하는 양방향 바인드 문이 있기 때문입니다. 대신 `CategoryID` 및 `SupplierID` 데이터 필드를 사용 하 여 `Bind` 문을 포함 해야 합니다. 이렇게 하려면 기존 Bind 문을 `Eval` 문으로 바꾼 다음 아래와 같이 `Text` 속성이 `CategoryID`에 바인딩되어 있는 숨겨진 레이블 컨트롤을 추가 하 고 양방향 데이터 바인딩을 사용 하 여 데이터 필드를 `SupplierID` 합니다.

[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample11.aspx)]

이러한 변경으로 이제 제품 정보를 성공적으로 삭제 하 고 편집할 수 있습니다. 5 단계에서는 동시성 위반이 감지 되는지 확인 하는 방법을 살펴보겠습니다. 그러나 지금은 소수의 레코드를 업데이트 하 고 삭제 하는 데 몇 분 정도 걸리며, 단일 사용자에 대 한 업데이트 및 삭제가 예상 대로 작동 하는지 확인 합니다.

## <a name="step-5-testing-the-optimistic-concurrency-support"></a>5 단계: 낙관적 동시성 지원 테스트

동시성 위반이 감지 되는지 확인 하기 위해 (무조건 덮어쓰는 데이터를 생성 하는 대신)이 페이지에서 두 개의 브라우저 창을 열어야 합니다. 두 브라우저 인스턴스 모두에서 Chai에 대 한 편집 단추를 클릭 합니다. 그런 다음 브라우저 중 하나 에서만 이름을 "Chai Tea"로 변경 하 고 업데이트를 클릭 합니다. 업데이트에 성공 하 고 GridView를 미리 편집 상태로 되돌립니다. "Chai Tea"를 새 제품 이름으로 바꿉니다.

그러나 다른 브라우저 창 인스턴스에서는 제품 이름 텍스트 상자에 "Chai"가 계속 표시 됩니다. 이 두 번째 브라우저 창에서 `UnitPrice` `25.00`로 업데이트 합니다. 낙관적 동시성을 지원 하지 않으면 두 번째 브라우저 인스턴스에서 업데이트를 클릭 하면 제품 이름을 "Chai"로 변경 하 여 첫 번째 브라우저 인스턴스의 변경 내용을 덮어씁니다. 그러나 낙관적 동시성을 사용 하는 경우 두 번째 브라우저 인스턴스에서 업데이트 단추를 클릭 하면 [system.data.dbconcurrencyexception](https://msdn.microsoft.com/library/system.data.dbconcurrencyexception.aspx)이 발생 합니다.

[![동시성 위반이 감지 되 면 System.data.dbconcurrencyexception이 Throw 됩니다.](implementing-optimistic-concurrency-cs/_static/image48.png)](implementing-optimistic-concurrency-cs/_static/image47.png)

**그림 17**: 동시성 위반이 감지 되 면 `DBConcurrencyException`이 throw 됩니다 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image49.png)).

`DBConcurrencyException`는 DAL의 batch 업데이트 패턴이 사용 되는 경우에만 throw 됩니다. DB 직접 패턴은 예외를 발생 시 키 지 않으며, 단순히 영향을 받은 행이 없음을 나타냅니다. 이를 설명 하기 위해 브라우저 인스턴스 GridView를 모두 미리 편집 상태로 되돌립니다. 그런 다음, 첫 번째 브라우저 인스턴스에서 편집 단추를 클릭 하 고 제품 이름을 "Chai Tea"에서 "Chai"로 변경 하 고 업데이트를 클릭 합니다. 두 번째 브라우저 창에서 Chai에 대 한 삭제 단추를 클릭 합니다.

삭제를 클릭 하면 페이지가 다시 게시 되 고, GridView는 ObjectDataSource의 `Delete()` 메서드를 호출 하 고, ObjectDataSource는 `ProductsOptimisticConcurrencyBLL` 클래스의 `DeleteProduct` 메서드를 호출 하 여 원래 값을 따라 전달 합니다. 두 번째 브라우저 인스턴스의 원래 `ProductName` 값은 "Chai Tea" 이며 데이터베이스의 현재 `ProductName` 값과 일치 하지 않습니다. 따라서 데이터베이스에 `WHERE` 절이 충족 하는 레코드가 없으므로 데이터베이스에 대해 실행 되는 `DELETE` 문은 0 개 행에 영향을 줍니다. `DeleteProduct` 메서드는 `false`를 반환 하 고 ObjectDataSource의 데이터를 GridView에 바인딩 합니다.

최종 사용자의 관점에서 두 번째 브라우저 창에서 Chai Tea에 대 한 삭제 단추를 클릭 하면 화면이 깜박이는 것으로 표시 되 고, 이제는 "Chai" (첫 번째 브라우저에서 변경한 제품 이름)로 표시 되는 제품도 있습니다. 인스턴스). 사용자가 삭제 단추를 다시 클릭 하면 GridView의 원래 `ProductName` 값 ("Chai")이 데이터베이스의 값과 일치 하므로 삭제가 성공적으로 수행 됩니다.

이러한 두 경우 모두 사용자 환경이 이상적이 지 않습니다. Batch 업데이트 패턴을 사용 하는 경우 `DBConcurrencyException` 예외에 대 한 핵심 사항을 정보를 사용자에 게 표시 하지 않으려고 합니다. DB 직접 패턴을 사용할 때의 동작은 사용자 명령이 실패 하는 경우와 다소 혼동 되지만 이유를 정확 하 게 알 수 없습니다.

이러한 두 가지 문제를 해결 하기 위해 업데이트 또는 삭제가 실패 한 이유에 대 한 설명을 제공 하는 레이블 웹 컨트롤을 페이지에 만들 수 있습니다. 일괄 처리 업데이트 패턴의 경우 GridView의 사후 수준 이벤트 처리기에서 `DBConcurrencyException` 예외가 발생 했는지 여부를 확인 하 고 필요에 따라 경고 레이블을 표시할 수 있습니다. DB direct 메서드의 경우 BLL 메서드의 반환 값 (한 행이 영향을 받는 경우 `false`에는 `true`)을 검토 하 고 필요에 따라 정보 메시지를 표시할 수 있습니다.

## <a name="step-6-adding-informational-messages-and-displaying-them-in-the-face-of-a-concurrency-violation"></a>6 단계: 정보 메시지를 추가 하 고 동시성 위반이 발생할 때 표시

동시성 위반이 발생할 경우 발생 하는 동작은 DAL의 batch 업데이트 또는 DB direct 패턴의 사용 여부에 따라 달라 집니다. 이 자습서에서는 업데이트에 사용 되는 일괄 처리 업데이트 패턴 및 삭제에 사용 되는 DB direct 패턴을 사용 하 여 두 패턴을 모두 사용 합니다. 시작 하려면 데이터를 삭제 하거나 업데이트 하려고 할 때 동시성 위반이 발생 했음을 설명 하는 두 개의 Label 웹 컨트롤을 페이지에 추가 해 보겠습니다. 레이블 컨트롤의 `Visible` 및 `EnableViewState` 속성을 `false`로 설정 합니다. 이렇게 하면 해당 `Visible` 속성이 `true`으로 프로그래밍 방식으로 설정 된 특정 페이지 방문을 제외 하 고 각 페이지를 방문할 때마다 숨겨집니다.

[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample12.aspx)]

`Visible`, `EnabledViewState`및 `Text` 속성을 설정 하는 것 외에도 `CssClass` 속성을 `Warning`로 설정 하 여 레이블이 크고 빨강, 기울임꼴, 굵은 글꼴로 표시 되도록 합니다. 이 CSS `Warning` 클래스를 정의 하 고 스타일에 추가 하 여 자습서 *삽입, 업데이트 및 삭제와 관련 된 이벤트를 검사* 합니다.

이러한 레이블을 추가한 후 Visual Studio의 디자이너는 그림 18과 유사 하 게 표시 됩니다.

[![두 개의 Label 컨트롤이 페이지에 추가 되었습니다.](implementing-optimistic-concurrency-cs/_static/image51.png)](implementing-optimistic-concurrency-cs/_static/image50.png)

**그림 18**: 페이지에 두 개의 Label 컨트롤이 추가 되었습니다 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image52.png)).

이러한 레이블 웹 컨트롤을 사용 하면 동시성 위반이 발생 한 시기를 확인 하는 방법을 검토할 수 있습니다 .이 시점에서 적절 한 레이블의 `Visible` 속성을 `true`으로 설정 하 여 정보 메시지를 표시할 수 있습니다.

## <a name="handling-concurrency-violations-when-updating"></a>업데이트할 때 동시성 위반 처리

먼저 batch 업데이트 패턴을 사용할 때 동시성 위반을 처리 하는 방법을 살펴보겠습니다. 이러한 위반으로 인해 `DBConcurrencyException` 예외가 throw 되기 때문에 업데이트 프로세스 중에 `DBConcurrencyException` 예외가 발생 했는지 여부를 확인 하려면 ASP.NET 페이지에 코드를 추가 해야 합니다. 이 경우 다른 사용자가 레코드 편집을 시작 하 고 업데이트 단추를 클릭할 때와 동일한 데이터를 수정 했기 때문에 변경 내용이 저장 되지 않았습니다 .를 설명 하는 메시지를 사용자에 게 표시 해야 합니다.

*ASP.NET 페이지 자습서의 BLL 및 DAL 수준 예외 처리* 에서 살펴본 것 처럼 이러한 예외는 데이터 웹 컨트롤의 사후 수준 이벤트 처리기에서 검색 되 고 표시 되지 않을 수 있습니다. 따라서 `DBConcurrencyException` 예외가 throw 되었는지 확인 하는 GridView의 `RowUpdated` 이벤트에 대 한 이벤트 처리기를 만들어야 합니다. 이 이벤트 처리기는 아래 이벤트 처리기 코드에 표시 된 것 처럼 업데이트 프로세스 중에 발생 한 모든 예외에 대 한 참조를 전달 합니다.

[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample13.cs)]

`DBConcurrencyException` 예외가 발생할 경우이 이벤트 처리기는 `UpdateConflictMessage` 레이블 컨트롤을 표시 하 고 예외가 처리 되었음을 나타냅니다. 이 코드를 사용 하면 레코드를 업데이트할 때 동시성 위반이 발생할 때 다른 사용자의 수정 내용을 동시에 덮어쓸 수 있기 때문에 사용자의 변경 내용이 손실 됩니다. 특히 GridView는 사전 편집 상태로 반환 되 고 현재 데이터베이스 데이터에 바인딩됩니다. 이렇게 하면 이전에 표시 되지 않은 다른 사용자의 변경 내용으로 GridView 행이 업데이트 됩니다. 또한 `UpdateConflictMessage` Label 컨트롤은 사용자에 게 발생 한 작업을 설명 합니다. 이 이벤트 시퀀스는 그림 19에 자세히 설명 되어 있습니다.

[동시성 위반이 발생 하는 경우 사용자 업데이트가 손실 ![](implementing-optimistic-concurrency-cs/_static/image54.png)](implementing-optimistic-concurrency-cs/_static/image53.png)

**그림 19**: 동시성 위반이 발생 한 경우 사용자 업데이트 손실 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image55.png))

> [!NOTE]
> 또는 GridView를 미리 편집 상태로 되돌리는 대신 전달 된 `GridViewUpdatedEventArgs` 개체의 `KeepInEditMode` 속성을 true로 설정 하 여 GridView를 편집 상태로 둘 수 있습니다. 그러나이 방법을 사용 하는 경우 다른 사용자의 값이 편집 인터페이스에 로드 되도록 해당 `DataBind()` 메서드를 호출 하 여 데이터를 GridView에 다시 바인딩해야 합니다. 이 자습서에서 다운로드할 수 있는 코드에는 `RowUpdated` 이벤트 처리기에서 주석으로 처리 된 두 줄의 코드가 있습니다. 이러한 코드 줄의 주석 처리를 제거 하면 동시성 위반 후 GridView가 편집 모드로 유지 됩니다.

## <a name="responding-to-concurrency-violations-when-deleting"></a>삭제할 때 동시성 위반에 대 한 응답

DB 직접 패턴을 사용 하면 동시성 위반이 발생 하는 경우 예외가 발생 하지 않습니다. 대신, WHERE 절이 레코드와 일치 하지 않기 때문에 데이터베이스 문은 단순히 레코드에 영향을 주지 않습니다. BLL에서 만든 모든 데이터 수정 메서드는 정확히 하나의 레코드에 영향을 미치는지 여부를 나타내는 부울 값을 반환 하도록 디자인 되었습니다. 따라서 레코드를 삭제할 때 동시성 위반이 발생 했는지 확인 하려면 BLL의 `DeleteProduct` 메서드에 대 한 반환 값을 검사할 수 있습니다.

BLL 메서드의 반환 값은 이벤트 처리기로 전달 되는 `ObjectDataSourceStatusEventArgs` 개체의 `ReturnValue` 속성을 통해 ObjectDataSource의 사후 수준 이벤트 처리기에서 검사할 수 있습니다. `DeleteProduct` 메서드에서 반환 값을 결정 하는 데 관심이 있으므로 ObjectDataSource의 `Deleted` 이벤트에 대 한 이벤트 처리기를 만들어야 합니다. `ReturnValue` 속성은 `object` 형식이 며, 예외가 발생 하 고 메서드가 값을 반환 하기 전에 중단 된 경우에 `null` 수 있습니다. 따라서 먼저 `ReturnValue` 속성이 `null` 없고 부울 값 인지 확인 해야 합니다. 이 검사를 통과 한다고 가정 하면 `ReturnValue` `false`경우 `DeleteConflictMessage` 레이블 컨트롤을 표시 합니다. 다음 코드를 사용 하 여이 작업을 수행할 수 있습니다.

[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample14.cs)]

동시성 위반이 발생 하면 사용자의 삭제 요청이 취소 됩니다. GridView가 새로 고쳐지고 사용자가 페이지를 로드 한 시간과 삭제 단추를 클릭 한 시간 사이에 해당 레코드에 발생 한 변경 내용을 표시 합니다. 이러한 위반이 transpires 면 발생 한 상황을 설명 하는 `DeleteConflictMessage` 레이블이 표시 됩니다 (그림 20 참조).

[동시성 위반이 발생 하는 경우 사용자 삭제가 취소 ![](implementing-optimistic-concurrency-cs/_static/image57.png)](implementing-optimistic-concurrency-cs/_static/image56.png)

**그림 20**: 동시성 위반이 발생 하는 경우 사용자 삭제 취소 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image58.png))

## <a name="summary"></a>요약

여러 동시 사용자가 데이터를 업데이트 하거나 삭제할 수 있도록 하는 모든 응용 프로그램에서 동시성 위반에 대 한 기회가 있습니다. 이러한 위반이에 대해 고려 되지 않는 경우 두 사용자가 마지막 쓰기 "wins"에서 가져오는 것과 동일한 데이터를 동시에 업데이트 하는 경우 다른 사용자의 변경 내용을 덮어씁니다. 또는 개발자가 낙관적 또는 비관적 동시성 제어를 구현할 수 있습니다. 낙관적 동시성 제어에서는 동시성 위반이 자주 발생 하지 않으며, 단순히 동시성 위반을 구성 하는 update 또는 delete 명령을 허용 하지 않는다고 가정 합니다. 비관적 동시성 제어에서는 동시성 위반이 자주 발생 하 고 사용자의 업데이트 또는 삭제 명령을 거부 하는 것이 허용 되지 않는 것으로 가정 합니다. 비관적 동시성 제어를 사용 하는 경우 레코드를 업데이트 하는 작업을 수행 하면 다른 사용자가 잠겨 있는 동안 레코드를 수정 하거나 삭제할 수 없게 됩니다.

.NET의 형식화 된 데이터 집합은 낙관적 동시성 제어를 지원 하기 위한 기능을 제공 합니다. 특히 데이터베이스에 대해 실행 되는 `UPDATE` 및 `DELETE` 문은 모든 테이블의 열을 포함 하 여 레코드의 현재 데이터가 사용자가 업데이트 또는 삭제를 수행할 때 수행한 원래 데이터와 일치 하는 경우에만 업데이트 또는 삭제를 수행 합니다. DAL이 낙관적 동시성을 지원 하도록 구성 되 면 BLL 메서드를 업데이트 해야 합니다. 또한 해당 데이터 웹 컨트롤에서 원래 값을 검색 하 여 BLL에 전달 하도록 BLL로 다운을 호출 하는 ASP.NET 페이지를 구성 해야 합니다.

이 자습서에서 살펴본 것 처럼 ASP.NET 웹 응용 프로그램에서 낙관적 동시성 제어를 구현 하려면 DAL 및 BLL을 업데이트 하 고 ASP.NET 페이지에서 지원을 추가 해야 합니다. 이 추가 된 작업은 사용자의 응용 프로그램에 따라 달라 지는 시간 및 노력에 따라 결정 됩니다. 동시 사용자가 데이터를 업데이트 하거나 업데이트 하는 데이터가 서로 다른 경우 동시성 제어는 주요 문제가 아닙니다. 그러나 사이트의 여러 사용자가 동일한 데이터를 사용 하 여 작업을 정기적으로 수행 하는 경우 동시성 제어를 통해 한 사용자의 업데이트나 삭제가 다른의를 덮어쓰는 것을 방지할 수 있습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

> [!div class="step-by-step"]
> [이전](customizing-the-data-modification-interface-cs.md)
> [다음](adding-client-side-confirmation-when-deleting-cs.md)
