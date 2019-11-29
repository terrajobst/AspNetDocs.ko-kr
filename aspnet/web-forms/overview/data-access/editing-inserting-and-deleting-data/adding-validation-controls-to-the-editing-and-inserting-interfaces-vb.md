---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb
title: 편집 및 삽입 인터페이스에 유효성 검사 컨트롤 추가 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 데이터 웹 컨트롤의 EditItemTemplate 및 InsertItemTemplate에 유효성 검사 컨트롤을 추가 하는 것이 얼마나 쉬운지 알아봅니다.
ms.author: riande
ms.date: 07/17/2006
ms.assetid: e3d7028a-7a22-4a4f-babe-d53afc41c0e2
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb
msc.type: authoredcontent
ms.openlocfilehash: 5c5ad110ee0836f0a464b02a2b29254e2e06381e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74571347"
---
# <a name="adding-validation-controls-to-the-editing-and-inserting-interfaces-vb"></a>편집 및 삽입 인터페이스에 유효성 검사 컨트롤 추가(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_19_VB.exe) 또는 [PDF 다운로드](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/datatutorial19vb1.pdf)

> 이 자습서에서는 더 간단 하 게 사용자 인터페이스를 제공 하기 위해 데이터 웹 컨트롤의 EditItemTemplate 및 InsertItemTemplate에 유효성 검사 컨트롤을 추가 하는 것이 얼마나 쉬운지 알아봅니다.

## <a name="introduction"></a>소개

지난 세 자습서에 대해 살펴본 예제에서 GridView 및 DetailsView 컨트롤은 모두 BoundFields 및 CheckBoxFields로 구성 되었습니다. GridView 또는 DetailsView을 데이터 소스에 바인딩할 때 Visual Studio에서 자동으로 추가 되는 필드 형식입니다. 스마트 태그를 통해 제어 합니다. GridView 또는 DetailsView의 행을 편집 하는 경우 읽기 전용이 아닌 BoundFields은 최종 사용자가 기존 데이터를 수정할 수 있는 텍스트 상자로 변환 됩니다. 마찬가지로, DetailsView 컨트롤에 새 레코드를 삽입 하는 경우 `InsertVisible` 속성이 `True` (기본값)로 설정 된 해당 BoundFields는 사용자가 새 레코드의 필드 값을 제공할 수 있는 빈 텍스트 상자를 렌더링 합니다. 마찬가지로, 표준 읽기 전용 인터페이스에서 사용 하지 않도록 설정 된 CheckBoxFields는 편집 및 삽입 인터페이스의 사용 확인란으로 변환 됩니다.

BoundField 및 CheckBoxField에 대 한 기본 편집 및 삽입 인터페이스는 유용할 수 있지만 인터페이스에는 어떤 종류의 유효성 검사가 없습니다. `ProductName` 필드를 생략 하거나 `UnitsInStock` (예:-50)에 대해 잘못 된 값을 입력 하는 경우와 같이 사용자가 실수로 데이터를 입력 하는 경우 응용 프로그램 아키텍처의 깊이에서 예외가 발생 합니다. [이전 자습서](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md)에서 설명한 대로이 예외를 정상적으로 처리할 수 있지만 사용자 인터페이스를 편집 하거나 삽입 하는 것은 사용자가 첫 번째 위치의 잘못 된 데이터를 입력 하지 못하도록 하는 유효성 검사 컨트롤을 포함 하는 것이 가장 좋습니다.

사용자 지정 된 편집 또는 삽입 인터페이스를 제공 하기 위해 BoundField 또는 CheckBoxField를 Templatefield로 변환로 바꾸어야 합니다. [GridView 컨트롤에서 서식 파일 필드를 사용](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md) 하 고 [DetailsView 컨트롤 자습서에서 서식](../custom-formatting/using-templatefields-in-the-detailsview-control-vb.md) 파일 필드를 사용 하는 방법에 대 한 설명 항목에 해당 하는 서식 파일 필드는 서로 다른 행 상태에 대해 별도의 인터페이스를 정의 하는 여러 템플릿으로 구성할 수 있습니다. Templatefield로 변환의 `ItemTemplate`은 DetailsView 또는 GridView 컨트롤에서 읽기 전용 필드 또는 행을 렌더링할 때 사용 되는 반면 `EditItemTemplate` 및 `InsertItemTemplate`는 각각 편집 및 삽입 모드에 사용할 인터페이스를 지정 합니다.

이 자습서에서는 Templatefield로 변환의 `EditItemTemplate`에 유효성 검사 컨트롤을 추가 하는 것이 얼마나 쉬운지 확인 하 고 `InsertItemTemplate` 하 여 보다 간단 하 게 사용자 인터페이스를 제공 합니다. 특히이 자습서에서는 [삽입, 업데이트 및 삭제 자습서와 관련 된 이벤트를 검사](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md) 하 고 적절 한 유효성 검사를 포함 하는 편집 및 삽입 인터페이스를 보강 하 여 만든 예제를 사용 합니다.

## <a name="step-1-replicating-the-example-fromexamining-the-events-associated-with-inserting-updating-and-deletingexamining-the-events-associated-with-inserting-updating-and-deleting-vbmd"></a>1 단계:[삽입, 업데이트 및 삭제와 관련 된 이벤트를 검사](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md) 하 여 예제를 복제 합니다.

[삽입, 업데이트 및 삭제 자습서와 관련 된 이벤트를 검사](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md) 하는 중에는 편집 가능한 GridView에서 제품의 이름과 가격을 나열 하는 페이지를 만들었습니다. 또한이 페이지에는 `DefaultMode` 속성이 `Insert`로 설정 된 DetailsView이 포함 되어 있으므로 항상 삽입 모드로 렌더링 됩니다. 이 DetailsView에서 사용자는 새 제품의 이름과 가격을 입력 한 다음 삽입을 클릭 하 여 시스템에 추가할 수 있습니다 (그림 1 참조).

[이전 예제를 ![사용자가 새 제품을 추가 하 고 기존 제품을 편집할 수 있습니다.](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image2.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image1.png)

**그림 1**: 이전 예제에서는 사용자가 새 제품을 추가 하 고 기존 제품을 편집할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image3.png)).

이 자습서의 목표는 DetailsView 및 GridView를 보강 하 여 유효성 검사 컨트롤을 제공 하는 것입니다. 특히 유효성 검사 논리는 다음과 같습니다.

- 제품을 삽입 하거나 편집할 때 이름을 제공 해야 합니다.
- 레코드를 삽입할 때 가격을 제공 해야 합니다. 레코드를 편집할 때 가격은 여전히 필요 하지만 이전 자습서에서 이미 존재 하는 GridView의 `RowUpdating` 이벤트 처리기에서 프로그래밍 방식 논리를 사용 합니다.
- 가격에 대해 입력 한 값이 유효한 통화 형식 인지 확인 합니다.

이전 예제를 확대 하 여 유효성 검사를 포함 하는 것을 살펴보기 전에 먼저 `DataModificationEvents.aspx` 페이지의 예제를이 자습서의 페이지 (`UIValidation.aspx`)로 복제 해야 합니다. 이를 수행 하려면 `DataModificationEvents.aspx` 페이지의 선언적 태그와 해당 소스 코드를 모두 복사 해야 합니다. 먼저 다음 단계를 수행 하 여 선언적 태그를 복사 합니다.

1. Visual Studio에서 `DataModificationEvents.aspx` 페이지 열기
2. 페이지의 선언 태그 (페이지 맨 아래에 있는 원본 단추 클릭)로 이동 합니다.
3. 그림 2에 나와 있는 것 처럼 `<asp:Content>` 및 `</asp:Content>` 태그 (3 ~ 44 줄) 내에서 텍스트를 복사 합니다.

[&lt;asp: Content&gt; 컨트롤 내에서 텍스트 ![복사 합니다.](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image5.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image4.png)

**그림 2**: `<asp:Content>` 컨트롤 내에서 텍스트 복사 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image6.png))

1. `UIValidation.aspx` 페이지 열기
2. 페이지의 선언적 태그로 이동
3. `<asp:Content>` 컨트롤 내에 텍스트를 붙여넣습니다.

소스 코드를 복사 하려면 `DataModificationEvents.aspx.vb` 페이지를 열고 `EditInsertDelete_DataModificationEvents` 클래스 *내 에서만* 텍스트를 복사 합니다. 3 개의 이벤트 처리기 (`Page_Load`, `GridView1_RowUpdating`및 `ObjectDataSource1_Inserting`)를 복사 하지만 클래스 선언을 복사 **하지** 않습니다. `UIValidation.aspx.vb`의 `EditInsertDelete_UIValidation` 클래스 *내* 에 복사 된 텍스트를 붙여넣습니다.

`DataModificationEvents.aspx`의 콘텐츠 및 코드를 `UIValidation.aspx`으로 이동한 후 잠시 브라우저에서 진행률을 테스트 합니다. 이러한 두 페이지에서 동일한 출력이 표시 되 고 동일한 기능이 제공 됩니다 (작업 중인 `DataModificationEvents.aspx`의 스크린샷는 그림 1을 참조 하세요).

## <a name="step-2-converting-the-boundfields-into-templatefields"></a>2 단계: BoundFields를 템플릿 필드로 변환

편집 및 삽입 인터페이스에 유효성 검사 컨트롤을 추가 하려면 DetailsView 및 GridView 컨트롤에서 사용 하는 BoundFields를 템플릿 필드로 변환 해야 합니다. 이를 위해서는 GridView 및 DetailsView의 스마트 태그에서 각각 열 편집 및 필드 편집 링크를 클릭 합니다. 여기에서 각 BoundFields을 선택 하 고 "이 필드를 Templatefield로 변환로 변환" 링크를 클릭 합니다.

[![각 DetailsView의 및 GridView의 BoundFields를 템플릿 필드로 변환 합니다.](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image8.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image7.png)

**그림 3**: 각 DetailsView의 BoundFields 및 GridView의 작업을 템플릿 필드로 변환 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image9.png))

필드 대화 상자를 통해 BoundField을 Templatefield로 변환로 변환 하면 동일한 읽기 전용, 편집 및 삽입 인터페이스를 BoundField 자체와 같은 Templatefield로 변환 생성 합니다. 다음 태그는 Templatefield로 변환로 변환 된 후 DetailsView의 `ProductName` 필드에 대 한 선언적 구문을 보여 줍니다.

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample1.aspx)]

이 Templatefield로 변환에는 `EditItemTemplate`및 `InsertItemTemplate``ItemTemplate`자동으로 생성 된 세 가지 템플릿이 있습니다. `ItemTemplate`은 레이블 웹 컨트롤을 사용 하 여 단일 데이터 필드 값 (`ProductName`)을 표시 하는 반면 `EditItemTemplate` 및 `InsertItemTemplate`는 데이터 필드 값을 양방향 데이터 바인딩을 사용 하 여 텍스트 상자의 `Text` 속성과 연결 하는 TextBox 웹 컨트롤의 데이터 필드 값을 표시 합니다. 이 페이지에 삽입에 대 한 DetailsView만 사용 하 고 있기 때문에 `ItemTemplate`를 제거 하 고 두 개의 템플릿 필드에서 `EditItemTemplate` 수 있습니다. 단, 그대로 두면 됩니다.

GridView는 DetailsView의 기본 제공 기능을 지원 하지 않으므로 GridView의 `ProductName` 필드를 Templatefield로 변환으로 변환 하면 `ItemTemplate` 및 `EditItemTemplate`만 생성 됩니다.

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample2.aspx)]

"이 필드를 Templatefield로 변환으로 변환"을 클릭 하면 Visual Studio에서 해당 템플릿이 변환 된 BoundField의 사용자 인터페이스를 모방 하는 Templatefield로 변환를 만들었습니다. 브라우저를 통해이 페이지를 방문 하 여이를 확인할 수 있습니다. BoundFields를 대신 사용 하는 경우에는 템플릿 필드의 모양과 동작이 환경과 동일 하다는 것을 알 수 있습니다.

> [!NOTE]
> 필요에 따라 템플릿에서 편집 인터페이스를 사용자 지정할 수 있습니다. 예를 들어 `UnitPrice` 템플릿 필드에 TextBox를 `ProductName` textbox 보다 작은 textbox로 렌더링 하는 것이 좋습니다. 이를 위해 텍스트 상자의 `Columns` 속성을 적절 한 값으로 설정 하거나 `Width` 속성을 통해 절대 너비를 제공할 수 있습니다. 다음 자습서에서는 TextBox를 대체 데이터 입력 웹 컨트롤로 바꿔서 편집 인터페이스를 완전히 사용자 지정 하는 방법을 알아봅니다.

## <a name="step-3-adding-the-validation-controls-to-the-gridviewsedititemtemplate-s"></a>3 단계: GridView의`EditItemTemplate` s에 유효성 검사 컨트롤 추가

데이터 입력 양식을 생성할 때는 사용자가 필수 필드를 입력 하 고 제공 된 모든 입력이 올바른 형식의 올바른 값입니다. 사용자의 입력이 유효한 지 확인 하기 위해 ASP.NET는 단일 입력 컨트롤의 값에 대 한 유효성을 검사 하는 데 사용 하도록 디자인 된 5 가지 기본 제공 유효성 검사 컨트롤을 제공 합니다.

- [Requiredfieldvalidator](https://msdn.microsoft.com/library/5hbw267h(VS.80).aspx) 가 값을 제공 했는지 확인 합니다.
- [Comparevalidator](https://msdn.microsoft.com/library/db330ayw(VS.80).aspx) 가 다른 웹 컨트롤 값 또는 상수 값에 대해 값의 유효성을 검사 하거나 지정 된 데이터 형식에 대 한 값의 형식이 유효한 지 확인 합니다.
- [RangeValidator](https://msdn.microsoft.com/library/f70d09xt.aspx) 는 값의 범위 내에 값이 있는지 확인 합니다.
- [RegularExpressionValidator](https://msdn.microsoft.com/library/eahwtc9e.aspx) [정규식](http://en.wikipedia.org/wiki/Regular_expression) 에 대해 값의 유효성을 검사 합니다.
- [CustomValidator](https://msdn.microsoft.com/library/9eee01cx(VS.80).aspx) 사용자 정의 메서드를 사용 하 여 값의 유효성을 검사 합니다.

이러한 다섯 가지 컨트롤에 대 한 자세한 내용은 [ASP.NET 빠른 시작 자습서](https://asp.net/QuickStart/aspnet/)의 [유효성 검사 컨트롤 섹션](https://quickstarts.asp.net/quickstartv20/aspnet/doc/ctrlref/validation/default.aspx) 을 참조 하세요.

이 자습서에서는 detailsview의 `UnitPrice` Templatefield로 변환에서 DetailsView 및 GridView의 `ProductName` 템플릿 필드와 RequiredFieldValidator 모두에 RequiredFieldValidator를 사용 해야 합니다. 또한 입력 된 가격의 값이 0 보다 크거나 같고 유효한 통화 형식으로 표시 되도록 하는 두 컨트롤의 `UnitPrice` 템플릿 필드에 CompareValidator를 추가 해야 합니다.

> [!NOTE]
> ASP.NET 1.x는 이와 동일한 5 가지 유효성 검사 컨트롤을가지고 있지만 ASP.NET 2.0에는 여러 가지 향상 된 기능이 추가 되었으며, Internet Explorer 이외의 브라우저에서 클라이언트 쪽 스크립트를 지원 하 고, 페이지의 유효성 검사 컨트롤을로 분할할 수 있습니다. 유효성 검사 그룹. 2\.0의 새 유효성 검사 제어 기능에 대 한 자세한 내용은 개로 나누어서 the [Validation Controls in ASP.NET 2.0](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)를 참조 하세요.

GridView의 템플릿 필드에 `EditItemTemplate` s에 필요한 유효성 검사 컨트롤을 추가 하는 것부터 시작 해 보겠습니다. 이 작업을 수행 하려면 GridView의 스마트 태그에서 템플릿 편집 링크를 클릭 하 여 템플릿 편집 인터페이스를 표시 합니다. 여기에서 드롭다운 목록에서 편집할 템플릿을 선택할 수 있습니다. 편집 인터페이스를 확대 하려고 하므로 `ProductName` 및 `UnitPrice`의 `EditItemTemplate` s에 유효성 검사 컨트롤을 추가 해야 합니다.

[![ProductName 및 UnitPrice의 EditItemTemplates을 확장 해야 합니다.](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image11.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image10.png)

**그림 4**: `ProductName` 및 `UnitPrice`의 `EditItemTemplate`을 확장 해야 합니다 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image12.png)).

`ProductName` `EditItemTemplate`에서 도구 상자에서 텍스트 상자 뒤에 배치 하 여 RequiredFieldValidator를 도구 상자에서 템플릿 편집 인터페이스로 끌어 추가 합니다.

[EditItemTemplate에 RequiredFieldValidator를 추가 ![](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image14.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image13.png)

**그림 5**: `ProductName` `EditItemTemplate`에 RequiredFieldValidator 추가 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image15.png))

모든 유효성 검사 컨트롤은 단일 ASP.NET 웹 컨트롤의 입력에 대 한 유효성을 검사 하는 방식으로 작동 합니다. 따라서 방금 추가한 RequiredFieldValidator가 `EditItemTemplate`텍스트 상자에 대해 유효성을 검사 해야 함을 나타내야 합니다. 유효성 검사 컨트롤의 [ControlToValidate 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.controltovalidate(VS.80).aspx) 을 적절 한 웹 컨트롤의 `ID` 설정 하 여이를 수행 합니다. 텍스트 상자에는 현재 `TextBox1`의 비 descript `ID` 있지만 더 적절 한 항목으로 변경해 보겠습니다. 템플릿에서 텍스트 상자를 클릭 한 다음 속성 창에서 `ID` `TextBox1`에서 `EditProductName`로 변경 합니다.

[텍스트 상자 ID를 EditProductName으로 변경 ![](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image17.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image16.png)

**그림 6**: 텍스트 상자의 `ID`를 `EditProductName`으로 변경 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image18.png))

그런 다음 RequiredFieldValidator의 `ControlToValidate` 속성을 `EditProductName`로 설정 합니다. 마지막으로 [ErrorMessage 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.errormessage(VS.80).aspx) 을 "제품 이름을 제공 해야 합니다."로 설정 하 고 [Text 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.text(VS.80).aspx) 을 "\*"로 설정 합니다. 제공 되는 경우 `Text` 속성 값은 유효성 검사에 실패 하는 경우 유효성 검사 컨트롤에 표시 되는 텍스트입니다. 필요한 `ErrorMessage` 속성 값은 ValidationSummary 컨트롤에서 사용 됩니다. `Text` 속성 값을 생략 하면 `ErrorMessage` 속성 값도 잘못 된 입력에 대 한 유효성 검사 컨트롤에 표시 되는 텍스트입니다.

RequiredFieldValidator의 이러한 세 가지 속성을 설정한 후 화면은 그림 7과 유사 하 게 표시 됩니다.

[RequiredFieldValidator의 ControlToValidate, ErrorMessage 및 Text 속성을 설정 ![](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image20.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image19.png)

**그림 7**: RequiredFieldValidator의 `ControlToValidate`, `ErrorMessage`및 `Text` 속성 설정 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image21.png))

RequiredFieldValidator가 `ProductName` `EditItemTemplate`에 추가 되 면 `UnitPrice` `EditItemTemplate`에 필요한 유효성 검사를 추가 하는 것만 남았습니다. 이 페이지에서 레코드를 편집할 때 `UnitPrice` 선택 사항 이므로 RequiredFieldValidator를 추가할 필요가 없습니다. 그러나 입력 유효성 검사기를 추가 하 여 제공 되는 경우 `UnitPrice`의 형식이 적절 하 게 지정 되 고가 0 보다 크거나 같으면 CompareValidator를 추가 해야 합니다.

`UnitPrice` `EditItemTemplate`에 CompareValidator를 추가 하기 전에 먼저 TextBox 웹 컨트롤의 ID를 `TextBox2`에서 `EditUnitPrice`로 변경 하겠습니다. 이렇게 변경한 후에는 CompareValidator를 추가 하 고, 해당 `ControlToValidate` 속성을 `EditUnitPrice`로 설정 하 고, `ErrorMessage` 속성을 "0 보다 크거나 같고 통화 기호를 포함할 수 없습니다."와 `Text` 속성을 "\*"로 설정 합니다.

`UnitPrice` 값이 0 보다 크거나 같아야 함을 나타내려면 CompareValidator의 [Operator 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.operator(VS.80).aspx) 을 `GreaterThanEqual`로, 해당 값을 "0 ["으로 설정](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.valuetocompare(VS.80).aspx) 하 고 해당 [Type 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basecomparevalidator.type.aspx) 을 `Currency`로 설정 합니다. 다음 선언 구문은 이러한 변경을 수행한 후 `UnitPrice` Templatefield로 변환의 `EditItemTemplate`를 보여 줍니다.

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample3.aspx)]

이러한 변경을 수행한 후 브라우저에서 페이지를 엽니다. 제품을 편집할 때 이름을 생략 하거나 잘못 된 가격 값을 입력 하려고 하면 텍스트 상자 옆에 별표가 표시 됩니다. 그림 8에 나와 있는 것 처럼 $19.95과 같은 통화 기호를 포함 하는 가격 값은 잘못 된 것으로 간주 됩니다. CompareValidator의 `Currency` `Type`는 숫자 구분 기호 (예: 문화권 설정에 따라 쉼표 또는 마침표)와 선행 더하기 또는 빼기 기호를 허용 하지만 통화 기호는 허용 *하지* 않습니다. 이 동작은 편집 인터페이스에서 현재 통화 형식을 사용 하 여 `UnitPrice`를 렌더링 하므로 플렉스 사용자를 지정할 수 있습니다.

> [!NOTE]
> *삽입, 업데이트 및 삭제 자습서와 관련 된 이벤트* 에서 BoundField의 `DataFormatString` 속성을 통화로 지정 하기 위해 `{0:c}`로 설정 합니다. 또한 `ApplyFormatInEditMode` 속성을 true로 설정 하 여 GridView의 편집 인터페이스에서 `UnitPrice`를 통화로 서식 지정 합니다. BoundField을 Templatefield로 변환로 변환 하는 경우 Visual Studio는 `<%# Bind("UnitPrice", "{0:c}") %>`데이터 바인딩 구문을 사용 하 여 이러한 설정을 지정 하 고 TextBox의 `Text` 속성을 통화로 지정 합니다.

[입력이 잘못 된 텍스트 상자 옆에 별표가 표시 ![](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image23.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image22.png)

**그림 8**: 잘못 된 입력이 있는 텍스트 상자 옆에 별표 표시 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image24.png))

유효성 검사는 그대로 작동 하지만, 사용자는 레코드를 편집할 때 통화 기호를 수동으로 제거 해야 합니다 .이는 허용 되지 않습니다. 이를 해결 하기 위해 다음과 같은 세 가지 옵션이 있습니다.

1. `UnitPrice` 값의 형식이 통화로 지정 되지 않도록 `EditItemTemplate`를 구성 합니다.
2. 사용자가 CompareValidator를 제거 하 고 올바른 형식의 통화 값을 제대로 확인 하는 RegularExpressionValidator로 바꿔서 통화 기호를 입력할 수 있습니다. 여기에서 발생 하는 문제는 통화 값의 유효성을 검사 하는 정규식이 매우 간단 하지 않으며, 문화권 설정을 통합 하려는 경우 코드를 작성 해야 한다는 것입니다.
3. 유효성 검사 컨트롤을 완전히 제거 하 고 GridView의 `RowUpdating` 이벤트 처리기에서 서버 쪽 유효성 검사 논리를 사용 합니다.

이 연습에 대 한 옵션 #1 살펴보겠습니다. 현재 `UnitPrice`은 `EditItemTemplate`의 텍스트 상자에 대 한 데이터 바인딩 식으로 인해 통화 형식으로 지정 됩니다. `<%# Bind("UnitPrice", "{0:c}") %>`. Bind 문을 `Bind("UnitPrice", "{0:n2}")`로 변경 합니다. 그러면 결과의 형식이 전체 자릿수와 같은 숫자로 지정 됩니다. 선언적 구문을 통해 직접 수행 하거나 `UnitPrice` Templatefield로 변환의 `EditItemTemplate` `EditUnitPrice` 텍스트 상자에서 데이터 바인딩 편집 링크를 클릭 하 여이 작업을 수행할 수 있습니다 (그림 9 및 10 참조).

[입력란의 데이터 바인딩 편집 링크를 클릭 ![](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image26.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image25.png)

**그림 9**: 입력란의 데이터 바인딩 편집 링크 클릭 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image27.png))

[Bind 문에 서식 지정자를 지정 ![](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image29.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image28.png)

**그림 10**: `Bind` 문에 서식 지정자 지정 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image30.png))

이와 같이 변경 하면 편집 인터페이스에서 형식이 지정 된 가격은 쉼표를 그룹 구분 기호로 포함 하 고 마침표를 소수 구분 기호로 포함 하지만 통화 기호는 그대로 둡니다.

> [!NOTE]
> `UnitPrice` `EditItemTemplate`는 RequiredFieldValidator를 포함 하지 않으므로 다시 게시를 뒤따르게 업데이트 논리를 시작할 수 있습니다. 그러나 *삽입, 업데이트 및 삭제 자습서와 관련 된 이벤트 검사* 에서 복사 된 `RowUpdating` 이벤트 처리기에는 `UnitPrice` 제공 되도록 하는 프로그래밍 검사가 포함 되어 있습니다. 이 논리를 그대로 제거 하거나 그대로 유지 하거나 `UnitPrice` `EditItemTemplate`에 RequiredFieldValidator를 추가 합니다.

## <a name="step-4-summarizing-data-entry-problems"></a>4 단계: 데이터 입력 문제 요약

5 개의 유효성 검사 컨트롤 외에도 ASP.NET에는 잘못 된 데이터를 검색 한 유효성 검사 컨트롤의 `ErrorMessage`을 표시 하는 [ValidationSummary 컨트롤이](https://msdn.microsoft.com/library/f9h59855(VS.80).aspx)포함 되어 있습니다. 이 요약 데이터는 웹 페이지 또는 모달 클라이언트 쪽 messagebox에서 텍스트로 표시 될 수 있습니다. 유효성 검사 문제를 요약 하는 클라이언트 쪽 messagebox를 포함 하도록이 자습서를 개선 하겠습니다.

이를 수행 하려면 도구 상자에서 ValidationSummary 컨트롤을 디자이너로 끌어 옵니다. 유효성 검사 컨트롤의 위치는 단지 messagebox로 요약을 표시 하도록 구성 하기 때문에 중요 하지 않습니다. 컨트롤을 추가한 후 [Showsummary 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showsummary(VS.80).aspx) 을 `False`로 설정 하 고 [showsummary 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showmessagebox(VS.80).aspx) 을 `True`로 설정 합니다. 또한 유효성 검사 오류는 클라이언트 쪽 messagebox에 요약 됩니다.

[유효성 검사 오류가 클라이언트 쪽 Messagebox에 요약 ![](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image32.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image31.png)

**그림 11**: 유효성 검사 오류가 클라이언트 쪽 Messagebox에 요약 되어 있습니다 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image33.png)).

## <a name="step-5-adding-the-validation-controls-to-the-detailsviewsinsertitemtemplate"></a>5 단계: DetailsView의`InsertItemTemplate`에 유효성 검사 컨트롤 추가

이 자습서에 대해 남아 있는 모든 것은 DetailsView의 삽입 인터페이스에 유효성 검사 컨트롤을 추가 하는 것입니다. 유효성 검사 컨트롤을 DetailsView의 템플릿에 추가 하는 프로세스는 3 단계에서 검사 한 것과 동일 합니다. 따라서이 단계에서는 작업을 간단히 설명 합니다. GridView의 `EditItemTemplate` s를 사용 하는 것 처럼 `ID` 텍스트 상자의 이름을 nondescript `TextBox1`에서 바꾸고 `InsertProductName` 및 `InsertUnitPrice`으로 `TextBox2` 하는 것이 좋습니다.

`ProductName` `InsertItemTemplate`에 RequiredFieldValidator를 추가 합니다. 템플릿의 텍스트 상자 `ID`에 대 한 `ControlToValidate` `Text` 속성을 "\*"로 설정 하 고 해당 `ErrorMessage` 속성을 "제품 이름을 제공 해야 합니다."로 설정 합니다.

새 레코드를 추가할 때이 페이지에 `UnitPrice` 필요 하므로 `UnitPrice` `InsertItemTemplate`에 RequiredFieldValidator를 추가 하 고 `ControlToValidate`, `Text`및 `ErrorMessage` 속성을 적절 하 게 설정 합니다. 마지막으로, GridView의 `ErrorMessage`에서 `Type`의 CompareValidator와 같이 `ControlToValidate`, `Text`, `Operator`, `ValueToCompare`, `UnitPrice`및 `EditItemTemplate`속성을 구성 하 여 `UnitPrice` `InsertItemTemplate`에 CompareValidator를 추가 합니다.

이러한 유효성 검사 컨트롤을 추가한 후에는 이름이 제공 되지 않았거나 가격이 음수 이거나 형식이 잘못 된 경우 시스템에 새 제품을 추가할 수 없습니다.

[![유효성 검사 논리가 DetailsView의 삽입 인터페이스에 추가 되었습니다.](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image35.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image34.png)

**그림 12**: 유효성 검사 논리가 DetailsView의 삽입 인터페이스에 추가 되었습니다 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image36.png)).

## <a name="step-6-partitioning-the-validation-controls-into-validation-groups"></a>6 단계: 유효성 검사 컨트롤을 유효성 검사 그룹으로 분할

이 페이지는 두 가지 논리적으로 서로 다른 유효성 검사 컨트롤 집합, 즉 GridView의 편집 인터페이스에 해당 하는 컨트롤과 DetailsView의 삽입 인터페이스에 해당 하는 컨트롤을 구성 합니다. 기본적으로 포스트백이 발생 하면 페이지의 *모든* 유효성 검사 컨트롤이 선택 됩니다. 그러나 레코드를 편집할 때 DetailsView의 삽입 인터페이스 유효성 검사 컨트롤의 유효성을 검사 하지 않으려고 합니다. 그림 13은 사용자가 완전 한 값으로 제품을 편집 하는 경우 현재 딜레마를 보여 줍니다. 삽입 인터페이스의 이름 및 가격 값이 비어 있기 때문에 업데이트를 클릭 하면 유효성 검사 오류가 발생 합니다.

[제품을 업데이트 ![삽입 하는 인터페이스의 유효성 검사 컨트롤이 발생 합니다.](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image38.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image37.png)

**그림 13**: 제품을 업데이트 하면 삽입 인터페이스의 유효성 검사 컨트롤이 발생 합니다 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image39.png)).

ASP.NET 2.0의 유효성 검사 컨트롤은 `ValidationGroup` 속성을 통해 유효성 검사 그룹으로 분할할 수 있습니다. 그룹의 유효성 검사 컨트롤 집합을 연결 하려면 `ValidationGroup` 속성을 동일한 값으로 설정 하면 됩니다. 이 자습서의 경우 GridView의 템플릿 필드에서 유효성 검사 컨트롤의 `ValidationGroup` 속성을 `EditValidationControls`로 설정 하 고 DetailsView의 템플릿 필드의 `ValidationGroup` 속성을 `InsertValidationControls`로 설정 합니다. 이러한 변경은 선언적 태그에서 직접 수행 하거나 디자이너의 편집 템플릿 인터페이스를 사용할 때 속성 창을 통해 수행할 수 있습니다.

유효성 검사 컨트롤 외에도 ASP.NET 2.0의 단추 및 단추 관련 컨트롤에는 `ValidationGroup` 속성이 포함 되어 있습니다. 유효성 검사 그룹의 유효성 검사기는 동일한 `ValidationGroup` 속성 설정을 가진 단추로 포스트백이 발생 한 경우에만 유효성 검사를 수행 합니다. 예를 들어 DetailsView의 삽입 단추가 `InsertValidationControls` 유효성 검사 그룹을 트리거하기 위해 CommandField의 `ValidationGroup` 속성을 `InsertValidationControls`으로 설정 해야 합니다 (그림 14 참조). 또한 GridView의 CommandField's 속성을 `EditValidationControls`로 설정 합니다.

[![DetailsView의 CommandField's ValidationGroup 속성을 InsertValidationControls로 설정 합니다.](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image41.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image40.png)

**그림 14**: DetailsView의 commandfield's 속성을 `InsertValidationControls`로 설정 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image42.png))

이러한 변경 후에는 DetailsView 및 GridView의 템플릿 필드와 CommandFields가 다음과 같이 표시 됩니다.

DetailsView의 템플릿 필드 및 CommandField

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample4.aspx)]

GridView의 CommandField 및 템플릿 필드

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample5.aspx)]

이 시점에서 편집 별 유효성 검사 컨트롤은 GridView의 업데이트 단추를 클릭 한 경우에만 발생 하 고, DetailsView의 삽입 단추를 클릭 한 경우에만 삽입 별 유효성 검사 컨트롤이 실행 되어 그림 13에 의해 강조 표시 된 문제를 해결 합니다. 그러나이 변경 내용으로 잘못 된 데이터를 입력할 때 ValidationSummary 컨트롤은 더 이상 표시 되지 않습니다. ValidationSummary 컨트롤에는 또한 `ValidationGroup` 속성이 포함 되어 있으며 해당 유효성 검사 그룹의 유효성 검사 컨트롤에 대 한 요약 정보만 표시 합니다. 따라서이 페이지에는 `InsertValidationControls` 유효성 검사 그룹 및 `EditValidationControls`에 대 한 유효성 검사 컨트롤이 두 개 있어야 합니다.

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample6.aspx)]

이 외에도 자습서가 완료 되었습니다.

## <a name="summary"></a>요약

BoundFields는 삽입 및 편집 인터페이스를 모두 제공할 수 있지만 인터페이스는 사용자 지정할 수 없습니다. 일반적으로 사용자가 올바른 형식으로 필요한 입력을 입력할 수 있도록 편집 및 삽입 인터페이스에 유효성 검사 컨트롤을 추가 하려고 합니다. 이를 위해 BoundFields를 템플릿 필드로 변환 하 고 유효성 검사 컨트롤을 해당 템플릿에 추가 해야 합니다. 이 자습서에서는 *삽입, 업데이트 및 삭제 자습서와 관련 된 이벤트 검사* 에서 예제를 확장 하 여 DetailsView의 삽입 인터페이스와 GridView의 편집 인터페이스에 유효성 검사 컨트롤을 추가 했습니다. 또한 ValidationSummary 컨트롤을 사용 하 여 요약 유효성 검사 정보를 표시 하는 방법 및 페이지의 유효성 검사 컨트롤을 고유한 유효성 검사 그룹으로 분할 하는 방법을 살펴보았습니다.

이 자습서에서 살펴본 것 처럼 템플릿 필드를 사용 하면 편집 및 삽입 인터페이스를 확대 하 여 유효성 검사 컨트롤을 포함할 수 있습니다. 또한 추가 입력 웹 컨트롤을 포함 하도록 템플릿 필드를 확장 하 여 텍스트 상자를 보다 적합 한 웹 컨트롤로 바꿀 수 있습니다. 다음 자습서에서는 텍스트 상자 컨트롤을 데이터 바인딩된 DropDownList 컨트롤로 바꾸는 방법에 대해 설명 합니다 .이 컨트롤은 외래 키 (예: `Products` 테이블의 `CategoryID` 또는 `SupplierID`)를 편집할 때 적합 합니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Liz Shulok 및 Zack Jones 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md)
> [다음](customizing-the-data-modification-interface-vb.md)
