---
uid: identity/overview/migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity
title: 기존 웹 사이트를 SQL 멤버 자격에서 ASP.NET Identity-ASP.NET 4.x로 마이그레이션
author: Rick-Anderson
description: 이 자습서에서는 SQL 멤버 자격을 사용 하 여 만든 사용자 및 역할 데이터를 사용 하 여 기존 웹 응용 프로그램을 새 ASP.NET Identity s로 마이그레이션하는 단계를 보여 줍니다.
ms.author: riande
ms.date: 12/19/2014
ms.custom: seoapril2019
ms.assetid: 220d3d75-16b2-4240-beae-a5b534f06419
msc.legacyurl: /identity/overview/migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 633229cc4311d151121bf6a91b9fa8aeecca1197
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471635"
---
# <a name="migrating-an-existing-website-from-sql-membership-to-aspnet-identity"></a>기존 웹 사이트를 SQL 멤버 자격에서 ASP.NET Identity로 마이그레이션

[Rick Anderson](https://twitter.com/RickAndMSFT), [suhas Joshi](https://github.com/suhasj)

> 이 자습서에서는 새 ASP.NET Identity 시스템에 SQL 멤버 자격을 사용 하 여 만든 사용자 및 역할 데이터를 사용 하 여 기존 웹 응용 프로그램을 마이그레이션하는 단계를 보여 줍니다. 이 방법은 기존 데이터베이스 스키마를 ASP.NET Identity에 필요한 것으로 변경 하 고 이전/새 클래스에 연결 하는 것을 포함 합니다. 이 접근 방식을 채택 하 고 나면 데이터베이스를 마이그레이션한 후에 Id에 대 한 향후 업데이트를 손쉽게 처리할 수 있습니다.

이 자습서에서는 사용자 및 역할 데이터를 만들기 위해 Visual Studio 2010을 사용 하 여 만든 웹 응용 프로그램 템플릿 (Web Forms)을 사용 합니다. 그런 다음 SQL 스크립트를 사용 하 여 기존 데이터베이스를 Id 시스템에 필요한 테이블로 마이그레이션합니다. 다음으로 필요한 NuGet 패키지를 설치 하 고 멤버 관리를 위해 Id 시스템을 사용 하는 새 계정 관리 페이지를 추가 합니다. 마이그레이션을 테스트 하면 SQL 멤버 자격을 사용 하 여 만든 사용자가 로그인 할 수 있어야 하 고 새 사용자가 등록할 수 있어야 합니다. 전체 샘플은 [여기](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SQLMembership-Identity-OWIN/)에서 찾을 수 있습니다. 또한 [ASP.NET Membership에서 ASP.NET Identity로 마이그레이션을](http://travis.io/blog/2015/03/24/migrate-from-aspnet-membership-to-aspnet-identity.html)참조 하세요.

## <a name="getting-started"></a>시작

### <a name="creating-an-application-with-sql-membership"></a>SQL 멤버 자격으로 응용 프로그램 만들기

1. SQL 멤버 자격을 사용 하 고 사용자 및 역할 데이터를 포함 하는 기존 응용 프로그램으로 시작 해야 합니다. 이 문서의 목적을 위해 Visual Studio 2010에서 웹 응용 프로그램을 만들어 보겠습니다.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image1.jpg)
2. ASP.NET 구성 도구를 사용 하 여 두 명의 사용자 ( **Oldadminuser** 및 **olduser** )를 만듭니다.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image1.png)

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image2.jpg)
3. Admin 이라는 역할을 만들고 해당 역할에 사용자로 ' oldAdminUser '를 추가 합니다.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image2.png)
4. Default.aspx를 사용 하 여 사이트의 관리 섹션을 만듭니다. 관리자 역할의 사용자만 액세스할 수 있도록 web.config 파일에 권한 부여 태그를 설정 합니다. 자세한 내용은 여기를 참조 하세요 [https://www.asp.net/web-forms/tutorials/security/roles/role-based-authorization-cs](../../../web-forms/overview/older-versions-security/roles/role-based-authorization-cs.md)

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image3.png)
5. SQL 멤버 자격 시스템에서 만든 테이블을 이해 하려면 서버 탐색기에서 데이터베이스를 확인 합니다. 사용자 로그인 데이터는 aspnet\_사용자 및 aspnet\_멤버 자격 테이블에 저장 되는 반면 역할 데이터는 aspnet\_역할 테이블에 저장 됩니다. Aspnet\_UsersInRoles 테이블에 역할이 저장 되는 사용자에 대 한 정보입니다. 기본 멤버 관리를 위해 위의 표에 있는 정보를 ASP.NET Identity 시스템으로 이식 하는 것으로 충분 합니다.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image4.png)

### <a name="migrating-to-visual-studio-2013"></a>Visual Studio 2013로 마이그레이션

1. [최신 업데이트](https://www.microsoft.com/download/details.aspx?id=44921)와 함께 웹 또는 Visual Studio 2013에 대 한 Visual Studio Express 2013을 설치 합니다.
2. 설치 된 Visual Studio 버전에서 위의 프로젝트를 엽니다. 컴퓨터에 SQL Server Express 설치 되어 있지 않은 경우에는 연결 문자열에 SQL Express가 사용 되므로 프로젝트를 열 때 프롬프트가 표시 됩니다. SQL Express를 설치 하도록 선택 하거나 관련 작업을 수행 하 여 연결 문자열을 LocalDb로 변경할 수 있습니다. 이 문서에서는 LocalDb로 변경 합니다.
3. Web.config를 열고에서 연결 문자열을 변경 합니다. SQLExpress에서 (LocalDb) v 11.0입니다. 연결 문자열에서 ' User Instance = t r u e '를 제거 합니다.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image3.jpg)
4. 서버 탐색기를 열고 테이블 스키마 및 데이터를 관찰할 수 있는지 확인 합니다.
5. ASP.NET Identity 시스템은 버전 4.5 이상의 프레임 워크에서 작동 합니다. 응용 프로그램 대상을 4.5 이상으로 변경 합니다.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image5.png)

    프로젝트를 빌드하여 오류가 없는지 확인 합니다.

### <a name="installing-the-nuget-packages"></a>Nuget 패키지 설치

1. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 &gt; **NuGet 패키지 관리**를 클릭 합니다. 검색 상자에 "Asp.net Identity"를 입력 합니다. 결과 목록에서 패키지를 선택 하 고 설치를 클릭 합니다. "동의 함" 단추를 클릭 하 여 사용권 계약에 동의 합니다. 이 패키지는 종속성 패키지를 설치 합니다. EntityFramework 및 Microsoft ASP.NET Identity Core를 참조 하세요. 마찬가지로 다음 패키지를 설치 합니다 (OAuth 로그인을 사용 하도록 설정 하지 않으려면 마지막 4 OWIN 패키지를 건너뜀).

   - Microsoft.AspNet.Identity.Owin
   - Microsoft.Owin.Host.SystemWeb
   - Microsoft.Owin.Security.Facebook
   - Microsoft.Owin.Security.Google
   - Microsoft.Owin.Security.MicrosoftAccount
   - Microsoft.Owin.Security.Twitter

     ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image6.png)

### <a name="migrate-database-to-the-new-identity-system"></a>새 Id 시스템으로 데이터베이스 마이그레이션

다음 단계는 기존 데이터베이스를 ASP.NET Identity 시스템에 필요한 스키마로 마이그레이션하는 것입니다. 이를 위해 새 테이블을 만들고 기존 사용자 정보를 새 테이블로 마이그레이션하는 일련의 명령이 있는 SQL 스크립트를 실행 합니다. 스크립트 파일은 [여기](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/SQLMembership-Identity-OWIN/Migrations.sql)에서 찾을 수 있습니다.

이 스크립트 파일은이 샘플과 관련 된 것입니다. SQL 멤버 자격을 사용 하 여 만든 테이블에 대 한 스키마가 사용자 지정 되거나 수정 된 경우에는 스크립트를 적절 하 게 변경 해야 합니다.

### <a name="how-to-generate-the-sql-script-for-schema-migration"></a>스키마 마이그레이션을 위한 SQL 스크립트를 생성 하는 방법

ASP.NET Identity 클래스가 기존 사용자의 데이터와 함께 작동 하 게 하려면 데이터베이스 스키마를 ASP.NET Identity에 필요한 것으로 마이그레이션해야 합니다. 새 테이블을 추가 하 고 해당 테이블에 기존 정보를 복사 하 여이 작업을 수행할 수 있습니다. 기본적으로 ASP.NET Identity는 EntityFramework를 사용 하 여 Id 모델 클래스를 데이터베이스에 다시 매핑하여 정보를 저장/검색 합니다. 이러한 모델 클래스는 사용자 및 역할 개체를 정의 하는 핵심 Id 인터페이스를 구현 합니다. 데이터베이스의 테이블과 열은 이러한 모델 클래스를 기반으로 합니다. Id v 2.1.0의 EntityFramework 모델 클래스와 해당 속성은 아래에 정의 되어 있습니다.

| **IdentityUser** | **형식** | **IdentityRole** | **IdentityUserRole** | **IdentityUserLogin** | **IdentityUserClaim** |
| --- | --- | --- | --- | --- | --- |
| Id | 문자열 | Id | RoleId | ProviderKey | Id |
| 사용자 이름 | 문자열 | 속성 | UserId | UserId | ClaimType |
| PasswordHash | 문자열 |  |  | LoginProvider | ClaimValue |
| SecurityStamp | 문자열 |  |  |  | 사용자\_Id |
| Email | 문자열 |  |  |  |  |
| EmailConfirmed | bool |  |  |  |  |
| PhoneNumber | 문자열 |  |  |  |  |
| PhoneNumberConfirmed | bool |  |  |  |  |
| LockoutEnabled | bool |  |  |  |  |
| LockoutEndDate | DateTime |  |  |  |  |
| AccessFailedCount | int |  |  |  |  |

이러한 각 모델에 대 한 테이블은 속성에 해당 하는 열이 있어야 합니다. 클래스와 테이블 간의 매핑은 `IdentityDBContext`의 `OnModelCreating` 메서드에서 정의 됩니다. 이를 구성의 흐름 API 방법 이라고 하며, 자세한 내용은 [여기](https://msdn.microsoft.com/data/jj591617.aspx)를 참조 하세요. 클래스에 대 한 구성은 아래에서 설명 하는 것과 같습니다.

| **클래스** | **테이블** | **기본 키** | **외래 키** |
| --- | --- | --- | --- |
| IdentityUser | AspnetUsers | Id |  |
| IdentityRole | AspnetRoles | Id |  |
| IdentityUserRole | AspnetUserRole | UserId + RoleId | 사용자\_Id-&gt;AspnetUsers RoleId-&gt;AspnetRoles |
| IdentityUserLogin | AspnetUserLogins | ProviderKey + UserId + LoginProvider | UserId-&gt;AspnetUsers |
| IdentityUserClaim | AspnetUserClaims | Id | 사용자\_Id-&gt;AspnetUsers |

이 정보를 사용 하 여 새 테이블을 만드는 SQL 문을 만들 수 있습니다. 각 문을 개별적으로 작성 하거나 필요에 따라 편집할 수 있는 EntityFramework PowerShell 명령을 사용 하 여 전체 스크립트를 생성할 수 있습니다. 이렇게 하려면 VS의 **보기** 또는 **도구** 메뉴에서 **패키지 관리자 콘솔** 을 엽니다.

- "마이그레이션 사용" 명령을 실행 하 여 EntityFramework 마이그레이션을 사용 하도록 설정 합니다.
- /Vb. C#데이터베이스를 만드는 초기 설정 코드를 만드는 "추가 마이그레이션 초기" 명령을 실행 합니다.
- 마지막 단계는 모델 클래스를 기반으로 SQL 스크립트를 생성 하는 "업데이트-데이터베이스 – 스크립트" 명령을 실행 하는 것입니다.

[!INCLUDE[](../../../includes/identity/alter-command-exception.md)]

이 데이터베이스 생성 스크립트를 시작으로 사용 하 여 새 열을 추가 하 고 데이터를 복사할 수 있습니다. 이를 사용 하면 이후 버전의 Id 릴리스에서 모델 클래스가 변경 될 때 EntityFramework가 데이터베이스 스키마를 수정 하는 데 사용 하는 `_MigrationHistory` 테이블을 생성 한다는 이점이 있습니다.

SQL 멤버 자격 사용자 정보에는 Id 사용자 모델 클래스 (전자 메일, 암호 시도, 마지막 로그인 날짜, 마지막 잠금 날짜 등)와 다른 속성이 추가 되었습니다. 이 정보는 유용한 정보 이며 Id 시스템으로 전달 됩니다. 이 작업을 수행 하려면 사용자 모델에 속성을 추가 하 고 데이터베이스의 테이블 열에 속성을 다시 매핑합니다. `IdentityUser` 모델을 서브 클래스 하는 클래스를 추가 하 여이 작업을 수행할 수 있습니다. 이 사용자 지정 클래스에 속성을 추가 하 고 SQL 스크립트를 편집 하 여 테이블을 만들 때 해당 열을 추가할 수 있습니다. 이 클래스의 코드는 문서에 자세히 설명 되어 있습니다. 새 속성을 추가한 후 `AspnetUsers` 테이블을 만들기 위한 SQL 스크립트는 다음과 같습니다.

[!code-sql[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample1.sql)]

다음으로 SQL 멤버 자격 데이터베이스에서 Id에 대 한 새로 추가 된 테이블로 기존 정보를 복사 해야 합니다. 이 작업은 한 테이블에서 다른 테이블로 데이터를 직접 복사 하 여 SQL을 통해 수행할 수 있습니다. 테이블 행에 데이터를 추가 하려면 `INSERT INTO [Table]` 구문을 사용 합니다. 다른 테이블에서 복사 하려면 `INSERT INTO` 문을 `SELECT` 문과 함께 사용할 수 있습니다. 사용자 정보를 모두 얻으려면 *aspnet\_사용자* 및 *Aspnet\_멤버 자격* 테이블을 쿼리하고 데이터를 *AspNetUsers* 테이블에 복사 해야 합니다. `JOIN` 및 `LEFT OUTER JOIN` 문과 함께 `INSERT INTO` 및 `SELECT`를 사용 합니다. 테이블 간에 데이터를 쿼리하고 복사 하는 방법에 대 한 자세한 내용은 [이](https://technet.microsoft.com/library/ms190750%28v=sql.105%29.aspx) 링크를 참조 하세요. 또한 AspnetUserLogins 및 AspnetUserClaims 테이블은 기본적으로이에 매핑되는 SQL 멤버 자격에 대 한 정보가 없으므로 시작 하기에는 비어 있습니다. 사용자 및 역할에 대 한 정보만 복사 됩니다. 이전 단계에서 만든 프로젝트의 경우 사용자 테이블에 정보를 복사 하는 SQL 쿼리는 다음과 같습니다.

[!code-sql[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample2.sql)]

위의 SQL 문에서 *aspnet\_사용자* 및 *Aspnet\_멤버 자격* 테이블의 각 사용자에 대 한 정보를 *AspnetUsers* 테이블의 열에 복사 합니다. 여기에서 수행 하는 유일한 수정 사항은 암호를 복사 하는 것입니다. SQL 멤버 자격의 암호에 대 한 암호화 알고리즘에서 ' PasswordSalt ' 및 ' Passwordsalt '을 사용 하므로 Id로 암호를 해독 하는 데 사용할 수 있도록 해시 된 암호와 함께이를 복사 합니다. 이에 대해서는 사용자 지정 암호 hasher를 연결 하는 경우 문서에 자세히 설명 되어 있습니다.

이 스크립트 파일은이 샘플과 관련 된 것입니다. 추가 테이블이 있는 응용 프로그램의 경우 개발자는 비슷한 방법을 따라 사용자 모델 클래스의 속성을 추가 하 고 AspnetUsers 테이블의 열에 매핑할 수 있습니다. 스크립트를 실행 하려면

1. 서버 탐색기를 엽니다. ' ApplicationServices ' 연결을 확장 하 여 테이블을 표시 합니다. 테이블 노드를 마우스 오른쪽 단추로 클릭 하 고 ' 새 쿼리 ' 옵션을 선택 합니다.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image7.png)
2. 쿼리 창에서 전체 SQL 스크립트를 복사 하 여 migration .sql 파일에 붙여넣습니다. ' 실행 ' 화살표 단추를 눌러 스크립트 파일을 실행 합니다.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image4.jpg)

    서버 탐색기 창을 새로 고칩니다. 데이터베이스에 5 개의 새 테이블이 생성 됩니다.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image8.png)

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image9.png)

    다음은 SQL 멤버 자격 테이블의 정보가 새 Id 시스템에 매핑되는 방법입니다.

    aspnet\_역할-&gt; AspNetRoles

    asp.net\_netUsers 및 asp\_Netusers--&gt; AspNetUsers

    aspnet\_UserInRoles--&gt; AspNetUserRoles

    위의 섹션에서 설명한 대로 AspNetUserClaims 및 AspNetUserLogins 테이블은 비어 있습니다. AspNetUser 테이블의 ' 판별자 ' 필드는 다음 단계로 정의 된 모델 클래스 이름과 일치 해야 합니다. 또한 PasswordHash 열은 ' 암호화 된 암호 | 암호 솔트 | 암호 형식 ' 형식입니다. 이렇게 하면 이전 암호를 다시 사용할 수 있도록 특별 한 SQL 멤버 자격 암호화 논리를 사용할 수 있습니다. 이에 대해서는이 문서의 뒷부분에서 설명 합니다.

### <a name="creating-models-and-membership-pages"></a>모델 및 멤버 자격 페이지 만들기

앞에서 설명한 대로 Id 기능은 Entity Framework를 사용 하 여 기본적으로 계정 정보를 저장 하기 위해 데이터베이스와 통신 합니다. 테이블의 기존 데이터로 작업 하려면 테이블에 다시 매핑하고 Id 시스템에 후크 하는 모델 클래스를 만들어야 합니다. Id 계약의 일부로 모델 클래스는 Id. Core dll에 정의 된 인터페이스를 구현 하거나, Microsoft. AspNet. i d. EntityFramework에서 사용할 수 있는 이러한 인터페이스의 기존 구현을 확장할 수 있습니다.

이 샘플에서 AspNetRoles, AspNetUserClaims, AspNetLogins 및 AspNetUserRole 테이블은 기존 Id 시스템 구현과 유사한 열을 포함 합니다. 따라서 기존 클래스를 다시 사용 하 여 이러한 테이블에 매핑할 수 있습니다. AspNetUser 테이블에는 SQL 멤버 자격 테이블의 추가 정보를 저장 하는 데 사용 되는 몇 가지 추가 열이 있습니다. ' IdentityUser '의 기존 구현을 확장 하 고 추가 속성을 추가 하는 모델 클래스를 만들어이를 매핑할 수 있습니다.

1. 프로젝트에서 모델 폴더를 만들고 클래스 사용자를 추가 합니다. 클래스의 이름은 ' AspnetUsers ' 테이블의 ' 판별자 ' 열에 추가 된 데이터와 일치 해야 합니다.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image10.png)

    사용자 클래스는 IdentityUser *프레임 워크* dll에 있는 클래스를 확장 해야 합니다. AspNetUser 열에 다시 매핑되는 클래스의 속성을 선언 합니다. 속성 ID, 사용자 이름, PasswordHash 및 SecurityStamp는 IdentityUser에 정의 되므로 생략 됩니다. 다음은 모든 속성을 포함 하는 사용자 클래스에 대 한 코드입니다.

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample3.cs)]
2. 모델의 데이터를 테이블에 다시 저장 하 고 테이블에서 데이터를 검색 하 여 모델을 채우도록 Entity Framework DbContext 클래스가 필요 합니다. IdentityDbContext는 Id 테이블과 상호 작용 하 여 정보를 검색 하 고 저장 하는 클래스를 정의 *합니다.* IdentityDbContext&lt;tuser&gt;은 IdentityUser 클래스를 확장 하는 클래스 일 수 있는 ' TUser ' 클래스를 사용 합니다.

    ' 모델 ' 폴더에서 IdentityDbContext를 확장 하 고 1 단계에서 만든 ' User ' 클래스를 전달 하는 새 클래스 ApplicationDBContext를 만듭니다.

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample4.cs)]
3. 새 Id 시스템의 사용자 관리&gt;&lt;는 *Microsoft. n.* n e t. n e t. n e t. n e t. n e t. n e t. n e t. n e t. 1 단계에서 만든 ' User ' 클래스를 전달 하 여 UserManager를 확장 하는 사용자 지정 클래스를 만들어야 합니다.

    모델 폴더에서 UserManager&lt;사용자를 확장 하는 새 클래스 UserManager를 만듭니다&gt;

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample5.cs)]
4. 응용 프로그램 사용자의 암호는 암호화 되어 데이터베이스에 저장 됩니다. SQL 멤버 자격에 사용 되는 암호화 알고리즘은 새 Id 시스템의 암호화 알고리즘과 다릅니다. 이전 암호를 다시 사용 하려면 이전 사용자가 SQL 멤버 자격 알고리즘을 사용 하 여 로그인 할 때 암호를 선택적으로 해독 해야 하며, 새 사용자의 경우 Id로 암호화 알고리즘을 사용 합니다.

    UserManager 클래스에는 ' IPasswordHasher ' 인터페이스를 구현 하는 클래스의 인스턴스를 저장 하는 ' PasswordHasher ' 속성이 있습니다. 사용자 인증 트랜잭션 중에 암호를 암호화/암호 해독 하는 데 사용 됩니다. 3 단계에서 정의한 UserManager 클래스에서 새 클래스 SQLPasswordHasher를 만들고 아래 코드를 복사 합니다.

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample6.cs)]

    System.string 및 system.servicemodel 네임 스페이스를 가져와서 컴파일 오류를 해결 합니다.

    EncodePassword 메서드는 기본 SQL 멤버 자격 암호화 구현에 따라 암호를 암호화 합니다. 이는 System.web dll에서 가져옵니다. 이전 앱에서 사용자 지정 구현을 사용한 경우 여기에 반영 해야 합니다. *EncodePassword* 메서드를 사용 하 여 지정 된 암호를 해시 하거나 데이터베이스에 있는 기존 암호를 사용 하 여 일반 텍스트 암호를 확인 하는 두 가지 다른 메서드인 *Hashpassword* 및 *verifyhashedpassword* 를 정의 해야 합니다.

    SQL 멤버 자격 시스템은 PasswordHash, PasswordSalt 및 Passwordsalt을 사용 하 여 암호를 등록 하거나 변경할 때 사용자가 입력 한 암호를 해시 합니다. 마이그레이션하는 동안 세 필드는 모두 ' | ' 문자로 구분 된 AspNetUser 테이블의 PasswordHash 열에 저장 됩니다. 사용자가 로그인 하 고 암호에 이러한 필드가 있는 경우 SQL 멤버 자격 암호화를 사용 하 여 암호를 확인 합니다. 그렇지 않으면 Id 시스템의 기본 암호화를 사용 하 여 암호를 확인 합니다. 이렇게 하면 앱이 마이그레이션되면 이전 사용자가 암호를 변경할 필요가 없습니다.
5. UserManager 클래스의 생성자를 선언 하 고 생성자의 속성에 SQLPasswordHasher로 전달 합니다.

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample7.cs)]

### <a name="create-new-account-management-pages"></a>새 계정 관리 페이지 만들기

마이그레이션의 다음 단계는 사용자가 등록 하 고 로그인 할 수 있는 계정 관리 페이지를 추가 하는 것입니다. SQL 멤버 자격의 이전 계정 페이지는 새 Id 시스템에서 작동 하지 않는 컨트롤을 사용 합니다. 새 사용자 관리 페이지를 추가 하려면 프로젝트를 이미 만들었고 NuGet 패키지를 추가 했으므로 ' 응용 프로그램에 사용자를 등록 하기 위한 Web Forms 추가 ' 단계에서 시작 하 [https://www.asp.net/identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project](../getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project.md) 이 링크의 자습서를 따르세요.

여기에 있는 프로젝트를 사용 하려면 샘플에 대 한 몇 가지 변경 작업을 수행 해야 합니다.

- Register.aspx.cs 및 Login.aspx.cs 코드 뒤 클래스는 Id 패키지의 `UserManager`를 사용 하 여 사용자를 만듭니다. 이 예에서는 앞에서 설명한 단계를 수행 하 여 모델 폴더에 추가 된 UserManager를 사용 합니다.
- Register.aspx.cs 및 Login.aspx.cs 코드 뒤 클래스에서 IdentityUser 대신 만들어진 사용자 클래스를 사용 합니다. 사용자 지정 사용자 클래스에서 Id 시스템으로 후크 합니다.
- 데이터베이스를 만드는 부분은 건너뛸 수 있습니다.
- 개발자는 새 사용자의 ApplicationId를 현재 응용 프로그램 ID와 일치 하도록 설정 해야 합니다. 이 작업을 수행 하려면 Register.aspx.cs 클래스에서 사용자 개체가 만들어지기 전에이 응용 프로그램에 대 한 ApplicationId를 쿼리하고 사용자를 만들기 전에 설정 합니다.

    예제:

    Register.aspx.cs 페이지에서 메서드를 정의 하 여 aspnet\_응용 프로그램 테이블을 쿼리하고 응용 프로그램 이름에 따라 응용 프로그램 Id를 가져옵니다.

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample8.cs)]

    이제 사용자 개체에 대해 설정 합니다.

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample9.cs)]

이전 사용자 이름 및 암호를 사용 하 여 기존 사용자에 게 로그인 합니다. 등록 페이지를 사용 하 여 새 사용자를 만들 수 있습니다. 또한 사용자가 예상 대로 역할에 있는지 확인 합니다.

Id 시스템으로 이식 하면 사용자가 응용 프로그램에 대 한 OAuth (Open Authentication)를 추가할 수 있습니다. OAuth가 설정 [된 예제를](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SQLMembership-Identity-OWIN/) 참조 하세요.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 사용자를 SQL 멤버 자격에서 ASP.NET Identity로 이식 하는 방법을 살펴보았습니다. 하지만 프로필 데이터를 이식 하지 않았습니다. 다음 자습서에서는 SQL 멤버 자격에서 새 Id 시스템으로 프로필 데이터 포팅에 대해 살펴봅니다.

이 문서의 맨 아래에 의견을 남길 수 있습니다.

*문서를 검토 하기 위한 Tom Dykstra 및 Rick Anderson에 감사 합니다.*
