---
uid: signalr/overview/deployment/using-signalr-with-azure-web-sites
title: Azure App Service에서 Web Apps와 함께 SignalR 사용 | Microsoft Docs
author: bradygaster
description: 이 문서에서는 Microsoft Azure에서 실행 되는 SignalR 응용 프로그램을 구성 하는 방법을 설명 합니다. 자습서 Visual Studio 2013 또는 Vis에서 사용 되는 소프트웨어 버전
ms.author: bradyg
ms.date: 07/01/2015
ms.assetid: 2a7517a0-b88c-4162-ade3-9bf6ca7062fd
msc.legacyurl: /signalr/overview/deployment/using-signalr-with-azure-web-sites
msc.type: authoredcontent
ms.openlocfilehash: 0e6a18bdbe9cc47e89b5a458753845afb53595f1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450185"
---
# <a name="using-signalr-with-web-apps-in-azure-app-service"></a><span data-ttu-id="b0662-104">Azure App Service에서 Web Apps에 SignalR 사용</span><span class="sxs-lookup"><span data-stu-id="b0662-104">Using SignalR with Web Apps in Azure App Service</span></span>

<span data-ttu-id="b0662-105">[Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="b0662-105">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="b0662-106">이 문서에서는 Microsoft Azure에서 실행 되는 SignalR 응용 프로그램을 구성 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0662-106">This document describes how to configure a SignalR application that runs on Microsoft Azure.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="b0662-107">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="b0662-107">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="b0662-108">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) 또는 Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="b0662-108">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) or Visual Studio 2012</span></span>
> - <span data-ttu-id="b0662-109">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="b0662-109">.NET 4.5</span></span>
> - <span data-ttu-id="b0662-110">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="b0662-110">SignalR version 2</span></span>
> - <span data-ttu-id="b0662-111">Visual Studio 2013 또는 2012 용 Azure SDK 2.3</span><span class="sxs-lookup"><span data-stu-id="b0662-111">Azure SDK 2.3 for Visual Studio 2013 or 2012</span></span>
>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="b0662-112">질문 및 설명</span><span class="sxs-lookup"><span data-stu-id="b0662-112">Questions and comments</span></span>
>
> <span data-ttu-id="b0662-113">이 자습서와 페이지 맨 아래에 있는 의견에서 개선할 수 있는 방법에 대 한 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="b0662-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="b0662-114">자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR), [StackOverflow.com](http://stackoverflow.com/)또는 [Microsoft Azure 포럼](https://social.msdn.microsoft.com/Forums/windowsazure/home?category=windowsazureplatform)에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0662-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR), [StackOverflow.com](http://stackoverflow.com/), or the [Microsoft Azure forums](https://social.msdn.microsoft.com/Forums/windowsazure/home?category=windowsazureplatform).</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="b0662-115">목차</span><span class="sxs-lookup"><span data-stu-id="b0662-115">Table of Contents</span></span>

- [<span data-ttu-id="b0662-116">소개</span><span class="sxs-lookup"><span data-stu-id="b0662-116">Introduction</span></span>](#introduction)
- [<span data-ttu-id="b0662-117">Azure App Service에 SignalR 웹 앱 배포</span><span class="sxs-lookup"><span data-stu-id="b0662-117">Deploying a SignalR Web App to Azure App Service</span></span>](#deploying)
- [<span data-ttu-id="b0662-118">Azure App Service에서 Websocket 사용</span><span class="sxs-lookup"><span data-stu-id="b0662-118">Enabling WebSockets on Azure App Service</span></span>](#websocket)
- [<span data-ttu-id="b0662-119">Azure Redis Cache 백플레인 사용</span><span class="sxs-lookup"><span data-stu-id="b0662-119">Using the Azure Redis Cache Backplane</span></span>](#backplane)
- [<span data-ttu-id="b0662-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b0662-120">Next Steps</span></span>](#nextsteps)

<a id="introduction"></a>
## <a name="introduction"></a><span data-ttu-id="b0662-121">소개</span><span class="sxs-lookup"><span data-stu-id="b0662-121">Introduction</span></span>

<span data-ttu-id="b0662-122">ASP.NET SignalR를 사용 하 여 서버와 웹 또는 .NET 클라이언트 간에 새로운 수준의 상호 작용을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0662-122">ASP.NET SignalR can be used to bring a new level of interactivity between servers and web or .NET clients.</span></span> <span data-ttu-id="b0662-123">Azure에서 호스트 되는 경우 SignalR 응용 프로그램은 클라우드에서 실행 되는 고가용성, 확장 가능 및 고성능 환경을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0662-123">When hosted in Azure, SignalR applications can take advantage of the highly available, scalable, and performant environment that running in the cloud provides.</span></span>

<a id="deploying"></a>
## <a name="deploying-a-signalr-web-app-to-azure-app-service"></a><span data-ttu-id="b0662-124">Azure App Service에 SignalR 웹 앱 배포</span><span class="sxs-lookup"><span data-stu-id="b0662-124">Deploying a SignalR Web App to Azure App Service</span></span>

<span data-ttu-id="b0662-125">SignalR는 Azure에 응용 프로그램을 배포 하 고 온-프레미스 서버에 배포 하는 경우 특정 복잡성을 추가 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b0662-125">SignalR doesn't add any particular complications to deploying an application to Azure versus deploying to an on-premises server.</span></span> <span data-ttu-id="b0662-126">SignalR를 사용 하는 응용 프로그램은 구성 또는 기타 설정의 변경 없이 Azure에서 호스팅될 수 있습니다 (Websocket 지원의 경우 아래 [Azure App Service에서 Websocket 사용](#websocket) 을 참조 하세요.) 이 자습서에서는 초보자를 위한 [자습서](../getting-started/tutorial-getting-started-with-signalr.md) 에서 만든 응용 프로그램을 Azure에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0662-126">An application that uses SignalR can be hosted in Azure without any changes in configuration or other settings (though for WebSockets support, see [Enabling WebSockets on Azure App Service](#websocket) below.) For this tutorial, you'll deploy the application created in the [Getting Started Tutorial](../getting-started/tutorial-getting-started-with-signalr.md) to Azure.</span></span>

<span data-ttu-id="b0662-127">**필수 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="b0662-127">**Prerequisites**</span></span>

- <span data-ttu-id="b0662-128">Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="b0662-128">Visual Studio 2013.</span></span> <span data-ttu-id="b0662-129">Visual Visual Studio 2013 Studio가 없는 경우 Express for Web이 Azure SDK의 설치에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0662-129">If you don't have Visual Studio, Visual Studio 2013 Express for Web is included in the install of the Azure SDK.</span></span>
- <span data-ttu-id="b0662-130">[Visual Studio 2013 용 AZURE sdk 2.3](https://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409) 또는 [Visual Studio 2012 용 azure sdk 2.3](https://go.microsoft.com/fwlink/p/?linkid=323511)</span><span class="sxs-lookup"><span data-stu-id="b0662-130">[Azure SDK 2.3 for Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409) or [Azure SDK 2.3 for Visual Studio 2012](https://go.microsoft.com/fwlink/p/?linkid=323511).</span></span>
- <span data-ttu-id="b0662-131">이 자습서를 완료하려면 Azure 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b0662-131">To complete this tutorial, you will need an Azure subscription.</span></span> <span data-ttu-id="b0662-132">[MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)하거나 [평가판 구독에 등록할](https://azure.microsoft.com/pricing/free-trial/)수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0662-132">You can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), or [sign up for a trial subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span>

### <a name="deploying-a-signalr-web-app-to-azure"></a><span data-ttu-id="b0662-133">SignalR 웹 앱을 Azure에 배포</span><span class="sxs-lookup"><span data-stu-id="b0662-133">Deploying a SignalR web app to Azure</span></span>

1. <span data-ttu-id="b0662-134">초보자를 위한 [자습서](../getting-started/tutorial-getting-started-with-signalr.md)를 완료 하거나 [코드 갤러리](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)에서 완료 된 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0662-134">Complete the [Getting Started Tutorial](../getting-started/tutorial-getting-started-with-signalr.md), or download the finished project from [Code Gallery](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9).</span></span>
2. <span data-ttu-id="b0662-135">Visual Studio에서 **빌드**, **SignalR 채팅 게시**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0662-135">In Visual Studio, select **Build**, **Publish SignalR Chat**.</span></span>
3. <span data-ttu-id="b0662-136">"웹 게시" 대화 상자에서 "Microsoft Azure 웹 사이트"를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0662-136">In the "Publish Web" dialog, select "Windows Azure Web Sites".</span></span>

    ![Azure 웹 사이트 선택](using-signalr-with-azure-web-sites/_static/image1.png)
4. <span data-ttu-id="b0662-138">Microsoft 계정에 로그인 하지 않은 경우 "기존 웹 사이트 선택" 대화 상자에서 **로그인 ...** 을 클릭 하 고 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0662-138">If you aren't signed in to your Microsoft account, click **Sign In...** in the "Select Existing Web Site" dialog, and sign in.</span></span>

    ![기존 웹 사이트 선택](using-signalr-with-azure-web-sites/_static/image2.png)    ![Azure에 로그인](using-signalr-with-azure-web-sites/_static/image3.png)
5. <span data-ttu-id="b0662-141">"기존 웹 사이트 선택" 대화 상자에서 **새로 만들기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0662-141">In the "Select Existing Web Site" dialog, click **New**.</span></span>

    ![새 웹 사이트](using-signalr-with-azure-web-sites/_static/image4.png)
6. <span data-ttu-id="b0662-143">"Windows Azure에서 사이트 만들기" 대화 상자에서 고유한 앱 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0662-143">In the "Create site on Windows Azure" dialog, enter a unique app name.</span></span> <span data-ttu-id="b0662-144">지역 드롭다운에서 가장 가까운 지역을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0662-144">Select the region closest to you in the Region dropdown.</span></span> <span data-ttu-id="b0662-145">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b0662-145">Click **Create**.</span></span>

    ![Azure에서 사이트 만들기](using-signalr-with-azure-web-sites/_static/image5.png)
7. <span data-ttu-id="b0662-147">"웹 게시" 대화 상자에서 **게시**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0662-147">In the "Publish Web" dialog, click **Publish**.</span></span>

    ![사이트 게시](using-signalr-with-azure-web-sites/_static/image6.png)
8. <span data-ttu-id="b0662-149">앱이 게시를 완료 하면 Azure App Service Web Apps에서 호스트 되는 SignalR Chat 응용 프로그램이 브라우저에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b0662-149">When the app has completed publishing, the SignalR Chat application hosted in Azure App Service Web Apps will open in a browser.</span></span>

    ![브라우저에서 사이트 열기](using-signalr-with-azure-web-sites/_static/image7.png)

<a id="websocket"></a>
### <a name="enabling-websockets-on-azure-app-service-web-apps"></a><span data-ttu-id="b0662-151">Azure App Service Web Apps에서 Websocket 사용</span><span class="sxs-lookup"><span data-stu-id="b0662-151">Enabling WebSockets on Azure App Service Web Apps</span></span>

<span data-ttu-id="b0662-152">Websocket은 SignalR 응용 프로그램에서 사용 하기 위해 웹 앱에서 명시적으로 사용 하도록 설정 해야 합니다. 그렇지 않으면 다른 프로토콜이 사용 됩니다. 자세한 내용은 [전송 및 대체](../getting-started/introduction-to-signalr.md#transports) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b0662-152">WebSockets needs to be explicitly enabled in your web app to be used in a SignalR application; otherwise, other protocols will be used (See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for details).</span></span>

<span data-ttu-id="b0662-153">Azure App Service Web Apps에서 Websocket을 사용 하려면 웹 앱의 구성 섹션에서 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0662-153">In order to use WebSockets on Azure App Service Web Apps, enable it in the configuration section of the web app.</span></span> <span data-ttu-id="b0662-154">이렇게 하려면 [Azure 관리 포털](https://manage.windowsazure.com/)에서 웹 앱을 열고 구성을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0662-154">To do this, open your web app in the [Azure Management Portal](https://manage.windowsazure.com/), and select Configure.</span></span>

![구성 탭](using-signalr-with-azure-web-sites/_static/image8.png)

<span data-ttu-id="b0662-156">구성 페이지의 맨 위에서 .NET 4.5이 웹 앱에 사용 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0662-156">At the top of the configuration page, ensure that .NET 4.5 is used for your web app.</span></span>

![.NET framework 버전 4.5 설정](using-signalr-with-azure-web-sites/_static/image9.png)

<span data-ttu-id="b0662-158">구성 페이지의 **websocket** 설정에서 **켜기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0662-158">On the configuration page, in the **WebSockets** setting, select **On**.</span></span>

![Websocket 설정: 설정](using-signalr-with-azure-web-sites/_static/image10.png)

<span data-ttu-id="b0662-160">구성 페이지의 맨 아래에서 **저장** 을 선택 하 여 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0662-160">At the bottom of the Configuration page, select **Save** to save your changes.</span></span>

![설정 저장](using-signalr-with-azure-web-sites/_static/image11.png)

<a id="backplane"></a>
## <a name="using-the-azure-redis-cache-backplane"></a><span data-ttu-id="b0662-162">Azure Redis Cache 백플레인 사용</span><span class="sxs-lookup"><span data-stu-id="b0662-162">Using the Azure Redis Cache Backplane</span></span>

<span data-ttu-id="b0662-163">웹 앱에 여러 인스턴스를 사용 하 고 해당 인스턴스의 사용자가 서로 상호 작용 해야 하는 경우 (예를 들어 한 인스턴스에서 만든 채팅 메시지는 다른 인스턴스에 연결 된 사용자에 게 도달 하는 경우), 응용 프로그램에서 [Azure Redis Cache 백플레인](../performance/scaleout-with-redis.md) 를 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0662-163">If you use multiple instances for your web app, and the users of those instances need to interact with one another (so that, for instance, chat messages created in one instance can reach the users connected to other instances), the [Azure Redis Cache backplane](../performance/scaleout-with-redis.md) must be implemented in your application.</span></span>

<a id="nextsteps"></a>
## <a name="next-steps"></a><span data-ttu-id="b0662-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b0662-164">Next Steps</span></span>

<span data-ttu-id="b0662-165">Azure App Service Web Apps에 대 한 자세한 내용은 [Web Apps 개요](https://azure.microsoft.com/documentation/articles/app-service-web-overview/)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b0662-165">For more information on Web Apps in Azure App Service, see [Web Apps overview](https://azure.microsoft.com/documentation/articles/app-service-web-overview/).</span></span>
