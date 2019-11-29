---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/implementing-optimistic-concurrency-with-the-sqldatasource-vb
title: SqlDataSource를 사용 하 여 낙관적 동시성 구현 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 낙관적 동시성 제어의 필수 사항을 검토 한 다음 SqlDataSource 컨트롤을 사용 하 여 구현 하는 방법을 탐색 합니다.
ms.author: riande
ms.date: 02/20/2007
ms.assetid: a8fa72ee-8328-4854-a419-c1b271772303
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/implementing-optimistic-concurrency-with-the-sqldatasource-vb
msc.type: authoredcontent
ms.openlocfilehash: 431734b5245c20ac840147cf0827fa7f8d1e4d17
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598050"
---
# <a name="implementing-optimistic-concurrency-with-the-sqldatasource-vb"></a>SqlDataSource를 사용하여 낙관적 동시성 구현(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_50_VB.exe) 또는 [PDF 다운로드](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/datatutorial50vb1.pdf)

> 이 자습서에서는 낙관적 동시성 제어의 필수 사항을 검토 한 다음 SqlDataSource 컨트롤을 사용 하 여 구현 하는 방법을 탐색 합니다.

## <a name="introduction"></a>소개

앞의 자습서에서는 삽입, 업데이트 및 삭제 기능을 SqlDataSource 컨트롤에 추가 하는 방법을 살펴보았습니다. 간단히 말해서 이러한 기능을 제공 하려면 컨트롤의 `InsertCommand`, `UpdateCommand`또는 `DeleteCommand` 속성에서 해당 하는 `INSERT`, `UPDATE`또는 `DELETE` SQL 문을 `InsertParameters`, `UpdateParameters`및 `DeleteParameters` 컬렉션의 적절 한 매개 변수와 함께 지정 해야 합니다. 이러한 속성 및 컬렉션을 수동으로 지정할 수 있지만 데이터 원본 구성 마법사의 고급 단추를 사용 하면 `SELECT` 문을 기반으로 이러한 문을 자동으로 만들 수 있는 `INSERT`, `UPDATE`및 `DELETE` 문 생성 확인란이 제공 됩니다.

`INSERT`, `UPDATE`및 `DELETE` 문 생성 확인란을 사용 하는 고급 SQL 생성 옵션 대화 상자에는 낙관적 동시성 사용 옵션이 포함 되어 있습니다 (그림 1 참조). 이 확인란을 선택 하면 사용자가 모눈에 데이터를 마지막으로 로드 한 이후 기본 데이터베이스 데이터가 수정 되지 않은 경우에만 자동 생성 된 `UPDATE` 및 `DELETE` 문의 `WHERE` 절이 업데이트 또는 삭제를 수행 하도록 수정 됩니다.

![고급 SQL 생성 옵션 대화 상자에서 낙관적 동시성 지원을 추가할 수 있습니다.](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image1.gif)

**그림 1**: 고급 SQL 생성 옵션 대화 상자에서 낙관적 동시성 지원을 추가할 수 있습니다.

낙관적 [동시성 구현](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md) 자습서로 돌아가서 낙관적 동시성 제어의 기본 사항과 ObjectDataSource에 추가 하는 방법을 살펴보았습니다. 이 자습서에서는 낙관적 동시성 제어의 필수 사항을 재손질 하 고 SqlDataSource를 사용 하 여 구현 하는 방법을 탐색 합니다.

## <a name="a-recap-of-optimistic-concurrency"></a>낙관적 동시성에 대 한 요약

여러 사용자가 동일한 데이터를 편집 하거나 삭제할 수 있도록 하는 웹 응용 프로그램의 경우 한 사용자가 실수로 다른 변경 내용을 덮어쓸 수 있습니다. [낙관적 동시성 구현](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md) 자습서에서 다음 예제를 제공 했습니다.

Jisun 및 Sam 이라는 두 사용자가 모두 응용 프로그램의 페이지를 방문 하 여 방문자가 GridView 컨트롤을 통해 제품을 업데이트 하 고 삭제할 수 있다고 가정 합니다. 둘 다 동시에 Chai에 대 한 편집 단추를 클릭 합니다. Jisun은 제품 이름을 Chai Tea로 변경 하 고 업데이트 단추를 클릭 합니다. Net result는 데이터베이스로 전송 되는 `UPDATE` 문으로, *모든* 제품의 업데이트 가능한 필드 `ProductName`를 설정 합니다 (Jisun은 한 필드만 업데이트 된 경우에도). 이 시점에서 데이터베이스에는이 특정 제품에 대 한 Chai Tea, category 음료, 공급자 Exotic Liquids 등의 값이 있습니다. 그러나 Sam s에서 GridView는 편집 가능한 GridView 행의 제품 이름을 Chai으로 표시 합니다. Jisun 변경이 커밋된 후 몇 초 후에 Sam이 범주를 조미료로 업데이트 하 고 업데이트를 클릭 합니다. 이로 인해 `UPDATE` 문이 제품 이름을 Chai, `CategoryID` 해당 조미료 범주 ID로 설정 하는 데이터베이스로 전송 됩니다. 제품 이름에 대 한 jisun 변경 내용을 덮어썼습니다.

그림 2에서는이 상호 작용을 보여 줍니다.

[두 사용자가 레코드를 동시에 업데이트 하는 경우 ![한 사용자가 다른 사용자의 변경 내용을 덮어쓸 가능성이 있습니다.](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image2.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image1.png)

**그림 2**: 두 사용자가 동시에 레코드를 업데이트 하는 경우 한 사용자가 변경 하 여 다른를 덮어쓸 가능성이 있습니다 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image2.png)).

펼치기에서이 시나리오를 방지 하려면 [동시성 제어](http://en.wikipedia.org/wiki/Concurrency_control) 의 형태를 구현 해야 합니다. [낙관적 동시성](http://en.wikipedia.org/wiki/Optimistic_concurrency_control) 이 자습서에서는 동시성 충돌이 발생할 수 있는 것으로 가정 하 고 이러한 충돌은 거의 발생 하지 않습니다. 따라서 충돌이 발생 하면 낙관적 동시성 제어는 다른 사용자가 동일한 데이터를 수정 했기 때문에 변경 내용을 저장할 수 있음을 사용자에 게 알립니다.

> [!NOTE]
> 많은 동시성 충돌이 있거나 이러한 충돌이 지속할 않는 것으로 간주 되는 응용 프로그램의 경우 비관적 동시성 제어를 대신 사용할 수 있습니다. 비관적 동시성 제어에 대 한 자세한 설명은 [낙관적 동시성 구현](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md) 자습서를 다시 참조 하세요.

낙관적 동시성 제어는 업데이트 또는 삭제 하는 레코드의 값이 업데이트 또는 삭제 프로세스가 시작 된 것과 동일한 지 확인 하는 방식으로 작동 합니다. 예를 들어 편집 가능한 GridView에서 편집 단추를 클릭 하면 레코드의 값이 데이터베이스에서 읽어서 텍스트 상자와 다른 웹 컨트롤에 표시 됩니다. 이러한 원래 값은 GridView에 의해 저장 됩니다. 나중에 사용자가 변경 하 고 업데이트 단추를 클릭 한 후에는 사용 되는 `UPDATE` 문이 원래 값과 새 값을 고려해 야 하며, 사용자가 편집을 시작한 원래 값이 데이터베이스에 있는 값과 동일한 경우에만 기본 데이터베이스 레코드를 업데이트 해야 합니다. 그림 3에서는 이러한 이벤트 시퀀스를 보여 줍니다.

[업데이트 또는 삭제에 대 한 ![성공 하려면 원래 값이 현재 데이터베이스 값과 같아야 합니다.](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image3.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image3.png)

**그림 3**: 업데이트 또는 삭제가 성공 하려면 원래 값이 현재 데이터베이스 값과 같아야 합니다 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image4.png)).

낙관적 동시성을 구현 하는 방법에는 여러 가지가 있습니다 (여러 옵션에 대 한 간략 한 개요는 [Peter Bromberg](http://peterbromberg.net/)의 [낙관적 동시성 업데이트 논리](http://www.eggheadcafe.com/articles/20050719.asp) 참조). SqlDataSource에서 사용 하는 기술 (데이터 액세스 계층에 사용 되는 ADO.NET 형식화 된 데이터 집합)은 모든 원래 값의 비교를 포함 하도록 `WHERE` 절을 보강 합니다. 예를 들어 다음 `UPDATE` 문은 현재 데이터베이스 값이 GridView의 레코드를 업데이트할 때 원래 검색 된 값과 동일한 경우에만 제품의 이름과 가격을 업데이트 합니다. `@ProductName` 및 `@UnitPrice` 매개 변수는 사용자가 입력 한 새 값을 포함 하는 반면 `@original_ProductName` 및 `@original_UnitPrice`에는 편집 단추를 클릭 했을 때 원래 GridView로 로드 된 값이 포함 됩니다.

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample1.sql)]

이 자습서에서 볼 수 있듯이, SqlDataSource를 사용 하 여 낙관적 동시성 제어를 사용 하도록 설정 하는 것은 확인란을 선택 하는 것 만큼 간단 합니다.

## <a name="step-1-creating-a-sqldatasource-that-supports-optimistic-concurrency"></a>1 단계: 낙관적 동시성을 지 원하는 SqlDataSource 만들기

먼저 `SqlDataSource` 폴더에서 `OptimisticConcurrency.aspx` 페이지를 엽니다. SqlDataSource 컨트롤을 도구 상자에서 디자이너로 끌어 `ID` 속성이 `ProductsDataSourceWithOptimisticConcurrency`되도록 설정 합니다. 그런 다음 컨트롤의 스마트 태그에서 데이터 소스 구성 링크를 클릭 합니다. 마법사의 첫 번째 화면에서 `NORTHWINDConnectionString` 작업을 선택 하 고 다음을 클릭 합니다.

[NORTHWINDConnectionString를 사용 하 여 작업 ![선택 합니다.](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image4.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image5.png)

**그림 4**: `NORTHWINDConnectionString` 사용 하도록 선택 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image6.png))

이 예에서는 사용자가 `Products` 테이블을 편집할 수 있도록 하는 GridView를 추가 합니다. 따라서 그림 5와 같이 Select 문 구성 화면의 드롭다운 목록에서 `Products` 테이블을 선택 하 고 `ProductID`, `ProductName`, `UnitPrice`및 `Discontinued` 열을 선택 합니다.

[Products 테이블에서 ![ProductID, ProductName, UnitPrice 및 지원 되지 않는 열을 반환 합니다.](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image5.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image7.png)

**그림 5**: `Products` 테이블에서 `ProductID`, `ProductName`, `UnitPrice`및 `Discontinued` 열 반환 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image8.png))

열을 선택 하 고 고급 단추를 클릭 하 여 고급 SQL 생성 옵션 대화 상자를 표시 합니다. `INSERT`, `UPDATE`및 `DELETE` 문을 생성 하 고 낙관적 동시성 확인란을 선택 하 고 확인을 클릭 합니다 (스크린샷을 보려면 그림 1로 다시 참조). 다음, 마침을 차례로 클릭 하 여 마법사를 완료 합니다.

데이터 원본 구성 마법사를 완료 한 후에는 잠시 후에 결과 `DeleteCommand`를 검사 하 고 속성과 `DeleteParameters` 및 `UpdateParameters` 컬렉션을 `UpdateCommand` 합니다. 이 작업을 수행 하는 가장 쉬운 방법은 왼쪽 아래 모서리의 원본 탭을 클릭 하 여 페이지의 선언 구문을 확인 하는 것입니다. 여기에서 `UpdateCommand` 값을 찾을 수 있습니다.

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample2.sql)]

`UpdateParameters` 컬렉션에 7 개의 매개 변수가 있습니다.

[!code-aspx[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample3.aspx)]

마찬가지로 `DeleteCommand` 속성 및 `DeleteParameters` 컬렉션은 다음과 같습니다.

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample4.sql)]

[!code-aspx[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample5.aspx)]

낙관적 동시성 사용 옵션을 선택 하 여 `UpdateCommand`의 `WHERE` 절을 확대 하 고 속성을 `DeleteCommand` 하 고 해당 매개 변수 컬렉션에 추가 매개 변수를 추가 하는 것 외에도 다음 두 가지 속성을 조정 합니다.

- [`ConflictDetection` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.conflictdetection.aspx) 을 `OverwriteChanges` (기본값)에서로 변경 `CompareAllValues`
- [`OldValuesParameterFormatString` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.oldvaluesparameterformatstring.aspx) 을 {0} (기본값)에서 원래\_{0}로 변경 합니다.

데이터 웹 컨트롤이 SqlDataSource s `Update()` 또는 `Delete()` 메서드를 호출 하면 원래 값이 전달 됩니다. SqlDataSource s `ConflictDetection` 속성이 `CompareAllValues`로 설정 된 경우 이러한 원래 값이 명령에 추가 됩니다. `OldValuesParameterFormatString` 속성은 이러한 원래 값 매개 변수에 사용 되는 명명 패턴을 제공 합니다. 데이터 원본 구성 마법사는 원래\_{0}를 사용 하 고 `UpdateCommand`에서 원래 매개 변수의 이름을 각각, `DeleteCommand` 속성 및 `UpdateParameters` 하 고 컬렉션을 적절 하 게 `DeleteParameters` 합니다.

> [!NOTE]
> SqlDataSource 컨트롤 삽입 기능을 사용 하지 않으므로 `InsertCommand` 속성과 `InsertParameters` 컬렉션을 자유롭게 제거할 수 있습니다.

## <a name="correctly-handlingnullvalues"></a>`NULL`값 올바르게 처리

아쉽게도 낙관적 동시성을 사용 하는 경우 데이터 원본 구성 마법사에서 자동으로 생성 된 확장 `UPDATE` 및 `DELETE` 문은 `NULL` 값이 포함 된 레코드에서 작동 *하지 않습니다* . 그 이유를 확인 하려면 다음 `UpdateCommand`을 수행 하십시오.

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample6.sql)]

`Products` 테이블의 `UnitPrice` 열에는 `NULL` 값이 있을 수 있습니다. 특정 레코드에 `UnitPrice`에 대 한 `NULL` 값이 있는 경우 `NULL = NULL`는 항상 False를 반환 하므로 `WHERE` 절 부분 `[UnitPrice] = @original_UnitPrice`는 *항상* false로 평가 됩니다. 따라서 `NULL` 값을 포함 하는 레코드는 `UPDATE` 및 `DELETE` 문 `WHERE` 절은 업데이트 하거나 삭제할 행을 반환 하지 않으므로 편집 하거나 삭제할 수 없습니다.

> [!NOTE]
> 이 버그는 처음에는 2004의 6 월에 [잘못 된 SQL 문을 생성](https://connect.microsoft.com/VisualStudio/feedback/ViewFeedback.aspx?FeedbackID=93937) 하 고 다음 버전의 ASP.NET에서 수정 하도록 예약 된 따르면에 처음으로 보고 되었습니다.

이 문제를 해결 하려면 `NULL` 값을 가질 수 있는 **모든** 열에 대 한 `UpdateCommand` 및 `DeleteCommand` 속성에서 `WHERE` 절을 수동으로 업데이트 해야 합니다. 일반적으로 `[ColumnName] = @original_ColumnName`를로 변경 합니다.

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample7.sql)]

이 수정은 속성 창의 UpdateQuery 또는 DeleteQuery 옵션을 통해 또는 데이터 구성에서 사용자 지정 SQL 문 또는 저장 프로시저 지정 옵션의 업데이트 및 삭제 탭을 통해 선언적 태그를 통해 직접 만들 수 있습니다. 원본 마법사. 또한 `UpdateCommand` 및 `DeleteCommand` s `WHERE` 절에서 `NULL` 값을 포함할 수 있는 *모든* 열에 대해 이러한 수정 작업을 수행 해야 합니다.

이를 예제에 적용 하면 다음과 같은 수정 된 `UpdateCommand` 및 `DeleteCommand` 값이 생성 됩니다.

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample8.sql)]

## <a name="step-2-adding-a-gridview-with-edit-and-delete-options"></a>2 단계: 편집 및 삭제 옵션을 사용 하 여 GridView 추가

SqlDataSource가 낙관적 동시성을 지원 하도록 구성 된 경우이 동시성 제어를 활용 하는 페이지에 데이터 웹 컨트롤을 추가 하는 것만 남았습니다. 이 자습서에서는 편집 및 삭제 기능을 모두 제공 하는 GridView를 추가 해 보겠습니다. 이렇게 하려면 GridView를 도구 상자에서 디자이너로 끌고 `ID`를 `Products`로 설정 합니다. GridView s 스마트 태그에서 1 단계에서 추가한 `ProductsDataSourceWithOptimisticConcurrency` SqlDataSource 컨트롤에 바인딩합니다. 마지막으로 스마트 태그에서 편집 사용 및 삭제 옵션 사용 옵션을 선택 합니다.

[![GridView에 GridView를 바인딩하고 편집 및 삭제를 사용 하도록 설정 합니다.](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image6.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image9.png)

**그림 6**: SqlDataSource에 GridView 바인딩 및 편집 및 삭제 사용 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image10.png))

GridView를 추가한 후에는 `ProductID` BoundField를 제거 하 고 `ProductName` BoundField s `HeaderText` 속성을 Product로 변경 하 고 `HeaderText` 속성이 간단히 Price가 되도록 `UnitPrice` BoundField를 업데이트 하 여 모양을 구성 합니다. 이상적으로는 `ProductName` 값에 대해 RequiredFieldValidator를 포함 하도록 편집 인터페이스를 개선 하 고 `UnitPrice` 값에 대해 CompareValidator를 포함 하 여 적절 한 형식의 숫자 값을 보장 합니다. GridView의 편집 인터페이스를 사용자 지정 하는 방법에 대 한 자세한 내용은 [데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) 자습서를 참조 하세요.

> [!NOTE]
> Gridview에서 SqlDataSource로 전달 된 원래 값이 뷰 상태에 저장 되므로 GridView의 뷰 상태를 사용 하도록 설정 해야 합니다.

GridView를 수정한 후 GridView 및 SqlDataSource 선언 태그는 다음과 같이 표시 됩니다.

[!code-aspx[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample9.aspx)]

작동 중인 낙관적 동시성 제어를 보려면 두 브라우저 창을 열고 둘 다에서 `OptimisticConcurrency.aspx` 페이지를 로드 합니다. 두 브라우저에서 첫 번째 제품에 대 한 편집 단추를 클릭 합니다. 한 브라우저에서 제품 이름을 변경 하 고 업데이트를 클릭 합니다. 브라우저가 다시 게시 되 고 GridView가 미리 편집 모드로 돌아가 앞서 편집한 레코드의 새 제품 이름을 표시 합니다.

두 번째 브라우저 창에서 가격을 변경 하 고 제품 이름을 원래 값으로 그대로 두고 업데이트를 클릭 합니다. 다시 게시 시 그리드는 미리 편집 모드로 반환 되지만 가격에 대 한 변경 내용은 기록 되지 않습니다. 두 번째 브라우저는 이전 가격과 새 제품 이름 중 첫 번째 값과 동일한 값을 보여 줍니다. 두 번째 브라우저 창에서 변경한 내용이 손실 되었습니다. 뿐만 아니라 동시성 위반이 발생 했다는 것을 나타내는 예외 나 메시지가 없기 때문에 변경 내용이 자동으로 손실 되었습니다.

[두 번째 브라우저 창의 변경 내용이 자동으로 손실 ![](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image7.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image11.png)

**그림 7**: 두 번째 브라우저 창의 변경 내용이 자동으로 손실 됨 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image12.png))

`UPDATE` 문 s `WHERE` 절이 모든 레코드를 필터링 하 여 행에 영향을 주지 않기 때문에 두 번째 브라우저의 변경 내용이 커밋되지 않은 이유는입니다. `UPDATE` 문을 다시 살펴보겠습니다.

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample10.sql)]

두 번째 브라우저 창이 레코드를 업데이트 하면 `WHERE` 절에 지정 된 원래 제품 이름이 첫 번째 브라우저에서 변경 되었으므로 기존 제품 이름과 일치 하지 않습니다. 따라서 문이 `[ProductName] = @original_ProductName` False를 반환 하 고 `UPDATE` 레코드에 영향을 주지 않습니다.

> [!NOTE]
> Delete는 동일한 방식으로 작동 합니다. 두 브라우저 창을 연 상태에서 지정 된 제품을 편집 하 고 변경 내용을 저장 하 여 시작 합니다. 한 브라우저에 변경 내용을 저장 한 후 다른 브라우저에서 동일한 제품에 대 한 삭제 단추를 클릭 합니다. `DELETE` 문 s `WHERE` 절에서 원래 값이 일치 하지 않으므로 삭제는 자동으로 실패 합니다.

두 번째 브라우저 창의 최종 사용자 관점에서 업데이트 단추를 클릭 한 후 그리드는 미리 편집 모드로 반환 되지만 변경 내용은 손실 되었습니다. 그러나 변경 내용이 적용 되지 않은 시각적 피드백은 없습니다. 이상적으로 사용자의 변경 내용이 동시성 위반에 대해 손실 된 경우에는이를 알리고, 표를 편집 모드로 유지 합니다. 이를 수행 하는 방법을 살펴보겠습니다.

## <a name="step-3-determining-when-a-concurrency-violation-has-occurred"></a>3 단계: 동시성 위반이 발생 한 경우 확인

동시성 위반으로 인해 발생 한 변경 내용이 거부 되므로 동시성 위반이 발생 했을 때 사용자에 게 경고 하는 것이 좋습니다. 사용자에 게 경고를 표시 하려면 `ConcurrencyViolationMessage` 페이지 맨 위에 레이블 웹 컨트롤을 추가 합니다. `Text` 속성이 다음 메시지를 표시 합니다. 다른 사용자가 동시에 업데이트 한 레코드를 업데이트 하거나 삭제 하려고 했습니다. 다른 사용자의 변경 내용을 검토 한 다음 업데이트 또는 삭제를 다시 실행 하십시오. 레이블 컨트롤 s `CssClass` 속성을 경고로 설정 합니다 .이 클래스는 빨강, 기울임꼴, 굵은 글꼴 및 크게 텍스트를 표시 하는 `Styles.css`에 정의 된 CSS 클래스입니다. 마지막으로 `Visible` 레이블 및 `EnableViewState` 속성을 `False`로 설정 합니다. 이렇게 하면 명시적으로 `Visible` 속성을 `True`로 설정 하는 포스트백만 제외 하 고 레이블이 숨겨집니다.

[경고를 표시 하는 레이블 컨트롤을 페이지에 추가 ![](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image8.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image13.png)

**그림 8**: 페이지에 레이블 컨트롤을 추가 하 여 경고 표시 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image14.png))

업데이트 또는 삭제를 수행 하는 경우 데이터 소스 제어에서 요청 된 업데이트 또는 삭제를 수행한 후 GridView s `RowUpdated` 및 `RowDeleted` 이벤트 처리기가 발생 합니다. 이러한 이벤트 처리기에서 작업의 영향을 받은 행 수를 확인할 수 있습니다. 0 개 행이 영향을 받는 경우 `ConcurrencyViolationMessage` 레이블을 표시 하려고 합니다.

`RowUpdated` 및 `RowDeleted` 이벤트 모두에 대 한 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-vb[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample11.vb)]

두 이벤트 처리기 모두 `e.AffectedRows` 속성을 확인 하 고, 0과 같으면 `ConcurrencyViolationMessage` 레이블 s `Visible` 속성을 `True`로 설정 합니다. 또한 `RowUpdated` 이벤트 처리기에서 `KeepInEditMode` 속성을 true로 설정 하 여 GridView에 편집 모드를 유지 하도록 지시 합니다. 이렇게 하려면 다른 사용자의 데이터가 편집 인터페이스에 로드 되도록 데이터를 모눈에 다시 바인딩해야 합니다. 이는 GridView s `DataBind()` 메서드를 호출 하 여 수행 됩니다.

그림 9와 같이이 두 이벤트 처리기를 사용 하면 동시성 위반이 발생할 때마다 매우 눈에 띄는 메시지가 표시 됩니다.

[동시성 위반이 발생 한 경우 메시지를 표시 ![](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image9.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image15.png)

**그림 9**: 동시성 위반이 발생 한 경우 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image16.png)) 메시지가 표시 됨

## <a name="summary"></a>요약

여러 사용자가 동시에 동일한 데이터를 편집할 수 있는 웹 응용 프로그램을 만들 때 동시성 제어 옵션을 고려해 야 합니다. 기본적으로 ASP.NET 데이터 웹 컨트롤과 데이터 소스 컨트롤은 동시성 제어를 사용 하지 않습니다. 이 자습서에서 살펴본 것 처럼 SqlDataSource를 사용 하 여 낙관적 동시성 제어를 구현 하는 것은 비교적 빠르고 간단 합니다. SqlDataSource는 추가 `WHERE` 절을 자동 생성 된 `UPDATE` 및 `DELETE` 문에 추가 하는 데 필요한 대부분의 투자할를 처리 하지만 `NULL` 값을 올바르게 처리 하는 방법 섹션에서 설명 하는 것 처럼 `NULL` 값 열을 처리할 때 약간의 미묘한 내용이 있습니다.

이 자습서에서는 SqlDataSource 검사를 마칩니다. 나머지 자습서에서는 ObjectDataSource 및 계층화 된 아키텍처를 사용 하 여 데이터 작업으로 돌아갑니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

> [!div class="step-by-step"]
> [이전](inserting-updating-and-deleting-data-with-the-sqldatasource-vb.md)
