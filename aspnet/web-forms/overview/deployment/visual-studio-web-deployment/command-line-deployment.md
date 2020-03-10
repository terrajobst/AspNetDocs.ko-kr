---
uid: web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 명령줄 배포 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 ASP.NET 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자 (usin ...)에 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 82b8dea0-f062-4ee4-8784-3ffa30fbb1ca
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
msc.type: authoredcontent
ms.openlocfilehash: 13cfe4492398b59f2c80394689cc113ccb218c60
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78512075"
---
# <a name="aspnet-web-deployment-using-visual-studio-command-line-deployment"></a><span data-ttu-id="fccfd-103">Visual Studio를 사용 하 여 ASP.NET 웹 배포: 명령줄 배포</span><span class="sxs-lookup"><span data-stu-id="fccfd-103">ASP.NET Web Deployment using Visual Studio: Command Line Deployment</span></span>

<span data-ttu-id="fccfd-104">만든 사람 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="fccfd-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="fccfd-105">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="fccfd-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="fccfd-106">이 자습서 시리즈에서는 Visual Studio 2012 또는 Visual Studio 2010를 사용 하 여 Azure App Service Web Apps 또는 타사 호스팅 공급자에 게 ASP.NET 웹 응용 프로그램을 배포 (게시) 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="fccfd-107">계열에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="fccfd-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="fccfd-108">개요</span><span class="sxs-lookup"><span data-stu-id="fccfd-108">Overview</span></span>

<span data-ttu-id="fccfd-109">이 자습서에서는 명령줄에서 Visual Studio 웹 게시 파이프라인을 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-109">This tutorial shows you how to invoke the Visual Studio web publish pipeline from the command line.</span></span> <span data-ttu-id="fccfd-110">이는 일반적으로 [소스 코드 버전 제어 시스템](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md)을 사용 하 여 Visual Studio에서 수동으로 수행 하는 대신 [배포 프로세스를 자동화](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) 하려는 시나리오에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-110">This is useful for scenarios where you want to [automate the deployment process](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) instead of doing it manually in Visual Studio, typically by using a [source code version control system](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md).</span></span>

## <a name="make-a-change-to-deploy"></a><span data-ttu-id="fccfd-111">배포를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-111">Make a change to deploy</span></span>

<span data-ttu-id="fccfd-112">현재 정보 페이지에 템플릿 코드가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-112">Currently the About page displays the template code.</span></span>

![템플릿 코드가 포함 된 정보 페이지](command-line-deployment/_static/image1.png)

<span data-ttu-id="fccfd-114">학생 등록의 요약을 표시 하는 코드로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-114">You'll replace that with code that displays a summary of student enrollment.</span></span>

<span data-ttu-id="fccfd-115">*About .aspx* 페이지를 열고 `MainContent` `Content` 요소 내의 모든 태그를 삭제 한 후 다음 태그를 해당 위치에 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-115">Open the *About.aspx* page, delete all of the markup inside the `MainContent` `Content` element, and insert the following markup in its place:</span></span>

[!code-aspx[Main](command-line-deployment/samples/sample1.aspx)]

<span data-ttu-id="fccfd-116">프로젝트를 실행 하 고 **정보** 페이지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-116">Run the project and select the **About** page.</span></span>

![[정보] 페이지](command-line-deployment/_static/image2.png)

## <a name="deploy-to-test-by-using-the-command-line"></a><span data-ttu-id="fccfd-118">명령줄을 사용 하 여 테스트에 배포</span><span class="sxs-lookup"><span data-stu-id="fccfd-118">Deploy to Test by using the command line</span></span>

<span data-ttu-id="fccfd-119">다른 데이터베이스 변경 내용을 배포 하지 않으므로 aspnet-ContosoUniversity 데이터베이스에 대해 dbDacFx 데이터베이스 배포를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-119">You won't be deploying another database change, so disable dbDacFx database deployment for the aspnet-ContosoUniversity database.</span></span> <span data-ttu-id="fccfd-120">**웹 게시** 마법사를 열고 세 개의 게시 프로필 각각의 **설정** 탭에서 **데이터베이스 업데이트** 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-120">Open the **Publish Web** wizard, and in each of the three publish profiles, clear the **Update Database** check box on the **Settings** tab.</span></span>

<span data-ttu-id="fccfd-121">Windows 8 시작 페이지에서 **v s 2012에 대 한 개발자 명령 프롬프트**를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-121">In the Windows 8 Start page, search for **Developer Command Prompt for VS2012**.</span></span>

<span data-ttu-id="fccfd-122">**V s 2012에** 대 한 개발자 명령 프롬프트 아이콘을 마우스 오른쪽 단추로 클릭 하 고 **관리자 권한으로 실행**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-122">Right-click the icon for **Developer Command Prompt for VS2012** and click **Run as administrator**.</span></span>

<span data-ttu-id="fccfd-123">명령 프롬프트에서 다음 명령을 입력 하 여 솔루션 파일의 경로를 솔루션 파일의 경로로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-123">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file:</span></span>

[!code-console[Main](command-line-deployment/samples/sample2.cmd)]

<span data-ttu-id="fccfd-124">MSBuild는 솔루션을 빌드하고 테스트 환경에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-124">MSBuild builds the solution and deploys it to the test environment.</span></span>

![명령줄 출력](command-line-deployment/_static/image3.png)

<span data-ttu-id="fccfd-126">브라우저를 열고 `http://localhost/ContosoUniversity`로 이동한 다음 **정보** 페이지를 클릭 하 여 배포가 성공 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-126">Open a browser and go to `http://localhost/ContosoUniversity`, then click the **About** page to verify that the deployment was successful.</span></span>

<span data-ttu-id="fccfd-127">테스트에서 학생을 만들지 않은 경우 **학생 본문 통계** 제목 아래에 빈 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-127">If you haven't created any students in test, you'll see an empty page under the **Student Body Statistics** heading.</span></span> <span data-ttu-id="fccfd-128">**학생 페이지로 이동** 하 여 **학생 추가**를 클릭 하 고, 일부 학생을 추가한 후 **정보** 페이지로 돌아와서 학생 통계를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-128">Go to the **Students** page, click **Add Student**, and add some students, and then return to the **About** page to see student statistics.</span></span>

![테스트 환경의 정보 페이지](command-line-deployment/_static/image4.png)

## <a name="key-command-line-options"></a><span data-ttu-id="fccfd-130">키 명령줄 옵션</span><span class="sxs-lookup"><span data-stu-id="fccfd-130">Key command line options</span></span>

<span data-ttu-id="fccfd-131">입력 한 명령이 솔루션 파일 경로 및 두 개의 속성을 MSBuild에 전달 했습니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-131">The command that you entered passed the solution file path and two properties to MSBuild:</span></span>

[!code-console[Main](command-line-deployment/samples/sample3.cmd)]

### <a name="deploying-the-solution-versus-deploying-individual-projects"></a><span data-ttu-id="fccfd-132">솔루션 배포 및 개별 프로젝트 배포</span><span class="sxs-lookup"><span data-stu-id="fccfd-132">Deploying the solution versus deploying individual projects</span></span>

<span data-ttu-id="fccfd-133">솔루션 파일을 지정 하면 솔루션의 모든 프로젝트가 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-133">Specifying the solution file causes all projects in the solution to be built.</span></span> <span data-ttu-id="fccfd-134">솔루션에 여러 웹 프로젝트가 있는 경우 다음 MSBuild 동작이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-134">If you have multiple web projects in the solution, the following MSBuild behavior applies:</span></span>

- <span data-ttu-id="fccfd-135">명령줄에서 지정 하는 속성은 모든 프로젝트에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-135">The properties that you specify on the command line are passed to every project.</span></span> <span data-ttu-id="fccfd-136">따라서 각 웹 프로젝트에는 사용자가 지정한 이름의 게시 프로필이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-136">Therefore, each web project must have a publish profile with the name that you specify.</span></span> <span data-ttu-id="fccfd-137">`/p:PublishProfile=Test`지정 하는 경우 각 웹 프로젝트에 *Test*라는 게시 프로필이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-137">If you specify `/p:PublishProfile=Test`, each web project must have a publish profile named *Test*.</span></span>
- <span data-ttu-id="fccfd-138">다른 프로젝트를 빌드할 수 없는 경우 한 프로젝트를 성공적으로 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-138">You might successfully publish one project when another one doesn't even build.</span></span> <span data-ttu-id="fccfd-139">자세한 내용은 stackoverflow 스레드 [MSBuild가 두 개의 패키지와 함께 실패](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages)하는 경우를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="fccfd-139">For more information, see the stackoverflow thread [MSBuild fails with two packages](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages).</span></span>

<span data-ttu-id="fccfd-140">솔루션 대신 개별 프로젝트를 지정 하는 경우 Visual Studio 버전을 지정 하는 매개 변수를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-140">If you specify an individual project instead of a solution, you have to add a parameter that specifies the Visual Studio version.</span></span> <span data-ttu-id="fccfd-141">Visual Studio 2012을 사용 하는 경우 명령줄은 다음 예제와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-141">If you are using Visual Studio 2012 the command line would be similar to the following example:</span></span>

[!code-console[Main](command-line-deployment/samples/sample4.cmd?highlight=1)]

<span data-ttu-id="fccfd-142">Visual Studio 2010의 버전 번호는 10.0입니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-142">The version number for Visual Studio 2010 is 10.0.</span></span> <span data-ttu-id="fccfd-143">자세한 내용은 [Visual Studio project compatibility And VisualStudioVersion](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx) On Sayed Hashimi 블로그 (영문)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="fccfd-143">For more information, see [Visual Studio project compatibility and VisualStudioVersion](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx) on Sayed Hashimi's blog.</span></span>

### <a name="specifying-the-publish-profile"></a><span data-ttu-id="fccfd-144">게시 프로필 지정</span><span class="sxs-lookup"><span data-stu-id="fccfd-144">Specifying the publish profile</span></span>

<span data-ttu-id="fccfd-145">다음 예제와 같이 이름이 나 *pubxml* 파일의 전체 경로로 게시 프로필을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-145">You can specify the publish profile by name or by the full path to the *.pubxml* file, as shown in the following example:</span></span>

[!code-console[Main](command-line-deployment/samples/sample5.cmd?highlight=1)]

### <a name="web-publish-methods-supported-for-command-line-publishing"></a><span data-ttu-id="fccfd-146">명령줄 게시에 대해 지원 되는 웹 게시 방법</span><span class="sxs-lookup"><span data-stu-id="fccfd-146">Web publish methods supported for command-line publishing</span></span>

<span data-ttu-id="fccfd-147">명령줄 게시에는 세 가지 게시 방법이 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-147">Three publish methods are supported for command line publishing:</span></span>

- <span data-ttu-id="fccfd-148">`MSDeploy`-웹 배포를 사용 하 여 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-148">`MSDeploy` - Publish by using Web Deploy.</span></span>
- <span data-ttu-id="fccfd-149">`Package`-웹 배포 패키지를 만들어 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-149">`Package` - Publish by creating a Web Deploy Package.</span></span> <span data-ttu-id="fccfd-150">패키지를 만드는 MSBuild 명령과 별도로 패키지를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-150">You have to install the package separately from the MSBuild command that creates it.</span></span>
- <span data-ttu-id="fccfd-151">`FileSystem`-지정 된 폴더에 파일을 복사 하 여 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-151">`FileSystem` - Publish by copying files to a specified folder.</span></span>

### <a name="specifying-the-build-configuration-and-platform"></a><span data-ttu-id="fccfd-152">빌드 구성 및 플랫폼 지정</span><span class="sxs-lookup"><span data-stu-id="fccfd-152">Specifying the build configuration and platform</span></span>

<span data-ttu-id="fccfd-153">Visual Studio 또는 명령줄에서 빌드 구성 및 플랫폼을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-153">The build configuration and platform must be set in Visual Studio or on the command line.</span></span> <span data-ttu-id="fccfd-154">게시 프로필에는 `LastUsedBuildConfiguration` 및 `LastUsedPlatform`라는 속성이 포함 되지만, 프로젝트가 빌드되는 방식을 결정 하기 위해 이러한 속성을 설정할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-154">The publish profiles include properties that are named `LastUsedBuildConfiguration` and `LastUsedPlatform`, but you can't set these properties in order to determine how the project is built.</span></span> <span data-ttu-id="fccfd-155">자세한 내용은 MSBuild: Sayed Hashimi의 블로그에서 [구성 속성을 설정 하는 방법](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="fccfd-155">For more information, see [MSBuild: how to set the configuration property](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx) on Sayed Hashimi's blog.</span></span>

## <a name="deploy-to-staging"></a><span data-ttu-id="fccfd-156">스테이징에 배포</span><span class="sxs-lookup"><span data-stu-id="fccfd-156">Deploy to staging</span></span>

<span data-ttu-id="fccfd-157">Azure에 배포 하려면 명령줄에 암호를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-157">To deploy to Azure, you must add the password to the command line.</span></span> <span data-ttu-id="fccfd-158">Visual Studio의 게시 프로필에 암호를 저장 한 경우 해당 암호는 *pubxml 사용자* 파일에 암호화 된 형식으로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-158">If you saved the password in the publish profile in Visual Studio, it was stored in encrypted form in the your *.pubxml.user* file.</span></span> <span data-ttu-id="fccfd-159">명령줄 배포를 수행할 때 MSBuild에서 해당 파일에 액세스할 수 없으므로 명령줄 매개 변수에서 암호를 전달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-159">That file is not accessed by MSBuild when you do a command line deployment, so you have to pass in the password in a command line parameter.</span></span>

1. <span data-ttu-id="fccfd-160">준비 웹 사이트에 대해 이전에 다운로드 한 *publishsettings* 파일에서 필요한 암호를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-160">Copy the password that you need from the *.publishsettings* file that you downloaded earlier for the staging web site.</span></span> <span data-ttu-id="fccfd-161">암호는 웹 배포 `publishProfile` 요소에 대 한 `userPWD` 특성의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-161">The password is the value of the `userPWD` attribute for the Web Deploy `publishProfile` element.</span></span>

    ![웹 배포 암호](command-line-deployment/_static/image5.png)
2. <span data-ttu-id="fccfd-163">Windows 8 시작 페이지에서 **v s 2012에 대 한 개발자 명령 프롬프트**를 검색 하 고 아이콘을 클릭 하 여 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-163">In the Windows 8 Start page, search for **Developer Command Prompt for VS2012**, and click the icon to open the command prompt.</span></span> <span data-ttu-id="fccfd-164">(로컬 컴퓨터에서 IIS에 배포 하지 않으므로 이번에는 관리자 권한으로 열 필요가 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="fccfd-164">(You don't have to open it as administrator this time because you aren't deploying to IIS on the local computer.)</span></span>
3. <span data-ttu-id="fccfd-165">명령 프롬프트에서 다음 명령을 입력 하 여 솔루션 파일의 경로를 솔루션 파일의 경로로 바꾸고 암호를 사용 하 여 암호를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-165">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file and the password with your password:</span></span>

    [!code-console[Main](command-line-deployment/samples/sample6.cmd)]

    <span data-ttu-id="fccfd-166">이 명령줄에는 `/p:AllowUntrustedCertificate=true`추가 매개 변수가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-166">Notice that this command line includes an extra parameter: `/p:AllowUntrustedCertificate=true`.</span></span> <span data-ttu-id="fccfd-167">이 자습서를 작성 하는 동안 명령줄에서 Azure에 게시할 때 `AllowUntrustedCertificate` 속성을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-167">As this tutorial is being written, the `AllowUntrustedCertificate` property must be set when you publish to Azure from the command line.</span></span> <span data-ttu-id="fccfd-168">이 버그에 대 한 수정이 해제 되 면 해당 매개 변수는 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-168">When the fix for this bug is released, you won't need that parameter.</span></span>
4. <span data-ttu-id="fccfd-169">브라우저를 열고 준비 사이트의 URL로 이동한 다음 **정보** 페이지를 클릭 하 여 배포에 성공 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-169">Open a browser and go to the URL of your staging site, and then click the **About** page to verify that the deployment was successful.</span></span>

    <span data-ttu-id="fccfd-170">앞에서 설명한 것 처럼 테스트 환경에 대 한 몇 가지 학생을 만들어 **정보** 페이지에 대 한 통계를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-170">As you saw earlier for the test environment, you might have to create some students to see statistics on the **About** page.</span></span>

## <a name="deploy-to-production"></a><span data-ttu-id="fccfd-171">프로덕션에 배포</span><span class="sxs-lookup"><span data-stu-id="fccfd-171">Deploy to production</span></span>

<span data-ttu-id="fccfd-172">프로덕션에 배포 하는 프로세스는 스테이징 프로세스와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-172">The process for deploying to production is similar to the process for staging.</span></span>

1. <span data-ttu-id="fccfd-173">프로덕션 웹 사이트에 대해 이전에 다운로드 한 *publishsettings* 파일에서 필요한 암호를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-173">Copy the password that you need from the *.publishsettings* file that you downloaded earlier for the production web site.</span></span>
2. <span data-ttu-id="fccfd-174">**V s 2012에 대 한 개발자 명령 프롬프트를**엽니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-174">Open **Developer Command Prompt for VS2012**.</span></span>
3. <span data-ttu-id="fccfd-175">명령 프롬프트에서 다음 명령을 입력 하 여 솔루션 파일의 경로를 솔루션 파일의 경로로 바꾸고 암호를 사용 하 여 암호를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-175">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file and the password with your password:</span></span>

    [!code-console[Main](command-line-deployment/samples/sample7.cmd)]

    <span data-ttu-id="fccfd-176">실제 프로덕션 사이트의 경우 데이터베이스가 변경 된 경우 일반적으로 응용 프로그램을 배포 하기 전에 *오프 라인 .htm 파일\_* 사이트에 복사 하 고 성공적인 배포 후에 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-176">For a real production site, if there was also a database change, you would typically copy the *app\_offline.htm* file to the site before deployment and delete it after successful deployment.</span></span>
4. <span data-ttu-id="fccfd-177">브라우저를 열고 준비 사이트의 URL로 이동한 다음 **정보** 페이지를 클릭 하 여 배포에 성공 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-177">Open a browser and go to the URL of your staging site, and then click the **About** page to verify that the deployment was successful.</span></span>

## <a name="summary"></a><span data-ttu-id="fccfd-178">요약</span><span class="sxs-lookup"><span data-stu-id="fccfd-178">Summary</span></span>

<span data-ttu-id="fccfd-179">이제 명령줄을 사용 하 여 응용 프로그램 업데이트를 배포 했습니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-179">You have now deployed an application update by using the command line.</span></span>

![테스트 환경의 정보 페이지](command-line-deployment/_static/image6.png)

<span data-ttu-id="fccfd-181">다음 자습서에는 웹 게시 파이프라인을 확장 하는 방법의 예제가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-181">In the next tutorial, you will see an example of how to extend the web publish pipeline.</span></span> <span data-ttu-id="fccfd-182">이 예제에서는 프로젝트에 포함 되지 않은 파일을 배포 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fccfd-182">The example will show you how to deploy files that are not included in the project.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="fccfd-183">[이전](deploying-a-database-update.md)
> [다음](deploying-extra-files.md)</span><span class="sxs-lookup"><span data-stu-id="fccfd-183">[Previous](deploying-a-database-update.md)
[Next](deploying-extra-files.md)</span></span>
