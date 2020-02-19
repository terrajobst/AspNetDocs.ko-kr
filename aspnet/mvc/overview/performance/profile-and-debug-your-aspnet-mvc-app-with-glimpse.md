---
uid: mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
title: ASP.NET MVC 앱을 사용 하 여 프로 파일링 및 디버그 | Microsoft Docs
author: Rick-Anderson
description: 그래픽용는 ASP.NET에 대 한 자세한 성능, 디버깅 및 진단 정보를 제공 하는 오픈 소스 NuGet 패키지의 패밀리입니다.
ms.author: riande
ms.date: 03/26/2015
ms.assetid: c205805f-efdd-4fa7-9616-f26eab180611
msc.legacyurl: /mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
msc.type: authoredcontent
ms.openlocfilehash: d3689147a3bc3aa1f4180c377d2483a94bdd95a9
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457663"
---
# <a name="profile-and-debug-your-aspnet-mvc-app-with-glimpse"></a><span data-ttu-id="18763-103">Glimpse를 사용하여 ASP.NET MVC 앱 프로파일링 및 디버그</span><span class="sxs-lookup"><span data-stu-id="18763-103">Profile and debug your ASP.NET MVC app with Glimpse</span></span>

<span data-ttu-id="18763-104">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="18763-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="18763-105">그래픽용는 ASP.NET apps에 대 한 자세한 성능, 디버깅 및 진단 정보를 제공 하는 오픈 소스 NuGet 패키지의 증가 하는 패밀리입니다.</span><span class="sxs-lookup"><span data-stu-id="18763-105">Glimpse is a thriving and growing family of open source NuGet packages that provides detailed performance, debugging and diagnostic information for ASP.NET apps.</span></span> <span data-ttu-id="18763-106">모든 페이지의 아래쪽에 주요 성능 메트릭을 설치 하 고 간단 하 고 신속 하 게 표시 하 고 표시 하는 것이 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="18763-106">It's trivial to install, lightweight, ultra-fast, and displays key performance metrics at the bottom of every page.</span></span> <span data-ttu-id="18763-107">서버에서 진행 되는 작업을 확인 해야 하는 경우 앱을 드릴 다운할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18763-107">It allows you to drill down into your app when you need to find out what's going on at the server.</span></span> <span data-ttu-id="18763-108">여기서는 Azure 테스트 환경을 포함 하 여 개발 주기 전체에서 사용 하는 것이 가장 중요 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="18763-108">Glimpse provides so much valuable information we recommend you use it throughout your development cycle, including your Azure test environment.</span></span> <span data-ttu-id="18763-109">[Fiddler](http://www.telerik.com/fiddler) 및 [F-12 개발 도구](https://msdn.microsoft.com/library/ie/gg589512(v=vs.85).aspx) 는 클라이언트 쪽 보기를 제공 하는 반면,는 서버에서 자세히 보기를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="18763-109">While [Fiddler](http://www.telerik.com/fiddler) and the [F-12 development tools](https://msdn.microsoft.com/library/ie/gg589512(v=vs.85).aspx) provide a client side view, Glimpse provides a detailed view from the server.</span></span> <span data-ttu-id="18763-110">이 자습서에서는 ASP.NET MVC 및 EF 패키지를 사용 하는 데 중점을 두고 있지만 다른 많은 패키지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18763-110">This tutorial will focus on using the Glimpse ASP.NET MVC and EF packages, but many other packages are available.</span></span> <span data-ttu-id="18763-111">가능 하면 유지 관리 하는 데 도움이 되는 적절 한 적절 한 [문서](http://getglimpse.com/Docs/) 에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="18763-111">Where possible I will link to the appropriate [Glimpse docs](http://getglimpse.com/Docs/) which I help maintain.</span></span> <span data-ttu-id="18763-112">예를 들어 오픈 소스 프로젝트는 소스 코드와 문서에 기여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18763-112">Glimpse is an open source project, you too can contribute to the source code and the docs.</span></span>

- [<span data-ttu-id="18763-113">설치 하는 중</span><span class="sxs-lookup"><span data-stu-id="18763-113">Installing Glimpse</span></span>](#ig)
- [<span data-ttu-id="18763-114">Localhost에 대해 잠깐 사용</span><span class="sxs-lookup"><span data-stu-id="18763-114">Enable Glimpse for localhost</span></span>](#eg)
- [<span data-ttu-id="18763-115">타임 라인 탭</span><span class="sxs-lookup"><span data-stu-id="18763-115">The Timeline tab</span></span>](#Time)
- [<span data-ttu-id="18763-116">모델 바인딩</span><span class="sxs-lookup"><span data-stu-id="18763-116">Model Binding</span></span>](#mb)
- [<span data-ttu-id="18763-117">경로</span><span class="sxs-lookup"><span data-stu-id="18763-117">Routes</span></span>](#route)
- [<span data-ttu-id="18763-118">Azure에서의 사용</span><span class="sxs-lookup"><span data-stu-id="18763-118">Using Glimpse on Azure</span></span>](#da)
- [<span data-ttu-id="18763-119">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="18763-119">Additional Resources</span></span>](#addRes)

<a id="ig"></a>
## <a name="installing-glimpse"></a><span data-ttu-id="18763-120">설치 하는 중</span><span class="sxs-lookup"><span data-stu-id="18763-120">Installing Glimpse</span></span>

<span data-ttu-id="18763-121">NuGet 패키지 관리자 콘솔 또는 **Nuget 패키지 관리** 콘솔에서이를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18763-121">You can install Glimpse from the NuGet package manager console or from the **Manage NuGet Packages** console.</span></span> <span data-ttu-id="18763-122">이 데모에서는 Mvc5 및 EF6 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="18763-122">For this demo, I'll install the Mvc5 and EF6 packages:</span></span>

![NuGet 대화 상자에서 잠깐 설치](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image1.png)

<span data-ttu-id="18763-124">간략 한 예를 검색 *합니다.*</span><span class="sxs-lookup"><span data-stu-id="18763-124">Search for *Glimpse.EF*</span></span>

![NuGet 설치 대화 상자에서의. EF](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image2.png)

<span data-ttu-id="18763-126">설치 된 **패키지**를 선택 하면 다음과 같은 확인 종속 모듈이 설치 된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18763-126">By selecting **Installed packages**, you can see the Glimpse dependent modules installed:</span></span>

![대화 상자에서 설치 된 간략 한 패키지](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image3.png)

<span data-ttu-id="18763-128">다음 명령은 패키지 관리자 콘솔에서 MVC5 및 EF6 모듈을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="18763-128">The following commands install Glimpse MVC5 and EF6 modules from the package manager console:</span></span>

[!code-console[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample1.cmd)]

<a id="eg"></a>
## <a name="enable-glimpse-for-localhost"></a><span data-ttu-id="18763-129">Localhost에 대해 잠깐 사용</span><span class="sxs-lookup"><span data-stu-id="18763-129">Enable Glimpse for localhost</span></span>

<span data-ttu-id="18763-130">http://localhost:&lt;p ort #&gt;/glimpse.axd로 이동 하 고, [ <strong>설정</strong> ] 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="18763-130">Navigate to http://localhost:&lt;port #&gt;/glimpse.axd and click the <strong>Turn Glimpse On</strong> button.</span></span>

![에서의이 페이지](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image4.png)

<span data-ttu-id="18763-132">즐겨찾기 표시줄이 표시 되어 있는 경우에는 해당 단추를 끌어 놓고 책갈피를 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18763-132">If you have your favorites bar displayed, you can drag and drop the Glimpse buttons and add them as bookmarklets:</span></span>

![이 책갈피를 사용 하 여 IE 사용](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image5.png)

<span data-ttu-id="18763-134">이제 앱을 탐색할 수 있으며 페이지 아래쪽에 HUD ( **헤드 준비) 표시** 가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18763-134">You can now navigate your app, and the **Heads Up Display** (HUD) is shown at the bottom of the page.</span></span>

![HUD를 사용 하는 연락처 관리자 페이지](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image6.png)

<span data-ttu-id="18763-136">[HUD](http://getglimpse.com/Docs/Heads-up-Display) 에서 위에 표시 된 타이밍 정보를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="18763-136">The [Glimpse HUD page](http://getglimpse.com/Docs/Heads-up-Display) details the timing information shown above.</span></span> <span data-ttu-id="18763-137">HUD 표시 되는 성능 저하 데이터는 테스트 주기를 시작 하기 전에 즉시 문제를 알릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18763-137">The unobtrusive performance data the HUD displays can notify you of a problem immediately - before you get to the test cycle.</span></span> <span data-ttu-id="18763-138">오른쪽 아래 모서리에 있는 &quot;g&quot;를 클릭 하면 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18763-138">Clicking on the &quot;g&quot; in the lower right corner brings up the Glimpse panel:</span></span>

![잠깐 패널](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image7.png)

<span data-ttu-id="18763-140">위의 이미지에서 [실행 탭](http://getglimpse.com/Docs/Execution-Tab) 이 선택 되어 파이프라인의 작업 및 필터에 대 한 타이밍 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="18763-140">In the image above, the [Execution tab](http://getglimpse.com/Docs/Execution-Tab) is selected, which shows timing details of the actions and filters in the pipeline.</span></span> <span data-ttu-id="18763-141">파이프라인의 6 단계에서 [중지 된 조사식 필터 타이머가](http://www.nuget.org/packages/StopWatch/) 시작 되는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18763-141">You can see my [Stop Watch filter timer](http://www.nuget.org/packages/StopWatch/) start at stage 6 of the pipeline.</span></span> <span data-ttu-id="18763-142">내 광원 가중치 타이머가 유용한 프로필/타이밍 데이터를 제공할 수 있지만 뷰를 권한 부여 및 렌더링 하는 데 소요 된 모든 시간이 누락 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18763-142">While my light weight timer can provide useful profile/timing data, it misses all the time spent in authorization and rendering the view.</span></span> <span data-ttu-id="18763-143">[Azure에 대 한 ASP.NET MVC 앱의 프로필 및 시간](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx)에서 내 타이머를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18763-143">You can read about my timer at [Profile and Time your ASP.NET MVC app all the way to Azure](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx).</span></span> <span data-ttu-id="18763-144">탭 [페이지는](http://getglimpse.com/Docs/Tabs) 각 탭의 자세한 정보에 대 한 링크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="18763-144">The [Tabs](http://getglimpse.com/Docs/Tabs) page provides links to detailed information on each tab.</span></span>

<a id="Time"></a>
## <a name="the-timeline-tab"></a><span data-ttu-id="18763-145">타임 라인 탭</span><span class="sxs-lookup"><span data-stu-id="18763-145">The Timeline tab</span></span>

<span data-ttu-id="18763-146">강사 컨트롤러에 대 한 다음 코드를 변경 하 여 Tom Dykstra의 처리 중인 [EF 6/MVC 5 자습서](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) 를 수정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="18763-146">I've modified Tom Dykstra's outstanding [EF 6/MVC 5 tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) with the following code change to the instructors controller:</span></span>

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample2.cs?highlight=1,20-31)]

<span data-ttu-id="18763-147">위의 코드는 쿼리 문자열 (`eager`)을 전달 하 여 데이터의 즉시 또는 명시적 로드를 제어 하도록 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="18763-147">The code above allows me to pass in query string (`eager`) to control eager or explicit loading of data.</span></span> <span data-ttu-id="18763-148">아래 이미지에서는 명시적 로드를 사용 하며, 타이밍 페이지에는 `Index` 동작 메서드에서 로드 된 각 등록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18763-148">In the image below, explicit loading is used and the timing page shows each enrollment loaded in the `Index` action method:</span></span>

![명시적 로드(explicit loading)](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image8.png)

<span data-ttu-id="18763-150">다음 코드에서는 즉시를 지정 하 고 `Index` 뷰를 호출한 후 각 등록을 인출 합니다.</span><span class="sxs-lookup"><span data-stu-id="18763-150">In the following code, eager is specified, and each enrollment is fetched after the `Index` view is called:</span></span>

![즉시 지정](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image9.png)

<span data-ttu-id="18763-152">시간 세그먼트를 마우스로 가리키면 자세한 타이밍 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18763-152">You can hover over a time segment to get detailed timing information:</span></span>

![자세한 타이밍을 보려면 마우스로 가리킵니다.](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image10.png)

<a id="mb"></a>
## <a name="model-binding"></a><span data-ttu-id="18763-154">모델 바인딩</span><span class="sxs-lookup"><span data-stu-id="18763-154">Model Binding</span></span>

<span data-ttu-id="18763-155">[모델 바인딩 탭](http://getglimpse.com/Docs/Model-Binding-Tab) 은 폼 변수를 바인딩하는 방법과 일부의 바인딩이 필요한 이유를 이해 하는 데 도움이 되는 다양 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="18763-155">The [model binding tab](http://getglimpse.com/Docs/Model-Binding-Tab) provides a wealth of information to help you understand how your form variables are bound and why some are not bound as would expect.</span></span> <span data-ttu-id="18763-156">아래 이미지 **는를 보여** 줍니다.</span><span class="sxs-lookup"><span data-stu-id="18763-156">The image below shows the **?**</span></span> <span data-ttu-id="18763-157">아이콘을 클릭 하 여 해당 기능에 대 한 표시 도움말 페이지를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18763-157">icon, which you can click on to bring up the glimpse help page for that feature.</span></span>

![모델 바인딩 보기](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image11.png)

<a id="route"></a>
## <a name="routes"></a><span data-ttu-id="18763-159">경로</span><span class="sxs-lookup"><span data-stu-id="18763-159">Routes</span></span>

 <span data-ttu-id="18763-160">확인 경로 탭은 라우팅을 디버그 하 고 이해 하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18763-160">The Glimpse Routes tab will can help you debug and understand routing.</span></span> <span data-ttu-id="18763-161">아래 이미지에서 제품 경로를 선택 하 고 (녹색, 간략 한 설명 규칙으로 표시 됨)</span><span class="sxs-lookup"><span data-stu-id="18763-161">In the image below, the product route is selected (and it shows in green, a Glimpse convention).</span></span> <span data-ttu-id="18763-162">경로 제약 조건](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png) 선택한 제품 이름 ![영역 및 데이터 토큰만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18763-162">![product name selected](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png) Route constraints, Areas and data tokens are also displayed.</span></span> <span data-ttu-id="18763-163">자세한 내용은 [ASP.NET MVC 5에서](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx) 확인 [경로](http://getglimpse.com/Docs/Routes-Tab) 및 특성 라우팅을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="18763-163">See [Glimpse Routes](http://getglimpse.com/Docs/Routes-Tab) and [Attribute Routing in ASP.NET MVC 5](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx) for more information.</span></span> 

<a id="da"></a>
## <a name="using-glimpse-on-azure"></a><span data-ttu-id="18763-164">Azure에서의 사용</span><span class="sxs-lookup"><span data-stu-id="18763-164">Using Glimpse on Azure</span></span>

<span data-ttu-id="18763-165">기본 보안 정책에는 로컬 호스트 에서만 표시 되는 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18763-165">The Glimpse default security policy only allows Glimpse data to be displayed from local host.</span></span> <span data-ttu-id="18763-166">원격 서버 (예: Azure의 웹 앱)에서이 데이터를 볼 수 있도록이 보안 정책을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18763-166">You can change this security policy so you can view this data on a remote server (such as a web app on Azure).</span></span> <span data-ttu-id="18763-167">Azure에서 테스트 환경의 경우, *웹 .config* 파일의 아래쪽에 강조 표시 된 표시를 추가 하 여이를 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18763-167">For test environments on Azure, add the highlighted mark up to the bottom of the *web.config* file to enable Glimpse:</span></span>

[!code-xml[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample3.xml?highlight=2-6)]

<span data-ttu-id="18763-168">이 변경 만으로 모든 사용자가 원격 사이트에서 사용자의 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18763-168">With this change alone, any user can see your Glimpse data on a remote site.</span></span> <span data-ttu-id="18763-169">위의 태그를 게시 프로필에 추가 하는 것이 좋습니다. 게시 프로필을 사용 하는 경우에만 배포 됩니다 (예: Azure 테스트 프로필). 이 경우에는 `canViewGlimpseData` 역할을 추가 하 고이 역할의 사용자만이 데이터를 볼 수 있도록 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="18763-169">Consider adding the markup above to a publish profile so it's only deployed an applied when you use that publish profile (for example, your Azure test profile.) To restrict Glimpse data, we will add the `canViewGlimpseData` role and only allow users in this role to view Glimpse data.</span></span>

<span data-ttu-id="18763-170">*GlimpseSecurityPolicy.cs* 파일에서 주석을 제거 하 고 `Administrator`에서 `canViewGlimpseData` 역할로 [IsInRole](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx) 호출을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="18763-170">Remove the comments from the *GlimpseSecurityPolicy.cs* file and change the [IsInRole](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx) call from `Administrator` to the `canViewGlimpseData` role:</span></span>

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample4.cs?highlight=6)]

> [!WARNING]
> <span data-ttu-id="18763-171">보안-잠깐에서 제공 되는 다양 한 데이터는 앱의 보안을 노출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18763-171">Security - The rich data provided by Glimpse could expose the security of your app.</span></span> <span data-ttu-id="18763-172">Microsoft는 생성 앱에서 사용 하기 위해이에 대 한 보안 감사를 수행 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="18763-172">Microsoft has not performed a security audit of Glimpse for use on productions apps.</span></span>

<span data-ttu-id="18763-173">역할을 추가 하는 방법에 대 한 자세한 내용은 my [Deploy a Secure ASP.NET MVC 5 web apps With Membership, OAuth 및 SQL Database To Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/) tutorial를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="18763-173">For information on adding roles, see my [Deploy a Secure ASP.NET MVC 5 web app with Membership, OAuth, and SQL Database to Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/) tutorial.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="18763-174">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="18763-174">Additional Resources</span></span>

- [<span data-ttu-id="18763-175">멤버 자격, OAuth 및 SQL Database가 포함 된 보안 ASP.NET MVC 5 앱을 Azure에 배포</span><span class="sxs-lookup"><span data-stu-id="18763-175">Deploy a Secure ASP.NET MVC 5 app with Membership, OAuth, and SQL Database to Azure</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)
- <span data-ttu-id="18763-176">간략 한 [구성](http://getglimpse.com/Docs/Configuration) -탭 구성, 런타임 정책, 로깅 등의 문서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="18763-176">[Glimpse Configuration](http://getglimpse.com/Docs/Configuration) - Doc page on configuring tabs, runtime policy, logging and more.</span></span>
