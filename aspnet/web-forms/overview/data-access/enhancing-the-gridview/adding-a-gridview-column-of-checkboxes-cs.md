---
uid: web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs
title: 확인란의 GridView 열 추가 (C#) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 GridView 컨트롤에 확인란 열을 추가 하 여 사용자에 게 여러 개의 G 행을 선택할 수 있는 직관적인 방법을 제공 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 03/06/2007
ms.assetid: f63a9443-2db0-4f80-8246-840d3e86c2a3
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs
msc.type: authoredcontent
ms.openlocfilehash: b9d1ed50e8d88202c3286b4cd0e9ebf111dfbe21
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78478271"
---
# <a name="adding-a-gridview-column-of-checkboxes-c"></a>확인란의 GridView 열 추가(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_52_CS.exe) 또는 [PDF 다운로드](adding-a-gridview-column-of-checkboxes-cs/_static/datatutorial52cs1.pdf)

> 이 자습서에서는 GridView 컨트롤에 확인란 열을 추가 하 여 사용자에 게 GridView의 여러 행을 선택할 수 있는 직관적인 방법을 제공 하는 방법을 보여 줍니다.

## <a name="introduction"></a>소개

이전 자습서에서는 특정 레코드를 선택 하기 위해 GridView에 라디오 단추 열을 추가 하는 방법을 살펴보았습니다. 사용자가 그리드에서 최대 하나의 항목을 선택할 수 있는 경우 라디오 단추 열은 적절 한 사용자 인터페이스입니다. 그러나 때때로 사용자가 표에서 임의 개수의 항목을 선택할 수 있도록 할 수 있습니다. 예를 들어 웹 기반 전자 메일 클라이언트는 일반적으로 확인란의 열이 있는 메시지 목록을 표시 합니다. 사용자는 임의의 수의 메시지를 선택한 다음 전자 메일을 다른 폴더로 이동 하거나 삭제 하는 등의 작업을 수행할 수 있습니다.

이 자습서에서는 확인란의 열을 추가 하는 방법 및 다시 게시할 때 선택 된 확인란을 확인 하는 방법을 알아봅니다. 특히 웹 기반 전자 메일 클라이언트 사용자 인터페이스와 긴밀 하 게 비슷한 예제를 작성 합니다. 이 예에는 `Products` 데이터베이스 테이블에서 각 행에 확인란을 포함 하 여 제품을 나열 하는 페이징된 GridView가 포함 됩니다 (그림 1 참조). 선택한 제품 삭제 단추를 클릭 하면 선택한 제품이 삭제 됩니다.

[각 제품 행 ![확인란을 포함 합니다.](adding-a-gridview-column-of-checkboxes-cs/_static/image1.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image1.png)

**그림 1**: 각 제품 행에는 확인란 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-checkboxes-cs/_static/image2.png))이 포함 되어 있습니다.

## <a name="step-1-adding-a-paged-gridview-that-lists-product-information"></a>1 단계: 제품 정보를 나열 하는 페이징된 GridView 추가

확인란의 열을 추가 하는 것에 대해 걱정 하기 전에 먼저 페이징을 지 원하는 GridView에서 제품을 나열 하는 데 초점을 둡니다. 먼저 `EnhancedGridView` 폴더에서 `CheckBoxField.aspx` 페이지를 열고 GridView를 도구 상자에서 디자이너로 끌어와 `ID`를 `Products`로 설정 합니다. 그런 다음 GridView를 `ProductsDataSource`라는 새 ObjectDataSource에 바인딩하려면 선택 합니다. `ProductsBLL` 클래스를 사용 하 여 `GetProducts()` 메서드를 호출 하 여 데이터를 반환 하도록 ObjectDataSource를 구성 합니다. 이 GridView는 읽기 전용 이므로 업데이트, 삽입 및 삭제 탭의 드롭다운 목록을 (없음)으로 설정 합니다.

[ProductsDataSource 라는 새 ObjectDataSource를 만들 ![](adding-a-gridview-column-of-checkboxes-cs/_static/image2.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image3.png)

**그림 2**: `ProductsDataSource` 라는 새 ObjectDataSource 만들기 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-checkboxes-cs/_static/image4.png))

[GetProducts () 메서드를 사용 하 여 데이터를 검색 하도록 ObjectDataSource를 구성 ![](adding-a-gridview-column-of-checkboxes-cs/_static/image3.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image5.png)

**그림 3**: `GetProducts()` 메서드를 사용 하 여 데이터를 검색 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-checkboxes-cs/_static/image6.png))

[업데이트, 삽입 및 삭제 탭의 드롭다운 목록을 (없음)으로 설정 ![](adding-a-gridview-column-of-checkboxes-cs/_static/image4.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image7.png)

**그림 4**: 업데이트, 삽입 및 삭제 탭의 드롭다운 목록을 (없음)로 설정 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-checkboxes-cs/_static/image8.png))

데이터 소스 구성 마법사를 완료 한 후 Visual Studio에서는 제품 관련 데이터 필드에 대 한 BoundColumns 및 CheckBoxColumn을 자동으로 만듭니다. 이전 자습서에서와 같이 `ProductName`, `CategoryName`및 `UnitPrice` BoundFields를 제외한 모든 항목을 제거 하 고 `HeaderText` 속성을 Product, Category 및 Price로 변경 합니다. `UnitPrice` BoundField를 구성 하 여 해당 값의 서식을 통화로 지정 합니다. 또한 스마트 태그에서 페이징 사용 확인란을 선택 하 여 페이징을 지원 하도록 GridView를 구성 합니다.

또한 선택한 제품을 삭제 하는 사용자 인터페이스도 추가 합니다. GridView 아래에 단추 웹 컨트롤을 추가 하 고 해당 `ID` `DeleteSelectedProducts`로 설정 하 고 `Text` 속성을 선택 하 여 선택한 제품을 삭제 합니다. 이 예에서는 데이터베이스에서 실제로 제품을 삭제 하는 대신 삭제 된 제품을 나타내는 메시지를 표시 합니다. 이를 수용 하려면 단추 아래에 Label 웹 컨트롤을 추가 합니다. 해당 ID를 `DeleteResults`설정 하 고 `Text` 속성의 선택을 취소 한 다음 `Visible` 및 `EnableViewState` 속성을 `false`로 설정 합니다.

이러한 변경을 수행한 후 GridView, ObjectDataSource, Button 및 Label s 선언 태그는 다음과 유사 합니다.

[!code-aspx[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample1.aspx)]

잠시 시간을 들 여 브라우저에서 페이지를 봅니다 (그림 5 참조). 이 시점에서 처음 10 개 제품의 이름, 범주 및 가격이 표시 되어야 합니다.

[![처음 10 개 제품의 이름, 범주 및 가격이 나열 됩니다.](adding-a-gridview-column-of-checkboxes-cs/_static/image5.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image9.png)

**그림 5**: 처음 10 개 제품의 이름, 범주 및 가격이 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-checkboxes-cs/_static/image10.png)).

## <a name="step-2-adding-a-column-of-checkboxes"></a>2 단계: 확인란 열 추가

ASP.NET 2.0에는 CheckBoxField가 포함 되므로 확인란의 열을 GridView에 추가 하는 데 사용할 수 있습니다. 그러나 CheckBoxField가 부울 데이터 필드를 사용 하도록 설계 되었으므로이는 그렇지 않습니다. 즉, CheckBoxField을 사용 하려면 렌더링 된 확인란이 선택 되었는지 여부를 확인 하기 위해 값이 확인 되는 기본 데이터 필드를 지정 해야 합니다. CheckBoxField를 사용 하 여 선택 하지 않은 확인란의 열만 포함할 수 있습니다.

대신 Templatefield로 변환를 추가 하 고 CheckBox 웹 컨트롤을 `ItemTemplate`에 추가 해야 합니다. 계속 해 서 `Products` GridView에 Templatefield로 변환를 추가 하 고 첫 번째 (맨 왼쪽) 필드로 만듭니다. GridView의 스마트 태그에서 템플릿 편집 링크를 클릭 한 다음 CheckBox 웹 컨트롤을 도구 상자에서 `ItemTemplate`끌어옵니다. 이 CheckBox s `ID` 속성을 `ProductSelector`로 설정 합니다.

[Templatefield로 변환 s ItemTemplate에 이름이 인 CheckBox 웹 컨트롤을 추가 합니다. ![](adding-a-gridview-column-of-checkboxes-cs/_static/image6.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image11.png)

**그림 6**: templatefield로 변환 s `ItemTemplate`에 `ProductSelector` 라는 CheckBox 웹 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-checkboxes-cs/_static/image12.png))

Templatefield로 변환 및 CheckBox 웹 컨트롤이 추가 되 면 이제 각 행에 확인란이 포함 됩니다. 그림 7에서는 Templatefield로 변환 및 확인란이 추가 된 후 브라우저를 통해 볼 때이 페이지를 보여 줍니다.

[![각 제품 행에는 이제 확인란이 포함 되어 있습니다.](adding-a-gridview-column-of-checkboxes-cs/_static/image7.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image13.png)

**그림 7**: 각 제품 행에는 이제 확인란이 포함 되어 있습니다 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-checkboxes-cs/_static/image14.png)).

## <a name="step-3-determining-what-checkboxes-were-checked-on-postback"></a>3 단계: 다시 게시할 때 체크 인 한 확인란 확인

이 시점에는 checkbox 열이 있지만 다시 게시할 때 체크 인 한 확인란을 결정할 수 있는 방법은 없습니다. 그러나 선택한 제품 삭제 단추를 클릭 하면 해당 제품을 삭제 하기 위해 어떤 확인란을 선택 했는지 확인 해야 합니다.

GridView s의 [`Rows` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rows.aspx) 은 gridview의 데이터 행에 대 한 액세스를 제공 합니다. 이러한 행을 반복 하 고 CheckBox 컨트롤에 프로그래밍 방식으로 액세스 한 다음 `Checked` 속성을 참조 하 여 확인란이 선택 되었는지 여부를 확인할 수 있습니다.

`DeleteSelectedProducts` Button Web control s `Click` 이벤트에 대 한 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-csharp[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample2.cs)]

`Rows` 속성은 GridView의 데이터 행을 구성을 하는 `GridViewRow` 인스턴스의 컬렉션을 반환 합니다. `foreach` 루프는이 컬렉션을 열거 합니다. 각 `GridViewRow` 개체에 대해 `row.FindControl("controlID")`를 사용 하 여 행 s 확인란에 프로그래밍 방식으로 액세스 합니다. 확인란을 선택 하면 `DataKeys` 컬렉션에서 해당 `ProductID` 값의 행이 검색 됩니다. 이 연습에서는 `DeleteResults` 레이블에 정보 메시지를 표시 합니다. 하지만 작업 중인 응용 프로그램에서는 대신 `ProductsBLL` 클래스 s `DeleteProduct(productID)` 메서드를 호출 하 게 됩니다.

이 이벤트 처리기가 추가 되 면 선택한 제품 삭제 단추를 클릭 하면 선택한 제품의 `ProductID`가 표시 됩니다.

[선택한 제품 삭제 단추를 클릭 하면 선택한 Productid 나열 됩니다. ![](adding-a-gridview-column-of-checkboxes-cs/_static/image8.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image15.png)

**그림 8**: 선택한 제품 삭제 단추를 클릭 하면 선택한 `ProductID` 제품이 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-checkboxes-cs/_static/image16.png)).

## <a name="step-4-adding-check-all-and-uncheck-all-buttons"></a>4 단계: 모두 선택 확인 및 모든 단추 선택 취소

사용자가 현재 페이지의 모든 제품을 삭제 하려는 경우에는 각각의 10 개 확인란을 선택 해야 합니다. 클릭 하면 표의 모든 확인란을 선택 하는 모두 확인 단추를 추가 하 여이 프로세스를 신속 하 게 수행할 수 있습니다. 모두 선택 취소 단추는 동일 하 게 유용 합니다.

페이지에 두 개의 단추 웹 컨트롤을 추가 하 여 GridView 위에 배치 합니다. 첫 번째 `ID`를 `CheckAll`로 설정 하 고 `Text` 속성을 모두 확인 합니다. `UncheckAll` `ID` 두 번째를 설정 하 고 `Text` 속성을 모두 선택 취소 합니다.

[!code-aspx[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample3.aspx)]

그런 다음 호출 될 때 `Products` GridView s `Rows` 컬렉션을 열거 하 고 각 CheckBox `Checked` 속성을 전달 된 *checkState* 매개 변수의 값으로 설정 하는 `ToggleCheckState(checkState)` 코드를 만든 클래스에 메서드를 만듭니다.

[!code-csharp[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample4.cs)]

그런 다음 `CheckAll` 및 `UncheckAll` 단추에 대 한 `Click` 이벤트 처리기를 만듭니다. `CheckAll` s 이벤트 처리기에서 `ToggleCheckState(true)`만 호출 합니다. `UncheckAll`에서 `ToggleCheckState(false)`를 호출 합니다.

[!code-csharp[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample5.cs)]

이 코드를 사용 하면 모두 확인 단추를 클릭 하면 포스트백이 발생 하 고 GridView의 모든 확인란을 확인 합니다. 마찬가지로 모두 선택 취소를 클릭 하 여 모든 확인란의 선택을 취소 합니다. 그림 9는 모두 확인 단추가 선택 된 후의 화면을 보여 줍니다.

[모두 확인 단추를 클릭 하면 모든 확인란이 선택 ![.](adding-a-gridview-column-of-checkboxes-cs/_static/image9.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image17.png)

**그림 9**: 모두 확인 단추를 클릭 하면 모든 확인란 선택 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-checkboxes-cs/_static/image18.png))

> [!NOTE]
> 확인란의 열을 표시 하는 경우 모든 확인란을 선택 하거나 선택 취소 하는 한 가지 방법은 머리글 행의 확인란을 선택 하는 것입니다. 또한 현재 모두 확인/모든 구현 선택을 취소 하려면 다시 게시 해야 합니다. 그러나 확인란을 선택 하거나 선택 취소 하 여 클라이언트 쪽 스크립트를 통해 완전히 snappier 사용자 환경을 제공할 수 있습니다. 클라이언트 쪽 기술을 사용 하는 방법에 대 한 설명과 함께 모두 확인 및 모두 선택 취소에 대 한 머리글 행 확인란을 사용 하 여 살펴보려면 [클라이언트 쪽 스크립트를 사용 하 여 GridView의 모든 확인란을 선택 하 고 모두 확인](http://aspnet.4guysfromrolla.com/articles/053106-1.aspx)확인란을 선택 합니다.

## <a name="summary"></a>요약

계속 하기 전에 사용자가 GridView에서 임의 개수의 행을 선택할 수 있도록 해야 하는 경우에는 checkbox 열을 추가 하는 옵션이 있습니다. 이 자습서에서 살펴본 것 처럼 GridView의 확인란 열을 포함 하는 것은 CheckBox 웹 컨트롤을 사용 하 여 Templatefield로 변환를 추가 하는 것입니다. 이전 자습서에서 설명한 것과 같이 웹 컨트롤을 사용 하 여 태그를 템플릿에 직접 삽입 하는 것과 같이 ASP.NET는 자동으로 확인란을 기억 하 고 다시 게시 하는 동안 검사 되지 않았음을 확인 합니다. 코드의 확인란에 프로그래밍 방식으로 액세스 하 여 지정 된 확인란이 선택 되었는지 확인 하거나 선택 된 상태를 변경할 수도 있습니다.

이 자습서와 마지막 항목에서는 GridView에 행 선택기 열을 추가 하는 방법을 살펴보았습니다. 다음 자습서에서는 약간의 작업을 통해 GridView에 삽입 기능을 추가할 수 있는 방법을 살펴보겠습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

> [!div class="step-by-step"]
> [이전](adding-a-gridview-column-of-radio-buttons-cs.md)
> [다음](inserting-a-new-record-from-the-gridview-s-footer-cs.md)
