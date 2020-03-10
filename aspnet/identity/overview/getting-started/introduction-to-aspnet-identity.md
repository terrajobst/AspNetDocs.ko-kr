---
uid: identity/overview/getting-started/introduction-to-aspnet-identity
title: ASP.NET Identity 소개-ASP.NET 4.x
author: jongalloway
description: ASP.NET 멤버 자격 시스템은 2005에서 ASP.NET 2.0에 다시 도입 된 것으로, 웹 응용 프로그램의 typicall ...
ms.author: riande
ms.date: 01/22/2019
ms.assetid: 38717fc1-5989-43cf-952d-4007cc1dd923
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/introduction-to-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 0268dfc16cd2cfb1e79ee14997a4c5eb247af950
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471737"
---
# <a name="introduction-to-aspnet-identity"></a>ASP.NET Identity 소개

> ASP.NET 멤버 자격 시스템은 2005의 ASP.NET 2.0에 다시 도입 된 것으로, 웹 응용 프로그램이 일반적으로 인증 및 권한 부여를 처리 하는 방법에 많은 변화가 있었습니다. ASP.NET Identity는 웹, 휴대폰 또는 태블릿에 대 한 최신 응용 프로그램을 빌드할 때 멤버 자격 시스템을 새로 디자인 하는 것입니다.

## <a name="background-membership-in-aspnet"></a>배경: ASP.NET의 멤버 자격

### <a name="aspnet-membership"></a>ASP.NET 멤버 자격

[ASP.NET 멤버 자격은](https://msdn.microsoft.com/library/yh26yfzy(v=VS.100).aspx) 폼 인증 및 사용자 이름, 암호 및 프로필 데이터에 대 한 SQL Server 데이터베이스와 관련 된 2005에서 공통적으로 적용 되는 사이트 멤버 자격 요구 사항을 해결 하도록 설계 되었습니다. 현재 웹 응용 프로그램에 대 한 다양 한 데이터 저장소 옵션 배열이 있으며 대부분의 개발자는 사이트에서 인증 및 권한 부여 기능을 위해 소셜 id 공급자를 사용할 수 있도록 합니다. ASP.NET 멤버 자격 디자인의 제한 사항으로 인해 이러한 전환이 어려워집니다.

- 데이터베이스 스키마는 SQL Server 용으로 설계 되었으며 변경할 수 없습니다. 프로필 정보를 추가할 수 있지만 추가 데이터는 다른 테이블에 압축 되므로 프로필 공급자 API를 제외 하 고는 어떤 방법으로도 액세스 하기 어렵습니다.
- 공급자 시스템을 사용 하면 지원 데이터 저장소를 변경할 수 있지만 시스템은 관계형 데이터베이스에 대 한 적절 한 가정을 기반으로 설계 되었습니다. Azure Storage 테이블과 같은 비관계형 저장소 메커니즘에 멤버 자격 정보를 저장 하는 공급자를 작성할 수 있지만, NoSQL 데이터베이스에 적용 되지 않는 메서드에 대 한 많은 코드와 많은 `System.NotImplementedException` 예외를 작성 하 여 관계형 설계를 해결 해야 합니다.
- 로그인/로그 아웃 기능은 폼 인증을 기반으로 하기 때문에 멤버 자격 시스템에서는 [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)를 사용할 수 없습니다. OWIN에는 외부 id 공급자 (예: Microsoft 계정, Facebook, Google, Twitter)를 사용 하 여 로그인을 지원 하 고 온-Active Directory 프레미스에서 조직 계정을 사용 하 여 로그인 하는 것을 비롯 하 여 인증을 위한 미들웨어 구성 요소가 포함 됩니다. 또는 Azure Active Directory. OWIN에는 OAuth 2.0, JWT 및 CORS도 지원 됩니다.

### <a name="aspnet-simple-membership"></a>ASP.NET 단순 멤버 자격

[ASP.NET 단순 멤버 자격은](../../../web-pages/overview/security/16-adding-security-and-membership.md) ASP.NET 웹 페이지에 대 한 멤버 자격 시스템으로 개발 되었습니다. WebMatrix 및 Visual Studio 2010 s p 1과 함께 출시 되었습니다. 간단한 멤버 자격의 목표는 웹 페이지 응용 프로그램에 멤버 자격 기능을 쉽게 추가할 수 있도록 하는 것 이었습니다.

간단한 구성원 자격으로 사용자 프로필 정보를 쉽게 사용자 지정할 수 있지만 ASP.NET 멤버 자격과 관련 된 다른 문제를 여전히 공유 하 고 몇 가지 제한 사항이 있습니다.

- 관계형이 아닌 저장소에 멤버 자격 시스템 데이터를 유지 하기는 어렵습니다.
- OWIN와 함께 사용할 수 없습니다.
- 기존 ASP.NET 멤버 자격 공급자와는 잘 작동 하지 않으며 확장할 수 없습니다.

### <a name="aspnet-universal-providers"></a>ASP.NET 범용 공급자

[ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx) 은 Microsoft Azure SQL Database에 멤버 자격 정보를 유지할 수 있도록 개발 되었으며 SQL Server Compact 에서도 작동 합니다. Universal Providers은 Entity Framework Code First을 기반으로 작성 되었습니다. 즉, Universal Providers를 사용 하 여 EF에서 지 원하는 모든 저장소에 데이터를 유지할 수 있습니다. Universal Providers를 사용 하는 경우 데이터베이스 스키마도 상당히 많이 정리 되었습니다.

Universal Providers는 ASP.NET 멤버 자격 인프라를 기반으로 하므로 SqlMembership Provider와 동일한 제한 사항을 계속 제공 합니다. 즉, 관계형 데이터베이스용으로 설계 되었으며 프로필 및 사용자 정보를 사용자 지정 하기가 어렵습니다. 이러한 공급자는 로그인 및 로그 아웃 기능에도 폼 인증을 사용 합니다.

## <a name="aspnet-identity"></a>ASP.NET ID

ASP.NET의 멤버 자격 스토리가 년에 걸쳐 발전 함에 따라 ASP.NET 팀은 고객의 의견을 많이 얻었습니다.

사용자가 자신의 응용 프로그램에 등록 한 사용자 이름 및 암호를 입력 하 여 로그인 하는 것은 더 이상 유효 하지 않습니다. 웹이 더 소셜 되었습니다. 사용자는 Facebook, Twitter 및 기타 소셜 웹 사이트와 같은 소셜 채널을 통해 실시간으로 서로 상호 작용 합니다. 개발자는 자신의 웹 사이트에서 풍부한 환경을 사용할 수 있도록 사용자가 소셜 id를 사용 하 여 로그인 할 수 있도록 하려고 합니다. 최신 멤버 자격 시스템은 Facebook, Twitter 등의 인증 공급자에 대 한 리디렉션 기반 로그인을 사용 하도록 설정 해야 합니다.

웹 개발이 진화 함에 따라 웹 개발의 패턴을 했습니다. 응용 프로그램 코드의 단위 테스트는 응용 프로그램 개발자에 게 중요 한 문제입니다. 2008 ASP.NET는 개발자가 단위 테스트 가능한 ASP.NET 응용 프로그램을 빌드하는 데 도움이 되는 MVC (모델-뷰-컨트롤러) 패턴을 기반으로 새 프레임 워크를 추가 했습니다. 응용 프로그램 논리를 단위 테스트 하려는 개발자는 멤버 자격 시스템을 사용 하 여이 작업을 수행할 수 있습니다.

웹 응용 프로그램 개발의 이러한 변경을 고려 하 여 다음과 같은 목적으로 ASP.NET Identity 개발 되었습니다.

- **1 ASP.NET Identity 시스템**

    - ASP.NET Identity는 ASP.NET MVC, Web Forms, 웹 페이지, Web API 및 SignalR와 같은 모든 ASP.NET 프레임 워크와 함께 사용할 수 있습니다.
    - ASP.NET Identity는 웹, 휴대폰, 스토어 또는 하이브리드 응용 프로그램을 빌드할 때 사용할 수 있습니다.
- **사용자에 대 한 프로필 데이터의 용이성**

    - 사용자는 사용자 및 프로필 정보 스키마를 제어할 수 있습니다. 예를 들어 사용자가 응용 프로그램에 계정을 등록할 때 사용자가 입력 한 생년월일을 저장 하도록 시스템을 쉽게 설정할 수 있습니다.

- **지 속성 컨트롤**

    - 기본적으로 ASP.NET Identity 시스템은 모든 사용자 정보를 데이터베이스에 저장 합니다. ASP.NET Identity는 Entity Framework Code First를 사용 하 여 모든 지 속성 메커니즘을 구현 합니다.
    - 데이터베이스 스키마를 제어 하므로 테이블 이름을 변경 하거나 기본 키의 데이터 형식을 변경 하는 등의 일반적인 작업은 간단 합니다.
    - `System.NotImplementedExceptions` 예외를 throw 하지 않고도 SharePoint, Azure Storage Table Service, NoSQL 데이터베이스 등의 다양 한 저장소 메커니즘을 쉽게 연결할 수 있습니다.
- **유닛 테스트 용이성**

    - ASP.NET Identity를 사용 하면 웹 응용 프로그램을 더 많은 장치를 테스트할 수 있습니다. ASP.NET Identity를 사용 하는 응용 프로그램의 일부에 대 한 단위 테스트를 작성할 수 있습니다.
- **역할 공급자**

    - 역할을 통해 응용 프로그램의 일부에 대 한 액세스를 제한할 수 있는 역할 공급자가 있습니다. "관리자"와 같은 역할을 쉽게 만들고 역할에 사용자를 추가할 수 있습니다.
- **클레임 기반**

    - ASP.NET Identity은 클레임 기반 인증을 지원 합니다. 여기서 사용자의 id는 클레임 집합으로 표시 됩니다. 개발자는 클레임을 사용 하 여 역할에서 허용 하는 것 보다 사용자의 id를 설명할 때 훨씬 더 많은 정보를 사용할 수 있습니다. 역할 멤버 자격은 부울 (멤버 또는 비 멤버) 뿐 이지만 클레임에는 사용자의 id 및 멤버 자격에 대 한 다양 한 정보가 포함 될 수 있습니다.
- **소셜 로그인 공급자**

    - Microsoft 계정, Facebook, Twitter, Google 등의 소셜 로그인을 응용 프로그램에 쉽게 추가 하 고 사용자 관련 데이터를 응용 프로그램에 저장할 수 있습니다.

- **OWIN 통합**

    - ASP.NET 인증은 이제 모든 OWIN 기반 호스트에서 사용할 수 있는 OWIN 미들웨어를 기반으로 합니다. ASP.NET Identity은 System.web에 종속 되지 않습니다. 완벽 하 게 호환 되는 OWIN 프레임 워크 이며 모든 OWIN 호스팅된 응용 프로그램에서 사용할 수 있습니다.
    - ASP.NET Identity은 웹 사이트에서 사용자의 로그인/로그 아웃에 대해 OWIN 인증을 사용 합니다. 즉, FormsAuthentication를 사용 하 여 쿠키를 생성 하는 대신 응용 프로그램에서 OWIN CookieAuthentication를 사용 하 여이 작업을 수행 합니다.
- **NuGet 패키지**

    - ASP.NET Identity는 Visual Studio 2017와 함께 제공 되는 ASP.NET MVC, Web Forms 및 Web API 템플릿에 설치 되는 NuGet 패키지로 재배포할 수 있습니다. NuGet 갤러리에서이 NuGet 패키지를 다운로드할 수 있습니다.
    - ASP.NET Identity를 NuGet 패키지로 해제 하면 ASP.NET 팀이 새로운 기능 및 버그 수정을 반복 하 고 민첩 한 방식으로 개발자에 게 제공할 수 있습니다.

## <a name="get-started-with-aspnet-identity"></a>ASP.NET Identity 시작

ASP.NET Identity는 ASP.NET MVC, Web Forms, Web API 및 SPA에 대 한 Visual Studio 2017 프로젝트 템플릿에서 사용 됩니다. 이 연습에서는 프로젝트 템플릿이 ASP.NET Identity를 사용 하 여 사용자를 등록 하 고 로그인 하 고 로그 아웃 하는 기능을 추가 하는 방법을 설명 합니다.

ASP.NET Identity는 다음 절차를 사용 하 여 구현 됩니다. 이 문서의 목적은 ASP.NET Identity에 대 한 개략적인 개요를 제공 하는 것입니다. 이 단계를 단계별로 수행 하거나 세부 정보를 읽을 수 있습니다. 새 API를 사용 하 여 사용자, 역할 및 프로필 정보를 추가 하는 등 ASP.NET Identity를 사용 하 여 앱을 만드는 방법에 대 한 자세한 내용은이 문서의 끝에 있는 다음 단계 섹션을 참조 하세요.

1. 개별 계정으로 ASP.NET MVC 응용 프로그램을 만듭니다. ASP.NET MVC, Web Forms, Web API, SignalR 등에서 ASP.NET Identity를 사용할 수 있습니다. 이 문서에서는 ASP.NET MVC 응용 프로그램부터 시작 합니다.  
  
    ![](introduction-to-aspnet-identity/_static/image1.png)
2. 만든 프로젝트에는 ASP.NET Identity에 대 한 다음 3 개의 패키지가 포함 됩니다.

    - [`Microsoft.AspNet.Identity.EntityFramework`](http://www.nuget.org/packages/Microsoft.AspNet.Identity.EntityFramework/)  
   이 패키지에는 SQL Server에 대 한 ASP.NET Identity 데이터 및 스키마를 유지 하는 ASP.NET Identity Entity Framework 구현이 있습니다.
    - [`Microsoft.AspNet.Identity.Core`](http://www.nuget.org/packages/Microsoft.AspNet.Identity.Core/)  
   이 패키지에는 ASP.NET Identity에 대 한 핵심 인터페이스가 있습니다. 이 패키지를 사용 하 여 Azure Table Storage, NoSQL 데이터베이스 등의 서로 다른 지 속성 저장소를 대상으로 하는 ASP.NET Identity에 대 한 구현을 작성할 수 있습니다.
    - [`Microsoft.AspNet.Identity.OWIN`](http://www.nuget.org/packages/Microsoft.AspNet.Identity.Owin/)  
   이 패키지에는 ASP.NET 응용 프로그램의 ASP.NET Identity에 OWIN 인증을 연결 하는 데 사용 되는 기능이 포함 되어 있습니다. 응용 프로그램에 로그인 기능을 추가 하 고 OWIN 쿠키 인증 미들웨어를 호출 하 여 쿠키를 생성할 때 사용 됩니다.
3. 사용자 만들기  
   응용 프로그램을 시작 하 고 **등록** 링크를 클릭 하 여 사용자를 만듭니다. 다음 그림은 사용자 이름 및 암호를 수집 하는 등록 페이지를 보여 줍니다.  
  
    ![](introduction-to-aspnet-identity/_static/image2.png)  
  
   사용자가 **등록** 단추를 선택 하면 계정 컨트롤러의 `Register` 작업에서 아래 강조 표시 된 것 처럼 ASP.NET Identity API를 호출 하 여 사용자를 만듭니다.

    [!code-csharp[Main](introduction-to-aspnet-identity/samples/sample1.cs?highlight=8-9)]
4. 로그인합니다.  
   사용자가 성공적으로 만들어지면 `SignInAsync` 메서드로 로그인 됩니다.  

    [!code-csharp[Main](introduction-to-aspnet-identity/samples/sample6.cs?highlight=12)]

   `SignInManager.SignInAsync` 메서드는 [ClaimsIdentity](https://msdn.microsoft.com/library/system.security.claims.claimsidentity.aspx)을 생성 합니다. ASP.NET Identity 및 OWIN 쿠키 인증은 클레임 기반 시스템 이므로 프레임 워크를 사용 하려면 앱에서 사용자에 대 한 ClaimsIdentity를 생성 해야 합니다. ClaimsIdentity에는 사용자가 속한 역할 등 사용자에 대 한 모든 클레임에 대 한 정보가 있습니다.   
 
5. 로그 오프 합니다.  
   계정 컨트롤러에서 로그 오프 작업을 호출 하려면 **로그 오프** 링크를 선택 합니다. 

    [!code-csharp[Main](introduction-to-aspnet-identity/samples/sample5.cs?highlight=6)]

   위의 강조 표시 된 코드는 OWIN `AuthenticationManager.SignOut` 메서드를 보여 줍니다. 이는 Web Forms의 [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx) 모듈에서 사용 하는 SignOut 메서드와 유사 합니다 [.](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx)

## <a name="components-of-aspnet-identity"></a>ASP.NET Identity 구성 요소

아래 다이어그램은 ASP.NET Identity 시스템의 구성 요소를 보여 줍니다. [이](introduction-to-aspnet-identity/_static/image3.png) 구성 요소를 확장 하려면 다이어그램에서 선택 합니다. 녹색의 패키지는 ASP.NET Identity 시스템을 구성 합니다. 다른 모든 패키지는 ASP.NET 응용 프로그램에서 ASP.NET Identity 시스템을 사용 하는 데 필요한 종속성입니다.

[![](introduction-to-aspnet-identity/_static/image5.png)](introduction-to-aspnet-identity/_static/image4.png)

다음은 앞에서 언급 되지 않은 NuGet 패키지에 대 한 간단한 설명입니다.

- [Microsoft.Owin.Security.Cookies](http://www.nuget.org/packages/Microsoft.Owin.Security.Cookies/)  
 응용 프로그램에서 ASP와 비슷한 쿠키 기반 인증을 사용할 수 있도록 하는 미들웨어입니다. NET의 폼 인증.
- [EntityFramework](http://www.nuget.org/packages/EntityFramework/)  
 Entity Framework 관계형 데이터베이스에 대해 Microsoft에서 권장 하는 데이터 액세스 기술입니다.

## <a name="migrating-from-membership-to-aspnet-identity"></a>멤버 자격에서 ASP.NET Identity로 마이그레이션

ASP.NET 멤버 자격 또는 간단한 구성원 자격을 사용 하는 기존 앱을 새 ASP.NET Identity 시스템으로 마이그레이션하는 방법에 대 한 지침을 곧 제공할 예정입니다.

## <a name="next-steps"></a>다음 단계

- [Facebook 및 Google OAuth2 및 Openid connect Sign-on을 사용 하 여 ASP.NET MVC 5 앱 만들기](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)  
 이 자습서에서는 ASP.NET Identity API를 사용 하 여 사용자 데이터베이스에 프로필 정보를 추가 하 고 Google 및 Facebook으로 인증 하는 방법을 설명 합니다.
- [인증 및 SQL DB를 사용하여 ASP.NET MVC 앱을 만들고 Azure App Service에 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)  
 이 자습서에서는 Id API를 사용 하 여 사용자 및 역할을 추가 하는 방법을 보여 줍니다.
- [https://github.com/rustd/AspnetIdentitySample](https://github.com/rustd/AspnetIdentitySample)  
 기본 역할 및 사용자 지원을 추가 하는 방법과 역할 및 사용자 관리를 수행 하는 방법을 보여 주는 샘플 응용 프로그램입니다.
