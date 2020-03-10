---
uid: web-forms/overview/older-versions-security/admin/unlocking-and-approving-user-accounts-vb
title: 사용자 계정 잠금 해제 및 승인 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 관리자가 사용자의 잠금 및 승인 된 상태를 관리할 수 있는 웹 페이지를 빌드하는 방법을 보여 줍니다. 새 사용자를 승인 하는 방법도 확인할 예정입니다.
ms.author: riande
ms.date: 04/01/2008
ms.assetid: 041854a5-ea8c-4de0-82f1-121ba6cb2893
msc.legacyurl: /web-forms/overview/older-versions-security/admin/unlocking-and-approving-user-accounts-vb
msc.type: authoredcontent
ms.openlocfilehash: 4a7474676b8f502c583e226678de2b275e0ea3c7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517733"
---
# <a name="unlocking-and-approving-user-accounts-vb"></a>사용자 계정 잠금 해제 및 승인(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/VB.14.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial14_UnlockAndApprove_vb.pdf)

> 이 자습서에서는 관리자가 사용자의 잠금 및 승인 된 상태를 관리할 수 있는 웹 페이지를 빌드하는 방법을 보여 줍니다. 전자 메일 주소를 확인 한 후에만 새 사용자를 승인 하는 방법도 확인할 수 있습니다.

## <a name="introduction"></a>소개

사용자 이름, 암호 및 메일과 함께 각 사용자 계정에는 사용자가 사이트에 로그인 할 수 있는지 여부를 결정 하는 두 개의 상태 필드인 잠금 및 승인이 있습니다. 지정 된 시간 (분) 내에 지정 된 횟수 만큼 잘못 된 자격 증명을 제공 하는 경우 사용자가 자동으로 잠깁니다. 기본 설정은 10 분 이내에 잘못 된 로그인을 5 번 시도한 후 사용자를 잠급니다. 승인 됨 상태는 새 사용자가 사이트에 로그온 할 수 있게 되기 전에 일부 작업을 수행 해야 하는 경우에 유용 합니다. 예를 들어 사용자는 먼저 전자 메일 주소를 확인 하거나 관리자가 승인을 받아야 로그인 할 수 있습니다.

잠긴 사용자 또는 승인 되지 않은 사용자는 로그인 할 수 없기 때문에 이러한 상태를 다시 설정할 수 있는 방법에 대해서만 궁금해 합니다. ASP.NET에는 사용자의 잠금 및 승인 된 상태를 관리 하기 위한 기본 제공 기능이 나 웹 컨트롤이 포함 되지 않습니다. 이러한 결정은 사이트 별로 처리 되어야 하기 때문입니다. 일부 사이트에서는 모든 새 사용자 계정 (기본 동작)을 자동으로 승인할 수 있습니다. 다른 사용자는 관리자가 새 계정을 승인 하거나 등록 시 제공 된 전자 메일 주소로 전송 된 링크를 방문할 때까지 사용자를 승인 하지 않습니다. 마찬가지로, 일부 사이트는 관리자가 자신의 상태를 다시 설정할 때까지 사용자를 잠글 수 있으며, 다른 사이트는 잠긴 사용자에 게 계정을 잠금 해제 하기 위해 방문할 수 있는 URL을 사용 하 여 전자 메일을 보냅니다.

이 자습서에서는 관리자가 사용자의 잠금 및 승인 된 상태를 관리할 수 있는 웹 페이지를 빌드하는 방법을 보여 줍니다. 전자 메일 주소를 확인 한 후에만 새 사용자를 승인 하는 방법도 확인할 수 있습니다.

## <a name="step-1-managing-users-locked-out-and-approved-statuses"></a>1 단계: 사용자의 잠금 및 승인 된 상태 관리

인터페이스를 <a id="Tutorial12"> </a> [*빌드하여 여러 자습서에서 하나의 사용자 계정을 선택*](building-an-interface-to-select-one-user-account-from-many-vb.md) 하 고 필터링 된 GridView에서 각 사용자 계정에 나열 된 페이지를 만들었습니다. 표에는 각 사용자의 이름과 전자 메일, 승인 된 상태 및 잠긴 상태, 현재 온라인 상태 인지 여부 및 사용자에 대 한 의견이 나열 됩니다. 사용자의 승인 및 잠긴 상태를 관리 하기 위해이 표를 편집할 수 있도록 설정할 수 있습니다. 사용자의 승인 됨 상태를 변경 하기 위해 관리자는 먼저 사용자 계정을 찾은 다음 해당 GridView 행을 편집 하 여 승인 된 확인란을 선택 하거나 선택 취소 합니다. 또는 별도의 ASP.NET 페이지를 통해 승인 및 잠금 상태를 관리할 수 있습니다.

이 자습서에서는 `ManageUsers.aspx` 및 `UserInformation.aspx`의 두 ASP.NET 페이지를 사용 합니다. 여기서의 개념은 `ManageUsers.aspx`는 시스템의 사용자 계정을 나열 하는 반면, `UserInformation.aspx`를 사용 하면 관리자가 특정 사용자에 대해 승인 및 잠금 상태를 관리할 수 있습니다. 첫 번째 비즈니스 순서는 링크의 열로 렌더링 되는 하이퍼링크 필드를 포함 하도록 `ManageUsers.aspx`에서 GridView를 확대 하는 것입니다. 각 링크에서 `UserInformation.aspx?user=UserName`를 가리키도록 하려고 합니다. 여기서 *UserName* 은 편집할 사용자의 이름입니다.

> [!NOTE]
> <a id="Tutorial13"> </a> [*암호 복구 및 변경*](recovering-and-changing-passwords-vb.md) 에 대 한 코드를 다운로드 한 경우에는 `ManageUsers.aspx` 페이지에 이미 "관리" 링크 집합이 포함 되어 있고 `UserInformation.aspx` 페이지에서 선택한 사용자의 암호를 변경 하기 위한 인터페이스를 제공 하는 것을 알 수 있습니다. 이 자습서와 관련 된 코드에서 해당 기능을 복제 하지 않기로 결정 했습니다. 멤버 자격 API를 우회 하 고 사용자 암호를 변경 하기 위해 SQL Server 데이터베이스와 직접 작동 하기 때문입니다. 이 자습서는 `UserInformation.aspx` 페이지를 사용 하 여 처음부터 시작 됩니다.

### <a name="adding-manage-links-to-theuseraccountsgridview"></a>`UserAccounts`GridView에 "관리" 링크 추가

`ManageUsers.aspx` 페이지를 열고 `UserAccounts` GridView에 하이퍼링크 필드를 추가 합니다. 하이퍼링크 필드의 `Text` 속성을 "Manage"로 설정 하 고 해당 `DataNavigateUrlFields` 및 `DataNavigateUrlFormatString` 속성을 `UserName` 및 "UserInformation .aspx? user ={0}"로 설정 합니다. 이러한 설정은 하이퍼링크의 모든 하이퍼링크가 "관리" 텍스트를 표시 하지만 각 링크가 적절 한 *사용자 이름* 값을 querystring에 전달 하도록 하이퍼링크 필드를 구성 합니다.

하이퍼링크 필드를 GridView에 추가한 후 브라우저를 통해 `ManageUsers.aspx` 페이지를 봅니다. 그림 1에 나와 있는 것 처럼 각 GridView 행은 이제 "관리" 링크를 포함 합니다. Bruce의 "관리" 링크는 `UserInformation.aspx?user=Bruce`를 가리키며, Dave의 "관리" 링크는 `UserInformation.aspx?user=Dave`를 가리킵니다.

[하이퍼링크 필드 ![에 추가](unlocking-and-approving-user-accounts-vb/_static/image2.png)](unlocking-and-approving-user-accounts-vb/_static/image1.png)

**그림 1**: 하이퍼링크 필드에 각 사용자 계정에 대 한 "관리" 링크가 추가 됩니다 ([전체 크기 이미지를 보려면 클릭](unlocking-and-approving-user-accounts-vb/_static/image3.png)).

잠시 후 `UserInformation.aspx` 페이지에 대 한 사용자 인터페이스 및 코드를 만들지만 먼저 사용자의 잠긴 상태와 승인 된 상태를 프로그래밍 방식으로 변경 하는 방법에 대해 알아보겠습니다. [`MembershipUser` 클래스](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx) 에는 [`IsLockedOut`](https://msdn.microsoft.com/library/system.web.security.membershipuser.islockedout.aspx) 및 [`IsApproved` 속성이](https://msdn.microsoft.com/library/system.web.security.membershipuser.isapproved.aspx)있습니다. `IsLockedOut` 속성은 읽기 전용입니다. 사용자를 프로그래밍 방식으로 잠그는 메커니즘이 없습니다. 사용자의 잠금을 해제 하려면 `MembershipUser` 클래스의 [`UnlockUser` 메서드](https://msdn.microsoft.com/library/system.web.security.membershipuser.unlockuser.aspx)를 사용 합니다. `IsApproved` 속성은 읽고 쓸 수 있습니다. 이 속성에 대 한 변경 내용을 저장 하려면 `Membership` 클래스의 [`UpdateUser` 메서드](https://msdn.microsoft.com/library/system.web.security.membership.updateuser.aspx)를 호출 하 여 수정 된 `MembershipUser` 개체를 전달 해야 합니다.

`IsApproved` 속성은 읽고 쓸 수 있기 때문에 CheckBox 컨트롤은이 속성을 구성 하는 데 가장 적합 한 사용자 인터페이스 요소입니다. 그러나 관리자는 사용자를 잠글 수 없고 사용자만 잠금을 해제할 수 있으므로 `IsLockedOut` 속성에는 CheckBox가 작동 하지 않습니다. `IsLockedOut` 속성에 적합 한 사용자 인터페이스는 클릭 하면 사용자 계정의 잠금을 해제 하는 단추입니다. 사용자가 잠겨 있는 경우에만이 단추를 사용 하도록 설정 해야 합니다.

### <a name="creating-theuserinformationaspxpage"></a>`UserInformation.aspx`페이지 만들기

이제 `UserInformation.aspx`사용자 인터페이스를 구현할 준비가 되었습니다. 이 페이지를 열고 다음 웹 컨트롤을 추가 합니다.

- 클릭 하면 관리자를 `ManageUsers.aspx` 페이지로 반환 하는 HyperLink 컨트롤입니다.
- 선택한 사용자의 이름을 표시 하기 위한 레이블 웹 컨트롤입니다. 이 레이블의 `ID` `UserNameLabel` 설정 하 고 Text 속성을 지웁니다.
- `IsApproved`이름이 지정 된 CheckBox 컨트롤입니다. `AutoPostBack` 속성을 `True`로 설정 합니다.
- 사용자의 마지막으로 잠긴 날짜를 표시 하는 레이블 컨트롤입니다. 이 레이블의 이름을 `LastLockedOutDateLabel` 하 고 `Text` 속성을 지웁니다.
- 사용자를 잠금 해제 하는 단추입니다. 이 단추의 이름을 `UnlockUserButton` 하 고 `Text` 속성을 "사용자 잠금 해제"로 설정 합니다.
- "사용자의 승인 됨 상태가 업데이트 되었습니다."와 같은 상태 메시지를 표시 하는 레이블 컨트롤입니다. 이 컨트롤의 이름을 `StatusMessage`하 고 `Text` 속성의 선택을 취소 한 다음 `CssClass` 속성을 `Important`로 설정 합니다. `Important` CSS 클래스는 `Styles.css` 스타일 시트 파일에 정의 되어 있으며, 해당 텍스트를 크게, 빨간색 글꼴로 표시 합니다.)

이러한 컨트롤을 추가한 후에는 Visual Studio의 디자인 뷰 그림 2의 스크린샷 처럼 표시 됩니다.

[UserInformation .aspx의 사용자 인터페이스를 만들 ![](unlocking-and-approving-user-accounts-vb/_static/image5.png)](unlocking-and-approving-user-accounts-vb/_static/image4.png)

**그림 2**: `UserInformation.aspx`에 대 한 사용자 인터페이스 만들기 ([전체 크기 이미지를 보려면 클릭](unlocking-and-approving-user-accounts-vb/_static/image6.png))

사용자 인터페이스가 완료 되 면 다음 작업은 선택한 사용자의 정보에 따라 `IsApproved` 확인란 및 기타 컨트롤을 설정 하는 것입니다. 페이지의 `Load` 이벤트에 대 한 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-vb[Main](unlocking-and-approving-user-accounts-vb/samples/sample1.vb)]

위의 코드는 나중에 다시 게시 하지 않고 페이지를 처음 방문 하는 것을 확인 하 여 시작 합니다. 그런 다음 `user` querystring 필드를 통해 전달 된 사용자 이름을 읽고 `Membership.GetUser(username)` 메서드를 통해 해당 사용자 계정에 대 한 정보를 검색 합니다. Querystring을 통해 사용자 이름을 제공 하지 않거나 지정 된 사용자를 찾을 수 없는 경우 관리자가 `ManageUsers.aspx` 페이지로 다시 전송 됩니다.

그러면 `MembershipUser` 개체의 `UserName` 값이 `UserNameLabel`에 표시 되 고 `IsApproved` 확인란이 `IsApproved` 속성 값을 기준으로 검사 됩니다.

`MembershipUser` 개체의 [`LastLockoutDate` 속성](https://msdn.microsoft.com/library/system.web.security.membershipuser.lastlockoutdate.aspx) 은 사용자가 마지막으로 잠긴 경우를 나타내는 `DateTime` 값을 반환 합니다. 사용자가 잠긴 적이 없는 경우 반환 되는 값은 멤버 자격 공급자에 따라 달라 집니다. 새 계정을 만들면 `SqlMembershipProvider` `aspnet_Membership` 테이블의 `LastLockoutDate` 필드가 `1754-01-01 12:00:00 AM`로 설정 됩니다. 위의 코드는 `LastLockoutDate` 속성이 2000 년 이전에 발생 하는 경우 `LastLockoutDateLabel`에 빈 문자열을 표시 합니다. 그렇지 않으면 `LastLockoutDate` 속성의 날짜 부분이 레이블에 표시 됩니다. `UnlockUserButton`의 `Enabled` 속성은 사용자의 잠긴 상태로 설정 됩니다. 즉, 사용자가 잠겨 있는 경우에만이 단추를 사용할 수 있습니다.

잠시 시간을 사용 하 여 브라우저를 통해 `UserInformation.aspx` 페이지를 테스트 합니다. 물론, `ManageUsers.aspx`에서 시작 하 고 관리할 사용자 계정을 선택 해야 합니다. `UserInformation.aspx`도착할 때 `IsApproved` 확인란은 사용자가 승인 된 경우에만 확인 됩니다. 사용자가 잠긴 적이 있으면 마지막으로 잠긴 날짜가 표시 됩니다. 사용자 잠금 해제 단추는 사용자가 현재 잠겨 있는 경우에만 사용할 수 있습니다. `IsApproved` 확인란을 선택 하거나 선택 취소 하거나 사용자 잠금 해제 단추를 클릭 하면 포스트백이 발생 하지만 해당 이벤트에 대 한 이벤트 처리기를 아직 만들지 않았으므로 사용자 계정이 수정 되지 않습니다.

Visual Studio로 돌아가서 `IsApproved` CheckBox의 `CheckedChanged` 이벤트와 `UnlockUser` 단추의 `Click` 이벤트에 대 한 이벤트 처리기를 만듭니다. `CheckedChanged` 이벤트 처리기에서 사용자의 `IsApproved` 속성을 확인란의 `Checked` 속성으로 설정 하 고 `Membership.UpdateUser`에 대 한 호출을 통해 변경 내용을 저장 합니다. `Click` 이벤트 처리기에서 `MembershipUser` 개체의 `UnlockUser` 메서드를 호출 하기만 하면 됩니다. 두 이벤트 처리기의 `StatusMessage` 레이블에 적절 한 메시지를 표시 합니다.

[!code-vb[Main](unlocking-and-approving-user-accounts-vb/samples/sample2.vb)]

### <a name="testing-theuserinformationaspxpage"></a>`UserInformation.aspx`페이지 테스트

이러한 이벤트 처리기를 사용 하 여 페이지를 다시 방문 하 고 사용자를 승인 하지 않았습니다. 그림 3에 나와 있는 것 처럼 사용자의 `IsApproved` 속성이 성공적으로 수정 되었음을 나타내는 간략 한 메시지가 페이지에 표시 됩니다.

[![Chris가 승인 되지 않음](unlocking-and-approving-user-accounts-vb/_static/image8.png)](unlocking-and-approving-user-accounts-vb/_static/image7.png)

**그림 3**: Chris가 승인 되지 않음 ([전체 크기 이미지를 보려면 클릭](unlocking-and-approving-user-accounts-vb/_static/image9.png))

다음으로, 로그 아웃 하 고 계정이 방금 승인 되지 않은 사용자로 로그인을 시도 합니다. 사용자가 승인 되지 않았기 때문에 로그인 할 수 없습니다. 기본적으로 사용자가 로그인 할 수 없는 경우에는 사용자가 로그인 할 수 없는 경우에도 로그인 컨트롤이 동일한 메시지를 표시 합니다. <a id="Tutorial6"> </a>그러나 [*멤버 자격 사용자 저장소에 대 한 사용자 자격 증명 유효성 검사*](../membership/validating-user-credentials-against-the-membership-user-store-vb.md) 자습서에서는 더 적절 한 메시지를 표시 하도록 로그인 컨트롤을 개선 하는 방법을 살펴보았습니다. 그림 4와 같이 Chris는 계정이 아직 승인 되지 않았기 때문에 로그인 할 수 없음을 설명 하는 메시지를 표시 합니다.

[계정이 승인 되지 않았으므로 ![Chris에 게 로그인 할 수 없습니다.](unlocking-and-approving-user-accounts-vb/_static/image11.png)](unlocking-and-approving-user-accounts-vb/_static/image10.png)

**그림 4**: 계정이 승인 되지 않아 로그인 할 수 없음 ([전체 크기 이미지를 보려면 클릭](unlocking-and-approving-user-accounts-vb/_static/image12.png))

잠긴 기능을 테스트 하려면 승인 된 사용자로 로그인을 시도 하지만 잘못 된 암호를 사용 합니다. 사용자 계정이 잠길 때까지이 프로세스를 필요한 횟수 만큼 반복 합니다. 잠긴 계정에서 로그인을 시도 하는 경우 사용자 지정 메시지를 표시 하도록 로그인 제어도 업데이트 되었습니다. 로그인 페이지에서 다음과 같은 메시지가 표시 되기 시작 하면 계정이 잠긴 것을 알 수 있습니다. "잘못 된 로그인 시도 횟수가 너무 많아 계정이 잠겼습니다. 계정을 잠금 해제 하려면 관리자에 게 문의 하세요. "

`ManageUsers.aspx` 페이지로 돌아가 잠긴 사용자에 대 한 관리 링크를 클릭 합니다. 그림 5와 같이 사용자 잠금 해제 단추를 사용 하도록 설정 해야 `LastLockedOutDateLabel`에 값이 표시 됩니다. 사용자 잠금 해제 단추를 클릭 하 여 사용자 계정의 잠금을 해제 합니다. 사용자를 잠금 해제 한 후에는 다시 로그인 할 수 있습니다.

[![Dave가 시스템에서 잠겼습니다.](unlocking-and-approving-user-accounts-vb/_static/image14.png)](unlocking-and-approving-user-accounts-vb/_static/image13.png)

**그림 5**: Dave가 시스템에서 잠겨 있음 ([전체 크기 이미지를 보려면 클릭](unlocking-and-approving-user-accounts-vb/_static/image15.png))

## <a name="step-2-specifying-new-users-approved-status"></a>2 단계: 새 사용자의 승인 된 상태 지정

승인 됨 상태는 새 사용자가 로그인 하 고 사이트의 사용자 관련 기능에 액세스할 수 있도록 하기 위해 일부 작업을 수행 하려는 경우에 유용 합니다. 예를 들어 로그인 및 등록 페이지를 제외한 모든 페이지에는 인증 된 사용자만 액세스할 수 있는 개인 웹 사이트를 실행할 수 있습니다. 그러나 웹 사이트가 웹 사이트에 도달 하면 어떻게 되나요? 등록 페이지를 찾고 계정을 만들 까 요? 이러한 상황이 발생 하지 않도록 하려면 등록 페이지를 `Administration` 폴더로 이동한 후 관리자가 각 계정을 수동으로 만들어야 합니다. 또는 누구나 등록 하도록 허용할 수 있지만 관리자가 사용자 계정을 승인할 때까지 사이트 액세스를 금지 합니다.

기본적으로 CreateUserWizard 컨트롤은 새 계정을 승인 합니다. 컨트롤의 [`DisableCreatedUser` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.disablecreateduser.aspx)을 사용 하 여이 동작을 구성할 수 있습니다. 새 사용자 계정을 승인 하지 않으려면이 속성을 `True`로 설정 합니다.

> [!NOTE]
> 기본적으로 CreateUserWizard 컨트롤은 새 사용자 계정에 자동으로 기록 합니다. 이 동작은 컨트롤의 [`LoginCreatedUser` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.logincreateduser.aspx)에 의해 결정 됩니다. 승인 되지 않은 사용자가 사이트에 로그인 할 수 없기 때문에 `DisableCreatedUser` `True` 경우 `LoginCreatedUser` 속성의 값에 관계 없이 새 사용자 계정이 사이트에 기록 되지 않습니다.

`Membership.CreateUser` 메서드를 통해 프로그래밍 방식으로 새 사용자 계정을 만드는 경우 승인 되지 않은 사용자 계정을 만들려면 새 사용자의 `IsApproved` 속성 값을 입력 매개 변수로 허용 하는 오버 로드 중 하나를 사용 합니다.

## <a name="step-3-approving-users-by-verifying-their-email-address"></a>3 단계: 전자 메일 주소를 확인 하 여 사용자 승인

사용자 계정을 지 원하는 대부분의 웹 사이트는 등록할 때 제공 된 전자 메일 주소를 확인할 때까지 새 사용자를 승인 하지 않습니다. 이 확인 프로세스는 고유 하 고 검증 된 전자 메일 주소가 필요 하 고 등록 프로세스에 추가 단계를 추가 하기 때문에 일반적으로 봇, 스팸 메일을 차단 하는 데 사용 됩니다. 이 모델을 사용 하면 새 사용자가 등록할 때 확인 페이지에 대 한 링크가 포함 된 전자 메일 메시지가 전송 됩니다. 사용자는 링크를 방문 하 여 전자 메일을 수신 했으며 제공 된 전자 메일 주소가 유효한 지를 입증 했습니다. 확인 페이지는 사용자 승인을 담당 합니다. 이는 자동으로 발생할 수 있으므로이 페이지에 도달 하는 모든 사용자를 승인 하거나 [CAPTCHA](http://en.wikipedia.org/wiki/Captcha)등의 추가 정보를 제공 하는 사용자만 승인 합니다.

이 워크플로를 수용 하려면 새 사용자가 승인 되지 않도록 먼저 계정 만들기 페이지를 업데이트 해야 합니다. `Membership` 폴더에서 `EnhancedCreateUserWizard.aspx` 페이지를 열고 CreateUserWizard 컨트롤의 `DisableCreatedUser` 속성을 `True`로 설정 합니다.

다음으로, 계정을 확인 하는 방법에 대 한 지침이 포함 된 전자 메일을 새 사용자에 게 보내도록 CreateUserWizard 컨트롤을 구성 해야 합니다. 특히 querystring을 통해 새 사용자의 `UserId`를 전달 하는 `Verification.aspx` 페이지에 대 한 전자 메일의 링크를 포함 합니다. `Verification.aspx` 페이지는 지정 된 사용자를 조회 하 고 승인 된 것으로 표시 합니다.

### <a name="sending-a-verification-email-to-new-users"></a>새 사용자에 게 확인 메일 보내기

CreateUserWizard 컨트롤에서 전자 메일을 보내려면 해당 `MailDefinition` 속성을 적절 하 게 구성 합니다. <a id="Tutorial13"> </a> [이전 자습서](recovering-and-changing-passwords-vb.md)에서 설명한 대로 ChangePassword 및 passwordrecovery 컨트롤에는 CreateUserWizard 컨트롤의 경우와 동일한 방식으로 작동 하는 [`MailDefinition` 속성이](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.maildefinition.aspx) 포함 되어 있습니다.

> [!NOTE]
> `MailDefinition` 속성을 사용 하려면 `Web.config`에서 메일 배달 옵션을 지정 해야 합니다. 자세한 내용은 [ASP.NET에서 전자 메일 보내기](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)를 참조 하세요.

먼저 `EmailTemplates` 폴더에 `CreateUserWizard.txt` 라는 새 전자 메일 템플릿을 만듭니다. 템플릿에 다음 텍스트를 사용 합니다.

[!code-aspx[Main](unlocking-and-approving-user-accounts-vb/samples/sample3.aspx)]

`MailDefinition`의 `BodyFileName` 속성을 "~/EmailTemplates/CreateUserWizard.txt"로 설정 하 고 해당 `Subject` 속성을 "웹 사이트를 시작 합니다. 계정을 활성화 하세요. "

`CreateUserWizard.txt` 전자 메일 템플릿에는 `<%VerificationUrl%>` 자리 표시 자가 포함 되어 있습니다. `Verification.aspx` 페이지에 대 한 URL이 배치 됩니다. CreateUserWizard는 `<%UserName%>` 및 `<%Password%>` 자리 표시자를 새 계정의 사용자 이름 및 암호로 자동으로 대체 하지만 기본 제공 `<%VerificationUrl%>` 자리 표시 자가 없습니다. 적절 한 확인 URL로 수동으로 바꾸어야 합니다.

이 작업을 수행 하려면 CreateUserWizard의 [`SendingMail` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.sendingmail.aspx) 에 대 한 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-vb[Main](unlocking-and-approving-user-accounts-vb/samples/sample4.vb)]

`SendingMail` 이벤트는 `CreatedUser` 이벤트 후에 발생 합니다. 즉, 위의 이벤트 처리기가 실행 될 때 새 사용자 계정이 이미 생성 된 시간입니다. CreateUserWizard 컨트롤에 입력 된 `UserName`를 전달 하 여 `Membership.GetUser` 메서드를 호출 하 여 새 사용자의 `UserId` 값에 액세스할 수 있습니다. 그런 다음 확인 URL이 구성 됩니다. `Request.Url.GetLeftPart(UriPartial.Authority)` 문은 URL의 `http://yourserver.com` 부분을 반환 합니다. `Request.ApplicationPath`는 응용 프로그램이 루 팅 된 경로를 반환 합니다. 그런 다음 확인 URL은 `Verification.aspx?ID=userId`로 정의 됩니다. 그러면이 두 문자열이 연결 되어 전체 URL을 형성 합니다. 마지막으로, 전자 메일 메시지 본문 (`e.Message.Body`)은 전체 URL로 바뀐 `<%VerificationUrl%>`를 모두 포함 합니다.

결과적으로 새 사용자는 승인 되지 않으므로 사이트에 로그인 할 수 없습니다. 또한 확인 URL에 대 한 링크가 포함 된 전자 메일을 자동으로 보냅니다 (그림 6 참조).

[새 사용자 ![확인 URL에 대 한 링크가 포함 된 전자 메일을 받습니다.](unlocking-and-approving-user-accounts-vb/_static/image17.png)](unlocking-and-approving-user-accounts-vb/_static/image16.png)

**그림 6**: 새 사용자는 확인 URL에 대 한 링크가 포함 된 전자 메일을 받습니다 ([전체 크기 이미지를 보려면 클릭](unlocking-and-approving-user-accounts-vb/_static/image18.png)).

> [!NOTE]
> CreateUserWizard 컨트롤의 default CreateUserWizard step은 사용자 계정이 생성 되었음을 알리는 메시지를 표시 하 고 계속 단추를 표시 합니다. 이 단추를 클릭 하면 사용자가 컨트롤의 `ContinueDestinationPageUrl` 속성에 지정 된 URL로 이동 합니다. `EnhancedCreateUserWizard.aspx`의 CreateUserWizard는 새 사용자를 `~/Membership/AdditionalUserInfo.aspx`에 보내도록 구성 되며,이를 통해 사용자에 게 출생지, 홈페이지 URL 및 서명을 입력 하 라는 메시지가 표시 됩니다. 이 정보는 로그온 한 사용자만 추가할 수 있으므로이 속성을 업데이트 하 여 사용자를 사이트 홈페이지 (`~/Default.aspx`)로 다시 전송 하는 것이 좋습니다. 또한 `EnhancedCreateUserWizard.aspx` 페이지 또는 CreateUserWizard 단계를 확대 하 여 사용자에 게 확인 전자 메일을 보냈는지 알리고이 메일의 지침을 따를 때까지 계정이 활성화 되지 않도록 해야 합니다. 이러한 수정 사항을 판독기에 대 한 연습으로 남겨 둡니다.

### <a name="creating-the-verification-page"></a>확인 페이지 만들기

최종 작업은 `Verification.aspx` 페이지를 만드는 것입니다. 이 페이지를 루트 폴더에 추가 하 고 `Site.master` 마스터 페이지와 연결 합니다. 대부분의 이전 콘텐츠 페이지를 사이트에 추가 하 고 나면 콘텐츠 페이지에서 마스터 페이지의 기본 콘텐츠를 사용 하도록 `LoginContent` ContentPlaceHolder를 참조 하는 콘텐츠 컨트롤을 제거 합니다.

레이블 웹 컨트롤을 `Verification.aspx` 페이지에 추가 하 고 해당 `ID`를 `StatusMessage`로 설정 하 고 text 속성을 지웁니다. 다음으로 `Page_Load` 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-vb[Main](unlocking-and-approving-user-accounts-vb/samples/sample5.vb)]

위의 코드를 대량으로 사용 하면 querystring을 통해 제공 된 UserId가 있는지, 유효한 `Guid` 값인지, 기존 사용자 계정을 참조 하는지 확인 합니다. 이러한 검사를 모두 통과 하면 사용자 계정이 승인 됩니다. 그렇지 않으면 적절 한 상태 메시지가 표시 됩니다.

그림 7에는 브라우저를 통해 방문할 때 `Verification.aspx` 페이지가 표시 됩니다.

[이제 새 사용자의 계정이 승인 ![](unlocking-and-approving-user-accounts-vb/_static/image20.png)](unlocking-and-approving-user-accounts-vb/_static/image19.png)

**그림 7**: 이제 새 사용자의 계정이 승인 되었습니다 ([전체 크기 이미지를 보려면 클릭](unlocking-and-approving-user-accounts-vb/_static/image21.png)).

## <a name="summary"></a>요약

모든 멤버 자격 사용자 계정에는 사용자가 사이트에 로그인 할 수 있는지 여부를 결정 하는 두 가지 상태 (`IsLockedOut` 및 `IsApproved`가 있습니다. 사용자가 로그인 하려면 이러한 두 속성을 모두 `True` 해야 합니다.

사용자의 잠긴 상태는 무차별 암호 대입 방법을 통해 해커의 사이트로 손상 될 가능성을 줄이기 위해 보안 조치로 사용 됩니다. 구체적으로 말하면 특정 기간 내에 잘못 된 로그인 시도가 특정 횟수를 초과 하는 경우 사용자가 잠깁니다. 이러한 범위는 `Web.config`의 멤버 자격 공급자 설정을 통해 구성할 수 있습니다.

승인 됨 상태는 일반적으로 일부 작업이 의심할 때까지 새 사용자가 로그인 하지 못하도록 하는 수단으로 사용 됩니다. 아마도 사이트에서 먼저 관리자가 새 계정을 승인 하거나 3 단계에서 살펴본 대로 전자 메일 주소를 확인 하 여 새 계정을 승인 해야 할 수 있습니다.

행복 한 프로그래밍

### <a name="about-the-author"></a>저자 정보

Scott Mitchell는 여러 ASP/ASP. NET books의 작성자와 4GuysFromRolla.com의 창립자가 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 *[24 시간 이내에 ASP.NET 2.0을 sams teach yourself](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 것입니다. Scott은 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) 또는 [http://ScottOnWriting.NET](http://scottonwriting.net/)의 블로그를 통해 연결할 수 있습니다.

### <a name="special-thanks-to"></a>특별 해 주셔서 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) 에 줄을 놓습니다.

> [!div class="step-by-step"]
> [이전](recovering-and-changing-passwords-vb.md)
