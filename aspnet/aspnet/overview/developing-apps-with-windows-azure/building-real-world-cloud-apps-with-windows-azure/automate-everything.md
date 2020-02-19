---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
title: 모든 항목 자동화 (Azure를 사용 하 여 실제 클라우드 앱 빌드) | Microsoft Docs
author: MikeWasson
description: Azure e-learning을 사용 하 여 실제 클라우드 앱 빌드는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 여기에는 다음을 수행할 수 있는 13 개의 패턴과 사례가 설명 되어 있습니다.
ms.author: riande
ms.date: 06/12/2014
ms.assetid: ba6e6baa-9b9f-471f-b39d-b007a3addadc
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
msc.type: authoredcontent
ms.openlocfilehash: e741a753a36ebdaefbff8eee0b38911785c716ac
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457169"
---
# <a name="automate-everything-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="94878-104">모든 항목 자동화 (Azure를 사용 하 여 실제 클라우드 앱 빌드)</span><span class="sxs-lookup"><span data-stu-id="94878-104">Automate Everything (Building Real-World Cloud Apps with Azure)</span></span>

<span data-ttu-id="94878-105">사람, [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="94878-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="94878-106">[Fix It 프로젝트 다운로드](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자 서적 다운로드](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="94878-106">[Download Fix It Project](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="94878-107">Azure e-learning을 **사용 하 여 실제 클라우드 앱 빌드** 는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="94878-108">클라우드의 웹 앱을 성공적으로 개발 하는 데 도움이 되는 13 개의 패턴 및 사례에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="94878-109">전자 문서에 대 한 소개는 [첫 번째 챕터](introduction.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="94878-109">For an introduction to the e-book, see [the first chapter](introduction.md).</span></span>

<span data-ttu-id="94878-110">처음에는 소프트웨어 개발 프로젝트에 실제로 적용 되는 세 가지 패턴이 있습니다. 특히 클라우드 프로젝트에도 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94878-110">The first three patterns we'll look at actually apply to any software development project, but especially to cloud projects.</span></span> <span data-ttu-id="94878-111">이 패턴은 개발 작업 자동화에 대 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="94878-111">This pattern is about automating development tasks.</span></span> <span data-ttu-id="94878-112">수동 프로세스가 느리고 오류가 발생 하기 쉬우므로 중요 한 항목입니다. 최대한 많은 항목을 최대한으로 자동화 하면 빠르고 안정적 이며 민첩 한 워크플로를 설정 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94878-112">It's an important topic because manual processes are slow and error-prone; automating as many of them as possible helps set up a fast, reliable, and agile workflow.</span></span> <span data-ttu-id="94878-113">온-프레미스 환경에서 자동화 하기가 어렵거나 불가능 한 많은 작업을 쉽게 자동화할 수 있으므로 클라우드 개발에는 고유 하 게 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-113">It's uniquely important for cloud development because you can easily automate many tasks that are difficult or impossible to automate in an on-premises environment.</span></span> <span data-ttu-id="94878-114">예를 들어 새 웹 서버와 백 엔드 Vm, 데이터베이스, blob 저장소 (파일 저장소), 큐 등을 비롯 한 전체 테스트 환경을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-114">For example, you can set up whole test environments including new web server and back-end VMs, databases, blob storage (file storage), queues, etc.</span></span>

## <a name="devops-workflow"></a><span data-ttu-id="94878-115">DevOps 워크플로</span><span class="sxs-lookup"><span data-stu-id="94878-115">DevOps Workflow</span></span>

<span data-ttu-id="94878-116">"DevOps" 라는 용어가 점점 늘어나고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-116">Increasingly you hear the term "DevOps."</span></span> <span data-ttu-id="94878-117">소프트웨어를 효율적으로 개발 하기 위해 개발 및 운영 작업을 통합 해야 한다는 인식을 통해 개발 된 용어입니다.</span><span class="sxs-lookup"><span data-stu-id="94878-117">The term developed out of a recognition that you have to integrate development and operations tasks in order to develop software efficiently.</span></span> <span data-ttu-id="94878-118">사용 하도록 설정할 워크플로의 종류는 앱을 개발 하 고, 배포 하 고, 프로덕션 환경에서 학습 하 고, 학습 한 내용에 대 한 응답으로 변경 하 고, 빠르고 안정적으로 주기를 반복 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="94878-118">The kind of workflow you want to enable is one in which you can develop an app, deploy it, learn from production usage of it, change it in response to what you've learned, and repeat the cycle quickly and reliably.</span></span>

<span data-ttu-id="94878-119">일부 성공적인 클라우드 개발 팀은 하루에 여러 번 라이브 환경에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-119">Some successful cloud development teams deploy multiple times a day to a live environment.</span></span> <span data-ttu-id="94878-120">Azure 팀은 2-3 개월 마다 주요 업데이트를 배포 하는 데 사용 되지만, 이제 2-3 일 마다 및 주 2-3 릴리스 마다 몇 분 마다 업데이트를 릴리스 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-120">The Azure team used to deploy a major update every 2-3 months, but now it releases minor updates every 2-3 days and major releases every 2-3 weeks.</span></span> <span data-ttu-id="94878-121">이러한 흐름을 가져오면 고객 피드백에 응답 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94878-121">Getting into that cadence really helps you be responsive to customer feedback.</span></span>

<span data-ttu-id="94878-122">이렇게 하려면 반복 가능 하 고 안정적 이며 예측 가능 하며 주기 시간이 낮은 개발 및 배포 주기를 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-122">In order to do that, you have to enable a development and deployment cycle that is repeatable, reliable, predictable, and has low cycle time.</span></span>

![DevOps 워크플로](automate-everything/_static/image1.png)

<span data-ttu-id="94878-124">즉, 기능에 대해 아이디어를 사용 하 고 고객을 사용 하 고 피드백을 제공 하는 시간 사이의 기간은 가능한 한 짧아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-124">In other words, the period of time between when you have an idea for a feature and when the customers are using it and providing feedback must be as short as possible.</span></span> <span data-ttu-id="94878-125">처음 세 가지 패턴 (모든 것, 소스 제어 및 연속 통합 및 배달 자동화)은 이러한 종류의 프로세스를 사용 하기 위해 권장 되는 모범 사례에 대 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="94878-125">The first three patterns – automate everything, source control, and continuous integration and delivery -- are all about best practices that we recommend in order to enable that kind of process.</span></span>

## <a name="azure-management-scripts"></a><span data-ttu-id="94878-126">Azure 관리 스크립트</span><span class="sxs-lookup"><span data-stu-id="94878-126">Azure management scripts</span></span>

<span data-ttu-id="94878-127">[이 e-learning 소개](introduction.md)에서는 웹 기반 콘솔 인 Azure 관리 포털를 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-127">In the [introduction to this e-book](introduction.md), you saw the web-based console, the Azure Management Portal.</span></span> <span data-ttu-id="94878-128">관리 포털을 사용 하면 Azure에 배포한 모든 리소스를 모니터링 하 고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-128">The management portal enables you to monitor and manage all of the resources that you have deployed on Azure.</span></span> <span data-ttu-id="94878-129">웹 앱 및 Vm과 같은 서비스를 만들고 삭제 하 고, 서비스를 구성 하 고, 서비스 작업을 모니터링 하는 등의 작업을 수행 하는 쉬운 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="94878-129">It's an easy way to create and delete services such as web apps and VMs, configure those services, monitor service operation, and so forth.</span></span> <span data-ttu-id="94878-130">훌륭한 도구 이지만이를 사용 하는 것은 수동 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="94878-130">It's a great tool, but using it is a manual process.</span></span> <span data-ttu-id="94878-131">팀 환경에서 모든 규모의 프로덕션 응용 프로그램을 개발 하려는 경우에는 Azure를 학습 하 고 탐색 한 다음 반복적으로 수행 하는 프로세스를 자동화 하기 위해 포털 UI를 진행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-131">If you're going to develop a production application of any size, and especially in a team environment, we recommend that you go through the portal UI in order to learn and explore Azure, and then automate the processes that you'll be doing repetitively.</span></span>

<span data-ttu-id="94878-132">관리 포털 또는 Visual Studio에서 수동으로 수행할 수 있는 거의 모든 작업은 REST 관리 API를 호출 하 여 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-132">Nearly everything that you can do manually in the management portal or from Visual Studio can also be done by calling the REST management API.</span></span> <span data-ttu-id="94878-133">[Windows PowerShell](https://msdn.microsoft.com/library/windowsazure/jj156055.aspx)을 사용 하 여 스크립트를 작성 하거나 [Chef](http://www.opscode.com/chef/) 또는 [퍼핏](http://puppetlabs.com/puppet/what-is-puppet)와 같은 오픈 소스 프레임 워크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-133">You can write scripts using [Windows PowerShell](https://msdn.microsoft.com/library/windowsazure/jj156055.aspx), or you can use an open source framework such as [Chef](http://www.opscode.com/chef/) or [Puppet](http://puppetlabs.com/puppet/what-is-puppet).</span></span> <span data-ttu-id="94878-134">Mac 또는 Linux 환경에서 Bash 명령줄 도구를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-134">You can also use the Bash command-line tool in a Mac or Linux environment.</span></span> <span data-ttu-id="94878-135">Azure는 이러한 다양 한 환경에 대 한 스크립팅 Api를 포함 하 고 있으며 스크립트 대신 코드를 작성 하려는 경우에 [.net 관리 api](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx) 를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-135">Azure has scripting APIs for all those different environments, and it has a [.NET management API](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx) in case you want to write code instead of script.</span></span>

<span data-ttu-id="94878-136">Fix It 앱의 경우 테스트 환경을 만들고 해당 환경에 프로젝트를 배포 하는 프로세스를 자동화 하는 Windows PowerShell 스크립트를 만들었습니다. 이러한 스크립트의 내용 중 일부를 검토해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-136">For the Fix It app we've created some Windows PowerShell scripts that automate the processes of creating a test environment and deploying the project to that environment, and we'll review some of the contents of those scripts.</span></span>

## <a name="environment-creation-script"></a><span data-ttu-id="94878-137">환경 만들기 스크립트</span><span class="sxs-lookup"><span data-stu-id="94878-137">Environment creation script</span></span>

<span data-ttu-id="94878-138">여기서 살펴볼 첫 번째 스크립트의 이름은 *New-AzureWebsiteEnv*입니다.</span><span class="sxs-lookup"><span data-stu-id="94878-138">The first script we'll look at is named *New-AzureWebsiteEnv.ps1*.</span></span> <span data-ttu-id="94878-139">테스트를 위해 Fix It 앱을 배포할 수 있는 Azure 환경을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94878-139">It creates an Azure environment that you can deploy the Fix It app to for testing.</span></span> <span data-ttu-id="94878-140">이 스크립트에서 수행 하는 주요 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-140">The main tasks that this script performs are the following:</span></span>

- <span data-ttu-id="94878-141">웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94878-141">Create a web app.</span></span>
- <span data-ttu-id="94878-142">스토리지 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94878-142">Create a storage account.</span></span> <span data-ttu-id="94878-143">(Blob 및 큐에 필요 합니다. 이후 단원에서 볼 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="94878-143">(Required for blobs and queues, as you'll see in later chapters.)</span></span>
- <span data-ttu-id="94878-144">SQL Database 서버와 두 개의 데이터베이스 (응용 프로그램 데이터베이스 및 멤버 자격 데이터베이스)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94878-144">Create a SQL Database server and two databases: an application database, and a membership database.</span></span>
- <span data-ttu-id="94878-145">앱이 저장소 계정 및 데이터베이스에 액세스 하는 데 사용할 수 있는 설정을 Azure에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-145">Store settings in Azure that the app will use to access the storage account and databases.</span></span>
- <span data-ttu-id="94878-146">배포를 자동화 하는 데 사용 되는 설정 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94878-146">Create settings files that will be used to automate deployment.</span></span>

### <a name="run-the-script"></a><span data-ttu-id="94878-147">스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="94878-147">Run the script</span></span>

> [!NOTE]
> <span data-ttu-id="94878-148">이 장에서는 스크립트 및 스크립트 실행을 위해 입력 하는 명령에 대 한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="94878-148">This part of the chapter shows examples of scripts and the commands that you enter in order to run them.</span></span> <span data-ttu-id="94878-149">이 데모에서는 스크립트를 실행 하기 위해 알아야 할 모든 사항을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-149">This a demo and doesn't provide everything you need to know in order to run the scripts.</span></span> <span data-ttu-id="94878-150">단계별 방법에 대 한 지침은 [부록: Fix It 샘플 응용 프로그램](the-fix-it-sample-application.md#deploybase)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="94878-150">For step-by-step how-to-do-it instructions, see [Appendix: The Fix It Sample Application](the-fix-it-sample-application.md#deploybase).</span></span>

<span data-ttu-id="94878-151">Azure 서비스를 관리 하는 PowerShell 스크립트를 실행 하려면 Azure PowerShell 콘솔을 설치 하 고 Azure 구독을 사용 하도록 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-151">To run a PowerShell script that manages Azure services you have to install the Azure PowerShell console and configure it to work with your Azure subscription.</span></span> <span data-ttu-id="94878-152">설정이 완료 되 면 다음과 같은 명령을 사용 하 여 It 환경 생성 수정 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-152">Once you're set up, you can run the Fix It environment creation script with a command like this one:</span></span>

`.\New-AzureWebsiteEnv.ps1 -Name <websitename> -SqlDatabasePassword <password>`

<span data-ttu-id="94878-153">`Name` 매개 변수는 데이터베이스 및 저장소 계정을 만들 때 사용할 이름을 지정 하 고, `SqlDatabasePassword` 매개 변수는 SQL Database에 대해 생성 되는 관리자 계정의 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-153">The `Name` parameter specifies the name to be used when creating the database and storage accounts, and the `SqlDatabasePassword` parameter specifies the password for the admin account that will be created for SQL Database.</span></span> <span data-ttu-id="94878-154">나중에 살펴볼 수 있는 다른 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-154">There are other parameters you can use that we'll look at later.</span></span>

![PowerShell 창](automate-everything/_static/image2.png)

<span data-ttu-id="94878-156">스크립트가 완료 되 면 관리 포털에서 만들어진 항목을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-156">After the script finishes you can see in the management portal what was created.</span></span> <span data-ttu-id="94878-157">두 개의 데이터베이스를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-157">You'll find two databases:</span></span>

![데이터베이스](automate-everything/_static/image3.png)

<span data-ttu-id="94878-159">저장소 계정:</span><span class="sxs-lookup"><span data-stu-id="94878-159">A storage account:</span></span>

![스토리지 계정](automate-everything/_static/image4.png)

<span data-ttu-id="94878-161">웹 앱:</span><span class="sxs-lookup"><span data-stu-id="94878-161">And a web app:</span></span>

![웹 사이트](automate-everything/_static/image5.png)

<span data-ttu-id="94878-163">웹 앱에 대 한 **구성** 탭에서 저장소 계정 설정 및 Fix it 앱에 대 한 SQL database 연결 문자열을 설정 하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-163">On the **Configure** tab for the web app, you can see that it has the storage account settings and SQL database connection strings set up for the Fix It app.</span></span>

![appSettings 및 connectionStrings](automate-everything/_static/image6.png)

<span data-ttu-id="94878-165">이제 *Automation* 폴더에 *&lt;websitename&gt;pubxml* 파일이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-165">The *Automation* folder now also contains a *&lt;websitename&gt;.pubxml* file.</span></span> <span data-ttu-id="94878-166">이 파일에는 MSBuild에서 방금 만든 Azure 환경에 응용 프로그램을 배포 하는 데 사용 하는 설정이 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94878-166">This file stores settings that MSBuild will use to deploy the application to the Azure environment that was just created.</span></span> <span data-ttu-id="94878-167">다음은 그 예입니다.</span><span class="sxs-lookup"><span data-stu-id="94878-167">For example:</span></span>

[!code-xml[Main](automate-everything/samples/sample1.xml)]

<span data-ttu-id="94878-168">여기에서 볼 수 있듯이 스크립트는 전체 테스트 환경을 만들었으며 전체 프로세스는 약 90 초 내에 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94878-168">As you can see, the script has created a complete test environment, and the whole process is done in about 90 seconds.</span></span>

<span data-ttu-id="94878-169">팀의 다른 사용자가 테스트 환경을 만들려는 경우 스크립트를 실행 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94878-169">If someone else on your team wants to create a test environment, they can just run the script.</span></span> <span data-ttu-id="94878-170">뿐만 아니라 사용 중인 환경과 동일한 환경을 사용 하는 것을 확신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-170">Not only is it fast, but also they can be confident that they are using an environment identical to the one you're using.</span></span> <span data-ttu-id="94878-171">관리 포털 UI를 사용 하 여 모든 사용자가 수동으로 설정 하는 경우에는 확실 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-171">You couldn't be quite as confident of that if everyone was setting things up manually by using the management portal UI.</span></span>

### <a name="a-look-at-the-scripts"></a><span data-ttu-id="94878-172">스크립트 살펴보기</span><span class="sxs-lookup"><span data-stu-id="94878-172">A look at the scripts</span></span>

<span data-ttu-id="94878-173">실제로이 작업을 수행 하는 세 가지 스크립트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-173">There are actually three scripts that do this work.</span></span> <span data-ttu-id="94878-174">명령줄에서 하나를 호출 하 고 다른 두 항목을 자동으로 사용 하 여 일부 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-174">You call one from the command line and it automatically uses the other two to do some of the tasks:</span></span>

- <span data-ttu-id="94878-175">*New-AzureWebSiteEnv* 는 기본 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="94878-175">*New-AzureWebSiteEnv.ps1* is the main script.</span></span>

    - <span data-ttu-id="94878-176">*New-AzureStorage* 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94878-176">*New-AzureStorage.ps1* creates the storage account.</span></span>
    - <span data-ttu-id="94878-177">*New-AzureSql* 는 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94878-177">*New-AzureSql.ps1* creates the databases.</span></span>

### <a name="parameters-in-the-main-script"></a><span data-ttu-id="94878-178">주 스크립트의 매개 변수</span><span class="sxs-lookup"><span data-stu-id="94878-178">Parameters in the main script</span></span>

<span data-ttu-id="94878-179">주 스크립트 *New-AzureWebSiteEnv*은 몇 가지 매개 변수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-179">The main script, *New-AzureWebSiteEnv.ps1*, defines several parameters:</span></span>

[!code-powershell[Main](automate-everything/samples/sample2.ps1)]

<span data-ttu-id="94878-180">두 매개 변수가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-180">Two parameters are required:</span></span>

- <span data-ttu-id="94878-181">스크립트에서 만드는 웹 앱의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="94878-181">The name of the web app that the script creates.</span></span> <span data-ttu-id="94878-182">URL: `<name>.azurewebsites.net`에도 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94878-182">(This is also used for the URL: `<name>.azurewebsites.net`.)</span></span>
- <span data-ttu-id="94878-183">스크립트에서 만드는 데이터베이스 서버의 새 관리자에 대 한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="94878-183">The password for the new administrative user of the database server that the script creates.</span></span>

<span data-ttu-id="94878-184">선택적 매개 변수를 사용 하 여 데이터 센터 위치 (기본값은 "미국 서 부"), 데이터베이스 서버 관리자 이름 (기본값은 "dbuser"), 데이터베이스 서버에 대 한 방화벽 규칙을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-184">Optional parameters enable you to specify the data center location (defaults to "West US"), database server administrator name (defaults to "dbuser"), and a firewall rule for the database server.</span></span>

### <a name="create-the-web-app"></a><span data-ttu-id="94878-185">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="94878-185">Create the web app</span></span>

<span data-ttu-id="94878-186">스크립트는 `New-AzureWebsite` cmdlet을 호출 하 여 웹 앱을 만들고 웹 앱 이름 및 위치 매개 변수 값으로 전달 하 여 웹 앱을 만드는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-186">The first thing the script does is create the web app by calling the `New-AzureWebsite` cmdlet, passing in to it the web app name and location parameter values:</span></span>

[!code-powershell[Main](automate-everything/samples/sample3.ps1?highlight=2)]

### <a name="create-the-storage-account"></a><span data-ttu-id="94878-187">스토리지 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="94878-187">Create the storage account</span></span>

<span data-ttu-id="94878-188">그런 다음 주 스크립트는 *New-AzureStorage* 스크립트를 실행 하 여 저장소 계정 이름에 대해 " *&lt;websitename&gt;* 저장소"를 지정 하 고 웹 앱과 동일한 데이터 센터 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-188">Then the main script runs the *New-AzureStorage.ps1* script, specifying "*&lt;websitename&gt;* storage" for the storage account name, and the same data center location as the web app.</span></span>

[!code-powershell[Main](automate-everything/samples/sample4.ps1?highlight=3)]

<span data-ttu-id="94878-189">*New-AzureStorage* 는 `New-AzureStorageAccount` cmdlet을 호출 하 여 저장소 계정을 만들고 계정 이름과 액세스 키 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-189">*New-AzureStorage.ps1* calls the `New-AzureStorageAccount` cmdlet to create the storage account, and it returns the account name and access key values.</span></span> <span data-ttu-id="94878-190">저장소 계정의 blob 및 큐에 액세스 하려면 응용 프로그램에 이러한 값이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-190">The application will need these values in order to access the blobs and queues in the storage account.</span></span>

[!code-powershell[Main](automate-everything/samples/sample5.ps1?highlight=2)]

<span data-ttu-id="94878-191">항상 새 저장소 계정을 만들 필요는 없습니다. 필요에 따라 기존 저장소 계정을 사용 하도록 지시 하는 매개 변수를 추가 하 여 스크립트를 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-191">You might not always want to create a new storage account; you could enhance the script by adding a parameter that optionally directs it to use an existing storage account.</span></span>

### <a name="create-the-databases"></a><span data-ttu-id="94878-192">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="94878-192">Create the databases</span></span>

<span data-ttu-id="94878-193">기본 스크립트는 기본 데이터베이스 및 방화벽 규칙 이름을 설정한 후 데이터베이스 생성 스크립트 *New-AzureSql.* p s 1을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-193">The main script then runs the database creation script, *New-AzureSql.ps1*, after setting up default database and firewall rule names:</span></span>

[!code-powershell[Main](automate-everything/samples/sample6.ps1)]

[!code-powershell[Main](automate-everything/samples/sample7.ps1?highlight=2)]

<span data-ttu-id="94878-194">데이터베이스 생성 스크립트는 개발 컴퓨터의 IP 주소를 검색 하 고, 개발 컴퓨터에서 서버에 연결 하 고 관리할 수 있도록 방화벽 규칙을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-194">The database creation script retrieves the dev machine's IP address and sets a firewall rule so the dev machine can connect to and manage the server.</span></span> <span data-ttu-id="94878-195">그런 다음 데이터베이스 생성 스크립트는 데이터베이스를 설정 하는 몇 가지 단계를 거칩니다.</span><span class="sxs-lookup"><span data-stu-id="94878-195">The database creation script then goes through several steps to set up the databases:</span></span>

- <span data-ttu-id="94878-196">`New-AzureSqlDatabaseServer` cmdlet을 사용 하 여 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94878-196">Creates the server by using the `New-AzureSqlDatabaseServer` cmdlet.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample8.ps1?highlight=1)]
- <span data-ttu-id="94878-197">개발 컴퓨터에서 서버를 관리 하 고 웹 앱이 서버에 연결할 수 있도록 하는 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94878-197">Creates firewall rules to enable the dev machine to manage the server and to enable the web app to connect to it.</span></span> 

    [!code-powershell[Main](automate-everything/samples/sample9.ps1?highlight=3,5)]
- <span data-ttu-id="94878-198">`New-AzureSqlDatabaseServerContext` cmdlet을 사용 하 여 서버 이름과 자격 증명을 포함 하는 데이터베이스 컨텍스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94878-198">Creates a database context that includes the server name and credentials, by using the `New-AzureSqlDatabaseServerContext` cmdlet.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample10.ps1?highlight=4)]

    <span data-ttu-id="94878-199">`New-PSCredentialFromPlainText`은 `ConvertTo-SecureString` cmdlet을 호출 하 여 암호를 암호화 하 고 `Get-Credential` cmdlet이 반환 하는 것과 동일한 형식의 `PSCredential` 개체를 반환 하는 스크립트의 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="94878-199">`New-PSCredentialFromPlainText` is a function in the script that calls the `ConvertTo-SecureString` cmdlet to encrypt the password and returns a `PSCredential` object, the same type that the `Get-Credential` cmdlet returns.</span></span>
- <span data-ttu-id="94878-200">`New-AzureSqlDatabase` cmdlet을 사용 하 여 응용 프로그램 데이터베이스 및 멤버 자격 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94878-200">Creates the application database and the membership database by using the `New-AzureSqlDatabase` cmdlet.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample11.ps1?highlight=2,5)]
- <span data-ttu-id="94878-201">는 로컬로 정의 된 함수를 호출 하 여 각 데이터베이스에 대 한 연결 문자열을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94878-201">Calls a locally defined function to create a connection string for each database.</span></span> <span data-ttu-id="94878-202">응용 프로그램에서는 이러한 연결 문자열을 사용 하 여 데이터베이스에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-202">The application will use these connection strings to access the databases.</span></span> 

    [!code-powershell[Main](automate-everything/samples/sample12.ps1?highlight=1-2)]

    <span data-ttu-id="94878-203">SQLAzureDatabaseConnectionString는 제공 된 매개 변수 값에서 연결 문자열을 만드는 스크립트에 정의 된 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="94878-203">Get-SQLAzureDatabaseConnectionString is a function defined in the script that creates the connection string from the parameter values supplied to it.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample13.ps1?highlight=1)]
- <span data-ttu-id="94878-204">데이터베이스 서버 이름 및 연결 문자열을 사용 하 여 해시 테이블을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-204">Returns a hash table with the database server name and the connection strings.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample14.ps1)]

<span data-ttu-id="94878-205">Fix It 앱은 별도의 멤버 자격과 응용 프로그램 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-205">The Fix It app uses separate membership and application databases.</span></span> <span data-ttu-id="94878-206">또한 멤버 자격 및 응용 프로그램 데이터를 모두 단일 데이터베이스에 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-206">It's also possible to put both membership and application data in a single database.</span></span>

### <a name="store-app-settings-and-connection-strings"></a><span data-ttu-id="94878-207">앱 설정 및 연결 문자열 저장</span><span class="sxs-lookup"><span data-stu-id="94878-207">Store app settings and connection strings</span></span>

<span data-ttu-id="94878-208">Azure에는 Web.config 파일에서 `appSettings` 또는 `connectionStrings` 컬렉션을 읽으려고 할 때 응용 프로그램에 반환 되는 내용을 자동으로 재정의 하는 설정 및 연결 문자열을 저장할 수 있는 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-208">Azure has a feature that enables you to store settings and connection strings that automatically override what is returned to the application when it tries to read the `appSettings` or `connectionStrings` collections in the Web.config file.</span></span> <span data-ttu-id="94878-209">배포할 때 [web.config 변환을](../../../../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md) 적용 하는 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-209">This is an alternative to applying [Web.config transformations](../../../../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md) when you deploy.</span></span> <span data-ttu-id="94878-210">자세한 내용은이 설명서의 뒷부분에 나오는 [Azure에 중요 한 데이터 저장](source-control.md#appsettings) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="94878-210">For more information, see [Store sensitive data in Azure](source-control.md#appsettings) later in this e-book.</span></span>

<span data-ttu-id="94878-211">환경 만들기 스크립트는 azure에서 실행 될 때 응용 프로그램이 저장소 계정 및 데이터베이스에 액세스 하는 데 필요한 모든 `appSettings` 및 `connectionStrings` 값을 Azure에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-211">The environment creation script stores in Azure all of the `appSettings` and `connectionStrings` values that the application needs to access the storage account and databases when it runs in Azure.</span></span>

[!code-powershell[Main](automate-everything/samples/sample15.ps1)]

[!code-powershell[Main](automate-everything/samples/sample16.ps1)]

[!code-powershell[Main](automate-everything/samples/sample17.ps1?highlight=2)]

<span data-ttu-id="94878-212">[새 유물](http://newrelic.com/) 은 [모니터링 및 원격 분석](monitoring-and-telemetry.md) 챕터에서 설명 하는 원격 분석 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="94878-212">[New Relic](http://newrelic.com/) is a telemetry framework that we demonstrate in the [Monitoring and Telemetry](monitoring-and-telemetry.md) chapter.</span></span> <span data-ttu-id="94878-213">또한 환경 생성 스크립트는 웹 앱을 다시 시작 하 여 새 유물 설정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-213">The environment creation script also restarts the web app to make sure that it picks up the New Relic settings.</span></span>

[!code-powershell[Main](automate-everything/samples/sample18.ps1?highlight=2)]

### <a name="preparing-for-deployment"></a><span data-ttu-id="94878-214">배포 준비</span><span class="sxs-lookup"><span data-stu-id="94878-214">Preparing for deployment</span></span>

<span data-ttu-id="94878-215">프로세스가 끝나면 환경 만들기 스크립트에서 두 함수를 호출 하 여 배포 스크립트에서 사용 되는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94878-215">At the end of the process, the environment creation script calls two functions to create files that will be used by the deployment script.</span></span>

<span data-ttu-id="94878-216">이러한 함수 중 하나는 게시 프로필 *(&lt;websitename&gt;* 파일)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94878-216">One of these functions creates a publish profile *(&lt;websitename&gt;.pubxml* file).</span></span> <span data-ttu-id="94878-217">이 코드는 Azure REST API를 호출 하 여 게시 설정을 가져오고 정보를 *publishsettings* 파일에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-217">The code calls the Azure REST API to get the publish settings, and it saves the information in a *.publishsettings* file.</span></span> <span data-ttu-id="94878-218">그런 다음 템플릿 파일 (*pubxml*)과 함께 해당 파일의 정보를 사용 하 여 게시 프로필을 포함 하는 *pubxml* 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94878-218">Then it uses the information from that file along with a template file (*pubxml.template*) to create the *.pubxml* file that contains the publish profile.</span></span> <span data-ttu-id="94878-219">이 2 단계 프로세스는 Visual Studio에서 수행 하는 작업을 시뮬레이션 *합니다. publishsettings* 파일을 다운로드 하 고 가져와서 게시 프로필을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94878-219">This two-step process simulates what you do in Visual Studio: download a *.publishsettings* file and import that to create a publish profile.</span></span>

<span data-ttu-id="94878-220">다른 함수는 다른 템플릿 파일 (website-environment)을 사용 하 여 배포 스크립트에서 *pubxml* 파일과 함께 사용할 설정을 포함 하는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94878-220">The other function uses another template file (website-environment.template) to create a *website-environment.xml* file that contains settings the deployment script will use along with the *.pubxml* file.</span></span>

### <a name="troubleshooting-and-error-handling"></a><span data-ttu-id="94878-221">문제 해결 및 오류 처리</span><span class="sxs-lookup"><span data-stu-id="94878-221">Troubleshooting and error handling</span></span>

<span data-ttu-id="94878-222">스크립트는 프로그램과 유사 합니다. 실패할 수 있으며, 오류 및 발생 원인에 대 한 정보를 파악 하고자 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-222">Scripts are like programs: they can fail, and when they do you want to know as much as you can about the failure and what caused it.</span></span> <span data-ttu-id="94878-223">이러한 이유로 환경 만들기 스크립트는 `VerbosePreference` 변수의 값을 `SilentlyContinue`에서 `Continue`으로 변경 하 여 모든 자세한 정보 메시지가 표시 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-223">For this reason, the environment creation script changes the value of the `VerbosePreference` variable from `SilentlyContinue` to `Continue` so that all verbose messages are displayed.</span></span> <span data-ttu-id="94878-224">또한 `ErrorActionPreference` 변수의 값을 `Continue`에서 `Stop`으로 변경 하 여 종료 되지 않는 오류가 발생 해도 스크립트가 중지 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-224">It also changes the value of the `ErrorActionPreference` variable from `Continue` to `Stop`, so that the script stops even when it encounters non-terminating errors:</span></span>

[!code-powershell[Main](automate-everything/samples/sample19.ps1)]

<span data-ttu-id="94878-225">작업을 수행 하기 전에 스크립트는 시작 시간을 저장 하 여 경과 된 시간을 계산할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-225">Before it does any work, the script stores the start time so that it can calculate the elapsed time when it's done:</span></span>

[!code-powershell[Main](automate-everything/samples/sample20.ps1)]

<span data-ttu-id="94878-226">작업이 완료 되 면 스크립트는 경과 된 시간을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-226">After it completes its work, the script displays the elapsed time:</span></span>

[!code-powershell[Main](automate-everything/samples/sample21.ps1)]

<span data-ttu-id="94878-227">그리고 모든 키 작업에 대해 스크립트는 다음과 같은 자세한 정보 메시지를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-227">And for every key operation the script writes verbose messages, for example:</span></span>

[!code-powershell[Main](automate-everything/samples/sample22.ps1)]

## <a name="deployment-script"></a><span data-ttu-id="94878-228">배포 스크립트</span><span class="sxs-lookup"><span data-stu-id="94878-228">Deployment script</span></span>

<span data-ttu-id="94878-229">*New-AzureWebsiteEnv* 스크립트는 환경을 만들기 위해 수행 하는 작업, *Publish-AzureWebsite* 스크립트는 응용 프로그램 배포를 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="94878-229">What the *New-AzureWebsiteEnv.ps1* script does for environment creation, the *Publish-AzureWebsite.ps1* script does for application deployment.</span></span>

<span data-ttu-id="94878-230">배포 스크립트는 환경 생성 스크립트에서 만든 *website-environment* 파일에서 웹 앱의 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="94878-230">The deployment script gets the name of the web app from the *website-environment.xml* file created by the environment creation script.</span></span>

[!code-powershell[Main](automate-everything/samples/sample23.ps1)]

<span data-ttu-id="94878-231">*Publishsettings* 파일에서 배포 사용자 암호를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="94878-231">It gets the deployment user password from the *.publishsettings* file:</span></span>

[!code-powershell[Main](automate-everything/samples/sample24.ps1)]

<span data-ttu-id="94878-232">프로젝트를 빌드하고 배포 하는 [MSBuild](http://msbuildbook.com/) 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-232">It executes the [MSBuild](http://msbuildbook.com/) command that builds and deploys the project:</span></span>

[!code-powershell[Main](automate-everything/samples/sample25.ps1)]

<span data-ttu-id="94878-233">명령줄에서 `Launch` 매개 변수를 지정한 경우 `Show-AzureWebsite` cmdlet을 호출 하 여 웹 사이트 URL에 대 한 기본 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="94878-233">And if you've specified the `Launch` parameter on the command line, it calls the `Show-AzureWebsite` cmdlet to open your default browser to the website URL.</span></span>

[!code-powershell[Main](automate-everything/samples/sample26.ps1?highlight=3)]

<span data-ttu-id="94878-234">다음과 같은 명령을 사용 하 여 배포 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-234">You can run the deployment script with a command like this one:</span></span>

`.\Publish-AzureWebsite.ps1 ..\MyFixIt\MyFixIt.csproj -Launch`

<span data-ttu-id="94878-235">완료 되 면 브라우저는 클라우드에서 실행 중인 사이트가 `<websitename>.azurewebsites.net` URL에 열립니다.</span><span class="sxs-lookup"><span data-stu-id="94878-235">And when it's done, the browser opens with the site running in the cloud at the `<websitename>.azurewebsites.net` URL.</span></span>

![Windows Azure에 배포 된 It 앱 수정](automate-everything/_static/image7.png)

## <a name="summary"></a><span data-ttu-id="94878-237">요약</span><span class="sxs-lookup"><span data-stu-id="94878-237">Summary</span></span>

<span data-ttu-id="94878-238">이러한 스크립트를 사용 하면 동일한 옵션을 사용 하 여 동일한 단계가 항상 동일한 순서로 실행 되도록 확신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-238">With these scripts you can be confident that the same steps will always be executed in the same order using the same options.</span></span> <span data-ttu-id="94878-239">이렇게 하면 팀의 각 개발자가 다른 팀 멤버의 환경 또는 프로덕션 환경에서 실제로 동일한 방식으로 작동 하지 않는 특정 컴퓨터에서 무언가를 누락 하거나 사용자 지정 항목을 배포할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-239">This helps ensure that each developer on the team doesn't miss something or mess something up or deploy something custom on his own machine that won't actually work the same way in another team member's environment or in production.</span></span>

<span data-ttu-id="94878-240">이와 비슷한 방식으로 Linux 또는 Mac에서 실행할 수 있는 REST API, Windows PowerShell 스크립트, .NET 언어 API 또는 Bash 유틸리티를 사용 하 여 관리 포털에서 수행할 수 있는 대부분의 Azure 관리 기능을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-240">In a similar way, you can automate most Azure management functions that you can do in the management portal, by using the REST API, Windows PowerShell scripts, a .NET language API, or a Bash utility that you can run on Linux or Mac.</span></span>

<span data-ttu-id="94878-241">[다음 장에서](source-control.md) 는 소스 코드를 살펴보고 소스 코드 리포지토리에 스크립트를 포함 하는 것이 중요 한 이유를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-241">In the [next chapter](source-control.md) we'll look at source code and explain why it's important to include your scripts in your source code repository.</span></span>

## <a name="resources"></a><span data-ttu-id="94878-242">리소스</span><span class="sxs-lookup"><span data-stu-id="94878-242">Resources</span></span>

- <span data-ttu-id="94878-243">[Azure 용 Windows PowerShell을 설치 하 고 구성](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-243">[Install and Configure Windows PowerShell for Azure](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1).</span></span> <span data-ttu-id="94878-244">Azure PowerShell cmdlet을 설치 하는 방법 및 Azure 계정을 관리 하기 위해 컴퓨터에 필요한 인증서를 설치 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-244">Explains how to install the Azure PowerShell cmdlets and how to install the certificate that you need on your computer in order to manage your Azure account.</span></span> <span data-ttu-id="94878-245">PowerShell 자체를 학습 하기 위한 리소스 링크도 있으므로이 작업을 시작 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="94878-245">This is a great place to get started because it also has links to resources for learning PowerShell itself.</span></span>
- <span data-ttu-id="94878-246">[Azure 스크립트 센터](https://docs.microsoft.com/azure/automation/automation-runbook-gallery).</span><span class="sxs-lookup"><span data-stu-id="94878-246">[Azure Script Center](https://docs.microsoft.com/azure/automation/automation-runbook-gallery).</span></span> <span data-ttu-id="94878-247">WindowsAzure.com 포털을 사용 하 여 Azure 서비스를 관리 하는 스크립트를 개발 하기 위한 링크, 시작 자습서에 대 한 링크, cmdlet 참조 설명서와 소스 코드 및 샘플 스크립트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-247">WindowsAzure.com portal to resources for developing scripts that manage Azure services, with links to getting started tutorials, cmdlet reference documentation and source code, and sample scripts</span></span>
- <span data-ttu-id="94878-248">[주말 스크립터: Azure 및 PowerShell 시작](https://blogs.technet.com/b/heyscriptingguy/archive/2013/06/22/weekend-scripter-getting-started-with-windows-azure-and-powershell.aspx)</span><span class="sxs-lookup"><span data-stu-id="94878-248">[Weekend Scripter: Getting Started with Azure and PowerShell](https://blogs.technet.com/b/heyscriptingguy/archive/2013/06/22/weekend-scripter-getting-started-with-windows-azure-and-powershell.aspx).</span></span> <span data-ttu-id="94878-249">Windows PowerShell 전용 블로그에서이 게시물은 Azure 관리 기능에 PowerShell을 사용 하는 것에 대 한 유용한 소개를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-249">In a blog dedicated to Windows PowerShell, this post provides a great introduction to using PowerShell for Azure management functions.</span></span>
- <span data-ttu-id="94878-250">[Azure 플랫폼 간 명령줄 인터페이스를 설치 하 고 구성](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-250">[Install and Configure the Azure Cross-Platform Command-Line Interface](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).</span></span> <span data-ttu-id="94878-251">Mac 및 Linux 및 Windows 시스템에서 작동 하는 Azure scripting framework에 대 한 시작 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="94878-251">Getting-started tutorial for an Azure scripting framework that works on Mac and Linux as well as Windows systems.</span></span>
- <span data-ttu-id="94878-252">[Azure sdk 및 도구 다운로드 항목의 명령줄 도구 섹션을 참조](https://azure.microsoft.com/downloads/)하세요.</span><span class="sxs-lookup"><span data-stu-id="94878-252">[Command-line tools section of the Download Azure SDKs and Tools topic](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="94878-253">Azure에 대 한 명령줄 도구와 관련 된 설명서 및 다운로드를 위한 포털 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="94878-253">Portal page for documentation and downloads related to command-line tools for Azure.</span></span>
- <span data-ttu-id="94878-254">[Azure 관리 라이브러리 및 .NET을 사용한 자동화](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx)(영문).</span><span class="sxs-lookup"><span data-stu-id="94878-254">[Automating everything with the Azure Management Libraries and .NET](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx).</span></span> <span data-ttu-id="94878-255">Scott Hanselman는 Azure 용 .NET 관리 API를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="94878-255">Scott Hanselman introduces the .NET management API for Azure.</span></span>
- <span data-ttu-id="94878-256">[Windows PowerShell 스크립트를 사용하여 개발 및 테스트 환경에 게시](https://msdn.microsoft.com/library/azure/dn642480.aspx).</span><span class="sxs-lookup"><span data-stu-id="94878-256">[Using Windows PowerShell Scripts to Publish to Dev and Test Environments](https://msdn.microsoft.com/library/azure/dn642480.aspx).</span></span> <span data-ttu-id="94878-257">Visual Studio에서 웹 프로젝트에 대해 자동으로 생성 하는 게시 스크립트를 사용 하는 방법을 설명 하는 MSDN 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="94878-257">MSDN documentation that explains how to use publish scripts that Visual Studio automatically generates for web projects.</span></span>
- <span data-ttu-id="94878-258">[PowerShell Tools for Visual Studio 2013](https://visualstudiogallery.msdn.microsoft.com/c9eb3ba8-0c59-4944-9a62-6eee37294597).</span><span class="sxs-lookup"><span data-stu-id="94878-258">[PowerShell Tools for Visual Studio 2013](https://visualstudiogallery.msdn.microsoft.com/c9eb3ba8-0c59-4944-9a62-6eee37294597).</span></span> <span data-ttu-id="94878-259">Visual studio에서 Windows PowerShell에 대 한 언어 지원을 추가 하는 visual Studio 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="94878-259">Visual Studio extension that adds language support for Windows PowerShell in Visual Studio.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="94878-260">[이전](introduction.md)
> [다음](source-control.md)</span><span class="sxs-lookup"><span data-stu-id="94878-260">[Previous](introduction.md)
[Next](source-control.md)</span></span>
