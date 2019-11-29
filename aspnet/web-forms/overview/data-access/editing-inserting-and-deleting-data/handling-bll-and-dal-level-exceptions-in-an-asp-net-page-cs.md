---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs
title: ASP.NET 페이지에서 BLL 및 DAL 수준의 예외 처리 (C#) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는의 삽입, 업데이트 또는 삭제 작업을 수행 하는 동안 예외가 발생 하는 정보를 제공 하는 오류 메시지를 표시 하는 방법을 알아봅니다.
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 49d8a66c-3ea8-4087-839f-179d1d94512a
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs
msc.type: authoredcontent
ms.openlocfilehash: 2b9cdb5af6f33171b191d5a80473c7796eb098d9
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74589323"
---
# <a name="handling-bll--and-dal-level-exceptions-in-an-aspnet-page-c"></a>ASP.NET 페이지에서 BLL 및 DAL 수준의 예외 처리(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_18_CS.exe) 또는 [PDF 다운로드](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/datatutorial18cs1.pdf)

> 이 자습서에서는 ASP.NET data 웹 컨트롤의 삽입, 업데이트 또는 삭제 작업을 수행 하는 동안 예외가 발생 하는 정보를 제공 하는 오류 메시지를 표시 하는 방법을 알아봅니다.

## <a name="introduction"></a>소개

계층화 된 응용 프로그램 아키텍처를 사용 하는 ASP.NET 웹 응용 프로그램의 데이터 작업에는 다음과 같은 세 가지 일반적인 단계가 포함 됩니다.

1. 호출 해야 하는 비즈니스 논리 계층의 메서드와 전달할 매개 변수 값을 결정 합니다. 매개 변수 값은 하드 코딩 되거나, 프로그래밍 방식으로 할당 되거나, 사용자가 입력 한 입력이 될 수 있습니다.
2. 메서드를 호출합니다.
3. 결과를 처리 합니다. 데이터를 반환 하는 BLL 메서드를 호출 하는 경우 데이터를 데이터 웹 컨트롤에 바인딩하는 작업이 포함 될 수 있습니다. 데이터를 수정 하는 BLL 메서드의 경우 반환 값을 기반으로 하는 일부 작업을 수행 하거나 2 단계에서 발생 한 예외를 정상적으로 처리 하는 작업을 포함할 수 있습니다.

[이전 자습서](examining-the-events-associated-with-inserting-updating-and-deleting-cs.md)에서 살펴본 것 처럼 ObjectDataSource와 데이터 웹 컨트롤 모두 1 및 3 단계에 대 한 확장성을 제공 합니다. 예를 들어 GridView는 해당 ObjectDataSource의 `UpdateParameters` 컬렉션에 필드 값을 할당 하기 전에 `RowUpdating` 이벤트를 발생 시킵니다. ObjectDataSource가 작업을 완료 한 후 `RowUpdated` 이벤트가 발생 합니다.

1 단계에서 발생 하는 이벤트를 이미 검사 했으며이 이벤트를 사용 하 여 입력 매개 변수를 사용자 지정 하거나 작업을 취소할 수 있는 방법을 살펴보았습니다. 이 자습서에서는 작업이 완료 된 후에 발생 하는 이벤트에 주목 합니다. 이러한 사후 수준 이벤트 처리기를 사용 하면 작업 중에 예외가 발생 했는지 여부를 확인 하 고 정상적으로 처리할 수 있습니다. 표준 ASP.NET를 기본적으로 사용 하는 대신 화면에 친숙 한 정보 오류 메시지를 표시 합니다. 예외 페이지.

이러한 사후 수준 이벤트 작업을 설명 하기 위해 편집 가능한 GridView의 제품을 나열 하는 페이지를 만들어 보겠습니다. 제품을 업데이트 하는 경우 예외가 발생 하는 경우 ASP.NET 페이지가 GridView 위에 오류가 발생 했음을 설명 하는 짧은 메시지를 표시 합니다. 시작 하겠습니다.

## <a name="step-1-creating-an-editable-gridview-of-products"></a>1 단계: 편집 가능한 제품 GridView 만들기

이전 자습서에서는 두 개의 필드인 `ProductName`와 `UnitPrice`를 사용 하 여 편집 가능한 GridView를 만들었습니다. 이렇게 하려면 각 product 필드에 대 한 매개 변수 대신 세 개의 입력 매개 변수 (제품 이름, 단가 및 ID)만 허용 하는 `ProductsBLL` 클래스의 `UpdateProduct` 메서드에 대 한 추가 오버 로드를 만들어야 합니다. 이 자습서에서는이 기법을 다시 연습 하 여 제품의 이름, 단위 당 수량, 단가 및 재고 단위를 표시 하는 편집 가능한 GridView를 만들고 재고의 이름, 단가 및 단위도 편집할 수 있습니다.

이 시나리오를 수용 하려면 제품의 이름, 단가, 재고 단위 및 ID의 네 가지 매개 변수를 허용 하는 `UpdateProduct` 메서드의 다른 오버 로드가 필요 합니다. `ProductsBLL` 클래스에 다음 메서드를 추가 합니다.

[!code-csharp[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/samples/sample1.cs)]

이 메서드가 완료 되 면 이러한 4 가지 특정 제품 필드를 편집할 수 있는 ASP.NET 페이지를 만들 준비가 되었습니다. `EditInsertDelete` 폴더에서 `ErrorHandling.aspx` 페이지를 열고 디자이너를 통해 페이지에 GridView를 추가 합니다. GridView를 새 ObjectDataSource에 바인딩하여 `Select()` 메서드를 `ProductsBLL` 클래스의 `GetProducts()` 메서드에 매핑하고 `Update()` 메서드를 앞서 만든 `UpdateProduct` 오버 로드에 매핑합니다.

[4 개의 입력 매개 변수를 허용 하는 UpdateProduct 메서드 오버 로드를 사용 ![](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image2.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image1.png)

**그림 1**: 4 개의 입력 매개 변수를 허용 하는 `UpdateProduct` 메서드 오버 로드 사용 ([전체 크기 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image3.png))

그러면 4 개의 매개 변수가 있는 `UpdateParameters` 컬렉션과 각 product 필드에 대 한 필드가 있는 GridView가 만들어집니다. ObjectDataSource의 선언적 태그는 `OldValuesParameterFormatString` 속성에 `original_{0}`값을 할당 합니다. 그러면 BLL 클래스의 `original_productID` 전달 된 입력 매개 변수가 필요 하지 않기 때문에 예외가 발생 합니다. 선언적 구문에서이 설정을 완전히 제거 해야 합니다. 그렇지 않으면 `{0}`기본값으로 설정 합니다.

그런 다음 `ProductName`, `QuantityPerUnit`, `UnitPrice`및 `UnitsInStock` BoundFields만 포함 하도록 GridView를 줄이려면 상당한 합니다. 또한 필요에 따라 필요한 필드 수준 서식 지정 (예: `HeaderText` 속성 변경)을 자유롭게 적용할 수 있습니다.

이전 자습서에서는 읽기 전용 모드 및 편집 모드의 통화로 `UnitPrice` BoundField의 형식을 지정 하는 방법을 살펴보았습니다. 여기에서 동일한 작업을 수행해 보겠습니다. 그림 2에 표시 된 것 처럼 BoundField의 `DataFormatString` 속성을 `{0:c}`로 설정 하 고, 해당 `HtmlEncode` 속성을 `false`로 설정 하 고, 해당 `ApplyFormatInEditMode`을 `true`으로 설정 해야 합니다.

[화폐로 표시 되도록 UnitPrice BoundField 구성 ![](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image5.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image4.png)

**그림 2**: `UnitPrice` BoundField를 통화로 표시 하도록 구성 ([전체 크기 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image6.png))

편집 인터페이스의 통화로 `UnitPrice` 서식을 지정 하려면 통화 형식 문자열을 `decimal` 값으로 구문 분석 하는 GridView의 `RowUpdating` 이벤트에 대 한 이벤트 처리기를 만들어야 합니다. 마지막 자습서의 `RowUpdating` 이벤트 처리기도 사용자가 `UnitPrice` 값을 제공 했는지 확인 합니다. 그러나이 자습서에서는 사용자가 가격을 생략할 수 있습니다.

[!code-csharp[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/samples/sample2.cs)]

GridView는 `QuantityPerUnit` BoundField를 포함 하지만이 BoundField은 표시 목적 으로만 사용 해야 하며 사용자가 편집할 수 없습니다. 이를 정렬 하려면 BoundFields ' `ReadOnly` 속성을 `true`로 설정 하기만 하면 됩니다.

[QuantityPerUnit BoundField를 읽기 전용으로 설정 ![](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image8.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image7.png)

**그림 3**: `QuantityPerUnit` BoundField 읽기 전용으로 설정 ([전체 크기 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image9.png))

마지막으로 GridView의 스마트 태그에서 편집 사용 확인란을 선택 합니다. 이러한 단계를 완료 한 후 `ErrorHandling.aspx` 페이지의 디자이너는 그림 4와 같이 표시 됩니다.

[필요한 BoundFields를 제외한 모든를 제거 하 고 편집 사용 확인란을 선택 합니다. ![](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image11.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image10.png)

**그림 4**: 필요한 BoundFields를 제외 하 고 모두 제거 하 고 편집 사용 확인란을 선택 합니다 ([전체 크기 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image12.png)).

이 시점에서 모든 제품의 `ProductName`, `QuantityPerUnit`, `UnitPrice`및 `UnitsInStock` 필드가 나열 됩니다. 그러나 `ProductName`, `UnitPrice`및 `UnitsInStock` 필드만 편집할 수 있습니다.

[이제 사용자 ![재고 필드에서 제품의 이름, 가격 및 단위를 쉽게 편집할 수 있습니다.](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image14.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image13.png)

**그림 5**: 이제 사용자는 재고 필드에서 제품의 이름, 가격 및 단위를 쉽게 편집할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image15.png)).

## <a name="step-2-gracefully-handling-dal-level-exceptions"></a>2 단계: DAL 수준 예외를 정상적으로 처리

편집 가능한 GridView는 사용자가 편집 된 제품의 이름, 가격 및 재고 단위에 대 한 올바른 값을 입력 하는 경우 wonderfully 작동 하지만 잘못 된 값을 입력 하면 예외가 발생 합니다. 예를 들어 `ProductName` 값을 생략 하면 `ProductsRow` 클래스의 `ProductName` 속성에 `AllowDBNull` 속성이 `false`로 설정 되어 있기 때문에 [system.data.nonullallowedexception](https://msdn.microsoft.com/library/default.asp?url=/library/cpref/html/frlrfsystemdatanonullallowedexceptionclasstopic.asp) 이 throw 됩니다. 데이터베이스가 다운 되 면 데이터베이스에 연결을 시도할 때 TableAdapter에서 `SqlException`이 throw 됩니다. 작업을 수행 하지 않고 이러한 예외는 데이터 액세스 계층에서 비즈니스 논리 계층으로 버블링 된 다음 ASP.NET 페이지와 마지막으로 ASP.NET 런타임으로 버블링 됩니다.

웹 응용 프로그램을 구성 하는 방법 및 응용 프로그램을 `localhost`에서 방문 하는지 여부에 따라 처리 되지 않은 예외로 인해 일반 서버 오류 페이지, 자세한 오류 보고서 또는 사용자에 게 친숙 한 웹 페이지가 표시 될 수 있습니다. ASP.NET 런타임이 catch 되지 않은 예외에 응답 하는 방법에 대 한 자세한 내용은 [ASP.NET의 웹 응용 프로그램 오류 처리](http://www.15seconds.com/issue/030102.htm) 및 [customErrors 요소](https://msdn.microsoft.com/library/h0hfz6fc(VS.80).aspx) 를 참조 하세요.

그림 6에서는 `ProductName` 값을 지정 하지 않고 제품 업데이트를 시도할 때 발생 하는 화면을 보여 줍니다. 이는 `localhost`을 통해 제공 될 때 표시 되는 기본 자세한 오류 보고서입니다.

[제품 이름을 생략 ![예외 정보가 표시 됩니다.](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image17.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image16.png)

**그림 6**: 제품 이름을 생략 하면 예외 정보가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image18.png)).

이러한 예외 정보는 응용 프로그램을 테스트할 때 유용 하지만, 최종 사용자에 게 예외를 발생 한 화면에 표시 하는 것은 이상적인 것 보다 낮습니다. 최종 사용자가 `NoNullAllowedException` 무엇 인지 또는 왜 발생 했는지 알 수 없습니다. 더 나은 방법은 제품 업데이트를 시도 하는 데 문제가 있다는 것을 설명 하는 보다 사용자에 게 친숙 한 메시지를 사용자에 게 제공 하는 것입니다.

작업을 수행할 때 예외가 발생 하는 경우 ObjectDataSource 및 데이터 웹 컨트롤의 사후 수준 이벤트는이를 감지 하 고 ASP.NET 런타임에 대 한 버블링에서 예외를 취소 하는 수단을 제공 합니다. 이 예제에서는 예외가 발생 했는지 여부를 확인 하 고 레이블 웹 컨트롤에 예외 세부 정보를 표시 하는 GridView의 `RowUpdated` 이벤트에 대 한 이벤트 처리기를 만들어 보겠습니다.

ASP.NET 페이지에 레이블을 추가 하 고 해당 `ID` 속성을 `ExceptionDetails` 설정 하 고 `Text` 속성을 지워 시작 합니다. 이 메시지에 사용자의 눈동자를 그리려면 `CssClass` 속성을 이전 자습서의 `Styles.css` 파일에 추가한 CSS 클래스인 `Warning`으로 설정 합니다. 이 CSS 클래스를 통해 레이블의 텍스트가 빨강, 기울임꼴, 굵게, 초대형 글꼴로 표시 됩니다.

[페이지에 Label 웹 컨트롤을 추가 ![](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image20.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image19.png)

**그림 7**: 페이지에 Label 웹 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image21.png))

예외가 발생 한 직후에이 Label 웹 컨트롤을 표시 하려면 `Page_Load` 이벤트 처리기에서 `Visible` 속성을 false로 설정 합니다.

[!code-csharp[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/samples/sample3.cs)]

이 코드를 사용 하 여 첫 번째 페이지를 방문 하 고 이후에 다시 게시 하면 `ExceptionDetails` 컨트롤의 `Visible` 속성이 `false`으로 설정 됩니다. GridView의 `RowUpdated` 이벤트 처리기에서 검색할 수 있는 DAL 또는 BLL 수준 예외의 면에서 `ExceptionDetails` 컨트롤의 `Visible` 속성을 true로 설정 합니다. 웹 컨트롤 이벤트 처리기는 페이지 수명 주기의 `Page_Load` 이벤트 처리기 이후에 발생 하므로 레이블이 표시 됩니다. 그러나 다음 포스트백에서 `Page_Load` 이벤트 처리기는 `Visible` 속성을 다시 `false`으로 되돌리고 뷰에서 다시 숨깁니다.

> [!NOTE]
> 또는 선언적 구문에서 `Visible` 속성 `false`을 할당 하 고 해당 뷰 상태 (`EnableViewState` 속성을 `false`로 설정)를 사용 하지 않도록 설정 하 여 `Page_Load`에서 `ExceptionDetails` 컨트롤의 `Visible` 속성을 설정 하는 데 필요한 기능을 제거할 수 있습니다. 이후 자습서에서는이 대체 방법을 사용 합니다.

레이블 컨트롤이 추가 되 면 다음 단계는 GridView의 `RowUpdated` 이벤트에 대 한 이벤트 처리기를 만드는 것입니다. 디자이너에서 GridView를 선택 하 고 속성 창으로 이동한 후 번개 아이콘을 클릭 하 여 GridView의 이벤트를 나열 합니다. 이 자습서의 앞부분에서이 이벤트에 대 한 이벤트 처리기를 만들었으므로 GridView의 `RowUpdating` 이벤트에 대 한 항목이 이미 있습니다. `RowUpdated` 이벤트에 대 한 이벤트 처리기도 만듭니다.

![GridView의 RowUpdated 이벤트에 대 한 이벤트 처리기 만들기](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image22.png)

**그림 8**: GridView의 `RowUpdated` 이벤트에 대 한 이벤트 처리기 만들기

> [!NOTE]
> 코드 지향 클래스 파일의 맨 위에 있는 드롭다운 목록을 통해 이벤트 처리기를 만들 수도 있습니다. 왼쪽의 드롭다운 목록에서 GridView를 선택 하 고 오른쪽에 있는 `RowUpdated` 이벤트를 선택 합니다.

이 이벤트 처리기를 만들면 ASP.NET 페이지의 코드 숨김이 클래스에 다음 코드가 추가 됩니다.

[!code-csharp[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/samples/sample4.cs)]

이 이벤트 처리기의 두 번째 입력 매개 변수는 예외를 처리 하는 데 필요한 세 가지 속성을 포함 하는 [GridViewUpdatedEventArgs](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridviewupdatedeventargs.aspx)형식의 개체입니다.

- throw 된 예외에 대 한 참조를 `Exception` 합니다. 예외가 throw 되지 않은 경우이 속성의 값은 `null`
- 예외가 `RowUpdated` 이벤트 처리기에서 처리 되었는지 여부를 나타내는 부울 값을 `ExceptionHandled` 합니다. `false` (기본값) 이면 예외가 다시 throw 되 고 ASP.NET 런타임으로 배치 됩니다.
- `true`로 설정 하면 편집 된 GridView 행이 편집 모드에 남아 `KeepInEditMode`. `false` (기본값) 이면 GridView 행이 읽기 전용 모드로 돌아갑니다.

그런 다음 코드는 `Exception` `null`되지 않았는지 확인 해야 합니다. 즉, 작업을 수행 하는 동안 예외가 발생 했음을 확인 해야 합니다. 이 경우 다음과 같은 작업을 수행 합니다.

- `ExceptionDetails` 레이블에 사용자에 게 친숙 한 메시지 표시
- 예외가 처리 되었음을 표시 합니다.
- 편집 모드에서 GridView 행 유지

이러한 목표를 달성 하는 코드는 다음과 같습니다.

[!code-csharp[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/samples/sample5.cs)]

이 이벤트 처리기는 `e.Exception` `null`되었는지 확인 하 여 시작 합니다. 그렇지 않은 경우 `ExceptionDetails` 레이블의 `Visible` 속성은 `true`로 설정 되 고 해당 `Text` 속성은 "제품을 업데이트 하는 데 문제가 있습니다."로 설정 됩니다. Throw 된 실제 예외의 세부 정보는 `e.Exception` 개체의 `InnerException` 속성에 있습니다. 이 내부 예외를 검사 하 고 특정 형식이 면 `ExceptionDetails` 레이블의 `Text` 속성에 추가 유용한 메시지가 추가 됩니다. 마지막으로 `ExceptionHandled` 및 `KeepInEditMode` 속성이 모두 `true`로 설정 됩니다.

그림 9에서는 제품 이름을 생략 하는 경우이 페이지의 스크린샷 그림 10에서는 잘못 된 `UnitPrice` 값 (-50)을 입력할 때의 결과를 보여 줍니다.

[![ProductName BoundField는 값을 포함 해야 합니다.](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image24.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image23.png)

**그림 9**: `ProductName` BoundField는 값을 포함 해야 합니다 ([전체 크기 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image25.png)).

[![음수 UnitPrice 값은 사용할 수 없습니다.](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image27.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image26.png)

**그림 10**: 음수 `UnitPrice` 값이 허용 되지 않음 ([전체 크기 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image28.png))

`e.ExceptionHandled` 속성을 `true`로 설정 하면 `RowUpdated` 이벤트 처리기에서 예외를 처리 했음을 나타냅니다. 따라서 예외는 ASP.NET 런타임으로 전파 되지 않습니다.

> [!NOTE]
> 그림 9와 10은 잘못 된 사용자 입력으로 인해 발생 하는 예외를 처리 하는 정상적인 방법을 보여 줍니다. ASP.NET 페이지는 `ProductsBLL` 클래스의 `UpdateProduct` 메서드를 호출 하기 전에 사용자 입력이 올바른지 확인 해야 하기 때문에 이러한 잘못 된 입력은 처음에는 비즈니스 논리 계층에 도달 하지 않습니다. 다음 자습서에서는 편집 및 삽입 인터페이스에 유효성 검사 컨트롤을 추가 하 여 비즈니스 논리 계층에 제출 된 데이터가 비즈니스 규칙을 따르는지 확인 하는 방법을 알아봅니다. 유효성 검사 컨트롤은 사용자가 제공 하는 데이터가 유효 해질 때까지 `UpdateProduct` 메서드 호출을 방지할 뿐만 아니라 데이터 입력 문제를 식별 하는 데 더 유용한 사용자 환경을 제공 합니다.

## <a name="step-3-gracefully-handling-bll-level-exceptions"></a>3 단계: BLL 수준 예외를 정상적으로 처리

데이터를 삽입, 업데이트 또는 삭제 하는 경우 데이터 액세스 계층이 데이터 관련 오류 발생 시 예외를 throw 할 수 있습니다. 데이터베이스가 오프 라인 이거나, 필요한 데이터베이스 테이블 열에 값이 지정 되지 않았거나, 테이블 수준 제약 조건이 위반 되었을 수 있습니다. 비즈니스 논리 계층에서는 엄격한 데이터 관련 예외 외에도 예외를 사용 하 여 비즈니스 규칙이 위반 된 시기를 나타낼 수 있습니다. 예를 들어 [비즈니스 논리 계층 만들기](../introduction/creating-a-business-logic-layer-cs.md) 자습서에서 원래 `UpdateProduct` 오버 로드에 비즈니스 규칙 검사를 추가 했습니다. 특히, 사용자가 제품을 단종 된 것으로 표시 한 경우에는 해당 공급 업체가 제공 하는 제품이 아닌 제품만 필요 합니다. 이 조건을 위반 하는 경우 `ApplicationException` throw 됩니다.

이 자습서에서 만든 `UpdateProduct` 오버 로드의 경우 `UnitPrice` 필드가 원래 `UnitPrice` 값의 두 배가 넘는 새 값으로 설정 되는 것을 금지 하는 비즈니스 규칙을 추가 해 보겠습니다. 이를 수행 하려면 `UpdateProduct` 오버 로드를 조정 하 여이 검사를 수행 하 고 규칙을 위반 하는 경우 `ApplicationException`을 throw 합니다. 업데이트 된 메서드는 다음과 같습니다.

[!code-csharp[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/samples/sample6.cs)]

이러한 변경으로 인해 기존 가격의 두 배가 넘는 가격 업데이트는 `ApplicationException`을 throw 합니다. DAL에서 발생 한 예외와 마찬가지로,이 `ApplicationException` BLL에서 발생 하는이를 검색 하 고 GridView의 `RowUpdated` 이벤트 처리기에서 처리할 수 있습니다. 실제로 작성 된 `RowUpdated` 이벤트 처리기의 코드는이 예외를 올바르게 검색 하 고 `ApplicationException`의 `Message` 속성 값을 표시 합니다. 그림 11은 사용자가 Chai의 가격을 $50.00로 업데이트 하려고 시도 하는 경우의 스크린샷 ($19.95의 현재 가격의 2 배 이상)을 보여 줍니다.

[비즈니스 규칙이 가격을 허용 하지 않는 경우 제품 가격을 2 배 이상으로 ![합니다.](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image30.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image29.png)

**그림 11**: 기간을 허용 하지 않는 비즈니스 규칙은 제품의 가격을 두 배로 늘리는 경우 ([전체 크기 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image31.png))

> [!NOTE]
> 비즈니스 논리 규칙은 `UpdateProduct` 메서드 오버 로드 및 일반적인 메서드로 리팩터링 하는 것이 가장 좋습니다. 이는 판독기의 연습으로 남아 있습니다.

## <a name="summary"></a>요약

삽입, 업데이트 및 삭제 작업 중에는 데이터 웹 컨트롤과 ObjectDataSource가 모두 실제 작업을 bookend 하는 사전 및 사후 수준 이벤트를 발생 시킵니다. 이 자습서와 앞에서 살펴본 것 처럼 편집 가능한 GridView를 사용 하 여 작업 하는 경우 GridView의 `RowUpdating` 이벤트가 발생 하 고 그 다음에 ObjectDataSource의 `Updating` 이벤트가 발생 합니다 .이 시점에서 ObjectDataSource의 내부 개체에 대 한 update 명령이 수행 됩니다. 작업이 완료 되 면 ObjectDataSource의 `Updated` 이벤트가 실행 된 다음 GridView의 `RowUpdated` 이벤트가 발생 합니다.

작업 결과를 검사 하 고 응답 하기 위해 사후 수준 이벤트에 대 한 입력 매개 변수를 사용자 지정 하기 위해 사전 수준 이벤트에 대 한 이벤트 처리기를 만들 수 있습니다. 사후 수준 이벤트 처리기는 작업 중에 예외가 발생 했는지 여부를 검색 하는 데 가장 일반적으로 사용 됩니다. 예외가 발생 하는 경우 이러한 사후 수준 이벤트 처리기는 선택적으로 예외를 처리할 수 있습니다. 이 자습서에서는 친숙 한 오류 메시지를 표시 하 여 이러한 예외를 처리 하는 방법을 살펴보았습니다.

다음 자습서에서는 데이터 서식 문제 (예: 음수 `UnitPrice`입력)에서 발생 하는 예외의 가능성을 완화 하는 방법을 알아봅니다. 특히 편집 및 삽입 인터페이스에 유효성 검사 컨트롤을 추가 하는 방법을 살펴보겠습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Liz Shulok입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](examining-the-events-associated-with-inserting-updating-and-deleting-cs.md)
> [다음](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs.md)
