---
uid: web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
title: ASP.NET 웹 페이지 (Razor) 사이트에서 읽을 수 있는 Url 만들기 | Microsoft Docs
author: Rick-Anderson
description: 이 문서에서는 Razor (ASP.NET 웹 페이지) 웹 사이트의 라우팅을 설명 하 고이를 통해 SEO에 대해 더 읽기 쉽고 향상 된 Url을 사용 하는 방법을 설명 합니다. 수행할 작업 ...
ms.author: riande
ms.date: 02/17/2014
ms.assetid: a8aac1ac-89de-4415-afe0-97a41c6423d2
msc.legacyurl: /web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: 832db8e144cab730f16c78f67c12feb9b7c92c7c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509909"
---
# <a name="creating-readable-urls-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="42bb7-104">ASP.NET 웹 페이지 (Razor) 사이트에서 읽을 수 있는 Url 만들기</span><span class="sxs-lookup"><span data-stu-id="42bb7-104">Creating Readable URLs in ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="42bb7-105">만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="42bb7-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="42bb7-106">이 문서에서는 Razor (ASP.NET 웹 페이지) 웹 사이트의 라우팅을 설명 하 고이를 통해 SEO에 대해 더 읽기 쉽고 향상 된 Url을 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-106">This article describes routing in an ASP.NET Web Pages (Razor) website, and how this lets you use URLs that are more readable and better for SEO.</span></span>
> 
> <span data-ttu-id="42bb7-107">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="42bb7-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="42bb7-108">ASP.NET에서 라우팅을 사용 하 여 더 읽기 쉽고 검색 가능한 Url을 사용할 수 있도록 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-108">How ASP.NET uses routing to let you use more readable and searchable URLs.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="42bb7-109">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="42bb7-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="42bb7-110">ASP.NET 웹 페이지 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="42bb7-110">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="42bb7-111">이 자습서는 ASP.NET 웹 페이지 2 에서도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-111">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="about-routing"></a><span data-ttu-id="42bb7-112">라우팅 정보</span><span class="sxs-lookup"><span data-stu-id="42bb7-112">About Routing</span></span>

<span data-ttu-id="42bb7-113">사이트의 페이지에 대 한 Url은 사이트의 작동 방식에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-113">The URLs for the pages in your site can have an impact on how well the site works.</span></span> <span data-ttu-id="42bb7-114">친숙 한&quot; &quot;URL을 사용 하면 사용자가 사이트를 보다 쉽게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-114">A URL that's &quot;friendly&quot; can make it easier for people to use the site.</span></span> <span data-ttu-id="42bb7-115">사이트의 SEO (검색 엔진 최적화)에도 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-115">It can also help with search-engine optimization (SEO) for the site.</span></span> <span data-ttu-id="42bb7-116">ASP.NET 웹 사이트에는 친숙 한 Url을 자동으로 사용 하는 기능이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-116">ASP.NET websites include the ability to use friendly URLs automatically.</span></span>

<span data-ttu-id="42bb7-117">ASP.NET를 사용 하면 단순히 서버의 파일을 가리키는 대신 사용자 동작을 설명 하는 의미 있는 Url을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-117">ASP.NET lets you create meaningful URLs that describe user actions instead of just pointing to a file on the server.</span></span> <span data-ttu-id="42bb7-118">가상 블로그에 대해 다음 Url을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-118">Consider these URLs for a fictional blog:</span></span>

- `http://www.contoso.com/Blog/blog.cshtml?categories=hardware`
- `http://www.contoso.com//Blog/blog.cshtml?startdate=2009-11-01&enddate=2009-11-30`

<span data-ttu-id="42bb7-119">이러한 Url을 다음과 같이 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-119">Compare those URLs to the following ones:</span></span>

- `http://www.contoso.com/Blog/categories/hardware/`
- `http://www.contoso.com/Blog/2009/November`

<span data-ttu-id="42bb7-120">첫 번째 쌍의 사용자 *는 블로그의 blog 페이지를* 사용 하 여 블로그를 표시 하 고 올바른 범주나 날짜 범위를 가져오는 쿼리 문자열을 생성 해야 한다는 것을 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-120">In the first pair, a user would have to know that the blog is displayed using the *blog.cshtml* page, and would then have to construct a query string that gets the right category or date range.</span></span> <span data-ttu-id="42bb7-121">두 번째 예제 집합은 이해 하 고 만드는 것이 훨씬 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-121">The second set of examples is much easier to comprehend and create.</span></span>

<span data-ttu-id="42bb7-122">또한 첫 번째 예제에 대 한 Url은 특정 파일 (*블로그. cshtml*)을 직접 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-122">The URLs for the first example also point directly to a specific file (*blog.cshtml*).</span></span> <span data-ttu-id="42bb7-123">어떤 이유로 든 블로그를 서버의 다른 폴더로 이동 했거나 다른 페이지를 사용 하도록 블로그를 다시 작성 한 경우 링크가 잘못 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-123">If for some reason the blog were moved to another folder on the server, or if the blog were rewritten to use a different page, the links would be wrong.</span></span> <span data-ttu-id="42bb7-124">두 번째 Url 집합은 특정 페이지를 가리키지 않으므로 블로그 구현이 나 위치가 변경 되더라도 Url은 여전히 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-124">The second set of URLs doesn't point to a specific page, so even if the blog implementation or location changes, the URLs would still be valid.</span></span>

<span data-ttu-id="42bb7-125">ASP.NET는 *라우팅을*사용 하므로 ASP.NET 웹 페이지에서 위의 예제와 같은 친숙 한 url을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-125">In ASP.NET Web Pages, you can create friendlier URLs like those in the above examples because ASP.NET uses *routing*.</span></span> <span data-ttu-id="42bb7-126">라우팅은 URL에서 요청을 수행할 수 있는 페이지 (또는 페이지)로의 논리적 매핑을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-126">Routing creates logical mapping from a URL to a page (or pages) that can fulfill the request.</span></span> <span data-ttu-id="42bb7-127">매핑은 논리적이 아닌 특정 파일에 대 한 논리적 이기 때문에 라우팅은 사이트의 Url을 정의 하는 방법에 뛰어난 유연성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-127">Because the mapping is logical (not physical, to a specific file), routing provides great flexibility in how you define the URLs for your site.</span></span>

## <a name="how-routing-works"></a><span data-ttu-id="42bb7-128">라우팅 작동 방법</span><span class="sxs-lookup"><span data-stu-id="42bb7-128">How Routing Works</span></span>

<span data-ttu-id="42bb7-129">ASP.NET에서 요청을 처리 하는 경우 URL을 읽어 라우팅하는 방법을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-129">When ASP.NET processes a request, it reads the URL to determine how to route it.</span></span> <span data-ttu-id="42bb7-130">ASP.NET는 URL의 개별 세그먼트를 디스크의 파일 (왼쪽에서 오른쪽으로 이동)과 일치 시 키 려 고 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-130">ASP.NET tries to match individual segments of the URL to files on disk, going from left to right.</span></span> <span data-ttu-id="42bb7-131">일치 하는 항목이 있으면 URL에 남아 있는 항목이 *경로 정보*로 페이지에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-131">If there's a match, anything remaining in the URL is passed to the page as *path information*.</span></span>

<span data-ttu-id="42bb7-132">누군가가 다음 URL을 사용 하 여 요청을 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-132">Imagine that someone makes a request using this URL:</span></span>

`http://www.contoso.com/a/b/c`

<span data-ttu-id="42bb7-133">검색은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-133">The search goes like this:</span></span>

1. <span data-ttu-id="42bb7-134">*/A/b/c.cshtml*경로와 이름을 가진 파일이 있나요?</span><span class="sxs-lookup"><span data-stu-id="42bb7-134">Is there a file with the path and name of */a/b/c.cshtml*?</span></span> <span data-ttu-id="42bb7-135">이 경우 해당 페이지를 실행 하 고 정보를 전달 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-135">If so, run that page and pass no information to it.</span></span> <span data-ttu-id="42bb7-136">기타...</span><span class="sxs-lookup"><span data-stu-id="42bb7-136">Otherwise ...</span></span>
2. <span data-ttu-id="42bb7-137">*/A/b.cshtml*경로와 이름을 가진 파일이 있나요?</span><span class="sxs-lookup"><span data-stu-id="42bb7-137">Is there a file with the path and name of */a/b.cshtml*?</span></span> <span data-ttu-id="42bb7-138">이 경우 해당 페이지를 실행 하 여 `c` 값을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-138">If so, run that page and pass the value `c` to it.</span></span> <span data-ttu-id="42bb7-139">그렇지 않은 경우 ...</span><span class="sxs-lookup"><span data-stu-id="42bb7-139">Otherwise …</span></span>
3. <span data-ttu-id="42bb7-140">*/A.cshtml*경로와 이름을 가진 파일이 있나요?</span><span class="sxs-lookup"><span data-stu-id="42bb7-140">Is there a file with the path and name of */a.cshtml*?</span></span> <span data-ttu-id="42bb7-141">이 경우 해당 페이지를 실행 하 여 `b/c` 값을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-141">If so, run that page and pass the value `b/c` to it.</span></span>

<span data-ttu-id="42bb7-142">지정 된 폴더에 있는 ASP.NET 파일에 *대해 정확* 하 게 일치 하는 항목이 검색에서 발견 된 경우에는 해당 파일을 계속 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-142">If the search found no exact matches for *.cshtml* files in their specified folders, ASP.NET continues looking for these files in turn:</span></span>

1. <span data-ttu-id="42bb7-143">*/a/b/c/default.cshtml* (경로 정보 없음).</span><span class="sxs-lookup"><span data-stu-id="42bb7-143">*/a/b/c/default.cshtml* (no path information).</span></span>
2. <span data-ttu-id="42bb7-144">*/a/b/c/index.cshtml* (경로 정보 없음).</span><span class="sxs-lookup"><span data-stu-id="42bb7-144">*/a/b/c/index.cshtml* (no path information).</span></span>

> [!NOTE]
> <span data-ttu-id="42bb7-145">명확 하 게 하기 위해 특정 페이지에 대 한 요청 (즉 *, 파일 확장명을 포함* 하는 요청)은 예상한 것과 똑같이 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-145">To be clear, requests for specific pages (that is, requests that include the *.cshtml* filename extension) work just like you'd expect.</span></span> <span data-ttu-id="42bb7-146">`http://www.contoso.com/a/b.cshtml` 같은 요청은 b 페이지를 실행 합니다 *.*</span><span class="sxs-lookup"><span data-stu-id="42bb7-146">A request like `http://www.contoso.com/a/b.cshtml` will run the page *b.cshtml* just fine.</span></span>

<span data-ttu-id="42bb7-147">페이지 내에서 페이지의 `UrlData` 속성 (사전)을 통해 경로 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-147">Inside a page, you can get the path information via the page's `UrlData` property, which is a dictionary.</span></span> <span data-ttu-id="42bb7-148">이름이 *Viewcustomers* 인 파일이 있고 사이트에서이 요청을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-148">Imagine that you have a file named *ViewCustomers.cshtml* and your site gets this request:</span></span>

`http://mysite.com/myWebSite/ViewCustomers/1000`

<span data-ttu-id="42bb7-149">위의 규칙에 설명 된 대로 요청이 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-149">As described in the rules above, the request will go to your page.</span></span> <span data-ttu-id="42bb7-150">페이지 내에서 다음과 같은 코드를 사용 하 여 경로 정보를 가져오고 표시할 수 있습니다 (이 경우 값 &quot;1000&quot;).</span><span class="sxs-lookup"><span data-stu-id="42bb7-150">Inside the page, you can use code like the following to get and display the path information (in this case, the value &quot;1000&quot;):</span></span>

[!code-html[Main](creating-readable-urls-in-aspnet-web-pages-sites/samples/sample1.html)]

> [!NOTE]
> <span data-ttu-id="42bb7-151">라우팅은 전체 파일 이름을 포함 하지 않으므로 이름이 같지만 파일 이름 확장명 (예: *m* 및 *m*)이 다른 페이지가 있는 경우 모호성이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-151">Because routing doesn't involve complete file names, there can be ambiguity if you have pages that have the same name but different file-name extensions (for example, *MyPage.cshtml* and *MyPage.html*).</span></span> <span data-ttu-id="42bb7-152">라우팅 문제를 방지 하기 위해 사이트에 이름이 서로 다른 페이지가 없는지 확인 하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-152">In order to avoid problems with routing, it's best to make sure that you don't have pages in your site whose names differ only in their extension.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="42bb7-153">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="42bb7-153">Additional Resources</span></span>

<span data-ttu-id="42bb7-154">[WebMatrix-url, UrlData 및 SEO에 대 한 라우팅](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO)입니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-154">[WebMatrix - URLs, UrlData and Routing for SEO](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO).</span></span> <span data-ttu-id="42bb7-155">Mike Brind의이 블로그 항목에서는 ASP.NET 웹 페이지에서 라우팅의 작동 방식에 대 한 추가 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="42bb7-155">This blog entry by Mike Brind provides some additional details on how routing works in ASP.NET Web Pages.</span></span>
