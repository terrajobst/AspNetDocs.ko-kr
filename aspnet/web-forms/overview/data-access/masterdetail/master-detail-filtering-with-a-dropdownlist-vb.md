---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-vb
title: DropDownList를 사용 하 여 마스터/세부 정보 필터링 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 GridView에서 마스터 레코드를 표시 하는 방법과 GridView에서 선택한 목록 항목의 세부 정보를 표시 하는 방법을 알아봅니다.
ms.author: riande
ms.date: 03/31/2010
ms.assetid: ea44717e-ab2e-46cd-a692-e4a9c0de194c
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 62cd296a3f36e1779666a6b5db15b0ce2488d0e4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74640222"
---
# <a name="masterdetail-filtering-with-a-dropdownlist-vb"></a>DropDownList 한 개로 마스터/세부 정보 필터링(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_7_VB.exe) 또는 [PDF 다운로드](master-detail-filtering-with-a-dropdownlist-vb/_static/datatutorial07vb1.pdf)

> 이 자습서에서는 GridView에서 마스터 레코드를 표시 하는 방법과 GridView에서 선택한 목록 항목의 세부 정보를 표시 하는 방법을 알아봅니다.

## <a name="introduction"></a>소개

일반 보고서 유형으로는 *마스터/세부 정보 보고서*가 있습니다 .이 보고서는 보고서가 "마스터" 레코드 집합을 표시 하는 것으로 시작 합니다. 그러면 사용자가 마스터 레코드 중 하나로 드릴 다운 하 여 해당 마스터 레코드의 "세부 정보"를 볼 수 있습니다. 마스터/세부 정보 보고서는 모든 범주를 표시 하는 보고서와 같이 사용자가 특정 범주를 선택 하 고 연결 된 제품을 표시할 수 있도록 하는 일대다 관계를 시각화 하는 데 적합 한 옵션입니다. 또한 마스터/세부 정보 보고서는 특히 많은 열을 포함 하는 테이블의 세부 정보를 표시 하는 데 유용 합니다. 예를 들어 마스터/세부 보고서의 "마스터" 수준에는 데이터베이스에 있는 제품의 제품 이름 및 단가만 표시 되 고 특정 제품으로 드릴 다운 하면 추가 제품 필드 (범주, 공급자, 단위당 수량 등)가 표시 됩니다.

마스터/세부 정보 보고서를 구현할 수 있는 여러 가지 방법이 있습니다. 이를 통해 다음 세 가지 자습서에서는 다양 한 마스터/세부 정보 보고서를 살펴보겠습니다. 이 자습서에서는 GridView에서 마스터 [레코드를 표시](https://msdn.microsoft.com/library/dtx91y0z.aspx) 하는 방법과 GridView에서 선택한 목록 항목의 세부 정보를 표시 하는 방법을 알아봅니다. 특히이 자습서의 마스터/세부 정보 보고서에는 범주 및 제품 정보가 나열 됩니다.

## <a name="step-1-displaying-the-categories-in-a-dropdownlist"></a>1 단계: DropDownList에 범주 표시

마스터/세부 정보 보고서에는 선택한 목록 항목의 제품이 GridView의 페이지 아래쪽에 표시 되는 DropDownList의 범주가 나열 됩니다. 앞서 첫 번째 작업은 범주를 DropDownList에 표시 하는 것입니다. `Filtering` 폴더에서 `FilterByDropDownList.aspx` 페이지를 열고 도구 상자에서 페이지의 디자이너로 DropDownList를 끌어서 `ID` 속성을 `Categories`로 설정 합니다. 다음으로, DropDownList의 스마트 태그에서 데이터 소스 선택 링크를 클릭 합니다. 그러면 데이터 소스 구성 마법사가 표시 됩니다.

[DropDownList의 데이터 원본을 지정 ![](master-detail-filtering-with-a-dropdownlist-vb/_static/image2.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image1.png)

**그림 1**: DropDownList의 데이터 원본 지정 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-vb/_static/image3.png))

`CategoriesBLL` 클래스의 `GetCategories()` 메서드를 호출 하는 `CategoriesDataSource` 라는 새 ObjectDataSource를 추가 하도록 선택 합니다.

[새 ObjectDataSource 명명 된 범주 Datasource를 추가 ![](master-detail-filtering-with-a-dropdownlist-vb/_static/image5.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image4.png)

**그림 2**: 이름이 `CategoriesDataSource` 새 ObjectDataSource 추가 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-vb/_static/image6.png))

[![범주 Bll 클래스를 사용 하도록 선택 합니다.](master-detail-filtering-with-a-dropdownlist-vb/_static/image8.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image7.png)

**그림 3**: `CategoriesBLL` 클래스를 사용 하도록 선택 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-vb/_static/image9.png))

[GetCategories () 메서드를 사용 하도록 ObjectDataSource를 구성 ![](master-detail-filtering-with-a-dropdownlist-vb/_static/image11.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image10.png)

**그림 4**: `GetCategories()` 메서드를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-vb/_static/image12.png))

ObjectDataSource를 구성한 후에는 DropDownList에 표시 해야 하는 데이터 원본 필드와 목록 항목의 값으로 연결 해야 하는 데이터 원본 필드를 지정 해야 합니다. `CategoryName` 필드를 표시 하 고 각 목록 항목의 값으로 `CategoryID` 합니다.

[DropDownList에서 범주 필드를 표시 하 고 CategoryID를 값으로 사용 ![](master-detail-filtering-with-a-dropdownlist-vb/_static/image14.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image13.png)

**그림 5**: DropDownList에 `CategoryName` 필드가 표시 되 고 `CategoryID` 값으로 사용 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-vb/_static/image15.png))

이 시점에서 `Categories` 테이블의 레코드를 사용 하 여 채워진 DropDownList 컨트롤이 있습니다 (약 6 초 후에 수행 됨). 그림 6에서는 브라우저를 통해 볼 때의 진행률을 보여 줍니다.

[드롭다운 목록에서 현재 범주를 ![합니다.](master-detail-filtering-with-a-dropdownlist-vb/_static/image17.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image16.png)

**그림 6**: 드롭다운 목록에 현재 범주가 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-vb/_static/image18.png)).

## <a name="step-2-adding-the-products-gridview"></a>2 단계: Products GridView 추가

마스터/세부 정보 보고서의 마지막 단계는 선택한 범주와 관련 된 제품을 나열 하는 것입니다. 이를 수행 하려면 페이지에 GridView를 추가 하 고 이름이 `productsDataSource`인 새 ObjectDataSource를 만듭니다. `productsDataSource` 컨트롤이 `ProductsBLL` 클래스의 `GetProductsByCategoryID(categoryID)` 메서드에서 데이터를 추려내 합니다.

[![GetProductsByCategoryID (categoryID) 메서드를 선택 합니다.](master-detail-filtering-with-a-dropdownlist-vb/_static/image20.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image19.png)

**그림 7**: `GetProductsByCategoryID(categoryID)` 방법 선택 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-vb/_static/image21.png))

이 메서드를 선택 하면 ObjectDataSource 마법사에서 메서드의 *`categoryID`* 매개 변수에 대 한 값을 묻는 메시지를 표시 합니다. 선택한 `categories` DropDownList 항목의 값을 사용 하려면 매개 변수 소스를 제어 하 고 ControlID를 `Categories`설정 합니다.

[categoryID 매개 변수를 DropDownList 범주의 값으로 설정 ![합니다.](master-detail-filtering-with-a-dropdownlist-vb/_static/image23.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image22.png)

**그림 8**: *`categoryID`* 매개 변수를 `Categories` DropDownList 값으로 설정 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-vb/_static/image24.png))

잠시 후 브라우저에서 진행 상황을 확인해 보세요. 페이지를 처음 방문 하면 선택 된 범주 (음료)에 속하는 해당 제품이 표시 됩니다 (그림 9에 표시 된 것 처럼). 그러나 DropDownList를 변경 해도 데이터가 업데이트 되지는 않습니다. 이는 GridView를 업데이트 하기 위해 포스트백이 수행 되어야 하기 때문입니다. 이를 위해 다음 두 가지 옵션을 사용할 수 없습니다 (코드를 작성 해야 하는 것은 아님).

- **범주 DropDownList의**[AutoPostBack 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.listcontrol.autopostback%28VS.80%29.aspx)을**True로** 설정 합니다. 이는 DropDownList의 스마트 태그에서 Enable AutoPostBack 옵션을 선택 하 여 수행할 수 있습니다. 이렇게 하면 사용자가 DropDownList의 선택 된 항목을 변경할 때마다 포스트백이 트리거됩니다. 따라서 사용자가 DropDownList에서 새 범주를 선택 하면 포스트백이 뒤따르게 되 고 새로 선택한 범주에 대 한 제품으로 GridView가 업데이트 됩니다. 이 방법은이 자습서에서 사용한 방법입니다.
- **DropDownList 옆에 단추 웹 컨트롤을 추가 합니다.** `Text` 속성을 새로 고침으로 설정 하거나 비슷한 항목으로 설정 합니다. 이 방법에서는 사용자가 새 범주를 선택 하 고 단추를 클릭 해야 합니다. 단추를 클릭 하면 포스트백이 발생 하 고 GridView를 업데이트 하 여 선택한 범주의 제품이 나열 됩니다.

그림 9와 10은 마스터/세부 보고서를 실행 하는 방법을 보여 줍니다.

[페이지를 처음 방문할 때 ![음료 제품이 표시 됩니다.](master-detail-filtering-with-a-dropdownlist-vb/_static/image26.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image25.png)

**그림 9**: 페이지를 처음 방문할 때 음료 제품이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-vb/_static/image27.png)).

[새 제품 (생성)을 선택 ![자동으로 포스트백이 발생 하 고 GridView가 업데이트 됩니다.](master-detail-filtering-with-a-dropdownlist-vb/_static/image29.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image28.png)

**그림 10**: 새 제품 (생성)을 선택 하면 자동으로 다시 게시 되 고 GridView가 업데이트 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-vb/_static/image30.png)).

## <a name="adding-a----choose-a-category----list-item"></a>"--범주 선택--" 목록 항목 추가

`FilterByDropDownList.aspx` 페이지를 처음 방문 하면 범주 DropDownList의 첫 번째 목록 항목 (음료)이 기본적으로 선택 되어 GridView의 음료 제품이 표시 됩니다. 첫 번째 범주의 제품을 표시 하는 대신 "--범주 선택--"과 같은 항목을 선택 하는 DropDownList 항목을 대신 사용할 수 있습니다.

DropDownList에 새 목록 항목을 추가 하려면 속성 창로 이동 하 여 `Items` 속성에서 줄임표를 클릭 합니다. `Text` "--범주 선택--"과 `Value` `-1`를 사용 하 여 새 목록 항목을 추가 합니다.

[a를 추가 ![--범주 선택--목록 항목](master-detail-filtering-with-a-dropdownlist-vb/_static/image32.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image31.png)

**그림 11**: a--범주 선택--목록 항목 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-vb/_static/image33.png))

또는 다음 태그를 DropDownList에 추가 하 여 목록 항목을 추가할 수 있습니다.

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-vb/samples/sample1.aspx)]

또한 범주를 ObjectDataSource에서 DropDownList에 바인딩할 때 `AppendDataBoundItems` True가 아니면 수동으로 추가 된 목록 항목을 덮어쓰도록 `AppendDataBoundItems` DropDownList 컨트롤의을 True로 설정 해야 합니다.

![AppendDataBoundItems 속성을 True로 설정 합니다.](master-detail-filtering-with-a-dropdownlist-vb/_static/image34.png)

**그림 12**: `AppendDataBoundItems` 속성을 True로 설정

이러한 변경 후 페이지를 처음 방문 하면 "--범주 선택--" 옵션이 선택 되 고 제품이 표시 되지 않습니다.

[초기 페이지 로드에 ![표시 되는 제품이 없습니다.](master-detail-filtering-with-a-dropdownlist-vb/_static/image36.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image35.png)

**그림 13**: 초기 페이지 로드에서 제품이 표시 되지 않음 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-vb/_static/image37.png))

"--범주 선택--" 목록 항목을 선택 했기 때문에 제품이 표시 되지 않습니다. "목록 항목을 선택 했기 때문 `-1``CategoryID` `-1`입니다. 이 동작을 원하는 경우이 시점에서 작업을 수행 합니다. 그러나 "--범주 선택--" 목록 항목을 선택할 때 *모든* 범주를 표시 하려는 경우 `ProductsBLL` 클래스로 돌아가서 전달 된 *`categoryID`* 매개 변수가 0 보다 작은 경우 `GetProducts()` 메서드를 호출 하도록 `GetProductsByCategoryID(categoryID)` 메서드를 사용자 지정 합니다.

[!code-vb[Main](master-detail-filtering-with-a-dropdownlist-vb/samples/sample2.vb)]

여기서 사용 되는 기법은 모든 공급자를 [선언적 매개 변수](../basic-reporting/declarative-parameters-cs.md) 자습서에 다시 표시 하는 데 사용 하는 방법과 비슷합니다 .이 예에서는 `-1` 값을 사용 하 여 `Nothing`와는 반대로 모든 레코드를 검색 해야 함을 나타냅니다. 이는 `GetProductsByCategoryID(categoryID)` 메서드의 *`categoryID`* 매개 변수에 정수 값이 전달 될 것으로 예상 하는 반면 선언적 매개 변수 자습서에서는 문자열 입력 매개 변수를 전달 하기 때문입니다.

그림 14에서는 "--범주 선택--" 옵션이 선택 되어 있는 `FilterByDropDownList.aspx`의 스크린샷을 보여 줍니다. 여기서는 모든 제품이 기본적으로 표시 되며, 사용자는 특정 범주를 선택 하 여 표시 범위를 좁힐 수 있습니다.

[이제 모든 제품이 기본적으로 나열 ![](master-detail-filtering-with-a-dropdownlist-vb/_static/image39.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image38.png)

**그림 14**: 이제 모든 제품이 기본적으로 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-vb/_static/image40.png)).

## <a name="summary"></a>요약

계층적으로 관련 된 데이터를 표시 하는 경우 사용자가 계층의 맨 위에서 데이터를 확인 하 고 세부 정보로 드릴 다운할 수 있는 마스터/세부 정보 보고서를 사용 하 여 데이터를 표시 하는 것이 좋습니다. 이 자습서에서는 선택한 범주의 제품을 보여 주는 간단한 마스터/세부 정보 보고서 작성을 검토 했습니다. 이는 범주 목록에 대해 DropDownList을 사용 하 고 선택한 범주에 속한 제품에 대해 GridView를 사용 하 여 수행 되었습니다.

[다음 자습서](master-detail-filtering-with-two-dropdownlists-vb.md) 에서는 두 개의 dropdownlist를 사용 하 여 DropDownList 인터페이스를 한 단계 더 살펴보겠습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

> [!div class="step-by-step"]
> [이전](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)
> [다음](master-detail-filtering-with-two-dropdownlists-vb.md)
