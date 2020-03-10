---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-acess-two-pages-datalist-cs
title: 두 페이지에 걸쳐 마스터/세부 정보C#필터링 () | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 마스터/세부 보고서를 두 페이지에 분리 하는 방법에 대해 살펴봅니다. ' 마스터 ' 페이지에서 Repeater 컨트롤을 사용 하 여 categ 목록을 렌더링 합니다.
ms.author: riande
ms.date: 10/30/2010
ms.assetid: 68b8c023-92fa-4df6-9563-1764e16e4b04
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-acess-two-pages-datalist-cs
msc.type: authoredcontent
ms.openlocfilehash: 545b24a66476c55aff88ac62d3a6528105fea6c0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78491651"
---
# <a name="masterdetail-filtering-across-two-pages-c"></a>두 페이지에 걸쳐 마스터/세부 정보 필터링(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_34_CS.exe) 또는 [PDF 다운로드](master-detail-filtering-acess-two-pages-datalist-cs/_static/datatutorial34cs1.pdf)

> 이 자습서에서는 마스터/세부 보고서를 두 페이지에 분리 하는 방법에 대해 살펴봅니다. "마스터" 페이지에서 Repeater 컨트롤을 사용 하 여 클릭 하면 "세부 정보" 페이지로 이동 합니다 .이 페이지에서 두 열 DataList는 선택 된 범주에 속하는 제품을 표시 합니다.

## <a name="introduction"></a>소개

[이전 자습서](master-detail-filtering-with-a-dropdownlist-datalist-cs.md) 에서는 dropdownlist를 사용 하 여 "마스터" 레코드를 표시 하 고 "details"를 표시 하는 DataList를 사용 하는 단일 웹 페이지에서 마스터/세부 보고서를 표시 하는 방법을 살펴보았습니다. 마스터/세부 보고서에 사용 되는 또 다른 일반적인 패턴은 한 웹 페이지에 마스터 레코드를 포함 하 고 다른 하나에 세부 정보를 포함 하는 것입니다. 이전 [마스터/세부 정보 필터링의 두 페이지](../masterdetail/master-detail-filtering-across-two-pages-cs.md) 자습서에서 GridView를 사용 하 여 시스템의 모든 공급자를 표시 하는이 패턴을 검토 했습니다. 이 GridView에는 쿼리 문자열의 `SupplierID`를 전달 하 여 두 번째 페이지에 대 한 링크로 렌더링 되는 하이퍼링크 필드가 포함 되었습니다. 두 번째 페이지는 GridView를 사용 하 여 선택한 공급자가 제공 하는 제품을 나열 합니다.

이러한 두 페이지 마스터/세부 정보 보고서는 DataList 및 Repeater 컨트롤을 사용 하 여 수행할 수 있습니다. 유일한 차이점은 DataList와 Repeater 모두 hyperlink 필드 컨트롤에 대 한 지원을 제공 하지 않는다는 것입니다. 대신 컨트롤의 `ItemTemplate`에 HyperLink 웹 컨트롤 또는 앵커 HTML 요소 (`<a>`)를 추가 해야 합니다. 그런 다음 선언적 또는 프로그래밍 방식을 사용 하 여 하이퍼링크의 `NavigateUrl` 속성 또는 앵커의 `href` 특성을 사용자 지정할 수 있습니다.

이 자습서에서는 Repeater 컨트롤을 사용 하 여 한 페이지의 글머리 기호 목록에 있는 범주를 나열 하는 예제를 살펴봅니다. 각 목록 항목에는 범주 이름과 설명이 포함 되며, 범주 이름은 두 번째 페이지에 대 한 링크로 표시 됩니다. 이 링크를 클릭 하면 사용자가 두 번째 페이지로 whisk, 여기서 DataList는 선택 된 범주에 속하는 제품을 표시 합니다.

## <a name="step-1-displaying-the-categories-in-a-bulleted-list"></a>1 단계: 글머리 기호 목록에 범주 표시

마스터/세부 정보 보고서를 만드는 첫 번째 단계는 "마스터" 레코드를 표시 하 여 시작 하는 것입니다. 따라서 첫 번째 작업은 "마스터" 페이지에 범주를 표시 하는 것입니다. `DataListRepeaterFiltering` 폴더에서 `CategoryListMaster.aspx` 페이지를 열고, Repeater 컨트롤을 추가 하 고, 스마트 태그를 선택 하 여 새 ObjectDataSource를 추가 합니다. `CategoriesBLL` 클래스의 `GetCategories` 메서드에서 데이터에 액세스 하도록 새 ObjectDataSource를 구성 합니다 (그림 1 참조).

[범주 Bll 클래스의 GetCategories 메서드를 사용 하도록 ObjectDataSource를 구성 ![](master-detail-filtering-acess-two-pages-datalist-cs/_static/image2.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image1.png)

**그림 1**: `CategoriesBLL` 클래스의 `GetCategories` 메서드를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-acess-two-pages-datalist-cs/_static/image3.png))

다음으로 각 범주 이름과 설명을 글머리 기호 목록의 항목으로 표시 하도록 Repeater의 템플릿을 정의 합니다. 세부 정보 페이지에 대 한 각 범주 링크를 사용 하는 것에 대해 걱정할 필요가 없습니다. 다음은 Repeater 및 ObjectDataSource의 선언 태그를 보여 줍니다.

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample1.aspx)]

이 마크업이 완료 되 면 잠시 후 브라우저를 통해 진행 상황을 확인 합니다. 그림 2에 나와 있는 것 처럼, Repeater는 각 범주의 이름과 설명을 보여 주는 글머리 기호 목록으로 렌더링 합니다.

[각 범주가 글머리 기호 목록 항목으로 표시 ![](master-detail-filtering-acess-two-pages-datalist-cs/_static/image5.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image4.png)

**그림 2**: 각 범주가 글머리 기호 목록 항목으로 표시 됨 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-acess-two-pages-datalist-cs/_static/image6.png))

## <a name="step-2-turning-the-category-name-into-a-link-to-the-details-page"></a>2 단계: 범주 이름을 세부 정보 페이지에 대 한 링크로 설정

사용자가 지정 된 범주에 대 한 "세부 정보" 정보를 표시할 수 있도록 하려면 클릭 하면 각 글머리 기호 목록 항목에 대 한 링크를 추가 해야 합니다 .이 링크를 클릭 하면 사용자가 두 번째 페이지 (`ProductsForCategoryDetails.aspx`)로 이동 합니다. 그러면이 두 번째 페이지에서 DataList를 사용 하 여 선택한 범주의 제품을 표시 합니다. 링크를 클릭 한 범주를 확인 하려면 몇 가지 메커니즘을 통해 클릭 한 범주의 `CategoryID`를 두 번째 페이지로 전달 해야 합니다. 한 페이지에서 다른 페이지로 스칼라 데이터를 전송 하는 가장 간단 하 고 간단한 방법은이 자습서에서 사용할 옵션인 querystring을 통하는 것입니다. 특히 `ProductsForCategoryDetails.aspx` 페이지에는 선택한 *`categoryID`* 값이 `CategoryID`라는 querystring 필드를 통해 전달 될 것으로 간주 됩니다. 예를 들어 `CategoryID` 1 인 음료 범주에 대 한 제품을 보려면 사용자가 `ProductsForCategoryDetails.aspx?CategoryID=1`를 방문 합니다.

Repeater에서 각 글머리 기호 목록 항목에 대 한 하이퍼링크를 만들려면 하이퍼링크 웹 컨트롤 또는 HTML 앵커 요소 (`<a>`)를 `ItemTemplate`에 추가 해야 합니다. 각 행에 대해 하이퍼링크가 동일 하 게 표시 되는 경우에는 어떤 방법으로도 충분 합니다. 반복기의 경우 앵커 요소를 사용 하는 것이 좋습니다. 앵커 요소를 사용 하려면 다음과 같이 Repeater의 ItemTemplate을 업데이트 합니다.

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample2.aspx)]

`CategoryID` 앵커 요소의 `href` 특성에 직접 삽입할 수 있습니다. 그러나이 작업을 수행 하려면 `href` 특성 내의 `Eval` 메서드가 문자열 (`"CategoryID"`)을 따옴표로 구분 하므로 아포스트로피를 사용 하 여 `href` 특성의 값을 구분 하는 것이 좋습니다 (따옴표). 또는 하이퍼링크 웹 컨트롤을 대신 사용할 수 있습니다.

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample3.aspx)]

URL의 정적 부분 (`ProductsForCategoryDetails.aspx?CategoryID`)이 문자열 연결을 사용 하 여 데이터 바인딩 구문 내에서 직접 `Eval("CategoryID")` 결과에 추가 되는 방식을 확인 합니다.

HyperLink 컨트롤을 사용할 경우의 장점 중 하나는 필요한 경우 Repeater의 `ItemDataBound` 이벤트 처리기에서 프로그래밍 방식으로 액세스할 수 있다는 것입니다. 예를 들어 연결 된 제품이 없는 범주에 대 한 링크가 아니라 범주 이름을 텍스트로 표시할 수 있습니다. 이러한 검사는 `ItemDataBound` 이벤트 처리기에서 프로그래밍 방식으로 수행할 수 있습니다. 연결 된 제품이 없는 범주에 대해 하이퍼링크의 `NavigateUrl` 속성은 빈 문자열로 설정 될 수 있습니다. 따라서 특정 범주 이름 렌더링이 링크 대신 일반 텍스트로 생성 됩니다. `ItemDataBound` 이벤트 처리기를 통해 프로그래밍 방식 논리에 따라 DataList 및 Repeater의 내용에 서식을 지정 하는 방법에 대 한 자세한 내용은 [데이터에 따라 datalist 및 Repeater 서식 지정](../displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-cs.md) 자습서를 다시 참조 하세요.

함께 사용 하는 경우 페이지에서 앵커 요소나 HyperLink 컨트롤 방식을 자유롭게 사용할 수 있습니다. 방법에 관계 없이 브라우저를 통해 페이지를 볼 때 각 범주 이름을 `ProductsForCategoryDetails.aspx`에 대 한 링크로 렌더링 하 여 해당 하는 `CategoryID` 값을 전달 해야 합니다 (그림 3 참조).

[이제 범주 이름이 ProductsForCategoryDetails에 연결 ![.](master-detail-filtering-acess-two-pages-datalist-cs/_static/image8.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image7.png)

**그림 3**: 이제 범주 이름이 `ProductsForCategoryDetails.aspx` 연결 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-acess-two-pages-datalist-cs/_static/image9.png)).

## <a name="step-3-listing-the-products-that-belong-to-the-selected-category"></a>3 단계: 선택한 범주에 속한 제품 나열

`CategoryListMaster.aspx` 페이지가 완료 되 면 `ProductsForCategoryDetails.aspx`"세부 정보" 페이지를 구현 하는 데 주의를 기울일 준비가 되었습니다. 이 페이지를 열고 도구 상자에서 디자이너로 DataList를 끌어서 `ID` 속성을 `ProductsInCategory`로 설정 합니다. 다음으로, DataList의 스마트 태그를 선택 하 여 페이지에 새 ObjectDataSource를 추가 하 고 `ProductsInCategoryDataSource`이름을 지정 합니다. `ProductsBLL` 클래스의 `GetProductsByCategoryID(categoryID)` 메서드를 호출 하도록 구성 합니다. 삽입, 업데이트 및 삭제 탭의 드롭다운 목록을 (없음)로 설정 합니다.

[ProductsBLL 클래스의 GetProductsByCategoryID (categoryID) 메서드를 사용 하도록 ObjectDataSource를 구성 ![](master-detail-filtering-acess-two-pages-datalist-cs/_static/image11.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image10.png)

**그림 4**: `ProductsBLL` 클래스의 `GetProductsByCategoryID(categoryID)` 메서드를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-acess-two-pages-datalist-cs/_static/image12.png))

`GetProductsByCategoryID(categoryID)` 메서드는 입력 매개 변수 ( *`categoryID`* )를 허용 하므로 데이터 소스 선택 마법사는 매개 변수의 원본을 지정할 수 있는 기회를 제공 합니다. QueryStringField `CategoryID`를 사용 하 여 매개 변수 원본을 QueryString으로 설정 합니다.

[![Querystring 필드 CategoryID를 매개 변수의 소스로 사용 합니다.](master-detail-filtering-acess-two-pages-datalist-cs/_static/image14.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image13.png)

**그림 5**: 매개 변수의 소스로 `CategoryID` Querystring 필드 사용 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-acess-two-pages-datalist-cs/_static/image15.png))

이전 자습서에서 살펴본 것 처럼 데이터 소스 선택 마법사를 완료 한 후 Visual Studio에서 각 데이터 필드 이름과 값을 나열 하는 DataList에 대 한 `ItemTemplate`를 자동으로 만듭니다. 이 템플릿을 제품 이름, 공급 업체 및 가격만 표시 하는 템플릿으로 바꿉니다. 또한 DataList의 `RepeatColumns` 속성을 2로 설정 합니다. 이러한 변경 후에는 DataList 및 ObjectDataSource의 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample4.aspx)]

이 페이지의 작동 방식을 보려면 `CategoryListMaster.aspx` 페이지에서 시작 합니다. 그런 다음 범주 글머리 기호 목록에서 링크를 클릭 합니다. 이렇게 하면 querystring을 통해 `CategoryID`를 전달 하는 `ProductsForCategoryDetails.aspx`으로 이동 합니다. 그러면 `ProductsForCategoryDetails.aspx`의 `ProductsInCategoryDataSource` ObjectDataSource는 지정 된 범주에 대 한 제품만 가져와 DataList에 표시 하며,이는 행당 두 제품을 렌더링 합니다. 그림 6에는 음료를 볼 때 `ProductsForCategoryDetails.aspx`의 스크린샷에 나와 있습니다.

[음료를 표시 하는 ![행당 2 개](master-detail-filtering-acess-two-pages-datalist-cs/_static/image17.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image16.png)

**그림 6**: 음료는 행당 2 개 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-acess-two-pages-datalist-cs/_static/image18.png))로 표시 됩니다.

## <a name="step-4-displaying-category-information-on-productsforcategorydetailsaspx"></a>4 단계: ProductsForCategoryDetails에서 범주 정보 표시

사용자가 `CategoryListMaster.aspx`의 범주를 클릭 하면 선택 된 범주에 속하는 제품을 `ProductsForCategoryDetails.aspx` 하 고 표시 합니다. 그러나 `ProductsForCategoryDetails.aspx`에는 선택한 범주에 대 한 시각적 단서가 없습니다. 음료를 클릭 하지만 실수로 조미료를 클릭 한 사용자는 `ProductsForCategoryDetails.aspx`도달 하면 실수를 현실화 하는 방법이 없습니다. 이러한 잠재적인 문제를 완화 하기 위해 `ProductsForCategoryDetails.aspx` 페이지의 맨 위에 선택한 범주 (이름 및 설명)에 대 한 정보를 표시할 수 있습니다.

이를 수행 하려면 `ProductsForCategoryDetails.aspx`의 Repeater 컨트롤 위에 FormView를 추가 합니다. 그런 다음 `CategoryDataSource` 라는 FormView의 스마트 태그에서 페이지에 새 ObjectDataSource를 추가 하 고 `CategoriesBLL` 클래스의 `GetCategoryByCategoryID(categoryID)` 메서드를 사용 하도록 구성 합니다.

[범주 Bll 클래스의 GetCategoryByCategoryID (categoryID) 메서드를 통해 범주에 대 한 정보에 액세스 ![](master-detail-filtering-acess-two-pages-datalist-cs/_static/image20.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image19.png)

**그림 7**: `CategoriesBLL` 클래스의 `GetCategoryByCategoryID(categoryID)` 메서드를 통해 범주에 대 한 정보 액세스 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-acess-two-pages-datalist-cs/_static/image21.png))

3 단계에서 추가 된 `ProductsInCategoryDataSource` ObjectDataSource와 마찬가지로 `CategoryDataSource`의 데이터 원본 구성 마법사는 `GetCategoryByCategoryID(categoryID)` 메서드의 입력 매개 변수에 대 한 원본을 확인 하는 메시지를 표시 합니다. 이전과 동일한 설정을 사용 하 여 매개 변수 원본을 QueryString으로 설정 하 고 QueryStringField 값을 `CategoryID` (그림 5로 다시 참조) 합니다.

마법사를 완료 한 후 Visual Studio에서 FormView에 대 한 `ItemTemplate`, `EditItemTemplate`및 `InsertItemTemplate`을 자동으로 만듭니다. 읽기 전용 인터페이스를 제공 하기 때문에 `EditItemTemplate`를 제거 하 고 `InsertItemTemplate`수 있습니다. 또한 FormView의 `ItemTemplate`을 자유롭게 사용자 지정할 수 있습니다. 불필요 한 템플릿을 제거 하 고 ItemTemplate을 사용자 지정한 후에는 FormView와 ObjectDataSource의 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample5.aspx)]

그림 8에서는 브라우저를 통해이 페이지를 볼 때의 스크린샷을 보여 줍니다.

> [!NOTE]
> FormView 외에도 사용자를 다시 목록 (`CategoryListMaster.aspx`) 목록으로 다시 이동 하는 FormView 위에 HyperLink 컨트롤을 추가 했습니다. 이 링크를 다른 곳에 추가 하거나 생략 하려면 자유롭게 사용 합니다.

[이제 페이지 맨 위에 ![범주 정보가 표시 됩니다.](master-detail-filtering-acess-two-pages-datalist-cs/_static/image23.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image22.png)

**그림 8**: 이제 범주 정보가 페이지 맨 위에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-acess-two-pages-datalist-cs/_static/image24.png)).

## <a name="step-5-displaying-a-message-if-no-products-belong-to-the-selected-category"></a>5 단계: 선택한 범주에 속한 제품이 없으면 메시지 표시

`CategoryListMaster.aspx` 페이지에는 관련 제품이 있는지 여부에 관계 없이 시스템의 모든 범주가 나열 됩니다. 사용자가 연결 된 제품이 없는 범주를 클릭 하는 경우 해당 데이터 원본에 항목이 없으므로 `ProductsForCategoryDetails.aspx`의 DataList가 렌더링 되지 않습니다. 이전 자습서에서 살펴본 것 처럼 GridView는 데이터 원본에 레코드가 없는 경우 표시할 문자 메시지를 지정 하는 데 사용할 수 있는 `EmptyDataText` 속성을 제공 합니다. 불행 하 게도 DataList 나 Repeater에는 이러한 속성이 없습니다.

선택한 범주에 대해 일치 하는 제품이 없음을 사용자에 게 알리는 메시지를 표시 하려면 일치 하는 제품이 없는 이벤트에 표시 되는 메시지에 `Text` 속성이 할당 되어 있는 페이지에 레이블 컨트롤을 추가 해야 합니다. 그런 다음 DataList에 항목이 포함 되는지 여부에 따라 `Visible` 속성을 프로그래밍 방식으로 설정 해야 합니다.

이를 수행 하려면 먼저 DataList 아래에 레이블을 추가 합니다. `ID` 속성을 `NoProductsMessage`로 설정 하 고 `Text` 속성을 "선택한 범주에 대 한 제품이 없습니다 ..."로 설정 합니다. 다음으로, 데이터가 `ProductsInCategory` DataList에 바인딩 되었는지 여부에 따라이 레이블의 `Visible` 속성을 프로그래밍 방식으로 설정 해야 합니다. 이 할당은 데이터를 DataList에 바인딩한 후에 수행 해야 합니다. GridView, DetailsView 및 FormView의 경우, 데이터 바인딩에서 완료 된 후에 발생 하는 컨트롤의 `DataBound` 이벤트에 대 한 이벤트 처리기를 만들 수 있습니다. 그러나 DataList와 Repeater 모두 `DataBound` 이벤트를 사용할 수 없습니다.

이 특정 예제에서는 페이지의 `Load` 이벤트 이전에 데이터가 DataList에 할당 되기 때문에 `Page_Load` 이벤트 처리기에서 레이블의 `Visible` 속성을 할당할 수 있습니다. 그러나이 방법은 나중에 페이지의 수명 주기에서 ObjectDataSource의 데이터가 DataList에 바인딩될 수 있기 때문에 일반적인 경우에는 작동 하지 않습니다. 예를 들어 표시 된 데이터가 다른 컨트롤의 값을 기반으로 하는 경우 (예: DropDownList를 사용 하 여 마스터/세부 정보 보고서를 표시 하 여 "마스터" 레코드를 저장 하는 경우) 페이지 수명 주기에서 `PreRender` 단계까지 데이터를 데이터 웹 컨트롤에 다시 바인딩할 수 없습니다.

모든 경우에 대해 작동 하는 한 가지 솔루션은 `Item` 또는 `AlternatingItem`의 항목 형식을 바인딩할 때 DataList의 `ItemDataBound` (또는 `ItemCreated`) 이벤트 처리기에서 `False`에 `Visible` 속성을 할당 하는 것입니다. 이 경우 데이터 원본에 하나 이상의 데이터 항목이 있으므로 `NoProductsMessage` 레이블을 숨길 수 있습니다. 이 이벤트 처리기 외에도, DataList의 `DataBinding` 이벤트에 대 한 이벤트 처리기가 필요 합니다. 여기서 레이블의 `Visible` 속성을 `True`로 초기화 합니다. `DataBinding` 이벤트는 `ItemDataBound` 이벤트 이전에 발생 하므로 레이블의 `Visible` 속성은 처음에 `True`로 설정 됩니다. 그러나 데이터 항목이 있는 경우 `False`로 설정 됩니다. 다음 코드는이 논리를 구현 합니다.

[!code-csharp[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample6.cs)]

Northwind 데이터베이스의 모든 범주는 하나 이상의 제품과 연결 됩니다. 이 기능을 테스트 하기 위해이 자습서에 대 한 Northwind 데이터베이스를 수동으로 조정 하 여 생성 범주 (`CategoryID` = 7)와 관련 된 모든 제품을 해산물 범주 (`CategoryID` = 8)에 재할당 했습니다. 새 쿼리를 선택 하 고 다음 `UPDATE` 문을 사용 하 여 서버 탐색기에서이 작업을 수행할 수 있습니다.

[!code-sql[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample7.sql)]

이에 따라 데이터베이스를 업데이트 한 후 `CategoryListMaster.aspx` 페이지로 돌아가서 생성 링크를 클릭 합니다. 생성 범주에 속한 제품이 더 이상 없기 때문에 "선택한 범주에 대 한 제품이 없습니다 ..."가 표시 됩니다. 그림 9에 표시 된 메시지입니다.

[선택한 범주에 속한 제품이 없는 경우 메시지가 표시 ![](master-detail-filtering-acess-two-pages-datalist-cs/_static/image26.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image25.png)

**그림 9**: 선택한 범주에 속한 제품이 없으면 메시지가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-acess-two-pages-datalist-cs/_static/image27.png)).

## <a name="summary"></a>요약

마스터/세부 정보 보고서에는 단일 페이지에 마스터 및 세부 레코드가 모두 표시 될 수 있지만 대부분의 웹 사이트에서는 두 개의 웹 페이지에서 분리 됩니다. 이 자습서에서는 "마스터" 웹 페이지에서 리피터를 사용 하 고 "세부 정보" 페이지에 나열 된 관련 제품을 사용 하 여 글머리 기호 목록에 나열 된 범주를 사용 하 여 이러한 마스터/세부 정보 보고서를 구현 하는 방법을 살펴보았습니다. 마스터 웹 페이지의 각 목록 항목에는 행의 `CategoryID` 값을 따라 전달 된 세부 정보 페이지에 대 한 링크가 포함 되어 있습니다.

세부 정보 페이지에서 지정 된 공급자에 대 한 제품 검색은 `ProductsBLL` 클래스의 `GetProductsByCategoryID(categoryID)` 방법을 통해 수행 되었습니다. `CategoryID` querystring 값을 매개 변수 원본으로 사용 하 여 *`categoryID`* 매개 변수 값을 선언적으로 지정 했습니다. 또한 FormView를 사용 하 여 세부 정보 페이지에 범주 세부 정보를 표시 하는 방법 및 선택한 범주에 속한 제품이 없는 경우 메시지를 표시 하는 방법을 살펴보았습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별 해 주셔서 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Zack Jones 및 Liz Shulok입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](master-detail-filtering-with-a-dropdownlist-datalist-cs.md)
> [다음](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md)
