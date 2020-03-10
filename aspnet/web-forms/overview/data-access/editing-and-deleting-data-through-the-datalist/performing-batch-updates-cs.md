---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/performing-batch-updates-cs
title: 일괄 처리 업데이트 수행C#() | Microsoft Docs
author: rick-anderson
description: 모든 항목이 편집 모드에 있고 해당 값을 저장할 수 있는 완전히 편집 가능한 DataList를 만드는 방법에 대 한 자세한 내용은 ...
ms.author: riande
ms.date: 10/30/2006
ms.assetid: 57743ca7-5695-4e07-aed1-44b297f245a9
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/performing-batch-updates-cs
msc.type: authoredcontent
ms.openlocfilehash: cde12a4d24555216adc49dd02818901278932eaa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78480047"
---
# <a name="performing-batch-updates-c"></a>일괄 처리 업데이트 수행(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_37_CS.exe) 또는 [PDF 다운로드](performing-batch-updates-cs/_static/datatutorial37cs1.pdf)

> 모든 항목이 편집 모드에 있고 페이지의 "모두 업데이트" 단추를 클릭 하 여 값을 저장할 수 있는 완전히 편집 가능한 DataList를 만드는 방법에 대해 알아봅니다.

## <a name="introduction"></a>소개

[이전 자습서](an-overview-of-editing-and-deleting-data-in-the-datalist-cs.md) 에서는 항목 수준 DataList를 만드는 방법을 살펴보았습니다. 표준 편집 가능한 GridView와 마찬가지로 DataList의 각 항목에는 클릭 하면 항목을 편집할 수 있도록 하는 편집 단추가 포함 됩니다. 이러한 항목 수준 편집은 가끔씩만 업데이트 되는 데이터에 적합 하지만 특정 사용 사례 시나리오에서는 사용자가 많은 레코드를 편집 해야 합니다. 사용자가 수십 개의 레코드를 편집 해야 하 고 편집을 클릭 하 고 편집을 클릭 한 다음 각 항목에 대해 업데이트를 클릭 하면 클릭의 양이 생산성을 저하 시킬 수 있습니다. 이러한 경우에는 완전히 편집 가능한 DataList를 제공 하는 것이 좋습니다 .이 경우 *모든* 항목이 편집 모드에 있고 페이지의 모두 업데이트 단추를 클릭 하 여 값을 편집할 수 있습니다 (그림 1 참조).

[완전히 편집 가능한 DataList의 각 항목 ![수정할 수 있습니다.](performing-batch-updates-cs/_static/image2.png)](performing-batch-updates-cs/_static/image1.png)

**그림 1**: 완전히 편집 가능한 DataList의 각 항목을 수정할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](performing-batch-updates-cs/_static/image3.png)).

이 자습서에서는 사용자가 완전히 편집 가능한 DataList를 사용 하 여 공급자 주소 정보를 업데이트할 수 있도록 하는 방법을 살펴보겠습니다.

## <a name="step-1-create-the-editable-user-interface-in-the-datalist-s-itemtemplate"></a>1 단계: DataList s ItemTemplate에서 편집 가능한 사용자 인터페이스 만들기

이전 자습서에서 표준 항목 수준 편집 가능 DataList를 만드는 경우 다음 두 가지 템플릿을 사용 했습니다.

- `ItemTemplate`에는 읽기 전용 사용자 인터페이스 (각 제품의 이름과 가격을 표시 하기 위한 레이블 웹 컨트롤)가 포함 되어 있습니다.
- `EditItemTemplate`에는 편집 모드 사용자 인터페이스 (두 TextBox 웹 컨트롤)가 포함 되어 있습니다.

DataList s `EditItemIndex` 속성은 `EditItemTemplate`을 사용 하 여 렌더링 되는 `DataListItem` (있는 경우)을 결정 합니다. 특히 `ItemIndex` 값이 DataList s `EditItemIndex` 속성과 일치 하는 `DataListItem` `EditItemTemplate`를 사용 하 여 렌더링 됩니다. 이 모델은 한 번에 하나의 항목만 편집할 수 있지만 완전히 편집 가능한 DataList를 만드는 경우에는 잘 작동 합니다.

완전히 편집 가능한 DataList의 경우 편집 가능한 인터페이스를 사용 하 여 *모든* `DataListItem`를 렌더링 하려고 합니다. 이를 수행 하는 가장 간단한 방법은 `ItemTemplate`에서 편집 가능한 인터페이스를 정의 하는 것입니다. 공급자 주소 정보를 수정 하기 위해 편집 가능한 인터페이스에는 공급자 이름이 텍스트로 포함 되 고 주소, 구/군/시 및 국가 값의 텍스트 상자가 포함 됩니다.

먼저 `BatchUpdate.aspx` 페이지를 열고 DataList 컨트롤을 추가 하 고 `ID` 속성을 `Suppliers`로 설정 합니다. DataList s 스마트 태그에서 `SuppliersDataSource`라는 새 ObjectDataSource 컨트롤을 추가 합니다.

[SuppliersDataSource 라는 새 ObjectDataSource를 만들 ![](performing-batch-updates-cs/_static/image5.png)](performing-batch-updates-cs/_static/image4.png)

**그림 2**: `SuppliersDataSource` 라는 새 ObjectDataSource 만들기 ([전체 크기 이미지를 보려면 클릭](performing-batch-updates-cs/_static/image6.png))

`SuppliersBLL` 클래스 s `GetSuppliers()` 메서드를 사용 하 여 데이터를 검색 하도록 ObjectDataSource를 구성 합니다 (그림 3 참조). 위의 자습서와 같이 ObjectDataSource를 통해 공급자 정보를 업데이트 하는 대신, 비즈니스 논리 계층에서 직접 작업 합니다. 따라서 업데이트 탭에서 드롭다운 목록을 (없음)으로 설정 합니다 (그림 4 참조).

[GetSuppliers () 메서드를 사용 하 여 공급자 정보를 검색 ![](performing-batch-updates-cs/_static/image8.png)](performing-batch-updates-cs/_static/image7.png)

**그림 3**: `GetSuppliers()` 메서드를 사용 하 여 공급자 정보 검색 ([전체 크기 이미지를 보려면 클릭](performing-batch-updates-cs/_static/image9.png))

[업데이트 탭에서 드롭다운 목록을 (없음)으로 설정 ![](performing-batch-updates-cs/_static/image11.png)](performing-batch-updates-cs/_static/image10.png)

**그림 4**: 업데이트 탭에서 드롭다운 목록을 (없음)으로 설정 ([전체 크기 이미지를 보려면 클릭](performing-batch-updates-cs/_static/image12.png))

마법사를 완료 한 후 Visual Studio에서 자동으로 DataList s `ItemTemplate` 생성 하 여 데이터 소스에서 반환 하는 각 데이터 필드를 레이블 웹 컨트롤에 표시 합니다. 대신 편집 인터페이스를 제공 하도록이 템플릿을 수정 해야 합니다. `ItemTemplate`는 DataList의 스마트 태그에서 템플릿 편집 옵션을 사용 하거나 선언적 구문을 통해 직접 디자이너를 통해 사용자 지정할 수 있습니다.

공급자의 이름을 텍스트로 표시 하는 편집 인터페이스를 만들고 공급자의 주소, 구/군/시 및 국가 값에 대 한 텍스트 상자를 포함 합니다. 이러한 변경을 수행한 후에는 페이지의 선언 구문이 다음과 같이 표시 됩니다.

[!code-aspx[Main](performing-batch-updates-cs/samples/sample1.aspx)]

> [!NOTE]
> 위의 자습서와 마찬가지로이 자습서의 DataList는 해당 뷰 상태를 사용 하도록 설정 해야 합니다.

`ItemTemplate` I m에서 `SupplierPropertyLabel` 및 `SupplierPropertyValue`두 개의 새 CSS 클래스를 사용 합니다 .이 클래스는 `Styles.css` 클래스에 추가 되 고 `ProductPropertyLabel` 및 `ProductPropertyValue` CSS 클래스와 동일한 스타일 설정을 사용 하도록 구성 됩니다.

[!code-css[Main](performing-batch-updates-cs/samples/sample2.css)]

이러한 변경을 수행한 후 브라우저를 통해이 페이지를 방문 하세요. 그림 5에 표시 된 것 처럼 각 DataList 항목은 공급자 이름을 텍스트로 표시 하 고 텍스트 상자를 사용 하 여 주소, 도시 및 국가를 표시 합니다.

[DataList의 각 공급자 ![편집할 수 있습니다.](performing-batch-updates-cs/_static/image14.png)](performing-batch-updates-cs/_static/image13.png)

**그림 5**: DataList의 각 공급자를 편집할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](performing-batch-updates-cs/_static/image15.png)).

## <a name="step-2-adding-an-update-all-button"></a>2 단계: 모두 업데이트 단추 추가

그림 5의 각 공급 업체에는 해당 주소, 도시 및 국가 필드가 텍스트 상자에 표시 되지만 현재는 사용 가능한 업데이트 단추가 없습니다. 완전히 편집 가능한 DataLists을 사용 하 여 항목당 업데이트 단추를 사용 하는 대신, 페이지에는 클릭 시 DataList의 *모든* 레코드를 업데이트 하는 단일 업데이트 모두 단추가 있습니다. 이 자습서에서는 페이지 맨 위에 1 개의 업데이트를 모두 추가 하 고, 아래쪽에 하나를 추가 합니다. 단추를 클릭 해도 동일한 효과가 있습니다.

먼저 DataList 위에 단추 웹 컨트롤을 추가 하 고 `ID` 속성을 `UpdateAll1`로 설정 합니다. 그런 다음 두 번째 Button 웹 컨트롤을 DataList 아래에 추가 하 고 해당 `ID`을 `UpdateAll2`로 설정 합니다. 두 단추의 `Text` 속성을 모두 업데이트로 설정 합니다. 마지막으로 두 단추 `Click` 이벤트에 대 한 이벤트 처리기를 만듭니다. 각 이벤트 처리기에서 업데이트 논리를 복제 하는 대신,를 사용 하면 이벤트 처리기가이 세 번째 메서드를 호출 하는 `UpdateAllSupplierAddresses`세 번째 메서드로 해당 논리를 리팩터링할 수 있습니다.

[!code-csharp[Main](performing-batch-updates-cs/samples/sample3.cs)]

그림 6은 업데이트 모두 단추가 추가 된 후의 페이지를 보여 줍니다.

[![두 업데이트 모두 페이지에 추가 되었습니다.](performing-batch-updates-cs/_static/image17.png)](performing-batch-updates-cs/_static/image16.png)

**그림 6**: 페이지에 두 개의 업데이트 모두 단추가 추가 되었습니다 ([전체 크기 이미지를 보려면 클릭](performing-batch-updates-cs/_static/image18.png)).

## <a name="step-3-updating-all-of-the-suppliers-address-information"></a>3 단계: 모든 공급자 주소 정보 업데이트

모든 DataList 항목을 편집 인터페이스를 표시 하 고 모두 업데이트 단추를 추가 하 여, 일괄 업데이트를 수행 하는 코드를 작성 하는 것만 남았습니다. 특히 DataList s 항목을 반복 하 고 각 항목에 대해 `SuppliersBLL` 클래스 `UpdateSupplierAddress` 메서드를 호출 해야 합니다.

Datalist를 구성을 하는 `DataListItem` 인스턴스의 컬렉션은 DataList s [`Items` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.items.aspx)을 통해 액세스할 수 있습니다. `DataListItem`에 대 한 참조를 사용 하 여 `DataKeys` 컬렉션에서 해당 `SupplierID`를 가져오고 다음 코드에서 보여 주는 것 처럼 `ItemTemplate` 내에서 TextBox 웹 컨트롤을 프로그래밍 방식으로 참조할 수 있습니다.

[!code-csharp[Main](performing-batch-updates-cs/samples/sample4.cs)]

사용자가 업데이트 모두 단추 중 하나를 클릭 하면 `UpdateAllSupplierAddresses` 메서드가 `Suppliers` DataList의 각 `DataListItem`를 반복 하 고 `SuppliersBLL` 클래스의 `UpdateSupplierAddress` 메서드를 호출 하 여 해당 값을 전달 합니다. 주소, 구/군/시 또는 국가 패스에 대해 입력 하지 않은 값은 `UpdateSupplierAddress` (빈 문자열이 아님)에 `Nothing` 값 이므로 기본 레코드의 필드에 대 한 데이터베이스가 `NULL` 됩니다.

> [!NOTE]
> 향상 된 기능으로, 일괄 업데이트를 수행한 후에 몇 가지 확인 메시지를 제공 하는 상태 레이블 웹 컨트롤을 페이지에 추가할 수 있습니다.

## <a name="updating-only-those-addresses-that-have-been-modified"></a>수정 된 주소만 업데이트

이 자습서에 사용 되는 batch 업데이트 알고리즘은 주소 정보가 변경 되었는지 여부에 관계 없이 DataList의 *모든* 공급자에 대 한 `UpdateSupplierAddress` 메서드를 호출 합니다. 이러한 블라인드 업데이트는 일반적으로 성능 문제가 아니지만 데이터베이스 테이블에 대 한 변경 내용을 다시 감사 하는 경우 불필요 한 레코드가 발생할 수 있습니다. 예를 들어 트리거를 사용 하 여 모든 `UPDATE` s를 `Suppliers` 테이블에 기록 하는 경우 사용자가 모두 업데이트 단추를 클릭 하면 사용자가 변경 했는지 여부에 관계 없이 시스템의 각 공급자에 대해 새 감사 레코드가 생성 됩니다.

ADO.NET DataTable 및 DataAdapter 클래스는 수정, 삭제 및 새 레코드만이 모든 데이터베이스 통신을 발생 하는 일괄 업데이트를 지원 하도록 설계 되었습니다. DataTable의 각 행에는 행이 DataTable에 추가 되었는지, 삭제 되었는지, 수정 됨 또는 변경 되지 않은 상태로 유지 되는지를 나타내는 [`RowState` 속성이](https://msdn.microsoft.com/library/system.data.datarow.rowstate.aspx) 있습니다. DataTable이 처음 채워질 때 모든 행이 변경 되지 않은 상태로 표시 됩니다. 행 s 열의 값을 변경 하면 해당 행이 수정 된 것으로 표시 됩니다.

`SuppliersBLL` 클래스에서 먼저 단일 공급자 레코드에서 `SuppliersDataTable`으로 읽은 후 다음 코드를 사용 하 여 `Address`, `City`및 `Country` 열 값을 설정 하 여 지정 된 공급자의 주소 정보를 업데이트 합니다.

[!code-csharp[Main](performing-batch-updates-cs/samples/sample5.cs)]

이 코드 naively는 값이 변경 되었는지 여부에 관계 없이 `SuppliersDataTable`의 `SuppliersRow`에 전달 된 주소, 구/군/시 및 국가 값을 할당 합니다. 이러한 수정으로 인해 `SuppliersRow` s `RowState` 속성이 수정 된 것으로 표시 됩니다. 데이터 액세스 계층 s `Update` 메서드가 호출 되 면 `SupplierRow` 수정 되어 `UPDATE` 명령이 데이터베이스에 전송 되는 것을 볼 수 있습니다.

그러나이 메서드에 코드를 추가 하 여 전달 된 주소, 구/군/시 및 국가 값이 `SuppliersRow` 기존 값과 다를 경우에만 해당 값을 할당 한다고 가정해 보겠습니다. 주소, 구/군/시 및 국가가 기존 데이터와 같은 경우에는 변경 내용이 적용 되지 않으며 `SupplierRow` s `RowState`는 변경 되지 않은 상태로 표시 됩니다. 결과적으로 DAL s `Update` 메서드가 호출 되 면 `SuppliersRow` 수정 되지 않았기 때문에 데이터베이스를 호출 하지 않습니다.

이러한 변경을 적용 하려면 전달 된 주소, 구/군/시 및 국가 값을 무조건 할당 하는 문을 다음 코드로 바꿉니다.

[!code-csharp[Main](performing-batch-updates-cs/samples/sample6.cs)]

이 추가 된 코드를 사용 하 여 DAL s `Update` 메서드는 주소 관련 값이 변경 된 레코드만을 위해 데이터베이스에 `UPDATE` 문을 보냅니다.

또는 전달 된 주소 필드와 데이터베이스 데이터 사이에 차이가 있는지 여부를 추적 하 고, 없는 경우 DAL s `Update` 메서드에 대 한 호출을 무시 하면 됩니다. 이 방법은 db direct 메서드를 다시 사용 하는 경우에 효과적으로 작동 합니다 .이 메서드는 `RowState`를 검사 하 여 데이터베이스 호출이 실제로 필요한 지 여부를 확인할 수 있는 `SuppliersRow` 인스턴스를 전달 하지 않기 때문입니다.

> [!NOTE]
> `UpdateSupplierAddress` 메서드가 호출 될 때마다 업데이트 된 레코드에 대 한 정보를 검색 하기 위해 데이터베이스에 대 한 호출이 수행 됩니다. 그런 다음 데이터를 변경 하는 경우 데이터베이스에 대 한 다른 호출을 수행 하 여 테이블 행을 업데이트 합니다. 이 워크플로는 `BatchUpdate.aspx` 페이지의 *모든* 변경 내용을 포함 하는 `EmployeesDataTable` 인스턴스를 허용 하는 `UpdateSupplierAddress` 메서드 오버 로드를 만들어 최적화할 수 있습니다. 그런 다음 데이터베이스에 대 한 호출을 수행 하 여 `Suppliers` 테이블의 모든 레코드를 가져올 수 있습니다. 그런 다음 두 개의 결과 집합을 열거 하 고 변경 내용이 발생 한 레코드만 업데이트할 수 있습니다.

## <a name="summary"></a>요약

이 자습서에서는 완전히 편집 가능한 DataList를 만드는 방법에 대해 알아보았습니다 .이를 통해 사용자는 여러 공급자의 주소 정보를 빠르게 수정할 수 있습니다. 먼저 DataList s `ItemTemplate`의 공급자 주소, 구/군/시 및 국가 값에 대해 TextBox 웹 컨트롤을 편집 하는 인터페이스를 정의 합니다. 다음에는 DataList의 위와 아래에 모두 업데이트 단추가 추가 되었습니다. 사용자가 변경 내용을 적용 하 고 모두 업데이트 단추를 클릭 하면 `DataListItem` s가 열거 되 고 `SuppliersBLL` 클래스 `UpdateSupplierAddress` 메서드에 대 한 호출이 수행 됩니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Zack Jones 및 켄은 Pespisa입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](an-overview-of-editing-and-deleting-data-in-the-datalist-cs.md)
> [다음](handling-bll-and-dal-level-exceptions-cs.md)
