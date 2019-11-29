---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-with-two-dropdownlists-cs
title: 두 Dropdownlist를 사용 하는 마스터/C#세부 정보 필터링 () | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 마스터/세부 관계를 확장 하 여 세 번째 계층을 추가 하 고, 두 개의 DropDownList 컨트롤을 사용 하 여 원하는 부모 및 최상위 항목을 선택 합니다.
ms.author: riande
ms.date: 03/31/2010
ms.assetid: ac4b0d77-4816-4ded-afd0-88dab667aedd
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-with-two-dropdownlists-cs
msc.type: authoredcontent
ms.openlocfilehash: e24b7f91d34fbce1676f7f28ebb7d23903157f7f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74625803"
---
# <a name="masterdetail-filtering-with-two-dropdownlists-c"></a>DropDownList 두 개로 마스터/세부 정보 필터링(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_8_CS.exe) 또는 [PDF 다운로드](master-detail-filtering-with-two-dropdownlists-cs/_static/datatutorial08cs1.pdf)

> 이 자습서에서는 마스터/세부 관계를 확장 하 여 세 번째 계층을 추가 하 고, 두 개의 DropDownList 컨트롤을 사용 하 여 원하는 부모 및 최상위 레코드를 선택 합니다.

## <a name="introduction"></a>소개

[이전 자습서](master-detail-filtering-with-a-dropdownlist-cs.md) 에서는 범주 및 선택 된 범주에 속하는 제품을 보여 주는 GridView로 채워진 단일 DropDownList을 사용 하 여 간단한 마스터/세부 정보 보고서를 표시 하는 방법을 살펴보았습니다. 이 보고서 패턴은 일 대 다 관계를 포함 하는 레코드를 표시할 때 잘 작동 하며 여러 개의 일대다 관계를 포함 하는 시나리오에 맞게 쉽게 확장할 수 있습니다. 예를 들어 주문 입력 시스템에는 고객, 주문 및 주문 라인 항목에 해당 하는 테이블이 있습니다. 지정 된 고객에 게는 여러 항목으로 구성 된 각 주문의 주문이 여러 개 있을 수 있습니다. 이러한 데이터는 두 개의 Dropdownlist 및 GridView를 사용 하 여 사용자에 게 제공 될 수 있습니다. 첫 번째 DropDownList에는 데이터베이스에 있는 각 고객에 대 한 목록 항목이 있으며 두 번째 항목의 내용이 선택한 고객에 의해 배치 된 주문입니다. GridView를 선택 하면 선택한 주문의 줄 항목이 나열 됩니다.

Northwind 데이터베이스는 `Customers`, `Orders`및 `Order Details` 테이블에 정식 고객/주문/주문 정보 정보를 포함 하는 반면 이러한 테이블은 아키텍처에서 캡처되지 않습니다. 그럼에도 불구 하 고 두 개의 종속 된 Dropdownlist 사용 하는 것도 보여 줄 수 있습니다. 첫 번째 DropDownList에는 선택한 범주에 속하는 범주와 두 번째 제품이 나열 됩니다. 그러면 DetailsView에서 선택한 제품에 대 한 세부 정보를 나열 합니다.

## <a name="step-1-creating-and-populating-the-categories-dropdownlist"></a>1 단계: 범주 만들기 및 채우기

첫 번째 목표는 범주를 나열 하는 DropDownList을 추가 하는 것입니다. 이러한 단계는 앞의 자습서에서 자세히 검토 했지만 완전성을 위해 여기에 요약 되어 있습니다.

`Filtering` 폴더에서 `MasterDetailsDetails.aspx` 페이지를 열고 페이지에 DropDownList를 추가 하 고 `ID` 속성을 `Categories`로 설정한 다음 해당 스마트 태그에서 데이터 소스 구성 링크를 클릭 합니다. 데이터 소스 구성 마법사에서 새 데이터 원본을 추가 하도록 선택 합니다.

[DropDownList에 대 한 새 데이터 소스를 추가 ![](master-detail-filtering-with-two-dropdownlists-cs/_static/image2.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image1.png)

**그림 1**: DropDownList에 대 한 새 데이터 소스 추가 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image3.png))

새 데이터 원본은 자연스럽 게 ObjectDataSource 여야 합니다. 새 ObjectDataSource `CategoriesDataSource`의 이름을로 `CategoriesBLL` 개체의 `GetCategories()` 메서드를 호출 합니다.

[![범주 Bll 클래스를 사용 하도록 선택 합니다.](master-detail-filtering-with-two-dropdownlists-cs/_static/image5.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image4.png)

**그림 2**: `CategoriesBLL` 클래스를 사용 하도록 선택 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image6.png))

[GetCategories () 메서드를 사용 하도록 ObjectDataSource를 구성 ![](master-detail-filtering-with-two-dropdownlists-cs/_static/image8.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image7.png)

**그림 3**: `GetCategories()` 메서드를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image9.png))

ObjectDataSource를 구성한 후에는 `Categories` DropDownList에 표시 해야 하는 데이터 원본 필드와 목록 항목에 대 한 값으로 구성 해야 하는 데이터 원본 필드를 지정 해야 합니다. `CategoryName` 필드를 표시로 설정 하 고 `CategoryID` 각 목록 항목의 값으로 설정 합니다.

[DropDownList에서 범주 필드를 표시 하 고 CategoryID를 값으로 사용 ![](master-detail-filtering-with-two-dropdownlists-cs/_static/image11.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image10.png)

**그림 4**: DropDownList에 `CategoryName` 필드가 표시 되 고 `CategoryID`을 값으로 사용 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image12.png))

이 시점에서 `Categories` 테이블의 레코드로 채워지는 DropDownList 컨트롤 (`Categories`)이 있습니다. 사용자가 DropDownList에서 새 범주를 선택 하는 경우 2 단계에서 만들 제품의 DropDownList을 새로 고치기 위해 다시 게시를 수행 해야 합니다. 따라서 `categories` DropDownList의 스마트 태그에서 Enable AutoPostBack 옵션을 선택 합니다.

[AutoPostBack 범주에 대해를 사용 하도록 설정 합니다. ![](master-detail-filtering-with-two-dropdownlists-cs/_static/image14.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image13.png)

**그림 5**: `Categories` DropDownList에 대해 AutoPostBack 사용 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image15.png))

## <a name="step-2-displaying-the-selected-categorys-products-in-a-second-dropdownlist"></a>2 단계: 두 번째 DropDownList에서 선택한 범주의 제품 표시

`Categories` DropDownList이 완료 되 면 다음 단계는 선택한 범주에 속한 제품의 DropDownList을 표시 하는 것입니다. 이를 수행 하려면 `ProductsByCategory`라는 페이지에 다른 DropDownList을 추가 합니다. `Categories` DropDownList과 마찬가지로 `ProductsByCategoryDataSource`라는 `ProductsByCategory` DropDownList에 대해 새 ObjectDataSource를 만듭니다.

[ProductsByCategory DropDownList에 새 데이터 원본을 추가 ![](master-detail-filtering-with-two-dropdownlists-cs/_static/image17.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image16.png)

**그림 6**: `ProductsByCategory` DropDownList에 대 한 새 데이터 소스 추가 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image18.png))

[ProductsByCategoryDataSource 라는 새 ObjectDataSource를 만들 ![](master-detail-filtering-with-two-dropdownlists-cs/_static/image20.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image19.png)

**그림 7**: 이름이 `ProductsByCategoryDataSource` 새 ObjectDataSource 만들기 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image21.png))

`ProductsByCategory` DropDownList은 선택 된 범주에 속하는 제품만 표시 해야 하므로 ObjectDataSource에서 `ProductsBLL` 개체의 `GetProductsByCategoryID(categoryID)` 메서드를 호출 하도록 합니다.

[![ProductsBLL 클래스를 사용 하도록 선택 합니다.](master-detail-filtering-with-two-dropdownlists-cs/_static/image23.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image22.png)

**그림 8**: `ProductsBLL` 클래스를 사용 하도록 선택 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image24.png))

[GetProductsByCategoryID (categoryID) 메서드를 사용 하도록 ObjectDataSource를 구성 ![](master-detail-filtering-with-two-dropdownlists-cs/_static/image26.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image25.png)

**그림 9**: `GetProductsByCategoryID(categoryID)` 메서드를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image27.png))

마법사의 마지막 단계에서는 *`categoryID`* 매개 변수의 값을 지정 해야 합니다. 이 매개 변수를 `Categories` DropDownList에서 선택한 항목에 할당 합니다.

[범주 DropDownList에서 categoryID 매개 변수 값을 가져올 ![](master-detail-filtering-with-two-dropdownlists-cs/_static/image29.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image28.png)

**그림 10**: `Categories` DropDownList에서 *`categoryID`* 매개 변수 값 가져오기 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image30.png))

ObjectDataSource가 구성 되 면 DropDownList 항목의 표시 및 값에 사용할 데이터 원본 필드를 지정 하는 것만 남았습니다. `ProductName` 필드를 표시 하 고 `ProductID` 필드를 값으로 사용 합니다.

[![DropDownList의 ListItems Text 및 Value 속성에 사용 되는 데이터 원본 필드를 지정 합니다.](master-detail-filtering-with-two-dropdownlists-cs/_static/image32.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image31.png)

**그림 11**: DropDownList의 `ListItem` s ' `Text` 및 `Value` 속성에 사용 되는 데이터 원본 필드 지정 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image33.png))

ObjectDataSource와 `ProductsByCategory` DropDownList이 구성 되 면 페이지에는 두 개의 Dropdownlist 표시 됩니다. 첫 번째는 모든 범주를 나열 하 고 두 번째는 선택한 범주에 속한 제품을 나열 합니다. 사용자가 첫 번째 DropDownList에서 새 범주를 선택 하면 다시 게시가 뒤따르게 두 번째 DropDownList은 새로 선택 된 범주에 속하는 제품을 보여 주는 다시 바인딩 됩니다. 그림 12와 13은 브라우저를 통해 볼 때 작업의 `MasterDetailsDetails.aspx`을 보여 줍니다.

[![페이지를 처음 방문할 때 음료 범주가 선택 됩니다.](master-detail-filtering-with-two-dropdownlists-cs/_static/image35.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image34.png)

**그림 12**: 페이지를 처음 방문할 때 음료 범주가 선택 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image36.png)).

[다른 범주를 선택 ![새 범주의 제품이 표시 됩니다.](master-detail-filtering-with-two-dropdownlists-cs/_static/image38.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image37.png)

**그림 13**: 다른 범주를 선택 하면 새 범주의 제품이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image39.png)).

현재 `productsByCategory` DropDownList이 변경 되 면 포스트백을 발생 시 키 *지 않습니다* . 그러나 선택한 제품의 세부 정보를 표시 하는 DetailsView를 추가 하 고 나면 다시 게시를 수행 해야 합니다 (3 단계). 따라서 `productsByCategory` DropDownList의 스마트 태그에서 AutoPostBack 사용 확인란을 선택 합니다.

[productsByCategory DropDownList에 AutoPostBack 기능을 사용 하도록 설정 ![](master-detail-filtering-with-two-dropdownlists-cs/_static/image41.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image40.png)

**그림 14**: `productsByCategory` DropDownList에 대해 AutoPostBack 기능 사용 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image42.png))

## <a name="step-3-using-a-detailsview-to-display-details-for-the-selected-product"></a>3 단계: DetailsView를 사용 하 여 선택한 제품에 대 한 세부 정보 표시

마지막 단계는 DetailsView에서 선택한 제품에 대 한 세부 정보를 표시 하는 것입니다. 이렇게 하려면 DetailsView을 페이지에 추가 하 고, 해당 `ID` 속성을 `ProductDetails`로 설정 하 고,이에 대 한 새 ObjectDataSource를 만듭니다. *`productID`* 매개 변수의 값에 대해 `ProductsByCategory` DropDownList의 선택 된 값을 사용 하 여 `ProductsBLL` 클래스의 `GetProductByProductID(productID)` 메서드에서 데이터를 가져오도록이 ObjectDataSource를 구성 합니다.

[![ProductsBLL 클래스를 사용 하도록 선택 합니다.](master-detail-filtering-with-two-dropdownlists-cs/_static/image44.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image43.png)

**그림 15**: `ProductsBLL` 클래스를 사용 하도록 선택 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image45.png))

[Getproductid Byproductid (productID) 메서드를 사용 하도록 ObjectDataSource를 구성 ![](master-detail-filtering-with-two-dropdownlists-cs/_static/image47.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image46.png)

**그림 16**: `GetProductByProductID(productID)` 메서드를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image48.png))

[ProductsByCategory DropDownList에서 productID 매개 변수 값을 ![끌어옵니다.](master-detail-filtering-with-two-dropdownlists-cs/_static/image50.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image49.png)

**그림 17**: `ProductsByCategory` DropDownList에서 *`productID`* 매개 변수 값 가져오기 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image51.png))

DetailsView에서 사용 가능한 필드를 표시 하도록 선택할 수 있습니다. `ProductID`, `SupplierID`및 `CategoryID` 필드를 제거 하 고 나머지 필드의 순서를 다시 지정 하 고 서식을 지정 했습니다. 또한 DetailsView의 `Height` 및 `Width` 속성을 지워 DetailsView을 지정 된 크기로 제한 하지 않고 데이터를 가장 잘 표시 하는 데 필요한 너비로 확장할 수 있습니다. 전체 태그는 다음과 같습니다.

[!code-aspx[Main](master-detail-filtering-with-two-dropdownlists-cs/samples/sample1.aspx)]

잠시 시간을 사용 하 여 브라우저에서 `MasterDetailsDetails.aspx` 페이지를 사용해 보세요. 언뜻 보면 모든 것이 원하는 대로 작동 하는 것 처럼 보일 수 있지만 미묘한 문제가 있습니다. 새 범주를 선택 하는 경우 선택 된 범주에 대 한 제품을 포함 하도록 `ProductsByCategory` DropDownList이 업데이트 되지만 `ProductDetails` DetailsView은 이전 제품 정보를 계속 표시 합니다. 선택한 범주에 대해 다른 제품을 선택 하면 DetailsView이 업데이트 됩니다. 또한 철저 하 게 테스트 하는 경우에는 `Categories` DropDownList에서 음료를 선택 하 고 조미료 한 다음 Confections) 다른 모든 범주를 선택 하면 `ProductDetails` DetailsView이 새로 고쳐집니다.

이 문제를 구체화할 수 하는 데 도움이 되도록 특정 예제를 살펴보겠습니다. 페이지를 처음 방문 하면 음료 범주가 선택 되 고 관련 제품이 `ProductsByCategory` DropDownList에 로드 됩니다. Chai는 선택한 제품 이며 해당 세부 정보는 그림 18와 같이 `ProductDetails` DetailsView에 표시 됩니다.

[선택한 제품의 세부 정보가 DetailsView에 표시 ![](master-detail-filtering-with-two-dropdownlists-cs/_static/image53.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image52.png)

**그림 18**: 선택한 제품의 세부 정보는 DetailsView에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image54.png)).

범주 선택을 음료에서 조미료로 변경 하는 경우 다시 게시가 발생 하 고 `ProductsByCategory` DropDownList이 그에 따라 업데이트 되지만 DetailsView에 Chai에 대 한 세부 정보가 표시 됩니다.

[이전에 선택한 제품의 세부 정보가 계속 표시 ![](master-detail-filtering-with-two-dropdownlists-cs/_static/image56.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image55.png)

**그림 19**: 이전에 선택한 제품의 세부 정보는 계속 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image57.png)).

목록에서 새 제품을 선택 하면 DetailsView가 예상 대로 새로 고쳐집니다. 제품을 변경한 후 새 범주를 선택 하면 DetailsView은 새로 고쳐지지 않습니다. 그러나 새 제품을 선택 하는 대신 새 범주를 선택 하는 경우에는 DetailsView이 새로 고쳐집니다. 전 세계에서 무슨 일이 있나요?

이 문제는 페이지 수명 주기의 타이밍 문제입니다. 페이지가 요청 될 때마다 렌더링으로 여러 단계를 진행 합니다. 다음 단계 중 하나에서 ObjectDataSource 컨트롤은 `SelectParameters` 값이 변경 되었는지 확인 합니다. 이 경우 ObjectDataSource에 바인딩된 데이터 웹 컨트롤이 표시를 새로 고쳐야 한다는 것을 알고 있습니다. 예를 들어 새 범주를 선택 하면 `ProductsByCategoryDataSource` ObjectDataSource에서 해당 매개 변수 값이 변경 된 것을 감지 하 고 `ProductsByCategory` DropDownList을 다시 바인딩 하 여 선택한 범주에 대 한 제품을 가져옵니다.

이러한 상황에서 발생 하는 문제는 연결 된 데이터 웹 컨트롤을 다시 바인딩하기 *전에* objectdatasources에서 변경 된 매개 변수를 확인 하는 페이지 수명 주기의 지점이 발생 하는 것입니다. 따라서 새 범주를 선택 하는 경우 `ProductsByCategoryDataSource` ObjectDataSource에서 해당 매개 변수 값의 변경 내용을 검색 합니다. 그러나 `ProductDetails` DetailsView에서 사용 하는 ObjectDataSource는 아직 바인딩 되지 `ProductsByCategory` 않았기 때문에 이러한 변경 내용을 확인 하지 않습니다. 수명 주기 뒷부분에서 `ProductsByCategory` 항목은 ObjectDataSource에 다시 바인딩되어 새로 선택 된 범주에 대 한 제품을 점령 합니다. `ProductsByCategory` DropDownList의 값이 변경 된 경우 `ProductDetails` DetailsView의 ObjectDataSource에서 해당 매개 변수 값 검사를 이미 수행 했습니다. 따라서 DetailsView은 이전 결과를 표시 합니다. 이 상호 작용은 그림 20에 나와 있습니다.

[ProductsByCategory DropDownList 값이 변경 되었는지 확인 합니다. ![](master-detail-filtering-with-two-dropdownlists-cs/_static/image59.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image58.png)

**그림 20**: `ProductDetails` DetailsView의 ObjectDataSource에서 변경 내용을 확인 한 후에 `ProductsByCategory` DropDownList 값이 변경 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image60.png)).

이를 해결 하려면 `ProductsByCategory` DropDownList이 바인딩된 후 `ProductDetails` DetailsView을 명시적으로 다시 바인딩해야 합니다. `ProductsByCategory` DropDownList의 `DataBound` 이벤트가 발생 하는 경우 `ProductDetails` DetailsView의 `DataBind()` 메서드를 호출 하 여이를 수행할 수 있습니다. `MasterDetailsDetails.aspx` 페이지의 코드 숨김이 클래스에 다음 이벤트 처리기 코드를 추가 합니다 (이벤트 처리기를 추가 하는 방법에 대 한 자세한 내용은 "[ObjectDataSource의 매개 변수 값을 프로그래밍 방식으로 설정](../basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)" 참조).

[!code-csharp[Main](master-detail-filtering-with-two-dropdownlists-cs/samples/sample2.cs)]

`ProductDetails` DetailsView의 `DataBind()` 메서드에 대 한이 명시적 호출이 추가 된 후에는 자습서가 정상적으로 작동 합니다. 그림 21은 이러한 변경이 이전 문제를 해결 하는 방법을 강조 표시 합니다.

[ProductsByCategory DropDownList의 데이터 바인딩 이벤트가 발생 하면 제품 세부 정보 DetailsView이 명시적으로 새로 고쳐집니다 ![](master-detail-filtering-with-two-dropdownlists-cs/_static/image62.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image61.png)

**그림 21**: `ProductsByCategory` DropDownList의 `DataBound` 이벤트가 발생 하면 `ProductDetails` DetailsView이 명시적으로 새로 고쳐집니다 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-two-dropdownlists-cs/_static/image63.png)).

## <a name="summary"></a>요약

DropDownList은 마스터/세부 정보 보고서에 대 한 이상적인 사용자 인터페이스 요소로 사용 되며 마스터 및 세부 레코드 간에 일 대 다 관계가 있습니다. 이전 자습서에서는 단일 DropDownList을 사용 하 여 선택 된 범주로 표시 되는 제품을 필터링 하는 방법을 살펴보았습니다. 이 자습서에서는 제품의 GridView를 DropDownList로 바꾸고 DetailsView을 사용 하 여 선택한 제품의 세부 정보를 표시 했습니다. 이 자습서에서 설명 하는 개념은 고객, 주문 및 주문 항목과 같은 다 대 다 관계를 포함 하는 데이터 모델로 쉽게 확장할 수 있습니다. 일반적으로는 일 대 다 관계의 "일" 엔터티 각각에 대 한 DropDownList을 언제 든 지 추가할 수 있습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Hilton Gid Esenow 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](master-detail-filtering-with-a-dropdownlist-cs.md)
> [다음](master-detail-filtering-across-two-pages-cs.md)
