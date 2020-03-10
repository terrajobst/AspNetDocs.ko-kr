---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
title: '5 부: 비즈니스 논리 | Microsoft Docs'
author: JoeStagner
description: 이 자습서 시리즈에서는 Tailspin Spyworks 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 5 부에서는 비즈니스 논리를 추가 합니다.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: eaef475a-ca91-47ea-a4a7-d074005ed80c
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
msc.type: authoredcontent
ms.openlocfilehash: c60eece9223c47304786d7b0d0ca4b11ac0572e9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78511547"
---
# <a name="part-5-business-logic"></a><span data-ttu-id="24c1e-104">5 부: 비즈니스 논리</span><span class="sxs-lookup"><span data-stu-id="24c1e-104">Part 5: Business Logic</span></span>

<span data-ttu-id="24c1e-105">만든 사람 [Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="24c1e-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="24c1e-106">Tailspin Spyworks는 .NET 플랫폼을 위한 강력 하 고 확장 가능한 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="24c1e-107">ASP.NET 4의 새로운 기능을 사용 하 여 쇼핑, 구매 및 관리를 포함 한 온라인 상점을 구축 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="24c1e-108">이 자습서 시리즈에서는 Tailspin Spyworks 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="24c1e-109">5 부에서는 비즈니스 논리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-109">Part 5 adds some business logic.</span></span>

## <a id="_Toc260221671"></a><span data-ttu-id="24c1e-110">일부 비즈니스 논리 추가</span><span class="sxs-lookup"><span data-stu-id="24c1e-110">Adding Some Business Logic</span></span>

<span data-ttu-id="24c1e-111">누군가가 웹 사이트를 방문할 때마다 쇼핑 환경을 사용할 수 있도록 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-111">We want our shopping experience to be available whenever someone visits our web site.</span></span> <span data-ttu-id="24c1e-112">방문자는 등록 되거나 로그인 되지 않은 경우에도 쇼핑 카트에 항목을 찾아보고 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-112">Visitors will be able to browse and add items to the shopping cart even if they are not registered or logged in.</span></span> <span data-ttu-id="24c1e-113">체크 아웃할 준비가 되 면 인증할 수 있는 옵션이 제공 되 고 아직 구성원이 아닌 경우에는 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-113">When they are ready to check out they will be given the option to authenticate and if they are not yet members they will be able to create an account.</span></span>

<span data-ttu-id="24c1e-114">즉, 쇼핑 카트를 익명 상태에서 "등록 된 사용자" 상태로 변환 하는 논리를 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-114">This means that we will need to implement the logic to convert the shopping cart from an anonymous state to a "Registered User" state.</span></span>

<span data-ttu-id="24c1e-115">"클래스" 라는 디렉터리를 만든 다음 폴더를 마우스 오른쪽 단추로 클릭 하 고 MyShoppingCart.cs 이라는 새 "클래스" 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-115">Let's create a directory named "Classes" then Right-Click on the folder and create a new "Class" file named MyShoppingCart.cs</span></span>

![](tailspin-spyworks-part-5/_static/image1.jpg)

![](tailspin-spyworks-part-5/_static/image1.png)

<span data-ttu-id="24c1e-116">앞에서 설명한 것 처럼 MyShoppingCart 페이지를 구현 하는 클래스를 확장 하 고를 사용 하 여이 작업을 수행 합니다. NET의 강력한 "Partial 클래스" 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-116">As previously mentioned we will be extending the class that implements the MyShoppingCart.aspx page and we will do this using .NET's powerful "Partial Class" construct.</span></span>

<span data-ttu-id="24c1e-117">MyShoppingCart.aspx.cf 파일에 대해 생성 된 호출은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-117">The generated call for our MyShoppingCart.aspx.cf file looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample1.cs)]

<span data-ttu-id="24c1e-118">"Partial" 키워드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-118">Note the use of the "partial" keyword.</span></span>

<span data-ttu-id="24c1e-119">방금 생성 한 클래스 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-119">The class file that we just generated looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample2.cs)]

<span data-ttu-id="24c1e-120">Partial 키워드를이 파일에 추가 하 여 구현을 병합 합니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-120">We will merge our implementations by adding the partial keyword to this file as well.</span></span>

<span data-ttu-id="24c1e-121">이제 새 클래스 파일이 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-121">Our new class file now looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample3.cs)]

<span data-ttu-id="24c1e-122">클래스에 추가 하는 첫 번째 메서드는 "AddItem" 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-122">The first method that we will add to our class is the "AddItem" method.</span></span> <span data-ttu-id="24c1e-123">사용자가 제품 목록 및 제품 세부 정보 페이지에서 "아트에 추가" 링크를 클릭할 때 최종적으로 호출 되는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-123">This is the method that will ultimately be called when the user clicks on the "Add to Art" links on the Product List and Product Details pages.</span></span>

<span data-ttu-id="24c1e-124">페이지 맨 위에 있는 using 문에 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-124">Append the following to the using statements at the top of the page.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample4.cs)]

<span data-ttu-id="24c1e-125">그런 다음이 메서드를 MyShoppingCart 클래스에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-125">And add this method to the MyShoppingCart class.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample5.cs)]

<span data-ttu-id="24c1e-126">LINQ to Entities 사용 하 여 항목이 이미 카트에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-126">We are using LINQ to Entities to see if the item is already in the cart.</span></span> <span data-ttu-id="24c1e-127">이 경우 항목의 주문 수량을 업데이트 합니다. 그렇지 않으면 선택한 항목에 대 한 새 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-127">If so, we update the order quantity of the item, otherwise we create a new entry for the selected item</span></span>

<span data-ttu-id="24c1e-128">이 메서드를 호출 하기 위해이 메서드를 클래스 뿐만 아니라 항목이 추가 된 후 현재 쇼핑 a = cart를 표시 하는 지 수 카트 .aspx 페이지를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-128">In order to call this method we will implement an AddToCart.aspx page that not only class this method but then displayed the current shopping a=cart after the item has been added.</span></span>

<span data-ttu-id="24c1e-129">솔루션 탐색기에서 솔루션 이름을 마우스 오른쪽 단추로 클릭 하 고 이전에 수행한 것 처럼 새 페이지와 새 페이지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-129">Right-Click on the solution name in the solution explorer and add and new page named AddToCart.aspx as we have done previously.</span></span>

<span data-ttu-id="24c1e-130">이 페이지를 사용 하 여 저렴 한 문제 등의 중간 결과를 표시할 수는 있지만 구현 시 페이지는 실제로 렌더링 되지 않고 "추가" 논리를 호출 하 고 리디렉션을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-130">While we could use this page to display interim results like low stock issues, etc, in our implementation, the page will not actually render, but rather call the "Add" logic and redirect.</span></span>

<span data-ttu-id="24c1e-131">이를 위해 페이지\_Load 이벤트에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-131">To accomplish this we'll add the following code to the Page\_Load event.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample6.cs)]

<span data-ttu-id="24c1e-132">QueryString 매개 변수에서 쇼핑 카트에 추가 하 고 클래스의 AddItem 메서드를 호출 하 여 제품을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-132">Note that we are retrieving the product to add to the shopping cart from a QueryString parameter and calling the AddItem method of our class.</span></span>

<span data-ttu-id="24c1e-133">오류가 발생 하지 않는다고 가정할 경우 다음을 완벽 하 게 구현 하는 SHoppingCart 페이지로 제어가 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-133">Assuming no errors are encountered control is passed to the SHoppingCart.aspx page which we will fully implement next.</span></span> <span data-ttu-id="24c1e-134">오류가 발생 해야 하는 경우 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-134">If there should be an error we throw an exception.</span></span>

<span data-ttu-id="24c1e-135">현재는 전역 오류 처리기를 아직 구현 하지 않았으므로이 예외는 응용 프로그램에서 처리 되지 않지만 곧 해결 될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-135">Currently we have not yet implemented a global error handler so this exception would go unhandled by our application but we will remedy this shortly.</span></span>

<span data-ttu-id="24c1e-136">또한 Debug. Fail () 문을 사용 합니다 (`using System.Diagnostics;)`을 통해 사용 가능</span><span class="sxs-lookup"><span data-stu-id="24c1e-136">Note also the use of the statement Debug.Fail() (available via `using System.Diagnostics;)`</span></span>

<span data-ttu-id="24c1e-137">응용 프로그램이 디버거 내에서 실행 되는 경우이 메서드는 지정 된 오류 메시지와 함께 응용 프로그램 상태에 대 한 정보가 포함 된 자세한 대화 상자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-137">Is the application is running inside the debugger, this method will display a detailed dialog with information about the applications state along with the error message that we specify.</span></span>

<span data-ttu-id="24c1e-138">프로덕션 환경에서 실행 하는 경우에는 Debug. Fail () 문이 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-138">When running in production the Debug.Fail() statement is ignored.</span></span>

<span data-ttu-id="24c1e-139">이 코드에서는 장바구니 클래스 이름 "GetShoppingCartId"의 메서드 호출을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-139">You will note in the code above a call to a method in our shopping cart class names "GetShoppingCartId".</span></span>

<span data-ttu-id="24c1e-140">다음과 같이 메서드를 구현 하는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-140">Add the code to implement the method as follows.</span></span>

<span data-ttu-id="24c1e-141">또한 업데이트 및 체크 아웃 단추와 "total" 카트를 표시할 수 있는 레이블만 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-141">Note that we've also added update and checkout buttons and a label where we can display the cart "total".</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample7.cs)]

<span data-ttu-id="24c1e-142">이제 쇼핑 카트에 항목을 추가할 수 있지만 제품을 추가한 후에 카트를 표시 하는 논리를 구현 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-142">We can now add items to our shopping cart but we have not implemented the logic to display the cart after a product has been added.</span></span>

<span data-ttu-id="24c1e-143">따라서 MyShoppingCart 페이지에서 다음과 같이 EntityDataSource 컨트롤과 GridVire 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-143">So, in the MyShoppingCart.aspx page we'll add an EntityDataSource control and a GridVire control as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample8.aspx)]

<span data-ttu-id="24c1e-144">카트 업데이트 단추를 두 번 클릭 하 고 태그의 선언에 지정 된 click 이벤트 처리기를 생성할 수 있도록 디자이너에서 폼을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-144">Call up the form in the designer so that you can double click on the Update Cart button and generate the click event handler that is specified in the declaration in the markup.</span></span>

<span data-ttu-id="24c1e-145">나중에 세부 정보를 구현 하지만,이 작업을 수행 하면 오류 없이 응용 프로그램을 빌드하고 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-145">We'll implement the details later but doing this will let us build and run our application without errors.</span></span>

<span data-ttu-id="24c1e-146">응용 프로그램을 실행 하 고 장바구니에 항목을 추가 하면이 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-146">When you run the application and add an item to the shopping cart you will see this.</span></span>

![](tailspin-spyworks-part-5/_static/image2.jpg)

<span data-ttu-id="24c1e-147">3 개의 사용자 지정 열을 구현 하 여 "기본" 그리드 표시에서 벗어난 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-147">Note that we have deviated from the "default" grid display by implementing three custom columns.</span></span>

<span data-ttu-id="24c1e-148">첫 번째는 수량에 대 한 편집 가능 "바인딩" 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-148">The first is an Editable, "Bound" field for the Quantity:</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample9.aspx)]

<span data-ttu-id="24c1e-149">다음은 줄 항목 합계를 표시 하는 "계산 된" 열입니다. 항목의 순위는 주문 수량입니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-149">The next is a "calculated" column that displays the line item total (the item cost times the quantity to be ordered):</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample10.aspx)]

<span data-ttu-id="24c1e-150">마지막으로 사용자가 쇼핑 차트에서 항목을 제거 해야 함을 나타내는 데 사용할 CheckBox 컨트롤이 포함 된 사용자 지정 열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-150">Lastly we have a custom column that contains a CheckBox control that the user will use to indicate that the item should be removed from the shopping chart.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample11.aspx)]

![](tailspin-spyworks-part-5/_static/image3.jpg)

<span data-ttu-id="24c1e-151">표시 된 것 처럼 주문 합계 행이 비어 있으므로 주문 합계를 계산 하는 논리를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-151">As you can see, the Order Total line is empty so let's add some logic to calculate the Order Total.</span></span>

<span data-ttu-id="24c1e-152">먼저 MyShoppingCart 클래스에 대 한 "GetTotal" 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-152">We'll first implement a "GetTotal" method to our MyShoppingCart Class.</span></span>

<span data-ttu-id="24c1e-153">MyShoppingCart.cs 파일에서 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-153">In the MyShoppingCart.cs file add the following code.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample12.cs)]

<span data-ttu-id="24c1e-154">그런 다음 페이지\_Load 이벤트 처리기에서 GetTotal 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-154">Then in the Page\_Load event handler we'll can call our GetTotal method.</span></span> <span data-ttu-id="24c1e-155">동시에 테스트를 추가 하 여 쇼핑 카트가 비어 있는지 확인 하 고, 표시 되는 경우 적절 하 게 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-155">At the same time we'll add a test to see if the shopping cart is empty and adjust the display accordingly if it is.</span></span>

<span data-ttu-id="24c1e-156">이제 장바구니를 비워 두면 다음을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-156">Now if the shopping cart is empty we get this:</span></span>

![](tailspin-spyworks-part-5/_static/image4.jpg)

<span data-ttu-id="24c1e-157">그렇지 않은 경우 합계가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-157">And if not, we see our total.</span></span>

![](tailspin-spyworks-part-5/_static/image5.jpg)

<span data-ttu-id="24c1e-158">그러나이 페이지는 아직 완료 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-158">However, this page is not yet complete.</span></span>

<span data-ttu-id="24c1e-159">제거 하도록 표시 된 항목을 제거 하 고 사용자가 표에서 일부를 변경 했을 때 새 수량 값을 확인 하 여 쇼핑 카트를 다시 계산 하는 추가 논리가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-159">We will need additional logic to recalculate the shopping cart by removing items marked for removal and by determining new quantity values as some may have been changed in the grid by the user.</span></span>

<span data-ttu-id="24c1e-160">MyShoppingCart.cs의 쇼핑 카트 클래스에 "RemoveItem" 메서드를 추가 하 여 사용자가 제거를 위해 항목을 표시 하는 경우를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-160">Lets add a "RemoveItem" method to our shopping cart class in MyShoppingCart.cs to handle the case when a user marks an item for removal.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample13.cs)]

<span data-ttu-id="24c1e-161">이제 사용자가 GridView에서 주문할 품질을 변경 하는 경우를 처리 하는 방법을 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-161">Now let's ad a method to handle the circumstance when a user simply changes the quality to be ordered in the GridView.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample14.cs)]

<span data-ttu-id="24c1e-162">기본 제거 및 업데이트 기능을 사용 하면 데이터베이스에서 쇼핑 카트를 실제로 업데이트 하는 논리를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-162">With the basic Remove and Update features in place we can implement the logic that actually updates the shopping cart in the database.</span></span> <span data-ttu-id="24c1e-163">(MyShoppingCart.cs)</span><span class="sxs-lookup"><span data-stu-id="24c1e-163">(In MyShoppingCart.cs)</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample15.cs)]

<span data-ttu-id="24c1e-164">이 메서드에는 두 개의 매개 변수가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-164">You'll note that this method expects two parameters.</span></span> <span data-ttu-id="24c1e-165">하나는 쇼핑 카트 Id이 고 다른 하나는 사용자 정의 유형의 개체 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-165">One is the shopping cart Id and the other is an array of objects of user defined type.</span></span>

<span data-ttu-id="24c1e-166">따라서 사용자 인터페이스 세부 사항에 대 한 논리 종속성을 최소화 하기 위해 GridView 컨트롤에 직접 액세스 해야 하는 메서드 없이 코드에 쇼핑 카트 항목을 전달 하는 데 사용할 수 있는 데이터 구조를 정의 했습니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-166">So as to minimize the dependency of our logic on user interface specifics, we've defined a data structure that we can use to pass the shopping cart items to our code without our method needing to directly access the GridView control.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample16.cs)]

<span data-ttu-id="24c1e-167">MyShoppingCart.aspx.cs 파일에서 다음과 같이 업데이트 단추 클릭 이벤트 처리기에서이 구조를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-167">In our MyShoppingCart.aspx.cs file we can use this structure in our Update Button Click Event handler as follows.</span></span> <span data-ttu-id="24c1e-168">카트를 업데이트 하는 것 외에도 카트 합계도 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-168">Note that in addition to updating the cart we will update the cart total as well.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample17.cs)]

<span data-ttu-id="24c1e-169">특히 다음 코드 줄을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-169">Note with particular interest this line of code:</span></span>

[!code-javascript[Main](tailspin-spyworks-part-5/samples/sample18.js)]

<span data-ttu-id="24c1e-170">GetValues ()은 MyShoppingCart.aspx.cs에서 다음과 같이 구현할 특수 도우미 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-170">GetValues() is a special helper function that we will implement in MyShoppingCart.aspx.cs as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample19.cs)]

<span data-ttu-id="24c1e-171">이를 통해 GridView 컨트롤에서 바인딩된 요소의 값에 쉽게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-171">This provides a clean way to access the values of the bound elements in our GridView control.</span></span> <span data-ttu-id="24c1e-172">"항목 제거" CheckBox 컨트롤이 바인딩되지 않았으므로 FindControl () 메서드를 통해 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-172">Since our "Remove Item" CheckBox Control is not bound we'll access it via the FindControl() method.</span></span>

<span data-ttu-id="24c1e-173">프로젝트 개발의이 단계에서는 체크 아웃 프로세스를 구현할 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-173">At this stage in your project's development we are getting ready to implement the checkout process.</span></span>

<span data-ttu-id="24c1e-174">이렇게 하기 전에 Visual Studio를 사용 하 여 멤버 자격 데이터베이스를 생성 하 고 멤버 자격 리포지토리에 사용자를 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="24c1e-174">Before doing so let's use Visual Studio to generate the membership database and add a user to the membership repository.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="24c1e-175">[이전](tailspin-spyworks-part-4.md)
> [다음](tailspin-spyworks-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="24c1e-175">[Previous](tailspin-spyworks-part-4.md)
[Next](tailspin-spyworks-part-6.md)</span></span>
