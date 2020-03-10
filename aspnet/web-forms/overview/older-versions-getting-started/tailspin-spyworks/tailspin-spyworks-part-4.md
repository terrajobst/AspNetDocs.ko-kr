---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
title: '4 부: 제품 나열 | Microsoft Docs'
author: JoeStagner
description: 이 자습서 시리즈에서는 Tailspin Spyworks 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 4 부에서는 GridView를 사용 하 여 제품을 나열 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 4fab47d5-a6ec-4fdc-91f0-651a093a24b9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
msc.type: authoredcontent
ms.openlocfilehash: 7af1b8afa2ecc8df9846f2edd2091b26b93a811c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78457283"
---
# <a name="part-4-listing-products"></a><span data-ttu-id="01a56-104">4 부: 제품 나열</span><span class="sxs-lookup"><span data-stu-id="01a56-104">Part 4: Listing Products</span></span>

<span data-ttu-id="01a56-105">만든 사람 [Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="01a56-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="01a56-106">Tailspin Spyworks는 .NET 플랫폼을 위한 강력 하 고 확장 가능한 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="01a56-107">ASP.NET 4의 새로운 기능을 사용 하 여 쇼핑, 구매 및 관리를 포함 한 온라인 상점을 구축 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="01a56-108">이 자습서 시리즈에서는 Tailspin Spyworks 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="01a56-109">4 부에서는 GridView 컨트롤을 사용 하 여 제품을 나열 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-109">Part 4 covers listing products with the GridView control.</span></span>

## <a id="_Toc260221670"></a><span data-ttu-id="01a56-110">GridView 컨트롤을 사용 하 여 제품 나열</span><span class="sxs-lookup"><span data-stu-id="01a56-110">Listing Products with the GridView Control</span></span>

<span data-ttu-id="01a56-111">솔루션에서 "마우스 오른쪽 단추를 클릭" 하 고 "추가" 및 "새 항목"을 선택 하 여 ProductsList 페이지를 구현 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-111">Let's begin implementing our ProductsList.aspx page by "Right Clicking" on our solution and selecting "Add" and "New Item".</span></span>

![](tailspin-spyworks-part-4/_static/image1.jpg)

<span data-ttu-id="01a56-112">"마스터 페이지를 사용 하 여 웹 양식"을 선택 하 고 페이지 이름을 ProductsList로 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-112">Choose "Web Form Using Master Page" and enter a page name of ProductsList.aspx".</span></span>

<span data-ttu-id="01a56-113">"추가"를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-113">Click "Add".</span></span>

![](tailspin-spyworks-part-4/_static/image2.jpg)

<span data-ttu-id="01a56-114">그런 다음, Site.master 페이지를 배치할 "스타일" 폴더를 선택 하 고 "폴더 내용" 창에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-114">Next choose the "Styles" folder where we placed the Site.Master page and select it from the "Contents of folder" window.</span></span>

![](tailspin-spyworks-part-4/_static/image3.jpg)

<span data-ttu-id="01a56-115">"확인"을 클릭 하 여 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-115">Click "Ok" to create the page.</span></span>

<span data-ttu-id="01a56-116">데이터베이스는 아래와 같이 제품 데이터로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-116">Our database is populated with product data as seen below.</span></span>

![](tailspin-spyworks-part-4/_static/image4.jpg)

<span data-ttu-id="01a56-117">페이지를 만든 후에는 다시 엔터티 데이터 원본을 사용 하 여 해당 제품 데이터에 액세스할 수 있지만이 인스턴스에서는 제품 엔터티를 선택 해야 하며, 선택한 범주에 대 한 항목 으로만 반환 되는 항목을 제한 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-117">After our page is created we'll again use an Entity Data Source to access that product data, but in this instance we need to select the Product Entities and we need to restrict the items that are returned to only those for the selected Category.</span></span>

<span data-ttu-id="01a56-118">이를 위해 WHERE 절을 자동으로 생성 하도록 EntityDataSource에 지시 하 고 WhereParameter를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-118">To accomplish this we'll tell the EntityDataSource to Auto Generate the WHERE clause and we'll specify the WhereParameter.</span></span>

<span data-ttu-id="01a56-119">"제품 범주 메뉴"에서 메뉴 항목을 만들었을 때 각 링크에 대 한 QueryString에 CategoryID를 추가 하 여 링크를 동적으로 작성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-119">You'll recall that when we created the Menu Items in our "Product Category Menu" we dynamically built the link by adding the CategoryID to the QueryString for each link.</span></span> <span data-ttu-id="01a56-120">해당 QueryString 매개 변수에서 WHERE 매개 변수를 파생 하도록 엔터티 데이터 소스에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-120">We will tell the Entity Data Source to derive the WHERE parameter from that QueryString parameter.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample1.aspx)]

<span data-ttu-id="01a56-121">다음으로 제품 목록을 표시 하도록 ListView 컨트롤을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-121">Next, we'll configure the ListView control to display a list of products.</span></span> <span data-ttu-id="01a56-122">최적의 쇼핑 환경을 만들려면 ListVew에 표시 되는 각 개별 제품에 몇 가지 간결한 기능을 압축 합니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-122">To create an optimal shopping experience we'll compact several concise features into each individual product displayed in our ListVew.</span></span>

- <span data-ttu-id="01a56-123">제품 이름은 제품의 세부 정보 보기에 대 한 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-123">The product name will be a link to the product's detail view.</span></span>
- <span data-ttu-id="01a56-124">제품의 가격이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-124">The product's price will be displayed.</span></span>
- <span data-ttu-id="01a56-125">제품 이미지가 표시 되 고 응용 프로그램의 카탈로그 이미지 디렉터리에서 이미지를 동적으로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-125">An image of the product will be displayed and we'll dynamically select the image from a catalog images directory in our application.</span></span>
- <span data-ttu-id="01a56-126">특정 제품을 쇼핑 카트에 즉시 추가 하는 링크가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-126">We will include a link to immediately add the specific product to the shopping cart.</span></span>

<span data-ttu-id="01a56-127">ListView 컨트롤 인스턴스의 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-127">Here is the markup for our ListView control instance.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample2.aspx)]

<span data-ttu-id="01a56-128">표시 된 각 제품에 대 한 여러 링크를 동적으로 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-128">We are dynamically building several links for each displayed product.</span></span>

<span data-ttu-id="01a56-129">또한 새 페이지를 테스트 하기 전에 다음과 같이 제품 카탈로그 이미지에 대 한 디렉터리 구조를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-129">Also, before we test own new page we need to create the directory structure for the product catalog images as follows.</span></span>

![](tailspin-spyworks-part-4/_static/image1.png)

<span data-ttu-id="01a56-130">제품 이미지에 액세스할 수 있게 되 면 제품 목록 페이지를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-130">Once our product images are accessible we can test our product list page.</span></span>

![](tailspin-spyworks-part-4/_static/image5.jpg)

<span data-ttu-id="01a56-131">사이트의 홈 페이지에서 범주 목록 링크 중 하나를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-131">From the site's home page, click on one of the Category List Links.</span></span>

![](tailspin-spyworks-part-4/_static/image6.jpg)

<span data-ttu-id="01a56-132">이제는 제품 세부 정보 .aspx 페이지 및 기능 카트 기능을 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-132">Now we need to implement the ProductDetails.aspx page and the AddToCart functionality.</span></span>

<span data-ttu-id="01a56-133">파일-&gt;새로 만들기를 사용 하 여 이전에 했던 것 처럼 사이트 마스터 페이지를 사용 하 여 페이지 이름 제품 정보 .aspx를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-133">Use File-&gt;New to create a page name ProductDetails.aspx using the site Master Page as we did previously.</span></span>

<span data-ttu-id="01a56-134">EntityDataSource 컨트롤을 다시 사용 하 여 데이터베이스의 특정 제품 레코드에 액세스 하 고, 다음과 같이 ASP.NET FormView 컨트롤을 사용 하 여 제품 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-134">We will again use an EntityDataSource control to access the specific product record in the database and we will use an ASP.NET FormView control to display the product data as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample3.aspx)]

<span data-ttu-id="01a56-135">서식 지정이 약간 재미를 보이는 경우 걱정 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="01a56-135">Don't worry if the formatting looks a bit funny to you.</span></span> <span data-ttu-id="01a56-136">위의 태그는 나중에 구현할 몇 가지 기능에 대해 표시 레이아웃의 공간을 남겨 둡니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-136">The markup above leaves room in the display layout for a couple of features we'll implement later on.</span></span>

<span data-ttu-id="01a56-137">쇼핑 카트는 응용 프로그램의 더 복잡 한 논리를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-137">The Shopping Cart will represent the more complex logic in our application.</span></span> <span data-ttu-id="01a56-138">시작 하려면 파일-&gt;New를 사용 하 여 MyShoppingCart 라는 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-138">To get started, use File-&gt;New to create a page called MyShoppingCart.aspx.</span></span>

<span data-ttu-id="01a56-139">ShoppingCart 이름은 선택 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-139">Note that we are not choosing the name ShoppingCart.aspx.</span></span>

<span data-ttu-id="01a56-140">데이터베이스는 "ShoppingCart" 라는 테이블을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-140">Our database contains a table named "ShoppingCart".</span></span> <span data-ttu-id="01a56-141">엔터티 데이터 모델 생성 된 경우 데이터베이스의 각 테이블에 대해 클래스가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-141">When we generated an Entity Data Model a class was created for each table in the database.</span></span> <span data-ttu-id="01a56-142">따라서 엔터티 데이터 모델는 "ShoppingCart" 라는 엔터티 클래스를 생성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-142">Therefore, the Entity Data Model generated an Entity Class named "ShoppingCart".</span></span> <span data-ttu-id="01a56-143">쇼핑 카트 구현에 해당 이름을 사용 하거나 필요에 맞게 확장할 수 있도록 모델을 편집할 수 있지만, 충돌을 방지 하는 이름을 대신 선택 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-143">We could edit the model so that we could use that name for our shopping cart implementation or extend it for our needs, but we will opt instead to simply select a name that will avoid the conflict.</span></span>

<span data-ttu-id="01a56-144">또한 간단한 쇼핑 카트를 만들고 쇼핑 카트 표시를 사용 하 여 쇼핑 카트 논리를 포함 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-144">It's also worth noting that we will be creating a simple shopping cart and embedding the shopping cart logic with the shopping cart display.</span></span> <span data-ttu-id="01a56-145">또한 완전히 별도의 비즈니스 계층에서 쇼핑 카트를 구현 하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01a56-145">We might also choose to implement our shopping cart in a completely separate Business Layer.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="01a56-146">[이전](tailspin-spyworks-part-3.md)
> [다음](tailspin-spyworks-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="01a56-146">[Previous](tailspin-spyworks-part-3.md)
[Next](tailspin-spyworks-part-5.md)</span></span>
