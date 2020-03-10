---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
title: '9 부: 등록 및 체크 아웃 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 9 부에서는 등록 및 체크 아웃을 다룹니다.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: d65c5c2b-a039-463f-ad29-25cf9fb7a1ba
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
msc.type: authoredcontent
ms.openlocfilehash: 040bc0ccef889fb9a7c3d9b5ce88c75b7b754248
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450899"
---
# <a name="part-9-registration-and-checkout"></a><span data-ttu-id="84cd7-104">9 부: 등록 및 체크 아웃</span><span class="sxs-lookup"><span data-stu-id="84cd7-104">Part 9: Registration and Checkout</span></span>

<span data-ttu-id="84cd7-105">받은 사람 ( [Jon Galloway](https://github.com/jongalloway) )</span><span class="sxs-lookup"><span data-stu-id="84cd7-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="84cd7-106">MVC Music Store는 웹 개발용 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 소개 하 고 설명 하는 자습서 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="84cd7-107">MVC Music Store는 온라인으로 음악 앨범을 판매 하 고 기본적인 사이트 관리, 사용자 로그인 및 쇼핑 카트 기능을 구현 하는 간단한 샘플 저장소 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="84cd7-108">이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="84cd7-109">9 부에서는 등록 및 체크 아웃을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-109">Part 9 covers Registration and Checkout.</span></span>

<span data-ttu-id="84cd7-110">이 섹션에서는 쇼핑객의 주소 및 지불 정보를 수집 하는 CheckoutController를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-110">In this section, we will be creating a CheckoutController which will collect the shopper's address and payment information.</span></span> <span data-ttu-id="84cd7-111">사용자는 체크 아웃 하기 전에 사이트에 등록 해야 하므로이 컨트롤러는 권한 부여가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-111">We will require users to register with our site prior to checking out, so this controller will require authorization.</span></span>

<span data-ttu-id="84cd7-112">사용자는 "체크 아웃" 단추를 클릭 하 여 쇼핑 카트에서 체크 아웃 프로세스로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-112">Users will navigate to the checkout process from their shopping cart by clicking the "Checkout" button.</span></span>

![](mvc-music-store-part-9/_static/image1.jpg)

<span data-ttu-id="84cd7-113">사용자가 로그인 되어 있지 않으면 사용자에 게 로그인 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-113">If the user is not logged in, they will be prompted to.</span></span>

![](mvc-music-store-part-9/_static/image1.png)

<span data-ttu-id="84cd7-114">로그인에 성공 하면 사용자에 게 주소 및 지불 보기가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-114">Upon successful login, the user is then shown the Address and Payment view.</span></span>

![](mvc-music-store-part-9/_static/image2.png)

<span data-ttu-id="84cd7-115">양식을 채우고 주문을 제출 하면 주문 확인 화면이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-115">Once they have filled the form and submitted the order, they will be shown the order confirmation screen.</span></span>

![](mvc-music-store-part-9/_static/image3.png)

<span data-ttu-id="84cd7-116">존재 하지 않는 순서 또는 사용자에 게 속하지 않는 순서를 보려는 경우 오류 보기가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-116">Attempting to view either a non-existent order or an order that doesn't belong to you will show the Error view.</span></span>

![](mvc-music-store-part-9/_static/image4.png)

## <a name="migrating-the-shopping-cart"></a><span data-ttu-id="84cd7-117">쇼핑 카트 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="84cd7-117">Migrating the Shopping Cart</span></span>

<span data-ttu-id="84cd7-118">쇼핑 프로세스는 익명 이지만 사용자가 체크 아웃 단추를 클릭 하면 등록 하 고 로그인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-118">While the shopping process is anonymous, when the user clicks on the Checkout button, they will be required to register and login.</span></span> <span data-ttu-id="84cd7-119">사용자는 방문 간에 쇼핑 카트 정보를 유지 관리 하므로 등록 또는 로그인이 완료 되 면 장바구니 정보를 사용자와 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-119">Users will expect that we will maintain their shopping cart information between visits, so we will need to associate the shopping cart information with a user when they complete registration or login.</span></span>

<span data-ttu-id="84cd7-120">ShoppingCart 클래스에는 현재 카트에 있는 모든 항목을 사용자 이름과 연결 하는 메서드가 이미 있기 때문에 실제로는이 작업을 수행 하는 것이 매우 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-120">This is actually very simple to do, as our ShoppingCart class already has a method which will associate all the items in the current cart with a username.</span></span> <span data-ttu-id="84cd7-121">사용자가 등록 또는 로그인을 완료 하는 경우에만이 메서드를 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-121">We will just need to call this method when a user completes registration or login.</span></span>

<span data-ttu-id="84cd7-122">멤버 자격 및 권한 부여를 설정할 때 추가한 **Accountcontroller** 클래스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-122">Open the **AccountController** class that we added when we were setting up Membership and Authorization.</span></span> <span data-ttu-id="84cd7-123">MvcMusicStore를 참조 하는 using 문을 추가 하 고 다음 MigrateShoppingCart 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-123">Add a using statement referencing MvcMusicStore.Models, then add the following MigrateShoppingCart method:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample1.cs)]

<span data-ttu-id="84cd7-124">다음으로, 아래와 같이 사용자의 유효성을 검사 한 후 MigrateShoppingCart를 호출 하도록 LogOn post 작업을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-124">Next, modify the LogOn post action to call MigrateShoppingCart after the user has been validated, as shown below:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample2.cs)]

<span data-ttu-id="84cd7-125">사용자 계정이 성공적으로 생성 된 후 즉시 등록 게시 작업을 동일 하 게 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-125">Make the same change to the Register post action, immediately after the user account is successfully created:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample3.cs)]

<span data-ttu-id="84cd7-126">이제 등록 또는 로그인에 성공 하면 익명 쇼핑 카트는 사용자 계정으로 자동으로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-126">That's it - now an anonymous shopping cart will be automatically transferred to a user account upon successful registration or login.</span></span>

## <a name="creating-the-checkoutcontroller"></a><span data-ttu-id="84cd7-127">CheckoutController 만들기</span><span class="sxs-lookup"><span data-stu-id="84cd7-127">Creating the CheckoutController</span></span>

<span data-ttu-id="84cd7-128">Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 빈 컨트롤러 템플릿을 사용 하 여 CheckoutController 라는 프로젝트에 새 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-128">Right-click on the Controllers folder and add a new Controller to the project named CheckoutController using the Empty controller template.</span></span>

![](mvc-music-store-part-9/_static/image5.png)

<span data-ttu-id="84cd7-129">먼저, 사용자가를 체크 인하기 전에 등록 하도록 요구 하도록 컨트롤러 클래스 선언 위에 권한 부여 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-129">First, add the Authorize attribute above the Controller class declaration to require users to register before checkout:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample4.cs)]

<span data-ttu-id="84cd7-130">*참고:이는 이전에 StoreManagerController에 대 한 변경 내용과 유사 하지만,이 경우에는 사용자가 관리자 역할에 있어야 합니다. 체크 아웃 컨트롤러에서는 사용자에 게 로그인이 필요 하지만 관리자가 될 필요는 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="84cd7-130">*Note: This is similar to the change we previously made to the StoreManagerController, but in that case the Authorize attribute required that the user be in an Administrator role. In the Checkout Controller, we're requiring the user be logged in but aren't requiring that they be administrators.*</span></span>

<span data-ttu-id="84cd7-131">간단히 하기 위해이 자습서에서는 지불 정보를 처리 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-131">For the sake of simplicity, we won't be dealing with payment information in this tutorial.</span></span> <span data-ttu-id="84cd7-132">대신, 사용자가 판촉 코드를 사용 하 여 체크 아웃할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-132">Instead, we are allowing users to check out using a promotional code.</span></span> <span data-ttu-id="84cd7-133">PromoCode 라는 상수를 사용 하 여이 프로 모션 코드를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-133">We will store this promotional code using a constant named PromoCode.</span></span>

<span data-ttu-id="84cd7-134">StoreController와 마찬가지로 storeDB 라는 MusicStoreEntities 클래스의 인스턴스를 포함 하는 필드를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-134">As in the StoreController, we'll declare a field to hold an instance of the MusicStoreEntities class, named storeDB.</span></span> <span data-ttu-id="84cd7-135">MusicStoreEntities 클래스를 사용 하기 위해 MvcMusicStore 네임 스페이스에 대 한 using 문을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-135">In order to make use of the MusicStoreEntities class, we will need to add a using statement for the MvcMusicStore.Models namespace.</span></span> <span data-ttu-id="84cd7-136">체크 아웃 컨트롤러의 위쪽이 아래에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-136">The top of our Checkout controller appears below.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample5.cs)]

<span data-ttu-id="84cd7-137">CheckoutController에는 다음과 같은 컨트롤러 작업이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-137">The CheckoutController will have the following controller actions:</span></span>

<span data-ttu-id="84cd7-138">**AddressAndPayment (GET 메서드)** 는 사용자가 정보를 입력할 수 있는 폼을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-138">**AddressAndPayment (GET method)** will display a form to allow the user to enter their information.</span></span>

<span data-ttu-id="84cd7-139">**AddressAndPayment (POST 메서드)** 는 입력의 유효성을 검사 하 고 주문을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-139">**AddressAndPayment (POST method)** will validate the input and process the order.</span></span>

<span data-ttu-id="84cd7-140">사용자가 체크 아웃 프로세스를 성공적으로 완료 한 후 **완료** 가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-140">**Complete** will be shown after a user has successfully finished the checkout process.</span></span> <span data-ttu-id="84cd7-141">이 보기에는 확인으로 사용자의 주문 번호가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-141">This view will include the user's order number, as confirmation.</span></span>

<span data-ttu-id="84cd7-142">먼저 AddressAndPayment에 대해 컨트롤러를 만들 때 생성 된 인덱스 컨트롤러 작업의 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-142">First, let's rename the Index controller action (which was generated when we created the controller) to AddressAndPayment.</span></span> <span data-ttu-id="84cd7-143">이 컨트롤러 작업은 단순히 체크 아웃 폼을 표시 하므로 모델 정보가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-143">This controller action just displays the checkout form, so it doesn't require any model information.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample6.cs)]

<span data-ttu-id="84cd7-144">AddressAndPayment POST 메서드는 StoreManagerController에서 사용한 것과 동일한 패턴을 따릅니다. 즉, 폼 제출을 수락 하 고 주문을 완료 하 고 실패 하면 양식을 다시 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-144">Our AddressAndPayment POST method will follow the same pattern we used in the StoreManagerController: it will try to accept the form submission and complete the order, and will re-display the form if it fails.</span></span>

<span data-ttu-id="84cd7-145">양식 입력이 주문에 대 한 유효성 검사 요구 사항을 충족 하는지 확인 한 후에는 PromoCode 양식 값을 직접 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-145">After validating the form input meets our validation requirements for an Order, we will check the PromoCode form value directly.</span></span> <span data-ttu-id="84cd7-146">모든 것이 올바르면 주문에 업데이트 된 정보를 저장 하 고, 주문 프로세스를 완료 하도록 ShoppingCart 개체에 지시 하 고, 전체 작업으로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-146">Assuming everything is correct, we will save the updated information with the order, tell the ShoppingCart object to complete the order process, and redirect to the Complete action.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample7.cs)]

<span data-ttu-id="84cd7-147">체크 아웃 프로세스가 성공적으로 완료 되 면 사용자가 전체 컨트롤러 작업으로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-147">Upon successful completion of the checkout process, users will be redirected to the Complete controller action.</span></span> <span data-ttu-id="84cd7-148">이 작업은 주문 번호를 확인으로 표시 하기 전에 주문이 로그인 한 사용자에 게 실제로 속하는지 확인 하는 간단한 검사를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-148">This action will perform a simple check to validate that the order does indeed belong to the logged-in user before showing the order number as a confirmation.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample8.cs)]

<span data-ttu-id="84cd7-149">*참고: 프로젝트를 시작 했을 때/Views/Shared 폴더에 오류 보기가 자동으로 생성 되었습니다.*</span><span class="sxs-lookup"><span data-stu-id="84cd7-149">*Note: The Error view was automatically created for us in the /Views/Shared folder when we began the project.*</span></span>

<span data-ttu-id="84cd7-150">전체 CheckoutController 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-150">The complete CheckoutController code is as follows:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample9.cs)]

## <a name="adding-the-addressandpayment-view"></a><span data-ttu-id="84cd7-151">AddressAndPayment 뷰 추가</span><span class="sxs-lookup"><span data-stu-id="84cd7-151">Adding the AddressAndPayment view</span></span>

<span data-ttu-id="84cd7-152">이제 AddressAndPayment view를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-152">Now, let's create the AddressAndPayment view.</span></span> <span data-ttu-id="84cd7-153">AddressAndPayment controller 작업 중 하나를 마우스 오른쪽 단추로 클릭 하 고 아래와 같이 강력한 형식의 AddressAndPayment 라는 뷰를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-153">Right-click on one of the AddressAndPayment controller actions and add a view named AddressAndPayment which is strongly typed as an Order and uses the Edit template, as shown below.</span></span>

![](mvc-music-store-part-9/_static/image6.png)

<span data-ttu-id="84cd7-154">이 보기는 StoreManagerEdit 뷰를 작성 하는 동안 확인 된 기술 중 두 가지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-154">This view will make use of two of the techniques we looked at while building the StoreManagerEdit view:</span></span>

- <span data-ttu-id="84cd7-155">Html. EditorForModel ()을 사용 하 여 주문 모델에 대 한 양식 필드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-155">We will use Html.EditorForModel() to display form fields for the Order model</span></span>
- <span data-ttu-id="84cd7-156">유효성 검사 특성을 사용 하 여 Order 클래스를 사용 하는 유효성 검사 규칙을 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-156">We will leverage validation rules using an Order class with validation attributes</span></span>

<span data-ttu-id="84cd7-157">먼저 Html. EditorForModel ()을 사용 하 고 프로 모션 코드에 대 한 추가 텍스트 상자를 사용 하도록 양식 코드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-157">We'll start by updating the form code to use Html.EditorForModel(), followed by an additional textbox for the Promo Code.</span></span> <span data-ttu-id="84cd7-158">AddressAndPayment 뷰에 대 한 전체 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-158">The complete code for the AddressAndPayment view is shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample10.cshtml)]

## <a name="defining-validation-rules-for-the-order"></a><span data-ttu-id="84cd7-159">주문에 대 한 유효성 검사 규칙 정의</span><span class="sxs-lookup"><span data-stu-id="84cd7-159">Defining validation rules for the Order</span></span>

<span data-ttu-id="84cd7-160">이제 뷰가 설정 되었으므로 이전에 앨범 모델에 대해 했던 것 처럼 주문 모델에 대 한 유효성 검사 규칙을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-160">Now that our view is set up, we will set up the validation rules for our Order model as we did previously for the Album model.</span></span> <span data-ttu-id="84cd7-161">모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 Order 라는 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-161">Right-click on the Models folder and add a class named Order.</span></span> <span data-ttu-id="84cd7-162">이전에 앨범에 사용한 유효성 검사 특성 외에도 정규식을 사용 하 여 사용자 전자 메일 주소의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-162">In addition to the validation attributes we used previously for the Album, we will also be using a Regular Expression to validate the user's email address.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample11.cs)]

<span data-ttu-id="84cd7-163">누락 되거나 잘못 된 정보를 사용 하 여 양식을 전송 하려고 하면 클라이언트 쪽 유효성 검사를 사용 하 여 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-163">Attempting to submit the form with missing or invalid information will now show error message using client-side validation.</span></span>

![](mvc-music-store-part-9/_static/image7.png)

<span data-ttu-id="84cd7-164">확인 프로세스에 대 한 대부분의 하드 작업을 완료 했습니다. 몇 가지 경우에는 거의 필요 하지 않으며 종료 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-164">Okay, we've done most of the hard work for the checkout process; we just have a few odds and ends to finish.</span></span> <span data-ttu-id="84cd7-165">두 개의 간단한 뷰를 추가 해야 하며 로그인 프로세스 중에 카트 정보를 전달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-165">We need to add two simple views, and we need to take care of the handoff of the cart information during the login process.</span></span>

## <a name="adding-the-checkout-complete-view"></a><span data-ttu-id="84cd7-166">체크 아웃 완료 보기 추가</span><span class="sxs-lookup"><span data-stu-id="84cd7-166">Adding the Checkout Complete view</span></span>

<span data-ttu-id="84cd7-167">주문 ID를 표시 하기만 하면 체크 아웃 완료 보기가 매우 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-167">The Checkout Complete view is pretty simple, as it just needs to display the Order ID.</span></span> <span data-ttu-id="84cd7-168">전체 컨트롤러 작업을 마우스 오른쪽 단추로 클릭 하 고 int로 강력 하 게 형식화 된 Complete 라는 뷰를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-168">Right-click on the Complete controller action and add a view named Complete which is strongly typed as an int.</span></span>

![](mvc-music-store-part-9/_static/image8.png)

<span data-ttu-id="84cd7-169">이제 아래와 같이 주문 ID를 표시 하도록 뷰 코드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-169">Now we will update the view code to display the Order ID, as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample12.cshtml)]

## <a name="updating-the-error-view"></a><span data-ttu-id="84cd7-170">오류 보기 업데이트</span><span class="sxs-lookup"><span data-stu-id="84cd7-170">Updating The Error view</span></span>

<span data-ttu-id="84cd7-171">기본 템플릿에는 사이트의 다른 곳에서 다시 사용할 수 있도록 공유 보기 폴더의 오류 보기가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-171">The default template includes an Error view in the Shared views folder so that it can be re-used elsewhere in the site.</span></span> <span data-ttu-id="84cd7-172">이 오류 보기에는 매우 간단한 오류가 포함 되어 있으며 사이트 레이아웃을 사용 하지 않으므로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-172">This Error view contains a very simple error and doesn't use our site Layout, so we'll update it.</span></span>

<span data-ttu-id="84cd7-173">일반 오류 페이지 이므로 콘텐츠는 매우 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-173">Since this is a generic error page, the content is very simple.</span></span> <span data-ttu-id="84cd7-174">사용자가 작업을 다시 시도 하려는 경우 기록에서 이전 페이지로 이동 하는 메시지와 링크를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="84cd7-174">We'll include a message and a link to navigate to the previous page in history if the user wants to re-try their action.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample13.cshtml)]

> [!div class="step-by-step"]
> <span data-ttu-id="84cd7-175">[이전](mvc-music-store-part-8.md)
> [다음](mvc-music-store-part-10.md)</span><span class="sxs-lookup"><span data-stu-id="84cd7-175">[Previous](mvc-music-store-part-8.md)
[Next](mvc-music-store-part-10.md)</span></span>
