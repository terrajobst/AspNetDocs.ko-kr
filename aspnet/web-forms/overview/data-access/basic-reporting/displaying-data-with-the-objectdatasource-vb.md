---
uid: web-forms/overview/data-access/basic-reporting/displaying-data-with-the-objectdatasource-vb
title: ObjectDataSource를 사용 하 여 데이터 표시 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는이 컨트롤을 사용 하 여 ObjectDataSource 컨트롤을 확인 합니다 .이 컨트롤을 사용 하 여 이전 자습서에서 만든 BLL에서 검색 된 데이터를 havi에서 바인딩할 수 있습니다.
ms.author: riande
ms.date: 03/31/2010
ms.assetid: d62c3a63-0940-4019-874e-4a4047df0c1c
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/displaying-data-with-the-objectdatasource-vb
msc.type: authoredcontent
ms.openlocfilehash: 754188352cbfb08e610027f5b7890a32bd88ae26
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78483053"
---
# <a name="displaying-data-with-the-objectdatasource-vb"></a>ObjectDataSource를 사용하여 데이터 표시(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_4_VB.exe) 또는 [PDF 다운로드](displaying-data-with-the-objectdatasource-vb/_static/datatutorial04vb1.pdf)

> 이 자습서에서는이 컨트롤을 사용 하 여 ObjectDataSource 컨트롤에서 코드 줄을 작성할 필요 없이 이전 자습서에서 만든 BLL에서 가져온 데이터를 바인딩할 수 있습니다.

## <a name="introduction"></a>소개

응용 프로그램 아키텍처 및 웹 사이트 페이지 레이아웃이 완료 되 면 다양 한 공통 데이터 및 보고 관련 작업을 수행 하는 방법에 대 한 탐색을 시작할 준비가 되었습니다. 이전 자습서에서는 ASP.NET 페이지에서 DAL 및 BLL의 데이터를 데이터 웹 컨트롤에 프로그래밍 방식으로 바인딩하는 방법에 대해 살펴보았습니다. 이 구문은 데이터 웹 컨트롤의 `DataSource` 속성을 표시 하 고 컨트롤의 `DataBind()` 메서드를 호출 하는 것이 ASP.NET 1.x 응용 프로그램에서 사용 되는 패턴이 며 2.0 응용 프로그램에서 계속 사용할 수 있습니다. 그러나 ASP.NET 2.0의 새 데이터 소스 컨트롤은 데이터를 사용 하는 선언적 방법을 제공 합니다. 이러한 컨트롤을 사용 하면 코드 줄을 작성할 필요 없이 이전 자습서에서 만든 BLL에서 가져온 데이터를 바인딩할 수 있습니다.

ASP.NET 2.0에는 [사용자 지정 데이터 소스 컨트롤](https://msdn.microsoft.com/library/default.asp?url=/library/dnvs05/html/DataSourceCon1.asp)(필요한 경우)을 빌드할 수 있지만 [SqlDataSource](https://msdn.microsoft.com/library/dz12d98w%28vs.80%29.aspx), [AccessDataSource](https://msdn.microsoft.com/library/8e5545e1.aspx), [ObjectDataSource](https://msdn.microsoft.com/library/9a4kyhcx.aspx), [XmlDataSource](https://msdn.microsoft.com/library/e8d8587a%28en-US,VS.80%29.aspx)및 [SiteMapDataSource](https://msdn.microsoft.com/library/5ex9t96x%28en-US,VS.80%29.aspx) 의 5 가지 기본 제공 데이터 소스 컨트롤이 포함 되어 있습니다. 자습서 응용 프로그램에 대 한 아키텍처를 개발 했으므로 BLL 클래스에 대해 ObjectDataSource를 사용 하 게 됩니다.

![ASP.NET 2.0에는 5 가지 기본 제공 데이터 원본 컨트롤이 포함 되어 있습니다.](displaying-data-with-the-objectdatasource-vb/_static/image1.png)

**그림 1**: ASP.NET 2.0에는 5 가지 기본 제공 데이터 원본 컨트롤이 포함 되어 있습니다.

ObjectDataSource는 다른 개체에서 작업 하기 위한 프록시로 사용 됩니다. ObjectDataSource를 구성 하려면이 기본 개체와 해당 메서드가 ObjectDataSource의 `Select`, `Insert`, `Update`및 `Delete` 메서드에 매핑되는 방식을 지정 합니다. 이 기본 개체를 지정 하 고 해당 메서드를 ObjectDataSource에 매핑한 후에는 ObjectDataSource를 데이터 웹 컨트롤에 바인딩할 수 있습니다. ASP.NET에는 GridView, DetailsView, RadioButtonList 및 DropDownList을 비롯 한 많은 데이터 웹 컨트롤이 포함 되어 있습니다. 페이지 수명 주기 동안 데이터 웹 컨트롤이 바인딩되는 데이터에 액세스 해야 할 수 있습니다 .이 작업은 ObjectDataSource의 `Select` 메서드를 호출 하 여 수행 합니다. 데이터 웹 컨트롤이 삽입, 업데이트 또는 삭제를 지 원하는 경우 ObjectDataSource의 `Insert`, `Update`또는 `Delete` 메서드에 대 한 호출이 수행 될 수 있습니다. 그런 다음 아래 다이어그램에 나와 있는 것 처럼 이러한 호출은 ObjectDataSource를 사용 하 여 해당 하는 기본 개체의 메서드에 라우팅됩니다.

[ObjectDataSource가 프록시로 사용 되는 ![](displaying-data-with-the-objectdatasource-vb/_static/image3.png)](displaying-data-with-the-objectdatasource-vb/_static/image2.png)

**그림 2**: ObjectDataSource를 프록시로 사용 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-vb/_static/image4.png))

ObjectDataSource를 사용 하 여 데이터를 삽입, 업데이트 또는 삭제 하는 메서드를 호출할 수 있지만, 데이터를 반환 하는 경우에만 중점적으로 살펴보겠습니다. 이후 자습서에서는 데이터를 수정 하는 ObjectDataSource 및 데이터 웹 컨트롤을 사용 하는 방법을 살펴봅니다.

## <a name="step-1-adding-and-configuring-the-objectdatasource-control"></a>1 단계: ObjectDataSource 컨트롤 추가 및 구성

먼저 `BasicReporting` 폴더에서 `SimpleDisplay.aspx` 페이지를 열고 디자인 뷰로 전환한 다음 ObjectDataSource 컨트롤을 도구 상자에서 페이지의 디자인 화면으로 끌어 옵니다. ObjectDataSource는 태그를 생성 하지 않으므로 디자인 화면에 회색 상자로 표시 됩니다. 지정 된 개체에서 메서드를 호출 하 여 데이터에 액세스 하기만 하면 됩니다. ObjectDataSource에서 반환 된 데이터는 GridView, DetailsView, FormView 등의 데이터 웹 컨트롤에 의해 표시 될 수 있습니다.

> [!NOTE]
> 또는 먼저 데이터 웹 컨트롤을 페이지에 추가한 다음 해당 스마트 태그를 통해 드롭다운 목록에서 새 데이터 원본 &lt;&gt; 옵션을 선택할 수 있습니다.

ObjectDataSource의 기본 개체를 지정 하 고 해당 개체의 메서드가 ObjectDataSource에 매핑되는 방법을 지정 하려면 ObjectDataSource의 스마트 태그에서 데이터 소스 구성 링크를 클릭 합니다.

[![스마트 태그에서 데이터 소스 구성 링크를 클릭 합니다.](displaying-data-with-the-objectdatasource-vb/_static/image6.png)](displaying-data-with-the-objectdatasource-vb/_static/image5.png)

**그림 3**: 스마트 태그에서 데이터 소스 구성 링크 클릭 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-vb/_static/image7.png))

그러면 데이터 원본 구성 마법사가 열립니다. 먼저 ObjectDataSource가 작동 하는 개체를 지정 해야 합니다. "데이터 구성 요소만 표시" 확인란이 선택 되어 있으면이 화면의 드롭다운 목록에 `DataObject` 특성으로 데코레이팅된 개체만 나열 됩니다. 현재 목록에는 형식화 된 데이터 집합의 Tableadapter와 이전 자습서에서 만든 BLL 클래스가 포함 됩니다. 비즈니스 논리 계층 클래스에 `DataObject` 특성을 추가 하지 않은 경우이 목록에 표시 되지 않습니다. 이 경우에는 "데이터 구성 요소만 표시" 확인란의 선택을 취소 하 여 모든 개체를 볼 수 있습니다. 여기에는 BLL 클래스 (형식화 된 데이터 집합의 다른 클래스와 함께 Datatable, Datarow 등)가 포함 됩니다.

이 첫 번째 화면에서 드롭다운 목록에서 `ProductsBLL` 클래스를 선택 하 고 다음을 클릭 합니다.

[ObjectDataSource 컨트롤과 함께 사용할 개체를 지정 ![](displaying-data-with-the-objectdatasource-vb/_static/image9.png)](displaying-data-with-the-objectdatasource-vb/_static/image8.png)

**그림 4**: ObjectDataSource 컨트롤과 함께 사용할 개체 지정 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-vb/_static/image10.png))

마법사의 다음 화면에 ObjectDataSource에서 호출할 메서드를 선택 하 라는 메시지가 표시 됩니다. 드롭다운 목록에는 이전 화면에서 선택한 개체의 데이터를 반환 하는 메서드가 나열 되어 있습니다. 여기에 `GetProductByProductID`, `GetProducts`, `GetProductsByCategoryID`및 `GetProductsBySupplierID`표시 됩니다. 드롭다운 목록에서 `GetProducts` 메서드를 선택 하 고 마침을 클릭 합니다 (이전 자습서에 표시 된 것 처럼 `ProductBLL`의 메서드에 `DataObjectMethodAttribute`를 추가한 경우이 옵션은 기본적으로 선택 됨).

[![선택 탭에서 데이터를 반환 하는 방법을 선택 합니다.](displaying-data-with-the-objectdatasource-vb/_static/image12.png)](displaying-data-with-the-objectdatasource-vb/_static/image11.png)

**그림 5**: 선택 탭에서 데이터를 반환 하는 방법 선택 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-vb/_static/image13.png))

## <a name="configure-the-objectdatasource-manually"></a>수동으로 ObjectDataSource 구성

ObjectDataSource의 데이터 원본 구성 마법사는 사용 하는 개체를 신속 하 게 지정 하 고 호출 되는 개체의 메서드를 연결 하는 빠른 방법을 제공 합니다. 그러나 속성 창 또는 선언적 태그에서 직접 속성을 통해 ObjectDataSource를 구성할 수 있습니다. `TypeName` 속성을 사용할 기본 개체의 형식으로 설정 하 고, 데이터를 검색할 때 호출할 메서드에 대 한 `SelectMethod`만 설정 합니다.

[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample1.aspx)]

데이터 원본 구성 마법사를 선호 하는 경우에도 마법사에서 개발자가 만든 클래스만 나열 하므로 ObjectDataSource를 수동으로 구성 해야 하는 경우가 있을 수 있습니다. 사용자 계정 정보에 액세스 하거나 파일 시스템 정보를 사용 하기 위해 [디렉터리 클래스](https://msdn.microsoft.com/library/system.io.directory.aspx) 와 같은 .NET Framework [의 클래스에](https://msdn.microsoft.com/library/system.web.security.membership.aspx)ObjectDataSource를 바인딩하려면 해당 objectdatasource의 속성을 수동으로 설정 해야 합니다.

## <a name="step-2-adding-a-data-web-control-and-binding-it-to-the-objectdatasource"></a>2 단계: 데이터 웹 컨트롤을 추가 하 고 ObjectDataSource에 바인딩

ObjectDataSource가 페이지에 추가 되 고 구성 되 면 페이지에 데이터 웹 컨트롤을 추가 하 여 ObjectDataSource의 `Select` 메서드에서 반환 되는 데이터를 표시할 준비가 된 것입니다. 모든 데이터 웹 컨트롤을 ObjectDataSource에 바인딩할 수 있습니다. GridView, DetailsView 및 FormView에 ObjectDataSource의 데이터를 표시 하는 방법을 살펴보겠습니다.

## <a name="binding-a-gridview-to-the-objectdatasource"></a>ObjectDataSource에 GridView 바인딩

도구 상자의 GridView 컨트롤을 `SimpleDisplay.aspx`의 디자인 화면에 추가 합니다. GridView의 스마트 태그에서 1 단계에서 추가한 ObjectDataSource 컨트롤을 선택 합니다. 그러면 ObjectDataSource의 `Select` 메서드에서 데이터에 의해 반환 되는 각 속성 (즉, Products DataTable에서 정의한 속성)에 대해 GridView에 BoundField이 자동으로 생성 됩니다.

[GridView가 페이지에 추가 되 고 ObjectDataSource에 바인딩 ![](displaying-data-with-the-objectdatasource-vb/_static/image15.png)](displaying-data-with-the-objectdatasource-vb/_static/image14.png)

**그림 6**: GridView가 페이지에 추가 되 고 ObjectDataSource에 바인딩 되었습니다 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-vb/_static/image16.png)).

그런 다음 스마트 태그에서 열 편집 옵션을 클릭 하 여 GridView의 BoundFields을 사용자 지정 하거나 다시 정렬 하거나 제거할 수 있습니다.

[열 편집 대화 상자를 통해 GridView의 BoundFields 관리 ![](displaying-data-with-the-objectdatasource-vb/_static/image18.png)](displaying-data-with-the-objectdatasource-vb/_static/image17.png)

**그림 7**: 열 편집 대화 상자를 통해 GridView의 BoundFields 관리 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-vb/_static/image19.png))

잠시 후에 `ProductID`, `SupplierID`, `CategoryID`, `QuantityPerUnit`, `UnitsInStock`, `UnitsOnOrder`및 `ReorderLevel` BoundFields를 제거 하 여 GridView의 BoundFields을 수정 합니다. 왼쪽 아래에 있는 목록에서 BoundField를 선택 하 고 삭제 단추 (빨간색 X)를 클릭 하 여 제거 하면 됩니다. 다음으로, 이러한 BoundFields를 선택 하 고 위쪽 화살표를 클릭 하 여 `CategoryName` 및 `SupplierName` BoundFields 앞에 `UnitPrice` BoundField 앞에 오도록 BoundFields을 다시 정렬 합니다. 나머지 BoundFields의 `HeaderText` 속성을 각각 `Products`, `Category`, `Supplier`및 `Price`로 설정 합니다. 그런 다음 BoundField의 `HtmlEncode` 속성을 False로 설정 하 고 해당 `DataFormatString` 속성을 `{0:c}`로 설정 하 여 `Price` BoundField를 통화로 서식 지정 합니다. 마지막으로 `ItemStyle`/`HorizontalAlign` 속성을 통해 `Price`을 오른쪽에 가로로 맞추고 `Discontinued` 확인란을 가운데에 맞춥니다.

[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample2.aspx)]

[GridView의 BoundFields 사용자 지정 ![](displaying-data-with-the-objectdatasource-vb/_static/image21.png)](displaying-data-with-the-objectdatasource-vb/_static/image20.png)

**그림 8**: GridView의 BoundFields 사용자 지정 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-vb/_static/image22.png))

## <a name="using-themes-for-a-consistent-look"></a>일관 된 모양으로 테마 사용

이러한 자습서에서는 가능한 경우 외부 파일에 정의 된 css 스타일 시트를 사용 하는 대신 모든 컨트롤 수준 스타일 설정을 제거 합니다. `Styles.css` 파일에는 이러한 자습서에서 사용 되는 데이터 웹 컨트롤의 모양을 지정 하는 데 사용 해야 하는 `DataWebControlStyle`, `HeaderStyle`, `RowStyle`및 `AlternatingRowStyle` CSS 클래스가 포함 되어 있습니다. 이를 위해 GridView의 `CssClass` 속성을 `DataWebControlStyle`로 설정 하 고 해당 `HeaderStyle`, `RowStyle`및 `AlternatingRowStyle` 속성의 `CssClass` 속성을 적절 하 게 설정할 수 있습니다.

웹 컨트롤에서 이러한 `CssClass` 속성을 설정 하는 경우 자습서에 추가 된 모든 데이터 웹 컨트롤에 대해 이러한 속성 값을 명시적으로 설정 하는 것을 명심 해야 합니다. 보다 쉽게 관리할 수 있는 방법은 테마를 사용 하 여 GridView, DetailsView 및 FormView 컨트롤에 대 한 기본 CSS 관련 속성을 정의 하는 것입니다. 테마는 일반적인 모양과 느낌을 적용 하기 위해 사이트에서 페이지에 적용할 수 있는 컨트롤 수준 속성 설정, 이미지 및 CSS 클래스의 컬렉션입니다.

테마에는 이미지 또는 CSS 파일이 포함 되지 않습니다. 웹 응용 프로그램의 루트 폴더에 정의 된 스타일 `Styles.css` 시트는 그대로 유지 되지만 두 개의 스킨이 포함 됩니다. 스킨은 웹 컨트롤에 대 한 기본 속성을 정의 하는 파일입니다. 구체적으로 말하면 GridView 및 DetailsView 컨트롤에 대 한 스킨 파일이 기본 `CssClass`관련 속성을 나타내는 것입니다.

먼저 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 새 항목 추가를 선택 하 여 `GridView.skin` 라는 프로젝트에 새 스킨 파일을 추가 합니다.

[GridView. skin 이라는 스킨 파일을 추가 ![](displaying-data-with-the-objectdatasource-vb/_static/image24.png)](displaying-data-with-the-objectdatasource-vb/_static/image23.png)

**그림 9**: 이름이 `GridView.skin` 스킨 파일 추가 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-vb/_static/image25.png))

스킨 파일은 `App_Themes` 폴더에 있는 테마에 배치 해야 합니다. 이러한 폴더가 아직 없기 때문에 Visual Studio에서 첫 번째 스킨을 추가 하는 경우 microsoft에서 제안 하는 항목을 작성 합니다. 예를 클릭 하 `App_Theme` 폴더를 만들고 여기에 새 `GridView.skin` 파일을 저장 합니다.

[![Visual Studio에서 App_Theme 폴더를 만들 수 있습니다.](displaying-data-with-the-objectdatasource-vb/_static/image27.png)](displaying-data-with-the-objectdatasource-vb/_static/image26.png)

**그림 10**: Visual Studio에서 `App_Theme` 폴더를 만들도록 허용 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-vb/_static/image28.png))

그러면 `GridView.skin`스킨 파일이 있는 GridView 라는 `App_Themes` 폴더에 새 테마가 생성 됩니다.

![GridView 테마가 App_Theme 폴더에 추가 되었습니다.](displaying-data-with-the-objectdatasource-vb/_static/image29.png)

**그림 11**: GridView 테마가 `App_Theme` 폴더에 추가 되었습니다.

GridView 테마의 이름을 DataWebControls로 바꿉니다 (`App_Theme` 폴더에서 GridView 폴더를 마우스 오른쪽 단추로 클릭 하 고 이름 바꾸기를 선택). 다음으로 `GridView.skin` 파일에 다음 태그를 입력 합니다.

[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample3.aspx)]

DataWebControls 테마를 사용 하는 페이지에서 모든 GridView의 `CssClass`관련 속성에 대 한 기본 속성을 정의 합니다. 곧 사용할 데이터 웹 컨트롤인 DetailsView에 대해 다른 스킨을 추가 해 보겠습니다. `DetailsView.skin` 라는 DataWebControls 테마에 새 스킨을 추가 하 고 다음 태그를 추가 합니다.

[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample4.aspx)]

테마를 정의한 후 마지막 단계는 ASP.NET 페이지에 테마를 적용 하는 것입니다. 테마는 페이지 별로 또는 웹 사이트의 모든 페이지에 적용할 수 있습니다. 웹 사이트의 모든 페이지에이 테마를 사용 하겠습니다. 이 작업을 수행 하려면 `Web.config`의 `<system.web>` 섹션에 다음 태그를 추가 합니다.

[!code-xml[Main](displaying-data-with-the-objectdatasource-vb/samples/sample5.xml)]

이제 모든 작업을 마쳤습니다. `styleSheetTheme` 설정은 테마에 지정 된 속성이 컨트롤 수준에서 지정 된 속성을 재정의 *하지* 않아야 함을 나타냅니다. 테마 설정에서 제어 설정을 거부가 지정 하려면 `styleSheetTheme`대신 `theme` 특성을 사용 합니다. 그러나 테마 설정은 Visual Studio 디자인 뷰에 표시 되지 않습니다. 테마 및 스킨에 대 한 자세한 내용은 테마를 사용 하 여 [ASP.NET 테마 및 스킨 개요](https://msdn.microsoft.com/library/ykzx33wh.aspx) 및 [서버 쪽 스타일](https://quickstarts.asp.net/quickstartv20/aspnet/doc/themes/stylesheettheme.aspx) 을 참조 하세요. 테마를 사용 하도록 페이지를 구성 하는 방법에 대 한 자세한 내용은 [방법: ASP.NET 테마 적용](https://msdn.microsoft.com/library/0yy5hxdk%28VS.80%29.aspx) 을 참조 하세요.

[GridView ![제품의 이름, 범주, 공급자, 가격 및 단종 된 정보를 표시 합니다.](displaying-data-with-the-objectdatasource-vb/_static/image31.png)](displaying-data-with-the-objectdatasource-vb/_static/image30.png)

**그림 12**: GridView는 제품의 이름, 범주, 공급자, 가격 및 단종 되지 않은 정보를 표시 합니다 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-vb/_static/image32.png)).

## <a name="displaying-one-record-at-a-time-in-the-detailsview"></a>DetailsView에서 한 번에 하나의 레코드 표시

GridView는 바인딩된 데이터 소스 컨트롤에서 반환 하는 각 레코드에 대해 하나의 행을 표시 합니다. 그러나 한 번에 하나의 레코드 또는 한 레코드씩 표시 하려는 경우가 있습니다. [DetailsView 컨트롤](https://msdn.microsoft.com/library/s3w1w7t4.aspx) 은이 기능을 제공 하 고, 두 개의 열이 있는 HTML `<table>` 렌더링 하 고, 컨트롤에 바인딩된 각 열 이나 속성에 대해 행을 하나씩 렌더링 합니다. DetailsView를 90도 회전 한 단일 레코드를 사용 하는 GridView로 간주할 수 있습니다.

`SimpleDisplay.aspx`에서 GridView *위에* DetailsView 컨트롤을 추가 하 여 시작 합니다. 다음으로 GridView와 동일한 ObjectDataSource 컨트롤에 바인딩합니다. GridView와 마찬가지로 BoundField은 ObjectDataSource의 `Select` 메서드에서 반환 하는 개체의 각 속성에 대해 DetailsView에 추가 됩니다. 유일한 차이점은 DetailsView의 BoundFields가 세로로 배치 되는 것이 아니라 가로로 배치 된다는 것입니다.

[페이지에 DetailsView을 추가 ![ObjectDataSource에 바인딩](displaying-data-with-the-objectdatasource-vb/_static/image34.png)](displaying-data-with-the-objectdatasource-vb/_static/image33.png)

**그림 13**: 페이지에 DetailsView을 추가 하 고 ObjectDataSource에 바인딩 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-vb/_static/image35.png))

GridView와 마찬가지로 DetailsView의 BoundFields을 조정 된 하 여 ObjectDataSource에서 반환 된 데이터의 더 많은 사용자 지정 표시를 제공할 수 있습니다. 그림 14에서는 BoundFields 및 `CssClass` 속성이 GridView 예제와 비슷하게 보이도록 구성 된 후의 DetailsView을 보여 줍니다.

[DetailsView에서 단일 레코드를 표시 ![](displaying-data-with-the-objectdatasource-vb/_static/image37.png)](displaying-data-with-the-objectdatasource-vb/_static/image36.png)

**그림 14**: DetailsView에서 단일 레코드 표시 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-vb/_static/image38.png))

DetailsView에는 해당 데이터 원본에서 반환 된 첫 번째 레코드만 표시 됩니다. 사용자가 한 번에 하나씩 모든 레코드를 단계별로 실행할 수 있도록 하려면 DetailsView에 대해 페이징을 사용 하도록 설정 해야 합니다. 이렇게 하려면 Visual Studio로 돌아가서 DetailsView의 스마트 태그에서 페이징 사용 확인란을 선택 합니다.

[DetailsView 컨트롤에서 페이징을 사용 하도록 설정 ![](displaying-data-with-the-objectdatasource-vb/_static/image40.png)](displaying-data-with-the-objectdatasource-vb/_static/image39.png)

**그림 15**: DetailsView 컨트롤에서 페이징 사용 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-vb/_static/image41.png))

[페이징이 활성화 된 ![DetailsView를 사용 하면 사용자가 모든 제품을 볼 수 있습니다.](displaying-data-with-the-objectdatasource-vb/_static/image43.png)](displaying-data-with-the-objectdatasource-vb/_static/image42.png)

**그림 16**: 페이징을 사용 하는 경우 DetailsView을 사용 하면 사용자가 모든 제품을 볼 수 있습니다 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-vb/_static/image44.png)).

이후 자습서에서 페이징에 대해 자세히 설명 합니다.

## <a name="a-more-flexible-layout-for-showing-one-record-at-a-time"></a>한 번에 하나의 레코드를 표시 하기 위한 보다 유연한 레이아웃

DetailsView은 ObjectDataSource에서 반환 된 각 레코드를 표시 하는 방법에 매우 고정 되어 있습니다. 데이터를 보다 유연 하 게 볼 수 있습니다. 예를 들어 제품의 이름, 범주, 공급자, 가격 및 중단 되지 않은 정보를 각각 별도의 행에 표시 하는 대신, 이름 및 공급 업체 정보가 더 작은 글꼴 크기로 이름 및 가격 아래에 표시 되는 `<h4>` 제목에 제품 이름 및 가격을 표시 하는 것이 좋습니다. 값 옆에 속성 이름 (제품, 범주 등)을 표시 하는 것을 고려 하지 않을 수 있습니다.

[FormView 컨트롤](https://msdn.microsoft.com/library/fyf1dk77.aspx) 은 이러한 수준의 사용자 지정을 제공 합니다. GridView는 필드 (예: GridView 및 DetailsView do)를 사용 하는 대신, 웹 컨트롤, 정적 HTML 및 [데이터 바인딩 구문을](http://www.15seconds.com/issue/040630.htm)혼합 하 여 사용할 수 있는 템플릿을 사용 합니다. ASP.NET 1.x의 Repeater 컨트롤에 익숙한 경우 FormView를 단일 레코드를 표시 하는 리피터로 간주할 수 있습니다.

`SimpleDisplay.aspx` 페이지의 디자인 화면에 FormView 컨트롤을 추가 합니다. 처음에는 FormView를 회색 블록으로 표시 하 여 최소한의 컨트롤 `ItemTemplate`를 제공 해야 한다고 알립니다.

[FormView에 ItemTemplate을 포함 해야 ![](displaying-data-with-the-objectdatasource-vb/_static/image46.png)](displaying-data-with-the-objectdatasource-vb/_static/image45.png)

**그림 17**: FormView는 `ItemTemplate`을 포함 해야 합니다 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-vb/_static/image47.png)).

Formview의 스마트 태그를 사용 하 여 FormView를 데이터 소스 컨트롤에 직접 바인딩할 수 있습니다. 그러면 `EditItemTemplate` 및 `InsertItemTemplate`와 함께 ObjectDataSource 컨트롤의 `InsertMethod` 및 `UpdateMethod` 속성이 설정 된 경우 자동으로 기본 `ItemTemplate` 만들어집니다. 그러나이 예제에서는 데이터를 FormView에 바인딩하고 해당 `ItemTemplate`를 수동으로 지정 합니다. 먼저 FormView의 `DataSourceID` 속성을 `ObjectDataSource1`ObjectDataSource 컨트롤의 `ID`로 설정 합니다. 다음으로 `ItemTemplate`를 만들어 `<h4>` 요소에 제품 이름과 가격을 표시 하 고 그 아래에 더 작은 글꼴 크기의 범주 및 운송 업체 이름을 표시 합니다.

[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample6.aspx)]

[첫 번째 제품 ![(Chai) 사용자 지정 형식으로 표시 됩니다.](displaying-data-with-the-objectdatasource-vb/_static/image49.png)](displaying-data-with-the-objectdatasource-vb/_static/image48.png)

**그림 18**: 첫 번째 제품 (Chai)이 사용자 지정 형식으로 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-vb/_static/image50.png)).

`<%# Eval(propertyName) %>`는 데이터 바인딩 구문입니다. `Eval` 메서드는 FormView 컨트롤에 바인딩되는 현재 개체에 대해 지정 된 속성의 값을 반환 합니다. 데이터 바인딩의 기능 및 제한에 대 한 자세한 내용은 [ASP.NET 2.0의 간소화 및 확장 된 데이터 바인딩 구문](http://www.15seconds.com/issue/040630.htm) Alex Homer의 문서를 참조 하세요.

DetailsView 처럼 FormView는 ObjectDataSource에서 반환 된 첫 번째 레코드만 표시 합니다. FormView에서 페이징을 사용 하도록 설정 하 여 방문자가 한 번에 하나씩 제품을 단계별로 실행할 수 있습니다.

## <a name="summary"></a>요약

ASP.NET 2.0의 ObjectDataSource 컨트롤을 통해 코드 줄을 작성 하지 않고도 비즈니스 논리 계층에서 데이터 액세스 및 표시를 수행할 수 있습니다. ObjectDataSource는 클래스의 지정 된 메서드를 호출 하 고 결과를 반환 합니다. 이러한 결과는 ObjectDataSource에 바인딩된 데이터 웹 컨트롤에 표시 될 수 있습니다. 이 자습서에서는 GridView, DetailsView 및 FormView 컨트롤을 ObjectDataSource에 바인딩하는 방법에 대해 살펴보았습니다.

지금까지 ObjectDataSource를 사용 하 여 매개 변수가 없는 메서드를 호출 하는 방법만 살펴보았습니다. 그러나 `ProductBLL` 클래스의 `GetProductsByCategoryID(categoryID)`와 같이 입력 매개 변수가 필요한 메서드를 호출 하려면 어떻게 해야 하나요? 하나 이상의 매개 변수가 필요한 메서드를 호출 하려면 이러한 매개 변수의 값을 지정 하도록 ObjectDataSource를 구성 해야 합니다. [다음 자습서](declarative-parameters-vb.md)에서이를 수행 하는 방법을 살펴보겠습니다.

행복 한 프로그래밍

## <a name="further-reading"></a>추가 참고 자료

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [고유한 데이터 소스 컨트롤 만들기](https://msdn.microsoft.com/library/ms364049.aspx)
- [ASP.NET 2.0에 대 한 GridView 예제](https://msdn.microsoft.com/library/aa479339.aspx)
- [ASP.NET 2.0의 단순화 및 확장 된 데이터 바인딩 구문](http://www.15seconds.com/issue/040630.htm)
- [ASP.NET 2.0의 테마](http://www.odetocode.com/Articles/423.aspx)
- [테마를 사용 하는 서버 쪽 스타일](https://quickstarts.asp.net/quickstartv20/aspnet/doc/themes/stylesheettheme.aspx)
- [방법: 프로그래밍 방식으로 ASP.NET 테마 적용](https://msdn.microsoft.com/library/tx35bd89.aspx)

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Hilton Gid Esenow 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)
> [다음](declarative-parameters-vb.md)
