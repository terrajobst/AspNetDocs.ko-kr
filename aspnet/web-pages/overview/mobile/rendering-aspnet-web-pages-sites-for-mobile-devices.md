---
uid: web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
title: 모바일 장치용 Razor (ASP.NET 웹 페이지) 사이트 렌더링 | Microsoft Docs
author: Rick-Anderson
description: '이 문서에서는 모바일 장치에서 적절히 렌더링 되는 ASP.NET 웹 페이지 (Razor) 사이트에서 페이지를 만드는 방법을 설명 합니다. 학습 내용: 방법 ...'
ms.author: riande
ms.date: 02/17/2014
ms.assetid: f15ab392-c05e-4269-83bf-7c6d2b8c8ec8
msc.legacyurl: /web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
msc.type: authoredcontent
ms.openlocfilehash: c012348d65e48a275cb0e4808fef2a7f31e5fb33
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454355"
---
# <a name="rendering-aspnet-web-pages-razor-sites-for-mobile-devices"></a><span data-ttu-id="81912-104">모바일 장치용 Razor (ASP.NET 웹 페이지) 사이트 렌더링</span><span class="sxs-lookup"><span data-stu-id="81912-104">Rendering ASP.NET Web Pages (Razor) Sites for Mobile Devices</span></span>

<span data-ttu-id="81912-105">만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="81912-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="81912-106">이 문서에서는 모바일 장치에서 적절히 렌더링 되는 ASP.NET 웹 페이지 (Razor) 사이트에서 페이지를 만드는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="81912-106">This article describes how to create pages in an ASP.NET Web Pages (Razor) site that will render appropriately on mobile devices.</span></span>
> 
> <span data-ttu-id="81912-107">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="81912-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="81912-108">명명 규칙을 사용 하 여 모바일 장치용으로 특별히 디자인 된 페이지를 지정 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="81912-108">How to use a naming convention to specify that a page is designed specifically for mobile devices.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="81912-109">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="81912-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="81912-110">ASP.NET 웹 페이지 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="81912-110">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="81912-111">이 자습서는 ASP.NET 웹 페이지 2 에서도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="81912-111">This tutorial also works with ASP.NET Web Pages 2.</span></span>

<span data-ttu-id="81912-112">ASP.NET 웹 페이지를 사용 하 여 모바일 또는 기타 장치에서 콘텐츠를 렌더링 하기 위한 사용자 지정 디스플레이를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81912-112">ASP.NET Web Pages lets you create custom displays for rendering content on mobile or other devices.</span></span>

<span data-ttu-id="81912-113">ASP.NET 웹 페이지 사이트에서 장치별 페이지를 만드는 가장 간단한 방법은 파일 이름 지정 패턴을 사용 하는 것입니다. 예: 파일 *이름. Mobile. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="81912-113">The simplest way to create device-specific page in an ASP.NET Web Pages site is by using a file-naming pattern like this: *FileName.Mobile.cshtml*.</span></span> <span data-ttu-id="81912-114">두 버전의 페이지를 만들 수 있습니다. 예를 들어 한 페이지의 페이지를 만들 수 있습니다 (예: *myfile* 및 이름이 *myfile*).</span><span class="sxs-lookup"><span data-stu-id="81912-114">You can create two versions of a page (for example, one named *MyFile.cshtml* and one named *MyFile.Mobile.cshtml*).</span></span> <span data-ttu-id="81912-115">런타임에 모바일 장치에서 *myfile. cshtml*를 요청 하면 ASP.NET는 *myfile*에서 콘텐츠를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="81912-115">At run time, when a mobile device requests *MyFile.cshtml*, ASP.NET renders the content from *MyFile.Mobile.cshtml*.</span></span> <span data-ttu-id="81912-116">그렇지 않으면 *MyFile* 이 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81912-116">Otherwise, *MyFile.cshtml* is rendered.</span></span>

<span data-ttu-id="81912-117">다음 예제에서는 모바일 장치에 대 한 콘텐츠 페이지를 추가 하 여 모바일 렌더링을 사용 하도록 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="81912-117">The following example shows how to enable mobile rendering by adding a content page for mobile devices.</span></span> <span data-ttu-id="81912-118">1 *. cshtml* 에는 콘텐츠와 탐색 사이드바가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81912-118">*Page1.cshtml* contains content plus a navigation sidebar.</span></span> <span data-ttu-id="81912-119">로 *이동 합니다. 휴대폰과* 동일한 콘텐츠를 포함 하지만 사이드바는 생략 합니다.</span><span class="sxs-lookup"><span data-stu-id="81912-119">*Page1.Mobile.cshtml* contains the same content, but omits the sidebar.</span></span>

1. <span data-ttu-id="81912-120">ASP.NET 웹 페이지 사이트에서 *파일 이름으로* 파일을 만들고 현재 콘텐츠를 다음 태그로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="81912-120">In an ASP.NET Web Pages site, create a file named *Page1.cshtml* and replace the current content with following markup.</span></span>

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample1.html)]
2. <span data-ttu-id="81912-121">파일 이름으로 파일을 *만들고, 기존* 내용을 다음 태그로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="81912-121">Create a file named *Page1.Mobile.cshtml* and replace the existing content with the following markup.</span></span> <span data-ttu-id="81912-122">더 작은 화면에서 렌더링 하기 쉽도록 페이지의 모바일 버전에 탐색 섹션이 생략 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81912-122">Notice that the mobile version of the page omits the navigation section for better rendering on a smaller screen.</span></span>

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample2.html)]
3. <span data-ttu-id="81912-123">바탕 화면 브라우저를 실행 하 고 1, *cshtml*로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="81912-123">Run a desktop browser and browse to *Page1.cshtml*.</span></span> <span data-ttu-id="81912-124">![mobilesites](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="81912-124">![mobilesites-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)</span></span>
4. <span data-ttu-id="81912-125">모바일 브라우저 (또는 모바일 장치 에뮬레이터)를 실행 하 고, 1, *cshtml*로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="81912-125">Run a mobile browser (or a mobile device emulator) and browse to *Page1.cshtml*.</span></span> <span data-ttu-id="81912-126">*. Mobile* 은 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="81912-126">(Notice that you do not include *.mobile.*</span></span> <span data-ttu-id="81912-127">URL의 일부로 포함 됩니다. 요청이 ASP.NET로 *이동* *하는 경우에도*는를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="81912-127">as part of the URL.) Even though the request is to *Page1.cshtml*, ASP.NET renders *Page1.Mobile.cshtml*.</span></span>

    ![mobilesites-2](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="81912-129">모바일 페이지를 테스트 하려면 데스크톱 컴퓨터에서 실행 되는 모바일 장치 시뮬레이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81912-129">To test mobile pages, you can use a mobile device simulator that runs on a desktop computer.</span></span> <span data-ttu-id="81912-130">이 도구를 사용 하면 모바일 장치 (일반적으로 훨씬 더 작은 표시 영역)에서 볼 수 있는 웹 페이지를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81912-130">This tool lets you test web pages as they would look on mobile devices (that is, typically with a much smaller display area).</span></span> <span data-ttu-id="81912-131">시뮬레이터의 한 가지 예는 Mozilla Firefox 용 [사용자 에이전트 전환기 추가 기능이](http://addons.mozilla.org/firefox/addon/user-agent-switcher/) 며,이 기능을 사용 하면 Firefox의 데스크톱 버전에서 다양 한 모바일 브라우저를 에뮬레이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81912-131">One example of a simulator is the [User Agent Switcher add-on](http://addons.mozilla.org/firefox/addon/user-agent-switcher/) for Mozilla Firefox, which lets you emulate various mobile browsers from a desktop version of Firefox.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="81912-132">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="81912-132">Additional Resources</span></span>

<span data-ttu-id="81912-133">[Windows Phone 에뮬레이터](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)</span><span class="sxs-lookup"><span data-stu-id="81912-133">[Windows Phone Emulator](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)</span></span>
