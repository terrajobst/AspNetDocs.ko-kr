---
uid: web-forms/overview/data-access/paging-and-sorting/paging-and-sorting-report-data-cs
title: 보고서 데이터 페이징 및 정렬 (C#) | Microsoft Docs
author: rick-anderson
description: 페이징 및 정렬은 온라인 응용 프로그램에 데이터를 표시 하는 경우 매우 일반적인 두 가지 기능입니다. 이 자습서에서는 정렬을 추가 하는 방법에 대해 살펴보겠습니다.
ms.author: riande
ms.date: 08/15/2006
ms.assetid: 811a6ef2-ec66-4c8e-a089-6f795056e288
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/paging-and-sorting-report-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 2f77040316dadc218b8183e52628dc0cfe3b35a1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78502301"
---
# <a name="paging-and-sorting-report-data-c"></a>페이징 및 정렬 보고서 데이터(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_24_CS.exe) 또는 [PDF 다운로드](paging-and-sorting-report-data-cs/_static/datatutorial24cs1.pdf)

> 페이징 및 정렬은 온라인 응용 프로그램에 데이터를 표시 하는 경우 매우 일반적인 두 가지 기능입니다. 이 자습서에서는 보고서에 대 한 정렬 및 페이징을 추가 하는 방법에 대해 설명 합니다 .이에 대해서는 향후 자습서에서 살펴보겠습니다.

## <a name="introduction"></a>소개

페이징 및 정렬은 온라인 응용 프로그램에 데이터를 표시 하는 경우 매우 일반적인 두 가지 기능입니다. 예를 들어 온라인 서 점에서 ASP.NET 책을 검색 하는 경우 수백 개의 이러한 책이 있을 수 있지만 검색 결과를 나열 하는 보고서에는 페이지당 10 개의 일치 항목만 나열 됩니다. 또한 제목, 가격, 페이지 수, 작성자 이름 등을 기준으로 결과를 정렬할 수 있습니다. 지난 23 개의 자습서에서는 데이터를 추가, 편집 및 삭제 하는 데 사용할 수 있는 인터페이스를 포함 하 여 다양 한 보고서를 작성 하는 방법을 살펴보았습니다. 그러나 DetailsView 및 FormView를 사용 하 여 데이터를 정렬 하는 방법에 대해서는 살펴보았습니다. 제어가.

이 자습서에서는 몇 가지 확인란을 선택 하 여 수행할 수 있는 보고서에 정렬과 페이징을 추가 하는 방법에 대해 알아봅니다. 불행 하 게도이 간단한 구현에서는 정렬 인터페이스가 약간의 단점을 유지 하 고 페이징 루틴이 많은 결과 집합을 효율적으로 페이징할 수 있도록 설계 되지 않았습니다. 이후 자습서에서는 기본 페이징 및 정렬 솔루션의 제한 사항을 해결 하는 방법을 알아봅니다.

## <a name="step-1-adding-the-paging-and-sorting-tutorial-web-pages"></a>1 단계: 페이징 및 정렬 자습서 웹 페이지 추가

이 자습서를 시작 하기 전에 먼저이 자습서와 다음 3 개에 필요한 ASP.NET 페이지를 추가 해 보겠습니다. `PagingAndSorting`이라는 프로젝트에서 새 폴더를 만들어 시작 합니다. 그런 다음이 폴더에 다음 5 개의 ASP.NET 페이지를 추가 하 여 마스터 페이지 `Site.master`를 사용 하도록 구성 된 페이지를 모두 구성 합니다.

- `Default.aspx`
- `SimplePagingSorting.aspx`
- `EfficientPaging.aspx`
- `SortParameter.aspx`
- `CustomSortingUI.aspx`

![PagingAndSorting 폴더를 만들고 자습서 ASP.NET 페이지를 추가 합니다.](paging-and-sorting-report-data-cs/_static/image1.png)

**그림 1**: PagingAndSorting 폴더를 만들고 자습서 ASP.NET 페이지 추가

그런 다음 `Default.aspx` 페이지를 열고 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤을 `UserControls` 폴더에서 디자인 화면으로 끌어 옵니다. [마스터 페이지 및 사이트 탐색](../introduction/master-pages-and-site-navigation-cs.md) 자습서에서 만든이 사용자 정의 컨트롤은 사이트 맵을 열거 하 고 현재 섹션의 이러한 자습서를 글머리 기호 목록에 표시 합니다.

![SectionLevelTutorialListing 사용자 정의 컨트롤을 Default.aspx에 추가 합니다.](paging-and-sorting-report-data-cs/_static/image2.png)

**그림 2**: Default.aspx에 SectionLevelTutorialListing 사용자 정의 컨트롤 추가

글머리 기호 목록에 만들 페이징 및 정렬 자습서를 표시 하려면 사이트 맵에 추가 해야 합니다. `Web.sitemap` 파일을 열고 사이트 맵 노드 태그를 편집, 삽입 및 삭제 한 후 다음 태그를 추가 합니다.

[!code-xml[Main](paging-and-sorting-report-data-cs/samples/sample1.xml)]

![새 ASP.NET 페이지를 포함 하도록 사이트 맵 업데이트](paging-and-sorting-report-data-cs/_static/image3.png)

**그림 3**: 새 ASP.NET 페이지를 포함 하도록 사이트 맵 업데이트

## <a name="step-2-displaying-product-information-in-a-gridview"></a>2 단계: GridView에서 제품 정보 표시

실제로 페이징 및 정렬 기능을 구현 하기 전에는 먼저 제품 정보를 나열 하는 페이징할 수 없고 페이징할 수 없는 표준 GridView를 만듭니다. 이 작업은이 자습서 시리즈 전체에 걸쳐 몇 번 수행 되었지만 이러한 단계를 잘 이해 해야 합니다. 먼저 `SimplePagingSorting.aspx` 페이지를 열고 GridView 컨트롤을 도구 상자에서 디자이너로 끌어 `ID` 속성을 `Products`로 설정 합니다. 다음으로, ProductsBLL 클래스 s `GetProducts()` 메서드를 사용 하 여 모든 제품 정보를 반환 하는 새 ObjectDataSource를 만듭니다.

![GetProducts () 메서드를 사용 하 여 모든 제품에 대 한 정보를 검색 합니다.](paging-and-sorting-report-data-cs/_static/image4.png)

**그림 4**: getproducts () 메서드를 사용 하 여 모든 제품에 대 한 정보 검색

이 보고서는 읽기 전용 보고서 이므로 ObjectDataSource s `Insert()`, `Update()`또는 `Delete()` 메서드를 해당 `ProductsBLL` 메서드에 매핑할 필요가 없습니다. 따라서 업데이트, 삽입 및 삭제 탭의 드롭다운 목록에서 (없음)을 선택 합니다.

![업데이트, 삽입 및 삭제 탭의 드롭다운 목록에서 (없음) 옵션을 선택 합니다.](paging-and-sorting-report-data-cs/_static/image5.png)

**그림 5**: 업데이트, 삽입 및 삭제 탭의 드롭다운 목록에서 (없음) 옵션을 선택 합니다.

다음으로는 제품 이름, 공급 업체, 범주, 가격 및 중단 되지 않은 상태를 표시 하도록 GridView의 필드를 사용자 지정 하겠습니다. 또한 `HeaderText` 속성을 조정 하거나 가격의 서식을 통화로 지정 하는 등의 필드 수준 서식 변경 작업을 자유롭게 수행할 수 있습니다. 이러한 변경 후에는 GridView의 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](paging-and-sorting-report-data-cs/samples/sample2.aspx)]

그림 6에서는 브라우저를 통해 볼 때의 진행률을 보여 줍니다. 이 페이지에는 각 제품의 이름, 범주, 공급자, 가격 및 단종 됨 상태를 보여 주는 모든 제품이 한 화면에 나열 됩니다.

[각 제품이 나열 ![](paging-and-sorting-report-data-cs/_static/image7.png)](paging-and-sorting-report-data-cs/_static/image6.png)

**그림 6**: 각 제품이 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](paging-and-sorting-report-data-cs/_static/image8.png)).

## <a name="step-3-adding-paging-support"></a>3 단계: 페이징 지원 추가

한 화면에 *모든* 제품을 나열 하면 데이터를 읽는 사용자에 대 한 정보 오버 로드가 발생할 수 있습니다. 결과를 보다 쉽게 관리할 수 있도록 데이터를 더 작은 데이터 페이지로 분할 하 고 사용자가 한 번에 한 페이지씩 데이터를 단계별로 실행할 수 있도록 합니다. 이렇게 하려면 GridView의 스마트 태그에서 페이징 사용 확인란을 선택 하기만 하면 됩니다. 그러면 GridView s [`AllowPaging` 속성이](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.allowpaging.aspx) `true`로 설정 됩니다.

[페이징 지원을 추가 하려면 페이징 사용 확인란을 선택 ![.](paging-and-sorting-report-data-cs/_static/image10.png)](paging-and-sorting-report-data-cs/_static/image9.png)

**그림 7**: 페이징 사용 확인란을 선택 하 여 페이징 지원 추가 ([전체 크기 이미지를 보려면 클릭](paging-and-sorting-report-data-cs/_static/image11.png))

페이징을 사용 하도록 설정 하면 페이지당 표시 되는 레코드 수가 제한 되 고 GridView에 *페이징 인터페이스가* 추가 됩니다. 그림 7과 같은 기본 페이징 인터페이스는 사용자가 데이터의 한 페이지에서 다른 페이지로 빠르게 이동할 수 있도록 하는 일련의 페이지 번호입니다. 이전 자습서에서 DetailsView 및 FormView 컨트롤에 페이징 지원을 추가 하는 경우이 페이징 인터페이스를 확인 해야 합니다.

DetailsView 컨트롤과 FormView 컨트롤은 페이지당 단일 레코드만 표시 합니다. 그러나 GridView는 [`PageSize` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.pagesize.aspx) 을 확인 하 여 페이지당 표시할 레코드 수를 결정 합니다 .이 속성의 기본값은 10입니다.

다음 속성을 사용 하 여이 GridView, DetailsView 및 FormView의 페이징 인터페이스를 사용자 지정할 수 있습니다.

- `PagerStyle` 페이징 인터페이스에 대 한 스타일 정보를 나타냅니다. `BackColor`, `ForeColor`, `CssClass`, `HorizontalAlign`등과 같은 설정을 지정할 수 있습니다.
- `PagerSettings`에는 페이징 인터페이스의 기능을 사용자 지정할 수 있는 속성의 일련 포함 됩니다. `PageButtonCount` 페이징 인터페이스에 표시 되는 숫자 페이지 번호의 최대 수를 나타냅니다 (기본값은 10). [`Mode` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pagersettings.mode.aspx) 은 페이징 인터페이스의 작동 방법을 나타내며 다음과 같이 설정할 수 있습니다. 

    - `NextPrevious`는 다음 단추와 이전 단추를 표시 하 여 사용자가 한 번에 한 페이지씩 앞뒤로 이동할 수 있도록 합니다.
    - `NextPreviousFirstLast` 다음 및 이전 단추 외에도, 첫 번째 및 마지막 단추를 포함 하 여 사용자가 데이터의 첫 번째 또는 마지막 페이지로 빠르게 이동할 수 있도록 합니다.
    - `Numeric`는 일련의 페이지 번호를 표시 하 여 사용자가 페이지로 바로 이동할 수 있도록 합니다.
    - 페이지 번호 외에도 `NumericFirstLast`에는 첫 번째 및 마지막 단추가 포함 되어 있으므로 사용자가 데이터의 첫 페이지 또는 마지막 페이지로 빠르게 이동할 수 있습니다. 첫 번째/마지막 단추는 숫자 페이지 번호가 모두 맞지 않는 경우에만 표시 됩니다.

또한 GridView, DetailsView 및 FormView는 모두 현재 표시 되는 페이지와 총 데이터 페이지 수를 나타내는 `PageIndex` 및 `PageCount` 속성을 제공 합니다. `PageIndex` 속성의 인덱스는 0부터 시작 합니다. 즉, 데이터의 첫 페이지를 볼 때 `PageIndex` 0이 됩니다. 반면 `PageCount`는 1에서 계산을 시작 합니다. 즉, `PageIndex` 0에서 `PageCount - 1`사이의 값으로 제한 됩니다.

를 사용 하 여 GridView의 페이징 인터페이스에 대 한 기본 모양을 개선 합니다. 특히를 사용 하 여 페이징 인터페이스를 밝은 회색 배경과 오른쪽 맞춤 합니다. GridView s `PagerStyle` 속성을 통해 이러한 속성을 직접 설정 하는 대신, `Styles.css` 이름 `PagerRowStyle`에서 CSS 클래스를 만든 다음 테마를 통해 `PagerStyle` s `CssClass` 속성을 할당 하겠습니다. `Styles.css`를 열고 다음 CSS 클래스 정의를 추가 하 여 시작 합니다.

[!code-css[Main](paging-and-sorting-report-data-cs/samples/sample3.css)]

그런 다음 `App_Themes` 폴더 내의 `DataWebControls` 폴더에서 `GridView.skin` 파일을 엽니다. *마스터 페이지 및 사이트 탐색* 자습서에서 설명 했 듯이 스킨 파일은 웹 컨트롤에 대 한 기본 속성 값을 지정 하는 데 사용할 수 있습니다. 따라서 `PagerStyle` s `CssClass` 속성을 `PagerRowStyle`로 설정 하는 것을 포함 하도록 기존 설정을 보강 합니다. 또한 `NumericFirstLast` 페이징 인터페이스를 사용 하 여 최대 5 개의 숫자 페이지 단추를 표시 하도록 페이징 인터페이스를 구성 해 보겠습니다.

[!code-aspx[Main](paging-and-sorting-report-data-cs/samples/sample4.aspx)]

## <a name="the-paging-user-experience"></a>페이징 사용자 환경

그림 8에서는 GridView s 페이징 사용 확인란이 선택 된 후 브라우저를 통해 방문 하 고 `GridView.skin` 파일을 통해 `PagerStyle` 및 `PagerSettings` 구성을 수행한 후 웹 페이지를 보여 줍니다. 10 개의 레코드만 표시 되 고 페이징 인터페이스는 첫 번째 데이터 페이지를 표시 하 고 있음을 나타냅니다.

[페이징을 사용 하는 ![레코드의 하위 집합만 한 번에 표시 됩니다.](paging-and-sorting-report-data-cs/_static/image13.png)](paging-and-sorting-report-data-cs/_static/image12.png)

**그림 8**: 페이징을 사용 하도록 설정 하면 레코드의 하위 집합만 한 번에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](paging-and-sorting-report-data-cs/_static/image14.png)).

사용자가 페이징 인터페이스에서 페이지 번호 중 하나를 클릭 하면 다시 게시를 ensues 하 고 페이지를 다시 로드 하 여 요청 된 페이지의 레코드를 표시 합니다. 그림 9에서는 최종 데이터 페이지를 확인 한 후의 결과를 보여 줍니다. 최종 페이지에는 하나의 레코드만 있습니다. 이는 총 81 개의 레코드가 있기 때문입니다 .이로 인해 페이지당 10 개의 레코드와 유일한 레코드가 있는 페이지가 하나 이상 있습니다.

[페이지 번호를 클릭 하면 포스트백이 발생 하 고 레코드의 적절 한 하위 집합이 표시 됩니다. ![](paging-and-sorting-report-data-cs/_static/image16.png)](paging-and-sorting-report-data-cs/_static/image15.png)

**그림 9**: 페이지 번호를 클릭 하면 포스트백이 발생 하 고 레코드의 적절 한 하위 집합이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](paging-and-sorting-report-data-cs/_static/image17.png)).

## <a name="paging-s-server-side-workflow"></a>페이징 s 서버 쪽 워크플로

최종 사용자가 페이징 인터페이스의 단추를 클릭 하면 다시 게시 ensues 및 다음 서버 쪽 워크플로가 시작 됩니다.

1. GridView s (또는 DetailsView 또는 FormView) `PageIndexChanging` 이벤트가 발생 합니다.
2. ObjectDataSource는 BLL의 *모든* 데이터를 다시 요청 합니다. gridview의 `PageIndex` 및 `PageSize` 속성 값은 GridView에서 표시 해야 하는 BLL에서 반환 된 레코드를 확인 하는 데 사용 됩니다.
3. GridView s `PageIndexChanged` 이벤트가 발생 합니다.

2 단계에서 ObjectDataSource는 데이터 원본의 모든 데이터를 다시 요청 합니다. 이러한 페이징 스타일은 일반적으로 `AllowPaging` 속성을 `true`로 설정할 때 기본적으로 사용 되는 페이징 동작 이므로 *기본 페이징*이라고 합니다. 기본 페이징을 사용 하 여 데이터 웹 컨트롤 naively는 데이터의 각 페이지에 대 한 모든 레코드를 검색 합니다. 단, 레코드의 하위 집합만 브라우저에 전송 된 HTML로 실제로 렌더링 되는 경우에도 마찬가지입니다. 데이터베이스 데이터를 BLL 또는 ObjectDataSource에서 캐시 하지 않는 한, 매우 많은 결과 집합 또는 동시 사용자가 많은 웹 응용 프로그램의 경우 기본 페이징이 작동할 됩니다.

다음 자습서에서는 *사용자 지정 페이징을*구현 하는 방법을 살펴보겠습니다. 사용자 지정 페이징을 사용 하면 요청 된 데이터 페이지에 필요한 정확한 레코드 집합만 검색 하도록 ObjectDataSource에 지시할 수 있습니다. 짐작할 수 있듯이 사용자 지정 페이징은 큰 결과 집합을 통해 페이징의 효율성을 크게 향상 시킵니다.

> [!NOTE]
> 기본 페이징은 매우 많은 결과 집합을 페이징할 때 나 여러 사용자가 동시에 수행 하는 사이트의 경우에는 적합 하지 않지만, 사용자 지정 페이징은 구현 하기 위해 더 많은 변경과 노력이 필요 하며,이는 기본적으로 확인란을 선택 하는 것 만큼 간단 하지 않습니다. 페이징). 따라서 기본 페이징은 작고 트래픽이 적은 웹 사이트에 적합 하거나 비교적 작은 결과 집합을 통해 페이징할 때 보다 쉽고 빠르게 구현할 수 있습니다.

예를 들어 데이터베이스에 100 개 이상의 제품이 포함 되지 않는다는 것을 알고 있는 경우 사용자 지정 페이징에 의해 수행 되는 최소 성능 향상은이를 구현 하는 데 필요한 노력으로 인해 상쇄 될 가능성이 높습니다. 그러나 하루에 수천 또는 수만 개의 제품이 있을 수 있으므로 사용자 지정 페이징을 구현 *하지 않으면* 응용 프로그램의 확장성이 크게 저하 됩니다.

## <a name="step-4-customizing-the-paging-experience"></a>4 단계: 페이징 환경 사용자 지정

데이터 웹 컨트롤은 사용자의 페이징 환경을 개선 하는 데 사용할 수 있는 여러 가지 속성을 제공 합니다. 예를 들어 `PageCount` 속성은 총 페이지 수를 표시 하 고, `PageIndex` 속성은 방문한 현재 페이지를 나타내며, 사용자를 특정 페이지로 빠르게 이동 하도록 설정할 수 있습니다. 이러한 속성을 사용 하 여 사용자의 페이징 환경을 개선 하는 방법을 설명 하기 위해 페이지에 레이블 웹 컨트롤을 추가 하 여 현재 방문 하는 페이지를 사용자에 게 알려 주는 DropDownList 컨트롤과 함께 지정 된 페이지로 빠르게 이동할 수 있도록 합니다. .

먼저 페이지에 Label 웹 컨트롤을 추가 하 고, 해당 `ID` 속성을 `PagingInformation`로 설정 하 고, `Text` 속성을 지웁니다. 다음으로, GridView s `DataBound` 이벤트에 대 한 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-csharp[Main](paging-and-sorting-report-data-cs/samples/sample5.cs)]

이 이벤트 처리기는 `PagingInformation` 레이블 s `Text` 속성을 현재 방문 하 고 있는 페이지를 사용자에 게 알리는 메시지에 할당 합니다 .이 메시지에는 `Products.PageCount` 총 페이지 수를 `Products.PageIndex + 1` 있습니다. `Products.PageIndex` 인덱스는 0부터 시작 하므로 `PageIndex` 속성에 1을 추가 합니다. 데이터를 GridView에 바인딩할 때마다 `DataBound` 이벤트가 발생 하는 반면, `PageIndexChanged` 이벤트 처리기는 페이지 인덱스가 변경 될 때만 발생 하기 때문에 `PageIndexChanged` 이벤트 처리기와는 달리이 레이블 s `Text` 속성을 `DataBound` 이벤트 처리기에 할당 합니다. 첫 번째 페이지에서 GridView가 처음에 데이터 바인딩된 경우 `PageIndexChanging` 이벤트는 발생 하지 않습니다 (`DataBound` 이벤트의 경우).

이 외에도 사용자에 게 방문 하는 페이지 및 해당 데이터의 총 페이지 수를 나타내는 메시지가 표시 됩니다.

[현재 페이지 번호와 총 페이지 수를 표시 ![](paging-and-sorting-report-data-cs/_static/image19.png)](paging-and-sorting-report-data-cs/_static/image18.png)

**그림 10**: 현재 페이지 번호와 총 페이지 수 표시 ([전체 크기 이미지를 보려면 클릭](paging-and-sorting-report-data-cs/_static/image20.png))

레이블 컨트롤 외에도 현재 표시 된 페이지를 선택 하 여 GridView의 페이지 번호를 나열 하는 DropDownList 컨트롤을 추가 해 보겠습니다. 여기서의 개념은 사용자가 DropDownList에서 새 페이지 인덱스를 선택 하 여 현재 페이지에서 다른 페이지로 빠르게 이동할 수 있다는 것입니다. 먼저 DropDownList을 디자이너에 추가 하 고 해당 `ID` 속성을 `PageList`로 설정 하 고 스마트 태그에서 Enable AutoPostBack 옵션을 선택 합니다.

그런 다음 `DataBound` 이벤트 처리기로 돌아가서 다음 코드를 추가 합니다.

[!code-csharp[Main](paging-and-sorting-report-data-cs/samples/sample6.cs)]

이 코드는 `PageList` DropDownList의 항목을 지우는 것부터 시작 합니다. 이는 페이지 수가 변경 될 것으로 생각 하는 것은 아니지만 다른 사용자가 시스템을 동시에 사용 하 여 `Products` 테이블에서 레코드를 추가 하거나 제거할 수 있으므로 불필요 한 것 같습니다. 이러한 삽입 또는 삭제는 데이터 페이지 수를 변경할 수 있습니다.

다음으로는 페이지 번호를 다시 만들고 현재 GridView에 매핑되는 항목을 기본값으로 선택 `PageIndex` 해야 합니다. 이를 위해 0부터 `PageCount - 1`까지 루프를 수행 하 고, 각 반복에서 새 `ListItem`를 추가 하 고, 현재 반복 인덱스가 GridView s `PageIndex` 속성과 같으면 `Selected` 속성을 true로 설정 합니다.

마지막으로 사용자가 목록에서 다른 항목을 선택할 때마다 발생 하는 DropDownList s `SelectedIndexChanged` 이벤트에 대 한 이벤트 처리기를 만들어야 합니다. 이 이벤트 처리기를 만들려면 디자이너에서 DropDownList을 두 번 클릭 한 후 다음 코드를 추가 하면 됩니다.

[!code-csharp[Main](paging-and-sorting-report-data-cs/samples/sample7.cs)]

그림 11에 표시 된 것 처럼 GridView s `PageIndex` 속성을 변경 하면 데이터가 GridView로 변경 됩니다. GridView s `DataBound` 이벤트 처리기에서 적절 한 DropDownList `ListItem`를 선택 합니다.

[페이지 6 드롭다운 목록 항목을 선택할 때 사용자가 여섯 번째 페이지로 자동으로 이동 ![](paging-and-sorting-report-data-cs/_static/image22.png)](paging-and-sorting-report-data-cs/_static/image21.png)

**그림 11**: 페이지 6 드롭다운 목록 항목을 선택할 때 사용자가 여섯 번째 페이지로 자동 이동 ([전체 크기 이미지를 보려면 클릭](paging-and-sorting-report-data-cs/_static/image23.png))

## <a name="step-5-adding-bi-directional-sorting-support"></a>5 단계: 양방향 정렬 지원 추가

양방향 정렬 지원을 추가 하는 것은 페이징 지원을 추가 하는 것 처럼 간단 합니다. GridView s 스마트 태그 (GridView s [`AllowSorting` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.allowsorting.aspx) 을 `true`로 설정)에서 정렬 사용 옵션을 선택 하기만 하면 됩니다. 그러면 GridView 필드의 각 헤더가 클릭 될 때 포스트백이 발생 하 고 클릭 한 열을 기준으로 정렬 된 데이터를 오름차순으로 반환 하는 Linkbutton로 렌더링 됩니다. 동일한 헤더 LinkButton를 다시 클릭 하면 데이터를 내림차순으로 다시 정렬 합니다.

> [!NOTE]
> 형식화 된 데이터 집합이 아닌 사용자 지정 데이터 액세스 계층을 사용 하는 경우 GridView의 스마트 태그에 정렬 사용 옵션이 없을 수 있습니다. 기본적으로 정렬을 지 원하는 데이터 원본에 바인딩된 GridViews이 확인란을 사용할 수 있습니다. 형식화 된 데이터 집합은 ADO.NET DataTable이 호출 되 면 지정 된 조건을 사용 하 여 DataTable s Datarow를 정렬 하는 `Sort` 메서드를 제공 하므로 기본 정렬 지원을 제공 합니다.

DAL이 기본적으로 정렬를 지 원하는 개체를 반환 하지 않는 경우 데이터를 정렬 하거나 DAL을 기준으로 데이터를 정렬할 수 있는 비즈니스 논리 계층에 정렬 정보를 전달 하도록 ObjectDataSource를 구성 해야 합니다. 이후 자습서에서는 비즈니스 논리 및 데이터 액세스 계층에서 데이터를 정렬 하는 방법을 살펴보겠습니다.

정렬 Linkbutton은 HTML 하이퍼링크로 렌더링 됩니다. 현재 색 (열어 보지 않은 링크의 경우 파란색, 방문한 링크의 경우 진한 빨강)은 머리글 행의 배경색과 충돌 합니다. 대신, 방문한 적이 있는지 여부에 관계 없이 모든 머리글 행 링크가 흰색으로 표시 되도록 합니다. 이 작업은 `Styles.css` 클래스에 다음을 추가 하 여 수행할 수 있습니다.

[!code-css[Main](paging-and-sorting-report-data-cs/samples/sample8.css)]

이 구문은 HeaderStyle 클래스를 사용 하는 요소 내에서 해당 하이퍼링크를 표시할 때 흰색 텍스트를 사용 함을 나타냅니다.

이 CSS 추가 후 브라우저를 통해 페이지를 방문 하는 경우 화면은 그림 12와 유사 하 게 표시 됩니다. 특히 그림 12는 가격 필드의 머리글 링크를 클릭 한 후의 결과를 보여줍니다.

[단가를 기준으로 결과를 오름차순으로 정렬 ![](paging-and-sorting-report-data-cs/_static/image25.png)](paging-and-sorting-report-data-cs/_static/image24.png)

**그림 12**: 단가를 기준으로 결과가 오름차순으로 정렬 됨 ([전체 크기 이미지를 보려면 클릭](paging-and-sorting-report-data-cs/_static/image26.png))

## <a name="examining-the-sorting-workflow"></a>정렬 워크플로 검사

BoundField, CheckBoxField, Templatefield로 변환 등의 모든 GridView 필드에는 해당 필드 정렬 머리글 링크를 클릭할 때 데이터를 정렬 하는 데 사용 해야 하는 식을 나타내는 `SortExpression` 속성이 있습니다. GridView에도 `SortExpression` 속성이 있습니다. 정렬 헤더 LinkButton를 클릭 하면 GridView는 해당 필드 `SortExpression` 값을 `SortExpression` 속성에 할당 합니다. 그런 다음 데이터를 ObjectDataSource에서 다시 검색 하 고 GridView s `SortExpression` 속성에 따라 정렬 합니다. 다음 목록에서는 최종 사용자가 GridView에서 데이터를 정렬할 때 transpires 하는 일련의 단계에 대해 자세히 설명 합니다.

1. GridView s [정렬 이벤트가](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sorting(VS.80).aspx) 발생 합니다.
2. GridView s [`SortExpression` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sortexpression.aspx) 은 정렬 헤더 LinkButton를 클릭 한 필드의 `SortExpression` 설정 됩니다.
3. ObjectDataSource는 BLL에서 모든 데이터를 다시 검색 한 다음 GridView s를 사용 하 여 데이터를 정렬 `SortExpression`
4. GridView s의 `PageIndex` 속성은 0으로 다시 설정 됩니다. 즉, 사용자가 첫 번째 데이터 페이지로 반환 될 때 (페이징 지원이 구현 되었다고 가정)
5. GridView s [`Sorted` 이벤트가](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sorted(VS.80).aspx) 발생 합니다.

기본 페이징과 마찬가지로 기본 정렬 옵션은 BLL의 *모든* 레코드를 다시 검색 합니다. 페이징이 없는 정렬을 사용 하거나 기본 페이징을 사용 하는 정렬을 사용 하는 경우 이러한 성능 저하를 피할 수 있는 방법이 없습니다 (데이터베이스 데이터를 캐시 하는 것이 부족 함). 그러나 이후 자습서에서 볼 수 있듯이, 사용자 지정 페이징을 사용 하는 경우 데이터를 효율적으로 정렬할 수 있습니다.

GridView를 gridview의 스마트 태그 드롭다운 목록에서 GridView에 바인딩하는 경우 각 GridView 필드는 `ProductsRow` 클래스의 데이터 필드 이름에 `SortExpression` 속성을 자동으로 할당 합니다. 예를 들어 다음 선언 태그에 표시 된 것 처럼 `ProductName` BoundField s `SortExpression`는 `ProductName`로 설정 됩니다.

[!code-aspx[Main](paging-and-sorting-report-data-cs/samples/sample9.aspx)]

필드는 `SortExpression` 속성을 지워 (빈 문자열에 할당) 정렬할 수 없도록 구성할 수 있습니다. 이를 설명 하기 위해 고객이 가격을 기준으로 제품을 정렬 하는 것을 원하지 않는 경우를 가정해 보겠습니다. `UnitPrice` BoundField s `SortExpression` 속성은 선언 태그나 필드 대화 상자를 통해 제거할 수 있습니다 .이 대화 상자는 GridView의 스마트 태그에서 열 편집 링크를 클릭 하 여 액세스할 수 있습니다.

![단가를 기준으로 결과를 오름차순으로 정렬 했습니다.](paging-and-sorting-report-data-cs/_static/image27.png)

**그림 13**: 단가를 기준으로 결과가 오름차순으로 정렬 됨

`UnitPrice` BoundField에 대 한 `SortExpression` 속성이 제거 되 면 헤더는 링크가 아닌 텍스트로 렌더링 되므로 사용자가 가격을 기준으로 데이터를 정렬할 수 없게 됩니다.

[SortExpression 속성을 제거 하면 사용자가 더 이상 가격으로 제품을 정렬할 수 없습니다. ![](paging-and-sorting-report-data-cs/_static/image29.png)](paging-and-sorting-report-data-cs/_static/image28.png)

**그림 14**: SortExpression 속성을 제거 하 여 사용자가 더 이상 제품을 가격 기준으로 정렬할 수 없음 ([전체 크기 이미지를 보려면 클릭](paging-and-sorting-report-data-cs/_static/image30.png))

## <a name="programmatically-sorting-the-gridview"></a>프로그래밍 방식으로 GridView 정렬

GridView s [`Sort` 메서드](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sort.aspx)를 사용 하 여 프로그래밍 방식으로 gridview의 내용을 정렬할 수도 있습니다. `SortExpression` 값을 전달 하 여 [`SortDirection`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sortdirection.aspx) (`Ascending` 또는 `Descending`)와 함께 정렬 하 고 GridView s 데이터가 다시 정렬 됩니다.

`UnitPrice` 기준으로 정렬을 해제 한 이유는 고객이 가장 저렴 한 제품만 구입 하는 것이 걱정 되기 때문입니다. 그러나 가장 비용이 많이 드는 제품을 구입 하는 것이 좋습니다. 따라서 가격을 기준으로 제품을 정렬할 수 있는 것과 마찬가지로 가장 비싼 가격부터 이상으로 제품을 정렬할 수 있습니다.

이를 수행 하려면 페이지에 단추 웹 컨트롤을 추가 하 고, 해당 `ID` 속성을 `SortPriceDescending`로 설정 하 고, 해당 `Text` 속성을 가격 기준으로 정렬 합니다. 그런 다음 디자이너에서 Button 컨트롤을 두 번 클릭 하 여 단추 `Click` 이벤트에 대 한 이벤트 처리기를 만듭니다. 이 이벤트 처리기에 다음 코드를 추가 합니다.

[!code-csharp[Main](paging-and-sorting-report-data-cs/samples/sample10.cs)]

이 단추를 클릭 하면 비용이 가장 많이 드는 비용이 가장 많이 드는 첫 번째 페이지로 사용자가 가장 비쌉니다 (그림 15 참조).

[단추를 클릭 하면 가장 비용이 많이 드는 것부터 가장 비싼 순서로 제품을 ![](paging-and-sorting-report-data-cs/_static/image32.png)](paging-and-sorting-report-data-cs/_static/image31.png)

**그림 15**: 단추를 클릭 하면 비용이 가장 많이 드는 것부터 최소까지 ([전체 크기 이미지를 보려면 클릭](paging-and-sorting-report-data-cs/_static/image33.png))

## <a name="summary"></a>요약

이 자습서에서는 기본 페이징 및 정렬 기능을 구현 하는 방법을 살펴보았습니다 .이 둘은 모두 확인란을 선택 하는 것 만큼 쉽습니다. 사용자가 데이터를 통해 정렬 하거나 페이지를 정렬 하는 경우 유사한 워크플로 펼칩니다:

1. 다시 게시 ensues
2. 데이터 웹 컨트롤의 사전 수준 이벤트가 발생 하는 경우 (`PageIndexChanging` 또는 `Sorting`)
3. ObjectDataSource에서 모든 데이터를 다시 검색 합니다.
4. 데이터 웹 컨트롤 s 사후 수준 이벤트가 발생 하는 경우 (`PageIndexChanged` 또는 `Sorted`)

기본 페이징 및 정렬을 구현 하는 것은 간단 하며, 보다 효율적인 사용자 지정 페이징을 활용 하거나 페이징 또는 정렬 인터페이스를 더욱 향상 시키려면 더 많은 노력을 해지 해야 합니다. 이후 자습서에서는 다음 항목을 살펴봅니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

> [!div class="step-by-step"]
> [다음](efficiently-paging-through-large-amounts-of-data-cs.md)
