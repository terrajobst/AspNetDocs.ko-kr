---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb
title: 데이터 수정 인터페이스 사용자 지정 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 표준 텍스트 상자 및 CheckBox 컨트롤을 alternati로 대체 하 여 편집 가능한 GridView의 인터페이스를 사용자 지정 하는 방법을 살펴보겠습니다.
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 4830d984-bd2c-4a08-bfe5-2385599f1f7d
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: 85ec7bdde6b2bffbbda066b0441bbd36b7072197
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74584923"
---
# <a name="customizing-the-data-modification-interface-vb"></a>데이터 수정 인터페이스 사용자 지정(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_20_VB.exe) 또는 [PDF 다운로드](customizing-the-data-modification-interface-vb/_static/datatutorial20vb1.pdf)

> 이 자습서에서는 표준 텍스트 상자 및 CheckBox 컨트롤을 대체 입력 웹 컨트롤로 바꿔서 편집 가능한 GridView의 인터페이스를 사용자 지정 하는 방법에 대해 살펴보겠습니다.

## <a name="introduction"></a>소개

GridView 및 DetailsView 컨트롤에서 사용 하는 BoundFields 및 CheckBoxFields는 읽기 전용, 편집 가능 및 삽입 가능 인터페이스를 렌더링 하는 기능 때문에 데이터를 수정 하는 프로세스를 간소화 합니다. 이러한 인터페이스는 추가로 선언 태그나 코드를 추가할 필요 없이 렌더링할 수 있습니다. 그러나 BoundField 및 CheckBoxField의 인터페이스에는 실제 시나리오에서 자주 필요한 사용자 지정 가능성 부족 합니다. GridView 또는 DetailsView에서 편집 또는 삽입 가능한 인터페이스를 사용자 지정 하려면 Templatefield로 변환를 대신 사용 해야 합니다.

[이전 자습서](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md) 에서는 유효성 검사 웹 컨트롤을 추가 하 여 데이터 수정 인터페이스를 사용자 지정 하는 방법을 살펴보았습니다. 이 자습서에서는 BoundField 및 CheckBoxField의 표준 TextBox 및 CheckBox 컨트롤을 대체 입력 웹 컨트롤로 대체 하 여 실제 데이터 컬렉션 웹 컨트롤을 사용자 지정 하는 방법을 살펴보겠습니다. 특히 제품의 이름, 범주, 공급 업체 및 단종 된 상태를 업데이트 하는 데 사용할 수 있는 편집 가능한 GridView를 빌드합니다. 특정 행을 편집할 때 범주 및 공급자 필드는 선택할 수 있는 범주 및 공급자 집합이 포함 된 Dropdownlist로 렌더링 됩니다. 또한 CheckBoxField의 기본 확인란을 두 가지 옵션인 "Active" 및 "단종"을 제공 하는 RadioButtonList 컨트롤로 바꿉니다.

[![GridView의 편집 인터페이스에 Dropdownlist 및 Radiobutton이 포함 되어 있습니다.](customizing-the-data-modification-interface-vb/_static/image2.png)](customizing-the-data-modification-interface-vb/_static/image1.png)

**그림 1**: GridView의 편집 인터페이스에 Dropdownlist 및 radiobutton ([전체 크기 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image3.png))이 포함 되어 있습니다.

## <a name="step-1-creating-the-appropriateupdateproductoverload"></a>1 단계: 적절 한`UpdateProduct`오버 로드 만들기

이 자습서에서는 제품 이름, 범주, 공급 업체 및 단종 된 상태를 편집할 수 있도록 하는 편집 가능한 GridView를 작성 합니다. 따라서 5 개의 입력 매개 변수를 허용 하는 `UpdateProduct` 오버 로드 (4 개의 제품 값과 `ProductID`를 더한 값이 필요 합니다. 이전 오버 로드에서와 같이 다음과 같이 합니다.

1. 데이터베이스에서 지정 된 `ProductID`에 대 한 제품 정보를 검색 합니다.
2. `ProductName`, `CategoryID`, `SupplierID`및 `Discontinued` 필드를 업데이트 합니다.
3. TableAdapter의 `Update()` 메서드를 통해 DAL에 업데이트 요청을 보냅니다.

간단히 하기 위해이 특정 오버 로드의 경우 중단 됨으로 표시 되는 제품이 해당 공급 업체에서 제공 하는 유일한 제품이 아님을 확인 하는 비즈니스 규칙 검사를 생략 했습니다. 원하는 경우에는 논리를 별도의 메서드에 추가 하는 것이 좋습니다.

다음 코드에서는 `ProductsBLL` 클래스의 새 `UpdateProduct` 오버 로드를 보여 줍니다.

[!code-vb[Main](customizing-the-data-modification-interface-vb/samples/sample1.vb)]

## <a name="step-2-crafting-the-editable-gridview"></a>2 단계: 편집 가능한 GridView를 만들고 있습니다.

`UpdateProduct` 오버 로드를 추가 하면 편집 가능한 GridView를 만들 준비가 되었습니다. `EditInsertDelete` 폴더에서 `CustomizedUI.aspx` 페이지를 열고 디자이너에 GridView 컨트롤을 추가 합니다. 다음으로 GridView의 스마트 태그에서 새 ObjectDataSource를 만듭니다. `ProductBLL` 클래스의 `GetProducts()` 메서드를 통해 제품 정보를 검색 하 고 방금 만든 `UpdateProduct` 오버 로드를 사용 하 여 제품 데이터를 업데이트 하도록 ObjectDataSource를 구성 합니다. 삽입 및 삭제 탭의 드롭다운 목록에서 (없음)을 선택 합니다.

[위에서 만든 UpdateProduct 오버 로드를 사용 하도록 ObjectDataSource를 구성 ![](customizing-the-data-modification-interface-vb/_static/image5.png)](customizing-the-data-modification-interface-vb/_static/image4.png)

**그림 2**: 막 만든 `UpdateProduct` 오버 로드를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image6.png))

데이터 수정 자습서에서 살펴본 것 처럼 Visual Studio에서 만든 ObjectDataSource의 선언 구문은 `original_{0}`에 `OldValuesParameterFormatString` 속성을 할당 합니다. 물론 원래 `ProductID` 값이 전달 될 것으로 간주 되기 때문에 비즈니스 논리 계층에서는 작동 하지 않습니다. 따라서 이전 자습서에서 수행한 것 처럼 잠시 후에 선언적 구문에서이 속성 할당을 제거 하거나 대신이 속성의 값을 `{0}`로 설정 합니다.

이 변경 후 ObjectDataSource의 선언 태그는 다음과 같습니다.

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample2.aspx)]

`OldValuesParameterFormatString` 속성이 제거 되었으며 `UpdateProduct` 오버 로드에 필요한 각 입력 매개 변수에 대 한 `UpdateParameters` 컬렉션에 `Parameter` 있는지 확인 합니다.

ObjectDataSource는 제품 값의 하위 집합만 업데이트 하도록 구성 되지만 현재 GridView에는 *모든* product 필드가 표시 됩니다. 잠시 후 다음을 수행 하도록 GridView를 편집 합니다.

- `ProductName`, `SupplierName`, `CategoryName` BoundFields 및 `Discontinued` CheckBoxField만 포함 됩니다.
- `CategoryName` 및 `SupplierName` 필드가 `Discontinued` CheckBoxField의 왼쪽에 표시 됩니다.
- `CategoryName` 및 `SupplierName` BoundFields ' `HeaderText` 속성은 각각 "Category" 및 "공급자"로 설정 됩니다.
- 편집 지원이 사용 하도록 설정 되어 있습니다. GridView의 스마트 태그에서 편집 사용 확인란을 선택 합니다.

이러한 변경 후에 디자이너는 아래와 같은 GridView의 선언 구문을 사용 하 여 그림 3과 유사 하 게 표시 됩니다.

[![GridView에서 불필요 한 필드를 제거 합니다.](customizing-the-data-modification-interface-vb/_static/image8.png)](customizing-the-data-modification-interface-vb/_static/image7.png)

**그림 3**: GridView에서 불필요 한 필드 제거 ([전체 크기 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image9.png))

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample3.aspx)]

이 시점에서 GridView의 읽기 전용 동작이 완료 됩니다. 데이터를 볼 때 각 제품은 GridView의 행으로 렌더링 되어 제품의 이름, 범주, 공급 업체 및 단종 상태를 표시 합니다.

[GridView의 읽기 전용 인터페이스가 완료 ![](customizing-the-data-modification-interface-vb/_static/image11.png)](customizing-the-data-modification-interface-vb/_static/image10.png)

**그림 4**: GridView의 읽기 전용 인터페이스가 완료 되었습니다 ([전체 크기 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image12.png)).

> [!NOTE]
> [데이터 삽입, 업데이트 및 삭제 자습서의 개요](an-overview-of-inserting-updating-and-deleting-data-cs.md)에서 설명한 것 처럼 GridView의 뷰 상태를 사용 하도록 설정 하는 것이 매우 중요 합니다 (기본 동작). GridView s `EnableViewState` 속성을 `false`로 설정 하면 동시 사용자가 실수로 레코드를 삭제 하거나 편집 하는 위험을 발생 시킬 수 있습니다. 자세한 내용은 [경고: 편집 및/또는 삭제를 지원 하 고 해당 뷰 상태를 사용할 수 없는 ASP.NET 2.0 gridviews/DetailsView/FormViews의 동시성 문제](http://scottonwriting.net/sowblog/posts/10054.aspx) 를 참조 하세요.

## <a name="step-3-using-a-dropdownlist-for-the-category-and-supplier-editing-interfaces"></a>3 단계: 범주 및 공급자 편집 인터페이스에 대 한 DropDownList 사용

`ProductsRow` 개체에는 `SupplierName` 데이터베이스 테이블의 실제 외래 키 ID 값과 `Products` 및 `Name` 테이블의 해당 `Categories` 값을 제공 하는 `CategoryID`, `CategoryName`, `SupplierID`및 `Suppliers` 속성이 포함 되어 있습니다. `ProductRow`의 `CategoryID` 및 `SupplierID`은 모두 읽고 쓸 수 있으며, `CategoryName` 및 `SupplierName` 속성은 읽기 전용으로 표시 됩니다.

`CategoryName` 및 `SupplierName` 속성의 읽기 전용 상태로 인해 해당 BoundFields는 `ReadOnly` 속성을 `True`로 설정 하 여 행을 편집할 때 이러한 값이 수정 되지 않도록 합니다. `ReadOnly` 속성을 `False`로 설정 하 고, `CategoryName`를 렌더링 하 고, 편집 하는 동안 텍스트 상자를 `SupplierName` 하는 경우 이러한 접근 방식은 `UpdateProduct` 및 `CategoryName` 입력을 사용 하는 `SupplierName` 오버 로드가 없으므로 사용자가 제품을 업데이트 하려고 할 때 예외를 발생 시킵니다. 실제로 다음과 같은 두 가지 이유로 이러한 오버 로드를 만들지 않으려고 합니다.

- `Products` 테이블에는 `SupplierName` 또는 `CategoryName` 필드가 없지만 `SupplierID` 및 `CategoryID`는 있습니다. 따라서 메서드에서 조회 테이블의 값이 아닌 이러한 특정 ID 값을 전달 하려고 합니다.
- 사용자가 사용 가능한 범주와 공급 업체 및 올바른 철자를 알아야 하므로 공급자 또는 범주의 이름을 입력 하도록 요구 하는 것이 이상적입니다.

공급자 및 범주 필드에는 읽기 전용 모드 (현재는 그대로) 및 편집할 때 적용 가능한 옵션의 드롭다운 목록에 있는 범주 및 공급자 이름이 표시 됩니다. 최종 사용자는 드롭다운 목록을 사용 하 여 선택할 수 있는 범주와 공급자를 빠르게 확인 하 고 더 쉽게 선택할 수 있습니다.

이 동작을 제공 하려면 `SupplierName` 및 `CategoryName` BoundFields를 템플릿 필드로 변환 해야 합니다 .이 필드는 `ItemTemplate` `SupplierName` 및 `CategoryName` 값을 내보내고 해당 `EditItemTemplate`에서 DropDownList 컨트롤을 사용 하 여 사용 가능한 범주 및 공급자를 나열 합니다.

## <a name="adding-thecategoriesandsuppliersdropdownlists"></a>`Categories`및`Suppliers`Dropdownlist 추가

먼저 `SupplierName`를 변환 하 고 GridView의 스마트 태그에서 열 편집 링크를 클릭 하 여 BoundFields를 템플릿 필드로 `CategoryName` 합니다. 왼쪽 아래에 있는 목록에서 BoundField를 선택 합니다. "이 필드를 Templatefield로 변환으로 변환" 링크를 클릭 합니다. 변환 프로세스는 아래 선언 구문에 나와 있는 것 처럼 `ItemTemplate`와 `EditItemTemplate`를 모두 사용 하 여 Templatefield로 변환를 만듭니다.

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample4.aspx)]

BoundField는 읽기 전용으로 표시 되어 있으므로 `ItemTemplate` 및 `EditItemTemplate`에는 `Text` 속성이 적용 되는 데이터 필드 (`CategoryName`, 위의 구문)에 바인딩되는 Label 웹 컨트롤이 포함 되어 있습니다. 레이블 웹 컨트롤을 DropDownList 컨트롤로 바꿔서 `EditItemTemplate`를 수정 해야 합니다.

이전 자습서에서 살펴본 것 처럼 디자이너를 통해 또는 선언적 구문에서 직접 템플릿을 편집할 수 있습니다. 디자이너를 통해 편집 하려면 GridView의 스마트 태그에서 템플릿 편집 링크를 클릭 하 고 범주 필드의 `EditItemTemplate`사용 하도록 선택 합니다. 레이블 웹 컨트롤을 제거 하 고 dropdownlist 컨트롤로 바꿔서 DropDownList의 ID 속성을 `Categories`로 설정 합니다.

[텍스트 상자를 제거 하 고 EditItemTemplate에 DropDownList을 추가 ![](customizing-the-data-modification-interface-vb/_static/image14.png)](customizing-the-data-modification-interface-vb/_static/image13.png)

**그림 5**: 텍스트 상자를 제거 하 고 `EditItemTemplate`에 DropDownList 추가 ([전체 크기 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image15.png))

다음으로 DropDownList를 사용 가능한 범주로 채워야 합니다. DropDownList의 스마트 태그에서 데이터 소스 선택 링크를 클릭 하 고 옵트인을 선택 하 여 `CategoriesDataSource`라는 새 ObjectDataSource를 만듭니다.

[![범주 Datasource 라는 새 ObjectDataSource 컨트롤을 만듭니다.](customizing-the-data-modification-interface-vb/_static/image17.png)](customizing-the-data-modification-interface-vb/_static/image16.png)

**그림 6**: `CategoriesDataSource` 이라는 새 ObjectDataSource 컨트롤 만들기 ([전체 크기 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image18.png))

이 ObjectDataSource가 모든 범주를 반환 하도록 하려면 `CategoriesBLL` 클래스의 `GetCategories()` 메서드에 바인딩합니다.

[ObjectDataSource를 범주 Bll의 GetCategories () 메서드에 ![바인딩합니다.](customizing-the-data-modification-interface-vb/_static/image20.png)](customizing-the-data-modification-interface-vb/_static/image19.png)

**그림 7**: ObjectDataSource를 `CategoriesBLL`의 `GetCategories()` 메서드에 바인딩 ([전체 크기 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image21.png))

마지막으로 값으로 사용 되는 `CategoryID` 필드를 사용 하 여 `CategoryName` 필드가 각 DropDownList `ListItem`에 표시 되도록 DropDownList의 설정을 구성 합니다.

[범주 필드와 값으로 사용 되는 CategoryID를 표시 ![](customizing-the-data-modification-interface-vb/_static/image23.png)](customizing-the-data-modification-interface-vb/_static/image22.png)

**그림 8**: `CategoryName` 필드가 표시 되 고 `CategoryID` 값으로 사용 ([전체 크기 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image24.png))

이러한 변경을 수행한 후 `CategoryName` Templatefield로 변환의 `EditItemTemplate`에 대 한 선언적 태그는 DropDownList 및 ObjectDataSource를 모두 포함 합니다.

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample5.aspx)]

> [!NOTE]
> `EditItemTemplate`에서 DropDownList의 뷰 상태를 사용 하도록 설정 해야 합니다. 곧 DropDownList의 선언적 구문에 데이터 바인딩 구문을 추가 하 고 `Eval()` `Bind()`와 같은 데이터 바인딩 명령을 추가 하 여 뷰 상태를 사용 하는 컨트롤에만 나타날 수 있습니다.

이러한 단계를 반복 하 여 `SupplierName` Templatefield로 변환의 `EditItemTemplate`에 `Suppliers` 라는 DropDownList을 추가 합니다. 이렇게 하려면 `EditItemTemplate`에 DropDownList을 추가 하 고 다른 ObjectDataSource를 만들어야 합니다. 그러나 `Suppliers` DropDownList의 ObjectDataSource는 `SuppliersBLL` 클래스의 `GetSuppliers()` 메서드를 호출 하도록 구성 되어야 합니다. 또한 `Suppliers` DropDownList을 구성 하 여 `CompanyName` 필드를 표시 하 고 `SupplierID` 필드를 `ListItem` s에 대 한 값으로 사용 합니다.

두 `EditItemTemplate` s에 Dropdownlist를 추가한 후 브라우저에서 페이지를 로드 하 고 Chef Anton의 Cajun Seasoning product에 대 한 편집 단추를 클릭 합니다. 그림 9에 표시 된 것 처럼 제품의 범주 및 공급자 열은 선택할 수 있는 범주 및 공급자가 포함 된 드롭다운 목록으로 렌더링 됩니다. 그러나 Chef Anton의 Cajun Seasoning가 새 Orleans Cajun Delights에서 제공 되는 경우에도 두 드롭다운 목록의 *첫 번째* 항목이 기본적으로 선택 되어 있습니다 (범주의 음료 및 Exotic Liquids).

[드롭다운 목록의 첫 번째 항목을 ![기본적으로 선택 됩니다.](customizing-the-data-modification-interface-vb/_static/image26.png)](customizing-the-data-modification-interface-vb/_static/image25.png)

**그림 9**: 드롭다운 목록의 첫 번째 항목이 기본적으로 선택 되어 있습니다 ([전체 크기 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image27.png)).

또한 업데이트를 클릭 하면 제품의 `CategoryID` 및 `SupplierID` 값이 `NULL`으로 설정 된 것을 알 수 있습니다. 이러한 원치 않는 동작은 `EditItemTemplate` s의 Dropdownlist가 기본 제품 데이터의 데이터 필드에 바인딩되지 않기 때문에 발생 합니다.

## <a name="binding-the-dropdownlists-to-thecategoryidandsupplieriddata-fields"></a>`CategoryID`및`SupplierID`데이터 필드에 Dropdownlist 바인딩

편집 된 제품의 범주 및 공급자 드롭다운 목록을 적절 한 값으로 설정 하 고 업데이트를 클릭 했을 때 이러한 값이 BLL의 `UpdateProduct` 메서드로 다시 전송 되도록 하려면 Dropdownlist ' `SelectedValue` 속성을 `CategoryID`에 바인딩하고 양방향 데이터 바인딩을 사용 하 여 데이터 필드를 `SupplierID` 해야 합니다. `Categories` DropDownList를 사용 하 여이를 수행 하려면 선언적 구문에 `SelectedValue='<%# Bind("CategoryID") %>'`를 직접 추가할 수 있습니다.

또는 디자이너를 통해 템플릿을 편집 하 고 DropDownList의 스마트 태그에서 데이터 바인딩 편집 링크를 클릭 하 여 DropDownList의 데이터 집합을 설정할 수 있습니다. 그런 다음 양방향 데이터 바인딩을 사용 하 여 `SelectedValue` 속성이 `CategoryID` 필드에 바인딩되어야 함을 표시 합니다 (그림 10 참조). 선언적 또는 디자이너 프로세스를 반복 하 여 `SupplierID` 데이터 필드를 `Suppliers` DropDownList에 바인딩합니다.

[양방향 데이터 바인딩을 사용 하 여 ![CategoryID를 DropDownList의 SelectedValue 속성에 바인딩합니다.](customizing-the-data-modification-interface-vb/_static/image29.png)](customizing-the-data-modification-interface-vb/_static/image28.png)

**그림 10**: 양방향 데이터 바인딩을 사용 하 여 `CategoryID`를 DropDownList의 `SelectedValue` 속성에 바인딩 ([전체 크기 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image30.png))

바인딩이 두 Dropdownlist의 `SelectedValue` 속성에 적용 된 후에는 편집 된 제품의 범주 및 공급자 열이 기본적으로 현재 제품의 값으로 바뀝니다. 업데이트를 클릭 하면 선택한 드롭다운 목록 항목의 `CategoryID` 및 `SupplierID` 값이 `UpdateProduct` 메서드에 전달 됩니다. 그림 11에서는 데이터 바인딩 문이 추가 된 후의 자습서를 보여 줍니다. Chef Anton의 Cajun Seasoning에 대해 선택한 드롭다운 목록 항목은 제대로 작동 하 고 새로운 Orleans Cajun Delights에 대 한 정보를 확인 합니다.

[![편집 된 제품의 현재 범주 및 공급자 값이 기본적으로 선택 됩니다.](customizing-the-data-modification-interface-vb/_static/image32.png)](customizing-the-data-modification-interface-vb/_static/image31.png)

**그림 11**: 편집 된 제품의 현재 범주 및 공급자 값이 기본적으로 선택 되어 있습니다 ([전체 크기 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image33.png)).

## <a name="handlingnullvalues"></a>`NULL`값 처리

`Products` 테이블의 `CategoryID` 및 `SupplierID` 열을 `NULL`수 있지만 `EditItemTemplate`의 Dropdownlist에는 `NULL` 값을 나타내는 목록 항목이 포함 되지 않습니다. 이 경우 두 가지 결과가 발생 합니다.

- 사용자는 인터페이스를 사용 하 여 제품의 범주 또는 공급자를`NULL` 이외의 값에서 `NULL`로 변경할 수 없습니다.
- 제품에 `NULL` `CategoryID` 또는 `SupplierID`있는 경우 편집 단추를 클릭 하면 예외가 발생 합니다. 이는 `Bind()` 문의 `CategoryID` (또는 `SupplierID`)에서 반환 된 `NULL` 값이 DropDownList의 값에 매핑되지 않기 때문입니다. (`SelectedValue` 속성이 목록 항목의 컬렉션에 *없는* 값으로 설정 된 경우에는 dropdownlist에서 예외가 throw 됩니다.)

`NULL` `CategoryID` 및 `SupplierID` 값을 지원 하기 위해 각 DropDownList에 다른 `ListItem`를 추가 하 여 `NULL` 값을 표시 해야 합니다. DropDownList 자습서를 사용 하 여 [마스터/세부 정보 필터링](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) 에서 dropdownlist의 `AppendDataBoundItems` 속성을 `True`로 설정 하 고 추가 `ListItem`를 수동으로 추가 하는 것과 관련 된 데이터 바인딩된 DropDownList에 추가 `ListItem`를 추가 하는 방법을 살펴보았습니다. 그러나 이전 자습서에서는 `-1`의 `Value`를 사용 하 여 `ListItem`를 추가 했습니다. 그러나 ASP.NET의 데이터 바인딩 논리는 빈 문자열을 `NULL` 값으로 자동으로 변환 하 고 그 반대의 경우도 마찬가지입니다. 따라서이 자습서에서는 `ListItem`의 `Value`를 빈 문자열로 만들려고 합니다.

Dropdownlist ' `AppendDataBoundItems` 속성을 `True`으로 설정 하 여 시작 합니다. 다음으로, 다음 `<asp:ListItem>` 요소를 각 DropDownList에 추가 하 여 선언적 태그가 표시 되도록 `NULL` `ListItem`를 추가 합니다.

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample6.aspx)]

이 `ListItem`에 대 한 텍스트 값으로 "(None)"을 사용 하기로 선택 했지만 원하는 경우 빈 문자열을 사용 하도록 변경할 수도 있습니다.

> [!NOTE]
> DropDownList 자습서를 *사용 하 여 마스터/세부 정보 필터링* 에서 살펴본 것 처럼 속성 창에서 dropdownlist의 `Items` 속성을 클릭 하 여 디자이너를 통해 `ListItem`를 dropdownlist에 추가할 수 있습니다 (`ListItem` 컬렉션 편집기가 표시 됨). 그러나 선언적 구문을 통해이 자습서에 대 한 `NULL` `ListItem`를 추가 해야 합니다. `ListItem` 컬렉션 편집기를 사용 하는 경우 생성 된 선언적 구문은 빈 문자열이 할당 될 때 `Value` 설정을 완전히 생략 하 고 `<asp:ListItem>(None)</asp:ListItem>`와 같은 선언 태그를 만듭니다. 이는 무해 한 것 처럼 보일 수 있지만, 값이 누락 되 면 DropDownList은 대신 `Text` 속성 값을 사용 합니다. 즉,이 `NULL` `ListItem`를 선택 하면 `CategoryID`에 "(없음)" 값이 할당 되어 예외가 발생 합니다. `Value=""`를 명시적으로 설정 하 여 `NULL` `ListItem`를 선택 하면 `CategoryID`에 `NULL` 값이 할당 됩니다.

Suppliers DropDownList에 대해 이러한 단계를 반복 합니다.

이 추가 `ListItem`를 사용 하면 그림 12와 같이 편집 인터페이스에서 제품의 `CategoryID` 및 `SupplierID` 필드에 `NULL` 값을 할당할 수 있습니다.

[제품의 범주 또는 공급 업체에 NULL 값을 할당 하려면 (없음)을 선택 ![.](customizing-the-data-modification-interface-vb/_static/image35.png)](customizing-the-data-modification-interface-vb/_static/image34.png)

**그림 12**: (없음)을 선택 하 여 제품의 범주 또는 공급 업체에 대 한 `NULL` 값 할당 ([전체 크기 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image36.png))

## <a name="step-4-using-radiobuttons-for-the-discontinued-status"></a>4 단계: 단종 된 상태에 대해 Radiobutton 사용

현재 제품의 `Discontinued` 데이터 필드는 CheckBoxField를 사용 하 여 표현 됩니다 .이 필드는 편집 중인 행에 대해 읽기 전용 행 및 사용 확인란을 사용 하지 않도록 설정 된 확인란을 렌더링 합니다. 이 사용자 인터페이스를 사용 하는 것이 적합할 수 있지만 필요한 경우 Templatefield로 변환를 사용 하 여 사용자 지정할 수 있습니다. 이 자습서에서는 사용자가 제품의 `Discontinued` 값을 지정할 수 있는 두 가지 옵션 "활성" 및 "중단"이 있는 RadioButtonList 컨트롤을 사용 하는 Templatefield로 변환로 CheckBoxField를 변경 하겠습니다.

`Discontinued` CheckBoxField를 Templatefield로 변환로 변환 하 여 시작 합니다. 그러면 `ItemTemplate` 및 `EditItemTemplate`를 사용 하 여 Templatefield로 변환을 만듭니다. 두 템플릿에는 모두 `Discontinued` 데이터 필드에 바인딩된 `Checked` 속성이 있는 확인란이 포함 되어 있으며, 두 가지 사이의 유일한 차이점은 `ItemTemplate`의 CheckBox `Enabled` 속성이 `False`로 설정 된다는 것입니다.

`ItemTemplate` 및 `EditItemTemplate`의 확인란을 모두 RadioButtonList 컨트롤을 사용 하 여 RadioButtonLists ' `ID` 속성을 `DiscontinuedChoice`로 설정 합니다. 다음으로 RadioButtonLists에 각각 "False" 값을 가진 "활성" 이라는 두 개의 라디오 단추와 "True" 값을 갖는 "단종" 레이블이 지정 된 라디오 단추가 각각 하나씩 포함 되어야 함을 표시 합니다. 이를 위해 선언적 구문을 통해에 `<asp:ListItem>` 요소를 직접 입력 하거나 디자이너에서 `ListItem` 컬렉션 편집기를 사용할 수 있습니다. 그림 13에서는 두 개의 라디오 단추 옵션이 지정 된 후 `ListItem` 컬렉션 편집기를 보여 줍니다.

[RadioButtonList에 활성 및 지원 되지 않는 옵션을 추가 ![](customizing-the-data-modification-interface-vb/_static/image38.png)](customizing-the-data-modification-interface-vb/_static/image37.png)

**그림 13**: RadioButtonList에 활성 및 중단 된 옵션 추가 ([전체 크기 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image39.png))

`ItemTemplate`의 RadioButtonList를 편집할 수 없으므로 `Enabled` 속성을 `False`로 설정 하 여 `Enabled` 속성을 `True`의 RadioButtonList에 대 한 `EditItemTemplate`(기본값)로 둡니다. 이렇게 하면 편집 되지 않은 행의 라디오 단추가 읽기 전용으로 설정 되지만 사용자가 편집 된 행의 RadioButton 값을 변경할 수 있습니다.

제품의 `Discontinued` 데이터 필드에 따라 적절 한 라디오 단추가 선택 되도록 RadioButtonList 컨트롤의 `SelectedValue` 속성을 할당 해야 합니다. 이 자습서의 앞부분에서 살펴본 Dropdownlist와 마찬가지로이 데이터 바인딩 구문은 선언적 태그에 직접 추가 하거나 RadioButtonLists ' 스마트 태그의 데이터 바인딩 편집 링크를 통해 추가할 수 있습니다.

두 RadioButtonLists를 추가 하 고 구성 하 고 나면 `Discontinued` Templatefield로 변환의 선언 태그는 다음과 같습니다.

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample7.aspx)]

이러한 변경 내용으로 인해 `Discontinued` 열이 확인란 목록에서 라디오 단추 쌍 목록으로 변환 되었습니다 (그림 14 참조). 제품을 편집 하는 경우 해당 라디오 단추가 선택 되 고, 다른 라디오 단추를 선택 하 고 업데이트를 클릭 하 여 제품의 단종 된 상태를 업데이트할 수 있습니다.

[지원 되지 않는 확인란이 라디오 단추 쌍으로 대체 ![](customizing-the-data-modification-interface-vb/_static/image41.png)](customizing-the-data-modification-interface-vb/_static/image40.png)

**그림 14**: 단종 된 확인란이 라디오 단추 쌍으로 대체 되었습니다 ([전체 크기 이미지를 보려면 클릭](customizing-the-data-modification-interface-vb/_static/image42.png)).

> [!NOTE]
> `Products` 데이터베이스의 `Discontinued` 열에는 `NULL` 값이 포함 될 수 없으므로 인터페이스에서 `NULL` 정보를 캡처하는 데 걱정할 필요가 없습니다. 그러나 `Discontinued` 열에 `NULL` 값이 포함 될 수 있는 경우 category 및 공급자 Dropdownlist 같이 `Value` 빈 문자열 (`Value=""`)로 설정 된 세 번째 라디오 단추를 목록에 추가 하려고 합니다.

## <a name="summary"></a>요약

BoundField 및 CheckBoxField는 읽기 전용, 편집 및 삽입 인터페이스를 자동으로 렌더링 하지만 사용자 지정 기능을 제공 하지는 않습니다. 그러나 종종 이전 자습서에서 살펴본 것 처럼 유효성 검사 컨트롤을 추가 하거나이 자습서에서 살펴본 것 처럼 데이터 컬렉션 사용자 인터페이스를 사용자 지정 하 여 편집 또는 삽입 인터페이스를 사용자 지정 해야 합니다. Templatefield로 변환를 사용 하 여 인터페이스를 사용자 지정 하는 작업은 다음 단계에서 합계를 계산할 수 있습니다.

1. Templatefield로 변환를 추가 하거나 기존 BoundField 또는 CheckBoxField를 Templatefield로 변환로 변환 합니다.
2. 필요에 따라 인터페이스 보강
3. 양방향 데이터 바인딩을 사용 하 여 새로 추가 된 웹 컨트롤에 적절 한 데이터 필드 바인딩

기본 제공 ASP.NET 웹 컨트롤 외에도 사용자 지정, 컴파일된 서버 컨트롤 및 사용자 정의 컨트롤을 사용 하 여 Templatefield로 변환의 템플릿을 사용자 지정할 수 있습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

> [!div class="step-by-step"]
> [이전](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)
> [다음](implementing-optimistic-concurrency-vb.md)
