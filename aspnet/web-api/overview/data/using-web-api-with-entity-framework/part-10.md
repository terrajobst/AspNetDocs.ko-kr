---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-10
title: Azure Azure App Service에 앱 게시 Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 10fd812b-94d6-4967-be97-a31ce9c45e2c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-10
msc.type: authoredcontent
ms.openlocfilehash: a9a7b74a07c71b47253c0af304c7a26ffa4eaae5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504761"
---
# <a name="publish-the-app-to-azure-azure-app-service"></a><span data-ttu-id="ba77e-102">Azure Azure App Service에 앱 게시</span><span class="sxs-lookup"><span data-stu-id="ba77e-102">Publish the App to Azure Azure App Service</span></span>

<span data-ttu-id="ba77e-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ba77e-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="ba77e-104">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="ba77e-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="ba77e-105">마지막 단계로 Azure에 응용 프로그램을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba77e-105">As the last step, you will publish the application to Azure.</span></span> <span data-ttu-id="ba77e-106">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba77e-106">In Solution Explorer, right-click the project and select **Publish**.</span></span>

![](part-10/_static/image1.png)

<span data-ttu-id="ba77e-107">**게시** 를 클릭 하면 **웹 게시** 대화 상자가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba77e-107">Clicking **Publish** invokes the **Publish Web** dialog.</span></span> <span data-ttu-id="ba77e-108">프로젝트를 처음 만들 때 **클라우드에서 호스트** 를 선택한 경우 연결 및 설정이 이미 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba77e-108">If you checked **Host in Cloud** when you first created the project, then the connection and settings are already configured.</span></span> <span data-ttu-id="ba77e-109">이 경우 **설정** 탭을 클릭 하 고 Code First 마이그레이션&quot;&quot;실행을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba77e-109">In that case, just click the **Settings** tab and check &quot;Execute Code First Migrations&quot;.</span></span> <span data-ttu-id="ba77e-110">(처음부터 **클라우드의 호스트** 를 확인 하지 않은 경우 [다음 섹션](#new-website)의 단계를 따르세요.)</span><span class="sxs-lookup"><span data-stu-id="ba77e-110">(If you didn't check **Host in Cloud** at the beginning, then follow the steps in the [next section](#new-website).)</span></span>

[![](part-10/_static/image3.png)](part-10/_static/image2.png)

<span data-ttu-id="ba77e-111">앱을 배포 하려면 **게시**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba77e-111">To deploy the app, click **Publish**.</span></span> <span data-ttu-id="ba77e-112">**웹 게시 작업** 창에서 게시 진행률을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba77e-112">You can view the publishing progress in the **Web Publish Activity** window.</span></span> <span data-ttu-id="ba77e-113">**보기** 메뉴에서 **다른 창**을 선택한 다음 **웹 게시 작업**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba77e-113">(From the **View** menu, select **Other Windows**, then select **Web Publish Activity**.)</span></span>

![](part-10/_static/image4.png)

<span data-ttu-id="ba77e-114">Visual Studio에서 앱 배포가 완료 되 면 기본 브라우저가 자동으로 배포 된 웹 사이트의 URL로 열리며, 만든 응용 프로그램은 이제 클라우드에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba77e-114">When Visual Studio finishes deploying the app, the default browser automatically opens to the URL of the deployed website, and the application that you created is now running in the cloud.</span></span> <span data-ttu-id="ba77e-115">브라우저 주소 표시줄의 URL은 사이트가 인터넷에서 로드 되 고 있음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ba77e-115">The URL in the browser address bar shows that the site is being loaded from the Internet.</span></span>

[![](part-10/_static/image6.png)](part-10/_static/image5.png)

<a id="new-website"></a>
## <a name="deploying-to-a-new-website"></a><span data-ttu-id="ba77e-116">새 웹 사이트에 배포</span><span class="sxs-lookup"><span data-stu-id="ba77e-116">Deploying to a New Website</span></span>

<span data-ttu-id="ba77e-117">프로젝트를 처음 만들 때 **클라우드의 호스트** 를 확인 하지 않은 경우 지금 새 웹 앱을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba77e-117">If you did not check **Host in Cloud** when you first created the project, you can configure a new web app now.</span></span> <span data-ttu-id="ba77e-118">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba77e-118">In Solution Explorer, right-click the project and select **Publish**.</span></span> <span data-ttu-id="ba77e-119">**프로필** 탭을 선택 하 고 **Microsoft Azure Websites**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba77e-119">Select the **Profile** tab and click **Microsoft Azure Websites**.</span></span> <span data-ttu-id="ba77e-120">현재 Azure에 로그인 하지 않은 경우 로그인 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba77e-120">If you aren't currently signed in to Azure, you will be prompted to sign in.</span></span>

[![](part-10/_static/image8.png)](part-10/_static/image7.png)

<span data-ttu-id="ba77e-121">**기존 웹 사이트** 대화 상자에서 **새로 만들기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba77e-121">In the **Existing Websites** dialog, click **New**.</span></span>

![](part-10/_static/image9.png)

<span data-ttu-id="ba77e-122">사이트 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba77e-122">Enter a site name.</span></span> <span data-ttu-id="ba77e-123">Azure 구독 및 지역을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba77e-123">Select your Azure subscription and the region.</span></span> <span data-ttu-id="ba77e-124">**데이터베이스 서버**에서 **새 서버 만들기**를 선택 하거나 기존 서버를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba77e-124">Under **Database server**, select **Create New Server**, or select an existing server.</span></span> <span data-ttu-id="ba77e-125">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ba77e-125">Click **Create**.</span></span>

[![](part-10/_static/image11.png)](part-10/_static/image10.png)

<span data-ttu-id="ba77e-126">**설정** 탭을 클릭 하 &quot;Code First 마이그레이션&quot;실행을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba77e-126">Click the **Settings** tab and check &quot;Execute Code First Migrations&quot;.</span></span> <span data-ttu-id="ba77e-127">그런 다음, **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ba77e-127">Then click **Publish**.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="ba77e-128">이전</span><span class="sxs-lookup"><span data-stu-id="ba77e-128">Previous</span></span>](part-9.md)
