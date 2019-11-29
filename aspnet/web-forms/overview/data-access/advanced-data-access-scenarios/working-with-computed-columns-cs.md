---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/working-with-computed-columns-cs
title: 계산 열 작업 (C#) | Microsoft Docs
author: rick-anderson
description: 데이터베이스 테이블을 만들 때에는 값이 일반적으로 정의 되는 식에서 계산 되는 계산 열을 정의 하는 Microsoft SQL Server 있습니다.
ms.author: riande
ms.date: 08/03/2007
ms.assetid: 57459065-ed7c-4dfe-ac9c-54c093abc261
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/working-with-computed-columns-cs
msc.type: authoredcontent
ms.openlocfilehash: ad6a96f2721510c2478f707c8eed018ae797f27a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74603169"
---
# <a name="working-with-computed-columns-c"></a>계산 열 작업(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_71_CS.zip) 또는 [PDF 다운로드](working-with-computed-columns-cs/_static/datatutorial71cs1.pdf)

> 데이터베이스 테이블을 만들 때 Microsoft SQL Server은 일반적으로 동일한 데이터베이스 레코드의 다른 값을 참조 하는 식에서 계산 된 값을 갖는 계산 열을 정의할 수 있습니다. 이러한 값은 데이터베이스에서 읽기 전용 이며 Tableadapter를 사용할 때 특별 한 고려 사항이 필요 합니다. 이 자습서에서는 계산 열에서 발생 하는 문제를 충족 하는 방법을 알아봅니다.

## <a name="introduction"></a>소개

Microsoft SQL Server은 일반적으로 동일한 테이블에 있는 다른 열의 값을 참조 하는 식에서 계산 된 값을 갖는 열인 *[계산 열](https://msdn.microsoft.com/library/ms191250.aspx)* 을 허용 합니다. 예를 들어 시간 추적 데이터 모델에는 `ServicePerformed`, `EmployeeID`, `Rate`, `Duration`등의 열이 있는 `ServiceLog` 라는 테이블이 있을 수 있습니다. 웹 페이지나 기타 프로그래밍 인터페이스를 통해 서비스 항목 (요금에 대 한 요금을 곱한 금액)에 따른 금액을 계산할 수 있지만이 정보를 보고 하는 `AmountDue` 라는 `ServiceLog` 테이블에 열을 포함 하는 것이 편리할 수 있습니다. 이 열은 일반 열로 만들 수 있지만 `Rate` 또는 `Duration` 열 값이 변경 될 때마다 업데이트 해야 합니다. 식 `Rate * Duration`를 사용 하 여 `AmountDue` 열을 계산 열로 설정 하는 것이 더 나은 방법입니다. 이렇게 하면 쿼리에서 참조 될 때마다 SQL Server에서 `AmountDue` 열 값을 자동으로 계산 합니다.

계산 열 값은 식에 의해 결정 되므로 이러한 열은 읽기 전용 이므로 `INSERT` 또는 `UPDATE` 문에서 할당 된 값을 가질 수 없습니다. 그러나 계산 열이 임시 SQL 문을 사용 하는 TableAdapter에 대 한 주 쿼리의 일부인 경우 자동 생성 된 `INSERT` 및 `UPDATE` 문에 자동으로 포함 됩니다. 따라서 계산 된 열에 대 한 참조를 제거 하려면 TableAdapter s `INSERT` 및 `UPDATE` 쿼리와 `InsertCommand` 및 `UpdateCommand` 속성을 업데이트 해야 합니다.

임시 SQL 문을 사용 하는 TableAdapter에서 계산 열을 사용 하는 한 가지 문제는 tableadapter 구성 마법사가 완료 될 때마다 TableAdapter s `INSERT` 및 `UPDATE` 쿼리가 자동으로 다시 생성 된다는 것입니다. 따라서 마법사를 다시 실행 하면 `INSERT`에서 수동으로 제거 된 계산 열과 `UPDATE` 쿼리가 다시 나타납니다. 저장 프로시저를 사용 하는 Tableadapter는이 brittleness를 방해 하지 않지만 3 단계에서 해결할 수 있는 고유한 것이 있습니다.

이 자습서에서는 Northwind 데이터베이스의 `Suppliers` 테이블에 계산 열을 추가한 다음이 테이블과 계산 열을 사용 하는 해당 TableAdapter를 만듭니다. Tableadapter 구성 마법사를 사용 하는 경우 사용자 지정이 손실 되지 않도록 TableAdapter에서 임시 SQL 문 대신 저장 프로시저를 사용 합니다.

S를 시작 하겠습니다.

## <a name="step-1-adding-a-computed-column-to-thesupplierstable"></a>1 단계:`Suppliers`테이블에 계산 열 추가

Northwind 데이터베이스에 계산 열이 없으므로 직접 추가 해야 합니다. 이 자습서에서는 `FullContactName` 라는 `Suppliers` 테이블에 계산 열을 추가 하 여 `ContactName` (`ContactTitle`, `CompanyName`) 형식의 담당자 이름, 제목 및 회사를 반환 하는 회사를 반환 합니다. 이 계산 열은 공급자에 대 한 정보를 표시할 때 보고서에서 사용할 수 있습니다.

서버 탐색기에서 `Suppliers` 테이블을 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 테이블 정의 열기를 선택 하 여 `Suppliers` 테이블 정의를 엽니다. 그러면 테이블의 열과 해당 속성 (예: 데이터 형식, `NULL` s 등을 허용할지 여부 등)이 표시 됩니다. 계산 열을 추가 하려면 열 이름을 테이블 정의에 입력 하 여 시작 합니다. 그런 다음 속성 창 열에서 계산 열 사양 섹션 아래의 (수식) 텍스트 상자에 식을 입력 합니다 (그림 1 참조). 계산 열의 이름을 `FullContactName` 하 고 다음 식을 사용 합니다.

[!code-sql[Main](working-with-computed-columns-cs/samples/sample1.sql)]

`+` 연산자를 사용 하 여 SQL에서 문자열을 연결할 수 있습니다. 기존 프로그래밍 언어의 조건 처럼 `CASE` 문을 사용할 수 있습니다. 위의 식에서 `CASE` 문은 다음과 같이 읽을 수 있습니다. `ContactTitle`이 `NULL` 되지 않으면 쉼표와 연결 된 `ContactTitle` 값을 출력 합니다. 그렇지 않으면 아무 것도 내보내지 않습니다. `CASE` 문의 유용성에 대 한 자세한 내용은 [SQL `CASE` 문의 기능](http://www.4guysfromrolla.com/webtech/102704-1.shtml)을 참조 하세요.

> [!NOTE]
> 여기에서 `CASE` 문을 사용 하는 대신 `ISNULL(ContactTitle, '')`를 사용할 수도 있습니다. [`ISNULL(checkExpression, replacementValue)`](https://msdn.microsoft.com/library/ms184325.aspx) 는 NULL이 아닌 경우 *checkexpression* 을 반환 하 고 그렇지 않으면 *replacementValue*를 반환 합니다. 이 인스턴스에서 `ISNULL` 또는 `CASE`는 작동 하지만 `CASE` 문의 유연성이 `ISNULL`일치 하지 않는 복잡 한 시나리오가 있습니다.

이 계산 열을 추가한 후 화면은 그림 1의 스크린샷 처럼 보입니다.

[FullContactName 라는 계산 열을 Suppliers 테이블에 추가 ![](working-with-computed-columns-cs/_static/image2.png)](working-with-computed-columns-cs/_static/image1.png)

**그림 1**: `FullContactName` 라는 계산 열을 `Suppliers` 테이블에 추가 ([전체 크기 이미지를 보려면 클릭](working-with-computed-columns-cs/_static/image3.png))

계산 열의 이름을 지정 하 고 해당 식을 입력 한 후에는 도구 모음에서 저장 아이콘을 클릭 하거나, Ctrl + S를 누르거나, 파일 메뉴로 이동 하 고 `Suppliers`저장을 선택 하 여 변경 내용을 테이블에 저장 합니다.

테이블을 저장 하면 `Suppliers` 테이블의 열 목록에 추가 된 열을 포함 하 여 서버 탐색기를 새로 고쳐야 합니다. 또한 (수식) 텍스트 상자에 입력 된 식이 불필요 한 공백을 제거 하 고 열 이름을 대괄호 (`[]`)로 둘러싸고 괄호를 포함 하 여 작업 순서를 보다 명확 하 게 표시 하는 동등한 식으로 자동 조정 됩니다.

[!code-sql[Main](working-with-computed-columns-cs/samples/sample2.sql)]

Microsoft SQL Server 계산 열에 대 한 자세한 내용은 [기술 문서](https://msdn.microsoft.com/library/ms191250.aspx)를 참조 하세요. 또한 [방법:](https://msdn.microsoft.com/library/ms188300.aspx) 계산 열을 만드는 단계별 연습은 계산 열 지정을 참조 하세요.

> [!NOTE]
> 기본적으로 계산 열은 테이블에 물리적으로 저장 되지 않고 쿼리에서 참조 될 때마다 다시 계산 됩니다. 그러나 유지 됨 확인란을 선택 하면 계산 열을 테이블에 물리적으로 저장 하도록 SQL Server에 지시할 수 있습니다. 이렇게 하면 계산 열에 인덱스를 만들 수 있으므로 해당 `WHERE` 절에서 계산 열 값을 사용 하는 쿼리의 성능을 향상 시킬 수 있습니다. 자세한 내용은 [계산 열에 인덱스 만들기](https://msdn.microsoft.com/library/ms189292.aspx) 를 참조 하세요.

## <a name="step-2-viewing-the-computed-column-s-values"></a>2 단계: 계산 열 값 보기

데이터 액세스 계층에서 작업을 시작 하기 전에 `FullContactName` 값을 확인 하는 데 1 분 정도 걸립니다. 서버 탐색기에서 `Suppliers` 테이블 이름을 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 새 쿼리를 선택 합니다. 그러면 쿼리에 포함할 테이블을 선택 하 라는 메시지를 표시 하는 쿼리 창이 표시 됩니다. `Suppliers` 테이블을 추가 하 고 닫기를 클릭 합니다. 그런 다음 Suppliers 테이블에서 `CompanyName`, `ContactName`, `ContactTitle`및 `FullContactName` 열을 확인 합니다. 마지막으로 도구 모음에서 빨간 느낌표 아이콘을 클릭 하 여 쿼리를 실행 하 고 결과를 확인 합니다.

그림 2에 나와 있는 것 처럼 u 형식을 사용 하 여 `CompanyName`, `ContactName`및 `ContactTitle` 열을 나열 하는 `FullContactName`결과에 포함 됩니다.`ContactName` (`ContactTitle`, `CompanyName`).

[FullContactName ContactName (ContactTitle, CompanyName) 형식을 사용 하는 ![](working-with-computed-columns-cs/_static/image5.png)](working-with-computed-columns-cs/_static/image4.png)

**그림 2**: `ContactName` 형식 (`ContactTitle`, `CompanyName`)을 사용 하 `FullContactName` ([전체 크기 이미지를 보려면 클릭](working-with-computed-columns-cs/_static/image6.png))

## <a name="step-3-adding-thesupplierstableadapterto-the-data-access-layer"></a>3 단계: 데이터 액세스 계층에`SuppliersTableAdapter`추가

응용 프로그램에서 공급자 정보를 사용 하려면 먼저 DAL에서 TableAdapter 및 DataTable을 만들어야 합니다. 이러한 작업은 이전 자습서에서 살펴본 것과 동일한 간단한 단계를 사용 하 여 수행 하는 것이 가장 좋습니다. 그러나 계산 열을 사용 하 여 작업 하는 데는 몇 가지 사항이 있습니다.

임시 SQL 문을 사용 하는 TableAdapter를 사용 하는 경우 tableadapter 구성 마법사를 통해 TableAdapter의 주 쿼리에 계산 열을 간단히 포함할 수 있습니다. 그러나 이렇게 하면 계산 열이 포함 된 `INSERT` 및 `UPDATE` 문이 자동 생성 됩니다. 이러한 메서드 중 하나 `SqlException`를 실행 하려고 하면 열 ColumnName이 계산 열 이거나 UNION 연산자의 결과가 throw 되기 때문에 열 *ColumnName* 을 수정할 수 없습니다. `INSERT` 및 `UPDATE` 문은 TableAdapter의 `InsertCommand` 및 `UpdateCommand` 속성을 통해 수동으로 조정할 수 있지만 TableAdapter 구성 마법사가 다시 실행 될 때마다 이러한 사용자 지정이 손실 됩니다.

임시 SQL 문을 사용 하는 Tableadapter의 brittleness 때문에 계산 열로 작업할 때 저장 프로시저를 사용 하는 것이 좋습니다. 기존 저장 프로시저를 사용 하는 경우 [형식화 된 데이터 집합의 tableadapter 자습서에 대 한 기존 저장 프로시저 사용](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) 의 설명에 따라 tableadapter를 구성 하면 됩니다. 그러나 TableAdapter 마법사에서 저장 프로시저를 만드는 경우에는 처음에 주 쿼리에서 계산 열을 생략 하는 것이 중요 합니다. 주 쿼리에 계산 열을 포함 하는 경우 TableAdapter 구성 마법사가 완료 되 면 해당 저장 프로시저를 만들 수 없다는 알림을 표시 합니다. 간단히 말해서 계산 열을 사용 하지 않는 주 쿼리를 사용 하 여 먼저 TableAdapter를 구성 하 고 해당 저장 프로시저와 TableAdapter s `SelectCommand`를 수동으로 업데이트 하 여 계산 열을 포함 해야 합니다. 이 방법은`JOIN`*s* 자습서를 [사용 하기 위해 TableAdapter를 업데이트](updating-the-tableadapter-to-use-joins-cs.md) 하는 데 사용 되는 방법과 비슷합니다.

이 자습서에서는를 사용 하 여 새 TableAdapter를 추가 하 고 저장 프로시저를 자동으로 만듭니다. 따라서 처음에는 주 쿼리에서 `FullContactName` 계산 열을 생략 해야 합니다.

먼저 `~/App_Code/DAL` 폴더에서 `NorthwindWithSprocs` 데이터 집합을 엽니다. 디자이너를 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 새 TableAdapter를 추가 하도록 선택 합니다. 이렇게 하면 TableAdapter 구성 마법사가 시작 됩니다. 데이터를 쿼리할 데이터베이스 (`NORTHWNDConnectionString` `Web.config`)를 지정 하 고 다음을 클릭 합니다. `Suppliers` 테이블을 쿼리 하거나 수정 하기 위한 저장 프로시저를 아직 만들지 않았기 때문에 새 저장 프로시저 만들기 옵션을 선택 하 여 마법사에서 해당 테이블을 만들고 다음을 클릭 합니다.

[![새 저장 프로시저 만들기 옵션을 선택 합니다.](working-with-computed-columns-cs/_static/image8.png)](working-with-computed-columns-cs/_static/image7.png)

**그림 3**: 새 저장 프로시저 만들기 옵션 선택 ([전체 크기 이미지를 보려면 클릭](working-with-computed-columns-cs/_static/image9.png))

이후 단계에서 주 쿼리를 묻는 메시지를 표시 합니다. 각 공급자에 대 한 `SupplierID`, `CompanyName`, `ContactName`및 `ContactTitle` 열을 반환 하는 다음 쿼리를 입력 합니다. 이 쿼리는 계산 열 (`FullContactName`)을 의도적으로 생략 합니다. 4 단계에서이 열을 포함 하도록 해당 저장 프로시저를 업데이트 합니다.

[!code-sql[Main](working-with-computed-columns-cs/samples/sample3.sql)]

주 쿼리를 입력 하 고 다음을 클릭 하면 마법사에서 생성 되는 네 개의 저장 프로시저 이름을 지정할 수 있습니다. 그림 4에서 보여 주는 것 처럼 이러한 저장 프로시저 `Suppliers_Select`, `Suppliers_Insert`, `Suppliers_Update`및 `Suppliers_Delete`의 이름을로 합니다.

[자동 생성 된 저장 프로시저의 이름을 사용자 지정 ![](working-with-computed-columns-cs/_static/image11.png)](working-with-computed-columns-cs/_static/image10.png)

**그림 4**: 자동 생성 된 저장 프로시저의 이름 사용자 지정 ([전체 크기 이미지를 보려면 클릭](working-with-computed-columns-cs/_static/image12.png))

다음 마법사 단계에서는 TableAdapter의 메서드 이름을 지정 하 고 데이터에 액세스 하 고 업데이트 하는 데 사용 되는 패턴을 지정할 수 있습니다. 세 개의 확인란을 모두 선택 된 상태로 두고 `GetData` 메서드의 이름을 `GetSuppliers`로 바꿉니다. 마침을 클릭하여 마법사를 완료합니다.

[GetData 메서드를 GetSuppliers로 이름 바꾸기 ![](working-with-computed-columns-cs/_static/image14.png)](working-with-computed-columns-cs/_static/image13.png)

**그림 5**: `GetData` 메서드의 이름을 `GetSuppliers` ([전체 크기 이미지를 보려면 클릭](working-with-computed-columns-cs/_static/image15.png))

마침을 클릭 하면 마법사가 4 개의 저장 프로시저를 만들고 TableAdapter 및 해당 DataTable을 형식화 된 데이터 집합에 추가 합니다.

## <a name="step-4-including-the-computed-column-in-the-tableadapter-s-main-query"></a>4 단계: TableAdapter 주 쿼리에 계산 열 포함

이제 `FullContactName` 계산 열을 포함 하도록 3 단계에서 만든 TableAdapter 및 DataTable을 업데이트 해야 합니다. 이 작업은 다음 두 단계로 구성됩니다.

1. `Suppliers_Select` 저장 프로시저를 업데이트 하 여 `FullContactName` 계산 열을 반환 합니다.
2. 해당 `FullContactName` 열을 포함 하도록 DataTable을 업데이트 합니다.

먼저 서버 탐색기로 이동 하 여 저장 프로시저 폴더로 드릴 다운 합니다. `Suppliers_Select` 저장 프로시저를 열고 `FullContactName` 계산 열을 포함 하도록 `SELECT` 쿼리를 업데이트 합니다.

[!code-sql[Main](working-with-computed-columns-cs/samples/sample4.sql)]

도구 모음에서 저장 아이콘을 클릭 하거나, Ctrl + S를 누르거나, 파일 메뉴에서 `Suppliers_Select` 저장 옵션을 선택 하 여 저장 프로시저에 대 한 변경 내용을 저장 합니다.

그런 다음 데이터 집합 디자이너로 돌아가서 `SuppliersTableAdapter`를 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 구성을 선택 합니다. 이제 `Suppliers_Select` 열에는 데이터 열 컬렉션에 `FullContactName` 열이 포함 됩니다.

[TableAdapter s 구성 마법사를 실행 하 여 DataTable의 열을 업데이트 ![](working-with-computed-columns-cs/_static/image17.png)](working-with-computed-columns-cs/_static/image16.png)

**그림 6**: TableAdapter s 구성 마법사를 실행 하 여 DataTable s 열 업데이트 ([전체 크기 이미지를 보려면 클릭](working-with-computed-columns-cs/_static/image18.png))

마침을 클릭하여 마법사를 완료합니다. 그러면 `SuppliersDataTable`에 해당 열이 자동으로 추가 됩니다. TableAdapter 마법사는 `FullContactName` 열이 계산 열 이므로 읽기 전용 임을 감지할 수 있을 정도로 지능적입니다. 따라서 열 s `ReadOnly` 속성을 `true`로 설정 합니다. 이를 확인 하려면 `SuppliersDataTable`에서 열을 선택한 다음 속성 창으로 이동 합니다 (그림 7 참조). `FullContactName` 열 s `DataType` 및 `MaxLength` 속성도 그에 따라 설정 됩니다.

[FullContactName 열이 읽기 전용으로 표시 ![](working-with-computed-columns-cs/_static/image20.png)](working-with-computed-columns-cs/_static/image19.png)

**그림 7**: `FullContactName` 열이 읽기 전용으로 표시 되어 있습니다 ([전체 크기 이미지를 보려면 클릭](working-with-computed-columns-cs/_static/image21.png)).

## <a name="step-5-adding-agetsupplierbysupplieridmethod-to-the-tableadapter"></a>5 단계: TableAdapter에`GetSupplierBySupplierID`메서드 추가

이 자습서에서는 업데이트 가능한 표에 공급 업체를 표시 하는 ASP.NET 페이지를 만듭니다. 이전 자습서에서는 DAL에서 특정 레코드를 강력한 형식의 DataTable로 검색 하 고 해당 속성을 업데이트 한 다음 업데이트 된 DataTable을 다시 DAL으로 전송 하 여 변경 내용을에 전파 함으로써 비즈니스 논리 계층에서 단일 레코드를 업데이트 했습니다. 데이터베이스입니다. 이 첫 번째 단계를 수행 하려면 DAL에서 업데이트 되는 레코드를 검색 합니다. 먼저 `GetSupplierBySupplierID(supplierID)` 메서드를 DAL에 추가 해야 합니다.

데이터 집합 디자인에서 `SuppliersTableAdapter`를 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 쿼리 추가 옵션을 선택 합니다. 3 단계에서와 같이 새 저장 프로시저 만들기 옵션을 선택 하 여 마법사에서 새 저장 프로시저를 생성 하도록 합니다 (이 마법사의 스크린샷에 대해서는 그림 3 참조). 이 메서드는 여러 열이 있는 레코드를 반환 하므로 행을 반환 하는 SELECT 인 SQL 쿼리를 사용 하 고 다음을 클릭 함을 표시 합니다.

[![행을 반환 하는 옵션을 선택 합니다.](working-with-computed-columns-cs/_static/image23.png)](working-with-computed-columns-cs/_static/image22.png)

**그림 8**: 행을 반환 하는 값 선택 옵션 선택 ([전체 크기 이미지를 보려면 클릭](working-with-computed-columns-cs/_static/image24.png))

후속 단계에서는이 메서드에 사용할 쿼리를 묻는 메시지를 표시 합니다. 주 쿼리와 동일한 데이터 필드를 반환 하지만 특정 공급자에 대해 다음을 입력 합니다.

[!code-sql[Main](working-with-computed-columns-cs/samples/sample5.sql)]

다음 화면은 자동 생성 될 저장 프로시저의 이름을 묻는 메시지를 표시 합니다. 이 저장 프로시저의 이름을 `Suppliers_SelectBySupplierID` 하 고 다음을 클릭 합니다.

[저장 프로시저의 이름을 ![Suppliers_SelectBySupplierID](working-with-computed-columns-cs/_static/image26.png)](working-with-computed-columns-cs/_static/image25.png)

**그림 9**: 저장 프로시저의 이름 `Suppliers_SelectBySupplierID` ([전체 크기 이미지를 보려면 클릭](working-with-computed-columns-cs/_static/image27.png))

마지막으로, 마법사에서 TableAdapter에 사용할 데이터 액세스 패턴 및 메서드 이름을 묻는 메시지를 표시 합니다. 두 확인란을 모두 선택 된 상태로 두고 `FillBy` 및 `GetDataBy` 메서드의 이름을 각각 `FillBySupplierID` 및 `GetSupplierBySupplierID`로 바꿉니다.

[![TableAdapter 메서드의 FillBySupplierID 및 GetSupplierBySupplierID 이름](working-with-computed-columns-cs/_static/image29.png)](working-with-computed-columns-cs/_static/image28.png)

**그림 10**: TableAdapter 메서드 이름 `FillBySupplierID` 및 `GetSupplierBySupplierID` ([전체 크기 이미지를 보려면 클릭](working-with-computed-columns-cs/_static/image30.png))

마침을 클릭하여 마법사를 완료합니다.

## <a name="step-6-creating-the-business-logic-layer"></a>6 단계: 비즈니스 논리 계층 만들기

1 단계에서 만든 계산 열을 사용 하는 ASP.NET 페이지를 만들기 전에 먼저 BLL에 해당 메서드를 추가 해야 합니다. 7 단계에서 만든 ASP.NET 페이지를 통해 사용자는 공급자를 보고 편집할 수 있습니다. 따라서 항상 모든 공급 업체를 가져오는 메서드를 제공 하 고 특정 공급자를 업데이트 하는 메서드를 제공 해야 합니다.

`~/App_Code/BLL` 폴더에 `SuppliersBLLWithSprocs` 라는 새 클래스 파일을 만들고 다음 코드를 추가 합니다.

[!code-csharp[Main](working-with-computed-columns-cs/samples/sample6.cs)]

다른 BLL 클래스와 마찬가지로 `SuppliersBLLWithSprocs`에는 `public` 및 `GetSuppliers`의 두 가지 `UpdateSupplier`메서드와 함께 `SuppliersTableAdapter` 클래스의 인스턴스를 반환 하는 `protected` `Adapter` 속성이 있습니다. `GetSuppliers` 메서드는를 호출 하 고 데이터 액세스 계층의 해당 `GetSupplier` 메서드에서 반환 되는 `SuppliersDataTable` 반환 합니다. `UpdateSupplier` 메서드는 DAL s `GetSupplierBySupplierID(supplierID)` 메서드 호출을 통해 업데이트 되는 특정 공급자에 대 한 정보를 검색 합니다. 그런 다음 `CategoryName`, `ContactName`및 `ContactTitle` 속성을 업데이트 하 고, 수정 된 `SuppliersRow` 개체를 전달 하 여 데이터 액세스 계층 `Update` 메서드를 호출 하 여 이러한 변경 내용을 데이터베이스에 커밋합니다.

> [!NOTE]
> `SupplierID` 및 `CompanyName`를 제외 하 고 Suppliers 테이블의 모든 열은 `NULL` 값을 허용 합니다. 따라서 전달 된 `contactName` 또는 `contactTitle` 매개 변수가 `null` 인 경우 각각 `ContactTitle` 및 `NULL` 메서드를 사용 하 여 해당 `ContactName` 및 `SetContactNameNull` 속성을 `SetContactTitleNull` 데이터베이스 값으로 설정 해야 합니다.

## <a name="step-7-working-with-the-computed-column-from-the-presentation-layer"></a>7 단계: 프레젠테이션 계층에서 계산 열 사용

`Suppliers` 테이블에 계산 열이 추가 되 고 DAL 및 BLL이 적절히 업데이트 되 면 `FullContactName` 계산 열을 사용 하는 ASP.NET 페이지를 작성할 준비가 된 것입니다. 먼저 `AdvancedDAL` 폴더에서 `ComputedColumns.aspx` 페이지를 열고 GridView를 도구 상자에서 디자이너로 끌어 옵니다. GridView s `ID` 속성을 `Suppliers`로 설정 하 고 스마트 태그에서 `SuppliersDataSource`라는 새 ObjectDataSource에 바인딩합니다. 6 단계에서 다시 추가한 `SuppliersBLLWithSprocs` 클래스를 사용 하도록 ObjectDataSource를 구성 하 고 다음을 클릭 합니다.

[SuppliersBLLWithSprocs 클래스를 사용 하도록 ObjectDataSource 구성 ![](working-with-computed-columns-cs/_static/image32.png)](working-with-computed-columns-cs/_static/image31.png)

**그림 11**: `SuppliersBLLWithSprocs` 클래스를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](working-with-computed-columns-cs/_static/image33.png))

`SuppliersBLLWithSprocs` 클래스에는 `GetSuppliers` 및 `UpdateSupplier`라는 두 가지 메서드만 정의 되어 있습니다. 이러한 두 가지 방법이 선택 및 업데이트 탭에 각각 지정 되어 있는지 확인 하 고 마침을 클릭 하 여 ObjectDataSource의 구성을 완료 합니다.

데이터 소스 구성 마법사가 완료 되 면 Visual Studio에서 반환 된 각 데이터 필드에 대해 BoundField를 추가 합니다. `SupplierID` BoundField를 제거 하 고 `CompanyName`, `ContactName`, `ContactTitle`및 `FullContactName` BoundFields의 `HeaderText` 속성을 회사, 연락처 이름, 제목 및 전체 연락처 이름으로 변경 합니다. 스마트 태그에서 편집 사용 확인란을 선택 하 여 GridView s 기본 제공 편집 기능을 설정 합니다.

BoundFields를 GridView에 추가 하는 것 외에도 데이터 원본 마법사가 완료 되 면 Visual Studio가 ObjectDataSource s `OldValuesParameterFormatString` 속성을 원래\_{0}설정 합니다. 이 설정을 기본값으로 되돌려 {0} 합니다.

GridView와 ObjectDataSource를 편집한 후에는 해당 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](working-with-computed-columns-cs/samples/sample7.aspx)]

그런 다음 브라우저를 통해이 페이지를 방문 합니다. 그림 12와 같이 각 공급 업체는 `FullContactName` 열을 포함 하는 표에 나열 됩니다. 해당 값은 `ContactName` (`ContactTitle`, `CompanyName`)로 형식이 지정 된 다른 세 열의 연결입니다.

[각 공급 업체 ![표에 나열 됩니다.](working-with-computed-columns-cs/_static/image35.png)](working-with-computed-columns-cs/_static/image34.png)

**그림 12**: 각 공급자가 표에 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](working-with-computed-columns-cs/_static/image36.png)).

특정 공급자에 대 한 편집 단추를 클릭 하면 다시 게시 되 고 해당 행이 편집 인터페이스에서 렌더링 됩니다 (그림 13 참조). 처음 세 개의 열은 기본 편집 인터페이스에서 렌더링 됩니다. 텍스트 상자 컨트롤 `Text` 속성은 데이터 필드의 값으로 설정 됩니다. 그러나 `FullContactName` 열은 텍스트로 유지 됩니다. 데이터 소스 구성 마법사가 완료 되 면 GridView에 BoundFields이 추가 되 면 `SuppliersDataTable`의 해당 `FullContactName` 열에 `ReadOnly` 속성이 `true`로 설정 되어 있기 때문에 `FullContactName` BoundField s `ReadOnly` 속성이 `true`로 설정 됩니다. 4 단계에서 설명한 대로 `FullContactName` s `ReadOnly` 속성은 TableAdapter에서 열이 계산 열 임을 검색 했기 때문에 `true`로 설정 되었습니다.

[FullContactName 열을 편집할 수 ![](working-with-computed-columns-cs/_static/image38.png)](working-with-computed-columns-cs/_static/image37.png)

**그림 13**: `FullContactName` 열을 편집할 수 없음 ([전체 크기 이미지를 보려면 클릭](working-with-computed-columns-cs/_static/image39.png))

계속 해 서 편집 가능한 하나 이상의 열 값을 업데이트 하 고 업데이트를 클릭 합니다. `FullContactName` 값이 변경 내용을 반영 하도록 자동으로 업데이트 되는 방식을 확인 합니다.

> [!NOTE]
> GridView는 현재 편집 가능한 필드에 대해 BoundFields를 사용 하 여 기본 편집 인터페이스를 생성 합니다. `CompanyName` 필드는 필수 이므로 RequiredFieldValidator를 포함 하는 Templatefield로 변환로 변환 되어야 합니다. 관심이 있는 독자를 위한 연습으로 남겨 둡니다. BoundField을 Templatefield로 변환로 변환 하 고 유효성 검사 컨트롤을 추가 하는 방법에 대 한 단계별 지침은 [인터페이스 편집 및 삽입에 유효성 검사 컨트롤 추가 자습서를](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-cs.md) 참조 하세요.

## <a name="summary"></a>요약

테이블에 대 한 스키마를 정의 하는 경우 계산 열을 포함할 수 Microsoft SQL Server. 이러한 열은 일반적으로 동일한 레코드의 다른 열에 있는 값을 참조 하는 식에서 계산 된 값을 갖는 열입니다. 계산 열의 값은 식을 기반으로 하기 때문에 읽기 전용 이며 `INSERT` 또는 `UPDATE` 문에서 값을 할당할 수 없습니다. 이는 TableAdapter의 주 쿼리에서 계산 열을 사용 하 여 해당 `INSERT`, `UPDATE`및 `DELETE` 문을 자동으로 생성 하려고 하는 경우의 문제를 소개 합니다.

이 자습서에서는 계산 열에 의해 발생 하는 문제를 회피 하는 기술에 대해 설명 했습니다. 특히 임시 SQL 문을 사용 하는 Tableadapter에서 brittleness 내재 된 저장 프로시저를 사용 했습니다. TableAdapter 마법사에서 새 저장 프로시저를 만들 때 데이터 수정 저장 프로시저가 생성 되지 않도록 하기 때문에 기본 쿼리에서 처음에 계산 열을 생략 하는 것이 중요 합니다. TableAdapter를 처음 구성한 후에는 해당 `SelectCommand` 저장 프로시저를 다시 계산 하 여 계산 열을 포함할 수 있습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Hilton Geisenow와 Teresa Murphy 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](adding-additional-datatable-columns-cs.md)
> [다음](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs.md)
