---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-vb
title: 데이터에 따라 DataList 및 Repeater 서식 지정 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 ...로 서식 지정 함수를 사용 하 여 DataList 및 Repeater 컨트롤의 모양을 지정 하는 방법에 대 한 예제를 단계별로 설명 합니다.
ms.author: riande
ms.date: 09/13/2006
ms.assetid: e2f401ae-37bb-4b19-aa97-d6b385d40f88
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-vb
msc.type: authoredcontent
ms.openlocfilehash: c9b60e4dacd992962942034e84c01cb82e039c81
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78508097"
---
# <a name="formatting-the-datalist-and-repeater-based-upon-data-vb"></a>데이터를 기반으로 DataList 및 반복기 서식 지정(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_30_VB.exe) 또는 [PDF 다운로드](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/datatutorial30vb1.pdf)

> 이 자습서에서는 템플릿 내에서 형식 지정 함수를 사용 하거나 데이터 바인딩된 이벤트를 처리 하 여 DataList 및 Repeater 컨트롤의 모양을 지정 하는 방법에 대 한 예제를 단계별로 설명 합니다.

## <a name="introduction"></a>소개

위의 자습서에서 살펴본 것 처럼 DataList는 모양에 영향을 주는 다양 한 스타일 관련 속성을 제공 합니다. 특히 DataList s `HeaderStyle`, `ItemStyle`, `AlternatingItemStyle`및 `SelectedItemStyle` 속성에 기본 CSS 클래스를 할당 하는 방법을 살펴보았습니다. 이러한 네 가지 속성 외에도 DataList에는 `Font`, `ForeColor`, `BackColor`, `BorderWidth`등의 여러 가지 다른 스타일 관련 속성이 포함 되어 있습니다. Repeater 컨트롤에는 스타일 관련 속성이 포함 되어 있지 않습니다. 이러한 스타일 설정은 Repeater 템플릿의 태그 내에서 직접 수행 해야 합니다.

그러나 데이터의 형식을 지정 하는 방법은 데이터 자체에 따라 달라 집니다. 예를 들어 제품을 나열 하는 경우 제품 정보를 밝은 회색 글꼴 색으로 표시 하는 것이 좋습니다. 그렇지 않으면 0 인 경우 `UnitsInStock` 값을 강조 표시할 수 있습니다. 이전 자습서에서 살펴본 것 처럼 GridView, DetailsView 및 FormView는 데이터에 따라 모양을 지정 하는 두 가지 고유한 방법을 제공 합니다.

- **`DataBound` 이벤트는** 데이터를 각 항목에 바인딩한 후에 발생 하는 적절 한 `DataBound` 이벤트에 대 한 이벤트 처리기를 만듭니다 .이 이벤트는 GridView가 `RowDataBound` 이벤트 였던 경우에 발생 합니다. DataList 및 Repeater는 `ItemDataBound` 이벤트입니다. 이 이벤트 처리기에서 방금 바인딩된 데이터를 검사 하 고 형식을 결정할 수 있습니다. 데이터 자습서에 [따라 사용자 지정 서식 지정](../custom-formatting/custom-formatting-based-upon-data-vb.md) 에서이 기법을 검토 했습니다.
- **템플릿의 서식 지정 함수** DetailsView 또는 GridView 컨트롤에서 템플릿 필드를 사용할 때 또는 FormView 컨트롤의 템플릿에 서식 지정 함수를 추가할 수 있습니다. ASP.NET 페이지의 코드 숨겨진 클래스, 비즈니스 논리 계층 또는 웹 응용 프로그램에서 액세스할 수 있는 다른 클래스 라이브러리에 서식 함수를 추가할 수 있습니다. 이 서식 지정 함수는 임의의 수의 입력 매개 변수를 사용할 수 있지만 템플릿에서 렌더링할 HTML을 반환 해야 합니다. 서식 지정 함수는 [GridView 컨트롤 자습서의 템플릿 사용 필드](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md) 에서 먼저 검사 되었습니다.

이러한 서식 지정 기법은 DataList 및 Repeater 컨트롤에서 사용할 수 있습니다. 이 자습서에서는 두 가지 방법을 모두 사용 하 여 예제를 단계별로 안내 합니다.

## <a name="using-theitemdataboundevent-handler"></a>`ItemDataBound`이벤트 처리기 사용

데이터 소스 컨트롤이 나 컨트롤 `DataSource` 속성에 데이터를 프로그래밍 방식으로 할당 하 고 해당 `DataBind()` 메서드를 호출 하 여 데이터를 DataList에 바인딩하면 DataList s `DataBinding` 이벤트가 발생 하 고, 데이터 소스가 열거 되며, 각 데이터 레코드가 DataList에 바인딩됩니다. 데이터 소스의 각 레코드에 대해 DataList는 [`DataListItem`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalistitem.aspx) 개체를 만든 다음 현재 레코드에 바인딩됩니다. 이 과정에서 DataList는 다음과 같은 두 이벤트를 발생 시킵니다.

- `DataListItem`를 만든 후에 **`ItemCreated`** 발생 합니다.
- 현재 레코드가 `DataListItem`에 바인딩된 후에 **`ItemDataBound`** 발생 합니다.

다음 단계에서는 DataList 컨트롤의 데이터 바인딩 프로세스를 간략하게 설명 합니다.

1. DataList s [`DataBinding` 이벤트가](https://msdn.microsoft.com/library/system.web.ui.control.databinding.aspx) 발생 합니다.
2. 데이터는 DataList에 바인딩됩니다.  
  
   데이터 원본의 각 레코드에 대해 

    1. `DataListItem` 개체 만들기
    2. [`ItemCreated` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.itemcreated.aspx) 를 발생 시킵니다.
    3. 레코드를 `DataListItem`에 바인딩
    4. [`ItemDataBound` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.itemdatabound.aspx) 를 발생 시킵니다.
    5. `Items` 컬렉션에 `DataListItem` 추가

Repeater 컨트롤에 데이터를 바인딩할 때 동일한 일련의 단계를 진행 합니다. 유일한 차이점은 `DataListItem` 인스턴스가 생성 되는 대신, Repeater는 [`RepeaterItem`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeateritem(VS.80).aspx)s를 사용 한다는 것입니다.

> [!NOTE]
> Astute reader는 데이터에 데이터에 바인딩될 때 DataList 및 Repeater가 데이터에 바인딩될 때 수행 되는 단계 시퀀스 사이에 약간의 비정상을 발견할 수 있습니다. 데이터 바인딩 프로세스의 비상 끝에서 GridView는 `DataBound` 이벤트를 발생 시킵니다. 그러나 DataList 또는 Repeater 컨트롤에는 이러한 이벤트가 없습니다. 이는 ASP.NET 1. x 시간 안에 DataList 및 Repeater 컨트롤이 다시 만들어졌으므로 사전 및 사후 수준 이벤트 처리기 패턴이 보편화 되기 때문입니다.

GridView와 마찬가지로 데이터를 기반으로 서식을 지정 하는 한 가지 옵션은 `ItemDataBound` 이벤트에 대 한 이벤트 처리기를 만드는 것입니다. 이 이벤트 처리기는 `DataListItem` 또는 `RepeaterItem`에만 바인딩된 데이터를 검사 하 고 필요에 따라 컨트롤의 서식에 영향을 줍니다.

DataList 컨트롤의 경우 표준 `Font`, `ForeColor`, `BackColor`, `CssClass`등을 포함 하는 `DataListItem`의 스타일 관련 속성을 사용 하 여 전체 항목에 대 한 서식 지정 변경을 구현할 수 있습니다. DataList의 템플릿 내에서 특정 웹 컨트롤의 형식에 영향을 주려면 이러한 웹 컨트롤의 스타일을 프로그래밍 방식으로 액세스 하 고 수정 해야 합니다. 데이터 자습서에 *따라 사용자 지정 서식 지정* 에서이를 다시 수행 하는 방법을 살펴보았습니다. Repeater 컨트롤과 마찬가지로 `RepeaterItem` 클래스에는 스타일 관련 속성이 없습니다. 따라서 `ItemDataBound` 이벤트 처리기의 `RepeaterItem`에 대 한 모든 스타일 관련 변경 내용은 프로그래밍 방식으로 템플릿 내에서 웹 컨트롤에 액세스 하 고 업데이트 하 여 수행 해야 합니다.

DataList 및 Repeater의 `ItemDataBound` 서식 지정 기법은 거의 동일 하므로 예제에서는 DataList를 사용 하는 데 중점을 둡니다.

## <a name="step-1-displaying-product-information-in-the-datalist"></a>1 단계: DataList에서 제품 정보 표시

서식 지정에 대해 걱정 하기 전에 먼저 DataList를 사용 하 여 제품 정보를 표시 하는 페이지를 만들어 보겠습니다. [이전 자습서](displaying-data-with-the-datalist-and-repeater-controls-vb.md) 에서는 `ItemTemplate` 각 제품 이름, 범주, 공급자, 단위당 수량 및 가격을 표시 하는 DataList를 만들었습니다. 이 자습서의 여기에서이 기능을 반복 해 보세요. 이렇게 하려면 DataList와 ObjectDataSource를 처음부터 다시 만들거나 이전 자습서에서 만든 페이지 (`Basics.aspx`)에서 해당 컨트롤을 복사 하 여이 자습서의 페이지 (`Formatting.aspx`)에 붙여 넣을 수 있습니다.

`Basics.aspx`에서 DataList 및 ObjectDataSource 기능을 `Formatting.aspx`로 복제 한 후에는 `ID` 속성을 `DataList1`에서 더 설명적인 `ItemDataBoundFormattingExample`으로 변경 합니다. 다음으로, 브라우저에서 DataList를 봅니다. 그림 1에 나와 있는 것 처럼 각 제품의 형식 차이는 배경색을 대체 하기 위한 것입니다.

[![는 제품이 DataList 컨트롤에 나열 됩니다.](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image2.png)](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image1.png)

**그림 1**:이 제품은 DataList 컨트롤 ([전체 크기 이미지를 보려면 클릭](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image3.png))에 나열 되어 있습니다.

이 자습서에서는 가격이 $20.00 미만인 제품의 이름과 단가가 모두 노란색으로 강조 표시 되도록 DataList의 형식을 지정 합니다.

## <a name="step-2-programmatically-determining-the-value-of-the-data-in-the-itemdatabound-event-handler"></a>2 단계: ItemDataBound 바인딩된 이벤트 처리기에서 프로그래밍 방식으로 데이터 값 확인

가격이 $20.00 미만 인 제품만 사용자 지정 서식 지정이 적용 되므로 각 제품의 가격을 확인할 수 있어야 합니다. DataList에 데이터를 바인딩할 때 DataList는 데이터 원본에 있는 레코드를 열거 하 고 각 레코드에 대해 `DataListItem` 인스턴스를 만들어 데이터 원본 레코드를 `DataListItem`에 바인딩합니다. 특정 레코드의 데이터가 현재 `DataListItem` 개체에 바인딩된 후에는 DataList s `ItemDataBound` 이벤트가 발생 합니다. 이 이벤트에 대 한 이벤트 처리기를 만들어 현재 `DataListItem`의 데이터 값을 검사 하 고, 이러한 값에 따라 형식 변경을 수행 하는 데 필요한 값을 확인할 수 있습니다.

DataList에 대 한 `ItemDataBound` 이벤트를 만들고 다음 코드를 추가 합니다.

[!code-vb[Main](formatting-the-datalist-and-repeater-based-upon-data-vb/samples/sample1.vb)]

DataList s `ItemDataBound` 이벤트 처리기의 개념 및 의미 체계는 데이터 자습서에 *따라 사용자 지정 서식 지정* 에서 GridView s `RowDataBound` 이벤트 처리기에서 사용 하는 것과 동일 하지만 구문은 약간 다릅니다. `ItemDataBound` 이벤트가 발생 하면 데이터에 바인딩되는 `DataListItem` `e.Item`를 통해 해당 이벤트 처리기로 전달 됩니다 `e.Row`(예를 들어, GridView s `RowDataBound` 이벤트 처리기와 마찬가지로). DataList s `ItemDataBound` 이벤트 처리기는 머리글 행, 바닥글 행 및 구분 기호 행을 포함 하 여 DataList에 추가 된 *각* 행에 대해 발생 합니다. 그러나 제품 정보는 데이터 행에만 바인딩됩니다. 따라서 `ItemDataBound` 이벤트를 사용 하 여 DataList에 바인딩된 데이터를 검사 하는 경우 먼저 데이터 항목을 다시 사용 하 고 있는지 확인 해야 합니다. 이 작업을 수행 하려면 [다음 8 개 값](https://msdn.microsoft.com/library/system.web.ui.webcontrols.listitemtype.aspx)중 하나를 사용할 수 있는 `DataListItem` s [`ItemType` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalistitem.itemtype.aspx)을 확인 하면 됩니다.

- `AlternatingItem`
- `EditItem`
- `Footer`
- `Header`
- `Item`
- `Pager`
- `SelectedItem`
- `Separator`

`Item`와 `AlternatingItem``DataListItem`는 모두 DataList s 데이터 항목을 구성을 합니다. `Item` 또는 `AlternatingItem`를 사용 하 여 작업을 다시 수행 한다고 가정 하 고 현재 `DataListItem`에 바인딩된 실제 `ProductsRow` 인스턴스에 액세스 합니다. `DataListItem` s [`DataItem` 속성](https://msdn.microsoft.com/system.web.ui.webcontrols.datalistitem.dataitem.aspx) 에는 `DataRowView` 개체에 대 한 참조가 포함 되어 있으며, 해당 `Row` 속성은 실제 `ProductsRow` 개체에 대 한 참조를 제공 합니다.

다음으로 `ProductsRow` 인스턴스 `UnitPrice` 속성을 확인 합니다. Products 테이블 s `UnitPrice` 필드는 `NULL` 값을 허용 하므로 `UnitPrice` 속성에 액세스 하기 전에 먼저 `IsUnitPriceNull()` 메서드를 사용 하 여 `NULL` 값이 있는지 확인 해야 합니다. `UnitPrice` 값이 `NULL`되지 않은 경우 $20.00 보다 작음을 확인 합니다. 실제로 $20.00 아래에 있는 경우 사용자 지정 서식 지정을 적용 해야 합니다.

## <a name="step-3-highlighting-the-product-s-name-and-price"></a>3 단계: 제품 이름 및 가격 강조 표시

제품 가격이 $20.00 미만 이라는 것을 확인 한 후에는 이름 및 가격을 강조 표시 하기만 하면 됩니다. 이를 위해 먼저 제품 이름 및 가격을 표시 하는 `ItemTemplate`에서 레이블 컨트롤을 프로그래밍 방식으로 참조 해야 합니다. 다음에는 노란색 배경을 표시 해야 합니다. 이러한 서식 지정 정보는`LabelID.BackColor = Color.Yellow`(레이블 `BackColor` 속성)를 직접 수정 하 여 적용할 수 있습니다. 하지만 모든 표시 관련 문제는 연계 스타일 시트를 통해 표현 해야 합니다. 실제로는 `Styles.css` - `AffordablePriceEmphasis`에 정의 된 원하는 서식을 제공 하는 스타일 시트를 이미 사용 하 고 있습니다 .이 스타일 시트는 *데이터 자습서에 따라 사용자 지정 서식 지정* 에서 작성 및 설명 합니다.

서식 지정을 적용 하려면 다음 코드에 표시 된 것 처럼 두 개의 Label 웹 컨트롤 `CssClass` 속성을 `AffordablePriceEmphasis`로 설정 하면 됩니다.

[!code-vb[Main](formatting-the-datalist-and-repeater-based-upon-data-vb/samples/sample2.vb)]

`ItemDataBound` 이벤트 처리기가 완료 되 면 브라우저에서 `Formatting.aspx` 페이지를 다시 방문 합니다. 그림 2에 나와 있는 것 처럼 가격이 $20.00 인 제품의 이름과 가격은 모두 강조 표시 됩니다.

[$20.00 미만의 제품이 강조 표시 된 ![](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image5.png)](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image4.png)

**그림 2**: $20.00 미만의 제품이 강조 표시 됨 ([전체 크기 이미지를 보려면 클릭](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image6.png))

> [!NOTE]
> DataList는 HTML `<table>`렌더링 되므로 해당 `DataListItem` 인스턴스에는 전체 항목에 특정 스타일을 적용 하기 위해 설정할 수 있는 스타일 관련 속성이 있습니다. 예를 들어 가격이 $20.00 미만이 면 *전체* 항목을 강조 표시 하려는 경우 레이블을 참조 하는 코드를 대체 하 고 `CssClass` 속성을 다음 코드 줄로 설정할 수 있습니다. `e.Item.CssClass = "AffordablePriceEmphasis"` (그림 3 참조).

그러나 Repeater 컨트롤을 구성 하는 `RepeaterItem`는 이러한 스타일 수준 속성을 제공 하지 않습니다. 따라서 사용자 지정 서식을 Repeater에 적용 하려면 그림 2에서 했던 것 처럼 Repeater의 템플릿 내에서 웹 컨트롤에 대 한 스타일 속성의 응용 프로그램이 필요 합니다.

[![$20.00 아래의 제품에 대해 전체 제품 항목이 강조 표시 됩니다.](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image8.png)](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image7.png)

**그림 3**: $20.00의 제품에 대 한 전체 제품 항목 강조 표시 ([전체 크기 이미지를 보려면 클릭](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image9.png))

## <a name="using-formatting-functions-from-within-the-template"></a>템플릿 내에서 서식 함수 사용

Gridview *컨트롤의 템플릿 필드 사용* 자습서에서는 gridview templatefield로 변환 내에서 서식 함수를 사용 하 여 gridview의 행에 바인딩된 데이터에 따라 사용자 지정 서식을 적용 하는 방법을 살펴보았습니다. 서식 지정 함수는 템플릿에서 호출할 수 있는 메서드 이며 그 자리에 내보낼 HTML을 반환 합니다. 서식 지정 함수는 ASP.NET 페이지의 코드 숨김이 클래스에 상주할 수도 있고, `App_Code` 폴더나 별도의 클래스 라이브러리 프로젝트에 있는 클래스 파일에 중앙 집중화 될 수도 있습니다. 여러 ASP.NET 페이지 또는 다른 ASP.NET 웹 응용 프로그램에서 동일한 서식 지정 함수를 사용 하도록 계획 하는 경우 ASP.NET 페이지의 코드 숨김으로 서식 지정 함수를 이동 하는 것이 적합 합니다.

서식 지정 함수를 보여 주기 위해 제품 정보에 제품 이름 옆에 있는 [중단] 텍스트 (단종 된 텍스트)를 포함 하도록 합니다. 또한 `ItemDataBound` 이벤트 처리기 예제에서와 같이 $20.00 보다 작은 경우에는 가격이 노란색으로 강조 표시 되도록 합니다. 가격이 $20.00 이상인 경우에는를 사용 하 여 실제 가격을 표시 하지 않고 텍스트 대신 가격 견적에 대해를 호출 해 보세요. 그림 4에서는 이러한 서식 규칙이 적용 된 제품의 스크린샷을 보여 줍니다.

[비용이 많이 드는 제품에 대 한 ![가격은 텍스트로 바뀌고 가격 견적에 대해를 호출 하세요.](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image11.png)](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image10.png)

**그림 4**: 비용이 많이 드는 제품의 경우 가격은 텍스트로 바뀌고 통화에 대해를 호출 하세요 ([전체 크기 이미지를 보려면 클릭](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image12.png)).

## <a name="step-1-create-the-formatting-functions"></a>1 단계: 서식 지정 함수 만들기

이 예제에서는 두 가지 형식 지정 함수를 사용 합니다. 하나는 [단종 됨] 텍스트와 함께 제품 이름을 표시 하 고, 필요한 경우에는 강조 표시 된 가격이 $20.00 보다 작은 경우에는 강조 표시 된 가격을 표시 하 고, 그렇지 않은 경우에는를 호출 하 여 해당 하는 경우에는를 호출 하세요 ASP.NET 페이지의 코드 숨김이 클래스에서 이러한 함수를 만들고 `DisplayProductNameAndDiscontinuedStatus` 하 고 `DisplayPrice`이름을 지정 합니다. 두 메서드는 모두 문자열로 렌더링할 HTML을 반환 해야 하며, ASP.NET 페이지의 선언적 구문 부분에서 호출 하기 위해 둘 다 `Protected` (또는 `Public`)로 표시 되어야 합니다. 이러한 두 메서드의 코드는 다음과 같습니다.

[!code-vb[Main](formatting-the-datalist-and-repeater-based-upon-data-vb/samples/sample3.vb)]

`DisplayProductNameAndDiscontinuedStatus` 메서드는 `productName` 및 `discontinued` 데이터 필드의 값을 스칼라 값으로 수락 하는 반면 `DisplayPrice` 메서드는 `ProductsRow` 스칼라 값이 아닌 `unitPrice` 인스턴스를 허용 합니다. 어느 방법이 든 작동 합니다. 그러나 형식 지정 함수가 데이터베이스 `NULL` 값을 포함할 수 있는 스칼라 값을 사용 하는 경우 (예: `UnitPrice`, `ProductName` 또는 `Discontinued` `NULL` 값을 허용 하지 않음) 이러한 스칼라 입력을 처리할 때 특별히 주의 해야 합니다.

특히 들어오는 값은 필요한 데이터 형식이 아닌 `DBNull` 인스턴스일 수 있으므로 입력 매개 변수는 `Object` 형식 이어야 합니다. 또한 들어오는 값이 데이터베이스 `NULL` 값 인지 여부를 확인 하는 검사를 수행 해야 합니다. 즉, `DisplayPrice` 메서드를 사용 하 여 가격을 스칼라 값으로 적용 하려는 경우에는 다음 코드를 사용 해야 합니다.

[!code-vb[Main](formatting-the-datalist-and-repeater-based-upon-data-vb/samples/sample4.vb)]

`unitPrice` 입력 매개 변수는 `Object` 형식이 며 `unitPrice` `DBNull` 인지 여부를 확인 하도록 조건문을 수정 합니다. 또한 `unitPrice` 입력 매개 변수는 `Object`으로 전달 되기 때문에 10 진수 값으로 캐스팅 해야 합니다.

## <a name="step-2-calling-the-formatting-function-from-the-datalist-s-itemtemplate"></a>2 단계: DataList s ItemTemplate에서 형식 지정 함수 호출

ASP.NET page s의 코드 숨김이 클래스에 서식 지정 함수를 추가 하면 DataList s `ItemTemplate`에서 이러한 형식 지정 함수를 호출 하는 것만 남았습니다. 템플릿에서 서식 함수를 호출 하려면 데이터 바인딩 구문 내에 함수 호출을 추가 합니다.

[!code-aspx[Main](formatting-the-datalist-and-repeater-based-upon-data-vb/samples/sample5.aspx)]

DataList s `ItemTemplate`에서 `ProductNameLabel` 레이블 웹 컨트롤은 현재 `Text` 속성을 `<%# Eval("ProductName") %>`결과에 할당 하 여 제품 이름을 표시 합니다. 이름에 [단종] 텍스트를 표시 하도록 하려면 필요한 경우 `Text` 속성에 `DisplayProductNameAndDiscontinuedStatus` 메서드의 값을 할당 하도록 선언적 구문을 업데이트 합니다. 이 작업을 수행 하는 경우 `Eval("columnName")` 구문을 사용 하 여 제품 이름과 중단 된 값을 전달 해야 합니다. `Eval`는 `Object`형식의 값을 반환 하지만 `DisplayProductNameAndDiscontinuedStatus` 메서드에서는 `String` 및 `Boolean`형식의 입력 매개 변수가 필요 합니다. 따라서 `Eval` 메서드에서 반환 되는 값을 필요한 입력 매개 변수 형식으로 캐스팅 해야 합니다. 예를 들면 다음과 같습니다.

[!code-aspx[Main](formatting-the-datalist-and-repeater-based-upon-data-vb/samples/sample6.aspx)]

가격을 표시 하려면 제품 이름과 [단종] 텍스트를 표시 하는 것 처럼 `UnitPriceLabel` 레이블 s `Text` 속성을 `DisplayPrice` 메서드에서 반환 된 값으로 설정 하면 됩니다. 그러나 `UnitPrice`를 스칼라 입력 매개 변수로 전달 하는 대신 전체 `ProductsRow` 인스턴스를 전달 합니다.

[!code-aspx[Main](formatting-the-datalist-and-repeater-based-upon-data-vb/samples/sample7.aspx)]

현재 위치의 형식 지정 함수에 대 한 호출을 사용 하 여 브라우저에서 진행 상황을 확인 합니다. 화면은 그림 5와 유사 하 게 표시 됩니다. 즉, [단종] 텍스트와 해당 제품에 대 한 가격 책정을 포함 하 여 더 $20.00 이상 사용 되지 않는 제품의 가격을 텍스트로 바꿀 수 있습니다.

[비용이 많이 드는 제품에 대 한 ![가격은 텍스트로 바뀌고 가격 견적에 대해를 호출 하세요.](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image14.png)](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image13.png)

**그림 5**: 비용이 많이 드는 제품의 경우 가격은 텍스트로 바뀌고 통화에 대해를 호출 하세요 ([전체 크기 이미지를 보려면 클릭](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image15.png)).

## <a name="summary"></a>요약

두 가지 기술을 사용 하 여 데이터에 따라 DataList 또는 Repeater 컨트롤의 내용에 서식을 지정할 수 있습니다. 첫 번째 방법은 `ItemDataBound` 이벤트에 대 한 이벤트 처리기를 만드는 것입니다 .이 이벤트는 데이터 원본의 각 레코드가 새 `DataListItem` 나 `RepeaterItem`에 바인딩되어 있을 때 발생 합니다. `ItemDataBound` 이벤트 처리기에서 현재 항목의 데이터를 검사할 수 있고 서식 지정을 템플릿 내용에 적용 하거나 `DataListItem` 전체 항목 자체에 적용할 수 있습니다.

또는 형식 지정 함수를 통해 사용자 지정 서식 지정을 실현할 수 있습니다. 서식 지정 함수는 해당 위치로 내보낼 HTML을 반환 하는 DataList 또는 Repeater s 템플릿에서 호출할 수 있는 메서드입니다. 서식 함수에서 반환 하는 HTML은 현재 항목에 바인딩되는 값에 의해 결정 되는 경우가 많습니다. 이러한 값은 스칼라 값으로 형식 지정 함수에 전달 하거나 항목에 바인딩되는 전체 개체 (예: `ProductsRow` 인스턴스)에 전달할 수 있습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Yaakov Ellis, Randy Schmidt 및 Liz Shulok 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](displaying-data-with-the-datalist-and-repeater-controls-vb.md)
> [다음](showing-multiple-records-per-row-with-the-datalist-control-vb.md)
