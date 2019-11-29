---
uid: web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
title: ASP.NET Web API 1-ASP.NET 4.x에서 CRUD 작업을 사용 하도록 설정
author: MikeWasson
description: 자습서에서는 ASP.NET 4.x의 ASP.NET Web API을 사용 하 여 HTTP 서비스에서 CRUD 작업을 지 원하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 01/28/2012
ms.custom: seoapril2019
ms.assetid: c125ca47-606a-4d6f-a1fc-1fc62928af93
msc.legacyurl: /web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
msc.type: authoredcontent
ms.openlocfilehash: a096fd1c54df33b40115907a5c2517b2e3fec5b8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600332"
---
# <a name="enabling-crud-operations-in-aspnet-web-api-1"></a><span data-ttu-id="65512-103">ASP.NET Web API 1에서 CRUD 작업 사용</span><span class="sxs-lookup"><span data-stu-id="65512-103">Enabling CRUD Operations in ASP.NET Web API 1</span></span>

<span data-ttu-id="65512-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="65512-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="65512-105">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="65512-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-c4761894)

> <span data-ttu-id="65512-106">이 자습서에서는 ASP.NET 4.x의 ASP.NET Web API을 사용 하 여 HTTP 서비스에서 CRUD 작업을 지 원하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="65512-106">This tutorial shows how to support CRUD operations in an HTTP service using ASP.NET Web API for ASP.NET 4.x.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="65512-107">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="65512-107">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="65512-108">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="65512-108">Visual Studio 2012</span></span>
> - <span data-ttu-id="65512-109">Web API 1 (Web API 2 에서도 작동)</span><span class="sxs-lookup"><span data-stu-id="65512-109">Web API 1 (also works with Web API 2)</span></span>

<span data-ttu-id="65512-110">CRUD는 네 가지 기본 데이터베이스 작업 인 &quot;만들기, 읽기, 업데이트 및 삭제&quot;를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="65512-110">CRUD stands for &quot;Create, Read, Update, and Delete,&quot; which are the four basic database operations.</span></span> <span data-ttu-id="65512-111">또한 대부분의 HTTP 서비스는 REST 또는 REST Api를 통해 CRUD 작업을 모델링 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-111">Many HTTP services also model CRUD operations through REST or REST-like APIs.</span></span>

<span data-ttu-id="65512-112">이 자습서에서는 매우 간단한 웹 API를 빌드하여 제품 목록을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-112">In this tutorial, you will build a very simple web API to manage a list of products.</span></span> <span data-ttu-id="65512-113">각 제품에는 이름, 가격 및 범주 (예: &quot;장난감&quot; 또는 &quot;하드웨어&quot;)와 제품 ID가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65512-113">Each product will contain a name, price, and category (such as &quot;toys&quot; or &quot;hardware&quot;), plus a product ID.</span></span>

<span data-ttu-id="65512-114">Products API는 다음 메서드를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-114">The products API will expose following methods.</span></span>

| <span data-ttu-id="65512-115">동작</span><span class="sxs-lookup"><span data-stu-id="65512-115">Action</span></span> | <span data-ttu-id="65512-116">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="65512-116">HTTP method</span></span> | <span data-ttu-id="65512-117">상대 URI</span><span class="sxs-lookup"><span data-stu-id="65512-117">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="65512-118">모든 제품 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="65512-118">Get a list of all products</span></span> | <span data-ttu-id="65512-119">가져오기</span><span class="sxs-lookup"><span data-stu-id="65512-119">GET</span></span> | <span data-ttu-id="65512-120">/api/제품</span><span class="sxs-lookup"><span data-stu-id="65512-120">/api/products</span></span> |
| <span data-ttu-id="65512-121">ID로 제품 가져오기</span><span class="sxs-lookup"><span data-stu-id="65512-121">Get a product by ID</span></span> | <span data-ttu-id="65512-122">가져오기</span><span class="sxs-lookup"><span data-stu-id="65512-122">GET</span></span> | <span data-ttu-id="65512-123">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="65512-123">/api/products/*id*</span></span> |
| <span data-ttu-id="65512-124">범주별로 제품 가져오기</span><span class="sxs-lookup"><span data-stu-id="65512-124">Get a product by category</span></span> | <span data-ttu-id="65512-125">가져오기</span><span class="sxs-lookup"><span data-stu-id="65512-125">GET</span></span> | <span data-ttu-id="65512-126">/api/products? 범주 =*범주*</span><span class="sxs-lookup"><span data-stu-id="65512-126">/api/products?category=*category*</span></span> |
| <span data-ttu-id="65512-127">새 제품 만들기</span><span class="sxs-lookup"><span data-stu-id="65512-127">Create a new product</span></span> | <span data-ttu-id="65512-128">올리기</span><span class="sxs-lookup"><span data-stu-id="65512-128">POST</span></span> | <span data-ttu-id="65512-129">/api/제품</span><span class="sxs-lookup"><span data-stu-id="65512-129">/api/products</span></span> |
| <span data-ttu-id="65512-130">제품 업데이트</span><span class="sxs-lookup"><span data-stu-id="65512-130">Update a product</span></span> | <span data-ttu-id="65512-131">PUT</span><span class="sxs-lookup"><span data-stu-id="65512-131">PUT</span></span> | <span data-ttu-id="65512-132">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="65512-132">/api/products/*id*</span></span> |
| <span data-ttu-id="65512-133">제품 삭제</span><span class="sxs-lookup"><span data-stu-id="65512-133">Delete a product</span></span> | <span data-ttu-id="65512-134">Delete</span><span class="sxs-lookup"><span data-stu-id="65512-134">DELETE</span></span> | <span data-ttu-id="65512-135">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="65512-135">/api/products/*id*</span></span> |

<span data-ttu-id="65512-136">일부 Uri에는 경로에 제품 ID가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65512-136">Notice that some of the URIs include the product ID in path.</span></span> <span data-ttu-id="65512-137">예를 들어 ID가 28 인 제품을 가져오기 위해 클라이언트는 `http://hostname/api/products/28`에 대 한 GET 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="65512-137">For example, to get the product whose ID is 28, the client sends a GET request for `http://hostname/api/products/28`.</span></span>

### <a name="resources"></a><span data-ttu-id="65512-138">자료</span><span class="sxs-lookup"><span data-stu-id="65512-138">Resources</span></span>

<span data-ttu-id="65512-139">제품 API는 다음 두 리소스 유형에 대 한 Uri를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-139">The products API defines URIs for two resource types:</span></span>

| <span data-ttu-id="65512-140">리소스</span><span class="sxs-lookup"><span data-stu-id="65512-140">Resource</span></span> | <span data-ttu-id="65512-141">URI</span><span class="sxs-lookup"><span data-stu-id="65512-141">URI</span></span> |
| --- | --- |
| <span data-ttu-id="65512-142">모든 제품의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="65512-142">The list of all the products.</span></span> | <span data-ttu-id="65512-143">/api/제품</span><span class="sxs-lookup"><span data-stu-id="65512-143">/api/products</span></span> |
| <span data-ttu-id="65512-144">개별 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="65512-144">An individual product.</span></span> | <span data-ttu-id="65512-145">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="65512-145">/api/products/*id*</span></span> |

### <a name="methods"></a><span data-ttu-id="65512-146">메서드</span><span class="sxs-lookup"><span data-stu-id="65512-146">Methods</span></span>

<span data-ttu-id="65512-147">다음과 같이 네 가지 주요 HTTP 메서드 (GET, PUT, POST 및 DELETE)를 CRUD 작업에 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65512-147">The four main HTTP methods (GET, PUT, POST, and DELETE) can be mapped to CRUD operations as follows:</span></span>

- <span data-ttu-id="65512-148">GET은 지정 된 URI에서 리소스의 표현을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-148">GET retrieves the representation of the resource at a specified URI.</span></span> <span data-ttu-id="65512-149">GET은 서버에 부작용이 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-149">GET should have no side effects on the server.</span></span>
- <span data-ttu-id="65512-150">지정 된 URI에 리소스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-150">PUT updates a resource at a specified URI.</span></span> <span data-ttu-id="65512-151">서버에서 클라이언트가 새 Uri를 지정할 수 있도록 허용 하는 경우 PUT을 사용 하 여 지정 된 URI에 새 리소스를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65512-151">PUT can also be used to create a new resource at a specified URI, if the server allows clients to specify new URIs.</span></span> <span data-ttu-id="65512-152">이 자습서의 경우 API는 PUT을 통해 만들기를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="65512-152">For this tutorial, the API will not support creation through PUT.</span></span>
- <span data-ttu-id="65512-153">POST는 새 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="65512-153">POST creates a new resource.</span></span> <span data-ttu-id="65512-154">서버는 새 개체에 대 한 URI를 할당 하 고이 URI를 응답 메시지의 일부로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-154">The server assigns the URI for the new object and returns this URI as part of the response message.</span></span>
- <span data-ttu-id="65512-155">DELETE 지정 된 URI에서 리소스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-155">DELETE deletes a resource at a specified URI.</span></span>

<span data-ttu-id="65512-156">참고: PUT 메서드는 전체 제품 엔터티를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-156">Note: The PUT method replaces the entire product entity.</span></span> <span data-ttu-id="65512-157">즉, 클라이언트는 업데이트 된 제품의 전체 표현을 전송 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-157">That is, the client is expected to send a complete representation of the updated product.</span></span> <span data-ttu-id="65512-158">부분 업데이트를 지원 하려는 경우 패치 방법이 선호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65512-158">If you want to support partial updates, the PATCH method is preferred.</span></span> <span data-ttu-id="65512-159">이 자습서에서는 패치를 구현 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="65512-159">This tutorial does not implement PATCH.</span></span>

## <a name="create-a-new-web-api-project"></a><span data-ttu-id="65512-160">새 Web API 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="65512-160">Create a New Web API Project</span></span>

<span data-ttu-id="65512-161">먼저 Visual Studio를 실행 하 고 **시작** 페이지에서 **새 프로젝트** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-161">Start by running Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="65512-162">또는 **파일** 메뉴에서 **새로 만들기** , **프로젝트**를 차례로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-162">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="65512-163">**템플릿** 창에서 **설치 된 템플릿** 을 선택 하 고  **C# 시각적** 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-163">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="65512-164">**시각적 개체 C#** 에서 **웹**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-164">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="65512-165">프로젝트 템플릿 목록에서 **ASP.NET MVC 4 웹 응용 프로그램**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-165">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="65512-166">프로젝트 이름을 &quot;제품 저장소로&quot; 하 고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-166">Name the project &quot;ProductStore&quot; and click **OK**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image1.png)

<span data-ttu-id="65512-167">**New ASP.NET MVC 4 프로젝트** 대화 상자에서 **Web API** 를 선택 하 고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-167">In the **New ASP.NET MVC 4 Project** dialog, select **Web API** and click **OK**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image2.png)

## <a name="adding-a-model"></a><span data-ttu-id="65512-168">모델 추가</span><span class="sxs-lookup"><span data-stu-id="65512-168">Adding a Model</span></span>

<span data-ttu-id="65512-169">*모델*은 애플리케이션에서 데이터를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="65512-169">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="65512-170">ASP.NET Web API에서는 강력한 형식의 CLR 개체를 모델로 사용할 수 있으며, 자동으로 클라이언트에 대해 XML 또는 JSON으로 serialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65512-170">In ASP.NET Web API, you can use strongly typed CLR objects as models, and they will automatically be serialized to XML or JSON for the client.</span></span>

<span data-ttu-id="65512-171">제품 저장소 API의 경우 데이터는 제품으로 구성 되므로 `Product`이라는 새 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="65512-171">For the ProductStore API, our data consists of products, so we'll create a new class named `Product`.</span></span>

<span data-ttu-id="65512-172">솔루션 탐색기 아직 표시 되지 않으면 **보기** 메뉴를 클릭 하 고 **솔루션 탐색기**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-172">If Solution Explorer is not already visible, click the **View** menu and select **Solution Explorer**.</span></span> <span data-ttu-id="65512-173">솔루션 탐색기에서 **모델** 폴더를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-173">In Solution Explorer, right-click the **Models** folder.</span></span> <span data-ttu-id="65512-174">상황에 맞는 메뉴에서 **추가**를 선택한 다음 **클래스**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-174">From the context menu, select **Add**, then select **Class**.</span></span> <span data-ttu-id="65512-175">클래스 이름을 Product&quot;&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-175">Name the class &quot;Product&quot;.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image3.png)

<span data-ttu-id="65512-176">`Product` 클래스에 다음 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-176">Add the following properties to the `Product` class.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample1.cs)]

## <a name="adding-a-repository"></a><span data-ttu-id="65512-177">리포지토리 추가</span><span class="sxs-lookup"><span data-stu-id="65512-177">Adding a Repository</span></span>

<span data-ttu-id="65512-178">제품 컬렉션을 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-178">We need to store a collection of products.</span></span> <span data-ttu-id="65512-179">서비스 구현에서 컬렉션을 분리 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="65512-179">It's a good idea to separate the collection from our service implementation.</span></span> <span data-ttu-id="65512-180">이렇게 하면 서비스 클래스를 다시 작성 하지 않고도 백업 저장소를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65512-180">That way, we can change the backing store without rewriting the service class.</span></span> <span data-ttu-id="65512-181">이러한 종류의 디자인을 *리포지토리* 패턴 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-181">This type of design is called the *repository* pattern.</span></span> <span data-ttu-id="65512-182">먼저 리포지토리의 제네릭 인터페이스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-182">Start by defining a generic interface for the repository.</span></span>

<span data-ttu-id="65512-183">솔루션 탐색기에서 **모델** 폴더를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-183">In Solution Explorer, right-click the **Models** folder.</span></span> <span data-ttu-id="65512-184">**추가**를 선택한 다음 **새 항목**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-184">Select **Add**, then select **New Item**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image4.png)

<span data-ttu-id="65512-185">**템플릿** 창에서 **설치 된 템플릿** 을 선택 하 고 노드 C# 를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-185">In the **Templates** pane, select **Installed Templates** and expand the C# node.</span></span> <span data-ttu-id="65512-186">에서 C# **코드**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-186">Under C#, select **Code**.</span></span> <span data-ttu-id="65512-187">코드 템플릿 목록에서 **인터페이스**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-187">In the list of code templates, select **Interface**.</span></span> <span data-ttu-id="65512-188">인터페이스 이름을 IProductRepository&quot;로 &quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-188">Name the interface &quot;IProductRepository&quot;.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image5.png)

<span data-ttu-id="65512-189">다음 구현을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-189">Add the following implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample2.cs)]

<span data-ttu-id="65512-190">이제 &quot;ProductRepository 라는 모델 폴더에 다른 클래스를 추가 합니다.&quot;이 클래스는 `IProductRepository` 인터페이스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-190">Now add another class to the Models folder, named &quot;ProductRepository.&quot; This class will implement the `IProductRepository` interface.</span></span> <span data-ttu-id="65512-191">다음 구현을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-191">Add the following implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample3.cs)]

<span data-ttu-id="65512-192">리포지토리는 로컬 메모리에 목록을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-192">The repository keeps the list in local memory.</span></span> <span data-ttu-id="65512-193">이는 자습서에서 양호 하지만 실제 응용 프로그램에서는 데이터를 외부에 저장 하거나 클라우드 저장소에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-193">This is OK for a tutorial, but in a real application, you would store the data externally, either a database or in cloud storage.</span></span> <span data-ttu-id="65512-194">리포지토리 패턴을 사용 하면 나중에 구현을 더 쉽게 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65512-194">The repository pattern will make it easier to change the implementation later.</span></span>

## <a name="adding-a-web-api-controller"></a><span data-ttu-id="65512-195">Web API 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="65512-195">Adding a Web API Controller</span></span>

<span data-ttu-id="65512-196">ASP.NET MVC를 사용 하 여 작업 한 경우 이미 컨트롤러에 대해 잘 알고 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="65512-196">If you have worked with ASP.NET MVC, then you are already familiar with controllers.</span></span> <span data-ttu-id="65512-197">ASP.NET Web API에서 *컨트롤러* 는 클라이언트의 HTTP 요청을 처리 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="65512-197">In ASP.NET Web API, a *controller* is a class that handles HTTP requests from the client.</span></span> <span data-ttu-id="65512-198">새 프로젝트 마법사는 프로젝트를 만들 때 두 개의 컨트롤러를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="65512-198">The New Project wizard created two controllers for you when it created the project.</span></span> <span data-ttu-id="65512-199">이를 확인 하려면 솔루션 탐색기의 컨트롤러 폴더를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-199">To see them, expand the Controllers folder in Solution Explorer.</span></span>

- <span data-ttu-id="65512-200">HomeController는 기존의 ASP.NET MVC 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="65512-200">HomeController is a traditional ASP.NET MVC controller.</span></span> <span data-ttu-id="65512-201">이는 사이트에 대 한 HTML 페이지의 서비스를 담당 하며 웹 API와 직접 관련 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="65512-201">It is responsible for serving HTML pages for the site, and is not directly related to our web API.</span></span>
- <span data-ttu-id="65512-202">Valuecontroller는 예제 WebAPI controller입니다.</span><span class="sxs-lookup"><span data-stu-id="65512-202">ValuesController is an example WebAPI controller.</span></span>

<span data-ttu-id="65512-203">솔루션 탐색기에서 파일을 마우스 오른쪽 단추로 클릭 하 고 삭제를 선택 하 여 다음으로 이동 하 여 Valuecontroller를 삭제 **합니다.**</span><span class="sxs-lookup"><span data-stu-id="65512-203">Go ahead and delete ValuesController, by right-clicking the file in Solution Explorer and selecting **Delete.**</span></span> <span data-ttu-id="65512-204">이제 다음과 같이 새 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-204">Now add a new controller, as follows:</span></span>

<span data-ttu-id="65512-205">**솔루션 탐색기**에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-205">In **Solution Explorer**, right-click the Controllers folder.</span></span> <span data-ttu-id="65512-206">**추가** 를 선택한 다음 **컨트롤러**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-206">Select **Add** and then select **Controller**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image6.png)

<span data-ttu-id="65512-207">**컨트롤러 추가** 마법사에서 컨트롤러 이름을 ProductsController&quot;로 &quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-207">In the **Add Controller** wizard, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="65512-208">**템플릿** 드롭다운 목록에서 **빈 API 컨트롤러**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-208">In the **Template** drop-down list, select **Empty API Controller**.</span></span> <span data-ttu-id="65512-209">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-209">Then click **Add**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image7.png)

> [!NOTE]
> <span data-ttu-id="65512-210">컨트롤러를 컨트롤러 라는 폴더에 배치할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="65512-210">It is not necessary to put your controllers into a folder named Controllers.</span></span> <span data-ttu-id="65512-211">폴더 이름은 중요 하지 않습니다. 단순히 소스 파일을 구성 하는 편리한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="65512-211">The folder name is not important; it is simply a convenient way to organize your source files.</span></span>

<span data-ttu-id="65512-212">**컨트롤러 추가** 마법사가 Controllers 폴더에 ProductsController.cs 라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="65512-212">The **Add Controller** wizard will create a file named ProductsController.cs in the Controllers folder.</span></span> <span data-ttu-id="65512-213">이 파일이 아직 열려 있지 않으면 파일을 두 번 클릭 하 여 엽니다.</span><span class="sxs-lookup"><span data-stu-id="65512-213">If this file is not open already, double-click the file to open it.</span></span> <span data-ttu-id="65512-214">다음 **using** 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-214">Add the following **using** statement:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample4.cs)]

<span data-ttu-id="65512-215">**IProductRepository** 인스턴스를 보유 하는 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-215">Add a field that holds an **IProductRepository** instance.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample5.cs)]

> [!NOTE]
> <span data-ttu-id="65512-216">컨트롤러를 `IProductRepository`의 특정 구현에 연결 하기 때문에 컨트롤러에서 `new ProductRepository()`를 호출 하는 것은 최적의 디자인이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="65512-216">Calling `new ProductRepository()` in the controller is not the best design, because it ties the controller to a particular implementation of `IProductRepository`.</span></span> <span data-ttu-id="65512-217">더 나은 접근 방법은 [웹 API 종속성 확인자 사용](../advanced/dependency-injection.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="65512-217">For a better approach, see [Using the Web API Dependency Resolver](../advanced/dependency-injection.md).</span></span>

## <a name="getting-a-resource"></a><span data-ttu-id="65512-218">리소스 가져오기</span><span class="sxs-lookup"><span data-stu-id="65512-218">Getting a Resource</span></span>

<span data-ttu-id="65512-219">제품 저장소 API는 여러 &quot;&quot; 작업을 HTTP GET 메서드로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-219">The ProductStore API will expose several &quot;read&quot; actions as HTTP GET methods.</span></span> <span data-ttu-id="65512-220">각 작업은 `ProductsController` 클래스의 메서드에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-220">Each action will correspond to a method in the `ProductsController` class.</span></span>

| <span data-ttu-id="65512-221">동작</span><span class="sxs-lookup"><span data-stu-id="65512-221">Action</span></span> | <span data-ttu-id="65512-222">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="65512-222">HTTP method</span></span> | <span data-ttu-id="65512-223">상대 URI</span><span class="sxs-lookup"><span data-stu-id="65512-223">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="65512-224">모든 제품 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="65512-224">Get a list of all products</span></span> | <span data-ttu-id="65512-225">가져오기</span><span class="sxs-lookup"><span data-stu-id="65512-225">GET</span></span> | <span data-ttu-id="65512-226">/api/제품</span><span class="sxs-lookup"><span data-stu-id="65512-226">/api/products</span></span> |
| <span data-ttu-id="65512-227">ID로 제품 가져오기</span><span class="sxs-lookup"><span data-stu-id="65512-227">Get a product by ID</span></span> | <span data-ttu-id="65512-228">가져오기</span><span class="sxs-lookup"><span data-stu-id="65512-228">GET</span></span> | <span data-ttu-id="65512-229">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="65512-229">/api/products/*id*</span></span> |
| <span data-ttu-id="65512-230">범주별로 제품 가져오기</span><span class="sxs-lookup"><span data-stu-id="65512-230">Get a product by category</span></span> | <span data-ttu-id="65512-231">가져오기</span><span class="sxs-lookup"><span data-stu-id="65512-231">GET</span></span> | <span data-ttu-id="65512-232">/api/products? 범주 =*범주*</span><span class="sxs-lookup"><span data-stu-id="65512-232">/api/products?category=*category*</span></span> |

<span data-ttu-id="65512-233">모든 제품 목록을 가져오려면 `ProductsController` 클래스에 다음 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-233">To get the list of all products, add this method to the `ProductsController` class:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample6.cs)]

<span data-ttu-id="65512-234">메서드 이름은 GET&quot;&quot;으로 시작 되므로 규칙에 따라 GET 요청에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="65512-234">The method name starts with &quot;Get&quot;, so by convention it maps to GET requests.</span></span> <span data-ttu-id="65512-235">또한 메서드에는 매개 변수가 없기 때문에 경로에 *&quot;id&quot;* 세그먼트가 포함 되지 않은 URI에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="65512-235">Also, because the method has no parameters, it maps to a URI that does not contain an *&quot;id&quot;* segment in the path.</span></span>

<span data-ttu-id="65512-236">ID로 제품을 가져오려면 `ProductsController` 클래스에 다음 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-236">To get a product by ID, add this method to the `ProductsController` class:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample7.cs)]

<span data-ttu-id="65512-237">또한이 메서드 이름은 &quot;Get&quot;로 시작 하지만 메서드에 *id*라는 매개 변수가 있습니다. 이 매개 변수는 URI 경로의 &quot;id&quot; 세그먼트로 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="65512-237">This method name also starts with &quot;Get&quot;, but the method has a parameter named *id*. This parameter is mapped to the &quot;id&quot; segment of the URI path.</span></span> <span data-ttu-id="65512-238">ASP.NET Web API 프레임 워크는 매개 변수에 대해 ID를 올바른 데이터 형식 (**int**)으로 자동 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-238">The ASP.NET Web API framework automatically converts the ID to the correct data type (**int**) for the parameter.</span></span>

<span data-ttu-id="65512-239">GetProduct 메서드는 *id* 가 유효 하지 않은 경우 **HttpResponseException** 형식의 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-239">The GetProduct method throws an exception of type **HttpResponseException** if *id* is not valid.</span></span> <span data-ttu-id="65512-240">이 예외는 프레임 워크에서 404 (찾을 수 없음) 오류로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65512-240">This exception will be translated by the framework into a 404 (Not Found) error.</span></span>

<span data-ttu-id="65512-241">마지막으로, 범주를 기준으로 제품을 찾는 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-241">Finally, add a method to find products by category:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample8.cs)]

<span data-ttu-id="65512-242">요청 URI에 쿼리 문자열이 있는 경우 Web API는 컨트롤러 메서드의 매개 변수와 쿼리 매개 변수를 일치 시 키 려 고 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-242">If the request URI has a query string, Web API tries to match the query parameters to parameters on the controller method.</span></span> <span data-ttu-id="65512-243">따라서 "api/products? category =*category*" 형식의 URI가이 메서드에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="65512-243">Therefore, a URI of the form "api/products?category=*category*" will map to this method.</span></span>

## <a name="creating-a-resource"></a><span data-ttu-id="65512-244">리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="65512-244">Creating a Resource</span></span>

<span data-ttu-id="65512-245">다음으로 `ProductsController` 클래스에 메서드를 추가 하 여 새 제품을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="65512-245">Next, we'll add a method to the `ProductsController` class to create a new product.</span></span> <span data-ttu-id="65512-246">다음은 메서드를 간단 하 게 구현한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="65512-246">Here is a simple implementation of the method:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample9.cs)]

<span data-ttu-id="65512-247">이 메서드에 대 한 두 가지 사항을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-247">Note two things about this method:</span></span>

- <span data-ttu-id="65512-248">메서드 이름은 &quot;&quot;으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-248">The method name starts with &quot;Post...&quot;.</span></span> <span data-ttu-id="65512-249">새 제품을 만들기 위해 클라이언트는 HTTP POST 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="65512-249">To create a new product, the client sends an HTTP POST request.</span></span>
- <span data-ttu-id="65512-250">메서드는 Product 형식의 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-250">The method takes a parameter of type Product.</span></span> <span data-ttu-id="65512-251">Web API에서 복합 형식이 포함 된 매개 변수는 요청 본문에서 deserialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65512-251">In Web API, parameters with complex types are deserialized from the request body.</span></span> <span data-ttu-id="65512-252">따라서 클라이언트는 product 개체의 serialize 된 표현을 XML 또는 JSON 형식으로 보낼 것으로 간주 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-252">Therefore, we expect the client to send a serialized representation of a product object, in either XML or JSON format.</span></span>

<span data-ttu-id="65512-253">이 구현은 작동 하지만 완전히 완전 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="65512-253">This implementation will work, but it is not quite complete.</span></span> <span data-ttu-id="65512-254">이상적으로 HTTP 응답에는 다음과 같은 내용이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65512-254">Ideally, we would like the HTTP response to include the following:</span></span>

- <span data-ttu-id="65512-255">**응답 코드:** 기본적으로 Web API 프레임 워크는 응답 상태 코드를 200 (OK)로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-255">**Response code:** By default, the Web API framework sets the response status code to 200 (OK).</span></span> <span data-ttu-id="65512-256">하지만 HTTP/1.1 프로토콜에 따라 POST 요청으로 인해 리소스가 생성 될 때 서버는 상태 201 (만듦)로 회신 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-256">But according to the HTTP/1.1 protocol, when a POST request results in the creation of a resource, the server should reply with status 201 (Created).</span></span>
- <span data-ttu-id="65512-257">**위치:** 서버는 리소스를 만들 때 응답의 Location 헤더에 새 리소스의 URI를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-257">**Location:** When the server creates a resource, it should include the URI of the new resource in the Location header of the response.</span></span>

<span data-ttu-id="65512-258">ASP.NET Web API를 사용 하면 HTTP 응답 메시지를 쉽게 조작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65512-258">ASP.NET Web API makes it easy to manipulate the HTTP response message.</span></span> <span data-ttu-id="65512-259">다음은 향상 된 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="65512-259">Here is the improved implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample10.cs)]

<span data-ttu-id="65512-260">이제 메서드 반환 형식은 **HttpResponseMessage**입니다.</span><span class="sxs-lookup"><span data-stu-id="65512-260">Notice that the method return type is now **HttpResponseMessage**.</span></span> <span data-ttu-id="65512-261">제품 대신 **HttpResponseMessage** 를 반환 하 여 상태 코드 및 위치 헤더를 포함 하는 HTTP 응답 메시지의 세부 정보를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65512-261">By returning an **HttpResponseMessage** instead of a Product, we can control the details of the HTTP response message, including the status code and the Location header.</span></span>

<span data-ttu-id="65512-262">**CreateResponse** 메서드는 **HttpResponseMessage** 를 만들고 Product 개체의 serialize 된 표현을 응답 메시지의 본문에 자동으로 씁니다.</span><span class="sxs-lookup"><span data-stu-id="65512-262">The **CreateResponse** method creates an **HttpResponseMessage** and automatically writes a serialized representation of the Product object into the body fo the response message.</span></span>

> [!NOTE]
> <span data-ttu-id="65512-263">이 예에서는 `Product`의 유효성을 검사 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="65512-263">This example does not validate the `Product`.</span></span> <span data-ttu-id="65512-264">모델 유효성 검사에 대 한 자세한 내용은 [ASP.NET Web API의 모델 유효성 검사](../formats-and-model-binding/model-validation-in-aspnet-web-api.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="65512-264">For information about model validation, see [Model Validation in ASP.NET Web API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span></span>

## <a name="updating-a-resource"></a><span data-ttu-id="65512-265">리소스 업데이트</span><span class="sxs-lookup"><span data-stu-id="65512-265">Updating a Resource</span></span>

<span data-ttu-id="65512-266">PUT을 사용 하 여 제품을 업데이트 하는 것은 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-266">Updating a product with PUT is straightforward:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample11.cs)]

<span data-ttu-id="65512-267">메서드 이름은 &quot;Put ...&quot;로 시작 하므로 Web API는이를 일치 시켜 요청을 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-267">The method name starts with &quot;Put...&quot;, so Web API matches it to PUT requests.</span></span> <span data-ttu-id="65512-268">메서드는 제품 ID와 업데이트 된 제품의 두 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-268">The method takes two parameters, the product ID and the updated product.</span></span> <span data-ttu-id="65512-269">*Id* 매개 변수는 URI 경로에서 가져오고 *product* 매개 변수는 요청 본문에서 deserialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65512-269">The *id* parameter is taken from the URI path, and the *product* parameter is deserialized from the request body.</span></span> <span data-ttu-id="65512-270">기본적으로 ASP.NET Web API 프레임 워크는 요청 본문의 경로 및 복합 형식에서 단순 매개 변수 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-270">By default, the ASP.NET Web API framework takes simple parameter types from the route and complex types from the request body.</span></span>

## <a name="deleting-a-resource"></a><span data-ttu-id="65512-271">리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="65512-271">Deleting a Resource</span></span>

<span data-ttu-id="65512-272">리소스를 삭제 하려면 "Delete ..."를 정의 합니다. 방법이.</span><span class="sxs-lookup"><span data-stu-id="65512-272">To delete a resource, define a "Delete..." method.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample12.cs)]

<span data-ttu-id="65512-273">삭제 요청이 성공 하면 상태를 설명 하는 엔터티 본문과 함께 상태 200 (OK)을 반환할 수 있습니다. 삭제가 아직 보류 중인 경우 상태 202 (수락 됨) 또는 상태 204 (콘텐츠 없음) (엔터티 본문이 없음)입니다.</span><span class="sxs-lookup"><span data-stu-id="65512-273">If a DELETE request succeeds, it can return status 200 (OK) with an entity-body that describes the status; status 202 (Accepted) if the deletion is still pending; or status 204 (No Content) with no entity body.</span></span> <span data-ttu-id="65512-274">이 경우 `DeleteProduct` 메서드에 `void` 반환 형식이 있으므로 ASP.NET Web API에서 자동으로이를 상태 코드 204 (내용 없음)로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="65512-274">In this case, the `DeleteProduct` method has a `void` return type, so ASP.NET Web API automatically translates this into status code 204 (No Content).</span></span>
