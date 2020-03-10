---
uid: web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
title: ASP.NET Web API 2 (C#)-ASP.NET 4.X를 시작 합니다.
author: MikeWasson
description: 코드를 사용 하는 자습서입니다. ASP.NET Web API를 사용 하 여 제품 목록을 반환 하는 Web API를 만듭니다.
ms.author: riande
ms.date: 11/28/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
msc.type: authoredcontent
ms.openlocfilehash: 3e35c2bc0e46dfdb4544b772775eddd533f27be3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448553"
---
# <a name="get-started-with-aspnet-web-api-2-c"></a><span data-ttu-id="a03e9-104">ASP.NET Web API 2 (C#) 시작</span><span class="sxs-lookup"><span data-stu-id="a03e9-104">Get Started with ASP.NET Web API 2 (C#)</span></span>

<span data-ttu-id="a03e9-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a03e9-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="a03e9-106">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="a03e9-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Sample-code-of-Getting-c56ccb28)

<span data-ttu-id="a03e9-107">이 자습서에서는 ASP.NET Web API를 사용 하 여 제품 목록을 반환 하는 Web API를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-107">In this tutorial, you will use ASP.NET Web API to create a web API that returns a list of products.</span></span>

<span data-ttu-id="a03e9-108">HTTP는 웹 페이지를 처리 하기 위한 것이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-108">HTTP is not just for serving up web pages.</span></span> <span data-ttu-id="a03e9-109">HTTP는 서비스 및 데이터를 노출 하는 Api를 빌드하기 위한 강력한 플랫폼 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-109">HTTP is also a powerful platform for building APIs that expose services and data.</span></span> <span data-ttu-id="a03e9-110">HTTP는 단순 하 고 유연 하며 다양 한 장소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-110">HTTP is simple, flexible, and ubiquitous.</span></span> <span data-ttu-id="a03e9-111">거의 모든 플랫폼에서 HTTP 라이브러리를 사용할 수 있으므로 HTTP 서비스는 브라우저, 모바일 장치 및 기존 데스크톱 응용 프로그램을 비롯 한 광범위 한 클라이언트에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-111">Almost any platform that you can think of has an HTTP library, so HTTP services can reach a broad range of clients, including browsers, mobile devices, and traditional desktop applications.</span></span>

<span data-ttu-id="a03e9-112">ASP.NET Web API은 .NET Framework을 기반으로 웹 Api를 빌드하기 위한 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-112">ASP.NET Web API is a framework for building web APIs on top of the .NET Framework.</span></span> 

## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="a03e9-113">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="a03e9-113">Software versions used in the tutorial</span></span>

- [<span data-ttu-id="a03e9-114">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="a03e9-114">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
- <span data-ttu-id="a03e9-115">Web API 2</span><span class="sxs-lookup"><span data-stu-id="a03e9-115">Web API 2</span></span>

<span data-ttu-id="a03e9-116">이 자습서의 최신 버전은 [ASP.NET Core 및 Visual Studio For Windows를 사용 하 여 WEB API 만들기](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a03e9-116">See [Create a web API with ASP.NET Core and Visual Studio for Windows](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api) for a newer version of this tutorial.</span></span>

## <a name="create-a-web-api-project"></a><span data-ttu-id="a03e9-117">웹 API 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="a03e9-117">Create a Web API Project</span></span>

<span data-ttu-id="a03e9-118">이 자습서에서는 ASP.NET Web API를 사용 하 여 제품 목록을 반환 하는 Web API를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-118">In this tutorial, you will use ASP.NET Web API to create a web API that returns a list of products.</span></span> <span data-ttu-id="a03e9-119">프런트 엔드 웹 페이지는 jQuery를 사용 하 여 결과를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-119">The front-end web page uses jQuery to display the results.</span></span>

![](tutorial-your-first-web-api/_static/image1.png)

<span data-ttu-id="a03e9-120">Visual Studio를 시작 하 고 **시작** 페이지에서 **새 프로젝트** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-120">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="a03e9-121">또는 **파일** 메뉴에서 **새로 만들기** , **프로젝트**를 차례로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-121">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="a03e9-122">**템플릿** 창에서 **설치 된 템플릿** 을 선택 하 고  **C# 시각적** 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-122">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="a03e9-123">**시각적 개체 C#** 에서 **웹**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-123">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="a03e9-124">프로젝트 템플릿 목록에서 **ASP.NET 웹 응용 프로그램**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-124">In the list of project templates, select **ASP.NET Web Application**.</span></span> <span data-ttu-id="a03e9-125">프로젝트 이름을 "ProductsApp"로 선택 하 고 **확인을**클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-125">Name the project "ProductsApp" and click **OK**.</span></span>

![](tutorial-your-first-web-api/_static/image2.png)

<span data-ttu-id="a03e9-126">**새 ASP.NET 프로젝트** 대화 상자에서 **빈** 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-126">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span> <span data-ttu-id="a03e9-127">&quot;에 대 한 &quot;폴더 및 핵심 참조 추가에서 **WEB API**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-127">Under &quot;Add folders and core references for&quot;, check **Web API**.</span></span> <span data-ttu-id="a03e9-128">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-128">Click **OK**.</span></span>

![](tutorial-your-first-web-api/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="a03e9-129">&quot;Web API&quot; 템플릿을 사용 하 여 Web API 프로젝트를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-129">You can also create a Web API project using the &quot;Web API&quot; template.</span></span> <span data-ttu-id="a03e9-130">Web API 템플릿에서는 ASP.NET MVC를 사용 하 여 API 도움말 페이지를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-130">The Web API template uses ASP.NET MVC to provide API help pages.</span></span> <span data-ttu-id="a03e9-131">MVC 없이 Web API를 표시 하려고 하기 때문에이 자습서에 빈 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-131">I'm using the Empty template for this tutorial because I want to show Web API without MVC.</span></span> <span data-ttu-id="a03e9-132">일반적으로 Web API를 사용 하기 위해 ASP.NET MVC를 알 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-132">In general, you don't need to know ASP.NET MVC to use Web API.</span></span>

## <a name="adding-a-model"></a><span data-ttu-id="a03e9-133">모델 추가</span><span class="sxs-lookup"><span data-stu-id="a03e9-133">Adding a Model</span></span>

<span data-ttu-id="a03e9-134">*모델*은 애플리케이션에서 데이터를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-134">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="a03e9-135">JSON, XML 또는 다른 형식으로 모델을 자동으로 serialize 한 다음, serialize 된 데이터를 HTTP 응답 메시지의 본문에 쓸 ASP.NET Web API 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-135">ASP.NET Web API can automatically serialize your model to JSON, XML, or some other format, and then write the serialized data into the body of the HTTP response message.</span></span> <span data-ttu-id="a03e9-136">클라이언트에서 serialization 형식을 읽을 수 있으면 개체를 deserialize 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-136">As long as a client can read the serialization format, it can deserialize the object.</span></span> <span data-ttu-id="a03e9-137">대부분의 클라이언트는 XML 또는 JSON을 구문 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-137">Most clients can parse either XML or JSON.</span></span> <span data-ttu-id="a03e9-138">또한 클라이언트는 HTTP 요청 메시지의 Accept 헤더를 설정 하 여 원하는 형식을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-138">Moreover, the client can indicate which format it wants by setting the Accept header in the HTTP request message.</span></span>

<span data-ttu-id="a03e9-139">먼저 제품을 나타내는 간단한 모델을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-139">Let's start by creating a simple model that represents a product.</span></span>

<span data-ttu-id="a03e9-140">솔루션 탐색기가 표시되지 않는 경우 **보기** 메뉴를 클릭하고 **솔루션 탐색기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-140">If Solution Explorer is not already visible, click the **View** menu and select **Solution Explorer**.</span></span> <span data-ttu-id="a03e9-141">솔루션 탐색기에서 Models 폴더를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-141">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="a03e9-142">상황에 맞는 메뉴에서 **추가**를 선택한 다음 **클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-142">From the context menu, select **Add** then select **Class**.</span></span>

![](tutorial-your-first-web-api/_static/image4.png)

<span data-ttu-id="a03e9-143">클래스 이름을 Product&quot;&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-143">Name the class &quot;Product&quot;.</span></span> <span data-ttu-id="a03e9-144">`Product` 클래스에 다음 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-144">Add the following properties to the `Product` class.</span></span>

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample1.cs)]

## <a name="adding-a-controller"></a><span data-ttu-id="a03e9-145">컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="a03e9-145">Adding a Controller</span></span>

<span data-ttu-id="a03e9-146">Web API에서 *컨트롤러*는 HTTP 요청을 처리하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-146">In Web API, a *controller* is an object that handles HTTP requests.</span></span> <span data-ttu-id="a03e9-147">제품의 목록이 나 ID로 지정 된 단일 제품을 반환할 수 있는 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-147">We'll add a controller that can return either a list of products or a single product specified by ID.</span></span>

> [!NOTE]
> <span data-ttu-id="a03e9-148">ASP.NET MVC를 사용한 경우 이미 컨트롤러에 대해 잘 알고 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-148">If you have used ASP.NET MVC, you are already familiar with controllers.</span></span> <span data-ttu-id="a03e9-149">Web API 컨트롤러는 MVC 컨트롤러와 비슷하지만 **컨트롤러** 클래스 대신 **ApiController** 클래스를 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-149">Web API controllers are similar to MVC controllers, but inherit the **ApiController** class instead of the **Controller** class.</span></span>

<span data-ttu-id="a03e9-150">**솔루션 탐색기**에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-150">In **Solution Explorer**, right-click the Controllers folder.</span></span> <span data-ttu-id="a03e9-151">**추가**를 선택한 후 **컨트롤러**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-151">Select **Add** and then select **Controller**.</span></span>

![](tutorial-your-first-web-api/_static/image5.png)

<span data-ttu-id="a03e9-152">**스캐폴드 추가** 대화 상자에서 **Web API 컨트롤러 - 비어 있음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-152">In the **Add Scaffold** dialog, select **Web API Controller - Empty**.</span></span> <span data-ttu-id="a03e9-153">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-153">Click **Add**.</span></span>

![](tutorial-your-first-web-api/_static/image6.png)

<span data-ttu-id="a03e9-154">**컨트롤러 추가** 대화 상자에서 컨트롤러 이름을 ProductsController&quot;로 &quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-154">In the **Add Controller** dialog, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="a03e9-155">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-155">Click **Add**.</span></span>

![](tutorial-your-first-web-api/_static/image7.png)

<span data-ttu-id="a03e9-156">스 캐 폴딩은 Controllers 폴더에 ProductsController.cs 라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-156">The scaffolding creates a file named ProductsController.cs in the Controllers folder.</span></span>

![](tutorial-your-first-web-api/_static/image8.png)

> [!NOTE]
> <span data-ttu-id="a03e9-157">컨트롤러를 컨트롤러 라는 폴더에 배치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-157">You don't need to put your controllers into a folder named Controllers.</span></span> <span data-ttu-id="a03e9-158">폴더 이름은 원본 파일을 구성 하는 편리한 방법일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-158">The folder name is just a convenient way to organize your source files.</span></span>

<span data-ttu-id="a03e9-159">이 파일이 열려 있지 않으면 파일을 두 번 클릭하여 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-159">If this file is not open already, double-click the file to open it.</span></span> <span data-ttu-id="a03e9-160">이 파일의 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-160">Replace the code in this file with the following:</span></span>

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample2.cs)]

<span data-ttu-id="a03e9-161">예제를 간단 하 게 유지 하기 위해 제품은 컨트롤러 클래스 내부의 고정 배열에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-161">To keep the example simple, products are stored in a fixed array inside the controller class.</span></span> <span data-ttu-id="a03e9-162">물론 실제 응용 프로그램에서는 데이터베이스를 쿼리하거나 다른 외부 데이터 원본을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-162">Of course, in a real application, you would query a database or use some other external data source.</span></span>

<span data-ttu-id="a03e9-163">컨트롤러는 제품을 반환 하는 두 가지 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-163">The controller defines two methods that return products:</span></span>

- <span data-ttu-id="a03e9-164">`GetAllProducts` 메서드는 전체 제품 목록을 **IEnumerable&lt;Product&gt;** 형식으로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-164">The `GetAllProducts` method returns the entire list of products as an **IEnumerable&lt;Product&gt;** type.</span></span>
- <span data-ttu-id="a03e9-165">`GetProduct` 메서드는 해당 ID로 단일 제품을 조회 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-165">The `GetProduct` method looks up a single product by its ID.</span></span>

<span data-ttu-id="a03e9-166">이것으로 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-166">That's it!</span></span> <span data-ttu-id="a03e9-167">웹 API가 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-167">You have a working web API.</span></span> <span data-ttu-id="a03e9-168">컨트롤러의 각 메서드는 하나 이상의 Uri에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-168">Each method on the controller corresponds to one or more URIs:</span></span>

| <span data-ttu-id="a03e9-169">Controller 메서드</span><span class="sxs-lookup"><span data-stu-id="a03e9-169">Controller Method</span></span> | <span data-ttu-id="a03e9-170">URI</span><span class="sxs-lookup"><span data-stu-id="a03e9-170">URI</span></span> |
| --- | --- |
| <span data-ttu-id="a03e9-171">GetAllProducts</span><span class="sxs-lookup"><span data-stu-id="a03e9-171">GetAllProducts</span></span> | <span data-ttu-id="a03e9-172">/api/제품</span><span class="sxs-lookup"><span data-stu-id="a03e9-172">/api/products</span></span> |
| <span data-ttu-id="a03e9-173">GetProduct</span><span class="sxs-lookup"><span data-stu-id="a03e9-173">GetProduct</span></span> | <span data-ttu-id="a03e9-174">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="a03e9-174">/api/products/*id*</span></span> |

<span data-ttu-id="a03e9-175">`GetProduct` 메서드의 경우 URI의 *id* 는 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-175">For the `GetProduct` method, the *id* in the URI is a placeholder.</span></span> <span data-ttu-id="a03e9-176">예를 들어 ID가 5 인 제품을 가져오려면 URI가 `api/products/5`됩니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-176">For example, to get the product with ID of 5, the URI is `api/products/5`.</span></span>

<span data-ttu-id="a03e9-177">웹 API가 HTTP 요청을 컨트롤러 메서드로 라우팅하는 방법에 대 한 자세한 내용은 [ASP.NET Web API 라우팅](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a03e9-177">For more information about how Web API routes HTTP requests to controller methods, see [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

## <a name="calling-the-web-api-with-javascript-and-jquery"></a><span data-ttu-id="a03e9-178">Javascript 및 jQuery를 사용 하 여 Web API 호출</span><span class="sxs-lookup"><span data-stu-id="a03e9-178">Calling the Web API with Javascript and jQuery</span></span>

<span data-ttu-id="a03e9-179">이 섹션에서는 AJAX를 사용 하 여 web API를 호출 하는 HTML 페이지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-179">In this section, we'll add an HTML page that uses AJAX to call the web API.</span></span> <span data-ttu-id="a03e9-180">JQuery를 사용 하 여 AJAX를 호출 하 고 결과를 사용 하 여 페이지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-180">We'll use jQuery to make the AJAX calls and also to update the page with the results.</span></span>

<span data-ttu-id="a03e9-181">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 선택한 다음 **새 항목**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-181">In Solution Explorer, right-click the project and select **Add**, then select **New Item**.</span></span>

![](tutorial-your-first-web-api/_static/image9.png)

<span data-ttu-id="a03e9-182">**새 항목 추가** 대화 상자에서 **C#시각적 개체**아래에 있는 **웹** 노드를 선택 하 고 **HTML 페이지** 항목을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-182">In the **Add New Item** dialog, select the **Web** node under **Visual C#**, and then select the **HTML Page** item.</span></span> <span data-ttu-id="a03e9-183">페이지 이름을 index. html&quot;로 &quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-183">Name the page &quot;index.html&quot;.</span></span>

![](tutorial-your-first-web-api/_static/image10.png)

<span data-ttu-id="a03e9-184">이 파일의 모든 항목을 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-184">Replace everything in this file with the following:</span></span>

[!code-html[Main](tutorial-your-first-web-api/samples/sample3.html)]

<span data-ttu-id="a03e9-185">여러 가지 방법으로 jQuery를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-185">There are several ways to get jQuery.</span></span> <span data-ttu-id="a03e9-186">이 예제에서는 [Microsoft AJAX CDN](../../../ajax/cdn/overview.md)을 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-186">In this example, I used the [Microsoft Ajax CDN](../../../ajax/cdn/overview.md).</span></span> <span data-ttu-id="a03e9-187">또한 [http://jquery.com/](http://jquery.com/)에서 다운로드할 수 있으며, ASP.NET "Web API" 프로젝트 템플릿에는 jQuery도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-187">You can also download it from [http://jquery.com/](http://jquery.com/), and the ASP.NET "Web API" project template includes jQuery as well.</span></span>

### <a name="getting-a-list-of-products"></a><span data-ttu-id="a03e9-188">제품 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="a03e9-188">Getting a List of Products</span></span>

<span data-ttu-id="a03e9-189">제품 목록을 가져오려면 HTTP GET 요청을 &quot;/api/products&quot;보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-189">To get a list of products, send an HTTP GET request to &quot;/api/products&quot;.</span></span>

<span data-ttu-id="a03e9-190">JQuery [Getjson](http://api.jquery.com/jQuery.getJSON/) 함수는 AJAX 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-190">The jQuery [getJSON](http://api.jquery.com/jQuery.getJSON/) function sends an AJAX request.</span></span> <span data-ttu-id="a03e9-191">For response에 JSON 개체의 배열이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-191">For response contains array of JSON objects.</span></span> <span data-ttu-id="a03e9-192">`done` 함수는 요청이 성공 하는 경우 호출 되는 콜백을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-192">The `done` function specifies a callback that is called if the request succeeds.</span></span> <span data-ttu-id="a03e9-193">콜백에서 제품 정보를 사용 하 여 DOM을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-193">In the callback, we update the DOM with the product information.</span></span>

[!code-html[Main](tutorial-your-first-web-api/samples/sample4.html)]

### <a name="getting-a-product-by-id"></a><span data-ttu-id="a03e9-194">ID로 제품 가져오기</span><span class="sxs-lookup"><span data-stu-id="a03e9-194">Getting a Product By ID</span></span>

<span data-ttu-id="a03e9-195">ID로 제품을 가져오려면 HTTP GET 요청을 &quot;/api/products/*id*&quot;보냅니다. 여기서 *ID* 는 제품 id입니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-195">To get a product by ID, send an HTTP GET request to &quot;/api/products/*id*&quot;, where *id* is the product ID.</span></span>

[!code-javascript[Main](tutorial-your-first-web-api/samples/sample5.js)]

<span data-ttu-id="a03e9-196">AJAX 요청을 보내기 위해 `getJSON`를 호출 하지만 이번에는 요청 URI에 ID를 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-196">We still call `getJSON` to send the AJAX request, but this time we put the ID in the request URI.</span></span> <span data-ttu-id="a03e9-197">이 요청의 응답은 단일 제품의 JSON 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-197">The response from this request is a JSON representation of a single product.</span></span>

## <a name="running-the-application"></a><span data-ttu-id="a03e9-198">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="a03e9-198">Running the Application</span></span>

<span data-ttu-id="a03e9-199">F5 키를 눌러 애플리케이션 디버깅을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-199">Press F5 to start debugging the application.</span></span> <span data-ttu-id="a03e9-200">웹 페이지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-200">The web page should look like the following:</span></span>

![](tutorial-your-first-web-api/_static/image11.png)

<span data-ttu-id="a03e9-201">ID로 제품을 가져오려면 ID를 입력 하 고 검색을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-201">To get a product by ID, enter the ID and click Search:</span></span>

![](tutorial-your-first-web-api/_static/image12.png)

<span data-ttu-id="a03e9-202">잘못 된 ID를 입력 하면 서버에서 HTTP 오류가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-202">If you enter an invalid ID, the server returns an HTTP error:</span></span>

![](tutorial-your-first-web-api/_static/image13.png)

## <a name="using-f12-to-view-the-http-request-and-response"></a><span data-ttu-id="a03e9-203">F12 키를 사용 하 여 HTTP 요청 및 응답 보기</span><span class="sxs-lookup"><span data-stu-id="a03e9-203">Using F12 to View the HTTP Request and Response</span></span>

<span data-ttu-id="a03e9-204">HTTP 서비스를 사용 하는 경우 HTTP 요청 및 요청 메시지를 확인 하는 것이 매우 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-204">When you are working with an HTTP service, it can be very useful to see the HTTP request and request messages.</span></span> <span data-ttu-id="a03e9-205">Internet Explorer 9의 F12 개발자 도구를 사용 하 여이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-205">You can do this by using the F12 developer tools in Internet Explorer 9.</span></span> <span data-ttu-id="a03e9-206">Internet Explorer 9에서 **F12** 키를 눌러 도구를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-206">From Internet Explorer 9, press **F12** to open the tools.</span></span> <span data-ttu-id="a03e9-207">**네트워크** 탭을 클릭 하 고 **캡처 시작**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-207">Click the **Network** tab and press **Start Capturing**.</span></span> <span data-ttu-id="a03e9-208">이제 웹 페이지로 돌아가 **F5** 키를 눌러 웹 페이지를 다시 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-208">Now go back to the web page and press **F5** to reload the web page.</span></span> <span data-ttu-id="a03e9-209">Internet Explorer는 브라우저와 웹 서버 간의 HTTP 트래픽을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-209">Internet Explorer will capture the HTTP traffic between the browser and the web server.</span></span> <span data-ttu-id="a03e9-210">요약 보기에는 페이지에 대 한 모든 네트워크 트래픽이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-210">The summary view shows all the network traffic for a page:</span></span>

![](tutorial-your-first-web-api/_static/image14.png)

<span data-ttu-id="a03e9-211">상대 URI "api/products/" 항목을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-211">Locate the entry for the relative URI "api/products/".</span></span> <span data-ttu-id="a03e9-212">이 항목을 선택 하 고 **자세히 보기로 이동을**클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-212">Select this entry and click **Go to detailed view**.</span></span> <span data-ttu-id="a03e9-213">자세히 보기에는 요청 및 응답 헤더와 본문을 볼 수 있는 탭이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-213">In the detail view, there are tabs to view the request and response headers and bodies.</span></span> <span data-ttu-id="a03e9-214">예를 들어 **요청 헤더** 탭을 클릭 하면 클라이언트가 Accept 헤더에 &quot;application/json&quot; 요청한 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-214">For example, if you click the **Request headers** tab, you can see that the client requested &quot;application/json&quot; in the Accept header.</span></span>

![](tutorial-your-first-web-api/_static/image15.png)

<span data-ttu-id="a03e9-215">응답 본문 탭을 클릭 하면 제품 목록이 JSON으로 serialize 된 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-215">If you click the Response body tab, you can see how the product list was serialized to JSON.</span></span> <span data-ttu-id="a03e9-216">다른 브라우저는 비슷한 기능을가지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-216">Other browsers have similar functionality.</span></span> <span data-ttu-id="a03e9-217">또 다른 유용한 도구는 [Fiddler](http://www.fiddler2.com/fiddler2/)웹 디버깅 프록시입니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-217">Another useful tool is [Fiddler](http://www.fiddler2.com/fiddler2/), a web debugging proxy.</span></span> <span data-ttu-id="a03e9-218">Fiddler를 사용 하 여 HTTP 트래픽을 볼 수 있으며 요청에서 HTTP 헤더에 대 한 모든 권한을 제공 하는 HTTP 요청을 작성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-218">You can use Fiddler to view your HTTP traffic, and also to compose HTTP requests, which gives you full control over the HTTP headers in the request.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="a03e9-219">Azure에서 실행 되는이 앱 확인</span><span class="sxs-lookup"><span data-stu-id="a03e9-219">See this App Running on Azure</span></span>

<span data-ttu-id="a03e9-220">완료 된 사이트가 라이브 웹 앱으로 실행 되 고 있는지 확인 하 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="a03e9-220">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="a03e9-221">다음 단추를 클릭 하기만 하면 Azure 계정에 전체 버전의 앱을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-221">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](https://azuredeploy.net/deploybutton.png)](https://deploy.azure.com/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebAPI-ProductsApp#/form/setup)

<span data-ttu-id="a03e9-222">Azure에이 솔루션을 배포 하려면 Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-222">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="a03e9-223">계정이 아직 없는 경우 다음과 같은 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-223">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="a03e9-224">[무료로 azure 계정 열기](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) -유료 azure 서비스를 사용 하는 데 사용할 수 있는 크레딧을 확보 하 고, 사용한 후에도 계정을 유지 하 고 무료 Azure 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-224">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="a03e9-225">[Msdn 구독자 혜택 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -msdn 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03e9-225">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a03e9-226">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a03e9-226">Next Steps</span></span>

- <span data-ttu-id="a03e9-227">POST, PUT 및 DELETE 작업을 지원 하 고 데이터베이스에 대 한 쓰기를 지 원하는 HTTP 서비스의 전체 예제는 [Entity Framework 6에서 WEB API 2 사용](../data/using-web-api-with-entity-framework/part-1.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a03e9-227">For a more complete example of an HTTP service that supports POST, PUT, and DELETE actions and writes to a database, see [Using Web API 2 with Entity Framework 6](../data/using-web-api-with-entity-framework/part-1.md).</span></span>
- <span data-ttu-id="a03e9-228">HTTP 서비스를 기반으로 유체 및 응답성이 뛰어난 웹 응용 프로그램을 만드는 방법에 대 한 자세한 내용은 [ASP.NET Single Page Application](../../../single-page-application/index.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a03e9-228">For more about creating fluid and responsive web applications on top of an HTTP service, see [ASP.NET Single Page Application](../../../single-page-application/index.md).</span></span>
- <span data-ttu-id="a03e9-229">Azure App Service에 Visual Studio 웹 프로젝트를 배포 하는 방법에 대 한 자세한 내용은 [Azure App Service에서 ASP.NET 웹 앱 만들기](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a03e9-229">For information about how to deploy a Visual Studio web project to Azure App Service, see [Create an ASP.NET web app in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span>
