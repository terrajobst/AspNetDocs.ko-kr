---
uid: web-forms/overview/older-versions-security/roles/creating-and-managing-roles-vb
title: 역할 만들기 및 관리 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 역할 프레임 워크를 구성 하는 데 필요한 단계를 살펴봅니다. 그 다음에는 역할을 만들고 삭제 하는 웹 페이지를 빌드합니다.
ms.author: riande
ms.date: 03/24/2008
ms.assetid: 83af9f5f-9a00-4f83-8afc-e98bdd49014e
msc.legacyurl: /web-forms/overview/older-versions-security/roles/creating-and-managing-roles-vb
msc.type: authoredcontent
ms.openlocfilehash: 825e2afb750925637d308b7ceb35e1b02b708c1d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74586429"
---
# <a name="creating-and-managing-roles-vb"></a>역할 만들기 및 관리(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/VB.09.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/aspnet_tutorial09_CreatingRoles_vb.pdf)

> 이 자습서에서는 역할 프레임 워크를 구성 하는 데 필요한 단계를 살펴봅니다. 그 다음에는 역할을 만들고 삭제 하는 웹 페이지를 빌드합니다.

## <a name="introduction"></a>소개

<a id="_msoanchor_1"> </a> [*사용자 기반 권한 부여*](../membership/user-based-authorization-vb.md) 자습서에서는 URL 권한 부여를 사용 하 여 페이지 집합에서 특정 사용자를 제한 하 고, 방문한 사용자에 따라 ASP.NET 페이지의 기능을 조정 하는 선언적 및 프로그래밍 방식의 기술을 살펴보았습니다. 그러나 사용자를 기준으로 페이지 액세스 또는 기능에 대 한 권한을 부여 하는 것은 사용자 계정이 많거나 사용자의 권한이 자주 변경 되는 시나리오에서 유지 관리 하기가 어려울 수 있습니다. 사용자가 특정 작업을 수행 하기 위한 권한 부여를 얻거나 잃을 때 관리자는 적절 한 URL 권한 부여 규칙, 선언적 마크업 및 코드를 업데이트 해야 합니다.

일반적으로 사용자를 그룹이 나 *역할로* 분류 한 다음 역할 별로 사용 권한을 적용 하는 데 도움이 됩니다. 예를 들어 대부분의 웹 응용 프로그램에는 관리 사용자 에게만 예약 된 특정 페이지 또는 작업 집합이 있습니다. *사용자 기반 권한 부여* 자습서에서 배운 기술을 사용 하 여 지정 된 사용자 계정에서 관리 작업을 수행할 수 있도록 적절 한 URL 권한 부여 규칙, 선언적 태그 및 코드를 추가 합니다. 그러나 새 관리자가 추가 되었거나 기존 관리자의 관리 권한이 해지 된 경우에는 구성 파일 및 웹 페이지를 반환 하 고 업데이트 해야 합니다. 그러나 역할을 사용 하 여 관리자 역할을 만들고 이러한 신뢰할 수 있는 사용자를 관리자 역할에 할당할 수 있습니다. 다음으로, 관리자 역할에서 다양 한 관리 작업을 수행할 수 있도록 적절 한 URL 권한 부여 규칙, 선언적 태그 및 코드를 추가 합니다. 이 인프라를 구축 하 고 나면 사이트에 새 관리자를 추가 하거나 기존 관리자를 제거 하는 것은 관리자 역할에서 사용자를 포함 하거나 제거 하는 것 만큼 간단 합니다. 구성, 선언 태그 또는 코드 변경이 필요 하지 않습니다.

ASP.NET는 역할을 정의 하 고 사용자 계정과 연결 하는 역할 프레임 워크를 제공 합니다. 역할 프레임 워크를 사용 하면 역할을 만들고 삭제 하 고, 역할에서 사용자를 추가 하거나 제거 하 고, 특정 역할에 속한 사용자 집합을 확인 하 고, 사용자가 특정 역할에 속하는지 여부를 알 수 있습니다. 역할 프레임 워크가 구성 된 후에는 URL 권한 부여 규칙을 통해 역할 별로 페이지에 대 한 액세스를 제한 하 고, 현재 로그온 한 사용자의 역할에 따라 페이지에 추가 정보나 기능을 표시 하거나 숨길 수 있습니다.

이 자습서에서는 역할 프레임 워크를 구성 하는 데 필요한 단계를 살펴봅니다. 그 다음에는 역할을 만들고 삭제 하는 웹 페이지를 빌드합니다. <a id="_msoanchor_2"> </a> [*사용자에 게 역할 할당*](assigning-roles-to-users-vb.md) 자습서에서는 역할에서 사용자를 추가 및 제거 하는 방법을 살펴보겠습니다. <a id="_msoanchor_3"> </a> [*역할 기반 권한 부여*](role-based-authorization-vb.md) 자습서에서는 방문한 사용자의 역할에 따라 페이지 기능을 조정 하는 방법과 함께 역할 별로 페이지에 대 한 액세스를 제한 하는 방법을 알아봅니다. 시작 하겠습니다.

## <a name="step-1-adding-new-aspnet-pages"></a>1 단계: 새 ASP.NET 페이지 추가

이 자습서 및 다음 두 가지는 다양 한 역할 관련 함수 및 기능을 검사 합니다. 이러한 자습서에서 다루는 항목을 구현 하려면 일련의 ASP.NET 페이지가 필요 합니다. 이러한 페이지를 만들어 사이트 맵을 업데이트 해 보겠습니다.

`Roles`이라는 프로젝트에서 새 폴더를 만들어 시작 합니다. 그런 다음 `Roles` 폴더에 4 개의 새 ASP.NET 페이지를 추가 하 여 각 페이지를 `Site.master` 마스터 페이지에 연결 합니다. 페이지 이름:

- `ManageRoles.aspx`
- `UsersAndRoles.aspx`
- `CreateUserWizardWithRoles.aspx`
- `RoleBasedAuthorization.aspx`

이 시점에서 프로젝트의 솔루션 탐색기은 그림 1에 표시 된 화면과 비슷해야 합니다.

[![새 페이지 4 개가 역할 폴더에 추가 되었습니다.](creating-and-managing-roles-vb/_static/image2.png)](creating-and-managing-roles-vb/_static/image1.png)

**그림 1**: `Roles` 폴더에 새 페이지 4 개 추가 ([전체 크기 이미지를 보려면 클릭](creating-and-managing-roles-vb/_static/image3.png))

각 페이지에는 마스터 페이지의 ContentPlaceHolders 표시자 각각에 대해 하나씩, `MainContent` 및 `LoginContent`의 두 콘텐츠 컨트롤이 있습니다.

[!code-aspx[Main](creating-and-managing-roles-vb/samples/sample1.aspx)]

`LoginContent` ContentPlaceHolder의 기본 태그는 사용자가 인증 되었는지 여부에 따라 사이트에서 로그온 하거나 로그 오프할 수 있는 링크를 표시 합니다. 그러나 ASP.NET 페이지에 `Content2` Content 컨트롤이 있으면 마스터 페이지의 기본 태그를 재정의 합니다. <a id="_msoanchor_4"> </a> [*폼 인증 자습서 개요*](../introduction/an-overview-of-forms-authentication-vb.md) 에서 설명한 대로 기본 태그 재정의는 왼쪽 열에 로그인 관련 옵션을 표시 하지 않으려는 페이지에서 유용 합니다.

그러나 이러한 네 페이지에서는 `LoginContent` ContentPlaceHolder에 대 한 마스터 페이지의 기본 태그를 표시 하려고 합니다. 따라서 `Content2` 콘텐츠 컨트롤에 대 한 선언적 태그를 제거 합니다. 이렇게 한 후 네 페이지의 각 태그에는 하나의 콘텐츠 컨트롤만 포함 되어야 합니다.

마지막으로, 이러한 새 웹 페이지를 포함 하도록 사이트 맵 (`Web.sitemap`)을 업데이트 해 보겠습니다. 멤버 자격 자습서에 대해 추가한 `<siteMapNode>` 뒤에 다음 XML을 추가 합니다.

[!code-xml[Main](creating-and-managing-roles-vb/samples/sample2.xml)]

사이트 맵이 업데이트 된 상태에서 브라우저를 통해 사이트를 방문 합니다. 그림 2에 나와 있는 것 처럼 왼쪽의 탐색에는 역할 자습서에 대 한 항목이 포함 되어 있습니다.

[![새 페이지 4 개가 역할 폴더에 추가 되었습니다.](creating-and-managing-roles-vb/_static/image5.png)](creating-and-managing-roles-vb/_static/image4.png)

**그림 2**: `Roles` 폴더에 새 페이지 4 개 추가 ([전체 크기 이미지를 보려면 클릭](creating-and-managing-roles-vb/_static/image6.png))

## <a name="step-2-specifying-and-configuring-the-roles-framework-provider"></a>2 단계: 역할 프레임 워크 공급자 지정 및 구성

멤버 프레임 워크와 마찬가지로 역할 프레임 워크는 공급자 모델 위에 빌드됩니다. <a id="_msoanchor_5"> </a> [*보안 기본 사항 및 ASP.NET 지원*](../introduction/security-basics-and-asp-net-support-vb.md) 자습서에 설명 된 대로 .NET Framework에는 [`AuthorizationStoreRoleProvider`](https://msdn.microsoft.com/library/system.web.security.authorizationstoreroleprovider.aspx), [`WindowsTokenRoleProvider`](https://msdn.microsoft.com/library/system.web.security.windowstokenroleprovider.aspx)및 [`SqlRoleProvider`](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx)의 세 가지 기본 제공 역할 공급자가 제공 됩니다. 이 자습서 시리즈는 Microsoft SQL Server 데이터베이스를 역할 저장소로 사용 하는 `SqlRoleProvider`를 중심으로 설명 합니다.

아래에는 역할 프레임 워크가 포함 되어 있으며, `SqlRoleProvider` 멤버 프레임 워크 및 `SqlMembershipProvider`와 동일 하 게 작동 합니다. .NET Framework는 역할 프레임 워크에 대 한 API 역할을 하는 `Roles` 클래스를 포함 합니다. `Roles` 클래스에는 `CreateRole`, `DeleteRole`, `GetAllRoles`, `AddUserToRole`, `IsUserInRole`등과 같은 공유 메서드가 있습니다. 이러한 메서드 중 하나를 호출 하면 `Roles` 클래스가 구성 된 공급자에 대 한 호출을 위임 합니다. `SqlRoleProvider`은 응답에서 역할 관련 테이블 (`aspnet_Roles` 및 `aspnet_UsersInRoles`)과 함께 작동 합니다.

응용 프로그램에서 `SqlRoleProvider` 공급자를 사용 하기 위해 저장소로 사용할 데이터베이스를 지정 해야 합니다. `SqlRoleProvider`에는 지정 된 역할 저장소가 특정 데이터베이스 테이블, 뷰 및 저장 프로시저를 포함 하는 것으로 예상 됩니다. 이러한 필수 데이터베이스 개체는 [`aspnet_regsql.exe` 도구](https://msdn.microsoft.com/library/ms229862.aspx)를 사용 하 여 추가할 수 있습니다. 이 시점에는 `SqlRoleProvider`에 필요한 스키마가 있는 데이터베이스가 이미 있습니다. <a id="_msoanchor_6"> </a> [*SQL Server에서 멤버 자격 스키마 만들기*](../membership/creating-the-membership-schema-in-sql-server-vb.md) 자습서로 돌아가서 `SecurityTutorials.mdf` 라는 데이터베이스를 만들고 `aspnet_regsql.exe` 사용 하 여 `SqlRoleProvider`에 필요한 데이터베이스 개체를 포함 하는 응용 프로그램 서비스를 추가 했습니다. 따라서 역할을 지원 하 고 `SecurityTutorials.mdf` 데이터베이스에서 역할 저장소로 `SqlRoleProvider`을 사용 하도록 역할 프레임 워크에 알려야 합니다.

역할 프레임 워크는 응용 프로그램 `Web.config` 파일의 `<roleManager>` 요소를 통해 구성 됩니다. 기본적으로 역할 지원은 사용 되지 않습니다. 이 기능을 사용 하려면 [`<roleManager>`](https://msdn.microsoft.com/library/ms164660.aspx) 요소의 `enabled` 특성을 다음과 같이 `true`로 설정 해야 합니다.

[!code-xml[Main](creating-and-managing-roles-vb/samples/sample3.xml)]

기본적으로 모든 웹 응용 프로그램에는 `SqlRoleProvider`형식의 `AspNetSqlRoleProvider` 라는 역할 공급자가 있습니다. 이 기본 공급자는 `machine.config` (`%WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG`에 있음)에 등록 됩니다.

[!code-xml[Main](creating-and-managing-roles-vb/samples/sample4.xml)]

공급자의 `connectionStringName` 특성은 사용 되는 역할 저장소를 지정 합니다. `AspNetSqlRoleProvider` 공급자는이 특성을 `LocalSqlServer`로 설정 합니다 .이 특성은 기본적으로 `App_Data` 이라는 `aspnet.mdf`폴더에 있는 SQL Server 2005 Express Edition 데이터베이스에 `machine.config`에도 정의 됩니다.

따라서 응용 프로그램의 `Web.config` 파일에서 공급자 정보를 지정 하지 않고 역할 프레임 워크를 사용 하도록 설정 하는 경우 응용 프로그램은 등록 된 기본 역할 공급자 인 `AspNetSqlRoleProvider`를 사용 합니다. `~/App_Data/aspnet.mdf` 데이터베이스가 없으면 ASP.NET 런타임은 자동으로이를 만들고 응용 프로그램 서비스 스키마를 추가 합니다. 그러나 `aspnet.mdf` 데이터베이스를 사용 하지 않으려고 합니다. 대신 이미 만들고 응용 프로그램 서비스 스키마를 추가한 `SecurityTutorials.mdf` 데이터베이스를 사용 하려고 합니다. 이 수정 작업은 다음 두 가지 방법 중 하나로 수행할 수 있습니다.

- <strong>`Web.config`</strong>에서<strong>`LocalSqlServer`</strong> <strong>연결 문자열 이름</strong> <strong>에 대 한 값을 지정</strong> 합니다 <strong>.</strong> `Web.config`에서 `LocalSqlServer` 연결 문자열 이름 값을 덮어써서 등록 된 기본 역할 공급자 (`AspNetSqlRoleProvider`)를 사용 하 여 `SecurityTutorials.mdf` 데이터베이스에서 올바르게 작동할 수 있습니다. 이 기술에 대 한 자세한 내용은 [Scott Guthrie](https://weblogs.asp.net/scottgu/)의 블로그 게시물, [SQL Server 2000 또는 SQL Server 2005를 사용 하도록 ASP.NET 2.0 애플리케이션 서비스 구성](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx)을 참조 하세요.
- <strong>`SqlRoleProvider`</strong> <strong>형식의 등록 된 새 공급자를 추가</strong> 하 고<strong>`SecurityTutorials.mdf`</strong>데이터베이스 <strong>를 가리키도록</strong> <strong>`connectionStringName`</strong>설정을 <strong>구성</strong> <strong>합니다.</strong> 이 방법은 <a id="_msoanchor_7"> </a> [*SQL Server 자습서에서 멤버 자격 스키마 만들기*](../membership/creating-the-membership-schema-in-sql-server-vb.md) 에서 권장 하 고 사용 하는 방법입니다 .이 방법에서는이 자습서에서 사용 하는 방법에 대해서도 알아보겠습니다.

`Web.config` 파일에 다음 역할 구성 태그를 추가 합니다. 이 태그는 이름이 `SecurityTutorialsSqlRoleProvider.` 새 공급자를 등록 합니다.

[!code-xml[Main](creating-and-managing-roles-vb/samples/sample5.xml)]

위의 태그는 `<roleManager>` 요소의 `defaultProvider` 특성을 통해 `SecurityTutorialsSqlRoleProvider`를 기본 공급자로 정의 합니다. 또한 `SecurityTutorialsSqlRoleProvider`의 `applicationName` 설정을 `SecurityTutorials`로 설정 합니다 .이 설정은 멤버 자격 공급자 (`SecurityTutorialsSqlMembershipProvider`)에서 사용 하는 것과 `applicationName` 동일 합니다. 여기에 표시 되지 않지만 `SqlRoleProvider`에 대 한 [`<add>` 요소](https://msdn.microsoft.com/library/ms164662.aspx) 에는 데이터베이스 제한 시간 (초)을 지정 하는 `commandTimeout` 특성이 포함 될 수도 있습니다. 기본값은 30입니다.

이 구성 태그를 사용 하면 응용 프로그램 내에서 역할 기능을 사용할 준비가 되었습니다.

> [!NOTE]
> 위의 구성 태그는 `<roleManager>` 요소의 `enabled` 및 `defaultProvider` 특성을 사용 하는 방법을 보여 줍니다. 역할 프레임 워크에서 사용자 별로 역할 정보를 연결 하는 방법에 영향을 주는 다양 한 특성이 있습니다. <a id="_msoanchor_8"> </a> [*역할 기반 권한 부여*](role-based-authorization-vb.md) 자습서에서 이러한 설정을 살펴볼 것입니다.

## <a name="step-3-examining-the-roles-api"></a>3 단계: 역할 API 검사

역할 프레임 워크의 기능은 역할 기반 작업을 수행 하기 위한 13 공유 메서드를 포함 하는 [`Roles` 클래스](https://msdn.microsoft.com/library/system.web.security.roles.aspx)를 통해 노출 됩니다. 4 단계와 6 단계에서 역할을 만들고 삭제 하는 방법을 살펴보면 시스템에서 역할을 추가 하거나 제거 하는 [`CreateRole`](https://msdn.microsoft.com/library/system.web.security.roles.createrole.aspx) 및 [`DeleteRole`](https://msdn.microsoft.com/library/system.web.security.roles.deleterole.aspx) 방법을 사용 합니다.

시스템의 모든 역할 목록을 가져오려면 [`GetAllRoles` 메서드](https://msdn.microsoft.com/library/system.web.security.roles.getallroles.aspx) 를 사용 합니다 (5 단계 참조). [`RoleExists` 메서드](https://msdn.microsoft.com/library/system.web.security.roles.roleexists.aspx) 는 지정 된 역할이 있는지 여부를 나타내는 부울 값을 반환 합니다.

다음 자습서에서는 사용자를 역할에 연결 하는 방법을 살펴봅니다. `Roles` 클래스의 [`AddUserToRole`](https://msdn.microsoft.com/library/system.web.security.roles.addusertorole.aspx), [`AddUserToRoles`](https://msdn.microsoft.com/library/system.web.security.roles.addusertoroles.aspx), [`AddUsersToRole`](https://msdn.microsoft.com/library/system.web.security.roles.adduserstorole.aspx)및 [`AddUsersToRoles`](https://msdn.microsoft.com/library/system.web.security.roles.adduserstoroles.aspx) 메서드는 하나 이상의 역할에 하나 이상의 사용자를 추가 합니다. 역할에서 사용자를 제거 하려면 [`RemoveUserFromRole`](https://msdn.microsoft.com/library/system.web.security.roles.removeuserfromrole.aspx), [`RemoveUserFromRoles`](https://msdn.microsoft.com/library/system.web.security.roles.removeuserfromroles.aspx), [`RemoveUsersFromRole`](https://msdn.microsoft.com/library/system.web.security.roles.removeusersfromrole.aspx)또는 [`RemoveUsersFromRoles`](https://msdn.microsoft.com/library/system.web.security.roles.removeusersfromroles.aspx) 메서드를 사용 합니다.

<a id="_msoanchor_9"> </a> [*역할 기반 권한 부여*](role-based-authorization-vb.md) 자습서에서는 현재 로그인 한 사용자의 역할에 따라 프로그래밍 방식으로 기능을 표시 하거나 숨기는 방법을 살펴보겠습니다. 이를 위해 역할 클래스의 [`FindUsersInRole`](https://msdn.microsoft.com/library/system.web.security.roles.findusersinrole.aspx), [`GetRolesForUser`](https://msdn.microsoft.com/library/system.web.security.roles.getrolesforuser.aspx), [`GetUsersInRole`](https://msdn.microsoft.com/library/system.web.security.roles.getusersinrole.aspx)또는 [`IsUserInRole`](https://msdn.microsoft.com/library/system.web.security.roles.isuserinrole.aspx) 메서드를 사용할 수 있습니다.

> [!NOTE]
> 이러한 메서드 중 하나가 호출 될 때마다 `Roles` 클래스가 구성 된 공급자에 대 한 호출을 위임 합니다. 이 경우에는 호출이 `SqlRoleProvider`전송 되 고 있음을 의미 합니다. 그러면 `SqlRoleProvider`는 호출 된 메서드를 기반으로 적절 한 데이터베이스 작업을 수행 합니다. 예를 들어 코드 `Roles.CreateRole("Administrators")`는 `aspnet_Roles_CreateRole` 저장 프로시저를 실행 하 `SqlRoleProvider`를 생성 합니다 .이 프로시저는 관리자 라는 `aspnet_Roles` 테이블에 새 레코드를 삽입 합니다.

이 자습서의 나머지 부분에서는 `Roles` 클래스의 `CreateRole`, `GetAllRoles`및 `DeleteRole` 메서드를 사용 하 여 시스템에서 역할을 관리 하는 방법을 살펴봅니다.

## <a name="step-4-creating-new-roles"></a>4 단계: 새 역할 만들기

역할은 임의로 사용자를 그룹화 하는 방법을 제공 하며, 가장 일반적으로이 그룹은 권한 부여 규칙을 적용 하는 더 편리한 방법으로 사용 됩니다. 하지만 역할을 권한 부여 메커니즘으로 사용 하려면 먼저 응용 프로그램에 존재 하는 역할을 정의 해야 합니다. 아쉽게도 ASP.NET에는 CreateRoleWizard 컨트롤이 포함 되어 있지 않습니다. 새 역할을 추가 하려면 적절 한 사용자 인터페이스를 만들고 역할 API를 직접 호출 해야 합니다. 좋은 소식은이를 매우 쉽게 수행할 수 있다는 것입니다.

> [!NOTE]
> CreateRoleWizard 웹 컨트롤은 없지만 웹 응용 프로그램의 구성을 보고 관리 하는 데 도움이 되도록 설계 된 로컬 ASP.NET 응용 프로그램 인 [ASP.NET 웹 사이트 관리 도구가](https://msdn.microsoft.com/library/ms228053.aspx)있습니다. 그러나 두 가지 이유로 ASP.NET 웹 사이트 관리 도구의 큰 팬은 아닙니다. 첫째,이는 약간 버그가 있는 사용자 환경에서 원하는 작업을 수행할 수 있습니다. 둘째로, ASP.NET 웹 사이트 관리 도구는 로컬 에서만 작동 하도록 설계 되었습니다. 즉, 라이브 사이트의 역할을 원격으로 관리 해야 하는 경우 고유한 역할 관리 웹 페이지를 만들어야 합니다. 이러한 두 가지 이유 때문에이 자습서에서는 ASP.NET 웹 사이트 관리 도구에 의존 하지 않고 웹 페이지에서 필요한 역할 관리 도구를 구축 하는 방법에 중점을 둡니다.

`Roles` 폴더에서 `ManageRoles.aspx` 페이지를 열고 텍스트 상자와 단추 웹 컨트롤을 페이지에 추가 합니다. TextBox 컨트롤의 `ID` 속성을 `RoleName`로 설정 하 고 단추의 `ID` 및 `Text` 속성을 각각 `CreateRoleButton`로 설정 하 고 역할을 만듭니다. 이제 페이지의 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](creating-and-managing-roles-vb/samples/sample6.aspx)]

다음으로 디자이너에서 `CreateRoleButton` Button 컨트롤을 두 번 클릭 하 여 `Click` 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-vb[Main](creating-and-managing-roles-vb/samples/sample7.vb)]

위의 코드는 `RoleName` 텍스트 상자에 입력 한 잘린 역할 이름을 `newRoleName` 변수에 할당 하 여 시작 합니다. 그런 다음 `Roles` 클래스의 `RoleExists` 메서드를 호출 하 여 역할 `newRoleName`이 시스템에 이미 있는지 여부를 확인 합니다. 역할이 없으면 `CreateRole` 메서드에 대 한 호출을 통해 생성 됩니다. `CreateRole` 메서드에 시스템에 이미 있는 역할 이름이 전달 되 면 `ProviderException` 예외가 throw 됩니다. 이렇게 하면 코드에서 `CreateRole`를 호출 하기 전에 역할이 시스템에 아직 존재 하지 않는지 확인 합니다. `Click` 이벤트 처리기는 `RoleName` TextBox의 `Text` 속성을 지웁니다.

> [!NOTE]
> 사용자가 `RoleName` 텍스트 상자에 값을 입력 하지 않으면 어떻게 되는지 궁금할 수 있습니다. `CreateRole` 메서드에 전달 된 값이 `Nothing` 또는 빈 문자열인 경우 예외가 발생 합니다. 마찬가지로 역할 이름에 쉼표가 포함 되어 있으면 예외가 발생 합니다. 따라서 페이지에는 사용자가 역할을 입력 하 고 쉼표가 포함 되지 않도록 유효성 검사 컨트롤이 포함 되어야 합니다. 판독기에 대 한 연습으로 둡니다.

관리자 라는 역할을 만들어 보겠습니다. 브라우저를 통해 `ManageRoles.aspx` 페이지를 방문 하 여 텍스트 상자에 관리자를 입력 하 고 (그림 3 참조) 역할 만들기 단추를 클릭 합니다.

[관리자 역할을 만드는 ![](creating-and-managing-roles-vb/_static/image8.png)](creating-and-managing-roles-vb/_static/image7.png)

**그림 3**: 관리자 역할 만들기 ([전체 크기 이미지를 보려면 클릭](creating-and-managing-roles-vb/_static/image9.png))

어떻게 되나요? 포스트백이 발생 하지만 역할이 실제로 시스템에 추가 되었다는 시각적 신호는 없습니다. 5 단계에서이 페이지를 업데이트 하 여 시각적 피드백을 포함 합니다. 그러나 지금은 `SecurityTutorials.mdf` 데이터베이스로 이동 하 여 `aspnet_Roles` 테이블의 데이터를 표시 하 여 역할이 만들어졌는지 확인할 수 있습니다. 그림 4와 같이 `aspnet_Roles` 테이블에는 단순히 추가 된 관리자 역할에 대 한 레코드가 포함 되어 있습니다.

[관리자에 대 한 행이 있는 aspnet_Roles 테이블 ![](creating-and-managing-roles-vb/_static/image11.png)](creating-and-managing-roles-vb/_static/image10.png)

**그림 4**: 관리자에 대 한 행이 있는 `aspnet_Roles` 테이블 ([전체 크기 이미지를 보려면 클릭](creating-and-managing-roles-vb/_static/image12.png))

## <a name="step-5-displaying-the-roles-in-the-system"></a>5 단계: 시스템에서 역할 표시

현재 역할의 목록이 시스템에 포함 되도록 `ManageRoles.aspx` 페이지를 늘려 보겠습니다. 이를 수행 하려면 GridView 컨트롤을 페이지에 추가 하 고 해당 `ID` 속성을 `RoleList`로 설정 합니다. 다음으로, 다음 코드를 사용 하 여 `DisplayRolesInGrid` 이라는 페이지의 코드 숨김이 클래스에 메서드를 추가 합니다.

[!code-vb[Main](creating-and-managing-roles-vb/samples/sample8.vb)]

`Roles` 클래스의 `GetAllRoles` 메서드는 시스템의 모든 역할을 문자열 배열로 반환 합니다. 그런 다음이 문자열 배열을 GridView에 바인딩합니다. 페이지가 처음 로드 될 때 역할 목록을 GridView에 바인딩하려면 페이지의 `Page_Load` 이벤트 처리기에서 `DisplayRolesInGrid` 메서드를 호출 해야 합니다. 다음 코드는 페이지를 처음 방문할 때이 메서드를 호출 하지만 이후에 다시 게시 하는 경우에는 호출 하지 않습니다.

[!code-vb[Main](creating-and-managing-roles-vb/samples/sample9.vb)]

이 코드가 준비 되 면 브라우저를 통해 페이지를 방문 하세요. 그림 5와 같이 항목 이라는 레이블이 지정 된 단일 열이 있는 표가 표시 됩니다. 표는 4 단계에서 추가한 관리자 역할에 대 한 행을 포함 합니다.

[GridView ![단일 열에 역할을 표시 합니다.](creating-and-managing-roles-vb/_static/image14.png)](creating-and-managing-roles-vb/_static/image13.png)

**그림 5**: GridView가 단일 열에 역할을 표시 합니다 ([전체 크기 이미지를 보려면 클릭](creating-and-managing-roles-vb/_static/image15.png)).

Gridview의 `AutoGenerateColumns` 속성이 True (기본값)로 설정 되어 있으므로 gridview는 항목으로 레이블이 지정 된 유일한 열을 표시 합니다 .이로 인해 GridView가 `DataSource`의 각 속성에 대 한 열을 자동으로 만듭니다. 배열에는 배열의 요소를 나타내는 단일 속성이 있으므로 GridView의 단일 열이 있습니다.

GridView를 사용 하 여 데이터를 표시 하는 경우 GridView에서 암시적으로 생성 하는 대신 열을 명시적으로 정의 하는 것이 좋습니다. 열을 명시적으로 정의 하 여 데이터의 형식을 지정 하 고, 열을 다시 정렬 하 고, 다른 일반적인 작업을 수행 하는 것이 훨씬 쉽습니다. 따라서 해당 열이 명시적으로 정의 되도록 GridView의 선언적 태그를 업데이트 해 보겠습니다.

GridView의 `AutoGenerateColumns` 속성을 False로 설정 하 여 시작 합니다. 그런 다음 Templatefield로 변환를 모눈에 추가 하 고, 해당 `HeaderText` 속성을 역할로 설정 하 고, 배열의 내용을 표시 하도록 `ItemTemplate`를 구성 합니다. 이렇게 하려면 `RoleNameLabel` 이라는 Label 웹 컨트롤을 `ItemTemplate`에 추가 하 고 `Text` 속성을에 바인딩합니다 `Container.DataItem.`

이러한 속성과 `ItemTemplate`의 내용은 선언적으로 설정 하거나 GridView의 필드 대화 상자 및 템플릿 편집 인터페이스를 통해 설정할 수 있습니다. 필드 대화 상자에 연결 하려면 GridView의 스마트 태그에서 열 편집 링크를 클릭 합니다. 그런 다음 필드 자동 생성 확인란의 선택을 취소 하 여 `AutoGenerateColumns` 속성을 False로 설정 하 고 `HeaderText` 속성을 Role로 설정 하 여 Templatefield로 변환를 GridView에 추가 합니다. `ItemTemplate`내용을 정의 하려면 GridView의 스마트 태그에서 템플릿 편집 옵션을 선택 합니다. Label 웹 컨트롤을 `ItemTemplate`끌어 놓고 `ID` 속성을 `RoleNameLabel`로 설정 하 고 해당 `Text` 속성이 `Container.DataItem`에 바인딩되도록 데이터 바인딩 설정을 구성 합니다.

사용 하는 방법에 관계 없이 GridView의 결과 선언 태그는 다음과 유사 하 게 됩니다.

[!code-aspx[Main](creating-and-managing-roles-vb/samples/sample10.aspx)]

> [!NOTE]
> 배열 내용은 `<%# Container.DataItem %>`데이터 바인딩 구문을 사용 하 여 표시 됩니다. GridView에 바인딩된 배열의 내용을 표시할 때이 구문이 사용 되는 이유에 대 한 자세한 설명은이 자습서의 범위를 벗어나는 것입니다. 이러한 문제에 대 한 자세한 내용은 [스칼라 배열을 데이터 웹 컨트롤에 바인딩](http://aspnet.4guysfromrolla.com/articles/082504-1.aspx)을 참조 하세요.

현재는 페이지를 처음 방문할 때 `RoleList` GridView가 역할 목록에만 바인딩되어 있습니다. 새 역할이 추가 될 때마다 그리드를 새로 고쳐야 합니다. 이를 수행 하려면 새 역할을 만들 경우 `DisplayRolesInGrid` 메서드를 호출 하도록 `CreateRoleButton` 단추의 `Click` 이벤트 처리기를 업데이트 합니다.

[!code-vb[Main](creating-and-managing-roles-vb/samples/sample11.vb)]

이제 사용자가 새 역할을 추가 하면 `RoleList` GridView가 포스트백에 방금 추가 된 역할을 표시 하 여 역할이 성공적으로 만들어졌는지 시각적 피드백을 제공 합니다. 이를 설명 하려면 브라우저를 통해 `ManageRoles.aspx` 페이지를 방문 하 여 감독자 라는 역할을 추가 합니다. 역할 만들기 단추를 클릭 하면 다시 게시가 뒤따르게 새 역할인 감독자 뿐만 아니라 관리자도 포함 하도록 표가 업데이트 됩니다.

[감독자 역할이 추가 된 ![](creating-and-managing-roles-vb/_static/image17.png)](creating-and-managing-roles-vb/_static/image16.png)

**그림 6**: 감독자 역할이 추가 됨 ([전체 크기 이미지를 보려면 클릭](creating-and-managing-roles-vb/_static/image18.png))

## <a name="step-6-deleting-roles"></a>6 단계: 역할 삭제

이 시점에서 사용자는 새 역할을 만들고 `ManageRoles.aspx` 페이지에서 기존 역할을 모두 볼 수 있습니다. 사용자가 역할을 삭제할 수도 있습니다. `Roles.DeleteRole` 메서드에는 두 개의 오버 로드가 있습니다.

- [`DeleteRole(roleName)`](https://msdn.microsoft.com/library/ek4sywc0.aspx) - *roleName*역할을 삭제 합니다. 역할이 하나 이상의 멤버를 포함 하는 경우 예외가 throw 됩니다.
- [`DeleteRole(roleName, throwOnPopulatedRole)`](https://msdn.microsoft.com/library/38h6wf59.aspx) - *roleName*역할을 삭제 합니다. *ThrowOnPopulateRole* 가 `True`되 면 역할이 하나 이상의 멤버를 포함 하는 경우 예외가 throw 됩니다. *ThrowOnPopulateRole* 가 `False`되 면 멤버가 포함 되어 있는지 여부에 관계 없이 역할이 삭제 됩니다. 내부적으로 `DeleteRole(roleName)` 메서드는 `DeleteRole(roleName, True)`를 호출 합니다.

*RoleName* 가 `Nothing` 또는 빈 문자열이 고 *roleName* 에 쉼표가 포함 된 경우에도 `DeleteRole` 메서드는 예외를 throw 합니다. *RoleName* 가 시스템에 없으면 예외를 발생 시 키 지 않고 `DeleteRole` 자동으로 실패 합니다.

클릭 하면 선택한 역할을 삭제 하는 삭제 단추를 포함 하도록 `ManageRoles.aspx`에서 GridView를 확대 하겠습니다. 필드 대화 상자로 이동 하 고 CommandField 옵션 아래에 있는 삭제 단추를 추가 하 여 GridView에 삭제 단추를 추가 하 여 시작 합니다. 삭제 단추를 맨 왼쪽 열로 만들고 해당 `DeleteText` 속성을 역할 삭제로 설정 합니다.

[![RoleList GridView에 삭제 단추를 추가 합니다.](creating-and-managing-roles-vb/_static/image20.png)](creating-and-managing-roles-vb/_static/image19.png)

**그림 7**: `RoleList` GridView에 삭제 단추 추가 ([전체 크기 이미지를 보려면 클릭](creating-and-managing-roles-vb/_static/image21.png))

삭제 단추를 추가한 후 GridView의 선언 태그는 다음과 같이 표시 됩니다.

[!code-aspx[Main](creating-and-managing-roles-vb/samples/sample12.aspx)]

다음으로 GridView의 `RowDeleting` 이벤트에 대 한 이벤트 처리기를 만듭니다. 역할 삭제 단추를 클릭할 때 다시 게시 될 때 발생 하는 이벤트입니다. 다음 코드를 이벤트 처리기에 추가합니다.

[!code-vb[Main](creating-and-managing-roles-vb/samples/sample13.vb)]

이 코드는 역할 삭제 단추가 클릭 된 행에서 `RoleNameLabel` 웹 컨트롤을 프로그래밍 방식으로 참조 하 여 시작 합니다. 그런 다음 `Roles.DeleteRole` 메서드를 호출 하 여 `RoleNameLabel`의 `Text`를 전달 하 고 `False`역할에 연결 된 사용자가 있는지 여부에 관계 없이 역할을 삭제 합니다. 마지막으로, `RoleList` GridView가 새로 고쳐지고 방금 삭제 된 역할이 표에 더 이상 표시 되지 않습니다.

> [!NOTE]
> 역할 삭제 단추는 역할을 삭제 하기 전에 사용자에 게 어떤 종류의 확인도 필요 하지 않습니다. 동작을 확인 하는 가장 쉬운 방법 중 하나는 클라이언트 쪽 확인 대화 상자를 통하는 것입니다. 이 기술에 대 한 자세한 내용은 [삭제할 때 클라이언트 쪽 확인 추가](https://asp.net/learn/data-access/tutorial-42-vb.aspx)를 참조 하세요.

## <a name="summary"></a>요약

대부분의 웹 응용 프로그램에는 특정 사용자 클래스 에서만 사용할 수 있는 특정 권한 부여 규칙 또는 페이지 수준 기능이 있습니다. 예를 들어 관리자만 액세스할 수 있는 웹 페이지 집합이 있을 수 있습니다. 사용자를 기준으로 이러한 권한 부여 규칙을 정의 하는 대신 역할을 기반으로 규칙을 정의 하는 것이 더 유용 합니다. 즉, 사용자의 Scott 및 Jisun에서 관리 웹 페이지에 액세스할 수 있도록 명시적으로 허용 하는 것이 아니라 관리자 역할 구성원이 이러한 페이지에 액세스 하는 것을 허용한 다음, Scott 및 Jisun을 관리자 역할.

역할 프레임 워크를 사용 하면 역할을 쉽게 만들고 관리할 수 있습니다. 이 자습서에서는 Microsoft SQL Server 데이터베이스를 역할 저장소로 사용 하는 `SqlRoleProvider`를 사용 하도록 역할 프레임 워크를 구성 하는 방법을 살펴보았습니다. 또한 시스템의 기존 역할을 나열 하 고 새 역할을 만들고 기존 역할을 삭제할 수 있는 웹 페이지를 만들었습니다. 이후 자습서에서는 사용자를 역할에 할당 하는 방법 및 역할 기반 권한 부여를 적용 하는 방법을 알아봅니다.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 정보

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 2.0의 멤버 자격, 역할 및 프로필 검사](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [방법: ASP.NET 2.0에서 역할 관리자 사용](https://msdn.microsoft.com/library/ms998314.aspx)
- [역할 공급자](https://msdn.microsoft.com/library/aa478950.aspx)
- [웹 사이트 관리 도구 롤링](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [`<roleManager>` 요소에 대 한 기술 설명서](https://msdn.microsoft.com/library/ms164660.aspx)
- [멤버 자격 및 역할 관리자 Api 사용](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/security/membership.aspx)

### <a name="about-the-author"></a>작성자 정보

Scott Mitchell는 여러 ASP/ASP. NET books의 작성자와 4GuysFromRolla.com의 창립자가 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 *[24 시간 이내에 ASP.NET 2.0을 sams teach yourself](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 것입니다. Scott은 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) 또는 [http://ScottOnWriting.NET](http://scottonwriting.net/)의 블로그를 통해 연결할 수 있습니다.

### <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서에 대 한 리드 검토자는 Alicja Maziarz, Suchi Banerjee 및 Teresa Murphy를 포함 합니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) 에 줄을 놓습니다.

> [!div class="step-by-step"]
> [이전](role-based-authorization-cs.md)
> [다음](assigning-roles-to-users-vb.md)
