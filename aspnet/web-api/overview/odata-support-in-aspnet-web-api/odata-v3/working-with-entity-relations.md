---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
title: Web API 2를 사용 하 여 OData v3에서 엔터티 관계 지원 | Microsoft Docs
author: MikeWasson
description: 대부분의 데이터 집합은 엔터티 간의 관계를 정의 합니다. 고객에 게는 주문이 있습니다. 서적에는 작성자가 있습니다. 제품에는 공급자가 있습니다. 클라이언트는 OData를 사용 하 여 탐색할 수 있습니다 ...
ms.author: riande
ms.date: 02/26/2014
ms.assetid: 1e4c2eb4-b6cf-42ff-8a65-4d71ddca0394
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
msc.type: authoredcontent
ms.openlocfilehash: 726a7d51123805e05f6831ef9cd7eaa84b6c44bd
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600308"
---
# <a name="supporting-entity-relations-in-odata-v3-with-web-api-2"></a><span data-ttu-id="c8832-104">Web API 2를 사용 하 여 OData v3에서 엔터티 관계 지원</span><span class="sxs-lookup"><span data-stu-id="c8832-104">Supporting Entity Relations in OData v3 with Web API 2</span></span>

<span data-ttu-id="c8832-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c8832-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="c8832-106">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="c8832-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="c8832-107">대부분의 데이터 집합은 엔터티 간의 관계를 정의 합니다. 고객에 게는 주문이 있습니다. 서적에는 작성자가 있습니다. 제품에는 공급자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-107">Most data sets define relations between entities: Customers have orders; books have authors; products have suppliers.</span></span> <span data-ttu-id="c8832-108">클라이언트는 OData를 사용 하 여 엔터티 관계를 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-108">Using OData, clients can navigate over entity relations.</span></span> <span data-ttu-id="c8832-109">제품을 제공 하는 경우 공급자를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-109">Given a product, you can find the supplier.</span></span> <span data-ttu-id="c8832-110">관계를 만들거나 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-110">You can also create or remove relationships.</span></span> <span data-ttu-id="c8832-111">예를 들어 제품의 공급 업체를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-111">For example, you can set the supplier for a product.</span></span>
> 
> <span data-ttu-id="c8832-112">이 자습서에서는 ASP.NET Web API에서 이러한 작업을 지 원하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-112">This tutorial shows how to support these operations in ASP.NET Web API.</span></span> <span data-ttu-id="c8832-113">이 자습서는 [WEB API 2를 사용 하 여 OData V3 끝점 만들기](creating-an-odata-endpoint.md)자습서를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-113">The tutorial builds on the tutorial [Creating an OData v3 Endpoint with Web API 2](creating-an-odata-endpoint.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="c8832-114">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="c8832-114">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="c8832-115">Web API 2</span><span class="sxs-lookup"><span data-stu-id="c8832-115">Web API 2</span></span>
> - <span data-ttu-id="c8832-116">OData 버전 3</span><span class="sxs-lookup"><span data-stu-id="c8832-116">OData Version 3</span></span>
> - <span data-ttu-id="c8832-117">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="c8832-117">Entity Framework 6</span></span>

## <a name="add-a-supplier-entity"></a><span data-ttu-id="c8832-118">공급자 엔터티 추가</span><span class="sxs-lookup"><span data-stu-id="c8832-118">Add a Supplier Entity</span></span>

<span data-ttu-id="c8832-119">먼저 OData 피드에 새 엔터티 형식을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-119">First we need to add a new entity type to our OData feed.</span></span> <span data-ttu-id="c8832-120">`Supplier` 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-120">We'll add a `Supplier` class.</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample1.cs)]

<span data-ttu-id="c8832-121">이 클래스는 엔터티 키에 대 한 문자열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-121">This class uses a string for the entity key.</span></span> <span data-ttu-id="c8832-122">실제로는 정수 키를 사용 하는 것 보다 일반적이 지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-122">In practice, that might be less common than using an integer key.</span></span> <span data-ttu-id="c8832-123">그러나 OData에서 정수 외에 다른 키 형식을 처리 하는 방법을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-123">But it's worth seeing how OData handles other key types besides integers.</span></span>

<span data-ttu-id="c8832-124">다음으로 `Product` 클래스에 `Supplier` 속성을 추가 하 여 관계를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-124">Next, we'll create a relation by adding a `Supplier` property to the `Product` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample2.cs)]

<span data-ttu-id="c8832-125">`ProductServiceContext` 클래스에 새 **Dbset** 을 추가 하 Entity Framework 데이터베이스에 `Supplier` 테이블을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-125">Add a new **DbSet** to the `ProductServiceContext` class, so that Entity Framework will include the `Supplier` table in the database.</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample3.cs?highlight=9)]

<span data-ttu-id="c8832-126">WebApiConfig.cs에서 EDM 모델에 "Suppliers" 엔터티를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-126">In WebApiConfig.cs, add a "Suppliers" entity to the EDM model:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample4.cs?highlight=4)]

## <a name="navigation-properties"></a><span data-ttu-id="c8832-127">탐색 속성</span><span class="sxs-lookup"><span data-stu-id="c8832-127">Navigation Properties</span></span>

<span data-ttu-id="c8832-128">제품에 대 한 공급자를 가져오기 위해 클라이언트는 GET 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-128">To get the supplier for a product, the client sends a GET request:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample5.cmd)]

<span data-ttu-id="c8832-129">여기에서 "공급자"는 `Product` 형식에 대 한 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-129">Here "Supplier" is a navigation property on the `Product` type.</span></span> <span data-ttu-id="c8832-130">이 경우 `Supplier`는 단일 항목을 참조 하지만 탐색 속성은 컬렉션 (일 대 다 또는 다 대 다 관계)을 반환할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-130">In this case, `Supplier` refers to a single item, but a navigation property can also return a collection (one-to-many or many-to-many relation).</span></span>

<span data-ttu-id="c8832-131">이 요청을 지원 하려면 `ProductsController` 클래스에 다음 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-131">To support this request, add the following method to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample6.cs)]

<span data-ttu-id="c8832-132">*키* 매개 변수는 제품의 키입니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-132">The *key* parameter is the key of the product.</span></span> <span data-ttu-id="c8832-133">메서드는 관련 엔터티&#8212;(이 경우 `Supplier` 인스턴스)를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-133">The method returns the related entity&#8212;in this case, a `Supplier` instance.</span></span> <span data-ttu-id="c8832-134">메서드 이름과 매개 변수 이름이 모두 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-134">The method name and parameter name are both important.</span></span> <span data-ttu-id="c8832-135">일반적으로 탐색 속성의 이름이 "X" 인 경우 "GetX" 라는 메서드를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-135">In general, if the navigation property is named "X", you need to add a method named "GetX".</span></span> <span data-ttu-id="c8832-136">메서드는 부모 키의 데이터 형식과 일치 하는 "*key*" 라는 매개 변수를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-136">The method must take a parameter named "*key*" that matches the data type of the parent's key.</span></span>

<span data-ttu-id="c8832-137">*키* 매개 변수에 **[Fromodatauri]** 특성을 포함 하는 것도 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-137">It is also important to include the **[FromOdataUri]** attribute in the *key* parameter.</span></span> <span data-ttu-id="c8832-138">이 특성은 요청 URI에서 키를 구문 분석할 때 OData 구문 규칙을 사용 하도록 Web API에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-138">This attribute tells Web API to use OData syntax rules when it parses the key from the request URI.</span></span>

## <a name="creating-and-deleting-links"></a><span data-ttu-id="c8832-139">링크 만들기 및 삭제</span><span class="sxs-lookup"><span data-stu-id="c8832-139">Creating and Deleting Links</span></span>

<span data-ttu-id="c8832-140">OData는 두 엔터티 간의 관계를 만들거나 제거 하는 것을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-140">OData supports creating or removing relationships between two entities.</span></span> <span data-ttu-id="c8832-141">OData 용어에서 관계는 "링크"입니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-141">In OData terminology, the relationship is a "link."</span></span> <span data-ttu-id="c8832-142">각 링크에는 *엔터티*/$links/*엔터티*형식의 URI가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-142">Each link has a URI with the form *entity*/$links/*entity*.</span></span> <span data-ttu-id="c8832-143">예를 들어 제품에서 공급자로의 링크는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-143">For example, the link from product to supplier looks like this:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample7.cmd)]

<span data-ttu-id="c8832-144">새 링크를 만들기 위해 클라이언트는 링크 URI에 POST 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-144">To create a new link, the client sends a POST request to the link URI.</span></span> <span data-ttu-id="c8832-145">요청의 본문은 대상 엔터티의 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-145">The body of the request is the URI of the target entity.</span></span> <span data-ttu-id="c8832-146">예를 들어 "CTSO" 라는 키가 있는 공급 업체가 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-146">For example, suppose there is a supplier with the key "CTSO".</span></span> <span data-ttu-id="c8832-147">"Product (1)"에서 "공급자 (' CTSO ')"로의 링크를 만들려면 클라이언트는 다음과 같은 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-147">To create a link from "Product(1)" to "Supplier('CTSO')", the client sends a request like the following:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample8.cmd)]

<span data-ttu-id="c8832-148">링크를 삭제 하기 위해 클라이언트는 링크 URI에 DELETE 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-148">To delete a link, the client sends a DELETE request to the link URI.</span></span>

<span data-ttu-id="c8832-149">**링크 만들기**</span><span class="sxs-lookup"><span data-stu-id="c8832-149">**Creating Links**</span></span>

<span data-ttu-id="c8832-150">클라이언트에서 제품 공급자 링크를 만들 수 있도록 하려면 `ProductsController` 클래스에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-150">To enable a client to create product-supplier links, add the following code to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample9.cs)]

<span data-ttu-id="c8832-151">이 메서드는</span><span class="sxs-lookup"><span data-stu-id="c8832-151">This method takes three parameters:</span></span>

- <span data-ttu-id="c8832-152">*키*: 부모 엔터티에 대 한 키 (제품)</span><span class="sxs-lookup"><span data-stu-id="c8832-152">*key*: The key to the parent entity (the product)</span></span>
- <span data-ttu-id="c8832-153">*navigationProperty*: 탐색 속성의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-153">*navigationProperty*: The name of the navigation property.</span></span> <span data-ttu-id="c8832-154">이 예제에서 유일 하 게 유효한 탐색 속성은 "공급 업체"입니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-154">In this example, the only valid navigation property is "Supplier".</span></span>
- <span data-ttu-id="c8832-155">*link*: 관련 엔터티의 OData URI입니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-155">*link*: The OData URI of the related entity.</span></span> <span data-ttu-id="c8832-156">이 값은 요청 본문에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-156">This value is taken from the request body.</span></span> <span data-ttu-id="c8832-157">예를 들어, 링크 URI는 ID = ' CTSO ' 인 공급자를 의미 하는 "`http://localhost/odata/Suppliers('CTSO')`일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-157">For example, the link URI might be "`http://localhost/odata/Suppliers('CTSO')`, meaning the supplier with ID = ‘CTSO'.</span></span>

<span data-ttu-id="c8832-158">메서드는 링크를 사용 하 여 공급자를 조회 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-158">The method uses the link to look up the supplier.</span></span> <span data-ttu-id="c8832-159">일치 하는 공급자가 있는 경우 메서드는 `Product.Supplier` 속성을 설정 하 고 결과를 데이터베이스에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-159">If the matching supplier is found, the method sets the `Product.Supplier` property and saves the result to the database.</span></span>

<span data-ttu-id="c8832-160">가장 어려운 부분은 링크 URI를 구문 분석 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-160">The hardest part is parsing the link URI.</span></span> <span data-ttu-id="c8832-161">기본적으로 해당 URI에 GET 요청을 보낸 결과를 시뮬레이션 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-161">Basically, you need to simulate the result of sending a GET request to that URI.</span></span> <span data-ttu-id="c8832-162">다음 도우미 메서드는이 작업을 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-162">The following helper method shows how to do this.</span></span> <span data-ttu-id="c8832-163">메서드는 Web API 라우팅 프로세스를 호출 하 고 구문 분석 된 OData 경로를 나타내는 **ODataPath** 인스턴스를 다시 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-163">The method invokes the Web API routing process and gets back an **ODataPath** instance that represents the parsed OData path.</span></span> <span data-ttu-id="c8832-164">링크 URI의 경우 세그먼트 중 하나가 엔터티 키 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-164">For a link URI, one of the segments should be the entity key.</span></span> <span data-ttu-id="c8832-165">그렇지 않은 경우 클라이언트에서 잘못 된 URI를 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-165">(If not, the client sent a bad URI.)</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample10.cs)]

<span data-ttu-id="c8832-166">**링크 삭제**</span><span class="sxs-lookup"><span data-stu-id="c8832-166">**Deleting Links**</span></span>

<span data-ttu-id="c8832-167">링크를 삭제 하려면 `ProductsController` 클래스에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-167">To delete a link, add the following code to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample11.cs)]

<span data-ttu-id="c8832-168">이 예제에서 탐색 속성은 단일 `Supplier` 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-168">In this example, the navigation property is a single `Supplier` entity.</span></span> <span data-ttu-id="c8832-169">탐색 속성이 컬렉션인 경우 링크를 삭제 하는 URI에는 관련 엔터티에 대 한 키가 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-169">If the navigation property is a collection, the URI to delete a link must include a key for the related entity.</span></span> <span data-ttu-id="c8832-170">예를 들면 다음과 같습니다.:</span><span class="sxs-lookup"><span data-stu-id="c8832-170">For example:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample12.cmd)]

<span data-ttu-id="c8832-171">이 요청은 고객 1의 주문 1을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-171">This request removes order 1 from customer 1.</span></span> <span data-ttu-id="c8832-172">이 경우 DeleteLink 메서드의 시그니처는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-172">In this case, the DeleteLink method will have the following signature:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample13.cs)]

<span data-ttu-id="c8832-173">*RelatedKey* 매개 변수는 관련 엔터티에 대 한 키를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-173">The *relatedKey* parameter gives the key for the related entity.</span></span> <span data-ttu-id="c8832-174">따라서 `DeleteLink` 메서드에서 *키* 매개 변수를 기준으로 기본 엔터티를 조회 하 고 *relatedKey* 매개 변수를 통해 관련 엔터티를 찾은 다음 연결을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-174">So in your `DeleteLink` method, look up the primary entity by the *key* parameter, find the related entity by the *relatedKey* parameter, and then remove the association.</span></span> <span data-ttu-id="c8832-175">데이터 모델에 따라 두 버전의 `DeleteLink`를 모두 구현 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-175">Depending on your data model, you might need to implement both versions of `DeleteLink`.</span></span> <span data-ttu-id="c8832-176">Web API는 요청 URI에 따라 올바른 버전을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8832-176">Web API will call the correct version based on the request URI.</span></span>
