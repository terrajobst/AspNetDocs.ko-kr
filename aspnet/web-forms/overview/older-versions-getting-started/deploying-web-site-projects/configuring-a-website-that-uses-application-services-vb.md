---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-a-website-that-uses-application-services-vb
title: 애플리케이션 서비스를 사용 하는 웹 사이트 구성 (VB) | Microsoft Docs
author: rick-anderson
description: ASP.NET 버전 2.0에는 일련의 응용 프로그램 서비스가 도입 되었습니다 .이 서비스는 .NET Framework의 일부 이며 ...
ms.author: riande
ms.date: 04/23/2009
ms.assetid: 9c31a42f-d8bb-4c0f-9ccc-597d4f70ac42
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-a-website-that-uses-application-services-vb
msc.type: authoredcontent
ms.openlocfilehash: 19e7258b558372259c7554a36c6ad73ce572dfa8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521657"
---
# <a name="configuring-a-website-that-uses-application-services-vb"></a>애플리케이션 서비스를 사용하는 웹 사이트 구성(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/E/6/F/E6FE3A1F-EE3A-4119-989A-33D1A9F6F6DD/ASPNET_Hosting_Tutorial_09_VB.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial09_AppServicesConfig_vb.pdf)

> ASP.NET 버전 2.0에는 .NET Framework의 일부 이며 웹 응용 프로그램에 다양 한 기능을 추가 하는 데 사용할 수 있는 블록 서비스를 구축 하는 일련의 응용 프로그램 서비스가 도입 되었습니다. 이 자습서에서는 프로덕션 환경에서 응용 프로그램 서비스를 사용 하도록 웹 사이트를 구성 하 고 프로덕션 환경에서 사용자 계정 및 역할을 관리 하는 것과 관련 된 일반적인 문제를 해결 하는 방법을 설명 합니다.

## <a name="introduction"></a>소개

ASP.NET 버전 2.0에는 .NET Framework의 일부 이며 웹 응용 프로그램에 다양 한 기능을 추가 하는 데 사용할 수 있는 블록 서비스를 구축 하는 일련의 *응용 프로그램 서비스가*도입 되었습니다. 응용 프로그램 서비스에는 다음이 포함 됩니다.

- **멤버 자격** -사용자 계정을 만들고 관리 하기 위한 API입니다.
- **역할** -사용자를 그룹으로 분류 하기 위한 API입니다.
- **Profile** -사용자 지정 사용자 관련 콘텐츠를 저장 하기 위한 API입니다.
- **사이트 맵** -계층 구조 형식으로 사이트의 논리 구조를 정의 하는 API로,이 API는 메뉴 및 이동 경로와 같은 탐색 컨트롤을 통해 표시 될 수 있습니다.
- **개인 설정** -사용자 지정 기본 설정을 유지 관리 하기 위한 API로, 주로 [*웹 파트*](https://msdn.microsoft.com/library/e0s9t4ck.aspx)에 사용 됩니다.
- **상태 모니터링** -실행 중인 웹 응용 프로그램에 대 한 성능, 보안, 오류 및 기타 시스템 상태 메트릭을 모니터링 하기 위한 API입니다.

응용 프로그램 서비스 Api는 특정 구현과 연결 되지 않습니다. 대신 특정 *공급자*를 사용 하도록 응용 프로그램 서비스에 지시 하 고 해당 공급자는 특정 기술을 사용 하 여 서비스를 구현 합니다. 웹 호스팅 회사에서 호스트 되는 인터넷 기반 웹 응용 프로그램에 가장 일반적으로 사용 되는 공급자는 SQL Server 데이터베이스 구현을 사용 하는 공급자입니다. 예를 들어 `SqlMembershipProvider`는 Microsoft SQL Server 데이터베이스에 사용자 계정 정보를 저장 하는 멤버 자격 API에 대 한 공급자입니다.

응용 프로그램 서비스 및 SQL Server 공급자를 사용 하면 응용 프로그램을 배포할 때 몇 가지 과제가 추가 됩니다. 먼저 응용 프로그램 서비스 데이터베이스 개체를 개발 데이터베이스와 프로덕션 데이터베이스 모두에서 적절히 생성 하 고 적절 하 게 초기화 해야 합니다. 또한 수행 해야 하는 중요 한 구성 설정이 있습니다.

> [!NOTE]
> 응용 프로그램 서비스 Api는 런타임에 API 구현 세부 정보를 제공 하는 데 사용할 수 있는 디자인 패턴 인 [*공급자 모델*](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)을 사용 하 여 설계 되었습니다. .NET Framework는 SQL Server 데이터베이스 구현을 사용 하는 멤버 자격 및 역할 Api의 공급자 인 `SqlMembershipProvider` 및 `SqlRoleProvider`와 같이 사용할 수 있는 여러 응용 프로그램 서비스 공급자와 함께 제공 됩니다. 사용자 지정 공급자를 만들고 플러그 인할 수도 있습니다. 실제로 책 리뷰 웹 응용 프로그램에는 사이트 맵 API (`ReviewSiteMapProvider`)에 대 한 사용자 지정 공급자가 이미 포함 되어 있으며,이 공급자는 `Genres` 데이터에서 사이트 맵을 생성 하 고 데이터베이스에 `Books` 테이블을 생성 합니다.

이 자습서에서는 책 리뷰 웹 응용 프로그램을 확장 하 여 멤버 자격 및 역할 Api를 사용 하는 방법을 살펴봅니다. 그런 다음 SQL Server 데이터베이스 구현에 응용 프로그램 서비스를 사용 하는 웹 응용 프로그램을 배포 하는 과정을 안내 하 고 프로덕션 환경에서 사용자 계정 및 역할을 관리 하는 일반적인 문제를 해결 합니다.

## <a name="updates-to-the-book-reviews-application"></a>책 리뷰 응용 프로그램에 대 한 업데이트

이전 몇 가지 자습서를 통해 책 리뷰 웹 응용 프로그램은 정적 웹 사이트에서 동적 데이터 기반 웹 응용 프로그램으로 업데이트 되었으며, 장르 및 리뷰 관리를 위한 일련의 관리 페이지가 포함 되어 있습니다. 그러나이 관리 섹션은 현재 보호 되지 않습니다. 사용자가 관리 페이지 URL을 waltz 하 고 사이트에서 검토를 생성, 편집 또는 삭제할 수 있습니다. 웹 사이트의 특정 부분을 보호 하는 일반적인 방법은 사용자 계정을 구현한 다음 URL 권한 부여 규칙을 사용 하 여 특정 사용자 또는 역할에 대 한 액세스를 제한 하는 것입니다. 이 자습서에서는 웹 응용 프로그램에서 다운로드할 수 있는 웹 응용 프로그램을 검토 하 여 사용자 계정 및 역할을 지원 합니다. 이 역할에는 Admin 이라는 단일 역할이 정의 되며이 역할의 사용자만 관리 페이지에 액세스할 수 있습니다.

> [!NOTE]
> 북 리뷰 웹 응용 프로그램에서 Scott, Jisun, Alice 라는 세 개의 사용자 계정을 만들었습니다. 세 사용자 모두 암호는 동일 합니다. **password!** Scott 및 Jisun은 관리자 역할에 있지 않으며 Alice는 그렇지 않습니다. 사이트 s 관리 되지 않는 페이지는 익명 사용자가 계속 액세스할 수 있습니다. 즉, 관리자 역할에서 사용자로 로그인 해야 하는 경우를 제외 하 고는 사이트를 방문 하기 위해 로그인 할 필요가 없습니다.

책 리뷰 응용 프로그램 마스터 페이지는 인증 된 사용자와 익명 사용자에 대해 다른 사용자 인터페이스를 포함 하도록 업데이트 되었습니다. 익명 사용자가 사이트를 방문 하는 경우 오른쪽 위 모서리에 로그인 링크가 표시 됩니다. 인증 된 사용자에 게 "환영 뒤로, *사용자 이름*!" 이라는 메시지가 표시 됩니다. 로그 아웃 링크를 만듭니다. 또한 방문자를 인증 하기 위한 사용자 인터페이스와 논리를 제공 하는 로그인 웹 컨트롤이 포함 된 로그인 페이지 (`~/Login.aspx`)가 있습니다. 관리자만 새 계정을 만들 수 있습니다. `~/Admin` 폴더에서 사용자 계정을 만들고 관리 하는 페이지가 있습니다.

### <a name="configuring-the-membership-and-roles-apis"></a>멤버 자격 및 역할 Api 구성

책 리뷰 웹 응용 프로그램은 멤버 자격과 역할 Api를 사용 하 여 사용자 계정을 지원 하 고 해당 사용자를 역할 (즉, 관리자 역할)로 그룹화 합니다. `SqlMembershipProvider` 및 `SqlRoleProvider` 공급자 클래스는 SQL Server 데이터베이스에 계정 및 역할 정보를 저장 하려고 하기 때문에 사용 됩니다.

> [!NOTE]
> 이 자습서는 멤버 자격 및 역할 Api를 지원 하도록 웹 응용 프로그램을 구성 하는 방법에 대 한 자세한 검사를 위한 것이 아닙니다. 이러한 Api와 웹 사이트를 사용 하도록 구성 하기 위해 수행 해야 하는 단계에 대 한 자세한 내용은 [*웹 사이트 보안 자습서*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)를 참조 하세요.

SQL Server 데이터베이스에 응용 프로그램 서비스를 사용 하려면 먼저 이러한 공급자가 사용 하는 데이터베이스 개체를 사용자 계정 및 역할 정보를 저장 하려는 데이터베이스에 추가 해야 합니다. 이러한 필수 데이터베이스 개체에는 다양 한 테이블, 뷰 및 저장 프로시저가 포함 됩니다. 달리 지정 되지 않은 경우 `SqlMembershipProvider` 및 `SqlRoleProvider` 공급자 클래스는 응용 프로그램의 `App_Data` 폴더에 있는 `ASPNETDB` 이라는 SQL Server Express Edition 데이터베이스를 사용 합니다. 이러한 데이터베이스가 없는 경우 런타임에 이러한 공급자가 필요한 데이터베이스 개체를 사용 하 여 자동으로 만들어집니다.

웹 사이트의 응용 프로그램 관련 데이터가 저장 되는 동일한 데이터베이스에서 응용 프로그램 서비스 데이터베이스 개체를 만드는 것이 일반적으로 이상적인 방법입니다. .NET Framework는 지정 된 데이터베이스에 데이터베이스 개체를 설치 하는 `aspnet_regsql.exe` 라는 도구와 함께 제공 됩니다. 이 도구를 사용 하 여 `App_Data` 폴더 (개발 데이터베이스)의 `Reviews.mdf` 데이터베이스에 이러한 개체를 추가 했습니다. 프로덕션 데이터베이스에 이러한 개체를 추가할 때이 자습서의 뒷부분에서이 도구를 사용 하는 방법을 살펴보겠습니다.

`ASPNETDB` 이외의 데이터베이스에 응용 프로그램 서비스 데이터베이스 개체를 추가 하는 경우 `SqlMembershipProvider` 및 `SqlRoleProvider` 공급자 클래스 구성을 사용자 지정 하 여 적절 한 데이터베이스를 사용 하도록 해야 합니다. 멤버 자격 공급자를 사용자 지정 하려면 `Web.config`의 `<system.web>` 섹션 내에 [ *&lt;멤버 자격&gt; 요소*](https://msdn.microsoft.com/library/1b9hw62f.aspx) 를 추가 합니다. [ *&lt;roleManager&gt; 요소*](https://msdn.microsoft.com/library/ms164660.aspx) 를 사용 하 여 역할 공급자를 구성 합니다. 다음 코드 조각은 서적 검토 응용 `Web.config` 프로그램에서 가져온 것으로, 멤버 자격 및 역할 Api에 대 한 구성 설정을 보여 줍니다. 둘 다 `SqlMembershipProvider` 및 `SqlRoleProvider` 공급자를 사용 하는 새 공급자 `ReviewMembership` 및 `ReviewRole`를 등록 합니다.

[!code-xml[Main](configuring-a-website-that-uses-application-services-vb/samples/sample1.xml)]

`Web.config` 파일 s `<authentication>` 요소도 폼 기반 인증을 지원 하도록 구성 되었습니다.

[!code-xml[Main](configuring-a-website-that-uses-application-services-vb/samples/sample2.xml)]

### <a name="limiting-access-to-the-administration-pages"></a>관리 페이지에 대 한 액세스 제한

ASP.NET를 사용 하면 *URL 권한 부여* 기능을 통해 사용자 또는 역할별로 특정 파일 또는 폴더에 대 한 액세스 권한을 쉽게 부여 하거나 거부할 수 있습니다. ( *Iis와 ASP.NET 개발 서버 자습서의 핵심 차이점* 에서 url 권한 부여를 간략하게 설명 하 고 iis 및 ASP.NET 개발 서버가 정적 및 동적 콘텐츠에 대해 url 권한 부여 규칙을 다르게 적용 하는 방법을 살펴보았습니다. 관리자 역할의 사용자를 제외 하 고 `~/Admin` 폴더에 대 한 액세스를 금지 하려면이 폴더에 URL 권한 부여 규칙을 추가 해야 합니다. 특히 URL 권한 부여 규칙은 관리자 역할의 사용자를 허용 하 고 다른 모든 사용자를 거부 해야 합니다. 이 작업을 수행 하려면 다음 내용을 사용 하 여 `~/Admin` 폴더에 `Web.config` 파일을 추가 합니다.

[!code-xml[Main](configuring-a-website-that-uses-application-services-vb/samples/sample3.xml)]

ASP.NET s URL 권한 부여 기능 및이 기능을 사용 하 여 사용자 및 역할에 대 한 권한 부여 규칙을 설명 하는 방법에 대 한 자세한 내용은 내 [*웹 사이트 보안 자습서*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)에서 [*사용자 기반 권한*](../../older-versions-security/membership/user-based-authorization-vb.md) 부여 및 [*역할 기반 권한 부여*](../../older-versions-security/roles/role-based-authorization-vb.md) 자습서를 참조 하세요.

## <a name="deploying-a-web-application-that-uses-application-services"></a>애플리케이션 서비스를 사용 하는 웹 응용 프로그램 배포

응용 프로그램 서비스를 사용 하는 웹 사이트와 응용 프로그램 서비스 정보를 데이터베이스에 저장 하는 공급자를 배포 하는 경우 응용 프로그램 서비스에 필요한 데이터베이스 개체를 프로덕션 데이터베이스에 만들어야 합니다. 처음에는 프로덕션 데이터베이스에 이러한 개체가 포함 되어 있지 않으므로 응용 프로그램을 처음 배포할 때 (또는 응용 프로그램 서비스를 추가한 후 처음으로 배포 하는 경우)에는 추가 단계를 수행 하 여 다음과 같은 필수 데이터베이스 개체를 가져와야 합니다. 프로덕션 데이터베이스.

개발 환경에서 만든 사용자 계정을 프로덕션 환경에 복제 하려는 경우 응용 프로그램 서비스를 사용 하는 웹 사이트를 배포할 때 또 다른 과제가 발생할 수 있습니다. 멤버 자격 및 역할 구성에 따라 개발 환경에서 만든 사용자 계정을 프로덕션 데이터베이스로 성공적으로 복사 하는 경우에도 이러한 사용자는 프로덕션에서 웹 응용 프로그램에 로그인 할 수 없게 될 수 있습니다. 이 문제의 원인을 확인 하 고이를 방지 하는 방법에 대해 설명 합니다.

ASP.NET는 Visual Studio에서 시작할 수 있는 훌륭한 [*웹 사이트 관리 도구 (WSAT)* ](https://msdn.microsoft.com/library/yy40ytx0.aspx) 와 함께 제공 되며, 웹 기반 인터페이스를 통해 사용자 계정, 역할 및 권한 부여 규칙을 관리할 수 있습니다. 아쉽게도 WSAT는 로컬 웹 사이트에 대해서만 작동 합니다. 즉, 프로덕션 환경에서 웹 응용 프로그램에 대 한 사용자 계정, 역할 및 권한 부여 규칙을 원격으로 관리 하는 데 사용할 수 없습니다. 프로덕션 웹 사이트에서 WSAT와 유사한 동작을 구현 하는 다양 한 방법을 살펴보겠습니다.

### <a name="adding-the-database-objects-using-aspnet_regsqlexe"></a>Sql server aspnet\_를 사용 하 여 데이터베이스 개체 추가

*데이터베이스 배포* 자습서에서는 개발 데이터베이스에서 프로덕션 데이터베이스로 테이블 및 데이터를 복사 하는 방법을 보여 주었습니다. 이러한 기술은 응용 프로그램 서비스 데이터베이스 개체를 프로덕션 데이터베이스에 복사 하는 데 사용할 수 있습니다. 또 다른 옵션은 데이터베이스에서 응용 프로그램 서비스 데이터베이스 개체를 추가 하거나 제거 하는 `aspnet_regsql.exe` 도구입니다.

> [!NOTE]
> `aspnet_regsql.exe` 도구는 지정 된 데이터베이스에 데이터베이스 개체를 만듭니다. 이러한 데이터베이스 개체의 데이터를 개발 데이터베이스에서 프로덕션 데이터베이스로 마이그레이션하지 않습니다. 개발 데이터베이스의 사용자 계정 및 역할 정보를 프로덕션 데이터베이스에 복사 하는 것을 의미 하는 경우에는 *데이터베이스 배포* 자습서에서 설명 하는 기술을 사용 합니다.

`aspnet_regsql.exe` 도구를 사용 하 여 프로덕션 데이터베이스에 데이터베이스 개체를 추가 하는 방법을 살펴보겠습니다. Windows 탐색기를 열고 컴퓨터의 .NET Framework 버전 2.0 디렉터리 (% WINDIR% \)로 이동 하 여 시작 합니다. NET\Framework\v2.0.50727. `aspnet_regsql.exe` 도구를 찾아야 합니다. 이 도구는 명령줄에서 사용할 수 있지만 그래픽 사용자 인터페이스도 포함 합니다. `aspnet_regsql.exe` 파일을 두 번 클릭 하 여 그래픽 구성 요소를 시작 합니다.

도구는 해당 용도를 설명 하는 시작 화면을 표시 합니다. 다음을 클릭 하 여 그림 1에 표시 된 "설치 옵션 선택" 화면으로 이동 합니다. 여기에서 응용 프로그램 서비스 데이터베이스 개체를 추가 하거나 데이터베이스에서 제거 하도록 선택할 수 있습니다. 이러한 개체를 프로덕션 데이터베이스에 추가 하려면 "응용 프로그램 서비스에 대 한 SQL Server 구성" 옵션을 선택 하 고 다음을 클릭 합니다.

[![애플리케이션 서비스에 대 한 SQL Server를 구성 하도록 선택 합니다.](configuring-a-website-that-uses-application-services-vb/_static/image2.jpg)](configuring-a-website-that-uses-application-services-vb/_static/image1.jpg)

**그림 1**: 애플리케이션 서비스에 대 한 SQL Server를 구성 하도록 선택 ([전체 크기 이미지를 보려면 클릭](configuring-a-website-that-uses-application-services-vb/_static/image3.jpg))

"서버 및 데이터베이스 선택" 화면에서 데이터베이스에 연결 하는 데 필요한 정보를 묻는 메시지를 표시 합니다. 웹 호스팅 회사에서 제공 하는 데이터베이스 서버, 보안 자격 증명 및 데이터베이스 이름을 입력 하 고 다음을 클릭 합니다.

> [!NOTE]
> 데이터베이스 서버 및 자격 증명을 입력 한 후 데이터베이스 드롭다운 목록을 확장 하면 오류가 발생할 수 있습니다. `aspnet_regsql.exe` 도구는 `sysdatabases` 시스템 테이블을 쿼리하여 서버에 있는 데이터베이스 목록을 검색 하지만 일부 웹 호스팅 회사는이 정보를 공개적으로 사용할 수 없도록 데이터베이스 서버를 잠급니다. 이 오류가 발생 하면 드롭다운 목록에 데이터베이스 이름을 직접 입력할 수 있습니다.

[데이터베이스 연결 정보를 사용 하 여 도구를 제공 ![](configuring-a-website-that-uses-application-services-vb/_static/image5.jpg)](configuring-a-website-that-uses-application-services-vb/_static/image4.jpg)

**그림 2**: 데이터베이스 연결 정보를 사용 하 여 도구 제공 ([전체 크기 이미지를 보려면 클릭](configuring-a-website-that-uses-application-services-vb/_static/image6.jpg))

이후 화면에는 응용 프로그램 서비스 데이터베이스 개체가 지정 된 데이터베이스에 추가 될 예정입니다. 다음을 클릭 하 여이 작업을 완료 합니다. 몇 분 후에 데이터베이스 개체가 추가 되었음을 알리는 최종 화면이 표시 됩니다 (그림 3 참조).

[성공 ![프로덕션 데이터베이스에 애플리케이션 서비스 데이터베이스 개체가 추가 되었습니다.](configuring-a-website-that-uses-application-services-vb/_static/image8.jpg)](configuring-a-website-that-uses-application-services-vb/_static/image7.jpg)

**그림 3**: 성공! 애플리케이션 서비스 데이터베이스 개체가 프로덕션 데이터베이스에 추가 되었습니다 ([전체 크기 이미지를 보려면 클릭](configuring-a-website-that-uses-application-services-vb/_static/image9.jpg)).

응용 프로그램 서비스 데이터베이스 개체가 프로덕션 데이터베이스에 성공적으로 추가 되었는지 확인 하려면 SQL Server Management Studio를 열고 프로덕션 데이터베이스에 연결 합니다. 그림 4에 표시 된 것 처럼 이제 데이터베이스, `aspnet_Applications`, `aspnet_Membership`, `aspnet_Users`등에 응용 프로그램 서비스 데이터베이스 테이블이 표시 됩니다.

[데이터베이스 개체가 프로덕션 데이터베이스에 추가 되었는지 확인 ![](configuring-a-website-that-uses-application-services-vb/_static/image11.jpg)](configuring-a-website-that-uses-application-services-vb/_static/image10.jpg)

**그림 4**: 데이터베이스 개체가 프로덕션 데이터베이스에 추가 되었는지 확인 ([전체 크기 이미지를 보려면 클릭](configuring-a-website-that-uses-application-services-vb/_static/image12.jpg))

처음으로 웹 응용 프로그램을 배포 하거나 응용 프로그램 서비스 사용을 시작한 후 처음으로 `aspnet_regsql.exe` 도구를 사용 해야 합니다. 이러한 데이터베이스 개체가 프로덕션 데이터베이스에 있으면 다시 추가 하거나 수정할 필요가 없습니다.

### <a name="copying-user-accounts-from-development-to-production"></a>개발에서 프로덕션으로 사용자 계정 복사

`SqlMembershipProvider` 및 `SqlRoleProvider` 공급자 클래스를 사용 하 여 SQL Server 데이터베이스에 응용 프로그램 서비스 정보를 저장 하는 경우 사용자 계정 및 역할 정보는 `aspnet_Users`, `aspnet_Membership`, `aspnet_Roles`및 `aspnet_UsersInRoles`를 비롯 한 다양 한 데이터베이스 테이블에 저장 됩니다. 개발 중에 개발 환경에서 사용자 계정을 만드는 경우 해당 하는 데이터베이스 테이블에서 해당 레코드를 복사 하 여 프로덕션에서 해당 사용자 계정을 복제할 수 있습니다. 데이터베이스 게시 마법사를 사용 하 여 응용 프로그램 서비스 데이터베이스 개체를 배포한 경우에도 레코드를 복사 하도록 선택 했을 수 있습니다. 이렇게 하면 개발에서 만든 사용자 계정이 프로덕션 환경에도 포함 됩니다. 그러나 구성 설정에 따라 계정이 개발에서 만들어지고 프로덕션 환경으로 복사 된 사용자가 프로덕션 웹 사이트에서 로그인 할 수 없다는 것을 알 수 있습니다. 무엇을 제공하나요?

`SqlMembershipProvider` 및 `SqlRoleProvider` 공급자 클래스는 단일 데이터베이스를 여러 응용 프로그램에 대 한 사용자 저장소로 사용할 수 있도록 설계 되었습니다. 각 응용 프로그램에는 동일한 이름의 사용자 이름 및 역할이 겹치는 사용자가 있습니다. 이러한 유연성을 위해 데이터베이스는 `aspnet_Applications` 테이블의 응용 프로그램 목록을 유지 관리 하 고 각 사용자는 이러한 응용 프로그램 중 하 나와 연결 됩니다. 특히 `aspnet_Users` 테이블에는 각 사용자를 `aspnet_Applications` 테이블의 레코드에 연결 하는 `ApplicationId` 열이 있습니다.

`ApplicationId` 열 외에도 `aspnet_Applications` 테이블에는 응용 프로그램에 대해 사용자에 게 친숙 한 이름을 제공 하는 `ApplicationName` 열이 포함 되어 있습니다. 웹 사이트가 로그인 페이지에서 사용자 자격 증명의 유효성을 검사 하는 등의 사용자 계정으로 작업을 시도 하는 경우 `SqlMembershipProvider` 클래스에 사용할 응용 프로그램을 알려야 합니다. 이는 일반적으로 응용 프로그램 이름을 제공 하 여이를 수행 하며,이 값은 `applicationName` 특성을 통해 `Web.config`의 공급자 구성에서 제공 됩니다.

하지만 `Web.config`에서 `applicationName` 특성을 지정 하지 않으면 어떻게 되나요? 이 경우 멤버 자격 시스템은 응용 프로그램 루트 경로를 `applicationName` 값으로 사용 합니다. `Web.config`에서 `applicationName` 특성을 명시적으로 설정 하지 않은 경우 개발 환경 및 프로덕션 환경에서 다른 응용 프로그램 루트를 사용 하 여 응용 프로그램 서비스에서 다른 응용 프로그램 이름과 연결할 가능성이 있습니다. 이러한 불일치가 발생 하면 개발 환경에서 만든 사용자에 게 프로덕션 환경의 `ApplicationId` 값과 일치 하지 않는 `ApplicationId` 값이 포함 됩니다. 결과적으로 해당 사용자가 로그인 할 수 없습니다.

> [!NOTE]
> 이러한 상황에서 사용자 계정이 일치 하지 않는 `ApplicationId` 값을 사용 하 여 프로덕션에 복사 된 경우, 이러한 잘못 된 `ApplicationId` 값을 프로덕션에 사용 되는 `ApplicationId`로 업데이트 하는 쿼리를 작성할 수 있습니다. 업데이트 된 후 개발 환경에서 계정이 만들어진 사용자는 이제 프로덕션 환경에서 웹 응용 프로그램에 로그인 할 수 있습니다.

좋은 소식은 두 환경에서 동일한 `ApplicationId` 사용 하 고 모든 응용 프로그램 서비스 공급자에 대해 `Web.config`에서 `applicationName` 특성을 명시적으로 설정 하기 위해 수행할 수 있는 간단한 단계가 있다는 것입니다. `<membership>`에서 `applicationName` 특성을 "BookReviews"로 명시적으로 설정 하 고 `Web.config`에서이 조각과 `<roleManager>` 요소를 표시 합니다.

[!code-xml[Main](configuring-a-website-that-uses-application-services-vb/samples/sample4.xml)]

`applicationName` 특성을 설정 하는 방법 및 그에 대 한 설명에 대 한 자세한 내용은 [*Scott Guthrie*](https://weblogs.asp.net/scottgu/) s 블로그 게시물을 참조 하 고 [*ASP.NET 멤버 자격 및 기타 공급자를 구성할 때 항상 applicationName 속성을 설정*](https://weblogs.asp.net/scottgu/443634)합니다.

### <a name="managing-user-accounts-in-the-production-environment"></a>프로덕션 환경의 사용자 계정 관리

ASP.NET 웹 사이트 관리 도구 (WSAT)를 사용 하면 사용자 계정을 쉽게 만들고 관리 하 고, 역할을 정의 하 고 적용 하 고, 사용자 및 역할 기반 권한 부여 규칙을 쉽게 확인할 수 있습니다. 솔루션 탐색기로 이동 하 고 ASP.NET 구성 아이콘을 클릭 하거나 웹 사이트 또는 프로젝트 메뉴로 이동 하 고 ASP.NET 구성 메뉴 항목을 선택 하 여 Visual Studio에서 WSAT를 시작할 수 있습니다. 아쉽게도 WSAT는 로컬 웹 사이트에만 사용할 수 있습니다. 따라서 워크스테이션에서 WSAT를 사용 하 여 프로덕션 환경에서 웹 사이트를 관리할 수 없습니다.

좋은 소식은 WSAT에서 제공 하는 모든 기능을 멤버 자격 및 역할 Api를 통해 프로그래밍 방식으로 사용할 수 있다는 것입니다. 또한 대부분의 WSAT 화면은 표준 ASP.NET 로그인 관련 컨트롤을 사용 합니다. 간단히 말해서 필요한 관리 기능을 제공 하는 ASP.NET 페이지를 웹 사이트에 추가할 수 있습니다.

이전 자습서에서는 책 리뷰 웹 응용 프로그램을 업데이트 하 여 `~/Admin` 폴더를 포함 하 고 있으며이 폴더는 관리자 역할의 사용자만 허용 하도록 구성 되어 있습니다. 관리자가 새 사용자 계정을 만들 수 있는 `CreateAccount.aspx` 라는 폴더에 페이지를 추가 했습니다. 이 페이지에서는 CreateUserWizard 컨트롤을 사용 하 여 새 사용자 계정을 만들기 위한 사용자 인터페이스와 백 엔드 논리를 표시 합니다. 무엇 보다도 새 사용자를 관리자 역할에 추가 해야 하는지 여부를 묻는 확인란을 포함 하도록 컨트롤을 사용자 지정 했습니다 (그림 5 참조). 약간의 작업을 통해 WSAT에서 제공 하는 사용자 및 역할 관리 관련 작업을 구현 하는 페이지의 사용자 지정 집합을 빌드할 수 있습니다.

> [!NOTE]
> 로그인 관련 ASP.NET 웹 컨트롤과 함께 멤버 자격 및 역할 Api를 사용 하는 방법에 대 한 자세한 내용은 [*웹 사이트 보안 자습서*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)를 참조 하세요. CreateUserWizard 컨트롤을 사용자 지정 하는 방법에 대 한 자세한 내용은 [*사용자 계정 만들기*](../../older-versions-security/membership/creating-user-accounts-vb.md) 및 [*추가 사용자 정보 저장*](../../older-versions-security/membership/storing-additional-user-information-vb.md) 자습서를 참조 하거나 [*CreateUserWizard 컨트롤을 사용자 지정*](http://aspnet.4guysfromrolla.com/articles/070506-1.aspx)하 여 [*erich Peterson*](http://www.erichpeterson.com/) s 문서를 참조 하세요.

[![관리자는 새 사용자 계정을 만들 수 있습니다.](configuring-a-website-that-uses-application-services-vb/_static/image14.jpg)](configuring-a-website-that-uses-application-services-vb/_static/image13.jpg)

**그림 5**: 관리자가 새 사용자 계정을 만들 수 있습니다 ([전체 크기 이미지를 보려면 클릭](configuring-a-website-that-uses-application-services-vb/_static/image15.jpg)).

WSAT의 전체 기능을 확인 해야 하는 경우 사용자 지정 WSAT와 유사한 도구를 빌드하는 과정을 안내 하는 작성자의 [*웹 사이트 관리 도구*](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)를 확인 합니다. Dan은 응용 프로그램의 C#소스 코드 ()를 공유 하 고 호스트 된 웹 사이트에 추가 하는 방법에 대 한 단계별 지침을 제공 합니다.

## <a name="summary"></a>요약

응용 프로그램 서비스 데이터베이스 구현을 사용 하는 웹 응용 프로그램을 배포할 때 먼저 프로덕션 데이터베이스에 필수 데이터베이스 개체가 있는지 확인 해야 합니다. 이러한 개체는 *데이터베이스 배포* 자습서에 설명 된 기술을 사용 하 여 추가할 수 있습니다. 또는이 자습서에서 살펴본 것 처럼 `aspnet_regsql.exe` 도구를 사용할 수 있습니다. 개발 및 프로덕션 환경에서 사용 되는 응용 프로그램 이름 동기화를 중심으로 작업 하는 기타 과제 (프로덕션 환경에서 개발 환경에서 만든 사용자 및 역할을 사용 하려는 경우 중요) 및에 대 한 기술 프로덕션 환경에서 사용자 및 역할 관리

행복 한 프로그래밍

### <a name="further-reading"></a>추가 참고 자료

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [*ASP.NET SQL Server 등록 도구 (aspnet_regsql)* ](https://msdn.microsoft.com/library/ms229862.aspx)
- [*SQL Server에 대 한 애플리케이션 서비스 데이터베이스 만들기*](https://msdn.microsoft.com/library/x28wfk74.aspx)
- [*SQL Server에서 멤버 자격 스키마 만들기*](../../older-versions-security/membership/creating-the-membership-schema-in-sql-server-vb.md)
- [*ASP.NET s 멤버 자격, 역할 및 프로필 검사*](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [*사용자 고유의 웹 사이트 관리 도구 롤링*](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [*웹 사이트 보안 자습서*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)
- [*웹 사이트 관리 도구 개요*](https://msdn.microsoft.com/library/yy40ytx0.aspx)

> [!div class="step-by-step"]
> [이전](configuring-the-production-web-application-to-use-the-production-database-vb.md)
> [다음](strategies-for-database-development-and-deployment-vb.md)
