---
uid: web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-vb
title: 데이터를 기반으로 하는 사용자 지정 서식 지정 (VB) | Microsoft Docs
author: rick-anderson
description: 이에 바인딩된 데이터를 기반으로 GridView, DetailsView 또는 FormView의 형식을 조정 하는 것은 여러 가지 방법으로 수행할 수 있습니다. 이 자습서에서는 ...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: df5a1525-386f-4632-972c-57b199870bc3
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 268dc763ef6954903f721a3015daaf10bf9bccb1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78482765"
---
# <a name="custom-formatting-based-upon-data-vb"></a>데이터에 따라 사용자 지정 형식 지정(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_11_VB.exe) 또는 [PDF 다운로드](custom-formatting-based-upon-data-vb/_static/datatutorial11vb1.pdf)

> 이에 바인딩된 데이터를 기반으로 GridView, DetailsView 또는 FormView의 형식을 조정 하는 것은 여러 가지 방법으로 수행할 수 있습니다. 이 자습서에서는 데이터 바인딩된 및 RowDataBound 바인딩 이벤트 처리기를 사용 하 여 데이터 바인딩된 서식 지정을 수행 하는 방법을 살펴보겠습니다.

## <a name="introduction"></a>소개

많은 스타일 관련 속성을 통해 GridView, DetailsView 및 FormView 컨트롤의 모양을 사용자 지정할 수 있습니다. `CssClass`, `Font`, `BorderWidth`, `BorderStyle`, `BorderColor`, `Width`, `Height`등의 속성은 렌더링 된 컨트롤의 일반적인 모양을 지시 합니다. `HeaderStyle`, `RowStyle`, `AlternatingRowStyle`등의 속성을 사용 하 여 이러한 동일한 스타일 설정을 특정 섹션에 적용할 수 있습니다. 마찬가지로 이러한 스타일 설정은 필드 수준에서 적용할 수 있습니다.

그러나 많은 시나리오에서 서식 지정 요구 사항은 표시 된 데이터의 값에 따라 달라 집니다. 예를 들어 품절 제품에 주목 하기 위해 제품 정보를 표시 하는 보고서는 `UnitsInStock` 및 `UnitsOnOrder` 필드가 모두 0 인 제품에 대해 배경색을 노란색으로 설정할 수 있습니다. 비용이 많이 드는 제품을 강조 하기 위해 이러한 제품의 가격을 굵게 표시 하는 글꼴을 $75.00 이상으로 표시 하려고 할 수 있습니다.

이에 바인딩된 데이터를 기반으로 GridView, DetailsView 또는 FormView의 형식을 조정 하는 것은 여러 가지 방법으로 수행할 수 있습니다. 이 자습서에서는 `DataBound` 및 `RowDataBound` 이벤트 처리기를 사용 하 여 데이터 바인딩된 서식 지정을 수행 하는 방법을 살펴보겠습니다. 다음 자습서에서는 다른 방법을 살펴보겠습니다.

## <a name="using-the-detailsview-controlsdataboundevent-handler"></a>DetailsView 컨트롤의`DataBound`이벤트 처리기 사용

데이터 소스 컨트롤이 나 컨트롤의 `DataSource` 속성에 데이터를 프로그래밍 방식으로 할당 하 고 해당 `DataBind()` 메서드를 호출 하 여 데이터를 DetailsView에 바인딩하면 다음과 같은 일련의 단계가 수행 됩니다.

1. 데이터 웹 컨트롤의 `DataBinding` 이벤트가 발생 합니다.
2. 데이터는 데이터 웹 컨트롤에 바인딩됩니다.
3. 데이터 웹 컨트롤의 `DataBound` 이벤트가 발생 합니다.

사용자 지정 논리는 이벤트 처리기를 통해 1 단계 및 3 단계 바로 뒤에 삽입 될 수 있습니다. `DataBound` 이벤트에 대 한 이벤트 처리기를 만들어 데이터 웹 컨트롤에 바인딩된 데이터를 프로그래밍 방식으로 확인 하 고 필요에 따라 형식을 조정할 수 있습니다. 이를 설명 하기 위해 제품에 대 한 일반 정보를 나열 하는 DetailsView을 만들어 $75.00를 초과 하는 경우 ***굵은 기울임꼴 글꼴로*** `UnitPrice` 값을 표시 합니다.

## <a name="step-1-displaying-the-product-information-in-a-detailsview"></a>1 단계: DetailsView에서 제품 정보 표시

`CustomFormatting` 폴더에서 `CustomColors.aspx` 페이지를 열고, 도구 상자에서 DetailsView 컨트롤을 디자이너로 끌고, `ID` 속성 값을 `ExpensiveProductsPriceInBoldItalic`로 설정 하 고, `ProductsBLL` 클래스의 `GetProducts()` 메서드를 호출 하는 새 ObjectDataSource 컨트롤에 바인딩합니다. 이 작업을 수행 하는 자세한 단계는 앞의 자습서에서 자세히 검토 했으므로 간략하게 설명 합니다.

ObjectDataSource를 DetailsView에 바인딩한 후에는 잠시 시간을 사용 하 여 필드 목록을 수정 합니다. `ProductID`, `SupplierID`, `CategoryID`, `UnitsInStock`, `UnitsOnOrder`, `ReorderLevel`및 `Discontinued` BoundFields를 제거 하 고 나머지 BoundFields의 이름을 바꾸고 다시 포맷 했습니다. 또한 `Width` 및 `Height` 설정을 해제 했습니다. DetailsView에는 단일 레코드만 표시 되므로 최종 사용자가 모든 제품을 볼 수 있도록 하려면 페이징을 사용 하도록 설정 해야 합니다. 이렇게 하려면 DetailsView의 스마트 태그에서 페이징 사용 확인란을 선택 합니다.

[![그림 1: DetailsView의 스마트 태그에서 페이징 사용 확인란을 선택 합니다.](custom-formatting-based-upon-data-vb/_static/image2.png)](custom-formatting-based-upon-data-vb/_static/image1.png)

**그림 1**: 그림 1: DetailsView의 스마트 태그에서 페이징 사용 확인란을 선택 합니다 ([전체 크기 이미지를 보려면 클릭](custom-formatting-based-upon-data-vb/_static/image3.png)).

이러한 변경 후에는 DetailsView 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](custom-formatting-based-upon-data-vb/samples/sample1.aspx)]

잠시 시간을 들 여 브라우저에서이 페이지를 테스트해 보세요.

[DetailsView 컨트롤 ![한 번에 하나의 제품을 표시 합니다.](custom-formatting-based-upon-data-vb/_static/image5.png)](custom-formatting-based-upon-data-vb/_static/image4.png)

**그림 2**: DetailsView 컨트롤은 한 번에 하나의 제품을 표시 합니다 ([전체 크기 이미지를 보려면 클릭](custom-formatting-based-upon-data-vb/_static/image6.png)).

## <a name="step-2-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a>2 단계: 데이터 바인딩된 이벤트 처리기에서 프로그래밍 방식으로 데이터 값 확인

`UnitPrice` 값이 $75.00를 초과 하는 제품에 대 한 굵게 기울임꼴 글꼴로 가격을 표시 하기 위해 먼저 `UnitPrice` 값을 프로그래밍 방식으로 확인할 수 있어야 합니다. DetailsView의 경우 `DataBound` 이벤트 처리기에서이를 수행할 수 있습니다. 이벤트 처리기를 만들려면 디자이너에서 DetailsView를 클릭 한 다음 속성 창로 이동 합니다. 표시 되지 않으면 F4 키를 누르거나 보기 메뉴로 이동 하 여 속성 창 메뉴 옵션을 선택 합니다. 속성 창에서 번개 볼트 아이콘을 클릭 하 여 DetailsView의 이벤트를 나열 합니다. 그런 다음 `DataBound` 이벤트를 두 번 클릭 하거나 만들려는 이벤트 처리기의 이름을 입력 합니다.

![데이터 바인딩된 이벤트에 대 한 이벤트 처리기 만들기](custom-formatting-based-upon-data-vb/_static/image7.png)

**그림 3**: `DataBound` 이벤트에 대 한 이벤트 처리기 만들기

> [!NOTE]
> ASP.NET 페이지의 코드 부분에서 이벤트 처리기를 만들 수도 있습니다. 페이지 맨 위에 두 개의 드롭다운 목록이 있습니다. 왼쪽 드롭다운 목록에서 개체를 선택 하 고 오른쪽 드롭다운 목록에서 처리기를 만들려는 이벤트를 선택 하면 Visual Studio에서 적절 한 이벤트 처리기를 자동으로 만듭니다.

이렇게 하면 이벤트 처리기가 자동으로 생성 되 고 추가 된 코드 부분으로 이동 합니다. 이 시점에서 다음을 확인할 수 있습니다.

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample2.vb)]

DetailsView에 바인딩된 데이터는 `DataItem` 속성을 통해 액세스할 수 있습니다. 강력한 형식의 DataRow 인스턴스 컬렉션으로 구성 된 강력한 형식의 DataTable에 컨트롤을 바인딩하는 것을 기억 하세요. DataTable이 DetailsView에 바인딩되면 DataTable의 첫 번째 DataRow가 DetailsView의 `DataItem` 속성에 할당 됩니다. 특히 `DataItem` 속성에 `DataRowView` 개체가 할당 됩니다. `DataRowView`의 `Row` 속성을 사용 하 여 실제로 `ProductsRow` 인스턴스인 기본 DataRow 개체에 액세스할 수 있습니다. 이 `ProductsRow` 인스턴스가 있으면 단순히 개체의 속성 값을 검사 하 여 결정을 내릴 수 있습니다.

다음 코드에서는 DetailsView 컨트롤에 바인딩되는 `UnitPrice` 값이 $75.00 보다 큰지 여부를 확인 하는 방법을 보여 줍니다.

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample3.vb)]

> [!NOTE]
> `UnitPrice`는 데이터베이스에 `NULL` 값이 있을 수 있으므로 먼저 `ProductsRow`의 `UnitPrice` 속성에 액세스 하기 전에 `NULL` 값을 처리 하 고 있지 않은지 확인 합니다. 이 검사는 `NULL` 값이 있을 때 `UnitPrice` 속성에 액세스 하려고 하면 `ProductsRow` 개체가 [StrongTypingException 예외](https://msdn.microsoft.com/library/system.data.strongtypingexception.aspx)를 throw 하기 때문에 중요 합니다.

## <a name="step-3-formatting-the-unitprice-value-in-the-detailsview"></a>3 단계: DetailsView에서 UnitPrice 값 서식 지정

이 시점에서 DetailsView에 바인딩된 `UnitPrice` 값에 $75.00을 초과 하는 값이 있는지 여부를 확인할 수 있지만이에 따라 DetailsView의 형식을 프로그래밍 방식으로 조정 하는 방법을 확인 해야 합니다. DetailsView에서 전체 행의 서식을 수정 하려면 `DetailsViewID.Rows(index)`을 사용 하 여 프로그래밍 방식으로 행에 액세스 합니다. 특정 셀을 수정 하려면 access `DetailsViewID.Rows(index).Cells(index)`를 사용 합니다. 행 또는 셀에 대 한 참조가 있으면 스타일 관련 속성을 설정 하 여 모양을 조정할 수 있습니다.

행에 프로그래밍 방식으로 액세스 하려면 행의 인덱스 (0부터 시작)를 알아야 합니다. `UnitPrice` 행은 DetailsView에서 5 번째 행 이며 인덱스 4를 제공 하 고 `ExpensiveProductsPriceInBoldItalic.Rows(4)`를 사용 하 여 프로그래밍 방식으로 액세스할 수 있게 합니다. 이 시점에서 다음 코드를 사용 하 여 전체 행의 내용이 굵은 기울임꼴 글꼴로 표시 될 수 있습니다.

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample4.vb)]

그러나 *이렇게 하면 레이블* (Price) 및 값이 굵게 표시 되 고 기울임꼴로 표시 됩니다. 값을 굵게 표시 하 고 기울임꼴로 표시 하려는 경우 다음을 사용 하 여이 서식을 행의 두 번째 셀에 적용 해야 합니다.

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample5.vb)]

이 자습서에서는 앞에서 설명한 대로 특정 스타일 속성을 설정 하는 대신 스타일 시트를 사용 하 여 렌더링 된 태그와 스타일 관련 정보를 명확 하 게 분리 하므로 스타일 시트 클래스를 대신 사용할 수 있습니다. `Styles.css` 스타일 시트를 열고 다음 정의를 사용 하 여 `ExpensivePriceEmphasis` 라는 새 CSS 클래스를 추가 합니다.

[!code-css[Main](custom-formatting-based-upon-data-vb/samples/sample6.css)]

그런 다음 `DataBound` 이벤트 처리기에서 셀의 `CssClass` 속성을 `ExpensivePriceEmphasis`로 설정 합니다. 다음 코드에서는 `DataBound` 이벤트 처리기를 전체적으로 보여 줍니다.

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample7.vb)]

$75.00 보다 저렴 한 Chai 볼 때 가격은 일반 글꼴로 표시 됩니다 (그림 4 참조). 그러나 가격이 $97.00 인 Mishi Kobe Niku를 볼 때 가격은 굵은 기울임꼴 글꼴로 표시 됩니다 (그림 5 참조).

[$75.00 보다 작은 ![가격은 일반 글꼴로 표시 됩니다.](custom-formatting-based-upon-data-vb/_static/image9.png)](custom-formatting-based-upon-data-vb/_static/image8.png)

**그림 4**: $75.00 보다 작은 가격은 일반 글꼴로 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](custom-formatting-based-upon-data-vb/_static/image10.png)).

[![고가의 제품 가격은 굵은 기울임꼴 글꼴로 표시 됩니다.](custom-formatting-based-upon-data-vb/_static/image12.png)](custom-formatting-based-upon-data-vb/_static/image11.png)

**그림 5**: 고가의 제품 가격은 굵은 기울임꼴 글꼴로 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](custom-formatting-based-upon-data-vb/_static/image13.png)).

## <a name="using-the-formview-controlsdataboundevent-handler"></a>FormView 컨트롤의`DataBound`이벤트 처리기 사용

FormView에 바인딩된 내부 데이터를 확인 하는 단계는 DetailsView의 `DataBound` 이벤트 처리기를 만드는 단계와 동일 하며 `DataItem` 속성을 컨트롤에 바인딩된 적절 한 개체 형식으로 캐스팅 하 고 진행 방법을 결정 합니다. 그러나 FormView와 DetailsView은 사용자 인터페이스 모양이 업데이트 되는 방식에 따라 다릅니다.

FormView에 BoundFields가 포함 되어 있지 않으므로 `Rows` 컬렉션이 없습니다. 대신 FormView는 정적 HTML, 웹 컨트롤 및 데이터 바인딩 구문이 혼합 되어 있을 수 있는 템플릿으로 구성 됩니다. FormView의 스타일을 조정 하려면 일반적으로 FormView의 템플릿 내에서 하나 이상의 웹 컨트롤 스타일을 조정 해야 합니다.

이를 설명 하기 위해 FormView를 사용 하 여 이전 예제와 같은 제품을 나열 해 보겠습니다. 하지만 이번에는 재고 단위가 10 보다 작거나 같은 경우 빨간색 글꼴로 표시 되는 재고의 제품 이름과 단위도 표시 해 보겠습니다.

## <a name="step-4-displaying-the-product-information-in-a-formview"></a>4 단계: FormView에서 제품 정보 표시

DetailsView 아래 `CustomColors.aspx` 페이지에 FormView를 추가 하 고 `ID` 속성을 `LowStockedProductsInRed`로 설정 합니다. FormView를 이전 단계에서 만든 ObjectDataSource 컨트롤에 바인딩합니다. 이렇게 하면 FormView에 대 한 `ItemTemplate`, `EditItemTemplate`및 `InsertItemTemplate` 만들어집니다. `EditItemTemplate`를 제거 하 고 `InsertItemTemplate` `ItemTemplate`를 간소화 하 여 각각의 적절 하 게 명명 된 레이블 컨트롤에 `ProductName` 및 `UnitsInStock` 값만 포함 합니다. 이전 예제에서 DetailsView와 마찬가지로 FormView의 스마트 태그에서 페이징 사용 확인란을 선택 합니다.

이러한 편집 후에는 FormView의 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](custom-formatting-based-upon-data-vb/samples/sample8.aspx)]

`ItemTemplate`에는 다음이 포함 됩니다.

- **정적 HTML** 텍스트 "Product:" 및 "Unit In Stock:"은 `<br />` 및 `<b>` 요소와 함께 사용 됩니다.
- **웹** 에서는 두 개의 레이블 컨트롤 `ProductNameLabel` 및 `UnitsInStockLabel`를 제어 합니다.
- **데이터 바인딩 구문** 이러한 필드의 값을 레이블 컨트롤의 `Text` 속성에 할당 하는 `<%# Bind("ProductName") %>` 및 `<%# Bind("UnitsInStock") %>` 구문입니다.

## <a name="step-5-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a>5 단계: 데이터 바인딩된 이벤트 처리기에서 프로그래밍 방식으로 데이터 값 확인

FormView의 태그가 완료 되 면 다음 단계는 `UnitsInStock` 값이 10 보다 작거나 같은지를 프로그래밍 방식으로 확인 하는 것입니다. 이는 DetailsView과 동일한 방식으로 FormView와 정확히 동일한 방법으로 수행 됩니다. 먼저 FormView의 `DataBound` 이벤트에 대 한 이벤트 처리기를 만듭니다.

![데이터 바인딩된 이벤트 처리기 만들기](custom-formatting-based-upon-data-vb/_static/image14.png)

**그림 6**: `DataBound` 이벤트 처리기 만들기

이벤트 처리기에서 FormView의 `DataItem` 속성을 `ProductsRow` 인스턴스로 캐스팅 하 고 `UnitsInPrice` 값이 빨간색 글꼴로 표시 되어야 하는지 여부를 확인 합니다.

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample9.vb)]

## <a name="step-6-formatting-the-unitsinstocklabel-label-control-in-the-formviews-itemtemplate"></a>6 단계: FormView의 ItemTemplate에서 UnitsInStockLabel Label 컨트롤 서식 지정

마지막 단계는 값이 10 이하인 경우 표시 되는 `UnitsInStock` 값을 빨간색 글꼴로 서식 지정 하는 것입니다. 이를 수행 하려면 `ItemTemplate`에서 `UnitsInStockLabel` 컨트롤에 프로그래밍 방식으로 액세스 하 고 해당 텍스트가 빨간색으로 표시 되도록 스타일 속성을 설정 해야 합니다. 템플릿에서 웹 컨트롤에 액세스 하려면 다음과 같이 `FindControl("controlID")` 메서드를 사용 합니다.

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample10.vb)]

이 예제에서는 `ID` 값이 `UnitsInStockLabel`레이블 컨트롤에 액세스 하려고 하므로 다음을 사용 합니다.

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample11.vb)]

웹 컨트롤에 대 한 프로그래밍 참조가 있으면 필요에 따라 스타일 관련 속성을 수정할 수 있습니다. 이전 예제와 마찬가지로 `LowUnitsInStockEmphasis`라는 `Styles.css`에서 CSS 클래스를 만들었습니다. Label 웹 컨트롤에이 스타일을 적용 하려면 해당 `CssClass` 속성을 적절 하 게 설정 합니다.

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample12.vb)]

> [!NOTE]
> 템플릿 서식을 지정 하는 구문은 `FindControl("controlID")`를 사용 하 여 웹 컨트롤에 프로그래밍 방식으로 액세스 한 다음, DetailsView 또는 GridView 컨트롤에서 템플릿 [필드](https://msdn.microsoft.com/library/system.web.ui.webcontrols.templatefield(VS.80).aspx) 를 사용 하는 경우에도 사용할 수 있습니다. 다음 자습서에서 템플릿 필드를 살펴보겠습니다.

그림 7에는 `UnitsInStock` 값이 10 보다 큰 제품을 볼 때 FormView가 표시 되 고, 그림 8의 제품에는 10 보다 작은 값이 있습니다.

[재고가 충분히 많은 제품 ![사용자 지정 서식 지정이 적용 되지 않습니다.](custom-formatting-based-upon-data-vb/_static/image16.png)](custom-formatting-based-upon-data-vb/_static/image15.png)

**그림 7**: 재고에 충분히 큰 단위가 포함 된 제품의 경우 사용자 지정 서식 지정이 적용 되지 않음 ([전체 크기 이미지를 보려면 클릭](custom-formatting-based-upon-data-vb/_static/image17.png))

[값이 10 이하인 제품에 대해 재고 번호 단위를 빨간색으로 표시 ![](custom-formatting-based-upon-data-vb/_static/image19.png)](custom-formatting-based-upon-data-vb/_static/image18.png)

**그림 8**: 10 이하의 값을 포함 하는 제품에 대해 재고 번호 단위는 빨간색으로 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](custom-formatting-based-upon-data-vb/_static/image20.png)).

## <a name="formatting-with-the-gridviewsrowdataboundevent"></a>GridView의`RowDataBound`이벤트로 서식 지정

이전에는 DetailsView 및 FormView가 데이터 바인딩 중에 진행률을 제어 하는 단계의 순서를 살펴보았습니다. 이러한 단계를 다시 리프레셔로 살펴보겠습니다.

1. 데이터 웹 컨트롤의 `DataBinding` 이벤트가 발생 합니다.
2. 데이터는 데이터 웹 컨트롤에 바인딩됩니다.
3. 데이터 웹 컨트롤의 `DataBound` 이벤트가 발생 합니다.

이 세 가지 간단한 단계는 단일 레코드만 표시 하므로 DetailsView 및 FormView에 충분 합니다. GridView에 바인딩된 *모든* 레코드를 표시 하는 경우 (첫 번째만이 아니라) 2 단계는 약간 더 복잡 합니다.

2 단계에서 GridView는 데이터 소스를 열거 하 고 각 레코드에 대해 `GridViewRow` 인스턴스를 만들고 현재 레코드를 여기에 바인딩합니다. GridView에 추가 된 각 `GridViewRow`에 대해 두 개의 이벤트가 발생 합니다.

- `GridViewRow`를 만든 후에 **`RowCreated`** 발생 합니다.
- **`RowDataBound`** 현재 레코드가 `GridViewRow`바인딩된 후에 발생 합니다.

GridView의 경우 다음과 같은 일련의 단계를 통해 데이터 바인딩을 보다 정확 하 게 설명할 수 있습니다.

1. GridView의 `DataBinding` 이벤트가 발생 합니다.
2. 데이터가 GridView에 바인딩됩니다.   
  
   데이터 원본의 각 레코드에 대해 

    1. `GridViewRow` 개체 만들기
    2. `RowCreated` 이벤트를 발생 시킵니다.
    3. 레코드를 `GridViewRow`에 바인딩
    4. `RowDataBound` 이벤트를 발생 시킵니다.
    5. `Rows` 컬렉션에 `GridViewRow` 추가
3. GridView의 `DataBound` 이벤트가 발생 합니다.

GridView의 개별 레코드 형식을 사용자 지정 하려면 `RowDataBound` 이벤트에 대 한 이벤트 처리기를 만들어야 합니다. 이를 설명 하기 위해 `CustomColors.aspx` 페이지에 GridView를 추가 해 보겠습니다. 여기에는 각 제품에 대 한 이름, 범주 및 가격이 표시 되 고 가격이 노랑 배경색으로 $10.00 미만인 제품이 강조 표시 됩니다.

## <a name="step-7-displaying-product-information-in-a-gridview"></a>7 단계: GridView에 제품 정보 표시

이전 예제에서 FormView 아래의 GridView를 추가 하 고 해당 `ID` 속성을 `HighlightCheapProducts`로 설정 합니다. 페이지의 모든 제품을 반환 하는 ObjectDataSource가 이미 있으므로 GridView를 해당에 바인딩합니다. 마지막으로, 제품의 이름, 범주 및 가격만 포함 하도록 GridView의 BoundFields를 편집 합니다. 이러한 편집 후 GridView의 태그는 다음과 같습니다.

[!code-aspx[Main](custom-formatting-based-upon-data-vb/samples/sample13.aspx)]

그림 9에서는 브라우저를 통해 볼 때이 시점에 대 한 진행률을 보여 줍니다.

[GridView ![각 제품의 이름, 범주 및 가격이 나열 됩니다.](custom-formatting-based-upon-data-vb/_static/image22.png)](custom-formatting-based-upon-data-vb/_static/image21.png)

**그림 9**: GridView에 각 제품의 이름, 범주 및 가격이 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](custom-formatting-based-upon-data-vb/_static/image23.png)).

## <a name="step-8-programmatically-determining-the-value-of-the-data-in-the-rowdatabound-event-handler"></a>8 단계: RowDataBound 바인딩 이벤트 처리기에서 프로그래밍 방식으로 데이터 값 결정

`ProductsDataTable` GridView에 바인딩되면 `ProductsRow` 인스턴스가 열거 되 고 각 `ProductsRow`에 대해 `GridViewRow` 만들어집니다. `GridViewRow`의 `DataItem` 속성은 특정 `ProductRow`에 할당 된 후 GridView의 `RowDataBound` 이벤트 처리기가 발생 합니다. GridView에 바인딩된 각 제품의 `UnitPrice` 값을 확인 하려면 GridView의 `RowDataBound` 이벤트에 대 한 이벤트 처리기를 만들어야 합니다. 이 이벤트 처리기에서는 현재 `GridViewRow`에 대 한 `UnitPrice` 값을 검사 하 고 해당 행에 대 한 서식 지정을 결정할 수 있습니다.

이 이벤트 처리기는 FormView 및 DetailsView와 동일한 일련의 단계를 사용 하 여 만들 수 있습니다.

![GridView의 RowDataBound 바인딩된 이벤트에 대 한 이벤트 처리기 만들기](custom-formatting-based-upon-data-vb/_static/image24.png)

**그림 10**: GridView의 `RowDataBound` 이벤트에 대 한 이벤트 처리기 만들기

이러한 방식으로 이벤트 처리기를 만들면 다음 코드가 ASP.NET 페이지의 코드 부분에 자동으로 추가 됩니다.

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample14.vb)]

`RowDataBound` 이벤트가 발생 하는 경우 이벤트 처리기는 이름이 `Row`인 속성이 있는 `GridViewRowEventArgs`형식의 개체를 두 번째 매개 변수로 전달 합니다. 이 속성은 단순히 데이터 바인딩된 `GridViewRow`에 대 한 참조를 반환 합니다. `GridViewRow`에 바인딩된 `ProductsRow` 인스턴스에 액세스 하려면 다음과 같이 `DataItem` 속성을 사용 합니다.

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample15.vb)]

`RowDataBound` 이벤트 처리기를 사용 하는 경우 GridView는 여러 행 형식으로 구성 되 고 *모든* 행 형식에 대해이 이벤트가 발생 한다는 점에 유의 해야 합니다. `GridViewRow`형식은 `RowType` 속성에 의해 결정 될 수 있으며 가능한 값 중 하나를 가질 수 있습니다.

- GridView의 `DataSource` 레코드에 바인딩된 행을 `DataRow`
- GridView의 `DataSource` 비어 있는 경우 표시 되는 행 `EmptyDataRow`
- 바닥글 행을 `Footer` 합니다. GridView의 `ShowFooter` 속성이로 설정 된 경우 표시 됩니다 `True`
- 머리글 행을 `Header` 합니다. GridView의 ShowHeader 속성이 `True` (기본값)로 설정 된 경우 표시 됩니다.
- 페이징을 구현 하는 GridView의 `Pager` 페이징 인터페이스를 표시 하는 행입니다.
- GridView에는 사용 되지 않지만 DataList 및 Repeater 컨트롤의 `RowType` 속성에서 사용 되는 `Separator` 다음 자습서에서 설명 하는 두 가지 데이터 웹 컨트롤

`EmptyDataRow`, `Header`, `Footer`및 `Pager` 행은 `DataSource` 레코드와 연결 되지 않으므로 해당 `Nothing` 속성의 값은 항상 `DataItem`입니다. 이러한 이유로 현재 `GridViewRow`의 `DataItem` 속성을 사용 하기 전에 먼저 `DataRow`를 처리 하 고 있는지 확인 해야 합니다. 다음과 같이 `GridViewRow`의 `RowType` 속성을 확인 하 여이 작업을 수행할 수 있습니다.

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample16.vb)]

## <a name="step-9-highlighting-the-row-yellow-when-the-unitprice-value-is-less-than-1000"></a>9 단계: UnitPrice 값이 $10.00 보다 작은 경우 노란색 행 강조 표시

마지막 단계는 해당 행의 `UnitPrice` 값이 $10.00 보다 작은 경우 전체 `GridViewRow`를 프로그래밍 방식으로 강조 표시 하는 것입니다. GridView의 행 이나 셀에 액세스 하기 위한 구문은 전체 행에 액세스 하기 위해 DetailsView `GridViewID.Rows(index)`와 동일 하며, `GridViewID.Rows(index).Cells(index)` 특정 셀에 액세스 하는 데 사용 됩니다. 그러나 `RowDataBound` 이벤트 처리기가 데이터 바인딩된 `GridViewRow`를 발생 시키면 GridView의 `Rows` 컬렉션에 추가 됩니다. 따라서 Rows 컬렉션을 사용 하 여 `RowDataBound` 이벤트 처리기에서 현재 `GridViewRow` 인스턴스에 액세스할 수 없습니다.

`GridViewID.Rows(index)`대신 `e.Row`를 사용 하 여 `RowDataBound` 이벤트 처리기에서 현재 `GridViewRow` 인스턴스를 참조할 수 있습니다. 즉, 사용 하는 `RowDataBound` 이벤트 처리기에서 현재 `GridViewRow` 인스턴스를 강조 표시 하기 위해 다음을 수행 합니다.

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample17.vb)]

`GridViewRow`의 `BackColor` 속성을 직접 설정 하는 대신 CSS 클래스를 사용 하는 것이 좋습니다. 배경색을 노란색으로 설정 하는 `AffordablePriceEmphasis` 라는 CSS 클래스를 만들었습니다. 완료 된 `RowDataBound` 이벤트 처리기는 다음과 같습니다.

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample18.vb)]

[![가장 저렴 한 제품을 노란색으로 강조 표시 합니다.](custom-formatting-based-upon-data-vb/_static/image26.png)](custom-formatting-based-upon-data-vb/_static/image25.png)

**그림 11**: 가장 저렴 한 제품을 노란색으로 강조 표시 ([전체 크기 이미지를 보려면 클릭](custom-formatting-based-upon-data-vb/_static/image27.png))

## <a name="summary"></a>요약

이 자습서에서는 컨트롤에 바인딩된 데이터를 기반으로 GridView, DetailsView 및 FormView의 형식을 지정 하는 방법을 살펴보았습니다. 이를 위해 필요에 따라 기본 데이터가 형식 변경과 함께 검사 된 `DataBound` 또는 `RowDataBound` 이벤트에 대 한 이벤트 처리기를 만들었습니다. DetailsView 또는 FormView에 바인딩된 데이터에 액세스 하려면 `DataBound` 이벤트 처리기에서 `DataItem` 속성을 사용 합니다. GridView의 경우 각 `GridViewRow` 인스턴스의 `DataItem` 속성은 `RowDataBound` 이벤트 처리기에서 사용할 수 있는 해당 행에 바인딩된 데이터를 포함 합니다.

데이터 웹 컨트롤의 서식 지정을 프로그래밍 방식으로 조정 하는 구문은 웹 컨트롤과 서식 지정 되는 데이터의 표시 방법에 따라 달라 집니다. DetailsView 및 GridView 컨트롤의 경우 행과 셀은 서 수 인덱스로 액세스할 수 있습니다. 템플릿을 사용 하는 FormView의 경우 `FindControl("controlID")` 메서드는 일반적으로 템플릿 내에서 웹 컨트롤을 찾는 데 사용 됩니다.

다음 자습서에서는 GridView 및 DetailsView에서 템플릿을 사용 하는 방법을 살펴보겠습니다. 또한 기본 데이터를 기반으로 서식을 지정 하는 다른 기술을 살펴보겠습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서에 대 한 잠재 고객 검토자가 E.R. Gilmore, Dennis Patterson이 및 Dan Jagers. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](displaying-summary-information-in-the-gridview-s-footer-cs.md)
> [다음](using-templatefields-in-the-gridview-control-vb.md)
