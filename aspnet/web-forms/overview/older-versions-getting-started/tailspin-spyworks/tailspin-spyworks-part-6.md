---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
title: '6 부: ASP.NET 멤버 자격 | Microsoft Docs'
author: JoeStagner
description: 이 자습서 시리즈에서는 Tailspin Spyworks 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 6 부는 ASP.NET 멤버 자격을 추가 합니다.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: f70a310c-9557-4743-82cb-655265676d39
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
msc.type: authoredcontent
ms.openlocfilehash: b0caa89dc9ffb5bb7451fa2d9d346c7db2bf1466
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454883"
---
# <a name="part-6-aspnet-membership"></a><span data-ttu-id="a1fa2-104">6 부: ASP.NET 멤버 자격</span><span class="sxs-lookup"><span data-stu-id="a1fa2-104">Part 6: ASP.NET Membership</span></span>

<span data-ttu-id="a1fa2-105">만든 사람 [Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="a1fa2-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="a1fa2-106">Tailspin Spyworks는 .NET 플랫폼을 위한 강력 하 고 확장 가능한 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="a1fa2-107">ASP.NET 4의 새로운 기능을 사용 하 여 쇼핑, 구매 및 관리를 포함 한 온라인 상점을 구축 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="a1fa2-108">이 자습서 시리즈에서는 Tailspin Spyworks 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="a1fa2-109">6 부는 ASP.NET 멤버 자격을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-109">Part 6 adds ASP.NET Membership.</span></span>

## <a id="_Toc260221672"></a><span data-ttu-id="a1fa2-110">ASP.NET 멤버 자격 사용</span><span class="sxs-lookup"><span data-stu-id="a1fa2-110">Working with ASP.NET Membership</span></span>

![](tailspin-spyworks-part-6/_static/image1.png)

<span data-ttu-id="a1fa2-111">보안을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-111">Click Security</span></span>

![](tailspin-spyworks-part-6/_static/image1.jpg)

<span data-ttu-id="a1fa2-112">폼 인증을 사용 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-112">Make sure that we are using forms authentication.</span></span>

![](tailspin-spyworks-part-6/_static/image2.jpg)

<span data-ttu-id="a1fa2-113">"사용자 만들기" 링크를 사용 하 여 두 명의 사용자를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-113">Use the "Create User" link to create a couple of users.</span></span>

![](tailspin-spyworks-part-6/_static/image3.jpg)

<span data-ttu-id="a1fa2-114">완료 되 면 솔루션 탐색기 창을 참조 하 고 보기를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-114">When done, refer to the Solution Explorer window and refresh the view.</span></span>

![](tailspin-spyworks-part-6/_static/image2.png)

<span data-ttu-id="a1fa2-115">ASPNETDB.MDF를 확인 합니다. MDF를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-115">Note that the ASPNETDB.MDF fine has been created.</span></span> <span data-ttu-id="a1fa2-116">이 파일에는 멤버 자격과 같은 핵심 ASP.NET 서비스를 지 원하는 테이블이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-116">This file contains the tables to support the core ASP.NET services like membership.</span></span>

<span data-ttu-id="a1fa2-117">이제 체크 아웃 프로세스의 구현을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-117">Now we can begin implementing the checkout process.</span></span>

<span data-ttu-id="a1fa2-118">먼저 CheckOut .aspx 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-118">Begin by creating a CheckOut.aspx page.</span></span>

<span data-ttu-id="a1fa2-119">체크 인 한 사용자만 체크 인 .aspx 페이지를 사용할 수 있으므로 로그인 한 사용자에 대 한 액세스를 제한 하 고 로그인 페이지에 로그인 하지 않은 사용자를 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-119">The CheckOut.aspx page should only be available to users who are logged in so we will restrict access to logged in users and redirect users who are not logged in to the LogIn page.</span></span>

<span data-ttu-id="a1fa2-120">이렇게 하려면 web.config 파일의 구성 섹션에 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-120">To do this we'll add the following to the configuration section of our web.config file.</span></span>

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample1.xml)]

<span data-ttu-id="a1fa2-121">ASP.NET Web Forms 응용 프로그램에 대 한 템플릿은 인증 섹션을 web.config 파일에 자동으로 추가 하 고 기본 로그인 페이지를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-121">The template for ASP.NET Web Forms applications automatically added an authentication section to our web.config file and established the default login page.</span></span>

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample2.xml)]

<span data-ttu-id="a1fa2-122">사용자가 로그인 할 때 익명 쇼핑 카트를 마이그레이션하려면 로그인 .aspx 코드 뒤에 있는 파일을 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-122">We must modify the Login.aspx code behind file to migrate an anonymous shopping cart when the user logs in.</span></span> <span data-ttu-id="a1fa2-123">페이지\_Load 이벤트를 다음과 같이 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-123">Change the Page\_Load event as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample3.cs)]

<span data-ttu-id="a1fa2-124">그런 다음 "LoggedIn" 이벤트 처리기를 추가 하 여 새로 로그인 한 사용자에 게 세션 이름을 설정 하 고 MyShoppingCart 클래스에서 MigrateCart 메서드를 호출 하 여 장바구니의 임시 세션 id를 사용자의 임시 세션 id로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-124">Then add a "LoggedIn" event handler like this to set the session name to the newly logged in user and change the temporary session id in the shopping cart to that of the user by calling the MigrateCart method in our MyShoppingCart class.</span></span> <span data-ttu-id="a1fa2-125">(.Cs 파일에서 구현 됨)</span><span class="sxs-lookup"><span data-stu-id="a1fa2-125">(Implemented in the .cs file)</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample4.cs)]

<span data-ttu-id="a1fa2-126">이와 같이 MigrateCart () 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-126">Implement the MigrateCart() method like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample5.cs)]

<span data-ttu-id="a1fa2-127">체크아웃할 때 쇼핑 카트 페이지에서와 마찬가지로 체크 아웃 페이지에서 EntityDataSource 및 GridView를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-127">In checkout.aspx we'll use an EntityDataSource and a GridView in our check out page much as we did in our shopping cart page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-6/samples/sample6.aspx)]

<span data-ttu-id="a1fa2-128">GridView 컨트롤은 MyList\_RowDataBound 바인딩된 "이벤트 처리기를 지정 하므로 다음과 같이 해당 이벤트 처리기를 구현 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-128">Note that our GridView control specifies an "ondatabound" event handler named MyList\_RowDataBound so let's implement that event handler like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample7.cs)]

<span data-ttu-id="a1fa2-129">이 방법은 각 행이 바인딩될 때 쇼핑 카트의 누계를 유지 하 고 GridView의 아래쪽 행을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-129">This method keeps a running total of the shopping cart as each row is bound and updates the bottom row of the GridView.</span></span>

<span data-ttu-id="a1fa2-130">이 단계에서는 배치할 주문에 대 한 "검토" 프레젠테이션을 구현 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-130">At this stage we have implemented a "review" presentation of the order to be placed.</span></span>

<span data-ttu-id="a1fa2-131">페이지\_Load 이벤트에 몇 줄의 코드를 추가 하 여 빈 카트 시나리오를 처리 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-131">Let's handle an empty cart scenario by adding a few lines of code to our Page\_Load event:</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample8.cs)]

<span data-ttu-id="a1fa2-132">사용자가 "제출" 단추를 클릭 하면 제출 단추 클릭 이벤트 처리기에서 다음 코드가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-132">When the user clicks on the "Submit" button we will execute the following code in the Submit Button Click Event handler.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample9.cs)]

<span data-ttu-id="a1fa2-133">주문 제출 프로세스의 "기타"는 MyShoppingCart 클래스의 SubmitOrder () 메서드를 통해 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-133">The "meat" of the order submission process is to be implemented in the SubmitOrder() method of our MyShoppingCart class.</span></span>

<span data-ttu-id="a1fa2-134">SubmitOrder는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-134">SubmitOrder will:</span></span>

- <span data-ttu-id="a1fa2-135">쇼핑 카트에 있는 모든 품목을 가져와 새 주문 레코드와 연결 된 OrderDetails 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-135">Take all the line items in the shopping cart and use them to create a new Order Record and the associated OrderDetails records.</span></span>
- <span data-ttu-id="a1fa2-136">운송 날짜를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-136">Calculate Shipping Date.</span></span>
- <span data-ttu-id="a1fa2-137">쇼핑 카트를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-137">Clear the shopping cart.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample10.cs)]

<span data-ttu-id="a1fa2-138">이 샘플 응용 프로그램의 목적에 따라 현재 날짜에 2 일을 추가 하 여 운송 날짜를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-138">For the purposes of this sample application we'll calculate a ship date by simply adding two days to the current date.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample11.cs)]

<span data-ttu-id="a1fa2-139">이제 응용 프로그램을 실행 하면 쇼핑 프로세스를 처음부터 끝까지 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1fa2-139">Running the application now will permit us to test the shopping process from start to finish.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a1fa2-140">[이전](tailspin-spyworks-part-5.md)
> [다음](tailspin-spyworks-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="a1fa2-140">[Previous](tailspin-spyworks-part-5.md)
[Next](tailspin-spyworks-part-7.md)</span></span>
