---
uid: web-forms/overview/data-access/custom-formatting/displaying-summary-information-in-the-gridview-s-footer-cs
title: GridView의 바닥글에 요약 정보 표시 (C#) | Microsoft Docs
author: rick-anderson
description: 요약 정보는 종종 요약 행의 보고서 아래쪽에 표시 됩니다. GridView 컨트롤에는 pr 할 수 있는 셀이 포함 된 바닥글 행이 포함 될 수 있습니다.
ms.author: riande
ms.date: 03/31/2010
ms.assetid: d50edc31-9286-4c6a-8635-be09e72752a4
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/displaying-summary-information-in-the-gridview-s-footer-cs
msc.type: authoredcontent
ms.openlocfilehash: b258a2bdeaea8da4e9c5c5d8043b167d94e1e817
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74616816"
---
# <a name="displaying-summary-information-in-the-gridviews-footer-c"></a>GridView의 바닥글에 요약 정보 표시(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_15_CS.exe) 또는 [PDF 다운로드](displaying-summary-information-in-the-gridview-s-footer-cs/_static/datatutorial15cs1.pdf)

> 요약 정보는 종종 요약 행의 보고서 아래쪽에 표시 됩니다. GridView 컨트롤에는 프로그래밍 방식으로 집계 데이터를 삽입할 수 있는 셀이 포함 된 바닥글 행이 포함 될 수 있습니다. 이 자습서에서는이 바닥글 행에 집계 데이터를 표시 하는 방법을 알아봅니다.

## <a name="introduction"></a>소개

각 제품의 가격, 재고 단위, 주문 단위 및 순서 바꾸기 수준을 볼 수 있을 뿐 아니라, 사용자가 평균 가격, 재고 단위의 총 수 등의 집계 정보에도 관심이 있을 수 있습니다. 이러한 요약 정보는 대개 요약 행의 보고서 아래쪽에 표시 됩니다. GridView 컨트롤에는 프로그래밍 방식으로 집계 데이터를 삽입할 수 있는 셀이 포함 된 바닥글 행이 포함 될 수 있습니다.

이 작업은 다음과 같은 세 가지 문제를 제공 합니다.

1. 바닥글 행을 표시 하도록 GridView 구성
2. 요약 데이터 확인 즉, 평균 가격이 나 재고 단위의 합계를 계산 하려면 어떻게 해야 하나요?
3. 바닥글 행의 해당 셀에 요약 데이터 삽입

이 자습서에서는 이러한 문제를 해결 하는 방법을 알아봅니다. 특히 GridView에 표시 된 선택한 범주의 제품을 사용 하 여 드롭다운 목록에 있는 범주를 나열 하는 페이지를 만듭니다. GridView에는 평균 가격과 전체 단위 수를 표시 하 고 해당 범주의 제품에 대 한 주문에 대 한 바닥글 행이 포함 됩니다.

[GridView의 바닥글 행에 ![요약 정보가 표시 됩니다.](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image2.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image1.png)

**그림 1**: GridView 바닥글 행에 요약 정보가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image3.png)).

이 자습서의 범주를 products 마스터/세부 정보 인터페이스와 함께 사용 하 여 이전 [마스터/세부 정보 필터링](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) 에서 적용 되는 개념을 DropDownList 자습서로 작성 합니다. 이전 자습서를 아직 수행 하지 않은 경우이 자습서를 계속 진행 하기 전에이 작업을 수행 하세요.

## <a name="step-1-adding-the-categories-dropdownlist-and-products-gridview"></a>1 단계: DropDownList 및 Products GridView 추가

GridView 바닥글에 요약 정보를 추가 하는 것과 관련 하 여 먼저 마스터/세부 정보 보고서를 작성해 보겠습니다. 이 첫 번째 단계를 완료 한 후에는 요약 데이터를 포함 하는 방법을 살펴보겠습니다.

먼저 `CustomFormatting` 폴더에서 `SummaryDataInFooter.aspx` 페이지를 엽니다. DropDownList 컨트롤을 추가 하 고 해당 `ID`을 `Categories`로 설정 합니다. 다음으로, DropDownList의 스마트 태그에서 데이터 소스 선택 링크를 클릭 하 고 옵트인을 선택 하 여 `CategoriesBLL` 클래스의 `GetCategories()` 메서드를 호출 하는 `CategoriesDataSource` 라는 새 ObjectDataSource를 추가 합니다.

[새 ObjectDataSource 명명 된 범주 Datasource를 추가 ![](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image5.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image4.png)

**그림 2**: 이름이 `CategoriesDataSource` 새 ObjectDataSource 추가 ([전체 크기 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image6.png))

[ObjectDataSource에서 Categories Bll 클래스의 GetCategories () 메서드를 호출 하 ![](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image8.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image7.png)

**그림 3**: ObjectDataSource에서 `CategoriesBLL` 클래스의 `GetCategories()` 메서드를 호출 하도록 합니다 ([전체 크기 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image9.png)).

ObjectDataSource를 구성한 후 마법사는 표시 되어야 하는 데이터 필드 값 및 DropDownList의 `ListItem` 값에 해당 하는 값을 지정 해야 하는 DropDownList의 데이터 원본 구성 마법사를 반환 합니다. `CategoryName` 필드를 표시 하 고 `CategoryID` 값으로 사용 합니다.

[ListItems에 대 한 텍스트 및 값으로 범주 및 CategoryID 필드를 각각 사용할 ![](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image11.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image10.png)

**그림 4**: `CategoryName` 및 `CategoryID` 필드를 각각 `ListItem` s에 대 한 `Text` 및 `Value` 사용 ([전체 크기 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image12.png))

이 시점에서 시스템의 범주를 나열 하는 DropDownList (`Categories`)이 있습니다. 이제 선택 된 범주에 속하는 제품을 나열 하는 GridView를 추가 해야 합니다. 그러나 먼저 DropDownList의 스마트 태그에서 AutoPostBack 사용 확인란을 선택 합니다. Dropdownlist 자습서를 사용 하 여 *마스터/세부 정보 필터링* 에서 설명한 대로 dropdownlist의 `AutoPostBack` 속성을 `true` 설정 하 여 페이지는 dropdownlist 값이 변경 될 때마다 다시 게시 됩니다. 이렇게 하면 GridView가 새로 고쳐지고 새로 선택한 범주에 해당 하는 제품이 표시 됩니다. `AutoPostBack` 속성이 `false` (기본값)로 설정 된 경우 범주를 변경 해도 포스트백이 발생 하지 않으므로 나열 된 제품이 업데이트 되지 않습니다.

[![DropDownList의 스마트 태그에서 Enable AutoPostBack 확인란을 선택 합니다.](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image14.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image13.png)

**그림 5**: DropDownList의 스마트 태그에서 Enable AutoPostBack ([전체 크기 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image15.png)) 확인란을 선택 합니다.

선택한 범주에 대 한 제품을 표시 하기 위해 페이지에 GridView 컨트롤을 추가 합니다. GridView의 `ID` `ProductsInCategory` 설정 하 고 `ProductsInCategoryDataSource`라는 새 ObjectDataSource에 바인딩합니다.

[새 ObjectDataSource 라는 새 ObjectDataSource를 추가 ![](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image17.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image16.png)

**그림 6**: 이름이 `ProductsInCategoryDataSource` 새 ObjectDataSource 추가 ([전체 크기 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image18.png))

`ProductsBLL` 클래스의 `GetProductsByCategoryID(categoryID)` 메서드를 호출 하도록 ObjectDataSource를 구성 합니다.

[ObjectDataSource에서 GetProductsByCategoryID (categoryID) 메서드를 호출 하 ![](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image20.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image19.png)

**그림 7**: ObjectDataSource에서 `GetProductsByCategoryID(categoryID)` 메서드 호출 ([전체 크기 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image21.png))

`GetProductsByCategoryID(categoryID)` 메서드는 입력 매개 변수를 사용 하기 때문에 마법사의 마지막 단계에서 매개 변수 값의 원본을 지정할 수 있습니다. 선택한 범주에서 해당 제품을 표시 하기 위해 `Categories` DropDownList에서 매개 변수를 가져옵니다.

[선택한 범주에 있는 categoryID 매개 변수 값을 가져옵니다 ![가져옵니다.](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image23.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image22.png)

**그림 8**: 선택한 범주 DropDownList에서 *`categoryID`* 매개 변수 값 가져오기 ([전체 크기 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image24.png))

마법사를 완료 한 후 GridView에는 각 제품 속성에 대 한 BoundField이 있습니다. `ProductName`, `UnitPrice`, `UnitsInStock`및 `UnitsOnOrder` BoundFields만 표시 되도록 이러한 BoundFields를 정리 하겠습니다. 나머지 BoundFields (예: 통화로 `UnitPrice` 형식 지정)에 필드 수준 설정을 자유롭게 추가할 수 있습니다. 이러한 변경을 수행한 후 GridView의 선언 태그는 다음과 같이 표시 됩니다.

[!code-aspx[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample1.aspx)]

이 시점에는 선택한 범주에 속한 제품에 대해 이름, 단가, 재고 단위 및 발주량을 표시 하는 완전히 작동 하는 마스터/세부 정보 보고서가 있습니다.

[선택한 범주에 있는 categoryID 매개 변수 값을 가져옵니다 ![가져옵니다.](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image26.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image25.png)

**그림 9**: 선택한 범주 DropDownList에서 *`categoryID`* 매개 변수 값 가져오기 ([전체 크기 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image27.png))

## <a name="step-2-displaying-a-footer-in-the-gridview"></a>2 단계: GridView에 바닥글 표시

GridView 컨트롤은 머리글 및 바닥글 행을 모두 표시할 수 있습니다. 이러한 행은 `ShowHeader` 및 `ShowFooter` 속성의 값에 따라 각각 표시 되며 `ShowHeader` 기본적으로 `true`를 사용 하 고 `ShowFooter`에 `false`합니다. GridView에 바닥글을 포함 하려면 단순히 해당 `ShowFooter` 속성을 `true`로 설정 합니다.

[GridView의 ShowFooter 속성을 true로 설정 ![](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image29.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image28.png)

**그림 10**: GridView의 `ShowFooter` 속성을 `true`로 설정 ([전체 크기 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image30.png))

바닥글 행에는 GridView에 정의 된 각 필드에 대 한 셀이 있습니다. 그러나 이러한 셀은 기본적으로 비어 있습니다. 잠시 시간을 들 여 브라우저에서 진행률을 확인 하세요. 이제 `ShowFooter` 속성이 `true`로 설정 되어 있으면 GridView에 빈 바닥글 행이 포함 됩니다.

[이제 GridView에 바닥글 행이 포함 됩니다 ![](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image32.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image31.png)

**그림 11**: GridView는 이제 바닥글 행을 포함 합니다 ([전체 크기 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image33.png)).

그림 11의 바닥글 행은 흰색 배경 이므로 나타나지 않습니다. 진한 빨강 배경을 지정 하는 `Styles.css`에 `FooterStyle` CSS 클래스를 만든 다음 `DataWebControls` 테마에서 `GridView.skin` 스킨 파일을 구성 하 여이 CSS 클래스를 GridView의 `FooterStyle`속성에 할당 합니다. 스킨과 테마를 사용 하 여 브러시를 만들어야 하는 경우 ObjectDataSource 자습서를 [사용 하 여 데이터 표시](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md) 를 다시 참조 하세요.

`Styles.css`에 다음 CSS 클래스를 추가 하 여 시작 합니다.

[!code-css[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample2.css)]

`FooterStyle` CSS 클래스는 스타일의 `HeaderStyle` 클래스와 유사 하지만 `HeaderStyle`의 배경색은 더 어둡고 텍스트는 굵은 글꼴로 표시 됩니다. 또한 바닥글의 텍스트는 오른쪽 맞춤 되지만 머리글의 텍스트는 가운데 맞춤 됩니다.

그런 다음이 CSS 클래스를 모든 GridView 바닥글에 연결 하려면 `DataWebControls` 테마에서 `GridView.skin` 파일을 열고 `FooterStyle`의 `CssClass` 속성을 설정 합니다. 이 추가 후 파일의 태그는 다음과 같습니다.

[!code-aspx[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample3.aspx)]

아래 스크린샷에 나와 있는 것 처럼 이러한 변경으로 인해 바닥글을 보다 명확 하 게 파악할 수 있습니다.

[이제 GridView의 바닥글 행에 Reddish 배경색이 있습니다. ![](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image35.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image34.png)

**그림 12**: GridView의 바닥글 행에는 Reddish 배경색 ([전체 크기 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image36.png))이 표시 됩니다.

## <a name="step-3-computing-the-summary-data"></a>3 단계: 요약 데이터 계산

GridView의 바닥글이 표시 되 면 다음에 직면 하는 문제는 요약 데이터를 계산 하는 방법입니다. 이 집계 정보를 계산 하는 방법에는 다음 두 가지가 있습니다.

1. SQL 쿼리를 통해 데이터베이스에 대 한 추가 쿼리를 실행 하 여 특정 범주에 대 한 요약 데이터를 계산할 수 있습니다. SQL에는 데이터를 요약 하는 데 사용할 데이터를 지정 하기 위해 `GROUP BY` 절과 함께 다양 한 집계 함수가 포함 되어 있습니다. 다음 SQL 쿼리는 필요한 정보를 다시 가져옵니다.  

    [!code-sql[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample4.sql)]

    물론 `SummaryDataInFooter.aspx` 페이지에서 직접이 쿼리를 실행 하는 대신 `ProductsTableAdapter` 및 `ProductsBLL`에서 메서드를 만드는 것이 좋습니다.
2. 이 정보를 GridView에 추가 하는 경우 데이터 자습서에 [따라 사용자 지정 서식 지정](custom-formatting-based-upon-data-cs.md) 에 설명 된 대로 gridview의 `RowDataBound` 이벤트 처리기는 데이터 바인딩된 후 gridview에 추가 되는 각 행에 대해 한 번씩 발생 합니다. 이 이벤트에 대 한 이벤트 처리기를 만들면 집계 하려는 값의 누계를 유지할 수 있습니다. 마지막 데이터 행을 GridView에 바인딩한 후에는 평균을 계산 하는 데 필요한 합계와 정보가 있습니다.

일반적으로 데이터베이스에 대 한 여행 및 데이터 액세스 계층 및 비즈니스 논리 계층에서 요약 기능을 구현 하는 데 필요한 노력을 저장할 때 두 번째 방법을 사용 하지만 어떤 방법으로도 충분 합니다. 이 자습서에서는 두 번째 옵션을 사용 하 고 `RowDataBound` 이벤트 처리기를 사용 하 여 누계를 추적 하겠습니다.

디자이너에서 GridView를 선택 하 고 속성 창에서 번개 아이콘을 클릭 한 다음 `RowDataBound` 이벤트를 두 번 클릭 하 여 GridView에 대 한 `RowDataBound` 이벤트 처리기를 만듭니다. 이렇게 하면 `SummaryDataInFooter.aspx` 페이지의 코드 숨김이 클래스에 `ProductsInCategory_RowDataBound` 라는 새 이벤트 처리기가 만들어집니다.

[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample5.cs)]

누계를 유지 하려면 이벤트 처리기 범위 밖의 변수를 정의 해야 합니다. 다음 네 개의 페이지 수준 변수를 만듭니다.

- 형식의 `_totalUnitPrice``decimal`
- 형식의 `_totalNonNullUnitPriceCount``int`
- 형식의 `_totalUnitsInStock``int`
- 형식의 `_totalUnitsOnOrder``int`

그런 다음 `RowDataBound` 이벤트 처리기에서 발생 하는 각 데이터 행에 대해 이러한 3 개의 변수를 증가 하는 코드를 작성 합니다.

[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample6.cs)]

`RowDataBound` 이벤트 처리기는 DataRow를 처리 하 고 있는지 확인 하 여 시작 합니다. 설정 된 후에는 `e.Row`의 `GridViewRow` 개체에 바인딩된 `Northwind.ProductsRow` 인스턴스가 `product`변수에 저장 됩니다. 그런 다음 전체 변수를 실행 하면 현재 제품의 해당 값이 증가 합니다 (데이터베이스 `NULL` 값이 포함 되어 있지 않은 것으로 가정). 평균 가격은 이러한 두 숫자의 몫 이므로 실행 중인 `UnitPrice` 합계와`NULL` 되지 않은 `UnitPrice` 레코드 수를 모두 추적 합니다.

## <a name="step-4-displaying-the-summary-data-in-the-footer"></a>4 단계: 바닥글에 요약 데이터 표시

요약 데이터의 합계를 사용 하 여 마지막 단계는 GridView 바닥글 행에 표시 하는 것입니다. `RowDataBound` 이벤트 처리기를 통해 프로그래밍 방식으로이 작업을 수행할 수 있습니다. 바닥글 행을 포함 하 여 GridView에 바인딩된 *모든* 행에 대해 `RowDataBound` 이벤트 처리기가 발생 한다는 것을 기억 하세요. 따라서 다음 코드를 사용 하 여 바닥글 행에 데이터를 표시 하도록 이벤트 처리기를 확장할 수 있습니다.

[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample7.cs)]

모든 데이터 행이 추가 된 후에 바닥글 행이 GridView에 추가 되기 때문에 누적 된 총 계산이 완료 되 면 바닥글에 요약 데이터를 표시할 준비가 된 것입니다. 마지막 단계는 바닥글의 셀에 이러한 값을 설정 하는 것입니다.

특정 바닥글 셀에 텍스트를 표시 하려면 `Cells` 인덱싱이 0에서 시작 하는 `e.Row.Cells[index].Text = value`을 사용 합니다. 다음 코드는 평균 가격 (총 가격을 제품 수로 나눈 값)을 계산 하 고 해당 GridView의 해당 바닥글 셀에 있는 전체 단위 수와 함께 재고 및 단위 수를 표시 합니다.

[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample8.cs)]

그림 13에는이 코드가 추가 된 후의 보고서가 나와 있습니다. `ToString("c")`에서 평균 가격 요약 정보의 서식을 통화와 같이 지정 하는 방법을 확인 합니다.

[이제 GridView의 바닥글 행에 Reddish 배경색이 있습니다. ![](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image38.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image37.png)

**그림 13**: GridView의 바닥글 행에 Reddish 배경색 ([전체 크기 이미지를 보려면 클릭](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image39.png))

## <a name="summary"></a>요약

요약 데이터를 표시 하는 것은 일반적인 보고서 요구 사항이 며 GridView 컨트롤을 사용 하면 해당 정보를 바닥글 행에 쉽게 포함할 수 있습니다. GridView의 `ShowFooter` 속성이 `true`로 설정 되 고 `RowDataBound` 이벤트 처리기를 통해 프로그래밍 방식으로 셀에 텍스트를 설정할 수 있으면 바닥글 행이 표시 됩니다. 요약 데이터를 계산 하려면 데이터베이스를 다시 쿼리하거나 ASP.NET 페이지의 코드 숨김으로 코드를 사용 하 여 요약 데이터를 프로그래밍 방식으로 계산 하는 방법으로 수행할 수 있습니다.

이 자습서에서는 GridView, DetailsView 및 FormView 컨트롤을 사용 하 여 사용자 지정 형식에 대 한 검사를 마칩니다. 다음 자습서에서는 이러한 동일한 컨트롤을 사용 하 여 데이터 삽입, 업데이트 및 삭제에 대 한 탐색을 시작 합니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

> [!div class="step-by-step"]
> [이전](using-the-formview-s-templates-cs.md)
> [다음](custom-formatting-based-upon-data-vb.md)
