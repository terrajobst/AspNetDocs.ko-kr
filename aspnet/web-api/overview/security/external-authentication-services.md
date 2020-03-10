---
uid: web-api/overview/security/external-authentication-services
title: ASP.NET Web API (C#)를 사용 하는 외부 인증 서비스 | Microsoft Docs
author: rmcmurray
description: ASP.NET Web API에서 외부 인증 서비스를 사용 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 3bb8eb15-b518-44f5-a67d-a27e051aedc6
msc.legacyurl: /web-api/overview/security/external-authentication-services
msc.type: authoredcontent
ms.openlocfilehash: b2571552a3f8040ff42bfa0a9fa48981f71a1e4b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447419"
---
# <a name="external-authentication-services-with-aspnet-web-api-c"></a><span data-ttu-id="2f1ba-103">ASP.NET Web API (C#)을 사용 하는 외부 인증 서비스</span><span class="sxs-lookup"><span data-stu-id="2f1ba-103">External Authentication Services with ASP.NET Web API (C#)</span></span>

<span data-ttu-id="2f1ba-104">Visual Studio 2017 및 ASP.NET 4.7.2는 SPA ( [단일 페이지 응용 프로그램](../../../single-page-application/index.md) ) 및 [Web API](../../index.md) 서비스에 대 한 보안 옵션을 확장 하 여 여러 OAuth/openid connect 및 소셜 미디어 인증 서비스 (Microsoft 계정, Twitter, Facebook, Google 등)를 포함 하는 외부 인증 서비스와 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-104">Visual Studio 2017 and ASP.NET 4.7.2 expand the security options for [Single Page Applications](../../../single-page-application/index.md) (SPA) and [Web API](../../index.md) services to integrate with external authentication services, which include several OAuth/OpenID and social media authentication services: Microsoft Accounts, Twitter, Facebook, and Google.</span></span>  

### <a name="in-this-walkthrough"></a><span data-ttu-id="2f1ba-105">이 연습에서</span><span class="sxs-lookup"><span data-stu-id="2f1ba-105">In this Walkthrough</span></span>

- [<span data-ttu-id="2f1ba-106">외부 인증 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="2f1ba-106">Using External Authentication Services</span></span>](#USING)
- [<span data-ttu-id="2f1ba-107">샘플 웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="2f1ba-107">Creating the Sample Web Application</span></span>](#SAMPLE)
- [<span data-ttu-id="2f1ba-108">Facebook 인증 사용</span><span class="sxs-lookup"><span data-stu-id="2f1ba-108">Enabling Facebook Authentication</span></span>](#FACEBOOK)
- [<span data-ttu-id="2f1ba-109">Google 인증 사용</span><span class="sxs-lookup"><span data-stu-id="2f1ba-109">Enabling Google Authentication</span></span>](#GOOGLE)
- [<span data-ttu-id="2f1ba-110">Microsoft 인증 사용</span><span class="sxs-lookup"><span data-stu-id="2f1ba-110">Enabling Microsoft Authentication</span></span>](#MICROSOFT)
- [<span data-ttu-id="2f1ba-111">Twitter 인증 사용</span><span class="sxs-lookup"><span data-stu-id="2f1ba-111">Enabling Twitter Authentication</span></span>](#TWITTER)
- [<span data-ttu-id="2f1ba-112">추가 정보</span><span class="sxs-lookup"><span data-stu-id="2f1ba-112">Additional Information</span></span>](#MOREINFO)

    - [<span data-ttu-id="2f1ba-113">외부 인증 서비스 결합</span><span class="sxs-lookup"><span data-stu-id="2f1ba-113">Combining External Authentication Services</span></span>](#COMBINE)
    - [<span data-ttu-id="2f1ba-114">정규화 된 도메인 이름을 사용 하도록 IIS Express 구성</span><span class="sxs-lookup"><span data-stu-id="2f1ba-114">Configuring IIS Express to use a Fully Qualified Domain Name</span></span>](#FQDN)
    - [<span data-ttu-id="2f1ba-115">Microsoft 인증에 대 한 응용 프로그램 설정을 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="2f1ba-115">How to Obtain your Application Settings for Microsoft Authentication</span></span>](#OBTAIN)
    - [<span data-ttu-id="2f1ba-116">선택 사항: 로컬 등록 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="2f1ba-116">Optional: Disable Local Registration</span></span>](#DISABLE)

### <a name="prerequisites"></a><span data-ttu-id="2f1ba-117">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="2f1ba-117">Prerequisites</span></span>

<span data-ttu-id="2f1ba-118">이 연습의 예제를 따르려면 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-118">To follow the examples in this walkthrough, you need to have the following:</span></span>

- <span data-ttu-id="2f1ba-119">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="2f1ba-119">Visual Studio 2017</span></span>
- <span data-ttu-id="2f1ba-120">다음 소셜 미디어 인증 서비스 중 하나에 대 한 응용 프로그램 식별자 및 비밀 키가 포함 된 개발자 계정:</span><span class="sxs-lookup"><span data-stu-id="2f1ba-120">A developer account with the application identifier and secret key for one of the following social media authentication services:</span></span>

  - <span data-ttu-id="2f1ba-121">Microsoft 계정 ([https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070))</span><span class="sxs-lookup"><span data-stu-id="2f1ba-121">Microsoft Accounts ([https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070))</span></span>
  - <span data-ttu-id="2f1ba-122">Twitter ([https://dev.twitter.com/](https://dev.twitter.com/))</span><span class="sxs-lookup"><span data-stu-id="2f1ba-122">Twitter ([https://dev.twitter.com/](https://dev.twitter.com/))</span></span>
  - <span data-ttu-id="2f1ba-123">Facebook ([https://developers.facebook.com/](https://developers.facebook.com/))</span><span class="sxs-lookup"><span data-stu-id="2f1ba-123">Facebook ([https://developers.facebook.com/](https://developers.facebook.com/))</span></span>
  - <span data-ttu-id="2f1ba-124">Google ([https://developers.google.com/](https://developers.google.com))</span><span class="sxs-lookup"><span data-stu-id="2f1ba-124">Google ([https://developers.google.com/](https://developers.google.com))</span></span>

<a id="USING"></a>
## <a name="using-external-authentication-services"></a><span data-ttu-id="2f1ba-125">외부 인증 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="2f1ba-125">Using External Authentication Services</span></span>

<span data-ttu-id="2f1ba-126">현재 웹 개발자에 게 제공 되는 외부 인증 서비스는 새 웹 응용 프로그램을 만들 때 개발 시간을 단축 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-126">The abundance of external authentication services that are currently available to web developers help to reduce development time when creating new web applications.</span></span> <span data-ttu-id="2f1ba-127">일반적으로 웹 사용자는 널리 사용 되는 웹 서비스 및 소셜 미디어 웹 사이트용으로 여러 기존 계정을 포함 하므로 웹 응용 프로그램은 외부 웹 서비스 또는 소셜 미디어 웹 사이트의 인증 서비스를 구현할 때 개발 시간을 저장 합니다. 인증 구현을 만드는 데 소요 된 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-127">Web users typically have several existing accounts for popular web services and social media websites, therefore when a web application implements the authentication services from an external web service or social media website, it saves the development time that would have been spent creating an authentication implementation.</span></span> <span data-ttu-id="2f1ba-128">외부 인증 서비스를 사용 하면 최종 사용자가 웹 응용 프로그램에 대 한 다른 계정을 만들 필요가 없으며 다른 사용자 이름과 암호를 기억할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-128">Using an external authentication service saves end users from having to create another account for your web application, and also from having to remember another username and password.</span></span>

<span data-ttu-id="2f1ba-129">이전에는 개발자에 게 고유한 인증 구현을 만들거나 외부 인증 서비스를 응용 프로그램에 통합 하는 방법을 배울 수 있는 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-129">In the past, developers have had two choices: create their own authentication implementation, or learn how to integrate an external authentication service into their applications.</span></span> <span data-ttu-id="2f1ba-130">가장 기본적인 수준에서 다음 다이어그램은 외부 인증 서비스를 사용 하도록 구성 된 웹 응용 프로그램에서 정보를 요청 하는 사용자 에이전트 (웹 브라우저)의 간단한 요청 흐름을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-130">At the most basic level, the following diagram illustrates a simple request flow for a user agent (web browser) that is requesting information from a web application that is configured to use an external authentication service:</span></span>

[![](external-authentication-services/_static/image2.png "Click to Expand the Image")](external-authentication-services/_static/image1.png)

<span data-ttu-id="2f1ba-131">위의 다이어그램에서 사용자 에이전트 (또는이 예제의 웹 브라우저)는 웹 브라우저를 외부 인증 서비스로 리디렉션하는 웹 응용 프로그램에 요청을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-131">In the preceding diagram, the user agent (or web browser in this example) makes a request to a web application, which redirects the web browser to an external authentication service.</span></span> <span data-ttu-id="2f1ba-132">사용자 에이전트는 외부 인증 서비스에 자격 증명을 보내고, 사용자 에이전트가 성공적으로 인증 되 면 외부 인증 서비스는 사용자 에이전트를 원래 웹 응용 프로그램으로 리디렉션하여 사용자 에이전트가 웹 응용 프로그램에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-132">The user agent sends its credentials to the external authentication service, and if the user agent has successfully authenticated, the external authentication service will redirect the user agent to the original web application with some form of token which the user agent will send to the web application.</span></span> <span data-ttu-id="2f1ba-133">웹 응용 프로그램은 토큰을 사용 하 여 사용자 에이전트가 외부 인증 서비스에 의해 성공적으로 인증 되었는지 확인 하 고 웹 응용 프로그램은이 토큰을 사용 하 여 사용자 에이전트에 대 한 추가 정보를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-133">The web application will use the token to verify that the user agent has been successfully authenticated by the external authentication service, and the web application may use the token to gather more information about the user agent.</span></span> <span data-ttu-id="2f1ba-134">응용 프로그램이 사용자 에이전트 정보 처리를 완료 하면 웹 응용 프로그램은 권한 부여 설정에 따라 사용자 에이전트에 대 한 적절 한 응답을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-134">Once the application is done processing the user agent's information, the web application will return the appropriate response to the user agent based on its authorization settings.</span></span>

<span data-ttu-id="2f1ba-135">이 두 번째 예제에서는 사용자 에이전트가 웹 응용 프로그램 및 외부 권한 부여 서버와 협상 하 고 웹 응용 프로그램은 외부 권한 부여 서버와의 추가 통신을 수행 하 여 사용자에 대 한 추가 정보를 검색 합니다. 에이전트</span><span class="sxs-lookup"><span data-stu-id="2f1ba-135">In this second example, the user agent negotiates with the web application and external authorization server, and the web application performs additional communication with the external authorization server to retrieve additional information about the user agent:</span></span>

[![](external-authentication-services/_static/image4.png "Click to Expand the Image")](external-authentication-services/_static/image3.png)

<span data-ttu-id="2f1ba-136">Visual Studio 2017 및 ASP.NET 4.7.2는 다음 인증 서비스에 대 한 기본 제공 통합 기능을 제공 하 여 개발자를 위한 외부 인증 서비스와의 통합을 용이 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-136">Visual Studio 2017 and ASP.NET 4.7.2 make integration with external authentication services easier for developers by providing built-in integration for the following authentication services:</span></span>

- <span data-ttu-id="2f1ba-137">Facebook</span><span class="sxs-lookup"><span data-stu-id="2f1ba-137">Facebook</span></span>
- <span data-ttu-id="2f1ba-138">Google</span><span class="sxs-lookup"><span data-stu-id="2f1ba-138">Google</span></span>
- <span data-ttu-id="2f1ba-139">Microsoft 계정 (Windows Live ID 계정)</span><span class="sxs-lookup"><span data-stu-id="2f1ba-139">Microsoft Accounts (Windows Live ID accounts)</span></span>
- <span data-ttu-id="2f1ba-140">Twitter</span><span class="sxs-lookup"><span data-stu-id="2f1ba-140">Twitter</span></span>

<span data-ttu-id="2f1ba-141">이 연습의 예제에서는 Visual Studio 2017와 함께 제공 되는 새로운 ASP.NET 웹 응용 프로그램 템플릿을 사용 하 여 지원 되는 각 외부 인증 서비스를 구성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-141">The examples in this walkthrough will demonstrate how to configure each of the supported external authentication services by using the new ASP.NET Web Application template that ships with Visual Studio 2017.</span></span>

> [!NOTE]
> <span data-ttu-id="2f1ba-142">필요한 경우 외부 인증 서비스의 설정에 FQDN을 추가 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-142">If necessary, you may need to add your FQDN to the settings for your external authentication service.</span></span> <span data-ttu-id="2f1ba-143">이 요구 사항은 클라이언트에서 사용 하는 FQDN과 일치 하도록 응용 프로그램 설정의 FQDN을 요구 하는 일부 외부 인증 서비스에 대 한 보안 제약 조건을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-143">This requirement is based on security constraints for some external authentication services which require the FQDN in your application settings to match the FQDN that is used by your clients.</span></span> <span data-ttu-id="2f1ba-144">이에 대 한 단계는 각 외부 인증 서비스에 따라 크게 달라 집니다. 각 외부 인증 서비스에 대 한 설명서를 참조 하 여 필요한 경우와 이러한 설정을 구성 하는 방법을 확인 해야 합니다. 이 환경을 테스트 하는 데 FQDN을 사용 하도록 IIS Express를 구성 해야 하는 경우이 연습의 뒷부분에 나오는 [정규화 된 도메인 이름을 사용 하도록 IIS Express 구성](#FQDN) 섹션을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-144">(The steps for this will vary greatly for each external authentication service; you will need to consult the documentation for each external authentication service to see if this is required and how to configure these settings.) If you need to configure IIS Express to use an FQDN for testing this environment, see the [Configuring IIS Express to use a Fully Qualified Domain Name](#FQDN) section later in this walkthrough.</span></span>

<a id="SAMPLE"></a>
## <a name="create-a-sample-web-application"></a><span data-ttu-id="2f1ba-145">샘플 웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="2f1ba-145">Create a Sample Web Application</span></span>

<span data-ttu-id="2f1ba-146">다음 단계는 ASP.NET 웹 응용 프로그램 템플릿을 사용 하 여 샘플 응용 프로그램을 만드는 과정을 안내 하며,이 연습 뒷부분의 각 외부 인증 서비스에 대해이 샘플 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-146">The following steps will lead you through creating a sample application by using the ASP.NET Web Application template, and you will use this sample application for each of the external authentication services later in this walkthrough.</span></span>

<span data-ttu-id="2f1ba-147">Visual Studio 2017를 시작 하 고 시작 페이지에서 **새 프로젝트** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-147">Start Visual Studio 2017 and select **New Project** from the Start page.</span></span> <span data-ttu-id="2f1ba-148">또는 **파일** 메뉴에서 **새로 만들기** , **프로젝트**를 차례로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-148">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<!-- [![](external-authentication-services/_static/image6.png "Click to Expand the Image")](external-authentication-services/_static/image5.png) -->

<span data-ttu-id="2f1ba-149">**새 프로젝트** 대화 상자가 표시 되 면 **설치 됨** 을 선택 하 고 **시각적 C#개체** 를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-149">When the **New Project** dialog box is displayed, select **Installed** and expand **Visual C#**.</span></span> <span data-ttu-id="2f1ba-150">**시각적 개체 C#** 에서 **웹**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-150">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="2f1ba-151">프로젝트 템플릿 목록에서 **ASP.NET 웹 응용 프로그램 (.Net Framework)** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-151">In the list of project templates, select **ASP.NET Web Application (.Net Framework)**.</span></span> <span data-ttu-id="2f1ba-152">프로젝트의 이름을 입력 하 고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-152">Enter a name for your project and click **OK**.</span></span>

[![](external-authentication-services/_static/image71.png "Click to Expand the Image")](external-authentication-services/_static/image71.png)

<span data-ttu-id="2f1ba-153">**새 ASP.NET 프로젝트가** 표시 되 면 **단일 페이지 응용 프로그램** 템플릿을 선택 하 고 **프로젝트 만들기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-153">When the **New ASP.NET Project** is displayed, select the **Single Page Application** template and click **Create Project**.</span></span>

[![](external-authentication-services/_static/image72.png "Click to Expand the Image")](external-authentication-services/_static/image72.png)

<span data-ttu-id="2f1ba-154">Visual Studio 2017가 프로젝트를 만들 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-154">Wait as Visual Studio 2017 creates your project.</span></span>

<!-- [![](external-authentication-services/_static/image12.png "Click to Expand the Image")](external-authentication-services/_static/image11.png) -->

<span data-ttu-id="2f1ba-155">Visual Studio 2017가 프로젝트 만들기를 완료 하면 **앱\_시작** 폴더에 있는 *Startup.Auth.cs* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-155">When Visual Studio 2017 has finished creating your project, open the *Startup.Auth.cs* file that is located in the **App\_Start** folder.</span></span>

<span data-ttu-id="2f1ba-156">프로젝트를 처음 만들 때 *Startup.Auth.cs* file에서 외부 인증 서비스를 사용 하도록 설정 하지 않았습니다. 다음은 ASP.NET 응용 프로그램을 사용 하 여 Microsoft 계정, Twitter, Facebook 또는 Google 인증을 사용 하기 위해 외부 인증 서비스 및 모든 관련 설정을 사용 하도록 설정 하는 섹션을 강조 표시 하는 코드의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-156">When you first create the project, none of the external authentication services are enabled in *Startup.Auth.cs* file; the following illustrates what your code might resemble, with the sections highlighted for where you would enable an external authentication service and any relevant settings in order to use Microsoft Accounts, Twitter, Facebook, or Google authentication with your ASP.NET application:</span></span>

[!code-csharp[Main](external-authentication-services/samples/sample1.cs)]

<span data-ttu-id="2f1ba-157">F5 키를 눌러 웹 응용 프로그램을 빌드 및 디버그할 때 외부 인증 서비스가 정의 되지 않은 것을 볼 수 있는 로그인 화면이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-157">When you press F5 to build and debug your web application, it will display a login screen where you will see that no external authentication services have been defined.</span></span>

[![](external-authentication-services/_static/image73.png "Click to Expand the Image")](external-authentication-services/_static/image73.png)

<span data-ttu-id="2f1ba-158">다음 섹션에서는 Visual Studio 2017에서 ASP.NET와 함께 제공 되는 각 외부 인증 서비스를 사용 하도록 설정 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-158">In the following sections, you will learn how to enable each of the external authentication services that are provided with ASP.NET in Visual Studio 2017.</span></span>

<a id="FACEBOOK"></a>
## <a name="enabling-facebook-authentication"></a><span data-ttu-id="2f1ba-159">Facebook 인증 사용</span><span class="sxs-lookup"><span data-stu-id="2f1ba-159">Enabling Facebook authentication</span></span>

<span data-ttu-id="2f1ba-160">Facebook 인증을 사용 하려면 Facebook 개발자 계정을 만들어야 하며, 프로젝트에서 작동 하려면 Facebook의 응용 프로그램 ID 및 비밀 키가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-160">Using Facebook authentication requires you to create a Facebook developer account, and your project will require an application ID and secret key from Facebook in order to function.</span></span> <span data-ttu-id="2f1ba-161">Facebook 개발자 계정을 만들고 응용 프로그램 ID 및 비밀 키를 가져오는 방법에 대 한 자세한 내용은 [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-161">For information about creating a Facebook developer account and obtaining your application ID and secret key, see [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).</span></span>

<span data-ttu-id="2f1ba-162">응용 프로그램 ID 및 비밀 키를 가져온 후에는 다음 단계를 사용 하 여 웹 응용 프로그램에 대해 Facebook 인증을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-162">Once you have obtained your application ID and secret key, use the following steps to enable Facebook authentication for your web application:</span></span>

1. <span data-ttu-id="2f1ba-163">프로젝트가 Visual Studio 2017에서 열리면 *Startup.Auth.cs* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-163">When your project is open in Visual Studio 2017, open the *Startup.Auth.cs* file.</span></span>

2. <span data-ttu-id="2f1ba-164">코드의 Facebook 인증 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-164">Locate the Facebook authentication section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample2.cs)]
3. <span data-ttu-id="2f1ba-165">&quot;//&quot; 문자를 제거 하 여 강조 표시 된 코드 줄의 주석 처리를 제거 하 고 응용 프로그램 ID 및 비밀 키를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-165">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your application ID and secret key.</span></span> <span data-ttu-id="2f1ba-166">이러한 매개 변수를 추가한 후에는 프로젝트를 다시 컴파일할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-166">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample3.cs)]
4. <span data-ttu-id="2f1ba-167">F5 키를 눌러 웹 브라우저에서 웹 응용 프로그램을 열면 Facebook이 외부 인증 서비스로 정의 된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-167">When you press F5 to open your web application in your web browser, you will see that Facebook has been defined as an external authentication service:</span></span>

    [![](external-authentication-services/_static/image74.png "Click to Expand the Image")](external-authentication-services/_static/image74.png)
5. <span data-ttu-id="2f1ba-168">**Facebook** 단추를 클릭 하면 브라우저는 facebook 로그인 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-168">When you click the **Facebook** button, your browser will be redirected to the Facebook login page:</span></span>

    [![](external-authentication-services/_static/image22.png "Click to Expand the Image")](external-authentication-services/_static/image21.png)
6. <span data-ttu-id="2f1ba-169">Facebook 자격 증명을 입력 하 고 **로그인**을 클릭 하면 웹 브라우저가 웹 응용 프로그램으로 다시 리디렉션됩니다. 그러면 facebook 계정에 연결 하려는 **사용자 이름을** 입력 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-169">After you enter your Facebook credentials and click **Log in**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Facebook account:</span></span>

    [![](external-authentication-services/_static/image24.png "Click to Expand the Image")](external-authentication-services/_static/image23.png)
7. <span data-ttu-id="2f1ba-170">사용자 이름을 입력 하 고 **등록** 단추를 클릭 하면 웹 응용 프로그램에서 Facebook 계정에 대 한 기본 **홈 페이지** 를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-170">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Facebook account:</span></span>

    [![](external-authentication-services/_static/image26.png "Click to Expand the Image")](external-authentication-services/_static/image25.png)

<a id="GOOGLE"></a>
## <a name="enabling-google-authentication"></a><span data-ttu-id="2f1ba-171">Google 인증 사용</span><span class="sxs-lookup"><span data-stu-id="2f1ba-171">Enabling Google Authentication</span></span>

<span data-ttu-id="2f1ba-172">Google 인증을 사용 하려면 Google 개발자 계정을 만들어야 하며, 프로젝트는 작동 하기 위해 Google의 응용 프로그램 ID 및 비밀 키가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-172">Using Google authentication requires you to create a Google developer account, and your project will require an application ID and secret key from Google in order to function.</span></span> <span data-ttu-id="2f1ba-173">Google 개발자 계정을 만들고 응용 프로그램 ID 및 비밀 키를 가져오는 방법에 대 한 자세한 내용은 [https://developers.google.com](https://developers.google.com)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-173">For information about creating a Google developer account and obtaining your application ID and secret key, see [https://developers.google.com](https://developers.google.com).</span></span>

<span data-ttu-id="2f1ba-174">웹 응용 프로그램에 대해 Google 인증을 사용 하도록 설정 하려면 다음 단계를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-174">To enable Google authentication for your web application, use the following steps:</span></span>

1. <span data-ttu-id="2f1ba-175">프로젝트가 Visual Studio 2017에서 열리면 *Startup.Auth.cs* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-175">When your project is open in Visual Studio 2017, open the *Startup.Auth.cs* file.</span></span>

2. <span data-ttu-id="2f1ba-176">코드의 Google 인증 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-176">Locate the Google authentication section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample4.cs)]
3. <span data-ttu-id="2f1ba-177">&quot;//&quot; 문자를 제거 하 여 강조 표시 된 코드 줄의 주석 처리를 제거 하 고 응용 프로그램 ID 및 비밀 키를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-177">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your application ID and secret key.</span></span> <span data-ttu-id="2f1ba-178">이러한 매개 변수를 추가한 후에는 프로젝트를 다시 컴파일할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-178">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample5.cs)]
4. <span data-ttu-id="2f1ba-179">F5 키를 눌러 웹 브라우저에서 웹 응용 프로그램을 열면 Google이 외부 인증 서비스로 정의 된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-179">When you press F5 to open your web application in your web browser, you will see that Google has been defined as an external authentication service:</span></span>

    [![](external-authentication-services/_static/image75.png "Click to Expand the Image")](external-authentication-services/_static/image75.png)
5. <span data-ttu-id="2f1ba-180">**Google** 단추를 클릭 하면 브라우저는 google 로그인 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-180">When you click the **Google** button, your browser will be redirected to the Google login page:</span></span>

    [![](external-authentication-services/_static/image32.png "Click to Expand the Image")](external-authentication-services/_static/image31.png)
6. <span data-ttu-id="2f1ba-181">Google 자격 증명을 입력 하 고 **로그인**을 클릭 하면 google에서 웹 응용 프로그램에 google 계정에 액세스할 수 있는 권한이 있는지 확인 하는 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-181">After you enter your Google credentials and click **Sign in**, Google will prompt you to verify that your web application has permissions to access your Google account:</span></span>

    [![](external-authentication-services/_static/image34.png "Click to Expand the Image")](external-authentication-services/_static/image33.png)
7. <span data-ttu-id="2f1ba-182">**수락**을 클릭 하면 웹 브라우저가 웹 응용 프로그램으로 다시 리디렉션되고 Google 계정에 연결할 **사용자 이름을** 입력 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-182">When you click **Accept**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Google account:</span></span>

    [![](external-authentication-services/_static/image36.png "Click to Expand the Image")](external-authentication-services/_static/image35.png)
8. <span data-ttu-id="2f1ba-183">사용자 이름을 입력 하 고 **등록** 단추를 클릭 하면 웹 응용 프로그램은 Google 계정에 대 한 기본 **홈 페이지** 를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-183">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Google account:</span></span>

    [![](external-authentication-services/_static/image38.png "Click to Expand the Image")](external-authentication-services/_static/image37.png)

<a id="MICROSOFT"></a>
## <a name="enabling-microsoft-authentication"></a><span data-ttu-id="2f1ba-184">Microsoft 인증 사용</span><span class="sxs-lookup"><span data-stu-id="2f1ba-184">Enabling Microsoft Authentication</span></span>

<span data-ttu-id="2f1ba-185">Microsoft 인증을 사용 하려면 개발자 계정을 만들어야 하며, 기능을 위해서는 클라이언트 ID와 클라이언트 암호가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-185">Microsoft authentication requires you to create a developer account, and it requires a client ID and client secret in order to function.</span></span> <span data-ttu-id="2f1ba-186">Microsoft 개발자 계정을 만들고 클라이언트 ID 및 클라이언트 암호를 가져오는 방법에 대 한 자세한 내용은 [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-186">For information about creating a Microsoft developer account and obtaining your client ID and client secret, see [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070).</span></span>

<span data-ttu-id="2f1ba-187">소비자 키 및 소비자 암호를 가져온 후에는 다음 단계를 사용 하 여 웹 응용 프로그램에 대 한 Microsoft 인증을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-187">Once you have obtained your consumer key and consumer secret, use the following steps to enable Microsoft authentication for your web application:</span></span>

1. <span data-ttu-id="2f1ba-188">프로젝트가 Visual Studio 2017에서 열리면 *Startup.Auth.cs* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-188">When your project is open in Visual Studio 2017, open the *Startup.Auth.cs* file.</span></span>

2. <span data-ttu-id="2f1ba-189">코드의 Microsoft 인증 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-189">Locate the Microsoft authentication section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample6.cs)]
3. <span data-ttu-id="2f1ba-190">&quot;//&quot; 문자를 제거 하 여 강조 표시 된 코드 줄의 주석 처리를 제거 하 고 클라이언트 ID 및 클라이언트 암호를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-190">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your client ID and client secret.</span></span> <span data-ttu-id="2f1ba-191">이러한 매개 변수를 추가한 후에는 프로젝트를 다시 컴파일할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-191">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample7.cs)]
4. <span data-ttu-id="2f1ba-192">F5 키를 눌러 웹 브라우저에서 웹 응용 프로그램을 열면 Microsoft가 외부 인증 서비스로 정의 된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-192">When you press F5 to open your web application in your web browser, you will see that Microsoft has been defined as an external authentication service:</span></span>

    [![](external-authentication-services/_static/image42.png "Click to Expand the Image")](external-authentication-services/_static/image41.png)
5. <span data-ttu-id="2f1ba-193">**Microsoft** 단추를 클릭 하면 브라우저가 microsoft 로그인 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-193">When you click the **Microsoft** button, your browser will be redirected to the Microsoft login page:</span></span>

    [![](external-authentication-services/_static/image44.png "Click to Expand the Image")](external-authentication-services/_static/image43.png)
6. <span data-ttu-id="2f1ba-194">Microsoft 자격 증명을 입력 하 고 **로그인**을 클릭 하면 웹 응용 프로그램에 Microsoft 계정에 액세스할 수 있는 권한이 있는지 확인 하는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-194">After you enter your Microsoft credentials and click **Sign in**, you will be prompted to verify that your web application has permissions to access your Microsoft account:</span></span>

    [![](external-authentication-services/_static/image46.png "Click to Expand the Image")](external-authentication-services/_static/image45.png)
7. <span data-ttu-id="2f1ba-195">**예**를 클릭 하면 웹 브라우저가 웹 응용 프로그램으로 다시 리디렉션되고 Microsoft 계정와 연결할 **사용자 이름을** 입력 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-195">When you click **Yes**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Microsoft account:</span></span>

    [![](external-authentication-services/_static/image48.png "Click to Expand the Image")](external-authentication-services/_static/image47.png)
8. <span data-ttu-id="2f1ba-196">사용자 이름을 입력 하 고 **등록** 단추를 클릭 하면 웹 응용 프로그램에서 Microsoft 계정에 대 한 기본 **홈 페이지** 를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-196">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Microsoft account:</span></span>

    [![](external-authentication-services/_static/image50.png "Click to Expand the Image")](external-authentication-services/_static/image49.png)

<a id="TWITTER"></a>
## <a name="enabling-twitter-authentication"></a><span data-ttu-id="2f1ba-197">Twitter 인증 사용</span><span class="sxs-lookup"><span data-stu-id="2f1ba-197">Enabling Twitter Authentication</span></span>

<span data-ttu-id="2f1ba-198">Twitter 인증을 사용 하려면 개발자 계정을 만들어야 하며, 작동 하려면 소비자 키 및 소비자 암호가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-198">Twitter authentication requires you to create a developer account, and it requires a consumer key and consumer secret in order to function.</span></span> <span data-ttu-id="2f1ba-199">Twitter 개발자 계정을 만들고 소비자 키 및 소비자 암호를 가져오는 방법에 대 한 자세한 내용은 [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-199">For information about creating a Twitter developer account and obtaining your consumer key and consumer secret, see [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).</span></span>

<span data-ttu-id="2f1ba-200">소비자 키 및 소비자 암호를 가져온 후에는 다음 단계를 사용 하 여 웹 응용 프로그램에 대해 Twitter 인증을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-200">Once you have obtained your consumer key and consumer secret, use the following steps to enable Twitter authentication for your web application:</span></span>

1. <span data-ttu-id="2f1ba-201">프로젝트가 Visual Studio 2017에서 열리면 *Startup.Auth.cs* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-201">When your project is open in Visual Studio 2017, open the *Startup.Auth.cs* file.</span></span>

2. <span data-ttu-id="2f1ba-202">코드의 Twitter 인증 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-202">Locate the Twitter authentication section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample8.cs)]
3. <span data-ttu-id="2f1ba-203">&quot;//&quot; 문자를 제거 하 여 강조 표시 된 코드 줄의 주석 처리를 제거 하 고 소비자 키 및 소비자 암호를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-203">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your consumer key and consumer secret.</span></span> <span data-ttu-id="2f1ba-204">이러한 매개 변수를 추가한 후에는 프로젝트를 다시 컴파일할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-204">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample9.cs)]
4. <span data-ttu-id="2f1ba-205">F5 키를 눌러 웹 브라우저에서 웹 응용 프로그램을 열면 Twitter가 외부 인증 서비스로 정의 된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-205">When you press F5 to open your web application in your web browser, you will see that Twitter has been defined as an external authentication service:</span></span>

    [![](external-authentication-services/_static/image54.png "Click to Expand the Image")](external-authentication-services/_static/image53.png)
5. <span data-ttu-id="2f1ba-206">**Twitter** 단추를 클릭 하면 브라우저는 twitter 로그인 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-206">When you click the **Twitter** button, your browser will be redirected to the Twitter login page:</span></span>

    [![](external-authentication-services/_static/image56.png "Click to Expand the Image")](external-authentication-services/_static/image55.png)
6. <span data-ttu-id="2f1ba-207">Twitter 자격 증명을 입력 하 고 **앱 권한 부여**를 클릭 하면 웹 브라우저가 웹 응용 프로그램으로 다시 리디렉션되고 Twitter 계정에 연결할 **사용자 이름을** 입력 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-207">After you enter your Twitter credentials and click **Authorize app**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Twitter account:</span></span>

    [![](external-authentication-services/_static/image58.png "Click to Expand the Image")](external-authentication-services/_static/image57.png)
7. <span data-ttu-id="2f1ba-208">사용자 이름을 입력 하 고 **등록** 단추를 클릭 하면 웹 응용 프로그램에서 Twitter 계정에 대 한 기본 **홈 페이지** 를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-208">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Twitter account:</span></span>

    [![](external-authentication-services/_static/image60.png "Click to Expand the Image")](external-authentication-services/_static/image59.png)

<a id="MOREINFO"></a>
## <a name="additional-information"></a><span data-ttu-id="2f1ba-209">추가 정보</span><span class="sxs-lookup"><span data-stu-id="2f1ba-209">Additional Information</span></span>

<span data-ttu-id="2f1ba-210">OAuth 및 Openid connect를 사용 하는 응용 프로그램을 만드는 방법에 대 한 자세한 내용은 다음 Url을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-210">For additional information about creating applications that use OAuth and OpenID, see the following URLs:</span></span>

- [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)
- [https://go.microsoft.com/fwlink/?LinkID=243995](https://go.microsoft.com/fwlink/?LinkID=243995)

<a id="COMBINE"></a>
### <a name="combining-external-authentication-services"></a><span data-ttu-id="2f1ba-211">외부 인증 서비스 결합</span><span class="sxs-lookup"><span data-stu-id="2f1ba-211">Combining External Authentication Services</span></span>

<span data-ttu-id="2f1ba-212">유연성을 높이기 위해 여러 외부 인증 서비스를 동시에 정의할 수 있습니다. 이렇게 하면 웹 응용 프로그램의 사용자가 사용 하도록 설정 된 외부 인증 서비스의 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-212">For greater flexibility, you can define multiple external authentication services at the same time - this allows your web application's users to use an account from any of the enabled external authentication services:</span></span>

[![](external-authentication-services/_static/image62.png "Click to Expand the Image")](external-authentication-services/_static/image61.png)

<a id="FQDN"></a>
### <a name="configure-iis-express-to-use-a-fully-qualified-domain-name"></a><span data-ttu-id="2f1ba-213">정규화 된 도메인 이름을 사용 하도록 IIS Express 구성</span><span class="sxs-lookup"><span data-stu-id="2f1ba-213">Configure IIS Express to use a fully qualified domain name</span></span>

<span data-ttu-id="2f1ba-214">일부 외부 인증 공급자는 `http://localhost:port/`와 같은 HTTP 주소를 사용 하 여 응용 프로그램 테스트를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-214">Some external authentication providers do not support testing your application by using an HTTP address like `http://localhost:port/`.</span></span> <span data-ttu-id="2f1ba-215">이 문제를 해결 하려면 호스트 파일에 정적 FQDN (정규화 된 도메인 이름) 매핑을 추가 하 고 테스트/디버깅에 FQDN을 사용 하도록 Visual Studio 2017에서 프로젝트 옵션을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-215">To work around this issue, you can add a static Fully Qualified Domain Name (FQDN) mapping to your HOSTS file and configure your project options in Visual Studio 2017 to use the FQDN for testing/debugging.</span></span> <span data-ttu-id="2f1ba-216">이렇게 하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-216">To do so, use the following steps:</span></span>

- <span data-ttu-id="2f1ba-217">호스트 파일의 고정 FQDN 매핑을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-217">Add a static FQDN mapping your HOSTS file:</span></span>

  1. <span data-ttu-id="2f1ba-218">Windows에서 관리자 권한 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-218">Open an elevated command prompt in Windows.</span></span>
  2. <span data-ttu-id="2f1ba-219">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-219">Type the following command:</span></span>

      <span data-ttu-id="2f1ba-220"><kbd>메모장%WinDir%\system32\drivers\etc\hosts</kbd></span><span class="sxs-lookup"><span data-stu-id="2f1ba-220"><kbd>notepad %WinDir%\system32\drivers\etc\hosts</kbd></span></span>
  3. <span data-ttu-id="2f1ba-221">HOSTS 파일에 다음과 같은 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-221">Add an entry like the following to the HOSTS file:</span></span>

      <span data-ttu-id="2f1ba-222"><kbd>127.0.0.1 www.wingtiptoys.com</kbd></span><span class="sxs-lookup"><span data-stu-id="2f1ba-222"><kbd>127.0.0.1 www.wingtiptoys.com</kbd></span></span>
  4. <span data-ttu-id="2f1ba-223">HOSTS 파일을 저장 하 고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-223">Save and close your HOSTS file.</span></span>

- <span data-ttu-id="2f1ba-224">FQDN을 사용 하도록 Visual Studio 프로젝트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-224">Configure your Visual Studio project to use the FQDN:</span></span>

  1. <span data-ttu-id="2f1ba-225">Visual Studio 2017 **에서 프로젝트가 열리면 프로젝트 메뉴를** 클릭 한 다음 프로젝트의 속성을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-225">When your project is open in Visual Studio 2017, click the **Project** menu, and then select your project's properties.</span></span> <span data-ttu-id="2f1ba-226">예를 들어 **WebApplication1 속성**을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-226">For example, you might select **WebApplication1 Properties**.</span></span>
  2. <span data-ttu-id="2f1ba-227">**웹** 탭을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-227">Select the **Web** tab.</span></span>
  3. <span data-ttu-id="2f1ba-228"><strong>프로젝트 Url</strong>에 대 한 FQDN을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-228">Enter your FQDN for the <strong>Project Url</strong>.</span></span> <span data-ttu-id="2f1ba-229">예를 들어 호스트 파일에 추가한 FQDN 매핑 인 경우 <kbd><http://www.wingtiptoys.com></kbd> 를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-229">For example, you would enter <kbd><http://www.wingtiptoys.com></kbd> if that was the FQDN mapping that you added to your HOSTS file.</span></span>

- <span data-ttu-id="2f1ba-230">응용 프로그램에 FQDN을 사용 하도록 IIS Express를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-230">Configure IIS Express to use the FQDN for your application:</span></span>

    1. <span data-ttu-id="2f1ba-231">Windows에서 관리자 권한 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-231">Open an elevated command prompt in Windows.</span></span>
    2. <span data-ttu-id="2f1ba-232">다음 명령을 입력 하 여 IIS Express 폴더로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-232">Type the following command to change to your IIS Express folder:</span></span>

        <span data-ttu-id="2f1ba-233"><kbd>cd/d &quot;%ProgramFiles%\IIS Express&quot;</kbd></span><span class="sxs-lookup"><span data-stu-id="2f1ba-233"><kbd>cd /d &quot;%ProgramFiles%\IIS Express&quot;</kbd></span></span>
    3. <span data-ttu-id="2f1ba-234">다음 명령을 입력 하 여 응용 프로그램에 FQDN을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-234">Type the following command to add the FQDN to your application:</span></span>

        <span data-ttu-id="2f1ba-235"><kbd>appcmd.exe set config-section: system.web/sites/+&quot;[name = ' WebApplication1 ']. bindings. [protocol = ' http ', bindingInformation = ' \*: 80: wingtiptoys ']&quot;/commit: apphost</kbd></span><span class="sxs-lookup"><span data-stu-id="2f1ba-235"><kbd>appcmd.exe set config -section:system.applicationHost/sites /+&quot;[name='WebApplication1'].bindings.[protocol='http',bindingInformation='\*:80:www.wingtiptoys.com']&quot; /commit:apphost</kbd></span></span>

  <span data-ttu-id="2f1ba-236">여기서 **WebApplication1** 은 프로젝트의 이름이 고, **bindingInformation** 에는 테스트에 사용할 포트 번호 및 FQDN이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-236">Where **WebApplication1** is the name of your project and **bindingInformation** contains the port number and FQDN that you want to use for your testing.</span></span>

<a id="OBTAIN"></a>
### <a name="how-to-obtain-your-application-settings-for-microsoft-authentication"></a><span data-ttu-id="2f1ba-237">Microsoft 인증에 대 한 응용 프로그램 설정을 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="2f1ba-237">How to Obtain your Application Settings for Microsoft Authentication</span></span>

<span data-ttu-id="2f1ba-238">Microsoft 인증을 위해 Windows Live에 응용 프로그램을 연결 하는 것은 간단한 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-238">Linking an application to Windows Live for Microsoft Authentication is a simple process.</span></span> <span data-ttu-id="2f1ba-239">응용 프로그램을 Windows Live에 아직 연결 하지 않은 경우 다음 단계를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-239">If you have not already linked an application to Windows Live, you can use the following steps:</span></span>

1. <span data-ttu-id="2f1ba-240">[https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070) 로 이동 하 고 메시지가 표시 되 면 Microsoft 계정 이름과 암호를 입력 한 다음 **로그인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-240">Browse to [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070) and enter your Microsoft account name and password when prompted, then click **Sign in**:</span></span>

   <!--  [![](external-authentication-services/_static/image64.png "Click to Expand the Image")](external-authentication-services/_static/image63.png) -->
2. <span data-ttu-id="2f1ba-241">**앱 추가** 를 선택 하 고 메시지가 표시 되 면 응용 프로그램의 이름을 입력 한 다음 **만들기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-241">Select **Add an app** and enter the name of your application when prompted, and then click **Create**:</span></span>

    [![](external-authentication-services/_static/image79.png "Click to Expand the Image")](external-authentication-services/_static/image79.png)
3. <span data-ttu-id="2f1ba-242">**이름** 아래에서 앱을 선택 하면 해당 응용 프로그램 속성 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-242">Select your app under **Name** and its application properties page appears.</span></span>

4. <span data-ttu-id="2f1ba-243">응용 프로그램에 대 한 리디렉션 도메인을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-243">Enter the redirect domain for your application.</span></span> <span data-ttu-id="2f1ba-244">**응용 프로그램 ID** 를 복사 하 고 **응용 프로그램**암호에서 **암호 생성**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-244">Copy the **Application ID** and, under **Application Secrets**, select **Generate Password**.</span></span> <span data-ttu-id="2f1ba-245">표시 되는 암호를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-245">Copy the password that appears.</span></span> <span data-ttu-id="2f1ba-246">응용 프로그램 ID 및 암호는 클라이언트 ID 및 클라이언트 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-246">The application ID and password are your client ID and client secret.</span></span> <span data-ttu-id="2f1ba-247">**확인** , **저장**을 차례로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-247">Select **Ok** and then **Save**.</span></span>

    [![](external-authentication-services/_static/image77.png "Click to Expand the Image")](external-authentication-services/_static/image77.png)

<a id="DISABLE"></a>
### <a name="optional-disable-local-registration"></a><span data-ttu-id="2f1ba-248">선택 사항: 로컬 등록 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="2f1ba-248">Optional: Disable Local Registration</span></span>

<span data-ttu-id="2f1ba-249">현재 ASP.NET 로컬 등록 기능을 통해 자동 프로그램 (봇)에서 구성원 계정을 만들 수 있습니다. 예를 들어 [CAPTCHA](../../../web-pages/overview/security/16-adding-security-and-membership.md)와 같은 봇 방지 및 유효성 검사 기술을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-249">The current ASP.NET local registration functionality does not prevent automated programs (bots) from creating member accounts; for example, by using a bot-prevention and validation technology like [CAPTCHA](../../../web-pages/overview/security/16-adding-security-and-membership.md).</span></span> <span data-ttu-id="2f1ba-250">따라서 로그인 페이지에서 로컬 로그인 양식 및 등록 링크를 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-250">Because of this, you should remove the local login form and registration link on the login page.</span></span> <span data-ttu-id="2f1ba-251">이렇게 하려면 프로젝트에서 *\_Login* 페이지를 열고 로컬 로그인 패널 및 등록 링크에 대 한 줄을 주석으로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-251">To do so, open the *\_Login.cshtml* page in your project, and then comment out the lines for the local login panel and the registration link.</span></span> <span data-ttu-id="2f1ba-252">결과 페이지는 다음 코드 샘플과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-252">The resulting page should look like the following code sample:</span></span>

[!code-html[Main](external-authentication-services/samples/sample10.html)]

<span data-ttu-id="2f1ba-253">로컬 로그인 패널과 등록 링크를 사용 하지 않도록 설정 하면 로그인 페이지가 사용 하도록 설정한 외부 인증 공급자만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f1ba-253">Once the local login panel and the registration link have been disabled, your login page will only display the external authentication providers that you have enabled:</span></span>

[![](external-authentication-services/_static/image70.png "Click to Expand the Image")](external-authentication-services/_static/image69.png)
