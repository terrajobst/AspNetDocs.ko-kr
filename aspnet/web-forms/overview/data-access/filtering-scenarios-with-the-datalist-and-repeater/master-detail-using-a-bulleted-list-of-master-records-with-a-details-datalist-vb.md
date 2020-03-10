---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb
title: 세부 정보 DataList를 사용 하 여 마스터 레코드의 글머리 기호 목록을 사용 하는 마스터/세부 정보 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 위의 자습서에 대 한 두 페이지 마스터/세부 정보 보고서를 단일 페이지로 압축 하 고, t ...의 범주 이름에 대 한 글머리 기호 목록을 표시 합니다.
ms.author: riande
ms.date: 10/17/2006
ms.assetid: ee20742f-6fb7-49a0-a009-058fe363aacb
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb
msc.type: authoredcontent
ms.openlocfilehash: 81d72c666925e89729464e7ea696bde8d323e277
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78490691"
---
# <a name="masterdetail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb"></a>세부 정보 DataList와 함께 마스터 레코드의 글머리 기호 목록을 사용하는 마스터/세부 정보(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_35_VB.exe) 또는 [PDF 다운로드](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/datatutorial35vb1.pdf)

> 이 자습서에서는 이전 자습서의 두 페이지 마스터/세부 정보 보고서를 단일 페이지로 압축 하 여 화면 왼쪽에 있는 범주 이름의 글머리 기호 목록과 화면 오른쪽에 있는 선택한 범주의 제품을 보여 줍니다.

## <a name="introduction"></a>소개

[이전 자습서](master-detail-filtering-acess-two-pages-datalist-vb.md) 에서는 마스터/세부 보고서를 두 페이지에 분리 하는 방법에 대해 살펴보았습니다. 마스터 페이지에서 Repeater 컨트롤을 사용 하 여 범주의 글머리 기호 목록을 렌더링 했습니다. 각 범주 이름은 클릭 하면 사용자가 세부 정보 페이지로 이동 하는 하이퍼링크입니다. 여기서 두 열 DataList는 선택 된 범주에 속하는 제품을 보여 줍니다.

이 자습서에서는 두 페이지 자습서를 단일 페이지로 압축 하 고, 각 범주 이름이 LinkButton으로 렌더링 된 상태에서 화면 왼쪽에 있는 범주 이름의 글머리 기호 목록을 표시 합니다. 범주 이름 중 하나를 클릭 하면 다시 게시가 Linkbutton 선택한 범주 s 제품이 화면 오른쪽의 두 열 DataList에 바인딩됩니다. 각 범주 이름을 표시 하는 것 외에도 왼쪽의 Repeater에는 지정 된 범주에 대 한 총 제품 수가 표시 됩니다 (그림 1 참조).

[범주 이름 및 제품의 총 수가 왼쪽에 표시 ![](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image2.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image1.png)

**그림 1**: 범주 이름 및 총 제품 수가 왼쪽에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image3.png)).

## <a name="step-1-displaying-a-repeater-in-the-left-portion-of-the-screen"></a>1 단계: 화면의 왼쪽 부분에 리피터 표시

이 자습서의 경우 선택한 범주 제품의 왼쪽에 글머리 기호 목록이 표시 되어야 합니다. 웹 페이지 내의 콘텐츠는 표준 HTML 요소 단락 태그, 구분 되지 않는 공백, `<table>` s 등을 사용 하 여 배치 하거나 CSS (연계 스타일 시트) 기술을 통해 배치할 수 있습니다. 지금까지 모든 자습서에서 CSS 기술을 사용 하 여 위치를 지정 했습니다. [마스터 페이지 및 사이트 탐색](../introduction/master-pages-and-site-navigation-vb.md) 자습서의 마스터 페이지에서 탐색 사용자 인터페이스를 빌드할 때 탐색 목록 및 주요 콘텐츠의 정확한 픽셀 오프셋을 나타내는 *절대 위치 지정*을 사용 했습니다. 또는 CSS를 사용 하 여 한 요소의 오른쪽 이나 왼쪽을 *부동*으로 배치할 수 있습니다. DataList 왼쪽의 Repeater를 부동으로 하 여 선택한 범주 제품의 왼쪽에 범주의 글머리 기호 목록을 표시할 수 있습니다.

`DataListRepeaterFiltering` 폴더에서 `CategoriesAndProducts.aspx` 페이지를 열고 Repeater와 DataList를 페이지에 추가 합니다. Repeater s `ID`를 `Categories`로 설정 하 고 DataList s를 `CategoryProducts`로 설정 합니다. 소스 뷰로 이동 하 여 Repeater 및 DataList 컨트롤을 자체 `<div>` 요소 내에 배치 합니다. 즉, `<div>` 요소 내에 먼저 Repeater를 묶은 다음 Repeater 바로 뒤의 고유한 `<div>` 요소에서 DataList를 묶습니다. 이 시점에서 태그는 다음과 유사 하 게 표시 됩니다.

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample1.aspx)]

DataList의 왼쪽에 있는 반복기를 부동 하려면 다음과 같이 `float` CSS 스타일 특성을 사용 해야 합니다.

[!code-html[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample2.html)]

`float: left;`는 첫 번째 `<div>` 요소를 두 번째 요소 왼쪽으로 부동 합니다. `width` 및 `padding-right` 설정은 첫 번째 `<div>` s `width` 및 `<div>` 요소 내용과 오른쪽 여백 사이에 추가 되는 패딩 크기를 표시 합니다. CSS의 부동 요소에 대 한 자세한 내용은 [Floatutorial](http://css.maxdesign.com.au/floatutorial/)를 확인 하세요.

첫 번째 `<p>` 요소 `style` 특성을 통해 스타일 설정을 직접 지정 하는 대신 `FloatLeft`라는 `Styles.css`에서 새 CSS 클래스를 만들 수 있습니다.

[!code-css[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample3.css)]

그런 다음 `<div>` `<div class="FloatLeft">`으로 바꿀 수 있습니다.

CSS 클래스를 추가 하 고 `CategoriesAndProducts.aspx` 페이지에서 태그를 구성한 후 디자이너로 이동 합니다. DataList의 왼쪽에는 Repeater 부동이 표시 됩니다 (데이터 원본이 나 템플릿을 구성 하는 데 앞서 회색 상자로 표시 됨).

[Repeater가 DataList의 왼쪽에 있는 ![합니다.](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image5.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image4.png)

**그림 2**: Repeater가 DataList의 왼쪽에 표시 되는 경우 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image6.png))

## <a name="step-2-determining-the-number-of-products-for-each-category"></a>2 단계: 각 범주에 대 한 제품 수 결정

Repeater 및 DataList s 주위에 태그가 완료 되 면 범주 데이터를 Repeater 컨트롤에 바인딩할 준비가 된 것입니다. 그러나 그림 1에 나와 있는 범주의 글머리 기호 목록에는 각 범주 이름 뿐만 아니라 범주와 관련 된 제품의 수도 표시 되어야 합니다. 이 정보에 액세스 하려면 다음 중 하나를 수행 합니다.

- **ASP.NET 페이지의 코드 숨김이 클래스에서이 정보를 확인 합니다.** 특정 *`categoryID`* 제공 `ProductsBLL` 클래스 `GetProductsByCategoryID(categoryID)` 메서드를 호출 하 여 연결 된 제품 수를 확인할 수 있습니다. 이 메서드는 지정 된 *`categoryID`* 에 대 한 제품 수에 해당 하는 `ProductsRow`의 수를 나타내는 `Count` 속성이 있는 `ProductsDataTable` 개체를 반환 합니다. Repeater에 바인딩된 각 범주에 대해 `ProductsBLL` 클래스 s `GetProductsByCategoryID(categoryID)` 메서드를 호출 하 고 출력에 개수를 포함 하는 Repeater에 대 한 `ItemDataBound` 이벤트 처리기를 만들 수 있습니다.
- **`NumberOfProducts` 열을 포함 하도록 형식화 된 데이터 집합의 `CategoriesDataTable`을 업데이트 합니다.** 그런 다음이 정보를 포함 하도록 `CategoriesDataTable`에서 `GetCategories()` 메서드를 업데이트 하거나 `GetCategories()` 그대로 두고 `GetCategoriesAndNumberOfProducts()`이라는 새 `CategoriesDataTable` 메서드를 만들 수 있습니다.

이러한 두 가지 방법을 모두 살펴보겠습니다. 첫 번째 방법은 데이터 액세스 계층을 업데이트할 필요가 없기 때문에 구현 하는 것이 더 간단 합니다. 그러나 데이터베이스와의 더 많은 통신이 필요 합니다. `ItemDataBound` 이벤트 처리기의 `ProductsBLL` 클래스 s `GetProductsByCategoryID(categoryID)` 메서드에 대 한 호출은 Repeater에 표시 된 각 범주에 대 한 추가 데이터베이스 호출을 추가 합니다. 이 기법을 사용 하는 경우 *n* + 1 개의 데이터베이스 호출이 있습니다. 여기서 *n* 은 Repeater에 표시 되는 범주 수입니다. 두 번째 방법을 사용 하는 경우 `CategoriesBLL` 클래스 s `GetCategories()` (또는 `GetCategoriesAndNumberOfProducts()`) 메서드의 각 범주에 대 한 정보를 포함 하 여 제품 수를 반환 하므로 데이터베이스에 대해 한 번만 이동 합니다.

## <a name="determining-the-number-of-products-in-the-itemdatabound-event-handler"></a>ItemDataBound 바인딩된 이벤트 처리기의 제품 수 결정

Repeater s `ItemDataBound` 이벤트 처리기의 각 범주에 대 한 제품 수를 결정 하는 데는 기존 데이터 액세스 계층을 수정할 필요가 없습니다. 모든 수정 작업은 `CategoriesAndProducts.aspx` 페이지 내에서 직접 수행할 수 있습니다. 먼저 Repeater s 스마트 태그를 통해 `CategoriesDataSource` 라는 새 ObjectDataSource를 추가 합니다. 그런 다음 `CategoriesBLL` 클래스의 `GetCategories()` 메서드에서 데이터를 검색 하도록 `CategoriesDataSource` ObjectDataSource를 구성 합니다.

[범주 Bll 클래스 s GetCategories () 메서드를 사용 하도록 ObjectDataSource를 구성 ![](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image8.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image7.png)

**그림 3**: `CategoriesBLL` 클래스 s `GetCategories()` 메서드를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image9.png))

`Categories` Repeater의 각 항목을 클릭 하 여 클릭 하 고 클릭 하면 `CategoryProducts` DataList에서 선택한 범주에 해당 하는 제품이 표시 됩니다. 이 작업을 수행 하려면 각 범주를 하이퍼링크로 만들어 동일한 페이지 (`CategoriesAndProducts.aspx`)에 다시 연결 하 고, 이전 자습서에서 살펴본 것 처럼 querystring을 통해 `CategoryID`를 전달 합니다. 이 방법의 장점은 특정 범주를 표시 하는 페이지를 검색 엔진에 의해 책갈피 및 인덱싱할 수 있다는 것입니다.

또는 각 범주를이 자습서에 사용할 LinkButton으로 만들 수 있습니다. LinkButton은 사용자 브라우저에서 하이퍼링크로 렌더링 하지만 클릭 하면 다시 게시를 유도 합니다. 다시 게시 시 선택 된 범주에 속하는 제품을 표시 하려면 DataList s ObjectDataSource를 새로 고쳐야 합니다. 이 자습서에서 하이퍼링크를 사용 하면 LinkButton를 사용 하는 것 보다 더 적합 합니다. 그러나 LinkButton를 사용 하는 것이 더 유용 합니다. 이 예제에서는 하이퍼링크 접근 방식이 이상적 이지만 대신 LinkButton를 사용 하 여 탐색 해 보세요. LinkButton를 사용 하면 하이퍼링크를 사용 하 여 발생 하지 않는 몇 가지 과제가 도입 됩니다. 따라서이 자습서에서는 LinkButton를 사용 하 여 이러한 문제를 강조 하 고, 하이퍼링크 대신 LinkButton을 사용할 수 있는 시나리오에 대 한 솔루션을 제공 합니다.

> [!NOTE]
> LinkButton 대신 HyperLink 컨트롤이 나 `<a>` 요소를 사용 하 여이 자습서를 반복 하는 것이 좋습니다.

다음 태그는 Repeater와 ObjectDataSource의 선언 구문을 보여 줍니다. Repeater s 템플릿은 각 항목을 LinkButton 하 여 글머리 기호 목록을 렌더링 합니다.

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample4.aspx)]

> [!NOTE]
> 이 자습서에서는 Repeater의 뷰 상태를 사용 하도록 설정 해야 합니다 (Repeater의 선언 구문에서 `EnableViewState="False"` 생략). 3 단계에서는 DataList s ObjectDataSource s `SelectParameters` 컬렉션을 업데이트할 Repeater s `ItemCommand` 이벤트에 대 한 이벤트 처리기를 만듭니다. 그러나 뷰 상태가 사용 하지 않도록 설정 된 경우에는 Repeater s `ItemCommand`발생 하지 않습니다. Repeater s `ItemCommand` 이벤트를 발생 시키기 위해 뷰 상태를 사용 하도록 설정 해야 하는 이유에 대 한 자세한 내용은 ASP.NET 질문 및 [해당 솔루션](http://scottonwriting.net/sowBlog/posts/1268.aspx) [의 Stumper을](http://scottonwriting.net/sowblog/posts/1263.aspx) 참조 하세요.

`ID` 속성 값이 `ViewCategory` 인 LinkButton의 `Text` 속성 집합이 없습니다. 범주 이름만 표시 하려는 경우 다음과 같이 데이터 바인딩 구문을 통해 Text 속성을 선언적으로 설정 합니다.

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample5.aspx)]

그러나 범주 이름과 해당 범주에 속하는 제품 *수를 모두* 표시 하려고 합니다. 다음 코드에 나와 있는 것 처럼 `ProductBLL` 클래스 s `GetCategoriesByProductID(categoryID)` 메서드를 호출 하 고 결과 `ProductsDataTable`에서 반환 되는 레코드 수를 결정 하 여이 정보를 Repeater s `ItemDataBound` 이벤트 처리기에서 검색할 수 있습니다.

[!code-vb[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample6.vb)]

먼저 데이터 항목 (`ItemType` `Item` 또는 `AlternatingItem`)을 사용 하 여 작업을 다시 수행 하 고 현재 `RepeaterItem`에 방금 바인딩된 `CategoriesRow` 인스턴스를 참조 하는 것을 확인 합니다. 다음으로 `ProductsBLL` 클래스의 인스턴스를 만들고 해당 `GetCategoriesByProductID(categoryID)` 메서드를 호출 하 고 `Count` 속성을 사용 하 여 반환 되는 레코드 수를 확인 하 여이 범주에 대 한 제품 수를 결정 합니다. 마지막으로 ItemTemplate의 `ViewCategory` LinkButton는 참조이 고 해당 `Text` 속성은 *범주* (*numberofproductsincategory*)로 설정 됩니다. 여기서 *numberofproductsincategory* 는 소수 자릿수가 0 인 숫자로 서식 지정 됩니다.

> [!NOTE]
> 또는 `CategoryName` 범주를 수락 하 고 `CategoryID` 값을 사용 하 고 `GetCategoriesByProductID(categoryID)` 메서드를 호출 하 여 확인 된 대로 범주의 제품 수와 연결 된 `CategoryName`을 반환 하는 ASP.NET 페이지의 코드를 만든 클래스에 *서식 함수* 를 추가 했을 수 있습니다. 이러한 형식 지정 함수의 결과는 `ItemDataBound` 이벤트 처리기에 대 한 필요성을 대체 하는 LinkButton s Text 속성에 선언적으로 할당 될 수 있습니다. 서식 지정 함수를 사용 하는 방법에 대 한 자세한 내용은 [GridView 컨트롤의 템플릿 사용 필드](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md) 또는 [데이터에 따라 DataList 및 Repeater 서식 지정](../displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-vb.md) 자습서를 참조 하세요.

이 이벤트 처리기를 추가한 후 잠시 시간을 내 서 브라우저를 통해 페이지를 테스트 합니다. 각 범주가 글머리 기호 목록에 나열 되 고 범주 이름과 연결 된 제품의 수와 범주를 표시 하는 방법을 확인 합니다 (그림 4 참조).

[![각 범주 이름 및 제품 수가 표시 됩니다.](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image11.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image10.png)

**그림 4**: 각 범주 이름과 제품 수가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image12.png)).

## <a name="updating-thecategoriesdatatableandcategoriestableadapterto-include-the-number-of-products-for-each-category"></a>각 범주에 대 한 제품 수를 포함 하도록`CategoriesDataTable`및`CategoriesTableAdapter`업데이트

각 범주에 대 한 제품 수를 Repeater에 바인딩하여 결정 하는 대신이 정보를 기본적으로 포함 하도록 데이터 액세스 계층의 `CategoriesDataTable` 및 `CategoriesTableAdapter`를 조정 하 여이 프로세스를 간소화할 수 있습니다. 이를 위해 `CategoriesDataTable` 새 열을 추가 하 여 연결 된 제품 수를 유지 해야 합니다. DataTable에 새 열을 추가 하려면 형식화 된 데이터 집합 (`App_Code\DAL\Northwind.xsd`)을 열고 수정할 DataTable을 마우스 오른쪽 단추로 클릭 한 다음 추가/열을 선택 합니다. `CategoriesDataTable`에 새 열을 추가 합니다 (그림 5 참조).

[범주 데이터 원본에 새 열을 추가 ![](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image14.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image13.png)

**그림 5**: `CategoriesDataSource`에 새 열 추가 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image15.png))

이렇게 하면 이름이 `Column1`새 열이 추가 됩니다 .이 열은 다른 이름을 입력 하기만 하면 변경할 수 있습니다. 새 열의 이름을 `NumberOfProducts`로 바꿉니다. 다음으로이 열의 속성을 구성 해야 합니다. 새 열을 클릭 하 고 속성 창로 이동 합니다. 그림 6에 표시 된 것 처럼 `System.String`의 열 `DataType` 속성을 `System.Int32`으로 변경 하 고 `ReadOnly` 속성을 `True`로 설정 합니다.

![새 열의 데이터 형식 및 ReadOnly 속성 설정](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image16.png)

**그림 6**: 새 열의 `DataType` 및 `ReadOnly` 속성 설정

이제 `CategoriesDataTable`에 `NumberOfProducts` 열이 있지만 해당 값은 해당 하는 TableAdapter s 쿼리로 설정 되지 않습니다. 범주 정보를 검색할 때마다 이러한 정보를 반환 하려는 경우 `GetCategories()` 메서드를 업데이트 하 여이 정보를 반환할 수 있습니다. 그러나 드문 경우에만 (예:이 자습서의 경우 처럼) 관련 제품의 수를 지정 해야 하는 경우에는 `GetCategories()` 그대로 두고이 정보를 반환 하는 새 메서드를 만들 수 있습니다. 에서는이 두 가지 방법을 사용 하 여 `GetCategoriesAndNumberOfProducts()`라는 새 메서드를 만듭니다.

이 새 `GetCategoriesAndNumberOfProducts()` 메서드를 추가 하려면 `CategoriesTableAdapter`을 마우스 오른쪽 단추로 클릭 하 고 새 쿼리를 선택 합니다. 그러면 이전 자습서에서 여러 번 사용한 TableAdapter 쿼리 구성 마법사가 나타납니다. 이 방법에서는 쿼리가 행을 반환 하는 임시 SQL 문을 사용 하도록 하 여 마법사를 시작 합니다.

[임시 SQL 문을 사용 하 여 메서드를 ![만듭니다.](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image18.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image17.png)

**그림 7**: 임시 SQL 문을 사용 하 여 메서드 만들기 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image19.png))

[SQL 문이 행을 반환 ![](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image21.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image20.png)

**그림 8**: SQL 문이 행을 반환 합니다 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image22.png)).

다음 마법사 화면에서 사용할 쿼리를 묻는 메시지를 표시 합니다. 범주와 연결 된 제품 수와 함께 각 범주 `CategoryID`, `CategoryName`및 `Description` 필드를 반환 하려면 다음 `SELECT` 문을 사용 합니다.

[!code-sql[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample7.sql)]

[사용할 쿼리를 지정 ![](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image24.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image23.png)

**그림 9**: 사용할 쿼리 지정 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image25.png))

범주와 관련 된 제품 수를 계산 하는 하위 쿼리는 `NumberOfProducts`로 별칭이 지정 됩니다. 이 명명 일치는이 하위 쿼리에서 반환 되는 값이 `CategoriesDataTable` s `NumberOfProducts` 열과 연결 되도록 합니다.

이 쿼리를 입력 한 후 마지막 단계는 새 메서드의 이름을 선택 하는 것입니다. `FillWithNumberOfProducts` 및 `GetCategoriesAndNumberOfProducts`를 사용 하 여 DataTable을 채우고 DataTable 패턴을 반환 합니다.

[![새 TableAdapter의 메서드 이름으로 Numberofproducts 및 Get범주 Andnumberofproducts를 Fill.](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image27.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image26.png)

**그림 10**: 새 TableAdapter의 메서드 이름 `FillWithNumberOfProducts` 및 `GetCategoriesAndNumberOfProducts` ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image28.png))

이 시점에서 데이터 액세스 계층은 범주별 제품 수를 포함 하도록 확장 되었습니다. 모든 프레젠테이션 계층은 별도의 비즈니스 논리 계층을 통해 DAL에 대 한 모든 호출을 라우트 하므로 해당 하는 `GetCategoriesAndNumberOfProducts` 메서드를 `CategoriesBLL` 클래스에 추가 해야 합니다.

[!code-vb[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample8.vb)]

DAL 및 BLL이 완료 되 면이 데이터를 `CategoriesAndProducts.aspx`의 `Categories` Repeater에 바인딩할 준비가 되었습니다. `ItemDataBound` 이벤트 처리기 섹션의 제품 수 결정에서 Repeater에 대해 ObjectDataSource를 이미 만든 경우이 ObjectDataSource를 삭제 하 고 Repeater s `DataSourceID` 속성 설정을 제거 합니다. 또한 ASP.NET 코드 지향 클래스에서 `Handles Categories.OnItemDataBound` 구문을 제거 하 여 이벤트 처리기에서 Repeater s `ItemDataBound` 이벤트를 연결 해제 합니다.

원래 상태로 Repeater를 다시 사용 하 여 Repeater 스마트 태그를 통해 `CategoriesDataSource` 라는 새 ObjectDataSource를 추가 합니다. `CategoriesBLL` 클래스를 사용 하도록 ObjectDataSource를 구성 하지만 `GetCategories()` 메서드를 사용 하는 대신 `GetCategoriesAndNumberOfProducts()`를 대신 사용 하도록 합니다 (그림 11 참조).

[Get범주 Andnumberofproducts 메서드를 사용 하도록 ObjectDataSource를 구성 ![](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image30.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image29.png)

**그림 11**: `GetCategoriesAndNumberOfProducts` 메서드를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image31.png))

그런 다음 LinkButton s `Text` 속성이 데이터 바인딩 구문을 사용 하 여 선언적으로 할당 되 고 `CategoryName` 및 `NumberOfProducts` 데이터 필드를 모두 포함 하도록 `ItemTemplate`를 업데이트 합니다. Repeater 및 `CategoriesDataSource` ObjectDataSource의 전체 선언적 태그는 다음과 같습니다.

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample9.aspx)]

`NumberOfProducts` 열을 포함 하도록 DAL을 업데이트 하 여 렌더링 되는 출력은 `ItemDataBound` 이벤트 처리기 접근 방법을 사용 하는 것과 같습니다 (범주 이름과 제품 수를 표시 하는 리피터의 스크린샷 확인).

## <a name="step-3-displaying-the-selected-category-s-products"></a>3 단계: 선택한 범주 제품 표시

이 시점에서 범주 목록과 각 범주의 제품 수를 표시 하는 `Categories` 리피터가 있습니다. Repeater는 클릭 하면 다시 게시를 발생 시키는 각 범주에 대해 LinkButton를 사용 합니다 .이 경우에는 `CategoryProducts` DataList에서 선택한 범주에 해당 하는 제품을 표시 해야 합니다.

한 가지 문제는 DataList에 선택한 범주에 해당 하는 제품만 표시 하는 방법입니다. [세부 정보 DetailsView 자습서에서 선택 가능한 마스터 GridView를 사용 하는 마스터/세부](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md) 정보에서 행을 선택할 수 있는 GridView를 빌드하는 방법 및 선택한 행의 세부 정보가 동일한 페이지의 DetailsView에 표시 되는 방법을 살펴보았습니다. GridView s objectdatasource는 `ProductsBLL` s `GetProducts()` 메서드를 사용 하는 모든 제품에 대 한 정보를 반환 하 고, DetailsView s ObjectDataSource는 `GetProductsByProductID(productID)` 메서드를 사용 하 여 선택한 제품에 대 한 정보를 검색 했습니다. *`productID`* 매개 변수 값은 GridView s `SelectedValue` 속성의 값과 연결 하 여 선언적으로 제공 됩니다. 그러나 Repeater에는 `SelectedValue` 속성이 없으며 매개 변수 소스로 사용할 수 없습니다.

> [!NOTE]
> 이는 LinkButton를 Repeater에서 사용할 때 표시 되는 문제 중 하나입니다. 대신 쿼리를 사용 하 여 `CategoryID`를 전달 하는 하이퍼링크를 사용 했 고 해당 QueryString 필드를 매개 변수 값의 원본으로 사용할 수 있습니다.

그러나 Repeater에 대 한 `SelectedValue` 속성이 없다는 것을 걱정 하기 전에는 먼저 DataList에 DataList를 바인딩하고 해당 `ItemTemplate`를 지정 합니다.

DataList s 스마트 태그에서 `CategoryProductsDataSource` 라는 새 ObjectDataSource를 추가 하 고 `ProductsBLL` 클래스 s `GetProductsByCategoryID(categoryID)` 메서드를 사용 하도록 구성 합니다. 이 자습서의 DataList는 읽기 전용 인터페이스를 제공 하므로 삽입, 업데이트 및 삭제 탭의 드롭다운 목록을 (없음)으로 자유롭게 설정 합니다.

[ProductsBLL 클래스 s GetProductsByCategoryID (categoryID) 메서드를 사용 하도록 ObjectDataSource 구성 ![](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image33.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image32.png)

**그림 12**: `ProductsBLL` 클래스 `GetProductsByCategoryID(categoryID)` 메서드를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image34.png))

`GetProductsByCategoryID(categoryID)` 메서드에 입력 매개 변수 ( *`categoryID`* )가 필요 하기 때문에 데이터 소스 구성 마법사를 사용 하 여 매개 변수 원본을 지정할 수 있습니다. GridView 또는 DataList에 범주가 나열 되어 있으면 매개 변수 소스 드롭다운 목록을 제어 하 고 ControlID를 데이터 웹 컨트롤의 `ID`로 설정 합니다. 그러나 Repeater에는 `SelectedValue` 속성이 없으므로 매개 변수 소스로 사용할 수 없습니다. 확인 하는 경우에는 ControlID 드롭다운 목록에 DataList의 `ID` 인 컨트롤 `ID``CategoryProducts`하나만 포함 되어 있는 것을 확인할 수 있습니다.

지금은 매개 변수 원본 드롭다운 목록을 None으로 설정 합니다. LinkButton 범주를 Repeater에서 클릭 하는 경우이 매개 변수 값을 프로그래밍 방식으로 할당 합니다.

[categoryID 매개 변수에 대 한 매개 변수 원본을 지정 하지 ![](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image36.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image35.png)

**그림 13**: *`categoryID`* 매개 변수에 대 한 매개 변수 원본을 지정 하지 않음 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image37.png))

데이터 소스 구성 마법사를 완료 한 후 Visual Studio에서 DataList s `ItemTemplate`자동으로 생성 합니다. 이 기본 `ItemTemplate`를 앞의 자습서에서 사용한 템플릿으로 바꿉니다. 또한 DataList s `RepeatColumns` 속성을 2로 설정 합니다. 이러한 변경을 수행한 후 DataList의 선언 태그와 연결 된 ObjectDataSource는 다음과 같습니다.

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample10.aspx)]

현재 `CategoryProductsDataSource` ObjectDataSource s *`categoryID`* 매개 변수는 설정 되지 않으므로 페이지를 볼 때 제품이 표시 되지 않습니다. 이 매개 변수 값은 Repeater에서 클릭 한 범주의 `CategoryID`를 기준으로 설정 해야 합니다. 여기에는 두 가지 과제가 있습니다. 첫 번째는 `ItemTemplate` Repeater s에서 LinkButton이 클릭 된 시기를 결정 하는 방법입니다. 둘째, LinkButton을 클릭 한 해당 범주의 `CategoryID`를 어떻게 확인할 수 있나요?

Button 및 ImageButton 컨트롤과 같은 LinkButton는 `Click` 이벤트와 [`Command` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.command.aspx)를 포함 합니다. `Click` 이벤트는 LinkButton를 클릭 했는지만 확인 하도록 디자인 되었습니다. 그러나 경우에 따라 LinkButton를 클릭 했음을 알리는 것 외에도 이벤트 처리기에 몇 가지 추가 정보를 전달 해야 합니다. 이 경우 LinkButton s [`CommandName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.commandname.aspx) 및 [`CommandArgument`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.commandargument.aspx) 속성에이 추가 정보를 할당할 수 있습니다. 그런 다음 LinkButton를 클릭 하면 해당 `Command` 이벤트가 발생 하 고 (`Click` 이벤트 대신) 이벤트 처리기에 `CommandName` 및 `CommandArgument` 속성의 값이 전달 됩니다.

Repeater의 템플릿 내에서 `Command` 이벤트가 발생 하면 Repeater s [`ItemCommand` 이벤트가](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeater.itemcommand.aspx) 발생 하 고 `CommandName` `CommandArgument` 클릭 한 LinkButton (또는 단추 또는 ImageButton)의 값이 전달 됩니다. 따라서 Repeater에서 LinkButton 범주가 클릭 된 시기를 확인 하려면 다음을 수행 해야 합니다.

1. Repeater s `ItemTemplate`에 있는 LinkButton의 `CommandName` 속성을 일부 값 (ListProducts를 사용 함)으로 설정 합니다. 이 `CommandName` 값을 설정 하 여 LinkButton를 클릭 하면 LinkButton s `Command` 이벤트가 발생 합니다.
2. LinkButton s `CommandArgument` 속성을 현재 항목의 `CategoryID`값으로 설정 합니다.
3. Repeater s `ItemCommand` 이벤트에 대 한 이벤트 처리기를 만듭니다. 이벤트 처리기에서 `CategoryProductsDataSource` ObjectDataSource s `CategoryID` 매개 변수를 전달 된 `CommandArgument`의 값으로 설정 합니다.

범주 Repeater에 대 한 다음 `ItemTemplate` 태그는 1 및 2 단계를 구현 합니다. 데이터 바인딩 구문을 사용 하 여 `CategoryID` 데이터 항목에 `CommandArgument` 값이 할당 되는 방식을 확인 합니다.

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample11.aspx)]

`ItemCommand` 이벤트 처리기를 만들 때마다 먼저 들어오는 `CommandName` 값을 확인 하는 것이 좋습니다. Repeater 내에서 Button, LinkButton 또는 *ImageButton에 의해* 발생 하는 *모든* `Command` 이벤트는 `ItemCommand` 이벤트가 발생 하기 때문입니다. 현재 이러한 LinkButton 한 개만 있으므로 나중에 (또는 팀의 다른 개발자), 클릭 하면 동일한 `ItemCommand` 이벤트 처리기가 발생 하는 추가 단추 웹 컨트롤을 Repeater에 추가할 수 있습니다. 따라서 `CommandName` 속성을 확인 하 고 예상 되는 값과 일치 하는 경우에만 프로그래밍 논리를 처리 하는 것이 가장 좋습니다.

전달 된 `CommandName` 값이 ListProducts와 일치 하는지 확인 한 후 이벤트 처리기는 `CategoryProductsDataSource` ObjectDataSource s `CategoryID` 매개 변수를 전달 된 `CommandArgument`값에 할당 합니다. ObjectDataSource s `SelectParameters` 수정 하면 자동으로 DataList가 데이터 원본에 다시 바인딩하고 새로 선택한 범주에 대 한 제품이 표시 됩니다.

[!code-vb[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample12.vb)]

이러한 추가 기능을 사용 하면 자습서를 완료할 수 있습니다. 잠시 시간을 내 서 브라우저에서 테스트 하세요. 그림 14는 페이지를 처음 방문할 때의 화면을 보여 줍니다. 범주는 아직 선택 하지 않았으므로 제품이 표시 되지 않습니다. 생성 등의 범주를 클릭 하면 두 열 보기로 제품 범주의 해당 제품이 표시 됩니다 (그림 15 참조).

[페이지를 처음 방문할 때 제품이 표시 되지 ![](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image39.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image38.png)

**그림 14**: 페이지를 처음 방문할 때 제품이 표시 되지 않음 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image40.png))

[생성 범주를 클릭 ![오른쪽에 일치 하는 제품이 나열 됩니다.](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image42.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image41.png)

**그림 15**: 생성 범주를 클릭 하면 오른쪽에 일치 하는 제품이 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image43.png)).

## <a name="summary"></a>요약

이 자습서에서 보았듯이 앞에서 설명한 것 처럼 마스터/세부 정보 보고서를 두 페이지에 분산 하거나 하나에 통합할 수 있습니다. 그러나 마스터/세부 정보 보고서를 단일 페이지에 표시 하면 페이지에서 마스터 및 세부 정보 레코드를 레이아웃 하는 데 가장 적합 한 몇 가지 과제가 발생 합니다. *세부 정보 DetailsView 자습서에서 선택 가능한 마스터 GridView를 사용 하는 마스터/세부* 정보 레코드가 마스터 레코드 위에 표시 됩니다. 이 자습서에서는 CSS 기술을 사용 하 여 마스터 레코드를 세부 정보 왼쪽으로 부동으로 만들었습니다.

마스터/세부 정보 보고서를 표시 하는 것과 함께, 각 범주와 관련 된 제품 수를 검색 하는 방법 뿐만 아니라 Repeater 내에서 LinkButton (또는 단추 또는 ImageButton)를 클릭할 때 서버측 논리를 수행 하는 방법도 살펴보았습니다.

이 자습서에서는 DataList 및 Repeater를 사용 하 여 마스터/세부 정보 보고서에 대 한 검사를 완료 합니다. 다음 자습서 집합에서는 편집 및 삭제 기능을 DataList 컨트롤에 추가 하는 방법을 보여 줍니다.

행복 한 프로그래밍

## <a name="further-reading"></a>추가 참고 자료

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- CSS를 사용 하 여 부동 CSS 요소에 대 한 자습서 [Floatutorial](http://css.maxdesign.com.au/floatutorial/)
- Css를 사용 하 여 요소를 배치 하는 방법에 대 한 [Css 위치 지정](http://www.brainjar.com/css/positioning/)
- `<table>` s와 다른 HTML 요소를 사용 하 여 콘텐츠를 배치 하도록 [html로 콘텐츠 레이아웃](http://www.w3schools.com/html/html_layout.asp)

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Zack Jones 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](master-detail-filtering-acess-two-pages-datalist-vb.md)
