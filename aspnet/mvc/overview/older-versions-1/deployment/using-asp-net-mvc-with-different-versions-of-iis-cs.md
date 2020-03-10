---
uid: mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-cs
title: 다른 버전의 IIS ()에서 ASP.NET MVCC#사용 () | Microsoft Docs
author: microsoft
description: 이 자습서에서는 다양 한 버전의 인터넷 정보 서비스에서 ASP.NET MVC 및 URL 라우팅을 사용 하는 방법에 대해 알아봅니다. 다른 전략을 배우고 있습니다 ...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: b0cf4a34-2c1d-4717-bb54-ff029e722990
msc.legacyurl: /mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-cs
msc.type: authoredcontent
ms.openlocfilehash: 3b0a9509c0600f3598fd1218a7b383430548d4c0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486527"
---
# <a name="using-aspnet-mvc-with-different-versions-of-iis-c"></a><span data-ttu-id="b050e-104">다양한 버전의 IIS에 ASP.NET MVC 사용(C#)</span><span class="sxs-lookup"><span data-stu-id="b050e-104">Using ASP.NET MVC with Different Versions of IIS (C#)</span></span>

<span data-ttu-id="b050e-105">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="b050e-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="b050e-106">이 자습서에서는 다양 한 버전의 인터넷 정보 서비스에서 ASP.NET MVC 및 URL 라우팅을 사용 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-106">In this tutorial, you learn how to use ASP.NET MVC, and URL Routing, with different versions of Internet Information Services.</span></span> <span data-ttu-id="b050e-107">Iis 7.0 (클래식 모드), IIS 6.0 및 이전 버전의 IIS에서 ASP.NET MVC를 사용 하기 위한 다양 한 전략에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-107">You learn different strategies for using ASP.NET MVC with IIS 7.0 (classic mode), IIS 6.0, and earlier versions of IIS.</span></span>

<span data-ttu-id="b050e-108">ASP.NET MVC 프레임 워크는 ASP.NET 라우팅에 의존 하 여 브라우저 요청을 컨트롤러 작업으로 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-108">The ASP.NET MVC framework depends on ASP.NET Routing to route browser requests to controller actions.</span></span> <span data-ttu-id="b050e-109">ASP.NET 라우팅을 활용 하기 위해 웹 서버에서 추가 구성 단계를 수행 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-109">In order to take advantage of ASP.NET Routing, you might have to perform additional configuration steps on your web server.</span></span> <span data-ttu-id="b050e-110">응용 프로그램의 인터넷 정보 서비스 (IIS) 버전과 요청 처리 모드에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-110">It all depends on the version of Internet Information Services (IIS) and the request processing mode for your application.</span></span>

<span data-ttu-id="b050e-111">다음은 다양 한 버전의 IIS에 대 한 요약입니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-111">Here's a summary of the different versions of IIS:</span></span>

- <span data-ttu-id="b050e-112">IIS 7.0 (통합 모드)-ASP.NET 라우팅을 사용 하는 데 필요한 특별 한 구성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-112">IIS 7.0 (integrated mode) - No special configuration necessary to use ASP.NET Routing.</span></span>
- <span data-ttu-id="b050e-113">IIS 7.0 (클래식 모드)-ASP.NET 라우팅을 사용 하기 위해 특별 한 구성을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-113">IIS 7.0 (classic mode) - You need to perform special configuration to use ASP.NET Routing.</span></span>
- <span data-ttu-id="b050e-114">IIS 6.0 이상-ASP.NET 라우팅을 사용 하기 위해 특별 한 구성을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-114">IIS 6.0 or below - You need to perform special configuration to use ASP.NET Routing.</span></span>

<span data-ttu-id="b050e-115">IIS의 최신 버전은 7.5 (Win7) 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-115">The latest version of IIS is version 7.5 (on Win7).</span></span> <span data-ttu-id="b050e-116">Iis의 IIS 7은 Windows Server 2008 및 VISTA/SP1 이상에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-116">IIS 7 of IIS is included with Windows Server 2008 AND VISTA/SP1 and higher.</span></span> <span data-ttu-id="b050e-117">또한 Home Basic을 제외한 모든 버전의 Vista 운영 체제에 IIS 7.0를 설치할 수 있습니다 ( [https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)참조).</span><span class="sxs-lookup"><span data-stu-id="b050e-117">You also can install IIS 7.0 on any version of the Vista operating system except Home Basic (see [https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)).</span></span>

<span data-ttu-id="b050e-118">IIS 7.0는 요청을 처리 하기 위한 두 가지 모드를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-118">IIS 7.0 supports two modes for processing requests.</span></span> <span data-ttu-id="b050e-119">통합 모드 또는 클래식 모드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-119">You can use integrated mode or classic mode.</span></span> <span data-ttu-id="b050e-120">통합 모드에서 IIS 7.0를 사용 하는 경우 특별 한 구성 단계를 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-120">You don't need to perform any special configuration steps when using IIS 7.0 in integrated mode.</span></span> <span data-ttu-id="b050e-121">그러나 클래식 모드에서 IIS 7.0를 사용 하는 경우 추가 구성을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-121">However, you do need to perform additional configuration when using IIS 7.0 in classic mode.</span></span>

<span data-ttu-id="b050e-122">Microsoft Windows Server 2003에는 IIS 6.0이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-122">Microsoft Windows Server 2003 includes IIS 6.0.</span></span> <span data-ttu-id="b050e-123">Windows Server 2003 운영 체제를 사용 하는 경우 IIS 6.0를 IIS 7.0로 업그레이드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-123">You cannot upgrade IIS 6.0 to IIS 7.0 when using the Windows Server 2003 operating system.</span></span> <span data-ttu-id="b050e-124">IIS 6.0를 사용 하는 경우 추가 구성 단계를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-124">You must perform additional configuration steps when using IIS 6.0.</span></span>

<span data-ttu-id="b050e-125">Microsoft Windows XP Professional에는 IIS 5.1이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-125">Microsoft Windows XP Professional includes IIS 5.1.</span></span> <span data-ttu-id="b050e-126">IIS 5.1를 사용 하는 경우 추가 구성 단계를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-126">You must perform additional configuration steps when using IIS 5.1.</span></span>

<span data-ttu-id="b050e-127">마지막으로 Microsoft Windows 2000 및 Microsoft Windows 2000 Professional에는 IIS 5.0가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-127">Finally, Microsoft Windows 2000 and Microsoft Windows 2000 Professional includes IIS 5.0.</span></span> <span data-ttu-id="b050e-128">IIS 5.0를 사용 하는 경우 추가 구성 단계를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-128">You must perform additional configuration steps when using IIS 5.0.</span></span>

## <a name="integrated-versus-classic-mode"></a><span data-ttu-id="b050e-129">통합 모드 및 클래식 모드</span><span class="sxs-lookup"><span data-stu-id="b050e-129">Integrated versus Classic Mode</span></span>

<span data-ttu-id="b050e-130">IIS 7.0는 서로 다른 두 가지 요청 처리 모드인 통합 및 클래식 모드를 사용 하 여 요청을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-130">IIS 7.0 can process requests using two different request processing modes: integrated and classic.</span></span> <span data-ttu-id="b050e-131">통합 모드는 더 나은 성능과 더 많은 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-131">Integrated mode provides better performance and more features.</span></span> <span data-ttu-id="b050e-132">클래식 모드는 이전 버전의 IIS와 이전 버전과의 호환성을 위해 포함 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-132">Classic mode is included for backwards compatibility with earlier versions of IIS.</span></span>

<span data-ttu-id="b050e-133">요청 처리 모드는 응용 프로그램 풀에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-133">The request processing mode is determined by the application pool.</span></span> <span data-ttu-id="b050e-134">응용 프로그램과 연결 된 응용 프로그램 풀을 확인 하 여 특정 웹 응용 프로그램에서 사용 하는 처리 모드를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-134">You can determine which processing mode is being used by a particular web application by determining the application pool associated with the application.</span></span> <span data-ttu-id="b050e-135">다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="b050e-135">Follow these steps:</span></span>

1. <span data-ttu-id="b050e-136">인터넷 정보 서비스 관리자를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-136">Launch the Internet Information Services Manager</span></span>
2. <span data-ttu-id="b050e-137">연결 창에서 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-137">In the Connections window, select an application</span></span>
3. <span data-ttu-id="b050e-138">작업 창에서 **기본 설정** 링크를 클릭 하 여 응용 프로그램 편집 대화 상자를 엽니다 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="b050e-138">In the Actions window, click the **Basic Settings** link to open the Edit Application dialog box (see Figure 1)</span></span>
4. <span data-ttu-id="b050e-139">선택한 응용 프로그램 풀을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-139">Take note of the Application pool selected.</span></span>

<span data-ttu-id="b050e-140">기본적으로 IIS는 **DefaultAppPool** 및 **클래식 .net AppPool**의 두 가지 응용 프로그램 풀을 지원 하도록 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-140">By default, IIS is configured to support two application pools: **DefaultAppPool** and **Classic .NET AppPool**.</span></span> <span data-ttu-id="b050e-141">DefaultAppPool를 선택 하면 응용 프로그램이 통합 요청 처리 모드로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-141">If DefaultAppPool is selected, then your application is running in integrated request processing mode.</span></span> <span data-ttu-id="b050e-142">클래식 .NET AppPool이 선택 되어 있으면 응용 프로그램이 클래식 요청 처리 모드로 실행 되 고 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-142">If Classic .NET AppPool is selected, your application is running in classic request processing mode.</span></span>

<span data-ttu-id="b050e-143">[새 프로젝트 대화 상자 ![](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b050e-143">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.png)</span></span>

<span data-ttu-id="b050e-144">**그림 1**: 요청 처리 모드 검색 ([전체 크기 이미지를 보려면 클릭](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="b050e-144">**Figure 1**: Detecting the request processing mode([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.png))</span></span>

<span data-ttu-id="b050e-145">응용 프로그램 편집 대화 상자에서 요청 처리 모드를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-145">Notice that you can modify the request processing mode within the Edit Application dialog box.</span></span> <span data-ttu-id="b050e-146">선택 단추를 클릭 하 고 응용 프로그램과 연결 된 응용 프로그램 풀을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-146">Click the Select button and change the application pool associated with the application.</span></span> <span data-ttu-id="b050e-147">클래식 모드에서 통합 모드로 ASP.NET 응용 프로그램을 변경 하는 경우 호환성 문제가 있음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-147">Realize that there are compatibility issues when changing an ASP.NET application from classic to integrated mode.</span></span> <span data-ttu-id="b050e-148">자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b050e-148">For more information, see the following articles:</span></span>

- <span data-ttu-id="b050e-149">Windows Vista 및 Windows Server 2008에서 ASP.NET 1.1를 IIS 7.0로 업그레이드 [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)</span><span class="sxs-lookup"><span data-stu-id="b050e-149">Upgrading ASP.NET 1.1 to IIS 7.0 on Windows Vista and Windows Server 2008 -- [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)</span></span>
- <span data-ttu-id="b050e-150">ASP.NET와 IIS 7.0 통합- [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)</span><span class="sxs-lookup"><span data-stu-id="b050e-150">ASP.NET Integration With IIS 7.0 - [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)</span></span>

<span data-ttu-id="b050e-151">ASP.NET 응용 프로그램에서 DefaultAppPool를 사용 하는 경우 추가 단계를 수행 하 여 ASP.NET 라우팅 (그리고 따라서 ASP.NET MVC)이 작동 하도록 할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-151">If an ASP.NET application is using the DefaultAppPool, then you don't need to perform any additional steps to get ASP.NET Routing (and therefore ASP.NET MVC) to work.</span></span> <span data-ttu-id="b050e-152">그러나 ASP.NET 응용 프로그램이 클래식 .NET AppPool을 사용 하도록 구성 된 경우에는 계속 해 서 읽기 작업을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-152">However, if the ASP.NET application is configured to use the Classic .NET AppPool then keep reading, you have more work to do.</span></span>

## <a name="using-aspnet-mvc-with-older-versions-of-iis"></a><span data-ttu-id="b050e-153">이전 버전의 IIS에서 ASP.NET MVC 사용</span><span class="sxs-lookup"><span data-stu-id="b050e-153">Using ASP.NET MVC with Older Versions of IIS</span></span>

<span data-ttu-id="b050e-154">Iis 7.0 보다 이전 버전의 IIS에서 ASP.NET MVC를 사용 해야 하거나 클래식 모드에서 IIS 7.0를 사용 해야 하는 경우에는 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-154">If you need to use ASP.NET MVC with an older version of IIS than IIS 7.0, or you need to use IIS 7.0 in classic mode, then you have two options.</span></span> <span data-ttu-id="b050e-155">먼저, 경로 테이블을 수정 하 여 파일 확장명을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-155">First, you can modify the route table to use file extensions.</span></span> <span data-ttu-id="b050e-156">예를 들어/Dv/cvdetails와 같은 URL을 요청 하는 대신/Store.aspx/Details.와 같은 URL을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-156">For example, instead of requesting a URL like /Store/Details, you would request a URL like /Store.aspx/Details.</span></span>

<span data-ttu-id="b050e-157">두 번째 옵션은 *와일드 카드 스크립트 맵*이라는 항목을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-157">The second option is to create something called a *wildcard script map*.</span></span> <span data-ttu-id="b050e-158">와일드 카드 스크립트 맵을 사용 하면 모든 요청을 ASP.NET 프레임 워크에 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-158">A wildcard script map enables you to map every request into the ASP.NET framework.</span></span>

<span data-ttu-id="b050e-159">웹 서버에 대 한 액세스 권한이 없는 경우 (예: ASP.NET MVC 응용 프로그램이 인터넷 서비스 공급자에 의해 호스트 되는 경우) 첫 번째 옵션을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-159">If you don't have access to your web server (for example, your ASP.NET MVC application is being hosted by an Internet Service Provider) then you'll need to use the first option.</span></span> <span data-ttu-id="b050e-160">Url의 모양을 수정 하지 않고 웹 서버에 액세스할 수 있는 경우 두 번째 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-160">If you don't want to modify the appearance of your URLs, and you have access to your web server, then you can use the second option.</span></span>

<span data-ttu-id="b050e-161">다음 섹션에서 각 옵션에 대해 자세히 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-161">We explore each option in detail in the following sections.</span></span>

## <a name="adding-extensions-to-the-route-table"></a><span data-ttu-id="b050e-162">경로 테이블에 확장 추가</span><span class="sxs-lookup"><span data-stu-id="b050e-162">Adding Extensions to the Route Table</span></span>

<span data-ttu-id="b050e-163">이전 버전의 IIS에서 작동 하도록 ASP.NET 라우팅을 가져오는 가장 쉬운 방법은 global.asax 파일에서 경로 테이블을 수정 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-163">The easiest way to get ASP.NET Routing to work with older versions of IIS is to modify your route table in the Global.asax file.</span></span> <span data-ttu-id="b050e-164">목록 1의 기본 및 수정 되지 않은 global.asax 파일은 기본 경로 라는 하나의 경로를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-164">The default and unmodified Global.asax file in Listing 1 configures one route named the Default route.</span></span>

<span data-ttu-id="b050e-165">**목록 1-global.asax (수정 되지 않음)**</span><span class="sxs-lookup"><span data-stu-id="b050e-165">**Listing 1 - Global.asax (unmodified)**</span></span>

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample1.cs)]

<span data-ttu-id="b050e-166">목록 1에서 구성 된 기본 경로를 사용 하면 다음과 같은 Url을 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-166">The Default route configured in Listing 1 enables you to route URLs that look like this:</span></span>

<span data-ttu-id="b050e-167">/Home/Index</span><span class="sxs-lookup"><span data-stu-id="b050e-167">/Home/Index</span></span>

<span data-ttu-id="b050e-168">/Product/Details/3</span><span class="sxs-lookup"><span data-stu-id="b050e-168">/Product/Details/3</span></span>

<span data-ttu-id="b050e-169">/Product</span><span class="sxs-lookup"><span data-stu-id="b050e-169">/Product</span></span>

<span data-ttu-id="b050e-170">아쉽게도 이전 버전의 IIS는 이러한 요청을 ASP.NET 프레임 워크에 전달 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-170">Unfortunately, older versions of IIS won't pass these requests to the ASP.NET framework.</span></span> <span data-ttu-id="b050e-171">따라서 이러한 요청은 컨트롤러에 라우팅되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-171">Therefore, these requests won't get routed to a controller.</span></span> <span data-ttu-id="b050e-172">예를 들어/Home/Index URL에 대 한 브라우저 요청을 만들면 그림 2의 오류 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-172">For example, if you make a browser request for the URL /Home/Index then you'll get the error page in Figure 2.</span></span>

<span data-ttu-id="b050e-173">[새 프로젝트 대화 상자 ![](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="b050e-173">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.png)</span></span>

<span data-ttu-id="b050e-174">**그림 2**: 404를 찾을 수 없음 오류 수신 ([전체 크기 이미지를 보려면 클릭](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="b050e-174">**Figure 2**: Receiving a 404 Not Found error([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.png))</span></span>

<span data-ttu-id="b050e-175">이전 버전의 IIS는 특정 요청을 ASP.NET 프레임 워크에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-175">Older versions of IIS only map certain requests to the ASP.NET framework.</span></span> <span data-ttu-id="b050e-176">올바른 파일 확장명을 포함 하는 URL에 대 한 요청 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-176">The request must be for a URL with the right file extension.</span></span> <span data-ttu-id="b050e-177">예를 들어/SomePage.aspx에 대 한 요청은 ASP.NET 프레임 워크에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-177">For example, a request for /SomePage.aspx gets mapped to the ASP.NET framework.</span></span> <span data-ttu-id="b050e-178">그러나/SomePage.htm에 대 한 요청은 그렇지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-178">However, a request for /SomePage.htm does not.</span></span>

<span data-ttu-id="b050e-179">따라서 ASP.NET 라우팅이 작동 하려면 ASP.NET 프레임 워크에 매핑되는 파일 확장명을 포함 하도록 기본 경로를 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-179">Therefore, to get ASP.NET Routing to work, we must modify the Default route so that it includes a file extension that is mapped to the ASP.NET framework.</span></span>

<span data-ttu-id="b050e-180">`registermvc.wsf`이라는 스크립트를 사용 하 여이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-180">This is done using a script named `registermvc.wsf`.</span></span> <span data-ttu-id="b050e-181">ASP.NET MVC 1 릴리스에는 `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`에 포함 되어 있지만 ASP.NET 2부터이 스크립트는 [http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978)에서 사용할 수 있는 ASP.NET 퓨처로 이동 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-181">It was included with the ASP.NET MVC 1 release in `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`, but as of ASP.NET 2 this script has been moved to the ASP.NET Futures, available at [http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978).</span></span>

<span data-ttu-id="b050e-182">이 스크립트를 실행 하면 IIS를 사용 하 여 새로운 mvc 확장이 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-182">Executing this script registers a new .mvc extension with IIS.</span></span> <span data-ttu-id="b050e-183">Mvc 확장명을 등록 한 후에는 Global.asax 파일에서 경로를 수정 하 여 경로에. i a g 확장명을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-183">After you register the .mvc extension, you can modify your routes in the Global.asax file so that the routes use the .mvc extension.</span></span>

<span data-ttu-id="b050e-184">목록 2에서 수정 된 global.asax 파일은 이전 버전의 IIS와 함께 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-184">The modified Global.asax file in Listing 2 works with older versions of IIS.</span></span>

<span data-ttu-id="b050e-185">**목록 2-global.asax (확장으로 수정 됨)**</span><span class="sxs-lookup"><span data-stu-id="b050e-185">**Listing 2 - Global.asax (modified with extensions)**</span></span>

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample2.cs)]

<span data-ttu-id="b050e-186">**중요**: global.asax 파일을 변경한 후 ASP.NET MVC 응용 프로그램을 다시 빌드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-186">**Important**: remember to build your ASP.NET MVC Application again after changing the Global.asax file.</span></span>

<span data-ttu-id="b050e-187">목록 2의 Global.asax 파일에는 두 가지 중요 한 변경 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-187">There are two important changes to the Global.asax file in Listing 2.</span></span> <span data-ttu-id="b050e-188">이제 Global.asax에 정의 된 두 개의 경로가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-188">There are now two routes defined in the Global.asax.</span></span> <span data-ttu-id="b050e-189">기본 경로에 대 한 URL 패턴 인 첫 번째 경로는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-189">The URL pattern for the Default route, the first route, now looks like:</span></span>

<span data-ttu-id="b050e-190">{controller}.mvc/{action}/{id}</span><span class="sxs-lookup"><span data-stu-id="b050e-190">{controller}.mvc/{action}/{id}</span></span>

<span data-ttu-id="b050e-191">. M a m 확장명을 추가 하면 ASP.NET 라우팅 모듈이 가로채는 파일 형식을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-191">The addition of the .mvc extension changes the type of files that the ASP.NET Routing module intercepts.</span></span> <span data-ttu-id="b050e-192">이러한 변경으로 ASP.NET MVC 응용 프로그램은 이제 다음과 같은 요청을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-192">With this change, the ASP.NET MVC application now routes requests like the following:</span></span>

<span data-ttu-id="b050e-193">/Home.mvc/Index/</span><span class="sxs-lookup"><span data-stu-id="b050e-193">/Home.mvc/Index/</span></span>

<span data-ttu-id="b050e-194">/Product.mvc/Details/3</span><span class="sxs-lookup"><span data-stu-id="b050e-194">/Product.mvc/Details/3</span></span>

<span data-ttu-id="b050e-195">/Product.mvc/</span><span class="sxs-lookup"><span data-stu-id="b050e-195">/Product.mvc/</span></span>

<span data-ttu-id="b050e-196">두 번째 경로인 루트 경로는 new입니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-196">The second route, the Root route, is new.</span></span> <span data-ttu-id="b050e-197">루트 경로에 대 한이 URL 패턴은 빈 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-197">This URL pattern for the Root route is an empty string.</span></span> <span data-ttu-id="b050e-198">이 경로는 응용 프로그램의 루트에 대해 수행 된 요청을 일치 시키는 데 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-198">This route is necessary for matching requests made against the root of your application.</span></span> <span data-ttu-id="b050e-199">예를 들어 루트 경로는 다음과 같은 요청과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-199">For example, the Root route will match a request that looks like this:</span></span>

[http://www.YourApplication.com/](http://www.YourApplication.com/)

<span data-ttu-id="b050e-200">경로 테이블을 수정한 후에는 응용 프로그램의 모든 링크가 이러한 새 URL 패턴과 호환 되는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-200">After making these modifications to your route table, you'll need to make sure that all of the links in your application are compatible with these new URL patterns.</span></span> <span data-ttu-id="b050e-201">즉, 모든 링크에 해당 하는 확장명을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-201">In other words, make sure that all of your links include the .mvc extension.</span></span> <span data-ttu-id="b050e-202">Html.actionlink () 도우미 메서드를 사용 하 여 링크를 생성 하는 경우 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-202">If you use the Html.ActionLink() helper method to generate your links, then you should not need to make any changes.</span></span>

<span data-ttu-id="b050e-203">Registermvc. wcf 스크립트를 사용 하는 대신 ASP.NET framework에 직접 매핑된 IIS에 새 확장을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-203">Instead of using the registermvc.wcf script, you can add a new extension to IIS that is mapped to the ASP.NET framework by hand.</span></span> <span data-ttu-id="b050e-204">새 확장을 직접 추가 하는 경우 **해당 파일이 있는지 확인** 확인란을 선택 하지 않았는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-204">When adding a new extension yourself, make sure that the checkbox labeled **Verify that file exists** is not checked.</span></span>

## <a name="hosted-server"></a><span data-ttu-id="b050e-205">호스팅된 서버</span><span class="sxs-lookup"><span data-stu-id="b050e-205">Hosted Server</span></span>

<span data-ttu-id="b050e-206">웹 서버에 대 한 액세스 권한이 항상 있는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-206">You don't always have access to your web server.</span></span> <span data-ttu-id="b050e-207">예를 들어 인터넷 호스팅 공급자를 사용 하 여 ASP.NET MVC 응용 프로그램을 호스트 하는 경우 IIS에 대 한 액세스 권한이 반드시 있어야 하는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-207">For example, if you are hosting your ASP.NET MVC application using an Internet Hosting Provider, then you won't necessarily have access to IIS.</span></span>

<span data-ttu-id="b050e-208">이 경우 ASP.NET framework에 매핑되는 기존 파일 확장명 중 하나를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-208">In that case, you should use one of the existing file extensions that are mapped to the ASP.NET framework.</span></span> <span data-ttu-id="b050e-209">ASP.NET에 매핑되는 파일 확장명의 예로는 .aspx, trace.axd 및 .ashx 확장명이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-209">Examples of file extensions mapped to ASP.NET include the .aspx, .axd, and .ashx extensions.</span></span>

<span data-ttu-id="b050e-210">예를 들어 목록 3의 수정 된 global.asax 파일은. x 확장명 대신 .aspx 확장명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-210">For example, the modified Global.asax file in Listing 3 uses the .aspx extension instead of the .mvc extension.</span></span>

<span data-ttu-id="b050e-211">**목록 3-global.asax (.aspx 확장명으로 수정 됨)**</span><span class="sxs-lookup"><span data-stu-id="b050e-211">**Listing 3 - Global.asax (modified with .aspx extensions)**</span></span>

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample3.cs)]

<span data-ttu-id="b050e-212">목록 3의 Global.asax 파일은 이전 global.asax 파일과 정확히 동일 합니다. 단,이 파일은 확장명이. x x x 인 확장명이 아닌 .aspx 확장명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-212">The Global.asax file in Listing 3 is exactly the same as the previous Global.asax file except for the fact that it uses the .aspx extension instead of the .mvc extension.</span></span> <span data-ttu-id="b050e-213">.Aspx 확장을 사용 하기 위해 원격 웹 서버에서 설치를 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-213">You don't have to perform any setup on your remote web server to use the .aspx extension.</span></span>

## <a name="creating-a-wildcard-script-map"></a><span data-ttu-id="b050e-214">와일드 카드 스크립트 매핑 만들기</span><span class="sxs-lookup"><span data-stu-id="b050e-214">Creating a Wildcard Script Map</span></span>

<span data-ttu-id="b050e-215">ASP.NET MVC 응용 프로그램에 대 한 Url을 수정 하지 않고 웹 서버에 액세스할 수 있는 경우에는 추가 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-215">If you don't want to modify the URLs for your ASP.NET MVC application, and you have access to your web server, then you have an additional option.</span></span> <span data-ttu-id="b050e-216">웹 서버에 대 한 모든 요청을 ASP.NET 프레임 워크로 매핑하는 와일드 카드 스크립트 맵을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-216">You can create a wildcard script map that maps all requests to the web server to the ASP.NET framework.</span></span> <span data-ttu-id="b050e-217">이렇게 하면 기본 ASP.NET MVC 경로 테이블을 IIS 7.0 (클래식 모드) 또는 IIS 6.0과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-217">That way, you can use the default ASP.NET MVC route table with IIS 7.0 (in classic mode) or IIS 6.0.</span></span>

<span data-ttu-id="b050e-218">이 옵션을 선택 하면 IIS에서 웹 서버에 대해 수행 된 모든 요청을 가로챕니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-218">Be aware that this option causes IIS to intercept every request made against the web server.</span></span> <span data-ttu-id="b050e-219">여기에는 이미지, 기본 ASP 페이지 및 HTML 페이지에 대 한 요청이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-219">This includes requests for images, classic ASP pages, and HTML pages.</span></span> <span data-ttu-id="b050e-220">따라서 와일드 카드 스크립트 맵을 ASP.NET에 사용 하도록 설정 하면 성능에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-220">Therefore, enabling a wildcard script map to ASP.NET does have performance implications.</span></span>

<span data-ttu-id="b050e-221">IIS 7.0에 대 한 와일드 카드 스크립트 맵을 사용 하도록 설정 하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-221">Here's how you enable a wildcard script map for IIS 7.0:</span></span>

1. <span data-ttu-id="b050e-222">연결 창에서 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-222">Select your application in the Connections window</span></span>
2. <span data-ttu-id="b050e-223">**기능** 보기가 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-223">Make sure that the **Features** view is selected</span></span>
3. <span data-ttu-id="b050e-224">**처리기 매핑** 단추를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-224">Double-click the **Handler Mappings** button</span></span>
4. <span data-ttu-id="b050e-225">**와일드 카드 스크립트 매핑 추가** 링크를 클릭 합니다 (그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="b050e-225">Click the **Add Wildcard Script Map** link (see Figure 3)</span></span>
5. <span data-ttu-id="b050e-226">Aspnet\_isapi .dll 파일의 경로를 입력 합니다 (이 경로를 PageHandlerFactory 스크립트 맵에서 복사할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="b050e-226">Enter the path to the aspnet\_isapi.dll file (You can copy this path from the PageHandlerFactory script map)</span></span>
6. <span data-ttu-id="b050e-227">이름 MVC 입력</span><span class="sxs-lookup"><span data-stu-id="b050e-227">Enter the name MVC</span></span>
7. <span data-ttu-id="b050e-228">**확인** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-228">Click the **OK** button</span></span>

<span data-ttu-id="b050e-229">[새 프로젝트 대화 상자 ![](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="b050e-229">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.png)</span></span>

<span data-ttu-id="b050e-230">**그림 3**: IIS 7.0를 사용 하 여 와일드 카드 스크립트 매핑 만들기 ([전체 크기 이미지를 보려면 클릭](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="b050e-230">**Figure 3**: Creating a wildcard script map with IIS 7.0([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image6.png))</span></span>

<span data-ttu-id="b050e-231">IIS 6.0를 사용 하 여 와일드 카드 스크립트 맵을 만들려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="b050e-231">Follow these steps to create a wildcard script map with IIS 6.0:</span></span>

1. <span data-ttu-id="b050e-232">웹 사이트를 마우스 오른쪽 단추로 클릭 하 고 속성을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-232">Right-click a website and select Properties</span></span>
2. <span data-ttu-id="b050e-233">**홈 디렉터리** 탭을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-233">Select the **Home Directory** tab</span></span>
3. <span data-ttu-id="b050e-234">**구성** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-234">Click the **Configuration** button</span></span>
4. <span data-ttu-id="b050e-235">**매핑** 탭 선택</span><span class="sxs-lookup"><span data-stu-id="b050e-235">Select the **Mappings** tab</span></span>
5. <span data-ttu-id="b050e-236">**삽입** 단추를 클릭 합니다 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="b050e-236">Click the **Insert** button (see Figure 4)</span></span>
6. <span data-ttu-id="b050e-237">Aspnet\_의 경로를 실행 파일 필드에 붙여넣습니다 (.aspx 파일에 대 한 스크립트 맵에서이 경로를 복사할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="b050e-237">Paste the path to the aspnet\_isapi.dll into the Executable field (you can copy this path from the script map for .aspx files)</span></span>
7. <span data-ttu-id="b050e-238">**해당 파일이 있는지 확인** 이라는 레이블이 지정 된 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-238">Uncheck the checkbox labeled **Verify that file exists**</span></span>
8. <span data-ttu-id="b050e-239">**확인** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-239">Click the **OK** button</span></span>

<span data-ttu-id="b050e-240">[새 프로젝트 대화 상자 ![](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="b050e-240">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image7.png)</span></span>

<span data-ttu-id="b050e-241">**그림 4**: IIS 6.0를 사용 하 여 와일드 카드 스크립트 매핑 만들기 ([전체 크기 이미지를 보려면 클릭](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="b050e-241">**Figure 4**: Creating a wildcard script map with IIS 6.0([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image8.png))</span></span>

<span data-ttu-id="b050e-242">와일드 카드 스크립트 맵을 사용 하도록 설정한 후에는 루트 경로를 포함 하도록 Global.asax 파일의 경로 테이블을 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-242">After you enable wildcard script maps, you need to modify the route table in the Global.asax file so that it includes a Root route.</span></span> <span data-ttu-id="b050e-243">그렇지 않으면 응용 프로그램의 루트 페이지에 대 한 요청을 수행할 때 그림 5의 오류 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-243">Otherwise, you'll get the error page in Figure 5 when you make a request for the root page of your application.</span></span> <span data-ttu-id="b050e-244">목록 4에서 수정 된 global.asax 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-244">You can use the modified Global.asax file in Listing 4.</span></span>

<span data-ttu-id="b050e-245">[새 프로젝트 대화 상자 ![](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="b050e-245">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image9.png)</span></span>

<span data-ttu-id="b050e-246">**그림 5**: 루트 경로 오류 누락 ([전체 크기 이미지를 보려면 클릭](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="b050e-246">**Figure 5**: Missing Root route error([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image10.png))</span></span>

<span data-ttu-id="b050e-247">**목록 4-global.asax (루트 경로를 사용 하 여 수정 됨)**</span><span class="sxs-lookup"><span data-stu-id="b050e-247">**Listing 4 - Global.asax (modified with Root route)**</span></span>

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample4.cs)]

<span data-ttu-id="b050e-248">IIS 7.0 또는 IIS 6.0에 대해 와일드 카드 스크립트 맵을 사용 하도록 설정한 후 다음과 같이 기본 경로 테이블에서 작동 하는 요청을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-248">After you enable a wildcard script map for either IIS 7.0 or IIS 6.0, you can make requests that work with the default route table that look like this:</span></span>

/

<span data-ttu-id="b050e-249">/Home/Index</span><span class="sxs-lookup"><span data-stu-id="b050e-249">/Home/Index</span></span>

<span data-ttu-id="b050e-250">/Product/Details/3</span><span class="sxs-lookup"><span data-stu-id="b050e-250">/Product/Details/3</span></span>

<span data-ttu-id="b050e-251">/Product</span><span class="sxs-lookup"><span data-stu-id="b050e-251">/Product</span></span>

## <a name="summary"></a><span data-ttu-id="b050e-252">요약</span><span class="sxs-lookup"><span data-stu-id="b050e-252">Summary</span></span>

<span data-ttu-id="b050e-253">이 자습서의 목표는 이전 버전의 IIS를 사용 하는 경우 ASP.NET MVC를 사용 하는 방법, 즉 클래식 모드에서 IIS 7.0를 사용 하는 방법을 설명 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-253">The goal of this tutorial was to explain how you can use ASP.NET MVC when using an older version of IIS (or IIS 7.0 in classic mode).</span></span> <span data-ttu-id="b050e-254">ASP.NET 라우팅은 이전 버전의 IIS에서 작동 하는 두 가지 방법, 즉 기본 경로 테이블 수정 또는 와일드 카드 스크립트 맵 만들기에 대해 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-254">We discussed two methods of getting ASP.NET Routing to work with older versions of IIS: Modify the default route table or create a wildcard script map.</span></span>

<span data-ttu-id="b050e-255">첫 번째 옵션을 사용 하려면 ASP.NET MVC 응용 프로그램에서 사용 되는 Url을 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-255">The first option requires you to modify the URLs used in your ASP.NET MVC application.</span></span> <span data-ttu-id="b050e-256">이 첫 번째 옵션의 가장 큰 이점 중 하나는 경로 테이블을 수정 하기 위해 웹 서버에 액세스할 필요가 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-256">One very significant advantage of this first option is that you do not need access to a web server in order to modify the route table.</span></span> <span data-ttu-id="b050e-257">즉, 인터넷 호스팅 회사에서 ASP.NET MVC 응용 프로그램을 호스트 하는 경우에도이 첫 번째 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-257">That means that you can use this first option even when hosting your ASP.NET MVC application with an Internet hosting company.</span></span>

<span data-ttu-id="b050e-258">두 번째 옵션은 와일드 카드 스크립트 맵을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-258">The second option is to create a wildcard script map.</span></span> <span data-ttu-id="b050e-259">이 두 번째 옵션은 Url을 수정할 필요가 없다는 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-259">The advantage of this second option is that you do not need to modify your URLs.</span></span> <span data-ttu-id="b050e-260">이 두 번째 옵션의 단점은 ASP.NET MVC 응용 프로그램의 성능에 영향을 줄 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b050e-260">The disadvantage of this second option is that it can impact the performance of your ASP.NET MVC application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="b050e-261">다음</span><span class="sxs-lookup"><span data-stu-id="b050e-261">Next</span></span>](using-asp-net-mvc-with-different-versions-of-iis-vb.md)
