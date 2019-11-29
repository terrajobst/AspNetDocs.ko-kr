---
uid: web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/sorting-data-in-a-datalist-or-repeater-control-vb
title: DataList 또는 Repeater 컨트롤에서 데이터 정렬 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 DataList 및 Repeater에 정렬 지원을 포함 하는 방법 뿐만 아니라 데이터를 사용할 수 있는 DataList 또는 Repeater를 구성 하는 방법을 살펴봅니다.
ms.author: riande
ms.date: 11/13/2006
ms.assetid: 97c13898-0741-45f9-b3fa-7540ab1679e6
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/sorting-data-in-a-datalist-or-repeater-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 81e07bec8569b9ee987dfaa84dec9eec95a2692f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74638161"
---
# <a name="sorting-data-in-a-datalist-or-repeater-control-vb"></a>DataList 또는 반복기 컨트롤에서 데이터 정렬(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_45_VB.exe) 또는 [PDF 다운로드](sorting-data-in-a-datalist-or-repeater-control-vb/_static/datatutorial45vb1.pdf)

> 이 자습서에서는 DataList 및 Repeater에 정렬 지원을 포함 하는 방법 뿐만 아니라 데이터를 페이징 하 고 정렬할 수 있는 DataList 또는 Repeater를 구성 하는 방법을 살펴봅니다.

## <a name="introduction"></a>소개

[이전 자습서](paging-report-data-in-a-datalist-or-repeater-control-vb.md) 에서는 DataList에 페이징 지원을 추가 하는 방법을 살펴보았습니다. `PagedDataSource` 개체를 반환 하는 `ProductsBLL` 클래스 (`GetProductsAsPagedDataSource`)에서 새 메서드를 만들었습니다. Datalist 또는 Repeater에 바인딩되면 DataList 또는 Repeater는 요청한 데이터 페이지만 표시 합니다. 이 기법은 기본 제공 기본 페이징 기능을 제공 하기 위해 GridView, DetailsView 및 FormView 컨트롤에서 내부적으로 사용 되는 것과 비슷합니다.

GridView는 페이징 지원을 제공 하는 것 외에도 기본적으로 제공 되는 정렬을 지원 합니다. DataList와 Repeater 모두 기본 제공 정렬 기능을 제공 하지 않습니다. 그러나 약간의 코드를 사용 하 여 정렬 기능을 추가할 수 있습니다. 이 자습서에서는 DataList 및 Repeater에 정렬 지원을 포함 하는 방법 뿐만 아니라 데이터를 페이징 하 고 정렬할 수 있는 DataList 또는 Repeater를 구성 하는 방법을 살펴봅니다.

## <a name="a-review-of-sorting"></a>정렬에 대 한 검토

[보고서 데이터 페이징 및 정렬](../paging-and-sorting/paging-and-sorting-report-data-vb.md) 자습서에서 살펴본 것 처럼 GridView 컨트롤은 기본 정렬 지원을 제공 합니다. 각 GridView 필드에는 데이터를 정렬 하는 기준이 되는 데이터 필드를 나타내는 연결 된 `SortExpression`있을 수 있습니다. GridView s `AllowSorting` 속성이 `true`로 설정 된 경우 `SortExpression` 속성 값이 있는 각 GridView 필드의 헤더는 LinkButton로 렌더링 됩니다. 사용자가 특정 GridView 필드 헤더를 클릭 하면 포스트백이 발생 하 고 클릭 한 필드 `SortExpression`에 따라 데이터가 정렬 됩니다.

GridView 컨트롤에는 데이터를 정렬 하는 GridView 필드의 `SortExpression`을 저장 하는 `SortExpression` 속성도 있습니다. 또한 `SortDirection` 속성은 데이터를 오름차순으로 정렬할지 아니면 내림차순으로 정렬할지를 나타냅니다. 사용자가 특정 GridView 필드 헤더 링크를 연속 해 서 두 번 클릭 하면 정렬 순서가 전환 됩니다.

GridView가 데이터 소스 컨트롤에 바인딩되면 해당 `SortExpression` 및 `SortDirection` 속성을 데이터 소스 컨트롤에 전달 합니다. 데이터 소스 컨트롤은 데이터를 검색 한 다음 제공 된 `SortExpression` 및 `SortDirection` 속성에 따라 정렬 합니다. 데이터를 정렬 하 고 나면 데이터 소스 컨트롤에서 GridView로 반환 됩니다.

DataList 또는 Repeater 컨트롤과이 기능을 복제 하려면 다음을 수행 해야 합니다.

- 정렬 인터페이스 만들기
- 정렬할 데이터 필드와 오름차순으로 정렬할지 아니면 내림차순으로 정렬할지를 지정 합니다.
- 특정 데이터 필드를 기준으로 데이터를 정렬 하도록 ObjectDataSource에 지시

3 단계와 4 단계에서이 세 가지 작업을 수행 합니다. 다음에는 DataList 또는 Repeater에서 페이징 및 정렬 지원을 모두 포함 하는 방법을 살펴보겠습니다.

## <a name="step-2-displaying-the-products-in-a-repeater"></a>2 단계: 리피터에 제품 표시

정렬 관련 기능을 구현 하는 방법에 대 한 자세한 내용을 보려면 먼저 Repeater 컨트롤에 제품을 나열 해 보세요. 먼저 `PagingSortingDataListRepeater` 폴더에서 `Sorting.aspx` 페이지를 엽니다. Repeater 컨트롤을 웹 페이지에 추가 하 고 해당 `ID` 속성을 `SortableProducts`로 설정 합니다. Repeater s 스마트 태그에서 `ProductsDataSource` 라는 새 ObjectDataSource를 만들고 `ProductsBLL` 클래스의 `GetProducts()` 메서드에서 데이터를 검색 하도록 구성 합니다. 삽입, 업데이트 및 삭제 탭의 드롭다운 목록에서 (없음) 옵션을 선택 합니다.

[ObjectDataSource를 만든 ![GetProductsAsPagedDataSource () 메서드를 사용 하도록 구성 합니다.](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image2.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image1.png)

**그림 1**: ObjectDataSource를 만들고 `GetProductsAsPagedDataSource()` 메서드를 사용 하도록 구성 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image3.png))

[업데이트, 삽입 및 삭제 탭의 드롭다운 목록을 (없음)으로 설정 ![](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image5.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image4.png)

**그림 2**: 업데이트, 삽입 및 삭제 탭의 드롭다운 목록을 (없음)로 설정 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image6.png))

DataList와는 달리 Visual Studio에서는 데이터 소스에 바인딩한 후에 Repeater 컨트롤에 대 한 `ItemTemplate`를 자동으로 만들지 않습니다. 또한 Repeater 컨트롤의 스마트 태그에는 DataList s에 있는 템플릿 편집 옵션이 없으므로이 `ItemTemplate` 선언적으로 추가 해야 합니다. 제품 이름, 공급자 및 범주를 표시 하는 이전 자습서에서와 동일한 `ItemTemplate`를 사용 합니다.

`ItemTemplate`를 추가한 후에는 Repeater 및 ObjectDataSource s 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample1.aspx)]

그림 3에서는 브라우저를 통해 볼 때이 페이지를 보여 줍니다.

[![각 제품 이름, 공급 업체 및 범주가 표시 됩니다.](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image8.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image7.png)

**그림 3**: 각 제품 이름, 공급 업체 및 범주가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image9.png)).

## <a name="step-3-instructing-the-objectdatasource-to-sort-the-data"></a>3 단계: ObjectDataSource에 데이터 정렬을 지시

Repeater에 표시 되는 데이터를 정렬 하려면 데이터를 정렬 하는 기준이 되는 정렬 식을 ObjectDataSource에 알려야 합니다. ObjectDataSource가 해당 데이터를 검색 하기 전에 먼저 [`Selecting` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selecting.aspx)를 발생 시킵니다 .이 이벤트는 정렬 식을 지정할 수 있는 기회를 제공 합니다. `Selecting` 이벤트 처리기에 [`DataSourceSelectArguments`](https://msdn.microsoft.com/library/system.web.ui.datasourceselectarguments.aspx)형식의 [`Arguments`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourceselectingeventargs.arguments.aspx) 속성이 있는 [`ObjectDataSourceSelectingEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourceselectingeventargs.aspx)형식의 개체가 전달 되었습니다. `DataSourceSelectArguments` 클래스는 데이터 소비자의 데이터 관련 요청을 데이터 소스 컨트롤에 전달 하 고 [`SortExpression` 속성](https://msdn.microsoft.com/library/system.web.ui.datasourceselectarguments.sortexpression.aspx)을 포함 하도록 디자인 되었습니다.

ASP.NET 페이지에서 ObjectDataSource로 정렬 정보를 전달 하려면 `Selecting` 이벤트에 대 한 이벤트 처리기를 만들고 다음 코드를 사용 합니다.

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample2.vb)]

*SortExpression* 값에는 데이터를 정렬 하는 데 사용할 데이터 필드의 이름 (예: ProductName)이 할당 되어야 합니다. 정렬 방향 관련 속성은 없으므로 데이터를 내림차순으로 정렬 하려는 경우 *sortExpression* 값 (예: ProductName desc)에 문자열 DESC를 추가 합니다.

계속 해 서 몇 가지 다른 하드 코드 된 값을 *sortExpression* 하 고 브라우저에서 결과를 테스트 합니다. 그림 4와 같이 ProductName DESC를 *sortExpression*으로 사용 하는 경우 제품 이름을 역순으로 역순으로 정렬 합니다.

[![제품 이름을 역순으로 역순으로 정렬 합니다.](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image11.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image10.png)

**그림 4**: 제품 이름을 역순으로 역순으로 정렬 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image12.png))

## <a name="step-4-creating-the-sorting-interface-and-remembering-the-sort-expression-and-direction"></a>4 단계: 정렬 인터페이스 만들기 및 정렬 식 및 방향 기억

GridView에서 정렬 지원을 켜면 정렬할 수 있는 각 필드의 머리글 텍스트를 LinkButton로 변환 하 여 클릭 시 데이터를 적절 하 게 정렬 합니다. 이러한 정렬 인터페이스를 사용 하면 데이터를 열에 깔끔하게 배치 하는 GridView를 사용할 수 있습니다. 그러나 DataList 및 Repeater 컨트롤의 경우 다른 정렬 인터페이스가 필요 합니다. 데이터 목록에 대 한 일반적인 정렬 인터페이스 (데이터 그리드와 반대)는 데이터를 정렬 하는 데 사용할 수 있는 필드를 제공 하는 드롭다운 목록입니다. 에서이 자습서에 대 한 인터페이스를 구현 해 보세요.

`SortableProducts` Repeater 위에 DropDownList 웹 컨트롤을 추가 하 고 `ID` 속성을 `SortBy`로 설정 합니다. 속성 창에서 `Items` 속성의 줄임표를 클릭 하 여 ListItem 컬렉션 편집기를 엽니다. `ListItem`를 추가 하 여 `ProductName`, `CategoryName`및 `SupplierName` 필드를 기준으로 데이터를 정렬 합니다. 또한 이름을 기준으로 제품을 사전순으로 정렬 하는 `ListItem`를 추가 합니다.

`ListItem` `Text` 속성은 모든 값 (예: 이름)으로 설정할 수 있지만 `Value` 속성은 데이터 필드의 이름 (예: ProductName)으로 설정 해야 합니다. 결과를 내림차순으로 정렬 하려면 ProductName DESC와 같이 문자열 DESC를 데이터 필드 이름에 추가 합니다.

![정렬할 때 각 데이터 필드에 대 한 ListItem 추가](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image13.png)

**그림 5**: 정렬 가능한 각 데이터 필드에 대 한 `ListItem` 추가

마지막으로, DropDownList의 오른쪽에 단추 웹 컨트롤을 추가 합니다. 해당 `ID` `RefreshRepeater`로 설정 하 고 `Text` 속성을 새로 고칩니다.

`ListItem` s를 만들고 새로 고침 단추를 추가한 후에는 DropDownList 및 Button s의 선언 구문이 다음과 같이 표시 됩니다.

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample3.aspx)]

정렬 DropDownList이 완료 되 면 다음에는 하드 코드 된 정렬 식과 달리 선택한 `SortBy``ListItem` s `Value` 속성을 사용 하도록 ObjectDataSource s `Selecting` 이벤트 처리기를 업데이트 해야 합니다.

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample4.vb)]

이 시점에서 처음 페이지를 방문 하는 경우에는 기본적으로 `SortBy` `ListItem` 선택 되어 `ProductName` 데이터 필드를 기준으로 제품이 정렬 됩니다 (그림 6 참조). 그림 7에 표시 된 것 처럼 범주와 같은 다른 정렬 옵션을 선택 하 고 새로 고침을 클릭 하면 다시 게시가 발생 하 고 범주 이름으로 데이터가 다시 정렬 됩니다.

[처음에는 제품 이름을 기준으로 제품을 정렬 ![합니다.](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image15.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image14.png)

**그림 6**: 제품 이름을 기준으로 처음 정렬 됩니다 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image16.png)).

[이제 제품이 범주별로 정렬 ![](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image18.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image17.png)

**그림 7**: 이제 제품을 범주별로 정렬 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image19.png))

> [!NOTE]
> [새로 고침] 단추를 클릭 하면 Repeater의 뷰 상태를 사용할 수 없기 때문에 데이터가 자동으로 다시 정렬 되므로 Repeater가 다시 게시 될 때마다 데이터 원본에 다시 바인딩됩니다. Repeater s 뷰 상태를 사용 하도록 설정 하면 정렬 드롭다운 목록을 변경 해도 정렬 순서에 영향을 주지 않습니다. 이를 해결 하려면 새로 고침 단추 s `Click` 이벤트에 대 한 이벤트 처리기를 만들고 repeater s `DataBind()` 메서드를 호출 하 여 해당 데이터 원본에 Repeater를 다시 바인딩합니다.

## <a name="remembering-the-sort-expression-and-direction"></a>정렬 식 및 방향 기억

정렬 되지 않은 관련 포스트백이 발생할 수 있는 페이지에서 정렬 가능한 DataList 또는 Repeater를 만들 때 다시 게시 간에 정렬 식과 방향을 기억 해야 합니다. 예를 들어 각 제품에 삭제 단추를 포함 하도록이 자습서의 Repeater를 업데이트 했다고 가정해 보겠습니다. 사용자가 삭제 단추를 클릭 하면 선택한 제품을 삭제 하는 코드를 실행 하 고 데이터를 Repeater에 다시 바인딩합니다. 다시 게시 하는 동안 정렬 정보가 지속 되지 않으면 화면에 표시 되는 데이터가 원래 정렬 순서로 되돌아갑니다.

이 자습서에서 DropDownList은 암시적으로 정렬 식 및 방향을 해당 뷰 상태에 저장 합니다. 다른 정렬 인터페이스를 사용 하는 경우를 예로 들 수 있습니다. 예를 들어 Linkbutton는 여러 가지 정렬 옵션을 제공 하 여 다시 게시에 대 한 정렬 순서를 염두에 두어야 합니다. 이는 쿼리 문자열에 sort 매개 변수를 포함 하거나 다른 상태 지 속성 기술을 통해 페이지의 뷰 상태에 정렬 매개 변수를 저장 하 여 수행할 수 있습니다.

이 자습서의 이후 예제에서는 페이지의 뷰 상태에서 정렬 세부 정보를 유지 하는 방법을 알아봅니다.

## <a name="step-5-adding-sorting-support-to-a-datalist-that-uses-default-paging"></a>5 단계: 기본 페이징을 사용 하는 DataList에 정렬 지원 추가

앞의 [자습서](paging-report-data-in-a-datalist-or-repeater-control-vb.md) 에서는 DataList를 사용 하 여 기본 페이징을 구현 하는 방법을 살펴보았습니다. 에서이 이전 예제를 확장 하 여 페이징된 데이터를 정렬 하는 기능을 포함 하도록 합니다. 먼저 `SortingWithDefaultPaging.aspx`를 열고 `PagingSortingDataListRepeater` 폴더에 있는 페이지를 `Paging.aspx` 합니다. `Paging.aspx` 페이지에서 소스 단추를 클릭 하 여 페이지의 선언적 태그를 확인 합니다. 선택한 텍스트를 복사 하 여 (그림 8 참조) `<asp:Content>` 태그 사이에 `SortingWithDefaultPaging.aspx`의 선언적 태그에 붙여넣습니다.

[&lt;asp: Content&gt; 태그에서 SortingWithDefaultPaging에 선언 된 태그를 ![복제 합니다.](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image21.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image20.png)

**그림 8**: `Paging.aspx` `<asp:Content>` 태그의 선언적 태그를 `SortingWithDefaultPaging.aspx`에 복제 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image22.png))

선언적 태그를 복사한 후에는 `Paging.aspx` 페이지의 코드 숨김으로 된 클래스의 메서드 및 속성을 `SortingWithDefaultPaging.aspx`의 코드 기반 클래스로 복사 합니다. 다음으로 브라우저에서 `SortingWithDefaultPaging.aspx` 페이지를 봅니다. `Paging.aspx`와 동일한 기능 및 모양을 표시 해야 합니다.

## <a name="enhancing-productsbll-to-include-a-default-paging-and-sorting-method"></a>기본 페이징 및 정렬 방법을 포함 하도록 ProductsBLL 향상

이전 자습서에서는 `PagedDataSource` 개체를 반환 하는 `ProductsBLL` 클래스에 `GetProductsAsPagedDataSource(pageIndex, pageSize)` 메서드를 만들었습니다. 이 `PagedDataSource` 개체는 *모든* 제품 (BLL s `GetProducts()` 메서드 사용)으로 채워졌습니다. 그러나 DataList에 바인딩하면 지정 된 *pageIndex* 및 *pageSize* 입력 매개 변수에 해당 하는 레코드만 표시 됩니다.

이 자습서의 앞부분에서는 ObjectDataSource s `Selecting` 이벤트 처리기에서 정렬 식을 지정 하 여 정렬 지원을 추가 했습니다. 이는 `GetProducts()` 메서드에서 반환 하는 `ProductsDataTable` 같이 ObjectDataSource가 정렬할 수 있는 개체를 반환 하는 경우에 효과적입니다. 그러나 `GetProductsAsPagedDataSource` 메서드에서 반환 하는 `PagedDataSource` 개체는 내부 데이터 원본의 정렬을 지원 하지 않습니다. 대신 `PagedDataSource`에 배치 *하기 전에* `GetProducts()` 메서드에서 반환 된 결과를 정렬 해야 합니다.

이를 수행 하려면 `ProductsBLL` 클래스 `GetProductsSortedAsPagedDataSource(sortExpression, pageIndex, pageSize)`에서 새 메서드를 만듭니다. `GetProducts()` 메서드에서 반환 되는 `ProductsDataTable`를 정렬 하려면 기본 `DataTableView`의 `Sort` 속성을 지정 합니다.

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample5.vb)]

`GetProductsSortedAsPagedDataSource` 메서드는 이전 자습서에서 만든 `GetProductsAsPagedDataSource` 메서드와 약간 다릅니다. 특히 `GetProductsSortedAsPagedDataSource`는 추가 입력 매개 변수 `sortExpression` 수락 하 고이 값을 `ProductDataTable` s `DefaultView`의 `Sort` 속성에 할당 합니다. 몇 줄의 코드는 나중에 `PagedDataSource` 개체 데이터 원본에 `ProductDataTable` s `DefaultView`할당 됩니다.

## <a name="calling-the-getproductssortedaspageddatasource-method-and-specifying-the-value-for-the-sortexpression-input-parameter"></a>GetProductsSortedAsPagedDataSource 메서드를 호출 하 고 SortExpression 입력 매개 변수에 대 한 값 지정

`GetProductsSortedAsPagedDataSource` 메서드가 완료 되 면 다음 단계는이 매개 변수에 대 한 값을 제공 하는 것입니다. `SortingWithDefaultPaging.aspx`의 ObjectDataSource는 현재 `GetProductsAsPagedDataSource` 메서드를 호출 하도록 구성 되어 있으며, 두 개의 입력 매개 변수를 `SelectParameters` 컬렉션에 지정 된 두 `QueryStringParameters`를 통해 전달 합니다. 이러한 두 `QueryStringParameters`는 `GetProductsAsPagedDataSource` 메서드의 s *pageIndex* 및 *pageSize* 매개 변수에 대 한 소스가 querystring 필드 `pageIndex` 및 `pageSize`에서 제공 된다는 것을 의미 합니다.

ObjectDataSource s `SelectMethod` 속성이 새 `GetProductsSortedAsPagedDataSource` 메서드를 호출 하도록 업데이트 합니다. 그런 다음 *sortExpression* 입력 매개 변수가 `sortExpression`querystring 필드에서 액세스 되도록 새 `QueryStringParameter`을 추가 합니다. `QueryStringParameter` s `DefaultValue`를 ProductName으로 설정 합니다.

이러한 변경 후에 ObjectDataSource의 선언 태그는 다음과 같습니다.

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample6.aspx)]

이 시점에서 `SortingWithDefaultPaging.aspx` 페이지는 제품 이름을 기준으로 결과를 사전순으로 정렬 합니다 (그림 9 참조). 이는 기본적으로 ProductName의 값이 `GetProductsSortedAsPagedDataSource` 메서드 s *sortExpression* 매개 변수로 전달 되기 때문입니다.

[![기본적으로 결과는 ProductName을 기준으로 정렬 됩니다.](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image24.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image23.png)

**그림 9**: 기본적으로 결과는 `ProductName`를 기준으로 정렬 됩니다 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image25.png)).

`SortingWithDefaultPaging.aspx?sortExpression=CategoryName`와 같은 `sortExpression` querystring 필드를 수동으로 추가 하는 경우 결과는 지정 된 `sortExpression`를 기준으로 정렬 됩니다. 그러나이 `sortExpression` 매개 변수는 데이터의 다른 페이지로 이동할 때 querystring에 포함 되지 않습니다. 실제로 다음 또는 마지막 페이지 단추를 클릭 하면 `Paging.aspx`으로 돌아갑니다. 또한 현재 정렬 인터페이스가 없습니다. 사용자가 페이지 데이터의 정렬 순서를 변경할 수 있는 유일한 방법은 querystring을 직접 조작 하는 것입니다.

## <a name="creating-the-sorting-interface"></a>정렬 인터페이스 만들기

먼저 `RedirectUser` 메서드를 업데이트 하 여 사용자를 `SortingWithDefaultPaging.aspx` (`Paging.aspx`대신)로 보내고 querystring에 `sortExpression` 값을 포함 해야 합니다. 또한 `SortExpression` 속성의 읽기 전용 페이지 수준 이라는 속성을 추가 해야 합니다. 이전 자습서에서 만든 `PageIndex` 및 `PageSize` 속성과 마찬가지로이 속성은 `sortExpression` querystring 필드가 있는 경우 해당 필드의 값을 반환 하 고 그렇지 않은 경우에는 기본값 (ProductName)을 반환 합니다.

현재 `RedirectUser` 메서드는 표시할 페이지의 인덱스를 단일 입력 매개 변수로만 허용 합니다. 그러나 querystring에 지정 된 것 이외의 정렬 식을 사용 하 여 사용자를 특정 데이터 페이지로 리디렉션해야 하는 경우가 있을 수 있습니다. 잠시 후에이 페이지에 대 한 정렬 인터페이스를 만들어 지정 된 열을 기준으로 데이터를 정렬 하는 일련의 단추 웹 컨트롤이 포함 됩니다. 이러한 단추 중 하나를 클릭 하면 적절 한 정렬 식 값을 전달 하는 사용자를 리디렉션해야 합니다. 이 기능을 제공 하려면 `RedirectUser` 메서드의 두 가지 버전을 만듭니다. 첫 번째는 페이지 인덱스만 표시 하 고 두 번째는 페이지 인덱스 및 정렬 식을 허용 하는 것입니다.

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample7.vb)]

이 자습서의 첫 번째 예제에서는 DropDownList을 사용 하 여 정렬 인터페이스를 만들었습니다. 이 예제에서는 `ProductName`를 기준으로 정렬 하기 위해 DataList one 위에 배치 된 세 개의 단추 웹 컨트롤인 `CategoryName`를 사용 하 고 `SupplierName`에 대해 하나를 사용 합니다. 3 개의 단추 웹 컨트롤을 추가 하 고 해당 `ID` 및 `Text` 속성을 적절 하 게 설정 합니다.

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample8.aspx)]

그런 다음 각에 대 한 `Click` 이벤트 처리기를 만듭니다. 이벤트 처리기는 `RedirectUser` 메서드를 호출 하 여 사용자를 적절 한 정렬 식을 사용 하 여 첫 번째 페이지로 반환 해야 합니다.

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample9.vb)]

페이지를 처음 방문할 때 데이터는 사전순으로 제품 이름을 기준으로 정렬 됩니다 (그림 9 참조). 다음 단추를 클릭 하 여 데이터의 두 번째 페이지로 이동한 다음 범주별로 정렬 단추를 클릭 합니다. 이렇게 하면 데이터의 첫 페이지를 범주 이름으로 정렬 하 여 반환 합니다 (그림 10 참조). 마찬가지로, 공급자 기준 정렬 단추를 클릭 하면 데이터의 첫 페이지에서 시작 하 여 공급자가 데이터를 정렬 합니다. 데이터를 페이징할 때 정렬 선택을 기억 합니다. 그림 11에서는 범주별로 정렬 한 후 데이터의 열 세 번째 페이지로 이동 하는 페이지를 보여 줍니다.

[제품이 범주별로 정렬 ![](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image27.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image26.png)

**그림 10**: 제품을 범주별로 정렬 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image28.png))

[데이터를 페이징할 때 정렬 식을 기억 ![](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image30.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image29.png)

**그림 11**: 데이터를 페이징할 때 정렬 식 기억 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image31.png))

## <a name="step-6-custom-paging-through-records-in-a-repeater"></a>6 단계: Repeater에서 레코드를 통한 사용자 지정 페이징

DataList 예제는 비효율적 기본 페이징 기술을 사용 하 여 5 단계 페이지에서 데이터를 통해 검사 했습니다. 충분 한 양의 데이터를 페이징할 때는 사용자 지정 페이징이 반드시 사용 되어야 합니다. [많은 양의 데이터를 효율적으로 페이징](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb.md) 하 고 [사용자 지정 페이징 데이터를 정렬](../paging-and-sorting/sorting-custom-paged-data-vb.md) 하는 방법으로 돌아가서 사용자 지정 페이징 및 사용자 지정 페이징 데이터 정렬을 위해 BLL의 기본 및 사용자 지정 페이징 및 만든 메서드 간의 차이점을 검사 했습니다. 특히이 두 가지 이전 자습서에서는 다음 세 가지 메서드를 `ProductsBLL` 클래스에 추가 했습니다.

- `GetProductsPaged(startRowIndex, maximumRows)`는 *Startrowindex* 에서 시작 하 여 *maximumrows*를 초과 하지 않는 레코드의 특정 하위 집합을 반환 합니다.
- `GetProductsPagedAndSorted(sortExpression, startRowIndex, maximumRows)`는 지정 된 *sortExpression* 입력 매개 변수를 기준으로 정렬 된 레코드의 특정 하위 집합을 반환 합니다.
- `TotalNumberOfProducts()` `Products` 데이터베이스 테이블의 총 레코드 수를 제공 합니다.

이러한 메서드를 사용 하 여 DataList 또는 Repeater 컨트롤을 통해 데이터를 효율적으로 페이징 하 고 정렬할 수 있습니다. 이를 설명 하기 위해 사용자 지정 페이징 지원을 사용 하 여 Repeater 컨트롤을 만드는 것으로 시작 하겠습니다. 그런 다음 정렬 기능을 추가 합니다.

`PagingSortingDataListRepeater` 폴더에서 `SortingWithCustomPaging.aspx` 페이지를 열고 `ID` 속성을 `Products`로 설정 하 여 페이지에 Repeater를 추가 합니다. Repeater s 스마트 태그에서 `ProductsDataSource`라는 새 ObjectDataSource를 만듭니다. `ProductsBLL` 클래스의 `GetProductsPaged` 메서드에서 데이터를 선택 하도록 구성 합니다.

[ProductsBLL 클래스 s Get 메서드를 사용 하도록 ObjectDataSource 구성 ![](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image33.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image32.png)

**그림 12**: `ProductsBLL` 클래스 s `GetProductsPaged` 메서드를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image34.png))

업데이트, 삽입 및 삭제 탭의 드롭다운 목록을 (없음)로 설정 하 고 다음 단추를 클릭 합니다. 이제 데이터 원본 구성 마법사는 `GetProductsPaged` 메서드 s *Startrowindex* 및 *maximumrows* 입력 매개 변수의 출처를 묻는 메시지를 표시 합니다. 실제로 이러한 입력 매개 변수는 무시 됩니다. 대신 *Startrowindex* 및 *maximumrows* 값은이 자습서의 첫 번째 데모에서 *SortExpression* 를 지정한 방법과 마찬가지로 ObjectDataSource s `Selecting` 이벤트 처리기의 `Arguments` 속성을 통해 전달 됩니다. 따라서 마법사에서 매개 변수 원본 드롭다운 목록을 None으로 설정 된 상태로 둡니다.

[매개 변수 소스가 None으로 설정 된 상태로 유지 ![](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image36.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image35.png)

**그림 13**: 매개 변수 원본을 None으로 설정 된 상태로 유지 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image37.png))

> [!NOTE]
> ObjectDataSource s `EnablePaging` 속성을 `true`로 설정 *하지* 마십시오. 이렇게 하면 ObjectDataSource에서 자체 *Startrowindex* 및 *maximumrows* 매개 변수를 `SelectMethod`의 기존 매개 변수 목록에 자동으로 포함 시킵니다. `EnablePaging` 속성은 사용자 지정 페이징된 데이터를 GridView, DetailsView 또는 FormView 컨트롤에 바인딩하는 경우에 유용 합니다. 이러한 컨트롤은 `EnablePaging` 속성이 `true`때만 사용 가능한 ObjectDataSource의 특정 동작을 필요로 하기 때문입니다. DataList 및 Repeater에 대해 페이징 지원을 수동으로 추가 해야 하므로 ASP.NET 페이지 내에서 직접 필요한 기능을 굽기이 속성을 `false` (기본값)로 설정 된 상태로 둡니다.

마지막으로, 제품 이름, 범주 및 공급자가 표시 되도록 반복 `ItemTemplate`를 정의 합니다. 이러한 변경 후에는 Repeater 및 ObjectDataSource s 선언 구문이 다음과 같이 표시 됩니다.

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample10.aspx)]

잠시 시간을 내 서 브라우저를 통해 페이지를 방문 하면 레코드가 반환 되지 않습니다. 이는 *Startrowindex* 및 *maximumrows* 매개 변수 값을 지정 하기 위한 것 이기 때문입니다. 따라서 0의 값은 둘 다에 대해 전달 됩니다. 이러한 값을 지정 하려면 ObjectDataSource s `Selecting` 이벤트에 대 한 이벤트 처리기를 만들고 이러한 매개 변수 값을 프로그래밍 방식으로 0과 5의 하드 코딩 된 값으로 설정 합니다.

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample11.vb)]

이 변경 내용으로 브라우저를 통해 볼 때 페이지에는 처음 5 개 제품이 표시 됩니다.

[처음 5 개 레코드가 표시 ![](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image39.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image38.png)

**그림 14**: 처음 5 개 레코드가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image40.png)).

> [!NOTE]
> 효율적인 사용자 지정 페이징 쿼리를 수행 하는 `GetProductsPaged` 저장 프로시저에서 `ProductName`여 결과를 정렬 하기 때문에 그림 14에 나열 된 제품은 제품 이름별로 정렬 됩니다.

사용자가 페이지를 단계별로 실행할 수 있도록 하기 위해 시작 행 인덱스 및 최대 행을 추적 하 고 다시 게시 간에 이러한 값을 기억해 야 합니다. 기본 페이징 예제에서는 querystring 필드를 사용 하 여 이러한 값을 유지 했습니다. 이 데모에서는 페이지의 뷰 상태에이 정보를 저장 합니다. 다음 두 가지 속성을 만듭니다.

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample12.vb)]

다음으로, `StartRowIndex`를 사용 하 고 하드 코드 된 값 0과 5 대신 `MaximumRows` 속성을 사용 하도록 선택 하는 이벤트 처리기의 코드를 업데이트 합니다.

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample13.vb)]

이 시점에서 페이지에는 처음 5 개의 레코드만 표시 됩니다. 그러나 이러한 속성이 준비 되 면 페이징 인터페이스를 만들 준비가 된 것입니다.

## <a name="adding-the-paging-interface"></a>페이징 인터페이스 추가

는 표시 되는 데이터 페이지 및 총 페이지 수를 표시 하는 레이블 웹 컨트롤을 포함 하 여 기본 페이징 예제에서 사용 되는 동일한 첫 번째, 이전, 다음의 마지막 페이징 인터페이스를 사용 합니다. 네 개의 단추 웹 컨트롤과 레이블을 Repeater 아래에 추가 합니다.

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample14.aspx)]

다음에는 네 개의 단추에 대 한 `Click` 이벤트 처리기를 만듭니다. 이러한 단추 중 하나를 클릭 하면 `StartRowIndex`를 업데이트 하 고 데이터를 Repeater에 다시 바인딩해야 합니다. 첫 번째, 이전 및 다음 단추에 대 한 코드는 충분히 간단 하지만 마지막 단추는 데이터의 마지막 페이지에 대 한 시작 행 인덱스를 결정 하는 방법 이 인덱스를 계산 하 고 다음 및 마지막 단추를 사용 하도록 설정 해야 하는지 여부를 결정할 수 있도록 하려면 전체에서 페이징 하는 레코드 수를 알아야 합니다. `ProductsBLL` 클래스 s `TotalNumberOfProducts()` 메서드를 호출 하 여이를 확인할 수 있습니다. `TotalNumberOfProducts()` 메서드의 결과를 반환 하는 `TotalRowCount` 라는 읽기 전용 페이지 수준 속성을 만듭니다.

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample15.vb)]

이제이 속성을 사용 하 여 마지막 페이지의 시작 행 인덱스를 확인할 수 있습니다. 특히 `TotalRowCount` 1을 뺀 값의 정수 결과를 `MaximumRows`으로 나눈 값을 `MaximumRows`에 곱합니다. 이제 네 가지 페이징 인터페이스 단추에 대 한 `Click` 이벤트 처리기를 작성할 수 있습니다.

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample16.vb)]

마지막으로 데이터의 첫 페이지를 볼 때 페이징 인터페이스에서 첫 번째 및 이전 단추를 사용 하지 않도록 설정 하 고 마지막 페이지를 볼 때 다음 및 마지막 단추를 사용 하지 않도록 설정 해야 합니다. 이 작업을 수행 하려면 ObjectDataSource s `Selecting` 이벤트 처리기에 다음 코드를 추가 합니다.

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample17.vb)]

이러한 `Click` 이벤트 처리기와 코드를 추가 하 여 현재 시작 행 인덱스를 기반으로 페이징 인터페이스 요소를 사용 하거나 사용 하지 않도록 설정한 후 브라우저에서 페이지를 테스트 합니다. 그림 15에 설명 된 것 처럼 페이지를 처음 방문할 때 첫 번째 단추와 이전 단추가 사용 하지 않도록 설정 됩니다. 다음을 클릭 하면 두 번째 데이터 페이지가 표시 되 고 마지막을 클릭 하면 마지막 페이지가 표시 됩니다 (그림 16 및 17 참조). 데이터의 마지막 페이지를 볼 때 다음 및 마지막 단추를 모두 사용할 수 없습니다.

[제품의 첫 페이지를 볼 때 이전 및 마지막 단추가 사용 하지 않도록 설정 된 ![](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image42.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image41.png)

**그림 15**: 제품의 첫 페이지를 볼 때 이전 및 마지막 단추를 사용할 수 없는 경우 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image43.png))

[![제품의 두 번째 페이지가 표시 됩니다.](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image45.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image44.png)

**그림 16**: 제품의 두 번째 페이지가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image46.png)).

[마지막 클릭 ![데이터의 마지막 페이지를 표시 합니다.](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image48.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image47.png)

**그림 17**: 마지막 클릭 데이터의 마지막 페이지를 표시 합니다 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image49.png)).

## <a name="step-7-including-sorting-support-with-the-custom-paged-repeater"></a>7 단계: 사용자 지정 페이징 Repeater를 사용 하 여 정렬 지원 포함

이제 사용자 지정 페이징이 구현 되었으므로 정렬 지원을 포함할 준비가 되었습니다. `ProductsBLL` 클래스 s `GetProductsPagedAndSorted` 메서드는 `GetProductsPaged`와 동일한 *Startrowindex* 및 *maximumrows* 입력 매개 변수를 갖지만 추가 *sortExpression* 입력 매개 변수를 허용 합니다. `SortingWithCustomPaging.aspx`에서 `GetProductsPagedAndSorted` 메서드를 사용 하려면 다음 단계를 수행 해야 합니다.

1. ObjectDataSource s `SelectMethod` 속성을 `GetProductsPaged`에서 `GetProductsPagedAndSorted`로 변경 합니다.
2. *SortExpression* `Parameter` 개체를 ObjectDataSource s `SelectParameters` 컬렉션에 추가 합니다.
3. 페이지의 뷰 상태를 통해 다시 게시 간에 값을 유지 하는 개인 페이지 수준 `SortExpression` 속성을 만듭니다.
4. Objectdatasource s `Selecting` 이벤트 처리기를 업데이트 하 여 ObjectDataSource s *sortExpression* 매개 변수에 페이지 수준 `SortExpression` 속성 값을 할당 합니다.
5. 정렬 인터페이스를 만듭니다.

먼저 ObjectDataSource s `SelectMethod` 속성을 업데이트 하 고 *sortExpression* `Parameter`를 추가 합니다. *SortExpression* `Parameter` s `Type` 속성이 `String`으로 설정 되어 있는지 확인 합니다. 이러한 처음 두 가지 작업을 완료 한 후 ObjectDataSource의 선언 태그는 다음과 같습니다.

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample18.aspx)]

그 다음에는 값이 표시 되도록 serialize 된 페이지 수준 `SortExpression` 속성이 필요 합니다. 정렬 식 값이 설정 되지 않은 경우 ProductName을 기본값으로 사용 합니다.

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample19.vb)]

ObjectDataSource가 `GetProductsPagedAndSorted` 메서드를 호출 하기 전에 *sortExpression* `Parameter`을 `SortExpression` 속성 값으로 설정 해야 합니다. `Selecting` 이벤트 처리기에서 다음 코드 줄을 추가 합니다.

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample20.vb)]

모든 것은 정렬 인터페이스를 구현 하는 것입니다. 마지막 예제에서와 같이 사용자가 제품 이름, 범주 또는 공급자를 기준으로 결과를 정렬할 수 있도록 하는 세 개의 단추 웹 컨트롤을 사용 하 여 정렬 인터페이스를 구현 해 보겠습니다.

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample21.aspx)]

이러한 세 가지 단추 컨트롤에 대 한 `Click` 이벤트 처리기를 만듭니다. 이벤트 처리기에서 `StartRowIndex`를 0으로 다시 설정 하 고, `SortExpression`를 적절 한 값으로 설정 하 고, 데이터를 Repeater에 다시 바인딩합니다.

[!code-vb[Main](sorting-data-in-a-datalist-or-repeater-control-vb/samples/sample22.vb)]

이것이 전부입니다! 사용자 지정 페이징 및 정렬을 구현 하는 단계가 많이 있지만,이 단계는 기본 페이징에 필요한 단계와 매우 비슷합니다. 그림 18은 범주별로 정렬 될 때 데이터의 마지막 페이지를 볼 때의 제품을 보여 줍니다.

[범주별로 정렬 된 마지막 데이터 페이지 ![표시 됩니다.](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image51.png)](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image50.png)

**그림 18**: 범주별로 정렬 된 마지막 데이터 페이지가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](sorting-data-in-a-datalist-or-repeater-control-vb/_static/image52.png)).

> [!NOTE]
> 이전 예제에서 공급자 SupplierName를 기준으로 정렬 하는 것이 정렬 식으로 사용 되었습니다. 그러나 사용자 지정 페이징 구현에는 CompanyName을 사용 해야 합니다. 이는 사용자 지정 페이징 `GetProductsPagedAndSorted` 구현을 담당 하는 저장 프로시저가 `ROW_NUMBER()` 키워드에 정렬 식을 전달 하기 때문입니다. `ROW_NUMBER()` 키워드에는 별칭이 아닌 실제 열 이름이 필요 하기 때문입니다. 따라서 `CompanyName` (`Suppliers` 테이블의 열 이름)을 사용 해야 합니다. 정렬 식의 `SELECT` 쿼리 (`SupplierName`)에 사용 되는 별칭이 아닙니다.

## <a name="summary"></a>요약

DataList 나 Repeater는 기본 제공 되는 정렬을 지원 하지 않지만 약간의 코드와 사용자 지정 정렬 인터페이스를 사용 하 여 이러한 기능을 추가할 수 있습니다. 정렬을 구현할 때 페이징이 아닌 경우 ObjectDataSource s `Select` 메서드에 전달 된 `DataSourceSelectArguments` 개체를 통해 정렬 식을 지정할 수 있습니다. 이 `DataSourceSelectArguments` 개체 `SortExpression` 속성은 ObjectDataSource s `Selecting` 이벤트 처리기에서 할당할 수 있습니다.

이미 페이징 지원을 제공 하는 DataList 또는 Repeater에 정렬 기능을 추가 하려면 정렬 식을 허용 하는 메서드를 포함 하도록 비즈니스 논리 계층을 사용자 지정 하는 것이 가장 쉬운 방법입니다. 그러면이 정보를 ObjectDataSource s `SelectParameters`의 매개 변수를 통해 전달할 수 있습니다.

이 자습서에서는 DataList 및 Repeater 컨트롤을 사용한 페이징 및 정렬에 대 한 검사를 완료 합니다. 다음 및 최종 자습서에서는 항목 별로 사용자가 시작 하는 사용자 지정 기능을 제공 하기 위해 DataList 및 Repeater s 템플릿에 단추 웹 컨트롤을 추가 하는 방법을 살펴봅니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 David Suru입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](paging-report-data-in-a-datalist-or-repeater-control-vb.md)
