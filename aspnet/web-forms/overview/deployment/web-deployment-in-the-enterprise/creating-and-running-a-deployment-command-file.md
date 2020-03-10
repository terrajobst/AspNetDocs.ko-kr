---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
title: 배포 명령 파일 만들기 및 실행 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 Microsoft Build Engine (MSBuild) 프로젝트 파일을 사용 하 여 배포를 단일 단계로 실행 하는 데 사용할 수 있는 명령 파일을 빌드하는 방법에 대해 설명 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c61560e9-9f6c-4985-834a-08a3eabf9c3c
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
msc.type: authoredcontent
ms.openlocfilehash: f1477ff423e4898385066a35b42503f3c70dcc68
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78514979"
---
# <a name="creating-and-running-a-deployment-command-file"></a><span data-ttu-id="04156-103">배포 명령 파일 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="04156-103">Creating and Running a Deployment Command File</span></span>

<span data-ttu-id="04156-104">[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="04156-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="04156-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="04156-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="04156-106">이 항목에서는 Microsoft Build Engine (MSBuild) 프로젝트 파일을 사용 하 여 반복 가능한 단일 프로세스로 배포를 실행할 수 있는 명령 파일을 빌드하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="04156-106">This topic describes how to build a command file that will let you run a deployment using Microsoft Build Engine (MSBuild) project files as a single-step, repeatable process.</span></span>

<span data-ttu-id="04156-107">이 항목에서는 Fabrikam, i n c. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 기반으로 하는 일련의 자습서의 일부를 형성 합니다. 이 자습서 [시리즈에서는 샘플](the-contact-manager-solution.md) 솔루션&#x2014;&#x2014;을 사용 하 여 ASP.NET MVC 3 응용 프로그램, Windows Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 비롯 한 현실적인 복잡성의 웹 응용 프로그램을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="04156-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager](the-contact-manager-solution.md) solution&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="04156-108">이러한 자습서의 핵심에 나오는 배포 방법은 빌드&#x2014; [프로세스 이해](understanding-the-build-process.md)에서 설명 하는 빌드 프로세스 이해에 설명 된 분할 프로젝트 파일 방식을 기반으로 합니다. 빌드 프로세스는 모든 대상 환경에 적용 되는 빌드 명령을 포함 하 고 다른 하나는 환경 특정 빌드 및 배포 설정을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="04156-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Build Process](understanding-the-build-process.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="04156-109">빌드 시 환경 관련 프로젝트 파일은 환경에 관계 없는 프로젝트 파일에 병합 되어 전체 빌드 명령 집합을 형성 합니다.</span><span class="sxs-lookup"><span data-stu-id="04156-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="process-overview"></a><span data-ttu-id="04156-110">프로세스 개요</span><span class="sxs-lookup"><span data-stu-id="04156-110">Process Overview</span></span>

<span data-ttu-id="04156-111">이 항목에서는 이러한 프로젝트 파일을 사용 하 여 대상 환경에 반복 가능한 배포를 수행 하는 명령 파일을 만들고 실행 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="04156-111">In this topic, you'll learn how to create and run a command file that uses these project files to perform a repeatable deployment to your target environment.</span></span> <span data-ttu-id="04156-112">기본적으로 명령 파일에는 다음을 수행 하는 MSBuild 명령만 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04156-112">Essentially, the command file simply needs to contain an MSBuild command that:</span></span>

- <span data-ttu-id="04156-113">MSBuild에 환경 독립적 *게시 proj* 파일을 실행 하도록 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="04156-113">Tells MSBuild to execute the environment-agnostic *Publish.proj* file.</span></span>
- <span data-ttu-id="04156-114">환경 관련 프로젝트 설정 및 찾을 위치를 포함 하는 파일을 *Publish. proj* 파일에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="04156-114">Tells the *Publish.proj* file which file contains the environment-specific project settings and where to find it.</span></span>

## <a name="create-an-msbuild-command"></a><span data-ttu-id="04156-115">MSBuild 명령 만들기</span><span class="sxs-lookup"><span data-stu-id="04156-115">Create an MSBuild Command</span></span>

<span data-ttu-id="04156-116">[빌드 프로세스 이해](understanding-the-build-process.md)에 설명 된&#x2014;대로 환경 관련 프로젝트 파일 (예: *Env)* &#x2014;은 빌드 시 환경 독립적인 *Publish proj* 파일로 가져오도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="04156-116">As described in [Understanding the Build Process](understanding-the-build-process.md), the environment-specific project file&#x2014;for example, *Env-Dev.proj*&#x2014;is designed to be imported into the environment-agnostic *Publish.proj* file at build time.</span></span> <span data-ttu-id="04156-117">이러한 두 파일은 모두 MSBuild에서 솔루션을 빌드하고 배포 하는 방법을 알려 주는 전체 명령 집합을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="04156-117">Together, these two files provide a complete set of instructions that tell MSBuild how to build and deploy your solution.</span></span>

<span data-ttu-id="04156-118">*Publish. proj* 파일은 **import** 요소를 사용 하 여 환경 관련 프로젝트 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="04156-118">The *Publish.proj* file uses an **Import** element to import the environment-specific project file.</span></span>

[!code-xml[Main](creating-and-running-a-deployment-command-file/samples/sample1.xml)]

<span data-ttu-id="04156-119">따라서 Msbuild.exe를 사용 하 여 Contact Manager 솔루션을 빌드 및 배포 하는 경우 다음을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04156-119">As such, when you use MSBuild.exe to build and deploy the Contact Manager solution, you need to:</span></span>

- <span data-ttu-id="04156-120">*Publish. proj* 파일에서 msbuild.exe를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="04156-120">Run MSBuild.exe on the *Publish.proj* file.</span></span>
- <span data-ttu-id="04156-121">**TargetEnvPropsFile**라는 명령줄 매개 변수를 제공 하 여 환경 관련 프로젝트 파일의 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="04156-121">Specify the location of the environment-specific project file by supplying a command-line parameter named **TargetEnvPropsFile**.</span></span>

<span data-ttu-id="04156-122">이렇게 하려면 MSBuild 명령이 다음과 유사 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04156-122">To do this, your MSBuild command should resemble this:</span></span>

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample2.cmd)]

<span data-ttu-id="04156-123">여기에서 반복 가능한 단일 단계 배포로 이동 하는 간단한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="04156-123">From here, it's a simple step to move to a repeatable, single-step deployment.</span></span> <span data-ttu-id="04156-124">MSBuild 명령을 .cmd 파일에 추가 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04156-124">All you need to do is to add your MSBuild command to a .cmd file.</span></span> <span data-ttu-id="04156-125">Contact Manager 솔루션에서 Publish 폴더에는이를 수행 하는 *Publish-Dev* 라는 파일이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04156-125">In the Contact Manager solution, the Publish folder includes a file named *Publish-Dev.cmd* that does exactly this.</span></span>

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample3.cmd)]

> [!NOTE]
> <span data-ttu-id="04156-126">**/Sfl** 스위치는 msbuild.exe가 호출 된 작업 디렉터리에 *msbuild.exe* 라는 로그 파일을 만들도록 msbuild에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="04156-126">The **/fl** switch instructs MSBuild to create a log file named *msbuild.log* in the working directory in which MSBuild.exe was invoked.</span></span>

<span data-ttu-id="04156-127">Contact Manager 솔루션을 배포 하거나 다시 배포 하려면 *Publish-Dev* 파일을 실행 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04156-127">To deploy or redeploy the Contact Manager solution, all you need to do is run the *Publish-Dev.cmd* file.</span></span> <span data-ttu-id="04156-128">이 파일을 실행 하면 MSBuild에서 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="04156-128">When you run the file, MSBuild will:</span></span>

- <span data-ttu-id="04156-129">솔루션의 모든 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="04156-129">Build all the projects in the solution.</span></span>
- <span data-ttu-id="04156-130">웹 응용 프로그램 프로젝트용 배포 가능한 웹 패키지를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="04156-130">Generate deployable web packages for the web application projects.</span></span>
- <span data-ttu-id="04156-131">데이터베이스 프로젝트용 .dbschema 및 deploymanifest 파일을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="04156-131">Generate .dbschema and .deploymanifest files for the database projects.</span></span>
- <span data-ttu-id="04156-132">웹 서버에 웹 패키지를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="04156-132">Deploy the web packages to the web server.</span></span>
- <span data-ttu-id="04156-133">데이터베이스 서버에 데이터베이스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="04156-133">Deploy the database to the database server.</span></span>

## <a name="run-the-deployment"></a><span data-ttu-id="04156-134">배포 실행</span><span class="sxs-lookup"><span data-stu-id="04156-134">Run the Deployment</span></span>

<span data-ttu-id="04156-135">대상 환경에 대 한 명령 파일을 만든 경우 파일을 실행 하 여 전체 배포를 완료할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04156-135">When you've created a command file for your target environment, you should be able to complete the entire deployment by simply running the file.</span></span>

<span data-ttu-id="04156-136">**테스트 환경에 연락처 관리자 솔루션을 배포 하려면**</span><span class="sxs-lookup"><span data-stu-id="04156-136">**To deploy the Contact Manager solution to your test environment**</span></span>

1. <span data-ttu-id="04156-137">개발자 워크스테이션에서 Windows 탐색기를 연 다음 *Publish-Dev* 파일의 위치로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="04156-137">On your developer workstation, open Windows Explorer, and then browse to the location of the *Publish-Dev.cmd* file.</span></span>
2. <span data-ttu-id="04156-138">파일을 두 번 클릭 하 여 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="04156-138">Double-click the file to run it.</span></span>
3. <span data-ttu-id="04156-139">**파일 열기 – 보안 경고** 대화 상자가 나타나면 **실행**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="04156-139">If an **Open File – Security Warning** dialog box appears, click **Run**.</span></span>
4. <span data-ttu-id="04156-140">구성 설정 및 테스트 서버가 올바르게 설정 된 경우 MSBuild가 프로젝트 파일 처리를 완료 하면 명령 프롬프트 창에 **빌드 성공** 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04156-140">If your configuration settings and test servers are set up correctly, the Command Prompt window will show a **Build succeeded** message when MSBuild has finished processing the project files.</span></span>

    ![](creating-and-running-a-deployment-command-file/_static/image1.png)
5. <span data-ttu-id="04156-141">이 환경에 솔루션을 처음 배포 하는 경우에는 테스트 웹 서버 컴퓨터 **\_계정을 datawriter 여부** 및 **db\_** **데이터베이스에 추가 해야 합니다** .</span><span class="sxs-lookup"><span data-stu-id="04156-141">If this is the first time you've deployed the solution to this environment, you'll need to add the test web server machine account to the **db\_datawriter** and **db\_datareader** roles on the **ContactManager** database.</span></span> <span data-ttu-id="04156-142">이 절차는 [웹 배포 게시용 데이터베이스 서버 구성](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md)에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04156-142">This procedure is described in [Configure a Database Server for Web Deploy Publishing](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="04156-143">데이터베이스를 만들 때에만 이러한 권한을 할당 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04156-143">You only need to assign these permissions when you create the database.</span></span> <span data-ttu-id="04156-144">기본적으로 빌드 프로세스는 모든 배포&#x2014;에서 데이터베이스를 다시 만들지 않고 기존 데이터베이스와 최신 스키마를 비교 하 고 필요한 변경만 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="04156-144">By default, the build process will not recreate the database on every deployment&#x2014;instead, it will compare the existing database to the latest schema and make only the changes required.</span></span> <span data-ttu-id="04156-145">따라서 솔루션을 처음 배포할 때에만 이러한 데이터베이스 역할을 매핑해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04156-145">As a result, you should only need to map these database roles the first time you deploy the solution.</span></span>
6. <span data-ttu-id="04156-146">Internet Explorer를 열고 연락처 관리자 응용 프로그램의 URL로 이동 합니다 (예: `http://testweb1:85/ContactManager/`).</span><span class="sxs-lookup"><span data-stu-id="04156-146">Open Internet Explorer and browse to the URL of the Contact Manager application (for example, `http://testweb1:85/ContactManager/`).</span></span>
7. <span data-ttu-id="04156-147">응용 프로그램이 예상 대로 작동 하 고 연락처를 추가할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="04156-147">Verify that the application works as expected and you're able to add contacts.</span></span>

    ![](creating-and-running-a-deployment-command-file/_static/image2.png)

## <a name="conclusion"></a><span data-ttu-id="04156-148">결론</span><span class="sxs-lookup"><span data-stu-id="04156-148">Conclusion</span></span>

<span data-ttu-id="04156-149">MSBuild 지침을 포함 하는 명령 파일을 만들면 특정 대상 환경에 다중 프로젝트 솔루션을 빌드하고 배포 하는 빠르고 쉬운 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="04156-149">Creating a command file containing your MSBuild instructions provides you with a quick and easy way of building and deploying a multi-project solution to a specific destination environment.</span></span> <span data-ttu-id="04156-150">여러 대상 환경에 솔루션을 반복적으로 배포 해야 하는 경우 여러 명령 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04156-150">If you need to repeatedly deploy your solution to multiple destination environments, you can create multiple command files.</span></span> <span data-ttu-id="04156-151">각 명령 파일에서 MSBuild 명령은 동일한 유니버설 프로젝트 파일을 만들지만 다른 환경 특정 프로젝트 파일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="04156-151">In each command file, the MSBuild command will build the same universal project file, but it will specify a different environment-specific project file.</span></span> <span data-ttu-id="04156-152">예를 들어 개발자 또는 테스트 환경에 게시 하는 명령 파일에는 다음 MSBuild 명령이 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04156-152">For example, a command file to publish to a developer or test environment might contain this MSBuild command:</span></span>

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample4.cmd)]

<span data-ttu-id="04156-153">스테이징 환경에 게시할 명령 파일에는 다음 MSBuild 명령이 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04156-153">A command file to publish to a staging environment might contain this MSBuild command:</span></span>

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample5.cmd)]

> [!NOTE]
> <span data-ttu-id="04156-154">사용자의 서버 환경에 맞는 환경 관련 프로젝트 파일을 사용자 지정 하는 방법에 대 한 지침은 [대상 환경에 대 한 배포 속성 구성](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="04156-154">For guidance on how to customize the environment-specific project files for your own server environments, see [Configure Deployment Properties for a Target Environment](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).</span></span>

<span data-ttu-id="04156-155">MSBuild 명령의 속성을 재정의 하거나 다양 한 다른 스위치를 설정 하 여 각 환경에 대 한 빌드 프로세스를 사용자 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04156-155">You can also customize the build process for each environment by overriding properties or setting various other switches in your MSBuild command.</span></span> <span data-ttu-id="04156-156">자세한 내용은 [MSBuild 명령줄 참조](https://msdn.microsoft.com/library/ms164311.aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="04156-156">For more information, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="04156-157">[이전](deploying-database-projects.md)
> [다음](manually-installing-web-packages.md)</span><span class="sxs-lookup"><span data-stu-id="04156-157">[Previous](deploying-database-projects.md)
[Next](manually-installing-web-packages.md)</span></span>
