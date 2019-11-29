---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
title: Web API 2를 사용 하 여 OData v3 끝점 만들기 | Microsoft Docs
author: MikeWasson
description: OData (Open Data Protocol)는 웹에 대 한 데이터 액세스 프로토콜입니다. OData는 데이터를 구조화 하 고, 데이터를 쿼리하고, 데이터를 조작 하는 일관 된 방법을 제공 합니다.
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 262843d6-43a2-4f1c-82d9-0b90ae6df0cf
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
msc.type: authoredcontent
ms.openlocfilehash: e68a454398f109dfd089be9c9a44d3fe662acc2f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600426"
---
# <a name="creating-an-odata-v3-endpoint-with-web-api-2"></a><span data-ttu-id="eb30a-104">Web API 2를 사용 하 여 OData v3 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="eb30a-104">Creating an OData v3 Endpoint with Web API 2</span></span>

<span data-ttu-id="eb30a-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="eb30a-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="eb30a-106">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="eb30a-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="eb30a-107">OData ( [Open Data Protocol](http://www.odata.org/) )는 웹에 대 한 데이터 액세스 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-107">The [Open Data Protocol](http://www.odata.org/) (OData) is a data access protocol for the web.</span></span> <span data-ttu-id="eb30a-108">OData는 데이터를 구조화 하 고, 데이터를 쿼리하고, CRUD 작업 (만들기, 읽기, 업데이트 및 삭제)을 통해 데이터 집합을 조작 하는 일관 된 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-108">OData provides a uniform way to structure data, query the data, and manipulate the data set through CRUD operations (create, read, update, and delete).</span></span> <span data-ttu-id="eb30a-109">OData는 AtomPub (XML) 및 JSON 형식을 모두 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-109">OData supports both AtomPub (XML) and JSON formats.</span></span> <span data-ttu-id="eb30a-110">또한 OData는 데이터에 대 한 메타 데이터를 노출 하는 방법을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-110">OData also defines a way to expose metadata about the data.</span></span> <span data-ttu-id="eb30a-111">클라이언트는 메타 데이터를 사용 하 여 데이터 집합에 대 한 형식 정보 및 관계를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-111">Clients can use the metadata to discover the type information and relationships for the data set.</span></span>
>
> <span data-ttu-id="eb30a-112">ASP.NET Web API를 사용 하면 데이터 집합에 대 한 OData 끝점을 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-112">ASP.NET Web API makes it easy to create an OData endpoint for a data set.</span></span> <span data-ttu-id="eb30a-113">끝점이 지 원하는 OData 작업을 정확 하 게 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-113">You can control exactly which OData operations the endpoint supports.</span></span> <span data-ttu-id="eb30a-114">비 OData 끝점과 함께 여러 OData 끝점을 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-114">You can host multiple OData endpoints, alongside non-OData endpoints.</span></span> <span data-ttu-id="eb30a-115">데이터 모델, 백 엔드 비즈니스 논리 및 데이터 계층에 대 한 모든 권한을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-115">You have full control over your data model, back-end business logic, and data layer.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="eb30a-116">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="eb30a-116">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="eb30a-117">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="eb30a-117">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="eb30a-118">Web API 2</span><span class="sxs-lookup"><span data-stu-id="eb30a-118">Web API 2</span></span>
> - <span data-ttu-id="eb30a-119">OData 버전 3</span><span class="sxs-lookup"><span data-stu-id="eb30a-119">OData Version 3</span></span>
> - <span data-ttu-id="eb30a-120">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="eb30a-120">Entity Framework 6</span></span>
> - [<span data-ttu-id="eb30a-121">Fiddler 웹 디버깅 프록시 (선택 사항)</span><span class="sxs-lookup"><span data-stu-id="eb30a-121">Fiddler Web Debugging Proxy (Optional)</span></span>](http://www.fiddler2.com)
>
> <span data-ttu-id="eb30a-122">웹 API OData 지원은 [ASP.NET 및 Web Tools 2012.2 업데이트](https://go.microsoft.com/fwlink/?LinkId=282650)에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-122">Web API OData support was added in [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="eb30a-123">그러나이 자습서에서는 Visual Studio 2013에 추가 된 스 캐 폴딩을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-123">However, this tutorial uses scaffolding that was added in Visual Studio 2013.</span></span>

<span data-ttu-id="eb30a-124">이 자습서에서는 클라이언트가 쿼리할 수 있는 간단한 OData 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-124">In this tutorial, you will create a simple OData endpoint that clients can query.</span></span> <span data-ttu-id="eb30a-125">끝점에 대 한 C# 클라이언트도 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-125">You will also create a C# client for the endpoint.</span></span> <span data-ttu-id="eb30a-126">이 자습서를 완료 한 후에는 엔터티 관계, 동작 및 $expand/$select를 포함 하 여 더 많은 기능을 추가 하는 방법을 보여 주는 다음 자습서 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-126">After you complete this tutorial, the next set of tutorials show how to add more functionality, including entity relations, actions, and $expand/$select.</span></span>

- [<span data-ttu-id="eb30a-127">Visual Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="eb30a-127">Create the Visual Studio Project</span></span>](#create-project)
- [<span data-ttu-id="eb30a-128">엔터티 모델 추가</span><span class="sxs-lookup"><span data-stu-id="eb30a-128">Add an Entity Model</span></span>](#add-model)
- [<span data-ttu-id="eb30a-129">OData 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="eb30a-129">Add an OData Controller</span></span>](#add-controller)
- [<span data-ttu-id="eb30a-130">EDM 및 경로 추가</span><span class="sxs-lookup"><span data-stu-id="eb30a-130">Add the EDM and Route</span></span>](#edm)
- [<span data-ttu-id="eb30a-131">데이터베이스 초기값 지정 (선택 사항)</span><span class="sxs-lookup"><span data-stu-id="eb30a-131">Seed the Database (Optional)</span></span>](#seed-db)
- [<span data-ttu-id="eb30a-132">OData 끝점 탐색</span><span class="sxs-lookup"><span data-stu-id="eb30a-132">Exploring the OData Endpoint</span></span>](#explore)
- [<span data-ttu-id="eb30a-133">OData 직렬화 형식</span><span class="sxs-lookup"><span data-stu-id="eb30a-133">OData Serialization Formats</span></span>](#formats)

<a id="create-project"></a>
## <a name="create-the-visual-studio-project"></a><span data-ttu-id="eb30a-134">Visual Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="eb30a-134">Create the Visual Studio Project</span></span>

<span data-ttu-id="eb30a-135">이 자습서에서는 기본 CRUD 작업을 지 원하는 OData 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-135">In this tutorial, you will create an OData endpoint that supports basic CRUD operations.</span></span> <span data-ttu-id="eb30a-136">이 끝점은 단일 리소스 (제품 목록)를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-136">The endpoint will expose a single resource, a list of products.</span></span> <span data-ttu-id="eb30a-137">이후 자습서에서는 더 많은 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-137">Later tutorials will add more features.</span></span>

<span data-ttu-id="eb30a-138">Visual Studio를 시작 하 고 시작 페이지에서 **새 프로젝트** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-138">Start Visual Studio and select **New Project** from the Start page.</span></span> <span data-ttu-id="eb30a-139">또는 **파일** 메뉴에서 **새로 만들기** , **프로젝트**를 차례로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-139">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="eb30a-140">**템플릿** 창에서 **설치 된 템플릿** 을 선택 하 고 시각적 C# 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-140">In the **Templates** pane, select **Installed Templates** and expand the Visual C# node.</span></span> <span data-ttu-id="eb30a-141">**시각적 개체 C#** 에서 **웹**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-141">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="eb30a-142">**ASP.NET 웹 응용 프로그램** 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-142">Select **the ASP.NET Web Application** template.</span></span>

![](creating-an-odata-endpoint/_static/image1.png)

<span data-ttu-id="eb30a-143">**새 ASP.NET 프로젝트** 대화 상자에서 **빈** 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-143">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span> <span data-ttu-id="eb30a-144">&quot;에 대 한 폴더 및 핵심 참조 추가 &quot;에서 **WEB API**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-144">Under &quot;Add folders and core references for...&quot;, check **Web API**.</span></span> <span data-ttu-id="eb30a-145">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-145">Click **OK**.</span></span>

![](creating-an-odata-endpoint/_static/image2.png)

<a id="add-model"></a>
## <a name="add-an-entity-model"></a><span data-ttu-id="eb30a-146">엔터티 모델 추가</span><span class="sxs-lookup"><span data-stu-id="eb30a-146">Add an Entity Model</span></span>

<span data-ttu-id="eb30a-147">*모델*은 애플리케이션에서 데이터를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-147">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="eb30a-148">이 자습서에서는 제품을 나타내는 모델이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-148">For this tutorial, we need a model that represents a product.</span></span> <span data-ttu-id="eb30a-149">모델은 OData 엔터티 형식에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-149">The model corresponds to our OData entity type.</span></span>

<span data-ttu-id="eb30a-150">솔루션 탐색기에서 모델 폴더를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-150">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="eb30a-151">상황에 맞는 메뉴에서 **추가** 를 선택한 다음 **클래스**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-151">From the context menu, select **Add** then select **Class**.</span></span>

![](creating-an-odata-endpoint/_static/image3.png)

<span data-ttu-id="eb30a-152">새 항목 **추가** 대화 상자에서 클래스 이름을 Product&quot;로 &quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-152">In the **Add New** Item dialog, name the class &quot;Product&quot;.</span></span>

![](creating-an-odata-endpoint/_static/image4.png)

> [!NOTE]
> <span data-ttu-id="eb30a-153">규칙에 따라 모델 클래스는 모델 폴더에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-153">By convention, model classes are placed in the Models folder.</span></span> <span data-ttu-id="eb30a-154">사용자 고유의 프로젝트에서이 규칙을 따를 필요는 없지만이 자습서에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-154">You don't have to follow this convention in your own projects, but we'll use it for this tutorial.</span></span>

<span data-ttu-id="eb30a-155">Product.cs 파일에서 다음 클래스 정의를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-155">In the Product.cs file, add the following class definition:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample1.cs)]

<span data-ttu-id="eb30a-156">ID 속성은 엔터티 키가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-156">The ID property will be the entity key.</span></span> <span data-ttu-id="eb30a-157">클라이언트는 ID로 제품을 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-157">Clients can query products by ID.</span></span> <span data-ttu-id="eb30a-158">이 필드는 백 엔드 데이터베이스의 기본 키 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-158">This field would also be the primary key in the back-end database.</span></span>

<span data-ttu-id="eb30a-159">이제 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-159">Build the project now.</span></span> <span data-ttu-id="eb30a-160">다음 단계에서는 리플렉션을 사용 하 여 제품 유형을 찾는 몇 가지 Visual Studio 스 캐 폴딩을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-160">In the next step, we'll use some Visual Studio scaffolding that uses reflection to find the Product type.</span></span>

<a id="add-controller"></a>
## <a name="add-an-odata-controller"></a><span data-ttu-id="eb30a-161">OData 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="eb30a-161">Add an OData Controller</span></span>

<span data-ttu-id="eb30a-162">*컨트롤러* 는 HTTP 요청을 처리 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-162">A *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="eb30a-163">OData 서비스에서 각 엔터티 집합에 대해 별도의 컨트롤러를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-163">You define a separate controller for each entity set in you OData service.</span></span> <span data-ttu-id="eb30a-164">이 자습서에서는 단일 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-164">In this tutorial, we'll create a single controller.</span></span>

<span data-ttu-id="eb30a-165">솔루션 탐색기에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-165">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="eb30a-166">**추가** 를 선택한 다음 **컨트롤러**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-166">Select **Add** and then select **Controller**.</span></span>

![](creating-an-odata-endpoint/_static/image5.png)

<span data-ttu-id="eb30a-167">**스 캐 폴드 추가** 대화 상자에서 Entity Framework&quot;를 사용 하 여 작업을 포함 하는 Web API 2 OData 컨트롤러 &quot;를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-167">In the **Add Scaffold** dialog, select &quot;Web API 2 OData Controller with actions, using Entity Framework&quot;.</span></span>

![](creating-an-odata-endpoint/_static/image6.png)

<span data-ttu-id="eb30a-168">**컨트롤러 추가** 대화 상자에서 컨트롤러 이름을 "ProductsController"로 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-168">In the **Add Controller** dialog, name the controller "ProductsController".</span></span> <span data-ttu-id="eb30a-169">비동기 컨트롤러 작업 사용 &quot;&quot; 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-169">Select the &quot;Use async controller actions&quot; checkbox.</span></span> <span data-ttu-id="eb30a-170">**모델** 드롭다운 목록에서 Product 클래스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-170">In the **Model** drop-down list, select the Product class.</span></span>

![](creating-an-odata-endpoint/_static/image7.png)

<span data-ttu-id="eb30a-171">**새 데이터 컨텍스트 ...** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-171">Click the **New data context...** button.</span></span> <span data-ttu-id="eb30a-172">데이터 컨텍스트 형식에 대 한 기본 이름을 그대로 두고 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-172">Leave the default name for the data context type, and click **Add**.</span></span>

![](creating-an-odata-endpoint/_static/image8.png)

<span data-ttu-id="eb30a-173">컨트롤러 추가 대화 상자에서 추가를 클릭 하 여 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-173">Click Add in the Add Controller dialog to add the controller.</span></span>

![](creating-an-odata-endpoint/_static/image9.png)

<span data-ttu-id="eb30a-174">참고:&quot;유형을 가져오는 중 오류가 발생 했습니다 &quot;오류 메시지가 표시 되는 경우 Product 클래스를 추가한 후 Visual Studio 프로젝트를 빌드 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-174">Note: If you get an error message that says &quot;There was an error getting the type...&quot;, make sure that you built the Visual Studio project after you added the Product class.</span></span> <span data-ttu-id="eb30a-175">스 캐 폴딩은 리플렉션을 사용 하 여 클래스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-175">The scaffolding uses reflection to find the class.</span></span>

![](creating-an-odata-endpoint/_static/image10.png)

<span data-ttu-id="eb30a-176">스 캐 폴딩은 두 코드 파일을 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-176">The scaffolding adds two code files to the project:</span></span>

- <span data-ttu-id="eb30a-177">Products.cs는 OData 끝점을 구현 하는 Web API 컨트롤러를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-177">Products.cs defines the Web API controller that implements the OData endpoint.</span></span>
- <span data-ttu-id="eb30a-178">ProductServiceContext.cs는 Entity Framework 사용 하 여 기본 데이터베이스를 쿼리 하는 메서드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-178">ProductServiceContext.cs provides methods to query the underlying database, using Entity Framework.</span></span>

![](creating-an-odata-endpoint/_static/image11.png)

<a id="edm"></a>
## <a name="add-the-edm-and-route"></a><span data-ttu-id="eb30a-179">EDM 및 경로 추가</span><span class="sxs-lookup"><span data-stu-id="eb30a-179">Add the EDM and Route</span></span>

<span data-ttu-id="eb30a-180">솔루션 탐색기에서 앱\_시작 폴더를 확장 하 고 이름이 WebApiConfig.cs 인 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-180">In Solution Explorer, expand the App\_Start folder and open the file named WebApiConfig.cs.</span></span> <span data-ttu-id="eb30a-181">이 클래스는 Web API에 대 한 구성 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-181">This class holds configuration code for Web API.</span></span> <span data-ttu-id="eb30a-182">이 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-182">Replace this code with the following:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample2.cs)]

<span data-ttu-id="eb30a-183">이 코드는 다음 두 가지 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-183">This code does two things:</span></span>

- <span data-ttu-id="eb30a-184">OData 끝점에 대 한 EDM (엔터티 데이터 모델)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-184">Creates an Entity Data Model (EDM) for the OData endpoint.</span></span>
- <span data-ttu-id="eb30a-185">끝점에 대 한 경로를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-185">Adds a route for the endpoint.</span></span>

<span data-ttu-id="eb30a-186">EDM은 데이터의 추상 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-186">An EDM is an abstract model of the data.</span></span> <span data-ttu-id="eb30a-187">EDM은 메타 데이터 문서를 만들고 서비스에 대 한 Uri를 정의 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-187">The EDM is used to create the metadata document and define the URIs for the service.</span></span> <span data-ttu-id="eb30a-188">**ODataConventionModelBuilder** 는 기본 명명 규칙 edm 집합을 사용 하 여 edm을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-188">The **ODataConventionModelBuilder** creates an EDM by using a set of default naming conventions EDM.</span></span> <span data-ttu-id="eb30a-189">이 방법에는 최소한의 코드가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-189">This approach requires the least code.</span></span> <span data-ttu-id="eb30a-190">EDM을 보다 세부적으로 제어 하려는 경우 **만드는** 클래스를 사용 하 여 속성, 키 및 탐색 속성을 명시적으로 추가 하 여 edm을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-190">If you want more control over the EDM, you can use the **ODataModelBuilder** class to create the EDM by adding properties, keys, and navigation properties explicitly.</span></span>

<span data-ttu-id="eb30a-191">**EntitySet** 메서드는 EDM에 엔터티 집합을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-191">The **EntitySet** method adds an entity set to the EDM:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample3.cs)]

<span data-ttu-id="eb30a-192">"Products" 문자열은 엔터티 집합의 이름을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-192">The string "Products" defines the name of the entity set.</span></span> <span data-ttu-id="eb30a-193">컨트롤러의 이름은 엔터티 집합의 이름과 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-193">The name of the controller must match the name of the entity set.</span></span> <span data-ttu-id="eb30a-194">이 자습서에서 엔터티 집합의 이름은 "Products"이 고 컨트롤러의 이름은 `ProductsController`입니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-194">In this tutorial, the entity set is named "Products" and the controller is named `ProductsController`.</span></span> <span data-ttu-id="eb30a-195">"제품 집합" 엔터티 집합의 이름을 지정 하는 경우 컨트롤러의 이름을 `ProductSetController`합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-195">If you named the entity set "ProductSet", you would name the controller `ProductSetController`.</span></span> <span data-ttu-id="eb30a-196">끝점에는 여러 엔터티 집합이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-196">Note that an endpoint can have multiple entity sets.</span></span> <span data-ttu-id="eb30a-197">각 엔터티 집합에 대해 **EntitySet&lt;t&gt;** 를 호출한 다음 해당 하는 컨트롤러를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-197">Call **EntitySet&lt;T&gt;** for each entity set, and then define a corresponding controller.</span></span>

<span data-ttu-id="eb30a-198">**MapODataRoute** 메서드는 OData 끝점에 대 한 경로를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-198">The **MapODataRoute** method adds a route for the OData endpoint.</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample4.cs)]

<span data-ttu-id="eb30a-199">첫 번째 매개 변수는 경로에 대 한 친숙 한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-199">The first parameter is a friendly name for the route.</span></span> <span data-ttu-id="eb30a-200">서비스의 클라이언트에는이 이름이 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-200">Clients of your service do not see this name.</span></span> <span data-ttu-id="eb30a-201">두 번째 매개 변수는 끝점의 URI 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-201">The second parameter is the URI prefix for the endpoint.</span></span> <span data-ttu-id="eb30a-202">이 코드를 지정 하면 Products 엔터티 집합에 대 한 URI는 http://<em>hostname</em>/Odata/products로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-202">Given this code, the URI for the Products entity set is http://<em>hostname</em>/odata/Products.</span></span> <span data-ttu-id="eb30a-203">응용 프로그램에는 둘 이상의 OData 끝점이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-203">Your application can have more than one OData endpoint.</span></span> <span data-ttu-id="eb30a-204">각 끝점에 대해 <strong>MapODataRoute</strong> 를 호출 하 고 고유한 경로 이름 및 고유한 URI 접두사를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-204">For each endpoint, call <strong>MapODataRoute</strong> and provide a unique route name and a unique URI prefix.</span></span>

<a id="seed-db"></a>
## <a name="seed-the-database-optional"></a><span data-ttu-id="eb30a-205">데이터베이스 초기값 지정 (선택 사항)</span><span class="sxs-lookup"><span data-stu-id="eb30a-205">Seed the Database (Optional)</span></span>

<span data-ttu-id="eb30a-206">이 단계에서는 Entity Framework를 사용 하 여 일부 테스트 데이터로 데이터베이스를 초기값으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-206">In this step, you will use Entity Framework to seed the database with some test data.</span></span> <span data-ttu-id="eb30a-207">이 단계는 선택 사항 이지만 OData 끝점을 즉시 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-207">This step is optional, but it lets you test out your OData endpoint right away.</span></span>

<span data-ttu-id="eb30a-208">**도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-208">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="eb30a-209">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-209">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample5.cmd)]

<span data-ttu-id="eb30a-210">그러면 migration 이라는 폴더와 이름이 Configuration.cs 인 코드 파일이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-210">This adds a folder named Migrations and a code file named Configuration.cs.</span></span>

![](creating-an-odata-endpoint/_static/image12.png)

<span data-ttu-id="eb30a-211">이 파일을 열고 다음 코드를 `Configuration.Seed` 메서드에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-211">Open this file and add the following code to the `Configuration.Seed` method.</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample6.cs)]

<span data-ttu-id="eb30a-212">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-212">In the Package Manager Console Window, enter the following commands:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample7.cmd)]

<span data-ttu-id="eb30a-213">이러한 명령은 데이터베이스를 만든 다음 해당 코드를 실행 하는 코드를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-213">These commands generate code that creates the database, and then executes that code.</span></span>

<a id="explore"></a>
## <a name="exploring-the-odata-endpoint"></a><span data-ttu-id="eb30a-214">OData 끝점 탐색</span><span class="sxs-lookup"><span data-stu-id="eb30a-214">Exploring the OData Endpoint</span></span>

<span data-ttu-id="eb30a-215">이 섹션에서는 [Fiddler 웹 디버깅 프록시](http://www.fiddler2.com) 를 사용 하 여 끝점에 요청을 보내고 응답 메시지를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-215">In this section, we'll use the [Fiddler Web Debugging Proxy](http://www.fiddler2.com) to send requests to the endpoint and examine the response messages.</span></span> <span data-ttu-id="eb30a-216">그러면 OData 끝점의 기능을 이해 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-216">This will help you to understand the capabilities of an OData endpoint.</span></span>

<span data-ttu-id="eb30a-217">Visual Studio에서 F5 키를 눌러 디버깅을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-217">In Visual Studio, press F5 to start debugging.</span></span> <span data-ttu-id="eb30a-218">기본적으로 Visual Studio는 `http://localhost:*port*`하기 위해 브라우저를 엽니다. 여기서 *port* 는 프로젝트 설정에 구성 된 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-218">By default, Visual Studio opens your browser to `http://localhost:*port*`, where *port* is the port number configured in the project settings.</span></span>

<span data-ttu-id="eb30a-219">프로젝트 설정에서 포트 번호를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-219">You can change the port number in the project settings.</span></span> <span data-ttu-id="eb30a-220">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-220">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="eb30a-221">속성 창에서 **웹**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-221">In the properties window, select **Web**.</span></span> <span data-ttu-id="eb30a-222">**프로젝트 Url**아래에 포트 번호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-222">Enter the port number under **Project Url**.</span></span>

### <a name="service-document"></a><span data-ttu-id="eb30a-223">서비스 문서</span><span class="sxs-lookup"><span data-stu-id="eb30a-223">Service Document</span></span>

<span data-ttu-id="eb30a-224">*서비스 문서* 에는 OData 끝점에 대 한 엔터티 집합 목록이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-224">The *service document* contains a list of the entity sets for the OData endpoint.</span></span> <span data-ttu-id="eb30a-225">서비스 문서를 가져오려면 서비스의 루트 URI에 GET 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-225">To get the service document, send a GET request to the root URI of the service.</span></span>

<span data-ttu-id="eb30a-226">Fiddler를 사용 하 여 **작성기** 탭에 다음 URI를 입력 합니다 `http://localhost:port/odata/`. 여기서 *port* 는 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-226">Using Fiddler, enter the following URI in the **Composer** tab: `http://localhost:port/odata/`, where *port* is the port number.</span></span>

![](creating-an-odata-endpoint/_static/image13.png)

<span data-ttu-id="eb30a-227">**실행** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-227">Click the **Execute** button.</span></span> <span data-ttu-id="eb30a-228">Fiddler는 응용 프로그램에 HTTP GET 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-228">Fiddler sends an HTTP GET request to your application.</span></span> <span data-ttu-id="eb30a-229">웹 세션 목록에 응답이 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-229">You should see the response in the Web Sessions list.</span></span> <span data-ttu-id="eb30a-230">모든 것이 작동 하는 경우 상태 코드는 200가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-230">If everything is working, the status code will be 200.</span></span>

![](creating-an-odata-endpoint/_static/image14.png)

<span data-ttu-id="eb30a-231">웹 세션 목록에서 응답을 두 번 클릭 하면 검사기 탭에서 응답 메시지의 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-231">Double-click the response in the Web Sessions list to see the details of the response message in the Inspectors tab.</span></span>

![](creating-an-odata-endpoint/_static/image15.png)

<span data-ttu-id="eb30a-232">원시 HTTP 응답 메시지는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-232">The raw HTTP response message should look similar to the following:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample8.cmd)]

<span data-ttu-id="eb30a-233">기본적으로 Web API는 AtomPub 형식으로 서비스 문서를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-233">By default, Web API returns the service document in AtomPub format.</span></span> <span data-ttu-id="eb30a-234">JSON을 요청 하려면 HTTP 요청에 다음 헤더를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-234">To request JSON, add the following header to the HTTP request:</span></span>

`Accept: application/json`

![](creating-an-odata-endpoint/_static/image16.png)

<span data-ttu-id="eb30a-235">이제 HTTP 응답은 JSON 페이로드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-235">Now the HTTP response contains a JSON payload:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample9.cmd)]

### <a name="service-metadata-document"></a><span data-ttu-id="eb30a-236">서비스 메타 데이터 문서</span><span class="sxs-lookup"><span data-stu-id="eb30a-236">Service Metadata Document</span></span>

<span data-ttu-id="eb30a-237">*서비스 메타 데이터 문서* 에서는 CSDL (개념 스키마 정의 언어) 이라는 XML 언어를 사용 하 여 서비스의 데이터 모델에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-237">The *service metadata document* describes the data model of the service, using an XML language called the Conceptual Schema Definition Language (CSDL).</span></span> <span data-ttu-id="eb30a-238">메타 데이터 문서는 서비스의 데이터 구조를 보여 주며 클라이언트 코드를 생성 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-238">The metadata document shows the structure of the data in the service, and can be used to generate client code.</span></span>

<span data-ttu-id="eb30a-239">메타 데이터 문서를 가져오려면 GET 요청을 `http://localhost:port/odata/$metadata`으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-239">To get the metadata document, send a GET request to `http://localhost:port/odata/$metadata`.</span></span> <span data-ttu-id="eb30a-240">이 자습서에 표시 된 끝점에 대 한 메타 데이터는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-240">Here is the metadata for the endpoint shown in this tutorial.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample10.cmd)]

### <a name="entity-set"></a><span data-ttu-id="eb30a-241">엔터티 집합</span><span class="sxs-lookup"><span data-stu-id="eb30a-241">Entity Set</span></span>

<span data-ttu-id="eb30a-242">Products 엔터티 집합을 가져오려면 `http://localhost:port/odata/Products`에 GET 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-242">To get the Products entity set, send a GET request to `http://localhost:port/odata/Products`.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample11.cmd)]

### <a name="entity"></a><span data-ttu-id="eb30a-243">엔터티</span><span class="sxs-lookup"><span data-stu-id="eb30a-243">Entity</span></span>

<span data-ttu-id="eb30a-244">개별 제품을 가져오려면 GET 요청을 `http://localhost:port/odata/Products(1)`으로 보냅니다. 여기서 "1"은 제품 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-244">To get an individual product, send a GET request to `http://localhost:port/odata/Products(1)`, where "1" is the product ID.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample12.cmd)]

<a id="formats"></a>
## <a name="odata-serialization-formats"></a><span data-ttu-id="eb30a-245">OData 직렬화 형식</span><span class="sxs-lookup"><span data-stu-id="eb30a-245">OData Serialization Formats</span></span>

<span data-ttu-id="eb30a-246">OData는 다음과 같은 여러 serialization 형식을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-246">OData supports several serialization formats:</span></span>

- <span data-ttu-id="eb30a-247">Atom Pub (XML)</span><span class="sxs-lookup"><span data-stu-id="eb30a-247">Atom Pub (XML)</span></span>
- <span data-ttu-id="eb30a-248">JSON "light" (OData v3에 도입 됨)</span><span class="sxs-lookup"><span data-stu-id="eb30a-248">JSON "light" (introduced in OData v3)</span></span>
- <span data-ttu-id="eb30a-249">JSON "verbose" (OData v2)</span><span class="sxs-lookup"><span data-stu-id="eb30a-249">JSON "verbose" (OData v2)</span></span>

<span data-ttu-id="eb30a-250">기본적으로 Web API는 AtomPubJSON "light" 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-250">By default, Web API uses AtomPubJSON "light" format.</span></span>

<span data-ttu-id="eb30a-251">AtomPub 형식을 가져오려면 Accept 헤더를 "application/atom + xml"로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-251">To get AtomPub format, set the Accept header to "application/atom+xml".</span></span> <span data-ttu-id="eb30a-252">예제 응답 본문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-252">Here is an example response body:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample13.cmd)]

<span data-ttu-id="eb30a-253">Atom 형식의 뚜렷한 단점 중 하나를 확인할 수 있습니다. JSON 밝은 것 보다 훨씬 더 자세한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-253">You can see one obvious disadvantage of the Atom format: It's a lot more verbose than the JSON light.</span></span> <span data-ttu-id="eb30a-254">그러나 클라이언트가 AtomPub를 이해 하는 경우 클라이언트는 JSON을 통해 해당 형식을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-254">However, if you have a client that understands AtomPub, the client might prefer that format over JSON.</span></span>

<span data-ttu-id="eb30a-255">동일한 엔터티의 JSON light 버전은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-255">Here is the JSON light version of the same entity:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample14.cmd)]

<span data-ttu-id="eb30a-256">JSON 광원 형식은 OData 프로토콜의 버전 3에서 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-256">The JSON light format was introduced in version 3 of the OData protocol.</span></span> <span data-ttu-id="eb30a-257">이전 버전과의 호환성을 위해 클라이언트는 이전의 "verbose" JSON 형식을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-257">For backward compatibility, a client can request the older "verbose" JSON format.</span></span> <span data-ttu-id="eb30a-258">자세한 JSON을 요청 하려면 Accept 헤더를 `application/json;odata=verbose`설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-258">To request verbose JSON, set the Accept header to `application/json;odata=verbose`.</span></span> <span data-ttu-id="eb30a-259">자세한 버전은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-259">Here is the verbose version:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample15.cmd)]

<span data-ttu-id="eb30a-260">이 형식은 응답 본문에서 더 많은 메타 데이터를 전달 하므로 전체 세션에 상당한 오버 헤드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-260">This format conveys more metadata in the response body, which can add considerable overhead over an entire session.</span></span> <span data-ttu-id="eb30a-261">또한 "d" 라는 속성에 개체를 래핑하여 간접 참조 수준을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb30a-261">Also, it adds a level of indirection by wrapping the object in a property named "d".</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb30a-262">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eb30a-262">Next Steps</span></span>

- [<span data-ttu-id="eb30a-263">엔터티 관계 추가</span><span class="sxs-lookup"><span data-stu-id="eb30a-263">Add Entity Relations</span></span>](working-with-entity-relations.md)
- [<span data-ttu-id="eb30a-264">OData 작업 추가</span><span class="sxs-lookup"><span data-stu-id="eb30a-264">Add OData Actions</span></span>](odata-actions.md)
- [<span data-ttu-id="eb30a-265">.NET 클라이언트에서 OData 서비스 호출</span><span class="sxs-lookup"><span data-stu-id="eb30a-265">Call the OData Service From a .NET Client</span></span>](calling-an-odata-service-from-a-net-client.md)
