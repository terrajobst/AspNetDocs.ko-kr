---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/adding-validation-controls-to-the-datalist-s-editing-interface-cs
title: DataList의 편집 인터페이스에 유효성 검사 컨트롤 추가 (C#) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 보다 간단 하 게 편집할 수 있는 사용자 int를 제공 하기 위해 DataList의 EditItemTemplate에 유효성 검사 컨트롤을 추가 하는 것이 얼마나 쉬운지 알아봅니다.
ms.author: riande
ms.date: 10/30/2006
ms.assetid: 3ecc21c5-da0e-40ab-abb4-fac1e47398ad
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/adding-validation-controls-to-the-datalist-s-editing-interface-cs
msc.type: authoredcontent
ms.openlocfilehash: e3c14b7098da832bd28f57026e81dcb7f7ba7130
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78480857"
---
# <a name="adding-validation-controls-to-the-datalists-editing-interface-c"></a>DataList의 편집 인터페이스에 유효성 검사 컨트롤 추가(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_39_CS.exe) 또는 [PDF 다운로드](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/datatutorial39cs1.pdf)

> 이 자습서에서는 보다 간단 하 게 편집할 수 있는 사용자 인터페이스를 제공 하기 위해 DataList의 EditItemTemplate에 유효성 검사 컨트롤을 추가 하는 것이 얼마나 쉬운지 알아봅니다.

## <a name="introduction"></a>소개

지금까지 DataList 편집 자습서에서는 누락 된 제품 이름 또는 음수 가격과 같은 잘못 된 사용자 입력으로 인해 예외가 발생 하더라도 DataLists 편집 인터페이스에는 자동 관리 사용자 입력 유효성 검사가 포함 되지 않았습니다. [이전 자습서](handling-bll-and-dal-level-exceptions-cs.md) 에서는 발생 한 예외에 대 한 정보를 catch 하 고 정상적으로 표시 하기 위해 DataList s `UpdateCommand` 이벤트 처리기에 예외 처리 코드를 추가 하는 방법을 살펴보았습니다. 그러나 편집 인터페이스에는 사용자가 처음에 이러한 데이터를 입력 하지 못하도록 하는 유효성 검사 컨트롤이 포함 됩니다.

이 자습서에서는 보다 간단 하 게 편집할 수 있는 사용자 인터페이스를 제공 하기 위해 DataList s `EditItemTemplate`에 유효성 검사 컨트롤을 추가 하는 것이 얼마나 쉬운지 알아봅니다. 특히이 자습서에서는 이전 자습서에서 만든 예제를 사용 하 고 편집 인터페이스를 보강 하 여 적절 한 유효성 검사를 포함 합니다.

## <a name="step-1-replicating-the-example-fromhandling-bll--and-dal-level-exceptions"></a>1 단계:[BLL 및 DAL 수준의 예외 처리](handling-bll-and-dal-level-exceptions-cs.md) 에서 예제 복제

[BLL 및 DAL 수준 예외 처리](handling-bll-and-dal-level-exceptions-cs.md) 자습서에서 2 열 편집 가능 DataList에서 제품의 이름과 가격을 나열 하는 페이지를 만들었습니다. 이 자습서의 목표는 유효성 검사 컨트롤을 포함 하도록 DataList s 편집 인터페이스를 확대 하는 것입니다. 특히 유효성 검사 논리는 다음과 같습니다.

- 제품 이름을 제공 해야 합니다.
- 가격에 대해 입력 한 값이 유효한 통화 형식 인지 확인 합니다.
- 음수 `UnitPrice` 값이 잘못 되었기 때문에 가격에 대해 입력 한 값이 0 보다 크거나 같은지 확인 합니다.

이전 예제를 확대 하 여 유효성 검사를 포함 하는 것을 확인 하기 전에 먼저 `EditDeleteDataList` 폴더의 `ErrorHandling.aspx` 페이지에서이 자습서의 페이지 (`UIValidation.aspx`)로 예제를 복제 해야 합니다. 이를 위해 `ErrorHandling.aspx` 페이지의 선언적 태그와 해당 소스 코드를 모두 복사 해야 합니다. 먼저 다음 단계를 수행 하 여 선언적 태그를 복사 합니다.

1. Visual Studio에서 `ErrorHandling.aspx` 페이지 열기
2. 페이지의 선언 태그 (페이지 맨 아래에 있는 원본 단추 클릭)로 이동 합니다.
3. 그림 1에 나와 있는 것 처럼 `<asp:Content>` 및 `</asp:Content>` 태그 (3 ~ 32 줄) 내에서 텍스트를 복사 합니다.

[&lt;asp: Content&gt; 컨트롤 내에서 텍스트 ![복사 합니다.](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image2.png)](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image1.png)

**그림 1**: `<asp:Content>` 컨트롤 내에서 텍스트 복사 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image3.png))

1. `UIValidation.aspx` 페이지 열기
2. 페이지의 선언적 태그로 이동
3. `<asp:Content>` 컨트롤 내에 텍스트를 붙여넣습니다.

소스 코드를 복사 하려면 `ErrorHandling.aspx.vb` 페이지를 열고 `EditDeleteDataList_ErrorHandling` 클래스 *내 에서만* 텍스트를 복사 합니다. `DisplayExceptionDetails` 메서드와 함께 세 개의 이벤트 처리기 (`Products_EditCommand`, `Products_CancelCommand`및 `Products_UpdateCommand`)를 복사 하지만 클래스 선언이 나 `using` 문은 복사 **하지** 않습니다. `UIValidation.aspx.vb`의 `EditDeleteDataList_UIValidation` 클래스 *내* 에 복사 된 텍스트를 붙여넣습니다.

`ErrorHandling.aspx`에서 `UIValidation.aspx`콘텐츠 및 코드를 이동한 후 잠시 브라우저에서 페이지를 테스트 합니다. 이러한 두 페이지에서 동일한 출력이 표시 되 고 동일한 기능이 경험 됩니다 (그림 2 참조).

[UIValidation .aspx 페이지 ![ErrorHandling .aspx의 기능을 모방 합니다.](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image5.png)](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image4.png)

**그림 2**: `UIValidation.aspx` 페이지에서 `ErrorHandling.aspx`의 기능 모방 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image6.png))

## <a name="step-2-adding-the-validation-controls-to-the-datalist-s-edititemtemplate"></a>2 단계: DataList s EditItemTemplate에 유효성 검사 컨트롤 추가

데이터 입력 양식을 생성할 때는 사용자가 모든 필수 필드를 입력 하 고 제공 된 모든 입력이 올바른 형식의 올바른 값입니다. 사용자 입력이 유효한 지 확인 하기 위해 ASP.NET는 단일 입력 웹 컨트롤의 값에 대 한 유효성을 검사 하도록 디자인 된 5 가지 기본 제공 유효성 검사 컨트롤을 제공 합니다.

- [Requiredfieldvalidator](https://msdn.microsoft.com/library/5hbw267h(VS.80).aspx) 가 값을 제공 했는지 확인 합니다.
- [Comparevalidator](https://msdn.microsoft.com/library/db330ayw(VS.80).aspx) 가 다른 웹 컨트롤 값 또는 상수 값에 대해 값의 유효성을 검사 하거나 지정 된 데이터 형식에 대 한 값의 형식이 유효한 지 확인 합니다.
- [RangeValidator](https://msdn.microsoft.com/library/f70d09xt.aspx) 는 값의 범위 내에 값이 있는지 확인 합니다.
- [RegularExpressionValidator](https://msdn.microsoft.com/library/eahwtc9e.aspx) [정규식](http://en.wikipedia.org/wiki/Regular_expression) 에 대해 값의 유효성을 검사 합니다.
- [CustomValidator](https://msdn.microsoft.com/library/9eee01cx(VS.80).aspx) 사용자 정의 메서드를 사용 하 여 값의 유효성을 검사 합니다.

이러한 다섯 가지 컨트롤에 대 한 자세한 내용은 [인터페이스 편집 및 삽입 자습서의 유효성 검사 컨트롤 추가](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-cs.md) 또는 [ASP.NET 빠른 시작 자습서](https://quickstarts.asp.net)의 [유효성 검사 컨트롤 섹션](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/validation/default.aspx) 을 참조 하세요.

이 자습서에서는 제품 이름에 대 한 값이 제공 되었는지 확인 하는 데 RequiredFieldValidator를 사용 해야 하며, 입력 된 가격이 0 보다 크거나 같고 유효한 통화 형식으로 표시 되도록 하려면 CompareValidator를 사용 해야 합니다.

> [!NOTE]
> ASP.NET 1.x는 이와 동일한 5 가지 유효성 검사 컨트롤을 포함 하 고 있지만, ASP.NET 2.0에는 여러 가지 향상 된 기능이 추가 되었으며, Internet Explorer 외에도 브라우저에 대 한 클라이언트 쪽 스크립트 지원과 페이지의 유효성 검사 컨트롤을 분할 하는 기능이 추가 되었습니다. 유효성 검사 그룹. 2\.0의 새 유효성 검사 제어 기능에 대 한 자세한 내용은 개로 나누어서 the [Validation Controls in ASP.NET 2.0](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)를 참조 하세요.

필요한 유효성 검사 컨트롤을 DataList s `EditItemTemplate`에 추가 하 여를 시작 합니다. 이 작업은 DataList의 스마트 태그에서 템플릿 편집 링크를 클릭 하거나 선언적 구문을 통해 디자이너를 통해 수행할 수 있습니다. 디자인 뷰에서 템플릿 편집 옵션을 사용 하 여 프로세스를 단계별로 실행 합니다. DataList s `EditItemTemplate`편집 하도록 선택한 후 도구 상자에서 템플릿 편집 인터페이스로 끌어와 RequiredFieldValidator를 추가 하 여 `ProductName` 텍스트 상자 뒤에 배치 합니다.

[EditItemTemplate 다음에 RequiredFieldValidator를 추가 ![ProductName 텍스트 상자](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image8.png)](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image7.png)

**그림 3**: `ProductName` TextBox `EditItemTemplate After`에 RequiredFieldValidator 추가 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image9.png))

모든 유효성 검사 컨트롤은 단일 ASP.NET 웹 컨트롤의 입력에 대 한 유효성을 검사 하는 방식으로 작동 합니다. 따라서 방금 추가한 RequiredFieldValidator가 `ProductName` 텍스트 상자에 대해 유효성을 검사 하도록 지정 해야 합니다. 이 작업은 유효성 검사 컨트롤의 [`ControlToValidate` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.controltovalidate(VS.80).aspx) 을 적절 한 웹 컨트롤의 `ID` (이 인스턴스에서`ProductName`)로 설정 하 여 수행 합니다. 그런 다음 [`ErrorMessage` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.errormessage(VS.80).aspx) 을로 설정 하 고 \*에 제품 이름과 [`Text` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.text(VS.80).aspx) 을 제공 해야 합니다. 제공 되는 경우 `Text` 속성 값은 유효성 검사에 실패 하는 경우 유효성 검사 컨트롤에 표시 되는 텍스트입니다. 필요한 `ErrorMessage` 속성 값은 ValidationSummary 컨트롤에서 사용 됩니다. `Text` 속성 값이 생략 되 면 유효성 검사 컨트롤에서 잘못 된 입력에 대해 `ErrorMessage` 속성 값이 표시 됩니다.

RequiredFieldValidator의 이러한 세 가지 속성을 설정한 후 화면은 그림 4와 유사 하 게 표시 됩니다.

[RequiredFieldValidator s ControlToValidate, ErrorMessage 및 Text 속성을 설정 ![](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image11.png)](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image10.png)

**그림 4**: RequiredFieldValidator s `ControlToValidate`, `ErrorMessage`및 `Text` 속성 설정 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image12.png))

RequiredFieldValidator를 `EditItemTemplate`에 추가 하면 제품 가격 텍스트 상자에 필요한 유효성 검사를 추가 하는 것만 남았습니다. 레코드를 편집할 때 `UnitPrice`은 선택 사항이 기 때문에 RequiredFieldValidator를 추가할 필요가 없습니다. 그러나 입력 유효성 검사기를 추가 하 여 제공 되는 경우 `UnitPrice`의 형식이 적절 하 게 지정 되 고가 0 보다 크거나 같으면 CompareValidator를 추가 해야 합니다.

`EditItemTemplate`에 CompareValidator를 추가 하 고 `ControlToValidate` 속성을 `UnitPrice`로 설정 합니다. 해당 `ErrorMessage` 속성은 0 보다 크거나 같고 통화 기호 및 `Text` 속성을 \*에 포함할 수 없습니다. `UnitPrice` 값이 0 보다 크거나 같아야 함을 나타내려면 CompareValidator s [`Operator` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.operator(VS.80).aspx) 을 `GreaterThanEqual`, [`ValueToCompare` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.valuetocompare(VS.80).aspx) 을 0으로, 해당 [`Type` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basecomparevalidator.type.aspx) 을 `Currency`로 설정 합니다.

이러한 두 유효성 검사 컨트롤을 추가한 후에는 DataList s `EditItemTemplate` s 선언 구문이 다음과 같이 표시 됩니다.

[!code-aspx[Main](adding-validation-controls-to-the-datalist-s-editing-interface-cs/samples/sample1.aspx)]

이러한 변경을 수행한 후 브라우저에서 페이지를 엽니다. 제품을 편집할 때 이름을 생략 하거나 잘못 된 가격 값을 입력 하려고 하면 텍스트 상자 옆에 별표가 표시 됩니다. 그림 5와 같이 $19.95와 같은 통화 기호를 포함 하는 가격 값은 잘못 된 것으로 간주 됩니다. CompareValidator s `Currency` `Type`는 숫자 구분 기호 (예: 문화권 설정에 따라 쉼표 또는 마침표)와 선행 더하기 또는 빼기 기호를 허용 하지만 통화 기호는 허용 *하지* 않습니다. 이 동작은 편집 인터페이스에서 현재 통화 형식을 사용 하 여 `UnitPrice`를 렌더링 하므로 플렉스 사용자를 지정할 수 있습니다.

[입력이 잘못 된 텍스트 상자 옆에 별표가 표시 ![](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image14.png)](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image13.png)

**그림 5**: 잘못 된 입력이 있는 입력란 옆에 별표 표시 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image15.png))

유효성 검사는 그대로 작동 하지만, 사용자는 레코드를 편집할 때 통화 기호를 수동으로 제거 해야 합니다 .이는 허용 되지 않습니다. 또한 편집 인터페이스에 잘못 된 입력이 있으면 클릭 하면 다시 게시를 호출 하 게 됩니다. 사용자 입력의 유효성에 관계 없이 취소 단추는 DataList를 사전 편집 상태로 반환 하는 것이 가장 좋습니다. 또한 브라우저에서 JavaScript를 지원 하지 않거나 지원을 사용 하지 않도록 설정 하는 사용자가 유효성 검사 컨트롤 클라이언트 쪽 논리를 건너뛸 수 있으므로, DataList s `UpdateCommand` 이벤트 처리기에서 제품 정보를 업데이트 하기 전에 페이지의 데이터가 유효한 지 확인 해야 합니다.

## <a name="removing-the-currency-symbol-from-the-edititemtemplate-s-unitprice-textbox"></a>EditItemTemplate s UnitPrice 텍스트 상자에서 통화 기호 제거

CompareValidator s `Currency``Type`사용 하는 경우 유효성을 검사 하는 입력에는 통화 기호가 포함 되지 않아야 합니다. 이러한 기호가 있으면 CompareValidator가 입력을 잘못 된 것으로 표시 합니다. 그러나 편집 인터페이스는 현재 `UnitPrice` 텍스트 상자에 통화 기호를 포함 합니다. 즉, 사용자는 변경 내용을 저장 하기 전에 명시적으로 통화 기호를 제거 해야 합니다. 이를 해결 하려면 다음 세 가지 옵션을 사용할 수 있습니다.

1. `UnitPrice` TextBox 값의 형식이 통화로 지정 되지 않도록 `EditItemTemplate`를 구성 합니다.
2. 사용자가 CompareValidator를 제거 하 고 올바른 형식의 통화 값을 확인 하는 RegularExpressionValidator로 바꿔서 통화 기호를 입력할 수 있습니다. 여기에서 질문은 통화 값의 유효성을 검사 하는 정규식이 CompareValidator 만큼 간단 하지 않으며 문화권 설정을 통합 하려는 경우 코드를 작성 해야 한다는 것입니다.
3. 유효성 검사 컨트롤을 완전히 제거 하 고 GridView s `RowUpdating` 이벤트 처리기에서 사용자 지정 서버 쪽 유효성 검사 논리를 사용 합니다.

이 자습서에 대해 s 옵션 1로 이동 하겠습니다. 현재 `UnitPrice`은 `EditItemTemplate`의 텍스트 상자에 대 한 데이터 바인딩 식으로 인해 통화 값으로 형식이 지정 됩니다. `<%# Eval("UnitPrice", "{0:c}") %>`. `Eval` 문을 `Eval("UnitPrice", "{0:n2}")`로 변경 합니다. 그러면 결과의 형식이 전체 자릿수와 같은 숫자로 지정 됩니다. 선언적 구문을 통해 직접 수행 하거나 DataList s `EditItemTemplate`의 `UnitPrice` 텍스트 상자에서 데이터 바인딩 편집 링크를 클릭 하 여이 작업을 수행할 수 있습니다.

이와 같이 변경 하면 편집 인터페이스에서 형식이 지정 된 가격은 쉼표를 그룹 구분 기호로 포함 하 고 마침표를 소수 구분 기호로 포함 하지만 통화 기호는 그대로 둡니다.

> [!NOTE]
> 편집 가능한 인터페이스에서 통화 형식을 제거 하는 경우 통화 기호를 텍스트 상자 외부의 텍스트로 저장 하는 것이 좋습니다. 이는 사용자에 게 통화 기호를 제공할 필요가 없다는 힌트 역할을 합니다.

## <a name="fixing-the-cancel-button"></a>취소 단추 수정

기본적으로 유효성 검사 웹 컨트롤은 클라이언트 쪽에서 유효성 검사를 수행 하기 위해 JavaScript를 내보냅니다. 단추, LinkButton 또는 ImageButton을 클릭 하면 포스트백이 발생 하기 전에 해당 페이지의 유효성 검사 컨트롤이 클라이언트 쪽에서 확인 됩니다. 잘못 된 데이터가 있는 경우 다시 게시가 취소 됩니다. 그러나 특정 단추에 대해 데이터의 유효성은 어떤 않으므로 수 있습니다. 이 경우 잘못 된 데이터로 인해 포스트백이 취소 되는 것은 걸림돌입니다.

취소 단추는 이러한 예입니다. 사용자가 제품 이름을 생략 하는 것과 같이 잘못 된 데이터를 입력 한 후 제품을 모두 저장 하 고 취소 단추를 클릭 하지 않기로 결정 합니다. 현재 취소 단추는 페이지의 유효성 검사 컨트롤을 트리거하여 제품 이름이 누락 된 것으로 보고 하 고 다시 게시를 방지 합니다. 사용자는 편집 프로세스를 취소 하기 위해 `ProductName` 텍스트 상자에 일부 텍스트를 입력 해야 합니다.

다행히 Button, LinkButton 및 ImageButton에는 단추를 클릭할 때 유효성 검사 논리가 시작 되어야 하는지 여부를 나타내는 [`CausesValidation` 속성이](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.causesvalidation.aspx) 있습니다 (기본값은 `True`). 취소 단추 s `CausesValidation` 속성을 `False`로 설정 합니다.

## <a name="ensuring-the-inputs-are-valid-in-the-updatecommand-event-handler"></a>UpdateCommand 이벤트 처리기에서 입력을 사용할 수 있도록 보장

유효성 검사 컨트롤에서 내보낸 클라이언트 쪽 스크립트로 인해 사용자가 잘못 된 입력을 입력 하는 경우 유효성 검사 컨트롤은 `CausesValidation` 속성이 `True` 되는 단추, LinkButton 또는 ImageButton 컨트롤에 의해 시작 된 포스트백을 취소 합니다 (기본값). 그러나 사용자가 antiquated 브라우저에서 방문 하거나 JavaScript 지원이 사용 하지 않도록 설정 된 경우 클라이언트 쪽 유효성 검사는 실행 되지 않습니다.

모든 ASP.NET 유효성 검사 컨트롤은 다시 게시 시 유효성 검사 논리를 즉시 반복 하 고 [`Page.IsValid` 속성](https://msdn.microsoft.com/library/system.web.ui.page.isvalid.aspx)을 통해 페이지의 입력에 대 한 전체 유효성을 보고 합니다. 그러나 `Page.IsValid`의 값을 기반으로 하 여 페이지 흐름이 중단 되거나 중지 되지 않습니다. 개발자는 유효한 입력 데이터를 가정 하는 코드를 계속 하기 전에 `Page.IsValid` 속성의 값이 `True` 인지 확인 해야 합니다.

사용자가 JavaScript를 사용 하지 않도록 설정 하는 경우 페이지를 방문 하 고, 제품을 편집 하 고, 가격 값을 너무 많이 입력 하 고, 업데이트 단추를 클릭 하면 클라이언트 쪽 유효성 검사가 무시 되 고 다시 게시가 뒤따르게 됩니다. 다시 게시 시 ASP.NET page s `UpdateCommand` 이벤트 처리기가 실행 되 고 `Decimal`에 대해 너무 많은 비용이 분석 되려고 할 때 예외가 발생 합니다. 예외 처리가 있으므로 이러한 예외는 정상적으로 처리 되지만 `Page.IsValid`의 값이 `True`인 경우에만 `UpdateCommand` 이벤트 처리기를 사용 하 여 처음부터 잘못 된 데이터가 지연 되지 않도록 할 수 있습니다.

`Try` 블록 바로 앞에 `UpdateCommand` 이벤트 처리기의 시작 부분에 다음 코드를 추가 합니다.

[!code-csharp[Main](adding-validation-controls-to-the-datalist-s-editing-interface-cs/samples/sample2.cs)]

이 외에도 제품은 제출 된 데이터가 유효한 경우에만 업데이트 됩니다. 대부분의 사용자는 유효성 검사 컨트롤 클라이언트 쪽 스크립트 때문에 잘못 된 데이터를 다시 게시할 수 없지만, 브라우저에서 JavaScript를 지원 하지 않거나 JavaScript 지원을 사용 하지 않도록 설정 된 사용자는 클라이언트 쪽 검사를 무시 하 고 잘못 된 데이터를 제출할 수 있습니다.

> [!NOTE]
> Astute 판독기는 GridView를 사용 하 여 데이터를 업데이트할 때 페이지의 코드 기반 클래스에서 `Page.IsValid` 속성을 명시적으로 확인할 필요가 없다는 것을 기억 합니다. 이는 GridView가 `Page.IsValid` 속성을 사용 하 여 `True`값을 반환 하는 경우에만 업데이트를 진행 하기 때문입니다.

## <a name="step-3-summarizing-data-entry-problems"></a>3 단계: 데이터 입력 문제 요약

5 개의 유효성 검사 컨트롤 외에도 ASP.NET에는 잘못 된 데이터를 검색 한 유효성 검사 컨트롤의 `ErrorMessage`을 표시 하는 [ValidationSummary 컨트롤이](https://msdn.microsoft.com/library/f9h59855(VS.80).aspx)포함 되어 있습니다. 이 요약 데이터는 웹 페이지 또는 모달 클라이언트 쪽 messagebox에서 텍스트로 표시 될 수 있습니다. 에서 유효성 검사 문제를 요약 하는 클라이언트 쪽 messagebox를 포함 하도록이 자습서를 개선할 수 있습니다.

이를 수행 하려면 도구 상자에서 ValidationSummary 컨트롤을 디자이너로 끌어 옵니다. ValidationSummary 컨트롤의 위치는 단지 messagebox로 요약을 표시 하도록 구성 하기 때문에 중요 하지 않습니다. 컨트롤을 추가한 후 [`ShowSummary` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showsummary(VS.80).aspx) 을 `False`로 설정 하 고 [`ShowMessageBox` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showmessagebox(VS.80).aspx) 을 `True`로 설정 합니다. 이 외에도 유효성 검사 오류는 클라이언트 쪽 messagebox에 요약 되어 있습니다 (그림 6 참조).

[유효성 검사 오류가 클라이언트 쪽 Messagebox에 요약 ![](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image17.png)](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image16.png)

**그림 6**: 유효성 검사 오류는 클라이언트 쪽 Messagebox에 요약 되어 있습니다 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image18.png)).

## <a name="summary"></a>요약

이 자습서에서는 유효성 검사 컨트롤을 사용 하 여 업데이트 워크플로에서 사용을 시도 하기 전에 사용자 입력이 유효한 지 미리 확인 하는 방법으로 예외 가능성을 줄이는 방법에 대해 살펴보았습니다. ASP.NET은 특정 웹 컨트롤의 입력을 검사 하 고 입력의 유효성을 다시 보고 하도록 디자인 된 5 가지 유효성 검사 웹 컨트롤을 제공 합니다. 이 자습서에서는 이러한 다섯 가지를 사용 하 여 RequiredFieldValidator와 CompareValidator를 모두 사용 하 여 제품 이름이 제공 되었으며 가격에 0 보다 크거나 같은 통화 형식이 있는지 확인 합니다.

DataList의 편집 인터페이스에 유효성 검사 컨트롤을 추가 하는 것은 도구 상자에서 `EditItemTemplate`로 끌고 몇 가지 속성을 설정 하는 것 만큼 간단 합니다. 기본적으로 유효성 검사 컨트롤은 클라이언트 쪽 유효성 검사 스크립트를 자동으로 내보냅니다. 또한 게시 시 서버 쪽 유효성 검사를 제공 하 여 `Page.IsValid` 속성에 누적 결과를 저장 합니다. 단추, LinkButton 또는 ImageButton이 클릭 될 때 클라이언트 쪽 유효성 검사를 무시 하려면 단추 s `CausesValidation` 속성을 `False`로 설정 합니다. 또한 다시 게시 시 전송 된 데이터를 사용 하 여 작업을 수행 하기 전에 `Page.IsValid` 속성이 `True`를 반환 하는지 확인 합니다.

지금까지 검토 한 모든 DataList 편집 자습서에는 제품 이름에 대 한 텍스트 상자와 가격에 대 한 편집 인터페이스가 매우 단순 합니다. 그러나 편집 인터페이스에는 Dropdownlist, 달력, 라디오 단추, 확인란 등과 같은 다양 한 웹 컨트롤이 포함 될 수 있습니다. 다음 자습서에서는 다양 한 웹 컨트롤을 사용 하는 인터페이스를 구축 하는 방법을 살펴보겠습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Dennis Patterson이, 켄은 Pespisa 및 Liz Shulok 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](handling-bll-and-dal-level-exceptions-cs.md)
> [다음](customizing-the-datalist-s-editing-interface-cs.md)
