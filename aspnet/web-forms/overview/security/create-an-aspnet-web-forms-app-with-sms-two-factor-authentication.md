---
uid: web-forms/overview/security/create-an-aspnet-web-forms-app-with-sms-two-factor-authentication
title: SMS 2 단계 인증을 사용 하 여 ASP.NET Web Forms 앱 만들기C#() | Microsoft Docs
author: Erikre
description: 이 자습서에서는 2 단계 인증을 사용 하 여 ASP.NET Web Forms 앱을 빌드하는 방법을 보여 줍니다. 이 자습서는 Cr ... 라는 자습서를 보완 하기 위해 설계 되었습니다.
ms.author: riande
ms.date: 10/09/2014
ms.assetid: 716264ae-ab72-45de-bfc5-53a6237089cf
msc.legacyurl: /web-forms/overview/security/create-an-aspnet-web-forms-app-with-sms-two-factor-authentication
msc.type: authoredcontent
ms.openlocfilehash: c9558aca8a655071c0c94ed66433cf721f26c011
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78455981"
---
# <a name="create-an-aspnet-web-forms-app-with-sms-two-factor-authentication-c"></a>SMS 2단계 인증을 사용하는 ASP.NET Web Forms 앱 만들기(C#)

[Erik Reitan](https://github.com/Erikre)

[전자 메일 및 SMS 2 단계 인증을 사용 하 여 ASP.NET Web Forms 앱 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-Forms-App-with-5a0ff94e)

> 이 자습서에서는 2 단계 인증을 사용 하 여 ASP.NET Web Forms 앱을 빌드하는 방법을 보여 줍니다. 이 자습서는 [사용자 등록, 전자 메일 확인 및 암호 재설정을 사용 하 여 보안 ASP.NET Web Forms 앱 만들기](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md)라는 자습서를 보완 하기 위해 설계 되었습니다. 또한이 자습서는 Rick Anderson의 [MVC 자습서](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)를 기반으로 합니다.

## <a name="introduction"></a>소개

이 자습서에서는 Visual Studio를 사용 하 여 2 단계 인증을 지 원하는 ASP.NET Web Forms 응용 프로그램을 만드는 데 필요한 단계를 안내 합니다. 2 단계 인증은 추가 사용자 인증 단계입니다. 이 추가 단계에서는 로그인 중에 고유한 개인 식별 번호 (PIN)를 생성 합니다. PIN은 일반적으로 사용자에 게 전자 메일 또는 SMS 메시지로 전송 됩니다. 그러면 앱의 사용자가 로그인 할 때 추가 인증 조치로 PIN을 입력 합니다.

### <a name="tutorial-tasks-and-information"></a>자습서 작업 및 정보:

- [ASP.NET Web Forms 앱 만들기](#createWebForms)
- [SMS 및 2 단계 인증 설정](#SMS)
- [등록 된 사용자에 대해 2 단계 인증 사용](#use2FA)
- [추가 리소스](#addRes)

<a id="createWebForms"></a>
## <a name="create-an-aspnet-web-forms-app"></a>ASP.NET Web Forms 앱 만들기

웹 또는 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) [에 대해 Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 을 설치 하 고 실행 하 여 시작 합니다. [업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 이상을 설치 Visual Studio 2013. 또한 아래에 설명 된 대로 [Twilio](https://www.twilio.com/try-twilio) 계정을 만들어야 합니다.

> [!NOTE]
> 중요:이 자습서를 완료 하려면 [Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 이상을 설치 해야 합니다.

1. 새 프로젝트 ( **새**프로젝트 &gt; -**파일** )를 만들고 **새 프로젝트** 대화 상자에서 .NET Framework 버전 4.5.2과 함께 **ASP.NET 웹 응용 프로그램** 템플릿을 선택 합니다.
2. **새 ASP.NET 프로젝트** 대화 상자에서 **Web Forms** 템플릿을 선택 합니다. 기본 인증을 **개별 사용자 계정**으로 그대로 둡니다. 그런 다음 **확인** 을 클릭 하 여 새 프로젝트를 만듭니다.  
    ![새 ASP.NET 프로젝트 대화 상자](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image1.png)
3. 프로젝트에 대해 SSL(Secure Sockets Layer) (SSL)을 사용 하도록 설정 합니다. [시작 Web Forms 자습서 시리즈](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)의 **프로젝트에 대해 SSL 사용** 섹션에서 사용할 수 있는 단계를 따릅니다.
4. Visual Studio에서 **패키지 관리자 콘솔** (**도구** -&gt; **NuGet 패키지** 관리자 -&gt; **패키지 관리자 콘솔**)을 열고 다음 명령을 입력 합니다.  
    `Install-Package Twilio`

<a id="SMS"></a>
## <a name="setup-sms-and-two-factor-authentication"></a>SMS 및 2 단계 인증 설정

이 자습서에서는 Twilio를 사용 하지만 모든 SMS 공급자를 사용할 수 있습니다.

1. [Twilio](https://www.twilio.com/try-twilio) 계정을 만듭니다.
2. Twilio 계정의 **대시보드** 탭에서 **계정 SID** 및 **인증 토큰** 을 복사 합니다. 나중에 앱에 추가 합니다.
3. **숫자** 탭에서 Twilio **전화 번호도** 함께 복사 합니다.
4. 앱에서 Twilio **계정 SID**, **인증 토큰** 및 **전화 번호** 를 사용할 수 있도록 설정 합니다. 작업을 간단 하 게 유지 하기 위해 web.config 파일에 이러한 값을 *저장 합니다.* Azure에 배포 하는 경우 웹 사이트 구성 탭의 **appSettings** 섹션에 값을 안전 하 게 저장할 수 있습니다. 또한 전화 번호를 추가할 때 번호만 사용 합니다.   
   SendGrid 자격 증명을 추가할 수도 있습니다. SendGrid는 전자 메일 알림 서비스입니다. SendGrid를 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 [사용자 등록, 전자 메일 확인 및 암호 재설정을 사용 하 여 보안 ASP.NET Web Forms 앱 만들기](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md) 자습서의 ' 후크 Up SendGrid ' 섹션을 참조 하세요.

    [!code-xml[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample1.xml?highlight=2,6-10)]

    > [!WARNING]
    > 보안-중요 한 데이터를 소스 코드에 저장 하지 않습니다. 이 예제에서 계정과 자격 증명은 *web.config 파일의* **appSettings** 섹션에 저장 됩니다. Azure에서 Azure Portal의 **[구성](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** 탭에서 이러한 값을 안전 하 게 저장할 수 있습니다. 관련 정보는 [ASP.NET 및 Azure에 암호 및 기타 중요 한 데이터를 배포 하기 위한 모범 사례](/aspnet/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure)Rick Anderson의 항목을 참조 하세요.
5. 다음 변경 내용을 노란색으로 강조 표시 하 여 *앱\_Start\IdentityConfig.cs* 파일에 `SmsService` 클래스를 구성 합니다. 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample2.cs?highlight=5-17)]
6. *IdentityConfig.cs* 파일의 시작 부분에 다음 `using` 문을 추가 합니다. 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample3.cs?highlight=1-4)]
7. 노란색으로 강조 표시 된 줄을 제거 하 여 *계정/관리 .aspx* 파일을 업데이트 합니다.  

    [!code-aspx[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample4.aspx?highlight=38,53,57-60,63,66,70,73)]
8. *Manage.aspx.cs* 의 `Page_Load` 처리기에서 노란색으로 강조 표시 된 코드 줄의 주석 처리를 제거 하 여 다음과 같이 표시 되도록 합니다. 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample5.cs?highlight=8)]
9. *TwoFactorAuthenticationSignIn.aspx.cs* *계정*/코드 숨김에서 노란색으로 강조 표시 된 다음 코드를 추가 하 여 `Page_Load` 처리기를 업데이트 합니다. 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample6.cs?highlight=3-4,13)]

   위의 코드를 변경 하면 인증 옵션을 포함 하는 "Providers" DropDownList이 첫 번째 값으로 다시 설정 되지 않습니다. 이렇게 하면 사용자가 첫 번째만이 아니라 인증할 때 사용할 모든 옵션을 성공적으로 선택할 수 있습니다.
10. **솔루션 탐색기**에서 default.aspx를 마우스 오른쪽 *단추로 클릭 하* 고 **시작 페이지로 설정**을 선택 합니다.
11. 앱을 테스트 하 여 먼저 앱을 빌드한 다음 (**Ctrl**+**Shift**+**B**), 앱을 실행 (**F5**) 하 고 **등록** 을 선택 하 여 새 사용자 계정을 만들거나 사용자 계정이 이미 등록 된 경우 **로그인** 을 선택 합니다.
12. 사용자가 로그인 한 후 탐색 모음에서 사용자 ID (전자 메일 주소)를 클릭 하 여 **계정 관리** 페이지 (.aspx)를 표시 합니다.  
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image2.png)
13. **계정 관리** 페이지에서 **전화 번호** 옆에 있는 **추가** 를 클릭 합니다.  
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image3.png)
14. 사용자가 SMS 메시지 (문자 메시지)를 받을 전화 번호를 추가 하 고 **제출** 단추를 클릭 합니다.   
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image4.png)  
    이 시점에서 앱은 *web.config* 의 자격 증명을 사용 하 여 Twilio에 연결 합니다. SMS 메시지 (문자 메시지)가 사용자 계정과 연결 된 휴대폰으로 전송 됩니다. Twilio 대시보드를 보면 Twilio 메시지가 전송 되었는지 확인할 수 있습니다.
15. 몇 초 후에 사용자 계정과 연결 된 휴대폰에서 확인 코드를 포함 하는 문자 메시지를 받게 됩니다. 확인 코드를 입력 하 고 **Submit**를 누릅니다.  
     ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image5.png)

<a id="use2FA"></a>
## <a name="enable-two-factor-authentication-for-a-registered-user"></a>등록 된 사용자에 대해 2 단계 인증 사용

이 시점에서 앱에 대해 2 단계 인증을 사용 하도록 설정 했습니다. 사용자가 2 단계 인증을 사용 하려면 UI를 사용 하 여 설정을 변경 하면 됩니다. 

1. 앱의 사용자는 탐색 모음에서 사용자 ID (전자 메일 별칭)를 클릭 하 여 **계정 관리** 페이지를 표시 함으로써 특정 계정에 대해 2 단계 인증을 사용 하도록 설정할 수 있습니다. 그런 다음 **사용** 링크를 클릭 하 여 계정에 대해 2 단계 인증을 사용 하도록 설정 합니다.![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image6.png)
2. 로그 오프 한 다음 다시 로그인 합니다. 전자 메일을 사용 하도록 설정한 경우 2 단계 인증에 대해 SMS 또는 전자 메일을 선택할 수 있습니다. 전자 메일을 사용 하도록 설정 하지 않은 경우 [사용자 등록, 전자 메일 확인 및 암호 재설정을 사용 하 여 보안 ASP.NET Web Forms 앱 만들기](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md)라는 자습서를 참조 하세요.![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image7.png)
3. SMS 또는 전자 메일에서 코드를 입력할 수 있는 경우 2 단계 인증 페이지가 표시 됩니다.![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image8.png)  
 **이 브라우저 저장** 확인란을 클릭 하면 상자를 선택한 브라우저와 장치를 사용할 때 2 단계 인증을 사용 하 여 로그인 할 필요가 없게 됩니다. 악의적인 사용자가 장치에 대 한 액세스 권한을 얻을 수 없는 한, 2 단계 인증을 사용 하도록 설정 하 고, **이 브라우저** 를 클릭 하면 신뢰할 수 없는 장치의 모든 액세스에 대해 강력한 2 단계 인증 보호를 유지 하면서 한 단계 암호 액세스를 편리 하 게 사용할 수 있습니다. 정기적으로 사용 하는 모든 개인 장치에서이 수행할 수 있습니다.

<a id="addRes"></a>
## <a name="additional-resources"></a>추가 리소스

- [ASP.NET ID와 SMS 및 전자 메일을 사용한 2단계 인증](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)
- [ASP.NET Identity 권장 리소스에 대 한 링크](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [멤버 자격, OAuth 및 SQL Database를 사용 하 여 Azure 웹 사이트에 보안 ASP.NET Web Forms 앱 배포](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)
- [ASP.NET Web Forms tutorial 시리즈-OAuth 2.0 공급자 추가](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#OAuthWebForms)
- [ASP.NET Web Forms tutorial 시리즈-프로젝트에 SSL 사용](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)
- [계정 확인 및 암호 복구 ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [Facebook에서 앱 만들기 및 프로젝트에 앱 연결](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
