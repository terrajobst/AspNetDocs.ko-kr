---
uid: web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
title: ASP.NET Web API 1-ASP.NET에서에서 CRUD 작업을 사용 하도록 설정 하면 4.x
author: MikeWasson
description: 자습서에서는 ASP.NET Web API를 사용 하 여 ASP.NET에 대 한 HTTP 서비스에서 CRUD 작업을 지 원하는 방법을 보여 줍니다. 4.x 합니다.
ms.author: riande
ms.date: 01/28/2012
ms.custom: seoapril2019
ms.assetid: c125ca47-606a-4d6f-a1fc-1fc62928af93
msc.legacyurl: /web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
msc.type: authoredcontent
ms.openlocfilehash: 855c3fa35d82173c87d13adb51e10fd13698ade5
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59381356"
---
# <a name="enabling-crud-operations-in-aspnet-web-api-1"></a><span data-ttu-id="6a7e6-103">ASP.NET Web API 1에서에서 CRUD 작업을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="6a7e6-103">Enabling CRUD Operations in ASP.NET Web API 1</span></span>

<span data-ttu-id="6a7e6-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="6a7e6-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="6a7e6-105">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="6a7e6-105">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-c4761894)

> <span data-ttu-id="6a7e6-106">이 자습서에서는 ASP.NET Web API를 사용 하 여 ASP.NET에 대 한 HTTP 서비스에서 CRUD 작업을 지 원하는 방법을 보여 줍니다. 4.x 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-106">This tutorial shows how to support CRUD operations in an HTTP service using ASP.NET Web API for ASP.NET 4.x.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="6a7e6-107">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="6a7e6-107">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="6a7e6-108">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="6a7e6-108">Visual Studio 2012</span></span>
> - <span data-ttu-id="6a7e6-109">Web API 1 (또한 Web API 2를 사용 하 여 작동)</span><span class="sxs-lookup"><span data-stu-id="6a7e6-109">Web API 1 (also works with Web API 2)</span></span>


<span data-ttu-id="6a7e6-110">CRUD &quot;만들기, 읽기, 업데이트 및 삭제,&quot; 는 4 개의 기본 데이터베이스 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-110">CRUD stands for &quot;Create, Read, Update, and Delete,&quot; which are the four basic database operations.</span></span> <span data-ttu-id="6a7e6-111">많은 HTTP 서비스는도 비슷한 REST Api 또는 REST를 통해 CRUD 작업을 모델링합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-111">Many HTTP services also model CRUD operations through REST or REST-like APIs.</span></span>

<span data-ttu-id="6a7e6-112">이 자습서에서는 매우 간단한 web API 제품 목록을 관리를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-112">In this tutorial, you will build a very simple web API to manage a list of products.</span></span> <span data-ttu-id="6a7e6-113">각 제품 이름, 가격 및 범주에 포함 됩니다 (같은 &quot;toys&quot; 하거나 &quot;하드웨어&quot;), plus 제품 id입니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-113">Each product will contain a name, price, and category (such as &quot;toys&quot; or &quot;hardware&quot;), plus a product ID.</span></span>

<span data-ttu-id="6a7e6-114">제품 API는 다음 메서드 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-114">The products API will expose following methods.</span></span>

| <span data-ttu-id="6a7e6-115">작업</span><span class="sxs-lookup"><span data-stu-id="6a7e6-115">Action</span></span> | <span data-ttu-id="6a7e6-116">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="6a7e6-116">HTTP method</span></span> | <span data-ttu-id="6a7e6-117">상대 URI</span><span class="sxs-lookup"><span data-stu-id="6a7e6-117">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6a7e6-118">모든 제품의 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="6a7e6-118">Get a list of all products</span></span> | <span data-ttu-id="6a7e6-119">가져오기</span><span class="sxs-lookup"><span data-stu-id="6a7e6-119">GET</span></span> | <span data-ttu-id="6a7e6-120">api 제품</span><span class="sxs-lookup"><span data-stu-id="6a7e6-120">/api/products</span></span> |
| <span data-ttu-id="6a7e6-121">제품 ID 별로 가져오기</span><span class="sxs-lookup"><span data-stu-id="6a7e6-121">Get a product by ID</span></span> | <span data-ttu-id="6a7e6-122">가져오기</span><span class="sxs-lookup"><span data-stu-id="6a7e6-122">GET</span></span> | <span data-ttu-id="6a7e6-123">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="6a7e6-123">/api/products/*id*</span></span> |
| <span data-ttu-id="6a7e6-124">제품 범주별으로 가져오기</span><span class="sxs-lookup"><span data-stu-id="6a7e6-124">Get a product by category</span></span> | <span data-ttu-id="6a7e6-125">가져오기</span><span class="sxs-lookup"><span data-stu-id="6a7e6-125">GET</span></span> | <span data-ttu-id="6a7e6-126">/api/products?category=*category*</span><span class="sxs-lookup"><span data-stu-id="6a7e6-126">/api/products?category=*category*</span></span> |
| <span data-ttu-id="6a7e6-127">새 제품 만들기</span><span class="sxs-lookup"><span data-stu-id="6a7e6-127">Create a new product</span></span> | <span data-ttu-id="6a7e6-128">올리기</span><span class="sxs-lookup"><span data-stu-id="6a7e6-128">POST</span></span> | <span data-ttu-id="6a7e6-129">api 제품</span><span class="sxs-lookup"><span data-stu-id="6a7e6-129">/api/products</span></span> |
| <span data-ttu-id="6a7e6-130">제품 업데이트</span><span class="sxs-lookup"><span data-stu-id="6a7e6-130">Update a product</span></span> | <span data-ttu-id="6a7e6-131">PUT</span><span class="sxs-lookup"><span data-stu-id="6a7e6-131">PUT</span></span> | <span data-ttu-id="6a7e6-132">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="6a7e6-132">/api/products/*id*</span></span> |
| <span data-ttu-id="6a7e6-133">제품 삭제</span><span class="sxs-lookup"><span data-stu-id="6a7e6-133">Delete a product</span></span> | <span data-ttu-id="6a7e6-134">Delete</span><span class="sxs-lookup"><span data-stu-id="6a7e6-134">DELETE</span></span> | <span data-ttu-id="6a7e6-135">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="6a7e6-135">/api/products/*id*</span></span> |

<span data-ttu-id="6a7e6-136">경로 있는 제품 ID를 포함 된 Uri의 일부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-136">Notice that some of the URIs include the product ID in path.</span></span> <span data-ttu-id="6a7e6-137">예를 들어, 제품 ID가 28을 가져오려면 클라이언트에서 보냅니다 GET 요청에 대 한 `http://hostname/api/products/28`합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-137">For example, to get the product whose ID is 28, the client sends a GET request for `http://hostname/api/products/28`.</span></span>

### <a name="resources"></a><span data-ttu-id="6a7e6-138">자료</span><span class="sxs-lookup"><span data-stu-id="6a7e6-138">Resources</span></span>

<span data-ttu-id="6a7e6-139">API 제품 두 리소스 유형에 대 한 Uri를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-139">The products API defines URIs for two resource types:</span></span>

| <span data-ttu-id="6a7e6-140">리소스</span><span class="sxs-lookup"><span data-stu-id="6a7e6-140">Resource</span></span> | <span data-ttu-id="6a7e6-141">URI</span><span class="sxs-lookup"><span data-stu-id="6a7e6-141">URI</span></span> |
| --- | --- |
| <span data-ttu-id="6a7e6-142">모든 제품의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-142">The list of all the products.</span></span> | <span data-ttu-id="6a7e6-143">api 제품</span><span class="sxs-lookup"><span data-stu-id="6a7e6-143">/api/products</span></span> |
| <span data-ttu-id="6a7e6-144">개별 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-144">An individual product.</span></span> | <span data-ttu-id="6a7e6-145">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="6a7e6-145">/api/products/*id*</span></span> |

### <a name="methods"></a><span data-ttu-id="6a7e6-146">메서드</span><span class="sxs-lookup"><span data-stu-id="6a7e6-146">Methods</span></span>

<span data-ttu-id="6a7e6-147">네 가지 주요 HTTP 메서드 (GET, PUT, POST 및 DELETE)는 다음과 같은 CRUD 작업에 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-147">The four main HTTP methods (GET, PUT, POST, and DELETE) can be mapped to CRUD operations as follows:</span></span>

- <span data-ttu-id="6a7e6-148">가져오기에 지정된 된 URI에서 리소스의 표현을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-148">GET retrieves the representation of the resource at a specified URI.</span></span> <span data-ttu-id="6a7e6-149">GET 서버에 파생 작업이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-149">GET should have no side effects on the server.</span></span>
- <span data-ttu-id="6a7e6-150">PUT은 지정된 된 URI에서 리소스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-150">PUT updates a resource at a specified URI.</span></span> <span data-ttu-id="6a7e6-151">이 서버에 새 Uri를 지정 하는 클라이언트에서는 PUT 지정된 된 URI에 새 리소스를 만드는 데도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-151">PUT can also be used to create a new resource at a specified URI, if the server allows clients to specify new URIs.</span></span> <span data-ttu-id="6a7e6-152">이 자습서에서는 API는 PUT 통해 만들기를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-152">For this tutorial, the API will not support creation through PUT.</span></span>
- <span data-ttu-id="6a7e6-153">게시물에는 새 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-153">POST creates a new resource.</span></span> <span data-ttu-id="6a7e6-154">서버는 새 개체에 대 한 URI를 할당 하 고 응답 메시지의 일부로이 URI를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-154">The server assigns the URI for the new object and returns this URI as part of the response message.</span></span>
- <span data-ttu-id="6a7e6-155">삭제 지정된 된 URI에서 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-155">DELETE deletes a resource at a specified URI.</span></span>

<span data-ttu-id="6a7e6-156">참고: PUT 메서드는 전체 제품 엔터티를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-156">Note: The PUT method replaces the entire product entity.</span></span> <span data-ttu-id="6a7e6-157">즉, 클라이언트는 업데이트 된 제품의 완전 한 표현이 전송 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-157">That is, the client is expected to send a complete representation of the updated product.</span></span> <span data-ttu-id="6a7e6-158">부분 업데이트를 지원 하려는 경우 PATCH 메서드를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-158">If you want to support partial updates, the PATCH method is preferred.</span></span> <span data-ttu-id="6a7e6-159">이 자습서는 패치를 구현 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-159">This tutorial does not implement PATCH.</span></span>

## <a name="create-a-new-web-api-project"></a><span data-ttu-id="6a7e6-160">새 웹 API 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="6a7e6-160">Create a New Web API Project</span></span>

<span data-ttu-id="6a7e6-161">선택한 Visual Studio를 실행 하 여 시작 **새 프로젝트** 에서 합니다 **시작** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-161">Start by running Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="6a7e6-162">또는에서 **파일** 메뉴에서 **새로 만들기** 차례로 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-162">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="6a7e6-163">에 **템플릿** 창 **설치 된 템플릿** 확장 하 고는 **Visual C#** 노드.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-163">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="6a7e6-164">아래 **Visual C#** 를 선택 **웹**합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-164">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="6a7e6-165">프로젝트 템플릿 목록에서 선택 **ASP.NET MVC 4 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-165">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="6a7e6-166">프로젝트 이름을 &quot;ProductStore&quot; 누릅니다 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-166">Name the project &quot;ProductStore&quot; and click **OK**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image1.png)

<span data-ttu-id="6a7e6-167">에 **새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **Web API** 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-167">In the **New ASP.NET MVC 4 Project** dialog, select **Web API** and click **OK**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image2.png)

## <a name="adding-a-model"></a><span data-ttu-id="6a7e6-168">모델 추가</span><span class="sxs-lookup"><span data-stu-id="6a7e6-168">Adding a Model</span></span>

<span data-ttu-id="6a7e6-169">*모델*은 애플리케이션에서 데이터를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-169">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="6a7e6-170">ASP.NET Web API에서 강력한 형식의 CLR 개체로 사용 하 여 모델을 하 고 이러한을 자동으로 직렬화할지 XML 또는 JSON을 클라이언트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-170">In ASP.NET Web API, you can use strongly typed CLR objects as models, and they will automatically be serialized to XML or JSON for the client.</span></span>

<span data-ttu-id="6a7e6-171">ProductStore API에 대 한 데이터 제품 구성, 라는 새 클래스를 만들어 보겠습니다 `Product`합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-171">For the ProductStore API, our data consists of products, so we'll create a new class named `Product`.</span></span>

<span data-ttu-id="6a7e6-172">솔루션 탐색기 표시 되지 않으면 클릭 합니다 **뷰** 선택한 메뉴 **솔루션 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-172">If Solution Explorer is not already visible, click the **View** menu and select **Solution Explorer**.</span></span> <span data-ttu-id="6a7e6-173">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 합니다 **모델** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-173">In Solution Explorer, right-click the **Models** folder.</span></span> <span data-ttu-id="6a7e6-174">상황에 맞는 메뉴에서 선택 **추가**을 선택한 후 **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-174">From the context menu, select **Add**, then select **Class**.</span></span> <span data-ttu-id="6a7e6-175">클래스의 이름을 &quot;제품&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-175">Name the class &quot;Product&quot;.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image3.png)

<span data-ttu-id="6a7e6-176">다음 속성을 추가 합니다 `Product` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-176">Add the following properties to the `Product` class.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample1.cs)]

## <a name="adding-a-repository"></a><span data-ttu-id="6a7e6-177">리포지토리 추가</span><span class="sxs-lookup"><span data-stu-id="6a7e6-177">Adding a Repository</span></span>

<span data-ttu-id="6a7e6-178">제품의 컬렉션을 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-178">We need to store a collection of products.</span></span> <span data-ttu-id="6a7e6-179">서비스 구현에서 컬렉션을 분리 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-179">It's a good idea to separate the collection from our service implementation.</span></span> <span data-ttu-id="6a7e6-180">이런 방식으로 백업 저장소 서비스 클래스를 다시 작성 하지 않고 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-180">That way, we can change the backing store without rewriting the service class.</span></span> <span data-ttu-id="6a7e6-181">이러한 유형의 설계 라고 합니다 *리포지토리* 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-181">This type of design is called the *repository* pattern.</span></span> <span data-ttu-id="6a7e6-182">리포지토리에 대 한 제네릭 인터페이스를 정의 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-182">Start by defining a generic interface for the repository.</span></span>

<span data-ttu-id="6a7e6-183">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 합니다 **모델** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-183">In Solution Explorer, right-click the **Models** folder.</span></span> <span data-ttu-id="6a7e6-184">선택 **추가**을 선택한 후 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-184">Select **Add**, then select **New Item**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image4.png)

<span data-ttu-id="6a7e6-185">에 **템플릿을** 창 **설치 된 템플릿** C# 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-185">In the **Templates** pane, select **Installed Templates** and expand the C# node.</span></span> <span data-ttu-id="6a7e6-186">C#에서 선택 **코드**합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-186">Under C#, select **Code**.</span></span> <span data-ttu-id="6a7e6-187">코드 템플릿 목록에서 선택 **인터페이스**합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-187">In the list of code templates, select **Interface**.</span></span> <span data-ttu-id="6a7e6-188">인터페이스의 이름을 &quot;IProductRepository&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-188">Name the interface &quot;IProductRepository&quot;.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image5.png)

<span data-ttu-id="6a7e6-189">다음 구현을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-189">Add the following implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample2.cs)]

<span data-ttu-id="6a7e6-190">이제 다른 클래스 라는 Models 폴더를 추가 &quot;ProductRepository 합니다.&quot; 이 클래스는 `IProductRepository` 인터페이스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-190">Now add another class to the Models folder, named &quot;ProductRepository.&quot; This class will implement the `IProductRepository` interface.</span></span> <span data-ttu-id="6a7e6-191">다음 구현을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-191">Add the following implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample3.cs)]

<span data-ttu-id="6a7e6-192">로컬 메모리에 유지 하는 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-192">The repository keeps the list in local memory.</span></span> <span data-ttu-id="6a7e6-193">이 자습서의 경우 되지만 실제 응용 프로그램에서 데이터를 외부에서 두 데이터베이스를 저장할 수 있습니다 또는 클라우드 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-193">This is OK for a tutorial, but in a real application, you would store the data externally, either a database or in cloud storage.</span></span> <span data-ttu-id="6a7e6-194">리포지토리 패턴 구현을 변경 합니다. 나중에 쉽게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-194">The repository pattern will make it easier to change the implementation later.</span></span>

## <a name="adding-a-web-api-controller"></a><span data-ttu-id="6a7e6-195">웹 API 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="6a7e6-195">Adding a Web API Controller</span></span>

<span data-ttu-id="6a7e6-196">ASP.NET MVC를 사용 하 여 보았다면 다음 이미 잘 알고 있다면 컨트롤러를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-196">If you have worked with ASP.NET MVC, then you are already familiar with controllers.</span></span> <span data-ttu-id="6a7e6-197">ASP.NET Web API에는 *컨트롤러* 클라이언트로부터 HTTP 요청을 처리 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-197">In ASP.NET Web API, a *controller* is a class that handles HTTP requests from the client.</span></span> <span data-ttu-id="6a7e6-198">새 프로젝트 마법사는 프로젝트를 만들 때 두 컨트롤러를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-198">The New Project wizard created two controllers for you when it created the project.</span></span> <span data-ttu-id="6a7e6-199">이러한 작업을 확인 하려면 솔루션 탐색기에서 컨트롤러 폴더를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-199">To see them, expand the Controllers folder in Solution Explorer.</span></span>

- <span data-ttu-id="6a7e6-200">HomeController는 기존 ASP.NET MVC 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-200">HomeController is a traditional ASP.NET MVC controller.</span></span> <span data-ttu-id="6a7e6-201">사이트에 대 한 HTML 페이지를 제공 하는 일을 담당 하며 웹 API 직접 관련이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-201">It is responsible for serving HTML pages for the site, and is not directly related to our web API.</span></span>
- <span data-ttu-id="6a7e6-202">ValuesController 예제 WebAPI 컨트롤러를 경우</span><span class="sxs-lookup"><span data-stu-id="6a7e6-202">ValuesController is an example WebAPI controller.</span></span>

<span data-ttu-id="6a7e6-203">계속 해 서 ValuesController, 솔루션 탐색기에서 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 하 여 삭제 **삭제 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6a7e6-203">Go ahead and delete ValuesController, by right-clicking the file in Solution Explorer and selecting **Delete.**</span></span> <span data-ttu-id="6a7e6-204">이제 다음과 같이 새 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-204">Now add a new controller, as follows:</span></span>

<span data-ttu-id="6a7e6-205">**솔루션 탐색기**, Controllers 폴더를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-205">In **Solution Explorer**, right-click the Controllers folder.</span></span> <span data-ttu-id="6a7e6-206">선택 **추가** 선택한 후 **컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-206">Select **Add** and then select **Controller**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image6.png)

<span data-ttu-id="6a7e6-207">에 **컨트롤러 추가** 마법사에서 컨트롤러 이름 &quot;ProductsController&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-207">In the **Add Controller** wizard, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="6a7e6-208">에 **템플릿을** 드롭 다운 목록에서 **빈 API 컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-208">In the **Template** drop-down list, select **Empty API Controller**.</span></span> <span data-ttu-id="6a7e6-209">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-209">Then click **Add**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image7.png)

> [!NOTE]
> <span data-ttu-id="6a7e6-210">컨트롤러 컨트롤러 라는 폴더에 배치 하는 데 필요한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-210">It is not necessary to put your controllers into a folder named Controllers.</span></span> <span data-ttu-id="6a7e6-211">폴더 이름은 중요 하지 않습니다. 원본 파일을 구성 하려면 편리한 방법일 뿐 이며</span><span class="sxs-lookup"><span data-stu-id="6a7e6-211">The folder name is not important; it is simply a convenient way to organize your source files.</span></span>


<span data-ttu-id="6a7e6-212">합니다 **컨트롤러 추가** Controllers 폴더에서 ProductsController.cs 라는 파일을 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-212">The **Add Controller** wizard will create a file named ProductsController.cs in the Controllers folder.</span></span> <span data-ttu-id="6a7e6-213">이 파일이 열려 있지 않으면 이미를 열려는 파일을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-213">If this file is not open already, double-click the file to open it.</span></span> <span data-ttu-id="6a7e6-214">다음을 추가 합니다 **를 사용 하 여** 문:</span><span class="sxs-lookup"><span data-stu-id="6a7e6-214">Add the following **using** statement:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample4.cs)]

<span data-ttu-id="6a7e6-215">보유 하는 필드를 추가 하는 **IProductRepository** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-215">Add a field that holds an **IProductRepository** instance.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample5.cs)]

> [!NOTE]
> <span data-ttu-id="6a7e6-216">호출 `new ProductRepository()` 컨트롤러의 아니므로 가장 적합 한 디자인의 특정 구현에 컨트롤러 통제 `IProductRepository`합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-216">Calling `new ProductRepository()` in the controller is not the best design, because it ties the controller to a particular implementation of `IProductRepository`.</span></span> <span data-ttu-id="6a7e6-217">더 나은 방법은 참조 하세요 [웹 API 종속성 확인자를 사용 하 여](../advanced/dependency-injection.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-217">For a better approach, see [Using the Web API Dependency Resolver](../advanced/dependency-injection.md).</span></span>


## <a name="getting-a-resource"></a><span data-ttu-id="6a7e6-218">리소스 가져오기</span><span class="sxs-lookup"><span data-stu-id="6a7e6-218">Getting a Resource</span></span>

<span data-ttu-id="6a7e6-219">여러 ProductStore API 노출 &quot;읽을&quot; HTTP GET 메서드를 사용 하 여 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-219">The ProductStore API will expose several &quot;read&quot; actions as HTTP GET methods.</span></span> <span data-ttu-id="6a7e6-220">각 작업의 메서드에 해당 합니다 `ProductsController` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-220">Each action will correspond to a method in the `ProductsController` class.</span></span>

| <span data-ttu-id="6a7e6-221">작업</span><span class="sxs-lookup"><span data-stu-id="6a7e6-221">Action</span></span> | <span data-ttu-id="6a7e6-222">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="6a7e6-222">HTTP method</span></span> | <span data-ttu-id="6a7e6-223">상대 URI</span><span class="sxs-lookup"><span data-stu-id="6a7e6-223">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6a7e6-224">모든 제품의 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="6a7e6-224">Get a list of all products</span></span> | <span data-ttu-id="6a7e6-225">가져오기</span><span class="sxs-lookup"><span data-stu-id="6a7e6-225">GET</span></span> | <span data-ttu-id="6a7e6-226">api 제품</span><span class="sxs-lookup"><span data-stu-id="6a7e6-226">/api/products</span></span> |
| <span data-ttu-id="6a7e6-227">제품 ID 별로 가져오기</span><span class="sxs-lookup"><span data-stu-id="6a7e6-227">Get a product by ID</span></span> | <span data-ttu-id="6a7e6-228">가져오기</span><span class="sxs-lookup"><span data-stu-id="6a7e6-228">GET</span></span> | <span data-ttu-id="6a7e6-229">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="6a7e6-229">/api/products/*id*</span></span> |
| <span data-ttu-id="6a7e6-230">제품 범주별으로 가져오기</span><span class="sxs-lookup"><span data-stu-id="6a7e6-230">Get a product by category</span></span> | <span data-ttu-id="6a7e6-231">가져오기</span><span class="sxs-lookup"><span data-stu-id="6a7e6-231">GET</span></span> | <span data-ttu-id="6a7e6-232">/api/products?category=*category*</span><span class="sxs-lookup"><span data-stu-id="6a7e6-232">/api/products?category=*category*</span></span> |

<span data-ttu-id="6a7e6-233">모든 제품의 목록을 가져오려면이 메서드를 추가 합니다 `ProductsController` 클래스:</span><span class="sxs-lookup"><span data-stu-id="6a7e6-233">To get the list of all products, add this method to the `ProductsController` class:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample6.cs)]

<span data-ttu-id="6a7e6-234">메서드 이름을 사용 하 여 시작 &quot;가져올&quot;이므로 규칙에 따라 GET 요청에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-234">The method name starts with &quot;Get&quot;, so by convention it maps to GET requests.</span></span> <span data-ttu-id="6a7e6-235">또한 메서드 매개 변수가 없으면 때문에 매핑될 없는 URI는 *&quot;id&quot;* 경로의 세그먼트입니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-235">Also, because the method has no parameters, it maps to a URI that does not contain an *&quot;id&quot;* segment in the path.</span></span>

<span data-ttu-id="6a7e6-236">제품 ID 가져오려면이 메서드를 추가 합니다 `ProductsController` 클래스:</span><span class="sxs-lookup"><span data-stu-id="6a7e6-236">To get a product by ID, add this method to the `ProductsController` class:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample7.cs)]

<span data-ttu-id="6a7e6-237">이 메서드 이름을 사용 하 여 시작 &quot;가져옵니다&quot;, 메서드 라는 매개 변수를 되었지만 *id*합니다. 이 매개 변수에 매핑되는 &quot;id&quot; URI 경로의 세그먼트입니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-237">This method name also starts with &quot;Get&quot;, but the method has a parameter named *id*. This parameter is mapped to the &quot;id&quot; segment of the URI path.</span></span> <span data-ttu-id="6a7e6-238">ASP.NET Web API 프레임 워크를 자동으로 ID는 올바른 데이터 형식으로 변환 (**int**) 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-238">The ASP.NET Web API framework automatically converts the ID to the correct data type (**int**) for the parameter.</span></span>

<span data-ttu-id="6a7e6-239">GetProduct 메서드 형식의 예외를 throw **HttpResponseException** 하는 경우 *id* 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-239">The GetProduct method throws an exception of type **HttpResponseException** if *id* is not valid.</span></span> <span data-ttu-id="6a7e6-240">이 예외는 404 (찾을 수 없음) 오류가 프레임 워크에 의해 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-240">This exception will be translated by the framework into a 404 (Not Found) error.</span></span>

<span data-ttu-id="6a7e6-241">마지막으로 범주별으로 제품을 검색 하는 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-241">Finally, add a method to find products by category:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample8.cs)]

<span data-ttu-id="6a7e6-242">요청 URI 쿼리 문자열에 있으면 웹 API 컨트롤러 메서드에 매개 변수가 쿼리 매개 변수를 찾으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-242">If the request URI has a query string, Web API tries to match the query parameters to parameters on the controller method.</span></span> <span data-ttu-id="6a7e6-243">따라서 폼의 URI "api/제품? category =*범주*"이 메서드에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-243">Therefore, a URI of the form "api/products?category=*category*" will map to this method.</span></span>

## <a name="creating-a-resource"></a><span data-ttu-id="6a7e6-244">리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="6a7e6-244">Creating a Resource</span></span>

<span data-ttu-id="6a7e6-245">다음으로 메서드를 추가한는 `ProductsController` 새 제품을 만드는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-245">Next, we'll add a method to the `ProductsController` class to create a new product.</span></span> <span data-ttu-id="6a7e6-246">메서드의 간단한 구현을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-246">Here is a simple implementation of the method:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample9.cs)]

<span data-ttu-id="6a7e6-247">이 메서드에 대 한 두 참고 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-247">Note two things about this method:</span></span>

- <span data-ttu-id="6a7e6-248">메서드 이름을 사용 하 여 시작 &quot;게시 하는 중... &quot;.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-248">The method name starts with &quot;Post...&quot;.</span></span> <span data-ttu-id="6a7e6-249">클라이언트는 새 제품을 만들려면 HTTP POST 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-249">To create a new product, the client sends an HTTP POST request.</span></span>
- <span data-ttu-id="6a7e6-250">메서드는 제품 형식의 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-250">The method takes a parameter of type Product.</span></span> <span data-ttu-id="6a7e6-251">Web API에서 복합 형식으로 매개 변수는 요청 본문에서 deserialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-251">In Web API, parameters with complex types are deserialized from the request body.</span></span> <span data-ttu-id="6a7e6-252">따라서 제품 개체의 serialize 된 표현에 XML 또는 JSON 형식으로 보내도록 클라이언트를 기대 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-252">Therefore, we expect the client to send a serialized representation of a product object, in either XML or JSON format.</span></span>

<span data-ttu-id="6a7e6-253">이 구현에서 작동 하지만 매우 완전 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-253">This implementation will work, but it is not quite complete.</span></span> <span data-ttu-id="6a7e6-254">이상적으로 다음과 같습니다에 대 한 HTTP 응답을 싶습니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-254">Ideally, we would like the HTTP response to include the following:</span></span>

- <span data-ttu-id="6a7e6-255">**응답 코드:** 기본적으로 Web API 프레임 워크는 응답 상태 코드 200 (정상)를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-255">**Response code:** By default, the Web API framework sets the response status code to 200 (OK).</span></span> <span data-ttu-id="6a7e6-256">하지만 HTTP/1.1 프로토콜에 따라 리소스를 만드는 POST 요청을 생성 하는 경우 서버 회신 해야 함 상태 201 (만들어짐).</span><span class="sxs-lookup"><span data-stu-id="6a7e6-256">But according to the HTTP/1.1 protocol, when a POST request results in the creation of a resource, the server should reply with status 201 (Created).</span></span>
- <span data-ttu-id="6a7e6-257">**위치:** 서버 리소스를 만들 때 새 리소스의 URI는 응답의 Location 헤더에 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-257">**Location:** When the server creates a resource, it should include the URI of the new resource in the Location header of the response.</span></span>

<span data-ttu-id="6a7e6-258">ASP.NET Web API 쉽게 HTTP 응답 메시지를 조작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-258">ASP.NET Web API makes it easy to manipulate the HTTP response message.</span></span> <span data-ttu-id="6a7e6-259">향상 된 구현은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-259">Here is the improved implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample10.cs)]

<span data-ttu-id="6a7e6-260">메서드 반환 형식을 이제는 **HttpResponseMessage**합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-260">Notice that the method return type is now **HttpResponseMessage**.</span></span> <span data-ttu-id="6a7e6-261">반환 하 여는 **HttpResponseMessage** 제품을 대신 상태 코드 및 Location 헤더를 포함 하 여 HTTP 응답 메시지의 세부 정보를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-261">By returning an **HttpResponseMessage** instead of a Product, we can control the details of the HTTP response message, including the status code and the Location header.</span></span>

<span data-ttu-id="6a7e6-262">합니다 **CreateResponse** 메서드를 만듭니다를 **HttpResponseMessage** 자동으로 본문에 직렬화 된 표현을 Product 개체를 작성 및 fo 응답 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-262">The **CreateResponse** method creates an **HttpResponseMessage** and automatically writes a serialized representation of the Product object into the body fo the response message.</span></span>

> [!NOTE]
> <span data-ttu-id="6a7e6-263">이 예제에서는 유효성을 검사 하지 않습니다는 `Product`합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-263">This example does not validate the `Product`.</span></span> <span data-ttu-id="6a7e6-264">모델 유효성 검사에 대 한 자세한 내용은 [ASP.NET Web API의 모델 유효성 검사](../formats-and-model-binding/model-validation-in-aspnet-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-264">For information about model validation, see [Model Validation in ASP.NET Web API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span></span>


## <a name="updating-a-resource"></a><span data-ttu-id="6a7e6-265">리소스 업데이트</span><span class="sxs-lookup"><span data-stu-id="6a7e6-265">Updating a Resource</span></span>

<span data-ttu-id="6a7e6-266">PUT을 사용 하 여 제품을 업데이트 하는 것은 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-266">Updating a product with PUT is straightforward:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample11.cs)]

<span data-ttu-id="6a7e6-267">메서드 이름을 사용 하 여 시작 &quot;배치 하는 중... &quot;이므로 PUT 요청에 Web API와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-267">The method name starts with &quot;Put...&quot;, so Web API matches it to PUT requests.</span></span> <span data-ttu-id="6a7e6-268">메서드는 두 개의 매개 변수, 제품 ID 및 업데이트 된 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-268">The method takes two parameters, the product ID and the updated product.</span></span> <span data-ttu-id="6a7e6-269">합니다 *id* 매개 변수는 URI 경로에서 가져온 것 하며 *제품* 요청 본문에서 deserialize 되는 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-269">The *id* parameter is taken from the URI path, and the *product* parameter is deserialized from the request body.</span></span> <span data-ttu-id="6a7e6-270">기본적으로 ASP.NET Web API 프레임 워크는 경로에서 간단한 매개 변수 형식 및 요청 본문에서 복합 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-270">By default, the ASP.NET Web API framework takes simple parameter types from the route and complex types from the request body.</span></span>

## <a name="deleting-a-resource"></a><span data-ttu-id="6a7e6-271">리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-271">Deleting a Resource</span></span>

<span data-ttu-id="6a7e6-272">리소스를 삭제 하려면 "삭제..."를 정의 합니다. 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="6a7e6-272">To delete a resource, define a "Delete..." method.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample12.cs)]

<span data-ttu-id="6a7e6-273">삭제 요청에 성공 하면; 상태를 설명 하는 엔터티 본문을 사용 하 여 200 (정상) 상태를 반환할 수 것 상태 202 (수락)를 삭제 하는 여전히 보류 중이면 또는 상태 엔터티 본문 없이 204 (내용 없음).</span><span class="sxs-lookup"><span data-stu-id="6a7e6-273">If a DELETE request succeeds, it can return status 200 (OK) with an entity-body that describes the status; status 202 (Accepted) if the deletion is still pending; or status 204 (No Content) with no entity body.</span></span> <span data-ttu-id="6a7e6-274">이 경우에 `DeleteProduct` 메서드가 `void` 반환 형식, 하므로 ASP.NET Web API 자동으로 변환이 상태 코드 204 (내용 없음).</span><span class="sxs-lookup"><span data-stu-id="6a7e6-274">In this case, the `DeleteProduct` method has a `void` return type, so ASP.NET Web API automatically translates this into status code 204 (No Content).</span></span>
