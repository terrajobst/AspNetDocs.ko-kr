---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
title: '7 부: 기본 페이지 만들기 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: eb32a17b-626c-4373-9a7d-3387992f3c04
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
msc.type: authoredcontent
ms.openlocfilehash: fe4074c701159a137be3644d65ca844f160c2399
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599982"
---
# <a name="part-7-creating-the-main-page"></a><span data-ttu-id="b33f3-102">7 부: 기본 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="b33f3-102">Part 7: Creating the Main Page</span></span>

<span data-ttu-id="b33f3-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b33f3-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="b33f3-104">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="b33f3-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-the-main-page"></a><span data-ttu-id="b33f3-105">기본 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="b33f3-105">Creating the Main Page</span></span>

<span data-ttu-id="b33f3-106">이 섹션에서는 주 응용 프로그램 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-106">In this section, you will create the main application page.</span></span> <span data-ttu-id="b33f3-107">이 페이지는 관리 페이지 보다 복잡 하므로 여러 단계로 접근 합니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-107">This page will be more complex than the Admin page, so we'll approach it in several steps.</span></span> <span data-ttu-id="b33f3-108">이 과정에서 몇 가지 고급에 대 한 몇 가지 고급 녹아웃 기술이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-108">Along the way, you'll see some more advanced Knockout.js techniques.</span></span> <span data-ttu-id="b33f3-109">페이지의 기본 레이아웃은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-109">Here is the basic layout of the page:</span></span>

![](using-web-api-with-entity-framework-part-7/_static/image1.png)

- <span data-ttu-id="b33f3-110">"Products"는 제품 배열을 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-110">"Products" holds an array of products.</span></span>
- <span data-ttu-id="b33f3-111">"카트"는 수량이 포함 된 제품의 배열을 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-111">"Cart" holds an array of products with quantities.</span></span> <span data-ttu-id="b33f3-112">"카트에 추가"를 클릭 하면 카트를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-112">Clicking "Add to Cart" updates the cart.</span></span>
- <span data-ttu-id="b33f3-113">"Orders"는 주문 Id의 배열을 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-113">"Orders" holds an array of order IDs.</span></span>
- <span data-ttu-id="b33f3-114">"세부 정보"는 항목 배열 (수량이 있는 제품) 인 주문 세부 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-114">"Details" holds an order detail, which is an array of items (products with quantities)</span></span>

<span data-ttu-id="b33f3-115">데이터 바인딩이나 스크립트 없이 HTML에서 몇 가지 기본 레이아웃을 정의 하는 것부터 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-115">We'll start by defining some basic layout in HTML, with no data binding or script.</span></span> <span data-ttu-id="b33f3-116">파일 Views/Home/Index를 열고 모든 내용을 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-116">Open the file Views/Home/Index.cshtml and replace all of the contents with the following:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample1.html)]

<span data-ttu-id="b33f3-117">다음으로 스크립트 섹션을 추가 하 고 빈 뷰-모델을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-117">Next, add a Scripts section and create an empty view-model:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-7/samples/sample2.cshtml)]

<span data-ttu-id="b33f3-118">이전에 스케치 된 디자인을 기반으로 하는 보기 모델에는 제품, 카트, 주문 및 세부 정보에 대 한 관찰 가능 개체 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-118">Based on the design sketched earlier, our view model needs observables for products, cart, orders, and details.</span></span> <span data-ttu-id="b33f3-119">`AppViewModel` 개체에 다음 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-119">Add the following variables to the `AppViewModel` object:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample3.js)]

<span data-ttu-id="b33f3-120">사용자는 제품 목록의 항목을 카트에 추가 하 고 카트에 항목을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-120">Users can add items from the products list into the cart, and remove items from the cart.</span></span> <span data-ttu-id="b33f3-121">이러한 함수를 캡슐화 하기 위해 제품을 나타내는 또 다른 뷰 모델 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-121">To encapsulate these functions, we'll create another view-model class that represents a product.</span></span> <span data-ttu-id="b33f3-122">다음 코드를 `AppViewModel`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-122">Add the following code to `AppViewModel`:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample4.js?highlight=4)]

<span data-ttu-id="b33f3-123">`ProductViewModel` 클래스에는 카트에 제품을 이동 하는 데 사용 되는 두 개의 함수가 포함 되어 있습니다. `addItemToCart`는 제품의 한 단위를 카트에 추가 하 고 `removeAllFromCart` 제품의 모든 수량을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-123">The `ProductViewModel` class contains two functions that are used to move the product to and from the cart: `addItemToCart` adds one unit of the product to the cart, and `removeAllFromCart` removes all quantities of the product.</span></span>

<span data-ttu-id="b33f3-124">사용자는 기존 주문을 선택 하 고 주문 세부 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-124">Users can select an existing order and get the order details.</span></span> <span data-ttu-id="b33f3-125">이 기능은 다른 보기-모델에 캡슐화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-125">We'll encapsulate this functionality into another view-model:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample5.js?highlight=4)]

<span data-ttu-id="b33f3-126">`OrderDetailsViewModel`은 순서로 초기화 되며 서버에 AJAX 요청을 전송 하 여 주문 정보를 페치합니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-126">The `OrderDetailsViewModel` is initialized with an order, and it fetches the order details by sending an AJAX request to the server.</span></span>

<span data-ttu-id="b33f3-127">또한 `OrderDetailsViewModel`에 `total` 속성이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-127">Also, notice the `total` property on the `OrderDetailsViewModel`.</span></span> <span data-ttu-id="b33f3-128">이 속성은 [계산 된 관찰](http://knockoutjs.com/documentation/computedObservables.html)가능 이라고 하는 특수 한 종류의 관찰 가능입니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-128">This property is a special kind of observable called a [computed observable](http://knockoutjs.com/documentation/computedObservables.html).</span></span> <span data-ttu-id="b33f3-129">이름에서 알 수 있듯이 계산 된 관찰 가능을 통해 계산 된 값&#8212;(이 경우 주문의 총 비용)에 데이터를 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-129">As the name implies, a computed observable lets you data bind to a computed value&#8212;in this case, the total cost of the order.</span></span>

<span data-ttu-id="b33f3-130">그런 다음 `AppViewModel`에 다음 함수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-130">Next, add these functions to `AppViewModel`:</span></span>

- <span data-ttu-id="b33f3-131">`resetCart` 카트에 있는 모든 항목을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-131">`resetCart` removes all items from the cart.</span></span>
- <span data-ttu-id="b33f3-132">`getDetails`는 주문에 대 한 세부 정보를 가져옵니다 (`details` 목록에 새 `OrderDetailsViewModel` 푸시).</span><span class="sxs-lookup"><span data-stu-id="b33f3-132">`getDetails` gets the details for an order (by pushing a new `OrderDetailsViewModel` onto the `details` list).</span></span>
- <span data-ttu-id="b33f3-133">`createOrder` 새 주문을 만들고 카트를 비웁니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-133">`createOrder` creates a new order and empties the cart.</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample6.js?highlight=4)]

<span data-ttu-id="b33f3-134">마지막으로 제품 및 주문에 대 한 AJAX 요청을 작성 하 여 뷰 모델을 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-134">Finally, initialize the view model by making AJAX requests for the products and orders:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample7.js)]

<span data-ttu-id="b33f3-135">코드는 많지만,이를 단계별로 작성 했으므로 디자인을 명확 하 게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-135">OK, that's a lot of code, but we built it up step-by-step, so hopefully the design is clear.</span></span> <span data-ttu-id="b33f3-136">이제 HTML에 일부 녹아웃 바인딩을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-136">Now we can add some Knockout.js bindings to the HTML.</span></span>

<span data-ttu-id="b33f3-137">**상품**</span><span class="sxs-lookup"><span data-stu-id="b33f3-137">**Products**</span></span>

<span data-ttu-id="b33f3-138">제품 목록에 대 한 바인딩은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-138">Here are the bindings for the product list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample8.html)]

<span data-ttu-id="b33f3-139">이는 products 배열을 반복 하 고 이름 및 가격을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-139">This iterates over the products array and displays the name and price.</span></span> <span data-ttu-id="b33f3-140">"주문에 추가" 단추는 사용자가 로그인 한 경우에만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-140">The "Add to Order" button is visible only when the user is logged in.</span></span>

<span data-ttu-id="b33f3-141">"주문에 추가" 단추는 제품의 `ProductViewModel` 인스턴스에서 `addItemToCart`를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-141">The "Add to Order" button calls `addItemToCart` on the `ProductViewModel` instance for the product.</span></span> <span data-ttu-id="b33f3-142">이는 녹아웃의 유용한 기능을 보여 줍니다. 뷰 모델에 다른 뷰 모델이 포함 되어 있으면 바인딩을 내부 모델에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-142">This demonstrates a nice feature of Knockout.js: When a view-model contains other view-models, you can apply the bindings to the inner model.</span></span> <span data-ttu-id="b33f3-143">이 예에서는 `foreach` 내의 바인딩이 각 `ProductViewModel` 인스턴스에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-143">In this example, the bindings within the `foreach` are applied to each of the `ProductViewModel` instances.</span></span> <span data-ttu-id="b33f3-144">이 방법은 모든 기능을 단일 뷰 모델에 배치 하는 것 보다 훨씬 더 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-144">This approach is much cleaner than putting all of the functionality into a single view-model.</span></span>

<span data-ttu-id="b33f3-145">**마차**</span><span class="sxs-lookup"><span data-stu-id="b33f3-145">**Cart**</span></span>

<span data-ttu-id="b33f3-146">카트에 대 한 바인딩은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-146">Here are the bindings for the cart:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample9.html)]

<span data-ttu-id="b33f3-147">그러면 카트 배열을 반복 하 고 이름, 가격 및 수량을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-147">This iterates over the cart array and displays the name, price, and quantity.</span></span> <span data-ttu-id="b33f3-148">"제거" 링크와 "주문 만들기" 단추는 뷰 모델 함수에 바인딩되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-148">Note that the "Remove" link and the "Create Order" button are bound to view-model functions.</span></span>

<span data-ttu-id="b33f3-149">**주문과**</span><span class="sxs-lookup"><span data-stu-id="b33f3-149">**Orders**</span></span>

<span data-ttu-id="b33f3-150">주문 목록에 대 한 바인딩은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-150">Here are the bindings for the orders list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample10.html)]

<span data-ttu-id="b33f3-151">주문을 반복 하 고 주문 ID를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-151">This iterates over the orders and shows the order ID.</span></span> <span data-ttu-id="b33f3-152">링크의 click 이벤트는 `getDetails` 함수에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-152">The click event on the link is bound to the `getDetails` function.</span></span>

<span data-ttu-id="b33f3-153">**주문 정보**</span><span class="sxs-lookup"><span data-stu-id="b33f3-153">**Order Details**</span></span>

<span data-ttu-id="b33f3-154">주문 정보에 대 한 바인딩은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-154">Here are the bindings for the order details:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample11.html)]

<span data-ttu-id="b33f3-155">그러면 주문의 항목을 반복 하 여 제품, 가격 및 수량을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-155">This iterates over the items in the order and displays the product, price, and quantity.</span></span> <span data-ttu-id="b33f3-156">주변 div는 세부 정보 배열에 하나 이상의 항목이 포함 된 경우에만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-156">The surrounding div is visible only if the details array contains one or more items.</span></span>

## <a name="conclusion"></a><span data-ttu-id="b33f3-157">결론</span><span class="sxs-lookup"><span data-stu-id="b33f3-157">Conclusion</span></span>

<span data-ttu-id="b33f3-158">이 자습서에서는 Entity Framework를 사용 하 여 데이터베이스와 통신 하는 응용 프로그램을 만들고 ASP.NET Web API 데이터 계층 위에 공용 인터페이스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-158">In this tutorial, you created an application that uses Entity Framework to communicate with the database, and ASP.NET Web API to provide a public-facing interface on top of the data layer.</span></span> <span data-ttu-id="b33f3-159">ASP.NET MVC 4를 사용 하 여 HTML 페이지를 렌더링 하 고, .js와 jQuery를 사용 하 여 페이지를 다시 로드 하지 않고 동적 상호 작용을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b33f3-159">We use ASP.NET MVC 4 to render the HTML pages, and Knockout.js plus jQuery to provide dynamic interactions without page reloads.</span></span>

<span data-ttu-id="b33f3-160">추가 리소스:</span><span class="sxs-lookup"><span data-stu-id="b33f3-160">Additional resources:</span></span>

- [<span data-ttu-id="b33f3-161">ASP.NET 데이터 액세스 내용 맵</span><span class="sxs-lookup"><span data-stu-id="b33f3-161">ASP.NET Data Access Content Map</span></span>](https://msdn.microsoft.com/library/6759sth4.aspx)
- [<span data-ttu-id="b33f3-162">Entity Framework 개발자 센터</span><span class="sxs-lookup"><span data-stu-id="b33f3-162">Entity Framework Developer Center</span></span>](https://msdn.microsoft.com/data/ef)

> [!div class="step-by-step"]
> [<span data-ttu-id="b33f3-163">이전</span><span class="sxs-lookup"><span data-stu-id="b33f3-163">Previous</span></span>](using-web-api-with-entity-framework-part-6.md)
