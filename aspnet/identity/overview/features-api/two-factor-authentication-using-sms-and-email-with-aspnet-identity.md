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
# <a name="two-factorauthentication-using-sms-and-email-with-aspnet-identity"></a><span data-ttu-id="d46d2-104">SMS 및 전자 메일을 사용 하는 2 단계 인증 ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="d46d2-104">Two-factor authentication using SMS and email with ASP.NET Identity</span></span>

<span data-ttu-id="d46d2-105">[Jia-hao Kung](https://github.com/HaoK), [Pranav rastogi](https://github.com/rustd), [Rick Anderson](https://twitter.com/RickAndMSFT), [suhas](https://github.com/suhasj)</span><span class="sxs-lookup"><span data-stu-id="d46d2-105">by [Hao Kung](https://github.com/HaoK), [Pranav Rastogi](https://github.com/rustd), [Rick Anderson](https://twitter.com/RickAndMSFT), [Suhas Joshi](https://github.com/suhasj)</span></span>

> <span data-ttu-id="d46d2-106">이 자습서에서는 SMS 및 전자 메일을 사용 하 여 2 단계 인증 (2FA)을 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-106">This tutorial will show you how to set up Two-factor authentication (2FA) using SMS and email.</span></span>
> 
> <span data-ttu-id="d46d2-107">이 문서는[@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)(Rick Anderson), Pranav Rastogi ([@rustd](https://twitter.com/rustd)), jia-hao Kung, suhas Joshi에 의해 작성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-107">This article was written by Rick Anderson ([@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)), Pranav Rastogi ([@rustd](https://twitter.com/rustd)), Hao Kung, and Suhas Joshi.</span></span> <span data-ttu-id="d46d2-108">NuGet 샘플은 주로 Jia-hao Kung에 의해 작성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-108">The NuGet sample was written primarily by Hao Kung.</span></span>

<span data-ttu-id="d46d2-109">이 항목에서는 다음에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-109">This topic covers the following:</span></span>

- [<span data-ttu-id="d46d2-110">Identity 샘플 빌드</span><span class="sxs-lookup"><span data-stu-id="d46d2-110">Building the Identity sample</span></span>](#build)
- [<span data-ttu-id="d46d2-111">2 단계 인증을 위한 SMS 설정</span><span class="sxs-lookup"><span data-stu-id="d46d2-111">Set up SMS for Two-factor authentication</span></span>](#SMS)
- [<span data-ttu-id="d46d2-112">2 단계 인증 사용</span><span class="sxs-lookup"><span data-stu-id="d46d2-112">Enable Two-factor authentication</span></span>](#enable2)
- [<span data-ttu-id="d46d2-113">2 단계 인증 공급자를 등록 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d46d2-113">How to register a Two-factor authentication provider</span></span>](#reg)
- [<span data-ttu-id="d46d2-114">소셜 및 로컬 로그인 계정 결합</span><span class="sxs-lookup"><span data-stu-id="d46d2-114">Combine social and local login accounts</span></span>](#combine)
- [<span data-ttu-id="d46d2-115">무차별 암호 대입 공격 으로부터 계정 잠금</span><span class="sxs-lookup"><span data-stu-id="d46d2-115">Account lockout from brute force attacks</span></span>](#lock)

<a id="build"></a>

## <a name="building-the-identity-sample"></a><span data-ttu-id="d46d2-116">Identity 샘플 빌드</span><span class="sxs-lookup"><span data-stu-id="d46d2-116">Building the Identity sample</span></span>

<span data-ttu-id="d46d2-117">이 섹션에서는 NuGet을 사용 하 여 작업 하는 샘플을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-117">In this section, you'll use NuGet to download a sample we will work with.</span></span> <span data-ttu-id="d46d2-118">웹 또는 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) [에 대해 Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 을 설치 하 고 실행 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-118">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="d46d2-119">Visual Studio [2013 업데이트 2](https://go.microsoft.com/fwlink/?LinkId=390521) 이상을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-119">Install Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521) or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="d46d2-120">경고:이 자습서를 완료 하려면 Visual Studio [2013 업데이트 2](https://go.microsoft.com/fwlink/?LinkId=390521) 를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-120">Warning: You must install Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521) to complete this tutorial.</span></span>

1. <span data-ttu-id="d46d2-121">***빈*** ASP.NET 웹 프로젝트를 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-121">Create a new ***empty*** ASP.NET Web project.</span></span>
2. <span data-ttu-id="d46d2-122">패키지 관리자 콘솔에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-122">In the Package Manager Console, enter the following the following commands:</span></span>  
  
    `Install-Package SendGrid`  
    `Install-Package -Prerelease Microsoft.AspNet.Identity.Samples`  
  
   <span data-ttu-id="d46d2-123">이 자습서에서는 [SendGrid](http://sendgrid.com/) 를 사용 하 여 sms texting에 대 한 전자 메일 및 [Twilio](https://www.twilio.com/) 또는 대상 [sms](https://www.aspsms.com/asp.net/identity/testcredits/) 를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-123">In this tutorial, we'll use [SendGrid](http://sendgrid.com/) to send email and [Twilio](https://www.twilio.com/) or [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) for sms texting.</span></span> <span data-ttu-id="d46d2-124">`Identity.Samples` 패키지는 작업할 코드를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-124">The `Identity.Samples` package installs the code we will be working with.</span></span>
3. <span data-ttu-id="d46d2-125">[SSL을 사용 하도록 프로젝트](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-125">Set the [project to use SSL](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>
4. <span data-ttu-id="d46d2-126">*선택 사항*: 내 [메일 확인 자습서](account-confirmation-and-password-recovery-with-aspnet-identity.md) 의 지침에 따라 SendGrid를 연결 하 고 앱을 실행 하 고 전자 메일 계정을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-126">*Optional*: Follow the instructions in my [Email confirmation tutorial](account-confirmation-and-password-recovery-with-aspnet-identity.md) to hook up SendGrid and then run the app and register an email account.</span></span>
5. <span data-ttu-id="d46d2-127">*선택 사항:* 샘플 (계정 컨트롤러의 `ViewBag.Link` 코드에서 데모 전자 메일 링크 확인 코드를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-127">*Optional:* Remove the demo email link confirmation code from the sample (The `ViewBag.Link` code in the account controller.</span></span> <span data-ttu-id="d46d2-128">`DisplayEmail` 및 `ForgotPasswordConfirmation` 작업 메서드 및 razor 뷰)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="d46d2-128">See the `DisplayEmail` and `ForgotPasswordConfirmation` action methods and razor views ).</span></span>
6. <span data-ttu-id="d46d2-129">*선택 사항:* 관리 및 계정 컨트롤러와 *Views\Account\VerifyCode.cshtml* 및 *Views\Manage\VerifyPhoneNumber.cshtml* razor 보기에서 `ViewBag.Status` 코드를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-129">*Optional:* Remove the `ViewBag.Status` code from the Manage and Account controllers and from the *Views\Account\VerifyCode.cshtml* and *Views\Manage\VerifyPhoneNumber.cshtml* razor views.</span></span> <span data-ttu-id="d46d2-130">또는 연결 하 고 전자 메일 및 SMS 메시지를 보내지 않고도이 앱이 로컬에서 작동 하는 방식을 테스트 하기 위해 `ViewBag.Status` 표시를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-130">Alternatively, you can keep the `ViewBag.Status` display to test how this app works locally without having to hook up and send email and SMS messages.</span></span>

> [!NOTE]
> <span data-ttu-id="d46d2-131">경고:이 샘플에서 보안 설정을 변경 하는 경우 생성 된 변경 내용을 명시적으로 호출 하는 보안 감사를 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-131">Warning: If you change any of the security settings in this sample, productions apps will need to undergo a security audit that explicitly calls out the changes made.</span></span>

<a id="SMS"></a>

## <a name="set-up-sms-for-two-factor-authentication"></a><span data-ttu-id="d46d2-132">2 단계 인증을 위한 SMS 설정</span><span class="sxs-lookup"><span data-stu-id="d46d2-132">Set up SMS for Two-factor authentication</span></span>

<span data-ttu-id="d46d2-133">이 자습서에서는 Twilio 또는 기능 SMS를 사용 하는 방법에 대 한 지침을 제공 하지만 다른 SMS 공급자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-133">This tutorial provides instructions for using either Twilio or ASPSMS but you can use any other SMS provider.</span></span>

1. <span data-ttu-id="d46d2-134">**SMS 공급자를 사용 하 여 사용자 계정 만들기**</span><span class="sxs-lookup"><span data-stu-id="d46d2-134">**Creating a User Account with an SMS provider**</span></span>  
  
   <span data-ttu-id="d46d2-135">[Twilio](https://www.twilio.com/try-twilio) 또는 기타 [sms](https://www.aspsms.com/asp.net/identity/testcredits/) 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-135">Create a [Twilio](https://www.twilio.com/try-twilio) or an [ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/) account.</span></span>
2. <span data-ttu-id="d46d2-136">**추가 패키지 설치 또는 서비스 참조 추가**</span><span class="sxs-lookup"><span data-stu-id="d46d2-136">**Installing additional packages or adding service references**</span></span>  
  
   <span data-ttu-id="d46d2-137">Twilio</span><span class="sxs-lookup"><span data-stu-id="d46d2-137">Twilio:</span></span>  
   <span data-ttu-id="d46d2-138">패키지 관리자 콘솔에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-138">In the Package Manager Console, enter the following command:</span></span>  
    `Install-Package Twilio`  
  
   <span data-ttu-id="d46d2-139">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="d46d2-139">ASPSMS:</span></span>  
   <span data-ttu-id="d46d2-140">다음 서비스 참조를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-140">The following service reference needs to be added:</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image1.png)  
  
   <span data-ttu-id="d46d2-141">주소:</span><span class="sxs-lookup"><span data-stu-id="d46d2-141">Address:</span></span>  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   <span data-ttu-id="d46d2-142">네임스페이스:</span><span class="sxs-lookup"><span data-stu-id="d46d2-142">Namespace:</span></span>  
    `ASPSMSX2`
3. <span data-ttu-id="d46d2-143">**SMS 공급자 사용자 자격 증명 파악**</span><span class="sxs-lookup"><span data-stu-id="d46d2-143">**Figuring out SMS Provider User credentials**</span></span>  
  
   <span data-ttu-id="d46d2-144">Twilio</span><span class="sxs-lookup"><span data-stu-id="d46d2-144">Twilio:</span></span>  
   <span data-ttu-id="d46d2-145">Twilio 계정의 **대시보드** 탭에서 **계정 SID** 및 **인증 토큰**을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-145">From the **Dashboard** tab of your Twilio account, copy the **Account SID** and **Auth token**.</span></span>  
  
   <span data-ttu-id="d46d2-146">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="d46d2-146">ASPSMS:</span></span>  
   <span data-ttu-id="d46d2-147">계정 설정에서 **Userkey** 로 이동 하 여 자체 정의 된 **암호**와 함께 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-147">From your account settings, navigate to **Userkey** and copy it together with your self-defined **Password**.</span></span>  
  
   <span data-ttu-id="d46d2-148">나중에 `SMSAccountIdentification` 및 `SMSAccountPassword` 변수에 이러한 값을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-148">We will later store these values in the variables `SMSAccountIdentification` and `SMSAccountPassword` .</span></span>
4. <span data-ttu-id="d46d2-149">**SenderID/송신자 지정**</span><span class="sxs-lookup"><span data-stu-id="d46d2-149">**Specifying SenderID / Originator**</span></span>  
  
   <span data-ttu-id="d46d2-150">Twilio</span><span class="sxs-lookup"><span data-stu-id="d46d2-150">Twilio:</span></span>  
   <span data-ttu-id="d46d2-151">**숫자** 탭에서 Twilio 전화 번호를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-151">From the **Numbers** tab, copy your Twilio phone number.</span></span>  
  
   <span data-ttu-id="d46d2-152">ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="d46d2-152">ASPSMS:</span></span>  
   <span data-ttu-id="d46d2-153">**보낸 사람 잠금 해제** 메뉴 내에서 하나 이상의 발신자의 잠금을 해제 하거나 영숫자 송신자 (모든 네트워크에서 지원 되지 않음)를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-153">Within the **Unlock Originators** Menu, unlock one or more Originators or choose an alphanumeric Originator (Not supported by all networks).</span></span>  
  
   <span data-ttu-id="d46d2-154">나중에 `SMSAccountFrom` 변수에이 값을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-154">We will later store this value in the variable `SMSAccountFrom` .</span></span>
5. <span data-ttu-id="d46d2-155">**SMS 공급자 자격 증명을 앱으로 전송**</span><span class="sxs-lookup"><span data-stu-id="d46d2-155">**Transferring SMS provider credentials into app**</span></span>  
  
   <span data-ttu-id="d46d2-156">앱에서 자격 증명 및 발신자 전화 번호를 사용할 수 있도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-156">Make the credentials and sender phone number available to the app:</span></span>

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample1.cs)]

    > [!WARNING]
    > <span data-ttu-id="d46d2-157">보안-중요 한 데이터를 소스 코드에 저장 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-157">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="d46d2-158">예제를 단순하게 유지 하기 위해 위의 코드에 계정 및 자격 증명이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-158">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="d46d2-159">Jon Atten의 [ASP.NET MVC: 소스 제어에서 비공개 설정 유지](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="d46d2-159">See Jon Atten's [ASP.NET MVC: Keep Private Settings Out of Source Control](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx).</span></span>
6. <span data-ttu-id="d46d2-160">**SMS 공급자에 대 한 데이터 전송 구현**</span><span class="sxs-lookup"><span data-stu-id="d46d2-160">**Implementation of data transfer to SMS provider**</span></span>  
  
   <span data-ttu-id="d46d2-161">*앱\_Start\IdentityConfig.cs* 파일에서 `SmsService` 클래스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-161">Configure the `SmsService`  class in the *App\_Start\IdentityConfig.cs* file.</span></span>  
  
   <span data-ttu-id="d46d2-162">사용 된 SMS 공급자에 따라 **Twilio** 또는 기타 **sms** 섹션을 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-162">Depending on the used SMS provider activate either the **Twilio** or the **ASPSMS** section:</span></span> 

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample2.cs)]
7. <span data-ttu-id="d46d2-163">앱을 실행 하 고 이전에 등록 한 계정으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-163">Run the app and log in with the account you previously registered.</span></span>
8. <span data-ttu-id="d46d2-164">`Manage` 컨트롤러에서 `Index` 작업 메서드를 활성화 하는 사용자 ID를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-164">Click on your User ID, which activates the `Index` action method in `Manage` controller.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image2.png)
9. <span data-ttu-id="d46d2-165">추가를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-165">Click Add.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image3.png)
10. <span data-ttu-id="d46d2-166">몇 초 후에 확인 코드를 포함 하는 문자 메시지를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-166">In a few seconds you will get a text message with the verification code.</span></span> <span data-ttu-id="d46d2-167">입력 하 고 **제출**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-167">Enter it and press **Submit**.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image4.png)
11. <span data-ttu-id="d46d2-168">관리 보기에는 전화 번호가 추가 된 것이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-168">The Manage view shows your phone number was added.</span></span>  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image5.png)

### <a name="examine-the-code"></a><span data-ttu-id="d46d2-169">코드 검사</span><span class="sxs-lookup"><span data-stu-id="d46d2-169">Examine the code</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample3.cs?highlight=2)]

<span data-ttu-id="d46d2-170">`Manage` 컨트롤러의 `Index` 작업 메서드는 이전 작업을 기반으로 상태 메시지를 설정 하 고 로컬 암호를 변경 하거나 로컬 계정을 추가할 수 있는 링크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-170">The `Index` action method in `Manage` controller sets the status message based on your previous action and provides links to change your local password or add a local account.</span></span> <span data-ttu-id="d46d2-171">`Index` 메서드는이 브라우저에 대해 상태 또는 2FA 전화 번호, 외부 로그인, 2FA, 2FA, 기억을 2FA 메서드 (뒷부분에서 설명 함)를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-171">The `Index` method also displays the state or your 2FA phone number, external logins, 2FA enabled, and remember 2FA method for this browser(explained later).</span></span> <span data-ttu-id="d46d2-172">제목 표시줄에서 사용자 ID (전자 메일)를 클릭 하면 메시지가 전달 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-172">Clicking on your user ID (email) in the title bar doesn't pass a message.</span></span> <span data-ttu-id="d46d2-173">**전화 번호** 를 클릭 하면 링크 제거 `Message=RemovePhoneSuccess` 쿼리 문자열로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-173">Clicking on the **Phone Number : remove** link passes `Message=RemovePhoneSuccess` as a query string.</span></span>  
  
`https://localhost:44300/Manage?Message=RemovePhoneSuccess`

<span data-ttu-id="d46d2-174">[![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image6.png)]</span><span class="sxs-lookup"><span data-stu-id="d46d2-174">[![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image6.png)]</span></span>

<span data-ttu-id="d46d2-175">`AddPhoneNumber` 작업 메서드는 SMS 메시지를 받을 수 있는 전화 번호를 입력할 수 있는 대화 상자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-175">The `AddPhoneNumber` action method displays a dialog box to enter a phone number that can receive SMS messages.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample4.cs)]

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image7.png)

<span data-ttu-id="d46d2-176">**확인 코드 보내기** 단추를 클릭 하면 전화 번호가 HTTP POST `AddPhoneNumber` 작업 메서드에 게시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-176">Clicking on the **Send verification code** button posts the phone number to the HTTP POST `AddPhoneNumber` action method.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample5.cs?highlight=12)]

<span data-ttu-id="d46d2-177">`GenerateChangePhoneNumberTokenAsync` 메서드는 SMS 메시지에 설정 되는 보안 토큰을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-177">The `GenerateChangePhoneNumberTokenAsync` method generates the security token which will be set in the SMS message.</span></span> <span data-ttu-id="d46d2-178">SMS 서비스가 구성 된 경우 토큰은 &quot;문자열로 전송 됩니다. 보안 코드는 &quot;&gt;&lt;토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-178">If the SMS service has been configured, the token is sent as the string &quot;Your security code is &lt;token&gt;&quot;.</span></span> <span data-ttu-id="d46d2-179">`SmsService.SendAsync` 메서드가 비동기적으로 호출 되 면 앱이 `VerifyPhoneNumber` 작업 메서드로 리디렉션됩니다 (다음 대화 상자 표시). 그러면 확인 코드를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-179">The `SmsService.SendAsync` method to is called asynchronously, then the app is redirected to the `VerifyPhoneNumber` action method (which displays the following dialog), where you can enter the verification code.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image8.png)

<span data-ttu-id="d46d2-180">코드를 입력 하 고 제출을 클릭 하면 코드가 HTTP POST `VerifyPhoneNumber` 작업 메서드에 게시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-180">Once you enter the code and click submit, the code is posted to the HTTP POST `VerifyPhoneNumber` action method.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample6.cs)]

<span data-ttu-id="d46d2-181">`ChangePhoneNumberAsync` 메서드는 게시 된 보안 코드를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-181">The `ChangePhoneNumberAsync` method checks the posted security code.</span></span> <span data-ttu-id="d46d2-182">코드가 올바르면 전화 번호가 `AspNetUsers` 테이블의 `PhoneNumber` 필드에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-182">If the code is correct, the phone number is added to the `PhoneNumber` field of the `AspNetUsers` table.</span></span> <span data-ttu-id="d46d2-183">호출에 성공 하면 `SignInAsync` 메서드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-183">If that call is successful, the `SignInAsync` method is called:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample7.cs)]

<span data-ttu-id="d46d2-184">`isPersistent` 매개 변수는 인증 세션이 여러 요청에서 지속 되는지 여부를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-184">The `isPersistent` parameter sets whether the authentication session is persisted across multiple requests.</span></span>

<span data-ttu-id="d46d2-185">보안 프로필을 변경 하면 새 보안 스탬프가 생성 되어 *AspNetUsers* 테이블의 `SecurityStamp` 필드에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-185">When you change your security profile, a new security stamp is generated and stored in the `SecurityStamp` field of the *AspNetUsers* table.</span></span> <span data-ttu-id="d46d2-186">`SecurityStamp` 필드는 보안 쿠키와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-186">Note, the `SecurityStamp` field is different from the security cookie.</span></span> <span data-ttu-id="d46d2-187">보안 쿠키는 `AspNetUsers` 테이블 (또는 Identity DB의 다른 위치)에 저장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-187">The security cookie is not stored in the `AspNetUsers` table (or anywhere else in the Identity DB).</span></span> <span data-ttu-id="d46d2-188">보안 쿠키 토큰은 [DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx) 를 사용 하 여 자체 서명 되며 `UserId, SecurityStamp` 및 만료 시간 정보를 사용 하 여 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-188">The security cookie token is self-signed using [DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx) and is created with the `UserId, SecurityStamp` and expiration time information.</span></span>

<span data-ttu-id="d46d2-189">쿠키 미들웨어는 각 요청에서 쿠키를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-189">The cookie middleware checks the cookie on each request.</span></span> <span data-ttu-id="d46d2-190">`Startup` 클래스의 `SecurityStampValidator` 메서드는 DB에 적중 하 고 `validateInterval`에 지정 된 대로 주기적으로 보안 스탬프를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-190">The `SecurityStampValidator` method in the `Startup` class hits the DB and checks security stamp periodically, as specified with the `validateInterval`.</span></span> <span data-ttu-id="d46d2-191">이는 보안 프로필을 변경 하지 않는 한 30 분 마다 (이 샘플에서) 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-191">This only happens every 30 minutes (in our sample) unless you change your security profile.</span></span> <span data-ttu-id="d46d2-192">데이터베이스에 대 한 왕복을 최소화 하기 위해 30 분 간격을 선택 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-192">The 30 minute interval was chosen to minimize trips to the database.</span></span>

<span data-ttu-id="d46d2-193">보안 프로필을 변경 하는 경우 `SignInAsync` 메서드를 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-193">The `SignInAsync` method needs to be called when any change is made to the security profile.</span></span> <span data-ttu-id="d46d2-194">보안 프로필이 변경 되 면 데이터베이스는 `SecurityStamp` 필드를 업데이트 하 고 `SignInAsync` 메서드를 호출 하지 않으면 다음에 OWIN 파이프라인이 데이터베이스 (`validateInterval`)에 *도달할 때 까지만* 로그인 상태를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-194">When the security profile changes, the database is updates the `SecurityStamp` field, and without calling the `SignInAsync` method you would stay logged in *only* until the next time the OWIN pipeline hits the database (the `validateInterval`).</span></span> <span data-ttu-id="d46d2-195">즉시 반환 되도록 `SignInAsync` 메서드를 변경 하 고 쿠키 `validateInterval` 속성을 30 분에서 5 초로 설정 하 여이를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-195">You can test this by changing the `SignInAsync` method to return immediately, and setting the cookie `validateInterval` property from 30 minutes to 5 seconds:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample8.cs?highlight=3)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample9.cs?highlight=20-21)]

<span data-ttu-id="d46d2-196">위의 코드를 변경 하면 보안 프로필을 변경할 수 있습니다. 예를 들어 **두 가지 요소를 사용 하도록 설정한**상태를 변경 하 여 보안 프로필을 변경할 수 있으며, `SecurityStampValidator.OnValidateIdentity` 메서드가 실패 하면 5 초 이내에 로그 아웃 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-196">With the above code changes, you can change your security profile (for example, by changing the state of **Two Factor Enabled**) and you will be logged out in 5 seconds when the `SecurityStampValidator.OnValidateIdentity` method fails.</span></span> <span data-ttu-id="d46d2-197">`SignInAsync` 메서드에서 반환 줄을 제거 하 고 다른 보안 프로필을 변경 하 고 로그 아웃 하지 않습니다. `SignInAsync` 메서드는 새 보안 쿠키를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-197">Remove the return line in the `SignInAsync` method, make another security profile change and you will not be logged out. The `SignInAsync` method generates a new security cookie.</span></span>

<a id="enable2"></a>

## <a name="enable-two-factor-authentication"></a><span data-ttu-id="d46d2-198">2 단계 인증을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="d46d2-198">Enable two-factor authentication</span></span>

<span data-ttu-id="d46d2-199">샘플 앱에서 2 단계 인증 (2FA)을 사용 하도록 설정 하려면 UI를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-199">In the sample app, you need to use the UI to enable two-factor authentication (2FA).</span></span> <span data-ttu-id="d46d2-200">2FA를 사용 하도록 설정 하려면 탐색 모음에서 사용자 ID (전자 메일 별칭)를 클릭 합니다.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="d46d2-200">To enable 2FA, click on your user ID (email alias) in the navigation bar.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image9.png)</span></span>  
<span data-ttu-id="d46d2-201">2FA 사용을 클릭 합니다.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="d46d2-201">Click on enable 2FA.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image10.png)</span></span> <span data-ttu-id="d46d2-202">로그 아웃 한 다음 다시 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-202">Log out, then log back in.</span></span> <span data-ttu-id="d46d2-203">전자 메일을 사용 하도록 설정한 경우 ( [이전 자습서](account-confirmation-and-password-recovery-with-aspnet-identity.md)참조) 2FA의 SMS 또는 전자 메일을 선택할 수 있습니다.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="d46d2-203">If you've enabled email (see my [previous tutorial](account-confirmation-and-password-recovery-with-aspnet-identity.md)), you can select the SMS or email for 2FA.![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image11.png)</span></span> <span data-ttu-id="d46d2-204">코드를 입력할 수 있는 코드 확인 페이지가 표시 됩니다 (SMS 또는 전자 메일에서).![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="d46d2-204">The Verify Code page is displayed where you can enter the code (from SMS or email).![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image12.png)</span></span> <span data-ttu-id="d46d2-205">**이 브라우저 기억을** 확인란을 클릭 하면 해당 컴퓨터 및 브라우저를 사용 하 여 로그온 하는 데 2fa를 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-205">Clicking on the **Remember this browser** check box will exempt you from needing to use 2FA to log on with that computer and browser.</span></span> <span data-ttu-id="d46d2-206">2FA를 사용 하도록 설정 하 고 **이 브라우저** 를 클릭 하면 컴퓨터에 액세스할 수 없는 한 악의적인 사용자가 계정에 액세스 하는 것과 같은 강력한 2fa 보호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-206">Enabling 2FA and clicking on the **Remember this browser** will provide you with strong 2FA protection from malicious users trying to access your account, as long as they don't have access to your computer.</span></span> <span data-ttu-id="d46d2-207">정기적으로 사용 하는 모든 개인 컴퓨터에서이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-207">You can do this on any private machine you regularly use.</span></span> <span data-ttu-id="d46d2-208">**이 브라우저 기억을**설정 하면 정기적으로 사용 하지 않는 컴퓨터에서 2fa의 보안을 강화 하 고, 사용자 컴퓨터에서 2fa를 거치지 않아도 편리 하 게 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-208">By setting **Remember this browser**, you get the added security of 2FA from computers you don't regularly use, and you get the convenience on not having to go through 2FA on your own computers.</span></span> 

<a id="reg"></a>
## <a name="how-to-register-a-two-factor-authentication-provider"></a><span data-ttu-id="d46d2-209">2 단계 인증 공급자를 등록 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d46d2-209">How to register a Two-factor authentication provider</span></span>

<span data-ttu-id="d46d2-210">새 MVC 프로젝트를 만들 때 *IdentityConfig.cs* 파일에는 2 단계 인증 공급자를 등록 하는 다음 코드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-210">When you create a new MVC project, the *IdentityConfig.cs* file contains the following code to register a Two-factor authentication provider:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample10.cs?highlight=22-35)]

## <a name="add-a-phone-number-for-2fa"></a><span data-ttu-id="d46d2-211">2FA의 전화 번호 추가</span><span class="sxs-lookup"><span data-stu-id="d46d2-211">Add a phone number for 2FA</span></span>

<span data-ttu-id="d46d2-212">`Manage` 컨트롤러의 `AddPhoneNumber` 작업 메서드는 보안 토큰을 생성 하 고 사용자가 제공한 전화 번호로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-212">The `AddPhoneNumber` action method in the `Manage` controller generates a security token and sends it to the phone number you have provided.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample11.cs)]

<span data-ttu-id="d46d2-213">토큰을 보낸 후에는 `VerifyPhoneNumber` 작업 메서드로 리디렉션하고 2FA에 SMS를 등록 하는 코드를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-213">After sending the token, it redirects to the `VerifyPhoneNumber` action method, where you can enter the code to register SMS for 2FA.</span></span> <span data-ttu-id="d46d2-214">SMS 2FA는 전화 번호를 확인할 때까지 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-214">SMS 2FA is not used until you have verified the phone number.</span></span>

## <a name="enabling-2fa"></a><span data-ttu-id="d46d2-215">2FA 사용</span><span class="sxs-lookup"><span data-stu-id="d46d2-215">Enabling 2FA</span></span>

<span data-ttu-id="d46d2-216">`EnableTFA` 작업 메서드는 2FA를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-216">The `EnableTFA` action method enables 2FA:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample12.cs)]

<span data-ttu-id="d46d2-217">사용 2FA가 보안 프로필에 대 한 변경 이기 때문에 `SignInAsync`를 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-217">Note the `SignInAsync` must be called because enable 2FA is a change to the security profile.</span></span> <span data-ttu-id="d46d2-218">2FA를 사용 하도록 설정한 경우 사용자가 등록 한 2FA 접근 방식 (샘플의 SMS 및 전자 메일)을 사용 하 여 2FA를 사용 하 여 로그인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-218">When 2FA is enabled, the user will need to use 2FA to log in, using the 2FA approaches they have registered (SMS and email in the sample).</span></span>

<span data-ttu-id="d46d2-219">QR 코드 생성기와 같은 2 개의 FA 공급자를 추가 하거나 직접 작성할 수 있습니다 ( [ASP.NET Identity에서 Google 인증자 사용](https://www.jerriepelser.com//blog/using-google-authenticator-asp-net-identity/)참조).</span><span class="sxs-lookup"><span data-stu-id="d46d2-219">You can add more 2FA providers such as QR code generators or you can write you own (See [Using Google Authenticator with ASP.NET Identity](https://www.jerriepelser.com//blog/using-google-authenticator-asp-net-identity/)).</span></span>

> [!NOTE]
> <span data-ttu-id="d46d2-220">2FA 코드는 [시간 기반 일회용 암호 알고리즘](http://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm) 을 사용 하 여 생성 되 고 코드는 6 분 동안 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-220">The 2FA codes are generated using [Time-based One-time Password Algorithm](http://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm) and codes are valid for six minutes.</span></span> <span data-ttu-id="d46d2-221">코드를 입력 하는 데 6 분 이상 소요 되 면 잘못 된 코드 오류 메시지를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-221">If you take more than six minutes to enter the code, you'll get an Invalid code error message.</span></span>

<a id="combine"></a>

## <a name="combine-social-and-local-login-accounts"></a><span data-ttu-id="d46d2-222">소셜 및 로컬 로그인 계정 결합</span><span class="sxs-lookup"><span data-stu-id="d46d2-222">Combine social and local login accounts</span></span>

<span data-ttu-id="d46d2-223">전자 메일 링크를 클릭 하 여 로컬 및 소셜 계정을 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-223">You can combine local and social accounts by clicking on your email link.</span></span> <span data-ttu-id="d46d2-224">다음 시퀀스 &quot;RickAndMSFT@gmail.com&quot; 먼저 로컬 로그인으로 만들어지므로 먼저 계정을 소셜 로그인으로 만든 다음 로컬 로그인을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-224">In the following sequence &quot;RickAndMSFT@gmail.com&quot; is first created as a local login, but you can create the account as a social log in first, then add a local login.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image13.png)

<span data-ttu-id="d46d2-225">**관리** 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-225">Click on the **Manage** link.</span></span> <span data-ttu-id="d46d2-226">이 계정과 연결 된 0 외부 (소셜 로그인)를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-226">Note the 0 external (social logins) associated with this account.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image14.png)

<span data-ttu-id="d46d2-227">다른 로그인 서비스에 대 한 링크를 클릭 하 고 앱 요청을 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-227">Click the link to another log in service and accept the app requests.</span></span> <span data-ttu-id="d46d2-228">두 계정을 결합 하 여 두 계정을 사용 하 여 로그온 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-228">The two accounts have been combined, you will be able to log on with either account.</span></span> <span data-ttu-id="d46d2-229">인증 서비스의 소셜 로그인이 다운 되거나 소셜 계정에 대 한 액세스 권한이 손실 될 가능성이 있는 경우 사용자가 로컬 계정을 추가 하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-229">You might want your users to add local accounts in case their social log in authentication service is down, or more likely they have lost access to their social account.</span></span>

<span data-ttu-id="d46d2-230">다음 그림에서 Tom은 **외부 로그인** 에서 볼 수 있는 소셜 로그인입니다. 1은 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-230">In the following image, Tom is a social log in (which you can see from the **External Logins: 1** shown on the page).</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image15.png)

<span data-ttu-id="d46d2-231">**암호 선택** 을 클릭 하면 동일한 계정에 연결 된 로컬 로그를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-231">Clicking on **Pick a password** allows you to add a local log on associated with the same account.</span></span>

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image16.png)

<a id="lock"></a>

## <a name="account-lockout-from-brute-force-attacks"></a><span data-ttu-id="d46d2-232">무차별 암호 대입 공격 으로부터 계정 잠금</span><span class="sxs-lookup"><span data-stu-id="d46d2-232">Account lockout from brute force attacks</span></span>

<span data-ttu-id="d46d2-233">사용자 잠금을 사용 하도록 설정 하 여 사전 공격 으로부터 앱 계정을 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-233">You can protect the accounts on your app from dictionary attacks by enabling user lockout.</span></span> <span data-ttu-id="d46d2-234">`ApplicationUserManager Create` 메서드의 다음 코드는 잠금 해제를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-234">The following code in the `ApplicationUserManager Create` method configures lock out:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample13.cs)]

<span data-ttu-id="d46d2-235">위의 코드는 2 단계 인증에 대해서만 잠금을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-235">The code above enables lockout for two factor authentication only.</span></span> <span data-ttu-id="d46d2-236">계정 컨트롤러의 `Login` 메서드에서 `shouldLockout`를 true로 변경 하 여 로그인 잠금을 설정할 수 있지만 계정이 [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) 로그인 공격에 취약 하기 때문에 로그인에 대 한 잠금을 사용 하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-236">While you can enable lock out for logins by changing `shouldLockout` to true in the `Login` method of the account controller, we recommend you not enable lock out for logins because it makes the account susceptible to [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) login attacks.</span></span> <span data-ttu-id="d46d2-237">샘플 코드에서는 `ApplicationDbInitializer Seed` 메서드에서 만든 관리자 계정에 대해 잠금이 사용 하지 않도록 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-237">In the sample code, lockout is disabled for the admin account created in the `ApplicationDbInitializer Seed` method:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample14.cs?highlight=19)]

## <a name="requiring-a-user-to-have-a-validated-email-account"></a><span data-ttu-id="d46d2-238">사용자에 게 유효성을 검사 한 전자 메일 계정 필요</span><span class="sxs-lookup"><span data-stu-id="d46d2-238">Requiring a user to have a validated email account</span></span>

<span data-ttu-id="d46d2-239">다음 코드에서는 사용자가 로그인 하기 전에 유효성을 검사 한 전자 메일 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-239">The following code requires a user to have a validated email account before they can log in:</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample15.cs?highlight=8-17)]

## <a name="how-signinmanager-checks-for-2fa-requirement"></a><span data-ttu-id="d46d2-240">SignInManager에서 2FA 요구 사항을 확인 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d46d2-240">How SignInManager checks for 2FA requirement</span></span>

<span data-ttu-id="d46d2-241">로컬 로그인과 소셜 로그인은 모두 2FA가 사용 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-241">Both the local log in and social log in check to see if 2FA is enabled.</span></span> <span data-ttu-id="d46d2-242">2FA를 사용 하는 경우 `SignInManager` logon 메서드가 `SignInStatus.RequiresVerification`를 반환 하 고 사용자가 `SendCode` 작업 메서드로 리디렉션됩니다. 여기서 사용자는 코드를 입력 하 여 로그를 순서 대로 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-242">If 2FA is enabled, the `SignInManager` logon method returns `SignInStatus.RequiresVerification`, and the user will be redirected to the `SendCode` action method, where they will have to enter the code to complete the log in sequence.</span></span> <span data-ttu-id="d46d2-243">사용자가 사용자 로컬 쿠키에 대해 RememberMe를 설정 하는 경우 `SignInManager`은 `SignInStatus.Success`을 반환 하 고 2FA를 통과 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-243">If the user has RememberMe is set on the users local cookie, the `SignInManager` will return `SignInStatus.Success` and they will not have to go through 2FA.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample16.cs?highlight=20-22)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample17.cs?highlight=10-11,17-18)]

<span data-ttu-id="d46d2-244">다음 코드에서는 `SendCode` 작업 메서드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-244">The following code shows the `SendCode` action method.</span></span> <span data-ttu-id="d46d2-245">[Selectlistitem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) 은 사용자에 대해 사용 하도록 설정 된 모든 2fa 메서드를 사용 하 여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-245">A [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) is created with all the 2FA methods enabled for the user.</span></span> <span data-ttu-id="d46d2-246">[Selectlistitem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) 은 [DropDownListFor](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist.aspx) 도우미에 전달 되며,이를 통해 사용자는 2fa 접근 방식 (일반적으로 메일 및 SMS)을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-246">The [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) is passed to the [DropDownListFor](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist.aspx) helper, which allows the user to select the 2FA approach (typically email and SMS).</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample18.cs)]

<span data-ttu-id="d46d2-247">사용자가 2FA 방법을 게시 하면 `HTTP POST SendCode` 동작 메서드가 호출 되 고, `SignInManager`는 2FA 코드를 보내고, 사용자는 코드를 입력 하 여 로그인을 완료할 수 있는 `VerifyCode` 작업 메서드로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-247">Once the user posts the 2FA approach, the `HTTP POST SendCode` action method is called, the `SignInManager` sends the 2FA code, and the user is redirected to the `VerifyCode` action method where they can enter the code to complete the log in.</span></span>

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample19.cs?highlight=3,13-14,18)]

## <a name="2fa-lockout"></a><span data-ttu-id="d46d2-248">2FA 잠금</span><span class="sxs-lookup"><span data-stu-id="d46d2-248">2FA Lockout</span></span>

<span data-ttu-id="d46d2-249">로그인 암호 시도 실패 시 계정 잠금을 설정할 수 있지만이 방법을 사용 하면 로그인이 [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) 잠금에 취약 해질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-249">Although you can set account lockout on login password attempt failures, that approach makes your login susceptible to [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) lockouts.</span></span> <span data-ttu-id="d46d2-250">2FA와만 계정 잠금을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-250">We recommend you use account lockout only with 2FA.</span></span> <span data-ttu-id="d46d2-251">`ApplicationUserManager` 만들어지면 샘플 코드는 2FA 잠금과 `MaxFailedAccessAttemptsBeforeLockout`를 5로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-251">When the `ApplicationUserManager` is created, the sample code sets 2FA lockout and `MaxFailedAccessAttemptsBeforeLockout` to five.</span></span> <span data-ttu-id="d46d2-252">사용자가 로컬 계정 또는 소셜 계정을 통해 로그인 하면 2FA에서 실패 한 각 시도가 저장 되 고, 최대 시도 횟수에 도달 하면 사용자가 5 분 동안 잠깁니다 (잠금 시간을 `DefaultAccountLockoutTimeSpan`로 설정할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="d46d2-252">Once a user logs in (through local account or social account), each failed attempt at 2FA is stored, and if the maximum attempts is reached, the user is locked out for five minutes (you can set the lock out time with `DefaultAccountLockoutTimeSpan`).</span></span>

<a id="addRes"></a>

## <a name="additional-resources"></a><span data-ttu-id="d46d2-253">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="d46d2-253">Additional Resources</span></span>

- <span data-ttu-id="d46d2-254">[권장 리소스 ASP.NET Identity](../getting-started/aspnet-identity-recommended-resources.md) Id 블로그, 비디오, 자습서 등의 전체 목록과 유용한 링크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-254">[ASP.NET Identity Recommended Resources](../getting-started/aspnet-identity-recommended-resources.md) Complete list of Identity blogs, videos, tutorials and great SO links.</span></span>
- <span data-ttu-id="d46d2-255">[Facebook, Twitter, LinkedIn 및 Google OAuth2 sign-on이 포함 된 MVC 5 앱](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 은 사용자 테이블에 프로필 정보를 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-255">[MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) also shows how to add profile information to the users table.</span></span>
- <span data-ttu-id="d46d2-256">[ASP.NET MVC 및 id 2.0: John Atten의 기본 사항을 이해](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx) 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-256">[ASP.NET MVC and Identity 2.0: Understanding the Basics](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx) by John Atten.</span></span>
- [<span data-ttu-id="d46d2-257">계정 확인 및 암호 복구 ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="d46d2-257">Account Confirmation and Password Recovery with ASP.NET Identity</span></span>](account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [<span data-ttu-id="d46d2-258">ASP.NET ID 소개</span><span class="sxs-lookup"><span data-stu-id="d46d2-258">Introduction to ASP.NET Identity</span></span>](../getting-started/introduction-to-aspnet-identity.md)
- <span data-ttu-id="d46d2-259">Pranav Rastogi가 [ASP.NET Identity 2.0.0의 RTM을 발표](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-259">[Announcing RTM of ASP.NET Identity 2.0.0](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) by Pranav Rastogi.</span></span>
- <span data-ttu-id="d46d2-260">[ASP.NET Identity 2.0: John Atten에서 계정 유효성 검사 및 2 단계 권한 부여를 설정](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46d2-260">[ASP.NET Identity 2.0: Setting Up Account Validation and Two-Factor Authorization](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) by John Atten.</span></span>
