---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-cs
title: 프로덕션 웹 사이트의 사용자 및 역할 (C#) | Microsoft Docs
author: rick-anderson
description: ASP.NET 웹 사이트 관리 도구 (WSAT)는 멤버 자격 및 역할 설정을 구성 하 고 만들기, 편집, ...을 위한 웹 기반 사용자 인터페이스를 제공 합니다.
ms.author: riande
ms.date: 06/09/2009
ms.assetid: dbc54313-5d05-4285-98b3-726edea6d0c9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-cs
msc.type: authoredcontent
ms.openlocfilehash: c47bd2c1661f129dd8856916de04b8ba459fbfec
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74616543"
---
# <a name="users-and-roles-on-the-production-website-c"></a>프로덕션 웹 사이트의 사용자 및 역할 (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[PDF 다운로드](https://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial16_CustomAWAT_cs.pdf)

> ASP.NET 웹 사이트 관리 도구 (WSAT)는 멤버 자격 및 역할 설정을 구성 하 고 사용자 및 역할을 생성, 편집 및 삭제 하기 위한 웹 기반 사용자 인터페이스를 제공 합니다. 불행 하 게 WSAT는 localhost에서 방문 하는 경우에만 작동 합니다. 즉, 브라우저를 통해 프로덕션 웹 사이트의 관리 도구에 연결할 수 없습니다. 좋은 소식은 프로덕션 환경에서 사용자 및 역할을 관리할 수 있도록 하는 해결 방법이 있다는 것입니다. 이 자습서에서는 이러한 대안과 기타 문제를 살펴봅니다.

## <a name="introduction"></a>소개

ASP.NET 2.0에는 웹 응용 프로그램에 추가할 수 있는 블록 서비스를 구성 하는 여러 *응용 프로그램 서비스가*도입 되었습니다. 멤버 자격 및 역할 서비스를 책 리뷰 웹 사이트에 추가 하 [ *는 애플리케이션 서비스 자습서를 사용 하는 웹 사이트 구성* ](configuring-a-website-that-uses-application-services-cs.md)에 다시 추가 했습니다. 멤버 자격 서비스는 사용자 계정 만들기 및 관리를 용이 하 게 합니다. 역할 서비스는 사용자를 그룹으로 분류 하기 위한 API를 제공 합니다. 서적 검토 사이트에는 세 개의 사용자 계정, 즉 Scott, Jisun, Alice 및 단일 역할인 관리자 (관리자 역할)가 있습니다.

ASP. NET의 응용 프로그램 서비스는 특정 구현에 연결 되지 않습니다. 대신 특정 *공급자*를 사용 하도록 응용 프로그램 서비스에 지시 하 고 해당 공급자는 특정 기술을 사용 하 여 서비스를 구현 합니다. 멤버 자격 및 역할 서비스에 대 한 `SqlMembershipProvider` 및 `SqlRoleProvider` 공급자를 사용 하도록 책 리뷰 웹 응용 프로그램을 구성 했습니다. 이러한 두 공급자는 SQL Server 데이터베이스에 사용자 계정 및 역할 정보를 저장 하 고 웹 호스팅 회사에서 호스트 되는 인터넷 기반 웹 응용 프로그램에 가장 일반적으로 사용 되는 공급자입니다.

멤버 자격 및 역할 서비스를 사용 하는 개발자의 일반적인 문제는 프로덕션 환경에서 사용자 및 역할을 관리 하는 것입니다. 프로덕션 웹 사이트에서 사용자 계정을 삭제 하거나, 새 역할을 추가 하거나 기존 역할에 기존 사용자를 추가 하려면 어떻게 하나요? 이 자습서에서는 프로덕션 웹 사이트에서 사용자 및 역할을 관리 하는 다양 한 기술을 살펴봅니다.

## <a name="using-the-aspnet-web-site-administration-tool"></a>ASP.NET 웹 사이트 관리 도구 사용

ASP.NET에는 사용자 계정 및 역할을 쉽게 만들고 관리 하 고 사용자 및 역할 기반 권한 부여 규칙을 지정 하는 데 사용 되는 WSAT ( [웹 사이트 관리 도구](https://msdn.microsoft.com/library/yy40ytx0.aspx) )가 포함 되어 있습니다. WSAT를 사용 하려면 솔루션 탐색기에서 ASP.NET 구성 아이콘을 클릭 하거나 웹 사이트 또는 프로젝트 메뉴로 이동 하 여 ASP.NET 구성 옵션을 선택 합니다. 두 가지 방법 중 하나는 웹 브라우저를 시작 하 고 다음과 같은 주소에서 WSAT을 가리킵니다. `http://localhost:portNumber/asp.netwebadminfiles/default.aspx?applicationPhysicalPath=pathToApplication`

WSAT는 다음과 같은 세 가지 섹션으로 구분 됩니다.

- **보안** -사용자, 역할 및 권한 부여 규칙을 관리 합니다.
- **Applicationconfiguration** -여기에서 &lt;appSettings&gt; 및 SMTP 설정을 관리 합니다. 응용 프로그램을 오프 라인으로 전환 하 고 여기에서 디버깅 및 추적 설정을 관리할 수 있을 뿐만 아니라 기본 사용자 지정 오류 페이지를 지정할 수도 있습니다.
- **Providerconfiguration** -응용 프로그램 서비스에 사용 되는 공급자를 구성 합니다.

보안 섹션 ( **그림 1**에 표시)에는 새 사용자를 만들고, 사용자를 관리 하 고, 역할을 만들고 관리 하 고, 액세스 규칙을 만들고 관리 하기 위한 링크가 포함 되어 있습니다. 여기에서 시스템에 새 역할을 추가 하거나, 기존 사용자를 삭제 하거나, 특정 사용자 계정에서 역할을 추가 또는 제거할 수 있습니다.

[![](users-and-roles-on-the-production-website-cs/_static/image2.png)](users-and-roles-on-the-production-website-cs/_static/image1.png)

**그림 1**: WSAT 보안 섹션에는 사용자 및 역할을 관리 하는 옵션이 포함 되어 있습니다.  
([전체 크기 이미지를 보려면 클릭](users-and-roles-on-the-production-website-cs/_static/image3.png))

아쉽게도 WSAT는 로컬 에서만 액세스할 수 있습니다. 원격 프로덕션 웹 사이트의 WSAT를 방문할 수 없습니다. `www.yoursite.com/asp.netwebadminfiles/default.aspx`를 방문 하는 경우 404 응답 없음 응답을 받게 됩니다. WSAT을 구동 하는 코드는 .NET Framework에서 `Membership` 및 `Roles` 클래스를 사용 하 여 사용자 및 역할을 만들고 편집 하 고 삭제 합니다. 이러한 클래스는 웹 응용 프로그램의 구성 정보를 참조 하 여 사용할 공급자를 결정 합니다. [ *애플리케이션 서비스 사용 하는 웹 사이트 구성* 자습서](configuring-a-website-that-uses-application-services-cs.md) 로 돌아가서 `SqlMembershipProvider` 및 `SqlRoleProvider` 공급자를 사용 하도록 책 리뷰 웹 사이트를 설치 합니다. 이 수반 `<membership>` 및 `<roleManager>` 섹션을 `Web.config`에 추가 합니다.

[!code-xml[Main](users-and-roles-on-the-production-website-cs/samples/sample1.xml)]

`<membership>` 및 `<roleManager>` 섹션은 각각 `type` 특성의 `SqlMembershipProvider` 및 `SqlRoleProvider` 공급자를 참조 합니다. 이러한 공급자는 지정 된 SQL Server 데이터베이스에 사용자 및 역할 정보를 저장 합니다. 이러한 공급자가 사용 하는 데이터베이스는 `~/ConfigSections/databaseConnectionStrings.config` 파일에 정의 된 `ReviewsConnectionString``connectionStringName` 특성으로 지정 됩니다. 개발 환경의 `databaseConnectionStrings.config` 파일은 개발 데이터베이스에 대 한 연결 문자열을 포함 하는 반면 프로덕션 상의 `databaseConnectionStrings.config` 파일에는 프로덕션 데이터베이스에 대 한 연결 문자열이 포함 되어 있습니다.

간단히 말해서 WSAT는 개발 환경을 통해 로컬로 액세스 해야 하며 `databaseConnectionStrings.config` 파일에 지정 된 데이터베이스의 사용자 및 역할 정보를 사용 하 여 작동 합니다. 따라서 개발 환경에서 `databaseConnectionStrings.config` 파일의 연결 문자열 정보를 변경 하는 경우 프로덕션 환경에서 WSAT를 로컬로 사용 하 여 사용자 및 역할을 관리할 수 있습니다.

이 기능을 설명 하려면 개발 환경에서 Visual Studio의 `databaseConnectionStrings.config` 파일을 열고 개발 데이터베이스 연결 문자열을 프로덕션 데이터베이스 연결 문자열로 바꿉니다. 그런 다음 WSAT를 시작 하 고 보안 탭으로 이동 하 여 Sam 이라는 새 사용자를 암호 "password!"로 추가 합니다. (따옴표 less). **그림 2** 에서는이 계정을 만들 때 WSAT 화면을 보여 줍니다.

[![](users-and-roles-on-the-production-website-cs/_static/image5.png)](users-and-roles-on-the-production-website-cs/_static/image4.png)

**그림 2**: 프로덕션 환경에서 Sam 이라는 새 사용자 만들기  
([전체 크기 이미지를 보려면 클릭](users-and-roles-on-the-production-website-cs/_static/image6.png))

`databaseConnectionStrings.config`에서 프로덕션 데이터베이스 서버를 가리키도록 연결 문자열을 변경 했으므로 Sam이 프로덕션 환경에서 사용자로 추가 되었습니다. 이를 확인 하려면 `databaseConnectionStrings.config` 파일의 연결 문자열을 다시 개발 데이터베이스로 변경한 다음 개발 환경에서 `Login.aspx` 페이지를 방문 합니다. Sam으로 로그인을 시도 합니다 ( **그림 3**참조).

[![](users-and-roles-on-the-production-website-cs/_static/image8.png)](users-and-roles-on-the-production-website-cs/_static/image7.png)

**그림 3**: 개발 환경에서 Sam으로 로그인 할 수 없음  
([전체 크기 이미지를 보려면 클릭](users-and-roles-on-the-production-website-cs/_static/image9.png))

사용자 계정 정보가 로컬 데이터베이스에 없으므로 개발 환경에서 Sam으로 로그인 할 수 없습니다. 대신가 프로덕션 데이터베이스에 추가 되었습니다. 이를 확인 하려면 개발 및 프로덕션 데이터베이스에서 `aspnet_Users` 테이블의 내용을 확인 합니다. 개발 환경에서는 사용자에 게 Scott, Jisun 및 Alice에 대 한 3 개의 레코드만 있어야 합니다. 그러나 프로덕션 데이터베이스의 `aspnet_Users` 테이블에는 Scott, Jisun, Alice 및 Sam 이라는 4 개의 레코드가 있습니다. 따라서 Sam은 프로덕션에서 웹 사이트를 통해 로그인 할 수 있지만 개발 환경을 통해서는 로그인 할 수 없습니다.

[![](users-and-roles-on-the-production-website-cs/_static/image11.png)](users-and-roles-on-the-production-website-cs/_static/image10.png)

**그림 4**: Sam이 프로덕션 웹 사이트에 로그인 할 수 있음  
([전체 크기 이미지를 보려면 클릭](users-and-roles-on-the-production-website-cs/_static/image12.png))

> [!NOTE]
> WSAT 사용이 완료 되 면 `databaseConnectionStrings.config` 파일의 연결 문자열을 개발 데이터베이스의 연결 문자열로 다시 변경 해야 합니다. 그렇지 않으면 개발 환경을 통해 사이트를 테스트할 때 프로덕션 데이터로 작업 합니다. 방금 설명한 기술을 사용 하면 WSAT를 사용 하 여 사용자 및 역할을 원격으로 관리 하 고, 다른 WSAT 구성 옵션 (액세스 규칙, SMTP 설정, 디버깅 및 추적 설정 등)을 변경 하 여 `Web.config` 파일을 수정할 수도 있습니다. 따라서 설정에 대 한 변경 내용은 프로덕션 환경이 아닌 개발 환경에 적용 됩니다.

## <a name="creating-custom-user-and-role-management-web-pages"></a>사용자 지정 사용자 및 역할 관리 웹 페이지 만들기

WSAT는 사용자 및 역할을 관리 하는 데 사용할 수 있는 기본 시스템을 제공 하지만 로컬로 시작 하 고 프로덕션에서 사용자 및 역할을 관리 하기 위해 연결 문자열 정보를 변경 해야 합니다. 사용자 계정을 지 원하는 대부분의 웹 사이트에는 관리자가 사이트 내의 페이지에서 사용자와 역할을 관리할 수 있는 많은 사용자 및 역할 관리 웹 페이지가 포함 되어 있습니다. 이러한 웹 기반 관리 페이지를 사용 하면 사용자 및 역할을 훨씬 쉽게 관리할 수 있으며, 또는 Visual Studio를 사용 하 여 WSAT를 시작 하는 기술 배경에 대 한 액세스 권한이 없는 많은 관리자 또는 관리자가 있을 수 있습니다.

ASP.NET에는 다양 한 관리 웹 페이지를 끌어서 놓기를 쉽게 구현할 수 있도록 하는 다양 한 기본 제공 로그인 관련 웹 컨트롤이 포함 되어 있습니다. 예를 들어 CreateUserWizard 컨트롤을 페이지로 끌어와 몇 가지 속성을 설정 하 여 관리자가 새 사용자 계정을 만들 수 있는 페이지를 만들 수 있습니다. 실제로 **그림 2** 에 표시 된 WSAT 사용자를 만드는 페이지는 페이지에 추가할 수 있는 것과 동일한 CreateUserWizard 컨트롤을 사용 합니다. 또한 멤버 자격 및 역할 서비스 기능은 .NET Framework의 `Membership` 및 `Roles` 클래스를 통해 프로그래밍 방식으로 사용할 수 있습니다. 이러한 클래스를 사용 하 여 사용자 및 역할을 만들고, 편집 하 고, 삭제 하는 코드를 작성할 수 있을 뿐만 아니라 사용자를 역할에 추가 또는 제거 하 고 역할에 있는 사용자를 확인 하 고 다른 사용자 및 역할 관련 작업을 수행할 수 있습니다.

[ *애플리케이션 서비스를 사용 하는 웹 사이트 구성* 자습서](configuring-a-website-that-uses-application-services-cs.md) 에서는 `CreateAccount.aspx`이라는 `Admin` 폴더에 페이지를 추가 했습니다. 관리자는이 페이지에서 사이트에 새 사용자 계정을 추가 하 고 새로 만든 사용자가 관리자 역할에 있는지 여부를 지정할 수 있습니다 ( **그림 5**참조).

[![](users-and-roles-on-the-production-website-cs/_static/image14.png)](users-and-roles-on-the-production-website-cs/_static/image13.png)

**그림 5**: 관리자가 새 사용자 계정을 만들 수 있습니다.  
([전체 크기 이미지를 보려면 클릭](users-and-roles-on-the-production-website-cs/_static/image15.png))

`Membership` 및 `Roles` 클래스 및 로그인 관련 ASP.NET 웹 컨트롤 사용에 대 한 단계별 지침과 함께 사용자 및 역할 관리 페이지를 빌드하는 방법에 대 한 자세한 내용은 [웹 사이트 보안 자습서](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)를 참조 하세요. 웹 페이지를 작성 하는 방법에 대 한 지침을 통해 새 계정을 만들고, 역할을 만들고 관리 하 고, 역할에 사용자를 할당 하 고, 기타 일반적인 관리 작업을 할 수 있습니다.

프로덕션 웹 사이트에서 WSAT 같은 기능을 구현 하기 위해 항상 WSAT의 기능을 구현 하는 고유한 웹 페이지 시리즈를 빌드할 수 있습니다. 시작 하려면 `%WINDIR%\Microsoft.NET\Framework\v2.0.50727\ASP.NETWebAdminFiles`폴더에 있는 WSAT 소스 코드를 확인 합니다. 또 다른 옵션은 Dan Clem의 WSAT 대체를 사용 하는 것입니다 .이 대체 항목은 [자신의 웹 사이트 관리 도구를 롤링](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)하는 문서에서 공유 합니다. Dan은 사용자 지정 WSAT와 유사한 도구를 빌드하는 과정을 안내 하 고, 응용 프로그램의 소스 코드를 다운로드 ( C#) 하 고, 호스트 된 웹 사이트에 사용자 지정 WSAT를 추가 하기 위한 단계별 지침을 제공 합니다.

## <a name="summary"></a>요약

ASP.NET 웹 사이트 관리 도구 (WSAT)는 멤버 자격 및 역할 응용 프로그램 서비스와 함께 사용 하 여 웹 사이트에 대 한 사용자 및 역할 정보를 관리할 수 있습니다. 아쉽게도 WSAT는 로컬 에서만 액세스할 수 있으며 프로덕션 웹 사이트에서 방문할 수 없습니다. 그러나 개발 환경에서 프로덕션 데이터베이스를 가리키도록 연결 문자열을 변경 하 여 프로덕션 웹 사이트의 사용자 및 역할을 관리 하는 데 WSAT를 사용할 수 있습니다.

WSAT 접근 방식은 사용자 및 역할을 관리 하는 빠르고 쉬운 방법을 사용 하지만, Visual Studio에서 WSAT를 시작 하 고 연결 문자열 정보에 대 한 임시 변경도 시작 합니다. WSAT는 프로덕션 환경에서 사용자 및 역할을 관리 하는 빠른 방법을 제공 하지만, 여러 관리자가 있는 웹 사이트 또는 Visual Studio 및 WSAT에 익숙하지 않은 관리자의 경우에는 잘 작동 하지 않습니다. 이러한 이유로 사용자 계정을 지 원하는 대부분의 웹 사이트에는 관리 웹 페이지 집합이 포함 됩니다. 이러한 웹 페이지 집합은 WSAT에 대 한 필요성을 제거 하 고 모든 컴퓨터의 다양 한 관리자가 사용할 수 있도록 합니다.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 정보

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP를 검사 합니다. 네트워크의 멤버 자격, 역할 및 프로필](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [사용자 고유의 웹 사이트 관리 도구 롤링](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [웹 사이트 관리 도구 개요](https://msdn.microsoft.com/library/yy40ytx0.aspx)
- [웹 사이트 보안 자습서](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)

> [!div class="step-by-step"]
> [이전](precompiling-your-website-cs.md)
> [다음](asp-net-hosting-options-vb.md)
