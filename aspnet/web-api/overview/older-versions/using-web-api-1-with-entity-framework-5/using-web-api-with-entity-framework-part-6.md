---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
title: '6 부: 제품 및 주문 컨트롤러 만들기 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 91ee29ee-0689-40ee-914a-e7dd733b6622
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
msc.type: authoredcontent
ms.openlocfilehash: e0bf88e3477acbde910cde956042449bc86ce79a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421289"
---
# <a name="part-6-creating-product-and-order-controllers"></a><span data-ttu-id="6bdc2-102">6 부: 제품 및 주문 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="6bdc2-102">Part 6: Creating Product and Order Controllers</span></span>

<span data-ttu-id="6bdc2-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="6bdc2-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="6bdc2-104">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="6bdc2-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-a-products-controller"></a><span data-ttu-id="6bdc2-105">제품 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="6bdc2-105">Add a Products Controller</span></span>

<span data-ttu-id="6bdc2-106">관리자 컨트롤러는 관리자 권한을 가진 사용자를 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-106">The Admin controller is for users who have administrator privileges.</span></span> <span data-ttu-id="6bdc2-107">반면, 고객은 제품을 볼 수 있지만 생성, 업데이트 또는 삭제할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-107">Customers, on the other hand, can view products but cannot create, update, or delete them.</span></span>

<span data-ttu-id="6bdc2-108">Get 메서드를 열어 둔 상태에서 Post, Put 및 Delete 메서드에 대 한 액세스를 쉽게 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-108">We can easily restrict access to the Post, Put, and Delete methods, while leaving the Get methods open.</span></span> <span data-ttu-id="6bdc2-109">그러나 제품에 대해 반환 되는 데이터를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-109">But look at the data that is returned for a product:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample1.json?highlight=1)]

<span data-ttu-id="6bdc2-110">`ActualCost` 속성은 고객에 게 표시 되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-110">The `ActualCost` property should not be visible to customers!</span></span> <span data-ttu-id="6bdc2-111">이 솔루션은 고객에 게 표시 되는 속성의 하위 집합을 포함 하는 DTO ( *데이터 전송 개체* )를 정의 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-111">The solution is to define a *data transfer object* (DTO) that includes a subset of properties that should be visible to customers.</span></span> <span data-ttu-id="6bdc2-112">LINQ to project `Product` 인스턴스를 사용 하 여 인스턴스를 `ProductDTO` 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-112">We will use LINQ to project `Product` instances to `ProductDTO` instances.</span></span>

<span data-ttu-id="6bdc2-113">`ProductDTO` 라는 클래스를 모델 폴더에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-113">Add a class named `ProductDTO` to the Models folder.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample2.cs)]

<span data-ttu-id="6bdc2-114">이제 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-114">Now add the controller.</span></span> <span data-ttu-id="6bdc2-115">솔루션 탐색기에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-115">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="6bdc2-116">**추가**를 선택한 다음 **컨트롤러**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-116">Select **Add**, then select **Controller**.</span></span> <span data-ttu-id="6bdc2-117">**컨트롤러 추가** 대화 상자에서 컨트롤러 이름을 ProductsController&quot;로 &quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-117">In the **Add Controller** dialog, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="6bdc2-118">**템플릿**아래에서 **빈 API 컨트롤러**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-118">Under **Template**, select **Empty API controller**.</span></span>

![](using-web-api-with-entity-framework-part-6/_static/image1.png)

<span data-ttu-id="6bdc2-119">소스 파일의 모든 항목을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-119">Replace everything in the source file with the following code:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample3.cs)]

<span data-ttu-id="6bdc2-120">컨트롤러는 여전히 `OrdersContext`를 사용 하 여 데이터베이스를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-120">The controller still uses the `OrdersContext` to query the database.</span></span> <span data-ttu-id="6bdc2-121">그러나 `Product` 인스턴스를 직접 반환 하는 대신 `MapProducts`를 호출 하 여 `ProductDTO` 인스턴스에 프로젝션 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-121">But instead of returning `Product` instances directly, we call `MapProducts` to project them onto `ProductDTO` instances:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample4.cs?highlight=1)]

<span data-ttu-id="6bdc2-122">`MapProducts` 메서드는 **IQueryable**을 반환 하므로 다른 쿼리 매개 변수를 사용 하 여 결과를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-122">The `MapProducts` method returns an **IQueryable**, so we can compose the result with other query parameters.</span></span> <span data-ttu-id="6bdc2-123">쿼리에 **where** 절을 추가 하는 `GetProduct` 메서드에서이를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-123">You can see this in the `GetProduct` method, which adds a **where** clause to the query:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample5.cs?highlight=2)]

## <a name="add-an-orders-controller"></a><span data-ttu-id="6bdc2-124">주문 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="6bdc2-124">Add an Orders Controller</span></span>

<span data-ttu-id="6bdc2-125">그런 다음 사용자가 주문을 만들고 볼 수 있도록 하는 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-125">Next, add a controller that lets users create and view orders.</span></span>

<span data-ttu-id="6bdc2-126">다른 DTO 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-126">We'll start with another DTO.</span></span> <span data-ttu-id="6bdc2-127">솔루션 탐색기에서 모델 폴더를 마우스 오른쪽 단추로 클릭 하 `OrderDTO` 라는 클래스를 추가 합니다. 다음 구현을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-127">In Solution Explorer, right-click the Models folder and add a class named `OrderDTO` Use the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample6.cs)]

<span data-ttu-id="6bdc2-128">이제 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-128">Now add the controller.</span></span> <span data-ttu-id="6bdc2-129">솔루션 탐색기에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-129">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="6bdc2-130">**추가**를 선택한 다음 **컨트롤러**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-130">Select **Add**, then select **Controller**.</span></span> <span data-ttu-id="6bdc2-131">**컨트롤러 추가** 대화 상자에서 다음 옵션을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-131">In the **Add Controller** dialog, set the following options:</span></span>

- <span data-ttu-id="6bdc2-132">**컨트롤러 이름**에 "OrdersController"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-132">Under **Controller Name**, enter "OrdersController".</span></span>
- <span data-ttu-id="6bdc2-133">**템플릿**에서 "Entity Framework 사용 하 여 읽기/쓰기 작업을 포함 하는 API 컨트롤러를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-133">Under **Template**, select "API controller with read/write actions, using Entity Framework".</span></span>
- <span data-ttu-id="6bdc2-134">**모델 클래스**에서 &quot;Order (제품 스토어. 모델)&quot;를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-134">Under **Model class**, select &quot;Order (ProductStore.Models)&quot;.</span></span>
- <span data-ttu-id="6bdc2-135">**데이터 컨텍스트 클래스**에서 &quot;OrdersContext (제품 스토어. 모델)&quot;를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-135">Under **Data context class**, select &quot;OrdersContext (ProductStore.Models)&quot;.</span></span>

![](using-web-api-with-entity-framework-part-6/_static/image2.png)

<span data-ttu-id="6bdc2-136">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-136">Click **Add**.</span></span> <span data-ttu-id="6bdc2-137">그러면 이름이 OrdersController.cs 인 파일이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-137">This adds a file named OrdersController.cs.</span></span> <span data-ttu-id="6bdc2-138">다음에는 컨트롤러의 기본 구현을 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-138">Next, we need to modify the default implementation of the controller.</span></span>

<span data-ttu-id="6bdc2-139">먼저 `PutOrder` 및 `DeleteOrder` 메서드를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-139">First, delete the `PutOrder` and `DeleteOrder` methods.</span></span> <span data-ttu-id="6bdc2-140">이 샘플에서는 고객이 기존 주문을 수정 하거나 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-140">For this sample, customers cannot modify or delete existing orders.</span></span> <span data-ttu-id="6bdc2-141">실제 응용 프로그램에서는 이러한 경우를 처리 하는 백 엔드 논리가 많이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-141">In a real application, you would need lots of back-end logic to handle these cases.</span></span> <span data-ttu-id="6bdc2-142">(예를 들어 주문이 이미 배송 되었습니까?)</span><span class="sxs-lookup"><span data-stu-id="6bdc2-142">(For example, was the order already shipped?)</span></span>

<span data-ttu-id="6bdc2-143">사용자에 게 속한 주문만 반환 하도록 `GetOrders` 메서드를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-143">Change the `GetOrders` method to return just the orders that belong to the user:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample7.cs)]

<span data-ttu-id="6bdc2-144">`GetOrder` 메서드를 다음과 같이 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-144">Change the `GetOrder` method as follows:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample8.cs)]

<span data-ttu-id="6bdc2-145">다음은 메서드에 적용 된 변경 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-145">Here are the changes that we made to the method:</span></span>

- <span data-ttu-id="6bdc2-146">반환 값은 `Order`대신 `OrderDTO` 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-146">The return value is an `OrderDTO` instance, instead of an `Order`.</span></span>
- <span data-ttu-id="6bdc2-147">주문에 대 한 데이터베이스를 쿼리할 때 [Dbquery. Include](https://msdn.microsoft.com/library/gg696395) 메서드를 사용 하 여 관련 `OrderDetail` 및 `Product` 엔터티를 인출 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-147">When we query the database for the order, we use the [DbQuery.Include](https://msdn.microsoft.com/library/gg696395) method to fetch the related `OrderDetail` and `Product` entities.</span></span>
- <span data-ttu-id="6bdc2-148">프로젝션을 사용 하 여 결과를 평면화 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-148">We flatten the result by using a projection.</span></span>

<span data-ttu-id="6bdc2-149">HTTP 응답은 수량을 포함 하는 제품 배열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-149">The HTTP response will contain an array of products with quantities:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample9.json)]

<span data-ttu-id="6bdc2-150">이 형식은 클라이언트에서 중첩 된 엔터티 (주문, 세부 정보 및 제품)를 포함 하는 원래 개체 그래프 보다 더 쉽게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-150">This format is easier for clients to consume than the original object graph, which contains nested entities (order, details, and products).</span></span>

<span data-ttu-id="6bdc2-151">이 `PostOrder`가장 먼저 고려해 야 할 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-151">The last method to consider it `PostOrder`.</span></span> <span data-ttu-id="6bdc2-152">현재이 메서드는 `Order` 인스턴스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-152">Right now, this method takes an `Order` instance.</span></span> <span data-ttu-id="6bdc2-153">그러나 클라이언트에서 다음과 같이 요청 본문을 보내는 경우에는 어떻게 되는지 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-153">But consider what happens if a client sends a request body like this:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample10.json)]

<span data-ttu-id="6bdc2-154">이는 잘 구성 된 순서 이며, Entity Framework는이를 데이터베이스에 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-154">This is a well-structured order, and Entity Framework will happily insert it into the database.</span></span> <span data-ttu-id="6bdc2-155">하지만 이전에 존재 하지 않았던 제품 엔터티를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-155">But it contains a Product entity that did not exist previously.</span></span> <span data-ttu-id="6bdc2-156">클라이언트는 데이터베이스에 새 제품을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-156">The client just created a new product in our database!</span></span> <span data-ttu-id="6bdc2-157">이는 koala의 주문에 대 한 주문이 표시 되는 주문 처리 부서에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-157">This will be a surprise to the order fulfillment department, when they see an order for koala bears.</span></span> <span data-ttu-id="6bdc2-158">도덕적는 POST 또는 PUT 요청에서 허용 하는 데이터에 대 한 주의를 기울여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-158">The moral is, be really careful about the data you accept in a POST or PUT request.</span></span>

<span data-ttu-id="6bdc2-159">이 문제를 방지 하려면 `PostOrder` 메서드를 변경 하 여 `OrderDTO` 인스턴스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-159">To avoid this problem, change the `PostOrder` method to take an `OrderDTO` instance.</span></span> <span data-ttu-id="6bdc2-160">`OrderDTO`를 사용 하 여 `Order`를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-160">Use the `OrderDTO` to create the `Order`.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample11.cs)]

<span data-ttu-id="6bdc2-161">`ProductID` 및 `Quantity` 속성을 사용 하며, 클라이언트에서 제품 이름 또는 가격 중 하나에 대해 보낸 값을 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-161">Notice that we use the `ProductID` and `Quantity` properties, and we ignore any values that the client sent for either product name or price.</span></span> <span data-ttu-id="6bdc2-162">제품 ID가 유효 하지 않은 경우 데이터베이스의 foreign key 제약 조건을 위반 하 고 삽입이 실패 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-162">If the product ID is not valid, it will violate the foreign key constraint in the database, and the insert will fail, as it should.</span></span>

<span data-ttu-id="6bdc2-163">다음은 전체 `PostOrder` 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-163">Here is the complete `PostOrder` method:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample12.cs)]

<span data-ttu-id="6bdc2-164">마지막으로 **권한 부여** 특성을 컨트롤러에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-164">Finally, add the **Authorize** attribute to the controller:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample13.cs)]

<span data-ttu-id="6bdc2-165">이제 등록 된 사용자만 주문을 만들거나 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bdc2-165">Now only registered users can create or view orders.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6bdc2-166">[이전](using-web-api-with-entity-framework-part-5.md)
> [다음](using-web-api-with-entity-framework-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="6bdc2-166">[Previous](using-web-api-with-entity-framework-part-5.md)
[Next](using-web-api-with-entity-framework-part-7.md)</span></span>
