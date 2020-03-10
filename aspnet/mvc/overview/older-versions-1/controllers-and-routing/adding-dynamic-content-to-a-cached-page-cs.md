---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
title: 캐시 된 페이지에 동적 콘텐츠 추가 (C#) | Microsoft Docs
author: microsoft
description: 동일한 페이지에서 동적 및 캐시 된 콘텐츠를 혼합 하는 방법에 대해 알아봅니다. 캐시 후 대체를 사용 하 여 배너 광고 o와 같은 동적 콘텐츠를 표시할 수 있습니다.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 2ddd4407-d143-4a94-877c-21771bfb97a6
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
msc.type: authoredcontent
ms.openlocfilehash: be43712d3dd5235117558e991d9dd71aa30ec470
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486941"
---
# <a name="adding-dynamic-content-to-a-cached-page-c"></a><span data-ttu-id="26dae-104">캐시된 페이지에 동적 콘텐츠 추가(C#)</span><span class="sxs-lookup"><span data-stu-id="26dae-104">Adding Dynamic Content to a Cached Page (C#)</span></span>

<span data-ttu-id="26dae-105">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="26dae-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="26dae-106">동일한 페이지에서 동적 및 캐시 된 콘텐츠를 혼합 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-106">Learn how to mix dynamic and cached content in the same page.</span></span> <span data-ttu-id="26dae-107">캐시 후 대체를 사용 하면 출력이 캐시 된 페이지 내에서 배너 광고 또는 뉴스 항목과 같은 동적 콘텐츠를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-107">Post-cache substitution enables you to display dynamic content, such as banner advertisements or news items, within a page that has been output cached.</span></span>

<span data-ttu-id="26dae-108">출력 캐싱을 활용 하면 ASP.NET MVC 응용 프로그램의 성능을 크게 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-108">By taking advantage of output caching, you can dramatically improve the performance of an ASP.NET MVC application.</span></span> <span data-ttu-id="26dae-109">페이지가 요청 될 때마다 페이지를 다시 생성 하는 대신 페이지를 한 번 생성 하 고 여러 사용자를 위해 메모리에 캐시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-109">Instead of regenerating a page each and every time the page is requested, the page can be generated once and cached in memory for multiple users.</span></span>

<span data-ttu-id="26dae-110">하지만 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-110">But there is a problem.</span></span> <span data-ttu-id="26dae-111">페이지에 동적 콘텐츠를 표시 해야 하는 경우 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="26dae-111">What if you need to display dynamic content in the page?</span></span> <span data-ttu-id="26dae-112">예를 들어 페이지에 배너 광고를 표시 하려고 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-112">For example, imagine that you want to display a banner advertisement in the page.</span></span> <span data-ttu-id="26dae-113">모든 사용자가 동일한 보급 알림을 볼 수 있도록 배너 보급 알림이 캐시 되는 것을 원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-113">You don't want the banner advertisement to be cached so that every user sees the very same advertisement.</span></span> <span data-ttu-id="26dae-114">그렇게 하는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-114">You wouldn't make any money that way!</span></span>

<span data-ttu-id="26dae-115">다행히 쉬운 솔루션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-115">Fortunately, there is an easy solution.</span></span> <span data-ttu-id="26dae-116">*사후 캐시 대체*라는 ASP.NET 프레임 워크의 기능을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-116">You can take advantage of a feature of the ASP.NET framework called *post-cache substitution*.</span></span> <span data-ttu-id="26dae-117">캐시 후 대체를 사용 하 여 메모리에 캐시 된 페이지에서 동적 콘텐츠를 대체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-117">Post-cache substitution enables you to substitute dynamic content in a page that has been cached in memory.</span></span>

<span data-ttu-id="26dae-118">일반적으로 [OutputCache] 특성을 사용 하 여 페이지 캐시를 출력 하면 페이지가 서버와 클라이언트 (웹 브라우저) 모두에 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-118">Normally, when you output cache a page by using the [OutputCache] attribute, the page is cached on both the server and the client (the web browser).</span></span> <span data-ttu-id="26dae-119">사후 캐시 대체를 사용 하는 경우 페이지는 서버에만 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-119">When you use post-cache substitution, a page is cached only on the server.</span></span>

#### <a name="using-post-cache-substitution"></a><span data-ttu-id="26dae-120">사후 캐시 대체 사용</span><span class="sxs-lookup"><span data-stu-id="26dae-120">Using Post-Cache Substitution</span></span>

<span data-ttu-id="26dae-121">사후 캐시 대체를 사용 하려면 두 단계가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-121">Using post-cache substitution requires two steps.</span></span> <span data-ttu-id="26dae-122">먼저 캐시 된 페이지에 표시 하려는 동적 콘텐츠를 나타내는 문자열을 반환 하는 메서드를 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-122">First, you need to define a method that returns a string that represents the dynamic content that you want to display in the cached page.</span></span> <span data-ttu-id="26dae-123">다음으로 Httpresponse.cache () 메서드를 호출 하 여 페이지에 동적 콘텐츠를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-123">Next, you call the HttpResponse.WriteSubstitution() method to inject the dynamic content into the page.</span></span>

<span data-ttu-id="26dae-124">예를 들어 캐시 된 페이지에 다른 뉴스 항목을 임의로 표시 하려는 경우를 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-124">Imagine, for example, that you want to randomly display different news items in a cached page.</span></span> <span data-ttu-id="26dae-125">목록 1의 클래스는 RenderNews () 라는 단일 메서드를 노출 하 여 세 개의 뉴스 항목 목록에서 뉴스 항목 하나를 임의로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-125">The class in Listing 1 exposes a single method, named RenderNews(), that randomly returns one news item from a list of three news items.</span></span>

<span data-ttu-id="26dae-126">**목록 1 – Models\News.cs**</span><span class="sxs-lookup"><span data-stu-id="26dae-126">**Listing 1 – Models\News.cs**</span></span>

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample1.cs)]

<span data-ttu-id="26dae-127">사후 캐시 대체를 활용 하려면 WriteSubstitution () 메서드를 호출 Httpresponse.cache.</span><span class="sxs-lookup"><span data-stu-id="26dae-127">To take advantage of post-cache substitution, you call the HttpResponse.WriteSubstitution() method.</span></span> <span data-ttu-id="26dae-128">WriteSubstitution () 메서드는 캐시 된 페이지의 영역을 동적 콘텐츠로 바꾸도록 코드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-128">The WriteSubstitution() method sets up the code to replace a region of the cached page with dynamic content.</span></span> <span data-ttu-id="26dae-129">WriteSubstitution () 메서드는 목록 2의 보기에 임의의 뉴스 항목을 표시 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-129">The WriteSubstitution() method is used to display the random news item in the view in Listing 2.</span></span>

<span data-ttu-id="26dae-130">**목록 2 – Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="26dae-130">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample2.aspx)]

<span data-ttu-id="26dae-131">RenderNews 메서드는 WriteSubstitution () 메서드에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-131">The RenderNews method is passed to the WriteSubstitution() method.</span></span> <span data-ttu-id="26dae-132">RenderNews 메서드는 호출 되지 않습니다 (괄호 없음).</span><span class="sxs-lookup"><span data-stu-id="26dae-132">Notice that the RenderNews method is not called (there are no parentheses).</span></span> <span data-ttu-id="26dae-133">대신 메서드에 대 한 참조는 WriteSubstitution ()에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-133">Instead a reference to the method is passed to WriteSubstitution().</span></span>

<span data-ttu-id="26dae-134">인덱스 뷰가 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-134">The Index view is cached.</span></span> <span data-ttu-id="26dae-135">뷰는 컨트롤러에서 목록 3에 의해 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-135">The view is returned by the controller in Listing 3.</span></span> <span data-ttu-id="26dae-136">Index () 동작은 인덱스 보기가 60 초 동안 캐시 되도록 하는 [OutputCache] 특성으로 데코 레이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-136">Notice that the Index() action is decorated with an [OutputCache] attribute that causes the Index view to be cached for 60 seconds.</span></span>

<span data-ttu-id="26dae-137">**목록 3 – Controllers\ homecontroller.cs**</span><span class="sxs-lookup"><span data-stu-id="26dae-137">**Listing 3 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample3.cs)]

<span data-ttu-id="26dae-138">인덱스 뷰가 캐시 된 경우에도 인덱스 페이지를 요청 하면 다른 임의의 뉴스 항목이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-138">Even though the Index view is cached, different random news items are displayed when you request the Index page.</span></span> <span data-ttu-id="26dae-139">인덱스 페이지를 요청 하는 경우 페이지에 표시 되는 시간은 60 초 동안 변경 되지 않습니다 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="26dae-139">When you request the Index page, the time displayed by the page does not change for 60 seconds (see Figure 1).</span></span> <span data-ttu-id="26dae-140">시간이 변경 되지 않는다는 사실은 페이지가 캐시 되었음을 증명 합니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-140">The fact that the time does not change proves that the page is cached.</span></span> <span data-ttu-id="26dae-141">그러나 WriteSubstitution () 메서드에 의해 삽입 된 콘텐츠 (임의 뉴스 항목)는 각 요청과 함께 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-141">However, the content injected by the WriteSubstitution() method – the random news item – changes with each request .</span></span>

<span data-ttu-id="26dae-142">**그림 1-캐시 된 페이지에 동적 뉴스 항목 삽입**</span><span class="sxs-lookup"><span data-stu-id="26dae-142">**Figure 1 – Injecting dynamic news items in a cached page**</span></span>

![clip_image002](adding-dynamic-content-to-a-cached-page-cs/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a><span data-ttu-id="26dae-144">도우미 메서드에서 캐시 후 대체 사용</span><span class="sxs-lookup"><span data-stu-id="26dae-144">Using Post-Cache Substitution in Helper Methods</span></span>

<span data-ttu-id="26dae-145">사후 캐시 대체를 활용 하는 보다 쉬운 방법은 사용자 지정 도우미 메서드 내에서 WriteSubstitution () 메서드에 대 한 호출을 캡슐화 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-145">An easier way to take advantage of post-cache substitution is to encapsulate the call to the WriteSubstitution() method within a custom helper method.</span></span> <span data-ttu-id="26dae-146">이 방법은 목록 4의 도우미 메서드에 의해 설명 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-146">This approach is illustrated by the helper method in Listing 4.</span></span>

<span data-ttu-id="26dae-147">**목록 4 – AdHelper.cs**</span><span class="sxs-lookup"><span data-stu-id="26dae-147">**Listing 4 – AdHelper.cs**</span></span>

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample4.cs)]

<span data-ttu-id="26dae-148">목록 4에는 RenderBanner ()와 RenderBannerInternal () 라는 두 개의 메서드를 노출 하는 정적 클래스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-148">Listing 4 contains a static class that exposes two methods: RenderBanner() and RenderBannerInternal().</span></span> <span data-ttu-id="26dae-149">RenderBanner () 메서드는 실제 도우미 메서드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-149">The RenderBanner() method represents the actual helper method.</span></span> <span data-ttu-id="26dae-150">이 메서드는 다른 도우미 메서드와 마찬가지로 뷰에서 Html RenderBanner ()를 호출할 수 있도록 표준 ASP.NET MVC HtmlHelper 클래스를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-150">This method extends the standard ASP.NET MVC HtmlHelper class so that you can call Html.RenderBanner() in a view just like any other helper method.</span></span>

<span data-ttu-id="26dae-151">RenderBanner () 메서드는 RenderBannerInternal () 메서드를 WriteSubstitution () 메서드에 전달 하는 WriteSubstitution () 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-151">The RenderBanner() method calls the HttpResponse.WriteSubstitution() method passing the RenderBannerInternal() method to the WriteSubstitution() method.</span></span>

<span data-ttu-id="26dae-152">RenderBannerInternal () 메서드는 전용 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-152">The RenderBannerInternal() method is a private method.</span></span> <span data-ttu-id="26dae-153">이 메서드는 도우미 메서드로 노출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-153">This method won't be exposed as a helper method.</span></span> <span data-ttu-id="26dae-154">RenderBannerInternal () 메서드는 세 개의 배너 광고 이미지 목록에서 하나의 배너 광고 이미지를 임의로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-154">The RenderBannerInternal() method randomly returns one banner advertisement image from a list of three banner advertisement images.</span></span>

<span data-ttu-id="26dae-155">목록 5의 수정 된 인덱스 뷰는 RenderBanner () 도우미 메서드를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-155">The modified Index view in Listing 5 illustrates how you can use the RenderBanner() helper method.</span></span> <span data-ttu-id="26dae-156">MvcApplication1 네임 스페이스를 가져오기 위해 추가 &lt;% @ Import%&gt; 지시어가 뷰의 맨 위에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-156">Notice that an additional &lt;%@ Import %&gt; directive is included at the top of the view to import the MvcApplication1.Helpers namespace.</span></span> <span data-ttu-id="26dae-157">이 네임 스페이스를 가져오지 않는 경우 RenderBanner () 메서드는 Html 속성에 메서드로 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-157">If you neglect to import this namespace, then the RenderBanner() method won't appear as a method on the Html property.</span></span>

<span data-ttu-id="26dae-158">**목록 5 – Views\Home\Index.aspx (RenderBanner () 메서드 포함)**</span><span class="sxs-lookup"><span data-stu-id="26dae-158">**Listing 5 – Views\Home\Index.aspx (with RenderBanner() method)**</span></span>

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample5.aspx)]

<span data-ttu-id="26dae-159">목록 5에서 보기에 의해 렌더링 된 페이지를 요청 하면 각 요청과 함께 다른 배너 알림이 표시 됩니다 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="26dae-159">When you request the page rendered by the view in Listing 5, a different banner advertisement is displayed with each request (see Figure 2).</span></span> <span data-ttu-id="26dae-160">페이지가 캐시 되지만 배너 보급 알림은 RenderBanner () 도우미 메서드에 의해 동적으로 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-160">The page is cached, but the banner advertisement is injected dynamically by the RenderBanner() helper method.</span></span>

<span data-ttu-id="26dae-161">**그림 2 – 무작위 배너 광고를 표시 하는 인덱스 뷰**</span><span class="sxs-lookup"><span data-stu-id="26dae-161">**Figure 2 – The Index view displaying a random banner advertisement**</span></span>

![clip_image004](adding-dynamic-content-to-a-cached-page-cs/_static/image2.jpg)

#### <a name="summary"></a><span data-ttu-id="26dae-163">요약</span><span class="sxs-lookup"><span data-stu-id="26dae-163">Summary</span></span>

<span data-ttu-id="26dae-164">이 자습서에서는 캐시 된 페이지의 콘텐츠를 동적으로 업데이트 하는 방법에 대해 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-164">This tutorial explained how you can dynamically update content in a cached page.</span></span> <span data-ttu-id="26dae-165">WriteSubstitution () 메서드를 사용 하 여 캐시 된 페이지에 동적 콘텐츠를 삽입할 수 있도록 설정 하는 방법을 배웠습니다 Httpresponse.cache.</span><span class="sxs-lookup"><span data-stu-id="26dae-165">You learned how to use the HttpResponse.WriteSubstitution() method to enable dynamic content to be injected in a cached page.</span></span> <span data-ttu-id="26dae-166">또한 HTML 도우미 메서드 내에서 WriteSubstitution () 메서드에 대 한 호출을 캡슐화 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-166">You also learned how to encapsulate the call to the WriteSubstitution() method within an HTML helper method.</span></span>

<span data-ttu-id="26dae-167">가능 하면 캐시 활용 – 웹 응용 프로그램의 성능에 큰 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-167">Take advantage of caching whenever possible – it can have a dramatic impact on the performance of your web applications.</span></span> <span data-ttu-id="26dae-168">이 자습서에 설명 된 대로 페이지에 동적 콘텐츠를 표시 해야 하는 경우에도 캐싱을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26dae-168">As explained in this tutorial, you can take advantage of caching even when you need to display dynamic content in your pages.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="26dae-169">[이전](improving-performance-with-output-caching-cs.md)
> [다음](creating-a-controller-cs.md)</span><span class="sxs-lookup"><span data-stu-id="26dae-169">[Previous](improving-performance-with-output-caching-cs.md)
[Next](creating-a-controller-cs.md)</span></span>
