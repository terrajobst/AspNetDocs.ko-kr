---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
title: '8 부: Ajax 업데이트가 포함 된 쇼핑 카트 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 8 부에서는 Ajax 업데이트가 포함 된 쇼핑 카트를 다룹니다.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 26b2f55e-ed42-4277-89b0-c941eb754145
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
msc.type: authoredcontent
ms.openlocfilehash: 89897ad41b217764cbd17317d4bf5d6a5c5d488f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433517"
---
# <a name="part-8-shopping-cart-with-ajax-updates"></a><span data-ttu-id="b3d85-104">8 부: Ajax 업데이트가 포함 된 쇼핑 카트</span><span class="sxs-lookup"><span data-stu-id="b3d85-104">Part 8: Shopping Cart with Ajax Updates</span></span>

<span data-ttu-id="b3d85-105">받은 사람 ( [Jon Galloway](https://github.com/jongalloway) )</span><span class="sxs-lookup"><span data-stu-id="b3d85-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="b3d85-106">MVC Music Store는 웹 개발용 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 소개 하 고 설명 하는 자습서 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="b3d85-107">MVC Music Store는 온라인으로 음악 앨범을 판매 하 고 기본적인 사이트 관리, 사용자 로그인 및 쇼핑 카트 기능을 구현 하는 간단한 샘플 저장소 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="b3d85-108">이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="b3d85-109">8 부에서는 Ajax 업데이트가 포함 된 쇼핑 카트를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-109">Part 8 covers Shopping Cart with Ajax Updates.</span></span>

<span data-ttu-id="b3d85-110">사용자가 등록 하지 않고 카트에 앨범을 저장할 수 있지만 체크 아웃을 완료 하려면 게스트로 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-110">We'll allow users to place albums in their cart without registering, but they'll need to register as guests to complete checkout.</span></span> <span data-ttu-id="b3d85-111">쇼핑 및 체크 아웃 프로세스는 두 개의 컨트롤러로 구분 됩니다. ShoppingCart Controller는 장바구니에 항목을 익명으로 추가할 수 있으며, 체크 아웃 프로세스를 처리 하는 체크 아웃 컨트롤러를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-111">The shopping and checkout process will be separated into two controllers: a ShoppingCart Controller which allows anonymously adding items to a cart, and a Checkout Controller which handles the checkout process.</span></span> <span data-ttu-id="b3d85-112">이 섹션에서 쇼핑 카트를 시작 하 고 다음 섹션에서 체크 아웃 프로세스를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-112">We'll start with the Shopping Cart in this section, then build the Checkout process in the following section.</span></span>

## <a name="adding-the-cart-order-and-orderdetail-model-classes"></a><span data-ttu-id="b3d85-113">카트, 주문 및 OrderDetail 모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="b3d85-113">Adding the Cart, Order, and OrderDetail model classes</span></span>

<span data-ttu-id="b3d85-114">쇼핑 카트 및 체크 아웃 프로세스는 일부 새로운 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-114">Our Shopping Cart and Checkout processes will make use of some new classes.</span></span> <span data-ttu-id="b3d85-115">모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 다음 코드를 사용 하 여 Cart 클래스 (Cart.cs)를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-115">Right-click the Models folder and add a Cart class (Cart.cs) with the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample1.cs)]

<span data-ttu-id="b3d85-116">이 클래스는 RecordId 속성에 대 한 [Key] 특성을 제외 하 고 지금까지 사용한 다른 다른 클래스와 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-116">This class is pretty similar to others we've used so far, with the exception of the [Key] attribute for the RecordId property.</span></span> <span data-ttu-id="b3d85-117">카트 항목에는 익명 쇼핑을 허용 하는 CartID 라는 문자열 식별자가 있지만 테이블에는 RecordId 라는 정수 기본 키가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-117">Our Cart items will have a string identifier named CartID to allow anonymous shopping, but the table includes an integer primary key named RecordId.</span></span> <span data-ttu-id="b3d85-118">Entity Framework 규칙에 따라 코드 우선에는 Cart 라는 테이블의 기본 키가 CartId 또는 ID가 될 것으로 예상 되지만, 원하는 경우 주석이 나 코드를 통해 쉽게 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-118">By convention, Entity Framework Code-First expects that the primary key for a table named Cart will be either CartId or ID, but we can easily override that via annotations or code if we want.</span></span> <span data-ttu-id="b3d85-119">이는 Entity Framework 코드에서 간단한 규칙을 사용 하는 방법에 대 한 예입니다. 첫 번째 규칙을 사용 하는 경우에는 사용 하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-119">This is an example of how we can use the simple conventions in Entity Framework Code-First when they suit us, but we're not constrained by them when they don't.</span></span>

<span data-ttu-id="b3d85-120">다음으로, 다음 코드를 사용 하 여 Order 클래스 (Order.cs)를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-120">Next, add an Order class (Order.cs) with the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample2.cs)]

<span data-ttu-id="b3d85-121">이 클래스는 주문의 요약 및 배달 정보를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-121">This class tracks summary and delivery information for an order.</span></span> <span data-ttu-id="b3d85-122">아직 만들지 않은 클래스에 종속 된 OrderDetails 탐색 속성이 있으므로 **아직 컴파일되지 않습니다**.</span><span class="sxs-lookup"><span data-stu-id="b3d85-122">**It won't compile yet**, because it has an OrderDetails navigation property which depends on a class we haven't created yet.</span></span> <span data-ttu-id="b3d85-123">이제 OrderDetail.cs 라는 클래스를 추가 하 고 다음 코드를 추가 하 여이를 수정 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-123">Let's fix that now by adding a class named OrderDetail.cs, adding the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample3.cs)]

<span data-ttu-id="b3d85-124">MusicStoreEntities 클래스에 대 한 마지막 업데이트 중 하나는 Dbsets&lt;음악가&gt;포함 하 여 새 모델 클래스를 노출 하는 DbSets를 포함 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-124">We'll make one last update to our MusicStoreEntities class to include DbSets which expose those new Model classes, also including a DbSet&lt;Artist&gt;.</span></span> <span data-ttu-id="b3d85-125">업데이트 된 MusicStoreEntities 클래스는 아래와 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-125">The updated MusicStoreEntities class appears as below.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample4.cs)]

## <a name="managing-the-shopping-cart-business-logic"></a><span data-ttu-id="b3d85-126">쇼핑 카트 비즈니스 논리 관리</span><span class="sxs-lookup"><span data-stu-id="b3d85-126">Managing the Shopping Cart business logic</span></span>

<span data-ttu-id="b3d85-127">다음으로 모델 폴더에 ShoppingCart 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-127">Next, we'll create the ShoppingCart class in the Models folder.</span></span> <span data-ttu-id="b3d85-128">ShoppingCart 모델은 Cart 테이블에 대 한 데이터 액세스를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-128">The ShoppingCart model handles data access to the Cart table.</span></span> <span data-ttu-id="b3d85-129">또한 쇼핑 카트에 항목을 추가 하 고 제거 하는 비즈니스 논리를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-129">Additionally, it will handle the business logic to for adding and removing items from the shopping cart.</span></span>

<span data-ttu-id="b3d85-130">사용자가 장바구니에 항목을 추가 하기 위해 계정에 등록 하도록 요구 하지 않기 때문에 사용자가 쇼핑 카트에 액세스할 때 GUID 또는 GUID (globally unique identifier)를 사용 하 여 사용자에 게 임시 고유 식별자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-130">Since we don't want to require users to sign up for an account just to add items to their shopping cart, we will assign users a temporary unique identifier (using a GUID, or globally unique identifier) when they access the shopping cart.</span></span> <span data-ttu-id="b3d85-131">ASP.NET Session 클래스를 사용 하 여이 ID를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-131">We'll store this ID using the ASP.NET Session class.</span></span>

<span data-ttu-id="b3d85-132">*참고: ASP.NET 세션은 사이트를 떠날 때 만료 되는 사용자 관련 정보를 저장 하는 편리한 장소입니다. 세션 상태를 잘못 사용 하는 것은 대규모 사이트에서 성능에 영향을 미칠 수 있지만, 데모용으로 사용 하는 것은 데모용입니다.*</span><span class="sxs-lookup"><span data-stu-id="b3d85-132">*Note: The ASP.NET Session is a convenient place to store user-specific information which will expire after they leave the site. While misuse of session state can have performance implications on larger sites, our light use will work well for demonstration purposes.*</span></span>

<span data-ttu-id="b3d85-133">ShoppingCart 클래스는 다음 메서드를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-133">The ShoppingCart class exposes the following methods:</span></span>

<span data-ttu-id="b3d85-134">기능 **카트** 는 앨범을 매개 변수로 사용 하 여 사용자의 카트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-134">**AddToCart** takes an Album as a parameter and adds it to the user's cart.</span></span> <span data-ttu-id="b3d85-135">카트 테이블은 각 앨범의 수량을 추적 하므로 필요한 경우 새 행을 만들기 위한 논리를 포함 하거나 사용자가 이미 앨범 복사본 하나를 주문한 경우에만 수량을 증가 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-135">Since the Cart table tracks quantity for each album, it includes logic to create a new row if needed or just increment the quantity if the user has already ordered one copy of the album.</span></span>

<span data-ttu-id="b3d85-136">**RemoveFromCart** 는 앨범 ID를 사용 하 여 사용자의 카트에 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-136">**RemoveFromCart** takes an Album ID and removes it from the user's cart.</span></span> <span data-ttu-id="b3d85-137">사용자가 카트에 앨범 복사본을 하나만 포함 하는 경우 행이 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-137">If the user only had one copy of the album in their cart, the row is removed.</span></span>

<span data-ttu-id="b3d85-138">**EmptyCart** 사용자의 쇼핑 카트에 있는 모든 항목을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-138">**EmptyCart** removes all items from a user's shopping cart.</span></span>

<span data-ttu-id="b3d85-139">**Getcartitems** 는 표시 또는 처리를 위해 cartitems 목록을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-139">**GetCartItems** retrieves a list of CartItems for display or processing.</span></span>

<span data-ttu-id="b3d85-140">**Getcount** 는 사용자가 쇼핑 카트에 있는 총 앨범 수를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-140">**GetCount** retrieves a the total number of albums a user has in their shopping cart.</span></span>

<span data-ttu-id="b3d85-141">**Gettotal** 은 카트에 있는 모든 항목의 총 비용을 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-141">**GetTotal** calculates the total cost of all items in the cart.</span></span>

<span data-ttu-id="b3d85-142">**Createorder** 는 체크 아웃 단계에서 쇼핑 카트를 주문으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-142">**CreateOrder** converts the shopping cart to an order during the checkout phase.</span></span>

<span data-ttu-id="b3d85-143">**Getcart** 는 컨트롤러에서 카트 개체를 얻을 수 있도록 하는 정적 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-143">**GetCart** is a static method which allows our controllers to obtain a cart object.</span></span> <span data-ttu-id="b3d85-144">**Getcartid** 메서드를 사용 하 여 사용자 세션에서 cartid 읽기를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-144">It uses the **GetCartId** method to handle reading the CartId from the user's session.</span></span> <span data-ttu-id="b3d85-145">GetCartId 메서드는 사용자의 세션에서 사용자의 CartId를 읽을 수 있도록 HttpContextBase를 요구 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-145">The GetCartId method requires the HttpContextBase so that it can read the user's CartId from user's session.</span></span>

<span data-ttu-id="b3d85-146">전체 **ShoppingCart 클래스**는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-146">Here's the complete **ShoppingCart class**:</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample5.cs)]

## <a name="viewmodels"></a><span data-ttu-id="b3d85-147">ViewModels</span><span class="sxs-lookup"><span data-stu-id="b3d85-147">ViewModels</span></span>

<span data-ttu-id="b3d85-148">쇼핑 카트 컨트롤러는 모델 개체에 명확 하 게 매핑되지 않는 일부 복잡 한 정보를 보기에 전달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-148">Our Shopping Cart Controller will need to communicate some complex information to its views which doesn't map cleanly to our Model objects.</span></span> <span data-ttu-id="b3d85-149">보기에 맞게 모델을 수정 하지 않으려고 합니다. 모델 클래스는 사용자 인터페이스가 아니라 도메인을 나타내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-149">We don't want to modify our Models to suit our views; Model classes should represent our domain, not the user interface.</span></span> <span data-ttu-id="b3d85-150">저장소 관리자 드롭다운 정보에서와 같이 ViewBag 클래스를 사용 하 여 보기에 정보를 전달 하는 것이 한 가지 해결 방법 이지만 ViewBag를 통해 많은 정보를 전달 하는 것은 관리 하기가 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-150">One solution would be to pass the information to our Views using the ViewBag class, as we did with the Store Manager dropdown information, but passing a lot of information via ViewBag gets hard to manage.</span></span>

<span data-ttu-id="b3d85-151">이에 대 한 해결 방법은 *ViewModel* 패턴을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-151">A solution to this is to use the *ViewModel* pattern.</span></span> <span data-ttu-id="b3d85-152">이 패턴을 사용 하는 경우 특정 뷰 시나리오에 최적화 된 강력한 형식의 클래스를 만들고, 뷰 템플릿에 필요한 동적 값/콘텐츠에 대 한 속성을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-152">When using this pattern we create strongly-typed classes that are optimized for our specific view scenarios, and which expose properties for the dynamic values/content needed by our view templates.</span></span> <span data-ttu-id="b3d85-153">그러면 컨트롤러 클래스는 이러한 뷰 최적화 클래스를 채우고 사용할 뷰 템플릿으로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-153">Our controller classes can then populate and pass these view-optimized classes to our view template to use.</span></span> <span data-ttu-id="b3d85-154">이렇게 하면 보기 템플릿 내에서 형식 안전성, 컴파일 시간 검사 및 편집기 IntelliSense를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-154">This enables type-safety, compile-time checking, and editor IntelliSense within view templates.</span></span>

<span data-ttu-id="b3d85-155">쇼핑 카트 컨트롤러에서 사용할 두 가지 뷰 모델을 만듭니다. ShoppingCartViewModel는 사용자의 쇼핑 카트 콘텐츠를 보유 하 고, ShoppingCartRemoveViewModel는 사용자가 항목을 제거할 때 확인 정보를 표시 하는 데 사용 됩니다. 카트를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-155">We'll create two View Models for use in our Shopping Cart controller: the ShoppingCartViewModel will hold the contents of the user's shopping cart, and the ShoppingCartRemoveViewModel will be used to display confirmation information when a user removes something from their cart.</span></span>

<span data-ttu-id="b3d85-156">구성 된 상태를 유지 하기 위해 프로젝트의 루트에 새 ViewModels 폴더를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-156">Let's create a new ViewModels folder in the root of our project to keep things organized.</span></span> <span data-ttu-id="b3d85-157">프로젝트를 마우스 오른쪽 단추로 클릭 하 고 추가/새 폴더를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-157">Right-click the project, select Add / New Folder.</span></span>

![](mvc-music-store-part-8/_static/image1.jpg)

<span data-ttu-id="b3d85-158">폴더 이름을 ViewModels으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-158">Name the folder ViewModels.</span></span>

![](mvc-music-store-part-8/_static/image1.png)

<span data-ttu-id="b3d85-159">다음으로 ViewModels 폴더에 ShoppingCartViewModel 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-159">Next, add the ShoppingCartViewModel class in the ViewModels folder.</span></span> <span data-ttu-id="b3d85-160">여기에는 카트 항목의 목록 및 카트에 있는 모든 항목의 총 가격을 포함 하는 10 진수 값 이라는 두 가지 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-160">It has two properties: a list of Cart items, and a decimal value to hold the total price for all items in the cart.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample6.cs)]

<span data-ttu-id="b3d85-161">이제 다음 네 가지 속성을 사용 하 여 ShoppingCartRemoveViewModel를 ViewModels 폴더에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-161">Now add the ShoppingCartRemoveViewModel to the ViewModels folder, with the following four properties.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample7.cs)]

## <a name="the-shopping-cart-controller"></a><span data-ttu-id="b3d85-162">쇼핑 카트 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="b3d85-162">The Shopping Cart Controller</span></span>

<span data-ttu-id="b3d85-163">쇼핑 카트 컨트롤러에는 카트에 항목 추가, 카트에 항목 제거, 카트에 있는 항목 보기의 세 가지 주요 목적이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-163">The Shopping Cart controller has three main purposes: adding items to a cart, removing items from the cart, and viewing items in the cart.</span></span> <span data-ttu-id="b3d85-164">ShoppingCartViewModel, ShoppingCartRemoveViewModel 및 ShoppingCart 라는 세 개의 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-164">It will make use of the three classes we just created: ShoppingCartViewModel, ShoppingCartRemoveViewModel, and ShoppingCart.</span></span> <span data-ttu-id="b3d85-165">StoreController 및 StoreManagerController와 마찬가지로 MusicStoreEntities의 인스턴스를 포함 하는 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-165">As in the StoreController and StoreManagerController, we'll add a field to hold an instance of MusicStoreEntities.</span></span>

<span data-ttu-id="b3d85-166">빈 컨트롤러 템플릿을 사용 하 여 프로젝트에 새 쇼핑 카트 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-166">Add a new Shopping Cart controller to the project using the Empty controller template.</span></span>

![](mvc-music-store-part-8/_static/image2.png)

<span data-ttu-id="b3d85-167">전체 ShoppingCart 컨트롤러는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-167">Here's the complete ShoppingCart Controller.</span></span> <span data-ttu-id="b3d85-168">인덱스 및 컨트롤러 추가 작업은 매우 익숙할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-168">The Index and Add Controller actions should look very familiar.</span></span> <span data-ttu-id="b3d85-169">제거 및 Carttsummary 컨트롤러 작업은 다음 섹션에서 설명 하는 두 가지 특수 한 경우를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-169">The Remove and CartSummary controller actions handle two special cases, which we'll discuss in the following section.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample8.cs)]

## <a name="ajax-updates-with-jquery"></a><span data-ttu-id="b3d85-170">JQuery를 사용 하 여 Ajax 업데이트</span><span class="sxs-lookup"><span data-stu-id="b3d85-170">Ajax Updates with jQuery</span></span>

<span data-ttu-id="b3d85-171">다음으로 ShoppingCartViewModel에 강력한 형식의 쇼핑 카트 인덱스 페이지를 만들고 이전과 동일한 방법으로 목록 뷰 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-171">We'll next create a Shopping Cart Index page that is strongly typed to the ShoppingCartViewModel and uses the List View template using the same method as before.</span></span>

![](mvc-music-store-part-8/_static/image3.png)

<span data-ttu-id="b3d85-172">그러나이 경우에는 html.actionlink를 사용 하 여 카트에 항목을 제거 하는 대신 jQuery를 사용 하 여이 보기의 모든 링크에 대 한 click 이벤트를 "연결" 하 여 HTML 클래스 RemoveLink를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-172">However, instead of using an Html.ActionLink to remove items from the cart, we'll use jQuery to "wire up" the click event for all links in this view which have the HTML class RemoveLink.</span></span> <span data-ttu-id="b3d85-173">이 click 이벤트 처리기는 폼을 게시 하는 대신 RemoveFromCart controller 동작에 대 한 AJAX 콜백을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-173">Rather than posting the form, this click event handler will just make an AJAX callback to our RemoveFromCart controller action.</span></span> <span data-ttu-id="b3d85-174">RemoveFromCart는 JSON 직렬화 된 결과를 반환 합니다. 그러면 jQuery 콜백은 jQuery를 사용 하 여 페이지에 대 한 4 개의 빠른 업데이트를 구문 분석 하 고 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-174">The RemoveFromCart returns a JSON serialized result, which our jQuery callback then parses and performs four quick updates to the page using jQuery:</span></span>

- 1. <span data-ttu-id="b3d85-175">삭제 된 앨범을 목록에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-175">Removes the deleted album from the list</span></span>
- 2. <span data-ttu-id="b3d85-176">헤더의 카트 수를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-176">Updates the cart count in the header</span></span>
- 3. <span data-ttu-id="b3d85-177">사용자에 게 업데이트 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-177">Displays an update message to the user</span></span>
- 4. <span data-ttu-id="b3d85-178">카트 총 가격을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-178">Updates the cart total price</span></span>

<span data-ttu-id="b3d85-179">제거 시나리오는 인덱스 뷰 내에서 Ajax 콜백에 의해 처리 되므로 RemoveFromCart 작업에 대 한 추가 뷰는 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-179">Since the remove scenario is being handled by an Ajax callback within the Index view, we don't need an additional view for RemoveFromCart action.</span></span> <span data-ttu-id="b3d85-180">/ShoppingCart/Index 뷰에 대 한 전체 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-180">Here is the complete code for the /ShoppingCart/Index view:</span></span>

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample9.cshtml)]

<span data-ttu-id="b3d85-181">이를 테스트 하기 위해 쇼핑 카트에 항목을 추가할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-181">In order to test this out, we need to be able to add items to our shopping cart.</span></span> <span data-ttu-id="b3d85-182">"장바구니에 추가" 단추를 포함 하도록 **매장 세부 정보** 보기를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-182">We'll update our **Store Details** view to include an "Add to cart" button.</span></span> <span data-ttu-id="b3d85-183">여기서는이 보기를 마지막으로 업데이트 한 이후 추가 된 앨범 추가 정보 (장르, 음악가, 가격 및 앨범 아트)를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-183">While we're at it, we can include some of the Album additional information which we've added since we last updated this view: Genre, Artist, Price, and Album Art.</span></span> <span data-ttu-id="b3d85-184">업데이트 된 저장소 세부 정보 보기 코드는 아래와 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-184">The updated Store Details view code appears as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample10.cshtml)]

<span data-ttu-id="b3d85-185">이제 스토어를 클릭 하 고 쇼핑 카트에 앨범 추가 및 제거를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-185">Now we can click through the store and test adding and removing Albums to and from our shopping cart.</span></span> <span data-ttu-id="b3d85-186">응용 프로그램을 실행 하 고 저장소 인덱스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-186">Run the application and browse to the Store Index.</span></span>

![](mvc-music-store-part-8/_static/image4.png)

<span data-ttu-id="b3d85-187">다음으로, 장르를 클릭 하 여 앨범 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-187">Next, click on a Genre to view a list of albums.</span></span>

![](mvc-music-store-part-8/_static/image5.png)

<span data-ttu-id="b3d85-188">이제 앨범 제목을 클릭 하면 "장바구니에 추가" 단추를 포함 하 여 업데이트 된 앨범 세부 정보 보기가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-188">Clicking on an Album title now shows our updated Album Details view, including the "Add to cart" button.</span></span>

![](mvc-music-store-part-8/_static/image6.png)

<span data-ttu-id="b3d85-189">"카트에 추가" 단추를 클릭 하면 장바구니 요약 목록이 포함 된 쇼핑 카트 인덱스 보기가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-189">Clicking the "Add to cart" button shows our Shopping Cart Index view with the shopping cart summary list.</span></span>

![](mvc-music-store-part-8/_static/image7.png)

<span data-ttu-id="b3d85-190">쇼핑 카트를 로드 한 후 카트에서 제거 링크를 클릭 하 여 쇼핑 카트에 Ajax 업데이트를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-190">After loading up your shopping cart, you can click on the Remove from cart link to see the Ajax update to your shopping cart.</span></span>

![](mvc-music-store-part-8/_static/image8.png)

<span data-ttu-id="b3d85-191">등록 되지 않은 사용자가 카트에 항목을 추가할 수 있도록 하는 작업 중인 장바구니를 구축 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-191">We've built out a working shopping cart which allows unregistered users to add items to their cart.</span></span> <span data-ttu-id="b3d85-192">다음 섹션에서는 체크 아웃 프로세스를 등록 하 고 완료할 수 있도록 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d85-192">In the following section, we'll allow them to register and complete the checkout process.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b3d85-193">[이전](mvc-music-store-part-7.md)
> [다음](mvc-music-store-part-9.md)</span><span class="sxs-lookup"><span data-stu-id="b3d85-193">[Previous](mvc-music-store-part-7.md)
[Next](mvc-music-store-part-9.md)</span></span>
