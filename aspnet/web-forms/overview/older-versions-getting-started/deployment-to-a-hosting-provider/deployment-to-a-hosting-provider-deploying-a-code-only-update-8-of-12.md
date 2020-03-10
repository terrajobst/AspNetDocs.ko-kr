---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
title: 'Visual Studio 또는 Visual Web Developer를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 코드 전용 업데이트 배포-8/12 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 Visual Stu ...를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 11/17/2011
ms.assetid: ddf6252f-9413-4c0c-a360-2cef8d231717
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
msc.type: authoredcontent
ms.openlocfilehash: e4d094ef84a747c36ce05ddb0e3d1ce0391d5605
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78455075"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-code-only-update---8-of-12"></a><span data-ttu-id="ed61e-103">Visual Studio 또는 Visual Web Developer를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 코드 전용 업데이트 배포-8/12</span><span class="sxs-lookup"><span data-stu-id="ed61e-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Deploying a Code-Only Update - 8 of 12</span></span>

<span data-ttu-id="ed61e-104">만든 사람 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="ed61e-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="ed61e-105">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="ed61e-105">Download Starter Project</span></span>](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="ed61e-106">이 자습서 시리즈에서는 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC for Web을 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="ed61e-107">웹 게시 업데이트를 설치 하는 경우 Visual Studio 2010을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="ed61e-108">시리즈에 대 한 소개는 [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ed61e-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="ed61e-109">Visual Studio 2012의 RC 릴리스 후에 도입 된 배포 기능을 보여 주는 자습서는 SQL Server Compact 이외의 SQL Server 버전을 배포 하는 방법을 보여 주고 Azure App Service Web Apps에 배포 하는 방법을 보여 줍니다. [Visual Studio를 사용 하 여 ASP.NET 웹 배포](../../deployment/visual-studio-web-deployment/introduction.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ed61e-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Azure App Service Web Apps, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="ed61e-110">개요</span><span class="sxs-lookup"><span data-stu-id="ed61e-110">Overview</span></span>

<span data-ttu-id="ed61e-111">초기 배포 후에는 웹 사이트를 유지 관리 하 고 개발 하는 작업이 계속 진행 되며 업데이트를 배포 하는 데 오랜 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-111">After the initial deployment, your work of maintaining and developing your web site continues, and before long you will want to deploy an update.</span></span> <span data-ttu-id="ed61e-112">이 자습서는 응용 프로그램 코드에 업데이트를 배포 하는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-112">This tutorial takes you through the process of deploying an update to your application code.</span></span> <span data-ttu-id="ed61e-113">이 업데이트에는 데이터베이스 변경 내용이 포함 되지 않습니다. 다음 자습서에서 데이터베이스 변경 내용을 배포 하는 것과 관련 된 다른 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-113">This update does not involve a database change; you'll see what's different about deploying a database change in the next tutorial.</span></span>

<span data-ttu-id="ed61e-114">미리 알림: 자습서를 진행할 때 오류 메시지가 표시 되거나 문제가 해결 되지 않으면 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-114">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="making-a-code-change"></a><span data-ttu-id="ed61e-115">코드 변경</span><span class="sxs-lookup"><span data-stu-id="ed61e-115">Making a Code Change</span></span>

<span data-ttu-id="ed61e-116">응용 프로그램에 대 한 업데이트의 간단한 예로, **강사** 페이지에 선택한 강사가 학습 한 과정 목록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-116">As a simple example of an update to your application, you'll add to the **Instructors** page a list of courses taught by the selected instructor.</span></span>

<span data-ttu-id="ed61e-117">**강사** 페이지를 실행 하는 경우 표에 **Select** 링크가 있지만 행 배경이 회색으로 전환 되는 것 외에는 아무것도 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-117">If you run the **Instructors** page, you'll notice that there are **Select** links in the grid, but they don't do anything other than make the row background turn gray.</span></span>

<span data-ttu-id="ed61e-118">[![Instructors_page](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ed61e-118">[![Instructors_page](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image1.png)</span></span>

<span data-ttu-id="ed61e-119">이제 **선택** 링크를 클릭 하면 실행 되는 코드를 추가 하 고 선택한 강사가 학습 한 과정의 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-119">Now you'll add code that runs when the **Select** link is clicked and displays a list of courses taught by the selected instructor .</span></span>

<span data-ttu-id="ed61e-120">*강사 .aspx*에서 **ErrorMessageLabel** `Label` 컨트롤 바로 뒤에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-120">In *Instructors.aspx*, add the following markup immediately after the **ErrorMessageLabel** `Label` control:</span></span>

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample1.aspx)]

<span data-ttu-id="ed61e-121">페이지를 실행 하 고 강사를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-121">Run the page and select an instructor.</span></span> <span data-ttu-id="ed61e-122">강사가 학습 한 과정의 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-122">You see a list of courses taught by that instructor.</span></span>

<span data-ttu-id="ed61e-123">[![Instructors_page_with_courses](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="ed61e-123">[![Instructors_page_with_courses](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image3.png)</span></span>

## <a name="deploying-the-code-update-to-the-test-environment"></a><span data-ttu-id="ed61e-124">테스트 환경에 코드 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="ed61e-124">Deploying the Code Update to the Test Environment</span></span>

<span data-ttu-id="ed61e-125">테스트 환경에 배포 하는 것은 한 번의 클릭으로 게시를 다시 실행 하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-125">Deploying to the test environment is a simple matter of running one-click publish again.</span></span> <span data-ttu-id="ed61e-126">이 프로세스를 빠르게 수행 하기 위해 **웹에서 게시** 도구 모음을 클릭 하 여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-126">To make this process quicker, you can use the **Web One Click Publish** toolbar.</span></span>

<span data-ttu-id="ed61e-127">**보기** 메뉴에서 **도구 모음** 을 선택 하 고 **웹 하나**를 선택 하 여 게시를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-127">In the **View** menu, choose **Toolbars** and then select **Web One Click Publish**.</span></span>

![Selecting_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image5.png)

<span data-ttu-id="ed61e-129">**솔루션 탐색기**에서 ContosoUniversity 프로젝트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-129">In **Solution Explorer**, select the ContosoUniversity project.</span></span>

<span data-ttu-id="ed61e-130">**웹에서 게시** 도구 모음을 클릭 한 다음 **테스트** 게시 프로필을 선택 하 고 **웹 게시** 를 클릭 합니다 (화살표가 왼쪽 및 오른쪽을 가리키는 아이콘).</span><span class="sxs-lookup"><span data-stu-id="ed61e-130">the **Web One Click Publish** toolbar, choose the **Test** publish profile and then click **Publish Web** (the icon with arrows pointing left and right).</span></span>

![Web_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image6.png)

<span data-ttu-id="ed61e-132">Visual Studio는 업데이트 된 응용 프로그램을 배포 하 고 브라우저는 홈 페이지에 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-132">Visual Studio deploys the updated application, and the browser automatically opens to the home page.</span></span> <span data-ttu-id="ed61e-133">강사 페이지를 실행 하 고 강사를 선택 하 여 업데이트가 성공적으로 배포 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-133">Run the Instructors page and select an instructor to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="ed61e-134">[![Instructors_page_with_courses_Test](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="ed61e-134">[![Instructors_page_with_courses_Test](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image7.png)</span></span>

<span data-ttu-id="ed61e-135">또한 일반적으로 재발 테스트를 수행 합니다. 즉, 사이트의 나머지 부분을 테스트 하 여 새 변경으로 인해 기존 기능이 중단 되지 않는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-135">You would normally also do regression testing (that is, test the rest of the site to make sure that the new change didn't break any existing functionality).</span></span> <span data-ttu-id="ed61e-136">그러나이 자습서에서는이 단계를 건너뛰고 업데이트를 프로덕션에 배포 하는 과정을 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-136">But for this tutorial you'll skip that step and proceed to deploy the update to production.</span></span>

## <a name="preventing-redeployment-of-the-initial-database-state-to-production"></a><span data-ttu-id="ed61e-137">프로덕션에 초기 데이터베이스 상태 다시 배포 방지</span><span class="sxs-lookup"><span data-stu-id="ed61e-137">Preventing Redeployment of the Initial Database State to Production</span></span>

<span data-ttu-id="ed61e-138">실제 응용 프로그램에서 사용자는 초기 배포 후 프로덕션 사이트와 상호 작용 하며 데이터베이스는 라이브 데이터로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-138">In a real application, users interact with your production site after your initial deployment, and the databases are populated with live data.</span></span> <span data-ttu-id="ed61e-139">따라서 모든 라이브 데이터를 초기화 하는 초기 상태에서 멤버 자격 데이터베이스를 다시 배포 하는 것을 원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-139">Therefore, you don't want to redeploy the membership database in its initial state, which would wipe out all of the live data.</span></span> <span data-ttu-id="ed61e-140">SQL Server Compact 데이터베이스는 *app\_data* 폴더에 있는 파일 이므로 *앱\_데이터* 폴더의 파일이 배포 되지 않도록 배포 설정을 변경 하 여이를 방지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-140">Since SQL Server Compact databases are files in the *App\_Data* folder, you have to prevent this by changing deployment settings so that files in the *App\_Data* folder aren't deployed.</span></span>

<span data-ttu-id="ed61e-141">ContosoUniversity 프로젝트에 대 한 **프로젝트 속성** 창을 열고 **웹 패키지 및 게시** 탭을 선택 합니다. **구성** 드롭다운 상자에 **활성 (릴리스)** 또는 **릴리스** 가 선택 되어 있는지 확인 하 고, **앱\_데이터 폴더에서 파일 제외**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-141">Open the **Project Properties** window for the ContosoUniversity project, and select the **Package/Publish Web** tab. Make sure that the **Configuration** drop-down box has either **Active (Release)** or **Release** selected, select **Exclude files from the App\_Data folder**.</span></span>

![Exclude_files_from_the_App_Data_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image9.png)

<span data-ttu-id="ed61e-143">나중에 디버그 빌드를 배포 하기로 결정 한 경우 디버그 빌드 구성에 대해 동일한 변경 작업을 수행 하는 것이 좋습니다. **구성** 을 **디버그** 로 변경 하 고 **앱\_데이터 폴더에서 파일 제외**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-143">In case you decide to deploy a debug build in the future, it's a good idea to make the same change for the Debug build configuration: change **Configuration** to **Debug** and then select **Exclude files from the App\_Data folder**.</span></span>

<span data-ttu-id="ed61e-144">**웹 패키지 및 게시** 탭을 저장 하 고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-144">Save and close the **Package/Publish Web** tab.</span></span>

> [!NOTE] 
> 
> [!IMPORTANT]
> <span data-ttu-id="ed61e-145">게시 프로필에서 선택한 **대상에서 추가 파일을 제거** 하지 않았는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-145">Make sure that you don't have **Remove additional files at destination** selected in your publish profiles.</span></span> <span data-ttu-id="ed61e-146">이 옵션을 선택 하면 배포 프로세스에서 앱\_데이터에 포함 된 데이터베이스를 삭제 하 고, 응용 프로그램\_데이터 폴더 자체를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-146">If you select that option, the deployment process will delete the databases that you have in App\_Data in the deployed site, and it will delete the App\_Data folder itself.</span></span>

## <a name="preventing-user-access-to-the-production-site-during-update"></a><span data-ttu-id="ed61e-147">업데이트 중에 프로덕션 사이트에 대 한 사용자 액세스 방지</span><span class="sxs-lookup"><span data-stu-id="ed61e-147">Preventing User Access to the Production Site During Update</span></span>

<span data-ttu-id="ed61e-148">이제 배포 하는 변경 내용이 단일 페이지에 간단 하 게 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-148">The change you're deploying now is a simple change to a single page.</span></span> <span data-ttu-id="ed61e-149">하지만 경우에 따라 대규모 변경 사항을 배포 하는 경우에는 사용자가 배포를 완료 하기 전에 페이지를 요청 하는 경우 사이트가 이상으로 동작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-149">But sometimes you deploy larger changes, and in that case the site can behave strangely if a user requests a page before deployment is finished.</span></span> <span data-ttu-id="ed61e-150">이를 방지 하기 위해 *오프 라인 .htm 파일\_앱* 을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-150">To prevent this, you can use an *app\_offline.htm* file.</span></span> <span data-ttu-id="ed61e-151">응용 프로그램의 루트 폴더에 *app\_* 라는 파일을 배치 하는 경우 IIS는 응용 프로그램을 실행 하는 대신 해당 파일을 자동으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-151">When you put a file named *app\_offline.htm* in the root folder of your application, IIS automatically displays that file instead of running your application.</span></span> <span data-ttu-id="ed61e-152">따라서 배포 중에 액세스를 차단 하려면 앱을 루트 폴더에 *\_오프 라인* 으로 설정 하 고, 배포 프로세스를 실행 한 다음, *응용 프로그램\_오프 라인으로*제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-152">So to prevent access during deployment, you put *app\_offline.htm* in the root folder, run the deployment process, and then remove *app\_offline.htm*.</span></span>

<span data-ttu-id="ed61e-153">**솔루션 탐색기**에서 솔루션 (프로젝트 중 하나가 아님)을 마우스 오른쪽 단추로 클릭 하 고 **새 솔루션 폴더**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-153">In **Solution Explorer**, right-click the solution (not one of the projects) and select **New Solution Folder**.</span></span>

![Creating_a_solution_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image10.png)

<span data-ttu-id="ed61e-155">폴더 이름을 *솔루션*으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-155">Name the folder *SolutionFiles*.</span></span>

<span data-ttu-id="ed61e-156">새 폴더에서 *앱\_오프 라인 .htm*이라는 HTML 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-156">In the new folder create an HTML page named *app\_offline.htm*.</span></span> <span data-ttu-id="ed61e-157">기존 내용을 다음 태그로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-157">Replace the existing contents with the following markup:</span></span>

[!code-html[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample2.html)]

<span data-ttu-id="ed61e-158">호스팅 공급자의 제어판에서 FTP 연결 또는 **파일 관리자** 유틸리티를 사용 하 여 *오프 라인 .htm 파일\_응용 프로그램* 을 사이트에 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-158">You can copy the *app\_offline.htm* file to the site by using an FTP connection or the **File Manager** utility in the hosting provider's control panel.</span></span> <span data-ttu-id="ed61e-159">이 자습서에서는 **파일 관리자**를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-159">For this tutorial, you'll use the **File Manager**.</span></span>

<span data-ttu-id="ed61e-160">[프로덕션 환경에 배포](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) 자습서에서 했던 것 처럼 제어판을 열고 **파일 관리자** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-160">Open the control panel and select **File Manager** as you did in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial.</span></span> <span data-ttu-id="ed61e-161">**Contosouniversity.com** 를 선택한 다음 **wwwroot** 를 선택 하 여 응용 프로그램의 루트 폴더를 가져온 다음 **업로드**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-161">Select **contosouniversity.com** and then **wwwroot** to get to your application's root folder, and then click **Upload**.</span></span>

<span data-ttu-id="ed61e-162">[![Upload_button_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="ed61e-162">[![Upload_button_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image11.png)</span></span>

<span data-ttu-id="ed61e-163">**파일 업로드** 대화 상자에서 *오프 라인 .htm 파일\_앱* 을 선택 하 고 **업로드**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-163">In the **Upload File** dialog box, select the *app\_offline.htm* file and then click **Upload**.</span></span>

<span data-ttu-id="ed61e-164">[![Upload_dialog_box_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="ed61e-164">[![Upload_dialog_box_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image13.png)</span></span>

<span data-ttu-id="ed61e-165">사용 중인 사이트의 URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-165">Browse to your site's URL.</span></span> <span data-ttu-id="ed61e-166">이제 홈 페이지 대신 *앱\_오프 라인 .htm* 페이지가 표시 되는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-166">You see that the *app\_offline.htm* page is now displayed instead of your home page.</span></span>

<span data-ttu-id="ed61e-167">[App_offline ![htm_page_in_production](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="ed61e-167">[![App_offline.htm_page_in_production](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image15.png)</span></span>

<span data-ttu-id="ed61e-168">이제 프로덕션 환경에 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-168">You are now ready to deploy to production.</span></span>

## <a name="deploying-the-code-update-to-the-production-environment"></a><span data-ttu-id="ed61e-169">프로덕션 환경에 코드 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="ed61e-169">Deploying the Code Update to the Production Environment</span></span>

<span data-ttu-id="ed61e-170">웹에서 **게시** 도구 모음을 클릭 한 다음 **프로덕션** 게시 프로필을 선택 하 고 **웹 게시**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-170">In the **Web One Click Publish** toolbar, choose the **Production** publish profile and then click **Publish Web**.</span></span>

<span data-ttu-id="ed61e-171">Visual Studio는 업데이트 된 응용 프로그램을 배포 하 고 사이트의 홈 페이지에 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-171">Visual Studio deploys the updated application and opens the browser to the site's home page.</span></span> <span data-ttu-id="ed61e-172">*앱\_오프 라인 .htm* 파일이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-172">The *app\_offline.htm* file is displayed.</span></span> <span data-ttu-id="ed61e-173">테스트를 완료 하 여 성공적인 배포를 확인 하려면 먼저 *오프 라인 .htm 파일\_앱* 을 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-173">Before you can test to verify successful deployment, you must remove the *app\_offline.htm* file.</span></span>

<span data-ttu-id="ed61e-174">제어판에서 **파일 관리자** 응용 프로그램으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-174">Return to the **File Manager** application in the control panel.</span></span> <span data-ttu-id="ed61e-175">**Contosouniversity.com** 및 **wwwroot**를 선택 하 고 **앱\_오프 라인 .htm**을 선택한 다음 **삭제**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-175">Select **contosouniversity.com** and **wwwroot**, select **app\_offline.htm**, and then click **Delete**.</span></span>

<span data-ttu-id="ed61e-176">[Deleting_app_offline ![](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="ed61e-176">[![Deleting_app_offline.htm](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image17.png)</span></span>

<span data-ttu-id="ed61e-177">브라우저에서 공용 사이트의 강사 페이지를 열고 강사를 선택 하 여 업데이트가 성공적으로 배포 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-177">In the browser, open the Instructors page in the public site, and select an instructor to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="ed61e-178">[![Instructors_page_with_courses_Prod](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="ed61e-178">[![Instructors_page_with_courses_Prod](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image19.png)</span></span>

<span data-ttu-id="ed61e-179">이제 데이터베이스 변경 내용이 포함 되지 않은 응용 프로그램 업데이트를 배포 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-179">You've now deployed an application update that did not involve a database change.</span></span> <span data-ttu-id="ed61e-180">다음 자습서에서는 데이터베이스 변경 내용을 배포 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ed61e-180">The next tutorial shows you how to deploy a database change.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ed61e-181">[이전](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
> [다음](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="ed61e-181">[Previous](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
[Next](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)</span></span>
