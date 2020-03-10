---
uid: identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity
title: 계정 확인 & 암호 복구-ASP.NET Identity (C#)-ASP.NET 4.x
author: HaoK
description: 이 자습서를 수행 하기 전에 먼저 로그인, 전자 메일 확인 및 암호 재설정을 사용 하 여 보안 ASP.NET MVC 5 웹 앱 만들기를 완료 해야 합니다. 이 자습서 ...
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 8d54180d-f826-4df7-b503-7debf5ed9fb3
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 4b2c88280df39aa81d60f9508910e8fe5d6db6b8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499985"
---
# <a name="account-confirmation-and-password-recovery-with-aspnet-identity-c"></a>ASP.NET Identity (C#)를 사용 하 여 계정 확인 및 암호 복구

> 이 자습서를 수행 하기 전에 먼저 [로그인, 전자 메일 확인 및 암호 재설정을 사용 하 여 보안 ASP.NET MVC 5 웹 앱 만들기를](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)완료 해야 합니다. 이 자습서에는 자세한 내용이 포함 되어 있으며 로컬 계정 확인을 위한 전자 메일을 설정 하 고 사용자가 ASP.NET Identity에서 잊어버린 암호를 재설정할 수 있도록 허용 하는 방법을 보여 줍니다.

로컬 사용자 계정을 사용 하려면 사용자가 계정에 대 한 암호를 만들어야 하 고 해당 암호가 웹 앱에 안전 하 게 저장 됩니다. 또한 ASP.NET Identity는 사용자가 앱에 대 한 암호를 만들 필요가 없는 소셜 계정도 지원 합니다. [소셜 계정은](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) Google, Twitter, Facebook, Microsoft 등의 타사를 사용 하 여 사용자를 인증 합니다. 이 항목에서는 다음에 대해 설명합니다.

- [ASP.NET MVC 앱을 만들고](#createMvc) ASP.NET Identity 기능을 탐색 합니다.
- [Identity 샘플 빌드](#build)
- [전자 메일 확인 설정](#email)

새 사용자가 로컬 계정을 만드는 전자 메일 별칭을 등록 합니다.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image1.png)

등록 단추를 선택 하면 유효성 검사 토큰이 포함 된 확인 전자 메일을 전자 메일 주소로 보냅니다.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image2.png)

계정에 대 한 확인 토큰이 포함 된 전자 메일을 사용자에 게 보냅니다.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image3.png)

링크를 선택 하면 계정이 확인 됩니다.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image4.png)

<a id="passwordReset"></a>

## <a name="password-recoveryreset"></a>암호 복구/다시 설정

암호를 잊은 로컬 사용자는 자신의 전자 메일 계정으로 전송 되는 보안 토큰을 사용 하 여 암호를 재설정할 수 있습니다.  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image5.png)  
  
사용자는 곧 암호를 재설정할 수 있는 링크를 포함 하는 전자 메일을 받게 됩니다.  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image6.png)  
링크를 선택 하면 다시 설정 페이지로 이동 합니다.  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image7.png)  
  
**다시 설정** 단추를 선택 하면 암호가 다시 설정 된 것을 확인 합니다.  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image8.png)

<a id="createMvc"></a>

## <a name="create-an-aspnet-web-app"></a>ASP.NET 웹앱 만들기

[Visual Studio 2017](https://visualstudio.microsoft.com/)을 설치 하 고 실행 하 여 시작 합니다.

1. 새 ASP.NET 웹 프로젝트를 만들고 MVC 템플릿을 선택 합니다. Web Forms는 ASP.NET Identity도 지원 하므로 web Forms 앱에서 유사한 단계를 따를 수 있습니다.
2. **개별 사용자 계정**에 대 한 인증을 변경 합니다.
3. 앱을 실행 하 고, **등록** 링크를 선택 하 고, 사용자를 등록 합니다. 이때 전자 메일에 대 한 유일한 유효성 검사는 [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) 특성을 사용 하는 것입니다.
4. 서버 탐색기에서 **데이터 Connections\DefaultConnection\Tables\AspNetUsers**로 이동 하 고 마우스 오른쪽 단추를 클릭 한 다음 **테이블 정의 열기**를 선택 합니다.

    다음 이미지는 `AspNetUsers` 스키마를 보여 줍니다.

    ![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image9.png)
5. **AspNetUsers** 테이블을 마우스 오른쪽 단추로 클릭 하 고 **테이블 데이터 표시**를 선택 합니다.  
  
    ![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image10.png)  
  
   이 시점에서 전자 메일이 확인 되지 않았습니다.

ASP.NET Identity에 대 한 기본 데이터 저장소는 Entity Framework 있지만 다른 데이터 저장소를 사용 하 고 추가 필드를 추가 하도록 구성할 수 있습니다. 이 자습서의 끝부분에 있는 [추가 리소스](#addRes) 섹션을 참조 하세요.

[OWIN startup 클래스](../../../aspnet/overview/owin-and-katana/owin-startup-class-detection.md) ( *Startup.cs* )는 앱이 시작 되 고 OWIN 파이프라인을 구성 하 고 ASP.NET Identity를 초기화 하는 *앱\_Start\Startup.Auth.cs*에서 `ConfigureAuth` 메서드를 호출할 때 호출 됩니다. `ConfigureAuth` 메서드를 검사합니다. 각 `CreatePerOwinContext` 호출은 지정 된 형식의 인스턴스를 만들기 위해 요청 마다 한 번씩 호출 되는 콜백 (`OwinContext`에 저장 됨)을 등록 합니다. 생성자와 각 형식 (`ApplicationDbContext, ApplicationUserManager`)의 `Create` 메서드에서 중단점을 설정 하 고 각 요청에서 호출 되는지 확인할 수 있습니다. `ApplicationDbContext` 및 `ApplicationUserManager` 인스턴스는 응용 프로그램 전체에서 액세스할 수 있는 OWIN 컨텍스트에 저장 됩니다. 쿠키 미들웨어를 통해 OWIN 파이프라인에 후크를 ASP.NET Identity 합니다. 자세한 내용은 [ASP.NET Identity에서 UserManager 클래스에 대 한 요청당 요청 수명 관리](https://blogs.msdn.com/b/webdev/archive/2014/02/12/per-request-lifetime-management-for-usermanager-class-in-asp-net-identity.aspx)를 참조 하세요.

보안 프로필을 변경 하면 새 보안 스탬프가 생성 되어 *AspNetUsers* 테이블의 `SecurityStamp` 필드에 저장 됩니다. `SecurityStamp` 필드는 보안 쿠키와 다릅니다. 보안 쿠키는 `AspNetUsers` 테이블 (또는 Identity DB의 다른 위치)에 저장 되지 않습니다. 보안 쿠키 토큰은 [DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx) 를 사용 하 여 자체 서명 되며 `UserId, SecurityStamp` 및 만료 시간 정보를 사용 하 여 생성 됩니다.

쿠키 미들웨어는 각 요청에서 쿠키를 확인 합니다. `Startup` 클래스의 `SecurityStampValidator` 메서드는 DB에 적중 하 고 `validateInterval`에 지정 된 대로 주기적으로 보안 스탬프를 확인 합니다. 이는 보안 프로필을 변경 하지 않는 한 30 분 마다 (이 샘플에서) 발생 합니다. 데이터베이스에 대 한 왕복을 최소화 하기 위해 30 분 간격을 선택 했습니다. 자세한 내용은 제 [2 단계 인증 자습서](index.md) 를 참조 하세요.

코드의 설명에 따라 `UseCookieAuthentication` 메서드는 쿠키 인증을 지원 합니다. `SecurityStamp` 필드 및 연결 된 코드는 앱에 대 한 추가 보안 계층을 제공 합니다. 암호를 변경 하면 로그인 한 브라우저에서 로그 아웃 됩니다. `SecurityStampValidator.OnValidateIdentity` 메서드를 사용 하면 사용자가 로그인 할 때 앱이 보안 토큰의 유효성을 검사할 수 있습니다 .이는 암호를 변경 하거나 외부 로그인을 사용할 때 사용 됩니다. 이는 이전 암호를 사용 하 여 생성 된 모든 토큰 (쿠키)이 무효화 되도록 하기 위해 필요 합니다. 샘플 프로젝트에서 사용자 암호를 변경 하는 경우 사용자에 대 한 새 토큰이 생성 되 고, 이전 토큰은 무효화 되 고 `SecurityStamp` 필드가 업데이트 됩니다.

Id 시스템을 사용 하면 사용자 보안 프로필이 변경 될 때 (예: Facebook, Google, Microsoft 계정 등에서와 같이 사용자가 암호를 변경 하거나 연결 된 로그인을 변경 하는 경우) 사용자가 앱을 구성할 수 있습니다. 브라우저 인스턴스. 예를 들어 아래 이미지는 단일 단추를 선택 하 여 사용자가 모든 브라우저 인스턴스 (이 경우에는 IE, Firefox 및 Chrome)에서 로그 아웃할 수 있도록 하는 [단일 signout 샘플](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SingleSignOutSample) 앱을 보여 줍니다. 또는 샘플을 사용 하면 특정 브라우저 인스턴스에서만 로그 아웃할 수 있습니다.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image11.png)

[단일 signout 샘플](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SingleSignOutSample) 앱은 ASP.NET Identity를 사용 하 여 보안 토큰을 다시 생성 하는 방법을 보여 줍니다. 이는 이전 암호를 사용 하 여 생성 된 모든 토큰 (쿠키)이 무효화 되도록 하기 위해 필요 합니다. 이 기능은 응용 프로그램에 대 한 추가 보안 계층을 제공 합니다. 암호를 변경 하면이 응용 프로그램에 로그인 한 사용자가 로그 아웃 됩니다.

*앱\_Start\IdentityConfig.cs* 파일은 `ApplicationUserManager`, `EmailService` 및 `SmsService` 클래스를 포함 합니다. `EmailService` 및 `SmsService` 클래스는 각각 `IIdentityMessageService` 인터페이스를 구현 하므로 각 클래스에 전자 메일 및 SMS를 구성 하는 공통 메서드가 있습니다. 이 자습서에서는 [SendGrid](http://sendgrid.com/)를 통해 전자 메일 알림을 추가 하는 방법만 보여 주지만 SMTP 및 기타 메커니즘을 사용 하 여 전자 메일을 보낼 수 있습니다.

`Startup` 클래스에는 소셜 로그인 (Facebook, Twitter 등)을 추가 하는 상용구 강판도 포함 되어 있습니다. 자세한 내용은 [facebook, twitter, LinkedIn 및 Google OAuth2 sign-on을 사용 하는 자습서 MVC 5 앱](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 을 참조 하세요.

사용자 id 정보를 포함 하는 `ApplicationUserManager` 클래스를 검토 하 고 다음 기능을 구성 합니다.

- 암호 수준 요구 사항.
- 사용자 잠금 (시도 및 시간)입니다.
- 2 단계 인증 (2FA). 다른 자습서에서 2FA와 SMS에 대해 살펴보겠습니다.
- 전자 메일 및 SMS 서비스를 연결 합니다. (다른 자습서에서 SMS를 다루겠습니다.)

`ApplicationUserManager` 클래스는 제네릭 `UserManager<ApplicationUser>` 클래스에서 파생 됩니다. `ApplicationUser`는 [IdentityUser](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework.identityuser.aspx)에서 파생 됩니다. `IdentityUser` 제네릭 `IdentityUser` 클래스에서 파생 됩니다.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample1.cs)]

위의 속성은 위에 표시 된 `AspNetUsers` 테이블의 속성과 일치 합니다.

`IUser`의 제네릭 인수를 사용 하면 기본 키에 대해 서로 다른 형식을 사용 하 여 클래스를 파생할 수 있습니다. 기본 키를 문자열에서 int 또는 GUID로 변경 하는 방법을 보여 주는 [ChangePK](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/ChangePK) 샘플을 참조 하세요.

### <a name="applicationuser"></a>ApplicationUser

`ApplicationUser` (`public class ApplicationUserManager : UserManager<ApplicationUser>`)는 *Models\IdentityModels.cs* 에서 다음과 같이 정의 됩니다.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample2.cs?highlight=8-9)]

위의 강조 표시 된 코드는 [ClaimsIdentity](https://msdn.microsoft.com/library/system.security.claims.claimsidentity.aspx)을 생성 합니다. ASP.NET Identity 및 OWIN 쿠키 인증은 클레임 기반 이므로 프레임 워크에서 사용자에 대 한 `ClaimsIdentity`을 생성 해야 합니다. `ClaimsIdentity`에는 사용자의 이름, 사용 기간 및 사용자가 속한 역할 등 사용자에 대 한 모든 클레임에 대 한 정보가 있습니다. 이 단계에서 사용자에 게 더 많은 클레임을 추가할 수도 있습니다.

OWIN `AuthenticationManager.SignIn` 메서드는 `ClaimsIdentity`를 전달 하 고 사용자를 로그인 합니다.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample3.cs?highlight=4-6)]

[Facebook, Twitter, LinkedIn 및 Google OAuth2 sign-on이 포함 된 MVC 5 앱](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 은 `ApplicationUser` 클래스에 속성을 추가 하는 방법을 보여 줍니다.

## <a name="email-confirmation"></a>전자 메일 확인

새 사용자가 등록 하는 전자 메일을 확인 하 여 다른 사용자를 가장 하지 않았는지 확인 하는 것이 좋습니다. 즉, 다른 사용자의 전자 메일을 사용 하 여 등록 하지 않았습니다. 토론 포럼이 있다고 가정 하면 `"bob@example.com"` `"joe@contoso.com"`등록 하지 않도록 합니다. 전자 메일 확인 없이 앱에서 원치 않는 전자 메일을 받을 수 `"joe@contoso.com"`. Bob이 실수로 `"bib@example.com"`로 등록 했다고 가정 하면 앱이 올바른 전자 메일을가지고 있지 않기 때문에 암호 복구를 사용할 수 없습니다. 전자 메일 확인은 봇의 제한 된 보호만 제공 하며, 결정 된 스팸 메일을 보호 하는 것을 제공 하지 않으며 등록 하는 데 사용할 수 있는 많은 작업 메일 별칭이 있습니다. 아래 샘플에서 사용자는 계정이 확인 된 후 (에 등록 된 전자 메일 계정에서 받은 확인 링크를 선택 하 여) 암호를 변경할 수 없습니다. 이 작업 흐름을 다른 시나리오에 적용할 수 있습니다. 예를 들어 관리자가 만든 새 계정에 대 한 암호를 확인 하 고 다시 설정 하기 위해 링크를 전송 하 여 프로필을 변경할 때 사용자에 게 전자 메일을 보낼 수 있습니다. 일반적으로 새 사용자가 전자 메일, SMS 문자 메시지 또는 다른 메커니즘을 통해 확인 되기 전에 데이터를 웹 사이트에 게시 하는 것을 방지 하려고 합니다. <a id="build"></a>

## <a name="build-a-more-complete-sample"></a>더 완전 한 샘플 빌드

이 섹션에서는 NuGet을 사용 하 여에서 사용할 수 있는 전체 샘플을 다운로드 합니다.

1. ***빈*** ASP.NET 웹 프로젝트를 새로 만듭니다.
2. 패키지 관리자 콘솔에서 다음 명령을 입력 합니다. 

    [!code-console[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample4.cmd)]

   이 자습서에서는 [SendGrid](http://sendgrid.com/) 를 사용 하 여 전자 메일을 보냅니다. `Identity.Samples` 패키지는 작업할 코드를 설치 합니다.
3. [SSL을 사용 하도록 프로젝트](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)를 설정 합니다.
4. 앱을 실행 하 고 **등록** 링크를 선택 하 고 등록 양식을 게시 하 여 로컬 계정 만들기를 테스트 합니다.
5. 전자 메일 확인을 시뮬레이트하는 데모 전자 메일 링크를 선택 합니다.
6. 샘플 (계정 컨트롤러의 `ViewBag.Link` 코드에서 데모 전자 메일 링크 확인 코드를 제거 합니다. `DisplayEmail` 및 `ForgotPasswordConfirmation` 작업 메서드 및 razor 뷰)를 참조 하세요.

> [!WARNING]
> 이 샘플에서 보안 설정을 변경 하는 경우 생성 된 변경 내용을 명시적으로 호출 하는 보안 감사를 생성 해야 합니다.

## <a name="examine-the-code-in-app_startidentityconfigcs"></a>앱\_Start\IdentityConfig.cs에서 코드를 검사 합니다.

이 샘플에서는 계정을 만들어 *관리자* 역할에 추가 하는 방법을 보여 줍니다. 샘플의 전자 메일을 관리자 계정에 사용할 메일로 바꾸어야 합니다. 현재 관리자 계정을 만드는 가장 쉬운 방법은 `Seed` 메서드를 프로그래밍 방식으로 만드는 것입니다. 사용자 및 역할을 만들고 관리 하는 데 사용할 수 있는 도구를 나중에 제공 하고자 합니다. 예제 코드를 사용 하 여 사용자 및 역할을 만들고 관리할 수 있지만 역할 및 사용자 관리 페이지를 실행 하려면 먼저 관리자 계정이 있어야 합니다. 이 샘플에서는 DB가 시드 될 때 관리자 계정이 생성 됩니다.

암호를 변경 하 고 전자 메일 알림을 받을 수 있는 계정으로 이름을 변경 합니다.

> [!WARNING]
> 보안-중요 한 데이터를 소스 코드에 저장 하지 않습니다.

앞에서 설명한 것 처럼 startup 클래스의 `app.CreatePerOwinContext` 호출은 앱 DB 콘텐츠, 사용자 관리자 및 역할 관리자 클래스의 `Create` 메서드에 콜백을 추가 합니다. OWIN 파이프라인은 각 요청에 대해 이러한 클래스에 대 한 `Create` 메서드를 호출 하 고 각 클래스에 대 한 컨텍스트를 저장 합니다. 계정 컨트롤러는 OWIN 컨텍스트를 포함 하는 HTTP 컨텍스트에서 사용자 관리자를 노출 합니다.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample5.cs)]

사용자가 로컬 계정을 등록 하면 `HTTP Post Register` 메서드가 호출 됩니다.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample6.cs)]

위의 코드는 모델 데이터를 사용 하 여 입력 한 전자 메일 및 암호를 사용 하 여 새 사용자 계정을 만듭니다. 전자 메일 별칭이 데이터 저장소에 있으면 계정 만들기가 실패 하 고 양식이 다시 표시 됩니다. `GenerateEmailConfirmationTokenAsync` 메서드는 보안 확인 토큰을 만들어 ASP.NET Identity 데이터 저장소에 저장 합니다. [Url. Action](https://msdn.microsoft.com/library/dd505232(v=vs.118).aspx) 메서드는 `UserId` 및 확인 토큰을 포함 하는 링크를 만듭니다. 그런 다음이 링크를 사용자에 게 메일로 보낼 수 있습니다. 사용자는 자신의 메일 앱에서 링크를 선택 하 여 계정을 확인할 수 있습니다.

<a id="email"></a>

## <a name="set-up-email-confirmation"></a>전자 메일 확인 설정

[Azure SendGrid 등록 페이지로](https://azure.microsoft.com/gallery/store/sendgrid/sendgrid-azure/) 이동 하 여 무료 계정에 등록 합니다. SendGrid를 구성 하기 위해 다음과 유사한 코드를 추가 합니다.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample7.cs?highlight=5)]

> [!NOTE]
> 전자 메일 클라이언트는 텍스트 메시지 (HTML 없음)만 허용 하는 경우가 많습니다. 텍스트와 HTML로 메시지를 제공 해야 합니다. 위의 SendGrid 샘플에서이 작업은 위에 표시 된 `myMessage.Text` 및 `myMessage.Html` 코드를 사용 하 여 수행 됩니다.

다음 코드는 `message.Body` 링크만 반환 하는 [send-mailmessage](https://msdn.microsoft.com/library/system.net.mail.mailmessage.aspx) 클래스를 사용 하 여 전자 메일을 보내는 방법을 보여 줍니다.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample8.cs)]

> [!WARNING]
> 보안-중요 한 데이터를 소스 코드에 저장 하지 않습니다. 계정 및 자격 증명은 appSetting에 저장 됩니다. Azure에서 Azure Portal의 **[구성](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** 탭에서 이러한 값을 안전 하 게 저장할 수 있습니다. [암호 및 기타 중요 한 데이터를 ASP.NET 및 Azure에 배포 하는 방법에 대 한 모범 사례](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)를 참조 하세요.

SendGrid 자격 증명을 입력 하 고, 앱을 실행 하 고, 전자 메일 별칭을 사용 하 여 등록 하면 전자 메일의 확인 링크를 선택할 수 있습니다. [Outlook.com](http://outlook.com) 메일 계정으로이 작업을 수행 하는 방법을 보려면 [ C# Outlook.Com smtp 호스트에 대 한](http://typecastexception.com/post/2013/12/20/C-SMTP-Configuration-for-OutlookCom-SMTP-Host.aspx) John atten의 smtp 구성 및[ASP.NET Identity 2.0: 계정 유효성 검사 및 2 단계 권한 부여 게시물 설정](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) 을 참조 하세요.

사용자가 **등록** 단추를 선택 하면 유효성 검사 토큰이 포함 된 확인 전자 메일이 전자 메일 주소로 전송 됩니다.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image12.png)

계정에 대 한 확인 토큰이 포함 된 전자 메일을 사용자에 게 보냅니다.

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image13.png)

## <a name="examine-the-code"></a>코드 검사

다음 코드는 `POST ForgotPassword` 메서드를 보여 줍니다.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample9.cs)]

사용자 전자 메일이 확인 되지 않은 경우 메서드가 자동으로 실패 합니다. 잘못 된 전자 메일 주소에 대해 오류가 게시 된 경우 악의적인 사용자가 해당 정보를 사용 하 여 공격을 위해 유효한 userId (전자 메일 별칭)를 찾을 수 있습니다.

다음 코드에서는 사용자가 전송 된 전자 메일의 확인 링크를 선택할 때 호출 되는 계정 컨트롤러의 `ConfirmEmail` 메서드를 보여 줍니다.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample10.cs)]

잊어버린 암호 토큰을 사용 하면 무효화 됩니다. `Create` 메서드의 다음 코드 변경 ( *앱\_Start\IdentityConfig.cs* 파일)은 3 시간 후에 만료 되도록 토큰을 설정 합니다.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample11.cs?highlight=6-8)]

위의 코드를 사용 하 여 잊어버린 암호와 전자 메일 확인 토큰은 3 시간 후에 만료 됩니다. 기본 `TokenLifespan`는 1 일입니다.

다음 코드에서는 전자 메일 확인 방법을 보여 줍니다.

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample12.cs)]

 앱을 더 안전 하 게 만들기 위해 ASP.NET Identity 2 단계 인증 (2FA)을 지원 합니다. ASP.NET Identity 2.0: John Atten에서 [계정 유효성 검사 및 2 단계 권한 부여 설정](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) 을 참조 하세요. 로그인 암호 시도 실패 시 계정 잠금을 설정할 수 있지만이 방법을 사용 하면 로그인이 [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) 잠금에 취약 해질 수 있습니다. 2FA와만 계정 잠금을 사용 하는 것이 좋습니다.  
<a id="addRes"></a>

## <a name="additional-resources"></a>추가 리소스

- [ASP.NET ID에 대한 사용자 지정 스토리지 공급자 개요](../extensibility/overview-of-custom-storage-providers-for-aspnet-identity.md)
- [Facebook, Twitter, LinkedIn 및 Google OAuth2 sign-on이 포함 된 MVC 5 앱](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 은 사용자 테이블에 프로필 정보를 추가 하는 방법을 보여 줍니다.
- [ASP.NET MVC 및 id 2.0: John Atten의 기본 사항을 이해](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx) 합니다.
- [ASP.NET ID 소개](../getting-started/introduction-to-aspnet-identity.md)
- Pranav Rastogi가 [ASP.NET Identity 2.0.0의 RTM을 발표](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) 합니다.
