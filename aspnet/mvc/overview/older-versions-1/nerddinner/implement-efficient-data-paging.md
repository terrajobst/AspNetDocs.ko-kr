---
uid: mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
title: 효율적인 데이터 페이징 구현 | Microsoft Docs
author: microsoft
description: 8 단계에서는 수천 개의 Dinners를 한 번에 표시 하는 대신/Dinners URL에 페이징 지원을 추가 하는 방법을 보여 줍니다. 여기서는 10 개의 예정 된 Dinners
ms.author: riande
ms.date: 07/27/2010
ms.assetid: adea836d-dbc2-4005-94ea-53aef09e9e34
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
msc.type: authoredcontent
ms.openlocfilehash: 2d9a0dba381b71755ac626f76d52bc5bcb434447
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486485"
---
# <a name="implement-efficient-data-paging"></a><span data-ttu-id="bab07-103">효율적인 데이터 페이징 구현</span><span class="sxs-lookup"><span data-stu-id="bab07-103">Implement Efficient Data Paging</span></span>

<span data-ttu-id="bab07-104">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="bab07-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="bab07-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="bab07-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="bab07-106">ASP.NET MVC 1을 사용 하 여 작고 완전 한 웹 응용 프로그램을 빌드하는 방법을 안내 하는 무료 ["Nerddinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 의 8 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-106">This is step 8 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="bab07-107">8 단계에서는 수천 개의 Dinners를 한 번에 표시 하는 대신/Dinners URL에 페이징 지원을 추가 하는 방법을 보여 줍니다 .이 경우에는 한 번에 10 개의 Dinners를 표시 하 고 최종 사용자가 다시 SEO 방식으로 전체 목록에 대 한 페이지를 앞뒤로 이동할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-107">Step 8 shows how to add paging support to our /Dinners URL so that instead of displaying 1000s of dinners at once, we'll only display 10 upcoming dinners at a time - and allow end-users to page back and forward through the entire list in an SEO friendly way.</span></span>
> 
> <span data-ttu-id="bab07-108">ASP.NET MVC 3을 사용 하는 경우 [mvc 3 시작](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [mvc Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-8-paging-support"></a><span data-ttu-id="bab07-109">NerdDinner Step 8: 페이징 지원</span><span class="sxs-lookup"><span data-stu-id="bab07-109">NerdDinner Step 8: Paging Support</span></span>

<span data-ttu-id="bab07-110">사이트가 성공적으로 완료 되 면 수천 개의 예정 된 dinners가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-110">If our site is successful, it will have thousands of upcoming dinners.</span></span> <span data-ttu-id="bab07-111">이러한 모든 dinners를 처리 하 고 사용자가 탐색할 수 있도록 UI를 확장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-111">We need to make sure that our UI scales to handle all of these dinners, and allows users to browse them.</span></span> <span data-ttu-id="bab07-112">이를 사용 하도록 설정 하기 위해 */Dinners* URL에 대 한 페이징 지원을 추가 하 여 수천 개의 Dinners를 한 번에 표시 하 고, 최종 사용자가 다시 SEO 방식으로 전체 목록에 대해 페이지를 이동 하 고 전달할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-112">To enable this, we'll add paging support to our */Dinners* URL so that instead of displaying 1000s of dinners at once, we'll only display 10 upcoming dinners at a time - and allow end-users to page back and forward through the entire list in an SEO friendly way.</span></span>

### <a name="index-action-method-recap"></a><span data-ttu-id="bab07-113">Index () 동작 메서드 요약</span><span class="sxs-lookup"><span data-stu-id="bab07-113">Index() Action Method Recap</span></span>

<span data-ttu-id="bab07-114">현재, DinnersController 클래스 내의 Index () 동작 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-114">The Index() action method within our DinnersController class currently looks like below:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample1.cs)]

<span data-ttu-id="bab07-115">*/Dinners* URL에 대 한 요청이 이루어지면 예정 된 모든 Dinners 목록을 검색 한 다음 모든 항목의 목록을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-115">When a request is made to the */Dinners* URL, it retrieves a list of all upcoming dinners and then renders a listing of all of them out:</span></span>

![](implement-efficient-data-paging/_static/image1.png)

### <a name="understanding-iqueryablelttgt"></a><span data-ttu-id="bab07-116">IQueryable&lt;T&gt; 이해</span><span class="sxs-lookup"><span data-stu-id="bab07-116">Understanding IQueryable&lt;T&gt;</span></span>

<span data-ttu-id="bab07-117">*IQueryable&lt;t&gt;* 은 .net 3.5의 일부로 LINQ를 사용 하 여 도입 된 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-117">*IQueryable&lt;T&gt;* is an interface that was introduced with LINQ as part of .NET 3.5.</span></span> <span data-ttu-id="bab07-118">이를 통해 강력한 "지연 된 실행" 시나리오를 사용할 수 있습니다 .이 시나리오에서는를 활용 하 여 페이징 지원을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-118">It enables powerful "deferred execution" scenarios that we can take advantage of to implement paging support.</span></span>

<span data-ttu-id="bab07-119">이 FindUpcomingDinners () 메서드에서 IQueryable&lt;Dinner&gt; 시퀀스를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-119">In our DinnerRepository we are returning an IQueryable&lt;Dinner&gt; sequence from our FindUpcomingDinners() method:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample2.cs)]

<span data-ttu-id="bab07-120">FindUpcomingDinners () 메서드에서 반환 하는 IQueryable&lt;Dinner&gt; 개체는 LINQ to SQL를 사용 하 여 데이터베이스에서 Dinner objects를 검색 하는 쿼리를 캡슐화 합니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-120">The IQueryable&lt;Dinner&gt; object returned by our FindUpcomingDinners() method encapsulates a query to retrieve Dinner objects from our database using LINQ to SQL.</span></span> <span data-ttu-id="bab07-121">중요 한 점은 쿼리의 데이터에 대 한 액세스/반복을 시도 하거나에 대해 ToList () 메서드를 호출할 때까지 데이터베이스에 대해 쿼리를 실행 하지 않는다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-121">Importantly, it won't execute the query against the database until we attempt to access/iterate over the data in the query, or until we call the ToList() method on it.</span></span> <span data-ttu-id="bab07-122">FindUpcomingDinners () 메서드를 호출 하는 코드는 쿼리를 실행 하기 전에 필요에 따라 IQueryable&lt;Dinner&gt; 개체에 "연결 된" 작업/필터를 추가 하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-122">The code calling our FindUpcomingDinners() method can optionally choose to add additional "chained" operations/filters to the IQueryable&lt;Dinner&gt; object before executing the query.</span></span> <span data-ttu-id="bab07-123">그런 다음 데이터가 요청 될 때 데이터베이스에 대해 결합 된 쿼리를 실행 하기에 충분 한 LINQ to SQL 합니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-123">LINQ to SQL is then smart enough to execute the combined query against the database when the data is requested.</span></span>

<span data-ttu-id="bab07-124">페이징 논리를 구현 하기 위해 다음에는 ToList ()를 호출 하기 전에 반환 된 IQueryable&lt;Dinner&gt; 시퀀스에 추가 "Skip" 및 "Take" 연산자를 적용 하도록 DinnersController의 Index () 동작 메서드를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-124">To implement paging logic we can update our DinnersController's Index() action method so that it applies additional "Skip" and "Take" operators to the returned IQueryable&lt;Dinner&gt; sequence before calling ToList() on it:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample3.cs)]

<span data-ttu-id="bab07-125">위의 코드는 데이터베이스에서 처음 10 개의 예정 된 dinners를 건너뛴 다음 백 20 dinners을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-125">The above code skips over the first 10 upcoming dinners in the database, and then returns back 20 dinners.</span></span> <span data-ttu-id="bab07-126">LINQ to SQL는 웹 서버가 아닌 SQL database에서이 건너뛴 논리를 수행 하는 최적화 된 SQL 쿼리를 생성할 수 있을 정도로 지능적입니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-126">LINQ to SQL is smart enough to construct an optimized SQL query that performs this skipping logic in the SQL database – and not in the web-server.</span></span> <span data-ttu-id="bab07-127">즉, 데이터베이스에 수백만 개의 예정 된 Dinners가 있는 경우에도이 요청에 포함 된 10 개만 검색 됩니다 (효율적이 고 확장 가능).</span><span class="sxs-lookup"><span data-stu-id="bab07-127">This means that even if we have millions of upcoming Dinners in the database, only the 10 we want will be retrieved as part of this request (making it efficient and scalable).</span></span>

### <a name="adding-a-page-value-to-the-url"></a><span data-ttu-id="bab07-128">URL에 "page" 값 추가</span><span class="sxs-lookup"><span data-stu-id="bab07-128">Adding a "page" value to the URL</span></span>

<span data-ttu-id="bab07-129">특정 페이지 범위를 하드 코딩 하는 대신 Url에 사용자가 요청 하는 Dinner range를 나타내는 "page" 매개 변수를 포함 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-129">Instead of hard-coding a specific page range, we'll want our URLs to include a "page" parameter that indicates which Dinner range a user is requesting.</span></span>

#### <a name="using-a-querystring-value"></a><span data-ttu-id="bab07-130">Querystring 값 사용</span><span class="sxs-lookup"><span data-stu-id="bab07-130">Using a Querystring value</span></span>

<span data-ttu-id="bab07-131">아래 코드에서는 querystring 매개 변수를 지원 하도록 Index () 작업 메서드를 업데이트 하 고 */Dinners? page = 2*와 같은 url을 사용 하도록 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-131">The code below demonstrates how we can update our Index() action method to support a querystring parameter and enable URLs like */Dinners?page=2*:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample4.cs)]

<span data-ttu-id="bab07-132">위의 Index () 동작 메서드에는 "page" 라는 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-132">The Index() action method above has a parameter named "page".</span></span> <span data-ttu-id="bab07-133">이 매개 변수는 nullable 정수로 선언 됩니다 (int?는이를 나타냄).</span><span class="sxs-lookup"><span data-stu-id="bab07-133">The parameter is declared as a nullable integer (that is what int? indicates).</span></span> <span data-ttu-id="bab07-134">즉, */Dinners? page = 2* URL을 사용 하면 값이 "2"가 매개 변수 값으로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-134">This means that the */Dinners?page=2* URL will cause a value of "2" to be passed as the parameter value.</span></span> <span data-ttu-id="bab07-135">*/Dinners* URL (querystring 값이 없는 경우)을 사용 하면 null 값이 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-135">The */Dinners* URL (without a querystring value) will cause a null value to be passed.</span></span>

<span data-ttu-id="bab07-136">페이지 값을 페이지 크기 (이 경우 10 행)로 곱하여 건너뛸 dinners 수를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-136">We are multiplying the page value by the page size (in this case 10 rows) to determine how many dinners to skip over.</span></span> <span data-ttu-id="bab07-137">Nullable 형식을 처리할 때 유용 하 게 사용 되는 [ C# null "병합" 연산자 (??)](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx) 를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-137">We are using the [C# null "coalescing" operator (??)](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx) which is useful when dealing with nullable types.</span></span> <span data-ttu-id="bab07-138">위의 코드는 페이지 매개 변수가 null 인 경우 페이지 값을 0으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-138">The code above assigns page the value of 0 if the page parameter is null.</span></span>

#### <a name="using-embedded-url-values"></a><span data-ttu-id="bab07-139">포함 된 URL 값 사용</span><span class="sxs-lookup"><span data-stu-id="bab07-139">Using Embedded URL values</span></span>

<span data-ttu-id="bab07-140">Querystring 값을 사용 하는 대신 실제 URL 내에 페이지 매개 변수를 포함 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-140">An alternative to using a querystring value would be to embed the page parameter within the actual URL itself.</span></span> <span data-ttu-id="bab07-141">예: */Dinners/Page/2* 또는 */Dinners/2*.</span><span class="sxs-lookup"><span data-stu-id="bab07-141">For example: */Dinners/Page/2* or */Dinners/2*.</span></span> <span data-ttu-id="bab07-142">ASP.NET MVC에는 이와 같은 시나리오를 쉽게 지원할 수 있게 해 주는 강력한 URL 라우팅 엔진이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-142">ASP.NET MVC includes a powerful URL routing engine that makes it easy to support scenarios like this.</span></span>

<span data-ttu-id="bab07-143">들어오는 모든 URL 또는 URL 형식을 원하는 컨트롤러 클래스나 작업 메서드에 매핑하는 사용자 지정 라우팅 규칙을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-143">We can register custom routing rules that map any incoming URL or URL format to any controller class or action method we want.</span></span> <span data-ttu-id="bab07-144">프로젝트 내에서 global.asax 파일을 열려면 다음을 수행 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-144">All we need to-do is to open the Global.asax file within our project:</span></span>

![](implement-efficient-data-paging/_static/image2.png)

<span data-ttu-id="bab07-145">그런 다음 경로에 대 한 첫 번째 호출과 같은 MapRoute () 도우미 메서드를 사용 하 여 새 매핑 규칙을 등록 합니다. MapRoute ():</span><span class="sxs-lookup"><span data-stu-id="bab07-145">And then register a new mapping rule using the MapRoute() helper method like the first call to routes.MapRoute() below:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample5.cs)]

<span data-ttu-id="bab07-146">위에서 "UpcomingDinners" 라는 새 라우팅 규칙을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-146">Above we are registering a new routing rule named "UpcomingDinners".</span></span> <span data-ttu-id="bab07-147">URL 형식 "Dinners/Page/{page}"를 나타냅니다. 여기서 {Page}는 URL에 포함 된 매개 변수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-147">We are indicating it has the URL format "Dinners/Page/{page}" – where {page} is a parameter value embedded within the URL.</span></span> <span data-ttu-id="bab07-148">MapRoute () 메서드의 세 번째 매개 변수는이 형식과 일치 하는 Url을 DinnersController 클래스의 Index () 동작 메서드에 매핑해야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-148">The third parameter to the MapRoute() method indicates that we should map URLs that match this format to the Index() action method on the DinnersController class.</span></span>

<span data-ttu-id="bab07-149">Querystring 시나리오를 사용 하 여 이전에 했던 것과 정확히 동일한 인덱스 () 코드를 사용할 수 있습니다. 단, 지금은 "page" 매개 변수는 URL에서 제공 되 고 querystring은 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-149">We can use the exact same Index() code we had before with our Querystring scenario – except now our "page" parameter will come from the URL and not the querystring:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample6.cs)]

<span data-ttu-id="bab07-150">이제 응용 프로그램을 실행 하 고 */Dinners* 를 입력 하는 경우 처음 10 개의 예정 Dinners이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-150">And now when we run the application and type in */Dinners* we'll see the first 10 upcoming dinners:</span></span>

![](implement-efficient-data-paging/_static/image3.png)

<span data-ttu-id="bab07-151">*/Dinners/Page/1* 을 입력 하면 Dinners의 다음 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-151">And when we type in */Dinners/Page/1* we'll see the next page of dinners:</span></span>

![](implement-efficient-data-paging/_static/image4.png)

### <a name="adding-page-navigation-ui"></a><span data-ttu-id="bab07-152">페이지 탐색 UI 추가</span><span class="sxs-lookup"><span data-stu-id="bab07-152">Adding page navigation UI</span></span>

<span data-ttu-id="bab07-153">페이징 시나리오를 완료 하는 마지막 단계는 사용자가 Dinner data를 쉽게 건너뛸 수 있도록 보기 템플릿 내에서 "다음" 및 "이전" 탐색 UI를 구현 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-153">The last step to complete our paging scenario will be to implement "next" and "previous" navigation UI within our view template to enable users to easily skip over the Dinner data.</span></span>

<span data-ttu-id="bab07-154">이를 올바르게 구현 하려면 데이터베이스의 총 Dinners 수와이를 변환 하는 데이터 페이지 수를 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-154">To implement this correctly, we'll need to know the total number of Dinners in the database, as well as how many pages of data this translates to.</span></span> <span data-ttu-id="bab07-155">그런 다음 현재 요청 된 "페이지" 값이 데이터의 시작 또는 끝에 있는지 여부를 계산 하 고 그에 따라 "이전" 및 "다음" UI를 표시 하거나 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-155">We'll then need to calculate whether the currently requested "page" value is at the beginning or end of the data, and show or hide the "previous" and "next" UI accordingly.</span></span> <span data-ttu-id="bab07-156">Index () 작업 메서드 내에서이 논리를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-156">We could implement this logic within our Index() action method.</span></span> <span data-ttu-id="bab07-157">또는 더 다시 사용할 수 있는 방식으로이 논리를 캡슐화 하는 도우미 클래스를 프로젝트에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-157">Alternatively we can add a helper class to our project that encapsulates this logic in a more re-usable way.</span></span>

<span data-ttu-id="bab07-158">다음은 .NET Framework 기본 제공 되는 목록&lt;T&gt; 컬렉션 클래스에서 파생 되는 간단한 "PaginatedList" 도우미 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-158">Below is a simple "PaginatedList" helper class that derives from the List&lt;T&gt; collection class built-into the .NET Framework.</span></span> <span data-ttu-id="bab07-159">이 클래스는 IQueryable 데이터의 시퀀스를 다시 매기는 데 사용할 수 있는 다시 사용할 수 있는 컬렉션 클래스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-159">It implements a re-usable collection class that can be used to paginate any sequence of IQueryable data.</span></span> <span data-ttu-id="bab07-160">이러한 작업을 수행 하는 데 사용 되는&lt;Dinner&gt; 결과에 대해 IQueryable을 사용 하는 것이 좋지만, iqueryable&lt;Product&gt; 또는 IQueryable&lt;고객&gt; 다른 응용 프로그램 시나리오에 대 한 결과를 쉽게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-160">In our NerdDinner application we'll have it work over IQueryable&lt;Dinner&gt; results, but it could just as easily be used against IQueryable&lt;Product&gt; or IQueryable&lt;Customer&gt; results in other application scenarios:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample7.cs)]

<span data-ttu-id="bab07-161">위에서 "PageIndex", "PageSize", "TotalCount" 및 "TotalPages"와 같은 속성을 계산 하 고 표시 하는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-161">Notice above how it calculates and then exposes properties like "PageIndex", "PageSize", "TotalCount", and "TotalPages".</span></span> <span data-ttu-id="bab07-162">또한 컬렉션의 데이터 페이지가 원래 시퀀스의 시작 또는 끝에 있는지 여부를 나타내는 두 개의 도우미 속성인 "HasPreviousPage" 및 "HasNextPage"를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-162">It also then exposes two helper properties "HasPreviousPage" and "HasNextPage" that indicate whether the page of data in the collection is at the beginning or end of the original sequence.</span></span> <span data-ttu-id="bab07-163">위의 코드는 두 개의 SQL 쿼리를 실행 하 여 두 개의 SQL 쿼리를 실행 합니다. 첫 번째는 Dinner objects의 총 수를 검색 하는 것입니다 .이는 개체를 반환 하지 않고 정수를 반환 하는 "SELECT COUNT" 문을 수행 하는 것이 고, 두 번째는의 행만 검색 하는 것입니다. 현재 데이터 페이지의 데이터베이스에서 필요한 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-163">The above code will cause two SQL queries to be run - the first to retrieve the count of the total number of Dinner objects (this doesn't return the objects – rather it performs a "SELECT COUNT" statement that returns an integer), and the second to retrieve just the rows of data we need from our database for the current page of data.</span></span>

<span data-ttu-id="bab07-164">그런 다음 FindUpcomingDinners () 결과에서 PaginatedList&lt;Dinner&gt;를 만들어이를 뷰 템플릿에 전달 하는 데 사용할 수 있습니다. Index () 도우미 메서드를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-164">We can then update our DinnersController.Index() helper method to create a PaginatedList&lt;Dinner&gt; from our DinnerRepository.FindUpcomingDinners() result, and pass it to our view template:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample8.cs)]

<span data-ttu-id="bab07-165">그런 다음 \Views\Dinners\Index.aspx view 템플릿이 viewpage&lt;에서 상속 하도록 view 템플릿을 업데이트 하 고, IEnumerable&lt;Dinner&lt;&gt;하는 ViewPage 대신 PaginatedList&lt;Dinner&gt;&gt; 하 고, 다음 코드를 보기 템플릿 아래쪽에 추가 하 여 다음 및 이전 탐색 UI를 표시 하거나 숨길 수 있습니다.&gt;</span><span class="sxs-lookup"><span data-stu-id="bab07-165">We can then update the \Views\Dinners\Index.aspx view template to inherit from ViewPage&lt;NerdDinner.Helpers.PaginatedList&lt;Dinner&gt;&gt; instead of ViewPage&lt;IEnumerable&lt;Dinner&gt;&gt;, and then add the following code to the bottom of our view-template to show or hide next and previous navigation UI:</span></span>

[!code-aspx[Main](implement-efficient-data-paging/samples/sample9.aspx)]

<span data-ttu-id="bab07-166">위의 RouteLink () 도우미 메서드를 사용 하 여 하이퍼링크를 생성 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-166">Notice above how we are using the Html.RouteLink() helper method to generate our hyperlinks.</span></span> <span data-ttu-id="bab07-167">이 메서드는 이전에 사용한 Html.actionlink () 도우미 메서드와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-167">This method is similar to the Html.ActionLink() helper method we've used previously.</span></span> <span data-ttu-id="bab07-168">차이점은 Global.asax 파일 내에서 설정 하는 "UpcomingDinners" 라우팅 규칙을 사용 하 여 URL을 생성 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-168">The difference is that we are generating the URL using the "UpcomingDinners" routing rule we setup within our Global.asax file.</span></span> <span data-ttu-id="bab07-169">이렇게 하면 */Dinners/Page/{page}* – 형식의 Index () 작업 메서드에 대 한 url을 생성할 수 있습니다. 여기서 {Page} 값은 현재 PageIndex를 기준으로 위에서 제공 하는 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-169">This ensures that we'll generate URLs to our Index() action method that have the format: */Dinners/Page/{page}* – where the {page} value is a variable we are providing above based on the current PageIndex.</span></span>

<span data-ttu-id="bab07-170">이제 응용 프로그램을 다시 실행 하면 브라우저에서 한 번에 10 개의 dinners 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-170">And now when we run our application again we'll see 10 dinners at a time in our browser:</span></span>

![](implement-efficient-data-paging/_static/image5.png)

<span data-ttu-id="bab07-171">또한 페이지 맨 아래에는 &lt;&lt;&lt; 하 고 &gt;&gt;검색 엔진 액세스 가능 Url을 사용 하 여 데이터를 앞뒤로 건너뛸 수 있습니다.&gt;</span><span class="sxs-lookup"><span data-stu-id="bab07-171">We also have &lt;&lt;&lt; and &gt;&gt;&gt; navigation UI at the bottom of the page that allows us to skip forwards and backwards over our data using search engine accessible URLs:</span></span>

![](implement-efficient-data-paging/_static/image6.png)

| <span data-ttu-id="bab07-172">**측면 토픽: IQueryable&lt;T&gt;의 의미 이해**</span><span class="sxs-lookup"><span data-stu-id="bab07-172">**Side Topic: Understanding the implications of IQueryable&lt;T&gt;**</span></span> |
| --- |
| <span data-ttu-id="bab07-173">IQueryable&lt;T&gt;는 페이징 및 컴퍼지션 기반 쿼리와 같은 다양 한 흥미로운 지연 된 실행 시나리오를 가능 하 게 해 주는 매우 강력한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-173">IQueryable&lt;T&gt; is a very powerful feature that enables a variety of interesting deferred execution scenarios (like paging and composition based queries).</span></span> <span data-ttu-id="bab07-174">모든 강력한 기능을 사용 하는 것과 마찬가지로 사용 하는 방법에 주의 하 여 악용 되지 않는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-174">As with all powerful features, you want to be careful with how you use it and make sure it is not abused.</span></span> <span data-ttu-id="bab07-175">리포지토리에서 IQueryable&lt;T&gt; 결과를 반환 한다는 것을 인식 하는 것이 중요 합니다 .이를 통해 호출 코드에서 연결 된 연산자 메서드를 추가 하 여 최종 쿼리 실행에 참여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-175">It is important to recognize that returning an IQueryable&lt;T&gt; result from your repository enables calling code to append on chained operator methods to it, and so participate in the ultimate query execution.</span></span> <span data-ttu-id="bab07-176">이러한 기능을 호출 하는 코드를 제공 하지 않으려는 경우 이미 실행 한 쿼리 결과를 포함 하는 IList&lt;T&gt; 또는 IEnumerable&lt;T&gt; 결과를 다시 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-176">If you do not want to provide calling code this ability, then you should return back IList&lt;T&gt; or IEnumerable&lt;T&gt; results - which contain the results of a query that has already executed.</span></span> <span data-ttu-id="bab07-177">페이지 매김 시나리오의 경우 실제 데이터 페이지 매김 논리를 호출 되는 리포지토리 메서드에 푸시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-177">For pagination scenarios this would require you to push the actual data pagination logic into the repository method being called.</span></span> <span data-ttu-id="bab07-178">이 시나리오에서는 FindUpcomingDinners () finder 메서드를 업데이트 하 여 PaginatedList를 반환 하는 서명을 포함할 수 있습니다. PaginatedList&lt; Dinner&gt; FindUpcomingDinners (int pageIndex, int pageSize) {} 또는 IList&lt;Dinner&gt;을 반환 하 고 "totalCount" out 매개 변수를 사용 하 여 총 Dinners: IList&lt;Dinner&gt; FindUpcomingDinners (int pageIndex, int pageSize, out int totalCount) {}을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-178">In this scenario we might update our FindUpcomingDinners() finder method to have a signature that either returned a PaginatedList: PaginatedList&lt; Dinner&gt; FindUpcomingDinners(int pageIndex, int pageSize) { } Or return back an IList&lt;Dinner&gt;, and use a "totalCount" out param to return the total count of Dinners: IList&lt;Dinner&gt; FindUpcomingDinners(int pageIndex, int pageSize, out int totalCount) { }</span></span> |

### <a name="next-step"></a><span data-ttu-id="bab07-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bab07-179">Next Step</span></span>

<span data-ttu-id="bab07-180">이제 응용 프로그램에 인증 및 권한 부여 지원을 추가 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bab07-180">Let's now look at how we can add authentication and authorization support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="bab07-181">[이전](re-use-ui-using-master-pages-and-partials.md)
> [다음](secure-applications-using-authentication-and-authorization.md)</span><span class="sxs-lookup"><span data-stu-id="bab07-181">[Previous](re-use-ui-using-master-pages-and-partials.md)
[Next](secure-applications-using-authentication-and-authorization.md)</span></span>
