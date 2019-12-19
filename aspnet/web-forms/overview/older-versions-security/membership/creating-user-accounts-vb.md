---
uid: web-forms/overview/older-versions-security/membership/creating-user-accounts-vb
title: 사용자 계정 만들기 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 SqlMembershipProvider를 통해 멤버 자격 프레임 워크를 사용 하 여 새 사용자 계정을 만드는 방법을 알아봅니다. 새 us를 만드는 방법을 알아봅니다.
ms.author: riande
ms.date: 01/18/2008
ms.assetid: 9ef3e893-bebe-4b13-9fe5-8b71720dd85e
msc.legacyurl: /web-forms/overview/older-versions-security/membership/creating-user-accounts-vb
msc.type: authoredcontent
ms.openlocfilehash: 01be198c329f372ddcd529ad8a369f2d3426a9fc
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74628125"
---
# <a name="creating-user-accounts-vb"></a>사용자 계정 만들기(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_05_VB.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial05_CreatingUsers_vb.pdf)

> 이 자습서에서는 SqlMembershipProvider를 통해 멤버 자격 프레임 워크를 사용 하 여 새 사용자 계정을 만드는 방법을 알아봅니다. 새 사용자를 프로그래밍 방식으로 만들고 ASP를 통해 만드는 방법을 알아봅니다. NET의 기본 제공 CreateUserWizard 컨트롤입니다.

## <a name="introduction"></a>소개

<a id="_msoanchor_1"> </a> [이전 자습서](creating-the-membership-schema-in-sql-server-vb.md) 에서는 데이터베이스에 응용 프로그램 서비스 스키마를 설치 했습니다 .이 스키마는 `SqlMembershipProvider` 및 `SqlRoleProvider`에 필요한 테이블, 뷰 및 저장 프로시저를 추가 했습니다. 그러면이 시리즈의 나머지 자습서에 필요한 인프라가 생성 됩니다. 이 자습서에서는 `SqlMembershipProvider`를 통해 멤버 자격 프레임 워크를 사용 하 여 새 사용자 계정을 만드는 방법을 알아봅니다. 새 사용자를 프로그래밍 방식으로 만들고 ASP를 통해 만드는 방법을 알아봅니다. NET의 기본 제공 CreateUserWizard 컨트롤입니다.

새 사용자 계정을 만드는 방법을 배우는 것 외에도 *<a id="_msoanchor_2"></a>[폼 인증 개요 개요](../introduction/an-overview-of-forms-authentication-vb.md)* 에서 만든 데모 웹 사이트를 업데이트 한 후 *<a id="_msoanchor_3"></a>[폼 인증 구성 및 고급 항목](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md)* 자습서에서 고급을 업데이트 해야 합니다. 데모 웹 응용 프로그램에는 하드 코드 된 사용자 이름/암호 쌍에 대해 사용자 자격 증명의 유효성을 검사 하는 로그인 페이지가 있습니다. 또한 `Global.asax`에는 인증 된 사용자에 대 한 사용자 지정 `IPrincipal` 및 `IIdentity` 개체를 만드는 코드가 포함 되어 있습니다. 로그인 페이지를 업데이트 하 여 멤버 자격 프레임 워크에 대 한 사용자 자격 증명의 유효성을 검사 하 고 사용자 지정 주 및 id 논리를 제거 합니다.

시작 하겠습니다.

## <a name="the-forms-authentication-and-membership-checklist"></a>폼 인증 및 멤버 자격 검사 목록

멤버 자격 프레임 워크에 대 한 작업을 시작 하기 전에이 점에 도달 하기 위해 수행한 중요 한 단계를 검토해 보겠습니다. 폼 기반 인증 시나리오에서 `SqlMembershipProvider`와 함께 멤버 자격 프레임 워크를 사용 하는 경우 웹 응용 프로그램에서 멤버 자격 기능을 구현 하기 전에 다음 단계를 수행 해야 합니다.

1. **폼 기반 인증을 사용 합니다.** *<a id="_msoanchor_4"></a>[폼 인증 개요](../introduction/an-overview-of-forms-authentication-vb.md)* 에 설명 된 대로 `Web.config` 편집 하 고 `<authentication>` 요소의 `mode` 특성을 `Forms`로 설정 하 여 폼 인증을 사용 하도록 설정 합니다. 폼 인증을 사용 하는 경우 각 수신 요청은 *폼 인증 티켓*(있는 경우)을 검사 하 여 요청자를 식별 합니다.
2. **응용 프로그램 서비스 스키마를 적절 한 데이터베이스에 추가 합니다.** `SqlMembershipProvider` 사용 하는 경우 응용 프로그램 서비스 스키마를 데이터베이스에 설치 해야 합니다. 일반적으로이 스키마는 응용 프로그램의 데이터 모델을 보유 하는 동일한 데이터베이스에 추가 됩니다. *<a id="_msoanchor_5"></a>[SQL Server 자습서에서 멤버 자격 스키마 만들기](creating-the-membership-schema-in-sql-server-vb.md)* 에서는 `aspnet_regsql.exe` 도구를 사용 하 여이를 수행 하는 방법을 살펴보았습니다.
3. **2 단계에서 데이터베이스를 참조 하도록 웹 응용 프로그램의 설정을 사용자 지정 합니다.** *SQL Server에서 멤버 자격 스키마 만들기* 자습서에서는 `SqlMembershipProvider` 2 단계에서 선택한 데이터베이스를 사용 하도록 웹 응용 프로그램을 구성 하는 두 가지 방법, 즉 `LocalSqlServer` 연결 문자열 이름을 수정 하는 방법을 보여 주었습니다. 또는 새 등록 된 공급자를 멤버 프레임 워크 공급자 목록에 추가 하 고 2 단계의 데이터베이스를 사용 하도록 새 공급자를 사용자 지정 합니다.

`SqlMembershipProvider` 및 폼 기반 인증을 사용 하는 웹 응용 프로그램을 빌드할 때 `Membership` 클래스 또는 ASP.NET Login 웹 컨트롤을 사용 하기 전에 다음 세 단계를 수행 해야 합니다. 이전 자습서에서 이러한 단계를 이미 수행 했으므로 멤버 프레임 워크 사용을 시작할 준비가 되었습니다.

## <a name="step-1-adding-new-aspnet-pages"></a>1단계: 새 ASP.NET 페이지 추가

이 자습서 및 다음 세 가지는 다양 한 멤버 자격 관련 함수 및 기능을 검사 합니다. 이러한 자습서에서 다루는 항목을 구현 하려면 일련의 ASP.NET 페이지가 필요 합니다. 이러한 페이지를 만든 다음 사이트 맵 파일을 `(Web.sitemap)`합니다.

`Membership`이라는 프로젝트에서 새 폴더를 만들어 시작 합니다. 그런 다음 `Membership` 폴더에 5 개의 새 ASP.NET 페이지를 추가 하 여 각 페이지를 `Site.master` 마스터 페이지에 연결 합니다. 페이지 이름:

- `CreatingUserAccounts.aspx`
- `UserBasedAuthorization.aspx`
- `EnhancedCreateUserWizard.aspx`
- `AdditionalUserInfo.aspx`
- `Guestbook.aspx`

이 시점에서 프로젝트의 솔루션 탐색기은 그림 1에 표시 된 화면과 비슷해야 합니다.

[![멤버 자격 폴더에 5 개의 새 페이지가 추가 되었습니다.](creating-user-accounts-vb/_static/image2.png)](creating-user-accounts-vb/_static/image1.png)

**그림 1**: `Membership` 폴더에 5 개의 새 페이지가 추가 되었습니다 ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-vb/_static/image3.png)).

각 페이지에는 마스터 페이지의 ContentPlaceHolders 표시자 각각에 대해 하나씩, `MainContent` 및 `LoginContent`의 두 콘텐츠 컨트롤이 있습니다.

[!code-aspx[Main](creating-user-accounts-vb/samples/sample1.aspx)]

`LoginContent` ContentPlaceHolder의 기본 태그는 사용자가 인증 되었는지 여부에 따라 사이트에서 로그온 하거나 로그 오프할 수 있는 링크를 표시 합니다. 그러나 `Content2` 콘텐츠 컨트롤이 있으면 마스터 페이지의 기본 태그를 재정의 합니다. *<a id="_msoanchor_6"></a>[폼 인증 자습서 개요](../introduction/an-overview-of-forms-authentication-vb.md)* 에서 설명한 것 처럼이 기능은 왼쪽 열에 로그인 관련 옵션을 표시 하지 않으려는 페이지에서 유용 합니다.

그러나 이러한 다섯 페이지의 경우 `LoginContent` ContentPlaceHolder에 대 한 마스터 페이지의 기본 태그를 표시 하려고 합니다. 따라서 `Content2` 콘텐츠 컨트롤에 대 한 선언적 태그를 제거 합니다. 이렇게 한 후에는 5 페이지의 각 태그에 하나의 콘텐츠 컨트롤만 포함 되어야 합니다.

## <a name="step-2-creating-the-site-map"></a>2단계: 사이트 맵 만들기

가장 간단한 웹 사이트는 일종의 탐색 사용자 인터페이스를 구현 해야 합니다. 탐색 사용자 인터페이스는 사이트의 다양 한 섹션에 대 한 간단한 링크 목록 일 수 있습니다. 또는 이러한 링크를 메뉴 또는 트리 뷰로 정렬할 수 있습니다. 페이지 개발자로 서 탐색 사용자 인터페이스를 만드는 것은 스토리의 절반에 불과합니다. 또한 유지 관리 가능 하 고 업데이트 가능한 방식으로 사이트의 논리 구조를 정의 하는 몇 가지 방법이 필요 합니다. 새 페이지를 추가 하거나 기존 페이지를 제거 하면 단일 원본 (사이트 맵)을 업데이트 하 고 사이트의 탐색 사용자 인터페이스를 통해 해당 수정 내용을 반영할 수 있습니다.

사이트 맵을 정의 하 고 사이트 맵을 기반으로 하는 탐색 사용자 인터페이스를 구현 하는 이러한 두 작업은 사이트 맵 프레임 워크 및 ASP.NET 버전 2.0에 추가 된 탐색 웹 컨트롤 덕분에 쉽게 수행할 수 있습니다. 개발자는 사이트 맵 프레임 워크를 사용 하 여 사이트 맵을 정의한 다음 프로그래밍 API ( [`SiteMap` 클래스](https://msdn.microsoft.com/library/system.web.sitemap.aspx))를 통해 액세스할 수 있습니다. 기본 제공 탐색 웹 컨트롤에는 [메뉴 컨트롤](https://msdn.microsoft.com/library/bz09dy46.aspx), [TreeView 컨트롤](https://msdn.microsoft.com/library/3eafky27.aspx)및 [SiteMapPath 컨트롤이](https://msdn.microsoft.com/library/3eafky27.aspx)포함 됩니다.

멤버 자격 및 역할 프레임 워크와 마찬가지로 사이트 맵 프레임 워크는 [공급자 모델](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)위에 빌드됩니다. 사이트 맵 공급자 클래스의 작업은 XML 파일 또는 데이터베이스 테이블과 같은 영구 데이터 저장소에서 `SiteMap` 클래스에 사용 되는 메모리 내 구조를 생성 하는 것입니다. .NET Framework는 XML 파일 ([`XmlSiteMapProvider`](https://msdn.microsoft.com/library/system.web.xmlsitemapprovider.aspx))에서 사이트 맵 데이터를 읽는 기본 사이트 맵 공급자와 함께 제공 되며,이 공급자는이 자습서에서 사용할 공급자입니다. 일부 대체 사이트 맵 공급자 구현에 대 한 자세한 내용은이 자습서의 끝부분에 있는 추가 판독값 섹션을 참조 하세요.

기본 사이트 맵 공급자는 `Web.sitemap` 이라는 올바른 형식의 XML 파일이 루트 디렉터리에 존재 하는 것으로 예상 합니다. 이 기본 공급자를 사용 하 고 있으므로 이러한 파일을 추가 하 고 적절 한 XML 형식으로 사이트 맵 구조를 정의 해야 합니다. 파일을 추가 하려면 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 새 항목 추가를 선택 합니다. 대화 상자에서 `Web.sitemap`이라는 사이트 맵 형식의 파일을 추가 합니다.

[프로젝트의 루트 디렉터리에 web.sitemap 이라는 파일을 추가 ![](creating-user-accounts-vb/_static/image5.png)](creating-user-accounts-vb/_static/image4.png)

**그림 2**: 프로젝트의 루트 디렉터리에 `Web.sitemap` 이라는 파일 추가 ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-vb/_static/image6.png))

XML 사이트 맵 파일은 웹 사이트의 구조를 계층 구조로 정의 합니다. 이 계층 관계는 `<siteMapNode>` 요소의 상위 구조를 통해 XML 파일에서 모델링 됩니다. `Web.sitemap`는 정확히 하나의 `<siteMapNode>` 자식이 있는 `<siteMap>` 부모 노드로 시작 해야 합니다. 이 최상위 `<siteMapNode>` 요소는 계층의 루트를 나타내며, 임의 개수의 하위 노드가 있을 수 있습니다. 각 `<siteMapNode>` 요소는 `title` 특성을 포함 해야 하며, 선택적으로 `url` 및 `description` 특성을 포함할 수 있습니다. 비어 있지 않은 각 `url` 특성은 고유 해야 합니다.

`Web.sitemap` 파일에 다음 XML을 입력 합니다.

[!code-xml[Main](creating-user-accounts-vb/samples/sample2.xml)]

위의 사이트 맵 태그는 그림 3에 표시 된 계층 구조를 정의 합니다.

[사이트 맵이 계층 구조 탐색 구조를 나타내는 ![](creating-user-accounts-vb/_static/image8.png)](creating-user-accounts-vb/_static/image7.png)

**그림 3**: 사이트 맵은 계층적 탐색 구조를 나타냅니다 ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-vb/_static/image9.png)).

## <a name="step-3-updating-the-master-page-to-include-a-navigational-user-interface"></a>3단계: 탐색 사용자 인터페이스를 포함 하도록 마스터 페이지 업데이트

ASP.NET에는 사용자 인터페이스 디자인을 위한 다양 한 탐색 관련 웹 컨트롤이 포함 되어 있습니다. 여기에는 메뉴, TreeView 및 SiteMapPath 컨트롤이 포함 됩니다. 메뉴와 TreeView 컨트롤은 각각 메뉴 또는 트리의 사이트 맵 구조를 렌더링 하는 반면, SiteMapPath은 방문한 현재 노드와 상위 항목을 보여 주는 이동 경로를 표시 합니다. 사이트 맵 데이터는 SiteMapDataSource을 사용 하 여 다른 데이터 웹 컨트롤에 바인딩할 수 있으며 `SiteMap` 클래스를 통해 프로그래밍 방식으로 액세스할 수 있습니다.

사이트 맵 프레임 워크 및 탐색 컨트롤에 대 한 자세한 설명은이 자습서 시리즈의 범위를 벗어나기 때문에, 자체 탐색 사용자 인터페이스를 작성 하는 데 시간을 할애 하는 대신, *[ASP.NET 2.0 자습서 시리즈의 데이터로 작업](../../data-access/index.md)* 하는 데 사용 된 것을 대신 사용 하 여 그림 4에 표시 된 것 처럼 Repeater 컨트롤을 사용 하 여 2 심층 글머리 기호 목록을 표시 합니다.

### <a name="adding-a-two-level-list-of-links-in-the-left-column"></a>왼쪽 열에 링크의 두 수준 목록 추가

이 인터페이스를 만들려면 다음과 같은 선언 태그를 `Site.master` 마스터 페이지의 왼쪽 열에 추가 합니다. 여기서 텍스트는 다음과 같습니다. 메뉴를 여기로 이동 ... 현재가 있습니다.

[!code-aspx[Main](creating-user-accounts-vb/samples/sample3.aspx)]

위의 태그는 `menu` 이라는 Repeater 컨트롤을 `Web.sitemap`에 정의 된 사이트 맵 계층 구조를 반환 하는 SiteMapDataSource에 바인딩합니다. SiteMapDataSource 컨트롤의 [`ShowStartingNode` 속성이](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sitemapdatasource.showstartingnode.aspx) False로 설정 되어 있으므로 홈 노드의 하위 항목으로 시작 하는 사이트 맵의 계층 구조를 반환 하기 시작 합니다. Repeater는 이러한 각 노드 (현재는 멤버 자격)를 `<li>` 요소에 표시 합니다. 또 다른 내부 리피터는 중첩 된 순서가 지정 되지 않은 목록에 현재 노드의 자식을 표시 합니다.

그림 4에서는 2 단계에서 만든 사이트 맵 구조를 사용 하 여 위의 태그의 렌더링 된 출력을 보여 줍니다. 바닐라는 순서가 지정 되지 않은 목록 태그를 렌더링 합니다. `Styles.css`에 정의 된 css 스타일 시트 규칙은 멋지고-보기 편 레이아웃을 담당 합니다. 위의 마크업이 작동 하는 방식에 대 한 자세한 내용은 [마스터 페이지 및 사이트 탐색](https://asp.net/learn/data-access/tutorial-03-vb.aspx) 자습서를 참조 하세요.

[![탐색 사용자 인터페이스가 중첩 된 순서가 지정 되지 않은 목록을 사용 하 여 렌더링 됩니다.](creating-user-accounts-vb/_static/image11.png)](creating-user-accounts-vb/_static/image10.png)

**그림 4**: 탐색 사용자 인터페이스는 순서가 지정 되지 않은 중첩 된 목록을 사용 하 여 렌더링 됩니다 ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-vb/_static/image12.png)).

### <a name="adding-breadcrumb-navigation"></a>이동 경로 탐색 추가

왼쪽 열에 있는 링크 목록 외에도 각 페이지가 [이동 경로](http://en.wikipedia.org/wiki/Breadcrumb_%28navigation%29)를 표시 하도록 합니다. Breadcrumb은 사이트 계층 구조 내에서 사용자의 현재 위치를 빠르게 보여 주는 탐색 사용자 인터페이스 요소입니다. SiteMapPath 컨트롤은 사이트 맵 프레임 워크를 사용 하 여 사이트 맵에서 현재 페이지의 위치를 확인 한 다음이 정보를 기반으로 하 여 이동 경로를 표시 합니다.

특히 `<span>` 요소를 마스터 페이지의 header `<div>` 요소에 추가 하 고 새 `<span>` 요소의 `class` 특성을 breadcrumb으로 설정 합니다. `Styles.css` 클래스에는 이동 경로 클래스에 대 한 규칙이 포함 되어 있습니다. 다음으로,이 새 `<span>` 요소에 SiteMapPath을 추가 합니다.

[!code-aspx[Main](creating-user-accounts-vb/samples/sample4.aspx)]

그림 5는 `~/Membership/CreatingUserAccounts.aspx`을 방문할 때 SiteMapPath의 출력을 보여 줍니다.

[이동 경로를 ![사이트 맵에 현재 페이지와 해당 상위 항목이 표시 됩니다.](creating-user-accounts-vb/_static/image14.png)](creating-user-accounts-vb/_static/image13.png)

**그림 5**: 이동 경로는 현재 페이지와 해당 상위 항목을 사이트 맵에 표시 합니다 ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-vb/_static/image15.png)).

## <a name="step-4-removing-the-custom-principal-and-identity-logic"></a>4단계: 사용자 지정 보안 주체 및 Id 논리 제거

*<a id="_msoanchor_7"></a>[폼 인증 구성 및 고급 토픽](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md)* 자습서에서는 사용자 지정 principal 및 identity 개체를 인증 된 사용자에 게 연결 하는 방법을 살펴보았습니다. 이를 위해 `FormsAuthenticationModule`에서 사용자를 인증 한 후에 발생 하는 응용 프로그램의 `PostAuthenticateRequest` 이벤트에 대 한 `Global.asax` 이벤트 처리기를 만들어이를 수행 했습니다. 이 이벤트 처리기에서는 `FormsAuthenticationModule`에 의해 추가 된 `GenericPrincipal` 및 `FormsIdentity` 개체를 해당 자습서에서 만든 `CustomPrincipal` 및 `CustomIdentity` 개체와 바꿉니다.

사용자 지정 principal 및 identity 개체는 특정 시나리오에서 유용 하지만 대부분의 경우 `GenericPrincipal` 및 `FormsIdentity` 개체만으로 충분 합니다. 따라서 기본 동작으로 돌아가는 것이 좋을 것입니다. `PostAuthenticateRequest` 이벤트 처리기를 제거 하거나 주석으로 처리 하거나 `Global.asax` 파일을 완전히 삭제 하 여이 변경을 수행 합니다.

> [!NOTE]
> `Global.asax`에서 코드를 주석 처리 하거나 제거한 후에는 `User.Identity` 속성을 `CustomIdentity` 인스턴스로 캐스팅 하는 코드 `Default.aspx's` 코드를 주석으로 처리 해야 합니다.

## <a name="step-5-programmatically-creating-a-new-user"></a>5단계: 프로그래밍 방식으로 새 사용자 만들기

멤버 자격 프레임 워크를 통해 새 사용자 계정을 만들려면 `Membership` 클래스의 [`CreateUser` 메서드](https://msdn.microsoft.com/library/system.web.security.membership.createuser.aspx)를 사용 합니다. 이 메서드에는 사용자 이름, 암호 및 기타 사용자 관련 필드에 대 한 입력 매개 변수가 있습니다. 호출 시, 구성 된 멤버 자격 공급자에 게 새 사용자 계정 만들기를 위임한 다음, 만든 사용자 계정을 나타내는 [`MembershipUser` 개체](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx) 를 반환 합니다.

`CreateUser` 메서드에는 각각 서로 다른 수의 입력 매개 변수를 허용 하는 4 개의 오버 로드가 있습니다.

- [`CreateUser(username, password)`](https://msdn.microsoft.com/library/d8t4h2es.aspx)
- [`CreateUser(username, password, email)`](https://msdn.microsoft.com/library/t8yy6w3h.aspx)
- [`CreateUser(username, password, email, passwordQuestion, passwordAnswer, isApproved, MembershipCreateStatus)`](https://msdn.microsoft.com/library/82xx2e62.aspx)
- [`CreateUser(username, password, email, passwordQuestion, passwordAnswer, isApproved, providerUserKey, MembershipCreateStatus)`](https://msdn.microsoft.com/library/ms152012.aspx)

이러한 4 개의 오버 로드는 수집 되는 정보의 양에 따라 다릅니다. 예를 들어 첫 번째 오버 로드에는 새 사용자 계정에 대 한 사용자 이름 및 암호만 필요 하지만 두 번째 오버 로드에는 사용자의 전자 메일 주소도 필요 합니다.

이러한 오버 로드는 새 사용자 계정을 만드는 데 필요한 정보는 멤버 자격 공급자의 구성 설정에 따라 달라 집니다. *<a id="_msoanchor_8"></a>[SQL Server에서 멤버 자격 스키마 만들기](creating-the-membership-schema-in-sql-server-vb.md)* 자습서에서는 `Web.config`의 멤버 자격 공급자 구성 설정 지정을 검토 했습니다. 표 2에는 구성 설정의 전체 목록이 포함 되어 있습니다.

사용할 수 있는 `CreateUser` 오버 로드에 영향을 주는 멤버 자격 공급자 구성 설정 중 하나는 `requiresQuestionAndAnswer` 설정입니다. `requiresQuestionAndAnswer`이 `true` (기본값)로 설정 된 경우 새 사용자 계정을 만들 때 보안 질문과 대답을 지정 해야 합니다. 이 정보는 사용자가 암호를 재설정 하거나 변경 해야 하는 경우 나중에 사용 됩니다. 특히,이 시점에서 보안 질문을 표시 하 고 암호를 재설정 하거나 변경 하기 위해 올바른 대답을 입력 해야 합니다. 따라서 `requiresQuestionAndAnswer` `true` 설정 된 경우 처음 두 `CreateUser` 오버 로드 중 하나를 호출 하면 보안 질문과 대답이 누락 되기 때문에 예외가 발생 합니다. 응용 프로그램이 현재 보안 질문 및 대답을 요구 하도록 구성 되어 있으므로 사용자를 프로그래밍 방식으로 만들 때 두 개의 오버 로드 중 하나를 사용 해야 합니다.

`CreateUser` 방법을 사용 하 여 설명 하기 위해 사용자에 게 이름, 암호, 전자 메일 및 미리 정의 된 보안 질문에 대 한 답변을 입력 하 라는 메시지를 표시 하는 사용자 인터페이스를 만들어 보겠습니다. `Membership` 폴더에서 `CreatingUserAccounts.aspx` 페이지를 열고 콘텐츠 컨트롤에 다음 웹 컨트롤을 추가 합니다.

- `Username` 이라는 텍스트 상자
- `TextMode` 속성이로 설정 된 `Password`이라는 텍스트 상자입니다 `Password`
- `Email` 이라는 텍스트 상자
- `Text` 속성이 지워진 `SecurityQuestion` 레이블이 지정 된 레이블입니다.
- `SecurityAnswer` 이라는 텍스트 상자
- `Text` 속성이 사용자 계정을 만들도록 설정 된 `CreateAccountButton` 라는 단추
- `Text` 속성이 지워진 `CreateAccountResults` 이라는 레이블 컨트롤

이 시점에서 화면은 그림 6에 표시 된 스크린샷과 유사 하 게 표시 됩니다.

[![다양 한 웹 컨트롤을 만들기 Useraccounts .aspx 페이지에 추가 합니다.](creating-user-accounts-vb/_static/image17.png)](creating-user-accounts-vb/_static/image16.png)

**그림 6**: `CreatingUserAccounts.aspx Page`에 다양 한 웹 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-vb/_static/image18.png))

`SecurityQuestion` 레이블 및 `SecurityAnswer` TextBox는 미리 정의 된 보안 질문을 표시 하 고 사용자의 대답을 수집 하기 위한 것입니다. 보안 질문과 대답은 사용자 단위로 저장 되므로 각 사용자가 자신의 보안 질문을 정의 하도록 허용할 수는 있습니다. 그러나이 예제에서는 다음과 같은 일반적인 보안 질문을 사용 하기로 결정 했습니다. 선호 하는 색은 무엇 인가요?

이 미리 정의 된 보안 질문을 구현 하려면 `passwordQuestion`이라는 페이지의 코드 숨김이 있는 클래스에 상수를 추가 하 여 보안 질문을 할당 합니다. 그런 다음 `Page_Load` 이벤트 처리기에서이 상수를 `SecurityQuestion` 레이블의 `Text` 속성에 할당 합니다.

[!code-vb[Main](creating-user-accounts-vb/samples/sample5.vb)]

다음으로 `CreateAccountButton'` s `Click` 이벤트에 대 한 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-vb[Main](creating-user-accounts-vb/samples/sample6.vb)]

`Click` 이벤트 처리기는 [`MembershipCreateStatus`](https://msdn.microsoft.com/library/system.web.security.membershipcreatestatus.aspx)형식의 `createStatus` 라는 변수를 정의 하 여 시작 합니다. `MembershipCreateStatus`은 `CreateUser` 작업의 상태를 나타내는 열거형입니다. 예를 들어 사용자 계정이 성공적으로 생성 되는 경우 결과 `MembershipCreateStatus` 인스턴스는 `Success;` 값으로 설정 됩니다. 즉, 동일한 사용자 이름을 가진 사용자가 이미 있기 때문에 작업이 실패 하면 `DuplicateUserName`값으로 설정 됩니다. 에서 사용 하는 `CreateUser` 오버 로드에서는 `MembershipCreateStatus` 인스턴스를 메서드에 전달 해야 합니다. 이 매개 변수는 `CreateUser` 메서드 내에서 적절 한 값으로 설정 되며, 메서드 호출 후에 해당 값을 검사 하 여 사용자 계정이 성공적으로 만들어졌는지 여부를 확인할 수 있습니다.

`CreateUser`를 호출한 후 `createStatus`를 전달 하면 `createStatus`에 할당 된 값에 따라 적절 한 메시지를 출력 하는 데 `Select Case` 문이 사용 됩니다. 그림 7은 새 사용자가 성공적으로 만들어진 경우의 출력을 보여 줍니다. 그림 8 및 9는 사용자 계정이 생성 되지 않을 때의 출력을 보여 줍니다. 그림 8에서 방문자는 멤버 자격 공급자의 구성 설정에서 확인 된 암호 강도 요구 사항을 충족 하지 않는 5 자로 된 암호를 입력 했습니다. 그림 9에서 방문자는 기존 사용자 이름 (그림 7에서 만든 사용자 계정)을 사용 하 여 사용자 계정을 만들려고 합니다.

[새 사용자 계정을 성공적으로 만들었습니다 ![](creating-user-accounts-vb/_static/image20.png)](creating-user-accounts-vb/_static/image19.png)

**그림 7**: 새 사용자 계정을 만들었습니다 ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-vb/_static/image21.png)).

[제공 된 암호가 너무 Weak ![사용자 계정이 생성 되지 않음](creating-user-accounts-vb/_static/image23.png)](creating-user-accounts-vb/_static/image22.png)

**그림 8**: 제공 된 암호가 너무 Weak 사용자 계정이 생성 되지 않음 ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-vb/_static/image24.png))

[사용자 이름이 이미 사용 중 이므로 사용자 계정이 생성 되지 ![](creating-user-accounts-vb/_static/image26.png)](creating-user-accounts-vb/_static/image25.png)

**그림 9**: 사용자 이름이 이미 사용 중 이므로 사용자 계정이 생성 되지 않습니다 ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-vb/_static/image27.png)).

> [!NOTE]
> 처음 두 `CreateUser` 메서드 오버 로드 중 하나를 사용할 때 성공 또는 실패를 확인 하는 방법을 궁금할 수 있습니다. 둘 중 하나에 `MembershipCreateStatus`형식의 매개 변수가 없습니다. 이러한 처음 두 오버 로드는 `MembershipCreateStatus`형식의 [`StatusCode` 속성이](https://msdn.microsoft.com/library/system.web.security.membershipcreateuserexception.statuscode.aspx) 포함 된 오류 발생 시 [`MembershipCreateUserException` 예외](https://msdn.microsoft.com/library/system.web.security.membershipcreateuserexception.aspx) 를 throw 합니다.

몇 가지 사용자 계정을 만든 후 `aspnet_Users`의 내용과 `SecurityTutorials.mdf` 데이터베이스의 `aspnet_Membership` 테이블을 나열 하 여 계정이 만들어졌는지 확인 합니다. 그림 10에 표시 된 것 처럼 `CreatingUserAccounts.aspx` 페이지를 통해 두 명의 사용자를 추가 했습니다. Tito 및 Bruce.

멤버 자격 사용자 저장소에 두 명의 사용자가 ![[합니다. Tito 및 Bruce](creating-user-accounts-vb/_static/image29.png)](creating-user-accounts-vb/_static/image28.png)

**그림 10**: 멤버 자격 사용자 저장소에는 두 명의 사용자가 있습니다. Tito 및 Bruce ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-vb/_static/image30.png))

이제 멤버 자격 사용자 저장소에 Bruce와 Tito의 계정 정보가 포함 되어 있지만 Bruce 또는 Tito가 사이트에 로그온 할 수 있도록 하는 기능을 구현 해야 합니다. 현재 `Login.aspx`는 하드 코드 된 사용자 이름/암호 쌍 집합에 대해 사용자 자격 증명의 유효성을 검사 합니다. 즉, 멤버 프레임 워크에 대해 제공 된 자격 증명의 유효성을 검사 *하지* 않습니다. 이제 `aspnet_Users`에 새 사용자 계정이 표시 되 고 `aspnet_Membership` 테이블이 충분 해야 합니다. *<a id="_msoanchor_9"></a>[멤버 자격 사용자 저장소에 대 한 사용자 자격 증명의 유효성을 검사](validating-user-credentials-against-the-membership-user-store-vb.md)* 하는 다음 자습서에서는 멤버 자격 저장소에 대해 유효성을 검사 하도록 로그인 페이지를 업데이트 합니다.

> [!NOTE]
> `SecurityTutorials.mdf` 데이터베이스에 사용자가 표시 되지 않으면 웹 응용 프로그램에서 사용자 저장소로 `ASPNETDB.mdf` 데이터베이스를 사용 하는 기본 멤버 자격 공급자 인 `AspNetSqlMembershipProvider`를 사용 하 고 있기 때문일 수 있습니다. 이것이 문제 인지 확인 하려면 솔루션 탐색기에서 새로 고침 단추를 클릭 합니다. `ASPNETDB.mdf` 라는 데이터베이스가 `App_Data` 폴더에 추가 된 경우이 문제가 발생 합니다. 멤버 자격 공급자를 올바르게 구성 하는 방법에 대 한 지침은 *<a id="_msoanchor_10"></a>[SQL Server에서 멤버 자격 스키마 만들기](creating-the-membership-schema-in-sql-server-vb.md)* 자습서의 4 단계로 돌아갑니다.

대부분의 사용자 계정 만들기 시나리오에서 방문자는 사용자 이름, 암호, 전자 메일 및 기타 필수 정보를 입력할 수 있는 몇 가지 인터페이스가 제공 됩니다 .이 경우에는 새 계정이 만들어집니다. 이 단계에서는 이러한 인터페이스를 직접 빌드하고, `Membership.CreateUser` 메서드를 사용 하 여 사용자의 입력을 기반으로 새 사용자 계정을 프로그래밍 방식으로 추가 하는 방법을 살펴보았습니다. 그러나 코드에서 새 사용자 계정도 만들었습니다. 사용자에 게 사용자가 만든 사용자 계정으로 사이트에 로그인 하거나 사용자에 게 확인 전자 메일을 보내는 등의 추가 작업을 수행 하지 않았습니다. 이러한 추가 단계에는 단추의 `Click` 이벤트 처리기에 추가 코드가 필요 합니다.

ASP.NET는 사용자 계정 만들기 프로세스를 처리 하기 위해 디자인 된 CreateUserWizard 컨트롤과 함께 제공 됩니다 .이 컨트롤은 새 사용자 계정을 만들기 위한 사용자 인터페이스를 렌더링 하 고 멤버 자격 프레임 워크에서 계정을 만들고 사후 계정을 수행 하는 데 사용 됩니다. 확인 전자 메일을 보내고 사이트에 자신을 만든 사용자를 로깅하는 등의 작업을 만듭니다. CreateUserWizard 컨트롤을 사용 하는 것은 CreateUserWizard 컨트롤을 도구 상자에서 페이지로 끈 다음 몇 가지 속성을 설정 하는 것 만큼 간단 합니다. 대부분의 경우 한 줄의 코드를 작성할 필요가 없습니다. 6 단계에서이 유용한 컨트롤을 자세히 살펴보겠습니다.

새 사용자 계정이 일반적인 계정 만들기 웹 페이지를 통해서만 생성 되는 경우 CreateUserWizard 컨트롤이 사용자의 요구를 충족 하기 때문에 `CreateUser` 메서드를 사용 하는 코드를 작성 해야 하는 경우가 거의 없습니다. 그러나 `CreateUser` 방법은 고도로 사용자 지정 된 계정 만들기 사용자 환경이 필요 하거나 대체 인터페이스를 통해 프로그래밍 방식으로 새 사용자 계정을 만들어야 하는 시나리오에서 유용 합니다. 예를 들어 사용자가 다른 응용 프로그램의 사용자 정보를 포함 하는 XML 파일을 업로드할 수 있도록 하는 페이지가 있을 수 있습니다. 페이지는 업로드 된 XML 파일의 내용을 구문 분석 하 고 `CreateUser` 메서드를 호출 하 여 XML에 표시 된 각 사용자에 대해 새 계정을 만들 수 있습니다.

## <a name="step-6-creating-a-new-user-with-the-createuserwizard-control"></a>6단계: CreateUserWizard 컨트롤을 사용 하 여 새 사용자 만들기

ASP.NET는 다양 한 로그인 웹 컨트롤과 함께 제공 됩니다. 이러한 컨트롤은 여러 일반 사용자 계정 및 로그인 관련 시나리오를 지원 합니다. [CreateUserWizard 컨트롤](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/createuserwizard.aspx) 은 멤버 프레임 워크에 새 사용자 계정을 추가 하기 위한 사용자 인터페이스를 제공 하도록 디자인 된 이러한 컨트롤 중 하나입니다.

다른 많은 로그인 관련 웹 컨트롤과 마찬가지로 CreateUserWizard를 사용 하 여 코드를 한 줄도 작성할 필요가 없습니다. 이 메서드는 멤버 자격 공급자의 구성 설정을 기반으로 사용자 인터페이스를 직관적으로 제공 하 고 사용자가 필요한 정보를 입력 하 고 사용자 만들기 단추를 클릭 한 후 `Membership` 클래스의 `CreateUser` 메서드를 내부적으로 호출 합니다. CreateUserWizard 컨트롤은 사용자 지정이 매우 가능 합니다. 계정 만들기 프로세스의 다양 한 단계에서 발생 하는 이벤트의 호스트가 있습니다. 필요에 따라 계정 만들기 워크플로에 사용자 지정 논리를 삽입 하는 이벤트 처리기를 만들 수 있습니다. 또한 CreateUserWizard의 모양은 매우 유연 합니다. 기본 인터페이스의 모양을 정의 하는 여러 속성이 있습니다. 필요한 경우 컨트롤을 템플릿으로 변환 하거나 추가 사용자 등록 단계를 추가할 수 있습니다.

CreateUserWizard 컨트롤의 기본 인터페이스 및 동작을 사용 하는 방법을 살펴보겠습니다. 그런 다음 컨트롤의 속성 및 이벤트를 통해 모양을 사용자 지정 하는 방법을 탐색 합니다.

### <a name="examining-the-createuserwizards-default-interface-and-behavior"></a>CreateUserWizard의 기본 인터페이스 및 동작 검사

`Membership` 폴더의 `CreatingUserAccounts.aspx` 페이지로 돌아가서 디자인 또는 분할 모드로 전환한 다음 페이지 맨 위에 CreateUserWizard 컨트롤을 추가 합니다. CreateUserWizard 컨트롤은 도구 상자의 로그인 컨트롤 섹션 아래에 있습니다. 컨트롤을 추가한 후 `ID` 속성을 `RegisterUser`로 설정 합니다. 그림 11의 스크린샷에 나와 있는 것 처럼 CreateUserWizard는 새 사용자의 사용자 이름, 암호, 전자 메일 주소, 보안 질문 및 답변에 대 한 텍스트 상자를 사용 하 여 인터페이스를 렌더링 합니다.

[![CreateUserWizard 컨트롤은 제네릭 Create User 인터페이스를 렌더링 합니다.](creating-user-accounts-vb/_static/image32.png)](creating-user-accounts-vb/_static/image31.png)

**그림 11**: CreateUserWizard 컨트롤은 일반 Create User 인터페이스를 렌더링 합니다 ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-vb/_static/image33.png)).

CreateUserWizard 컨트롤에 의해 생성 된 기본 사용자 인터페이스를 5 단계에서 만든 인터페이스와 비교해 보겠습니다. 처음에는 CreateUserWizard 컨트롤을 사용 하 여 방문자가 보안 질문과 대답을 모두 지정할 수 있습니다. 반면에, 수동으로 만든 인터페이스는 미리 정의 된 보안 질문을 사용 했습니다. CreateUserWizard 컨트롤의 인터페이스는 유효성 검사 컨트롤도 포함 하 고 있지만 인터페이스의 폼 필드에 대 한 유효성 검사는 아직 구현 하지 않았습니다. 그리고 CreateUserWizard control 인터페이스에는 암호 확인 텍스트 상자 (암호 및 비교 암호 텍스트 상자를 입력 하는 텍스트가 같은지 확인 하는 CompareValidator와 함께)가 포함 되어 있습니다.

흥미로운 점은 CreateUserWizard 컨트롤이 해당 사용자 인터페이스를 렌더링할 때 멤버 자격 공급자의 구성 설정을 확인 하는 것입니다. 예를 들어 보안 질문과 대답 텍스트 상자는 `requiresQuestionAndAnswer`이 True로 설정 된 경우에만 표시 됩니다. 마찬가지로 CreateUserWizard는 암호 강도 요구 사항이 충족 되도록 RegularExpressionValidator 컨트롤을 자동으로 추가 하 고 `minRequiredPasswordLength`, `minRequiredNonalphanumericCharacters`및 `passwordStrengthRegularExpression` 구성 설정에 따라 `ErrorMessage` 및 `ValidationExpression` 속성을 설정 합니다.

CreateUserWizard 컨트롤은 이름에서 알 수 있듯이, [마법사 컨트롤](https://msdn.microsoft.com/library/s2etd1ek.aspx)에서 파생 됩니다. 마법사 컨트롤은 여러 단계 태스크를 완료 하기 위한 인터페이스를 제공 하도록 디자인 되었습니다. 마법사 컨트롤에는 각각 해당 단계의 HTML 및 웹 컨트롤을 정의 하는 템플릿인 `WizardSteps`의 임의 수가 있을 수 있습니다. 마법사 컨트롤은 처음에 첫 번째 `WizardStep`를 표시 하 고, 사용자가 한 단계에서 다음 단계로 진행 하거나 이전 단계로 돌아갈 수 있도록 하는 탐색 컨트롤을 표시 합니다.

그림 11의 선언 태그에 표시 된 대로 CreateUserWizard 컨트롤의 기본 인터페이스에는 두 개의 `WizardStep` s가 포함 됩니다.

- [`CreateUserWizardStep`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizardstep.aspx) ? 새 사용자 계정 만들기에 대 한 정보를 수집 하는 인터페이스를 렌더링 합니다. 그림 11에 표시 된 단계입니다.
- [`CompleteWizardStep`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.completewizardstep.aspx) ? 계정이 성공적으로 만들어졌는지 나타내는 메시지를 렌더링 합니다.

CreateUserWizard의 모양과 동작은 이러한 단계 중 하나를 템플릿으로 변환 하거나 고유한 `WizardStep` s를 추가 하 여 수정할 수 있습니다. *추가 사용자 정보 저장* 자습서에서 등록 인터페이스에 `WizardStep`를 추가 하는 방법을 살펴보겠습니다.

CreateUserWizard 컨트롤이 작동 하는 것을 확인해 보겠습니다. 브라우저를 통해 `CreatingUserAccounts.aspx` 페이지를 방문 하세요. CreateUserWizard의 인터페이스에 일부 잘못 된 값을 입력 하 여 시작 합니다. 암호 강도 요구 사항에 맞지 않는 암호를 입력 하거나 사용자 이름 텍스트 상자를 비워 둡니다. CreateUserWizard는 적절 한 오류 메시지를 표시 합니다. 그림 12에서는 불충분 강력한 암호로 사용자를 만들려고 할 때의 출력을 보여 줍니다.

[CreateUserWizard에서 유효성 검사 컨트롤을 자동으로 삽입 ![](creating-user-accounts-vb/_static/image35.png)](creating-user-accounts-vb/_static/image34.png)

**그림 12**: CreateUserWizard는 자동으로 유효성 검사 컨트롤을 삽입 합니다 ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-vb/_static/image36.png)).

그런 다음 CreateUserWizard에 적절 한 값을 입력 하 고 사용자 만들기 단추를 클릭 합니다. 필수 필드가 입력 되었고 암호의 강도가 충분 하다 고 가정 하면 CreateUserWizard는 멤버 자격 프레임 워크를 통해 새 사용자 계정을 만든 다음 `CompleteWizardStep`인터페이스를 표시 합니다 (그림 13 참조). CreateUserWizard는 내부적으로 5 단계에서 했던 것 처럼 `Membership.CreateUser` 메서드를 호출 합니다.

[![새 사용자 계정을 만들었습니다.](creating-user-accounts-vb/_static/image38.png)](creating-user-accounts-vb/_static/image37.png)

**그림 13**: 새 사용자 계정을 만들었습니다 ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-vb/_static/image39.png)).

> [!NOTE]
> 그림 13에 표시 된 것 처럼 `CompleteWizardStep`의 인터페이스에는 계속 단추가 포함 됩니다. 그러나이 시점에서 클릭 하면 다시 게시를 수행 하 여 방문자를 동일한 페이지에 그대로 둡니다. 속성 섹션을 통해 CreateUserWizard의 모양과 동작을 사용자 지정 하는 경우이 단추를 통해 방문자를 `Default.aspx` (또는 다른 페이지)에 보내는 방법을 살펴봅니다.

새 사용자 계정을 만든 후 Visual Studio로 돌아가서 그림 10과 같이 `aspnet_Users` 및 `aspnet_Membership` 테이블을 검토 하 여 계정이 성공적으로 만들어졌는지 확인 합니다.

### <a name="customizing-the-createuserwizards-behavior-and-appearance-through-its-properties"></a>속성을 통해 CreateUserWizard의 동작 및 모양 사용자 지정

CreateUserWizard는 속성, `WizardStep` s 및 이벤트 처리기를 통해 다양 한 방법으로 사용자 지정할 수 있습니다. 이 섹션에서는 속성을 통해 컨트롤의 모양을 사용자 지정 하는 방법을 살펴보겠습니다. 다음 섹션에서는 이벤트 처리기를 통해 컨트롤의 동작을 확장 하는 방법을 살펴봅니다.

사실상 CreateUserWizard 컨트롤의 기본 사용자 인터페이스에 표시 되는 모든 텍스트는 다양 한의 속성을 통해 사용자 지정할 수 있습니다. 예를 들어 텍스트 상자 왼쪽에 표시 되는 사용자 이름, 암호, 암호 확인, 전자 메일, 보안 질문 및 보안 대답 레이블은 각각 [`UserNameLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.usernamelabeltext.aspx), [`PasswordLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.passwordlabeltext.aspx), [`ConfirmPasswordLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.confirmpasswordlabeltext.aspx), [`EmailLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.emaillabeltext.aspx), [`QuestionLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.questionlabeltext.aspx)및 [`AnswerLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.answerlabeltext.aspx) 속성으로 사용자 지정할 수 있습니다. 마찬가지로 `CreateUserWizardStep` 및 `CompleteWizardStep`에서 사용자 만들기 및 계속 단추에 대 한 텍스트를 지정 하는 속성과 이러한 단추가 단추, Linkbutton 또는 ImageButtons으로 렌더링 되는 경우에도 속성이 있습니다.

색, 테두리, 글꼴 및 기타 시각적 요소는 스타일 속성의 호스트를 통해 구성할 수 있습니다. CreateUserWizard 컨트롤 자체에는 `BackColor`, `BorderStyle`, `CssClass`, `Font`등의 공통 웹 컨트롤 스타일 속성이 있으며, CreateUserWizard 인터페이스의 특정 섹션에 대 한 모양을 정의 하기 위한 다양 한 스타일 속성이 있습니다. 예를 들어 [`TextBoxStyle` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.textboxstyle.aspx)은 `CreateUserWizardStep`의 텍스트 상자에 대 한 스타일을 정의 하는 반면 [`TitleTextStyle` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.titletextstyle.aspx) 은 제목 스타일 (새 계정에 등록)을 정의 합니다.

모양 관련 속성 외에도 CreateUserWizard 컨트롤의 동작에 영향을 주는 다양 한 속성이 있습니다. [`DisplayCancelButton` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.wizard.displaycancelbutton.aspx)을 True로 설정 하면 사용자 만들기 단추 옆에 있는 취소 단추가 표시 됩니다 (기본값은 False 임). 취소 단추를 표시 하는 경우에는 취소를 클릭 한 후 사용자가 전송 되는 페이지를 지정 하는 [`CancelDestinationPageUrl` 속성도](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.continuedestinationpageurl.aspx)설정 해야 합니다. 이전 섹션에서 설명한 것 처럼 `CompleteWizardStep`의 인터페이스에 있는 계속 단추를 누르면 포스트백이 발생 하지만 방문자가 같은 페이지에 남게 됩니다. 계속 단추를 클릭 한 후 방문자를 다른 페이지로 보내려면 [`ContinueDestinationPageUrl` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.continuedestinationpageurl.aspx)에서 URL을 지정 하면 됩니다.

취소 단추를 표시 하 고 취소 또는 계속 단추를 클릭할 때 방문자를 `Default.aspx`으로 보내기 위해 `RegisterUser` CreateUserWizard 컨트롤을 업데이트 해 보겠습니다. 이를 수행 하려면 `DisplayCancelButton` 속성을 True로 설정 하 고 `CancelDestinationPageUrl` 및 `ContinueDestinationPageUrl` 속성을 모두 ~/Default.aspx.로 설정 합니다. 그림 14에서는 브라우저를 통해 볼 때 업데이트 된 CreateUserWizard를 보여 줍니다.

[CreateUserWizardStep에 취소 단추가 포함 된 ![](creating-user-accounts-vb/_static/image41.png)](creating-user-accounts-vb/_static/image40.png)

**그림 14**: `CreateUserWizardStep`에는 취소 단추 ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-vb/_static/image42.png))가 포함 되어 있습니다.

방문자가 사용자 이름, 암호, 전자 메일 주소 및 보안 질문과 대답을 입력 하 고 사용자 만들기를 클릭 하면 새 사용자 계정이 만들어지고 방문자가 새로 만든 사용자로 로그인 됩니다. 페이지를 방문 하는 사람이 자신에 대 한 새 계정을 만드는 것으로 가정 하면이는 원하는 동작이 될 수 있습니다. 그러나 관리자가 새 사용자 계정을 추가 하도록 할 수 있습니다. 이렇게 하면 사용자 계정이 만들어지지만 관리자는 새로 만든 계정이 아닌 관리자 권한으로 로그인 상태로 유지 됩니다. 부울 [`LoginCreatedUser` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.logincreateduser.aspx)을 통해이 동작을 수정할 수 있습니다.

멤버 자격 프레임 워크의 사용자 계정에는 승인 된 플래그가 포함 되어 있습니다. 승인 되지 않은 사용자는 사이트에 로그인 할 수 없습니다. 기본적으로 새로 만든 계정은 승인 됨으로 표시 되어 사용자가 즉시 사이트에 로그인 할 수 있습니다. 그러나 새 사용자 계정을 승인 되지 않음으로 표시 하는 것이 가능 합니다. 사용자가 로그인 하기 전에 관리자가 새 사용자를 수동으로 승인 하려고 할 수 있습니다. 또는 등록 시 입력 한 전자 메일 주소가 유효한 지 확인 한 후에 사용자가 로그온 하도록 허용 하는 것이 좋습니다. 어떤 경우 든 CreateUserWizard 컨트롤의 [`DisableCreatedUser` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.disablecreateduser.aspx) 을 True로 설정 하 여 새로 만든 사용자 계정을 승인 되지 않음으로 표시 하도록 할 수 있습니다 (기본값은 False 임).

메모의 다른 동작 관련 속성에는 `AutoGeneratePassword` 및 `MailDefinition`있습니다. [`AutoGeneratePassword` 속성이](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.autogeneratepassword.aspx) True로 설정 된 경우 `CreateUserWizardStep`는 암호 및 암호 확인 텍스트 상자를 표시 하지 않습니다. 대신, `Membership` 클래스의 [`GeneratePassword` 메서드](https://msdn.microsoft.com/library/system.web.security.membership.generatepassword.aspx)를 사용 하 여 새로 만든 사용자의 암호를 자동으로 생성 합니다. `GeneratePassword` 메서드는 구성 된 암호 강도 요구 사항을 충족 하기 위해 충분 한 수의 영숫자가 아닌 문자를 사용 하 여 지정 된 길이의 암호를 생성 합니다.

[`MailDefinition` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.maildefinition.aspx) 은 계정 만들기 프로세스 중에 지정 된 전자 메일 주소로 전자 메일을 보내려는 경우에 유용 합니다. `MailDefinition` 속성에는 생성 된 전자 메일 메시지에 대 한 정보를 정의 하는 일련의 하위 속성이 포함 되어 있습니다. 이러한 하위 속성은 `Subject`, `Priority`, `IsBodyHtml`, `From`, `CC`, `BodyFileName`등의 옵션을 포함 합니다. [`BodyFileName` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.bodyfilename.aspx) 은 전자 메일 메시지의 본문을 포함 하는 텍스트 또는 HTML 파일을 가리킵니다. 본문은 `<%UserName%>` 및 `<%Password%>`의 미리 정의 된 두 자리 표시자를 지원 합니다. 이러한 자리 표시자 (`BodyFileName` 파일에 있는 경우)는 단순히 생성 된 사용자의 이름과 암호로 바뀝니다.

> [!NOTE]
> `CreateUserWizard` 컨트롤의 `MailDefinition` 속성은 새 계정을 만들 때 전송 되는 전자 메일 메시지에 대 한 세부 정보만 지정 합니다. 전자 메일 메시지를 실제로 전송 하는 방법 (즉, SMTP 서버 또는 메일 드롭 디렉터리 사용, 인증 정보 등)에 대 한 세부 정보는 포함 되지 않습니다. 이러한 하위 수준 세부 정보는 `Web.config`의 `<system.net>` 섹션에서 정의 해야 합니다. 이러한 구성 설정에 대 한 자세한 내용과 일반적인 ASP.NET 2.0에서 전자 메일을 보내는 방법에 대 한 자세한 내용은 [faq의 SystemNetMail.com](http://www.systemnetmail.com/) 및 my 문서, [ASP.NET 2.0에서 전자 메일 보내기](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)를 참조 하세요.

### <a name="extending-the-createuserwizards-behavior-using-event-handlers"></a>이벤트 처리기를 사용 하 여 CreateUserWizard의 동작 확장

CreateUserWizard 컨트롤은 해당 워크플로 중에 많은 이벤트를 발생 시킵니다. 예를 들어 방문자가 사용자 이름, 암호 및 기타 관련 정보를 입력 하 고 사용자 만들기 단추를 클릭 하면 CreateUserWizard 컨트롤은 [`CreatingUser` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.creatinguser.aspx)를 발생 시킵니다. 만들기 프로세스 중에 문제가 발생 하면 [`CreateUserError` 이벤트가](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createusererror.aspx) 발생 합니다. 그러나 사용자가 성공적으로 만들어지면 [`CreatedUser` 이벤트가](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createduser.aspx) 발생 합니다. 추가로 발생 하는 CreateUserWizard 컨트롤 이벤트가 있지만 이러한 이벤트는 가장 germane 세 가지입니다.

특정 시나리오에서는 적절 한 이벤트에 대 한 이벤트 처리기를 만들어 수행할 수 있는 CreateUserWizard 워크플로를 탭 할 수 있습니다. 이를 설명 하기 위해 사용자 이름 및 암호에 대 한 사용자 지정 유효성 검사를 포함 하도록 `RegisterUser` CreateUserWizard 컨트롤을 개선 하겠습니다. 특히 사용자 이름에 선행 또는 후행 공백을 포함할 수 없고 사용자 이름이 암호의 어디에도 표시 되지 않도록 CreateUserWizard을 개선 합니다. 간단히 말해서, 누군가가 "Scott"과 같은 사용자 이름을 만들거나 Scott 및 Scott. 1234와 같은 사용자 이름/암호 조합을 갖지 못하도록 방지 하려고 합니다.

이렇게 하려면 추가 유효성 검사를 수행 하는 `CreatingUser` 이벤트에 대 한 이벤트 처리기를 만듭니다. 제공 된 데이터가 유효 하지 않으면 만들기 프로세스를 취소 해야 합니다. 또한 페이지에 레이블 웹 컨트롤을 추가 하 여 사용자 이름 또는 암호가 잘못 되었음을 설명 하는 메시지를 표시 해야 합니다. 먼저 CreateUserWizard 컨트롤 아래에 Label 컨트롤을 추가 하 고 해당 `ID` 속성을 `InvalidUserNameOrPasswordMessage`로 설정 하 고 `ForeColor` 속성을 `Red`로 설정 합니다. `Text` 속성을 지우고 해당 `EnableViewState` 및 `Visible` 속성을 False로 설정 합니다.

[!code-aspx[Main](creating-user-accounts-vb/samples/sample7.aspx)]

다음으로 CreateUserWizard 컨트롤의 `CreatingUser` 이벤트에 대 한 이벤트 처리기를 만듭니다. 이벤트 처리기를 만들려면 디자이너에서 컨트롤을 선택한 다음 속성 창로 이동 합니다. 여기에서 번개 아이콘을 클릭 한 다음 적절 한 이벤트를 두 번 클릭 하 여 이벤트 처리기를 만듭니다.

다음 코드를 `CreatingUser` 이벤트 처리기에 추가합니다.

[!code-vb[Main](creating-user-accounts-vb/samples/sample8.vb)]

CreateUserWizard 컨트롤에 입력 한 사용자 이름 및 암호는 각각 [`UserName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.username.aspx) 및 [`Password` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.password.aspx)을 통해 사용할 수 있습니다. 위의 이벤트 처리기에서 이러한 속성을 사용 하 여 제공 된 사용자 이름에 선행 또는 후행 공백이 포함 되어 있는지 여부와 사용자 이름을 암호 내에서 찾을 수 있는지 여부를 확인 합니다. 이러한 조건 중 하나를 충족 하는 경우 오류 메시지가 `InvalidUserNameOrPasswordMessage` 레이블에 표시 되 고 이벤트 처리기의 `e.Cancel` 속성이 `True`로 설정 됩니다. `e.Cancel`이 `True`으로 설정 된 경우 CreateUserWizard는 해당 워크플로를 단기 회로 하므로 사용자 계정 생성 프로세스를 효과적으로 취소 합니다.

그림 15에서는 사용자가 선행 공백이 있는 사용자 이름을 입력 하는 경우 `CreatingUserAccounts.aspx`의 스크린샷을 보여 줍니다.

[선행 공백이 나 후행 공백이 있는 ![사용자 이름은 허용 되지 않습니다.](creating-user-accounts-vb/_static/image44.png)](creating-user-accounts-vb/_static/image43.png)

**그림 15**: 선행 또는 후행 공백이 있는 사용자 이름은 허용 되지 않습니다 ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-vb/_static/image45.png)).

> [!NOTE]
> *<a id="_msoanchor_11"></a>[추가 사용자 정보 저장](storing-additional-user-information-vb.md)* 자습서에서 CreateUserWizard 컨트롤의 `CreatedUser` 이벤트를 사용 하는 예제를 확인할 수 있습니다.

## <a name="summary"></a>요약

`Membership` 클래스의 `CreateUser` 메서드는 멤버 자격 프레임 워크에 새 사용자 계정을 만듭니다. 구성 된 멤버 자격 공급자에 대 한 호출을 위임 하 여이를 수행 합니다. `SqlMembershipProvider`경우 `CreateUser` 메서드는 `aspnet_Users` 및 `aspnet_Membership` 데이터베이스 테이블에 레코드를 추가 합니다.

5 단계에서 살펴본 것 처럼 새 사용자 계정을 프로그래밍 방식으로 만들 수 있지만 더 빠르고 쉬운 방법은 CreateUserWizard 컨트롤을 사용 하는 것입니다. 이 컨트롤은 사용자 정보를 수집 하 고 멤버 자격 프레임 워크에서 새 사용자를 만들기 위한 다단계 사용자 인터페이스를 렌더링 합니다. 내부적으로이 컨트롤은 5 단계에서 검사 한 것과 동일한 `Membership.CreateUser` 메서드를 사용 하지만 컨트롤은 사용자 인터페이스, 유효성 검사 컨트롤을 만들고, 코드를 작성 하지 않고도 사용자 계정 만들기 오류에 응답 합니다.

이제 새로운 사용자 계정을 만드는 기능이 준비 되었습니다. 그러나 로그인 페이지는 두 번째 자습서에서 지정한 하드 코드 된 자격 증명에 대해 유효성 검사를 계속 합니다. <a id="_msoanchor_12"> </a> [다음 자습서](validating-user-credentials-against-the-membership-user-store-vb.md) 에서는 멤버 자격 프레임 워크에 대해 사용자가 제공한 자격 증명의 유효성을 검사 하도록 `Login.aspx`를 업데이트 합니다.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 정보

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [`CreateUser` 기술 문서](https://msdn.microsoft.com/library/system.web.security.membershipprovider.createuser.aspx)
- [CreateUserWizard 컨트롤 개요](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/createuserwizard.aspx)
- [파일 시스템 기반 사이트 맵 공급자 만들기](http://aspnet.4guysfromrolla.com/articles/020106-1.aspx)
- [ASP.NET 2.0 마법사 컨트롤을 사용 하 여 단계별 사용자 인터페이스 만들기](http://aspnet.4guysfromrolla.com/articles/061406-1.aspx)
- [ASP.NET 2.0의 사이트 탐색 검사](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [마스터 페이지 및 사이트 탐색](https://asp.net/learn/data-access/tutorial-03-vb.aspx)
- [대기 중인 SQL 사이트 맵 공급자](https://msdn.microsoft.com/msdnmag/issues/06/02/WickedCode/default.aspx)

### <a name="about-the-author"></a>작성자 정보

Scott Mitchell는 여러 ASP/ASP. NET books의 작성자와 4GuysFromRolla.com의 창립자가 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 *[24 시간 이내에 ASP.NET 2.0을 sams teach yourself](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 것입니다. Scott은 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) 또는 [http://ScottOnWriting.NET](http://scottonwriting.net/)의 블로그를 통해 연결할 수 있습니다.

### <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Teresa Murphy입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면 [mitchell@4GuysFromRolla.com](mailto:mitchell@4guysfromrolla.com)에서 줄을 삭제 합니다.

> [!div class="step-by-step"]
> [이전](creating-the-membership-schema-in-sql-server-vb.md)
> [다음](validating-user-credentials-against-the-membership-user-store-vb.md)
