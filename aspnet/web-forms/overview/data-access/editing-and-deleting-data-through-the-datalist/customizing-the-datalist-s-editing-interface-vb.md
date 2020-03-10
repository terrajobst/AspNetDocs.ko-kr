---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/customizing-the-datalist-s-editing-interface-vb
title: DataList의 편집 인터페이스 사용자 지정 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 Dropdownlist 및 CheckBox를 포함 하는 DataList에 대 한 다양 한 편집 인터페이스를 만듭니다.
ms.author: riande
ms.date: 10/30/2006
ms.assetid: 718628e2-224c-455f-b33a-a41efd48d5a0
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/customizing-the-datalist-s-editing-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: adee419764cff2f39ee16962080c24b52553aa14
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78480461"
---
# <a name="customizing-the-datalists-editing-interface-vb"></a>DataList의 편집 인터페이스 사용자 지정(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_40_VB.exe) 또는 [PDF 다운로드](customizing-the-datalist-s-editing-interface-vb/_static/datatutorial40vb1.pdf)

> 이 자습서에서는 Dropdownlist 및 CheckBox를 포함 하는 DataList에 대 한 다양 한 편집 인터페이스를 만듭니다.

## <a name="introduction"></a>소개

DataList s의 태그 및 웹 컨트롤 `EditItemTemplate` 편집 가능한 인터페이스를 정의 합니다. 지금까지 살펴본 편집 가능한 모든 DataList 예제에서는 편집 가능한 인터페이스가 TextBox 웹 컨트롤로 구성 되었습니다. [이전 자습서](adding-validation-controls-to-the-datalist-s-editing-interface-vb.md) 에서는 유효성 검사 컨트롤을 추가 하 여 편집 시간 사용자 환경을 개선 했습니다.

Dropdownlist, RadioButtonLists, 캘린더 등의 텍스트 상자 이외의 웹 컨트롤을 포함 하도록 `EditItemTemplate`를 추가로 확장할 수 있습니다. 텍스트 상자와 마찬가지로 다른 웹 컨트롤을 포함 하도록 편집 인터페이스를 사용자 지정 하는 경우 다음 단계를 따릅니다.

1. 웹 컨트롤을 `EditItemTemplate`에 추가 합니다.
2. 데이터 바인딩 구문을 사용 하 여 해당 하는 데이터 필드 값을 해당 속성에 할당 합니다.
3. `UpdateCommand` 이벤트 처리기에서 프로그래밍 방식으로 웹 컨트롤 값에 액세스 하 여 적절 한 BLL 메서드에 전달 합니다.

이 자습서에서는 Dropdownlist 및 CheckBox를 포함 하는 DataList에 대 한 다양 한 편집 인터페이스를 만듭니다. 특히 제품 정보를 나열 하 고 제품 이름, 공급자, 범주 및 중단 된 상태를 업데이트 하도록 허용 하는 DataList를 만듭니다 (그림 1 참조).

[편집 인터페이스 ![텍스트 상자, 두 개의 Dropdownlist 및 확인란을 포함 합니다.](customizing-the-datalist-s-editing-interface-vb/_static/image2.png)](customizing-the-datalist-s-editing-interface-vb/_static/image1.png)

**그림 1**: 편집 인터페이스에는 텍스트 상자, 두 개의 Dropdownlist 및 확인란 ([전체 크기 이미지를 보려면 클릭](customizing-the-datalist-s-editing-interface-vb/_static/image3.png))이 포함 되어 있습니다.

## <a name="step-1-displaying-product-information"></a>1 단계: 제품 정보 표시

DataList s 편집 가능 인터페이스를 만들려면 먼저 읽기 전용 인터페이스를 빌드해야 합니다. 먼저 `EditDeleteDataList` 폴더에서 `CustomizedUI.aspx` 페이지를 열고 디자이너에서 페이지에 DataList를 추가 하 여 `ID` 속성을 `Products`로 설정 합니다. DataList s 스마트 태그에서 새 ObjectDataSource를 만듭니다. 이 새 ObjectDataSource `ProductsDataSource`의 이름을로 설정 하 고 `ProductsBLL` 클래스의 `GetProducts` 메서드에서 데이터를 검색 하도록 구성 합니다. 이전에 편집 가능한 DataList 자습서와 마찬가지로 비즈니스 논리 계층으로 직접 이동 하 여 편집 된 제품 정보를 업데이트 합니다. 따라서 업데이트, 삽입 및 삭제 탭의 드롭다운 목록을 (없음)으로 설정 합니다.

[![업데이트, 삽입 및 삭제 탭 드롭다운 목록을 (없음)으로 설정 합니다.](customizing-the-datalist-s-editing-interface-vb/_static/image5.png)](customizing-the-datalist-s-editing-interface-vb/_static/image4.png)

**그림 2**: 업데이트, 삽입 및 삭제 탭 드롭다운 목록을 (없음)로 설정 ([전체 크기 이미지를 보려면 클릭](customizing-the-datalist-s-editing-interface-vb/_static/image6.png))

ObjectDataSource를 구성한 후 Visual Studio에서 반환 된 각 데이터 필드의 이름과 값을 나열 하는 DataList의 기본 `ItemTemplate`를 만듭니다. 템플릿이 범주 이름, 공급 업체 이름, 가격 및 단종 상태와 함께 `<h4>` 요소의 제품 이름을 나열 하도록 `ItemTemplate`를 수정 합니다. 또한 편집 단추를 추가 하 여 해당 `CommandName` 속성이 편집으로 설정 되어 있는지 확인 합니다. 내 `ItemTemplate`에 대 한 선언적 태그는 다음과 같습니다.

[!code-aspx[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample1.aspx)]

위의 태그는 제품 이름에는 &lt;h4&gt; 제목을 사용 하 고 나머지 필드에는 네 개의 열 `<table>` 사용 하 여 제품 정보를 배치 합니다. 이전 자습서에서는 `Styles.css`에 정의 된 `ProductPropertyLabel` 및 `ProductPropertyValue` CSS 클래스에 대해 설명 했습니다. 그림 3에서는 브라우저를 통해 볼 때의 진행률을 보여 줍니다.

[![각 제품의 이름, 공급자, 범주, 단종 된 상태 및 가격이 표시 됩니다.](customizing-the-datalist-s-editing-interface-vb/_static/image8.png)](customizing-the-datalist-s-editing-interface-vb/_static/image7.png)

**그림 3**: 이름, 공급자, 범주, 단종 된 상태 및 각 제품의 가격이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](customizing-the-datalist-s-editing-interface-vb/_static/image9.png)).

## <a name="step-2-adding-the-web-controls-to-the-editing-interface"></a>2 단계: 편집 인터페이스에 웹 컨트롤 추가

사용자 지정 DataList 편집 인터페이스를 빌드하는 첫 번째 단계는 필요한 웹 컨트롤을 `EditItemTemplate`에 추가 하는 것입니다. 특히, 해당 범주에 대 한 DropDownList, 공급자에 대 한 DropDownList 및 단종 된 상태에 대 한 확인란을 선택 해야 합니다. 이 예제에서는 제품 가격을 편집할 수 없기 때문에 Label 웹 컨트롤을 사용 하 여 계속 표시할 수 있습니다.

편집 인터페이스를 사용자 지정 하려면 DataList s 스마트 태그에서 템플릿 편집 링크를 클릭 하 고 드롭다운 목록에서 `EditItemTemplate` 옵션을 선택 합니다. `EditItemTemplate`에 DropDownList을 추가 하 고 해당 `ID`를 `Categories`로 설정 합니다.

[범주에 대 한 DropDownList을 추가 ![](customizing-the-datalist-s-editing-interface-vb/_static/image11.png)](customizing-the-datalist-s-editing-interface-vb/_static/image10.png)

**그림 4**: 범주에 대 한 DropDownList 추가 ([전체 크기 이미지를 보려면 클릭](customizing-the-datalist-s-editing-interface-vb/_static/image12.png))

다음으로, DropDownList의 스마트 태그에서 데이터 원본 선택 옵션을 선택 하 고 `CategoriesDataSource`라는 새 ObjectDataSource를 만듭니다. `CategoriesBLL` 클래스 s `GetCategories()` 메서드를 사용 하도록이 ObjectDataSource를 구성 합니다 (그림 5 참조). 그런 다음 각 `ListItem` s `Text` 및 `Value` 속성에 사용할 데이터 필드를 입력 하 라는 메시지가 표시 됩니다. 그림 6에 표시 된 것 처럼 DropDownList에 `CategoryName` 데이터 필드를 표시 하 고 `CategoryID` 값으로 사용 하도록 합니다.

[새 ObjectDataSource 라는 범주 데이터 원본을 만듭니다 ![](customizing-the-datalist-s-editing-interface-vb/_static/image14.png)](customizing-the-datalist-s-editing-interface-vb/_static/image13.png)

**그림 5**: 이름이 `CategoriesDataSource` 새 ObjectDataSource 만들기 ([전체 크기 이미지를 보려면 클릭](customizing-the-datalist-s-editing-interface-vb/_static/image15.png))

[DropDownList s 표시 및 값 필드를 구성 ![](customizing-the-datalist-s-editing-interface-vb/_static/image17.png)](customizing-the-datalist-s-editing-interface-vb/_static/image16.png)

**그림 6**: DropDownList s 표시 및 값 필드 구성 ([전체 크기 이미지를 보려면 클릭](customizing-the-datalist-s-editing-interface-vb/_static/image18.png))

이러한 일련의 단계를 반복 하 여 공급자에 대 한 DropDownList을 만듭니다. 이 DropDownList의 `ID`를 `Suppliers` 하 고 해당 ObjectDataSource `SuppliersDataSource`의 이름을로 설정 합니다.

두 Dropdownlist를 추가한 후에는 단종 된 상태에 대 한 확인란을 추가 하 고 제품 이름에 텍스트 상자를 추가 합니다. 확인란 및 텍스트 상자에 대 한 `ID`를 각각 `Discontinued` 및 `ProductName`로 설정 합니다. 사용자가 제품 이름에 대 한 값을 제공할 수 있도록 RequiredFieldValidator를 추가 합니다.

마지막으로 업데이트 및 취소 단추를 추가 합니다. 이러한 두 단추에 대해 `CommandName` 속성이 각각 Update 및 Cancel로 설정 되도록 해야 합니다.

원하는 대로 편집 인터페이스를 자유롭게 레이아웃 하세요. 다음 선언 구문과 스크린샷에서 설명 하는 것 처럼 읽기 전용 인터페이스에서 동일한 네 열 `<table>` 레이아웃을 사용 하기로 결정 했습니다.

[!code-aspx[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample2.aspx)]

[편집 인터페이스를 읽기 전용 인터페이스 처럼 배치 ![](customizing-the-datalist-s-editing-interface-vb/_static/image20.png)](customizing-the-datalist-s-editing-interface-vb/_static/image19.png)

**그림 7**: 편집 인터페이스는 읽기 전용 인터페이스와 같이 레이아웃 됩니다 ([전체 크기 이미지를 보려면 클릭](customizing-the-datalist-s-editing-interface-vb/_static/image21.png)).

## <a name="step-3-creating-the-editcommand-and-cancelcommand-event-handlers"></a>3 단계: EditCommand 및 CancelCommand 이벤트 처리기 만들기

현재 `EditItemTemplate`에는 데이터 바인딩 구문이 없습니다. `UnitPriceLabel`를 제외 하 고 `ItemTemplate`의 축 자 위에 복사 되었습니다. 데이터 바인딩 구문은 일시적으로 추가 되지만 먼저 DataList s `EditCommand` 및 `CancelCommand` 이벤트에 대 한 이벤트 처리기를 만듭니다. `EditCommand` 이벤트 처리기의 책임이 편집 단추를 클릭 한 DataList 항목에 대 한 편집 인터페이스를 렌더링 하는 것입니다. 반면 `CancelCommand`의 작업은 DataList를 사전 편집 상태로 반환 하는 것입니다.

이러한 두 이벤트 처리기를 만들고 다음 코드를 사용 하도록 합니다.

[!code-vb[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample3.vb)]

이러한 두 이벤트 처리기를 배치한 상태에서 편집 단추를 클릭 하면 편집 인터페이스가 표시 되 고 취소 단추를 클릭 하면 편집 된 항목이 읽기 전용 모드로 돌아갑니다. 그림 8에서는 편집 단추가 Chef Anton s Gumbo Mix에 대해 클릭 된 후의 DataList를 보여 줍니다. 편집 인터페이스에 데이터 바인딩 구문을 추가 하려고 하기 때문에 `ProductName` TextBox는 비어 있고 `Discontinued` 확인란은 선택 취소 되어 있고 `Categories`에서 선택한 첫 번째 항목과 `Suppliers` Dropdownlist.

[편집 단추를 클릭 하면 편집 인터페이스가 표시 ![.](customizing-the-datalist-s-editing-interface-vb/_static/image23.png)](customizing-the-datalist-s-editing-interface-vb/_static/image22.png)

**그림 8**: 편집 단추를 클릭 하면 편집 인터페이스가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](customizing-the-datalist-s-editing-interface-vb/_static/image24.png)).

## <a name="step-4-adding-the-databinding-syntax-to-the-editing-interface"></a>4 단계: 편집 인터페이스에 데이터 바인딩 구문 추가

편집 인터페이스에 현재 제품 값이 표시 되도록 하려면 데이터 바인딩 구문을 사용 하 여 데이터 필드 값을 적절 한 웹 컨트롤 값에 할당 해야 합니다. 디자이너를 통해 템플릿 편집 화면으로 이동 하 고 웹 컨트롤 스마트 태그에서 데이터 바인딩 편집 링크를 선택 하 여 데이터 바인딩 구문을 적용할 수 있습니다. 또는 선언적 태그에 직접 데이터 바인딩 구문을 추가할 수 있습니다.

`ProductName` 데이터 필드 값을 `ProductName` TextBox s `Text` 속성에 할당 하 고, `CategoryID` 및 `SupplierID` 데이터 필드 값을 `Categories` 및 `Suppliers` Dropdownlist `SelectedValue` 속성에 할당 하 고, `Discontinued` 데이터 필드 값을 `Discontinued` CheckBox s `Checked` 속성에 할당 합니다. 디자이너를 통해 또는 선언적 태그를 통해 직접 이러한 변경을 수행한 후 브라우저를 통해 페이지를 다시 방문 하 고 Chef Anton s Gumbo 조합에 대 한 편집 단추를 클릭 합니다. 그림 9에 표시 된 것 처럼 데이터 바인딩 구문은 텍스트 상자, Dropdownlist 및 확인란에 현재 값을 추가 했습니다.

[편집 단추를 클릭 하면 편집 인터페이스가 표시 ![.](customizing-the-datalist-s-editing-interface-vb/_static/image26.png)](customizing-the-datalist-s-editing-interface-vb/_static/image25.png)

**그림 9**: 편집 단추를 클릭 하면 편집 인터페이스가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](customizing-the-datalist-s-editing-interface-vb/_static/image27.png)).

## <a name="step-5-saving-the-user-s-changes-in-the-updatecommand-event-handler"></a>5 단계: UpdateCommand 이벤트 처리기에서 사용자 변경 내용 저장

사용자가 제품을 편집 하 고 업데이트 단추를 클릭 하면 포스트백이 발생 하 고 DataList s `UpdateCommand` 이벤트가 발생 합니다. 이벤트 처리기에서 `EditItemTemplate`의 웹 컨트롤에서 값을 읽고 BLL과 인터페이스 하 여 데이터베이스의 제품을 업데이트 해야 합니다. 이전 자습서에서 보았듯이 업데이트 된 제품의 `ProductID` `DataKeys` 컬렉션을 통해 액세스할 수 있습니다. 사용자가 입력 한 필드는 다음 코드에 표시 된 대로 `FindControl("controlID")`를 사용 하 여 프로그래밍 방식으로 웹 컨트롤을 참조 하 여 액세스 됩니다.

[!code-vb[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample4.vb)]

이 코드는 페이지의 모든 유효성 검사 컨트롤이 올바른지 확인 하기 위해 `Page.IsValid` 속성을 확인 하 여 시작 합니다. `Page.IsValid` `True`되 면 편집 된 제품의 `ProductID` 값을 `DataKeys` 컬렉션에서 읽고 `EditItemTemplate`의 데이터 입력 웹 컨트롤을 프로그래밍 방식으로 참조 합니다. 그런 다음 이러한 웹 컨트롤의 값을 적절 한 `UpdateProduct` 오버 로드에 전달 하는 변수로 읽어옵니다. 데이터를 업데이트 한 후에는 DataList가 미리 편집 상태로 돌아갑니다.

> [!NOTE]
> 코드와이 예제를 집중적으로 유지 하기 위해 [BLL 및 DAL 수준 예외 처리](handling-bll-and-dal-level-exceptions-vb.md) 자습서에 추가 된 예외 처리 논리를 생략 했습니다. 연습으로이 자습서를 완료 한 후이 기능을 추가 합니다.

## <a name="step-6-handling-null-categoryid-and-supplierid-values"></a>6 단계: NULL CategoryID 및 공급자 값 처리

Northwind 데이터베이스를 사용 하면 `Products` 테이블 s `CategoryID` 및 `SupplierID` 열에 대해 `NULL` 값을 사용할 수 있습니다. 그러나 현재 편집 인터페이스는 `NULL` 값을 현재 수용 하지 않습니다. `CategoryID` 또는 `SupplierID` `ArgumentOutOfRangeException` 열에 대해 `NULL` 값이 있는 제품을 편집 하려고 하면 다음과 유사한 오류 메시지가 표시 됩니다. *' Categories '에는 항목 목록에 존재 하지 않기 때문에 잘못 된 SelectedValue가 있습니다* . 또한 현재`NULL` 되지 않은 값에서 `NULL` 1로 제품 범주나 공급자 값을 변경할 수 있는 방법은 없습니다.

Category 및 공급자 Dropdownlist에 대 한 `NULL` 값을 지원 하려면 추가 `ListItem`를 추가 해야 합니다. (없음)을이 `ListItem`에 대 한 `Text` 값으로 사용 하도록 선택 했지만, 원하는 경우에는 다른 값 (예: 빈 문자열)으로 변경할 수 있습니다. 마지막으로 Dropdownlist `AppendDataBoundItems`를 `True`으로 설정 해야 합니다. 이렇게 하지 않으면 DropDownList에 바인딩된 범주 및 공급자가 정적으로 추가 된 `ListItem`을 덮어씁니다.

이러한 변경을 수행한 후에는 DataList s `EditItemTemplate`의 Dropdownlist 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample5.aspx)]

> [!NOTE]
> 정적 `ListItem`은 디자이너를 통해 또는 선언적 구문을 통해 직접 DropDownList에 추가할 수 있습니다. 데이터베이스 `NULL` 값을 나타내는 DropDownList 항목을 추가할 때는 선언적 구문을 통해 `ListItem`를 추가 해야 합니다. 디자이너에서 `ListItem` 컬렉션 편집기를 사용 하는 경우 생성 된 선언적 구문은 빈 문자열이 할당 될 때 `Value` 설정을 완전히 생략 하 여 `<asp:ListItem>(None)</asp:ListItem>`와 같은 선언 태그를 만듭니다. 이는 무해 하 게 보일 수 있지만 누락 된 `Value`를 사용 하면 DropDownList에서 `Text` 속성 값을 사용 합니다. 즉,이 `NULL` `ListItem`를 선택 하면 제품 데이터 필드에 값 (None)이 할당 됩니다 (이 자습서에서는`CategoryID` 또는 `SupplierID`) .이로 인해 예외가 발생 합니다. `Value=""`를 명시적으로 설정 하 여 `NULL` `ListItem`를 선택 하면 제품 데이터 필드에 `NULL` 값이 할당 됩니다.

잠시 시간을 내 서 브라우저를 통해 진행 상황을 확인 하세요. 제품을 편집할 때 `Categories` 및 `Suppliers` Dropdownlist에는 모두 DropDownList의 시작 부분에 (없음) 옵션이 있습니다.

[범주 및 공급 업체 Dropdownlist (없음) 옵션을 포함 하는 ![](customizing-the-datalist-s-editing-interface-vb/_static/image29.png)](customizing-the-datalist-s-editing-interface-vb/_static/image28.png)

**그림 10**: `Categories` 및 `Suppliers` dropdownlist는 (없음) 옵션 ([전체 크기 이미지를 보려면 클릭](customizing-the-datalist-s-editing-interface-vb/_static/image30.png))을 포함 합니다.

(없음) 옵션을 데이터베이스 `NULL` 값으로 저장 하려면 `UpdateCommand` 이벤트 처리기로 돌아가야 합니다. `categoryIDValue` 및 `supplierIDValue` 변수를 nullable 정수로 변경 하 고 DropDownList `SelectedValue`가 빈 문자열이 아닌 경우에만 `Nothing` 이외의 값을 할당 합니다.

[!code-vb[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample6.vb)]

이러한 변경으로 인해 사용자가 `NULL` 데이터베이스 값에 해당 하는 드롭다운 목록에서 (없음) 옵션을 선택 하는 경우 `Nothing` 값이 `UpdateProduct` BLL 메서드에 전달 됩니다.

## <a name="summary"></a>요약

이 자습서에서는 세 가지 입력 웹 컨트롤을 포함 하는 더 복잡 한 DataList 편집 인터페이스를 만드는 방법에 대해 설명 합니다 .이 인터페이스에는 텍스트 상자, 두 개의 Dropdownlist 및 유효성 검사 컨트롤과 함께 확인란이 포함 되어 있습니다. 편집 인터페이스를 빌드할 때 사용 되는 웹 컨트롤에 관계 없이 단계가 동일 합니다. 웹 컨트롤을 DataList s `EditItemTemplate`에 추가 하 여 시작 합니다. 데이터 바인딩 구문을 사용 하 여 해당 하는 데이터 필드 값을 적절 한 웹 컨트롤 속성에 할당 합니다. 그리고 `UpdateCommand` 이벤트 처리기에서 웹 컨트롤과 적절 한 속성에 프로그래밍 방식으로 액세스 하 여 해당 값을 BLL에 전달 합니다.

편집 인터페이스를 만들 때 텍스트 상자와 다른 웹 컨트롤의 컬렉션으로 구성 되어 있는지 여부에 관계 없이 데이터베이스 `NULL` 값을 올바르게 처리 해야 합니다. `NULL` s를 사용 하는 경우 편집 인터페이스에서 기존 `NULL` 값을 올바르게 표시 하는 것이 아니라 값을 `NULL`으로 표시 하는 수단을 제공 해야 합니다. DataLists에 있는 Dropdownlist의 경우 일반적으로 `Value` 속성이 명시적으로 빈 문자열 (`Value=""`)로 설정 되 고 `UpdateCommand` 이벤트 처리기에 비트 코드를 추가 하 여 `NULL``ListItem` 선택 되었는지 여부를 확인 하는 정적 `ListItem`를 추가 합니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서에 대 한 잠재 고객 검토자는 Dennis Patterson이, David Suru 및 Randy Schmidt 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](adding-validation-controls-to-the-datalist-s-editing-interface-vb.md)
