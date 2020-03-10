---
uid: web-pages/overview/ui-layouts-and-themes/10-working-with-video
title: ASP.NET 웹 페이지 (Razor) 사이트에 비디오 표시 | Microsoft Docs
author: Rick-Anderson
description: 이 장에서는 Razor 구문 페이지를 사용 하 여 ASP.NET 웹 페이지에 비디오를 표시 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 332fb3da-e2a5-460d-bb90-dd911e1e2c95
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/10-working-with-video
msc.type: authoredcontent
ms.openlocfilehash: 516d46f38ce8910209f4207c474b0404bf012950
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510383"
---
# <a name="displaying-video-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="92bc2-103">ASP.NET 웹 페이지 (Razor) 사이트에 비디오 표시</span><span class="sxs-lookup"><span data-stu-id="92bc2-103">Displaying Video in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="92bc2-104">만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="92bc2-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="92bc2-105">이 문서에서는 Razor (ASP.NET 웹 페이지) 웹 사이트에서 비디오 (미디어) 플레이어를 사용 하 여 사용자가 사이트에 저장 된 비디오를 볼 수 있도록 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-105">This article explains how to use a video (media) player in an ASP.NET Web Pages (Razor) website to let users view videos that are stored on the site.</span></span> <span data-ttu-id="92bc2-106">Razor 구문 ASP.NET 웹 페이지를 사용 하면 Flash ( *.swf*), Media Player ( *.Wmv*) 및 Silverlight ( *.xap*) 비디오를 재생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-106">ASP.NET Web Pages with Razor syntax lets you play Flash (*.swf*), Media Player (*.wmv*), and Silverlight (*.xap*) videos.</span></span>
> 
> <span data-ttu-id="92bc2-107">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="92bc2-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="92bc2-108">비디오 플레이어를 선택 하는 방법</span><span class="sxs-lookup"><span data-stu-id="92bc2-108">How to choose a video player.</span></span>
> - <span data-ttu-id="92bc2-109">웹 페이지에 비디오를 추가 하는 방법</span><span class="sxs-lookup"><span data-stu-id="92bc2-109">How to add video to a web page.</span></span>
> - <span data-ttu-id="92bc2-110">비디오 플레이어 특성을 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="92bc2-110">How to set video player attributes.</span></span>
> 
> <span data-ttu-id="92bc2-111">다음은이 문서에서 소개 하는 ASP.NET Razor 페이지 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-111">These are the ASP.NET Razor pages features introduced in the article:</span></span>
> 
> - <span data-ttu-id="92bc2-112">`Video` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-112">The `Video` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="92bc2-113">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="92bc2-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="92bc2-114">ASP.NET 웹 페이지 (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="92bc2-114">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="92bc2-115">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="92bc2-115">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="92bc2-116">이 자습서는 WebMatrix 3 에서도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-116">This tutorial also works with WebMatrix 3.</span></span>

## <a name="introduction"></a><span data-ttu-id="92bc2-117">소개</span><span class="sxs-lookup"><span data-stu-id="92bc2-117">Introduction</span></span>

<span data-ttu-id="92bc2-118">사이트에 비디오를 표시 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-118">You might want to display a video on your site.</span></span> <span data-ttu-id="92bc2-119">이 작업을 수행 하는 한 가지 방법은 YouTube와 같이 이미 비디오가 있는 사이트에 연결 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-119">One way to do that is to link to a site that already has the video, like YouTube.</span></span> <span data-ttu-id="92bc2-120">이러한 사이트의 비디오를 자체 페이지에 직접 포함 하려는 경우 일반적으로 사이트에서 HTML 태그를 가져온 다음 페이지에 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-120">If you want to embed a video from these sites directly in your own pages, you can usually get HTML markup from the site and then copy it into your page.</span></span> <span data-ttu-id="92bc2-121">예를 들어 다음 예제에서는 YouTube 비디오를 포함 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-121">For example, the following example shows how to embed a YouTube video:</span></span>

[!code-html[Main](10-working-with-video/samples/sample1.html?highlight=10-14)]

<span data-ttu-id="92bc2-122">자신의 웹 사이트에 있는 비디오를 재생 하려는 경우 (공용 비디오 공유 사이트가 아님) 다음과 같은 포함 태그를 사용 하 여 직접 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-122">If you want to play a video that's on your own website (not on a public video-sharing site), you can't directly link to it using embedded markup like this.</span></span> <span data-ttu-id="92bc2-123">그러나 미디어 플레이어를 페이지에서 직접 렌더링 하는 `Video` 도우미를 사용 하 여 사이트에서 비디오를 재생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-123">However, you can play videos from your site by using the `Video` helper, which renders a media player directly in a page.</span></span>

<a id="Choosing_a_Video_Player"></a>
## <a name="choosing-a-video-player"></a><span data-ttu-id="92bc2-124">비디오 플레이어 선택</span><span class="sxs-lookup"><span data-stu-id="92bc2-124">Choosing a Video Player</span></span>

<span data-ttu-id="92bc2-125">비디오 파일에는 많은 형식이 있으며 각 형식에는 일반적으로 다른 플레이어와 플레이어를 구성 하는 다른 방법이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-125">There are lots of formats for video files, and each format typically requires a different player and a different way to configure the player.</span></span> <span data-ttu-id="92bc2-126">ASP.NET Razor 페이지에서 `Video` 도우미를 사용 하 여 웹 페이지에서 비디오를 재생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-126">In ASP.NET Razor pages, you can play a video in a web page using the `Video` helper.</span></span> <span data-ttu-id="92bc2-127">`Video` 도우미는 웹 페이지에 비디오를 추가 하는 데 일반적으로 사용 되는 `object` 및 `embed` HTML 요소를 자동으로 생성 하므로 웹 페이지에 비디오를 포함 하는 프로세스를 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-127">The `Video` helper simplifies the process of embedding videos in a web page because it automatically generates the `object` and `embed` HTML elements that are normally used to add video to the page.</span></span>

<span data-ttu-id="92bc2-128">`Video` 도우미는 다음과 같은 미디어 플레이어를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-128">The `Video` helper supports the following media players:</span></span>

- <span data-ttu-id="92bc2-129">Adobe Flash</span><span class="sxs-lookup"><span data-stu-id="92bc2-129">Adobe Flash</span></span>
- <span data-ttu-id="92bc2-130">Windows MediaPlayer</span><span class="sxs-lookup"><span data-stu-id="92bc2-130">Windows MediaPlayer</span></span>
- <span data-ttu-id="92bc2-131">Microsoft Silverlight</span><span class="sxs-lookup"><span data-stu-id="92bc2-131">Microsoft Silverlight</span></span>

### <a name="the-flash-player"></a><span data-ttu-id="92bc2-132">플래시 플레이어</span><span class="sxs-lookup"><span data-stu-id="92bc2-132">The Flash Player</span></span>

<span data-ttu-id="92bc2-133">`Video` 도우미의 `Flash` 플레이어를 사용 하면 웹 페이지에서 Flash 비디오 ( *.swf* 파일)를 재생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-133">The `Flash` player of the `Video` helper let you play Flash videos (*.swf* files) in a web page.</span></span> <span data-ttu-id="92bc2-134">최소한 비디오 파일의 경로를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-134">At a minimum, you have to provide a path to the video file.</span></span> <span data-ttu-id="92bc2-135">아무 것도 지정 하지 않고 경로를 지정 하는 경우 플레이어는 현재 버전의 Flash에서 설정 된 기본값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-135">If you specify nothing but the path, the player uses default values that are set by the current version of Flash.</span></span> <span data-ttu-id="92bc2-136">일반적인 기본 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-136">Typical default settings are:</span></span>

- <span data-ttu-id="92bc2-137">비디오는 기본 너비와 높이를 사용 하 여 배경색 없이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-137">The video is displayed using its default width and height and without a background color.</span></span>
- <span data-ttu-id="92bc2-138">페이지가 로드 되 면 비디오가 자동으로 재생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-138">The video plays automatically when the page loads.</span></span>
- <span data-ttu-id="92bc2-139">비디오는 명시적으로 중지 될 때까지 지속적으로 반복 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-139">The video loops continuously until it's explicitly stopped.</span></span>
- <span data-ttu-id="92bc2-140">비디오를 축소 하 여 특정 크기에 맞게 비디오를 자르는 것이 아니라 비디오를 모두 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-140">The video is scaled to show all of the video, rather than cropping the video to fit a specific size.</span></span>
- <span data-ttu-id="92bc2-141">비디오는 창에서 재생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-141">The video plays in a window.</span></span>

### <a name="the-mediaplayer-player"></a><span data-ttu-id="92bc2-142">MediaPlayer 플레이어</span><span class="sxs-lookup"><span data-stu-id="92bc2-142">The MediaPlayer Player</span></span>

<span data-ttu-id="92bc2-143">`Video` 도우미의 `MediaPlayer` 플레이어를 사용 하면 웹 페이지에서 Windows Media 비디오 ( *.wmv* 파일), windows media 오디오 ( *.wma* 파일) 및 mp3 ( *. mp3* 파일)를 재생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-143">The `MediaPlayer` player of the `Video` helper lets you play Windows Media videos (*.wmv* files), Windows Media audio (*.wma* files), and MP3 (*.mp3* files) in a web page.</span></span> <span data-ttu-id="92bc2-144">재생할 미디어 파일의 경로를 포함 해야 합니다. 다른 모든 매개 변수는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-144">You must include path of the media file to play; all other parameters are optional.</span></span> <span data-ttu-id="92bc2-145">경로만 지정 하는 경우 플레이어는 다음과 같이 현재 버전의 MediaPlayer에 설정 된 기본 설정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-145">If you specify only a path, the player uses default settings set by the current version of MediaPlayer, such as:</span></span>

- <span data-ttu-id="92bc2-146">비디오는 기본 너비와 높이를 사용 하 여 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-146">The video is displayed using its default width and height.</span></span>
- <span data-ttu-id="92bc2-147">페이지가 로드 되 면 비디오가 자동으로 재생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-147">The video plays automatically when the page loads.</span></span>
- <span data-ttu-id="92bc2-148">비디오가 한 번 재생 됩니다 (반복 하지 않음).</span><span class="sxs-lookup"><span data-stu-id="92bc2-148">The video plays once (it doesn't loop).</span></span>
- <span data-ttu-id="92bc2-149">플레이어는 사용자 인터페이스에 컨트롤의 전체 집합을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-149">The player displays the full set of controls in the user interface.</span></span>
- <span data-ttu-id="92bc2-150">비디오는 창에서 재생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-150">The video plays in a window.</span></span>

### <a name="the-silverlight-player"></a><span data-ttu-id="92bc2-151">Silverlight 플레이어</span><span class="sxs-lookup"><span data-stu-id="92bc2-151">The Silverlight Player</span></span>

<span data-ttu-id="92bc2-152">`Video` 도우미의 `Silverlight` 플레이어를 사용 하 여 Windows Media 비디오 ( *.wmv* 파일), Windows Media 오디오 ( *.wma* 파일) 및 mp3 ( *. mp3* 파일)를 재생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-152">The `Silverlight` player of the `Video` helper lets you play Windows Media Video (*.wmv* files), Windows Media Audio (*.wma* files), and MP3 (*.mp3* files).</span></span> <span data-ttu-id="92bc2-153">Silverlight 기반 응용 프로그램 패키지 ( *.xap* 파일)를 가리키도록 path 매개 변수를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-153">You must set the path parameter to point to a Silverlight-based application package (*.xap* file).</span></span> <span data-ttu-id="92bc2-154">또한 width 및 height 매개 변수를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-154">You also must set the width and height parameters.</span></span> <span data-ttu-id="92bc2-155">모든 다른 매개 변수는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-155">All other parameters are optional.</span></span> <span data-ttu-id="92bc2-156">비디오 용 Silverlight 플레이어를 사용 하는 경우 필수 매개 변수만 설정 하면 Silverlight 플레이어에서 배경색 없이 비디오를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-156">When you use the Silverlight player for video, if you set only the required parameters, the Silverlight player displays the video without a background color.</span></span>

> [!NOTE]
> <span data-ttu-id="92bc2-157">Silverlight를 아직 모르는 경우: *.xap* 파일은 *.xaml* 파일의 레이아웃 지침, 어셈블리의 관리 코드 및 선택적 리소스를 포함 하는 압축 된 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-157">In case you don't already know Silverlight: the *.xap* file is a compressed file that contains layout instructions in a *.xaml* file, managed code in assemblies, and optional resources.</span></span> <span data-ttu-id="92bc2-158">Visual Studio에서 *.xap* 파일을 Silverlight 응용 프로그램 프로젝트로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-158">You can create a *.xap* file in Visual Studio as a Silverlight application project.</span></span>

<span data-ttu-id="92bc2-159">`Silverlight` 비디오 플레이어는 플레이어에 대해 제공 하는 설정과 *.xap* 파일에 제공 되는 설정을 모두 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-159">The `Silverlight` video player uses both the settings that you provide for the player and the settings that are provided in the *.xap* file.</span></span>

> [!TIP] 
> 
> <a id="SB_MimeTypes"></a>
> ### <a name="mime-types"></a><span data-ttu-id="92bc2-160">MIME 형식</span><span class="sxs-lookup"><span data-stu-id="92bc2-160">MIME Types</span></span>
> 
> <span data-ttu-id="92bc2-161">브라우저에서 파일을 다운로드할 때 브라우저는 파일 형식이 렌더링 되는 문서에 대해 지정 된 MIME 형식과 일치 하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-161">When a browser downloads a file, the browser makes sure that the file type matches the MIME type that's specified for the document that's being rendered.</span></span> <span data-ttu-id="92bc2-162">MIME 형식은 파일의 콘텐츠 형식 또는 미디어 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-162">The MIME type is the content type or media type of a file.</span></span> <span data-ttu-id="92bc2-163">`Video` 도우미는 다음과 같은 MIME 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-163">The `Video` helper uses the following MIME types:</span></span>
> 
> - `application/x-shockwave-flash`
> - `application/x-mplayer2`
> - `application/x-silverlight-2`

<a id="Playing_Flash"></a>
## <a name="playing-flash-swf-videos"></a><span data-ttu-id="92bc2-164">플래시 (.swf) 비디오 재생</span><span class="sxs-lookup"><span data-stu-id="92bc2-164">Playing Flash (.swf) Videos</span></span>

<span data-ttu-id="92bc2-165">이 절차에서는 *.sample*이라는 Flash 비디오를 재생 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-165">This procedure shows you how to play a Flash video named *sample.swf*.</span></span> <span data-ttu-id="92bc2-166">이 절차에서는 사용자가 사이트에 *미디어* 라는 폴더를가지고 있으며 해당 폴더에 *.swf* 파일이 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-166">The procedure assumes that you've got a folder named *Media* on your site and that the *.swf* file is in that folder.</span></span>

1. <span data-ttu-id="92bc2-167">[ASP.NET 웹 페이지 사이트에 도우미 설치](https://go.microsoft.com/fwlink/?LinkId=252372)의 설명에 따라 웹 사이트에 ASP.NET 웹 도우미 라이브러리를 추가 합니다 (아직 추가 하지 않은 경우).</span><span class="sxs-lookup"><span data-stu-id="92bc2-167">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.</span></span>
2. <span data-ttu-id="92bc2-168">웹 사이트에서 페이지를 추가 하 고 이름을 *FlashVideo*로 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-168">In the website, add a page and name it *FlashVideo.cshtml*.</span></span>
3. <span data-ttu-id="92bc2-169">페이지에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-169">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample2.cshtml)]
4. <span data-ttu-id="92bc2-170">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-170">Run the page in a browser.</span></span> <span data-ttu-id="92bc2-171">(파일을 실행 하기 전에 해당 페이지가 **파일** 작업 영역에서 선택 되어 있는지 확인 합니다.) 페이지가 표시 되 고 비디오가 자동으로 재생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-171">(Make sure the page is selected in the **Files** workspace before you run it.) The page is displayed and the video plays automatically.</span></span> 

    <span data-ttu-id="92bc2-172">![이미지로](10-working-with-video/_static/image1.jpg "-1 ch08_video")</span><span class="sxs-lookup"><span data-stu-id="92bc2-172">![[image]](10-working-with-video/_static/image1.jpg "ch08_video-1.jpg")</span></span>

<span data-ttu-id="92bc2-173">Flash 비디오에 대 한 `quality` 매개 변수를 `low`, `autolow`, `autohigh`, `medium`, `high`및 `best`로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-173">You can set the `quality` parameter for a Flash video to `low`, `autolow`, `autohigh`, `medium`, `high`, and `best`:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample3.cshtml)]

<span data-ttu-id="92bc2-174">다음과 같이 설정할 수 있는 `scale` 매개 변수를 사용 하 여 특정 크기에서 재생 되도록 플래시 비디오를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-174">You can change the Flash video to play at a specific size using the `scale` parameter, which you can set to the following:</span></span>

- <span data-ttu-id="92bc2-175">`showall`입니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-175">`showall`.</span></span> <span data-ttu-id="92bc2-176">이렇게 하면 원래 가로 세로 비율을 유지 하면서 전체 비디오가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-176">This makes the entire video visible while maintaining the original aspect ratio.</span></span> <span data-ttu-id="92bc2-177">그러나 각 면에 테두리가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-177">However, you might end up with borders on each side.</span></span>
- <span data-ttu-id="92bc2-178">`noorder`입니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-178">`noorder`.</span></span> <span data-ttu-id="92bc2-179">이는 원래 가로 세로 비율을 유지 하면서 비디오를 확장 하지만 잘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-179">This scales the video while maintaining the original aspect ratio, but it might be cropped.</span></span>
- <span data-ttu-id="92bc2-180">`exactfit`입니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-180">`exactfit`.</span></span> <span data-ttu-id="92bc2-181">이렇게 하면 원래 가로 세로 비율을 유지 하지 않고 전체 비디오가 표시 되지만 왜곡이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-181">This makes the entire video visible without preserving the original aspect ratio, but distortion may occur.</span></span>

<span data-ttu-id="92bc2-182">`scale` 매개 변수를 지정 하지 않으면 전체 비디오가 표시 되 고 원래 가로 세로 비율이 자르기 없이 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-182">If you don't specify a `scale` parameter, the entire video will be visible and the original aspect ratio will be maintained without any cropping.</span></span> <span data-ttu-id="92bc2-183">다음 예제에서는 `scale` 매개 변수를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-183">The following example shows how to use the `scale` parameter:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample4.cshtml)]

<span data-ttu-id="92bc2-184">Flash player는 `windowMode`라는 비디오 모드 설정을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-184">The Flash player supports a video mode setting named `windowMode`.</span></span> <span data-ttu-id="92bc2-185">`window`, `opaque`및 `transparent`로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-185">You can set this to `window`, `opaque`, and `transparent`.</span></span> <span data-ttu-id="92bc2-186">기본적으로 `windowMode`은 웹 페이지의 별도 창에 비디오를 표시 하는 `window`로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-186">By default, the `windowMode` is set to `window`, which displays the video in a separate window on the web page.</span></span> <span data-ttu-id="92bc2-187">`opaque` 설정은 웹 페이지의 비디오 뒤에 나오는 모든 항목을 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-187">The `opaque` setting hides everything behind the video on the web page.</span></span> <span data-ttu-id="92bc2-188">`transparent` 설정을 사용 하면 비디오의 일부가 투명 하다 고 가정 하는 웹 페이지의 배경이 비디오를 통해 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-188">The `transparent` setting lets the background of the web page show through the video, assuming any part of the video is transparent.</span></span>

<a id="Playing_MediaPlayer"></a>
## <a name="playing-mediaplayer-wmv-videos"></a><span data-ttu-id="92bc2-189">MediaPlayer ( *.wmv*) 비디오 재생</span><span class="sxs-lookup"><span data-stu-id="92bc2-189">Playing MediaPlayer (*.wmv*) Videos</span></span>

<span data-ttu-id="92bc2-190">다음 절차에서는 *media* 폴더에 있는 *Sample .Wmv* 라는 창 미디어 비디오를 재생 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-190">The following procedure shows you how to play a Window Media video named *sample.wmv* that's in the *Media* folder.</span></span>

1. <span data-ttu-id="92bc2-191">[ASP.NET 웹 페이지 사이트에 도우미 설치](https://go.microsoft.com/fwlink/?LinkId=252372)에 설명 된 대로 ASP.NET 웹 도우미 라이브러리를 웹 사이트에 추가 합니다 (아직 없는 경우).</span><span class="sxs-lookup"><span data-stu-id="92bc2-191">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="92bc2-192">*MediaPlayerVideo*라는 새 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-192">Create a new page named *MediaPlayerVideo.cshtml*.</span></span>
3. <span data-ttu-id="92bc2-193">페이지에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-193">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample5.cshtml)]
4. <span data-ttu-id="92bc2-194">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-194">Run the page in a browser.</span></span> <span data-ttu-id="92bc2-195">비디오가 자동으로 로드 되 고 재생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-195">The video loads and plays automatically.</span></span> 

    <span data-ttu-id="92bc2-196">![이미지로](10-working-with-video/_static/image2.jpg "-2 ch08_video")</span><span class="sxs-lookup"><span data-stu-id="92bc2-196">![[image]](10-working-with-video/_static/image2.jpg "ch08_video-2.jpg")</span></span>

<span data-ttu-id="92bc2-197">비디오를 자동으로 재생 하는 횟수를 나타내는 정수로 `playCount`를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-197">You can set `playCount` to an integer that indicates how many times to play the video automatically:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample6.cshtml)]

<span data-ttu-id="92bc2-198">`uiMode` 매개 변수를 사용 하 여 사용자 인터페이스에 표시 되는 컨트롤을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-198">The `uiMode` parameter lets you specify which controls show up in the user interface.</span></span> <span data-ttu-id="92bc2-199">`uiMode`을 `invisible`, `none`, `mini`또는 `full`로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-199">You can set `uiMode` to `invisible`, `none`, `mini`, or `full`.</span></span> <span data-ttu-id="92bc2-200">`uiMode` 매개 변수를 지정 하지 않으면 비디오 창 뿐만 아니라 상태 창, 검색 표시줄, 컨트롤 단추 및 볼륨 컨트롤과 함께 비디오가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-200">If you don't specify a `uiMode` parameter, the video will be displayed with the status window, seek bar, control buttons, and volume controls in addition to the video window.</span></span> <span data-ttu-id="92bc2-201">플레이어를 사용 하 여 오디오 파일을 재생 하는 경우에도 이러한 컨트롤이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-201">These controls will also be displayed if you use the player to play an audio file.</span></span> <span data-ttu-id="92bc2-202">`uiMode` 매개 변수를 사용 하는 방법의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-202">Here's an example of how to use the `uiMode` parameter:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample7.cshtml)]

<span data-ttu-id="92bc2-203">기본적으로 오디오는 비디오가 재생 될 때 켜 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-203">By default, audio is on when the video plays.</span></span> <span data-ttu-id="92bc2-204">`mute` 매개 변수를 true로 설정 하 여 오디오를 음소거 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-204">You can mute the audio by setting the `mute` parameter to true:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample8.cshtml)]

<span data-ttu-id="92bc2-205">`volume` 매개 변수를 0에서 100 사이의 값으로 설정 하 여 MediaPlayer 비디오의 오디오 수준을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-205">You can control the audio level of the MediaPlayer video by setting the `volume` parameter to a value between 0 and 100.</span></span> <span data-ttu-id="92bc2-206">기본값은 50입니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-206">The default value is 50.</span></span> <span data-ttu-id="92bc2-207">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-207">Here's an example:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample9.cshtml)]

<a id="Playing_Silverlight"></a>
## <a name="playing-silverlight-videos"></a><span data-ttu-id="92bc2-208">Silverlight 비디오 재생</span><span class="sxs-lookup"><span data-stu-id="92bc2-208">Playing Silverlight Videos</span></span>

<span data-ttu-id="92bc2-209">이 절차에서는 *Media*라는 폴더에 있는 Silverlight *.xap* 페이지에 포함 된 비디오를 재생 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-209">This procedure shows you how to play video contained in a Silverlight *.xap* page that's in a folder named *Media*.</span></span>

1. <span data-ttu-id="92bc2-210">[ASP.NET 웹 페이지 사이트에 도우미 설치](https://go.microsoft.com/fwlink/?LinkId=252372)에 설명 된 대로 ASP.NET 웹 도우미 라이브러리를 웹 사이트에 추가 합니다 (아직 없는 경우).</span><span class="sxs-lookup"><span data-stu-id="92bc2-210">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already .</span></span>
2. <span data-ttu-id="92bc2-211">*SilverlightVideo*라는 새 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-211">Create a new page named *SilverlightVideo.cshtml*.</span></span>
3. <span data-ttu-id="92bc2-212">페이지에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-212">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample10.cshtml)]
4. <span data-ttu-id="92bc2-213">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="92bc2-213">Run the page in a browser.</span></span> 

    <span data-ttu-id="92bc2-214">![이미지로](10-working-with-video/_static/image3.jpg "-3 ch08_video")</span><span class="sxs-lookup"><span data-stu-id="92bc2-214">![[image]](10-working-with-video/_static/image3.jpg "ch08_video-3.jpg")</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="92bc2-215">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="92bc2-215">Additional Resources</span></span>

<span data-ttu-id="92bc2-216">[Silverlight 개요](https://msdn.microsoft.com/library/bb404700(VS.95).aspx)</span><span class="sxs-lookup"><span data-stu-id="92bc2-216">[Silverlight Overview](https://msdn.microsoft.com/library/bb404700(VS.95).aspx)</span></span>

[<span data-ttu-id="92bc2-217">Flash 개체 및 EMBED 태그 특성</span><span class="sxs-lookup"><span data-stu-id="92bc2-217">Flash OBJECT and EMBED tag attributes</span></span>](http://kb2.adobe.com/cps/127/tn_12701.html)

<span data-ttu-id="92bc2-218">[Windows Media Player 11 SDK 매개 변수 태그](https://msdn.microsoft.com/library/aa392321(VS.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="92bc2-218">[Windows Media Player 11 SDK PARAM Tags](https://msdn.microsoft.com/library/aa392321(VS.85).aspx)</span></span>
