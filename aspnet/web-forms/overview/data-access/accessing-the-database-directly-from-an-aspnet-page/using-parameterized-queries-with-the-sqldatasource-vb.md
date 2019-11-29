---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/using-parameterized-queries-with-the-sqldatasource-vb
title: SqlDataSource와 함께 매개 변수가 있는 쿼리 사용 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 SqlDataSource 컨트롤을 계속 살펴보고 매개 변수가 있는 쿼리를 정의 하는 방법을 알아봅니다. 선언를 모두 지정할 수 있습니다.
ms.author: riande
ms.date: 02/20/2007
ms.assetid: e322f34c-83b7-41ea-ab65-ab1e0bdcc609
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/using-parameterized-queries-with-the-sqldatasource-vb
msc.type: authoredcontent
ms.openlocfilehash: 19b93ff6c0878ae6ed546d347cafef95fd2a01e6
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74597437"
---
# <a name="using-parameterized-queries-with-the-sqldatasource-vb"></a>SqlDataSource와 함께 매개 변수가 있는 쿼리 사용(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_48_VB.exe) 또는 [PDF 다운로드](using-parameterized-queries-with-the-sqldatasource-vb/_static/datatutorial48vb1.pdf)

> 이 자습서에서는 SqlDataSource 컨트롤을 계속 살펴보고 매개 변수가 있는 쿼리를 정의 하는 방법을 알아봅니다. 매개 변수는 선언적으로 프로그래밍 방식으로 지정할 수 있으며 querystring, 세션 상태, 다른 컨트롤 등의 여러 위치에서 끌어올 수 있습니다.

## <a name="introduction"></a>소개

이전 자습서에서는 SqlDataSource 컨트롤을 사용 하 여 데이터베이스에서 직접 데이터를 검색 하는 방법을 살펴보았습니다. 데이터 원본 구성 마법사를 사용 하 여 데이터베이스를 선택한 다음 테이블 또는 뷰에서 반환할 열을 선택 합니다. 사용자 지정 SQL 문을 입력 합니다. 또는 저장 프로시저를 사용 합니다. 테이블이 나 뷰에서 열을 선택 하거나 사용자 지정 SQL 문을 입력 하는 경우에는 SqlDataSource 컨트롤 s `SelectCommand` 속성에 결과 임시 SQL `SELECT` 문이 할당 됩니다 .이 `SELECT`은 SqlDataSource s `Select()` 메서드가 호출 될 때 (프로그래밍 방식으로 또는 데이터 웹 컨트롤에서 자동으로) 실행 되는 문입니다.

이전 자습서 s에서 사용 되는 SQL `SELECT` 문에는 `WHERE` 절이 없습니다. `SELECT` 문에서 `WHERE` 절을 사용 하 여 반환 되는 결과를 제한할 수 있습니다. 예를 들어 제품의 이름을 $50.00 이상으로 표시 하려면 다음 쿼리를 사용할 수 있습니다.

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample1.sql)]

일반적으로 `WHERE` 절에 사용 되는 값은 querystring 값, 세션 변수, 페이지의 웹 컨트롤에 있는 사용자 입력 등의 외부 소스에 의해 결정 됩니다. 이러한 입력은 *매개 변수*를 사용 하 여 지정 하는 것이 가장 좋습니다. Microsoft SQL Server에서 매개 변수는 다음과 같이 `@parameterName`를 사용 하 여 표시 됩니다.

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample2.sql)]

SqlDataSource는 `SELECT` 문과 `INSERT`, `UPDATE`및 `DELETE` 문에 대해 매개 변수가 있는 쿼리를 지원 합니다. 또한 매개 변수 값은 querystring, 세션 상태, 페이지의 컨트롤 등 다양 한 원본에서 자동으로 끌어올 수 있으며 프로그래밍 방식으로 할당 될 수도 있습니다. 이 자습서에서는 매개 변수가 있는 쿼리를 정의 하는 방법 뿐만 아니라 선언적으로 프로그래밍 방식으로 매개 변수 값을 지정 하는 방법에 대해 알아봅니다.

> [!NOTE]
> 이전 자습서에서는 SqlDataSource와 함께 첫 번째 46 자습서를 선택 하 여 개념적 유사성을 나타내는 ObjectDataSource를 비교 했습니다. 이러한 유사성도 매개 변수로 확장 됩니다. 비즈니스 논리 계층의 메서드에 대 한 입력 매개 변수에 매핑된 ObjectDataSource s 매개 변수입니다. SqlDataSource를 사용 하 여 매개 변수는 SQL 쿼리 내에서 직접 정의 됩니다. 두 컨트롤 모두 `Select()`, `Insert()`, `Update()`및 `Delete()` 메서드에 대 한 매개 변수 컬렉션을 포함 하며, 두 컨트롤 모두 미리 정의 된 원본 (querystring 값, 세션 변수 등)에서 채우거 나 프로그래밍 방식으로 할당 된 이러한 매개 변수 값을 가질 수 있습니다.

## <a name="creating-a-parameterized-query"></a>매개 변수가 있는 쿼리 만들기

SqlDataSource 컨트롤 s 데이터 원본 구성 마법사는 데이터베이스 레코드를 검색 하기 위해 실행할 명령을 정의 하는 세 가지 방법을 제공 합니다.

- 기존 테이블 또는 뷰에서 열을 선택 하 여
- 사용자 지정 SQL 문을 입력 하 여 또는
- 저장 프로시저 선택

기존 테이블이 나 뷰에서 열을 선택 하는 경우 `WHERE` 절 추가 대화 상자를 통해 `WHERE` 절의 매개 변수를 지정 해야 합니다. 그러나 사용자 지정 SQL 문을 만들 때 `@parameterName`를 사용 하 여 각 매개 변수를 나타내는 매개 변수를 `WHERE` 절에 직접 입력할 수 있습니다. [저장 프로시저](http://www.awprofessional.com/articles/article.asp?p=25288&amp;rl=1) 는 하나 이상의 SQL 문으로 구성 되며 이러한 문은 매개 변수화 할 수 있습니다. 그러나 SQL 문에 사용 되는 매개 변수는 저장 프로시저에 입력 매개 변수로 전달 되어야 합니다.

매개 변수가 있는 쿼리를 만드는 것은 SqlDataSource s `SelectCommand` 지정 하는 방법에 따라 달라 지므로,는 세 가지 방법을 모두 살펴보겠습니다. 시작 하려면 `SqlDataSource` 폴더에서 `ParameterizedQueries.aspx` 페이지를 열고 SqlDataSource 컨트롤을 도구 상자에서 디자이너로 끌고 `ID`를 `Products25BucksAndUnderDataSource`로 설정 합니다. 그런 다음 컨트롤의 스마트 태그에서 데이터 소스 구성 링크를 클릭 합니다. 사용할 데이터베이스 (`NORTHWINDConnectionString`)를 선택 하 고 다음을 클릭 합니다.

## <a name="step-1-adding-awhereclause-when-picking-the-columns-from-a-table-or-view"></a>1 단계: 테이블이 나 뷰에서 열을 선택할 때`WHERE`절 추가

SqlDataSource 컨트롤을 사용 하 여 데이터베이스에서 반환할 데이터를 선택 하는 경우 데이터 원본 구성 마법사를 사용 하 여 기존 테이블 또는 뷰에서 반환할 열을 선택할 수 있습니다 (그림 1 참조). 이렇게 하면 SqlDataSource s `Select()` 메서드가 호출 될 때 데이터베이스에 전송 되는 SQL `SELECT` 문이 자동으로 빌드됩니다. 이전 자습서에서와 같이 드롭다운 목록에서 Products 테이블을 선택 하 고 `ProductID`, `ProductName`및 `UnitPrice` 열을 확인 합니다.

[테이블이 나 뷰에서 반환할 열을 선택 ![](using-parameterized-queries-with-the-sqldatasource-vb/_static/image1.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image1.png)

**그림 1**: 테이블 또는 뷰에서 반환할 열 선택 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image2.png))

`SELECT` 문에 `WHERE` 절을 포함 하려면 `WHERE` 절 추가 대화 상자를 표시 하는 `WHERE` 단추를 클릭 합니다 (그림 2 참조). `SELECT` 쿼리에서 반환 되는 결과를 제한 하는 매개 변수를 추가 하려면 먼저 열을 선택 하 여 데이터를 필터링 합니다. 그런 다음 필터링에 사용할 연산자 (=, &lt;, &lt;=, &gt;등)를 선택 합니다. 마지막으로 querystring 또는 session 상태에서와 같이 매개 변수 값의 원본을 선택 합니다. 매개 변수를 구성한 후 추가 단추를 클릭 하 여 `SELECT` 쿼리에 포함 합니다.

이 예에서는 `UnitPrice` 값이 $25.00 보다 작거나 같은 결과만 반환 합니다. 따라서 열 드롭다운 목록에서 `UnitPrice`을 선택 하 고 연산자 드롭다운 목록에서 &lt;=를 선택 합니다. 하드 코드 된 매개 변수 값 (예: $25.00)을 사용 하거나 매개 변수 값을 프로그래밍 방식으로 지정 하는 경우 원본 드롭다운 목록에서 없음을 선택 합니다. 그런 다음 값 텍스트 상자 25.00에 하드 코드 된 매개 변수 값을 입력 하 고 추가 단추를 클릭 하 여 프로세스를 완료 합니다.

[WHERE 절 추가 대화 상자에서 반환 된 결과를 제한 ![](using-parameterized-queries-with-the-sqldatasource-vb/_static/image2.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image3.png)

**그림 2**: `WHERE` 절 추가 대화 상자에서 반환 된 결과 제한 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image4.png))

매개 변수를 추가한 후 확인을 클릭 하 여 데이터 원본 구성 마법사로 돌아갑니다. 이제 마법사 아래쪽의 `SELECT` 문에 `@UnitPrice`라는 매개 변수가 있는 `WHERE` 절이 포함 됩니다.

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample3.sql)]

> [!NOTE]
> `WHERE` 절 추가 대화 상자에서 `WHERE` 절에 여러 조건을 지정 하는 경우 마법사는이를 `AND` 연산자와 조인 합니다. `WHERE` 절에 `OR`를 포함 해야 하는 경우 (예: `WHERE UnitPrice <= @UnitPrice OR Discontinued = 1`) 사용자 지정 SQL 문 화면을 통해 `SELECT` 문을 빌드해야 합니다.

SqlDataSource 구성 (다음, 마침을 차례로 클릭)을 완료 한 다음 SqlDataSource의 선언적 태그를 검사 합니다. 태그에는 이제 `SelectCommand`의 매개 변수에 대 한 소스를 출력 하는 `<SelectParameters>` 컬렉션이 포함 되어 있습니다.

[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample4.aspx)]

SqlDataSource s `Select()` 메서드를 호출 하면 `UnitPrice` 매개 변수 값 (25.00)이 데이터베이스로 전송 되기 전에 `SelectCommand`의 `@UnitPrice` 매개 변수에 적용 됩니다. 결과적으로 $25.00 보다 작거나 같은 제품만 `Products` 테이블에서 반환 됩니다. 이를 확인 하려면 GridView를 페이지에 추가 하 고이 데이터 원본에 바인딩한 다음 브라우저를 통해 페이지를 봅니다. 그림 3에서 확인 하는 것 처럼 나열 된 제품만 $25.00 보다 작거나 같아야 합니다.

[$25.00 보다 작거나 같은 제품만 ![표시 됩니다.](using-parameterized-queries-with-the-sqldatasource-vb/_static/image3.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image5.png)

**그림 3**: $25.00 보다 작거나 같은 제품만 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image6.png)).

## <a name="step-2-adding-parameters-to-a-custom-sql-statement"></a>2 단계: 사용자 지정 SQL 문에 매개 변수 추가

사용자 지정 SQL 문을 추가할 때 `WHERE` 절을 명시적으로 입력 하거나 쿼리 작성기의 필터 셀에 값을 지정할 수 있습니다. 이를 보여 주기 위해 s s 1이 특정 임계값 보다 작은 GridView의 제품만 표시 해 보겠습니다. `ParameterizedQueries.aspx` 페이지에 TextBox를 추가 하 여 사용자 로부터이 임계값을 수집 하는 것부터 시작 합니다. TextBox s `ID` 속성을 `MaxPrice`로 설정 합니다. 단추 웹 컨트롤을 추가 하 고 해당 `Text` 속성을 설정 하 여 일치 하는 제품을 표시 합니다.

그런 다음 GridView를 페이지로 끌고 해당 스마트 태그에서 `ProductsFilteredByPriceDataSource`라는 새 SqlDataSource를 만들도록 선택 합니다. 데이터 원본 구성 마법사에서 사용자 지정 SQL 문 또는 저장 프로시저 지정 화면으로 이동 하 여 (그림 4 참조) 다음 쿼리를 입력 합니다.

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample5.sql)]

수동으로 또는 쿼리 작성기를 통해 쿼리를 입력 한 후 다음을 클릭 합니다.

[![매개 변수 값 보다 작거나 같은 제품만 반환 합니다.](using-parameterized-queries-with-the-sqldatasource-vb/_static/image4.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image7.png)

**그림 4**: 매개 변수 값 보다 작거나 같은 제품만 반환 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image8.png))

쿼리에 매개 변수가 포함 되어 있으므로 마법사의 다음 화면에서 매개 변수 값의 원본을 묻는 메시지를 표시 합니다. 매개 변수 원본 드롭다운 목록에서 컨트롤을 선택 하 고 ControlID 드롭다운 목록에서 `MaxPrice` (TextBox 컨트롤 s `ID` 값)을 선택 합니다. 사용자가 `MaxPrice` 텍스트 상자에 텍스트를 입력 하지 않은 경우에 사용할 선택적 기본값을 입력할 수도 있습니다. 이때 기본값을 입력 하지 마십시오.

[MaxPrice TextBox s Text 속성이 매개 변수 원본으로 사용 ![](using-parameterized-queries-with-the-sqldatasource-vb/_static/image5.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image9.png)

**그림 5**: `MaxPrice` TextBox s `Text` 속성은 매개 변수 소스로 사용 됩니다 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image10.png)).

다음, 마침을 차례로 클릭 하 여 데이터 소스 구성 마법사를 완료 합니다. GridView, TextBox, Button 및 SqlDataSource의 선언 태그는 다음과 같습니다.

[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample6.aspx)]

SqlDataSource s `<SelectParameters>` 섹션 내의 매개 변수는 `ControlParameter`이며 `ControlID` 및 `PropertyName`같은 추가 속성을 포함 합니다. SqlDataSource s `Select()` 메서드가 호출 되 면 `ControlParameter`는 지정 된 웹 컨트롤 속성의 값을 가져와 하 고이를 `SelectCommand`의 해당 매개 변수에 할당 합니다. 이 예에서는 `MaxPrice` s Text 속성이 `@MaxPrice` 매개 변수 값으로 사용 됩니다.

잠시 시간을 내 서 브라우저를 통해이 페이지를 봅니다. 페이지를 처음 방문 하거나 `MaxPrice` 텍스트 상자에 값이 없을 때마다 GridView에 레코드가 표시 되지 않습니다.

[MaxPrice TextBox가 비어 있을 때 레코드가 표시 되지 ![](using-parameterized-queries-with-the-sqldatasource-vb/_static/image6.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image11.png)

**그림 6**: `MaxPrice` TextBox가 비어 있을 때 레코드가 표시 되지 않음 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image12.png))

제품이 표시 되지 않는 이유는 기본적으로 매개 변수 값에 대 한 빈 문자열이 데이터베이스 `NULL` 값으로 변환 되기 때문입니다. `[UnitPrice] <= NULL` 비교는 항상 False로 평가 되므로 결과가 반환 되지 않습니다.

텍스트 상자에 값 (예: 5.00)을 입력 하 고 일치 하는 제품 표시 단추를 클릭 합니다. 다시 게시 시 SqlDataSource는 해당 매개 변수 소스 중 하나가 변경 되었음을 GridView에 알립니다. 따라서 GridView는 SqlDataSource에 다시 바인딩되어 $5.00 보다 작거나 같은 제품을 표시 합니다.

[$5.00 보다 작거나 같은 ![제품이 표시 됩니다.](using-parameterized-queries-with-the-sqldatasource-vb/_static/image7.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image13.png)

**그림 7**: $5.00 보다 작거나 같은 제품이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image14.png)).

## <a name="initially-displaying-all-products"></a>처음에 모든 제품 표시

페이지가 처음 로드 될 때 제품을 표시 하지 않고 *모든* 제품을 표시 하는 것이 좋습니다. `MaxPrice` TextBox가 비어 있을 때마다 모든 제품을 나열 하는 한 가지 방법은 Northwind Traders가 $100만을 초과 하는 재고를 보유 하 고 있는 것은 아니기 때문에 100만와 같이 매개 변수의 기본값을 만드세요 high value로 설정 하는 것입니다. 그러나이 방법은 shortsighted 다른 상황에서 작동 하지 않을 수 있습니다.

이전 자습서에서는 [선언적 매개 변수](../basic-reporting/declarative-parameters-vb.md) 및 [DropDownList을 사용 하 여 마스터/세부 정보 필터링](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md) 에서 유사한 문제가 발생 했습니다. Microsoft의 솔루션은이 논리를 비즈니스 논리 계층에 배치 하는 것 이었습니다. 특히, BLL에서 들어오는 값을 검사 하 고 `NULL` 또는 예약 된 값이 있는 경우 호출은 모든 레코드를 반환 하는 DAL 메서드로 라우팅됩니다. 들어오는 값이 표준 필터링 값인 경우 제공 된 값을 사용 하 여 매개 변수가 있는 `WHERE` 절을 사용 하는 SQL 문을 실행 한 DAL 메서드가 호출 됩니다.

아쉽게도 SqlDataSource를 사용할 때 아키텍처를 우회 합니다. 대신 `@MaximumPrice` 매개 변수가 `NULL` 되거나 예약 된 값이 있는 경우 모든 레코드를 지능적으로 가져오는 SQL 문을 사용자 지정 해야 합니다. 이 연습에서는 `@MaximumPrice` 매개 변수가 `-1.0`와 같으면 *모든* 레코드가 반환 됩니다. (`-1.0`에는 음수 `UnitPrice` 값을 가질 수 없으므로 예약 된 값으로 작동 합니다.) 이를 위해 다음 SQL 문을 사용할 수 있습니다.

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample7.sql)]

`@MaximumPrice` 매개 변수가 `-1.0`인 경우이 `WHERE` 절은 *모든* 레코드를 반환 합니다. 매개 변수 값이 `-1.0`되지 않은 경우 `UnitPrice` `@MaximumPrice` 매개 변수 값 보다 작거나 같은 제품만 반환 됩니다. `@MaximumPrice` 매개 변수의 기본값을 `-1.0`로 설정 하면 첫 번째 페이지 로드 (또는 `MaxPrice` TextBox가 비어 있을 때마다)에서 `@MaximumPrice` `-1.0` 값이 표시 되 고 모든 제품이 표시 됩니다.

[![MaxPrice TextBox가 비어 있는 경우 모든 제품이 표시 됩니다.](using-parameterized-queries-with-the-sqldatasource-vb/_static/image8.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image15.png)

**그림 8**: 이제 `MaxPrice` TextBox가 비어 있을 때 모든 제품이 표시 됨 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image16.png))

이 방법에 유의 해야 할 몇 가지 주의 사항이 있습니다. 먼저 SQL 쿼리에서 사용 되는 매개 변수의 데이터 형식을 유추 합니다. `WHERE` 절을 `@MaximumPrice = -1.0`에서 `@MaximumPrice = -1`으로 변경 하면 런타임에서는 매개 변수를 정수로 처리 합니다. 그런 다음 `MaxPrice` 텍스트 상자를 10 진수 값 (예: 5.00)에 할당 하려고 하면 5.00을 정수로 변환할 수 없으므로 오류가 발생 합니다. 이를 해결 하려면 `WHERE` 절에서 `@MaximumPrice = -1.0`를 사용 하 고 있는지 확인 하 고, `ControlParameter` 개체 s `Type` 속성을 10 진수로 설정 합니다.

둘째, `WHERE` 절에 `OR @MaximumPrice = -1.0`를 추가 하 여 쿼리 엔진이 `UnitPrice` (있는 경우)에서 인덱스를 사용할 수 없기 때문에 테이블 스캔이 발생 합니다. 이는 `Products` 테이블에 충분 한 수의 레코드가 있는 경우 성능에 영향을 줄 수 있습니다. 이 논리를 저장 프로시저로 이동 하는 것이 더 효율적입니다. 모든 레코드를 반환 해야 하는 경우에는 `WHERE` 절을 사용 하지 않고 `Products` 테이블에서 `SELECT` 쿼리를 수행 하는 것이 `IF` 문이 `WHERE` 조건을 포함 하 여 인덱스를 사용할 수 있도록 해야 합니다.

## <a name="step-3-creating-and-using-parameterized-stored-procedures"></a>3 단계: 매개 변수화 된 저장 프로시저 만들기 및 사용

저장 프로시저에는 저장 프로시저 내에 정의 된 SQL 문에 사용할 수 있는 입력 매개 변수 집합이 포함 될 수 있습니다. SqlDataSource에서 입력 매개 변수를 허용 하는 저장 프로시저를 사용 하도록 구성 하는 경우 이러한 매개 변수 값은 임시 SQL 문과 동일한 기술을 사용 하 여 지정할 수 있습니다.

SqlDataSource에서 저장 프로시저를 사용 하는 방법을 보여 주기 위해 `GetProductsByCategory`라는 Northwind 데이터베이스에 새 저장 프로시저를 만들어 보겠습니다. 그러면 `@CategoryID` 라는 매개 변수를 수락 하 고 `CategoryID` 열이 `@CategoryID`와 일치 하는 제품의 모든 열을 반환 합니다. 저장 프로시저를 만들려면 서버 탐색기로 이동 하 여 `NORTHWND.MDF` 데이터베이스로 드릴 다운 합니다. 서버 탐색기 표시 되지 않으면 보기 메뉴로 이동 하 여 서버 탐색기 옵션을 선택 합니다.

`NORTHWND.MDF` 데이터베이스에서 저장 프로시저 폴더를 마우스 오른쪽 단추로 클릭 하 고 새 저장 프로시저 추가를 선택 하 고 다음 구문을 입력 합니다.

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample8.sql)]

저장 아이콘 (또는 Ctrl + S)을 클릭 하 여 저장 프로시저를 저장 합니다. 저장 프로시저 폴더에서 마우스 오른쪽 단추를 클릭 하 고 실행을 선택 하 여 저장 프로시저를 테스트할 수 있습니다. 이렇게 하면 저장 프로시저의 매개 변수 (이 인스턴스에서`@CategoryID`)를 입력 하 라는 메시지가 표시 되 고 그 후에 결과가 출력 창에 표시 됩니다.

[@CategoryID 1을 사용 하 여 실행 될 때 GetProductsByCategory 저장 프로시저 ![](using-parameterized-queries-with-the-sqldatasource-vb/_static/image9.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image17.png)

**그림 9**: `@CategoryID` 1을 사용 하 여 실행 되는 `GetProductsByCategory` 저장 프로시저 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image18.png))

에서이 저장 프로시저를 사용 하 여 GridView의 음료 범주에 있는 모든 제품을 표시 하도록 합니다. 새 GridView를 페이지에 추가 하 고 `BeverageProductsDataSource`이라는 새 SqlDataSource에 바인딩합니다. 사용자 지정 SQL 문 또는 저장 프로시저 지정 화면으로 이동 하 여 저장 프로시저 라디오 단추를 선택 하 고 드롭다운 목록에서 `GetProductsByCategory` 저장 프로시저를 선택 합니다.

[드롭다운 목록에서 GetProductsByCategory 저장 프로시저 ![선택 합니다.](using-parameterized-queries-with-the-sqldatasource-vb/_static/image10.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image19.png)

**그림 10**: 드롭다운 목록에서 `GetProductsByCategory` 저장 프로시저 선택 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image20.png))

저장 프로시저는 입력 매개 변수 (`@CategoryID`)를 허용 하므로 다음을 클릭 하 여이 매개 변수 값의 원본을 지정 하 라는 메시지를 표시 합니다. 음료 `CategoryID` 1 이므로 매개 변수 원본 드롭다운 목록을 None으로 두고 DefaultValue 텍스트 상자에 1을 입력 합니다.

[하드 코드 된 값 1을 사용 하 여 음료 범주의 제품을 반환 ![](using-parameterized-queries-with-the-sqldatasource-vb/_static/image11.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image21.png)

**그림 11**: 하드 코드 된 값 1을 사용 하 여 음료 범주의 제품 반환 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image22.png))

다음 선언 태그와 같이 저장 프로시저를 사용할 때 SqlDataSource s `SelectCommand` 속성은 저장 프로시저의 이름으로 설정 되 고 [`SelectCommandType` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.selectcommandtype.aspx) 은 `StoredProcedure`로 설정 되며이는 `SelectCommand`이 임시 SQL 문이 아닌 저장 프로시저의 이름 임을 나타냅니다.

[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample9.aspx)]

브라우저에서 페이지를 테스트 합니다. `GetProductsByCategory` 저장 프로시저가 `Products` 테이블의 모든 열을 반환 하기 때문에 *모든* product 필드가 표시 되기는 하지만 음료 범주에 속하는 제품만 표시 됩니다. 물론 gridview s 열 편집 대화 상자에서 GridView에 표시 되는 필드를 제한 하거나 사용자 지정할 수 있습니다.

[모든 음료를 표시 ![](using-parameterized-queries-with-the-sqldatasource-vb/_static/image12.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image23.png)

**그림 12**: 모든 음료 표시 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image24.png))

## <a name="step-4-programmatically-invoking-a-sqldatasource-sselectstatement"></a>4 단계: 프로그래밍 방식으로 SqlDataSource s`Select()`문 호출

지금까지 이전 자습서 및이 자습서에서 살펴본 예제는 SqlDataSource 컨트롤을 GridView에 직접 바인딩 했습니다. 그러나 SqlDataSource 컨트롤의 데이터를 프로그래밍 방식으로 액세스 하 고 코드에서 열거할 수 있습니다. 이는 데이터를 검사 하기 위해 쿼리 해야 하지만 표시할 필요가 없는 경우에 특히 유용할 수 있습니다. 모든 상용구 ADO.NET 코드를 작성 하 여 데이터베이스에 연결 하 고, 명령을 지정 하 고, 결과를 검색 하는 대신 SqlDataSource가이 단조로운 코드를 처리할 수 있도록 합니다.

프로그래밍 방식으로 SqlDataSource s 데이터를 사용 하는 방법을 설명 하기 위해 상사가 임의로 선택 된 범주 및 관련 제품의 이름을 표시 하는 웹 페이지를 만들도록 요청 하는 것으로 가정 합니다. 즉, 사용자가이 페이지를 방문 하면 `Categories` 테이블에서 임의로 범주를 선택 하 고 범주 이름을 표시 한 다음 해당 범주에 속하는 제품을 나열 하려고 합니다.

이를 위해서는 두 개의 SqlDataSource 컨트롤이 `Categories` 테이블에서 임의의 범주를 잡고 다른 범주를 가져오도록 해야 합니다. 이 단계에서 임의의 범주 레코드를 검색 하는 SqlDataSource를 빌드합니다. 5 단계에서는 범주 제품을 검색 하는 SqlDataSource를 만드는 방법을 살펴봅니다.

`ParameterizedQueries.aspx`에 SqlDataSource를 추가 하 여 시작 하 고 `ID`을 `RandomCategoryDataSource`로 설정 합니다. 다음 SQL 쿼리를 사용 하도록 구성 합니다.

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample10.sql)]

`ORDER BY NEWID()`는 임의의 순서로 정렬 된 레코드를 반환 합니다 ( [`NEWID()`를 사용 하 여 레코드를 임의로 정렬](http://www.sqlteam.com/item.asp?ItemID=8747)). `SELECT TOP 1` 결과 집합에서 첫 번째 레코드를 반환 합니다. 이 쿼리에서는 임의로 선택 된 단일 범주의 `CategoryID` 및 `CategoryName` 열 값을 반환 합니다.

범주 `CategoryName` 값을 표시 하려면 레이블 웹 컨트롤을 페이지에 추가 하 고 해당 `ID` 속성을 `CategoryNameLabel`로 설정 하 고 `Text` 속성을 선택 취소 합니다. SqlDataSource 컨트롤에서 데이터를 프로그래밍 방식으로 검색 하려면 해당 `Select()` 메서드를 호출 해야 합니다. [`Select()` 메서드에](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.select.aspx) 는 데이터를 반환 하기 전에 메시지 하는 방법을 지정 하는 [`DataSourceSelectArguments`](https://msdn.microsoft.com/library/system.web.ui.datasourceselectarguments.aspx)형식의 단일 입력 매개 변수가 필요 합니다. 여기에는 데이터 정렬 및 필터링에 대 한 지침이 포함 될 수 있으며, SqlDataSource 컨트롤의 데이터를 정렬 하거나 페이징할 때 데이터 웹 컨트롤에서 사용 됩니다. 그러나이 예제에서는 데이터를 반환 하기 전에 수정할 필요가 없으므로 `DataSourceSelectArguments.Empty` 개체를 전달 합니다.

`Select()` 메서드는 `IEnumerable`를 구현 하는 개체를 반환 합니다. 반환 되는 정확한 형식은 SqlDataSource 컨트롤의 [`DataSourceMode` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.datasourcemode.aspx)값에 따라 다릅니다. 이전 자습서에서 설명한 대로이 속성은 `DataSet` 또는 `DataReader`값으로 설정할 수 있습니다. `DataSet`로 설정 된 경우 `Select()` 메서드는 [DataView](https://msdn.microsoft.com/library/01s96x0z.aspx) 개체를 반환 합니다. `DataReader`로 설정 된 경우 [`IDataReader`](https://msdn.microsoft.com/library/system.data.idatareader.aspx)를 구현 하는 개체를 반환 합니다. `RandomCategoryDataSource` SqlDataSource는 `DataSourceMode` 속성을 `DataSet` (기본값)로 설정 하므로 DataView 개체를 사용 하 게 됩니다.

다음 코드에서는 `RandomCategoryDataSource` SqlDataSource에서 DataView로 레코드를 검색 하는 방법 뿐만 아니라 첫 번째 DataView 행에서 `CategoryName` 열 값을 읽는 방법을 보여 줍니다.

[!code-vb[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample11.vb)]

`randomCategoryView(0)`는 DataView의 첫 번째 `DataRowView`를 반환 합니다. `randomCategoryView(0)("CategoryName")`는이 첫 번째 행의 `CategoryName` 열 값을 반환 합니다. DataView는 느슨하게 형식화 되어 있습니다. 특정 열 값을 참조 하려면 열 이름을 문자열 (이 경우 범주)로 전달 해야 합니다. 그림 13에서는 페이지를 볼 때 `CategoryNameLabel`에 표시 되는 메시지를 보여 줍니다. 물론 표시 되는 실제 범주 이름은 페이지를 방문할 때마다 (다시 게시 포함) `RandomCategoryDataSource` SqlDataSource에서 임의로 선택 됩니다.

[임의로 선택한 범주 이름을 ![표시 됩니다.](using-parameterized-queries-with-the-sqldatasource-vb/_static/image13.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image25.png)

**그림 13**: 임의로 선택한 범주 이름 표시 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image26.png))

> [!NOTE]
> SqlDataSource 컨트롤 s `DataSourceMode` 속성이 `DataReader`로 설정 된 경우 `Select()` 메서드의 반환 값을 `IDataReader`캐스팅 해야 합니다. 첫 번째 행에서 `CategoryName` 열 값을 읽으려면 다음 코드와 같은 코드를 사용 합니다.

[!code-vb[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample12.vb)]

SqlDataSource가 범주를 임의로 선택 하면 범주 제품을 나열 하는 GridView를 추가할 준비가 된 것입니다.

> [!NOTE]
> 레이블 웹 컨트롤을 사용 하 여 범주 이름을 표시 하는 대신, 페이지에 FormView 또는 DetailsView을 추가 하 여 SqlDataSource에 바인딩하면 됩니다. 그러나 레이블을 사용 하 여 프로그래밍 방식으로 SqlDataSource s `Select()` 문을 호출 하 고 결과 데이터를 코드에서 사용 하는 방법을 탐색할 수 있었습니다.

## <a name="step-5-assigning-parameter-values-programmatically"></a>5 단계: 프로그래밍 방식으로 매개 변수 값 할당

이 자습서에서 지금까지 살펴본 모든 예제는 하드 코드 된 매개 변수 값 또는 미리 정의 된 매개 변수 원본 중 하나에서 가져온 값 (querystring 값, 페이지의 웹 컨트롤 등) 중 하나를 사용 했습니다. 그러나 SqlDataSource 컨트롤의 매개 변수를 프로그래밍 방식으로 설정할 수도 있습니다. 현재 예제를 완료 하려면 지정 된 범주에 속하는 모든 제품을 반환 하는 SqlDataSource가 필요 합니다. 이 SqlDataSource는 `Page_Load` 이벤트 처리기에서 `RandomCategoryDataSource` SqlDataSource에서 반환 된 `CategoryID` 열 값을 기반으로 값을 설정 해야 하는 `CategoryID` 매개 변수를 포함 합니다.

먼저 페이지에 GridView를 추가 하 고이를 `ProductsByCategoryDataSource`라는 새 SqlDataSource에 바인딩합니다. 3 단계에서와 같이 `GetProductsByCategory` 저장 프로시저를 호출 하도록 SqlDataSource를 구성 합니다. 매개 변수 소스 드롭다운 목록을 None으로 설정 된 채로 두고이 기본값을 프로그래밍 방식으로 설정 하므로 기본값을 입력 하지 않습니다.

[매개 변수 소스 또는 기본값을 지정 하지 ![](using-parameterized-queries-with-the-sqldatasource-vb/_static/image14.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image27.png)

**그림 14**: 매개 변수 소스 또는 기본값을 지정 하지 않음 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image28.png))

SqlDataSource 마법사를 완료 한 후 결과 선언 태그는 다음과 같이 표시 됩니다.

[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample13.aspx)]

`Page_Load` 이벤트 처리기에서 프로그래밍 방식으로 `CategoryID` 매개 변수의 `DefaultValue`을 할당할 수 있습니다.

[!code-vb[Main](using-parameterized-queries-with-the-sqldatasource-vb/samples/sample14.vb)]

이 외에도 페이지에는 임의로 선택 된 범주와 관련 된 제품을 보여 주는 GridView가 포함 되어 있습니다.

[매개 변수 소스 또는 기본값을 지정 하지 ![](using-parameterized-queries-with-the-sqldatasource-vb/_static/image15.gif)](using-parameterized-queries-with-the-sqldatasource-vb/_static/image29.png)

**그림 15**: 매개 변수 소스 또는 기본값을 지정 하지 않음 ([전체 크기 이미지를 보려면 클릭](using-parameterized-queries-with-the-sqldatasource-vb/_static/image30.png))

## <a name="summary"></a>요약

SqlDataSource를 사용 하 여 페이지 개발자는 매개 변수 값이 하드 코딩 되거나 미리 정의 된 매개 변수 소스에서 끌어오고 프로그래밍 방식으로 할당 될 수 있는 매개 변수가 있는 쿼리를 정의할 수 있습니다. 이 자습서에서는 임시 SQL 쿼리와 저장 프로시저 모두에 대해 데이터 원본 구성 마법사에서 매개 변수가 있는 쿼리를 작성 하는 방법을 살펴보았습니다. 또한 하드 코드 된 매개 변수 소스와 웹 컨트롤을 매개 변수 소스로 사용 하 고 프로그래밍 방식으로 매개 변수 값을 지정 하는 방법을 살펴보았습니다.

ObjectDataSource와 마찬가지로, SqlDataSource는 기본 데이터를 수정 하는 기능을 제공 합니다. 다음 자습서에서는 SqlDataSource를 사용 하 여 `INSERT`, `UPDATE`및 `DELETE` 문을 정의 하는 방법을 살펴보겠습니다. 이러한 문이 추가 된 후에는 GridView, DetailsView 및 FormView 컨트롤에 내재 된 기능을 기본 제공 하는 삽입, 편집 및 삭제 기능을 활용할 수 있습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Scott Clyde, Randell Schmidt 및 켄은 Pespisa입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](querying-data-with-the-sqldatasource-control-vb.md)
> [다음](inserting-updating-and-deleting-data-with-the-sqldatasource-vb.md)
