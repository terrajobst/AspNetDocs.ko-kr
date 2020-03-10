---
uid: web-forms/overview/data-access/masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs
title: 세부 정보 DetailView (C#)와 함께 선택 가능한 마스터 GridView를 사용 하 여 마스터/세부 정보 | Microsoft Docs
author: rick-anderson
description: 이 자습서에는 각 제품의 이름과 가격이 선택 단추와 함께 포함 되어 있는 GridView가 포함 됩니다. Particu에 대 한 선택 단추를 클릭 합니다.
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 0f982827-f8f9-420d-b36b-57b23f5aa519
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs
msc.type: authoredcontent
ms.openlocfilehash: 04c427341f063729bd23b416a96f5acb20702792
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78503627"
---
# <a name="masterdetail-using-a-selectable-master-gridview-with-a-details-detailview-c"></a>세부 정보 DetailView와 함께 선택 가능한 마스터 GridView를 사용하는 마스터/세부 정보(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_10_CS.exe) 또는 [PDF 다운로드](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/datatutorial10cs1.pdf)

> 이 자습서에는 각 제품의 이름과 가격이 선택 단추와 함께 포함 되어 있는 GridView가 포함 됩니다. 특정 제품에 대해 선택 단추를 클릭 하면 해당 전체 정보가 동일한 페이지의 DetailsView 컨트롤에 표시 됩니다.

## <a name="introduction"></a>소개

[이전 자습서](master-detail-filtering-across-two-pages-cs.md) 에서는 두 개의 웹 페이지인 "마스터" 웹 페이지를 사용 하 여 마스터/세부 정보 보고서를 만드는 방법에 대해 알아보았습니다. 여기에서 공급자 목록을 표시 했습니다. 선택한 공급 업체에서 제공 하는 제품을 나열 하는 "세부 정보" 웹 페이지입니다. 이 두 페이지 보고서 형식은 한 페이지로 압축할 수 있습니다. 이 자습서에는 각 제품의 이름과 가격이 선택 단추와 함께 포함 되어 있는 GridView가 포함 됩니다. 특정 제품에 대해 선택 단추를 클릭 하면 해당 전체 정보가 동일한 페이지의 DetailsView 컨트롤에 표시 됩니다.

[선택 단추를 클릭 ![제품의 세부 정보가 표시 됩니다.](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image2.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image1.png)

**그림 1**: 선택 단추를 클릭 하면 제품의 세부 정보가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image3.png)).

## <a name="step-1-creating-a-selectable-gridview"></a>1 단계: 선택 가능한 GridView 만들기

2 페이지 마스터/세부 정보 보고서에는 클릭 하면 쿼리 문자열에서 클릭 한 행의 `SupplierID` 값을 전달 하는 세부 정보 페이지로 사용자를 전송 하는 하이퍼링크가 포함 되어 있음을 기억 하세요. 이러한 하이퍼링크는 하이퍼링크 필드를 사용 하 여 각 GridView 행에 추가 되었습니다. 단일 페이지 마스터/세부 정보 보고서의 경우 클릭 하면 세부 정보가 표시 되는 각 GridView 행에 대 한 단추가 필요 합니다. 다시 게시를 발생 시키고 해당 행을 GridView의 [Selectedrow](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedrow.aspx)로 표시 하는 각 행에 대해 선택 단추를 포함 하도록 GridView 컨트롤을 구성할 수 있습니다.

먼저 `Filtering` 폴더의 `DetailsBySelecting.aspx` 페이지에 GridView 컨트롤을 추가 하 고 `ID` 속성을 `ProductsGrid`로 설정 합니다. 다음으로 `ProductsBLL` 클래스의 `GetProducts()` 메서드를 호출 하는 `AllProductsDataSource` 라는 새 ObjectDataSource를 추가 합니다.

[AllProductsDataSource 라는 ObjectDataSource를 만들 ![](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image5.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image4.png)

**그림 2**: 이름이 `AllProductsDataSource` ObjectDataSource 만들기 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image6.png))

[ProductsBLL 클래스를 사용 ![](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image8.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image7.png)

**그림 3**: `ProductsBLL` 클래스 사용 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image9.png))

[GetProducts () 메서드를 호출 하도록 ObjectDataSource를 구성 ![](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image11.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image10.png)

**그림 4**: `GetProducts()` 메서드를 호출 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image12.png))

`ProductName` 및 `UnitPrice` BoundFields를 제외 하 고 모두 제거 하는 GridView의 필드를 편집 합니다. 또한 `UnitPrice` BoundField의 서식을 통화로 지정 하 고 BoundFields의 `HeaderText` 속성을 변경 하는 것과 같이 필요에 따라 이러한 BoundFields를 자유롭게 사용자 지정할 수 있습니다. 이러한 단계는 GridView의 스마트 태그에서 열 편집 링크를 클릭 하거나 선언적 구문을 수동으로 구성 하 여 그래픽으로 수행할 수 있습니다.

[ProductName 및 UnitPrice BoundFields를 제외한 모든 ![제거](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image14.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image13.png)

**그림 5**: `ProductName` 및 `UnitPrice` BoundFields를 제외한 모두 제거 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image15.png))

GridView의 최종 태그는 다음과 같습니다.

[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/samples/sample1.aspx)]

다음으로 GridView를 선택 가능으로 표시 해야 합니다. 그러면 각 행에 선택 단추가 추가 됩니다. 이를 위해서는 GridView의 스마트 태그에서 선택 사용 확인란을 선택 하면 됩니다.

[GridView의 행을 선택할 수 있도록 ![](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image17.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image16.png)

**그림 6**: GridView의 행을 선택할 수 있도록 설정 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image18.png))

선택 사용 옵션을 선택 하면 `ShowSelectButton` 속성이 True로 설정 된 `ProductsGrid` GridView에 CommandField가 추가 됩니다. 그러면 그림 6에 나와 있는 것 처럼 GridView의 각 행에 대해 선택 단추가 생성 됩니다. 기본적으로 선택 단추는 Linkbutton로 렌더링 되지만 CommandField의 `ButtonType` 속성을 통해 단추 또는 ImageButtons을 대신 사용할 수 있습니다.

[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/samples/sample2.aspx)]

GridView 행의 선택 단추를 클릭 하면 ensues가 다시 게시 되 고 GridView의 `SelectedRow` 속성이 업데이트 됩니다. `SelectedRow` 속성 외에도 GridView는 [SelectedIndex](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedindex%28VS.80%29.aspx), [SelectedValue](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedvalue%28VS.80%29.aspx)및 [selecteddatakey](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selecteddatakey%28VS.80%29.aspx) 속성을 제공 합니다. `SelectedIndex` 속성은 선택한 행의 인덱스를 반환 하는 반면 `SelectedValue` 및 `SelectedDataKey` 속성은 GridView의 [DataKeyNames 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.datakeynames%28VS.80%29.aspx)에 따라 값을 반환 합니다.

`DataKeyNames` 속성은 각 행과 하나 이상의 데이터 필드 값을 연결 하는 데 사용 되며, 각 GridView 행에서 기본 데이터의 정보를 고유 하 게 식별 하는 데 주로 사용 됩니다. `SelectedValue` 속성은 선택한 행에 대 한 첫 번째 `DataKeyNames` 데이터 필드의 값을 반환 합니다. 여기서 `SelectedDataKey` 속성은 선택한 행의 `DataKey` 개체를 반환 합니다. 여기에는 해당 행에 대 한 지정 된 데이터 키 필드의 모든 값이 포함 됩니다.

디자이너를 통해 데이터 소스를 GridView, DetailsView 또는 FormView에 바인딩하는 경우 `DataKeyNames` 속성은 고유 하 게 식별 되는 데이터 필드로 자동 설정 됩니다. 이전 자습서에서이 속성을 자동으로 설정 했지만이 예는 지정 된 `DataKeyNames` 속성 없이 작동 했습니다. 그러나이 자습서에서 선택할 수 있는 GridView와 삽입, 업데이트 및 삭제를 검사할 이후 자습서의 경우에는 `DataKeyNames` 속성을 올바르게 설정 해야 합니다. 잠시 후 GridView의 `DataKeyNames` 속성이 `ProductID`로 설정 되었는지 확인 합니다.

지금까지 브라우저를 통해 진행 상황을 살펴보겠습니다. GridView는 Select LinkButton와 함께 모든 제품의 이름과 가격을 나열 합니다. 선택 단추를 클릭 하면 포스트백이 발생 합니다. 2 단계에서는 선택한 제품에 대 한 세부 정보를 표시 하 여이 포스트백에 대해 DetailsView이 응답 하는 방법을 알아봅니다.

[![각 제품 행에 Select LinkButton이 포함 되어 있습니다.](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image20.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image19.png)

**그림 7**: 각 제품 행에 Select LinkButton 포함 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image21.png))

### <a name="highlighting-the-selected-row"></a>선택한 행 강조 표시

`ProductsGrid` GridView에는 선택한 행의 비주얼 스타일을 지시 하는 데 사용할 수 있는 `SelectedRowStyle` 속성이 있습니다. 이 기능을 사용 하면 현재 선택 된 GridView의 행을 보다 명확 하 게 표시 하 여 사용자 환경을 향상 시킬 수 있습니다. 이 자습서에서는 선택한 행을 노란색 배경으로 강조 표시 합니다.

이전 자습서와 마찬가지로 CSS 클래스로 정의 된 미적 관련 설정을 유지 하려고 합니다. 따라서 `Styles.css` `SelectedRowStyle`라는 새 CSS 클래스를 만듭니다.

[!code-css[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/samples/sample3.css)]

이 CSS 클래스를 자습서 시리즈의 *모든* gridviews의 `SelectedRowStyle` 속성에 적용 하려면 아래와 같이 `SelectedRowStyle` 설정을 포함 하도록 `DataWebControls` 테마에서 `GridView.skin` 스킨을 편집 합니다.

[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/samples/sample4.aspx)]

이 외에도 선택한 GridView 행이 노란색 배경색으로 강조 표시 됩니다.

[GridView의 SelectedRowStyle 속성을 사용 하 여 선택한 행의 모양을 사용자 지정 ![](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image23.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image22.png)

**그림 8**: GridView의 `SelectedRowStyle` 속성을 사용 하 여 선택한 행의 모양을 사용자 지정 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image24.png))

## <a name="step-2-displaying-the-selected-products-details-in-a-detailsview"></a>2 단계: DetailsView에서 선택한 제품의 세부 정보 표시

`ProductsGrid` GridView가 완료 되 면 선택한 특정 제품에 대 한 정보를 표시 하는 DetailsView만 추가 하면 됩니다. GridView 위에 DetailsView 컨트롤을 추가 하 고 `ProductDetailsDataSource`라는 새 ObjectDataSource를 만듭니다. 이 DetailsView에서 선택한 제품에 대 한 특정 정보를 표시 하려고 하므로 `ProductsBLL` 클래스의 `GetProductByProductID(productID)` 메서드를 사용 하도록 `ProductDetailsDataSource`를 구성 합니다.

[ProductsBLL 클래스의 Getbyproductid (productID) 메서드를 호출 ![합니다.](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image26.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image25.png)

**그림 9**: `ProductsBLL` 클래스의 `GetProductByProductID(productID)` 메서드 호출 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image27.png))

GridView 컨트롤의 `SelectedValue` 속성에서 가져온 *`productID`* 매개 변수의 값이 있어야 합니다. 앞에서 설명한 것 처럼 GridView의 `SelectedValue` 속성은 선택한 행에 대 한 첫 번째 데이터 키 값을 반환 합니다. 따라서 GridView의 `DataKeyNames` 속성이 `ProductID`로 설정 되어 있으므로 `SelectedValue`에서 선택한 행의 `ProductID` 값이 반환 됩니다.

[productID 매개 변수를 GridView의 SelectedValue 속성으로 설정 ![](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image29.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image28.png)

**그림 10**: *`productID`* 매개 변수를 GridView의 `SelectedValue` 속성으로 설정 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image30.png))

`productDetailsDataSource` ObjectDataSource를 올바르게 구성 하 고 DetailsView에 바인딩한 후에는이 자습서를 완료 합니다. 페이지를 처음 방문 하면 행이 선택 되지 않으므로 GridView의 `SelectedValue` 속성은 `null`을 반환 합니다. `NULL` `ProductID` 값을 포함 하는 제품이 없으므로 `GetProductByProductID(productID)` 메서드에서 레코드가 반환 되지 않습니다. 즉, DetailsView은 표시 되지 않습니다 (그림 11 참조). GridView 행의 선택 단추를 클릭 하면 다시 게시 ensues 및 DetailsView이 새로 고쳐집니다. 이번에는 GridView의 `SelectedValue` 속성이 선택 된 행의 `ProductID`을 반환 하 고, `GetProductByProductID(productID)` 메서드에서는 특정 제품에 대 한 정보가 포함 된 `ProductsDataTable`를 반환 하며, DetailsView은 이러한 세부 정보를 표시 합니다 (그림 12 참조).

[![처음으로 방문 하면 GridView만 표시 됩니다.](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image32.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image31.png)

**그림 11**: 처음 방문한 경우 GridView만 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image33.png)).

[행을 선택할 때 ![제품의 세부 정보가 표시 됩니다.](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image35.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image34.png)

**그림 12**: 행을 선택할 때 제품의 세부 정보가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image36.png)).

## <a name="summary"></a>요약

이 및 앞의 세 가지 자습서에서는 마스터/세부 보고서를 표시 하는 다양 한 기술을 살펴보았습니다. 이 자습서에서는 선택 가능한 GridView를 사용 하 여 마스터 레코드를 보관 하 고 DetailsView을 사용 하 여 동일한 페이지에서 선택한 마스터 레코드에 대 한 세부 정보를 표시 하는 방법을 살펴보았습니다. 이전 자습서에서는 Dropdownlist를 사용 하 여 마스터/세부 정보 보고서를 표시 하 고 한 웹 페이지에서 마스터 레코드를 표시 하 고 다른 웹 페이지에 대 한 세부 레코드를 표시 하는 방법을 살펴보았습니다

이 자습서에서는 마스터/세부 정보 보고서에 대 한 검사를 마칩니다. 다음 자습서부터 GridView, DetailsView 및 FormView로 사용자 지정 된 서식 지정의 탐색을 시작 합니다. 이러한 컨트롤의 모양을 사용자 지정 하는 방법, GridView 바닥글의 데이터를 요약 하는 방법 및 템플릿을 사용 하 여 레이아웃을 보다 세부적으로 제어 하는 방법을 알아봅니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Hilton Gid Esenow 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](master-detail-filtering-across-two-pages-cs.md)
> [다음](master-detail-filtering-with-a-dropdownlist-vb.md)
