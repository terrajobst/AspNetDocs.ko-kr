---
uid: whitepapers/side-by-side-with-10
title: ASP.NET .NET Framework 1.0 및 1.1의 Side-by-side 실행 | Microsoft Docs
author: rick-anderson
description: 이 백서에서는 컴퓨터에 .NET 1.0 및 .NET 1.1를 모두 설치 하 여 ASP.NET 웹 응용 프로그램이 두 버전의 fram에서 실행 되도록 하는 방법에 대해 설명 합니다.
ms.author: riande
ms.date: 02/10/2010
ms.assetid: bdea2003-e964-4db5-9092-d56cc7560616
msc.legacyurl: /whitepapers/side-by-side-with-10
msc.type: content
ms.openlocfilehash: c123545099013af71569bce4707f2b3eb732c344
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78513833"
---
# <a name="aspnet-side-by-side-execution-of-net-framework-10-and-11"></a><span data-ttu-id="db6bb-103">.NET Framework 1.0 및 1.1의 ASP.NET Side-by-Side 실행</span><span class="sxs-lookup"><span data-stu-id="db6bb-103">ASP.NET Side-by-Side Execution of .NET Framework 1.0 and 1.1</span></span>

> <span data-ttu-id="db6bb-104">이 백서에서는 컴퓨터에 .NET 1.0 및 .NET 1.1를 모두 설치 하 여 ASP.NET 웹 응용 프로그램이 두 가지 버전의 프레임 워크에서 실행 될 수 있도록 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-104">This whitepaper describes how to install both .NET 1.0 and .NET 1.1 on your machine, allowing an ASP.NET Web application to run on either version of the framework.</span></span>
> 
> <span data-ttu-id="db6bb-105">ASP.NET 1.0 및 ASP.NET 1.1에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-105">Applies to ASP.NET 1.0 and ASP.NET 1.1.</span></span>

<span data-ttu-id="db6bb-106">ASP.NET에서는 응용 프로그램을 동일한 컴퓨터에 설치 하 고 다른 버전의 .NET Framework를 사용 하는 경우 함께 실행 하는 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-106">In ASP.NET, applications are said to be running side by side when they are installed on the same computer, but use different versions of the .NET Framework.</span></span> <span data-ttu-id="db6bb-107">다음 항목에서는 side-by-side 실행을 위해 ASP.NET 응용 프로그램을 구성 하는 방법에 대해 설명 하 고 다음에 대 한 자세한 단계를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-107">The following topic describes how to configure ASP.NET applications for side-by-side execution and provides detailed steps to:</span></span>

- [<span data-ttu-id="db6bb-108">설치 하는 동안 .NET Framework 버전 1.0에 대 한 웹 응용 프로그램의 매핑을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-108">Maintain your Web application's mapping to .NET Framework version 1.0 during installation</span></span>](#1)
- [<span data-ttu-id="db6bb-109">웹 응용 프로그램을 특정 버전의 .NET Framework에 매핑</span><span class="sxs-lookup"><span data-stu-id="db6bb-109">Map a Web application to a specific version of the .NET Framework</span></span>](#2)
- [<span data-ttu-id="db6bb-110">웹 사이트에서 사용 하는 .NET Framework 버전 찾기</span><span class="sxs-lookup"><span data-stu-id="db6bb-110">Find the version of the .NET Framework that a Web site is using</span></span>](#3)

<span data-ttu-id="db6bb-111">일반적으로 컴퓨터에서 구성 요소나 응용 프로그램을 업데이트 하면 이전 버전이 제거 되 고 최신 버전으로 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-111">Traditionally, when a component or application is updated on a computer, the older version is removed and replaced with the newer version.</span></span> <span data-ttu-id="db6bb-112">새 버전이 이전 버전과 호환 되지 않는 경우이는 일반적으로 구성 요소 또는 응용 프로그램을 사용 하는 다른 응용 프로그램을 중단 합니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-112">If the new version is not compatible with the previous version, this usually breaks other applications that use the component or application.</span></span> <span data-ttu-id="db6bb-113">.NET Framework는 side-by-side 실행을 지원 합니다 .이를 통해 여러 버전의 어셈블리 또는 응용 프로그램을 동시에 같은 컴퓨터에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-113">The .NET Framework provides support for side-by-side execution, which allows multiple versions of an assembly or application to be installed on the same computer at the same time.</span></span> <span data-ttu-id="db6bb-114">여러 버전을 동시에 설치할 수 있으므로 관리 되는 응용 프로그램은 다른 버전을 사용 하는 응용 프로그램에 영향을 주지 않고 사용할 버전을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-114">Because multiple versions can be installed simultaneously, managed applications can select which version to use without affecting applications that use a different version.</span></span>

<span data-ttu-id="db6bb-115">기본적으로 .NET Framework 버전 1.1을 설치 하는 동안 모든 기존 ASP.NET 응용 프로그램은 최신 버전의 .NET Framework를 사용 하도록 자동으로 다시 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-115">By default, during the installation of the .NET Framework version 1.1, all existing ASP.NET applications are automatically reconfigured to use the latest version of the .NET Framework.</span></span> <span data-ttu-id="db6bb-116">ASP.NET 응용 프로그램을 기본적으로 .NET Framework 1.1으로 설정 하지 않으려는 경우 설치 하는 동안이를 방지 하는 방법을 알아보려면 [여기](#1) 를 클릭 하십시오.</span><span class="sxs-lookup"><span data-stu-id="db6bb-116">If you do not want your ASP.NET applications to default to .NET Framework 1.1, click [here](#1) to learn how to prevent this during installation.</span></span>

<span data-ttu-id="db6bb-117">1\.1 .NET Framework 웹 서버를 업데이트 하 고 하나 이상의 웹 응용 프로그램을 .NET Framework 1.0를 실행 하려면 인터넷 정보 서비스 (IIS) 스크립트 맵을 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-117">If you update your Web server to .NET Framework 1.1 and want one or more Web applications to run .NET Framework 1.0, you need to update the Internet Information Services (IIS) Script Map.</span></span> <span data-ttu-id="db6bb-118">스크립트 매핑은 특정 웹 응용 프로그램에 대 한 .aspx 파일 확장명을 .NET Framework 버전에 매핑하는 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-118">The script mapping is the mechanism to map the .aspx file extension for a specific Web application to a version of the .NET Framework.</span></span> <span data-ttu-id="db6bb-119">웹 응용 프로그램을 특정 버전의 .NET Framework에 매핑하는 방법을 알아보려면 [여기](#2) 를 클릭 하십시오.</span><span class="sxs-lookup"><span data-stu-id="db6bb-119">Click [here](#2) to learn how to map a Web application to a specific version of the .NET Framework.</span></span>

<span data-ttu-id="db6bb-120">인터넷 정보 관리자 또는 ASP.NET IIS 등록 도구 (Aspnet\_regiis .exe)를 사용 하 여 특정 웹 응용 프로그램을 실행 하는 .NET Framework 버전을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-120">You can use the Internet Information Manger or the ASP.NET IIS Registration Tool (Aspnet\_regiis.exe) to find which .NET Framework version is running a particular Web application.</span></span> <span data-ttu-id="db6bb-121">웹 사이트에서 사용 하는 .NET Framework 버전을 확인 하는 방법을 알아보려면 [여기](#3) 를 클릭 하십시오.</span><span class="sxs-lookup"><span data-stu-id="db6bb-121">Click [here](#3) to learn how to find the version of the .NET Framework that a Web site is using.</span></span>

<span data-ttu-id="db6bb-122">.NET Framework 1.1으로 마이그레이션하는 경우의 한 가지 가져오기 고려 사항은 .NET Framework의 각 버전이 자체 Machine.config 파일을 사용 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-122">One import consideration when migrating to .NET Framework 1.1 is that each version of the .NET Framework uses its own Machine.config file.</span></span> <span data-ttu-id="db6bb-123">따라서 web.config 파일을 변경 하는 경우에는 해당 변경 내용을 .NET Framework 1.1 Machine.config 파일로 마이그레이션해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-123">As a result, if a Web administrator has made changes to the Machine.config file, those changes must be migrated to the .NET Framework 1.1 Machine.config file.</span></span>

<a id="1"></a>

## <a name="maintaining-your-web-applications-mapping-to-net-framework-10-during-installation"></a><span data-ttu-id="db6bb-124">설치 하는 동안 .NET Framework 1.0에 대 한 웹 응용 프로그램의 매핑 유지 관리</span><span class="sxs-lookup"><span data-stu-id="db6bb-124">Maintaining your Web application's mapping to .NET Framework 1.0 during installation</span></span>

<span data-ttu-id="db6bb-125">기본적으로 모든 기존 ASP.NET 응용 프로그램은 설치 중에 자동으로 다시 구성 되어 최신 버전의 .NET Framework을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-125">By default, all existing ASP.NET applications are automatically reconfigured during installation to use the newer version of the .NET Framework.</span></span> <span data-ttu-id="db6bb-126">최신 버전의 .NET Framework을 사용 하 여 응용 프로그램은 새로운 릴리스에 포함 된 향상 된 기능 및 새로운 기능을 모두 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-126">Using the newer version of the .NET Framework, applications can take full advantage of improvements and new features included in the new release.</span></span> <span data-ttu-id="db6bb-127">이와 동시에 업데이트 되는 응용 프로그램을 세밀 하 게 제어할 수 있는 웹 관리자는 .NET Framework 설치 하는 동안 모든 기존 ASP.NET 응용 프로그램을 자동으로 다시 매핑할 수 없도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-127">At the same time, the Web administrator, who might want granular control over which applications are updated, can prevent the automatic remapping of all existing ASP.NET applications during installation of the .NET Framework.</span></span>

<span data-ttu-id="db6bb-128">전체 ASP.NET 응용 프로그램이 최신 버전의 .NET Framework 자동으로 다시 매핑 되지 않도록 웹 관리자는 Dotnetfx.exe 설치 프로그램과 함께/noaspupgrade 명령줄 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-128">To prevent the automatic remapping of the entire ASP.NET application to the newer version of the .NET Framework, the Web administrator can use the /noaspupgrade command-line option with the Dotnetfx.exe setup program.</span></span>

<span data-ttu-id="db6bb-129">**ASP.NET 응용 프로그램의 전체 다시 매핑을 최신 버전으로 방지 하려면**</span><span class="sxs-lookup"><span data-stu-id="db6bb-129">**To prevent total remapping of ASP.NET application to newer version**</span></span>

1. <span data-ttu-id="db6bb-130">**시작**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-130">Go to **Start**.</span></span>
2. <span data-ttu-id="db6bb-131">**실행**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-131">Click on **run**.</span></span>
3. <span data-ttu-id="db6bb-132">**cmd**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-132">Type **cmd**.</span></span>
4. <span data-ttu-id="db6bb-133">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-133">Click **OK**.</span></span>  
  
    ![](side-by-side-with-10/_static/image1.gif)
5. <span data-ttu-id="db6bb-134">명령 프롬프트에서 다음 줄을 입력 하 여 .NET Framework 설치를 시작 합니다. **dotnetfx.exe/c: "install/noaspupgrade?**</span><span class="sxs-lookup"><span data-stu-id="db6bb-134">From the command prompt, type the following line to start the installation of the .NET Framework: **Dotnetfx.exe /c:"install /noaspupgrade?**.</span></span>  
  
    ![](side-by-side-with-10/_static/image2.gif)
6. <span data-ttu-id="db6bb-135">Microsoft .NET Framework 1.1 설치에서 **예** 를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-135">Click **Yes** in the Microsoft .NET Framework 1.1 Setup.</span></span> <span data-ttu-id="db6bb-136">그러면 .NET Framework 1.1의 설치 프로세스가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-136">This will start the setup process of the .NET Framework 1.1.</span></span>  
  
    ![](side-by-side-with-10/_static/image3.gif)

<a id="2"></a>

## <a name="map-a-web-application-to-a-specific-version-of-the-net-framework"></a><span data-ttu-id="db6bb-137">웹 응용 프로그램을 특정 버전의 .NET Framework에 매핑</span><span class="sxs-lookup"><span data-stu-id="db6bb-137">Map a Web application to a specific version of the .NET Framework</span></span>

<span data-ttu-id="db6bb-138">각 버전의 .NET Framework에는 ASP.NET IIS 등록 도구 (Aspnet\_regiis) 버전이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-138">Each version of the .NET Framework includes a version of the ASP.NET IIS Registration Tool (Aspnet\_regiis.exe).</span></span> <span data-ttu-id="db6bb-139">이 도구를 사용 하면 관리자가 특정 버전의 .NET Framework에서 웹 응용 프로그램을 실행 하도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-139">This tool enables administrators to specify that a Web application be run under a particular version of the .NET Framework.</span></span> <span data-ttu-id="db6bb-140">이를 .NET Framework 버전의 웹 응용 프로그램에 매핑 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-140">This is referred to as mapping a Web application to a version of the .NET Framework.</span></span> <span data-ttu-id="db6bb-141">관리자는 웹 응용 프로그램과 연결 될 .NET Framework 버전에 해당 하는 Aspnet\_regiis .exe를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-141">Administrators must select the Aspnet\_regiis.exe that corresponds to the version of the .NET Framework that will be associated with the Web application.</span></span> <span data-ttu-id="db6bb-142">예를 들어 웹 사이트에서 .NET Framework 1.1를 사용 하도록 지정 하려는 관리자는 .NET Framework 1.1과 함께 제공 되는 Aspnet\_를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-142">For example, an administrator who wants to specify that a Web site use .NET Framework 1.1 must use the Aspnet\_regiis.exe that comes with .NET Framework 1.1.</span></span>

<span data-ttu-id="db6bb-143">버전 1.0에 대 한 Aspnet\_regiis .exe는 다음 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-143">The Aspnet\_regiis.exe for version 1.0 is located at:</span></span>

- <span data-ttu-id="db6bb-144">C:\windows\ microsoft.net \framework\\**v v1.0.3705**\aspnet\_regiis</span><span class="sxs-lookup"><span data-stu-id="db6bb-144">C:\WINDOWS\Microsoft.NET\Framework\\**v1.0.3705**\aspnet\_regiis</span></span>

<span data-ttu-id="db6bb-145">버전 1, 1에 대 한 Aspnet\_은 다음 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-145">The Aspnet\_regiis.exe for version 1,1 is located at:</span></span>

- <span data-ttu-id="db6bb-146">C:\windows\ microsoft.net \framework\\**v 1.1.4322**\aspnet\_regiis</span><span class="sxs-lookup"><span data-stu-id="db6bb-146">C:\WINDOWS\Microsoft.NET\Framework\\**v1.1.4322**\aspnet\_regiis</span></span>

<span data-ttu-id="db6bb-147">Aspnet\_regiis는 웹 응용 프로그램을 매핑하는 스크립트에 대 한 두 가지 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-147">The Aspnet\_regiis.exe provides two options for script mapping a Web application:</span></span>

- <span data-ttu-id="db6bb-148">**-** 는 경로 및 해당 하위 디렉터리에 스크립트 맵을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-148">**-s** sets the script map in the path and in its child directories.</span></span>
- <span data-ttu-id="db6bb-149">**-sn** 경로에 스크립트 맵을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-149">**-sn** sets the script map in the path only.</span></span>

<span data-ttu-id="db6bb-150">경로는 W3SVC/ROOT/{WebSiteNumber}/{Application\_Name} 형식으로 정의 되는 웹 응용 프로그램 IIS 메타 데이터 경로를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-150">The path defines the Web application IIS metadata path, which is defined in the form of W3SVC/ROOT/{WebSiteNumber}/{Application\_Name}.</span></span> <span data-ttu-id="db6bb-151">예를 들어 기본 웹 사이트 아래에 있는 Portal 이라는 웹 응용 프로그램의 경우 메타 베이스 경로는 W3SVC/1/ROOT/Portal입니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-151">For example, for a Web application called Portal located under the default Web site, the metabase path is W3SVC/1/ROOT/Portal.</span></span>

![](side-by-side-with-10/_static/image4.gif)

<span data-ttu-id="db6bb-152">메타 베이스 편집기 라는 도구를 사용 하 여 메타 베이스 경로를 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-152">Note You can also use a tool called the Metabase Editor to get the metabase path.</span></span> <span data-ttu-id="db6bb-153">이 도구는 [https://support.microsoft.com/default.aspx?scid=kb; en-us; 232068](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068) 의 Microsoft 지원 사이트에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-153">You can download this tool from the Microsoft Support site at [https://support.microsoft.com/default.aspx?scid=kb;en-us;232068.](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068)</span></span>

- <span data-ttu-id="db6bb-154">Aspnet\_regiis .exe/1/ROOT/Portal을 실행 하 여 포털 IIS 스크립트 맵과 해당 하위 응용 프로그램을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-154">Run Aspnet\_regiis.exe -s W3SVC/1/ROOT/Portal to update the portal IIS script map and its subapplication.</span></span>  
  
    ![](side-by-side-with-10/_static/image5.gif)

- <span data-ttu-id="db6bb-155">포털의 하위 디렉터리에 있는 응용 프로그램에 영향을 주지 않고 포털 IIS 스크립트 맵을 업데이트 하려면 Aspnet-sn W3SVC/1/ROOT/Portal\_를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-155">Run Aspnet\_regiis.exe -sn W3SVC/1/ROOT/Portal to update the portal IIS script map, without affecting applications in the portal?s subdirectories.</span></span>  
  
    ![](side-by-side-with-10/_static/image6.gif)

<a id="3"></a>

## <a name="find-the-net-framework-version-that-a-web-application-is-using"></a><span data-ttu-id="db6bb-156">웹 응용 프로그램에서 사용 하는 .NET Framework 버전 찾기</span><span class="sxs-lookup"><span data-stu-id="db6bb-156">Find the .NET Framework version that a Web application is using</span></span>

<span data-ttu-id="db6bb-157">관리자는 Internet Service Manager를 사용 하 여 웹 사이트를 실행 하는 .NET Framework 버전을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-157">An administrator can use the Internet Service Manager to find which version of the .NET Framework runs a Web site.</span></span> <span data-ttu-id="db6bb-158">서로 다른 운영 체제 버전은 인터넷 Service Manager를 다르게 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-158">Different operating system versions launch the Internet Service Manager differently.</span></span> <span data-ttu-id="db6bb-159">Service manager를 시작 하려면 아래 나열 된 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="db6bb-159">To start the service manager, follow the steps listed below.</span></span>

<span data-ttu-id="db6bb-160">**인터넷 Service Manager를 시작 하려면**</span><span class="sxs-lookup"><span data-stu-id="db6bb-160">**To start Internet Service Manager**</span></span>

1. <span data-ttu-id="db6bb-161">**시작**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-161">Go to **Start**.</span></span>
2. <span data-ttu-id="db6bb-162">**실행**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-162">Click on **run**.</span></span>
3. <span data-ttu-id="db6bb-163">**Inetmgr**을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-163">Type **inetmgr**.</span></span>  
  
    ![](side-by-side-with-10/_static/image7.gif)
4. <span data-ttu-id="db6bb-164">인터넷 Service Manager에서 보려는 .NET Framework의 버전을 포함 하는 웹 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-164">From the Internet Service Manager, select the Web application whose version of the .NET Framework you want to know.</span></span>  
  
    ![](side-by-side-with-10/_static/image8.gif)
5. <span data-ttu-id="db6bb-165">웹 응용 프로그램을 마우스 오른쪽 단추로 클릭 하 고 속성을 클릭 **합니다.**</span><span class="sxs-lookup"><span data-stu-id="db6bb-165">Right-click on the Web application, and click on **Properties.**</span></span>  
  
    ![](side-by-side-with-10/_static/image9.gif)
6. <span data-ttu-id="db6bb-166">속성 창에서 구성을 선택 **합니다.**</span><span class="sxs-lookup"><span data-stu-id="db6bb-166">From the Property window, select **Configuration.**</span></span>  
  
    ![](side-by-side-with-10/_static/image10.gif)
7. <span data-ttu-id="db6bb-167">응용 프로그램 매핑 테이블에서 **.aspx**를 선택 하 고 **편집**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-167">From the application mapping table, select **.aspx**, and click **Edit**.</span></span>  
  
    ![](side-by-side-with-10/_static/image11.gif)
8. <span data-ttu-id="db6bb-168">**실행 파일** 텍스트 상자에서 스크롤하여 버전 디렉터리를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-168">From the **Executable** text box, look at the version directory by scrolling.</span></span> <span data-ttu-id="db6bb-169">버전 디렉터리가 1.1.4322 인 경우 응용 프로그램은 .NET Framework 1.1에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-169">If the version directory is v.1.1.4322, the application is mapped to .NET Framework 1.1.</span></span> <span data-ttu-id="db6bb-170">반대로 버전 디렉터리가 v v1.0.3705 인 경우 응용 프로그램은 .NET Framework 1.0에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="db6bb-170">Conversely, if the version directory is v1.0.3705, the application is mapped to .NET Framework 1.0.</span></span>  
  
    ![](side-by-side-with-10/_static/image12.gif)
