---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment
title: 배포를 지 원하는 빌드 정의 만들기 | Microsoft Docs
author: jrjlee
description: Team Foundation Server (TFS) 2010에서 모든 종류의 빌드를 수행 하려면 팀 프로젝트 내에서 빌드 정의를 만들어야 합니다. 이 항목의 내용
ms.author: riande
ms.date: 05/04/2012
ms.assetid: fe47a018-f6d0-4979-80e7-5b1fa75a5865
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment
msc.type: authoredcontent
ms.openlocfilehash: e11c91a824446572aaf0b3bc6954b9b8ffb4eaff
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78489011"
---
# <a name="creating-a-build-definition-that-supports-deployment"></a><span data-ttu-id="c646a-104">배포를 지원하는 빌드 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="c646a-104">Creating a Build Definition That Supports Deployment</span></span>

<span data-ttu-id="c646a-105">[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="c646a-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="c646a-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="c646a-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="c646a-107">Team Foundation Server (TFS) 2010에서 모든 종류의 빌드를 수행 하려면 팀 프로젝트 내에서 빌드 정의를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-107">If you want to perform any kind of build in Team Foundation Server (TFS) 2010, you need to create a build definition within your team project.</span></span> <span data-ttu-id="c646a-108">이 항목에서는 TFS에서 새 빌드 정의를 만드는 방법과 팀 빌드에서 빌드 프로세스의 일부로 웹 배포를 제어 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-108">This topic describes how to create a new build definition in TFS and how to control web deployment as part of the build process in Team Build.</span></span>

<span data-ttu-id="c646a-109">이 항목에서는 Fabrikam, i n c. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 기반으로 하는 일련의 자습서의 일부를 형성 합니다. 이 자습서 시리즈에서는 샘플 솔루션&#x2014;&#x2014;을 사용 [하 여](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)ASP.NET MVC 3 응용 프로그램, Windows Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 비롯 한 현실적인 복잡성의 웹 응용 프로그램을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-109">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="c646a-110">이러한 자습서의 핵심에 나오는 배포 방법은 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)에 설명 된 프로젝트 파일을 이해 하는 방법에 설명 되어 있습니다. 프로젝트 파일에 대 한 빌드 및 배포 프로세스는 모든&#x2014;대상 환경에 적용 되는 빌드 명령을 포함 하는 두 개의 프로젝트 파일과 환경 특정 빌드 및 배포 설정을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-110">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build and deployment process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="c646a-111">빌드 시 환경 관련 프로젝트 파일은 환경에 관계 없는 프로젝트 파일에 병합 되어 전체 빌드 명령 집합을 형성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-111">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="c646a-112">작업 개요</span><span class="sxs-lookup"><span data-stu-id="c646a-112">Task Overview</span></span>

<span data-ttu-id="c646a-113">빌드 정의는 TFS에서 팀 프로젝트에 대 한 빌드가 발생 하는 방법 및 시기를 제어 하는 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-113">A build definition is the mechanism that controls how and when builds occur for team projects in TFS.</span></span> <span data-ttu-id="c646a-114">각 빌드 정의는 다음을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-114">Each build definition specifies:</span></span>

- <span data-ttu-id="c646a-115">Visual Studio 솔루션 파일 또는 MSBuild (사용자 지정 Microsoft Build Engine) 프로젝트 파일과 같이 빌드 하려는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-115">The things you want to build, like Visual Studio solution files or custom Microsoft Build Engine (MSBuild) project files.</span></span>
- <span data-ttu-id="c646a-116">수동 트리거, CI (지속적인 통합), 제어 된 체크 인 등 빌드를 수행 하는 시기를 결정 하는 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-116">The criteria that determine when a build should take place, like manual triggers, continuous integration (CI), or gated check-ins.</span></span>
- <span data-ttu-id="c646a-117">팀 빌드에서 웹 패키지 및 데이터베이스 스크립트와 같은 배포 아티팩트를 포함 하 여 빌드 출력을 보내야 하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-117">The location to which Team Build should send build outputs, including deployment artifacts like web packages and database scripts.</span></span>
- <span data-ttu-id="c646a-118">각 빌드를 유지 해야 하는 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-118">The amount of time that each build should be retained.</span></span>
- <span data-ttu-id="c646a-119">빌드 프로세스의 다양 한 다른 매개 변수</span><span class="sxs-lookup"><span data-stu-id="c646a-119">Various other parameters of the build process.</span></span>

> [!NOTE]
> <span data-ttu-id="c646a-120">빌드 정의에 대 한 자세한 내용은 [빌드 프로세스 정의](https://msdn.microsoft.com/library/ms181715.aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="c646a-120">For more information on build definitions, see [Define Your Build Process](https://msdn.microsoft.com/library/ms181715.aspx).</span></span>

<span data-ttu-id="c646a-121">이 항목에서는 개발자가 새 콘텐츠를 체크 인할 때 빌드가 트리거되도록 CI를 사용 하는 빌드 정의를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-121">This topic will show you how to create a build definition that uses CI, so that a build is triggered when a developer checks in new content.</span></span> <span data-ttu-id="c646a-122">빌드가 성공 하면 빌드 서비스는 사용자 지정 프로젝트 파일을 실행 하 여 솔루션을 테스트 환경에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-122">If the build succeeds, the build service runs a custom project file to deploy the solution to a test environment.</span></span>

<span data-ttu-id="c646a-123">빌드를 트리거할 때 이러한 작업이 수행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-123">When you trigger a build, these actions need to happen:</span></span>

- <span data-ttu-id="c646a-124">먼저 팀 빌드에서 솔루션을 빌드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-124">First, Team Build should build the solution.</span></span> <span data-ttu-id="c646a-125">이 프로세스의 일부로 팀 빌드는 웹 게시 파이프라인 (WPP)을 호출 하 여 솔루션의 각 웹 응용 프로그램 프로젝트에 대 한 웹 배포 패키지를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-125">As part of this process, Team Build will invoke the Web Publishing Pipeline (WPP) to generate web deployment packages for each of the web application projects in the solution.</span></span> <span data-ttu-id="c646a-126">또한 팀 빌드는 솔루션과 연결 된 단위 테스트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-126">Team Build will also run any unit tests associated with the solution.</span></span>
- <span data-ttu-id="c646a-127">솔루션 빌드에 실패 하는 경우 팀 빌드에서 추가 작업을 수행 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-127">If the solution build fails, Team Build should take no further action.</span></span> <span data-ttu-id="c646a-128">단위 테스트 오류는 빌드 실패로 처리 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-128">Unit test failures should be treated as a build failure.</span></span>
- <span data-ttu-id="c646a-129">솔루션 빌드가 성공적으로 완료 되 면 팀 빌드에서 솔루션의 배포를 제어 하는 사용자 지정 프로젝트 파일을 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-129">If the solution build succeeds, Team Build should run the custom project file that controls the deployment of the solution.</span></span> <span data-ttu-id="c646a-130">이 프로세스의 일부로 팀 빌드는 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)를 호출 하 여 패키지 된 웹 응용 프로그램을 대상 웹 서버에 설치 하 고, VSDBCMD 유틸리티를 호출 하 여 데이터베이스 만들기를 실행 합니다. 대상 데이터베이스 서버에 대 한 스크립트</span><span class="sxs-lookup"><span data-stu-id="c646a-130">As part of this process, Team Build will invoke the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) to install the packaged web applications on the destination web servers, and it will invoke the VSDBCMD.exe utility to run database creation scripts on the destination database servers.</span></span>

<span data-ttu-id="c646a-131">다음은이 프로세스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-131">This illustrates the process:</span></span>

![](creating-a-build-definition-that-supports-deployment/_static/image1.png)

<span data-ttu-id="c646a-132">[Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) 샘플 솔루션에는 Msbuild 또는 팀 빌드에서 실행할 수 있는 사용자 지정 msbuild 프로젝트 파일인 *Publish. proj*가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-132">The [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) sample solution includes a custom MSBuild project file, *Publish.proj*, that you can run from MSBuild or Team Build.</span></span> <span data-ttu-id="c646a-133">[빌드 프로세스 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)에 설명 된 대로이 프로젝트 파일은 웹 패키지 및 데이터베이스를 대상 환경에 배포 하는 논리를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-133">As described in [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md), this project file defines the logic that deploys your web packages and databases to a target environment.</span></span> <span data-ttu-id="c646a-134">이 파일은 팀 빌드에서 실행 되는 경우 빌드 및 패키징 프로세스를 생략 하는 논리를 포함 하며, 실행 될 배포 작업만 남겨 둡니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-134">The file includes logic that omits the building and packaging process if it's running in Team Build, leaving just the deployment tasks to run.</span></span> <span data-ttu-id="c646a-135">이러한 방식으로 배포를 자동화 하는 경우 일반적으로 솔루션을 성공적으로 빌드하고 배포 프로세스를 시작 됩니다 전에 단위 테스트를 통과 하도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-135">This is because when you automate deployment in this way, you'll typically want to ensure that the solution builds successfully and passes any unit tests before the deployment process commences.</span></span>

<span data-ttu-id="c646a-136">다음 섹션에서는 새 빌드 정의를 만들어이 프로세스를 구현 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-136">The next section explains how to implement this process by creating a new build definition.</span></span>

> [!NOTE]
> <span data-ttu-id="c646a-137">자동화 된&#x2014;단일 프로세스에서 솔루션&#x2014;을 빌드, 테스트 및 배포 하는이 절차는 테스트 환경에 배포 하는 데 가장 적합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-137">This procedure&#x2014;in which a single automated process builds, tests, and deploys a solution&#x2014;is likely to be most suited to deployment to test environments.</span></span> <span data-ttu-id="c646a-138">스테이징 및 프로덕션 환경의 경우 테스트 환경에서 이미 확인 하 고 유효성을 검사 한 이전 빌드의 콘텐츠를 배포 하는 것이 훨씬 더 많을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-138">For staging and production environments you're a lot more likely to want to deploy content from a previous build that you've already verified and validated in a test environment.</span></span> <span data-ttu-id="c646a-139">이 방법은 다음 항목인 [특정 빌드 배포](deploying-a-specific-build.md)항목에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-139">This approach is described in the next topic, [Deploying a Specific Build](deploying-a-specific-build.md).</span></span>

### <a name="who-performs-this-procedure"></a><span data-ttu-id="c646a-140">이 절차를 수행 하는 사용자</span><span class="sxs-lookup"><span data-stu-id="c646a-140">Who Performs This Procedure?</span></span>

<span data-ttu-id="c646a-141">일반적으로 TFS 관리자는이 절차를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-141">Typically, a TFS administrator performs this procedure.</span></span> <span data-ttu-id="c646a-142">개발자 팀 리더가 TFS의 팀 프로젝트 컬렉션을 담당 하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-142">In some cases, a developer team leader may take responsibility for the team project collection in TFS.</span></span> <span data-ttu-id="c646a-143">새 빌드 정의를 만들려면 솔루션을 포함 하는 팀 프로젝트 컬렉션에 대 한 **Project Collection Build Administrators** 그룹의 멤버 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-143">In order to create a new build definition, you need to be a member of the **Project Collection Build Administrators** group for the team project collection that contains your solution.</span></span>

## <a name="create-a-build-definition-for-ci-and-deployment"></a><span data-ttu-id="c646a-144">CI 및 배포에 대 한 빌드 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="c646a-144">Create a Build Definition for CI and Deployment</span></span>

<span data-ttu-id="c646a-145">다음 절차에서는 CI가 트리거하는 빌드 정의를 만드는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-145">The next procedure describes how to create a build definition that CI triggers.</span></span> <span data-ttu-id="c646a-146">빌드가 성공 하면 사용자 지정 MSBuild 프로젝트 파일에서 논리를 사용 하 여 솔루션이 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-146">If the build succeeds, the solution is deployed using the logic in a custom MSBuild project file.</span></span>

<span data-ttu-id="c646a-147">**CI 및 배포에 대 한 빌드 정의를 만들려면**</span><span class="sxs-lookup"><span data-stu-id="c646a-147">**To create a build definition for CI and deployment**</span></span>

1. <span data-ttu-id="c646a-148">Visual Studio 2010의 **팀 탐색기** 창에서 팀 프로젝트 노드를 확장 하 고 **빌드**를 마우스 오른쪽 단추로 클릭 한 다음 **새 빌드 정의**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-148">In Visual Studio 2010, in the **Team Explorer** window, expand your team project node, right-click **Builds**, and then click **New Build Definition**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image2.png)
2. <span data-ttu-id="c646a-149">**일반** 탭에서 빌드 정의 이름 (예: **deploytotest**) 및 설명 (선택 사항)을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-149">On the **General** tab, give the build definition a name (for example, **DeployToTest**) and an optional description.</span></span>
3. <span data-ttu-id="c646a-150">**트리거** 탭에서 새 빌드를 트리거할 기준을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-150">On the **Trigger** tab, select the criteria on which you want to trigger a new build.</span></span> <span data-ttu-id="c646a-151">예를 들어, 개발자가 새 코드를 체크 인할 때마다 솔루션을 빌드하고 테스트 환경에 배포 하려는 경우 **연속 통합**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-151">For example, if you want to build the solution and deploy to the test environment every time a developer checks in new code, select **Continuous Integration**.</span></span>
4. <span data-ttu-id="c646a-152">**빌드 기본값** 탭의 **다음 저장 폴더에 빌드 출력 복사** 상자에 저장 폴더의 UNC (범용 명명 규칙) 경로를 입력 합니다 (예: **\\TFSBUILD\Drops**).</span><span class="sxs-lookup"><span data-stu-id="c646a-152">On the **Build Defaults** tab, in the **Copy build output to the following drop folder** box, type the Universal Naming Convention (UNC) path of your drop folder (for example, **\\TFSBUILD\Drops**).</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image3.png)

    > [!NOTE]
    > <span data-ttu-id="c646a-153">이 저장 위치는 구성 하는 보존 정책에 따라 여러 빌드를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-153">This drop location stores several builds, depending on the retention policy you configure.</span></span> <span data-ttu-id="c646a-154">특정 빌드에서 스테이징 또는 프로덕션 환경으로 배포 아티팩트를 게시 하려는 경우이 위치에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-154">When you want to publish deployment artifacts from a specific build to a staging or production environment, this is where you'll find them.</span></span>
5. <span data-ttu-id="c646a-155">**프로세스** 탭의 **빌드 프로세스 파일** 드롭다운 목록에서 **defaulttemplate .xaml** 을 선택 된 채로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-155">On the **Process** tab, in the **Build process file** dropdown list, leave **DefaultTemplate.xaml** selected.</span></span> <span data-ttu-id="c646a-156">모든 새 팀 프로젝트에 추가 되는 기본 빌드 프로세스 템플릿 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-156">This is one of the default build process templates that get added to all new team projects.</span></span>
6. <span data-ttu-id="c646a-157">**빌드 프로세스 매개 변수** 테이블에서 **빌드할 항목** 행을 클릭 한 다음 **줄임표** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-157">In the **Build process parameters** table, click in the **Items to Build** row, and then click the **ellipsis** button.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image4.png)
7. <span data-ttu-id="c646a-158">**빌드할 항목** 대화 상자에서 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-158">In the **Items to Build** dialog box, click **Add**.</span></span>
8. <span data-ttu-id="c646a-159">솔루션 파일의 위치로 이동한 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-159">Browse to the location of your solution file, and then click **OK**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image5.png)
9. <span data-ttu-id="c646a-160">**빌드할 항목** 대화 상자에서 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-160">In the **Items to Build** dialog box, click **Add**.</span></span>
10. <span data-ttu-id="c646a-161">다음 **형식의 항목** 드롭다운 목록에서 **MSBuild 프로젝트 파일**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-161">In the **Items of type** dropdown list, select **MSBuild Project files**.</span></span>
11. <span data-ttu-id="c646a-162">배포 프로세스를 제어 하는 사용자 지정 프로젝트 파일의 위치로 이동 하 여 파일을 선택한 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-162">Browse to the location of the custom project file with which you control the deployment process, select the file, and then click **OK**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image6.png)
12. <span data-ttu-id="c646a-163">이제 **빌드할 항목** 대화 상자에 두 개의 항목이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-163">The **Items to Build** dialog box should now show two items.</span></span> <span data-ttu-id="c646a-164">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-164">Click **OK**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image7.png)
13. <span data-ttu-id="c646a-165">**프로세스** 탭의 **빌드 프로세스 매개 변수** 테이블에서 **고급** 섹션을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-165">On the **Process** tab, in the **Build process parameters** table, expand the **Advanced** section.</span></span>
14. <span data-ttu-id="c646a-166">**Msbuild arguments** 행에서 빌드할 항목 중 *하나* 에 필요한 MSBuild 명령줄 인수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-166">In the **MSBuild Arguments** row, add any MSBuild command-line arguments that *either* of your items to build requires.</span></span> <span data-ttu-id="c646a-167">Contact Manager 솔루션 시나리오에서는 다음과 같은 인수가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-167">In the Contact Manager solution scenario, these arguments are required:</span></span>

    [!code-console[Main](creating-a-build-definition-that-supports-deployment/samples/sample1.cmd)]

    ![](creating-a-build-definition-that-supports-deployment/_static/image8.png)
15. <span data-ttu-id="c646a-168">이 예제에서:</span><span class="sxs-lookup"><span data-stu-id="c646a-168">In this example:</span></span>

    1. <span data-ttu-id="c646a-169">Contact Manager 솔루션을 빌드하는 경우 **Deployonbuild = true** 및 **deploytarget = package** 인수를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-169">The **DeployOnBuild=true** and **DeployTarget=package** arguments are required when you build the Contact Manager solution.</span></span> <span data-ttu-id="c646a-170">이렇게 하면 [웹 응용 프로그램 프로젝트 빌드 및 패키징](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)에 설명 된 대로 각 웹 응용 프로그램 프로젝트를 빌드한 후 웹 배포 패키지를 만들도록 MSBuild에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-170">This instructs MSBuild to create web deployment packages after building each web application project, as described in [Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md).</span></span>
    2. <span data-ttu-id="c646a-171">**TargetEnvPropsFile** 인수는 *Publish. proj* 파일을 빌드할 때 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-171">The **TargetEnvPropsFile** argument is required when you build the *Publish.proj* file.</span></span> <span data-ttu-id="c646a-172">이 속성은 [빌드 프로세스 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)에 설명 된 대로 환경 관련 구성 파일의 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-172">This property indicates the location of the environment-specific configuration file, as described in [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span>
16. <span data-ttu-id="c646a-173">**보존 정책** 탭에서 필요에 따라 유지할 각 유형의 빌드 수를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-173">On the **Retention Policy** tab, configure how many builds of each type you want to retain as required.</span></span>
17. <span data-ttu-id="c646a-174">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-174">Click **Save**.</span></span>

## <a name="queue-a-build"></a><span data-ttu-id="c646a-175">큐에 빌드 대기시키기</span><span class="sxs-lookup"><span data-stu-id="c646a-175">Queue a Build</span></span>

<span data-ttu-id="c646a-176">이 시점에서 하나 이상의 새 빌드 정의를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-176">At this point, you have created at least one new build definition.</span></span> <span data-ttu-id="c646a-177">이제 정의한 빌드 프로세스가 빌드 정의에 지정 된 트리거에 따라 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-177">The build process you defined will now run according to the triggers you specified in the build definition.</span></span>

<span data-ttu-id="c646a-178">CI를 사용 하도록 빌드 정의를 구성한 경우 다음과 같은 두 가지 방법으로 빌드 정의를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-178">If you've configured your build definition to use CI, you can test your build definition in two ways:</span></span>

- <span data-ttu-id="c646a-179">팀 프로젝트에 대 한 일부 콘텐츠를 체크 인하고 자동 빌드를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-179">Check in some content to the team project to trigger an automatic build.</span></span>
- <span data-ttu-id="c646a-180">수동으로 빌드를 큐에 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-180">Queue a build manually.</span></span>

<span data-ttu-id="c646a-181">**수동으로 빌드를 큐에 대기 시키려면**</span><span class="sxs-lookup"><span data-stu-id="c646a-181">**To queue a build manually**</span></span>

1. <span data-ttu-id="c646a-182">**팀 탐색기** 창에서 빌드 정의를 마우스 오른쪽 단추로 클릭 한 다음 **새 빌드 큐 대기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-182">In the **Team Explorer** window, right-click the build definition, and then click **Queue New Build**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image9.png)
2. <span data-ttu-id="c646a-183">**빌드 큐 대기** 대화 상자에서 빌드 속성을 검토 한 다음 **큐**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-183">In the **Queue Build** dialog box, review the build properties, and then click **Queue**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image10.png)

<span data-ttu-id="c646a-184">수동으로 트리거 했는지 여부에 관계 없이 빌드의&#x2014;진행률 및 결과를 검토 하려면 **팀 탐색기** 창에서 빌드 정의&#x2014;를 자동으로 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-184">To review the progress and the outcome of a build&#x2014;regardless of whether it was triggered manually or automatically&#x2014;double-click the build definition in the **Team Explorer** window.</span></span> <span data-ttu-id="c646a-185">그러면 **빌드 탐색기** 탭이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-185">This will open a **Build Explorer** tab.</span></span>

![](creating-a-build-definition-that-supports-deployment/_static/image11.png)

<span data-ttu-id="c646a-186">여기에서 실패 한 빌드의 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-186">From here, you can troubleshoot failed builds.</span></span> <span data-ttu-id="c646a-187">개별 빌드를 두 번 클릭 하면 요약 정보를 보고 자세한 로그 파일을 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-187">If you double-click an individual build, you can view summary information and click through to detailed log files.</span></span>

![](creating-a-build-definition-that-supports-deployment/_static/image12.png)

<span data-ttu-id="c646a-188">이 정보를 사용 하 여 실패 한 빌드의 문제를 해결 하 고 다른 빌드를 시도 하기 전에 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-188">You can use this information to troubleshoot failed builds and address any problems before you attempt another build.</span></span>

> [!NOTE]
> <span data-ttu-id="c646a-189">배포 논리를 실행 하는 빌드는 대상 환경에 필요한 사용 권한을 빌드 서버에 부여 하기 전까지 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-189">Builds that execute deployment logic are likely to fail until you have granted the build server any permissions required in the destination environment.</span></span> <span data-ttu-id="c646a-190">자세한 내용은 [팀 빌드 배포에 대 한 사용 권한 구성](configuring-permissions-for-team-build-deployment.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="c646a-190">For more information, see [Configuring Permissions for Team Build Deployment](configuring-permissions-for-team-build-deployment.md).</span></span>

## <a name="monitor-the-build-process"></a><span data-ttu-id="c646a-191">빌드 프로세스 모니터링</span><span class="sxs-lookup"><span data-stu-id="c646a-191">Monitor the Build Process</span></span>

<span data-ttu-id="c646a-192">TFS는 빌드 프로세스를 모니터링 하는 데 도움이 되는 광범위 한 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-192">TFS provides a broad range of functionality to help you monitor the build process.</span></span> <span data-ttu-id="c646a-193">예를 들어, TFS는 빌드가 완료 되 면 작업 표시줄 알림 영역에 전자 메일을 보내거나 경고를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-193">For example, TFS can send you an email or display alerts in your taskbar notification area when a build has completed.</span></span> <span data-ttu-id="c646a-194">자세한 내용은 [빌드 실행 및 모니터링](https://msdn.microsoft.com/library/ms181721.aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="c646a-194">For more information, see [Run and Monitor Builds](https://msdn.microsoft.com/library/ms181721.aspx).</span></span>

## <a name="conclusion"></a><span data-ttu-id="c646a-195">결론</span><span class="sxs-lookup"><span data-stu-id="c646a-195">Conclusion</span></span>

<span data-ttu-id="c646a-196">이 항목에서는 TFS에서 빌드 정의를 만드는 방법에 대해 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-196">This topic described how to create a build definition in TFS.</span></span> <span data-ttu-id="c646a-197">빌드 정의는 CI에 대해 구성 되므로 개발자가 팀 프로젝트에 대 한 콘텐츠를 체크 인할 때마다 빌드 프로세스가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-197">The build definition is configured for CI, so the build process runs whenever a developer checks in content to the team project.</span></span> <span data-ttu-id="c646a-198">빌드 정의는 사용자 지정 MSBuild 프로젝트 파일을 실행 하 여 웹 패키지와 데이터베이스 스크립트를 대상 서버 환경에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-198">The build definition executes a custom MSBuild project file to deploy web packages and database scripts to a target server environment.</span></span>

<span data-ttu-id="c646a-199">자동화 된 배포가 빌드 프로세스의 일부로 성공 하려면 대상 웹 서버 및 대상 데이터베이스 서버의 빌드 서비스 계정에 적절 한 권한을 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-199">In order for an automated deployment to succeed as part of a build process, you'll need to grant appropriate permissions to the build service account on the target web servers and the target database server.</span></span> <span data-ttu-id="c646a-200">이 자습서의 최종 항목인 [팀 빌드 배포에 대 한 사용 권한 구성](configuring-permissions-for-team-build-deployment.md)에서는 팀 빌드 서버에서 자동화 된 배포에 필요한 사용 권한을 식별 하 고 구성 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c646a-200">The final topic in this tutorial, [Configuring Permissions for Team Build Deployment](configuring-permissions-for-team-build-deployment.md), describes how to identify and configure the permissions required for automated deployment from a Team Build server.</span></span>

## <a name="further-reading"></a><span data-ttu-id="c646a-201">추가 참고 자료</span><span class="sxs-lookup"><span data-stu-id="c646a-201">Further Reading</span></span>

<span data-ttu-id="c646a-202">빌드 정의를 만드는 방법에 대 한 자세한 내용은 [기본 빌드 정의 만들기](https://msdn.microsoft.com/library/ms181716.aspx) 및 [빌드 프로세스 정의](https://msdn.microsoft.com/library/ms181715.aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="c646a-202">For more information on creating build definitions, see [Create a Basic Build Definition](https://msdn.microsoft.com/library/ms181716.aspx) and [Define Your Build Process](https://msdn.microsoft.com/library/ms181715.aspx).</span></span> <span data-ttu-id="c646a-203">빌드를 큐에 추가 하는 방법에 대 한 자세한 지침은 [빌드 큐 대기](https://msdn.microsoft.com/library/ms181722.aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="c646a-203">For more guidance on queuing builds, see [Queue a Build](https://msdn.microsoft.com/library/ms181722.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c646a-204">[이전](configuring-a-tfs-build-server-for-web-deployment.md)
> [다음](deploying-a-specific-build.md)</span><span class="sxs-lookup"><span data-stu-id="c646a-204">[Previous](configuring-a-tfs-build-server-for-web-deployment.md)
[Next](deploying-a-specific-build.md)</span></span>
