---
uid: web-forms/overview/data-access/paging-and-sorting/creating-a-customized-sorting-user-interface-cs
title: 사용자 지정 된 정렬 사용자 인터페이스 만들기C#() | Microsoft Docs
author: rick-anderson
description: 정렬 된 데이터의 긴 목록을 표시 하는 경우 구분 기호 행을 도입 하 여 관련 데이터를 그룹화 하는 것이 매우 유용할 수 있습니다. 이 자습서에서는 다음 방법에 대해 알아봅니다.
ms.author: riande
ms.date: 08/15/2006
ms.assetid: 6f81b633-9d01-4e52-ae4a-2ea6bc109475
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/creating-a-customized-sorting-user-interface-cs
msc.type: authoredcontent
ms.openlocfilehash: 93ec07a13de80e4c874ff46b5dfa626b60b632c8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78502709"
---
# <a name="creating-a-customized-sorting-user-interface-c"></a>사용자 지정된 정렬 사용자 인터페이스 만들기(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_27_CS.exe) 또는 [PDF 다운로드](creating-a-customized-sorting-user-interface-cs/_static/datatutorial27cs1.pdf)

> 정렬 된 데이터의 긴 목록을 표시 하는 경우 구분 기호 행을 도입 하 여 관련 데이터를 그룹화 하는 것이 매우 유용할 수 있습니다. 이 자습서에서는 이러한 정렬 사용자 인터페이스를 만드는 방법을 알아봅니다.

## <a name="introduction"></a>소개

정렬 된 열에 몇 개의 다른 값만 있는 경우 정렬 된 데이터의 긴 목록을 표시 하는 경우 최종 사용자는 정확히 차이가 발생 하는 위치를 정확 하 게 파악 하는 것이 어려울 수 있습니다. 예를 들어 데이터베이스에는 81 개의 제품이 있지만 9 개의 범주를 선택할 수 있습니다 (고유 범주 8 개와 `NULL` 옵션). 해산물 범주에 속하는 제품을 검사 하려는 사용자의 경우를 고려 합니다. 단일 GridView의 *모든* 제품을 나열 하는 페이지에서 사용자는 범주를 기준으로 결과를 정렬 하는 것이 가장 좋습니다. 모든 해산물 제품을 함께 그룹화 하는 것이 좋습니다. 범주별로 정렬 한 후에 사용자는 목록을 검색 하 여 해산물 그룹 제품이 시작 및 종료 되는 위치를 확인 해야 합니다. 결과는 범주 이름을 기준으로 사전순으로 정렬 되므로 해산물 제품을 찾는 것은 어렵지 않지만 표에서 항목 목록을 자세히 검색 해야 합니다.

정렬 된 그룹 간의 경계를 강조 하기 위해 많은 웹 사이트에서는 이러한 그룹 사이에 구분 기호를 추가 하는 사용자 인터페이스를 사용 합니다. 그림 1에 표시 된 것과 같은 구분 기호를 사용 하면 사용자가 특정 그룹을 더 빠르게 찾고 해당 경계를 식별할 수 있을 뿐만 아니라 데이터에 존재 하는 고유한 그룹을 확인할 수 있습니다.

[각 범주 그룹을 명확 하 게 식별 ![](creating-a-customized-sorting-user-interface-cs/_static/image2.png)](creating-a-customized-sorting-user-interface-cs/_static/image1.png)

**그림 1**: 각 범주 그룹을 명확 하 게 식별 ([전체 크기 이미지를 보려면 클릭](creating-a-customized-sorting-user-interface-cs/_static/image3.png))

이 자습서에서는 이러한 정렬 사용자 인터페이스를 만드는 방법을 알아봅니다.

## <a name="step-1-creating-a-standard-sortable-gridview"></a>1 단계: 정렬 가능한 표준 GridView 만들기

GridView를 보강 하 여 향상 된 정렬 인터페이스를 제공 하는 방법을 살펴보기 전에 먼저 제품을 나열 하는 정렬 가능한 표준 GridView를 만들어 보겠습니다. 먼저 `PagingAndSorting` 폴더에서 `CustomSortingUI.aspx` 페이지를 엽니다. 페이지에 GridView를 추가 하 고, 해당 `ID` 속성을 `ProductList`로 설정 하 고, 새 ObjectDataSource에 바인딩합니다. `ProductsBLL` 클래스 s `GetProducts()` 메서드를 사용 하 여 레코드를 선택 하도록 ObjectDataSource를 구성 합니다.

그런 다음 `ProductName`, `CategoryName`, `SupplierName`, `UnitPrice` BoundFields 및 단종 된 CheckBoxField 포함 하도록 GridView를 구성 합니다. 마지막으로 GridView의 스마트 태그에서 정렬 사용 확인란을 선택 하 여 (또는 해당 `AllowSorting` 속성을 `true`로 설정) 정렬을 지원 하도록 GridView를 구성 합니다. `CustomSortingUI.aspx` 페이지를 추가 하 고 나면 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](creating-a-customized-sorting-user-interface-cs/samples/sample1.aspx)]

잠시 후 브라우저에서 지금까지 진행 상황을 확인 하세요. 그림 2에서는 데이터를 범주별로 사전순으로 정렬할 때 정렬 가능한 GridView를 보여 줍니다.

[정렬할 수 있는 GridView s 데이터를 범주별로 정렬 ![](creating-a-customized-sorting-user-interface-cs/_static/image5.png)](creating-a-customized-sorting-user-interface-cs/_static/image4.png)

**그림 2**: 정렬 가능한 GridView s 데이터를 범주별로 정렬 ([전체 크기 이미지를 보려면 클릭](creating-a-customized-sorting-user-interface-cs/_static/image6.png))

## <a name="step-2-exploring-techniques-for-adding-the-separator-rows"></a>2 단계: 구분 기호 행을 추가 하는 기술 탐색

정렬할 수 있는 일반 GridView를 사용 하는 경우 각 고유 정렬 된 그룹 앞에 GridView의 구분 기호 행을 추가할 수 있습니다. 그러나 이러한 행을 GridView에 삽입 하려면 어떻게 해야 하나요? 기본적으로 GridView의 행을 반복 하 고 정렬 된 열의 값 간에 차이가 발생 하는 위치를 확인 한 다음 적절 한 구분 기호 행을 추가 해야 합니다. 이 문제에 대해 생각 하는 경우 솔루션이 GridView s `RowDataBound` 이벤트 처리기의 어딘가에 있는 것으로 자연스럽 게 보입니다. [데이터에 따라 사용자 지정 서식 지정](../custom-formatting/custom-formatting-based-upon-data-cs.md) 자습서에서 설명한 대로이 이벤트 처리기는 행 데이터를 기반으로 행 수준 서식을 적용할 때 일반적으로 사용 됩니다. 그러나이 이벤트 처리기에서 프로그래밍 방식으로 GridView에 행을 추가할 수 없으므로 `RowDataBound` 이벤트 처리기는 솔루션이 아닙니다. GridView s `Rows` 컬렉션은 실제로 읽기 전용입니다.

GridView에 행을 추가 하려면 다음 세 가지 옵션 중에서 선택할 수 있습니다.

- GridView에 바인딩된 실제 데이터에 이러한 메타 데이터 구분 기호 행을 추가 합니다.
- GridView를 데이터에 바인딩한 후에 `TableRow` 인스턴스를 GridView 컨트롤 컬렉션에 추가 합니다.
- GridView 컨트롤을 확장 하 고 GridView 구조를 생성 하는 메서드를 재정의 하는 사용자 지정 서버 컨트롤을 만듭니다.

이 기능이 여러 웹 페이지 또는 여러 웹 사이트에 필요한 경우 사용자 지정 서버 컨트롤을 만드는 것이 가장 좋은 방법입니다. 그러나 매우 많은 코드와 GridView의 내부 작동 수준에 대 한 철저 한 탐색이 수반 됩니다. 따라서이 자습서에서는이 옵션을 고려 하지 않습니다.

다른 두 옵션은 GridView에 바인딩되는 실제 데이터에 구분 기호 행을 추가 하 고 GridView의 컨트롤 컬렉션을 조작 하 여 문제를 다르게 공격 하 고 논의 하는 것입니다.

## <a name="adding-rows-to-the-data-bound-to-the-gridview"></a>GridView에 바인딩된 데이터에 행 추가

GridView는 데이터 원본에 바인딩될 때 데이터 원본에서 반환 하는 각 레코드에 대 한 `GridViewRow`를 만듭니다. 따라서 GridView에 바인딩하기 전에 데이터 원본에 구분 기호 레코드를 추가 하 여 필요한 구분 기호 행을 삽입할 수 있습니다. 그림 3에서는 이러한 개념을 보여 줍니다.

![한 가지 방법으로 데이터 원본에 구분 기호 행 추가](creating-a-customized-sorting-user-interface-cs/_static/image7.png)

**그림 3**: 데이터 원본에 구분 기호 행 추가를 포함 하는 한 가지 방법

특별 한 구분 기호가 없으므로 따옴표로 구분 된 용어 구분 기호 레코드를 사용 합니다. 대신 데이터 원본의 특정 레코드가 일반 데이터 행이 아닌 구분 기호로 사용 된다는 플래그를 지정 해야 합니다. 이 예제에서는 `ProductRows`로 구성 된 GridView에 `ProductsDataTable` 인스턴스를 다시 바인딩합니다. `CategoryID` 속성을 `-1`로 설정 하 여 레코드를 구분 기호로 플래그를 설정할 수 있습니다. 이러한 값은 정상적으로 존재할 수 없기 때문입니다.

이 기술을 활용 하기 위해 다음 단계를 수행 해야 합니다.

1. GridView에 바인딩할 데이터를 프로그래밍 방식으로 검색 (`ProductsDataTable` 인스턴스)
2. GridView s `SortExpression`를 기준으로 데이터를 정렬 하 고 `SortDirection` 속성을 설정 합니다.
3. `ProductsDataTable`에서 `ProductsRows`을 반복 하 여 정렬 된 열의 차이가 있는 위치를 찾습니다.
4. 각 그룹 경계에서 DataTable `ProductsRow` 인스턴스를 DataTable에 삽입 합니다. 하나는 `-1` (또는 레코드를 구분 기호로 표시 하도록 결정 된 모든 지정) `CategoryID`.
5. 구분 기호 행을 삽입 한 후 데이터를 프로그래밍 방식으로 GridView에 바인딩합니다.

이러한 다섯 단계 외에도 GridView s `RowDataBound` 이벤트에 대 한 이벤트 처리기를 제공 해야 합니다. 여기서는 각 `DataRow`를 확인 하 고 구분 행 인지 확인 합니다 .이 행은 `CategoryID` 설정이 `-1`되었습니다. 이 경우 셀에 표시 되는 텍스트 서식 또는 텍스트를 조정 하는 것이 좋습니다.

이 기법을 사용 하 여 정렬 그룹 경계를 삽입 하는 데는 GridView s `Sorting` 이벤트에 대 한 이벤트 처리기를 제공 하 고 `SortExpression` 및 `SortDirection` 값을 추적 해야 하므로 위에 설명 된 것 보다 약간 더 많은 작업이 필요 합니다.

## <a name="manipulating-the-gridview-s-control-collection-after-it-s-been-databound"></a>데이터 바인딩된 후 GridView 컨트롤 컬렉션 조작

GridView에 바인딩하기 전에 데이터를 전달 하는 대신 데이터를 GridView에 바인딩한 *후* 에 구분 기호 행을 추가할 수 있습니다. 데이터 바인딩 프로세스는 GridView의 컨트롤 계층 구조를 구성 합니다. 즉, 실제로는 셀 컬렉션으로 구성 된 행의 컬렉션으로 구성 된 `Table` 인스턴스입니다. 특히 GridView의 컨트롤 컬렉션에는 `GridViewRow` (`TableRow` 클래스에서 파생 됨)의 루트에 있는 `Table` 개체와, GridView에 바인딩된 `DataSource`의 각 레코드에 대 한 `TableCell` 개체와 `GridViewRow`의 각 데이터 필드에 대 한 각 `DataSource`인스턴스의 개체가 포함 되어 있습니다.

각 정렬 그룹 사이에 구분 기호 행을 추가 하려면이 컨트롤 계층 구조를 만든 후 직접 조작할 수 있습니다. 페이지를 렌더링 하는 시간을 기준으로 GridView의 컨트롤 계층이 마지막으로 생성 되었음을 확신할 수 있습니다. 따라서이 방법은 `Page` 클래스 `Render` 메서드를 재정의 합니다 .이 시점에서 GridView s 최종 컨트롤 계층 구조가 필요한 구분 기호 행을 포함 하도록 업데이트 됩니다. 그림 4에서는이 프로세스를 보여 줍니다.

[![GridView의 컨트롤 계층 구조를 조작 하는 대체 기술](creating-a-customized-sorting-user-interface-cs/_static/image9.png)](creating-a-customized-sorting-user-interface-cs/_static/image8.png)

**그림 4**: 대체 기술이 GridView의 컨트롤 계층 구조를 조작 ([전체 크기 이미지를 보려면 클릭](creating-a-customized-sorting-user-interface-cs/_static/image10.png))

이 자습서에서는이 두 가지 방법을 사용 하 여 사용자 환경 정렬을 사용자 지정 합니다.

> [!NOTE]
> 이 자습서에서 설명 하는 코드는 [GridView 정렬 그룹화를 사용 하 여 비트를 재생](http://aspadvice.com/blogs/joteke/archive/2006/02/11/15130.aspx)하는 [teemu Keiski](http://aspadvice.com/blogs/joteke/default.aspx) s 블로그 항목에 제공 된 예제를 기반으로 합니다.

## <a name="step-3-adding-the-separator-rows-to-the-gridview-s-control-hierarchy"></a>3 단계: GridView 컨트롤 계층 구조에 구분 기호 행 추가

컨트롤 계층 구조를 만들어 해당 페이지에서 마지막으로 만든 후에는 GridView의 컨트롤 계층에 구분 기호 행만 추가 하려고 하기 때문에 페이지 수명 주기 끝에서, 실제 GridView c 이전에이 추가를 수행 하려고 합니다. o 계층이 HTML로 렌더링 되었습니다. 이 작업을 수행할 수 있는 최신 시점으로, 다음 메서드 시그니처를 사용 하 여 코드 숨김이 클래스에서 재정의할 수 있는 `Page` 클래스 `Render` 이벤트입니다.

[!code-csharp[Main](creating-a-customized-sorting-user-interface-cs/samples/sample2.cs)]

`Page` 클래스의 원래 `Render` 메서드가 `base.Render(writer)` 호출 되 면 페이지의 각 컨트롤이 렌더링 되어 컨트롤 계층 구조를 기반으로 태그가 생성 됩니다. 따라서 페이지가 렌더링 되기 전에 `base.Render(writer)`를 호출 하 고, `base.Render(writer)`를 호출 하기 전에 GridView의 컨트롤 계층 구조를 조작 하는 것이 필수적입니다. 따라서 구분 기호 행이 렌더링 되기 전에 GridView의 컨트롤 계층 구조에 추가 됩니다.

정렬 그룹 헤더를 삽입 하려면 먼저 사용자가 데이터를 정렬 하도록 요청 했는지 확인 해야 합니다. 기본적으로 GridView s의 콘텐츠는 정렬 되지 않으므로 그룹 정렬 헤더를 입력할 필요가 없습니다.

> [!NOTE]
> 페이지가 처음 로드 될 때 특정 열을 기준으로 GridView를 정렬 하려면 첫 번째 페이지에서 GridView s `Sort` 메서드를 호출 합니다 (이후 포스트백의 경우는 제외). 이를 수행 하려면 `if (!Page.IsPostBack)` 조건부 내의 `Page_Load` 이벤트 처리기에이 호출을 추가 합니다. `Sort` 방법에 대 한 자세한 내용은 [보고서 데이터 페이징 및 정렬](paging-and-sorting-report-data-cs.md) 자습서 정보를 참조 하세요.

데이터가 정렬 된 것으로 가정 하면 다음 태스크는 데이터가 정렬 된 열을 확인 한 다음 해당 열 값의 차이를 찾는 행을 검색 하는 것입니다. 다음 코드는 데이터가 정렬 되었는지 확인 하 고 데이터가 정렬 된 기준이 되는 열을 찾습니다.

[!code-csharp[Main](creating-a-customized-sorting-user-interface-cs/samples/sample3.cs)]

GridView를 아직 정렬 하지 않은 경우 GridView s `SortExpression` 속성이 설정 되지 않습니다. 따라서이 속성에 값이 있는 경우에만 구분 기호 행을 추가 하려고 합니다. 이 경우 다음에 데이터를 정렬 하는 기준이 되는 열의 인덱스를 결정 해야 합니다. 이는 GridView의 `Columns` 컬렉션을 반복 하 여 `SortExpression` 속성이 GridView s `SortExpression` 속성과 같은 열을 검색 하는 방식으로 수행 됩니다. 열 s 인덱스 외에도 구분 기호 행을 표시할 때 사용 되는 `HeaderText` 속성을 가져옵니다.

데이터를 정렬 하는 데 사용 되는 열의 인덱스를 사용 하 여 마지막 단계는 GridView의 행을 열거 하는 것입니다. 각 행에 대해 정렬 된 열 값이 이전 행의 정렬 된 열 값과 다른 지 여부를 확인 해야 합니다. 그렇다면 새 `GridViewRow` 인스턴스를 컨트롤 계층 구조에 삽입 해야 합니다. 이 작업은 다음 코드를 사용 하 여 수행 됩니다.

[!code-csharp[Main](creating-a-customized-sorting-user-interface-cs/samples/sample4.cs)]

이 코드는 먼저 GridView s 컨트롤 계층의 루트에 있는 `Table` 개체를 프로그래밍 방식으로 참조 하 고 `lastValue`라는 문자열 변수를 만듭니다. `lastValue`를 사용 하 여 현재 행의 정렬 된 열 값을 이전 행의 값과 비교할 수 있습니다. 그런 다음 GridView s `Rows` 컬렉션을 열거 하 고 각 행에 대해 정렬 된 열의 값이 `currentValue` 변수에 저장 됩니다.

> [!NOTE]
> 특정 행의 정렬 된 열 값을 확인 하려면 셀 `Text` 속성을 사용 합니다. 이는 BoundFields에서 잘 작동 하지만, 템플릿 필드, CheckBoxFields 등에 대해 원하는 대로 작동 하지 않습니다. 대체 GridView 필드를 고려 하는 방법을 살펴보겠습니다.

그런 다음 `currentValue` 및 `lastValue` 변수를 비교 합니다. 서로 다른 경우 컨트롤 계층 구조에 새 구분 기호 행을 추가 해야 합니다. 이렇게 하려면 `Table` 개체의 `Rows` 컬렉션에서 `GridViewRow` 인덱스를 확인 하 고, 새 `GridViewRow` 및 `TableCell` 인스턴스를 만든 다음, `TableCell` 및 `GridViewRow`를 컨트롤 계층 구조에 추가 합니다.

구분 기호 행 s 유일한 `TableCell`은 GridView의 전체 너비에 적용 되 고 `SortHeaderRowStyle` CSS 클래스를 사용 하 여 서식이 지정 되며, 정렬 그룹 이름 (예: 범주) 및 그룹 값 (예: 음료)을 모두 보여 주는 `Text` 속성이 있습니다. 마지막으로 `lastValue` `currentValue`값으로 업데이트 됩니다.

정렬 그룹 머리글 행 `SortHeaderRowStyle`의 서식을 지정 하는 데 사용 되는 CSS 클래스를 `Styles.css` 파일에 지정 해야 합니다. 자유롭게 사용할 수 있는 스타일 설정을 자유롭게 사용할 수 있습니다. 다음을 사용 했습니다.

[!code-css[Main](creating-a-customized-sorting-user-interface-cs/samples/sample5.css)]

현재 코드를 사용 하 여 정렬 인터페이스는 BoundField 정렬할 때 정렬 그룹 헤더를 추가 합니다 (공급 업체 별로 정렬할 때 스크린샷을 보여 주는 그림 5 참조). 그러나 다른 필드 형식 (예: CheckBoxField 또는 Templatefield로 변환)을 기준으로 정렬 하는 경우 정렬 그룹 머리글이 검색 되지 않습니다 (그림 6 참조).

[BoundFields 기준으로 정렬할 때 정렬 인터페이스에 정렬 그룹 머리글이 포함 ![](creating-a-customized-sorting-user-interface-cs/_static/image12.png)](creating-a-customized-sorting-user-interface-cs/_static/image11.png)

**그림 5**: BoundFields 기준으로 정렬할 때 정렬 인터페이스에 정렬 그룹 머리글 포함 ([전체 크기 이미지를 보려면 클릭](creating-a-customized-sorting-user-interface-cs/_static/image13.png))

[CheckBoxField을 정렬할 때 정렬 그룹 헤더가 누락 ![](creating-a-customized-sorting-user-interface-cs/_static/image15.png)](creating-a-customized-sorting-user-interface-cs/_static/image14.png)

**그림 6**: CheckBoxField을 정렬할 때 정렬 그룹 머리글 누락 ([전체 크기 이미지를 보려면 클릭](creating-a-customized-sorting-user-interface-cs/_static/image16.png))

CheckBoxField 정렬할 때 정렬 그룹 머리글이 누락 되는 이유는 코드에서 현재 `TableCell` s `Text` 속성만 사용 하 여 각 행에 대해 정렬 된 열의 값을 결정 하기 때문입니다. CheckBoxFields의 `TableCell` s `Text` 속성은 빈 문자열입니다. 대신 `TableCell` s `Controls` 컬렉션에 있는 CheckBox 웹 컨트롤을 통해 값을 사용할 수 있습니다.

BoundFields 이외의 필드 형식을 처리 하려면 `TableCell` s `Controls` 컬렉션에 CheckBox가 있는지 확인 하기 위해 `currentValue` 변수가 할당 된 코드를 보강 해야 합니다. `currentValue = gvr.Cells[sortColumnIndex].Text`를 사용 하는 대신이 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-a-customized-sorting-user-interface-cs/samples/sample6.cs)]

이 코드는 현재 행에 대 한 정렬 된 열 `TableCell`를 검사 하 여 `Controls` 컬렉션에 컨트롤이 있는지 확인 합니다. 이 있는 경우 첫 번째 컨트롤이 CheckBox 이면 `currentValue` 변수는 CheckBox의 `Checked` 속성에 따라 예 또는 아니요로 설정 됩니다. 그렇지 않으면 `TableCell` s `Text` 속성에서 값을 가져옵니다. GridView에 있을 수 있는 모든 템플릿 필드의 정렬을 처리 하기 위해이 논리를 복제할 수 있습니다.

위의 코드 추가 기능을 사용 하면 더 이상 사용 되지 않는 CheckBoxField 정렬할 때 정렬 그룹 머리글이 표시 됩니다 (그림 7 참조).

[CheckBoxField 정렬할 때 정렬 그룹 머리글이 현재 표시 ![](creating-a-customized-sorting-user-interface-cs/_static/image18.png)](creating-a-customized-sorting-user-interface-cs/_static/image17.png)

**그림 7**: 이제 CheckBoxField을 정렬할 때 정렬 그룹 머리글이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](creating-a-customized-sorting-user-interface-cs/_static/image19.png)).

> [!NOTE]
> `CategoryID`, `SupplierID`또는 `UnitPrice` 필드에 대 한 `NULL` 데이터베이스 값을 포함 하는 제품이 있는 경우 이러한 값은 기본적으로 GridView에 빈 문자열로 표시 됩니다. 즉, `NULL` 값이 있는 해당 제품에 대 한 구분 기호 행 s 텍스트는 category와 같이 표시 됩니다. 즉, 범주 뒤에는 category: 음료와 같이 이름이 없습니다. 여기에 값을 표시 하려는 경우 BoundFields [`NullDisplayText` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.boundfield.nulldisplaytext.aspx) 을 표시 하려는 텍스트로 설정 하거나, `currentValue`를 구분 기호 행의 `Text` 속성에 할당할 때 Render 메서드에서 조건문을 추가할 수 있습니다.

## <a name="summary"></a>요약

GridView에는 정렬 인터페이스를 사용자 지정 하기 위한 여러 가지 기본 제공 옵션이 포함 되어 있지 않습니다. 그러나 약간의 하위 수준 코드를 사용 하는 경우 GridView의 컨트롤 계층 구조를 조정 하 여 더 사용자 지정 된 인터페이스를 만들 수 있습니다. 이 자습서에서는 정렬 가능한 GridView에 대 한 정렬 그룹 구분 기호 행을 추가 하 여 고유 그룹과 해당 그룹 경계를 보다 쉽게 식별 하는 방법을 살펴보았습니다. 사용자 지정 된 정렬 인터페이스의 추가 예를 보려면 [Scott Guthrie](https://weblogs.asp.net/scottgu/) s [ASP.NET 2.0 GridView 정렬 팁과 트릭](https://weblogs.asp.net/scottgu/archive/2006/02/11/437995.aspx) 블로그 항목을 확인 하세요.

행복 한 프로그래밍

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

> [!div class="step-by-step"]
> [이전](sorting-custom-paged-data-cs.md)
> [다음](paging-and-sorting-report-data-vb.md)
