---
uid: web-forms/videos/how-do-i/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information
title: '[방법:] 사용자 지정 정보에 따라 ASP.NET 페이지의 캐싱 제어 | Microsoft Docs'
author: rick-anderson
description: 이 비디오에서 Chris Pel는 사용자 지정 정보에 따라 ASP.NET 페이지를 캐싱하는 조건을 제어 하는 방법을 보여 줍니다. 샘플 페이지가 생성 된 다음 O ...
ms.author: riande
ms.date: 02/19/2009
ms.assetid: f230c316-1313-4b8f-967c-62f9684fe378
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information
msc.type: video
ms.openlocfilehash: 676bc8f234a6e517104d07fd58a0ff14aec73e69
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506771"
---
# <a name="how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information"></a><span data-ttu-id="cf0ac-104">[방법:] 사용자 지정 정보에 따라 ASP.NET 페이지의 캐싱 제어</span><span class="sxs-lookup"><span data-stu-id="cf0ac-104">[How Do I:] Control the Caching of an ASP.NET Page Based Upon Custom Information</span></span>

<span data-ttu-id="cf0ac-105">사람- [Chris pel](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="cf0ac-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="cf0ac-106">이 비디오에서 Chris Pel는 사용자 지정 정보에 따라 ASP.NET 페이지를 캐싱하는 조건을 제어 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-106">In this video Chris Pels shows how to control the criteria for caching an ASP.NET page based upon custom information.</span></span> <span data-ttu-id="cf0ac-107">샘플 페이지가 만들어지고, 사용자 지정 값을 포함 하는 VaryByCustom 특성과 함께 OutputCache 지시어가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-107">A sample page is created and then the OutputCache directive is used with the VaryByCustom attribute which contains a custom value.</span></span> <span data-ttu-id="cf0ac-108">그런 다음, GetVaryCustomByString () 메서드는 global.asax 모듈에서 재정의 되어 사용자 지정 특성의 처리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-108">Next, the GetVaryCustomByString() method is overridden in the global.asax module which provides the handling of the custom attribute.</span></span> <span data-ttu-id="cf0ac-109">이 메서드에서는 캐시 된 버전의 페이지를 고유 하 게 식별 하는 문자열이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-109">In that method a string is returned that uniquely identifies the cached version of the page.</span></span> <span data-ttu-id="cf0ac-110">마지막으로, 사용자 지정 값을 사용 하는 캐싱이 웹 사이트의 여러 가지 방법으로 사용 되는 방법에 대 한 논의가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-110">Finally, there is a discussion about how caching using a custom value can be used in several ways for a web site.</span></span>

[<span data-ttu-id="cf0ac-111">&#9654;비디오 보기 (12 분)</span><span class="sxs-lookup"><span data-stu-id="cf0ac-111">&#9654; Watch video (12 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-control-the-caching-of-an-aspnet-page-based-upon-custom-information)
