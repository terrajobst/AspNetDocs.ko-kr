---
uid: mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication
title: SMS 및 전자 메일 2 단계 인증을 사용 하는 ASP.NET MVC 5 앱 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 2 단계 인증을 사용 하 여 ASP.NET MVC 5 웹 앱을 빌드하는 방법을 보여 줍니다. 다음을 사용 하 여 보안 ASP.NET MVC 5 웹 앱 만들기를 완료 해야 합니다.
ms.author: riande
ms.date: 08/20/2015
ms.assetid: f50a5cdb-c06a-46ed-aa14-fc5b049dc8dc
msc.legacyurl: /mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication
msc.type: authoredcontent
ms.openlocfilehash: c14149d802bfc0a227a839a2981dc3e8a3849c25
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457598"
---
# <a name="aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication"></a>SMS 및 전자 메일 2단계 인증을 사용하는 ASP.NET MVC 5 앱

[Rick Anderson](https://twitter.com/RickAndMSFT)

> 이 자습서에서는 2 단계 인증을 사용 하 여 ASP.NET MVC 5 웹 앱을 빌드하는 방법을 보여 줍니다. 계속 하기 전에 [로그인, 전자 메일 확인 및 암호 재설정을 사용 하 여 보안 ASP.NET MVC 5 웹 앱 만들기를](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) 완료 해야 합니다. [여기](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)에서 완성 된 응용 프로그램을 다운로드할 수 있습니다. 다운로드에는 전자 메일 또는 SMS 공급자를 설정 하지 않고도 전자 메일 확인 및 SMS를 테스트할 수 있는 디버깅 도우미가 포함 되어 있습니다.
> 
> 이 자습서는 [Rick Anderson](https://blogs.msdn.com/rickAndy) (Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) )에 의해 작성 되었습니다.

- [ASP.NET MVC 앱 만들기](#createMvc)
- [2 단계 인증을 위한 SMS 설정](#SMS)
- [2 단계 인증 사용](#enable2)
- [추가 리소스](#addRes)

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a>ASP.NET MVC 앱 만들기

웹 또는 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) [에 대해 Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 을 설치 하 고 실행 하 여 시작 합니다. [Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 이상을 설치 합니다.

> [!NOTE]
> 경고: 계속 하기 전에 [로그인, 전자 메일 확인 및 암호 재설정을 사용 하 여 보안 ASP.NET MVC 5 웹 앱 만들기를](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) 완료 해야 합니다. 이 자습서를 완료 하려면 [Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 이상을 설치 해야 합니다.

1. 새 ASP.NET 웹 프로젝트를 만들고 MVC 템플릿을 선택 합니다. Web Forms는 ASP.NET Identity도 지원 하므로 web Forms 앱에서 비슷한 단계를 따를 수 있습니다.  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image1.png)
2. 기본 인증을 **개별 사용자 계정**으로 그대로 둡니다. Azure에서 앱을 호스팅하려면 확인란을 선택 된 상태로 둡니다. 이 자습서의 뒷부분에서는 Azure에 배포 합니다. [Azure 계정을 무료로 열](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)수 있습니다.
3. [SSL을 사용 하도록 프로젝트](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)를 설정 합니다.

<a id="SMS"></a>
## <a name="set-up-sms-for-two-factor-authentication"></a>2 단계 인증을 위한 SMS 설정

이 자습서에서는 Twilio 또는 기능 SMS를 사용 하는 방법에 대 한 지침을 제공 하지만 다른 SMS 공급자를 사용할 수 있습니다.

1. **SMS 공급자를 사용 하 여 사용자 계정 만들기**  
  
   [Twilio](https://www.twilio.com/try-twilio) 또는 기타 [sms](https://www.aspsms.com/asp.net/identity/testcredits/) 계정을 만듭니다.
2. **추가 패키지 설치 또는 서비스 참조 추가**  
  
   Twilio  
   패키지 관리자 콘솔에서 다음 명령을 입력합니다.  
    `Install-Package Twilio`  
  
   ASPSMS:  
   다음 서비스 참조를 추가 해야 합니다.  
  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image2.png)  
  
   주소:  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   네임스페이스:  
    `ASPSMSX2`
3. **SMS 공급자 사용자 자격 증명 파악**  
  
   Twilio  
   Twilio 계정의 **대시보드** 탭에서 **계정 SID** 및 **인증 토큰**을 복사 합니다.  
  
   ASPSMS:  
   계정 설정에서 **Userkey** 로 이동 하 여 자체 정의 된 **암호**와 함께 복사 합니다.  
  
   나중에 이러한 값을 `"SMSAccountIdentification"` 키 내의 *web.config 파일에 저장 하 고* `"SMSAccountPassword"` 합니다.
4. **SenderID/송신자 지정**  
  
   Twilio  
   **숫자** 탭에서 Twilio 전화 번호를 복사 합니다.  
  
   ASPSMS:  
   **보낸 사람 잠금 해제** 메뉴 내에서 하나 이상의 발신자의 잠금을 해제 하거나 영숫자 송신자 (모든 네트워크에서 지원 되지 않음)를 선택 합니다.  
  
   나중에이 값을 키 `"SMSAccountFrom"` 내의 *web.config 파일에 저장 합니다.*
5. **SMS 공급자 자격 증명을 앱으로 전송**  
  
   앱에서 자격 증명 및 발신자 전화 번호를 사용할 수 있도록 설정 합니다. 작업을 단순하게 유지 하기 위해 이러한 값을 *web.config* 파일에 저장 합니다. Azure에 배포할 때 웹 사이트 구성 탭의 **앱 설정** 섹션에 값을 안전 하 게 저장할 수 있습니다. 

    [!code-xml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample1.xml?highlight=8-10)]

    > [!WARNING]
    > 보안-중요 한 데이터를 소스 코드에 저장 하지 않습니다. 예제를 단순하게 유지 하기 위해 위의 코드에 계정 및 자격 증명이 추가 됩니다. [암호 및 기타 중요 한 데이터를 ASP.NET 및 Azure에 배포 하는 방법에 대 한 모범 사례](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)를 참조 하세요.
6. **SMS 공급자에 대 한 데이터 전송 구현**  
  
   *앱\_Start\IdentityConfig.cs* 파일에서 `SmsService` 클래스를 구성 합니다.  
  
   사용 된 SMS 공급자에 따라 **Twilio** 또는 기타 **sms** 섹션을 활성화 합니다. 

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample2.cs)]
7. *Views\Manage\Index.cshtml* Razor 뷰를 업데이트 합니다. (참고: 종료 코드에서 주석을 제거 하지 말고 아래 코드를 사용 하십시오.)  

    [!code-cshtml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample3.cshtml?highlight=29-66)]
8. `ManageController`의 `EnableTwoFactorAuthentication` 및 `DisableTwoFactorAuthentication` 작업 메서드에[[ValidateAntiForgeryToken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.118).aspx) 특성이 있는지 확인 합니다.  

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample4.cs?highlight=3,16)]
9. 앱을 실행 하 고 이전에 등록 한 계정으로 로그인 합니다.
10. `Manage` 컨트롤러에서 `Index` 작업 메서드를 활성화 하는 사용자 ID를 클릭 합니다.  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image3.png)
11. 추가를 클릭합니다.  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image4.png)
12. `AddPhoneNumber` 작업 메서드는 SMS 메시지를 받을 수 있는 전화 번호를 입력할 수 있는 대화 상자를 표시 합니다.

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample5.cs)]

    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image5.png)
13. 몇 초 후에 확인 코드를 포함 하는 문자 메시지를 받게 됩니다. 입력 하 고 **제출**을 누릅니다.  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image6.png)
14. 관리 보기에는 전화 번호가 추가 된 것이 표시 됩니다.

<a id="enable2"></a>
## <a name="enable-two-factor-authentication"></a>2 단계 인증을 사용 하도록 설정

템플릿에서 생성 된 앱에서 2 단계 인증 (2FA)을 사용 하도록 설정 하려면 UI를 사용 해야 합니다. 2FA를 사용 하도록 설정 하려면 탐색 모음에서 사용자 ID (전자 메일 별칭)를 클릭 합니다.

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image7.png)

2FA 사용을 클릭 합니다.

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image8.png)

로그 아웃 한 다음 다시 로그인 합니다. 전자 메일을 사용 하도록 설정한 경우 ( [이전 자습서](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)참조) 2FA의 SMS 또는 전자 메일을 선택할 수 있습니다.

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image9.png)

코드를 입력할 수 있는 코드 확인 페이지가 표시 됩니다 (SMS 또는 전자 메일에서).

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image10.png)

**이 브라우저 저장** 확인란을 클릭 하면 상자를 선택한 브라우저와 장치를 사용 하는 경우에는 2fa를 사용 하 여 로그인 할 필요가 없게 됩니다. 악의적인 사용자가 장치에 대 한 액세스 권한을 얻을 수 없는 한, 2FA를 사용 하도록 설정 하 고 기억을 클릭 하면 **이 브라우저** 는 신뢰할 수 있는 장치에서 모든 액세스를 위한 강력한 2fa 보호를 유지 하면서 한 단계 암호 액세스를 편리 하 게 제공 합니다. 정기적으로 사용 하는 모든 개인 장치에서이 수행할 수 있습니다.

이 자습서에서는 새 ASP.NET MVC 앱에서 2FA를 사용 하도록 설정 하는 방법을 간략하게 소개 합니다. [SMS 및 전자 메일을 사용 하는 내 자습서 2 단계 인증은](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) 샘플에 포함 된 코드에 대 한 세부 정보를 ASP.NET Identity.

<a id="addRes"></a>
## <a name="additional-resources"></a>추가 리소스

- [SMS 및 전자 메일을 사용 하는 2 단계 인증 ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) 2 단계 인증에 대 한 세부 정보를 확인 합니다.
- [ASP.NET Identity 권장 리소스에 대 한 링크](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [계정 확인 및 암호 복구 ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) 암호 복구 및 계정 확인에 대해 자세히 설명 합니다.
- [Facebook, Twitter, LinkedIn 및 Google OAuth2 sign-on을 사용한 MVC 5 앱](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 이 자습서에서는 Facebook 및 Google OAuth 2 권한 부여를 사용 하 여 ASP.NET MVC 5 앱을 작성 하는 방법을 보여 줍니다. 또한 Id 데이터베이스에 데이터를 추가 하는 방법을 보여 줍니다.
- [멤버 자격, OAuth 및 SQL Database가 포함 된 보안 ASP.NET MVC 앱을 Azure 웹에 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다. 이 자습서에서는 Azure 배포, 역할을 사용 하 여 앱을 보호 하는 방법, 멤버 자격 API를 사용 하 여 사용자 및 역할을 추가 하는 방법 및 추가 보안 기능을 추가 합니다.
- [OAuth 2 용 Google 앱 만들기 및 프로젝트에 앱 연결](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [Facebook에서 앱 만들기 및 프로젝트에 앱 연결](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [프로젝트에서 SSL 설정](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
- [C# 및 ASP.NET MVC 개발 환경을 설정 하는 방법](https://www.twilio.com/docs/usage/tutorials/how-to-set-up-your-csharp-and-asp-net-mvc-development-environment)
