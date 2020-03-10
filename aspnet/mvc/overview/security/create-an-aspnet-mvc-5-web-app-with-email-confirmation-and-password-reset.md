---
uid: mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
title: 로그인, 전자 메일 확인 및 암호 재설정 (C#)을 사용 하 여 보안 ASP.NET MVC 5 웹 앱 만들기 Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 ASP.NET Identity 멤버 자격 시스템을 사용 하 여 전자 메일 확인 및 암호 재설정으로 ASP.NET MVC 5 웹 앱을 빌드하는 방법을 보여 줍니다. Ca ...
ms.author: riande
ms.date: 03/26/2015
ms.assetid: d4911cb3-1afb-4805-b860-10818c4b1280
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
msc.type: authoredcontent
ms.openlocfilehash: 6169c972ad0f4ee2079d3638c54a5accc4b8b3de
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78432737"
---
# <a name="create-a-secure-aspnet-mvc-5-web-app-with-log-in-email-confirmation-and-password-reset-c"></a>로그인, 전자 메일 확인 및 암호 재설정 기능이 있는 보안 ASP.NET MVC 5 웹앱 만들기(C#)

[Rick Anderson](https://twitter.com/RickAndMSFT)

이 자습서에서는 ASP.NET Identity 멤버 자격 시스템을 사용 하 여 전자 메일 확인 및 암호 재설정으로 ASP.NET MVC 5 웹 앱을 빌드하는 방법을 보여 줍니다.

.NET Core를 사용 하는이 자습서의 업데이트 된 버전은 [ASP.NET Core의 계정 확인 및 암호 복구](/aspnet/core/security/authentication/accconfirm)를 참조 하세요.

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a>ASP.NET MVC 앱 만들기

웹 또는 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) [에 대해 Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 을 설치 하 고 실행 하 여 시작 합니다. [Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 이상을 설치 합니다.

> [!NOTE]
> 경고:이 자습서를 완료 하려면 [Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 이상을 설치 해야 합니다.

1. 새 ASP.NET 웹 프로젝트를 만들고 MVC 템플릿을 선택 합니다. Web Forms는 ASP.NET Identity도 지원 하므로 web Forms 앱에서 비슷한 단계를 따를 수 있습니다.  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image1.png)
2. 기본 인증을 **개별 사용자 계정**으로 그대로 둡니다. Azure에서 앱을 호스팅하려면 확인란을 선택 된 상태로 둡니다. 이 자습서의 뒷부분에서는 Azure에 배포 합니다. [Azure 계정을 무료로 열](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)수 있습니다.
3. [SSL을 사용 하도록 프로젝트](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)를 설정 합니다.
4. 앱을 실행 하 고 **등록** 링크를 클릭 한 다음 사용자를 등록 합니다. 이때 전자 메일에 대 한 유일한 유효성 검사는 [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) 특성을 사용 하는 것입니다.
5. 서버 탐색기에서 **데이터 Connections\DefaultConnection\Tables\AspNetUsers**로 이동 하 고 마우스 오른쪽 단추를 클릭 한 다음 **테이블 정의 열기**를 선택 합니다.

    다음 이미지는 `AspNetUsers` 스키마를 보여 줍니다.

    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image2.png)
6. **AspNetUsers** 테이블을 마우스 오른쪽 단추로 클릭 하 고 **테이블 데이터 표시**를 선택 합니다.  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image3.png)  
 이 시점에서 전자 메일이 확인 되지 않았습니다.
7. 행을 클릭 하 고 삭제를 선택 합니다. 다음 단계에서이 전자 메일을 다시 추가 하 고 확인 전자 메일을 보냅니다.

## <a name="email-confirmation"></a>전자 메일 확인

새 사용자 등록의 전자 메일을 확인 하 여 다른 사용자를 가장 하지 않았는지 확인 하는 것이 좋습니다. 즉, 다른 사용자의 전자 메일을 사용 하 여 등록 하지 않았습니다. 토론 포럼이 있다고 가정 하면 `"bob@example.com"` `"joe@contoso.com"`등록 하지 않도록 합니다. 전자 메일 확인 없이 앱에서 원치 않는 전자 메일을 받을 수 `"joe@contoso.com"`. Bob이 실수로 `"bib@example.com"`로 등록 했다고 가정 하면 앱이 올바른 전자 메일을가지고 있지 않기 때문에 암호 복구를 사용할 수 없습니다. 전자 메일 확인은 봇의 제한 된 보호만 제공 하며, 결정 된 스팸 메일을 보호 하는 것을 제공 하지 않으며 등록 하는 데 사용할 수 있는 많은 작업 메일 별칭이 있습니다.

일반적으로 새 사용자가 전자 메일, SMS 문자 메시지 또는 다른 메커니즘을 통해 확인 되기 전에 데이터를 웹 사이트에 게시 하는 것을 방지 하려고 합니다. <a id="build"></a>아래 섹션에서는 전자 메일 확인을 사용 하도록 설정 하 고 코드를 수정 하 여 새로 등록 된 사용자가 전자 메일을 확인 한 후에 로그인 하지 않도록 합니다.

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a>SendGrid 후크

이 섹션의 지침은 최신이 아닙니다. 업데이트 된 지침은 [SendGrid 전자 메일 공급자 구성](/aspnet/core/security/authentication/accconfirm#configure-email-provider) 을 참조 하세요.

이 자습서에서는 [SendGrid](http://sendgrid.com/)를 통해 전자 메일 알림을 추가 하는 방법을 보여 주지만 SMTP 및 기타 메커니즘을 사용 하 여 전자 메일을 보낼 수 있습니다 ( [추가 리소스](#addRes)참조).

1. 패키지 관리자 콘솔에서 다음 명령을 입력합니다. 

    [!code-console[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample1.cmd)]
2. [Azure SendGrid 등록 페이지로](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409) 이동 하 여 무료 SendGrid 계정에 등록 합니다. *App_Start/identityconfig.cs*에서 다음과 비슷한 코드를 추가 하 여 SendGrid를 구성 합니다.

    [!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample2.cs?highlight=3,5)]

다음 포함을 추가 해야 합니다.

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample3.cs)]

이 샘플을 간단 하 게 유지 하기 위해 web.config 파일에 응용 프로그램 설정을 *저장 합니다.*

[!code-xml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample4.xml)]

> [!WARNING]
> 보안-중요 한 데이터를 소스 코드에 저장 하지 않습니다. 계정 및 자격 증명은 appSetting에 저장 됩니다. Azure에서 Azure Portal의 **[구성](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** 탭에서 이러한 값을 안전 하 게 저장할 수 있습니다. [암호 및 기타 중요 한 데이터를 ASP.NET 및 Azure에 배포 하는 방법에 대 한 모범 사례](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)를 참조 하세요.

### <a name="enable-email-confirmation-in-the-account-controller"></a>계정 컨트롤러에서 전자 메일 확인 사용

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample5.cs?highlight=16-21)]

*Views\Account\ConfirmEmail.cshtml* 파일에 올바른 razor 구문이 있는지 확인 합니다. 첫 번째 줄의 @ 문자가 없을 수도 있습니다. )

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample6.cshtml?highlight=1)]

앱을 실행 하 고 등록 링크를 클릭 합니다. 등록 양식을 제출 하면 로그인 됩니다.

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image4.png)

전자 메일 계정을 확인 하 고 링크를 클릭 하 여 전자 메일을 확인 합니다.

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a>로그인 하기 전에 전자 메일 확인 필요

현재 사용자가 등록 양식을 완료 하면 로그인 됩니다. 일반적으로에 로그인 하기 전에 전자 메일을 확인 하려고 합니다. 아래 섹션에는 새 사용자가 로그인 (인증 됨) 전에 확인 된 전자 메일을 포함 하도록 코드를 수정 합니다. `HttpPost Register` 메서드를 다음과 같이 강조 표시 된 변경 내용으로 업데이트 합니다.

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample7.cs?highlight=14-15,23-30)]

`SignInAsync` 메서드를 주석으로 처리 하면 등록을 통해 사용자에 게 로그인 되지 않습니다. `TempData["ViewBagLink"] = callbackUrl;` 줄을 사용 하 여 전자 메일을 보내지 않고 [앱을 디버깅](#dbg) 하 고 등록을 테스트할 수 있습니다. `ViewBag.Message`은 확인 지침을 표시 하는 데 사용 됩니다. [다운로드 샘플](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952) 에는 전자 메일을 설정 하지 않고 전자 메일 확인을 테스트 하는 코드가 포함 되어 있으며,이를 사용 하 여 응용 프로그램을 디버그할 수도 있습니다.

`Views\Shared\Info.cshtml` 파일을 만들고 다음 razor 태그를 추가 합니다.

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample8.cshtml)]

Home 컨트롤러의 `Contact` 작업 메서드에 [권한 부여 특성](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx) 을 추가 합니다. **연락처** 링크를 클릭 하 여 익명 사용자에 게 액세스 권한이 없고 인증 된 사용자에 게 액세스 권한이 있는지 확인할 수 있습니다.

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample9.cs?highlight=1)]

또한 `HttpPost Login` 작업 메서드를 업데이트 해야 합니다.

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample10.cs?highlight=13-22)]

*Views\Shared\Error.cshtml* 보기를 업데이트 하 여 오류 메시지를 표시 합니다.

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample11.cshtml?highlight=8-17)]

**AspNetUsers** 테이블에서 테스트 하려는 전자 메일 별칭이 포함 된 모든 계정을 삭제 합니다. 앱을 실행 하 고 전자 메일 주소를 확인 한 후에만 로그인 할 수 있는지 확인 합니다. 전자 메일 주소를 확인 한 후 **연락처** 링크를 클릭 합니다.

<a id="reset"></a>
## <a name="password-recoveryreset"></a>암호 복구/다시 설정

계정 컨트롤러의 `HttpPost ForgotPassword` 동작 메서드에서 주석 문자를 제거 합니다.

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample12.cs?highlight=17-20)]

*Views\Account\Login.cshtml* razor 뷰 파일 [의 `ForgotPassword`/에서 주석](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx) 문자를 제거 합니다.

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample13.cshtml?highlight=47-50)]

이제 로그인 페이지에 암호를 다시 설정 하는 링크가 표시 됩니다.

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a>전자 메일 다시 보내기 확인 링크

사용자가 새 로컬 계정을 만들면 로그온 하기 전에 사용 해야 하는 확인 링크를 전자 메일로 보낼 수 있습니다. 사용자가 실수로 확인 전자 메일을 삭제 하거나 전자 메일이 도착 하지 않은 경우 확인 링크를 다시 전송 해야 합니다. 다음 코드 변경 내용에서는이를 사용 하도록 설정 하는 방법을 보여 줍니다.

다음 도우미 메서드를 *Controllers\accountcontroller.cs* 파일의 아래쪽에 추가 합니다.

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample14.cs)]

새 도우미를 사용 하도록 Register 메서드를 업데이트 합니다.

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample15.cs?highlight=17)]

사용자 계정이 확인 되지 않은 경우 암호를 다시 보내도록 로그인 메서드를 업데이트 합니다.

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample16.cs?highlight=20)]

<a id="combine"></a>
## <a name="combine-social-and-local-login-accounts"></a>소셜 및 로컬 로그인 계정 결합

전자 메일 링크를 클릭 하 여 로컬 및 소셜 계정을 결합할 수 있습니다. 다음 시퀀스에서는 먼저 로컬 로그인으로 만들어진 **RickAndMSFT@gmail.com** 있지만 먼저 계정을 소셜 로그인으로 만든 다음 로컬 로그인을 추가할 수 있습니다.

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image5.png)

**관리** 링크를 클릭 합니다. **외부 로그인** 을 기록해 둡니다 .이 계정과 연결 된 0입니다.

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image6.png)

다른 로그인 서비스에 대 한 링크를 클릭 하 고 앱 요청을 수락 합니다. 두 계정을 결합 하 여 두 계정을 사용 하 여 로그온 할 수 있습니다. 인증 서비스의 소셜 로그인이 다운 되거나 소셜 계정에 대 한 액세스 권한이 손실 될 가능성이 있는 경우 사용자가 로컬 계정을 추가 하도록 할 수 있습니다.

다음 그림에서 Tom은 **외부 로그인** 에서 볼 수 있는 소셜 로그인입니다. 1은 페이지에 표시 됩니다.

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image7.png)

**암호 선택** 을 클릭 하면 동일한 계정에 연결 된 로컬 로그를 추가할 수 있습니다.

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image8.png)

## <a name="email-confirmation-in-more-depth"></a>더 깊이 있는 전자 메일 확인

[ASP.NET Identity를 사용 하 여 내 자습서 계정 확인 및 암호 복구](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) 는이 항목에 자세히 설명 되어 있습니다.

<a id="dbg"></a>
## <a name="debugging-the-app"></a>앱 디버깅

링크를 포함 하는 전자 메일을 받을 수 없는 경우:

- 정크 또는 스팸 폴더를 확인 합니다.
- SendGrid 계정에 로그인 하 고 [전자 메일 활동 링크](https://sendgrid.com/logs/index)를 클릭 합니다.

전자 메일 없이 확인 링크를 테스트 하려면 완료 된 [샘플](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)을 다운로드 합니다. 확인 링크와 확인 코드는 페이지에 표시 됩니다.

<a id="addRes"></a>
## <a name="additional-resources"></a>추가 리소스

- [ASP.NET Identity 권장 리소스에 대 한 링크](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [계정 확인 및 암호 복구 ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) 암호 복구 및 계정 확인에 대해 자세히 설명 합니다.
- [Facebook, Twitter, LinkedIn 및 Google OAuth2 sign-on을 사용한 MVC 5 앱](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 이 자습서에서는 Facebook 및 Google OAuth 2 권한 부여를 사용 하 여 ASP.NET MVC 5 앱을 작성 하는 방법을 보여 줍니다. 또한 Id 데이터베이스에 데이터를 추가 하는 방법을 보여 줍니다.
- [멤버 자격, OAuth 및 SQL Database를 사용 하 여 Azure에 보안 ASP.NET MVC 앱을 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다. 이 자습서에서는 Azure 배포, 역할을 사용 하 여 앱을 보호 하는 방법, 멤버 자격 API를 사용 하 여 사용자 및 역할을 추가 하는 방법 및 추가 보안 기능을 추가 합니다.
- [OAuth 2 용 Google 앱 만들기 및 프로젝트에 앱 연결](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [Facebook에서 앱 만들기 및 프로젝트에 앱 연결](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [프로젝트에서 SSL 설정](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
