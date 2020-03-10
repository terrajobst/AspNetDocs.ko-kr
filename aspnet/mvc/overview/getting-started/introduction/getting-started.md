---
uid: mvc/overview/getting-started/introduction/getting-started
title: ASP.NET MVC 5 시작 | Microsoft Docs
author: Rick-Anderson
ms.author: riande
ms.date: 10/04/2018
ms.assetid: f3d8adbe-55e7-4fd4-84a8-7155bc45c676
msc.legacyurl: /mvc/overview/getting-started/introduction/getting-started
msc.type: authoredcontent
ms.openlocfilehash: ca39bc37c757c0452cf56624c8e37c04df4b41f2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78487955"
---
# <a name="getting-started-with-aspnet-mvc-5"></a><span data-ttu-id="9b940-102">ASP.NET MVC 5 시작</span><span class="sxs-lookup"><span data-stu-id="9b940-102">Getting started with ASP.NET MVC 5</span></span>

<span data-ttu-id="9b940-103">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="9b940-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](../../../../includes/razor.md)]

<span data-ttu-id="9b940-104">이 자습서에서는 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)을 사용 하 여 ASP.NET MVC 5 웹 앱을 빌드하는 기본 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-104">This tutorial teaches you the basics of building an ASP.NET MVC 5 web app using [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span> <span data-ttu-id="9b940-105">자습서의 최종 소스 코드는 [GitHub](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie/MvcMovie)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-105">The final source code for the tutorial is located on [GitHub](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie/MvcMovie).</span></span>

<span data-ttu-id="9b940-106">이 자습서는 [Scott Guthrie](https://weblogs.asp.net/scottgu/) (twitter[@scottgu](https://twitter.com/scottgu) ), [scott Hanselman](http://www.hanselman.com/blog/) (Twitter: [@shanselman](https://twitter.com/shanselman) ) 및 [Rick Anderson](https://twitter.com/RickAndMSFT) ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) )에 의해 작성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-106">This tutorial was written by [Scott Guthrie](https://weblogs.asp.net/scottgu/) (twitter[@scottgu](https://twitter.com/scottgu) ), [Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](https://twitter.com/shanselman) ), and [Rick Anderson](https://twitter.com/RickAndMSFT) ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) )</span></span>

<span data-ttu-id="9b940-107">Azure에이 앱을 배포 하려면 Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-107">You need an Azure account to deploy this app to Azure:</span></span>

- <span data-ttu-id="9b940-108">[Azure 계정을 무료로 열](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) 수 있음-유료 azure 서비스를 사용 하는 데 사용할 수 있는 크레딧을 확보 하 고, 사용한 후에도 계정을 유지 하 고 무료 Azure 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-108">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="9b940-109">[MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) 할 수 있음 - MSDN 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-109">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="get-started"></a><span data-ttu-id="9b940-110">시작하기</span><span class="sxs-lookup"><span data-stu-id="9b940-110">Get started</span></span>

<span data-ttu-id="9b940-111">[Visual Studio 2017을 설치](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-111">Start by [installing Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span> <span data-ttu-id="9b940-112">그런 다음 Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-112">Then, open Visual Studio.</span></span>

<span data-ttu-id="9b940-113">Visual Studio는 IDE 또는 통합 된 개발 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-113">Visual Studio is an IDE, or integrated development environment.</span></span> <span data-ttu-id="9b940-114">Microsoft Word를 사용 하 여 문서를 작성 하는 것 처럼 IDE를 사용 하 여 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-114">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="9b940-115">Visual Studio에는 제공 되는 다양 한 옵션을 보여 주는 목록이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-115">In Visual Studio, there's a list along the bottom showing various options available to you.</span></span> <span data-ttu-id="9b940-116">IDE에서 작업을 수행 하는 다른 방법을 제공 하는 메뉴도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-116">There's also a menu that provides another way to perform tasks in the IDE.</span></span> <span data-ttu-id="9b940-117">예를 들어 **시작 페이지**에서 **새 프로젝트** 를 선택 하는 대신 메뉴 모음을 사용 하 여 **파일** > **새 프로젝트**를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-117">For example, instead of selecting **New Project** on the **Start page**, you can use the menu bar and select **File** > **New Project**.</span></span>

![](getting-started/_static/image1.png)

## <a name="create-your-first-app"></a><span data-ttu-id="9b940-118">첫 번째 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="9b940-118">Create your first app</span></span>

<span data-ttu-id="9b940-119">**시작 페이지**에서 **새 프로젝트**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-119">On the **Start page**, select **New Project**.</span></span> <span data-ttu-id="9b940-120">**새 프로젝트** 대화 상자에서 왼쪽의 **시각적 C#**  범주를 선택한 다음 **웹**을 선택 하 고 **.NET Framework (ASP.NET web Application)** 프로젝트 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-120">In the **New project** dialog box, select the **Visual C#** category on the left, then **Web**, and then select the **ASP.NET Web Application (.NET Framework)** project template.</span></span> <span data-ttu-id="9b940-121">프로젝트 이름을 "MvcMovie"로 지정한 다음 **확인을**선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-121">Name your project "MvcMovie" and then choose **OK**.</span></span>

![](getting-started/_static/image2.png)

<span data-ttu-id="9b940-122">**New ASP.NET 웹 응용 프로그램** 대화 상자에서 **MVC** 를 선택한 다음 **확인**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-122">In the **New ASP.NET Web Application** dialog, choose **MVC** and then choose **OK**.</span></span>

![](getting-started/_static/image3.png)

<span data-ttu-id="9b940-123">Visual Studio는 방금 만든 ASP.NET MVC 프로젝트에 대 한 기본 템플릿을 사용 하 여 작업을 수행 하는 응용 프로그램을 지금 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-123">Visual Studio used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="9b940-124">이는 간단한 "Hello World!"입니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-124">This is a simple "Hello World!"</span></span> <span data-ttu-id="9b940-125">프로젝트를 시작 하 고 응용 프로그램을 시작 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-125">project, and it's a good place to start your application.</span></span>

![](getting-started/_static/image4.png)

<span data-ttu-id="9b940-126">**F5** 키를 눌러 디버깅을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-126">Press **F5** to start debugging.</span></span> <span data-ttu-id="9b940-127">**F5**키를 누르면 Visual Studio에서 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) 시작 하 고 웹 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-127">When you press **F5**, Visual Studio starts [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs your web app.</span></span> <span data-ttu-id="9b940-128">그러면 Visual Studio가 브라우저를 시작 하 고 응용 프로그램의 홈 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-128">Visual Studio then launches a browser and opens the application's home page.</span></span> <span data-ttu-id="9b940-129">브라우저의 주소 표시줄에 `localhost:port#` 표시 되 고 `example.com`와 같은 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-129">Notice that the address bar of the browser says `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="9b940-130">`localhost`은 항상 자신의 로컬 컴퓨터를 가리키지만이 경우에는 방금 빌드한 응용 프로그램을 실행 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-130">That's because `localhost` always points to your own local computer, which in this case is running the application you just built.</span></span> <span data-ttu-id="9b940-131">Visual Studio에서 웹 프로젝트를 실행 하면 웹 서버에 대해 임의의 포트가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-131">When Visual Studio runs a web project, a random port is used for the web server.</span></span> <span data-ttu-id="9b940-132">아래 이미지에서 포트 번호는 1234입니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-132">In the image below, the port number is 1234.</span></span> <span data-ttu-id="9b940-133">응용 프로그램을 실행 하면 다른 포트 번호가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-133">When you run the application, you'll see a different port number.</span></span>

![](getting-started/_static/image5.png)

<span data-ttu-id="9b940-134">바로이 기본 템플릿은 `Home`, `Contact`및 `About` 페이지를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-134">Right out of the box this default template gives you `Home`, `Contact`, and `About` pages.</span></span> <span data-ttu-id="9b940-135">아래 이미지는 **홈**, **정보**및 **연락처** 링크를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-135">The image below doesn't show the **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="9b940-136">브라우저 창의 크기에 따라 탐색 아이콘을 클릭 하 여 이러한 링크를 확인 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-136">Depending on the size of your browser window, you might need to click the navigation icon to see these links.</span></span>

![](getting-started/_static/image6.png)

<span data-ttu-id="9b940-137">응용 프로그램은 등록 및 로그인도 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-137">The application also provides support to register and log in.</span></span> <span data-ttu-id="9b940-138">다음 단계는이 응용 프로그램의 작동 방식을 변경 하 고 ASP.NET MVC에 대해 약간 자세히 알아보는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-138">The next step is to change how this application works and learn a little bit about ASP.NET MVC.</span></span> <span data-ttu-id="9b940-139">ASP.NET MVC 응용 프로그램을 닫고 일부 코드를 변경 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-139">Close the ASP.NET MVC application and let's change some code.</span></span>

<span data-ttu-id="9b940-140">현재 자습서 목록은 [MVC 권장 문서](../mvc-learning-sequence.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="9b940-140">For a list of current tutorials, see [MVC recommended articles](../mvc-learning-sequence.md).</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="9b940-141">Azure에서 실행 되는이 앱 확인</span><span class="sxs-lookup"><span data-stu-id="9b940-141">See this app running on Azure</span></span>

<span data-ttu-id="9b940-142">완료 된 사이트가 라이브 웹 앱으로 실행 되 고 있는지 확인 하 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="9b940-142">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="9b940-143">다음 단추를 클릭 하기만 하면 Azure 계정에 전체 버전의 앱을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-143">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](https://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?repository=https://github.com/dotnet/AspNetDocs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie&amp;WT.mc_id=deploy_azure_aspnet)

<span data-ttu-id="9b940-144">Azure에이 솔루션을 배포 하려면 Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-144">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="9b940-145">계정이 아직 없는 경우 다음 옵션 중 하나를 사용 하 여 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-145">If you don't already have an account, use one of the following options to create one:</span></span>

- <span data-ttu-id="9b940-146">[무료로 azure 계정 열기](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) -유료 azure 서비스를 사용 하는 데 사용할 수 있는 크레딧을 확보 하 고, 사용한 후에도 계정을 유지 하 고 무료 Azure 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-146">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="9b940-147">[Visual studio 구독자 혜택 활성화](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers) -visual studio 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b940-147">[Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers) - Your Visual Studio subscription gives you credits every month that you can use for paid Azure services.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="9b940-148">다음</span><span class="sxs-lookup"><span data-stu-id="9b940-148">Next</span></span>](adding-a-controller.md)
