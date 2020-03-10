---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
title: MSBuild 프로젝트 파일에서 Windows PowerShell 스크립트 실행 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 빌드 및 배포 프로세스의 일부로 Windows PowerShell 스크립트를 실행 하는 방법에 대해 설명 합니다. 스크립트를 로컬로 실행할 수 있습니다. 즉,
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 55f1ae45-fcb5-43a9-8415-fa5b935fc9c9
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
msc.type: authoredcontent
ms.openlocfilehash: 7b09c07b8b7c2a61ca534f7a66a929593f3d04ca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78441449"
---
# <a name="running-windows-powershell-scripts-from-msbuild-project-files"></a><span data-ttu-id="14dff-104">MSBuild 프로젝트 파일에서 Windows PowerShell 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="14dff-104">Running Windows PowerShell Scripts from MSBuild Project Files</span></span>

<span data-ttu-id="14dff-105">[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="14dff-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="14dff-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="14dff-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="14dff-107">이 항목에서는 빌드 및 배포 프로세스의 일부로 Windows PowerShell 스크립트를 실행 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-107">This topic describes how to run a Windows PowerShell script as part of a build and deployment process.</span></span> <span data-ttu-id="14dff-108">대상 웹 서버 또는 데이터베이스 서버와 같이 로컬에서 (즉, 빌드 서버에서) 또는 원격으로 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-108">You can run a script locally (in other words, on the build server) or remotely, like on a destination web server or database server.</span></span>
> 
> <span data-ttu-id="14dff-109">배포 후 Windows PowerShell 스크립트를 실행 하려는 많은 이유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-109">There are lots of reasons why you might want to run a post-deployment Windows PowerShell script.</span></span> <span data-ttu-id="14dff-110">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-110">For example, you might want to:</span></span>
> 
> - <span data-ttu-id="14dff-111">레지스트리에 사용자 지정 이벤트 소스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-111">Add a custom event source to the registry.</span></span>
> - <span data-ttu-id="14dff-112">업로드할 파일 시스템 디렉터리를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-112">Generate a file system directory for uploads.</span></span>
> - <span data-ttu-id="14dff-113">빌드 디렉터리를 정리 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-113">Clean up build directories.</span></span>
> - <span data-ttu-id="14dff-114">사용자 지정 로그 파일에 항목을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-114">Write entries to a custom log file.</span></span>
> - <span data-ttu-id="14dff-115">새로 프로 비전 된 웹 응용 프로그램에 사용자를 초대 하는 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-115">Send emails inviting users to a newly provisioned web application.</span></span>
> - <span data-ttu-id="14dff-116">적절 한 권한이 있는 사용자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-116">Create user accounts with the appropriate permissions.</span></span>
> - <span data-ttu-id="14dff-117">SQL Server 인스턴스 간에 복제를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-117">Configure replication between SQL Server instances.</span></span>
> 
> <span data-ttu-id="14dff-118">이 항목에서는 MSBuild (Microsoft Build Engine) 프로젝트 파일의 사용자 지정 대상에서 로컬 및 원격으로 Windows PowerShell 스크립트를 실행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-118">This topic will show you how to run Windows PowerShell scripts both locally and remotely from a custom target in a Microsoft Build Engine (MSBuild) project file.</span></span>

<span data-ttu-id="14dff-119">이 항목에서는 Fabrikam, i n c. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 기반으로 하는 일련의 자습서의 일부를 형성 합니다. 이 자습서 시리즈에서는 샘플 솔루션&#x2014;&#x2014;을 사용 [하 여](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)ASP.NET MVC 3 응용 프로그램, Windows Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 비롯 한 현실적인 복잡성의 웹 응용 프로그램을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-119">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="14dff-120">이러한 자습서의 핵심에 나오는 배포 방법은 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)에 설명 된 프로젝트 파일을 이해 하는 방법에 설명 되어 있습니다 .이는 빌드 프로세스가 모든 대상 환경에 적용&#x2014;되는 빌드 명령을 포함 하는 두 개의 프로젝트 파일과 환경 특정 빌드 및 배포 설정을 포함 하는 프로젝트 파일에 의해 제어 됩니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-120">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="14dff-121">빌드 시 환경 관련 프로젝트 파일은 환경에 관계 없는 프로젝트 파일에 병합 되어 전체 빌드 명령 집합을 형성 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-121">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="14dff-122">작업 개요</span><span class="sxs-lookup"><span data-stu-id="14dff-122">Task Overview</span></span>

<span data-ttu-id="14dff-123">자동 또는 단일 단계 배포 프로세스의 일부로 Windows PowerShell 스크립트를 실행 하려면 다음과 같은 개략적인 작업을 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-123">To run a Windows PowerShell script as part of an automated or single-step deployment process, you'll need to complete these high-level tasks:</span></span>

- <span data-ttu-id="14dff-124">Windows PowerShell 스크립트를 솔루션에 추가 하 고 소스 제어에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-124">Add the Windows PowerShell script to your solution and to source control.</span></span>
- <span data-ttu-id="14dff-125">Windows PowerShell 스크립트를 호출 하는 명령을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-125">Create a command that invokes your Windows PowerShell script.</span></span>
- <span data-ttu-id="14dff-126">명령에서 모든 예약 된 XML 문자를 이스케이프 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-126">Escape any reserved XML characters in your command.</span></span>
- <span data-ttu-id="14dff-127">사용자 지정 MSBuild 프로젝트 파일에서 대상을 만들고 **Exec** 작업을 사용 하 여 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-127">Create a target in your custom MSBuild project file and use the **Exec** task to run your command.</span></span>

<span data-ttu-id="14dff-128">이 항목에서는 이러한 절차를 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-128">This topic will show you how to perform these procedures.</span></span> <span data-ttu-id="14dff-129">이 항목의 작업 및 연습에서는 이미 MSBuild 대상과 속성을 잘 알고 있고 사용자 지정 MSBuild 프로젝트 파일을 사용 하 여 빌드 및 배포 프로세스를 구동 하는 방법을 이해 하 고 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-129">The tasks and walkthroughs in this topic assume that you're already familiar with MSBuild targets and properties, and that you understand how to use a custom MSBuild project file to drive a build and deployment process.</span></span> <span data-ttu-id="14dff-130">자세한 내용은 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md) 및 [빌드 프로세스 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="14dff-130">For more information, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span>

## <a name="creating-and-adding-windows-powershell-scripts"></a><span data-ttu-id="14dff-131">Windows PowerShell 스크립트 만들기 및 추가</span><span class="sxs-lookup"><span data-stu-id="14dff-131">Creating and Adding Windows PowerShell Scripts</span></span>

<span data-ttu-id="14dff-132">이 항목의 태스크에서는 MSBuild에서 스크립트를 실행 하는 방법을 보여 주기 위해 **Logdeploy. ps1** 이라는 샘플 Windows PowerShell 스크립트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-132">The tasks in this topic use a sample Windows PowerShell script named **LogDeploy.ps1** to illustrate how to run scripts from MSBuild.</span></span> <span data-ttu-id="14dff-133">**Logdeploy. ps1** 스크립트에는 로그 파일에 한 줄 항목을 기록 하는 간단한 함수가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-133">The **LogDeploy.ps1** script contains a simple function that writes a single-line entry to a log file:</span></span>

[!code-powershell[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample1.ps1)]

<span data-ttu-id="14dff-134">**Logdeploy. ps1** 스크립트는 두 개의 매개 변수를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-134">The **LogDeploy.ps1** script accepts two parameters.</span></span> <span data-ttu-id="14dff-135">첫 번째 매개 변수는 항목을 추가할 로그 파일의 전체 경로를 나타내고, 두 번째 매개 변수는 로그 파일에 기록 하려는 배포 대상을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-135">The first parameter represents the full path to the log file to which you want to add an entry, and the second parameter represents the deployment destination that you want to record in the log file.</span></span> <span data-ttu-id="14dff-136">스크립트를 실행 하면 로그 파일에 다음 형식으로 줄이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-136">When you run the script, it adds a line to the log file in this format:</span></span>

[!code-html[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample2.html)]

<span data-ttu-id="14dff-137">MSBuild에서 **Logdeploy. ps1** 스크립트를 사용할 수 있도록 하려면 다음을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-137">To make the **LogDeploy.ps1** script available to MSBuild, you need to:</span></span>

- <span data-ttu-id="14dff-138">소스 제어에 스크립트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-138">Add the script to source control.</span></span>
- <span data-ttu-id="14dff-139">Visual Studio 2010에서 솔루션에 스크립트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-139">Add the script to your solution in Visual Studio 2010.</span></span>

<span data-ttu-id="14dff-140">빌드 서버 또는 원격 컴퓨터에서 스크립트를 실행할 계획 인지 여부에 관계 없이 솔루션 콘텐츠와 함께 스크립트를 배포할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-140">You don't need to deploy the script with your solution content, regardless of whether you plan to run the script on the build server or on a remote computer.</span></span> <span data-ttu-id="14dff-141">한 가지 옵션은 솔루션 폴더에 스크립트를 추가 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-141">One option is to add the script to a solution folder.</span></span> <span data-ttu-id="14dff-142">Contact Manager 예제에서 배포 프로세스의 일부로 Windows PowerShell 스크립트를 사용 하려는 경우 게시 솔루션 폴더에 스크립트를 추가 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-142">In the Contact Manager example, because you want to use the Windows PowerShell script as part of the deployment process, it makes sense to add the script to the Publish solution folder.</span></span>

![](running-windows-powershell-scripts-from-msbuild-project-files/_static/image1.png)

<span data-ttu-id="14dff-143">솔루션 폴더의 콘텐츠는 빌드 서버에 원본 자료로 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-143">The contents of solution folders are copied to build servers as source material.</span></span> <span data-ttu-id="14dff-144">그러나 프로젝트 출력의 일부는 구성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-144">However, they form no part of any project output.</span></span>

## <a name="executing-a-windows-powershell-script-on-the-build-server"></a><span data-ttu-id="14dff-145">빌드 서버에서 Windows PowerShell 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="14dff-145">Executing a Windows PowerShell Script on the Build Server</span></span>

<span data-ttu-id="14dff-146">일부 시나리오에서는 프로젝트를 빌드하는 컴퓨터에서 Windows PowerShell 스크립트를 실행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-146">In some scenarios, you may want to run Windows PowerShell scripts on the computer that builds your projects.</span></span> <span data-ttu-id="14dff-147">예를 들어 Windows PowerShell 스크립트를 사용 하 여 빌드 폴더를 정리 하거나 사용자 지정 로그 파일에 항목을 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-147">For example, you might use a Windows PowerShell script to clean up build folders or write entries to a custom log file.</span></span>

<span data-ttu-id="14dff-148">구문 측면에서 MSBuild 프로젝트 파일을 사용 하 여 Windows PowerShell 스크립트를 실행 하는 것은 일반 명령 프롬프트에서 Windows PowerShell 스크립트를 실행 하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-148">In terms of syntax, running a Windows PowerShell script from an MSBuild project file is the same as running a Windows PowerShell script from a regular command prompt.</span></span> <span data-ttu-id="14dff-149">Powershell .exe 실행 파일을 호출 하 고 **– command** 스위치를 사용 하 여 Windows powershell을 실행 하려는 명령을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-149">You need to invoke the powershell.exe executable and use the **–command** switch to provide the commands you want Windows PowerShell to run.</span></span> <span data-ttu-id="14dff-150">Windows PowerShell v2에서는 **– file** 스위치를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-150">(In Windows PowerShell v2, you can also use the **–file** switch).</span></span> <span data-ttu-id="14dff-151">이 명령은 다음 형식을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-151">The command should take this format:</span></span>

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample3.cmd)]

<span data-ttu-id="14dff-152">다음은 그 예입니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-152">For example:</span></span>

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample4.cmd)]

<span data-ttu-id="14dff-153">스크립트의 경로에 공백이 포함 된 경우 파일 경로를 앰퍼샌드 앞에 오는 작은따옴표로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-153">If the path to your script includes spaces, you need to enclose the file path in single quotes preceded by an ampersand.</span></span> <span data-ttu-id="14dff-154">사용자가 이미 명령을 묶는 데 사용 했기 때문에 큰따옴표를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-154">You can't use double quotes, because you've already used them to enclose the command:</span></span>

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample5.cmd)]

<span data-ttu-id="14dff-155">MSBuild에서이 명령을 호출 하는 경우 몇 가지 사항을 추가로 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-155">There are a few additional considerations when you invoke this command from MSBuild.</span></span> <span data-ttu-id="14dff-156">먼저 **-비 대화형** 플래그를 포함 하 여 스크립트가 자동으로 실행 되도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-156">First, you should include the **–NonInteractive** flag to ensure that the script executes quietly.</span></span> <span data-ttu-id="14dff-157">다음으로 적절 한 인수 값을 사용 하 여 **– set-executionpolicy** 플래그를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-157">Next, you should include the **–ExecutionPolicy** flag with an appropriate argument value.</span></span> <span data-ttu-id="14dff-158">이는 Windows PowerShell이 스크립트에 적용 되는 실행 정책을 지정 하며, 스크립트 실행을 방해할 수 있는 기본 실행 정책을 재정의할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-158">This specifies the execution policy that Windows PowerShell will apply to your script and allows you to override the default execution policy, which may prevent execution of your script.</span></span> <span data-ttu-id="14dff-159">다음 인수 값 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-159">You can choose from these argument values:</span></span>

- <span data-ttu-id="14dff-160">**제한** 값을 사용 하면 스크립트가 서명 되었는지 여부에 관계 없이 Windows PowerShell에서 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-160">A value of **Unrestricted** will allow Windows PowerShell to execute your script, regardless of whether the script is signed.</span></span>
- <span data-ttu-id="14dff-161">**RemoteSigned** 값을 사용 하면 Windows PowerShell에서 로컬 컴퓨터에 생성 된 서명 되지 않은 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-161">A value of **RemoteSigned** will allow Windows PowerShell to execute unsigned scripts that were created on the local machine.</span></span> <span data-ttu-id="14dff-162">그러나 다른 곳에서 만든 스크립트는 서명 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-162">However, scripts that were created elsewhere must be signed.</span></span> <span data-ttu-id="14dff-163">실제로는 빌드 서버에서 로컬로 Windows PowerShell 스크립트를 만들 가능성이 거의 없습니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-163">(In practice, you're very unlikely to have created a Windows PowerShell script locally on a build server).</span></span>
- <span data-ttu-id="14dff-164">**AllSigned** 값을 사용 하면 Windows PowerShell에서 서명 된 스크립트만 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-164">A value of **AllSigned** will allow Windows PowerShell to execute signed scripts only.</span></span>

<span data-ttu-id="14dff-165">기본 실행 정책은 Windows PowerShell에서 스크립트 파일을 실행할 수 없도록 **제한**됩니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-165">The default execution policy is **Restricted**, which prevents Windows PowerShell from running any script files.</span></span>

<span data-ttu-id="14dff-166">마지막으로, Windows PowerShell 명령에서 발생 하는 모든 예약 된 XML 문자를 이스케이프 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-166">Finally, you need to escape any reserved XML characters that occur in your Windows PowerShell command:</span></span>

- <span data-ttu-id="14dff-167">작은따옴표를 **&amp;apos;** 로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-167">Replace single quotes with **&amp;apos;**</span></span>
- <span data-ttu-id="14dff-168">큰따옴표를 **&amp;q;** 로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-168">Replace double quotes with **&amp;quot;**</span></span>
- <span data-ttu-id="14dff-169">앰퍼샌드를 **&amp;amp** 로 바꾸기</span><span class="sxs-lookup"><span data-stu-id="14dff-169">Replace ampersands with **&amp;amp;**</span></span>

- <span data-ttu-id="14dff-170">이러한 변경을 수행 하는 경우 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-170">When you make these changes, your command will resemble this:</span></span>

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample6.cmd)]

<span data-ttu-id="14dff-171">사용자 지정 MSBuild 프로젝트 파일 내에서 새 대상을 만들고 **Exec** 작업을 사용 하 여 다음 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-171">Within your custom MSBuild project file, you can create a new target and use the **Exec** task to run this command:</span></span>

[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample7.xml)]

<span data-ttu-id="14dff-172">이 예제에서는 다음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-172">In this example, note that:</span></span>

- <span data-ttu-id="14dff-173">매개 변수 값 및 Windows PowerShell 실행 파일의 위치와 같은 모든 변수는 MSBuild 속성으로 선언 됩니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-173">Any variables, like parameter values and the location of the Windows PowerShell executable, are declared as MSBuild properties.</span></span>
- <span data-ttu-id="14dff-174">사용자가 명령줄에서 이러한 값을 재정의할 수 있도록 하는 조건이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-174">Conditions are included to enable users to override these values from the command line.</span></span>
- <span data-ttu-id="14dff-175">**MSDeployComputerName** 속성은 프로젝트 파일의 다른 위치에 선언 됩니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-175">The **MSDeployComputerName** property is declared elsewhere in the project file.</span></span>

<span data-ttu-id="14dff-176">빌드 프로세스의 일부로이 대상을 실행 하면 Windows PowerShell에서 명령을 실행 하 고 지정한 파일에 로그 항목을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-176">When you execute this target as part of your build process, Windows PowerShell will run your command and write a log entry to the file you specified.</span></span>

## <a name="executing-a-windows-powershell-script-on-a-remote-computer"></a><span data-ttu-id="14dff-177">원격 컴퓨터에서 Windows PowerShell 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="14dff-177">Executing a Windows PowerShell Script on a Remote Computer</span></span>

<span data-ttu-id="14dff-178">Windows PowerShell은 WinRM ( [Windows 원격 관리](https://msdn.microsoft.com/library/windows/desktop/aa384426.aspx) )을 통해 원격 컴퓨터에서 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-178">Windows PowerShell is capable of running scripts on remote computers through [Windows Remote Management](https://msdn.microsoft.com/library/windows/desktop/aa384426.aspx) (WinRM).</span></span> <span data-ttu-id="14dff-179">이렇게 하려면 [Invoke Command](https://technet.microsoft.com/library/dd347578.aspx) cmdlet을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-179">To do this, you need to use the [Invoke-Command](https://technet.microsoft.com/library/dd347578.aspx) cmdlet.</span></span> <span data-ttu-id="14dff-180">이를 통해 원격 컴퓨터에 스크립트를 복사 하지 않고 하나 이상의 원격 컴퓨터에 대해 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-180">This lets you execute your script against one or more remote computers without copying the script to the remote computers.</span></span> <span data-ttu-id="14dff-181">모든 결과는 스크립트를 실행 한 로컬 컴퓨터로 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-181">Any results are returned to the local computer from which you ran the script.</span></span>

> [!NOTE]
> <span data-ttu-id="14dff-182">**호출 명령** cmdlet을 사용 하 여 원격 컴퓨터에서 Windows PowerShell 스크립트를 실행 하기 전에 원격 메시지를 수락 하도록 WinRM 수신기를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-182">Before you use the **Invoke-Command** cmdlet to execute Windows PowerShell scripts on a remote computer, you need to configure a WinRM listener to accept remote messages.</span></span> <span data-ttu-id="14dff-183">원격 컴퓨터에서 **winrm quickconfig** 명령을 실행 하 여이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-183">You can do this by running the command **winrm quickconfig** on the remote computer.</span></span> <span data-ttu-id="14dff-184">자세한 내용은 [Windows 원격 관리 설치 및 구성](https://msdn.microsoft.com/library/windows/desktop/aa384372(v=vs.85).aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="14dff-184">For more information, see [Installation and Configuration for Windows Remote Management](https://msdn.microsoft.com/library/windows/desktop/aa384372(v=vs.85).aspx).</span></span>

<span data-ttu-id="14dff-185">Windows PowerShell 창에서이 구문을 사용 하 여 원격 컴퓨터에서 **Logdeploy.** p s 1 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-185">From a Windows PowerShell window, you'd use this syntax to run the **LogDeploy.ps1** script on a remote computer:</span></span>

[!code-powershell[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample8.ps1)]

> [!NOTE]
> <span data-ttu-id="14dff-186">**Invoke 명령을** 사용 하 여 스크립트 파일을 실행 하는 다른 여러 가지 방법이 있지만이 방법은 매개 변수 값을 제공 하 고 공백을 사용 하 여 경로를 관리 해야 하는 경우에 가장 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-186">There are various other ways of using **Invoke-Command** to run a script file, but this approach is the most straightforward when you need to provide parameter values and manage paths with spaces.</span></span>

<span data-ttu-id="14dff-187">명령 프롬프트에서이 명령을 실행 하는 경우 Windows PowerShell 실행 파일을 호출 하 고 **– command** 매개 변수를 사용 하 여 지침을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-187">When you run this from a command prompt, you need to invoke the Windows PowerShell executable and use the **–command** parameter to provide your instructions:</span></span>

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample9.cmd)]

<span data-ttu-id="14dff-188">이전과 마찬가지로 MSBuild에서 명령을 실행할 때 몇 가지 추가 스위치를 제공 하 고 예약 된 XML 문자를 이스케이프 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-188">As before, you need to provide some additional switches and escape any reserved XML characters when you run the command from MSBuild:</span></span>

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample10.cmd)]

<span data-ttu-id="14dff-189">마지막으로, 이전과 같이 사용자 지정 MSBuild 대상 내에서 **Exec** 작업을 사용 하 여 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-189">Finally, as before, you can use the **Exec** task within a custom MSBuild target to execute your command:</span></span>

[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample11.xml)]

<span data-ttu-id="14dff-190">빌드 프로세스의 일부로이 대상을 실행 하는 경우 Windows PowerShell은 **– computername** 인수에 지정 된 컴퓨터에서 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-190">When you execute this target as part of your build process, Windows PowerShell will run your script on the computer you specified in the **–computername** argument.</span></span>

## <a name="conclusion"></a><span data-ttu-id="14dff-191">결론</span><span class="sxs-lookup"><span data-stu-id="14dff-191">Conclusion</span></span>

<span data-ttu-id="14dff-192">이 항목에서는 MSBuild 프로젝트 파일에서 Windows PowerShell 스크립트를 실행 하는 방법에 대해 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-192">This topic described how to run a Windows PowerShell script from an MSBuild project file.</span></span> <span data-ttu-id="14dff-193">이 방법을 사용 하 여 자동 또는 단일 단계 빌드 및 배포 프로세스의 일부로 Windows PowerShell 스크립트를 로컬 또는 원격 컴퓨터에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14dff-193">You can use this approach to run a Windows PowerShell script, either locally or on a remote computer, as part of an automated or single-step build and deployment process.</span></span>

## <a name="further-reading"></a><span data-ttu-id="14dff-194">추가 참고 자료</span><span class="sxs-lookup"><span data-stu-id="14dff-194">Further Reading</span></span>

<span data-ttu-id="14dff-195">Windows PowerShell 스크립트에 서명 하 고 실행 정책을 관리 하는 방법에 대 한 지침은 [Windows Powershell 스크립트 실행](https://technet.microsoft.com/library/ee176949.aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="14dff-195">For guidance on signing Windows PowerShell scripts and managing execution policies, see [Running Windows PowerShell Scripts](https://technet.microsoft.com/library/ee176949.aspx).</span></span> <span data-ttu-id="14dff-196">원격 컴퓨터에서 Windows PowerShell 명령을 실행 하는 방법에 대 한 지침은 [원격 명령 실행](https://technet.microsoft.com/library/dd819505.aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="14dff-196">For guidance on running Windows PowerShell commands from a remote computer, see [Running Remote Commands](https://technet.microsoft.com/library/dd819505.aspx).</span></span>

<span data-ttu-id="14dff-197">사용자 지정 MSBuild 프로젝트 파일을 사용 하 여 배포 프로세스를 제어 하는 방법에 대 한 자세한 내용은 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md) 및 [빌드 프로세스 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="14dff-197">For more information on using custom MSBuild project files to control the deployment process, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="14dff-198">[이전](taking-web-applications-offline-with-web-deploy.md)
> [다음](troubleshooting-the-packaging-process.md)</span><span class="sxs-lookup"><span data-stu-id="14dff-198">[Previous](taking-web-applications-offline-with-web-deploy.md)
[Next](troubleshooting-the-packaging-process.md)</span></span>
