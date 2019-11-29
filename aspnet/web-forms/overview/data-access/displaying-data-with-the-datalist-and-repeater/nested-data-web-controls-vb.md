---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/nested-data-web-controls-vb
title: 중첩 된 데이터 웹 컨트롤 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 다른 리피터 안에 중첩 된 리피터를 사용 하는 방법을 살펴봅니다. 이 예에서는 내부 반복기를 모두 채우는 방법을 보여 줍니다.
ms.author: riande
ms.date: 09/13/2006
ms.assetid: 8b7fcf7b-722b-498d-a4e4-7c93701e0c95
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/nested-data-web-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: c3c62ce4293498d3b325031ac9817f8935b183b2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74629552"
---
# <a name="nested-data-web-controls-vb"></a>중첩된 데이터 웹 컨트롤(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_32_VB.exe) 또는 [PDF 다운로드](nested-data-web-controls-vb/_static/datatutorial32vb1.pdf)

> 이 자습서에서는 다른 리피터 안에 중첩 된 리피터를 사용 하는 방법을 살펴봅니다. 이 예제에서는 내부 반복기를 선언적으로 프로그래밍 방식으로 채우는 방법을 보여 줍니다.

## <a name="introduction"></a>소개

정적 HTML 및 데이터 바인딩 구문 외에도 템플릿에서는 웹 컨트롤 및 사용자 정의 컨트롤을 포함할 수 있습니다. 이러한 웹 컨트롤은 선언적, 데이터 바인딩 구문을 통해 할당 된 속성을 포함 하거나 적절 한 서버 쪽 이벤트 처리기에서 프로그래밍 방식으로 액세스할 수 있습니다.

템플릿 내에 컨트롤을 포함 하면 모양과 사용자 환경을 사용자 지정 하 고에 맞게 개선할 수 있습니다. 예를 들어 [Gridview 컨트롤의 템플릿 필드 사용](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md) 자습서에서는 직원 채용 날짜를 표시 하는 일정 컨트롤을 templatefield로 변환에 추가 하 여 GridView s 표시를 사용자 지정 하는 방법을 살펴보았습니다. [편집 및 삽입 인터페이스에 유효성 검사 컨트롤 추가](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md) 및 [데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) 자습서에서는 유효성 검사 컨트롤, 텍스트 상자, dropdownlist 및 기타 웹 컨트롤을 추가 하 여 편집 및 삽입 인터페이스를 사용자 지정 하는 방법을 살펴보았습니다.

템플릿에 다른 데이터 웹 컨트롤이 포함 될 수도 있습니다. 즉, 해당 템플릿 내에서 다른 DataList (또는 Repeater, GridView 또는 DetailsView 등)를 포함 하는 DataList를 사용할 수 있습니다. 이러한 인터페이스의 문제는 적절 한 데이터를 내부 데이터 웹 컨트롤에 바인딩하는 것입니다. ObjectDataSource를 사용 하는 선언적 옵션에서 프로그래밍 방식으로 사용할 수 있는 몇 가지 방법이 있습니다.

이 자습서에서는 다른 리피터 안에 중첩 된 리피터를 사용 하는 방법을 살펴봅니다. 외부 Repeater는 범주 이름과 설명을 표시 하는 데이터베이스의 각 범주에 대 한 항목을 포함 합니다. 각 범주 항목의 내부 리피터는 글머리 기호 목록에서 해당 범주에 속하는 각 제품에 대 한 정보를 표시 합니다 (그림 1 참조). 이 예제에서는 내부 반복기를 선언적으로 프로그래밍 방식으로 채우는 방법을 보여 줍니다.

[각 범주와 제품과 함께 ![나열 됩니다.](nested-data-web-controls-vb/_static/image2.png)](nested-data-web-controls-vb/_static/image1.png)

**그림 1**: 각 범주 (제품 포함)가 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](nested-data-web-controls-vb/_static/image3.png)).

## <a name="step-1-creating-the-category-listing"></a>1 단계: 범주 목록 만들기

중첩 된 데이터 웹 컨트롤을 사용 하는 페이지를 만들 때 내부 중첩 된 컨트롤에 대해 걱정 하지 않고 가장 바깥쪽 데이터 웹 컨트롤을 먼저 디자인, 작성 및 테스트 하는 것이 좋습니다. 따라서 각 범주에 대 한 이름 및 설명을 나열 하는 페이지에 리피터를 추가 하는 데 필요한 단계를 시작 하겠습니다.

먼저 `DataListRepeaterBasics` 폴더에서 `NestedControls.aspx` 페이지를 열고 `ID` 속성을 `CategoryList`로 설정 하 여 Repeater 컨트롤을 페이지에 추가 합니다. Repeater s 스마트 태그에서 `CategoriesDataSource`라는 새 ObjectDataSource를 만들도록 선택 합니다.

[새 ObjectDataSource 범주 Datasource의 이름을 ![합니다.](nested-data-web-controls-vb/_static/image5.png)](nested-data-web-controls-vb/_static/image4.png)

**그림 2**: 새 ObjectDataSource `CategoriesDataSource` 이름 ([전체 크기 이미지를 보려면 클릭](nested-data-web-controls-vb/_static/image6.png))

`CategoriesBLL` 클래스 s `GetCategories` 메서드에서 데이터를 끌어올 수 있도록 ObjectDataSource를 구성 합니다.

[범주 Bll 클래스 GetCategories 메서드를 사용 하도록 ObjectDataSource를 구성 ![](nested-data-web-controls-vb/_static/image8.png)](nested-data-web-controls-vb/_static/image7.png)

**그림 3**: `CategoriesBLL` 클래스 s `GetCategories` 메서드를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](nested-data-web-controls-vb/_static/image9.png))

반복기의 템플릿 콘텐츠를 지정 하려면 소스 뷰로 이동 하 여 선언적 구문을 수동으로 입력 해야 합니다. `<h4>` 요소에 범주 이름을 표시 하는 `ItemTemplate`을 추가 하 고 단락 요소 (`<p>`)에 범주에 대 한 설명을 표시 합니다. 또한 각 범주를 가로 규칙 (`<hr>`)으로 구분 합니다. 이러한 변경을 수행한 후에는 페이지에 다음과 유사한 Repeater와 ObjectDataSource에 대 한 선언 구문이 포함 되어야 합니다.

[!code-aspx[Main](nested-data-web-controls-vb/samples/sample1.aspx)]

그림 4는 브라우저를 통해 볼 때의 진행률을 보여 줍니다.

[각 범주 이름 및 설명이 나열 되어 ![수평선 규칙으로 구분 됩니다.](nested-data-web-controls-vb/_static/image11.png)](nested-data-web-controls-vb/_static/image10.png)

**그림 4**: 각 범주 이름 및 설명이 가로 규칙에 따라 구분 되어 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](nested-data-web-controls-vb/_static/image12.png)).

## <a name="step-2-adding-the-nested-product-repeater"></a>2 단계: 중첩 된 제품 리피터 추가

범주 목록이 완료 되 면 다음 작업은 해당 범주에 속하는 제품에 대 한 정보를 표시 하는 `CategoryList` s `ItemTemplate`에 대 한 Repeater를 추가 하는 것입니다. 이 내부 리피터의 데이터를 검색할 수 있는 여러 가지 방법이 있으며,이 중 두 가지는 곧 살펴볼 것입니다. 지금은 `CategoryList` Repeater s `ItemTemplate`내에서 제품 리피터를 만들어 보겠습니다. 특히 제품의 이름과 가격을 포함 하 여 각 목록 항목을 포함 하는 제품 리피터가 각 제품을 글머리 기호 목록에 표시 하도록 합니다.

이 반복을 만들려면 `CategoryList` s `ItemTemplate`에 내부 Repeater s 선언적 구문 및 템플릿을 수동으로 입력 해야 합니다. `CategoryList` Repeater s `ItemTemplate`안에 다음 태그를 추가 합니다.

[!code-aspx[Main](nested-data-web-controls-vb/samples/sample2.aspx)]

## <a name="step-3-binding-the-category-specific-products-to-the-productsbycategorylist-repeater"></a>3 단계: ProductsByCategoryList Repeater에 범주 관련 제품 바인딩

이 시점에서 브라우저를 통해 페이지를 방문 하는 경우에는 데이터를 Repeater에 바인딩하지 못했기 때문에 화면이 그림 4와 동일 하 게 보입니다. 적절 한 제품 레코드를 찾아 Repeater에 바인딩할 수 있는 몇 가지 방법이 있습니다. 다른 방법 보다 더 효율적입니다. 여기서 가장 중요 한 문제는 지정 된 범주에 대 한 적절 한 제품을 다시 가져오는 것입니다.

내부 Repeater 컨트롤에 바인딩할 데이터는 `CategoryList` Repeater s `ItemTemplate`의 ObjectDataSource를 통해 또는 프로그래밍 방식으로 ASP.NET 페이지의 코드 숨김이 페이지에서 액세스할 수 있습니다. 마찬가지로,이 데이터는 내부 반복에서 `DataSourceID` 선언적으로 또는 선언적 데이터 바인딩 구문을 통해 또는 선언적으로 `CategoryList` Repeater s `ItemDataBound` 이벤트 처리기에서 내부 반복기를 참조 하 고 프로그래밍 방식으로 `DataSource` 속성을 설정 하 고 해당 `DataBind()` 메서드를 호출 하 여 프로그래밍 방식으로 내부 Repeater에 바인딩될 수 있습니다. 이러한 각 방법을 살펴보겠습니다.

## <a name="accessing-the-data-declaratively-with-an-objectdatasource-control-and-theitemdataboundevent-handler"></a>ObjectDataSource 컨트롤과`ItemDataBound`이벤트 처리기를 사용 하 여 선언적으로 데이터 액세스

이 자습서 시리즈를 통해 ObjectDataSource를 광범위 하 게 사용 했기 때문에이 예제에서 데이터에 액세스 하는 가장 일반적인 선택은 ObjectDataSource를 사용 하는 것입니다. `ProductsBLL` 클래스에는 지정 된 *`categoryID`* 에 속하는 해당 제품에 대 한 정보를 반환 하는 `GetProductsByCategoryID(categoryID)` 메서드가 있습니다. 따라서 `CategoryList` Repeater s `ItemTemplate`에 ObjectDataSource를 추가 하 고이 클래스의 메서드를 사용 하 여 데이터에 액세스 하도록 구성할 수 있습니다.

아쉽게도 반복기는 디자인 뷰를 통해 해당 템플릿을 편집할 수 없도록 하므로이 ObjectDataSource 컨트롤의 선언 구문을 직접 추가 해야 합니다. 다음 구문에서는이 새 ObjectDataSource (`ProductsByCategoryDataSource`)를 추가한 후 `CategoryList` Repeater s `ItemTemplate`를 보여 줍니다.

[!code-aspx[Main](nested-data-web-controls-vb/samples/sample3.aspx)]

ObjectDataSource 방법을 사용 하는 경우 `ProductsByCategoryList` Repeater s `DataSourceID` 속성을 ObjectDataSource의 `ID` (`ProductsByCategoryDataSource`)로 설정 해야 합니다. 또한 ObjectDataSource에는 `GetProductsByCategoryID(categoryID)` 메서드에 전달 되는 *`categoryID`* 값을 지정 하는 `<asp:Parameter>` 요소가 있습니다. 그러나이 값을 지정 하는 방법은 무엇입니까? 이상적으로는 다음과 같이 데이터 바인딩 구문을 사용 하 여 `<asp:Parameter>` 요소의 `DefaultValue` 속성을 설정할 수 있습니다.

[!code-aspx[Main](nested-data-web-controls-vb/samples/sample4.aspx)]

아쉽게도 데이터 바인딩 구문은 `DataBinding` 이벤트를 포함 하는 컨트롤 에서만 유효 합니다. `Parameter` 클래스는 이러한 이벤트를 사용할 수 없으므로 위의 구문이 잘못 되어 런타임 오류가 발생 합니다.

이 값을 설정 하려면 `CategoryList` Repeater s `ItemDataBound` 이벤트에 대 한 이벤트 처리기를 만들어야 합니다. `ItemDataBound` 이벤트는 Repeater에 바인딩된 각 항목에 대해 한 번씩 발생 한다는 것을 기억 하세요. 따라서 외부 Repeater에 대해이 이벤트가 발생 될 때마다 현재 `CategoryID` 값을 `ProductsByCategoryDataSource` ObjectDataSource s `CategoryID` 매개 변수에 할당할 수 있습니다.

다음 코드를 사용 하 여 `CategoryList` Repeater s `ItemDataBound` 이벤트에 대 한 이벤트 처리기를 만듭니다.

[!code-vb[Main](nested-data-web-controls-vb/samples/sample5.vb)]

이 이벤트 처리기는 머리글, 바닥글 또는 구분 기호 항목이 아닌 데이터 항목을 다시 처리 하 여 시작 합니다. 다음으로 현재 `RepeaterItem`에 바인딩된 실제 `CategoriesRow` 인스턴스를 참조 합니다. 마지막으로 `ItemTemplate`에서 ObjectDataSource를 참조 하 고 현재 `RepeaterItem`의 `CategoryID`에 `CategoryID` 매개 변수 값을 할당 합니다.

이 이벤트 처리기를 사용 하 여 각 `RepeaterItem`의 `ProductsByCategoryList` Repeater는 `RepeaterItem` s 범주의 해당 제품에 바인딩됩니다. 그림 5는 결과 출력의 스크린샷을 보여 줍니다.

[외부 Repeater에는 각 범주가 나열 ![. 내부는 해당 범주에 대 한 제품을 나열 합니다.](nested-data-web-controls-vb/_static/image14.png)](nested-data-web-controls-vb/_static/image13.png)

**그림 5**: 외부 리피터는 각 범주를 나열 합니다. 내부 항목에는 해당 범주에 대 한 제품이 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](nested-data-web-controls-vb/_static/image15.png)).

## <a name="accessing-the-products-by-category-data-programmatically"></a>프로그래밍 방식으로 범주 데이터로 제품 액세스

ObjectDataSource를 사용 하 여 현재 범주에 대 한 제품을 검색 하는 대신, `CategoryID`에 전달 될 때 적절 한 제품 집합을 반환 하는 ASP.NET 페이지의 코드 숨김이 클래스 (또는 `App_Code` 폴더 또는 별도의 클래스 라이브러리 프로젝트)에서 메서드를 만들 수 있습니다. ASP.NET 페이지의 코드 숨김이 클래스에 이러한 메서드가 있고 `GetProductsInCategory(categoryID)`이름이 지정 되어 있다고 가정 합니다. 이 메서드를 사용 하면 다음 선언 구문을 사용 하 여 현재 범주의 제품을 내부 Repeater에 바인딩할 수 있습니다.

[!code-aspx[Main](nested-data-web-controls-vb/samples/sample6.aspx)]

Repeater s `DataSource` 속성은 데이터 바인딩 구문을 사용 하 여 해당 데이터가 `GetProductsInCategory(categoryID)` 메서드에서 제공 됨을 표시 합니다. `Eval("CategoryID")`는 `Object`형식의 값을 반환 하므로 `GetProductsInCategory(categoryID)` 메서드에 전달 하기 전에 개체를 `Integer` 캐스팅 합니다. 데이터 바인딩 구문을 통해 여기에서 액세스 하는 `CategoryID`는 *외부* 리피터 (`CategoryList`)에서 `Categories` 테이블의 레코드에 바인딩된 `CategoryID`입니다. 따라서 `CategoryID`는 데이터베이스 `NULL` 값이 될 수 없다는 것을 알고 있으므로 `DBNull`를 다시 처리 하 고 있는지 확인 하지 않고 `Eval` 메서드를 무조건 캐스팅할 수 있습니다.

이 방법을 사용 하면 `GetProductsInCategory(categoryID)` 메서드를 만들고 제공 된 *`categoryID`* 제공 된 적절 한 제품 집합을 검색 해야 합니다. 이 작업을 수행 하려면 `ProductsBLL` 클래스 s `GetProductsByCategoryID(categoryID)` 메서드에서 반환 된 `ProductsDataTable` 반환 하면 됩니다. `NestedControls.aspx` 페이지에 대 한 코드 숨김이 클래스에서 `GetProductsInCategory(categoryID)` 메서드를 만듭니다. 이렇게 하려면 다음 코드를 사용 합니다.

[!code-vb[Main](nested-data-web-controls-vb/samples/sample7.vb)]

이 메서드는 단순히 `ProductsBLL` 메서드의 인스턴스를 만들고 `GetProductsByCategoryID(categoryID)` 메서드의 결과를 반환 합니다. 메서드는 `Public` 또는 `Protected`로 표시 되어야 합니다. 메서드가 `Private`표시 되는 경우에는 ASP.NET 페이지의 선언적 태그에서 액세스할 수 없습니다.

이 새로운 기술을 사용 하도록 이러한 변경을 수행한 후 잠시 시간을 들 여 브라우저를 통해 페이지를 봅니다. ObjectDataSource 및 `ItemDataBound` 이벤트 처리기 접근 방식을 사용할 때 출력이 출력과 동일 해야 합니다 (스크린샷 보려면 그림 5 참조).

> [!NOTE]
> ASP.NET page s 코드 busywork 클래스에 `GetProductsInCategory(categoryID)` 메서드를 만드는 것 처럼 보일 수 있습니다. 이 메서드는 모두 `ProductsBLL` 클래스의 인스턴스를 만들고 해당 `GetProductsByCategoryID(categoryID)` 메서드의 결과를 반환 합니다. `DataSource='<%# ProductsBLL.GetProductsByCategoryID(CType(Eval("CategoryID"), Integer)) %>'`?와 같이 내부 Repeater의 데이터 바인딩 구문에서이 메서드를 직접 호출 하지 않는 이유는 무엇 인가요? 이 구문은 `ProductsBLL` 클래스의 현재 구현에서 작동 하지 않지만 (`GetProductsByCategoryID(categoryID)` 메서드가 인스턴스 메서드 이기 때문) 정적 `GetProductsByCategoryID(categoryID)` 메서드를 포함 하거나 클래스에 정적 `Instance()` 메서드를 포함 하 여 `ProductsBLL` 클래스의 새 인스턴스를 반환 하도록 `ProductsBLL`를 수정할 수 있습니다.

이러한 수정 작업을 수행 하면 ASP.NET page s의 코드 숨김이 클래스에서 `GetProductsInCategory(categoryID)` 메서드가 필요 하지 않지만 코드를 사용 하는 클래스 메서드를 사용 하면 검색 된 데이터를 더 유연 하 게 사용할 수 있습니다.

## <a name="retrieving-all-of-the-product-information-at-once"></a>모든 제품 정보를 한 번에 검색

이전 클래스의 `GetProductsByCategoryID(categoryID)` 메서드 `ProductsBLL`를 호출 하 여 현재 범주에 대 한 제품을 확인 하는 두 가지 방법입니다. 첫 번째 방법은 ObjectDataSource를 통해, 두 번째는 코드 숨김이 클래스의 `GetProductsInCategory(categoryID)` 메서드를 통해 수행 합니다. 이 메서드가 호출 될 때마다 비즈니스 논리 계층은 데이터 액세스 계층으로 이동 하 여 `CategoryID` 필드가 제공 된 입력 매개 변수와 일치 하는 `Products` 테이블의 행을 반환 하는 SQL 문을 사용 하 여 데이터베이스를 쿼리 합니다.

시스템에서 *n* 개의 범주를 지정 하는 경우이 방법은 데이터베이스 하나에 대 한 안전망 *n* + 1을 호출 하 여 모든 범주를 가져온 다음 *n* 을 호출 하 여 각 범주와 관련 된 제품을 가져옵니다. 그러나 한 번의 호출로 두 개의 데이터베이스를 호출 하 여 모든 범주를 가져오고 모든 제품을 가져오는 데 필요한 모든 데이터를 검색할 수 있습니다. 모든 제품을 설치한 후에는 해당 제품을 필터링 하 여 현재 `CategoryID`와 일치 하는 제품만 해당 범주에 있는 내부 리피터에 게 바인딩할 수 있습니다.

이 기능을 제공 하기 위해 ASP.NET 페이지의 코드 숨김이 클래스에서 `GetProductsInCategory(categoryID)` 메서드를 약간만 수정 해야 합니다. `ProductsBLL` 클래스 `GetProductsByCategoryID(categoryID)` 메서드의 결과를 무조건 반환 하는 대신, 먼저 *모든* 제품에 액세스 (이미 액세스 하지 않은 경우) 한 다음 전달 된 `CategoryID`에 따라 제품의 필터링 된 보기만 반환 하면 됩니다.

[!code-vb[Main](nested-data-web-controls-vb/samples/sample8.vb)]

페이지 수준 변수를 추가 `allProducts`합니다. 이는 모든 제품에 대 한 정보를 포함 하며 `GetProductsInCategory(categoryID)` 메서드가 처음 호출 될 때 채워집니다. `allProducts` 개체가 생성 되 고 채워져 있는지 확인 한 후에는이 메서드는 `CategoryID` 지정 된 `CategoryID`와 일치 하는 행만 액세스할 수 있도록 DataTable의 결과를 필터링 합니다. 이 접근 방식은 *N* + 1에서 2로 데이터베이스에 액세스 하는 횟수를 줄입니다.

이 향상 된 기능은 페이지의 렌더링 된 태그에 변경 내용을 적용 하지 않으며 다른 방법 보다 더 작은 레코드를 반환 하지 않습니다. 단지 데이터베이스에 대 한 호출 수를 줄입니다.

> [!NOTE]
> 데이터베이스 액세스의 수를 줄이면 성능이 명확. 그러나 그렇지 않을 수도 있습니다. 예를 들어 `CategoryID` `NULL`된 많은 수의 제품이 있는 경우 `GetProducts` 메서드를 호출 하면 표시 되지 않는 많은 제품이 반환 됩니다. 또한 범주 하위 집합만 표시 하는 경우에는 모든 제품을 반환 하는 것이 불필요 한 것일 수 있습니다 .이 경우 페이징이 구현 된 경우에 해당 합니다.

두 기술의 성능을 분석 하는 경우에만 surefire 유일한 방법은 응용 프로그램의 일반적인 사례 시나리오에 맞게 조정 된 제어 된 테스트를 실행 하는 것입니다.

## <a name="summary"></a>요약

이 자습서에서는 하나의 데이터 웹 컨트롤 내에 데이터 웹 컨트롤을 중첩 하는 방법을 살펴보았습니다. 특히 외부 반복을 사용 하 여 각 범주에 대 한 항목을 글머리 기호 목록에 있는 각 범주에 대 한 제품을 나열 하는 내부 리피터로 표시 하는 방법을 살펴보았습니다. 중첩 된 사용자 인터페이스를 빌드하는 주된 문제는 올바른 데이터를 내부 데이터 웹 컨트롤에 액세스 하 고 바인딩하는 것입니다. 이 자습서에서는 다양 한 기술을 사용할 수 있습니다. 첫 번째 방법은 `DataSourceID` 속성을 통해 내부 데이터 웹 컨트롤에 바인딩된 `ItemTemplate` 외부 데이터 웹 컨트롤에서 ObjectDataSource를 사용 하 여 검사 했습니다. 두 번째 기술은 ASP.NET 페이지의 코드 숨김으로 된 클래스의 메서드를 통해 데이터에 액세스 했습니다. 그런 다음이 메서드를 데이터 바인딩 구문을 통해 내부 데이터 웹 컨트롤 `DataSource` 속성에 바인딩할 수 있습니다.

이 자습서에서 검사 한 중첩 된 사용자 인터페이스가 Repeater 내에 중첩 된 Repeater를 사용 했지만 이러한 기술은 다른 데이터 웹 컨트롤로 확장 될 수 있습니다. 표를 GridView 내에서 중첩 하거나 DataList 내에서 GridView를 중첩할 수 있습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Zack Jones 및 Liz Shulok입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](showing-multiple-records-per-row-with-the-datalist-control-vb.md)
