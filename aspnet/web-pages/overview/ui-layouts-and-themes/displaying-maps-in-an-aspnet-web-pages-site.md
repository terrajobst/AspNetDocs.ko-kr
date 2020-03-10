---
uid: web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
title: ASP.NET 웹 페이지 (Razor) 사이트에서 맵 표시 | Microsoft Docs
author: Rick-Anderson
description: 이 문서에서는 Bing, Google, Ma ...에서 제공 하는 매핑 서비스를 기준으로 Razor (ASP.NET 웹 페이지) 웹 사이트의 페이지에 대화형 맵을 표시 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 02/20/2014
ms.assetid: b5c268dd-ca6a-4562-b94c-a220fcf01f58
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 36f3b753cf312504892872ff54bef49854588990
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518723"
---
# <a name="displaying-maps-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="1d7e4-103">ASP.NET 웹 페이지 (Razor) 사이트에서 맵 표시</span><span class="sxs-lookup"><span data-stu-id="1d7e4-103">Displaying Maps in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="1d7e4-104">만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="1d7e4-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="1d7e4-105">이 문서에서는 Bing, Google, MapQuest 및 Yahoo에서 제공 하는 매핑 서비스를 기반으로 하는 ASP.NET 웹 페이지 (Razor) 웹 사이트의 페이지에 대화형 지도를 표시 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-105">This article explains how to display interactive maps on pages in an ASP.NET Web Pages (Razor) website based on mapping services provided by Bing, Google, MapQuest, and Yahoo.</span></span>
> 
> <span data-ttu-id="1d7e4-106">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="1d7e4-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="1d7e4-107">주소를 기준으로 맵을 생성 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d7e4-107">How to generate a map based on an address.</span></span>
> - <span data-ttu-id="1d7e4-108">위도 및 경도 좌표를 기준으로 맵을 생성 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-108">How to generate a map based on latitude and longitude coordinates.</span></span>
> - <span data-ttu-id="1d7e4-109">Bing Maps 개발자 계정을 등록 하 고 Bing Maps에서 사용할 키를 가져오는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-109">How to register a Bing Maps Developer Account and get a key to use with Bing Maps.</span></span>
> 
> <span data-ttu-id="1d7e4-110">다음은이 문서에서 소개 하는 ASP.NET 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-110">This is the ASP.NET feature introduced in the article:</span></span>
> 
> - <span data-ttu-id="1d7e4-111">`Maps` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-111">The `Maps` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="1d7e4-112">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="1d7e4-112">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="1d7e4-113">ASP.NET 웹 페이지 (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="1d7e4-113">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="1d7e4-114">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="1d7e4-114">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="1d7e4-115">이 자습서는 WebMatrix 3 에서도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-115">This tutorial also works with WebMatrix 3.</span></span>

<span data-ttu-id="1d7e4-116">웹 페이지에서 `Maps` 도우미를 사용 하 여 페이지에 지도를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-116">In Web Pages, you can display maps on a page by using `Maps` helper.</span></span> <span data-ttu-id="1d7e4-117">주소 또는 경도 및 위도 좌표 집합을 기준으로 맵을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-117">You can generate maps based either on an address or on a set of longitude and latitude coordinates.</span></span> <span data-ttu-id="1d7e4-118">`Maps` 클래스를 사용 하면 Bing, Google, MapQuest 및 Yahoo를 비롯 한 인기 있는 맵 엔진을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-118">The `Maps` class lets you call into popular map engines including Bing, Google, MapQuest, and Yahoo.</span></span>

<span data-ttu-id="1d7e4-119">페이지에 매핑을 추가 하는 단계는 호출 하는 맵 엔진에 관계 없이 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-119">The steps for adding mapping to a page are the same regardless of which of the map engines you call.</span></span> <span data-ttu-id="1d7e4-120">지도를 표시 하는 데 사용할 수 있는 메서드를 만든 다음 `Maps` 도우미의 메서드를 호출 하는 JavaScript 파일 참조를 추가 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-120">You just add a JavaScript file reference that makes available methods to display the map, and then you call methods of the `Maps` helper.</span></span>

<span data-ttu-id="1d7e4-121">사용 하는 `Maps` 도우미 방법을 기반으로 하는 맵 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-121">You choose a map service based on which `Maps` helper method you use.</span></span> <span data-ttu-id="1d7e4-122">다음 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-122">You can use any of these:</span></span>

- `Maps.GetBingHtml`
- `Maps.GetGoogleHtml`
- `Maps.GetYahooHtml`
- `Maps.GetMapQuestHtml`

## <a name="installing-the-pieces-you-need"></a><span data-ttu-id="1d7e4-123">필요한 부분 설치</span><span class="sxs-lookup"><span data-stu-id="1d7e4-123">Installing the Pieces You Need</span></span>

<span data-ttu-id="1d7e4-124">지도를 표시 하려면 다음 부분이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-124">To display maps, you need these pieces:</span></span>

- <span data-ttu-id="1d7e4-125">`Maps` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-125">The `Maps` helper.</span></span> <span data-ttu-id="1d7e4-126">이 도우미는 ASP.NET 웹 도우미 라이브러리의 버전 2에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-126">This helper is in version 2 of the ASP.NET Web Helpers Library.</span></span> <span data-ttu-id="1d7e4-127">라이브러리를 아직 추가 하지 않은 경우 사이트에서 NuGet 패키지로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-127">If you haven't already added the library, you can install it in your site as a NuGet package.</span></span> <span data-ttu-id="1d7e4-128">자세한 내용은 [ASP.NET 웹 페이지 사이트에 도우미 설치](https://go.microsoft.com/fwlink/?LinkId=252372)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-128">For details, see [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372).</span></span> <span data-ttu-id="1d7e4-129">갤러리에서 `microsoft-web-helpers` 패키지를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-129">(In the Gallery, search for the `microsoft-web-helpers` package.)</span></span>
- <span data-ttu-id="1d7e4-130">JQuery 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-130">The jQuery library.</span></span> <span data-ttu-id="1d7e4-131">일부 WebMatrix 사이트 템플릿은 해당 *스크립트* 폴더에 jQuery 라이브러리를 이미 포함 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-131">Several of the WebMatrix site templates already include jQuery libraries in their *Script* folders.</span></span> <span data-ttu-id="1d7e4-132">이러한 라이브러리가 없으면 [jQuery.org](http://jQuery.org) 사이트에서 직접 최신 jQuery 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-132">If you do not have these libraries, you can download the latest jQuery library directly from the [jQuery.org](http://jQuery.org) site.</span></span> <span data-ttu-id="1d7e4-133">또는 템플릿을 사용 하 여 새 사이트 (예: **시작 사이트** 템플릿)를 만든 다음 해당 사이트의 jQuery 파일을 현재 사이트로 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-133">Or you can create a new site using a template (for example, the **Starter Site** template) and then copy the jQuery files from that site to your current site.</span></span>

<span data-ttu-id="1d7e4-134">마지막으로, Bing maps를 사용 하려는 경우 먼저 (무료) 계정을 만들고 키를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-134">Finally, if you want to use Bing maps, you must first create a (free) account and get a key.</span></span> <span data-ttu-id="1d7e4-135">키를 가져오려면 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-135">To get a key, follow these steps:</span></span>

1. <span data-ttu-id="1d7e4-136">[Bing Maps 개발자 계정](https://www.microsoft.com/maps/developers/web.aspx)에 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-136">Create an account on the [Bing Maps Developer Account](https://www.microsoft.com/maps/developers/web.aspx).</span></span> <span data-ttu-id="1d7e4-137">Microsoft 계정 (Windows Live ID)도 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-137">You must have a Microsoft account (Windows Live ID) as well.</span></span>

    <span data-ttu-id="1d7e4-138">**평가/테스트**에 키를 사용 하도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-138">You can specify that you want to use the key for **Evaluation/Test**.</span></span> <span data-ttu-id="1d7e4-139">WebMatrix 및 IIS Express를 사용 하 여 자신의 컴퓨터에서 매핑 함수를 테스트 하는 경우 **사이트** 작업 영역으로 이동 하 여 사이트의 URL (예: 포트 번호가 다를 수 있지만 `http://localhost:50408`)을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-139">If you are testing the mapping function on your own computer using WebMatrix and IIS Express, go the **Site** workspace and note the URL of your site (for example, `http://localhost:50408`, although your port number will probably be different).</span></span> <span data-ttu-id="1d7e4-140">등록할 때이 *localhost* 주소를 사이트로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-140">You can use this *localhost* address as the site when you register.</span></span>
2. <span data-ttu-id="1d7e4-141">계정에 등록 한 후 Bing Maps 계정 센터로 이동 하 고 **키 만들기 또는 보기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-141">After you have registered for an account, go to the Bing Maps Account Center and click **Create or view keys**:</span></span>

    ![매핑-2](displaying-maps-in-an-aspnet-web-pages-site/_static/image1.png)
3. <span data-ttu-id="1d7e4-143">Bing에서 만든 키를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-143">Record the key that Bing creates.</span></span>

## <a name="creating-a-map-based-on-an-address-using-google"></a><span data-ttu-id="1d7e4-144">주소를 기준으로 맵 만들기 (Google 사용)</span><span class="sxs-lookup"><span data-stu-id="1d7e4-144">Creating a Map Based on an Address (Using Google)</span></span>

<span data-ttu-id="1d7e4-145">다음 예제에서는 주소를 기준으로 맵을 렌더링 하는 페이지를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-145">The following example shows how to create a page that renders a map based on an address.</span></span> <span data-ttu-id="1d7e4-146">이 예제에서는 Google Maps를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-146">This example shows how to use Google Maps.</span></span>

1. <span data-ttu-id="1d7e4-147">사이트의 루트에 *Mapaddress. cshtml* 라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-147">Create a file named *MapAddress.cshtml* in the root of the site.</span></span> <span data-ttu-id="1d7e4-148">이 페이지는 전달 하는 주소를 기준으로 맵을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-148">This page will generate a map based on an address that you pass to it.</span></span>
2. <span data-ttu-id="1d7e4-149">다음 코드를 파일에 복사 하 여 기존 콘텐츠를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-149">Copy the following code into the file, overwriting the existing content.</span></span>

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    <span data-ttu-id="1d7e4-150">페이지의 다음 기능을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-150">Notice the following features of the page:</span></span>

    - <span data-ttu-id="1d7e4-151">`<head>` 요소의 `<script>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-151">The `<script>` element in the `<head>` element.</span></span> <span data-ttu-id="1d7e4-152">예제에서 `<script>` 요소는 jQuery 라이브러리 버전 1.6.4의 압축 된 (압축) 버전인 *jquery-1.10.2.min.js 1.6.4* 파일을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-152">In the example, the `<script>` element references the *jquery-1.6.4.min.js* file, which is a minified (compressed) version of the jQuery library, version 1.6.4.</span></span> <span data-ttu-id="1d7e4-153">참조에서는 *.js* 파일이 사이트의 *Scripts* 폴더에 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-153">Note that the reference assumes that the *.js* file is in the *Scripts* folder of your site.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="1d7e4-154">다른 버전의 jQuery 라이브러리를 사용 하는 경우 해당 버전을 올바르게 가리키는지 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-154">If you're using a different version of the jQuery library, just make sure that you're pointing to that version correctly.</span></span>
    - <span data-ttu-id="1d7e4-155">페이지 본문의 `@Maps.GetGoogleHtml`에 대 한 호출입니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-155">The call to the `@Maps.GetGoogleHtml` in the body of the page.</span></span> <span data-ttu-id="1d7e4-156">주소를 매핑하려면 주소 문자열을 전달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-156">To map an address, you must pass an address string.</span></span> <span data-ttu-id="1d7e4-157">다른 맵 엔진에 대 한 메서드는 비슷한 방식으로 작동 합니다 (`@Maps.GetYahooHtml`, `@Maps.GetMapQuestHtml`).</span><span class="sxs-lookup"><span data-stu-id="1d7e4-157">The methods for the other map engines work in a similar way (`@Maps.GetYahooHtml`, `@Maps.GetMapQuestHtml`).</span></span>
3. <span data-ttu-id="1d7e4-158">페이지를 실행 하 고 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-158">Run the page and enter an address.</span></span> <span data-ttu-id="1d7e4-159">이 페이지에는 사용자가 지정한 위치를 표시 하는 Google 지도를 기반으로 지도가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-159">The page displays a map, based on Google Maps, that shows the location that you specified.</span></span>

     ![매핑-1](displaying-maps-in-an-aspnet-web-pages-site/_static/image2.png)

## <a name="creating-a-map-based-on-latitude-and-longitude-coordinates-using-bing"></a><span data-ttu-id="1d7e4-161">위도 및 경도 좌표를 기준으로 지도 만들기 (Bing 사용)</span><span class="sxs-lookup"><span data-stu-id="1d7e4-161">Creating a Map Based on Latitude and Longitude Coordinates (Using Bing)</span></span>

<span data-ttu-id="1d7e4-162">이 예제에서는 좌표를 기준으로 지도를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-162">This example shows how to create a map based on coordinates.</span></span> <span data-ttu-id="1d7e4-163">이 예에서는 Bing maps를 사용 하는 방법과 Bing 키를 포함 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-163">This example shows how to use Bing maps and how to include your Bing key.</span></span> <span data-ttu-id="1d7e4-164">(Bing 키를 사용 하지 않고 다른 맵 엔진을 사용 하 여 좌표를 기준으로 지도를 만들 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="1d7e4-164">(You can create a map based on coordinates using the other map engines also, without using a Bing key.)</span></span>

1. <span data-ttu-id="1d7e4-165">사이트의 루트에 *Mapcoordinates. cshtml* 라는 파일을 만들고 기존 콘텐츠를 다음 코드 및 태그로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-165">Create a file named *MapCoordinates.cshtml* in the root of the site and replace the existing content with the following code and markup:</span></span>

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample2.cshtml)]
2. <span data-ttu-id="1d7e4-166">`your-key-here`를 앞에서 생성 한 Bing Maps 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-166">Replace `your-key-here` with the Bing Maps key that you generated earlier.</span></span>
3. <span data-ttu-id="1d7e4-167">*Mapcoordinates. cshtml* 페이지를 실행 하 고, 위도 및 경도 좌표를 입력 한 다음, **지도** 를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-167">Run the *MapCoordinates.cshtml* page, enter latitude and longitude coordinates, and then click the **Map It!**</span></span> <span data-ttu-id="1d7e4-168">단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-168">button.</span></span> <span data-ttu-id="1d7e4-169">(좌표를 모르는 경우 다음을 시도 하세요.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-169">(If you don't know any coordinates, try the following.</span></span> <span data-ttu-id="1d7e4-170">Microsoft Redmond 캠퍼스의 위치입니다.)</span><span class="sxs-lookup"><span data-stu-id="1d7e4-170">This is a location on the Microsoft Redmond campus.)</span></span>

   - <span data-ttu-id="1d7e4-171">위도: 47.6781005859375</span><span class="sxs-lookup"><span data-stu-id="1d7e4-171">Latitude: 47.6781005859375</span></span>
   - <span data-ttu-id="1d7e4-172">경도:-122.158317565918</span><span class="sxs-lookup"><span data-stu-id="1d7e4-172">Longitude: -122.158317565918</span></span>

     <span data-ttu-id="1d7e4-173">지정한 좌표를 사용 하 여 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d7e4-173">The page is displayed using the coordinates that you specified.</span></span>

     ![매핑-3](displaying-maps-in-an-aspnet-web-pages-site/_static/image3.png)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="1d7e4-175">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1d7e4-175">Additional Resources</span></span>

[<span data-ttu-id="1d7e4-176">Microsoft Maps API 참조</span><span class="sxs-lookup"><span data-stu-id="1d7e4-176">Microsoft.Maps API Reference</span></span>](https://msdn.microsoft.com/library/gg427611.aspx)
