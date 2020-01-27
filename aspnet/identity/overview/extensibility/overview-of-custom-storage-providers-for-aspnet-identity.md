---
uid: identity/overview/extensibility/overview-of-custom-storage-providers-for-aspnet-identity
title: ASP.NET Identity에 대 한 사용자 지정 저장소 공급자 개요-ASP.NET 4.x
author: Rick-Anderson
description: ASP.NET Identity는 사용자 고유의 저장소 공급자를 만들어 응용 프로그램에 연결 하는 데 사용할 수 있는 확장 가능한 시스템입니다.
ms.author: riande
ms.date: 10/13/2014
ms.assetid: 681a9204-462e-4260-9a0b-19f0644d6ad7
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/extensibility/overview-of-custom-storage-providers-for-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 21baedf6285b411f89627df9ca25d47a2a42e387
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519104"
---
# <a name="overview-of-custom-storage-providers-for-aspnet-identity"></a>ASP.NET Identity에 대한 사용자 지정 스토리지 공급자 개요

[Tom FitzMacken](https://github.com/tfitzmac)

> ASP.NET Identity는 사용자 고유의 저장소 공급자를 만들고 응용 프로그램을 다시 작동 시 키 지 않고도 응용 프로그램에 연결할 수 있도록 하는 확장 가능한 시스템입니다. 이 항목에서는 ASP.NET Identity에 대 한 사용자 지정 저장소 공급자를 만드는 방법에 대해 설명 합니다. 사용자 고유의 저장소 공급자를 만드는 데 중요 한 개념을 다루지만 사용자 지정 저장소 공급자를 구현 하는 단계별 연습은 제공 하지 않습니다.
> 
> 사용자 지정 저장소 공급자를 구현 하는 예제는 [사용자 지정 MySQL ASP.NET Identity 저장소 공급자 구현](implementing-a-custom-mysql-aspnet-identity-storage-provider.md)을 참조 하세요.
> 
> 이 항목은 ASP.NET Identity 2.0에 대해 업데이트 되었습니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - Visual Studio 2013 업데이트 2
> - ASP.NET Identity 2

## <a name="introduction"></a>소개

기본적으로 ASP.NET Identity 시스템은 SQL Server 데이터베이스에 사용자 정보를 저장 하 고 Entity Framework Code First를 사용 하 여 데이터베이스를 만듭니다. 많은 응용 프로그램에서이 접근 방식은 잘 작동 합니다. 그러나 Azure Table Storage와 같은 다른 형식의 지 속성 메커니즘을 사용 하거나, 기본 구현과 매우 다른 데이터베이스 테이블이 이미 있을 수 있습니다. 두 경우 모두 저장소 메커니즘에 맞게 사용자 지정 된 공급자를 작성 하 고 해당 공급자를 응용 프로그램에 연결할 수 있습니다.

ASP.NET Identity는 대부분의 Visual Studio 2013 템플릿에 기본적으로 포함 되어 있습니다. [Microsoft AspNet Identity EntityFramework NuGet 패키지](http://www.nuget.org/packages/Microsoft.AspNet.Identity.EntityFramework/)를 통해 ASP.NET Identity에 대 한 업데이트를 가져올 수 있습니다.

이 항목은 다음과 같은 섹션으로 구성됩니다.

- [아키텍처 이해](#architecture)
- [저장 되는 데이터 이해](#data)
- [데이터 액세스 계층 만들기](#dal)
- [사용자 클래스 사용자 지정](#user)
- [사용자 저장소 사용자 지정](#userstore)
- [Role 클래스 사용자 지정](#role)
- [역할 저장소 사용자 지정](#rolestore)
- [새 저장소 공급자를 사용 하도록 응용 프로그램 다시 구성](#reconfigure)
- [사용자 지정 저장소 공급자의 기타 구현](#other)

<a id="architecture"></a>
## <a name="understand-the-architecture"></a>아키텍처 이해

ASP.NET Identity는 관리자 및 저장소 라는 클래스로 구성 됩니다. 관리자는 응용 프로그램 개발자가 ASP.NET Identity 시스템에서 사용자 만들기와 같은 작업을 수행 하는 데 사용 하는 개략적인 클래스입니다. 저장소는 사용자 및 역할과 같은 엔터티를 유지 하는 방법을 지정 하는 하위 수준 클래스입니다. 저장소는 지 속성 메커니즘과 긴밀 하 게 연관 되어 있지만 관리자가 저장소에서 분리 되어 있으므로 전체 응용 프로그램을 중단 하지 않고 지 속성 메커니즘을 대체할 수 있습니다.

다음 다이어그램에서는 웹 응용 프로그램이 관리자와 상호 작용 하는 방식과 데이터 액세스 계층과 상호 작용 하는 방법을 보여 줍니다.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image1.png)

ASP.NET Identity에 대 한 사용자 지정 저장소 공급자를 만들려면 데이터 원본, 데이터 액세스 계층 및이 데이터 액세스 계층과 상호 작용 하는 저장소 클래스를 만들어야 합니다. 동일한 관리자 Api를 계속 사용 하 여 사용자에 대 한 데이터 작업을 수행할 수 있지만 이제 데이터는 다른 저장소 시스템에 저장 됩니다.

UserManager 또는 RoleManager의 새 인스턴스를 만들 때 사용자 클래스의 형식을 제공 하 고 저장소 클래스의 인스턴스를 인수로 전달 하므로 관리자 클래스를 사용자 지정할 필요가 없습니다. 이 접근 방식을 사용 하면 사용자 지정 클래스를 기존 구조에 연결할 수 있습니다. [새 저장소 공급자를 사용 하도록 응용 프로그램 다시 구성](#reconfigure)섹션에서 사용자 지정 저장소 클래스로 usermanager 및 RoleManager를 인스턴스화하는 방법을 확인할 수 있습니다.

<a id="data"></a>
## <a name="understand-the-data-that-is-stored"></a>저장 되는 데이터 이해

사용자 지정 저장소 공급자를 구현 하려면 ASP.NET Identity에 사용 되는 데이터 형식을 이해 하 고 응용 프로그램과 관련 된 기능을 결정 해야 합니다.

| 데이터 | 설명 |
| --- | --- |
| Users | 웹 사이트의 등록 된 사용자입니다. 사용자 Id와 사용자 이름을 포함 합니다. 사용자가 Facebook 등의 외부 사이트에서 자격 증명을 사용 하는 대신 사이트와 관련 된 자격 증명을 사용 하 여 로그인 하 고 사용자 자격 증명에서 변경 내용이 있는지 여부를 나타내는 보안 스탬프를 사용 하 여 로그인 하는 경우 해시 된 암호를 포함할 수 있습니다. 전자 메일 주소, 전화 번호, 2 단계 인증을 사용 하는지 여부, 현재 실패 한 로그인 횟수 및 계정이 잠겨 있는지 여부를 포함할 수도 있습니다. |
| 사용자 클레임 | 사용자의 id를 나타내는 사용자에 대 한 문 (또는 클레임) 집합입니다. 에서는 역할을 통해 달성할 수 있는 것 보다 더 큰 사용자 id 식을 사용할 수 있습니다. |
| 사용자 로그인 | 사용자에 게 로그인 할 때 사용할 외부 인증 공급자 (예: Facebook)에 대 한 정보입니다. |
| 역할 | 사이트에 대 한 권한 부여 그룹. 역할 Id와 역할 이름 (예: "Admin" 또는 "Employee")을 포함 합니다. |

<a id="dal"></a>
## <a name="create-the-data-access-layer"></a>데이터 액세스 계층 만들기

이 항목에서는 사용자가 사용 하려는 지 속성 메커니즘 및 해당 메커니즘에 대 한 엔터티를 만드는 방법을 잘 알고 있다고 가정 합니다. 이 항목에서는 리포지토리 또는 데이터 액세스 클래스를 만드는 방법에 대 한 자세한 정보는 제공 하지 않습니다. 대신 ASP.NET Identity 작업할 때 결정 해야 하는 디자인 결정에 대 한 몇 가지 제안을 제공 합니다.

사용자 지정 저장소 공급자에 대 한 리포지토리를 설계할 때 자유롭게 자유롭게 사용할 수 있습니다. 응용 프로그램에서 사용 하려는 기능에 대 한 리포지토리를 만들어야 합니다. 예를 들어 응용 프로그램에서 역할을 사용 하지 않는 경우 역할 또는 사용자 역할에 대 한 저장소를 만들 필요가 없습니다. 기술 및 기존 인프라에는 ASP.NET Identity의 기본 구현과 매우 다른 구조가 필요할 수 있습니다. 데이터 액세스 계층에서 리포지토리의 구조를 사용 하는 논리를 제공 합니다.

ASP.NET Identity 2.0에 대 한 데이터 리포지토리의 MySQL 구현에 대해서는 [MySQLIdentity](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql)을 참조 하세요.

데이터 액세스 계층에서 데이터 원본에 ASP.NET Identity 데이터를 저장 하는 논리를 제공 합니다. 사용자 지정 저장소 공급자에 대 한 데이터 액세스 계층에는 사용자 및 역할 정보를 저장 하는 다음과 같은 클래스가 포함 될 수 있습니다.

| 클래스 | 설명 | 예 |
| --- | --- | --- |
| 컨텍스트 | 정보를 캡슐화 하 여 지 속성 메커니즘에 연결 하 고 쿼리를 실행 합니다. 이 클래스는 데이터 액세스 계층의 핵심입니다. 다른 데이터 클래스에는이 클래스의 인스턴스가 있어야 작업을 수행할 수 있습니다. 또한이 클래스의 인스턴스를 사용 하 여 저장소 클래스를 초기화 합니다. | [MySQLDatabase](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) |
| 사용자 저장소 | 사용자 정보 (예: 사용자 이름 및 암호 해시)를 저장 하 고 검색 합니다. | [UserTable (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserTable.cs) |
| 역할 저장소 | 역할 이름 등의 역할 정보를 저장 하 고 검색 합니다. | [RoleTable (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleTable.cs) |
| UserClaims 저장소 | 사용자 클레임 정보 (예: 클레임 유형 및 값)를 저장 하 고 검색 합니다. | [UserClaimsTable (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) |
| UserLogins 저장소 | 사용자 로그인 정보 (예: 외부 인증 공급자)를 저장 하 고 검색 합니다. | [UserLoginsTable (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) |
| UserRole 저장소 | 사용자가 할당 된 역할을 저장 하 고 검색 합니다. | [UserRoleTable (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) |

응용 프로그램에서 사용 하려는 클래스만 구현 하면 됩니다.

데이터 액세스 클래스에서 특정 지 속성 메커니즘에 대 한 데이터 작업을 수행 하는 코드를 제공 합니다. 예를 들어 MySQL 구현 내에서 UserTable 클래스는 사용자 데이터베이스 테이블에 새 레코드를 삽입 하는 메서드를 포함 합니다. `_database` 라는 변수는 MySQLDatabase 클래스의 인스턴스입니다.

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample1.cs)]

데이터 액세스 클래스를 만든 후에는 데이터 액세스 계층의 특정 메서드를 호출 하는 저장소 클래스를 만들어야 합니다.

<a id="user"></a>
## <a name="customize-the-user-class"></a>사용자 클래스 사용자 지정

사용자 고유의 저장소 공급자를 구현 하는 경우 IdentityUser [프레임 워크](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework(v=vs.108).aspx) 네임 스페이스의 [클래스에 해당 하는 사용자 ](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework.identityuser(v=vs.108).aspx) 클래스를 만들어야 합니다.

다음 다이어그램에서는 만들어야 하는 IdentityUser 클래스와이 클래스에서 구현할 인터페이스를 보여 줍니다.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image2.png)

[IUser&lt;TKey&gt;](https://msdn.microsoft.com/library/dn613291(v=vs.108).aspx) 인터페이스는 요청 된 작업을 수행할 때 usermanager가 호출 하려고 하는 속성을 정의 합니다. 인터페이스에는 Id 및 사용자 이름의 두 속성이 포함 되어 있습니다. [IUser&lt;TKey&gt;](https://msdn.microsoft.com/library/dn613291(v=vs.108).aspx) 인터페이스를 사용 하 여 일반 **TKey** 매개 변수를 통해 사용자의 키 형식을 지정할 수 있습니다. Id 속성의 유형이 TKey 매개 변수의 값과 일치 합니다.

또한 Id 프레임 워크는 키에 문자열 값을 사용 하려는 경우 제네릭 매개 변수 없이 [IUser](https://msdn.microsoft.com/library/microsoft.aspnet.identity.iuser(v=vs.108).aspx) 인터페이스를 제공 합니다.

IdentityUser 클래스는 IUser를 구현 하 고 웹 사이트의 사용자에 대 한 추가 속성 또는 생성자를 포함 합니다. 다음 예제에서는 키에 정수를 사용 하는 IdentityUser 클래스를 보여 줍니다. Id 필드는 제네릭 매개 변수의 값과 일치 하도록 **int** 로 설정 됩니다. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample2.cs)]

 완전 한 구현은 [IdentityUser (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityUser.cs)를 참조 하세요. 

<a id="userstore"></a>
## <a name="customize-the-user-store"></a>사용자 저장소 사용자 지정

또한 사용자에 대 한 모든 데이터 작업에 대해 메서드를 제공 하는 UserStore 클래스를 만듭니다. 이 클래스는 [MICROSOFT .asp. id](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework(v=vs.108).aspx) 네임 스페이스의 [Userstore&lt;tuser&gt;](https://msdn.microsoft.com/library/dn315446(v=vs.108).aspx) 클래스와 동일 합니다. UserStore 클래스에서 [iuserstore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613276(v=vs.108).aspx) 및 선택적 인터페이스를 구현 합니다. 응용 프로그램에서 제공 하려는 기능을 기준으로 구현할 선택적 인터페이스를 선택 합니다.

다음 그림은 만들어야 하는 UserStore 클래스와 관련 인터페이스를 보여 줍니다.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image3.png)

Visual Studio의 기본 프로젝트 템플릿에는 많은 선택적 인터페이스가 사용자 저장소에 구현 된 것으로 가정 하는 코드가 포함 되어 있습니다. 사용자 지정 된 사용자 저장소를 사용 하 여 기본 템플릿을 사용 하는 경우 사용자 저장소에 선택적 인터페이스를 구현 하거나 구현 하지 않은 인터페이스에서 더 이상 메서드를 호출 하지 않도록 템플릿 코드를 변경 해야 합니다.

 다음 예제에서는 간단한 사용자 저장소 클래스를 보여 줍니다. **Tuser** 제네릭 매개 변수는 사용자 클래스의 형식 (일반적으로 정의한 IdentityUser 클래스)을 사용 합니다. **TKey** 제네릭 매개 변수는 사용자 키의 유형을 사용 합니다. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample3.cs)]

 이 예제에서 ExampleDatabase 형식의 *데이터베이스* 라는 매개 변수를 사용 하는 생성자는 데이터 액세스 클래스를 전달 하는 방법을 보여 주는 것입니다. 예를 들어 MySQL 구현에서이 생성자는 MySQLDatabase 형식의 매개 변수를 사용 합니다. 

UserStore 클래스 내에서 작업을 수행 하기 위해 만든 데이터 액세스 클래스를 사용 합니다. 예를 들어 MySQL 구현에서 UserStore 클래스는 Userstore의 인스턴스를 사용 하 여 새 레코드를 삽입 하는 CreateAsync 메서드를 포함 합니다. **Usertable** 개체의 **Insert** 메서드는 이전 섹션에 표시 된 것과 동일한 메서드입니다. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample4.cs)]

### <a name="interfaces-to-implement-when-customizing-user-store"></a>사용자 저장소를 사용자 지정할 때 구현할 인터페이스

다음 이미지는 각 인터페이스에 정의 된 기능에 대 한 자세한 정보를 보여 줍니다. 모든 선택적 인터페이스는 IUserStore에서 상속 됩니다.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image4.png)

- **IUserStore**  
  [Iuserstore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613278(v=vs.108).aspx) 인터페이스만 사용자 저장소에서 구현 해야 하는 인터페이스입니다. 사용자를 만들고, 업데이트 하 고, 삭제 하 고, 검색 하는 메서드를 정의 합니다.
- **IUserClaimStore**  
  [Iuserclaimstore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613265(v=vs.108).aspx) 인터페이스는 사용자 클레임을 사용 하기 위해 사용자 저장소에 구현 해야 하는 메서드를 정의 합니다. 사용자 클레임을 추가, 제거 및 검색 하는 메서드를 포함 합니다.
- **IUserLoginStore**  
  [IUserLoginStore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613272(v=vs.108).aspx) 는 외부 인증 공급자를 사용 하기 위해 사용자 저장소에 구현 해야 하는 메서드를 정의 합니다. 사용자 로그인을 추가, 제거 및 검색 하는 메서드와 로그인 정보를 기반으로 사용자를 검색 하는 방법이 포함 되어 있습니다.
- **IUserRoleStore**  
  [Iuserrolestore&lt;TKey, TUser&gt;](https://msdn.microsoft.com/library/dn613276(v=vs.108).aspx) 인터페이스는 사용자를 역할에 매핑하기 위해 사용자 저장소에 구현 해야 하는 메서드를 정의 합니다. 사용자의 역할을 추가, 제거 및 검색 하는 메서드와 사용자가 역할에 할당 되었는지 여부를 확인 하는 메서드가 포함 되어 있습니다.
- **IUserPasswordStore**  
  [Iuserpasswordstore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613273(v=vs.108).aspx) 인터페이스는 해시 된 암호를 유지 하기 위해 사용자 저장소에 구현 해야 하는 메서드를 정의 합니다. 해시 된 암호를 가져오고 설정 하는 메서드와 사용자가 암호를 설정 했는지 여부를 나타내는 메서드를 포함 합니다.
- **IUserSecurityStampStore**  
  [IUserSecurityStampStore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613277(v=vs.108).aspx) 인터페이스는 사용자 계정 정보가 변경 되었는지 여부를 나타내는 데 보안 스탬프를 사용 하기 위해 사용자 저장소에서 구현 해야 하는 메서드를 정의 합니다. 이 스탬프는 사용자가 암호를 변경 하거나 로그인을 추가 하거나 제거 하는 경우 업데이트 됩니다. 보안 스탬프를 가져오고 설정 하기 위한 메서드를 포함 합니다.
- **IUserTwoFactorStore**  
  [IUserTwoFactorStore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613279(v=vs.108).aspx) 인터페이스는 2 단계 인증을 구현 하기 위해 구현 해야 하는 메서드를 정의 합니다. 사용자에 대해 2 단계 인증을 사용할 수 있는지 여부를 가져오고 설정 하는 메서드를 포함 합니다.
- **IUserPhoneNumberStore**  
  [IUserPhoneNumberStore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613275(v=vs.108).aspx) 인터페이스는 사용자 전화 번호를 저장 하기 위해 구현 해야 하는 메서드를 정의 합니다. 전화 번호를 가져오고 설정 하는 방법 및 전화 번호가 확인 되었는지 여부를 나타내는 메서드가 포함 되어 있습니다.
- **IUserEmailStore**  
  [Iuseremailstore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613143(v=vs.108).aspx) 인터페이스는 사용자 전자 메일 주소를 저장 하기 위해 구현 해야 하는 메서드를 정의 합니다. 전자 메일 주소를 가져오고 설정 하는 방법과 전자 메일이 확인 되었는지 여부를 나타내는 메서드가 포함 되어 있습니다.
- **IUserLockoutStore**  
  [IUserLockoutStore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613271(v=vs.108).aspx) 인터페이스는 계정 잠금에 대 한 정보를 저장 하기 위해 구현 해야 하는 메서드를 정의 합니다. 현재 실패 한 액세스 시도 횟수를 가져오고, 계정을 잠글 수 있는지 여부를 가져오거나 설정 하 고, 잠금 종료 날짜를 가져오고 설정 하 고, 실패 한 시도 횟수를 증가 시키고, 실패 한 시도 횟수를 다시 설정 하는 메서드를 포함 합니다.
- **IQueryableUserStore**  
  [Iqueryableuserstore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613267(v=vs.108).aspx) 인터페이스는 쿼리 가능한 사용자 저장소를 제공 하기 위해 구현 해야 하는 멤버를 정의 합니다. 쿼리 가능한 사용자를 포함 하는 속성을 포함 합니다.

  응용 프로그램에 필요한 인터페이스를 구현 합니다. 예를 들어 다음과 같이 IUserClaimStore, IUserLoginStore, Iuserclaimstore, Iuserclaimstore, IUserSecurityStampStore 인터페이스 등이 있습니다. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample5.cs)]

모든 인터페이스를 포함 한 전체 구현에 대 한 자세한 내용은 [Userstore (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserStore.cs)를 참조 하세요.

### <a name="identityuserclaim-identityuserlogin-and-identityuserrole"></a>IdentityUserClaim, IdentityUserLogin 및 IdentityUserRole

[IdentityUserClaim](https://msdn.microsoft.com/library/dn613250(v=vs.108).aspx), [IdentityUserLogin](https://msdn.microsoft.com/library/dn613251(v=vs.108).aspx)및 [IdentityUserRole](https://msdn.microsoft.com/library/dn613252(v=vs.108).aspx) 클래스의 구현을 포함 하는 Microsoft. 이러한 기능을 사용 하는 경우 이러한 클래스의 고유한 버전을 만들고 응용 프로그램에 대 한 속성을 정의 하는 것이 좋습니다. 그러나 기본 작업 (예: 사용자의 클레임 추가 또는 제거)을 수행할 때 이러한 엔터티를 메모리로 로드 하지 않는 것이 더 효율적일 수 있습니다. 대신 백엔드 저장소 클래스는 데이터 소스에서 이러한 작업을 직접 실행할 수 있습니다. 예를 들어 Userstore () 메서드는 UserclaimFindByUserId (user)를 호출할 수 있습니다. Id) 메서드는 해당 테이블에 대 한 쿼리를 직접 실행 하 고 클레임 목록을 반환 합니다.

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample6.cs)]

<a id="role"></a>
## <a name="customize-the-role-class"></a>Role 클래스 사용자 지정

사용자 고유의 저장소 공급자를 구현 하는 경우 [IdentityRole](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework.identityrole(v=vs.108).aspx) [프레임 워크](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework(v=vs.108).aspx) 네임 스페이스의  클래스에 해당 하는 역할 클래스를 만들어야 합니다.

다음 다이어그램에서는 만들어야 하는 IdentityRole 클래스와이 클래스에서 구현할 인터페이스를 보여 줍니다.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image5.png)

[Irole&lt;TKey&gt;](https://msdn.microsoft.com/library/dn613268(v=vs.108).aspx) 인터페이스는 요청 된 작업을 수행할 때 RoleManager에서 호출 하려고 하는 속성을 정의 합니다. 인터페이스에는 Id와 이름 이라는 두 가지 속성이 있습니다. [Irole&lt;TKey&gt;](https://msdn.microsoft.com/library/dn613268(v=vs.108).aspx) 인터페이스를 사용 하 여 일반 **TKey** 매개 변수를 통해 역할의 키 형식을 지정할 수 있습니다. Id 속성의 유형이 TKey 매개 변수의 값과 일치 합니다.

또한 Id 프레임 워크는 키에 문자열 값을 사용 하려는 경우 제네릭 매개 변수 없이 [Irole](https://msdn.microsoft.com/library/microsoft.aspnet.identity.irole(v=vs.108).aspx) 인터페이스를 제공 합니다.

다음 예제에서는 키에 정수를 사용 하는 IdentityRole 클래스를 보여 줍니다. Id 필드는 제네릭 매개 변수의 값과 일치 하도록 int로 설정 됩니다. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample7.cs)]

 완전 한 구현은 [IdentityRole (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityRole.cs)를 참조 하세요. 

<a id="rolestore"></a>
## <a name="customize-the-role-store"></a>역할 저장소 사용자 지정

또한 역할에 대 한 모든 데이터 작업에 대해 메서드를 제공 하는 RoleStore 클래스를 만듭니다. 이 클래스는 Microsoft .ASP. Id 네임 스페이스의 [Rolestore&lt;TRole&gt;](https://msdn.microsoft.com/library/dn468181(v=vs.108).aspx) 클래스와 동일 합니다. RoleStore 클래스에서 [Irolestore&lt;TRole, tkey&gt;](https://msdn.microsoft.com/library/dn613266(v=vs.108).aspx) 및 선택적으로 [IQueryableRoleStore&lt;trole, tkey&gt;](https://msdn.microsoft.com/library/dn613262(v=vs.108).aspx) 인터페이스를 구현 합니다.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image6.png)

다음 예제에서는 역할 저장소 클래스를 보여 줍니다. TRole 제네릭 매개 변수는 일반적으로 정의한 IdentityRole 클래스인 역할 클래스의 형식을 사용 합니다. TKey 제네릭 매개 변수는 역할 키의 유형을 사용 합니다. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample8.cs)]

- **IRoleStore&lt;TRole&gt;**  
  [Irolestore](https://msdn.microsoft.com/library/dn468195.aspx) 인터페이스는 역할 저장소 클래스에서 구현 하는 메서드를 정의 합니다. 역할을 만들고, 업데이트 하 고, 삭제 하 고, 검색 하는 메서드가 포함 되어 있습니다.
- **RoleStore&lt;TRole&gt;**  
  RoleStore를 사용자 지정 하려면 IRoleStore 인터페이스를 구현 하는 클래스를 만듭니다. 시스템에서 역할을 사용 하려는 경우에만이 클래스를 구현 해야 합니다. ExampleDatabase 형식의 *데이터베이스* 라는 매개 변수를 사용 하는 생성자는 데이터 액세스 클래스를 전달 하는 방법을 보여 주는 것입니다. 예를 들어 MySQL 구현에서이 생성자는 MySQLDatabase 형식의 매개 변수를 사용 합니다.  
  
  완전 한 구현은 [Rolestore (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleStore.cs) 를 참조 하세요.

<a id="reconfigure"></a>
## <a name="reconfigure-application-to-use-new-storage-provider"></a>새 저장소 공급자를 사용 하도록 응용 프로그램 다시 구성

새 저장소 공급자를 구현 했습니다. 이제이 저장소 공급자를 사용 하도록 응용 프로그램을 구성 해야 합니다. 기본 저장소 공급자가 프로젝트에 포함 된 경우 기본 공급자를 제거 하 고 공급자로 바꾸어야 합니다.

### <a name="replace-default-storage-provider-in-mvc-project"></a>MVC 프로젝트에서 기본 저장소 공급자 바꾸기

1. **NuGet 패키지 관리** 창에서 **Microsoft ASP.NET id entityframework** 패키지를 제거 합니다. Id. EntityFramework에 대해 설치 된 패키지를 검색 하 여이 패키지를 찾을 수 있습니다.  
    ![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image7.png) Entity Framework를 제거할지 묻는 메시지가 표시 됩니다. 응용 프로그램의 다른 부분에 필요 하지 않은 경우 제거할 수 있습니다.
2. 모델 폴더의 IdentityModels.cs 파일에서 **Applicationuser** 및 **ApplicationDbContext** 클래스를 삭제 하거나 주석으로 처리 합니다. MVC 응용 프로그램에서 전체 IdentityModels.cs 파일을 삭제할 수 있습니다. Web Forms 응용 프로그램에서 두 클래스를 삭제 하지만 IdentityModels.cs 파일에도 있는 도우미 클래스를 유지 해야 합니다.
3. 저장소 공급자가 별도의 프로젝트에 있는 경우 웹 응용 프로그램에 참조를 추가 합니다.
4. `using Microsoft.AspNet.Identity.EntityFramework;`에 대 한 모든 참조를 저장소 공급자의 네임 스페이스에 대 한 using 문으로 바꿉니다.
5. **Startup.Auth.cs** 클래스에서 적절 한 컨텍스트의 단일 인스턴스를 사용 하도록 **ConfigureAuth** 메서드를 변경 합니다. 

    [!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample9.cs?highlight=3)]
6. 앱\_시작 폴더에서 **IdentityConfig.cs**을 엽니다. ApplicationUserManager 클래스에서 사용자 지정 된 사용자 저장소를 사용 하는 사용자 관리자를 반환 하도록 **만들기** 메서드를 변경 합니다. 

    [!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample10.cs?highlight=3)]
7. **Applicationuser** 에 대 한 모든 참조를 **IdentityUser**로 바꿉니다.
8. 기본 프로젝트에는 IUser 인터페이스에서 정의 되지 않은 사용자 클래스의 일부 멤버가 포함 되어 있습니다. 전자 메일, PasswordHash, GenerateUserIdentityAsync 등이 있습니다. 사용자 클래스에 이러한 멤버가 없는 경우 해당 멤버를 구현 하거나 이러한 멤버를 사용 하는 코드를 변경 해야 합니다.
9. RoleManager의 인스턴스를 만든 경우 새 RoleStore 클래스를 사용 하도록 해당 코드를 변경 합니다.  

    [!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample11.cs)]
10. 기본 프로젝트는 키에 대 한 문자열 값을 포함 하는 사용자 클래스를 위해 설계 되었습니다. 사용자 클래스의 형식 (예: 정수)이 다른 경우 해당 형식으로 작업 하려면 프로젝트를 변경 해야 합니다. [ASP.NET Identity에서 사용자의 기본 키 변경](change-primary-key-for-users-in-aspnet-identity.md)을 참조 하세요.
11. 필요한 경우 Web.config 파일에 연결 문자열을 추가 합니다.

<a id="other"></a>
## <a name="other-resources"></a>기타 리소스

- 블로그: [ASP.NET Identity 구현](http://odetocode.com/blogs/scott/archive/2014/01/20/implementing-asp-net-identity.aspx)
- 자습서 및 GIT 코드: [Simple. Data Asp.Net Id 공급자](http://designcoderelease.blogspot.co.uk/2015/03/simpledata-aspnet-identity-provider.html)
- 자습서:[기본 id 계정 설정 및 외부 DB에서 가리키기](http://typecastexception.com/post/2013/10/27/Configuring-Db-Connection-and-Code-First-Migration-for-Identity-Accounts-in-ASPNET-MVC-5-and-Visual-Studio-2013.aspx) [@xivSolutions](https://twitter.com/xivSolutions)합니다.
- 자습서[: 사용자 지정 MySQL ASP.NET Identity 저장소 공급자 구현](implementing-a-custom-mysql-aspnet-identity-storage-provider.md)
- [SoftFluent](http://www.softfluent.com/) 별 [엔터티](http://blog.codefluententities.com/2014/04/30/asp-net-identity-v2-and-codefluent-entities/)
- James Randall, "의 [Azure Table Storage](https://www.nuget.org/packages/accidentalfish.aspnet.identity.azure/) 입니다.
- Azure Table Storage: [AspNet. Identity.](https://github.com/stuartleeks/leeksnet.AspNet.Identity.TableStorage) [@stuartleeks](https://twitter.com/stuartleeks).
- [Daniel Wertheim의](https://github.com/danielwertheim/mycouch.aspnet.identity)
- 탄력적 Searc[h:](https://github.com/bmbsqd/elastic-identity) Bombsquad AB에서 탄력적 id를 확인 합니다.
- [MongoDB](http://www.nuget.org/packages/MongoDB.AspNet.Identity/) Jonathan Sheely Jonathan Sheely.
- [Nhibernate](https://github.com/milesibastos/NHibernate.AspNet.Identity) Milesi Bastos by를 확인 합니다.
- [@tourismgeek](https://twitter.com/tourismgeek) [RavenDB](http://www.nuget.org/packages/AspNet.Identity.RavenDB/1.0.0) .
- [RavenDB.AspNet.Identity](https://github.com/ILMServices/RavenDB.AspNet.Identity) by [ILMServices](http://www.ilmservice.com/).
- Redis: [Redis.AspNet.Identity](https://github.com/aminjam/Redis.AspNet.Identity)
- "데이터베이스 우선" 사용자 저장소에 대 한 EF 코드를 생성 하는 T4 템플릿: [AspNet. id. EntityFramework](https://github.com/cbfrank/AspNet.Identity.EntityFramework)
