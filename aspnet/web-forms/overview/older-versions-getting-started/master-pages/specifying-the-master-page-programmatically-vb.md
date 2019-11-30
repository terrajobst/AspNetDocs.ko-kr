---
uid: web-forms/overview/older-versions-getting-started/master-pages/specifying-the-master-page-programmatically-vb
title: 프로그래밍 방식으로 마스터 페이지 지정 (VB) | Microsoft Docs
author: rick-anderson
description: PreInit 이벤트 처리기를 통해 프로그래밍 방식으로 콘텐츠 페이지의 마스터 페이지를 설정 하는 방법을 살펴봅니다.
ms.author: riande
ms.date: 07/28/2008
ms.assetid: 0edcd653-f24a-41aa-aef4-75f868fe5ac2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/specifying-the-master-page-programmatically-vb
msc.type: authoredcontent
ms.openlocfilehash: 3b039b22bef38ae6ebf80be070820dc1638f87f4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74618607"
---
# <a name="specifying-the-master-page-programmatically-vb"></a>마스터 페이지를 프로그래밍 방식으로 지정(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_09_VB.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_09_VB.pdf)

> PreInit 이벤트 처리기를 통해 프로그래밍 방식으로 콘텐츠 페이지의 마스터 페이지를 설정 하는 방법을 살펴봅니다.

## <a name="introduction"></a>소개

개최 예제에서는 [*마스터 페이지를 사용 하 여 사이트 전체 레이아웃을 만들기*](creating-a-site-wide-layout-using-master-pages-vb.md)때문에 모든 콘텐츠 페이지에서 `@Page` 지시문의 `MasterPageFile` 특성을 통해 해당 마스터 페이지를 선언적으로 참조 했습니다. 예를 들어 다음 `@Page` 지시문은 콘텐츠 페이지를 마스터 페이지 `Site.master`에 연결 합니다.

[!code-aspx[Main](specifying-the-master-page-programmatically-vb/samples/sample1.aspx)]

`System.Web.UI` 네임 스페이스의 [`Page` 클래스](https://msdn.microsoft.com/library/system.web.ui.page.aspx) 에는 콘텐츠 페이지의 마스터 페이지에 대 한 경로를 반환 하는 [`MasterPageFile` 속성이](https://msdn.microsoft.com/library/system.web.ui.page.masterpagefile.aspx) 포함 되어 있습니다. 이 속성은 `@Page` 지시문에 의해 설정 됩니다. 이 속성은 콘텐츠 페이지의 마스터 페이지를 프로그래밍 방식으로 지정 하는 데에도 사용할 수 있습니다. 이 방법은 페이지를 방문 하는 사용자와 같은 외부 요소를 기준으로 마스터 페이지를 동적으로 할당 하려는 경우에 유용 합니다.

이 자습서에서는 웹 사이트에 두 번째 마스터 페이지를 추가 하 고 런타임에 사용할 마스터 페이지를 동적으로 결정 합니다.

## <a name="step-1-a-look-at-the-page-lifecycle"></a>1 단계: 페이지 수명 주기 살펴보기

콘텐츠 페이지 ASP.NET 페이지에 대 한 요청이 웹 서버에 도착할 때마다 ASP.NET 엔진은 페이지의 콘텐츠 컨트롤을 마스터 페이지의 해당 ContentPlaceHolder 컨트롤에 퓨즈 해야 합니다. 이 fusion은 일반적인 페이지 수명 주기를 진행할 수 있는 단일 컨트롤 계층 구조를 만듭니다.

그림 1에서는이 fusion을 보여 줍니다. 그림 1의 1 단계에서는 초기 콘텐츠 및 마스터 페이지 컨트롤 계층 구조를 보여 줍니다. PreInit 스테이지의 비상 끝에서 페이지의 콘텐츠 컨트롤은 마스터 페이지의 해당 ContentPlaceHolders 표시자에 추가 됩니다 (2 단계). 이 퓨전 후에 마스터 페이지는 퓨즈 컨트롤 계층 구조의 루트로 사용 됩니다. 그런 다음이 퓨즈 컨트롤 계층 구조를 페이지에 추가 하 여 완성 된 컨트롤 계층 구조를 생성 합니다 (3 단계). 결과적으로 페이지의 컨트롤 계층 구조에는 퓨즈 컨트롤 계층 구조가 포함 됩니다.

[PreInit 단계에서 마스터 페이지 및 콘텐츠 페이지의 컨트롤 계층 구조를 함께 사용할 ![](specifying-the-master-page-programmatically-vb/_static/image2.png)](specifying-the-master-page-programmatically-vb/_static/image1.png)

**그림 01**: 마스터 페이지 및 콘텐츠 페이지의 컨트롤 계층 구조가 PreInit 단계 중에 함께 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](specifying-the-master-page-programmatically-vb/_static/image3.png)).

## <a name="step-2-setting-themasterpagefileproperty-from-code"></a>2 단계: 코드에서`MasterPageFile`속성 설정

이 fusion에서 사용 하는 마스터 페이지는 `Page` 개체의 `MasterPageFile` 속성 값에 따라 다릅니다. `@Page` 지시문에 `MasterPageFile` 특성을 설정 하면 페이지 수명 주기의 첫 단계인 초기화 단계에서 `Page`의 `MasterPageFile` 속성을 할당 하는 효과가 있습니다. 또는 프로그래밍 방식으로이 속성을 설정할 수 있습니다. 그러나 그림 1의 퓨전이 발생 하기 전에이 속성을 설정 해야 합니다.

PreInit 스테이지가 시작 될 때 `Page` 개체는 [`PreInit` 이벤트](https://msdn.microsoft.com/library/system.web.ui.page.preinit.aspx) 를 발생 시키고 해당 [`OnPreInit` 메서드](https://msdn.microsoft.com/library/system.web.ui.page.onpreinit.aspx)를 호출 합니다. 마스터 페이지를 프로그래밍 방식으로 설정 하려면 `PreInit` 이벤트에 대 한 이벤트 처리기를 만들거나 `OnPreInit` 메서드를 재정의할 수 있습니다. 두 가지 방법을 살펴보겠습니다.

먼저 사이트 홈페이지에 대 한 코드 지향 클래스 파일인 `Default.aspx.vb`를 엽니다. 다음 코드를 입력 하 여 페이지의 `PreInit` 이벤트에 대 한 이벤트 처리기를 추가 합니다.

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample2.vb)]

여기에서 `MasterPageFile` 속성을 설정할 수 있습니다. "~/Site.master" 값을 `MasterPageFile` 속성에 할당 하도록 코드를 업데이트 합니다.

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample3.vb)]

중단점을 설정 하 고 디버깅을 시작 하는 경우 `Default.aspx` 페이지를 방문할 때마다 또는이 페이지에 포스트백이 있을 때마다 `Page_PreInit` 이벤트 처리기가 실행 되 고 `MasterPageFile` 속성이 "~/Site.master"에 할당 됩니다.

또는 `Page` 클래스의 `OnPreInit` 메서드를 재정의 하 고 여기서 `MasterPageFile` 속성을 설정할 수 있습니다. 이 예에서는 특정 페이지에서 마스터 페이지를 설정 하지 않고 `BasePage`하는 것이 좋습니다. [*마스터 페이지 자습서에서 제목, 메타 태그 및 기타 HTML 헤더를 지정 하*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md) 여 사용자 지정 기본 페이지 클래스 (`BasePage`)를 다시 만들었습니다. 현재 `BasePage` `Page` 클래스의 `OnLoadComplete` 메서드를 재정의 합니다 .이 메서드는 사이트 맵 데이터를 기반으로 페이지의 `Title` 속성을 설정 합니다. `BasePage` 업데이트 하면 `OnPreInit` 메서드를 재정의 하 여 마스터 페이지를 프로그래밍 방식으로 지정할 수 있습니다.

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample4.vb)]

모든 콘텐츠 페이지가 `BasePage`에서 파생 되기 때문에 이제 모든 콘텐츠 페이지가 해당 마스터 페이지를 프로그래밍 방식으로 할당 합니다. 이 시점에서 `Default.aspx.vb`의 `PreInit` 이벤트 처리기는 불필요 합니다. 자유롭게 제거할 수 있습니다.

### <a name="what-about-thepagedirective"></a>`@Page`지시문은 무엇 인가요?

약간의 혼란 스 러 울 수 있는 것은 `BasePage` 클래스의 `OnPreInit` 메서드에서 프로그래밍 방식으로, 그리고 각 콘텐츠 페이지의 `@Page` 지시문에서 `MasterPageFile` 특성을 통해 콘텐츠 페이지의 `MasterPageFile` 속성을 두 위치에서 지정 하는 것입니다.

페이지 수명 주기의 첫 번째 단계는 초기화 단계입니다. 이 단계에서 `Page` 개체의 `MasterPageFile` 속성에는 `@Page` 지시문 (제공 된 경우)의 `MasterPageFile` 특성 값이 할당 됩니다. PreInit 단계는 초기화 단계를 따르고 `Page` 개체의 `MasterPageFile` 속성을 프로그래밍 방식으로 설정 하 여 `@Page` 지시문에서 할당 된 값을 덮어씁니다. `Page` 개체의 `MasterPageFile` 속성을 프로그래밍 방식으로 설정 하기 때문에 최종 사용자 환경에 영향을 주지 않고 `@Page` 지시문에서 `MasterPageFile` 특성을 제거할 수 있습니다. 이를 이해 하려면 계속 해 서 `Default.aspx`의 `@Page` 지시문에서 `MasterPageFile` 특성을 제거한 다음 브라우저를 통해 페이지를 방문 하세요. 짐작할 수 있듯이 출력은 특성이 제거 되기 전과 동일 합니다.

`MasterPageFile` 속성이 `@Page` 지시문을 통해 설정 되는지 아니면 프로그래밍 방식으로 최종 사용자 환경에 대해 중요 하지 않습니다. 그러나 `@Page` 지시문의 `MasterPageFile` 특성은 디자인 타임에 디자이너에서 WYSIWYG 뷰를 생성 하는 데 사용 됩니다. Visual Studio에서 `Default.aspx`로 돌아가서 디자이너로 이동 하면 "마스터 페이지 오류: 페이지에 마스터 페이지 참조가 필요 하지만 아무것도 지정 되지 않은 컨트롤이 있습니다." 라는 메시지가 표시 됩니다 (그림 2 참조).

즉, Visual Studio에서 다양 한 디자인 타임 환경을 이용 하려면 `MasterPageFile` 특성을 `@Page` 지시문에 남겨 두어야 합니다.

[![Visual Studio는 @Page 지시문의 MasterPageFile 특성을 사용 하 여 디자인 뷰를 렌더링 합니다.](specifying-the-master-page-programmatically-vb/_static/image5.png)](specifying-the-master-page-programmatically-vb/_static/image4.png)

**그림 02**: Visual Studio에서는 `@Page` 지시문의 `MasterPageFile` 특성을 사용 하 여 디자인 뷰를 렌더링 합니다 ([전체 크기 이미지를 보려면 클릭](specifying-the-master-page-programmatically-vb/_static/image6.png)).

## <a name="step-3-creating-an-alternative-master-page"></a>3 단계: 대체 마스터 페이지 만들기

런타임에 프로그래밍 방식으로 콘텐츠 페이지의 마스터 페이지를 설정할 수 있으므로 일부 외부 조건에 따라 특정 마스터 페이지를 동적으로 로드할 수 있습니다. 이 기능은 사용자에 따라 사이트의 레이아웃이 달라 야 하는 경우에 유용할 수 있습니다. 예를 들어 블로그 엔진 웹 응용 프로그램을 사용 하면 사용자가 블로그의 레이아웃을 선택할 수 있습니다. 여기서 각 레이아웃은 다른 마스터 페이지와 연결 됩니다. 런타임에 방문자가 사용자의 블로그를 볼 때 웹 응용 프로그램은 블로그의 레이아웃을 결정 하 고 해당 마스터 페이지를 콘텐츠 페이지에 동적으로 연결 해야 합니다.

일부 외부 조건에 따라 런타임에 마스터 페이지를 동적으로 로드 하는 방법을 살펴보겠습니다. 현재 웹 사이트에는 마스터 페이지 (`Site.master`)가 하나 뿐입니다. 런타임에 마스터 페이지를 선택 하는 방법을 설명 하는 다른 마스터 페이지가 필요 합니다. 이 단계에서는 새 마스터 페이지를 만들고 구성 하는 방법을 집중적으로 설명 합니다. 4 단계에서는 런타임에 사용할 마스터 페이지를 결정 하는 방법을 살펴봅니다.

`Alternate.master`이라는 루트 폴더에 새 마스터 페이지를 만듭니다. 또한 `AlternateStyles.css`이라는 웹 사이트에 새 스타일 시트를 추가 합니다.

[다른 마스터 페이지 및 CSS 파일을 웹 사이트에 추가 ![](specifying-the-master-page-programmatically-vb/_static/image8.png)](specifying-the-master-page-programmatically-vb/_static/image7.png)

**그림 03**: 다른 마스터 페이지 및 CSS 파일을 웹 사이트에 추가 ([전체 크기 이미지를 보려면 클릭](specifying-the-master-page-programmatically-vb/_static/image9.png))

페이지 맨 위에 제목을 표시 하 고 짙은 배경으로 표시 하도록 `Alternate.master` 마스터 페이지를 디자인 했습니다. 왼쪽 열을 분배 된 해당 콘텐츠를 `MainContent` ContentPlaceHolder 컨트롤 아래로 이동 했으므로 이제 페이지의 전체 너비를 차지 합니다. 또한 순서가 지정 되지 않은 단원 목록을 nixed `MainContent`위의 가로 목록으로 대체 했습니다. 마스터 페이지에서 사용 하는 글꼴 및 색 (및 확장, 해당 콘텐츠 페이지)도 업데이트 했습니다. 그림 4는 `Alternate.master` 마스터 페이지를 사용할 때 `Default.aspx`을 보여 줍니다.

> [!NOTE]
> ASP.NET에는 *테마*를 정의 하는 기능이 포함 되어 있습니다. 테마는 런타임에 페이지에 적용할 수 있는 이미지, CSS 파일 및 스타일 관련 웹 컨트롤 속성 설정의 컬렉션입니다. 테마는 사이트의 레이아웃이 표시 되는 이미지와 CSS 규칙에만 다른 경우에 사용할 수 있는 방법입니다. 다른 웹 컨트롤을 사용 하거나 매우 다른 레이아웃을 사용 하는 경우와 같이 레이아웃이 훨씬 더 큰 경우에는 별도의 마스터 페이지를 사용 해야 합니다. 테마에 대 한 자세한 내용은이 자습서의 끝부분에 있는 추가 읽기 섹션을 참조 하세요.

[콘텐츠 페이지 ![이제 새로운 모양과 느낌을 사용할 수 있습니다.](specifying-the-master-page-programmatically-vb/_static/image11.png)](specifying-the-master-page-programmatically-vb/_static/image10.png)

**그림 04**: 이제 콘텐츠 페이지에서 새로운 모양과 느낌을 사용할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](specifying-the-master-page-programmatically-vb/_static/image12.png)).

마스터 및 콘텐츠 페이지의 태그가 퓨즈 인 경우 `MasterPage` 클래스는 콘텐츠 페이지의 모든 콘텐츠 컨트롤이 마스터 페이지의 ContentPlaceHolder를 참조 하는지 확인 합니다. 존재 하지 않는 ContentPlaceHolder를 참조 하는 콘텐츠 컨트롤이 발견 되 면 예외가 throw 됩니다. 즉, 콘텐츠 페이지에 할당 되는 마스터 페이지의 콘텐츠 페이지에는 각 콘텐츠 컨트롤에 대 한 ContentPlaceHolder가 있어야 합니다.

`Site.master` 마스터 페이지에는 4 개의 ContentPlaceHolder 컨트롤이 포함 되어 있습니다.

- `head`
- `MainContent`
- `QuickLoginUI`
- `LeftColumnContent`

웹 사이트의 콘텐츠 페이지 중 일부에는 하나 또는 두 개의 콘텐츠 컨트롤만 포함 됩니다. 다른 항목에는 사용 가능한 각 ContentPlaceHolders 표시자에 대 한 콘텐츠 컨트롤이 포함 됩니다. `Site.master`의 모든 ContentPlaceHolders 표시자에 대 한 콘텐츠 컨트롤을 포함 하는 콘텐츠 페이지에 새 마스터 페이지 (`Alternate.master`)를 할당 하는 경우에도 `Site.master`와 동일한 ContentPlaceHolder 컨트롤을 `Alternate.master` 하는 것이 중요 합니다.

`Alternate.master` 마스터 페이지가 광산과 비슷하게 보이도록 하려면 (그림 4 참조) `AlternateStyles.css` 스타일 시트에서 마스터 페이지의 스타일을 정의 하는 것부터 시작 합니다. `AlternateStyles.css`에 다음 규칙을 추가 합니다.

[!code-css[Main](specifying-the-master-page-programmatically-vb/samples/sample5.css)]

그런 다음 `Alternate.master`에 다음 선언적 태그를 추가 합니다. 여기에서 볼 수 있듯이 `Alternate.master`에는 `Site.master`의 ContentPlaceHolder 컨트롤과 동일한 `ID` 값을 가진 4 개의 ContentPlaceHolder 컨트롤이 포함 되어 있습니다. 또한 ASP.NET AJAX 프레임 워크를 사용 하는 웹 사이트의 해당 페이지에 필요한 ScriptManager 컨트롤을 포함 합니다.

[!code-aspx[Main](specifying-the-master-page-programmatically-vb/samples/sample6.aspx)]

### <a name="testing-the-new-master-page"></a>새 마스터 페이지 테스트

이 새 마스터 페이지를 테스트 하려면 `MasterPageFile` 속성에 `"~/Alternate.maser"` 값이 할당 되도록 `BasePage` 클래스의 `OnPreInit` 메서드를 업데이트 한 후 웹 사이트를 방문 합니다. `~/Admin/AddProduct.aspx` 및 `~/Admin/Products.aspx`를 제외 하 고 모든 페이지가 오류 없이 작동 해야 합니다. `~/Admin/AddProduct.aspx`에서 DetailsView에 제품을 추가 하면 마스터 페이지의 `GridMessageText` 속성을 설정 하려고 시도 하는 코드 줄에서 `NullReferenceException` 발생 합니다. `~/Admin/Products.aspx` 방문할 때 "'\_.ASP ' 형식의 개체를 ' .asp\_master ' 형식으로 캐스팅할 수 없습니다." 라는 메시지와 함께 페이지 로드 시 `InvalidCastException` throw 됩니다.

이러한 오류는 `Site.master` 코드 숨김이 `Alternate.master`에 정의 되지 않은 공용 이벤트, 속성 및 메서드를 포함 하기 때문에 발생 합니다. 이러한 두 페이지의 태그 부분에는 `Site.master` 마스터 페이지를 참조 하는 `@MasterType` 지시문이 있습니다.

[!code-aspx[Main](specifying-the-master-page-programmatically-vb/samples/sample7.aspx)]

또한 `~/Admin/AddProduct.aspx`의 DetailsView의 `ItemInserted` 이벤트 처리기에는 느슨하게 형식화 된 `Page.Master` 속성을 `Site`형식의 개체로 캐스팅 하는 코드가 포함 되어 있습니다. `@MasterType` 지시문 (이러한 방식으로 사용 됨) 및 `ItemInserted` 이벤트 처리기의 캐스팅은 `~/Admin/AddProduct.aspx` 및 `~/Admin/Products.aspx` 페이지를 `Site.master` 마스터 페이지로 긴밀 하 게 결합.

이 밀접 한 결합을 중단 하기 위해 `Site.master` 하 고 공용 멤버에 대 한 정의를 포함 하는 공통 기본 클래스에서 파생 `Alternate.master` 파생 시킬 수 있습니다. 다음에는이 공통 기본 형식을 참조 하도록 `@MasterType` 지시어를 업데이트할 수 있습니다.

### <a name="creating-a-custom-base-master-page-class"></a>사용자 지정 기본 마스터 페이지 클래스 만들기

`BaseMasterPage.vb` 이라는 `App_Code` 폴더에 새 클래스 파일을 추가 하 고 `System.Web.UI.MasterPage`에서 파생 되도록 합니다. `BaseMasterPage`에서 `RefreshRecentProductsGrid` 메서드와 `GridMessageText` 속성을 정의 해야 하지만 `Site.master`에서 해당 멤버를 이동할 수 없습니다. 이러한 멤버는 `Site.master` 마스터 페이지 (`RecentProducts` GridView 및 `GridMessage` 레이블)와 관련 된 웹 컨트롤에서 작동 하기 때문입니다.

이러한 멤버는 이러한 멤버를 정의 하지만 실제로는 `BaseMasterPage`의 파생 클래스 (`Site.master` 및 `Alternate.master`)에 의해 구현 되는 방식으로 `BaseMasterPage` 구성 해야 합니다. 이 유형의 상속은 클래스를 `MustInherit`으로 표시 하 고 해당 멤버를 `MustOverride`으로 표시 하 여 수행할 수 있습니다. 간단히 말해서 이러한 키워드를 클래스에 추가 하 고 해당 두 개의 멤버가 `BaseMasterPage` `RefreshRecentProductsGrid` 및 `GridMessageText`구현 되지 않았지만 파생 된 클래스에 대해이를 알립니다.

또한 `BaseMasterPage`에서 `PricesDoubled` 이벤트를 정의 하 고 파생 클래스에서 이벤트를 발생 시킬 수 있는 수단을 제공 해야 합니다. 이 동작을 용이 하 게 하기 위해 .NET Framework에 사용 되는 패턴은 기본 클래스에서 공용 이벤트를 만들고 `OnEventName`라는 보호 된 재정의 가능한 메서드를 추가 하는 것입니다. 그런 다음 파생 된 클래스는이 메서드를 호출 하 여 이벤트를 발생 시키거나 이벤트 발생 전후에 코드를 즉시 실행 하도록 재정의할 수 있습니다.

다음 코드를 포함 하도록 `BaseMasterPage` 클래스를 업데이트 합니다.

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample8.vb)]

그런 다음 `Site.master` 코드 숨김으로 클래스로 이동 하 여 `BaseMasterPage`에서 파생 시킵니다. `BaseMasterPage`에 `MustOverride` 표시 된 멤버가 포함 되어 있으므로 `Site.master`에서 해당 멤버를 재정의 해야 합니다. 메서드 및 속성 정의에 `Overrides` 키워드를 추가 합니다. 또한 기본 클래스의 `OnPricesDoubled` 메서드를 호출 하 여 `DoublePrice` 단추의 `Click` 이벤트 처리기에서 `PricesDoubled` 이벤트를 발생 시키는 코드를 업데이트 합니다.

이러한 수정 후 `Site.master` 코드를 포함 하는 클래스는 다음 코드를 포함 해야 합니다.

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample9.vb)]

`BaseMasterPage`에서 파생 하 고 두 개의 `MustOverride` 멤버를 재정의 하려면 `Alternate.master`의 코드 숨김이 클래스도 업데이트 해야 합니다. 그러나 `Alternate.master`에는 최신 제품을 나열 하는 GridView와 새 제품이 데이터베이스에 추가 된 후 메시지를 표시 하는 레이블이 포함 되지 않기 때문에 이러한 메서드는 아무것도 수행할 필요가 없습니다.

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample10.vb)]

### <a name="referencing-the-base-master-page-class"></a>기본 마스터 페이지 클래스 참조

이제 `BaseMasterPage` 클래스를 완료 하 고 두 개의 마스터 페이지가 확장 되었으므로 최종 단계는이 공통 형식을 참조 하도록 `~/Admin/AddProduct.aspx` 및 `~/Admin/Products.aspx` 페이지를 업데이트 하는 것입니다. 에서 두 페이지의 `@MasterType` 지시어를 변경 하 여 시작 합니다.

[!code-aspx[Main](specifying-the-master-page-programmatically-vb/samples/sample11.aspx)]

받는 사람:

[!code-aspx[Main](specifying-the-master-page-programmatically-vb/samples/sample12.aspx)]

`@MasterType` 속성은 파일 경로를 참조 하는 대신 기본 형식 (`BaseMasterPage`)을 참조 합니다. 결과적으로, 두 페이지의 코드 숨김이 클래스에서 사용 되는 강력한 형식의 `Master` 속성은 이제 `Site`형식이 아닌 `BaseMasterPage` 형식입니다. 이렇게 변경 하면 `~/Admin/Products.aspx`다시 시작 됩니다. 이전에는 페이지가 `Alternate.master` 마스터 페이지를 사용 하도록 구성 되어 있지만 `@MasterType` 지시문이 `Site.master` 파일을 참조 하기 때문에 캐스팅 오류가 발생 했습니다. 그러나 이제 페이지는 오류 없이 렌더링 됩니다. 이는 `Alternate.master` 마스터 페이지가 확장 된 후 `BaseMasterPage` 형식의 개체로 캐스팅 될 수 있기 때문입니다.

`~/Admin/AddProduct.aspx`에서 수행 해야 하는 작은 변경 내용이 하나 있습니다. DetailsView 컨트롤의 `ItemInserted` 이벤트 처리기는 강력한 형식의 `Master` 속성과 느슨하게 형식화 된 `Page.Master` 속성을 모두 사용 합니다. `@MasterType` 지시어를 업데이트할 때 강력한 형식의 참조를 수정 했지만 느슨하게 형식화 된 참조를 업데이트 해야 합니다. 다음 코드 줄을 바꿉니다.

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample13.vb)]

다음을 사용 하 여 `Page.Master` 기본 형식으로 캐스팅 합니다.

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample14.vb)]

## <a name="step-4-determining-what-master-page-to-bind-to-the-content-pages"></a>4 단계: 콘텐츠 페이지에 바인딩할 마스터 페이지 결정

`BasePage` 클래스는 현재 페이지 수명 주기의 PreInit 단계에서 하드 코드 된 값으로 모든 콘텐츠 페이지의 `MasterPageFile` 속성을 설정 합니다. 이 코드를 업데이트 하 여 일부 외부 요소에서 마스터 페이지의 기반이 되도록 할 수 있습니다. 로드할 마스터 페이지는 현재 로그온 한 사용자의 기본 설정에 따라 달라 집니다. 이 경우 현재 방문한 사용자의 마스터 페이지 기본 설정을 조회 하는 `BasePage`의 `OnPreInit` 메서드에서 코드를 작성 해야 합니다.

사용자가 `Site.master` 또는 `Alternate.master`를 사용 하 여 마스터 페이지를 선택 하 고이 선택 항목을 세션 변수에 저장할 수 있는 웹 페이지를 만들어 보겠습니다. `ChooseMasterPage.aspx`이라는 루트 디렉터리에 새 웹 페이지를 만들어 시작 합니다. 이 페이지 또는 다른 콘텐츠 페이지 예측이를 만들 때 마스터 페이지가 `BasePage`에서 프로그래밍 방식으로 설정 되기 때문에 마스터 페이지에 바인딩할 필요가 없습니다. 그러나 새 페이지를 마스터 페이지에 바인딩하지 않으면 새 페이지의 기본 선언적 태그에 웹 폼 및 마스터 페이지에서 제공 하는 다른 콘텐츠가 포함 됩니다. 이 태그를 적절 한 콘텐츠 컨트롤로 수동으로 바꾸어야 합니다. 이러한 이유로 새 ASP.NET 페이지를 마스터 페이지에 바인딩하는 것이 더 쉽습니다.

> [!NOTE]
> `Site.master` 및 `Alternate.master`는 ContentPlaceHolder 컨트롤 집합이 동일 하기 때문에 새 콘텐츠 페이지를 만들 때 어떤 마스터 페이지를 선택 하 든 상관 없습니다. 일관성을 위해 `Site.master`를 사용 하는 것이 좋습니다.

[웹 사이트에 새 콘텐츠 페이지를 추가 ![](specifying-the-master-page-programmatically-vb/_static/image14.png)](specifying-the-master-page-programmatically-vb/_static/image13.png)

**그림 05**: 웹 사이트에 새 콘텐츠 페이지 추가 ([전체 크기 이미지를 보려면 클릭](specifying-the-master-page-programmatically-vb/_static/image15.png))

이 단원에 대 한 항목을 포함 하도록 `Web.sitemap` 파일을 업데이트 합니다. Master Pages 및 ASP.NET AJAX 단원의 `<siteMapNode>` 아래에 다음 태그를 추가 합니다.

[!code-xml[Main](specifying-the-master-page-programmatically-vb/samples/sample15.xml)]

`ChooseMasterPage.aspx` 페이지에 콘텐츠를 추가 하기 전에 페이지의 코드 숨김이 클래스를 업데이트 하 여 `BasePage` (`System.Web.UI.Page`아닌)에서 파생 되도록 합니다. 그런 다음 페이지에 DropDownList 컨트롤을 추가 하 고, 해당 `ID` 속성을 `MasterPageChoice`로 설정 하 고, "~/Site.master" 및 "~/Alternate.master"의 `Text` 값을 사용 하 여 두 개의 ListItems를 추가 합니다.

단추 웹 컨트롤을 페이지에 추가 하 고 해당 `ID` 및 `Text` 속성을 `SaveLayout` 및 "레이아웃 선택 저장"으로 설정 합니다. 이 시점에서 페이지의 선언 태그는 다음과 같이 표시 됩니다.

[!code-aspx[Main](specifying-the-master-page-programmatically-vb/samples/sample16.aspx)]

페이지를 처음 방문할 때 사용자의 현재 선택 된 마스터 페이지를 표시 해야 합니다. `Page_Load` 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample17.vb)]

위의 코드는 첫 번째 페이지 방문 에서만 실행 되며 이후 포스트백에는 실행 되지 않습니다. 먼저 세션 변수가 `MyMasterPage` 있는지 확인 합니다. 이 경우 `MasterPageChoice` DropDownList에서 일치 하는 ListItem을 찾으려고 시도 합니다. 일치 하는 ListItem이 있으면 해당 `Selected` 속성이 `True`로 설정 됩니다.

또한 사용자의 선택 항목을 `MyMasterPage` 세션 변수에 저장 하는 코드도 필요 합니다. `SaveLayout` 단추의 `Click` 이벤트에 대 한 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample18.vb)]

> [!NOTE]
> 다시 게시 될 때 `Click` 이벤트 처리기가 실행 될 때 마스터 페이지가 이미 선택 되어 있습니다. 따라서 사용자의 드롭다운 목록 선택은 다음 페이지가 방문할 때까지 적용 되지 않습니다. `Response.Redirect`는 브라우저가 `ChooseMasterPage.aspx`를 다시 요청 하도록 합니다.

`ChooseMasterPage.aspx` 페이지가 완료 되 면 최종 작업에서 `MyMasterPage` 세션 변수의 값을 기반으로 `MasterPageFile` 속성을 할당 `BasePage` 합니다. 세션 변수가 설정 되지 않은 경우 `BasePage` 기본값을 `Site.master`로 설정 합니다.

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample19.vb)]

> [!NOTE]
> `Page` 개체의 `MasterPageFile` 속성을 할당 하는 코드를 `OnPreInit` 이벤트 처리기와 두 개의 개별 메서드로 이동 했습니다. 이 첫 번째 메서드인 `SetMasterPageFile`는 두 번째 메서드인 `GetMasterPageFileFromSession`에서 반환 된 값에 `MasterPageFile` 속성을 할당 합니다. `BasePage`를 확장 하는 이후 클래스가 필요한 경우 사용자 지정 논리를 구현 하기 위해 선택적으로 재정의할 수 있도록 `SetMasterPageFile` 메서드 `Overridable` 표시 했습니다. 다음 자습서에서 `BasePage`의 `SetMasterPageFile` 속성을 재정의 하는 예제가 나와 있습니다.

이 코드가 준비 되 면 `ChooseMasterPage.aspx` 페이지를 방문 하세요. 처음에는 `Site.master` 마스터 페이지가 선택 되어 있습니다 (그림 6 참조). 그러나 사용자는 드롭다운 목록에서 다른 마스터 페이지를 선택할 수 있습니다.

[![콘텐츠 페이지는 사이트 마스터 페이지를 사용 하 여 표시 됩니다.](specifying-the-master-page-programmatically-vb/_static/image17.png)](specifying-the-master-page-programmatically-vb/_static/image16.png)

**그림 06**: `Site.master` 마스터 페이지를 사용 하 여 콘텐츠 페이지가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](specifying-the-master-page-programmatically-vb/_static/image18.png)).

[이제 대체 마스터 페이지를 사용 하 여 콘텐츠 페이지 ![표시 됩니다.](specifying-the-master-page-programmatically-vb/_static/image20.png)](specifying-the-master-page-programmatically-vb/_static/image19.png)

**그림 07**: 이제 `Alternate.master` 마스터 페이지를 사용 하 여 콘텐츠 페이지가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](specifying-the-master-page-programmatically-vb/_static/image21.png)).

## <a name="summary"></a>요약

콘텐츠 페이지를 방문 하면 해당 콘텐츠 컨트롤은 마스터 페이지의 ContentPlaceHolder 컨트롤을 사용 하 여 퓨즈 됩니다. 콘텐츠 페이지의 마스터 페이지는 `Page` 클래스의 `MasterPageFile` 속성으로 표시 됩니다 .이 속성은 초기화 단계에서 `@Page` 지시문의 `MasterPageFile` 특성에 할당 됩니다. 이 자습서에 설명 된 대로 PreInit 단계를 완료 하기 전에 `MasterPageFile` 속성에 값을 할당할 수 있습니다. 마스터 페이지를 프로그래밍 방식으로 지정할 수 있으면 외부 요소에 따라 콘텐츠 페이지를 마스터 페이지에 동적으로 바인딩하는 것과 같은 고급 시나리오를 위한 도어가 열립니다.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 정보

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 페이지 수명 주기 다이어그램](http://emanish.googlepages.com/Asp.Net2.0Lifecycle.PNG)
- [ASP.NET 페이지 수명 주기 개요](https://msdn.microsoft.com/library/ms178472.aspx)
- [ASP.NET 테마 및 스킨 개요](https://msdn.microsoft.com/library/ykzx33wh.aspx)
- [마스터 페이지: 팁, 요령 및 트랩](http://www.odetocode.com/articles/450.aspx)
- [ASP.NET의 테마](http://www.odetocode.com/articles/423.aspx)

### <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)는 여러 ASP/ASP. NET books의 작성자와 4GuysFromRolla.com의 창립자가 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 3.5을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)것입니다. Scott은 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) 또는 [http://ScottOnWriting.NET](http://scottonwriting.net/)의 블로그를 통해 연결할 수 있습니다.

### <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Suchi Banerjee. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) 에 줄을 놓습니다.

> [!div class="step-by-step"]
> [이전](master-pages-and-asp-net-ajax-vb.md)
> [다음](nested-master-pages-vb.md)
