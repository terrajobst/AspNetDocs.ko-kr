---
uid: web-forms/videos/how-do-i/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header
title: '[방법:]  HTTP 헤더의 정보에 따라 ASP.NET 페이지를 캐시 합니다. | Microsoft Docs'
author: rick-anderson
description: 이 비디오에서 Chris Pel는 페이지의 HTTP 헤더에 있는 정보에 따라 페이지를 ASP.NET 출력 캐시에 유지 하는 방법을 보여 줍니다. 첫째, 가능한 HTTP를 ...
ms.author: riande
ms.date: 02/26/2009
ms.assetid: 0f8df1bd-080a-4eeb-980c-c2fbb05d30c2
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header
msc.type: video
ms.openlocfilehash: 79c27f39793a4a3a94ea412838fb3844579e874d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506975"
---
# <a name="how-do-i--cache-an-aspnet-page-based-upon-information-in-the-http-header"></a><span data-ttu-id="d7391-104">[방법:]  HTTP 헤더의 정보에 따라 ASP.NET 페이지를 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7391-104">[How Do I:]  Cache an ASP.NET Page Based Upon Information in the HTTP Header</span></span>

<span data-ttu-id="d7391-105">사람- [Chris pel](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="d7391-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="d7391-106">이 비디오에서 Chris Pel는 페이지의 HTTP 헤더에 있는 정보에 따라 페이지를 ASP.NET 출력 캐시에 유지 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d7391-106">In this video Chris Pels shows how to keep a page in the ASP.NET output cache based upon information in the page's HTTP header.</span></span> <span data-ttu-id="d7391-107">첫 번째는 잠재적 HTTP 헤더 값을 검토 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d7391-107">First, the potential HTTP header values are reviewed.</span></span> <span data-ttu-id="d7391-108">그런 다음 샘플 페이지를 만든 다음, OutputCache 지시문은 사용자 브라우저의 언어에 따라 캐싱을 제어 하는 "accept-language" (HTTP 헤더) 값을 포함 하는 VaryByHeader 특성과 함께 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7391-108">Then, a sample page is created and then the OutputCache directive is used with the VaryByHeader attribute which contains a value "accept-language", an HTTP header, to control caching based upon the language of the user's browser.</span></span> <span data-ttu-id="d7391-109">이 샘플 페이지는 영어로 설정 된 IE와 프랑스어를 사용 하도록 설정 된 FireFox에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7391-109">The sample page is viewed in IE which is set to English and then in FireFox which is set to use French.</span></span> <span data-ttu-id="d7391-110">마지막으로, web.config 파일에서 캐시 정의를 CacheProfile으로 이동 하는 옵션에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7391-110">Finally, the option to move the cache definition to a CacheProfile in the web.config file is discussed.</span></span>

[<span data-ttu-id="d7391-111">&#9654;비디오 보기 (12 분)</span><span class="sxs-lookup"><span data-stu-id="d7391-111">&#9654; Watch video (12 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-cache-an-aspnet-page-based-upon-information-in-the-http-header)
