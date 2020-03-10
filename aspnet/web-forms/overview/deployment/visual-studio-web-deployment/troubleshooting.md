---
uid: web-forms/overview/deployment/visual-studio-web-deployment/troubleshooting
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 문제 해결 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 ASP.NET 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자 (usin ...)에 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 06/01/2015
ms.assetid: c0090595-ab3b-4b9b-9e16-7a1891e8cb2f
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: b42476fca18b04f4557a216ee205cfd9220023e8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78465095"
---
# <a name="aspnet-web-deployment-using-visual-studio-troubleshooting"></a><span data-ttu-id="b44eb-103">Visual Studio를 사용 하 여 ASP.NET 웹 배포: 문제 해결</span><span class="sxs-lookup"><span data-stu-id="b44eb-103">ASP.NET Web Deployment using Visual Studio: Troubleshooting</span></span>

<span data-ttu-id="b44eb-104">만든 사람 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="b44eb-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="b44eb-105">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="b44eb-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="b44eb-106">이 자습서 시리즈에서는 Visual Studio 2012 또는 Visual Studio 2010를 사용 하 여 Azure App Service Web Apps 또는 타사 호스팅 공급자에 게 ASP.NET 웹 응용 프로그램을 배포 (게시) 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="b44eb-107">계열에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b44eb-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

<span data-ttu-id="b44eb-108">이 페이지에서는 Visual Studio를 사용 하 여 ASP.NET 웹 응용 프로그램을 배포할 때 발생할 수 있는 몇 가지 일반적인 문제에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-108">This page describes some common problems that may arise when you deploy an ASP.NET web application by using Visual Studio.</span></span> <span data-ttu-id="b44eb-109">각각에 대해 하나 이상의 가능한 원인과 해당 솔루션이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-109">For each one, one or more possible causes and corresponding solutions are provided.</span></span>

<span data-ttu-id="b44eb-110">표시 되는 시나리오는 Azure 및 타사 호스팅 공급자에 모두 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-110">The scenarios shown apply to both Azure and third-party hosting providers.</span></span> <span data-ttu-id="b44eb-111">Azure App Service에서 웹앱 문제 해결에 대한 자세한 내용은 다음 리소스를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="b44eb-111">For more information about troubleshooting web apps in Azure App Service, see the following resources:</span></span>

- [<span data-ttu-id="b44eb-112">Visual Studio를 사용하여 Azure App Service의 웹앱 문제 해결</span><span class="sxs-lookup"><span data-stu-id="b44eb-112">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)
- [<span data-ttu-id="b44eb-113">Azure App Service에서 Web Apps 모니터링</span><span class="sxs-lookup"><span data-stu-id="b44eb-113">Monitor Web Apps in Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-monitor//)
- <span data-ttu-id="b44eb-114">[.Net 용 Windows AZURE SDK 2.0 릴리스 발표](http://https://weblogs.asp.net/scottgu/announcing-the-release-of-windows-azure-sdk-2-0-for-net) (ScottGu의 블로그) Visual Studio에서 진단 로그를 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-114">[Announcing the release of Windows Azure SDK 2.0 for .NET](http://https://weblogs.asp.net/scottgu/announcing-the-release-of-windows-azure-sdk-2-0-for-net) (ScottGu's blog, shows how to get diagnostic logs in Visual Studio)</span></span>

## <a name="server-error-in--application---current-custom-error-settings-prevent-details-of-the-error-from-being-viewed-remotely"></a><span data-ttu-id="b44eb-115">'/' 응용 프로그램에 서버 오류가 있습니다.-현재 사용자 지정 오류 설정으로 인해 오류에 대 한 세부 정보가 원격으로 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-115">Server Error in '/' Application - Current Custom Error Settings Prevent Details of the Error from Being Viewed Remotely</span></span>

### <a name="scenario"></a><span data-ttu-id="b44eb-116">시나리오</span><span class="sxs-lookup"><span data-stu-id="b44eb-116">Scenario</span></span>

<span data-ttu-id="b44eb-117">원격 호스트에 사이트를 배포한 후 web.config 파일의 customErrors 설정이 표시 되는 오류 메시지가 표시 되지만 오류의 실제 원인을 나타내는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-117">After deploying a site to a remote host, you get an error message that mentions the customErrors setting in the Web.config file but doesn't indicate what the actual cause of the error was:</span></span>

[!code-xml[Main](troubleshooting/samples/sample1.xml)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b44eb-118">가능한 원인 및 해결 방법</span><span class="sxs-lookup"><span data-stu-id="b44eb-118">Possible Cause and Solution</span></span>

<span data-ttu-id="b44eb-119">기본적으로 ASP.NET는 웹 응용 프로그램이 로컬 컴퓨터에서 실행 중인 경우에만 자세한 오류 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-119">By default, ASP.NET shows detailed error information only when your web application is running on the local computer.</span></span> <span data-ttu-id="b44eb-120">일반적으로 해커는이 정보를 사용 하 여 응용 프로그램의 취약성을 찾을 수 있기 때문에 웹 응용 프로그램을 인터넷을 통해 공개적으로 사용할 수 있는 경우 자세한 오류 정보를 표시 하지 않으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-120">Generally you don't want to display detailed error information when your web application is publicly available over the Internet, because hackers may be able to use this information to find vulnerabilities in the application.</span></span> <span data-ttu-id="b44eb-121">그러나 사이트 또는 업데이트를 사이트에 배포 하는 경우 어떤 경우에도 오류가 발생 하 여 실제 오류 메시지를 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-121">However, when you are deploying a site or updates to a site, sometimes something will go wrong and you need to get the actual error message.</span></span>

<span data-ttu-id="b44eb-122">응용 프로그램이 원격 호스트에서 실행 될 때 자세한 오류 메시지를 표시 하도록 하려면 Web.config 파일을 편집 하 여 customErrors 모드 off를 설정 하 고, 응용 프로그램을 다시 배포 하 고, 응용 프로그램을 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-122">To enable the application to display detailed error messages when it runs on the remote host, edit the Web.config file to set customErrors mode off, redeploy the application, and run the application again:</span></span>

1. <span data-ttu-id="b44eb-123">응용 프로그램 Web.config 파일의 system.web 요소에 customErrors 요소가 있으면 mode 특성을 "off"로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-123">If the application Web.config file has a customErrors element in the system.web element, change the mode attribute to "off".</span></span> <span data-ttu-id="b44eb-124">그렇지 않은 경우 다음 예제와 같이 mode 특성을 "off"로 설정 하 여 system.web 요소에 customErrors 요소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-124">Otherwise add a customErrors element in the system.web element with the mode attribute set to "off", as shown in the following example:</span></span> 

    [!code-xml[Main](troubleshooting/samples/sample2.xml)]
2. <span data-ttu-id="b44eb-125">애플리케이션을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-125">Deploy the application.</span></span>
3. <span data-ttu-id="b44eb-126">응용 프로그램을 실행 하 고 이전에 발생 한 오류를 발생 시킨 모든 항목을 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-126">Run the application and repeat whatever you did earlier that caused the error to occur.</span></span> <span data-ttu-id="b44eb-127">이제 실제 오류 메시지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-127">Now you can see what the actual error message is.</span></span>
4. <span data-ttu-id="b44eb-128">오류가 해결 되 면 원래 customErrors 설정을 복원 하 고 응용 프로그램을 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-128">When you have resolved the error, restore the original customErrors setting and redeploy the application.</span></span>

## <a name="cannot-createshadow-copy-contosouniversity-when-that-file-already-exists"></a><span data-ttu-id="b44eb-129">해당 파일이 이미 있는 경우 ' ContosoUniversity '를 만들거나 섀도 복사할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-129">Cannot create/shadow copy 'ContosoUniversity' when that file already exists.</span></span>

### <a name="scenario"></a><span data-ttu-id="b44eb-130">시나리오</span><span class="sxs-lookup"><span data-stu-id="b44eb-130">Scenario</span></span>

<span data-ttu-id="b44eb-131">Visual Studio에서 프로젝트를 실행 하려고 하면 다음 예제와 같은 메시지가 포함 된 오류 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-131">When you try to run a project in Visual Studio you get an error page with a message like the following example:</span></span>

<span data-ttu-id="b44eb-132">'/' 애플리케이션의 서버 오류.</span><span class="sxs-lookup"><span data-stu-id="b44eb-132">Server Error in '/' Application.</span></span> <span data-ttu-id="b44eb-133">해당 파일이 이미 있는 경우 ' ContosoUniversity '를 만들거나 섀도 복사할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-133">Cannot create/shadow copy 'ContosoUniversity' when that file already exists.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b44eb-134">가능한 원인 및 해결 방법</span><span class="sxs-lookup"><span data-stu-id="b44eb-134">Possible Cause and Solution</span></span>

<span data-ttu-id="b44eb-135">잠시 기다렸다가 브라우저를 새로 고치거 나 사이트를 다시 컴파일한 후 다시 실행 해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="b44eb-135">Wait a minute and refresh the browser, or recompile the site and try running it again.</span></span>

## <a name="access-is-denied-in-a-web-page-that-uses-sql-server-compact"></a><span data-ttu-id="b44eb-136">SQL Server Compact를 사용 하는 웹 페이지에서 액세스가 거부 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-136">Access is Denied in a Web Page that Uses SQL Server Compact</span></span>

### <a name="scenario"></a><span data-ttu-id="b44eb-137">시나리오</span><span class="sxs-lookup"><span data-stu-id="b44eb-137">Scenario</span></span>

<span data-ttu-id="b44eb-138">SQL Server Compact를 사용 하는 사이트를 배포 하 고 데이터베이스에 액세스 하는 배포 된 사이트에서 페이지를 실행 하는 경우 다음 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-138">When you deploy a site that uses SQL Server Compact and you run a page in the deployed site that accesses the database, you see the following error message:</span></span>

<span data-ttu-id="b44eb-139">액세스가 거부되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-139">Access is denied.</span></span> <span data-ttu-id="b44eb-140">(HRESULT의 예외: 0x80070005 (E\_ACCESSDENIED))</span><span class="sxs-lookup"><span data-stu-id="b44eb-140">(Exception from HRESULT: 0x80070005 (E\_ACCESSDENIED))</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b44eb-141">가능한 원인 및 해결 방법</span><span class="sxs-lookup"><span data-stu-id="b44eb-141">Possible Cause and Solution</span></span>

<span data-ttu-id="b44eb-142">서버의 네트워크 서비스 계정에서 *bin\amd64* 또는 *bin\x86* 폴더에 있는 SQL SERVICE Compact 네이티브 이진 파일을 읽을 수 있어야 하지만 해당 폴더에 대 한 읽기 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-142">The NETWORK SERVICE account on the server needs to be able to read SQL Service Compact native binaries that are in the *bin\amd64* or *bin\x86* folder, but it does not have read permissions for those folders.</span></span> <span data-ttu-id="b44eb-143">*Bin* 폴더에서 네트워크 서비스에 대 한 읽기 권한을 설정 하 고 하위 폴더에 대 한 사용 권한을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-143">Set read permission for NETWORK SERVICE on the *bin* folder, making sure to extend the permissions to subfolders.</span></span>

## <a name="cannot-read-configuration-file-due-to-insufficient-permissions"></a><span data-ttu-id="b44eb-144">권한 부족으로 인해 구성 파일을 읽을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-144">Cannot Read Configuration File Due to Insufficient Permissions</span></span>

### <a name="scenario"></a><span data-ttu-id="b44eb-145">시나리오</span><span class="sxs-lookup"><span data-stu-id="b44eb-145">Scenario</span></span>

<span data-ttu-id="b44eb-146">Visual Studio 게시 단추를 클릭 하 여 로컬 컴퓨터의 IIS에 응용 프로그램을 배포 하면 게시가 실패 하 고 **출력** 창에 다음과 유사한 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-146">When you click the Visual Studio publish button to deploy an application to IIS on your local machine, publishing fails and the **Output** window shows an error message similar to this:</span></span>

<span data-ttu-id="b44eb-147">' MACHINE/리디렉션 ' IIS 구성 파일을 읽는 동안 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-147">An error occurred when reading the IIS Configuration File 'MACHINE/REDIRECTION'.</span></span> <span data-ttu-id="b44eb-148">이 작업을 수행 하는 id ... 오류: 권한이 충분 하지 않아 구성 파일을 읽을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-148">The identity performing this operation was ... Error: Cannot read configuration file due to insufficient permissions.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b44eb-149">가능한 원인 및 해결 방법</span><span class="sxs-lookup"><span data-stu-id="b44eb-149">Possible Cause and Solution</span></span>

<span data-ttu-id="b44eb-150">로컬 컴퓨터에서 한 번 클릭으로 IIS에 게시를 사용 하려면 관리자 권한으로 Visual Studio를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-150">To use one-click publish to IIS on your local machine, you must be running Visual Studio with administrator permissions.</span></span> <span data-ttu-id="b44eb-151">Visual Studio를 닫고 관리자 권한으로 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-151">Close Visual Studio and restart it with administrator permissions.</span></span>

## <a name="could-not-connect-to-the-destination-computer--using-the-specified-process"></a><span data-ttu-id="b44eb-152">대상 컴퓨터에 연결할 수 없습니다. 지정 된 프로세스 사용</span><span class="sxs-lookup"><span data-stu-id="b44eb-152">Could Not Connect to the Destination Computer ... Using the Specified Process</span></span>

### <a name="scenario"></a><span data-ttu-id="b44eb-153">시나리오</span><span class="sxs-lookup"><span data-stu-id="b44eb-153">Scenario</span></span>

<span data-ttu-id="b44eb-154">Visual Studio 게시 단추를 클릭 하 여 응용 프로그램을 배포 하면 게시가 실패 하 고 **출력** 창에 다음과 유사한 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-154">When you click the Visual Studio publish button to deploy an application, publishing fails and the **Output** window shows an error message similar to this:</span></span>

[!code-console[Main](troubleshooting/samples/sample3.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b44eb-155">가능한 원인 및 해결 방법</span><span class="sxs-lookup"><span data-stu-id="b44eb-155">Possible Cause and Solution</span></span>

<span data-ttu-id="b44eb-156">프록시 서버에서 대상 서버와의 통신을 중단 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-156">A proxy server is interrupting communication with the destination server.</span></span> <span data-ttu-id="b44eb-157">Windows 제어판 또는 Internet Explorer에서 **인터넷 옵션** 을 선택 하 고 **연결** 탭을 선택 합니다. **인터넷 속성** 대화 상자에서 **LAN 설정**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-157">From the Windows Control Panel or in Internet Explorer, select **Internet Options** and select the **Connections** tab. In the **Internet Properties** dialog box, click **LAN Settings**.</span></span> <span data-ttu-id="b44eb-158">**Lan (Local Area Network) 설정** 대화 상자에서 **자동으로 설정 검색** 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-158">In the **Local Area Network (LAN) Settings** dialog box, clear the **Automatically detect settings** checkbox.</span></span> <span data-ttu-id="b44eb-159">그런 다음 게시 단추를 다시 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-159">Then click the publish button again.</span></span>

<span data-ttu-id="b44eb-160">문제가 지속 되 면 시스템 관리자에 게 문의 하 여 프록시 또는 방화벽 설정으로 수행할 수 있는 작업을 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b44eb-160">If the problem persists, contact your system administrator to determine what can be done with proxy or firewall settings.</span></span> <span data-ttu-id="b44eb-161">웹 배포는 웹 관리 서비스 배포 (8172)에 비표준 포트를 사용 하기 때문에 문제가 발생 합니다. 다른 연결의 경우 웹 배포는 포트 80를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-161">The problem happens because Web Deploy uses a non-standard port for Web Management Service deployment (8172); for other connections, Web Deploy uses port 80.</span></span> <span data-ttu-id="b44eb-162">타사 호스팅 공급자에 배포 하는 경우 일반적으로 웹 관리 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-162">When you are deploying to a third-party hosting provider, you are typically using the Web Management Service.</span></span>

## <a name="default-net-40-application-pool-does-not-exist"></a><span data-ttu-id="b44eb-163">기본 .NET 4.0 응용 프로그램 풀이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-163">Default .NET 4.0 Application Pool Does Not Exist</span></span>

### <a name="scenario"></a><span data-ttu-id="b44eb-164">시나리오</span><span class="sxs-lookup"><span data-stu-id="b44eb-164">Scenario</span></span>

<span data-ttu-id="b44eb-165">.NET Framework 4가 필요한 응용 프로그램을 배포 하는 경우 다음 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-165">When you deploy an application that requires the .NET Framework 4, you see the following error message:</span></span>

<span data-ttu-id="b44eb-166">기본 .NET 4.0 응용 프로그램 풀이 없거나 응용 프로그램을 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-166">The default .NET 4.0 application pool does not exist or the application could not be added.</span></span> <span data-ttu-id="b44eb-167">ASP.NET 4.0이이 컴퓨터에 설치 되어 있는지 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="b44eb-167">Please verify that ASP.NET 4.0 is installed on this machine.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b44eb-168">가능한 원인 및 해결 방법</span><span class="sxs-lookup"><span data-stu-id="b44eb-168">Possible Cause and Solution</span></span>

<span data-ttu-id="b44eb-169">ASP.NET 4가 IIS에 설치 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-169">ASP.NET 4 is not installed in IIS.</span></span> <span data-ttu-id="b44eb-170">배포 하는 서버가 개발 컴퓨터 이며 Visual Studio 2010가 설치 되어 있는 경우에는 ASP.NET 4가 컴퓨터에 설치 되어 있지만 IIS에 설치 되어 있지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-170">If the server you are deploying to is your development computer and has Visual Studio 2010 installed on it, ASP.NET 4 is installed on the computer but might not be installed in IIS.</span></span> <span data-ttu-id="b44eb-171">배포 하는 서버에서 관리자 권한 명령 프롬프트를 열고 다음 명령을 실행 하 여 IIS에 ASP.NET 4를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-171">On the server that you are deploying to, open an elevated command prompt and install ASP.NET 4 in IIS by running the following commands:</span></span>

[!code-console[Main](troubleshooting/samples/sample4.cmd)]

<span data-ttu-id="b44eb-172">기본 응용 프로그램 풀의 .NET Framework 버전을 수동으로 설정 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-172">You might also need to manually set the .NET Framework version of the default application pool.</span></span> <span data-ttu-id="b44eb-173">자세한 내용은이 시리즈의 테스트 환경으로 IIS에 배포 자습서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b44eb-173">For more information, see the Deploying to IIS as a Test Environment tutorial in this series.</span></span>

## <a name="format-of-the-initialization-string-does-not-conform-to-specification-starting-at-index-0"></a><span data-ttu-id="b44eb-174">초기화 문자열의 형식이 인덱스 0부터 시작 하는 사양과 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-174">Format of the initialization string does not conform to specification starting at index 0.</span></span>

### <a name="scenario"></a><span data-ttu-id="b44eb-175">시나리오</span><span class="sxs-lookup"><span data-stu-id="b44eb-175">Scenario</span></span>

<span data-ttu-id="b44eb-176">한 번 클릭 게시를 사용 하 여 응용 프로그램을 배포한 후 데이터베이스에 액세스 하는 페이지를 실행 하면 다음과 같은 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-176">After you deploy an application using one-click publish, when you run a page that accesses the database you get the following error message:</span></span>

<span data-ttu-id="b44eb-177">초기화 문자열의 형식이 인덱스 0부터 시작 하는 사양과 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-177">Format of the initialization string does not conform to specification starting at index 0.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b44eb-178">가능한 원인 및 해결 방법</span><span class="sxs-lookup"><span data-stu-id="b44eb-178">Possible Cause and Solution</span></span>

<span data-ttu-id="b44eb-179">배포 된 사이트에서 web.config 파일을 열고 다음 예제와 같이 연결 문자열 값이 `$(ReplaceableToken_`로 시작 하는지 *확인 합니다.*</span><span class="sxs-lookup"><span data-stu-id="b44eb-179">Open the *Web.config* file in the deployed site and check to see whether the connection string values begin with `$(ReplaceableToken_`, as in the following example:</span></span>

[!code-xml[Main](troubleshooting/samples/sample5.xml)]

<span data-ttu-id="b44eb-180">연결 문자열이이 예제 처럼 보이는 경우 프로젝트 파일을 편집 하 고 모든 빌드 구성에 대 한 PropertyGroup 요소에 다음 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-180">If the connection strings look like this example, edit the project file and add the following property to the PropertyGroup element that is for all build configurations:</span></span>

[!code-xml[Main](troubleshooting/samples/sample6.xml)]

<span data-ttu-id="b44eb-181">그런 다음 응용 프로그램을 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-181">Then redeploy the application.</span></span>

## <a name="http-500-internal-server-error"></a><span data-ttu-id="b44eb-182">HTTP 500 내부 서버 오류</span><span class="sxs-lookup"><span data-stu-id="b44eb-182">HTTP 500 Internal Server Error</span></span>

### <a name="scenario"></a><span data-ttu-id="b44eb-183">시나리오</span><span class="sxs-lookup"><span data-stu-id="b44eb-183">Scenario</span></span>

<span data-ttu-id="b44eb-184">배포 된 사이트를 실행 하는 경우 오류의 원인을 나타내는 특정 정보가 없는 다음 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-184">When you run the deployed site, you see the following error message without specific information indicating the cause of the error:</span></span>

<span data-ttu-id="b44eb-185">HTTP 오류 500-내부 서버 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-185">HTTP Error 500 - Internal Server Error.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b44eb-186">가능한 원인 및 해결 방법</span><span class="sxs-lookup"><span data-stu-id="b44eb-186">Possible Cause and Solution</span></span>

<span data-ttu-id="b44eb-187">500 오류가 원인에는 여러 가지가 있지만, 이러한 자습서를 수행 하는 경우 Web.config 변환 파일 중 하나에서 XML 요소를 잘못 된 위치에 배치 하는 것이 가능한 원인 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-187">There are many causes of 500 errors, but one possible cause if you are following these tutorials is that you put an XML element in the wrong place in one of the Web.config transformation files.</span></span> <span data-ttu-id="b44eb-188">예를 들어 &lt;구성&gt;바로 아래에 있는 대신 &lt;system.web&gt;에서 &lt;위치&gt; 요소를 삽입 하는 변환을 배치 하면이 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-188">For example, you would get this error if you put the transformation that inserts a &lt;location&gt; element under &lt;system.web&gt; instead of directly under &lt;configuration&gt;.</span></span> <span data-ttu-id="b44eb-189">Web.config 변환 미리 보기 기능을 사용 하 여 변환이 의도 한 대로 작동 하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-189">You can use the Web.config transform preview feature to verify that transformations are working as intended.</span></span> <span data-ttu-id="b44eb-190">잘못 코딩 된 변환을 찾은 경우이 솔루션은 변환 파일을 수정 하 고 다시 배포 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-190">The solution if you find a transform that was coded incorrectly is to correct the transformation file and redeploy.</span></span> <span data-ttu-id="b44eb-191">오류가 명확 하지 않은 경우에는 변환을 주석으로 처리 하 고 다시 배포 하 여 500 오류가 발생 한 원인을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-191">If an error isn't obvious, try commenting out transforms and redeploying to see which one is causing the 500 error.</span></span>

## <a name="http-50021-internal-server-error"></a><span data-ttu-id="b44eb-192">HTTP 500.21 내부 서버 오류</span><span class="sxs-lookup"><span data-stu-id="b44eb-192">HTTP 500.21 Internal Server Error</span></span>

### <a name="scenario"></a><span data-ttu-id="b44eb-193">시나리오</span><span class="sxs-lookup"><span data-stu-id="b44eb-193">Scenario</span></span>

<span data-ttu-id="b44eb-194">배포 된 사이트를 실행 하는 경우 다음 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-194">When you run the deployed site, you see the following error message:</span></span>

<span data-ttu-id="b44eb-195">HTTP 오류 500.21-내부 서버 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-195">HTTP Error 500.21 - Internal Server Error.</span></span> <span data-ttu-id="b44eb-196">"PageHandlerFactory 통합" 처리기의 모듈 목록에 잘못 된 "ManagedPipelineHandler" 모듈이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-196">Handler "PageHandlerFactory-Integrated" has a bad module "ManagedPipelineHandler" in its module list.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b44eb-197">가능한 원인 및 해결 방법</span><span class="sxs-lookup"><span data-stu-id="b44eb-197">Possible Cause and Solution</span></span>

<span data-ttu-id="b44eb-198">배포한 사이트는 ASP.NET 4 이지만 ASP.NET 4는 서버의 IIS에 등록 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-198">The site you have deployed targets ASP.NET 4, but ASP.NET 4 is not registered in IIS on the server.</span></span> <span data-ttu-id="b44eb-199">서버에서 관리자 권한 명령 프롬프트를 열고 다음 명령을 실행 하 여 ASP.NET 4를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-199">On the server open an elevated command prompt and register ASP.NET 4 by running the following commands:</span></span>

[!code-console[Main](troubleshooting/samples/sample7.cmd)]

<span data-ttu-id="b44eb-200">기본 응용 프로그램 풀의 .NET Framework 버전을 수동으로 설정 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-200">You might also need to manually set the .NET Framework version of the default application pool.</span></span> <span data-ttu-id="b44eb-201">자세한 내용은이 시리즈의 테스트 환경으로 IIS에 배포 자습서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b44eb-201">For more information, see the Deploying to IIS as a Test Environment tutorial in this series.</span></span>

## <a name="login-failed-opening-sql-server-express-database-in-app_data"></a><span data-ttu-id="b44eb-202">앱\_데이터에서 SQL Server Express 데이터베이스를 여는 데 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-202">Login Failed Opening SQL Server Express Database in App\_Data</span></span>

### <a name="scenario"></a><span data-ttu-id="b44eb-203">시나리오</span><span class="sxs-lookup"><span data-stu-id="b44eb-203">Scenario</span></span>

<span data-ttu-id="b44eb-204">응용 프로그램 *\_Data* 폴더의 .mdf 파일로 SQL Server Express 데이터베이스를 가리키도록 *web.config* 파일 연결 문자열을 업데이트 하 고 응용 프로그램을 처음 실행할 때 다음과 같은 오류 메시지가 표시 *됩니다* .</span><span class="sxs-lookup"><span data-stu-id="b44eb-204">You updated the *Web.config* file connection string to point to a SQL Server Express database as an *.mdf* file in your *App\_Data* folder, and the first time you run the application you see the following error message:</span></span>

<span data-ttu-id="b44eb-205">SqlException: 로그인에서 요청한 "DatabaseName" 데이터베이스를 열 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-205">System.Data.SqlClient.SqlException: Cannot open database "DatabaseName" requested by the login.</span></span> <span data-ttu-id="b44eb-206">로그인이 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-206">The login failed.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b44eb-207">가능한 원인 및 해결 방법</span><span class="sxs-lookup"><span data-stu-id="b44eb-207">Possible Cause and Solution</span></span>

<span data-ttu-id="b44eb-208">이전에 기존 데이터베이스의 *.mdf* 파일을 삭제 한 경우에도 *.mdf* 파일의 이름은 컴퓨터에 있었던 SQL Server Express 데이터베이스의 이름과 일치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-208">The name of the *.mdf* file cannot match the name of any SQL Server Express database that has ever existed on your computer, even if you deleted the *.mdf* file of the previously existing database.</span></span> <span data-ttu-id="b44eb-209">*.Mdf* 파일의 이름을 데이터베이스 이름으로 사용 된 적이 없는 이름으로 변경 하 고 *web.config* 파일을 변경 하 여 새 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-209">Change the name of the *.mdf* file to a name that has never been used as a database name and change the *Web.config* file to use the new name.</span></span> <span data-ttu-id="b44eb-210">또는 [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) 를 사용 하 여 이전에 기존 SQL Server Express 데이터베이스를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-210">As an alternative, you can use [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) to delete previously existing SQL Server Express databases.</span></span>

## <a name="model-compatibility-cannot-be-checked"></a><span data-ttu-id="b44eb-211">모델 호환성을 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-211">Model Compatibility Cannot be Checked</span></span>

### <a name="scenario"></a><span data-ttu-id="b44eb-212">시나리오</span><span class="sxs-lookup"><span data-stu-id="b44eb-212">Scenario</span></span>

<span data-ttu-id="b44eb-213">새 SQL Server Express 데이터베이스를 가리키도록 *web.config* 파일 연결 문자열을 업데이트 하 고 응용 프로그램을 처음 실행할 때 다음과 같은 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-213">You updated the *Web.config* file connection string to point to a new SQL Server Express database, and the first time you run the application you see the following error message:</span></span>

<span data-ttu-id="b44eb-214">데이터베이스에 모델 메타 데이터가 포함 되어 있지 않으므로 모델 호환성을 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-214">Model compatibility cannot be checked because the database does not contain model metadata.</span></span> <span data-ttu-id="b44eb-215">DbModelBuilder 규칙에 IncludeMetadataConvention이 추가 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-215">Ensure that IncludeMetadataConvention has been added to the DbModelBuilder conventions.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b44eb-216">가능한 원인 및 해결 방법</span><span class="sxs-lookup"><span data-stu-id="b44eb-216">Possible Cause and Solution</span></span>

<span data-ttu-id="b44eb-217">컴퓨터에서 web.config 파일에 저장 한 데이터베이스 이름이 이미 사용 된 경우 데이터베이스에 일부 테이블이 이미 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-217">If the database name you put in the Web.config file was ever used before on your computer, a database might already exist with some tables in it.</span></span> <span data-ttu-id="b44eb-218">이전에 컴퓨터에서 사용 되지 않은 새 이름을 선택 하 고이 새 데이터베이스 이름을 사용 하도록 *web.config 파일을 변경 합니다.*</span><span class="sxs-lookup"><span data-stu-id="b44eb-218">Select a new name that has not been used on your computer before and change the *Web.config* file to point to use this new database name.</span></span> <span data-ttu-id="b44eb-219">또는 [SQL Server Express 유틸리티](https://www.microsoft.com/download/details.aspx?DisplayLang=en&amp;id=3990) 또는 [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) 를 사용 하 여 기존 데이터베이스를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-219">As an alternative, you can use [SQL Server Express Utility](https://www.microsoft.com/download/details.aspx?DisplayLang=en&amp;id=3990) or [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) to delete the existing database.</span></span>

## <a name="sql-error-when-a-script-attempts-to-create-users-or-roles"></a><span data-ttu-id="b44eb-220">스크립트에서 사용자 또는 역할을 만들려고 할 때 SQL 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-220">SQL Error When a Script Attempts to Create Users or Roles</span></span>

### <a name="scenario"></a><span data-ttu-id="b44eb-221">시나리오</span><span class="sxs-lookup"><span data-stu-id="b44eb-221">Scenario</span></span>

<span data-ttu-id="b44eb-222">**Sql 패키지 및 게시** 탭에서 구성 된 데이터베이스 배포를 사용 하 고 있습니다. 배포 중에 실행 되는 sql 스크립트에는 사용자 만들기 또는 역할 만들기 명령이 포함 되며, 이러한 명령이 실행 되 면 스크립트 실행이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-222">You are using database deployment configured on the **Package/Publish SQL** tab, SQL scripts that run during deployment include Create User or Create Role commands, and script execution fails when those commands are executed.</span></span> <span data-ttu-id="b44eb-223">다음과 같이 보다 자세한 메시지가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-223">You might see more detailed messages, such as the following:</span></span>

[!code-console[Main](troubleshooting/samples/sample8.cmd)]

<span data-ttu-id="b44eb-224">**SQL 패키지 및 게시** 탭이 아니라 **웹 게시** 마법사에서 데이터베이스 배포를 구성 했을 때이 오류가 발생 하는 경우 [구성 및 배포](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment) 포럼에서 스레드를 만들면이 문제 해결 페이지에 솔루션이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-224">If this error occurs when you have configured database deployment in the **Publish Web** wizard rather than the **Package/Publish SQL** tab, create a thread in the [Configuration and Deployment](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment) forum, and the solution will be added to this troubleshooting page.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b44eb-225">가능한 원인 및 해결 방법</span><span class="sxs-lookup"><span data-stu-id="b44eb-225">Possible Cause and Solution</span></span>

<span data-ttu-id="b44eb-226">배포를 수행 하는 데 사용 하는 사용자 계정에 사용자 또는 역할을 만들 수 있는 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-226">The user account you are using to perform deployment does not have permission to create users or roles.</span></span> <span data-ttu-id="b44eb-227">예를 들어 호스팅 회사는 db\_datareader, db\_datawriter 여부 및 db\_ddladmin 역할을 사용자가 설정 하는 사용자 계정에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-227">For example, the hosting company might assign the db\_datareader, db\_datawriter, and db\_ddladmin roles to the user account that it sets up for you.</span></span> <span data-ttu-id="b44eb-228">이러한 데이터는 대부분의 데이터베이스 개체를 만드는 데 충분 하지만 사용자 또는 역할을 만드는 데에는 충분 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-228">These are sufficient for creating most database objects, but not for creating users or roles.</span></span> <span data-ttu-id="b44eb-229">이 오류를 방지 하는 한 가지 방법은 데이터베이스 배포에서 사용자와 역할을 제외 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-229">One way to avoid the error is by excluding users and roles from database deployment.</span></span> <span data-ttu-id="b44eb-230">이렇게 하려면 데이터베이스에서 자동으로 생성 된 스크립트에 대 한 다음 특성을 포함 하도록 자동으로 생성 된 스크립트에 대 한 보도 요소를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-230">You can do this by editing the PreSource element for the database's automatically generated script so that it includes the following attributes:</span></span>

[!code-console[Main](troubleshooting/samples/sample9.cmd)]

<span data-ttu-id="b44eb-231">프로젝트 파일에서 보도 Ource 요소를 편집 하는 방법에 대 한 자세한 내용은 [방법: 프로젝트 파일의 배포 설정 편집](https://msdn.microsoft.com/library/ff398069(v=vs.100).aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b44eb-231">For information about how to edit the PreSource element in the project file, see [How to: Edit Deployment Settings in the Project File](https://msdn.microsoft.com/library/ff398069(v=vs.100).aspx).</span></span> <span data-ttu-id="b44eb-232">개발 데이터베이스의 사용자 또는 역할이 대상 데이터베이스에 있어야 하는 경우 호스팅 공급자에 게 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b44eb-232">If the users or roles in your development database need to be in the destination database, contact your hosting provider for assistance.</span></span>

## <a name="sql-server-timeout-error-when-running-custom-scripts-during-deployment"></a><span data-ttu-id="b44eb-233">배포 하는 동안 사용자 지정 스크립트를 실행 하는 동안 SQL Server 시간 초과 오류 발생</span><span class="sxs-lookup"><span data-stu-id="b44eb-233">SQL Server Timeout Error When Running Custom Scripts During Deployment</span></span>

### <a name="scenario"></a><span data-ttu-id="b44eb-234">시나리오</span><span class="sxs-lookup"><span data-stu-id="b44eb-234">Scenario</span></span>

<span data-ttu-id="b44eb-235">배포 하는 동안 실행할 사용자 지정 SQL 스크립트를 지정 하 고 웹 배포 실행 하면 시간 초과 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-235">You have specified custom SQL scripts to run during deployment, and when Web Deploy runs them, they time out.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b44eb-236">가능한 원인 및 해결 방법</span><span class="sxs-lookup"><span data-stu-id="b44eb-236">Possible Cause and Solution</span></span>

<span data-ttu-id="b44eb-237">다른 트랜잭션 모드를 포함 하는 여러 스크립트를 실행 하면 시간 초과 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-237">Running multiple scripts that have different transaction modes can cause time-out errors.</span></span> <span data-ttu-id="b44eb-238">기본적으로 자동으로 생성 된 스크립트는 트랜잭션에서 실행 되지만 사용자 지정 스크립트는 그렇지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-238">By default, automatically generated scripts run in a transaction, but custom scripts do not.</span></span> <span data-ttu-id="b44eb-239">**Sql 패키지 및 게시** 탭에서 **기존 데이터베이스에서 데이터 및/또는 스키마 가져오기** 옵션을 선택 하 고 사용자 지정 sql 스크립트를 추가 하는 경우 모든 스크립트가 동일한 트랜잭션 설정을 사용 하도록 일부 스크립트의 트랜잭션 설정을 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-239">If you select the **Pull data and/or schema from an existing database** option on the **Package/Publish SQL** tab, and if you add a custom SQL script, you must change transaction settings on some scripts so that all scripts use the same transaction settings.</span></span> <span data-ttu-id="b44eb-240">자세한 내용은 [방법: 웹 응용 프로그램 프로젝트를 사용 하 여 데이터베이스 배포](https://msdn.microsoft.com/library/dd465343.aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b44eb-240">For more information, see [How to: Deploy a Database With a Web Application Project](https://msdn.microsoft.com/library/dd465343.aspx).</span></span>

<span data-ttu-id="b44eb-241">모든 것이 동일 하지만이 오류가 발생 하지 않도록 트랜잭션 설정을 구성한 경우 스크립트를 별도로 실행 하는 것이 가능한 해결 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-241">If you have configured transaction settings so that all are the same but still get this error, a possible workaround is to run the scripts separately.</span></span> <span data-ttu-id="b44eb-242">SQL **패키지 및 게시** 탭의 **데이터베이스 스크립트** 표에서 제한 시간 오류를 발생 시키는 스크립트에 대 한 **포함** 확인란의 선택을 취소 한 다음 프로젝트를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-242">In the **Database Scripts** grid in the **Package/Publish** SQL tab, clear the **Include** check box for the script that causes the timeout error, then publish the project.</span></span> <span data-ttu-id="b44eb-243">그런 다음 **데이터베이스 스크립트** 그리드로 돌아가서 해당 스크립트의 **포함** 확인란을 선택 하 고 다른 스크립트에 대 한 **포함** 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-243">Then go back into the **Database Scripts** grid, select that script's **Include** check box, and clear the **Include** check boxes for the other scripts.</span></span> <span data-ttu-id="b44eb-244">그런 다음 프로젝트를 다시 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-244">Then publish the project again.</span></span> <span data-ttu-id="b44eb-245">이번에는 게시할 때 선택한 사용자 지정 스크립트만 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-245">This time when you publish, only the selected custom script runs.</span></span>

## <a name="stream-data-of-site-manifest-is-not-yet-available"></a><span data-ttu-id="b44eb-246">사이트 매니페스트의 스트림 데이터를 아직 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-246">Stream Data of Site Manifest Is Not Yet Available</span></span>

### <a name="scenario"></a><span data-ttu-id="b44eb-247">시나리오</span><span class="sxs-lookup"><span data-stu-id="b44eb-247">Scenario</span></span>

<span data-ttu-id="b44eb-248">T (테스트) 옵션을 사용 하 여 *배포 .cmd* 파일을 사용 하 여 패키지를 설치 하는 경우 다음 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-248">When you are installing a package using the *deploy.cmd* file with the t (test) option, you see the following error message:</span></span>

<span data-ttu-id="b44eb-249">오류: ' sitemanifest/dbFullSql [@path= ' C:\TEMP\AdventureWorksGrant.sql ']/sqlScript '의 스트림 데이터를 아직 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-249">Error: The stream data of 'sitemanifest/dbFullSql[@path='C:\TEMP\AdventureWorksGrant.sql']/sqlScript' is not yet available.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b44eb-250">가능한 원인 및 해결 방법</span><span class="sxs-lookup"><span data-stu-id="b44eb-250">Possible Cause and Solution</span></span>

<span data-ttu-id="b44eb-251">오류 메시지는 명령이 테스트 보고서를 생성할 수 없음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-251">The error message means that the command cannot produce a test report.</span></span> <span data-ttu-id="b44eb-252">그러나 y (실제 설치) 옵션을 사용 하는 경우 명령이 실행 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-252">However, the command might run if you use the y (actual installation) option.</span></span> <span data-ttu-id="b44eb-253">이 메시지는 테스트 모드에서 명령을 실행 하는 데 문제가 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-253">The message indicates only that there is a problem with running the command in test mode.</span></span>

## <a name="this-application-requires-managedruntimeversion-v40"></a><span data-ttu-id="b44eb-254">이 응용 프로그램에는 ManagedRuntimeVersion v 4.0이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-254">This Application Requires ManagedRuntimeVersion v4.0</span></span>

### <a name="scenario"></a><span data-ttu-id="b44eb-255">시나리오</span><span class="sxs-lookup"><span data-stu-id="b44eb-255">Scenario</span></span>

<span data-ttu-id="b44eb-256">배포 하려고 하면 다음과 같은 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-256">When you attempt to deploy, you see the following error message:</span></span>

<span data-ttu-id="b44eb-257">사용 하려는 응용 프로그램 풀의 ' managedRuntimeVersion ' 속성이 ' v 2.0 '으로 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-257">The application pool that you are trying to use has the 'managedRuntimeVersion' property set to 'v2.0'.</span></span> <span data-ttu-id="b44eb-258">이 응용 프로그램에는 ' v 4.0 '이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-258">This application requires 'v4.0'.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b44eb-259">가능한 원인 및 해결 방법</span><span class="sxs-lookup"><span data-stu-id="b44eb-259">Possible Cause and Solution</span></span>

<span data-ttu-id="b44eb-260">ASP.NET 4가 IIS에 설치 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-260">ASP.NET 4 is not installed in IIS.</span></span> <span data-ttu-id="b44eb-261">배포 하는 서버가 개발 컴퓨터 이며 Visual Studio 2010가 설치 되어 있는 경우에는 ASP.NET 4가 컴퓨터에 설치 되어 있지만 IIS에 설치 되어 있지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-261">If the server you are deploying to is your development computer and has Visual Studio 2010 installed on it, ASP.NET 4 is installed on the computer but might not be installed in IIS.</span></span> <span data-ttu-id="b44eb-262">배포 하는 서버에서 관리자 권한 명령 프롬프트를 열고 다음 명령을 실행 하 여 IIS에 ASP.NET 4를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-262">On the server that you are deploying to, open an elevated command prompt and install ASP.NET 4 in IIS by running the following commands:</span></span>

[!code-console[Main](troubleshooting/samples/sample10.cmd)]

## <a name="unable-to-cast-microsoftwebdeploymentdeploymentprovideroptions"></a><span data-ttu-id="b44eb-263">Microsoft. Deployment. DeploymentProviderOptions를 캐스팅할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-263">Unable to cast Microsoft.Web.Deployment.DeploymentProviderOptions</span></span>

### <a name="scenario"></a><span data-ttu-id="b44eb-264">시나리오</span><span class="sxs-lookup"><span data-stu-id="b44eb-264">Scenario</span></span>

<span data-ttu-id="b44eb-265">패키지를 배포 하는 경우 다음 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-265">When you are deploying a package, you see the following error message:</span></span>

<span data-ttu-id="b44eb-266">' Microsoft. Deployment. DeploymentProviderOptions ' 형식의 개체를 ' Microsoft. Deployment. DeploymentProviderOptions '로 캐스팅할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-266">Unable to cast object of type 'Microsoft.Web.Deployment.DeploymentProviderOptions' to 'Microsoft.Web.Deployment.DeploymentProviderOptions'.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b44eb-267">가능한 원인 및 해결 방법</span><span class="sxs-lookup"><span data-stu-id="b44eb-267">Possible Cause and Solution</span></span>

<span data-ttu-id="b44eb-268">웹 배포 1.1 UI를 사용 하 여 IIS 관리자에서 웹 배포 2.0이 설치 된 서버에 배포 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-268">You are trying to deploy from IIS Manager using the Web Deploy 1.1 UI to a server that has Web Deploy 2.0 installed.</span></span> <span data-ttu-id="b44eb-269">패키지를 가져와서 IIS 원격 관리 도구를 사용 하 여 배포 하는 경우 연결을 설정할 때 **사용 가능한 새 기능** 대화 상자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-269">If you are using the IIS Remote Administration Tool to deploy by importing a package, check the **New Features Available** dialog box when you establish the connection.</span></span> <span data-ttu-id="b44eb-270">이 대화 상자는 연결이 처음 설정 될 때 한 번만 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-270">(This dialog box might only be shown once when the connection is first established.</span></span> <span data-ttu-id="b44eb-271">연결을 지우고 다시 시작 하려면 IIS 관리자를 닫고 명령 프롬프트에 inetmgr/reset를 입력 하 여 다시 시작 합니다. 나열 된 기능 중 하나가 **UI 웹 배포**이 고 8 보다 낮은 버전의 버전을 포함 하는 경우 배포 하는 서버에 1.1 및 2.0 버전의 웹 배포 설치 되어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-271">To clear the connection and start over, close IIS Manager and start it up again by entering inetmgr /reset at the command prompt.) If one of the features listed is **Web Deploy UI**, and it has a version number lower than 8, the server you are deploying to might have both 1.1 and 2.0 versions of Web Deploy installed.</span></span> <span data-ttu-id="b44eb-272">2\.0가 설치 된 클라이언트에서 배포 하려면 서버에 웹 배포 2.0만 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-272">To deploy from a client that has 2.0 installed, the server must have only Web Deploy 2.0 installed.</span></span> <span data-ttu-id="b44eb-273">이 문제를 해결 하려면 호스팅 공급자에 게 문의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-273">You will have to contact your hosting provider to resolve this problem.</span></span>

## <a name="unable-to-load-the-native-components-of-sql-server-compact"></a><span data-ttu-id="b44eb-274">SQL Server Compact의 네이티브 구성 요소를 로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-274">Unable to load the native components of SQL Server Compact</span></span>

### <a name="scenario"></a><span data-ttu-id="b44eb-275">시나리오</span><span class="sxs-lookup"><span data-stu-id="b44eb-275">Scenario</span></span>

<span data-ttu-id="b44eb-276">배포 된 사이트를 실행 하는 경우 다음 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-276">When you run the deployed site, you see the following error message:</span></span>

<span data-ttu-id="b44eb-277">ADO.NET 공급자 버전 8482에 해당 하는 SQL Server Compact의 네이티브 구성 요소를 로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-277">Unable to load the native components of SQL Server Compact corresponding to the ADO.NET provider of version 8482.</span></span> <span data-ttu-id="b44eb-278">올바른 버전의 SQL Server Compact를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-278">Install the correct version of SQL Server Compact.</span></span> <span data-ttu-id="b44eb-279">자세한 내용은 기술 자료 문서 974247을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b44eb-279">Refer to KB article 974247 for more details.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b44eb-280">가능한 원인 및 해결 방법</span><span class="sxs-lookup"><span data-stu-id="b44eb-280">Possible Cause and Solution</span></span>

<span data-ttu-id="b44eb-281">배포 된 사이트에는 응용 프로그램의 *bin* 폴더 아래에 네이티브 어셈블리가 있는 *amd64* 및 *x86* 하위 폴더가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-281">The deployed site does not have *amd64* and *x86* subfolders with the native assemblies in them under the application's *bin* folder.</span></span> <span data-ttu-id="b44eb-282">SQL Server Compact 설치 된 컴퓨터에서 네이티브 어셈블리는 *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private*에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-282">On a computer that has SQL Server Compact installed, the native assemblies are located in *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private*.</span></span> <span data-ttu-id="b44eb-283">Visual Studio 프로젝트에서 올바른 폴더에 올바른 파일을 가져오는 가장 좋은 방법은 NuGet SqlServerCompact 패키지를 설치 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-283">The best way to get the correct files into the correct folders in a Visual Studio project is to install the NuGet SqlServerCompact package.</span></span> <span data-ttu-id="b44eb-284">패키지 설치는 네이티브 어셈블리를 *amd64* 및 *x 86*으로 복사 하는 빌드 후 스크립트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-284">Package installation adds a post-build script to copy the native assemblies into *amd64* and *x86*.</span></span> <span data-ttu-id="b44eb-285">그러나 이러한 배포를 배포 하려면 프로젝트에 수동으로 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-285">In order for these to be deployed, however, you have to manually include them in the project.</span></span> <span data-ttu-id="b44eb-286">자세한 내용은 [SQL Server Compact 배포](../../older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) 자습서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b44eb-286">For more information, see the [Deploying SQL Server Compact](../../older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) tutorial.</span></span>

## <a name="path-is-not-valid-error-after-deploying-an-entity-framework-code-first-application"></a><span data-ttu-id="b44eb-287">Entity Framework Code First 응용 프로그램을 배포한 후 "경로가 잘못 되었습니다." 오류</span><span class="sxs-lookup"><span data-stu-id="b44eb-287">"Path is not valid" error after deploying an Entity Framework Code First application</span></span>

### <a name="scenario"></a><span data-ttu-id="b44eb-288">시나리오</span><span class="sxs-lookup"><span data-stu-id="b44eb-288">Scenario</span></span>

<span data-ttu-id="b44eb-289">Entity Framework Code First 마이그레이션를 사용 하는 응용 프로그램을 배포 하 고 SQL Server Compact와 같은 DBMS를 앱\_데이터 폴더의 파일에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-289">You deploy an application that uses Entity Framework Code First Migrations and a DBMS such as SQL Server Compact which stores its database in a file in the App\_Data folder.</span></span> <span data-ttu-id="b44eb-290">첫 번째 배포 후에 데이터베이스를 만들도록 Code First 마이그레이션 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-290">You have Code First Migrations configured to create the database after your first deployment.</span></span> <span data-ttu-id="b44eb-291">응용 프로그램을 실행 하면 다음 예제와 같은 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-291">When you run the application you get an error message like the following example:</span></span>

<span data-ttu-id="b44eb-292">경로가 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-292">The path is not valid.</span></span> <span data-ttu-id="b44eb-293">데이터베이스의 디렉터리를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-293">Check the directory for the database.</span></span> <span data-ttu-id="b44eb-294">[Path = c:\inetpub\wwwroot\App\_Data\DatabaseName.sdf]</span><span class="sxs-lookup"><span data-stu-id="b44eb-294">[Path = c:\inetpub\wwwroot\App\_Data\DatabaseName.sdf ]</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b44eb-295">가능한 원인 및 해결 방법</span><span class="sxs-lookup"><span data-stu-id="b44eb-295">Possible Cause and Solution</span></span>

<span data-ttu-id="b44eb-296">Code First에서 데이터베이스를 만들려고 하지만 응용 프로그램\_데이터 폴더가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-296">Code First is attempting to create the database but the App\_Data folder does not exist.</span></span> <span data-ttu-id="b44eb-297">배포할 때 *앱\_data* 폴더에 파일이 없거나, 프로젝트 속성 창의 **웹 패키지 및 게시** 탭에서 **앱\_데이터 제외** 를 선택 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-297">Either you didn't have any files in the *App\_Data* folder when you deployed, or you selected **Exclude App\_Data** on the **Package/Publish Web** tab of the Project Properties window.</span></span> <span data-ttu-id="b44eb-298">서버에 복사할 폴더에 파일이 없는 경우 배포 프로세스에서 서버에 폴더를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-298">The deployment process won't create a folder on the server if there are no files in the folder to be copied to the server.</span></span> <span data-ttu-id="b44eb-299">사이트에서 데이터베이스를 이미 설정한 경우에는 게시 프로필의 **대상에서 추가 파일 제거** 를 선택한 경우 배포 프로세스에서 파일 및 *앱\_데이터* 폴더 자체를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-299">If you already had the database set up in the site, the deployment process will delete the files and the *App\_Data* folder itself if you selected **Remove additional files at destination** in the publish profile.</span></span> <span data-ttu-id="b44eb-300">이 문제를 해결 하려면 *응용 프로그램\_data* 폴더에 .txt 파일과 같은 자리 표시자 파일을 배치 하 고, **앱 제외\_데이터** 를 선택 하 고 다시 배포 하지 않았는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-300">To solve the problem, put a placeholder file such as a .txt file in the *App\_Data* folder, make sure you do not have **Exclude App\_Data** selected, and redeploy.</span></span>

## <a name="com-object-that-has-been-separated-from-its-underlying-rcw-cannot-be-used"></a><span data-ttu-id="b44eb-301">"내부 RCW에서 분리 된 COM 개체를 사용할 수 없습니다."</span><span class="sxs-lookup"><span data-stu-id="b44eb-301">"COM object that has been separated from its underlying RCW cannot be used."</span></span>

### <a name="scenario"></a><span data-ttu-id="b44eb-302">시나리오</span><span class="sxs-lookup"><span data-stu-id="b44eb-302">Scenario</span></span>

<span data-ttu-id="b44eb-303">한 번의 클릭으로 게시를 사용 하 여 응용 프로그램을 배포한 후이 오류가 발생 하기 시작 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-303">You have been successfully using one-click publish to deploy your application and then you start getting this error:</span></span>

<span data-ttu-id="b44eb-304">웹 배포 작업이 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-304">Web deployment task failed.</span></span> <span data-ttu-id="b44eb-305">(원격 에이전트 URL '<https://serverurl.com/msdeploy.axd?site=sitename>'에 대 한 요청을 완료할 수 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="b44eb-305">(Could not complete the request to remote agent URL '<https://serverurl.com/msdeploy.axd?site=sitename>'.)</span></span>  
 <span data-ttu-id="b44eb-306">원격 에이전트 URL '<https://url/msdeploy.axd?site=sitename>'에 대 한 요청을 완료할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-306">Could not complete the request to remote agent URL '<https://url/msdeploy.axd?site=sitename>'.</span></span>  
<span data-ttu-id="b44eb-307">요청이 중단 되었습니다. 요청이 취소 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-307">The request was aborted: The request was canceled.</span></span>  
<span data-ttu-id="b44eb-308">내부 RCW에서 분리 된 COM 개체를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-308">COM object that has been separated from its underlying RCW cannot be used.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b44eb-309">가능한 원인 및 해결 방법</span><span class="sxs-lookup"><span data-stu-id="b44eb-309">Possible Cause and Solution</span></span>

<span data-ttu-id="b44eb-310">일반적으로이 오류를 해결 하려면 Visual Studio를 닫고 다시 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-310">Closing and restarting Visual Studio is usually all that is required to resolve this error.</span></span>

## <a name="deployment-fails-because-user-credentials-used-for-publishing-dont-have-setacl-authority"></a><span data-ttu-id="b44eb-311">게시에 사용 된 사용자 자격 증명에 setACL 기관이 없으므로 배포가 실패 함</span><span class="sxs-lookup"><span data-stu-id="b44eb-311">Deployment Fails Because User Credentials Used for Publishing Don't Have setACL Authority</span></span>

### <a name="scenario"></a><span data-ttu-id="b44eb-312">시나리오</span><span class="sxs-lookup"><span data-stu-id="b44eb-312">Scenario</span></span>

<span data-ttu-id="b44eb-313">폴더 사용 권한을 설정할 권한이 없다는 것을 나타내는 오류로 인해 게시에 실패 합니다. 사용 중인 사용자 계정에는 setACL 기관이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-313">Publishing fails with an error that indicates you don't have authority to set folder permissions (the user account you are using doesn't have setACL authority).</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b44eb-314">가능한 원인 및 해결 방법</span><span class="sxs-lookup"><span data-stu-id="b44eb-314">Possible Cause and Solution</span></span>

<span data-ttu-id="b44eb-315">기본적으로 Visual Studio는 사이트의 루트 폴더에 대 한 읽기 권한과 앱\_데이터 폴더에 대 한 쓰기 권한을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-315">By default, Visual Studio sets read permissions on the root folder of the site and write permissions on the App\_Data folder.</span></span> <span data-ttu-id="b44eb-316">사이트 폴더에 대 한 기본 사용 권한이 정확 하 고 설정 하지 않아도 되는 경우이 동작을 사용 하지 않도록 설정 합니다 .이 동작을 사용 하지 않도록 설정 **&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** 을 게시 프로필 파일 (단일 프로필에 영향을 줌) 또는 wpp .targets 파일 (모든 프로필에 영향을 줌)에&lt;추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-316">If you know that the default permissions on site folders are correct and do not need to be set, you disable this behavior by adding **&lt;IncludeSetACLProviderOn Destination&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** to the publish profile file (to affect a single profile) or to the wpp.targets file (to affect all profiles).</span></span> <span data-ttu-id="b44eb-317">이러한 파일을 편집 하는 방법에 대 한 자세한 내용은 [방법: 프로필 (pubxml) 파일의 배포 설정 편집](https://msdn.microsoft.com/library/ff398069.aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b44eb-317">For information about how to edit these files, see [How to: Edit Deployment Settings in Profile (.pubxml) Files](https://msdn.microsoft.com/library/ff398069.aspx).</span></span>

## <a name="access-denied-errors-when-the-application-tries-to-write-to-an-application-folder"></a><span data-ttu-id="b44eb-318">응용 프로그램이 응용 프로그램 폴더에 쓰려고 할 때 액세스 거부 오류</span><span class="sxs-lookup"><span data-stu-id="b44eb-318">Access Denied Errors when the Application Tries to Write to an Application Folder</span></span>

### <a name="scenario"></a><span data-ttu-id="b44eb-319">시나리오</span><span class="sxs-lookup"><span data-stu-id="b44eb-319">Scenario</span></span>

<span data-ttu-id="b44eb-320">응용 프로그램 폴더에 대 한 쓰기 권한이 없기 때문에 응용 프로그램 폴더 중 하나에서 파일을 만들거나 편집 하려고 할 때 응용 프로그램 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-320">Your application errors when it tries to create or edit a file in one of the application folders, because it does not have write authority for that folder.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b44eb-321">가능한 원인 및 해결 방법</span><span class="sxs-lookup"><span data-stu-id="b44eb-321">Possible Cause and Solution</span></span>

<span data-ttu-id="b44eb-322">기본적으로 Visual Studio는 사이트의 루트 폴더에 대 한 읽기 권한과 앱\_데이터 폴더에 대 한 쓰기 권한을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-322">By default, Visual Studio sets read permissions on the root folder of the site and write permissions on the App\_Data folder.</span></span> <span data-ttu-id="b44eb-323">하위 폴더에 대 한 쓰기 권한이 응용 프로그램에 필요한 경우이 시리즈의 폴더 권한 설정 및 프로덕션 환경에 배포 자습서에 표시 된 것 처럼 해당 폴더에 대 한 권한을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-323">If your application needs write access to a sub-folder, you can set permissions for that folder as shown in the Setting Folder Permissions and Deploying to the Production Environment tutorials in this series.</span></span> <span data-ttu-id="b44eb-324">응용 프로그램에 사이트의 루트 폴더에 대 한 쓰기 액세스 권한이 필요한 경우에는 해당 응용 프로그램에서 **includesetacl&gt;&lt;&gt;provider&lt;** 을 추가 하 여 루트 폴더에 대 한 읽기 전용 액세스를 설정 하는 것을 방지 해야 합니다 .이 경우에는 게시 프로필 파일 (단일 프로필에 영향을 주는) 또는 wpp .targets 파일 (모든 프로필에 영향을 줌</span><span class="sxs-lookup"><span data-stu-id="b44eb-324">If your application needs write access to the root folder of the site, you have to prevent it from setting read-only access on the root folder by adding **&lt;IncludeSetACLProviderOn Destination&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** to the publish profile file (to affect a single profile) or to the wpp.targets file (to affect all profiles).</span></span> <span data-ttu-id="b44eb-325">이러한 파일을 편집 하는 방법에 대 한 자세한 내용은 [방법: 프로필 (pubxml) 파일의 배포 설정 편집](https://msdn.microsoft.com/library/ff398069.aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b44eb-325">For information about how to edit these files, see [How to: Edit Deployment Settings in Profile (.pubxml) Files](https://msdn.microsoft.com/library/ff398069.aspx).</span></span>

<a id="aspnet45error"></a>

## <a name="configuration-error---targetframework-attribute-references-a-version-that-is-later-than-the-installed-version-of-the-net-framework"></a><span data-ttu-id="b44eb-326">구성 오류-targetFramework 특성이 설치 된 버전 보다 최신 버전을 참조 .NET Framework</span><span class="sxs-lookup"><span data-stu-id="b44eb-326">Configuration Error - targetFramework attribute references a version that is later than the installed version of the .NET Framework</span></span>

### <a name="scenario"></a><span data-ttu-id="b44eb-327">시나리오</span><span class="sxs-lookup"><span data-stu-id="b44eb-327">Scenario</span></span>

<span data-ttu-id="b44eb-328">ASP.NET 4.5를 대상으로 하는 웹 프로젝트를 성공적으로 게시 했지만,이 응용 프로그램을 실행 하는 경우 (customErrors 모드가 Web.config 파일에서 "off"로 설정 된 경우) 다음 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-328">You successfully published a web project that targets ASP.NET 4.5, but when you run the application (with the customErrors mode set to "off" in the Web.config file) you get the following error:</span></span>

<span data-ttu-id="b44eb-329">Web.config 파일의 &lt;컴파일&gt; 요소에 있는 ' targetFramework ' 특성은 .NET Framework 버전 4.0 이상 (예: '&lt;컴파일 targetFramework = "4.0"&gt;')에만 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-329">The 'targetFramework' attribute in the &lt;compilation&gt; element of the Web.config file is used only to target version 4.0 and later of the .NET Framework (for example, '&lt;compilation targetFramework="4.0"&gt;').</span></span> <span data-ttu-id="b44eb-330">' TargetFramework ' 특성은 현재 설치 된 .NET Framework 버전 보다 최신 버전을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-330">The 'targetFramework' attribute currently references a version that is later than the installed version of the .NET Framework.</span></span> <span data-ttu-id="b44eb-331">.NET Framework의 올바른 대상 버전을 지정 하거나 필요한 .NET Framework 버전을 설치 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b44eb-331">Specify a valid target version of the .NET Framework, or install the required version of the .NET Framework.</span></span>

<span data-ttu-id="b44eb-332">오류 페이지의 원본 오류 상자는 Web.config의 다음 줄을 오류의 원인으로 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-332">The Source Error box of the error page highlights the following line from Web.config as the cause of the error:</span></span>

<span data-ttu-id="b44eb-333">&lt;컴파일 targetFramework = "4.5"/&gt;</span><span class="sxs-lookup"><span data-stu-id="b44eb-333">&lt;compilation targetFramework="4.5" /&gt;</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b44eb-334">가능한 원인 및 해결 방법</span><span class="sxs-lookup"><span data-stu-id="b44eb-334">Possible Cause and Solution</span></span>

<span data-ttu-id="b44eb-335">서버에서 ASP.NET 4.5를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-335">The server does not support ASP.NET 4.5.</span></span> <span data-ttu-id="b44eb-336">호스팅 공급자에 게 문의 하 여 ASP.NET 4.5에 대 한 지원을 추가할 수 있는 시기 및 시기를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-336">Contact the hosting provider to determine when and if support for ASP.NET 4.5 can be added.</span></span> <span data-ttu-id="b44eb-337">서버를 업그레이드할 수 없는 경우 대신 ASP.NET 4 또는 이전 버전을 대상으로 하는 웹 프로젝트를 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-337">If upgrading the server is not an option, you have to deploy a web project that targets ASP.NET 4 or earlier instead.</span></span>

<span data-ttu-id="b44eb-338">ASP.NET 4 또는 이전 웹 프로젝트를 동일한 대상에 배포 하는 경우 **웹 게시** 마법사의 **설정** 탭에서 **대상에서 추가 파일 제거** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-338">If you deploy an ASP.NET 4 or earlier web project to the same destination, select the **Remove additional files at destination** check box on the **Settings** tab of the **Publish Web** wizard.</span></span> <span data-ttu-id="b44eb-339">**대상에서 추가 파일 제거**를 선택 하지 않으면 계속 해 서 구성 오류 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-339">If you don't select **Remove additional files at destination**, you will continue to get the Configuration Error page.</span></span>

<span data-ttu-id="b44eb-340">프로젝트 **속성** 창에는 대상 프레임 워크 드롭다운 목록이 포함 되어 있지만 **.NET Framework 4.5** 에서 **.NET Framework 4**로 변경 하면이 문제를 해결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-340">The project **Properties** windows includes a Target framework drop-down list, but you can't resolve this problem by just changing that from **.NET Framework 4.5** to **.NET Framework 4**.</span></span> <span data-ttu-id="b44eb-341">대상 프레임 워크를 이전 프레임 워크 버전으로 변경 하는 경우 프로젝트는 이후 프레임 워크 버전의 어셈블리에 대 한 참조를 계속 가지 며 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-341">If you change the target framework to an earlier framework version, the project will still have references to the later framework version's assemblies and will not run.</span></span> <span data-ttu-id="b44eb-342">이러한 참조를 수동으로 변경 하거나 .NET Framework 4 또는 이전 버전을 대상으로 하는 새 프로젝트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-342">You have to manually change those references or create a new project that targets .NET Framework 4 or earlier.</span></span> <span data-ttu-id="b44eb-343">자세한 내용은 [.NET Framework 대상 웹 사이트](https://msdn.microsoft.com/library/bb398791(v=vs.100).aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b44eb-343">For more information, see [.NET Framework Targeting for Web Sites](https://msdn.microsoft.com/library/bb398791(v=vs.100).aspx).</span></span>

## <a name="medium-trust-errors"></a><span data-ttu-id="b44eb-344">보통 신뢰 오류</span><span class="sxs-lookup"><span data-stu-id="b44eb-344">Medium Trust Errors</span></span>

### <a name="scenario"></a><span data-ttu-id="b44eb-345">시나리오</span><span class="sxs-lookup"><span data-stu-id="b44eb-345">Scenario</span></span>

<span data-ttu-id="b44eb-346">프로덕션 환경에서 응용 프로그램을 실행 하는 경우 보통 신뢰와 관련 된 오류를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-346">When you run your application in production, it gets an error related to medium trust.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b44eb-347">가능한 원인 및 해결 방법</span><span class="sxs-lookup"><span data-stu-id="b44eb-347">Possible Cause and Solution</span></span>

<span data-ttu-id="b44eb-348">대부분의 타사 호스팅 공급자는 보통 신뢰 수준에서 웹 사이트를 실행 합니다. 즉, 일부 작업을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-348">Many third-party hosting providers run your web site in medium trust, which means that there are some things it isn't allowed to do.</span></span> <span data-ttu-id="b44eb-349">예를 들어 응용 프로그램 코드는 Windows 레지스트리에 액세스할 수 없고 응용 프로그램의 폴더 계층 구조 외부에 있는 파일을 읽거나 쓸 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-349">For example, application code can't access the Windows registry and can't read or write files that are outside of your application's folder hierarchy.</span></span> <span data-ttu-id="b44eb-350">기본적으로 응용 프로그램은 로컬 컴퓨터에서 *완전 신뢰로* 실행 됩니다. 즉, 응용 프로그램이 프로덕션 환경에 배포할 때 실패 하는 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-350">By default your application runs in *full trust* on your local computer, which means that the application might be able to do things that would fail when you deploy it to production.</span></span>

<span data-ttu-id="b44eb-351">문제를 해결 하기 위해 로컬 IIS 환경의 보통 신뢰 수준에서 실행 되도록 응용 프로그램을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-351">You can configure the application to run in medium trust in the local IIS environment in order to troubleshoot.</span></span> <span data-ttu-id="b44eb-352">이렇게 하려면 응용 프로그램 *web.config* 파일을 열고 다음 예제와 같이 system.web 요소에 **trust** 요소를 추가 **합니다.**</span><span class="sxs-lookup"><span data-stu-id="b44eb-352">To do that, open the application *Web.config* file, and add a **trust** element in the **system.web** element, as shown in this example.</span></span>

[!code-xml[Main](troubleshooting/samples/sample11.xml)]

<span data-ttu-id="b44eb-353">이제 응용 프로그램은 로컬 컴퓨터 에서도 IIS의 보통 신뢰 수준으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-353">The application will now run in medium trust in IIS even on your local computer.</span></span>

<span data-ttu-id="b44eb-354">Azure App Service에 배포 하는 경우에는이 작업을 수행 하지 마세요. Azure에는 보통 신뢰가 필요 하지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-354">Don't do this if you are deploying to Azure App Service, because Azure does not require medium trust.</span></span> <span data-ttu-id="b44eb-355">이 자습서를 2012 년 2 월에 작성 하는 시점에이 방법을 사용 하 여 응용 프로그램이 보통 신뢰로 실행 되도록 하면 Azure에서 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-355">At the time this tutorial is being written in February, 2012, using this method to make your application run in medium trust will cause an error in Azure.</span></span>

<span data-ttu-id="b44eb-356">Entity Framework Code First 마이그레이션를 사용 하 고 보통 신뢰 수준에서 응용 프로그램을 실행 하는 호스팅 공급자에 배포 하는 경우 버전 5.0 이상을 설치 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-356">If you are using Entity Framework Code First Migrations and you are deploying to a hosting provider that runs your application in medium trust, make sure that you have version 5.0 or later installed.</span></span> <span data-ttu-id="b44eb-357">Entity Framework 버전 4.3에서는 마이그레이션에 데이터베이스 스키마를 업데이트 하기 위해 완전 신뢰가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-357">In Entity Framework version 4.3, Migrations requires full trust in order to update the database schema.</span></span>

## <a name="http-40417-not-found-error"></a><span data-ttu-id="b44eb-358">HTTP 404.17 찾을 수 없음 오류</span><span class="sxs-lookup"><span data-stu-id="b44eb-358">HTTP 404.17 Not Found Error</span></span>

### <a name="scenario"></a><span data-ttu-id="b44eb-359">시나리오</span><span class="sxs-lookup"><span data-stu-id="b44eb-359">Scenario</span></span>

<span data-ttu-id="b44eb-360">IIS의 개발 컴퓨터에서 배포 된 사이트를 실행 하는 경우 서버에서 Default.aspx를 처리할 수 없음을 보고 하는 다음과 같은 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-360">When you run the deployed site on your development computer in IIS, you see the following error message reporting that the server can't process Default.aspx:</span></span>

<span data-ttu-id="b44eb-361">HTTP 오류 404.17-찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="b44eb-361">HTTP Error 404.17 - Not Found</span></span>

<span data-ttu-id="b44eb-362">요청 된 콘텐츠는 스크립트로 표시 되며 정적 파일 처리기에서 제공 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-362">The requested content appears to be script and will not be served by the static file handler.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b44eb-363">가능한 원인 및 해결 방법</span><span class="sxs-lookup"><span data-stu-id="b44eb-363">Possible Cause and Solution</span></span>

<span data-ttu-id="b44eb-364">ASP.NET 4.5이 컴퓨터에 설치 되어 있지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b44eb-364">ASP.NET 4.5 might not be installed on your computer.</span></span> <span data-ttu-id="b44eb-365">ASP.NET 4.5을 설치 하는 방법을 설명 하는이 시리즈의 테스트 환경으로 IIS에 배포 자습서의 단계를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b44eb-365">See the steps in the Deploying to IIS as a Test Environment tutorial in this series that explain how to install ASP.NET 4.5.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="b44eb-366">이전</span><span class="sxs-lookup"><span data-stu-id="b44eb-366">Previous</span></span>](deploying-extra-files.md)
