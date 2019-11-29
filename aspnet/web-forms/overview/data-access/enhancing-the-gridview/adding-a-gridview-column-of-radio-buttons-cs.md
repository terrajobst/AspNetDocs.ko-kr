---
uid: web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-radio-buttons-cs
title: 라디오 단추의 GridView 열 추가 (C#) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 GridView 컨트롤에 라디오 단추 열을 추가 하 여 사용자에 게의 단일 행을 선택 하는 보다 직관적인 방법을 제공 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 03/06/2007
ms.assetid: 32377145-ec25-4715-8370-a1c590a331d5
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-radio-buttons-cs
msc.type: authoredcontent
ms.openlocfilehash: b59cc64b14c6414e6558fdb8a281644db8386701
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74593267"
---
# <a name="adding-a-gridview-column-of-radio-buttons-c"></a>라디오 단추의 GridView 열 추가(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_51_CS.exe) 또는 [PDF 다운로드](adding-a-gridview-column-of-radio-buttons-cs/_static/datatutorial51cs1.pdf)

> 이 자습서에서는 GridView 컨트롤에 라디오 단추 열을 추가 하 여 사용자에 게 GridView의 단일 행을 선택 하는 보다 직관적인 방법을 제공 하는 방법을 보여 줍니다.

## <a name="introduction"></a>소개

GridView 컨트롤은 다양 한 기본 제공 기능을 제공 합니다. 여기에는 텍스트, 이미지, 하이퍼링크 및 단추를 표시 하는 여러 가지 필드가 포함 됩니다. 추가 사용자 지정을 위한 템플릿을 지원 합니다. 마우스를 몇 번 클릭 하면 단추를 통해 각 행을 선택할 수 있는 GridView를 만들거나 기능을 편집 하거나 삭제할 수 있습니다. 제공 된 기능을 다양 한도 하지만 지원 되지 않는 추가 기능을 추가 해야 하는 경우가 종종 있습니다. 이 자습서 및 다음 두 가지에서는 추가 기능을 포함 하도록 GridView s 기능을 개선 하는 방법을 살펴보겠습니다.

이 자습서와 다음은 행 선택 프로세스를 개선 하는 데 중점을 두는 것입니다. [DetailView 세부 정보를 사용 하 여 선택 가능한 마스터 GridView를 사용 하 여 마스터/세부](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)정보에서 검토 한 대로 선택 단추가 포함 된 GridView에 commandfield를 추가할 수 있습니다. 이 단추를 클릭 하면 다시 게시 ensues 및 GridView s `SelectedIndex` 속성이 해당 선택 단추를 클릭 한 행의 인덱스로 업데이트 됩니다. [세부 정보 DetailView 자습서와 함께 선택 가능한 마스터 GridView를 사용 하는 마스터/세부](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md) 정보에서이 기능을 사용 하 여 선택한 GridView 행의 세부 정보를 표시 하는 방법을 살펴보았습니다.

선택 단추는 다양 한 상황에서 작동 하지만 다른 작업에도 작동 하지 않을 수 있습니다. 단추를 사용 하는 대신 두 개의 다른 사용자 인터페이스 요소 (라디오 단추 및 확인란)를 선택 하는 데 주로 사용 됩니다. 선택 단추 대신 각 행에 라디오 단추나 확인란이 포함 되도록 GridView를 확장할 수 있습니다. 사용자가 GridView 레코드 중 하나만 선택할 수 있는 시나리오에서는 선택 단추 보다 라디오 단추가 선호 될 수 있습니다. 사용자가 웹 기반 전자 메일 응용 프로그램에서와 같은 여러 레코드를 선택할 수 있는 경우, 사용자가 여러 메시지를 선택 하 여 삭제할 수 있습니다. 확인란은 선택 단추 또는 라디오 단추에서 사용할 수 없는 기능을 제공 합니다. 사용자 인터페이스.

이 자습서에서는 GridView에 라디오 단추 열을 추가 하는 방법을 살펴봅니다. 계속 해 서 자습서에서 확인란을 사용 하는 방법을 살펴봅니다.

## <a name="step-1-creating-the-enhancing-the-gridview-web-pages"></a>1 단계: GridView 웹 페이지 향상 만들기

라디오 단추 열을 포함 하도록 GridView를 개선 하기 전에 먼저이 자습서와 다음 두 가지에 필요한 웹 사이트 프로젝트에 ASP.NET 페이지를 만들어 보겠습니다. `EnhancedGridView`이라는 새 폴더를 추가 하 여 시작 합니다. 그런 다음, 다음 ASP.NET 페이지를 해당 폴더에 추가 하 여 각 페이지를 `Site.master` 마스터 페이지에 연결 합니다.

- `Default.aspx`
- `RadioButtonField.aspx`
- `CheckBoxField.aspx`
- `InsertThroughFooter.aspx`

![SqlDataSource 관련 자습서에 대 한 ASP.NET 페이지 추가](adding-a-gridview-column-of-radio-buttons-cs/_static/image1.gif)

**그림 1**: SqlDataSource 관련 자습서에 대 한 ASP.NET 페이지 추가

다른 폴더와 마찬가지로 `EnhancedGridView` 폴더의 `Default.aspx`에는 해당 섹션의 자습서가 나열 됩니다. `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤은이 기능을 제공 합니다. 따라서이 사용자 정의 컨트롤을 솔루션 탐색기에서 페이지 디자인 뷰로 끌어 `Default.aspx`에 추가 합니다.

[SectionLevelTutorialListing 사용자 정의 컨트롤을 Default.aspx에 추가 ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image2.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image1.png)

**그림 2**: `Default.aspx`에 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-cs/_static/image2.png))

마지막으로, 이러한 4 개의 페이지를 `Web.sitemap` 파일에 항목으로 추가 합니다. 특히, SqlDataSource 컨트롤을 사용 하 여 뒤에 다음 태그를 추가 `<siteMapNode>`합니다.

[!code-xml[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample1.xml)]

`Web.sitemap`업데이트 한 후 브라우저를 통해 자습서 웹 사이트를 잠시 기다려 주십시오. 이제 왼쪽의 메뉴에는 자습서 편집, 삽입 및 삭제를 위한 항목이 포함 되어 있습니다.

![이제 사이트 맵에 GridView 자습서 향상을 위한 항목이 포함 되어 있습니다.](adding-a-gridview-column-of-radio-buttons-cs/_static/image3.gif)

**그림 3**: 이제 GridView 자습서 향상을 위한 항목을 포함 하는 사이트 맵

## <a name="step-2-displaying-the-suppliers-in-a-gridview"></a>2 단계: GridView에서 공급자 표시

이 자습서에서는를 사용 하 여 USA의 공급자를 나열 하는 GridView를 빌드하고 각 GridView 행에서 라디오 단추를 제공 합니다. 라디오 단추를 통해 공급자를 선택 하면 사용자가 단추를 클릭 하 여 공급 업체 제품을 볼 수 있습니다. 이 작업을 수행 하는 것은 간단 하지만 특히 복잡 한 여러 가지 미묘한 방법이 있습니다. 이러한 세부 사항을 살펴보기 전에 먼저 공급자를 나열 하는 GridView를 가져옵니다.

먼저 `EnhancedGridView` 폴더에서 `RadioButtonField.aspx` 페이지를 열고 도구 상자에서 디자이너로 끌어 옵니다. GridView s `ID`를 `Suppliers`로 설정 하 고 스마트 태그에서 새 데이터 원본을 만들도록 선택 합니다. 특히 `SuppliersBLL` 개체에서 데이터를 가져오는 `SuppliersDataSource` 라는 ObjectDataSource를 만듭니다.

[SuppliersDataSource 라는 새 ObjectDataSource를 만들 ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image4.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image3.png)

**그림 4**: 이름이 `SuppliersDataSource` 새 ObjectDataSource 만들기 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-cs/_static/image4.png))

[SuppliersBLL 클래스를 사용 하도록 ObjectDataSource 구성 ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image5.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image5.png)

**그림 5**: `SuppliersBLL` 클래스를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-cs/_static/image6.png))

해당 공급자를 USA에만 나열 하려면 선택 탭의 드롭다운 목록에서 `GetSuppliersByCountry(country)` 메서드를 선택 합니다.

[SuppliersBLL 클래스를 사용 하도록 ObjectDataSource 구성 ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image6.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image7.png)

**그림 6**: `SuppliersBLL` 클래스를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-cs/_static/image8.png))

업데이트 탭에서 (없음) 옵션을 선택 하 고 다음을 클릭 합니다.

[SuppliersBLL 클래스를 사용 하도록 ObjectDataSource 구성 ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image7.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image9.png)

**그림 7**: `SuppliersBLL` 클래스를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-cs/_static/image10.png))

`GetSuppliersByCountry(country)` 메서드는 매개 변수를 허용 하므로 데이터 원본 구성 마법사에서 해당 매개 변수의 원본을 확인 하는 메시지를 표시 합니다. 하드 코드 된 값 (이 예제에서는 USA)을 지정 하려면 매개 변수 원본 드롭다운 목록을 없음으로 설정 된 채로 두고 텍스트 상자에 기본값을 입력 합니다. 마침을 클릭하여 마법사를 완료합니다.

[country 매개 변수의 기본값으로 USA를 사용 ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image8.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image11.png)

**그림 8**: `country` 매개 변수의 기본값으로 USA 사용 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-cs/_static/image12.png))

마법사를 완료 한 후 GridView에는 각 공급자 데이터 필드에 대 한 BoundField 포함 됩니다. `CompanyName`, `City`및 `Country` BoundFields를 제외한 모든을 제거 하 고 `CompanyName` BoundFields `HeaderText` 속성의 이름을 공급자로 바꿉니다. 이렇게 하 고 나면 GridView 및 ObjectDataSource 선언 구문이 다음과 같이 표시 됩니다.

[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample2.aspx)]

이 자습서에서는 사용자가 공급자 목록과 동일한 페이지 또는 다른 페이지에서 선택한 공급자 제품을 볼 수 있도록 허용 합니다. 이를 수용 하려면 두 개의 단추 웹 컨트롤을 페이지에 추가 합니다. 이러한 두 단추의 `ID` s를 `ListProducts` 및 `SendToProducts`으로 설정 했습니다. `ListProducts`를 클릭 하면 포스트백이 발생 하 고 선택한 공급자 제품이 동일한 페이지에 나열 되지만 `SendToProducts`를 클릭 하면 해당 제품을 나열 하는 다른 페이지로 whisked 됩니다.

그림 9에서는 브라우저를 통해 볼 때 `Suppliers` GridView와 두 개의 단추 웹 컨트롤을 보여 줍니다.

[미국의 해당 공급 업체에 게 이름, 구/군/시 및 국가 정보가 나열 되어 ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image9.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image13.png)

**그림 9**: 미국의 이름, 구/군/시 및 국가 정보가 나열 된 공급 업체 ([전체 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-cs/_static/image14.png))

## <a name="step-3-adding-a-column-of-radio-buttons"></a>3 단계: 라디오 단추 열 추가

이 시점에서 `Suppliers` GridView에는 미국의 각 공급 업체의 회사 이름, 도시 및 국가를 표시 하는 세 가지 BoundFields 있습니다. 그러나 여전히 라디오 단추 열은 없습니다. 아쉽게도 GridView는 기본 제공 RadioButtonField를 포함 하지 않습니다. 그렇지 않은 경우에는이를 그리드에 추가 하 고 수행 하면 됩니다. 대신 Templatefield로 변환를 추가 하 고 해당 `ItemTemplate`를 구성 하 여 라디오 단추를 렌더링 하 여 각 GridView 행의 라디오 단추를 만들 수 있습니다.

처음에는 Templatefield로 변환의 `ItemTemplate`에 RadioButton 웹 컨트롤을 추가 하 여 원하는 사용자 인터페이스를 구현할 수 있다고 가정할 수 있습니다. 이 경우 GridView의 각 행에 단일 라디오 단추가 추가 되지만 라디오 단추는 그룹화 할 수 없기 때문에 함께 사용할 수 없습니다. 즉, 최종 사용자가 GridView에서 동시에 여러 라디오 단추를 선택할 수 있습니다.

RadioButton 웹 컨트롤을 사용 하는 경우에도 필요한 기능이 제공 되지 않지만, 결과 라디오 단추가 그룹화 되지 않은 이유를 확인 하는 것이 Templatefield로 변환이 방법을 구현 해 보겠습니다. 먼저 Suppliers GridView에 Templatefield로 변환를 추가 하 여 가장 왼쪽에 있는 필드를 만듭니다. 그런 다음 GridView의 스마트 태그에서 템플릿 편집 링크를 클릭 하 고 도구 상자에서 Templatefield로 변환 s `ItemTemplate`로 RadioButton 웹 컨트롤을 끕니다 (그림 10 참조). RadioButton s `ID` 속성을 `RowSelector`로 설정 하 고 `GroupName` 속성을 `SuppliersGroup`로 설정 합니다.

[ItemTemplate에 RadioButton 웹 컨트롤을 추가 ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image10.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image15.png)

**그림 10**: `ItemTemplate`에 RadioButton 웹 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-cs/_static/image16.png))

디자이너를 통해 이러한 추가 작업을 수행한 후에는 GridView의 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample3.aspx)]

RadioButton s [`GroupName` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.radiobutton.groupname(VS.80).aspx) 은 일련의 라디오 단추를 그룹화 하는 데 사용 됩니다. `GroupName` 값이 같은 모든 RadioButton 컨트롤은 그룹화 된 것으로 간주 됩니다. 한 번에 하나의 라디오 단추만 그룹에서 선택할 수 있습니다. `GroupName` 속성은 렌더링 된 라디오 단추 `name` 특성의 값을 지정 합니다. 브라우저는 라디오 단추 `name` 특성을 검사 하 여 라디오 단추 그룹화를 결정 합니다.

`ItemTemplate`에 RadioButton 웹 컨트롤이 추가 된 상태에서 브라우저를 통해이 페이지를 방문 하 여 표 형태의 행에 있는 라디오 단추를 클릭 합니다. 그림 11에 표시 된 것 처럼 라디오 단추가 그룹화 되지 않아 모든 행을 선택할 수 있도록 합니다.

[GridView s 라디오 단추가 그룹화 되지 ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image11.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image17.png)

**그림 11**: GridView s 라디오 단추가 그룹화 되지 않음 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-cs/_static/image18.png))

라디오 단추가 그룹화 되지 않는 이유는 동일한 `GroupName` 속성 설정이 있더라도 렌더링 된 `name` 특성이 서로 다르기 때문입니다. 이러한 차이점을 확인 하려면 브라우저에서 뷰/소스를 수행 하 고 라디오 단추 태그를 검사 합니다.

[!code-html[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample4.html)]

`name` 및 `id` 특성이 속성 창에 지정 된 정확한 값이 아니라 다른 `ID` 값이 앞에 표시 되는 것을 확인할 수 있습니다. 렌더링 된 `id` 및 `name` 특성의 앞에 추가 `ID` 값이 추가 되는 `ID`의 라디오 단추는 부모 컨트롤 `GridViewRow` s, GridView s `ID`, 콘텐츠 컨트롤의 `ID`및 웹 폼을 `ID`합니다. GridView의 렌더링 된 각 웹 컨트롤에는 고유한 `id` 및 `name` 값이 있도록 이러한 `ID`가 추가 됩니다.

렌더링 되는 각 컨트롤에는 다른 `name`와 `id` 필요 합니다 .이는 브라우저에서 클라이언트 쪽의 각 컨트롤을 고유 하 게 식별 하는 방법과 웹 서버에서 다시 게시할 때 발생 하는 작업 또는 변경 작업을 식별 하는 방법 이기 때문입니다. 예를 들어 RadioButton의 선택 상태가 변경 될 때마다 일부 서버 쪽 코드를 실행 하려고 한다고 가정 합니다. RadioButton s `AutoPostBack` 속성을 `true`로 설정 하 고 `CheckChanged` 이벤트에 대 한 이벤트 처리기를 만들어이를 수행할 수 있습니다. 그러나 모든 라디오 단추에 대해 렌더링 된 `name` 및 `id` 값이 동일 하면 다시 게시할 때 클릭 한 특정 RadioButton을 확인할 수 없습니다.

이 중에서 가장 짧은 것은 RadioButton 웹 컨트롤을 사용 하 여 GridView에서 라디오 단추 열을 만들 수 없다는 것입니다. 대신, 낡은 기술을 사용 하 여 각 GridView 행에 적절 한 태그가 삽입 되도록 해야 합니다.

> [!NOTE]
> RadioButton 웹 컨트롤과 마찬가지로, 서식 파일에 추가 될 때 라디오 단추 HTML 컨트롤은 고유한 `name` 특성을 포함 하 여 모눈의 라디오 단추를 그룹화 하지 않습니다. Html 컨트롤을 잘 모르는 경우 특히 ASP.NET 2.0에서 HTML 컨트롤이 거의 사용 되지 않으므로이 메모는 무시 해도 됩니다. 하지만 더 자세히 알아보려면 [Allen](http://odetocode.com/blogs/scott/default.aspx) 의 블로그 항목 [웹 컨트롤 및 HTML 컨트롤](http://www.odetocode.com/Articles/348.aspx)을 참조 하세요.

## <a name="using-a-literal-control-to-inject-radio-button-markup"></a>리터럴 컨트롤을 사용 하 여 라디오 단추 태그 삽입

GridView 내의 모든 라디오 단추를 올바르게 그룹화 하려면 `ItemTemplate`라디오 단추 태그를 수동으로 삽입 해야 합니다. 각 라디오 단추에는 동일한 `name` 특성이 필요 하지만 클라이언트 쪽 스크립트를 통해 라디오 단추에 액세스 하려는 경우 고유한 `id` 특성이 있어야 합니다. 사용자가 라디오 단추를 선택 하 고 페이지를 포스트백 한 후 브라우저는 선택한 라디오 단추 `value` 특성의 값을 다시 보냅니다. 따라서 각 라디오 단추에는 고유한 `value` 특성이 필요 합니다. 마지막으로, 다시 게시 시 선택 된 라디오 단추 하나에 `checked` 특성을 추가 해야 합니다. 그렇지 않으면 사용자가 선택 하 여 다시 게시 한 후 라디오 단추가 기본 상태로 돌아갑니다 (모두 선택 취소 됨).

하위 수준 태그를 템플릿에 삽입 하기 위해 수행할 수 있는 두 가지 방법이 있습니다. 하나는 코드를 혼합 하 고 코드를 표시 하는 클래스에 정의 된 형식 지정 메서드를 호출 하는 것입니다. 이 기술은 [GridView 컨트롤 자습서의 템플릿 사용 필드](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md) 에서 처음으로 설명 했습니다. 이 경우 다음과 같은 내용이 표시 될 수 있습니다.

[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample5.aspx)]

여기서 `GetUniqueRadioButton` 및 `GetRadioButtonValue`은 적절 한 `id`을 반환 하 고 각 라디오 단추에 대 한 특성 값을 `value` 코드를 만든 클래스에서 정의 되는 메서드입니다. 이 방법은 `id` 및 `value` 특성을 할당 하는 데 적합 하지만 데이터 바인딩 구문은 데이터를 GridView에 처음 바인딩할 때만 실행 되므로 `checked` 특성 값을 지정 해야 하는 경우에는 짧습니다. 따라서 GridView에서 뷰 상태를 사용 하는 경우 페이지를 처음 로드할 때 (또는 GridView를 데이터 소스에 명시적으로 다시 바인딩할 때)에만 서식 지정 메서드가 실행 되므로 `checked` 특성을 설정 하는 함수는 포스트백 시 호출 되지 않습니다. 이 문서의 범위를 벗어나는 다소 미묘한 문제 이며,이에 대해서는 그대로 둡니다. 하지만 위의 방법을 사용 하 여 중단 되는 지점으로 작업 하는 것이 좋습니다. 이러한 연습을 통해 작업 버전이 더 이상 표시 되지 않지만 GridView와 데이터 바인딩 수명 주기를 보다 깊이 있게 이해할 수 있습니다.

템플릿에 사용자 지정, 하위 수준 마크업을 삽입 하는 다른 방법은 템플릿에 [리터럴 컨트롤](https://msdn.microsoft.com/library/sz4949ks(VS.80).aspx) 을 추가 하는 것입니다. 그런 다음 GridView s `RowCreated` 또는 `RowDataBound` 이벤트 처리기에서 리터럴 컨트롤에 프로그래밍 방식으로 액세스 하 고 `Text` 속성을 내보낼 태그로 설정할 수 있습니다.

Templatefield로 변환 s `ItemTemplate`에서 RadioButton을 제거 하 여 시작 하 고 리터럴 컨트롤로 바꿉니다. 리터럴 컨트롤 `ID` `RadioButtonMarkup`로 설정 합니다.

[ItemTemplate에 리터럴 컨트롤을 추가 ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image12.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image19.png)

**그림 12**: `ItemTemplate`에 리터럴 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-cs/_static/image20.png))

다음으로, GridView s `RowCreated` 이벤트에 대 한 이벤트 처리기를 만듭니다. 데이터를 GridView로 바인딩 하는지 여부에 관계 없이 추가 된 모든 행에 대해 `RowCreated` 이벤트가 한 번 발생 합니다. 즉, 뷰 상태에서 데이터를 다시 로드 하는 경우에도 `RowCreated` 이벤트가 계속 발생 하 고이를 사용 하는 이유는 데이터가 데이터 웹 컨트롤에 명시적으로 바인딩되는 경우에만 발생 하는 `RowDataBound` 대신 사용 하는 것입니다.

이 이벤트 처리기에서는 데이터 행을 다시 처리 하는 경우에만 계속 진행 하려고 합니다. 각 데이터 행에 대해 프로그래밍 방식으로 `RadioButtonMarkup` 리터럴 컨트롤을 참조 하 고 `Text` 속성을 내보낼 태그로 설정 합니다. 다음 코드에서 보여 주는 것 처럼 내보낸 태그는 `name` 특성이 `SuppliersGroup`로 설정 된 라디오 단추를 만듭니다 .이 단추는 `id` 특성이 `RowSelectorX`로 설정 됩니다. 여기서 *X* 는 gridview 행의 인덱스이 고 `value` 특성은 gridview 행의 인덱스로 설정 합니다.

[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample6.cs)]

GridView 행을 선택 하 고 포스트백이 발생 하면 선택한 공급자의 `SupplierID`에 관심이 있습니다. 따라서 각 라디오 단추의 값이 GridView 행의 인덱스 대신 실제 `SupplierID` 이어야 한다고 생각할 수 있습니다. 이는 특정 상황에서 작동할 수 있지만 `SupplierID`를 무조건 수락 하 고 처리 하는 것은 보안상 위험할 수 있습니다. 예를 들어, GridView에는 미국의 공급 업체만 나열 됩니다. 그러나 `SupplierID` 라디오 단추에서 직접 전달 되는 경우 다시 게시 시 다시 전송 된 `SupplierID` 값을 짓궂은 사용자가 조작 하지 않는 것은 무엇 인가요? 행 인덱스를 `value`로 사용 하 고 `DataKeys` 컬렉션에서 다시 게시를 `SupplierID` 가져오는 경우 사용자가 GridView 행 중 하 나와 연결 된 `SupplierID` 값 중 하나를 사용 하도록 할 수 있습니다.

이 이벤트 처리기 코드를 추가한 후에는 브라우저에서 페이지를 테스트 하는 데 1 분 정도 걸립니다. 첫째, 표에 있는 라디오 단추를 한 번에 하나만 선택할 수 있습니다. 그러나 라디오 단추를 선택 하 고 단추 중 하나를 클릭 하면 포스트백이 발생 하 고 라디오 단추가 모두 초기 상태로 돌아갑니다. 즉, 다시 게시 시 선택한 라디오 단추가 더 이상 선택 되지 않습니다. 이 문제를 해결 하려면 다시 게시에서 보낸 선택한 라디오 단추 인덱스를 검사 하 고 행 인덱스 일치 항목의 내보낸 태그에 `checked="checked"` 특성을 추가 하도록 `RowCreated` 이벤트 처리기를 보강 해야 합니다.

포스트백이 발생 하면 브라우저는 `name`를 다시 보내고 선택한 라디오 단추를 `value` 합니다. `Request.Form["name"]`를 사용 하 여 프로그래밍 방식으로 값을 검색할 수 있습니다. [`Request.Form` 속성](https://msdn.microsoft.com/library/system.web.httprequest.form.aspx) 은 폼 변수를 나타내는 [`NameValueCollection`](https://msdn.microsoft.com/library/system.collections.specialized.namevaluecollection.aspx) 를 제공 합니다. 폼 변수는 웹 페이지에 있는 양식 필드의 이름 및 값 이며, 다시 게시가 ensues 때마다 웹 브라우저에서 다시 보냅니다. GridView에 있는 라디오 단추의 렌더링 된 `name` 특성이 `SuppliersGroup`되기 때문에 웹 페이지가 다시 게시 될 때 브라우저는 다른 폼 필드와 함께 웹 서버로 `SuppliersGroup=valueOfSelectedRadioButton`을 다시 보냅니다. 그러면 `Request.Form["SuppliersGroup"]`를 사용 하 여 `Request.Form` 속성에서이 정보에 액세스할 수 있습니다.

`RowCreated` 이벤트 처리기 뿐만 아니라 단추 웹 컨트롤에 대 한 `Click` 이벤트 처리기에서 선택 된 라디오 단추 인덱스를 확인 해야 하므로, 라디오 단추 중 하나를 선택한 경우 라디오 단추가 선택 되어 있지 않은 경우 `-1`를 반환 하는 코드 숨김이 클래스에 `SuppliersSelectedIndex` 속성을 추가 합니다.

[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample7.cs)]

이 속성이 추가 되 면 `SuppliersSelectedIndex` `e.Row.RowIndex`같을 때 `RowCreated` 이벤트 처리기에 `checked="checked"` 태그를 추가 하는 것을 알 수 있습니다. 이 논리를 포함 하도록 이벤트 처리기를 업데이트 합니다.

[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample8.cs)]

이렇게 변경 하면 다시 게시 후 선택한 라디오 단추가 선택 된 상태로 유지 됩니다. 선택 된 라디오 단추를 지정 하는 기능이 있으므로 페이지를 처음 방문할 때 첫 번째 GridView 행의 라디오 단추가 선택 됩니다 .이 단추는 기본적으로 선택 되어 있지 않고 현재는 현재 동작). 첫 번째 라디오 단추를 기본적으로 선택 하려면 `if (SuppliersSelectedIndex == e.Row.RowIndex)` 문을 `if (SuppliersSelectedIndex == e.Row.RowIndex || (!Page.IsPostBack && e.Row.RowIndex == 0))`으로 변경 하면 됩니다.

이 시점에서 gridview에 그룹화 된 라디오 단추 열을 추가 하 여 다시 게시 간에 단일 GridView 행을 선택 하 고 기억할 수 있습니다. 다음 단계는 선택한 공급자가 제공 하는 제품을 표시 하는 것입니다. 4 단계에서는 사용자를 다른 페이지로 리디렉션하는 방법에 대해 설명 하 고, 선택 된 `SupplierID`따라 보냅니다. 5 단계에서는 선택한 공급자 제품을 동일한 페이지의 GridView에 표시 하는 방법을 알아봅니다.

> [!NOTE]
> Templatefield로 변환를 사용 하는 대신 (이 긴 3 단계를 중심으로) 적절 한 사용자 인터페이스 및 기능을 렌더링 하는 사용자 지정 `DataControlField` 클래스를 만들 수 있습니다. [`DataControlField` 클래스](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datacontrolfield.aspx) 는 BoundField, CheckBoxField, templatefield로 변환 및 기타 기본 제공 GridView 및 DetailsView 필드가 파생 되는 기본 클래스입니다. 사용자 지정 `DataControlField` 클래스를 만들면 라디오 단추 열을 선언 구문을 사용 하 여 추가 하 고 다른 웹 페이지 및 다른 웹 응용 프로그램에 대 한 기능을 훨씬 쉽게 복제할 수 있습니다.

그러나 ASP.NET에서 컴파일된 사용자 지정 컨트롤을 만든 경우에는 상당한 양의 투자할가 필요 하 고 신중 하 게 처리 해야 하는 세부 및에 지 사례 호스트로 전달 됩니다. 따라서 지금은 라디오 단추 열을은 선형화 사용자 지정 `DataControlField` 클래스로 구현 하 고 Templatefield로 변환 옵션을 사용 하는 것이 좋습니다. 아마도 향후 자습서에서 사용자 지정 `DataControlField` 클래스를 만들고, 사용 하 고, 배포 하는 방법을 살펴볼 수 있습니다.

## <a name="step-4-displaying-the-selected-supplier-s-products-in-a-separate-page"></a>4 단계: 별도의 페이지에 선택한 공급자 제품 표시

사용자가 GridView 행을 선택한 후에는 선택한 공급 업체 제품을 표시 해야 합니다. 경우에 따라 별도의 페이지에 이러한 제품을 표시 하는 것이 좋을 수도 있습니다. 먼저 개별 페이지에서 제품을 표시 하는 방법을 살펴보겠습니다. 5 단계에서는 선택한 공급자 제품을 표시 하기 위해 `RadioButtonField.aspx`에 GridView를 추가 하는 방법을 살펴보겠습니다.

현재 페이지 `ListProducts` 및 `SendToProducts`에는 두 개의 단추 웹 컨트롤이 있습니다. `SendToProducts` 단추를 클릭 하면 `~/Filtering/ProductsForSupplierDetails.aspx`사용자를 전송 하려고 합니다. 이 페이지는 [두 페이지에서 마스터/세부 정보 필터링](../masterdetail/master-detail-filtering-across-two-pages-cs.md) 자습서에 생성 되었으며 `SupplierID`라는 querystring 필드를 통해 `SupplierID` 전달 되는 공급자에 대 한 제품을 표시 합니다.

이 기능을 제공 하려면 `SendToProducts` Button s `Click` 이벤트에 대 한 이벤트 처리기를 만듭니다. 3 단계에서는 라디오 단추가 선택 된 행의 인덱스를 반환 하는 `SuppliersSelectedIndex` 속성을 추가 했습니다. 해당 `SupplierID`는 GridView의 `DataKeys` 컬렉션에서 검색할 수 있으며, 사용자는 `Response.Redirect("url")`를 사용 하 여 `~/Filtering/ProductsForSupplierDetails.aspx?SupplierID=SupplierID`으로 보낼 수 있습니다.

[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample9.cs)]

이 코드는 GridView에서 라디오 단추 중 하나를 선택 하는 한 wonderfully 작동 합니다. 처음에 GridView에 라디오 단추가 선택 되어 있지 않은 경우 사용자가 `SendToProducts` 단추를 클릭 하면 `SuppliersSelectedIndex` `-1`됩니다. 그러면 `-1`가 `DataKeys` 컬렉션의 인덱스 범위를 벗어나면 예외가 throw 됩니다. 그러나이는 기본적으로 GridView의 첫 번째 라디오 단추를 선택 하는 것 처럼 3 단계에서 설명한 대로 `RowCreated` 이벤트 처리기를 업데이트 하기로 결정 한 경우에는 문제가 되지 않습니다.

`-1`의 `SuppliersSelectedIndex` 값을 수용 하려면 GridView 위의 페이지에 Label 웹 컨트롤을 추가 합니다. `ID` 속성을 `ChooseSupplierMsg`, 해당 `CssClass` 속성을 `Warning`로 설정 하 고, 해당 `EnableViewState` 및 `Visible` 속성을 `false`로 설정 하 고, 해당 `Text` 속성을 표에서 공급자를 선택 합니다. CSS 클래스 `Warning`는 텍스트를 빨강, 기울임꼴, 굵은 글꼴로 표시 하 고 `Styles.css`에 정의 되어 있습니다. `EnableViewState` 및 `Visible` 속성을 `false`로 설정 하면 컨트롤의 `Visible` 속성을 프로그래밍 방식으로 `true`으로 설정 하는 포스트백만 제외 하 고 레이블이 렌더링 되지 않습니다.

[GridView 위에 레이블 웹 컨트롤을 추가 ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image13.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image21.png)

**그림 13**: GridView 위에 레이블 웹 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-cs/_static/image22.png))

다음으로 `Click` 이벤트 처리기를 늘려 `SuppliersSelectedIndex`이 0 보다 작은 경우 `ChooseSupplierMsg` 레이블을 표시 하 고, 그렇지 않은 경우 `~/Filtering/ProductsForSupplierDetails.aspx?SupplierID=SupplierID` 사용자를 리디렉션합니다.

[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample10.cs)]

브라우저에서 페이지를 방문 하 고 GridView에서 공급자를 선택 하기 전에 `SendToProducts` 단추를 클릭 합니다. 그림 14와 같이 `ChooseSupplierMsg` 레이블을 표시 합니다. 그런 다음 공급자를 선택 하 고 `SendToProducts` 단추를 클릭 합니다. 그러면 선택한 공급자가 제공 하는 제품을 나열 하는 페이지로 whisk 됩니다. 그림 15에서는 Breweries 공급자가 선택 된 경우의 `ProductsForSupplierDetails.aspx` 페이지를 보여 줍니다.

[공급자를 선택 하지 않은 경우 ChooseSupplierMsg 레이블이 표시 ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image14.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image23.png)

**그림 14**: 공급자를 선택 하지 않은 경우 `ChooseSupplierMsg` 레이블이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-cs/_static/image24.png)).

[선택한 공급자 제품 ![ProductsForSupplierDetails에 표시 됩니다.](adding-a-gridview-column-of-radio-buttons-cs/_static/image15.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image25.png)

**그림 15**: 선택한 공급자 제품이 `ProductsForSupplierDetails.aspx` 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-cs/_static/image26.png)).

## <a name="step-5-displaying-the-selected-supplier-s-products-on-the-same-page"></a>5 단계: 같은 페이지에서 선택한 공급 업체 제품 표시

4 단계에서는 사용자를 다른 웹 페이지에 전송 하 여 선택한 공급 업체 제품을 표시 하는 방법을 살펴보았습니다. 또는 선택한 공급자의 제품을 동일한 페이지에 표시할 수 있습니다. 이를 설명 하기 위해 `RadioButtonField.aspx`에 다른 GridView를 추가 하 여 선택한 공급 업체 제품을 표시 합니다.

공급자가 선택 된 후에만이 제품 GridView를 표시 하려면 `Suppliers` GridView 아래에 Panel 웹 컨트롤을 추가 하 고 해당 `ID`를 `ProductsBySupplierPanel`로 설정 하 고 `Visible` 속성을 `false`로 설정 합니다. 패널 내에서 선택한 공급자에 대 한 텍스트 제품을 추가한 다음 이름이 `ProductsBySupplier`인 GridView를 추가 합니다. GridView s 스마트 태그에서을 선택 하 여 `ProductsBySupplierDataSource`라는 새 ObjectDataSource에 바인딩합니다.

[ProductsBySupplier GridView를 새 ObjectDataSource에 바인딩 ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image16.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image27.png)

**그림 16**: 새 ObjectDataSource에 `ProductsBySupplier` GridView 바인딩 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-cs/_static/image28.png))

다음으로 `ProductsBLL` 클래스를 사용 하도록 ObjectDataSource를 구성 합니다. 선택한 공급자가 제공 하는 제품만 검색 하려고 하기 때문에 ObjectDataSource가 해당 데이터를 검색 하는 `GetProductsBySupplierID(supplierID)` 메서드를 호출 하도록 지정 합니다. 업데이트, 삽입 및 삭제 탭의 드롭다운 목록에서 (없음)을 선택 합니다.

[GetProductsBySupplierID (공급자) 메서드를 사용 하도록 ObjectDataSource를 구성 ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image17.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image29.png)

**그림 17**: `GetProductsBySupplierID(supplierID)` 메서드를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-cs/_static/image30.png))

[업데이트, 삽입 및 삭제 탭에서 드롭다운 목록을 (없음)으로 설정 ![](adding-a-gridview-column-of-radio-buttons-cs/_static/image18.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image31.png)

**그림 18**: 업데이트, 삽입 및 삭제 탭에서 드롭다운 목록을 (없음)으로 설정 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-cs/_static/image32.png))

SELECT, UPDATE, INSERT 및 DELETE 탭을 구성한 후 다음을 클릭 합니다. `GetProductsBySupplierID(supplierID)` 메서드에는 입력 매개 변수가 필요 하므로 데이터 원본 만들기 마법사에서 매개 변수 값의 원본을 지정 하 라는 메시지를 표시 합니다.

여기에는 매개 변수 값의 원본을 지정 하는 몇 가지 옵션이 있습니다. 기본 매개 변수 개체를 사용 하 고 `SuppliersSelectedIndex` 속성 값을 ObjectDataSource s `Selecting` 이벤트 처리기의 매개 변수 `DefaultValue` 속성에 프로그래밍 방식으로 할당할 수 있습니다. ObjectDataSource의 매개 변수 값을 프로그래밍 방식으로 지정 하려면 리프레셔에 대해 [objectdatasource의 매개 변수 값 자습서를 프로그래밍 방식](../basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-cs.md) 으로 다시 참조 하세요.

또는 ControlParameter를 사용 하 고 `Suppliers` GridView s [`SelectedValue` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedvalue.aspx) 을 참조할 수 있습니다 (그림 19 참조). GridView s `SelectedValue` 속성은 [`SelectedIndex` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedindex.aspx)에 해당 하는 `DataKey` 값을 반환 합니다. 이 옵션이 작동 하려면 `ListProducts` 단추를 클릭할 때 GridView s `SelectedIndex` 속성을 선택 된 행으로 프로그래밍 방식으로 설정 해야 합니다. 추가 된 혜택으로, `SelectedIndex`설정 하 여 선택한 레코드는 `DataWebControls` 테마 (노란색 배경)에 정의 된 `SelectedRowStyle`에 적용 됩니다.

[ControlParameter를 사용 하 ![GridView s SelectedValue을 매개 변수 원본으로 지정 합니다.](adding-a-gridview-column-of-radio-buttons-cs/_static/image19.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image33.png)

**그림 19**: controlparameter를 사용 하 여 GridView s SelectedValue을 매개 변수 소스로 지정 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-cs/_static/image34.png))

마법사가 완료 되 면 Visual Studio에서 제품 데이터 필드에 대 한 필드를 자동으로 추가 합니다. `ProductName`, `CategoryName`및 `UnitPrice` BoundFields를 제외한 모든 항목을 제거 하 고 `HeaderText` 속성을 Product, Category 및 Price로 변경 합니다. `UnitPrice` BoundField를 구성 하 여 해당 값의 서식을 통화로 지정 합니다. 이러한 변경을 수행한 후 패널, GridView 및 ObjectDataSource의 선언 태그는 다음과 같습니다.

[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample11.aspx)]

이 연습을 완료 하려면 GridView s `SelectedIndex` 속성을 `SelectedSuppliersIndex`로 설정 하 고 `ProductsBySupplierPanel` 패널의 `Visible` 속성을 `true` 단추를 클릭할 때 `ListProducts`으로 설정 해야 합니다. 이 작업을 수행 하려면 `ListProducts` Button Web control s `Click` 이벤트에 대 한 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample12.cs)]

GridView에서 공급자를 선택 하지 않은 경우 `ChooseSupplierMsg` 레이블이 표시 되 고 `ProductsBySupplierPanel` 패널이 숨겨집니다. 그렇지 않고 공급자를 선택한 경우 `ProductsBySupplierPanel` 표시 되 고 GridView s `SelectedIndex` 속성이 업데이트 됩니다.

그림 20에서는 Breweries 공급자를 선택 하 고 페이지에 제품 표시 단추를 클릭 한 후의 결과를 보여 줍니다.

[![에서 제공 하는 제품이 동일한 페이지에 나열 됩니다.](adding-a-gridview-column-of-radio-buttons-cs/_static/image20.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image35.png)

**그림 20**: (Breweries 피트)에서 제공 하는 제품이 동일한 페이지에 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-cs/_static/image36.png)).

## <a name="summary"></a>요약

[세부 정보 DetailView 자습서와 함께 선택 가능한 마스터 GridView를 사용 하 여 마스터/세부](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md) 정보에서 설명한 대로 `ShowSelectButton` 속성이 `true`로 설정 된 commandfield를 사용 하 여 GridView에서 레코드를 선택할 수 있습니다. 그러나 CommandField는 일반 푸시 단추, 링크 또는 이미지로 단추를 표시 합니다. 대체 행 선택 사용자 인터페이스는 각 GridView 행에 라디오 단추나 확인란을 제공 하는 것입니다. 이 자습서에서는 라디오 단추 열을 추가 하는 방법을 살펴보았습니다.

불행 하 게도 라디오 단추 열을 추가 하는 것은 무엇 보다 간단 하거나 간단 하지 않을 수 있습니다. 단추를 클릭 하 여 추가할 수 있는 기본 제공 RadioButtonField 없으며, Templatefield로 변환 내에 RadioButton 웹 컨트롤을 사용 하면 고유한 문제 집합이 도입 됩니다. 결과적으로 이러한 인터페이스를 제공 하기 위해 사용자 지정 `DataControlField` 클래스를 만들어야 하거나 `RowCreated` 이벤트 중에 적절 한 HTML을 Templatefield로 변환에 삽입 해야 합니다.

라디오 단추 열을 추가 하는 방법을 살펴본 후에는 확인란 열을 추가 하는 것에 주목 하세요. 사용자는 확인란의 열을 사용 하 여 하나 이상의 GridView 행을 선택 하 고 선택한 모든 행 (예: 웹 기반 전자 메일 클라이언트에서 전자 메일 집합 선택)에 대해 일부 작업을 수행한 다음 선택한 모든 메일을 삭제 하도록 선택할 수 있습니다. 다음 자습서에서는 이러한 열을 추가 하는 방법을 알아봅니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 David Suru입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [다음](adding-a-gridview-column-of-checkboxes-cs.md)
