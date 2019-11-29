---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-cs
title: DataList 및 Repeater 컨트롤을 사용 하 여 데이터C#표시 () | Microsoft Docs
author: rick-anderson
description: 위의 자습서에서 GridView 컨트롤을 사용 하 여 데이터를 표시 했습니다. 이 자습서부터 다음을 사용 하 여 일반적인 보고 패턴 빌드를 살펴보겠습니다.
ms.author: riande
ms.date: 09/13/2006
ms.assetid: 0591cacc-b34b-4cf6-885e-2c9953bb0946
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: 09d3faf811f21a66bb5c234f71d77b2552ae6516
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74623480"
---
# <a name="displaying-data-with-the-datalist-and-repeater-controls-c"></a>DataList 및 반복기 컨트롤을 사용하여 데이터 표시(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_29_CS.exe) 또는 [PDF 다운로드](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/datatutorial29cs1.pdf)

> 위의 자습서에서 GridView 컨트롤을 사용 하 여 데이터를 표시 했습니다. 이 자습서를 시작 하면 이러한 컨트롤을 사용 하 여 데이터를 표시 하는 기본 사항부터 시작 하 여 DataList 및 Repeater 컨트롤을 사용 하 여 일반적인 보고 패턴 빌드를 살펴보겠습니다.

## <a name="introduction"></a>소개

이전 28 개 자습서의 모든 예제에서 GridView 컨트롤로 전환 된 데이터 소스의 여러 레코드를 표시 해야 하는 경우 GridView는 데이터 원본의 각 레코드에 대해 행을 렌더링 하 여 레코드의 데이터 필드를 열에 표시 합니다. GridView를 사용 하 여 데이터를 표시, 페이징, 정렬, 편집 및 삭제 하는 것이 가장 좋습니다. 또한 GridView 구조를 담당 하는 태그에는 각 레코드에 대 한 테이블 행 (`<tr>`) 및 각 필드에 대 한 테이블 셀 (`<td>`)이 포함 된 HTML `<table>` 포함 되어 있습니다.

여러 레코드를 표시할 때 모양과 렌더링 된 태그에서 더 높은 수준의 사용자 지정을 제공 하기 위해 ASP.NET 2.0는 DataList 및 Repeater 컨트롤을 제공 합니다 (둘 다 ASP.NET 버전 1.x 에서도 사용할 수 있음). DataList 및 Repeater 컨트롤은 BoundFields, CheckBoxFields, ButtonFields 등의 템플릿을 사용 하 여 해당 콘텐츠를 렌더링 합니다. GridView와 마찬가지로 DataList는 HTML `<table>`렌더링 하지만 테이블 행당 여러 데이터 원본 레코드를 표시할 수 있습니다. 반면, Repeater는 명시적으로 지정 된 것 보다 더 많은 태그를 렌더링 하지 않으며 내보낸 태그를 정확 하 게 제어 해야 하는 경우 이상적인 후보입니다.

다음 수십 가지 자습서를 통해 이러한 컨트롤 템플릿을 사용 하 여 데이터를 표시 하는 기본 사항부터 시작 하 여 DataList 및 Repeater 컨트롤과 함께 일반적인 보고 패턴을 빌드하는 방법을 살펴보겠습니다. 이러한 컨트롤의 형식을 지정 하는 방법, DataList에서 데이터 원본 레코드의 레이아웃을 변경 하는 방법, 공통 마스터/세부 시나리오, 데이터를 편집 하 고 삭제 하는 방법, 레코드를 페이징 하는 방법 등을 확인할 수 있습니다.

## <a name="step-1-adding-the-datalist-and-repeater-tutorial-web-pages"></a>1 단계: DataList 및 Repeater 자습서 웹 페이지 추가

이 자습서를 시작 하기 전에 먼저이 자습서에 필요한 ASP.NET 페이지를 추가 하 고 DataList 및 Repeater를 사용 하 여 데이터를 표시 하는 다음 몇 가지 자습서를 수행 하겠습니다. `DataListRepeaterBasics`이라는 프로젝트에서 새 폴더를 만들어 시작 합니다. 그런 다음이 폴더에 다음 5 개의 ASP.NET 페이지를 추가 하 여 마스터 페이지 `Site.master`를 사용 하도록 구성 된 페이지를 모두 구성 합니다.

- `Default.aspx`
- `Basics.aspx`
- `Formatting.aspx`
- `RepeatColumnAndDirection.aspx`
- `NestedControls.aspx`

![DataListRepeaterBasics 폴더를 만들고 자습서 ASP.NET 페이지를 추가 합니다.](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image1.png)

**그림 1**: `DataListRepeaterBasics` 폴더 만들기 및 자습서 ASP.NET 페이지 추가

`Default.aspx` 페이지를 열고 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤을 `UserControls` 폴더에서 디자인 화면으로 끌어 옵니다. [마스터 페이지 및 사이트 탐색](../introduction/master-pages-and-site-navigation-cs.md) 자습서에서 만든이 사용자 정의 컨트롤은 사이트 맵을 열거 하 고 현재 섹션의 자습서를 글머리 기호 목록에 표시 합니다.

[SectionLevelTutorialListing 사용자 정의 컨트롤을 Default.aspx에 추가 ![](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image3.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image2.png)

**그림 2**: `Default.aspx`에 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image4.png))

글머리 기호 목록에 생성할 DataList 및 Repeater 자습서가 표시 되도록 하려면 사이트 맵에 추가 해야 합니다. `Web.sitemap` 파일을 열고 사용자 지정 단추 추가 사이트 맵 노드 태그 뒤에 다음 태그를 추가 합니다.

[!code-xml[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample1.xml)]

![새 ASP.NET 페이지를 포함 하도록 사이트 맵 업데이트](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image5.png)

**그림 3**: 새 ASP.NET 페이지를 포함 하도록 사이트 맵 업데이트

## <a name="step-2-displaying-product-information-with-the-datalist"></a>2 단계: DataList를 사용 하 여 제품 정보 표시

FormView와 마찬가지로 DataList 컨트롤의 렌더링 된 출력은 BoundFields, CheckBoxFields 등의 템플릿에 따라 달라 집니다. FormView와 달리 DataList는 독립가 아닌 레코드 집합을 표시 하도록 설계 되었습니다. 를 사용 하 여이 자습서를 시작 하 고, DataList에 제품 정보를 바인딩합니다. 먼저 `DataListRepeaterBasics` 폴더에서 `Basics.aspx` 페이지를 엽니다. 그런 다음, 도구 상자에서 DataList를 디자이너로 끌어 옵니다. 그림 4에서 보여 주는 것 처럼 DataList s 템플릿을 지정 하기 전에 디자이너에서 회색 상자로 표시 합니다.

[![DataList를 도구 상자에서 디자이너로 끌어 옵니다.](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image7.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image6.png)

**그림 4**: 도구 상자의 DataList를 디자이너로 끌기 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image8.png))

DataList s 스마트 태그에서 새 ObjectDataSource를 추가 하 고 `ProductsBLL` 클래스 s `GetProducts` 메서드를 사용 하도록 구성 합니다. 이 자습서에서 읽기 전용 DataList를 다시 만들기 때문에 마법사의 삽입, 업데이트 및 삭제 탭에서 드롭다운 목록을 (없음)으로 설정 합니다.

[새 ObjectDataSource를 만들 ![Opt](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image10.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image9.png)

**그림 5**: 새 ObjectDataSource를 만드는 옵트인 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image11.png))

[ProductsBLL 클래스를 사용 하도록 ObjectDataSource 구성 ![](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image13.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image12.png)

**그림 6**: `ProductsBLL` 클래스를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image14.png))

[GetProducts 메서드를 사용 하 여 모든 제품에 대 한 정보를 검색 ![](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image16.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image15.png)

**그림 7**: `GetProducts` 메서드를 사용 하 여 모든 제품에 대 한 정보 검색 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image17.png))

ObjectDataSource를 구성 하 고 스마트 태그를 통해 DataList와 연결 하면 Visual Studio에서 데이터 소스에서 반환 된 각 데이터 필드의 이름과 값을 표시 하는 `ItemTemplate`을 자동으로 만듭니다 (아래 태그 참조). 이 기본 `ItemTemplate`의 모양은 디자이너를 통해 FormView에 데이터 소스를 바인딩할 때 자동으로 생성 되는 템플릿의 경우와 동일 합니다.

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample2.aspx)]

> [!NOTE]
> FormView의 스마트 태그를 통해 FormView 컨트롤에 데이터 소스를 바인딩하는 경우 Visual Studio는 `ItemTemplate`, `InsertItemTemplate`및 `EditItemTemplate`를 만들었습니다. 그러나 DataList를 사용 하면 `ItemTemplate` 만들어집니다. 이는 DataList에는 FormView에서 제공 하는 것과 동일한 기본 제공 편집 및 삽입 지원이 없기 때문입니다. DataList에는 편집 및 삭제 관련 이벤트가 포함 되어 있으며, 약간의 코드를 사용 하 여 편집 및 삭제 지원을 추가할 수 있지만, FormView와 마찬가지로 간단한 기본 지원 기능이 없습니다. 이후 자습서에서 DataList를 사용 하 여 편집 및 삭제 지원을 포함 하는 방법을 살펴보겠습니다.

을 사용 하 여이 템플릿의 모양을 개선 합니다. 모든 데이터 필드를 표시 하는 대신 제품 이름, 공급자, 범주, 단위당 수량 및 단가만 표시 합니다. 또한 `<h4>` 제목에 이름을 표시 하 고 머리글 아래의 `<table>`를 사용 하 여 나머지 필드를 레이아웃 합니다.

이러한 변경을 위해 DataList의 스마트 태그에서 템플릿 편집 기능을 사용 하 여 템플릿 편집 링크를 클릭 하거나 페이지의 선언적 구문을 통해 수동으로 템플릿을 수정할 수 있습니다. 디자이너에서 템플릿 편집 옵션을 사용 하는 경우 결과 태그가 다음 태그와 정확히 일치 하지 않을 수 있지만, 브라우저를 통해 볼 때 그림 8에 표시 된 화면과 매우 유사 하 게 표시 됩니다.

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample3.aspx)]

> [!NOTE]
> 위의 예제에서는 `Text` 속성에 데이터 바인딩 구문의 값이 할당 된 레이블 웹 컨트롤을 사용 합니다. 또는 레이블을 모두 생략 하 여 데이터 바인딩 구문도 입력할 수 있습니다. 즉, `<asp:Label ID="CategoryNameLabel" runat="server" Text='<%# Eval("CategoryName") %>' />`를 사용 하는 대신 `<%# Eval("CategoryName") %>`선언 구문을 대신 사용할 수 있습니다.

그러나 Label 웹 컨트롤에서 나가면 두 가지 이점을 제공 합니다. 첫째, 다음 자습서에서 볼 수 있듯이 데이터를 기반으로 데이터를 보다 쉽게 서식 지정 하는 방법을 제공 합니다. 두 번째로, 디자이너의 템플릿 편집 옵션은 일부 웹 컨트롤 외부에 표시 되는 선언적 데이터 바인딩 구문을 표시 하지 않습니다. 대신, 템플릿 편집 인터페이스는 정적 태그 및 웹 컨트롤 작업을 용이 하 게 하기 위해 디자인 되었으며 웹 컨트롤 스마트 태그에서 액세스할 수 있는 데이터 바인딩 편집 대화 상자를 통해 모든 데이터 바인딩을 수행 한다고 가정 합니다.

따라서 디자이너를 통해 템플릿을 편집 하는 옵션을 제공 하는 DataList로 작업 하는 경우 템플릿 편집 인터페이스를 통해 콘텐츠를 액세스할 수 있도록 레이블 웹 컨트롤을 사용 하는 것이 좋습니다. 잠시 후에는 반복기가 원본 뷰에서 템플릿 콘텐츠를 편집 해야 합니다. 결과적으로, 반복 되는 템플릿을 작성 하는 경우 프로그래밍 논리를 기반으로 데이터 바인딩된 텍스트의 모양에 서식을 지정 해야 한다는 것을 알고 있지 않으면 레이블 웹 컨트롤을 생략 하는 경우가 많습니다.

[각 제품 출력 ![DataList s ItemTemplate을 사용 하 여 렌더링 됩니다.](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image19.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image18.png)

**그림 8**: 각 제품의 출력이 DataList s `ItemTemplate`를 사용 하 여 렌더링 됩니다 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image20.png)).

## <a name="step-3-improving-the-appearance-of-the-datalist"></a>3 단계: DataList의 모양 향상

GridView와 마찬가지로 DataList는 `Font`, `ForeColor`, `BackColor`, `CssClass`, `ItemStyle`, `AlternatingItemStyle`, `SelectedItemStyle`등과 같은 다양 한 스타일 관련 속성을 제공 합니다. GridView 및 DetailsView 컨트롤을 사용할 때 이러한 두 컨트롤에 대 한 `CssClass` 속성을 미리 정의 하 고 몇 가지 하위 속성 (`RowStyle`, `HeaderStyle`등)의 `CssClass` 속성을 미리 정의한 `DataWebControls` 테마에서 스킨 파일을 만들었습니다. 는 DataList에 대해 동일한 작업을 수행 합니다.

[ObjectDataSource를 사용 하 여 데이터 표시](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md) 자습서에서 설명 하는 것 처럼 스킨 파일은 웹 컨트롤에 대 한 기본 모양 관련 속성을 지정 합니다. 테마는 웹 사이트의 특정 모양과 느낌을 정의 하는 스킨, CSS, 이미지 및 JavaScript 파일의 컬렉션입니다. ObjectDataSource를 *사용 하 여 데이터 표시* 자습서에서는 현재 두 개의 스킨 파일 (`GridView.skin` 및 `DetailsView.skin`)을 포함 하는 `DataWebControls` 테마 (`App_Themes` 폴더 안에 폴더로 구현 됨)를 만들었습니다. 세 번째 스킨 파일을 추가 하 여 DataList에 대해 미리 정의 된 스타일 설정을 지정 해 보겠습니다.

스킨 파일을 추가 하려면 `App_Themes/DataWebControls` 폴더를 마우스 오른쪽 단추로 클릭 하 고 새 항목 추가를 선택한 다음 목록에서 스킨 파일 옵션을 선택 합니다. 파일 이름을 `DataList.skin`로 지정합니다.

[![DataList. skin 이라는 새 스킨 파일을 만듭니다.](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image22.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image21.png)

**그림 9**: `DataList.skin` 이라는 새 스킨 파일 만들기 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image23.png))

`DataList.skin` 파일에 대해 다음 태그를 사용 합니다.

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample4.aspx)]

이러한 설정은 GridView 및 DetailsView 컨트롤과 함께 사용 되는 것과 동일한 CSS 클래스를 적절 한 DataList 속성에 할당 합니다. 여기 `DataWebControlStyle`, `AlternatingRowStyle`, `RowStyle`등에서 사용 되는 CSS 클래스는 `Styles.css` 파일에 정의 되며 이전 자습서에서 추가 되었습니다.

이 스킨 파일이 추가 되 면 디자이너에서 DataList의 모양이 업데이트 됩니다. 새 스킨 파일의 효과를 확인 하려면 디자이너 뷰를 새로 고쳐야 할 수도 있습니다. 보기 메뉴에서 새로 고침을 선택 합니다. 그림 10에 표시 된 것 처럼 각 교대 제품은 연한 분홍 배경색을 갖습니다.

[![DataList. skin 이라는 새 스킨 파일을 만듭니다.](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image25.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image24.png)

**그림 10**: `DataList.skin` 이라는 새 스킨 파일 만들기 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image26.png))

## <a name="step-4-exploring-the-datalist-s-other-templates"></a>4 단계: DataList s 기타 템플릿 탐색

`ItemTemplate`외에도 DataList는 다음과 같은 여섯 가지 선택적 템플릿을 지원 합니다.

- `HeaderTemplate` 제공 되는 경우 출력에 머리글 행을 추가 하 고이 행을 렌더링 하는 데 사용 됩니다.
- 교대로 반복 되는 항목을 렌더링 하는 데 사용 `AlternatingItemTemplate`
- 선택한 항목을 렌더링 하는 데 사용 `SelectedItemTemplate`. 선택한 항목은 인덱스가 DataList s [`SelectedIndex` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.selectedindex.aspx) 에 해당 하는 항목입니다.
- 편집 중인 항목을 렌더링 하는 데 사용 `EditItemTemplate`
- `SeparatorTemplate` 제공 하는 경우 각 항목 사이에 구분 기호를 추가 하 고이 구분 기호를 렌더링 하는 데 사용 됩니다.
- `FooterTemplate`-제공 되는 경우 출력에 바닥글 행을 추가 하 고이 행을 렌더링 하는 데 사용 됩니다.

`HeaderTemplate` 또는 `FooterTemplate`를 지정 하는 경우 DataList는 렌더링 된 출력에 머리글 또는 바닥글 행을 추가 합니다. GridView의 머리글과 바닥글 행과 마찬가지로 DataList의 머리글과 바닥글은 데이터에 바인딩되지 않습니다. 따라서 바인딩된 데이터에 액세스 하려고 하는 `HeaderTemplate` 또는 `FooterTemplate`의 모든 데이터 바인딩 구문은 빈 문자열을 반환 합니다.

> [!NOTE]
> [Gridview s 바닥글의 요약 정보를 표시](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-cs.md) 하는 것과 같이 머리글 및 바닥글 행이 데이터 바인딩 구문을 지원 하지 않는 반면, gridview s `RowDataBound` 이벤트 처리기에서 데이터 관련 정보를 이러한 행에 직접 삽입할 수 있습니다. 이 기법을 사용 하 여 컨트롤에 바인딩된 데이터에서 실행 중인 합계 또는 기타 정보를 계산 하 고 해당 정보를 바닥글에 할당할 수 있습니다. 이와 동일한 개념을 DataList 및 Repeater 컨트롤에 적용할 수 있습니다. 유일한 차이점은 DataList 및 Repeater의 경우 `RowDataBound` 이벤트 대신 `ItemDataBound` 이벤트에 대 한 이벤트 처리기를 만드는 것입니다.

이 예에서는를 사용 하 여 DataList의 맨 위에 표시 되는 제품 정보를 `<h3>` 제목을 사용 합니다. 이를 수행 하려면 적절 한 태그를 사용 하 여 `HeaderTemplate`를 추가 합니다. 디자이너에서이를 수행 하려면 DataList의 스마트 태그에서 템플릿 편집 링크를 클릭 하 고, 드롭다운 목록에서 머리글 템플릿을 선택 하 고, 스타일 드롭다운 목록에서 제목 3 옵션을 선택한 후 텍스트를 입력 합니다 (그림 11 참조).

[텍스트 제품 정보를 사용 하 여 HeaderTemplate를 추가 ![](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image28.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image27.png)

**그림 11**: 텍스트 제품 정보를 사용 하 여 `HeaderTemplate` 추가 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image29.png))

또는 `<asp:DataList>` 태그 내에 다음 태그를 입력 하 여 선언적으로 추가할 수 있습니다.

[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample5.html)]

각 제품 목록 사이에 공백을 추가 하려면 각 섹션 사이에 줄을 포함 하는 `SeparatorTemplate`를 추가 해 보겠습니다. 수평선 (`<hr>`) 태그는 이러한 구분선을 추가 합니다. 다음 태그를 포함 하도록 `SeparatorTemplate`를 만듭니다.

[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample6.html)]

> [!NOTE]
> `HeaderTemplate` 및 `FooterTemplates`와 마찬가지로 `SeparatorTemplate` 데이터 원본의 레코드에 바인딩되지 않으므로 DataList에 바인딩된 데이터 소스 레코드에 직접 액세스할 수 없습니다.

이러한 추가 작업을 수행한 후 브라우저를 통해 페이지를 볼 때 그림 12와 같이 표시 됩니다. 머리글 행과 각 제품 목록 사이의 줄을 기록해 둡니다.

[![DataList에는 머리글 행이 포함 되 고 각 제품 목록 사이에는 수평선 규칙이 포함 됩니다.](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image31.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image30.png)

**그림 12**: DataList에는 각 제품 목록 사이에 헤더 행과 수평선 규칙이 포함 되어 있습니다 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image32.png)).

## <a name="step-5-rendering-specific-markup-with-the-repeater-control"></a>5 단계: Repeater 컨트롤로 특정 태그 렌더링

그림 12의 DataList 예제를 방문할 때 브라우저에서 뷰/소스를 수행 하는 경우 datalist는 DataList에 바인딩된 각 항목에 대해 단일 테이블 셀 (`<td>`)을 포함 하는 테이블 행 (`<tr>`)이 포함 된 HTML `<table>`를 내보냅니다. 실제로이 출력은 단일 Templatefield로 변환를 사용 하 여 GridView에서 내보내는 항목과 동일 합니다. 이후 자습서에서 볼 수 있듯이 DataList는 출력의 추가 사용자 지정을 허용 하 여 테이블당 여러 개의 데이터 원본 레코드를 표시할 수 있도록 합니다.

그러나 HTML `<table>`를 내보내지 않으려면 어떻게 해야 하나요? 데이터 웹 컨트롤에 의해 생성 된 태그를 전체 및 완전히 제어 하려면 Repeater 컨트롤을 사용 해야 합니다. DataList와 마찬가지로 Repeater는 템플릿을 기반으로 생성 됩니다. 그러나 Repeater는 다음 5 가지 템플릿만 제공 합니다.

- `HeaderTemplate` 지정 된 경우 항목 앞에 지정 된 태그를 추가 합니다.
- 항목을 렌더링 하는 데 사용 `ItemTemplate`
- 제공 된 경우 `AlternatingItemTemplate` 교대로 반복 되는 항목을 렌더링 하는 데 사용 됩니다.
- `SeparatorTemplate` 지정 된 경우 각 항목 사이에 지정 된 태그를 추가 합니다.
- `FooterTemplate`-제공 되는 경우 지정 된 태그를 항목 뒤에 추가 합니다.

ASP.NET 1.x에서 Repeater 컨트롤은 데이터 원본에서 가져온 데이터의 글머리 기호 목록을 표시 하는 데 주로 사용 되었습니다. 이 경우 `HeaderTemplate` 및 `FooterTemplates`에는 각각 여는 태그와 닫는 `<ul>` 태그가 포함 되지만 `ItemTemplate`에는 데이터 바인딩 구문이 있는 `<li>` 요소가 포함 됩니다. [마스터 페이지 및 사이트 탐색](../introduction/master-pages-and-site-navigation-cs.md) 자습서의 두 예제에서 본 것 처럼 ASP.NET 2.0에서이 방법을 사용할 수 있습니다.

- `Site.master` 마스터 페이지에서 Repeater는 최상위 사이트 맵 콘텐츠의 글머리 기호 목록을 표시 하는 데 사용 되었습니다 (기본 보고, 필터링 보고서, 사용자 지정 형식 등). 다른 중첩 된 Repeater는 최상위 섹션의 자식 섹션을 표시 하는 데 사용 되었습니다.
- `SectionLevelTutorialListing.ascx`에서 Repeater는 현재 사이트 맵 섹션의 하위 섹션에 대 한 글머리 기호 목록을 표시 하는 데 사용 되었습니다.

> [!NOTE]
> ASP.NET 2.0에는 간단한 글머리 기호 목록을 표시 하기 위해 데이터 소스 컨트롤에 바인딩할 수 있는 새로운 [BulletedList 컨트롤이](https://msdn.microsoft.com/library/ms228101.aspx)도입 되었습니다. BulletedList 컨트롤을 사용 하 여 목록 관련 HTML을 지정할 필요가 없습니다. 대신 각 목록 항목에 대 한 텍스트로 표시할 데이터 필드를 지정 합니다.

Repeater는 모든 데이터 catch 웹 컨트롤의 역할을 합니다. 필요한 태그를 생성 하는 기존 컨트롤이 없으면 Repeater 컨트롤을 사용할 수 있습니다. Repeater를 사용 하 여 설명 하기 위해에는 2 단계에서 만든 제품 정보 DataList 위에 표시 되는 범주 목록이 표시 됩니다. 특히, 각 범주가 테이블의 열로 표시 된 단일 행 HTML `<table>`에 범주가 표시 되도록 합니다.

이를 수행 하려면 먼저 도구 상자의 Repeater 컨트롤을 디자이너의 제품 정보 DataList로 끌어 옵니다. DataList와 마찬가지로, 해당 템플릿이 정의 될 때까지 Repeater는 처음에 회색 상자로 표시 됩니다.

[디자이너에 리피터를 추가 ![](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image34.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image33.png)

**그림 13**: 디자이너에 리피터 추가 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image35.png))

Repeater s 스마트 태그에는 하나의 옵션만 있습니다. 데이터 소스를 선택 합니다. 새 ObjectDataSource를 만들어 `CategoriesBLL` 클래스 s `GetCategories` 메서드를 사용 하도록 구성 합니다.

[새 ObjectDataSource를 만들 ![](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image37.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image36.png)

**그림 14**: 새 ObjectDataSource 만들기 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image38.png))

[범주 Bll 클래스를 사용 하도록 ObjectDataSource 구성 ![](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image40.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image39.png)

**그림 15**: `CategoriesBLL` 클래스를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image41.png))

[GetCategories 메서드를 사용 하 여 모든 범주에 대 한 정보를 검색 ![](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image43.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image42.png)

**그림 16**: `GetCategories` 메서드를 사용 하 여 모든 범주에 대 한 정보 검색 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image44.png))

DataList와 달리 Visual Studio에서는 데이터 소스에 바인딩한 후에도 자동으로 Repeater에 대해 ItemTemplate을 만들지 않습니다. 또한, Repeater s 템플릿은 디자이너를 통해 구성할 수 없으며 선언적으로 지정 해야 합니다.

각 범주에 대 한 열이 있는 단일 행 `<table>`로 범주를 표시 하려면 다음과 유사한 태그를 내보내려면 Repeater가 필요 합니다.

[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample7.html)]

`<td>Category X</td>` 텍스트는 반복 되는 부분 이므로 Repeater s ItemTemplate에 표시 됩니다. `<table><tr>`-앞에 나타나는 태그는 `HeaderTemplate`에 배치 되 고 끝 태그 `</tr></table>`는 `FooterTemplate`에 배치 됩니다. 이러한 템플릿 설정을 입력 하려면 왼쪽 아래 모서리에 있는 원본 단추를 클릭 하 여 ASP.NET 페이지의 선언적 부분으로 이동 하 고 다음 구문을 입력 합니다.

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample8.aspx)]

Repeater는 해당 템플릿에 지정 된 대로 정확한 태그를 내보내고, 아무 것도 하지 않습니다. 그림 17은 브라우저를 통해 볼 때의 출력을 보여 줍니다.

[단일 행 HTML &lt;테이블&gt; ![별도의 열에 각 범주 나열](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image46.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image45.png)

**그림 17**: 단일 행 HTML `<table>` 별도의 열에 각 범주 나열 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image47.png))

## <a name="step-6-improving-the-appearance-of-the-repeater"></a>6 단계: Repeater의 모양 향상

Repeater는 해당 템플릿에 의해 지정 된 태그를 정확 하 게 가져오므로 Repeater에 대 한 스타일 관련 속성은 없습니다. Repeater에 의해 생성 되는 콘텐츠의 모양을 변경 하려면 필요한 HTML 또는 CSS 콘텐츠를 Repeater 템플릿에 직접 직접 추가 해야 합니다.

이 예에서는 DataList에서 교대로 반복 되는 행과 같이 category 열에 대체 배경색을 사용 합니다. 이렇게 하려면 다음과 같이 `ItemTemplate` 및 `AlternatingItemTemplate` 템플릿을 통해 각 Repeater 항목에 `RowStyle` CSS 클래스를 할당 하 고 `AlternatingRowStyle` CSS 클래스를 각 교대로 반복 되는 반복기 항목에 할당 해야 합니다.

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample9.aspx)]

텍스트 제품 범주를 사용 하 여 출력에 머리글 행을 추가할 수도 있습니다. 결과 `<table>` 구성 될 열 수를 알 수 없으므로 모든 열에 걸쳐 있는 머리글 행을 생성 하는 가장 간단한 방법은 *두 개의* `<table>` s를 사용 하는 것입니다. 첫 번째 `<table>`에는 두 행이 포함 되 고, 두 번째 행에는 시스템의 각 범주에 대 한 열이 있는 두 번째 단일 행 `<table>` 포함 됩니다. 즉, 다음 태그를 내보내야 합니다.

[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample10.html)]

다음 `HeaderTemplate` 하 고 `FooterTemplate` 하면 원하는 태그가 생성 됩니다.

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample11.aspx)]

그림 18에서는 이러한 변경이 수행 된 후의 반복을 보여 줍니다.

[범주 열을 배경색으로 대체 하 고 머리글 행을 포함 하는 ![](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image49.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image48.png)

**그림 18**: 배경색으로 대체 되 고 머리글 행을 포함 하는 범주 열 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image50.png))

## <a name="summary"></a>요약

GridView 컨트롤을 사용 하면 데이터를 쉽게 표시 하 고, 편집 하 고, 삭제 하 고, 정렬 하 고, 페이지를 표시할 수 있지만 모양은 매우 boxy와 비슷합니다. 모양에 대 한 더 많은 제어를 위해 DataList 또는 Repeater 컨트롤을 사용 해야 합니다. 이러한 컨트롤은 모두 BoundFields, CheckBoxFields 등의 템플릿을 사용 하 여 레코드 집합을 표시 합니다.

DataList는 기본적으로 단일 Templatefield로 변환를 사용 하는 GridView와 마찬가지로 단일 테이블 행에 각 데이터 원본 레코드를 표시 하는 HTML `<table>` 렌더링 합니다. 그러나 이후 자습서에서 볼 수 있듯이 DataList는 테이블 행 마다 여러 레코드를 표시할 수 있도록 합니다. 반면에 Repeater는 해당 템플릿에 지정 된 태그를 엄격히 내보냅니다. 추가 태그를 추가 하지 않으므로 일반적으로 `<table>` 아닌 HTML 요소 (예: 글머리 기호 목록)에 데이터를 표시 하는 데 사용 됩니다.

DataList 및 Repeater는 렌더링 된 출력에서 더 많은 유연성을 제공 하지만 GridView에는 여러 기본 제공 기능이 없습니다. 향후 자습서에서 살펴볼 때 이러한 기능 중 일부는 너무 많은 노력 없이 다시 연결 될 수 있지만, GridView 대신 DataList 또는 Repeater를 사용 하면 이러한 기능을 구현 하지 않고도 사용할 수 있는 기능이 제한 됩니다. 직접.

행복 한 프로그래밍

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Yaakov Ellis, Liz Shulok, Randy Schmidt 및 Stacy 공원 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [다음](formatting-the-datalist-and-repeater-based-upon-data-cs.md)
