---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/inserting-updating-and-deleting-data-with-the-sqldatasource-vb
title: SqlDataSource를 사용 하 여 데이터 삽입, 업데이트 및 삭제 (VB) | Microsoft Docs
author: rick-anderson
description: 이전 자습서에서는 ObjectDataSource 컨트롤이 데이터 삽입, 업데이트 및 삭제를 허용 하는 방법을 배웠습니다. SqlDataSource 컨트롤이 t ...를 지원 합니다.
ms.author: riande
ms.date: 02/20/2007
ms.assetid: 9673bef3-892c-45ba-a7d8-0da3d6f48ec5
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/inserting-updating-and-deleting-data-with-the-sqldatasource-vb
msc.type: authoredcontent
ms.openlocfilehash: 4f7b282b09769272df8ff3a32aa4c509c8917481
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78508337"
---
# <a name="inserting-updating-and-deleting-data-with-the-sqldatasource-vb"></a>SqlDataSource를 사용하여 데이터 삽입, 업데이트 및 삭제(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_49_VB.exe) 또는 [PDF 다운로드](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/datatutorial49vb1.pdf)

> 이전 자습서에서는 ObjectDataSource 컨트롤이 데이터 삽입, 업데이트 및 삭제를 허용 하는 방법을 배웠습니다. SqlDataSource 컨트롤은 같은 작업을 지원 하지만 접근 방식은 서로 다르며,이 자습서에서는 데이터를 삽입, 업데이트 및 삭제 하도록 SqlDataSource를 구성 하는 방법을 보여 줍니다.

## <a name="introduction"></a>소개

[삽입, 업데이트 및 삭제 개요](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)에 설명 된 대로 GridView 컨트롤은 기본 제공 업데이트 및 삭제 기능을 제공 하는 반면, DetailsView 및 FormView 컨트롤은 편집 및 삭제 기능과 함께 삽입 지원을 포함 합니다. 이러한 데이터 수정 기능을 작성 해야 하는 코드 줄을 포함 하지 않고 데이터 소스 컨트롤에 직접 연결할 수 있습니다. ObjectDataSource를 사용 하 여 검사를 삽입, 업데이트 및 삭제 하는 방법에 [대 한 개요는](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md) GridView, DetailsView 및 FormView 컨트롤을 사용 하 여 삽입, 업데이트 및 삭제를 용이 하 게 합니다. 또는 ObjectDataSource 대신에 SqlDataSource를 사용할 수 있습니다.

삽입, 업데이트 및 삭제를 지원 하기 위해, 삽입, 업데이트 또는 삭제 작업을 수행 하기 위해 호출할 개체 계층 메서드를 지정 하는 데 필요한 ObjectDataSource를 사용 하 여 삽입, 업데이트 및 삭제를 지원 합니다. SqlDataSource를 사용 하 여 실행할 SQL 문 (또는 저장 프로시저) `INSERT`, `UPDATE`및 `DELETE`를 제공 해야 합니다. 이 자습서에서 볼 수 있듯이 이러한 문은 수동으로 만들거나 SqlDataSource의 데이터 원본 구성 마법사에서 자동으로 생성할 수 있습니다.

> [!NOTE]
> GridView, DetailsView 및 FormView 컨트롤의 삽입, 편집 및 삭제 기능을 이미 논의 했으므로이 자습서에서는 이러한 작업을 지원 하도록 SqlDataSource 컨트롤을 구성 하는 방법을 집중적으로 설명 합니다. GridView, DetailsView 및 FormView 내에서 이러한 기능을 구현 해야 하는 경우 [삽입, 업데이트 및 삭제 개요](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)부터 시작 하 여 데이터 편집, 삽입 및 삭제 자습서로 돌아갑니다.

## <a name="step-1-specifyinginsertupdate-anddeletestatements"></a>1 단계:`INSERT`,`UPDATE`및`DELETE`문 지정

이전 두 자습서에서 보았듯이 SqlDataSource 컨트롤에서 데이터를 검색 하려면 다음 두 가지 속성을 설정 해야 합니다.

1. `ConnectionString`는 쿼리를 보낼 데이터베이스를 지정 합니다.
2. `SelectCommand`-결과를 반환 하기 위해 실행할 임시 SQL 문이나 저장 프로시저 이름을 지정 합니다.

매개 변수가 있는 `SelectCommand` 값의 경우 매개 변수 값은 SqlDataSource s `SelectParameters` 컬렉션을 통해 지정 되며 하드 코드 된 값, 일반 매개 변수 소스 값 (querystring 필드, 세션 변수, 웹 컨트롤 값 등)을 포함 하거나 프로그래밍 방식으로 할당할 수 있습니다. SqlDataSource 컨트롤 s `Select()` 메서드를 프로그래밍 방식으로 또는 데이터 웹 컨트롤에서 자동으로 호출 하는 경우 데이터베이스에 대 한 연결이 설정 되 고 매개 변수 값이 쿼리에 할당 되 고 명령이 데이터베이스에 shuttled 됩니다. 그런 다음 컨트롤 `DataSourceMode` 속성의 값에 따라 데이터 집합 또는 DataReader로 결과가 반환 됩니다.

데이터를 선택 하는 것과 함께 SqlDataSource 컨트롤을 사용 하 여 `INSERT`, `UPDATE`및 `DELETE` SQL 문을 동일한 방식으로 제공 하 여 데이터를 삽입, 업데이트 및 삭제할 수 있습니다. 실행할 `InsertCommand`, `UpdateCommand`및 `DeleteCommand` 속성을 `INSERT`, `UPDATE`및 `DELETE` SQL 문에 할당 하기만 하면 됩니다. 문에 매개 변수가 있는 경우 (가장 항상 해당) `InsertParameters`, `UpdateParameters`및 `DeleteParameters` 컬렉션에 포함 합니다.

`InsertCommand`, `UpdateCommand`또는 `DeleteCommand` 값이 지정 되 면 해당 데이터 웹 컨트롤의 스마트 태그에서 삽입 사용, 편집 사용 또는 삭제 가능 옵션을 사용할 수 있게 됩니다. 이를 설명 하기 위해, [SqlDataSource 컨트롤을 사용 하 여 데이터 쿼리](querying-data-with-the-sqldatasource-control-vb.md) 자습서에서 만든 `Querying.aspx` 페이지의 예제를 사용 하 고 삭제 기능을 포함 하도록 확장 합니다.

먼저 `InsertUpdateDelete.aspx`를 열고 `SqlDataSource` 폴더에서 페이지 `Querying.aspx` 합니다. `Querying.aspx` 페이지의 디자이너에서 첫 번째 예제 (`ProductsDataSource` 및 `GridView1` 컨트롤)에서 SqlDataSource 및 GridView를 선택 합니다. 두 컨트롤을 선택한 후 편집 메뉴로 이동 하 여 복사를 선택 합니다 (또는 Ctrl + C만 적중). 그런 다음 `InsertUpdateDelete.aspx` 디자이너로 이동 하 여 컨트롤에 붙여넣습니다. `InsertUpdateDelete.aspx`로 두 컨트롤을 이동한 후 브라우저에서 페이지를 테스트 합니다. `Products` 데이터베이스 테이블의 모든 레코드에 대 한 `ProductID`, `ProductName`및 `UnitPrice` 열의 값이 표시 됩니다.

[모든 제품이 나열 되 ![ProductID 순으로 정렬 됩니다.](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image1.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image1.png)

**그림 1**: `ProductID` 기준으로 정렬 된 모든 제품 나열 ([전체 크기 이미지를 보려면 클릭](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image2.png))

## <a name="adding-the-sqldatasource-sdeletecommandanddeleteparametersproperties"></a>SqlDataSource s`DeleteCommand`및`DeleteParameters`속성 추가

이 시점에는 `Products` 테이블의 모든 레코드를 반환 하 고이 데이터를 렌더링 하는 GridView가 있습니다. 여기서의 목표는 사용자가 GridView를 통해 제품을 삭제할 수 있도록이 예제를 확장 하는 것입니다. 이를 수행 하려면 SqlDataSource 컨트롤 `DeleteCommand` 및 `DeleteParameters` 속성 값을 지정 하 고 삭제를 지원 하도록 GridView를 구성 해야 합니다.

`DeleteCommand` 및 `DeleteParameters` 속성은 여러 가지 방법으로 지정할 수 있습니다.

- 선언 구문
- 디자이너의 속성 창에서
- 데이터 원본 구성 마법사의 사용자 지정 SQL 문 또는 저장 프로시저 지정 화면에서
- 데이터 원본 구성 마법사의 뷰 테이블에서 열 지정 화면에 있는 고급 단추를 통해 `DeleteCommand` 및 `DeleteParameters` 속성에 사용 되는 `DELETE` SQL 문 및 매개 변수 컬렉션을 실제로 자동으로 생성 합니다.

2 단계에서 자동으로 `DELETE` 문을 만드는 방법을 살펴보겠습니다. 이제 데이터 소스 구성 마법사 또는 선언적 구문 옵션을 사용할 때에도 디자이너에서 속성 창를 사용 하겠습니다.

`InsertUpdateDelete.aspx`디자이너에서 `ProductsDataSource` SqlDataSource를 클릭 한 다음 속성 창를 표시 합니다. 보기 메뉴에서 속성 창를 선택 하거나 F4를 누르기만 하면 됩니다. 일련의 줄임표를 표시 하는 DeleteQuery 속성을 선택 합니다.

![속성 창에서 DeleteQuery 속성을 선택 합니다.](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image2.gif)

**그림 2**: 속성 창에서 Deletequery 속성을 선택 합니다.

> [!NOTE]
> SqlDataSource에는 DeleteQuery 속성이 없습니다. 대신 DeleteQuery는 `DeleteCommand` 및 `DeleteParameters` 속성의 조합 이며 디자이너를 통해 창을 볼 때 속성 창에만 나열 됩니다. 원본 뷰에서 속성 창를 확인 하는 경우 `DeleteCommand` 속성을 대신 찾을 수 있습니다.

DeleteQuery 속성에서 줄임표를 클릭 하 여 명령 및 매개 변수 편집기 대화 상자를 표시 합니다 (그림 3 참조). 이 대화 상자에서 `DELETE` SQL 문을 지정 하 고 매개 변수를 지정할 수 있습니다. `DELETE` 명령 텍스트 상자에 다음 쿼리를 입력 합니다 (원하는 경우 수동으로 또는 쿼리 작성기를 사용 하 여).

[!code-sql[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/samples/sample1.sql)]

그런 다음 매개 변수 새로 고침 단추를 클릭 하 여 아래 매개 변수 목록에 `@ProductID` 매개 변수를 추가 합니다.

[![속성 창에서 DeleteQuery 속성을 선택 합니다.](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image3.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image3.png)

**그림 3**: 속성 창에서 Deletequery 속성 선택 ([전체 크기 이미지를 보려면 클릭](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image4.png))

이 매개 변수에 대 한 값을 제공 *하지* 마십시오 (매개 변수 소스는 없음). GridView에 대 한 지원 삭제를 추가 하면 GridView는 삭제 단추를 클릭 한 행에 대 한 `DataKeys` 컬렉션 값을 사용 하 여이 매개 변수 값을 자동으로 제공 합니다.

> [!NOTE]
> `DELETE` 쿼리에 사용 되는 매개 변수 이름은 GridView, DetailsView 또는 FormView의 `DataKeyNames` 값 이름과 동일 *해야* 합니다. 즉, `DELETE` 문의 매개 변수는 Products 테이블의 기본 키 열 이름 (즉, GridView의 DataKeyNames 값)이 `ProductID`되기 때문에 `@ID``@ProductID` 대신 의도적으로 이름이 지정 됩니다.

매개 변수 이름과 `DataKeyNames` 값이 일치 하지 않으면 GridView에서 `DataKeys` 컬렉션의 값에 매개 변수를 자동으로 할당할 수 없습니다.

명령 및 매개 변수 편집기 대화 상자에 삭제 관련 정보를 입력 한 후 확인을 클릭 하 고 소스 뷰로 이동 하 여 결과 선언 태그를 검사 합니다.

[!code-aspx[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/samples/sample2.aspx)]

`DeleteCommand` 속성이 추가 되 고 `<DeleteParameters>` 섹션과 `productID`이라는 매개 변수 개체가 추가 됩니다.

## <a name="configuring-the-gridview-for-deleting"></a>삭제할 GridView 구성

`DeleteCommand` 속성이 추가 된 상태에서 GridView s 스마트 태그는 이제 삭제 사용 옵션을 포함 합니다. 계속 진행 하 여이 확인란을 선택 합니다. [삽입, 업데이트 및 삭제 개요](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)에 설명 된 대로 GridView는 `ShowDeleteButton` 속성이 `True`로 설정 된 commandfield를 추가 합니다. 그림 4와 같이 브라우저를 통해 페이지를 방문 하면 삭제 단추가 포함 됩니다. 일부 제품을 삭제 하 여이 페이지를 테스트 합니다.

[이제 각 GridView 행 ![에 삭제 단추가 포함 됩니다.](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image4.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image5.png)

**그림 4**: 각 GridView 행에는 이제 삭제 단추가 포함 됩니다 ([전체 크기 이미지를 보려면 클릭](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image6.png)).

삭제 단추를 클릭 하면 다시 게시가 발생 하 고 GridView는 `ProductID` 매개 변수를 삭제 단추를 클릭 한 행에 대 한 `DataKeys` 컬렉션 값의 값을 할당 하 고 SqlDataSource s `Delete()` 메서드를 호출 합니다. 그런 다음 SqlDataSource 컨트롤은 데이터베이스에 연결 하 고 `DELETE` 문을 실행 합니다. 그러면 GridView가 SqlDataSource에 다시 바인딩되어 현재 제품 집합을 가져오고 표시 합니다. 여기에는 더 이상 삭제 된 레코드가 포함 되지 않습니다.

> [!NOTE]
> GridView는 `DataKeys` 컬렉션을 사용 하 여 SqlDataSource 매개 변수를 채우기 때문에 GridView s `DataKeyNames` 속성은 기본 키를 구성 하는 열로 설정 되 고, SqlDataSource s `SelectCommand`는 이러한 열을 반환 하는 것이 중요 합니다. 또한 SqlDataSource s `DeleteCommand`의 매개 변수 이름이 `@ProductID`으로 설정 되어 있어야 합니다. `DataKeyNames` 속성이 설정 되지 않았거나 매개 변수의 이름이 `@ProductsID`이 아닌 경우 삭제 단추를 클릭 하면 포스트백이 발생 하지만 실제로 레코드는 삭제 되지 않습니다.

그림 5는이 상호 작용을 그래픽으로 보여 줍니다. 데이터 웹 컨트롤에서 삽입, 업데이트 및 삭제와 관련 된 이벤트 체인에 대 한 자세한 내용은 자습서 [삽입, 업데이트 및 삭제와 연결 된 이벤트 검사](../editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-vb.md) 를 다시 참조 하세요.

![GridView에서 삭제 단추를 클릭 하면 SqlDataSource s Delete () 메서드가 호출 됩니다.](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image5.gif)

**그림 5**: GridView에서 삭제 단추를 클릭 하면 SqlDataSource s `Delete()` 메서드가 호출 됩니다.

## <a name="step-2-automatically-generating-theinsertupdate-anddeletestatements"></a>2 단계:`INSERT`,`UPDATE`및`DELETE`문 자동 생성

1 단계를 검사 하면 속성 창 또는 컨트롤의 선언적 구문을 통해 `INSERT`, `UPDATE`및 `DELETE` SQL 문을 지정할 수 있습니다. 그러나이 방법을 사용 하려면 SQL 문을 수동으로 작성 해야 합니다 .이는 단조로운 및 오류가 발생할 수 있습니다. 다행히 데이터 원본 구성 마법사는 뷰 테이블에서 열 지정 화면을 사용 하는 경우 `INSERT`, `UPDATE`및 `DELETE` 문을 자동으로 생성 하는 옵션을 제공 합니다.

에서이 자동 생성 옵션을 살펴보겠습니다. `InsertUpdateDelete.aspx`에서 DetailsView을 디자이너에 추가 하 고 `ID` 속성을 `ManageProducts`로 설정 합니다. 그런 다음, DetailsView의 스마트 태그에서 새 데이터 원본을 만들고 `ManageProductsDataSource`라는 SqlDataSource를 만들도록 선택 합니다.

[ManageProductsDataSource 라는 새 SqlDataSource를 만들 ![](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image6.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image7.png)

**그림 6**: `ManageProductsDataSource` 라는 새 SqlDataSource 만들기 ([전체 크기 이미지를 보려면 클릭](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image8.png))

데이터 원본 구성 마법사에서 `NORTHWINDConnectionString` 연결 문자열을 사용 하도록 선택 하 고 다음을 클릭 합니다. Select 문 구성 화면에서 테이블 또는 뷰에서 열 지정 라디오 단추를 선택 된 상태로 두고 드롭다운 목록에서 `Products` 테이블을 선택 합니다. 확인란 목록에서 `ProductID`, `ProductName`, `UnitPrice`및 `Discontinued` 열을 선택 합니다.

[Products 테이블을 사용 하 여 ![ProductID, ProductName, UnitPrice 및 단종 열을 반환 합니다.](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image7.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image9.png)

**그림 7**: `Products` 테이블을 사용 하 여 `ProductID`, `ProductName`, `UnitPrice`및 `Discontinued` 열 반환 ([전체 크기 이미지를 보려면 클릭](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image10.png))

선택한 테이블 및 열을 기반으로 `INSERT`, `UPDATE`및 `DELETE` 문을 자동으로 생성 하려면 고급 단추를 클릭 하 고 `INSERT`, `UPDATE`및 `DELETE` 문 생성 확인란을 선택 합니다.

![삽입, 업데이트 및 삭제 문 생성 확인란을 선택 합니다.](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image8.gif)

**그림 8**: `INSERT`, `UPDATE`및 `DELETE` 문 생성 확인란을 선택 합니다.

선택 된 테이블에 기본 키가 있고 기본 키 열 (또는 열)이 반환 된 열 목록에 포함 되어 있는 경우에만 `INSERT`, `UPDATE`및 `DELETE` 문 생성 확인란이 선택 가능한 됩니다. 낙관적 동시성 사용 확인란은 `INSERT`생성, `UPDATE`및 `DELETE` 문 생성 확인란이 선택 된 후에 선택할 수 있게 되 고, 결과 `UPDATE` 및 `DELETE` 문에 `WHERE` 절을 확장 하 여 낙관적 동시성 제어를 제공 합니다. 지금은이 확인란을 선택 하지 않은 상태로 둡니다. 다음 자습서에서 SqlDataSource 컨트롤을 사용 하 여 낙관적 동시성을 살펴보겠습니다.

`INSERT`, `UPDATE`및 `DELETE` 문 생성 확인란을 선택 하 고 확인을 클릭 하 여 Select 문 구성 화면으로 돌아간 후 다음을 클릭 하 고 마침을 클릭 하 여 데이터 원본 구성 마법사를 완료 합니다. 마법사가 완료 되 면 Visual Studio는 `ProductID`, `ProductName`및 `UnitPrice` 열에 대해 DetailsView에 BoundFields를 추가 하 고 `Discontinued` 열에 대해 CheckBoxField를 추가 합니다. DetailsView의 스마트 태그에서 페이징 사용 옵션을 선택 하 여이 페이지를 방문 하는 사용자가 제품을 단계별로 실행 하도록 할 수 있습니다. 또한 DetailsView s `Width` 및 `Height` 속성을 지웁니다.

스마트 태그에는 삽입 가능, 편집 가능 및 삭제 옵션 사용이 설정 되어 있습니다. 다음 선언 구문에서 볼 수 있듯이 SqlDataSource에 `InsertCommand`, `UpdateCommand`및 `DeleteCommand`에 대 한 값이 포함 되어 있기 때문입니다.

[!code-aspx[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/samples/sample3.aspx)]

SqlDataSource 컨트롤에 `InsertCommand`, `UpdateCommand`및 `DeleteCommand` 속성에 대해 자동으로 설정 된 값이 있는 경우를 확인 합니다. `InsertCommand` 및 `UpdateCommand` 속성에서 참조 되는 열 집합은 `SELECT` 문의 해당 열을 기반으로 합니다. 즉, `InsertCommand` 및 `UpdateCommand`에 *모든* Products 열을 포함 하는 대신 `ProductID``SelectCommand`에 지정 된 열만 있습니다. 예를 들어이 열은 [`IDENTITY` 열](http://www.sqlteam.com/item.asp?ItemID=102)이므로 값이 편집 될 때 값을 변경할 수 없으며 삽입 시 자동으로 할당 됩니다. 또한 `InsertCommand`, `UpdateCommand`및 `DeleteCommand` 속성의 각 매개 변수에 대해 `InsertParameters`, `UpdateParameters`및 `DeleteParameters` 컬렉션에 해당 하는 매개 변수가 있습니다.

DetailsView의 데이터 수정 기능을 설정 하려면 해당 스마트 태그에서 삽입 사용, 편집 사용 및 삭제 옵션 사용을 선택 합니다. 그러면 `ShowInsertButton`, `ShowEditButton`및 `ShowDeleteButton` 속성이 `True`로 설정 된 CommandField가 추가 됩니다.

브라우저에서 페이지를 방문 하 여 DetailsView에 포함 된 편집, 삭제 및 새로 만들기 단추를 확인 합니다. 편집 단추를 클릭 하면 DetailsView이 편집 모드로 전환 됩니다. 그러면 `ReadOnly` 속성이 `False` (기본값)으로 설정 되 고 CheckBoxField가 checkbox로 설정 된 각 BoundField 표시 됩니다.

[DetailsView s 기본 편집 인터페이스를 ![합니다.](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image9.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image11.png)

**그림 9**: DetailsView s 기본 편집 인터페이스 ([전체 크기 이미지를 보려면 클릭](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image12.png))

마찬가지로, 현재 선택한 제품을 삭제 하거나 시스템에 새 제품을 추가할 수 있습니다. `InsertCommand` 문은 `ProductName`, `UnitPrice`및 `Discontinued` 열 에서만 작동 하기 때문에 다른 열에는 `NULL` 또는 삽입 시 데이터베이스에서 할당 한 기본값이 있습니다. ObjectDataSource와 마찬가지로 `InsertCommand`에 `NULL` s를 허용 하지 않는 데이터베이스 테이블 열이 없는 경우 `INSERT` 문을 실행 하려고 하면 SQL 오류가 발생 합니다.

> [!NOTE]
> DetailsView s 삽입 및 편집 인터페이스는 사용자 지정 또는 유효성 검사를 수행 하지 않습니다. 유효성 검사 컨트롤을 추가 하거나 인터페이스를 사용자 지정 하려면 BoundFields를 템플릿 필드로 변환 해야 합니다. 자세한 내용은 [인터페이스 편집 및 삽입에 유효성 검사 컨트롤 추가](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md) 및 [데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) 을 참조 하세요.

또한 업데이트 및 삭제를 위해 DetailsView은 `DataKeyNames` 속성이 구성 된 경우에만 존재 하는 현재 제품 `DataKey` 값을 사용 합니다. 편집 또는 삭제 작업이 적용 되지 않는 것으로 나타나는 경우 `DataKeyNames` 속성이 설정 되어 있는지 확인 합니다.

## <a name="limitations-of-automatically-generating-sql-statements"></a>SQL 문 자동 생성의 제한 사항

테이블에서 열을 선택 하는 경우에만 `INSERT`, `UPDATE`및 `DELETE` 문 생성 옵션을 사용할 수 있으므로 보다 복잡 한 쿼리를 위해 1 단계에서 했던 것 처럼 사용자 고유의 `INSERT`, `UPDATE`및 `DELETE` 문을 작성 해야 합니다. 일반적으로 SQL `SELECT` 문은 `JOIN`를 사용 하 여 표시를 위해 하나 이상의 조회 테이블에서 데이터를 반환 합니다 (예: 제품 정보를 표시할 때 `Categories` 테이블의 `CategoryName` 필드 다시 가져오기). 동시에 사용자가 핵심 테이블 (이 경우`Products`)에 데이터를 편집, 업데이트 또는 삽입 하도록 허용할 수 있습니다.

`INSERT`, `UPDATE`및 `DELETE` 문을 수동으로 입력할 수 있지만 다음 시간 저장 팁을 고려 하십시오. 처음에는 SqlDataSource를 설정 하 여 `Products` 테이블 에서만 데이터를 다시 가져옵니다. 데이터 원본 구성 마법사 사용 `INSERT`, `UPDATE`및 `DELETE` 문을 자동으로 생성할 수 있도록 테이블 또는 뷰 화면에서 열을 지정 합니다. 그런 다음 마법사를 완료 한 후 속성 창에서 SelectQuery를 구성 하도록 선택 합니다. 또는 데이터 원본 구성 마법사로 돌아가 사용자 지정 SQL 문 또는 저장 프로시저 지정 옵션을 사용 합니다. 그런 다음 `JOIN` 구문을 포함 하도록 `SELECT` 문을 업데이트 합니다. 이 기술은 자동으로 생성 된 SQL 문의 시간 절약 혜택을 제공 하 고 더 많은 사용자 지정 `SELECT` 문을 허용 합니다.

`INSERT`, `UPDATE`및 `DELETE` 문을 자동으로 생성 하는 또 다른 제한 사항은 `INSERT` 및 `UPDATE` 문의 열이 `SELECT` 문에 의해 반환 되는 열을 기반으로 한다는 것입니다. 그러나 더 많거나 더 작은 필드를 업데이트 하거나 삽입 해야 할 수도 있습니다. 예를 들어 2 단계의 예제에서는 `UnitPrice` BoundField를 읽기 전용으로 설정할 수 있습니다. 이 경우 `UpdateCommand`에 표시 되지 않습니다. 또는 GridView에 표시 되지 않는 테이블 필드의 값을 설정 하는 것이 좋습니다. 예를 들어 새 레코드를 추가 하는 경우 `QuantityPerUnit` 값을 TODO로 설정 하는 것이 좋습니다.

이러한 사용자 지정이 필요한 경우에는 속성 창, 마법사에서 사용자 지정 SQL 문 또는 저장 프로시저 지정 옵션을 사용 하거나 선언적 구문을 통해 수동으로 만들어야 합니다.

> [!NOTE]
> 데이터 웹 컨트롤에 해당 필드를 포함 하지 않는 매개 변수를 추가 하는 경우 이러한 매개 변수 값에는 특정 방식으로 값을 할당 해야 한다는 점에 유의 하세요. 이러한 값은 `InsertCommand` 또는 `UpdateCommand`에서 직접 하드 코딩 된 값이 될 수 있습니다. 미리 정의 된 소스 (querystring, 세션 상태, 페이지의 웹 컨트롤 등)에서 가져올 수 있습니다. 이전 자습서에서 살펴본 것 처럼 또는를 프로그래밍 방식으로 할당할 수 있습니다.

## <a name="summary"></a>요약

데이터 웹 컨트롤에서 기본 제공 되는 삽입, 편집 및 삭제 기능을 활용 하기 위해 바인딩된 데이터 소스 컨트롤이 이러한 기능을 제공 해야 합니다. SqlDataSource의 경우 `INSERT`, `UPDATE`및 `DELETE` SQL 문을 `InsertCommand`, `UpdateCommand`및 `DeleteCommand` 속성에 할당 해야 합니다. 이러한 속성 및 해당 매개 변수 컬렉션은 데이터 원본 구성 마법사를 통해 수동으로 추가 하거나 자동으로 생성할 수 있습니다. 이 자습서에서는 두 가지 방법을 모두 살펴보았습니다.

[낙관적 동시성 구현](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md) 자습서에서 ObjectDataSource를 사용 하 여 낙관적 동시성을 사용 하는 것을 검토 했습니다. SqlDataSource 컨트롤은 낙관적 동시성 지원도 제공 합니다. 2 단계에서 설명한 대로 `INSERT`, `UPDATE`및 `DELETE` 문을 자동으로 생성 하는 경우 마법사는 낙관적 동시성 사용 옵션을 제공 합니다. 다음 자습서에서 볼 수 있듯이, SqlDataSource와 함께 낙관적 동시성을 사용 하면 `UPDATE` 및 `DELETE` 문에서 `WHERE` 절을 수정 하 여 데이터를 페이지에 마지막으로 표시 한 이후 다른 열의 값이 변경 되지 않도록 할 수 있습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

> [!div class="step-by-step"]
> [이전](using-parameterized-queries-with-the-sqldatasource-vb.md)
> [다음](implementing-optimistic-concurrency-with-the-sqldatasource-vb.md)
