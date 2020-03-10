---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/adding-additional-datatable-columns-cs
title: 추가 DataTable 열 추가 (C#) | Microsoft Docs
author: rick-anderson
description: TableAdapter 마법사를 사용 하 여 형식화 된 데이터 집합을 만드는 경우 해당 DataTable에는 주 데이터베이스 쿼리에서 반환 된 열이 포함 됩니다. 하지만
ms.author: riande
ms.date: 07/18/2007
ms.assetid: 615f3361-f21f-4338-8bc1-fce8ae071de9
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/adding-additional-datatable-columns-cs
msc.type: authoredcontent
ms.openlocfilehash: a96f254aa54e7077456ac1a9bd6c5e2a17619d96
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78444497"
---
# <a name="adding-additional-datatable-columns-c"></a>추가 DataTable 열 추가(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_70_CS.zip) 또는 [PDF 다운로드](adding-additional-datatable-columns-cs/_static/datatutorial70cs1.pdf)

> TableAdapter 마법사를 사용 하 여 형식화 된 데이터 집합을 만드는 경우 해당 DataTable에는 주 데이터베이스 쿼리에서 반환 된 열이 포함 됩니다. 그러나 DataTable에 추가 열을 포함 해야 하는 경우도 있습니다. 이 자습서에서는 추가 DataTable 열이 필요할 때 저장 프로시저를 권장 하는 이유를 알아봅니다.

## <a name="introduction"></a>소개

형식화 된 데이터 집합에 TableAdapter를 추가 하는 경우 해당 DataTable의 스키마는 TableAdapter의 주 쿼리에 의해 결정 됩니다. 예를 들어 주 쿼리가 *a*, *b*및 *c*데이터 필드를 반환 하는 경우 DataTable에 *는 A*, *b*, *c*라는 3 개의 해당 열이 포함 됩니다. TableAdapter는 주 쿼리 외에도 일부 매개 변수를 기반으로 데이터의 하위 집합을 반환 하는 추가 쿼리를 포함할 수 있습니다. 예를 들어 모든 제품에 대 한 정보를 반환 하는 `ProductsTableAdapter` s 주 쿼리 외에도 제공 된 매개 변수에 따라 특정 제품 정보를 반환 하는 `GetProductsByCategoryID(categoryID)` 및 `GetProductByProductID(productID)`와 같은 메서드가 포함 됩니다.

DataTable의 스키마가 있는 주 쿼리를 반영 하는 모델은 TableAdapter의 모든 메서드가 주 쿼리에 지정 된 것과 같거나 작은 데이터 필드를 반환 하는 경우 제대로 작동 합니다. TableAdapter 메서드가 추가 데이터 필드를 반환 해야 하는 경우 DataTable의 스키마를 적절 하 게 확장 해야 합니다. [세부 정보를 포함 하는 마스터 레코드의 글머리 기호 목록을 사용 하는 마스터/세부 정보 DataList](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md) 자습서에서는 기본 `NumberOfProducts`쿼리에 정의 된 `CategoryID`, `CategoryName`및 `Description` 데이터 필드를 반환 하 고 각 범주와 관련 된 제품 수를 보고 하는 추가 데이터 필드를 반환 하는 메서드를 `CategoriesTableAdapter`에 추가 했습니다. 이 새 메서드에서 `NumberOfProducts` 데이터 필드 값을 캡처하기 위해 `CategoriesDataTable`에 새 열을 수동으로 추가 했습니다.

[파일 업로드](../working-with-binary-files/uploading-files-cs.md) 자습서에 설명 된 것 처럼 임시 SQL 문을 사용 하 고 데이터 필드가 주 쿼리와 정확 하 게 일치 하지 않는 메서드를 사용 하는 tableadapter를 사용 하 여 많은 주의가 필요 합니다. TableAdapter 구성 마법사가 다시 실행 되는 경우 해당 데이터 필드 목록이 주 쿼리와 일치 하도록 TableAdapter의 모든 메서드를 업데이트 합니다. 따라서 사용자 지정 된 열 목록을 포함 하는 모든 메서드는 주 쿼리 열 목록으로 되돌아가고 필요한 데이터를 반환 하지 않습니다. 저장 프로시저를 사용 하는 경우에는이 문제가 발생 하지 않습니다.

이 자습서에서는 추가 열을 포함 하도록 DataTable의 스키마를 확장 하는 방법을 살펴보겠습니다. 이 자습서에서는 임시 SQL 문을 사용할 때 TableAdapter의 brittleness 때문에 저장 프로시저를 사용 합니다. 저장 프로시저를 사용 하도록 TableAdapter를 구성 하는 방법에 대 한 자세한 내용은 [형식화 된 데이터 집합의 tableadapter에 대 한 새 저장 프로시저 만들기](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) 및 [형식화 된 데이터 집합의 tableadapter 자습서에 대 한 기존 저장 프로시저 사용](https://data-access/tutorials/using-existing-stored-procedures-for-the-typed-dataset-amp-rsquo-s-tableadapters-cs) 을 참조 하세요.

## <a name="step-1-adding-apricequartilecolumn-to-theproductsdatatable"></a>1 단계:`ProductsDataTable`에`PriceQuartile`열 추가

형식화 된 *데이터 집합에 대 한 새 저장 프로시저 만들기 tableadapter* 자습서에서 `NorthwindWithSprocs`이라는 형식화 된 데이터 집합을 만들었습니다. 이 데이터 집합에는 현재 두 개의 `ProductsDataTable` Datatable와 `EmployeesDataTable`포함 되어 있습니다. `ProductsTableAdapter`에는 다음과 같은 세 가지 메서드가 있습니다.

- `GetProducts`-`Products` 테이블의 모든 레코드를 반환 하는 주 쿼리입니다.
- `GetProductsByCategoryID(categoryID)`-지정 된 *categoryID*를 포함 하는 모든 제품을 반환 합니다.
- `GetProductByProductID(productID)`-지정 된 *productID*를 사용 하 여 특정 제품을 반환 합니다.

주 쿼리와 두 개의 추가 메서드는 모두 동일한 데이터 필드 집합, 즉 `Products` 테이블의 모든 열을 반환 합니다. 상호 관련 된 하위 쿼리 또는 `Categories` 또는 `Suppliers` 테이블에서 관련 된 데이터를 가져오는 `JOIN` 없습니다. 따라서 `ProductsDataTable` `Products` 테이블의 각 필드에 해당 하는 열이 있습니다.

이 자습서에서는 모든 제품을 반환 하는 `GetProductsWithPriceQuartile` 라는 `ProductsTableAdapter`에 메서드를 추가 하겠습니다. 표준 제품 데이터 필드 외에도 `GetProductsWithPriceQuartile`에는 제품 가격의 사분이를 나타내는 `PriceQuartile` 데이터 필드도 포함 됩니다. 예를 들어 가격이 가장 비싼 25%에 해당 하는 제품의 `PriceQuartile` 값은 1이 고 가격은 하위 25%에 속하는 제품은 값이 4입니다. 그러나이 정보를 반환 하는 저장 프로시저를 만드는 방법에 대해 걱정할 때 까지는 먼저 `GetProductsWithPriceQuartile` 메서드를 사용할 때 `PriceQuartile` 결과를 저장할 열을 포함 하도록 `ProductsDataTable`를 업데이트 해야 합니다.

`NorthwindWithSprocs` 데이터 집합을 열고 `ProductsDataTable`을 마우스 오른쪽 단추로 클릭 합니다. 상황에 맞는 메뉴에서 추가를 선택한 다음 열을 선택 합니다.

[ProductsDataTable에 새 열을 추가 ![](adding-additional-datatable-columns-cs/_static/image2.png)](adding-additional-datatable-columns-cs/_static/image1.png)

**그림 1**: `ProductsDataTable`에 새 열 추가 ([전체 크기 이미지를 보려면 클릭](adding-additional-datatable-columns-cs/_static/image3.png))

그러면 `System.String`형식의 Column1 이라는 DataTable에 새 열이 추가 됩니다. 이 열 이름을 PriceQuartile로 업데이트 하 고 해당 형식을 `System.Int32`로 업데이트 하 여 1에서 4 사이의 숫자를 저장 하는 데 사용 되기 때문입니다. `ProductsDataTable`에서 새로 추가 된 열을 선택 하 고 속성 창에서 `Name` 속성을 PriceQuartile로 설정 하 고 `DataType` 속성을 `System.Int32`로 설정 합니다.

[새 열의 이름 및 데이터 형식 속성을 설정 ![](adding-additional-datatable-columns-cs/_static/image5.png)](adding-additional-datatable-columns-cs/_static/image4.png)

**그림 2**: 새 열 `Name` 설정 및 `DataType` 속성 ([전체 크기 이미지를 보려면 클릭](adding-additional-datatable-columns-cs/_static/image6.png))

그림 2에 나와 있는 것 처럼 열의 값이 고유 해야 하는지 여부, 열이 자동 증분 열 이면 데이터베이스 `NULL` 값이 허용 되는지 여부 등의 추가 속성을 설정할 수 있습니다. 이러한 값을 기본값으로 설정 해 둡니다.

## <a name="step-2-creating-thegetproductswithpricequartilemethod"></a>2 단계:`GetProductsWithPriceQuartile`메서드 만들기

이제 `PriceQuartile` 열을 포함 하도록 `ProductsDataTable` 업데이트 되었으므로 `GetProductsWithPriceQuartile` 메서드를 만들 준비가 되었습니다. TableAdapter를 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 쿼리 추가를 선택 하 여 시작 합니다. 그러면 TableAdapter 쿼리 구성 마법사가 표시 되며,이 마법사에서 임시 SQL 문이나 기존 저장 프로시저를 사용할지 여부를 묻는 메시지를 표시 합니다. 아직 가격 사분 데이터를 반환 하는 저장 프로시저가 없으므로 s 1에서이 저장 프로시저를 만들도록 허용할 수 있습니다. 새 저장 프로시저 만들기 옵션을 선택 하 고 다음을 클릭 합니다.

[TableAdapter 마법사에서 저장 프로시저를 만들도록 지시 ![](adding-additional-datatable-columns-cs/_static/image8.png)](adding-additional-datatable-columns-cs/_static/image7.png)

**그림 3**: 저장 프로시저를 만들도록 TableAdapter 마법사에 지시 ([전체 크기 이미지를 보려면 클릭](adding-additional-datatable-columns-cs/_static/image9.png))

그림 4에 표시 된 후속 화면에서 마법사는 추가할 쿼리 유형을 묻는 메시지를 표시 합니다. `GetProductsWithPriceQuartile` 메서드는 `Products` 테이블에서 모든 열과 레코드를 반환 하므로 행 반환 옵션을 선택 하 고 다음을 클릭 합니다.

[![쿼리는 여러 행을 반환 하는 SELECT 문이 됩니다.](adding-additional-datatable-columns-cs/_static/image11.png)](adding-additional-datatable-columns-cs/_static/image10.png)

**그림 4**: 쿼리는 여러 행을 반환 하는 `SELECT` 문이 됩니다 ([전체 크기 이미지를 보려면 클릭](adding-additional-datatable-columns-cs/_static/image12.png)).

그런 다음 `SELECT` 쿼리를 묻는 메시지가 표시 됩니다. 마법사에 다음 쿼리를 입력 합니다.

[!code-sql[Main](adding-additional-datatable-columns-cs/samples/sample1.sql)]

위의 쿼리는 SQL Server 2005 s new [`NTILE` 함수](https://msdn.microsoft.com/library/ms175126.aspx) 를 사용 하 여 결과를 4 개의 그룹으로 나눕니다. 여기서 그룹은 내림차순으로 정렬 된 `UnitPrice` 값에 따라 결정 됩니다.

아쉽게도 쿼리 작성기는 `OVER` 키워드를 구문 분석 하는 방법을 알지 못합니다. 위의 쿼리를 구문 분석할 때 오류가 표시 됩니다. 따라서 쿼리 작성기을 사용 하지 않고 마법사의 텍스트 상자에 위의 쿼리를 직접 입력 합니다.

> [!NOTE]
> NTILE 및 SQL Server 2005 s 기타 순위 지정 함수에 대 한 자세한 내용은 [SQL Server 2005 온라인 설명서](https://msdn.microsoft.com/library/ms189798.aspx)의 [Microsoft SQL Server 2005을 사용 하 여 순위 지정 결과 반환](http://www.4guysfromrolla.com/webtech/010406-1.shtml) 및 [순위 함수 섹션](https://msdn.microsoft.com/library/ms189798.aspx) 을 참조 하세요.

`SELECT` 쿼리를 입력 하 고 다음을 클릭 하면 마법사가 만들 저장 프로시저의 이름을 입력 하 라는 메시지를 표시 합니다. 새 저장 프로시저의 이름을 `Products_SelectWithPriceQuartile` 하 고 다음을 클릭 합니다.

[저장 프로시저의 이름을 ![Products_SelectWithPriceQuartile](adding-additional-datatable-columns-cs/_static/image14.png)](adding-additional-datatable-columns-cs/_static/image13.png)

**그림 5**: 저장 프로시저의 이름 `Products_SelectWithPriceQuartile` ([전체 크기 이미지를 보려면 클릭](adding-additional-datatable-columns-cs/_static/image15.png))

마지막으로 TableAdapter 메서드의 이름을 입력 하 라는 메시지가 표시 됩니다. DataTable 채우기 및 DataTable 반환 확인란을 모두 선택 된 상태로 두고 `FillWithPriceQuartile` 메서드의 이름을 지정 하 고 `GetProductsWithPriceQuartile`합니다.

[TableAdapter의 메서드 이름을 ![하 고 마침을 클릭 합니다.](adding-additional-datatable-columns-cs/_static/image17.png)](adding-additional-datatable-columns-cs/_static/image16.png)

**그림 6**: TableAdapter의 메서드 이름 및 마침 클릭 ([전체 크기 이미지를 보려면 클릭](adding-additional-datatable-columns-cs/_static/image18.png))

`SELECT` 쿼리를 지정 하 고 저장 프로시저와 TableAdapter 메서드를 지정 하 고 마침을 클릭 하 여 마법사를 완료 합니다. 이 시점에서 `OVER` SQL 구문이 나 문이 지원 되지 않는다는 경고가 표시 될 수 있습니다. 이러한 경고는 무시 해도 됩니다.

마법사를 완료 한 후에는 TableAdapter에 `FillWithPriceQuartile` 및 `GetProductsWithPriceQuartile` 메서드가 포함 되어야 하며 데이터베이스에 `Products_SelectWithPriceQuartile`이라는 저장 프로시저가 포함 되어야 합니다. TableAdapter가이 새 메서드를 실제로 포함 하 고 저장 프로시저가 데이터베이스에 올바르게 추가 되었는지 확인 합니다. 데이터베이스를 확인할 때 저장 프로시저가 표시 되지 않는 경우 저장 프로시저 폴더를 마우스 오른쪽 단추로 클릭 하 고 새로 고침을 선택 합니다.

![새 메서드가 TableAdapter에 추가 되었는지 확인 합니다.](adding-additional-datatable-columns-cs/_static/image19.png)

**그림 7**: 새 메서드가 TableAdapter에 추가 되었는지 확인

[![데이터베이스에 Products_SelectWithPriceQuartile 저장 프로시저가 포함 되어 있는지 확인 합니다.](adding-additional-datatable-columns-cs/_static/image21.png)](adding-additional-datatable-columns-cs/_static/image20.png)

**그림 8**: 데이터베이스에 `Products_SelectWithPriceQuartile` 저장 프로시저 포함 ([전체 크기 이미지를 보려면 클릭](adding-additional-datatable-columns-cs/_static/image22.png))

> [!NOTE]
> 임시 SQL 문 대신 저장 프로시저를 사용 하는 경우의 이점 중 하나는 TableAdapter 구성 마법사를 다시 실행 하면 저장 프로시저 열 목록이 수정 되지 않기 때문입니다. TableAdapter를 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 구성 옵션을 선택 하 여 마법사를 시작 하 고 마침을 클릭 하 여 마법사를 완료 하 여이를 확인 합니다. 그런 다음 데이터베이스로 이동 하 여 `Products_SelectWithPriceQuartile` 저장 프로시저를 확인 합니다. 열 목록은 수정 되지 않았습니다. 임시 SQL 문을 사용 하는 경우 TableAdapter 구성 마법사를 다시 실행 하면이 쿼리 열 목록이 주 쿼리 열 목록과 일치 하도록 되돌려 `GetProductsWithPriceQuartile` 메서드에서 사용 하는 쿼리에서 NTILE 문을 제거 합니다.

데이터 액세스 계층 s `GetProductsWithPriceQuartile` 메서드가 호출 되 면 TableAdapter는 `Products_SelectWithPriceQuartile` 저장 프로시저를 실행 하 고 반환 된 각 레코드의 `ProductsDataTable`에 행을 추가 합니다. 저장 프로시저에서 반환 되는 데이터 필드는 `ProductsDataTable` s 열에 매핑됩니다. 저장 프로시저에서 반환 된 `PriceQuartile` 데이터 필드가 있으므로 해당 값은 `ProductsDataTable` s `PriceQuartile` 열에 할당 됩니다.

쿼리가 `PriceQuartile` 데이터 필드를 반환 하지 않는 TableAdapter 메서드의 경우 `PriceQuartile` 열 값은 `DefaultValue` 속성으로 지정 된 값입니다. 그림 2에서 볼 수 있듯이이 값은 기본값 `DBNull`로 설정 됩니다. 다른 기본값을 선호 하는 경우에는 `DefaultValue` 속성을 적절 하 게 설정 하기만 하면 됩니다. `DataType` 열에 지정 된 `DefaultValue` 값이 유효한 지 확인 합니다. 즉, `PriceQuartile` 열에 대해 `System.Int32` 합니다.

이 시점에서 DataTable에 열을 추가 하는 데 필요한 단계를 수행 했습니다. 이 추가 열이 예상 대로 작동 하는지 확인 하려면를 사용 하 여 각 제품의 이름, 가격 및 가격 사분을 표시 하는 ASP.NET 페이지를 만듭니다. 그러나이 작업을 수행 하기 전에 먼저 비즈니스 논리 계층을 업데이트 하 여 DAL s `GetProductsWithPriceQuartile` 메서드를 호출 하는 메서드를 포함 해야 합니다. 3 단계에서 다음 BLL을 업데이트 한 다음 4 단계에서 ASP.NET 페이지를 만듭니다.

## <a name="step-3-augmenting-the-business-logic-layer"></a>3 단계: 비즈니스 논리 계층 확대

프레젠테이션 계층에서 새 `GetProductsWithPriceQuartile` 메서드를 사용 하기 전에 먼저 해당 메서드를 BLL에 추가 해야 합니다. `ProductsBLLWithSprocs` 클래스 파일을 열고 다음 코드를 추가 합니다.

[!code-csharp[Main](adding-additional-datatable-columns-cs/samples/sample2.cs)]

`ProductsBLLWithSprocs`의 다른 데이터 검색 메서드와 마찬가지로 `GetProductsWithPriceQuartile` 메서드는 DAL의 해당 `GetProductsWithPriceQuartile` 메서드를 호출 하 고 해당 결과를 반환 합니다.

## <a name="step-4-displaying-the-price-quartile-information-in-an-aspnet-web-page"></a>4 단계: ASP.NET 웹 페이지에서 가격 사분 기준 정보 표시

BLL 추가가 완료 되 면 각 제품의 가격 사분을 보여 주는 ASP.NET 페이지를 만들 준비가 되었습니다. `AdvancedDAL` 폴더에서 `AddingColumns.aspx` 페이지를 열고 GridView를 도구 상자에서 디자이너로 끌어 `ID` 속성을 `Products`로 설정 합니다. GridView s 스마트 태그에서 `ProductsDataSource`라는 새 ObjectDataSource에 바인딩합니다. `ProductsBLLWithSprocs` 클래스 s `GetProductsWithPriceQuartile` 메서드를 사용 하도록 ObjectDataSource를 구성 합니다. 이는 읽기 전용 그리드 이므로 업데이트, 삽입 및 삭제 탭의 드롭다운 목록을 (없음)으로 설정 합니다.

[ProductsBLLWithSprocs 클래스를 사용 하도록 ObjectDataSource 구성 ![](adding-additional-datatable-columns-cs/_static/image24.png)](adding-additional-datatable-columns-cs/_static/image23.png)

**그림 9**: `ProductsBLLWithSprocs` 클래스를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](adding-additional-datatable-columns-cs/_static/image25.png))

[GetProductsWithPriceQuartile 메서드에서 제품 정보를 검색 ![](adding-additional-datatable-columns-cs/_static/image27.png)](adding-additional-datatable-columns-cs/_static/image26.png)

**그림 10**: `GetProductsWithPriceQuartile` 메서드에서 제품 정보 검색 ([전체 크기 이미지를 보려면 클릭](adding-additional-datatable-columns-cs/_static/image28.png))

데이터 소스 구성 마법사를 완료 한 후 Visual Studio에서 메서드가 반환 하는 각 데이터 필드에 대해 BoundField 또는 CheckBoxField를 GridView에 자동으로 추가 합니다. 이러한 데이터 필드 중 하나는 `PriceQuartile`이며 1 단계에서 `ProductsDataTable` 추가 된 열입니다.

GridView 필드를 편집 하 여 `ProductName`, `UnitPrice`및 `PriceQuartile` BoundFields를 제외한 모든 필드를 제거 합니다. `UnitPrice` BoundField를 구성 하 여 값의 서식을 통화로 지정 하 고 `UnitPrice` 및 `PriceQuartile` BoundFields 오른쪽 맞춤 및 가운데 맞춤을 지정 합니다. 마지막으로 나머지 BoundFields `HeaderText` 속성을 Product, Price 및 Price 사분 각각로 업데이트 합니다. 또한 GridView s 스마트 태그에서 정렬 사용 확인란을 선택 합니다.

이러한 수정 후 GridView와 ObjectDataSource의 선언 태그는 다음과 같습니다.

[!code-aspx[Main](adding-additional-datatable-columns-cs/samples/sample3.aspx)]

그림 11에서는 브라우저를 통해 방문할 때이 페이지를 보여 줍니다. 처음에는 제품이 각 제품에 적절 한 `PriceQuartile` 값을 할당 하 여 가격을 기준으로 내림차순으로 정렬 되어 있습니다. 물론 가격과 관련 하 여 제품 순위를 반영 하는 가격 사분 열 값을 사용 하 여 다른 조건을 기준으로이 데이터를 정렬할 수 있습니다 (그림 12 참조).

[제품 가격에 따라 주문 하는 ![](adding-additional-datatable-columns-cs/_static/image30.png)](adding-additional-datatable-columns-cs/_static/image29.png)

**그림 11**: 제품이 가격을 기준으로 정렬 됨 ([전체 크기 이미지를 보려면 클릭](adding-additional-datatable-columns-cs/_static/image31.png))

[제품 이름을 기준으로 정렬 된 ![](adding-additional-datatable-columns-cs/_static/image33.png)](adding-additional-datatable-columns-cs/_static/image32.png)

**그림 12**: 제품 이름을 기준으로 정렬 ([전체 크기 이미지를 보려면 클릭](adding-additional-datatable-columns-cs/_static/image34.png))

> [!NOTE]
> 몇 줄의 코드를 사용 하 여 `PriceQuartile` 값을 기준으로 제품 행을 색으로 지정 하도록 GridView를 확장할 수 있습니다. Microsoft는 첫 번째 사분 위 수, 녹색, 연한 노랑 등의 제품을 색으로 색으로 할 수 있습니다. 잠시 후에이 기능을 추가 하는 것이 좋습니다. GridView 서식 지정에 리프레셔가 필요한 경우에는 [데이터에 따라 사용자 지정 서식 지정](../custom-formatting/custom-formatting-based-upon-data-cs.md) 자습서를 참조 하세요.

## <a name="an-alternative-approach---creating-another-tableadapter"></a>대체 방법-다른 TableAdapter 만들기

이 자습서에서 살펴본 것 처럼 주 쿼리에서 제공 하는 것 외의 다른 데이터 필드를 반환 하는 TableAdapter에 메서드를 추가 하는 경우 DataTable에 해당 열을 추가할 수 있습니다. 그러나 이러한 방법은 다른 데이터 필드를 반환 하는 TableAdapter의 메서드 수가 적고 해당 대체 데이터 필드가 주 쿼리와 너무 많이 다른 경우에만 제대로 작동 합니다.

DataTable에 열을 추가 하는 대신 다른 데이터 필드를 반환 하는 첫 번째 TableAdapter의 메서드를 포함 하는 데이터 집합에 다른 TableAdapter를 추가할 수 있습니다. 이 자습서에서는 `ProductsDataTable`에 `PriceQuartile` 열을 추가 하는 대신 (`GetProductsWithPriceQuartile` 메서드에서 사용 되는 경우) `Products_SelectWithPriceQuartile` 저장 프로시저를 주 쿼리로 사용한 `ProductsWithPriceQuartileTableAdapter` 이라는 데이터 집합에 TableAdapter를 추가 했을 수 있습니다. ASP.NET를 사용 하 여 제품 정보를 얻는 데 필요한 페이지는 `ProductsTableAdapter`을 계속 사용할 수는 없지만 `ProductsWithPriceQuartileTableAdapter`를 사용 합니다.

새 TableAdapter를 추가 하면 Datatable는 untarnished로 유지 되 고 해당 열은 TableAdapter의 메서드에서 반환 된 데이터 필드를 정확 하 게 미러링합니다. 그러나 Tableadapter를 추가 하면 반복적인 작업과 기능을 도입할 수 있습니다. 예를 들어 `PriceQuartile` 열을 표시 하는 이러한 페이지에서 삽입, 업데이트 및 삭제 지원을 제공 해야 하는 경우 `ProductsWithPriceQuartileTableAdapter` `InsertCommand`, `UpdateCommand`및 `DeleteCommand` 속성이 제대로 구성 되어 있어야 합니다. 이러한 속성은 `ProductsTableAdapter`를 미러링 하지만이 구성에서는 추가 단계를 소개 합니다. 또한 `ProductsTableAdapter` 및 `ProductsWithPriceQuartileTableAdapter` 클래스를 통해 데이터베이스에 제품을 업데이트, 삭제 또는 추가 하는 두 가지 방법이 있습니다.

이 자습서에 대 한 다운로드에는이 대체 방법을 보여 주는 `NorthwindWithSprocs` 데이터 집합의 `ProductsWithPriceQuartileTableAdapter` 클래스가 포함 되어 있습니다.

## <a name="summary"></a>요약

대부분의 시나리오에서 TableAdapter의 모든 메서드는 동일한 데이터 필드 집합을 반환 하지만 특정 메서드나 두 가지에서 추가 필드를 반환 해야 하는 경우가 있습니다. 예를 들어 [세부 정보를 포함 하는 마스터 레코드의 글머리 기호 목록을 사용 하는 마스터/세부 정보 DataList](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md) 자습서에서는 기본 쿼리 데이터 필드 외에 각 범주와 관련 된 제품 수를 보고 하는 `NumberOfProducts` 필드를 반환 하는 메서드를 `CategoriesTableAdapter`에 추가 했습니다. 이 자습서에서는 주 쿼리 데이터 필드 외에 `PriceQuartile` 필드를 반환 하는 `ProductsTableAdapter`에서 메서드를 추가 하는 방법을 살펴보았습니다. TableAdapter의 메서드에서 반환 된 추가 데이터 필드를 캡처하려면 해당 열을 DataTable에 추가 해야 합니다.

DataTable에 열을 수동으로 추가 하려면 TableAdapter에서 저장 프로시저를 사용 하는 것이 좋습니다. Tableadapter에서 임시 SQL 문을 사용 하는 경우 TableAdapter 구성 마법사가 실행 될 때마다 모든 메서드 데이터 필드 목록이 주 쿼리에서 반환한 데이터 필드로 되돌려집니다. 이 문제는 저장 프로시저로 확장 되지 않으므로이 자습서에서 사용 하는 것이 좋습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Randy Schmidt, Jacky Goor, Bernadette Leigh 및 Hilton Gid Esenow 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](updating-the-tableadapter-to-use-joins-cs.md)
> [다음](working-with-computed-columns-cs.md)
