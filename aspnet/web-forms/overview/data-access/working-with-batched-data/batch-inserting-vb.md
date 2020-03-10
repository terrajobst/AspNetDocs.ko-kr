---
uid: web-forms/overview/data-access/working-with-batched-data/batch-inserting-vb
title: 일괄 삽입 (VB) | Microsoft Docs
author: rick-anderson
description: 단일 작업에서 여러 데이터베이스 레코드를 삽입 하는 방법에 대해 알아봅니다. 사용자 인터페이스 계층에서 GridView를 확장 하 여 사용자가 여러 n ...을 입력할 수 있도록 합니다.
ms.author: riande
ms.date: 06/26/2007
ms.assetid: 48e2a4ae-77ca-4208-a204-c38c690ffb59
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/batch-inserting-vb
msc.type: authoredcontent
ms.openlocfilehash: 413a0e209b1899414eaab70aff07ee0d3223f28f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78501491"
---
# <a name="batch-inserting-vb"></a>일괄 삽입(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_66_VB.zip) 또는 [PDF 다운로드](batch-inserting-vb/_static/datatutorial66vb1.pdf)

> 단일 작업에서 여러 데이터베이스 레코드를 삽입 하는 방법에 대해 알아봅니다. 사용자 인터페이스 계층에서 GridView를 확장 하 여 사용자가 여러 개의 새 레코드를 입력할 수 있도록 합니다. 데이터 액세스 계층에서는 모든 삽입 작업이 성공 하거나 모든 삽입이 롤백될 수 있도록 트랜잭션 내에서 여러 삽입 작업을 래핑합니다.

## <a name="introduction"></a>소개

[일괄 업데이트](batch-updating-vb.md) 자습서에서 GridView 컨트롤을 사용자 지정 하 여 여러 레코드를 편집할 수 있는 인터페이스를 제공 하는 방법을 살펴보았습니다. 페이지를 방문 하는 사용자는 일련의 변경 작업을 수행한 다음 한 번의 클릭으로 일괄 처리 업데이트를 수행할 수 있습니다. 사용자가 일반적으로 한 번에 많은 레코드를 업데이트 하는 경우 이러한 인터페이스를 통해 [데이터 삽입, 업데이트 및 삭제 자습서의 개요](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md) 에서 처음으로 다시 탐색 된 기본 행 단위 편집 기능에 비해 수많은 클릭 및 키보드-마우스 컨텍스트 스위치를 절약할 수 있습니다.

이 개념은 레코드를 추가 하는 경우에도 적용 될 수 있습니다. 여기서는 Northwind Traders에서 특정 범주에 대 한 여러 제품이 포함 된 공급 업체의 상품을 받습니다. 예를 들어 서울 Traders에서 6 개의 다른 tea 및 커피 제품을 받을 수 있습니다. 사용자가 DetailsView 컨트롤을 통해 한 번에 6 개 제품을 입력 하는 경우에는 동일한 값을 여러 개 선택 해야 합니다. 즉, 동일한 범주 (음료), 동일한 공급 업체 (도쿄 Traders), 동일한 지원 되지 않는 값 ( False) 및 순서 값 (0)에 동일한 단위가 있습니다. 반복 되는 데이터 항목은 시간이 많이 걸리고 오류가 발생 하기 쉽습니다.

약간의 작업을 통해 사용자가 공급자 및 범주를 한 번 선택 하 고 일련의 제품 이름 및 단가를 입력 한 다음 단추를 클릭 하 여 데이터베이스에 새 제품을 추가할 수 있는 일괄 처리 삽입 인터페이스를 만들 수 있습니다 (그림 1 참조). 각 제품이 추가 되 면 `ProductName` 및 `UnitPrice` 데이터 필드에 텍스트 상자에 입력 한 값이 할당 되 고, 해당 `CategoryID` 및 `SupplierID` 값에는 폼의 맨 위에 있는 Dropdownlist의 값이 할당 됩니다. `Discontinued` 및 `UnitsOnOrder` 값은 각각 `False` 및 0의 하드 코드 된 값으로 설정 됩니다.

[일괄 삽입 인터페이스 ![](batch-inserting-vb/_static/image2.png)](batch-inserting-vb/_static/image1.png)

**그림 1**: 배치 삽입 인터페이스 ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image3.png))

이 자습서에서는 그림 1에 표시 된 배치 삽입 인터페이스를 구현 하는 페이지를 만듭니다. 이전 두 자습서와 마찬가지로 원자성을 보장 하기 위해 트랜잭션 범위 내에서 삽입을 래핑합니다. S를 시작 하겠습니다.

## <a name="step-1-creating-the-display-interface"></a>1 단계: 표시 인터페이스 만들기

이 자습서는 단일 페이지 (표시 영역 및 삽입 지역)로 구성 되어 있습니다. 이 단계에서 만들 표시 인터페이스는 GridView의 제품을 표시 하 고 제품 제품 배송 이라는 단추를 포함 합니다. 이 단추를 클릭 하면 표시 인터페이스가 그림 1에 표시 된 삽입 인터페이스로 바뀝니다. 표시 인터페이스는 배송에서 제품 추가 또는 취소 단추를 클릭 한 후에 반환 됩니다. 2 단계에서 삽입 인터페이스를 만듭니다.

두 개의 인터페이스를 포함 하는 페이지를 만들 때 한 번에 하나만 표시 되는 경우, 일반적으로 각 인터페이스는 다른 컨트롤의 컨테이너 역할을 하는 [Panel 웹 컨트롤](http://www.w3schools.com/aspnet/control_panel.asp)내에 배치 됩니다. 따라서 페이지에는 각 인터페이스 마다 하나씩 두 개의 Panel 컨트롤이 있습니다.

먼저 `BatchData` 폴더에서 `BatchInsert.aspx` 페이지를 열고 도구 상자에서 디자이너로 패널을 끌어 옵니다 (그림 2 참조). 패널 s `ID` 속성을 `DisplayInterface`로 설정 합니다. 패널을 디자이너에 추가 하면 해당 `Height` 및 `Width` 속성이 각각 50px 및 125px로 설정 됩니다. 속성 창에서 이러한 속성 값을 지우십시오.

[도구 상자에서 디자이너로 패널을 끌어 ![](batch-inserting-vb/_static/image5.png)](batch-inserting-vb/_static/image4.png)

**그림 2**: 도구 상자에서 디자이너로 패널 끌기 ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image6.png))

그런 다음 단추와 GridView 컨트롤을 패널로 끌어 옵니다. 단추 s `ID` 속성을 `ProcessShipment`로 설정 하 고 해당 `Text` 속성을 제품 배송을 처리 하도록 설정 합니다. GridView s `ID` 속성을 `ProductsGrid`로 설정 하 고 스마트 태그에서 `ProductsDataSource`라는 새 ObjectDataSource에 바인딩합니다. `ProductsBLL` 클래스 s `GetProducts` 메서드에서 데이터를 가져오도록 ObjectDataSource를 구성 합니다. 이 GridView는 데이터를 표시 하는 데만 사용 되므로 업데이트, 삽입 및 삭제 탭의 드롭다운 목록을 (없음)으로 설정 합니다. 마침을 클릭 하 여 데이터 원본 구성 마법사를 완료 합니다.

[ProductsBLL 클래스 s GetProducts 메서드에서 반환 된 데이터를 표시 ![](batch-inserting-vb/_static/image8.png)](batch-inserting-vb/_static/image7.png)

**그림 3**: `ProductsBLL` 클래스 s `GetProducts` 메서드에서 반환 된 데이터 표시 ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image9.png))

[업데이트, 삽입 및 삭제 탭의 드롭다운 목록을 (없음)으로 설정 ![](batch-inserting-vb/_static/image11.png)](batch-inserting-vb/_static/image10.png)

**그림 4**: 업데이트, 삽입 및 삭제 탭의 드롭다운 목록을 (없음)로 설정 ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image12.png))

ObjectDataSource 마법사를 완료 한 후에는 Visual Studio에서 product 데이터 필드에 대 한 BoundFields 및 CheckBoxField를 추가 합니다. `ProductName`, `CategoryName`, `SupplierName`, `UnitPrice`및 `Discontinued` 필드를 제외한 모든 필드를 제거 합니다. 미적 사용자 지정을 자유롭게 수행할 수 있습니다. `UnitPrice` 필드를 통화 값으로 지정 하 고, 필드를 다시 정렬 하 고, 여러 필드 `HeaderText` 값으로 이름을 지정 했습니다. 또한 GridView의 스마트 태그에서 페이징 사용 및 정렬 사용 확인란을 선택 하 여 페이징 및 정렬 지원을 포함 하도록 GridView를 구성 합니다.

Panel, Button, GridView 및 ObjectDataSource 컨트롤을 추가 하 고 GridView 필드를 사용자 지정 하 고 나면 페이지의 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](batch-inserting-vb/samples/sample1.aspx)]

단추 및 GridView의 태그는 여는 태그와 닫는 `<asp:Panel>` 태그 안에 표시 됩니다. 이러한 컨트롤은 `DisplayInterface` Panel 안에 있으므로 패널의 `Visible` 속성을 `False`으로 설정 하 여 숨길 수 있습니다. 3 단계에서는 단추 클릭에 대 한 응답으로 패널의 `Visible` 속성을 프로그래밍 방식으로 변경 하는 것을 확인 하 고 다른 인터페이스를 숨깁니다.

잠시 시간을 내 서 브라우저를 통해 진행 상황을 확인 하세요. 그림 5에 표시 된 것 처럼 한 번에 10 개의 제품을 나열 하는 GridView 위에 프로세스 제품 배송 단추가 표시 됩니다.

[![GridView가 제품을 나열 하 고 정렬 및 페이징 기능을 제공 합니다.](batch-inserting-vb/_static/image14.png)](batch-inserting-vb/_static/image13.png)

**그림 5**: GridView는 제품을 나열 하 고 정렬 및 페이징 기능을 제공 합니다 ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image15.png)).

## <a name="step-2-creating-the-inserting-interface"></a>2 단계: 삽입 인터페이스 만들기

표시 인터페이스가 완료 되 면 삽입 인터페이스를 만들 준비가 된 것입니다. 이 자습서에서는 단일 공급자 및 범주 값을 요청 하는 삽입 인터페이스를 만든 다음 사용자가 최대 5 개의 제품 이름 및 단가 값을 입력할 수 있도록 합니다. 이 인터페이스를 사용 하면 사용자는 모두 동일한 범주와 공급 업체를 공유 하지만 고유한 제품 이름 및 가격을 가진 새 제품을 5 개까지 추가할 수 있습니다.

먼저 도구 상자에서 디자이너로 패널을 끌어 기존 `DisplayInterface` 패널 아래에 배치 합니다. 새로 추가 된 패널의 `ID` 속성을 `InsertingInterface` 설정 하 고 `Visible` 속성을 `False`로 설정 합니다. 3 단계에서 `InsertingInterface` Panel s `Visible` 속성을 `True`로 설정 하는 코드를 추가 합니다. 또한 패널 s `Height`를 지우고 속성 값을 `Width` 합니다.

다음으로 그림 1에 표시 된 삽입 인터페이스를 만들어야 합니다. 이 인터페이스는 다양 한 HTML 기술을 통해 만들 수 있지만 매우 간단한 4 열 7 행 테이블을 사용 합니다.

> [!NOTE]
> HTML `<table>` 요소에 대 한 태그를 입력 하는 경우 소스 뷰를 사용 하는 것이 좋습니다. Visual Studio에는 디자이너를 통해 `<table>` 요소를 추가 하는 도구가 있지만 디자이너에서 `style` 설정에 대 한 요청을 너무 많이 태그에 삽입할 수 없습니다. `<table>` 태그를 만들면 일반적으로 디자이너로 돌아가 웹 컨트롤을 추가 하 고 해당 속성을 설정 합니다. 미리 결정 된 열 및 행이 있는 테이블을 만들 때 테이블 웹 컨트롤에 배치 된 웹 컨트롤은 `FindControl("controlID")` 패턴을 사용 해야만 액세스할 수 있으므로 [테이블 웹 컨트롤이](https://msdn.microsoft.com/library/system.web.ui.webcontrols.table.aspx) 아닌 정적 HTML을 사용 하는 것이 좋습니다. 그러나 테이블 웹 컨트롤을 프로그래밍 방식으로 생성할 수 있으므로 동적으로 크기가 지정 된 테이블 (행 또는 열이 일부 데이터베이스 또는 사용자 지정 조건에 따라 달라 지는 테이블)에 대해 테이블 웹 컨트롤을 사용 합니다.

`InsertingInterface` 패널의 `<asp:Panel>` 태그 안에 다음 태그를 입력 합니다.

[!code-html[Main](batch-inserting-vb/samples/sample2.html)]

이 `<table>` 태그에는 웹 컨트롤이 아직 포함 되어 있지 않습니다. 잠시 후 추가 하겠습니다. 각 `<tr>` 요소에는 공급자 및 범주 Dropdownlist이 이동할 머리글 행에 대 한 `BatchInsertHeaderRow` 특정 CSS 클래스 설정이 포함 되어 있습니다. 배송 및 취소에서 제품 추가 단추가 이동할 바닥글 행에 대 한 `BatchInsertFooterRow`입니다. 및는 제품 및 단가 TextBox 컨트롤을 포함 하는 행의 `BatchInsertRow` 및 `BatchInsertAlternatingRow` 값을 교대로 반복 합니다. 이러한 자습서에서 사용한 GridView 및 DetailsView 컨트롤과 비슷한 모양의 삽입 인터페이스를 제공 하기 위해 `Styles.css` 파일에 해당 CSS 클래스를 만들었습니다. 이러한 CSS 클래스는 다음과 같습니다.

[!code-css[Main](batch-inserting-vb/samples/sample3.css)]

이 태그를 입력 하면 디자인 뷰으로 돌아갑니다. 이 `<table>`는 그림 6에 나와 있는 것 처럼 디자이너에서 4 열, 7 행 테이블로 표시 되어야 합니다.

[삽입 인터페이스는 네 개의 열로 구성 된 7 행 테이블로 구성 됩니다 ![](batch-inserting-vb/_static/image17.png)](batch-inserting-vb/_static/image16.png)

**그림 6**: 삽입 인터페이스는 네 개의 열로 구성 된 7 행 테이블로 구성 됩니다 ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image18.png)).

이제 웹 컨트롤을 삽입 인터페이스에 추가할 준비가 되었습니다. 도구 상자의 두 Dropdownlist을 공급자에 대 한 테이블의 적절 한 셀 또는 범주에 대해 하나씩 끕니다.

공급자 DropDownList s `ID` 속성을 `Suppliers`로 설정 하 고 `SuppliersDataSource`라는 새 ObjectDataSource에 바인딩합니다. 새 ObjectDataSource를 구성 하 여 `SuppliersBLL` 클래스 s `GetSuppliers` 메서드에서 데이터를 검색 하 고 업데이트 탭의 드롭다운 목록을 (없음)으로 설정 합니다. 마침을 클릭하여 마법사를 완료합니다.

[SuppliersBLL 클래스 s GetSuppliers 메서드를 사용 하도록 ObjectDataSource 구성 ![](batch-inserting-vb/_static/image20.png)](batch-inserting-vb/_static/image19.png)

**그림 7**: `SuppliersBLL` 클래스 s `GetSuppliers` 메서드를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image21.png))

`Suppliers` DropDownList에 `CompanyName` 데이터 필드를 표시 하 고 `SupplierID` 데이터 필드를 `ListItem` 값으로 사용 하도록 합니다.

[CompanyName 데이터 필드를 표시 하 고 공급 업체를 값으로 사용 ![](batch-inserting-vb/_static/image23.png)](batch-inserting-vb/_static/image22.png)

**그림 8**: `CompanyName` 데이터 필드를 표시 하 고 `SupplierID` 값으로 사용 ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image24.png))

두 번째 DropDownList `Categories`의 이름을 지정 하 고 `CategoriesDataSource`라는 새 ObjectDataSource에 바인딩합니다. `CategoriesDataSource` ObjectDataSource를 구성 하 여 `CategoriesBLL` 클래스 s `GetCategories` 메서드를 사용 합니다. 업데이트 및 삭제 탭의 드롭다운 목록을 (없음)로 설정 하 고 마침을 클릭 하 여 마법사를 완료 합니다. 마지막으로 DropDownList에 `CategoryName` 데이터 필드를 표시 하 고 `CategoryID` 값으로 사용 하도록 합니다.

이러한 두 Dropdownlist를 추가 하 고 적절 하 게 구성 된 ObjectDataSources 원본에 바인딩한 후 화면은 그림 9와 유사 하 게 표시 됩니다.

[![머리글 행에 공급자 및 범주 Dropdownlist 포함 됩니다.](batch-inserting-vb/_static/image26.png)](batch-inserting-vb/_static/image25.png)

**그림 9**: 머리글 행에 `Suppliers` 및 `Categories` dropdownlist 포함 ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image27.png))

이제 각 새 제품의 이름과 가격을 수집 하는 텍스트 상자를 만들어야 합니다. 도구 상자의 TextBox 컨트롤을 5 개의 제품 이름 및 가격 행 각각에 대 한 디자이너로 끌어 옵니다. 텍스트 상자의 `ID` 속성을 `ProductName1`, `UnitPrice1`, `ProductName2`, `UnitPrice2`, `ProductName3`, `UnitPrice3`등으로 설정 합니다.

각 unit price 텍스트 상자에 CompareValidator를 추가 하 고 `ControlToValidate` 속성을 적절 한 `ID`로 설정 합니다. 또한 `Operator` 속성을 `GreaterThanEqual`, `ValueToCompare` 0, `Type` `Currency`로 설정 합니다. 이러한 설정은 입력 한 경우 가격이 0 보다 크거나 같은 유효한 통화 값이 되도록 CompareValidator에 지시 합니다. `Text` 속성을 \*로 설정 하 고 가격에 대 한 `ErrorMessage` 0 보다 크거나 같아야 합니다. 또한 통화 기호를 생략 하세요.

> [!NOTE]
> `Products` 데이터베이스 테이블의 `ProductName` 필드에서 `NULL` 값을 허용 하지 않더라도 삽입 인터페이스에는 RequiredFieldValidator 컨트롤이 포함 되지 않습니다. 사용자가 최대 5 개의 제품을 입력 하도록 하려고 하기 때문입니다. 예를 들어, 사용자가 처음 3 개 행에 대 한 제품 이름 및 단가를 제공 하 여 마지막 두 행을 비워 둔 경우에는 시스템에 세 개의 새 제품만 추가 하면 됩니다. 그러나 `ProductName` 필요 하므로, 해당 제품 이름 값이 제공 되는 단가가 입력 되었는지 확인 하려면 프로그래밍 방식으로 확인 해야 합니다. 4 단계에서이 검사를 살펴보겠습니다.

사용자 입력의 유효성을 검사할 때 값에 통화 기호가 포함 되어 있으면 CompareValidator에서 잘못 된 데이터를 보고 합니다. 가격을 입력할 때 통화 기호를 생략 하도록 사용자에 게 지시 하는 시각적 신호를 제공 하기 위해 각 단가 텍스트 상자의 앞에 $를 추가 합니다.

마지막으로 `InsertingInterface` 패널에 ValidationSummary 컨트롤을 추가 하 고, `ShowMessageBox` 속성을 `True`로 설정 하 고, 해당 `ShowSummary` 속성을 `False`로 설정 합니다. 이러한 설정을 사용 하는 경우 사용자가 잘못 된 단위 가격 값을 입력 하면 잘못 된 텍스트 상자 컨트롤 옆에 별표가 표시 되 고 ValidationSummary는 앞에서 지정한 오류 메시지를 표시 하는 클라이언트 쪽 messagebox를 표시 합니다.

이 시점에서 화면은 그림 10과 유사 하 게 표시 됩니다.

[현재 삽입 인터페이스 ![제품 이름 및 가격에 대 한 텍스트 상자가 포함 되어 있습니다.](batch-inserting-vb/_static/image29.png)](batch-inserting-vb/_static/image28.png)

**그림 10**: 이제 제품 이름 및 가격에 대 한 텍스트 상자가 삽입 인터페이스에 포함 됩니다 ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image30.png)).

다음에는 배송에서 제품 추가 및 취소 단추를 바닥글 행에 추가 해야 합니다. 도구 상자에서 두 단추 컨트롤을 삽입 인터페이스의 바닥글로 끌고, 단추 `ID` 속성을 `AddProducts`로 설정 하 고, `CancelButton` 및 `Text` 속성을 설정 하 여 제품을 배송 및 취소 각각에 추가 합니다. 또한 `CancelButton` 컨트롤 s `CausesValidation` 속성을 `false`로 설정 합니다.

마지막으로 두 인터페이스에 대 한 상태 메시지를 표시 하는 Label 웹 컨트롤을 추가 해야 합니다. 예를 들어 사용자가 제품의 새 배송을 성공적으로 추가한 경우 표시 인터페이스로 돌아가 확인 메시지를 표시 하려고 합니다. 그러나 사용자가 새 제품에 대 한 가격을 제공 하지만 제품 이름을 벗어나면 `ProductName` 필드가 필요 하므로 경고 메시지를 표시 해야 합니다. 이 메시지는 두 인터페이스에 대해 모두 표시 해야 하므로 패널 외부의 페이지 맨 위에 놓습니다.

레이블 웹 컨트롤을 도구 상자에서 디자이너의 페이지 맨 위로 끌어 옵니다. `ID` 속성을 `StatusLabel`로 설정 하 고 `Text` 속성을 지운 다음 `Visible` 및 `EnableViewState` 속성을 `False`로 설정 합니다. 이전 자습서에서 살펴본 것 처럼 `EnableViewState` 속성을 `False`로 설정 하면 레이블 속성 값을 프로그래밍 방식으로 변경 하 고 이후에 다시 게시할 때 기본값으로 다시 되돌릴 수 있습니다. 이렇게 하면 이후에 다시 게시할 때 사라지는 일부 사용자 작업에 응답 하 여 상태 메시지를 표시 하는 코드를 간소화할 수 있습니다. 마지막으로 `StatusLabel` 컨트롤 s `CssClass` 속성을 경고로 설정 합니다 .이는 `Styles.css`에 정의 된 CSS 클래스의 이름으로, 텍스트를 굵게 표시 합니다.

그림 11에서는 레이블이 추가 및 구성 된 후의 Visual Studio 디자이너를 보여 줍니다.

[![두 Panel 컨트롤 위에 StatusLabel 컨트롤을 추가 합니다.](batch-inserting-vb/_static/image32.png)](batch-inserting-vb/_static/image31.png)

**그림 11**: 두 Panel 컨트롤 위에 `StatusLabel` 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image33.png))

## <a name="step-3-switching-between-the-display-and-inserting-interfaces"></a>3 단계: 표시와 인터페이스 삽입 간 전환

이 시점에서 표시 및 삽입 인터페이스에 대 한 태그를 완성 했지만 다음 두 가지 작업을 계속 진행 합니다.

- 표시와 인터페이스 삽입 간 전환
- 배송 중인 제품을 데이터베이스에 추가

현재 표시 인터페이스가 표시 되지만 삽입 인터페이스는 숨겨집니다. 이는 `DisplayInterface` 패널 s `Visible` 속성이 `True` (기본값)로 설정 되어 있고 `InsertingInterface` 패널의 `Visible` 속성이 `False`로 설정 되어 있기 때문입니다. 두 인터페이스 간을 전환 하려면 각 컨트롤의 `Visible` 속성 값을 설정/해제 하기만 하면 됩니다.

제품 배송 처리 단추를 클릭할 때 표시 인터페이스에서 삽입 인터페이스로 이동 하려고 합니다. 따라서 다음 코드를 포함 하는이 단추 `Click` 이벤트에 대 한 이벤트 처리기를 만듭니다.

[!code-vb[Main](batch-inserting-vb/samples/sample4.vb)]

이 코드는 `DisplayInterface` 패널을 숨기고 `InsertingInterface` 패널을 표시 합니다.

다음으로 삽입 인터페이스의 배송 및 취소 단추 컨트롤에서 제품 추가에 대 한 이벤트 처리기를 만듭니다. 이러한 단추 중 하나를 클릭 하면 표시 인터페이스로 되돌려야 합니다. 일시적으로 추가 하는 메서드인 `ReturnToDisplayInterface`를 호출 하도록 두 단추 컨트롤에 대 한 `Click` 이벤트 처리기를 만듭니다. `InsertingInterface` 패널을 숨기고 `DisplayInterface` 패널을 표시 하는 것 외에도 `ReturnToDisplayInterface` 메서드는 웹 컨트롤을 편집 전 상태로 반환 해야 합니다. 여기에는 Dropdownlist `SelectedIndex` 속성을 0으로 설정 하 고 TextBox 컨트롤의 `Text` 속성을 지우는 작업이 포함 됩니다.

> [!NOTE]
> 표시 인터페이스를 반환 하기 전에 컨트롤을 미리 편집 상태로 반환 하지 않은 경우 발생할 수 있는 상황을 고려 합니다. 사용자가 제품 배송 처리 단추를 클릭 하 고 배송에서 제품을 입력 한 다음 배송에서 제품 추가를 클릭 합니다. 제품을 추가 하 고 사용자를 표시 인터페이스에 반환 합니다. 이 시점에서 사용자가 다른 배송을 추가 하려고 할 수 있습니다. 제품 배송 처리 단추를 클릭 하면 삽입 인터페이스를 반환 하지만 DropDownList 선택 및 텍스트 상자 값은 여전히 이전 값으로 채워집니다.

[!code-vb[Main](batch-inserting-vb/samples/sample5.vb)]

`Click` 이벤트 처리기는 모두 `ReturnToDisplayInterface` 메서드를 호출 하지만 4 단계에서 배송에서 제품 추가 `Click` 이벤트 처리기로 돌아가서 제품을 저장 하는 코드를 추가 합니다. `ReturnToDisplayInterface` `Suppliers`를 반환 하 고 첫 번째 옵션에 Dropdownlist을 `Categories` 합니다. 두 상수 `lastControlID` `firstControlID`는 삽입 인터페이스에서 제품 이름 및 단가 텍스트 상자의 이름을 지정 하는 데 사용 되는 시작 및 종료 컨트롤 인덱스 값을 표시 하 고, 텍스트 상자 컨트롤의 `Text` 속성을 다시 빈 문자열로 설정 하는 `For` 루프의 범위에 사용 됩니다. 마지막으로, 삽입 인터페이스가 숨겨지고 표시 인터페이스가 표시 되도록 패널 `Visible` 속성이 다시 설정 됩니다.

잠시 시간을 들 여 브라우저에서이 페이지를 테스트해 보세요. 페이지를 처음 방문할 때 그림 5에 표시 된 것 처럼 표시 인터페이스가 표시 되어야 합니다. 제품 배송 처리 단추를 클릭 합니다. 그러면이 페이지가 다시 게시 되 고 그림 12와 같이 삽입 인터페이스가 표시 됩니다. 배송에서 제품 추가 또는 취소 단추를 클릭 하면 표시 인터페이스로 돌아갑니다.

> [!NOTE]
> 삽입 인터페이스를 보는 동안 단위 가격 텍스트 상자에서 CompareValidators 검사기를 테스트 합니다. 지정 된 통화 값 또는 값이 0 보다 작은 가격이 포함 된 배송에서 제품 추가 단추를 클릭 하면 클라이언트 쪽 messagebox 경고가 표시 됩니다.

[제품 배송 단추를 클릭 한 후 삽입 인터페이스를 표시 ![](batch-inserting-vb/_static/image35.png)](batch-inserting-vb/_static/image34.png)

**그림 12**: 제품 배송 처리 단추를 클릭 한 후 삽입 인터페이스 표시 ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image36.png))

## <a name="step-4-adding-the-products"></a>4 단계: 제품 추가

이 자습서에 대 한 모든 것은 제품을 배송에서 제품 추가 단추 `Click` 이벤트 처리기에 데이터베이스에 저장 하는 것입니다. 이렇게 하려면 `ProductsDataTable`를 만들고 제공 된 각 제품 이름에 대 한 `ProductsRow` 인스턴스를 추가 합니다. 이러한 `ProductsRow` s를 추가 하면 `ProductsDataTable`를 전달 하는 `ProductsBLL` 클래스 `UpdateWithTransaction` 메서드를 호출 하 게 됩니다. [트랜잭션 자습서에서 데이터베이스 수정 내용 래핑](wrapping-database-modifications-within-a-transaction-vb.md) 에서 다시 만들어진 `UpdateWithTransaction` 메서드는 `ProductsDataTable`를 `ProductsTableAdapter`의 `UpdateWithTransaction` 메서드로 전달 합니다. 여기에서 ADO.NET 트랜잭션이 시작 되 고 TableAdapter는 DataTable에 추가 된 각 `ProductsRow`에 대 한 `INSERT` 문을 데이터베이스에 발급 합니다. 모든 제품이 오류 없이 추가 되었다고 가정 하면 트랜잭션이 커밋되고 그렇지 않으면 롤백됩니다.

배송에서 제품 추가 단추 `Click` 이벤트 처리기에 대 한 코드는 약간의 오류 검사를 수행 해야 합니다. 삽입 인터페이스에는 RequiredFieldValidators 검사기가 사용 되지 않으므로 사용자는 이름을 생략 하는 동안 제품에 대 한 가격을 입력할 수 있습니다. 제품 이름이 필요 하므로 이러한 조건이 충족 되는 경우 사용자에 게 경고를 펼칩니다 삽입을 진행 하지 않아도 됩니다. 전체 `Click` 이벤트 처리기 코드는 다음과 같습니다.

[!code-vb[Main](batch-inserting-vb/samples/sample6.vb)]

이벤트 처리기는 `Page.IsValid` 속성이 `True`값을 반환 하는지 확인 하 여 시작 합니다. `False`반환 하는 경우 하나 이상의 CompareValidators 검사기가 잘못 된 데이터를 보고 하 고 있음을 의미 합니다. 이 경우 입력 한 제품을 삽입 하려고 하지 않습니다. 또는 `ProductsRow` s `UnitPrice` 속성에 사용자가 입력 한 단가 값을 할당 하려고 할 때 예외가 발생 합니다.

다음으로 새 `ProductsDataTable` 인스턴스가 생성 됩니다 (`products`). `For` 루프는 제품 이름 및 단가 텍스트 상자를 반복 하는 데 사용 되 고 `Text` 속성은 지역 변수 `productName` 및 `unitPrice`읽습니다. 사용자가 단가에 대 한 값을 입력 했지만 해당 제품 이름에 대 한 값을 입력 하지 않은 경우에는 사용자가 단가를 제공 하는 경우 해당 제품의 이름도 포함 하 고 이벤트 처리기가 종료 되는 경우에도 `StatusLabel` 메시지를 표시 합니다.

제품 이름이 제공 된 경우 `ProductsDataTable` s `NewProductsRow` 메서드를 사용 하 여 새 `ProductsRow` 인스턴스를 만듭니다. 이 새로운 `ProductsRow` instance s `ProductName` 속성은 `SupplierID` 및 `CategoryID` 속성이 삽입 인터페이스 헤더에 있는 Dropdownlist의 `SelectedValue` 속성에 할당 되는 동안 현재 product name TextBox로 설정 됩니다. 사용자가 제품 가격에 대 한 값을 입력 한 경우 `ProductsRow` 인스턴스 `UnitPrice` 속성에 할당 됩니다. 그렇지 않으면 속성은 할당 되지 않은 상태로 유지 되며이로 인해 데이터베이스의 `UnitPrice`에 대 한 `NULL` 값이 할당 됩니다. 마지막으로 `Discontinued` 및 `UnitsOnOrder` 속성은 각각 하드 코딩 된 값 `False` 및 0에 할당 됩니다.

속성이 `ProductsRow` 인스턴스에 할당 된 후에는 `ProductsDataTable`에 추가 됩니다.

`For` 루프가 완료 되 면 제품이 추가 되었는지 여부를 확인 합니다. 모든 제품 이름 또는 가격을 입력 하기 전에 사용자가 배송에서 제품 추가를 클릭 했을 수 있습니다. `ProductsDataTable`에 제품이 하나 이상 있으면 `ProductsBLL` 클래스 s `UpdateWithTransaction` 메서드가 호출 됩니다. 그런 다음 새로 추가 된 제품이 표시 인터페이스에 표시 되도록 데이터를 `ProductsGrid` GridView에 다시 바인딩 합니다. `StatusLabel`는 확인 메시지를 표시 하 고 `ReturnToDisplayInterface`를 호출 하 여 삽입 인터페이스를 숨기고 표시 인터페이스를 표시 하도록 업데이트 됩니다.

제품을 입력 하지 않은 경우 삽입 인터페이스는 계속 표시 되지만 제품이 추가 되지 않았습니다. 메시지가 표시 됩니다. 텍스트 상자에 제품 이름 및 단가를 입력 하십시오.

그림 s 13, 14 및 15는 작동 중인 삽입 및 표시 인터페이스를 보여 줍니다. 그림 13에서 사용자는 해당 제품 이름 없이 단가 값을 입력 했습니다. 그림 14에서는 새 제품 3 개가 성공적으로 추가 된 후 표시 인터페이스를 보여 줍니다. 그림 15는 GridView에 새로 추가 된 두 개의 제품을 보여 줍니다 (셋째 페이지는 이전 페이지에 있습니다).

[단가를 입력할 때 제품 이름이 필요 ![](batch-inserting-vb/_static/image38.png)](batch-inserting-vb/_static/image37.png)

**그림 13**: 단가를 입력할 때 제품 이름이 필요 함 ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image39.png))

[공급자 Mayumi s에 대해 3 개의 New Veggies가 추가 ![](batch-inserting-vb/_static/image41.png)](batch-inserting-vb/_static/image40.png)

**그림 14**: 공급자 Mayumi s에 대해 3 개의 새 Veggies 추가 되었습니다 ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image42.png)).

[새 제품 ![GridView의 마지막 페이지에서 찾을 수 있습니다.](batch-inserting-vb/_static/image44.png)](batch-inserting-vb/_static/image43.png)

**그림 15**: 새 제품을 GridView의 마지막 페이지에서 찾을 수 있습니다 ([전체 크기 이미지를 보려면 클릭](batch-inserting-vb/_static/image45.png)).

> [!NOTE]
> 이 자습서에서 사용 되는 일괄 처리 삽입 논리는 트랜잭션 범위 내에서 삽입을 래핑합니다. 이를 확인 하기 위해 의도적으로 데이터베이스 수준 오류를 도입 합니다. 예를 들어 `Categories` DropDownList에서 선택한 값에 새 `ProductsRow` 인스턴스 s `CategoryID` 속성을 할당 하는 대신 `i * 5`같은 값에 할당 합니다. 여기서 `i`은 루프 인덱서 이며 1에서 5 사이의 값을 갖습니다. 따라서 일괄 삽입에서 두 개 이상의 제품을 추가 하는 경우 첫 번째 제품은 유효한 `CategoryID` 값 (5)을 갖지만 이후 제품에는 `Categories` 테이블의 `CategoryID` 값과 일치 하지 않는 `CategoryID` 값이 포함 됩니다. 결과적으로 첫 번째 `INSERT` 성공 하지만 후속 작업이 실패 하 고 foreign key 제약 조건 위반이 발생 합니다. 일괄 처리 삽입은 원자성 이므로 첫 번째 `INSERT` 롤백되고 일괄 처리 삽입 프로세스가 시작 되기 전의 상태로 데이터베이스를 되돌립니다.

## <a name="summary"></a>요약

이 기사와 이전 두 자습서에서는 데이터 일괄 처리를 업데이트, 삭제 및 삽입할 수 있는 인터페이스를 만들었습니다. 이러한 인터페이스를 사용 하면 [트랜잭션 자습서 내](wrapping-database-modifications-within-a-transaction-vb.md) 에서 데이터 액세스 계층에 추가한 트랜잭션 지원도 모두 사용 됩니다. 특정 시나리오에서 이러한 일괄 처리 사용자 인터페이스는 클릭, 다시 게시 및 키보드 간 컨텍스트 전환 횟수를 낮추고 기본 데이터의 무결성을 유지 하 여 최종 사용자 효율성을 크게 향상 시킵니다.

이 자습서에서는 일괄 처리 된 데이터로 작업 하는 방법에 대해 살펴봅니다. 다음 자습서 집합에서는 TableAdapter의 메서드에서 저장 프로시저를 사용 하 고, DAL에서 연결 및 명령 수준 설정을 구성 하 고, 연결 문자열을 암호화 하는 등의 다양 한 고급 데이터 액세스 계층 시나리오를 살펴봅니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Hilton Gid Esenow 및 S ren Jacob Lauritsen 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](batch-deleting-vb.md)
