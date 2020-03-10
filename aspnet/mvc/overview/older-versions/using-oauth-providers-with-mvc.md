---
uid: mvc/overview/older-versions/using-oauth-providers-with-mvc
title: MVC 4에서 OAuth 공급자 사용 | Microsoft Docs
author: Rick-Anderson
description: '이 자습서에서는 사용자가 외부 공급자 (예: Facebo)에서 자격 증명을 사용 하 여 로그인 할 수 있도록 하는 ASP.NET MVC 4 웹 응용 프로그램을 빌드하는 방법을 보여 줍니다.'
ms.author: riande
ms.date: 06/19/2013
ms.assetid: 7a87f16f-0e19-4f15-a88a-094ae866c4a2
msc.legacyurl: /mvc/overview/older-versions/using-oauth-providers-with-mvc
msc.type: authoredcontent
ms.openlocfilehash: 5dfd1305376a62f4987caea242ca0f6aac1018e9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433367"
---
# <a name="using-oauth-providers-with-mvc-4"></a><span data-ttu-id="6f1ca-103">MVC 4와 함께 OAuth 공급자 사용</span><span class="sxs-lookup"><span data-stu-id="6f1ca-103">Using OAuth Providers with MVC 4</span></span>

<span data-ttu-id="6f1ca-104">만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="6f1ca-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="6f1ca-105">이 자습서에서는 사용자가 Facebook, Twitter, Microsoft 또는 Google과 같은 외부 공급자의 자격 증명을 사용 하 여 로그인 한 다음 해당 공급자의 일부 기능을에 통합할 수 있도록 하는 ASP.NET MVC 4 웹 응용 프로그램을 빌드하는 방법을 보여 줍니다. 웹 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-105">This tutorial shows you how to build an ASP.NET MVC 4 web application that enables users to log in with credentials from an external provider, such as Facebook, Twitter, Microsoft, or Google, and then integrate some of the functionality from those providers into your web application.</span></span> <span data-ttu-id="6f1ca-106">간단히 하기 위해이 자습서에서는 Facebook에서 자격 증명을 사용 하는 방법을 집중적으로 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-106">For simplicity, this tutorial focuses on working with credentials from Facebook.</span></span>
> 
> <span data-ttu-id="6f1ca-107">ASP.NET MVC 5 웹 응용 프로그램에서 외부 자격 증명을 사용 하려면 [Facebook 및 Google OAuth2 및 Openid connect sign-on을 사용 하 여 ASP.NET MVC 5 앱 만들기](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-107">To use external credentials in an ASP.NET MVC 5 web application, see [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>
> 
> <span data-ttu-id="6f1ca-108">웹 사이트에서 이러한 자격 증명을 사용 하도록 설정 하면 수백만 명의 사용자가 이미 이러한 외부 공급자를 사용 하는 계정을 갖고 있기 때문에 상당한 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-108">Enabling these credentials in your web sites provides a significant advantage because millions of users already have accounts with these external providers.</span></span> <span data-ttu-id="6f1ca-109">이러한 사용자는 새 자격 증명 집합을 만들고 기억할 필요가 없는 경우 사이트에 등록 하는 것이 더 쉬운데 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-109">These users may be more inclined to sign up for your site if they do not have to create and remember a new set of credentials.</span></span> <span data-ttu-id="6f1ca-110">또한 사용자가 이러한 공급자 중 하나를 통해 로그인 한 후에는 공급자의 소셜 작업을 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-110">Also, after a user has logged in through one of these providers, you can incorporate social operations from the provider.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="6f1ca-111">빌드할 내용</span><span class="sxs-lookup"><span data-stu-id="6f1ca-111">What you'll build</span></span>

<span data-ttu-id="6f1ca-112">이 자습서에는 다음과 같은 두 가지 주요 목표가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-112">There are two main goals in this tutorial:</span></span>

1. <span data-ttu-id="6f1ca-113">사용자가 OAuth 공급자의 자격 증명으로 로그인 할 수 있도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-113">Enable a user to log in with credentials from an OAuth provider.</span></span>
2. <span data-ttu-id="6f1ca-114">공급자 로부터 계정 정보를 검색 하 고 해당 정보를 사이트의 계정 등록과 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-114">Retrieve account information from the provider and integrate that information with the account registration for your site.</span></span>

<span data-ttu-id="6f1ca-115">이 자습서의 예제에서는 Facebook을 인증 공급자로 사용 하는 방법에 중점을 두지만 모든 공급자를 사용 하도록 코드를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-115">Although the examples in this tutorial focus on using Facebook as the authentication provider, you can modify the code to use any of the providers.</span></span> <span data-ttu-id="6f1ca-116">모든 공급자를 구현 하는 단계는이 자습서에 표시 되는 단계와 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-116">The steps to implement any provider are very similar to the steps you will see in this tutorial.</span></span> <span data-ttu-id="6f1ca-117">공급자의 API 집합을 직접 호출 하는 경우에만 상당한 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-117">You will only notice significant differences when making direct calls to the provider's API set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f1ca-118">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="6f1ca-118">Prerequisites</span></span>

- <span data-ttu-id="6f1ca-119">[Microsoft Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads#vs) 또는 [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/downloads#d-2012-express)</span><span class="sxs-lookup"><span data-stu-id="6f1ca-119">[Microsoft Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads#vs) or [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/downloads#d-2012-express)</span></span>

<span data-ttu-id="6f1ca-120">또는</span><span class="sxs-lookup"><span data-stu-id="6f1ca-120">Or</span></span>

- <span data-ttu-id="6f1ca-121">Microsoft Visual Studio 2010 SP1 또는 [Visual Web Developer Express 2010 SP1](https://www.microsoft.com/visualstudio/eng/downloads#d-2010-express)</span><span class="sxs-lookup"><span data-stu-id="6f1ca-121">Microsoft Visual Studio 2010 SP1 or [Visual Web Developer Express 2010 SP1](https://www.microsoft.com/visualstudio/eng/downloads#d-2010-express)</span></span>
- [<span data-ttu-id="6f1ca-122">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="6f1ca-122">ASP.NET MVC 4</span></span>](https://go.microsoft.com/fwlink/?LinkId=243392)

<span data-ttu-id="6f1ca-123">또한이 항목에서는 ASP.NET MVC 및 Visual Studio에 대 한 기본 지식이 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-123">Furthermore, this topic assumes you have basic knowledge about ASP.NET MVC and Visual Studio.</span></span> <span data-ttu-id="6f1ca-124">ASP.NET MVC 4를 소개 해야 하는 경우 [ASP.NET mvc 4](getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)소개를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-124">If you need an introduction to ASP.NET MVC 4, see [Intro to ASP.NET MVC 4](getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md).</span></span>

## <a name="create-the-project"></a><span data-ttu-id="6f1ca-125">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="6f1ca-125">Create the project</span></span>

<span data-ttu-id="6f1ca-126">Visual Studio에서 새 ASP.NET MVC 4 웹 응용 프로그램을 만들고 &quot;OAuthMVC&quot;로 이름을로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-126">In Visual Studio, create a new ASP.NET MVC 4 Web Application, and name it &quot;OAuthMVC&quot;.</span></span> <span data-ttu-id="6f1ca-127">.NET Framework 4.5 또는 4 중 하나를 대상으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-127">You can target either .NET Framework 4.5 or 4.</span></span>

![프로젝트 만들기](using-oauth-providers-with-mvc/_static/image1.png)

<span data-ttu-id="6f1ca-129">새 ASP.NET MVC 4 프로젝트 창에서 **인터넷 응용 프로그램** 을 선택 하 고 **Razor** 를 뷰 엔진으로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-129">In the New ASP.NET MVC 4 Project window, select **Internet Application** and leave **Razor** as the view engine.</span></span>

![인터넷 응용 프로그램 선택](using-oauth-providers-with-mvc/_static/image2.png)

## <a name="enable-a-provider"></a><span data-ttu-id="6f1ca-131">공급자 사용</span><span class="sxs-lookup"><span data-stu-id="6f1ca-131">Enable a provider</span></span>

<span data-ttu-id="6f1ca-132">인터넷 응용 프로그램 템플릿을 사용 하 여 MVC 4 웹 응용 프로그램을 만들 때 프로젝트는 App\_시작 폴더에 AuthConfig.cs 라는 파일로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-132">When you create an MVC 4 web application with the Internet Application template, the project is created with a file named AuthConfig.cs in the App\_Start folder.</span></span>

![AuthConfig 파일](using-oauth-providers-with-mvc/_static/image3.png)

<span data-ttu-id="6f1ca-134">AuthConfig 파일에는 외부 인증 공급자에 대 한 클라이언트를 등록 하는 코드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-134">The AuthConfig file contains code to register clients for external authentication providers.</span></span> <span data-ttu-id="6f1ca-135">기본적으로이 코드는 주석 처리 되므로 외부 공급자를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-135">By default, this code is commented out, so none of the external providers are enabled.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample1.cs)]

<span data-ttu-id="6f1ca-136">외부 인증 클라이언트를 사용 하려면이 코드의 주석 처리를 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-136">You must uncomment this code to use the external authentication client.</span></span> <span data-ttu-id="6f1ca-137">사이트에 포함 하려는 공급자에 대해서만 주석 처리를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-137">You uncomment only the providers you want to include in your site.</span></span> <span data-ttu-id="6f1ca-138">이 자습서에서는 Facebook 자격 증명만 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-138">For this tutorial, you will only enable the Facebook credentials.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample2.cs)]

<span data-ttu-id="6f1ca-139">위의 예제에서 메서드에는 등록 매개 변수에 대 한 빈 문자열이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-139">Notice in the above example that the method includes empty strings for the registration parameters.</span></span> <span data-ttu-id="6f1ca-140">이제 응용 프로그램을 실행 하려고 하면 매개 변수에 대해 빈 문자열이 허용 되지 않기 때문에 응용 프로그램에서 인수 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-140">If you try to run the application now, the application throws an argument exception because empty strings are not allowed for the parameters.</span></span> <span data-ttu-id="6f1ca-141">유효한 값을 제공 하려면 다음 섹션에 표시 된 것 처럼 외부 공급자를 사용 하 여 웹 사이트를 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-141">To provide valid values, you must register your web site with the external providers, as shown in the next section.</span></span>

## <a name="registering-with-an-external-provider"></a><span data-ttu-id="6f1ca-142">외부 공급자를 사용 하 여 등록</span><span class="sxs-lookup"><span data-stu-id="6f1ca-142">Registering with an external provider</span></span>

<span data-ttu-id="6f1ca-143">외부 공급자의 자격 증명을 사용 하 여 사용자를 인증 하려면 웹 사이트를 공급자에 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-143">To authenticate users with credentials from an external provider, you must register your web site with the provider.</span></span> <span data-ttu-id="6f1ca-144">사이트를 등록 하면 클라이언트를 등록할 때 포함 하는 매개 변수 (예: 키 또는 id, 암호)가 수신 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-144">When you register your site, you will receive the parameters (such as key or id, and secret) to include when registering the client.</span></span> <span data-ttu-id="6f1ca-145">사용할 공급자가 포함 된 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-145">You must have an account with the providers you wish to use.</span></span>

<span data-ttu-id="6f1ca-146">이 자습서에서는 이러한 공급자에 등록 하기 위해 수행 해야 하는 단계를 모두 보여 주지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-146">This tutorial does not show all of the steps you must perform to register with these providers.</span></span> <span data-ttu-id="6f1ca-147">일반적으로이 단계는 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-147">The steps are typically not difficult.</span></span> <span data-ttu-id="6f1ca-148">사이트를 성공적으로 등록 하려면 해당 사이트에서 제공 하는 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-148">To successfully register your site, follow the instructions provided on those sites.</span></span> <span data-ttu-id="6f1ca-149">사이트 등록을 시작 하려면 다음에 대 한 개발자 사이트를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-149">To get started with registering your site, see the developer site for:</span></span>

- [<span data-ttu-id="6f1ca-150">Facebook</span><span class="sxs-lookup"><span data-stu-id="6f1ca-150">Facebook</span></span>](https://developers.facebook.com/)
- [<span data-ttu-id="6f1ca-151">Google</span><span class="sxs-lookup"><span data-stu-id="6f1ca-151">Google</span></span>](https://developers.google.com/)
- [<span data-ttu-id="6f1ca-152">Microsoft</span><span class="sxs-lookup"><span data-stu-id="6f1ca-152">Microsoft</span></span>](http://manage.dev.live.com/)
- [<span data-ttu-id="6f1ca-153">Twitter</span><span class="sxs-lookup"><span data-stu-id="6f1ca-153">Twitter</span></span>](https://dev.twitter.com/)

<span data-ttu-id="6f1ca-154">Facebook을 사용 하 여 사이트를 등록 하는 경우 아래 이미지에 나와 있는 것 처럼 사이트 도메인에 대 한 &quot;localhost&quot;를 제공 하 고 URL에 대해 `&quot; http://localhost/&quot;` 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-154">When registering your site with Facebook, you can provide &quot;localhost&quot; for the site domain and `&quot;http://localhost/&quot;` for the URL, as shown in the image below.</span></span> <span data-ttu-id="6f1ca-155">Localhost를 사용 하는 것은 대부분의 공급자에서 작동 하지만 현재 Microsoft 공급자와는 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-155">Using localhost works with most providers, but currently does not work with the Microsoft provider.</span></span> <span data-ttu-id="6f1ca-156">Microsoft 공급자의 경우 올바른 웹 사이트 URL을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-156">For the Microsoft provider, you must include a valid web site URL.</span></span>

![사이트 등록](using-oauth-providers-with-mvc/_static/image4.png)

<span data-ttu-id="6f1ca-158">이전 이미지에서 앱 id, 앱 비밀 및 연락처 전자 메일의 값이 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-158">In the previous image, the values for the app id, app secret, and contact email have been removed.</span></span> <span data-ttu-id="6f1ca-159">실제로 사이트를 등록 하는 경우 해당 값이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-159">When you actually register your site, those values will be present.</span></span> <span data-ttu-id="6f1ca-160">앱 id 및 앱 암호에 대 한 값을 응용 프로그램에 추가할 것 이므로이를 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-160">You will want to note the values for app id and app secret because you will add them to your application.</span></span>

## <a name="creating-test-users"></a><span data-ttu-id="6f1ca-161">테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="6f1ca-161">Creating test users</span></span>

<span data-ttu-id="6f1ca-162">기존 Facebook 계정을 사용 하 여 사이트를 테스트 하지 않을 경우이 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-162">If you do not mind using an existing Facebook account to test your site, you can skip this section.</span></span>

<span data-ttu-id="6f1ca-163">Facebook 앱 관리 페이지에서 응용 프로그램에 대 한 테스트 사용자를 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-163">You can easily create test users for your application within the Facebook app management page.</span></span> <span data-ttu-id="6f1ca-164">이러한 테스트 계정을 사용 하 여 사이트에 로그인 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-164">You can use these test accounts to log in to your site.</span></span> <span data-ttu-id="6f1ca-165">왼쪽 탐색 창에서 **역할** 링크를 클릭 하 고 **만들기** 링크를 클릭 하 여 테스트 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-165">You create test users by clicking the **Roles** link in the left navigation pane and the clicking the **Create** link.</span></span>

![테스트 사용자 만들기](using-oauth-providers-with-mvc/_static/image5.png)

<span data-ttu-id="6f1ca-167">Facebook 사이트에서 자동으로 요청 하는 테스트 계정 수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-167">The Facebook site automatically creates the number of test accounts that you request.</span></span>

## <a name="adding-application-id-and-secret-from-the-provider"></a><span data-ttu-id="6f1ca-168">공급자의 응용 프로그램 id 및 암호를 추가 하는 중</span><span class="sxs-lookup"><span data-stu-id="6f1ca-168">Adding application id and secret from the provider</span></span>

<span data-ttu-id="6f1ca-169">이제 Facebook에서 id 및 암호를 수신 했으므로 AuthConfig 파일로 돌아가서 매개 변수 값으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-169">Now that you have received the id and secret from Facebook, go back to the AuthConfig file and add them as the parameter values.</span></span> <span data-ttu-id="6f1ca-170">아래 표시 된 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-170">The values shown below are not real values.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample3.cs)]

## <a name="log-in-with-external-credentials"></a><span data-ttu-id="6f1ca-171">외부 자격 증명으로 로그인</span><span class="sxs-lookup"><span data-stu-id="6f1ca-171">Log in with external credentials</span></span>

<span data-ttu-id="6f1ca-172">사이트에서 외부 자격 증명을 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-172">That is all you have to do to enable external credentials in your site.</span></span> <span data-ttu-id="6f1ca-173">응용 프로그램을 실행 하 고 오른쪽 위 모서리의 로그인 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-173">Run your application and click the login link in the upper right corner.</span></span> <span data-ttu-id="6f1ca-174">템플릿은 Facebook을 공급자로 등록 하 고 공급자 단추를 포함 한다는 것을 자동으로 인식 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-174">The template automatically recognizes that you have registered Facebook as a provider and includes a button for the provider.</span></span> <span data-ttu-id="6f1ca-175">여러 공급자를 등록 하는 경우 각각에 대 한 단추가 자동으로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-175">If you register multiple providers, a button for each one is automatically included.</span></span>

![외부 로그인](using-oauth-providers-with-mvc/_static/image6.png)

<span data-ttu-id="6f1ca-177">이 자습서에서는 외부 공급자에 대 한 로그인 단추를 사용자 지정 하는 방법에 대해서는 설명 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-177">This tutorial does not cover how to customize the log in buttons for the external providers.</span></span> <span data-ttu-id="6f1ca-178">해당 정보는 [OAuth/openid connect 사용 시 로그인 UI 사용자 지정](https://blogs.msdn.com/b/pranav_rastogi/archive/2012/08/24/customizing-the-login-ui-when-using-oauth-openid.aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-178">For that information, see [Customizing the login UI when using OAuth/OpenID](https://blogs.msdn.com/b/pranav_rastogi/archive/2012/08/24/customizing-the-login-ui-when-using-oauth-openid.aspx).</span></span>

<span data-ttu-id="6f1ca-179">Facebook 단추를 클릭 하 여 Facebook 자격 증명으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-179">Click on the Facebook button to log in with Facebook credentials.</span></span> <span data-ttu-id="6f1ca-180">외부 공급자 중 하나를 선택 하면 해당 사이트로 리디렉션되고 해당 서비스에 로그인 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-180">When you select one of the external providers, you are redirected to that site and prompted by that service to log in.</span></span>

<span data-ttu-id="6f1ca-181">다음 이미지는 Facebook의 로그인 화면을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-181">The following image shows the login screen for Facebook.</span></span> <span data-ttu-id="6f1ca-182">Facebook 계정을 사용 하 여 oauthmvcexample 이라는 사이트에 로그인 하는 것을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-182">It notes that you are using your Facebook account to log in to a site named oauthmvcexample.</span></span>

![facebook 인증](using-oauth-providers-with-mvc/_static/image7.png)

<span data-ttu-id="6f1ca-184">Facebook 자격 증명을 사용 하 여 로그인 한 후에는 사이트에서 기본 정보에 액세스할 수 있음을 사용자에 게 알립니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-184">After logging in with Facebook credentials, a page informs the user that the site will have access to basic information.</span></span>

![권한 요청](using-oauth-providers-with-mvc/_static/image8.png)

<span data-ttu-id="6f1ca-186">**앱으로 이동**을 선택한 후에는 사용자가 사이트에 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-186">After selecting **Go to App**, the user must register for the site.</span></span> <span data-ttu-id="6f1ca-187">다음 그림은 사용자가 Facebook 자격 증명으로 로그인 한 후 등록 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-187">The following image shows the registration page after a user has logged in with Facebook credentials.</span></span> <span data-ttu-id="6f1ca-188">사용자 이름은 일반적으로 공급자의 이름으로 미리 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-188">The user name is typically pre-filled with a name from the provider.</span></span>

![register](using-oauth-providers-with-mvc/_static/image9.png)

<span data-ttu-id="6f1ca-190">등록 **을 클릭** 하 여 등록을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-190">Click **Register** to complete registration.</span></span> <span data-ttu-id="6f1ca-191">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-191">Close the browser.</span></span>

<span data-ttu-id="6f1ca-192">새 계정이 데이터베이스에 추가 된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-192">You can see that the new account has been added to your database.</span></span> <span data-ttu-id="6f1ca-193">서버 탐색기에서 **Defaultconnection** 데이터베이스를 열고 **Tables** 폴더를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-193">In Server Explorer, open the **DefaultConnection** database and open the **Tables** folder.</span></span>

![데이터베이스 테이블](using-oauth-providers-with-mvc/_static/image10.png)

<span data-ttu-id="6f1ca-195">**UserProfile** 테이블을 마우스 오른쪽 단추로 클릭 하 고 **테이블 데이터 표시**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-195">Right-click the **UserProfile** table and select **Show Table Data**.</span></span>

![데이터 표시](using-oauth-providers-with-mvc/_static/image11.png)

<span data-ttu-id="6f1ca-197">추가한 새 계정이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-197">You will see the new account you added.</span></span> <span data-ttu-id="6f1ca-198">**웹 페이지\_OAuthMembership** 테이블의 데이터를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-198">Look at the data in **webpage\_OAuthMembership** table.</span></span> <span data-ttu-id="6f1ca-199">방금 추가한 계정에 대 한 외부 공급자와 관련 된 추가 데이터가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-199">You will see more data related to the external provider for the account you just added.</span></span>

<span data-ttu-id="6f1ca-200">외부 인증만 사용 하도록 설정 하려면 작업이 완료 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-200">If you only want to enable external authentication, you are done.</span></span> <span data-ttu-id="6f1ca-201">그러나 다음 섹션에 표시 된 것 처럼 공급자의 정보를 새 사용자 등록 프로세스에 추가로 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-201">However, you can further integrate information from the provider into the new user registration process, as shown in the following sections.</span></span>

## <a name="create-models-for-additional-user-information"></a><span data-ttu-id="6f1ca-202">추가 사용자 정보에 대 한 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="6f1ca-202">Create models for additional user information</span></span>

<span data-ttu-id="6f1ca-203">이전 섹션에서 설명한 것 처럼, 기본 제공 계정 등록이 작동 하기 위해 추가 정보를 검색할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-203">As you noticed in the previous sections, you do not need to retrieve any additional information for the built-in account registration to work.</span></span> <span data-ttu-id="6f1ca-204">그러나 대부분의 외부 공급자는 사용자에 대 한 추가 정보를 다시 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-204">However, most external providers pass back additional information about the user.</span></span> <span data-ttu-id="6f1ca-205">다음 섹션에서는 해당 정보를 유지 하 고 데이터베이스에 저장 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-205">The following sections show how to retain that information and save it to a database.</span></span> <span data-ttu-id="6f1ca-206">특히 사용자의 전체 이름, 사용자 개인 웹 페이지의 URI 및 Facebook이 계정을 확인 했는지 여부를 나타내는 값에 대 한 값을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-206">Specifically, you will retain values for the user's full name, the URI of the user's personal web page, and a value that indicates whether Facebook has verified the account.</span></span>

<span data-ttu-id="6f1ca-207">[Code First 마이그레이션](https://msdn.microsoft.com/data/jj591621) 를 사용 하 여 추가 사용자 정보를 저장 하는 테이블을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-207">You will use [Code First Migrations](https://msdn.microsoft.com/data/jj591621) to add a table for storing additional user information.</span></span> <span data-ttu-id="6f1ca-208">기존 데이터베이스에 테이블을 추가 하는 것 이므로 먼저 현재 데이터베이스의 스냅숏을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-208">You are adding the table to an existing database, so you will first need to create a snapshot of the current database.</span></span> <span data-ttu-id="6f1ca-209">현재 데이터베이스의 스냅숏을 만들면 나중에 새 테이블만 포함 하는 마이그레이션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-209">By creating a snapshot of the current database, you can later create a migration that contains only the new table.</span></span> <span data-ttu-id="6f1ca-210">현재 데이터베이스의 스냅숏을 만들려면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-210">To create a snapshot of the current database:</span></span>

1. <span data-ttu-id="6f1ca-211">**패키지 관리자 콘솔** 을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-211">Open the **Package Manager Console**</span></span>
2. <span data-ttu-id="6f1ca-212">**사용-마이그레이션** 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-212">Run the command **enable-migrations**</span></span>
3. <span data-ttu-id="6f1ca-213">명령 **추가-마이그레이션 초기 – IgnoreChanges** 를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-213">Run the command **add-migration initial –IgnoreChanges**</span></span>
4. <span data-ttu-id="6f1ca-214">**Update-database** 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-214">Run the command **update-database**</span></span>

<span data-ttu-id="6f1ca-215">이제 새 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-215">Now, you will add the new properties.</span></span> <span data-ttu-id="6f1ca-216">모델 폴더에서 AccountModels.cs 파일을 열고 RegisterExternalLoginModel 클래스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-216">In the Models folder, open the AccountModels.cs file, and find the RegisterExternalLoginModel class.</span></span> <span data-ttu-id="6f1ca-217">RegisterExternalLoginModel 클래스에는 인증 공급자에서 반환 되는 값이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-217">The RegisterExternalLoginModel class holds values that come back from the authentication provider.</span></span> <span data-ttu-id="6f1ca-218">아래 강조 표시 된 것 처럼 FullName 및 Link 라는 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-218">Add properties named FullName and Link, as highlighted below.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample4.cs?highlight=9-13)]

<span data-ttu-id="6f1ca-219">또한 AccountModels.cs에서 ExtraUserInformation 라는 새 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-219">Also in AccountModels.cs, add a new class called ExtraUserInformation.</span></span> <span data-ttu-id="6f1ca-220">이 클래스는 데이터베이스에 생성 되는 새 테이블을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-220">This class represents the new table which will be created in the database.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample5.cs)]

<span data-ttu-id="6f1ca-221">새 클래스에 대 한 DbSet 속성을 만들기 위해 users 컨텍스트 클래스에서 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-221">In the UsersContext class, add the highlighted code below to create a DbSet property for the new class.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample6.cs?highlight=9)]

<span data-ttu-id="6f1ca-222">이제 새 테이블을 만들 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-222">You are now ready to create the new table.</span></span> <span data-ttu-id="6f1ca-223">다음 시간에 패키지 관리자 콘솔을 다시 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-223">Open the Package Manager Console again and this time:</span></span>

1. <span data-ttu-id="6f1ca-224">**Add Migration AddExtraUserInformation** 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-224">Run the command **add-migration AddExtraUserInformation**</span></span>
2. <span data-ttu-id="6f1ca-225">**Update-database** 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-225">Run the command **update-database**</span></span>

<span data-ttu-id="6f1ca-226">이제 새 테이블이 데이터베이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-226">The new table now exists in the database.</span></span>

## <a name="retrieve-the-additional-data"></a><span data-ttu-id="6f1ca-227">추가 데이터 검색</span><span class="sxs-lookup"><span data-stu-id="6f1ca-227">Retrieve the additional data</span></span>

<span data-ttu-id="6f1ca-228">추가 사용자 데이터를 검색 하는 방법에는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-228">There are two ways to retrieve additional user data.</span></span> <span data-ttu-id="6f1ca-229">첫 번째 방법은 인증 요청 중에 기본적으로 다시 전달 되는 사용자 데이터를 유지 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-229">The first way is to retain user data that is passed back, by default, during the authentication request.</span></span> <span data-ttu-id="6f1ca-230">두 번째 방법은 특히 공급자 API를 호출 하 고 자세한 정보를 요청 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-230">The second way is to specifically call the provider API and request more information.</span></span> <span data-ttu-id="6f1ca-231">FullName 및 Link에 대 한 값은 Facebook에 의해 자동으로 다시 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-231">Values for FullName and Link are automatically passed back by Facebook.</span></span> <span data-ttu-id="6f1ca-232">Facebook에서 Facebook API에 대 한 호출을 통해 계정이 검색 되었는지 여부를 나타내는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-232">A value that indicates whether Facebook has verified the account is retrieved through a call to the Facebook API.</span></span> <span data-ttu-id="6f1ca-233">먼저 FullName 및 Link에 대 한 값을 채운 후 나중에 확인 된 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-233">First, you will populate values for FullName and Link, and then later, you will get the verified value.</span></span>

<span data-ttu-id="6f1ca-234">추가 사용자 데이터를 검색 하려면 **Controllers** 폴더에서 **AccountController.cs** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-234">To retrieve the additional user data, open the **AccountController.cs** file in the **Controllers** folder.</span></span>

<span data-ttu-id="6f1ca-235">이 파일에는 계정을 로깅, 등록 및 관리 하는 논리가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-235">This file contains the logic for logging, registering, and managing accounts.</span></span> <span data-ttu-id="6f1ca-236">특히 **ExternalLoginCallback** 및 **ExternalLoginConfirmation**라는 메서드를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-236">In particular, notice the methods called **ExternalLoginCallback** and **ExternalLoginConfirmation**.</span></span> <span data-ttu-id="6f1ca-237">이러한 메서드 내에서 코드를 추가 하 여 응용 프로그램에 대 한 외부 로그인 작업을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-237">Within these methods, you can add code to customize external login operations for your application.</span></span> <span data-ttu-id="6f1ca-238">**ExternalLoginCallback** 메서드의 첫 번째 줄에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-238">The first line of the **ExternalLoginCallback** method contains:</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample7.cs)]

<span data-ttu-id="6f1ca-239">**Verifyauthentication** 메서드에서 반환 된 **Authenticationresult** 개체의 **ExtraData** 속성에 추가 사용자 데이터가 다시 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-239">Additional user data is passed back in the **ExtraData** property of the **AuthenticationResult** object that is returned from the **VerifyAuthentication** method.</span></span> <span data-ttu-id="6f1ca-240">Facebook 클라이언트는 **ExtraData** 속성에 다음과 같은 값을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-240">The Facebook client contains the following values in the **ExtraData** property:</span></span>

- <span data-ttu-id="6f1ca-241">id</span><span class="sxs-lookup"><span data-stu-id="6f1ca-241">id</span></span>
- <span data-ttu-id="6f1ca-242">name</span><span class="sxs-lookup"><span data-stu-id="6f1ca-242">name</span></span>
- <span data-ttu-id="6f1ca-243">link</span><span class="sxs-lookup"><span data-stu-id="6f1ca-243">link</span></span>
- <span data-ttu-id="6f1ca-244">gender</span><span class="sxs-lookup"><span data-stu-id="6f1ca-244">gender</span></span>
- <span data-ttu-id="6f1ca-245">accesstoken</span><span class="sxs-lookup"><span data-stu-id="6f1ca-245">accesstoken</span></span>

<span data-ttu-id="6f1ca-246">ExtraData 속성에서 다른 공급자는 비슷하지만 약간 다른 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-246">Other providers will have similar but slightly different data in the ExtraData property.</span></span>

<span data-ttu-id="6f1ca-247">사용자가 사이트를 처음 사용 하는 경우 일부 추가 데이터를 검색 하 고 해당 데이터를 확인 보기에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-247">If the user is new to your site, you will retrieve some the additional data and pass that data to the confirmation view.</span></span> <span data-ttu-id="6f1ca-248">메서드의 마지막 코드 블록은 사용자가 사이트를 처음 사용 하는 경우에만 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-248">The last block of code in the method is run only if the user is new to your site.</span></span> <span data-ttu-id="6f1ca-249">다음 줄을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-249">Replace the following line:</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample8.cs)]

<span data-ttu-id="6f1ca-250">다음 줄로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-250">With this line:</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample9.cs)]

<span data-ttu-id="6f1ca-251">이러한 변경에는 FullName 및 Link 속성에 대 한 값만 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-251">This change merely includes values for the FullName and Link properties.</span></span>

<span data-ttu-id="6f1ca-252">**ExternalLoginConfirmation** 메서드에서 아래 강조 표시 된 코드를 수정 하 여 추가 사용자 정보를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-252">In the **ExternalLoginConfirmation** method, modify the code as highlighted below to save the additional user information.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample10.cs?highlight=4,7-13)]

## <a name="adjusting-the-view"></a><span data-ttu-id="6f1ca-253">뷰 조정</span><span class="sxs-lookup"><span data-stu-id="6f1ca-253">Adjusting the view</span></span>

<span data-ttu-id="6f1ca-254">공급자에서 검색 하는 추가 사용자 데이터는 등록 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-254">The additional user data that you retrieve from the provider will be displayed in the registration page.</span></span>

<span data-ttu-id="6f1ca-255">**보기**/**계정** 폴더에서 **ExternalLoginConfirmation**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-255">In the **Views**/**Account** folder, open **ExternalLoginConfirmation.cshtml**.</span></span> <span data-ttu-id="6f1ca-256">사용자 이름에 대 한 기존 필드 아래에서 FullName, Link 및 Linklink에 대 한 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-256">Below the existing field for user name, add fields for FullName, Link, and PictureLink.</span></span>

[!code-cshtml[Main](using-oauth-providers-with-mvc/samples/sample11.cshtml)]

<span data-ttu-id="6f1ca-257">이제 응용 프로그램을 실행 하 고 저장 된 추가 정보를 사용 하 여 새 사용자를 등록할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-257">You are now almost ready to run the application and register a new user with the additional information saved.</span></span> <span data-ttu-id="6f1ca-258">사이트에 아직 등록 되지 않은 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-258">You must have an account that is not already registered with the site.</span></span> <span data-ttu-id="6f1ca-259">다른 테스트 계정을 사용 하거나, 다시 사용 하려는 계정에 대 한\_**UserProfile** 및 **웹 페이지** 의 행을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-259">You can either use a different test account, or delete the rows in the **UserProfile** and **webpages\_OAuthMembership** tables for the account you wish to reuse.</span></span> <span data-ttu-id="6f1ca-260">이러한 행을 삭제 하면 계정이 다시 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-260">By deleting those rows, you will ensure that the account is registered again.</span></span>

<span data-ttu-id="6f1ca-261">응용 프로그램을 실행 하 고 새 사용자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-261">Run the application and register the new user.</span></span> <span data-ttu-id="6f1ca-262">이번에는 확인 페이지에 더 많은 값이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-262">Notice that this time the confirmation page contains more values.</span></span>

![register](using-oauth-providers-with-mvc/_static/image12.png)

<span data-ttu-id="6f1ca-264">등록을 완료 한 후 브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-264">After completing registration, close the browser.</span></span> <span data-ttu-id="6f1ca-265">데이터베이스를 확인 하 여 **ExtraUserInformation** 테이블의 새 값을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-265">Look in the database to notice the new values in the **ExtraUserInformation** table.</span></span>

## <a name="install-nuget-package-for-facebook-api"></a><span data-ttu-id="6f1ca-266">Facebook API에 대 한 NuGet 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="6f1ca-266">Install NuGet package for Facebook API</span></span>

<span data-ttu-id="6f1ca-267">Facebook은 작업을 수행 하기 위해 호출할 수 있는 [API](https://developers.facebook.com/docs/reference/apis/) 를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-267">Facebook provides an [API](https://developers.facebook.com/docs/reference/apis/) that you can call to perform operations.</span></span> <span data-ttu-id="6f1ca-268">HTTP 요청을 전송 하거나 해당 요청을 쉽게 보낼 수 있도록 하는 NuGet 패키지 설치를 사용 하 여 Facebook API를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-268">You can call the Facebook API either by directing sending HTTP requests, or by using installing a NuGet package that facilitates sending those requests.</span></span> <span data-ttu-id="6f1ca-269">NuGet 패키지를 사용 하는 방법은이 자습서에 나와 있지만 NuGet 패키지 설치는 필수적이 지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-269">Using a NuGet package is shown in this tutorial, but installing NuGet package is not essential.</span></span> <span data-ttu-id="6f1ca-270">이 자습서에서는 Facebook C# SDK 패키지를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-270">This tutorial shows how to use the Facebook C# SDK package.</span></span> <span data-ttu-id="6f1ca-271">Facebook API 호출을 지 원하는 다른 NuGet 패키지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-271">There are other NuGet packages that assist with calling the Facebook API.</span></span>

<span data-ttu-id="6f1ca-272">**NuGet 패키지 관리** 창에서 Facebook C# SDK 패키지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-272">From the **Manage NuGet Packages** windows, select the Facebook C# SDK package.</span></span>

![패키지 설치](using-oauth-providers-with-mvc/_static/image13.png)

<span data-ttu-id="6f1ca-274">Facebook C# SDK를 사용 하 여 사용자에 대 한 액세스 토큰을 요구 하는 작업을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-274">You will use the Facebook C# SDK to call an operation that requires the access token for the user.</span></span> <span data-ttu-id="6f1ca-275">다음 섹션에서는 액세스 토큰을 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-275">The next section shows how to get the access token.</span></span>

## <a name="retrieve-access-token"></a><span data-ttu-id="6f1ca-276">액세스 토큰 검색</span><span class="sxs-lookup"><span data-stu-id="6f1ca-276">Retrieve access token</span></span>

<span data-ttu-id="6f1ca-277">대부분의 외부 공급자는 사용자의 자격 증명을 확인 한 후 액세스 토큰을 다시 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-277">Most external providers pass back an access token after the user's credentials are verified.</span></span> <span data-ttu-id="6f1ca-278">이 액세스 토큰은 인증 된 사용자만 사용할 수 있는 작업을 호출할 수 있도록 하기 때문에 매우 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-278">This access token is very important because it enables you to call operations that are only available to authenticated users.</span></span> <span data-ttu-id="6f1ca-279">따라서 더 많은 기능을 제공 하려는 경우 액세스 토큰을 검색 하 고 저장 하는 것이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-279">Therefore, retrieving and storing the access token is essential when you want to provide more functionality.</span></span>

<span data-ttu-id="6f1ca-280">외부 공급자에 따라 액세스 토큰은 제한 된 시간 동안만 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-280">Depending on the external provider, the access token may be valid for only a limited amount of time.</span></span> <span data-ttu-id="6f1ca-281">유효한 액세스 토큰이 있는지 확인 하기 위해 사용자가 로그인 할 때마다 검색 하 여 데이터베이스에 저장 하지 않고 세션 값으로 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-281">To ensure that you have a valid access token, you will retrieve it each time the user logs in, and store it as a session value rather than save it to a database.</span></span>

<span data-ttu-id="6f1ca-282">**ExternalLoginCallback** 메서드에서 액세스 토큰은 **Authenticationresult** 개체의 **ExtraData** 속성에도 다시 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-282">In the **ExternalLoginCallback** method, the access token is also passed back in the **ExtraData** property of the **AuthenticationResult** object.</span></span> <span data-ttu-id="6f1ca-283">강조 표시 된 코드를 **ExternalLoginCallback** 에 추가 하 여 액세스 토큰을 **세션** 개체에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-283">Add the highlighted code to **ExternalLoginCallback** to save the access token in the **Session** object.</span></span> <span data-ttu-id="6f1ca-284">이 코드는 사용자가 Facebook 계정으로 로그인 할 때마다 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-284">This code is run every time the user logs in with a Facebook account.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample12.cs?highlight=11-14)]

<span data-ttu-id="6f1ca-285">이 예제에서는 Facebook에서 액세스 토큰을 검색 하지만 &quot;accesstoken&quot;라는 동일한 키를 통해 외부 공급자에서 액세스 토큰을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-285">Although this example retrieves an access token from Facebook, you can retrieve the access token from any external provider through the same key named &quot;accesstoken&quot;.</span></span>

## <a name="logging-off"></a><span data-ttu-id="6f1ca-286">로그오프 중</span><span class="sxs-lookup"><span data-stu-id="6f1ca-286">Logging off</span></span>

<span data-ttu-id="6f1ca-287">기본 **로그 오프** 메서드는 사용자를 응용 프로그램에서 로그 아웃 하지만 외부 공급자에서 사용자를 로그 아웃 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-287">The default **LogOff** method logs the user out of your application, but does not log the user out of the external provider.</span></span> <span data-ttu-id="6f1ca-288">사용자를 Facebook에서 로그 오프 하 고 사용자가 로그 오프 한 후에도 토큰이 지속 되지 않도록 하려면 다음 강조 표시 된 코드를 AccountController의 **LogOff** 메서드에 추가 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-288">To log the user out of Facebook, and prevent the token from persisting after the user has logged off, you can add the following highlighted code to the **LogOff** method in the AccountController.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample13.cs?highlight=6-14)]

<span data-ttu-id="6f1ca-289">`next` 매개 변수에 제공 하는 값은 사용자가 Facebook에서 로그 아웃 한 후에 사용할 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-289">The value you provide in the `next` parameter is the URL to use after the user has logged out of Facebook.</span></span> <span data-ttu-id="6f1ca-290">로컬 컴퓨터에서 테스트 하는 경우 로컬 사이트에 올바른 포트 번호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-290">When testing on your local computer, you would provide the correct port number for your local site.</span></span> <span data-ttu-id="6f1ca-291">프로덕션 환경에서는 contoso.com와 같은 기본 페이지를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-291">In production, you would provide a default page, such as contoso.com.</span></span>

## <a name="retrieve-user-information-that-requires-the-access-token"></a><span data-ttu-id="6f1ca-292">액세스 토큰이 필요한 사용자 정보를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-292">Retrieve user information that requires the access token</span></span>

<span data-ttu-id="6f1ca-293">액세스 토큰을 저장 하 고 Facebook C# SDK 패키지를 설치 했으므로 이제이를 함께 사용 하 여 facebook에서 추가 사용자 정보를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-293">Now that you have stored the access token and installed the Facebook C# SDK package, you can use them together to request additional user information from Facebook.</span></span> <span data-ttu-id="6f1ca-294">**ExternalLoginConfirmation** 메서드에서 액세스 토큰의 값을 전달 하 여 **FacebookClient** 클래스의 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-294">In the **ExternalLoginConfirmation** method, create an instance of the **FacebookClient** class by passing the value of the access token.</span></span> <span data-ttu-id="6f1ca-295">현재 인증 된 사용자에 대해 **확인** 된 속성 값을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-295">Request the value of the **verified** property for the current, authenticated user.</span></span> <span data-ttu-id="6f1ca-296">**확인** 된 속성은 Facebook이 다른 방법 (예: 휴대폰으로 메시지 보내기)을 통해 계정의 유효성을 검사 했는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-296">The **verified** property indicates whether Facebook has validated the account through some other means, such as sending a message to a cell phone.</span></span> <span data-ttu-id="6f1ca-297">이 값을 데이터베이스에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-297">Save this value in the database.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample14.cs?highlight=7-18,25)]

<span data-ttu-id="6f1ca-298">사용자에 대 한 데이터베이스의 레코드를 삭제 하거나 다른 Facebook 계정을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-298">You will again need to either delete the records in the database for the user, or use a different Facebook account.</span></span>

<span data-ttu-id="6f1ca-299">응용 프로그램을 실행 하 고 새 사용자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-299">Run the application, and register the new user.</span></span> <span data-ttu-id="6f1ca-300">**ExtraUserInformation** 테이블을 확인 하 여 확인 된 속성의 값을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-300">Look at the **ExtraUserInformation** table to see the value for the Verified property.</span></span>

## <a name="conclusion"></a><span data-ttu-id="6f1ca-301">결론</span><span class="sxs-lookup"><span data-stu-id="6f1ca-301">Conclusion</span></span>

<span data-ttu-id="6f1ca-302">이 자습서에서는 사용자 인증 및 등록 데이터를 위해 Facebook과 통합 된 사이트를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-302">In this tutorial, you created a site that is integrated with Facebook for user authentication and registration data.</span></span> <span data-ttu-id="6f1ca-303">MVC 4 웹 응용 프로그램에 대해 설정 되는 기본 동작과 기본 동작을 사용자 지정 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-303">You learned about the default behavior that is set up for MVC 4 web application, and how to customize that default behavior.</span></span>

## <a name="related-topics"></a><span data-ttu-id="6f1ca-304">관련 항목</span><span class="sxs-lookup"><span data-stu-id="6f1ca-304">Related topics</span></span>

- [<span data-ttu-id="6f1ca-305">인증 및 SQL DB를 사용하여 ASP.NET MVC 앱을 만들고 Azure App Service에 배포</span><span class="sxs-lookup"><span data-stu-id="6f1ca-305">Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service</span></span>](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)
