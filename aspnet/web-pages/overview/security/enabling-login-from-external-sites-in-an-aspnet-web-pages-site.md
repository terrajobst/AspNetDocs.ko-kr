---
uid: web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
title: ASP.NET 웹 페이지 (Razor) 사이트에서 외부 사이트를 사용 하 여 로그인 | Microsoft Docs
author: Rick-Anderson
description: 이 문서에서는 Facebook, Google, Twitter, Yahoo 및 기타 사이트 (즉,를 지 원하는 방법)를 사용 하 여 ASP.NET 웹 페이지 (Razor) 사이트에 로그인 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 02/21/2014
ms.assetid: ef852096-a5bf-47b3-9945-125cde065093
msc.legacyurl: /web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 860b75422c3df1d191ed861344963bfc19270e8f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518789"
---
# <a name="logging-in-using-external-sites-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="7a83b-103">ASP.NET 웹 페이지 (Razor) 사이트에서 외부 사이트를 사용 하 여 로그인</span><span class="sxs-lookup"><span data-stu-id="7a83b-103">Logging In Using External Sites in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="7a83b-104">만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="7a83b-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="7a83b-105">이 문서에서는 Facebook, Google, Twitter, Yahoo 및 기타 사이트 (즉, 사이트에서 OAuth 및 Openid connect를 지 원하는 방법)를 사용 하 여 ASP.NET 웹 페이지 (Razor) 사이트에 로그인 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-105">This article explains how to log in to your ASP.NET Web Pages (Razor) site using Facebook, Google, Twitter, Yahoo, and other sites — that is, how to support OAuth and OpenID in your site.</span></span>
> 
> <span data-ttu-id="7a83b-106">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="7a83b-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="7a83b-107">WebMatrix 시작 사이트 템플릿을 사용 하는 경우 다른 사이트에서 로그인을 사용 하도록 설정 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-107">How to enable login from other sites when you use the WebMatrix Starter Site template.</span></span>
> 
> <span data-ttu-id="7a83b-108">다음은이 문서에서 소개 하는 ASP.NET 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-108">This is the ASP.NET feature introduced in the article:</span></span>
> 
> - <span data-ttu-id="7a83b-109">`OAuthWebSecurity` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-109">The `OAuthWebSecurity` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="7a83b-110">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="7a83b-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="7a83b-111">ASP.NET 웹 페이지 (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="7a83b-111">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="7a83b-112">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="7a83b-112">WebMatrix 3</span></span>

<span data-ttu-id="7a83b-113">ASP.NET 웹 페이지에는 [OAuth](http://oauth.net/) 및 [openid connect](http://openid.net/) 공급자에 대 한 지원이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-113">ASP.NET Web Pages includes support for [OAuth](http://oauth.net/) and [OpenID](http://openid.net/) providers.</span></span> <span data-ttu-id="7a83b-114">이러한 공급자를 사용 하 여 사용자가 Facebook, Twitter, Microsoft 및 Google에서 기존 자격 증명을 사용 하 여 사이트에 로그인 하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-114">Using these providers, you can let users log into your site using their existing credentials from Facebook, Twitter, Microsoft, and Google.</span></span> <span data-ttu-id="7a83b-115">예를 들어 Facebook 계정을 사용 하 여 로그인 하기 위해 사용자는 facebook 아이콘을 선택 하기만 하면 사용자 정보를 입력 하는 Facebook 로그인 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-115">For example, to log in using a Facebook account, users can just choose a Facebook icon, which redirects them to the Facebook login page where they enter their user information.</span></span> <span data-ttu-id="7a83b-116">그런 다음 Facebook 로그인을 사이트의 계정에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-116">They can then associate the Facebook login with their account on your site.</span></span> <span data-ttu-id="7a83b-117">웹 페이지 멤버 자격 기능과 관련 하 여 향상 된 기능은 사용자가 여러 로그인 (소셜 네트워킹 사이트의 로그인 포함)을 웹 사이트의 단일 계정으로 연결할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-117">A related enhancement to the Web Pages membership features is that users can associate multiple logins (including logins from social networking sites) with a single account on your website.</span></span>

<span data-ttu-id="7a83b-118">이 이미지는 **시작 사이트** 템플릿의 로그인 페이지를 보여 줍니다. 여기서 사용자는 Facebook, Twitter, Google 또는 Microsoft 아이콘을 선택 하 여 외부 계정으로 로그인 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-118">This image shows the Login page from the **Starter Site** template, where a user can choose a Facebook, Twitter, Google or Microsoft icon to enable logging in with an external account:</span></span>

![외부 공급자](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image1.png)

<span data-ttu-id="7a83b-120">**시작 사이트** 템플릿에서 몇 줄의 코드를 주석 처리 하 여 OAuth 및 openid connect 멤버 자격을 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-120">You can enable OAuth and OpenID membership by uncommenting a few lines of code in the **Starter Site** template.</span></span> <span data-ttu-id="7a83b-121">OAuth 및 Openid connect 공급자를 사용 하 여 작업 하는 데 사용 하는 메서드 및 속성은 `WebMatrix.Security.OAuthWebSecurity` 클래스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-121">The methods and properties you use to work with the OAuth and OpenID providers are in the `WebMatrix.Security.OAuthWebSecurity` class.</span></span> <span data-ttu-id="7a83b-122">**시작 사이트** 템플릿에는 전체 멤버 자격 인프라, 로그인 페이지, 멤버 자격 데이터베이스 및 사용자가 로컬 자격 증명을 사용 하 여 사이트에 로그인 하거나 다른 사이트의 사용자가 로그인 할 수 있도록 하는 모든 코드가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-122">The **Starter Site** template includes a full membership infrastructure, complete with a login page, a membership database, and all the code you need to let users log into your site using either local credentials or those from another site.</span></span>

<span data-ttu-id="7a83b-123">이 섹션에서는 사용자가 외부 사이트에서 **스타터 사이트** 템플릿을 기반으로 하는 사이트에 로그인 할 수 있도록 하는 방법에 대 한 예를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-123">This section provides an example of how to let users log in from external sites to a site that's based on the **Starter Site** template.</span></span> <span data-ttu-id="7a83b-124">시작 사이트를 만든 후이 작업을 수행 합니다 (자세한 내용은 참조).</span><span class="sxs-lookup"><span data-stu-id="7a83b-124">After creating a starter site, you do this (details follow):</span></span>

- <span data-ttu-id="7a83b-125">OAuth 공급자 (Facebook, Twitter 및 Microsoft)를 사용 하는 사이트의 경우 외부 사이트에 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-125">For the sites that use an OAuth provider (Facebook, Twitter, and Microsoft), you create an application on the external site.</span></span> <span data-ttu-id="7a83b-126">이를 통해 해당 사이트에 대 한 로그인 기능을 호출 하기 위해 필요한 응용 프로그램 키를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-126">This gives you application keys that you'll need in order to invoke the login feature for those sites.</span></span>
- <span data-ttu-id="7a83b-127">Google (Openid connect provider)을 사용 하는 사이트의 경우에는 응용 프로그램을 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-127">For sites that use an OpenID provider (Google), you do not have to create an application.</span></span> <span data-ttu-id="7a83b-128">이러한 모든 사이트에는 로그인 하 여 개발자 응용 프로그램을 만들기 위해 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-128">For all of these sites, you must have an account in order to log in and to create developer applications.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7a83b-129">Microsoft 응용 프로그램은 작동 하는 웹 사이트의 라이브 URL만 허용 하므로 로그인 테스트에는 로컬 웹 사이트 URL을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-129">Microsoft applications only accept a live URL for a working website, so you cannot use a local website URL for testing logins.</span></span>
- <span data-ttu-id="7a83b-130">적절 한 인증 공급자를 지정 하 고 사용 하려는 사이트에 로그인을 제출 하기 위해 웹 사이트의 몇 가지 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-130">Edit a few files in your website in order to specify the appropriate authentication provider and to submit a login to the site you want to use.</span></span>

<span data-ttu-id="7a83b-131">이 문서에서는 다음 작업에 대해 별도의 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-131">This article provides separate instructions for the following tasks:</span></span>

- [<span data-ttu-id="7a83b-132">Google 로그인 사용</span><span class="sxs-lookup"><span data-stu-id="7a83b-132">Enabling Google logins</span></span>](#To_enable_Google_logins)
- [<span data-ttu-id="7a83b-133">Facebook 로그인 사용</span><span class="sxs-lookup"><span data-stu-id="7a83b-133">Enabling Facebook logins</span></span>](#To_enable_Facebook_logins)
- [<span data-ttu-id="7a83b-134">Twitter 로그인 사용</span><span class="sxs-lookup"><span data-stu-id="7a83b-134">Enabling Twitter logins</span></span>](#To_enable_Twitter_logins)

<a id="To_enable_Google_logins"></a>
## <a name="enabling-google-logins"></a><span data-ttu-id="7a83b-135">Google 로그인 사용</span><span class="sxs-lookup"><span data-stu-id="7a83b-135">Enabling Google Logins</span></span>

1. <span data-ttu-id="7a83b-136">WebMatrix 시작 사이트 템플릿을 기반으로 하는 ASP.NET 웹 페이지 사이트를 만들거나 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-136">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="7a83b-137">*\_AppStart* 페이지를 열고 다음 코드 줄의 주석 처리를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-137">Open the *\_AppStart.cshtml* page and uncomment the following line of code.</span></span> 

    [!code-css[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample1.css)]

### <a name="testing-google-login"></a><span data-ttu-id="7a83b-138">Google 로그인 테스트</span><span class="sxs-lookup"><span data-stu-id="7a83b-138">Testing Google login</span></span>

1. <span data-ttu-id="7a83b-139">사이트의 *기본값. cshtml* 페이지를 실행 하 고 **로그인** 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-139">Run the *default.cshtml* page of your site and choose the **Log in** button.</span></span>
2. <span data-ttu-id="7a83b-140">*로그인* 페이지의 **다른 서비스를 사용 하 여** 로그인 섹션에서 **Google** 또는 **Yahoo** 제출 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-140">On the *Login* page, in the **Use another service to log in** section, choose either the **Google** or **Yahoo** submit button.</span></span> <span data-ttu-id="7a83b-141">이 예에서는 Google 로그인을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-141">This example uses the Google login.</span></span> 

    <span data-ttu-id="7a83b-142">웹 페이지에서 요청을 Google 로그인 페이지로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-142">The web page redirects the request to the Google login page.</span></span>

    ![Google 로그인](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image2.png)
3. <span data-ttu-id="7a83b-144">기존 Google 계정에 대 한 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-144">Enter credentials for an existing Google account.</span></span>
4. <span data-ttu-id="7a83b-145">*Localhost* 가 계정의 정보를 사용 하도록 허용할지 여부를 묻는 메시지가 표시 되 면 **허용**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-145">If Google asks you whether you want to allow *Localhost* to use information from the account, click **Allow**.</span></span>

    <span data-ttu-id="7a83b-146">이 코드는 Google 토큰을 사용 하 여 사용자를 인증 한 다음 웹 사이트의이 페이지로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-146">The code uses the Google token to authenticate the user, and then returns to this page on your website.</span></span> <span data-ttu-id="7a83b-147">이 페이지에서 사용자는 Google 로그인을 웹 사이트의 기존 계정과 연결 하거나, 사이트에 새 계정을 등록 하 여 외부 로그인을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-147">This page lets users associate their Google login with an existing account on your website, or they can register a new account on your site to associate the external login with.</span></span>

    ![oauth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image3.png)
5. <span data-ttu-id="7a83b-149">**연결** 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-149">Choose the **Associate** button.</span></span> <span data-ttu-id="7a83b-150">브라우저는 응용 프로그램의 홈 페이지로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-150">The browser returns to your application's home page.</span></span>

<a id="To_enable_Facebook_logins"></a>
## <a name="enabling-facebook-logins"></a><span data-ttu-id="7a83b-151">Facebook 로그인 사용</span><span class="sxs-lookup"><span data-stu-id="7a83b-151">Enabling Facebook Logins</span></span>

1. <span data-ttu-id="7a83b-152">[Facebook 개발자 사이트로](https://developers.facebook.com/apps) 이동 합니다 (아직 로그인 하지 않은 경우 로그인).</span><span class="sxs-lookup"><span data-stu-id="7a83b-152">Go to the [Facebook developers site](https://developers.facebook.com/apps) (log in if you're not already logged in).</span></span>
2. <span data-ttu-id="7a83b-153">새 응용 프로그램 **만들기** 단추를 선택한 다음 프롬프트에 따라 새 응용 프로그램을 만들고 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-153">Choose the **Create New App** button, and then follow the prompts to name and create the new application.</span></span>
3. <span data-ttu-id="7a83b-154">**앱이 Facebook과 통합 되는 방법 선택**섹션에서 **웹 사이트** 섹션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-154">In the section **Select how your app will integrate with Facebook**, choose the **Website** section.</span></span>
4. <span data-ttu-id="7a83b-155">사이트 **url** 필드에 사이트 url을 입력 합니다 (예: `http://www.example.com`).</span><span class="sxs-lookup"><span data-stu-id="7a83b-155">Fill in the **Site URL** field with the URL of your site (for example, `http://www.example.com`).</span></span> <span data-ttu-id="7a83b-156">**도메인** 필드는 선택 사항입니다. 이를 사용 하 여 전체 도메인 (예: *example.com*)에 대 한 인증을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-156">The **Domain** field is optional; you can use this to provide authentication for an entire domain (such as *example.com*).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="7a83b-157">`http://localhost:12345`와 같은 URL (로컬 포트 번호)을 사용 하 여 로컬 컴퓨터에서 사이트를 실행 하는 경우 사이트를 테스트 하기 위해 **사이트 url** 필드에이 값을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-157">If you are running a site on your local computer with a URL like `http://localhost:12345` (where the number is a local port number), you can add this value to the **Site URL** field for testing your site.</span></span> <span data-ttu-id="7a83b-158">그러나 로컬 사이트의 포트 번호가 변경 될 때마다 응용 프로그램의 **사이트 URL** 필드를 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-158">However, any time the port number of your local site changes, you will need to update the **Site URL** field of your application.</span></span>
5. <span data-ttu-id="7a83b-159">**변경 내용 저장** 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-159">Choose the **Save Changes** button.</span></span>
6. <span data-ttu-id="7a83b-160">**앱** 탭을 다시 선택 하 고 응용 프로그램의 시작 페이지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-160">Choose the **Apps** tab again, and then view the start page for your application.</span></span>
7. <span data-ttu-id="7a83b-161">응용 프로그램에 대 한 **앱 ID** 및 **앱 암호** 값을 복사 하 여 임시 텍스트 파일에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-161">Copy the **App ID** and **App Secret** values for your application and paste them into a temporary text file.</span></span> <span data-ttu-id="7a83b-162">웹 사이트 코드의 Facebook 공급자에 이러한 값을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-162">You will pass these values to the Facebook provider in your website code.</span></span>
8. <span data-ttu-id="7a83b-163">Facebook 개발자 사이트를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-163">Exit the Facebook developer site.</span></span>

<span data-ttu-id="7a83b-164">이제 사용자가 Facebook 계정을 사용 하 여 사이트에 로그인 할 수 있도록 웹 사이트의 두 페이지를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-164">Now you make changes to two pages in your website so that users will able to log into the site using their Facebook accounts.</span></span>

1. <span data-ttu-id="7a83b-165">WebMatrix 시작 사이트 템플릿을 기반으로 하는 ASP.NET 웹 페이지 사이트를 만들거나 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-165">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="7a83b-166">*\_AppStart* 페이지를 열고 Facebook OAuth 공급자에 대 한 코드의 주석 처리를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-166">Open the *\_AppStart.cshtml* page and uncomment the code for the Facebook OAuth provider.</span></span> <span data-ttu-id="7a83b-167">주석 처리가 제거 코드 블록은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-167">The uncommented code block looks like the following:</span></span> 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample2.cs)]
3. <span data-ttu-id="7a83b-168">Facebook 응용 프로그램에서 `appId` 매개 변수 값 (따옴표 내)으로 **앱 ID** 값을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-168">Copy the **App ID** value from the Facebook application as the value of the `appId` parameter (inside the quotation marks).</span></span>
4. <span data-ttu-id="7a83b-169">Facebook 응용 프로그램에서 `appSecret` 매개 변수 값으로 **앱 비밀** 값을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-169">Copy **App Secret** value from the Facebook application as the `appSecret` parameter value.</span></span>
5. <span data-ttu-id="7a83b-170">파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-170">Save and close the file.</span></span>

### <a name="testing-facebook-login"></a><span data-ttu-id="7a83b-171">Facebook 로그인 테스트</span><span class="sxs-lookup"><span data-stu-id="7a83b-171">Testing Facebook login</span></span>

1. <span data-ttu-id="7a83b-172">사이트의 *기본값. cshtml* 페이지를 실행 하 고 **로그인** 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-172">Run the site's *default.cshtml* page and choose the **Login** button.</span></span>
2. <span data-ttu-id="7a83b-173">*로그인* 페이지의 **다른 서비스를 사용 하 여** 로그인 섹션에서 **Facebook** 아이콘을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-173">On the *Login* page, in the **Use another service to log in** section, choose the **Facebook** icon.</span></span> 

    <span data-ttu-id="7a83b-174">웹 페이지에서 요청을 Facebook 로그인 페이지로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-174">The web page redirects the request to the Facebook login page.</span></span>

    ![oauth-2](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image4.png)
3. <span data-ttu-id="7a83b-176">Facebook 계정에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-176">Log into a Facebook account.</span></span> 

    <span data-ttu-id="7a83b-177">이 코드는 Facebook 토큰을 사용 하 여 사용자를 인증 한 다음 Facebook 로그인을 사이트 로그인에 연결할 수 있는 페이지로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-177">The code uses the Facebook token to authenticate you and then returns to a page where you can associate your Facebook login with your site's login.</span></span> <span data-ttu-id="7a83b-178">사용자 이름 또는 전자 메일 주소가 양식의 **전자 메일** 필드에 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-178">Your user name or email address is filled into the **Email** field on the form.</span></span>

    ![oauth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image5.png)
4. <span data-ttu-id="7a83b-180">**연결** 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-180">Choose the **Associate** button.</span></span> 

    <span data-ttu-id="7a83b-181">브라우저가 홈 페이지로 반환 되 고 로그인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-181">The browser returns to the home page and you are logged in.</span></span>

<a id="To_enable_Twitter_logins"></a>
## <a name="enabling-twitter-logins"></a><span data-ttu-id="7a83b-182">Twitter 로그인 사용</span><span class="sxs-lookup"><span data-stu-id="7a83b-182">Enabling Twitter Logins</span></span>

1. <span data-ttu-id="7a83b-183">[Twitter 개발자 사이트로](https://dev.twitter.com/)이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-183">Browse to the [Twitter developers site](https://dev.twitter.com/).</span></span>
2. <span data-ttu-id="7a83b-184">**앱 만들기** 링크를 선택 하 고 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-184">Choose the **Create an App** link and then log into the site.</span></span>
3. <span data-ttu-id="7a83b-185">**응용 프로그램 만들기** 양식에서 **이름** 및 **설명** 필드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-185">On the **Create an Application** form, fill in the **Name** and **Description** fields.</span></span>
4. <span data-ttu-id="7a83b-186">**웹** 사이트 필드에 사이트의 URL을 입력 합니다 (예: `http://www.example.com`).</span><span class="sxs-lookup"><span data-stu-id="7a83b-186">In the **WebSite** field, enter the URL of your site (for example, `http://www.example.com`).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="7a83b-187">`http://localhost:12345`같은 URL을 사용 하 여 사이트를 로컬로 테스트 하는 경우 Twitter에서 URL을 허용 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-187">If you're testing your site locally (using a URL like `http://localhost:12345`), Twitter might not accept the URL.</span></span> <span data-ttu-id="7a83b-188">그러나 로컬 루프백 IP 주소를 사용할 수 있습니다 (예: `http://127.0.0.1:12345`).</span><span class="sxs-lookup"><span data-stu-id="7a83b-188">However, you might be able to use the local loopback IP address (for example `http://127.0.0.1:12345`).</span></span> <span data-ttu-id="7a83b-189">이렇게 하면 응용 프로그램을 로컬로 테스트 하는 프로세스가 간단해 집니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-189">This simplifies the process of testing your application locally.</span></span> <span data-ttu-id="7a83b-190">그러나 로컬 사이트의 포트 번호가 변경 될 때마다 응용 프로그램의 **웹 사이트** 필드를 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-190">However, every time the port number of your local site changes, you'll need to update the **WebSite** field of your application.</span></span>
5. <span data-ttu-id="7a83b-191">사용자가 Twitter에 로그인 한 후 사용자가 반환할 웹 사이트의 페이지에 대 한 URL을 **콜백 url** 필드에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-191">In the **Callback URL** field, enter a URL for the page in your website that you want users to return to after logging into Twitter.</span></span> <span data-ttu-id="7a83b-192">예를 들어 로그인 상태를 인식 하는 시작 사이트의 홈 페이지로 사용자를 보내려면 **웹 사이트** 필드에 입력 한 것과 동일한 URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-192">For example, to send users to the home page of the Starter Site (which will recognize their logged-in status), enter the same URL that you entered in the **WebSite** field.</span></span>
6. <span data-ttu-id="7a83b-193">조건에 동의 하 고 **Twitter 응용 프로그램 만들기** 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-193">Accept the terms and choose the **Create your Twitter application** button.</span></span>
7. <span data-ttu-id="7a83b-194">**내 응용** 프로그램 방문 페이지에서 사용자가 만든 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-194">On the **My Applications** landing page, choose the application you created.</span></span>
8. <span data-ttu-id="7a83b-195">**세부 정보** 탭에서 아래쪽으로 스크롤하고 **내 액세스 토큰 만들기** 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-195">On the **Details** tab, scroll to the bottom and choose the **Create My Access Token** button.</span></span>
9. <span data-ttu-id="7a83b-196">**세부 정보** 탭에서 응용 프로그램에 대 한 **소비자 키** 및 **소비자 암호** 값을 복사 하 여 임시 텍스트 파일에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-196">On the **Details** tab, copy the **Consumer Key** and **Consumer Secret** values for your application and paste them into a temporary text file.</span></span> <span data-ttu-id="7a83b-197">웹 사이트 코드의 Twitter 공급자에 이러한 값을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-197">You'll pass these values to the Twitter provider in your website code.</span></span>
10. <span data-ttu-id="7a83b-198">Twitter 사이트를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-198">Exit the Twitter site.</span></span>

<span data-ttu-id="7a83b-199">이제 사용자가 Twitter 계정을 사용 하 여 사이트에 로그인 할 수 있도록 웹 사이트의 두 페이지를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-199">Now you make changes to two pages in your website so that users will be able to log into the site using their Twitter accounts.</span></span>

1. <span data-ttu-id="7a83b-200">WebMatrix 시작 사이트 템플릿을 기반으로 하는 ASP.NET 웹 페이지 사이트를 만들거나 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-200">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="7a83b-201">*\_AppStart* 페이지를 열고 Twitter OAuth 공급자에 대 한 코드의 주석 처리를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-201">Open the *\_AppStart.cshtml* page and uncomment the code for the Twitter OAuth provider.</span></span> <span data-ttu-id="7a83b-202">주석 처리가 제거 코드 블록은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-202">The uncommented code block looks like this:</span></span> 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample3.cs)]
3. <span data-ttu-id="7a83b-203">Twitter 응용 프로그램의 **소비자 키** 값을 따옴표 안에 있는 `consumerKey` 매개 변수의 값으로 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-203">Copy the **Consumer Key** value from the Twitter application as the value of the `consumerKey` parameter (inside the quotation marks).</span></span>
4. <span data-ttu-id="7a83b-204">Twitter 응용 프로그램의 **소비자 암호** 값을 `consumerSecret` 매개 변수의 값으로 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-204">Copy the **Consumer Secret** value from the Twitter application as the value of the `consumerSecret` parameter.</span></span>
5. <span data-ttu-id="7a83b-205">파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-205">Save and close the file.</span></span>

### <a name="testing-twitter-login"></a><span data-ttu-id="7a83b-206">Twitter 로그인 테스트</span><span class="sxs-lookup"><span data-stu-id="7a83b-206">Testing Twitter login</span></span>

1. <span data-ttu-id="7a83b-207">사이트의 *기본값. cshtml* 페이지를 실행 하 고 **로그인** 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-207">Run the *default.cshtml* page of your site and choose the **Login** button.</span></span>
2. <span data-ttu-id="7a83b-208">*로그인* 페이지의 **다른 서비스를 사용 하 여** 로그인 섹션에서 **Twitter** 아이콘을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-208">On the *Login* page, in the **Use another service to log in** section, choose the **Twitter** icon.</span></span> 

    <span data-ttu-id="7a83b-209">웹 페이지에서 사용자가 만든 응용 프로그램에 대 한 Twitter 로그인 페이지로 요청이 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-209">The web page redirects the request to a Twitter login page for the application you created.</span></span>

    ![oauth-4](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image6.png)
3. <span data-ttu-id="7a83b-211">Twitter 계정에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-211">Log into a Twitter account.</span></span>
4. <span data-ttu-id="7a83b-212">이 코드는 Twitter 토큰을 사용 하 여 사용자를 인증 한 다음 로그인을 웹 사이트 계정에 연결할 수 있는 페이지로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-212">The code uses the Twitter token to authenticate the user and then returns you to a page where you can associate your login with your website account.</span></span> <span data-ttu-id="7a83b-213">이름 또는 전자 메일 주소는 양식의 **전자 메일** 필드에 입력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-213">Your name or email address is filled into the **Email** field on the form.</span></span>

    ![oauth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image7.png)
5. <span data-ttu-id="7a83b-215">**연결** 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-215">Choose the **Associate** button.</span></span> 

    <span data-ttu-id="7a83b-216">브라우저가 홈 페이지로 반환 되 고 로그인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a83b-216">The browser returns to the home page and you are logged in.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="7a83b-217">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="7a83b-217">Additional Resources</span></span>

- [<span data-ttu-id="7a83b-218">사이트 전체 동작 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="7a83b-218">Customizing Site-Wide Behavior</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
- [<span data-ttu-id="7a83b-219">ASP.NET 웹 페이지 사이트에 보안 및 멤버 자격 추가</span><span class="sxs-lookup"><span data-stu-id="7a83b-219">Adding Security and Membership to an ASP.NET Web Pages Site</span></span>](https://go.microsoft.com/fwlink/?LinkID=202904)
