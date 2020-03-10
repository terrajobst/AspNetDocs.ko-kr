---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
title: Azure를 사용 하 여 실제 클라우드 앱 빌드 | Microsoft Docs
author: MikeWasson
description: 이 문서에서는 실제 클라우드 솔루션을 빌드하는 패턴 기반 접근 방식을 안내 합니다. 패턴은 개발 프로세스 뿐만 아니라 ...에도 적용 됩니다.
ms.author: riande
ms.date: 06/12/2014
ms.assetid: accfa16a-ab15-4c26-9ad4-babdc2a77d2e
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
msc.type: authoredcontent
ms.openlocfilehash: b88573b3702b755b155e8da35f5f8a67931bafc6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500651"
---
# <a name="building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="6174c-104">Azure를 사용 하 여 실제 클라우드 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="6174c-104">Building Real-World Cloud Apps with Azure</span></span>

<span data-ttu-id="6174c-105">사람, [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="6174c-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="6174c-106">[Fix It 프로젝트 다운로드](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자 서적 다운로드](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="6174c-106">[Download Fix It Project](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="6174c-107">이 문서에서는 실제 클라우드 솔루션을 빌드하는 패턴 기반 접근 방식을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-107">This e-book walks you through a patterns-based approach to building real-world cloud solutions.</span></span> <span data-ttu-id="6174c-108">패턴은 아키텍처 및 코딩 방식 뿐만 아니라 개발 프로세스에도 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-108">The patterns apply to the development process as well as to architecture and coding practices.</span></span>
> 
> <span data-ttu-id="6174c-109">콘텐츠는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 하며 2013, 2013 년 6 월 ([1](http://vimeo.com/68215538)부, [2 부](http://vimeo.com/68215602))의 Microsoft Tech Ed 오스트레일리아 ([1](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR324)부, [2](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR325)부)에서 Scott이 개발한 프레젠테이션을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-109">The content is based on a presentation developed by Scott Guthrie and delivered by him at the Norwegian Developers Conference (NDC) in June of 2013 ([part 1](http://vimeo.com/68215538), [part 2](http://vimeo.com/68215602)), and at Microsoft Tech Ed Australia in September, 2013 ([part 1](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR324), [part 2](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR325)).</span></span> <span data-ttu-id="6174c-110">비디오에서 필기 형식으로 전환 하는 동안 [다른 많은 사람들이](more-patterns-and-guidance.md#acknowledgments) 콘텐츠를 업데이트 하 고 보강 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-110">[Many others](more-patterns-and-guidance.md#acknowledgments) updated and augmented the content while transitioning it from video to written form.</span></span>

## <a name="intended-audience"></a><span data-ttu-id="6174c-111">대상 그룹</span><span class="sxs-lookup"><span data-stu-id="6174c-111">Intended Audience</span></span>

<span data-ttu-id="6174c-112">클라우드를 위한 개발, 클라우드로의 이동, 클라우드 개발에 대해 관심이 있는 개발자는 여기에서 알아야 하는 가장 중요 한 개념과 방법에 대 한 간결한 개요를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-112">Developers who are curious about developing for the cloud, considering a move to the cloud, or are new to cloud development will find here a concise overview of the most important concepts and practices they need to know.</span></span> <span data-ttu-id="6174c-113">개념은 구체적인 예제와 함께 설명 되어 있으며, 각 챕터는 다른 리소스에 연결 되어 자세한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-113">The concepts are illustrated with concrete examples, and each chapter links to other resources for more in-depth information.</span></span> <span data-ttu-id="6174c-114">Microsoft 프레임 워크 및 서비스에 대 한 추가 리소스의 예제와 링크는 다른 웹 개발 프레임 워크 및 클라우드 환경에도 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-114">The examples and the links to additional resources are for Microsoft frameworks and services, but the principles illustrated apply to other web development frameworks and cloud environments as well.</span></span>

<span data-ttu-id="6174c-115">이미 클라우드 용으로 개발 하 고 있는 개발자는이에 대 한 아이디어를 파악 하 여 더 성공적으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-115">Developers who are already developing for the cloud may find ideas here that will help make them more successful.</span></span> <span data-ttu-id="6174c-116">계열의 각 챕터를 독립적으로 읽을 수 있으므로 관심 있는 항목을 선택 하 고 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-116">Each chapter in the series can be read independently, so you can pick and choose topics that you're interested in.</span></span>

<span data-ttu-id="6174c-117">Scott Guthrie에서 *Azure 프레젠테이션을 사용 하 여 실제 클라우드 앱을 개발* 하 고 자세한 정보 및 업데이트 정보를 원하는 모든 사용자에 게 여기에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-117">Anyone who watched Scott Guthrie's *Building Real World Cloud Apps with Azure* presentation and wants more details and updated information will find that here.</span></span>

<a id="patterns"></a>
## <a name="cloud-development-patterns"></a><span data-ttu-id="6174c-118">클라우드 개발 패턴</span><span class="sxs-lookup"><span data-stu-id="6174c-118">Cloud development patterns</span></span>

<span data-ttu-id="6174c-119">이 전자 서적에서는 클라우드 개발을 위한 13 권장 패턴을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-119">This e-book explains thirteen recommended patterns for cloud development.</span></span> <span data-ttu-id="6174c-120">"Pattern"은 이러한 작업을 수행 하는 데 권장 되는 방법 (클라우드 앱 개발, 디자인 및 코딩에 대 한 최상의 방법)을 의미 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-120">"Pattern" is used here in a broad sense to mean a recommended way to do things: how best to go about developing, designing, and coding cloud apps.</span></span> <span data-ttu-id="6174c-121">이러한 패턴은 뒤에 오는 경우 "성공의 pit를 포함" 하는 데 도움이 되는 주요 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-121">These are key patterns which will help you "fall into the pit of success" if you follow them.</span></span>

- <span data-ttu-id="6174c-122">[모든](automate-everything.md)기능을 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-122">[Automate everything](automate-everything.md).</span></span>

    - <span data-ttu-id="6174c-123">스크립트를 사용 하 여 반복 되는 프로세스에서 효율성을 최대화 하 고 오류를 최소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-123">Use scripts to maximize efficiency and minimize errors in repetitive processes.</span></span>
    - <span data-ttu-id="6174c-124">데모: Azure 관리 스크립트</span><span class="sxs-lookup"><span data-stu-id="6174c-124">Demo: Azure management scripts.</span></span>
- <span data-ttu-id="6174c-125">[소스 제어](source-control.md).</span><span class="sxs-lookup"><span data-stu-id="6174c-125">[Source control](source-control.md).</span></span> 

    - <span data-ttu-id="6174c-126">DevOps 워크플로를 용이 하 게 하기 위해 소스 제어에서 분기 구조를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-126">Set up branching structure in source control to facilitate DevOps workflow.</span></span>
    - <span data-ttu-id="6174c-127">Demo: 소스 제어에 스크립트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-127">Demo: add scripts to source control.</span></span>
    - <span data-ttu-id="6174c-128">데모: 중요 한 데이터를 소스 제어에서 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-128">Demo: keep sensitive data out of source control.</span></span>
    - <span data-ttu-id="6174c-129">데모: Visual Studio에서 Git를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-129">Demo: use Git in Visual Studio.</span></span>
- <span data-ttu-id="6174c-130">[지속적인 통합 및 제공](continuous-integration-and-continuous-delivery.md)</span><span class="sxs-lookup"><span data-stu-id="6174c-130">[Continuous integration and delivery](continuous-integration-and-continuous-delivery.md).</span></span> 

    - <span data-ttu-id="6174c-131">각 소스 제어 체크 인을 사용 하 여 빌드 및 배포를 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-131">Automate build and deployment with each source control check-in.</span></span>
- <span data-ttu-id="6174c-132">[웹 개발 모범 사례](web-development-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="6174c-132">[Web development best practices](web-development-best-practices.md).</span></span> 

    - <span data-ttu-id="6174c-133">웹 계층 상태 비저장 유지.</span><span class="sxs-lookup"><span data-stu-id="6174c-133">Keep web tier stateless.</span></span>
    - <span data-ttu-id="6174c-134">데모: Azure App Service의 Web Apps 크기 조정 및 자동 크기 조정</span><span class="sxs-lookup"><span data-stu-id="6174c-134">Demo: scaling and auto-scaling in Web Apps in Azure App Service.</span></span>
    - <span data-ttu-id="6174c-135">세션 상태를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-135">Avoid session state.</span></span>
    - <span data-ttu-id="6174c-136">CDN을 사용할 수 없는 경우 대체 (fallback)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-136">Use a CDN with a fallback when the CDN is unavailable.</span></span>
    - <span data-ttu-id="6174c-137">비동기 프로그래밍 모델을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-137">Use asynchronous programming model.</span></span>
    - <span data-ttu-id="6174c-138">Demo: ASP.NET MVC 및 Entity Framework의 async</span><span class="sxs-lookup"><span data-stu-id="6174c-138">Demo: async in ASP.NET MVC and Entity Framework.</span></span>
- <span data-ttu-id="6174c-139">[Single sign-on](single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="6174c-139">[Single sign-on](single-sign-on.md).</span></span> 

    - <span data-ttu-id="6174c-140">Azure Active Directory 소개.</span><span class="sxs-lookup"><span data-stu-id="6174c-140">Introduction to Azure Active Directory.</span></span>
    - <span data-ttu-id="6174c-141">데모: Azure Active Directory을 사용 하는 ASP.NET 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-141">Demo: create an ASP.NET app that uses Azure Active Directory.</span></span>
- <span data-ttu-id="6174c-142">[데이터 저장소 옵션](data-storage-options.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-142">[Data storage options](data-storage-options.md).</span></span> 

    - <span data-ttu-id="6174c-143">데이터 저장소의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-143">Types of data stores.</span></span>
    - <span data-ttu-id="6174c-144">올바른 데이터 저장소를 선택 하는 방법</span><span class="sxs-lookup"><span data-stu-id="6174c-144">How to choose the right data store.</span></span>
    - <span data-ttu-id="6174c-145">데모: Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="6174c-145">Demo: Azure SQL Database.</span></span>
- <span data-ttu-id="6174c-146">[데이터 분할 전략](data-partitioning-strategies.md).</span><span class="sxs-lookup"><span data-stu-id="6174c-146">[Data partitioning strategies](data-partitioning-strategies.md).</span></span> 

    - <span data-ttu-id="6174c-147">관계형 데이터베이스의 크기를 쉽게 조정할 수 있도록 데이터를 가로 또는 세로로 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-147">Partition data vertically, horizontally, or both to facilitate scaling a relational database.</span></span>
- <span data-ttu-id="6174c-148">[비구조적 blob 저장소](unstructured-blob-storage.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-148">[Unstructured blob storage](unstructured-blob-storage.md).</span></span> 

    - <span data-ttu-id="6174c-149">Blob service를 사용 하 여 클라우드에 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-149">Store files in the cloud by using the blob service.</span></span>
    - <span data-ttu-id="6174c-150">데모: Fix It 앱에서 blob 저장소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-150">Demo: using blob storage in the Fix It app.</span></span>
- <span data-ttu-id="6174c-151">[오류가 계속 발생 하도록 디자인](design-to-survive-failures.md)</span><span class="sxs-lookup"><span data-stu-id="6174c-151">[Design to survive failures](design-to-survive-failures.md).</span></span> 

    - <span data-ttu-id="6174c-152">오류 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-152">Types of failures.</span></span>
    - <span data-ttu-id="6174c-153">실패 범위.</span><span class="sxs-lookup"><span data-stu-id="6174c-153">Failure Scope.</span></span>
    - <span data-ttu-id="6174c-154">Sla 이해.</span><span class="sxs-lookup"><span data-stu-id="6174c-154">Understanding SLAs.</span></span>
- <span data-ttu-id="6174c-155">[모니터링 및 원격 분석](monitoring-and-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="6174c-155">[Monitoring and telemetry](monitoring-and-telemetry.md).</span></span> 

    - <span data-ttu-id="6174c-156">원격 분석 앱을 구입 하 고 앱을 계측 하는 사용자 고유의 코드를 작성 해야 하는 이유입니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-156">Why you should both buy a telemetry app and write your own code to instrument your app.</span></span>
    - <span data-ttu-id="6174c-157">데모: Azure에 대 한 새 유물</span><span class="sxs-lookup"><span data-stu-id="6174c-157">Demo: New Relic for Azure</span></span>
    - <span data-ttu-id="6174c-158">데모: Fix It 앱에서 코드를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-158">Demo: logging code in the Fix It app.</span></span>
    - <span data-ttu-id="6174c-159">데모: Fix It 앱에서 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="6174c-159">Demo: dependency injection in the Fix It app.</span></span>
    - <span data-ttu-id="6174c-160">데모: Azure에서 기본 제공 되는 로깅 지원.</span><span class="sxs-lookup"><span data-stu-id="6174c-160">Demo: built-in logging support in Azure.</span></span>
- <span data-ttu-id="6174c-161">[일시적인 오류 처리](transient-fault-handling.md)</span><span class="sxs-lookup"><span data-stu-id="6174c-161">[Transient fault handling](transient-fault-handling.md).</span></span> 

    - <span data-ttu-id="6174c-162">일시적 오류의 영향을 완화 하기 위해 스마트 재시도/백오프 논리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-162">Use smart retry/back-off logic to mitigate the effect of transient failures.</span></span>
    - <span data-ttu-id="6174c-163">데모: Entity Framework 6에서 다시 시도/백오프</span><span class="sxs-lookup"><span data-stu-id="6174c-163">Demo: retry/back-off in Entity Framework 6.</span></span>
- <span data-ttu-id="6174c-164">[분산 캐싱](distributed-caching.md).</span><span class="sxs-lookup"><span data-stu-id="6174c-164">[Distributed caching](distributed-caching.md).</span></span> 

    - <span data-ttu-id="6174c-165">분산 캐싱을 사용 하 여 확장성을 높이고 데이터베이스 트랜잭션 비용을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-165">Improve scalability and reduce database transaction costs by using distributed caching.</span></span>
- <span data-ttu-id="6174c-166">[큐 중심 작업 패턴](queue-centric-work-pattern.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-166">[Queue-centric work pattern](queue-centric-work-pattern.md).</span></span> 

    - <span data-ttu-id="6174c-167">웹 및 작업자 계층을 느슨하게 결합 하 여 고가용성을 지원 하 고 확장성을 향상할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-167">Enable high availability and improve scalability by loosely coupling web and worker tiers.</span></span>
    - <span data-ttu-id="6174c-168">데모: Fix It 앱의 Azure storage 큐</span><span class="sxs-lookup"><span data-stu-id="6174c-168">Demo: Azure storage queues in the Fix It app.</span></span>
- <span data-ttu-id="6174c-169">[더 많은 클라우드 앱 패턴 및 지침](more-patterns-and-guidance.md)</span><span class="sxs-lookup"><span data-stu-id="6174c-169">[More cloud app patterns and guidance](more-patterns-and-guidance.md).</span></span>
- [<span data-ttu-id="6174c-170">부록: Fix It 애플리케이션 예제</span><span class="sxs-lookup"><span data-stu-id="6174c-170">Appendix: The Fix It Sample Application</span></span>](the-fix-it-sample-application.md)

    - <span data-ttu-id="6174c-171">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="6174c-171">Known Issues</span></span>
    - <span data-ttu-id="6174c-172">모범 사례</span><span class="sxs-lookup"><span data-stu-id="6174c-172">Best Practices</span></span>
    - <span data-ttu-id="6174c-173">다운로드, 빌드, 실행 및 배포 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-173">How to download, build, run, and deploy.</span></span>

<span data-ttu-id="6174c-174">이러한 패턴은 모든 클라우드 환경에 적용 되지만 Microsoft 기술 및 서비스 (예: Visual Studio, Team Foundation Service, ASP.NET, Azure)를 기반으로 하는 예제를 사용 하 여 설명 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-174">These patterns apply to all cloud environments, but we'll illustrate them by using examples based on Microsoft technologies and services, such as Visual Studio, Team Foundation Service, ASP.NET, and Azure.</span></span>

<span data-ttu-id="6174c-175">이 장의 나머지 부분에서는 fix it 샘플 응용 프로그램 및 Fix It 앱이 실행 되는 Azure App Service 클라우드 환경의 Web Apps를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-175">This remainder of this chapter introduces the Fix It sample application and the Web Apps in Azure App Service cloud environment that the Fix It app runs in.</span></span>

<a id="fixit"></a>
## <a name="the-fix-it-sample-application"></a><span data-ttu-id="6174c-176">Fix it 샘플 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="6174c-176">The Fix it sample application</span></span>

<span data-ttu-id="6174c-177">이 설명서에 표시 되는 대부분의 스크린 샷 및 코드 예제는 권장 되는 클라우드 앱 개발 패턴 및 사례를 보여 주기 위해 [Scott Guthrie](https://weblogs.asp.net/scottgu/) 에서 원래 개발한 Fix It 앱을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-177">Most of the screen shots and code examples shown in this e-book are based on the Fix It app originally developed by [Scott Guthrie](https://weblogs.asp.net/scottgu/) to demonstrate recommended cloud app development patterns and practices.</span></span>

![It 앱 홈 페이지 수정](introduction/_static/image1.png)

<span data-ttu-id="6174c-179">샘플 앱은 간단한 작업 항목 티켓 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-179">The sample app is a simple work item ticketing system.</span></span> <span data-ttu-id="6174c-180">수정 된 항목이 필요한 경우 티켓을 만들어 다른 사람에 게 할당 하 고, 다른 사용자는 로그인 하 여 자신에 게 할당 된 티켓을 확인 하 고 작업이 완료 되 면 티켓을 완료로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-180">When you need something fixed, you create a ticket and assign it to someone, and others can log in and see the tickets assigned to them and mark tickets as completed when the work is done.</span></span>

<span data-ttu-id="6174c-181">표준 Visual Studio 웹 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-181">It's a standard Visual Studio web project.</span></span> <span data-ttu-id="6174c-182">ASP.NET MVC를 기반으로 하며 SQL Server 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-182">It is built on ASP.NET MVC and uses a SQL Server database.</span></span> <span data-ttu-id="6174c-183">IIS Express에서 로컬로 실행할 수 있으며 클라우드에서 실행할 수 있도록 Azure 웹 사이트에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-183">It can run locally in IIS Express and can be deployed to a Azure Web Site to run in the cloud.</span></span> <span data-ttu-id="6174c-184">양식 인증 및 로컬 데이터베이스를 사용 하거나 Google과 같은 소셜 공급자를 사용 하 여 로그인 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-184">You can log in using forms authentication and a local database or by using a social provider such as Google.</span></span> <span data-ttu-id="6174c-185">(나중에 Active Directory 조직 계정으로 로그인 하는 방법도 보여 드리겠습니다.)</span><span class="sxs-lookup"><span data-stu-id="6174c-185">(Later we'll also show how to log in with an Active Directory organizational account.)</span></span>

![로그인 페이지](introduction/_static/image2.png)

<span data-ttu-id="6174c-187">로그인 한 후에는 티켓을 만들고, 사용자에 게 할당 하 고, 수정 하려는 항목의 그림을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-187">Once you're logged in you can create a ticket, assign it to someone, and upload a picture of what you want to get fixed.</span></span>

![Fix It 작업 만들기](introduction/_static/image3.png)

![만든 It 작업 수정](introduction/_static/image4.png)

<span data-ttu-id="6174c-190">사용자가 만든 작업 항목의 진행률을 추적 하 고, 자신에 게 할당 된 티켓을 확인 하 고, 티켓 세부 정보를 보고, 항목을 완료로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-190">You can track the progress of work items you created, see tickets assigned to you, view ticket details, and mark items as completed.</span></span>

<span data-ttu-id="6174c-191">이 앱은 기능 관점에서 매우 간단한 앱 이지만 수백만 명의 사용자로 확장할 수 있고 데이터베이스 오류 및 연결 종료와 같은 작업에 탄력적으로 대처할 수 있도록 빌드하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-191">This is a very simple app from a feature perspective, but you'll see how to build it so that it can scale to millions of users and will be resilient to things like database failures and connection terminations.</span></span> <span data-ttu-id="6174c-192">또한 간단 하 고 신속 하 게 개발 주기를 반복 하 여 간단 하 게 시작 하 고 앱을 더 효과적이 고 효율적으로 만들 수 있는 자동화 된 agile 개발 워크플로를 만드는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-192">You'll also see how to create an automated and agile development workflow, which enables you to start simple and make the app better and better by iterating the development cycle efficiently and quickly.</span></span>

<a id="waws"></a>
## <a name="web-apps-in-azure-app-service"></a><span data-ttu-id="6174c-193">Azure App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="6174c-193">Web Apps in Azure App Service</span></span>

<span data-ttu-id="6174c-194">Fix It 응용 프로그램에 사용 되는 클라우드 환경은 웹 사이트를 호출 하는 Azure의 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-194">The cloud environment used for the Fix It application is a service of Azure that we call Web Sites.</span></span> <span data-ttu-id="6174c-195">이 서비스는 Vm을 만들고, 업데이트를 유지 하 고, IIS를 설치 및 구성 하지 않고도 Azure에서 사용자 고유의 웹 앱을 호스트할 수 있는 방법입니다. Microsoft는 Vm에서 사이트를 호스팅하고 자동으로 백업 및 복구 및 기타 서비스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-195">This service is a way that you can host your own web app in Azure without having to create VMs and keep them updated, install and configure IIS, etc. We host your site on our VMs and automatically provide backup and recovery and other services for you.</span></span> <span data-ttu-id="6174c-196">웹 사이트 서비스는 ASP.NET, node.js, PHP 및 Python과 함께 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-196">The Web Sites service works with ASP.NET, Node.js, PHP, and Python.</span></span> <span data-ttu-id="6174c-197">Visual Studio, 웹 배포, FTP, Git 또는 TFS를 사용 하 여 매우 빠르게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-197">It enables you to deploy very quickly using Visual Studio, Web Deploy, FTP, Git, or TFS.</span></span> <span data-ttu-id="6174c-198">배포를 시작 하는 시간과 인터넷을 통해 업데이트를 사용할 수 있는 시간 사이에는 일반적으로 몇 초 밖에 안 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-198">It's usually just a few seconds between the time you start a deployment and the time your update is available over the Internet.</span></span> <span data-ttu-id="6174c-199">모든 작업을 무료로 시작할 수 있으며 트래픽이 증가 함에 따라 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-199">It's all free to get started, and you can scale up as your traffic grows.</span></span>

<span data-ttu-id="6174c-200">백그라운드에서 Azure App Service의 Web Apps는 사용자 고유의 Vm에서 IIS를 사용 하 여 웹 사이트를 호스트 하려는 경우 사용자가 직접 작성 해야 하는 다양 한 아키텍처 구성 요소 및 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-200">Behind the scenes, Web Apps in Azure App Service provides a lot of architectural components and features that you'd have to build yourself if you were going to host a web site using IIS on your own VMs.</span></span> <span data-ttu-id="6174c-201">한 구성 요소는 자동으로 IIS를 구성 하 고 응용 프로그램을 실행 하려는 Vm의 수에 따라 응용 프로그램을 설치 하는 배포 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-201">One component is a deployment end point that automatically configures IIS and installs your application on as many VMs as you want to run your site on.</span></span>

![배포 서비스](introduction/_static/image5.png)

<span data-ttu-id="6174c-203">사용자가 웹 사이트에 도달 하면 IIS Vm에 직접 도달 하지 않고 [ARR (응용 프로그램 요청 라우팅](https://www.iis.net/downloads/microsoft/application-request-routing) ) 부하 분산 장치를 통해 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-203">When a user hits the web site, they don't hit the IIS VMs directly, they go through [Application Request Routing (ARR)](https://www.iis.net/downloads/microsoft/application-request-routing) load balancers.</span></span> <span data-ttu-id="6174c-204">사용자의 서버에서 이러한 기능을 사용할 수 있지만, 여기서의 장점은 자동으로 설정 된다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-204">You can use these with your own servers, but the advantage here is that they're set up for you automatically.</span></span> <span data-ttu-id="6174c-205">세션 선호도, IIS의 큐 크기 및 각 컴퓨터의 CPU 사용과 같은 고려 사항을 고려 하는 스마트 추론을 사용 하 여 웹 사이트를 호스트 하는 Vm으로 트래픽을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-205">They use a smart heuristic that takes into account factors such as session affinity, queue depth in IIS, and CPU usage on each machine to direct traffic to the VMs that host your web site.</span></span>

![ARR 부하 분산 장치](introduction/_static/image6.png)

<span data-ttu-id="6174c-207">컴퓨터가 중단 되 면 Azure에서 자동으로이를 순환에서 가져오고, 새 VM 인스턴스를 회전 하 고, 새 인스턴스로 트래픽을 전송 하기 시작 합니다. 즉, 응용 프로그램에 대해 중단 시간을 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-207">If a machine goes down, Azure automatically pulls it from the rotation, spins up a new VM instance, and starts directing traffic to the new instance -- all with no down time for your application.</span></span>

![컴퓨터의 자동 복구 오류](introduction/_static/image7.png)

<span data-ttu-id="6174c-209">이 모든 작업은 자동으로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-209">All of this takes place automatically.</span></span> <span data-ttu-id="6174c-210">Windows PowerShell, Visual Studio 또는 Azure 관리 포털을 사용 하 여 웹 사이트를 만들고 응용 프로그램을 배포 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-210">All you need to do is create a web site and deploy your application to it, using Windows PowerShell, Visual Studio, or the Azure management portal.</span></span>

<span data-ttu-id="6174c-211">Visual Studio에서 웹 응용 프로그램을 만들고 Azure 웹 사이트에 배포 하는 방법을 보여 주는 빠르고 쉬운 단계별 자습서는 [azure 및 ASP.NET 시작](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="6174c-211">For a quick and easy step-by-step tutorial that shows how to create a web application in Visual Studio and deploy it to a Azure Web Site, see [Get started with Azure and ASP.NET](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span>

<a id="summary"></a>
## <a name="summary"></a><span data-ttu-id="6174c-212">요약</span><span class="sxs-lookup"><span data-stu-id="6174c-212">Summary</span></span>

<span data-ttu-id="6174c-213">이 소개에서는 책에서 다루는 항목의 목록, 샘플 응용 프로그램의 스크린샷 및 Azure App Service 클라우드 환경의 Web Apps에 대 한 간략 한 개요를 제공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-213">This introduction has provided a list of topics the book will cover, screenshots of the sample application, and a brief overview of the Web Apps in Azure App Service cloud environment.</span></span> <span data-ttu-id="6174c-214">및 클라우드에서 앱을 개발할 때의 뛰어난 이점 중 하나는 테스트 환경 만들기 및 코드 배포와 같은 반복적인 개발 작업을 쉽게 자동화할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-214">One of the great advantages of developing apps in and for the cloud is that it's easy to automate repetitive development tasks such as creating a test environment and deploying your code to it.</span></span> <span data-ttu-id="6174c-215">이 작업을 수행 하는 방법은 [다음 장의](automate-everything.md)주제입니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-215">How to do that is the subject of the [next chapter](automate-everything.md).</span></span>

## <a name="resources"></a><span data-ttu-id="6174c-216">리소스</span><span class="sxs-lookup"><span data-stu-id="6174c-216">Resources</span></span>

<span data-ttu-id="6174c-217">이 장에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="6174c-217">For more information about the topics covered in this chapter, see the following resources.</span></span>

<span data-ttu-id="6174c-218">설명서:</span><span class="sxs-lookup"><span data-stu-id="6174c-218">Documentation:</span></span>

- <span data-ttu-id="6174c-219">[Azure App Service에서 Web Apps](https://azure.microsoft.com/services/app-service/web/)합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-219">[Web Apps in Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="6174c-220">Web Apps에 대 한 Azure 설명서 포털 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-220">Portal page for Azure documentation about Web Apps.</span></span>
- [<span data-ttu-id="6174c-221">Web Apps, Cloud Services 및 Vm: 사용 시기</span><span class="sxs-lookup"><span data-stu-id="6174c-221">Web Apps, Cloud Services, and VMs: When to use which?</span></span>](https://azure.microsoft.com/documentation/articles/choose-web-site-cloud-service-vm/) <span data-ttu-id="6174c-222">이 장에 표시 된 것 처럼 WAWS는 Azure에서 웹 앱을 실행할 수 있는 세 가지 방법 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-222">WAWS as shown in this chapter is just one of three ways you can run web apps in Azure.</span></span> <span data-ttu-id="6174c-223">이 문서에서는 세 가지 방법의 차이점에 대해 설명 하 고 시나리오에 적합 한 항목을 선택 하는 방법에 대 한 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-223">This article explains the differences between the three ways and gives guidance on how to choose which one is right for your scenario.</span></span> <span data-ttu-id="6174c-224">웹 사이트와 마찬가지로 Cloud Services는 Azure의 PaaS 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-224">Like Web Sites, Cloud Services is a PaaS feature of Azure.</span></span> <span data-ttu-id="6174c-225">Vm은 IaaS 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-225">VMs are an IaaS feature.</span></span> <span data-ttu-id="6174c-226">PaaS 및 IaaS에 대 한 설명은 [데이터 옵션](data-storage-options.md#paasiaas) 챕터를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="6174c-226">For an explanation of PaaS versus IaaS, see the [Data Options](data-storage-options.md#paasiaas) chapter.</span></span>

<span data-ttu-id="6174c-227">비디오:</span><span class="sxs-lookup"><span data-stu-id="6174c-227">Videos:</span></span>

- [<span data-ttu-id="6174c-228">Scott Guthrie는 0 단계에서 시작 됩니다. Azure 클라우드 OS 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="6174c-228">Scott Guthrie starts at Step 0 - What is the Azure Cloud OS?</span></span>](https://azure.microsoft.com/documentation/videos/what-is-the-cloud-os-scottgu/)
- <span data-ttu-id="6174c-229">[웹 사이트 아키텍처-Stefan Schackow를 사용](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)합니다.</span><span class="sxs-lookup"><span data-stu-id="6174c-229">[Web Sites Architecture - with Stefan Schackow](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/).</span></span>
- <span data-ttu-id="6174c-230">[Nir Mashkowski를 사용 하는 Azure 웹 사이트의 내부](https://channel9.msdn.com/Shows/Web+Camps+TV/Windows-Azure-Web-Sites-Internals-with-Nir-Mashkowski).</span><span class="sxs-lookup"><span data-stu-id="6174c-230">[Azure Web Sites Internals with Nir Mashkowski](https://channel9.msdn.com/Shows/Web+Camps+TV/Windows-Azure-Web-Sites-Internals-with-Nir-Mashkowski).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="6174c-231">다음</span><span class="sxs-lookup"><span data-stu-id="6174c-231">Next</span></span>](automate-everything.md)
