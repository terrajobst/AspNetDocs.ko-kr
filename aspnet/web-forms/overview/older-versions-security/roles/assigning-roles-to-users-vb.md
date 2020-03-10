---
uid: web-forms/overview/older-versions-security/roles/assigning-roles-to-users-vb
title: 사용자에 게 역할 할당 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 사용자가 어떤 역할에 속하는지를 관리 하는 데 도움을 주는 두 개의 ASP.NET 페이지를 빌드합니다. 첫 번째 페이지에는 다음 항목을 확인 하는 기능이 포함 됩니다.
ms.author: riande
ms.date: 03/24/2008
ms.assetid: fd208ee9-69cc-4467-9783-b4e039bdd1d3
msc.legacyurl: /web-forms/overview/older-versions-security/roles/assigning-roles-to-users-vb
msc.type: authoredcontent
ms.openlocfilehash: b53df4494eb0faef7c5e4547c2bf95e5fb071298
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78507281"
---
# <a name="assigning-roles-to-users-vb"></a>사용자에 역할 할당(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/VB.10.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/aspnet_tutorial10_AssigningRoles_vb.pdf)

> 이 자습서에서는 사용자가 어떤 역할에 속하는지를 관리 하는 데 도움을 주는 두 개의 ASP.NET 페이지를 빌드합니다. 첫 번째 페이지에는 지정 된 역할에 속한 사용자, 특정 사용자가 속한 역할 및 특정 역할에서 특정 사용자를 할당 하거나 제거 하는 기능을 확인 하는 기능이 포함 됩니다. 두 번째 페이지에서는 새로 만든 사용자가 속한 역할을 지정 하는 단계가 포함 되도록 CreateUserWizard 컨트롤을 보강 합니다. 이는 관리자가 새 사용자 계정을 만들 수 있는 시나리오에서 유용 합니다.

## <a name="introduction"></a>소개

<a id="_msoanchor_1"> </a> [이전 자습서](creating-and-managing-roles-vb.md) 에서는 역할 프레임 워크 및 `SqlRoleProvider`를 검사 합니다. `Roles` 클래스를 사용 하 여 역할을 만들고, 검색 하 고, 삭제 하는 방법을 살펴보았습니다. 역할을 만들고 삭제 하는 것 외에도 역할에서 사용자를 할당 하거나 제거할 수 있어야 합니다. 아쉽게도 ASP.NET는 사용자가 어떤 역할에 속해 있는지를 관리 하기 위한 웹 컨트롤과 함께 제공 되지 않습니다. 대신, 이러한 연결을 관리 하기 위해 고유한 ASP.NET 페이지를 만들어야 합니다. 좋은 소식은 사용자를 역할에 추가 하 고 제거 하는 것입니다. `Roles` 클래스는 하나 이상의 역할에 하나 이상의 사용자를 추가 하는 여러 메서드를 포함 합니다.

이 자습서에서는 사용자가 어떤 역할에 속하는지를 관리 하는 데 도움을 주는 두 개의 ASP.NET 페이지를 빌드합니다. 첫 번째 페이지에는 지정 된 역할에 속한 사용자, 특정 사용자가 속한 역할 및 특정 역할에서 특정 사용자를 할당 하거나 제거 하는 기능을 확인 하는 기능이 포함 됩니다. 두 번째 페이지에서는 새로 만든 사용자가 속한 역할을 지정 하는 단계가 포함 되도록 CreateUserWizard 컨트롤을 보강 합니다. 이는 관리자가 새 사용자 계정을 만들 수 있는 시나리오에서 유용 합니다.

이제 시작하겠습니다.

## <a name="listing-what-users-belong-to-what-roles"></a>어떤 역할에 속한 사용자 나열

이 자습서의 첫 번째 비즈니스 순서는 사용자를 역할에 할당할 수 있는 웹 페이지를 만드는 것입니다. 사용자를 역할에 할당 하는 방법을 고려 하기 전에 먼저 어떤 역할에 속하는 사용자를 확인 하는 방법을 집중적으로 살펴보겠습니다. 이러한 정보를 표시 하는 방법에는 "role" 또는 "by user"와 같은 두 가지가 있습니다. 방문자가 역할을 선택한 다음 해당 역할에 속하는 모든 사용자를 표시 하거나 ("역할 기준" 표시) 방문자에 게 사용자를 선택 하 고 해당 사용자에 게 할당 된 역할 ("사용자" 표시)을 표시할 수 있습니다.

"역할별" 보기는 방문자가 특정 역할에 속한 사용자 집합을 알고자 하는 경우에 유용 합니다. 방문자가 특정 사용자의 역할을 알고 있어야 하는 경우 "사용자" 보기가 적합 합니다. 페이지에 "역할 기준" 및 "사용자" 인터페이스를 모두 포함 해 보겠습니다.

"사용자" 인터페이스 만들기를 시작 합니다. 이 인터페이스는 드롭다운 목록과 확인란 목록으로 구성 됩니다. 드롭다운 목록은 시스템의 사용자 집합으로 채워집니다. 이 확인란은 역할을 열거 합니다. 드롭다운 목록에서 사용자를 선택 하면 사용자가 속한 역할이 검사 됩니다. 그러면 페이지를 방문 하는 사용자가 확인란을 선택 하거나 선택 취소 하 여 해당 역할에서 선택한 사용자를 추가 하거나 제거할 수 있습니다.

> [!NOTE]
> 사용자 계정을 나열 하기 위해 드롭다운 목록을 사용 하는 것은 수백 명의 사용자 계정이 있는 웹 사이트에 적합 한 선택이 아닙니다. 드롭다운 목록은 사용자가 비교적 짧은 옵션 목록에서 한 항목을 선택할 수 있도록 디자인 되었습니다. 목록 항목 수가 늘어남에 따라 신속 하 게 복잡해 집니다. 잠재적으로 많은 수의 사용자 계정을 포함 하는 웹 사이트를 작성 하는 경우 다른 사용자 인터페이스를 사용 하는 것이 좋습니다. 예를 들어, 방문자에 게 문자를 선택 하 고 해당 문자를 선택 하 라는 메시지를 표시 하는 필터링 가능한 인터페이스 또는 선택한 문자로 시작 하는 사용자 이름이 있는 사용자를 표시 합니다.

## <a name="step-1-building-the-by-user-user-interface"></a>1 단계: "사용자" 사용자 인터페이스 빌드

`UsersAndRoles.aspx` 페이지를 엽니다. 페이지 맨 위에서 `ActionStatus` 이라는 레이블 웹 컨트롤을 추가 하 고 해당 `Text` 속성을 지웁니다. Microsoft는이 레이블을 사용 하 여 수행 된 작업에 대 한 피드백을 제공 하 고, "사용자 Tito를 관리자 역할에 추가 했습니다." 또는 "사용자 Jisun이 감독자 역할에서 제거 되었습니다."와 같은 메시지를 표시 합니다. 이러한 메시지를 출력 하기 위해 레이블의 `CssClass` 속성을 "Important"로 설정 합니다.

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample1.aspx)]

그런 다음 `Styles.css` 스타일 시트에 다음 CSS 클래스 정의를 추가 합니다.

[!code-css[Main](assigning-roles-to-users-vb/samples/sample2.css)]

이 CSS 정의는 긴 빨강 글꼴을 사용 하 여 레이블을 표시 하도록 브라우저에 지시 합니다. 그림 1에서는 Visual Studio 디자이너를 통해 이러한 효과를 보여 줍니다.

[레이블의 CssClass 속성을 ![하면 빨간색 글꼴이 크게 생성 됩니다.](assigning-roles-to-users-vb/_static/image2.png)](assigning-roles-to-users-vb/_static/image1.png)

**그림 1**: 레이블의 `CssClass` 속성으로 인해 큰 빨간색 글꼴이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](assigning-roles-to-users-vb/_static/image3.png)).

그런 다음 페이지에 DropDownList을 추가 하 고, 해당 `ID` 속성을 `UserList`로 설정 하 고, `AutoPostBack` 속성을 True로 설정 합니다. 이 DropDownList을 사용 하 여 시스템의 모든 사용자를 나열 합니다. 이 DropDownList은 MembershipUser 개체의 컬렉션에 바인딩됩니다. DropDownList에서 MembershipUser 개체의 UserName 속성을 표시 하 고이를 목록 항목의 값으로 사용 하려고 하므로 DropDownList의 `DataTextField` 및 `DataValueField` 속성을 "UserName"으로 설정 합니다.

DropDownList 아래에 `UsersRoleList`이라는 리피터를 추가 합니다. 이 리피터는 시스템의 모든 역할을 일련의 확인란으로 나열 합니다. 다음 선언 태그를 사용 하 여 Repeater의 `ItemTemplate`를 정의 합니다.

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample3.aspx)]

`ItemTemplate` 태그는 `RoleCheckBox`라는 단일 CheckBox 웹 컨트롤을 포함 합니다. CheckBox의 `AutoPostBack` 속성은 True로 설정 되 고 `Text` 속성은 `Container.DataItem`에 바인딩됩니다. 데이터 바인딩 구문이 `Container.DataItem` 된 이유는 역할 프레임 워크가 역할 이름 목록을 문자열 배열로 반환 하 고,이 문자열 배열이 Repeater에 바인딩할 수 있기 때문입니다. 이 구문을 사용 하 여 데이터 웹 컨트롤에 바인딩된 배열의 내용을 표시 하는 이유에 대 한 자세한 설명은이 자습서의 범위를 벗어나는 것입니다. 이러한 문제에 대 한 자세한 내용은 [스칼라 배열을 데이터 웹 컨트롤에 바인딩](http://aspnet.4guysfromrolla.com/articles/082504-1.aspx)을 참조 하세요.

이 시점에서 "사용자의" 인터페이스의 선언 태그는 다음과 유사 합니다.

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample4.aspx)]

이제 사용자 계정 집합을 DropDownList에 바인딩하는 코드를 작성 하 고 역할 집합을 리피터에 게 바인딩할 수 있습니다. 페이지의 코드 숨김이 클래스에서 다음 코드를 사용 하 여 `BindUsersToUserList` 라는 메서드와 `BindRolesList`라는 다른를 추가 합니다.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample5.vb)]

`BindUsersToUserList` 메서드는 [`Membership.GetAllUsers` 메서드](https://msdn.microsoft.com/library/dy8swhya.aspx)를 통해 시스템의 모든 사용자 계정을 검색 합니다. 그러면 [`MembershipUser` 인스턴스의](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)컬렉션인 [`MembershipUserCollection` 개체가](https://msdn.microsoft.com/library/system.web.security.membershipusercollection.aspx)반환 됩니다. 그런 다음이 컬렉션은 `UserList` DropDownList에 바인딩됩니다. 컬렉션을 구성을 `MembershipUser` 인스턴스에는 `UserName`, `Email`, `CreationDate`, `IsOnline`등의 다양 한 속성이 포함 되어 있습니다. DropDownList에 `UserName` 속성 값을 표시 하도록 지시 하려면 `UserList` DropDownList의 `DataTextField` 및 `DataValueField` 속성이 "UserName"으로 설정 되어 있는지 확인 합니다.

> [!NOTE]
> `Membership.GetAllUsers` 메서드에는 두 개의 오버 로드가 있습니다. 하나는 입력 매개 변수를 허용 하지 않고 모든 사용자를 반환 하 고, 다른 하나는 페이지 인덱스와 페이지 크기에 대 한 정수 값을 사용 하 고 사용자의 지정 된 하위 집합만 반환 합니다. 페이징할 수 있는 사용자 인터페이스 요소에 많은 양의 사용자 계정이 표시 되는 경우 두 번째 오버 로드를 사용 하 여 모든 것이 아니라 사용자 계정의 정확한 하위 집합만 반환 하기 때문에 사용자를 보다 효율적으로 페이징할 수 있습니다.

`BindRolesToList` 메서드는 시스템의 역할을 포함 하는 문자열 배열을 반환 하는 `Roles` 클래스의 [`GetAllRoles` 메서드](https://msdn.microsoft.com/library/system.web.security.roles.getallroles.aspx)를 호출 하 여 시작 합니다. 그런 다음이 문자열 배열을 Repeater에 바인딩합니다.

마지막으로 페이지가 처음 로드 될 때 이러한 두 메서드를 호출 해야 합니다. 다음 코드를 `Page_Load` 이벤트 처리기에 추가합니다.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample6.vb)]

이 코드를 적용 하면 잠시 브라우저를 통해 페이지를 방문 하세요. 화면은 그림 2와 유사 하 게 표시 됩니다. 모든 사용자 계정이 드롭다운 목록에 채워지며, 그 아래에서 각 역할이 확인란으로 나타납니다. DropDownList 및 확인란의 `AutoPostBack` 속성을 True로 설정 하 여 선택한 사용자를 변경 하거나 역할을 선택 하거나 선택 취소 하면 포스트백이 발생 합니다. 그러나 이러한 작업을 처리 하는 코드를 아직 작성 하지 않았으므로 아무 작업도 수행 되지 않습니다. 다음 두 섹션에서 이러한 작업을 다룰 것입니다.

[페이지 ![사용자 및 역할 표시](assigning-roles-to-users-vb/_static/image5.png)](assigning-roles-to-users-vb/_static/image4.png)

**그림 2**: 사용자 및 역할을 표시 하는 페이지 ([전체 크기 이미지를 보려면 클릭](assigning-roles-to-users-vb/_static/image6.png))

### <a name="checking-the-roles-the-selected-user-belongs-to"></a>선택한 사용자가 속한 역할을 확인 하는 중

페이지가 처음 로드 될 때 또는 방문자가 드롭다운 목록에서 새 사용자를 선택할 때마다 선택한 사용자가 해당 역할에 속하는 경우에만 지정 된 역할 확인란이 선택 되도록 `UsersRoleList`의 확인란을 업데이트 해야 합니다. 이 작업을 수행 하려면 다음 코드를 사용 하 여 `CheckRolesForSelectedUser` 라는 메서드를 만듭니다.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample7.vb)]

위의 코드는 선택한 사용자의 사용자를 확인 하 여 시작 합니다. 그런 다음 Roles 클래스의 [`GetRolesForUser(userName)` 메서드](https://msdn.microsoft.com/library/system.web.security.roles.getrolesforuser.aspx) 를 사용 하 여 지정 된 사용자의 역할 집합을 문자열 배열로 반환 합니다. 다음으로는 Repeater의 항목이 열거 되 고 각 항목의 `RoleCheckBox` CheckBox는 프로그래밍 방식으로 참조 됩니다. 이 확인란은 해당 역할이 해당 하는 역할이 `selectedUsersRoles` 문자열 배열에 포함 되어 있는 경우에만 확인 됩니다.

> [!NOTE]
> ASP.NET 버전 2.0을 사용 하는 경우에는 `Linq.Enumerable.Contains(Of String)(...)` 구문이 컴파일되지 않습니다. `Contains(Of String)` 메서드는 ASP.NET 3.5에 새로 포함 된 [LINQ 라이브러리](http://en.wikipedia.org/wiki/Language_Integrated_Query)의 일부입니다. 여전히 ASP.NET 버전 2.0을 사용 하는 경우 [`Array.IndexOf(Of String)` 메서드](https://msdn.microsoft.com/library/eha9t187.aspx) 를 대신 사용 합니다.

`CheckRolesForSelectedUser` 메서드는 페이지가 처음 로드 될 때와 `UserList` DropDownList의 선택 된 인덱스가 변경 될 때마다 호출 해야 합니다. 따라서 `BindUsersToUserList` 및 `BindRolesToList`를 호출한 후 `Page_Load` 이벤트 처리기에서이 메서드를 호출 합니다. 또한 DropDownList의 `SelectedIndexChanged` 이벤트에 대 한 이벤트 처리기를 만들고 여기에서이 메서드를 호출 합니다.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample8.vb)]

이 코드가 준비 되 면 브라우저를 통해 페이지를 테스트할 수 있습니다. 그러나 `UsersAndRoles.aspx` 페이지에는 현재 역할에 사용자를 할당할 수 있는 권한이 없으므로 사용자에 게 역할이 없습니다. 잠시 후에 역할에 사용자를 할당 하는 인터페이스를 만듭니다. 따라서이 코드가 작동 하는 단어를 사용 하 여 나중에 수행 하는지 확인 하거나, 지금이 기능을 테스트 하기 위해 레코드를 `aspnet_UsersInRoles` 테이블에 삽입 하 여 사용자를 역할에 수동으로 추가할 수 있습니다.

### <a name="assigning-and-removing-users-from-roles"></a>역할에서 사용자 할당 및 제거

방문자가 `UsersRoleList` Repeater의 확인란을 선택 하거나 선택 취소 하는 경우 해당 역할에서 선택한 사용자를 추가 하거나 제거 해야 합니다. CheckBox의 `AutoPostBack` 속성은 현재 True로 설정 되어 있으므로 Repeater의 확인란을 선택 하거나 선택 하지 않을 때마다 포스트백이 발생 합니다. 간단히 말해서 CheckBox의 `CheckChanged` 이벤트에 대 한 이벤트 처리기를 만들어야 합니다. 이 확인란은 Repeater 컨트롤 이므로 이벤트 처리기를 수동으로 추가 해야 합니다. 다음과 같이 이벤트 처리기를 `Protected` 메서드로 코드 숨김으로 추가 하 여 시작 합니다.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample9.vb)]

잠시 후이 이벤트 처리기에 대 한 코드를 작성 하기 위해를 반환 합니다. 하지만 먼저 이벤트 처리를 완료 해 보겠습니다. Repeater의 `ItemTemplate`에 있는 확인란에서 `OnCheckedChanged="RoleCheckBox_CheckChanged"`를 추가 합니다. 이 구문은 `RoleCheckBox`의 `CheckedChanged` 이벤트에 `RoleCheckBox_CheckChanged` 이벤트 처리기를 배선 합니다.

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample10.aspx)]

최종 작업은 `RoleCheckBox_CheckChanged` 이벤트 처리기를 완료 하는 것입니다. 이벤트를 발생 시킨 CheckBox 컨트롤을 참조 하 여 시작 해야 합니다 .이 확인란 인스턴스는 `Text` 및 `Checked` 속성을 통해 확인 되거나 선택 취소 된 역할을 알려 줍니다. 선택한 사용자의 사용자 이름과 함께이 정보를 사용 하 여 `Roles` 클래스의 [`AddUserToRole`](https://msdn.microsoft.com/library/system.web.security.roles.addusertorole.aspx) 또는 [`RemoveUserFromRole` 메서드](https://msdn.microsoft.com/library/system.web.security.roles.removeuserfromrole.aspx)를 통해 역할에서 사용자를 추가 하거나 제거 합니다.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample11.vb)]

위의 코드는 `sender` 입력 매개 변수를 통해 사용할 수 있는 이벤트를 발생 시킨 CheckBox를 프로그래밍 방식으로 참조 하 여 시작 합니다. 확인란을 선택 하면 선택한 사용자가 지정 된 역할에 추가 되 고, 그렇지 않으면 역할에서 제거 됩니다. 두 경우 모두 `ActionStatus` 레이블은 단지 수행한 동작을 요약 하는 메시지를 표시 합니다.

잠시 시간을 사용 하 여 브라우저를 통해이 페이지를 테스트 합니다. 사용자 Tito를 선택 하 고 관리자 및 감독자 역할 모두에 Tito를 추가 합니다.

[![Tito가 Administrators 및 감독자 역할에 추가 되었습니다.](assigning-roles-to-users-vb/_static/image8.png)](assigning-roles-to-users-vb/_static/image7.png)

**그림 3**: 관리자 및 감독자 역할에 Tito를 추가 했습니다 ([전체 크기 이미지를 보려면 클릭](assigning-roles-to-users-vb/_static/image9.png)).

다음으로, 드롭다운 목록에서 사용자 Bruce를 선택 합니다. 포스트백이 발생 하 고 `CheckRolesForSelectedUser`를 통해 Repeater의 확인란이 업데이트 됩니다. Bruce는 아직 어떠한 역할에도 속하지 않으므로 두 확인란을 선택 취소 합니다. 다음으로, 감독자 역할에 Bruce를 추가 합니다.

[![Bruce가 감독자 역할에 추가 되었습니다.](assigning-roles-to-users-vb/_static/image11.png)](assigning-roles-to-users-vb/_static/image10.png)

**그림 4**: Bruce가 감독자 역할에 추가 됨 ([전체 크기 이미지를 보려면 클릭](assigning-roles-to-users-vb/_static/image12.png))

`CheckRolesForSelectedUser` 메서드의 기능을 자세히 확인 하려면 Tito 또는 Bruce 이외의 사용자를 선택 합니다. 확인란을 선택 취소 하 여 어떤 역할에도 속하지 않는 것을 확인 합니다. Tito로 돌아갑니다. 관리자와 감독자 확인란을 모두 선택 해야 합니다.

## <a name="step-2-building-the-by-roles-user-interface"></a>2 단계: "역할 별" 사용자 인터페이스 빌드

이 시점에서 "사용자" 인터페이스를 완료 하 고 "주요 당면" 인터페이스를 시작할 준비가 되었습니다. "역할별" 인터페이스는 드롭다운 목록에서 역할을 선택 하 라는 메시지를 표시 한 다음 GridView에서 해당 역할에 속하는 사용자 집합을 표시 합니다.

다른 DropDownList 컨트롤을 `UsersAndRoles.aspx page`에 추가 합니다. Repeater 컨트롤 아래에이를 놓고 `RoleList`이름을로 지정 하 고 `AutoPostBack` 속성을 True로 설정 합니다. 그 아래에서 GridView를 추가 하 고 이름을 `RolesUserList`로 합니다. 이 GridView에는 선택한 역할에 속하는 사용자가 나열 됩니다. GridView의 `AutoGenerateColumns` 속성을 False로 설정 하 고, 표의 `Columns` 컬렉션에 Templatefield로 변환를 추가 하 고, `HeaderText` 속성을 "사용자"로 설정 합니다. Templatefield로 변환의 `ItemTemplate`를 정의 하 여 `UserNameLabel`이라는 레이블의 `Text` 속성에 `Container.DataItem` 데이터 바인딩 식의 값을 표시 합니다.

GridView를 추가 하 고 구성한 후에는 "역할별" 인터페이스의 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample12.aspx)]

`RoleList` DropDownList을 시스템의 역할 집합과 채워야 합니다. 이를 수행 하려면가 `Roles.GetAllRoles` 메서드에서 반환 하는 문자열 배열을 `RolesList` DropDownList (및 `UsersRoleList` Repeater)에 바인딩되도록 `BindRolesToList` 메서드를 업데이트 합니다.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample13.vb)]

`RoleList` DropDownList 컨트롤에 역할 집합을 바인딩하기 위해 `BindRolesToList` 메서드의 마지막 두 줄이 추가 되었습니다. 그림 5는 브라우저를 통해 볼 때 최종 결과를 보여 줍니다 .이는 시스템 역할로 채워진 드롭다운 목록입니다.

[역할이 RoleList DropDownList에 표시 ![](assigning-roles-to-users-vb/_static/image14.png)](assigning-roles-to-users-vb/_static/image13.png)

**그림 5**: `RoleList` DropDownList에 표시 되는 역할 ([전체 크기 이미지를 보려면 클릭](assigning-roles-to-users-vb/_static/image15.png))

### <a name="displaying-the-users-that-belong-to-the-selected-role"></a>선택한 역할에 속한 사용자 표시

페이지를 처음 로드 하거나 `RoleList` DropDownList에서 새 역할을 선택 하는 경우 GridView에서 해당 역할에 속하는 사용자 목록을 표시 해야 합니다. 다음 코드를 사용 하 여 `DisplayUsersBelongingToRole` 라는 메서드를 만듭니다.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample14.vb)]

이 메서드는 `RoleList` DropDownList에서 선택한 역할을 가져와 시작 합니다. 그런 다음 [`Roles.GetUsersInRole(roleName)` 메서드](https://msdn.microsoft.com/library/system.web.security.roles.getusersinrole.aspx) 를 사용 하 여 해당 역할에 속한 사용자 이름의 문자열 배열을 검색 합니다. 그런 다음이 배열은 `RolesUserList` GridView에 바인딩됩니다.

이 메서드는 페이지가 처음 로드 될 때와 `RoleList` DropDownList에서 선택 된 역할이 변경 될 때 두 가지 상황에서 호출 해야 합니다. 따라서 `CheckRolesForSelectedUser`를 호출한 후이 메서드가 호출 되도록 `Page_Load` 이벤트 처리기를 업데이트 합니다. 그런 다음 `RoleList`의 `SelectedIndexChanged` 이벤트에 대 한 이벤트 처리기를 만들고 여기에서이 메서드를 호출 합니다.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample15.vb)]

이 코드를 사용 하면 `RolesUserList` GridView에서 선택한 역할에 속하는 사용자를 표시 해야 합니다. 그림 6에서 볼 수 있듯이, 감독자 역할은 Bruce와 Tito의 두 멤버로 구성 됩니다.

[GridView ![선택한 역할에 속하는 사용자를 나열 합니다.](assigning-roles-to-users-vb/_static/image17.png)](assigning-roles-to-users-vb/_static/image16.png)

**그림 6**: GridView에 선택한 역할에 속하는 사용자 나열 ([전체 크기 이미지를 보려면 클릭](assigning-roles-to-users-vb/_static/image18.png))

### <a name="removing-users-from-the-selected-role"></a>선택한 역할에서 사용자 제거

"제거" 단추 열을 포함 하도록 `RolesUserList` GridView를 늘려 보겠습니다. 특정 사용자에 대 한 "제거" 단추를 클릭 하면 해당 역할에서 해당 사용자가 제거 됩니다.

먼저 GridView에 삭제 단추 필드를 추가 합니다. 이 필드가 가장 왼쪽에 표시 되도록 하 고 해당 `DeleteText` 속성을 "Delete" (기본값)에서 "Remove"로 변경 합니다.

[![추가 합니다.](assigning-roles-to-users-vb/_static/image20.png)](assigning-roles-to-users-vb/_static/image19.png)

**그림 7**: "제거" 단추를 GridView에 추가 ([전체 크기 이미지를 보려면 클릭](assigning-roles-to-users-vb/_static/image21.png))

"제거" 단추를 클릭 하면 ensues이 다시 게시 되 고 GridView의 `RowDeleting` 이벤트가 발생 합니다. 이 이벤트에 대 한 이벤트 처리기를 만들고 선택한 역할에서 사용자를 제거 하는 코드를 작성 해야 합니다. 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample16.vb)]

선택한 역할 이름을 확인 하 여 코드를 시작 합니다. 그런 다음 제거할 사용자의 사용자 이름을 결정 하기 위해 "제거" 단추를 클릭 한 행의 `UserNameLabel` 컨트롤을 프로그래밍 방식으로 참조 합니다. 그런 다음 `Roles.RemoveUserFromRole` 메서드에 대 한 호출을 통해 사용자를 역할에서 제거 합니다. 그러면 `RolesUserList` GridView가 새로 고쳐지고 `ActionStatus` 레이블 컨트롤을 통해 메시지가 표시 됩니다.

> [!NOTE]
> "제거" 단추는 역할에서 사용자를 제거 하기 전에 사용자가 어떤 종류의 확인도 필요 하지 않습니다. 사용자를 초대 하 여 일정 수준의 사용자 확인을 추가 합니다. 동작을 확인 하는 가장 쉬운 방법 중 하나는 클라이언트 쪽 확인 대화 상자를 통하는 것입니다. 이 기술에 대 한 자세한 내용은 [삭제할 때 클라이언트 쪽 확인 추가](https://asp.net/learn/data-access/tutorial-42-vb.aspx)를 참조 하세요.

그림 8에서는 사용자 Tito가 감독자 그룹에서 제거 된 후의 페이지를 보여 줍니다.

[![하는 경우 Tito는 더 이상 감독자가 아닙니다.](assigning-roles-to-users-vb/_static/image23.png)](assigning-roles-to-users-vb/_static/image22.png)

**그림 8**: Tito는 더 이상 감독자가 아닙니다 ([전체 크기 이미지를 보려면 클릭](assigning-roles-to-users-vb/_static/image24.png)).

### <a name="adding-new-users-to-the-selected-role"></a>선택한 역할에 새 사용자 추가

선택한 역할에서 사용자를 제거 하는 것과 함께이 페이지의 방문자는 선택한 역할에 사용자를 추가할 수도 있습니다. 선택한 역할에 사용자를 추가 하는 가장 좋은 인터페이스는 필요한 사용자 계정 수에 따라 달라 집니다. 웹 사이트가 수십 개의 사용자 계정에만 있는 경우 여기에서 DropDownList를 사용할 수 있습니다. 수천 개의 사용자 계정이 있을 수 있는 경우 방문자가 계정을 통해 페이지를 이동 하거나 특정 계정을 검색 하거나 다른 방식으로 사용자 계정을 필터링 할 수 있도록 하는 사용자 인터페이스를 포함 하는 것이 좋습니다.

이 페이지에서는 시스템의 사용자 계정 수에 관계 없이 작동 하는 매우 간단한 인터페이스를 사용 하겠습니다. 즉, 텍스트 상자를 사용 하 여 방문자에 게 선택한 역할에 추가 하려는 사용자의 사용자 이름을 입력 하 라는 메시지를 표시 합니다. 해당 이름을 가진 사용자가 없거나 사용자가 이미 역할의 구성원 인 경우 `ActionStatus` 레이블에 메시지를 표시 합니다. 그러나 사용자가 존재 하 고 역할의 멤버가 아닌 경우 해당 사용자를 역할에 추가 하 고 그리드를 새로 고칩니다.

텍스트 상자와 단추를 GridView 아래에 추가 합니다. 텍스트 상자의 `ID`를 `UserNameToAddToRole` 설정 하 고 단추의 `ID` 및 `Text` 속성을 각각 `AddUserToRoleButton` 및 "역할에 사용자 추가"로 설정 합니다.

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample17.aspx)]

다음으로 `AddUserToRoleButton`에 대 한 `Click` 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample18.vb)]

`Click` 이벤트 처리기에서 대부분의 코드는 다양 한 유효성 검사를 수행 합니다. 이를 통해 방문자는 `UserNameToAddToRole` 텍스트 상자에 사용자 이름을 제공 하 고, 사용자가 시스템에 존재 하며, 선택 된 역할에 속해 있지 않은지 확인할 수 있습니다. 이러한 검사 중 하나라도 실패 하면 `ActionStatus`에 적절 한 메시지가 표시 되 고 이벤트 처리기가 종료 됩니다. 모든 검사가 통과 되 면 사용자는 `Roles.AddUserToRole` 메서드를 통해 역할에 추가 됩니다. 그러면 텍스트 상자의 `Text` 속성이 지워지고 GridView가 새로 고쳐지고 `ActionStatus` 레이블에 지정 된 사용자가 선택한 역할에 성공적으로 추가 되었음을 나타내는 메시지가 표시 됩니다.

> [!NOTE]
> 지정 된 사용자가 선택 된 역할에 아직 속해 있지 않은지 확인 하려면 [`Roles.IsUserInRole(userName, roleName)` 메서드](https://msdn.microsoft.com/library/system.web.security.roles.isuserinrole.aspx)를 사용 합니다 .이 메서드는 *사용자 이름이* *roleName*의 멤버 인지 여부를 나타내는 부울 값을 반환 합니다. 역할 기반 권한 부여를 살펴볼 때 <a id="_msoanchor_2"> </a> [다음 자습서](role-based-authorization-vb.md) 에서이 방법을 다시 사용 합니다.

브라우저를 통해 페이지를 방문 하 고 `RoleList` DropDownList에서 감독자 역할을 선택 합니다. 잘못 된 사용자 이름을 입력 해 보세요. 사용자가 시스템에 존재 하지 않는다는 메시지가 표시 됩니다.

[![존재 하지 않는 사용자를 역할에 추가할 수 없습니다.](assigning-roles-to-users-vb/_static/image26.png)](assigning-roles-to-users-vb/_static/image25.png)

**그림 9**: 존재 하지 않는 사용자를 역할에 추가할 수 없음 ([전체 크기 이미지를 보려면 클릭](assigning-roles-to-users-vb/_static/image27.png))

이제 유효한 사용자를 추가 해 보세요. 계속 해 서 Tito를 감독자 역할에 다시 추가 합니다.

[![Tito가 감독자에 게 한 번입니다.](assigning-roles-to-users-vb/_static/image29.png)](assigning-roles-to-users-vb/_static/image28.png)

**그림 10**: 감독자에 게 한 번  ([전체 크기 이미지를 보려면 클릭](assigning-roles-to-users-vb/_static/image30.png))

## <a name="step-3-cross-updating-the-by-user-and-by-role-interfaces"></a>3 단계: "사용자" 및 "역할 기준" 인터페이스를 교차 업데이트

`UsersAndRoles.aspx` 페이지는 사용자 및 역할을 관리 하기 위한 두 가지 고유한 인터페이스를 제공 합니다. 현재이 두 인터페이스는 서로 독립적으로 작동 하므로 한 인터페이스에서 변경한 내용이 다른 인터페이스에 즉시 반영 되지 않을 수 있습니다. 예를 들어 페이지 방문자가 Bruce 및 Tito를 멤버로 나열 하는 `RoleList` DropDownList에서 감독자 역할을 선택 한다고 가정 합니다. 그런 다음 방문자는 `UserList` DropDownList에서 Tito를 선택 하 여 `UsersRoleList` Repeater의 관리자 및 감독자 확인란을 확인 합니다. 그러면 방문자가 Repeater에서 감독자 역할을 편집 하는 경우 Tito가 감독자 역할에서 제거 되지만이 수정 사항은 "역할" 인터페이스에 반영 되지 않습니다. GridView는 여전히 감독자 역할의 멤버가 되는 것으로 표시 합니다.

이 문제를 해결 하려면 `UsersRoleList` 리피터에서 역할을 선택 하거나 선택 취소할 때마다 GridView를 새로 고쳐야 합니다. 마찬가지로 사용자가 "role" 인터페이스에서 역할에 추가 되거나 제거 될 때마다 Repeater를 새로 고쳐야 합니다.

"사용자" 인터페이스의 Repeater는 `CheckRolesForSelectedUser` 메서드를 호출 하 여 새로 고쳐집니다. "Role" 인터페이스는 `RolesUserList` GridView의 `RowDeleting` 이벤트 처리기 및 `AddUserToRoleButton` 단추의 `Click` 이벤트 처리기에서 수정할 수 있습니다. 따라서 이러한 각 메서드에서 `CheckRolesForSelectedUser` 메서드를 호출 해야 합니다.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample19.vb)]

마찬가지로, "role" 인터페이스의 GridView는 `DisplayUsersBelongingToRole` 메서드를 호출 하 여 새로 고쳐지고 "사용자" 인터페이스는 `RoleCheckBox_CheckChanged` 이벤트 처리기를 통해 수정 됩니다. 따라서이 이벤트 처리기에서 `DisplayUsersBelongingToRole` 메서드를 호출 해야 합니다.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample20.vb)]

이러한 사소한 코드를 변경 하면 "사용자 기준" 및 "역할 기준" 인터페이스가 이제 올바르게 교차 업데이트 됩니다. 이를 확인 하려면 브라우저를 통해 페이지를 방문 하 고 `UserList`에서 Tito 및 감독자를 선택 하 고 `RoleList` Dropdownlist를 각각 선택 합니다. "사용자" 인터페이스의 Repeater에서 Tito에 대 한 감독자 역할을 선택 취소 하면 Tito는 "role" 인터페이스의 GridView에서 자동으로 제거 됩니다. "Role" 인터페이스에서 감독자 역할에 Tito를 추가 하면 "사용자" 인터페이스에서 감독자 확인란을 자동으로 다시 검사 합니다.

## <a name="step-4-customizing-the-createuserwizard-to-include-a-specify-roles-step"></a>4 단계: "역할 지정" 단계를 포함 하도록 CreateUserWizard 사용자 지정

<a id="_msoanchor_3"> </a> [*사용자 계정 만들기*](../membership/creating-user-accounts-vb.md) 자습서에서 CreateUserWizard 웹 컨트롤을 사용 하 여 새 사용자 계정을 만들기 위한 인터페이스를 제공 하는 방법을 살펴보았습니다. CreateUserWizard 컨트롤은 다음 두 가지 방법 중 하나로 사용할 수 있습니다.

- 방문자가 사이트에서 자신의 고유한 사용자 계정을 만드는 방법으로
- 관리자가 새 계정을 만들 수 있도록 하는 방법

첫 번째 사용 사례에서 방문자가 사이트에 제공 하 고 CreateUserWizard를 입력 하 여 사이트에 등록 하기 위해 정보를 입력 합니다. 두 번째 경우 관리자가 다른 사용자에 대 한 새 계정을 만듭니다.

관리자가 다른 사용자를 위해 계정을 만들 경우 관리자가 새 사용자 계정이 속한 역할을 지정할 수 있도록 하는 것이 유용할 수 있습니다. <a id="_msoanchor_4"> </a> [ *추가 사용자 정보* 저장](../membership/storing-additional-user-information-vb.md) 자습서에서 추가 `WizardSteps`를 추가 하 여 CreateUserWizard를 사용자 지정 하는 방법을 살펴보았습니다. 새 사용자의 역할을 지정 하기 위해 CreateUserWizard에 추가 단계를 추가 하는 방법을 살펴보겠습니다.

`CreateUserWizardWithRoles.aspx` 페이지를 열고 이름이 `RegisterUserWithRoles`인 CreateUserWizard 컨트롤을 추가 합니다. 컨트롤의 `ContinueDestinationPageUrl` 속성을 "~/Default.aspx"로 설정 합니다. 여기서는 관리자가이 CreateUserWizard 컨트롤을 사용 하 여 새 사용자 계정을 만드는 것 이므로 컨트롤의 `LoginCreatedUser` 속성을 False로 설정 합니다. 이 `LoginCreatedUser` 속성은 방문자가 자신에 게 생성 된 사용자로 자동으로 로그온 하는지 여부를 지정 하며 기본값은 True입니다. 관리자가 새 계정을 만들 때 자기 자신에 게 로그인 된 상태를 유지 하려는 경우에는이 설정을 False로 설정 합니다.

다음으로 "`WizardSteps`추가/제거 ..."를 선택 합니다. CreateUserWizard의 스마트 태그에서 옵션을 선택 하 고 새 `WizardStep`을 추가 하 여 `ID`을 `SpecifyRolesStep`로 설정 합니다. "새 계정에 등록" 단계를 수행 하 고 "완료" 단계 전에 `SpecifyRolesStep WizardStep` 이동 합니다. `WizardStep`의 `Title` 속성을 "역할 지정"으로 설정 하 고 `StepType` 속성을 `Step`로 설정 하 고 해당 `AllowReturn` 속성을 False로 설정 합니다.

[![추가 합니다.](assigning-roles-to-users-vb/_static/image32.png)](assigning-roles-to-users-vb/_static/image31.png)

**그림 11**: CreateUserWizard에 "역할 지정" `WizardStep` 추가 ([전체 크기 이미지를 보려면 클릭](assigning-roles-to-users-vb/_static/image33.png))

이렇게 변경 하면 CreateUserWizard의 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample21.aspx)]

"역할 지정" `WizardStep``RoleList.` 라는 CheckBoxList를 추가 합니다 .이 CheckBoxList는 사용 가능한 역할을 나열 하 여 페이지를 방문 하는 사용자가 새로 만든 사용자가 속한 역할을 확인할 수 있도록 합니다.

두 가지 코딩 작업이 있습니다. 먼저 `RoleList` CheckBoxList를 시스템의 역할로 채워야 합니다. 두 번째로, 사용자가 "역할 지정" 단계에서 "완료" 단계로 이동할 때 만든 사용자를 선택한 역할에 추가 해야 합니다. `Page_Load` 이벤트 처리기에서 첫 번째 작업을 수행할 수 있습니다. 다음 코드에서는 페이지에 대 한 첫 번째 방문에서 `RoleList` CheckBox를 프로그래밍 방식으로 참조 하 고 시스템의 역할을 해당 페이지에 바인딩합니다.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample22.vb)]

위의 코드는 잘 알고 있어야 합니다. <a id="_msoanchor_5"> </a> [ *추가 사용자 정보* 저장](../membership/storing-additional-user-information-vb.md) 자습서에서는 사용자 지정 `WizardStep`에서 웹 컨트롤을 참조 하는 두 개의 `FindControl` 문을 사용 했습니다. 그리고 CheckBoxList에 역할을 바인딩하는 코드는이 자습서의 앞부분에서 가져온 것입니다.

두 번째 프로그래밍 작업을 수행 하기 위해 "역할 지정" 단계가 완료 된 시기를 알아야 합니다. CreateUserWizard에는 방문자가 한 단계에서 다른 단계로 이동할 때마다 발생 하는 `ActiveStepChanged` 이벤트가 있습니다. 여기서는 사용자가 "완료" 단계에 도달 했는지 여부를 확인할 수 있습니다. 그렇다면 선택한 역할에 사용자를 추가 해야 합니다.

`ActiveStepChanged` 이벤트에 대 한 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample23.vb)]

사용자가 "완료" 단계에 도달한 경우 이벤트 처리기는 `RoleList` CheckBoxList의 항목을 열거 하 고, 사용자가 만든 사용자가 선택한 역할에 할당 됩니다.

브라우저를 통해이 페이지를 방문 하세요. CreateUserWizard의 첫 번째 단계는 새로운 사용자의 사용자 이름, 암호, 전자 메일 및 기타 키 정보를 요청 하는 표준 "새 계정에 등록" 단계입니다. 정보를 입력 하 여 Wanda 라는 새 사용자를 만듭니다.

[![Wanda 이라는 새 사용자를 만듭니다.](assigning-roles-to-users-vb/_static/image35.png)](assigning-roles-to-users-vb/_static/image34.png)

**그림 12**: Wanda 이라는 새 사용자 만들기 ([전체 크기 이미지를 보려면 클릭](assigning-roles-to-users-vb/_static/image36.png))

"사용자 만들기" 단추를 클릭 합니다. CreateUserWizard은 내부적으로 `Membership.CreateUser` 메서드를 호출 하 여 새 사용자 계정을 만든 후 다음 단계인 "역할 지정"으로 진행 합니다. 여기에 시스템 역할이 나열 됩니다. 감독자 확인란을 선택 하 고 다음을 클릭 합니다.

[Wanda을 감독자 역할의 구성원으로 설정 ![](assigning-roles-to-users-vb/_static/image38.png)](assigning-roles-to-users-vb/_static/image37.png)

**그림 13**: Wanda을 감독자 역할의 멤버로 만들기 ([전체 크기 이미지를 보려면 클릭](assigning-roles-to-users-vb/_static/image39.png))

[다음]을 클릭 하면 포스트백이 발생 하 고 `ActiveStep` "Complete" 단계로 업데이트 됩니다. `ActiveStepChanged` 이벤트 처리기에서 최근에 만든 사용자 계정이 감독자 역할에 할당 됩니다. 이를 확인 하려면 `UsersAndRoles.aspx` 페이지로 돌아가 `RoleList` DropDownList에서 감독자를 선택 합니다. 그림 14와 같이 감독자는 이제 Bruce, Tito 및 Wanda의 세 가지 사용자로 구성 됩니다.

[![Bruce, Tito 및 Wanda는 모두 감독자입니다.](assigning-roles-to-users-vb/_static/image41.png)](assigning-roles-to-users-vb/_static/image40.png)

**그림 14**: Bruce, Tito 및 Wanda는 모두 감독자입니다 ([전체 크기 이미지를 보려면 클릭](assigning-roles-to-users-vb/_static/image42.png)).

## <a name="summary"></a>요약

역할 프레임 워크는 특정 사용자의 역할에 대 한 정보를 검색 하는 메서드와 지정 된 역할에 속한 사용자를 결정 하는 메서드를 제공 합니다. 또한 하나 이상의 역할에 하나 이상의 사용자를 추가 하 고 제거 하는 방법에는 여러 가지가 있습니다. 이 자습서에서는 `AddUserToRole` 및 `RemoveUserFromRole`의 두 가지 방법에 대해 집중적으로 설명 했습니다. 단일 역할에 여러 사용자를 추가 하 고 단일 사용자에 게 여러 역할을 할당 하도록 디자인 된 추가 변형이 있습니다.

이 자습서에는 새로 만든 사용자의 역할을 지정 하 `WizardStep`를 포함 하도록 CreateUserWizard 컨트롤을 확장 하는 방법도 포함 되어 있습니다. 이러한 단계는 관리자가 새 사용자를 위한 사용자 계정을 만드는 프로세스를 간소화 하는 데 도움이 될 수 있습니다.

이 시점에서 역할을 만들고 삭제 하는 방법 및 역할에서 사용자를 추가 및 제거 하는 방법을 살펴보았습니다. 하지만 역할 기반 권한 부여를 적용 하는 것은 아직 확인 하지 않았습니다. <a id="_msoanchor_6"> </a> [다음 자습서](role-based-authorization-vb.md) 에서는 역할 별로 URL 권한 부여 규칙을 정의 하는 방법과 현재 로그인 한 사용자의 역할에 따라 페이지 수준 기능을 제한 하는 방법을 살펴보겠습니다.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 참고 자료

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 웹 사이트 관리 도구 개요](https://msdn.microsoft.com/library/ms228053.aspx)
- [ASP를 검사 합니다. 네트워크의 멤버 자격, 역할 및 프로필](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [웹 사이트 관리 도구 롤링](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)

### <a name="about-the-author"></a>저자 정보

Scott Mitchell는 여러 ASP/ASP. NET books의 작성자와 4GuysFromRolla.com의 창립자가 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 *[24 시간 이내에 ASP.NET 2.0을 sams teach yourself](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 것입니다. Scott은 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) 또는 [http://ScottOnWriting.NET](http://scottonwriting.net/)의 블로그를 통해 연결할 수 있습니다.

### <a name="special-thanks-to"></a>특별 해 주셔서 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Teresa Murphy입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) 에 줄을 놓습니다.

> [!div class="step-by-step"]
> [이전](creating-and-managing-roles-vb.md)
> [다음](role-based-authorization-vb.md)
