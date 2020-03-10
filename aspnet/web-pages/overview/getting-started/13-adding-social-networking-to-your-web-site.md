---
uid: web-pages/overview/getting-started/13-adding-social-networking-to-your-web-site
title: ASP.NET 웹 페이지 (Razor) 사이트에 소셜 네트워킹 추가 | Microsoft Docs
author: Rick-Anderson
description: 이 장에서는 소셜 네트워킹 서비스와 사이트를 통합 하는 방법에 대해 설명 합니다. 이 장에서 사용자는 웹 사이트에 책갈피를 지정 하 고 연결 하는 방법을 배웁니다.
ms.author: riande
ms.date: 02/21/2014
ms.assetid: 03c342f9-b35c-4d7c-b9ed-cd9aaaffedb6
msc.legacyurl: /web-pages/overview/getting-started/13-adding-social-networking-to-your-web-site
msc.type: authoredcontent
ms.openlocfilehash: 1637464b0473bba8133acbbf8918d92b4f552701
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422957"
---
# <a name="adding-social-networking-to-aspnet-web-pages-razor-sites"></a><span data-ttu-id="dcbd7-104">ASP.NET 웹 페이지 (Razor) 사이트에 소셜 네트워킹 추가</span><span class="sxs-lookup"><span data-stu-id="dcbd7-104">Adding Social Networking to ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="dcbd7-105">만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="dcbd7-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="dcbd7-106">이 문서에서는 ASP.NET 웹 페이지 (Razor) 웹 사이트의 페이지에 Facebook, Twitter, Reddit 및 Digg에 대 한 소셜 네트워킹 링크를 추가 하는 방법과 Twitter 피드, Xbox 게이머 카드 및 Gravatar 이미지를 포함 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-106">This article explains how to add social networking links for Facebook, Twitter, Reddit, and Digg to pages in an ASP.NET Web Pages (Razor) website, and how to include Twitter feeds, Xbox gamer cards, and Gravatar images.</span></span>
> 
> <span data-ttu-id="dcbd7-107">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="dcbd7-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="dcbd7-108">사용자가 사이트에 책갈피를 지정 하 고 연결 하도록 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-108">How to let people bookmark/link your site.</span></span>
> - <span data-ttu-id="dcbd7-109">Twitter 피드를 추가 하는 방법</span><span class="sxs-lookup"><span data-stu-id="dcbd7-109">How to add a Twitter feed.</span></span>
> - <span data-ttu-id="dcbd7-110">페이지에 Facebook **Like** 단추를 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-110">How to add a Facebook **Like** button to pages.</span></span>
> - <span data-ttu-id="dcbd7-111">Gravatar.com 이미지를 렌더링 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-111">How to render Gravatar.com images.</span></span>
> - <span data-ttu-id="dcbd7-112">사이트에서 Xbox 게이머 카드를 표시 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-112">How to display an Xbox gamer card on your site.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="dcbd7-113">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="dcbd7-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="dcbd7-114">ASP.NET 웹 페이지 (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="dcbd7-114">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="dcbd7-115">ASP.NET 웹 도우미 라이브러리 (NuGet 패키지)</span><span class="sxs-lookup"><span data-stu-id="dcbd7-115">ASP.NET Web Helper Library (NuGet package)</span></span>
>   
> 
> <span data-ttu-id="dcbd7-116">이 자습서는 ASP.NET 웹 도우미 라이브러리를 사용 하는 파트를 제외 하 고는 ASP.NET 웹 페이지 3 에서도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-116">This tutorial also works with ASP.NET Web Pages 3, except for parts that use the ASP.NET Web Helper Library.</span></span>

<a id="Linking_Your_Website"></a>
## <a name="linking-your-website-on-social-networking-sites"></a><span data-ttu-id="dcbd7-117">소셜 네트워킹 사이트에서 웹 사이트 연결</span><span class="sxs-lookup"><span data-stu-id="dcbd7-117">Linking Your Website on Social Networking Sites</span></span>

<span data-ttu-id="dcbd7-118">사용자가 사이트에서 무언가를 사용 하는 경우 친구와 공유 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-118">If people like something on your site, they often want to share it with friends.</span></span> <span data-ttu-id="dcbd7-119">사용자가 클릭 하 여 Digg, Reddit, Facebook, Twitter 또는 유사한 사이트의 페이지를 공유할 수 있는 문자 모양 (아이콘)을 표시 하 여이 작업을 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-119">You can make this easy by displaying glyphs (icons) that people can click to share a page on Digg, Reddit, Facebook, Twitter, or similar sites.</span></span>

<span data-ttu-id="dcbd7-120">이러한 문자 모양을 표시 하려면 페이지에 `LinkSharecode` 도우미를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-120">To display these glyphs, add the `LinkSharecode` helper to a page.</span></span> <span data-ttu-id="dcbd7-121">페이지를 방문 하는 사람은 개별 문자 모양을 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-121">People who visit your page can click an individual glyph.</span></span> <span data-ttu-id="dcbd7-122">해당 소셜 네트워킹 사이트의 계정이 있는 경우 해당 사이트의 페이지에 대 한 링크를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-122">If they have an account with that social networking site, they can then post a link to your page on that site.</span></span>

![그림 1](13-adding-social-networking-to-your-web-site/_static/image1.jpg)

1. <span data-ttu-id="dcbd7-124">[ASP.NET 웹 페이지 사이트에 도우미 설치](https://go.microsoft.com/fwlink/?LinkId=252372)의 설명에 따라 웹 사이트에 ASP.NET 웹 도우미 라이브러리를 추가 합니다 (아직 추가 하지 않은 경우).- *listlinkshare. cshtml* 라는 페이지를 만들고 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-124">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.- Create a page named *ListLinkShare.cshtml* and add the following markup:</span></span>

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample1.cshtml)]

    <span data-ttu-id="dcbd7-125">이 예에서는 `LinkShare` 도우미가 실행 될 때 페이지 제목이 매개 변수로 전달 되 고이는 페이지 제목을 소셜 네트워킹 사이트에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-125">In this example, when the `LinkShare` helper runs, the page title is passed as a parameter, which in turn passes the page title to the social networking site.</span></span> <span data-ttu-id="dcbd7-126">그러나 원하는 모든 문자열을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-126">However, you could pass in any string you want.</span></span> <span data-ttu-id="dcbd7-127">또한이 예제에서는 목록에 포함할 소셜 네트워킹 사이트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-127">This example also specifies which social networking sites to include in the list.</span></span> <span data-ttu-id="dcbd7-128">사이트와 관련 된 소셜 네트워킹 사이트를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-128">You can specify the social networking sites that are relevant to your site.</span></span>
2. <span data-ttu-id="dcbd7-129">브라우저에서 *Listlinkshare. cshtml* 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-129">Run the *ListLinkShare.cshtml* page in a browser.</span></span> <span data-ttu-id="dcbd7-130">(파일을 실행 하기 전에 해당 페이지가 **파일** 작업 영역에서 선택 되어 있는지 확인 합니다.)</span><span class="sxs-lookup"><span data-stu-id="dcbd7-130">(Make sure the page is selected in the **Files** workspace before you run it.)</span></span>
3. <span data-ttu-id="dcbd7-131">등록 한 사이트 중 하나에 대 한 문자 모양을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-131">Click a glyph for one of the sites that you're signed up for.</span></span> <span data-ttu-id="dcbd7-132">링크를 누르면 링크를 공유할 수 있는 선택한 소셜 네트워크 사이트의 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-132">The link takes you to the page on the selected social network site where you can share a link.</span></span> <span data-ttu-id="dcbd7-133">예를 들어 Reddit 링크를 클릭 하면 Reddit 웹 사이트의 `submit to reddit` 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-133">For example, if you click the Reddit link, you're taken to the `submit to reddit` page on the Reddit website.</span></span>

     ![그림 2](13-adding-social-networking-to-your-web-site/_static/image2.jpg)

<a id="Adding_a_Twitter_Feed"></a>
## <a name="adding-a-twitter-feed"></a><span data-ttu-id="dcbd7-135">Twitter 피드 추가</span><span class="sxs-lookup"><span data-stu-id="dcbd7-135">Adding a Twitter Feed</span></span>

<span data-ttu-id="dcbd7-136">Twitter API의 현재 버전과 호환 되는 Twitter 도우미를 사용 하는 방법에 대 한 자세한 내용은 [twitter 도우미](../ui-layouts-and-themes/twitter-helper.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-136">For information about using a Twitter helper that is compatible with the current version of the Twitter API, see [Twitter helper](../ui-layouts-and-themes/twitter-helper.md).</span></span> <span data-ttu-id="dcbd7-137">이 예제에서는 여러 페이지의 코드를 쉽게 다시 사용할 수 있도록 자체 도우미를 작성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-137">This example shows how to write your own helper so you can easily reuse the code from many pages.</span></span>

<a id="Displaying_a_Facebook_Button"></a>
## <a name="displaying-a-facebook-quotlikequot-button"></a><span data-ttu-id="dcbd7-138">&quot; 단추와 같은 Facebook &quot;표시</span><span class="sxs-lookup"><span data-stu-id="dcbd7-138">Displaying a Facebook &quot;Like&quot; Button</span></span>

<span data-ttu-id="dcbd7-139">경우에 따라 도우미에 의존 하지 않고 소셜 네트워킹 공급자에서 직접 코드를 가져오는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-139">In some cases, your best option is to get the code directly from the social networking provider rather than relying on a helper.</span></span> <span data-ttu-id="dcbd7-140">이는 소셜 네트워크 공급자가 도우미가 업데이트 되는 것 보다 더 빠르게 해당 옵션을 업데이트 하는 경우에 특히 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-140">This is especially true if the social network provider updates its options more quickly than the helper is updated.</span></span>

<span data-ttu-id="dcbd7-141">사이트에 Facebook 기능 (예: Like 단추)을 추가 하려면 [developers.facebook.com](https://developers.facebook.com/) 사이트에서 코드 조각을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-141">To add Facebook features (such as the Like button) to your site, you can retrieve code snippets from the [developers.facebook.com](https://developers.facebook.com/) site.</span></span> <span data-ttu-id="dcbd7-142">Facebook 사이트에서 해당 도구를 사용 하 여 사이트와 관련 된 코드 조각을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-142">On the Facebook site, you use their tools to generate a code snippet that is relevant to your site.</span></span>

<span data-ttu-id="dcbd7-143">다음 강조 표시 된 코드는 developers.facebook.com 사이트의 유사 단추 도구에서 검색 된 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-143">The following highlighted code is the code that was retrieved from the Like Button tool on the developers.facebook.com site.</span></span> <span data-ttu-id="dcbd7-144">사용자 고유의 앱 ID를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-144">You must provide your own app ID.</span></span>

[!code-html[Main](13-adding-social-networking-to-your-web-site/samples/sample2.html?highlight=7-14,16-17)]

<a id="Rendering_a_Gravatar_Image"></a>
## <a name="rendering-a-gravatar-image"></a><span data-ttu-id="dcbd7-145">Gravatar 이미지 렌더링</span><span class="sxs-lookup"><span data-stu-id="dcbd7-145">Rendering a Gravatar Image</span></span>

<span data-ttu-id="dcbd7-146">*Gravatar* (전 세계적으로 인식 되는 아바타&quot;)는 여러 웹 사이트에서 아바타 &#8212; &quot;(사용자를 나타내는 이미지)로 사용할 수 있는 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-146">A *Gravatar* (a &quot;globally recognized avatar&quot;) is an image that can be used on multiple websites as your avatar &#8212; that is, an image that represents you.</span></span> <span data-ttu-id="dcbd7-147">예를 들어 Gravatar는 포럼 게시물, 블로그 설명 등의 사람을 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-147">For example, a Gravatar can identify a person in a forum post, in a blog comment, and so on.</span></span> <span data-ttu-id="dcbd7-148">[http://www.gravatar.com/](http://www.gravatar.com/)의 Gravatar 웹 사이트에서 자신의 Gravatar를 등록할 수 있습니다. 웹 사이트의 사용자 이름 또는 전자 메일 주소 옆에 이미지를 표시 하려면 Gravatar 도우미를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-148">(You can register your own Gravatar at the Gravatar website at [http://www.gravatar.com/](http://www.gravatar.com/).) If you want to display images next to people's names or email addresses on your website, you can use the Gravatar helper.</span></span>

<span data-ttu-id="dcbd7-149">이 예제에서는 자신을 나타내는 단일 Gravatar를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-149">In this example, you're using a single Gravatar that represents yourself.</span></span> <span data-ttu-id="dcbd7-150">Gravatar를 사용 하는 또 다른 방법은 사용자가 사이트에 등록할 때 Gravatar 주소를 지정할 수 있도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-150">Another way to use a Gravatar is to let people specify their Gravatar address when they register on your site.</span></span> <span data-ttu-id="dcbd7-151">(사용자가 [ASP.NET 웹 페이지 사이트에 보안 및 멤버 자격을 추가](https://go.microsoft.com/fwlink/?LinkId=202904)하도록 등록 하는 방법을 알아볼 수 있습니다.) 그런 다음 해당 사용자에 대 한 정보를 표시할 때마다 사용자 이름을 표시 하는 위치에 Gravatar를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-151">(You can learn how to let people register in [Adding Security and Membership to an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202904).) Then whenever you display information for that user, you can just add the Gravatar to where you display the user's name.</span></span>

1. <span data-ttu-id="dcbd7-152">[ASP.NET 웹 페이지 사이트에 도우미 설치](https://go.microsoft.com/fwlink/?LinkId=252372)에 설명 된 대로 ASP.NET 웹 도우미 라이브러리를 웹 사이트에 추가 합니다 (아직 없는 경우).</span><span class="sxs-lookup"><span data-stu-id="dcbd7-152">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="dcbd7-153">*Gravatar*라는 새 웹 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-153">Create a new web page named *Gravatar.cshtml*.</span></span>
3. <span data-ttu-id="dcbd7-154">파일에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-154">Add the following markup to the file:</span></span> 

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample3.cshtml)]

    <span data-ttu-id="dcbd7-155">`Gravatar.GetHtml` 메서드는 페이지에 Gravatar 이미지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-155">The `Gravatar.GetHtml` method displays the Gravatar image on the page.</span></span> <span data-ttu-id="dcbd7-156">이미지의 크기를 변경 하려면 숫자를 두 번째 매개 변수로 포함 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-156">To change the size of the image, you can include a number as a second parameter.</span></span> <span data-ttu-id="dcbd7-157">기본 크기는 80입니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-157">The default size is 80.</span></span> <span data-ttu-id="dcbd7-158">80 보다 작은 숫자는 이미지를 더 작게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-158">Numbers less than 80 make the image smaller.</span></span> <span data-ttu-id="dcbd7-159">80 보다 큰 숫자는 이미지를 더 크게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-159">Numbers greater than 80 make the image larger.</span></span>
4. <span data-ttu-id="dcbd7-160">`Gravatar.GetHtml` 메서드에서 `<Your Gravatar account here>`을 Gravatar 계정에 사용 하는 전자 메일 주소로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-160">In the `Gravatar.GetHtml` methods, replace `<Your Gravatar account here>` with the email address that you use for your Gravatar account.</span></span> <span data-ttu-id="dcbd7-161">Gravatar 계정이 없는 경우에는 사용자의 전자 메일 주소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-161">(If you don't have a Gravatar account, you can use the email address of someone who does.)</span></span>
5. <span data-ttu-id="dcbd7-162">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-162">Run the page in your browser.</span></span> <span data-ttu-id="dcbd7-163">이 페이지에는 지정한 전자 메일 주소에 대 한 두 개의 Gravatar 이미지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-163">The page displays two Gravatar images for the email address you specified.</span></span> <span data-ttu-id="dcbd7-164">두 번째 이미지는 첫 번째 이미지 보다 작습니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-164">The second image is smaller than the first.</span></span> 

    ![그림 4](13-adding-social-networking-to-your-web-site/_static/image3.jpg)

<a id="Displaying_an_Xbox_Gamer_Card"></a>
## <a name="displaying-an-xbox-gamer-card"></a><span data-ttu-id="dcbd7-166">Xbox 게이머 카드 표시</span><span class="sxs-lookup"><span data-stu-id="dcbd7-166">Displaying an Xbox Gamer Card</span></span>

<span data-ttu-id="dcbd7-167">사용자가 Microsoft Xbox 게임을 온라인으로 재생 하는 경우 각 사용자에 게는 고유한 ID가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-167">When people play Microsoft Xbox games online, each user has a unique ID.</span></span> <span data-ttu-id="dcbd7-168">통계는 각 플레이어에 대해 평판, 게이머 점수 및 최근에 재생 된 게임을 보여 주는 게이머 카드 형식으로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-168">Statistics are kept for each player in the form of a gamer card, which shows their reputation, gamer score, and recently played games.</span></span> <span data-ttu-id="dcbd7-169">Xbox 게이머 라면 `GamerCard` 도우미를 사용 하 여 사이트의 페이지에 게이머 카드를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-169">If you're an Xbox gamer, you can show your gamer card on pages in your site by using the `GamerCard` helper.</span></span>

1. <span data-ttu-id="dcbd7-170">[ASP.NET 웹 페이지 사이트에 도우미 설치](https://go.microsoft.com/fwlink/?LinkId=252372)에 설명 된 대로 ASP.NET 웹 도우미 라이브러리를 웹 사이트에 추가 합니다 (아직 없는 경우).</span><span class="sxs-lookup"><span data-stu-id="dcbd7-170">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="dcbd7-171">*Xboxgamer. cshtml* 이라는 새 페이지를 만들고 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-171">Create a new page named *XboxGamer.cshtml* and add the following markup.</span></span>

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample4.cshtml)]

    <span data-ttu-id="dcbd7-172">`GamerCard.GetHtml` 속성을 사용 하 여 표시할 게이머 카드의 별칭을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-172">You use the `GamerCard.GetHtml` property to specify the alias for the gamer card to be displayed.</span></span>
3. <span data-ttu-id="dcbd7-173">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-173">Run the page in your browser.</span></span> <span data-ttu-id="dcbd7-174">지정 된 Xbox 게이머 카드가 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcbd7-174">The page displays the Xbox gamer card that you specified.</span></span>

    ![그림 5](13-adding-social-networking-to-your-web-site/_static/image4.jpg)
