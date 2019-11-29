---
uid: web-forms/overview/data-access/paging-and-sorting/sorting-custom-paged-data-cs
title: 사용자 지정 페이징 데이터 정렬C#() | Microsoft Docs
author: rick-anderson
description: 이전 자습서에서는 웹 페이지에 데이터를 프레젠테이션할 때 사용자 지정 페이징을 구현 하는 방법에 대해 알아보았습니다. 이 자습서에서는 위의 항목을 확장 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 08/15/2006
ms.assetid: 778baa4e-4af8-4665-947e-7a01d1a4dff2
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/sorting-custom-paged-data-cs
msc.type: authoredcontent
ms.openlocfilehash: e55ed9b92814753e95bdfdf26c2f051df6f2630d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74642385"
---
# <a name="sorting-custom-paged-data-c"></a>사용자 지정 페이징 데이터 정렬(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_26_CS.exe) 또는 [PDF 다운로드](sorting-custom-paged-data-cs/_static/datatutorial26cs1.pdf)

> 이전 자습서에서는 웹 페이지에 데이터를 프레젠테이션할 때 사용자 지정 페이징을 구현 하는 방법에 대해 알아보았습니다. 이 자습서에서는 사용자 지정 페이징 정렬을 지원 하기 위해 앞의 예제를 확장 하는 방법을 알아봅니다.

## <a name="introduction"></a>소개

기본 페이징과 비교할 때 사용자 지정 페이징은 여러 크기의 데이터를 페이징 하는 성능을 향상 시킬 수 있습니다. 많은 양의 데이터를 페이징할 때 사용자 지정 페이징이 사실상 페이징을 구현 하는 것이 좋습니다. 그러나 사용자 지정 페이징을 구현 하는 것은 기본 페이징을 구현 하는 것 보다 더 복잡 합니다. 그러나 특히 혼합에 정렬을 추가 하는 경우입니다. 이 자습서에서는 정렬 *및* 사용자 지정 페이징에 대 한 지원을 포함 하도록 앞의 예제를 확장 합니다.

> [!NOTE]
> 이 자습서는 앞의 자습서를 기반으로 하기 때문에 이전 자습서 s 웹 페이지 (`EfficientPaging.aspx`)의 `<asp:Content>` 요소 내에서 선언적 구문을 복사 하 여 `SortParameter.aspx` 페이지의 `<asp:Content>` 요소 사이에 붙여 넣는 것이 시작 되기 전에 수행 합니다. 한 ASP.NET 페이지의 기능을 다른 페이지로 복제 하는 방법에 대 한 자세한 내용은 [편집 및 삽입 인터페이스에 유효성 검사 컨트롤 추가](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-cs.md) 자습서의 1 단계를 다시 참조 하세요.

## <a name="step-1-reexamining-the-custom-paging-technique"></a>1 단계: 사용자 지정 페이징 기술 Reexamining

사용자 지정 페이징이 제대로 작동 하려면 시작 행 인덱스 및 최대 행 매개 변수가 지정 된 경우 레코드의 특정 하위 집합을 효율적으로 검색할 수 있는 몇 가지 기법을 구현 해야 합니다. 이러한 목표를 얻기 위해 사용할 수 있는 몇 가지 기술이 있습니다. 이전 자습서에서는 Microsoft SQL Server 2005 s new `ROW_NUMBER()` 순위 함수를 사용 하 여이를 수행 하는 방법을 살펴보았습니다. 즉, `ROW_NUMBER()` 순위 함수는 지정 된 정렬 순서에 따라 순위가 지정 된 쿼리에 의해 반환 된 각 행에 행 번호를 할당 합니다. 그러면 레코드의 적절 한 하위 집합이 번호가 매겨진 결과의 특정 섹션을 반환 하 여 얻어집니다. 다음 쿼리에서는이 기법을 사용 하 여 `ProductName`기준으로 사전순으로 정렬 된 결과를 순위를 지정 하는 경우 11에서 20까지 번호가 매겨진 제품을 반환 하는 방법을 보여 줍니다.

[!code-sql[Main](sorting-custom-paged-data-cs/samples/sample1.sql)]

이 기술은 특정 정렬 순서 (이 경우 사전순으로 정렬`ProductName`)를 사용 하 여 페이징에 적합 하지만 다른 정렬 식에 따라 정렬 된 결과를 표시 하도록 쿼리를 수정 해야 합니다. 이상적으로 위의 쿼리는 다음과 같이 `OVER` 절에서 매개 변수를 사용 하도록 다시 작성할 수 있습니다.

[!code-sql[Main](sorting-custom-paged-data-cs/samples/sample2.sql)]

불행 하지만 매개 변수가 있는 `ORDER BY` 절은 허용 되지 않습니다. 대신 `@sortExpression` 입력 매개 변수를 허용 하는 저장 프로시저를 만들어야 하지만 다음 해결 방법 중 하나를 사용 합니다.

- 사용할 수 있는 각 정렬 식에 대해 하드 코드 된 쿼리를 작성 합니다. 그런 다음 `IF/ELSE` T-sql 문을 사용 하 여 실행할 쿼리를 결정 합니다.
- `CASE` 문을 사용 하 여 `@sortExpressio` n 입력 매개 변수를 기반으로 동적 `ORDER BY` 식을 제공 합니다. 자세한 내용은 [SQL `CASE` 문의 기능](http://www.4guysfromrolla.com/webtech/102704-1.shtml) 에서 동적으로 쿼리 결과를 정렬 하는 데 사용 되는 섹션을 참조 하세요.
- 저장 프로시저에서 적절 한 쿼리를 문자열로 만든 다음 [`sp_executesql` 시스템 저장 프로시저](https://msdn.microsoft.com/library/ms188001.aspx) 를 사용 하 여 동적 쿼리를 실행 합니다.

이러한 각 해결 방법에는 몇 가지 단점이 있습니다. 첫 번째 옵션은 가능한 각 정렬 식에 대해 쿼리를 만들어야 하므로 다른 두 옵션으로 유지 관리할 수 없습니다. 따라서 나중에 GridView에 정렬 가능한 새 필드를 추가 하기로 결정 한 경우에는 돌아가서 저장 프로시저를 업데이트 해야 합니다. 두 번째 접근 방식에는 문자열이 아닌 데이터베이스 열을 기준으로 정렬할 때 성능 문제를 야기 하 고 첫 번째와 동일한 유지 관리 문제를 발생 시킬 수 있는 일부 미묘한 기능이 있습니다. 그리고 동적 SQL을 사용 하는 세 번째 선택 항목은 공격자가 선택한 입력 매개 변수 값을 전달 하는 저장 프로시저를 실행할 수 있는 경우 SQL 삽입 공격에 대 한 위험을 발생 시킵니다.

이러한 방법 중에 완벽 한 것은 아니지만 세 번째 옵션은 세 가지 중에서 가장 좋은 방법 이라고 생각 하면 됩니다. 동적 SQL을 사용 하면 다른 두 가지 방법으로는 불가능 한 수준의 유연성을 제공 합니다. 또한 공격자가 선택한 입력 매개 변수를 전달 하는 저장 프로시저를 실행할 수 있는 경우에만 SQL 삽입 공격이 악용 될 수 있습니다. DAL은 매개 변수가 있는 쿼리를 사용 하므로 ADO.NET는 아키텍처를 통해 데이터베이스에 전송 되는 매개 변수를 보호 합니다. 즉, 공격자가 저장 프로시저를 직접 실행할 수 있는 경우에만 SQL 삽입 공격 취약성이 존재 합니다.

이 기능을 구현 하려면 `GetProductsPagedAndSorted`라는 Northwind 데이터베이스에 새 저장 프로시저를 만듭니다. 이 저장 프로시저는 결과를 정렬 하 고 `OVER` 절에서 `ORDER BY` 텍스트 바로 뒤에 삽입 하는 방법을 지정 하는 `nvarchar(100`형식의 입력 매개 변수인 `@sortExpression`라는 세 개의 입력 매개 변수를 허용 해야 합니다. 그리고 `@startRowIndex` 및 `@maximumRows`이전 자습서에서 검사 한 `GetProductsPaged` 저장 프로시저와 동일한 두 개의 정수 입력 매개 변수입니다. 다음 스크립트를 사용 하 여 `GetProductsPagedAndSorted` 저장 프로시저를 만듭니다.

[!code-sql[Main](sorting-custom-paged-data-cs/samples/sample3.sql)]

저장 프로시저는 `@sortExpression` 매개 변수의 값이 지정 되어 있는지 확인 하 여 시작 합니다. 누락 된 경우 결과에 `ProductID`순위가 매겨집니다. 다음으로, 동적 SQL 쿼리가 생성 됩니다. 여기에서 동적 SQL 쿼리는 Products 테이블에서 모든 행을 검색 하는 데 사용 되는 이전 쿼리와 약간 다릅니다. 이전 예제에서는 하위 쿼리를 사용 하 여 각 제품에 연결 된 범주와 공급 업체 이름을 얻었습니다. 이러한 결정은 [데이터 액세스 계층 만들기](../introduction/creating-a-data-access-layer-cs.md) 자습서에 다시 적용 되었으며, TableAdapter는 이러한 쿼리에 대 한 연결 된 insert, update 및 delete 메서드를 자동으로 만들 수 없기 때문에 `JOIN` s를 사용 하는 대신 수행 되었습니다. 그러나 `GetProductsPagedAndSorted` 저장 프로시저는 범주 또는 공급자 이름을 기준으로 결과를 정렬 하려면 `JOIN`를 사용 해야 합니다.

이 동적 쿼리는 정적 쿼리 부분과 `@sortExpression`, `@startRowIndex`및 `@maximumRows` 매개 변수를 연결 하 여 작성 됩니다. `@startRowIndex` 및 `@maximumRows`는 정수 매개 변수 이므로 올바르게 연결 되려면 nvarchars로 변환 해야 합니다. 이 동적 SQL 쿼리를 생성 한 후에는 `sp_executesql`를 통해 실행 됩니다.

`@sortExpression`, `@startRowIndex`및 `@maximumRows` 매개 변수에 대해 서로 다른 값을 사용 하 여이 저장 프로시저를 테스트 합니다. 서버 탐색기에서 저장 프로시저 이름을 마우스 오른쪽 단추로 클릭 하 고 실행을 선택 합니다. 그러면 입력 매개 변수를 입력할 수 있는 저장 프로시저 실행 대화 상자가 표시 됩니다 (그림 1 참조). 범주 이름을 기준으로 결과를 정렬 하려면 `@sortExpression` 매개 변수 값으로 범주를 사용 합니다. 공급 업체 회사 이름을 기준으로 정렬 하려면 CompanyName을 사용 합니다. 매개 변수 값을 제공한 후 확인을 클릭 합니다. 결과는 출력 창에 표시 됩니다. 그림 2에서는 `UnitPrice` 기준으로 내림차순으로 정렬 하는 경우 11부터 20 까지의 제품을 반환할 때의 결과를 보여 줍니다.

![저장 프로시저의 세 입력 매개 변수에 대해 다른 값을 시도 합니다.](sorting-custom-paged-data-cs/_static/image1.png)

**그림 1**: 저장 프로시저의 세 가지 입력 매개 변수에 대해 다른 값 시도

[저장 프로시저의 결과 ![출력 창에 표시 됩니다.](sorting-custom-paged-data-cs/_static/image3.png)](sorting-custom-paged-data-cs/_static/image2.png)

**그림 2**: 출력 창에 저장 프로시저 결과가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](sorting-custom-paged-data-cs/_static/image4.png)).

> [!NOTE]
> `OVER` 절에서 지정 된 `ORDER BY` 열을 기준으로 결과를 순위를 지정 하는 경우 SQL Server 결과를 정렬 해야 합니다. 이는 결과를 정렬 하는 열에 대 한 클러스터형 인덱스가 있는 경우 또는 포함 하는 인덱스가 있는 경우 빠른 작업이 며 그렇지 않은 경우 비용이 더 많이 들 수 있습니다. 충분 한 크기의 쿼리에 대 한 성능을 향상 시키려면에서 결과의 순서를 지정 하는 열에 대해 비클러스터형 인덱스를 추가 하는 것이 좋습니다. 자세한 내용은 [SQL Server 2005의 순위 함수 및 성능](http://www.sql-server-performance.com/ak_ranking_functions.asp) 을 참조 하세요.

## <a name="step-2-augmenting-the-data-access-and-business-logic-layers"></a>2 단계: 데이터 액세스 및 비즈니스 논리 계층 확대

`GetProductsPagedAndSorted` 저장 프로시저를 만든 후 다음 단계는 응용 프로그램 아키텍처를 통해 저장 프로시저를 실행 하는 수단을 제공 하는 것입니다. 여기에는 DAL 및 BLL 모두에 적절 한 메서드를 추가 하는 것이 수반 됩니다. DAL에 메서드를 추가 하 여를 시작 하겠습니다. `Northwind.xsd` 형식화 된 데이터 집합을 열고 `ProductsTableAdapter`을 마우스 오른쪽 단추로 클릭 한 다음 상황에 맞는 메뉴에서 쿼리 추가 옵션을 선택 합니다. 이전 자습서에서와 같이 기존 저장 프로시저를 사용 하도록이 새 DAL 메서드를 구성 하려고 합니다 .이 경우에는 `GetProductsPagedAndSorted`합니다. 새 TableAdapter 메서드에서 기존 저장 프로시저를 사용 하도록 하는 것부터 시작 합니다.

![기존 저장 프로시저를 사용 하도록 선택](sorting-custom-paged-data-cs/_static/image5.png)

**그림 3**: 기존 저장 프로시저를 사용 하도록 선택

사용할 저장 프로시저를 지정 하려면 다음 화면의 드롭다운 목록에서 `GetProductsPagedAndSorted` 저장 프로시저를 선택 합니다.

![GetProductsPagedAndSorted 저장 프로시저 사용](sorting-custom-paged-data-cs/_static/image6.png)

**그림 4**: GetProductsPagedAndSorted 저장 프로시저 사용

이 저장 프로시저는 레코드 집합을 결과로 반환 하므로 다음 화면에서 테이블 형식 데이터를 반환 함을 표시 합니다.

![저장 프로시저에서 테이블 형식 데이터를 반환 함을 나타냄](sorting-custom-paged-data-cs/_static/image7.png)

**그림 5**: 저장 프로시저에서 테이블 형식 데이터를 반환 함을 나타냄

마지막으로 DataTable 채우기와 DataTable 패턴 반환을 모두 사용 하 여 `FillPagedAndSorted` 및 `GetProductsPagedAndSorted`메서드의 이름을 지정 하는 DAL 메서드를 만듭니다.

![메서드 이름 선택](sorting-custom-paged-data-cs/_static/image8.png)

**그림 6**: 메서드 이름 선택

이제 DAL을 확장 했으므로 BLL로 다시 전환할 준비가 되었습니다. `ProductsBLL` 클래스 파일을 열고 `GetProductsPagedAndSorted`새 메서드를 추가 합니다. 이 메서드는 `sortExpression`, `startRowIndex`및 `maximumRows`의 입력 매개 변수 3 개를 수락 해야 하며, 다음과 같이 DAL s `GetProductsPagedAndSorted` 메서드를 호출 해야 합니다.

[!code-csharp[Main](sorting-custom-paged-data-cs/samples/sample4.cs)]

## <a name="step-3-configuring-the-objectdatasource-to-pass-in-the-sortexpression-parameter"></a>3 단계: SortExpression 매개 변수를 전달 하도록 ObjectDataSource 구성

`GetProductsPagedAndSorted` 저장 프로시저를 사용 하는 메서드를 포함 하도록 DAL 및 BLL을 확장 하는 것은 `SortParameter.aspx` 페이지에서 ObjectDataSource를 구성 하 여 새 BLL 메서드를 사용 하 고 사용자가 결과 정렬을 요청한 열을 기반으로 `SortExpression` 매개 변수를 전달 하는 것입니다.

먼저 ObjectDataSource s `SelectMethod` `GetProductsPaged`에서 `GetProductsPagedAndSorted`로 변경 합니다. 이 작업은 데이터 소스 구성 마법사, 속성 창 또는 선언적 구문을 통해 직접 수행할 수 있습니다. 다음으로, ObjectDataSource s [`SortParameterName` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.sortparametername.aspx)의 값을 제공 해야 합니다. 이 속성이 설정 된 경우 ObjectDataSource는 GridView s `SortExpression` 속성을 `SelectMethod`전달 하려고 시도 합니다. 특히 ObjectDataSource는 이름이 `SortParameterName` 속성의 값과 같은 입력 매개 변수를 찾습니다. BLL s `GetProductsPagedAndSorted` 메서드에 `sortExpression`라는 정렬 식 입력 매개 변수가 있으므로 ObjectDataSource s `SortExpression` 속성을 sortExpression로 설정 합니다.

이러한 두 가지 변경을 수행한 후에는 ObjectDataSource의 선언 구문이 다음과 같이 표시 됩니다.

[!code-aspx[Main](sorting-custom-paged-data-cs/samples/sample5.aspx)]

> [!NOTE]
> 앞의 자습서와 마찬가지로, ObjectDataSource의 SelectParameters 컬렉션에 sortExpression, startRowIndex 또는 maximumRows 입력 매개 변수를 포함 *하지* 않는지 확인 합니다.

GridView에서 정렬을 사용 하도록 설정 하려면 gridview의 스마트 태그에서 정렬 사용 확인란을 선택 하면 됩니다. 그러면 gridview s의 `AllowSorting` 속성이 `true`로 설정 되 고 각 열에 대 한 머리글 텍스트가 LinkButton로 렌더링 됩니다. 최종 사용자가 Linkbutton 헤더 중 하나를 클릭 하면 다시 게시 ensues 및 다음 단계가 수행 됩니다.

1. GridView는 [`SortExpression` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sortexpression.aspx) 을 머리글 링크를 클릭 한 필드의 `SortExpression` 값으로 업데이트 합니다.
2. ObjectDataSource는 `GetProductsPagedAndSorted` 메서드를 호출 하 고, GridView s `SortExpression` 속성을 해당 `startRowIndex` 및 `maximumRows` 입력 매개 변수 값과 함께 메서드 `sortExpression` 입력 매개 변수에 대 한 값으로 전달 합니다.
3. BLL은 DAL s `GetProductsPagedAndSorted` 메서드를 호출 합니다.
4. DAL은 `GetProductsPagedAndSorted` 저장 프로시저를 실행 하 여 `@startRowIndex` 및 `@maximumRows` 입력 매개 변수 값과 함께 `@sortExpression` 매개 변수를 전달 합니다.
5. 저장 프로시저는 데이터의 적절 한 하위 집합을 BLL로 반환 하 여이를 ObjectDataSource로 반환 합니다. 그런 다음이 데이터는 GridView에 바인딩되고 HTML로 렌더링 된 다음 최종 사용자에 게 전송 됩니다.

그림 7은 `UnitPrice`를 기준으로 오름차순으로 정렬 된 결과의 첫 번째 페이지를 보여 줍니다.

[단가를 기준으로 결과를 정렬 ![](sorting-custom-paged-data-cs/_static/image10.png)](sorting-custom-paged-data-cs/_static/image9.png)

**그림 7**: 결과는 단가를 기준으로 정렬 됩니다 ([전체 크기 이미지를 보려면 클릭](sorting-custom-paged-data-cs/_static/image11.png)).

현재 구현에서는 제품 이름, 범주 이름, 단위당 수량 및 단가를 기준으로 결과를 올바르게 정렬할 수 있지만 공급자 이름을 기준으로 결과를 정렬 하려고 하면 런타임 예외가 발생 합니다 (그림 8 참조).

![공급자를 기준으로 결과를 정렬 하려고 하면 다음 런타임 예외가 발생 합니다.](sorting-custom-paged-data-cs/_static/image12.png)

**그림 8**: 공급자를 기준으로 결과를 정렬 하려고 하면 다음 런타임 예외가 발생 합니다.

이 예외는 GridView s `SupplierName` BoundField의 `SortExpression` `SupplierName`로 설정 되어 있기 때문에 발생 합니다. 그러나 `Suppliers` 테이블의 공급자 이름은 실제로이 열 이름에 `SupplierName`로 별칭이 지정 `CompanyName` 이라고 합니다. 그러나 `ROW_NUMBER()` 함수에서 사용 하는 `OVER` 절은 별칭을 사용할 수 없으며 실제 열 이름을 사용 해야 합니다. 따라서 `SupplierName` BoundField s `SortExpression`를 SupplierName에서 CompanyName으로 변경 합니다 (그림 9 참조). 그림 10에 표시 된 것 처럼이 변경 후에는 공급자를 기준으로 결과를 정렬할 수 있습니다.

![SupplierName BoundField s SortExpression를 CompanyName으로 변경](sorting-custom-paged-data-cs/_static/image13.png)

**그림 9**: SupplierName BoundField s SortExpression를 CompanyName으로 변경

[이제 공급자를 기준으로 결과를 정렬할 수 ![](sorting-custom-paged-data-cs/_static/image15.png)](sorting-custom-paged-data-cs/_static/image14.png)

**그림 10**: 이제 공급자를 기준으로 결과를 정렬할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](sorting-custom-paged-data-cs/_static/image16.png)).

## <a name="summary"></a>요약

이전 자습서에서 검사 한 사용자 지정 페이징 구현은 디자인 타임에 결과를 정렬 하는 순서를 지정 해야 했습니다. 즉, 구현 된 사용자 지정 페이징 구현이 동시에 정렬 기능을 제공할 수 없습니다. 이 자습서에서는 결과를 정렬할 수 있는 `@sortExpression` 입력 매개 변수를 포함 하도록 첫 번째에서 저장 프로시저를 확장 하 여 이러한 제한을 극복 했습니다 합니다.

이 저장 프로시저를 만들고 DAL 및 BLL에서 새 메서드를 만든 후 GridView의 현재 `SortExpression` 속성을 BLL `SelectMethod`에 전달 하도록 ObjectDataSource를 구성 하 여 정렬과 사용자 지정 페이징을 모두 제공 하는 GridView를 구현할 수 있었습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Carlos Santos입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](efficiently-paging-through-large-amounts-of-data-cs.md)
> [다음](creating-a-customized-sorting-user-interface-cs.md)
