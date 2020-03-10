---
uid: web-pages/overview/performance-and-traffic/14-analyzing-traffic
title: ASP.NET 웹 페이지 (Razor) 사이트의 방문자 정보 (분석) 추적 | Microsoft Docs
author: Rick-Anderson
description: 웹 사이트를 시작한 후 웹 사이트 트래픽을 분석할 수 있습니다.
ms.author: riande
ms.date: 02/17/2014
ms.assetid: 360bc6e1-84c5-4b8e-a84c-ea48ab807aa4
msc.legacyurl: /web-pages/overview/performance-and-traffic/14-analyzing-traffic
msc.type: authoredcontent
ms.openlocfilehash: 095a5572c755446e0661c052ca9de82d636429fd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421457"
---
# <a name="tracking-visitor-information-analytics-for-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="e8497-103">ASP.NET 웹 페이지 (Razor) 사이트의 방문자 정보 (분석) 추적</span><span class="sxs-lookup"><span data-stu-id="e8497-103">Tracking Visitor Information (Analytics) for an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="e8497-104">만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="e8497-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="e8497-105">이 문서에서는 도우미를 사용 하 여 ASP.NET 웹 페이지 (Razor) 웹 사이트의 페이지에 웹 사이트 분석을 추가 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-105">This article describes how to use a helper to add website analytics to pages in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="e8497-106">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="e8497-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="e8497-107">웹 사이트 트래픽에 대 한 정보를 분석 공급자에 게 보내는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-107">How to send information about your website traffic to an analytics provider.</span></span>
> 
> <span data-ttu-id="e8497-108">다음은이 문서에 도입 된 ASP.NET 프로그래밍 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-108">These are the ASP.NET programming features introduced in the article:</span></span>
> 
> - <span data-ttu-id="e8497-109">`Analytics` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-109">The `Analytics` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="e8497-110">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="e8497-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="e8497-111">ASP.NET 웹 페이지 (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="e8497-111">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="e8497-112">ASP.NET 웹 도우미 라이브러리 (NuGet 패키지)</span><span class="sxs-lookup"><span data-stu-id="e8497-112">ASP.NET Web Helpers Library (NuGet package)</span></span>

<span data-ttu-id="e8497-113">분석은 사용자가 사이트를 사용 하는 방법을 이해할 수 있도록 웹 사이트의 트래픽을 측정 하는 기술의 일반적인 용어입니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-113">Analytics is a general term for technology that measures traffic on your website so you can understand how people use the site.</span></span> <span data-ttu-id="e8497-114">Google, Yahoo, StatCounter 등의 서비스를 비롯 한 많은 분석 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-114">Many analytics services are available, including services from Google, Yahoo, StatCounter, and others.</span></span>

<span data-ttu-id="e8497-115">분석의 작동 방식은 추적 하려는 사이트를 등록 하는 분석 공급자를 사용 하 여 계정을 등록 하는 것입니다. 공급자는 사용자 계정에 대 한 ID 또는 추적 코드를 포함 하는 JavaScript 코드의 코드 조각을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-115">The way analytics works is that you sign up for an account with the analytics provider, where you register the site that you want to track. The provider sends you a snippet of JavaScript code that includes an ID or tracking code for your account.</span></span> <span data-ttu-id="e8497-116">추적 하려는 사이트의 웹 페이지에 JavaScript 코드 조각을 추가 합니다. 일반적으로 사이트의 모든 페이지에 표시 되는 바닥글 또는 레이아웃 페이지나 기타 HTML 태그에 분석 코드 조각을 추가 합니다. 사용자가 이러한 JavaScript 코드 조각 중 하나를 포함 하는 페이지를 요청 하면 코드 조각에서 현재 페이지에 대 한 정보를 분석 공급자에 게 보내고,이는 페이지에 대 한 다양 한 세부 정보를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-116">You add the JavaScript snippet to the web pages on the site that you want to track. (You typically add the analytics snippet to a footer or layout page or other HTML markup that appears on every page in your site.) When users request a page that contains one of these JavaScript snippets, the snippet sends information about the current page to the analytics provider, who records various details about the page.</span></span>

<span data-ttu-id="e8497-117">사이트 통계를 확인 하려는 경우 분석 공급자의 웹 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-117">When you want to have a look at your site statistics, you log into the analytics provider's website.</span></span> <span data-ttu-id="e8497-118">그러면 다음과 같이 사이트에 대 한 모든 종류의 보고서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-118">You can then view all sorts of reports about your site, like:</span></span>

- <span data-ttu-id="e8497-119">개별 페이지에 대 한 페이지 보기 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-119">The number of page views for individual pages.</span></span> <span data-ttu-id="e8497-120">이를 통해 사이트를 방문 하는 사용자 수와 사이트의 가장 인기 있는 페이지를 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-120">This tells you (roughly) how many people are visiting the site, and which pages on your site are the most popular.</span></span>
- <span data-ttu-id="e8497-121">사용자가 특정 페이지에 소비 하는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-121">How long people spend on specific pages.</span></span> <span data-ttu-id="e8497-122">이를 통해 홈 페이지에서 사용자의 관심을 유지 하는지 여부를 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-122">This can tell you things like whether your home page is keeping people's interest.</span></span>
- <span data-ttu-id="e8497-123">사용자가 사이트를 방문 하기 전에 방문한 사이트</span><span class="sxs-lookup"><span data-stu-id="e8497-123">What sites people were on before they visited your site.</span></span> <span data-ttu-id="e8497-124">이를 통해 트래픽이 링크에서 제공 되는지 검색에서 전송 되는지 여부를 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-124">This helps you understand whether your traffic is coming from links, from searches, and so on.</span></span>
- <span data-ttu-id="e8497-125">사용자가 사이트를 방문 하는 경우와 기간을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-125">When people visit your site and how long they stay.</span></span>
- <span data-ttu-id="e8497-126">방문자가 있는 국가</span><span class="sxs-lookup"><span data-stu-id="e8497-126">What countries your visitors are from.</span></span>
- <span data-ttu-id="e8497-127">방문자가 사용 하는 브라우저 및 운영 체제</span><span class="sxs-lookup"><span data-stu-id="e8497-127">What browsers and operating systems your visitors are using.</span></span>

    ![Ch14traffic-1](14-analyzing-traffic/_static/image1.jpg)

## <a name="using-a-helper-to-add-analytics-to-a-page"></a><span data-ttu-id="e8497-129">도우미를 사용 하 여 페이지에 분석 추가</span><span class="sxs-lookup"><span data-stu-id="e8497-129">Using a Helper to Add Analytics to a Page</span></span>

<span data-ttu-id="e8497-130">ASP.NET 웹 페이지에는 분석에 사용 되는 JavaScript 코드 조각을 쉽게 관리할 수 있게 해 주는 여러 분석 도우미 (`Analytics.GetGoogleHtml`, `Analytics.GetYahooHtml`및 `Analytics.GetStatCounterHtml`)가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-130">ASP.NET Web Pages includes several analytics helpers (`Analytics.GetGoogleHtml`, `Analytics.GetYahooHtml`, and `Analytics.GetStatCounterHtml`) that make it easy to manage the JavaScript snippets used for analytics.</span></span> <span data-ttu-id="e8497-131">JavaScript 코드를 넣는 방법과 위치를 파악 하는 대신, 페이지에 도우미를 추가 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-131">Instead of figuring out how and where to put the JavaScript code, all you have to do is add the helper to a page.</span></span> <span data-ttu-id="e8497-132">제공 해야 하는 유일한 정보는 계정 이름, ID 또는 추적 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-132">The only information you need to provide is your account name, ID, or tracking code.</span></span> <span data-ttu-id="e8497-133">StatCounter의 경우 몇 가지 추가 값도 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-133">(For StatCounter, you also have to provide a few additional values.)</span></span>

<span data-ttu-id="e8497-134">이 절차에서는 `GetGoogleHtml` 도우미를 사용 하는 레이아웃 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-134">In this procedure, you'll create a layout page that uses the `GetGoogleHtml` helper.</span></span> <span data-ttu-id="e8497-135">다른 분석 공급자 중 하나를 사용 하는 계정이 이미 있는 경우 해당 계정을 대신 사용 하 고 필요에 따라 약간의 조정을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-135">If you already have an account with one of the other analytics providers, you can use that account instead and make slight adjustments as needed.</span></span>

> [!NOTE]
> <span data-ttu-id="e8497-136">분석 계정을 만들 때 추적 하려는 사이트의 URL을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-136">When you create an analytics account, you register the URL of the site that you want to be tracking.</span></span> <span data-ttu-id="e8497-137">로컬 컴퓨터의 모든 항목을 테스트 하는 경우 실제 트래픽 (유일한 트래픽)을 추적 하지 않으므로 사이트 통계를 기록 하 고 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-137">If you're testing everything on your local computer, you won't be tracking actual traffic (the only traffic is you), so you won't be able to record and view site statistics.</span></span> <span data-ttu-id="e8497-138">그러나이 절차에서는 페이지에 분석 도우미를 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-138">But this procedure shows how you add an analytics helper to a page.</span></span> <span data-ttu-id="e8497-139">사이트를 게시 하는 경우 라이브 사이트는 분석 공급자에 게 정보를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-139">When you publish your site, the live site will send information to your analytics provider.</span></span>

1. <span data-ttu-id="e8497-140">[ASP.NET 웹 페이지 사이트에 도우미 설치](https://go.microsoft.com/fwlink/?LinkId=252372)의 설명에 따라 웹 사이트에 ASP.NET 웹 도우미 라이브러리를 추가 합니다 (아직 추가 하지 않은 경우).</span><span class="sxs-lookup"><span data-stu-id="e8497-140">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.</span></span>
2. <span data-ttu-id="e8497-141">Google Analytics를 사용 하 여 계정을 만들고 계정 이름을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-141">Create an account with Google Analytics and record the account name.</span></span>
3. <span data-ttu-id="e8497-142">*Analytics. cshtml* 이라는 레이아웃 페이지를 만들고 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-142">Create a layout page named *Analytics.cshtml* and add the following markup:</span></span>

    [!code-cshtml[Main](14-analyzing-traffic/samples/sample1.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="e8497-143">`</body>` 태그 앞에 있는 웹 페이지의 본문에 `Analytics` 도우미에 대 한 호출을 넣어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-143">You must place the call to the `Analytics` helper in the body of your web page (before the `</body>` tag).</span></span> <span data-ttu-id="e8497-144">그렇지 않으면 브라우저가 스크립트를 실행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-144">Otherwise, the browser will not run the script.</span></span>

    <span data-ttu-id="e8497-145">다른 분석 공급자를 사용 하는 경우 대신 다음 도우미 중 하나를 사용 하세요.</span><span class="sxs-lookup"><span data-stu-id="e8497-145">If you're using a different analytics provider, use one of the following helpers instead:</span></span>

    - <span data-ttu-id="e8497-146">(Yahoo) `@Analytics.GetYahooHtml("myaccount")`</span><span class="sxs-lookup"><span data-stu-id="e8497-146">(Yahoo) `@Analytics.GetYahooHtml("myaccount")`</span></span>
    - <span data-ttu-id="e8497-147">(StatCounter) `@Analytics.GetStatCounterHtml("project", "security")`</span><span class="sxs-lookup"><span data-stu-id="e8497-147">(StatCounter) `@Analytics.GetStatCounterHtml("project", "security")`</span></span>
4. <span data-ttu-id="e8497-148">`myaccount`을 1 단계에서 만든 계정, ID 또는 추적 코드의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-148">Replace `myaccount` with the name of the account, ID, or tracking code that you created in step 1.</span></span>
5. <span data-ttu-id="e8497-149">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-149">Run the page in the browser.</span></span> <span data-ttu-id="e8497-150">(파일을 실행 하기 전에 해당 페이지가 **파일** 작업 영역에서 선택 되어 있는지 확인 합니다.)</span><span class="sxs-lookup"><span data-stu-id="e8497-150">(Make sure the page is selected in the **Files** workspace before you run it.)</span></span>
6. <span data-ttu-id="e8497-151">브라우저에서 페이지 소스를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-151">In the browser, view the page source.</span></span> <span data-ttu-id="e8497-152">렌더링 된 분석 코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-152">You'll be able to see the rendered analytics code:</span></span>

    [!code-html[Main](14-analyzing-traffic/samples/sample2.html)]
7. <span data-ttu-id="e8497-153">Google 분석 사이트에 로그인 하 고 사이트에 대 한 통계를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-153">Log onto the Google Analytics site and examine the statistics for your site.</span></span> <span data-ttu-id="e8497-154">라이브 사이트에서 페이지를 실행 하는 경우 페이지 방문을 기록 하는 항목이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8497-154">If you're running the page on a live site, you see an entry that logs the visit to your page.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="e8497-155">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="e8497-155">Additional Resources</span></span>

- [<span data-ttu-id="e8497-156">Google 분석 사이트</span><span class="sxs-lookup"><span data-stu-id="e8497-156">Google Analytics site</span></span>](https://www.google.com/analytics/)
- [<span data-ttu-id="e8497-157">Yahoo! 웹 분석 사이트</span><span class="sxs-lookup"><span data-stu-id="e8497-157">Yahoo! Web Analytics site</span></span>](http://help.yahoo.com/l/us/yahoo/ywa/)
- [<span data-ttu-id="e8497-158">StatCounter 사이트</span><span class="sxs-lookup"><span data-stu-id="e8497-158">StatCounter site</span></span>](http://statcounter.com/)
