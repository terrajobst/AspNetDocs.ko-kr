---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
title: ASP.NET Web API 2.2를 사용 하 여 OData v4의 동작 및 함수 | Microsoft Docs
author: MikeWasson
description: OData에서 작업 및 함수는 엔터티에 대 한 CRUD 작업으로 쉽게 정의 되지 않는 서버 쪽 동작을 추가 하는 방법입니다. 이 자습서에서는 다음 방법을 보여 줍니다.
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 0e6fb03c-b16d-4bb0-ab0b-552bd2b6ece1
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
msc.type: authoredcontent
ms.openlocfilehash: f5af94e93e5b7f2351d40febbf1a468d635c9db1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448061"
---
# <a name="actions-and-functions-in-odata-v4-using-aspnet-web-api-22"></a><span data-ttu-id="f8512-104">ASP.NET Web API 2.2를 사용 하는 OData v4의 동작 및 함수</span><span class="sxs-lookup"><span data-stu-id="f8512-104">Actions and Functions in OData v4 Using ASP.NET Web API 2.2</span></span>

<span data-ttu-id="f8512-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="f8512-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="f8512-106">OData에서 작업 및 함수는 엔터티에 대 한 CRUD 작업으로 쉽게 정의 되지 않는 서버 쪽 동작을 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-106">In OData, actions and functions are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span> <span data-ttu-id="f8512-107">이 자습서에서는 Web API 2.2를 사용 하 여 OData v4 끝점에 작업 및 함수를 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-107">This tutorial shows how to add actions and functions to an OData v4 endpoint, using Web API 2.2.</span></span> <span data-ttu-id="f8512-108">자습서는 [ASP.NET Web API 2를 사용 하 여 OData V4 엔드포인트 만들기](create-an-odata-v4-endpoint.md) 자습서를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-108">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md)</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="f8512-109">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="f8512-109">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="f8512-110">웹 API 2.2</span><span class="sxs-lookup"><span data-stu-id="f8512-110">Web API 2.2</span></span>
> - <span data-ttu-id="f8512-111">OData v4</span><span class="sxs-lookup"><span data-stu-id="f8512-111">OData v4</span></span>
> - <span data-ttu-id="f8512-112">Visual Studio 2013 (Visual [Studio 2017 다운로드](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span><span class="sxs-lookup"><span data-stu-id="f8512-112">Visual Studio 2013 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span></span>
> - <span data-ttu-id="f8512-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="f8512-113">.NET 4.5</span></span>
>
> ## <a name="tutorial-versions"></a><span data-ttu-id="f8512-114">자습서 버전</span><span class="sxs-lookup"><span data-stu-id="f8512-114">Tutorial versions</span></span>
>
> <span data-ttu-id="f8512-115">OData 버전 3의 경우 [ASP.NET Web API 2의 Odata 작업](../odata-v3/odata-actions.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f8512-115">For OData Version 3, see [OData Actions in ASP.NET Web API 2](../odata-v3/odata-actions.md).</span></span>

<span data-ttu-id="f8512-116">작업과 *함수의* 차이점 은 작업에 부작용이 있을 수 있다는 것 이며 함수는 그렇지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-116">The difference between *actions* and *functions* is that actions can have side effects, and functions do not.</span></span> <span data-ttu-id="f8512-117">작업 및 함수는 모두 데이터를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-117">Both actions and functions can return data.</span></span> <span data-ttu-id="f8512-118">작업에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-118">Some uses for actions include:</span></span>

- <span data-ttu-id="f8512-119">복잡 한 트랜잭션.</span><span class="sxs-lookup"><span data-stu-id="f8512-119">Complex transactions.</span></span>
- <span data-ttu-id="f8512-120">여러 엔터티를 한 번에 조작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-120">Manipulating several entities at once.</span></span>
- <span data-ttu-id="f8512-121">엔터티의 특정 속성만 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-121">Allowing updates only to certain properties of an entity.</span></span>
- <span data-ttu-id="f8512-122">엔터티가 아닌 데이터를 보내는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-122">Sending data that is not an entity.</span></span>

<span data-ttu-id="f8512-123">함수는 엔터티 또는 컬렉션과 직접 일치 하지 않는 정보를 반환 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-123">Functions are useful for returning information that does not correspond directly to an entity or collection.</span></span>

<span data-ttu-id="f8512-124">작업 (또는 함수)은 단일 엔터티 또는 컬렉션을 대상으로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-124">An action (or function) can target a single entity or a collection.</span></span> <span data-ttu-id="f8512-125">OData 용어에서이는 *바인딩입니다*.</span><span class="sxs-lookup"><span data-stu-id="f8512-125">In OData terminology, this is the *binding*.</span></span> <span data-ttu-id="f8512-126">서비스에서 정적 작업으로 호출 되는 &quot;바인딩되지 않은&quot; 작업/함수를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-126">You can also have &quot;unbound&quot; actions/functions, which are called as static operations on the service.</span></span>

## <a name="example-adding-an-action"></a><span data-ttu-id="f8512-127">예: 작업 추가</span><span class="sxs-lookup"><span data-stu-id="f8512-127">Example: Adding an Action</span></span>

<span data-ttu-id="f8512-128">제품을 평가 하는 작업을 정의 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-128">Let's define an action to rate a product.</span></span>

> [!NOTE]
> <span data-ttu-id="f8512-129">이 자습서에서는 [ASP.NET Web API 2를 사용 하 여 OData V4 끝점 만들기](create-an-odata-v4-endpoint.md) 자습서를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-129">This tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md)</span></span>

<span data-ttu-id="f8512-130">먼저 등급을 나타내는 `ProductRating` 모델을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-130">First, add a `ProductRating` model to represent the ratings.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample1.cs)]

<span data-ttu-id="f8512-131">또한 EF가 데이터베이스에 등급 테이블을 만들 수 있도록 **Dbset** 을 `ProductsContext` 클래스에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-131">Also add a **DbSet** to the `ProductsContext` class, so that EF will create a Ratings table in the database.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample2.cs)]

### <a name="add-the-action-to-the-edm"></a><span data-ttu-id="f8512-132">EDM에 작업 추가</span><span class="sxs-lookup"><span data-stu-id="f8512-132">Add the Action to the EDM</span></span>

<span data-ttu-id="f8512-133">WebApiConfig.cs에서 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-133">In WebApiConfig.cs, add the following code:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample3.cs)]

<span data-ttu-id="f8512-134">**EntityTypeConfiguration** 메서드는 EDM (엔터티 데이터 모델)에 작업을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-134">The **EntityTypeConfiguration.Action** method adds an action to the entity data model (EDM).</span></span> <span data-ttu-id="f8512-135">**Parameter** 메서드는 동작에 대해 형식화 된 매개 변수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-135">The **Parameter** method specifies a typed parameter for the action.</span></span>

<span data-ttu-id="f8512-136">또한이 코드는 EDM에 대 한 네임 스페이스를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-136">This code also sets the namespace for the EDM.</span></span> <span data-ttu-id="f8512-137">네임 스페이스는 동작에 대 한 URI에 정규화 된 동작 이름이 포함 되기 때문에 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-137">The namespace matters because the URI for the action includes the fully-qualified action name:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample4.cmd)]

> [!NOTE]
> <span data-ttu-id="f8512-138">일반적인 IIS 구성에서이 URL의 점은 IIS에서 404 오류를 반환 하는 원인이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-138">In a typical IIS configuration, the dot in this URL will cause IIS to return error 404.</span></span> <span data-ttu-id="f8512-139">Web.config 파일에 다음 섹션을 추가 하 여이 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-139">You can resolve this by adding the following section to your Web.Config file:</span></span>

[!code-xml[Main](odata-actions-and-functions/samples/sample5.xml)]

### <a name="add-a-controller-method-for-the-action"></a><span data-ttu-id="f8512-140">작업에 대 한 컨트롤러 메서드 추가</span><span class="sxs-lookup"><span data-stu-id="f8512-140">Add a Controller Method for the Action</span></span>

<span data-ttu-id="f8512-141">&quot;Rate&quot; 작업을 사용 하도록 설정 하려면 다음 메서드를 `ProductsController`에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-141">To enable the &quot;Rate&quot; action, add the following method to `ProductsController`:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample6.cs)]

<span data-ttu-id="f8512-142">메서드 이름이 작업 이름과 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-142">Notice that the method name matches the action name.</span></span> <span data-ttu-id="f8512-143">**[HttpPost]** 특성은 메서드가 HTTP POST 메서드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-143">The **[HttpPost]** attribute specifies the method is an HTTP POST method.</span></span>

<span data-ttu-id="f8512-144">동작을 호출 하기 위해 클라이언트는 다음과 같은 HTTP POST 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-144">To invoke the action, the client sends an HTTP POST request like the following:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample7.cmd)]

<span data-ttu-id="f8512-145">작업에 대 한 URI는 엔터티 URI에 추가 된 정규화 된 작업 이름 이므로 작업에 대 한 URI가 제품 인스턴스에 바인딩되어&quot; &quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-145">The &quot;Rate&quot; action is bound to Product instances, so the URI for the action is the fully-qualified action name appended to the entity URI.</span></span> <span data-ttu-id="f8512-146">EDM 네임 스페이스를 &quot;제품 서비스&quot;로 설정 했으므로 정규화 된 작업 이름은 제품 서비스 &quot;입니다. Rate&quot;.</span><span class="sxs-lookup"><span data-stu-id="f8512-146">(Recall that we set the EDM namespace to &quot;ProductService&quot;, so the fully-qualified action name is &quot;ProductService.Rate&quot;.)</span></span>

<span data-ttu-id="f8512-147">요청의 본문은 작업 매개 변수를 JSON 페이로드로 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-147">The body of the request contains the action parameters as a JSON payload.</span></span> <span data-ttu-id="f8512-148">Web API는 JSON 페이로드를 매개 변수 값의 사전 인 **ODataActionParameters** 개체로 자동으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-148">Web API automatically converts the JSON payload to an **ODataActionParameters** object, which is just a dictionary of parameter values.</span></span> <span data-ttu-id="f8512-149">이 사전을 사용 하 여 컨트롤러 메서드의 매개 변수에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-149">Use this dictionary to access the parameters in your controller method.</span></span>

<span data-ttu-id="f8512-150">클라이언트에서 동작 매개 변수를 잘못 된 형식으로 보내는 경우 **Modelstate. IsValid** 값은 false입니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-150">If the client sends the action parameters in the wrong format, the value of **ModelState.IsValid** is false.</span></span> <span data-ttu-id="f8512-151">컨트롤러 메서드에서이 플래그를 확인 하 고 **IsValid** 가 false 인 경우 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-151">Check this flag in your controller method and return an error if **IsValid** is false.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample8.cs)]

## <a name="example-adding-a-function"></a><span data-ttu-id="f8512-152">예: 함수 추가</span><span class="sxs-lookup"><span data-stu-id="f8512-152">Example: Adding a Function</span></span>

<span data-ttu-id="f8512-153">이제 가장 비용이 많이 드는 제품을 반환 하는 OData 함수를 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-153">Now let's add an OData function that returns the most expensive product.</span></span> <span data-ttu-id="f8512-154">이전 처럼 첫 번째 단계는 함수를 EDM에 추가 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-154">As before, the first step is adding the function to the EDM.</span></span> <span data-ttu-id="f8512-155">WebApiConfig.cs에서 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-155">In WebApiConfig.cs, add the following code.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample9.cs)]

<span data-ttu-id="f8512-156">이 경우 함수는 개별 제품 인스턴스가 아닌 Products 컬렉션에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-156">In this case, the function is bound to the Products collection, rather than individual Product instances.</span></span> <span data-ttu-id="f8512-157">클라이언트는 GET 요청을 보내 함수를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-157">Clients invoke the function by sending a GET request:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample10.cmd)]

<span data-ttu-id="f8512-158">이 함수에 대 한 컨트롤러 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-158">Here is the controller method for this function:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample11.cs)]

<span data-ttu-id="f8512-159">메서드 이름이 함수 이름과 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-159">Notice that the method name matches the function name.</span></span> <span data-ttu-id="f8512-160">**[HttpGet]** 특성은 메서드가 HTTP GET 메서드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-160">The **[HttpGet]** attribute specifies the method is an HTTP GET method.</span></span>

<span data-ttu-id="f8512-161">HTTP 응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-161">Here is the HTTP response:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample12.cmd)]

## <a name="example-adding-an-unbound-function"></a><span data-ttu-id="f8512-162">예제: 바인딩되지 않은 함수 추가</span><span class="sxs-lookup"><span data-stu-id="f8512-162">Example: Adding an Unbound Function</span></span>

<span data-ttu-id="f8512-163">이전 예제는 컬렉션에 바인딩된 함수 였습니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-163">The previous example was a function bound to a collection.</span></span> <span data-ttu-id="f8512-164">다음 예제에서는 *바인딩되지* 않은 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-164">In this next example, we'll create an *unbound* function.</span></span> <span data-ttu-id="f8512-165">바인딩되지 않은 함수는 서비스에서 정적 작업으로 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-165">Unbound functions are called as static operations on the service.</span></span> <span data-ttu-id="f8512-166">이 예제의 함수는 지정 된 우편 번호에 대 한 판매 세율을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-166">The function in this example will return the sales tax for a given postal code.</span></span>

<span data-ttu-id="f8512-167">WebApiConfig 파일에서 함수를 EDM에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-167">In the WebApiConfig file, add the function to the EDM:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample13.cs)]

<span data-ttu-id="f8512-168">엔터티 형식 또는 컬렉션이 아닌 **만드는**에서 직접 **함수** 를 호출 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-168">Notice that we are calling **Function** directly on the **ODataModelBuilder**, instead of the entity type or collection.</span></span> <span data-ttu-id="f8512-169">이렇게 하면 함수가 바인딩되지 않음을 모델 작성기에 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-169">This tells the model builder that the function is unbound.</span></span>

<span data-ttu-id="f8512-170">함수를 구현 하는 컨트롤러 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-170">Here is the controller method that implements the function:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample14.cs)]

<span data-ttu-id="f8512-171">이 메서드를 배치한 웹 API 컨트롤러에는 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-171">It does not matter which Web API controller you place this method in.</span></span> <span data-ttu-id="f8512-172">`ProductsController`에 추가 하거나 별도의 컨트롤러를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-172">You could put it in `ProductsController`, or define a separate controller.</span></span> <span data-ttu-id="f8512-173">**[ODataRoute]** 특성은 함수에 대 한 URI 템플릿을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-173">The **[ODataRoute]** attribute defines the URI template for the function.</span></span>

<span data-ttu-id="f8512-174">클라이언트 요청 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f8512-174">Here is an example client request:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample15.cmd)]

<span data-ttu-id="f8512-175">HTTP 응답:</span><span class="sxs-lookup"><span data-stu-id="f8512-175">The HTTP response:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample16.cmd)]
