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
# <a name="create-a-secure-aspnet-mvc-5-web-app-with-log-in-email-confirmation-and-password-reset-c"></a><span data-ttu-id="6c999-104">로그인, 전자 메일 확인 및 암호 재설정 기능이 있는 보안 ASP.NET MVC 5 웹앱 만들기(C#)</span><span class="sxs-lookup"><span data-stu-id="6c999-104">Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset (C#)</span></span>

<span data-ttu-id="6c999-105">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="6c999-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="6c999-106">이 자습서에서는 ASP.NET Identity 멤버 자격 시스템을 사용 하 여 전자 메일 확인 및 암호 재설정으로 ASP.NET MVC 5 웹 앱을 빌드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-106">This tutorial shows you how to build an ASP.NET MVC 5 web app with email confirmation and password reset using the ASP.NET Identity membership system.</span></span>

<span data-ttu-id="6c999-107">.NET Core를 사용 하는이 자습서의 업데이트 된 버전은 [ASP.NET Core의 계정 확인 및 암호 복구](/aspnet/core/security/authentication/accconfirm)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="6c999-107">For an updated version of this tutorial that uses .NET Core, see [Account confirmation and password recovery in ASP.NET Core](/aspnet/core/security/authentication/accconfirm).</span></span>

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a><span data-ttu-id="6c999-108">ASP.NET MVC 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="6c999-108">Create an ASP.NET MVC app</span></span>

<span data-ttu-id="6c999-109">웹 또는 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) [에 대해 Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 을 설치 하 고 실행 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-109">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="6c999-110">[Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 이상을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-110">Install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="6c999-111">경고:이 자습서를 완료 하려면 [Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 이상을 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-111">Warning: You must install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher to complete this tutorial.</span></span>

1. <span data-ttu-id="6c999-112">새 ASP.NET 웹 프로젝트를 만들고 MVC 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-112">Create a new ASP.NET Web project and select the MVC template.</span></span> <span data-ttu-id="6c999-113">Web Forms는 ASP.NET Identity도 지원 하므로 web Forms 앱에서 비슷한 단계를 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-113">Web Forms also supports ASP.NET Identity, so you could follow similar steps in a web forms app.</span></span>  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image1.png)
2. <span data-ttu-id="6c999-114">기본 인증을 **개별 사용자 계정**으로 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-114">Leave the default authentication as **Individual User Accounts**.</span></span> <span data-ttu-id="6c999-115">Azure에서 앱을 호스팅하려면 확인란을 선택 된 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-115">If you'd like to host the app in Azure, leave the check box checked.</span></span> <span data-ttu-id="6c999-116">이 자습서의 뒷부분에서는 Azure에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-116">Later in the tutorial we will deploy to Azure.</span></span> <span data-ttu-id="6c999-117">[Azure 계정을 무료로 열](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-117">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
3. <span data-ttu-id="6c999-118">[SSL을 사용 하도록 프로젝트](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-118">Set the [project to use SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>
4. <span data-ttu-id="6c999-119">앱을 실행 하 고 **등록** 링크를 클릭 한 다음 사용자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-119">Run the app, click the **Register** link and register a user.</span></span> <span data-ttu-id="6c999-120">이때 전자 메일에 대 한 유일한 유효성 검사는 [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) 특성을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-120">At this point, the only validation on the email is with the [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) attribute.</span></span>
5. <span data-ttu-id="6c999-121">서버 탐색기에서 **데이터 Connections\DefaultConnection\Tables\AspNetUsers**로 이동 하 고 마우스 오른쪽 단추를 클릭 한 다음 **테이블 정의 열기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-121">In Server Explorer, navigate to **Data Connections\DefaultConnection\Tables\AspNetUsers**, right click and select **Open table definition**.</span></span>

    <span data-ttu-id="6c999-122">다음 이미지는 `AspNetUsers` 스키마를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-122">The following image shows the `AspNetUsers` schema:</span></span>

    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image2.png)
6. <span data-ttu-id="6c999-123">**AspNetUsers** 테이블을 마우스 오른쪽 단추로 클릭 하 고 **테이블 데이터 표시**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-123">Right click on the **AspNetUsers** table and select **Show Table Data**.</span></span>  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image3.png)  
 <span data-ttu-id="6c999-124">이 시점에서 전자 메일이 확인 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-124">At this point the email has not been confirmed.</span></span>
7. <span data-ttu-id="6c999-125">행을 클릭 하 고 삭제를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-125">Click on the row and select delete.</span></span> <span data-ttu-id="6c999-126">다음 단계에서이 전자 메일을 다시 추가 하 고 확인 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-126">You'll add this email again in the next step, and send a confirmation email.</span></span>

## <a name="email-confirmation"></a><span data-ttu-id="6c999-127">전자 메일 확인</span><span class="sxs-lookup"><span data-stu-id="6c999-127">Email confirmation</span></span>

<span data-ttu-id="6c999-128">새 사용자 등록의 전자 메일을 확인 하 여 다른 사용자를 가장 하지 않았는지 확인 하는 것이 좋습니다. 즉, 다른 사용자의 전자 메일을 사용 하 여 등록 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-128">It's a best practice to confirm the email of a new user registration to verify they are not impersonating someone else (that is, they haven't registered with someone else's email).</span></span> <span data-ttu-id="6c999-129">토론 포럼이 있다고 가정 하면 `"bob@example.com"` `"joe@contoso.com"`등록 하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-129">Suppose you had a discussion forum, you would want to prevent `"bob@example.com"` from registering as `"joe@contoso.com"`.</span></span> <span data-ttu-id="6c999-130">전자 메일 확인 없이 앱에서 원치 않는 전자 메일을 받을 수 `"joe@contoso.com"`.</span><span class="sxs-lookup"><span data-stu-id="6c999-130">Without email confirmation, `"joe@contoso.com"` could get unwanted email from your app.</span></span> <span data-ttu-id="6c999-131">Bob이 실수로 `"bib@example.com"`로 등록 했다고 가정 하면 앱이 올바른 전자 메일을가지고 있지 않기 때문에 암호 복구를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-131">Suppose Bob accidentally registered as `"bib@example.com"` and hadn't noticed it, he wouldn't be able to use password recover because the app doesn't have his correct email.</span></span> <span data-ttu-id="6c999-132">전자 메일 확인은 봇의 제한 된 보호만 제공 하며, 결정 된 스팸 메일을 보호 하는 것을 제공 하지 않으며 등록 하는 데 사용할 수 있는 많은 작업 메일 별칭이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-132">Email confirmation provides only limited protection from bots and doesn't provide protection from determined spammers, they have many working email aliases they can use to register.</span></span>

<span data-ttu-id="6c999-133">일반적으로 새 사용자가 전자 메일, SMS 문자 메시지 또는 다른 메커니즘을 통해 확인 되기 전에 데이터를 웹 사이트에 게시 하는 것을 방지 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-133">You generally want to prevent new users from posting any data to your web site before they have been confirmed by email, a SMS text message or another mechanism.</span></span> <a id="build"></a><span data-ttu-id="6c999-134">아래 섹션에서는 전자 메일 확인을 사용 하도록 설정 하 고 코드를 수정 하 여 새로 등록 된 사용자가 전자 메일을 확인 한 후에 로그인 하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-134">In the sections below, we will enable email confirmation and modify the code to prevent newly registered users from logging in until their email has been confirmed.</span></span>

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a><span data-ttu-id="6c999-135">SendGrid 후크</span><span class="sxs-lookup"><span data-stu-id="6c999-135">Hook up SendGrid</span></span>

<span data-ttu-id="6c999-136">이 섹션의 지침은 최신이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-136">The instructions in this section are not current.</span></span> <span data-ttu-id="6c999-137">업데이트 된 지침은 [SendGrid 전자 메일 공급자 구성](/aspnet/core/security/authentication/accconfirm#configure-email-provider) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="6c999-137">See [Configure SendGrid email provider](/aspnet/core/security/authentication/accconfirm#configure-email-provider) for updated instructions.</span></span>

<span data-ttu-id="6c999-138">이 자습서에서는 [SendGrid](http://sendgrid.com/)를 통해 전자 메일 알림을 추가 하는 방법을 보여 주지만 SMTP 및 기타 메커니즘을 사용 하 여 전자 메일을 보낼 수 있습니다 ( [추가 리소스](#addRes)참조).</span><span class="sxs-lookup"><span data-stu-id="6c999-138">Although this tutorial only shows how to add email notification through [SendGrid](http://sendgrid.com/), you can send email using SMTP and other mechanisms (see [additional resources](#addRes)).</span></span>

1. <span data-ttu-id="6c999-139">패키지 관리자 콘솔에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-139">In the Package Manager Console, enter the following command:</span></span> 

    [!code-console[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample1.cmd)]
2. <span data-ttu-id="6c999-140">[Azure SendGrid 등록 페이지로](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409) 이동 하 여 무료 SendGrid 계정에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-140">Go to the [Azure SendGrid sign up page](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409) and register for a free SendGrid account.</span></span> <span data-ttu-id="6c999-141">*App_Start/identityconfig.cs*에서 다음과 비슷한 코드를 추가 하 여 SendGrid를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-141">Configure SendGrid by adding code similar to the following in *App_Start/IdentityConfig.cs*:</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample2.cs?highlight=3,5)]

<span data-ttu-id="6c999-142">다음 포함을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-142">You'll need to add the following includes:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample3.cs)]

<span data-ttu-id="6c999-143">이 샘플을 간단 하 게 유지 하기 위해 web.config 파일에 응용 프로그램 설정을 *저장 합니다.*</span><span class="sxs-lookup"><span data-stu-id="6c999-143">To keep this sample simple, we'll store the app settings in the *web.config* file:</span></span>

[!code-xml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample4.xml)]

> [!WARNING]
> <span data-ttu-id="6c999-144">보안-중요 한 데이터를 소스 코드에 저장 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-144">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="6c999-145">계정 및 자격 증명은 appSetting에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-145">The account and credentials are stored in the appSetting.</span></span> <span data-ttu-id="6c999-146">Azure에서 Azure Portal의 **[구성](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** 탭에서 이러한 값을 안전 하 게 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-146">On Azure, you can securely store these values on the **[Configure](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** tab in the Azure portal.</span></span> <span data-ttu-id="6c999-147">[암호 및 기타 중요 한 데이터를 ASP.NET 및 Azure에 배포 하는 방법에 대 한 모범 사례](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="6c999-147">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>

### <a name="enable-email-confirmation-in-the-account-controller"></a><span data-ttu-id="6c999-148">계정 컨트롤러에서 전자 메일 확인 사용</span><span class="sxs-lookup"><span data-stu-id="6c999-148">Enable email confirmation in the Account controller</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample5.cs?highlight=16-21)]

<span data-ttu-id="6c999-149">*Views\Account\ConfirmEmail.cshtml* 파일에 올바른 razor 구문이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-149">Verify the *Views\Account\ConfirmEmail.cshtml* file has correct razor syntax.</span></span> <span data-ttu-id="6c999-150">첫 번째 줄의 @ 문자가 없을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-150">( The @ character in the first line might be missing.</span></span> <span data-ttu-id="6c999-151">)</span><span class="sxs-lookup"><span data-stu-id="6c999-151">)</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample6.cshtml?highlight=1)]

<span data-ttu-id="6c999-152">앱을 실행 하 고 등록 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-152">Run the app and click the Register link.</span></span> <span data-ttu-id="6c999-153">등록 양식을 제출 하면 로그인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-153">Once you submit the registration form, you are logged in.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image4.png)

<span data-ttu-id="6c999-154">전자 메일 계정을 확인 하 고 링크를 클릭 하 여 전자 메일을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-154">Check your email account and click on the link to confirm your email.</span></span>

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a><span data-ttu-id="6c999-155">로그인 하기 전에 전자 메일 확인 필요</span><span class="sxs-lookup"><span data-stu-id="6c999-155">Require email confirmation before log in</span></span>

<span data-ttu-id="6c999-156">현재 사용자가 등록 양식을 완료 하면 로그인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-156">Currently once a user completes the registration form, they are logged in.</span></span> <span data-ttu-id="6c999-157">일반적으로에 로그인 하기 전에 전자 메일을 확인 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-157">You generally want to confirm their email before logging them in.</span></span> <span data-ttu-id="6c999-158">아래 섹션에는 새 사용자가 로그인 (인증 됨) 전에 확인 된 전자 메일을 포함 하도록 코드를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-158">In the section below, we will modify the code to require new users to have a confirmed email before they are logged in (authenticated).</span></span> <span data-ttu-id="6c999-159">`HttpPost Register` 메서드를 다음과 같이 강조 표시 된 변경 내용으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-159">Update the `HttpPost Register` method with the following highlighted changes:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample7.cs?highlight=14-15,23-30)]

<span data-ttu-id="6c999-160">`SignInAsync` 메서드를 주석으로 처리 하면 등록을 통해 사용자에 게 로그인 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-160">By commenting out the `SignInAsync` method, the user will not be signed in by the registration.</span></span> <span data-ttu-id="6c999-161">`TempData["ViewBagLink"] = callbackUrl;` 줄을 사용 하 여 전자 메일을 보내지 않고 [앱을 디버깅](#dbg) 하 고 등록을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-161">The `TempData["ViewBagLink"] = callbackUrl;` line can be used to [debug the app](#dbg) and test registration without sending email.</span></span> <span data-ttu-id="6c999-162">`ViewBag.Message`은 확인 지침을 표시 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-162">`ViewBag.Message` is used to display the confirm instructions.</span></span> <span data-ttu-id="6c999-163">[다운로드 샘플](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952) 에는 전자 메일을 설정 하지 않고 전자 메일 확인을 테스트 하는 코드가 포함 되어 있으며,이를 사용 하 여 응용 프로그램을 디버그할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-163">The [download sample](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952) contains code to test email confirmation without setting up email, and can also be used to debug the application.</span></span>

<span data-ttu-id="6c999-164">`Views\Shared\Info.cshtml` 파일을 만들고 다음 razor 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-164">Create a `Views\Shared\Info.cshtml` file and add the following razor markup:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample8.cshtml)]

<span data-ttu-id="6c999-165">Home 컨트롤러의 `Contact` 작업 메서드에 [권한 부여 특성](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx) 을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-165">Add the [Authorize attribute](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx) to the `Contact` action method of the Home controller.</span></span> <span data-ttu-id="6c999-166">**연락처** 링크를 클릭 하 여 익명 사용자에 게 액세스 권한이 없고 인증 된 사용자에 게 액세스 권한이 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-166">You can click on the **Contact** link to verify anonymous users don't have access and authenticated users do have access.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample9.cs?highlight=1)]

<span data-ttu-id="6c999-167">또한 `HttpPost Login` 작업 메서드를 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-167">You must also update the `HttpPost Login` action method:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample10.cs?highlight=13-22)]

<span data-ttu-id="6c999-168">*Views\Shared\Error.cshtml* 보기를 업데이트 하 여 오류 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-168">Update the *Views\Shared\Error.cshtml* view to display the error message:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample11.cshtml?highlight=8-17)]

<span data-ttu-id="6c999-169">**AspNetUsers** 테이블에서 테스트 하려는 전자 메일 별칭이 포함 된 모든 계정을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-169">Delete any accounts in the **AspNetUsers** table that contain the email alias you wish to test with.</span></span> <span data-ttu-id="6c999-170">앱을 실행 하 고 전자 메일 주소를 확인 한 후에만 로그인 할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-170">Run the app and verify you can't log in until you have confirmed your email address.</span></span> <span data-ttu-id="6c999-171">전자 메일 주소를 확인 한 후 **연락처** 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-171">Once you confirm your email address, click the **Contact** link.</span></span>

<a id="reset"></a>
## <a name="password-recoveryreset"></a><span data-ttu-id="6c999-172">암호 복구/다시 설정</span><span class="sxs-lookup"><span data-stu-id="6c999-172">Password recovery/reset</span></span>

<span data-ttu-id="6c999-173">계정 컨트롤러의 `HttpPost ForgotPassword` 동작 메서드에서 주석 문자를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-173">Remove the comment characters from the `HttpPost ForgotPassword` action method in the account controller:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample12.cs?highlight=17-20)]

<span data-ttu-id="6c999-174">*Views\Account\Login.cshtml* razor 뷰 파일 [의 `ForgotPassword`/에서 주석](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx) 문자를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-174">Remove the comment characters from the `ForgotPassword` [ActionLink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx) in the *Views\Account\Login.cshtml* razor view file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample13.cshtml?highlight=47-50)]

<span data-ttu-id="6c999-175">이제 로그인 페이지에 암호를 다시 설정 하는 링크가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-175">The Log in page will now show a link to reset the password.</span></span>

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a><span data-ttu-id="6c999-176">전자 메일 다시 보내기 확인 링크</span><span class="sxs-lookup"><span data-stu-id="6c999-176">Resend email confirmation link</span></span>

<span data-ttu-id="6c999-177">사용자가 새 로컬 계정을 만들면 로그온 하기 전에 사용 해야 하는 확인 링크를 전자 메일로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-177">Once a user creates a new local account, they are emailed a confirmation link they are required to use before they can log on.</span></span> <span data-ttu-id="6c999-178">사용자가 실수로 확인 전자 메일을 삭제 하거나 전자 메일이 도착 하지 않은 경우 확인 링크를 다시 전송 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-178">If the user accidentally deletes the confirmation email, or the email never arrives, they will need the confirmation link sent again.</span></span> <span data-ttu-id="6c999-179">다음 코드 변경 내용에서는이를 사용 하도록 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-179">The following code changes show how to enable this.</span></span>

<span data-ttu-id="6c999-180">다음 도우미 메서드를 *Controllers\accountcontroller.cs* 파일의 아래쪽에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-180">Add the following helper method to the bottom of the *Controllers\AccountController.cs* file:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample14.cs)]

<span data-ttu-id="6c999-181">새 도우미를 사용 하도록 Register 메서드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-181">Update the Register method to use the new helper:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample15.cs?highlight=17)]

<span data-ttu-id="6c999-182">사용자 계정이 확인 되지 않은 경우 암호를 다시 보내도록 로그인 메서드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-182">Update the Login method to resend the password if the user account has not been confirmed:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample16.cs?highlight=20)]

<a id="combine"></a>
## <a name="combine-social-and-local-login-accounts"></a><span data-ttu-id="6c999-183">소셜 및 로컬 로그인 계정 결합</span><span class="sxs-lookup"><span data-stu-id="6c999-183">Combine social and local login accounts</span></span>

<span data-ttu-id="6c999-184">전자 메일 링크를 클릭 하 여 로컬 및 소셜 계정을 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-184">You can combine local and social accounts by clicking on your email link.</span></span> <span data-ttu-id="6c999-185">다음 시퀀스에서는 먼저 로컬 로그인으로 만들어진 **RickAndMSFT@gmail.com** 있지만 먼저 계정을 소셜 로그인으로 만든 다음 로컬 로그인을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-185">In the following sequence **RickAndMSFT@gmail.com** is first created as a local login, but you can create the account as a social log in first, then add a local login.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image5.png)

<span data-ttu-id="6c999-186">**관리** 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-186">Click on the **Manage** link.</span></span> <span data-ttu-id="6c999-187">**외부 로그인** 을 기록해 둡니다 .이 계정과 연결 된 0입니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-187">Note the **External Logins: 0** associated with this account.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image6.png)

<span data-ttu-id="6c999-188">다른 로그인 서비스에 대 한 링크를 클릭 하 고 앱 요청을 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-188">Click the link to another log in service and accept the app requests.</span></span> <span data-ttu-id="6c999-189">두 계정을 결합 하 여 두 계정을 사용 하 여 로그온 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-189">The two accounts have been combined, you will be able to log on with either account.</span></span> <span data-ttu-id="6c999-190">인증 서비스의 소셜 로그인이 다운 되거나 소셜 계정에 대 한 액세스 권한이 손실 될 가능성이 있는 경우 사용자가 로컬 계정을 추가 하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-190">You might want your users to add local accounts in case their social log in authentication service is down, or more likely they have lost access to their social account.</span></span>

<span data-ttu-id="6c999-191">다음 그림에서 Tom은 **외부 로그인** 에서 볼 수 있는 소셜 로그인입니다. 1은 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-191">In the following image, Tom is a social log in (which you can see from the **External Logins: 1** shown on the page).</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image7.png)

<span data-ttu-id="6c999-192">**암호 선택** 을 클릭 하면 동일한 계정에 연결 된 로컬 로그를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-192">Clicking on **Pick a password** allows you to add a local log on associated with the same account.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image8.png)

## <a name="email-confirmation-in-more-depth"></a><span data-ttu-id="6c999-193">더 깊이 있는 전자 메일 확인</span><span class="sxs-lookup"><span data-stu-id="6c999-193">Email confirmation in more depth</span></span>

<span data-ttu-id="6c999-194">[ASP.NET Identity를 사용 하 여 내 자습서 계정 확인 및 암호 복구](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) 는이 항목에 자세히 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-194">My tutorial [Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) goes into this topic with more details.</span></span>

<a id="dbg"></a>
## <a name="debugging-the-app"></a><span data-ttu-id="6c999-195">앱 디버깅</span><span class="sxs-lookup"><span data-stu-id="6c999-195">Debugging the app</span></span>

<span data-ttu-id="6c999-196">링크를 포함 하는 전자 메일을 받을 수 없는 경우:</span><span class="sxs-lookup"><span data-stu-id="6c999-196">If you don't get an email containing the link:</span></span>

- <span data-ttu-id="6c999-197">정크 또는 스팸 폴더를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-197">Check your junk or spam folder.</span></span>
- <span data-ttu-id="6c999-198">SendGrid 계정에 로그인 하 고 [전자 메일 활동 링크](https://sendgrid.com/logs/index)를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-198">Log into your SendGrid account and click on the [Email Activity link](https://sendgrid.com/logs/index).</span></span>

<span data-ttu-id="6c999-199">전자 메일 없이 확인 링크를 테스트 하려면 완료 된 [샘플](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-199">To test the verification link without email, download the [completed sample](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span></span> <span data-ttu-id="6c999-200">확인 링크와 확인 코드는 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-200">The confirmation link and confirmation codes will be displayed on the page.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="6c999-201">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="6c999-201">Additional Resources</span></span>

- [<span data-ttu-id="6c999-202">ASP.NET Identity 권장 리소스에 대 한 링크</span><span class="sxs-lookup"><span data-stu-id="6c999-202">Links to ASP.NET Identity Recommended Resources</span></span>](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- <span data-ttu-id="6c999-203">[계정 확인 및 암호 복구 ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) 암호 복구 및 계정 확인에 대해 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-203">[Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Goes into more detail on password recovery and account confirmation.</span></span>
- <span data-ttu-id="6c999-204">[Facebook, Twitter, LinkedIn 및 Google OAuth2 sign-on을 사용한 MVC 5 앱](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 이 자습서에서는 Facebook 및 Google OAuth 2 권한 부여를 사용 하 여 ASP.NET MVC 5 앱을 작성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-204">[MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) This tutorial shows you how to write an ASP.NET MVC 5 app with Facebook and Google OAuth 2 authorization.</span></span> <span data-ttu-id="6c999-205">또한 Id 데이터베이스에 데이터를 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-205">It also shows how to add additional data to the Identity database.</span></span>
- <span data-ttu-id="6c999-206">[멤버 자격, OAuth 및 SQL Database를 사용 하 여 Azure에 보안 ASP.NET MVC 앱을 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-206">[Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="6c999-207">이 자습서에서는 Azure 배포, 역할을 사용 하 여 앱을 보호 하는 방법, 멤버 자격 API를 사용 하 여 사용자 및 역할을 추가 하는 방법 및 추가 보안 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c999-207">This tutorial adds Azure deployment, how to secure your app with roles, how to use the membership API to add users and roles, and additional security features.</span></span>
- [<span data-ttu-id="6c999-208">OAuth 2 용 Google 앱 만들기 및 프로젝트에 앱 연결</span><span class="sxs-lookup"><span data-stu-id="6c999-208">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [<span data-ttu-id="6c999-209">Facebook에서 앱 만들기 및 프로젝트에 앱 연결</span><span class="sxs-lookup"><span data-stu-id="6c999-209">Creating the app in Facebook and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [<span data-ttu-id="6c999-210">프로젝트에서 SSL 설정</span><span class="sxs-lookup"><span data-stu-id="6c999-210">Setting up SSL in the Project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
