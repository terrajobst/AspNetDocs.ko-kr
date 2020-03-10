---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
title: 소스 제어에 콘텐츠 추가 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 TFS (Team Foundation Server) 2010에서 소스 제어에 콘텐츠를 추가 하는 방법에 대해 설명 합니다. 팀 프로젝트에 솔루션 및 프로젝트를 추가 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 86c14aab-c2dd-4f73-b40c-c6d52fa44950
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
msc.type: authoredcontent
ms.openlocfilehash: 16073dd2fb0ea1cc4ddbc94c843181933dc174c1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515111"
---
# <a name="adding-content-to-source-control"></a><span data-ttu-id="67745-104">소스 제어에 콘텐츠 추가</span><span class="sxs-lookup"><span data-stu-id="67745-104">Adding Content to Source Control</span></span>

<span data-ttu-id="67745-105">[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="67745-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="67745-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="67745-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="67745-107">이 항목에서는 TFS (Team Foundation Server) 2010에서 소스 제어에 콘텐츠를 추가 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-107">This topic explains how to add content to source control in Team Foundation Server (TFS) 2010.</span></span> <span data-ttu-id="67745-108">또한 TFS에서 팀 프로젝트에 솔루션 및 프로젝트를 추가 하는 방법에 대해 설명 하 고 프레임 워크 또는 어셈블리와 같은 외부 종속성을 소스 제어에 추가 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-108">It describes how to add solutions and projects to a team project in TFS, and it explains how to add external dependencies like frameworks or assemblies to source control.</span></span>

<span data-ttu-id="67745-109">이 항목에서는 Fabrikam, i n c. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 기반으로 하는 일련의 자습서의 일부를 형성 합니다. 이 자습서 시리즈에서는 샘플 솔루션&#x2014;&#x2014;을 사용 [하 여](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)ASP.NET MVC 3 응용 프로그램, Windows Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 비롯 한 현실적인 복잡성의 웹 응용 프로그램을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="67745-109">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

## <a name="task-overview"></a><span data-ttu-id="67745-110">작업 개요</span><span class="sxs-lookup"><span data-stu-id="67745-110">Task Overview</span></span>

<span data-ttu-id="67745-111">대부분의 경우 개발자 팀의 모든 멤버는 소스 제어에 콘텐츠를 추가할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-111">In most cases, every member of the developer team should be able to add content to source control.</span></span> <span data-ttu-id="67745-112">TFS에서 소스 제어에 솔루션을 추가 하려면 다음과 같은 개략적인 단계를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-112">To add a solution to source control in TFS, you'll need to complete these high-level steps:</span></span>

- <span data-ttu-id="67745-113">팀 프로젝트에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-113">Connect to a team project.</span></span>
- <span data-ttu-id="67745-114">서버의 팀 프로젝트 폴더 구조를 로컬 컴퓨터의 폴더 구조에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-114">Map the team project folder structure on the server to a folder structure on your local computer.</span></span>
- <span data-ttu-id="67745-115">솔루션과 해당 콘텐츠를 소스 제어에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-115">Add the solution and its contents to source control.</span></span>
- <span data-ttu-id="67745-116">소스 제어에 외부 종속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-116">Add any external dependencies to source control.</span></span>

<span data-ttu-id="67745-117">이 항목에서는 이러한 절차를 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="67745-117">This topic will show you how to perform these procedures.</span></span>

<span data-ttu-id="67745-118">이 항목의 작업 및 연습에서는 콘텐츠를 관리 하는 새 TFS 팀 프로젝트를 이미 만들었다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-118">The tasks and walkthroughs in this topic assume that you've already created a new TFS team project to manage your content.</span></span> <span data-ttu-id="67745-119">새 팀 프로젝트를 만드는 방법에 대 한 자세한 내용은 [TFS에서 팀 프로젝트 만들기](creating-a-team-project-in-tfs.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="67745-119">For more information on creating a new team project, see [Creating a Team Project in TFS](creating-a-team-project-in-tfs.md).</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="67745-120">이러한 절차를 수행 하는 사람은 누구 인가요?</span><span class="sxs-lookup"><span data-stu-id="67745-120">Who Performs These Procedures?</span></span>

<span data-ttu-id="67745-121">대부분의 경우 개발자 팀의 모든 멤버는 특정 팀 프로젝트 내에서 콘텐츠를 추가 하 고 수정할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-121">In most cases, every member of the developer team should be able to add and modify content within specific team projects.</span></span>

## <a name="connect-to-a-team-project-and-create-a-folder-mapping"></a><span data-ttu-id="67745-122">팀 프로젝트에 연결 하 고 폴더 매핑을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="67745-122">Connect to a Team Project and Create a Folder Mapping</span></span>

<span data-ttu-id="67745-123">소스 제어에 콘텐츠를 추가 하기 전에 팀 프로젝트에 연결 하 고 서버의 폴더 구조와 로컬 컴퓨터의 파일 시스템 간에 매핑을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-123">Before you add any content to source control, you need to connect to a team project and create a mapping between the folder structure on the server and the file system on your local machine.</span></span>

<span data-ttu-id="67745-124">**팀 프로젝트에 연결 하 고 로컬 경로를 매핑하려면**</span><span class="sxs-lookup"><span data-stu-id="67745-124">**To connect to a team project and map a local path**</span></span>

1. <span data-ttu-id="67745-125">개발자 워크스테이션에서 Visual Studio 2010을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="67745-125">On your developer workstation, open Visual Studio 2010.</span></span>
2. <span data-ttu-id="67745-126">Visual Studio의 **팀** 메뉴에서 **Team Foundation Server에 연결**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-126">In Visual Studio, on the **Team** menu, click **Connect to Team Foundation Server**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="67745-127">TFS 서버에 대 한 연결을 이미 구성한 경우에는 3-6 단계를 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67745-127">If you have already configured a connection to a TFS server, you can omit steps 3-6.</span></span>
3. <span data-ttu-id="67745-128">**팀 프로젝트에 연결** 대화 상자에서 **서버**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-128">In the **Connection to Team Project** dialog box, click **Servers**.</span></span>
4. <span data-ttu-id="67745-129">**Team Foundation Server 추가/제거** 대화 상자에서 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-129">In the **Add/Remove Team Foundation Server** dialog box, click **Add**.</span></span>
5. <span data-ttu-id="67745-130">**Team Foundation Server 추가** 대화 상자에서 TFS 인스턴스의 세부 정보를 입력 한 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-130">In the **Add Team Foundation Server** dialog box, provide the details of your TFS instance, and then click **OK**.</span></span>

    ![](adding-content-to-source-control/_static/image1.png)
6. <span data-ttu-id="67745-131">**Team Foundation Server 추가/제거** 대화 상자에서 **닫기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-131">In the **Add/Remove Team Foundation Server** dialog box, click **Close**.</span></span>
7. <span data-ttu-id="67745-132">**팀 프로젝트에 연결** 대화 상자에서 연결할 TFS 인스턴스를 선택 하 고 팀 프로젝트 컬렉션을 선택한 다음 추가 하려는 팀 프로젝트를 선택 하 고 **연결**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-132">In the **Connect to Team Project** dialog box, select the TFS instance you want to connect to, select the team project collection, select the team project you want to add to, and then click **Connect**.</span></span>

    ![](adding-content-to-source-control/_static/image2.png)
8. <span data-ttu-id="67745-133">**팀 탐색기** 창에서 팀 프로젝트를 확장 한 다음 **소스 제어**를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-133">In the **Team Explorer** window, expand your team project, and then double-click **Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image3.png)
9. <span data-ttu-id="67745-134">**소스 제어 탐색기** 탭에서 **매핑 안 함**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-134">On the **Source Control Explorer** tab, click **Not mapped**.</span></span>

    ![](adding-content-to-source-control/_static/image4.png)
10. <span data-ttu-id="67745-135">**맵** 대화 상자의 **로컬 폴더** 상자에서 팀 프로젝트에 대 한 루트 폴더로 사용할 로컬 폴더를 찾아보거나 만든 다음 **지도**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-135">In the **Map** dialog box, in the **Local folder** box, browse to (or create) a local folder to act as the root folder for the team project, and then click **Map**.</span></span>

    ![](adding-content-to-source-control/_static/image5.png)
11. <span data-ttu-id="67745-136">원본 파일을 다운로드 하 라는 메시지가 표시 되 면 **예**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-136">When you're prompted to download source files, click **Yes**.</span></span>

    ![](adding-content-to-source-control/_static/image6.png)

<span data-ttu-id="67745-137">이 시점에서 팀 프로젝트에 대 한 서버 쪽 폴더를 개발자 워크스테이션의 로컬 폴더에 매핑 했습니다.</span><span class="sxs-lookup"><span data-stu-id="67745-137">At this point, you have mapped the server-side folder for the team project to a local folder on your developer workstation.</span></span> <span data-ttu-id="67745-138">또한 팀 프로젝트에서 로컬 폴더 구조로 기존 콘텐츠를 다운로드 했습니다.</span><span class="sxs-lookup"><span data-stu-id="67745-138">You've also downloaded any existing content from the team project to your local folder structure.</span></span> <span data-ttu-id="67745-139">이제 소스 제어에 자신의 콘텐츠를 추가 하기 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67745-139">You can now start to add your own content to source control.</span></span>

## <a name="add-projects-and-solutions-to-source-control"></a><span data-ttu-id="67745-140">프로젝트 및 솔루션을 소스 제어에 추가</span><span class="sxs-lookup"><span data-stu-id="67745-140">Add Projects and Solutions to Source Control</span></span>

<span data-ttu-id="67745-141">프로젝트 및 솔루션을 소스 제어에 추가 하려면 먼저 로컬 컴퓨터의 팀 프로젝트에 대 한 매핑된 폴더로 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-141">To add projects and solutions to source control, you first need to move them to the mapped folder for the team project on your local machine.</span></span> <span data-ttu-id="67745-142">그런 다음 콘텐츠를 체크 인하고 서버와의 추가 내용을 동기화 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67745-142">You can then check in the content to synchronize your additions with the server.</span></span>

<span data-ttu-id="67745-143">**소스 제어에 프로젝트를 추가 하려면**</span><span class="sxs-lookup"><span data-stu-id="67745-143">**To add projects to source control**</span></span>

1. <span data-ttu-id="67745-144">개발자 워크스테이션에서 프로젝트와 솔루션을 팀 프로젝트에 대 한 매핑된 폴더 구조 내의 적절 한 위치로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-144">On your developer workstation, move your projects and solutions to an appropriate location within the mapped folder structure for the team project.</span></span>

    > [!NOTE]
    > <span data-ttu-id="67745-145">많은 조직에는 소스 제어에서 프로젝트와 솔루션을 구성 하는 방법에 대 한 기본 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67745-145">Many organizations will have a preferred approach to how projects and solutions should be organized in source control.</span></span> <span data-ttu-id="67745-146">폴더 구조를 구성 하는 방법에 대 한 지침은 [방법: Team Foundation Server에서 소스 제어 폴더 구조](https://msdn.microsoft.com/library/bb668992.aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="67745-146">For guidance on how to structure folders, see [How To: Structure Your Source Control Folders in Team Foundation Server](https://msdn.microsoft.com/library/bb668992.aspx).</span></span>
2. <span data-ttu-id="67745-147">Visual Studio 2010에서 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="67745-147">Open the solution in Visual Studio 2010.</span></span>
3. <span data-ttu-id="67745-148">**솔루션 탐색기** 창에서 솔루션을 마우스 오른쪽 단추로 클릭 한 다음 **소스 제어에 솔루션 추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-148">In the **Solution Explorer** window, right-click the solution, and then click **Add Solution to Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image7.png)

    > [!NOTE]
    > <span data-ttu-id="67745-149">일부 경우에는 조직이 TFS에서 콘텐츠를 구조화 하는 방법에 따라 소스 제어에 프로젝트를 개별적으로 추가 하 여 소스 코드를 구성 하는 방법을 보다 세밀 하 게 제어 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67745-149">In some cases, depending on how your organization likes to structure content in TFS, you may need to add projects to source control individually to provide more fine-grained control over how your source code is organized.</span></span>
4. <span data-ttu-id="67745-150">**소스 제어 탐색기** 탭에 팀 프로젝트의 서버 폴더 구조 내에 추가한 내용이 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-150">Verify that the **Source Control Explorer** tab displays the content you've added within the server folder structure for the team project.</span></span>

    ![](adding-content-to-source-control/_static/image8.png)

    > [!NOTE]
    > <span data-ttu-id="67745-151">로컬 파일 시스템의 매핑된 폴더에 솔루션을 추가 했으므로 **소스 제어 탐색기** 탭에는 추가 메시지를 표시 하지 않고 콘텐츠가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67745-151">The **Source Control Explorer** tab displays your content with no further prompting because you added your solution to a mapped folder on the local file system.</span></span> <span data-ttu-id="67745-152">솔루션이 매핑되지 않은 위치에 있는 경우 TFS와 로컬 파일 시스템 모두에서 폴더 위치를 지정 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67745-152">If your solution was in an unmapped location, you'd be prompted to specify folder locations in both TFS and your local file system.</span></span>
5. <span data-ttu-id="67745-153">**소스 제어 탐색기** 탭의 **폴더** 창에서 팀 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 (예: **연락처 관리자**) **보류 중인 변경 내용 체크 인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-153">On the **Source Control Explorer** tab, in the **Folders** pane, right-click the team project (for example, **ContactManager**), and then click **Check In Pending Changes**.</span></span>
6. <span data-ttu-id="67745-154">체크 인 **– 소스 파일** 대화 상자에 설명을 입력 한 다음 **체크**인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-154">In the **Check In – Source Files** dialog box, type a comment, and then click **Check In**.</span></span>

    ![](adding-content-to-source-control/_static/image9.png)

<span data-ttu-id="67745-155">이 시점에서 TFS의 소스 제어에 솔루션을 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="67745-155">At this point you have added your solution to source control in TFS.</span></span>

## <a name="add-external-dependencies-to-source-control"></a><span data-ttu-id="67745-156">소스 제어에 외부 종속성 추가</span><span class="sxs-lookup"><span data-stu-id="67745-156">Add External Dependencies to Source Control</span></span>

<span data-ttu-id="67745-157">프로젝트 또는 솔루션을 소스 제어에 추가 하면 프로젝트 또는 솔루션 내의 모든 파일 및 폴더도 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67745-157">When you add a project or solution to source control, any files and folders within your project or solution will also be added.</span></span> <span data-ttu-id="67745-158">그러나 많은 경우에 프로젝트와 솔루션은 로컬 어셈블리와 같은 외부 종속성을 사용 하 여 제대로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-158">However, in a lot of cases, projects and solutions also rely on external dependencies, like local assemblies, to function properly.</span></span> <span data-ttu-id="67745-159">팀 빌드와 개발자 팀의 다른 멤버가 코드를 성공적으로 빌드할 수 있도록 소스 제어에 이러한 리소스를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-159">You need to add any such resources to source control to let both Team Build and other members of the developer team build your code successfully.</span></span>

<span data-ttu-id="67745-160">예를 들어 Contact Manager 샘플 솔루션의 폴더 구조에는 패키지 라는 폴더가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67745-160">For example, the folder structure for the Contact Manager sample solution includes a folder named packages.</span></span> <span data-ttu-id="67745-161">여기에는 ADO.NET Entity Framework 4.1에 대 한 어셈블리와 다양 한 지원 리소스가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67745-161">This contains the assembly and various supporting resources for the ADO.NET Entity Framework 4.1.</span></span> <span data-ttu-id="67745-162">패키지 폴더는 Contact Manager 솔루션에 포함 되지 않지만 솔루션은이 솔루션을 사용 하지 않고 제대로 빌드되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67745-162">The packages folder is not part of the Contact Manager solution, but the solution will not build successfully without it.</span></span> <span data-ttu-id="67745-163">팀 빌드에서 솔루션을 빌드할 수 있도록 하려면 패키지 폴더를 소스 제어에 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-163">To enable Team Build to build the solution, you need to add the packages folder to source control.</span></span>

> [!NOTE]
> <span data-ttu-id="67745-164">패키지 폴더는 Visual Studio 2010에 대 한 NuGet 확장을 사용 하 여 솔루션에 Entity Framework 또는 유사한 리소스를 추가할 때 일반적으로 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-164">The inclusion of a packages folder is typical of what happens when you add the Entity Framework, or similar resources, to your solution using the NuGet extension for Visual Studio 2010.</span></span>

<span data-ttu-id="67745-165">**비 프로젝트 콘텐츠를 소스 제어에 추가 하려면**</span><span class="sxs-lookup"><span data-stu-id="67745-165">**To add non-project content to source control**</span></span>

1. <span data-ttu-id="67745-166">추가 하려는 항목 (예: 패키지 폴더)이 로컬 파일 시스템의 매핑된 폴더 내에서 적절 한 위치에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-166">Ensure that the items you want to add (for example, the packages folder) are in an appropriate location within a mapped folder on your local file system.</span></span>
2. <span data-ttu-id="67745-167">Visual Studio 2010의 **팀 탐색기** 창에서 팀 프로젝트를 확장 한 다음 **소스 제어**를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-167">In Visual Studio 2010, In the **Team Explorer** window, expand your team project, and then double-click **Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image10.png)
3. <span data-ttu-id="67745-168">**소스 제어 탐색기** 탭의 **폴더** 창에서 추가 하려는 항목이 포함 된 폴더를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-168">On the **Source Control Explorer** tab, in the **Folders** pane, select the folder that contains the item or items you want to add.</span></span>
4. <span data-ttu-id="67745-169">**폴더에 항목 추가** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-169">Click the **Add Items to Folder** button.</span></span>

    ![](adding-content-to-source-control/_static/image11.png)
5. <span data-ttu-id="67745-170">**소스 제어에 추가** 대화 상자에서 추가 하려는 폴더를 선택 하 고 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-170">In the **Add to Source Control** dialog box, select the folder or items you want to add, and then click **Next**.</span></span>

    ![](adding-content-to-source-control/_static/image12.png)
6. <span data-ttu-id="67745-171">제외 된 **항목** 탭에서 자동으로 제외 된 필수 항목 (예: 어셈블리)을 선택 하 고 **항목 포함**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-171">On the **Excluded items** tab, select any required items that have been automatically excluded (for example, assemblies), and then click **Include item(s)**.</span></span>

    ![](adding-content-to-source-control/_static/image13.png)
7. <span data-ttu-id="67745-172">**추가할 항목** 탭에서 포함 하려는 모든 파일이 나열 되는지 확인 한 다음 **마침**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-172">On the **Items to add** tab, verify that all the files you want to include are listed, and then click **Finish**.</span></span>

    ![](adding-content-to-source-control/_static/image14.png)
8. <span data-ttu-id="67745-173">**소스 제어 탐색기** 창에서 **체크** 인 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-173">In the **Source Control Explorer** window, click the **Check In** button.</span></span>

    ![](adding-content-to-source-control/_static/image15.png)
9. <span data-ttu-id="67745-174">체크 인 **– 소스 파일** 대화 상자에 설명을 입력 한 다음 **체크**인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-174">In the **Check In – Source Files** dialog box, type a comment, and then click **Check In**.</span></span>

<span data-ttu-id="67745-175">이 시점에서 솔루션에 대 한 외부 종속성을 소스 제어에 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="67745-175">At this point, you have added the external dependencies for your solution to source control.</span></span>

## <a name="conclusion"></a><span data-ttu-id="67745-176">결론</span><span class="sxs-lookup"><span data-stu-id="67745-176">Conclusion</span></span>

<span data-ttu-id="67745-177">이 항목에서는 팀 프로젝트에 연결 하 고, 폴더 구조를 매핑하고, 소스 제어에 콘텐츠를 추가 하는 방법에 대해 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="67745-177">This topic described how to connect to a team project, map a folder structure, and add content to source control.</span></span> <span data-ttu-id="67745-178">소스 제어에서 항목으로 작업 하는 방법에 대 한 자세한 내용은 [버전 제어 사용](https://msdn.microsoft.com/library/ms181368.aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="67745-178">For more information on how to work with items under source control, see [Using Version Control](https://msdn.microsoft.com/library/ms181368.aspx).</span></span>

<span data-ttu-id="67745-179">다음 항목인 [Tfs 빌드 서버를 웹 배포용으로 구성](configuring-a-tfs-build-server-for-web-deployment.md)에서는 솔루션을 빌드 및 배포 하기 위해 Tfs 팀 빌드 서버를 준비 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="67745-179">The next topic, [Configuring a TFS Build Server for Web Deployment](configuring-a-tfs-build-server-for-web-deployment.md), describes how to prepare a TFS Team Build server to build and deploy your solution.</span></span>

## <a name="further-reading"></a><span data-ttu-id="67745-180">추가 참고 자료</span><span class="sxs-lookup"><span data-stu-id="67745-180">Further Reading</span></span>

<span data-ttu-id="67745-181">TFS에서 원본 제어 작업에 대 한 자세한 내용은 [버전 제어 사용](https://msdn.microsoft.com/library/ms181368.aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="67745-181">For more comprehensive information on working with source control in TFS, see [Using Version Control](https://msdn.microsoft.com/library/ms181368.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="67745-182">[이전](creating-a-team-project-in-tfs.md)
> [다음](configuring-a-tfs-build-server-for-web-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="67745-182">[Previous](creating-a-team-project-in-tfs.md)
[Next](configuring-a-tfs-build-server-for-web-deployment.md)</span></span>
