---
uid: web-forms/overview/data-access/working-with-batched-data/batch-deleting-vb
title: 일괄 삭제 (VB) | Microsoft Docs
author: rick-anderson
description: 단일 작업에서 여러 데이터베이스 레코드를 삭제 하는 방법에 대해 알아봅니다. 사용자 인터페이스 계층에서 이전에 만든 향상 된 GridView에 대해 빌드 ...
ms.author: riande
ms.date: 06/26/2007
ms.assetid: 4fb72f75-32ab-4bf7-a764-be20367be726
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/batch-deleting-vb
msc.type: authoredcontent
ms.openlocfilehash: 0974a16764eee2ef03cf36b4b15f9ef41f99982b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78476459"
---
# <a name="batch-deleting-vb"></a>일괄 삭제(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_65_VB.zip) 또는 [PDF 다운로드](batch-deleting-vb/_static/datatutorial65vb1.pdf)

> 단일 작업에서 여러 데이터베이스 레코드를 삭제 하는 방법에 대해 알아봅니다. 사용자 인터페이스 계층에서는 이전 자습서에서 만든 향상 된 GridView를 기반으로 작성 되었습니다. 데이터 액세스 계층에서는 트랜잭션 내에서 여러 개의 삭제 작업을 래핑하여 모든 삭제가 성공 하거나 모든 삭제가 롤백되기를 확인 합니다.

## <a name="introduction"></a>소개

[이전 자습서](batch-updating-vb.md) 에서는 완전히 편집 가능한 GridView를 사용 하 여 일괄 처리 편집 인터페이스를 만드는 방법을 살펴보았습니다. 사용자가 일반적으로 한 번에 많은 레코드를 편집 하는 경우에는 일괄 처리 편집 인터페이스에서 훨씬 더 많은 포스트백 및 키보드-마우스 컨텍스트 전환이 필요 하므로 최종 사용자의 효율성을 향상 시킬 수 있습니다. 이 기술은 사용자가 한 번의 이동에서 많은 레코드를 삭제 하는 것이 일반적 인 페이지에도 유용 합니다.

온라인 전자 메일 클라이언트를 사용 하는 모든 사용자는 이미 가장 일반적인 배치 삭제 인터페이스 중 하나를 사용 하는 것이 이미 익숙할 것입니다. 즉, 선택한 모든 항목을 삭제 하는 표의 각 행에 있는 확인란을 선택 합니다 (그림 1 참조). 이 자습서에서는 웹 기반 인터페이스와 일련의 레코드를 단일 원자성 작업으로 삭제 하는 메서드를 모두 만드는 이전 자습서의 모든 하드 작업을 이미 수행 했기 때문에 더 간단 합니다. 확인란의 [Gridview 열 추가](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-vb.md) 자습서에서는 확인란의 열을 사용 하 여 gridview를 만들고 [트랜잭션 내에서 데이터베이스 수정 내용 래핑](wrapping-database-modifications-within-a-transaction-vb.md) 자습서에서 트랜잭션을 사용 하 여 `ProductID` 값의 `List<T>`를 삭제 하는 메서드를 생성 했습니다. 이 자습서에서는 이전 환경을 빌드하고 병합 하 여 작업 일괄 삭제 예제를 만듭니다.

[각 행 ![확인란을 포함 합니다.](batch-deleting-vb/_static/image1.gif)](batch-deleting-vb/_static/image1.png)

**그림 1**: 각 행에는 확인란 ([전체 크기 이미지를 보려면 클릭](batch-deleting-vb/_static/image2.png))이 포함 되어 있습니다.

## <a name="step-1-creating-the-batch-deleting-interface"></a>1 단계: 일괄 삭제 인터페이스 만들기

[확인란의 GridView 열 추가](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-vb.md) 자습서에서 일괄 삭제 인터페이스를 이미 만들었기 때문에 처음부터 새로 만드는 대신 `BatchDelete.aspx`으로 복사할 수 있습니다. 먼저 `BatchData` 폴더의 `BatchDelete.aspx` 페이지와 `EnhancedGridView` 폴더의 `CheckBoxField.aspx` 페이지를 엽니다. `CheckBoxField.aspx` 페이지에서 원본 뷰로 이동 하 고 그림 2와 같이 `<asp:Content>` 태그 사이에 태그를 복사 합니다.

[CheckBoxField의 선언적 태그를 클립보드에 복사 ![](batch-deleting-vb/_static/image2.gif)](batch-deleting-vb/_static/image3.png)

**그림 2**: `CheckBoxField.aspx`의 선언적 태그를 클립보드로 복사 ([전체 크기 이미지를 보려면 클릭](batch-deleting-vb/_static/image4.png))

그런 다음 `BatchDelete.aspx`의 원본 뷰로 이동 하 여 클립보드의 내용을 `<asp:Content>` 태그 안에 붙여넣습니다. 또한 `CheckBoxField.aspx.vb`의 코드 숨김이 클래스 내에서 코드를 복사 하 여 `BatchDelete.aspx.vb` (`DeleteSelectedProducts` 단추 s `Click` 이벤트 처리기, `ToggleCheckState` 메서드 및 `Click` 및 `CheckAll` 단추에 대 한 `UncheckAll` 이벤트 처리기)에 붙여 넣습니다. 이 콘텐츠를 복사 하 고 나면 `BatchDelete.aspx` 페이지의 코드 숨김이 클래스에 다음 코드가 포함 되어야 합니다.

[!code-vb[Main](batch-deleting-vb/samples/sample1.vb)]

선언적 태그 및 소스 코드를 복사 하 고 나 서 브라우저를 통해 확인 하 여 `BatchDelete.aspx` 테스트 합니다. GridView에서 처음 10 개 제품을 나열 하는 GridView가 표시 되어야 합니다. 각 행에는 제품 이름, 범주 및 가격이 나열 됩니다 (확인란 포함). 선택한 제품을 모두 선택 하 고 모두 선택 취소 하 고 삭제 하는 세 가지 단추가 있습니다. 모두 확인 단추를 클릭 하면 모든 확인란을 선택 하 고 모두 선택 취소는 모든 확인란의 선택을 취소 합니다. 선택한 제품 삭제를 클릭 하면 선택한 제품의 `ProductID` 값을 나열 하지만 실제로는 제품이 삭제 되지 않는다는 메시지가 표시 됩니다.

[CheckBoxField의 인터페이스가 BatchDeleting로 이동 되었습니다. ![](batch-deleting-vb/_static/image3.gif)](batch-deleting-vb/_static/image5.png)

**그림 3**: `CheckBoxField.aspx`의 인터페이스가 `BatchDeleting.aspx`으로 이동 되었습니다 ([전체 크기 이미지를 보려면 클릭](batch-deleting-vb/_static/image6.png)).

## <a name="step-2-deleting-the-checked-products-using-transactions"></a>2 단계: 트랜잭션을 사용 하 여 선택 된 제품 삭제

일괄 처리 삭제 인터페이스가 `BatchDeleting.aspx`에 성공적으로 복사 되 면 선택한 제품 삭제 단추가 `ProductsBLL` 클래스의 `DeleteProductsWithTransaction` 메서드를 사용 하 여 선택 된 제품을 삭제 하도록 코드를 업데이트 하는 것만 남았습니다. 트랜잭션 자습서에서 [데이터베이스 수정 내용 래핑](wrapping-database-modifications-within-a-transaction-vb.md) 에 추가 된이 메서드는 `ProductID` 값의 `List(Of T)` 입력으로 받아들이고 트랜잭션 범위 내에서 해당 하는 각 `ProductID`를 삭제 합니다.

`DeleteSelectedProducts` Button s `Click` 이벤트 처리기는 현재 다음 `For Each` 루프를 사용 하 여 각 GridView 행을 반복 합니다.

[!code-vb[Main](batch-deleting-vb/samples/sample2.vb)]

`ProductSelector` CheckBox 웹 컨트롤은 각 행에 대해 프로그래밍 방식으로 참조 됩니다. 이 확인란이 선택 되어 있으면 행 `ProductID` `DataKeys` 컬렉션에서 검색 되 고 `DeleteResults` 레이블 s `Text` 속성은 행을 삭제 하도록 선택 했음을 나타내는 메시지를 포함 하도록 업데이트 됩니다.

위의 코드는 `ProductsBLL` 클래스 `Delete` 메서드에 대 한 호출이 주석 처리 됨에 따라 실제로 레코드를 삭제 하지 않습니다. 이 삭제 논리가 적용 되었으므로 코드에서 제품이 삭제 되지만 원자성 작업 내에서는 삭제 되지 않습니다. 즉, 시퀀스에서 처음 몇 개의 삭제가 성공 했지만 나중에 실패 한 경우 (foreign key 제약 조건 위반으로 인해) 예외가 throw 되지만 이미 삭제 된 제품은 삭제 된 상태로 유지 됩니다.

원자성을 보장 하기 위해 `ProductsBLL` 클래스 s `DeleteProductsWithTransaction` 메서드를 대신 사용 해야 합니다. 이 메서드는 `ProductID` 값 목록을 허용 하므로 먼저 표에서이 목록을 컴파일한 다음 매개 변수로 전달 해야 합니다. 먼저 `Integer`형식의 `List(Of T)` 인스턴스를 만듭니다. `For Each` 루프 내에서 선택한 products `ProductID` 값을이 `List(Of T)`에 추가 해야 합니다. 루프 후이 `List(Of T)` `ProductsBLL` 클래스 `DeleteProductsWithTransaction` 메서드에 전달 해야 합니다. 다음 코드를 사용 하 여 `DeleteSelectedProducts` Button s `Click` 이벤트 처리기를 업데이트 합니다.

[!code-vb[Main](batch-deleting-vb/samples/sample3.vb)]

업데이트 된 코드는 `Integer` (`productIDsToDelete`) 형식의 `List(Of T)`를 만들고 삭제할 `ProductID` 값으로 채웁니다. `For Each` 루프 후 하나 이상의 제품이 선택 되어 있으면 `ProductsBLL` 클래스 s `DeleteProductsWithTransaction` 메서드가 호출 되 고이 목록을 전달 합니다. `DeleteResults` 레이블만 표시 되 고 데이터를 GridView로 데이터 바인딩 (새로 삭제 된 레코드가 더 이상 표에 행으로 표시 되지 않음).

그림 4는 삭제를 위해 여러 행이 선택 된 후의 GridView를 보여 줍니다. 그림 5는 선택한 제품 삭제 단추를 클릭 한 직후의 화면을 보여 줍니다. 그림 5에서 삭제 된 레코드의 `ProductID` 값은 GridView 아래 레이블에 표시 되 고 해당 행은 더 이상 GridView에 표시 되지 않습니다.

[선택한 제품을 삭제 ![](batch-deleting-vb/_static/image4.gif)](batch-deleting-vb/_static/image7.png)

**그림 4**: 선택한 제품이 삭제 됩니다 ([전체 크기 이미지를 보려면 클릭](batch-deleting-vb/_static/image8.png)).

[삭제 된 Products ProductID 값 ![GridView 아래에 나열 됩니다.](batch-deleting-vb/_static/image5.gif)](batch-deleting-vb/_static/image9.png)

**그림 5**: 삭제 된 Products `ProductID` 값은 GridView 아래에 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](batch-deleting-vb/_static/image10.png)).

> [!NOTE]
> `DeleteProductsWithTransaction` 메서드 원자성을 테스트 하려면 `Order Details` 테이블에서 제품에 대 한 항목을 수동으로 추가한 다음 해당 제품 (다른 사용자와 함께)을 삭제 하려고 시도 합니다. 연결 된 순서를 사용 하 여 제품을 삭제 하려고 하면 foreign key 제약 조건 위반이 발생 하지만, 선택한 다른 제품 삭제가 롤백되는 것을 확인할 수 있습니다.

## <a name="summary"></a>요약

일괄 삭제 인터페이스를 만들려면 확인란의 열과 함께 GridView를 추가 하 고 클릭 하면 선택한 모든 행을 단일 원자성 작업으로 삭제 하는 단추 웹 컨트롤이 포함 됩니다. 이 자습서에서는 두 가지 이전 자습서에서 작업을 함께 수행 하 고, [확인란의 GridView 열을 추가](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-vb.md) 하 고, [트랜잭션 내에서 데이터베이스 수정 내용을 래핑하](wrapping-database-modifications-within-a-transaction-vb.md)는 방법으로 piecing 하 여 이러한 인터페이스를 구축 했습니다. 첫 번째 자습서에서는 확인란 및 열이 포함 된 GridView를 만들었으며 후자에서 메서드를 구현 했습니다 .이 메서드는 `ProductID` 값 `List(Of T)` 전달 될 때 트랜잭션 범위 내에서 모두 삭제 되었습니다.

다음 자습서에서는 배치 삽입을 수행 하는 인터페이스를 만듭니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Hilton Gid Esenow 및 Teresa Murphy 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](batch-updating-vb.md)
> [다음](batch-inserting-vb.md)
