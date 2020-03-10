---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
title: '7 부: 기능 추가 | Microsoft Docs'
author: JoeStagner
description: 이 자습서 시리즈에서는 Tailspin Spyworks 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 7 부에서는 계정 revie 같은 추가 기능을 추가 합니다.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 50223ee9-11b9-4cf3-bca2-e2f10bf471f3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
msc.type: authoredcontent
ms.openlocfilehash: ffd2b862c727db9572c272b7b21bcc33c822fffa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521567"
---
# <a name="part-7-adding-features"></a><span data-ttu-id="e7f30-104">7 부: 기능 추가</span><span class="sxs-lookup"><span data-stu-id="e7f30-104">Part 7: Adding Features</span></span>

<span data-ttu-id="e7f30-105">만든 사람 [Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="e7f30-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="e7f30-106">Tailspin Spyworks는 .NET 플랫폼을 위한 강력 하 고 확장 가능한 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="e7f30-107">ASP.NET 4의 새로운 기능을 사용 하 여 쇼핑, 구매 및 관리를 포함 한 온라인 상점을 구축 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="e7f30-108">이 자습서 시리즈에서는 Tailspin Spyworks 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="e7f30-109">7 부에서는 계정 검토, 제품 리뷰, "인기 있는 항목" 및 "구매한" 사용자 정의 컨트롤 등의 추가 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-109">Part 7 adds additional features, such as account review, product reviews, and "popular items" and "also purchased" user controls.</span></span>

## <a id="_Toc260221673"></a><span data-ttu-id="e7f30-110">기능 추가</span><span class="sxs-lookup"><span data-stu-id="e7f30-110">Adding Features</span></span>

<span data-ttu-id="e7f30-111">사용자는 카탈로그를 찾아보고, 장바구니에 항목을 저장 하 고, 체크 아웃 프로세스를 완료할 수 있지만 사이트 개선을 위해 포함할 수 있는 다양 한 지원 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-111">Though users can browse our catalog, place items in their shopping cart, and complete the checkout process, there are a number of supporting features that we will include to improve our site.</span></span>

1. <span data-ttu-id="e7f30-112">계정 검토 (주문 나열 및 세부 정보 보기)</span><span class="sxs-lookup"><span data-stu-id="e7f30-112">Account Review (List orders placed and view details.)</span></span>
2. <span data-ttu-id="e7f30-113">일부 컨텍스트별 콘텐츠를 프런트 페이지에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-113">Add some context specific content to the front page.</span></span>
3. <span data-ttu-id="e7f30-114">사용자가 카탈로그에서 제품을 검토할 수 있는 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-114">Add a feature to let users Review the products in the catalog.</span></span>
4. <span data-ttu-id="e7f30-115">인기 있는 항목을 표시 하 고 해당 컨트롤을 front 페이지에 넣는 사용자 정의 컨트롤을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-115">Create a User Control to display Popular Items and Place that control on the front page.</span></span>
5. <span data-ttu-id="e7f30-116">"구매한 항목" 사용자 정의 컨트롤을 만들고 제품 정보 페이지에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-116">Create an "Also Purchased" user control and add it to the product details page.</span></span>
6. <span data-ttu-id="e7f30-117">연락처 페이지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-117">Add a Contact Page.</span></span>
7. <span data-ttu-id="e7f30-118">정보 페이지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-118">Add an About Page.</span></span>
8. <span data-ttu-id="e7f30-119">전역 오류</span><span class="sxs-lookup"><span data-stu-id="e7f30-119">Global Error</span></span>

## <a id="_Toc260221674"></a><span data-ttu-id="e7f30-120">계정 검토</span><span class="sxs-lookup"><span data-stu-id="e7f30-120">Account Review</span></span>

<span data-ttu-id="e7f30-121">"Account" 폴더에서 OrderDetails 라는 두 개의 .aspx 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-121">In the "Account" folder create two .aspx pages one named OrderList.aspx and the other named OrderDetails.aspx</span></span>

<span data-ttu-id="e7f30-122">OrderList .aspx는 이전에 했던 것 처럼 GridView 및 EntityDataSource 컨트롤을 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-122">OrderList.aspx will leverage the GridView and EntityDataSource controls much as we have previously.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample1.aspx)]

<span data-ttu-id="e7f30-123">EntityDataSource은 사용자가 로그인 할 때 세션 변수에 설정 된 사용자 이름 (WhereParameter 참조)에 대해 필터링 된 Orders 테이블에서 레코드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-123">The EntityDataSource selects records from the Orders table filtered on the UserName (see the WhereParameter) which we set in a session variable when the user log's in.</span></span>

<span data-ttu-id="e7f30-124">또한 GridView의 하이퍼링크 필드에는 다음 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-124">Note also these parameters in the HyperlinkField of the GridView:</span></span>

[!code-xml[Main](tailspin-spyworks-part-7/samples/sample2.xml)]

<span data-ttu-id="e7f30-125">이는 OrderID 필드를 OrderDetails 페이지에 대 한 QueryString 매개 변수로 지정 하는 각 제품에 대 한 주문 정보 뷰에 대 한 링크를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-125">These specify the link to the Order details view for each product specifying the OrderID field as a QueryString parameter to the OrderDetails.aspx page.</span></span>

## <a id="_Toc260221675"></a><span data-ttu-id="e7f30-126">OrderDetails</span><span class="sxs-lookup"><span data-stu-id="e7f30-126">OrderDetails.aspx</span></span>

<span data-ttu-id="e7f30-127">EntityDataSource 컨트롤을 사용 하 여 주문 데이터를 표시 하 고 FormView를 사용 하 여 주문 데이터를 표시 하 고 다른 EntityDataSource GridView를 사용 하 여 모든 주문의 줄 항목을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-127">We will use an EntityDataSource control to access the Orders and a FormView to display the Order data and another EntityDataSource with a GridView to display all the Order's line items.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample3.aspx)]

<span data-ttu-id="e7f30-128">코드 숨김이 파일 (OrderDetails.aspx.cs)에는 두 가지 약간의 정리 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-128">In the Code Behind file (OrderDetails.aspx.cs) we have two little bits of housekeeping.</span></span>

<span data-ttu-id="e7f30-129">먼저 OrderDetails가 항상 OrderId를 사용 하도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-129">First we need to make sure that OrderDetails always gets an OrderId.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample4.cs)]

<span data-ttu-id="e7f30-130">또한 품목에서 주문 합계를 계산 하 여 표시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-130">We also need to calculate and display the order total from the line items.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample5.cs)]

## <a id="_Toc260221676"></a><span data-ttu-id="e7f30-131">홈 페이지</span><span class="sxs-lookup"><span data-stu-id="e7f30-131">The Home Page</span></span>

<span data-ttu-id="e7f30-132">Default.aspx 페이지에 일부 정적 콘텐츠를 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-132">Let's add some static content to the Default.aspx page.</span></span>

<span data-ttu-id="e7f30-133">먼저 "Content" 폴더와이 폴더 내에 이미지 폴더를 만듭니다. 홈 페이지에서 사용할 이미지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-133">First I'll create a "Content" folder and within it an Images folder (and I'll include an image to be used on the home page.)</span></span>

<span data-ttu-id="e7f30-134">Default.aspx 페이지의 아래쪽 자리 표시자에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-134">Into the bottom placeholder of the Default.aspx page, add the following markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample6.aspx)]

## <a id="_Toc260221677"></a><span data-ttu-id="e7f30-135">제품 리뷰</span><span class="sxs-lookup"><span data-stu-id="e7f30-135">Product Reviews</span></span>

<span data-ttu-id="e7f30-136">먼저 제품 검토를 시작 하는 데 사용할 수 있는 폼에 대 한 링크를 포함 하는 단추를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-136">First we'll add a button with a link to a form that we can use to enter a product review.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample7.aspx)]

![](tailspin-spyworks-part-7/_static/image1.jpg)

<span data-ttu-id="e7f30-137">쿼리 문자열에 ProductID를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-137">Note that we are passing the ProductID in the query string</span></span>

<span data-ttu-id="e7f30-138">그런 다음 ReviewAdd 이라는 추가 페이지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-138">Next let's add page named ReviewAdd.aspx</span></span>

<span data-ttu-id="e7f30-139">이 페이지에서는 ASP.NET AJAX 컨트롤 도구 키트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-139">This page will use the ASP.NET AJAX Control Toolkit.</span></span> <span data-ttu-id="e7f30-140">아직 수행 하지 않은 경우 [Devexpress](http://devexpress.com/act) 에서 다운로드할 수 있습니다. 여기 [https://www.asp.net/learn/ajax-videos/video-76.aspx](../../../videos/ajax-control-toolkit/how-do-i-get-started-with-the-aspnet-ajax-control-toolkit.md)에서 Visual Studio와 함께 사용할 도구 키트를 설정 하는 방법에 대 한 지침이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-140">If you have not already done so you can download it from [DevExpress](http://devexpress.com/act) and there is guidance on setting up the toolkit for use with Visual Studio here [https://www.asp.net/learn/ajax-videos/video-76.aspx](../../../videos/ajax-control-toolkit/how-do-i-get-started-with-the-aspnet-ajax-control-toolkit.md).</span></span>

<span data-ttu-id="e7f30-141">디자인 모드에서 도구 상자의 컨트롤 및 유효성 검사기를 끌고 아래와 같은 폼을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-141">In design mode, drag controls and validators from the toolbox and build a form like the one below.</span></span>

![](tailspin-spyworks-part-7/_static/image2.jpg)

<span data-ttu-id="e7f30-142">태그는 다음과 유사 하 게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-142">The markup will look something like this.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample8.aspx)]

<span data-ttu-id="e7f30-143">이제 리뷰를 입력할 수 있으므로 제품 페이지에 해당 리뷰를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-143">Now that we can enter reviews, lets display those reviews on the product page.</span></span>

<span data-ttu-id="e7f30-144">이 태그를 제품 세부 정보 .aspx 페이지에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-144">Add this markup to the ProductDetails.aspx page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample9.aspx)]

<span data-ttu-id="e7f30-145">지금 응용 프로그램을 실행 하 고 제품으로 이동 하면 고객 리뷰를 비롯 한 제품 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-145">Running our application now and navigating to a product shows the product information including customer reviews.</span></span>

![](tailspin-spyworks-part-7/_static/image3.jpg)

## <a id="_Toc260221678"></a><span data-ttu-id="e7f30-146">인기 있는 항목 컨트롤 (사용자 정의 컨트롤 만들기)</span><span class="sxs-lookup"><span data-stu-id="e7f30-146">Popular Items Control (Creating User Controls)</span></span>

<span data-ttu-id="e7f30-147">웹 사이트에서 판매를 증가 시키기 위해 인기 있거나 관련 된 제품을 "추천 판매" 하는 두 가지 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-147">In order to increase sales on your web site we will add a couple of features to "suggestive sell" popular or related products.</span></span>

<span data-ttu-id="e7f30-148">이러한 기능 중 첫 번째 기능은 제품 카탈로그의 인기 제품 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-148">The first of these features will be a list of the more popular product in our product catalog.</span></span>

<span data-ttu-id="e7f30-149">응용 프로그램의 홈 페이지에 상위 판매 항목을 표시 하는 "사용자 정의 컨트롤"을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-149">We will create a "User Control" to display the top selling items on the home page of our application.</span></span> <span data-ttu-id="e7f30-150">이 컨트롤은 컨트롤이 되기 때문에 Visual Studio 디자이너의 컨트롤을 원하는 페이지에 끌어서 놓는 방법으로 페이지에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-150">Since this will be a control, we can use it on any page by simply dragging and dropping the control in Visual Studio's designer onto any page that we like.</span></span>

<span data-ttu-id="e7f30-151">Visual Studio의 솔루션 탐색기에서 솔루션 이름을 마우스 오른쪽 단추로 클릭 하 고 "Controls" 라는 새 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-151">In Visual Studio's solutions explorer, right-click on the solution name and create a new directory named "Controls".</span></span> <span data-ttu-id="e7f30-152">이 작업을 수행할 필요는 없지만 "Controls" 디렉터리에 모든 사용자 정의 컨트롤을 만들어 프로젝트를 구성 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-152">While it is not necessary to do so, we will help keep our project organized by creating all our user controls in the "Controls" directory.</span></span>

<span data-ttu-id="e7f30-153">Controls 폴더를 마우스 오른쪽 단추로 클릭 하 고 "새 항목"을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-153">Right-click on the controls folder and choose "New Item" :</span></span>

![](tailspin-spyworks-part-7/_static/image4.jpg)

<span data-ttu-id="e7f30-154">"PopularItems" 컨트롤의 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-154">Specify a name for our control of "PopularItems".</span></span> <span data-ttu-id="e7f30-155">사용자 정의 컨트롤용 파일 확장명은 .aspx이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-155">Note that the file extension for user controls is .ascx not .aspx.</span></span>

<span data-ttu-id="e7f30-156">인기 있는 항목 사용자 정의 컨트롤은 다음과 같이 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-156">Our Popular Items User control will be defined as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample10.aspx)]

<span data-ttu-id="e7f30-157">여기서는이 응용 프로그램에서 아직 사용 하지 않은 메서드를 사용 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-157">Here we're using a method we have not used yet in this application.</span></span> <span data-ttu-id="e7f30-158">Repeater 컨트롤을 사용 하는 대신, 데이터 소스 컨트롤을 사용 하는 대신 Repeater 컨트롤을 LINQ to Entities 쿼리의 결과에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-158">We're using the repeater control and instead of using a data source control we're binding the Repeater Control to the results of a LINQ to Entities query.</span></span>

<span data-ttu-id="e7f30-159">컨트롤의 코드 뒤에서 다음과 같이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-159">In the code behind of our control we do that as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample11.cs)]

<span data-ttu-id="e7f30-160">컨트롤 태그의 위쪽에 있는이 중요 한 줄도 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-160">Note also this important line at the top of our control's markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample12.aspx)]

<span data-ttu-id="e7f30-161">가장 인기 있는 항목은 분 단위로 변경 되지 않으므로 응용 프로그램의 성능을 향상 시키기 위해 aching 지시어를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-161">Since the most popular items won't be changing on a minute to minute basis we can add a aching directive to improve the performance of our application.</span></span> <span data-ttu-id="e7f30-162">이 지시문을 통해 컨트롤 코드는 캐시 된 컨트롤의 출력이 만료 될 때만 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-162">This directive will cause the controls code to only be executed when the cached output of the control expires.</span></span> <span data-ttu-id="e7f30-163">그렇지 않으면 캐시 된 버전의 컨트롤 출력이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-163">Otherwise, the cached version of the control's output will be used.</span></span>

<span data-ttu-id="e7f30-164">이제 Default.aspx 페이지에 새로운 컨트롤을 포함 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-164">Now all we have to do is include our new control in our Default.aspx page.</span></span>

<span data-ttu-id="e7f30-165">끌어서 놓기를 사용 하 여 컨트롤의 인스턴스를 기본 폼의 열린 열에 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-165">Use drag and drop to place an instance of the control in the open column of our Default form.</span></span>

![](tailspin-spyworks-part-7/_static/image5.jpg)

<span data-ttu-id="e7f30-166">이제 응용 프로그램을 실행할 때 홈 페이지에 가장 인기 있는 항목이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-166">Now when we run our application the home page displays the most popular items.</span></span>

![](tailspin-spyworks-part-7/_static/image6.jpg)

## <a id="_Toc260221679"></a><span data-ttu-id="e7f30-167">"구매한 사용자 정의 컨트롤 (매개 변수가 있는 사용자 정의 컨트롤)</span><span class="sxs-lookup"><span data-stu-id="e7f30-167">"Also Purchased" Control (User Controls with Parameters)</span></span>

<span data-ttu-id="e7f30-168">만들 두 번째 사용자 정의 컨트롤은 컨텍스트 특이성를 추가 하 여 다음 수준으로 판매 하는 추천을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-168">The second User Control that we'll create will take suggestive selling to the next level by adding context specificity.</span></span>

<span data-ttu-id="e7f30-169">상위 "구매한" 항목을 계산 하는 논리는 trivial이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-169">The logic to calculate the top "Also Purchased" items is non-trivial.</span></span>

<span data-ttu-id="e7f30-170">"또한 구매한" 제어는 현재 선택 된 ProductID에 대 한 OrderDetails 레코드 (이전에 구매한)를 선택 하 고 발견 되는 각각의 고유한 주문에 대해 OrderIDs를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-170">Our "Also Purchased" control will select the OrderDetails records (previously purchased) for the currently selected ProductID and grab the OrderIDs for each unique order that is found.</span></span>

<span data-ttu-id="e7f30-171">그런 다음 모든 주문에서 제품을 al으로 선택 하 고 구매한 수량을 합산 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-171">Then we will select al the products from all those Orders and sum the quantities purchased.</span></span> <span data-ttu-id="e7f30-172">이 수량 합계를 기준으로 제품을 정렬 하 고 상위 5 개 항목을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-172">We'll sort the products by that quantity sum and display the top five items.</span></span>

<span data-ttu-id="e7f30-173">이 논리의 복잡성을 고려 하 여이 알고리즘을 저장 프로시저로 구현할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-173">Given the complexity of this logic, we will implement this algorithm as a stored procedure.</span></span>

<span data-ttu-id="e7f30-174">저장 프로시저에 대 한 T-sql은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-174">The T-SQL for the stored procedure is as follows.</span></span>

[!code-sql[Main](tailspin-spyworks-part-7/samples/sample13.sql)]

<span data-ttu-id="e7f30-175">이 저장 프로시저 (SelectPurchasedWithProducts)는 응용 프로그램에 포함 했을 때 데이터베이스에 있었지만, 필요한 테이블 및 뷰 외에도 지정 된 엔터티 데이터 모델를 생성 한 경우 엔터티 데이터 모델 이 저장 프로시저를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-175">Note that this stored procedure (SelectPurchasedWithProducts) existed in the database when we included it in our application and when we generated the Entity Data Model we specified that, in addition to the Tables and Views that we needed, the Entity Data Model should include this stored procedure.</span></span>

<span data-ttu-id="e7f30-176">엔터티 데이터 모델에서 저장 프로시저에 액세스 하려면 함수를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-176">To access the stored procedure from the Entity Data Model we need to import the function.</span></span>

<span data-ttu-id="e7f30-177">솔루션 탐색기에서 엔터티 데이터 모델을 두 번 클릭 하 여 디자이너에서 열고 모델 브라우저를 연 다음 디자이너를 마우스 오른쪽 단추로 클릭 하 고 "함수 가져오기 추가"를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-177">Double Click on the Entity Data Model in the Solutions Explorer to open it in the designer and open the Model Browser, then right-click in the designer and select "Add Function Import".</span></span>

![](tailspin-spyworks-part-7/_static/image1.png)

<span data-ttu-id="e7f30-178">이렇게 하면이 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-178">Doing so will open this dialog.</span></span>

![](tailspin-spyworks-part-7/_static/image2.png)

<span data-ttu-id="e7f30-179">위에 표시 된 대로 필드를 입력 하 고, "SelectPurchasedWithProducts"를 선택 하 고, 가져온 함수의 이름에 프로시저 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-179">Fill out the fields as you see above, selecting the "SelectPurchasedWithProducts" and use the procedure name for the name of our imported function.</span></span>

<span data-ttu-id="e7f30-180">"확인"을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-180">Click "Ok".</span></span>

<span data-ttu-id="e7f30-181">이 작업을 수행 하면 모델의 다른 항목을 비롯 하 여 저장 프로시저를 간단히 프로그래밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-181">Having done this we can simply program against the stored procedure as we might any other item in the model.</span></span>

<span data-ttu-id="e7f30-182">따라서 "Controls" 폴더에서 AlsoPurchased 이라는 새 사용자 정의 컨트롤을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-182">So, in our "Controls" folder create a new user control named AlsoPurchased.ascx.</span></span>

<span data-ttu-id="e7f30-183">이 컨트롤에 대 한 태그는 PopularItems 컨트롤에 매우 익숙할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-183">The markup for this control will look very familiar to the PopularItems control.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample14.aspx)]

<span data-ttu-id="e7f30-184">주목할 만한 차이점은 렌더링 될 항목의 수는 제품 마다 다르므로 출력을 캐싱하지 않는다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-184">The notable difference is that are not caching the output since the item's to be rendered will differ by product.</span></span>

<span data-ttu-id="e7f30-185">ProductId는 컨트롤에 대 한 "속성"이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-185">The ProductId will be a "property" to the control.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample15.cs)]

<span data-ttu-id="e7f30-186">컨트롤의 PreRender 이벤트 처리기에서 3 가지 작업을 수행 하는 것을 eed.</span><span class="sxs-lookup"><span data-stu-id="e7f30-186">In the control's PreRender event handler we eed to do three things.</span></span>

1. <span data-ttu-id="e7f30-187">ProductID가 설정 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-187">Make sure the ProductID is set.</span></span>
2. <span data-ttu-id="e7f30-188">현재 제품으로 구매한 제품이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-188">See if there are any products that have been purchased with the current one.</span></span>
3. <span data-ttu-id="e7f30-189">#2에서 결정 된 일부 항목을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-189">Output some items as determined in #2.</span></span>

<span data-ttu-id="e7f30-190">모델을 통해 저장 프로시저를 호출 하는 것이 얼마나 쉬운지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-190">Note how easy it is to call the stored procedure through the model.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample16.cs)]

<span data-ttu-id="e7f30-191">"구매"를 확인 한 후에는 쿼리에 의해 반환 된 결과에만 repeater를 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-191">After determining that there ARE "also purchased" we can simply bind the repeater to the results returned by the query.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample17.cs)]

<span data-ttu-id="e7f30-192">"구매한 항목" 항목이 없는 경우 카탈로그에서 다른 인기 항목을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-192">If there were not any "also purchased" items we'll simply display other popular items from our catalog.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample18.cs)]

<span data-ttu-id="e7f30-193">"구매한 항목" 항목을 보려면 제품 세부 정보 .aspx 페이지를 열고 솔루션 탐색기에서 AlsoPurchased 컨트롤을 끌어 태그의이 위치에 표시 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-193">To view the "Also Purchased" items, open the ProductDetails.aspx page and drag the AlsoPurchased control from the Solutions Explorer so that it appears in this position in the markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample19.aspx)]

<span data-ttu-id="e7f30-194">이렇게 하면 제품 세부 정보 페이지의 맨 위에 있는 컨트롤에 대 한 참조가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-194">Doing so will create a reference to the control at the top of the ProductDetails page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample20.aspx)]

<span data-ttu-id="e7f30-195">AlsoPurchased 사용자 정의 컨트롤에 ProductId 숫자가 필요 하므로 페이지의 현재 데이터 모델 항목에 대 한 Eval 문을 사용 하 여 컨트롤의 ProductID 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-195">Since the AlsoPurchased user control requires a ProductId number we will set the ProductID property of our control by using an Eval statement against the current data model item of the page.</span></span>

![](tailspin-spyworks-part-7/_static/image3.png)

<span data-ttu-id="e7f30-196">지금 빌드하고 실행 하 여 제품으로 이동 하면 "구매한 항목" 항목이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7f30-196">When we build and run now and browse to a product we see the "Also Purchased" items.</span></span>

![](tailspin-spyworks-part-7/_static/image7.jpg)

> [!div class="step-by-step"]
> <span data-ttu-id="e7f30-197">[이전](tailspin-spyworks-part-6.md)
> [다음](tailspin-spyworks-part-8.md)</span><span class="sxs-lookup"><span data-stu-id="e7f30-197">[Previous](tailspin-spyworks-part-6.md)
[Next](tailspin-spyworks-part-8.md)</span></span>
