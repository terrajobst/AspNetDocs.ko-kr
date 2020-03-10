---
uid: web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
title: 유닛 테스트 ASP.NET Web API 2 | Entity Framework 모의 Microsoft Docs
author: Rick-Anderson
description: 이 지침 및 응용 프로그램에서는 Entity Framework를 사용 하는 Web API 2 응용 프로그램에 대 한 단위 테스트를 만드는 방법을 보여 줍니다. 다음을 수정 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 12/13/2013
ms.assetid: cd844025-ccad-41ce-8694-595f1022a49f
msc.legacyurl: /web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 258450107ee7443c4efd43a3b8e4851249745227
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447089"
---
# <a name="mocking-entity-framework-when-unit-testing-aspnet-web-api-2"></a><span data-ttu-id="c6ffa-104">유닛 테스트 ASP.NET Web API 2 Entity Framework 모의</span><span class="sxs-lookup"><span data-stu-id="c6ffa-104">Mocking Entity Framework when Unit Testing ASP.NET Web API 2</span></span>

<span data-ttu-id="c6ffa-105">만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="c6ffa-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[<span data-ttu-id="c6ffa-106">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="c6ffa-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> <span data-ttu-id="c6ffa-107">이 지침 및 응용 프로그램에서는 Entity Framework를 사용 하는 Web API 2 응용 프로그램에 대 한 단위 테스트를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-107">This guidance and application demonstrate how to create unit tests for your Web API 2 application that uses the Entity Framework.</span></span> <span data-ttu-id="c6ffa-108">스 캐 폴드 컨트롤러를 수정 하 여 테스트를 위해 컨텍스트 개체를 전달할 수 있도록 하는 방법과 Entity Framework 작업 하는 테스트 개체를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-108">It shows how to modify the scaffolded controller to enable passing a context object for testing, and how to create test objects that work with Entity Framework.</span></span>
>
> <span data-ttu-id="c6ffa-109">ASP.NET Web API를 사용한 단위 테스트에 대 한 소개는 [ASP.NET Web API 2를 사용한 단위 테스트](unit-testing-with-aspnet-web-api.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-109">For an introduction to unit testing with ASP.NET Web API, see [Unit Testing with ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md).</span></span>
>
> <span data-ttu-id="c6ffa-110">이 자습서에서는 사용자가 ASP.NET Web API의 기본 개념을 잘 알고 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-110">This tutorial assumes you are familiar with the basic concepts of ASP.NET Web API.</span></span> <span data-ttu-id="c6ffa-111">소개 자습서는 [ASP.NET Web API 2 시작](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-111">For an introductory tutorial, see [Getting Started with ASP.NET Web API 2](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="c6ffa-112">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="c6ffa-112">Software versions used in the tutorial</span></span>
>
> - [<span data-ttu-id="c6ffa-113">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="c6ffa-113">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="c6ffa-114">Web API 2</span><span class="sxs-lookup"><span data-stu-id="c6ffa-114">Web API 2</span></span>

## <a name="in-this-topic"></a><span data-ttu-id="c6ffa-115">항목 내용</span><span class="sxs-lookup"><span data-stu-id="c6ffa-115">In this topic</span></span>

<span data-ttu-id="c6ffa-116">이 항목에는 다음과 같은 섹션이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="c6ffa-117">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="c6ffa-117">Prerequisites</span></span>](#prereqs)
- [<span data-ttu-id="c6ffa-118">코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="c6ffa-118">Download code</span></span>](#download)
- [<span data-ttu-id="c6ffa-119">단위 테스트 프로젝트를 사용 하 여 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="c6ffa-119">Create application with unit test project</span></span>](#appwithunittest)
- [<span data-ttu-id="c6ffa-120">모델 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="c6ffa-120">Create the model class</span></span>](#modelclass)
- [<span data-ttu-id="c6ffa-121">컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="c6ffa-121">Add the controller</span></span>](#controller)
- [<span data-ttu-id="c6ffa-122">종속성 주입 추가</span><span class="sxs-lookup"><span data-stu-id="c6ffa-122">Add dependency injection</span></span>](#dependency)
- [<span data-ttu-id="c6ffa-123">테스트 프로젝트에 NuGet 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="c6ffa-123">Install NuGet packages in test project</span></span>](#testpackages)
- [<span data-ttu-id="c6ffa-124">테스트 컨텍스트 만들기</span><span class="sxs-lookup"><span data-stu-id="c6ffa-124">Create test context</span></span>](#testcontext)
- [<span data-ttu-id="c6ffa-125">테스트 만들기</span><span class="sxs-lookup"><span data-stu-id="c6ffa-125">Create tests</span></span>](#tests)
- [<span data-ttu-id="c6ffa-126">테스트 실행</span><span class="sxs-lookup"><span data-stu-id="c6ffa-126">Run tests</span></span>](#runtests)

<span data-ttu-id="c6ffa-127">[ASP.NET Web API 2를 사용 하 여 단위 테스트](unit-testing-with-aspnet-web-api.md)의 단계를 이미 완료 한 경우에는 [컨트롤러 추가](#controller)섹션으로 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-127">If you have already completed the steps in [Unit Testing with ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md), you can skip to the section [Add the controller](#controller).</span></span>

<a id="prereqs"></a>
## <a name="prerequisites"></a><span data-ttu-id="c6ffa-128">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="c6ffa-128">Prerequisites</span></span>

<span data-ttu-id="c6ffa-129">Visual Studio 2017 Community, Professional 또는 Enterprise edition</span><span class="sxs-lookup"><span data-stu-id="c6ffa-129">Visual Studio 2017 Community, Professional or Enterprise edition</span></span>

<a id="download"></a>
## <a name="download-code"></a><span data-ttu-id="c6ffa-130">코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="c6ffa-130">Download code</span></span>

<span data-ttu-id="c6ffa-131">완료 된 [프로젝트](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-131">Download the [completed project](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11).</span></span> <span data-ttu-id="c6ffa-132">다운로드 가능한 프로젝트에는이 항목에 대 한 단위 테스트 코드와 [단위 테스트 ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md) 항목 항목이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-132">The downloadable project includes unit test code for this topic and for the [Unit Testing ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md) topic.</span></span>

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a><span data-ttu-id="c6ffa-133">단위 테스트 프로젝트를 사용 하 여 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="c6ffa-133">Create application with unit test project</span></span>

<span data-ttu-id="c6ffa-134">응용 프로그램을 만들거나 기존 응용 프로그램에 단위 테스트 프로젝트를 추가할 때 단위 테스트 프로젝트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-134">You can either create a unit test project when creating your application or add a unit test project to an existing application.</span></span> <span data-ttu-id="c6ffa-135">이 자습서에서는 응용 프로그램을 만들 때 단위 테스트 프로젝트를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-135">This tutorial shows creating a unit test project when creating the application.</span></span>

<span data-ttu-id="c6ffa-136">ASP.NET **app**이라는 새 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-136">Create a new ASP.NET Web Application named **StoreApp**.</span></span>

<span data-ttu-id="c6ffa-137">새 ASP.NET 프로젝트 창에서 **빈** 템플릿을 선택 하 고 Web API에 대 한 폴더 및 핵심 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-137">In the New ASP.NET Project windows, select the **Empty** template and add folders and core references for Web API.</span></span> <span data-ttu-id="c6ffa-138">**단위 테스트 추가** 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-138">Select the **Add unit tests** option.</span></span> <span data-ttu-id="c6ffa-139">단위 테스트 프로젝트는 자동 **으로 이름이로 지정 됩니다.**</span><span class="sxs-lookup"><span data-stu-id="c6ffa-139">The unit test project is automatically named **StoreApp.Tests**.</span></span> <span data-ttu-id="c6ffa-140">이 이름을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-140">You can keep this name.</span></span>

![단위 테스트 프로젝트 만들기](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image1.png)

<span data-ttu-id="c6ffa-142">응용 프로그램을 만든 후에는 해당 응용 프로그램에 두 개의 **프로젝트를 포함** 하는 것을 볼 수 **있습니다.**</span><span class="sxs-lookup"><span data-stu-id="c6ffa-142">After creating the application, you will see it contains two projects - **StoreApp** and **StoreApp.Tests**.</span></span>

<a id="modelclass"></a>
## <a name="create-the-model-class"></a><span data-ttu-id="c6ffa-143">모델 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="c6ffa-143">Create the model class</span></span>

<span data-ttu-id="c6ffa-144">사용자 응용 프로그램 프로젝트에서 **Product.cs**라는 **모델** 폴더에 클래스 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-144">In your StoreApp project, add a class file to the **Models** folder named **Product.cs**.</span></span> <span data-ttu-id="c6ffa-145">파일 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-145">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample1.cs)]

<span data-ttu-id="c6ffa-146">솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-146">Build the solution.</span></span>

<a id="controller"></a>
## <a name="add-the-controller"></a><span data-ttu-id="c6ffa-147">컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="c6ffa-147">Add the controller</span></span>

<span data-ttu-id="c6ffa-148">Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** 및 **새 스 캐 폴드 항목**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-148">Right-click the Controllers folder and select **Add** and **New Scaffolded Item**.</span></span> <span data-ttu-id="c6ffa-149">Entity Framework를 사용 하 여 작업을 포함 하는 Web API 2 컨트롤러를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-149">Select Web API 2 Controller with actions, using Entity Framework.</span></span>

![새 컨트롤러 추가](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image2.png)

<span data-ttu-id="c6ffa-151">다음 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-151">Set the following values:</span></span>

- <span data-ttu-id="c6ffa-152">컨트롤러 이름: **제품 컨트롤러**</span><span class="sxs-lookup"><span data-stu-id="c6ffa-152">Controller name: **ProductController**</span></span>
- <span data-ttu-id="c6ffa-153">모델 클래스: **Product**</span><span class="sxs-lookup"><span data-stu-id="c6ffa-153">Model class: **Product**</span></span>
- <span data-ttu-id="c6ffa-154">데이터 컨텍스트 클래스: [아래에 표시 된 값을 채우는 **새 데이터 컨텍스트** 단추 선택]</span><span class="sxs-lookup"><span data-stu-id="c6ffa-154">Data context class: [Select **New data context** button which fills in the values seen below]</span></span>

![컨트롤러 지정](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image3.png)

<span data-ttu-id="c6ffa-156">**추가** 를 클릭 하 여 자동으로 생성 된 코드를 사용 하 여 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-156">Click **Add** to create the controller with automatically-generated code.</span></span> <span data-ttu-id="c6ffa-157">이 코드에는 Product 클래스의 인스턴스를 만들고, 검색 하 고, 업데이트 하 고, 삭제 하는 메서드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-157">The code includes methods for creating, retrieving, updating and deleting instances of the Product class.</span></span> <span data-ttu-id="c6ffa-158">다음 코드는 제품을 추가 하는 메서드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-158">The following code shows the method for add a Product.</span></span> <span data-ttu-id="c6ffa-159">이 메서드는 **IHttpActionResult**의 인스턴스를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-159">Notice that the method returns an instance of **IHttpActionResult**.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample2.cs)]

<span data-ttu-id="c6ffa-160">IHttpActionResult는 Web API 2의 새로운 기능 중 하나로, 단위 테스트 개발을 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-160">IHttpActionResult is one of the new features in Web API 2, and it simplifies unit test development.</span></span>

<span data-ttu-id="c6ffa-161">다음 섹션에서는 테스트 개체를 컨트롤러에 전달 하는 데 도움이 되도록 생성 된 코드를 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-161">In the next section, you will customize the generated code to facilitate passing test objects to the controller.</span></span>

<a id="dependency"></a>
## <a name="add-dependency-injection"></a><span data-ttu-id="c6ffa-162">종속성 주입 추가</span><span class="sxs-lookup"><span data-stu-id="c6ffa-162">Add dependency injection</span></span>

<span data-ttu-id="c6ffa-163">현재, 제품 컨트롤러 클래스는 하드 코드 되어 있으므로이 클래스의 인스턴스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-163">Currently, the ProductController class is hard-coded to use an instance of the StoreAppContext class.</span></span> <span data-ttu-id="c6ffa-164">종속성 주입 이라고 하는 패턴을 사용 하 여 응용 프로그램을 수정 하 고 하드 코드 된 종속성을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-164">You will use a pattern called dependency injection to modify your application and remove that hard-coded dependency.</span></span> <span data-ttu-id="c6ffa-165">이 종속성을 위반 하면 테스트할 때 모의 개체를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-165">By breaking this dependency, you can pass in a mock object when testing.</span></span>

<span data-ttu-id="c6ffa-166">**모델** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **IStoreAppContext**이라는 새 인터페이스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-166">Right-click the **Models** folder, and add a new interface named **IStoreAppContext**.</span></span>

<span data-ttu-id="c6ffa-167">코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-167">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample3.cs)]

<span data-ttu-id="c6ffa-168">StoreAppContext.cs 파일을 열고 다음과 같이 강조 표시를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-168">Open the StoreAppContext.cs file and make the following highlighted changes.</span></span> <span data-ttu-id="c6ffa-169">유의 해야 할 중요 한 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-169">The important changes to note are:</span></span>

- <span data-ttu-id="c6ffa-170">IStoreAppContext Appcontext 클래스는 인터페이스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-170">StoreAppContext class implements IStoreAppContext interface</span></span>
- <span data-ttu-id="c6ffa-171">MarkAsModified 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-171">MarkAsModified method is implemented</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample4.cs?highlight=6,14-17)]

<span data-ttu-id="c6ffa-172">ProductController.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-172">Open the ProductController.cs file.</span></span> <span data-ttu-id="c6ffa-173">강조 표시 된 코드와 일치 하도록 기존 코드를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-173">Change the existing code to match the highlighted code.</span></span> <span data-ttu-id="c6ffa-174">이러한 변경 내용으로 인해에는가 나 Appcontext에 대 한 종속성이 중단 되 고 다른 클래스가 컨텍스트 클래스에 대해 다른 개체를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-174">These changes break the dependency on StoreAppContext and enable other classes to pass in a different object for the context class.</span></span> <span data-ttu-id="c6ffa-175">이렇게 변경 하면 단위 테스트 중에 테스트 컨텍스트를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-175">This change will enable you to pass in a test context during unit tests.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample5.cs?highlight=4,7-12)]

<span data-ttu-id="c6ffa-176">제품 컨트롤러에서 수행 해야 하는 변경 내용이 하나 더 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-176">There is one more change you must make in ProductController.</span></span> <span data-ttu-id="c6ffa-177">**Putproduct** 메서드에서 엔터티 상태를 설정 하는 줄을 MarkAsModified 메서드에 대 한 호출로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-177">In the **PutProduct** method, replace the line that sets the entity state to modified with a call to the MarkAsModified method.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample6.cs?highlight=14-15)]

<span data-ttu-id="c6ffa-178">솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-178">Build the solution.</span></span>

<span data-ttu-id="c6ffa-179">이제 테스트 프로젝트를 설정할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-179">You are now ready to set up the test project.</span></span>

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a><span data-ttu-id="c6ffa-180">테스트 프로젝트에 NuGet 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="c6ffa-180">Install NuGet packages in test project</span></span>

<span data-ttu-id="c6ffa-181">빈 템플릿을 사용 하 여 응용 프로그램을 만드는 경우 단위 테스트 프로젝트 (사용자 응용 프로그램 테스트)에는 설치 된 NuGet 패키지가 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-181">When you use the Empty template to create an application, the unit test project (StoreApp.Tests) does not include any installed NuGet packages.</span></span> <span data-ttu-id="c6ffa-182">Web API 템플릿과 같은 다른 템플릿에는 단위 테스트 프로젝트의 일부 NuGet 패키지가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-182">Other templates, such as the Web API template, include some NuGet packages in the unit test project.</span></span> <span data-ttu-id="c6ffa-183">이 자습서에서는 Entity Framework 패키지와 Microsoft ASP.NET Web API 2 Core 패키지를 테스트 프로젝트에 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-183">For this tutorial, you must include the Entity Framework package and the Microsoft ASP.NET Web API 2 Core package to the test project.</span></span>

<span data-ttu-id="c6ffa-184">마우스 오른쪽 단추를 클릭 하 여 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-184">Right-click the StoreApp.Tests project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="c6ffa-185">해당 프로젝트에 패키지를 추가 하려면 사용자 응용 프로그램. 테스트 프로젝트를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-185">You must select the StoreApp.Tests project to add the packages to that project.</span></span>

![패키지 관리](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image4.png)

<span data-ttu-id="c6ffa-187">온라인 패키지에서 EntityFramework 패키지 (버전 6.0 이상)를 찾아서 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-187">From the Online packages, find and install the EntityFramework package (version 6.0 or later).</span></span> <span data-ttu-id="c6ffa-188">EntityFramework 패키지가 이미 설치 된 것으로 나타나는 경우에는 사용자 응용 프로그램 프로젝트 대신 파일 앱 프로젝트를 선택 했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-188">If it appears that the EntityFramework package is already installed, you may have selected the StoreApp project instead of the StoreApp.Tests project.</span></span>

![add Entity Framework](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image5.png)

<span data-ttu-id="c6ffa-190">Microsoft ASP.NET Web API 2 핵심 패키지를 찾아서 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-190">Find and install Microsoft ASP.NET Web API 2 Core package.</span></span>

![web api core 패키지 설치](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image6.png)

<span data-ttu-id="c6ffa-192">NuGet 패키지 관리 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-192">Close the Manage NuGet Packages window.</span></span>

<a id="testcontext"></a>
## <a name="create-test-context"></a><span data-ttu-id="c6ffa-193">테스트 컨텍스트 만들기</span><span class="sxs-lookup"><span data-stu-id="c6ffa-193">Create test context</span></span>

<span data-ttu-id="c6ffa-194">**Testdbset** 이라는 클래스를 테스트 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-194">Add a class named **TestDbSet** to the test project.</span></span> <span data-ttu-id="c6ffa-195">이 클래스는 테스트 데이터 집합에 대 한 기본 클래스로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-195">This class serves as the base class for your test data set.</span></span> <span data-ttu-id="c6ffa-196">코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-196">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample7.cs)]

<span data-ttu-id="c6ffa-197">다음 코드를 포함 하는 테스트 프로젝트에 **Testproductdbset** 이라는 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-197">Add a class named **TestProductDbSet** to the test project which contains the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample8.cs)]

<span data-ttu-id="c6ffa-198">**Teststoreappcontext** 라는 클래스를 추가 하 고 기존 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-198">Add a class named **TestStoreAppContext** and replace the existing code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample9.cs)]

<a id="tests"></a>
## <a name="create-tests"></a><span data-ttu-id="c6ffa-199">테스트 만들기</span><span class="sxs-lookup"><span data-stu-id="c6ffa-199">Create tests</span></span>

<span data-ttu-id="c6ffa-200">기본적으로 테스트 프로젝트에는 **UnitTest1.cs**라는 빈 테스트 파일이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-200">By default, your test project includes an empty test file named **UnitTest1.cs**.</span></span> <span data-ttu-id="c6ffa-201">이 파일은 테스트 메서드를 만드는 데 사용 하는 특성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-201">This file shows the attributes you use to create test methods.</span></span> <span data-ttu-id="c6ffa-202">이 자습서에서는 새 테스트 클래스를 추가 하기 때문에이 파일을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-202">For this tutorial, you can delete this file because you will add a new test class.</span></span>

<span data-ttu-id="c6ffa-203">**Test제품 컨트롤러** 라는 클래스를 테스트 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-203">Add a class named **TestProductController** to the test project.</span></span> <span data-ttu-id="c6ffa-204">코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-204">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample10.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a><span data-ttu-id="c6ffa-205">테스트 실행</span><span class="sxs-lookup"><span data-stu-id="c6ffa-205">Run tests</span></span>

<span data-ttu-id="c6ffa-206">이제 테스트를 실행할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-206">You are now ready to run the tests.</span></span> <span data-ttu-id="c6ffa-207">**TestMethod** 특성으로 표시 된 모든 메서드는 테스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-207">All of the method that are marked with the **TestMethod** attribute will be tested.</span></span> <span data-ttu-id="c6ffa-208">**테스트** 메뉴 항목에서 테스트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-208">From the **Test** menu item, run the tests.</span></span>

![테스트 실행](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image7.png)

<span data-ttu-id="c6ffa-210">**테스트 탐색기** 창을 열고 테스트 결과를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6ffa-210">Open the **Test Explorer** window, and notice the results of the tests.</span></span>

![테스트 결과](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image8.png)
