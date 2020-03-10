---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
title: '10 부: 탐색 및 사이트 디자인에 대 한 최종 업데이트, 결론 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 10 부에서는 탐색 및의 최종 업데이트를 다룹니다.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 0c6e4c2f-fcdb-4978-9656-1990c6f15727
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
msc.type: authoredcontent
ms.openlocfilehash: f701d1fbabc3e1a97c3750d00e96bf8dba1105cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433613"
---
# <a name="part-10-final-updates-to-navigation-and-site-design-conclusion"></a><span data-ttu-id="c36cb-104">10 부: 탐색 및 사이트 디자인에 대 한 최종 업데이트, 결론</span><span class="sxs-lookup"><span data-stu-id="c36cb-104">Part 10: Final Updates to Navigation and Site Design, Conclusion</span></span>

<span data-ttu-id="c36cb-105">받은 사람 ( [Jon Galloway](https://github.com/jongalloway) )</span><span class="sxs-lookup"><span data-stu-id="c36cb-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="c36cb-106">MVC Music Store는 웹 개발용 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 소개 하 고 설명 하는 자습서 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="c36cb-107">MVC Music Store는 온라인으로 음악 앨범을 판매 하 고 기본적인 사이트 관리, 사용자 로그인 및 쇼핑 카트 기능을 구현 하는 간단한 샘플 저장소 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="c36cb-108">이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="c36cb-109">10 부에서는 탐색 및 사이트 디자인, 결론의 최종 업데이트를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-109">Part 10 covers Final Updates to Navigation and Site Design, Conclusion.</span></span>

<span data-ttu-id="c36cb-110">사이트에 대 한 모든 주요 기능을 완료 했지만 사이트 탐색, 홈 페이지 및 스토어 찾아보기 페이지에 몇 가지 기능을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-110">We've completed all the major functionality for our site, but we still have some features to add to the site navigation, the home page, and the Store Browse page.</span></span>

## <a name="creating-the-shopping-cart-summary-partial-view"></a><span data-ttu-id="c36cb-111">쇼핑 카트 요약 부분 보기 만들기</span><span class="sxs-lookup"><span data-stu-id="c36cb-111">Creating the Shopping Cart Summary Partial View</span></span>

<span data-ttu-id="c36cb-112">전체 사이트에서 사용자의 쇼핑 카트에 있는 항목 수를 표시 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-112">We want to expose the number of items in the user's shopping cart across the entire site.</span></span>

![](mvc-music-store-part-10/_static/image1.png)

<span data-ttu-id="c36cb-113">사이트 마스터에 추가 되는 부분 보기를 만들어이를 쉽게 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-113">We can easily implement this by creating a partial view which is added to our Site.master.</span></span>

<span data-ttu-id="c36cb-114">앞에서 설명한 것 처럼 ShoppingCart 컨트롤러에는 부분 뷰를 반환 하는 CartSummary 동작 메서드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-114">As shown previously, the ShoppingCart controller includes a CartSummary action method which returns a partial view:</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample1.cs)]

<span data-ttu-id="c36cb-115">CartSummary 부분 보기를 만들려면 Views/ShoppingCart 폴더를 마우스 오른쪽 단추로 클릭 하 고 뷰 추가를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-115">To create the CartSummary partial view, right-click on the Views/ShoppingCart folder and select Add View.</span></span> <span data-ttu-id="c36cb-116">보기의 이름을 CartSummary로 표시 하 고 아래와 같이 "부분 보기 만들기" 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-116">Name the view CartSummary and check the "Create a partial view" checkbox as shown below.</span></span>

![](mvc-music-store-part-10/_static/image2.png)

<span data-ttu-id="c36cb-117">CartSummary 부분 보기는 정말 간단 합니다. 장바구니의 항목 수를 보여 주는 ShoppingCart Index 뷰에 대 한 링크 일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-117">The CartSummary partial view is really simple - it's just a link to the ShoppingCart Index view which shows the number of items in the cart.</span></span> <span data-ttu-id="c36cb-118">CartSummary. cshtml의 전체 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-118">The complete code for CartSummary.cshtml is as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample2.cshtml)]

<span data-ttu-id="c36cb-119">Html RenderAction 메서드를 사용 하 여 사이트 마스터를 포함 하 여 사이트의 모든 페이지에 부분 보기를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-119">We can include a partial view in any page in the site, including the Site master, by using the Html.RenderAction method.</span></span> <span data-ttu-id="c36cb-120">RenderAction을 사용 하려면 아래와 같이 작업 이름 ("CartSummary") 및 컨트롤러 이름 ("ShoppingCart")을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-120">RenderAction requires us to specify the Action Name ("CartSummary") and the Controller Name ("ShoppingCart") as below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample3.cshtml)]

<span data-ttu-id="c36cb-121">이를 사이트 레이아웃에 추가 하기 전에 모든 사이트를 한 번에 변경할 수 있도록 장르 메뉴도 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-121">Before adding this to the site Layout, we will also create the Genre Menu so we can make all of our Site.master updates at one time.</span></span>

## <a name="creating-the-genre-menu-partial-view"></a><span data-ttu-id="c36cb-122">장르 메뉴 부분 보기 만들기</span><span class="sxs-lookup"><span data-stu-id="c36cb-122">Creating the Genre Menu Partial View</span></span>

<span data-ttu-id="c36cb-123">스토어에서 사용할 수 있는 장르를 모두 나열 하는 장르 메뉴를 추가 하 여 사용자가 스토어를 탐색 하는 것이 훨씬 더 쉬워질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-123">We can make it a lot easier for our users to navigate through the store by adding a Genre Menu which lists all the Genres available in our store.</span></span>

![](mvc-music-store-part-10/_static/image3.png)

<span data-ttu-id="c36cb-124">동일한 단계를 수행 하 여 GenreMenu 부분 보기를 만든 다음 두 항목을 모두 사이트 마스터에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-124">We will follow the same steps also create a GenreMenu partial view, and then we can add them both to the Site master.</span></span> <span data-ttu-id="c36cb-125">먼저 StoreController에 다음 GenreMenu 컨트롤러 작업을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-125">First, add the following GenreMenu controller action to the StoreController:</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample4.cs)]

<span data-ttu-id="c36cb-126">이 작업은 부분 보기에 표시 되는 장르 목록을 반환 합니다. 여기에서 다음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-126">This action returns a list of Genres which will be displayed by the partial view, which we will create next.</span></span>

<span data-ttu-id="c36cb-127">*참고:이 컨트롤러 작업에는 [ChildActionOnly] 특성을 추가 했습니다 .이 작업은 부분 보기 에서만이 작업을 사용 하도록 합니다. 이 특성은/Store/GenreMenu. 이동 하 여 컨트롤러 작업을 실행할 수 없도록 합니다. 이는 부분 보기에는 필요 하지 않지만 컨트롤러 작업이 의도 한 대로 사용 되는지 확인 하는 것이 좋습니다. 또한 뷰가 아닌 PartialView를 반환 합니다 .이는 다른 보기에 포함 되어 있으므로이 뷰에 대 한 레이아웃을 사용 하지 않아야 함을 알 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="c36cb-127">*Note: We have added the [ChildActionOnly] attribute to this controller action, which indicates that we only want this action to be used from a Partial View. This attribute will prevent the controller action from being executed by browsing to /Store/GenreMenu. This isn't required for partial views, but it is a good practice, since we want to make sure our controller actions are used as we intend. We are also returning PartialView rather than View, which lets the view engine know that it shouldn't use the Layout for this view, as it is being included in other views.*</span></span>

<span data-ttu-id="c36cb-128">GenreMenu 컨트롤러 작업을 마우스 오른쪽 단추로 클릭 하 고 아래와 같이 장르 뷰 데이터 클래스를 사용 하 여 강력한 형식의 GenreMenu 라는 부분 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-128">Right-click on the GenreMenu controller action and create a partial view named GenreMenu which is strongly typed using the Genre view data class as shown below.</span></span>

![](mvc-music-store-part-10/_static/image4.png)

<span data-ttu-id="c36cb-129">다음과 같이 순서가 지정 되지 않은 목록을 사용 하 여 항목을 표시 하도록 GenreMenu 부분 뷰에 대 한 뷰 코드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-129">Update the view code for the GenreMenu partial view to display the items using an unordered list as follows.</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample5.cshtml)]

## <a name="updating-site-layout-to-display-our-partial-views"></a><span data-ttu-id="c36cb-130">부분 보기를 표시 하도록 사이트 레이아웃 업데이트</span><span class="sxs-lookup"><span data-stu-id="c36cb-130">Updating Site Layout to display our Partial Views</span></span>

<span data-ttu-id="c36cb-131">Html RenderAction ()을 호출 하 여 사이트 레이아웃 (/Views/Shared/\_Layout. cshtml)에 부분 보기를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-131">We can add our partial views to the Site Layout (/Views/Shared/\_Layout.cshtml) by calling Html.RenderAction().</span></span> <span data-ttu-id="c36cb-132">아래와 같이에서 추가 태그를 추가 하 고 표시 하는 몇 가지 추가 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-132">We'll add them both in, as well as some additional markup to display them, as shown below:</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample6.cshtml)]

<span data-ttu-id="c36cb-133">이제 응용 프로그램을 실행할 때 왼쪽 탐색 영역에 장르를 표시 하 고 맨 위에 카트 요약을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-133">Now when we run the application, we will see the Genre in the left navigation area and the Cart Summary at the top.</span></span>

## <a name="update-to-the-store-browse-page"></a><span data-ttu-id="c36cb-134">스토어 찾아보기 페이지로 업데이트</span><span class="sxs-lookup"><span data-stu-id="c36cb-134">Update to the Store Browse page</span></span>

<span data-ttu-id="c36cb-135">저장소 찾아보기 페이지가 작동 하지만 매우 양호 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-135">The Store Browse page is functional, but doesn't look very good.</span></span> <span data-ttu-id="c36cb-136">다음과 같이 보기 코드 (/Views/Store/Browse.cshtml에 있음)를 업데이트 하 여 앨범을 더 나은 레이아웃으로 표시 하도록 페이지를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-136">We can update the page to show the albums in a better layout by updating the view code (found in /Views/Store/Browse.cshtml) as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample7.cshtml)]

<span data-ttu-id="c36cb-137">여기서는 Url을 사용 합니다. 즉, 링크에 특별 한 서식을 적용 하 여 앨범 아트 워크를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-137">Here we are making use of Url.Action rather than Html.ActionLink so that we can apply special formatting to the link to include the album artwork.</span></span>

<span data-ttu-id="c36cb-138">*참고: 이러한 앨범에 대 한 일반 앨범 커버를 표시 합니다. 이 정보는 데이터베이스에 저장 되며 저장소 관리자를 통해 편집할 수 있습니다. 사용자 고유의 아트 워크를 추가 하는 것을 환영 합니다.*</span><span class="sxs-lookup"><span data-stu-id="c36cb-138">*Note: We are displaying a generic album cover for these albums. This information is stored in the database and is editable via the Store Manager. You are welcome to add your own artwork.*</span></span>

<span data-ttu-id="c36cb-139">이제 장르를 찾으면 앨범 아트 워크가 있는 그리드에 표시 되는 앨범이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-139">Now when we browse to a Genre, we will see the albums shown in a grid with the album artwork.</span></span>

![](mvc-music-store-part-10/_static/image5.png)

## <a name="updating-the-home-page-to-show-top-selling-albums"></a><span data-ttu-id="c36cb-140">홈 페이지를 업데이트 하 여 상위 판매 앨범 표시</span><span class="sxs-lookup"><span data-stu-id="c36cb-140">Updating the Home Page to show Top Selling Albums</span></span>

<span data-ttu-id="c36cb-141">판매를 늘리기 위해 홈 페이지에서 상위 판매 앨범을 기능 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-141">We want to feature our top selling albums on the home page to increase sales.</span></span> <span data-ttu-id="c36cb-142">HomeController를 처리 하기 위해 몇 가지 업데이트를 수행 하 고 몇 가지 추가 그래픽도 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-142">We'll make some updates to our HomeController to handle that, and add in some additional graphics as well.</span></span>

<span data-ttu-id="c36cb-143">먼저, EntityFramework가 연결 된 것을 알 수 있도록 앨범 클래스에 탐색 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-143">First, we'll add a navigation property to our Album class so that EntityFramework knows that they're associated.</span></span> <span data-ttu-id="c36cb-144">이제 **앨범** 클래스의 마지막 몇 줄은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-144">The last few lines of our **Album** class should now look like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample8.cs)]

<span data-ttu-id="c36cb-145">*참고:이 작업을 수행 하려면 using 문을 추가 하 여 system.xml 네임 스페이스를 가져와야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="c36cb-145">*Note: This will require adding a using statement to bring in the System.Collections.Generic namespace.*</span></span>

<span data-ttu-id="c36cb-146">먼저 다른 컨트롤러에서와 같이 문을 사용 하 여 storeDB 필드와 MvcMusicStore를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-146">First, we'll add a storeDB field and the MvcMusicStore.Models using statements, as in our other controllers.</span></span> <span data-ttu-id="c36cb-147">다음으로, OrderDetails에 따라 가장 인기 있는 앨범을 찾기 위해 데이터베이스를 쿼리 하는 HomeController에 다음 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-147">Next, we'll add the following method to the HomeController which queries our database to find top selling albums according to OrderDetails.</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample9.cs)]

<span data-ttu-id="c36cb-148">이것은 컨트롤러 작업으로 사용할 수 있도록 설정 하지 않기 때문에 전용 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-148">This is a private method, since we don't want to make it available as a controller action.</span></span> <span data-ttu-id="c36cb-149">편의를 위해 HomeController에 포함 하는 것이 좋지만 비즈니스 논리를 별도의 서비스 클래스로 이동 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-149">We are including it in the HomeController for simplicity, but you are encouraged to move your business logic into separate service classes as appropriate.</span></span>

<span data-ttu-id="c36cb-150">이렇게 하면 인덱스 컨트롤러 작업을 업데이트 하 여 상위 5 개 판매 된 앨범을 쿼리하고 뷰로 돌아갈 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-150">With that in place, we can update the Index controller action to query the top 5 selling albums and return them to the view.</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample10.cs)]

<span data-ttu-id="c36cb-151">업데이트 된 HomeController에 대 한 전체 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-151">The complete code for the updated HomeController is as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample11.cs)]

<span data-ttu-id="c36cb-152">마지막으로, 모델 유형을 업데이트 하 고 아래쪽에 앨범 목록을 추가 하 여 앨범 목록을 표시할 수 있도록 홈 인덱스 보기를 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-152">Finally, we'll need to update our Home Index view so that it can display a list of albums by updating the Model type and adding the album list to the bottom.</span></span> <span data-ttu-id="c36cb-153">이 기회를 통해 페이지에 제목 및 판촉 섹션을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-153">We will take this opportunity to also add a heading and a promotion section to the page.</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample12.cshtml)]

<span data-ttu-id="c36cb-154">이제 응용 프로그램을 실행할 때 인기 있는 앨범 및 판촉 메시지를 포함 하는 업데이트 된 홈 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-154">Now when we run the application, we'll see our updated home page with top selling albums and our promotional message.</span></span>

![](mvc-music-store-part-10/_static/image1.jpg)

## <a name="conclusion"></a><span data-ttu-id="c36cb-155">결론</span><span class="sxs-lookup"><span data-stu-id="c36cb-155">Conclusion</span></span>

<span data-ttu-id="c36cb-156">ASP.NET MVC를 사용 하면 데이터베이스 액세스, 멤버 자격, AJAX 등의 복잡 한 웹 사이트를 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-156">We've seen that ASP.NET MVC makes it easy to create a sophisticated website with database access, membership, AJAX, etc.</span></span> <span data-ttu-id="c36cb-157">매우 빠르게 합니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-157">pretty quickly.</span></span> <span data-ttu-id="c36cb-158">이 자습서에서는 사용자 고유의 ASP.NET MVC 응용 프로그램 빌드를 시작 하는 데 필요한 도구를 제공 하는 데 도움을 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="c36cb-158">Hopefully this tutorial has given you the tools you need to get started building your own ASP.NET MVC applications!</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="c36cb-159">이전</span><span class="sxs-lookup"><span data-stu-id="c36cb-159">Previous</span></span>](mvc-music-store-part-9.md)
