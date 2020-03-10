---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
title: 수동으로 웹 패키지 설치 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 웹 배포 패키지를 인터넷 정보 서비스 (IIS)로 수동으로 가져오는 방법에 대해 설명 합니다. 웹 항목을 빌드 및 패키징 하는 항목 ...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f11d22a7-5d32-4ad0-8a9b-276460a61c06
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
msc.type: authoredcontent
ms.openlocfilehash: f778549d3e26989a2e71ef21171adec521842729
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78514889"
---
# <a name="manually-installing-web-packages"></a><span data-ttu-id="e4620-104">수동으로 웹 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="e4620-104">Manually Installing Web Packages</span></span>

<span data-ttu-id="e4620-105">[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="e4620-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="e4620-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="e4620-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="e4620-107">이 항목에서는 웹 배포 패키지를 인터넷 정보 서비스 (IIS)로 수동으로 가져오는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-107">This topic describes how to manually import a web deployment package into Internet Information Services (IIS).</span></span>
> 
> <span data-ttu-id="e4620-108">[웹 응용 프로그램 프로젝트 빌드 및 패키징](building-and-packaging-web-application-projects.md) 항목에서는 IIS 웹 배포 도구 (웹 배포)를 Microsoft Build Engine (MSBuild) 및 웹 게시 파이프라인 (WPP)과 함께 사용 하 여 웹 응용 프로그램 프로젝트를 단일 zip 파일로 패키지할 수 있는 방법에 대해 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-108">The topic [Building and Packaging Web Application Projects](building-and-packaging-web-application-projects.md) described how the IIS Web Deployment Tool (Web Deploy), in conjunction with the Microsoft Build Engine (MSBuild) and the Web Publishing Pipeline (WPP), lets you package your web application projects into a single zip file.</span></span> <span data-ttu-id="e4620-109">일반적으로 웹 배포 패키지 (또는 배포 패키지) 라고 하는이 파일에는 웹 서버에서 웹 응용 프로그램을 다시 만들기 위해 IIS에 필요한 모든 콘텐츠 및 구성 정보가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-109">This file, commonly known as a web deployment package (or simply a deployment package), contains all the content and configuration information that IIS needs in order to re-create your web application on a web server.</span></span>
> 
> <span data-ttu-id="e4620-110">웹 배포 패키지를 만든 후에는 다양 한 방법으로 IIS 서버에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-110">Once you've created a web deployment package, you can publish it to an IIS server in various ways.</span></span> <span data-ttu-id="e4620-111">많은 시나리오에서 MSBuild, WPP 및 웹 배포 간의 통합 요소를 활용 하 여 자동화 된 단일 단계 빌드 및 배포 프로세스의 일부로 웹 패키지를 원격으로 만들고 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-111">In a lot of scenarios, you'll want to take advantage of the integration points between MSBuild, the WPP, and Web Deploy to create and install web packages remotely as part of an automated or single-step build and deployment process.</span></span> <span data-ttu-id="e4620-112">이 프로세스는 [웹 패키지 배포](deploying-web-packages.md)에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-112">This process is described in [Deploying Web Packages](deploying-web-packages.md).</span></span> <span data-ttu-id="e4620-113">그러나이는 항상 가능 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-113">However, this isn't always possible.</span></span> <span data-ttu-id="e4620-114">인터넷 연결 프로덕션 환경에 웹 응용 프로그램을 배포 하려는 경우를 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-114">Suppose you want to deploy a web application to an Internet-facing production environment.</span></span> <span data-ttu-id="e4620-115">보안상의 이유로, 이러한 프로덕션 환경은 빌드 서버와 별도의 서브넷에 있는 방화벽을 기반으로 하는 경계 네트워크 (DMZ, 완충 지역 및 스크린 된 서브넷이 라고도 함)의 방화벽 뒤에 있을 가능성이 가장 적습니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-115">For security reasons, such a production environment is at the very least likely to be behind a firewall on a subnet that is separate from the build server, in a perimeter network (also known as DMZ, demilitarized zone, and screened subnet).</span></span> <span data-ttu-id="e4620-116">대부분의 경우 프로덕션 환경은 별도의 도메인 이나 물리적으로 격리 된 네트워크에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-116">In lots of cases, the production environment will be on a separate domain or on a physically isolated network.</span></span>
> 
> <span data-ttu-id="e4620-117">이러한 시나리오에서 유일한 옵션은 웹 패키지를 대상 서버로 이식 하 고 IIS로 수동으로 가져오는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-117">In these scenarios, your only option may be to port the web package onto the destination server and manually import it into IIS.</span></span> <span data-ttu-id="e4620-118">이 방법으로는 자동화 된 배포가 불가능 하지만 웹 응용 프로그램&#x2014;을 게시 하는 매우 효율적인 기술은 웹 서버에 단일 zip 파일을 복사 하 고 마법사를 사용 하 여 가져오기 프로세스를 안내 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-118">Although this approach precludes automated deployment, it's still a highly effective technique for publishing a web application&#x2014;you simply copy a single zip file to your web server and use a wizard to guide you through the import process.</span></span>

<span data-ttu-id="e4620-119">이 항목에서는 Fabrikam, i n c. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 기반으로 하는 일련의 자습서의 일부를 형성 합니다. 이 자습서 시리즈에서는 샘플 솔루션&#x2014;&#x2014;을 사용 [하 여](the-contact-manager-solution.md)ASP.NET MVC 3 응용 프로그램, Windows Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 비롯 한 현실적인 복잡성의 웹 응용 프로그램을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-119">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

## <a name="task-overview"></a><span data-ttu-id="e4620-120">작업 개요</span><span class="sxs-lookup"><span data-stu-id="e4620-120">Task Overview</span></span>

<span data-ttu-id="e4620-121">웹 배포 패키지를 IIS로 가져오려면 이러한 개략적인 작업을 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-121">You'll need to complete these high-level tasks to import a web deployment package into IIS:</span></span>

- <span data-ttu-id="e4620-122">MSBuild 명령줄, 팀 빌드 또는 Visual Studio 2010을 사용 하 여 웹 배포 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-122">Create a web deployment package using the MSBuild command line, Team Build, or Visual Studio 2010.</span></span>
- <span data-ttu-id="e4620-123">웹 패키지를 대상 웹 서버에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-123">Copy the web package to the destination web server.</span></span>
- <span data-ttu-id="e4620-124">IIS 관리자의 응용 프로그램 패키지 가져오기 마법사를 사용 하 여 웹 패키지를 설치 하 고 연결 문자열 및 서비스 끝점과 같은 변수에 대 한 값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-124">Use the Import Application Package Wizard in IIS Manager to install the web package and provide values for variables like connection strings and service endpoints.</span></span>

<span data-ttu-id="e4620-125">이 항목에서는 이러한 절차를 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-125">This topic will show you how to perform these procedures.</span></span> <span data-ttu-id="e4620-126">이 항목의 작업 및 연습에서는 웹 패키지, 웹 배포 및 WPP의 개념에 대해 이미 잘 알고 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-126">The tasks and walkthroughs in this topic assume that you're already familiar with the concepts behind web packages, Web Deploy, and the WPP.</span></span> <span data-ttu-id="e4620-127">자세한 내용은 [웹 응용 프로그램 프로젝트 빌드 및 패키징](building-and-packaging-web-application-projects.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e4620-127">For more information, see [Building and Packaging Web Application Projects](building-and-packaging-web-application-projects.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e4620-128">이 항목은 필요한 구성 요소를 설치 하 고 패키지를 가져오기 위해 IIS 웹 사이트를 준비 하는 방법을 설명 하는 [웹 배포 게시용 웹 서버 구성 (오프 라인 배포)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)과 함께 사용 하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-128">This topic is best used in conjunction with [Configure a Web Server for Web Deploy Publishing (Offline Deployment)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md), which explains how to install the required components and prepare an IIS website for package import.</span></span>

## <a name="create-a-web-deployment-package"></a><span data-ttu-id="e4620-129">웹 배포 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="e4620-129">Create a Web Deployment Package</span></span>

<span data-ttu-id="e4620-130">첫 번째 작업은 배포할 웹 응용 프로그램 프로젝트에 대 한 웹 배포 패키지를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-130">The first task is to create a web deployment package for the web application project you want to deploy.</span></span> <span data-ttu-id="e4620-131">다양 한 방법으로 웹 패키지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-131">You can create web packages in a variety of ways.</span></span>

<span data-ttu-id="e4620-132">**방법 1: Visual Studio를 사용 하 여 빌드 프로세스의 일부로 패키지 만들기**</span><span class="sxs-lookup"><span data-stu-id="e4620-132">**Approach 1: Create a package as part of the build process with Visual Studio**</span></span>

<span data-ttu-id="e4620-133">프로젝트 속성 페이지의 **웹 패키지 및 게시** 탭을 통해 모든 빌드 후 웹 배포 패키지를 만들도록 웹 응용 프로그램 프로젝트를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-133">You can configure your web application project to create a web deployment package after every build through the **Package/Publish Web** tab on the project property pages.</span></span> <span data-ttu-id="e4620-134">이 프로세스는 [웹 응용 프로그램 프로젝트 빌드 및 패키징](building-and-packaging-web-application-projects.md)에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-134">This process is described in [Building and Packaging Web Application Projects](building-and-packaging-web-application-projects.md).</span></span>

<span data-ttu-id="e4620-135">**방법 2: MSBuild를 사용 하 여 빌드 프로세스의 일부로 패키지 만들기**</span><span class="sxs-lookup"><span data-stu-id="e4620-135">**Approach 2: Create a package as part of the build process with MSBuild**</span></span>

<span data-ttu-id="e4620-136">사용자 지정 MSBuild 프로젝트 파일이 나 명령줄에서 MSBuild를 직접 사용 하 여 웹 응용 프로그램 프로젝트를 빌드하는 경우 명령에 **Deployonbuild = true** 및 **Deploytarget = package** 속성을 포함 하 여 빌드 프로세스의 일부로 웹 배포 패키지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-136">If you build your web application project by using MSBuild directly, either through a custom MSBuild project file or from the command line, you can create a web deployment package as part of the build process by including the **DeployOnBuild=true** and **DeployTarget=Package** properties in your command.</span></span> <span data-ttu-id="e4620-137">이 프로세스는 [빌드 프로세스 이해](understanding-the-build-process.md)에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-137">This process is described in [Understanding the Build Process](understanding-the-build-process.md).</span></span>

<span data-ttu-id="e4620-138">**방법 3: Visual Studio에서 주문형 패키지 만들기**</span><span class="sxs-lookup"><span data-stu-id="e4620-138">**Approach 3: Create a package on demand in Visual Studio**</span></span>

<span data-ttu-id="e4620-139">언제 든 지 Visual Studio 2010에서 웹 응용 프로그램 프로젝트에 대 한 웹 배포 패키지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-139">You can create a web deployment package for a web application project at any time in Visual Studio 2010.</span></span> <span data-ttu-id="e4620-140">이렇게 하려면 **솔루션 탐색기** 창에서 웹 응용 프로그램 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 **배포 패키지 빌드**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-140">To do this, in the **Solution Explorer** window, right-click your web application project, and then click **Build Deployment Package**.</span></span>

![](manually-installing-web-packages/_static/image1.png)

<span data-ttu-id="e4620-141">**방법 4: 명령줄에서 주문형 패키지 만들기**</span><span class="sxs-lookup"><span data-stu-id="e4620-141">**Approach 4: Create a package on demand from the command line**</span></span>

<span data-ttu-id="e4620-142">MSBuild를 사용 하 여 웹 응용 프로그램 프로젝트에서 **패키지** 대상을 호출 하 여 명령줄에서 웹 배포 패키지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-142">You can create a web deployment package from the command line by invoking the **Package** target on your web application project using MSBuild.</span></span> <span data-ttu-id="e4620-143">명령은 다음과 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-143">The command should resemble this:</span></span>

[!code-console[Main](manually-installing-web-packages/samples/sample1.cmd)]

<span data-ttu-id="e4620-144">어떤 방법을 사용 하 든 최종 결과는 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-144">Whichever approach you use, the end result is the same.</span></span> <span data-ttu-id="e4620-145">WPP는 웹 응용 프로그램 프로젝트의 출력 폴더에 다양 한 지원 리소스와 함께 zip 파일로 웹 배포 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-145">The WPP creates a web deployment package as a zip file, together with various supporting resources, in the output folder for your web application project.</span></span>

![](manually-installing-web-packages/_static/image2.png)

<span data-ttu-id="e4620-146">웹 패키지를 수동으로 가져올 계획인 경우 zip 파일만 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-146">When you're planning to import the web package manually, you require only the zip file.</span></span> <span data-ttu-id="e4620-147">이 파일을 대상 웹 서버에 복사 하 고 가져오기 프로세스를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-147">Copy this file to your target web server and you can begin the import process.</span></span>

## <a name="import-a-web-package-into-iis"></a><span data-ttu-id="e4620-148">웹 패키지를 IIS로 가져오기</span><span class="sxs-lookup"><span data-stu-id="e4620-148">Import a Web Package into IIS</span></span>

<span data-ttu-id="e4620-149">다음 절차를 사용 하 여 로컬 파일 시스템에서 IIS 웹 사이트로 웹 배포 패키지를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-149">You can use the next procedure to import a web deployment package from the local file system into an IIS website.</span></span> <span data-ttu-id="e4620-150">이 절차를 수행 하기 전에 다음이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-150">Before you perform this procedure, ensure that you have:</span></span>

- <span data-ttu-id="e4620-151">웹 배포 패키지를 웹 서버에 복사 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-151">Copied the web deployment package to the web server.</span></span>
- <span data-ttu-id="e4620-152">응용 프로그램을 호스팅하도록 IIS 웹 서버를 구성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-152">Configured an IIS web server to host your application.</span></span>

<span data-ttu-id="e4620-153">웹 배포 패키지를 지원 하도록 IIS 웹 서버를 구성 하는 방법에 대 한 자세한 내용은 [웹 배포 게시용 웹 서버 구성 (오프 라인 배포)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e4620-153">For more information on configuring an IIS web server to support web deployment packages, see [Configure a Web Server for Web Deploy Publishing (Offline Deployment)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md).</span></span>

<span data-ttu-id="e4620-154">**IIS 관리자를 사용 하 여 웹 배포 패키지를 가져오려면**</span><span class="sxs-lookup"><span data-stu-id="e4620-154">**To import a web deployment package using IIS Manager**</span></span>

1. <span data-ttu-id="e4620-155">IIS 관리자의 **연결** 창에서 iis 웹 사이트를 마우스 오른쪽 단추로 클릭 하 고 **배포**를 가리킨 다음 **응용 프로그램 가져오기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-155">In IIS Manager, in the **Connections** pane, right-click your IIS website, point to **Deploy**, and then click **Import Application**.</span></span>

    ![](manually-installing-web-packages/_static/image3.png)
2. <span data-ttu-id="e4620-156">응용 프로그램 패키지 가져오기 마법사의 **패키지 선택** 페이지에서 웹 배포 패키지의 위치로 이동한 후 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-156">In the Import Application Package Wizard, on the **Select the Package** page, browse to the location of your web deployment package, and then click **Next**.</span></span>
3. <span data-ttu-id="e4620-157">**패키지 콘텐츠 선택** 페이지에서 필요 하지 않은 콘텐츠를 모두 선택 취소 하 고 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-157">On the **Select the Contents of the Package** page, clear any content that you don't require, and then click **Next**.</span></span>

    ![](manually-installing-web-packages/_static/image4.png)

    > [!NOTE]
    > <span data-ttu-id="e4620-158">많은 경우에 웹 배포 패키지와 함께 제공 되는 모든 항목을 가져오지 않으려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-158">In a lot of cases, you may not want to import everything that comes with a web deployment package.</span></span> <span data-ttu-id="e4620-159">예를 들어 웹 배포 연결 된 데이터베이스를 대체할 수 있도록 허용 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-159">For example, you may not want to allow Web Deploy to replace the associated database.</span></span>  
    > <span data-ttu-id="e4620-160">**권한 부여** 항목은 응용 프로그램 풀 id가 웹 사이트 콘텐츠를 저장 하는 물리적 폴더에 액세스할 수 있도록 대상 파일 시스템에 대 한 권한을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-160">The **Grant permissions** entries set permissions on the destination file system to ensure that the application pool identity can access the physical folder that stores the website content.</span></span> <span data-ttu-id="e4620-161">또한 익명 인증 사용자에 게는 응용 프로그램에서 MIME (다목적 Internet Mail Extensions) 형식 파일을 제공할 수 있도록 폴더에 대 한 읽기 권한이 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-161">In addition, the anonymous authentication user is granted read permission to the folder to let the application serve Multipurpose Internet Mail Extensions (MIME) type files.</span></span> <span data-ttu-id="e4620-162">원하는 경우 이러한 항목을 제거 하 고 수동으로 사용 권한을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-162">If you prefer, you can remove these entries and configure permissions manually.</span></span>
4. <span data-ttu-id="e4620-163">**응용 프로그램 패키지 정보 입력** 페이지에서 요청 된 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-163">On the **Enter Application Package Information** page, provide the requested information.</span></span>

    ![](manually-installing-web-packages/_static/image5.png)
5. <span data-ttu-id="e4620-164">웹 패키지를 만들 때 WPP는 응용 프로그램에 대 한 구성 파일을 분석 하 고 연결 문자열 및 서비스 끝점과 같은 모든 변수를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-164">When you create a web package, the WPP analyzes the configuration file for your application and detects any variables, like connection strings and service endpoints.</span></span> <span data-ttu-id="e4620-165">이 경우 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-165">In this case:</span></span>

    1. <span data-ttu-id="e4620-166">**응용 프로그램 경로** 는 응용 프로그램을 설치 하려는 IIS 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-166">**Application Path** is the IIS path where you want to install your application.</span></span> <span data-ttu-id="e4620-167">이 설정은 WPP에서 만드는 모든 배포 패키지에 공통적입니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-167">This setting is common to all deployment packages that the WPP creates.</span></span>
    2. <span data-ttu-id="e4620-168">**연락처 서비스 끝점 주소** 는 응용 프로그램이 배포 된 WCF 서비스와 통신 하는 데 사용 해야 하는 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-168">**ContactService Service Endpoint Address** is the address that the application should use to communicate with the deployed WCF service.</span></span> <span data-ttu-id="e4620-169">이 설정은 web.config 파일의 항목에 해당 *합니다.*</span><span class="sxs-lookup"><span data-stu-id="e4620-169">This setting corresponds to an entry in the *web.config* file.</span></span>
    3. <span data-ttu-id="e4620-170">첫 번째 **연결 문자열** 설정은 응용 프로그램과 연결 된 데이터베이스 (이 경우 ASP.NET membership database)를 배포 하는 데 사용 해야 하 웹 배포는 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-170">The first **Connection String** setting is the connection string that Web Deploy should use to deploy the database associated with the application (in this case an ASP.NET membership database).</span></span> <span data-ttu-id="e4620-171">이 설정은 Visual Studio의 **SQL 패키지 및 게시** 탭에 있는 설정에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-171">This setting corresponds to the setting on the **Package/Publish SQL** tab in Visual Studio.</span></span>
    4. <span data-ttu-id="e4620-172">두 번째 **연결 문자열** 설정은 응용 프로그램이 실행 될 때 데이터베이스와 통신 하는 데 실제로 사용 하는 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-172">The second **Connection String** setting is the connection string that your application will actually use to communicate with the database when it's up and running.</span></span> <span data-ttu-id="e4620-173">이 *는 web.config 파일의* 연결 문자열 항목에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-173">This corresponds to a connection string entry in the *web.config* file.</span></span>

        > [!NOTE]
        > <span data-ttu-id="e4620-174">이러한 매개 변수를 제공 하는 위치에 대 한 자세한 내용은 [웹 패키지 배포에 대 한 매개 변수 구성](configuring-parameters-for-web-package-deployment.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e4620-174">For more information on where these parameters come from, see [Configuring Parameters for Web Package Deployment](configuring-parameters-for-web-package-deployment.md).</span></span>
6. <span data-ttu-id="e4620-175">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-175">Click **Next**.</span></span>
7. <span data-ttu-id="e4620-176">이 웹 사이트에 응용 프로그램을 처음 배포 하는 경우를 설치 하기 전에 기존 콘텐츠를 모두 삭제할지 여부를 지정 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-176">If this is not the first time you've deployed the application to this website, you'll be prompted to specify whether you want to delete all existing content prior to installation.</span></span> <span data-ttu-id="e4620-177">요구 사항에 적합 한 옵션을 선택 하 고 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-177">Choose the option that's appropriate for your requirements, and then click **Next**.</span></span>

    ![](manually-installing-web-packages/_static/image6.png)
8. <span data-ttu-id="e4620-178">IIS에서 패키지 설치를 완료 한 후 **마침**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-178">When IIS has finished installing the package, click **Finish**.</span></span>

    ![](manually-installing-web-packages/_static/image7.png)

<span data-ttu-id="e4620-179">이 시점에서 IIS에 웹 응용 프로그램을 게시 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-179">At this point, you've successfully published your web application to IIS.</span></span>

## <a name="conclusion"></a><span data-ttu-id="e4620-180">결론</span><span class="sxs-lookup"><span data-stu-id="e4620-180">Conclusion</span></span>

<span data-ttu-id="e4620-181">이 항목에서는 IIS 관리자를 사용 하 여 웹 배포 패키지를 IIS 웹 사이트로 가져오는 방법에 대해 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-181">This topic described how to import a web deployment package into an IIS website using IIS Manager.</span></span> <span data-ttu-id="e4620-182">이 웹 응용 프로그램 게시 방식은 보안 또는 인프라 제약 조건으로 인해 원격 배포가 불가능 하거나 바람직하지 않은 경우에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4620-182">This approach to web application publishing is appropriate when security or infrastructure constraints make remote deployment impossible or undesirable.</span></span>

## <a name="further-reading"></a><span data-ttu-id="e4620-183">추가 참고 자료</span><span class="sxs-lookup"><span data-stu-id="e4620-183">Further Reading</span></span>

<span data-ttu-id="e4620-184">웹 패키지를 수동으로 가져오는 기능을 지원 하도록 IIS 웹 서버를 구성 하는 방법에 대 한 지침은 [웹 배포 게시용 웹 서버 구성 (오프 라인 배포)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e4620-184">For guidance on how to configure an IIS web server to support manually importing a web package, see [Configure a Web Server for Web Deploy Publishing (Offline Deployment)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md).</span></span> <span data-ttu-id="e4620-185">웹 패키지를 배포 하는 방법에 대 한 일반적인 지침은 [연습: 웹 배포 패키지를 사용 하 여 웹 응용 프로그램 프로젝트 배포 (1/4 부)](https://msdn.microsoft.com/library/dd483479.aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e4620-185">For more general guidance on deploying web packages, see [Walkthrough: Deploying a Web Application Project Using a Web Deployment Package (Part 1 of 4)](https://msdn.microsoft.com/library/dd483479.aspx).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="e4620-186">이전</span><span class="sxs-lookup"><span data-stu-id="e4620-186">Previous</span></span>](creating-and-running-a-deployment-command-file.md)
