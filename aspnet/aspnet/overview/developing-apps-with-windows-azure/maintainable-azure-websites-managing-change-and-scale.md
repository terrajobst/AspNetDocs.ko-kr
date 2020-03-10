---
uid: aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
title: '실습: 유지 관리 가능한 Azure Websites: 변경 및 확장 관리 | Microsoft Docs'
author: rick-anderson
description: 이 랩에서 Microsoft Azure를 사용 하 여 웹 사이트를 쉽게 빌드하고 프로덕션에 배포 하는 방법을 알아봅니다.
ms.author: riande
ms.date: 07/16/2014
ms.assetid: ecfd0eb4-c4ad-44e6-9db9-a2a66611ff6a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
msc.type: authoredcontent
ms.openlocfilehash: c88bae40a8aa092037c0b359ee391acaf161cf10
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506375"
---
# <a name="hands-on-lab-maintainable-azure-websites-managing-change-and-scale"></a><span data-ttu-id="5ddd8-103">실습: 유지 관리 가능한 Azure Websites: 변경 및 확장 관리</span><span class="sxs-lookup"><span data-stu-id="5ddd8-103">Hands on Lab: Maintainable Azure Websites: Managing Change and Scale</span></span>

<span data-ttu-id="5ddd8-104">[웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="5ddd8-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="5ddd8-105">웹 캠프 교육 키트 다운로드</span><span class="sxs-lookup"><span data-stu-id="5ddd8-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

> <span data-ttu-id="5ddd8-106">Microsoft Azure를 사용 하면 웹 사이트를 쉽게 빌드하고 프로덕션에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-106">Microsoft Azure makes it easy to build and deploy websites to production.</span></span> <span data-ttu-id="5ddd8-107">그러나 응용 프로그램이 라이브 상태인 경우에는 작업을 시작할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-107">But you're not done when your application is live, you're just getting started!</span></span> <span data-ttu-id="5ddd8-108">변경 요구 사항, 데이터베이스 업데이트, 크기 조정 등을 처리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-108">You'll need to handle changing requirements, database updates, scale, and more.</span></span> <span data-ttu-id="5ddd8-109">다행히 사이트를 원활 하 게 실행 하는 데 도움이 되는 다양 한 기능을 제공 하는 Azure App Service 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-109">Fortunately, Azure App Service has you covered, with plenty of features to help you keep your sites running smoothly.</span></span>
>
> <span data-ttu-id="5ddd8-110">Azure는 모든 규모의 웹 응용 프로그램에 대해 안전 하 고 유연한 개발, 배포 및 확장 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-110">Azure offers secure and flexible development, deployment and scaling options for any size web application.</span></span> <span data-ttu-id="5ddd8-111">인프라를 관리할 필요없이 기존의 도구를 활용하여 응용 프로그램을 만들고 배포하세요.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-111">Leverage your existing tools to create and deploy applications without the hassle of managing infrastructure.</span></span>
>
> <span data-ttu-id="5ddd8-112">선호 하는 개발 도구를 사용 하 여 만든 콘텐츠를 쉽게 배포 하 여 몇 분 내에 프로덕션 웹 응용 프로그램을 프로 비전 하세요.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-112">Provision a production web application yourself in minutes by easily deploying content created using your favorite development tool.</span></span> <span data-ttu-id="5ddd8-113">**Git**, **GitHub**, **Bitbucket**, **TFS**및 **DropBox**에 대 한 지원을 사용 하 여 소스 제어에서 직접 기존 사이트를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-113">You can deploy an existing site directly from source control with support for **Git**, **GitHub**, **Bitbucket**, **TFS**, and even **DropBox**.</span></span> <span data-ttu-id="5ddd8-114">Windows에서 **PowerShell** 을 사용 하거나 모든 OS에서 실행 되는 **CLI** 도구에서 즐겨 사용 하는 IDE 또는 스크립트에서 직접 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-114">Deploy directly from your favorite IDE or from scripts using **PowerShell** in Windows or **CLI** tools running on any OS.</span></span> <span data-ttu-id="5ddd8-115">배포 된 후에는 지속적인 배포 지원을 통해 사이트를 지속적으로 최신 상태로 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-115">Once deployed, keep your sites constantly up-to-date with support for continuous deployment.</span></span>
>
> <span data-ttu-id="5ddd8-116">Azure는 빅 이거나 작은 모든 데이터에 대 한 확장 가능 하 고 지속적인 클라우드 저장소, 백업 및 복구 솔루션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-116">Azure provides scalable, durable cloud storage, backup, and recovery solutions for any data, big or small.</span></span> <span data-ttu-id="5ddd8-117">프로덕션 환경에 응용 프로그램을 배포 하는 경우 테이블, Blob 및 SQL 데이터베이스와 같은 저장소 서비스는 클라우드에서 응용 프로그램을 확장 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-117">When deploying applications to a production environment, storage services such as Tables, Blobs and SQL Databases, help you scale your application in the cloud.</span></span>
>
> <span data-ttu-id="5ddd8-118">SQL database를 사용 하면 응용 프로그램의 새 버전을 배포할 때 생산적인 데이터베이스를 최신 상태로 유지 하는 것이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-118">With SQL Databases, it is important to keep your productive database up-to-date when deploying new versions of your application.</span></span> <span data-ttu-id="5ddd8-119">**Entity Framework Code First 마이그레이션**덕분에 몇 분 내에 환경을 업데이트 하기 위해 데이터 모델의 개발 및 배포가 간소화 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-119">Thanks to **Entity Framework Code First Migrations**, the development and deployment of your data model has been simplified to update your environments in minutes.</span></span> <span data-ttu-id="5ddd8-120">이 실습 랩에서는 Microsoft Azure의 프로덕션 환경에 웹 앱을 배포할 때 발생할 수 있는 다양 한 항목을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-120">This hands-on lab will show you the different topics you could encounter when deploying your web app to production environments in Microsoft Azure.</span></span>
>
> <span data-ttu-id="5ddd8-121">모든 샘플 코드와 코드 조각은 [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)에서 사용할 수 있는 웹 캠프 교육 키트에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-121">All sample code and snippets are included in the Web Camps Training Kit, available at [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).</span></span>
>
> <span data-ttu-id="5ddd8-122">이 항목에 대 한 자세한 적용 범위는 [Azure를 사용 하 여 실제 클라우드 앱 빌드](building-real-world-cloud-apps-with-windows-azure/introduction.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-122">For more in-depth coverage of this topic, see the [Building Real-World Cloud Apps with Azure e-book](building-real-world-cloud-apps-with-windows-azure/introduction.md).</span></span>

<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="5ddd8-123">개요</span><span class="sxs-lookup"><span data-stu-id="5ddd8-123">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="5ddd8-124">목표</span><span class="sxs-lookup"><span data-stu-id="5ddd8-124">Objectives</span></span>

<span data-ttu-id="5ddd8-125">이 실습 랩에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-125">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="5ddd8-126">기존 모델을 사용 하 여 Entity Framework 마이그레이션 사용</span><span class="sxs-lookup"><span data-stu-id="5ddd8-126">Enable Entity Framework Migrations with an existing model</span></span>
- <span data-ttu-id="5ddd8-127">Entity Framework 마이그레이션을 사용 하 여 개체 모델 및 데이터베이스를 적절 하 게 업데이트</span><span class="sxs-lookup"><span data-stu-id="5ddd8-127">Update the object model and database accordingly using Entity Framework Migrations</span></span>
- <span data-ttu-id="5ddd8-128">Git를 사용 하 여 Azure App Service에 배포</span><span class="sxs-lookup"><span data-stu-id="5ddd8-128">Deploy to Azure App Service using Git</span></span>
- <span data-ttu-id="5ddd8-129">Azure 관리 포털을 사용 하 여 이전 배포로 롤백</span><span class="sxs-lookup"><span data-stu-id="5ddd8-129">Rollback to a previous deployment using the Azure Management portal</span></span>
- <span data-ttu-id="5ddd8-130">Azure Storage를 사용 하 여 웹 앱 크기 조정</span><span class="sxs-lookup"><span data-stu-id="5ddd8-130">Use Azure Storage to scale a web app</span></span>
- <span data-ttu-id="5ddd8-131">Azure 관리 포털을 사용 하 여 웹 앱에 대 한 자동 크기 조정 구성</span><span class="sxs-lookup"><span data-stu-id="5ddd8-131">Configure auto-scaling for a web app using the Azure Management Portal</span></span>
- <span data-ttu-id="5ddd8-132">Visual Studio에서 부하 테스트 프로젝트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="5ddd8-132">Create and configure a load test project in Visual Studio</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="5ddd8-133">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="5ddd8-133">Prerequisites</span></span>

<span data-ttu-id="5ddd8-134">이 실습 실습을 완료 하려면 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-134">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="5ddd8-135">[웹 이상의 Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)</span><span class="sxs-lookup"><span data-stu-id="5ddd8-135">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>
- [<span data-ttu-id="5ddd8-136">.NET 용 Azure SDK 2.2</span><span class="sxs-lookup"><span data-stu-id="5ddd8-136">Azure SDK for .NET 2.2</span></span>](https://www.microsoft.com/windowsazure/sdk/)
- [<span data-ttu-id="5ddd8-137">GIT 버전 제어 시스템</span><span class="sxs-lookup"><span data-stu-id="5ddd8-137">GIT Version Control System</span></span>](http://git-scm.com/download)
- <span data-ttu-id="5ddd8-138">Microsoft Azure 구독</span><span class="sxs-lookup"><span data-stu-id="5ddd8-138">A Microsoft Azure subscription</span></span>

    - <span data-ttu-id="5ddd8-139">[무료 평가판](https://aka.ms/watk-freetrial) 등록</span><span class="sxs-lookup"><span data-stu-id="5ddd8-139">Sign up for a [Free Trial](https://aka.ms/watk-freetrial)</span></span>
    - <span data-ttu-id="5ddd8-140">MSDN 또는 MSDN 플랫폼 구독자가 포함 된 Visual Studio Professional, Test Professional, Premium 또는 Ultimate 인 경우 지금 [msdn 혜택](https://aka.ms/watk-msdn) 을 활성화 하 여 Azure에서 개발 및 테스트를 시작 하세요.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-140">If you are a Visual Studio Professional, Test Professional, Premium or Ultimate with MSDN or MSDN Platforms subscriber, activate your [MSDN benefit](https://aka.ms/watk-msdn) now to start developing and testing on Azure</span></span>
    - <span data-ttu-id="5ddd8-141">[BizSpark](https://aka.ms/watk-bizspark) 멤버는 Visual Studio Ultimate with MSDN 구독을 통해 Azure 혜택을 자동으로 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-141">[BizSpark](https://aka.ms/watk-bizspark) members automatically receive the Azure benefit through their Visual Studio Ultimate with MSDN subscriptions</span></span>
    - <span data-ttu-id="5ddd8-142">[Microsoft 파트너 네트워크](https://aka.ms/watk-mpn) Cloud Essentials 프로그램의 구성원은 무료로 월간 Azure 크레딧을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-142">Members of the [Microsoft Partner Network](https://aka.ms/watk-mpn) Cloud Essentials program receive monthly Azure credits at no charge</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="5ddd8-143">설치 프로그램</span><span class="sxs-lookup"><span data-stu-id="5ddd8-143">Setup</span></span>

<span data-ttu-id="5ddd8-144">이 실습 랩에서 연습을 실행 하려면 먼저 환경을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-144">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="5ddd8-145">Windows 탐색기를 열고 랩의 **원본** 폴더로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-145">Open Windows Explorer and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="5ddd8-146">**Setup.exe** 를 마우스 오른쪽 단추로 클릭 하 고 **관리자 권한으로 실행** 을 선택 하 여 환경을 구성 하는 설치 프로세스를 시작 하 고이 랩에 대 한 Visual Studio 코드 조각을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-146">Right-click on **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="5ddd8-147">사용자 계정 컨트롤 대화 상자가 표시 되 면 계속 하려면 작업을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-147">If the User Account Control dialog is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="5ddd8-148">설치 프로그램을 실행 하기 전에이 랩에 대 한 모든 종속성을 확인 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-148">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="5ddd8-149">코드 조각 사용</span><span class="sxs-lookup"><span data-stu-id="5ddd8-149">Using the Code Snippets</span></span>

<span data-ttu-id="5ddd8-150">랩 문서 전체에서 코드 블록을 삽입 하 라는 지침이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-150">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="5ddd8-151">사용자 편의를 위해이 코드의 대부분은 Visual Studio 2013 내에서 액세스할 수 있는 Visual Studio Code 코드 조각으로 제공 되며,이를 수동으로 추가 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-151">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="5ddd8-152">각 연습에는 각 연습을 서로 독립적으로 수행할 수 있는 연습 **시작** 폴더에 있는 시작 솔루션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-152">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="5ddd8-153">연습 중에 추가 된 코드 조각은 이러한 시작 솔루션에서 누락 되었으며, 연습을 완료할 때까지 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-153">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="5ddd8-154">연습에 대 한 소스 코드 내에서 해당 연습의 단계를 완료 하 여 생성 된 코드를 포함 하는 Visual Studio 솔루션을 포함 하는 **끝** 폴더를 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-154">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="5ddd8-155">이 실습 랩을 통해 작업할 때 추가 도움이 필요한 경우 이러한 솔루션을 지침으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-155">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="5ddd8-156">실습</span><span class="sxs-lookup"><span data-stu-id="5ddd8-156">Exercises</span></span>

<span data-ttu-id="5ddd8-157">이 실습 랩에는 다음 연습이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-157">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="5ddd8-158">Entity Framework 마이그레이션 사용</span><span class="sxs-lookup"><span data-stu-id="5ddd8-158">Using Entity Framework Migrations</span></span>](#Exercise1)
2. [<span data-ttu-id="5ddd8-159">스테이징에 웹 앱 배포</span><span class="sxs-lookup"><span data-stu-id="5ddd8-159">Deploying a Web App to Staging</span></span>](#Exercise2)
3. [<span data-ttu-id="5ddd8-160">프로덕션 환경에서 배포 롤백 수행</span><span class="sxs-lookup"><span data-stu-id="5ddd8-160">Performing Deployment Rollback in Production</span></span>](#Exercise3)
4. [<span data-ttu-id="5ddd8-161">Azure Storage를 사용 하 여 크기 조정</span><span class="sxs-lookup"><span data-stu-id="5ddd8-161">Scaling Using Azure Storage</span></span>](#Exercise4)
5. <span data-ttu-id="5ddd8-162">[Web Apps에 자동 크기 조정 사용](#Exercise5) (Visual Studio 2013 Ultimate edition의 경우 선택 사항)</span><span class="sxs-lookup"><span data-stu-id="5ddd8-162">[Using Autoscale for Web Apps](#Exercise5) (Optional for Visual Studio 2013 Ultimate edition)</span></span>

<span data-ttu-id="5ddd8-163">이 랩을 완료 하는 데 소요 되는 예상 시간: **75 분**</span><span class="sxs-lookup"><span data-stu-id="5ddd8-163">Estimated time to complete this lab: **75 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="5ddd8-164">Visual Studio를 처음 시작 하는 경우 미리 정의 된 설정 컬렉션 중 하나를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-164">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="5ddd8-165">미리 정의 된 각 컬렉션은 특정 개발 스타일에 맞게 디자인 되 고 창 레이아웃, 편집기 동작, IntelliSense 코드 조각 및 대화 상자 옵션을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-165">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="5ddd8-166">이 실습의 절차에서는 **일반 개발 설정** 컬렉션을 사용 하는 경우 Visual Studio에서 지정 된 작업을 수행 하는 데 필요한 작업을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-166">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="5ddd8-167">개발 환경에 대해 다른 설정 컬렉션을 선택 하는 경우 고려해 야 하는 단계에 차이가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-167">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>

<a id="Exercise1"></a>
### <a name="exercise-1-using-entity-framework-migrations"></a><span data-ttu-id="5ddd8-168">연습 1: Entity Framework 마이그레이션 사용</span><span class="sxs-lookup"><span data-stu-id="5ddd8-168">Exercise 1: Using Entity Framework Migrations</span></span>

<span data-ttu-id="5ddd8-169">응용 프로그램을 개발 하는 경우 데이터 모델이 시간이 지남에 따라 변경 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-169">When you are developing an application, your data model might change over time.</span></span> <span data-ttu-id="5ddd8-170">이러한 변경 내용은 데이터베이스의 기존 모델에 영향을 줄 수 있으며 (새 버전을 만드는 경우) 오류를 방지 하기 위해 데이터베이스를 최신 상태로 유지 하는 것이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-170">These changes could affect the existing model in your database (if you are creating a new version) and it is important to keep your database up-to-date to prevent errors.</span></span>

<span data-ttu-id="5ddd8-171">모델에서 이러한 변경 내용에 대 한 추적을 간소화 하기 위해 모델을 데이터베이스 스키마와 비교 하 여 자동으로 변경 내용을 감지 하 고 데이터베이스 업데이트를 위한 특정 코드를 생성 하 여 데이터베이스의 새 *버전* 을 만들 **Entity Framework Code First 마이그레이션** .</span><span class="sxs-lookup"><span data-stu-id="5ddd8-171">To simplify the tracking of these changes in your model, **Entity Framework Code First Migrations** automatically detect changes comparing your model with the database schema and generates specific code to update your database, creating new *versions* of your database.</span></span>

<span data-ttu-id="5ddd8-172">이 연습에서는 응용 프로그램에 대해 **마이그레이션을** 사용 하도록 설정 하는 방법과 데이터베이스 업데이트를 위한 변경 내용을 쉽게 검색 하 고 생성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-172">This exercise shows you how to enable **Migrations** for your application and how you can easily detect and generate changes to update your databases.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--enabling-migrations"></a><span data-ttu-id="5ddd8-173">작업 1-마이그레이션 사용</span><span class="sxs-lookup"><span data-stu-id="5ddd8-173">Task 1 – Enabling Migrations</span></span>

<span data-ttu-id="5ddd8-174">이 태스크에서는 **Geek of 퀴즈** 데이터베이스에 **Entity Framework Code First 마이그레이션** 를 사용 하도록 설정 하 고 모델을 변경 하 고 데이터베이스에 변경 내용을 반영 하는 방법을 이해 하는 단계를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-174">In this task, you will go through the steps of enabling **Entity Framework Code First Migrations** to the **Geek Quiz** database, changing the model and understanding how those changes are reflected in the database.</span></span>

1. <span data-ttu-id="5ddd8-175">Visual Studio를 열고 **Source\Ex1-UsingEntityFrameworkMigrations\Begin**에서 **GeekQuiz** 솔루션 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-175">Open Visual Studio and open the **GeekQuiz.sln** solution file from **Source\Ex1-UsingEntityFrameworkMigrations\Begin**.</span></span>
2. <span data-ttu-id="5ddd8-176">**NuGet** 패키지 종속성을 다운로드 하 고 설치 하기 위해 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-176">Build the solution in order to download and install the **NuGet** package dependencies.</span></span> <span data-ttu-id="5ddd8-177">이렇게 하려면 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **솔루션 빌드** 를 클릭 하거나 **ctrl + Shift + B**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-177">To do this, right-click the solution and click **Build Solution** or press **Ctrl + Shift + B**.</span></span>
3. <span data-ttu-id="5ddd8-178">Visual Studio의 **도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-178">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
4. <span data-ttu-id="5ddd8-179">**패키지 관리자 콘솔**에서 다음 명령을 입력 한 다음 **enter**키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-179">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span> <span data-ttu-id="5ddd8-180">기존 모델을 기반으로 하는 초기 마이그레이션이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-180">An initial migration based on the existing model will be created.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample1.ps1)]

    <span data-ttu-id="5ddd8-181">![마이그레이션 사용](maintainable-azure-websites-managing-change-and-scale/_static/image1.png "마이그레이션을 사용하도록 설정")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-181">![Enabling Migrations](maintainable-azure-websites-managing-change-and-scale/_static/image1.png "Enabling Migrations")</span></span>

    <span data-ttu-id="5ddd8-182">*마이그레이션 사용*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-182">*Enabling Migrations*</span></span>

    > [!NOTE]
    > <span data-ttu-id="5ddd8-183">이 명령은 **Configuration.cs**이라는 파일이 포함 된 geek of 퀴즈 프로젝트에 **마이그레이션** 폴더를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-183">This command adds a **Migrations** folder to Geek Quiz project that contains a file called **Configuration.cs**.</span></span> <span data-ttu-id="5ddd8-184">**구성** 클래스를 사용 하 여 사용자 컨텍스트에 대 한 마이그레이션 동작을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-184">The **Configuration** class allows you to configure how Migrations behaves for your context.</span></span>
5. <span data-ttu-id="5ddd8-185">마이그레이션을 사용 하는 경우 **Geek of 퀴즈** 에 필요한 초기 데이터로 데이터베이스를 채우도록 **구성** 클래스를 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-185">With Migrations enabled, you need to update the **Configuration** class to populate the database with the initial data that **Geek Quiz** requires.</span></span> <span data-ttu-id="5ddd8-186">**마이그레이션**아래에서이 랩의 **source\assets** 폴더에 있는 **Configuration.cs** 파일을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-186">Under **Migrations**, replace the **Configuration.cs** file with the one located in the **Source\Assets** folder of this lab.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5ddd8-187">**마이그레이션은** 모든 데이터베이스 업데이트에서 **초기값** 메서드를 호출 하므로 데이터베이스에서 레코드가 중복 되지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-187">Since **Migrations** will call the **Seed** method with every database update, you need to be sure that records are not duplicated in the database.</span></span> <span data-ttu-id="5ddd8-188">**Addorupdate** 메서드는 중복 데이터를 방지 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-188">The **AddOrUpdate** method will help to prevent duplicate data.</span></span>
6. <span data-ttu-id="5ddd8-189">초기 마이그레이션을 추가 하려면 다음 명령을 입력 한 다음 **enter**키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-189">To add an initial migration, enter the following command and then press **Enter**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5ddd8-190">LocalDB 인스턴스에 &quot;GeekQuizProd&quot; 라는 데이터베이스가 없는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-190">Make sure that there is no database named &quot;GeekQuizProd&quot; in your LocalDB instance.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample2.ps1)]

    <span data-ttu-id="5ddd8-191">![기본 스키마 마이그레이션 추가](maintainable-azure-websites-managing-change-and-scale/_static/image2.png "기본 스키마 마이그레이션 추가")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-191">![Adding base schema migration](maintainable-azure-websites-managing-change-and-scale/_static/image2.png "Adding base schema migration")</span></span>

    <span data-ttu-id="5ddd8-192">*기본 스키마 마이그레이션 추가*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-192">*Adding base schema migration*</span></span>

    > [!NOTE]
    > <span data-ttu-id="5ddd8-193">**추가-마이그레이션은** 마지막 마이그레이션을 만든 이후 모델에 대 한 변경 내용에 따라 다음 마이그레이션을 스 캐 폴드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-193">**Add-Migration** will scaffold the next migration based on changes you have made to your model since the last migration was created.</span></span> <span data-ttu-id="5ddd8-194">이 경우 프로젝트의 첫 번째 마이그레이션 이므로 **TriviaContext** 클래스에 정의 된 모든 테이블을 만들기 위한 스크립트가 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-194">In this case, as it is the first migration of the project, it will add the scripts to create all the tables defined in the **TriviaContext** class.</span></span>
7. <span data-ttu-id="5ddd8-195">다음 명령을 실행 하 여 마이그레이션을 실행 하 여 데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-195">Execute the migration to update the database by running the following command.</span></span> <span data-ttu-id="5ddd8-196">이 명령의 경우 **자세한 정보** 플래그를 지정 하 여 대상 데이터베이스에 적용 되는 SQL 문을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-196">For this command you will specify the **Verbose** flag to view the SQL statements being applied to the target database.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample3.ps1)]

    <span data-ttu-id="5ddd8-197">![초기 데이터베이스를 만드는 중](maintainable-azure-websites-managing-change-and-scale/_static/image3.png "초기 데이터베이스를 만드는 중")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-197">![Creating initial database](maintainable-azure-websites-managing-change-and-scale/_static/image3.png "Creating initial database")</span></span>

    <span data-ttu-id="5ddd8-198">*초기 데이터베이스를 만드는 중*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-198">*Creating initial database*</span></span>

    > [!NOTE]
    > <span data-ttu-id="5ddd8-199">**업데이트-** 데이터베이스에 보류 중인 모든 마이그레이션을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-199">**Update-Database** will apply any pending migrations to the database.</span></span> <span data-ttu-id="5ddd8-200">이 경우에는 web.config 파일에 정의 된 연결 문자열을 사용 하 여 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-200">In this case, it will create the database using the connection string defined in your web.config file.</span></span>
8. <span data-ttu-id="5ddd8-201">**보기** 메뉴로 이동 하 여 **SQL Server 개체 탐색기**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-201">Go to **View** menu and open **SQL Server Object Explorer**.</span></span>

    <span data-ttu-id="5ddd8-202">![SQL Server 개체 탐색기에서 열기](maintainable-azure-websites-managing-change-and-scale/_static/image4.png "SQL Server 개체 탐색기에서 열기")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-202">![Open in SQL Server Object Explorer](maintainable-azure-websites-managing-change-and-scale/_static/image4.png "Open in SQL Server Object Explorer")</span></span>

    <span data-ttu-id="5ddd8-203">*SQL Server 개체 탐색기에서 열기*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-203">*Open in SQL Server Object Explorer*</span></span>
9. <span data-ttu-id="5ddd8-204">**SQL Server 개체 탐색기** 창에서 **SQL Server** 노드를 마우스 오른쪽 단추로 클릭 하 고 **SQL Server 추가** ... 옵션을 선택 하 여 LocalDB 인스턴스에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-204">In the **SQL Server Object Explorer** window, connect to your LocalDB instance by right-clicking the **SQL Server** node and selecting **Add SQL Server...** option.</span></span>

    <span data-ttu-id="5ddd8-205">![SQL Server 인스턴스 추가](maintainable-azure-websites-managing-change-and-scale/_static/image5.png "SQL Server 인스턴스 추가")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-205">![Adding a SQL Server Instance](maintainable-azure-websites-managing-change-and-scale/_static/image5.png "Adding a SQL Server Instance")</span></span>

    <span data-ttu-id="5ddd8-206">*SQL Server 개체 탐색기에 SQL Server 인스턴스 추가*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-206">*Adding a SQL Server instance to SQL Server Object Explorer*</span></span>
10. <span data-ttu-id="5ddd8-207">**서버 이름** 을 *(localdb) \v11.0* 으로 설정 하 고 **Windows 인증** 을 인증 모드로 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-207">Set the **server name** to *(localdb)\v11.0* and leave **Windows Authentication** as your authentication mode.</span></span> <span data-ttu-id="5ddd8-208">**연결**을 클릭하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-208">Click **Connect** to continue.</span></span>

    <span data-ttu-id="5ddd8-209">![LocalDB에 연결](maintainable-azure-websites-managing-change-and-scale/_static/image6.png "LocalDB에 연결")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-209">![Connecting to LocalDB](maintainable-azure-websites-managing-change-and-scale/_static/image6.png "Connecting to LocalDB")</span></span>

    <span data-ttu-id="5ddd8-210">*LocalDB에 연결*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-210">*Connecting to LocalDB*</span></span>
11. <span data-ttu-id="5ddd8-211">**GeekQuizProd** 데이터베이스를 열고 **Tables** 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-211">Open the **GeekQuizProd** database and expand the **Tables** node.</span></span> <span data-ttu-id="5ddd8-212">여기에서 볼 수 있듯이 **TriviaContext** 클래스에 정의 된 모든 테이블을 생성 하는 **업데이트 데이터베이스** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-212">As you can see, the **Update-Database** command generated all the tables defined in the **TriviaContext** class.</span></span> <span data-ttu-id="5ddd8-213">Dbo를 찾습니다 **. TriviaQuestions** 테이블을 열고 columns 노드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-213">Locate the **dbo.TriviaQuestions** table and open the columns node.</span></span> <span data-ttu-id="5ddd8-214">다음 태스크에서는이 테이블에 새 열을 추가 하 고 **마이그레이션을**사용 하 여 데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-214">In the next task, you will add a new column to this table and update the database using **Migrations**.</span></span>

    <span data-ttu-id="5ddd8-215">![기타 정보 질문 열](maintainable-azure-websites-managing-change-and-scale/_static/image7.png "기타 정보 질문 열")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-215">![Trivia Questions Columns](maintainable-azure-websites-managing-change-and-scale/_static/image7.png "Trivia Questions Columns")</span></span>

    <span data-ttu-id="5ddd8-216">*기타 정보 질문 열*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-216">*Trivia Questions Columns*</span></span>

<a id="Ex1Task2"></a>
#### <a name="task-2--updating-database-schema-using-migrations"></a><span data-ttu-id="5ddd8-217">작업 2 – 마이그레이션을 사용 하 여 데이터베이스 스키마 업데이트</span><span class="sxs-lookup"><span data-stu-id="5ddd8-217">Task 2 – Updating Database Schema Using Migrations</span></span>

<span data-ttu-id="5ddd8-218">이 태스크에서는 **Entity Framework Code First 마이그레이션** 를 사용 하 여 모델의 변경 내용을 감지 하 고 데이터베이스를 업데이트 하는 데 필요한 코드를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-218">In this task, you will use **Entity Framework Code First Migrations** to detect a change in your model and generate the necessary code to update the database.</span></span> <span data-ttu-id="5ddd8-219">새 속성을 추가 하 여 **Triviaquestions** 엔터티를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-219">You will update the **TriviaQuestions** entity by adding a new property to it.</span></span> <span data-ttu-id="5ddd8-220">그런 다음 명령을 실행 하 여 테이블에 새 열을 포함 하는 새 마이그레이션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-220">Then you will run commands to create a new Migration to include the new column in the table.</span></span>

1. <span data-ttu-id="5ddd8-221">**솔루션 탐색기**에서 **모델** 폴더 내에 있는 **TriviaQuestion.cs** 파일을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-221">In **Solution Explorer**, double-click the **TriviaQuestion.cs** file located inside the **Models** folder.</span></span>
2. <span data-ttu-id="5ddd8-222">다음 코드 조각과 같이 **힌트**라는 새 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-222">Add a new property named **Hint**, as shown in the following code snippet.</span></span>

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample4.cs)]
3. <span data-ttu-id="5ddd8-223">**패키지 관리자 콘솔**에서 다음 명령을 입력 한 다음 **enter**키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-223">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span> <span data-ttu-id="5ddd8-224">모델의 변경 내용을 반영 하는 새 마이그레이션이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-224">A new migration will be created reflecting the change in our model.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample5.ps1)]

    <span data-ttu-id="5ddd8-225">![추가-마이그레이션](maintainable-azure-websites-managing-change-and-scale/_static/image8.png "추가-마이그레이션")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-225">![Add-Migration](maintainable-azure-websites-managing-change-and-scale/_static/image8.png "Add-Migration")</span></span>

    <span data-ttu-id="5ddd8-226">*추가-마이그레이션*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-226">*Add-Migration*</span></span>

    > [!NOTE]
    > <span data-ttu-id="5ddd8-227">마이그레이션 파일은 **위쪽** 및 **아래쪽**의 두 가지 방법으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-227">A Migration file is composed of two methods, **Up** and **Down**.</span></span>
    >
    > - <span data-ttu-id="5ddd8-228">**Up** 메서드는 현재 버전의 응용 프로그램을 데이터베이스에 적용 해야 하는 변경 내용을 지정 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-228">The **Up** method will be used to specify what changes the current version of our application need to apply to the database.</span></span>
    > - <span data-ttu-id="5ddd8-229">**Down** 은 **Up** 메서드에 추가한 변경 내용을 되돌리는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-229">The **Down** is used to reverse the changes we have added to the **Up** method.</span></span>
    >
    > <span data-ttu-id="5ddd8-230">데이터베이스 마이그레이션은 데이터베이스를 업데이트할 때 모든 마이그레이션을 타임 스탬프 순서 대로 실행 하 고 마지막 업데이트 이후 사용 되지 않은 경우에만 실행 됩니다. (\_MigrationHistory 테이블은 적용 된 마이그레이션을 추적 합니다.)</span><span class="sxs-lookup"><span data-stu-id="5ddd8-230">When the Database Migration updates the database, it will run all migrations in the timestamp order, and only those that have not been used since the last update (The \_MigrationHistory table keeps track of which migrations have been applied).</span></span> <span data-ttu-id="5ddd8-231">모든 마이그레이션의 **Up** 메서드가 호출 되 고 데이터베이스에 지정한 변경 내용을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-231">The **Up** method of all migrations will be called and will make the changes we have specified to the database.</span></span> <span data-ttu-id="5ddd8-232">이전 마이그레이션 단계로 돌아가려면 **Down** 메서드를 호출 하 여 변경 내용을 역순으로 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-232">If we decide to go back to a previous migration, the **Down** method will be called to redo the changes in a reverse order.</span></span>
4. <span data-ttu-id="5ddd8-233">**패키지 관리자 콘솔**에서 다음 명령을 입력 한 다음 **enter**키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-233">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample6.ps1)]
5. <span data-ttu-id="5ddd8-234">아래 이미지에 표시 된 것 처럼 새 열을 **Triviaquestions** 테이블에 추가 하는 **Alter Table** SQL 문을 생성 한 **업데이트 데이터베이스** 명령의 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-234">The output of the **Update-Database** command generated an **Alter Table** SQL statement to add a new column to the **TriviaQuestions** table, as shown in the image below.</span></span>

    <span data-ttu-id="5ddd8-235">![열 추가 SQL 문 생성](maintainable-azure-websites-managing-change-and-scale/_static/image9.png "열 추가 SQL 문 생성")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-235">![Add column SQL statement generated](maintainable-azure-websites-managing-change-and-scale/_static/image9.png "Add column SQL statement generated")</span></span>

    <span data-ttu-id="5ddd8-236">*열 추가 SQL 문 생성*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-236">*Add column SQL statement generated*</span></span>
6. <span data-ttu-id="5ddd8-237">**SQL Server 개체 탐색기**에서 dbo를 새로 고칩니다 **.** 새 **힌트** 열이 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-237">In **SQL Server Object Explorer**, refresh the **dbo.TriviaQuestions** table and check that the new **Hint** column is displayed.</span></span>

    <span data-ttu-id="5ddd8-238">![새 힌트 열 표시](maintainable-azure-websites-managing-change-and-scale/_static/image10.png "새 힌트 열 표시")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-238">![Showing the new Hint Column](maintainable-azure-websites-managing-change-and-scale/_static/image10.png "Showing the new Hint Column")</span></span>

    <span data-ttu-id="5ddd8-239">*새 힌트 열 표시*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-239">*Showing the new Hint Column*</span></span>
7. <span data-ttu-id="5ddd8-240">**TriviaQuestion.cs** 편집기로 돌아가서 다음 코드 조각과 같이 *Hint* 속성에 **stringlength** 제약 조건을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-240">Back in the **TriviaQuestion.cs** editor, add a **StringLength** constraint to the *Hint* property, as shown in the following code snippet.</span></span>

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample7.cs)]
8. <span data-ttu-id="5ddd8-241">**패키지 관리자 콘솔**에서 다음 명령을 입력 한 다음 **enter**키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-241">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample8.ps1)]
9. <span data-ttu-id="5ddd8-242">**패키지 관리자 콘솔**에서 다음 명령을 입력 한 다음 **enter**키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-242">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample9.ps1)]
10. <span data-ttu-id="5ddd8-243">**업데이트-데이터베이스** 명령의 출력은 아래 이미지에 나와 있는 것 처럼 **Triviaquestions** 테이블의 *힌트* 열 형식을 업데이트 하는 **Alter Table** SQL 문을 생성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-243">The output of the **Update-Database** command generated an **Alter Table** SQL statement to update the *hint* column type of the **TriviaQuestions** table, as shown in the image below.</span></span>

    <span data-ttu-id="5ddd8-244">![Alter column SQL 문이 생성 되었습니다.](maintainable-azure-websites-managing-change-and-scale/_static/image11.png "Alter column SQL 문이 생성 되었습니다.")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-244">![Alter column SQL statement generated](maintainable-azure-websites-managing-change-and-scale/_static/image11.png "Alter column SQL statement generated")</span></span>

    <span data-ttu-id="5ddd8-245">*Alter column SQL 문이 생성 되었습니다.*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-245">*Alter column SQL statement generated*</span></span>
11. <span data-ttu-id="5ddd8-246">**SQL Server 개체 탐색기**에서 dbo를 새로 고칩니다 **. TriviaQuestions** 테이블에서 **힌트** 열 형식이 **nvarchar (150)** 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-246">In **SQL Server Object Explorer**, refresh the **dbo.TriviaQuestions** table and check that the **Hint** column type is **nvarchar(150)**.</span></span>

    <span data-ttu-id="5ddd8-247">![새 제약 조건 표시](maintainable-azure-websites-managing-change-and-scale/_static/image12.png "새 제약 조건 표시")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-247">![Showing the new constraint](maintainable-azure-websites-managing-change-and-scale/_static/image12.png "Showing the new constraint")</span></span>

    <span data-ttu-id="5ddd8-248">*새 제약 조건 표시*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-248">*Showing the new constraint*</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-deploying-a-web-app-to-staging"></a><span data-ttu-id="5ddd8-249">연습 2: 스테이징에 웹 앱 배포</span><span class="sxs-lookup"><span data-stu-id="5ddd8-249">Exercise 2: Deploying a Web App to Staging</span></span>

<span data-ttu-id="5ddd8-250">**Azure App Service에서 Web Apps** 를 사용 하 여 준비 된 게시를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-250">**Web Apps in Azure App Service** enables you to perform staged publishing.</span></span> <span data-ttu-id="5ddd8-251">스테이징 된 게시를 통해 각 기본 프로덕션 사이트에 대 한 스테이징 사이트 슬롯을 만들고 중단 시간 없이 이러한 슬롯을 교환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-251">Staged publishing creates a staging site slot for each default production site and enables you to swap these slots with no down time.</span></span> <span data-ttu-id="5ddd8-252">이는 공용으로 릴리스하기 전에 변경 내용의 유효성을 검사 하 고, 사이트 콘텐츠를 증분 방식으로 통합 하 고, 변경 내용이 예상 대로 작동 하지 않는 경우 롤백하는 데 매우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-252">This is really useful to validate changes before releasing to the public, incrementally integrate site content, and roll back if changes are not working as expected.</span></span>

<span data-ttu-id="5ddd8-253">이 연습에서는 Git 소스 제어를 사용 하 여 웹 앱의 스테이징 환경에 **Geek of 퀴즈** 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-253">In this exercise, you will deploy the **Geek Quiz** application to the staging environment of your web app using Git source control.</span></span> <span data-ttu-id="5ddd8-254">이렇게 하려면 웹 앱을 만들고, 관리 포털에서 필수 구성 요소를 프로 비전 하 고, **Git** 리포지토리를 구성 하 고, 로컬 컴퓨터에서 스테이징 슬롯으로 응용 프로그램 소스 코드를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-254">To do this, you will create the web app and provision the required components at the management portal, configure a **Git** repository and push the application source code from your local computer to the staging slot.</span></span> <span data-ttu-id="5ddd8-255">또한 이전 연습에서 만든 **Code First 마이그레이션** 를 사용 하 여 프로덕션 데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-255">You will also update your production database with the **Code First Migrations** you created in the previous exercise.</span></span> <span data-ttu-id="5ddd8-256">그런 다음이 테스트 환경에서 응용 프로그램을 실행 하 여 해당 작업을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-256">You will then execute the application in this test environment to verify its operation.</span></span> <span data-ttu-id="5ddd8-257">기대에 따라 작동 하는 것이 만족 스 러 우면 응용 프로그램을 프로덕션 환경으로 승격 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-257">Once you are satisfied that it is working according to your expectations, you will promote the application to production.</span></span>

> [!NOTE]
> <span data-ttu-id="5ddd8-258">스테이징 된 게시를 사용 하도록 설정 하려면 웹 앱이 **표준 모드**여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-258">To enable staged publishing, the web app must be in **Standard mode**.</span></span> <span data-ttu-id="5ddd8-259">웹 앱을 표준 모드로 변경 하는 경우 추가 요금이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-259">Note that additional charges will be incurred if you change your web app to Standard mode.</span></span> <span data-ttu-id="5ddd8-260">가격 책정에 대 한 자세한 내용은 [App Service 가격 책정](https://azure.microsoft.com/pricing/details/app-service/)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-260">For more information about pricing, see [App Service Pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-web-app-in-azure-app-service"></a><span data-ttu-id="5ddd8-261">작업 1-Azure App Service에서 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="5ddd8-261">Task 1 – Creating a Web App in Azure App Service</span></span>

<span data-ttu-id="5ddd8-262">이 작업에서는 관리 포털에서 **Azure App Service** 웹 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-262">In this task, you will create a web app in **Azure App Service** from the management portal.</span></span> <span data-ttu-id="5ddd8-263">또한 응용 프로그램 데이터를 유지 하 고 소스 제어를 위해 로컬 Git 리포지토리를 구성 하도록 **SQL Database** 를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-263">You will also configure a **SQL Database** to persist the application data, and configure a local Git repository for source control.</span></span>

1. <span data-ttu-id="5ddd8-264">[Azure 관리 포털로](https://manage.windowsazure.com) 이동 하 여 구독과 연결 된 Microsoft 계정를 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-264">Go to the [Azure management portal](https://manage.windowsazure.com) and sign in using the Microsoft account associated with your subscription.</span></span>

    ![Azure 관리 포털에 로그인 합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image13.png)

    <span data-ttu-id="5ddd8-266">*Azure 관리 포털에 로그인 합니다.*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-266">*Sign in to the Azure management portal*</span></span>
2. <span data-ttu-id="5ddd8-267">페이지 아래쪽의 명령 모음에서 **새로 만들기** 를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-267">Click **New** in the command bar at the bottom of the page.</span></span>

    <span data-ttu-id="5ddd8-268">![새 웹 앱 만들기](maintainable-azure-websites-managing-change-and-scale/_static/image14.png "새 웹 앱 만들기")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-268">![Creating a new web app](maintainable-azure-websites-managing-change-and-scale/_static/image14.png "Creating a new web app")</span></span>

    <span data-ttu-id="5ddd8-269">*새 웹 앱 만들기*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-269">*Creating a new web app*</span></span>
3. <span data-ttu-id="5ddd8-270">**계산**, **웹 사이트** , **사용자 지정 만들기**를 차례로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-270">Click **Compute**, **Website** and then **Custom Create**.</span></span>

    <span data-ttu-id="5ddd8-271">![사용자 지정 만들기를 사용 하 여 새 웹 앱 만들기](maintainable-azure-websites-managing-change-and-scale/_static/image15.png "사용자 지정 만들기를 사용 하 여 새 웹 앱 만들기")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-271">![Creating a new web app using Custom Create](maintainable-azure-websites-managing-change-and-scale/_static/image15.png "Creating a new web app using Custom Create")</span></span>

    <span data-ttu-id="5ddd8-272">*사용자 지정 만들기를 사용 하 여 새 웹 앱 만들기*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-272">*Creating a new web app using Custom Create*</span></span>
4. <span data-ttu-id="5ddd8-273">**새 웹 사이트-사용자 지정 만들기** 대화 상자에서 사용 가능한 **URL** (예: *geek of*)을 제공 하 고, **지역** 드롭다운 목록에서 위치를 선택 하 고, **데이터베이스** 드롭다운 목록에서 **새 SQL 데이터베이스 만들기** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-273">In the **New Website - Custom Create** dialog box, provide an available **URL** (e.g. *geek-quiz*), select a location in the **Region** drop-down list, and select **Create a new SQL database** in the **Database** drop-down list.</span></span> <span data-ttu-id="5ddd8-274">마지막으로 **소스 제어에서 게시** 확인란을 선택 하 고 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-274">Finally, select the **Publish from source control** check box and click **Next**.</span></span>

    ![새 웹 앱 사용자 지정](maintainable-azure-websites-managing-change-and-scale/_static/image16.png)

    <span data-ttu-id="5ddd8-276">*새 웹 앱 사용자 지정*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-276">*Customizing the new web app*</span></span>
5. <span data-ttu-id="5ddd8-277">데이터베이스 설정에 대해 다음 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-277">Specify the following information for the database settings:</span></span>

   - <span data-ttu-id="5ddd8-278">**이름** 텍스트 상자에 데이터베이스 이름 (예: *geekquiz\_db*)을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-278">In the **Name** text box, enter a database name (e.g. *geekquiz\_db*)</span></span>
   - <span data-ttu-id="5ddd8-279">서버 **드롭다운** 목록에서 **새 SQL database 서버**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-279">In the Server **drop-down** list, select **New SQL database server**.</span></span> <span data-ttu-id="5ddd8-280">또는 기존 서버를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-280">Alternatively, you can select an existing server.</span></span>
   - <span data-ttu-id="5ddd8-281">**데이터베이스 사용자 이름** 및 **데이터베이스 암호** 상자에 SQL Database 서버에 대 한 관리자 사용자 이름 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-281">In the **Database username** and **Database password** boxes, enter the administrator username and password for the SQL database server.</span></span> <span data-ttu-id="5ddd8-282">이미 만든 서버를 선택 하는 경우 암호를 입력 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-282">If you select a server you have already created, you will be prompted for the password.</span></span>

     ![데이터베이스 설정 지정](maintainable-azure-websites-managing-change-and-scale/_static/image17.png)

     <span data-ttu-id="5ddd8-284">*데이터베이스 설정 지정*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-284">*Specifying the database settings*</span></span>
6. <span data-ttu-id="5ddd8-285">**다음**을 클릭하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-285">Click **Next** to continue.</span></span>
7. <span data-ttu-id="5ddd8-286">사용할 원본 제어에 대 한 **로컬 Git 리포지토리** 를 선택 하 고 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-286">Select **Local Git repository** for the source control to use and click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5ddd8-287">배포 자격 증명 (사용자 이름 및 암호)을 입력 하 라는 메시지가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-287">You may be prompted for the deployment credentials (a username and password).</span></span>

    ![Git 리포지토리 만들기](maintainable-azure-websites-managing-change-and-scale/_static/image18.png)

    <span data-ttu-id="5ddd8-289">*Git 리포지토리 만들기*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-289">*Creating the Git repository*</span></span>
8. <span data-ttu-id="5ddd8-290">새 웹 앱이 만들어질 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-290">Wait until the new web app is created.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5ddd8-291">기본적으로 Azure는 *azurewebsites.net* 에서 도메인을 제공 하지만 azure 관리 포털을 사용 하 여 사용자 지정 도메인을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-291">By default, Azure provides domains at *azurewebsites.net* but also gives you the possibility to set custom domains using the Azure management portal.</span></span> <span data-ttu-id="5ddd8-292">그러나 특정 Azure App Service 모드를 사용 하는 경우에만 사용자 지정 도메인을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-292">However, you can only manage custom domains if you are using certain Azure App Service modes.</span></span>
    >
    > <span data-ttu-id="5ddd8-293">Azure App Service는 무료, 공유, 기본, 표준 및 프리미엄 버전으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-293">Azure App Service is available in Free, Shared, Basic, Standard, and Premium editions.</span></span> <span data-ttu-id="5ddd8-294">무료 및 공유 모드에서는 모든 웹 앱이 다중 테 넌 트 환경에서 실행 되며 CPU, 메모리 및 네트워크 사용량에 대 한 할당량이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-294">In Free and Shared mode, all web apps run in a multi-tenant environment and have quotas for CPU, Memory, and Network usage.</span></span> <span data-ttu-id="5ddd8-295">사용 가능한 앱의 최대 수는 계획에 따라 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-295">The maximum number of free apps may vary with your plan.</span></span> <span data-ttu-id="5ddd8-296">표준 모드에서는 표준 Azure 계산 리소스에 해당 하는 전용 가상 컴퓨터에서 실행 되는 앱을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-296">In Standard mode, you choose which apps run on dedicated virtual machines that correspond to the standard Azure compute resources.</span></span> <span data-ttu-id="5ddd8-297">웹 앱 모드 구성은 웹 앱의 **크기 조정** 메뉴에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-297">You can find the web app mode configuration in the **Scale** menu of your web app.</span></span>
    >
    > <span data-ttu-id="5ddd8-298">![Azure App Service 모드](maintainable-azure-websites-managing-change-and-scale/_static/image19.png "Azure App Service 모드")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-298">![Azure App Service Modes](maintainable-azure-websites-managing-change-and-scale/_static/image19.png "Azure App Service Modes")</span></span>
    >
    > <span data-ttu-id="5ddd8-299">**공유** 또는 **표준** 모드를 사용 하는 경우에는 앱의 **구성** 메뉴로 이동 하 고 *도메인 이름*아래에서 도메인 **관리** 를 클릭 하 여 웹 앱에 대 한 사용자 지정 도메인을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-299">If you are using **Shared** or **Standard** mode, you will be able to manage custom domains for your web app by going to your app's **Configure** menu and clicking **Manage Domains** under *domain names*.</span></span>
    >
    > <span data-ttu-id="5ddd8-300">![도메인 관리](maintainable-azure-websites-managing-change-and-scale/_static/image20.png "도메인 관리")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-300">![Manage Domains](maintainable-azure-websites-managing-change-and-scale/_static/image20.png "Manage Domains")</span></span>
    >
    > <span data-ttu-id="5ddd8-301">![사용자 지정 도메인 관리](maintainable-azure-websites-managing-change-and-scale/_static/image21.png "사용자 지정 도메인 관리")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-301">![Manage Custom Domains](maintainable-azure-websites-managing-change-and-scale/_static/image21.png "Manage Custom Domains")</span></span>
9. <span data-ttu-id="5ddd8-302">웹 앱을 만든 후 **URL** 열 아래의 링크를 클릭 하 여 새 웹 앱이 실행 중인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-302">Once the web app is created, click the link under the **URL** column to check that the new web app is running.</span></span>

    ![새 웹 앱으로 이동](maintainable-azure-websites-managing-change-and-scale/_static/image22.png)

    <span data-ttu-id="5ddd8-304">*새 웹 앱으로 이동*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-304">*Browsing to the new web app*</span></span>

    ![웹 앱 실행 중](maintainable-azure-websites-managing-change-and-scale/_static/image23.png)

    <span data-ttu-id="5ddd8-306">*웹 앱 실행 중*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-306">*web app running*</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-production-sql-database"></a><span data-ttu-id="5ddd8-307">작업 2-프로덕션 SQL Database 만들기</span><span class="sxs-lookup"><span data-stu-id="5ddd8-307">Task 2 – Creating the Production SQL Database</span></span>

<span data-ttu-id="5ddd8-308">이 태스크에서는 **Entity Framework Code First 마이그레이션** 를 사용 하 여 이전 태스크에서 만든 **Azure SQL Database** 인스턴스를 대상으로 하는 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-308">In this task, you will use the **Entity Framework Code First Migrations** to create the database targeting the **Azure SQL Database** instance you created in the previous task.</span></span>

1. <span data-ttu-id="5ddd8-309">관리 포털에서 이전 작업에서 만든 웹 앱으로 이동 하 여 **대시보드로**이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-309">In the Management Portal, navigate to the web app you created in the previous task and go to its **Dashboard**.</span></span>
2. <span data-ttu-id="5ddd8-310">**대시보드** 페이지의 **빠른** 보기 섹션에서 **연결 문자열 보기** 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-310">In the **Dashboard** page, click **View connection strings** link under the **quick glance** section.</span></span>

    <span data-ttu-id="5ddd8-311">![연결 문자열 보기](maintainable-azure-websites-managing-change-and-scale/_static/image24.png "연결 문자열 보기")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-311">![View connection strings](maintainable-azure-websites-managing-change-and-scale/_static/image24.png "View connection strings")</span></span>

    <span data-ttu-id="5ddd8-312">*연결 문자열 보기*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-312">*View connection strings*</span></span>
3. <span data-ttu-id="5ddd8-313">**연결 문자열** 값을 복사 하 고 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-313">Copy the **connection string** value and close the dialog box.</span></span>

    <span data-ttu-id="5ddd8-314">![Azure 관리 포털의 연결 문자열](maintainable-azure-websites-managing-change-and-scale/_static/image25.png "Azure 관리 포털의 연결 문자열")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-314">![Connection String in Azure Management Portal](maintainable-azure-websites-managing-change-and-scale/_static/image25.png "Connection String in Azure Management Portal")</span></span>

    <span data-ttu-id="5ddd8-315">*Azure 관리 포털의 연결 문자열*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-315">*Connection String in Azure Management Portal*</span></span>
4. <span data-ttu-id="5ddd8-316">**Sql database** 를 클릭 하 여 AZURE에서 sql 데이터베이스의 목록을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-316">Click **SQL Databases** to see the list of SQL databases in Azure</span></span>

    <span data-ttu-id="5ddd8-317">![SQL Database 메뉴](maintainable-azure-websites-managing-change-and-scale/_static/image26.png "SQL Database 메뉴")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-317">![SQL Database menu](maintainable-azure-websites-managing-change-and-scale/_static/image26.png "SQL Database menu")</span></span>

    <span data-ttu-id="5ddd8-318">*SQL Database 메뉴*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-318">*SQL Database menu*</span></span>
5. <span data-ttu-id="5ddd8-319">이전 태스크에서 만든 데이터베이스를 찾아 서버를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-319">Locate the database you created in the previous task and click on the Server.</span></span>

    <span data-ttu-id="5ddd8-320">![SQL Database 서버](maintainable-azure-websites-managing-change-and-scale/_static/image27.png "SQL Database 서버")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-320">![SQL Database server](maintainable-azure-websites-managing-change-and-scale/_static/image27.png "SQL Database server")</span></span>

    <span data-ttu-id="5ddd8-321">*SQL Database 서버*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-321">*SQL Database server*</span></span>
6. <span data-ttu-id="5ddd8-322">서버의 **빠른 시작** 페이지에서 **구성**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-322">In the **Quick Start** page of the server, click on **Configure**.</span></span>

    <span data-ttu-id="5ddd8-323">![메뉴 구성](maintainable-azure-websites-managing-change-and-scale/_static/image28.png "메뉴 구성")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-323">![Configure menu](maintainable-azure-websites-managing-change-and-scale/_static/image28.png "Configure menu")</span></span>

    <span data-ttu-id="5ddd8-324">*메뉴 구성*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-324">*Configure menu*</span></span>
7. <span data-ttu-id="5ddd8-325">허용 된 ip **주소** 섹션에서 **허용 된 Ip 주소에 추가** 링크를 클릭 하 여 ip가 SQL Database 서버에 연결할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-325">In the **Allowed IP addresses** section, click on **Add to the allowed IP addresses** link to enable your IP to connect to the SQL Database server.</span></span>

    <span data-ttu-id="5ddd8-326">![허용 되는 IP 주소](maintainable-azure-websites-managing-change-and-scale/_static/image29.png "허용된 IP 주소")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-326">![Allowed IP addresses](maintainable-azure-websites-managing-change-and-scale/_static/image29.png "Allowed IP addresses")</span></span>

    <span data-ttu-id="5ddd8-327">*허용 되는 IP 주소*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-327">*Allowed IP addresses*</span></span>
8. <span data-ttu-id="5ddd8-328">페이지 아래쪽에서 **저장** 을 클릭하여 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-328">Click **Save** at the bottom of the page to complete the step.</span></span>
9. <span data-ttu-id="5ddd8-329">Visual Studio로 다시 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-329">Switch back to Visual Studio.</span></span>
10. <span data-ttu-id="5ddd8-330">**패키지 관리자 콘솔**에서 다음 명령을 실행 하 여 *[사용자의 연결 문자열]* 자리 표시자를 Azure에서 복사한 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-330">In the **Package Manager Console**, execute the following command replacing *[YOUR-CONNECTION-STRING]* placeholder with the connection string you copied from Azure</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample10.ps1)]

    <span data-ttu-id="5ddd8-331">![Windows Azure SQL Database를 대상으로 데이터베이스 업데이트](maintainable-azure-websites-managing-change-and-scale/_static/image30.png "Windows Azure SQL Database를 대상으로 데이터베이스 업데이트")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-331">![Update database targeting Windows Azure SQL Database](maintainable-azure-websites-managing-change-and-scale/_static/image30.png "Update database targeting Windows Azure SQL Database")</span></span>

    <span data-ttu-id="5ddd8-332">*데이터베이스 대상 지정 Azure SQL Database 업데이트*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-332">*Update database targeting Azure SQL Database*</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--deploying-geek-quiz-to-staging-using-git"></a><span data-ttu-id="5ddd8-333">작업 3-Git를 사용 하 여 스테이징에 Geek of 퀴즈 배포</span><span class="sxs-lookup"><span data-stu-id="5ddd8-333">Task 3 – Deploying Geek Quiz to Staging Using Git</span></span>

<span data-ttu-id="5ddd8-334">이 태스크에서는 웹 앱에서 준비 된 게시를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-334">In this task, you will enable staged publishing in your web app.</span></span> <span data-ttu-id="5ddd8-335">그런 다음 Git를 사용 하 여 로컬 컴퓨터에서 웹 앱의 스테이징 환경으로 Geek of 퀴즈 응용 프로그램을 직접 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-335">Then, you will use Git to publish the Geek Quiz application directly from your local computer to the staging environment of your web app.</span></span>

1. <span data-ttu-id="5ddd8-336">포털로 돌아가서 **이름** 열 아래에 있는 웹 앱의 이름을 클릭 하 여 관리 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-336">Go back to the portal and click the name of the web app under the **Name** column to display the management pages.</span></span>

    ![웹 앱 관리 페이지 열기](maintainable-azure-websites-managing-change-and-scale/_static/image31.png)

    <span data-ttu-id="5ddd8-338">*웹 앱 관리 페이지 열기*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-338">*Opening the web app management pages*</span></span>
2. <span data-ttu-id="5ddd8-339">**크기 조정** 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-339">Navigate to the **Scale** page.</span></span> <span data-ttu-id="5ddd8-340">**일반** 섹션에서 구성에 대해 **표준** 을 선택 하 고 명령 모음에서 **저장** 을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-340">Under the **general** section, select **Standard** for the configuration and click **Save** in the command bar.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5ddd8-341">현재 지역 및 구독의 모든 웹 앱을 **표준** 모드로 실행 하려면 **사이트 선택** 구성에서 **모두 선택** 확인란을 선택 된 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-341">To run all web apps in the current region and subscription in **Standard** mode, leave the **Select All** check box selected in the **Choose Sites** configuration.</span></span> <span data-ttu-id="5ddd8-342">그렇지 않은 경우 **모두 선택** 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-342">Otherwise, clear the **Select All** check box.</span></span>

    <span data-ttu-id="5ddd8-343">![웹 앱을 표준 모드로 업그레이드](maintainable-azure-websites-managing-change-and-scale/_static/image32.png "웹 앱을 표준 모드로 업그레이드")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-343">![Upgrading the web app to Standard mode](maintainable-azure-websites-managing-change-and-scale/_static/image32.png "Upgrading the web app to Standard mode")</span></span>

    <span data-ttu-id="5ddd8-344">*웹 앱을 표준 모드로 업그레이드*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-344">*Upgrading the Web App to Standard mode*</span></span>
3. <span data-ttu-id="5ddd8-345">**예** 를 클릭 하 여 변경 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-345">Click **Yes** to confirm the changes.</span></span>

    <span data-ttu-id="5ddd8-346">![표준 모드로 변경 확인](maintainable-azure-websites-managing-change-and-scale/_static/image33.png "웹 앱 모드 변경 계속")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-346">![Confirming the change to Standard mode](maintainable-azure-websites-managing-change-and-scale/_static/image33.png "Continuing with the changing of the web app mode")</span></span>

    <span data-ttu-id="5ddd8-347">*표준 모드로 변경 확인*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-347">*Confirming the change to Standard mode*</span></span>
4. <span data-ttu-id="5ddd8-348">**대시보드** 페이지로 이동 하 고 **빠른** 보기 섹션에서 **준비 된 게시 사용** 을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-348">Go to the **Dashboard** page and click **Enable staged publishing** under the **quick glance** section.</span></span>

    <span data-ttu-id="5ddd8-349">![준비 된 게시 사용](maintainable-azure-websites-managing-change-and-scale/_static/image34.png "준비 된 게시 사용")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-349">![Enabling staged publishing](maintainable-azure-websites-managing-change-and-scale/_static/image34.png "Enabling staged publishing")</span></span>

    <span data-ttu-id="5ddd8-350">*준비 된 게시 사용*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-350">*Enabling staged publishing*</span></span>
5. <span data-ttu-id="5ddd8-351">**예** 를 클릭 하 여 준비 된 게시를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-351">Click **Yes** to enable staged publishing.</span></span>

    <span data-ttu-id="5ddd8-352">![스테이징 된 게시 확인](maintainable-azure-websites-managing-change-and-scale/_static/image35.png "준비 된 게시를 사용 하려면 예를 클릭 합니다.")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-352">![Confirming staged publishing](maintainable-azure-websites-managing-change-and-scale/_static/image35.png "Clicking Yes to enable staged publishing")</span></span>

    <span data-ttu-id="5ddd8-353">*스테이징 된 게시 확인*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-353">*Confirming staged publishing*</span></span>
6. <span data-ttu-id="5ddd8-354">웹 앱 목록에서 웹 앱 이름의 왼쪽 표시를 확장 하 여 준비 사이트 슬롯을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-354">In the list of web apps, expand the mark to the left of your web app name to display the staging site slot.</span></span> <span data-ttu-id="5ddd8-355">웹 앱의 이름 뒤에 ***(준비)*** 가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-355">It has the name of your web app followed by ***(staging)***.</span></span> <span data-ttu-id="5ddd8-356">준비 사이트를 클릭 하 여 관리 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-356">Click the staging site to go to the management page.</span></span>

    <span data-ttu-id="5ddd8-357">![스테이징 웹 앱으로 이동](maintainable-azure-websites-managing-change-and-scale/_static/image36.png "스테이징 웹 앱으로 이동")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-357">![Navigating to the staging web app](maintainable-azure-websites-managing-change-and-scale/_static/image36.png "Navigating to the staging web app")</span></span>

    <span data-ttu-id="5ddd8-358">*준비 앱으로 이동*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-358">*Navigating to the staging app*</span></span>
7. <span data-ttu-id="5ddd8-359">관리 페이지는 다른 웹 앱의 관리 페이지와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-359">Notice that he management page looks like any other web app's management page.</span></span> <span data-ttu-id="5ddd8-360">**배포** 페이지로 이동 하 여 **Git URL** 값을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-360">Navigate to the **Deployments** page and copy the **Git URL** value.</span></span> <span data-ttu-id="5ddd8-361">이 연습에서는 나중에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-361">You will use it later in this exercise.</span></span>

    ![Git URL 값 복사](maintainable-azure-websites-managing-change-and-scale/_static/image37.png)

    <span data-ttu-id="5ddd8-363">*Git URL 값 복사*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-363">*Copying the Git URL value*</span></span>
8. <span data-ttu-id="5ddd8-364">새 **Git Bash** 콘솔을 열고 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-364">Open a new **Git Bash** console and execute the following commands.</span></span> <span data-ttu-id="5ddd8-365">이 랩의 **Source\Ex1-DeployingWebSiteToStaging\Begin** 폴더에 있는 **GeekQuiz** 솔루션의 경로를 사용 하 여 *[응용 프로그램 경로]* 자리 표시자를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-365">Update the *[YOUR-APPLICATION-PATH]* placeholder with the path to the **GeekQuiz** solution, located in the **Source\Ex1-DeployingWebSiteToStaging\Begin** folder of this lab.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample11.cmd)]

    ![Git 초기화 및 첫 번째 커밋](maintainable-azure-websites-managing-change-and-scale/_static/image38.png)

    <span data-ttu-id="5ddd8-367">*Git 초기화 및 첫 번째 커밋*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-367">*Git initialization and first commit*</span></span>
9. <span data-ttu-id="5ddd8-368">다음 명령을 실행 하 여 웹 앱을 원격 **Git** 리포지토리에 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-368">Run the following command to push your web app to the remote **Git** repository.</span></span> <span data-ttu-id="5ddd8-369">자리 표시자를 관리 포털에서 가져온 URL로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-369">Replace the placeholder with the URL you obtained from the management portal.</span></span> <span data-ttu-id="5ddd8-370">배포 암호를 입력 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-370">You will be prompted for your deployment password.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample12.cmd)]

    ![Windows Azure에 푸시](maintainable-azure-websites-managing-change-and-scale/_static/image39.png)

    <span data-ttu-id="5ddd8-372">*Azure에 푸시*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-372">*Pushing to Azure*</span></span>

    > [!NOTE]
    > <span data-ttu-id="5ddd8-373">웹 앱의 FTP 호스트 또는 GIT 리포지토리에 콘텐츠를 배포 하는 경우 웹 앱의 **빠른 시작** 또는 **대시보드** 관리 페이지에서 만든 **배포 자격 증명** 을 사용 하 여 인증 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-373">When you deploy content to the FTP host or GIT repository of a web app, you must authenticate using the **deployment credentials** that you created from the web app's **Quick Start** or **Dashboard** management pages.</span></span> <span data-ttu-id="5ddd8-374">배포 자격 증명을 모르는 경우 관리 포털을 사용 하 여 쉽게 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-374">If you do not know your deployment credentials you can easily reset them using the management portal.</span></span> <span data-ttu-id="5ddd8-375">웹 앱 **대시보드** 페이지를 열고 **배포 자격 증명 다시 설정** 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-375">Open the web app **Dashboard** page and click the **Reset your deployment credentials** link.</span></span> <span data-ttu-id="5ddd8-376">새 암호를 입력 하 고 **확인을**클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-376">Provide a new password and click **OK**.</span></span> <span data-ttu-id="5ddd8-377">배포 자격 증명은 구독과 연결 된 모든 웹 앱에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-377">Deployment credentials are valid for use with all web apps associated with your subscription.</span></span>
10. <span data-ttu-id="5ddd8-378">웹 앱이 Azure로 푸시 되었는지 확인 하려면 관리 포털로 돌아가서 **Websites**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-378">In order to verify the web app was successfully pushed to Azure, go back to the management portal and click **Websites**.</span></span>
11. <span data-ttu-id="5ddd8-379">웹 앱을 찾고 항목을 확장 하 여 스테이징 사이트 슬롯을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-379">Locate your web app and expand the entry to display the staging site slot.</span></span> <span data-ttu-id="5ddd8-380">해당 **이름을** 클릭 하 여 관리 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-380">Click its **Name** to go to the management page.</span></span>
12. <span data-ttu-id="5ddd8-381">배포 **를 클릭 하** 여 **배포 기록을**확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-381">Click **Deployments** to see the **deployment history**.</span></span> <span data-ttu-id="5ddd8-382">*&quot;초기 커밋&quot;* 를 사용 하 여 **활성 배포가** 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-382">Verify that there is an **Active Deployment** with your *&quot;Initial Commit&quot;*.</span></span>

    ![활성 배포](maintainable-azure-websites-managing-change-and-scale/_static/image40.png)

    <span data-ttu-id="5ddd8-384">*활성 배포*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-384">*Active deployment*</span></span>
13. <span data-ttu-id="5ddd8-385">마지막으로 명령 모음에서 **찾아보기** 를 클릭 하 여 웹 앱으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-385">Finally, click **Browse** in the command bar to go to the web app.</span></span>

    ![웹 앱 찾아보기](maintainable-azure-websites-managing-change-and-scale/_static/image41.png)

    <span data-ttu-id="5ddd8-387">*웹 앱 찾아보기*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-387">*Browse web app*</span></span>
14. <span data-ttu-id="5ddd8-388">응용 프로그램이 성공적으로 배포 되 면 Geek of 퀴즈 로그인 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-388">If the application is successfully deployed, you will see the Geek Quiz login page.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5ddd8-389">배포 된 응용 프로그램의 주소 URL에는 웹 앱의 이름, *-스테이징*이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-389">The address URL of the deployed application contains the name of your web app followed by *-staging*.</span></span>

    ![스테이징 환경에서 실행 되는 응용 프로그램](maintainable-azure-websites-managing-change-and-scale/_static/image42.png)

    <span data-ttu-id="5ddd8-391">*스테이징 환경에서 실행 되는 응용 프로그램*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-391">*Application running in the staging environment*</span></span>
15. <span data-ttu-id="5ddd8-392">응용 프로그램을 탐색 하려는 경우 **등록** 을 클릭 하 여 새 사용자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-392">If you wish to explore the application, click **Register** to register a new user.</span></span> <span data-ttu-id="5ddd8-393">사용자 이름, 전자 메일 주소 및 암호를 입력 하 여 계정 세부 정보를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-393">Complete the account details by entering a user name, email address and password.</span></span> <span data-ttu-id="5ddd8-394">그런 다음 응용 프로그램은 퀴즈의 첫 번째 질문을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-394">Next, the application shows the first question of the quiz.</span></span> <span data-ttu-id="5ddd8-395">몇 가지 질문에 답변 하 여 예상 대로 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-395">Answer a few questions to make sure it is working as expected.</span></span>

    ![응용 프로그램을 사용할 준비가 되었습니다.](maintainable-azure-websites-managing-change-and-scale/_static/image43.png)

    <span data-ttu-id="5ddd8-397">*응용 프로그램을 사용할 준비가 되었습니다.*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-397">*Application ready to be used*</span></span>

<a id="Ex2Task4"></a>
#### <a name="task-4--promoting-the-web-app-to-production"></a><span data-ttu-id="5ddd8-398">작업 4 – 웹 앱을 프로덕션으로 승격</span><span class="sxs-lookup"><span data-stu-id="5ddd8-398">Task 4 – Promoting the Web App to Production</span></span>

<span data-ttu-id="5ddd8-399">이제 스테이징 환경에서 웹 앱이 올바르게 작동 하는지 확인 했으므로 프로덕션으로 승격할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-399">Now that you have verified that the web app is working correctly in the staging environment, you are ready to promote it to production.</span></span> <span data-ttu-id="5ddd8-400">이 작업에서는 스테이징 사이트 슬롯을 프로덕션 사이트 슬롯으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-400">In this task, you will swap the staging site slot with the production site slot.</span></span>

1. <span data-ttu-id="5ddd8-401">관리 포털로 돌아가서 준비 사이트 슬롯을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-401">Go back to the management portal and select the staging site slot.</span></span> <span data-ttu-id="5ddd8-402">명령 모음에서 **교환** 을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-402">Click **Swap** in the command bar.</span></span>

    ![프로덕션으로 교환](maintainable-azure-websites-managing-change-and-scale/_static/image44.png)

    <span data-ttu-id="5ddd8-404">*프로덕션으로 교환*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-404">*Swap to production*</span></span>
2. <span data-ttu-id="5ddd8-405">확인 대화 상자에서 **예** 를 클릭 하 여 교환 작업을 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-405">Click **Yes** in the confirmation dialog box to proceed with the swap operation.</span></span> <span data-ttu-id="5ddd8-406">Azure는 프로덕션 사이트의 콘텐츠를 스테이징 사이트의 콘텐츠로 즉시 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-406">Azure will immediately swap the content of the production site with the content of the staging site.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5ddd8-407">준비 버전의 일부 설정은 자동으로 프로덕션 버전 (예: 연결 문자열 재정의, 처리기 매핑 등)으로 복사 되지만 다른 설정은 변경 되지 않습니다 (예: DNS 끝점, SSL 바인딩 등).</span><span class="sxs-lookup"><span data-stu-id="5ddd8-407">Some settings from the staged version will automatically be copied to the production version (e.g. connection string overrides, handler mappings, etc.) but other settings will not change (e.g. DNS endpoints, SSL bindings, etc.).</span></span>

    ![교환 작업 확인](maintainable-azure-websites-managing-change-and-scale/_static/image45.png)

    <span data-ttu-id="5ddd8-409">*교환 작업 확인*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-409">*Confirming swap operation*</span></span>
3. <span data-ttu-id="5ddd8-410">교환이 완료 되 면 프로덕션 슬롯을 선택 하 고 명령 모음에서 **찾아보기** 를 클릭 하 여 프로덕션 사이트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-410">Once the swap is complete, select the production slot and click **Browse** in the command bar to open the production site.</span></span> <span data-ttu-id="5ddd8-411">주소 표시줄에서 URL을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-411">Notice the URL in the address bar.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5ddd8-412">캐시를 지우려면 브라우저를 새로 고쳐야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-412">You might need to refresh your browser to clear cache.</span></span> <span data-ttu-id="5ddd8-413">Internet Explorer에서 **ctrl + R**을 눌러이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-413">In Internet Explorer, you can do this by pressing **CTRL+R**.</span></span>

    ![프로덕션 환경에서 실행 되는 웹 앱](maintainable-azure-websites-managing-change-and-scale/_static/image46.png)
4. <span data-ttu-id="5ddd8-415">**Gitbash** 콘솔에서 프로덕션 슬롯을 대상으로 하는 로컬 Git 리포지토리의 원격 URL을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-415">In the **GitBash** console, update the remote URL for the local Git repository to target the production slot.</span></span> <span data-ttu-id="5ddd8-416">이렇게 하려면 자리 표시자를 배포 사용자 이름으로 바꾸고 웹 앱의 이름을 바꾸는 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-416">To do this, run the following command replacing the placeholders with your deployment username and the name of your web app.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5ddd8-417">다음 연습에서는 랩의 단순성만 준비 하는 대신 프로덕션 사이트에 변경 내용을 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-417">In the following exercises, you will push changes to the production site instead of staging just for the simplicity of the lab.</span></span> <span data-ttu-id="5ddd8-418">실제 시나리오에서는 프로덕션으로 승격 하기 전에 스테이징 환경의 변경 내용을 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-418">In a real-world scenario, it is recommended to verify the changes in the staging environment before promoting to production.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample13.cmd)]

<a id="Exercise3"></a>
### <a name="exercise-3-performing-deployment-rollback-in-production"></a><span data-ttu-id="5ddd8-419">연습 3: 프로덕션 환경에서 배포 롤백 수행</span><span class="sxs-lookup"><span data-stu-id="5ddd8-419">Exercise 3: Performing Deployment Rollback in Production</span></span>

<span data-ttu-id="5ddd8-420">예를 들어 **무료** 또는 **공유** 모드로 작업 하는 경우 스테이징 및 프로덕션 사이에서 핫 교환을 수행할 준비 슬롯이 없는 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-420">There are scenarios where you do not have a staging slot to perform hot swap between staging and production, for example, if you are working with **Free** or **Shared** mode.</span></span> <span data-ttu-id="5ddd8-421">이러한 시나리오에서는 프로덕션 환경에 배포 하기 전에 로컬로 또는 원격 사이트에서 테스트 환경에서 응용 프로그램을 테스트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-421">In those scenarios, you should test your application in a testing environment –either locally or in a remote site– before deploying to production.</span></span> <span data-ttu-id="5ddd8-422">그러나 프로덕션 사이트에서 테스트 단계 중에 발견 되지 않은 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-422">However, it is possible that an issue not detected during the testing phase may arise in the production site.</span></span> <span data-ttu-id="5ddd8-423">이 경우에는 최대한 빨리 이전 및 안정적인 응용 프로그램 버전으로 쉽게 전환 하는 메커니즘을 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-423">In this case, it is important to have a mechanism to easily switch to a previous and more stable version of the application as quickly as possible.</span></span>

<span data-ttu-id="5ddd8-424">**Azure App Service**원본 제어에서 연속 배포를 수행 하면 관리 포털에서 제공 되는 **재배포** 작업을 통해이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-424">In **Azure App Service**, continuous deployment from source control makes this possible thanks to the **redeploy** action available in the management portal.</span></span> <span data-ttu-id="5ddd8-425">Azure는 리포지토리에 푸시되는 커밋에 연결 된 배포를 추적 하 고, 언제 든 지 이전 배포 중 하나를 사용 하 여 응용 프로그램을 다시 배포 하는 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-425">Azure keeps track of the deployments associated with the commits pushed to the repository and provides an option to redeploy your application using any of your previous deployments, at any time.</span></span>

<span data-ttu-id="5ddd8-426">이 연습에서는 의도적으로 *버그*를 삽입 하는 **geek of 퀴즈** 응용 프로그램의 코드를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-426">In this exercise you will perform a change to the code in the **Geek Quiz** application that intentionally injects a *bug*.</span></span> <span data-ttu-id="5ddd8-427">응용 프로그램을 프로덕션 환경에 배포 하 여 오류를 확인 한 다음 다시 배포 기능을 활용 하 여 이전 상태로 돌아갈 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-427">You will deploy the application to production to see the error, and then you will take advantage of the redeploy feature to go back to the previous state.</span></span>

<a id="Ex3Task1"></a>
#### <a name="task-1--updating-the-geek-quiz-application"></a><span data-ttu-id="5ddd8-428">작업 1 – Geek of 퀴즈 응용 프로그램 업데이트</span><span class="sxs-lookup"><span data-stu-id="5ddd8-428">Task 1 – Updating the Geek Quiz Application</span></span>

<span data-ttu-id="5ddd8-429">이 태스크에서는 코드의 작은 부분을 리팩터링 **하 여 데이터베이스** 에서 선택한 퀴즈 옵션을 검색 하는 논리의 일부를 새 메서드로 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-429">In this task, you will refactor a small piece of code of the **TriviaController** class to extract part of the logic that retrieves the selected quiz option from the database into a new method.</span></span>

1. <span data-ttu-id="5ddd8-430">이전 연습에서 **GeekQuiz** 솔루션을 사용 하 여 Visual Studio 인스턴스로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-430">Switch to the Visual Studio instance with the **GeekQuiz** solution from the previous exercise.</span></span>
2. <span data-ttu-id="5ddd8-431">**솔루션 탐색기**의 **Controllers** 폴더에서 **TriviaController.cs** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-431">In **Solution Explorer**, open the **TriviaController.cs** file inside the **Controllers** folder.</span></span>
3. <span data-ttu-id="5ddd8-432">**StoreAsync** 메서드를 찾고 다음 그림에 강조 표시 된 코드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-432">Locate the **StoreAsync** method and select the code highlighted in the following figure.</span></span>

    ![코드 선택](maintainable-azure-websites-managing-change-and-scale/_static/image47.png)

    <span data-ttu-id="5ddd8-434">*코드 선택*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-434">*Selecting the code*</span></span>
4. <span data-ttu-id="5ddd8-435">선택한 코드를 마우스 오른쪽 단추로 클릭 하 고 **리팩터링** 메뉴를 확장 한 다음 **메서드 추출 ...** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-435">Right-click the selected code, expand the **Refactor** menu and select **Extract Method...**.</span></span>

    ![새 메서드로 코드 추출](maintainable-azure-websites-managing-change-and-scale/_static/image48.png)

    <span data-ttu-id="5ddd8-437">*추출 방법 선택*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-437">*Selecting Extract Method*</span></span>
5. <span data-ttu-id="5ddd8-438">**메서드 추출** 대화 상자에서 새 메서드의 이름을 *MatchesOption* 로, **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-438">In the **Extract Method** dialog box, name the new method *MatchesOption* and click **OK**.</span></span>

    ![메서드 이름 지정](maintainable-azure-websites-managing-change-and-scale/_static/image49.png)

    <span data-ttu-id="5ddd8-440">*추출 된 메서드의 이름 지정*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-440">*Specifying the name for the extracted method*</span></span>
6. <span data-ttu-id="5ddd8-441">그런 다음 선택한 코드는 **MatchesOption** 메서드로 추출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-441">The selected code is then extracted into the **MatchesOption** method.</span></span> <span data-ttu-id="5ddd8-442">결과 코드는 다음 코드 조각에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-442">The resulting code is shown in the following snippet.</span></span>

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample14.cs)]
7. <span data-ttu-id="5ddd8-443">**Ctrl + S** 를 눌러 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-443">Press **CTRL + S** to save the changes.</span></span>

<a id="Ex3Task2"></a>
#### <a name="task-2--redeploying-the-geek-quiz-application"></a><span data-ttu-id="5ddd8-444">작업 2 – Geek of 퀴즈 응용 프로그램 재배포</span><span class="sxs-lookup"><span data-stu-id="5ddd8-444">Task 2 – Redeploying the Geek Quiz Application</span></span>

<span data-ttu-id="5ddd8-445">이제 이전 작업에서 변경한 내용을 리포지토리에 푸시하여 프로덕션 환경에 대 한 새 배포를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-445">You will now push the changes you made in the previous task to the repository, which will trigger a new deployment to the production environment.</span></span> <span data-ttu-id="5ddd8-446">그런 다음 Internet Explorer에서 제공 하는 **F12 개발 도구** 를 사용 하 여 문제를 해결 한 후 Azure 관리 포털에서 이전 배포에 대 한 롤백을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-446">Then, you will troubleshot an issue using the **F12 development tools** provided by Internet Explorer, and then perform a rollback to the previous deployment from the Azure management portal.</span></span>

1. <span data-ttu-id="5ddd8-447">새 **Git Bash** 콘솔을 열어 Azure App Service에 업데이트 된 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-447">Open a new **Git Bash** console to deploy the updated application to Azure App Service.</span></span>
2. <span data-ttu-id="5ddd8-448">다음 명령을 실행 하 여 변경 내용을 Azure에 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-448">Execute the following commands to push the changes to Azure.</span></span> <span data-ttu-id="5ddd8-449">**GeekQuiz** 솔루션에 대 한 경로를 사용 하 여 *[응용 프로그램 경로]* 자리 표시자를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-449">Update the *[YOUR-APPLICATION-PATH]* placeholder with the path to the **GeekQuiz** solution.</span></span> <span data-ttu-id="5ddd8-450">배포 암호를 입력 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-450">You will be prompted for your deployment password.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample15.cmd)]

    ![Azure에 리팩터링된 코드 푸시](maintainable-azure-websites-managing-change-and-scale/_static/image50.png)

    <span data-ttu-id="5ddd8-452">*Azure에 리팩터링된 코드 푸시*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-452">*Pushing refactored code to Azure*</span></span>
3. <span data-ttu-id="5ddd8-453">Internet Explorer를 열고 웹 앱으로 이동 합니다 (예: `http://<your-web-site>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="5ddd8-453">Open Internet Explorer and navigate to your web app (e.g. `http://<your-web-site>.azurewebsites.net`).</span></span> <span data-ttu-id="5ddd8-454">이전에 만든 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-454">Log in using the previously created credentials.</span></span>
4. <span data-ttu-id="5ddd8-455">**F12** 키를 눌러 개발 도구를 시작 하 고 **네트워크** 탭을 선택한 후 **재생** 단추를 클릭 하 여 기록을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-455">Press **F12** to launch the development tools, select the **Network** tab and click the **Play** button to start recording.</span></span>

    <span data-ttu-id="5ddd8-456">![네트워크 기록 시작](maintainable-azure-websites-managing-change-and-scale/_static/image51.png "네트워크 기록 시작")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-456">![Starting network recording](maintainable-azure-websites-managing-change-and-scale/_static/image51.png "Starting network recording")</span></span>

    <span data-ttu-id="5ddd8-457">*네트워크 기록 시작*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-457">*Starting network recording*</span></span>
5. <span data-ttu-id="5ddd8-458">퀴즈의 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-458">Select any option of the quiz.</span></span> <span data-ttu-id="5ddd8-459">아무것도 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-459">You will see that nothing happens.</span></span>
6. <span data-ttu-id="5ddd8-460">**F12** 창에서 HTTP 요청 POST에 해당 하는 항목은 http **500** 결과를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-460">In the **F12** window, the entry corresponding to the POST HTTP request shows an HTTP **500** result.</span></span>

    ![HTTP 500 오류](maintainable-azure-websites-managing-change-and-scale/_static/image52.png)

    <span data-ttu-id="5ddd8-462">*HTTP 500 오류*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-462">*HTTP 500 error*</span></span>
7. <span data-ttu-id="5ddd8-463">**콘솔** 탭을 선택 합니다. 오류의 세부 정보를 사용 하 여 오류가 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-463">Select the **Console** tab. An error is logged with the details of the cause.</span></span>

    ![기록 오류](maintainable-azure-websites-managing-change-and-scale/_static/image53.png)

    <span data-ttu-id="5ddd8-465">*기록 오류*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-465">*Logged error*</span></span>
8. <span data-ttu-id="5ddd8-466">오류의 세부 정보 부분을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-466">Locate the details part of the error.</span></span> <span data-ttu-id="5ddd8-467">이 오류는 이전 단계에서 커밋한 코드 리팩터링에 의해 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-467">Clearly, this error is caused by the code refactoring you committed in the previous steps.</span></span>

    <span data-ttu-id="5ddd8-468">`Details: LINQ to Entities does not recognize the method 'Boolean MatchesOption ...`입니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-468">`Details: LINQ to Entities does not recognize the method 'Boolean MatchesOption ...`.</span></span>
9. <span data-ttu-id="5ddd8-469">브라우저를 닫지 마세요.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-469">Do not close the browser.</span></span>
10. <span data-ttu-id="5ddd8-470">새 브라우저 인스턴스에서 [Azure 관리 포털로](https://manage.windowsazure.com) 이동 하 고 구독과 연결 된 Microsoft 계정를 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-470">In a new browser instance, navigate to the [Azure management portal](https://manage.windowsazure.com) and sign in using the Microsoft account associated with your subscription.</span></span>
11. <span data-ttu-id="5ddd8-471">**웹 사이트** 를 선택 하 고 연습 2에서 만든 웹 앱을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-471">Select **Websites** and click the web app you created in Exercise 2.</span></span>
12. <span data-ttu-id="5ddd8-472">**배포** 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-472">Navigate to the **Deployments** page.</span></span> <span data-ttu-id="5ddd8-473">수행 된 모든 커밋이 배포 기록에 나열 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-473">Notice that all the commits performed are listed in the deployment history.</span></span>

    ![기존 배포 목록](maintainable-azure-websites-managing-change-and-scale/_static/image54.png)

    <span data-ttu-id="5ddd8-475">*기존 배포 목록*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-475">*List of existing deployments*</span></span>
13. <span data-ttu-id="5ddd8-476">이전 커밋을 선택 하 고 명령 모음에서 다시 **배포** 를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-476">Select the previous commit and click **Redeploy** on the command bar.</span></span>

    ![이전 커밋 다시 배포](maintainable-azure-websites-managing-change-and-scale/_static/image55.png)

    <span data-ttu-id="5ddd8-478">*이전 커밋 다시 배포*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-478">*Redeploying the previous commit*</span></span>
14. <span data-ttu-id="5ddd8-479">확인하라는 메시지가 나타나면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-479">When prompted to confirm, click **Yes**.</span></span>

    ![재배포 확인](maintainable-azure-websites-managing-change-and-scale/_static/image56.png)
15. <span data-ttu-id="5ddd8-481">배포가 완료 되 면 웹 앱을 사용 하 여 브라우저 인스턴스로 다시 전환 하 고 **ctrl + F5**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-481">When the deployment completes, switch back to the browser instance with your web app and press **CTRL + F5**.</span></span>
16. <span data-ttu-id="5ddd8-482">옵션 중 하나를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-482">Click any of the options.</span></span> <span data-ttu-id="5ddd8-483">이제 플립 애니메이션이 발생 하 고 결과 (*올바른/잘못*됨)가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-483">The flip animation will now take place and the result (*correct/incorrect*) will be displayed.</span></span>
17. <span data-ttu-id="5ddd8-484">필드 **Git Bash** 콘솔로 전환 하 고 다음 명령을 실행 하 여 이전 커밋으로 되돌립니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-484">(Optional) Switch to the **Git Bash** console and execute the following commands to revert to the previous commit.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5ddd8-485">이러한 명령은 잘못 된 커밋에서 만든 Git 리포지토리의 모든 변경 내용을 취소 하는 새 커밋을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-485">These commands create a new commit that undoes all changes in the Git repository that were made in the bad commit.</span></span> <span data-ttu-id="5ddd8-486">그러면 Azure에서 새로운 커밋을 사용 하 여 응용 프로그램을 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-486">Azure will then redeploy the application using the new commit.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample16.cmd)]

<a id="Exercise4"></a>
### <a name="exercise-4-scaling-using-azure-storage"></a><span data-ttu-id="5ddd8-487">연습 4: Azure Storage 사용 하 여 크기 조정</span><span class="sxs-lookup"><span data-stu-id="5ddd8-487">Exercise 4: Scaling Using Azure Storage</span></span>

<span data-ttu-id="5ddd8-488">**Blob** 은 비디오, 오디오 및 이미지와 같은 대량의 구조화 되지 않은 텍스트 또는 이진 데이터를 저장 하는 가장 간단한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-488">**Blobs** are the simplest way to store large amounts of unstructured text or binary data such as video, audio and images.</span></span> <span data-ttu-id="5ddd8-489">응용 프로그램의 정적 콘텐츠를 저장소로 이동 하면 이미지 또는 문서를 브라우저에 직접 제공 하 여 응용 프로그램을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-489">Moving the static content of your application to Storage, helps to scale your application by serving images or documents directly to the browser.</span></span>

<span data-ttu-id="5ddd8-490">이 연습에서는 응용 프로그램의 정적 콘텐츠를 Blob 컨테이너로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-490">In this exercise, you will move the static content of your application to a Blob container.</span></span> <span data-ttu-id="5ddd8-491">그런 다음 콘텐츠를 Blob 컨테이너로 리디렉션하도록 **web.config** 에 **ASP.NET URL 재작성 규칙** 을 추가 하도록 응용 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-491">Then you will configure your application to add an **ASP.NET URL rewrite rule** in the **Web.config** to redirect your content to the Blob container.</span></span>

<a id="Ex4Task1"></a>
#### <a name="task-1--creating-an-azure-storage-account"></a><span data-ttu-id="5ddd8-492">작업 1-Azure Storage 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="5ddd8-492">Task 1 – Creating an Azure Storage Account</span></span>

<span data-ttu-id="5ddd8-493">이 작업에서는 관리 포털을 사용 하 여 새 저장소 계정을 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-493">In this task you will learn how to create a new storage account using the management portal.</span></span>

1. <span data-ttu-id="5ddd8-494">[Azure 관리 포털로](https://manage.windowsazure.com) 이동 하 고 구독과 연결 된 Microsoft 계정를 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-494">Navigate to the [Azure management portal](https://manage.windowsazure.com) and sign in using the Microsoft account associated with your subscription.</span></span>
2. <span data-ttu-id="5ddd8-495">**새로 만들기 | Data Services | 저장소 |** 새 저장소 계정 만들기를 시작 하기 위한 빠른 생성</span><span class="sxs-lookup"><span data-stu-id="5ddd8-495">Select **New | Data Services | Storage | Quick Create** to start creating a new storage account.</span></span> <span data-ttu-id="5ddd8-496">계정에 고유한 이름을 입력 하 고 목록에서 **지역을** 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-496">Enter a unique name for the account and select a **Region** from the list.</span></span> <span data-ttu-id="5ddd8-497">**저장소 계정 만들기** 를 클릭 하 여 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-497">Click **Create Storage Account** to continue.</span></span>

    <span data-ttu-id="5ddd8-498">![새 저장소 계정 만들기](maintainable-azure-websites-managing-change-and-scale/_static/image57.png "새 저장소 계정 만들기")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-498">![Creating a new Storage Account](maintainable-azure-websites-managing-change-and-scale/_static/image57.png "Creating a new Storage Account")</span></span>

    <span data-ttu-id="5ddd8-499">*새 저장소 계정 만들기*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-499">*Creating a new storage account*</span></span>
3. <span data-ttu-id="5ddd8-500">**저장소** 섹션에서 다음 단계를 계속 하기 위해 새 저장소 계정의 상태가 *온라인* 으로 변경 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-500">In the **Storage** section, wait until the status of the new storage account changes to *Online* in order to continue with the following step.</span></span>

    <span data-ttu-id="5ddd8-501">![저장소 계정이 만들어짐](maintainable-azure-websites-managing-change-and-scale/_static/image58.png "저장소 계정이 만들어짐")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-501">![Storage Account created](maintainable-azure-websites-managing-change-and-scale/_static/image58.png "Storage Account created")</span></span>

    <span data-ttu-id="5ddd8-502">*저장소 계정이 만들어짐*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-502">*Storage Account created*</span></span>
4. <span data-ttu-id="5ddd8-503">저장소 계정 이름을 클릭 한 다음 페이지 위쪽의 **대시보드** 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-503">Click on the storage account name and then click the **Dashboard** link at the top of the page.</span></span> <span data-ttu-id="5ddd8-504">**대시보드** 페이지는 응용 프로그램 내에서 사용할 수 있는 서비스 끝점과 계정 상태에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-504">The **Dashboard** page provides you with information about the status of the account and the service endpoints that can be used within your applications.</span></span>

    <span data-ttu-id="5ddd8-505">![저장소 계정 대시보드 표시](maintainable-azure-websites-managing-change-and-scale/_static/image59.png "저장소 계정 대시보드 표시")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-505">![Displaying the Storage Account Dashboard](maintainable-azure-websites-managing-change-and-scale/_static/image59.png "Displaying the Storage Account Dashboard")</span></span>

    <span data-ttu-id="5ddd8-506">*저장소 계정 대시보드 표시*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-506">*Displaying the Storage Account Dashboard*</span></span>
5. <span data-ttu-id="5ddd8-507">탐색 모음에서 **액세스 키 관리** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-507">Click the **Manage Access Keys** button in the navigation bar.</span></span>

    <span data-ttu-id="5ddd8-508">![액세스 키 관리 단추](maintainable-azure-websites-managing-change-and-scale/_static/image60.png "액세스 키 관리 단추")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-508">![Manage Access Keys button](maintainable-azure-websites-managing-change-and-scale/_static/image60.png "Manage Access Keys button")</span></span>

    <span data-ttu-id="5ddd8-509">*액세스 키 관리 단추*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-509">*Manage Access Keys button*</span></span>
6. <span data-ttu-id="5ddd8-510">**액세스 키 관리** 대화 상자에서 **저장소 계정 이름** 및 **기본 액세스 키** 를 다음 연습에서 필요에 따라 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-510">In the **Manage Access Keys** dialog box, copy the **Storage Account Name** and **Primary Access Key** as you will need them in the following exercise.</span></span> <span data-ttu-id="5ddd8-511">그런 다음 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-511">Then, close the dialog box.</span></span>

    <span data-ttu-id="5ddd8-512">![액세스 키 관리 대화 상자](maintainable-azure-websites-managing-change-and-scale/_static/image61.png "액세스 키 관리 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-512">![Manage Access Key dialog box](maintainable-azure-websites-managing-change-and-scale/_static/image61.png "Manage Access Key dialog box")</span></span>

    <span data-ttu-id="5ddd8-513">*액세스 키 관리 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-513">*Manage Access Key dialog box*</span></span>

<a id="Ex4Task2"></a>
#### <a name="task-2--uploading-an-asset-to-azure-blob-storage"></a><span data-ttu-id="5ddd8-514">작업 2-Azure Blob Storage에 자산 업로드</span><span class="sxs-lookup"><span data-stu-id="5ddd8-514">Task 2 – Uploading an Asset to Azure Blob Storage</span></span>

<span data-ttu-id="5ddd8-515">이 작업에서는 Visual Studio의 서버 탐색기 창을 사용 하 여 저장소 계정에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-515">In this task, you will use the Server Explorer window from Visual Studio to connect to your storage account.</span></span> <span data-ttu-id="5ddd8-516">그런 다음 blob 컨테이너를 만들고 Geek of 퀴즈 로고가 포함 된 파일을 컨테이너에 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-516">You will then create a blob container and upload a file with the Geek Quiz logo to the container.</span></span>

1. <span data-ttu-id="5ddd8-517">이전 연습에서 **GeekQuiz** 솔루션을 사용 하 여 Visual Studio 인스턴스로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-517">Switch to the Visual Studio instance with the **GeekQuiz** solution from the previous exercise.</span></span>
2. <span data-ttu-id="5ddd8-518">메뉴 모음에서 **보기** 를 선택 하 고 **서버 탐색기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-518">From the menu bar, select **View** and then click **Server Explorer**.</span></span>
3. <span data-ttu-id="5ddd8-519">**서버 탐색기**에서 **azure** 노드를 마우스 오른쪽 단추로 클릭 하 고 **azure에 연결 ...을**선택 합니다. 구독과 연결 된 Microsoft 계정를 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-519">In **Server Explorer**, right-click the **Azure** node and select **Connect to Azure...**. Sign in using the Microsoft account associated with your subscription.</span></span>

    ![Windows Azure에 연결](maintainable-azure-websites-managing-change-and-scale/_static/image62.png)

    <span data-ttu-id="5ddd8-521">*Azure에 연결*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-521">*Connect to Azure*</span></span>
4. <span data-ttu-id="5ddd8-522">**Azure** 노드를 확장 하 고 **저장소** 를 마우스 오른쪽 단추로 클릭 한 다음 **외부 저장소 연결**...을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-522">Expand the **Azure** node, right-click **Storage** and select **Attach External Storage...**.</span></span>
5. <span data-ttu-id="5ddd8-523">**새 저장소 계정 추가** 대화 상자에서 이전 작업에서 받은 **계정 이름** 및 **계정 키** 를 입력 하 고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-523">In the **Add New Storage Account** dialog box, enter the **Account name** and **Account key** you obtained in the previous task and click **OK**.</span></span>

    ![새 저장소 계정 추가 대화 상자](maintainable-azure-websites-managing-change-and-scale/_static/image63.png)

    <span data-ttu-id="5ddd8-525">*새 저장소 계정 추가 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-525">*Add New Storage Account dialog box*</span></span>
6. <span data-ttu-id="5ddd8-526">저장소 계정이 **저장소** 노드 아래에 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-526">Your storage account should appear under the **Storage** node.</span></span> <span data-ttu-id="5ddd8-527">저장소 계정을 확장 하 고 **blob** 을 마우스 오른쪽 단추로 클릭 한 다음 **blob 컨테이너 만들기**...를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-527">Expand your storage account, right-click **Blobs** and select **Create Blob Container...**.</span></span>

    <span data-ttu-id="5ddd8-528">![Blob 컨테이너 만들기](maintainable-azure-websites-managing-change-and-scale/_static/image64.png "Blob 컨테이너 만들기")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-528">![Create Blob Container](maintainable-azure-websites-managing-change-and-scale/_static/image64.png "Create Blob Container")</span></span>

    <span data-ttu-id="5ddd8-529">*Blob 컨테이너 만들기*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-529">*Create Blob Container*</span></span>
7. <span data-ttu-id="5ddd8-530">**Blob 컨테이너 만들기** 대화 상자에서 blob 컨테이너의 이름을 입력 하 고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-530">In the **Create Blob Container** dialog box, enter a name for the blob container and click **OK**.</span></span>

    <span data-ttu-id="5ddd8-531">![Blob 컨테이너 만들기 대화 상자](maintainable-azure-websites-managing-change-and-scale/_static/image65.png "Blob 컨테이너 만들기 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-531">![Create Blob Container dialog box](maintainable-azure-websites-managing-change-and-scale/_static/image65.png "Create Blob Container dialog box")</span></span>

    <span data-ttu-id="5ddd8-532">*Blob 컨테이너 만들기 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-532">*Create Blob Container dialog box*</span></span>
8. <span data-ttu-id="5ddd8-533">새 blob 컨테이너를 **blob** 노드에 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-533">The new blob container should be added to the **Blobs** node.</span></span> <span data-ttu-id="5ddd8-534">컨테이너의 액세스 권한을 변경 하 여 컨테이너를 공용으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-534">Change the access permissions in the container to make the container public.</span></span> <span data-ttu-id="5ddd8-535">이렇게 하려면 **images** 컨테이너를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-535">To do this, right-click the **images** container and select **Properties**.</span></span>

    <span data-ttu-id="5ddd8-536">![images 컨테이너 속성](maintainable-azure-websites-managing-change-and-scale/_static/image66.png "images 컨테이너 속성")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-536">![images container properties](maintainable-azure-websites-managing-change-and-scale/_static/image66.png "images container properties")</span></span>

    <span data-ttu-id="5ddd8-537">*Images 컨테이너 속성*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-537">*Images container properties*</span></span>
9. <span data-ttu-id="5ddd8-538">**속성** 창에서 **컨테이너**에 대 한 **공용 읽기 권한을** 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-538">In the **Properties** window, set the **Public Read Access** to **Container**.</span></span>

    <span data-ttu-id="5ddd8-539">![공용 읽기 액세스 속성 변경](maintainable-azure-websites-managing-change-and-scale/_static/image67.png "공용 읽기 액세스 속성 변경")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-539">![Changing public read access property](maintainable-azure-websites-managing-change-and-scale/_static/image67.png "Changing public read access property")</span></span>

    <span data-ttu-id="5ddd8-540">*공용 읽기 액세스 속성 변경*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-540">*Changing public read access property*</span></span>
10. <span data-ttu-id="5ddd8-541">공용 액세스 속성을 변경 하 시겠습니까? 라는 메시지가 표시 되 면 **예**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-541">When prompted if you are sure you want to change the public access property, click **Yes**.</span></span>

    <span data-ttu-id="5ddd8-542">![Microsoft Visual Studio 경고](maintainable-azure-websites-managing-change-and-scale/_static/image68.png "Microsoft Visual Studio 경고")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-542">![Microsoft Visual Studio warning](maintainable-azure-websites-managing-change-and-scale/_static/image68.png "Microsoft Visual Studio warning")</span></span>

    <span data-ttu-id="5ddd8-543">*Microsoft Visual Studio 경고*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-543">*Microsoft Visual Studio warning*</span></span>
11. <span data-ttu-id="5ddd8-544">**서버 탐색기**에서 **images** blob 컨테이너를 마우스 오른쪽 단추로 클릭 하 고 **blob 컨테이너 보기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-544">In **Server Explorer**, right-click in the **images** blob container and select **View Blob Container**.</span></span>

    <span data-ttu-id="5ddd8-545">![Blob 컨테이너 보기](maintainable-azure-websites-managing-change-and-scale/_static/image69.png "Blob 컨테이너 보기")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-545">![View Blob Container](maintainable-azure-websites-managing-change-and-scale/_static/image69.png "View Blob Container")</span></span>

    <span data-ttu-id="5ddd8-546">*Blob 컨테이너 보기*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-546">*View Blob Container*</span></span>
12. <span data-ttu-id="5ddd8-547">이미지 컨테이너가 새 창에서 열리고 항목이 없는 범례가 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-547">The images container should open in a new window and a legend with no entries should be shown.</span></span> <span data-ttu-id="5ddd8-548">**업로드** 아이콘을 클릭 하 여 blob 컨테이너에 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-548">Click the **upload** icon to upload a file to the blob container.</span></span>

    <span data-ttu-id="5ddd8-549">![항목이 없는 Images 컨테이너](maintainable-azure-websites-managing-change-and-scale/_static/image70.png "항목이 없는 Images 컨테이너")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-549">![Images container with no entries](maintainable-azure-websites-managing-change-and-scale/_static/image70.png "Images container with no entries")</span></span>

    <span data-ttu-id="5ddd8-550">*항목이 없는 Images 컨테이너*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-550">*Images container with no entries*</span></span>
13. <span data-ttu-id="5ddd8-551">**Blob 업로드** 대화 상자에서 랩의 **자산** 폴더로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-551">In the **Upload Blob** dialog box, navigate to the **Assets** folder of the lab.</span></span> <span data-ttu-id="5ddd8-552">**Logo-big** 파일을 선택 하 고 **열기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-552">Select the **logo-big.png** file and click **Open**.</span></span>
14. <span data-ttu-id="5ddd8-553">파일이 업로드 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-553">Wait until the file is uploaded.</span></span> <span data-ttu-id="5ddd8-554">업로드가 완료 되 면 파일이 images 컨테이너에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-554">When the upload completes, the file should be listed in the images container.</span></span> <span data-ttu-id="5ddd8-555">파일 항목을 마우스 오른쪽 단추로 클릭 하 고 **URL 복사**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-555">Right-click the file entry and select **Copy URL**.</span></span>

    <span data-ttu-id="5ddd8-556">![Blob URL 복사](maintainable-azure-websites-managing-change-and-scale/_static/image71.png "Blob 파일 URL 복사")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-556">![Copy blob URL](maintainable-azure-websites-managing-change-and-scale/_static/image71.png "Copy blob file URL")</span></span>

    <span data-ttu-id="5ddd8-557">*Blob URL 복사*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-557">*Copy blob URL*</span></span>
15. <span data-ttu-id="5ddd8-558">Internet Explorer를 열고 URL을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-558">Open Internet Explorer and paste the URL.</span></span> <span data-ttu-id="5ddd8-559">다음 이미지는 브라우저에 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-559">The following image should be shown in the browser.</span></span>

    <span data-ttu-id="5ddd8-560">![Windows Blob Storage의 logo-big 이미지](maintainable-azure-websites-managing-change-and-scale/_static/image72.png "저장소의 logo-big 이미지")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-560">![logo-big.png image from Windows Blob Storage](maintainable-azure-websites-managing-change-and-scale/_static/image72.png "logo-big.png image from storage")</span></span>

    <span data-ttu-id="5ddd8-561">*Azure Blob Storage logo-big 이미지*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-561">*logo-big.png image from Azure Blob Storage*</span></span>

<a id="Ex4Task3"></a>
#### <a name="task-3--updating-the-solution-to-consume-static-content-from-azure-blob-storage"></a><span data-ttu-id="5ddd8-562">작업 3 – Azure Blob Storage의 정적 콘텐츠를 사용 하도록 솔루션 업데이트</span><span class="sxs-lookup"><span data-stu-id="5ddd8-562">Task 3 – Updating the Solution to Consume Static Content from Azure Blob Storage</span></span>

<span data-ttu-id="5ddd8-563">이 작업에서는 **web.config 파일에** ASP.NET URL 재작성 규칙을 추가 하 여 Azure Blob Storage (웹 앱에 있는 이미지 대신)에 업로드 된 이미지를 사용 하도록 **GeekQuiz** 솔루션을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-563">In this task, you will configure the **GeekQuiz** solution to consume the image uploaded to Azure Blob Storage (instead of the image located in the web app) by adding an ASP.NET URL rewrite rule in the **web.config** file.</span></span>

1. <span data-ttu-id="5ddd8-564">Visual Studio에서 **GeekQuiz** 프로젝트 내의 **web.config 파일을** 열고 **&lt;system.webserver&gt;** 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-564">In Visual Studio, open the **Web.config** file inside the **GeekQuiz** project and locate the **&lt;system.webServer&gt;** element.</span></span>
2. <span data-ttu-id="5ddd8-565">다음 코드를 추가 하 여 URL 다시 쓰기 규칙을 추가 하 고, 자리 표시자를 저장소 계정 이름으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-565">Add the following code to add an URL rewrite rule, updating the placeholder with your storage account name.</span></span>

    <span data-ttu-id="5ddd8-566">(코드 조각- *WebSitesInProduction-Ex4-UrlRewriteRule*)</span><span class="sxs-lookup"><span data-stu-id="5ddd8-566">(Code Snippet - *WebSitesInProduction - Ex4 - UrlRewriteRule*)</span></span>

    [!code-xml[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample17.xml)]

    > [!NOTE]
    > <span data-ttu-id="5ddd8-567">URL 다시 쓰기는 들어오는 웹 요청을 가로채 고 요청을 다른 리소스로 리디렉션하는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-567">URL rewriting is the process of intercepting an incoming Web request and redirecting the request to a different resource.</span></span> <span data-ttu-id="5ddd8-568">URL 다시 쓰기 규칙은 요청을 리디렉션해야 할 때 다시 작성 엔진에 지시 하 고,이를 리디렉션해야 하는 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-568">The URL rewriting rules tells the rewriting engine when a request needs to be redirected, and where should they be redirected.</span></span> <span data-ttu-id="5ddd8-569">재작성 규칙은 요청 된 URL에서 찾을 패턴 (일반적으로 정규식 사용)과 패턴을 대체할 문자열 (있는 경우)의 두 문자열로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-569">A rewriting rule is composed of two strings: the pattern to look for in the requested URL (usually, using regular expressions), and the string to replace the pattern with, if found.</span></span> <span data-ttu-id="5ddd8-570">자세한 내용은 [ASP.NET에서 URL 다시 작성](https://msdn.microsoft.com/library/ms972974.aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-570">For more information, see [URL Rewriting in ASP.NET](https://msdn.microsoft.com/library/ms972974.aspx).</span></span>
3. <span data-ttu-id="5ddd8-571">**Ctrl + S** 를 눌러 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-571">Press **CTRL + S** to save the changes.</span></span>
4. <span data-ttu-id="5ddd8-572">새 **Git Bash** 콘솔을 열어 Azure App Service에 업데이트 된 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-572">Open a new **Git Bash** console to deploy the updated application to Azure App Service.</span></span>
5. <span data-ttu-id="5ddd8-573">다음 명령을 실행 하 여 변경 내용을 Azure에 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-573">Execute the following commands to push the changes to Azure.</span></span> <span data-ttu-id="5ddd8-574">**GeekQuiz** 솔루션에 대 한 경로를 사용 하 여 *[응용 프로그램 경로]* 자리 표시자를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-574">Update the *[YOUR-APPLICATION-PATH]* placeholder with the path to the **GeekQuiz** solution.</span></span> <span data-ttu-id="5ddd8-575">배포 암호를 입력 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-575">You will be prompted for your deployment password.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample18.cmd)]

    ![Azure에 업데이트 배포](maintainable-azure-websites-managing-change-and-scale/_static/image73.png)

    <span data-ttu-id="5ddd8-577">*Azure에 업데이트 배포*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-577">*Deploying update to Azure*</span></span>

<a id="Ex4Task4"></a>
#### <a name="task-4--verification"></a><span data-ttu-id="5ddd8-578">작업 4 – 확인</span><span class="sxs-lookup"><span data-stu-id="5ddd8-578">Task 4 – Verification</span></span>

<span data-ttu-id="5ddd8-579">이 작업에서는 **Internet Explorer** 를 사용 하 여 **geek of 퀴즈** 응용 프로그램을 검색 하 고 이미지에 대 한 URL 재작성 규칙이 작동 하는지 확인 하 고 **Azure Blob Storage**에서 호스트 되는 이미지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-579">In this task you will use **Internet Explorer** to browse the **Geek Quiz** application and check that the URL rewrite rule for images works and you are redirected to the image hosted on **Azure Blob Storage**.</span></span>

1. <span data-ttu-id="5ddd8-580">Internet Explorer를 열고 웹 앱으로 이동 합니다 (예: `http://<your-web-site>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="5ddd8-580">Open Internet Explorer and navigate to your web app (e.g. `http://<your-web-site>.azurewebsites.net`).</span></span> <span data-ttu-id="5ddd8-581">이전에 만든 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-581">Log in using the previously created credentials.</span></span>

    <span data-ttu-id="5ddd8-582">![이미지를 사용 하 여 Geek of 퀴즈 웹 앱 표시](maintainable-azure-websites-managing-change-and-scale/_static/image74.png "이미지를 사용 하 여 Geek of 퀴즈 웹 앱 표시")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-582">![Showing the Geek Quiz web app with the image](maintainable-azure-websites-managing-change-and-scale/_static/image74.png "Showing the Geek Quiz web app with the image")</span></span>

    <span data-ttu-id="5ddd8-583">*이미지를 사용 하 여 Geek of 퀴즈 웹 앱 표시*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-583">*Showing the Geek Quiz web app with the image*</span></span>
2. <span data-ttu-id="5ddd8-584">**F12** 키를 눌러 개발 도구를 시작 하 고 **네트워크** 탭을 선택한 후 기록을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-584">Press **F12** to launch the development tools, select the **Network** tab and start recording.</span></span>

    <span data-ttu-id="5ddd8-585">![네트워크 기록 시작](maintainable-azure-websites-managing-change-and-scale/_static/image75.png "네트워크 기록 시작")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-585">![Starting network recording](maintainable-azure-websites-managing-change-and-scale/_static/image75.png "Starting network recording")</span></span>

    <span data-ttu-id="5ddd8-586">*네트워크 기록 시작*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-586">*Starting network recording*</span></span>
3. <span data-ttu-id="5ddd8-587">**Ctrl +** f 5를 눌러 웹 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-587">Press **CTRL + F5** to refresh the web page.</span></span>
4. <span data-ttu-id="5ddd8-588">페이지가 로드 되 면 http **301** 결과 (리디렉션)를 사용 하는 **/img/logo-big.png** URL에 대 한 http 요청 및 http **200** 결과와 `http://[YOUR-STORAGE-ACCOUNT].blob.core.windows.net/images/logo-big.png` url에 대 한 다른 요청이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-588">Once the page has finished loading, you should see an HTTP request for the **/img/logo-big.png** URL with an HTTP **301** result (redirect) and another request for `http://[YOUR-STORAGE-ACCOUNT].blob.core.windows.net/images/logo-big.png` URL with a HTTP **200** result.</span></span>

    <span data-ttu-id="5ddd8-589">![URL 리디렉션 확인](maintainable-azure-websites-managing-change-and-scale/_static/image76.png "개발자 도구에서 리디렉션 표시")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-589">![Verifying the URL redirect](maintainable-azure-websites-managing-change-and-scale/_static/image76.png "Showing the redirect in Dev Tools")</span></span>

    <span data-ttu-id="5ddd8-590">*URL 리디렉션 확인*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-590">*Verifying the URL redirect*</span></span>

<a id="Exercise5"></a>
### <a name="exercise-5-using-autoscale-for-web-apps"></a><span data-ttu-id="5ddd8-591">연습 5: Web Apps에 자동 크기 조정 사용</span><span class="sxs-lookup"><span data-stu-id="5ddd8-591">Exercise 5: Using Autoscale for Web Apps</span></span>

> [!NOTE]
> <span data-ttu-id="5ddd8-592">이 연습은 **Visual Studio 2013 Ultimate Edition**에서만 사용할 수 있는 웹 로드 &amp; 성능 테스트에 대 한 지원이 필요 하기 때문에 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-592">This exercise is optional, since it requires support for Web Load &amp; Performance Testing which is only available for **Visual Studio 2013 Ultimate Edition**.</span></span> <span data-ttu-id="5ddd8-593">특정 Visual Studio 2013 기능에 대 한 자세한 내용은 [여기](https://www.microsoft.com/visualstudio/eng/products/compare)에서 버전을 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-593">For more information on specific Visual Studio 2013 features, compare versions [here](https://www.microsoft.com/visualstudio/eng/products/compare).</span></span>

<span data-ttu-id="5ddd8-594">**Azure App Service Web Apps** 는 **표준 모드**에서 실행 되는 웹 앱에 대 한 자동 크기 조정 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-594">**Azure App Service Web Apps** provides the Autoscale feature for web apps running in **Standard Mode**.</span></span> <span data-ttu-id="5ddd8-595">자동 크기 조정을 통해 Azure는 부하에 따라 웹 앱의 인스턴스 수를 자동으로 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-595">Autoscale lets Azure automatically scale the instance count of your web app depending on the load.</span></span> <span data-ttu-id="5ddd8-596">자동 크기 조정을 사용 하는 경우 Azure는 5 분 마다 웹 앱의 CPU를 확인 하 고 해당 시점에 필요에 따라 인스턴스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-596">When Autoscale is enabled, Azure checks the CPU of your web app once every five minutes and adds instances as needed at that point in time.</span></span> <span data-ttu-id="5ddd8-597">CPU 사용량이 낮은 경우 Azure는 웹 앱의 성능이 저하 되지 않도록 2 시간 마다 한 번씩 인스턴스를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-597">If the CPU usage is low, Azure will remove instances once every two hours to ensure that the performance of your web app is not degraded.</span></span>

<span data-ttu-id="5ddd8-598">이 연습에서는 **Geek of 퀴즈** 웹 앱에 대 한 **자동 크기 조정** 기능을 구성 하는 데 필요한 단계를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-598">In this exercise you will go through the steps required to configure the **Autoscale** feature for the **Geek Quiz** web app.</span></span> <span data-ttu-id="5ddd8-599">응용 프로그램에서 인스턴스 업그레이드를 트리거하기 위한 충분 한 CPU 부하를 생성 하기 위해 Visual Studio 부하 테스트를 실행 하 여이 기능을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-599">You will verify this feature by running a Visual Studio load test to generate enough CPU load on the application to trigger an instance upgrade.</span></span>

<a id="Ex5Task1"></a>
#### <a name="task-1--configuring-autoscale-based-on-the-cpu-metric"></a><span data-ttu-id="5ddd8-600">작업 1-CPU 메트릭에 따라 자동 크기 조정 구성</span><span class="sxs-lookup"><span data-stu-id="5ddd8-600">Task 1 – Configuring Autoscale Based on the CPU Metric</span></span>

<span data-ttu-id="5ddd8-601">이 작업에서는 Azure 관리 포털을 사용 하 여 연습 2에서 만든 웹 앱에 대 한 자동 크기 조정 기능을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-601">In this task you will use the Azure management portal to enable the Autoscale feature for the web app you created in Exercise 2.</span></span>

1. <span data-ttu-id="5ddd8-602">[Azure 관리 포털](https://manage.windowsazure.com/)에서 **웹 사이트** 를 선택 하 고 연습 2에서 만든 웹 앱을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-602">In the [Azure management portal](https://manage.windowsazure.com/), select **Websites** and click the web app you created in Exercise 2.</span></span>
2. <span data-ttu-id="5ddd8-603">**크기 조정** 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-603">Navigate to the **Scale** page.</span></span> <span data-ttu-id="5ddd8-604">**용량** 섹션에서 **메트릭 별 크기 조정** 구성에 대해 **CPU** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-604">Under the **capacity** section, select **CPU** for the **Scale by Metric** configuration.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5ddd8-605">CPU를 기준으로 크기를 조정 하는 경우 Azure는 CPU 사용량이 변경 될 경우 앱이 사용 하는 인스턴스 수를 동적으로 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-605">When scaling by CPU, Azure dynamically adjusts the number of instances that the app uses if the CPU usage changes.</span></span>

    <span data-ttu-id="5ddd8-606">![CPU 별로 크기를 조정 하도록 선택](maintainable-azure-websites-managing-change-and-scale/_static/image77.png "자동 크기 조정에 대 한 CPU 메트릭 선택")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-606">![Selecting to scale by CPU](maintainable-azure-websites-managing-change-and-scale/_static/image77.png "Selecting the CPU metric for auto scaling")</span></span>

    <span data-ttu-id="5ddd8-607">*CPU 별로 크기를 조정 하도록 선택*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-607">*Selecting to scale by CPU*</span></span>
3. <span data-ttu-id="5ddd8-608">**대상 CPU** 구성을 **20**-**40** %로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-608">Change the **Target CPU** configuration to **20**-**40** percent.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5ddd8-609">이 범위는 웹 앱에 대 한 평균 CPU 사용량을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-609">This range represents the average CPU usage for your web app.</span></span> <span data-ttu-id="5ddd8-610">Azure에서 인스턴스를 추가 하거나 제거 하 여 웹 앱을이 범위에 보관 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-610">Azure will add or remove instances to keep your web app in this range.</span></span> <span data-ttu-id="5ddd8-611">크기 조정에 사용 되는 최소 및 최대 인스턴스 수는 **인스턴스 수** 구성에 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-611">The minimum and maximum number of instances used for scaling is specified in the **Instance Count** configuration.</span></span> <span data-ttu-id="5ddd8-612">Azure는 이러한 제한을 초과 하거나 초과 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-612">Azure will never go above or beyond that limit.</span></span>
    >
    > <span data-ttu-id="5ddd8-613">기본 **대상 CPU** 값은이 랩의 목적 으로만 수정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-613">The default **Target CPU** values are modified just for the purposes of this lab.</span></span> <span data-ttu-id="5ddd8-614">작은 값을 사용 하 여 CPU 범위를 구성 하면 응용 프로그램에 보통 부하가 배치 될 때 자동 크기 조정을 트리거할 가능성이 높아집니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-614">By configuring the CPU range with small values, you are increasing the chances to trigger Autoscale when a moderate load is placed on the application.</span></span>

    <span data-ttu-id="5ddd8-615">![대상 CPU를 20 ~ 40% 사이로 변경](maintainable-azure-websites-managing-change-and-scale/_static/image78.png "대상 CPU를 20 ~ 40% 사이로 변경")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-615">![Changing the target CPU to be between 20 and 40 percent](maintainable-azure-websites-managing-change-and-scale/_static/image78.png "Changing the target CPU to be between 20 and 40 percent")</span></span>

    <span data-ttu-id="5ddd8-616">*대상 CPU를 20 ~ 40% 사이로 변경*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-616">*Changing the Target CPU to be between 20 and 40 percent*</span></span>
4. <span data-ttu-id="5ddd8-617">명령 모음에서 **저장** 을 클릭 하 여 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-617">Click **Save** in the command bar to save the changes.</span></span>

<a id="Ex5Task2"></a>
#### <a name="task-2--load-testing-with-visual-studio"></a><span data-ttu-id="5ddd8-618">작업 2-Visual Studio를 사용 하 여 부하 테스트</span><span class="sxs-lookup"><span data-stu-id="5ddd8-618">Task 2 – Load Testing with Visual Studio</span></span>

<span data-ttu-id="5ddd8-619">**자동 크기 조정을** 구성 했으므로 웹 앱에서 일부 CPU 로드를 생성 하기 위해 Visual Studio에서 **웹 성능 및 부하 테스트 프로젝트** 를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-619">Now that **Autoscale** has been configured, you will create a **Web Performance and Load Test Project** in Visual Studio to generate some CPU load on your web app.</span></span>

1. <span data-ttu-id="5ddd8-620">**Visual Studio Ultimate 2013** 열고 [파일]을 선택 합니다. **| 새로 만들기 | 프로젝트** ... 새 솔루션을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-620">Open **Visual Studio Ultimate 2013** and select **File | New | Project...** to start a new solution.</span></span>

    <span data-ttu-id="5ddd8-621">![새 프로젝트 만들기](maintainable-azure-websites-managing-change-and-scale/_static/image79.png "새 프로젝트 만들기")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-621">![Creating a new project](maintainable-azure-websites-managing-change-and-scale/_static/image79.png "Creating a new project")</span></span>

    <span data-ttu-id="5ddd8-622">*새 프로젝트 만들기*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-622">*Creating a new project*</span></span>
2. <span data-ttu-id="5ddd8-623">**새 프로젝트** 대화 상자의 시각적 개체  **C# 에서 웹 성능 및 부하 테스트 프로젝트를 선택 합니다. 테스트** 탭. **.NET Framework 4.5** 가 선택 되어 있는지 확인 하 고, 프로젝트 이름을 *WebAndLoadTestProject*로 지정 하 고, **위치** 를 선택 하 고, **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-623">In the **New Project** dialog box, select **Web Performance and Load Test Project** under the **Visual C# | Test** tab. Make sure **.NET Framework 4.5** is selected, name the project *WebAndLoadTestProject*, choose a **Location** and click **OK**.</span></span>

    <span data-ttu-id="5ddd8-624">![새 웹 및 부하 테스트 프로젝트 만들기](maintainable-azure-websites-managing-change-and-scale/_static/image80.png "새 웹 및 부하 테스트 프로젝트 만들기")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-624">![Creating a new Web and Load Test project](maintainable-azure-websites-managing-change-and-scale/_static/image80.png "Creating a new Web and Load Test project")</span></span>

    <span data-ttu-id="5ddd8-625">*새 웹 및 부하 테스트 프로젝트 만들기*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-625">*Creating a new Web and Load Test project*</span></span>
3. <span data-ttu-id="5ddd8-626">**Webtest1.webtest** 에서 **Webtest1.webtest** 노드를 마우스 오른쪽 단추로 클릭 하 고 **요청 추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-626">In the **WebTest1.webtest** Right-click the **WebTest1** node and click **Add Request**.</span></span>

    <span data-ttu-id="5ddd8-627">![Webtest1.webtest에 요청 추가](maintainable-azure-websites-managing-change-and-scale/_static/image81.png "Webtest1.webtest에 요청 추가")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-627">![Adding a request to WebTest1](maintainable-azure-websites-managing-change-and-scale/_static/image81.png "Adding a request to WebTest1")</span></span>

    <span data-ttu-id="5ddd8-628">*Webtest1.webtest에 요청 추가*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-628">*Adding a request to WebTest1*</span></span>
4. <span data-ttu-id="5ddd8-629">새 요청 노드의 **속성** 창에서 **url** 속성을 업데이트 하 여 웹 앱의 url (예: *[http://geek-quiz.azurewebsites.net/](http://geek-quiz.azurewebsites.net/)* )을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-629">In the **Properties** window of the new request node, update the **Url** property to point to the URL of your web app (e.g. *[http://geek-quiz.azurewebsites.net/](http://geek-quiz.azurewebsites.net/)*).</span></span>

    <span data-ttu-id="5ddd8-630">![Url 속성 변경](maintainable-azure-websites-managing-change-and-scale/_static/image82.png "Url 속성 변경")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-630">![Changing the Url property](maintainable-azure-websites-managing-change-and-scale/_static/image82.png "Changing the Url property")</span></span>

    <span data-ttu-id="5ddd8-631">*Url 속성 변경*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-631">*Changing the Url property*</span></span>
5. <span data-ttu-id="5ddd8-632">**Webtest1.webtest** 창에서 **webtest1.webtest** 를 마우스 오른쪽 단추로 클릭 하 고 **루프 추가**...를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-632">In the **WebTest1.webtest** window, right-click **WebTest1** and click **Add Loop...**.</span></span>

    <span data-ttu-id="5ddd8-633">![Webtest1.webtest에 루프 추가](maintainable-azure-websites-managing-change-and-scale/_static/image83.png "Webtest1.webtest에 루프 추가")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-633">![Adding a loop to WebTest1](maintainable-azure-websites-managing-change-and-scale/_static/image83.png "Adding a loop to WebTest1")</span></span>

    <span data-ttu-id="5ddd8-634">*Webtest1.webtest에 루프 추가*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-634">*Adding a loop to WebTest1*</span></span>
6. <span data-ttu-id="5ddd8-635">**루프에 조건부 규칙 및 항목 추가** 대화 상자에서 **for 루프** 규칙을 선택 하 고 다음 속성을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-635">In the **Add Conditional Rule and Items to Loop** dialog box, select the **For Loop** rule and modify the following properties.</span></span>

   1. <span data-ttu-id="5ddd8-636">**종료 값:** 1000</span><span class="sxs-lookup"><span data-stu-id="5ddd8-636">**Terminating value:** 1000</span></span>
   2. <span data-ttu-id="5ddd8-637">**컨텍스트 매개 변수 이름:** 반복</span><span class="sxs-lookup"><span data-stu-id="5ddd8-637">**Context Parameter Name:** Iterator</span></span>
   3. <span data-ttu-id="5ddd8-638">**증가값:** 1</span><span class="sxs-lookup"><span data-stu-id="5ddd8-638">**Increment Value:** 1</span></span>

      <span data-ttu-id="5ddd8-639">![For 루프 규칙을 선택 하 고 속성을 업데이트 합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image84.png "For 루프 규칙을 선택 하 고 속성을 업데이트 합니다.")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-639">![Selecting the For Loop rule and updating the properties](maintainable-azure-websites-managing-change-and-scale/_static/image84.png "Selecting the For Loop rule and updating the properties")</span></span>

      <span data-ttu-id="5ddd8-640">*For 루프 규칙을 선택 하 고 속성을 업데이트 합니다.*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-640">*Selecting the For Loop rule and updating the properties*</span></span>
7. <span data-ttu-id="5ddd8-641">**루프의 항목** 섹션에서 이전에 만든 요청을 루프의 첫 번째 항목과 마지막 항목으로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-641">Under the **Items in loop** section, select the request you created previously to be the first and last item for the loop.</span></span> <span data-ttu-id="5ddd8-642">계속하려면 **확인** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-642">Click **OK** to continue.</span></span>

    <span data-ttu-id="5ddd8-643">![루프의 첫 번째 및 마지막 항목 선택](maintainable-azure-websites-managing-change-and-scale/_static/image85.png "루프의 첫 번째 및 마지막 항목 선택")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-643">![Selecting the first and last items for the loop](maintainable-azure-websites-managing-change-and-scale/_static/image85.png "Selecting the first and last items for the loop")</span></span>

    <span data-ttu-id="5ddd8-644">*루프의 첫 번째 및 마지막 항목 선택*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-644">*Selecting the first and last items for the loop*</span></span>
8. <span data-ttu-id="5ddd8-645">**솔루션 탐색기**에서 **WebAndLoadTestProject** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가** 메뉴를 확장 한 다음 **부하 테스트**...를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-645">In **Solution Explorer**, right-click the **WebAndLoadTestProject** project, expand the **Add** menu and select **Load Test...**.</span></span>

    <span data-ttu-id="5ddd8-646">![WebAndLoadTestProject 프로젝트에 부하 테스트 추가](maintainable-azure-websites-managing-change-and-scale/_static/image86.png "WebAndLoadTestProject 프로젝트에 부하 테스트 추가")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-646">![Adding a Load Test to the WebAndLoadTestProject project](maintainable-azure-websites-managing-change-and-scale/_static/image86.png "Adding a Load Test to the WebAndLoadTestProject project")</span></span>

    <span data-ttu-id="5ddd8-647">*WebAndLoadTestProject 프로젝트에 부하 테스트 추가*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-647">*Adding a Load Test to the WebAndLoadTestProject project*</span></span>
9. <span data-ttu-id="5ddd8-648">**새 부하 테스트 마법사** 대화 상자에서 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-648">In the **New Load Test Wizard** dialog box, click **Next**.</span></span>

    <span data-ttu-id="5ddd8-649">![새 부하 테스트 마법사](maintainable-azure-websites-managing-change-and-scale/_static/image87.png "새 부하 테스트 마법사")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-649">![New Load Test Wizard](maintainable-azure-websites-managing-change-and-scale/_static/image87.png "New Load Test Wizard")</span></span>

    <span data-ttu-id="5ddd8-650">*새 부하 테스트 마법사*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-650">*New Load Test Wizard*</span></span>
10. <span data-ttu-id="5ddd8-651">**시나리오** 페이지에서 **인지 시간 사용 안 함** 을 선택 하 고 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-651">In the **Scenario** page, select **Do not use think times** and click **Next**.</span></span>

    <span data-ttu-id="5ddd8-652">![인지 시간을 사용 하지 않도록 선택](maintainable-azure-websites-managing-change-and-scale/_static/image88.png "인지 시간을 사용 하지 않도록 선택")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-652">![Selecting not to use think times](maintainable-azure-websites-managing-change-and-scale/_static/image88.png "Selecting not to use think times")</span></span>

    <span data-ttu-id="5ddd8-653">*인지 시간을 사용 하지 않도록 선택*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-653">*Selecting not to use think times*</span></span>
11. <span data-ttu-id="5ddd8-654">**부하 패턴** 페이지에서 **상수 로드** 옵션이 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-654">In the **Load Pattern** page, make sure that the **Constant Load** option is selected.</span></span> <span data-ttu-id="5ddd8-655">**사용자 수** 설정을 **250** 사용자로 변경 하 고 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-655">Change the **User Count** setting to **250** users and click **Next**.</span></span>

    <span data-ttu-id="5ddd8-656">![사용자 수를 250으로 변경](maintainable-azure-websites-managing-change-and-scale/_static/image89.png "사용자 수를 250으로 변경")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-656">![Changing the user count to 250](maintainable-azure-websites-managing-change-and-scale/_static/image89.png "Changing the user count to 250")</span></span>

    <span data-ttu-id="5ddd8-657">*사용자 수를 250으로 변경*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-657">*Changing the user count to 250*</span></span>
12. <span data-ttu-id="5ddd8-658">**테스트 조합 모델** 페이지에서 **순차적 테스트 순서를 기준으로** 을 선택 하 고 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-658">In the **Test Mix Model** page, select **Based on sequential test order** and click **Next**.</span></span>

    <span data-ttu-id="5ddd8-659">![테스트 조합 모델 선택](maintainable-azure-websites-managing-change-and-scale/_static/image90.png "테스트 조합 모델 선택")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-659">![Selecting the test mix model](maintainable-azure-websites-managing-change-and-scale/_static/image90.png "Selecting the test mix model")</span></span>

    <span data-ttu-id="5ddd8-660">*테스트 조합 모델 선택*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-660">*Selecting the test mix model*</span></span>
13. <span data-ttu-id="5ddd8-661">**테스트 조합 모델** 페이지에서 **추가 ...** 를 클릭 하 여 테스트를 조합에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-661">In the **Test Mix Model** page, click **Add...** to add a test to the mix.</span></span>

    <span data-ttu-id="5ddd8-662">![테스트 조합에 테스트 추가](maintainable-azure-websites-managing-change-and-scale/_static/image91.png "테스트 조합에 테스트 추가")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-662">![Adding a test to the test mix](maintainable-azure-websites-managing-change-and-scale/_static/image91.png "Adding a test to the test mix")</span></span>

    <span data-ttu-id="5ddd8-663">*테스트 조합에 테스트 추가*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-663">*Adding a test to the test mix*</span></span>
14. <span data-ttu-id="5ddd8-664">**테스트 추가** 대화 상자에서 **webtest1.webtest** 를 두 번 클릭 하 여 **선택한 테스트** 목록에 테스트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-664">In the **Add Tests** dialog box, double-click **WebTest1** to add the test to the **Selected tests** list.</span></span> <span data-ttu-id="5ddd8-665">계속하려면 **확인** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-665">Click **OK** to continue.</span></span>

    <span data-ttu-id="5ddd8-666">![Webtest1.webtest 테스트 추가](maintainable-azure-websites-managing-change-and-scale/_static/image92.png "Webtest1.webtest 테스트 추가")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-666">![Adding the WebTest1 test](maintainable-azure-websites-managing-change-and-scale/_static/image92.png "Adding the WebTest1 test")</span></span>

    <span data-ttu-id="5ddd8-667">*Webtest1.webtest 테스트 추가*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-667">*Adding the WebTest1 test*</span></span>
15. <span data-ttu-id="5ddd8-668">**테스트 조합** 페이지로 돌아가 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-668">Back in the **Test Mix** page, click **Next**.</span></span>

    <span data-ttu-id="5ddd8-669">![테스트 조합 완료 페이지](maintainable-azure-websites-managing-change-and-scale/_static/image93.png "테스트 조합 완료 페이지")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-669">![Completing the Test Mix page](maintainable-azure-websites-managing-change-and-scale/_static/image93.png "Completing the Test Mix page")</span></span>

    <span data-ttu-id="5ddd8-670">*테스트 조합 완료 페이지*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-670">*Completing the Test Mix page*</span></span>
16. <span data-ttu-id="5ddd8-671">**네트워크 조합** 페이지에서 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-671">In the **Network Mix** page, click **Next**.</span></span>

    <span data-ttu-id="5ddd8-672">![네트워크 조합 페이지에서 다음을 클릭 합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image94.png "네트워크 조합 페이지에서 다음을 클릭 합니다.")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-672">![Clicking next in the Network Mix page](maintainable-azure-websites-managing-change-and-scale/_static/image94.png "Clicking next in the Network Mix page")</span></span>

    <span data-ttu-id="5ddd8-673">*네트워크 조합 페이지에서 다음을 클릭 합니다.*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-673">*Clicking next in the Network Mix page*</span></span>
17. <span data-ttu-id="5ddd8-674">**브라우저 조합** 페이지에서 **Internet Explorer 10.0** 을 브라우저 형식으로 선택 하 고 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-674">In the **Browser Mix** page, select **Internet Explorer 10.0** as the browser type and click **Next**.</span></span>

    <span data-ttu-id="5ddd8-675">![브라우저 유형 선택](maintainable-azure-websites-managing-change-and-scale/_static/image95.png "브라우저 유형 선택")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-675">![Selecting the browser type](maintainable-azure-websites-managing-change-and-scale/_static/image95.png "Selecting the browser type")</span></span>

    <span data-ttu-id="5ddd8-676">*브라우저 유형 선택*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-676">*Selecting the browser type*</span></span>
18. <span data-ttu-id="5ddd8-677">**카운터 집합** 페이지에서 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-677">In the **Counter Sets** page, click **Next**.</span></span>

    <span data-ttu-id="5ddd8-678">![카운터 집합 페이지에서 다음을 클릭 합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image96.png "카운터 집합 페이지에서 다음을 클릭 합니다.")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-678">![Clicking Next in the Counter Sets page](maintainable-azure-websites-managing-change-and-scale/_static/image96.png "Clicking Next in the Counter Sets page")</span></span>

    <span data-ttu-id="5ddd8-679">*카운터 집합 페이지에서 다음을 클릭 합니다.*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-679">*Clicking Next in the Counter Sets page*</span></span>
19. <span data-ttu-id="5ddd8-680">**실행 설정** 페이지에서 **부하 테스트 기간** 을 **5 분** 으로 설정 하 고 **마침**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-680">In the **Run Settings** page, set the **Load test duration** to **5 minutes** and click **Finish**.</span></span>

    <span data-ttu-id="5ddd8-681">![부하 테스트 지속 시간을 5 분으로 설정](maintainable-azure-websites-managing-change-and-scale/_static/image97.png "부하 테스트 지속 시간을 5 분으로 설정")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-681">![Setting the load test duration to 5 minutes](maintainable-azure-websites-managing-change-and-scale/_static/image97.png "Setting the load test duration to 5 minutes")</span></span>

    <span data-ttu-id="5ddd8-682">*부하 테스트 지속 시간을 5 분으로 설정*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-682">*Setting the load test duration to 5 minutes*</span></span>
20. <span data-ttu-id="5ddd8-683">**솔루션 탐색기**에서 **로컬. settings** 파일을 두 번 클릭 하 여 테스트 설정을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-683">In **Solution Explorer**, double-click the **Local.settings** file to explore the test settings.</span></span> <span data-ttu-id="5ddd8-684">기본적으로 Visual Studio는 로컬 컴퓨터를 사용 하 여 테스트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-684">By default, Visual Studio uses your local computer to run the tests.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5ddd8-685">또는 **Azure Test Plans**를 사용 하 여 클라우드에서 부하 테스트를 실행 하도록 테스트 프로젝트를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-685">Alternatively, you can configure your test project to run the load tests in the cloud using **Azure Test Plans**.</span></span> <span data-ttu-id="5ddd8-686">Azure Test Plans은 CPU 용량, 사용 가능한 메모리, 네트워크 대역폭 등의 로컬 환경 제약 조건을 방지 하 여 보다 현실적인 부하를 시뮬레이션 하는 클라우드 기반 부하 테스트 서비스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-686">Azure Test Plans provides a cloud-based load testing service that simulates a more realistic load, avoiding local environment constraints like CPU capacity, available memory, and network bandwidth.</span></span> <span data-ttu-id="5ddd8-687">Azure Test Plans를 사용 하 여 부하 테스트를 실행 하는 방법에 대 한 자세한 내용은 [부하 테스트 시나리오](/azure/devops/test/load-test/overview?view=vsts)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-687">For more information about using Azure Test Plans to run load tests, see [Load testing scenarios](/azure/devops/test/load-test/overview?view=vsts).</span></span>

    ![테스트 설정](maintainable-azure-websites-managing-change-and-scale/_static/image98.png)

<a id="Ex5Task3"></a>
#### <a name="task-3--autoscale-verification"></a><span data-ttu-id="5ddd8-689">작업 3 – 자동 크기 조정 확인</span><span class="sxs-lookup"><span data-stu-id="5ddd8-689">Task 3 – Autoscale Verification</span></span>

<span data-ttu-id="5ddd8-690">이제 이전 작업에서 만든 부하 테스트를 실행 하 고 부하 상태에서 웹 앱이 작동 하는 방식을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-690">You will now execute the load test you created in the previous task and see how your web app behaves under load.</span></span>

1. <span data-ttu-id="5ddd8-691">**솔루션 탐색기**에서 **loadtest1.loadtest. loadtest** 를 두 번 클릭 하 여 부하 테스트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-691">In **Solution Explorer**, double-click **LoadTest1.loadtest** to open the load test.</span></span>

    <span data-ttu-id="5ddd8-692">![Loadtest1.loadtest. loadtest를 엽니다.](maintainable-azure-websites-managing-change-and-scale/_static/image99.png "Loadtest1.loadtest. loadtest를 엽니다.")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-692">![Opening LoadTest1.loadtest](maintainable-azure-websites-managing-change-and-scale/_static/image99.png "Opening LoadTest1.loadtest")</span></span>

    <span data-ttu-id="5ddd8-693">*Loadtest1.loadtest. loadtest를 엽니다.*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-693">*Opening LoadTest1.loadtest*</span></span>
2. <span data-ttu-id="5ddd8-694">**Loadtest1.loadtest loadtest** 창에서 도구 상자의 첫 번째 단추를 클릭 하 여 부하 테스트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-694">In the **LoadTest1.loadtest** window, click the first button in the toolbox to run the load test.</span></span>

    <span data-ttu-id="5ddd8-695">![부하 테스트 실행](maintainable-azure-websites-managing-change-and-scale/_static/image100.png "부하 테스트 실행")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-695">![Running the load test](maintainable-azure-websites-managing-change-and-scale/_static/image100.png "Running the load test")</span></span>

    <span data-ttu-id="5ddd8-696">*부하 테스트 실행*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-696">*Running the load test*</span></span>
3. <span data-ttu-id="5ddd8-697">부하 테스트가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-697">Wait until the load test completes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5ddd8-698">부하 테스트는 웹 앱에 요청을 동시에 보내는 여러 사용자를 시뮬레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-698">The load test simulates multiple users that send requests to the web app simultaneously.</span></span> <span data-ttu-id="5ddd8-699">테스트가 실행 중일 때 사용 가능한 카운터를 모니터링 하 여 부하 테스트 실행과 관련 된 오류, 경고 또는 기타 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-699">When the test is running, you can monitor the available counters to detect any errors, warnings or other information related to your load test run.</span></span>

    <span data-ttu-id="5ddd8-700">![부하 테스트 실행 중](maintainable-azure-websites-managing-change-and-scale/_static/image101.png "부하 테스트가 완료 될 때까지 대기")</span><span class="sxs-lookup"><span data-stu-id="5ddd8-700">![Load test running](maintainable-azure-websites-managing-change-and-scale/_static/image101.png "Waiting until the load test completes")</span></span>

    <span data-ttu-id="5ddd8-701">*부하 테스트 실행 중*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-701">*Load test running*</span></span>
4. <span data-ttu-id="5ddd8-702">테스트가 완료 되 면 관리 포털로 돌아가서 웹 앱의 **크기 조정** 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-702">Once the test completes, go back to the management portal and navigate to the **Scale** page of your web app.</span></span> <span data-ttu-id="5ddd8-703">**용량** 섹션 아래에 새 인스턴스가 자동으로 배포 되었음을 나타내는 그래프가 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-703">Under the **capacity** section, you should see in the graph that a new instance was automatically deployed.</span></span>

    ![새 인스턴스가 자동으로 배포 됨](maintainable-azure-websites-managing-change-and-scale/_static/image102.png)

    <span data-ttu-id="5ddd8-705">*새 인스턴스가 자동으로 배포 됨*</span><span class="sxs-lookup"><span data-stu-id="5ddd8-705">*New instance automatically deployed*</span></span>

    > [!NOTE]
    > <span data-ttu-id="5ddd8-706">그래프에 변경 내용이 표시 되는 데 몇 분 정도 걸릴 수 있습니다. **CTRL + f5** 키를 눌러 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-706">It may take several minutes for the changes to appear in the graph (press **CTRL + F5** periodically to refresh the page).</span></span> <span data-ttu-id="5ddd8-707">변경 내용이 표시 되지 않으면 다음을 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-707">If you do not see any changes, you can try the following:</span></span>
    >
    > - <span data-ttu-id="5ddd8-708">부하 테스트 기간 늘리기 (예: **10 분**)</span><span class="sxs-lookup"><span data-stu-id="5ddd8-708">Increase the duration of the load test (e.g. to **10 minutes**)</span></span>
    > - <span data-ttu-id="5ddd8-709">웹 앱의 자동 크기 조정 구성에서 **대상 CPU** 범위의 최대값과 최 댓 값을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-709">Reduce the maximum and minimum values of the **Target CPU** range in the Autoscale configuration of your web app</span></span>
    > - <span data-ttu-id="5ddd8-710">**Azure Test Plans**를 사용 하 여 클라우드에서 부하 테스트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-710">Run the load test in the cloud with **Azure Test Plans**.</span></span> <span data-ttu-id="5ddd8-711">자세한 내용은 [여기](/azure/devops/test/load-test/index?view=vsts)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-711">More information [here](/azure/devops/test/load-test/index?view=vsts)</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="5ddd8-712">요약</span><span class="sxs-lookup"><span data-stu-id="5ddd8-712">Summary</span></span>

<span data-ttu-id="5ddd8-713">이 실습 랩에서는 Azure에서 프로덕션 웹 앱에 응용 프로그램을 설치 하 고 배포 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-713">In this hands-on lab, you learned how to set up and deploy your application to production web apps in Azure.</span></span> <span data-ttu-id="5ddd8-714">먼저 **Entity Framework Code First 마이그레이션**를 사용 하 여 데이터베이스를 검색 하 고 업데이트 한 다음 **Git** 를 사용 하 여 사이트의 새 버전을 배포 하 고 안정적인 최신 버전의 사이트로 롤백을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-714">You started by detecting and updating your databases using **Entity Framework Code First Migrations**, then continued by deploying new versions of your site using **Git** and performing rollbacks to the latest stable version of your site.</span></span> <span data-ttu-id="5ddd8-715">또한 저장소를 사용 하 여 앱을 확장 하 여 정적 콘텐츠를 Blob 컨테이너로 이동 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="5ddd8-715">Additionally, you learned how to scale your app using Storage to move your static content to a Blob container.</span></span>
