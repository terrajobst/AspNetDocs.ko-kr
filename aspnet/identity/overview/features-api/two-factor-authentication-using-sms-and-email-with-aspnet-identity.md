---
uid: identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity
title: SMS 및 전자 메일을 사용 하는 2 단계 인증 ASP.NET Identity-ASP.NET 4.x
author: HaoK
description: 이 자습서에서는 SMS 및 전자 메일을 사용 하 여 2 단계 인증 (2FA)을 설정 하는 방법을 보여 줍니다. 이 문서는 Rick Anderson (@RickAndMSFT), Pr에서 작성 되었습니다.
ms.author: riande
ms.date: 09/15/2015
ms.assetid: 053e23c4-13c9-40fa-87cb-3e9b0823b31e
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 527b4392846e60dae0b216fdeabf21fd6618e4d7
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456740"
---
# <a name="two-factorauthentication-using-sms-and-email-with-aspnet-identity"></a>SMS 및 전자 메일을 사용 하는 2 단계 인증 ASP.NET Identity

[Jia-hao Kung](https://github.com/HaoK), [Pranav rastogi](https://github.com/rustd), [Rick Anderson](https://twitter.com/RickAndMSFT), [suhas](https://github.com/suhasj)

> 이 자습서에서는 SMS 및 전자 메일을 사용 하 여 2 단계 인증 (2FA)을 설정 하는 방법을 보여 줍니다.
> 
> 이 문서는[@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)(Rick Anderson), Pranav Rastogi ([@rustd](https://twitter.com/rustd)), jia-hao Kung, suhas Joshi에 의해 작성 되었습니다. NuGet 샘플은 주로 Jia-hao Kung에 의해 작성 되었습니다.

이 항목에서는 다음에 대해 설명합니다.

- [Identity 샘플 빌드](#build)
- [2 단계 인증을 위한 SMS 설정](#SMS)
- [2 단계 인증 사용](#enable2)
- [2 단계 인증 공급자를 등록 하는 방법](#reg)
- [소셜 및 로컬 로그인 계정 결합](#combine)
- [무차별 암호 대입 공격 으로부터 계정 잠금](#lock)

<a id="build"></a>

## <a name="building-the-identity-sample"></a>Identity 샘플 빌드

이 섹션에서는 NuGet을 사용 하 여 작업 하는 샘플을 다운로드 합니다. 웹 또는 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) [에 대해 Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 을 설치 하 고 실행 하 여 시작 합니다. Visual Studio [2013 업데이트 2](https://go.microsoft.com/fwlink/?LinkId=390521) 이상을 설치 합니다.

> [!NOTE]
> 경고:이 자습서를 완료 하려면 Visual Studio [2013 업데이트 2](https://go.microsoft.com/fwlink/?LinkId=390521) 를 설치 해야 합니다.

1. ***빈*** ASP.NET 웹 프로젝트를 새로 만듭니다.
2. 패키지 관리자 콘솔에서 다음 명령을 입력 합니다.  
  
    `Install-Package SendGrid`  
    `Install-Package -Prerelease Microsoft.AspNet.Identity.Samples`  
  
   이 자습서에서는 [SendGrid](http://sendgrid.com/) 를 사용 하 여 sms texting에 대 한 전자 메일 및 [Twilio](https://www.twilio.com/) 또는 대상 [sms](https://www.aspsms.com/asp.net/identity/testcredits/) 를 보냅니다. `Identity.Samples` 패키지는 작업할 코드를 설치 합니다.
3. [SSL을 사용 하도록 프로젝트](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)를 설정 합니다.
4. *선택 사항*: 내 [메일 확인 자습서](account-confirmation-and-password-recovery-with-aspnet-identity.md) 의 지침에 따라 SendGrid를 연결 하 고 앱을 실행 하 고 전자 메일 계정을 등록 합니다.
5. *선택 사항:* 샘플 (계정 컨트롤러의 `ViewBag.Link` 코드에서 데모 전자 메일 링크 확인 코드를 제거 합니다. `DisplayEmail` 및 `ForgotPasswordConfirmation` 작업 메서드 및 razor 뷰)를 참조 하세요.
6. *선택 사항:* 관리 및 계정 컨트롤러와 *Views\Account\VerifyCode.cshtml* 및 *Views\Manage\VerifyPhoneNumber.cshtml* razor 보기에서 `ViewBag.Status` 코드를 제거 합니다. 또는 연결 하 고 전자 메일 및 SMS 메시지를 보내지 않고도이 앱이 로컬에서 작동 하는 방식을 테스트 하기 위해 `ViewBag.Status` 표시를 유지할 수 있습니다.

> [!NOTE]
> 경고:이 샘플에서 보안 설정을 변경 하는 경우 생성 된 변경 내용을 명시적으로 호출 하는 보안 감사를 생성 해야 합니다.

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
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image1.png)  
  
   주소:  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   네임스페이스:  
    `ASPSMSX2`
3. **SMS 공급자 사용자 자격 증명 파악**  
  
   Twilio  
   Twilio 계정의 **대시보드** 탭에서 **계정 SID** 및 **인증 토큰**을 복사 합니다.  
  
   ASPSMS:  
   계정 설정에서 **Userkey** 로 이동 하 여 자체 정의 된 **암호**와 함께 복사 합니다.  
  
   나중에 `SMSAccountIdentification` 및 `SMSAccountPassword` 변수에 이러한 값을 저장 합니다.
4. **SenderID/송신자 지정**  
  
   Twilio  
   **숫자** 탭에서 Twilio 전화 번호를 복사 합니다.  
  
   ASPSMS:  
   **보낸 사람 잠금 해제** 메뉴 내에서 하나 이상의 발신자의 잠금을 해제 하거나 영숫자 송신자 (모든 네트워크에서 지원 되지 않음)를 선택 합니다.  
  
   나중에 `SMSAccountFrom` 변수에이 값을 저장 합니다.
5. **SMS 공급자 자격 증명을 앱으로 전송**  
  
   앱에서 자격 증명 및 발신자 전화 번호를 사용할 수 있도록 설정 합니다.

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample1.cs)]

    > [!WARNING]
    > 보안-중요 한 데이터를 소스 코드에 저장 하지 않습니다. 예제를 단순하게 유지 하기 위해 위의 코드에 계정 및 자격 증명이 추가 됩니다. Jon Atten의 [ASP.NET MVC: 소스 제어에서 비공개 설정 유지](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx)를 참조 하세요.
6. **SMS 공급자에 대 한 데이터 전송 구현**  
  
   *앱\_Start\IdentityConfig.cs* 파일에서 `SmsService` 클래스를 구성 합니다.  
  
   사용 된 SMS 공급자에 따라 **Twilio** 또는 기타 **sms** 섹션을 활성화 합니다. 

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample2.cs)]
7. 앱을 실행 하 고 이전에 등록 한 계정으로 로그인 합니다.
8. `Manage` 컨트롤러에서 `Index` 작업 메서드를 활성화 하는 사용자 ID를 클릭 합니다.  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image2.png)
9. 추가를 클릭합니다.  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image3.png)
10. 몇 초 후에 확인 코드를 포함 하는 문자 메시지를 받게 됩니다. 입력 하 고 **제출**을 누릅니다.  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image4.png)
11. 관리 보기에는 전화 번호가 추가 된 것이 표시 됩니다.  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image5.png)

### <a name="examine-the-code"></a>코드 검사

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample3.cs?highlight=2)]

`Manage` 컨트롤러의 `Index` 작업 메서드는 이전 작업을 기반으로 상태 메시지를 설정 하 고 로컬 암호를 변경 하거나 로컬 계정을 추가할 수 있는 링크를 제공 합니다. `Index` 메서드는이 브라우저에 대해 상태 또는 2FA 전화 번호, 외부 로그인, 2FA, 2FA, 기억을 2FA 메서드 (뒷부분에서 설명 함)를 표시 합니다. 제목 표시줄에서 사용자 ID (전자 메일)를 클릭 하면 메시지가 전달 되지 않습니다. **전화 번호** 를 클릭 하면 링크 제거 `Message=RemovePhoneSuccess` 쿼리 문자열로 전달 됩니다.  
  
`https://localhost:44300/Manage?Message=RemovePhoneSuccess`

[![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image6.png)]

`AddPhoneNumber` 작업 메서드는 SMS 메시지를 받을 수 있는 전화 번호를 입력할 수 있는 대화 상자를 표시 합니다.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample4.cs)]

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image7.png)

**확인 코드 보내기** 단추를 클릭 하면 전화 번호가 HTTP POST `AddPhoneNumber` 작업 메서드에 게시 됩니다.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample5.cs?highlight=12)]

`GenerateChangePhoneNumberTokenAsync` 메서드는 SMS 메시지에 설정 되는 보안 토큰을 생성 합니다. SMS 서비스가 구성 된 경우 토큰은 &quot;문자열로 전송 됩니다. 보안 코드는 &quot;&gt;&lt;토큰입니다. `SmsService.SendAsync` 메서드가 비동기적으로 호출 되 면 앱이 `VerifyPhoneNumber` 작업 메서드로 리디렉션됩니다 (다음 대화 상자 표시). 그러면 확인 코드를 입력할 수 있습니다.

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image8.png)

코드를 입력 하 고 제출을 클릭 하면 코드가 HTTP POST `VerifyPhoneNumber` 작업 메서드에 게시 됩니다.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample6.cs)]

`ChangePhoneNumberAsync` 메서드는 게시 된 보안 코드를 확인 합니다. 코드가 올바르면 전화 번호가 `AspNetUsers` 테이블의 `PhoneNumber` 필드에 추가 됩니다. 호출에 성공 하면 `SignInAsync` 메서드가 호출 됩니다.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample7.cs)]

`isPersistent` 매개 변수는 인증 세션이 여러 요청에서 지속 되는지 여부를 설정 합니다.

보안 프로필을 변경 하면 새 보안 스탬프가 생성 되어 *AspNetUsers* 테이블의 `SecurityStamp` 필드에 저장 됩니다. `SecurityStamp` 필드는 보안 쿠키와 다릅니다. 보안 쿠키는 `AspNetUsers` 테이블 (또는 Identity DB의 다른 위치)에 저장 되지 않습니다. 보안 쿠키 토큰은 [DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx) 를 사용 하 여 자체 서명 되며 `UserId, SecurityStamp` 및 만료 시간 정보를 사용 하 여 생성 됩니다.

쿠키 미들웨어는 각 요청에서 쿠키를 확인 합니다. `Startup` 클래스의 `SecurityStampValidator` 메서드는 DB에 적중 하 고 `validateInterval`에 지정 된 대로 주기적으로 보안 스탬프를 확인 합니다. 이는 보안 프로필을 변경 하지 않는 한 30 분 마다 (이 샘플에서) 발생 합니다. 데이터베이스에 대 한 왕복을 최소화 하기 위해 30 분 간격을 선택 했습니다.

보안 프로필을 변경 하는 경우 `SignInAsync` 메서드를 호출 해야 합니다. 보안 프로필이 변경 되 면 데이터베이스는 `SecurityStamp` 필드를 업데이트 하 고 `SignInAsync` 메서드를 호출 하지 않으면 다음에 OWIN 파이프라인이 데이터베이스 (`validateInterval`)에 *도달할 때 까지만* 로그인 상태를 유지 합니다. 즉시 반환 되도록 `SignInAsync` 메서드를 변경 하 고 쿠키 `validateInterval` 속성을 30 분에서 5 초로 설정 하 여이를 테스트할 수 있습니다.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample8.cs?highlight=3)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample9.cs?highlight=20-21)]

위의 코드를 변경 하면 보안 프로필을 변경할 수 있습니다. 예를 들어 **두 가지 요소를 사용 하도록 설정한**상태를 변경 하 여 보안 프로필을 변경할 수 있으며, `SecurityStampValidator.OnValidateIdentity` 메서드가 실패 하면 5 초 이내에 로그 아웃 됩니다. `SignInAsync` 메서드에서 반환 줄을 제거 하 고 다른 보안 프로필을 변경 하 고 로그 아웃 하지 않습니다. `SignInAsync` 메서드는 새 보안 쿠키를 생성 합니다.

<a id="enable2"></a>

## <a name="enable-two-factor-authentication"></a>2 단계 인증을 사용 하도록 설정

샘플 앱에서 2 단계 인증 (2FA)을 사용 하도록 설정 하려면 UI를 사용 해야 합니다. 2FA를 사용 하도록 설정 하려면 탐색 모음에서 사용자 ID (전자 메일 별칭)를 클릭 합니다.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image9.png)  
2FA 사용을 클릭 합니다.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image10.png) 로그 아웃 한 다음 다시 로그인 합니다. 전자 메일을 사용 하도록 설정한 경우 ( [이전 자습서](account-confirmation-and-password-recovery-with-aspnet-identity.md)참조) 2FA의 SMS 또는 전자 메일을 선택할 수 있습니다.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image11.png) 코드를 입력할 수 있는 코드 확인 페이지가 표시 됩니다 (SMS 또는 전자 메일에서).![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image12.png) **이 브라우저 기억을** 확인란을 클릭 하면 해당 컴퓨터 및 브라우저를 사용 하 여 로그온 하는 데 2fa를 사용할 필요가 없습니다. 2FA를 사용 하도록 설정 하 고 **이 브라우저** 를 클릭 하면 컴퓨터에 액세스할 수 없는 한 악의적인 사용자가 계정에 액세스 하는 것과 같은 강력한 2fa 보호를 제공 합니다. 정기적으로 사용 하는 모든 개인 컴퓨터에서이 작업을 수행할 수 있습니다. **이 브라우저 기억을**설정 하면 정기적으로 사용 하지 않는 컴퓨터에서 2fa의 보안을 강화 하 고, 사용자 컴퓨터에서 2fa를 거치지 않아도 편리 하 게 이용할 수 있습니다. 

<a id="reg"></a>
## <a name="how-to-register-a-two-factor-authentication-provider"></a>2 단계 인증 공급자를 등록 하는 방법

새 MVC 프로젝트를 만들 때 *IdentityConfig.cs* 파일에는 2 단계 인증 공급자를 등록 하는 다음 코드가 포함 되어 있습니다.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample10.cs?highlight=22-35)]

## <a name="add-a-phone-number-for-2fa"></a>2FA의 전화 번호 추가

`Manage` 컨트롤러의 `AddPhoneNumber` 작업 메서드는 보안 토큰을 생성 하 고 사용자가 제공한 전화 번호로 보냅니다.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample11.cs)]

토큰을 보낸 후에는 `VerifyPhoneNumber` 작업 메서드로 리디렉션하고 2FA에 SMS를 등록 하는 코드를 입력할 수 있습니다. SMS 2FA는 전화 번호를 확인할 때까지 사용 되지 않습니다.

## <a name="enabling-2fa"></a>2FA 사용

`EnableTFA` 작업 메서드는 2FA를 사용 하도록 설정 합니다.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample12.cs)]

사용 2FA가 보안 프로필에 대 한 변경 이기 때문에 `SignInAsync`를 호출 해야 합니다. 2FA를 사용 하도록 설정한 경우 사용자가 등록 한 2FA 접근 방식 (샘플의 SMS 및 전자 메일)을 사용 하 여 2FA를 사용 하 여 로그인 해야 합니다.

QR 코드 생성기와 같은 2 개의 FA 공급자를 추가 하거나 직접 작성할 수 있습니다 ( [ASP.NET Identity에서 Google 인증자 사용](https://www.jerriepelser.com//blog/using-google-authenticator-asp-net-identity/)참조).

> [!NOTE]
> 2FA 코드는 [시간 기반 일회용 암호 알고리즘](http://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm) 을 사용 하 여 생성 되 고 코드는 6 분 동안 유효 합니다. 코드를 입력 하는 데 6 분 이상 소요 되 면 잘못 된 코드 오류 메시지를 받게 됩니다.

<a id="combine"></a>

## <a name="combine-social-and-local-login-accounts"></a>소셜 및 로컬 로그인 계정 결합

전자 메일 링크를 클릭 하 여 로컬 및 소셜 계정을 결합할 수 있습니다. 다음 시퀀스 &quot;RickAndMSFT@gmail.com&quot; 먼저 로컬 로그인으로 만들어지므로 먼저 계정을 소셜 로그인으로 만든 다음 로컬 로그인을 추가할 수 있습니다.

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image13.png)

**관리** 링크를 클릭 합니다. 이 계정과 연결 된 0 외부 (소셜 로그인)를 확인 합니다.

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image14.png)

다른 로그인 서비스에 대 한 링크를 클릭 하 고 앱 요청을 수락 합니다. 두 계정을 결합 하 여 두 계정을 사용 하 여 로그온 할 수 있습니다. 인증 서비스의 소셜 로그인이 다운 되거나 소셜 계정에 대 한 액세스 권한이 손실 될 가능성이 있는 경우 사용자가 로컬 계정을 추가 하도록 할 수 있습니다.

다음 그림에서 Tom은 **외부 로그인** 에서 볼 수 있는 소셜 로그인입니다. 1은 페이지에 표시 됩니다.

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image15.png)

**암호 선택** 을 클릭 하면 동일한 계정에 연결 된 로컬 로그를 추가할 수 있습니다.

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image16.png)

<a id="lock"></a>

## <a name="account-lockout-from-brute-force-attacks"></a>무차별 암호 대입 공격 으로부터 계정 잠금

사용자 잠금을 사용 하도록 설정 하 여 사전 공격 으로부터 앱 계정을 보호할 수 있습니다. `ApplicationUserManager Create` 메서드의 다음 코드는 잠금 해제를 구성 합니다.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample13.cs)]

위의 코드는 2 단계 인증에 대해서만 잠금을 사용 하도록 설정 합니다. 계정 컨트롤러의 `Login` 메서드에서 `shouldLockout`를 true로 변경 하 여 로그인 잠금을 설정할 수 있지만 계정이 [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) 로그인 공격에 취약 하기 때문에 로그인에 대 한 잠금을 사용 하지 않는 것이 좋습니다. 샘플 코드에서는 `ApplicationDbInitializer Seed` 메서드에서 만든 관리자 계정에 대해 잠금이 사용 하지 않도록 설정 되어 있습니다.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample14.cs?highlight=19)]

## <a name="requiring-a-user-to-have-a-validated-email-account"></a>사용자에 게 유효성을 검사 한 전자 메일 계정 필요

다음 코드에서는 사용자가 로그인 하기 전에 유효성을 검사 한 전자 메일 계정이 있어야 합니다.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample15.cs?highlight=8-17)]

## <a name="how-signinmanager-checks-for-2fa-requirement"></a>SignInManager에서 2FA 요구 사항을 확인 하는 방법

로컬 로그인과 소셜 로그인은 모두 2FA가 사용 되는지 확인 합니다. 2FA를 사용 하는 경우 `SignInManager` logon 메서드가 `SignInStatus.RequiresVerification`를 반환 하 고 사용자가 `SendCode` 작업 메서드로 리디렉션됩니다. 여기서 사용자는 코드를 입력 하 여 로그를 순서 대로 완료 해야 합니다. 사용자가 사용자 로컬 쿠키에 대해 RememberMe를 설정 하는 경우 `SignInManager`은 `SignInStatus.Success`을 반환 하 고 2FA를 통과 하지 않아도 됩니다.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample16.cs?highlight=20-22)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample17.cs?highlight=10-11,17-18)]

다음 코드에서는 `SendCode` 작업 메서드를 보여 줍니다. [Selectlistitem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) 은 사용자에 대해 사용 하도록 설정 된 모든 2fa 메서드를 사용 하 여 만들어집니다. [Selectlistitem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) 은 [DropDownListFor](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist.aspx) 도우미에 전달 되며,이를 통해 사용자는 2fa 접근 방식 (일반적으로 메일 및 SMS)을 선택할 수 있습니다.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample18.cs)]

사용자가 2FA 방법을 게시 하면 `HTTP POST SendCode` 동작 메서드가 호출 되 고, `SignInManager`는 2FA 코드를 보내고, 사용자는 코드를 입력 하 여 로그인을 완료할 수 있는 `VerifyCode` 작업 메서드로 리디렉션됩니다.

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample19.cs?highlight=3,13-14,18)]

## <a name="2fa-lockout"></a>2FA 잠금

로그인 암호 시도 실패 시 계정 잠금을 설정할 수 있지만이 방법을 사용 하면 로그인이 [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) 잠금에 취약 해질 수 있습니다. 2FA와만 계정 잠금을 사용 하는 것이 좋습니다. `ApplicationUserManager` 만들어지면 샘플 코드는 2FA 잠금과 `MaxFailedAccessAttemptsBeforeLockout`를 5로 설정 합니다. 사용자가 로컬 계정 또는 소셜 계정을 통해 로그인 하면 2FA에서 실패 한 각 시도가 저장 되 고, 최대 시도 횟수에 도달 하면 사용자가 5 분 동안 잠깁니다 (잠금 시간을 `DefaultAccountLockoutTimeSpan`로 설정할 수 있음).

<a id="addRes"></a>

## <a name="additional-resources"></a>추가 리소스

- [권장 리소스 ASP.NET Identity](../getting-started/aspnet-identity-recommended-resources.md) Id 블로그, 비디오, 자습서 등의 전체 목록과 유용한 링크를 제공 합니다.
- [Facebook, Twitter, LinkedIn 및 Google OAuth2 sign-on이 포함 된 MVC 5 앱](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 은 사용자 테이블에 프로필 정보를 추가 하는 방법을 보여 줍니다.
- [ASP.NET MVC 및 id 2.0: John Atten의 기본 사항을 이해](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx) 합니다.
- [계정 확인 및 암호 복구 ASP.NET Identity](account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [ASP.NET ID 소개](../getting-started/introduction-to-aspnet-identity.md)
- Pranav Rastogi가 [ASP.NET Identity 2.0.0의 RTM을 발표](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) 합니다.
- [ASP.NET Identity 2.0: John Atten에서 계정 유효성 검사 및 2 단계 권한 부여를 설정](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) 합니다.
