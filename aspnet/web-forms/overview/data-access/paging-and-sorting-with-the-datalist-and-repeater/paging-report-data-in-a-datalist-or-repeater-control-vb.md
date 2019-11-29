---
uid: web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/paging-report-data-in-a-datalist-or-repeater-control-vb
title: DataList 또는 Repeater 컨트롤의 보고서 데이터 페이징 (VB) | Microsoft Docs
author: rick-anderson
description: DataList 나 Repeater에서 자동 페이징 또는 정렬 지원을 제공 하지 않지만이 자습서에서는 DataList 또는 Repeater에 페이징 지원을 추가 하는 방법을 보여 줍니다,...
ms.author: riande
ms.date: 11/13/2006
ms.assetid: bbd6b7f7-b98a-48b4-93f3-341d6a4f53c0
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/paging-report-data-in-a-datalist-or-repeater-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 5c65ca1f263e41748d99323dbdf1c28fdd077246
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74570018"
---
# <a name="paging-report-data-in-a-datalist-or-repeater-control-vb"></a>DataList 또는 반복기 컨트롤에서 보고서 데이터 페이징(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_44_VB.exe) 또는 [PDF 다운로드](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/datatutorial44vb1.pdf)

> DataList 나 Repeater에서 자동 페이징 또는 정렬 지원을 제공 하지 않지만이 자습서에서는 DataList 또는 Repeater에 페이징 지원을 추가 하 여 훨씬 더 유연한 페이징 및 데이터 표시 인터페이스를 허용 하는 방법을 보여 줍니다.

## <a name="introduction"></a>소개

페이징 및 정렬은 온라인 응용 프로그램에 데이터를 표시 하는 경우 매우 일반적인 두 가지 기능입니다. 예를 들어 온라인 서 점에서 ASP.NET 책을 검색 하는 경우 수백 개의 이러한 책이 있을 수 있지만 검색 결과를 나열 하는 보고서에는 페이지당 10 개의 일치 항목만 나열 됩니다. 또한 제목, 가격, 페이지 수, 작성자 이름 등을 기준으로 결과를 정렬할 수 있습니다. [보고서 데이터 페이징 및 정렬](../paging-and-sorting/paging-and-sorting-report-data-vb.md) 자습서에서 설명한 대로 GridView, DetailsView 및 FormView 컨트롤은 모두 checkbox의 틱에서 사용할 수 있는 기본 제공 페이징 지원을 제공 합니다. GridView에도 정렬 지원이 포함 됩니다.

아쉽게도 DataList 또는 Repeater는 자동 페이징 또는 정렬 지원을 제공 하지 않습니다. 이 자습서에서는 DataList 또는 Repeater에 페이징 지원을 추가 하는 방법을 살펴보겠습니다. 수동으로 페이징 인터페이스를 만들고, 적절 한 레코드 페이지를 표시 하 고, 다시 게시를 통해 페이지를 방문 해야 합니다. 이는 GridView, DetailsView 또는 FormView 보다 더 많은 시간과 코드를 사용 하지만 DataList 및 Repeater를 사용 하면 훨씬 더 유연한 페이징 및 데이터 표시 인터페이스를 사용할 수 있습니다.

> [!NOTE]
> 이 자습서에서는 페이징만 중점적으로 다룹니다. 다음 자습서에서는 정렬 기능을 추가 하는 데 주의를 기울여야 합니다.

## <a name="step-1-adding-the-paging-and-sorting-tutorial-web-pages"></a>1 단계: 페이징 및 정렬 자습서 웹 페이지 추가

이 자습서를 시작 하기 전에 먼저이 자습서에 필요한 ASP.NET 페이지를 추가 해 보겠습니다. `PagingSortingDataListRepeater`이라는 프로젝트에서 새 폴더를 만들어 시작 합니다. 그런 다음이 폴더에 다음 5 개의 ASP.NET 페이지를 추가 하 여 마스터 페이지 `Site.master`를 사용 하도록 구성 된 페이지를 모두 구성 합니다.

- `Default.aspx`
- `Paging.aspx`
- `Sorting.aspx`
- `SortingWithDefaultPaging.aspx`
- `SortingWithCustomPaging.aspx`

![PagingSortingDataListRepeater 폴더를 만들고 자습서 ASP.NET 페이지를 추가 합니다.](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image1.png)

**그림 1**: `PagingSortingDataListRepeater` 폴더 만들기 및 자습서 ASP.NET 페이지 추가

그런 다음 `Default.aspx` 페이지를 열고 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤을 `UserControls` 폴더에서 디자인 화면으로 끌어 옵니다. [마스터 페이지 및 사이트 탐색](../introduction/master-pages-and-site-navigation-vb.md) 자습서에서 만든이 사용자 정의 컨트롤은 사이트 맵을 열거 하 고 현재 섹션의 이러한 자습서를 글머리 기호 목록에 표시 합니다.

[SectionLevelTutorialListing 사용자 정의 컨트롤을 Default.aspx에 추가 ![](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image3.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image2.png)

**그림 2**: `Default.aspx`에 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image4.png))

글머리 기호 목록에 만들 페이징 및 정렬 자습서를 표시 하려면 사이트 맵에 추가 해야 합니다. `Web.sitemap` 파일을 열고 DataList 사이트 맵 노드 마크업을 사용 하 여 편집 및 삭제 후에 다음 태그를 추가 합니다.

[!code-xml[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample1.xml)]

![새 ASP.NET 페이지를 포함 하도록 사이트 맵 업데이트](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image5.png)

**그림 3**: 새 ASP.NET 페이지를 포함 하도록 사이트 맵 업데이트

## <a name="a-review-of-paging"></a>페이징 검토

이전 자습서에서는 GridView, DetailsView 및 FormView 컨트롤의 데이터를 페이징 하는 방법을 살펴보았습니다. 이 세 가지 컨트롤은 컨트롤의 스마트 태그에서 페이징 사용 옵션을 선택 하 여 구현할 수 있는 *기본 페이징* 이라는 간단한 형태의 페이징을 제공 합니다. 기본 페이징을 사용 하면 첫 번째 페이지에서 데이터 페이지를 요청 하거나 사용자가 다른 데이터 페이지로 이동할 때마다 GridView, DetailsView 또는 FormView 컨트롤이 ObjectDataSource의 *모든* 데이터를 다시 요청 합니다. 그런 다음 요청 된 페이지 인덱스와 페이지당 표시할 레코드 수를 지정 하 여 표시할 특정 레코드 집합을 캡처 합니다. [보고서 데이터 페이징 및 정렬](../paging-and-sorting/paging-and-sorting-report-data-vb.md) 자습서에서 기본 페이징에 대해 자세히 설명 했습니다.

기본 페이징은 각 페이지에 대 한 모든 레코드를 다시 요청 하므로 충분히 많은 양의 데이터를 페이징할 때에는 실용적이 지 않습니다. 예를 들어 페이지 크기가 10 인 5만 레코드를 페이징 한다고 가정 합니다. 사용자가 새 페이지로 이동할 때마다 그 중 10 개만 표시 되더라도 데이터베이스에서 5만 레코드를 모두 검색 해야 합니다.

*사용자 지정 페이징은* 요청 된 페이지에 표시할 레코드의 정확한 하위 집합만을 지정 하 여 기본 페이징의 성능 문제를 해결 합니다. 사용자 지정 페이징을 구현할 때는 정확한 레코드 집합만 효율적으로 반환 하는 SQL 쿼리를 작성 해야 합니다. SQL Server 2005 s new [`ROW_NUMBER()` 키워드](http://www.4guysfromrolla.com/webtech/010406-1.shtml) 를 사용 하 여 [많은 양의 데이터 자습서를 효율적으로 페이징](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb.md) 하 여 이러한 쿼리를 만드는 방법을 살펴보았습니다.

DataList 또는 Repeater 컨트롤에서 기본 페이징을 구현 하려면 [`PagedDataSource` 클래스](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.aspx) 를 콘텐츠를 페이징할 `ProductsDataTable` 주위에 래퍼로 사용할 수 있습니다. `PagedDataSource` 클래스에는 열거 가능한 개체에 할당할 수 있는 `DataSource` 속성이 있고, 페이지당 표시할 레코드 수와 현재 페이지 인덱스를 나타내는 [`PageSize`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.pagesize.aspx) 및 [`CurrentPageIndex`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.currentpageindex.aspx) 속성을 포함 합니다. 이러한 속성을 설정한 후에는 `PagedDataSource`를 데이터 웹 컨트롤의 데이터 원본으로 사용할 수 있습니다. 열거 되는 `PagedDataSource`는 `PageSize` 및 `CurrentPageIndex` 속성을 기반으로 내부 `DataSource` 레코드의 적절 한 하위 집합만 반환 합니다. 그림 4는 `PagedDataSource` 클래스의 기능을 보여 줍니다.

![PagedDataSource는 열거 가능한 개체를 페이징할 때 인터페이스로 래핑합니다.](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image6.png)

**그림 4**: `PagedDataSource`는 페이징할 때 사용 가능한 인터페이스로 열거 가능한 개체를 래핑합니다.

`PagedDataSource` 개체는 비즈니스 논리 계층에서 직접 생성 및 구성 하 고 ObjectDataSource 또는 Repeater를 통해 DataList 또는 Repeater에 바인딩할 수 있으며, ASP.NET 페이지의 코드 숨김이 클래스에서 직접 생성 및 구성할 수 있습니다. 후자의 방법을 사용 하는 경우 ObjectDataSource를 사용 하 여은 선형화 하 고 대신 프로그래밍 방식으로 페이지 데이터를 DataList 또는 Repeater에 바인딩해야 합니다.

또한 `PagedDataSource` 개체에는 사용자 지정 페이징을 지 원하는 속성이 있습니다. 그러나 표시할 정확한 레코드를 반환 하는 사용자 지정 페이징을 위해 디자인 된 `ProductsBLL` 클래스에 BLL 메서드가 이미 있기 때문에 사용자 지정 페이징에 `PagedDataSource` 사용을 무시할 수 있습니다.

이 자습서에서는 적절 하 게 구성 된 `PagedDataSource` 개체를 반환 하는 `ProductsBLL` 클래스에 새 메서드를 추가 하 여 DataList에서 기본 페이징을 구현 하는 방법을 살펴보겠습니다. 다음 자습서에서는 사용자 지정 페이징을 사용 하는 방법을 알아봅니다.

## <a name="step-2-adding-a-default-paging-method-in-the-business-logic-layer"></a>2 단계: 비즈니스 논리 계층에서 기본 페이징 메서드 추가

`ProductsBLL` 클래스에는 현재 모든 제품 정보 `GetProducts()` 반환 하는 메서드와 시작 인덱스 `GetProductsPaged(startRowIndex, maximumRows)`에서 특정 제품 하위 집합을 반환 하기 위한 메서드가 있습니다. 기본 페이징을 사용 하는 GridView, DetailsView 및 FormView 컨트롤은 모두 `GetProducts()` 메서드를 사용 하 여 모든 제품을 검색 한 다음, `PagedDataSource`를 내부적으로 사용 하 여 올바른 레코드 하위 집합만 표시 합니다. DataList 및 Repeater 컨트롤과이 기능을 복제 하기 위해이 동작을 모방 하는 새 메서드를 BLL에 만들 수 있습니다.

두 정수 입력 매개 변수를 사용 하는 `GetProductsAsPagedDataSource` 라는 `ProductsBLL` 클래스에 메서드를 추가 합니다.

- 표시할 페이지의 인덱스를 `pageIndex` 하 고 0으로 인덱싱됩니다.
- 페이지당 표시할 레코드 수를 `pageSize` 합니다.

`GetProductsAsPagedDataSource`은 `GetProducts()`의 *모든* 레코드를 검색 하 여 시작 합니다. 그런 다음 `PagedDataSource` 개체를 만들고 해당 `CurrentPageIndex` 및 `PageSize` 속성을 전달 된 `pageIndex` 및 `pageSize` 매개 변수의 값으로 설정 합니다. 이 메서드는 구성 된 `PagedDataSource`을 반환 하 여 종료 됩니다.

[!code-vb[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample2.vb)]

## <a name="step-3-displaying-product-information-in-a-datalist-using-default-paging"></a>3 단계: 기본 페이징을 사용 하 여 DataList에서 제품 정보 표시

`ProductsBLL` 클래스에 추가 된 `GetProductsAsPagedDataSource` 메서드를 사용 하 여 이제 기본 페이징을 제공 하는 DataList 또는 Repeater를 만들 수 있습니다. 먼저 `PagingSortingDataListRepeater` 폴더에서 `Paging.aspx` 페이지를 열고 datalist를 도구 상자에서 디자이너로 끌어와 DataList s `ID` 속성을 `ProductsDefaultPaging`로 설정 합니다. DataList s 스마트 태그에서 `ProductsDefaultPagingDataSource` 라는 새 ObjectDataSource를 만들고 `GetProductsAsPagedDataSource` 메서드를 사용 하 여 데이터를 검색 하도록 구성 합니다.

[ObjectDataSource를 만든 ![GetProductsAsPagedDataSource () 메서드를 사용 하도록 구성 합니다.](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image8.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image7.png)

**그림 5**: ObjectDataSource를 만들고 `GetProductsAsPagedDataSource` `()` 메서드를 사용 하도록 구성 ([전체 크기 이미지를 보려면 클릭](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image9.png))

업데이트, 삽입 및 삭제 탭의 드롭다운 목록을 (없음)로 설정 합니다.

[업데이트, 삽입 및 삭제 탭의 드롭다운 목록을 (없음)으로 설정 ![](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image11.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image10.png)

**그림 6**: 업데이트, 삽입 및 삭제 탭의 드롭다운 목록을 (없음)로 설정 ([전체 크기 이미지를 보려면 클릭](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image12.png))

`GetProductsAsPagedDataSource` 메서드에는 두 개의 입력 매개 변수가 필요 하기 때문에 마법사에서 이러한 매개 변수 값의 원본을 묻는 메시지를 표시 합니다.

페이지 인덱스와 페이지 크기 값은 다시 게시 간에 기억해 야 합니다. 뷰 상태에 저장 하거나, querystring에 보관 하거나, 세션 변수에 저장 하거나, 다른 기술을 사용 하 여 기억 될 수 있습니다. 이 자습서에서는 데이터의 특정 페이지를 책갈피로 허용 하는 장점이 있는 querystring을 사용 합니다.

특히 `pageIndex` 및 `pageSize` 매개 변수에 대 한 querystring 필드 pageIndex 및 pageSize를 각각 사용 합니다 (그림 7 참조). 사용자가이 페이지를 처음 방문할 때 querystring 값이 표시 되지 않으므로이 매개 변수에 대 한 기본값을 설정 합니다. `pageIndex`의 경우 기본값을 0 (첫 번째 데이터 페이지 표시)으로 설정 하 고 `pageSize` 기본값을 4로 설정 합니다.

[문자열 문자열을 pageIndex 및 pageSize 매개 변수의 소스로 사용 ![](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image14.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image13.png)

**그림 7**: `pageIndex`의 소스로 QueryString을 사용 하 고 매개 변수 `pageSize` ([전체 크기 이미지를 보려면 클릭](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image15.png))

ObjectDataSource를 구성한 후 Visual Studio에서 DataList에 대 한 `ItemTemplate`를 자동으로 만듭니다. 제품 이름, 범주 및 공급자만 표시 되도록 `ItemTemplate`를 사용자 지정 합니다. 또한 DataList s `RepeatColumns` 속성을 2로 설정 하 고 `Width`를 100%로 설정 하 고 `ItemStyle` s `Width`를 50%로 설정 합니다. 이러한 너비 설정에는 두 열에 대해 동일한 간격이 지정 됩니다.

이러한 변경을 수행한 후에는 DataList 및 ObjectDataSource s 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample3.aspx)]

> [!NOTE]
> 이 자습서에서는 업데이트 또는 삭제 기능을 수행 하지 않으므로 DataList s 뷰 상태를 사용 하지 않도록 설정 하 여 렌더링 된 페이지 크기를 줄일 수 있습니다.

브라우저를 통해이 페이지를 처음 방문 하는 경우에는 `pageIndex` 및 `pageSize` querystring 매개 변수가 제공 되지 않습니다. 따라서 0과 4의 기본값을 사용 합니다. 그림 8에 나와 있는 것 처럼이로 인해 처음 4 개 제품이 표시 되는 DataList가 생성 됩니다.

[처음 4 개 제품이 나열 ![](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image17.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image16.png)

**그림 8**: 처음 4 개 제품이 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image18.png)).

페이징 인터페이스가 없으면 현재 사용자가 두 번째 데이터 페이지로 이동할 수 있는 방법이 없습니다. 4 단계에서 페이징 인터페이스를 만듭니다. 그러나 지금은 querystring에서 페이징 조건을 직접 지정 하 여 페이징을 수행할 수 있습니다. 예를 들어 두 번째 페이지를 보려면 브라우저의 주소 표시줄에서 URL을 `Paging.aspx` `Paging.aspx?pageIndex=2` 변경 하 고 Enter 키를 누릅니다. 이렇게 하면 두 번째 데이터 페이지가 표시 됩니다 (그림 9 참조).

[데이터의 두 번째 페이지가 표시 ![](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image20.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image19.png)

**그림 9**: 두 번째 데이터 페이지가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image21.png)).

## <a name="step-4-creating-the-paging-interface"></a>4 단계: 페이징 인터페이스 만들기

구현할 수 있는 다양 한 페이징 인터페이스가 있습니다. GridView, DetailsView 및 FormView 컨트롤은 다음 네 가지 인터페이스를 선택할 수 있습니다.

- **그런 다음 이전** 사용자가 한 번에 한 페이지를 다음 또는 이전으로 이동할 수 있습니다.
- Next **, previous, first, last** , Next 및 이전 단추 외에도이 인터페이스에는 첫 번째 및 마지막 페이지로 이동 하는 첫 번째 단추와 마지막 단추가 포함 됩니다.
- **숫자** 페이징 인터페이스의 페이지 번호를 표시 하 여 사용자가 특정 페이지로 빠르게 이동할 수 있도록 합니다.
- 숫자 **, 첫 번째,** 숫자 페이지 번호 외의 마지막에는 처음 또는 매우 최근 페이지로 이동 하는 단추가 포함 되어 있습니다.

DataList 및 Repeater의 경우 페이징 인터페이스를 결정 하 고 구현 하는 일을 담당 합니다. 여기에는 특정 페이징 인터페이스 단추를 클릭할 때 페이지에서 필요한 웹 컨트롤을 만들고 요청 된 페이지를 표시 하는 작업이 포함 됩니다. 또한 특정 페이징 인터페이스 컨트롤을 사용 하지 않도록 설정 해야 할 수도 있습니다. 예를 들어 다음, 이전, 첫 번째 인터페이스를 사용 하 여 첫 번째 데이터 페이지를 볼 때 첫 번째 단추와 이전 단추를 모두 사용 하지 않도록 설정할 수 있습니다.

이 자습서에서는 다음, 이전, 첫 번째 및 마지막 인터페이스를 사용 합니다. 4 개의 단추 웹 컨트롤을 페이지에 추가 하 고 `ID` s를 `FirstPage`, `PrevPage`, `NextPage`및 `LastPage`로 설정 합니다. `Text` 속성을 &lt;&lt; 먼저, &lt; 이전, 다음 &gt;및 마지막 &gt;&gt;으로 설정 합니다.

[!code-aspx[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample4.aspx)]

다음으로 이러한 각 단추에 대 한 `Click` 이벤트 처리기를 만듭니다. 잠시 후 요청 된 페이지를 표시 하는 데 필요한 코드를 추가 합니다.

## <a name="remembering-the-total-number-of-records-being-paged-through"></a>페이징 되는 전체 레코드 수 기억

선택한 페이징 인터페이스에 관계 없이 페이징할 전체 레코드 수를 계산 하 고 기억할 필요가 있습니다. 총 행 수 (페이지 크기와 함께)는 페이징할 데이터 페이지 수를 결정 하며이는 추가 되거나 활성화 된 페이징 인터페이스 컨트롤을 결정 합니다. 빌드 중인 다음, 이전, 첫 번째 인터페이스에서 페이지 수는 두 가지 방법으로 사용 됩니다.

- 마지막 페이지가 표시 되는지 여부를 확인 하려면 다음 및 마지막 단추를 사용할 수 없습니다.
- 사용자가 마지막 단추를 클릭 하면 해당 단추를 마지막 페이지에 whisk 해야 합니다 .이 페이지의 인덱스는 페이지 수보다 하나 낮습니다.

페이지 수는 총 행 개수를 페이지 크기로 나눈 값으로 계산 됩니다. 예를 들어 페이지당 4 개의 레코드를 포함 하는 79 레코드를 페이징 하는 경우 페이지 수는 20 (79/4의 최대값)입니다. 숫자 페이징 인터페이스를 사용 하는 경우이 정보는 표시할 숫자 페이지 단추 수에 대 한 정보를 알려 줍니다. 페이징 인터페이스가 다음 또는 마지막 단추를 포함 하는 경우 페이지 수를 사용 하 여 다음 또는 마지막 단추를 사용 하지 않도록 설정할 시간을 결정 합니다.

페이징 인터페이스가 마지막 단추를 포함 하는 경우 마지막 단추를 클릭할 때 마지막 페이지 인덱스를 확인할 수 있도록 다시 게시 사이에 페이징 되는 전체 레코드 수를 기억해 야 합니다. 이를 용이 하 게 하려면 ASP.NET 페이지 s의 코드 숨김이 클래스에서 해당 값을 보기 상태로 유지 하는 `TotalRowCount` 속성을 만듭니다.

[!code-vb[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample5.vb)]

`TotalRowCount`뿐 아니라 페이지 인덱스, 페이지 크기 및 페이지 수에 쉽게 액세스 하기 위해 읽기 전용 페이지 수준 속성을 만듭니다.

[!code-vb[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample6.vb)]

## <a name="determining-the-total-number-of-records-being-paged-through"></a>페이징할 전체 레코드 수 결정

ObjectDataSource의 하위 집합만 DataList에 표시 되는 경우에도 ObjectDataSource s `Select()` 메서드에서 반환 된 `PagedDataSource` 개체는 *모두* 제품 레코드 내에 있습니다. `PagedDataSource` s [`Count` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.count.aspx) 은 DataList에 표시 되는 항목 수를 반환 합니다. [`DataSourceCount` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.datasourcecount.aspx) 은 `PagedDataSource`내의 총 항목 수를 반환 합니다. 따라서 ASP.NET page s `TotalRowCount` 속성 `PagedDataSource` s `DataSourceCount` 속성 값을 할당 해야 합니다.

이를 수행 하려면 ObjectDataSource s `Selected` 이벤트에 대 한 이벤트 처리기를 만듭니다. `Selected` 이벤트 처리기에서는 ObjectDataSource s `Select()` 메서드의 반환 값 (이 경우 `PagedDataSource`)에 액세스할 수 있습니다.

[!code-vb[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample7.vb)]

## <a name="displaying-the-requested-page-of-data"></a>요청 된 데이터 페이지 표시

사용자가 페이징 인터페이스의 단추 중 하나를 클릭할 때 요청한 데이터 페이지를 표시 해야 합니다. Querystring을 통해 페이징 매개 변수를 지정 하므로 요청한 데이터 페이지를 표시 하기 위해 `Response.Redirect(url)` 사용자의 브라우저에서 적절 한 페이징 매개 변수를 사용 하 여 `Paging.aspx` 페이지를 다시 요청 하도록 합니다. 예를 들어 두 번째 데이터 페이지를 표시 하기 위해 사용자를 `Paging.aspx?pageIndex=1`으로 리디렉션합니다.

이를 용이 하 게 하려면 사용자를 `Paging.aspx?pageIndex=sendUserToPageIndex`로 리디렉션하는 `RedirectUser(sendUserToPageIndex)` 메서드를 만듭니다. 그런 다음 네 가지 단추 `Click` 이벤트 처리기에서이 메서드를 호출 합니다. `FirstPage` `Click` 이벤트 처리기에서 `RedirectUser(0)`를 호출 하 여 첫 번째 페이지로 보냅니다. `PrevPage` `Click` 이벤트 처리기에서 `PageIndex - 1`를 페이지 인덱스로 사용 합니다. 합니다.

[!code-vb[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample8.vb)]

`Click` 이벤트 처리기가 완료 되 면 단추를 클릭 하 여 DataList s 레코드를 페이징할 수 있습니다. 잠시 사용해 보세요!

## <a name="disabling-paging-interface-controls"></a>페이징 인터페이스 컨트롤 사용 안 함

현재 표시 되는 페이지에 관계 없이 네 개의 단추가 모두 활성화 됩니다. 그러나 첫 번째 단추와 이전 단추를 사용 하지 않도록 설정 하 고 마지막 페이지를 표시할 때 다음 및 마지막 단추를 사용 하지 않도록 설정 하려고 합니다. ObjectDataSource s `Select()` 메서드에 의해 반환 되는 `PagedDataSource` 개체에는 데이터의 첫 페이지 또는 마지막 페이지를 볼 수 있는지 확인 하기 위해 검사할 수 있는 속성 [`IsFirstPage`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.isfirstpage.aspx) 및 [`IsLastPage`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.islastpage.aspx) 있습니다.

ObjectDataSource s `Selected` 이벤트 처리기에 다음을 추가 합니다.

[!code-vb[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample9.vb)]

이러한 추가 기능을 사용 하면 첫 번째 페이지를 볼 때 첫 번째 단추와 이전 단추가 비활성화 되 고 마지막 페이지를 볼 때 다음 및 마지막 단추는 비활성화 됩니다.

현재 보고 있는 페이지와 총 페이지 수를 사용자에 게 알리는 방법으로 페이징 인터페이스를 완료 합니다. 레이블 웹 컨트롤을 페이지에 추가 하 고 해당 `ID` 속성을 `CurrentPageNumber`로 설정 합니다. 현재 표시 되는 페이지 (`PageIndex + 1`)와 총 페이지 수 (`PageCount`)를 포함 하도록 ObjectDataSource s 선택한 이벤트 처리기에서 해당 `Text` 속성을 설정 합니다.

[!code-vb[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample10.vb)]

그림 10에는 처음 방문할 때 `Paging.aspx` 표시 됩니다. Querystring이 비어 있으므로 DataList는 기본적으로 처음 4 개 제품을 표시 합니다. 첫 번째 단추와 이전 단추를 사용할 수 없습니다. 다음을 클릭 하면 다음 4 개의 레코드가 표시 됩니다 (그림 11 참조). 이제 첫 번째 단추와 이전 단추가 사용 됩니다.

[데이터의 첫 페이지가 ![표시 됩니다.](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image23.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image22.png)

**그림 10**: 데이터의 첫 페이지가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image24.png)).

[데이터의 두 번째 페이지가 표시 ![](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image26.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image25.png)

**그림 11**: 두 번째 데이터 페이지가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image27.png)).

> [!NOTE]
> 사용자가 페이지당 볼 페이지 수를 지정할 수 있도록 허용 하 여 페이징 인터페이스를 더욱 향상 시킬 수 있습니다. 예를 들어, DropDownList은 5, 10, 25, 50 및 All과 같은 목록 페이지 크기 옵션을 추가할 수 있습니다. 페이지 크기를 선택할 때 사용자가 `Paging.aspx?pageIndex=0&pageSize=selectedPageSize`다시 리디렉션해야 합니다. 이 기능을 독자를 위한 연습으로 구현 해 둡니다.

## <a name="using-custom-paging"></a>사용자 지정 페이징 사용

DataList는 비효율적인 기본 페이징 기술을 사용 하 여 해당 데이터를 통해 페이지를 이동 합니다. 충분 한 양의 데이터를 페이징할 때는 사용자 지정 페이징이 반드시 사용 되어야 합니다. 구현 세부 정보는 약간 다르지만 DataList에서 사용자 지정 페이징의 구현에 대 한 개념은 기본 페이징의 경우와 동일 합니다. 사용자 지정 페이징을 사용 하 여 `ProductBLL` 클래스 `GetProductsPaged` 메서드 (`GetProductsAsPagedDataSource`대신)를 사용 합니다. [많은 양의 데이터를 효율적으로 페이징](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb.md) 자습서에서 설명한 대로 `GetProductsPaged`는 시작 행 인덱스와 반환할 최대 행 수를 전달 해야 합니다. 이러한 매개 변수는 기본 페이징에 사용 되는 `pageIndex` 및 `pageSize` 매개 변수와 마찬가지로 querystring을 통해 유지 관리할 수 있습니다.

사용자 지정 페이징을 사용 하는 `PagedDataSource` 없기 때문에 다른 기술을 사용 하 여 페이징할 수 있는 레코드의 총 수와 데이터의 첫 페이지 또는 마지막 페이지를 다시 표시할지 여부를 결정 해야 합니다. `ProductsBLL` 클래스의 `TotalNumberOfProducts()` 메서드는 페이징 되는 전체 제품 수를 반환 합니다. 데이터의 첫 페이지를 표시 하 고 있는지 확인 하려면 시작 행 인덱스 (0 인 경우)를 확인 한 다음 첫 번째 페이지를 표시 합니다. 시작 행 인덱스와 반환할 최대 행 수가 페이징할 때 마지막 페이지를 확인 하 고 있는 중입니다.

다음 자습서에서는 사용자 지정 페이징의 구현에 대해 더 자세히 살펴보겠습니다.

## <a name="summary"></a>요약

DataList 나 Repeater는 GridView, DetailsView 및 FormView 컨트롤에서 제공 되는 기본 페이징 지원 기능을 제공 하지 않지만 이러한 기능을 최소한의 노력으로 추가할 수 있습니다. 기본 페이징을 구현 하는 가장 쉬운 방법은 `PagedDataSource` 내의 전체 제품 집합을 래핑하고 `PagedDataSource`를 DataList 또는 Repeater에 바인딩하는 것입니다. 이 자습서에서는 `ProductsBLL` 클래스에 `GetProductsAsPagedDataSource` 메서드를 추가 하 여 `PagedDataSource`을 반환 했습니다. `ProductsBLL` 클래스는 사용자 지정 페이징 `GetProductsPaged` 및 `TotalNumberOfProducts`에 필요한 메서드를 이미 포함 하 고 있습니다.

사용자 지정 페이징에 대해 표시할 정확한 레코드 집합을 검색 하거나 기본 페이징에 대 한 `PagedDataSource`의 모든 레코드를 검색 하는 경우에도 페이징 인터페이스를 수동으로 추가 해야 합니다. 이 자습서에서는 네 개의 단추 웹 컨트롤이 포함 된 다음, 이전, 첫 번째 인터페이스를 만들었습니다. 또한 현재 페이지 번호와 총 페이지 수를 표시 하는 레이블 컨트롤이 추가 되었습니다.

다음 자습서에서는 DataList 및 Repeater에 정렬 지원을 추가 하는 방법을 알아봅니다. 또한 기본 및 사용자 지정 페이징을 사용 하는 예제를 사용 하 여 페이징 및 정렬 될 수 있는 DataList를 만드는 방법을 알아봅니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Liz Shulok, 켄은 Pespisa 및 Bernadette Leigh 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](sorting-data-in-a-datalist-or-repeater-control-cs.md)
> [다음](sorting-data-in-a-datalist-or-repeater-control-vb.md)
