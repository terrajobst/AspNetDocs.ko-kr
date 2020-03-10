---
uid: web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-detailsview-control-cs
title: DetailsView 컨트롤에서 서식 필드 사용 (C#) | Microsoft Docs
author: rick-anderson
description: GridView에서 사용할 수 있는 것과 동일한 템플릿 필드 기능을 DetailsView 컨트롤과 함께 사용할 수도 있습니다. 이 자습서에서는 제품 하나를 표시 합니다.
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 83efb21f-b231-446e-9356-f4c6cbcc6713
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-detailsview-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 55c667800a9fb19d200bcf4b68e2c59ca4ef5d0e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78481865"
---
# <a name="using-templatefields-in-the-detailsview-control-c"></a>DetailsView 컨트롤에서 TemplateFields 사용(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_13_CS.exe) 또는 [PDF 다운로드](using-templatefields-in-the-detailsview-control-cs/_static/datatutorial13cs1.pdf)

> GridView에서 사용할 수 있는 것과 동일한 템플릿 필드 기능을 DetailsView 컨트롤과 함께 사용할 수도 있습니다. 이 자습서에서는 서식 필드를 포함 하는 DetailsView을 사용 하 여 한 번에 하나의 제품을 표시 합니다.

## <a name="introduction"></a>소개

Templatefield로 변환는 BoundField, CheckBoxField, hyperlink 필드 및 기타 데이터 필드 컨트롤 보다 데이터를 렌더링할 때 더 높은 수준의 유연성을 제공 합니다. [이전 자습서](using-templatefields-in-the-gridview-control-cs.md) 에서는 GridView에서 templatefield로 변환를 사용 하 여 다음을 수행 하는 방법을 살펴보았습니다.

- 한 열에 여러 데이터 필드 값을 표시 합니다. 특히 `FirstName` 및 `LastName` 필드가 하나의 GridView 열로 결합 되었습니다.
- 대체 웹 컨트롤을 사용 하 여 데이터 필드 값을 표현 합니다. 달력 컨트롤을 사용 하 여 `HiredDate` 값을 표시 하는 방법을 살펴보았습니다.
- 기본 데이터를 기반으로 상태 정보를 표시 합니다. `Employees` 테이블에는 직원이 작업에서 있었던 일 수를 반환 하는 열이 포함 되어 있지 않지만 Templatefield로 변환 및 형식 지정 방법을 사용 하 여 이전 자습서의 GridView 예제에서 이러한 정보를 표시할 수 있습니다.

GridView에서 사용할 수 있는 것과 동일한 템플릿 필드 기능을 DetailsView 컨트롤과 함께 사용할 수도 있습니다. 이 자습서에서는 두 개의 템플릿 필드가 포함 된 DetailsView을 사용 하 여 한 번에 하나의 제품을 표시 합니다. 첫 번째 Templatefield로 변환는 `UnitPrice`, `UnitsInStock`및 `UnitsOnOrder` 데이터 필드를 하나의 DetailsView 행으로 결합 합니다. 두 번째 Templatefield로 변환는 `Discontinued` 필드의 값을 표시 하지만 `Discontinued` `true`경우 "YES"를 표시 하는 형식 지정 메서드를 사용 하 고 그렇지 않으면 "아니요"를 표시 합니다.

[![두 개의 템플릿 필드를 사용 하 여 표시를 사용자 지정 합니다.](using-templatefields-in-the-detailsview-control-cs/_static/image2.png)](using-templatefields-in-the-detailsview-control-cs/_static/image1.png)

**그림 1**: 표시를 사용자 지정 하는 데 사용 되는 두 개의 템플릿 필드 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-detailsview-control-cs/_static/image3.png))

이제 시작하겠습니다.

## <a name="step-1-binding-the-data-to-the-detailsview"></a>1 단계: DetailsView에 데이터 바인딩

이전 자습서에 설명 된 것 처럼 템플릿 필드를 사용 하 여 작업 하는 경우에는 단순히 BoundFields를 포함 하는 DetailsView 컨트롤을 만든 다음 새 템플릿 필드를 추가 하거나 필요에 따라 기존 BoundFields를 템플릿 필드로 변환 하 여 시작 하는 것이 가장 쉬운 경우가 많습니다. . 따라서 디자이너를 통해 페이지에 DetailsView을 추가 하 고 제품 목록을 반환 하는 ObjectDataSource에 바인딩하여이 자습서를 시작 합니다. 이러한 단계에서는 각 제품의 부울이 아닌 값 필드와 하나의 부울 값 필드 (단종 되지 않음)에 대해 BoundFields를 사용 하 여 DetailsView을 만듭니다.

`DetailsViewTemplateField.aspx` 페이지를 열고 DetailsView를 도구 상자에서 디자이너로 끌어 옵니다. DetailsView의 스마트 태그에서 `ProductsBLL` 클래스의 `GetProducts()` 메서드를 호출 하는 새 ObjectDataSource 컨트롤을 추가 하도록 선택 합니다.

[GetProducts () 메서드를 호출 하는 새 ObjectDataSource 컨트롤을 추가 ![](using-templatefields-in-the-detailsview-control-cs/_static/image5.png)](using-templatefields-in-the-detailsview-control-cs/_static/image4.png)

**그림 2**: `GetProducts()` 메서드를 호출 하는 새 ObjectDataSource 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-detailsview-control-cs/_static/image6.png))

이 보고서의 경우 `ProductID`, `SupplierID`, `CategoryID`및 `ReorderLevel` BoundFields를 제거 합니다. 그런 다음 `CategoryName` 및 `SupplierName` BoundFields이 `ProductName` BoundField 바로 뒤에 나타나도록 BoundFields을 다시 정렬 합니다. BoundFields에 대 한 속성 및 서식 속성을 적절 하 게 조정 하 `HeaderText`는 것은 마음에. GridView와 마찬가지로 이러한 BoundField 편집은 필드 대화 상자 (DetailsView의 스마트 태그에서 필드 편집 링크를 클릭 하 여 액세스 가능) 또는 선언적 구문을 통해 수행할 수 있습니다. 마지막으로 DetailsView 컨트롤이 표시 된 데이터에 따라 확장 될 수 있도록 하 고, 스마트 태그에서 페이징 사용 확인란을 선택 하 여 detailsview의 `Height`을 지우고 속성 값을 `Width` 합니다.

이러한 변경을 수행한 후에는 DetailsView 컨트롤의 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](using-templatefields-in-the-detailsview-control-cs/samples/sample1.aspx)]

잠시 시간을 사용 하 여 브라우저를 통해 페이지를 봅니다. 이 시점에서 제품의 이름, 범주, 공급자, 가격, 재고 단위, 주문 단위 및 단종 됨 상태를 표시 하는 행이 나열 된 단일 제품 (Chai)이 표시 됩니다.

[![일련의 BoundFields을 사용 하 여 제품의 세부 정보를 표시 합니다.](using-templatefields-in-the-detailsview-control-cs/_static/image8.png)](using-templatefields-in-the-detailsview-control-cs/_static/image7.png)

**그림 3**: 제품의 세부 정보는 일련의 BoundFields를 사용 하 여 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-detailsview-control-cs/_static/image9.png)).

## <a name="step-2-combining-the-price-units-in-stock-and-units-on-order-into-one-row"></a>2 단계: 가격, 재고 단위 및 주문에 대 한 단위를 한 행으로 결합

DetailsView에는 `UnitPrice`, `UnitsInStock`및 `UnitsOnOrder` 필드에 대 한 행이 있습니다. 새 Templatefield로 변환를 추가 하거나 기존 `UnitPrice`, `UnitsInStock`및 `UnitsOnOrder` BoundFields 중 하나를 Templatefield로 변환로 변환 하 여 이러한 데이터 필드를 단일 행으로 결합할 수 있습니다. 기존 BoundFields 변환을 개인적으로 선호 하는 반면 새 Templatefield로 변환를 추가 하 여 연습 하겠습니다.

DetailsView의 스마트 태그에서 필드 편집 링크를 클릭 하 여 필드 대화 상자를 표시 하는 것부터 시작 합니다. 그런 다음 새 Templatefield로 변환를 추가 하 고 해당 `HeaderText` 속성을 "Price and Inventory"로 설정 하 고 `UnitPrice` BoundField 위에 배치 되도록 새 Templatefield로 변환를 이동 합니다.

[![새 Templatefield로 변환를 DetailsView 컨트롤에 추가 합니다.](using-templatefields-in-the-detailsview-control-cs/_static/image11.png)](using-templatefields-in-the-detailsview-control-cs/_static/image10.png)

**그림 4**: DetailsView 컨트롤에 새 templatefield로 변환 추가 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-detailsview-control-cs/_static/image12.png))

이 새 Templatefield로 변환에는 `UnitPrice`, `UnitsInStock`및 `UnitsOnOrder`에 현재 표시 된 값이 포함 되므로 제거 하겠습니다.

이 단계의 마지막 작업은 Price 및 Inventory Templatefield로 변환에 대 한 `ItemTemplate` 태그를 정의 하는 것입니다 .이 작업은 디자이너에서 DetailsView의 템플릿 편집 인터페이스를 통하거나 컨트롤의 선언적 구문을 통해 수행할 수 있습니다. GridView와 마찬가지로, 스마트 태그의 템플릿 편집 링크를 클릭 하 여 DetailsView의 템플릿 편집 인터페이스에 액세스할 수 있습니다. 여기에서 드롭다운 목록에서 편집할 템플릿을 선택 하 고 도구 상자에서 웹 컨트롤을 추가할 수 있습니다.

이 자습서의 경우 Price 및 Inventory Templatefield로 변환의 `ItemTemplate`에 레이블 컨트롤을 추가 하 여 시작 합니다. 그런 다음 Label 웹 컨트롤의 스마트 태그에서 데이터 바인딩 편집 링크를 클릭 하 고 `Text` 속성을 `UnitPrice` 필드에 바인딩합니다.

[레이블의 Text 속성을 UnitPrice 데이터 필드에 ![바인딩합니다.](using-templatefields-in-the-detailsview-control-cs/_static/image14.png)](using-templatefields-in-the-detailsview-control-cs/_static/image13.png)

**그림 5**: 레이블의 `Text` 속성을 `UnitPrice` 데이터 필드에 바인딩 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-detailsview-control-cs/_static/image15.png))

## <a name="formatting-the-price-as-a-currency"></a>통화로 가격 서식 지정

이 외에도 Label Web control Price 및 Inventory Templatefield로 변환는 이제 선택한 제품의 가격만 표시 합니다. 그림 6에서는 브라우저를 통해 볼 때의 진행 상황을 보여 줍니다.

[가격 및 재고 Templatefield로 변환 가격을 표시 하는 ![](using-templatefields-in-the-detailsview-control-cs/_static/image17.png)](using-templatefields-in-the-detailsview-control-cs/_static/image16.png)

**그림 6**: 가격 및 재고 templatefield로 변환 가격 ([전체 이미지를 보려면 클릭](using-templatefields-in-the-detailsview-control-cs/_static/image18.png))을 표시 합니다.

제품의 가격은 통화 형식으로 지정 되지 않습니다. BoundField를 사용 하면 `HtmlEncode` 속성을 `false`로 설정 하 고 `DataFormatString` 속성을 `{0:formatSpecifier}`로 설정 하 여 형식을 지정할 수 있습니다. 그러나 Templatefield로 변환의 경우에는 데이터 바인딩 구문이 나 응용 프로그램 코드 내에 정의 된 서식 지정 메서드 (예: ASP.NET 페이지의 코드 숨김이 클래스)를 사용 하 여 서식 지정 명령을 지정 해야 합니다.

Label 웹 컨트롤에서 사용 되는 데이터 바인딩 구문의 서식을 지정 하려면 레이블의 스마트 태그에서 데이터 바인딩 편집 링크를 클릭 하 여 데이터 바인딩 대화 상자로 돌아갑니다. 서식 드롭다운 목록에서 직접 서식 지정 지침을 입력 하거나 정의 된 서식 문자열 중 하나를 선택할 수 있습니다. BoundField의 `DataFormatString` 속성과 마찬가지로 `{0:formatSpecifier}`를 사용 하 여 서식을 지정 합니다.

`UnitPrice` 필드의 경우 적절 한 드롭다운 목록 값을 선택 하거나 직접 `{0:C}`를 입력 하 여 지정 된 통화 서식을 사용 합니다.

[가격을 통화로 서식 지정 ![](using-templatefields-in-the-detailsview-control-cs/_static/image20.png)](using-templatefields-in-the-detailsview-control-cs/_static/image19.png)

**그림 7**: 가격을 통화로 서식 지정 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-detailsview-control-cs/_static/image21.png))

선언적으로 서식 지정은 `Bind` 또는 `Eval` 메서드에 두 번째 매개 변수로 표시 됩니다. 디자이너를 통해 설정 된 설정은 선언 태그에 다음 데이터 바인딩 식을 생성 합니다.

[!code-aspx[Main](using-templatefields-in-the-detailsview-control-cs/samples/sample2.aspx)]

## <a name="adding-the-remaining-data-fields-to-the-templatefield"></a>Templatefield로 변환에 나머지 데이터 필드 추가

이 시점에서 Price 및 Inventory Templatefield로 변환의 `UnitPrice` 데이터 필드를 표시 하 고 서식을 지정 했지만 `UnitsInStock` 및 `UnitsOnOrder` 필드를 표시 해야 합니다. 가격 및 괄호 아래 줄에이를 표시 해 보겠습니다. 디자이너의 템플릿 편집 인터페이스에서 템플릿 내에 커서를 놓고 표시 될 텍스트를 입력 하기만 하면 이러한 태그를 추가할 수 있습니다. 또는 선언적 구문에서이 태그를 직접 입력할 수 있습니다.

Price 및 Inventory Templatefield로 변환에서 다음과 같이 가격 및 인벤토리 정보를 표시 하도록 정적 태그, 레이블 웹 컨트롤 및 데이터 바인딩 구문을 추가 합니다.

*UnitPrice*  
(**재고/주문:** *UnitsInStock* / *UnitsOnOrder*)

이 작업을 수행한 후에는 DetailsView의 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](using-templatefields-in-the-detailsview-control-cs/samples/sample3.aspx)]

이러한 변경 내용으로 price 및 inventory 정보를 단일 DetailsView 행으로 통합 했습니다.

[가격 및 재고 정보가 단일 행에 표시 ![](using-templatefields-in-the-detailsview-control-cs/_static/image23.png)](using-templatefields-in-the-detailsview-control-cs/_static/image22.png)

**그림 8**: 가격 및 인벤토리 정보는 단일 행에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-detailsview-control-cs/_static/image24.png)).

## <a name="step-3-customizing-the-discontinued-field-information"></a>3 단계: 단종 된 필드 정보 사용자 지정

`Products` 테이블의 `Discontinued` 열은 제품이 단종 되었는지 여부를 나타내는 비트 값입니다. DetailsView (또는 GridView)를 데이터 소스 컨트롤에 바인딩할 때 `Discontinued`와 같은 부울 값 필드는 CheckBoxFields으로 구현 되지만 부울이 아닌 값 필드 (예: `ProductID`, `ProductName`등)는 BoundFields로 구현 됩니다. CheckBoxField은 데이터 필드의 값이 True 인지 여부를 확인 하 고 그렇지 않으면 선택 취소 된 비활성화 된 확인란으로 렌더링 합니다.

CheckBoxField를 표시 하는 대신 제품이 중단 되었는지 여부를 나타내는 텍스트를 표시 하는 것이 좋습니다. 이를 위해 DetailsView에서 CheckBoxField를 제거한 다음 `DataField` 속성이 `Discontinued`로 설정 된 BoundField를 추가할 수 있습니다. 잠시 기다려 주십시오. 이 변경 후에는 DetailsView에서 중단 된 제품에 대해 "True" 라는 텍스트를 표시 하 고 아직 활성 상태인 제품에 대해서는 "False"를 표시 합니다.

[![True 및 False 문자열을 사용 하 여 중단 된 상태를 표시 합니다.](using-templatefields-in-the-detailsview-control-cs/_static/image26.png)](using-templatefields-in-the-detailsview-control-cs/_static/image25.png)

**그림 9**: 문자열 True 및 False는 중단 된 상태를 표시 하는 데 사용 됩니다 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-detailsview-control-cs/_static/image27.png)).

문자열 "True" 또는 "False"를 사용 하지 않고 대신 "YES" 및 "NO"를 사용 하려고 한다고 가정해 보겠습니다. 이러한 사용자 지정은 Templatefield로 변환 및 형식 지정 방법을 지원 하 여 수행할 수 있습니다. 서식 지정 메서드는 다양 한 입력 매개 변수를 사용할 수 있지만 템플릿에 삽입할 HTML (문자열)을 반환 해야 합니다.

부울을 입력 매개 변수로 수락 하 고 문자열을 반환 하는 `DisplayDiscontinuedAsYESorNO` 라는 `DetailsViewTemplateField.aspx` 페이지의 코드를 만든 클래스에 서식 지정 메서드를 추가 합니다. 이전 자습서에서 설명한 대로이 메서드는 템플릿에서 액세스할 수 있도록 `protected` 또는 `public`로 표시 되어야 *합니다* .

[!code-csharp[Main](using-templatefields-in-the-detailsview-control-cs/samples/sample4.cs)]

이 메서드는 입력 매개 변수 (`discontinued`)를 확인 하 고 "YES" (`true`경우 "NO")를 반환 합니다.

> [!NOTE]
> 이전 자습서에서 검사 한 서식 지정 메서드에서는 `NULL`을 포함 하는 데이터 필드를 전달 했으며, 따라서 직원의 `HiredDate` 속성 값에 `EmployeesRow`의 `HiredDate` 속성에 액세스 하기 전에 데이터베이스 `NULL` 값이 있는지 확인 해야 합니다. `Discontinued` 열에는 데이터베이스 `NULL` 값이 할당 될 수 없으므로 이러한 검사가 필요 하지 않습니다. 또한이로 인해 메서드가 `object`형식의 매개 변수 또는 `ProductsRow` 인스턴스를 수락 하지 않고 부울 입력 매개 변수를 사용할 수 있습니다.

이 형식 지정 메서드를 완료 하면 Templatefield로 변환의 `ItemTemplate`에서 호출 하는 것만 남았습니다. Templatefield로 변환를 만들려면 BoundField `Discontinued` 제거 하 고 새 Templatefield로 변환를 추가 하거나 `Discontinued` BoundField을 Templatefield로 변환로 변환 합니다. 그런 다음 선언적 마크업 뷰에서 `DisplayDiscontinuedAsYESorNO` 메서드를 호출 하는 ItemTemplate을 포함 하도록 Templatefield로 변환를 편집 하 여 현재 `ProductRow` 인스턴스의 `Discontinued` 속성 값을 전달 합니다. 이는 `Eval` 메서드를 통해 액세스할 수 있습니다. 특히 Templatefield로 변환의 태그는 다음과 같습니다.

[!code-aspx[Main](using-templatefields-in-the-detailsview-control-cs/samples/sample5.aspx)]

이렇게 하면 DetailsView을 렌더링할 때 `DisplayDiscontinuedAsYESorNO` 메서드를 호출 하 여 `ProductRow` 인스턴스의 `Discontinued` 값을 전달 합니다. `Eval` 메서드는 `object`형식의 값을 반환 하지만 `DisplayDiscontinuedAsYESorNO` 메서드에 `bool`형식의 입력 매개 변수가 필요 하기 때문에 `Eval` 메서드 반환 값을 `bool`로 캐스팅 합니다. 그러면 `DisplayDiscontinuedAsYESorNO` 메서드는 받는 값에 따라 "YES" 또는 "NO"를 반환 합니다. 반환 된 값은이 DetailsView 행에 표시 되는 값입니다 (그림 10 참조).

[현재 지원 되지 않는 행에 ![예 또는 아니요 값이 표시 됩니다.](using-templatefields-in-the-detailsview-control-cs/_static/image29.png)](using-templatefields-in-the-detailsview-control-cs/_static/image28.png)

**그림 10**: 예 또는 현재 중단 된 행에 값이 표시 되지 않음 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-detailsview-control-cs/_static/image30.png))

## <a name="summary"></a>요약

DetailsView 컨트롤의 Templatefield로 변환를 사용 하면 다른 필드 컨트롤에서 사용할 수 있는 것 보다 더 많은 유연성을 제공 하 여 데이터를 표시할 수 있으며, 다음과 같은 상황에 적합 합니다.

- 하나의 GridView 열에 여러 데이터 필드를 표시 해야 합니다.
- 데이터는 일반 텍스트가 아닌 웹 컨트롤을 사용 하 여 가장 잘 표현 됩니다.
- 출력은 메타 데이터를 표시 하거나 데이터를 다시 포맷 하는 등의 기본 데이터에 따라 달라 집니다.

서식 필드 필드는 DetailsView의 기본 데이터를 렌더링할 때 더 많은 유연성을 사용할 수 있지만 각 필드가 HTML `<table>`의 행으로 렌더링 되는 경우에도 DetailsView 출력은 약간의 느낌이 있습니다.

FormView 컨트롤을 통해 렌더링 된 출력을 보다 유연 하 게 구성할 수 있습니다. FormView는 필드를 포함 하지 않고 일련의 템플릿 (`ItemTemplate`, `EditItemTemplate`, `HeaderTemplate`등)만 포함 합니다. 다음 자습서에서 FormView를 사용 하 여 렌더링 된 레이아웃을 더욱 세밀 하 게 제어 하는 방법을 알아봅니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Dan Jagers입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](using-templatefields-in-the-gridview-control-cs.md)
> [다음](using-the-formview-s-templates-cs.md)
