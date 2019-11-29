---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-with-a-dropdownlist-datalist-cs
title: DropDownList (C#)을 사용 하 여 마스터/세부 정보 필터링 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 Dropdownlist를 사용 하 여 단일 웹 페이지에서 마스터/세부 보고서를 표시 하는 방법을 보여 줍니다 .이를 통해 ' 마스터 ' 레코드와 DataList를 displ에 표시
ms.author: riande
ms.date: 07/18/2007
ms.assetid: 07fa47ae-e491-4a2f-b265-d342b9ddef46
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-with-a-dropdownlist-datalist-cs
msc.type: authoredcontent
ms.openlocfilehash: 8289f46fd6d0143802269d5c6196a4c40db9378c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74631045"
---
# <a name="masterdetail-filtering-with-a-dropdownlist-c"></a>DropDownList 한 개로 마스터/세부 정보 필터링(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_33_CS.exe) 또는 [PDF 다운로드](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/datatutorial33cs1.pdf)

> 이 자습서에서는 Dropdownlist를 사용 하 여 "마스터" 레코드를 표시 하 고 "details"를 표시 하는 DataList를 사용 하는 단일 웹 페이지에서 마스터/세부 보고서를 표시 하는 방법을 알아봅니다.

## <a name="introduction"></a>소개

먼저 DropDownList 자습서를 [사용 하 여 이전 마스터/세부 정보 필터링](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) 에서 GridView를 사용 하 여 만든 마스터/세부 정보 보고서는 "마스터" 레코드 집합을 표시 하는 것으로 시작 합니다. 그러면 사용자가 마스터 레코드 중 하나로 드릴 다운 하 여 해당 마스터 레코드의 "세부 정보"를 볼 수 있습니다. 마스터/세부 정보 보고서는 일 대 다 관계를 시각화 하 고 특히 "와이드" 테이블 (열이 많은 테이블)에서 자세한 정보를 표시 하는 데 적합 합니다. 이전 자습서에서 GridView 및 DetailsView 컨트롤을 사용 하 여 마스터/세부 보고서를 구현 하는 방법을 살펴보았습니다. 이 자습서 및 다음 두 가지에서는 이러한 개념을 다시 확인할 것 이지만 DataList 및 Repeater 컨트롤을 대신 사용 하는 방법에 중점을 둡니다.

이 자습서에서는 "details" 레코드가 DataList에 표시 된 "마스터" 레코드를 포함 하는 DropDownList을 사용 하는 방법을 살펴보겠습니다.

## <a name="step-1-adding-the-masterdetail-tutorial-web-pages"></a>1 단계: 마스터/세부 정보 자습서 웹 페이지 추가

이 자습서를 시작 하기 전에 먼저이 자습서에 필요한 폴더 및 ASP.NET 페이지와 DataList 및 Repeater 컨트롤을 사용 하 여 마스터/세부 정보 보고서를 처리 하는 다음 두 페이지를 추가 해 보겠습니다. `DataListRepeaterFiltering`이라는 프로젝트에서 새 폴더를 만들어 시작 합니다. 그런 다음이 폴더에 다음 5 개의 ASP.NET 페이지를 추가 하 여 마스터 페이지 `Site.master`를 사용 하도록 구성 된 페이지를 모두 구성 합니다.

- `Default.aspx`
- `FilterByDropDownList.aspx`
- `CategoryListMaster.aspx`
- `ProductsForCategoryDetails.aspx`
- `CategoriesAndProducts.aspx`

![DataListRepeaterFiltering 폴더를 만들고 자습서 ASP.NET 페이지를 추가 합니다.](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image1.png)

**그림 1**: `DataListRepeaterFiltering` 폴더 만들기 및 자습서 ASP.NET 페이지 추가

그런 다음 `Default.aspx` 페이지를 열고 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤을 `UserControls` 폴더에서 디자인 화면으로 끌어 옵니다. [마스터 페이지 및 사이트 탐색](../introduction/master-pages-and-site-navigation-cs.md) 자습서에서 만든이 사용자 정의 컨트롤은 사이트 맵을 열거 하 고 현재 섹션의 자습서를 글머리 기호 목록에 표시 합니다.

[SectionLevelTutorialListing 사용자 정의 컨트롤을 Default.aspx에 추가 ![](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image3.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image2.png)

**그림 2**: `Default.aspx`에 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image4.png))

글머리 기호 목록에 만들 마스터/세부 자습서를 표시 하려면 사이트 맵에 추가 해야 합니다. `Web.sitemap` 파일을 열고 "DataList 및 Repeater로 데이터 표시" 사이트 맵 노드 마크업을 사용 하 여 다음 태그를 추가 합니다.

[!code-xml[Main](master-detail-filtering-with-a-dropdownlist-datalist-cs/samples/sample1.xml)]

![새 ASP.NET 페이지를 포함 하도록 사이트 맵 업데이트](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image5.png)

**그림 3**: 새 ASP.NET 페이지를 포함 하도록 사이트 맵 업데이트

## <a name="step-2-displaying-the-categories-in-a-dropdownlist"></a>2 단계: DropDownList에 범주 표시

마스터/세부 정보 보고서에는 선택한 목록 항목의 제품이 DataList의 페이지 아래쪽에 표시 되는 DropDownList 범주가 나열 됩니다. 앞서 첫 번째 작업은 범주를 DropDownList에 표시 하는 것입니다. 먼저 `DataListRepeaterFiltering` 폴더에서 `FilterByDropDownList.aspx` 페이지를 열고 도구 상자의 DropDownList를 페이지의 디자이너로 끌어옵니다. 그런 다음 DropDownList의 `ID` 속성을 `Categories`로 설정 합니다. DropDownList의 스마트 태그에서 데이터 소스 선택 링크를 클릭 하 고 `CategoriesDataSource`라는 새 ObjectDataSource를 만듭니다.

[새 ObjectDataSource 명명 된 범주 Datasource를 추가 ![](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image7.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image6.png)

**그림 4**: 이름이 `CategoriesDataSource` 새 ObjectDataSource 추가 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image8.png))

`CategoriesBLL` 클래스의 `GetCategories()` 메서드를 호출 하도록 새 ObjectDataSource를 구성 합니다. ObjectDataSource를 구성한 후에는 DropDownList에 표시 되어야 하는 데이터 원본 필드와 각 목록 항목의 값으로 연결 해야 하는 데이터 원본 필드를 지정 해야 합니다. `CategoryName` 필드를 표시 하 고 각 목록 항목의 값으로 `CategoryID` 합니다.

[DropDownList에서 범주 필드를 표시 하 고 CategoryID를 값으로 사용 ![](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image10.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image9.png)

**그림 5**: DropDownList에 `CategoryName` 필드가 표시 되 고 `CategoryID` 값으로 사용 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image11.png))

이 시점에서 `Categories` 테이블의 레코드를 사용 하 여 채워진 DropDownList 컨트롤이 있습니다 (약 6 초 후에 수행 됨). 그림 6에서는 브라우저를 통해 볼 때의 진행률을 보여 줍니다.

[드롭다운 목록에서 현재 범주를 ![합니다.](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image13.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image12.png)

**그림 6**: 드롭다운 목록에 현재 범주가 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image14.png)).

## <a name="step-2-adding-the-products-datalist"></a>2 단계: 제품 DataList 추가

마스터/세부 정보 보고서의 마지막 단계는 선택한 범주와 관련 된 제품을 나열 하는 것입니다. 이를 수행 하려면 페이지에 DataList를 추가 하 고 `ProductsByCategoryDataSource`이라는 새 ObjectDataSource를 만듭니다. `ProductsByCategoryDataSource` 컨트롤이 `ProductsBLL` 클래스의 `GetProductsByCategoryID(categoryID)` 메서드에서 데이터를 검색 하도록 합니다. 이 마스터/세부 보고서는 읽기 전용 이므로 삽입, 업데이트 및 삭제 탭에서 (없음) 옵션을 선택 합니다.

[![GetProductsByCategoryID (categoryID) 메서드를 선택 합니다.](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image16.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image15.png)

**그림 7**: `GetProductsByCategoryID(categoryID)` 방법 선택 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image17.png))

다음을 클릭 한 후 ObjectDataSource 마법사는 `GetProductsByCategoryID(categoryID)` 메서드의 *`categoryID`* 매개 변수에 대 한 값의 원본을 알려 주는 메시지를 표시 합니다. 선택한 `categories` DropDownList 항목의 값을 사용 하려면 매개 변수 소스를 제어 하 고 ControlID를 `Categories`설정 합니다.

[categoryID 매개 변수를 DropDownList 범주의 값으로 설정 ![합니다.](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image19.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image18.png)

**그림 8**: *`categoryID`* 매개 변수를 `Categories` DropDownList 값으로 설정 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image20.png))

데이터 소스 구성 마법사가 완료 되 면 Visual Studio에서 각 데이터 필드의 이름과 값을 표시 하는 DataList에 대 한 `ItemTemplate`를 자동으로 생성 합니다. DataList를 개선 하 여 각 항목 사이에 `<hr>` 요소를 삽입 하는 `SeparatorTemplate`와 함께 제품의 이름, 범주, 공급자, 단위당 수량 및 가격만 표시 하는 `ItemTemplate`를 대신 사용 하도록 하겠습니다. [DataList 및 Repeater 컨트롤](../displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-cs.md) 을 사용 하 여 데이터 표시 자습서의 예제에서 `ItemTemplate`를 사용 하지만, 가장 시각적으로 멋진 템플릿 태그를 자유롭게 사용할 수 있습니다.

이러한 변경을 수행한 후에는 DataList와 해당 ObjectDataSource의 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-datalist-cs/samples/sample2.aspx)]

잠시 후 브라우저에서 진행 상황을 확인해 보세요. 페이지를 처음 방문 하면 선택 된 범주 (음료)에 속하는 제품이 표시 됩니다 (그림 9에 표시 된 것 처럼). 그러나 DropDownList를 변경 해도 데이터가 업데이트 되지 않습니다. 이는 DataList를 업데이트 하기 위해 포스트백이 수행 되어야 하기 때문입니다. 이렇게 하려면 DropDownList의 `AutoPostBack` 속성을 `true`로 설정 하거나 페이지에 단추 웹 컨트롤을 추가 합니다. 이 자습서에서는 DropDownList의 `AutoPostBack` 속성을 `true`으로 설정 했습니다.

그림 9와 10은 마스터/세부 보고서를 실행 하는 방법을 보여 줍니다.

[페이지를 처음 방문할 때 ![음료 제품이 표시 됩니다.](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image22.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image21.png)

**그림 9**: 페이지를 처음 방문할 때 음료 제품이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image23.png)).

[새 제품 (생성)을 선택 ![자동으로 포스트백이 발생 하 고 DataList가 업데이트 됩니다.](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image25.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image24.png)

**그림 10**: 새 제품 (생성)을 선택 하면 자동으로 포스트백이 발생 하 고 DataList ([전체 크기의 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image26.png))가 업데이트 됩니다.

## <a name="adding-a----choose-a-category----list-item"></a>"--범주 선택--" 목록 항목 추가

`FilterByDropDownList.aspx` 페이지를 처음 방문 하면 범주 DropDownList의 첫 번째 목록 항목 (음료)이 기본적으로 선택 되어 DataList의 음료 제품이 표시 됩니다. DropDownList 자습서를 *사용 하 여 마스터/세부 정보 필터링* 에서 기본적으로 선택 된 DropDownList에 "--범주 선택--" 옵션을 추가 하 고 선택 하면 데이터베이스의 *모든* 제품을 표시 했습니다. 이러한 접근 방식은 각 제품 행이 적은 양의 화면 부동산을 차지 하는 경우 GridView에 제품을 나열할 때 관리 하기 쉽습니다. 그러나 DataList를 사용 하는 경우 각 제품 정보는 훨씬 큰 화면 청크를 사용 합니다. 계속 해 서 "--범주 선택--" 옵션을 추가 하 고 기본적으로 선택 되어 있지만 선택 시 모든 제품을 표시 하는 대신 제품을 표시 하지 않도록 구성 하겠습니다.

DropDownList에 새 목록 항목을 추가 하려면 속성 창로 이동 하 여 `Items` 속성에서 줄임표를 클릭 합니다. `Text` "--범주 선택--"과 `Value` `0`를 사용 하 여 새 목록 항목을 추가 합니다.

![추가](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image27.png)

**그림 11**: "--범주 선택--" 목록 항목 추가

또는 다음 태그를 DropDownList에 추가 하 여 목록 항목을 추가할 수 있습니다.

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-datalist-cs/samples/sample3.aspx)]

또한 `false` (기본값)로 설정 되어 있고, 범주가 ObjectDataSource에서 DropDownList에 바인딩되면, 수동으로 추가 된 목록 항목을 덮어쓸 수 있으므로 DropDownList 컨트롤의 `AppendDataBoundItems`를 `true`으로 설정 해야 합니다.

![AppendDataBoundItems 속성을 True로 설정 합니다.](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image28.png)

**그림 12**: `AppendDataBoundItems` 속성을 True로 설정

"--범주 선택--" 목록 항목에 대해 `0` 값을 선택 하는 이유는 시스템에 `0`값이 없기 때문입니다. 따라서 "--범주 선택--" 목록 항목을 선택할 때 제품 레코드가 반환 되지 않습니다. 이를 확인 하려면 잠시 후 브라우저를 통해 페이지를 방문 하세요. 그림 13에 표시 된 것 처럼 페이지를 처음 볼 때 "--범주 선택--" 목록 항목을 선택 하면 제품이 표시 되지 않습니다.

[![](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image30.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image29.png)

**그림 13**: "--범주 선택--" 목록 항목을 선택 하면 제품이 표시 되지 않습니다 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image31.png)).

"--범주 선택--" 옵션을 선택한 경우에는 *모든* 제품을 표시 하는 대신 `-1` 값을 사용 합니다. Astute reader는 DropDownList를 사용 하 여 *마스터/세부 정보 필터링* 으로 돌아갈 때 `-1`의 *`categoryID`* 값이 전달 되 면 모든 제품 레코드가 반환 되도록 `ProductsBLL` 클래스의 `GetProductsByCategoryID(categoryID)` 메서드를 업데이트 했습니다.

## <a name="summary"></a>요약

계층적으로 관련 된 데이터를 표시 하는 경우 사용자가 계층의 맨 위에서 데이터를 확인 하 고 세부 정보로 드릴 다운할 수 있는 마스터/세부 정보 보고서를 사용 하 여 데이터를 표시 하는 것이 좋습니다. 이 자습서에서는 선택한 범주의 제품을 보여 주는 간단한 마스터/세부 정보 보고서 작성을 검토 했습니다. 이는 범주 목록에 대해 DropDownList을 사용 하 고 선택한 범주에 속한 제품에 대해 DataList를 사용 하 여 수행 되었습니다.

다음 자습서에서는 두 페이지에서 마스터 및 세부 정보 레코드를 분리 하는 방법을 살펴보겠습니다. 첫 번째 페이지에는 세부 정보를 볼 수 있는 링크가 포함 된 "마스터" 레코드 목록이 표시 됩니다. 링크를 클릭 하면 사용자가 두 번째 페이지로 whisk 선택한 마스터 레코드에 대 한 세부 정보가 표시 됩니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별 해 주셔서 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Randy Schmidt입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [다음](master-detail-filtering-acess-two-pages-datalist-cs.md)
