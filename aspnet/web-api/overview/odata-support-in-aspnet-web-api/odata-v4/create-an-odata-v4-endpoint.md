---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
title: ASP.NET Web API 2.2를 사용 하 여 OData v4 엔드포인트 만들기 Microsoft Docs
author: MikeWasson
description: OData (Open Data Protocol)는 웹에 대 한 데이터 액세스 프로토콜입니다. OData는 CRUD 작업을 통해 데이터 집합을 쿼리하고 조작 하는 일관 된 방법을 제공 합니다.
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 1e1927c0-ded1-4752-80fd-a146628d2f09
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
msc.type: authoredcontent
ms.openlocfilehash: 81d134cbd3231b9a0d5537ccbd1bbfe6419254af
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484499"
---
# <a name="create-an-odata-v4-endpoint-using-aspnet-web-api"></a><span data-ttu-id="23dcb-104">ASP.NET Web API를 사용 하 여 OData v4 엔드포인트 만들기</span><span class="sxs-lookup"><span data-stu-id="23dcb-104">Create an OData v4 Endpoint Using ASP.NET Web API</span></span> 

> <span data-ttu-id="23dcb-105">OData (Open Data Protocol)는 웹에 대 한 데이터 액세스 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-105">The Open Data Protocol (OData) is a data access protocol for the web.</span></span> <span data-ttu-id="23dcb-106">OData는 CRUD 작업 (만들기, 읽기, 업데이트 및 삭제)을 통해 데이터 집합을 쿼리하고 조작 하는 일관 된 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-106">OData provides a uniform way to query and manipulate data sets through CRUD operations (create, read, update, and delete).</span></span>
>
> <span data-ttu-id="23dcb-107">ASP.NET Web API는 프로토콜의 v3 및 v4를 모두 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-107">ASP.NET Web API supports both v3 and v4 of the protocol.</span></span> <span data-ttu-id="23dcb-108">V3 끝점과 side-by-side 끝점을 함께 실행 하는 v4 끝점을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-108">You can even have a v4 endpoint that runs side-by-side with a v3 endpoint.</span></span>
>
> <span data-ttu-id="23dcb-109">이 자습서에서는 CRUD 작업을 지 원하는 OData v4 끝점을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-109">This tutorial shows how to create an OData v4 endpoint that supports CRUD operations.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="23dcb-110">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="23dcb-110">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="23dcb-111">웹 API 5.2</span><span class="sxs-lookup"><span data-stu-id="23dcb-111">Web API 5.2</span></span>
> - <span data-ttu-id="23dcb-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="23dcb-112">OData v4</span></span>
> - <span data-ttu-id="23dcb-113">Visual Studio 2017 (Visual [studio 2017 다운로드](https://visualstudio.microsoft.com/downloads/))</span><span class="sxs-lookup"><span data-stu-id="23dcb-113">Visual Studio 2017 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/))</span></span>
> - <span data-ttu-id="23dcb-114">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="23dcb-114">Entity Framework 6</span></span>
> - <span data-ttu-id="23dcb-115">.NET 4.7.2</span><span class="sxs-lookup"><span data-stu-id="23dcb-115">.NET 4.7.2</span></span>
>
> ## <a name="tutorial-versions"></a><span data-ttu-id="23dcb-116">자습서 버전</span><span class="sxs-lookup"><span data-stu-id="23dcb-116">Tutorial versions</span></span>
>
> <span data-ttu-id="23dcb-117">OData 버전 3의 경우 [odata V3 끝점 만들기](../odata-v3/creating-an-odata-endpoint.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="23dcb-117">For the OData Version 3, see [Creating an OData v3 Endpoint](../odata-v3/creating-an-odata-endpoint.md).</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="23dcb-118">Visual Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="23dcb-118">Create the Visual Studio Project</span></span>

<span data-ttu-id="23dcb-119">Visual Studio의 **파일** 메뉴에서 **새로 만들기** &gt; **프로젝트**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-119">In Visual Studio, from the **File** menu, select **New** &gt; **Project**.</span></span>

<span data-ttu-id="23dcb-120">**설치** &gt;  **C# Visual** &gt; **web**을 확장 하 고 **.NET Framework (ASP.NET Web Application)** 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-120">Expand **Installed** &gt; **Visual C#** &gt; **Web**, and select the **ASP.NET Web Application (.NET Framework)** template.</span></span> <span data-ttu-id="23dcb-121">Project &quot;제품 서비스&quot;에 이름을로 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-121">Name the project &quot;ProductService&quot;.</span></span>

[![](create-an-odata-v4-endpoint/_static/image7.png)](create-an-odata-v4-endpoint/_static/image7.png)

<span data-ttu-id="23dcb-122">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-122">Select **OK**.</span></span>

[![](create-an-odata-v4-endpoint/_static/image8.png)](create-an-odata-v4-endpoint/_static/image8.png)

<span data-ttu-id="23dcb-123">**비어 있는** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-123">Select the **Empty** template.</span></span> <span data-ttu-id="23dcb-124">**다음에 대 한 폴더 및 핵심 참조 추가:** 에서 **Web API**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-124">Under **Add folders and core references for:**, select **Web API**.</span></span> <span data-ttu-id="23dcb-125">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-125">Select **OK**.</span></span>

## <a name="install-the-odata-packages"></a><span data-ttu-id="23dcb-126">OData 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="23dcb-126">Install the OData packages</span></span>

<span data-ttu-id="23dcb-127">**도구** 메뉴에서 **NuGet 패키지 관리자** &gt; **패키지 관리자 콘솔**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-127">From the **Tools** menu, select **NuGet Package Manager** &gt; **Package Manager Console**.</span></span> <span data-ttu-id="23dcb-128">패키지 관리자 콘솔 창에서 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-128">In the Package Manager Console window, type:</span></span>

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample1.cmd)]

<span data-ttu-id="23dcb-129">이 명령은 최신 OData NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-129">This command installs the latest OData NuGet packages.</span></span>

## <a name="add-a-model-class"></a><span data-ttu-id="23dcb-130">모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="23dcb-130">Add a model class</span></span>

<span data-ttu-id="23dcb-131">*모델* 은 응용 프로그램의 데이터 엔터티를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-131">A *model* is an object that represents a data entity in your application.</span></span>

<span data-ttu-id="23dcb-132">솔루션 탐색기에서 Models 폴더를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-132">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="23dcb-133">상황에 맞는 메뉴에서 &gt; **클래스** **추가** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-133">From the context menu, select **Add** &gt; **Class**.</span></span>

[![](create-an-odata-v4-endpoint/_static/image6.png)](create-an-odata-v4-endpoint/_static/image5.png)

> [!NOTE]
> <span data-ttu-id="23dcb-134">규칙에 따라 모델 클래스는 모델 폴더에 배치 되지만 사용자 고유의 프로젝트에서이 규칙을 따르지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-134">By convention, model classes are placed in the Models folder, but you don't have to follow this convention in your own projects.</span></span>

<span data-ttu-id="23dcb-135">클래스 `Product` 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-135">Name the class `Product`.</span></span> <span data-ttu-id="23dcb-136">Product.cs 파일에서 상용구 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-136">In the Product.cs file, replace the boilerplate code with the following:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample2.cs)]

<span data-ttu-id="23dcb-137">`Id` 속성은 엔터티 키입니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-137">The `Id` property is the entity key.</span></span> <span data-ttu-id="23dcb-138">클라이언트는 키를 기준으로 엔터티를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-138">Clients can query entities by key.</span></span> <span data-ttu-id="23dcb-139">예를 들어 ID가 5 인 제품을 가져오려면 URI가 `/Products(5)`됩니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-139">For example, to get the product with ID of 5, the URI is `/Products(5)`.</span></span> <span data-ttu-id="23dcb-140">또한 `Id` 속성은 백 엔드 데이터베이스의 기본 키가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-140">The `Id` property will also be the primary key in the back-end database.</span></span>

## <a name="enable-entity-framework"></a><span data-ttu-id="23dcb-141">Entity Framework 사용</span><span class="sxs-lookup"><span data-stu-id="23dcb-141">Enable Entity Framework</span></span>

<span data-ttu-id="23dcb-142">이 자습서에서는 EF (Entity Framework) Code First를 사용 하 여 백 엔드 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-142">For this tutorial, we'll use Entity Framework (EF) Code First to create the back-end database.</span></span>

> [!NOTE]
> <span data-ttu-id="23dcb-143">Web API OData에는 EF가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-143">Web API OData does not require EF.</span></span> <span data-ttu-id="23dcb-144">데이터베이스 엔터티를 모델로 변환할 수 있는 모든 데이터 액세스 계층을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-144">Use any data-access layer that can translate database entities into models.</span></span>

<span data-ttu-id="23dcb-145">먼저 EF 용 NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-145">First, install the NuGet package for EF.</span></span> <span data-ttu-id="23dcb-146">**도구** 메뉴에서 **NuGet 패키지 관리자** &gt; **패키지 관리자 콘솔**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-146">From the **Tools** menu, select **NuGet Package Manager** &gt; **Package Manager Console**.</span></span> <span data-ttu-id="23dcb-147">패키지 관리자 콘솔 창에서 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-147">In the Package Manager Console window, type:</span></span>

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample3.cmd)]

<span data-ttu-id="23dcb-148">Web.config 파일을 열고 **구성** 요소 내의 **configsections** 요소 뒤에 다음 섹션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-148">Open the Web.config file, and add the following section inside the **configuration** element, after the **configSections** element.</span></span>

[!code-xml[Main](create-an-odata-v4-endpoint/samples/sample4.xml?highlight=6)]

<span data-ttu-id="23dcb-149">이 설정은 LocalDB 데이터베이스에 대 한 연결 문자열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-149">This setting adds a connection string for a LocalDB database.</span></span> <span data-ttu-id="23dcb-150">이 데이터베이스는 응용 프로그램을 로컬로 실행할 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-150">This database will be used when you run the app locally.</span></span>

<span data-ttu-id="23dcb-151">그런 다음 `ProductsContext` 라는 클래스를 모델 폴더에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-151">Next, add a class named `ProductsContext` to the Models folder:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample5.cs)]

<span data-ttu-id="23dcb-152">생성자에서 `"name=ProductsContext"` 연결 문자열의 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-152">In the constructor, `"name=ProductsContext"` gives the name of the connection string.</span></span>

## <a name="configure-the-odata-endpoint"></a><span data-ttu-id="23dcb-153">OData 끝점 구성</span><span class="sxs-lookup"><span data-stu-id="23dcb-153">Configure the OData endpoint</span></span>

<span data-ttu-id="23dcb-154">File App\_Start/WebApiConfig .cs를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-154">Open the file App\_Start/WebApiConfig.cs.</span></span> <span data-ttu-id="23dcb-155">다음 **using** 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-155">Add the following **using** statements:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample6.cs)]

<span data-ttu-id="23dcb-156">그런 다음 **Register** 메서드에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-156">Then add the following code to the **Register** method:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample7.cs)]

<span data-ttu-id="23dcb-157">이 코드는 다음 두 가지 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-157">This code does two things:</span></span>

- <span data-ttu-id="23dcb-158">EDM (엔터티 데이터 모델)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-158">Creates an Entity Data Model (EDM).</span></span>
- <span data-ttu-id="23dcb-159">경로를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-159">Adds a route.</span></span>

<span data-ttu-id="23dcb-160">EDM은 데이터의 추상 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-160">An EDM is an abstract model of the data.</span></span> <span data-ttu-id="23dcb-161">EDM은 서비스 메타 데이터 문서를 만드는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-161">The EDM is used to create the service metadata document.</span></span> <span data-ttu-id="23dcb-162">**ODataConventionModelBuilder** 클래스는 기본 명명 규칙을 사용 하 여 EDM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-162">The **ODataConventionModelBuilder** class creates an EDM by using default naming conventions.</span></span> <span data-ttu-id="23dcb-163">이 방법에는 최소한의 코드가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-163">This approach requires the least code.</span></span> <span data-ttu-id="23dcb-164">EDM을 보다 세부적으로 제어 하려는 경우 **만드는** 클래스를 사용 하 여 속성, 키 및 탐색 속성을 명시적으로 추가 하 여 edm을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-164">If you want more control over the EDM, you can use the **ODataModelBuilder** class to create the EDM by adding properties, keys, and navigation properties explicitly.</span></span>

<span data-ttu-id="23dcb-165">*경로* 는 HTTP 요청을 끝점으로 라우팅하는 방법을 웹 API에 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-165">A *route* tells Web API how to route HTTP requests to the endpoint.</span></span> <span data-ttu-id="23dcb-166">OData v4 경로를 만들려면 **MapODataServiceRoute** 확장 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-166">To create an OData v4 route, call the **MapODataServiceRoute** extension method.</span></span>

<span data-ttu-id="23dcb-167">응용 프로그램에 여러 OData 끝점이 있는 경우 각각에 대해 별도의 경로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-167">If your application has multiple OData endpoints, create a separate route for each.</span></span> <span data-ttu-id="23dcb-168">각 경로에 고유한 경로 이름 및 접두사를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-168">Give each route a unique route name and prefix.</span></span>

## <a name="add-the-odata-controller"></a><span data-ttu-id="23dcb-169">OData 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="23dcb-169">Add the OData controller</span></span>

<span data-ttu-id="23dcb-170">*컨트롤러* 는 HTTP 요청을 처리 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-170">A *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="23dcb-171">OData 서비스의 각 엔터티 집합에 대해 별도의 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-171">You create a separate controller for each entity set in your OData service.</span></span> <span data-ttu-id="23dcb-172">이 자습서에서는 `Product` 엔터티에 대해 하나의 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-172">In this tutorial, you will create one controller, for the `Product` entity.</span></span>

<span data-ttu-id="23dcb-173">솔루션 탐색기에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 &gt; **클래스** **추가** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-173">In Solution Explorer, right-click the Controllers folder and select **Add** &gt; **Class**.</span></span> <span data-ttu-id="23dcb-174">클래스 `ProductsController` 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-174">Name the class `ProductsController`.</span></span>

> [!NOTE]
> <span data-ttu-id="23dcb-175">OData v3에 대 한이 자습서 버전은 컨트롤러 스 캐 폴딩 **추가** 를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-175">The version of this tutorial for OData v3 uses the **Add Controller** scaffolding.</span></span> <span data-ttu-id="23dcb-176">현재 OData v4에 대 한 스 캐 폴딩이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-176">Currently, there is no scaffolding for OData v4.</span></span>

<span data-ttu-id="23dcb-177">ProductsController.cs의 상용구 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-177">Replace the boilerplate code in ProductsController.cs with the following.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample8.cs)]

<span data-ttu-id="23dcb-178">컨트롤러는 `ProductsContext` 클래스를 사용 하 여 EF를 사용 하 여 데이터베이스에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-178">The controller uses the `ProductsContext` class to access the database using EF.</span></span> <span data-ttu-id="23dcb-179">컨트롤러는 **dispose** 메서드를 재정의 하 여 **ProductsContext**을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-179">Notice that the controller overrides the **Dispose** method to dispose of the **ProductsContext**.</span></span>

<span data-ttu-id="23dcb-180">컨트롤러의 시작 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-180">This is the starting point for the controller.</span></span> <span data-ttu-id="23dcb-181">다음으로 모든 CRUD 작업에 대 한 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-181">Next, we'll add methods for all of the CRUD operations.</span></span>

## <a name="query-the-entity-set"></a><span data-ttu-id="23dcb-182">엔터티 집합 쿼리</span><span class="sxs-lookup"><span data-stu-id="23dcb-182">Query the entity set</span></span>

<span data-ttu-id="23dcb-183">`ProductsController`에 다음 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-183">Add the following methods to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample9.cs)]

<span data-ttu-id="23dcb-184">매개 변수가 없는 `Get` 메서드의 버전은 전체 Products 컬렉션을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-184">The parameterless version of the `Get` method returns the entire Products collection.</span></span> <span data-ttu-id="23dcb-185">*키* 매개 변수가 있는 `Get` 메서드는 해당 키를 사용 하 여 제품을 찾습니다 (이 경우에는 `Id` 속성).</span><span class="sxs-lookup"><span data-stu-id="23dcb-185">The `Get` method with a *key* parameter looks up a product by its key (in this case, the `Id` property).</span></span>

<span data-ttu-id="23dcb-186">**[Enablequery]** 특성을 사용 하면 클라이언트가 $filter, $sort 및 $page 같은 쿼리 옵션을 사용 하 여 쿼리를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-186">The **[EnableQuery]** attribute enables clients to modify the query, by using query options such as $filter, $sort, and $page.</span></span> <span data-ttu-id="23dcb-187">자세한 내용은 [OData 쿼리 옵션 지원](../supporting-odata-query-options.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="23dcb-187">For more information, see [Supporting OData Query Options](../supporting-odata-query-options.md).</span></span>

## <a name="add-an-entity-to-the-entity-set"></a><span data-ttu-id="23dcb-188">엔터티 집합에 엔터티 추가</span><span class="sxs-lookup"><span data-stu-id="23dcb-188">Add an entity to the entity set</span></span>

<span data-ttu-id="23dcb-189">클라이언트가 데이터베이스에 새 제품을 추가 하도록 하려면 다음 메서드를 추가 하 여 `ProductsController`합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-189">To enable clients to add a new product to the database, add the following method to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample10.cs)]

## <a name="update-an-entity"></a><span data-ttu-id="23dcb-190">엔터티 업데이트</span><span class="sxs-lookup"><span data-stu-id="23dcb-190">Update an entity</span></span>

<span data-ttu-id="23dcb-191">OData는 엔터티 업데이트, 패치 및 PUT에 대 한 두 가지 다른 의미 체계를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-191">OData supports two different semantics for updating an entity, PATCH and PUT.</span></span>

- <span data-ttu-id="23dcb-192">패치는 부분 업데이트를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-192">PATCH performs a partial update.</span></span> <span data-ttu-id="23dcb-193">클라이언트는 업데이트할 속성만 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-193">The client specifies just the properties to update.</span></span>
- <span data-ttu-id="23dcb-194">PUT은 전체 엔터티를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-194">PUT replaces the entire entity.</span></span>

<span data-ttu-id="23dcb-195">PUT의 단점은 클라이언트는 변경 되지 않는 값을 포함 하 여 엔터티의 모든 속성에 대 한 값을 전송 해야 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-195">The disadvantage of PUT is that the client must send values for all of the properties in the entity, including values that are not changing.</span></span> <span data-ttu-id="23dcb-196">[OData 사양](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719) 에는 패치가 선호 됨이 명시 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-196">The [OData spec](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719) states that PATCH is preferred.</span></span>

<span data-ttu-id="23dcb-197">어떤 경우 든, PATCH 및 PUT 메서드의 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-197">In any case, here is the code for both PATCH and PUT methods:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample11.cs)]

<span data-ttu-id="23dcb-198">패치의 경우 컨트롤러는 **델타&lt;t&gt;** 유형을 사용 하 여 변경 내용을 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-198">In the case of PATCH, the controller uses the **Delta&lt;T&gt;** type to track the changes.</span></span>

## <a name="delete-an-entity"></a><span data-ttu-id="23dcb-199">엔터티 삭제</span><span class="sxs-lookup"><span data-stu-id="23dcb-199">Delete an entity</span></span>

<span data-ttu-id="23dcb-200">클라이언트가 데이터베이스에서 제품을 삭제할 수 있게 하려면 다음 메서드를 `ProductsController`에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="23dcb-200">To enable clients to delete a product from the database, add the following method to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample12.cs)]
