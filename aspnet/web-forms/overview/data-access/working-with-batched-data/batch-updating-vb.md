---
uid: web-forms/overview/data-access/working-with-batched-data/batch-updating-vb
title: 일괄 업데이트 (VB) | Microsoft Docs
author: rick-anderson
description: 단일 작업에서 여러 데이터베이스 레코드를 업데이트 하는 방법에 대해 알아봅니다. 사용자 인터페이스 계층에서 각 행을 편집할 수 있는 GridView를 작성 합니다. 데이터 ...
ms.author: riande
ms.date: 06/26/2007
ms.assetid: d191a204-d7ea-458d-b81c-0b9049ecb55f
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/batch-updating-vb
msc.type: authoredcontent
ms.openlocfilehash: f0bb83b17585876dd6d28a5893a223cce15da31d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74591020"
---
# <a name="batch-updating-vb"></a>일괄 업데이트(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_64_VB.zip) 또는 [PDF 다운로드](batch-updating-vb/_static/datatutorial64vb1.pdf)

> 단일 작업에서 여러 데이터베이스 레코드를 업데이트 하는 방법에 대해 알아봅니다. 사용자 인터페이스 계층에서 각 행을 편집할 수 있는 GridView를 작성 합니다. 데이터 액세스 계층에서는 여러 업데이트 작업을 트랜잭션 내에서 래핑하여 모든 업데이트가 성공 하거나 모든 업데이트가 롤백되는 것을 확인할 수 있습니다.

## <a name="introduction"></a>소개

[이전 자습서](wrapping-database-modifications-within-a-transaction-vb.md) 에서는 데이터 액세스 계층을 확장 하 여 데이터베이스 트랜잭션에 대 한 지원을 추가 하는 방법을 살펴보았습니다. 데이터베이스 트랜잭션은 일련의 데이터 수정 문이 하나의 원자성 작업으로 처리 되도록 보장 하므로 모든 수정 작업이 실패 하거나 모두 성공 하 게 됩니다. 이 낮은 수준의 DAL 기능을 사용 하면 일괄 처리 데이터 수정 인터페이스를 만들 수 있습니다.

이 자습서에서는 각 행을 편집할 수 있는 GridView를 빌드합니다 (그림 1 참조). 각 행이 편집 인터페이스에서 렌더링 되므로 편집, 업데이트 및 취소 단추의 열이 필요 하지 않습니다. 대신, 페이지에는 클릭 하면 GridView 행을 열거 하 고 데이터베이스를 업데이트 하는 두 개의 업데이트 제품 단추가 있습니다.

[![GridView의 각 행을 편집할 수 있습니다.](batch-updating-vb/_static/image1.gif)](batch-updating-vb/_static/image1.png)

**그림 1**: GridView의 각 행을 편집할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](batch-updating-vb/_static/image2.png)).

S를 시작 하겠습니다.

> [!NOTE]
> [일괄 처리 업데이트 수행](../editing-and-deleting-data-through-the-datalist/performing-batch-updates-vb.md) 자습서에서 DataList 컨트롤을 사용 하 여 일괄 처리 편집 인터페이스를 만들었습니다. 이 자습서는에서 GridView를 사용 하 고 일괄 업데이트가 트랜잭션 범위 내에서 수행 되는의 이전 버전과 다릅니다. 이 자습서를 완료 한 후 이전 자습서로 돌아가서 이전 자습서에서 추가한 데이터베이스 트랜잭션 관련 기능을 사용 하도록 업데이트 하는 것이 좋습니다.

## <a name="examining-the-steps-for-making-all-gridview-rows-editable"></a>모든 GridView 행을 편집할 수 있도록 하는 단계 검사

[데이터 삽입, 업데이트 및 삭제](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md) 자습서의 개요에 설명 된 대로 GridView는 행 단위로 기본 데이터를 편집 하는 기본 제공 지원을 제공 합니다. 내부적으로 GridView는 [`EditIndex` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.editindex(VS.80).aspx)을 통해 편집할 수 있는 행을 메모 합니다. GridView는 데이터 원본에 바인딩될 때 각 행을 검사 하 여 행의 인덱스가 `EditIndex`의 값과 같은지 확인 합니다. 이 경우 해당 행의 필드는 편집 인터페이스를 사용 하 여 렌더링 됩니다. BoundFields의 경우 편집 인터페이스는 `Text` 속성이 BoundField s `DataField` 속성으로 지정 된 데이터 필드의 값을 할당 하는 TextBox입니다. 템플릿 필드의 경우에는 `EditItemTemplate` `ItemTemplate`대신 사용 됩니다.

편집 워크플로는 사용자가 행의 편집 단추를 클릭 하면 시작 됩니다. 이렇게 하면 포스트백이 발생 하 고, GridView s `EditIndex` 속성을 클릭 된 행 인덱스로 설정 하 고, 데이터를 표 형식으로 다시 바인딩합니다. 행 취소 단추를 클릭 하면 데이터를 표 형식으로 다시 바인딩하기 전에 `EditIndex` `-1` 값으로 설정 됩니다. GridView의 행이 0부터 인덱싱을 시작 하므로 `EditIndex`를 `-1` 설정 하면 읽기 전용 모드에서 GridView를 표시 하는 효과가 있습니다.

`EditIndex` 속성은 행당 편집에 적합 하지만 일괄 편집을 위해 디자인 되지 않았습니다. 전체 GridView를 편집 가능 하 게 만들려면 편집 인터페이스를 사용 하 여 각 행을 렌더링 해야 합니다. 이를 수행 하는 가장 쉬운 방법은 편집 가능 필드가 `ItemTemplate`에 정의 된 편집 인터페이스를 사용 하 여 Templatefield로 변환로 구현 되는 위치를 만드는 것입니다.

다음 몇 가지 단계를 통해 완전히 편집 가능한 GridView를 만들게 됩니다. 1 단계에서 GridView와 해당 ObjectDataSource를 만들고 BoundFields 및 CheckBoxField를 템플릿 필드로 변환 합니다. 2 단계와 3 단계에서는 `EditItemTemplate`의 편집 인터페이스를 템플릿 필드에서 `ItemTemplate` s로 이동 합니다.

## <a name="step-1-displaying-product-information"></a>1 단계: 제품 정보 표시

행을 편집할 수 있는 GridView를 만드는 방법에 대해 설명 하기 전에 제품 정보를 표시 하는 것으로 시작 해 보겠습니다. `BatchData` 폴더에서 `BatchUpdate.aspx` 페이지를 열고 GridView를 도구 상자에서 디자이너로 끌어 옵니다. GridView s `ID`를 `ProductsGrid`로 설정 하 고 스마트 태그에서 `ProductsDataSource`라는 새 ObjectDataSource에 바인딩합니다. `ProductsBLL` 클래스 s `GetProducts` 메서드에서 데이터를 검색 하도록 ObjectDataSource를 구성 합니다.

[ProductsBLL 클래스를 사용 하도록 ObjectDataSource 구성 ![](batch-updating-vb/_static/image2.gif)](batch-updating-vb/_static/image3.png)

**그림 2**: `ProductsBLL` 클래스를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](batch-updating-vb/_static/image4.png))

[GetProducts 메서드를 사용 하 여 제품 데이터를 검색 ![](batch-updating-vb/_static/image3.gif)](batch-updating-vb/_static/image5.png)

**그림 3**: `GetProducts` 메서드를 사용 하 여 제품 데이터 검색 ([전체 크기 이미지를 보려면 클릭](batch-updating-vb/_static/image6.png))

GridView와 마찬가지로 ObjectDataSource의 수정 기능은 행 단위로 작동 하도록 디자인 되었습니다. 레코드 집합을 업데이트 하려면 데이터를 일괄 처리 하 고 BLL에 전달 하는 코드 ASP.NET 페이지의 코드를 약간 작성 해야 합니다. 따라서 ObjectDataSource s 업데이트, 삽입 및 삭제 탭의 드롭다운 목록을 (없음)으로 설정 합니다. 마침을 클릭하여 마법사를 완료합니다.

[업데이트, 삽입 및 삭제 탭의 드롭다운 목록을 (없음)으로 설정 ![](batch-updating-vb/_static/image4.gif)](batch-updating-vb/_static/image7.png)

**그림 4**: 업데이트, 삽입 및 삭제 탭의 드롭다운 목록을 (없음)로 설정 ([전체 크기 이미지를 보려면 클릭](batch-updating-vb/_static/image8.png))

데이터 소스 구성 마법사를 완료 한 후 ObjectDataSource의 선언적 태그는 다음과 같습니다.

[!code-aspx[Main](batch-updating-vb/samples/sample1.aspx)]

데이터 원본 구성 마법사를 완료 하면 Visual Studio에서 GridView의 product 데이터 필드에 대 한 BoundFields 및 CheckBoxField를 만들게 됩니다. 이 자습서에서는를 사용 하 여 사용자만 제품 이름, 범주, 가격 및 단종 된 상태를 보고 편집할 수 있습니다. `ProductName`, `CategoryName`, `UnitPrice`및 `Discontinued` 필드를 제외한 모든 필드를 제거 하 고 처음 세 필드의 `HeaderText` 속성 이름을 Product, Category 및 Price로 각각 변경 합니다. 마지막으로 GridView의 스마트 태그에서 페이징 사용 및 정렬 사용 확인란을 선택 합니다.

이 시점에서 GridView에는 3 개의 BoundFields (`ProductName`, `CategoryName`및 `UnitPrice`)와 CheckBoxField (`Discontinued`)가 있습니다. 이러한 4 개 필드를 템플릿 필드로 변환한 다음 Templatefield로 변환 s `EditItemTemplate`에서 편집 인터페이스를 `ItemTemplate`으로 이동 해야 합니다.

> [!NOTE]
> [데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) 자습서에서 템플릿 필드를 만들고 사용자 지정 하는 방법을 살펴보았습니다. BoundFields 및 CheckBoxField를 템플릿 필드로 변환 하 고 해당 `ItemTemplate` s에서 편집 인터페이스를 정의 하는 단계를 안내 하지만, 중단 하거나 리프레셔가 필요한 경우이 이전 자습서를 다시 참조할 수 없습니다.

GridView s 스마트 태그에서 열 편집 링크를 클릭 하 여 필드 대화 상자를 엽니다. 그런 다음 각 필드를 선택 하 고이 필드를 Templatefield로 변환으로 변환 링크를 클릭 합니다.

![기존 BoundFields 및 CheckBoxField를 템플릿 필드로 변환](batch-updating-vb/_static/image5.gif)

**그림 5**: 기존 BoundFields 및 CheckBoxField를 템플릿 필드로 변환

이제 각 필드가 Templatefield로 변환 이므로 `EditItemTemplate`의 편집 인터페이스를 `ItemTemplate` s로 이동할 수 있습니다.

## <a name="step-2-creating-theproductnameunitprice-anddiscontinuedediting-interfaces"></a>2 단계:`ProductName`,`UnitPrice`및`Discontinued`편집 인터페이스 만들기

`ProductName`, `UnitPrice`및 `Discontinued` 편집 인터페이스를 만드는 방법은이 단계의 항목 이며, 각 인터페이스가 Templatefield로 변환 s `EditItemTemplate`에 이미 정의 되어 있으므로 매우 간단 합니다. 적용 가능한 범주의 DropDownList을 만들어야 하므로 `CategoryName` 편집 인터페이스를 만드는 것은 약간 더 복잡 합니다. 이 `CategoryName` 편집 인터페이스는 3 단계에서 세울.

`ProductName` Templatefield로 변환로 시작 하겠습니다. GridView의 스마트 태그에서 템플릿 편집 링크를 클릭 하 고 `ProductName` Templatefield로 변환 s `EditItemTemplate`으로 드릴 다운 합니다. 텍스트 상자를 선택 하 고 클립보드에 복사한 다음 `ProductName` Templatefield로 변환 s `ItemTemplate`에 붙여넣습니다. 텍스트 상자 `ID` 속성을 `ProductName`로 변경 합니다.

그런 다음 `ItemTemplate`에 RequiredFieldValidator를 추가 하 여 사용자가 각 제품 이름에 대 한 값을 제공 하는지 확인 합니다. `ControlToValidate` 속성을 ProductName로 설정 합니다. `ErrorMessage` 속성은 제품 이름을 제공 해야 합니다. \*`Text` 속성입니다. 이러한 `ItemTemplate`을 추가 하면 화면이 그림 6과 유사 하 게 표시 됩니다.

[![ProductName Templatefield로 변환에는 이제 텍스트 상자와 RequiredFieldValidator가 포함 됩니다.](batch-updating-vb/_static/image6.gif)](batch-updating-vb/_static/image9.png)

**그림 6**: 이제 `ProductName` Templatefield로 변환에 TextBox 및 RequiredFieldValidator가 포함 됩니다 ([전체 크기 이미지를 보려면 클릭](batch-updating-vb/_static/image10.png)).

`UnitPrice` 편집 인터페이스의 경우 텍스트 상자를 `EditItemTemplate`에서 `ItemTemplate`로 복사 하 여 시작 합니다. 그런 다음, 입력란 앞에 $를 놓고 `ID` 속성을 UnitPrice로 설정 하 고 `Columns` 속성을 8로 설정 합니다.

또한 `UnitPrice` s `ItemTemplate`에 CompareValidator를 추가 하 여 사용자가 입력 한 값이 $0.00 보다 크거나 같은 유효한 통화 값 인지 확인 합니다. 유효성 검사기 s `ControlToValidate` 속성을 UnitPrice로 설정 하 고 해당 `ErrorMessage` 속성을 올바른 통화 값으로 입력 해야 합니다. 통화 기호를 생략 하 고, 해당 `Text` 속성을 \*, `Type` 속성을 `Currency`, `Operator` 속성을 `GreaterThanEqual`로, 해당 `ValueToCompare` 속성을 0으로 바꾸십시오.

[CompareValidator를 추가 하 여 입력 된 가격이 음수가 아닌 통화 값 인지 확인 ![](batch-updating-vb/_static/image7.gif)](batch-updating-vb/_static/image11.png)

**그림 7**: 입력 된 가격이 음수가 아닌 통화 값 인지 확인 하기 위해 comparevalidator 추가 ([전체 크기 이미지를 보려면 클릭](batch-updating-vb/_static/image12.png))

`Discontinued` Templatefield로 변환 `ItemTemplate`에 이미 정의 되어 있는 확인란을 사용할 수 있습니다. `ID`를 중단 된 것으로 설정 하 고 `Enabled` 속성을 `True`로 설정 하기만 하면 됩니다.

## <a name="step-3-creating-thecategorynameediting-interface"></a>3 단계:`CategoryName`편집 인터페이스 만들기

`CategoryName` Templatefield로 변환 s `EditItemTemplate`의 편집 인터페이스에는 `CategoryName` 데이터 필드의 값을 표시 하는 텍스트 상자가 포함 되어 있습니다. 가능한 범주를 나열 하는 DropDownList로 대체 해야 합니다.

> [!NOTE]
> [데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) 자습서에는 텍스트 상자와는 달리 DropDownList을 포함 하도록 템플릿을 사용자 지정 하는 방법에 대 한 자세한 설명이 포함 되어 있습니다. 여기에 나와 있는 단계는 완료 되지만 tersely 제공 됩니다. DropDownList 범주를 만들고 구성 하는 방법에 대 한 자세한 내용은 [데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) 자습서를 참조 하세요.

도구 상자의 DropDownList을 `CategoryName` Templatefield로 변환 s `ItemTemplate`로 끌어 `ID`를 `Categories`로 설정 합니다. 이 시점에서는 일반적으로 스마트 태그를 통해 Dropdownlist s 데이터 원본을 정의 하 여 새 ObjectDataSource를 만듭니다. 그러나이 경우 `ItemTemplate`내에 ObjectDataSource가 추가 됩니다. 그러면 각 GridView 행에 대해 ObjectDataSource 인스턴스가 생성 됩니다. 대신를 사용 하 여 GridView의 템플릿 필드 외부에 ObjectDataSource를 만듭니다. 템플릿 편집을 종료 하 고 objectdatasource를 도구 상자에서 `ProductsDataSource` ObjectDataSource 아래의 디자이너로 끌어옵니다. 새 ObjectDataSource `CategoriesDataSource`의 이름을로 설정 하 고 `CategoriesBLL` 클래스 s `GetCategories` 메서드를 사용 하도록 구성 합니다.

[범주 Bll 클래스를 사용 하도록 ObjectDataSource 구성 ![](batch-updating-vb/_static/image8.gif)](batch-updating-vb/_static/image13.png)

**그림 8**: `CategoriesBLL` 클래스를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](batch-updating-vb/_static/image14.png))

[GetCategories 메서드를 사용 하 여 범주 데이터를 검색 ![](batch-updating-vb/_static/image9.gif)](batch-updating-vb/_static/image15.png)

**그림 9**: `GetCategories` 메서드를 사용 하 여 범주 데이터 검색 ([전체 크기 이미지를 보려면 클릭](batch-updating-vb/_static/image16.png))

이 ObjectDataSource는 단순히 데이터를 검색 하는 데 사용 되므로 업데이트 및 삭제 탭의 드롭다운 목록을 (없음)으로 설정 합니다. 마침을 클릭하여 마법사를 완료합니다.

[업데이트 및 삭제 탭의 드롭다운 목록을 (없음)으로 설정 ![](batch-updating-vb/_static/image10.gif)](batch-updating-vb/_static/image17.png)

**그림 10**: 업데이트 및 삭제 탭의 드롭다운 목록을 (없음)로 설정 ([전체 크기 이미지를 보려면 클릭](batch-updating-vb/_static/image18.png))

마법사를 완료 한 후 `CategoriesDataSource`의 선언 태그는 다음과 같습니다.

[!code-aspx[Main](batch-updating-vb/samples/sample2.aspx)]

`CategoriesDataSource` 생성 및 구성 된 상태에서 `CategoryName` Templatefield로 변환 s `ItemTemplate`으로 돌아가서 DropDownList의 스마트 태그에서 데이터 소스 선택 링크를 클릭 합니다. 데이터 소스 구성 마법사의 첫 번째 드롭다운 목록에서 `CategoriesDataSource` 옵션을 선택 하 고 표시에 사용 되는 `CategoryName`을 값으로 `CategoryID` 선택 합니다.

[DropDownList을 범주 데이터 원본에 바인딩 ![](batch-updating-vb/_static/image11.gif)](batch-updating-vb/_static/image19.png)

**그림 11**: DropDownList을 `CategoriesDataSource`에 바인딩 ([전체 크기 이미지를 보려면 클릭](batch-updating-vb/_static/image20.png))

이때 `Categories` DropDownList은 모든 범주를 나열 하지만 GridView 행에 바인딩된 제품의 적절 한 범주는 아직 자동으로 선택 하지 않습니다. 이를 수행 하려면 `Categories` DropDownList s `SelectedValue`을 제품 `CategoryID` 값으로 설정 해야 합니다. DropDownList의 스마트 태그에서 데이터 바인딩 편집 링크를 클릭 하 고 그림 12와 같이 `SelectedValue` 속성을 `CategoryID` 데이터 필드에 연결 합니다.

![제품 CategoryID 값을 DropDownList s SelectedValue 속성에 바인딩합니다.](batch-updating-vb/_static/image12.gif)

**그림 12**: 제품 `CategoryID` 값을 DropDownList s `SelectedValue` 속성에 바인딩

마지막으로 발생 한 문제: 제품에 `CategoryID` 값이 지정 되지 않은 경우 `SelectedValue`의 데이터 바인딩 문이 예외를 발생 합니다. 이는 DropDownList에는 범주에 대 한 항목만 포함 되 고 `CategoryID`에 `NULL` 데이터베이스 값이 있는 제품에 대 한 옵션은 제공 하지 않기 때문입니다. 이를 해결 하려면 DropDownList s `AppendDataBoundItems` 속성을 `True`로 설정 하 고 드롭다운에 새 항목을 추가 하 여 선언적 구문에서 `Value` 속성을 생략 합니다. 즉, `Categories` DropDownList의 선언적 구문이 다음과 같이 표시 되는지 확인 합니다.

[!code-aspx[Main](batch-updating-vb/samples/sample3.aspx)]

`<asp:ListItem Value="">`를 선택 하는 방법에 대 한 자세한 내용을 확인 하 고 `Value` 특성이 명시적으로 빈 문자열로 설정 되어 있습니다. 이러한 추가 DropDownList 항목이 `NULL` 사례를 처리 하는 데 필요한 이유와 `Value` 속성을 빈 문자열에 할당 하는 이유를 보다 자세히 설명 하려면 [데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) 자습서를 다시 참조 하세요.

> [!NOTE]
> 여기에는 잠재적 성능 및 확장성 문제가 있습니다. 각 행에는 `CategoriesDataSource`를 데이터 소스로 사용 하는 DropDownList이 있으므로 `CategoriesBLL` 클래스 s `GetCategories` 메서드는 페이지 방문 당 *n* 번 호출 됩니다. 여기서 *n* 은 GridView의 행 수입니다. `GetCategories`에 대 한 이러한 *n* 호출은 데이터베이스에 *n* 개의 쿼리를 발생 시킬 수 있습니다. 이러한 데이터베이스에 미치는 영향은 요청 당 캐시에서 또는 SQL 캐싱 종속성 또는 매우 짧은 시간 기반 만료를 사용 하는 캐싱 계층을 통해 반환 된 범주를 있으므로 안전성이 떨어질 수 있습니다. 요청당 캐싱 옵션에 대 한 자세한 내용은 [요청 당 캐시 저장소`HttpContext.Items`](http://aspnet.4guysfromrolla.com/articles/060904-1.aspx)를 참조 하세요.

## <a name="step-4-completing-the-editing-interface"></a>4 단계: 편집 인터페이스 완료

진행 상황을 보기 위해 일시 중지 하지 않고 GridView의 템플릿에 대 한 몇 가지 변경 내용을 만들었습니다. 잠시 시간을 내 서 브라우저를 통해 진행 상황을 확인 하세요. 그림 13에 표시 된 것 처럼 각 행은 셀의 편집 인터페이스를 포함 하는 `ItemTemplate`를 사용 하 여 렌더링 됩니다.

[각 GridView 행을 편집할 수 있는 ![](batch-updating-vb/_static/image13.gif)](batch-updating-vb/_static/image21.png)

**그림 13**: 각 GridView 행을 편집할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](batch-updating-vb/_static/image22.png)).

이 시점에서 주의 해야 하는 몇 가지 사소한 서식 문제가 있습니다. 첫째, `UnitPrice` 값에는 소수점이 네 개 포함 되어 있습니다. 이 문제를 해결 하려면 `UnitPrice` Templatefield로 변환 s `ItemTemplate`으로 돌아가서 TextBox의 스마트 태그에서 데이터 바인딩 편집 링크를 클릭 합니다. 그런 다음 `Text` 속성을 숫자로 서식 지정 하도록 지정 합니다.

![텍스트 속성을 숫자로 서식 지정](batch-updating-vb/_static/image14.gif)

**그림 14**: `Text` 속성을 숫자로 서식 지정

둘째, `Discontinued` 열의 확인란을 왼쪽 맞춤으로 지정 하는 대신 가운데에 놓습니다. GridView의 스마트 태그에서 열 편집을 클릭 하 고 왼쪽 아래 모퉁이의 필드 목록에서 `Discontinued` Templatefield로 변환를 선택 합니다. `ItemStyle`로 드릴 다운 하 고 그림 15와 같이 `HorizontalAlign` 속성을 가운데로 설정 합니다.

![단종 된 확인란 가운데 맞춤](batch-updating-vb/_static/image15.gif)

**그림 15**: `Discontinued` 확인란 가운데 맞춤

그런 다음 ValidationSummary 컨트롤을 페이지에 추가 하 고 해당 `ShowMessageBox` 속성을 `True`로 설정 하 고 `ShowSummary` 속성을 `False`로 설정 합니다. 또한 클릭 하면 사용자의 변경 내용을 업데이트 하는 단추 웹 컨트롤을 추가 합니다. 특히 GridView 위에 있는 Button 웹 컨트롤 두 개를 추가 하 고 그 아래에 하나를 추가 하 여 두 컨트롤 `Text` 속성을 설정 하 여 제품을 업데이트 합니다.

GridView의 편집 인터페이스는 `ItemTemplate` s의 템플릿 필드에 정의 되어 있으므로 `EditItemTemplate`는 불필요 하 고 삭제 될 수 있습니다.

위에서 언급 한 서식을 변경한 후 단추 컨트롤을 추가 하 고 불필요 한 `EditItemTemplate` s를 제거 하 고 나면 페이지의 선언적 구문은 다음과 같습니다.

[!code-aspx[Main](batch-updating-vb/samples/sample4.aspx)]

그림 16은 단추 웹 컨트롤이 추가 되 고 형식이 변경 된 후 브라우저를 통해 볼 때이 페이지를 보여 줍니다.

[이제 페이지에 두 개의 업데이트 제품 단추가 포함 됩니다 ![](batch-updating-vb/_static/image16.gif)](batch-updating-vb/_static/image23.png)

**그림 16**: 이제 페이지에 두 개의 업데이트 제품 단추가 포함 됩니다 ([전체 크기 이미지를 보려면 클릭](batch-updating-vb/_static/image24.png)).

## <a name="step-5-updating-the-products"></a>5 단계: 제품 업데이트

사용자가이 페이지를 방문 하면 수정 사항이 적용 되 고 두 개의 업데이트 제품 단추 중 하나를 클릭 합니다. 이 시점에서 각 행에 대 한 사용자가 입력 한 값을 `ProductsDataTable` 인스턴스에 저장 한 다음이를 BLL 메서드에 전달 해야 합니다. 그런 다음 해당 `ProductsDataTable` 인스턴스를 DAL의 `UpdateWithTransaction` 메서드로 전달 합니다. [이전 자습서](wrapping-database-modifications-within-a-transaction-vb.md)에서 만든 `UpdateWithTransaction` 메서드는 변경 내용 일괄 처리가 원자성 작업으로 업데이트 되도록 합니다.

`BatchUpdate.aspx.vb`에서 `BatchUpdate` 라는 메서드를 만들고 다음 코드를 추가 합니다.

[!code-vb[Main](batch-updating-vb/samples/sample5.vb)]

이 메서드는 BLL `GetProducts` 메서드를 호출 하 여 `ProductsDataTable`의 모든 제품을 다시 가져오는 방식으로 시작 됩니다. 그런 다음 `ProductGrid` GridView s [`Rows` 컬렉션](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rows(VS.80).aspx)을 열거 합니다. `Rows` 컬렉션에는 GridView에 표시 되는 각 행에 대 한 [`GridViewRow` 인스턴스가](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridviewrow.aspx) 포함 됩니다. 페이지당 최대 10 개의 행을 표시 하기 때문에 GridView s `Rows` 컬렉션에는 10 개 이하의 항목이 있습니다.

각 행에 대해 `ProductID`은 `DataKeys` 컬렉션에서 grabbed `ProductsDataTable`에서 적절 한 `ProductsRow` 선택 됩니다. 4 개의 Templatefield로 변환 입력 컨트롤은 프로그래밍 방식으로 참조 되며 해당 값은 `ProductsRow` 인스턴스 속성에 할당 됩니다. 각 GridView 행의 값을 사용 하 여 `ProductsDataTable`를 업데이트 한 후에는 해당 값이 이전 자습서에서 살펴본 것 처럼 BLL s `UpdateWithTransaction` 메서드에 전달 되며,이 메서드는 DAL s `UpdateWithTransaction` 메서드를 호출 하기만 하면 됩니다.

이 자습서에 사용 되는 일괄 업데이트 알고리즘은 제품 정보가 변경 되었는지 여부에 관계 없이 GridView의 행에 해당 하는 `ProductsDataTable`의 각 행을 업데이트 합니다. 이러한 블라인드 업데이트는 일반적으로 성능 문제가 아니지만 데이터베이스 테이블에 대 한 변경 내용을 다시 감사 하는 경우 불필요 한 레코드가 발생할 수 있습니다. [일괄 처리 업데이트 수행](../editing-and-deleting-data-through-the-datalist/performing-batch-updates-vb.md) 자습서로 돌아가서 DataList를 사용 하 여 Batch 업데이트 인터페이스를 탐색 하 고 사용자가 실제로 수정한 레코드만 업데이트 하는 코드를 추가 했습니다. 원할 경우 언제 든 지이 자습서의 코드를 업데이트 하기 위해 [Batch 업데이트를 수행](../editing-and-deleting-data-through-the-datalist/performing-batch-updates-vb.md) 하는 방법을 자유롭게 사용할 수 있습니다.

> [!NOTE]
> 스마트 태그를 통해 데이터 소스를 GridView에 바인딩하는 경우 Visual Studio에서 자동으로 GridView s `DataKeyNames` 속성에 데이터 원본의 기본 키 값을 할당 합니다. 1 단계에 설명 된 대로 GridView s 스마트 태그를 사용 하 여 ObjectDataSource를 GridView에 바인딩하지 않은 경우 `DataKeys` 컬렉션을 통해 각 행에 대 한 `ProductID` 값에 액세스 하려면 GridView s `DataKeyNames` 속성을 ProductID로 수동으로 설정 해야 합니다.

`BatchUpdate`에 사용 되는 코드는 BLL의 `UpdateProduct` 메서드에서 사용 되는 코드와 유사 하며, `UpdateProduct` 메서드의 주요 차이점은 아키텍처에서 단일 `ProductRow` 인스턴스만 검색 한다는 것입니다. `ProductRow` 속성을 할당 하는 코드는 전체 패턴과 마찬가지로 `BatchUpdate`의 `For Each` 루프 내에 있는 코드와 `UpdateProducts` 메서드와 동일 합니다.

이 자습서를 완료 하려면 제품 업데이트 단추 중 하나를 클릭할 때 `BatchUpdate` 메서드를 호출 해야 합니다. 이러한 두 단추 컨트롤의 `Click` 이벤트에 대 한 이벤트 처리기를 만들고 이벤트 처리기에 다음 코드를 추가 합니다.

[!code-vb[Main](batch-updating-vb/samples/sample6.vb)]

먼저 `BatchUpdate`를 호출 합니다. 그런 다음 [`ClientScript` 속성](https://msdn.microsoft.com/library/system.web.ui.page.clientscript(VS.80).aspx) 은 업데이트 된 제품을 읽는 messagebox를 표시 하는 JavaScript를 삽입 하는 데 사용 됩니다.

이 코드를 테스트 하는 데 몇 분 정도 걸립니다. 브라우저를 통해 `BatchUpdate.aspx`를 방문 하 여 여러 행을 편집 하 고 업데이트 제품 단추 중 하나를 클릭 합니다. 입력 유효성 검사 오류가 없는 경우 제품이 업데이트 되었다는 messagebox가 표시 되어야 합니다. 업데이트의 원자성을 확인 하려면 `UnitPrice` 값 1234.56을 허용 하지 않는 것과 같은 임의 `CHECK` 제약 조건을 추가 하는 것이 좋습니다. 그런 다음 `BatchUpdate.aspx`에서 여러 레코드를 편집 하 여 제품의 `UnitPrice` 값 중 하나를 금지 값 (1234.56)으로 설정 합니다. 이렇게 하면 해당 일괄 처리 작업 중에 다른 변경 내용으로 제품 업데이트를 클릭 하면 오류가 발생 하 여 원래 값으로 롤백됩니다.

## <a name="an-alternativebatchupdatemethod"></a>대체`BatchUpdate`메서드

방금 검사 한 `BatchUpdate` 메서드는 BLL의 `GetProducts` 메서드에서 *모든* 제품을 검색 한 다음 GridView에 표시 된 레코드만 업데이트 합니다. 이 방법은 GridView가 페이징을 사용 하지 않는 경우에 적합 하지만,이 경우에는 수백, 수천 또는 수십 개의 제품이 있을 수 있지만 GridView에는 행이 10 개만 있을 수 있습니다. 이 경우에는 데이터베이스의 모든 제품을 수정 하는 데 필요한 모든 제품을 수정 하는 것이 이상적이 지 않습니다.

이러한 유형의 경우 대신 다음 `BatchUpdateAlternate` 방법을 사용 하는 것이 좋습니다.

[!code-vb[Main](batch-updating-vb/samples/sample7.vb)]

`BatchMethodAlternate`는 `products`라는 비어 있는 새 `ProductsDataTable`를 만들어 시작 합니다. 그런 다음 GridView s `Rows` 컬렉션을 단계별로 수행 하 고 각 행에 대해 BLL의 `GetProductByProductID(productID)` 메서드를 사용 하 여 특정 제품 정보를 가져옵니다. 검색 된 `ProductsRow` 인스턴스는 `BatchUpdate`와 동일한 방식으로 속성을 업데이트 했지만 행을 업데이트 한 후 DataTable s [`ImportRow(DataRow)` 메서드](https://msdn.microsoft.com/library/system.data.datatable.importrow(VS.80).aspx)를 통해 `products` `ProductsDataTable`으로 가져옵니다.

`For Each` 루프가 완료 되 면 GridView의 각 행에 대해 하나의 `ProductsRow` 인스턴스가 `products`에 포함 됩니다. 각 `ProductsRow` 인스턴스는 업데이트 대신 `products`에 추가 되었으므로 `UpdateWithTransaction` 메서드에 무조건 전달 하면 `ProductsTableAdapter`는 각 레코드를 데이터베이스에 삽입 하려고 시도 합니다. 대신 이러한 각 행이 수정 되었는지 (추가 되지 않음) 지정 해야 합니다.

`UpdateProductsWithTransaction`이름이 지정 된 BLL에 새 메서드를 추가 하 여이를 수행할 수 있습니다. 아래에 표시 된 `UpdateProductsWithTransaction`는 `ProductsDataTable`의 각 `ProductsRow` 인스턴스의 `RowState`를 `Modified`로 설정 하 고 `ProductsDataTable`를 DAL s `UpdateWithTransaction` 메서드에 전달 합니다.

[!code-vb[Main](batch-updating-vb/samples/sample8.vb)]

## <a name="summary"></a>요약

GridView는 기본 제공 행 단위 편집 기능을 제공 하지만 완전히 편집할 수 있는 인터페이스를 만드는 데는 지원 하지 않습니다. 이 자습서에서 보았듯이 이러한 인터페이스는 가능 하지만 약간의 작업이 필요 합니다. 모든 행을 편집할 수 있는 GridView를 만들려면 GridView의 필드를 템플릿 필드로 변환 하 고 `ItemTemplate` 내에서 편집 인터페이스를 정의 해야 합니다. 또한 모든 형식 업데이트 단추 웹 컨트롤을 GridView와 별도로 페이지에 추가 해야 합니다. 이러한 단추 `Click` 이벤트 처리기는 GridView의 `Rows` 컬렉션을 열거 하 고, `ProductsDataTable`에 변경 내용을 저장 하 고, 업데이트 된 정보를 적절 한 BLL 메서드에 전달 해야 합니다.

다음 자습서에서는 batch 삭제를 위한 인터페이스를 만드는 방법을 알아봅니다. 특히 각 GridView 행은 확인란을 포함 하 고, 모든 형식 업데이트 단추 대신 선택한 행 삭제 단추를 포함 합니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서에 대 한 리드 검토자는 Teresa Murphy 및 David Suru 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](wrapping-database-modifications-within-a-transaction-vb.md)
> [다음](batch-deleting-vb.md)
