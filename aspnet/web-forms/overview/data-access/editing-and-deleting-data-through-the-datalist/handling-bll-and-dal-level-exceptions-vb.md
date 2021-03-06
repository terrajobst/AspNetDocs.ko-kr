---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/handling-bll-and-dal-level-exceptions-vb
title: BLL 및 DAL 수준의 예외 처리 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 편집 가능한 DataList의 업데이트 워크플로 중에 발생 한 예외를 tactfully 처리 하는 방법을 알아봅니다.
ms.author: riande
ms.date: 10/30/2006
ms.assetid: ca665073-b379-4239-9404-f597663ca65e
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/handling-bll-and-dal-level-exceptions-vb
msc.type: authoredcontent
ms.openlocfilehash: 319ab44f2e65afc77f6f89ca8aa58c529f40d05c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78480155"
---
# <a name="handling-bll--and-dal-level-exceptions-vb"></a>BLL 및 DAL 수준의 예외 처리(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_38_VB.exe) 또는 [PDF 다운로드](handling-bll-and-dal-level-exceptions-vb/_static/datatutorial38vb1.pdf)

> 이 자습서에서는 편집 가능한 DataList의 업데이트 워크플로 중에 발생 한 예외를 tactfully 처리 하는 방법을 알아봅니다.

## <a name="introduction"></a>소개

DataList 자습서 [에서 데이터 편집 및 삭제 개요](an-overview-of-editing-and-deleting-data-in-the-datalist-cs.md) 에서 간단한 편집 및 삭제 기능을 제공 하는 datalist를 만들었습니다. 모든 기능을 사용 하는 동안에는 편집 또는 삭제 프로세스 중 발생 한 오류 때문에 처리 되지 않은 예외가 발생 하 여 사용자에 게 친숙 하지 않습니다. 예를 들어 제품 이름을 생략 하거나 제품을 편집 하는 경우 가격 책정 값을 매우 저렴 한 가격으로 입력 하면 예외가 throw 됩니다. 이 예외는 코드에서 catch 되지 않으므로 ASP.NET 런타임으로 버블링 되어 웹 페이지에서 예외 정보를 표시 합니다.

[ASP.NET 페이지 자습서의 BLL 및 DAL 수준 예외 처리](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md) 에서 살펴본 것 처럼 비즈니스 논리 또는 데이터 액세스 계층의 깊이에서 예외가 발생 하면 예외 정보가 ObjectDataSource로 반환 된 다음 GridView로 반환 됩니다. ObjectDataSource 또는 GridView에 대해 `Updated` 또는 `RowUpdated` 이벤트 처리기를 만들고 예외를 확인 한 다음 예외가 처리 되었음을 나타내는 방법으로 이러한 예외를 정상적으로 처리 하는 방법을 살펴보았습니다.

그러나 DataList 자습서에서는 데이터를 업데이트 하 고 삭제 하는 데 ObjectDataSource를 사용 하지 않습니다. 대신, BLL에 대해 직접 작업 하 고 있습니다. BLL 또는 DAL에서 발생 하는 예외를 검색 하려면 ASP.NET 페이지의 코드를 포함 하는 예외 처리 코드를 구현 해야 합니다. 이 자습서에서는 편집 가능한 DataList s 업데이트 워크플로 중에 발생 하는 예외를 더 tactfully 처리 하는 방법을 알아봅니다.

> [!NOTE]
> DataList에서 *데이터 편집 및 삭제 개요* 에서 datalist에서 데이터를 편집 하 고 삭제 하는 다양 한 기술에 대해 설명 했습니다. 업데이트 및 삭제를 위해 ObjectDataSource를 사용 하는 몇 가지 기술이 있습니다. 이러한 기술을 사용 하는 경우 ObjectDataSource의 `Updated` 또는 `Deleted` 이벤트 처리기를 통해 BLL 또는 DAL에서 예외를 처리할 수 있습니다.

## <a name="step-1-creating-an-editable-datalist"></a>1 단계: 편집 가능한 DataList 만들기

업데이트 워크플로 중에 발생 하는 예외를 처리 하는 것에 대해 걱정 하기 전에에서 편집 가능한 DataList를 먼저 만들어야 합니다. `EditDeleteDataList` 폴더에서 `ErrorHandling.aspx` 페이지를 열고, 디자이너에 DataList를 추가 하 고, `ID` 속성을 `Products`로 설정 하 고, 이름이 `ProductsDataSource`인 새 ObjectDataSource를 추가 합니다. `ProductsBLL` 클래스 s `GetProducts()` 메서드를 사용 하 여 레코드를 선택 하도록 ObjectDataSource를 구성 합니다. 삽입, 업데이트 및 삭제 탭의 드롭다운 목록을 (없음)로 설정 합니다.

[GetProducts () 메서드를 사용 하 여 제품 정보를 반환 ![](handling-bll-and-dal-level-exceptions-vb/_static/image2.png)](handling-bll-and-dal-level-exceptions-vb/_static/image1.png)

**그림 1**: `GetProducts()` 메서드를 사용 하 여 제품 정보 반환 ([전체 크기 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-vb/_static/image3.png))

ObjectDataSource 마법사를 완료 한 후 Visual Studio에서 DataList에 대 한 `ItemTemplate`를 자동으로 만듭니다. 각 제품 이름과 가격을 표시 하 고 편집 단추를 포함 하는 `ItemTemplate`로 대체 합니다. 그런 다음 이름 및 가격, 업데이트 및 취소 단추에 대 한 텍스트 상자 웹 컨트롤을 사용 하 여 `EditItemTemplate`를 만듭니다. 마지막으로, DataList s `RepeatColumns` 속성을 2로 설정 합니다.

이러한 변경 후에는 페이지의 선언적 태그가 다음과 같이 표시 됩니다. 편집, 취소 및 업데이트 단추가 각각 편집, 취소 및 업데이트로 설정 된 `CommandName` 속성이 있는지 확인 하려면 두 번 선택 합니다.

[!code-aspx[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample1.aspx)]

> [!NOTE]
> 이 자습서에서는 DataList s 뷰 상태를 사용 하도록 설정 해야 합니다.

잠시 시간을 투자 하 여 브라우저를 통해 진행 상황을 확인 하세요 (그림 2 참조).

[![각 제품에 편집 단추가 포함 됩니다.](handling-bll-and-dal-level-exceptions-vb/_static/image5.png)](handling-bll-and-dal-level-exceptions-vb/_static/image4.png)

**그림 2**: 각 제품에는 편집 단추 ([전체 크기 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-vb/_static/image6.png))가 포함 되어 있습니다.

현재 편집 단추를 클릭 하면 포스트백만 발생 하 고 아직 제품을 편집할 수 없게 됩니다. 편집을 사용 하도록 설정 하려면 DataList s `EditCommand`, `CancelCommand`및 `UpdateCommand` 이벤트에 대 한 이벤트 처리기를 만들어야 합니다. `EditCommand` 및 `CancelCommand` 이벤트는 DataList s `EditItemIndex` 속성을 업데이트 하 고 데이터를 DataList에 다시 바인딩합니다.

[!code-vb[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample2.vb)]

`UpdateCommand` 이벤트 처리기는 약간 더 복잡 합니다. `EditItemTemplate`에 있는 텍스트 상자의 텍스트 상자에서 제품 이름 및 가격과 함께 `DataKeys` 컬렉션에서 편집한 제품 `ProductID`를 읽은 다음 DataList를 사전 편집 상태로 되돌리기 전에 `ProductsBLL` 클래스의 `UpdateProduct` 메서드를 호출 해야 합니다.

지금은 *DataList 자습서에서 데이터 편집 및 삭제 개요* 의 `UpdateCommand` 이벤트 처리기에서 정확히 동일한 코드를 사용 하겠습니다. 2 단계에서 예외를 정상적으로 처리 하는 코드를 추가 합니다.

[!code-vb[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample3.vb)]

잘못 된 형식의 단가 형식이 될 수 있는 잘못 된 입력이 발생 하는 경우-$5.00와 같은 잘못 된 단가 값 또는 예외가 발생 합니다. 이 시점에서 `UpdateCommand` 이벤트 처리기는 예외 처리 코드를 포함 하지 않기 때문에 예외는 최종 사용자에 게 표시 되는 ASP.NET 런타임으로 버블링 됩니다 (그림 3 참조).

![처리 되지 않은 예외가 발생 하면 최종 사용자에 게 오류 페이지가 표시 됩니다.](handling-bll-and-dal-level-exceptions-vb/_static/image7.png)

**그림 3**: 처리 되지 않은 예외가 발생 하면 최종 사용자에 게 오류 페이지가 표시 됩니다.

## <a name="step-2-gracefully-handling-exceptions-in-the-updatecommand-event-handler"></a>2 단계: UpdateCommand 이벤트 처리기에서 적절 하 게 예외 처리

업데이트 워크플로 중에 `UpdateCommand` 이벤트 처리기, BLL 또는 DAL에서 예외가 발생할 수 있습니다. 예를 들어 사용자가 너무 많은 가격을 입력 하는 경우 `UpdateCommand` 이벤트 처리기의 `Decimal.Parse` 문은 `FormatException` 예외를 throw 합니다. 사용자가 제품 이름을 생략 하거나 가격에 음수 값이 있는 경우 DAL은 예외를 발생 시킵니다.

예외가 발생 하면 페이지 자체 내에 정보 메시지를 표시 하려고 합니다. `ID`이 `ExceptionDetails`로 설정 된 페이지에 Label 웹 컨트롤을 추가 합니다. `Styles.css` 파일에 정의 된 `Warning` CSS 클래스에 `CssClass` 속성을 할당 하 여 텍스트를 빨강, 굵은 글꼴 및 기울임꼴 글꼴로 표시 하도록 구성 합니다.

오류가 발생 하면 레이블만 한 번만 표시 됩니다. 즉, 이후에 다시 게시 하면 레이블 s 경고 메시지가 사라집니다. 이렇게 하려면 레이블 s `Text` 속성을 지우거 나 `Visible` 속성을 설정 하 여 `Page_Load` 이벤트 처리기에서 `False` ( [ASP.NET 페이지 자습서에서 BLL 및 DAL 수준의 예외 처리](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md) ) 또는 레이블 s 뷰 상태 지원을 사용 하지 않도록 설정 하 여이를 수행할 수 있습니다. 후자 옵션을 사용할 수 있습니다.

[!code-aspx[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample4.aspx)]

예외가 발생 하면 예외에 대 한 세부 정보를 `ExceptionDetails` Label 컨트롤 s `Text` 속성에 할당 합니다. 해당 뷰 상태는 사용 하지 않도록 설정 되어 있으므로 이후에 다시 게시할 때 `Text` 속성의 프로그래밍 변경 내용이 손실 되 고 기본 텍스트 (빈 문자열)로 다시 이동 하 여 경고 메시지를 숨깁니다.

페이지에 유용한 메시지를 표시 하기 위해 오류가 발생 한 시기를 확인 하려면 `UpdateCommand` 이벤트 처리기에 `Try ... Catch` 블록을 추가 해야 합니다. `Try` 부분은 예외를 발생 시킬 수 있는 코드를 포함 하는 반면 `Catch` 블록에는 예외 발생 시 실행 되는 코드가 포함 됩니다. `Try ... Catch` 블록에 대 한 자세한 내용은 .NET Framework 설명서의 [예외 처리 기본 사항](https://msdn.microsoft.com/library/2w8f0bss.aspx) 섹션을 참조 하세요.

[!code-vb[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample5.vb)]

`Try` 블록 내의 코드에서 모든 형식의 예외를 throw 하는 경우 `Catch` 블록 코드의 실행이 시작 됩니다. `DbException`, `NoNullAllowedException`, `ArgumentException`등에서 throw 되는 예외 형식은 첫 번째 위치의 오류를 정확 하 게 바뀌고에 따라 달라 집니다. 데이터베이스 수준에 문제가 있으면 `DbException`이 throw 됩니다. `UnitPrice`, `UnitsInStock`, `UnitsOnOrder`또는 `ReorderLevel` 필드에 대해 잘못 된 값을 입력 하는 경우 `ArgumentException` 클래스에서 이러한 필드 값의 유효성을 검사 하는 코드를 추가 했으므로 `ProductsDataTable` throw 됩니다 ( [비즈니스 논리 계층 만들기](../introduction/creating-a-business-logic-layer-vb.md) 자습서 참조).

최종 사용자에 게는 발생 한 예외 형식에 대 한 메시지 텍스트를 기반으로 하 여 더 유용한 설명을 제공할 수 있습니다. [ASP.NET 페이지에서 BLL 및 DAL 수준 예외를 처리 하](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md) 는 것과 거의 동일한 폼에서 사용 된 다음 코드는이 세부 정보를 제공 합니다.

[!code-vb[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample6.vb)]

이 자습서를 완료 하려면 catch 된 `Exception` 인스턴스 (`ex`)를 전달 하는 `Catch` 블록에서 `DisplayExceptionDetails` 메서드를 호출 하면 됩니다.

`Try ... Catch` 블록을 사용 하 여 사용자에 게는 그림 4 및 5 표시와 같은 보다 자세한 오류 메시지가 표시 됩니다. 예외의 면에서 DataList는 편집 모드로 유지 됩니다. 예외가 발생 한 후에는 DataList를 사전 편집 상태로 반환 하는 코드를 무시 하 고 제어 흐름을 즉시 `Catch` 블록으로 리디렉션할 수 있습니다.

[![사용자에 게 필수 필드가 생략 된 경우 오류 메시지가 표시 됩니다.](handling-bll-and-dal-level-exceptions-vb/_static/image9.png)](handling-bll-and-dal-level-exceptions-vb/_static/image8.png)

**그림 4**: 사용자가 필요한 필드를 생략 하면 오류 메시지가 표시 됨 ([전체 크기 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-vb/_static/image10.png))

[음수 가격을 입력할 때 오류 메시지가 표시 ![](handling-bll-and-dal-level-exceptions-vb/_static/image12.png)](handling-bll-and-dal-level-exceptions-vb/_static/image11.png)

**그림 5**: 음수 가격을 입력할 때 표시 되는 오류 메시지 ([전체 크기 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-vb/_static/image13.png))

## <a name="summary"></a>요약

GridView 및 ObjectDataSource는 워크플로를 업데이트 및 삭제 하는 동안 발생 한 예외에 대 한 정보를 포함 하는 사후 수준 이벤트 처리기를 제공 하 고, 예외가 발생 했는지 여부를 나타내기 위해 설정할 수 있는 속성을 제공 합니다. handled. 그러나 DataList를 사용 하 고 BLL을 직접 사용 하는 경우에는 이러한 기능을 사용할 수 없습니다. 대신 예외 처리를 구현 해야 합니다.

이 자습서에서는 `UpdateCommand` 이벤트 처리기에 `Try ... Catch` 블록을 추가 하 여 편집 가능한 DataList s 업데이트 워크플로에 예외 처리를 추가 하는 방법을 살펴보았습니다. 업데이트 워크플로 중에 예외가 발생 하면 `Catch` 블록의 코드가 실행 되어 `ExceptionDetails` 레이블에 유용한 정보가 표시 됩니다.

이 시점에서 DataList는 첫 번째 위치에서 발생 하는 예외를 방지 하는 작업을 수행 하지 않습니다. 부정적인 가격이 예외를 발생 시키는 경우에도 사용자가 이러한 잘못 된 입력을 입력 하는 것을 사전에 방지 하는 기능이 아직 추가 되지 않았습니다. 다음 자습서에서는 `EditItemTemplate`유효성 검사 컨트롤을 추가 하 여 잘못 된 사용자 입력으로 인해 발생 하는 예외를 줄이는 방법에 대해 알아봅니다.

행복 한 프로그래밍

## <a name="further-reading"></a>추가 참고 자료

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [예외 디자인 지침](https://msdn.microsoft.com/library/ms298399.aspx)
- [오류 로깅 모듈 및 처리기 (ELMAH)](http://workspaces.gotdotnet.com/elmah) (오류 로깅을 위한 오픈 소스 라이브러리)
- [.NET Framework 2.0에 대 한 Enterprise Library](https://www.microsoft.com/downloads/details.aspx?familyid=5A14E870-406B-4F2A-B723-97BA84AE80B5&amp;displaylang=en) (예외 관리 응용 프로그램 블록 포함)

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 켄은 Pespisa입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](performing-batch-updates-vb.md)
> [다음](adding-validation-controls-to-the-datalist-s-editing-interface-vb.md)
