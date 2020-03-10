---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
title: 패키징 프로세스 문제 해결 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 EnablePackageProcessLoggingAndAssert 속성을 사용 하 여 패키징 프로세스에 대 한 자세한 정보를 수집 하는 방법에 대해 설명 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 794bd819-00fc-47e2-876d-fc5d15e0de1c
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
msc.type: authoredcontent
ms.openlocfilehash: 8ad649dfff085a8774cc13c11d8a3e3d48277d66
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509753"
---
# <a name="troubleshooting-the-packaging-process"></a><span data-ttu-id="39c2c-103">패키징 프로세스 문제 해결</span><span class="sxs-lookup"><span data-stu-id="39c2c-103">Troubleshooting the Packaging Process</span></span>

<span data-ttu-id="39c2c-104">[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="39c2c-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="39c2c-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="39c2c-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="39c2c-106">이 항목에서는 Microsoft Build Engine (MSBuild)에서 **EnablePackageProcessLoggingAndAssert** 속성을 사용 하 여 패키징 프로세스에 대 한 자세한 정보를 수집 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-106">This topic describes how you can collect detailed information about the packaging process by using the **EnablePackageProcessLoggingAndAssert** property in the Microsoft Build Engine (MSBuild).</span></span>
> 
> <span data-ttu-id="39c2c-107">**EnablePackageProcessLoggingAndAssert** 속성을 **true**로 설정 하면 MSBuild에서 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-107">When you set the **EnablePackageProcessLoggingAndAssert** property to **true**, MSBuild will:</span></span>
> 
> - <span data-ttu-id="39c2c-108">패키징 프로세스에 대 한 추가 정보를 빌드 로그에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-108">Add additional information about the packaging process to the build logs.</span></span>
> - <span data-ttu-id="39c2c-109">특정 조건에 따라 오류를 기록 합니다. 예를 들어 패키지 목록에서 중복 된 파일을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-109">Log errors under certain conditions, for example, if duplicate files are found in the packaging list.</span></span>
> - <span data-ttu-id="39c2c-110">*ProjectName*\_패키지 폴더에 로그 디렉터리를 만들고이를 사용 하 여 패키지 중인 파일에 대 한 정보를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-110">Create a Log directory in the *ProjectName*\_Package folder and use it to record information about the files you're packaging.</span></span>
> 
> <span data-ttu-id="39c2c-111">패키징 프로세스가 실패 하거나 웹 배포 패키지에 원하는 파일이 포함 되지 않은 경우이 정보를 사용 하 여 프로세스 문제를 해결 하 고 문제가 발생 한 위치를 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-111">If the packaging process is failing, or your web deployment packages don't contain the files that you expect, you can use this information to troubleshoot the process and pinpoint where things are going wrong.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="39c2c-112">**EnablePackageProcessLoggingAndAssert** 속성은 **디버그** 구성을 사용 하 여 프로젝트를 빌드하는 경우에만 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-112">The **EnablePackageProcessLoggingAndAssert** property only works if you build your project using the **Debug** configuration.</span></span> <span data-ttu-id="39c2c-113">다른 구성에서는 속성이 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-113">The property is ignored in other configurations.</span></span>

<span data-ttu-id="39c2c-114">이 항목에서는 Fabrikam, i n c. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 기반으로 하는 일련의 자습서의 일부를 형성 합니다. 이 자습서 시리즈에서는 샘플 솔루션&#x2014;&#x2014;을 사용 [하 여](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)ASP.NET MVC 3 응용 프로그램, Windows Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 비롯 한 현실적인 복잡성의 웹 응용 프로그램을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-114">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="39c2c-115">이러한 자습서의 핵심에 나오는 배포 방법은 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)에 설명 된 프로젝트 파일을 이해 하는 방법에 설명 되어 있습니다 .이는 빌드 프로세스가 모든 대상 환경에 적용&#x2014;되는 빌드 명령을 포함 하는 두 개의 프로젝트 파일과 환경 특정 빌드 및 배포 설정을 포함 하는 프로젝트 파일에 의해 제어 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-115">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="39c2c-116">빌드 시 환경 관련 프로젝트 파일은 환경에 관계 없는 프로젝트 파일에 병합 되어 전체 빌드 명령 집합을 형성 합니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-116">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="understanding-the-enablepackageprocessloggingandassert-property"></a><span data-ttu-id="39c2c-117">EnablePackageProcessLoggingAndAssert 속성 이해</span><span class="sxs-lookup"><span data-stu-id="39c2c-117">Understanding the EnablePackageProcessLoggingAndAssert Property</span></span>

<span data-ttu-id="39c2c-118">웹 [응용 프로그램 프로젝트 빌드 및 패키징을](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md) 통해 웹 게시 파이프라인 (WPP)에서 msbuild의 기능을 확장 하 고 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)와 통합할 수 있는 msbuild 대상 집합을 제공 하는 방법에 대해 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-118">[Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md) described how the Web Publishing Pipeline (WPP) provides a set of MSBuild targets that extend the functionality of MSBuild and enable it to integrate with the Internet Information Services (IIS) Web Deployment Tool (Web Deploy).</span></span> <span data-ttu-id="39c2c-119">웹 응용 프로그램 프로젝트를 패키지할 때 WPP 대상을 호출 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-119">When you package a web application project, you're invoking WPP targets.</span></span>

<span data-ttu-id="39c2c-120">이러한 많은 WPP 대상에는 **EnablePackageProcessLoggingAndAssert** 속성이 **true**로 설정 된 경우 추가 정보를 기록 하는 조건부 논리가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-120">Lots of these WPP targets include conditional logic that logs additional information when the **EnablePackageProcessLoggingAndAssert** property is set to **true**.</span></span> <span data-ttu-id="39c2c-121">예를 들어 **패키지** 대상을 검토 하는 경우 추가 로그 디렉터리를 만들고 **EnablePackageProcessLoggingAndAssert** 가 **true**인 경우 텍스트 파일에 파일 목록을 기록 하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-121">For example, if you review the **Package** target, you can see that it creates an additional log directory and writes a list of files to a text file if **EnablePackageProcessLoggingAndAssert** is equal to **true**.</span></span>

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample1.xml)]

> [!NOTE]
> <span data-ttu-id="39c2c-122">WPP 대상은% PROGRAMFILES (x86)% \ MSBuild\Microsoft\VisualStudio\v10.0\Web 폴더에 있는 *Microsoft .targets* 파일에 정의 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-122">The WPP targets are defined in the *Microsoft.Web.Publishing.targets* file in the %PROGRAMFILES(x86)%\MSBuild\Microsoft\VisualStudio\v10.0\Web folder.</span></span> <span data-ttu-id="39c2c-123">이 파일을 열고 Visual Studio 2010 또는 모든 XML 편집기에서 대상을 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-123">You can open this file and review the targets in Visual Studio 2010 or any XML editor.</span></span> <span data-ttu-id="39c2c-124">파일의 내용을 수정 하지 않도록 주의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="39c2c-124">Take care not to modify the contents of the file.</span></span>

## <a name="enabling-the-additional-logging"></a><span data-ttu-id="39c2c-125">추가 로깅 사용</span><span class="sxs-lookup"><span data-stu-id="39c2c-125">Enabling the Additional Logging</span></span>

<span data-ttu-id="39c2c-126">프로젝트를 빌드하는 방법에 따라 다양 한 방법으로 **EnablePackageProcessLoggingAndAssert** 속성에 대 한 값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-126">You can supply a value for the **EnablePackageProcessLoggingAndAssert** property in various ways, depending on how you build your project.</span></span>

<span data-ttu-id="39c2c-127">명령줄에서 프로젝트를 빌드하는 경우 명령줄 인수로 **EnablePackageProcessLoggingAndAssert** 속성에 대 한 값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-127">If you build your project from the command line, you can supply a value for the **EnablePackageProcessLoggingAndAssert** property as a command-line argument:</span></span>

[!code-console[Main](troubleshooting-the-packaging-process/samples/sample2.cmd)]

<span data-ttu-id="39c2c-128">사용자 지정 프로젝트 파일을 사용 하 여 프로젝트를 빌드하는 경우 **MSBuild** 작업의 **Properties** 특성에 **EnablePackageProcessLoggingAndAssert** 값을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-128">If you're using a custom project file to build your projects, you can include the **EnablePackageProcessLoggingAndAssert** value in the **Properties** attribute of the **MSBuild** task:</span></span>

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample3.xml)]

<span data-ttu-id="39c2c-129">Team Foundation Server (TFS) 빌드 정의를 사용 하 여 프로젝트를 빌드하는 경우 **MSBuild 인수** 행에서 **EnablePackageProcessLoggingAndAssert** 속성에 대 한 값을 제공할 수 있습니다.![](troubleshooting-the-packaging-process/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="39c2c-129">If you're using a Team Foundation Server (TFS) build definition to build your projects, you can supply a value for the **EnablePackageProcessLoggingAndAssert** property in the **MSBuild Arguments** row:![](troubleshooting-the-packaging-process/_static/image1.png)</span></span>

> [!NOTE]
> <span data-ttu-id="39c2c-130">빌드 정의를 만들고 구성 하는 방법에 대 한 자세한 내용은 [배포를 지 원하는 빌드 정의 만들기](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="39c2c-130">For more information on creating and configuring build definitions, see [Creating a Build Definition That Supports Deployment](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md).</span></span>

<span data-ttu-id="39c2c-131">또는 모든 빌드에서 패키지를 포함 하려는 경우 웹 응용 프로그램 프로젝트에 대 한 프로젝트 파일을 수정 하 여 **EnablePackageProcessLoggingAndAssert** 속성을 **true**로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-131">Alternatively, if you want to include the package in every build, you can modify the project file for your web application project to set the **EnablePackageProcessLoggingAndAssert** property to **true**.</span></span> <span data-ttu-id="39c2c-132">.Csproj 또는 .vbproj 파일 내의 첫 번째 **PropertyGroup** 요소에 속성을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-132">You should add the property to the first **PropertyGroup** element within your .csproj or .vbproj file.</span></span>

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample4.xml)]

## <a name="reviewing-the-log-files"></a><span data-ttu-id="39c2c-133">로그 파일 검토</span><span class="sxs-lookup"><span data-stu-id="39c2c-133">Reviewing the Log Files</span></span>

<span data-ttu-id="39c2c-134">**EnablePackageProcessLoggingAndAssert** 가 **true**로 설정 된 웹 응용 프로그램 프로젝트를 빌드하고 패키지할 경우 MSBuild는 *ProjectName*\_package 폴더에 Log 라는 추가 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-134">When you build and package a web application project with **EnablePackageProcessLoggingAndAssert** set to **true**, MSBuild creates an additional folder named Log in the *ProjectName*\_Package folder.</span></span> <span data-ttu-id="39c2c-135">로그 폴더는 다음과 같은 다양 한 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-135">The Log folder contains various files:</span></span>

![](troubleshooting-the-packaging-process/_static/image2.png)

<span data-ttu-id="39c2c-136">표시 되는 파일 목록은 프로젝트의 항목 및 빌드 프로세스에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-136">The list of files that you see will vary according to the things in your project and your build process.</span></span> <span data-ttu-id="39c2c-137">그러나 이러한 파일은 일반적으로 프로세스의 다양 한 단계에서, WPP가 패키징을 위해 수집 하는 파일 목록을 기록 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-137">However, these files are typically used to record the list of files that the WPP is collecting for packaging, at various stages of the process:</span></span>

- <span data-ttu-id="39c2c-138">*PreExcludePipelineCollectFilesPhaseFileList* 파일은 제외에 지정 된 파일이 제거 되기 전에 MSBuild가 패키징을 수집 하는 파일을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-138">The *PreExcludePipelineCollectFilesPhaseFileList.txt* file lists the files that MSBuild collects for packaging before any files that are specified for exclusion are removed.</span></span>
- <span data-ttu-id="39c2c-139">*AfterExcludeFilesFilesList* 파일에는 제외 하도록 지정 된 파일이 제거 된 후 수정 된 파일 목록이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-139">The *AfterExcludeFilesFilesList.txt* file contains the modified file list after any files that are specified for exclusion are removed.</span></span>

    > [!NOTE]
    > <span data-ttu-id="39c2c-140">패키징 프로세스에서 파일 및 폴더를 제외 하는 방법에 대 한 자세한 내용은 [배포에서 파일 및 폴더 제외](excluding-files-and-folders-from-deployment.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="39c2c-140">For more information on excluding files and folders from the packaging process, see [Excluding Files and Folders from Deployment](excluding-files-and-folders-from-deployment.md).</span></span>
- <span data-ttu-id="39c2c-141">*AfterTransformWebConfig* 파일에는 *web.config* 변환이 수행 된 후 패키징을 위해 수집 된 파일이 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-141">The *AfterTransformWebConfig.txt* file lists the files collected for packaging after any *Web.config* transforms have been performed.</span></span> <span data-ttu-id="39c2c-142">이 목록에서 *web.config* 및 *web.config*와 같은 구성 관련 *web.config* 변환 파일은 패키징을 위해 파일 목록에서 제외 됩니다 (예:</span><span class="sxs-lookup"><span data-stu-id="39c2c-142">In this list, any configuration-specific *Web.config* transform files, like *Web.Debug.config* and *Web.Release.config*, are excluded from the list of files for packaging.</span></span> <span data-ttu-id="39c2c-143">*변환 된 단일 web.config가* 해당 자리에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-143">A single transformed *Web.config* is included in their place.</span></span>
- <span data-ttu-id="39c2c-144">*PostAutoParameterizationWebConfigConnectionStrings* *파일에는 web.config 파일의* 연결 문자열이 매개 변수화 된 후의 파일 목록이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-144">The *PostAutoParameterizationWebConfigConnectionStrings.txt* file contains the list of files after the connection strings in the *Web.config* file have been parameterized.</span></span> <span data-ttu-id="39c2c-145">이 프로세스를 통해 패키지를 배포할 때 대상 환경에 대 한 적절 한 설정으로 연결 문자열을 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-145">This is the process that lets you replace your connection strings with the right settings for your target environment when you deploy the package.</span></span>
- <span data-ttu-id="39c2c-146">*Prepackage* 파일에는 패키지에 포함할 완성 된 빌드 전 파일 목록이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-146">The *Prepackage.txt* file contains the finalized pre-build list of files to be included in the package.</span></span>

> [!NOTE]
> <span data-ttu-id="39c2c-147">추가 로그 파일의 이름은 일반적으로 WPP 대상에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-147">The names of the additional log files typically correspond to WPP targets.</span></span> <span data-ttu-id="39c2c-148">% PROGRAMFILES (x86)% \ MSBuild\Microsoft\VisualStudio\v10.0\Web 폴더에 있는 *Microsoft* .targets 파일을 검사 하 여 이러한 대상을 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-148">You can review these targets by examining the *Microsoft.Web.Publishing.targets* file in the %PROGRAMFILES(x86)%\MSBuild\Microsoft\VisualStudio\v10.0\Web folder.</span></span>

<span data-ttu-id="39c2c-149">웹 패키지의 내용이 예상과 다른 경우에는 이러한 파일을 검토 하 여 어떤 상황이 발생 했는지 확인 하는 것이 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-149">If the contents of your web package aren't what you expected, reviewing these files can be a useful way to identify at what point in the process things went wrong.</span></span>

## <a name="conclusion"></a><span data-ttu-id="39c2c-150">결론</span><span class="sxs-lookup"><span data-stu-id="39c2c-150">Conclusion</span></span>

<span data-ttu-id="39c2c-151">이 항목에서는 MSBuild에서 **EnablePackageProcessLoggingAndAssert** 속성을 사용 하 여 패키징 프로세스의 문제를 해결 하는 방법에 대해 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-151">This topic described how you can use the **EnablePackageProcessLoggingAndAssert** property in MSBuild to troubleshoot the packaging process.</span></span> <span data-ttu-id="39c2c-152">빌드 프로세스에 속성 값을 제공할 수 있는 다양 한 방법과 속성을 **true**로 설정할 때 기록 되는 추가 정보에 대해 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="39c2c-152">It explained the different ways in which you can supply the property value to the build process, and it described the additional information that is recorded when you set the property to **true**.</span></span>

## <a name="further-reading"></a><span data-ttu-id="39c2c-153">추가 참고 자료</span><span class="sxs-lookup"><span data-stu-id="39c2c-153">Further Reading</span></span>

<span data-ttu-id="39c2c-154">사용자 지정 MSBuild 프로젝트 파일을 사용 하 여 배포 프로세스를 제어 하는 방법에 대 한 자세한 내용은 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md) 및 [빌드 프로세스 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="39c2c-154">For more information on using custom MSBuild project files to control the deployment process, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span> <span data-ttu-id="39c2c-155">WPP 및 패키징 프로세스를 관리 하는 방법에 대 한 자세한 내용은 [웹 응용 프로그램 프로젝트 빌드 및 패키징](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="39c2c-155">For more information on the WPP and how it manages the packaging process, see [Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md).</span></span> <span data-ttu-id="39c2c-156">웹 배포 패키지에서 특정 파일 및 폴더를 제외 하는 방법에 대 한 지침은 [배포에서 파일 및 폴더 제외](excluding-files-and-folders-from-deployment.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="39c2c-156">For guidance on how to exclude specific files and folders from web deployment packages, see [Excluding Files and Folders from Deployment](excluding-files-and-folders-from-deployment.md).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="39c2c-157">이전</span><span class="sxs-lookup"><span data-stu-id="39c2c-157">Previous</span></span>](running-windows-powershell-scripts-from-msbuild-project-files.md)
