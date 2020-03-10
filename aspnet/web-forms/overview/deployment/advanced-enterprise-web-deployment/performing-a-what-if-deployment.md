---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
title: What If 배포 수행 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포) 및 V ...를 사용 하 여 ' what if ' (또는 시뮬레이션 된) 배포를 수행 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c711b453-01ac-4e65-a48c-93d99bf22e58
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
msc.type: authoredcontent
ms.openlocfilehash: 73a0e038cc0d4ebae0ffc8ed3fd2de4c9dad673c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510335"
---
# <a name="performing-a-what-if-deployment"></a><span data-ttu-id="0161b-103">“가상 시나리오” 배포 수행</span><span class="sxs-lookup"><span data-stu-id="0161b-103">Performing a "What If" Deployment</span></span>

<span data-ttu-id="0161b-104">[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="0161b-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="0161b-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="0161b-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="0161b-106">이 항목에서는 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포) 및 VSDBCMD를 사용 하 여 "가상으로" (또는 시뮬레이션 된) 배포를 수행 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-106">This topic describes how to perform "what if" (or simulated) deployments using the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) and VSDBCMD.</span></span> <span data-ttu-id="0161b-107">이렇게 하면 응용 프로그램을 실제로 배포 하기 전에 특정 대상 환경에서 배포 논리의 영향을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-107">This lets you determine the effects of your deployment logic on a particular target environment before you actually deploy your application.</span></span>

<span data-ttu-id="0161b-108">이 항목에서는 Fabrikam, i n c. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 기반으로 하는 일련의 자습서의 일부를 형성 합니다. 이 자습서 시리즈에서는 샘플 솔루션&#x2014;&#x2014;을 사용 [하 여](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)ASP.NET MVC 3 응용 프로그램, Windows Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 비롯 한 현실적인 복잡성의 웹 응용 프로그램을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-108">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="0161b-109">이러한 자습서의 핵심에 나오는 배포 방법은 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)에 설명 된 프로젝트 파일을 이해 하는 방법에 설명 되어 있습니다. 프로젝트 파일에 대 한 빌드 및 배포 프로세스는 모든&#x2014;대상 환경에 적용 되는 빌드 명령을 포함 하는 두 개의 프로젝트 파일과 환경 특정 빌드 및 배포 설정을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-109">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build and deployment process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="0161b-110">빌드 시 환경 관련 프로젝트 파일은 환경에 관계 없는 프로젝트 파일에 병합 되어 전체 빌드 명령 집합을 형성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-110">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="performing-a-what-if-deployment-for-web-packages"></a><span data-ttu-id="0161b-111">웹 패키지에 대 한 "What If" 배포 수행</span><span class="sxs-lookup"><span data-stu-id="0161b-111">Performing a "What If" Deployment for Web Packages</span></span>

<span data-ttu-id="0161b-112">웹 배포에는 "what if" (또는 평가판) 모드에서 배포를 수행할 수 있는 기능이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-112">Web Deploy includes functionality that lets you perform deployments in "what if" (or trial) mode.</span></span> <span data-ttu-id="0161b-113">"What if" 모드로 아티팩트를 배포 하는 경우 웹 배포는 배포를 수행 하는 것 처럼 로그 파일을 생성 하지만 실제로 대상 서버에서 아무것도 변경 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-113">When you deploy artifacts in "what if" mode, Web Deploy generates a log file as if you had performed the deployment, but it doesn't actually change anything on the destination server.</span></span> <span data-ttu-id="0161b-114">로그 파일을 검토 하면 특히 대상 서버에 대 한 배포의 영향을 이해 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-114">Reviewing the log file can help you to understand what impact your deployment will have on the destination server, in particular:</span></span>

- <span data-ttu-id="0161b-115">추가 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-115">What will get added.</span></span>
- <span data-ttu-id="0161b-116">업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-116">What will get updated.</span></span>
- <span data-ttu-id="0161b-117">삭제 될 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-117">What will get deleted.</span></span>

<span data-ttu-id="0161b-118">"What if" 배포는 실제로 대상 서버에서 어떤 것도 변경 하지 않기 때문에 항상 배포 성공 여부를 예측 하는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-118">Because a "what if" deployment doesn't actually change anything on the destination server, what it can't always do is predict whether a deployment will succeed.</span></span>

<span data-ttu-id="0161b-119">[웹 패키지 배포](../web-deployment-in-the-enterprise/deploying-web-packages.md)에 설명 된 대로, msdeploy.exe 명령줄 유틸리티를 직접 사용 하거나 빌드 프로세스&#x2014;에서 생성 하는 *.deploy .cmd* 파일을 실행 하 여 두 가지 방법으로 웹 배포를 사용 하 여 웹 패키지를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-119">As described in [Deploying Web Packages](../web-deployment-in-the-enterprise/deploying-web-packages.md), you can deploy web packages using Web Deploy in two ways&#x2014;by using the MSDeploy.exe command-line utility directly or by running the *.deploy.cmd* file that the build process generates.</span></span>

<span data-ttu-id="0161b-120">Msdeploy.exe를 직접 사용 하는 경우 명령에 **– whatif** 플래그를 추가 하 여 "what if" 배포를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-120">If you're using MSDeploy.exe directly, you can run a "what if" deployment by adding the **–whatif** flag to your command.</span></span> <span data-ttu-id="0161b-121">예를 들어 스테이징 환경에 배포 하는 경우에 발생 하는 결과를 평가 하기 위해 다음과 유사 하 게 Msdeploy.exe 명령이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-121">For example, to evaluate what would happen if you deployed the ContactManager.Mvc.zip package to a staging environment, the MSDeploy command should resemble this:</span></span>

[!code-console[Main](performing-a-what-if-deployment/samples/sample1.cmd)]

<span data-ttu-id="0161b-122">"What if" 배포 결과가 만족 스 러 우면 **– whatif** 플래그를 제거 하 여 라이브 배포를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-122">When you're satisfied with the results of your "what if" deployment, you can remove the **–whatif** flag to run a live deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="0161b-123">Msdeploy.exe의 명령줄 옵션에 대 한 자세한 내용은 [웹 배포 작업 설정](https://technet.microsoft.com/library/dd569089(WS.10).aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0161b-123">For more information on command-line options for MSDeploy.exe, see [Web Deploy Operation Settings](https://technet.microsoft.com/library/dd569089(WS.10).aspx).</span></span>

<span data-ttu-id="0161b-124">*. Deploy .cmd* 파일을 사용 하는 경우 명령에 **/y** 플래그 ("yes" 또는 업데이트 모드) 대신 **/t** 플래그 (평가판 모드) 플래그를 포함 하 여 "what if" 배포를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-124">If you're using the *.deploy.cmd* file, you can run a "what if" deployment by including the **/t** flag (trial mode) flag instead of the **/y** flag ("yes," or update mode) in your command.</span></span> <span data-ttu-id="0161b-125">예를 들어 .deploy 파일을 실행 하 여 *.* c a p. c a c .zip .zip 패키지를 배포한 경우 발생 하는 동작을 평가 하려면 명령이 다음과 유사 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-125">For example, to evaluate what would happen if you deployed the ContactManager.Mvc.zip package by running the *.deploy.cmd* file, your command should resemble this:</span></span>

[!code-console[Main](performing-a-what-if-deployment/samples/sample2.cmd)]

<span data-ttu-id="0161b-126">"평가 모드" 배포 결과에 만족 하는 경우 **/t** 플래그를 **/y** 플래그로 바꿔 라이브 배포를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-126">When you're satisfied with the results of your "trial mode" deployment, you can replace the **/t** flag with a **/y** flag to run a live deployment:</span></span>

[!code-console[Main](performing-a-what-if-deployment/samples/sample3.cmd)]

> [!NOTE]
> <span data-ttu-id="0161b-127">*. .Cmd* 파일을 사용 하는 명령줄 옵션에 대 한 자세한 내용은 [방법: 배포 파일을 사용 하 여 배포 패키지 설치](https://msdn.microsoft.com/library/ff356104.aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0161b-127">For more information on command-line options for *.deploy.cmd* files, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx).</span></span> <span data-ttu-id="0161b-128">플래그를 지정 하지 않고 *.deploy* 파일을 실행 하는 경우 명령 프롬프트에 사용 가능한 플래그의 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-128">If you run the *.deploy.cmd* file without specifying any flags, the command prompt will display a list of available flags.</span></span>

## <a name="performing-a-what-if-deployment-for-databases"></a><span data-ttu-id="0161b-129">데이터베이스에 대 한 "What If" 배포 수행</span><span class="sxs-lookup"><span data-stu-id="0161b-129">Performing a "What If" Deployment for Databases</span></span>

<span data-ttu-id="0161b-130">이 섹션에서는 VSDBCMD 유틸리티를 사용 하 여 증분 스키마 기반 데이터베이스 배포를 수행 하는 것으로 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-130">This section assumes that you're using the VSDBCMD utility to perform incremental, schema-based database deployment.</span></span> <span data-ttu-id="0161b-131">이 방법은 [데이터베이스 프로젝트 배포](../web-deployment-in-the-enterprise/deploying-database-projects.md)에 자세히 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-131">This approach is described in more detail in [Deploying Database Projects](../web-deployment-in-the-enterprise/deploying-database-projects.md).</span></span> <span data-ttu-id="0161b-132">여기에 설명 된 개념을 적용 하기 전에이 항목을 숙지 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-132">We recommend that you familiarize yourself with this topic before you apply the concepts described here.</span></span>

<span data-ttu-id="0161b-133">**배포** 모드에서 vsdbcmd를 사용 하는 경우 **/Dd** (또는 **/deploytodatabase**) 플래그를 사용 하 여 vsdbcmd에서 실제로 데이터베이스를 배포할지 아니면 배포 스크립트만 생성할지를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-133">When you use VSDBCMD in **Deploy** mode, you can use the **/dd** (or **/DeployToDatabase**) flag to control whether VSDBCMD actually deploys the database or just generates a deployment script.</span></span> <span data-ttu-id="0161b-134">.Dbschema 파일을 배포 하는 경우 다음과 같은 동작이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-134">If you're deploying a .dbschema file, this is the behavior:</span></span>

- <span data-ttu-id="0161b-135">**/Dd +** 또는 **/dd**을 지정 하는 경우 VSDBCMD는 배포 스크립트를 생성 하 고 데이터베이스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-135">If you specify **/dd+** or **/dd**, VSDBCMD will generate a deployment script and deploy the database.</span></span>
- <span data-ttu-id="0161b-136">**/Dd-** 를 지정 하거나 스위치를 생략 하면 VSDBCMD는 배포 스크립트만 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-136">If you specify **/dd-** or omit the switch, VSDBCMD will generate a deployment script only.</span></span>

> [!NOTE]
> <span data-ttu-id="0161b-137">.Dbschema 파일이 아닌 deploymanifest 파일을 배포 하는 경우 **/dd** 스위치의 동작은 훨씬 더 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-137">If you're deploying a .deploymanifest file rather than a .dbschema file, the behavior of the **/dd** switch is a lot more complicated.</span></span> <span data-ttu-id="0161b-138">기본적으로 deploymanifest 파일에는 값이 **True**인 **deploytodatabase** 요소가 포함 된 경우 **/dd** 스위치의 값을 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-138">Essentially, VSDBCMD will ignore the value of the **/dd** switch if the .deploymanifest file includes a **DeployToDatabase** element with a value of **True**.</span></span> <span data-ttu-id="0161b-139">[데이터베이스 프로젝트를 배포](../web-deployment-in-the-enterprise/deploying-database-projects.md) 하면이 동작이 전체적으로 설명 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-139">[Deploying Database Projects](../web-deployment-in-the-enterprise/deploying-database-projects.md) describes this behavior in full.</span></span>

<span data-ttu-id="0161b-140">예를 들어 데이터베이스를 실제로 배포 하지 않고 동료 **관리자** 데이터베이스에 대 한 배포 스크립트를 생성 하려면 VSDBCMD 명령이 다음과 유사 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-140">For example, to generate a deployment script for the **ContactManager** database without actually deploying the database, your VSDBCMD command should resemble this:</span></span>

[!code-console[Main](performing-a-what-if-deployment/samples/sample4.cmd)]

<span data-ttu-id="0161b-141">VSDBCMD는 차등 데이터베이스 배포 도구 이며, 현재 데이터베이스를 업데이트 하는 데 필요한 모든 SQL 명령 (있는 경우)을 지정 된 스키마에 포함 하기 위해 배포 스크립트가 동적으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-141">VSDBCMD is a differential database deployment tool, and as such the deployment script is dynamically generated to contain all the SQL commands necessary to update the current database, if one exists, to the specified schema.</span></span> <span data-ttu-id="0161b-142">배포 스크립트를 검토 하면 현재 데이터베이스와 해당 데이터베이스에 포함 된 데이터에 대 한 배포의 영향을 확인 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-142">Reviewing the deployment script is a useful way to determine what impact your deployment will have on the current database and the data it contains.</span></span> <span data-ttu-id="0161b-143">예를 들어 다음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-143">For example, you might want to determine:</span></span>

- <span data-ttu-id="0161b-144">기존 테이블을 제거할지 여부와이로 인해 데이터가 손실 될 수 있는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-144">Whether any existing tables will be removed, and whether that will result in data loss.</span></span>
- <span data-ttu-id="0161b-145">예를 들어 테이블을 분할 하거나 병합 하는 등의 작업 순서에서 데이터 손실 위험을 초래할 수 있는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-145">Whether the order of operations carries a risk of data loss, for example, if you're splitting or merging tables.</span></span>

<span data-ttu-id="0161b-146">배포 스크립트에 만족 하는 경우 **/dd +** 플래그로 VSDBCMD를 반복 하 여 변경 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-146">If you're happy with the deployment script, you can repeat the VSDBCMD with a **/dd+** flag to make the changes.</span></span> <span data-ttu-id="0161b-147">또는 요구 사항에 맞게 배포 스크립트를 편집한 다음 데이터베이스 서버에서 수동으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-147">Alternatively, you can edit the deployment script to meet your requirements and then execute it manually on the database server.</span></span>

## <a name="integrating-what-if-functionality-into-custom-project-files"></a><span data-ttu-id="0161b-148">"What If" 기능을 사용자 지정 프로젝트 파일에 통합</span><span class="sxs-lookup"><span data-stu-id="0161b-148">Integrating "What If" Functionality into Custom Project Files</span></span>

<span data-ttu-id="0161b-149">더 복잡 한 배포 시나리오에서는 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)에 설명 된 대로 사용자 지정 MSBuild (Microsoft Build Engine) 프로젝트 파일을 사용 하 여 빌드 및 배포 논리를 캡슐화 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-149">In more complex deployment scenarios, you'll want to use a custom Microsoft Build Engine (MSBuild) project file to encapsulate your build and deployment logic, as described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md).</span></span> <span data-ttu-id="0161b-150">예를 들어 [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) 샘플 솔루션에서 proj 파일을 *게시* 합니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-150">For example, in the [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) sample solution, the *Publish.proj* file:</span></span>

- <span data-ttu-id="0161b-151">솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-151">Builds the solution.</span></span>
- <span data-ttu-id="0161b-152">에서는 웹 배포를 사용 하 여 배포 된 응용 프로그램을 패키지 하 고 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-152">Uses Web Deploy to package and deploy the ContactManager.Mvc application.</span></span>
- <span data-ttu-id="0161b-153">에서는 웹 배포를 사용 하 여 서비스 응용 프로그램을 패키지 하 고 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-153">Uses Web Deploy to package and deploy the ContactManager.Service application.</span></span>
- <span data-ttu-id="0161b-154">는 **연락처 관리자** 데이터베이스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-154">Deploys the **ContactManager** database.</span></span>

<span data-ttu-id="0161b-155">이러한 방식으로 여러 웹 패키지 및/또는 데이터베이스의 배포를 단일 단계 프로세스에 통합 하는 경우 "what if" 모드로 전체 배포를 수행 하는 옵션을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-155">When you integrate the deployment of multiple web packages and/or databases into a single-step process in this way, you may also want the option of performing the entire deployment in a "what if" mode.</span></span>

<span data-ttu-id="0161b-156">*Publish. proj* 파일은이 작업을 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-156">The *Publish.proj* file demonstrates how you can do this.</span></span> <span data-ttu-id="0161b-157">먼저 "what if" 값을 저장할 속성을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-157">First, you need to create a property to store the "what if" value:</span></span>

[!code-xml[Main](performing-a-what-if-deployment/samples/sample5.xml)]

<span data-ttu-id="0161b-158">이 경우 기본값 **false**로 **WhatIf** 라는 속성을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-158">In this case, you've created a property named **WhatIf** with a default value of **false**.</span></span> <span data-ttu-id="0161b-159">사용자는 명령줄 매개 변수에서 속성을 **true** 로 설정 하 여이 값을 재정의할 수 있습니다. 잠시 후에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-159">Users can override this value by setting the property to **true** in a command-line parameter, as you'll see shortly.</span></span>

<span data-ttu-id="0161b-160">다음 단계는 플래그에 **WhatIf** 속성 값이 반영 되도록 모든 웹 배포 및 VSDBCMD 명령을 매개 변수화 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-160">The next stage is to parameterize any Web Deploy and VSDBCMD commands so that the flags reflect the **WhatIf** property value.</span></span> <span data-ttu-id="0161b-161">예를 들어, 다음 대상 ( *Publish. proj* 파일 및 간소화)은 *. .deploy* 파일을 실행 하 여 웹 패키지를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-161">For example, the next target (taken from the *Publish.proj* file and simplified) runs the *.deploy.cmd* file to deploy a web package.</span></span> <span data-ttu-id="0161b-162">기본적으로이 명령은 **/y** 스위치 ("예" 또는 업데이트 모드)를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-162">By default, the command includes a **/Y** switch ("yes," or update mode).</span></span> <span data-ttu-id="0161b-163">**WhatIf** 를 **true**로 설정 하면 **/t** 스위치 (평가판 또는 "what if" 모드)로 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-163">If **WhatIf** is set to **true**, this is replaced by a **/T** switch (trial, or "what if" mode).</span></span>

[!code-xml[Main](performing-a-what-if-deployment/samples/sample6.xml)]

<span data-ttu-id="0161b-164">마찬가지로 다음 대상은 VSDBCMD 유틸리티를 사용 하 여 데이터베이스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-164">Similarly, the next target uses the VSDBCMD utility to deploy a database.</span></span> <span data-ttu-id="0161b-165">기본적으로 **/dd** 스위치는 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-165">By default, a **/dd** switch is not included.</span></span> <span data-ttu-id="0161b-166">즉, VSDBCMD는 배포 스크립트를 생성 하지만 데이터베이스&#x2014;를 배포 하지 않습니다. 즉, "what if" 시나리오를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-166">This means that VSDBCMD will generate a deployment script but will not deploy the database&#x2014;in other words, a "what if" scenario.</span></span> <span data-ttu-id="0161b-167">**WhatIf** 속성이 **true**로 설정 되어 있지 않으면 **/DD** 스위치가 추가 되 고 VSDBCMD가 데이터베이스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-167">If the **WhatIf** property is not set to **true**, a **/dd** switch is added and VSDBCMD will deploy the database.</span></span>

[!code-xml[Main](performing-a-what-if-deployment/samples/sample7.xml)]

<span data-ttu-id="0161b-168">동일한 방법을 사용 하 여 프로젝트 파일의 모든 관련 명령을 매개 변수화 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-168">You can use the same approach to parameterize all the relevant commands in your project file.</span></span> <span data-ttu-id="0161b-169">"What if" 배포를 실행 하려는 경우 명령줄에서 **WhatIf** 속성 값을 제공 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-169">When you want to run a "what if" deployment, you can then simply provide a **WhatIf** property value from the command line:</span></span>

[!code-console[Main](performing-a-what-if-deployment/samples/sample8.cmd)]

<span data-ttu-id="0161b-170">이러한 방식으로 모든 프로젝트 구성 요소에 대 한 "가상의 경우" 배포를 한 번에 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-170">In this way, you can run a "what if" deployment for all your project components in a single step.</span></span>

## <a name="conclusion"></a><span data-ttu-id="0161b-171">결론</span><span class="sxs-lookup"><span data-stu-id="0161b-171">Conclusion</span></span>

<span data-ttu-id="0161b-172">이 항목에서는 웹 배포, VSDBCMD 및 MSBuild를 사용 하 여 "what if" 배포를 실행 하는 방법에 대해 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-172">This topic described how to run "what if" deployments using Web Deploy, VSDBCMD, and MSBuild.</span></span> <span data-ttu-id="0161b-173">"어떻게 할까요?" 배포를 사용 하면 대상 환경을 변경 하기 전에 제안 된 배포의 영향을 평가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0161b-173">A "what if" deployment lets you evaluate the impact of a proposed deployment before you actually make any changes to the destination environment.</span></span>

## <a name="further-reading"></a><span data-ttu-id="0161b-174">추가 참고 자료</span><span class="sxs-lookup"><span data-stu-id="0161b-174">Further Reading</span></span>

<span data-ttu-id="0161b-175">웹 배포 명령줄 구문에 대 한 자세한 내용은 [웹 배포 작업 설정](https://technet.microsoft.com/library/dd569089(WS.10).aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0161b-175">For more information on Web Deploy command-line syntax, see [Web Deploy Operation Settings](https://technet.microsoft.com/library/dd569089(WS.10).aspx).</span></span> <span data-ttu-id="0161b-176">*. Deploy .cmd* 파일을 사용 하는 경우 명령줄 옵션에 대 한 지침은 [방법: 배포 파일을 사용 하 여 배포 패키지 설치](https://msdn.microsoft.com/library/ff356104.aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0161b-176">For guidance on command-line options when you use the *.deploy.cmd* file, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx).</span></span> <span data-ttu-id="0161b-177">VSDBCMD 명령줄 구문에 대 한 지침은 [vsdbcmd에 대 한 명령줄 참조를 참조 하세요. EXE (배포 및 스키마 가져오기)](https://msdn.microsoft.com/library/dd193283.aspx)</span><span class="sxs-lookup"><span data-stu-id="0161b-177">For guidance on VSDBCMD command-line syntax, see [Command-Line Reference for VSDBCMD.EXE (Deployment and Schema Import)](https://msdn.microsoft.com/library/dd193283.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0161b-178">[이전](advanced-enterprise-web-deployment.md)
> [다음](customizing-database-deployments-for-multiple-environments.md)</span><span class="sxs-lookup"><span data-stu-id="0161b-178">[Previous](advanced-enterprise-web-deployment.md)
[Next](customizing-database-deployments-for-multiple-environments.md)</span></span>
