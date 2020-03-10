---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/updating-the-tableadapter-to-use-joins-vb
title: 조인을 사용 하도록 TableAdapter 업데이트 (VB) | Microsoft Docs
author: rick-anderson
description: 데이터베이스로 작업 하는 경우 여러 테이블에 분산 된 데이터를 요청 하는 것이 일반적입니다. 서로 다른 두 테이블에서 데이터를 검색 하려면 다음 중 하나를 사용할 수 있습니다.
ms.author: riande
ms.date: 07/18/2007
ms.assetid: e624a3e0-061b-4efc-8b0e-5877f9ff6714
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/updating-the-tableadapter-to-use-joins-vb
msc.type: authoredcontent
ms.openlocfilehash: 5c94baa99b126cdd24d69afc3d02bfe8b069419b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78427529"
---
# <a name="updating-the-tableadapter-to-use-joins-vb"></a>JOIN을 사용하도록 TableAdapter 업데이트(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_69_VB.zip) 또는 [PDF 다운로드](updating-the-tableadapter-to-use-joins-vb/_static/datatutorial69vb1.pdf)

> 데이터베이스로 작업 하는 경우 여러 테이블에 분산 된 데이터를 요청 하는 것이 일반적입니다. 서로 다른 두 테이블에서 데이터를 검색 하려면 상관 하위 쿼리 또는 조인 작업을 사용할 수 있습니다. 이 자습서에서는 기본 쿼리에 조인을 포함 하는 TableAdapter를 만드는 방법을 확인 하기 전에 상호 관련 된 하위 쿼리 및 조인 구문을 비교 합니다.

## <a name="introduction"></a>소개

관계형 데이터베이스를 사용 하는 데 관심이 있는 데이터가 여러 테이블에 분산 되는 경우가 많습니다. 예를 들어 제품 정보를 표시 하는 경우 각 제품의 해당 범주와 공급 업체 이름을 나열 하는 것이 좋습니다. `Products` 테이블에는 `CategoryID` 및 `SupplierID` 값이 있지만 실제 범주 및 공급자 이름은 각각 `Categories` 및 `Suppliers` 테이블에 있습니다.

관련 된 다른 테이블에서 정보를 검색 하기 위해 상호 관련 된 *하위 쿼리* 또는 `JOIN`*s*를 사용할 수 있습니다. 상관 하위 쿼리는 외부 쿼리의 열을 참조 하는 중첩 된 `SELECT` 쿼리입니다. 예를 들어 [데이터 액세스 계층 만들기](../introduction/creating-a-data-access-layer-vb.md) 자습서에서는 `ProductsTableAdapter` 주 쿼리에서 두 개의 상호 관련 된 하위 쿼리를 사용 하 여 각 제품에 대 한 범주 및 공급자 이름을 반환 했습니다. `JOIN`는 서로 다른 두 테이블의 관련 행을 병합 하는 SQL 구문입니다. [SqlDataSource 컨트롤을 사용 하 여 데이터 쿼리](../accessing-the-database-directly-from-an-aspnet-page/querying-data-with-the-sqldatasource-control-vb.md) 자습서에서 `JOIN`를 사용 하 여 각 제품과 함께 범주 정보를 표시 합니다.

Tableadapter와 `JOIN` s를 사용 하는 것의 이유는 TableAdapter s 마법사의 제한으로 인해 해당 `INSERT`, `UPDATE`및 `DELETE` 문을 자동으로 생성 하는 것입니다. 구체적으로 말하면 TableAdapter s 주 쿼리에 `JOIN` s가 포함 되어 있으면 TableAdapter는 `InsertCommand`, `UpdateCommand`및 `DeleteCommand` 속성에 대해 임시 SQL 문이나 저장 프로시저를 자동으로 만들 수 없습니다.

이 자습서에서는 기본 쿼리에 `JOIN`를 포함 하는 TableAdapter를 만드는 방법을 살펴보기 전에 상호 관련 된 하위 쿼리 및 `JOIN` s를 간략하게 비교 합니다.

## <a name="comparing-and-contrasting-correlated-subqueries-andjoin-s"></a>상관 관계 하위 쿼리 및`JOIN` s 비교 및 대조

`Northwind` 데이터 집합의 첫 번째 자습서에서 만든 `ProductsTableAdapter`는 상호 관련 된 하위 쿼리를 사용 하 여 각 제품의 해당 범주와 공급자 이름을 다시 가져옵니다. `ProductsTableAdapter` s 주 쿼리는 다음과 같습니다.

[!code-sql[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample1.sql)]

두 개의 상호 관련 된 하위 쿼리 `(SELECT CategoryName FROM Categories WHERE Categories.CategoryID = Products.CategoryID)`와 `(SELECT CompanyName FROM Suppliers WHERE Suppliers.SupplierID = Products.SupplierID)`는 외부 `SELECT` statement의 열 목록에 추가 열로 제품별 단일 값을 반환 하는 `SELECT` 쿼리입니다.

또는 각 제품의 공급 업체와 범주 이름을 반환 하는 데 `JOIN`를 사용할 수 있습니다. 다음 쿼리는 위와 같은 출력을 반환 하지만 하위 쿼리 대신 `JOIN` s를 사용 합니다.

[!code-sql[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample2.sql)]

`JOIN`는 특정 조건에 따라 한 테이블의 레코드를 다른 테이블의 레코드와 병합 합니다. 예를 들어 위의 쿼리에서 `LEFT JOIN Categories ON Categories.CategoryID = Products.CategoryID`은 각 제품 레코드를 `CategoryID` 값이 제품 `CategoryID` 값과 일치 하는 범주 레코드와 병합 하도록 SQL Server에 지시 합니다. 병합 된 결과를 사용 하면 각 제품에 해당 하는 범주 필드를 사용할 수 있습니다 (예: `CategoryName`).

> [!NOTE]
> `JOIN`은 관계형 데이터베이스에서 데이터를 쿼리할 때 주로 사용 됩니다. `JOIN` 구문이 처음 이거나 해당 사용에 대해 약간의 작업을 수행 해야 하는 경우 [W3 학교](http://www.w3schools.com/)에서 [SQL 조인 자습서](http://www.w3schools.com/sql/sql_join.asp) 를 수행 하는 것이 좋습니다. 또한 [SQL 온라인 설명서](https://msdn.microsoft.com/library/ms130214.aspx)의 [`JOIN` 기본](https://msdn.microsoft.com/library/ms191517.aspx) 사항 및 [하위 쿼리 기본](https://msdn.microsoft.com/library/ms189575.aspx) 단원을 참조 하십시오.

`JOIN` 및 상관 관계가 지정 된 하위 쿼리를 사용 하 여 다른 테이블에서 관련 된 데이터를 검색할 수 있으므로 많은 개발자가 해당 헤드를 사실일 사용할 방법을 궁금할 수 있습니다. 거의 동일한 작업을 수행 하는 모든 SQL 전문가는 거의 동일한 작업을 수행 했습니다. SQL Server는 거의 동일한 실행 계획을 생성 합니다. 그러면 사용자와 팀이 가장 편한 기법을 사용 하는 것이 좋습니다. 이는 imparting 후에 이러한 전문가가 상관 관계가 지정 된 하위 쿼리를 통해 `JOIN` s의 기본 설정을 즉시 표현 한다는 것을 설명 합니다.

형식화 된 데이터 집합을 사용 하 여 데이터 액세스 계층을 빌드하는 경우에는 하위 쿼리를 사용할 때 도구가 더 잘 작동 합니다. 특히 TableAdapter s 마법사는 주 쿼리에 `JOIN` s가 포함 되어 있지만 상호 관련 된 하위 쿼리가 사용 될 때 이러한 문을 자동으로 생성 하는 경우 해당 `INSERT`, `UPDATE`및 `DELETE` 문을 자동으로 생성 하지 않습니다.

이 단점을 탐색 하려면 `~/App_Code/DAL` 폴더에 임시 형식의 데이터 집합을 만듭니다. TableAdapter 구성 마법사 중에 임시 SQL 문을 사용 하도록 선택 하 고 다음 `SELECT` 쿼리를 입력 합니다 (그림 1 참조).

[!code-sql[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample3.sql)]

[조인을 포함 하는 주 쿼리를 입력 ![](updating-the-tableadapter-to-use-joins-vb/_static/image2.png)](updating-the-tableadapter-to-use-joins-vb/_static/image1.png)

**그림 1**: `JOIN` s를 포함 하는 기본 쿼리 입력 ([전체 크기 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-vb/_static/image3.png))

기본적으로 TableAdapter는 주 쿼리에 따라 `INSERT`, `UPDATE`및 `DELETE` 문을 자동으로 만듭니다. 고급 단추를 클릭 하면이 기능을 사용할 수 있는 것을 볼 수 있습니다. 이 설정에도 불구 하 고 주 쿼리에 `JOIN`가 포함 되어 있으므로 TableAdapter가 `INSERT`, `UPDATE`및 `DELETE` 문을 만들 수 없습니다.

![조인이 포함 된 기본 쿼리 입력](updating-the-tableadapter-to-use-joins-vb/_static/image4.png)

**그림 2**: `JOIN` s를 포함 하는 기본 쿼리 입력

마침을 클릭하여 마법사를 완료합니다. 이 시점에서 데이터 집합의 디자이너에는 `SELECT` query s 열 목록에 반환 된 각 필드에 대 한 열이 있는 DataTable이 포함 된 단일 TableAdapter가 포함 됩니다. 여기에는 그림 3에 나와 있는 것 처럼 `CategoryName` 및 `SupplierName`포함 됩니다.

![DataTable에는 열 목록에 반환 된 각 필드에 대 한 열이 포함 되어 있습니다.](updating-the-tableadapter-to-use-joins-vb/_static/image5.png)

**그림 3**: DataTable에는 열 목록에 반환 된 각 필드에 대 한 열이 포함 되어 있습니다.

DataTable에 적절 한 열이 있지만 TableAdapter에는 `InsertCommand`, `UpdateCommand`및 `DeleteCommand` 속성에 대 한 값이 부족 합니다. 이를 확인 하려면 디자이너에서 TableAdapter를 클릭 한 다음 속성 창로 이동 합니다. `InsertCommand`, `UpdateCommand`및 `DeleteCommand` 속성이 (없음)로 설정 된 것을 볼 수 있습니다.

[InsertCommand, UpdateCommand 및 DeleteCommand 속성을 (없음)으로 설정 ![](updating-the-tableadapter-to-use-joins-vb/_static/image7.png)](updating-the-tableadapter-to-use-joins-vb/_static/image6.png)

**그림 4**: `InsertCommand`, `UpdateCommand`및 `DeleteCommand` 속성이 (없음)로 설정 됨 ([전체 크기 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-vb/_static/image8.png))

이 단점을 해결 하기 위해 속성 창를 통해 `InsertCommand`, `UpdateCommand`및 `DeleteCommand` 속성에 대 한 SQL 문과 매개 변수를 수동으로 제공할 수 있습니다. 또는 `JOIN` s를 포함 *하지 않도록* TableAdapter s 주 쿼리를 구성 하 여 시작할 수 있습니다. 이렇게 하면 `INSERT`, `UPDATE`및 `DELETE` 문을 자동으로 생성할 수 있습니다. 마법사를 완료 한 후에는 `JOIN` 구문이 포함 되도록 속성 창에서 TableAdapter s `SelectCommand`를 수동으로 업데이트할 수 있습니다.

이 방법이 작동 하는 반면, 마법사를 통해 TableAdapter 주 쿼리가 다시 구성 될 때마다 자동 생성 된 `INSERT``UPDATE`및 `DELETE` 문이 다시 만들어지기 때문에 임시 SQL 쿼리를 사용할 때 매우 불안정. 즉, TableAdapter를 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 구성을 선택한 다음 마법사를 다시 완료 하면 나중에 수행 된 모든 사용자 지정 항목이 손실 됩니다.

TableAdapter s 자동 생성 `INSERT`, `UPDATE`및 `DELETE` 문의 brittleness는 다행히도 임시 SQL 문으로 제한 됩니다. TableAdapter에서 저장 프로시저를 사용 하는 경우 저장 프로시저를 수정 하지 않아도 `SelectCommand`, `InsertCommand`, `UpdateCommand`또는 `DeleteCommand` 저장 프로시저를 사용자 지정 하 고 TableAdapter 구성 마법사를 다시 실행할 수 있습니다.

다음 몇 가지 단계를 수행 하는 경우 처음에는 해당 insert, update 및 delete 저장 프로시저를 자동으로 생성 하도록 `JOIN` s를 생략 하는 주 쿼리를 사용 하는 TableAdapter를 만들게 됩니다. 그런 다음 관련 테이블에서 추가 열을 반환 하는 `JOIN`을 사용 하도록 `SelectCommand`를 업데이트 합니다. 마지막으로, 해당 비즈니스 논리 계층 클래스를 만들고 ASP.NET 웹 페이지에서 TableAdapter를 사용 하는 방법을 보여 줍니다.

## <a name="step-1-creating-the-tableadapter-using-a-simplified-main-query"></a>1 단계: 간소화 된 기본 쿼리를 사용 하 여 TableAdapter 만들기

이 자습서에서는 `NorthwindWithSprocs` 데이터 집합의 `Employees` 테이블에 대해 TableAdapter 및 강력한 형식의 DataTable을 추가 합니다. `Employees` 테이블에는 직원의 관리자 `EmployeeID` 지정 하는 `ReportsTo` 필드가 있습니다. 예를 들어 직원 황 수는 `ReportTo` 값이 5이 고,이는 선하라의 `EmployeeID`입니다. 따라서 황 병은 관리자에 게 보고 합니다. 각 직원의 `ReportsTo` 값을 보고 하는 것과 함께 해당 관리자의 이름을 검색할 수도 있습니다. `JOIN`를 사용 하 여이를 수행할 수 있습니다. 그러나 처음 TableAdapter를 만들 때 `JOIN`를 사용 하면 마법사가 해당 삽입, 업데이트 및 삭제 기능을 자동으로 생성 하지 않습니다. 따라서 주 쿼리는 `JOIN` s를 포함 하지 않는 TableAdapter를 만들어 시작 합니다. 그런 다음 2 단계에서 주 쿼리 저장 프로시저를 업데이트 하 여 `JOIN`를 통해 관리자 이름을 검색 합니다.

먼저 `~/App_Code/DAL` 폴더에서 `NorthwindWithSprocs` 데이터 집합을 엽니다. 디자이너를 마우스 오른쪽 단추로 클릭 하 고, 상황에 맞는 메뉴에서 추가 옵션을 선택 하 고, TableAdapter 메뉴 항목을 선택 합니다. 이렇게 하면 TableAdapter 구성 마법사가 시작 됩니다. 그림 5와 같이 마법사에서 새 저장 프로시저를 만들고 다음을 클릭 합니다. TableAdapter s 마법사에서 새 저장 프로시저를 만드는 방법에 대 한 자세한 내용은 [형식화 된 데이터 집합의 tableadapter 자습서에 대 한 새 저장 프로시저 만들기](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) 를 참조 하세요.

[![새 저장 프로시저 만들기 옵션을 선택 합니다.](updating-the-tableadapter-to-use-joins-vb/_static/image10.png)](updating-the-tableadapter-to-use-joins-vb/_static/image9.png)

**그림 5**: 새 저장 프로시저 만들기 옵션 선택 ([전체 크기 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-vb/_static/image11.png))

TableAdapter 주 쿼리에 대해 다음 `SELECT` 문을 사용 합니다.

[!code-sql[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample4.sql)]

이 쿼리에는 `JOIN` s가 포함 되어 있지 않으므로 TableAdapter 마법사는 주 쿼리를 실행 하는 저장 프로시저 뿐만 아니라 해당 `INSERT`, `UPDATE`및 `DELETE` 문을 사용 하 여 저장 프로시저를 자동으로 만듭니다.

다음 단계를 통해 TableAdapter의 저장 프로시저에 이름을 지정할 수 있습니다. 그림 6에 표시 된 것 처럼 이름 `Employees_Select`, `Employees_Insert`, `Employees_Update`및 `Employees_Delete`를 사용 합니다.

[TableAdapter 저장 프로시저의 이름을 ![합니다.](updating-the-tableadapter-to-use-joins-vb/_static/image13.png)](updating-the-tableadapter-to-use-joins-vb/_static/image12.png)

**그림 6**: TableAdapter의 저장 프로시저 이름 ([전체 크기 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-vb/_static/image14.png))

마지막 단계에서는 TableAdapter의 메서드 이름을 입력 하 라는 메시지를 표시 합니다. `Fill` 및 `GetEmployees`를 메서드 이름으로 사용 합니다. 또한 데이터베이스에 직접 업데이트를 보내는 메서드 만들기 (GenerateDBDirectMethods) 확인란을 선택 된 상태로 두어야 합니다.

[![TableAdapter 메서드 이름 채우기 및 GetEmployees](updating-the-tableadapter-to-use-joins-vb/_static/image16.png)](updating-the-tableadapter-to-use-joins-vb/_static/image15.png)

**그림 7**: TableAdapter의 메서드 이름 `Fill` 및 `GetEmployees` ([전체 크기 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-vb/_static/image17.png))

마법사를 완료 한 후에는 데이터베이스의 저장 프로시저를 잠시 살펴보겠습니다. `Employees_Select`, `Employees_Insert`, `Employees_Update`및 `Employees_Delete`의 네 가지 새 항목이 표시 됩니다. 그런 다음 `EmployeesDataTable`를 검사 하 고 막 만든 `EmployeesTableAdapter` 합니다. DataTable에는 주 쿼리에서 반환 하는 각 필드에 대 한 열이 포함 되어 있습니다. TableAdapter를 클릭 한 다음 속성 창로 이동 합니다. `InsertCommand`, `UpdateCommand`및 `DeleteCommand` 속성이 해당 저장 프로시저를 호출 하도록 올바르게 구성 된 것을 볼 수 있습니다.

[![TableAdapter에 삽입, 업데이트 및 삭제 기능이 포함 되어 있습니다.](updating-the-tableadapter-to-use-joins-vb/_static/image19.png)](updating-the-tableadapter-to-use-joins-vb/_static/image18.png)

**그림 8**: TableAdapter는 삽입, 업데이트 및 삭제 기능을 포함 합니다 ([전체 크기 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-vb/_static/image20.png)).

Insert, update 및 delete 저장 프로시저가 자동으로 생성 되 고 `InsertCommand`, `UpdateCommand`및 `DeleteCommand` 속성이 올바르게 구성 되어 있으면 `SelectCommand`의 저장 프로시저를 사용자 지정 하 여 각 직원의 관리자에 대 한 추가 정보를 반환할 준비가 된 것입니다. 특히 `JOIN`를 사용 하 여 `Employees_Select` 저장 프로시저를 업데이트 하 고 관리자 `FirstName` 및 `LastName` 값을 반환 해야 합니다. 저장 프로시저를 업데이트 한 후에는 이러한 추가 열을 포함 하도록 DataTable을 업데이트 해야 합니다. 2 단계와 3 단계에서 이러한 두 가지 작업을 살펴보겠습니다.

## <a name="step-2-customizing-the-stored-procedure-to-include-ajoin"></a>2 단계: 저장 프로시저를 사용자 지정 하 여`JOIN` 포함

먼저 서버 탐색기로 이동 하 여 Northwind 데이터베이스의 저장 프로시저 폴더로 드릴 다운 하 고 `Employees_Select` 저장 프로시저를 엽니다. 이 저장 프로시저가 표시 되지 않는 경우 저장 프로시저 폴더를 마우스 오른쪽 단추로 클릭 하 고 새로 고침을 선택 합니다. `LEFT JOIN`를 사용 하 여 관리자의 이름과 성을 반환 하도록 저장 프로시저를 업데이트 합니다.

[!code-sql[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample5.sql)]

`SELECT` 문을 업데이트 한 후 파일 메뉴로 이동 하 고 `Employees_Select`저장을 선택 하 여 변경 내용을 저장 합니다. 또는 도구 모음에서 저장 아이콘을 클릭 하거나 Ctrl + S를 누를 수도 있습니다. 변경 내용을 저장 한 후 서버 탐색기에서 `Employees_Select` 저장 프로시저를 마우스 오른쪽 단추로 클릭 하 고 실행을 선택 합니다. 저장 프로시저를 실행 하 고 출력 창에 결과를 표시 합니다 (그림 9 참조).

[저장 프로시저 결과가 ![표시 됩니다 출력 창](updating-the-tableadapter-to-use-joins-vb/_static/image22.png)](updating-the-tableadapter-to-use-joins-vb/_static/image21.png)

**그림 9**: 저장 프로시저 결과가 출력 창 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-vb/_static/image23.png)).

## <a name="step-3-updating-the-datatable-s-columns"></a>3 단계: DataTable의 열 업데이트

이 시점에서 `Employees_Select` 저장 프로시저는 `ManagerFirstName` 및 `ManagerLastName` 값을 반환 하지만 `EmployeesDataTable`에는 이러한 열이 없습니다. 이러한 누락 열은 다음 두 가지 방법 중 하나로 DataTable에 추가할 수 있습니다.

- **수동으로** -데이터 집합 디자이너에서 DataTable을 마우스 오른쪽 단추로 클릭 하 고 추가 메뉴에서 열을 선택 합니다. 그런 다음 열의 이름을 지정할 수 있으며 그에 따라 속성을 설정할 수 있습니다.
- **자동** -TableAdapter 구성 마법사는 `SelectCommand` 저장 프로시저에 의해 반환 된 필드를 반영 하도록 DataTable의 열을 업데이트 합니다. 임시 SQL 문을 사용 하는 경우 `SelectCommand`가 `JOIN`를 포함 하므로 마법사는 `InsertCommand`, `UpdateCommand`및 `DeleteCommand` 속성도 제거 합니다. 그러나 저장 프로시저를 사용 하는 경우 이러한 명령 속성은 그대로 유지 됩니다.

정보 DataList 및 [파일 업로드](../working-with-binary-files/uploading-files-vb.md) [와 함께 마스터 레코드의 글머리 기호 목록을 사용 하 여 마스터/세부](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb.md) 정보를 포함 하 여 이전 자습서에서 DataTable 열을 수동으로 추가 하는 방법에 대해서는 다음 자습서에서이 프로세스를 다시 자세히 살펴보겠습니다. 그러나이 자습서에서는 TableAdapter 구성 마법사를 통해 자동 접근 방법을 사용 합니다.

`EmployeesTableAdapter`를 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 구성을 선택 하 여 시작 합니다. 그러면 선택, 삽입, 업데이트 및 삭제에 사용 되는 저장 프로시저와 함께 반환 값 및 매개 변수 (있는 경우)를 나열 하는 TableAdapter 구성 마법사가 나타납니다. 그림 10에서는이 마법사를 보여 줍니다. 이제 `Employees_Select` 저장 프로시저가 `ManagerFirstName` 및 `ManagerLastName` 필드를 반환 하는 것을 볼 수 있습니다.

[![Employees_Select 저장 프로시저의 업데이트 된 열 목록이 마법사에 표시 됩니다.](updating-the-tableadapter-to-use-joins-vb/_static/image25.png)](updating-the-tableadapter-to-use-joins-vb/_static/image24.png)

**그림 10**: 마법사에 `Employees_Select` 저장 프로시저에 대 한 업데이트 된 열 목록 표시 ([전체 크기 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-vb/_static/image26.png))

마침을 클릭 하 여 마법사를 완료 합니다. 데이터 집합 디자이너로 반환 될 때 `EmployeesDataTable`에 `ManagerFirstName` 및 `ManagerLastName`라는 두 개의 추가 열이 포함 됩니다.

[EmployeesDataTable에 새 열이 두 개 포함 된 ![](updating-the-tableadapter-to-use-joins-vb/_static/image28.png)](updating-the-tableadapter-to-use-joins-vb/_static/image27.png)

**그림 11**: `EmployeesDataTable`에 새 열 두 개 포함 ([전체 크기 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-vb/_static/image29.png))

업데이트 된 `Employees_Select` 저장 프로시저가 적용 되 고 TableAdapter의 삽입, 업데이트 및 삭제 기능이 여전히 작동 하 고 있음을 보여 주기 위해 사용자가 직원을 보고 삭제할 수 있는 웹 페이지를 만듭니다. 그러나 이러한 페이지를 만들기 전에 먼저 `NorthwindWithSprocs` 데이터 집합에서 직원을 사용 하기 위해 비즈니스 논리 계층에서 새 클래스를 만들어야 합니다. 4 단계에서는 `EmployeesBLLWithSprocs` 클래스를 만듭니다. 5 단계에서는 ASP.NET 페이지에서이 클래스를 사용 합니다.

## <a name="step-4-implementing-the-business-logic-layer"></a>4 단계: 비즈니스 논리 계층 구현

`EmployeesBLLWithSprocs.vb`이라는 `~/App_Code/BLL` 폴더에 새 클래스 파일을 만듭니다. 이 클래스는 기존 `EmployeesBLL` 클래스의 의미 체계를 모방 합니다 .이 클래스는 새로운 메서드를 제공 하 고 `Northwind` 데이터 집합 대신 `NorthwindWithSprocs` 데이터 집합을 사용 합니다. `EmployeesBLLWithSprocs` 클래스에 다음 코드를 추가합니다.

[!code-vb[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample6.vb)]

`EmployeesBLLWithSprocs` 클래스 `Adapter` 속성은 `NorthwindWithSprocs` 데이터 집합 s `EmployeesTableAdapter`의 인스턴스를 반환 합니다. 클래스 `GetEmployees` 및 `DeleteEmployee` 메서드에서 사용 됩니다. `GetEmployees` 메서드는 `EmployeesTableAdapter` s 해당 `GetEmployees` 메서드를 호출 합니다 .이 메서드는 `Employees_Select` 저장 프로시저를 호출 하 고 그 결과를 `EmployeeDataTable`에 채웁니다. `DeleteEmployee` 메서드는 `Employees_Delete` 저장 프로시저를 호출 하는 `EmployeesTableAdapter` s `Delete` 메서드를 호출 합니다.

## <a name="step-5-working-with-the-data-in-the-presentation-layer"></a>5 단계: 프레젠테이션 계층에서 데이터 작업

`EmployeesBLLWithSprocs` 클래스가 완료 되 면 ASP.NET 페이지를 통해 직원 데이터 작업을 수행할 준비가 되었습니다. `AdvancedDAL` 폴더에서 `JOINs.aspx` 페이지를 열고 GridView를 도구 상자에서 디자이너로 끌어 `ID` 속성을 `Employees`로 설정 합니다. 그런 다음 GridView의 스마트 태그에서 표를 `EmployeesDataSource`이라는 새 ObjectDataSource 컨트롤에 바인딩합니다.

`EmployeesBLLWithSprocs` 클래스를 사용 하도록 ObjectDataSource를 구성 하 고, 선택 및 삭제 탭에서 `GetEmployees` 및 `DeleteEmployee` 메서드가 드롭다운 목록에서 선택 되었는지 확인 합니다. 마침을 클릭 하 여 ObjectDataSource s 구성을 완료 합니다.

[EmployeesBLLWithSprocs 클래스를 사용 하도록 ObjectDataSource 구성 ![](updating-the-tableadapter-to-use-joins-vb/_static/image31.png)](updating-the-tableadapter-to-use-joins-vb/_static/image30.png)

**그림 12**: `EmployeesBLLWithSprocs` 클래스를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-vb/_static/image32.png))

[ObjectDataSource에 GetEmployees 및 DeleteEmployee 메서드를 사용 ![](updating-the-tableadapter-to-use-joins-vb/_static/image34.png)](updating-the-tableadapter-to-use-joins-vb/_static/image33.png)

**그림 13**: ObjectDataSource에서 `GetEmployees` 및 `DeleteEmployee` 메서드를 사용 하도록 합니다 ([전체 크기 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-vb/_static/image35.png)).

Visual Studio는 각 `EmployeesDataTable`의 열에 대해 GridView에 BoundField를 추가 합니다. `Title`, `LastName`, `FirstName`, `ManagerFirstName`및 `ManagerLastName`를 제외 하 고 이러한 모든 BoundFields를 제거 하 고 마지막 4 개의 BoundFields에 대 한 `HeaderText` 속성의 이름을 Last name, First Name, Manager s First Name 및 Manager s Last Name으로 바꿉니다.

사용자가이 페이지에서 직원을 삭제할 수 있게 하려면 두 가지를 수행 해야 합니다. 먼저 스마트 태그에서 삭제 사용 옵션을 선택 하 여 삭제 기능을 제공 하도록 GridView에 지시 합니다. 그런 다음 objectdatasource 마법사 (`original_{0}`)에서 설정 된 값을 기본값 (`{0}`)로 설정 하 여 ObjectDataSource s `OldValuesParameterFormatString` 속성을 변경 합니다. 이러한 변경을 수행한 후 GridView와 ObjectDataSource의 선언 태그는 다음과 유사 하 게 표시 됩니다.

[!code-aspx[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample7.aspx)]

브라우저를 통해 방문 하 여 페이지를 테스트 합니다. 그림 14와 같이이 페이지에는 각 직원과 자신의 관리자 이름이 표시 됩니다 (있는 경우).

[Employees_Select 저장 프로시저의 조인 ![관리자의 이름을 반환 합니다.](updating-the-tableadapter-to-use-joins-vb/_static/image37.png)](updating-the-tableadapter-to-use-joins-vb/_static/image36.png)

**그림 14**: `Employees_Select` 저장 프로시저의 `JOIN`에서 관리자 이름 반환 ([전체 크기 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-vb/_static/image38.png))

삭제 단추를 클릭 하면 `Employees_Delete` 저장 프로시저의 실행으로 완료 되는 삭제 워크플로가 시작 됩니다. 그러나 저장 프로시저에서 시도 된 `DELETE` 문은 foreign key 제약 조건 위반으로 인해 실패 합니다 (그림 15 참조). 특히 각 직원은 `Orders` 테이블에 하나 이상의 레코드를 포함 하므로 삭제가 실패 합니다.

[해당 주문이 있는 직원을 삭제 ![Foreign Key 제약 조건 위반이 발생 합니다.](updating-the-tableadapter-to-use-joins-vb/_static/image40.png)](updating-the-tableadapter-to-use-joins-vb/_static/image39.png)

**그림 15**: 해당 주문이 있는 직원을 삭제 하면 Foreign Key 제약 조건 위반이 발생 합니다 ([전체 크기 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-vb/_static/image41.png)).

직원을 삭제할 수 있게 하려면 다음을 수행 합니다.

- Foreign key 제약 조건을 계단식 삭제로 업데이트 합니다.
- 삭제할 직원의 `Orders` 테이블에서 레코드를 수동으로 삭제 하거나
- `Employees_Delete` 저장 프로시저를 업데이트 하 여 먼저 `Employees` 레코드를 삭제 하기 전에 `Orders` 테이블에서 관련 레코드를 삭제 합니다. [형식화 된 데이터 집합의 tableadapter 자습서에서 기존 저장 프로시저를 사용 하](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) 는 방법에 대해 설명 했습니다.

독자를 위한 연습으로 남겨 둡니다.

## <a name="summary"></a>요약

관계형 데이터베이스를 사용 하는 경우 쿼리는 여러 관련 테이블에서 데이터를 가져오는 것이 일반적입니다. 상관 하위 쿼리 및 `JOIN` s는 쿼리에서 관련 테이블의 데이터에 액세스 하는 두 가지 방법을 제공 합니다. 이전 자습서에서는 TableAdapter가 `JOIN` s와 관련 된 쿼리에 대해 `INSERT`, `UPDATE`및 `DELETE` 문을 자동으로 생성할 수 없기 때문에 일반적으로 상관 하위 쿼리를 사용 했습니다. 이러한 값은 수동으로 제공할 수 있지만 임시 SQL 문을 사용 하는 경우 TableAdapter 구성 마법사가 완료 되 면 사용자 지정 항목을 덮어씁니다.

다행히 저장 프로시저를 사용 하 여 만든 Tableadapter는 임시 SQL 문을 사용 하 여 만든 것과 동일한 brittleness를 사용 하지 않습니다. 따라서 주 쿼리에서 저장 프로시저를 사용할 때 `JOIN`를 사용 하는 TableAdapter를 만들 수 있습니다. 이 자습서에서는 이러한 TableAdapter를 만드는 방법에 대해 살펴보았습니다. 해당 insert, update 및 delete 저장 프로시저가 자동으로 생성 되도록 TableAdapter의 주 쿼리에 대해 `JOIN`없는 `SELECT` 쿼리를 사용 하 여 시작 했습니다. TableAdapter의 초기 구성이 완료 되 면 `SelectCommand` 저장 프로시저를 확장 하 여 `JOIN`를 사용 하 고 TableAdapter 구성 마법사를 다시 실행 하 여 `EmployeesDataTable`의 열을 업데이트 합니다.

TableAdapter 구성 마법사를 다시 실행 하면 `Employees_Select` 저장 프로시저에서 반환 된 데이터 필드가 반영 되도록 `EmployeesDataTable` 열이 자동으로 업데이트 됩니다. 또는 이러한 열을 DataTable에 수동으로 추가할 수 있습니다. 다음 자습서에서 DataTable에 열을 수동으로 추가 하는 방법을 살펴보겠습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Hilton Geisenow, David Suru 및 Teresa Murphy입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)
> [다음](adding-additional-datatable-columns-vb.md)
