---
uid: web-forms/overview/data-access/introduction/master-pages-and-site-navigation-vb
title: 마스터 페이지 및 사이트 탐색 (VB) | Microsoft Docs
author: rick-anderson
description: 사용자에 게 친숙 한 웹 사이트의 한 가지 일반적인 특징은 일관 된 사이트 전체 페이지 레이아웃 및 탐색 구성표를 갖는 것입니다. 이 자습서에서는 다음을 보여 줍니다.
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 022801d8-a327-4d0c-8780-6094c9cee00d
msc.legacyurl: /web-forms/overview/data-access/introduction/master-pages-and-site-navigation-vb
msc.type: authoredcontent
ms.openlocfilehash: 4a2b5ba8c1781f1194f951a44661a8f7dd095f41
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78426029"
---
# <a name="master-pages-and-site-navigation-vb"></a>마스터 페이지 및 사이트 탐색(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_3_VB.exe) 또는 [PDF 다운로드](master-pages-and-site-navigation-vb/_static/datatutorial03vb1.pdf)

> 사용자에 게 친숙 한 웹 사이트의 한 가지 일반적인 특징은 일관 된 사이트 전체 페이지 레이아웃 및 탐색 구성표를 갖는 것입니다. 이 자습서에서는 쉽게 업데이트할 수 있는 모든 페이지에서 일관 된 모양과 느낌을 만드는 방법을 살펴봅니다.

## <a name="introduction"></a>소개

사용자에 게 친숙 한 웹 사이트의 한 가지 일반적인 특징은 일관 된 사이트 전체 페이지 레이아웃 및 탐색 구성표를 갖는 것입니다. ASP.NET 2.0에는 사이트 전체 페이지 레이아웃 및 탐색 구성표 (마스터 페이지 및 사이트 탐색)를 구현 하는 작업을 크게 간소화 하는 두 가지 새로운 기능이 도입 되었습니다. 마스터 페이지를 사용 하면 개발자가 지정 된 편집 가능한 영역으로 사이트 전체 템플릿을 만들 수 있습니다. 그런 다음이 템플릿을 사이트의 ASP.NET 페이지에 적용할 수 있습니다. 이러한 ASP.NET 페이지는 마스터 페이지의 지정 된 편집 가능한 영역에 대 한 콘텐츠만 제공 해야 합니다. 마스터 페이지의 다른 모든 태그는 마스터 페이지를 사용 하는 모든 ASP.NET 페이지에서 동일 합니다. 이 모델을 사용 하면 개발자가 사이트 전체 페이지 레이아웃을 정의 하 고 중앙 집중화 하 여 쉽게 업데이트할 수 있는 모든 페이지에서 일관 된 모양과 느낌을 쉽게 만들 수 있습니다.

사이트 [탐색 시스템](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx) 은 페이지 개발자가 프로그래밍 방식으로 쿼리할 수 있도록 사이트 맵과 해당 사이트 맵에 대 한 API를 정의 하는 메커니즘을 제공 합니다. 새 탐색 웹에서 메뉴, TreeView 및 SiteMapPath 컨트롤을 사용 하면 일반적인 탐색 사용자 인터페이스 요소에서 사이트 맵의 전체 또는 일부를 쉽게 렌더링할 수 있습니다. 기본 사이트 탐색 공급자를 사용 합니다. 즉, 사이트 맵은 XML 형식 파일에 정의 됩니다.

이러한 개념을 설명 하 고 자습서 웹 사이트를 더 사용할 수 있도록 하려면 사이트 전체 페이지 레이아웃 정의, 사이트 맵 구현 및 탐색 UI 추가 단원을 살펴보겠습니다. 이 자습서를 마치면 자습서 웹 페이지를 빌드하기 위한 세련 된 웹 사이트 디자인이 제공 됩니다.

[이 자습서의 최종 결과 ![](master-pages-and-site-navigation-vb/_static/image2.png)](master-pages-and-site-navigation-vb/_static/image1.png)

**그림 1**:이 자습서의 최종 결과 ([전체 크기 이미지를 보려면 클릭](master-pages-and-site-navigation-vb/_static/image3.png))

## <a name="step-1-creating-the-master-page"></a>1 단계: 마스터 페이지 만들기

첫 번째 단계는 사이트의 마스터 페이지를 만드는 것입니다. 현재 웹 사이트는 형식화 된 데이터 집합 (`Northwind.xsd`, `App_Code` 폴더), BLL 클래스 (`ProductsBLL.vb`, `CategoriesBLL.vb`등), 데이터베이스 (`App_Code` 폴더의`NORTHWND.MDF`), 구성 파일 (`App_Data`) 및 CSS 스타일 시트 파일 (`Web.config`) 으로만 구성 됩니다.`Styles.css` 앞의 자습서에서 이러한 예제를 더 자세히 reexamining 하기 때문에 처음 두 자습서에서 DAL 및 BLL을 사용 하는 것을 보여 주는 해당 페이지와 파일을 정리 했습니다.

![프로젝트의 파일](master-pages-and-site-navigation-vb/_static/image4.png)

**그림 2**: 프로젝트의 파일

마스터 페이지를 만들려면 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 새 항목 추가를 선택 합니다. 그런 다음 템플릿 목록에서 마스터 페이지 유형을 선택 하 고 `Site.master`이름을로 지정한 다음

[웹 사이트에 새 마스터 페이지를 추가 ![](master-pages-and-site-navigation-vb/_static/image6.png)](master-pages-and-site-navigation-vb/_static/image5.png)

**그림 3**: 웹 사이트에 새 마스터 페이지 추가 ([전체 크기 이미지를 보려면 클릭](master-pages-and-site-navigation-vb/_static/image7.png))

마스터 페이지에서 사이트 전체 페이지 레이아웃을 정의 합니다. 디자인 뷰를 사용 하 여 필요한 모든 레이아웃 또는 웹 컨트롤을 추가 하거나 소스 뷰에서 직접 태그를 추가할 수 있습니다. 내 마스터 페이지에서 css [스타일 시트](http://www.w3schools.com/css/default.asp) 를 사용 하 여 외부 파일 `Style.css`에 정의 된 css 설정을 사용 하 여 위치를 지정 하 고 스타일을 지정 합니다. 아래에 표시 된 태그를 구분할 수는 없지만, 탐색 `<div>`의 내용이 왼쪽에 표시 되 고 너비가 200 픽셀이 고정 되도록 하는 것을 의미 합니다.

Site.master

[!code-aspx[Main](master-pages-and-site-navigation-vb/samples/sample1.aspx)]

마스터 페이지는 정적 페이지 레이아웃 및 마스터 페이지를 사용 하는 ASP.NET 페이지에서 편집할 수 있는 영역을 모두 정의 합니다. 이러한 콘텐츠 편집 가능한 영역은 ContentPlaceHolder 컨트롤에 의해 표시 됩니다 .이 컨트롤은 콘텐츠 `<div>`내에서 볼 수 있습니다. 마스터 페이지에는 단일 ContentPlaceHolder (`MainContent`)가 있지만 마스터 페이지의 ContentPlaceHolders 표시자는 여러 개 있을 수 있습니다.

위에 입력 된 태그를 사용 하 여 디자인 뷰로 전환 하면 마스터 페이지의 레이아웃이 표시 됩니다. 이 마스터 페이지를 사용 하는 모든 ASP.NET 페이지는 `MainContent` 영역에 대 한 태그를 지정 하는 기능과 함께이 균일 한 레이아웃을 갖게 됩니다.

[디자인 뷰를 통해 볼 때 마스터 페이지 ![](master-pages-and-site-navigation-vb/_static/image9.png)](master-pages-and-site-navigation-vb/_static/image8.png)

**그림 4**: 디자인 뷰를 통해 볼 때 마스터 페이지 ([전체 크기 이미지를 보려면 클릭](master-pages-and-site-navigation-vb/_static/image10.png))

## <a name="step-2-adding-a-homepage-to-the-website"></a>2 단계: 웹 사이트에 홈 페이지 추가

마스터 페이지를 정의한 상태에서 웹 사이트에 대 한 ASP.NET 페이지를 추가할 준비가 되었습니다. 웹 사이트의 홈페이지 인 `Default.aspx`를 추가 하는 것부터 시작 해 보겠습니다. 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 새 항목 추가를 선택 합니다. 템플릿 목록에서 Web Form 옵션을 선택 하 고 파일 이름을 `Default.aspx`로 합니다. 또한 "마스터 페이지 선택" 확인란을 선택 합니다.

[새 웹 폼을 추가 ![마스터 페이지 선택 확인란을 선택 합니다.](master-pages-and-site-navigation-vb/_static/image12.png)](master-pages-and-site-navigation-vb/_static/image11.png)

**그림 5**: 마스터 페이지 선택 확인란을 선택 하 여 새 웹 폼 추가 ([전체 크기 이미지를 보려면 클릭](master-pages-and-site-navigation-vb/_static/image13.png))

확인 단추를 클릭 한 후이 새 ASP.NET 페이지에서 사용 해야 하는 마스터 페이지를 선택 하 라는 메시지가 표시 됩니다. 프로젝트에 마스터 페이지를 여러 개 포함할 수 있지만 여기에는 1 개만 있습니다.

[이 ASP.NET 페이지에서 사용 해야 하는 마스터 페이지 ![선택 합니다.](master-pages-and-site-navigation-vb/_static/image15.png)](master-pages-and-site-navigation-vb/_static/image14.png)

**그림 6**:이 ASP.NET 페이지에서 사용 해야 하는 마스터 페이지 선택 ([전체 크기 이미지를 보려면 클릭](master-pages-and-site-navigation-vb/_static/image16.png))

마스터 페이지를 선택 하면 새 ASP.NET 페이지에 다음 태그가 포함 됩니다.

Default.aspx

[!code-aspx[Main](master-pages-and-site-navigation-vb/samples/sample2.aspx)]

`@Page` 지시문에는 사용 된 마스터 페이지 파일에 대 한 참조가 있습니다 (`MasterPageFile="~/Site.master"`). ASP.NET 페이지의 태그에는 마스터 페이지에 정의 된 각 ContentPlaceHolder 컨트롤에 대 한 콘텐츠 컨트롤이 포함 되어 있으며, 컨트롤의 `ContentPlaceHolderID`는 특정 ContentPlaceHolder에 콘텐츠 컨트롤을 매핑합니다. 콘텐츠 컨트롤은 해당 ContentPlaceHolder 표시 하려는 태그를 저장 하는 위치입니다. `@Page` 지시문의 `Title` 특성을 홈으로 설정 하 고 콘텐츠 컨트롤에 몇 가지 환영 콘텐츠를 추가 합니다.

Default.aspx

[!code-aspx[Main](master-pages-and-site-navigation-vb/samples/sample3.aspx)]

`@Page` 지시문의 `Title` 특성을 사용 하면 `<title>` 요소가 마스터 페이지에 정의 되어 있는 경우에도 페이지의 제목을 ASP.NET 페이지에서 설정할 수 있습니다. `Page.Title`를 사용 하 여 프로그래밍 방식으로 제목을 설정할 수도 있습니다. 또한 마스터 페이지의 스타일 시트 (예: `Style.css`)에 대 한 참조는 ASP.NET 페이지가 마스터 페이지를 기준으로 하는 디렉터리에 관계 없이 모든 ASP.NET 페이지에서 작동 하도록 자동으로 업데이트 됩니다.

디자인 뷰로 전환 하면 브라우저에서 페이지가 어떻게 표시 되는지 확인할 수 있습니다. ASP.NET 페이지에 대 한 콘텐츠 편집 가능 영역만 편집할 수 있는 경우 마스터 페이지에 정의 된 비 ContentPlaceHolder 태그는 회색으로 표시 됩니다. 디자인 뷰

[ASP.NET 페이지에 대 한 디자인 보기 ![편집 가능 하 고 편집 가능 하지 않은 영역이 모두 표시 됩니다.](master-pages-and-site-navigation-vb/_static/image18.png)](master-pages-and-site-navigation-vb/_static/image17.png)

**그림 7**: ASP.NET 페이지의 디자인 뷰에는 편집 가능 하 고 편집 가능 하지 않은 영역이 모두 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-pages-and-site-navigation-vb/_static/image19.png)).

브라우저에서 `Default.aspx` 페이지를 방문 하면 ASP.NET 엔진이 페이지의 마스터 페이지 콘텐츠와 ASP를 자동으로 병합 합니다. NET의 콘텐츠를 통해 병합 된 콘텐츠를 요청 하는 브라우저로 전송 되는 최종 HTML로 렌더링 합니다. 마스터 페이지의 콘텐츠가 업데이트 되 면이 마스터 페이지를 사용 하는 모든 ASP.NET 페이지의 콘텐츠는 다음에 요청 될 때 새 마스터 페이지 콘텐츠와 다시 병합 됩니다. 간단히 말해서, 마스터 페이지 모델을 사용 하면 전체 사이트에서 변경 내용이 즉시 반영 되는 단일 페이지 레이아웃 템플릿 (마스터 페이지)을 정의할 수 있습니다.

## <a name="adding-additional-aspnet-pages-to-the-website"></a>웹 사이트에 추가 ASP.NET 페이지 추가

궁극적으로 다양 한 보고 데모를 포함 하는 사이트에 ASP.NET 페이지 스텁을 추가 해 보겠습니다. 총 데모 수가 35 개를 초과 하 게 되므로 스텁 페이지를 모두 만드는 것이 아니라 처음 몇 가지를 만들어 보겠습니다. 데모를 보다 효율적으로 관리 하기 위해 데모의 많은 범주가 있으므로 범주에 대 한 폴더 추가도 있습니다. 지금은 다음 세 개의 폴더를 추가 합니다.

- `BasicReporting`
- `Filtering`
- `CustomFormatting`

마지막으로 그림 8의 솔루션 탐색기 같이 새 파일을 추가 합니다. 각 파일을 추가할 때 "마스터 페이지 선택" 확인란을 선택 해야 합니다.

![다음 파일을 추가 합니다.](master-pages-and-site-navigation-vb/_static/image20.png)

**그림 8**: 다음 파일 추가

## <a name="step-2-creating-a-site-map"></a>2 단계: 사이트 맵 만들기

몇 페이지로 구성 된 웹 사이트를 관리 하는 문제 중 하나는 방문자가 사이트를 탐색 하는 간단한 방법을 제공 하는 것입니다. 먼저 사이트의 탐색 구조를 정의 해야 합니다. 그런 다음이 구조는 메뉴 또는 이동 경로와 같은 탐색 가능한 사용자 인터페이스 요소로 변환 되어야 합니다. 마지막으로, 사이트에 새 페이지를 추가 하 고 기존 페이지를 제거 하면 전체 프로세스를 유지 관리 하 고 업데이트 해야 합니다. ASP.NET 2.0 이전에는 개발자가 사이트의 탐색 구조를 만들어 유지 관리 하 고 탐색 가능한 사용자 인터페이스 요소로 변환 하는 기능을가지고 있었습니다. 그러나 ASP.NET 2.0를 사용 하 여 개발자는 매우 유연한 기본 제공 사이트 탐색 시스템을 활용할 수 있습니다.

ASP.NET 2.0 사이트 탐색 시스템은 개발자가 사이트 맵을 정의한 다음 프로그래밍 방식 API를 통해이 정보에 액세스할 수 있는 방법을 제공 합니다. ASP.NET에는 사이트 맵 데이터를 특정 방식으로 형식이 지정 된 XML 파일에 저장 해야 하는 사이트 맵 공급자가 제공 됩니다. 그러나 사이트 탐색 시스템은 [공급자 모델](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx) 을 기반으로 하기 때문에 사이트 맵 정보를 serialize 하는 다른 방법을 지원 하도록 확장할 수 있습니다. Jeff Prosise의 문서에서 [대기 중인 SQL 사이트 맵 공급자는](https://msdn.microsoft.com/msdnmag/issues/06/02/WickedCode/default.aspx) 사이트 맵을 SQL Server 데이터베이스에 저장 하는 사이트 맵 공급자를 만드는 방법을 보여 줍니다. 또 다른 옵션은 [파일 시스템 구조를 기반으로 사이트 맵 공급자를](http://aspnet.4guysfromrolla.com/articles/020106-1.aspx)만드는 것입니다.

그러나이 자습서에서는 ASP.NET 2.0와 함께 제공 되는 기본 사이트 맵 공급자를 사용 하겠습니다. 사이트 맵을 만들려면 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 새 항목 추가를 선택한 다음 사이트 맵 옵션을 선택 하면 됩니다. 이름을 `Web.sitemap`로 두고 추가 단추를 클릭 합니다.

[프로젝트에 사이트 맵을 추가 ![](master-pages-and-site-navigation-vb/_static/image22.png)](master-pages-and-site-navigation-vb/_static/image21.png)

**그림 9**: 프로젝트에 사이트 맵 추가 ([전체 크기 이미지를 보려면 클릭](master-pages-and-site-navigation-vb/_static/image23.png))

사이트 맵 파일은 XML 파일입니다. Visual Studio는 사이트 맵 구조에 대해 IntelliSense를 제공 합니다. 사이트 맵 파일은 루트 노드로 `<siteMap>` 노드를 포함 해야 합니다 .이 노드는 정확히 하나의 `<siteMapNode>` 자식 요소를 포함 해야 합니다. 첫 번째 `<siteMapNode>` 요소에는 임의 개수의 하위 `<siteMapNode>` 요소가 포함 될 수 있습니다.

파일 시스템 구조와 비슷하게 사이트 맵을 정의 합니다. 즉, 3 개의 폴더 각각에 대해 `<siteMapNode>` 요소를 추가 하 고 다음과 같이 해당 폴더의 각 ASP.NET 페이지에 대해 자식 `<siteMapNode>` 요소를 추가 합니다.

Web.sitemap

[!code-xml[Main](master-pages-and-site-navigation-vb/samples/sample4.xml)]

사이트 맵은 사이트의 다양 한 섹션을 설명 하는 계층 인 웹 사이트의 탐색 구조를 정의 합니다. `Web.sitemap`의 각 `<siteMapNode>` 요소는 사이트의 탐색 구조에 있는 섹션을 나타냅니다.

[사이트 맵이 계층 구조 탐색 구조를 나타내는 ![](master-pages-and-site-navigation-vb/_static/image25.png)](master-pages-and-site-navigation-vb/_static/image24.png)

**그림 10**: 계층 구조 탐색 구조를 나타내는 사이트 맵 ([전체 크기 이미지를 보려면 클릭](master-pages-and-site-navigation-vb/_static/image26.png))

ASP.NET는 .NET Framework의 사이트 맵 [클래스](https://msdn.microsoft.com/library/system.web.sitemap.aspx)를 통해 사이트 맵 구조를 노출 합니다. 이 클래스에는 사용자가 현재 방문 하 고 있는 섹션에 대 한 정보를 반환 하는 `CurrentNode` 속성이 있습니다. `RootNode` 속성은 사이트 맵 (홈)의 루트를 반환 합니다. `CurrentNode` 및 `RootNode` 속성은 모두 사이트 맵 계층 구조를 전달할 수 있는 `ParentNode`, `ChildNodes`, `NextSibling`, `PreviousSibling`등의 속성을 포함 하는 [SiteMapNode](https://msdn.microsoft.com/library/system.web.sitemapnode.aspx) 인스턴스를 반환 합니다.

## <a name="step-3-displaying-a-menu-based-on-the-site-map"></a>3 단계: 사이트 맵 기반 메뉴 표시

ASP.NET 2.0에서 데이터에 액세스 하는 것은 ASP.NET 1.x와 같이 프로그래밍 방식으로 또는 새 [데이터 소스 컨트롤](https://msdn.microsoft.com/library/ms227679.aspx)을 통해 선언적으로 수행할 수 있습니다. SqlDataSource 컨트롤과 같은 몇 가지 기본 제공 데이터 소스 컨트롤이 있습니다. 여기에는 관계형 데이터베이스 데이터 액세스, ObjectDataSource 컨트롤, 클래스의 데이터 액세스 등이 있습니다. [사용자 고유의 사용자 지정 데이터 소스 컨트롤](https://msdn.microsoft.com/asp.net/reference/data/default.aspx?pull=/library/dnvs05/html/DataSourceCon1.asp)을 만들 수도 있습니다.

데이터 원본 컨트롤은 ASP.NET 페이지와 기본 데이터 간의 프록시로 사용 됩니다. 데이터 소스 컨트롤의 검색 된 데이터를 표시 하기 위해 일반적으로 페이지에 다른 웹 컨트롤을 추가 하 고 데이터 소스 컨트롤에 바인딩합니다. 웹 컨트롤을 데이터 소스 컨트롤에 바인딩하려면 웹 컨트롤의 `DataSourceID` 속성을 데이터 소스 컨트롤의 `ID` 속성 값으로 설정 하기만 하면 됩니다.

사이트 맵 데이터로 작업 하는 데 도움이 되도록 ASP.NET에는 웹 사이트의 사이트 맵에 대해 웹 컨트롤을 바인딩할 수 있는 SiteMapDataSource 컨트롤이 포함 되어 있습니다. 두 웹 컨트롤 TreeView 및 메뉴는 일반적으로 탐색 사용자 인터페이스를 제공 하는 데 사용 됩니다. 이러한 두 컨트롤 중 하나에 사이트 맵 데이터를 바인딩하려면 `DataSourceID` 속성이 적절 하 게 설정 된 TreeView 또는 Menu 컨트롤과 함께 SiteMapDataSource를 페이지에 추가 하기만 하면 됩니다. 예를 들어 다음 태그를 사용 하 여 마스터 페이지에 메뉴 컨트롤을 추가할 수 있습니다.

[!code-aspx[Main](master-pages-and-site-navigation-vb/samples/sample5.aspx)]

내보낸 HTML을 보다 세부적으로 제어 하기 위해 다음과 같이 SiteMapDataSource 컨트롤을 Repeater 컨트롤에 바인딩할 수 있습니다.

[!code-aspx[Main](master-pages-and-site-navigation-vb/samples/sample6.aspx)]

SiteMapDataSource 컨트롤은 루트 사이트 맵 노드 (홈, 사이트 맵), 다음 수준 (기본 보고, 보고서 필터링 및 사용자 지정 형식)으로 시작 하 여 한 번에 한 수준으로 사이트 맵 계층 구조를 반환 합니다. SiteMapDataSource를 Repeater에 바인딩하는 경우 반환 되는 첫 번째 수준을 열거 하 고 첫 번째 수준에서 각 `SiteMapNode` 인스턴스의 `ItemTemplate`을 인스턴스화합니다. `SiteMapNode`의 특정 속성에 액세스 하기 위해 `Eval(propertyName)`를 사용할 수 있습니다 .이는 각 `SiteMapNode`의 `Url` 및 하이퍼링크 컨트롤에 대 한 `Title` 속성을 가져오는 방법입니다.

위의 Repeater 예제는 다음과 같은 태그를 렌더링 합니다.

[!code-html[Main](master-pages-and-site-navigation-vb/samples/sample7.html)]

이러한 사이트 맵 노드 (기본 보고, 보고서 필터링 및 사용자 지정 형식)는 첫 번째가 아닌 렌더링 되는 사이트 맵의 *두 번째* 수준으로 구성 됩니다. 이는 SiteMapDataSource의 `ShowStartingNode` 속성이 False로 설정 되어 SiteMapDataSource가 루트 사이트 맵 노드를 무시 하 고 대신 사이트 맵 계층 구조에서 두 번째 수준을 반환 하는 것 이기 때문입니다.

기본 보고에 대 한 자식을 표시 하 고, 보고서를 필터링 하며, 사용자 지정 된 서식 `SiteMapNode` s를 표시 하려면 초기 Repeater의 `ItemTemplate`에 다른 리피터를 추가할 수 있습니다. 이 두 번째 Repeater는 다음과 같이 `SiteMapNode` 인스턴스의 `ChildNodes` 속성에 바인딩됩니다.

[!code-aspx[Main](master-pages-and-site-navigation-vb/samples/sample8.aspx)]

이러한 두 반복기는 다음과 같은 태그를 생성 합니다. 일부 태그는 간단히 나타내기 위해 제거 되었습니다.

[!code-html[Main](master-pages-and-site-navigation-vb/samples/sample9.html)]

[Rachel Andrew](http://www.rachelandrew.co.uk/)의 책에서 선택한 css 스타일을 사용 하 여 [css Anthology: 101 필수 팁, 트릭, &amp; 해킹](https://www.amazon.com/gp/product/0957921888/qid=1137565739/sr=8-1/ref=pd_bbs_1/103-0562306-3386214?n=507846&amp;s=books&amp;v=glance), `<ul>` 및 `<li>` 요소는 태그가 다음과 같은 시각적 출력을 생성 하도록 스타일이 지정 됩니다.

![두 반복기 및 CSS에서 구성 된 메뉴](master-pages-and-site-navigation-vb/_static/image27.png)

**그림 11**: 두 반복기 및 일부 CSS에서 구성 된 메뉴

이 메뉴는 마스터 페이지에 있고 `Web.sitemap`에 정의 된 사이트 맵에 바인딩되어 있습니다. 즉, 사이트 맵에 대 한 모든 변경 내용이 `Site.master` 마스터 페이지를 사용 하는 모든 페이지에 즉시 반영 됩니다.

## <a name="disabling-viewstate"></a>ViewState 사용 안 함

모든 ASP.NET 컨트롤은 렌더링 된 HTML에서 숨겨진 양식 필드로 serialize 된 [뷰 상태](https://msdn.microsoft.com/msdnmag/issues/03/02/CuttingEdge/)에 필요에 따라 상태를 유지할 수 있습니다. 뷰 상태는 데이터 웹 컨트롤에 바인딩된 데이터와 같이 포스트백 간에 프로그래밍 방식으로 변경 된 상태를 기억할 수 있도록 컨트롤에서 사용 됩니다. 뷰 상태는 포스트백을 통해 정보를 기억할 수 있도록 허용 하지만, 클라이언트에 보내야 하는 태그의 크기를 늘려 면밀 하 게 모니터링 하지 않는 경우 심각한 페이지 크기를 초래 합니다. 데이터 웹 컨트롤 특히 GridView는 페이지에 수십 개의 추가 kb 태그를 추가 하는 데 특히 심각한 문제. 이러한 증가는 광대역 또는 인트라넷 사용자의 경우 무시할 수 있지만, 보기 상태는 전화 접속 사용자에 대 한 왕복에 몇 초 정도 추가할 수 있습니다.

보기 상태의 영향을 확인 하려면 브라우저의 페이지를 방문 하 여 웹 페이지에서 보낸 소스를 확인 합니다 (Internet Explorer에서 보기 메뉴로 이동 하 여 원본 옵션 선택). 페이지 [추적](https://msdn.microsoft.com/library/sfbfw58f.aspx) 을 설정 하 여 페이지의 각 컨트롤에서 사용 하는 뷰 상태 할당을 확인할 수도 있습니다. 뷰 상태 정보는 `__VIEWSTATE`이라는 숨겨진 양식 필드에서 serialize 되며 `<div>` 요소에서 여는 `<form>` 태그 바로 뒤에 있습니다. 뷰 상태는 사용 중인 Web Form이 있는 경우에만 지속 됩니다. ASP.NET 페이지의 선언적 구문에 `<form runat="server">` 포함 되어 있지 않으면 렌더링 된 태그에 `__VIEWSTATE` 숨겨진 폼 필드가 없습니다.

마스터 페이지에 의해 생성 된 `__VIEWSTATE` 양식 필드는 페이지의 생성 된 태그에 약 1800 바이트를 추가 합니다. SiteMapDataSource 컨트롤의 내용이 보기 상태로 유지 되기 때문에 이러한 추가 팽창은 주로 Repeater 컨트롤에 의해 발생 합니다. 추가 1800 바이트는 많은 필드와 레코드가 포함 된 GridView를 사용 하는 경우에는 상당한 영향을 받지 않을 수 있지만 뷰 상태를 10 개 이상으로 쉽게 swell 수 있습니다.

뷰 상태는 `EnableViewState` 속성을 `False`로 설정 하 여 렌더링 된 태그의 크기를 줄여 페이지나 컨트롤 수준에서 사용 하지 않도록 설정할 수 있습니다. 데이터 웹 컨트롤에 대 한 뷰 상태는 데이터를 다시 게시 하는 동안 데이터 웹 컨트롤에 바인딩된 데이터를 유지 하므로 데이터 웹 컨트롤에 대 한 뷰 상태를 사용 하지 않도록 설정 하는 경우 데이터는 각 및 포스트백 마다 바인딩되어야 합니다. ASP.NET 버전 1. x에서는이 책임이 페이지 개발자의 접근에 있습니다. 그러나 ASP.NET 2.0를 사용 하는 경우, 필요한 경우 데이터 웹 컨트롤이 다시 게시 될 때마다 데이터 소스 컨트롤에 다시 바인딩됩니다.

페이지의 뷰 상태를 줄이려면 Repeater 컨트롤의 `EnableViewState` 속성을 `False`로 설정 합니다. 이 작업은 디자이너의 속성 창 또는 소스 뷰에서 선언적으로 수행할 수 있습니다. 이러한 변경을 수행한 후에는 Repeater의 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](master-pages-and-site-navigation-vb/samples/sample10.aspx)]

이렇게 변경한 후에는 페이지의 렌더링 된 뷰 상태 크기가 52 바이트로 축소 되 고 97%가 보기 상태 크기로 절감 됩니다. 이 시리즈 전체의 자습서에서는 렌더링 된 태그의 크기를 줄이기 위해 기본적으로 데이터 웹 컨트롤의 뷰 상태를 사용 하지 않도록 설정 합니다. 대부분의 예제에서 `EnableViewState` 속성은 `False`으로 설정 되 고, 여기서는 언급 하지 않고 수행 됩니다. 데이터 웹 컨트롤에서 예상 된 기능을 제공 하기 위해 사용 하도록 설정 해야 하는 시나리오에서는 유일한 시간 보기 상태를 설명 합니다.

## <a name="step-4-adding-breadcrumb-navigation"></a>4 단계: 이동 경로 탐색 추가

마스터 페이지를 완료 하려면 각 페이지에 breadcrumb 탐색 UI 요소를 추가 해 보겠습니다. 이동 경로는 사이트 계층 구조 내에서 사용자의 현재 위치를 빠르게 보여줍니다. ASP.NET 2.0에서 breadcrumb을 추가 하는 것은 페이지에 SiteMapPath 컨트롤을 추가 하는 것이 쉽습니다. 코드가 필요 하지 않습니다.

사이트의 경우 헤더 `<div>`에이 컨트롤을 추가 합니다.

[!code-aspx[Main](master-pages-and-site-navigation-vb/samples/sample11.aspx)]

이동 경로에는 사용자가 사이트 맵 계층 구조에서 방문 하는 현재 페이지 뿐만 아니라 사이트 맵 노드의 "상위 항목"은 루트 (홈, 사이트 맵)까지 모두 표시 됩니다.

![이동 경로는 현재 페이지와 사이트 맵 계층 구조에 있는 상위 항목을 표시 합니다.](master-pages-and-site-navigation-vb/_static/image28.png)

**그림 12**: Breadcrumb은 사이트 맵 계층 구조에서 현재 페이지 및 상위 항목을 표시 합니다.

## <a name="step-5-adding-the-default-page-for-each-section"></a>5 단계: 각 섹션에 대 한 기본 페이지 추가

이 사이트의 자습서는 각 범주에 대 한 폴더와 해당 자습서를 해당 폴더 내 ASP.NET 페이지로 분류 하는 기본 보고, 필터링, 사용자 지정 서식 등의 다양 한 범주로 분류 됩니다. 또한 각 폴더에는 `Default.aspx` 페이지가 포함 되어 있습니다. 이 기본 페이지에는 현재 섹션에 대 한 모든 자습서를 표시 해 보겠습니다. 즉, `BasicReporting` 폴더의 `Default.aspx`에 대해 `SimpleDisplay.aspx`, `DeclarativeParams.aspx`및 `ProgrammaticParams.aspx`에 대 한 링크가 있습니다. 여기서는 `SiteMap` 클래스 및 데이터 웹 컨트롤을 사용 하 여 `Web.sitemap`에 정의 된 사이트 맵을 기반으로이 정보를 표시할 수 있습니다.

반복을 사용 하 여 순서가 지정 되지 않은 목록을 다시 표시 하지만 이번에는 자습서의 제목 및 설명을 표시 합니다. 이를 수행 하기 위한 태그와 코드는 각 `Default.aspx` 페이지에 대해 반복 해야 하므로 [사용자 정의 컨트롤](https://msdn.microsoft.com/library/y6wb1a0e.aspx)에서이 UI 논리를 캡슐화 할 수 있습니다. 웹 사이트에서 `UserControls` 이라는 폴더를 만들고 `SectionLevelTutorialListing.ascx`라는 웹 사용자 정의 컨트롤 형식의 새 항목에 추가 하 고 다음 태그를 추가 합니다.

[Usercontrol 폴더에 새 웹 사용자 정의 컨트롤을 추가 ![](master-pages-and-site-navigation-vb/_static/image30.png)](master-pages-and-site-navigation-vb/_static/image29.png)

**그림 13**: `UserControls` 폴더에 새 웹 사용자 정의 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](master-pages-and-site-navigation-vb/_static/image31.png))

SectionLevelTutorialListing.ascx

[!code-aspx[Main](master-pages-and-site-navigation-vb/samples/sample12.aspx)]

SectionLevelTutorialListing.ascx.vb

[!code-vb[Main](master-pages-and-site-navigation-vb/samples/sample13.vb)]

이전 Repeater 예제에서는 `SiteMap` 데이터를 반복기에 선언적으로 바인딩 했습니다. 그러나 `SectionLevelTutorialListing` 사용자 정의 컨트롤은 프로그래밍 방식으로 수행 됩니다. `Page_Load` 이벤트 처리기에서이 페이지의 URL이 사이트 맵의 노드에 매핑되는지 확인 합니다. 이 사용자 정의 컨트롤을 해당 하는 `<siteMapNode>` 항목이 없는 페이지에서 사용 하는 경우 `SiteMap.CurrentNode`는 `Nothing`을 반환 하 고 데이터는 Repeater에 바인딩되지 않습니다. `CurrentNode`있다고 가정 하 고 `ChildNodes` 컬렉션을 Repeater에 바인딩합니다. 사이트 맵은 각 섹션의 `Default.aspx` 페이지가 해당 섹션에 있는 모든 자습서의 부모 노드인 것으로 설정 되었으므로이 코드는 아래 스크린샷에 표시 된 것 처럼 섹션의 모든 자습서에 대 한 링크 및 설명을 표시 합니다.

이 반복기를 만든 후에는 각 폴더의 `Default.aspx` 페이지를 열고 디자인 뷰으로 이동한 다음, 솔루션 탐색기에서 사용자 정의 컨트롤을 자습서 목록이 표시 될 디자인 화면으로 끌어다 놓기만 하면 됩니다.

[사용자 정의 컨트롤이 default.aspx에 추가 된 ![](master-pages-and-site-navigation-vb/_static/image33.png)](master-pages-and-site-navigation-vb/_static/image32.png)

**그림 14**: `Default.aspx`에 추가 된 사용자 정의 컨트롤 ([전체 크기 이미지를 보려면 클릭](master-pages-and-site-navigation-vb/_static/image34.png))

[![기본 보고 자습서가 나열 됩니다.](master-pages-and-site-navigation-vb/_static/image36.png)](master-pages-and-site-navigation-vb/_static/image35.png)

**그림 15**: 기본 보고 자습서 나열 ([전체 크기 이미지를 보려면 클릭](master-pages-and-site-navigation-vb/_static/image37.png))

## <a name="summary"></a>요약

사이트 맵이 정의 되 고 마스터 페이지가 완료 되 면 데이터 관련 자습서에 대해 일관 된 페이지 레이아웃 및 탐색 구성표가 제공 됩니다. 사이트에 추가 하는 페이지 수에 관계 없이이 정보를 중앙 집중화 하기 때문에 사이트 전체 페이지 레이아웃 또는 사이트 탐색 정보를 업데이트 하는 작업은 빠르고 간단 합니다. 특히 페이지 레이아웃 정보는 마스터 페이지 `Site.master` 및 `Web.sitemap`의 사이트 맵에 정의 됩니다. 이 사이트 전체 페이지 레이아웃 및 탐색 메커니즘을 구현 하기 *위해 코드를* 작성 하지 않아도 되며, Visual Studio에서 전체 WYSIWYG 디자이너 지원을 유지 합니다.

데이터 액세스 계층 및 비즈니스 논리 계층을 완료 하 고 일관 된 페이지 레이아웃 및 사이트 탐색이 정의 되어 있으면 일반적인 보고 패턴을 살펴볼 준비가 되었습니다. 다음 세 가지 자습서에서는 GridView, DetailsView 및 FormView 컨트롤의 BLL에서 검색 된 데이터를 표시 하는 기본 보고 작업에 대해 살펴보겠습니다.

행복 한 프로그래밍

## <a name="further-reading"></a>추가 참고 자료

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 마스터 페이지 개요](https://msdn.microsoft.com/library/wtxbf3hh.aspx)
- [ASP.NET 2.0의 마스터 페이지](http://odetocode.com/Articles/419.aspx)
- [ASP.NET 2.0 디자인 템플릿](https://msdn.microsoft.com/asp.net/reference/design/templates/default.aspx)
- [ASP.NET 사이트 탐색 개요](https://msdn.microsoft.com/library/e468hxky.aspx)
- [ASP.NET 2.0의 사이트 탐색 검사](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [ASP.NET 2.0 사이트 탐색 기능](https://weblogs.asp.net/scottgu/archive/2005/11/20/431019.aspx)
- [ASP.NET 뷰 상태 이해](https://msdn.microsoft.com/library/default.asp?url=/library/dnaspp/html/viewstate.asp)
- [방법: ASP.NET 페이지에 추적 사용](https://msdn.microsoft.com/library/94c55d08%28VS.80%29.aspx)
- [ASP.NET 사용자 정의 컨트롤](https://msdn.microsoft.com/library/y6wb1a0e.aspx)

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서에 대 한 잠재 고객 검토자는 Liz Shulok, Dennis Patterson이 및 Hilton Gid Esenow 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](creating-a-business-logic-layer-vb.md)
