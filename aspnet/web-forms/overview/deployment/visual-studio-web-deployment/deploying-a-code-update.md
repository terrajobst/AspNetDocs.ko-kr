---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 코드 업데이트 배포 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 ASP.NET 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자 (usin ...)에 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 02/15/2013
ms.assetid: c76dbc35-a914-4ee3-919c-4f4d1fa05104
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
msc.type: authoredcontent
ms.openlocfilehash: 3881833bfe2a50a38a357614f92f434a04a8ab08
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78457643"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-a-code-update"></a><span data-ttu-id="a883c-103">Visual Studio를 사용 하 여 ASP.NET 웹 배포: 코드 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="a883c-103">ASP.NET Web Deployment using Visual Studio: Deploying a Code Update</span></span>

<span data-ttu-id="a883c-104">만든 사람 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="a883c-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="a883c-105">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="a883c-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="a883c-106">이 자습서 시리즈에서는 Visual Studio 2012 또는 Visual Studio 2010를 사용 하 여 Azure App Service Web Apps 또는 타사 호스팅 공급자에 게 ASP.NET 웹 응용 프로그램을 배포 (게시) 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="a883c-107">계열에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a883c-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="a883c-108">개요</span><span class="sxs-lookup"><span data-stu-id="a883c-108">Overview</span></span>

<span data-ttu-id="a883c-109">초기 배포 후에는 웹 사이트를 유지 관리 하 고 개발 하는 작업이 계속 진행 되며 업데이트를 배포 하는 데 오랜 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-109">After the initial deployment, your work of maintaining and developing your web site continues, and before long you will want to deploy an update.</span></span> <span data-ttu-id="a883c-110">이 자습서는 응용 프로그램 코드에 업데이트를 배포 하는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-110">This tutorial takes you through the process of deploying an update to your application code.</span></span> <span data-ttu-id="a883c-111">이 자습서에서 구현 하 고 배포 하는 업데이트에는 데이터베이스 변경 내용이 포함 되지 않습니다. 다음 자습서에서 데이터베이스 변경 내용을 배포 하는 것과 관련 된 다른 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-111">The update that you implement and deploy in this tutorial does not involve a database change; you'll see what's different about deploying a database change in the next tutorial.</span></span>

<span data-ttu-id="a883c-112">미리 알림: 자습서를 진행할 때 오류 메시지가 표시 되거나 문제가 해결 되지 않으면 [문제 해결 페이지](troubleshooting.md)를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-112">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="make-a-code-change"></a><span data-ttu-id="a883c-113">코드 변경</span><span class="sxs-lookup"><span data-stu-id="a883c-113">Make a code change</span></span>

<span data-ttu-id="a883c-114">응용 프로그램에 대 한 업데이트의 간단한 예로, **강사** 페이지에 선택한 강사가 학습 한 과정 목록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-114">As a simple example of an update to your application, you'll add to the **Instructors** page a list of courses taught by the selected instructor.</span></span>

<span data-ttu-id="a883c-115">**강사** 페이지를 실행 하는 경우 표에 **Select** 링크가 있지만 행 배경이 회색으로 전환 되는 것 외에는 아무것도 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-115">If you run the **Instructors** page, you'll notice that there are **Select** links in the grid, but they don't do anything other than make the row background turn gray.</span></span>

![선택 항목이 있는 강사 페이지](deploying-a-code-update/_static/image1.png)

<span data-ttu-id="a883c-117">이제 **선택** 링크를 클릭 하면 실행 되는 코드를 추가 하 고 선택한 강사가 학습 한 과정의 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-117">Now you'll add code that runs when the **Select** link is clicked and displays a list of courses taught by the selected instructor .</span></span>

1. <span data-ttu-id="a883c-118">*강사 .aspx*에서 **ErrorMessageLabel** `Label` 컨트롤 바로 뒤에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-118">In *Instructors.aspx*, add the following markup immediately after the **ErrorMessageLabel** `Label` control:</span></span>

    [!code-aspx[Main](deploying-a-code-update/samples/sample1.aspx)]
2. <span data-ttu-id="a883c-119">페이지를 실행 하 고 강사를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-119">Run the page and select an instructor.</span></span> <span data-ttu-id="a883c-120">강사가 학습 한 과정의 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-120">You see a list of courses taught by that instructor.</span></span>

    ![학습 코스를 사용 하는 강사 페이지](deploying-a-code-update/_static/image2.png)
3. <span data-ttu-id="a883c-122">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-122">Close the browser.</span></span>

## <a name="deploy-the-code-update-to-the-test-environment"></a><span data-ttu-id="a883c-123">테스트 환경에 코드 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="a883c-123">Deploy the code update to the test environment</span></span>

<span data-ttu-id="a883c-124">게시 프로필을 사용 하 여 테스트, 스테이징 및 프로덕션 환경에 배포 하려면 먼저 데이터베이스 게시 옵션을 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-124">Before you can use your publish profiles to deploy to test, staging, and production, you need to change database publishing options.</span></span> <span data-ttu-id="a883c-125">더 이상 멤버 자격 데이터베이스에 대 한 권한 부여 및 데이터 배포 스크립트를 실행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-125">You no longer need to run the grant and data deployment scripts for the membership database.</span></span>

1. <span data-ttu-id="a883c-126">ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 클릭 하 여 **웹 게시** 마법사를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-126">Open the **Publish Web** wizard by right-clicking the ContosoUniversity project and clicking **Publish**.</span></span>
2. <span data-ttu-id="a883c-127">**프로필** 드롭다운 목록에서 **테스트** 프로필을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-127">Click the **Test** profile in the **Profile** drop-down list.</span></span>
3. <span data-ttu-id="a883c-128">**설정** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-128">Click the **Settings** tab.</span></span>
4. <span data-ttu-id="a883c-129">**데이터베이스** 섹션의 **Defaultconnection** 에서 **데이터베이스 업데이트** 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-129">Under **DefaultConnection** in the **Databases** section, clear the **Update database** check box.</span></span>
5. <span data-ttu-id="a883c-130">**프로필** 탭을 클릭 한 다음 **프로필** 드롭다운 목록에서 **스테이징** 프로필을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-130">Click the **Profile** tab, and then click the **Staging** profile in the **Profile** drop-down list.</span></span>
6. <span data-ttu-id="a883c-131">**테스트** 프로필에 대 한 변경 내용을 저장할지 묻는 메시지가 표시 되 면 **예**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-131">When you are asked if you want to save the changes made to the **Test** profile, click **Yes**.</span></span>
7. <span data-ttu-id="a883c-132">준비 프로필에서 동일한 변경을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-132">Make the same change in the Staging profile.</span></span>
8. <span data-ttu-id="a883c-133">이 프로세스를 반복 하 여 프로덕션 프로필에서 동일한 변경을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-133">Repeat the process to make the same change in the Production profile.</span></span>
9. <span data-ttu-id="a883c-134">**웹 게시** 마법사를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-134">Close the **Publish Web** wizard.</span></span>

<span data-ttu-id="a883c-135">이제 테스트 환경에 배포 하는 것은 한 번의 클릭으로 다시 게시를 실행 하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-135">Deploying to the test environment is now a simple matter of running one-click publish again.</span></span> <span data-ttu-id="a883c-136">이 프로세스를 빠르게 수행 하기 위해 **웹에서 게시** 도구 모음을 클릭 하 여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-136">To make this process quicker, you can use the **Web One Click Publish** toolbar.</span></span>

1. <span data-ttu-id="a883c-137">**보기** 메뉴에서 **도구 모음** 을 선택 하 고 **웹 하나**를 선택 하 여 게시를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-137">In the **View** menu, choose **Toolbars** and then select **Web One Click Publish**.</span></span>

    ![Selecting_One_Click_Publish_toolbar](deploying-a-code-update/_static/image3.png)
2. <span data-ttu-id="a883c-139">**솔루션 탐색기**에서 ContosoUniversity 프로젝트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-139">In **Solution Explorer**, select the ContosoUniversity project.</span></span>
3. <span data-ttu-id="a883c-140">**웹에서 게시** 도구 모음을 클릭 한 다음 **테스트** 게시 프로필을 선택 하 고 **웹 게시** 를 클릭 합니다 (화살표가 왼쪽 및 오른쪽을 가리키는 아이콘).</span><span class="sxs-lookup"><span data-stu-id="a883c-140">the **Web One Click Publish** toolbar, choose the **Test** publish profile and then click **Publish Web** (the icon with arrows pointing left and right).</span></span>

    ![Web_One_Click_Publish_toolbar](deploying-a-code-update/_static/image4.png)
4. <span data-ttu-id="a883c-142">Visual Studio는 업데이트 된 응용 프로그램을 배포 하 고 브라우저는 홈 페이지에 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-142">Visual Studio deploys the updated application, and the browser automatically opens to the home page.</span></span>
5. <span data-ttu-id="a883c-143">강사 페이지를 실행 하 고 강사를 선택 하 여 업데이트가 성공적으로 배포 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-143">Run the Instructors page and select an instructor to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="a883c-144">또한 일반적으로 재발 테스트를 수행 합니다. 즉, 사이트의 나머지 부분을 테스트 하 여 새 변경으로 인해 기존 기능이 중단 되지 않는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-144">You would normally also do regression testing (that is, test the rest of the site to make sure that the new change didn't break any existing functionality).</span></span> <span data-ttu-id="a883c-145">그러나이 자습서에서는이 단계를 건너뛰고 스테이징 및 프로덕션에 업데이트를 배포 하는 과정을 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-145">But for this tutorial you'll skip that step and proceed to deploy the update to staging and production.</span></span>

<span data-ttu-id="a883c-146">를 다시 배포 하면 웹 배포는 변경 된 파일을 자동으로 확인 하 고 변경 된 파일만 서버로 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-146">When you redeploy, Web Deploy automatically determines which files have changed and only copies changed files to the server.</span></span> <span data-ttu-id="a883c-147">기본적으로 웹 배포는 파일에 마지막으로 변경 된 날짜를 사용 하 여 변경 된 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-147">By default, Web Deploy uses last-changed dates on files to determine which ones have changed.</span></span> <span data-ttu-id="a883c-148">일부 원본 제어 시스템은 파일 내용을 변경 하지 않는 경우에도 파일 날짜를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-148">Some source control systems change file dates even when you don't change the file contents.</span></span> <span data-ttu-id="a883c-149">이 경우 파일 체크섬을 사용 하 여 변경 된 파일을 확인 하도록 웹 배포를 구성 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-149">In that case, you might want to configure Web Deploy to use file checksums to determine which files have changed.</span></span> <span data-ttu-id="a883c-150">자세한 내용은 ASP.NET 배포 FAQ에서 [모든 파일을 변경 하지 않았지만 재배포 하는 이유](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a883c-150">For more information, see [Why do all of my files get redeployed although I didn't change them?](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum) in the ASP.NET Deployment FAQ.</span></span>

## <a name="take-the-application-offline-during-deployment"></a><span data-ttu-id="a883c-151">배포 하는 동안 응용 프로그램을 오프 라인 상태로 만들기</span><span class="sxs-lookup"><span data-stu-id="a883c-151">Take the application offline during deployment</span></span>

<span data-ttu-id="a883c-152">이제 배포 하는 변경 내용이 단일 페이지에 간단 하 게 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-152">The change you're deploying now is a simple change to a single page.</span></span> <span data-ttu-id="a883c-153">그러나 경우에 따라 더 큰 변경 내용을 배포 하거나, 코드 및 데이터베이스 변경 내용을 모두 배포 하는 경우, 사용자가 배포를 완료 하기 전에 페이지를 요청 하면 사이트가 제대로 동작 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-153">But sometimes you deploy larger changes, or you deploy both code and database changes, and the site might behave incorrectly if a user requests a page before deployment is finished.</span></span> <span data-ttu-id="a883c-154">배포가 진행 되는 동안 사용자가 사이트에 액세스 하지 못하도록 하려면 *오프 라인 .htm 파일\_앱* 을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-154">To prevent users from accessing the site while deployment is in progress, you can use an *app\_offline.htm* file.</span></span> <span data-ttu-id="a883c-155">응용 프로그램의 루트 폴더에 *app\_* 라는 파일을 배치 하는 경우 IIS는 응용 프로그램을 실행 하는 대신 해당 파일을 자동으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-155">When you put a file named *app\_offline.htm* in the root folder of your application, IIS automatically displays that file instead of running your application.</span></span> <span data-ttu-id="a883c-156">따라서 배포 중에 액세스를 차단 하려면 앱을 루트 폴더에 *\_오프 라인* 으로 전환 하 고 배포 프로세스를 실행 한 후 배포를 완료 한 후에 *앱\_오프 라인으로* 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-156">So to prevent access during deployment, you put *app\_offline.htm* in the root folder, run the deployment process, and then remove *app\_offline.htm* after successful deployment.</span></span>

<span data-ttu-id="a883c-157">배포를 시작할 때 서버에 기본 *앱\_오프 라인 .htm* 파일을 자동으로 배치 하 고 완료 되 면 해당 파일을 제거 하도록 웹 배포를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-157">You can configure Web Deploy to automatically put a default *app\_offline.htm* file on the server when it starts deploying and remove it when it finishes.</span></span> <span data-ttu-id="a883c-158">이렇게 하려면 게시 프로필 (pubxml) 파일에 다음 XML 요소를 추가 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-158">To do that all you have to do is add the following XML element to your publish profile (.pubxml) file:</span></span>

[!code-xml[Main](deploying-a-code-update/samples/sample2.xml)]

<span data-ttu-id="a883c-159">이 자습서의 경우 *오프 라인 .htm 파일\_* 사용자 지정 앱을 만들고 사용 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-159">For this tutorial you'll see how to create and use a custom *app\_offline.htm* file.</span></span>

<span data-ttu-id="a883c-160">스테이징 사이트에 액세스 하는 사용자가 없기 때문에 준비 사이트에서 *앱\_오프 라인* 으로 사용 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-160">Using *app\_offline.htm* in the staging site isn't required, because you don't have users accessing the staging site.</span></span> <span data-ttu-id="a883c-161">그러나 준비를 사용 하 여 프로덕션 환경에서 배포 하려는 모든 항목을 테스트 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-161">But it's a good practice to use staging to test everything the way you plan to deploy in production.</span></span>

### <a name="create-app_offlinehtm"></a><span data-ttu-id="a883c-162">앱\_오프 라인으로 만들기</span><span class="sxs-lookup"><span data-stu-id="a883c-162">Create app\_offline.htm</span></span>

1. <span data-ttu-id="a883c-163">**솔루션 탐색기**에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **추가**를 클릭 한 다음 **새 항목**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-163">In **Solution Explorer**, right-click the solution and click **Add**, and then click **New Item**.</span></span>
2. <span data-ttu-id="a883c-164">*App\_* 이라는 **html 페이지** 를 만듭니다. Visual Studio에서 기본적으로 만드는 *.html* 확장명에서 최종 "l"을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-164">Create an **HTML Page** named *app\_offline.htm* (delete the final "l" in the *.html* extension that Visual Studio creates by default).</span></span>
3. <span data-ttu-id="a883c-165">템플릿 태그를 다음 태그로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-165">Replace the template markup with the following markup:</span></span>

    [!code-html[Main](deploying-a-code-update/samples/sample3.html)]
4. <span data-ttu-id="a883c-166">파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-166">Save and close the file.</span></span>

### <a name="copy-app_offlinehtm-to-the-root-folder-of-the-web-site"></a><span data-ttu-id="a883c-167">응용 프로그램을 웹 사이트의 루트 폴더에\_오프 라인으로 복사</span><span class="sxs-lookup"><span data-stu-id="a883c-167">Copy app\_offline.htm to the root folder of the web site</span></span>

<span data-ttu-id="a883c-168">임의의 FTP 도구를 사용 하 여 웹 사이트에 파일을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-168">You can use any FTP tool to copy files to the web site.</span></span> <span data-ttu-id="a883c-169">[FileZilla](http://filezilla-project.org/) 은 인기 있는 FTP 도구 이며 스크린 샷에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-169">[FileZilla](http://filezilla-project.org/) is a popular FTP tool and is shown in the screen shots.</span></span>

<span data-ttu-id="a883c-170">FTP 도구를 사용 하려면 FTP URL, 사용자 이름 및 암호의 세 가지가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-170">To use an FTP tool, you need three things: the FTP URL, the user name, and the password.</span></span>

<span data-ttu-id="a883c-171">URL은 Azure 관리 포털의 웹 사이트 대시보드 페이지에 표시 되며, FTP의 사용자 이름 및 암호는 앞에서 다운로드 한 *publishsettings* 파일에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-171">The URL is shown on the web site's dashboard page in the Azure Management Portal, and the user name and password for FTP can be found in the *.publishsettings* file that you downloaded earlier.</span></span> <span data-ttu-id="a883c-172">다음 단계에서는 이러한 값을 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-172">The following steps show how to get these values.</span></span>

1. <span data-ttu-id="a883c-173">Azure 관리 포털에서 **웹 사이트** 탭을 클릭 한 다음 스테이징 웹 사이트를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-173">In the Azure Management Portal, click **Web Sites** tab and then click the staging web site.</span></span>
2. <span data-ttu-id="a883c-174">**대시보드** 페이지에서 아래쪽으로 스크롤하여 **빠른** 보기 섹션에서 FTP 호스트 이름을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-174">On the **Dashboard** page, scroll down to find the FTP host name in the **Quick Glance** section.</span></span>

    ![FTP 호스트 이름](deploying-a-code-update/_static/image5.png)
3. <span data-ttu-id="a883c-176">메모장 또는 다른 텍스트 편집기에서 *publishsettings* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-176">Open the staging *.publishsettings* file in Notepad or another text editor.</span></span>
4. <span data-ttu-id="a883c-177">FTP 프로필에 대 한 `publishProfile` 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-177">Find the `publishProfile` element for the FTP profile.</span></span>
5. <span data-ttu-id="a883c-178">`userName` 및 `userPWD` 값을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-178">Copy the `userName` and `userPWD` values.</span></span>

    ![FTP 자격 증명](deploying-a-code-update/_static/image6.png)
6. <span data-ttu-id="a883c-180">FTP 도구를 열고 FTP URL에 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-180">Open your FTP tool and log on to the FTP URL.</span></span>
7. <span data-ttu-id="a883c-181">솔루션 폴더의 *응용 프로그램\_오프 라인 .htm* 을 준비 사이트의 */site/pers* 폴더에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-181">Copy *app\_offline.htm* from the solution folder to the */site/wwwroot* folder in the staging site.</span></span>

    ![App_offline 복사](deploying-a-code-update/_static/image7.png)
8. <span data-ttu-id="a883c-183">준비 사이트의 URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-183">Browse to your staging site's URL.</span></span> <span data-ttu-id="a883c-184">이제 홈 페이지 대신 *앱\_오프 라인 .htm* 페이지가 표시 되는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-184">You see that the *app\_offline.htm* page is now displayed instead of your home page.</span></span>

    ![브라우저 창의 app_offline](deploying-a-code-update/_static/image8.png)

<span data-ttu-id="a883c-186">이제 스테이징에 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-186">You are now ready to deploy to staging.</span></span>

## <a name="deploy-the-code-update-to-staging-and-production"></a><span data-ttu-id="a883c-187">스테이징 및 프로덕션에 코드 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="a883c-187">Deploy the code update to staging and production</span></span>

1. <span data-ttu-id="a883c-188">웹에서 **게시** 도구 모음을 클릭 한 다음 **스테이징** 게시 프로필을 선택 하 고 **웹 게시**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-188">In the **Web One Click Publish** toolbar, choose the **Staging** publish profile and then click **Publish Web**.</span></span>

    <span data-ttu-id="a883c-189">Visual Studio는 업데이트 된 응용 프로그램을 배포 하 고 사이트의 홈 페이지에 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-189">Visual Studio deploys the updated application and opens the browser to the site's home page.</span></span> <span data-ttu-id="a883c-190">*앱\_오프 라인 .htm* 파일이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-190">The *app\_offline.htm* file is displayed.</span></span> <span data-ttu-id="a883c-191">테스트를 완료 하 여 성공적인 배포를 확인 하려면 먼저 *오프 라인 .htm 파일\_앱* 을 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-191">Before you can test to verify successful deployment, you must remove the *app\_offline.htm* file.</span></span>
2. <span data-ttu-id="a883c-192">FTP 도구로 돌아가서 준비 사이트에서 **앱\_오프 라인** 으로 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-192">Return to your FTP tool, and delete **app\_offline.htm** from the staging site.</span></span>
3. <span data-ttu-id="a883c-193">브라우저에서 준비 사이트의 강사 페이지를 열고 강사를 선택 하 여 업데이트가 성공적으로 배포 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-193">In the browser, open the Instructors page in the staging site, and select an instructor to verify that the update was successfully deployed.</span></span>
4. <span data-ttu-id="a883c-194">스테이징 에서처럼 프로덕션에 대해 동일한 절차를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-194">Follow the same procedure for production as you did for staging.</span></span>

<a id="specificfiles"></a>

## <a name="reviewing-changes-and-deploying-specific-files"></a><span data-ttu-id="a883c-195">변경 내용 검토 및 특정 파일 배포</span><span class="sxs-lookup"><span data-stu-id="a883c-195">Reviewing Changes and Deploying Specific Files</span></span>

<span data-ttu-id="a883c-196">Visual Studio 2012는 개별 파일을 배포 하는 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-196">Visual Studio 2012 also gives you the ability to deploy individual files.</span></span> <span data-ttu-id="a883c-197">선택한 파일의 경우 로컬 버전과 배포 된 버전 간의 차이점을 확인 하거나, 대상 환경에 파일을 배포 하거나, 대상 환경에서 로컬 프로젝트로 파일을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-197">For a selected file you can view differences between the local version and the deployed version, deploy the file to the destination environment, or copy the file from the destination environment to the local project.</span></span> <span data-ttu-id="a883c-198">자습서의이 섹션에서는 이러한 기능을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-198">In this section of the tutorial you see how to use these features.</span></span>

### <a name="make-a-change-to-deploy"></a><span data-ttu-id="a883c-199">배포를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-199">Make a change to deploy</span></span>

1. <span data-ttu-id="a883c-200">*Content/사이트인 .css*를 열고 `body` 태그의 블록을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-200">Open *Content/Site.css*, and find the block for the `body` tag.</span></span>
2. <span data-ttu-id="a883c-201">`background-color`의 값을 `#fff`에서 `darkblue`으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-201">Change the value for `background-color` from `#fff` to `darkblue`.</span></span>

    [!code-css[Main](deploying-a-code-update/samples/sample4.css?highlight=2)]

### <a name="view-the-change-in-the-publish-preview-window"></a><span data-ttu-id="a883c-202">게시 미리 보기 창에서 변경 내용 보기</span><span class="sxs-lookup"><span data-stu-id="a883c-202">View the change in the Publish Preview window</span></span>

<span data-ttu-id="a883c-203">**웹 게시** 마법사를 사용 하 여 프로젝트를 게시 하는 경우 **미리 보기** 창에서 파일을 두 번 클릭 하 여 게시 될 변경 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-203">When you use the **Publish Web** wizard to publish the project, you can see what changes are going to be published by double-clicking the file in the **Preview** window.</span></span>

1. <span data-ttu-id="a883c-204">ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-204">Right-click the ContosoUniversity project and click **Publish**.</span></span>
2. <span data-ttu-id="a883c-205">**프로필** 드롭다운 목록에서 **테스트** 게시 프로필을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-205">From the **Profile** drop-down list, select the **Test** publish profile.</span></span>
3. <span data-ttu-id="a883c-206">**미리 보기**를 클릭 한 다음 **미리 보기 시작**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-206">Click **Preview**, and then click **Start Preview**.</span></span>
4. <span data-ttu-id="a883c-207">**미리 보기** 창에서 **사이트 .css**를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-207">In the **Preview** pane, double-click **Site.css**.</span></span>

    ![Site .css를 두 번 클릭 합니다.](deploying-a-code-update/_static/image9.png)

    <span data-ttu-id="a883c-209">**변경 내용 미리 보기** 대화 상자에 배포할 변경 내용에 대 한 미리 보기가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-209">The **Preview changes** dialog shows a preview of the changes that will be deployed.</span></span>

    ![사이트 css에 대 한 변경 내용 미리 보기](deploying-a-code-update/_static/image10.png)

    <span data-ttu-id="a883c-211">*Web.config 파일을* 두 번 클릭 하면 **변경 내용 미리 보기** 대화 상자에 빌드 구성 변환과 게시 프로필 변환의 결과가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-211">If you double-click the *Web.config* file, the **Preview changes** dialog shows the effect of your build configuration transformations and publish profile transformations.</span></span> <span data-ttu-id="a883c-212">이 시점에서 서버에서 *web.config 파일을 변경 하는 작업* 을 수행 하지 않았기 때문에 변경 내용이 표시 되지 않을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-212">At this point you have not done anything that would cause the *Web.config* file on the server to change, so you expect to see no changes.</span></span> <span data-ttu-id="a883c-213">그러나 **변경 내용 미리 보기** 창에는 두 가지 변경 내용이 잘못 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-213">However, the **Preview changes** window incorrectly shows two changes.</span></span> <span data-ttu-id="a883c-214">두 XML 요소가 제거 되는 것 처럼 보입니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-214">It looks like two XML elements will be removed.</span></span> <span data-ttu-id="a883c-215">이러한 요소는 Code First context 클래스에 대해 **응용 프로그램에서 Code First 마이그레이션 실행을** 선택 하면 게시 프로세스를 통해 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-215">These elements are added by the publish process when you select **Execute Code First Migrations on application start** for a Code First context class.</span></span> <span data-ttu-id="a883c-216">비교는 게시 프로세스에서 해당 요소를 추가 하기 전에 수행 되므로 제거 되지 않더라도 제거 되는 것 처럼 보입니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-216">The comparison is done before the publish process adds those elements, so it looks like they are being removed although they will not be removed.</span></span> <span data-ttu-id="a883c-217">이 오류는 이후 릴리스에서 수정 될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-217">This error will be corrected in a future release.</span></span>
5. <span data-ttu-id="a883c-218">**닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-218">Click **Close**.</span></span>
6. <span data-ttu-id="a883c-219">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-219">Click **Publish**.</span></span>
7. <span data-ttu-id="a883c-220">브라우저가 테스트 사이트의 홈 페이지로 열리면 CTRL + F5 키를 눌러 CSS 변경의 영향을 확인 하기 위해 하드 새로 고침을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-220">When the browser opens to the home page of the Test site, press CTRL+F5 to cause a hard refresh in order to see the effect of the CSS change.</span></span>

    ![CSS 변경의 효과](deploying-a-code-update/_static/image11.png)
8. <span data-ttu-id="a883c-222">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-222">Close the browser.</span></span>

### <a name="publish-specific-files-from-solution-explorer"></a><span data-ttu-id="a883c-223">솔루션 탐색기에서 특정 파일 게시</span><span class="sxs-lookup"><span data-stu-id="a883c-223">Publish specific files from Solution Explorer</span></span>

<span data-ttu-id="a883c-224">파란색 배경을 원하지 않고 원래 색으로 되돌려야 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-224">Suppose you don't like the blue background and want to revert to the original color.</span></span> <span data-ttu-id="a883c-225">이 섹션에서는 **솔루션 탐색기**에서 직접 특정 파일을 게시 하 여 원래 설정을 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-225">In this section you'll restore the original settings by publishing a specific file directly from **Solution Explorer**.</span></span>

1. <span data-ttu-id="a883c-226">*Content/사이트인 .css* 를 열고 `background-color` 설정을 `#fff`으로 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-226">Open *Content/Site.css* and restore the `background-color` setting to `#fff`.</span></span>
2. <span data-ttu-id="a883c-227">**솔루션 탐색기**에서 *Content/Site .css* 파일을 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-227">In **Solution Explorer**, right-click the *Content/Site.css* file.</span></span>

    <span data-ttu-id="a883c-228">상황에 맞는 메뉴에는 세 가지 게시 옵션이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-228">The context menu shows three publish options.</span></span>

    ![솔루션 탐색기에서 옵션 게시](deploying-a-code-update/_static/image12.png)
3. <span data-ttu-id="a883c-230">**사이트 css에 대 한 변경 내용 미리 보기를**클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-230">Click **Preview changes to Site.css**.</span></span>

    <span data-ttu-id="a883c-231">로컬 파일과 대상 환경에 있는 버전의 차이점을 보여 주는 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-231">A window opens to show the differences between the local file and the version of it in the destination environment.</span></span>

    ![Diff-Content/Site.css](deploying-a-code-update/_static/image13.png)
4. <span data-ttu-id="a883c-233">**솔루션 탐색기**에서 **site. .css** 를 다시 마우스 오른쪽 단추로 클릭 하 고 **Publish Publish**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-233">In **Solution Explorer**, right-click **Site.css** again and click **Publish Site.css**.</span></span>

    <span data-ttu-id="a883c-234">**웹 게시 작업** 창에 파일이 게시 된 것으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-234">The **Web Publish Activity** window shows that the file has been published.</span></span>

    ![웹 게시 작업 창](deploying-a-code-update/_static/image14.png)
5. <span data-ttu-id="a883c-236">브라우저에서 `http://localhost/contosouniversity` URL을 연 다음 CTRL + f 5를 눌러 CSS 변경의 효과를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-236">Open a browser to the `http://localhost/contosouniversity` URL, and then press CTRL+F5 to cause a hard refresh in order to see the effect of the CSS change.</span></span>

    ![일반 CSS를 사용 하는 홈 페이지](deploying-a-code-update/_static/image15.png)
6. <span data-ttu-id="a883c-238">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-238">Close the browser.</span></span>

## <a name="summary"></a><span data-ttu-id="a883c-239">요약</span><span class="sxs-lookup"><span data-stu-id="a883c-239">Summary</span></span>

<span data-ttu-id="a883c-240">이제 데이터베이스 변경 내용이 포함 되지 않은 응용 프로그램 업데이트를 배포 하는 여러 가지 방법에 대해 알아보았습니다. 변경 사항을 미리 보고 업데이트를 확인 하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-240">You've now seen several ways to deploy an application update that does not involve a database change, and you've seen how to preview the changes to verify that what will be updated is what you expect.</span></span> <span data-ttu-id="a883c-241">강사 페이지에는 이제 학습 된 **강좌가** 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-241">The Instructors page now has a **Courses Taught** section.</span></span>

![학습 코스를 사용 하는 강사 페이지](deploying-a-code-update/_static/image16.png)

<span data-ttu-id="a883c-243">다음 자습서에서는 데이터베이스 변경 내용을 배포 하는 방법을 보여 줍니다. 데이터베이스와 강사 페이지에 생년월일 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a883c-243">The next tutorial shows you how to deploy a database change: you'll add a birthdate field to the database and to the Instructors page.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a883c-244">[이전](deploying-to-production.md)
> [다음](deploying-a-database-update.md)</span><span class="sxs-lookup"><span data-stu-id="a883c-244">[Previous](deploying-to-production.md)
[Next](deploying-a-database-update.md)</span></span>
