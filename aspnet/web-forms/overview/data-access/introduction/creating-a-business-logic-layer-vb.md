---
uid: web-forms/overview/data-access/introduction/creating-a-business-logic-layer-vb
title: 비즈니스 논리 레이어 만들기 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 데이터 교환을 위한 중개자 역할을 하는 BLL (비즈니스 논리 계층)으로 비즈니스 규칙을 중앙 집중화 하는 방법을 알아봅니다.
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 142e5181-29ce-4bb9-907b-2a0becf7928b
msc.legacyurl: /web-forms/overview/data-access/introduction/creating-a-business-logic-layer-vb
msc.type: authoredcontent
ms.openlocfilehash: 2ee4789ea9567b7bcd70eb63695e0b1d73076dc2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78490199"
---
# <a name="creating-a-business-logic-layer-vb"></a>비즈니스 논리 레이어 만들기(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_2_VB.exe) 또는 [PDF 다운로드](creating-a-business-logic-layer-vb/_static/datatutorial02vb1.pdf)

> 이 자습서에서는 프레젠테이션 계층과 DAL 사이에서 데이터 교환을 위한 중개자 역할을 하는 BLL (비즈니스 논리 계층)로 비즈니스 규칙을 중앙 집중화 하는 방법에 대해 알아봅니다.

## <a name="introduction"></a>소개

[첫 번째 자습서](creating-a-data-access-layer-vb.md) 에서 만든 DAL (데이터 액세스 계층)은 프레젠테이션 논리와 데이터 액세스 논리를 명확 하 게 구분 합니다. 그러나 DAL이 프레젠테이션 계층에서 데이터 액세스 세부 정보를 완전히 분리 하는 동안에는 적용 될 수 있는 비즈니스 규칙을 적용 하지 않습니다. 예를 들어, 응용 프로그램의 경우 `Discontinued` 필드가 1로 설정 된 경우 `Products` 테이블의 `CategoryID` 또는 `SupplierID` 필드를 수정할 수 없도록 하거나, seniority 규칙을 적용 하 여 직원이 해당 직원에 게 직원을 관리 하는 상황이 발생 하지 않도록 할 수 있습니다. 또 다른 일반적인 시나리오는 권한 부여입니다. 특정 역할의 사용자만 제품을 삭제 하거나 `UnitPrice` 값을 변경할 수 있습니다.

이 자습서에서는 프레젠테이션 계층과 DAL 간에 데이터 교환을 위한 중개자 역할을 하는 이러한 비즈니스 규칙을 BLL (비즈니스 논리 계층)으로 중앙 집중화 하는 방법에 대해 알아봅니다. 실제 응용 프로그램에서 BLL은 별도의 클래스 라이브러리 프로젝트로 구현 되어야 합니다. 그러나 이러한 자습서에서는 프로젝트 구조를 간소화 하기 위해 `App_Code` 폴더에 있는 일련의 클래스로 BLL을 구현 합니다. 그림 1에서는 프레젠테이션 계층, BLL 및 DAL 간의 아키텍처 관계를 보여 줍니다.

![BLL은 데이터 액세스 계층에서 프레젠테이션 계층을 분리 하 고 비즈니스 규칙을 적용 합니다.](creating-a-business-logic-layer-vb/_static/image1.png)

**그림 1**: BLL은 데이터 액세스 계층에서 프레젠테이션 계층을 분리 하 고 비즈니스 규칙을 적용 합니다.

[비즈니스 논리](http://en.wikipedia.org/wiki/Business_logic)를 구현 하는 별도의 클래스를 만드는 대신 partial 클래스를 사용 하 여 형식화 된 데이터 집합에 직접이 논리를 추가할 수 있습니다. 형식화 된 데이터 집합을 만들고 확장 하는 예제를 보려면 첫 번째 자습서를 다시 참조 하세요.

## <a name="step-1-creating-the-bll-classes"></a>1 단계: BLL 클래스 만들기

BLL은 DAL의 각 TableAdapter에 대해 하나씩 네 개의 클래스로 구성 됩니다. 이러한 각 BLL 클래스에는 DAL에서 각 TableAdapter를 검색, 삽입, 업데이트 및 삭제 하 여 적절 한 비즈니스 규칙을 적용 하는 메서드가 있습니다.

DAL 및 BLL 관련 클래스를 보다 명확 하 게 구분 하려면 `App_Code` 폴더 `DAL` 및 `BLL`에 두 개의 하위 폴더를 만들어 보겠습니다. 솔루션 탐색기에서 `App_Code` 폴더를 마우스 오른쪽 단추로 클릭 하 고 새 폴더를 선택 하면 됩니다. 이러한 두 폴더를 만든 후에는 첫 번째 자습서에서 만든 형식화 된 데이터 집합을 `DAL` 하위 폴더로 이동 합니다.

그런 다음 `BLL` 하위 폴더에 네 개의 BLL 클래스 파일을 만듭니다. 이를 수행 하려면 `BLL` 하위 폴더를 마우스 오른쪽 단추로 클릭 하 고 새 항목 추가를 선택한 다음 클래스 템플릿을 선택 합니다. `ProductsBLL`, `CategoriesBLL`, `SuppliersBLL`및 `EmployeesBLL`의 네 가지 클래스 이름을로 합니다.

![App_Code 폴더에 네 개의 새 클래스를 추가 합니다.](creating-a-business-logic-layer-vb/_static/image2.png)

**그림 2**: `App_Code` 폴더에 4 개의 새 클래스 추가

다음에는 각 클래스에 메서드를 추가 하 여 첫 번째 자습서에서 Tableadapter에 대해 정의 된 메서드를 간단 하 게 래핑합니다. 지금은 이러한 메서드는 DAL을 직접 호출 합니다. 나중에 돌아와서 필요한 비즈니스 논리를 추가 합니다.

> [!NOTE]
> Visual Studio Standard Edition 이상을 사용 하는 경우 (즉, Visual Web Developer를 사용 하 고 *있지* 않은 경우) [클래스 디자이너](https://msdn.microsoft.com/library/default.asp?url=/library/dv_vstechart/html/clssdsgnr.asp)를 사용 하 여 선택적으로 클래스를 시각적으로 디자인할 수 있습니다. Visual Studio의이 새로운 기능에 대 한 자세한 내용은 [클래스 디자이너 블로그](https://blogs.msdn.com/classdesigner/default.aspx) 를 참조 하세요.

`ProductsBLL` 클래스의 경우 총 7 개 메서드를 추가 해야 합니다.

- 모든 제품을 반환 `GetProducts()`
- `GetProductByProductID(productID)`는 지정 된 제품 ID를 가진 제품을 반환 합니다.
- `GetProductsByCategoryID(categoryID)`는 지정 된 범주의 모든 제품을 반환 합니다.
- `GetProductsBySupplier(supplierID)`는 지정 된 공급자의 모든 제품을 반환 합니다.
- `AddProduct(productName, supplierID, categoryID, quantityPerUnit, unitPrice, unitsInStock, unitsOnOrder, reorderLevel, discontinued)` 전달 된 값을 사용 하 여 데이터베이스에 새 제품을 삽입 합니다. 새로 삽입 한 레코드의 `ProductID` 값을 반환 합니다.
- `UpdateProduct(productName, supplierID, categoryID, quantityPerUnit, unitPrice, unitsInStock, unitsOnOrder, reorderLevel, discontinued, productID)`은 전달 된 값을 사용 하 여 데이터베이스의 기존 제품을 업데이트 합니다. 정확히 하나의 행이 업데이트 된 경우 `True`을 반환 하 고, 그렇지 않으면 `False`
- `DeleteProduct(productID)` 지정 된 제품을 데이터베이스에서 삭제 합니다.

ProductsBLL.vb

[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample1.vb)]

단순히 데이터 `GetProducts`, `GetProductByProductID`, `GetProductsByCategoryID`및 `GetProductBySuppliersID`를 반환 하는 메서드는 DAL로 간단히 호출할 때 매우 간단 합니다. 일부 시나리오에서는이 수준에서 구현 해야 하는 비즈니스 규칙 (예: 현재 로그온 한 사용자 또는 사용자가 속한 역할에 따라 권한 부여 규칙)이 있을 수 있습니다. 이러한 메서드는 그대로 둡니다. 이러한 메서드의 경우 BLL은 프레젠테이션 계층이 데이터 액세스 계층에서 기본 데이터에 액세스 하는 프록시로만 사용 됩니다.

`AddProduct` 및 `UpdateProduct` 메서드는 각각 다양 한 제품 필드의 값을 매개 변수로 사용 하 고 새 제품을 추가 하거나 기존 항목을 업데이트 합니다. 많은 `Product` 테이블의 열에 `NULL` 값 (`CategoryID`, `SupplierID`및 `UnitPrice`)을 사용할 수 있기 때문에 이러한 열에 매핑되는 `AddProduct` 및 `UpdateProduct`에 대 한 입력 매개 변수는 [nullable 형식을](https://msdn.microsoft.com/library/1t3y8s4s(v=vs.80).aspx)사용 합니다. Nullable 형식은 .NET 2.0의 새로운 기능으로, 대신 값 형식을 `Nothing`해야 하는지 여부를 나타내는 기술을 제공 합니다. 자세한 내용은 [Paul Vick](http://www.panopticoncentral.net/)의 블로그 항목 [NULLABLE 형식 및 VB](http://www.panopticoncentral.net/archive/2004/06/04/1180.aspx) 및 [nullable](https://msdn.microsoft.com/library/b3h38hb0%28VS.80%29.aspx) 구조체에 대 한 기술 설명서를 참조 하세요.

이 세 가지 메서드는 모두 작업에서 영향을 받는 행을 반환 하지 않을 수 있으므로 행이 삽입, 업데이트 또는 삭제 되었는지 여부를 나타내는 부울 값을 반환 합니다. 예를 들어, 페이지 개발자가 존재 하지 않는 제품에 대 한 `ProductID`를 전달 하 `DeleteProduct`를 호출 하는 경우 데이터베이스에 대해 실행 되는 `DELETE` 문은 아무런 영향을 주지 않으므로 `DeleteProduct` 메서드에서 `False`를 반환 합니다.

새 제품을 추가 하거나 기존 제품을 업데이트 하는 경우 `ProductsRow` 인스턴스를 수락 하는 것과는 반대로 새로운 또는 수정 된 제품의 필드 값이 스칼라 목록으로 사용 됩니다. 이 방법은 `ProductsRow` 클래스가 매개 변수가 없는 기본 생성자가 없는 ADO.NET `DataRow` 클래스에서 파생 되기 때문에 선택 되었습니다. 새 `ProductsRow` 인스턴스를 만들려면 먼저 `ProductsDataTable` 인스턴스를 만든 다음 `AddProduct`에서 수행 하는 `NewProductRow()` 메서드를 호출 해야 합니다. 이 단점은 ObjectDataSource를 사용 하 여 제품을 삽입 하 고 업데이트 하려고 할 때 rears. 즉, ObjectDataSource는 입력 매개 변수의 인스턴스를 만들려고 시도 합니다. BLL 메서드에 `ProductsRow` 인스턴스가 필요한 경우 ObjectDataSource는 하나를 만들려고 시도 하지만 매개 변수가 없는 기본 생성자가 없기 때문에 실패 합니다. 이 문제에 대 한 자세한 내용은 다음 두 가지 ASP.NET 포럼 게시물을 참조 하세요. [강력한 형식의 데이터 집합을 사용 하 여 ObjectDataSources 집합을 업데이트](https://forums.asp.net/1098630/ShowPost.aspx)하 고, [ObjectDataSource 및 강력한 형식의 데이터 집합에 문제가](https://forums.asp.net/1048212/ShowPost.aspx)있습니다.

다음으로 `AddProduct` 및 `UpdateProduct`에서 코드는 `ProductsRow` 인스턴스를 만들고이를 전달 된 값으로 채웁니다. DataRow의 DataColumns에 값을 할당할 때 다양 한 필드 수준 유효성 검사를 수행할 수 있습니다. 따라서 수동으로 전달 된 값을 DataRow에 다시 배치 하면 BLL 메서드에 전달 되는 데이터의 유효성을 보장할 수 있습니다. 그러나 Visual Studio에서 생성 하는 강력한 형식의 DataRow 클래스는 nullable 형식을 사용 하지 않습니다. 대신 DataRow의 특정 DataColumn이 `NULL` 데이터베이스 값과 일치 해야 함을 나타내려면 `SetColumnNameNull()` 메서드를 사용 해야 합니다.

`UpdateProduct`에서는 먼저 `GetProductByProductID(productID)`를 사용 하 여 업데이트 하기 위해 제품을 로드 합니다. 이는 데이터베이스에 불필요 하 게 이동 하는 것 처럼 보일 수 있지만, 이러한 추가 여행 방식은 낙관적 동시성을 탐색 하는 이후 자습서에서 유용한 것입니다. 낙관적 동시성은 동일한 데이터에 대해 동시에 작업 하는 두 사용자가 실수로 다른 사람의 변경 내용을 덮어쓰지 않도록 하는 기술입니다. 또한 전체 레코드를 사용 하면 DataRow의 열 하위 집합만 수정 하는 업데이트 메서드를 BLL에서 쉽게 만들 수 있습니다. `SuppliersBLL` 클래스를 탐색할 때 이러한 예를 확인할 수 있습니다.

마지막으로, `ProductsBLL` 클래스에는 [DataObject 특성이](https://msdn.microsoft.com/library/system.componentmodel.dataobjectattribute.aspx) 적용 되 고 (파일 위쪽의 클래스 문 바로 앞에 있는 `[System.ComponentModel.DataObject]` 구문) 메서드는 [DataObjectMethodAttribute 특성이](https://msdn.microsoft.com/library/system.componentmodel.dataobjectmethodattribute.aspx)있습니다. `DataObject` 특성은 클래스를 [ObjectDataSource 컨트롤](https://msdn.microsoft.com/library/9a4kyhcx.aspx)에 바인딩하는 데 적합 한 개체로 표시 하는 반면 `DataObjectMethodAttribute`는 메서드의 용도를 나타냅니다. 이후 자습서에서 볼 수 있듯이 ASP.NET 2.0의 ObjectDataSource를 사용 하면 클래스에서 데이터에 선언적으로 쉽게 액세스할 수 있습니다. ObjectDataSource의 마법사에서 바인딩할 수 있는 클래스의 목록을 필터링 하는 데 도움이 되도록 기본적으로 `DataObjects`으로 표시 된 클래스만 마법사의 드롭다운 목록에 표시 됩니다. `ProductsBLL` 클래스는 이러한 특성을 사용 하지 않고 작동 하지만이를 추가 하면 ObjectDataSource의 마법사에서 보다 쉽게 작업할 수 있습니다.

## <a name="adding-the-other-classes"></a>다른 클래스 추가

`ProductsBLL` 클래스를 완료 한 후에도 범주, 공급자 및 직원을 사용 하기 위한 클래스를 추가 해야 합니다. 위의 예제에서 설명한 개념을 사용 하 여 다음 클래스와 메서드를 만들어 보겠습니다.

- **CategoriesBLL.cs**

    - `GetCategories()`
    - `GetCategoryByCategoryID(categoryID)`
- **SuppliersBLL.cs**

    - `GetSuppliers()`
    - `GetSupplierBySupplierID(supplierID)`
    - `GetSuppliersByCountry(country)`
    - `UpdateSupplierAddress(supplierID, address, city, country)`
- **EmployeesBLL.cs**

    - `GetEmployees()`
    - `GetEmployeeByEmployeeID(employeeID)`
    - `GetEmployeesByManager(managerID)`

한 가지 주목할 만한 방법은 `SuppliersBLL` 클래스의 `UpdateSupplierAddress` 메서드입니다. 이 메서드는 공급자의 주소 정보만 업데이트 하기 위한 인터페이스를 제공 합니다. 내부적으로이 메서드는 지정 된 `supplierID`에 대 한 `SupplierDataRow` 개체에서 `GetSupplierBySupplierID`을 사용 하 여 읽고 해당 주소 관련 속성을 설정한 다음 `SupplierDataTable`의 `Update` 메서드를 호출 합니다. `UpdateSupplierAddress` 메서드는 다음과 같습니다.

[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample2.vb)]

BLL 클래스의 전체 구현에 대해서는이 문서의 다운로드를 참조 하세요.

## <a name="step-2-accessing-the-typed-datasets-through-the-bll-classes"></a>2 단계: BLL 클래스를 통해 형식화 된 데이터 집합에 액세스

첫 번째 자습서에서는 형식화 된 데이터 집합을 프로그래밍 방식으로 직접 작업 하는 예제를 살펴보았습니다. 그러나 BLL 클래스를 추가 하 여 프레젠테이션 계층이 대신 BLL에 대해 작동 해야 합니다. 첫 번째 자습서의 `AllProducts.aspx` 예제에서는 다음 코드에 표시 된 것 처럼 `ProductsTableAdapter`를 사용 하 여 제품 목록을 GridView에 바인딩합니다.

[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample3.vb)]

새 BLL 클래스를 사용 하려면 코드의 첫 번째 줄에서 `ProductsTableAdapter` 개체를 `ProductBLL` 개체로 대체 하기만 하면 됩니다.

[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample4.vb)]

BLL 클래스는 ObjectDataSource를 사용 하 여 형식화 된 데이터 집합과 마찬가지로 선언적으로 액세스할 수도 있습니다. 다음 자습서에서는 ObjectDataSource에 대해 더 자세히 설명 합니다.

[제품 목록이 GridView에 표시 ![](creating-a-business-logic-layer-vb/_static/image4.png)](creating-a-business-logic-layer-vb/_static/image3.png)

**그림 3**: GridView에 표시 되는 제품 목록 ([전체 크기 이미지를 보려면 클릭](creating-a-business-logic-layer-vb/_static/image5.png))

## <a name="step-3-adding-field-level-validation-to-the-datarow-classes"></a>3 단계: DataRow 클래스에 필드 수준 유효성 검사 추가

필드 수준 유효성 검사는 삽입 또는 업데이트할 때 비즈니스 개체의 속성 값과 관련 된 검사입니다. 제품에 대 한 일부 필드 수준 유효성 검사 규칙은 다음과 같습니다.

- `ProductName` 필드의 길이는 40 자이 하 여야 합니다.
- `QuantityPerUnit` 필드의 길이는 20 자이 하 여야 합니다.
- `ProductID`, `ProductName`및 `Discontinued` 필드가 필요 하지만 다른 모든 필드는 선택 사항입니다.
- `UnitPrice`, `UnitsInStock`, `UnitsOnOrder`및 `ReorderLevel` 필드는 0 보다 크거나 같아야 합니다.

이러한 규칙은 데이터베이스 수준에서 표시 될 수 있습니다. `ProductName` 및 `QuantityPerUnit` 필드의 문자 제한은 `Products` 테이블 (각각`nvarchar(40)` 및 `nvarchar(20)`)에 있는 해당 열의 데이터 형식에 의해 캡처됩니다. 필드가 필수이 고 선택적으로 데이터베이스 테이블 열에서 `NULL`를 허용 하는 경우로 표현 됩니다. 0 보다 크거나 같은 값만 `UnitPrice`, `UnitsInStock`, `UnitsOnOrder`또는 `ReorderLevel` 열로 만들 수 있도록 하는 네 가지 [check 제약 조건이](https://msdn.microsoft.com/library/ms188258.aspx) 있습니다.

데이터베이스에서 이러한 규칙을 적용 하는 것 외에도 데이터 집합 수준에서 적용 해야 합니다. 실제로 각 DataTable의 DataColumns 집합에 대해 필드 길이와 값 또는 선택적 값이 이미 캡처 되었는지 여부를 나타냅니다. 기존 필드 수준 유효성 검사를 자동으로 표시 하려면 데이터 집합 디자이너로 이동 하 여 Datatable 중 하나에서 필드를 선택한 다음 속성 창로 이동 합니다. 그림 4와 같이 `ProductsDataTable`의 `QuantityPerUnit` DataColumn의 최대 길이는 20 자이 고 `NULL` 값을 허용 합니다. `ProductsDataRow`의 `QuantityPerUnit` 속성을 20 자 보다 긴 문자열 값으로 설정 하려고 하면 `ArgumentException`이 throw 됩니다.

[DataColumn ![기본 필드 수준 유효성 검사를 제공 합니다.](creating-a-business-logic-layer-vb/_static/image7.png)](creating-a-business-logic-layer-vb/_static/image6.png)

**그림 4**: DataColumn은 기본 필드 수준 유효성 검사 ([전체 크기 이미지를 보려면 클릭](creating-a-business-logic-layer-vb/_static/image8.png))를 제공 합니다.

아쉽게도 속성 창를 통해 `UnitPrice` 값이 0 보다 크거나 같아야 하는 범위 검사를 지정할 수 없습니다. 이러한 형식의 필드 수준 유효성 검사를 제공 하기 위해 DataTable의 [Columnchanging](https://msdn.microsoft.com/library/system.data.datatable.columnchanging%28VS.80%29.aspx) 이벤트에 대 한 이벤트 처리기를 만들어야 합니다. [앞의 자습서](creating-a-data-access-layer-vb.md)에서 설명한 대로 형식화 된 데이터 집합에서 만든 Dataset, Datatable 및 DataRow 개체는 partial 클래스를 사용 하 여 확장할 수 있습니다. 이 기술을 사용 하 여 `ProductsDataTable` 클래스에 대 한 `ColumnChanging` 이벤트 처리기를 만들 수 있습니다. `ProductsDataTable.ColumnChanging.vb`이라는 `App_Code` 폴더에 클래스를 만들어 시작 합니다.

[![App_Code 폴더에 새 클래스를 추가 합니다.](creating-a-business-logic-layer-vb/_static/image10.png)](creating-a-business-logic-layer-vb/_static/image9.png)

**그림 5**: `App_Code` 폴더에 새 클래스 추가 ([전체 크기 이미지를 보려면 클릭](creating-a-business-logic-layer-vb/_static/image11.png))

그런 다음 `UnitPrice`, `UnitsInStock`, `UnitsOnOrder`및 `ReorderLevel` 열 값 (`NULL`되지 않는 경우)이 0 보다 크거나 같은 `ColumnChanging` 이벤트에 대 한 이벤트 처리기를 만듭니다. 이러한 열이 범위를 벗어나는 경우 `ArgumentException`를 throw 합니다.

ProductsDataTable.ColumnChanging.vb

[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample5.vb)]

## <a name="step-4-adding-custom-business-rules-to-the-blls-classes"></a>4 단계: 사용자 지정 비즈니스 규칙을 BLL의 클래스에 추가

필드 수준 유효성 검사 외에도 다음과 같은 단일 열 수준에서 표현할 수 없는 다양 한 엔터티 또는 개념을 포함 하는 높은 수준의 사용자 지정 비즈니스 규칙이 있을 수 있습니다.

- 제품이 중단 된 경우 `UnitPrice`를 업데이트할 수 없습니다.
- 직원의 거주 국가는 해당 관리자의 거주 국가와 동일 해야 합니다.
- 공급 업체가 제공 하는 유일한 제품인 제품은 중단할 수 없습니다.

BLL 클래스는 응용 프로그램의 비즈니스 규칙을 준수 하는지 확인 하는 검사를 포함 해야 합니다. 이러한 검사는 적용 되는 메서드에 직접 추가할 수 있습니다.

비즈니스 규칙에 따라 제품이 지정 된 공급 업체의 유일한 제품인 경우 단종 된 것으로 표시 되지 않을 수 있다고 가정 합니다. 즉, 제품 *x* 가 공급 업체 *Y*에서 구매한 유일한 제품인 경우 *x* 를 중단 된 것으로 표시할 수 없습니다. 그러나 공급 업체 *Y* 가 3 개 제품, *a*, *B*, *C*를 제공 하는 경우이를 모두 단종 된 것으로 표시할 수 있습니다. 홀수 비즈니스 규칙 이지만 비즈니스 규칙 및 일반적인 의미는 항상 정렬 되지 않습니다.

`UpdateProducts` 메서드에서이 비즈니스 규칙을 적용 하려면 `Discontinued` `True`으로 설정 되었는지 확인 한 다음 `GetProductsBySupplierID`를 호출 하 여이 제품의 공급자 로부터 구매한 제품 수를 확인 합니다. 이 공급자에서 하나의 제품만 구매한 경우 `ApplicationException`발생 합니다.

[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample6.vb)]

## <a name="responding-to-validation-errors-in-the-presentation-tier"></a>프레젠테이션 계층의 유효성 검사 오류에 응답

프레젠테이션 계층에서 BLL을 호출 하는 경우 발생할 수 있는 예외를 처리 하려고 할지 아니면 `HttpApplication`의 `Error` 이벤트를 발생 시킬 수 있는 최대 ASP.NET까지 버블링 되도록 할지 결정할 수 있습니다. BLL을 프로그래밍 방식으로 사용할 때 예외를 처리 하기 위해 Try ...를 사용할 수 있습니다. [ Catch](https://msdn.microsoft.com/library/fk6t46tz%28VS.80%29.aspx) 블록은 다음 예제와 같이 표시 됩니다.

[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample7.vb)]

이후 자습서에서 볼 수 있듯이 데이터 삽입, 업데이트 또는 삭제를 위해 데이터 웹 컨트롤을 사용할 때 BLL에서 버블링 되는 예외를 처리 하는 것은 `Try...Catch` 블록에서 코드를 래핑하는 대신 이벤트 처리기에서 직접 처리할 수 있습니다.

## <a name="summary"></a>요약

잘 설계 된 응용 프로그램은 각각 특정 역할을 캡슐화 하는 별개의 계층으로 제작 됩니다. 이 문서 시리즈의 첫 번째 자습서에서는 형식화 된 데이터 집합을 사용 하 여 데이터 액세스 계층을 만들었습니다. 이 자습서에서는 비즈니스 논리 계층을 응용 프로그램의 `App_Code` 폴더에서 DAL로 호출 하는 일련의 클래스로 빌드 했습니다. BLL은 응용 프로그램에 대 한 필드 수준 및 비즈니스 수준 논리를 구현 합니다. 이 자습서에서와 같이 별도의 BLL을 만드는 것 외에도, partial 클래스를 사용 하 여 Tableadapter의 메서드를 확장 하는 방법도 있습니다. 그러나이 기법을 사용 하 여 기존 메서드를 재정의할 수는 없으며,이 문서에서 수행한 방법으로 DAL 및 BLL을 완전히 분리 하지도 않습니다.

DAL 및 BLL이 완료 되 면 프레젠테이션 계층에서 시작할 준비가 된 것입니다. [다음 자습서](master-pages-and-site-navigation-vb.md) 에서는 데이터 액세스 항목에서 잠깐 우회 자습서에서 사용할 일관 된 페이지 레이아웃을 정의 합니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Liz Shulok, Dennis Patterson이, Carlos Santos 및 Hilton Gid Esenow 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](creating-a-data-access-layer-vb.md)
> [다음](master-pages-and-site-navigation-vb.md)
