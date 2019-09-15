---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 테스트에 배포 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 ASP.NET 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자 (usin ...)에 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 01/16/2019
ms.assetid: 8bf2c4fb-4ee5-4841-bfc2-03462c1f7a7a
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
msc.type: authoredcontent
ms.openlocfilehash: c45003325832258466a787bc589bf40e844248a2
ms.sourcegitcommit: 4b324a11131e38f920126066b94ff478aa9927f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70985851"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-to-test"></a><span data-ttu-id="f09fb-103">Visual Studio를 사용 하 여 ASP.NET 웹 배포: 테스트 환경에 배포</span><span class="sxs-lookup"><span data-stu-id="f09fb-103">ASP.NET Web Deployment using Visual Studio: Deploying to Test</span></span>

<span data-ttu-id="f09fb-104">만든 사람 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="f09fb-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="f09fb-105">이 자습서 시리즈에서는 Visual Studio 2017을 사용 하 여 Azure App Service Web Apps 또는 타사 호스팅 공급자에 ASP.NET 웹 응용 프로그램을 배포 (게시) 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-105">This tutorial series shows how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider using Visual Studio 2017.</span></span> <span data-ttu-id="f09fb-106">계열에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="f09fb-106">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

<span data-ttu-id="f09fb-107">최신 버전의 Azure에 배포 하는 경우 [azure에서 ASP.NET Core 웹 앱 만들기](/azure/app-service/app-service-web-get-started-dotnet)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f09fb-107">For a current version of deploying to Azure, see [Create an ASP.NET Core web app in Azure](/azure/app-service/app-service-web-get-started-dotnet).</span></span>

## <a name="overview"></a><span data-ttu-id="f09fb-108">개요</span><span class="sxs-lookup"><span data-stu-id="f09fb-108">Overview</span></span>

<span data-ttu-id="f09fb-109">이 자습서에서는 로컬 컴퓨터의 인터넷 정보 서버 (IIS)에 ASP.NET 웹 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-109">In this tutorial, you'll deploy an ASP.NET web application to Internet Information Server (IIS) on your local computer.</span></span>

<span data-ttu-id="f09fb-110">일반적으로 응용 프로그램을 개발 하는 경우 응용 프로그램을 실행 하 고 Visual Studio에서 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-110">Generally when you develop an application, you run it and test it in Visual Studio.</span></span> <span data-ttu-id="f09fb-111">기본적으로 Visual Studio 2017의 웹 응용 프로그램 프로젝트는 IIS Express를 개발 웹 서버로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-111">By default, web application projects in Visual Studio 2017 use IIS Express as the development web server.</span></span> <span data-ttu-id="f09fb-112">IIS Express은 기본적으로 Visual Studio 2017에서 사용 하는 Visual Studio 개발 서버 (Cassini 라고도 함) 보다 전체 IIS와 같은 방식으로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-112">IIS Express behaves more like full IIS than the Visual Studio Development Server (also known as Cassini), which Visual Studio 2017 uses by default.</span></span> <span data-ttu-id="f09fb-113">하지만 개발 웹 서버는 IIS와 똑같이 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-113">But neither development web server works exactly like IIS.</span></span> <span data-ttu-id="f09fb-114">따라서 앱이 Visual Studio에서 제대로 실행 되 고 테스트 되지만 IIS에 배포 되는 경우 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-114">Consequently, an app could run and test correctly in Visual Studio but fail when it's deployed to IIS.</span></span>

<span data-ttu-id="f09fb-115">다음 두 가지 방법으로 응용 프로그램을 안정적으로 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-115">You can reliably test your application in two ways:</span></span>

1. <span data-ttu-id="f09fb-116">나중에 프로덕션 환경에 배포 하는 데 사용 하는 것과 동일한 프로세스를 사용 하 여 개발 컴퓨터의 IIS에 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-116">Deploy your application to IIS on your development computer using the same process that you'll use later to deploy it to your production environment.</span></span>

   <span data-ttu-id="f09fb-117">웹 프로젝트를 실행할 때 IIS를 사용 하도록 Visual Studio를 구성할 수 있지만 배포 프로세스를 테스트 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-117">You can configure Visual Studio to use IIS when you run a web project, but that wouldn't test your deployment process.</span></span> <span data-ttu-id="f09fb-118">이 메서드는 배포 프로세스의 유효성을 검사 하 고 IIS에서 응용 프로그램이 올바르게 실행 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-118">This method validates your deployment process and that your application runs correctly under IIS.</span></span>

2. <span data-ttu-id="f09fb-119">프로덕션 환경과 유사한 테스트 환경에 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-119">Deploy your application to a test environment similar to your production environment.</span></span> 
 
   <span data-ttu-id="f09fb-120">이러한 자습서에 대 한 프로덕션 환경은 Azure App Service Web Apps 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-120">The production environment for these tutorials is Web Apps in Azure App Service.</span></span> <span data-ttu-id="f09fb-121">이상적인 테스트 환경은 Azure 서비스에서 만들어지는 추가 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-121">The ideal test environment is an additional web app created in the Azure Service.</span></span> <span data-ttu-id="f09fb-122">프로덕션 웹 앱과 동일한 방식으로 설정 되지만 테스트에만 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-122">Though it would be set up the same way as a production web app, you would only use it for testing.</span></span>

<span data-ttu-id="f09fb-123">옵션 2는 가장 안정적으로 테스트할 수 있는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-123">Option 2 is the most reliable way to test.</span></span> <span data-ttu-id="f09fb-124">옵션 2를 사용 하는 경우 옵션 1을 반드시 사용할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-124">If you use option 2, you don't necessarily need to use option 1.</span></span> <span data-ttu-id="f09fb-125">그러나 타사 호스팅 공급자에 배포 하는 경우에는 옵션 2를 사용할 수 없거나 비용이 많이 들 수 있습니다 .이 자습서 시리즈에서는 두 가지 방법을 모두 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-125">However if you're deploying to a third-party hosting provider, option 2 might not be feasible or might be expensive, so this tutorial series shows both methods.</span></span> <span data-ttu-id="f09fb-126">옵션 2에 대 한 지침은 [프로덕션 환경에 배포](deploying-to-production.md) 자습서에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-126">Guidance for option 2 is provided in the [Deploying to the Production Environment](deploying-to-production.md) tutorial.</span></span>

<span data-ttu-id="f09fb-127">Visual Studio에서 웹 서버를 사용 하는 방법에 대 한 자세한 내용은 [ASP.NET 웹 프로젝트용 Visual studio의 웹 서버](https://msdn.microsoft.com/library/58wxa9w5.aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f09fb-127">For more information about using web servers in Visual Studio, see [Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx).</span></span>

<span data-ttu-id="f09fb-128">지났으므로 자습서를 진행할 때 오류 메시지가 나타나거나 문제가 해결 되지 않으면 [문제 해결 페이지](troubleshooting.md)를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-128">Reminder: If you receive an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="download-the-contoso-university-starter-project"></a><span data-ttu-id="f09fb-129">Contoso 대학 스타터 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="f09fb-129">Download the Contoso University starter project</span></span>

<span data-ttu-id="f09fb-130">Contoso 대학 Visual Studio 시작 솔루션 및 프로젝트를 다운로드 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-130">Download and install the Contoso University Visual Studio starter solution and project.</span></span> <span data-ttu-id="f09fb-131">이 솔루션에는 완료 된 자습서가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-131">This solution contains the completed tutorial.</span></span> 

[<span data-ttu-id="f09fb-132">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="f09fb-132">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

## <a name="install-iis"></a><span data-ttu-id="f09fb-133">IIS 설치</span><span class="sxs-lookup"><span data-stu-id="f09fb-133">Install IIS</span></span>

<span data-ttu-id="f09fb-134">개발 컴퓨터에서 IIS에 배포 하려면 IIS 및 웹 배포 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-134">To deploy to IIS on your development computer, confirm that IIS and Web Deploy are installed.</span></span> <span data-ttu-id="f09fb-135">기본적으로 Visual Studio는 웹 배포를 설치 하지만 IIS는 기본 Windows 10, Windows 8 또는 Windows 7 구성에 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-135">By default, Visual Studio installs Web Deploy, but IIS isn't included in the default Windows 10, Windows 8, or Windows 7 configuration.</span></span> <span data-ttu-id="f09fb-136">IIS를 이미 설치 했 고 기본 응용 프로그램 풀이 이미 .NET 4로 설정 되어 있는 경우 [다음 섹션](#sqlexpress)으로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-136">If you've already installed IIS and the default application pool is already set to .NET 4, skip to [the next section](#sqlexpress).</span></span>

1. <span data-ttu-id="f09fb-137">[WPI (웹 플랫폼 설치 관리자)](https://www.microsoft.com/web/downloads/platform.aspx) 를 사용 하 여 IIS를 설치 하 고 웹 배포 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-137">It's recommended you use the [Web Platform Installer (WPI)](https://www.microsoft.com/web/downloads/platform.aspx) to install IIS and Web Deploy.</span></span> <span data-ttu-id="f09fb-138">WPI은 IIS를 포함 하는 권장 IIS 구성과 필요한 경우 필수 구성 요소 웹 배포 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-138">WPI installs a recommended IIS configuration that includes IIS and Web Deploy prerequisites if necessary.</span></span>

   <span data-ttu-id="f09fb-139">IIS, 웹 배포 또는 필수 구성 요소 중 하나를 이미 설치한 경우 WPI는 누락 된 항목만 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-139">If you've already installed IIS, Web Deploy, or any of their required components, the WPI installs only what is missing.</span></span>

   * <span data-ttu-id="f09fb-140">웹 플랫폼 설치 관리자를 사용 하 여 IIS 및 웹 배포를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-140">Use the Web Platform Installer to install IIS and Web Deploy:</span></span>
    
     ![WPI를 사용 하 여 IIS 설치](deploying-to-iis/_static/image30.png)

     ![WPI를 사용 하 여 웹 배포 설치](deploying-to-iis/_static/image31.png)

     <span data-ttu-id="f09fb-143">IIS 7이 설치 됨을 나타내는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-143">You'll see messages indicating that IIS 7 will be installed.</span></span> <span data-ttu-id="f09fb-144">이 링크는 Windows 8에서 IIS 8에 대해 작동 합니다. 그러나 Windows 8 이상에서는 다음 단계를 수행 하 여 ASP.NET 4.7가 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-144">The link works for IIS 8 in Windows 8; but for Windows 8 and later, go through the following steps to make sure that ASP.NET 4.7 is installed:</span></span>

   * <span data-ttu-id="f09fb-145">**제어판**프로그램 프로그램 및기능 > **Windows 기능 사용/사용 안 함을**엽니다. >  > </span><span class="sxs-lookup"><span data-stu-id="f09fb-145">Open **Control Panel** > **Programs** > **Programs and Features** > **Turn Windows features on or off**.</span></span>

   * <span data-ttu-id="f09fb-146">**인터넷 정보 서비스**, **World Wide Web 서비스**및 **응용 프로그램 개발 기능**을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-146">Expand **Internet Information Services**, **World Wide Web Services**, and **Application Development Features**.</span></span>
   
   * <span data-ttu-id="f09fb-147">**ASP.NET 4.7** 이 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-147">Confirm that **ASP.NET 4.7** is selected.</span></span>

     ![ASP.NET 4.7 선택](deploying-to-iis/_static/image1a.png)

   * <span data-ttu-id="f09fb-149">**World Wide Web Services** 및 **IIS 관리 콘솔이** 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-149">Confirm that **World Wide Web Services** and **IIS Management Console** is selected.</span></span> <span data-ttu-id="f09fb-150">그러면 IIS 및 IIS 관리자가 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-150">This installs IIS and IIS Manager.</span></span>
    
     ![World Wide Web 서비스 선택](deploying-to-iis/_static/image24.png)    
  
   * <span data-ttu-id="f09fb-152">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-152">Select **OK**.</span></span> <span data-ttu-id="f09fb-153">설치가 진행 중임을 나타내는 대화 상자 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-153">Dialog box messages indicating installation is taking place appear.</span></span>

<span data-ttu-id="f09fb-154">IIS를 설치한 후 **Iis 관리자** 를 실행 하 여 .NET Framework 버전 4가 기본 응용 프로그램 풀에 할당 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-154">After installing IIS, run **IIS Manager** to make sure that the .NET Framework version 4 is assigned to the default application pool.</span></span>

1. <span data-ttu-id="f09fb-155">WINDOWS + R을 눌러 **실행** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-155">Press WINDOWS+R to open the **Run** dialog box.</span></span>

   <span data-ttu-id="f09fb-156">Windows 8 이상에서는 **시작** 페이지에 "실행"을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-156">(On Windows 8 or later, enter "run" on the **Start** page.</span></span> <span data-ttu-id="f09fb-157">Windows 7의 경우 **시작** 메뉴에서 **실행** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-157">In Windows 7, select **Run** from the **Start** menu.</span></span> <span data-ttu-id="f09fb-158">**시작** 메뉴에 **실행** 이 없으면 작업 표시줄을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택한 다음 **시작 메뉴** 탭을 선택 하 고 **사용자 지정**을 선택 하 고 **명령 실행**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-158">If **Run** isn't in the **Start** menu, right-click the taskbar, select **Properties**, select the **Start Menu** tab, select **Customize**, and select **Run command**.)</span></span>

2. <span data-ttu-id="f09fb-159">"Inetmgr"을 입력 하 고 **확인을**선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-159">Enter "inetmgr" and select **OK**.</span></span>

3. <span data-ttu-id="f09fb-160">**연결** 창에서 서버 노드를 확장 하 고 **응용 프로그램 풀**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-160">In the **Connections** pane, expand the server node and select **Application Pools**.</span></span> <span data-ttu-id="f09fb-161">다음 그림과 같이 **DefaultAppPool** 이 .net framework 버전 4에 할당 된 경우 **응용 프로그램 풀** 창에서 다음 섹션으로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-161">In the **Application Pools** pane if **DefaultAppPool** is assigned to the .NET framework version 4 as in the following illustration, skip to the next section.</span></span>

   ![Inetmgr_showing_4.0_app_pools](deploying-to-iis/_static/image5a.png)

4. <span data-ttu-id="f09fb-163">응용 프로그램 풀이 두 개만 표시 되 고 둘 다 .NET Framework 2.0로 설정 된 경우 IIS에 ASP.NET 4를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-163">If you see only two application pools and both are set to .NET Framework 2.0, install ASP.NET 4 in IIS.</span></span>

   <span data-ttu-id="f09fb-164">Windows 8 이상에서는 ASP.NET 4.7가 설치 되어 있는지 확인 하는 방법에 대 한 이전 섹션의 지침을 참조 하거나 [windows 8 및 Windows Server 2012에 ASP.NET 4.5을 설치 하는 방법](https://support.microsoft.com/kb/2736284)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f09fb-164">For Windows 8 or later, see the previous section's instructions for making sure that ASP.NET 4.7 is installed or see [How to install ASP.NET 4.5 on Windows 8 and Windows Server 2012](https://support.microsoft.com/kb/2736284).</span></span> <span data-ttu-id="f09fb-165">Windows 7의 경우 Windows **시작** 메뉴에서 **명령 프롬프트** 를 마우스 오른쪽 단추로 클릭 하 고 **관리자 권한으로 실행**을 선택 하 여 명령 프롬프트 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-165">For Windows 7, open a command prompt window by right-clicking **Command Prompt** in the Windows **Start** menu and selecting **Run as Administrator**.</span></span> <span data-ttu-id="f09fb-166">다음 명령을 사용 하 여 [\_aspnet regiis](https://msdn.microsoft.com/library/k6h9cz8h.aspx) 를 실행 하 여 iis에 ASP.NET 4를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-166">Run [aspnet\_regiis.exe](https://msdn.microsoft.com/library/k6h9cz8h.aspx) to install ASP.NET 4 in IIS using the following commands.</span></span> <span data-ttu-id="f09fb-167">32 비트 시스템에서는 "Framework64"를 "Framework"로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-167">(In 32-bit systems, replace "Framework64" with "Framework".)</span></span>

   [!code-console[Main](deploying-to-iis/samples/sample1.cmd)]

   <span data-ttu-id="f09fb-168">이 명령은 .NET Framework 4에 대해 새 응용 프로그램 풀을 만들지만 기본 응용 프로그램 풀은 2.0로 설정 된 상태를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-168">This command creates new application pools for the .NET Framework 4, but the default application pool will remain set to 2.0.</span></span> <span data-ttu-id="f09fb-169">.NET 4를 대상으로 하는 응용 프로그램을 해당 응용 프로그램 풀에 배포 하는 중 이므로 응용 프로그램 풀을 .NET 4로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-169">You're deploying an application that targets .NET 4 to that application pool, so change the application pool to .NET 4.</span></span>

5. <span data-ttu-id="f09fb-170">**IIS 관리자**를 닫은 경우 다시 실행 하 고 서버 노드를 확장 한 다음 **응용 프로그램 풀**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-170">If you closed **IIS Manager**, run it again, expand the server node, and select **Application Pools**.</span></span>

6. <span data-ttu-id="f09fb-171">**응용 프로그램 풀** 창에서 **DefaultAppPool**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-171">In the **Application Pools** pane, select **DefaultAppPool**.</span></span> <span data-ttu-id="f09fb-172">**작업** 창에서 **기본 설정**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-172">In the **Actions** pane, select **Basic Settings**.</span></span>

   ![Inetmgr_selecting_Basic_Settings_for_app_pool](deploying-to-iis/_static/image25.png)

7. <span data-ttu-id="f09fb-174">**응용 프로그램 풀 편집** 대화 상자에서 **.net clr 버전** 을 **.net clr v 4.0.30319**로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-174">In the **Edit Application Pool** dialog box, change the **.NET CLR version** to **.NET CLR v4.0.30319**.</span></span> <span data-ttu-id="f09fb-175">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-175">Select **OK**.</span></span>

   ![Selecting_.NET_4_for_DefaultAppPool](deploying-to-iis/_static/image6a.png)

<span data-ttu-id="f09fb-177">이제 웹 응용 프로그램을 IIS에 게시할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-177">You're now ready to publish a web application to IIS.</span></span> <span data-ttu-id="f09fb-178">그러나 먼저 테스트를 위한 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-178">First, however, create databases for testing.</span></span>

<a id="sqlexpress"></a>

## <a name="install-sql-server-express"></a><span data-ttu-id="f09fb-179">SQL Server Express 설치</span><span class="sxs-lookup"><span data-stu-id="f09fb-179">Install SQL Server Express</span></span>

<span data-ttu-id="f09fb-180">LocalDB는 IIS에서 작동 하도록 설계 되지 않았으므로 테스트 환경에 SQL Server Express 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-180">LocalDB isn't designed to work in IIS, so your test environment has to have SQL Server Express installed.</span></span> <span data-ttu-id="f09fb-181">Visual Studio 2010 SQL Server Express를 사용 하는 경우 이미 기본적으로 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-181">If you're using Visual Studio 2010 SQL Server Express, it's already installed by default.</span></span> <span data-ttu-id="f09fb-182">Visual Studio 2012 이상 버전을 사용 하는 경우 SQL Server Express를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-182">If you're using Visual Studio 2012 or later, install SQL Server Express.</span></span>

<span data-ttu-id="f09fb-183">SQL Server Express를 설치 하려면 다운로드 센터에서 [다운로드 하 여 설치 합니다. Microsoft SQL Server 2017 Express edition](https://www.microsoft.com/sql-server/sql-server-editions-express)</span><span class="sxs-lookup"><span data-stu-id="f09fb-183">To install SQL Server Express, download and install it from [Download Center: Microsoft SQL Server 2017 Express edition](https://www.microsoft.com/sql-server/sql-server-editions-express).</span></span> 

<span data-ttu-id="f09fb-184">SQL Server 설치 센터의 첫 페이지에서 **새로 만들기 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가** 를 선택 하 고 지침에 따라 기본 선택 항목을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-184">On the first page of the SQL Server Installation Center, select **New SQL Server stand-alone installation or add features to an existing installation** and follow the instructions accepting the default choices.</span></span> <span data-ttu-id="f09fb-185">설치 마법사에서 기본 설정을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-185">In the installation wizard, accept the default settings.</span></span> <span data-ttu-id="f09fb-186">설치 옵션에 대 한 자세한 내용은 설치 [마법사에서 SQL Server 설치 (설치 프로그램)](https://msdn.microsoft.com/library/ms143219.aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f09fb-186">For more information about installation options, see [Install SQL Server from the Installation Wizard (Setup)](https://msdn.microsoft.com/library/ms143219.aspx).</span></span>

## <a name="create-sql-server-express-databases-for-the-test-environment"></a><span data-ttu-id="f09fb-187">테스트 환경에 대 한 SQL Server Express 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="f09fb-187">Create SQL Server Express databases for the test environment</span></span>

<span data-ttu-id="f09fb-188">Contoso 대학 응용 프로그램에는 두 개의 데이터베이스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-188">The Contoso University application has two databases:</span></span> 

1. <span data-ttu-id="f09fb-189">멤버 자격 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="f09fb-189">Membership database</span></span> 
2. <span data-ttu-id="f09fb-190">응용 프로그램 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="f09fb-190">Application database</span></span> 

<span data-ttu-id="f09fb-191">이러한 데이터베이스를 두 개의 개별 데이터베이스나 단일 데이터베이스에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-191">You can deploy these databases to two separate databases or to a single database.</span></span> <span data-ttu-id="f09fb-192">이러한 항목을 결합 하면 데이터베이스 간 조인이 쉬워집니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-192">Combining them makes database joins between them easier.</span></span> 

<span data-ttu-id="f09fb-193">타사 호스팅 공급자에 배포 하는 경우 호스팅 계획에서 결합 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-193">If you're deploying to a third-party hosting provider, your hosting plan might also give you a reason to combine them.</span></span> <span data-ttu-id="f09fb-194">예를 들어 공급자가 여러 데이터베이스에 대해 더 많은 요금을 청구 하거나 둘 이상의 데이터베이스를 허용 하지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-194">For example, the provider might charge more for multiple databases or might not even allow more than one database.</span></span>

<span data-ttu-id="f09fb-195">이 자습서에서는 테스트 환경의 두 데이터베이스와 스테이징 및 프로덕션 환경에 있는 하나의 데이터베이스에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-195">In this tutorial, you'll deploy to two databases in the test environment and to one database in the staging and production environments.</span></span>

<span data-ttu-id="f09fb-196">Visual Studio의 **보기** 메뉴에서 **서버 탐색기** (visual Web Developer의**데이터베이스 탐색기** )를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-196">From the **View** menu in Visual Studio, select **Server Explorer** (**Database Explorer** in Visual Web Developer).</span></span> <span data-ttu-id="f09fb-197">**데이터 연결** 을 마우스 오른쪽 단추로 클릭 하 고 **새 SQL Server 데이터베이스 만들기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-197">Right-click **Data Connections** and select **Create New SQL Server Database**.</span></span>

![Selecting_Create_New_SQL_Server_Database](deploying-to-iis/_static/image8.png)

<span data-ttu-id="f09fb-199">**새 SQL Server 데이터베이스 만들기** 대화 상자에서 **서버 이름** 상자에 ".\SQLExpress"를 입력 하 고 **새 데이터베이스 이름** 상자에 "ContosoUniversity"을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-199">In the **Create New SQL Server Database** dialog box, enter ".\SQLExpress" in the **Server name** box and "aspnet-ContosoUniversity" in the **New database name** box.</span></span> <span data-ttu-id="f09fb-200">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-200">Select **OK**.</span></span>

![Create aspnet-ContosoUniversity](deploying-to-iis/_static/image9.png)

<span data-ttu-id="f09fb-202">동일한 절차에 따라 이라는 `ContosoUniversity`새 SQL Server Express School 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-202">Follow the same procedure to create a new SQL Server Express School database named `ContosoUniversity`.</span></span>

<span data-ttu-id="f09fb-203">**서버 탐색기** 는 두 개의 새 데이터베이스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-203">**Server Explorer** shows the two new databases.</span></span>

![서버 탐색기의 새 데이터베이스](deploying-to-iis/_static/image10.png)

## <a name="create-a-grant-script-for-the-new-databases"></a><span data-ttu-id="f09fb-205">새 데이터베이스에 대 한 grant 스크립트 만들기</span><span class="sxs-lookup"><span data-stu-id="f09fb-205">Create a grant script for the new databases</span></span>

<span data-ttu-id="f09fb-206">응용 프로그램이 개발 컴퓨터의 IIS에서 실행 되는 경우 응용 프로그램은 기본 응용 프로그램 풀의 자격 증명을 사용 하 여 데이터베이스에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-206">When the application runs in IIS on your development computer, the application uses the default application pool's credentials to access the database.</span></span> <span data-ttu-id="f09fb-207">그러나 기본적으로 응용 프로그램 풀에는 데이터베이스를 열 수 있는 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-207">However, by default, the application pool doesn't have permission to open the databases.</span></span> <span data-ttu-id="f09fb-208">이는 해당 사용 권한을 부여 하기 위해 스크립트를 실행 해야 함을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-208">This means you need to run a script to grant that permission.</span></span> <span data-ttu-id="f09fb-209">이 섹션에서는 해당 스크립트를 만들고 나중에 실행 하 여 응용 프로그램이 IIS에서 실행 될 때 데이터베이스를 열 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-209">In this section, you'll create that script and run it later to make sure that the application can open the databases when it runs in IIS.</span></span>

<span data-ttu-id="f09fb-210">텍스트 편집기에서 다음 SQL 명령을 새 파일에 복사 하 고 *Grant .sql*로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-210">In a text editor, copy the following SQL commands into a new file and save it as *Grant.sql*.</span></span> 

[!code-sql[Main](deploying-to-iis/samples/sample2.sql)]

<span data-ttu-id="f09fb-211">Visual Studio에서 Contoso 대학 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-211">In Visual Studio, open the Contoso University solution.</span></span> <span data-ttu-id="f09fb-212">프로젝트 중 하나가 아닌 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **추가**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-212">Right-click the solution (not one of the projects), and select **Add**.</span></span> <span data-ttu-id="f09fb-213">**기존 항목**을 선택 하 고 *Grant .sql*로 이동 하 여 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-213">Select **Existing Item**, browse to *Grant.sql*, and open it.</span></span>

> [!NOTE]
> <span data-ttu-id="f09fb-214">이 스크립트는이 자습서에 지정 된 대로 2012 이상 및 Windows 10, Windows 8 또는 Windows 7의 IIS 설정에서 SQL Server Express 사용할 수 있도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-214">This script is designed to work with SQL Server Express 2012 or later and with the IIS settings in Windows 10, Windows 8, or Windows 7 as they are specified in this tutorial.</span></span> <span data-ttu-id="f09fb-215">다른 버전의 SQL Server 또는 Windows를 사용 하는 경우 또는 컴퓨터에 IIS를 다르게 설정 하는 경우이 스크립트를 변경 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-215">If you're using a different version of SQL Server or Windows, or if you set up IIS on your computer differently, changes to this script might be required.</span></span> <span data-ttu-id="f09fb-216">SQL Server 스크립트에 대 한 자세한 내용은 [SQL Server 온라인 설명서](https://go.microsoft.com/fwlink/?LinkId=132511)을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="f09fb-216">For more information about SQL Server scripts, see [SQL Server Books Online](https://go.microsoft.com/fwlink/?LinkId=132511).</span></span>

> [!NOTE] 
> <span data-ttu-id="f09fb-217">**보안 정보** 이 스크립트는 `db_owner` 런타임에 데이터베이스에 액세스 하는 사용자에 게 사용 권한을 부여 합니다 .이 작업은 프로덕션 환경에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-217">**Security Note** This script gives `db_owner` permissions to the user that accesses the database at run time, which is what you'll have in the production environment.</span></span> <span data-ttu-id="f09fb-218">일부 시나리오에서는 배포에 대해서만 전체 데이터베이스 스키마 업데이트 권한이 있는 사용자를 지정 하 고 데이터를 읽고 쓸 수 있는 권한만 있는 다른 사용자를 런타임에 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-218">In some scenarios, you might want to specify a user that has full database schema update permissions only for deployment and specify for run time a different user that has permissions only to read and write data.</span></span> <span data-ttu-id="f09fb-219">자세한 내용은이 자습서의 뒷부분에 나오는 [Code First 마이그레이션의 자동 Web.config 변경 내용 검토](#reviewingmigrations) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f09fb-219">For more information, see [Reviewing the Automatic Web.config Changes for Code First Migrations](#reviewingmigrations) later in this tutorial.</span></span>

<a id="publish"></a>

## <a name="run-the-grant-script-in-the-application-database"></a><span data-ttu-id="f09fb-220">응용 프로그램 데이터베이스에서 grant 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="f09fb-220">Run the grant script in the application database</span></span>

<span data-ttu-id="f09fb-221">데이터베이스 배포에서 [dbDacFx](https://docs.microsoft.com/iis/publish/using-web-deploy/dbdacfx-provider-for-incremental-database-publishing) 공급자를 사용 하므로 배포 중에 멤버 자격 데이터베이스에서 grant 스크립트를 실행 하도록 게시 프로필을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-221">You can configure the publish profile to run the grant script in the membership database during deployment because that database deployment uses the [dbDacFx](https://docs.microsoft.com/iis/publish/using-web-deploy/dbdacfx-provider-for-incremental-database-publishing) provider.</span></span> <span data-ttu-id="f09fb-222">응용 프로그램 데이터베이스를 배포 하는 방법 인 Code First 마이그레이션 배포 중에는 스크립트를 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-222">You can't run scripts during Code First Migrations deployment, which is how you're deploying the application database.</span></span> <span data-ttu-id="f09fb-223">즉, 응용 프로그램 데이터베이스에서 배포 하기 전에 스크립트를 수동으로 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-223">This means you have to manually run the script before deployment in the application database.</span></span>

1. <span data-ttu-id="f09fb-224">Visual Studio에서 이전에 만든 *Grant .sql* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-224">In Visual Studio, open the *Grant.sql* file that you created earlier.</span></span>

2. <span data-ttu-id="f09fb-225">**연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-225">Select **Connect**.</span></span> 

    ![연결 단추](deploying-to-iis/_static/image11.png)

3. <span data-ttu-id="f09fb-227">**서버에 연결** 대화 상자에서 **서버 이름**으로 *.\SQLExpress* 을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-227">In the **Connect to Server** dialog box, enter *.\SQLExpress* as the **Server Name**.</span></span> <span data-ttu-id="f09fb-228">**연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-228">Select **Connect**.</span></span>

4. <span data-ttu-id="f09fb-229">데이터베이스 드롭다운 목록에서 **ContosoUniversity**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-229">In the database drop-down list select **ContosoUniversity**.</span></span> <span data-ttu-id="f09fb-230">**실행**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-230">Select **Execute**.</span></span> 

   ![](deploying-to-iis/_static/image12.png)

<span data-ttu-id="f09fb-231">이제 응용 프로그램을 실행할 때 데이터베이스 테이블을 만들 수 있도록 응용 프로그램 데이터베이스에서 기본 응용 프로그램 풀 id에 충분 한 권한이 Code First 마이그레이션.</span><span class="sxs-lookup"><span data-stu-id="f09fb-231">The default application pool identity now has sufficient permissions in the application database for Code First Migrations to create the database tables when the application runs.</span></span>

## <a name="publish-to-iis"></a><span data-ttu-id="f09fb-232">IIS에 게시</span><span class="sxs-lookup"><span data-stu-id="f09fb-232">Publish to IIS</span></span>

<span data-ttu-id="f09fb-233">Visual Studio 및 웹 배포를 사용 하 여 IIS에 배포 하는 방법에는 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-233">There are several ways you can deploy to IIS using Visual Studio and Web Deploy:</span></span>

* <span data-ttu-id="f09fb-234">Visual Studio one 클릭 게시를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-234">Use Visual Studio one-click publish.</span></span>
* <span data-ttu-id="f09fb-235">명령줄에서 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-235">Publish from the command line.</span></span>
* <span data-ttu-id="f09fb-236">배포 패키지를 만들고 IIS 관리자를 사용 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-236">Create a deployment package and install it using IIS Manager.</span></span> <span data-ttu-id="f09fb-237">패키지에는 IIS에 사이트를 설치 하는 데 필요한 모든 파일 및 메타 데이터를 포함 하는 .zip 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-237">The package has a .zip file with all the files and metadata required to install a site in IIS.</span></span>
* <span data-ttu-id="f09fb-238">배포 패키지를 만들고 명령줄을 사용 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-238">Create a deployment package and install it using the command line.</span></span>

<span data-ttu-id="f09fb-239">배포 작업을 자동화 하기 위해 Visual Studio를 설정 하는 이전 자습서에서 수행한 프로세스는 이러한 모든 메서드에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-239">The process you went through in the previous tutorials to set up Visual Studio to automate deployment tasks applies to all of these methods.</span></span> <span data-ttu-id="f09fb-240">이러한 자습서에서는 처음 두 가지 방법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-240">In these tutorials, you'll use the first two methods.</span></span> <span data-ttu-id="f09fb-241">배포 패키지를 사용 하는 방법에 대 한 자세한 내용은 Visual Studio 및 ASP.NET 용 웹 배포 콘텐츠 맵에서 [웹 배포 패키지를 만들고 설치 하 여 웹 응용 프로그램 배포](https://go.microsoft.com/fwlink/p/?LinkId=282413#package) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f09fb-241">For information about using deployment packages, see [Deploying a web application by creating and installing a web deployment package](https://go.microsoft.com/fwlink/p/?LinkId=282413#package) in the Web Deployment Content Map for Visual Studio and ASP.NET.</span></span>

<span data-ttu-id="f09fb-242">게시 하기 전에 관리자 모드에서 Visual Studio를 실행 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-242">Before publishing, make sure that you're running Visual Studio in administrator mode.</span></span> <span data-ttu-id="f09fb-243">제목 표시줄에 **(관리자)** 가 표시 되지 않으면 Visual Studio를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-243">If you don't see **(Administrator)** in the title bar, close Visual Studio.</span></span> <span data-ttu-id="f09fb-244">Windows 8 이상 **시작** 페이지 또는 Windows 7 **시작** 메뉴에서 Visual Studio 아이콘을 마우스 오른쪽 단추로 클릭 하 고 **관리자 권한으로 실행**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-244">In the Windows 8 (or later) **Start** page or the Windows 7 **Start** menu, right-click the Visual Studio icon and select **Run as Administrator**.</span></span> <span data-ttu-id="f09fb-245">관리자 모드는 로컬 컴퓨터의 IIS에 게시 하는 경우에만 게시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-245">Administrator mode is only required for publishing when you're publishing to IIS on the local computer.</span></span>

### <a name="create-the-publish-profile"></a><span data-ttu-id="f09fb-246">게시 프로필 만들기</span><span class="sxs-lookup"><span data-stu-id="f09fb-246">Create the publish profile</span></span>

1. <span data-ttu-id="f09fb-247">**솔루션 탐색기**에서 **ContosoUniversity** 프로젝트가 아닌 **ContosoUniversity** 프로젝트를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-247">In **Solution Explorer**, right-click the **ContosoUniversity** project (not the **ContosoUniversity.DAL** project).</span></span> <span data-ttu-id="f09fb-248">**게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-248">Select **Publish**.</span></span> <span data-ttu-id="f09fb-249">**게시** 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-249">The **Publish** page appears.</span></span>

2. <span data-ttu-id="f09fb-250">**새 프로필**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-250">Select **New Profile**.</span></span> <span data-ttu-id="f09fb-251">**게시 대상 선택** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-251">The **Pick a publish target** dialog box appears.</span></span>

3. <span data-ttu-id="f09fb-252">**IIS, FTP 등을**선택 합니다. **프로필 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-252">Select **IIS, FTP, etc**. Select **Create Profile**.</span></span> <span data-ttu-id="f09fb-253">**게시** 마법사가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-253">The **Publish** wizard appears.</span></span>

   ![웹 게시 마법사 프로필 탭](deploying-to-iis/_static/image26.png)

4. <span data-ttu-id="f09fb-255">**게시 방법** 드롭다운 메뉴에서 **웹 배포**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-255">From the **Publish method** drop-down menu, select **Web Deploy**.</span></span>

5. <span data-ttu-id="f09fb-256">**서버**에 *localhost*를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-256">For **Server**, enter *localhost*.</span></span>

6. <span data-ttu-id="f09fb-257">**사이트 이름**에는 *기본 웹 사이트/ContosoUniversity*를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-257">For **Site name**, enter *Default Web Site/ContosoUniversity*.</span></span>

7. <span data-ttu-id="f09fb-258">**대상 URL**에 대해를 *http://localhost/ContosoUniversity* 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-258">For **Destination URL**, enter *http://localhost/ContosoUniversity*.</span></span>

   <span data-ttu-id="f09fb-259">**대상 URL** 설정은 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-259">The **Destination URL** setting isn't required.</span></span> <span data-ttu-id="f09fb-260">Visual Studio에서 응용 프로그램 배포를 마치면이 URL에 대 한 기본 브라우저가 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-260">When Visual Studio finishes deploying the application, it automatically opens your default browser to this URL.</span></span> <span data-ttu-id="f09fb-261">배포 후 브라우저를 자동으로 열지 않으려면이 상자를 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-261">If you don't want the browser to open automatically after deployment, leave this box blank.</span></span>

8. <span data-ttu-id="f09fb-262">**연결 유효성 검사** 를 선택 하 여 설정이 올바른지 확인 하 고 로컬 컴퓨터의 IIS에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-262">Select **Validate Connection** to verify that the settings are correct and you can connect to IIS on the local computer.</span></span>

   <span data-ttu-id="f09fb-263">녹색 확인 표시는 연결에 성공 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-263">A green check mark verifies that the connection is successful.</span></span>

   ![웹 게시 마법사 연결 탭](deploying-to-iis/_static/image27.png)

9. <span data-ttu-id="f09fb-265">**다음** 을 선택 하 여 **설정** 탭으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-265">Select **Next** to advance to the **Settings** tab.</span></span>

10. <span data-ttu-id="f09fb-266">**구성** 드롭다운 상자는 배포할 빌드 구성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-266">The **Configuration** drop-down box specifies the build configuration to deploy.</span></span> <span data-ttu-id="f09fb-267">기본값인 **Release**로 설정 된 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-267">Leave it set to the default value of **Release**.</span></span> <span data-ttu-id="f09fb-268">이 자습서에서는 디버그 빌드를 배포 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-268">You won't be deploying Debug builds in this tutorial.</span></span>

11. <span data-ttu-id="f09fb-269">**파일 게시 옵션**을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-269">Expand **File Publish Options**.</span></span> <span data-ttu-id="f09fb-270">**앱\_데이터 폴더에서 파일 제외**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-270">Select **Exclude files from the App\_Data folder**.</span></span>

    <span data-ttu-id="f09fb-271">테스트 환경에서 응용 프로그램은 응용 프로그램 *\_데이터* 폴더의 .mdf 파일이 아닌 로컬 SQL Server Express 인스턴스에서 만든 데이터베이스에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-271">In the test environment, the application accesses the databases that you created in the local SQL Server Express instance, not the .mdf files in the *App\_Data* folder.</span></span>

12. <span data-ttu-id="f09fb-272">게시 하 **는 동안 미리 컴파일** 을 그대로 두고 **대상에서 추가 파일 제거** 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-272">Leave the **Precompile during publishing** and **Remove additional files at destination** check boxes cleared.</span></span>

    ![설정 탭의 파일 게시 옵션](deploying-to-iis/_static/image15a.png)

    <span data-ttu-id="f09fb-274">미리 컴파일하면 주로 규모가 많은 사이트에 유용한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-274">Precompiling is an option that is useful mainly for large sites.</span></span> <span data-ttu-id="f09fb-275">사이트가 게시 된 후 페이지가 처음으로 요청 될 때 시작 시간을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-275">It can reduce startup time the first time a page is requested after the site is published.</span></span>

    <span data-ttu-id="f09fb-276">첫 번째 배포이 고 대상 폴더에 아직 파일이 없기 때문에 추가 파일을 제거할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-276">You don't need to remove additional files since this is your first deployment and there won't be any files in the destination folder yet.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f09fb-277">동일한 사이트에 대 한 후속 배포를 위해 **대상에서 추가 파일 제거** 를 선택 하는 경우 미리 보기 기능을 사용 하 여를 배포 하기 전에 파일이 삭제 되는 것을 미리 확인할 수 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-277">If you select **Remove additional files at destination** for a subsequent deployment to the same site, make sure that you use the preview feature so that you see in advance which files will be deleted before you deploy.</span></span> <span data-ttu-id="f09fb-278">예상 되는 동작은 웹 배포가 프로젝트에서 삭제 한 대상 서버에서 파일을 삭제 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-278">The expected behavior is that Web Deploy will delete files on the destination server that you have deleted in your project.</span></span> <span data-ttu-id="f09fb-279">그러나 원본 및 대상 폴더 아래의 전체 폴더 구조는 비교 됩니다. 일부 시나리오에서는 삭제 하지 않을 파일을 웹 배포 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-279">However, the entire folder structure under the source and destination folders is compared; and in some scenarios, Web Deploy might delete files you don't want to delete.</span></span>
    > 
    > <span data-ttu-id="f09fb-280">예를 들어 루트 폴더에 프로젝트를 배포할 때 서버의 하위 폴더에 웹 응용 프로그램이 있는 경우 하위 폴더가 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-280">For example if you have a web application in a subfolder on the server when you deploy a project to the root folder, the subfolder will be deleted.</span></span> <span data-ttu-id="f09fb-281">Contoso.com에 기본 사이트에 대 한 프로젝트가 하나 있고 contoso.com/blog에 블로그의 다른 프로젝트가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-281">You might have one project for the main site at contoso.com and another project for a blog at contoso.com/blog.</span></span> <span data-ttu-id="f09fb-282">블로그 응용 프로그램은 하위 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-282">The blog application is in a subfolder.</span></span> <span data-ttu-id="f09fb-283">기본 사이트를 배포할 때 **대상에서 추가 파일 제거** 를 선택 하면 블로그 응용 프로그램이 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-283">If you select **Remove additional files at destination** when you deploy the main site, the blog application will be deleted.</span></span>
    > 
    > <span data-ttu-id="f09fb-284">또 다른 예로, 앱\_데이터 폴더가 예기치 않게 삭제 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-284">For another example, your App\_Data folder might get deleted unexpectedly.</span></span> <span data-ttu-id="f09fb-285">SQL Server Compact와 같은 특정 데이터베이스는 응용 프로그램\_데이터 폴더에 데이터베이스 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-285">Certain databases such as SQL Server Compact store database files in the App\_Data folder.</span></span> <span data-ttu-id="f09fb-286">초기 배포 후에 후속 배포에서 데이터베이스 파일을 복사 하는 것을 원하지 않으므로 패키지/웹 게시 탭에서 **\_앱 데이터 제외** 를 선택 합니다. 선택한 **대상에서 추가 파일을 제거** 하는 경우 다음에 게시할 때 데이터베이스 파일과 앱\_데이터 폴더 자체가 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-286">After the initial deployment, you don't want to keep copying the database files in subsequent deployments, so you select  **Exclude App\_Data** on the Package/Publish Web tab. After you do that if you have **Remove additional files at destination** selected, your database files and the App\_Data folder itself will be deleted the next time you publish.</span></span>

### <a name="configure-deployment-for-the-membership-database"></a><span data-ttu-id="f09fb-287">멤버 자격 데이터베이스에 대 한 배포 구성</span><span class="sxs-lookup"><span data-stu-id="f09fb-287">Configure deployment for the membership database</span></span>

<span data-ttu-id="f09fb-288">다음 단계는 대화 상자의 **데이터베이스** 섹션에서 **defaultconnection** 데이터베이스에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-288">The following steps apply to the **DefaultConnection** database in the dialog box's **Databases** section.</span></span>

1. <span data-ttu-id="f09fb-289">**원격 연결 문자열** 상자에 새 SQL Server Express 멤버 자격 데이터베이스를 가리키는 다음 연결 문자열을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-289">In the **Remote connection string** box, enter the following connection string that points to the new SQL Server Express membership database.</span></span>

   [!code-console[Main](deploying-to-iis/samples/sample3.cmd)]

   <span data-ttu-id="f09fb-290">**런타임에이 연결 문자열 사용** 을 선택 했기 때문에 배포 프로세스는 배포 된 web.config 파일에이 연결 문자열을 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-290">The deployment process puts this connection string in the deployed Web.config file because **Use this connection string at runtime** is selected.</span></span>

    <span data-ttu-id="f09fb-291">**서버 탐색기**에서 연결 문자열을 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-291">You can also get the connection string from **Server Explorer**.</span></span> <span data-ttu-id="f09fb-292">**서버 탐색기**에서 **데이터 연결** 을 확장  **&lt;하 고 machinename&gt;\sqlexpress.aspnet-ContosoUniversity** 데이터베이스를 선택한 다음 **속성** 창에서 **연결 문자열을 복사 합니다.** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-292">In **Server Explorer**, expand **Data Connections** and select the **&lt;machinename&gt;\sqlexpress.aspnet-ContosoUniversity** database, then from the **Properties** window copy the **Connection String** value.</span></span> <span data-ttu-id="f09fb-293">이 연결 문자열에는 삭제할 `Pooling=False`수 있는 추가 설정이 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-293">That connection string will have one additional setting that you can delete: `Pooling=False`.</span></span>

2. <span data-ttu-id="f09fb-294">**데이터베이스 업데이트**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-294">Select **Update database**.</span></span>

   <span data-ttu-id="f09fb-295">이로 인해 배포 중에 대상 데이터베이스에 데이터베이스 스키마가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-295">This causes the database schema to be created in the destination database during deployment.</span></span> <span data-ttu-id="f09fb-296">다음 단계에서는 실행 해야 하는 추가 스크립트를 지정 합니다. 하나는 기본 응용 프로그램 풀에 대 한 데이터베이스 액세스 권한을 부여 하 고 다른 하나는 데이터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-296">In next steps, you specify the additional scripts that you need to run: one to grant database access to the default application pool and one to deploy data.</span></span>

3. <span data-ttu-id="f09fb-297">**데이터베이스 업데이트 구성**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-297">Select **Configure database updates**.</span></span>
 
4. <span data-ttu-id="f09fb-298">**데이터베이스 업데이트 구성** 대화 상자에서 **SQL 스크립트 추가**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-298">In the **Configure Database Updates** dialog box, select **Add SQL Script**.</span></span> <span data-ttu-id="f09fb-299">이전에 솔루션 폴더에 저장 한 *Grant .sql* 스크립트로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-299">Navigate to the *Grant.sql* script that you saved earlier in the solution folder.</span></span>

5. <span data-ttu-id="f09fb-300">프로세스를 반복 하 여 *aspnet-data-dev* 스크립트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-300">Repeat the process to add the *aspnet-data-dev.sql* script.</span></span>

   ![멤버 자격 데이터베이스에 대 한 데이터베이스 업데이트 구성](deploying-to-iis/_static/image16.png)

6. <span data-ttu-id="f09fb-302">**닫기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-302">Select **Close**.</span></span>

### <a name="configure-deployment-for-the-application-database"></a><span data-ttu-id="f09fb-303">응용 프로그램 데이터베이스에 대 한 배포 구성</span><span class="sxs-lookup"><span data-stu-id="f09fb-303">Configure deployment for the application database</span></span>

<span data-ttu-id="f09fb-304">`DbContext` Visual Studio는 Entity Framework 클래스를 검색 하면 **데이터베이스 업데이트** 확인란 대신 **Code First 마이그레이션 실행** 확인란이 있는 **데이터베이스** 섹션에 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-304">When Visual Studio detects an Entity Framework `DbContext` class, it creates an entry in the **Databases** section that has an **Execute Code First Migrations** check box instead of an **Update Database** check box.</span></span> <span data-ttu-id="f09fb-305">이 자습서에서는이 확인란을 사용 하 여 Code First 마이그레이션 배포를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-305">For this tutorial, you'll use that check box to specify Code First Migrations deployment.</span></span>

<span data-ttu-id="f09fb-306">일부 시나리오에서는 데이터베이스를 `DbContext` 사용할 수 있지만 마이그레이션 대신 dbDacFx 공급자를 사용 하 여 데이터베이스를 배포 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-306">In some scenarios, you might be using a `DbContext` database but you want to use the dbDacFx provider instead of Migrations to deploy the database.</span></span> <span data-ttu-id="f09fb-307">이 경우 MSDN의 ASP.NET 웹 배포 FAQ에서 [마이그레이션을 사용 하지 않고 Code First 데이터베이스 배포를 어떻게 할까요?](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f09fb-307">In that case, see [How do I deploy a Code First database without Migrations?](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) in the ASP.NET Web Deployment FAQ on MSDN.</span></span>

<span data-ttu-id="f09fb-308">다음 단계는 대화 상자의 **데이터베이스** 섹션에 있는 **schoolcontext.cs** 데이터베이스에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-308">The following steps apply to the **SchoolContext** database in the dialog box's **Databases** section.</span></span>

1. <span data-ttu-id="f09fb-309">**원격 연결 문자열** 상자에 새 SQL Server Express 응용 프로그램 데이터베이스를 가리키는 다음 연결 문자열을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-309">In the **Remote connection string** box, enter the following connection string that points to the new SQL Server Express application database.</span></span>

   [!code-console[Main](deploying-to-iis/samples/sample4.cmd)]

   <span data-ttu-id="f09fb-310">**런타임에이 연결 문자열 사용** 을 선택 했기 때문에 배포 프로세스는 배포 된 web.config 파일에이 연결 문자열을 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-310">The deployment process puts this connection string in the deployed Web.config file because **Use this connection string at runtime** is selected.</span></span>

   <span data-ttu-id="f09fb-311">또한 멤버 자격 데이터베이스 연결 문자열을 가져오는 것과 같은 방법으로 **서버 탐색기** 에서 응용 프로그램 데이터베이스 연결 문자열을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-311">You can also get the application database connection string from **Server Explorer** in the same way you got the membership database connection string.</span></span>

2. <span data-ttu-id="f09fb-312">**Code First 마이그레이션 실행 (응용 프로그램 시작 시 실행)** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-312">Select **Execute Code First Migrations (runs on application start)**.</span></span>

   <span data-ttu-id="f09fb-313">이 옵션을 선택 하면 배포 프로세스에서 배포 된 web.config 파일을 구성 하 여 `MigrateDatabaseToLatestVersion` 이니셜라이저를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-313">This option causes the deployment process to configure the deployed Web.config file to specify the `MigrateDatabaseToLatestVersion` initializer.</span></span> <span data-ttu-id="f09fb-314">이 이니셜라이저는 응용 프로그램이 배포 후 처음으로 데이터베이스에 액세스 하는 경우 데이터베이스를 최신 버전으로 자동으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-314">This initializer automatically updates the database to the latest version when the application accesses the database for the first time after deployment.</span></span>

### <a name="configure-publish-profile-transforms"></a><span data-ttu-id="f09fb-315">게시 프로필 변환 구성</span><span class="sxs-lookup"><span data-stu-id="f09fb-315">Configure publish profile transforms</span></span>

1. <span data-ttu-id="f09fb-316">**닫기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-316">Select **Close**.</span></span> <span data-ttu-id="f09fb-317">변경 내용을 저장할 것인지 묻는 메시지가 표시 되 면 **예** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-317">Select **Yes** when you are asked if you want to save changes.</span></span>

2. <span data-ttu-id="f09fb-318">**솔루션 탐색기**에서 **속성**, 기타 **프로필**을 차례로 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-318">In **Solution Explorer**, expand **Properties**, expand **PublishProfiles**.</span></span>

3. <span data-ttu-id="f09fb-319">*Customprofile. pubxml* 을 마우스 오른쪽 단추로 클릭 하 고 이름을 *Test. pubxml*로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-319">Right-click *CustomProfile.pubxml* and rename it *Test.pubxml*.</span></span>

4. <span data-ttu-id="f09fb-320">*테스트 pubxml*을 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-320">Right-click *Test.pubxml*.</span></span> <span data-ttu-id="f09fb-321">**구성 변환 추가**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-321">Select **Add Config Transform**.</span></span>

   ![구성 변환 메뉴 추가](deploying-to-iis/_static/image17.png)

   <span data-ttu-id="f09fb-323">Visual Studio에서 web.config *변환 파일을 만들고* 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-323">Visual Studio creates the *Web.Test.config* transform file and opens it.</span></span>

5. <span data-ttu-id="f09fb-324">*Web.config* 변환 파일에서 열기 구성 태그 바로 뒤에 다음 코드를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-324">In the *Web.Test.config* transform file, insert the following code immediately after the opening configuration tag.</span></span>

   [!code-xml[Main](deploying-to-iis/samples/sample5.xml)]

    <span data-ttu-id="f09fb-325">테스트 게시 프로필을 사용 하는 경우이 변환은 환경 표시기를 "Test"로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-325">When you use the Test publish profile, this transform sets the environment indicator to "Test".</span></span> <span data-ttu-id="f09fb-326">배포 된 사이트에 "Contoso 대학" H1 제목 뒤에 "(테스트)"가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-326">In the deployed site, you'll see "(Test)" after the "Contoso University" H1 heading.</span></span>

6. <span data-ttu-id="f09fb-327">파일을 저장한 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-327">Save and close the file.</span></span>

7. <span data-ttu-id="f09fb-328">*Web.config* 파일을 마우스 오른쪽 단추로 클릭 하 고 **변환 미리 보기** 를 선택 하 여 코딩 된 변환이 필요한 변경 내용을 생성 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-328">Right-click the *Web.Test.config* file and select **Preview Transform** to make sure that the transform you coded produces the expected changes.</span></span>

    <span data-ttu-id="f09fb-329">Web.config **미리 보기** 창에는 *web.config 변환과 web.config* 변환을 모두 적용 한 결과가 표시 *됩니다.*</span><span class="sxs-lookup"><span data-stu-id="f09fb-329">The **Web.config Preview** window shows the result of applying both the *Web.Release.config* transforms and the *Web.Test.config* transforms.</span></span>

### <a name="preview-the-deployment-updates"></a><span data-ttu-id="f09fb-330">배포 업데이트 미리 보기</span><span class="sxs-lookup"><span data-stu-id="f09fb-330">Preview the deployment updates</span></span>

1. <span data-ttu-id="f09fb-331">**웹 게시** 마법사를 다시 엽니다. ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**, **미리 보기**를 차례로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-331">Open the **Publish Web** wizard again (right-click the ContosoUniversity project, select **Publish**, then **Preview**).</span></span>

2. <span data-ttu-id="f09fb-332">**미리** 보기 대화 상자에서 **미리 보기 시작** 을 선택 하 여 복사할 파일의 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-332">In the **Preview** dialog box, select **Start Preview** to see a list of the files that will be copied.</span></span> 

   ![게시 미리 보기](deploying-to-iis/_static/image29.png)

   <span data-ttu-id="f09fb-334">**데이터베이스 미리 보기** 링크를 선택 하 여 멤버 자격 데이터베이스에서 실행할 스크립트를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-334">You can also select the **Preview database** link to see the scripts that will run in the membership database.</span></span> <span data-ttu-id="f09fb-335">Code First 마이그레이션 배포에 대해 스크립트가 실행 되지 않으므로 응용 프로그램 데이터베이스에 대 한 미리 보기는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-335">(No scripts are run for Code First Migrations deployment, so there's nothing to preview for the application database.)</span></span>

3. <span data-ttu-id="f09fb-336">**게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-336">Select **Publish**.</span></span>

   <span data-ttu-id="f09fb-337">Visual Studio가 관리자 모드가 아니면 사용 권한 오류 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-337">If Visual Studio is not in administrator mode, you might get a permissions error message.</span></span> <span data-ttu-id="f09fb-338">이 경우 Visual Studio를 닫고 관리자 모드에서 연 다음 다시 게시 해 보세요.</span><span class="sxs-lookup"><span data-stu-id="f09fb-338">In that case, close Visual Studio, open it in administrator mode, and try to publish again.</span></span>

   <span data-ttu-id="f09fb-339">Visual Studio가 관리자 모드에 있으면 **출력** 창에서 성공한 빌드 및 게시를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-339">If Visual Studio is in administrator mode, the **Output** window reports successful build and publish.</span></span>

   ![Output_window_publish_Test](deploying-to-iis/_static/image20.png)

   <span data-ttu-id="f09fb-341">게시 프로필 **연결** 탭의 **대상 URL** 상자에 URL을 입력 한 경우 브라우저는 컴퓨터의 IIS에서 실행 되는 Contoso 대학 홈 페이지에 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-341">If you entered the URL in the **Destination URL** box on the publish profile **Connection** tab, the browser automatically opens to the Contoso University Home page running in IIS on your computer.</span></span>

## <a name="test-in-the-test-environment"></a><span data-ttu-id="f09fb-342">테스트 환경에서 테스트</span><span class="sxs-lookup"><span data-stu-id="f09fb-342">Test in the test environment</span></span>

<span data-ttu-id="f09fb-343">환경 표시기는 환경 표시기에 대 한 *web.config 변환이 성공* 했음을 보여 주는 "(Dev)" 대신 "(테스트)"를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-343">Notice that the environment indicator shows "(Test)" instead of "(Dev)," which shows that the *Web.config* transformation for the environment indicator was successful.</span></span>

<span data-ttu-id="f09fb-344">**강사 페이지를** 실행 하 여 Code First가 강사 데이터로 데이터베이스를 시드 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-344">Run the **Instructors** page to verify that Code First seeded the database with instructor data.</span></span> <span data-ttu-id="f09fb-345">Code First 데이터베이스를 만든 다음 메서드를 `Seed` 실행 하기 때문에이 페이지를 선택 하면 로드 하는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-345">When you select this page, it may take a few minutes to load because Code First creates the database and then runs the `Seed` method.</span></span> <span data-ttu-id="f09fb-346">응용 프로그램이 아직 데이터베이스에 액세스를 시도 하지 않았기 때문에 홈 페이지에 있는 경우에는이 작업을 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-346">(It didn't do that when you were on the home page because the application didn't try to access the database yet.)</span></span>

<span data-ttu-id="f09fb-347">**학생** 탭을 선택 하 여 배포 된 데이터베이스에 학생이 없는 경우를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-347">Select the **Students** tab to verify that the deployed database has no students.</span></span>

<span data-ttu-id="f09fb-348">**학생** 메뉴에서 **학생 추가** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-348">Select **Add Students** from the **Students** menu.</span></span> <span data-ttu-id="f09fb-349">학생을 추가한 다음 **학생** 페이지에서 새 학생을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-349">Add a student, and then view the new student in the **Students** page.</span></span> <span data-ttu-id="f09fb-350">이는 데이터베이스에 성공적으로 쓸 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-350">This verifies that you can successfully write to the database.</span></span>

<span data-ttu-id="f09fb-351">**과정** 메뉴에서 **크레딧 업데이트**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-351">From the **Courses** menu, select **Update Credits**.</span></span> <span data-ttu-id="f09fb-352">[ **크레딧 업데이트** ] 페이지에는 관리자 권한이 필요 하므로 **로그인** 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-352">The **Update Credits** page requires administrator permissions, so the **Log In** page is displayed.</span></span> <span data-ttu-id="f09fb-353">이전에 만든 관리자 계정 자격 증명 ("admin" 및 "devpwd")을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-353">Enter the administrator account credentials that you created earlier ("admin" and "devpwd").</span></span> <span data-ttu-id="f09fb-354">[ **크레딧 업데이트** ] 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-354">The **Update Credits** page is displayed.</span></span> <span data-ttu-id="f09fb-355">이렇게 하면 이전 자습서에서 만든 관리자 계정이 테스트 환경에 올바르게 배포 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-355">This verifies that the administrator account that you created in the previous tutorial was correctly deployed to the test environment.</span></span>

<span data-ttu-id="f09fb-356">*C:\inetpub\wwwroot\ContosoUniversity* 폴더에 해당 하는 자리 표시자 파일만 포함 된 *ELMAH* 폴더가 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-356">Verify that an *ELMAH* folder exists in the *c:\inetpub\wwwroot\ContosoUniversity* folder with only the placeholder file in it.</span></span>

<a id="reviewingmigrations"></a>

## <a name="review-the-automatic-webconfig-changes-for-code-first-migrations"></a><span data-ttu-id="f09fb-357">Code First 마이그레이션에 대 한 자동 web.config 변경 내용 검토</span><span class="sxs-lookup"><span data-stu-id="f09fb-357">Review the automatic Web.config changes for Code First Migrations</span></span>

<span data-ttu-id="f09fb-358">*C:\inetpub\wwwroot\ContosoUniversity* 에서 배포 된 응용 프로그램의 *web.config* 파일을 열고 배포 프로세스가 Code First 마이그레이션 구성 된 위치를 확인 하 여 데이터베이스를 최신 버전으로 자동으로 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-358">Open the *Web.config* file in the deployed application at *C:\inetpub\wwwroot\ContosoUniversity* and you can see where the deployment process configured Code First Migrations to automatically update the database to the latest version.</span></span>

![](deploying-to-iis/_static/image21.png)

<span data-ttu-id="f09fb-359">또한 배포 프로세스에서는 데이터베이스 스키마를 업데이트 하는 데 독점적으로 사용할 Code First 마이그레이션에 대 한 새 연결 문자열을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-359">The deployment process also created a new connection string for Code First Migrations to use exclusively for updating the database schema:</span></span>

![Database_Publish 연결 문자열](deploying-to-iis/_static/image22.png)

<span data-ttu-id="f09fb-361">이 추가 연결 문자열을 사용 하 여 데이터베이스 스키마 업데이트에 대 한 사용자 계정과 응용 프로그램 데이터 액세스에 대 한 다른 사용자 계정을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-361">This additional connection string enables you to specify one user account for database schema updates and a different user account for application data access.</span></span> <span data-ttu-id="f09fb-362">예를 들어 db **\_소유자** 역할을 **db\_datawriter 여부** 역할을 사용 하 여 Code First 마이그레이션 및 **\_db datareader** 응용 프로그램에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-362">For example, you could assign the **db\_owner** role to Code First Migrations and **db\_datareader** with **db\_datawriter** roles to the application.</span></span> <span data-ttu-id="f09fb-363">응용 프로그램의 잠재적으로 악의적인 코드가 데이터베이스 스키마를 변경 하지 못하도록 하는 일반적인 심층 방어 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-363">This is a common defense-in-depth pattern that prevents potentially malicious code in the application from changing the database schema.</span></span> <span data-ttu-id="f09fb-364">예를 들어이 문제는 SQL 삽입 공격이 성공할 때 발생할 수 있습니다. 이러한 자습서에서는이 패턴을 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-364">(For example, this might happen in a successful SQL injection attack.) These tutorials don't use this pattern.</span></span> <span data-ttu-id="f09fb-365">시나리오에서이 패턴을 구현 하려면 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-365">To implement this pattern in your scenario, take these steps:</span></span>

1. <span data-ttu-id="f09fb-366">**웹 게시** 마법사의 **설정** 탭에서 전체 데이터베이스 스키마 업데이트 권한을 가진 사용자를 지정 하는 연결 문자열을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-366">In the **Publish Web** wizard under the **Settings** tab, enter the connection string that specifies a user with full database schema update permissions.</span></span> <span data-ttu-id="f09fb-367">**런타임에이 연결 문자열 사용** 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-367">Clear the **Use this connection string at runtime** check box.</span></span> <span data-ttu-id="f09fb-368">배포 된 web.config 파일에서 `DatabasePublish` 연결 문자열이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-368">In the deployed Web.config file, this becomes the `DatabasePublish` connection string.</span></span>

2. <span data-ttu-id="f09fb-369">응용 프로그램에서 런타임에 사용 하려는 연결 문자열에 대 한 web.config 파일 변환을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-369">Create a Web.config file transformation for the connection string that you want the application to use at run time.</span></span>

## <a name="summary"></a><span data-ttu-id="f09fb-370">요약</span><span class="sxs-lookup"><span data-stu-id="f09fb-370">Summary</span></span>

<span data-ttu-id="f09fb-371">이제 개발 컴퓨터의 IIS에 응용 프로그램을 배포 하 고 테스트 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-371">You've now deployed your application to IIS on your development computer and tested it there.</span></span>

![테스트의 홈 페이지](deploying-to-iis/_static/image23.png)

<span data-ttu-id="f09fb-373">이렇게 하면 배포 프로세스가 응용 프로그램의 콘텐츠를 올바른 위치 (배포 하지 않으려는 파일 제외)에 복사 하 고 배포 중에 IIS를 올바르게 구성 웹 배포 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-373">This verifies that the deployment process copied the application's content to the right location (excluding the files that you did not want to deploy) and also that Web Deploy configured IIS correctly during deployment.</span></span> <span data-ttu-id="f09fb-374">다음 자습서에서는 아직 수행 되지 않은 배포 작업을 찾는 테스트를 하나 더 실행 합니다. *느릅나무 ah* 폴더에 대 한 폴더 사용 권한을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-374">In the next tutorial, you'll run one more test that finds a deployment task that has not yet been done: setting folder permissions on the *Elm ah* folder.</span></span>

## <a name="more-information"></a><span data-ttu-id="f09fb-375">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="f09fb-375">More information</span></span>

<span data-ttu-id="f09fb-376">Visual Studio에서 IIS 또는 IIS Express를 실행 하는 방법에 대 한 자세한 내용은 다음 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f09fb-376">For information about running IIS or IIS Express in Visual Studio, see the following resources:</span></span>

- <span data-ttu-id="f09fb-377">IIS.net 사이트에 대 한 [개요를 IIS Express](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) 합니다.</span><span class="sxs-lookup"><span data-stu-id="f09fb-377">[IIS Express Overview](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) on the IIS.net site.</span></span>
- <span data-ttu-id="f09fb-378">Scott Guthrie의 블로그에서 [IIS Express 소개](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) .</span><span class="sxs-lookup"><span data-stu-id="f09fb-378">[Introducing IIS Express](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) on Scott Guthrie's blog.</span></span>
- <span data-ttu-id="f09fb-379">[Visual Studio에서 ASP.NET 웹 프로젝트용 웹 서버](https://msdn.microsoft.com/library/58wxa9w5.aspx).</span><span class="sxs-lookup"><span data-stu-id="f09fb-379">[Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx).</span></span>
- <span data-ttu-id="f09fb-380">[IIS와](../../older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md) ASP.NET 사이트의 ASP.NET 개발 서버의 핵심 차이점</span><span class="sxs-lookup"><span data-stu-id="f09fb-380">[Core Differences Between IIS and the ASP.NET Development Server](../../older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md) on the ASP.NET site.</span></span>

<span data-ttu-id="f09fb-381">응용 프로그램이 보통 신뢰 수준으로 실행 될 때 발생할 수 있는 문제에 대 한 자세한 내용은 Rolla 사이트에서 4 명의 회사에서 [ASP.NET 응용 프로그램을 Medium trust로 호스팅](http://www.4guysfromrolla.com/articles/100307-1.aspx) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f09fb-381">For information about what issues might arise when your application runs in medium trust, see [Hosting ASP.NET Applications in Medium Trust](http://www.4guysfromrolla.com/articles/100307-1.aspx) on the four Guys from Rolla site.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f09fb-382">[이전](project-properties.md)
> [다음](setting-folder-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="f09fb-382">[Previous](project-properties.md)
[Next](setting-folder-permissions.md)</span></span>
