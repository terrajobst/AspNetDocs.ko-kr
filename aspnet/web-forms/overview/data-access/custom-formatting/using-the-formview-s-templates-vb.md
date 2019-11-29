---
uid: web-forms/overview/data-access/custom-formatting/using-the-formview-s-templates-vb
title: FormView의 템플릿 사용 (VB) | Microsoft Docs
author: rick-anderson
description: DetailsView와 달리 FormView는 필드로 구성 되지 않습니다. 대신, FormView는 템플릿을 사용 하 여 렌더링 됩니다. 이 자습서에서는 다음을 사용 하 여 살펴보겠습니다.
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 67b25f4c-2823-42b6-b07d-1d650b3fd711
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-the-formview-s-templates-vb
msc.type: authoredcontent
ms.openlocfilehash: cafe47cf5766bb14503852ec6e9f305d1e6d426f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74618335"
---
# <a name="using-the-formviews-templates-vb"></a>FormView의 템플릿 사용 (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_14_VB.exe) 또는 [PDF 다운로드](using-the-formview-s-templates-vb/_static/datatutorial14vb1.pdf)

> DetailsView와 달리 FormView는 필드로 구성 되지 않습니다. 대신, FormView는 템플릿을 사용 하 여 렌더링 됩니다. 이 자습서에서는 FormView 컨트롤을 사용 하 여 데이터의 감소 된 표시를 제공 하는 방법을 살펴보겠습니다.

## <a name="introduction"></a>소개

마지막 두 자습서에서는 템플릿 필드를 사용 하 여 GridView 및 DetailsView 컨트롤의 출력을 사용자 지정 하는 방법을 살펴보았습니다. 템플릿 필드를 사용 하면 특정 필드의 내용이 고도로 사용자 지정 될 수 있지만, GridView와 DetailsView의 끝에는 모두 boxy, 그리드 모양의 모양이 있습니다. 대부분의 경우에는 표 형태의 레이아웃을 사용할 때 유용 하지만, 더 많은 유체를 사용할 경우에는 더 이상 필요 하지 않습니다. 단일 레코드를 표시 하는 경우 FormView 컨트롤을 사용 하 여 유체 레이아웃을 사용할 수 있습니다.

DetailsView와 달리 FormView는 필드로 구성 되지 않습니다. BoundField 또는 Templatefield로 변환를 FormView에 추가할 수 없습니다. 대신, FormView는 템플릿을 사용 하 여 렌더링 됩니다. FormView는 단일 Templatefield로 변환를 포함 하는 DetailsView 컨트롤로 생각 하면 됩니다. FormView는 다음 템플릿을 지원 합니다.

- FormView에 표시 되는 특정 레코드를 렌더링 하는 데 사용 `ItemTemplate`
- 선택적 머리글 행을 지정 하는 데 사용 `HeaderTemplate`
- 선택적 바닥글 행을 지정 하는 데 사용 `FooterTemplate`
- FormView의 `DataSource`에 레코드가 없는 경우 `EmptyDataTemplate` 컨트롤의 태그 렌더링을 위한 `ItemTemplate` 대신 `EmptyDataTemplate` 사용 됩니다.
- `PagerTemplate`를 사용 하 여 페이징이 활성화 된 FormViews의 페이징 인터페이스를 사용자 지정할 수 있습니다.
- `EditItemTemplate` / 편집 인터페이스를 사용자 지정 하거나 이러한 기능을 지 원하는 FormViews의 인터페이스를 삽입 하는 데 사용 `InsertItemTemplate`

이 자습서에서는 FormView 컨트롤을 사용 하 여 보다 엄격한 제품 표시를 제공 하는 방법을 살펴보겠습니다. 이름, 범주, 공급자 등에 대 한 필드를 포함 하는 대신 FormView의 `ItemTemplate` 헤더 요소와 `<table>`의 조합을 사용 하 여 이러한 값을 표시 합니다 (그림 1 참조).

[DetailsView에 표시 된 표 형태의 레이아웃에서 FormView 나누기를 ![합니다.](using-the-formview-s-templates-vb/_static/image2.png)](using-the-formview-s-templates-vb/_static/image1.png)

**그림 1**: FormView는 DetailsView에 표시 된 표 형태의 레이아웃에서 분리 됩니다 ([전체 크기 이미지를 보려면 클릭](using-the-formview-s-templates-vb/_static/image3.png)).

## <a name="step-1-binding-the-data-to-the-formview"></a>1 단계: FormView에 데이터 바인딩

`FormView.aspx` 페이지를 열고 도구 상자에서 FormView를 디자이너로 끌어 옵니다. FormView를 처음 추가 하는 경우에는 `ItemTemplate` 필요 함을 나타내는 회색 상자로 표시 됩니다.

[![ItemTemplate을 제공할 때까지 디자이너에서 FormView를 렌더링할 수 없습니다.](using-the-formview-s-templates-vb/_static/image5.png)](using-the-formview-s-templates-vb/_static/image4.png)

**그림 2**: `ItemTemplate` 제공 될 때까지 디자이너에서 FormView를 렌더링할 수 없음 ([전체 크기 이미지를 보려면 클릭](using-the-formview-s-templates-vb/_static/image6.png))

`ItemTemplate`는 직접 만들 수 있으며 (선언적 구문을 통해) 디자이너를 통해 FormView를 데이터 소스 컨트롤에 바인딩하여 자동으로 만들 수 있습니다. 이 자동 생성 `ItemTemplate`에는 각 필드의 이름과 `Text` 속성이 필드의 값에 바인딩되는 레이블 컨트롤을 나열 하는 HTML이 포함 되어 있습니다. 또한이 방법은 `InsertItemTemplate` 및 `EditItemTemplate`를 자동으로 만들며, 둘 다 데이터 소스 컨트롤에서 반환 하는 각 데이터 필드에 대 한 입력 컨트롤로 채워집니다.

템플릿을 자동으로 만들려면 FormView의 스마트 태그에서 `ProductsBLL` 클래스의 `GetProducts()` 메서드를 호출 하는 새 ObjectDataSource 컨트롤을 추가 합니다. 그러면 `ItemTemplate`, `InsertItemTemplate`및 `EditItemTemplate`를 사용 하 여 FormView가 만들어집니다. 편집 이나 삽입을 지 원하는 FormView를 만드는 데 관심이 없으므로 원본 뷰에서 `InsertItemTemplate`와 `EditItemTemplate`를 제거 합니다. 그런 다음 작업을 수행할 수 있는 깨끗 한 슬레이트를 갖도록 `ItemTemplate` 내에서 태그를 지웁니다.

`ItemTemplate`를 수동으로 빌드하는 경우 도구 상자에서 Designer로 끌어와 ObjectDataSource를 추가 하 고 구성할 수 있습니다. 그러나 디자이너에서 FormView의 데이터 원본을 설정 하지 마십시오. 대신 원본 뷰로 이동 하 여 FormView의 `DataSourceID` 속성을 ObjectDataSource의 `ID` 값으로 수동으로 설정 합니다. 다음으로 `ItemTemplate`를 수동으로 추가 합니다.

이 시점에서 수행 하는 방법에 관계 없이 FormView의 선언 태그는 다음과 같습니다.

[!code-aspx[Main](using-the-formview-s-templates-vb/samples/sample1.aspx)]

잠시 시간을 사용 하 여 FormView의 스마트 태그에서 페이징 사용 확인란을 선택 합니다. 이렇게 하면 FormView의 선언적 구문에 `AllowPaging="True"` 특성이 추가 됩니다. 또한 `EnableViewState` 속성을 False로 설정 합니다.

## <a name="step-2-defining-theitemtemplates-markup"></a>2 단계:`ItemTemplate`태그 정의

FormView가 ObjectDataSource 컨트롤에 바인딩되고 페이징을 지원 하도록 구성 된 상태에서 `ItemTemplate`에 대 한 콘텐츠를 지정할 준비가 되었습니다. 이 자습서에서는 제품 이름이 `<h3>` 제목에 표시 되어 있습니다. 다음에는 HTML `<table>`를 사용 하 여 첫 번째 및 세 번째 열에 속성 이름을 나열 하 고 두 번째 및 네 번째 열에 값을 나열 하는 네 열 테이블에 나머지 제품 속성을 표시 해 보겠습니다.

이 태그는 디자이너에서 FormView의 템플릿 편집 인터페이스를 통해 입력 하거나 선언적 구문을 통해 수동으로 입력할 수 있습니다. 템플릿으로 작업 하는 경우 일반적으로 선언적 구문으로 직접 작업 하는 것이 더 빠르지만, 가장 편안한 기술을 자유롭게 사용할 수 있습니다.

다음 태그는 `ItemTemplate`의 구조가 완료 된 후의 FormView 선언 태그를 보여 줍니다.

[!code-aspx[Main](using-the-formview-s-templates-vb/samples/sample2.aspx)]

예를 들어, 데이터 바인딩 구문 `<%# Eval("ProductName") %>`은 템플릿의 출력에 직접 삽입 될 수 있습니다. 즉, 레이블 컨트롤의 `Text` 속성에 할당할 필요가 없습니다. 예를 들어 `<h3><%# Eval("ProductName") %></h3>`를 사용 하 여 `<h3>` 요소에 표시 되는 `ProductName` 값이 있습니다 .이 값은 Chai가 `<h3>Chai</h3>`으로 렌더링 합니다.

`ProductPropertyLabel` 및 `ProductPropertyValue` CSS 클래스는 `<table>`에서 product 속성 이름 및 값의 스타일을 지정 하는 데 사용 됩니다. 이러한 CSS 클래스는 `Styles.css` 정의 되며 속성 이름이 굵게 표시 되 고 오른쪽에 맞춰집니다. 속성 값에 오른쪽 안쪽 여백이 추가 됩니다.

FormView에서 사용할 수 있는 CheckBoxFields 없기 때문에 `Discontinued` 값을 checkbox로 표시 하기 위해 자체 CheckBox 컨트롤을 추가 해야 합니다. `Enabled` 속성이 False로 설정 되어 읽기 전용으로 설정 되어 있고 CheckBox의 `Checked` 속성이 `Discontinued` 데이터 필드의 값에 바인딩되어 있습니다.

`ItemTemplate` 완료 되 면 제품 정보가 훨씬 더 많은 유체로 표시 됩니다. 마지막 자습서의 DetailsView 출력 (그림 3)을이 자습서의 FormView에서 생성 한 출력과 비교 합니다 (그림 4).

[고정 DetailsView 출력 ![](using-the-formview-s-templates-vb/_static/image8.png)](using-the-formview-s-templates-vb/_static/image7.png)

**그림 3**: 고정 DetailsView 출력 ([전체 크기 이미지를 보려면 클릭](using-the-formview-s-templates-vb/_static/image9.png))

[유체 FormView 출력 ![](using-the-formview-s-templates-vb/_static/image11.png)](using-the-formview-s-templates-vb/_static/image10.png)

**그림 4**: 유체 FormView 출력 ([전체 크기 이미지를 보려면 클릭](using-the-formview-s-templates-vb/_static/image12.png))

## <a name="summary"></a>요약

GridView 및 DetailsView 컨트롤은 템플릿 필드를 사용 하 여 출력을 사용자 지정할 수 있지만, 둘 다 표 형태의 데이터를 표시 합니다. 이러한 경우에는 감소 하는 레이아웃을 사용 하 여 단일 레코드를 표시 해야 하는 경우에는 FormView를 선택 하는 것이 좋습니다. DetailsView과 마찬가지로 FormView는 `DataSource`에서 단일 레코드를 렌더링 하지만 DetailsView와는 달리 템플릿으로 구성 되며 필드를 지원 하지 않습니다.

이 자습서에서 살펴본 것 처럼 FormView는 단일 레코드를 표시할 때 보다 유연한 레이아웃을 허용 합니다. 이후 자습서에서는 양식 보기와 동일한 수준의 유연성을 제공 하지만 여러 레코드 (예: GridView)를 표시할 수 있는 DataList 및 Repeater 컨트롤을 살펴보겠습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서에 대 한 잠재 고객 검토자가 E.R. Gilmore. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](using-templatefields-in-the-detailsview-control-vb.md)
> [다음](displaying-summary-information-in-the-gridview-s-footer-vb.md)
