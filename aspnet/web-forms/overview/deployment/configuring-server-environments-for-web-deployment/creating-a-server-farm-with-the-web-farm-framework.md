---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework
title: 웹 팜 프레임 워크를 사용 하 여 서버 팜 만들기 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 WFF (웹 팜 프레임 워크) 2.0를 사용 하 여 서버 컬렉션에서 웹 서버 팜을 만들고 구성 하는 방법에 대해 설명 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 656dd06d-806c-467c-863d-9fc45e5ba3ab
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework
msc.type: authoredcontent
ms.openlocfilehash: 204996514bed336e60ab77f184a923f04e7e2bba
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517499"
---
# <a name="creating-a-server-farm-with-the-web-farm-framework"></a><span data-ttu-id="29803-103">웹 팜 프레임워크를 사용하여 서버 팜 만들기</span><span class="sxs-lookup"><span data-stu-id="29803-103">Creating a Server Farm with the Web Farm Framework</span></span>

<span data-ttu-id="29803-104">[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="29803-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="29803-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="29803-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="29803-106">이 항목에서는 WFF (웹 팜 프레임 워크) 2.0를 사용 하 여 서버 컬렉션에서 웹 서버 팜을 만들고 구성 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-106">This topic describes how to use the Web Farm Framework (WFF) 2.0 to create and configure a web server farm from a collection of servers.</span></span>

<span data-ttu-id="29803-107">WFF를 사용 하면 부하 분산 된 여러 웹 서버에서 웹 플랫폼 제품과 구성 요소, 웹 응용 프로그램, 웹 사이트 및 구성 설정을 동기화 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-107">WFF lets you synchronize web platform products and components, web applications, websites, and configuration settings across multiple load-balanced web servers.</span></span> <span data-ttu-id="29803-108">스테이징 및 프로덕션 환경과 같은 웹 서버가 두 개 이상 필요한 시나리오에서는 배포 및 구성 프로세스를 크게 간소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-108">In scenarios where you need more than one web server, like staging and production environments, this can vastly simplify your deployment and configuration process.</span></span> <span data-ttu-id="29803-109">단일 서버&#x2014;에 *기본 서버*&#x2014;에 웹 응용 프로그램을 배포할 수 있으며, wff는 서버 팜의 다른 모든 웹 서버에서 해당 웹 응용 프로그램을 자동으로 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-109">You can deploy a web application to a single server&#x2014;the *primary server*&#x2014;and WFF will automatically replicate that web application on all the other web servers in the server farm.</span></span>

## <a name="understanding-the-web-farm-framework"></a><span data-ttu-id="29803-110">웹 팜 프레임 워크 이해</span><span class="sxs-lookup"><span data-stu-id="29803-110">Understanding the Web Farm Framework</span></span>

<span data-ttu-id="29803-111">WFF 2.0을 사용 하 여 웹 서버 그룹에 콘텐츠를 프로 비전, 관리 및 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-111">You can use WFF 2.0 to provision, manage, and deploy content to a group of web servers.</span></span> <span data-ttu-id="29803-112">WFF 배포는 다음 세 가지 주요 서버 역할로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29803-112">A WFF deployment consists of three key server roles:</span></span>

- <span data-ttu-id="29803-113">*컨트롤러 서버*입니다.</span><span class="sxs-lookup"><span data-stu-id="29803-113">The *controller server*.</span></span> <span data-ttu-id="29803-114">이 서버를 사용 하 여 WFF 서버 팜을 만들고 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-114">You use this server to create and configure WFF server farms.</span></span> <span data-ttu-id="29803-115">컨트롤러 서버는 웹 플랫폼 구성 요소, 구성 설정 및 서버 팜의 웹 서버 간 응용 프로그램의 동기화를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-115">The controller server manages the synchronization of web platform components, configuration settings, and applications between the web servers in a server farm.</span></span> <span data-ttu-id="29803-116">컨트롤러 서버에 WFF 2.0을 설치 하면 컨트롤러 서버는 서버 팜의 각 서버에 WFF 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-116">You install WFF 2.0 on the controller server, and the controller server will in turn install the WFF agent on each of the servers in a server farm.</span></span> <span data-ttu-id="29803-117">컨트롤러 서버는 개념적으로 모든 WFF 서버 팜에 속하며 단일 컨트롤러 서버는 여러 서버 팜을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-117">The controller server does not conceptually belong to any WFF server farm, and a single controller server can manage multiple server farms.</span></span> <span data-ttu-id="29803-118">이 시나리오에서는 단일 WFF 컨트롤러 서버를 사용 하 여 준비 서버 팜과 프로덕션 서버 팜을 만들고 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-118">In this scenario, you use a single WFF controller server to create and manage the staging server farm and the production server farm.</span></span>
- <span data-ttu-id="29803-119">*주 서버*입니다.</span><span class="sxs-lookup"><span data-stu-id="29803-119">The *primary server*.</span></span> <span data-ttu-id="29803-120">각 WFF 서버 팜은 단일 주 서버를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-120">Each WFF server farm includes a single primary server.</span></span> <span data-ttu-id="29803-121">웹 플랫폼 구성 요소를 설치 하거나 주 서버에 응용 프로그램을 배포 하는 경우 WFF는 서버 팜의 다른 모든 서버에 변경 내용을 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-121">When you install web platform components or deploy applications to the primary server, the WFF synchronizes your changes to all the other servers in the server farm.</span></span>
- <span data-ttu-id="29803-122">*보조 서버*입니다.</span><span class="sxs-lookup"><span data-stu-id="29803-122">The *secondary server*.</span></span> <span data-ttu-id="29803-123">각 WFF 서버 팜은 하나 이상의 보조 서버를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-123">Each WFF server farm includes one or more secondary servers.</span></span> <span data-ttu-id="29803-124">주 서버에서 수행 하는 모든 변경 내용은 서버 팜 내의 모든 보조 서버에 복제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29803-124">Any changes you make to the primary server are replicated to every secondary server within the server farm.</span></span>

<span data-ttu-id="29803-125">이러한 서버 역할이 Fabrikam, Inc. 스테이징 및 프로덕션 환경과 어떻게 관련 되는지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="29803-125">This shows how these server roles relate to the Fabrikam, Inc. staging and production environments:</span></span>

![](creating-a-server-farm-with-the-web-farm-framework/_static/image1.png)

<span data-ttu-id="29803-126">이 시나리오에서 스테이징 환경 및 프로덕션 환경은 둘 다 WFF 서버 팜으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29803-126">In this scenario, the staging environment and the production environment are both configured as WFF server farms.</span></span> <span data-ttu-id="29803-127">단일 WFF 컨트롤러 서버는 두 팜을 모두 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-127">A single WFF controller server manages both farms.</span></span> <span data-ttu-id="29803-128">각 서버 팜 내에서 주 서버에 대 한 모든 변경 내용은 모든 보조 서버에 복제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29803-128">Within each server farm, any changes to the primary server are replicated to every secondary server.</span></span>

<span data-ttu-id="29803-129">스테이징 및 프로덕션 환경 구성을 시작 하기 전에 다음 문서를 참조 하 여 WFF 2.0의 주요 개념을 숙지 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-129">Before you start to configure your staging and production environments, we recommend that you read these articles to familiarize yourself with the key concepts of WFF 2.0:</span></span>

- [<span data-ttu-id="29803-130">IIS 7 용 웹 팜 프레임 워크 2.0 개요</span><span class="sxs-lookup"><span data-stu-id="29803-130">Overview of the Web Farm Framework 2.0 for IIS 7</span></span>](https://go.microsoft.com/?linkid=9805126)
- [<span data-ttu-id="29803-131">IIS 7 용 웹 팜 프레임 워크 2.0를 사용 하 여 서버 팜 설정</span><span class="sxs-lookup"><span data-stu-id="29803-131">Setting up a Server Farm with the Web Farm Framework 2.0 for IIS 7</span></span>](https://go.microsoft.com/?linkid=9805127)
- [<span data-ttu-id="29803-132">IIS 7 용 웹 팜 프레임 워크 2.0에 대 한 시스템 및 플랫폼 요구 사항</span><span class="sxs-lookup"><span data-stu-id="29803-132">System and Platform Requirements for the Web Farm Framework 2.0 for IIS 7</span></span>](https://go.microsoft.com/?linkid=9805128)

## <a name="task-overview"></a><span data-ttu-id="29803-133">작업 개요</span><span class="sxs-lookup"><span data-stu-id="29803-133">Task Overview</span></span>

<span data-ttu-id="29803-134">이 항목의 작업 및 연습을 완료 하려면 하나 이상의 서버&#x2014;에 wff 컨트롤러 1 개, 서버 팜의 기본 웹 서버 하나, 서버 팜에 대 한 하나 이상의 보조 웹 서버가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-134">To complete the tasks and walkthroughs in this topic, you'll need at least three servers&#x2014;one WFF controller, one primary web server for the server farm, and one or more secondary web servers for the server farm.</span></span> <span data-ttu-id="29803-135">언제 든 지 WFF 서버 팜에 보조 서버를 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-135">You can add more secondary servers to a WFF server farm at any time.</span></span> <span data-ttu-id="29803-136">개략적인 수준에서 스테이징 또는 프로덕션 환경에 대 한 WFF 서버 팜을 만들고 구성 하려면 다음을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-136">At a high level, to create and configure a WFF server farm for your staging or production environment you'll need to:</span></span>

- <span data-ttu-id="29803-137">인터넷 정보 서비스 (IIS) 7.5 및 WFF 2.0를 설치 하 여 컨트롤러 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29803-137">Create a controller server by installing Internet Information Services (IIS) 7.5 and WFF 2.0.</span></span>
- <span data-ttu-id="29803-138">일반 관리자 계정을 만들고 방화벽 예외를 구성 하 여 주 서버와 보조 서버를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-138">Prepare primary and secondary servers by creating a common administrator account and configuring firewall exceptions.</span></span>
- <span data-ttu-id="29803-139">컨트롤러 서버에서 IIS 관리자를 사용 하 여 서버 팜을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-139">Configure the server farm by using IIS Manager on the controller server.</span></span>
- <span data-ttu-id="29803-140">IIS ARR (응용 프로그램 요청 라우팅) 또는 대체 부하 분산 기술을 사용 하 여 부하 분산을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-140">Configure load balancing using IIS Application Request Routing (ARR) or an alternative load-balancing technology.</span></span>

<span data-ttu-id="29803-141">이 항목의 작업 및 연습에서는 Windows Server 2008 r 2를 실행 하는 클린 서버 빌드를 시작 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-141">The tasks and walkthroughs in this topic assume that you're starting with clean server builds running Windows Server 2008 R2.</span></span> <span data-ttu-id="29803-142">시작 하기 전에 각 서버에 대해 다음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-142">Before you begin, for each server, ensure that:</span></span>

- <span data-ttu-id="29803-143">Windows Server 2008 R2 서비스 팩 1 및 사용 가능한 모든 업데이트가 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-143">Windows Server 2008 R2 Service Pack 1 and all available updates are installed.</span></span>
- <span data-ttu-id="29803-144">서버가 도메인에 가입 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-144">The server is domain-joined.</span></span>
- <span data-ttu-id="29803-145">서버에 고정 IP 주소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-145">The server has a static IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="29803-146">컴퓨터를 도메인에 가입 하는 방법에 대 한 자세한 내용은 [도메인에 컴퓨터 가입 및 로그온](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="29803-146">For more information on joining computers to a domain, see [Joining Computers to the Domain and Logging On](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx).</span></span> <span data-ttu-id="29803-147">고정 IP 주소를 구성 하는 방법에 대 한 자세한 내용은 [고정 Ip 주소 구성](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="29803-147">For more information on configuring static IP addresses, see [Configure a Static IP Address](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).</span></span>

## <a name="create-the-wff-controller-server"></a><span data-ttu-id="29803-148">WFF 컨트롤러 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="29803-148">Create the WFF Controller Server</span></span>

<span data-ttu-id="29803-149">WFF 컨트롤러 서버를 만들려면 IIS 7 이상 및 WFF 2.0 이상을 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-149">To create a WFF controller server, you'll need to install both IIS 7 or later and WFF 2.0 or later.</span></span> <span data-ttu-id="29803-150">내부적으로 WFF는 IIS 웹 배포 도구 (웹 배포) 2.x를 사용 하 여 팜의 서버를 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-150">Under the covers, WFF uses the IIS Web Deployment Tool (Web Deploy) 2.x to synchronize the servers in your farm.</span></span> <span data-ttu-id="29803-151">웹 플랫폼 설치 관리자를 사용 하 여 WFF를 설치 하는 경우 설치 관리자에서 자동으로 웹 배포를 다운로드 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-151">If you use the Web Platform Installer to install WFF, the installer will automatically download and install Web Deploy for you.</span></span>

<span data-ttu-id="29803-152">**WFF 컨트롤러 서버를 만들려면**</span><span class="sxs-lookup"><span data-stu-id="29803-152">**To create the WFF controller server**</span></span>

1. <span data-ttu-id="29803-153">[웹 플랫폼 설치 관리자](https://go.microsoft.com/?linkid=9739157)를 다운로드 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-153">Download and install the [Web Platform Installer](https://go.microsoft.com/?linkid=9739157).</span></span>
2. <span data-ttu-id="29803-154">**웹 플랫폼 설치 관리자 3.0** 창의 위쪽에서 **제품**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-154">At the top of the **Web Platform Installer 3.0** window, click **Products**.</span></span>
3. <span data-ttu-id="29803-155">창의 왼쪽에 있는 탐색 창에서 **서버**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-155">On the left side of the window, in the navigation pane, click **Server**.</span></span>
4. <span data-ttu-id="29803-156">**IIS 7 권장 구성** 행에서 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-156">In the **IIS 7 Recommended Configuration** row, click **Add**.</span></span>
5. <span data-ttu-id="29803-157"><strong>웹 팜 프레임 워크 2에서.</strong> <em>x</em> 행에서 <strong>추가</strong>를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-157">In the <strong>Web Farm Framework 2.</strong><em>x</em> row, click <strong>Add</strong>.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image2.png)
6. <span data-ttu-id="29803-158">**Install**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-158">Click **Install**.</span></span> <span data-ttu-id="29803-159">웹 플랫폼 설치 관리자는 다양 한 다른 종속성과 함께 웹 배포 도구를 설치 목록에 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-159">Notice that the Web Platform Installer has added the Web Deployment Tool, along with various other dependencies, to the installation list.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image3.png)
7. <span data-ttu-id="29803-160">사용 약관을 검토 하 고 약관에 동의 하는 경우 동의 **함**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-160">Review the license terms, and if you consent to the terms, click **I Accept**.</span></span>
8. <span data-ttu-id="29803-161">설치가 완료 되 면 **마침**을 클릭 하 고 **웹 플랫폼 설치 관리자 3.0** 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-161">When the installation is complete, click **Finish**, and then close the **Web Platform Installer 3.0** window.</span></span>

## <a name="configure-the-primary-and-secondary-servers"></a><span data-ttu-id="29803-162">주 서버 및 보조 서버 구성</span><span class="sxs-lookup"><span data-stu-id="29803-162">Configure the Primary and Secondary Servers</span></span>

<span data-ttu-id="29803-163">WFF 서버 팜을 만들기 전에 팜을 구성 하는 웹 서버에서 몇 가지 준비 작업을 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-163">Before you create a WFF server farm, you should complete some preparation tasks on the web servers that will make up the farm:</span></span>

- <span data-ttu-id="29803-164">방화벽 예외를 추가 하 여 **핵심 네트워킹**, **원격 관리**및 **파일 및 프린터 공유** 기능이 wff 컨트롤러 서버와 통신할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-164">Add firewall exceptions to allow the **Core Networking**, **Remote Administration**, and **File and Printer Sharing** features to communicate with the WFF controller server.</span></span>
- <span data-ttu-id="29803-165">Active Directory에서 도메인 계정 (예: **FABRIKAM\stagingfarm**)을 만들고 각 서버의 로컬 관리자 그룹에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-165">Create a domain account (for example, **FABRIKAM\stagingfarm**) in Active Directory and add it to the local administrators group on each server.</span></span> <span data-ttu-id="29803-166">서버 팜을 만들 때이 계정을 서버 팜 관리자 계정으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-166">You'll use this account as the server farm administrator account when you create the server farm.</span></span>

<span data-ttu-id="29803-167">Windows 방화벽에서 이러한 방화벽 예외를 구성 하는 방법에 대 한 자세한 내용은 [IIS 7 용 웹 팜 프레임 워크 2.0에 대 한 시스템 및 플랫폼 요구 사항](https://go.microsoft.com/?linkid=9805128)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="29803-167">For more information on how to configure these firewall exceptions in Windows Firewall, see [System and Platform Requirements for the Web Farm Framework 2.0 for IIS 7](https://go.microsoft.com/?linkid=9805128).</span></span> <span data-ttu-id="29803-168">다른 방화벽 시스템은 제품 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="29803-168">For other firewall systems, consult your product documentation.</span></span>

<span data-ttu-id="29803-169">Windows Server 2008 r 2의 로컬 관리자 그룹에 도메인 계정을 추가 하려면 다음 절차를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-169">You can use the next procedure to add a domain account to the local administrators group in Windows Server 2008 R2.</span></span> <span data-ttu-id="29803-170">즉, 서버 팜에&#x2014;추가 하려는 모든 서버에서이 절차를 수행 해야 합니다. 즉, 주 서버와 각 보조 서버의 로컬 관리자 그룹에 동일한 도메인 계정을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-170">You should perform this procedure on every server that you want to add to the server farm&#x2014;in other words, add the same domain account to the local administrators group on the primary server and on each secondary server.</span></span>

<span data-ttu-id="29803-171">**로컬 관리자 그룹에 도메인 계정을 추가 하려면**</span><span class="sxs-lookup"><span data-stu-id="29803-171">**To add a domain account to the local administrators group**</span></span>

1. <span data-ttu-id="29803-172">**시작** 메뉴에서 **관리 도구**를 가리킨 다음 **서버 관리자**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-172">On the **Start** menu, point to **Administrative Tools**, and then click **Server Manager**.</span></span>
2. <span data-ttu-id="29803-173">**서버 관리자** 창의 트리 뷰 창에서 **구성**, **로컬 사용자 및 그룹**을 차례로 확장 한 다음 **그룹**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-173">In the **Server Manager** window, in the tree view pane, expand **Configuration**, expand **Local Users and Groups**, and then click **Groups**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image4.png)
3. <span data-ttu-id="29803-174">**그룹** 창에서 **관리자**를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-174">In the **Groups** pane, double-click **Administrators**.</span></span>
4. <span data-ttu-id="29803-175">**관리자 속성** 대화 상자에서 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-175">In the **Administrators Properties** dialog box, click **Add**.</span></span>
5. <span data-ttu-id="29803-176">**사용자, 컴퓨터, 서비스 계정 또는 그룹 선택** 대화 상자에서 도메인 계정 (예: **FABRIKAM\stagingfarm**)을 입력 하거나 검색 한 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-176">In the **Select Users, Computers, Service Accounts, or Groups** dialog box, type (or browse) to your domain account (for example, **FABRIKAM\stagingfarm**), and then click **OK**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image5.png)
6. <span data-ttu-id="29803-177">**관리자 속성** 대화 상자에서 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-177">In the **Administrators Properties** dialog box, click **OK**.</span></span>

<span data-ttu-id="29803-178">서버를 서버 팜에 추가할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-178">Your servers are now ready to be added to a server farm.</span></span> <span data-ttu-id="29803-179">주 서버의 경우 두 경우 모두 서버 팜을&#x2014;만들기 전이나 후에 응용 프로그램 요구 사항을 충족 하도록 서버를 구성할 수 있습니다. wff는 동일한 제품, 구성 요소 또는 구성을 보조 서버에 배포 하 여 서버를 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-179">In the case of the primary server, you can configure the server to meet your application requirements before or after you create the server farm&#x2014;in both cases, the WFF will synchronize the servers by deploying the same products, components, or configuration to your secondary servers.</span></span> <span data-ttu-id="29803-180">간단히 하기 위해이 자습서에서는 서버 팜 만들기를 완료할 때 주 서버를 구성 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-180">For the sake of simplicity, this tutorial assumes that you'll configure the primary server when you've finished creating the server farm.</span></span>

## <a name="create-the-wff-server-farm"></a><span data-ttu-id="29803-181">WFF 서버 팜 만들기</span><span class="sxs-lookup"><span data-stu-id="29803-181">Create the WFF Server Farm</span></span>

<span data-ttu-id="29803-182">이 시점에서 모든 서버가 WFF 서버 팜에 추가 될 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-182">At this point, all your servers are ready to be added to a WFF server farm:</span></span>

- <span data-ttu-id="29803-183">컨트롤러 서버에 WFF를 설치 했습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-183">You've installed WFF on the controller server.</span></span>
- <span data-ttu-id="29803-184">기본 및 보조 웹 서버에서 방화벽 예외를 구성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-184">You've configured firewall exceptions on your primary and secondary web servers.</span></span>
- <span data-ttu-id="29803-185">기본 및 보조 웹 서버의 로컬 관리자 그룹에 도메인 계정을 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-185">You've added a domain account to the local administrators group on your primary and secondary web servers.</span></span>

<span data-ttu-id="29803-186">다음 단계는 WFF에서 서버 팜을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="29803-186">The next step is to create the server farm in WFF.</span></span> <span data-ttu-id="29803-187">이 작업은 WFF 컨트롤러 서버의 IIS 관리자에서 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-187">You can do this from IIS Manager on the WFF controller server.</span></span>

<span data-ttu-id="29803-188">**WFF 서버 팜을 만들려면**</span><span class="sxs-lookup"><span data-stu-id="29803-188">**To create a WFF server farm**</span></span>

1. <span data-ttu-id="29803-189">WFF 컨트롤러 서버의 **시작** 메뉴에서 **관리 도구**를 가리킨 다음 **인터넷 정보 서비스 (IIS) 관리자**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-189">On the WFF controller server, on the **Start** menu, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.</span></span>
2. <span data-ttu-id="29803-190">**연결** 창에서 로컬 서버 노드를 확장 하 고 **서버 팜**을 마우스 오른쪽 단추로 클릭 한 다음 **서버 팜 만들기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-190">In the **Connections** pane, expand the local server node, right-click **Server Farms**, and then click **Create Server Farm**.</span></span>
3. <span data-ttu-id="29803-191">**서버 팜 만들기** 대화 상자에서 서버 팜 (예: **스테이징 팜**)에 대 한 의미 있는 이름을 입력 한 다음 **서버 팜 프로 비전**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-191">In the **Create Server Farm** dialog box, type a meaningful name for the server farm (for example, **Staging Farm**), and then select **Provision server farm**.</span></span>
4. <span data-ttu-id="29803-192">각 서버의 로컬 관리자 그룹에 추가한 도메인 계정의 사용자 이름 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-192">Type the user name and password of the domain account that you added to the local administrators group on each server.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image6.png)
5. <span data-ttu-id="29803-193">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-193">Click **Next**.</span></span>
6. <span data-ttu-id="29803-194">**서버 추가** 페이지에서 주 서버의 FQDN (정규화 된 도메인 이름)을 입력 하 고 **주 서버**를 선택한 다음 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-194">On the **Add Servers** page, type the fully qualified domain name (FQDN) of the primary server, select **Primary Server**, and then click **Add**.</span></span>
7. <span data-ttu-id="29803-195">이 시점에서 WFF는 제공한 자격 증명을 사용 하 여 주 서버에 연결을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-195">At this point, WFF will attempt to contact the primary server using the credentials you provided.</span></span> <span data-ttu-id="29803-196">연결에 성공 하면 주 서버가 **서버 추가** 페이지의 테이블에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29803-196">If the connection succeeds, the primary server will be added to the table on the **Add Servers** page.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image7.png)

    > [!NOTE]
    > <span data-ttu-id="29803-197">**부하 분산에 서버를 사용할 수** 있다는 것이 기본적으로 선택 되어 있는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-197">You might have noticed that **Server is available for Load Balancing** is selected by default.</span></span> <span data-ttu-id="29803-198">WFF는 IIS ARR 모듈을 사용 하 여 부하 분산을 구현 하 고 서버 팜의 웹 서버에서 요청을 분산 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-198">WFF uses the IIS ARR module to implement load balancing and thereby distribute requests across the web servers in your server farm.</span></span> <span data-ttu-id="29803-199">대부분의 시나리오에서는 타사 부하 분산 솔루션을 대신 사용 하려는 경우 **부하 분산에 서버를 사용할 수 있음** 옵션을 선택 취소 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-199">In most scenarios, you'd only clear the **Server is available for Load Balancing** option if you wanted to use a third-party load balancing solution instead.</span></span>
8. <span data-ttu-id="29803-200">**서버 추가** 페이지에서 첫 번째 보조 서버의 FQDN을 입력 한 다음 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-200">On the **Add Servers** page, type the FQDN of your first secondary server, and then click **Add**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image8.png)
9. <span data-ttu-id="29803-201">팜의 추가 보조 서버에 대해 7 단계를 반복 하 고 **마침**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-201">Repeat step 7 for any additional secondary servers in your farm, and then click **Finish**.</span></span>

<span data-ttu-id="29803-202">이제 WFF 서버 팜이 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="29803-202">Your WFF server farm is now up and running.</span></span> <span data-ttu-id="29803-203">주 서버에 설치한 모든 웹 플랫폼 제품 또는 구성 요소와 주 서버에 배포 하는 웹 응용 프로그램이 나 콘텐츠가 모든 보조 서버에 자동으로 프로 비전 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29803-203">Any web platform products or components that you install on the primary server, and any web applications or content that you deploy to the primary server, will be automatically provisioned on all your secondary servers.</span></span>

<span data-ttu-id="29803-204">WFF는 광범위 하 고 복잡 한 항목이 며 [IIS 7 웹 사이트 용 Microsoft 웹 팜 프레임 워크 2.0](https://go.microsoft.com/?linkid=9805129) 웹 사이트에서 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-204">WFF is a broad and complex topic, and you can learn more about it on the [Microsoft Web Farm Framework 2.0 for IIS 7](https://go.microsoft.com/?linkid=9805129) website.</span></span> <span data-ttu-id="29803-205">그러나이 시점에서 알아야 하는 두 가지 기능 영역은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-205">For the time being, however, there are two features areas that you need to be aware of:</span></span>

- <span data-ttu-id="29803-206">*응용 프로그램 프로 비전은* 서버 팜의 모든 보조 서버에서 웹 응용 프로그램 및 구성 설정과 같은 주 서버에서 콘텐츠를 복제 하는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="29803-206">*Application provisioning* is the process that replicates content from the primary server, like web applications and configuration settings, across all the secondary servers in the server farm.</span></span> <span data-ttu-id="29803-207">예를 들어 기본 스테이징 서버에 Contact Manager 샘플 솔루션을 배포 하는 경우 WFF 응용 프로그램 프로 비전 프로세스는이 솔루션을 모든 보조 스테이징 서버에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-207">For example, if you deploy the Contact Manager sample solution to your primary staging server, the WFF application provisioning process will deploy this solution to all your secondary staging servers.</span></span> <span data-ttu-id="29803-208">기본적으로 응용 프로그램 프로 비전 프로세스는 30 초 마다 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29803-208">By default, the application provisioning process runs every 30 seconds.</span></span>
- <span data-ttu-id="29803-209">*플랫폼 프로 비전은* 주 서버에서 서버 팜의 모든 보조 서버에 웹 플랫폼 제품 및 구성 요소를 동기화 하는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="29803-209">*Platform provisioning* is the process that synchronizes web platform products and components from the primary server to all the secondary servers in the server farm.</span></span> <span data-ttu-id="29803-210">예를 들어 기본 준비 서버에 ASP.NET MVC 3을 설치 하는 경우 플랫폼 프로 비전 프로세스는 웹 플랫폼 설치 관리자를 사용 하 여 모든 보조 스테이징 서버에 ASP.NET MVC 3을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-210">For example, if you install ASP.NET MVC 3 on your primary staging server, the platform provisioning process will use the Web Platform Installer to install ASP.NET MVC 3 on all your secondary staging servers.</span></span> <span data-ttu-id="29803-211">기본적으로 플랫폼 프로 비전 프로세스는 5 분 마다 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29803-211">By default, the platform provisioning process runs every five minutes.</span></span>

<span data-ttu-id="29803-212">WFF 컨트롤러 서버의 IIS 관리자에서 기본 응용 프로그램 및 플랫폼 프로 비전 설정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-212">You can manage basic application and platform provisioning settings from IIS Manager on your WFF controller server.</span></span>

<span data-ttu-id="29803-213">**응용 프로그램 및 플랫폼 프로 비전 설정 살펴보기**</span><span class="sxs-lookup"><span data-stu-id="29803-213">**Explore application and platform provisioning settings**</span></span>

1. <span data-ttu-id="29803-214">IIS 관리자의 **연결** 창에서 서버 팜을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-214">In IIS Manager, in the **Connections** pane, select your server farm.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image9.png)
2. <span data-ttu-id="29803-215">**서버 팜** 창에서 **응용 프로그램 프로 비전**을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-215">In the **Server Farm** pane, double-click **Application Provisioning**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image10.png)
3. <span data-ttu-id="29803-216">여기에서 볼 수 있듯이 서버 팜은 현재 주 서버와 보조 서버 간의 웹 콘텐츠 및 구성 설정을 30 초 마다 동기화 하도록 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-216">As you can see, the server farm is currently configured to synchronize web content and configuration settings between the primary server and the secondary servers every 30 seconds.</span></span>
4. <span data-ttu-id="29803-217">**뒤로**를 클릭 한 다음 **플랫폼 프로 비전**을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-217">Click **Back**, and then double-click **Platform Provisioning**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image11.png)
5. <span data-ttu-id="29803-218">여기에서 볼 수 있듯이 서버 팜은 현재 주 서버와 보조 서버 간의 웹 플랫폼 제품과 구성 요소를 5 분 마다 동기화 하도록 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-218">As you can see, the server farm is currently configured to synchronize web platform products and components between the primary server and the secondary servers every five minutes.</span></span>
6. <span data-ttu-id="29803-219">**뒤로**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-219">Click **Back**.</span></span>
7. <span data-ttu-id="29803-220">서버 팜이 웹 플랫폼 제품을 즉시 동기화 하도록 강제 하려면 **작업** 창에서 **플랫폼 프로 비전**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-220">To force the server farm to synchronize web platform products immediately, in the **Actions** pane, click **Provision Platform**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image12.png)

    > [!NOTE]
    > <span data-ttu-id="29803-221">플랫폼 프로 비전은 다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-221">Platform provisioning may take some time.</span></span> <span data-ttu-id="29803-222">설치 관리자 프로세스는 서버 팜의 보조 서버에서 백그라운드로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29803-222">The installer process runs in the background on the secondary servers in your server farm.</span></span>
8. <span data-ttu-id="29803-223">프로 비전 프로세스가 완료 될 때까지 충분 한 시간을 허용 하면 주 서버에 추가한 제품 및 구성 요소가 보조 서버에 복제 되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-223">Once you've allowed sufficient time for the provisioning process to complete, you can verify that the products and components that you added to the primary server have now been replicated on the secondary servers.</span></span> <span data-ttu-id="29803-224">예를 들어 보조 서버에 로그온 하 고 **서버 관리자** 창을 사용 하 여 웹 서버 역할이 설치 되어 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-224">For example, you can log on to a secondary server and use the **Server Manager** window to verify that the web server role has been installed.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image13.png)
9. <span data-ttu-id="29803-225">설치 된 프로그램 목록을 확인 하 여 다양 한 웹 플랫폼 구성 요소가 추가 되었는지 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-225">You can also check the installed programs list to verify that various web platform components have been added.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image14.png)

## <a name="configure-load-balancing"></a><span data-ttu-id="29803-226">부하 분산 구성</span><span class="sxs-lookup"><span data-stu-id="29803-226">Configure Load Balancing</span></span>

<span data-ttu-id="29803-227">웹 팜을 만들 때 웹 서버 간에 HTTP 요청을 배포 하기 위해 일종의 부하 분산을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-227">When you create a web farm, you need to set up some form of load balancing to distribute HTTP requests between your web servers.</span></span> <span data-ttu-id="29803-228">이는 Windows Server 2008 네트워크 부하 분산, IIS ARR 또는 타사 소프트웨어 기반 또는 하드웨어 기반 부하 분산 솔루션 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-228">This could be Windows Server 2008 network load balancing, IIS ARR, or a third-party software-based or hardware-based load balancing solution.</span></span>

<span data-ttu-id="29803-229">WFF는 IIS ARR과 긴밀 하 게 통합 되도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-229">WFF is designed to integrate closely with IIS ARR.</span></span> <span data-ttu-id="29803-230">이 통합 기능을 활용 하려면 WFF 컨트롤러 서버에 ARR 모듈을 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-230">To take advantage of this integration, you need to install the ARR module on the WFF controller server.</span></span> <span data-ttu-id="29803-231">그런 다음 일반적으로 DNS (Domain Name System) 레코드를 구성 하 여 모든 웹 트래픽을 컨트롤러 서버로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="29803-231">You then direct all your web traffic to the controller server, typically by configuring Domain Name System (DNS) records.</span></span> <span data-ttu-id="29803-232">그러면 컨트롤러 서버는 서버 가용성 및 기타 다양 한 조건에 따라 팜의 서버 간에 들어오는 요청을 분산 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-232">The controller server will then distribute incoming requests among the servers in your farm, based on server availability and various other criteria.</span></span>

> [!NOTE]
> <span data-ttu-id="29803-233">WFF;에 ARR을 사용할 필요가 없습니다. WFF를 구성 하 여 타사 부하 분산 솔루션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-233">You don't have to use ARR with WFF; you can configure WFF to work with third-party load balancing solutions.</span></span> <span data-ttu-id="29803-234">자세한 내용은 [IIS 7 용 웹 팜 프레임 워크 2.0 개요](https://go.microsoft.com/?linkid=9805126)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="29803-234">For more information, see [Overview of the Web Farm Framework 2.0 for IIS 7](https://go.microsoft.com/?linkid=9805126).</span></span>

<span data-ttu-id="29803-235">ARR을 사용한 부하 분산은이 자습서에서 다루지 않는 복잡 한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="29803-235">Load balancing using ARR is a complex topic, most of which is beyond the scope of this tutorial.</span></span> <span data-ttu-id="29803-236">그러나 다음 절차를 사용 하 여 ARR 모듈을 설치 하 고 부하 분산을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-236">However, you can use the next procedure to install the ARR module and get started with load balancing.</span></span>

<span data-ttu-id="29803-237">**WFF 컨트롤러 서버에서 부하 분산을 설정 하려면**</span><span class="sxs-lookup"><span data-stu-id="29803-237">**To set up load balancing on the WFF controller server**</span></span>

1. <span data-ttu-id="29803-238">WFF 컨트롤러 서버에서 웹 플랫폼 설치 관리자를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-238">On the WFF controller server, launch the Web Platform Installer.</span></span>
2. <span data-ttu-id="29803-239">**웹 플랫폼 설치 관리자 3.0** 창의 위쪽에서 **제품**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-239">At the top of the **Web Platform Installer 3.0** window, click **Products**.</span></span>
3. <span data-ttu-id="29803-240">창의 왼쪽에 있는 탐색 창에서 **서버**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-240">On the left side of the window, in the navigation pane, click **Server**.</span></span>
4. <span data-ttu-id="29803-241">**응용 프로그램 요청 라우팅 2.5** 행에서 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-241">In the **Application Request Routing 2.5** row, click **Add**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image15.png)
5. <span data-ttu-id="29803-242">**설치**를 클릭 하 고 **웹 플랫폼 설치** 창의 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="29803-242">Click **Install**, and then follow the instructions in the **Web Platform Installation** window.</span></span>
6. <span data-ttu-id="29803-243">설치가 완료 되 면 IIS 관리자를 시작 하 고 **연결** 창에서 서버 팜 노드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-243">When the installation is complete, launch IIS Manager, and in the **Connections** pane, click your server farm node.</span></span> <span data-ttu-id="29803-244">**서버 팜** 창에는 여러 개의 새 아이콘이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-244">Notice that several new icons have been added to the **Server Farm** pane.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image16.png)
7. <span data-ttu-id="29803-245">**서버 팜** 창에서 **부하 분산**을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-245">In the **Server Farm** pane, double-click **Load Balance**.</span></span>
8. <span data-ttu-id="29803-246">**부하 분산** 창에서 부하 분산 알고리즘 (예: **최소 현재 요청**)을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-246">In the **Load Balance** pane, select a load balance algorithm (for example, **Least current request**).</span></span>

    > [!NOTE]
    > <span data-ttu-id="29803-247">부하 분산 알고리즘 및 기타 구성 설정에 대 한 자세한 내용은 [응용 프로그램 요청 라우팅 모듈](https://go.microsoft.com/?linkid=9805130)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="29803-247">For more information on load balancing algorithms and other configuration settings, see [Application Request Routing Module](https://go.microsoft.com/?linkid=9805130).</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image17.png)
9. <span data-ttu-id="29803-248">**작업** 창에서 **적용**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-248">In the **Actions** pane, click **Apply**.</span></span>

<span data-ttu-id="29803-249">이제 서버 팜의 서버에 대 한 기본 부하 분산을 구성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-249">You have now configured basic load balancing for the servers in your server farm.</span></span> <span data-ttu-id="29803-250">모든 웹 팜 트래픽을 컨트롤러 서버로 전달 하는 경우 요청은 가용성 및 선택한 부하 분산 알고리즘에 따라 팜의 서버 간에 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29803-250">If you direct all your web farm traffic to the controller server, the requests will be distributed between the servers in your farm according to availability and the load balancing algorithm you selected.</span></span>

<span data-ttu-id="29803-251">ARR을 사용 하 여 부하 분산을 구성 하는 방법에 대 한 자세한 내용은 [응용 프로그램 요청 라우팅 모듈](https://go.microsoft.com/?linkid=9805130)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="29803-251">For more information on how to configure load balancing with ARR, see [Application Request Routing Module](https://go.microsoft.com/?linkid=9805130).</span></span>

## <a name="monitor-the-server-farm"></a><span data-ttu-id="29803-252">서버 팜 모니터링</span><span class="sxs-lookup"><span data-stu-id="29803-252">Monitor the Server Farm</span></span>

<span data-ttu-id="29803-253">컨트롤러 서버에서 IIS 관리자를 통해 언제 든 지 서버 팜의 상태를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29803-253">You can monitor the health of your server farm at any time through IIS Manager on the controller server.</span></span> <span data-ttu-id="29803-254">**연결** 창에서 서버 팜을 확장 한 다음 **서버**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-254">In the **Connections** pane, expand your server farm, and then click **Servers**.</span></span> <span data-ttu-id="29803-255">가운데 창에는 팜의 각 서버에 대 한 요약이 최근 작업의 추적 로그와 함께 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29803-255">The center pane will show a summary of each server in the farm together with a trace log of recent activity.</span></span>

![](creating-a-server-farm-with-the-web-farm-framework/_static/image18.png)

## <a name="conclusion"></a><span data-ttu-id="29803-256">결론</span><span class="sxs-lookup"><span data-stu-id="29803-256">Conclusion</span></span>

<span data-ttu-id="29803-257">이제 WFF 서버 팜이 실행 중 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29803-257">Your WFF server farm should now be up and running.</span></span> <span data-ttu-id="29803-258">원하는&#x2014;배포 방법을 지원 하도록 주 서버를 구성할 수 있습니다. 자세한 내용은 추가 정보&#x2014;섹션을 참조 하십시오. 그러면 구성이 서버 팜의 각 보조 서버에서 복제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29803-258">You can configure the primary server to support whichever deployment approach you prefer&#x2014;see the Further Reading section for details&#x2014;and your configuration will be replicated on each secondary server in the server farm.</span></span>

## <a name="further-reading"></a><span data-ttu-id="29803-259">추가 참고 자료</span><span class="sxs-lookup"><span data-stu-id="29803-259">Further Reading</span></span>

<span data-ttu-id="29803-260">WFF 구성 및 사용의 모든 측면에 대 한 자세한 지침은 [Microsoft 웹 팜 프레임 워크 2.0 FOR IIS 7](https://go.microsoft.com/?linkid=9805129) 웹 사이트를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="29803-260">For more guidance on all aspects of configuring and using the WFF, see the [Microsoft Web Farm Framework 2.0 for IIS 7](https://go.microsoft.com/?linkid=9805129) website.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="29803-261">[이전](configuring-a-database-server-for-web-deploy-publishing.md)
> [다음](configuring-deployment-properties-for-a-target-environment.md)</span><span class="sxs-lookup"><span data-stu-id="29803-261">[Previous](configuring-a-database-server-for-web-deploy-publishing.md)
[Next](configuring-deployment-properties-for-a-target-environment.md)</span></span>
