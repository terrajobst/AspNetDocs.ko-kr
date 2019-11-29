---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-vb
title: 삽입, 업데이트 및 삭제와 연결 된 이벤트 검사 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 ASP.NET data 웹 컨트롤의 삽입, 업데이트 또는 삭제 작업 전후에 발생 하는 이벤트를 사용 하 여 검토 합니다. W ...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: c9bd10a7-eff8-4d8c-bec9-963c2aef2d6e
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-vb
msc.type: authoredcontent
ms.openlocfilehash: 35edb3cefc6fe23bb56e667c02d10dc7798f730d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74632803"
---
# <a name="examining-the-events-associated-with-inserting-updating-and-deleting-vb"></a>삽입, 업데이트 및 삭제와 연결된 이벤트 검사(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_17_VB.exe) 또는 [PDF 다운로드](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/datatutorial17vb1.pdf)

> 이 자습서에서는 ASP.NET data 웹 컨트롤의 삽입, 업데이트 또는 삭제 작업 전후에 발생 하는 이벤트를 사용 하 여 검토 합니다. 제품 필드의 하위 집합만 업데이트 하도록 편집 인터페이스를 사용자 지정 하는 방법에 대해서도 살펴봅니다.

## <a name="introduction"></a>소개

GridView, DetailsView 또는 FormView 컨트롤의 기본 제공 삽입, 편집 또는 삭제 기능을 사용 하는 경우 최종 사용자가 새 레코드를 추가 하거나 기존 레코드를 업데이트 또는 삭제 하는 프로세스를 완료할 때 다양 한 단계가 발생 합니다. [이전 자습서](an-overview-of-inserting-updating-and-deleting-data-vb.md)에서 설명한 대로 GridView에서 행을 편집 하면 편집 단추가 업데이트 및 취소 단추로 바뀌고 BoundFields 텍스트 상자로 바뀝니다. 최종 사용자가 데이터를 업데이트 하 고 업데이트를 클릭 하면 다시 게시 시 다음 단계가 수행 됩니다.

1. GridView는 `DataKeyNames` 속성을 통해 사용자가 입력 한 값과 함께 ObjectDataSource의 `UpdateParameters`를 편집 된 레코드의 고유 식별 필드로 채웁니다.
2. GridView는 ObjectDataSource의 `Update()` 메서드를 호출 하며,이 메서드는 기본 개체 (`ProductsDAL.UpdateProduct`이전 자습서의)에서 적절 한 메서드를 호출 합니다.
3. 이제 업데이트 된 변경 내용을 포함 하는 기본 데이터가 GridView에 바인딩 되었습니다.

이러한 단계를 수행 하는 동안 많은 이벤트가 발생 하 여 필요에 따라 사용자 지정 논리를 추가 하는 이벤트 처리기를 만들 수 있습니다. 예를 들어 1 단계 전에 GridView의 `RowUpdating` 이벤트가 발생 합니다. 지금은 유효성 검사 오류가 발생 하는 경우 업데이트 요청을 취소할 수 있습니다. `Update()` 메서드가 호출 되 면 ObjectDataSource의 `Updating` 이벤트가 발생 하 여 `UpdateParameters`의 값을 추가 하거나 사용자 지정할 수 있습니다. ObjectDataSource의 내부 개체의 메서드가 실행을 완료 하면 ObjectDataSource의 `Updated` 이벤트가 발생 합니다. `Updated` 이벤트에 대 한 이벤트 처리기는 업데이트 작업에 대 한 세부 정보 (예: 영향을 받는 행 수 및 예외 발생 여부)를 검사할 수 있습니다. 마지막으로 2 단계 이후에 GridView의 `RowUpdated` 이벤트가 발생 합니다. 이 이벤트에 대 한 이벤트 처리기는 수행 된 업데이트 작업에 대 한 추가 정보를 확인할 수 있습니다.

그림 1에서는 GridView를 업데이트할 때 발생 하는 이러한 일련의 이벤트와 단계를 보여 줍니다. 그림 1의 이벤트 패턴은 GridView로 업데이트 하는 데 고유 하지 않습니다. GridView, DetailsView 또는 FormView의 데이터를 삽입, 업데이트 또는 삭제 하는 것은 데이터 웹 컨트롤과 ObjectDataSource 모두에 대해 사전 및 사후 수준 이벤트의 동일한 순서를 precipitates 합니다.

[GridView에서 데이터를 업데이트할 때 일련의 사전 및 사후 이벤트 발생 ![](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image2.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image1.png)

**그림 1**: GridView에서 데이터를 업데이트할 때의 일련의 사전 및 사후 이벤트 발생 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image3.png))

이 자습서에서는 이러한 이벤트를 사용 하 여 기본 제공 되는 ASP.NET 데이터 웹 컨트롤의 삽입, 업데이트 및 삭제 기능을 확장 하는 방법을 살펴보겠습니다. 제품 필드의 하위 집합만 업데이트 하도록 편집 인터페이스를 사용자 지정 하는 방법에 대해서도 살펴봅니다.

## <a name="step-1-updating-a-productsproductnameandunitpricefields"></a>1 단계: 제품의`ProductName`및`UnitPrice`필드 업데이트

이전 자습서의 편집 인터페이스에서 읽기 전용이 아닌 *모든* 제품 필드를 포함 해야 했습니다. GridView에서 필드를 제거 하는 경우 `QuantityPerUnit`-데이터를 업데이트할 때 데이터 웹 컨트롤이 ObjectDataSource의 `QuantityPerUnit` `UpdateParameters` 값을 설정 하지 않습니다. 그러면 ObjectDataSource는 `Nothing` 값을 `UpdateProduct` BLL (비즈니스 논리 계층) 메서드로 전달 하 여 편집 된 데이터베이스 레코드의 `QuantityPerUnit` 열을 `NULL` 값으로 변경 합니다. 마찬가지로 `ProductName`와 같은 필수 필드가 편집 인터페이스에서 제거 되는 경우 " *' ProductName ' 열이 null을 허용 하지*않습니다." 라는 오류와 함께 업데이트가 실패 합니다. 이 동작의 이유는 ObjectDataSource가 각 product 필드에 대 한 입력 매개 변수를 예상 하는 `ProductsBLL` 클래스의 `UpdateProduct` 메서드를 호출 하도록 구성 되었기 때문입니다. 따라서 ObjectDataSource의 `UpdateParameters` 컬렉션은 메서드의 각 입력 매개 변수에 대 한 매개 변수를 포함 합니다.

최종 사용자가 필드의 하위 집합만 업데이트할 수 있는 데이터 웹 컨트롤을 제공 하려는 경우 ObjectDataSource의 `Updating` 이벤트 처리기에서 누락 된 `UpdateParameters` 값을 프로그래밍 방식으로 설정 하거나 필드의 하위 집합만 필요한 BLL 메서드를 만들고 호출 해야 합니다. 이러한 후자의 방법을 살펴보겠습니다.

특히 편집 가능한 GridView의 `ProductName` 및 `UnitPrice` 필드를 표시 하는 페이지를 만들어 보겠습니다. 이 GridView의 편집 인터페이스에서는 사용자가 두 개의 표시 된 필드인 `ProductName` 및 `UnitPrice`만 업데이트할 수 있습니다. 이 편집 인터페이스는 제품 필드의 하위 집합만 제공 하므로 기존 BLL의 `UpdateProduct` 메서드를 사용 하 고 누락 된 product 필드 값이 `Updating` 이벤트 처리기에서 프로그래밍 방식으로 설정 되어 있거나 GridView에 정의 된 필드의 하위 집합만 필요한 새 BLL 메서드를 만들어야 하는 ObjectDataSource를 만들어야 합니다. 이 자습서에서는 두 번째 옵션을 사용 하 여 입력 매개 변수 `productName`, `unitPrice`, `productID`에 사용 되는 `UpdateProduct` 메서드의 오버 로드를 만듭니다.

[!code-vb[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample1.vb)]

원래 `UpdateProduct` 메서드와 마찬가지로이 오버 로드는 데이터베이스에 지정 된 `ProductID`제품이 있는지 확인 하 여 시작 합니다. 그렇지 않으면 제품 정보 업데이트 요청이 실패 했음을 나타내는 `False`를 반환 합니다. 그렇지 않으면 기존 제품 레코드의 `ProductName` 및 `UnitPrice` 필드를 적절 하 게 업데이트 하 고 TableAdapter의 `Update()` 메서드를 호출 하 여 `ProductsRow` 인스턴스를 전달 하 여 업데이트를 커밋합니다.

이 외에도 `ProductsBLL` 클래스를 사용 하 여 간소화 된 GridView 인터페이스를 만들 준비가 되었습니다. `EditInsertDelete` 폴더에서 `DataModificationEvents.aspx`를 열고 페이지에 GridView를 추가 합니다. 새 ObjectDataSource를 만들고 `GetProducts`에 `Select()` 메서드 매핑을 사용 하 여 `ProductsBLL` 클래스를 사용 하도록 구성 하 고 `UpdateProduct`, `productName`및 `unitPrice`입력 매개 변수만 사용 하는 `productID` 오버 로드에 해당 `Update()` 메서드 매핑을 구성 합니다. 그림 2에서는 ObjectDataSource의 `Update()` 메서드를 `ProductsBLL` 클래스의 새 `UpdateProduct` 메서드 오버 로드에 매핑할 때 데이터 원본 만들기 마법사를 보여 줍니다.

[![ObjectDataSource의 Update () 메서드를 새 UpdateProduct 오버 로드에 매핑합니다.](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image5.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image4.png)

**그림 2**: ObjectDataSource의 `Update()` 메서드를 새 `UpdateProduct` 오버 로드에 매핑 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image6.png))

이 예제에서는 처음에는 데이터를 편집 하는 기능만 필요 하지만 레코드를 삽입 하거나 삭제 하는 것은 필요 하지 않습니다. 삽입 및 삭제 탭으로 이동 하 고 드롭다운 목록에서 (없음)을 선택 하 여 ObjectDataSource의 `Insert()` 및 `Delete()` 메서드가 `ProductsBLL` 클래스의 메서드에 매핑되지 않도록 명시적으로 지정 합니다.

[삽입 및 삭제 탭의 드롭다운 목록에서 (없음)을 선택 ![.](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image8.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image7.png)

**그림 3**: 삽입 및 삭제 탭의 드롭다운 목록에서 (없음) 선택 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image9.png))

이 마법사를 완료 한 후 GridView의 스마트 태그에서 편집 사용 확인란을 선택 합니다.

데이터 소스 만들기 마법사를 완료 하 고 GridView에 바인딩한 경우 Visual Studio에서 두 컨트롤에 대 한 선언적 구문을 만들었습니다. 원본 뷰로 이동 하 여 아래와 같이 ObjectDataSource의 선언 태그를 검사 합니다.

[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample2.aspx)]

ObjectDataSource의 `Insert()` 및 `Delete()` 메서드에 대 한 매핑이 없으므로 `InsertParameters` 또는 `DeleteParameters` 섹션이 없습니다. 또한 `Update()` 메서드는 세 개의 입력 매개 변수만 허용 하는 `UpdateProduct` 메서드 오버 로드에 매핑되므로 `UpdateParameters` 섹션에는 `Parameter` 인스턴스가 3 개만 있습니다.

ObjectDataSource의 `OldValuesParameterFormatString` 속성은 `original_{0}`로 설정 됩니다. 이 속성은 데이터 소스 구성 마법사를 사용 하는 경우 Visual Studio에서 자동으로 설정 됩니다. 그러나 BLL 메서드에 원래 `ProductID` 값이 전달 되는 것으로 간주 되지 않으므로 ObjectDataSource의 선언적 구문에서이 속성 할당을 모두 제거 합니다.

> [!NOTE]
> 디자인 뷰에 있는 속성 창에서 `OldValuesParameterFormatString` 속성 값을 지우면 속성은 여전히 선언 구문에 있지만 빈 문자열로 설정 됩니다. 선언적 구문에서 속성을 완전히 제거 하거나 속성 창에서 값을 기본값인 `{0}`로 설정 합니다.

ObjectDataSource에는 제품 이름, 가격 및 ID에 대 한 `UpdateParameters` 포함 되어 있지만 Visual Studio는 각 제품의 필드에 대해 GridView에서 BoundField 또는 CheckBoxField를 추가 했습니다.

[GridView ![각 제품의 필드에 대 한 BoundField 또는 CheckBoxField를 포함 합니다.](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image11.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image10.png)

**그림 4**: GridView에 각 제품의 필드에 대 한 BoundField 또는 CheckBoxField 포함 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image12.png))

최종 사용자가 제품을 편집 하 고 업데이트 단추를 클릭 하면 GridView는 읽기 전용이 아닌 필드를 열거 합니다. 그런 다음 ObjectDataSource의 `UpdateParameters` 컬렉션에 있는 해당 매개 변수 값을 사용자가 입력 한 값으로 설정 합니다. 해당 하는 매개 변수가 없는 경우 GridView는 컬렉션에 하나를 추가 합니다. 따라서 GridView에 모든 제품의 필드에 대 한 BoundFields 및 CheckBoxFields가 포함 되어 있으면 objectdatasource의 선언적 태그가 3 개의 입력 매개 변수만 지정 한다는 사실에도 ObjectDataSource는 이러한 모든 매개 변수를 사용 하는 `UpdateProduct` 오버 로드를 호출 합니다 (그림 5 참조). 마찬가지로 GridView에 `UpdateProduct` 오버 로드에 대 한 입력 매개 변수에 해당 하지 않는 읽기 전용 product 필드가 일부 조합 되어 있으면 업데이트를 시도할 때 예외가 발생 합니다.

[![GridView가 ObjectDataSource의 UpdateParameters 컬렉션에 매개 변수를 추가 합니다.](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image14.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image13.png)

**그림 5**: GridView가 ObjectDataSource의 `UpdateParameters` 컬렉션에 매개 변수 추가 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image15.png))

ObjectDataSource에서 제품의 이름, 가격 및 ID만 사용 하는 `UpdateProduct` 오버 로드를 호출 하도록 하려면 `ProductName` 및 `UnitPrice`에 대 한 편집 가능한 필드가 있도록 GridView를 제한 해야 합니다. 다른 BoundFields 및 CheckBoxFields을 제거 하거나, 다른 필드의 `ReadOnly` 속성을 `True`로 설정 하거나, 둘 중 일부를 조합 하 여이를 수행할 수 있습니다. 이 자습서에서는 `ProductName` 및 `UnitPrice` BoundFields를 제외한 모든 GridView 필드를 단순히 제거 하 고 그 후에 GridView의 선언적 태그가 다음과 같이 표시 되도록 합니다.

[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample3.aspx)]

`UpdateProduct` 오버 로드에는 세 개의 입력 매개 변수가 필요 하지만 GridView에는 두 개의 BoundFields 있습니다. `productID` 입력 매개 변수가 기본 키 값이 고 편집 된 행의 `DataKeyNames` 속성 값을 통해 전달 되기 때문입니다.

`UpdateProduct` 오버 로드와 함께 GridView를 사용 하 여 사용자는 다른 제품 필드를 잃지 않고 제품의 이름과 가격만 편집할 수 있습니다.

[인터페이스 ![제품의 이름과 가격만 편집할 수 있습니다.](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image17.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image16.png)

**그림 6**: 인터페이스에서 제품의 이름과 가격만 편집할 수 있음 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image18.png))

> [!NOTE]
> 이전 자습서에서 설명한 대로 GridView의 뷰 상태를 사용 하도록 설정 하는 것이 매우 중요 합니다 (기본 동작). GridView s `EnableViewState` 속성을 `false`로 설정 하면 동시 사용자가 실수로 레코드를 삭제 하거나 편집 하는 위험을 발생 시킬 수 있습니다. 자세한 내용은 [경고: 편집 및/또는 삭제를 지원 하 고 해당 뷰 상태를 사용할 수 없는 ASP.NET 2.0 gridviews/DetailsView/FormViews의 동시성 문제](http://scottonwriting.net/sowblog/posts/10054.aspx) 를 참조 하세요.

## <a name="improving-theunitpriceformatting"></a>`UnitPrice`서식 향상

그림 6에 표시 된 GridView 예제가 작동 하는 반면 `UnitPrice` 필드는 서식이 지정 되지 않으므로 통화 기호가 없고 소수 자릿수가 네 자리에 있는 가격 표시가 표시 됩니다. 편집할 수 없는 행에 통화 서식을 적용 하려면 `UnitPrice` BoundField의 `DataFormatString` 속성을 `{0:c}`로 설정 하 고 해당 `HtmlEncode` 속성을 `False`로 설정 하면 됩니다.

[UnitPrice의 DataFormatString 및 HtmlEncode 속성을 적절 하 게 설정 ![](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image20.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image19.png)

**그림 7**: `UnitPrice`의 `DataFormatString` 및 `HtmlEncode` 속성을 적절[하 게 설정 (전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image21.png))

이러한 변경으로 편집할 수 없는 행은 가격의 서식을 통화로 지정 합니다. 그러나 편집 된 행은 통화 기호 없이 네 개의 소수 자릿수로 값을 계속 표시 합니다.

[편집할 수 없는 행을 통화 값으로 서식 지정 ![](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image23.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image22.png)

**그림 8**: 편집할 수 없는 행의 서식이 통화 값으로 지정 되었습니다 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image24.png)).

`DataFormatString` 속성에 지정 된 서식 지정 지침은 BoundField의 `ApplyFormatInEditMode` 속성을 `True` (기본값은 `False`)로 설정 하 여 편집 인터페이스에 적용할 수 있습니다. 잠시 시간을 사용 하 여이 속성을 `True`설정 합니다.

[![UnitPrice BoundField의 ApplyFormatInEditMode 속성을 True로 설정 합니다.](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image26.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image25.png)

**그림 9**: `UnitPrice` BoundField의 `ApplyFormatInEditMode` 속성을 `True`로 설정 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image27.png))

이와 같이 변경 하면 편집 된 행에 표시 되는 `UnitPrice` 값도 통화로 형식이 지정 됩니다.

[편집 된 행의 UnitPrice 값이 현재 통화로 서식 지정 된 ![](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image29.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image28.png)

**그림 10**: 편집 된 행의 `UnitPrice` 값이 통화 형식으로 지정 됩니다 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image30.png)).

그러나 $19.00 등의 텍스트 상자에서 통화 기호를 사용 하 여 제품을 업데이트 하면 `FormatException`발생 합니다. GridView가 사용자 제공 값을 ObjectDataSource의 `UpdateParameters` 컬렉션에 할당 하려고 하면 `UnitPrice` 문자열 "$19.00"을 매개 변수에 필요한 `Decimal`으로 변환할 수 없습니다 (그림 11 참조). 이를 해결 하기 위해 GridView의 `RowUpdating` 이벤트에 대 한 이벤트 처리기를 만들고 사용자 제공 `UnitPrice`를 통화 형식 `Decimal`로 구문 분석 합니다.

GridView의 `RowUpdating` 이벤트는 [GridViewUpdateEventArgs](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridviewupdateeventargs(VS.80).aspx)형식의 개체를 두 번째 매개 변수로 받아들입니다. 여기에는 `NewValues` 사전을 ObjectDataSource의 `UpdateParameters` 컬렉션에 할당할 준비가 된 사용자 제공 값을 보유 하는 속성 중 하나로 포함 됩니다. `RowUpdating` 이벤트 처리기에서 다음 코드 줄과 함께 통화 형식을 사용 하 여 구문 분석 된 10 진수 값을 사용 하 여 `NewValues` 컬렉션의 기존 `UnitPrice` 값을 덮어쓸 수 있습니다.

[!code-vb[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample4.vb)]

사용자가 `UnitPrice` 값 (예: "$19.00")을 제공한 경우 Decimal로 계산 된 10 진수 값으로이 값을 덮어씁니다 [. 구문](https://msdn.microsoft.com/library/system.decimal.parse(VS.80).aspx)분석 하 고 값을 통화로 구문 분석 합니다. 이렇게 하면 통화 기호, 쉼표, 소수점 등의 경우 decimal을 올바르게 구문 분석 하 고, NumberStyles 네임 스페이스에서 [열거형](https://msdn.microsoft.com/library/system.globalization.numberstyles(VS.80).aspx) 을 사용 [합니다.](https://msdn.microsoft.com/library/abeh092z(VS.80).aspx)

그림 11은 사용자가 제공 하는 `UnitPrice`의 통화 기호로 인 한 문제를 모두 보여 주며, GridView의 `RowUpdating` 이벤트 처리기를 활용 하 여 이러한 입력을 올바르게 구문 분석 하는 방법을 보여 줍니다.

[편집 된 행의 UnitPrice 값이 현재 통화로 서식 지정 된 ![](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image32.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image31.png)

**그림 11**: 편집한 행의 `UnitPrice` 값이 통화 형식으로 지정 됨 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image33.png))

## <a name="step-2-prohibitingnull-unitprices"></a>2 단계:`NULL UnitPrices` 금지

데이터베이스가 `Products` 테이블의 `UnitPrice` 열에서 `NULL` 값을 허용 하도록 구성 되어 있는 동안이 특정 페이지를 방문 하는 사용자가 `NULL` `UnitPrice` 값을 지정 하지 못하게 할 수 있습니다. 즉, 사용자가 제품 행을 편집할 때 `UnitPrice` 값을 입력 하지 못한 경우에는 데이터베이스에 결과를 저장 하는 대신,이 페이지를 통해 편집 된 모든 제품에 지정 된 가격이 있어야 한다는 메시지를 사용자에 게 알리는 메시지를 표시 하려는 메시지를 표시 하려고 합니다.

GridView의 `RowUpdating` 이벤트 처리기에 전달 되는 `GridViewUpdateEventArgs` 개체에는 `True`로 설정 된 경우 업데이트 프로세스가 종료 되는 `Cancel` 속성이 포함 되어 있습니다. `RowUpdating` 이벤트 처리기를 확장 하 여 `e.Cancel`을 `True`로 설정 하 고 `NewValues` 컬렉션의 `UnitPrice` 값에 `Nothing`값이 있는 이유를 설명 하는 메시지를 표시 해 보겠습니다.

`MustProvideUnitPriceMessage`이라는 페이지에 Label 웹 컨트롤을 추가 하 여 시작 합니다. 사용자가 제품을 업데이트할 때 `UnitPrice` 값을 지정 하지 못하면이 레이블 컨트롤이 표시 됩니다. 레이블의 `Text` 속성을 "제품에 대 한 가격을 제공 해야 합니다."로 설정 합니다. 또한 다음과 같은 정의를 사용 하 여 `Warning` 이라는 `Styles.css` 새 CSS 클래스를 만들었습니다.

[!code-css[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample5.css)]

마지막으로 레이블의 `CssClass` 속성을 `Warning`로 설정 합니다. 이 시점에서 디자이너는 그림 12와 같이 GridView 위에 빨간색, 굵게, 기울임꼴, 매우 큰 글꼴 크기로 경고 메시지를 표시 해야 합니다.

[레이블이 GridView 위에 추가 된 ![](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image35.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image34.png)

**그림 12**: GridView 위에 레이블이 추가 됨 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image36.png))

기본적으로이 레이블은 숨겨야 하므로 `Visible` 속성을 `Page_Load` 이벤트 처리기에서 `False`로 설정 합니다.

[!code-vb[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample6.vb)]

사용자가 `UnitPrice`지정 하지 않고 제품을 업데이트 하려고 시도 하는 경우 업데이트를 취소 하 고 경고 레이블을 표시 하려고 합니다. 다음과 같이 GridView의 `RowUpdating` 이벤트 처리기를 확대 합니다.

[!code-vb[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample7.vb)]

사용자가 가격을 지정 하지 않고 제품을 저장 하려고 하면 업데이트가 취소 되 고 유용한 메시지가 표시 됩니다. 데이터베이스 및 비즈니스 논리는 `NULL` `UnitPrice` s를 허용 하지만이 특정 ASP.NET 페이지는 그렇지 않습니다.

[![사용자가 단가를 비워 둘 수 없음](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image38.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image37.png)

**그림 13**: 사용자가 `UnitPrice` 비워 둘 수 없음 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image39.png))

지금까지 GridView의 `RowUpdating` 이벤트를 사용 하 여 ObjectDataSource의 `UpdateParameters` 컬렉션에 할당 된 매개 변수 값을 프로그래밍 방식으로 변경 하 고 업데이트 프로세스를 모두 취소 하는 방법을 살펴보았습니다. 이러한 개념은 DetailsView 및 FormView 컨트롤로 전달 되며 삽입 및 삭제에도 적용 됩니다.

이러한 작업은 `Inserting`, `Updating`및 `Deleting` 이벤트에 대 한 이벤트 처리기를 통해 ObjectDataSource 수준에서 수행할 수도 있습니다. 이러한 이벤트는 기본 개체의 연결 된 메서드를 호출 하기 전에 발생 하며 입력 매개 변수 컬렉션을 수정 하거나 작업을 완전히 취소할 수 있는 마지막 기회를 제공 합니다. 이러한 세 이벤트에 대 한 이벤트 처리기에는 두 가지 대상 속성이 있는 [ObjectDataSourceMethodEventArgs](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourcemethodeventargs(VS.80).aspx) 형식의 개체가 전달 됩니다.

- [Cancel](https://msdn.microsoft.com/library/system.componentmodel.canceleventargs.cancel(VS.80).aspx)(`True`로 설정 된 경우 수행 중인 작업을 취소 합니다.
- [InputParameters](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourcemethodeventargs.inputparameters(VS.80).aspx)는 이벤트 처리기가 `Inserting`, `Updating`또는 `Deleting` 이벤트에 대 한 것인지에 따라 `InsertParameters`, `UpdateParameters`또는 `DeleteParameters`의 컬렉션입니다.

ObjectDataSource 수준에서 매개 변수 값을 사용 하 여 작업 하는 방법을 설명 하기 위해 사용자가 새 제품을 추가할 수 있는 DetailsView을 페이지에 포함 하겠습니다. 이 DetailsView은 데이터베이스에 새 제품을 빠르게 추가 하기 위한 인터페이스를 제공 하는 데 사용 됩니다. 새 제품을 추가할 때 사용자 인터페이스를 일관 되 게 유지 하려면 사용자가 `ProductName` 및 `UnitPrice` 필드 값만 입력할 수 있도록 합니다. 기본적으로 DetailsView의 삽입 인터페이스에 지정 되지 않은 값은 `NULL` 데이터베이스 값으로 설정 됩니다. 그러나 ObjectDataSource의 `Inserting` 이벤트를 사용 하 여 다른 기본값을 삽입할 수 있습니다. 잠시 후에 표시 됩니다.

## <a name="step-3-providing-an-interface-to-add-new-products"></a>3 단계: 새 제품을 추가 하기 위한 인터페이스 제공

도구 상자의 DetailsView을 GridView 위의 디자이너로 끌어다 놓고 `Height` 및 `Width` 속성을 지우고 페이지에 이미 있는 ObjectDataSource에 바인딩합니다. 이렇게 하면 각 제품의 필드에 대 한 BoundField 또는 CheckBoxField이 추가 됩니다. 이 DetailsView을 사용 하 여 새 제품을 추가 하려고 하므로 스마트 태그에서 삽입 사용 옵션을 선택 해야 합니다. 그러나 ObjectDataSource의 `Insert()` 메서드가 `ProductsBLL` 클래스의 메서드에 매핑되지 않았기 때문에 이러한 옵션은 없습니다. (데이터 원본을 구성할 때이 매핑을 (없음)으로 설정 한다는 것을 기억 하십시오).

ObjectDataSource를 구성 하려면 스마트 태그에서 데이터 소스 구성 링크를 선택 하 여 마법사를 시작 합니다. 첫 번째 화면에서는 ObjectDataSource가 바인딩되는 기본 개체를 변경할 수 있습니다. `ProductsBLL`로 설정 합니다. 다음 화면은 ObjectDataSource의 메서드에서 기본 개체의에 대 한 매핑을 나열 합니다. `Insert()` 및 `Delete()` 메서드가 메서드에 매핑되지 않아야 한다는 것을 명시적으로 표시 했지만 삽입 및 삭제 탭으로 이동 하면 매핑이 있는 것을 볼 수 있습니다. 이는 `ProductsBLL`의 `AddProduct` 및 `DeleteProduct` 메서드가 `DataObjectMethodAttribute` 특성을 사용 하 여 각각 `Insert()` 및 `Delete()`에 대 한 기본 메서드 임을 나타내는 것 이기 때문입니다. 따라서 일부 다른 값이 명시적으로 지정 되어 있지 않으면 마법사를 실행할 때마다 ObjectDataSource 마법사에서이를 선택 합니다.

`Insert()` 메서드를 `AddProduct` 메서드를 가리키는 상태로 두고 삭제 탭의 드롭다운 목록을 (없음)로 다시 설정 합니다.

[![삽입 탭의 드롭다운 목록을 AddProduct 메서드로 설정 합니다.](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image41.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image40.png)

**그림 14**: 삽입 탭의 드롭다운 목록을 `AddProduct` 메서드로 설정 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image42.png))

[![삭제 탭의 드롭다운 목록을 (없음)으로 설정 합니다.](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image44.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image43.png)

**그림 15**: 삭제 탭의 드롭다운 목록을 (없음)로 설정 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image45.png))

이러한 변경을 수행한 후 아래와 같이 ObjectDataSource의 선언 구문이 `InsertParameters` 컬렉션을 포함 하도록 확장 됩니다.

[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample8.aspx)]

마법사를 다시 실행 하면 `OldValuesParameterFormatString` 속성이 다시 추가 됩니다. 이 속성을 기본값 (`{0}`)으로 설정 하거나 선언적 구문에서 완전히 제거 하 여이 속성을 지우십시오.

ObjectDataSource는 삽입 기능을 제공 하므로 DetailsView의 스마트 태그에는 삽입 가능 확인란이 포함 됩니다. 디자이너로 돌아가서이 옵션을 선택 합니다. 그런 다음 두 개의 BoundFields `ProductName` 및 `UnitPrice`와 CommandField만 갖도록 DetailsView을 줄이려면 상당한 합니다. 이 시점에서 DetailsView의 선언 구문은 다음과 같습니다.

[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample9.aspx)]

그림 16은이 시점에서 브라우저를 통해 볼 때이 페이지를 보여 줍니다. 여기에서 볼 수 있듯이 DetailsView에는 첫 번째 제품의 이름과 가격이 나열 됩니다 (Chai). 그러나 원하는 것은 사용자가 데이터베이스에 새 제품을 신속 하 게 추가할 수 있는 방법을 제공 하는 삽입 인터페이스입니다.

[![DetailsView은 현재 읽기 전용 모드에서 렌더링 됩니다.](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image47.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image46.png)

**그림 16**: DetailsView은 현재 읽기 전용 모드에서 렌더링 됩니다 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image48.png)).

삽입 모드에서 DetailsView을 표시 하려면 `DefaultMode` 속성을 `Inserting`으로 설정 해야 합니다. 이렇게 하면 처음 방문할 때 DetailsView이 삽입 모드로 렌더링 되어 새 레코드를 삽입 한 후에도 삽입 모드로 유지 됩니다. 그림 17에 나와 있는 것 처럼 이러한 DetailsView은 새 레코드를 추가 하기 위한 빠른 인터페이스를 제공 합니다.

[![DetailsView은 새 제품을 빠르게 추가 하기 위한 인터페이스를 제공 합니다.](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image50.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image49.png)

**그림 17**: DetailsView은 새 제품을 빠르게 추가 하기 위한 인터페이스를 제공 합니다 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image51.png)).

사용자가 제품 이름 및 가격 (예: 그림 17에서와 같이 "Acme 물" 및 1.99)을 입력 하 고 삽입을 클릭 하면 ensues 및 삽입 워크플로 시작 됩니다가 데이터베이스에 추가 되는 새 제품 레코드에 culminating. DetailsView은 삽입 인터페이스를 유지 하며, GridView는 그림 18과 같이 새 제품을 포함 하기 위해 데이터 원본에 자동으로 자동으로 바인딩 됩니다.

![제품](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image52.png)

**그림 18**: "Acme 워터" 제품이 데이터베이스에 추가 되었습니다.

그림 18의 GridView가 표시 되지 않지만 DetailsView 인터페이스 `CategoryID`, `SupplierID`, `QuantityPerUnit`등에 없는 product 필드는 데이터베이스 값 `NULL` 할당 됩니다. 다음 단계를 수행 하 여이를 확인할 수 있습니다.

1. Visual Studio에서 서버 탐색기로 이동 합니다.
2. `NORTHWND.MDF` database 노드 확장
3. `Products` 데이터베이스 테이블 노드를 마우스 오른쪽 단추로 클릭 합니다.
4. 테이블 데이터 표시 선택

그러면 `Products` 테이블의 모든 레코드가 나열 됩니다. 그림 19에 나와 있는 것 처럼 `ProductID`, `ProductName`및 `UnitPrice` 이외의 모든 새 제품 열에는 `NULL` 값이 있습니다.

[![DetailsView에서 제공 되지 않은 제품 필드에 NULL 값이 할당 됩니다.](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image54.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image53.png)

**그림 19**: DetailsView에서 제공 하지 않는 제품 필드에 값 `NULL` 할당 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image55.png))

`NULL`가 최상의 기본 옵션이 아니거나 데이터베이스 열 자체에서 `NULL`를 허용 하지 않기 때문에 이러한 열 값 중 하나 이상에 대해 `NULL` 이외의 기본값을 제공할 수 있습니다. 이를 위해 DetailsView의 `InputParameters` 컬렉션에 대 한 매개 변수 값을 프로그래밍 방식으로 설정할 수 있습니다. 이 할당은 DetailsView의 `ItemInserting` 이벤트에 대 한 이벤트 처리기 또는 ObjectDataSource의 `Inserting` 이벤트에서 수행할 수 있습니다. 데이터 웹 컨트롤 수준에서 사전 및 사후 수준 이벤트를 사용 하는 것을 이미 살펴보았습니다. 이번에는 ObjectDataSource의 이벤트를 사용 하는 방법을 살펴보겠습니다.

## <a name="step-4-assigning-values-to-thecategoryidandsupplieridparameters"></a>4 단계:`CategoryID`및`SupplierID`매개 변수에 값 할당

이 자습서에서는이 인터페이스를 통해 새 제품을 추가할 때 응용 프로그램에 대해 `CategoryID` 및 `SupplierID` 값 1을 할당 해야 한다고 가정 합니다. 앞서 언급 했 듯이 ObjectDataSource는 데이터 수정 프로세스 중에 발생 하는 한 쌍의 사전 및 사후 수준 이벤트를 포함 합니다. `Insert()` 메서드가 호출 되 면 ObjectDataSource는 먼저 `Inserting` 이벤트를 발생 시킨 다음 해당 `Insert()` 메서드가 매핑되는 메서드를 호출 하 고 마지막으로 `Inserted` 이벤트를 발생 시킵니다. `Inserting` 이벤트 처리기는 입력 매개 변수를 조정 하거나 작업을 완전히 취소할 수 있는 마지막 기회를 하나 이상 활용 합니다.

> [!NOTE]
> 실제 응용 프로그램에서는 사용자가 범주 및 공급자를 지정 하거나, 일부 조건 또는 비즈니스 논리 (ID 1을 무조건 선택 하는 것이 아님)에 따라이 값을 선택 하는 것이 좋습니다. 예를 들어,이 예제에서는 ObjectDataSource의 사전 수준 이벤트에서 입력 매개 변수의 값을 프로그래밍 방식으로 설정 하는 방법을 보여 줍니다.

잠시를 사용 하 여 ObjectDataSource의 `Inserting` 이벤트에 대 한 이벤트 처리기를 만듭니다. 이벤트 처리기의 두 번째 입력 매개 변수는 매개 변수 컬렉션에 액세스 하는 속성 (`InputParameters`) 및 작업을 취소 하는 속성 (`Cancel`)을 포함 하는 `ObjectDataSourceMethodEventArgs`형식의 개체입니다.

[!code-vb[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample10.vb)]

이 시점에서 `InputParameters` 속성은 DetailsView에서 할당 된 값을 가진 ObjectDataSource의 `InsertParameters` 컬렉션을 포함 합니다. 이러한 매개 변수 중 하나의 값을 변경 하려면 `e.InputParameters("paramName") = value`을 사용 하면 됩니다. 따라서 `CategoryID`을 설정 하 고 값을 1로 `SupplierID` `Inserting` 이벤트 처리기를 다음과 같이 조정 합니다.

[!code-vb[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample11.vb)]

이번에는 새 제품 (예: Acme)을 추가할 때 새 제품의 `CategoryID` 및 `SupplierID` 열이 1로 설정 됩니다 (그림 20 참조).

[새 제품 ![이제 CategoryID 및 공급자 값을 1로 설정 합니다.](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image57.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image56.png)

**그림 20**: 이제 새 제품의 `CategoryID` 및 `SupplierID` 값이 1로 설정 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image58.png))

## <a name="summary"></a>요약

편집, 삽입 및 삭제 프로세스를 수행 하는 동안 데이터 웹 컨트롤과 ObjectDataSource는 다 수의 사전 및 사후 수준 이벤트를 처리 합니다. 이 자습서에서는 사전 수준 이벤트를 검사 하 고 이러한 이벤트를 사용 하 여 입력 매개 변수를 사용자 지정 하거나 데이터 수정 작업을 데이터 웹 컨트롤과 ObjectDataSource의 이벤트 둘 다에서 취소 하는 방법을 살펴보았습니다. 다음 자습서에서는 사후 수준 이벤트에 대 한 이벤트 처리기를 만들고 사용 하는 방법을 살펴봅니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Jackie Goor 및 Liz Shulok 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](an-overview-of-inserting-updating-and-deleting-data-vb.md)
> [다음](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md)
