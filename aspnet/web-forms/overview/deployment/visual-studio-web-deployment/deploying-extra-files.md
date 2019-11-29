---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 추가 파일 배포 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 ASP.NET 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자 (usin ...)에 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 03/23/2015
ms.assetid: 1cd91055-84bc-42c6-9d80-646f41429d4d
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
msc.type: authoredcontent
ms.openlocfilehash: eaa3141c22980f0c816e2f33b5597ac9fe69c23c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74594902"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-extra-files"></a><span data-ttu-id="58455-103">Visual Studio를 사용 하 여 ASP.NET 웹 배포: 추가 파일 배포</span><span class="sxs-lookup"><span data-stu-id="58455-103">ASP.NET Web Deployment using Visual Studio: Deploying Extra Files</span></span>

<span data-ttu-id="58455-104">만든 사람 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="58455-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="58455-105">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="58455-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="58455-106">이 자습서 시리즈에서는 Visual Studio 2012 또는 Visual Studio 2010를 사용 하 여 Azure App Service Web Apps 또는 타사 호스팅 공급자에 게 ASP.NET 웹 응용 프로그램을 배포 (게시) 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="58455-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="58455-107">계열에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="58455-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="58455-108">개요</span><span class="sxs-lookup"><span data-stu-id="58455-108">Overview</span></span>

<span data-ttu-id="58455-109">이 자습서에서는 Visual Studio 웹 게시 파이프라인을 확장 하 여 배포 하는 동안 추가 작업을 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="58455-109">This tutorial shows how to extend the Visual Studio web publish pipeline to do an additional task during deployment.</span></span> <span data-ttu-id="58455-110">작업은 프로젝트 폴더에 없는 추가 파일을 대상 웹 사이트로 복사 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="58455-110">The task is to copy extra files that are not in the project folder to the destination web site.</span></span>

<span data-ttu-id="58455-111">이 자습서에서는 파일 하나를 *추가 합니다.*</span><span class="sxs-lookup"><span data-stu-id="58455-111">For this tutorial you'll copy one extra file: *robots.txt*.</span></span> <span data-ttu-id="58455-112">이 파일을 스테이징에 배포 하 고 프로덕션에 배포 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="58455-112">You want to deploy this file to staging but not to production.</span></span> <span data-ttu-id="58455-113">[프로덕션에 배포](deploying-to-production.md) 자습서에서이 파일을 프로젝트에 추가 하 고 프로덕션 게시 프로필을 제외 하도록 구성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="58455-113">In [the Deploying to Production](deploying-to-production.md) tutorial, you added this file to the project and configured the Production publish profile to exclude it.</span></span> <span data-ttu-id="58455-114">이 자습서에서는 배포 하려는 모든 파일에 유용 하지만 프로젝트에 포함 하지 않으려는 경우에 유용 하 게 사용할 수 있는 다른 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="58455-114">In this tutorial you'll see an alternative method to handle this situation, one that will be useful for any files that you want to deploy but don't want to include in the project.</span></span>

## <a name="move-the-robotstxt-file"></a><span data-ttu-id="58455-115">로봇 .txt 파일 이동</span><span class="sxs-lookup"><span data-stu-id="58455-115">Move the robots.txt file</span></span>

<span data-ttu-id="58455-116">*로봇 .txt*를 처리 하는 다른 방법을 준비 하기 위해 자습서의이 섹션에서는 파일을 프로젝트에 포함 되지 않은 폴더로 이동 하 고 스테이징 환경에서 *로봇 .txt* 를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="58455-116">To prepare for a different method of handling *robots.txt*, in this section of the tutorial you move the file to a folder that is not included in the project, and you delete *robots.txt* from the staging environment.</span></span> <span data-ttu-id="58455-117">해당 환경에 파일을 배포 하는 새 방법이 제대로 작동 하는지 확인할 수 있도록 준비에서 파일을 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58455-117">It is necessary to delete the file from staging so that you can verify that your new method of deploying the file to that environment is working correctly.</span></span>

1. <span data-ttu-id="58455-118">**솔루션 탐색기**에서, *로봇 .txt* 파일을 마우스 오른쪽 단추로 클릭 하 고 **프로젝트에서 제외**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="58455-118">In **Solution Explorer**, right-click the *robots.txt* file and click **Exclude From Project**.</span></span>
2. <span data-ttu-id="58455-119">Windows 파일 탐색기를 사용 하 여 솔루션 폴더에 새 폴더를 만들고 이름을 *ExtraFiles*로 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="58455-119">Using Windows File Explorer, create a new folder in the solution folder and name it *ExtraFiles*.</span></span>
3. <span data-ttu-id="58455-120">*ContosoUniversity* 프로젝트 폴더에서 *ExtraFiles* 폴더로 *로봇 .txt* 파일을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="58455-120">Move the *robots.txt* file from the *ContosoUniversity* project folder to the *ExtraFiles* folder.</span></span>

    ![ExtraFiles 폴더](deploying-extra-files/_static/image1.png)
4. <span data-ttu-id="58455-122">FTP 도구를 사용 하 여 스테이징 웹 사이트에서 *로봇 .txt* 파일을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="58455-122">Using your FTP tool, delete the *robots.txt* file from the staging web site.</span></span>

    <span data-ttu-id="58455-123">또는 준비 게시 프로필의 **설정** 탭에 있는 **파일 게시 옵션** 에서 **대상에서 추가 파일 제거** 를 선택 하 고 스테이징에 다시 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58455-123">As an alternative, you can select **Remove additional files at destination** under **File Publish Options** on the **Settings** tab of the Staging publish profile, and republish to staging.</span></span>

## <a name="update-the-publish-profile-file"></a><span data-ttu-id="58455-124">게시 프로필 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="58455-124">Update the publish profile file</span></span>

<span data-ttu-id="58455-125">스테이징에는 *로봇이* 필요 하므로 배포 하기 위해 업데이트 해야 하는 게시 프로필은 스테이징입니다.</span><span class="sxs-lookup"><span data-stu-id="58455-125">You only need *robots.txt* in staging, so the only publish profile you need to update in order to deploy it is Staging.</span></span>

1. <span data-ttu-id="58455-126">Visual Studio에서 *준비. pubxml*을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="58455-126">In Visual Studio, open *Staging.pubxml*.</span></span>
2. <span data-ttu-id="58455-127">파일의 끝에서 닫는 `</Project>` 태그 앞에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="58455-127">At the end of the file, before the closing `</Project>` tag, add the following markup:</span></span>

    [!code-xml[Main](deploying-extra-files/samples/sample1.xml)]

    <span data-ttu-id="58455-128">이 코드는 배포할 추가 파일을 수집 하는 새 *대상을* 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="58455-128">This code creates a new *target* that will collect additional files to be deployed.</span></span> <span data-ttu-id="58455-129">대상은 지정 된 조건에 따라 MSBuild에서 실행할 하나 이상의 작업으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58455-129">A target is composed of one or more tasks that MSBuild will execute based on conditions you specify.</span></span>

    <span data-ttu-id="58455-130">`Include` 특성은 프로젝트 폴더와 같은 수준에 있는 파일을 찾을 폴더가 *ExtraFiles*지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="58455-130">The `Include` attribute specifies that the folder in which to find the files is *ExtraFiles*, located at the same level as the project folder.</span></span> <span data-ttu-id="58455-131">MSBuild는 해당 폴더의 모든 파일을 수집 하 고 하위 폴더에서 재귀적으로 모든 파일을 수집 합니다. 이중 별표는 재귀적 하위 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="58455-131">MSBuild will collect all files from that folder and recursively from any subfolders (the double asterisk specifies recursive subfolders).</span></span> <span data-ttu-id="58455-132">이 코드를 사용 하면 여러 파일 및 파일을 *ExtraFiles* 폴더 내에 있는 하위 폴더에 배치할 수 있으며 모두 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58455-132">With this code you could put multiple files, and files in subfolders inside the *ExtraFiles* folder, and all will be deployed.</span></span>

    <span data-ttu-id="58455-133">`DestinationRelativePath` 요소는 폴더와 파일을 *ExtraFiles* 폴더에 있는 것과 동일한 파일 및 폴더 구조에서 대상 웹 사이트의 루트 폴더에 복사 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="58455-133">The `DestinationRelativePath` element specifies that the folders and files should be copied to the root folder of the destination web site, in the same file and folder structure as they are found in the *ExtraFiles* folder.</span></span> <span data-ttu-id="58455-134">*ExtraFiles* 폴더 자체를 복사 하려는 경우 `DestinationRelativePath` 값은 *ExtraFiles\%(RecursiveDir)% (파일 이름)% (확장)* 입니다.</span><span class="sxs-lookup"><span data-stu-id="58455-134">If you wanted to copy the *ExtraFiles* folder itself, the `DestinationRelativePath` value would be *ExtraFiles\%(RecursiveDir)%(Filename)%(Extension)*.</span></span>
3. <span data-ttu-id="58455-135">파일의 끝에서 닫는 `</Project>` 태그 앞에 새 대상을 실행할 시기를 지정 하는 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="58455-135">At the end of the file, before the closing `</Project>` tag, add the following markup that specifies when to execute the new target.</span></span>

    [!code-xml[Main](deploying-extra-files/samples/sample2.xml)]

    <span data-ttu-id="58455-136">이 코드를 실행 하면 대상 폴더에 파일을 복사 하는 대상이 실행 될 때마다 새 `CustomCollectFiles` 대상이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58455-136">This code causes the new `CustomCollectFiles` target to be executed whenever the target that copies files to the destination folder is executed.</span></span> <span data-ttu-id="58455-137">게시 및 배포 패키지 만들기에 대 한 별도의 대상이 있고 게시 대신 배포 패키지를 사용 하 여 배포 하기로 결정 한 경우 새 대상이 두 대상에 모두 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58455-137">There is a separate target for publish versus deployment package creation, and the new target is injected in both targets in case you decide to deploy by using a deployment package instead of publishing.</span></span>

    <span data-ttu-id="58455-138">이제 *pubxml* 파일은 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="58455-138">The *.pubxml* file now looks like the following example:</span></span>

    [!code-xml[Main](deploying-extra-files/samples/sample3.xml?highlight=53-71)]
4. <span data-ttu-id="58455-139">*준비. pubxml* 파일을 저장 하 고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="58455-139">Save and close the *Staging.pubxml* file.</span></span>

## <a name="publish-to-staging"></a><span data-ttu-id="58455-140">스테이징에 게시</span><span class="sxs-lookup"><span data-stu-id="58455-140">Publish to staging</span></span>

<span data-ttu-id="58455-141">한 번 클릭 게시 또는 명령줄을 사용 하 여 스테이징 프로필을 사용 하 여 응용 프로그램을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="58455-141">Using one-click publish or the command line, publish the application by using the Staging profile.</span></span>

<span data-ttu-id="58455-142">한 번 클릭 게시를 사용 하는 경우 **미리 보기** 창에서 *로봇이* 복사 될 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58455-142">If you use one-click publish, you can verify in the **Preview** window that *robots.txt* will be copied.</span></span> <span data-ttu-id="58455-143">그렇지 않으면 FTP 도구를 사용 하 여 배포 후에 웹 사이트의 루트 폴더에 *로봇 .txt* 파일이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="58455-143">Otherwise, use your FTP tool to verify that the *robots.txt* file is in the root folder of the web site after deployment.</span></span>

## <a name="summary"></a><span data-ttu-id="58455-144">요약</span><span class="sxs-lookup"><span data-stu-id="58455-144">Summary</span></span>

<span data-ttu-id="58455-145">이는 ASP.NET 웹 응용 프로그램을 타사 호스팅 공급자에 배포 하는 방법에 대 한 자습서 시리즈를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="58455-145">This completes this series of tutorials on deploying an ASP.NET web application to a third-party hosting provider.</span></span> <span data-ttu-id="58455-146">이러한 자습서에서 설명 하는 항목에 대 한 자세한 내용은 [ASP.NET Deployment Content Map](https://go.microsoft.com/fwlink/p/?LinkId=282413)을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="58455-146">For more information about any of the topics covered in these tutorials, see the [ASP.NET Deployment Content Map](https://go.microsoft.com/fwlink/p/?LinkId=282413).</span></span>

## <a name="more-information"></a><span data-ttu-id="58455-147">추가 정보</span><span class="sxs-lookup"><span data-stu-id="58455-147">More information</span></span>

<span data-ttu-id="58455-148">MSBuild 파일을 사용 하는 방법을 알고 있는 경우에는 *pubxml* 파일 (프로필 관련 작업의 경우) *또는 프로젝트에* 대 한 코드를 작성 하 여 다른 여러 배포 작업을 자동화할 수 있습니다 (모든 프로필에 적용 되는 작업의 경우).</span><span class="sxs-lookup"><span data-stu-id="58455-148">If you know how to work with MSBuild files, you can automate many other deployment tasks by writing code in *.pubxml* files (for profile-specific tasks) or the project *.wpp.targets* file (for tasks that apply to all profiles).</span></span> <span data-ttu-id="58455-149">*Pubxml* 및. n e t *. .targets* 파일에 대 한 자세한 내용은 [방법: Visual Studio 웹 프로젝트의 게시 프로필 (pubxml) 파일 및 Wpp. .Targets 파일에서 배포 설정 편집](https://msdn.microsoft.com/library/ff398069)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="58455-149">For more information about *.pubxml* and *.wpp.targets* files, see [How to: Edit Deployment Settings in Publish Profile (.pubxml) Files and the .wpp.targets File in Visual Studio Web Projects](https://msdn.microsoft.com/library/ff398069).</span></span> <span data-ttu-id="58455-150">MSBuild 코드에 대 한 기본적인 소개는 엔터프라이즈 배포 시리즈의 **프로젝트 파일 분석** [: 프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="58455-150">For a basic introduction to MSBuild code, see **The Anatomy of a Project File** in [Enterprise Deployment Series: Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md).</span></span> <span data-ttu-id="58455-151">MSBuild 파일을 사용 하 여 사용자 고유의 시나리오에 대 한 작업을 수행 하는 방법에 대 한 자세한 내용은 [Microsoft Build Engine 내에서 msbuild 및 Team Foundation Build를 사용 하](http://msbuildbook.com) 여 Sayed Ibraham Hashimi 및 William (영문)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="58455-151">To learn how to work with MSBuild files to perform tasks for your own scenarios, see this book: [Inside the Microsoft Build Engine: Using MSBuild and Team Foundation Build](http://msbuildbook.com) by Sayed Ibraham Hashimi and William Bartholomew.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="58455-152">승인</span><span class="sxs-lookup"><span data-stu-id="58455-152">Acknowledgements</span></span>

<span data-ttu-id="58455-153">이 자습서 시리즈의 내용에 대해 상당한 기여를 수행한 다음 사용자에 게 감사 합니다.</span><span class="sxs-lookup"><span data-stu-id="58455-153">I would like to thank the following people who made significant contributions to the content of this tutorial series:</span></span>

- [<span data-ttu-id="58455-154">Alberto Poblacion, MVP &amp; MCT, 스페인</span><span class="sxs-lookup"><span data-stu-id="58455-154">Alberto Poblacion, MVP &amp; MCT, Spain</span></span>](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- <span data-ttu-id="58455-155">Jarod Ferguson, Data Platform Development MVP, 미국</span><span class="sxs-lookup"><span data-stu-id="58455-155">Jarod Ferguson, Data Platform Development MVP, United States</span></span>
- <span data-ttu-id="58455-156">Microsoft의 거칠게 Mittal</span><span class="sxs-lookup"><span data-stu-id="58455-156">Harsh Mittal, Microsoft</span></span>
- <span data-ttu-id="58455-157">[Jon Galloway](https://weblogs.asp.net/jgalloway) (twitter: [@jongalloway](http://twitter.com/jongalloway))</span><span class="sxs-lookup"><span data-stu-id="58455-157">[Jon Galloway](https://weblogs.asp.net/jgalloway) (twitter: [@jongalloway](http://twitter.com/jongalloway))</span></span>
- [<span data-ttu-id="58455-158">Kristina Olson, Microsoft</span><span class="sxs-lookup"><span data-stu-id="58455-158">Kristina Olson, Microsoft</span></span>](https://blogs.iis.net/krolson/default.aspx)
- [<span data-ttu-id="58455-159">Mike Pope, Microsoft</span><span class="sxs-lookup"><span data-stu-id="58455-159">Mike Pope, Microsoft</span></span>](http://www.mikepope.com/blog/DisplayBlog.aspx)
- <span data-ttu-id="58455-160">Mohit Srivastava, Microsoft</span><span class="sxs-lookup"><span data-stu-id="58455-160">Mohit Srivastava, Microsoft</span></span>
- [<span data-ttu-id="58455-161">Raffaele Rialdi, 이탈리아</span><span class="sxs-lookup"><span data-stu-id="58455-161">Raffaele Rialdi, Italy</span></span>](http://www.iamraf.net/)
- [<span data-ttu-id="58455-162">Rick Anderson, Microsoft</span><span class="sxs-lookup"><span data-stu-id="58455-162">Rick Anderson, Microsoft</span></span>](https://blogs.msdn.com/b/rickandy/)
- <span data-ttu-id="58455-163">[Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))</span><span class="sxs-lookup"><span data-stu-id="58455-163">[Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))</span></span>
- <span data-ttu-id="58455-164">[Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))</span><span class="sxs-lookup"><span data-stu-id="58455-164">[Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))</span></span>
- <span data-ttu-id="58455-165">[Scott 헌터, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))</span><span class="sxs-lookup"><span data-stu-id="58455-165">[Scott Hunter, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))</span></span>
- [<span data-ttu-id="58455-166">Srđan Božović, 세르비아</span><span class="sxs-lookup"><span data-stu-id="58455-166">Srđan Božović, Serbia</span></span>](http://msforge.net/blogs/zmajcek/)
- <span data-ttu-id="58455-167">[인 vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))</span><span class="sxs-lookup"><span data-stu-id="58455-167">[Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="58455-168">[이전](command-line-deployment.md)
> [다음](troubleshooting.md)</span><span class="sxs-lookup"><span data-stu-id="58455-168">[Previous](command-line-deployment.md)
[Next](troubleshooting.md)</span></span>
