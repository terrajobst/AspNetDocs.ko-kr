---
uid: web-forms/overview/data-access/custom-button-actions-with-the-datalist-and-repeater/custom-buttons-in-the-datalist-and-repeater-cs
title: DataList 및 Repeater (C#) |의 사용자 지정 단추 Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 Repeater를 사용 하 여 시스템의 범주를 나열 하는 인터페이스를 빌드하고 각 범주는 associ을 표시 하는 단추를 제공 합니다.
ms.author: riande
ms.date: 11/13/2006
ms.assetid: 1f42e332-78dc-438b-9e35-0c97aa0ad929
msc.legacyurl: /web-forms/overview/data-access/custom-button-actions-with-the-datalist-and-repeater/custom-buttons-in-the-datalist-and-repeater-cs
msc.type: authoredcontent
ms.openlocfilehash: e8cb1054068327c25e057b6df1cc7506feec8d37
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78465347"
---
# <a name="custom-buttons-in-the-datalist-and-repeater-c"></a>DataList 및 반복기의 사용자 지정 단추(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_46_CS.exe) 또는 [PDF 다운로드](custom-buttons-in-the-datalist-and-repeater-cs/_static/datatutorial46cs1.pdf)

> 이 자습서에서는 BulletedList 컨트롤을 사용 하 여 연결 된 제품을 표시 하는 단추를 제공 하는 각 범주를 사용 하 여 시스템의 범주를 나열 하는 리피터를 사용 하는 인터페이스를 빌드합니다.

## <a name="introduction"></a>소개

이전 17 개의 DataList 및 Repeater 자습서를 통해 읽기 전용 예제와 편집 및 삭제 예제를 모두 만들었습니다. DataList 내에서 기능을 편집 하 고 삭제 하는 데 도움이 되도록 DataList s에 단추를 추가 했습니다. 클릭 하면 다시 게시를 발생 시키고 단추 `CommandName` 속성에 해당 하는 DataList 이벤트를 발생 `ItemTemplate`. 예를 들어 `CommandName` 속성 값을 편집 하 여 `ItemTemplate`에 단추를 추가 하면 DataList s `EditCommand` 다시 게시 될 때 발생 합니다. `CommandName` 삭제가 있는 하나 `DeleteCommand`발생 합니다.

편집 및 삭제 단추 외에도 DataList 및 Repeater 컨트롤에는 클릭할 때 일부 사용자 지정 서버 쪽 논리를 수행 하는 단추, Linkbutton 또는 ImageButtons이 포함 될 수 있습니다. 이 자습서에서는 리피터를 사용 하 여 시스템의 범주를 나열 하는 인터페이스를 작성 합니다. 각 범주에 대해 Repeater에는 BulletedList 컨트롤을 사용 하 여 범주와 관련 된 제품을 표시 하는 단추가 포함 됩니다 (그림 1 참조).

[제품 표시 링크를 클릭 ![글머리 기호 목록의 제품 범주를 표시 합니다.](custom-buttons-in-the-datalist-and-repeater-cs/_static/image2.png)](custom-buttons-in-the-datalist-and-repeater-cs/_static/image1.png)

**그림 1**: 제품 표시 링크를 클릭 하면 글머리 기호 목록에 범주 제품이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](custom-buttons-in-the-datalist-and-repeater-cs/_static/image3.png)).

## <a name="step-1-adding-the-custom-button-tutorial-web-pages"></a>1 단계: 사용자 지정 단추 자습서 웹 페이지 추가

사용자 지정 단추를 추가 하는 방법을 살펴보기 전에 먼저이 자습서에 필요한 웹 사이트 프로젝트에 ASP.NET 페이지를 만들어 보겠습니다. `CustomButtonsDataListRepeater`이라는 새 폴더를 추가 하 여 시작 합니다. 다음으로 해당 폴더에 다음 두 개의 ASP.NET 페이지를 추가 하 여 각 페이지를 `Site.master` 마스터 페이지에 연결 합니다.

- `Default.aspx`
- `CustomButtons.aspx`

![사용자 지정 단추 관련 자습서에 대 한 ASP.NET 페이지 추가](custom-buttons-in-the-datalist-and-repeater-cs/_static/image4.png)

**그림 2**: 사용자 지정 단추 관련 자습서에 대 한 ASP.NET 페이지 추가

다른 폴더와 마찬가지로 `CustomButtonsDataListRepeater` 폴더의 `Default.aspx`에는 해당 섹션의 자습서가 나열 됩니다. `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤은이 기능을 제공 합니다. 솔루션 탐색기에서 디자인 뷰 페이지로 끌어서이 사용자 정의 컨트롤을 `Default.aspx`에 추가 합니다.

[SectionLevelTutorialListing 사용자 정의 컨트롤을 Default.aspx에 추가 ![](custom-buttons-in-the-datalist-and-repeater-cs/_static/image6.png)](custom-buttons-in-the-datalist-and-repeater-cs/_static/image5.png)

**그림 3**: `Default.aspx`에 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](custom-buttons-in-the-datalist-and-repeater-cs/_static/image7.png))

마지막으로 `Web.sitemap` 파일에 페이지를 항목으로 추가 합니다. 특히 DataList 및 Repeater `<siteMapNode>`를 사용 하 여 페이징 및 정렬 후에 다음 태그를 추가 합니다.

[!code-xml[Main](custom-buttons-in-the-datalist-and-repeater-cs/samples/sample1.xml)]

`Web.sitemap`업데이트 한 후 브라우저를 통해 자습서 웹 사이트를 잠시 기다려 주십시오. 이제 왼쪽의 메뉴에는 자습서 편집, 삽입 및 삭제를 위한 항목이 포함 되어 있습니다.

![이제 사이트 맵에 사용자 지정 단추 자습서에 대 한 항목이 포함 됩니다.](custom-buttons-in-the-datalist-and-repeater-cs/_static/image8.png)

**그림 4**: 이제 사이트 맵에 사용자 지정 단추 자습서에 대 한 항목이 포함 되어 있습니다.

## <a name="step-2-adding-the-list-of-categories"></a>2 단계: 범주 목록 추가

이 자습서에서는 클릭 하면 연결 된 범주 제품을 글머리 기호 목록에 표시 하는 모든 범주를 나열 하는 리피터를 만들어야 합니다. LinkButton 표시 합니다. 먼저 시스템의 범주를 나열 하는 간단한 리피터를 만들어 보겠습니다. 먼저 `CustomButtonsDataListRepeater` 폴더에서 `CustomButtons.aspx` 페이지를 엽니다. 도구 상자의 Repeater를 디자이너로 끌고 `ID` 속성을 `Categories`로 설정 합니다. 다음으로, Repeater s 스마트 태그에서 새 데이터 소스 컨트롤을 만듭니다. 특히 `CategoriesBLL` class s `GetCategories()` 메서드에서 데이터를 선택 하는 `CategoriesDataSource` 라는 새 ObjectDataSource 컨트롤을 만듭니다.

[범주 Bll 클래스 s GetCategories () 메서드를 사용 하도록 ObjectDataSource를 구성 ![](custom-buttons-in-the-datalist-and-repeater-cs/_static/image10.png)](custom-buttons-in-the-datalist-and-repeater-cs/_static/image9.png)

**그림 5**: `CategoriesBLL` 클래스 s `GetCategories()` 메서드를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](custom-buttons-in-the-datalist-and-repeater-cs/_static/image11.png))

Visual Studio에서 데이터 소스를 기반으로 기본 `ItemTemplate`을 만드는 DataList 컨트롤과는 달리, Repeater의 템플릿은 수동으로 정의 해야 합니다. 또한 Repeater의 템플릿은 선언적으로 만들고 편집 해야 합니다. 즉, Repeater의 스마트 태그에는 템플릿 편집 옵션이 없습니다.

왼쪽 아래 모서리에서 원본 탭을 클릭 하 고 `<h3>` 요소에 범주 이름을 표시 하는 `ItemTemplate`을 추가 하 고 단락 태그에 해당 설명을 추가 합니다. 각 범주 사이에 가로 규칙 (`<hr />`)을 표시 하는 `SeparatorTemplate`을 포함 합니다. 또한 제품을 표시 하도록 `Text` 속성이 설정 된 LinkButton를 추가 합니다. 이러한 단계를 완료 한 후 페이지의 선언 태그는 다음과 같습니다.

[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-cs/samples/sample2.aspx)]

그림 6에서는 브라우저를 통해 볼 때의 페이지를 보여 줍니다. 각 범주 이름 및 설명이 나열 됩니다. 제품 표시 단추를 클릭 하면 포스트백이 발생 하지만 아직 작업을 수행 하지는 않습니다.

[각 범주 이름 및 설명이 표시 되 고 제품 LinkButton 함께 표시 됩니다. ![](custom-buttons-in-the-datalist-and-repeater-cs/_static/image13.png)](custom-buttons-in-the-datalist-and-repeater-cs/_static/image12.png)

**그림 6**: 각 범주 이름 및 설명이 표시 됩니다. 여기에는 Show Products LinkButton ([전체 크기 이미지를 보려면 클릭](custom-buttons-in-the-datalist-and-repeater-cs/_static/image14.png))

## <a name="step-3-executing-server-side-logic-when-the-show-products-linkbutton-is-clicked"></a>3 단계: Products 표시 LinkButton를 클릭 하면 서버 쪽 논리 실행

DataList 또는 Repeater의 템플릿 내에서 단추, LinkButton 또는 ImageButton을 클릭할 때마다 포스트백이 발생 하 고 DataList 또는 Repeater s `ItemCommand` 이벤트가 발생 합니다. `ItemCommand` 이벤트 외에도, 단추 `CommandName` 속성이 예약 된 문자열 중 하나로 설정 된 경우 (삭제, 편집, 취소, 업데이트 또는 선택) DataList 컨트롤이 다른 특정 이벤트를 발생 시킬 수 있지만 `ItemCommand` 이벤트가 *항상* 발생 합니다.

DataList 또는 Repeater 내에서 단추를 클릭 하면 단추를 클릭 했을 때 (편집 및 삭제 단추와 같은 컨트롤에 여러 단추가 있을 수 있음) 및 일부 추가 정보 (예:)를 함께 전달 해야 하는 경우가 많습니다. 단추를 클릭 한 항목의 기본 키 값입니다. Button, LinkButton 및 ImageButton은 해당 값이 `ItemCommand` 이벤트 처리기에 전달 되는 두 개의 속성을 제공 합니다.

- 템플릿의 각 단추를 식별 하는 데 일반적으로 사용 되는 문자열 `CommandName`
- 기본 키 값과 같은 일부 데이터 필드의 값을 저장 하는 데 일반적으로 사용 되는 `CommandArgument`

이 예에서는 LinkButton s `CommandName` 속성을 ShowProducts로 설정 하 고, 데이터 바인딩 `CategoryArgument='<%# Eval("CategoryID") %>'`를 사용 하 여 `CategoryID` 현재 레코드의 기본 키 값을 `CommandArgument` 속성에 바인딩합니다. 이러한 두 속성을 지정한 후에는 LinkButton s 선언 구문이 다음과 같이 표시 됩니다.

[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-cs/samples/sample3.aspx)]

단추를 클릭 하면 포스트백이 발생 하 고 DataList 또는 Repeater s `ItemCommand` 이벤트가 발생 합니다. 이벤트 처리기에는 단추 `CommandName` 및 `CommandArgument` 값이 전달 됩니다.

Repeater s `ItemCommand` 이벤트에 대 한 이벤트 처리기를 만들고 이벤트 처리기로 전달 된 두 번째 매개 변수 (`e`)를 확인 합니다. 이 두 번째 매개 변수는 [`RepeaterCommandEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeatercommandeventargs.aspx) 형식 이며 다음 네 가지 속성을 포함 합니다.

- 클릭 한 단추 `CommandArgument` 속성의 값을 `CommandArgument` 합니다.
- 단추 `CommandName` 속성의 값을 `CommandName` 합니다.
- 클릭 한 단추 컨트롤에 대 한 참조를 `CommandSource` 합니다.
- 클릭 한 단추가 포함 된 [`RepeaterItem`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeateritem.aspx) 에 대 한 참조를 `Item` 합니다. Repeater에 바인딩된 각 레코드는 `RepeaterItem`로 매니페스트 됩니다.

선택한 범주 s `CategoryID` `CommandArgument` 속성을 통해 전달 되므로 `ItemCommand` 이벤트 처리기에서 선택한 범주와 관련 된 제품 집합을 가져올 수 있습니다. 그런 다음 이러한 제품은 `ItemTemplate`의 BulletedList 컨트롤에 바인딩될 수 있습니다 (추가 하기 위해 ve). 그런 다음, BulletedList를 추가 하 고, `ItemCommand` 이벤트 처리기에서 참조 하 고, 선택한 범주에 대 한 제품 집합에 바인딩하는 것은 4 단계에서 다룰 것입니다.

> [!NOTE]
> DataList s `ItemCommand` 이벤트 처리기에는 `RepeaterCommandEventArgs` 클래스와 동일한 네 가지 속성을 제공 하는 [`DataListCommandEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalistcommandeventargs.aspx)형식의 개체가 전달 됩니다.

## <a name="step-4-displaying-the-selected-category-s-products-in-a-bulleted-list"></a>4 단계: 선택한 범주 제품을 글머리 기호 목록에 표시

선택한 범주 s 제품은 원하는 수의 컨트롤을 사용 하 여 `ItemTemplate` 내에 표시 될 수 있습니다. 다른 중첩 된 Repeater, DataList, DropDownList, GridView 등을 추가할 수 있습니다. 그러나 제품을 글머리 기호 목록으로 표시 하려고 하기 때문에 BulletedList 컨트롤을 사용 합니다. `CustomButtons.aspx` 페이지의 선언적 태그로 돌아가면 제품 LinkButton 표시 후에 `ItemTemplate`에 BulletedList 컨트롤을 추가 합니다. BulletedLists s `ID`를 `ProductsInCategory`로 설정 합니다. BulletedList는 `DataTextField` 속성을 통해 지정 된 데이터 필드의 값을 표시 합니다. 이 컨트롤에는 제품 정보가 바인딩되어 있으므로 `DataTextField` 속성을 `ProductName`로 설정 합니다.

[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-cs/samples/sample4.aspx)]

`ItemCommand` 이벤트 처리기에서 `e.Item.FindControl("ProductsInCategory")`를 사용 하 여이 컨트롤을 참조 하 고 선택한 범주와 관련 된 제품 집합에 바인딩합니다.

[!code-csharp[Main](custom-buttons-in-the-datalist-and-repeater-cs/samples/sample5.cs)]

`ItemCommand` 이벤트 처리기에서 작업을 수행 하기 전에 먼저 들어오는 `CommandName`의 값을 확인 하는 것이 좋습니다. `ItemCommand` 이벤트 처리기는 단추를 클릭할 때 발생 하므로 템플릿에 *여러 단추가 있는* 경우 `CommandName` 값을 사용 하 여 수행할 작업을 파악 합니다. 단일 단추만 있으므로 여기에서 `CommandName`를 확인 하는 것이 좋지만 불과할. 그런 다음 선택한 범주의 `CategoryID` `CommandArgument` 속성에서 검색 됩니다. 그런 다음 템플릿의 BulletedList 컨트롤이 참조 되 고 `ProductsBLL` 클래스 `GetProductsByCategoryID(categoryID)` 메서드의 결과에 바인딩됩니다.

Datalist [에서 데이터 편집 및 삭제에 대 한 개요](../editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-cs.md)와 같이 datalist 내에서 단추를 사용 하는 이전 자습서에서는 `DataKeys` 컬렉션을 통해 지정 된 항목의 기본 키 값을 결정 했습니다. 이 접근 방식은 DataList에서 잘 작동 하지만, Repeater에는 `DataKeys` 속성이 없습니다. 대신, 기본 키 값을 제공 하는 대체 방법을 사용 해야 합니다. 예를 들어 `CommandArgument` 속성을 사용 하거나 템플릿 내의 숨겨진 Label 웹 컨트롤에 기본 키 값을 할당 하 고 `e.Item.FindControl("LabelID")`를 사용 하 여 `ItemCommand` 이벤트 처리기에서 해당 값을 다시 읽습니다.

`ItemCommand` 이벤트 처리기를 완료 한 후 잠시 브라우저에서이 페이지를 테스트 합니다. 그림 7에 표시 된 것 처럼 제품 표시 링크를 클릭 하면 포스트백이 발생 하 고 BulletedList에서 선택한 범주의 제품이 표시 됩니다. 또한이 제품 정보는 다른 범주 제품 링크를 클릭 한 경우에도 유지 됩니다.

> [!NOTE]
> 이 보고서의 동작을 수정 하 여 한 번에 하나의 범주 제품만 나열 되도록 하려면 BulletedList 컨트롤 s `EnableViewState` 속성을 `False`로 설정 하면 됩니다.

[BulletedList는 선택한 범주의 제품을 표시 하는 데 사용 됩니다. ![](custom-buttons-in-the-datalist-and-repeater-cs/_static/image16.png)](custom-buttons-in-the-datalist-and-repeater-cs/_static/image15.png)

**그림 7**: 선택한 범주의 제품을 표시 하는 데 사용 되는 BulletedList ([전체 크기 이미지를 보려면 클릭](custom-buttons-in-the-datalist-and-repeater-cs/_static/image17.png))

## <a name="summary"></a>요약

DataList 및 Repeater 컨트롤은 해당 템플릿 내에 원하는 수의 단추, Linkbutton 또는 ImageButtons를 포함할 수 있습니다. 이러한 단추를 클릭 하면 포스트백이 발생 하 고 `ItemCommand` 이벤트가 발생 합니다. 사용자 지정 서버 쪽 동작을 클릭 하는 단추와 연결 하려면 `ItemCommand` 이벤트에 대 한 이벤트 처리기를 만듭니다. 이 이벤트 처리기에서 먼저 들어오는 `CommandName` 값을 확인 하 여 클릭 한 단추를 확인 합니다. 선택적으로 단추 `CommandArgument` 속성을 통해 추가 정보를 제공할 수 있습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Dennis Patterson이입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [다음](custom-buttons-in-the-datalist-and-repeater-vb.md)
