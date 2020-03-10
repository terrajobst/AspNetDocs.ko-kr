---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
title: ASP.NET Web API 2에서 OData 작업 지원 | Microsoft Docs
author: MikeWasson
description: OData에서 작업은 엔터티에 대 한 CRUD 작업으로 쉽게 정의 되지 않는 서버 쪽 동작을 추가 하는 방법입니다. 작업에는 다음이 포함 됩니다. 구현 ...
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 2d7b3aa2-aa47-4e6e-b0ce-3d65a1c6fe02
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
msc.type: authoredcontent
ms.openlocfilehash: ae8b23f0868f992cb2bbbf14ee3f7ac848501515
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448175"
---
# <a name="supporting-odata-actions-in-aspnet-web-api-2"></a><span data-ttu-id="4890a-104">ASP.NET Web API 2에서 OData 작업 지원</span><span class="sxs-lookup"><span data-stu-id="4890a-104">Supporting OData Actions in ASP.NET Web API 2</span></span>

<span data-ttu-id="4890a-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="4890a-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="4890a-106">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="4890a-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="4890a-107">OData에서 *작업* 은 엔터티에 대 한 CRUD 작업으로 쉽게 정의 되지 않는 서버 쪽 동작을 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-107">In OData, *actions* are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span> <span data-ttu-id="4890a-108">작업에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-108">Some uses for actions include:</span></span>
> 
> - <span data-ttu-id="4890a-109">복잡 한 트랜잭션 구현</span><span class="sxs-lookup"><span data-stu-id="4890a-109">Implementing complex transactions.</span></span>
> - <span data-ttu-id="4890a-110">여러 엔터티를 한 번에 조작 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-110">Manipulating several entities at once.</span></span>
> - <span data-ttu-id="4890a-111">엔터티의 특정 속성만 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-111">Allowing updates only to certain properties of an entity.</span></span>
> - <span data-ttu-id="4890a-112">엔터티에 정의 되지 않은 서버로 정보를 보내는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-112">Sending information to the server that is not defined in an entity.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="4890a-113">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="4890a-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="4890a-114">Web API 2</span><span class="sxs-lookup"><span data-stu-id="4890a-114">Web API 2</span></span>
> - <span data-ttu-id="4890a-115">OData 버전 3</span><span class="sxs-lookup"><span data-stu-id="4890a-115">OData Version 3</span></span>
> - <span data-ttu-id="4890a-116">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="4890a-116">Entity Framework 6</span></span>

## <a name="example-rating-a-product"></a><span data-ttu-id="4890a-117">예: 제품 등급 매기기</span><span class="sxs-lookup"><span data-stu-id="4890a-117">Example: Rating a Product</span></span>

<span data-ttu-id="4890a-118">이 예에서는 사용자가 제품의 등급을 지정 하 고 각 제품의 평균 등급을 표시 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-118">In this example, we want to let users rate products, and then expose the average ratings for each product.</span></span> <span data-ttu-id="4890a-119">데이터베이스에서 제품에 키가 지정 된 등급의 목록을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-119">On the database, we will store a list of ratings, keyed to products.</span></span>

<span data-ttu-id="4890a-120">다음은 Entity Framework의 등급을 나타내는 데 사용할 수 있는 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-120">Here is the model we might use to represent the ratings in Entity Framework:</span></span>

[!code-csharp[Main](odata-actions/samples/sample1.cs)]

<span data-ttu-id="4890a-121">그러나 클라이언트가 `ProductRating` 개체를 "등급" 컬렉션에 게시 하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-121">But we don't want clients to POST a `ProductRating` object to a "Ratings" collection.</span></span> <span data-ttu-id="4890a-122">기본적으로 등급은 Products 컬렉션과 연결 되며 클라이언트는 등급 값을 게시 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-122">Intuitively, the rating is associated with the Products collection, and the client should only need to post the rating value.</span></span>

<span data-ttu-id="4890a-123">따라서 정상적인 CRUD 작업을 사용 하는 대신 클라이언트에서 제품에 대해 호출할 수 있는 작업을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-123">Therefore, instead of using the normal CRUD operations, we define an action that a client can invoke on a Product.</span></span> <span data-ttu-id="4890a-124">OData 용어에서 작업은 제품 엔터티에 *바인딩됩니다* .</span><span class="sxs-lookup"><span data-stu-id="4890a-124">In OData terminology, the action is *bound* to Product entities.</span></span>

><span data-ttu-id="4890a-125">작업은 서버에 부작용이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-125">Actions have side-effects on the server.</span></span> <span data-ttu-id="4890a-126">이러한 이유로 HTTP POST 요청을 사용 하 여 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-126">For this reason, they are invoked using HTTP POST requests.</span></span> <span data-ttu-id="4890a-127">작업에는 서비스 메타 데이터에 설명 되어 있는 매개 변수 및 반환 형식이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-127">Actions can have parameters and return types, which are described in the service metadata.</span></span> <span data-ttu-id="4890a-128">클라이언트는 요청 본문에 매개 변수를 보내고 서버는 응답 본문에 반환 값을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-128">The client sends the parameters in the request body, and the server sends the return value in the response body.</span></span> <span data-ttu-id="4890a-129">"등급 제품" 작업을 호출 하기 위해 클라이언트는 다음과 같은 URI에 게시물을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-129">To invoke the "Rate Product" action, the client sends a POST to a URI like the following:</span></span>

[!code-console[Main](odata-actions/samples/sample2.cmd)]

<span data-ttu-id="4890a-130">POST 요청의 데이터는 단순히 제품 등급입니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-130">The data in the POST request is simply the product rating:</span></span>

[!code-console[Main](odata-actions/samples/sample3.cmd)]

## <a name="declare-the-action-in-the-entity-data-model"></a><span data-ttu-id="4890a-131">엔터티 데이터 모델에서 작업을 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-131">Declare the Action in the Entity Data Model</span></span>

<span data-ttu-id="4890a-132">Web API 구성에서 EDM (엔터티 데이터 모델)에 작업을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-132">In your Web API configuration, add the action to the entity data model (EDM):</span></span>

[!code-csharp[Main](odata-actions/samples/sample4.cs)]

<span data-ttu-id="4890a-133">이 코드는 제품 엔터티에서 수행할 수 있는 작업으로 "RateProduct"를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-133">This code defines "RateProduct" as an action that can be performed on Product entities.</span></span> <span data-ttu-id="4890a-134">또한 동작이 "등급" 이라는 **int** 매개 변수를 사용 하 고 **정수** 값을 반환 한다는 것을 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-134">It also declares that the action takes an **int** parameter named "Rating", and returns an **int** value.</span></span>

## <a name="add-the-action-to-the-controller"></a><span data-ttu-id="4890a-135">컨트롤러에 작업 추가</span><span class="sxs-lookup"><span data-stu-id="4890a-135">Add the Action to the Controller</span></span>

<span data-ttu-id="4890a-136">"RateProduct" 작업은 제품 엔터티에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-136">The "RateProduct" action is bound to Product entities.</span></span> <span data-ttu-id="4890a-137">작업을 구현 하려면 `RateProduct` 라는 메서드를 Products 컨트롤러에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-137">To implement the action, add a method named `RateProduct` to the Products controller:</span></span>

[!code-csharp[Main](odata-actions/samples/sample5.cs)]

<span data-ttu-id="4890a-138">메서드 이름이 EDM의 작업 이름과 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-138">Notice that the method name matches the name of the action in the EDM.</span></span> <span data-ttu-id="4890a-139">메서드에는 두 개의 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-139">The method has two parameters:</span></span>

- <span data-ttu-id="4890a-140">*키*: 평가할 제품의 키입니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-140">*key*: The key for the product to rate.</span></span>
- <span data-ttu-id="4890a-141">*parameters*: 작업 매개 변수 값의 사전입니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-141">*parameters*: A dictionary of action parameter values.</span></span>

<span data-ttu-id="4890a-142">기본 라우팅 규칙을 사용 하는 경우 키 매개 변수의 이름을 "key"로 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-142">If you are using the default routing conventions, the key parameter must be named "key".</span></span> <span data-ttu-id="4890a-143">표시 된 것 처럼 **[Fromodatauri]** 특성도 포함 하는 것도 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-143">It is also important to include the **[FromOdataUri]** attribute, as shown.</span></span> <span data-ttu-id="4890a-144">이 특성은 요청 URI에서 키를 구문 분석할 때 OData 구문 규칙을 사용 하도록 Web API에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-144">This attribute tells Web API to use OData syntax rules when it parses the key from the request URI.</span></span>

<span data-ttu-id="4890a-145">*매개 변수* 사전을 사용 하 여 작업 매개 변수를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-145">Use the *parameters* dictionary to get the action parameters:</span></span>

[!code-csharp[Main](odata-actions/samples/sample6.cs)]

<span data-ttu-id="4890a-146">클라이언트에서 동작 매개 변수를 올바른 형식으로 보내는 경우 **Modelstate. IsValid** 값이 true입니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-146">If the client sends the action parameters in the correct format, the value of **ModelState.IsValid** is true.</span></span> <span data-ttu-id="4890a-147">이 경우 **ODataActionParameters** 사전을 사용 하 여 매개 변수 값을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-147">In that case, you can use the **ODataActionParameters** dictionary to get the parameter values.</span></span> <span data-ttu-id="4890a-148">이 예제에서 `RateProduct` 작업은 "등급" 이라는 단일 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-148">In this example, the `RateProduct` action takes a single parameter named "Rating".</span></span>

## <a name="action-metadata"></a><span data-ttu-id="4890a-149">작업 메타 데이터</span><span class="sxs-lookup"><span data-stu-id="4890a-149">Action Metadata</span></span>

<span data-ttu-id="4890a-150">서비스 메타 데이터를 보려면/odata/$metadata에 GET 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-150">To view the service metadata, send a GET request to /odata/$metadata.</span></span> <span data-ttu-id="4890a-151">다음은 `RateProduct` 작업을 선언 하는 메타 데이터의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-151">Here is the portion of the metadata that declares the `RateProduct` action:</span></span>

[!code-xml[Main](odata-actions/samples/sample7.xml)]

<span data-ttu-id="4890a-152">**FunctionImport** 요소는 작업을 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-152">The **FunctionImport** element declares the action.</span></span> <span data-ttu-id="4890a-153">대부분의 필드는 별도의 설명이 필요 하지만 두 가지는 주의를 기울여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-153">Most of the fields are self-explanatory, but two are worth noting:</span></span>

- <span data-ttu-id="4890a-154">**Isbindable** 가능은 최소한 시간 동안 대상 엔터티에서 작업을 호출할 수 있음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-154">**IsBindable** means the action can be invoked on the target entity, at least some of the time.</span></span>
- <span data-ttu-id="4890a-155">**IsAlwaysBindable** 은 대상 엔터티에서 항상 동작을 호출할 수 있음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-155">**IsAlwaysBindable** means the action can always be invoked on the target entity.</span></span>

<span data-ttu-id="4890a-156">차이점은 일부 동작은 클라이언트에서 항상 사용할 수 있지만 다른 작업은 엔터티의 상태에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-156">The difference is that some actions are always available to clients, but other actions might depend on the state of the entity.</span></span> <span data-ttu-id="4890a-157">예를 들어 "구매" 작업을 정의 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-157">For example, suppose you define a "Purchase" action.</span></span> <span data-ttu-id="4890a-158">재고에 있는 항목만 구매할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-158">You can only purchase an item that is in stock.</span></span> <span data-ttu-id="4890a-159">항목이 재고가 없으면 클라이언트에서 해당 작업을 호출할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-159">If the item is out of stock, a client cannot invoke that action.</span></span>

<span data-ttu-id="4890a-160">EDM을 정의 하는 경우 **동작** 메서드는 항상 바인딩할 수 있는 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-160">When you define the EDM, the **Action** method creates an always-bindable action:</span></span>

[!code-csharp[Main](odata-actions/samples/sample8.cs?highlight=1)]

<span data-ttu-id="4890a-161">이 항목의 뒷부분에서는 항상 바인딩할 수 있는 작업 ( *임시* 작업이 라고도 함)에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-161">I'll talk about not-always-bindable actions (also called *transient* actions) later in this topic.</span></span>

## <a name="invoking-the-action"></a><span data-ttu-id="4890a-162">작업 호출</span><span class="sxs-lookup"><span data-stu-id="4890a-162">Invoking the Action</span></span>

<span data-ttu-id="4890a-163">이제 클라이언트가이 작업을 호출 하는 방법을 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-163">Now let's see how a client would invoke this action.</span></span> <span data-ttu-id="4890a-164">클라이언트에서 ID가 4 인 제품에 등급 2를 제공 하려고 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-164">Suppose the client wants to give a rating of 2 to the product with ID = 4.</span></span> <span data-ttu-id="4890a-165">요청 본문에 JSON 형식을 사용 하는 예제 요청 메시지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-165">Here is an example request message, using JSON format for the request body:</span></span>

[!code-console[Main](odata-actions/samples/sample9.cmd)]

<span data-ttu-id="4890a-166">응답 메시지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-166">Here is the response message:</span></span>

[!code-console[Main](odata-actions/samples/sample10.cmd)]

## <a name="binding-an-action-to-an-entity-set"></a><span data-ttu-id="4890a-167">작업을 엔터티 집합에 바인딩</span><span class="sxs-lookup"><span data-stu-id="4890a-167">Binding an Action to an Entity Set</span></span>

<span data-ttu-id="4890a-168">이전 예제에서 작업은 단일 엔터티에 바인딩됩니다. 클라이언트는 단일 제품을 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-168">In the previous example, the action is bound to a single entity: The client rates a single product.</span></span> <span data-ttu-id="4890a-169">엔터티 컬렉션에 작업을 바인딩할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-169">You can also bind an action to a collection of entities.</span></span> <span data-ttu-id="4890a-170">다음과 같이 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-170">Just make the following changes:</span></span>

<span data-ttu-id="4890a-171">EDM에서 엔터티의 **컬렉션** 속성에 작업을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-171">In the EDM, add the action to the entity's **Collection** property.</span></span>

[!code-csharp[Main](odata-actions/samples/sample11.cs?highlight=1)]

<span data-ttu-id="4890a-172">Controller 메서드에서 *키* 매개 변수를 생략 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-172">In the controller method, omit the *key* parameter.</span></span>

[!code-csharp[Main](odata-actions/samples/sample12.cs)]

<span data-ttu-id="4890a-173">이제 클라이언트가 Products 엔터티 집합에 대 한 작업을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-173">Now the client invokes the action on the Products entity set:</span></span>

[!code-console[Main](odata-actions/samples/sample13.cmd)]

## <a name="actions-with-collection-parameters"></a><span data-ttu-id="4890a-174">컬렉션 매개 변수를 사용한 작업</span><span class="sxs-lookup"><span data-stu-id="4890a-174">Actions with Collection Parameters</span></span>

<span data-ttu-id="4890a-175">작업에는 값 컬렉션을 사용 하는 매개 변수가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-175">Actions can have parameters that take a collection of values.</span></span> <span data-ttu-id="4890a-176">EDM에서 **collectionparameter&lt;t&gt;** 를 사용 하 여 매개 변수를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-176">In the EDM, use **CollectionParameter&lt;T&gt;** to declare the parameter.</span></span>

[!code-csharp[Main](odata-actions/samples/sample14.cs)]

<span data-ttu-id="4890a-177">이 매개 변수는 **int** 값의 컬렉션을 사용 하는 "등급" 이라는 매개 변수를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-177">This declares a parameter named "Ratings" that takes a collection of **int** values.</span></span> <span data-ttu-id="4890a-178">Controller 메서드에서 **ODataActionParameters** 개체의 매개 변수 값을 가져오지만 이제 값은 **ICollection&lt;int&gt;** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-178">In the controller method, you still get the parameter value from the **ODataActionParameters** object, but now the value is an **ICollection&lt;int&gt;** value:</span></span>

[!code-csharp[Main](odata-actions/samples/sample15.cs)]

## <a name="transient-actions"></a><span data-ttu-id="4890a-179">임시 작업</span><span class="sxs-lookup"><span data-stu-id="4890a-179">Transient Actions</span></span>

<span data-ttu-id="4890a-180">"RateProduct" 예제에서 사용자는 항상 제품의 등급을 지정할 수 있으므로 작업을 항상 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-180">In the "RateProduct" example, users can always rate a product, so the action is always available.</span></span> <span data-ttu-id="4890a-181">하지만 일부 작업은 엔터티의 상태에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-181">But some actions depend on the state of the entity.</span></span> <span data-ttu-id="4890a-182">예를 들어 비디오 임대 서비스에서는 "체크 아웃" 작업을 항상 사용할 수 있는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-182">For example, in a video rental service, the "CheckOut" action is not always available.</span></span> <span data-ttu-id="4890a-183">이는 해당 비디오의 복사본을 사용할 수 있는지 여부에 따라 달라 집니다. 이 동작 유형을 *일시적* 동작 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-183">(It depends whether a copy of that video is available.) This type of action is called a *transient* action.</span></span>

<span data-ttu-id="4890a-184">서비스 메타 데이터에서 일시적인 작업에는 **IsAlwaysBindable** 가 false와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-184">In the service metadata, a transient action has **IsAlwaysBindable** equal to false.</span></span> <span data-ttu-id="4890a-185">이것은 실제로 기본값 이므로 메타 데이터는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-185">That's actually the default value, so the metadata will look like this:</span></span>

[!code-xml[Main](odata-actions/samples/sample16.xml)]

<span data-ttu-id="4890a-186">이 문제가 발생 하는 이유는 다음과 같습니다. 동작이 일시적인 경우 서버에서 작업을 사용할 수 있을 때 클라이언트에 게 알려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-186">Here's why this matters: If an action is transient, the server needs to tell the client when the action is available.</span></span> <span data-ttu-id="4890a-187">엔터티의 작업에 대 한 링크를 포함 하 여이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-187">It does this by including a link to the action in the entity.</span></span> <span data-ttu-id="4890a-188">동영상 엔터티에 대 한 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-188">Here is an example for a Movie entity:</span></span>

[!code-console[Main](odata-actions/samples/sample17.cmd)]

<span data-ttu-id="4890a-189">"#CheckOut" 속성에는 체크 아웃 작업에 대 한 링크가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-189">The "#CheckOut" property contains a link to the CheckOut action.</span></span> <span data-ttu-id="4890a-190">동작을 사용할 수 없는 경우 서버에서 해당 링크를 생략 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-190">If the action is not available, the server omits the link.</span></span>

<span data-ttu-id="4890a-191">EDM에서 임시 작업을 선언 하려면 **TransientAction** 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-191">To declare a transient action in the EDM, call the **TransientAction** method:</span></span>

[!code-csharp[Main](odata-actions/samples/sample18.cs)]

<span data-ttu-id="4890a-192">또한 지정 된 엔터티에 대 한 작업 링크를 반환 하는 함수를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-192">Also, you must provide a function that returns an action link for a given entity.</span></span> <span data-ttu-id="4890a-193">**Hasactionlink**를 호출 하 여이 함수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-193">Set this function by calling **HasActionLink**.</span></span> <span data-ttu-id="4890a-194">함수를 람다 식으로 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-194">You can write the function as a lambda expression:</span></span>

[!code-csharp[Main](odata-actions/samples/sample19.cs)]

<span data-ttu-id="4890a-195">동작을 사용할 수 있는 경우 람다 식에서 작업에 대 한 링크를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-195">If the action is available, the lambda expression returns a link to the action.</span></span> <span data-ttu-id="4890a-196">OData serializer는 엔터티를 직렬화 할 때이 링크를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-196">The OData serializer includes this link when it serializes the entity.</span></span> <span data-ttu-id="4890a-197">동작을 사용할 수 없는 경우 함수는 `null`반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4890a-197">When the action is not available, the function returns `null`.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4890a-198">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="4890a-198">Additional Resources</span></span>

[<span data-ttu-id="4890a-199">OData 작업 샘플</span><span class="sxs-lookup"><span data-stu-id="4890a-199">OData Actions Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v3/ODataActionsSample/)
