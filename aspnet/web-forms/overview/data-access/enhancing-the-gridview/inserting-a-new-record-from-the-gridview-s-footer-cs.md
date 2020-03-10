---
uid: web-forms/overview/data-access/enhancing-the-gridview/inserting-a-new-record-from-the-gridview-s-footer-cs
title: GridView의 바닥글에서 새 레코드 삽입 (C#) | Microsoft Docs
author: rick-anderson
description: GridView 컨트롤은 데이터의 새 레코드 삽입에 대 한 기본 제공 지원을 제공 하지 않지만이 자습서에서는 다음을 포함 하도록 GridView를 확대 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 03/06/2007
ms.assetid: 49545652-98af-46ba-9dbc-9ab529805d9b
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/inserting-a-new-record-from-the-gridview-s-footer-cs
msc.type: authoredcontent
ms.openlocfilehash: 6b337fe395a0ed54b03767111e73ea6d6c0ba23a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78477527"
---
# <a name="inserting-a-new-record-from-the-gridviews-footer-c"></a>GridView의 바닥글에서 새 레코드 삽입(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_53_CS.exe) 또는 [PDF 다운로드](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/datatutorial53cs1.pdf)

> GridView 컨트롤이 새 데이터 레코드 삽입에 대 한 기본 제공 지원을 제공 하지 않지만이 자습서에서는 삽입 인터페이스를 포함 하도록 GridView를 확대 하는 방법을 보여 줍니다.

## <a name="introduction"></a>소개

[데이터 삽입, 업데이트 및 삭제](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) 자습서의 개요에 설명 된 대로 GridView, DetailsView 및 FormView 웹 컨트롤에는 기본적으로 제공 되는 데이터 수정 기능이 포함 되어 있습니다. 선언적 데이터 소스 컨트롤과 함께 사용 하는 경우이 세 가지 웹 컨트롤을 빠르고 쉽게 구성 하 여 코드를 한 줄도 작성할 필요 없이 시나리오에서 데이터를 수정할 수 있습니다. 아쉽게도 DetailsView 및 FormView 컨트롤만 기본 제공 되는 삽입, 편집 및 삭제 기능을 제공 합니다. GridView는 편집 및 삭제 지원만 제공 합니다. 그러나 작은 엘 보 그리스를 사용 하면 삽입 인터페이스를 포함 하도록 GridView를 확대할 수 있습니다.

GridView에 삽입 기능을 추가 하는 경우 새 레코드를 추가 하는 방법, 삽입 인터페이스를 만드는 방법 및 새 레코드를 삽입 하는 코드를 작성 하는 방법을 결정 해야 합니다. 이 자습서에서는 GridView 바닥글 행에 삽입 인터페이스를 추가 하는 방법을 살펴봅니다 (그림 1 참조). 각 열에 대 한 바닥글 셀에는 적절 한 데이터 컬렉션 사용자 인터페이스 요소 (제품 이름에 대 한 텍스트 상자, 공급자에 대 한 DropDownList 등)가 포함 됩니다. 또한 클릭 하면 다시 게시를 발생 하 고 바닥글 행에 제공 된 값을 사용 하 여 `Products` 테이블에 새 레코드를 삽입 하는 추가 단추에 대 한 열이 필요 합니다.

[바닥글 행 ![새 제품을 추가 하기 위한 인터페이스를 제공 합니다.](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image1.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image1.png)

**그림 1**: 바닥글 행이 새 제품을 추가 하기 위한 인터페이스를 제공 합니다 ([전체 크기 이미지를 보려면 클릭](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image2.png)).

## <a name="step-1-displaying-product-information-in-a-gridview"></a>1 단계: GridView에서 제품 정보 표시

GridView의 바닥글에 삽입 인터페이스를 만드는 것을 고려 하기 전에 먼저 데이터베이스의 제품을 나열 하는 페이지에 GridView를 추가 하는 데 중점을 둡니다. 먼저 `EnhancedGridView` 폴더에서 `InsertThroughFooter.aspx` 페이지를 열고 gridview를 도구 상자에서 디자이너로 끌어와 GridView s `ID` 속성을 `Products`로 설정 합니다. 그런 다음 GridView s 스마트 태그를 사용 하 여 `ProductsDataSource`라는 새 ObjectDataSource에 바인딩합니다.

[ProductsDataSource 라는 새 ObjectDataSource를 만들 ![](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image2.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image3.png)

**그림 2**: `ProductsDataSource` 라는 새 ObjectDataSource 만들기 ([전체 크기 이미지를 보려면 클릭](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image4.png))

`ProductsBLL` 클래스 s `GetProducts()` 메서드를 사용 하 여 제품 정보를 검색 하도록 ObjectDataSource를 구성 합니다. 이 자습서에서는 편집 및 삭제에 대해 걱정할 필요 없이 삽입 기능을 추가 하는 데 중점을 둡니다. 따라서 삽입 탭의 드롭다운 목록이 `AddProduct()`로 설정 되어 있고 업데이트 및 삭제 탭의 드롭다운 목록이 (없음)로 설정 되어 있는지 확인 합니다.

[AddProduct 메서드를 ObjectDataSource s Insert () 메서드에 매핑합니다 ![](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image3.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image5.png)

**그림 3**: `AddProduct` 메서드를 ObjectDataSource s `Insert()` 메서드에 매핑 ([전체 크기 이미지를 보려면 클릭](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image6.png))

[![업데이트 및 삭제 탭 드롭다운 목록을 (없음)으로 설정 합니다.](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image4.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image7.png)

**그림 4**: 업데이트 및 삭제 탭 드롭다운 목록을 (없음)로 설정 ([전체 크기 이미지를 보려면 클릭](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image8.png))

ObjectDataSource의 데이터 소스 구성 마법사를 완료 한 후 Visual Studio에서 해당 하는 각 데이터 필드에 대 한 필드를 GridView에 자동으로 추가 합니다. 지금은 Visual Studio에서 추가한 모든 필드를 그대로 둡니다. 이 자습서의 뒷부분에서는 새 레코드를 추가할 때 값을 지정 해야 하는 일부 필드를 다시 시작 하 고 제거 합니다.

데이터베이스에는 80 개 제품이 있으므로 사용자는 새 레코드를 추가 하기 위해 웹 페이지의 맨 아래로 스크롤해야 합니다. 따라서를 사용 하 여 삽입 인터페이스를 더 잘 표시 하 고 액세스할 수 있도록 합니다. 페이징을 켜려면 GridView의 스마트 태그에서 페이징 사용 확인란을 선택 하면 됩니다.

이제 GridView와 ObjectDataSource의 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample1.aspx)]

[![모든 제품 데이터 필드가 페이징된 GridView에 표시 됩니다.](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image5.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image9.png)

**그림 5**: 모든 제품 데이터 필드가 페이징된 GridView에 표시 됨 ([전체 크기 이미지를 보려면 클릭](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image10.png))

## <a name="step-2-adding-a-footer-row"></a>2 단계: 바닥글 행 추가

GridView는 머리글 및 데이터 행과 함께 바닥글 행을 포함 합니다. 머리글 및 바닥글 행은 GridView s [`ShowHeader`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.showheader.aspx) 의 값과 [`ShowFooter`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.showfooter.aspx) 속성에 따라 표시 됩니다. 바닥글 행을 표시 하려면 `ShowFooter` 속성을 `true`로 설정 하기만 하면 됩니다. 그림 6에 나와 있는 것 처럼 `ShowFooter` 속성을 `true`로 설정 하면 바닥글 행이 표에 추가 됩니다.

[바닥글 행을 표시 ![ShowFooter를 True로 설정 합니다.](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image6.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image11.png)

**그림 6**: 바닥글 행을 표시 하려면 `ShowFooter` `True`으로 설정 ([전체 크기 이미지를 보려면 클릭](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image12.png))

바닥글 행에는 짙은 빨간색 배경색이 있습니다. 이는 ObjectDataSource 자습서를 사용 하 여 [데이터를 표시](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md) 하는 모든 페이지에 다시 만들고 적용 한 DataWebControls 테마 때문입니다. 특히 `GridView.skin` 파일은에서 `FooterStyle` CSS 클래스를 사용 하는 `FooterStyle` 속성을 구성 합니다. `FooterStyle` 클래스는 `Styles.css` 다음과 같이 정의 됩니다.

[!code-css[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample2.css)]

> [!NOTE]
> 이전 자습서에서 GridView s 바닥글 행을 사용 하 여 탐색 했습니다. 필요한 경우 리프레셔에 대 한 [GridView 바닥글 자습서의 요약 정보 표시](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-cs.md) 를 다시 참조 하세요.

`ShowFooter` 속성을 `true`로 설정한 후 잠시 시간을 내 서 브라우저의 출력을 확인 합니다. 현재 바닥글 행에는 텍스트 또는 웹 컨트롤이 포함 되어 있지 않습니다. 3 단계에서는 적절 한 삽입 인터페이스가 포함 되도록 각 GridView 필드의 바닥글을 수정 합니다.

[빈 바닥글 행 ![페이징 인터페이스 컨트롤 위에 표시 됩니다.](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image7.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image13.png)

**그림 7**: 빈 바닥글 행이 페이징 인터페이스 컨트롤 위에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image14.png)).

## <a name="step-3-customizing-the-footer-row"></a>3 단계: 바닥글 행 사용자 지정

[GridView 컨트롤의 템플릿 필드 사용](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md) 자습서에서 BoundFields 또는 CheckBoxFields가 아닌 템플릿 필드를 사용 하 여 특정 GridView 열의 표시를 크게 사용자 지정 하는 방법을 살펴보았습니다. [데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md) 에서 서식 필드를 사용 하 여 GridView의 편집 인터페이스를 사용자 지정 하는 방법을 살펴보았습니다. Templatefield로 변환은 특정 형식의 행에 사용 되는 태그, 웹 컨트롤 및 데이터 바인딩 구문의 혼합을 정의 하는 여러 템플릿으로 구성 되어 있습니다. 예를 들어 `ItemTemplate`은 읽기 전용 행에 사용 되는 템플릿을 지정 하는 반면, `EditItemTemplate`은 편집 가능한 행의 템플릿을 정의 합니다.

`ItemTemplate` 및 `EditItemTemplate`와 함께 Templatefield로 변환에는 바닥글 행에 대 한 콘텐츠를 지정 하는 `FooterTemplate`도 포함 됩니다. 따라서 인터페이스를 삽입 하는 각 필드에 필요한 웹 컨트롤을 `FooterTemplate`에 추가할 수 있습니다. 시작 하려면 GridView의 모든 필드를 템플릿 필드로 변환 합니다. 이렇게 하려면 GridView의 스마트 태그에서 열 편집 링크를 클릭 하 고 왼쪽 아래 모퉁이의 각 필드를 선택한 다음이 필드를 Templatefield로 변환으로 변환 링크를 클릭 합니다.

![각 필드를 Templatefield로 변환 변환](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image8.gif)

**그림 8**: 각 필드를 templatefield로 변환 변환

이 필드를 Templatefield로 변환 변환을 클릭 하면 현재 필드 형식이 해당 Templatefield로 변환으로 변환 됩니다. 예를 들어 각 BoundField는 해당 데이터 필드를 표시 하는 레이블과 텍스트 상자에 데이터 필드를 표시 하는 `EditItemTemplate`를 포함 하는 `ItemTemplate` Templatefield로 변환로 바뀝니다. `ProductName` BoundField는 다음 Templatefield로 변환 태그로 변환 되었습니다.

[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample3.aspx)]

마찬가지로 `Discontinued` CheckBoxField는 `ItemTemplate`와 `EditItemTemplate`에 CheckBox 웹 컨트롤 (`ItemTemplate` s 확인란을 사용 하지 않도록 설정 됨)이 포함 되어 있는 Templatefield로 변환로 변환 되었습니다. 읽기 전용 `ProductID` BoundField는 `ItemTemplate` 및 `EditItemTemplate`모두에 레이블 컨트롤이 있는 Templatefield로 변환으로 변환 되었습니다. 간단히 말해서 기존 GridView 필드를 Templatefield로 변환으로 변환 하는 것은 기존 필드 기능을 잃지 않고 보다 사용자 지정 가능한 Templatefield로 변환로 전환 하는 빠르고 쉬운 방법입니다.

에서 작업을 수행 하는 GridView는 편집을 지원 하지 않으므로 각 Templatefield로 변환에서 `EditItemTemplate`를 제거 하 여 `ItemTemplate`만 남겨 보세요. 이 작업을 수행한 후 GridView의 선언 태그는 다음과 같습니다.

[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample4.aspx)]

이제 각 GridView 필드가 Templatefield로 변환로 변환 되었으므로 `FooterTemplate`각 필드에 적절 한 삽입 인터페이스를 입력할 수 있습니다. 일부 필드에는 삽입 인터페이스가 없습니다 (예를 들어`ProductID`). 다른 항목은 새 제품 정보를 수집 하는 데 사용 되는 웹 컨트롤에 따라 다릅니다.

편집 인터페이스를 만들려면 GridView의 스마트 태그에서 템플릿 편집 링크를 선택 합니다. 그런 다음 드롭다운 목록에서 적절 한 필드 `FooterTemplate`를 선택 하 고 도구 상자의 적절 한 컨트롤을 디자이너로 끌어 옵니다.

[![각 필드에 적절 한 삽입 인터페이스를 추가 합니다. FooterTemplate](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image9.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image15.png)

**그림 9**: 각 필드 `FooterTemplate`에 적절 한 삽입 인터페이스 추가 ([전체 크기 이미지를 보려면 클릭](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image16.png))

다음 글머리 기호 목록은 추가할 인터페이스를 지정 하 여 GridView 필드를 열거 합니다.

- 없음을 `ProductID` 합니다.
- `ProductName` 텍스트 상자를 추가 하 고 해당 `ID`를 `NewProductName`로 설정 합니다. 사용자가 새 제품 이름에 대 한 값을 입력할 수 있도록 RequiredFieldValidator 컨트롤을 추가 합니다.
- 없음을 `SupplierID` 합니다.
- 없음을 `CategoryID` 합니다.
- 텍스트 상자를 추가 `QuantityPerUnit` `ID`를 `NewQuantityPerUnit`로 설정 합니다.
- 입력 한 값이 0 보다 크거나 같은 통화 값 인지 확인 하는 `NewUnitPrice` 라는 텍스트 상자와 CompareValidator를 추가 `UnitPrice` 합니다.
- `ID` `NewUnitsInStock`으로 설정 된 텍스트 상자를 사용 `UnitsInStock` 합니다. 입력 한 값이 0 보다 크거나 같은 정수 값 인지 확인 하는 CompareValidator를 포함 합니다.
- `ID` `NewUnitsOnOrder`으로 설정 된 텍스트 상자를 사용 `UnitsOnOrder` 합니다. 입력 한 값이 0 보다 크거나 같은 정수 값 인지 확인 하는 CompareValidator를 포함 합니다.
- `ID` `NewReorderLevel`으로 설정 된 텍스트 상자를 사용 `ReorderLevel` 합니다. 입력 한 값이 0 보다 크거나 같은 정수 값 인지 확인 하는 CompareValidator를 포함 합니다.
- 확인란을 추가 `Discontinued` `ID`를 `NewDiscontinued`로 설정 합니다.
- `CategoryName` DropDownList을 추가 하 고 해당 `ID`를 `NewCategoryID`로 설정 합니다. `CategoriesDataSource` 새 ObjectDataSource에 바인딩하고 `CategoriesBLL` 클래스 s `GetCategories()` 메서드를 사용 하도록 구성 합니다. `CategoryID` 데이터 필드를 값으로 사용 하 여 `ListItem` s에 `CategoryName` 데이터 필드를 표시 하도록 합니다.
- `SupplierName` DropDownList을 추가 하 고 해당 `ID`를 `NewSupplierID`로 설정 합니다. `SuppliersDataSource` 새 ObjectDataSource에 바인딩하고 `SuppliersBLL` 클래스 s `GetSuppliers()` 메서드를 사용 하도록 구성 합니다. `SupplierID` 데이터 필드를 값으로 사용 하 여 `ListItem` s에 `CompanyName` 데이터 필드를 표시 하도록 합니다.

각 유효성 검사 컨트롤에 대해 `FooterStyle` CSS 클래스의 흰색 전경색이 기본값 빨강 대신 사용 되도록 `ForeColor` 속성을 지웁니다. 또한 자세한 설명에는 `ErrorMessage` 속성을 사용 하 고 `Text` 속성은 별표로 설정 합니다. 유효성 검사 컨트롤의 텍스트에서 삽입 인터페이스를 두 줄로 래핑할 수 없도록 하려면 유효성 검사 컨트롤을 사용 하는 각 `FooterTemplate`에 대해 `FooterStyle` s `Wrap` 속성을 false로 설정 합니다. 마지막으로 GridView 아래에 ValidationSummary 컨트롤을 추가 하 고 해당 `ShowMessageBox` 속성을 `true`로 설정 하 고 `ShowSummary` 속성을 `false`로 설정 합니다.

새 제품을 추가할 때 `CategoryID` 및 `SupplierID`를 제공 해야 합니다. 이 정보는 `CategoryName` 및 `SupplierName` 필드에 대 한 바닥글 셀의 Dropdownlist을 통해 캡처됩니다. `CategoryID` 및 `SupplierID` 템플릿 필드와는 달리 이러한 필드를 사용 하도록 선택 했습니다. 그리드 s 데이터 행에서 사용자는 ID 값이 아닌 범주 및 공급자 이름을 보는 데 더 관심이 있을 수 있습니다. `CategoryID` 및 `SupplierID` 값은 이제 `CategoryName` 및 `SupplierName` 필드의 삽입 인터페이스에 캡처되고 있으므로 GridView에서 `CategoryID` 및 `SupplierID` 템플릿 필드를 제거할 수 있습니다.

마찬가지로 `ProductID`는 새 제품을 추가할 때 사용 되지 않으므로 `ProductID` Templatefield로 변환 제거 될 수도 있습니다. 그러나 `ProductID` 필드를 모눈에 남겨 둡니다. 삽입 인터페이스를 구성 하는 텍스트 상자, Dropdownlist, 확인란 및 유효성 검사 컨트롤 외에도, 클릭 하면 데이터베이스에 새 제품을 추가 하는 논리를 수행 하는 추가 단추도 필요 합니다. 4 단계에서는 `ProductID` Templatefield로 변환 s `FooterTemplate`의 삽입 인터페이스에 추가 단추를 포함 합니다.

자유롭게 다양 한 GridView 필드의 모양을 개선 합니다. 예를 들어 `UnitPrice` 값의 서식을 통화로 지정 하 고, `UnitsInStock`, `UnitsOnOrder`및 `ReorderLevel` 필드를 오른쪽에 맞추고, 템플릿 필드의 `HeaderText` 값을 업데이트할 수 있습니다.

`FooterTemplate` s에 인터페이스를 삽입 하는 slew을 만들고, `SupplierID`를 제거 하 고, 템플릿 필드를 `CategoryID` 하 고, 템플릿 필드를 정렬 하 고 서식을 지정 하 여 그리드의 미관를 향상 시키고, GridView의 선언적 태그는 다음과 유사 하 게 표시 됩니다.

[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample5.aspx)]

브라우저를 통해 볼 때 GridView s 바닥글 행에는 완성 된 삽입 인터페이스가 포함 됩니다 (그림 10 참조). 이 시점에서 삽입 인터페이스에는 사용자가 새 제품에 대 한 데이터를 입력 하 고 데이터베이스에 새 레코드를 삽입 하 려 함을 나타낼 수 있는 방법이 포함 되지 않습니다. 또한 바닥글에 입력 한 데이터를 `Products` 데이터베이스의 새 레코드로 변환 하는 방법을 설명 합니다. 4 단계에서 삽입 인터페이스에 추가 단추를 포함 하는 방법 및 클릭 하면 다시 게시 시 코드를 실행 하는 방법을 살펴보겠습니다. 5 단계에서는 바닥글의 데이터를 사용 하 여 새 레코드를 삽입 하는 방법을 보여 줍니다.

[![GridView 바닥글은 새 레코드를 추가 하기 위한 인터페이스를 제공 합니다.](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image10.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image17.png)

**그림 10**: GridView 바닥글은 새 레코드를 추가 하기 위한 인터페이스를 제공 합니다 ([전체 크기 이미지를 보려면 클릭](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image18.png)).

## <a name="step-4-including-an-add-button-in-the-inserting-interface"></a>4 단계: 삽입 인터페이스에 추가 단추 포함

바닥글 행 s 삽입 인터페이스에는 현재 사용자가 새 제품 정보 입력을 완료 했음을 나타낼 수 있는 방법이 없으므로 삽입 인터페이스에 추가 단추를 포함 해야 합니다. 기존 `FooterTemplate` s 중 하나에 배치 하거나이 목적을 위해 표에 새 열을 추가할 수 있습니다. 이 자습서에서는 `ProductID` Templatefield로 변환 s `FooterTemplate`에 추가 단추를 놓습니다.

디자이너에서 GridView s 스마트 태그의 템플릿 편집 링크를 클릭 한 다음 드롭다운 목록에서 `ProductID` 필드 `FooterTemplate`를 선택 합니다. 단추 웹 컨트롤 (또는 원하는 경우 LinkButton 또는 ImageButton)을 템플릿에 설정 하 고, 해당 ID를 `AddProduct`로 설정 하 고, `CommandName` 삽입 하 고, `Text` 속성을 그림 11과 같이 추가 합니다.

[![ProductID Templatefield로 변환 s FooterTemplate에 추가 단추를 놓습니다.](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image11.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image19.png)

**그림 11**: `ProductID` templatefield로 변환 s `FooterTemplate`에 추가 단추를 놓습니다 ([전체 크기 이미지를 보려면 클릭](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image20.png)).

추가 단추를 포함 한 후에는 브라우저에서 페이지를 테스트 합니다. 삽입 인터페이스에 잘못 된 데이터가 포함 된 추가 단추를 클릭할 때 포스트백은 짧은 short-circuit이 고 ValidationSummary 컨트롤은 잘못 된 데이터를 나타냅니다 (그림 12 참조). 적절 한 데이터를 입력 하면 추가 단추를 클릭 하면 포스트백이 발생 합니다. 그러나 데이터베이스에는 레코드가 추가 되지 않습니다. 실제로 삽입을 수행 하려면 약간의 코드를 작성 해야 합니다.

[삽입 인터페이스에 잘못 된 데이터가 있는 경우 추가 단추를 다시 게시 하는 것이 짧은 Short-circuit ![](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image12.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image21.png)

**그림 12**: 삽입 인터페이스에 잘못 된 데이터가 있는 경우 추가 단추 s 포스트백은 짧은 short-circuit ([전체 크기 이미지를 보려면 클릭](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image22.png))

> [!NOTE]
> 삽입 인터페이스의 유효성 검사 컨트롤이 유효성 검사 그룹에 할당 되지 않았습니다. 이는 삽입 인터페이스가 페이지의 유일한 유효성 검사 컨트롤 집합인 경우에만 제대로 작동 합니다. 그러나 페이지에 다른 유효성 검사 컨트롤이 있는 경우 (예: 그리드 s 편집 인터페이스의 유효성 검사 컨트롤) 삽입 인터페이스 및 추가 단추 `ValidationGroup` 속성의 유효성 검사 컨트롤에는 이러한 컨트롤과 특정 유효성 검사 그룹을 연결 하기 위해 동일한 값이 할당 되어야 합니다. 페이지의 유효성 검사 컨트롤 및 단추를 유효성 검사 그룹으로 분할 하는 방법에 대 한 자세한 내용은 [ASP.NET 2.0의 유효성 검사 컨트롤 개로 나누어서을](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx) 참조 하세요.

## <a name="step-5-inserting-a-new-record-into-theproductstable"></a>5 단계:`Products`테이블에 새 레코드 삽입

Gridview의 기본 제공 편집 기능을 활용 하는 경우 GridView는 업데이트를 수행 하는 데 필요한 모든 작업을 자동으로 처리 합니다. 특히 업데이트 단추를 클릭 하면 편집 인터페이스에서 입력 한 값이 ObjectDataSource s `UpdateParameters` 컬렉션의 매개 변수에 복사 되 고 ObjectDataSource s `Update()` 메서드를 호출 하 여 업데이트가 시작 됩니다. GridView는 이러한 기본 제공 기능을 삽입 하는 기능을 제공 하지 않으므로 ObjectDataSource s `Insert()` 메서드를 호출 하는 코드를 구현 하 고 삽입 인터페이스의 값을 ObjectDataSource s `InsertParameters` 컬렉션에 복사 해야 합니다.

이 삽입 논리는 추가 단추를 클릭 한 후에 실행 해야 합니다. GridView의 단추 [추가 및 응답](../custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-cs.md) 에 설명 된 대로 Gridview의 단추, LinkButton 또는 ImageButton이 클릭 될 때마다 gridview s `RowCommand` 이벤트가 다시 게시 될 때 발생 합니다. 이 이벤트는 단추, LinkButton 또는 ImageButton이 바닥글 행의 추가 단추와 같이 명시적으로 추가 되었거나 GridView에서 자동으로 추가 된 경우 (예: 정렬을 사용 하도록 설정 된 경우 각 열의 맨 위에 있는 Linkbutton 또는 페이징 사용이 선택 된 경우 페이징 인터페이스의 Linkbutton를 선택 합니다.

따라서 사용자에 게 추가 단추를 클릭 하 여 응답 하려면 GridView s `RowCommand` 이벤트에 대 한 이벤트 처리기를 만들어야 합니다. 이 이벤트는 GridView의 *단추,* LinkButton 또는 ImageButton을 클릭할 때마다 발생 하므로 이벤트 처리기에 전달 된 `CommandName` 속성이 추가 단추 (Insert)의 `CommandName` 값에 매핑되는 경우에만 삽입 논리를 진행 하는 것이 중요 합니다. 또한 유효성 검사 컨트롤이 유효한 데이터를 보고 하는 경우에만 계속 진행 해야 합니다. 이를 위해 다음 코드를 사용 하 여 `RowCommand` 이벤트에 대 한 이벤트 처리기를 만듭니다.

[!code-csharp[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample6.cs)]

> [!NOTE]
> 이벤트 처리기가 `Page.IsValid` 속성을 bothers 확인 하는 이유가 궁금할 수 있습니다. 그 후에는 삽입 인터페이스에 잘못 된 데이터가 제공 된 경우 포스트백이 억제 되지 않습니까? 이 가정은 사용자가 JavaScript를 사용 하지 않도록 설정 하거나 클라이언트 쪽 유효성 검사 논리를 우회 하는 단계를 수행한 경우에만 올바릅니다. 간단히 말해서 클라이언트 쪽 유효성 검사를 엄격 하 게 사용 하면 안 됩니다. 데이터를 사용 하기 전에 서버 쪽 유효성 검사를 항상 수행 해야 합니다.

1 단계에서는 `Insert()` 메서드가 `ProductsBLL` 클래스의 `AddProduct` 메서드에 매핑되도록 `ProductsDataSource` ObjectDataSource를 만들었습니다. `Products` 테이블에 새 레코드를 삽입 하려면 ObjectDataSource s `Insert()` 메서드를 호출 하기만 하면 됩니다.

[!code-csharp[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample7.cs)]

`Insert()` 메서드를 호출 했으므로 이제는 삽입 인터페이스에서 `ProductsBLL` 클래스 s `AddProduct` 메서드에 전달 된 매개 변수에 값을 복사 하는 것만 남았습니다. [삽입, 업데이트 및 삭제 자습서와 관련 된 이벤트를 검사](../editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs.md) 하는 방법에 대 한 자세한 내용은 ObjectDataSource s `Inserting` 이벤트를 통해 수행할 수 있습니다. `Inserting` 이벤트에서 `Products` GridView s 바닥글 행의 컨트롤을 프로그래밍 방식으로 참조 하 고 `e.InputParameters` 컬렉션에 해당 값을 할당 해야 합니다. 사용자가 `ReorderLevel` 텍스트 상자를 비워 두는 것과 같은 값을 생략 한 경우에는 데이터베이스에 삽입 된 값을 `NULL`하도록 지정 해야 합니다. `AddProducts` 메서드는 nullable 데이터베이스 필드에 nullable 형식을 허용 하므로 사용자 입력이 생략 된 경우 nullable 형식을 사용 하 고 해당 값을 `null`로 설정 하면 됩니다.

[!code-csharp[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample8.cs)]

`Inserting` 이벤트 처리기가 완료 되 면 GridView 바닥글 행을 통해 `Products` 데이터베이스 테이블에 새 레코드를 추가할 수 있습니다. 계속 해 서 몇 가지 새 제품을 추가 해 보세요.

## <a name="enhancing-and-customizing-the-add-operation"></a>추가 작업 향상 및 사용자 지정

현재 추가 단추를 클릭 하 여 데이터베이스 테이블에 새 레코드를 추가 하지만 레코드가 성공적으로 추가 되었다는 시각적 피드백은 제공 하지 않습니다. 이상적인 경우 레이블 웹 컨트롤 또는 클라이언트 쪽 경고 상자는 삽입이 성공 상태로 완료 되었음을 사용자에 게 알립니다. 독자를 위한 연습으로 남겨 둡니다.

이 자습서에 사용 된 GridView는 나열 된 제품에 정렬 순서를 적용 하지 않으며 최종 사용자가 데이터를 정렬할 수 없도록 합니다. 따라서 레코드는 기본 키 필드에 따라 데이터베이스에 있는 것 처럼 정렬 됩니다. 각 새 레코드에는 마지막 값 보다 큰 `ProductID` 값이 있으므로 새 제품이 추가 될 때마다 표 끝에 누적 됩니다. 따라서 새 레코드를 추가한 후 GridView의 마지막 페이지에 사용자를 자동으로 보낼 수 있습니다. 이 작업을 수행 하려면 `RowCommand` 이벤트 처리기에서 `ProductsDataSource.Insert()`를 호출한 후 다음 코드 줄을 추가 하 여 데이터를 GridView에 바인딩한 후 사용자를 마지막 페이지로 보내야 함을 표시 합니다.

[!code-csharp[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample9.cs)]

`SendUserToLastPage`은 `false`값이 처음 할당 된 페이지 수준 부울 변수입니다. GridView s `DataBound` 이벤트 처리기에서 `SendUserToLastPage`이 false 이면 `PageIndex` 속성이 업데이트 되어 사용자를 마지막 페이지로 보냅니다.

[!code-csharp[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample10.cs)]

`DataBound` 이벤트 처리기에서 `PageIndex` 속성이 설정 된 이유 (`RowCommand` 이벤트 처리기와는 달리)는 `RowCommand` 이벤트 처리기가 실행 될 때 `Products` 데이터베이스 테이블에 새 레코드를 추가 하기 때문에 발생 하기 때문입니다. 따라서 `RowCommand` 이벤트 처리기에서 마지막 페이지 인덱스 (`PageCount - 1`)는 새 제품이 추가 *되기 전의* 마지막 페이지 인덱스를 나타냅니다. 대부분 추가 되는 제품의 경우 새 제품을 추가한 후 마지막 페이지 인덱스는 동일 합니다. 그러나 추가 된 제품이 새 마지막 페이지 인덱스를 사용 하는 경우 `RowCommand` 이벤트 처리기에서 `PageIndex`를 잘못 업데이트 하면 마지막 페이지 인덱스와는 달리 마지막 페이지 (새 제품을 추가 하기 전의 마지막 페이지 인덱스)로 이동 합니다. `DataBound` 이벤트 처리기는 새 제품이 추가 된 후에 실행 되 고 데이터가 그리드로 다시 바인딩 되었으므로 `PageIndex` 속성을 설정 하 여 올바른 마지막 페이지 인덱스를 다시 가져오는 것을 알 수 있습니다.

마지막으로,이 자습서에 사용 된 GridView는 새 제품을 추가 하기 위해 수집 해야 하는 필드의 수로 인해 상당히 광범위 합니다. 이 너비로 인해 DetailsView의 세로 레이아웃을 선호 하는 경우가 있을 수 있습니다. 적은 수의 입력을 수집 하 여 GridView의 전체 너비를 줄일 수 있습니다. 새 제품을 추가할 때 `UnitsOnOrder`, `UnitsInStock`및 `ReorderLevel` 필드를 수집할 필요가 없습니다 .이 경우 GridView에서 이러한 필드를 제거할 수 있습니다.

수집 된 데이터를 조정 하기 위해 다음 두 가지 방법 중 하나를 사용할 수 있습니다.

- `UnitsOnOrder`, `UnitsInStock`및 `ReorderLevel` 필드에 대 한 값이 필요한 `AddProduct` 메서드를 계속 사용 합니다. `Inserting` 이벤트 처리기에서 삽입 인터페이스에서 제거 된 이러한 입력에 사용할 하드 코드 된 기본값을 제공 합니다.
- `ProductsBLL` 클래스에서 `UnitsOnOrder`, `UnitsInStock`및 `ReorderLevel` 필드의 입력을 허용 하지 않는 `AddProduct` 메서드의 새 오버 로드를 만듭니다. 그런 다음 ASP.NET 페이지에서이 새 오버 로드를 사용 하도록 ObjectDataSource를 구성 합니다.

두 옵션 모두 동일 하 게 작동 합니다. 이전 자습서에서는 두 번째 옵션을 사용 하 여 `ProductsBLL` 클래스 `UpdateProduct` 메서드에 대해 여러 오버 로드를 생성 했습니다.

## <a name="summary"></a>요약

GridView는 DetailsView 및 FormView에 있는 기본 제공 삽입 기능을 제공 하지 않지만 삽입 인터페이스를 바닥글 행에 추가할 수 있습니다. GridView에 바닥글 행을 표시 하려면 단순히 해당 `ShowFooter` 속성을 `true`로 설정 합니다. 필드를 Templatefield로 변환 변환 하 고 삽입 인터페이스를 `FooterTemplate`에 추가 하 여 각 필드에 대해 바닥글 행 콘텐츠를 사용자 지정할 수 있습니다. 이 자습서에서 살펴본 것 처럼 `FooterTemplate`에는 데이터 기반 웹 컨트롤 (예: Dropdownlist) 및 유효성 검사 컨트롤을 채울 수 있는 단추, 텍스트 상자, Dropdownlist, 확인란, 데이터 소스 컨트롤이 포함 될 수 있습니다. 사용자 입력을 수집 하는 컨트롤과 함께 추가 단추, LinkButton 또는 ImageButton이 필요 합니다.

추가 단추를 클릭 하면 삽입 워크플로를 시작 하기 위해 ObjectDataSource s `Insert()` 메서드가 호출 됩니다. 그런 다음 ObjectDataSource는 구성 된 삽입 메서드 (이 자습서에서는 `ProductsBLL` 클래스 `AddProduct` 메서드)를 호출 합니다. 삽입 메서드를 호출 하기 전에 GridView s 삽입 인터페이스의 값을 ObjectDataSource s `InsertParameters` 컬렉션에 복사 해야 합니다. 이렇게 하려면 ObjectDataSource s `Inserting` 이벤트 처리기에서 인터페이스 삽입 웹 컨트롤을 프로그래밍 방식으로 참조 합니다.

이 자습서에서는 GridView의 모양을 향상 시키는 방법을 살펴봅니다. 다음 자습서 집합에서는 이미지, Pdf, Word 문서 등의 이진 데이터를 사용 하는 방법과 데이터 웹 컨트롤을 사용 하는 방법을 살펴봅니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Bernadette Leigh입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](adding-a-gridview-column-of-checkboxes-cs.md)
> [다음](adding-a-gridview-column-of-radio-buttons-vb.md)
