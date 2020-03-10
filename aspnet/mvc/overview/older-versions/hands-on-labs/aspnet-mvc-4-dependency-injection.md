---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
title: ASP.NET MVC 4 종속성 주입 | Microsoft Docs
author: rick-anderson
description: 참고:이 실습 랩에서는 ASP.NET MVC 및 ASP.NET MVC 4 필터에 대 한 기본 지식이 있다고 가정 합니다. 이전에 ASP.NET MVC 4 필터를 사용 하지 않은 경우
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 84c7baca-1c54-4c44-8f52-4282122d6acb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 15c9d4dcb9e2c6b9f6adf54d65d15737b32cca3b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451823"
---
# <a name="aspnet-mvc-4-dependency-injection"></a><span data-ttu-id="22165-104">ASP.NET MVC 4 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="22165-104">ASP.NET MVC 4 Dependency Injection</span></span>

<span data-ttu-id="22165-105">[웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="22165-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="22165-106">웹 캠프 교육 키트 다운로드</span><span class="sxs-lookup"><span data-stu-id="22165-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="22165-107">이 실습 랩에서는 **ASP.NET mvc** 및 **ASP.NET mvc 4 필터**에 대 한 기본 지식이 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-107">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC** and **ASP.NET MVC 4 filters**.</span></span> <span data-ttu-id="22165-108">이전에 **ASP.NET mvc 4 필터** 를 사용 하지 않은 경우에는 **ASP.NET Mvc 사용자 지정 작업 필터** 실습 실습을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-108">If you have not used **ASP.NET MVC 4 filters** before, we recommend you to go over **ASP.NET MVC Custom Action Filters** Hands-on Lab.</span></span>

> [!NOTE]
> <span data-ttu-id="22165-109">모든 샘플 코드와 코드 조각은 [Microsoft 웹/WebCampTrainingKit 릴리스에서](https://aka.ms/webcamps-training-kit)제공 되는 웹 캠프 교육 키트에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-109">All sample code and snippets are included in the Web Camps Training Kit, available from at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="22165-110">이 랩에서 관련 된 프로젝트는 [ASP.NET MVC 4 종속성 주입](https://github.com/Microsoft-Web/HOL-MVC4DependencyInjection)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-110">The project specific to this lab is available at [ASP.NET MVC 4 Dependency Injection](https://github.com/Microsoft-Web/HOL-MVC4DependencyInjection).</span></span>

<span data-ttu-id="22165-111">**개체 지향 프로그래밍** 패러다임에서 개체는 기여자와 소비자가 있는 공동 작업 모델에서 함께 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-111">In **Object Oriented Programming** paradigm, objects work together in a collaboration model where there are contributors and consumers.</span></span> <span data-ttu-id="22165-112">기본적으로이 통신 모델은 개체와 구성 요소 간의 종속성을 생성 하므로 복잡성이 증가 하면 관리가 어려워집니다.</span><span class="sxs-lookup"><span data-stu-id="22165-112">Naturally, this communication model generates dependencies between objects and components, becoming difficult to manage when complexity increases.</span></span>

<span data-ttu-id="22165-113">![클래스 종속성 및 모델 복잡성](aspnet-mvc-4-dependency-injection/_static/image1.png "클래스 종속성 및 모델 복잡성")</span><span class="sxs-lookup"><span data-stu-id="22165-113">![Class dependencies and model complexity](aspnet-mvc-4-dependency-injection/_static/image1.png "Class dependencies and model complexity")</span></span>

<span data-ttu-id="22165-114">*클래스 종속성 및 모델 복잡성*</span><span class="sxs-lookup"><span data-stu-id="22165-114">*Class dependencies and model complexity*</span></span>

<span data-ttu-id="22165-115">클라이언트 개체가 서비스 위치를 주로 담당 하는 서비스를 사용 하 여 **팩터리 패턴** 및 인터페이스와 구현 간의 분리에 대해 들었습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-115">You have probably heard about the **Factory Pattern** and the separation between the interface and the implementation using services, where the client objects are often responsible for service location.</span></span>

<span data-ttu-id="22165-116">종속성 주입 패턴은 제어 반전의 특정 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="22165-116">The Dependency Injection pattern is a particular implementation of Inversion of Control.</span></span> <span data-ttu-id="22165-117">**IoC (제어 반전)** 는 개체에서 작업을 수행 하는 데 사용 하는 다른 개체를 만들지 않음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-117">**Inversion of Control (IoC)** means that objects do not create other objects on which they rely to do their work.</span></span> <span data-ttu-id="22165-118">대신 외부 소스에서 필요한 개체 (예: xml 구성 파일)를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="22165-118">Instead, they get the objects that they need from an outside source (for example, an xml configuration file).</span></span>

<span data-ttu-id="22165-119">**DI (종속성 주입)** 는 일반적으로 생성자 매개 변수를 전달 하 고 속성을 설정 하는 프레임 워크 구성 요소에서 개체 개입 없이이 작업을 수행 함을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-119">**Dependency Injection (DI)** means that this is done without the object intervention, usually by a framework component that passes constructor parameters and set properties.</span></span>

<a id="The_Dependency_Injection_DI_Design_Pattern"></a>
### <a name="the-dependency-injection-di-design-pattern"></a><span data-ttu-id="22165-120">DI (종속성 주입) 디자인 패턴</span><span class="sxs-lookup"><span data-stu-id="22165-120">The Dependency Injection (DI) Design Pattern</span></span>

<span data-ttu-id="22165-121">높은 수준에서 종속성 주입의 목표는 클라이언트 클래스 (예: *골퍼*)가 인터페이스를 충족 하는 항목 (예: *iclub*)을 요구 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="22165-121">At a high level, the goal of Dependency Injection is that a client class (e.g. *the golfer*) needs something that satisfies an interface (e.g. *IClub*).</span></span> <span data-ttu-id="22165-122">구체적 형식 (예: *WoodClub, IronClub, WedgeClub* 또는 *putterclub*)을 고려 하지 않고 다른 사람이이를 처리 하려고 합니다 (예: 좋은 *caddy*).</span><span class="sxs-lookup"><span data-stu-id="22165-122">It doesn't care what the concrete type is (e.g. *WoodClub, IronClub, WedgeClub* or *PutterClub*), it wants someone else to handle that (e.g. a good *caddy*).</span></span> <span data-ttu-id="22165-123">ASP.NET MVC의 종속성 확인자를 사용 하 여 다른 곳에 종속성 논리를 등록할 수 있습니다 (예: 컨테이너 또는 *클럽 모음*).</span><span class="sxs-lookup"><span data-stu-id="22165-123">The Dependency Resolver in ASP.NET MVC can allow you to register your dependency logic somewhere else (e.g. a container or a *bag of clubs*).</span></span>

<span data-ttu-id="22165-124">![종속성 주입 다이어그램](aspnet-mvc-4-dependency-injection/_static/image2.png "종속성 주입 그림")</span><span class="sxs-lookup"><span data-stu-id="22165-124">![Dependency Injection diagram](aspnet-mvc-4-dependency-injection/_static/image2.png "Dependency Injection illustration")</span></span>

<span data-ttu-id="22165-125">*종속성 주입-골프 비유*</span><span class="sxs-lookup"><span data-stu-id="22165-125">*Dependency Injection - Golf analogy*</span></span>

<span data-ttu-id="22165-126">종속성 주입 패턴 및 제어 반전을 사용 하면 다음과 같은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-126">The advantages of using Dependency Injection pattern and Inversion of Control are the following:</span></span>

- <span data-ttu-id="22165-127">클래스 결합을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="22165-127">Reduces class coupling</span></span>
- <span data-ttu-id="22165-128">코드 재사용 향상</span><span class="sxs-lookup"><span data-stu-id="22165-128">Increases code reusing</span></span>
- <span data-ttu-id="22165-129">코드 유지 관리 효율성 향상</span><span class="sxs-lookup"><span data-stu-id="22165-129">Improves code maintainability</span></span>
- <span data-ttu-id="22165-130">응용 프로그램 테스트 향상</span><span class="sxs-lookup"><span data-stu-id="22165-130">Improves application testing</span></span>

> [!NOTE]
> <span data-ttu-id="22165-131">종속성 주입은 추상 팩터리 디자인 패턴을 사용 하는 경우에 비해 약간 차이가 있지만 두 방법 간에는 약간의 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-131">Dependency Injection is sometimes compared with Abstract Factory Design Pattern, but there is a slight difference between both approaches.</span></span> <span data-ttu-id="22165-132">DI는 팩터리와 등록 된 서비스를 호출 하 여 종속성을 해결 하기 위한 프레임 워크를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-132">DI has a Framework working behind to solve dependencies by calling the factories and the registered services.</span></span>

<span data-ttu-id="22165-133">이제 종속성 주입 패턴을 이해 했으므로이 랩에서 ASP.NET MVC 4에서 적용 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="22165-133">Now that you understand the Dependency Injection Pattern, you will learn throughout this lab how to apply it in ASP.NET MVC 4.</span></span> <span data-ttu-id="22165-134">**컨트롤러** 에서 종속성 주입을 사용 하 여 데이터베이스 액세스 서비스를 포함 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-134">You will start using Dependency Injection in the **Controllers** to include a database access service.</span></span> <span data-ttu-id="22165-135">다음에는 서비스를 사용 하 고 정보를 표시 하는 종속성 주입을 **뷰에** 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-135">Next, you will apply Dependency Injection to the **Views** to consume a service and show information.</span></span> <span data-ttu-id="22165-136">마지막으로 DI를 ASP.NET MVC 4 필터로 확장 하 여 솔루션에 사용자 지정 작업 필터를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-136">Finally, you will extend the DI to ASP.NET MVC 4 Filters, injecting a custom action filter in the solution.</span></span>

<span data-ttu-id="22165-137">이 실습 랩에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="22165-137">In this Hands-on Lab, you will learn how to:</span></span>

- <span data-ttu-id="22165-138">NuGet 패키지를 사용 하 여 종속성 주입을 위해 ASP.NET MVC 4를 Unity와 통합</span><span class="sxs-lookup"><span data-stu-id="22165-138">Integrate ASP.NET MVC 4 with Unity for Dependency Injection using NuGet Packages</span></span>
- <span data-ttu-id="22165-139">ASP.NET MVC 컨트롤러 내에서 종속성 주입 사용</span><span class="sxs-lookup"><span data-stu-id="22165-139">Use Dependency Injection inside an ASP.NET MVC Controller</span></span>
- <span data-ttu-id="22165-140">ASP.NET MVC 뷰 내에서 종속성 주입 사용</span><span class="sxs-lookup"><span data-stu-id="22165-140">Use Dependency Injection inside an ASP.NET MVC View</span></span>
- <span data-ttu-id="22165-141">ASP.NET MVC 작업 필터 내에서 종속성 주입 사용</span><span class="sxs-lookup"><span data-stu-id="22165-141">Use Dependency Injection inside an ASP.NET MVC Action Filter</span></span>

> [!NOTE]
> <span data-ttu-id="22165-142">이 랩에서는 종속성 확인을 위해 Mvc3 NuGet 패키지를 사용 하 고 있지만 ASP.NET MVC 4에서 작동 하는 종속성 주입 프레임 워크를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-142">This Lab is using Unity.Mvc3 NuGet Package for dependency resolution, but it is possible to adapt any Dependency Injection Framework to work with ASP.NET MVC 4.</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="22165-143">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="22165-143">Prerequisites</span></span>

<span data-ttu-id="22165-144">이 랩을 완료 하려면 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-144">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="22165-145">[웹 또는 고급의 경우 2012 Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (설치 방법에 대 한 지침은 [부록 a를](#AppendixA) 참조 하세요.)</span><span class="sxs-lookup"><span data-stu-id="22165-145">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="22165-146">설치 프로그램</span><span class="sxs-lookup"><span data-stu-id="22165-146">Setup</span></span>

<span data-ttu-id="22165-147">**코드 조각 설치**</span><span class="sxs-lookup"><span data-stu-id="22165-147">**Installing Code Snippets**</span></span>

<span data-ttu-id="22165-148">편의를 위해이 랩에서 관리 하는 대부분의 코드는 Visual Studio 코드 조각으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-148">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="22165-149">코드 조각을 설치 하려면 **.\Source\Setup\CodeSnippets.vsi** 파일을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-149">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="22165-150">Visual Studio Code 코드 조각을 잘 모르는 경우이를 사용 하는 방법을 알아보려면이 문서의 부록 [B: 코드 조각&quot;사용](#AppendixB) &quot;부록을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="22165-150">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="22165-151">실습</span><span class="sxs-lookup"><span data-stu-id="22165-151">Exercises</span></span>

<span data-ttu-id="22165-152">이 실습 랩은 다음 연습으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22165-152">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="22165-153">연습 1: 컨트롤러 삽입</span><span class="sxs-lookup"><span data-stu-id="22165-153">Exercise 1: Injecting a Controller</span></span>](#Exercise1)
2. [<span data-ttu-id="22165-154">연습 2: 보기 삽입</span><span class="sxs-lookup"><span data-stu-id="22165-154">Exercise 2: Injecting a View</span></span>](#Exercise2)
3. [<span data-ttu-id="22165-155">연습 3: 필터 삽입</span><span class="sxs-lookup"><span data-stu-id="22165-155">Exercise 3: Injecting Filters</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="22165-156">각 연습에는 연습을 완료 한 후 얻게 되는 결과 솔루션을 포함 하는 **끝** 폴더가 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22165-156">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="22165-157">연습을 진행 하는 데 도움이 필요한 경우이 솔루션을 지침으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-157">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="22165-158">이 랩을 완료 하는 데 소요 되는 예상 시간: **30 분**</span><span class="sxs-lookup"><span data-stu-id="22165-158">Estimated time to complete this lab: **30 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Injecting_a_Controller"></a>
### <a name="exercise-1-injecting-a-controller"></a><span data-ttu-id="22165-159">연습 1: 컨트롤러 삽입</span><span class="sxs-lookup"><span data-stu-id="22165-159">Exercise 1: Injecting a Controller</span></span>

<span data-ttu-id="22165-160">이 연습에서는 NuGet 패키지를 사용 하 여 Unity를 통합 하 여 ASP.NET MVC 컨트롤러에서 종속성 주입을 사용 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-160">In this exercise, you will learn how to use Dependency Injection in ASP.NET MVC Controllers by integrating Unity using a NuGet Package.</span></span> <span data-ttu-id="22165-161">이러한 이유로 MvcMusicStore 컨트롤러에 서비스를 포함 하 여 데이터 액세스와 논리를 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-161">For that reason, you will include services into your MvcMusicStore controllers to separate the logic from the data access.</span></span> <span data-ttu-id="22165-162">서비스는 **Unity**의 도움으로 종속성 주입을 사용 하 여 확인 되는 컨트롤러 생성자에 새 종속성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22165-162">The services will create a new dependency in the controller constructor, which will be resolved using Dependency Injection with the help of **Unity**.</span></span>

<span data-ttu-id="22165-163">이 방법은 더 유연 하 고 쉽게 유지 관리 하 고 테스트할 수 있는 더 작은 결합 응용 프로그램을 생성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="22165-163">This approach will show you how to generate less coupled applications, which are more flexible and easier to maintain and test.</span></span> <span data-ttu-id="22165-164">ASP.NET MVC를 Unity와 통합 하는 방법에 대해서도 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="22165-164">You will also learn how to integrate ASP.NET MVC with Unity.</span></span>

<a id="About_StoreManager_Service"></a>
#### <a name="about-storemanager-service"></a><span data-ttu-id="22165-165">About StoreManager Service</span><span class="sxs-lookup"><span data-stu-id="22165-165">About StoreManager Service</span></span>

<span data-ttu-id="22165-166">이제 begin 솔루션에 제공 된 MVC Music 저장소에 **StoreService**이라는 저장소 컨트롤러 데이터를 관리 하는 서비스가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-166">The MVC Music Store provided in the begin solution now includes a service that manages the Store Controller data named **StoreService**.</span></span> <span data-ttu-id="22165-167">아래에서 매장 서비스 구현을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-167">Below you will find the Store Service implementation.</span></span> <span data-ttu-id="22165-168">모든 메서드는 모델 엔터티를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-168">Note that all the methods return Model entities.</span></span>

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample1.cs)]

<span data-ttu-id="22165-169">이제 시작 솔루션의 **StoreController** 가 **StoreService**을 소비 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-169">**StoreController** from the begin solution now consumes **StoreService**.</span></span> <span data-ttu-id="22165-170">모든 데이터 참조는 **StoreController**에서 제거 되었으므로 **StoreService**를 사용 하는 메서드를 변경 하지 않고 현재 데이터 액세스 공급자를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-170">All the data references were removed from **StoreController**, and now possible to modify the current data access provider without changing any method that consumes **StoreService**.</span></span>

<span data-ttu-id="22165-171">**StoreController** 구현이 클래스 생성자 내에서 **StoreService** 를 사용 하 여 종속성을 포함 한다는 것을 아래에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-171">You will find below that the **StoreController** implementation has a dependency with **StoreService** inside the class constructor.</span></span>

> [!NOTE]
> <span data-ttu-id="22165-172">이 연습에서 소개 하는 종속성은 IoC ( **제어 반전** )와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-172">The dependency introduced in this exercise is related to **Inversion of Control** (IoC).</span></span>
> 
> <span data-ttu-id="22165-173">**StoreController** 클래스 생성자는 클래스 내부에서 서비스 호출을 수행 하는 데 필수적인 **IStoreService** 형식 매개 변수를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-173">The **StoreController** class constructor receives an **IStoreService** type parameter, which is essential to perform service calls from inside the class.</span></span> <span data-ttu-id="22165-174">그러나 **StoreController** 는 모든 컨트롤러가 ASP.NET MVC와 함께 사용 해야 하는 기본 생성자 (매개 변수 없음)를 구현 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-174">However, **StoreController** does not implement the default constructor (with no parameters) that any controller must have to work with ASP.NET MVC.</span></span>
> 
> <span data-ttu-id="22165-175">종속성을 확인 하려면 추상 팩터리 (지정 된 형식의 개체를 반환 하는 클래스)에 의해 컨트롤러를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-175">To resolve the dependency, the controller has to be created by an abstract factory (a class that returns any object of the specified type).</span></span>

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="22165-176">매개 변수가 없는 생성자를 선언 하지 않았으므로 클래스에서 서비스 개체를 보내지 않고 StoreController를 만들려고 하면 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-176">You will get an error when the class tries to create the StoreController without sending the service object, as there is no parameterless constructor declared.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Running_the_Application"></a>
#### <a name="task-1---running-the-application"></a><span data-ttu-id="22165-177">작업 1-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="22165-177">Task 1 - Running the Application</span></span>

<span data-ttu-id="22165-178">이 작업에서는 응용 프로그램 논리에서 데이터 액세스를 분리 하는 저장소 컨트롤러에 서비스를 포함 하는 Begin 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-178">In this task, you will run the Begin application, which includes the service into the Store Controller that separates the data access from the application logic.</span></span>

<span data-ttu-id="22165-179">응용 프로그램을 실행할 때 컨트롤러 서비스가 기본적으로 매개 변수로 전달 되지 않기 때문에 예외를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-179">When running the application, you will receive an exception, as the controller service is not passed as a parameter by default:</span></span>

1. <span data-ttu-id="22165-180">**Source\ex01-injecting**에서 **시작** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="22165-180">Open the **Begin** solution located in **Source\Ex01-Injecting Controller\Begin**.</span></span>

   1. <span data-ttu-id="22165-181">계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-181">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="22165-182">이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-182">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="22165-183">**NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-183">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="22165-184">마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-184">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="22165-185">NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="22165-185">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="22165-186">NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-186">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="22165-187">이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-187">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="22165-188">**Ctrl + F5** 키를 눌러 디버깅 하지 않고 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-188">Press **Ctrl + F5** to run the application without debugging.</span></span> <span data-ttu-id="22165-189">**이 개체&quot;에 대해 정의 된 매개 변수가 없는 생성자** &quot;오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22165-189">You will get the error message &quot;**No parameterless constructor defined for this object**&quot;:</span></span>

    <span data-ttu-id="22165-190">![ASP.NET MVC Begin 응용 프로그램을 실행 하는 동안 오류 발생](aspnet-mvc-4-dependency-injection/_static/image3.png "ASP.NET MVC Begin 응용 프로그램을 실행 하는 동안 오류 발생")</span><span class="sxs-lookup"><span data-stu-id="22165-190">![Error while running ASP.NET MVC Begin Application](aspnet-mvc-4-dependency-injection/_static/image3.png "Error while running ASP.NET MVC Begin Application")</span></span>

    <span data-ttu-id="22165-191">*ASP.NET MVC Begin 응용 프로그램을 실행 하는 동안 오류 발생*</span><span class="sxs-lookup"><span data-stu-id="22165-191">*Error while running ASP.NET MVC Begin Application*</span></span>
3. <span data-ttu-id="22165-192">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-192">Close the browser.</span></span>

<span data-ttu-id="22165-193">다음 단계에서는이 컨트롤러에 필요한 종속성을 삽입 하기 위해 Music Store 솔루션에 대해 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-193">In the following steps you will work on the Music Store Solution to inject the dependency this controller needs.</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Including_Unity_into_MvcMusicStore_Solution"></a>
#### <a name="task-2---including-unity-into-mvcmusicstore-solution"></a><span data-ttu-id="22165-194">작업 2-Unity를 MvcMusicStore 솔루션으로 포함</span><span class="sxs-lookup"><span data-stu-id="22165-194">Task 2 - Including Unity into MvcMusicStore Solution</span></span>

<span data-ttu-id="22165-195">이 작업에서는 솔루션에 **Mvc3** NuGet 패키지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-195">In this task, you will include **Unity.Mvc3** NuGet Package to the solution.</span></span>

> [!NOTE]
> <span data-ttu-id="22165-196">Mvc3 패키지는 ASP.NET MVC 3 용으로 설계 되었지만 ASP.NET MVC 4와 완전히 호환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22165-196">Unity.Mvc3 package was designed for ASP.NET MVC 3, but it is fully compatible with ASP.NET MVC 4.</span></span>
> 
> <span data-ttu-id="22165-197">Unity는 인스턴스 및 유형 가로채기에 대 한 선택적 지원을 포함 하는 간단 하 고 확장 가능한 종속성 주입 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="22165-197">Unity is a lightweight, extensible dependency injection container with optional support for instance and type interception.</span></span> <span data-ttu-id="22165-198">모든 형식의 .NET 응용 프로그램에서 사용할 수 있는 범용 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="22165-198">It is a general-purpose container for use in any type of .NET application.</span></span> <span data-ttu-id="22165-199">이 클래스는 컨테이너에 대 한 구성 요소 구성을 지연 하 여 개체 만들기, 런타임에 종속성을 지정 하는 요구 사항 추상화, 요구 사항 추상화를 비롯 하 여 종속성 주입 메커니즘에 있는 모든 일반적인 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-199">It provides all the common features found in dependency injection mechanisms including: object creation, abstraction of requirements by specifying dependencies at runtime and flexibility, by deferring the component configuration to the container.</span></span>

1. <span data-ttu-id="22165-200">**MvcMusicStore** 프로젝트에 **Mvc3** NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-200">Install **Unity.Mvc3** NuGet Package in the **MvcMusicStore** project.</span></span> <span data-ttu-id="22165-201">이렇게 하려면 **다른 창** | **보기** 에서 **패키지 관리자 콘솔** 을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="22165-201">To do this, open the **Package Manager Console** from **View** | **Other Windows**.</span></span>
2. <span data-ttu-id="22165-202">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-202">Run the following command.</span></span>

    <span data-ttu-id="22165-203">PMC</span><span class="sxs-lookup"><span data-stu-id="22165-203">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-dependency-injection/samples/sample3.ps1)]

    <span data-ttu-id="22165-204">![Mvc3 NuGet 패키지를 설치 하는 중](aspnet-mvc-4-dependency-injection/_static/image4.png "Mvc3 NuGet 패키지를 설치 하는 중")</span><span class="sxs-lookup"><span data-stu-id="22165-204">![Installing Unity.Mvc3 NuGet Package](aspnet-mvc-4-dependency-injection/_static/image4.png "Installing Unity.Mvc3 NuGet Package")</span></span>

    <span data-ttu-id="22165-205">*Mvc3 NuGet 패키지를 설치 하는 중*</span><span class="sxs-lookup"><span data-stu-id="22165-205">*Installing Unity.Mvc3 NuGet Package*</span></span>
3. <span data-ttu-id="22165-206">**Mvc3** 패키지가 설치 되 면 unity 구성을 간소화 하기 위해 자동으로 추가 하는 파일 및 폴더를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-206">Once the **Unity.Mvc3** package is installed, explore the files and folders it automatically adds in order to simplify Unity configuration.</span></span>

    <span data-ttu-id="22165-207">![Mvc3 패키지가 설치 됨](aspnet-mvc-4-dependency-injection/_static/image5.png "Mvc3 패키지가 설치 됨")</span><span class="sxs-lookup"><span data-stu-id="22165-207">![Unity.Mvc3 package installed](aspnet-mvc-4-dependency-injection/_static/image5.png "Unity.Mvc3 package installed")</span></span>

    <span data-ttu-id="22165-208">*Mvc3 패키지가 설치 됨*</span><span class="sxs-lookup"><span data-stu-id="22165-208">*Unity.Mvc3 package installed*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Registering_Unity_in_Globalasaxcs_Application_Start"></a>
#### <a name="task-3---registering-unity-in-globalasaxcs-application_start"></a><span data-ttu-id="22165-209">작업 3-Global.asax.cs 응용 프로그램에서 Unity 등록\_시작</span><span class="sxs-lookup"><span data-stu-id="22165-209">Task 3 - Registering Unity in Global.asax.cs Application\_Start</span></span>

<span data-ttu-id="22165-210">이 작업에서는 **Global.asax.cs** 에 있는 **응용 프로그램\_시작** 메서드를 업데이트 하 여 Unity 부트스트래퍼 이니셜라이저를 호출한 다음 종속성 주입에 사용할 서비스와 컨트롤러를 등록 하는 부트스트래퍼 파일을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-210">In this task, you will update the **Application\_Start** method located in **Global.asax.cs** to call the Unity Bootstrapper initializer and then, update the Bootstrapper file registering the Service and Controller you will use for Dependency Injection.</span></span>

1. <span data-ttu-id="22165-211">이제 Unity 컨테이너와 종속성 확인자를 초기화 하는 파일인 부트스트래퍼가 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22165-211">Now, you will hook up the Bootstrapper which is the file that initializes the Unity container and Dependency Resolver.</span></span> <span data-ttu-id="22165-212">이렇게 하려면 **Global.asax.cs** 를 열고 **응용 프로그램\_Start** 메서드 내에 다음 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-212">To do this, open **Global.asax.cs** and add the following highlighted code within the **Application\_Start** method.</span></span>

    <span data-ttu-id="22165-213">(코드 조각- *ASP.NET 종속성 주입 랩-Ex01-Unity Unity*)</span><span class="sxs-lookup"><span data-stu-id="22165-213">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Initialize Unity*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample4.cs)]
2. <span data-ttu-id="22165-214">**Bootstrapper.cs** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="22165-214">Open **Bootstrapper.cs** file.</span></span>
3. <span data-ttu-id="22165-215">**MvcMusicStore** 및 **MusicStore**네임 스페이스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-215">Include the following namespaces: **MvcMusicStore.Services** and **MusicStore.Controllers**.</span></span>

    <span data-ttu-id="22165-216">(코드 조각- *ASP.NET 종속성 주입 랩-Ex01-부트스트래퍼 네임 스페이스 추가*)</span><span class="sxs-lookup"><span data-stu-id="22165-216">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Bootstrapper Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample5.cs)]
4. <span data-ttu-id="22165-217">**Buildunitycontainer** 메서드의 콘텐츠를 store Controller 및 store 서비스를 등록 하는 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="22165-217">Replace **BuildUnityContainer** method's content with the following code that registers Store Controller and Store Service.</span></span>

    <span data-ttu-id="22165-218">(코드 조각- *ASP.NET 종속성 주입 랩-Ex01-Register Store Controller And Service*)</span><span class="sxs-lookup"><span data-stu-id="22165-218">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Register Store Controller and Service*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample6.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="22165-219">작업 4-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="22165-219">Task 4 - Running the Application</span></span>

<span data-ttu-id="22165-220">이 작업에서는 응용 프로그램을 실행 하 여 Unity를 포함 한 후 응용 프로그램을 로드할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-220">In this task, you will run the application to verify that it can now be loaded after including Unity.</span></span>

1. <span data-ttu-id="22165-221">**F5** 키를 눌러 응용 프로그램을 실행 합니다. 그러면 응용 프로그램이 오류 메시지를 표시 하지 않고 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22165-221">Press **F5** to run the application, the application should now load without showing any error message.</span></span>

    <span data-ttu-id="22165-222">![종속성 주입을 사용 하 여 응용 프로그램 실행](aspnet-mvc-4-dependency-injection/_static/image6.png "종속성 주입을 사용 하 여 응용 프로그램 실행")</span><span class="sxs-lookup"><span data-stu-id="22165-222">![Running Application with Dependency Injection](aspnet-mvc-4-dependency-injection/_static/image6.png "Running Application with Dependency Injection")</span></span>

    <span data-ttu-id="22165-223">*종속성 주입을 사용 하 여 응용 프로그램 실행*</span><span class="sxs-lookup"><span data-stu-id="22165-223">*Running Application with Dependency Injection*</span></span>
2. <span data-ttu-id="22165-224">**/Store**으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-224">Browse to **/Store**.</span></span> <span data-ttu-id="22165-225">이제 **Unity**를 사용 하 여 만든 **StoreController**이 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22165-225">This will invoke **StoreController**, which is now created using **Unity**.</span></span>

    <span data-ttu-id="22165-226">![MVC Music Store](aspnet-mvc-4-dependency-injection/_static/image7.png "MVC Music Store")</span><span class="sxs-lookup"><span data-stu-id="22165-226">![MVC Music Store](aspnet-mvc-4-dependency-injection/_static/image7.png "MVC Music Store")</span></span>

    <span data-ttu-id="22165-227">*MVC Music Store*</span><span class="sxs-lookup"><span data-stu-id="22165-227">*MVC Music Store*</span></span>
3. <span data-ttu-id="22165-228">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-228">Close the browser.</span></span>

<span data-ttu-id="22165-229">다음 연습에서는 ASP.NET MVC 뷰 및 작업 필터 내에서 사용 하기 위해 종속성 주입 범위를 확장 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="22165-229">In the following exercises you will learn how to extend the Dependency Injection scope to use it inside ASP.NET MVC Views and Action Filters.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Injecting_a_View"></a>
### <a name="exercise-2-injecting-a-view"></a><span data-ttu-id="22165-230">연습 2: 보기 삽입</span><span class="sxs-lookup"><span data-stu-id="22165-230">Exercise 2: Injecting a View</span></span>

<span data-ttu-id="22165-231">이 연습에서는 ASP.NET MVC 4 for Unity 통합의 새로운 기능을 사용 하 여 뷰에서 종속성 주입을 사용 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-231">In this exercise, you will learn how to use Dependency Injection in a view with the new features of ASP.NET MVC 4 for Unity integration.</span></span> <span data-ttu-id="22165-232">이렇게 하려면 저장소 찾아보기 보기 내에서 사용자 지정 서비스를 호출 합니다. 그러면 아래에 메시지와 이미지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22165-232">In order to do that, you will call a custom service inside the Store Browse View, which will show a message and an image below.</span></span>

<span data-ttu-id="22165-233">그런 다음 프로젝트를 Unity와 통합 하 고 사용자 지정 종속성 해결 프로그램을 만들어 종속성을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-233">Then, you will integrate the project with Unity and create a custom dependency resolver to inject the dependencies.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Creating_a_View_that_Consumes_a_Service"></a>
#### <a name="task-1---creating-a-view-that-consumes-a-service"></a><span data-ttu-id="22165-234">작업 1-서비스를 사용 하는 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="22165-234">Task 1 - Creating a View that Consumes a Service</span></span>

<span data-ttu-id="22165-235">이 태스크에서는 새 종속성을 생성 하기 위해 서비스 호출을 수행 하는 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22165-235">In this task, you will create a view that performs a service call to generate a new dependency.</span></span> <span data-ttu-id="22165-236">서비스는이 솔루션에 포함 된 간단한 메시징 서비스로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22165-236">The service consists in a simple messaging service included in this solution.</span></span>

1. <span data-ttu-id="22165-237">**Source\ex02-injecting View\Begin** 폴더에 있는 **begin** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="22165-237">Open the **Begin** solution located in the **Source\Ex02-Injecting View\Begin** folder.</span></span> <span data-ttu-id="22165-238">그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-238">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="22165-239">제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-239">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="22165-240">이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-240">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="22165-241">**NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-241">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="22165-242">마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-242">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="22165-243">NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="22165-243">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="22165-244">NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-244">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="22165-245">이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-245">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
      > 
      > <span data-ttu-id="22165-246">자세한 내용은 [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="22165-246">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="22165-247">**MessageService.cs** 및 **IMessageService.cs** 클래스를 **/서비스**의 **Source \assets** 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-247">Include the **MessageService.cs** and the **IMessageService.cs** classes located in the **Source \Assets** folder in **/Services**.</span></span> <span data-ttu-id="22165-248">이렇게 하려면 **서비스** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **기존 항목 추가**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-248">To do this, right-click **Services** folder and select **Add Existing Item**.</span></span> <span data-ttu-id="22165-249">파일의 위치를 찾아 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-249">Browse to the files' location and include them.</span></span>

    <span data-ttu-id="22165-250">![메시지 서비스 및 서비스 인터페이스 추가](aspnet-mvc-4-dependency-injection/_static/image8.png "메시지 서비스 및 서비스 인터페이스 추가")</span><span class="sxs-lookup"><span data-stu-id="22165-250">![Adding Message Service and Service Interface](aspnet-mvc-4-dependency-injection/_static/image8.png "Adding Message Service and Service Interface")</span></span>

    <span data-ttu-id="22165-251">*메시지 서비스 및 서비스 인터페이스 추가*</span><span class="sxs-lookup"><span data-stu-id="22165-251">*Adding Message Service and Service Interface*</span></span>

    > [!NOTE]
    > <span data-ttu-id="22165-252">**IMessageService** 인터페이스는 **MessageService** 클래스에서 구현 하는 두 가지 속성을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-252">The **IMessageService** interface defines two properties implemented by the **MessageService** class.</span></span> <span data-ttu-id="22165-253">이러한 속성-**message** 및 **ImageUrl**-메시지와 표시할 이미지의 URL을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-253">These properties -**Message** and **ImageUrl**- store the message and the URL of the image to be displayed.</span></span>
3. <span data-ttu-id="22165-254">프로젝트의 루트 폴더에 폴더 **/페이지** 를 만든 다음 **source\assets**에서 기존 클래스 **MyBasePage.cs** 를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-254">Create the folder **/Pages** in the project's root folder, and then add the existing class **MyBasePage.cs** from **Source\Assets**.</span></span> <span data-ttu-id="22165-255">상속 하는 기본 페이지의 구조는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-255">The base page you will inherit from has the following structure.</span></span>

    <span data-ttu-id="22165-256">![Pages 폴더](aspnet-mvc-4-dependency-injection/_static/image9.png "페이지 폴더")</span><span class="sxs-lookup"><span data-stu-id="22165-256">![Pages folder](aspnet-mvc-4-dependency-injection/_static/image9.png "Pages folder")</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample7.cs)]
4. <span data-ttu-id="22165-257">**/Views/Store** 폴더에서 **Browse. cshtml** 뷰를 열고 **MyBasePage.cs**에서 상속 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-257">Open **Browse.cshtml** view from **/Views/Store** folder, and make it inherit from **MyBasePage.cs**.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample8.cshtml)]
5. <span data-ttu-id="22165-258">**찾아보기** 보기에서 **MessageService** 에 대 한 호출을 추가 하 여 서비스에서 검색 한 이미지와 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-258">In the **Browse** view, add a call to **MessageService** to display an image and a message retrieved by the service.</span></span>
   <span data-ttu-id="22165-259">(C#)</span><span class="sxs-lookup"><span data-stu-id="22165-259">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample9.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Including_a_Custom_Dependency_Resolver_and_a_Custom_View_Page_Activator"></a>
#### <a name="task-2---including-a-custom-dependency-resolver-and-a-custom-view-page-activator"></a><span data-ttu-id="22165-260">작업 2-사용자 지정 종속성 해결 프로그램 및 사용자 지정 뷰 페이지 활성기 포함</span><span class="sxs-lookup"><span data-stu-id="22165-260">Task 2 - Including a Custom Dependency Resolver and a Custom View Page Activator</span></span>

<span data-ttu-id="22165-261">이전 작업에서는 뷰 내부에 새 종속성을 삽입 하 여 내부에서 서비스 호출을 수행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-261">In the previous task, you injected a new dependency inside a view to perform a service call inside it.</span></span> <span data-ttu-id="22165-262">이제 ASP.NET MVC 종속성 주입 인터페이스 **Iviewpageactivator** 및 **되며 idependencyresolver**를 구현 하 여 해당 종속성을 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-262">Now, you will resolve that dependency by implementing the ASP.NET MVC Dependency Injection interfaces **IViewPageActivator** and **IDependencyResolver**.</span></span> <span data-ttu-id="22165-263">Unity를 사용 하 여 서비스 검색을 처리 하는 **되며 idependencyresolver** 의 구현을 솔루션에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-263">You will include in the solution an implementation of **IDependencyResolver** that will deal with the service retrieval by using Unity.</span></span> <span data-ttu-id="22165-264">그런 다음 뷰 만들기를 해결 하는 **Iviewpageactivator** 인터페이스의 또 다른 사용자 지정 구현을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-264">Then, you will include another custom implementation of **IViewPageActivator** interface that will solve the creation of the views.</span></span>

> [!NOTE]
> <span data-ttu-id="22165-265">ASP.NET MVC 3부터 종속성 주입에 대 한 구현이 서비스를 등록 하는 인터페이스를 간소화 했습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-265">Since ASP.NET MVC 3, the implementation for Dependency Injection had simplified the interfaces to register services.</span></span> <span data-ttu-id="22165-266">**되며 idependencyresolver** 및 **Iviewpageactivator** 는 종속성 주입에 대 한 ASP.NET MVC 3 기능의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="22165-266">**IDependencyResolver** and **IViewPageActivator** are part of ASP.NET MVC 3 features for Dependency Injection.</span></span>
> 
> <span data-ttu-id="22165-267">**-되며 idependencyresolver** interface는 이전 IMvcServiceLocator를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-267">**- IDependencyResolver** interface replaces the previous IMvcServiceLocator.</span></span> <span data-ttu-id="22165-268">되며 idependencyresolver의 구현자는 서비스 또는 서비스 컬렉션의 인스턴스를 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-268">Implementers of IDependencyResolver must return an instance of the service or a service collection.</span></span>
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample10.cs)]
> 
> <span data-ttu-id="22165-269">**-Iviewpageactivator** 인터페이스는 종속성 주입을 통해 뷰 페이지를 인스턴스화하는 방법을 보다 세밀 하 게 제어할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-269">**- IViewPageActivator** interface provides more fine-grained control over how view pages are instantiated via dependency injection.</span></span> <span data-ttu-id="22165-270">**Iviewpageactivator** 인터페이스를 구현 하는 클래스는 컨텍스트 정보를 사용 하 여 뷰 인스턴스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-270">The classes that implement **IViewPageActivator** interface can create view instances using context information.</span></span>
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample11.cs)]

1. <span data-ttu-id="22165-271">프로젝트의 루트 폴더에/**팩터리** 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22165-271">Create the /**Factories** folder in the project's root folder.</span></span>
2. <span data-ttu-id="22165-272">**/Sources/Assets/** 에서 **팩터리** 폴더로 솔루션에 **CustomViewPageActivator.cs** 를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-272">Include **CustomViewPageActivator.cs** to your solution from **/Sources/Assets/** to **Factories** folder.</span></span> <span data-ttu-id="22165-273">이렇게 하려면 **/ss** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 기존 항목** 을 선택한 다음 **CustomViewPageActivator.cs**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-273">To do that, right-click the **/Factories** folder, select **Add | Existing Item** and then select **CustomViewPageActivator.cs**.</span></span> <span data-ttu-id="22165-274">이 클래스는 Unity 컨테이너를 포함 하는 **Iviewpageactivator** 인터페이스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-274">This class implements the **IViewPageActivator** interface to hold the Unity Container.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample12.cs)]

    > [!NOTE]
    > <span data-ttu-id="22165-275">**Customviewpageactivator** 는 Unity 컨테이너를 사용 하 여 뷰 만들기를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-275">**CustomViewPageActivator** is responsible for managing the creation of a view by using a Unity container.</span></span>
3. <span data-ttu-id="22165-276">**UnityDependencyResolver.cs** 파일을 **/source/pers** **폴더에 포함** 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-276">Include **UnityDependencyResolver.cs** file from **/Sources/Assets** to **/Factories** folder.</span></span> <span data-ttu-id="22165-277">이렇게 하려면 **/ss** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 기존 항목** 을 선택한 다음 **UnityDependencyResolver.cs** 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-277">To do that, right-click the **/Factories** folder, select **Add | Existing Item** and then select **UnityDependencyResolver.cs** file.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample13.cs)]

    > [!NOTE]
    > <span data-ttu-id="22165-278">**UnityDependencyResolver** 클래스는 Unity의 사용자 지정 DependencyResolver입니다.</span><span class="sxs-lookup"><span data-stu-id="22165-278">**UnityDependencyResolver** class is a custom DependencyResolver for Unity.</span></span> <span data-ttu-id="22165-279">Unity 컨테이너 내에서 서비스를 찾을 수 없는 경우 기본 해결 프로그램은 invocated입니다.</span><span class="sxs-lookup"><span data-stu-id="22165-279">When a service cannot be found inside the Unity container, the base resolver is invocated.</span></span>

<span data-ttu-id="22165-280">다음 태스크에서는 모델에서 서비스 및 뷰의 위치를 알 수 있도록 두 구현이 모두 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22165-280">In the following task both implementations will be registered to let the model know the location of the services and the views.</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_-_Registering_for_Dependency_Injection_within_Unity_container"></a>
#### <a name="task-3---registering-for-dependency-injection-within-unity-container"></a><span data-ttu-id="22165-281">작업 3-Unity 컨테이너 내에서 종속성 주입에 등록</span><span class="sxs-lookup"><span data-stu-id="22165-281">Task 3 - Registering for Dependency Injection within Unity container</span></span>

<span data-ttu-id="22165-282">이 태스크에서는 종속성 주입 작업을 수행 하기 위해 모든 이전 항목을 함께 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-282">In this task, you will put all the previous things together to make Dependency Injection work.</span></span>

<span data-ttu-id="22165-283">이제 솔루션에는 다음과 같은 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-283">Up to now your solution has the following elements:</span></span>

- <span data-ttu-id="22165-284">**MyBaseClass** 에서 상속 되 고 **MessageService**를 소비 하는 **찾아보기** 뷰입니다.</span><span class="sxs-lookup"><span data-stu-id="22165-284">A **Browse** View that inherits from **MyBaseClass** and consumes **MessageService**.</span></span>
- <span data-ttu-id="22165-285">서비스 인터페이스에 대해 선언 된 종속성 주입을 포함 하는 중간 클래스-**MyBaseClass**-</span><span class="sxs-lookup"><span data-stu-id="22165-285">An intermediate class -**MyBaseClass**- that has dependency injection declared for the service interface.</span></span>
- <span data-ttu-id="22165-286">**MessageService** 및 **IMessageService**인터페이스를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-286">A service - **MessageService** - and its interface **IMessageService**.</span></span>
- <span data-ttu-id="22165-287">서비스 검색을 처리 하는 **UnityDependencyResolver** -에 대 한 사용자 지정 종속성 해결 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="22165-287">A custom dependency resolver for Unity - **UnityDependencyResolver** - that deals with service retrieval.</span></span>
- <span data-ttu-id="22165-288">페이지를 만드는 뷰 페이지 활성기- **Customviewpageactivator** -</span><span class="sxs-lookup"><span data-stu-id="22165-288">A View Page activator - **CustomViewPageActivator** - that creates the page.</span></span>

<span data-ttu-id="22165-289">**찾아보기** 보기를 삽입 하려면 이제 Unity 컨테이너에 사용자 지정 종속성 해결 프로그램을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-289">To inject **Browse** View, you will now register the custom dependency resolver in the Unity container.</span></span>

1. <span data-ttu-id="22165-290">**Bootstrapper.cs** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="22165-290">Open **Bootstrapper.cs** file.</span></span>
2. <span data-ttu-id="22165-291">**MessageService** 의 인스턴스를 Unity 컨테이너에 등록 하 여 서비스를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-291">Register an instance of **MessageService** into the Unity container to initialize the service:</span></span>

    <span data-ttu-id="22165-292">(코드 조각- *ASP.NET 종속성 주입 랩-Ex02-Register Message Service*)</span><span class="sxs-lookup"><span data-stu-id="22165-292">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Register Message Service*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample14.cs)]
3. <span data-ttu-id="22165-293">**MvcMusicStore** 네임 스페이스에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-293">Add a reference to **MvcMusicStore.Factories** namespace.</span></span>

    <span data-ttu-id="22165-294">(코드 조각- *ASP.NET 종속성 주입 랩-Ex02 네임 스페이스*)</span><span class="sxs-lookup"><span data-stu-id="22165-294">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Factories Namespace*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample15.cs)]
4. <span data-ttu-id="22165-295">**Customviewpageactivator** 를 Unity 컨테이너에 뷰 페이지 활성기로 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-295">Register **CustomViewPageActivator** as a View Page activator into the Unity container:</span></span>

    <span data-ttu-id="22165-296">(코드 조각- *ASP.NET 종속성 주입 랩-Ex02-Register CustomViewPageActivator*)</span><span class="sxs-lookup"><span data-stu-id="22165-296">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Register CustomViewPageActivator*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample16.cs)]
5. <span data-ttu-id="22165-297">ASP.NET MVC 4 기본 종속성 해결 프로그램을 **UnityDependencyResolver**인스턴스로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="22165-297">Replace ASP.NET MVC 4 default dependency resolver with an instance of **UnityDependencyResolver**.</span></span> <span data-ttu-id="22165-298">이렇게 하려면 **Initialize** 메서드 콘텐츠를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="22165-298">To do this, replace **Initialize** method content with the following code:</span></span>

    <span data-ttu-id="22165-299">(코드 조각- *ASP.NET 종속성 주입 랩-Ex02-종속성 확인자 업데이트*)</span><span class="sxs-lookup"><span data-stu-id="22165-299">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Update Dependency Resolver*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample17.cs)]

    > [!NOTE]
    > <span data-ttu-id="22165-300">ASP.NET MVC는 기본 종속성 확인자 클래스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-300">ASP.NET MVC provides a default dependency resolver class.</span></span> <span data-ttu-id="22165-301">Unity 용으로 만든 사용자 지정 종속성 해결 프로그램을 사용 하려면이 해결 프로그램을 바꾸어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-301">To work with custom dependency resolvers as the one we have created for unity, this resolver has to be replaced.</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="22165-302">작업 4-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="22165-302">Task 4 - Running the Application</span></span>

<span data-ttu-id="22165-303">이 작업에서는 응용 프로그램을 실행 하 여 저장소 브라우저가 서비스를 사용 하는지 확인 하 고 검색 된 이미지와 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-303">In this task, you will run the application to verify that the Store Browser consumes the service and shows the image and the message retrieved:</span></span>

1. <span data-ttu-id="22165-304">**F5** 키를 눌러 애플리케이션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-304">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="22165-305">장르 메뉴 내에서 **바위** 를 클릭 하 고 **MessageService** 가 보기에 삽입 되 고 환영 메시지와 이미지를 로드 하는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-305">Click **Rock** within the Genres Menu and see how the **MessageService** was injected to the view and loaded the welcome message and the image.</span></span> <span data-ttu-id="22165-306">이 예제에서는 &quot;**록**&quot;을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-306">In this example, we are entering to &quot;**Rock**&quot;:</span></span>

    <span data-ttu-id="22165-307">![MVC Music Store-뷰 삽입](aspnet-mvc-4-dependency-injection/_static/image10.png "MVC Music Store-뷰 삽입")</span><span class="sxs-lookup"><span data-stu-id="22165-307">![MVC Music Store - View Injection](aspnet-mvc-4-dependency-injection/_static/image10.png "MVC Music Store - View Injection")</span></span>

    <span data-ttu-id="22165-308">*MVC Music Store-뷰 삽입*</span><span class="sxs-lookup"><span data-stu-id="22165-308">*MVC Music Store - View Injection*</span></span>
3. <span data-ttu-id="22165-309">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-309">Close the browser.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Injecting_Action_Filters"></a>
### <a name="exercise-3-injecting-action-filters"></a><span data-ttu-id="22165-310">연습 3: 작업 필터 삽입</span><span class="sxs-lookup"><span data-stu-id="22165-310">Exercise 3: Injecting Action Filters</span></span>

<span data-ttu-id="22165-311">이전 실습 랩 **사용자 지정 작업 필터** 에서 필터 사용자 지정 및 삽입으로 작업 했습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-311">In the previous Hands-On lab **Custom Action Filters** you have worked with filters customization and injection.</span></span> <span data-ttu-id="22165-312">이 연습에서는 Unity 컨테이너를 사용 하 여 종속성 주입으로 필터를 삽입 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-312">In this exercise, you will learn how to inject filters with Dependency Injection by using the Unity container.</span></span> <span data-ttu-id="22165-313">이렇게 하려면 사이트의 활동을 추적 하는 사용자 지정 작업 필터를 Music Store 솔루션에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-313">To do that, you will add to the Music Store solution a custom action filter that will trace the activity of the site.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Including_the_Tracking_Filter_in_the_Solution"></a>
#### <a name="task-1---including-the-tracking-filter-in-the-solution"></a><span data-ttu-id="22165-314">작업 1-솔루션에 추적 필터 포함</span><span class="sxs-lookup"><span data-stu-id="22165-314">Task 1 - Including the Tracking Filter in the Solution</span></span>

<span data-ttu-id="22165-315">이 작업에서는 추적 이벤트에 사용자 지정 작업 필터를 음악 저장소에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-315">In this task, you will include in the Music Store a custom action filter to trace events.</span></span> <span data-ttu-id="22165-316">사용자 지정 작업 필터 개념은 이전 실습 &quot;사용자 지정 작업 필터&quot;이미 처리 되었으므로이 랩의 자산 폴더에 필터 클래스를 포함 한 다음 Unity 용 필터 공급자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22165-316">As custom action filter concepts are already treated in the previous Lab &quot;Custom Action Filters&quot;, you will just include the filter class from the Assets folder of this lab, and then create a Filter Provider for Unity:</span></span>

1. <span data-ttu-id="22165-317">**Source\ex03-삽입 작업 filter\begin** 폴더에 있는 **시작** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="22165-317">Open the **Begin** solution located in the **Source\Ex03 - Injecting Action Filter\Begin** folder.</span></span> <span data-ttu-id="22165-318">그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-318">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="22165-319">제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-319">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="22165-320">이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-320">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="22165-321">**NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-321">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="22165-322">마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-322">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="22165-323">NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="22165-323">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="22165-324">NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-324">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="22165-325">이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-325">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
      > 
      > <span data-ttu-id="22165-326">자세한 내용은 [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="22165-326">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="22165-327">**TraceActionFilter.cs** 파일을/ssource/cerui> **에 포함** 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-327">Include **TraceActionFilter.cs** file from **/Sources/Assets** to **/Filters** folder.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample18.cs)]

    > [!NOTE]
    > <span data-ttu-id="22165-328">이 사용자 지정 작업 필터는 ASP.NET 추적을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-328">This custom action filter performs ASP.NET tracing.</span></span> <span data-ttu-id="22165-329">자세한 참조는 &quot;ASP.NET MVC 4 로컬 및 동적 작업 필터&quot; Lab을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-329">You can check &quot;ASP.NET MVC 4 local and Dynamic Action Filters&quot; Lab for more reference.</span></span>
3. <span data-ttu-id="22165-330">**FilterProvider.cs** **폴더의** 프로젝트에 빈 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-330">Add the empty class **FilterProvider.cs** to the project in the folder **/Filters.**</span></span>
4. <span data-ttu-id="22165-331">**FilterProvider.cs**에 **system.web** 및 **Microsoft** 의 system.xml 네임 스페이스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-331">Add the **System.Web.Mvc** and **Microsoft.Practices.Unity** namespaces in **FilterProvider.cs**.</span></span>

    <span data-ttu-id="22165-332">(코드 조각- *ASP.NET 종속성 주입 랩-Ex03-네임 스페이스를 추가 하는 필터 공급자*)</span><span class="sxs-lookup"><span data-stu-id="22165-332">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample19.cs)]
5. <span data-ttu-id="22165-333">클래스가 **Ifilterprovider** 인터페이스에서 상속 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-333">Make the class inherit from **IFilterProvider** Interface.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample20.cs)]
6. <span data-ttu-id="22165-334">**Filterprovider** 클래스에서 **Iunitycontainer** 속성을 추가한 다음 클래스 생성자를 만들어 컨테이너를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-334">Add a **IUnityContainer** property in the **FilterProvider** class, and then create a class constructor to assign the container.</span></span>

    <span data-ttu-id="22165-335">(코드 조각- *ASP.NET 종속성 주입 랩-Ex03-필터 공급자 생성자*)</span><span class="sxs-lookup"><span data-stu-id="22165-335">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider Constructor*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample21.cs)]

    > [!NOTE]
    > <span data-ttu-id="22165-336">필터 공급자 클래스 생성자가 내부에 **새** 개체를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-336">The filter provider class constructor is not creating a **new** object inside.</span></span> <span data-ttu-id="22165-337">컨테이너는 매개 변수로 전달 되 고 종속성은 Unity에서 해결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22165-337">The container is passed as a parameter, and the dependency is solved by Unity.</span></span>
7. <span data-ttu-id="22165-338">**Filterprovider** 클래스에서 **ifilterprovider** 인터페이스에서 **getfilters** 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-338">In the **FilterProvider** class, implement the method **GetFilters** from **IFilterProvider** interface.</span></span>

    <span data-ttu-id="22165-339">(코드 조각- *ASP.NET 종속성 주입 랩-Ex03-필터 공급자 GetFilters*)</span><span class="sxs-lookup"><span data-stu-id="22165-339">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider GetFilters*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample22.cs)]

<a id="Ex3Task2"></a>

<a id="Task_2_-_Registering_and_Enabling_the_Filter"></a>
#### <a name="task-2---registering-and-enabling-the-filter"></a><span data-ttu-id="22165-340">작업 2-필터 등록 및 사용</span><span class="sxs-lookup"><span data-stu-id="22165-340">Task 2 - Registering and Enabling the Filter</span></span>

<span data-ttu-id="22165-341">이 작업에서는 사이트 추적을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-341">In this task, you will enable site tracking.</span></span> <span data-ttu-id="22165-342">이렇게 하려면 **Bootstrapper.cs BuildUnityContainer** 메서드에 필터를 등록 하 여 추적을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-342">To do that, you will register the filter in **Bootstrapper.cs BuildUnityContainer** method to start tracing:</span></span>

1. <span data-ttu-id="22165-343">프로젝트 루트에 있는 **web.config** 를 열고 system.web 그룹에서 추적 추적을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-343">Open **Web.config** located in the project root and enable trace tracking at System.Web group.</span></span>

    [!code-xml[Main](aspnet-mvc-4-dependency-injection/samples/sample23.xml)]
2. <span data-ttu-id="22165-344">**Bootstrapper.cs** at 프로젝트 루트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="22165-344">Open **Bootstrapper.cs** at project root.</span></span>
3. <span data-ttu-id="22165-345">**MvcMusicStore** 네임 스페이스에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-345">Add a reference to the **MvcMusicStore.Filters** namespace.</span></span>

    <span data-ttu-id="22165-346">(코드 조각- *ASP.NET 종속성 주입 랩-Ex03-부트스트래퍼 네임 스페이스 추가*)</span><span class="sxs-lookup"><span data-stu-id="22165-346">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Bootstrapper Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample24.cs)]
4. <span data-ttu-id="22165-347">**Buildunitycontainer** 메서드를 선택 하 고 Unity 컨테이너에 필터를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-347">Select the **BuildUnityContainer** method and register the filter in the Unity Container.</span></span> <span data-ttu-id="22165-348">필터 공급자 및 작업 필터를 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-348">You will have to register the filter provider as well as the action filter.</span></span>

    <span data-ttu-id="22165-349">(코드 조각- *ASP.NET 종속성 주입 랩-Ex03-Register FilterProvider 및 ActionFilter*)</span><span class="sxs-lookup"><span data-stu-id="22165-349">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Register FilterProvider and ActionFilter*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample25.cs)]

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="22165-350">작업 3-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="22165-350">Task 3 - Running the Application</span></span>

<span data-ttu-id="22165-351">이 작업에서는 응용 프로그램을 실행 하 고 사용자 지정 작업 필터가 작업을 추적 하는지 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-351">In this task, you will run the application and test that the custom action filter is tracing the activity:</span></span>

1. <span data-ttu-id="22165-352">**F5** 키를 눌러 애플리케이션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-352">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="22165-353">장르 메뉴에서 **바위** 를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-353">Click **Rock** within the Genres Menu.</span></span> <span data-ttu-id="22165-354">원하는 경우 더 많은 장르를 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-354">You can browse to more genres if you want to.</span></span>

    <span data-ttu-id="22165-355">![Music Store](aspnet-mvc-4-dependency-injection/_static/image11.png "Music Store")</span><span class="sxs-lookup"><span data-stu-id="22165-355">![Music Store](aspnet-mvc-4-dependency-injection/_static/image11.png "Music Store")</span></span>

    <span data-ttu-id="22165-356">*Music Store*</span><span class="sxs-lookup"><span data-stu-id="22165-356">*Music Store*</span></span>
3. <span data-ttu-id="22165-357">**/Trace.xml** 로 이동 하 여 응용 프로그램 추적 페이지를 표시 한 다음 **자세히 보기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-357">Browse to **/Trace.axd** to see the Application Trace page, and then click **View Details**.</span></span>

    <span data-ttu-id="22165-358">![응용 프로그램 추적 로그](aspnet-mvc-4-dependency-injection/_static/image12.png "응용 프로그램 추적 로그")</span><span class="sxs-lookup"><span data-stu-id="22165-358">![Application Trace Log](aspnet-mvc-4-dependency-injection/_static/image12.png "Application Trace Log")</span></span>

    <span data-ttu-id="22165-359">*응용 프로그램 추적 로그*</span><span class="sxs-lookup"><span data-stu-id="22165-359">*Application Trace Log*</span></span>

    <span data-ttu-id="22165-360">![응용 프로그램 추적-요청 정보](aspnet-mvc-4-dependency-injection/_static/image13.png "응용 프로그램 추적-요청 정보")</span><span class="sxs-lookup"><span data-stu-id="22165-360">![Application Trace - Request Details](aspnet-mvc-4-dependency-injection/_static/image13.png "Application Trace - Request Details")</span></span>

    <span data-ttu-id="22165-361">*응용 프로그램 추적-요청 정보*</span><span class="sxs-lookup"><span data-stu-id="22165-361">*Application Trace - Request Details*</span></span>
4. <span data-ttu-id="22165-362">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-362">Close the browser.</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="22165-363">요약</span><span class="sxs-lookup"><span data-stu-id="22165-363">Summary</span></span>

<span data-ttu-id="22165-364">이 실습 실습을 완료 하면 NuGet 패키지를 사용 하 여 Unity를 통합 하 여 ASP.NET MVC 4에서 종속성 주입을 사용 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-364">By completing this Hands-On Lab you have learned how to use Dependency Injection in ASP.NET MVC 4 by integrating Unity using a NuGet Package.</span></span> <span data-ttu-id="22165-365">이를 위해 컨트롤러, 뷰 및 작업 필터 내에서 종속성 주입을 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-365">To achieve that, you have used Dependency Injection inside controllers, views and action filters.</span></span>

<span data-ttu-id="22165-366">다음 개념을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-366">The following concepts were covered:</span></span>

- <span data-ttu-id="22165-367">ASP.NET MVC 4 종속성 주입 기능</span><span class="sxs-lookup"><span data-stu-id="22165-367">ASP.NET MVC 4 Dependency Injection features</span></span>
- <span data-ttu-id="22165-368">Mvc3 NuGet 패키지를 사용 하 여 unity 통합</span><span class="sxs-lookup"><span data-stu-id="22165-368">Unity integration using Unity.Mvc3 NuGet Package</span></span>
- <span data-ttu-id="22165-369">컨트롤러의 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="22165-369">Dependency Injection in Controllers</span></span>
- <span data-ttu-id="22165-370">뷰의 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="22165-370">Dependency Injection in Views</span></span>
- <span data-ttu-id="22165-371">작업 필터의 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="22165-371">Dependency injection of Action Filters</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="22165-372">부록 A: 웹에 대 한 Visual Studio Express 2012 설치</span><span class="sxs-lookup"><span data-stu-id="22165-372">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="22165-373">**[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)** 를 사용 하 여 웹 또는 다른 &quot;Express&quot; 버전 **에 대해 Microsoft Visual Studio Express 2012** 를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-373">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="22165-374">다음 지침에서는 *Microsoft 웹 플랫폼 설치 관리자*를 사용 하 여 *Visual studio Express 2012 for Web* 을 설치 하는 데 필요한 단계를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-374">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="22165-375">[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-375">Go to [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="22165-376">또는 웹 플랫폼 설치 관리자를 이미 설치한 경우에는 웹 플랫폼 설치 관리자를 열고 <em>Microsoft AZURE SDK&quot;를 사용 하 여 웹 용 2012 Visual Studio Express</em> &quot;제품을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-376">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="22165-377">**지금 설치**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-377">Click on **Install Now**.</span></span> <span data-ttu-id="22165-378">**웹 플랫폼 설치 관리자** 가 없으면 먼저이를 다운로드 하 여 설치 하도록 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="22165-378">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="22165-379">**웹 플랫폼 설치 관리자** 가 열리면 **설치** 를 클릭 하 여 설치를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-379">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="22165-380">![Visual Studio Express 설치](aspnet-mvc-4-dependency-injection/_static/image14.png "Visual Studio Express 설치")</span><span class="sxs-lookup"><span data-stu-id="22165-380">![Install Visual Studio Express](aspnet-mvc-4-dependency-injection/_static/image14.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="22165-381">*Visual Studio Express 설치*</span><span class="sxs-lookup"><span data-stu-id="22165-381">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="22165-382">모든 제품의 라이선스 및 사용 조건을 읽고 **동의** 함을 클릭 하 여 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-382">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![사용 조건 동의](aspnet-mvc-4-dependency-injection/_static/image15.png)

    <span data-ttu-id="22165-384">*사용 조건 동의*</span><span class="sxs-lookup"><span data-stu-id="22165-384">*Accepting the license terms*</span></span>
5. <span data-ttu-id="22165-385">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="22165-385">Wait until the downloading and installation process completes.</span></span>

    ![설치 진행률](aspnet-mvc-4-dependency-injection/_static/image16.png)

    <span data-ttu-id="22165-387">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="22165-387">*Installation progress*</span></span>
6. <span data-ttu-id="22165-388">설치가 완료 되 면 **마침**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-388">When the installation completes, click **Finish**.</span></span>

    ![설치 완료](aspnet-mvc-4-dependency-injection/_static/image17.png)

    <span data-ttu-id="22165-390">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="22165-390">*Installation completed*</span></span>
7. <span data-ttu-id="22165-391">**끝내기** 를 클릭 하 여 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-391">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="22165-392">웹에 대 한 Visual Studio Express를 열려면 **시작** 화면으로 이동 하 &quot;**VS Express**&quot;작성을 시작한 후 **VS Express for Web** 타일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-392">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 타일](aspnet-mvc-4-dependency-injection/_static/image18.png)

    <span data-ttu-id="22165-394">*VS Express for Web 타일*</span><span class="sxs-lookup"><span data-stu-id="22165-394">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="22165-395">부록 B: 코드 조각 사용</span><span class="sxs-lookup"><span data-stu-id="22165-395">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="22165-396">코드 조각을 사용 하면 필요한 모든 코드를 편리 하 게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-396">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="22165-397">랩 문서는 다음 그림에 표시 된 것 처럼 사용자가 사용할 수 있는 경우를 정확 하 게 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="22165-397">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="22165-398">![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입](aspnet-mvc-4-dependency-injection/_static/image19.png "Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입")</span><span class="sxs-lookup"><span data-stu-id="22165-398">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-dependency-injection/_static/image19.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="22165-399">*Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입*</span><span class="sxs-lookup"><span data-stu-id="22165-399">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="22165-400">***키보드를 사용 하 여 코드 조각을 추가 하려면C# (만 해당)***</span><span class="sxs-lookup"><span data-stu-id="22165-400">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="22165-401">코드를 삽입할 위치에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="22165-401">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="22165-402">조각 이름 (공백 또는 하이픈 제외)을 입력 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-402">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="22165-403">IntelliSense는 일치 하는 코드 조각의 이름을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-403">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="22165-404">올바른 코드 조각을 선택 하거나 전체 코드 조각 이름이 선택 될 때까지 계속 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-404">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="22165-405">Tab 키를 두 번 눌러 커서 위치에 코드 조각을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-405">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="22165-406">![코드 조각 이름 입력 시작](aspnet-mvc-4-dependency-injection/_static/image20.png "코드 조각 이름 입력 시작")</span><span class="sxs-lookup"><span data-stu-id="22165-406">![Start typing the snippet name](aspnet-mvc-4-dependency-injection/_static/image20.png "Start typing the snippet name")</span></span>

<span data-ttu-id="22165-407">*코드 조각 이름 입력 시작*</span><span class="sxs-lookup"><span data-stu-id="22165-407">*Start typing the snippet name*</span></span>

<span data-ttu-id="22165-408">![Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.](aspnet-mvc-4-dependency-injection/_static/image21.png "Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="22165-408">![Press Tab to select the highlighted snippet](aspnet-mvc-4-dependency-injection/_static/image21.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="22165-409">*Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="22165-409">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="22165-410">![Tab 키를 다시 누르면 코드 조각이 확장 됩니다.](aspnet-mvc-4-dependency-injection/_static/image22.png "Tab 키를 다시 누르면 코드 조각이 확장 됩니다.")</span><span class="sxs-lookup"><span data-stu-id="22165-410">![Press Tab again and the snippet will expand](aspnet-mvc-4-dependency-injection/_static/image22.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="22165-411">*Tab 키를 다시 누르면 코드 조각이 확장 됩니다.*</span><span class="sxs-lookup"><span data-stu-id="22165-411">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="22165-412">***마우스C#(, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면*** 1(sp1).</span><span class="sxs-lookup"><span data-stu-id="22165-412">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="22165-413">코드 조각을 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-413">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="22165-414">코드 **조각 삽입** 을 선택한 다음 **내 코드 조각을**선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-414">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="22165-415">목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="22165-415">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="22165-416">![코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.](aspnet-mvc-4-dependency-injection/_static/image23.png "코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="22165-416">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-dependency-injection/_static/image23.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="22165-417">*코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="22165-417">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="22165-418">![목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.](aspnet-mvc-4-dependency-injection/_static/image24.png "목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="22165-418">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-dependency-injection/_static/image24.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="22165-419">*목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="22165-419">*Pick the relevant snippet from the list, by clicking on it*</span></span>
