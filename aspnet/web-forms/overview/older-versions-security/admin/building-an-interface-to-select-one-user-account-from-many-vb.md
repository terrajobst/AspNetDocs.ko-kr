---
uid: web-forms/overview/older-versions-security/admin/building-an-interface-to-select-one-user-account-from-many-vb
title: 여러 (VB)에서 하나의 사용자 계정을 선택 하기 위한 인터페이스 빌드 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 필터링 가능한 페이징된 그리드를 사용 하 여 사용자 인터페이스를 작성 합니다. 특히 사용자 인터페이스는 다음에 대 한 일련의 Linkbutton 구성 됩니다.
ms.author: riande
ms.date: 04/01/2008
ms.assetid: da53380c-a16b-41c7-a20d-24343c735c52
msc.legacyurl: /web-forms/overview/older-versions-security/admin/building-an-interface-to-select-one-user-account-from-many-vb
msc.type: authoredcontent
ms.openlocfilehash: 6c711cdaab113d589d9c2535cb1b422de3f38103
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74614910"
---
# <a name="building-an-interface-to-select-one-user-account-from-many-vb"></a>여러 사용자 계정 중 하나를 선택하는 인터페이스 빌드(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/VB.12.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial12_SelectUser_vb.pdf)

> 이 자습서에서는 필터링 가능한 페이징된 그리드를 사용 하 여 사용자 인터페이스를 작성 합니다. 특히 사용자 인터페이스는 사용자 이름의 시작 문자를 기준으로 결과를 필터링 하는 일련의 Linkbutton와 일치 하는 사용자를 표시 하는 GridView 컨트롤로 구성 됩니다. 먼저 GridView의 모든 사용자 계정을 나열 합니다. 그런 다음 3 단계에서 Linkbutton 필터를 추가 합니다. 4 단계에서는 필터링 된 결과의 페이징에 대해 살펴봅니다. 2 ~ 4 단계에서 생성 된 인터페이스는 이후 자습서에서 특정 사용자 계정에 대 한 관리 작업을 수행 하는 데 사용 됩니다.

## <a name="introduction"></a>소개

<a id="_msoanchor_1"> </a> [*사용자에 게 역할 할당*](../roles/assigning-roles-to-users-vb.md) 자습서에서는 관리자가 사용자를 선택 하 고 역할을 관리 하기 위한 기초적인 인터페이스를 만들었습니다. 특히이 인터페이스는 관리자에 게 모든 사용자의 드롭다운 목록을 제공 합니다. 이러한 인터페이스는 수십 개 이상의 사용자 계정이 있지만 수백 또는 수천 개의 계정이 있는 사이트에는 적합 하지 않은 경우에 적합 합니다. 페이지를 필터링 할 수 있는 그리드는 사용자 기반이 많은 웹 사이트에 보다 적합 한 사용자 인터페이스입니다.

이 자습서에서는 이러한 사용자 인터페이스를 빌드합니다. 특히 사용자 인터페이스는 사용자 이름의 시작 문자를 기준으로 결과를 필터링 하는 일련의 Linkbutton와 일치 하는 사용자를 표시 하는 GridView 컨트롤로 구성 됩니다. 먼저 GridView의 모든 사용자 계정을 나열 합니다. 그런 다음 3 단계에서 Linkbutton 필터를 추가 합니다. 4 단계에서는 필터링 된 결과의 페이징에 대해 살펴봅니다. 2 ~ 4 단계에서 생성 된 인터페이스는 이후 자습서에서 특정 사용자 계정에 대 한 관리 작업을 수행 하는 데 사용 됩니다.

시작 하겠습니다.

## <a name="step-1-adding-new-aspnet-pages"></a>1 단계: 새 ASP.NET 페이지 추가

이 자습서 및 다음 두 가지는 다양 한 관리 관련 함수 및 기능을 검토 합니다. 이러한 자습서에서 다루는 항목을 구현 하려면 일련의 ASP.NET 페이지가 필요 합니다. 이러한 페이지를 만들어 사이트 맵을 업데이트 해 보겠습니다.

`Administration`이라는 프로젝트에서 새 폴더를 만들어 시작 합니다. 그런 다음 두 개의 새 ASP.NET 페이지를 폴더에 추가 하 고 각 페이지를 `Site.master` 마스터 페이지에 연결 합니다. 페이지 이름:

- `ManageUsers.aspx`
- `UserInformation.aspx`

또한 웹 사이트의 루트 디렉터리에 두 페이지 (`ChangePassword.aspx` 및 `RecoverPassword.aspx`를 추가 합니다.

이 4 개 페이지에는 마스터 페이지의 ContentPlaceHolders 표시자 각각에 대해 하나씩, `MainContent` 및 `LoginContent`라는 두 개의 콘텐츠 컨트롤이 있습니다.

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample1.aspx)]

이러한 페이지의 `LoginContent` ContentPlaceHolder에 대 한 마스터 페이지의 기본 태그를 표시 하려고 합니다. 따라서 `Content2` 콘텐츠 컨트롤에 대 한 선언적 태그를 제거 합니다. 이렇게 한 후에는 페이지의 태그에 하나의 콘텐츠 컨트롤만 포함 되어야 합니다.

`Administration` 폴더의 ASP.NET 페이지는 관리자 전용입니다. <a id="_msoanchor_2"> </a> [*역할 만들기 및 관리*](../roles/creating-and-managing-roles-vb.md) 자습서에서 시스템에 관리자 역할을 추가 했습니다. 이 역할에 대 한이 두 페이지에 대 한 액세스를 제한 합니다. 이를 수행 하려면 `Administration` 폴더에 `Web.config` 파일을 추가 하 고 Administrators 역할의 사용자를 허용 하 고 다른 모든 항목을 거부 하도록 `<authorization>` 요소를 구성 합니다.

[!code-xml[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample2.xml)]

이 시점에서 프로젝트의 솔루션 탐색기은 그림 1에 표시 된 화면과 비슷해야 합니다.

[새 페이지 4 개와 Web.config 파일이 웹 사이트에 추가 ![](building-an-interface-to-select-one-user-account-from-many-vb/_static/image2.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image1.png)

**그림 1**: 웹 사이트에 4 개의 새 페이지와 `Web.config` 파일이 추가 되었습니다 ([전체 크기 이미지를 보려면 클릭](building-an-interface-to-select-one-user-account-from-many-vb/_static/image3.png)).

마지막으로 `ManageUsers.aspx` 페이지에 항목을 포함 하도록 사이트 맵 (`Web.sitemap`)을 업데이트 합니다. 역할 자습서에 대해 추가한 `<siteMapNode>` 뒤에 다음 XML을 추가 합니다.

[!code-xml[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample3.xml)]

사이트 맵이 업데이트 된 상태에서 브라우저를 통해 사이트를 방문 합니다. 그림 2에 나와 있는 것 처럼 왼쪽의 탐색에는 관리 자습서에 대 한 항목이 포함 되어 있습니다.

[사이트 맵에 사용자 관리 라는 노드가 포함 ![](building-an-interface-to-select-one-user-account-from-many-vb/_static/image5.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image4.png)

**그림 2**: 사용자 관리 라는 노드를 포함 하는 사이트 맵 ([전체 크기 이미지를 보려면 클릭](building-an-interface-to-select-one-user-account-from-many-vb/_static/image6.png))

## <a name="step-2-listing-all-user-accounts-in-a-gridview"></a>2 단계: GridView의 모든 사용자 계정 나열

이 자습서의 최종 목표는 관리자가 관리할 사용자 계정을 선택 하는 데 사용할 수 있는 페이지를 필터링 할 수 있는 그리드를 만드는 것입니다. GridView의 *모든* 사용자를 나열 하는 것부터 시작 하겠습니다. 이 작업이 완료 되 면 필터링 및 페이징 인터페이스 및 기능을 추가 하 게 됩니다.

`Administration` 폴더에서 `ManageUsers.aspx` 페이지를 열고 GridView를 추가 하 여 해당 `ID`를 `UserAccounts`로 설정 하 고 `Membership` 클래스의 `GetAllUsers` 메서드를 사용 하 여 사용자 계정 집합을 GridView에 바인딩하는 코드를 작성 합니다. 이전 자습서에서 설명한 대로 `GetAllUsers` 메서드는 `MembershipUser` 개체의 컬렉션인 `MembershipUserCollection` 개체를 반환 합니다. 컬렉션의 각 `MembershipUser`에는 `UserName`, `Email`, `IsApproved`등의 속성이 포함 됩니다.

GridView에서 원하는 사용자 계정 정보를 표시 하려면 GridView의 `AutoGenerateColumns` 속성을 False로 설정 하 고 `IsApproved`, `IsLockedOut`및 `IsOnline` 속성에 대해 `UserName`, `Email`및 `Comment` 속성 및 CheckBoxFields에 대 한 BoundFields를 추가 합니다. 이 구성은 컨트롤의 선언적 태그나 필드 대화 상자를 통해 적용할 수 있습니다. 그림 3에서는 필드 자동 생성 확인란이 선택 취소 되 고 BoundFields 및 CheckBoxFields가 추가 및 구성 된 후의 필드 대화 상자 스크린샷을 보여 줍니다.

[BoundFields 및 CheckBoxFields 3 개를 GridView에 추가 ![](building-an-interface-to-select-one-user-account-from-many-vb/_static/image8.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image7.png)

**그림 3**: GridView에 세 개의 BoundFields 및 3 개의 CheckBoxFields 추가 ([전체 크기 이미지를 보려면 클릭](building-an-interface-to-select-one-user-account-from-many-vb/_static/image9.png))

GridView를 구성한 후에는 선언 태그가 다음과 유사 해야 합니다.

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample4.aspx)]

다음으로, 사용자 계정을 GridView에 바인딩하는 코드를 작성 해야 합니다. `BindUserAccounts` 라는 메서드를 만들어이 작업을 수행한 다음, 첫 번째 페이지의 `Page_Load` 이벤트 처리기에서이 작업을 호출 합니다.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample5.vb)]

잠시 시간을 내 서 브라우저를 통해 페이지를 테스트 합니다. 그림 4와 같이 `UserAccounts` GridView는 시스템의 모든 사용자에 대 한 사용자 이름, 전자 메일 주소 및 기타 관련 계정 정보를 나열 합니다.

[사용자 계정이 GridView에 나열 ![](building-an-interface-to-select-one-user-account-from-many-vb/_static/image11.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image10.png)

**그림 4**: 사용자 계정은 GridView에 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](building-an-interface-to-select-one-user-account-from-many-vb/_static/image12.png)).

## <a name="step-3-filtering-the-results-by-the-first-letter-of-the-username"></a>3 단계: 사용자 이름의 첫 글자를 기준으로 결과 필터링

현재 `UserAccounts` GridView에는 *모든* 사용자 계정이 표시 됩니다. 수백 또는 수천 개의 사용자 계정을 포함 하는 웹 사이트의 경우 사용자는 표시 된 계정을 신속 하 게 줄이려면 상당한 수 있어야 합니다. 이를 위해서는 필터링 Linkbutton을 페이지에 추가 하면 됩니다. 페이지에 27 개의 Linkbutton를 추가 해 보겠습니다. 하나는 알파벳의 각 문자에 대 한 LinkButton 하나를 포함 합니다. 방문자가 All LinkButton을 클릭 하면 GridView에 모든 사용자가 표시 됩니다. 특정 문자를 클릭 하면 해당 사용자 이름이 선택한 문자로 시작 하는 사용자만 표시 됩니다.

첫 번째 작업은 27 LinkButton 컨트롤을 추가 하는 것입니다. 한 가지 옵션은 한 번에 하나씩 27 Linkbutton을 선언적으로 만드는 것입니다. 좀 더 유연 하 게 사용 하려면 LinkButton를 렌더링 한 다음 필터링 옵션을 `String` 배열로 바인딩하는 `ItemTemplate`을 사용 하 여 Repeater 컨트롤을 사용 하는 것입니다.

`UserAccounts` GridView 위의 페이지에 Repeater 컨트롤을 추가 하 여 시작 합니다. Repeater의 `ID` 속성을 `FilteringUI` 구성 하 여 `ItemTemplate` `Text` 및 `CommandName` 속성이 현재 배열 요소에 바인딩된 LinkButton를 렌더링 하도록 Repeater의 템플릿을 구성 합니다. <a id="_msoanchor_3"> </a> [*사용자에 게 역할 할당*](../roles/assigning-roles-to-users-vb.md) 자습서에서 살펴본 것 처럼 `Container.DataItem` 데이터 바인딩 구문을 사용 하 여이를 수행할 수 있습니다. Repeater의 `SeparatorTemplate` 사용 하 여 각 링크 사이에 세로줄을 표시 합니다.

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample6.aspx)]

이 반복기를 원하는 필터링 옵션으로 채우려면 `BindFilteringUI`라는 메서드를 만듭니다. 첫 번째 페이지 로드 시 `Page_Load` 이벤트 처리기에서이 메서드를 호출 해야 합니다.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample7.vb)]

이 메서드는 배열에 있는 각 요소에 대 한 `String` `filterOptions` 배열의 요소로 필터링 옵션을 지정 합니다. Repeater는 해당 `Text` 및 배열 요소의 값에 할당 된 `CommandName` 속성을 사용 하 여 LinkButton를 렌더링 합니다.

그림 5에는 브라우저를 통해 볼 때 `ManageUsers.aspx` 페이지가 표시 됩니다.

[![리피터 목록 27 필터링 Linkbutton](building-an-interface-to-select-one-user-account-from-many-vb/_static/image14.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image13.png)

**그림 5**: Repeater에 27 필터링 linkbutton 나열 ([전체 크기 이미지를 보려면 클릭](building-an-interface-to-select-one-user-account-from-many-vb/_static/image15.png))

> [!NOTE]
> 사용자 이름은 숫자 및 문장 부호를 포함 하 여 모든 문자로 시작할 수 있습니다. 이러한 계정을 보려면 관리자가 All LinkButton 옵션을 사용 해야 합니다. 또는 숫자로 시작 하는 모든 사용자 계정을 반환 하는 LinkButton를 추가할 수 있습니다. 독자를 위한 연습으로 남겨 둡니다.

필터링 Linkbutton을 클릭 하면 포스트백이 발생 하 고 Repeater의 `ItemCommand` 이벤트가 발생 하지만 결과를 필터링 하는 코드를 아직 작성 하지 않았으므로 표 형태에 변경 내용이 없습니다. `Membership` 클래스에는 사용자 이름이 지정 된 검색 패턴과 일치 하는 사용자 계정을 반환 하는 [`FindUsersByName` 메서드가](https://technet.microsoft.com/library/system.web.security.membership.findusersbyname.aspx) 포함 되어 있습니다. 이 메서드를 사용 하 여 사용자 이름이 클릭 된 필터링 된 LinkButton의 `CommandName`에 지정 된 문자로 시작 하는 사용자 계정만 검색할 수 있습니다.

`ManageUser.aspx` 페이지의 코드 숨김으로 클래스를 업데이트 하 여 시작 합니다 .이 클래스에는 `UsernameToMatch` 라는 속성이 포함 되도록이 속성은 다시 게시 간에 사용자 이름 필터 문자열을 유지 합니다.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample8.vb)]

`UsernameToMatch` 속성은 UsernameToMatch 키를 사용 하 여 `ViewState` 컬렉션에 할당 된 값을 저장 합니다. 이 속성의 값을 읽으면 `ViewState` 컬렉션에 값이 있는지 확인 합니다. 그렇지 않은 경우 기본값 (빈 문자열)을 반환 합니다. `UsernameToMatch` 속성은 일반적인 패턴을 보여 주는 것입니다. 즉, 속성에 대 한 변경 내용이 다시 게시 간에 유지 되도록 값을 뷰 상태에 유지 합니다. 이 패턴에 대 한 자세한 내용은 [ASP.NET View 상태 이해](https://msdn.microsoftn-us/library/ms972976.aspx)를 참조 하세요.

다음으로 `BindUserAccounts` 메서드를 업데이트 하 여 `Membership.GetAllUsers`를 호출 하는 대신 `Membership.FindUsersByName`를 호출 하 고 SQL 와일드 카드 문자%가 추가 된 `UsernameToMatch` 속성의 값을 전달 합니다.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample9.vb)]

사용자 이름이 문자 A로 시작 하는 사용자만 표시 하려면 `UsernameToMatch` 속성을 A로 설정 하 고 `Membership.FindUsersByName("A%")``BindUserAccounts`를 호출 하면 사용자 이름이로 시작 하는 모든 사용자가 반환 됩니다. 마찬가지로, *모든* 사용자를 반환 하려면 `BindUserAccounts` 메서드가 `Membership.FindUsersByName("%")`를 호출 하 여 모든 사용자 계정을 반환 하도록 `UsernameToMatch` 속성에 빈 문자열을 할당 합니다.

Repeater의 `ItemCommand` 이벤트에 대 한 이벤트 처리기를 만듭니다. 이 이벤트는 필터 Linkbutton 중 하나를 클릭할 때마다 발생 합니다. `RepeaterCommandEventArgs` 개체를 통해 클릭 한 LinkButton의 `CommandName` 값이 전달 됩니다. `UsernameToMatch` 속성에 적절 한 값을 할당 한 다음 `BindUserAccounts` 메서드를 호출 해야 합니다. `CommandName` 모두 이면 모든 사용자 계정이 표시 되도록 `UsernameToMatch`에 빈 문자열을 할당 합니다. 그렇지 않으면 `CommandName` 값을 `UsernameToMatch`에 할당 합니다.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample10.vb)]

이 코드가 준비 되 면 필터링 기능을 테스트 합니다. 페이지를 처음 방문 하면 모든 사용자 계정이 표시 됩니다 (그림 5 참조). A LinkButton를 클릭 하면 포스트백이 발생 하 고로 시작 하는 사용자 계정만 표시 하는 결과가 필터링 됩니다.

[Linkbutton 필터링을 사용 하 여 사용자 이름이 특정 문자로 시작 하는 사용자를 표시 ![](building-an-interface-to-select-one-user-account-from-many-vb/_static/image17.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image16.png)

**그림 6**: 필터링 linkbutton를 사용 하 여 사용자 이름이 특정 문자로 시작 하는 사용자 표시 ([전체 크기 이미지를 보려면 클릭](building-an-interface-to-select-one-user-account-from-many-vb/_static/image18.png))

## <a name="step-4-updating-the-gridview-to-use-paging"></a>4 단계: 페이징을 사용 하도록 GridView 업데이트

그림 5와 6에 표시 된 GridView는 `FindUsersByName` 메서드에서 반환 된 모든 레코드를 나열 합니다. 수백 또는 수천 개의 사용자 계정이 있는 경우이로 인해 모든 계정을 볼 때 정보 오버 로드가 발생 하 게 될 수 있습니다 (모든 LinkButton를 클릭 하거나 처음 페이지를 방문 하는 경우와 마찬가지로). 사용자 계정을 관리 하기 쉬운 청크로 표시 하기 위해 한 번에 10 개의 사용자 계정을 표시 하도록 GridView를 구성 하겠습니다.

GridView 컨트롤은 두 가지 유형의 페이징을 제공 합니다.

- **기본 페이징** -쉬운 구현 이지만 비효율적입니다. 간단히 말해서, GridView는 기본 페이징을 사용 하 여 데이터 소스의 *모든* 레코드를 예상 합니다. 그런 다음 해당 레코드 페이지를 표시 합니다.
- **사용자 지정 페이징** -구현 하려면 더 많은 작업이 필요 하지만, 사용자 지정 페이징이 있는 경우 표시할 정확한 레코드 집합만 반환 하기 때문에 기본 페이징 보다 더 효율적입니다.

수천 개의 레코드를 페이징할 때 기본 페이징 및 사용자 지정 페이징의 성능 차이는 상당히 클 수 있습니다. 수백 또는 수천 개의 사용자 계정이 있을 수 있다고 가정 하 여이 인터페이스를 작성 하기 때문에 사용자 지정 페이징을 사용 하겠습니다.

> [!NOTE]
> 사용자 지정 페이징을 구현 하는 것과 관련 된 과제 뿐만 아니라 기본 페이징 및 사용자 지정 페이징 간의 차이점에 대 한 자세한 내용은 [많은 양의 데이터를 효율적으로 페이징](https://asp.net/learn/data-access/tutorial-25-vb.aspx)(영문)을 참조 하세요. 기본 페이징 및 사용자 지정 페이징의 성능 차이에 대 한 몇 가지 분석은 [SQL Server 2005를 사용 하 여 ASP.NET의 사용자 지정 페이징](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)을 참조 하세요.

사용자 지정 페이징을 구현 하려면 먼저 GridView에서 표시 하는 레코드의 정확한 하위 집합을 검색 하는 메커니즘이 필요 합니다. `Membership` 클래스의 `FindUsersByName` 메서드에는 페이지 인덱스와 페이지 크기를 지정 하 고 해당 레코드 범위에 속하는 사용자 계정만 반환 하는 오버 로드가 있습니다.

특히이 오버 로드에는 [`FindUsersByName(usernameToMatch, pageIndex, pageSize, totalRecords)`](https://msdn.microsoft.com/library/fa5st8b2.aspx)시그니처가 있습니다.

*PageIndex* 매개 변수는 반환할 사용자 계정의 페이지를 지정 합니다. *pageSize* 페이지당 표시할 레코드 수를 나타냅니다. *Totalrecords* 매개 변수는 사용자 저장소의 총 사용자 계정 수를 반환 하는 `ByRef` 매개 변수입니다.

> [!NOTE]
> `FindUsersByName`에서 반환 된 데이터는 사용자 이름을 기준으로 정렬 됩니다. 정렬 조건을 사용자 지정할 수 없습니다.

GridView 컨트롤에 바인딩되는 경우에만 사용자 지정 페이징을 사용 하도록 GridView를 구성할 수 있습니다. ObjectDataSource 컨트롤에서 사용자 지정 페이징을 구현 하려면 두 개의 메서드가 필요 합니다. 하나는 시작 행 인덱스 및 표시할 최대 레코드 수에 전달 되 고 해당 범위에 속하는 레코드의 정확한 하위 집합을 반환 합니다. 및은 페이징할 전체 레코드 수를 반환 하는 메서드입니다. `FindUsersByName` 오버 로드는 페이지 인덱스와 페이지 크기를 수락 하 고 `ByRef` 매개 변수를 통해 총 레코드 수를 반환 합니다. 따라서 인터페이스가 일치 하지 않습니다.

한 가지 옵션은 ObjectDataSource에서 필요로 하는 인터페이스를 노출 하는 프록시 클래스를 만든 다음 내부적으로 `FindUsersByName` 메서드를 호출 하는 것입니다. 이 문서에 사용할 수 있는 다른 옵션은 사용자 고유의 페이징 인터페이스를 만들고 GridView의 기본 제공 페이징 인터페이스 대신 사용 하는 것입니다.

### <a name="creating-a-first-previous-next-last-paging-interface"></a>첫 번째, 이전, 다음, 마지막 페이징 인터페이스 만들기

First, Previous, Next 및 Last Linkbutton를 사용 하 여 페이징 인터페이스를 빌드 해 보겠습니다. 첫 번째 LinkButton를 클릭 하면 사용자가 첫 번째 데이터 페이지로 이동 하는 반면 이전에는 이전 페이지로 돌아갑니다. 마찬가지로, Next 및 Last는 각각 사용자를 다음 페이지 및 마지막 페이지로 이동 합니다. `UserAccounts` GridView 아래에 4 개의 LinkButton 컨트롤을 추가 합니다.

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample11.aspx)]

그런 다음 각 LinkButton의 `Click` 이벤트에 대 한 이벤트 처리기를 만듭니다.

그림 7은 Visual Web Developer 디자인 뷰를 통해 볼 때의 네 가지 Linkbutton를 보여 줍니다.

[GridView 아래에 First, Previous, Next 및 Last Linkbutton를 추가 ![](building-an-interface-to-select-one-user-account-from-many-vb/_static/image20.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image19.png)

**그림 7**: GridView 아래에 첫 번째, 이전, 다음 및 마지막 linkbutton 추가 ([전체 크기 이미지를 보려면 클릭](building-an-interface-to-select-one-user-account-from-many-vb/_static/image21.png))

### <a name="keeping-track-of-the-current-page-index"></a>현재 페이지 인덱스 추적

사용자가 `ManageUsers.aspx` 페이지를 처음 방문 하거나 필터링 단추 중 하나를 클릭 하면 GridView에 데이터의 첫 페이지를 표시 하려고 합니다. 그러나 사용자가 탐색 Linkbutton 중 하나를 클릭 하면 페이지 인덱스를 업데이트 해야 합니다. 페이지 인덱스와 페이지당 표시할 레코드 수를 유지 하려면 페이지의 코드 숨김이 클래스에 다음 두 가지 속성을 추가 합니다.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample12.vb)]

`UsernameToMatch` 속성과 마찬가지로 `PageIndex` 속성은 상태를 보기 위해 해당 값을 유지 합니다. 읽기 전용 `PageSize` 속성은 하드 코드 된 값 10을 반환 합니다. 관심 있는 판독기를 초대 하 여 `PageIndex`와 동일한 패턴을 사용 하도록이 속성을 업데이트 한 다음 페이지를 방문 하는 사람이 페이지당 표시할 사용자 계정 수를 지정할 수 있도록 `ManageUsers.aspx` 페이지를 보강 합니다.

### <a name="retrieving-just-the-current-pages-records-updating-the-page-index-and-enabling-and-disabling-the-paging-interface-linkbuttons"></a>현재 페이지의 레코드만 검색 하 고, 페이지 인덱스를 업데이트 하 고, 페이징 인터페이스를 설정 및 해제 하는 방법 Linkbutton

페이징 인터페이스를 사용 하 고 `PageIndex` 및 `PageSize` 속성을 추가 하면 적절 한 `FindUsersByName` 오버 로드를 사용 하도록 `BindUserAccounts` 메서드를 업데이트할 준비가 됩니다. 또한이 메서드가 표시 되는 페이지에 따라 페이징 인터페이스를 사용 하거나 사용 하지 않도록 설정 해야 합니다. 데이터의 첫 페이지를 볼 때 첫 번째 링크와 이전 링크를 사용 하지 않도록 설정 해야 합니다. 마지막 페이지를 볼 때 다음 및 마지막을 사용 하지 않도록 설정 해야 합니다.

`BindUserAccounts` 메서드를 다음 코드로 업데이트합니다.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample13.vb)]

페이징할 수 있는 레코드의 총 수는 `FindUsersByName` 메서드의 마지막 매개 변수에 의해 결정 됩니다. 지정 된 사용자 계정 페이지가 반환 된 후에는 데이터의 첫 페이지 또는 마지막 페이지를 표시 하는지 여부에 따라 4 개의 Linkbutton 사용 하거나 사용 하지 않도록 설정 됩니다.

마지막 단계는 Linkbutton의 네 가지 `Click` 이벤트 처리기에 대 한 코드를 작성 하는 것입니다. 이러한 이벤트 처리기는 `PageIndex` 속성을 업데이트 한 다음, `BindUserAccounts` 호출을 통해 데이터를 GridView에 다시 바인딩해야 합니다 .이 이벤트 처리기는 첫 번째, 이전 및 다음 이벤트 처리기가 매우 간단 합니다. 그러나 마지막 페이지 인덱스를 결정 하기 위해 표시 되는 레코드 수를 결정 해야 하기 때문에 마지막 LinkButton에 대 한 `Click` 이벤트 처리기는 약간 더 복잡 합니다.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample14.vb)]

그림 8 및 9에서는 사용자 지정 페이징 인터페이스의 작동 방식을 보여 줍니다. 그림 8에는 모든 사용자 계정에 대 한 첫 번째 데이터 페이지를 볼 때 `ManageUsers.aspx` 페이지가 표시 됩니다. 13 개의 계정 중 10 개만 표시 됩니다. 다음 또는 마지막 링크를 클릭 하면 포스트백이 발생 하 고 `PageIndex` 1로 업데이트 되며 사용자 계정의 두 번째 페이지를 표에 바인딩합니다 (그림 9 참조).

[![처음 10 개의 사용자 계정이 표시 됩니다.](building-an-interface-to-select-one-user-account-from-many-vb/_static/image23.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image22.png)

**그림 8**: 처음 10 개의 사용자 계정이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](building-an-interface-to-select-one-user-account-from-many-vb/_static/image24.png)).

[![다음 링크를 클릭 하면 사용자 계정의 두 번째 페이지가 표시 됩니다.](building-an-interface-to-select-one-user-account-from-many-vb/_static/image26.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image25.png)

**그림 9**: 다음 링크를 클릭 하면 사용자 계정의 두 번째 페이지가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](building-an-interface-to-select-one-user-account-from-many-vb/_static/image27.png)).

## <a name="summary"></a>요약

관리자는 계정 목록에서 사용자를 선택 해야 하는 경우가 많습니다. 이전 자습서에서는 사용자로 채워진 드롭다운 목록을 사용 하는 방법에 대해 살펴보았습니다. 하지만이 접근 방식은 잘 확장 되지 않습니다. 이 자습서에서는 결과를 페이징된 GridView에 표시 하는 필터링 가능한 인터페이스를 더 나은 방법으로 살펴봅니다. 이 사용자 인터페이스를 사용 하 여 관리자는 수천 개의 사용자 계정을 빠르고 효율적으로 찾고 선택할 수 있습니다.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 정보

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [SQL Server 2005를 사용 하는 ASP.NET의 사용자 지정 페이징](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)
- [대량의 데이터를 효율적으로 페이징](https://asp.net/learn/data-access/tutorial-25-vb.aspx)
- [웹 사이트 관리 도구 롤링](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)

### <a name="about-the-author"></a>작성자 정보

Scott Mitchell는 여러 ASP/ASP. NET books의 작성자와 4GuysFromRolla.com의 창립자가 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 *[24 시간 이내에 ASP.NET 2.0을 sams teach yourself](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 것입니다. Scott은 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) 또는 [http://ScottOnWriting.NET](http://scottonwriting.net/)의 블로그를 통해 연결할 수 있습니다.

### <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Alicja Maziarz입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면 다음 줄을 삭제 합니다.

> [!div class="step-by-step"]
> [이전](unlocking-and-approving-user-accounts-cs.md)
> [다음](recovering-and-changing-passwords-vb.md)
