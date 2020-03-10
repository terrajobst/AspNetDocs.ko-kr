---
uid: web-forms/overview/older-versions-security/membership/storing-additional-user-information-cs
title: 추가 사용자 정보 저장 (C#) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 매우 기본적인 방명록 응용 프로그램을 빌드하여이 질문에 대 한 답변을 제공 합니다. 이 작업을 수행 하는 동안 modeli에 대해 다른 옵션을 살펴보겠습니다.
ms.author: riande
ms.date: 01/18/2008
ms.assetid: 1642132a-1ca5-4872-983f-ab59fc8865d3
msc.legacyurl: /web-forms/overview/older-versions-security/membership/storing-additional-user-information-cs
msc.type: authoredcontent
ms.openlocfilehash: 24b96e86bc93e03d2639b73e35ed1fd1271bac5a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515459"
---
# <a name="storing-additional-user-information-c"></a>추가 사용자 정보 저장(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_08_CS.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial08_ExtraUserInfo_cs.pdf)

> 이 자습서에서는 매우 기본적인 방명록 응용 프로그램을 빌드하여이 질문에 대 한 답변을 제공 합니다. 이 작업을 수행 하는 경우 데이터베이스에서 사용자 정보를 모델링 하는 다양 한 옵션을 살펴본 다음이 데이터를 멤버 프레임 프레임 워크에서 만든 사용자 계정에 연결 하는 방법을 확인 합니다.

## <a name="introduction"></a>소개

ASP. NET의 멤버 자격 프레임 워크는 사용자를 관리 하기 위한 유연한 인터페이스를 제공 합니다. 멤버 자격 API는 자격 증명의 유효성을 검사 하 고, 현재 로그온 한 사용자에 대 한 정보를 검색 하 고, 새 사용자 계정을 만들고, 사용자 계정을 삭제 하는 메서드를 포함 합니다. 멤버 자격 프레임 워크의 각 사용자 계정에는 자격 증명의 유효성을 검사 하 고 필수 사용자 계정 관련 작업을 수행 하는 데 필요한 속성만 포함 됩니다. 이는 멤버 자격 프레임 워크의 사용자 계정을 모델링 하는 [`MembershipUser` 클래스](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)의 메서드 및 속성에 의해 복합적 됩니다. 이 클래스에는 [`UserName`](https://msdn.microsoft.com/library/system.web.security.membershipuser.username.aspx), [`Email`](https://msdn.microsoft.com/library/system.web.security.membershipuser.email.aspx)및 [`IsLockedOut`](https://msdn.microsoft.com/library/system.web.security.membershipuser.islockedout.aspx)와 같은 속성과 [`GetPassword`](https://msdn.microsoft.com/library/system.web.security.membershipuser.getpassword.aspx) 및 [`UnlockUser`](https://msdn.microsoft.com/library/system.web.security.membershipuser.unlockuser.aspx)같은 메서드가 있습니다.

응용 프로그램에서 멤버 자격 프레임 워크에 포함 되지 않은 추가 사용자 정보를 저장 해야 하는 경우가 종종 있습니다. 예를 들어 온라인 대리점에서 각 사용자에 게 배송 및 대금 청구 주소, 지불 정보, 배달 기본 설정 및 연락처 전화 번호를 저장 하도록 허용 해야 할 수 있습니다. 또한 시스템의 각 순서는 특정 사용자 계정에 연결 됩니다.

`MembershipUser` 클래스는 `PhoneNumber` 또는 `DeliveryPreferences` 또는 `PastOrders`같은 속성을 포함 하지 않습니다. 응용 프로그램에 필요한 사용자 정보를 추적 하 고 멤버 자격 프레임 워크와 통합 하려면 어떻게 해야 하나요? 이 자습서에서는 매우 기본적인 방명록 응용 프로그램을 빌드하여이 질문에 대 한 답변을 제공 합니다. 이 작업을 수행 하는 경우 데이터베이스에서 사용자 정보를 모델링 하는 다양 한 옵션을 살펴본 다음이 데이터를 멤버 프레임 프레임 워크에서 만든 사용자 계정에 연결 하는 방법을 확인 합니다. 이제 시작하겠습니다.

## <a name="step-1-creating-the-guestbook-applications-data-model"></a>1 단계: 방명록 응용 프로그램의 데이터 모델 만들기

데이터베이스에서 사용자 정보를 캡처하여 멤버 자격 프레임 워크에서 만든 사용자 계정에 연결 하는 데 사용할 수 있는 다양 한 기술이 있습니다. 이러한 기술을 보여 주기 위해 자습서 웹 응용 프로그램을 보강 하 여 일종의 사용자 관련 데이터를 캡처하도록 해야 합니다. 현재 응용 프로그램의 데이터 모델에는 `SqlMembershipProvider`에 필요한 응용 프로그램 서비스 테이블만 포함 됩니다.

인증 된 사용자가 주석을 남길 수 있는 매우 간단한 방명록 응용 프로그램을 만들어 보겠습니다. 방명록 메모를 저장 하는 것 외에도 각 사용자가 자신의 집 마을, 홈페이지 및 서명을 저장할 수 있습니다. 제공 된 경우 사용자의 홈 타운, 홈 페이지 및 서명이 방명록에 남아 있는 각 메시지에 표시 됩니다.

### <a name="adding-theguestbookcommentstable"></a>`GuestbookComments`테이블 추가

방명록 주석을 캡처하려면 `CommentId`, `Subject`, `Body`, `CommentDate`등의 열이 있는 `GuestbookComments` 라는 데이터베이스 테이블을 만들어야 합니다. 또한 `GuestbookComments` 테이블의 각 레코드가 주석을 떠난 사용자를 참조 해야 합니다.

이 테이블을 데이터베이스에 추가 하려면 Visual Studio의 데이터베이스 탐색기로 이동 하 여 `SecurityTutorials` 데이터베이스로 드릴 다운 합니다. Tables 폴더를 마우스 오른쪽 단추로 클릭 하 고 새 테이블 추가를 선택 합니다. 그러면 새 테이블의 열을 정의할 수 있는 인터페이스가 나타납니다.

[SecurityTutorials 데이터베이스에 새 테이블을 추가 ![](storing-additional-user-information-cs/_static/image2.png)](storing-additional-user-information-cs/_static/image1.png)

**그림 1**: `SecurityTutorials` 데이터베이스에 새 테이블 추가 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image3.png))

그런 다음 `GuestbookComments`의 열을 정의 합니다. `uniqueidentifier`형식의 `CommentId` 이라는 열을 추가 하 여 시작 합니다. 이 열은 방명록의 각 주석을 고유 하 게 식별 하므로 `NULL` s를 허용 하지 않고 테이블의 기본 키로 표시 합니다. 각 `INSERT`에서 `CommentId` 필드에 값을 제공 하는 대신 열의 기본값을 `NEWID()`로 설정 하 여 `INSERT`의이 필드에 대해 새 `uniqueidentifier` 값이 자동으로 생성 되도록 지정할 수 있습니다. 이 첫 번째 필드를 추가한 후 기본 키로 표시 하 고 설정의 기본값을 설정 하면 화면이 그림 2에 표시 된 화면과 유사 하 게 표시 됩니다.

[CommentId 라는 기본 열을 추가 ![](storing-additional-user-information-cs/_static/image5.png)](storing-additional-user-information-cs/_static/image4.png)

**그림 2**: `CommentId` 이라는 기본 열 추가 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image6.png))

그런 다음 `nvarchar(50)` 형식의 `Subject` 이라는 열을 추가 하 고, `nvarchar(MAX)`형식의 `Body` 이라는 열을 추가 합니다. 두 열 모두에서 `NULL`을 허용 하지 않습니다. 그런 다음 `datetime`형식의 `CommentDate` 이라는 열을 추가 합니다. `NULL` s를 허용 하지 않고 `CommentDate` 열의 기본값을 `getdate()`로 설정 합니다.

사용자 계정을 각 방명록 주석과 연결 하는 열을 추가 하는 것만 남았습니다. 한 가지 옵션은 `nvarchar(256)`형식의 `UserName` 이라는 열을 추가 하는 것입니다. 이는 `SqlMembershipProvider`이외의 멤버 자격 공급자를 사용 하는 경우 적합 한 선택입니다. 그러나이 자습서 시리즈와 같이 `SqlMembershipProvider`사용 하는 경우 `aspnet_Users` 테이블의 `UserName` 열은 고유 하지 않을 수 있습니다. `aspnet_Users` 테이블의 기본 키는 `UserId` 이며 `uniqueidentifier`형식입니다. 따라서 `GuestbookComments` 테이블에 `uniqueidentifier` 형식의 `UserId` 라는 열이 있어야 합니다 (`NULL` 값 허용 안 함). 계속 진행 하 여이 열을 추가 합니다.

> [!NOTE]
> [*SQL Server의 멤버 자격 스키마 만들기*](creating-the-membership-schema-in-sql-server-cs.md) 자습서에서 설명 했 듯이 멤버 자격 프레임 워크는 여러 사용자 계정을 사용 하 여 여러 웹 응용 프로그램에서 동일한 사용자 저장소를 공유할 수 있도록 설계 되었습니다. 사용자 계정을 여러 응용 프로그램으로 분할 하 여이를 수행 합니다. 각 사용자 이름이 응용 프로그램 내에서 고유 하 게 보장 되는 동안 동일한 사용자 저장소를 사용 하는 다른 응용 프로그램에서 동일한 사용자 이름을 사용할 수 있습니다. `UserName` 및 `ApplicationId` 필드의 `aspnet_Users` 테이블에는 복합 `UNIQUE` 제약 조건이 있지만 하나는 `UserName` 필드에만 적용 됩니다. 따라서 aspnet\_사용자 테이블에 동일한 `UserName` 값을 가진 둘 이상의 레코드가 있을 수 있습니다. 그러나 `aspnet_Users` 테이블의 `UserId` 필드에는 기본 키 이므로 `UNIQUE` 제약 조건이 있습니다. `UNIQUE` 제약 조건은 `GuestbookComments`와 `aspnet_Users` 테이블 사이에 foreign key 제약 조건을 설정할 수 없기 때문에 중요 합니다.

`UserId` 열을 추가한 후 도구 모음에서 저장 아이콘을 클릭 하 여 테이블을 저장 합니다. 새 테이블의 이름을 `GuestbookComments`합니다.

`GuestbookComments` 테이블을 사용 하 여에 참석 하는 마지막 문제가 있습니다. `GuestbookComments.UserId` 열과 `aspnet_Users.UserId` 열 사이에 [foreign key 제약 조건을](https://msdn.microsoft.com/library/ms175464.aspx) 만들어야 합니다. 이렇게 하려면 도구 모음에서 관계 아이콘을 클릭 하 여 외래 키 관계 대화 상자를 시작 합니다. 또는 테이블 디자이너 메뉴로 이동 하 고 관계를 선택 하 여이 대화 상자를 시작할 수 있습니다.

외래 키 관계 대화 상자의 왼쪽 아래 모퉁이에 있는 추가 단추를 클릭 합니다. 이렇게 하면 관계에 참여 하는 테이블을 정의 해야 하지만 새 foreign key 제약 조건이 추가 됩니다.

[외래 키 관계 대화 상자를 사용 하 여 테이블의 Foreign Key 제약 조건을 관리할 ![](storing-additional-user-information-cs/_static/image8.png)](storing-additional-user-information-cs/_static/image7.png)

**그림 3**: 외래 키 관계 대화 상자를 사용 하 여 테이블의 Foreign Key 제약 조건 관리 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image9.png))

그런 다음 오른쪽의 "테이블 및 열 사양" 행에서 줄임표 아이콘을 클릭 합니다. 그러면 테이블 및 열 대화 상자가 시작 되며 여기에서 기본 키 테이블 및 열과 `GuestbookComments` 테이블의 외래 키 열을 지정할 수 있습니다. 특히 기본 키 테이블 및 열로 `aspnet_Users` 및 `UserId`를 선택 하 고 `GuestbookComments` 테이블에서 외래 키 열로 `UserId` 합니다 (그림 4 참조). 기본 및 외래 키 테이블 및 열을 정의한 후 확인을 클릭 하 여 외래 키 관계 대화 상자로 돌아갑니다.

[aspnet_Users와 ![된 메모 테이블 사이에 외래 키 제약 조건을 설정 합니다.](storing-additional-user-information-cs/_static/image11.png)](storing-additional-user-information-cs/_static/image10.png)

**그림 4**: `aspnet_Users`와 `GuesbookComments` 테이블 간의 Foreign Key 제약 조건 설정 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image12.png))

이 시점에서 foreign key 제약 조건이 설정 되었습니다. 이 제약 조건이 있으면 존재 하지 않는 사용자 계정을 참조 하는 방명록 항목이 되지 않도록 보장 하 여 두 테이블 간의 [관계 무결성](http://en.wikipedia.org/wiki/Referential_integrity) 을 보장 합니다. 기본적으로 foreign key 제약 조건은 해당 자식 레코드가 있는 경우 부모 레코드를 삭제 하지 못하게 합니다. 즉, 사용자가 하나 이상의 방명록 주석을 만든 다음 해당 사용자 계정을 삭제 하려고 하면 해당 방명록 주석이 먼저 삭제 되지 않는 한 삭제 작업이 실패 합니다.

부모 레코드를 삭제할 때 연결 된 자식 레코드를 자동으로 삭제 하도록 Foreign key 제약 조건을 구성할 수 있습니다. 즉, 사용자의 사용자 계정이 삭제 될 때 사용자의 방명록 항목이 자동으로 삭제 되도록 foreign key 제약 조건을 설정할 수 있습니다. 이를 수행 하려면 "삽입 및 업데이트 사양" 섹션을 확장 하 고 "규칙 삭제" 속성을 Cascade로 설정 합니다.

[Foreign Key 제약 조건을 Cascade 삭제로 구성 ![](storing-additional-user-information-cs/_static/image14.png)](storing-additional-user-information-cs/_static/image13.png)

**그림 5**: Cascade delete에 대해 Foreign Key 제약 조건 구성 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image15.png))

Foreign key 제약 조건을 저장 하려면 닫기 단추를 클릭 하 여 외래 키 관계를 종료 합니다. 그런 다음 도구 모음에서 저장 아이콘을 클릭 하 여 테이블과이 관계를 저장 합니다.

### <a name="storing-the-users-home-town-homepage-and-signature"></a>사용자의 홈 타운, 홈페이지 및 서명 저장

`GuestbookComments` 표에서는 사용자 계정과 일 대 다 관계를 공유 하는 정보를 저장 하는 방법을 보여 줍니다. 각 사용자 계정에는 연결 된 설명이 임의로 포함 될 수 있으므로이 관계는 각 주석을 특정 사용자에 게 다시 연결 하는 열을 포함 하는 테이블을 만들어 모델링 합니다. `SqlMembershipProvider`를 사용 하는 경우이 링크는 `uniqueidentifier` 형식의 `UserId` 열과이 열과 `aspnet_Users.UserId`간의 foreign key 제약 조건을 만들어 설정 하는 것이 가장 좋습니다.

이제 각 사용자 계정에 세 개의 열을 연결 하 여 사용자의 홈 타운, 홈 페이지 및 서명을 저장 해야 합니다 .이는 방명록 메모에 표시 됩니다. 이 작업을 수행 하는 방법에는 여러 가지가 있습니다.

- <strong>`aspnet_Users`</strong> <strong>또는</strong> <strong>`aspnet_Membership`</strong>테이블 <strong>에 새 열을 추가</strong> <strong>합니다.</strong> `SqlMembershipProvider`에서 사용 하는 스키마를 수정 하기 때문에이 방법은 사용 하지 않는 것이 좋습니다. 이 의사 결정은 haunt으로 돌아올 수 있습니다. ASP.NET의 이후 버전에서 다른 `SqlMembershipProvider` 스키마를 사용 하는 경우를 예로 들 수가 있습니다. Microsoft는 ASP.NET 2.0 `SqlMembershipProvider` 데이터를 새 스키마로 마이그레이션하는 도구를 포함할 수 있지만 ASP.NET 2.0 `SqlMembershipProvider` 스키마를 수정한 경우에는 이러한 변환을 수행할 수 없습니다.

- **ASP를 사용 합니다. 가정용 마을, 홈페이지 및 서명에 대 한 프로필 속성을 정의 하는 NET의 프로필 프레임 워크입니다.** ASP.NET에는 추가 사용자별 데이터를 저장 하도록 디자인 된 프로필 프레임 워크가 포함 되어 있습니다. 멤버 프레임 워크와 마찬가지로 프로필 프레임 워크는 공급자 모델 위에 빌드됩니다. .NET Framework는 SQL Server 데이터베이스에 프로필 데이터를 저장 하는 `SqlProfileProvider`와 함께 제공 됩니다. 실제로 데이터베이스에는 <a id="_msoanchor_2"> </a> [*SQL Server 자습서에서 멤버 자격 스키마 만들기*](creating-the-membership-schema-in-sql-server-cs.md) 에서 응용 프로그램 서비스를 다시 추가할 때 추가 된 `SqlProfileProvider` (`aspnet_Profile`)에서 이미 사용 된 테이블이 있습니다.   
  프로필 프레임 워크의 주요 혜택은 개발자가 `Web.config`에서 프로필 속성을 정의할 수 있다는 것입니다. 즉, 프로필 데이터를 기본 데이터 저장소로 serialize 하기 위해 코드를 작성할 필요가 없습니다. 간단히 말해 프로필 속성 집합을 정의 하 고 코드에서 작업 하는 것이 매우 쉽습니다. 그러나 버전을 관리 하는 경우 프로필 시스템을 사용 하는 것이 매우 바람직 하므로, 나중에 새 사용자 지정 속성을 추가 하거나 기존 속성을 제거 하거나 수정할 수 있는 응용 프로그램이 있는 경우 프로필 프레임 워크는  최상의 옵션입니다. 또한 `SqlProfileProvider`는 프로필 속성을 매우 비 정규화 된 방식으로 저장 하 여 프로필 데이터에 대해 직접 쿼리를 실행할 수 없게 합니다 (예: 뉴욕의 홈 타운을 가진 사용자 수).   
  프로필 프레임 워크에 대 한 자세한 내용은이 자습서의 끝부분에 있는 "추가 판독값" 섹션을 참조 하세요.

- <strong>데이터베이스의 새 테이블에 이러한 3 개의 열을 추가 하 고이 테이블과`aspnet_Users`사이에 일 대 일 관계를 설정</strong> <strong>합니다.</strong> 이 방법은 프로필 프레임 워크 보다 약간 더 많은 작업을 수행 하지만 데이터베이스에서 추가 사용자 속성을 모델링 하는 방법에 대 한 최대 유연성을 제공 합니다. 이 옵션은이 자습서에서 사용 하는 옵션입니다.

`UserProfiles` 라는 새 테이블을 만들어 각 사용자에 대 한 홈 타운, 홈 페이지 및 서명을 저장 합니다. 데이터베이스 탐색기 창의 Tables 폴더를 마우스 오른쪽 단추로 클릭 하 고 새 테이블을 만들도록 선택 합니다. 첫 번째 열의 이름을 `UserId` 하 고 해당 형식을 `uniqueidentifier`로 설정 합니다. `NULL` 값을 허용 하지 않고 열을 기본 키로 표시 합니다. 다음으로, `nvarchar(50)`형식의 `HomeTown` 이라는 열을 추가 합니다. `nvarchar(100)`형식의 `HomepageUrl` 및 형식의 시그니처를 `nvarchar(500)`합니다. 이러한 세 열은 모두 `NULL` 값을 허용할 수 있습니다.

[UserProfiles 테이블 ![만들려면](storing-additional-user-information-cs/_static/image17.png)](storing-additional-user-information-cs/_static/image16.png)

**그림 6**: `UserProfiles` 테이블 만들기 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image18.png))

테이블을 저장 하 고 이름을 `UserProfiles`으로 이름을로 합니다. 마지막으로 `UserProfiles` 테이블의 `UserId` 필드와 `aspnet_Users.UserId` 필드 사이에 foreign key 제약 조건을 설정 합니다. `GuestbookComments` 테이블과 `aspnet_Users` 테이블 사이에 foreign key 제약 조건이 있는 것 처럼이 제약 조건을 cascade로 삭제 합니다. `UserProfiles`의 `UserId` 필드가 기본 키 이기 때문에 각 사용자 계정에 대 한 `UserProfiles` 테이블에 레코드가 둘 이상 존재 하지 않게 됩니다. 이 유형의 관계를 일 대 일 이라고 합니다.

이제 데이터 모델을 만들었으므로 사용할 준비가 되었습니다. 2 단계와 3 단계에서 현재 로그온 한 사용자가 자신의 집 마을, 홈페이지 및 서명 정보를 보고 편집할 수 있는 방법을 살펴보겠습니다. 4 단계에서는 인증 된 사용자가 새 의견을 방명록에 제출 하 고 기존 문서를 볼 수 있도록 인터페이스를 만듭니다.

## <a name="step-2-displaying-the-users-home-town-homepage-and-signature"></a>2 단계: 사용자의 홈 마을, 홈페이지 및 서명 표시

현재 로그온 한 사용자가 주택 마을, 홈페이지 및 서명 정보를 보고 편집할 수 있도록 하는 다양 한 방법이 있습니다. TextBox 및 Label 컨트롤을 사용 하 여 사용자 인터페이스를 수동으로 만들거나 DetailsView 컨트롤과 같은 데이터 웹 컨트롤 중 하나를 사용할 수 있습니다. 데이터베이스 `SELECT` 및 `UPDATE` 문을 수행 하려면 페이지의 코드를 사용 하는 클래스에 ADO.NET 코드를 작성 하거나 SqlDataSource를 사용 하 여 선언적 방법을 사용 합니다. 이상적으로 응용 프로그램에는 계층화 된 아키텍처가 포함 되어 있으므로 페이지의 코드 숨김이 아닌 클래스에서 프로그래밍 방식으로 호출 하거나 ObjectDataSource 컨트롤을 통해 선언적으로 호출할 수 있습니다.

이 자습서 시리즈는 폼 인증, 권한 부여, 사용자 계정 및 역할에 중점을 두는 이러한 다양 한 데이터 액세스 옵션에 대해 자세히 설명 하거나 SQL 문을 직접 실행 하는 경우 계층화 된 아키텍처가 선호 되는 이유를 설명 하지 않습니다. ASP.NET 페이지에서 가장 빠르고 쉬운 옵션인 DetailsView 및 SqlDataSource를 사용 하는 방법을 살펴보겠습니다. 하지만 논의 된 개념은 대체 웹 컨트롤 및 데이터 액세스 논리에 적용 될 수 있습니다. ASP.NET의 데이터로 작업 하는 방법에 대 한 자세한 내용은 *[ASP.NET 2.0 자습서 시리즈의 데이터 사용 내 작업](../../data-access/index.md)* 을 참조 하세요.

`Membership` 폴더에서 `AdditionalUserInfo.aspx` 페이지를 열고 페이지에 DetailsView 컨트롤을 추가 하 고 `ID` 속성을 `UserProfile`로 설정 하 고 `Width` 및 `Height` 속성을 지웁니다. DetailsView의 스마트 태그를 확장 하 고 새 데이터 소스 컨트롤에 바인딩하려는를 선택 합니다. 그러면 DataSource 구성 마법사가 시작 됩니다 (그림 7 참조). 첫 번째 단계에서는 데이터 원본 유형을 지정 하 라는 메시지를 표시 합니다. `SecurityTutorials` 데이터베이스에 직접 연결 하기 때문에 데이터베이스 아이콘을 선택 하 여 `ID`을 `UserProfileDataSource`로 지정 합니다.

[UserProfileDataSource 라는 새 SqlDataSource 컨트롤을 추가 ![](storing-additional-user-information-cs/_static/image20.png)](storing-additional-user-information-cs/_static/image19.png)

**그림 7**: `UserProfileDataSource` 라는 새 SqlDataSource 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image21.png))

다음 화면은 사용할 데이터베이스를 묻는 메시지를 표시 합니다. `Web.config`에서 `SecurityTutorials` 데이터베이스에 대 한 연결 문자열을 이미 정의 했습니다. 이 연결 문자열 이름 – `SecurityTutorialsConnectionString` – 드롭다운 목록에 있어야 합니다. 이 옵션을 선택 하 고 다음을 클릭 합니다.

[드롭다운 목록에서 SecurityTutorialsConnectionString를 선택 ![](storing-additional-user-information-cs/_static/image23.png)](storing-additional-user-information-cs/_static/image22.png)

**그림 8**: 드롭다운 목록에서 `SecurityTutorialsConnectionString` 선택 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image24.png))

후속 화면에서는 쿼리할 테이블 및 열을 지정 하 라는 메시지를 표시 합니다. 드롭다운 목록에서 `UserProfiles` 테이블을 선택 하 고 모든 열을 선택 합니다.

[UserProfiles 테이블에서 모든 열을 다시 가져올 ![](storing-additional-user-information-cs/_static/image26.png)](storing-additional-user-information-cs/_static/image25.png)

**그림 9**: `UserProfiles` 테이블의 모든 열 다시 가져오기 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image27.png))

그림 9의 현재 쿼리는 `UserProfiles`의 *모든* 레코드를 반환 하지만 현재 로그온 한 사용자의 레코드에만 관심이 있습니다. `WHERE` 절을 추가 하려면 `WHERE` 단추를 클릭 하 여 `WHERE` 절 추가 대화 상자를 표시 합니다 (그림 10 참조). 여기에서 필터링 할 열, 연산자 및 필터 매개 변수의 소스를 선택할 수 있습니다. 열로 `UserId`를 선택 하 고 연산자로 "="를 선택 합니다.

아쉽게도 현재 로그온 한 사용자의 `UserId` 값을 반환 하는 기본 제공 매개 변수 소스가 없습니다. 이 값은 프로그래밍 방식으로 잡아 두어야 합니다. 따라서 원본 드롭다운 목록을 "없음"으로 설정 하 고 추가 단추를 클릭 하 여 매개 변수를 추가한 다음 확인을 클릭 합니다.

[UserId 열에서 필터 매개 변수를 추가 ![](storing-additional-user-information-cs/_static/image29.png)](storing-additional-user-information-cs/_static/image28.png)

**그림 10**: `UserId` 열에 필터 매개 변수 추가 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image30.png))

확인을 클릭 하면 그림 9에 표시 된 화면으로 돌아갑니다. 그러나 이번에는 화면 맨 아래에 있는 SQL 쿼리에 `WHERE` 절이 포함 되어야 합니다. 다음을 클릭 하 여 "쿼리 테스트" 화면으로 이동 합니다. 여기에서 쿼리를 실행 하 고 결과를 볼 수 있습니다. 마침을 클릭하여 마법사를 완료합니다.

DataSource 구성 마법사가 완료 되 면 Visual Studio에서 마법사에 지정 된 설정에 따라 SqlDataSource 컨트롤을 만듭니다. 또한 SqlDataSource의 `SelectCommand`에서 반환 하는 각 열에 대해 DetailsView에 BoundFields를 수동으로 추가 합니다. 사용자가이 값을 알 필요가 없기 때문에 DetailsView에 `UserId` 필드를 표시할 필요가 없습니다. 이 필드는 DetailsView 컨트롤의 선언적 태그에서 직접 제거 하거나 스마트 태그에서 "필드 편집" 링크를 클릭 하 여 제거할 수 있습니다.

이 시점에서 페이지의 선언 태그는 다음과 같이 표시 됩니다.

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample1.aspx)]

데이터를 선택 하기 전에 프로그래밍 방식으로 SqlDataSource 컨트롤의 `UserId` 매개 변수를 현재 로그인 한 사용자의 `UserId`으로 설정 해야 합니다. 이 작업은 SqlDataSource의 `Selecting` 이벤트에 대 한 이벤트 처리기를 만들고 다음 코드를 추가 하 여 수행할 수 있습니다.

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample2.cs)]

위의 코드는 `Membership` 클래스의 `GetUser` 메서드를 호출 하 여 현재 로그온 한 사용자에 대 한 참조를 가져오는 것으로 시작 합니다. 그러면 `ProviderUserKey` 속성이 `UserId`을 포함 하는 `MembershipUser` 개체가 반환 됩니다. 그러면 `UserId` 값이 SqlDataSource의 `@UserId` 매개 변수에 할당 됩니다.

> [!NOTE]
> `Membership.GetUser()` 메서드는 현재 로그온 한 사용자에 대 한 정보를 반환 합니다. 익명 사용자가 페이지를 방문 하는 경우 `null`값이 반환 됩니다. 이러한 경우 `ProviderUserKey` 속성을 읽으려고 할 때 다음 코드 줄에 `NullReferenceException` 됩니다. 물론 인증 된 사용자만이 폴더의 ASP.NET 리소스에 액세스할 수 있도록 이전 자습서에서 URL 권한 부여를 구성 했기 때문에 `AdditionalUserInfo.aspx` 페이지에서 `null` 값을 반환 하는 `Membership.GetUser()`에 대해 걱정할 필요가 없습니다. 익명 액세스가 허용 된 페이지에서 현재 로그온 한 사용자에 대 한 정보에 액세스 해야 하는 경우 해당 속성을 참조 하기 전에 `GetUser()` 메서드에서`null MembershipUser` 되지 않은 개체가 반환 되는지 확인 해야 합니다.

브라우저를 통해 `AdditionalUserInfo.aspx` 페이지를 방문 하는 경우 `UserProfiles` 테이블에 행을 추가 하기 때문에 빈 페이지가 표시 됩니다. 6 단계에서는 새 사용자 계정을 만들 때 `UserProfiles` 테이블에 새 행을 자동으로 추가 하도록 CreateUserWizard 컨트롤을 사용자 지정 하는 방법을 살펴보겠습니다. 그러나 지금은 테이블에서 레코드를 수동으로 만들어야 합니다.

Visual Studio에서 데이터베이스 탐색기로 이동 하 여 Tables 폴더를 확장 합니다. `aspnet_Users` 테이블을 마우스 오른쪽 단추로 클릭 하 고 "테이블 데이터 표시"를 선택 하 여 테이블의 레코드를 확인 합니다. `UserProfiles` 테이블에 대해 동일한 작업을 수행 합니다. 그림 11은 세로로 바둑판식으로 배열 될 때 이러한 결과를 보여 줍니다. 내 데이터베이스에는 현재 Bruce, Fred 및 Tito에 대 한 레코드를 `aspnet_Users` 있지만 `UserProfiles` 테이블에는 레코드가 없습니다.

[aspnet_Users 및 UserProfiles 테이블의 내용이 표시 ![](storing-additional-user-information-cs/_static/image32.png)](storing-additional-user-information-cs/_static/image31.png)

**그림 11**: `aspnet_Users` 및 `UserProfiles` 테이블의 내용이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image33.png)).

`HomeTown`, `HomepageUrl`및 `Signature` 필드에 대 한 값을 수동으로 입력 하 여 `UserProfiles` 테이블에 새 레코드를 추가 합니다. 새 `UserProfiles` 레코드에서 유효한 `UserId` 값을 가져오는 가장 쉬운 방법은 `aspnet_Users` 테이블의 특정 사용자 계정에서 `UserId` 필드를 선택 하 고 복사 하 여 `UserId`의 `UserProfiles`필드에 붙여 넣는 것입니다. 그림 12에서는 Bruce에 대해 새 레코드가 추가 된 후의 `UserProfiles` 테이블을 보여 줍니다.

[Bruce 용 UserProfiles에 레코드를 추가 ![](storing-additional-user-information-cs/_static/image35.png)](storing-additional-user-information-cs/_static/image34.png)

**그림 12**: bruce의 `UserProfiles`에 레코드가 추가 됨 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image36.png))

Bruce로 로그인 한 `AdditionalUserInfo.aspx` 페이지로 돌아갑니다. 그림 13에서 볼 수 있듯이 Bruce의 설정이 표시 됩니다.

[현재 방문한 사용자의 설정에 대 한 ![표시 됩니다.](storing-additional-user-information-cs/_static/image38.png)](storing-additional-user-information-cs/_static/image37.png)

**그림 13**: 현재 방문 중인 사용자에 대 한 설정이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image39.png)).

> [!NOTE]
> 계속 해 서 각 멤버 자격 사용자에 대 한 `UserProfiles` 테이블에서 레코드를 수동으로 추가 합니다. 6 단계에서는 새 사용자 계정을 만들 때 `UserProfiles` 테이블에 새 행을 자동으로 추가 하도록 CreateUserWizard 컨트롤을 사용자 지정 하는 방법을 살펴보겠습니다.

## <a name="step-3-allowing-the-user-to-edit-his-home-town-homepage-and-signature"></a>3 단계: 사용자가 자신의 집 마을, 홈페이지 및 서명을 편집할 수 있도록 허용

이 시점에서 현재 로그인 한 사용자는 홈 타운, 홈페이지 및 서명 설정을 볼 수 있지만 수정할 수는 없습니다. 데이터를 편집할 수 있도록 DetailsView 컨트롤을 업데이트 해 보겠습니다.

가장 먼저 해야 할 일은 SqlDataSource에 대 한 `UpdateCommand`를 추가 하 고 실행할 `UPDATE` 문과 해당 매개 변수를 지정 하는 것입니다. SqlDataSource를 선택 하 고 속성 창에서 UpdateQuery 속성 옆의 줄임표를 클릭 하 여 명령 및 매개 변수 편집기 대화 상자를 표시 합니다. 텍스트 상자에 다음 `UPDATE` 문을 입력 합니다.

[!code-sql[Main](storing-additional-user-information-cs/samples/sample3.sql)]

그런 다음 "매개 변수 새로 고침" 단추를 클릭 합니다 .이 단추를 클릭 하면 `UPDATE` 문의 각 매개 변수에 대해 SqlDataSource 컨트롤의 `UpdateParameters` 컬렉션에서 매개 변수를 만들 수 있습니다. 모든 매개 변수의 소스를 None으로 설정 하 고 확인 단추를 클릭 하 여 대화 상자를 완료 합니다.

[SqlDataSource의 UpdateCommand 및 UpdateParameters 지정 ![](storing-additional-user-information-cs/_static/image41.png)](storing-additional-user-information-cs/_static/image40.png)

**그림 14**: SqlDataSource의 `UpdateCommand` 및 `UpdateParameters` 지정 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image42.png))

SqlDataSource 컨트롤에 대 한 추가 작업으로 인해 DetailsView 컨트롤에서 편집을 지원할 수 있습니다. DetailsView의 스마트 태그에서 "편집 사용" 확인란을 선택 합니다. 이렇게 하면 `ShowEditButton` 속성이 True로 설정 된 컨트롤의 `Fields` 컬렉션에 CommandField가 추가 됩니다. 이렇게 하면 DetailsView이 읽기 전용 모드에서 표시 되 고 편집 모드로 표시 될 때 업데이트 및 취소 단추가 표시 될 때 편집 단추가 렌더링 됩니다. 그러나 사용자가 편집을 클릭 하도록 요구 하는 대신 DetailsView 컨트롤의 [`DefaultMode` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.defaultmode.aspx) 을 `Edit`로 설정 하 여 detailsview 렌더링을 "항상 편집 가능" 상태로 만들 수 있습니다.

이러한 변경 내용으로 DetailsView 컨트롤의 선언 태그는 다음과 유사 하 게 표시 됩니다.

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample4.aspx)]

CommandField 및 `DefaultMode` 속성이 추가 됩니다.

계속 해 서 브라우저를 통해이 페이지를 테스트 합니다. `UserProfiles`에 해당 하는 레코드가 있는 사용자로 방문할 때 사용자의 설정이 편집 가능한 인터페이스로 표시 됩니다.

[![DetailsView은 편집 가능한 인터페이스를 렌더링 합니다.](storing-additional-user-information-cs/_static/image44.png)](storing-additional-user-information-cs/_static/image43.png)

**그림 15**: DetailsView은 편집 가능한 인터페이스를 렌더링 합니다 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image45.png)).

값을 변경 하 고 업데이트 단추를 클릭 합니다. 아무 작업도 수행 되지 않는 것으로 나타납니다. 포스트백이 발생 하 고 값이 데이터베이스에 저장 되지만 저장이 발생 한 시각적 피드백이 없습니다.

이를 해결 하려면 Visual Studio로 돌아가서 DetailsView 위에 레이블 컨트롤을 추가 합니다. 해당 `ID` `SettingsUpdatedMessage`, `Text` 속성을 "사용자 설정이 업데이트 되었습니다."로 설정 하 고 `Visible` 및 `EnableViewState` 속성을 `false`로 설정 합니다.

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample5.aspx)]

DetailsView이 업데이트 될 때마다 `SettingsUpdatedMessage` 레이블을 표시 해야 합니다. 이 작업을 수행 하려면 DetailsView의 `ItemUpdated` 이벤트에 대 한 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample6.cs)]

브라우저를 통해 `AdditionalUserInfo.aspx` 페이지로 돌아가 데이터를 업데이트 합니다. 이번에는 유용한 상태 메시지가 표시 됩니다.

[설정이 업데이트 되 면 짧은 메시지가 표시 ![](storing-additional-user-information-cs/_static/image47.png)](storing-additional-user-information-cs/_static/image46.png)

**그림 16**: 설정이 업데이트 되 면 짧은 메시지가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image48.png)).

> [!NOTE]
> DetailsView 컨트롤의 편집 인터페이스는 원하는 것으로 유지 됩니다. 표준 크기의 텍스트 상자를 사용 하지만 서명 필드는 여러 줄 텍스트 상자 일 수 있습니다. RegularExpressionValidator는 홈페이지 URL (입력 한 경우)이 "http://" 또는 "https://"로 시작 하는지 확인 하는 데 사용 됩니다. 또한 DetailsView 컨트롤의 `DefaultMode` 속성이 `Edit`로 설정 되어 있기 때문에 취소 단추는 아무것도 수행 하지 않습니다. 제거 하거나 클릭 하면 사용자를 다른 페이지 (예: `~/Default.aspx`)로 리디렉션할 수 있습니다. 이러한 향상 된 기능을 독자를 위한 연습으로 그대로 둡니다.

### <a name="adding-a-link-to-theadditionaluserinfoaspxpage-in-the-master-page"></a>마스터 페이지의`AdditionalUserInfo.aspx`페이지에 대 한 링크 추가

현재 웹 사이트는 `AdditionalUserInfo.aspx` 페이지에 대 한 링크를 제공 하지 않습니다. 이에 도달 하려면 페이지의 URL을 브라우저의 주소 표시줄에 직접 입력 하면 됩니다. `Site.master` 마스터 페이지에서이 페이지에 대 한 링크를 추가 해 보겠습니다.

마스터 페이지에는 인증 된 방문자와 익명 방문자에 대해 서로 다른 태그를 표시 하는 `LoginContent` ContentPlaceHolder에 LoginView 웹 컨트롤이 포함 되어 있습니다. `AdditionalUserInfo.aspx` 페이지에 대 한 링크를 포함 하도록 LoginView 컨트롤의 `LoggedInTemplate`를 업데이트 합니다. 이러한 변경을 수행한 후에는 LoginView 컨트롤의 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample7.aspx)]

`LoggedInTemplate`에 `lnkUpdateSettings` HyperLink 컨트롤이 추가 되었습니다. 이 링크를 통해 인증 된 사용자는 빠르게 페이지로 이동 하 여 홈 마을, 홈페이지 및 서명 설정을 확인 하 고 수정할 수 있습니다.

## <a name="step-4-adding-new-guestbook-comments"></a>4 단계: 새 방명록 메모 추가

`Guestbook.aspx` 페이지에서는 인증 된 사용자가 방명록을 보고 메모를 남길 수 있습니다. 새 방명록 주석을 추가 하는 인터페이스를 만드는 것부터 시작 해 보겠습니다.

Visual Studio에서 `Guestbook.aspx` 페이지를 열고 두 개의 TextBox 컨트롤로 구성 된 사용자 인터페이스 (새 주석의 제목 및 본문에 대 한 하나)를 생성 합니다. 첫 번째 TextBox 컨트롤의 `ID` 속성을 `Subject`로 설정 하 고 `Columns` 속성을 40으로 설정 합니다. 두 번째 `ID` `Body`, `TextMode` `MultiLine`및 `Width` 속성을 각각 "95%" 및 8로 설정 합니다.`Rows` 사용자 인터페이스를 완료 하려면 `PostCommentButton` 이라는 단추 웹 컨트롤을 추가 하 고 `Text` 속성을 "주석 게시"로 설정 합니다.

각 방명록 주석에는 제목과 본문이 필요 하므로 각 텍스트 상자에 대해 RequiredFieldValidator를 추가 합니다. 이러한 컨트롤의 `ValidationGroup` 속성을 "추가 주석"으로 설정 합니다. 마찬가지로 `PostCommentButton` 컨트롤의 `ValidationGroup` 속성을 "추가 주석"으로 설정 합니다. ASP에 대 한 자세한 내용 NET의 유효성 검사 컨트롤, [ASP.NET의 폼 유효성](http://www.4guysfromrolla.com/webtech/090200-1.shtml)검사, [ASP.NET 2.0의 유효성 검사 컨트롤 개로 나누어서](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx), [W3Schools](http://www.w3schools.com/)의 [유효성 검사 서버 컨트롤 자습서](http://www.w3schools.com/aspnet/aspnet_refvalidationcontrols.asp) 를 참조 하세요.

사용자 인터페이스를 만든 후 페이지의 선언 태그는 다음과 같습니다.

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample8.aspx)]

사용자 인터페이스가 완료 되 면 다음 태스크는 `PostCommentButton` 클릭 될 때 `GuestbookComments` 테이블에 새 레코드를 삽입 하는 것입니다. 이 작업은 다양 한 방법으로 수행할 수 있습니다. 단추의 `Click` 이벤트 처리기에 ADO.NET 코드를 작성할 수 있습니다. SqlDataSource 컨트롤을 페이지에 추가 하 고 `InsertCommand`구성한 다음 `Click` 이벤트 처리기에서 `Insert` 메서드를 호출할 수 있습니다. 또는 새 방명록 주석을 삽입 하 고 `Click` 이벤트 처리기에서이 기능을 호출 하는 중간 계층을 빌드할 수 있습니다. 3 단계에서 SqlDataSource를 사용 하는 방법을 살펴보았으므로 여기에서 ADO.NET 코드를 사용 하겠습니다.

> [!NOTE]
> Microsoft SQL Server 데이터베이스에서 프로그래밍 방식으로 데이터에 액세스 하는 데 사용 되는 ADO.NET 클래스는 `System.Data.SqlClient` 네임 스페이스에 있습니다. 이 네임 스페이스를 페이지의 코드 숨김이 아닌 클래스 (예: `using System.Data.SqlClient;`)로 가져와야 할 수 있습니다.

`PostCommentButton`의 `Click` 이벤트에 대 한 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample9.cs)]

`Click` 이벤트 처리기는 사용자가 제공한 데이터가 유효한 지 확인 하 여 시작 합니다. 그렇지 않으면 이벤트 처리기는 레코드를 삽입 하기 전에 종료 됩니다. 제공 된 데이터가 유효한 것으로 가정 하면 현재 로그온 한 사용자의 `UserId` 값을 검색 하 여 `currentUserId` 지역 변수에 저장 합니다. `GuestbookComments`에 레코드를 삽입할 때 `UserId` 값을 제공 해야 하기 때문에이 값이 필요 합니다.

그런 다음 `SecurityTutorials` 데이터베이스에 대 한 연결 문자열을 `Web.config`에서 검색 하 고 `INSERT` SQL 문을 지정 합니다. 그런 다음 `SqlConnection` 개체를 만들어 엽니다. 다음으로 `SqlCommand` 개체가 생성 되 고 `INSERT` 쿼리에 사용 되는 매개 변수의 값이 할당 됩니다. 그런 다음 `INSERT` 문이 실행 되 고 연결이 닫혔습니다. 이벤트 처리기의 끝에서 사용자의 값이 다시 게시를 통해 유지 되지 않도록 `Subject` 및 `Body` 텍스트 상자 `Text` 속성이 지워집니다.

계속 해 서 브라우저에서이 페이지를 테스트 합니다. 이 페이지는 `Membership` 폴더에 있으므로 익명 방문자는 액세스할 수 없습니다. 따라서 아직 로그온 하지 않은 경우에는 먼저 로그온 해야 합니다. `Subject` 및 `Body` 텍스트 상자에 값을 입력 하 고 `PostCommentButton` 단추를 클릭 합니다. 이렇게 하면 `GuestbookComments`에 새 레코드가 추가 됩니다. 다시 게시 하는 경우 제공한 제목과 본문은 텍스트 상자에서 초기화 됩니다.

`PostCommentButton` 단추를 클릭 한 후에는 설명이 방명록에 추가 되었다는 시각적 피드백이 없습니다. 5 단계에서 수행 하는 기존 방명록 주석을 표시 하려면이 페이지를 업데이트 해야 합니다. 이를 완료 한 후에는 적절 한 시각적 피드백을 제공 하는 주석 목록에 방금 추가 된 주석이 표시 됩니다. 지금은 `GuestbookComments` 테이블의 내용을 검사 하 여 방명록 주석이 저장 되었는지 확인 합니다.

그림 17에서는 두 개의 주석이 남아 있는 후 `GuestbookComments` 테이블의 내용을 보여 줍니다.

[![GuestbookComments 테이블에서 방명록 주석을 볼 수 있습니다.](storing-additional-user-information-cs/_static/image50.png)](storing-additional-user-information-cs/_static/image49.png)

**그림 17**: `GuestbookComments` 표에서 방명록 주석을 볼 수 있습니다 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image51.png)).

> [!NOTE]
> 사용자가 잠재적으로 위험한 태그 (예: HTML)가 포함 된 방명록 주석을 삽입 하려고 하면 ASP.NET는 `HttpRequestValidationException`을 throw 합니다. 이 예외에 대 한 자세한 내용, 예외가 throw 된 이유 및 사용자가 잠재적으로 위험한 값을 제출할 수 있도록 허용 하는 방법에 대 한 자세한 내용은 [요청 유효성 검사 백서](../../../../whitepapers/request-validation.md)를 참조 하세요.

## <a name="step-5-listing-the-existing-guestbook-comments"></a>5 단계: 기존 방명록 설명 나열

`Guestbook.aspx` 페이지를 방문 하는 사용자는 의견을 남겨 둘 뿐만 아니라 방명록의 기존 주석도 볼 수 있습니다. 이를 수행 하려면 `CommentList` 이라는 ListView 컨트롤을 페이지 맨 아래에 추가 합니다.

> [!NOTE]
> ListView 컨트롤은 ASP.NET 버전 3.5의 새로운 버전입니다. 사용자 지정이 가능 하 고 유연한 레이아웃으로 항목의 목록을 표시 하도록 설계 되었지만 GridView와 같이 기본 제공 되는 편집, 삽입, 삭제, 페이징 및 정렬 기능을 계속 제공 합니다. ASP.NET 2.0를 사용 하는 경우 DataList 또는 Repeater 컨트롤을 대신 사용 해야 합니다. ListView를 사용 하는 방법에 대 한 자세한 내용은 [Scott Guthrie](https://weblogs.asp.net/scottgu/)의 블로그 항목, [Asp: listview 컨트롤](https://weblogs.asp.net/scottgu/archive/2007/08/10/the-asp-listview-control-part-1-building-a-product-listing-page-with-clean-css-ui.aspx)및 내 문서에서 [listview 컨트롤을 사용 하 여 데이터 표시](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)를 참조 하세요.

ListView의 스마트 태그를 열고 데이터 소스 선택 드롭다운 목록에서 컨트롤을 새 데이터 소스에 바인딩합니다. 2 단계에서 살펴본 것 처럼이 경우 데이터 소스 구성 마법사가 시작 됩니다. 데이터베이스 아이콘을 선택 하 고, 생성 된 SqlDataSource `CommentsDataSource`의 이름을로, 확인을 클릭 합니다. 그런 다음 드롭다운 목록에서 `SecurityTutorialsConnectionString` 연결 문자열을 선택 하 고 다음을 클릭 합니다.

2 단계에서이 시점에는 드롭다운 목록에서 `UserProfiles` 테이블을 선택 하 고 반환할 열을 선택 하 여 쿼리할 데이터를 지정 했습니다 (그림 9 참조). 그러나 이번에는 `GuestbookComments`의 레코드 뿐만 아니라 commenter의 주택 마을, 홈페이지, 서명 및 사용자 이름과 같은 레코드를 복원 하는 SQL 문을 만들 수 있습니다. 따라서 "사용자 지정 SQL 문 또는 저장 프로시저 지정" 라디오 단추를 선택 하 고 다음을 클릭 합니다.

그러면 "사용자 지정 문 또는 저장 프로시저 정의" 화면이 표시 됩니다. 쿼리 작성기 단추를 클릭 하 여 쿼리를 그래픽으로 작성 합니다. 쿼리 하려는 테이블을 지정 하 라는 메시지를 표시 하 여 쿼리 작성기를 시작 합니다. `GuestbookComments`, `UserProfiles`및 `aspnet_Users` 테이블을 선택 하 고 확인을 클릭 합니다. 이렇게 하면 세 개의 테이블이 모두 디자인 화면에 추가 됩니다. `GuestbookComments`, `UserProfiles`및 `aspnet_Users` 테이블 사이에 foreign key 제약 조건이 있으므로 쿼리 작성기는 이러한 테이블을 자동으로 `JOIN` 합니다.

계속 해 서 반환할 열을 지정 합니다. `GuestbookComments` 테이블에서 `Subject`, `Body`및 `CommentDate` 열을 선택 합니다. `UserProfiles` 테이블에서 `HomeTown`, `HomepageUrl`및 `Signature` 열을 반환 합니다. `aspnet_Users`에서 `UserName`을 반환 합니다. 또한 가장 최근의 게시물이 먼저 반환 되도록 `SELECT` 쿼리의 끝에 "`ORDER BY CommentDate DESC`"를 추가 합니다. 이러한 항목을 선택 하면 쿼리 작성기 인터페이스가 그림 18의 스크린샷 처럼 표시 됩니다.

[![생성 된 쿼리가 GuestbookComments, UserProfiles 및 aspnet_Users 테이블에 조인 합니다.](storing-additional-user-information-cs/_static/image53.png)](storing-additional-user-information-cs/_static/image52.png)

**그림 18**: 생성 된 쿼리 `JOIN` `GuestbookComments`, `UserProfiles`및 `aspnet_Users` 테이블 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image54.png))

확인을 클릭 하 여 쿼리 작성기 창을 닫고 "사용자 지정 문 또는 저장 프로시저 정의" 화면으로 돌아갑니다. 다음을 클릭 하 여 "쿼리 테스트" 화면으로 이동 합니다. 여기서 쿼리 테스트 단추를 클릭 하 여 쿼리 결과를 볼 수 있습니다. 준비가 되 면 마침을 클릭 하 여 데이터 원본 구성 마법사를 완료 합니다.

2 단계에서 데이터 원본 구성 마법사를 완료 하면 `SelectCommand`에서 반환 된 각 열에 대해 BoundField를 포함 하도록 연결 된 DetailsView 컨트롤의 `Fields` 컬렉션이 업데이트 되었습니다. 그러나 ListView는 변경 되지 않은 상태로 유지 됩니다. 여전히 레이아웃을 정의 해야 합니다. ListView의 레이아웃은 선언적 태그 또는 해당 스마트 태그의 "ListView 구성" 옵션을 통해 수동으로 생성할 수 있습니다. 일반적으로 태그를 직접 정의 하는 것이 좋습니다. 그러나 가장 자연 스러운 메서드를 사용 하는 것이 좋습니다.

내 ListView 컨트롤에 대해 다음 `LayoutTemplate`, `ItemTemplate`및 `ItemSeparatorTemplate`를 사용 하 여 종료 되었습니다.

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample10.aspx)]

`LayoutTemplate`는 컨트롤이 내보내는 태그를 정의 하는 반면 `ItemTemplate`는 SqlDataSource에서 반환 된 각 항목을 렌더링 합니다. `ItemTemplate`의 결과 태그는 `LayoutTemplate`의 `itemPlaceholder` 컨트롤에 배치 됩니다. `itemPlaceholder`외에도 `LayoutTemplate`에는 DataPager 컨트롤이 포함 되어 있습니다 .이 컨트롤은 ListView에서 페이지당 10 개의 방명록 주석 (기본값)만 표시 하도록 제한 하 고 페이징 인터페이스를 렌더링 합니다.

내 `ItemTemplate`는 각 방명록 주석의 제목을 제목 아래에 있는 `<h4>` 요소에 표시 합니다. 본문을 표시 하는 데 사용 되는 구문은 `Eval("Body")` databinding 문에 의해 반환 된 데이터를 가져와 문자열로 변환 하 고 줄 바꿈을 `<br />` 요소로 바꿉니다. HTML에서 공백을 무시 하므로 주석을 제출할 때 입력 된 줄 바꿈을 표시 하기 위해이 변환이 필요 합니다. 사용자의 서명은 기울임꼴로 표시 되 고, 사용자의 홈 타운, 홈 페이지에 대 한 링크, 주석이 작성 된 날짜 및 시간, 주석을 떠난 사람의 사용자 이름 등이 표시 됩니다.

잠시 시간을 사용 하 여 브라우저를 통해 페이지를 봅니다. 여기에 표시 된 5 단계에서 방명록에 추가한 의견이 표시 되어야 합니다.

[이제 방명록 ![방명록의 주석을 표시 합니다.](storing-additional-user-information-cs/_static/image56.png)](storing-additional-user-information-cs/_static/image55.png)

**그림 19**: 이제 방명록의 주석을 표시 `Guestbook.aspx` ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image57.png))

새 메모를 방명록에 추가 해 보세요. `PostCommentButton` 단추를 클릭 하면 페이지가 다시 게시 되 고 주석이 데이터베이스에 추가 되지만 ListView 컨트롤은 새 주석을 표시 하도록 업데이트 되지 않습니다. 다음 중 하나를 수행 하 여 해결할 수 있습니다.

- 데이터베이스에 새 주석을 삽입 한 후 ListView 컨트롤의 `DataBind()` 메서드를 호출 하도록 `PostCommentButton` 단추의 `Click` 이벤트 처리기 업데이트 또는
- ListView 컨트롤의 `EnableViewState` 속성을 `false`로 설정 합니다. 이 방법은 컨트롤의 뷰 상태를 사용 하지 않도록 설정 하 여 다시 게시할 때마다 기본 데이터에 다시 바인딩해야 하기 때문에 작동 합니다.

이 자습서에서 다운로드할 자습서 웹 사이트에서는 두 가지 방법을 모두 보여 줍니다. ListView 컨트롤의 `EnableViewState` 속성은 `false` 하 고 데이터를 ListView에 프로그래밍 방식으로 다시 바인딩하는 데 필요한 코드는 `Click` 이벤트 처리기에 있지만 주석 처리 됩니다.

> [!NOTE]
> 현재 `AdditionalUserInfo.aspx` 페이지를 사용 하 여 사용자는 홈 타운, 홈 페이지 및 서명 설정을 보고 편집할 수 있습니다. 로그인 한 사용자의 방명록 주석을 표시 하도록 `AdditionalUserInfo.aspx`를 업데이트 하는 것이 좋을 수 있습니다. 즉, 사용자는 자신의 정보를 검토 하 고 수정 하는 것 외에도 `AdditionalUserInfo.aspx` 페이지를 방문 하 여 이전에 만든 방명록 의견을 확인할 수 있습니다. 관심이 있는 독자를 위한 연습으로 남겨 둡니다.

## <a name="step-6-customizing-the-createuserwizard-control-to-include-an-interface-for-the-home-town-homepage-and-signature"></a>6 단계: 홈 타운, 홈 페이지 및 서명에 대 한 인터페이스를 포함 하도록 CreateUserWizard 컨트롤 사용자 지정

`Guestbook.aspx` 페이지에서 사용 하는 `SELECT` 쿼리는 `INNER JOIN`를 사용 하 여 `GuestbookComments`, `UserProfiles`및 `aspnet_Users` 테이블 간에 관련 레코드를 결합 합니다. `UserProfiles`에서 레코드가 없는 사용자가 방명록 주석을 만들면 `INNER JOIN` `UserProfiles` 및 `aspnet_Users`에 일치 하는 레코드가 있는 경우에만 `GuestbookComments` 레코드만 반환 하기 때문에이 주석은 ListView에 표시 되지 않습니다. 3 단계에서 본 것 처럼 사용자에 게 `UserProfiles` 레코드가 없는 경우 `AdditionalUserInfo.aspx` 페이지에서 해당 설정을 보거나 편집할 수 없습니다.

디자인 결정으로 인해 멤버 자격 시스템의 모든 사용자 계정에는 `UserProfiles` 테이블에 일치 하는 레코드가 있어야 한다는 것이 중요 합니다. CreateUserWizard를 통해 새 멤버 자격 사용자 계정을 만들 때마다 `UserProfiles`에 해당 레코드를 추가 합니다.

[*사용자 계정 만들기*](creating-user-accounts-cs.md) 자습서에 설명 된 대로 새 멤버 자격 사용자 계정이 만들어진 후 CreateUserWizard 컨트롤은 해당 [`CreatedUser` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createduser.aspx)를 발생 시킵니다. 이 이벤트에 대 한 이벤트 처리기를 만들고 방금 만든 사용자의 UserId를 가져온 다음 `HomeTown`, `HomepageUrl`및 `Signature` 열에 대해 기본값을 사용 하 여 `UserProfiles` 테이블에 레코드를 삽입할 수 있습니다. 또한 추가 텍스트 상자를 포함 하도록 CreateUserWizard 컨트롤의 인터페이스를 사용자 지정 하 여 사용자에 게 이러한 값을 묻는 메시지를 표시할 수 있습니다.

먼저 기본값을 사용 하 여 `CreatedUser` 이벤트 처리기의 `UserProfiles` 테이블에 새 행을 추가 하는 방법을 살펴보겠습니다. 다음으로, 새 사용자의 홈 타운, 홈페이지 및 서명을 수집 하기 위해 추가 양식 필드를 포함 하도록 CreateUserWizard 컨트롤의 사용자 인터페이스를 사용자 지정 하는 방법을 알아봅니다.

### <a name="adding-a-default-row-touserprofiles"></a>`UserProfiles`에 기본 행 추가

[*사용자 계정 만들기*](creating-user-accounts-cs.md) 자습서에서 `Membership` 폴더의 `CreatingUserAccounts.aspx` 페이지에 CreateUserWizard 컨트롤을 추가 했습니다. CreateUserWizard 컨트롤에서 사용자 계정을 만들 때 `UserProfiles` 테이블에 레코드를 추가 하도록 하려면 CreateUserWizard 컨트롤의 기능을 업데이트 해야 합니다. `CreatingUserAccounts.aspx` 페이지를 변경 하는 대신 `EnhancedCreateUserWizard.aspx` 페이지에 새 CreateUserWizard 컨트롤을 추가 하 고이 자습서에 대 한 수정 내용을 적용 해 보겠습니다.

Visual Studio에서 `EnhancedCreateUserWizard.aspx` 페이지를 열고 도구 상자에서 CreateUserWizard 컨트롤을 페이지로 끌어 옵니다. CreateUserWizard 컨트롤의 `ID` 속성을 `NewUserWizard`로 설정 합니다. <a id="_msoanchor_5"> </a> [*사용자 계정 만들기*](creating-user-accounts-cs.md) 자습서에서 설명한 대로 CreateUserWizard의 기본 사용자 인터페이스는 방문자에 게 필요한 정보를 표시 합니다. 이 정보가 제공 되 면 컨트롤은 한 줄의 코드를 작성 하지 않고도 멤버 자격 프레임 워크에서 내부적으로 새 사용자 계정을 만듭니다.

CreateUserWizard 컨트롤은 해당 워크플로 중에 많은 이벤트를 발생 시킵니다. 방문자가 요청 정보를 제공 하 고 양식을 전송 하면 CreateUserWizard 컨트롤은 처음에 [`CreatingUser` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.creatinguser.aspx)를 발생 시킵니다. 만들기 프로세스 중에 문제가 발생 하면 [`CreateUserError` 이벤트가](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createusererror.aspx) 발생 합니다. 그러나 사용자가 성공적으로 만들어지면 [`CreatedUser` 이벤트가](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createduser.aspx) 발생 합니다. <a id="_msoanchor_6"> </a> [*사용자 계정 만들기*](creating-user-accounts-cs.md) 자습서에서는 `CreatingUser` 이벤트에 대 한 이벤트 처리기를 만들어 제공 된 사용자 이름에 선행 또는 후행 공백이 포함 되지 않았는지와 사용자 이름이 암호에 표시 되지 않았는지 확인 합니다.

방금 만든 사용자에 대 한 `UserProfiles` 테이블에서 행을 추가 하려면 `CreatedUser` 이벤트에 대 한 이벤트 처리기를 만들어야 합니다. `CreatedUser` 이벤트가 발생 한 시간에는 멤버 자격 프레임 워크에서 사용자 계정이 이미 만들어져 있으므로 계정의 UserId 값을 검색할 수 있습니다.

`NewUserWizard`의 `CreatedUser` 이벤트에 대 한 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample11.cs)]

위의 코드는 바로 추가 된 사용자 계정의 UserId를 검색 하 여 생물 합니다. 이는 `Membership.GetUser(username)` 메서드를 사용 하 여 특정 사용자에 대 한 정보를 반환한 다음 `ProviderUserKey` 속성을 사용 하 여 UserId를 검색 하는 방식으로 수행 됩니다. CreateUserWizard 컨트롤에 사용자가 입력 한 사용자 이름은 해당 [`UserName` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.username.aspx)을 통해 사용할 수 있습니다.

그런 다음 `Web.config`에서 연결 문자열을 검색 하 고 `INSERT` 문을 지정 합니다. 필요한 ADO.NET 개체가 인스턴스화되어 명령이 실행 됩니다. 이 코드는 `@HomeTown`, `@HomepageUrl`및 `@Signature` 매개 변수에 [`DBNull`](https://msdn.microsoft.com/library/system.dbnull.aspx) 인스턴스를 할당 하며,이는 `NULL`, `HomeTown`및 `HomepageUrl`필드에 데이터베이스 `Signature` 값을 삽입할 때 효과가 있습니다.

브라우저를 통해 `EnhancedCreateUserWizard.aspx` 페이지를 방문 하 여 새 사용자 계정을 만듭니다. 이렇게 한 후에는 Visual Studio로 돌아가서 `aspnet_Users`의 내용과 `UserProfiles` 테이블을 검토 합니다 (예: 그림 12에서). `aspnet_Users`에 새 사용자 계정이 표시 되 고 해당 `UserProfiles` 행 (`HomeTown`, `HomepageUrl`및 `Signature`에 대 한 `NULL` 값 포함)이 표시 됩니다.

[새 사용자 계정 및 UserProfiles 레코드가 추가 ![](storing-additional-user-information-cs/_static/image59.png)](storing-additional-user-information-cs/_static/image58.png)

**그림 20**: 새 사용자 계정 및 `UserProfiles` 레코드가 추가 되었습니다 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image60.png)).

방문자가 새 계정 정보를 제공 하 고 "사용자 만들기" 단추를 클릭 하면 사용자 계정이 만들어지고 `UserProfiles` 테이블에 행이 추가 됩니다. 그러면 CreateUserWizard는 성공 메시지와 계속 단추를 표시 하는 `CompleteWizardStep`표시 합니다. [계속] 단추를 클릭 하면 포스트백이 발생 하지만 작업이 수행 되지 않고 사용자가 `EnhancedCreateUserWizard.aspx` 페이지에서 중단 된 상태로 유지 됩니다.

CreateUserWizard 컨트롤의 [`ContinueDestinationPageUrl` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.continuedestinationpageurl.aspx)을 통해 계속 단추를 클릭할 때 사용자를 보낼 URL을 지정할 수 있습니다. `ContinueDestinationPageUrl` 속성을 "~/Membership/AdditionalUserInfo.aspx"로 설정 합니다. 그러면 새 사용자가 `AdditionalUserInfo.aspx`하 여 설정을 확인 하 고 업데이트할 수 있습니다.

### <a name="customizing-the-createuserwizards-interface-to-prompt-for-the-new-users-home-town-homepage-and-signature"></a>CreateUserWizard의 인터페이스를 사용자 지정 하 여 새 사용자의 홈 타운, 홈 페이지 및 서명 확인

CreateUserWizard 컨트롤의 기본 인터페이스는 사용자 이름, 암호 및 전자 메일과 같은 핵심 사용자 계정 정보만 수집 해야 하는 간단한 계정 생성 시나리오에서 충분 합니다. 하지만 계정을 만드는 동안 방문자에 게 자택 마을, 홈페이지 및 서명을 입력 하 라는 메시지를 표시 하려면 어떻게 해야 하나요? 등록 시 추가 정보를 수집 하도록 CreateUserWizard 컨트롤의 인터페이스를 사용자 지정할 수 있으며,이 정보는 `CreatedUser` 이벤트 처리기에서 기본 데이터베이스에 추가 레코드를 삽입 하는 데 사용 될 수 있습니다.

CreateUserWizard 컨트롤은 페이지 개발자가 일련의 정렬 된 `WizardSteps`를 정의할 수 있도록 하는 컨트롤인 ASP.NET Wizard 컨트롤을 확장 합니다. 마법사 컨트롤은 활성 단계를 렌더링 하 고 방문자가 이러한 단계를 이동할 수 있도록 하는 탐색 인터페이스를 제공 합니다. 마법사 컨트롤은 긴 작업을 여러 개의 짧은 단계로 분할 하는 데 적합 합니다. 마법사 컨트롤에 대 한 자세한 내용은 [ASP.NET 2.0 마법사 컨트롤을 사용 하 여 단계별 사용자 인터페이스 만들기](http://aspnet.4guysfromrolla.com/articles/061406-1.aspx)를 참조 하세요.

CreateUserWizard 컨트롤의 기본 태그는 두 개의 `WizardSteps``CreateUserWizardStep` 및 `CompleteWizardStep`를 정의 합니다.

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample12.aspx)]

첫 번째 `WizardStep``CreateUserWizardStep`는 사용자 이름, 암호, 전자 메일 등을 요청 하는 인터페이스를 렌더링 합니다. 방문자가이 정보를 제공 하 고 "사용자 만들기"를 클릭 하면 성공 메시지와 계속 단추를 표시 하는 `CompleteWizardStep`표시 됩니다.

추가 양식 필드를 포함 하도록 CreateUserWizard 컨트롤의 인터페이스를 사용자 지정 하려면 다음을 수행할 수 있습니다.

- <strong>추가 사용자 인터페이스 요소를 포함할 새`WizardStep`s를</strong> <strong>하나 이상 만듭니다</strong> . CreateUserWizard에 새 `WizardStep`를 추가 하려면 스마트 태그에서 "`WizardSteps`추가/제거" 링크를 클릭 하 여 `WizardStep` 컬렉션 편집기를 시작 합니다. 여기에서 마법사의 단계를 추가, 제거 또는 다시 정렬할 수 있습니다. 이는이 자습서에서 사용할 방법입니다.

- <strong>`CreateUserWizardStep`</strong>를 <strong>편집 가능한</strong> <strong>`WizardStep`</strong>변환 <strong>합니다.</strong> 이렇게 하면 `CreateUserWizardStep`이 해당 태그가 `CreateUserWizardStep`의와 일치 하는 사용자 인터페이스를 정의 하는 해당 `WizardStep`로 바뀝니다. `CreateUserWizardStep`를 `WizardStep`으로 변환 하면 컨트롤의 위치를 변경 하거나이 단계에 추가 사용자 인터페이스 요소를 추가할 수 있습니다. `CreateUserWizardStep` 또는 `CompleteWizardStep`를 편집 가능한 `WizardStep`변환 하려면 컨트롤의 스마트 태그에서 "사용자 지정 만들기 단계" 또는 "완료 단계 사용자 지정" 링크를 클릭 합니다.

- **위의 두 옵션을 조합 하 여 사용 합니다.**

CreateUserWizard 컨트롤은 해당 `CreateUserWizardStep`내에서 "사용자 만들기" 단추를 클릭할 때 사용자 계정 만들기 프로세스를 실행 한다는 점을 명심 해야 합니다. `CreateUserWizardStep` 후에 추가 `WizardStep` s가 있는지 여부는 중요 하지 않습니다.

CreateUserWizard 컨트롤에 사용자 지정 `WizardStep`를 추가 하 여 추가 사용자 입력을 수집 하는 경우 `CreateUserWizardStep`앞 이나 뒤에 사용자 지정 `WizardStep`을 배치할 수 있습니다. `CreateUserWizardStep` 앞에 오는 경우 사용자 지정 `WizardStep`에서 수집 된 추가 사용자 입력을 `CreatedUser` 이벤트 처리기에 사용할 수 있습니다. 그러나 사용자 지정 `WizardStep` `CreateUserWizardStep` 한 후에 사용자 지정 `WizardStep` 표시 될 때 새 사용자 계정이 이미 만들어지고 `CreatedUser` 이벤트가 이미 발생 한 것입니다.

그림 21에서는 추가 된 `WizardStep` `CreateUserWizardStep`앞에 오는 워크플로를 보여 줍니다. `CreatedUser` 이벤트가 발생 하는 시간에 추가 사용자 정보가 수집 되었으므로 `CreatedUser` 이벤트 처리기를 업데이트 하 여 이러한 입력을 검색 하 고 `DBNull.Value`대신 `INSERT` 문의 매개 변수 값에 사용 해야 합니다.

[추가 WizardStep가 CreateUserWizardStep 앞에 CreateUserWizard 워크플로를 ![합니다.](storing-additional-user-information-cs/_static/image62.png)](storing-additional-user-information-cs/_static/image61.png)

**그림 21**: 추가 `WizardStep` `CreateUserWizardStep` 앞에 있는 CreateUserWizard 워크플로 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image63.png))

그러나 사용자 지정 `WizardStep` `CreateUserWizardStep`*뒤* 에 배치 되는 경우 사용자가 자신의 집 마을, 홈페이지 또는 서명을 입력할 수 있기 전에 사용자 계정 만들기 프로세스가 수행 됩니다. 이 경우 그림 22와 같이 사용자 계정을 만든 후이 추가 정보를 데이터베이스에 삽입 해야 합니다.

[추가 WizardStep가 CreateUserWizardStep 뒤에 나오면 CreateUserWizard 워크플로를 ![합니다.](storing-additional-user-information-cs/_static/image65.png)](storing-additional-user-information-cs/_static/image64.png)

**그림 22**: `CreateUserWizardStep` 후에 추가 `WizardStep` 되는 경우의 CreateUserWizard 워크플로 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image66.png))

그림 22에 표시 된 워크플로는 2 단계가 완료 될 때까지 `UserProfiles` 테이블에 레코드를 삽입 하기 위해 대기 합니다. 그러나 방문자가 1 단계를 수행한 후 브라우저를 닫으면 사용자 계정이 생성 되었지만 `UserProfiles`에 레코드가 추가 되지 않은 상태에 도달 하 게 됩니다. 한 가지 해결 방법은 1 단계 후에 발생 하는 `CreatedUser` 이벤트 처리기의 `UserProfiles`에 `NULL` 또는 기본값이 삽입 된 레코드를 포함 하 고 2 단계를 완료 한 후이 레코드를 업데이트 하는 것입니다. 이렇게 하면 사용자가 중간에 등록 프로세스를 종료 하는 경우에도 사용자 계정에 대 한 `UserProfiles` 레코드가 추가 됩니다.

이 자습서에서는 `CreateUserWizardStep` 이후에 발생 하지만 `CompleteWizardStep`이전에 발생 하는 새 `WizardStep`를 만들어 보겠습니다. 먼저 WizardStep을 준비 하 고 구성 하 고 코드를 살펴보겠습니다.

CreateUserWizard 컨트롤의 스마트 태그에서 `WizardStep` 컬렉션 편집기 대화 상자를 표시 하는 "추가/제거 `WizardStep` s"를 선택 합니다. 새 `WizardStep`을 추가 하 고, 해당 `ID`를 `UserSettings`로 설정 하 고, 해당 `Title`를 "설정"으로 설정 하 고 `StepType`를 `Step`로 설정 합니다. 그런 다음 그림 23과 같이 `CreateUserWizardStep` ("새 계정에 등록") 및 `CompleteWizardStep` ("완료") 앞에 오도록 배치 합니다.

[새 WizardStep를 CreateUserWizard 컨트롤에 추가 ![](storing-additional-user-information-cs/_static/image68.png)](storing-additional-user-information-cs/_static/image67.png)

**그림 23**: CreateUserWizard 컨트롤에 새 `WizardStep` 추가 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image69.png))

확인을 클릭 하 여 `WizardStep` 컬렉션 편집기 대화 상자를 닫습니다. 새 `WizardStep`는 CreateUserWizard 컨트롤의 업데이트 된 선언적 태그로 복합적 됩니다.

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample13.aspx)]

새 `<asp:WizardStep>` 요소를 확인 합니다. 여기에서 새 사용자의 홈 타운, 홈 페이지 및 서명을 수집 하려면 사용자 인터페이스를 추가 해야 합니다. 이 콘텐츠는 선언적 구문이 나 디자이너를 통해 입력할 수 있습니다. 디자이너를 사용 하려면 스마트 태그의 드롭다운 목록에서 "사용자 설정" 단계를 선택 하 여 디자이너의 단계를 확인 합니다.

> [!NOTE]
> 스마트 태그의 드롭다운 목록에서 단계를 선택 하면 시작 단계의 인덱스를 지정 하는 CreateUserWizard 컨트롤의 [`ActiveStepIndex` 속성이](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.activestepindex.aspx)업데이트 됩니다. 따라서이 드롭다운 목록을 사용 하 여 디자이너의 "설정" 단계를 편집 하는 경우 사용자가 `EnhancedCreateUserWizard.aspx` 페이지를 처음 방문할 때이 단계가 표시 되도록 "새 계정에 등록"으로 다시 설정 해야 합니다.

`HomeTown`, `HomepageUrl`및 `Signature`라는 세 개의 TextBox 컨트롤을 포함 하는 "사용자 설정" 단계 내에서 사용자 인터페이스를 만듭니다. 이 인터페이스를 생성 한 후에는 CreateUserWizard의 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample14.aspx)]

계속 해 서 브라우저를 통해이 페이지를 방문 하 고 홈 타운, 홈 페이지 및 서명에 대 한 값을 지정 하 여 새 사용자 계정을 만듭니다. `CreateUserWizardStep` 완료 한 후에는 멤버 프레임 워크에서 사용자 계정을 만들고 `CreatedUser` 이벤트 처리기를 실행 합니다. 그러면 `UserProfiles`에 새 행이 추가 되지만 `HomeTown`, `HomepageUrl`, `Signature`에 대 한 데이터베이스 `NULL` 값이 사용 됩니다. 홈 타운, 홈 페이지 및 서명에 입력 한 값은 사용 되지 않습니다. Net result는 `HomeTown`, `HomepageUrl`및 `Signature` 필드를 아직 지정 하지 않은 `UserProfiles` 레코드를 포함 하는 새 사용자 계정입니다.

사용자가 입력 한 집 타운, honepage 및 서명 값을 사용 하 고 적절 한 `UserProfiles` 레코드를 업데이트 하는 "사용자 설정" 단계 후에 코드를 실행 해야 합니다. 사용자가 마법사 컨트롤의 단계 간을 이동할 때마다 마법사의 [`ActiveStepChanged` 이벤트가](https://msdn.microsoft.com/library/system.web.ui.webcontrols.wizard.activestepchanged.aspx) 발생 합니다. "설정" 단계가 완료 되 면이 이벤트에 대 한 이벤트 처리기를 만들고 `UserProfiles` 테이블을 업데이트할 수 있습니다.

CreateUserWizard의 `ActiveStepChanged` 이벤트에 대 한 이벤트 처리기를 추가 하 고 다음 코드를 추가 합니다.

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample15.cs)]

위의 코드는 단순히 "완료" 단계에 도달 했는지 확인 하 여 시작 합니다. "전체" 단계는 "사용자 설정" 단계 바로 다음에 발생 하므로 방문자가 "전체" 단계에 도달 하면 "설정" 단계를 완료 했다는 것을 의미 합니다.

이 경우 `UserSettings WizardStep`내에서 TextBox 컨트롤을 프로그래밍 방식으로 참조 해야 합니다. 이를 위해서는 먼저 `FindControl` 메서드를 사용 하 여 `UserSettings WizardStep`를 프로그래밍 방식으로 참조 한 다음 `WizardStep`내에서 텍스트 상자를 참조 합니다. 텍스트 상자가 참조 되 면 `UPDATE` 문을 실행할 준비가 된 것입니다. `UPDATE` 문에는 `CreatedUser` 이벤트 처리기의 `INSERT` 문과 동일한 수의 매개 변수가 있지만 여기서는 사용자가 제공 하는 홈 타운, 홈 페이지 및 서명 값을 사용 합니다.

이 이벤트 처리기를 사용 하는 경우 브라우저를 통해 `EnhancedCreateUserWizard.aspx` 페이지를 방문 하 고 홈 타운, 홈 페이지 및 서명 값을 지정 하는 새 사용자 계정을 만듭니다. 새 계정을 만든 후에는 방금 입력 한 홈 타운, 홈 페이지 및 서명 정보가 표시 되는 `AdditionalUserInfo.aspx` 페이지로 리디렉션됩니다.

> [!NOTE]
> 현재 웹 사이트에는 방문자가 새 계정을 만들 수 있는 두 페이지가 있습니다. `CreatingUserAccounts.aspx` 및 `EnhancedCreateUserWizard.aspx`. 웹 사이트의 사이트 맵 및 로그인 페이지가 `CreatingUserAccounts.aspx` 페이지를 가리키기는 하지만 `CreatingUserAccounts.aspx` 페이지에서 사용자에 게 홈 타운, 홈 페이지 및 서명 정보를 입력 하 라는 메시지를 표시 하지 않고 `UserProfiles`에 해당 행을 추가 하지 않습니다. 따라서 `CreatingUserAccounts.aspx` 페이지를 업데이트 하 여이 기능을 제공 하거나 사이트 맵 및 로그인 페이지에서 `CreatingUserAccounts.aspx`대신 `EnhancedCreateUserWizard.aspx`를 참조 하도록 업데이트 합니다. 후자 옵션을 선택 하는 경우 `EnhancedCreateUserWizard.aspx` 페이지에 대 한 익명 사용자의 액세스를 허용 하도록 `Membership` 폴더의 `Web.config` 파일을 업데이트 해야 합니다.

## <a name="summary"></a>요약

이 자습서에서는 멤버 자격 프레임 워크 내에서 사용자 계정과 관련 된 데이터를 모델링 하는 기술을 살펴보았습니다. 특히 사용자 계정과 일 대 다 관계를 공유 하는 엔터티와 일 대 일 관계를 공유 하는 데이터를 모델링 하는 방법을 살펴보았습니다. 또한 SqlDataSource 컨트롤을 사용 하는 몇 가지 예제와 ADO.NET 코드를 사용 하 여이 관련 정보를 표시, 삽입 및 업데이트 하는 방법을 살펴보았습니다.

이 자습서에서는 사용자 계정에 대 한 확인을 완료 합니다. 다음 자습서부터 역할에 주의를 기울여야 합니다. 다음 몇 가지 자습서에서는 역할 프레임 워크에서 새로운 역할을 만드는 방법, 사용자에 게 역할을 할당 하는 방법, 사용자가 속한 역할을 결정 하는 방법, 역할 기반 권한 부여를 적용 하는 방법을 참조 하세요.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 참고 자료

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 2.0에서 데이터 액세스 및 업데이트](http://aspnet.4guysfromrolla.com/articles/011106-1.aspx)
- [ASP.NET 2.0 마법사 컨트롤](https://weblogs.asp.net/scottgu/archive/2006/02/21/438732.aspx)
- [ASP.NET 2.0 마법사 컨트롤을 사용 하 여 단계별 사용자 인터페이스 만들기](http://aspnet.4guysfromrolla.com/articles/061406-1.aspx)
- [사용자 지정 DataSource 컨트롤 매개 변수 만들기](http://aspnet.4guysfromrolla.com/articles/110106-1.aspx)
- [CreateUserWizard 컨트롤 사용자 지정](http://aspnet.4guysfromrolla.com/articles/070506-1.aspx)
- [DetailsView 컨트롤 빠른 시작](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/data/detailsview.aspx)
- [ListView 컨트롤을 사용 하 여 데이터 표시](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)
- [ASP.NET 2.0에서 유효성 검사 컨트롤 개로 나누어서](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)
- [삽입 및 데이터 삭제 편집](../../data-access/editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)
- [ASP.NET의 폼 유효성 검사](http://www.4guysfromrolla.com/webtech/090200-1.shtml)
- [사용자 지정 사용자 등록 정보 수집](https://weblogs.asp.net/scottgu/archive/2006/07/05/Tip_2F00_Trick_3A00_-Gathering-Custom-User-Registration-Information.aspx)
- [ASP.NET 2.0의 프로필](http://www.odetocode.com/Articles/440.aspx)
- [Asp: ListView 컨트롤](https://weblogs.asp.net/scottgu/archive/2007/08/10/the-asp-listview-control-part-1-building-a-product-listing-page-with-clean-css-ui.aspx)
- [사용자 프로필 빠른 시작](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/profile/default.aspx)

### <a name="about-the-author"></a>저자 정보

Scott Mitchell는 여러 ASP/ASP. NET books의 작성자와 4GuysFromRolla.com의 창립자가 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 *[24 시간 이내에 ASP.NET 2.0을 sams teach yourself](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 것입니다. Scott은 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) 또는 [http://ScottOnWriting.NET](http://scottonwriting.net/)의 블로그를 통해 연결할 수 있습니다.

### <a name="special-thanks-to"></a>특별 해 주셔서 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)에서 줄을 삭제 합니다.

> [!div class="step-by-step"]
> [이전](user-based-authorization-cs.md)
> [다음](creating-the-membership-schema-in-sql-server-vb.md)
