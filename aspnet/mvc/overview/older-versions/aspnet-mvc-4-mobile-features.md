---
uid: mvc/overview/older-versions/aspnet-mvc-4-mobile-features
title: ASP.NET MVC 4 모바일 기능 | Microsoft Docs
author: Rick-Anderson
description: 이제 Azure 웹 사이트에 ASP.NET MVC 5 모바일 웹 응용 프로그램 배포의 코드 샘플과 함께이 자습서의 MVC 5 버전이 있습니다.
ms.author: riande
ms.date: 08/15/2012
ms.assetid: 27dc4fc8-1b51-43b0-933f-fc1b52476523
msc.legacyurl: /mvc/overview/older-versions/aspnet-mvc-4-mobile-features
msc.type: authoredcontent
ms.openlocfilehash: 907a16946c93761cd543135b0b226c8696b041f0
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74594640"
---
# <a name="aspnet-mvc-4-mobile-features"></a><span data-ttu-id="c7f75-103">ASP.NET MVC 4 모바일 기능</span><span class="sxs-lookup"><span data-stu-id="c7f75-103">ASP.NET MVC 4 Mobile Features</span></span>

<span data-ttu-id="c7f75-104">[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="c7f75-104">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

> <span data-ttu-id="c7f75-105">이제 [Azure 웹 사이트에 ASP.NET MVC 5 모바일 웹 응용 프로그램 배포](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/)의 코드 샘플과 함께이 자습서의 MVC 5 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-105">There is now an MVC 5 version of this tutorial with code samples at [Deploy an ASP.NET MVC 5 Mobile Web Application on Azure Web Sites](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/).</span></span>

<span data-ttu-id="c7f75-106">이 자습서에서는 ASP.NET MVC 4 웹 응용 프로그램에서 모바일 기능을 사용 하는 방법에 대 한 기본 사항을 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-106">This tutorial will teach you the basics of how to work with mobile features in an ASP.NET MVC 4 Web application.</span></span> <span data-ttu-id="c7f75-107">이 자습서에서는 [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) 또는 Visual web Developer 2010 Express 서비스 팩 1 (&quot;Visual web DEVELOPER 또는 VWD&quot;)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-107">For this tutorial, you can use [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) or Visual Web Developer 2010 Express Service Pack 1 (&quot;Visual Web Developer or VWD&quot;).</span></span> <span data-ttu-id="c7f75-108">이미 있는 경우 Visual Studio의 professional 버전을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-108">You can use the professional version of Visual Studio if you already have that.</span></span>

<span data-ttu-id="c7f75-109">시작 하기 전에 아래 나열 된 필수 구성 요소를 설치 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-109">Before you start, make sure you've installed the prerequisites listed below.</span></span>

- <span data-ttu-id="c7f75-110">[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) (권장) 또는 Visual Studio Web DEVELOPER Express SP1.</span><span class="sxs-lookup"><span data-stu-id="c7f75-110">[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) (recommended) or Visual Studio Web Developer Express SP1.</span></span> <span data-ttu-id="c7f75-111">Visual Studio 2012은 ASP.NET MVC 4를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-111">Visual Studio 2012 contains ASP.NET MVC 4.</span></span> <span data-ttu-id="c7f75-112">Visual Web Developer 2010를 사용 하는 경우 [ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392)를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-112">If you are using Visual Web Developer 2010, you must install [ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392).</span></span>

<span data-ttu-id="c7f75-113">모바일 브라우저 에뮬레이터도 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-113">You will also need a mobile browser emulator.</span></span> <span data-ttu-id="c7f75-114">다음 중 하나가 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-114">Any of the following will work:</span></span>

- <span data-ttu-id="c7f75-115">[Windows 7 Phone 에뮬레이터](https://msdn.microsoft.com/library/ff402563(VS.92).aspx).</span><span class="sxs-lookup"><span data-stu-id="c7f75-115">[Windows 7 Phone Emulator](https://msdn.microsoft.com/library/ff402563(VS.92).aspx).</span></span> <span data-ttu-id="c7f75-116">이 에뮬레이터는이 자습서의 스크린 샷 대부분에서 사용 되는 에뮬레이터입니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-116">(This is the emulator that's used in most of the screen shots in this tutorial.)</span></span>
- <span data-ttu-id="c7f75-117">IPhone을 에뮬레이트 하도록 사용자 에이전트 문자열을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-117">Change the user agent string to emulate an iPhone.</span></span> <span data-ttu-id="c7f75-118">[이](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) 블로그 항목을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="c7f75-118">See [this](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) blog entry.</span></span>
- [<span data-ttu-id="c7f75-119">Opera 모바일 에뮬레이터</span><span class="sxs-lookup"><span data-stu-id="c7f75-119">Opera Mobile Emulator</span></span>](http://www.opera.com/developer/tools/mobile/)
- <span data-ttu-id="c7f75-120">사용자 에이전트가 iPhone으로 설정 된 [Apple Safari](http://www.apple.com/safari/download/) .</span><span class="sxs-lookup"><span data-stu-id="c7f75-120">[Apple Safari](http://www.apple.com/safari/download/) with the user agent set to iPhone.</span></span> <span data-ttu-id="c7f75-121">Safari의 사용자 에이전트를 "iPhone"으로 설정 하는 방법에 대 한 지침은 Alison의 블로그에서 [safari가 IE](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) 를 가장 하는 방법을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="c7f75-121">For instructions on how to set the user agent in Safari to "iPhone", see [How to let Safari pretend it's IE](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) on David Alison's blog.</span></span>

<span data-ttu-id="c7f75-122">소스 코드를 포함 C# 하는 Visual Studio 프로젝트는 다음 항목에 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-122">Visual Studio projects with C# source code are available to accompany this topic:</span></span>

- [<span data-ttu-id="c7f75-123">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="c7f75-123">Starter project download</span></span>](https://go.microsoft.com/fwlink/?linkid=228307&amp;clcid=0x409)
- [<span data-ttu-id="c7f75-124">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="c7f75-124">Completed project download</span></span>](https://go.microsoft.com/fwlink/?linkid=228306&amp;clcid=0x409)

### <a name="what-youll-build"></a><span data-ttu-id="c7f75-125">빌드할 내용</span><span class="sxs-lookup"><span data-stu-id="c7f75-125">What You'll Build</span></span>

<span data-ttu-id="c7f75-126">이 자습서에서는 [시작 프로젝트](https://go.microsoft.com/fwlink/?LinkId=228307)에 제공 된 간단한 회의 목록 응용 프로그램에 모바일 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-126">For this tutorial, you'll add mobile features to the simple conference-listing application that's provided in the [starter project](https://go.microsoft.com/fwlink/?LinkId=228307).</span></span> <span data-ttu-id="c7f75-127">다음 스크린샷은 [Windows 7 Phone 에뮬레이터](https://msdn.microsoft.com/library/ff402563(VS.92).aspx)에 표시 된 대로 완료 된 응용 프로그램의 태그 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-127">The following screenshot shows the tags page of the completed application as seen in the [Windows 7 Phone Emulator](https://msdn.microsoft.com/library/ff402563(VS.92).aspx).</span></span> <span data-ttu-id="c7f75-128">키보드 입력을 단순화 하려면 [Windows Phone 에뮬레이터에 대 한 키보드 매핑](https://msdn.microsoft.com/library/ff754352(v=vs.92).aspx) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="c7f75-128">See [Keyboard Mapping for Windows Phone Emulator](https://msdn.microsoft.com/library/ff754352(v=vs.92).aspx) to simplify keyboard input.</span></span>

<span data-ttu-id="c7f75-129">[![p1_Tags_CompletedProj](aspnet-mvc-4-mobile-features/_static/image2.png)](aspnet-mvc-4-mobile-features/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c7f75-129">[![p1_Tags_CompletedProj](aspnet-mvc-4-mobile-features/_static/image2.png)](aspnet-mvc-4-mobile-features/_static/image1.png)</span></span>

<span data-ttu-id="c7f75-130">Internet Explorer 버전 9 또는 10, FireFox 또는 Chrome을 사용 하 여 [사용자 에이전트 문자열](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)을 설정 하 여 모바일 응용 프로그램을 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-130">You can use Internet Explorer version 9 or 10, FireFox or Chrome to develop your mobile application by setting the [user agent string](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/).</span></span> <span data-ttu-id="c7f75-131">다음 그림은 iPhone을 에뮬레이션 하는 Internet Explorer를 사용 하는 완료 된 자습서를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-131">The following image shows the completed tutorial using Internet Explorer emulating an iPhone.</span></span> <span data-ttu-id="c7f75-132">Internet Explorer F-12 개발자 도구 및 [Fiddler 도구](http://www.fiddler2.com/fiddler2/) 를 사용 하 여 응용 프로그램을 디버그할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-132">You can use the Internet Explorer F-12 developer tools and the [Fiddler tool](http://www.fiddler2.com/fiddler2/) to help debug your application.</span></span>

![](aspnet-mvc-4-mobile-features/_static/image3.png)

### <a name="skills-youll-learn"></a><span data-ttu-id="c7f75-133">배울 기술</span><span class="sxs-lookup"><span data-stu-id="c7f75-133">Skills You'll Learn</span></span>

<span data-ttu-id="c7f75-134">학습할 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-134">Here's what you'll learn:</span></span>

- <span data-ttu-id="c7f75-135">ASP.NET MVC 4 템플릿에서 HTML5 `viewport` 특성 및 적응형 렌더링을 사용 하 여 모바일 장치에서 디스플레이를 개선 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-135">How the ASP.NET MVC 4 templates use the HTML5 `viewport` attribute and adaptive rendering to improve display on mobile devices.</span></span>
- <span data-ttu-id="c7f75-136">모바일 관련 보기를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="c7f75-136">How to create mobile-specific views.</span></span>
- <span data-ttu-id="c7f75-137">사용자가 모바일 뷰와 응용 프로그램의 데스크톱 보기 간을 전환할 수 있도록 하는 보기 전환기를 만드는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-137">How to create a view switcher that lets users toggle between a mobile view and a desktop view of the application.</span></span>

### <a name="getting-started"></a><span data-ttu-id="c7f75-138">시작</span><span class="sxs-lookup"><span data-stu-id="c7f75-138">Getting Started</span></span>

<span data-ttu-id="c7f75-139">다음 링크를 사용 하 여 시작 프로젝트용 회의 목록 응용 프로그램을 다운로드 합니다. [다운로드](https://go.microsoft.com/fwlink/?LinkId=228307).</span><span class="sxs-lookup"><span data-stu-id="c7f75-139">Download the conference-listing application for the starter project using the following link: [Download](https://go.microsoft.com/fwlink/?LinkId=228307).</span></span> <span data-ttu-id="c7f75-140">그런 다음 Windows 탐색기에서 *Mvcmobile .zip* 파일을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-140">Then in Windows Explorer, right-click the *MvcMobile.zip* file and choose **Properties**.</span></span> <span data-ttu-id="c7f75-141">**Mvcmobile .Zip 속성** 대화 상자에서 **차단 해제** 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-141">In the **MvcMobile.zip Properties** dialog box, choose the **Unblock** button.</span></span> <span data-ttu-id="c7f75-142">차단 해제는 웹에서 다운로드 한 *.zip* 파일을 사용 하려고 할 때 발생 하는 보안 경고를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-142">(Unblocking prevents a security warning that occurs when you try to use a *.zip* file that you've downloaded from the web.)</span></span>

![p1_unBlock](aspnet-mvc-4-mobile-features/_static/image4.png)

<span data-ttu-id="c7f75-144">*Mvcmobile .zip* 파일을 마우스 오른쪽 단추로 클릭 하 고 **압축 풀기** 를 선택 하 여 파일의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-144">Right-click the *MvcMobile.zip* file and select **Extract All** to unzip the file.</span></span> <span data-ttu-id="c7f75-145">Visual Studio에서 *Mvcmobile .sln* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-145">In Visual Studio, open the *MvcMobile.sln* file.</span></span>

<span data-ttu-id="c7f75-146">CTRL + f 5를 눌러 응용 프로그램을 실행 하면 데스크톱 브라우저에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-146">Press CTRL+F5 to run the application, which will display it in your desktop browser.</span></span> <span data-ttu-id="c7f75-147">모바일 브라우저 에뮬레이터를 시작 하 고, 회의 응용 프로그램의 URL을 에뮬레이터에 복사한 다음, **태그별로 찾아보기** 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-147">Start your mobile browser emulator, copy the URL for the conference application into the emulator, and then click the **Browse by tag** link.</span></span> <span data-ttu-id="c7f75-148">Windows Phone 에뮬레이터를 사용 하는 경우 URL 표시줄을 클릭 하 고 일시 중지 키를 눌러 키보드 액세스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-148">If you are using the Windows Phone Emulator, click in the URL bar and press the Pause key to get keyboard access.</span></span> <span data-ttu-id="c7f75-149">아래 이미지는 *Alltags* 뷰 ( **태그로 찾아보기**선택)를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-149">The image below shows the *AllTags* view (from choosing **Browse by tag**).</span></span>

<span data-ttu-id="c7f75-150">[![p1_browseTag](aspnet-mvc-4-mobile-features/_static/image6.png)](aspnet-mvc-4-mobile-features/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="c7f75-150">[![p1_browseTag](aspnet-mvc-4-mobile-features/_static/image6.png)](aspnet-mvc-4-mobile-features/_static/image5.png)</span></span>

<span data-ttu-id="c7f75-151">모바일 장치에서 디스플레이를 매우 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-151">The display is very readable on a mobile device.</span></span> <span data-ttu-id="c7f75-152">ASP.NET 링크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-152">Choose the ASP.NET link.</span></span>

<span data-ttu-id="c7f75-153">[![p1_tagged_ASPNET](aspnet-mvc-4-mobile-features/_static/image8.png)](aspnet-mvc-4-mobile-features/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="c7f75-153">[![p1_tagged_ASPNET](aspnet-mvc-4-mobile-features/_static/image8.png)](aspnet-mvc-4-mobile-features/_static/image7.png)</span></span>

<span data-ttu-id="c7f75-154">ASP.NET 태그 보기는 매우 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-154">The ASP.NET tag view is very cluttered.</span></span> <span data-ttu-id="c7f75-155">예를 들어 **날짜** 열은 읽기가 매우 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-155">For example, the **Date** column is very difficult to read.</span></span> <span data-ttu-id="c7f75-156">이 자습서의 뒷부분에서는 모바일 브라우저용으로 특별히 표시 되 고 표시를 읽을 수 있도록 하는 *Alltags* 보기의 버전을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-156">Later in the tutorial you'll create a version of the *AllTags* view that's specifically for mobile browsers and that will make the display readable.</span></span>

<span data-ttu-id="c7f75-157">참고: 현재 버그가 모바일 캐싱 엔진에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-157">Note: Currently a bug exists in the mobile caching engine.</span></span> <span data-ttu-id="c7f75-158">프로덕션 응용 프로그램의 경우 [고정 displaymodes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) nugget 패키지를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-158">For production applications, you must install the [Fixed DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) nugget package.</span></span> <span data-ttu-id="c7f75-159">해결 방법에 대 한 자세한 내용은 [ASP.NET MVC 4 Mobile 캐싱 버그 수정](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="c7f75-159">See [ASP.NET MVC 4 Mobile Caching Bug Fixed](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) for details on the fix.</span></span>

## <a name="css-media-queries"></a><span data-ttu-id="c7f75-160">CSS 미디어 쿼리</span><span class="sxs-lookup"><span data-stu-id="c7f75-160">CSS Media Queries</span></span>

<span data-ttu-id="c7f75-161">[Css 미디어 쿼리](http://www.w3.org/TR/css3-mediaqueries/) 는 미디어 유형의 css에 대 한 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-161">[CSS media queries](http://www.w3.org/TR/css3-mediaqueries/) are an extension to CSS for media types.</span></span> <span data-ttu-id="c7f75-162">이를 통해 특정 브라우저 (사용자 에이전트)에 대 한 기본 CSS 규칙을 재정의 하는 규칙을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-162">They allow you to create rules that override the default CSS rules for specific browsers (user agents).</span></span> <span data-ttu-id="c7f75-163">모바일 브라우저를 대상으로 하는 CSS에 대 한 일반적인 규칙은 최대 화면 크기를 정의 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-163">A common rule for CSS that targets mobile browsers is defining the maximum screen size.</span></span> <span data-ttu-id="c7f75-164">새 ASP.NET MVC 4 인터넷 프로젝트를 만들 때 생성 된 *Content\site.xml* 파일에는 다음 미디어 쿼리가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-164">The *Content\Site.css* file that's created when you create a new ASP.NET MVC 4 Internet project contains the following media query:</span></span>

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample1.css)]

<span data-ttu-id="c7f75-165">브라우저 창의 너비가 850 픽셀이 면이 미디어 블록 내에서 CSS 규칙을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-165">If the browser window is 850 pixels wide or less, it will use the CSS rules inside this media block.</span></span> <span data-ttu-id="c7f75-166">이와 같은 CSS 미디어 쿼리를 사용 하 여 데스크톱 브라우저의 광범위 한 표시를 위해 디자인 된 기본 CSS 규칙 보다 작은 브라우저 (예: 모바일 브라우저)에서 HTML 콘텐츠를 더 잘 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-166">You can use CSS media queries like this to provide a better display of HTML content on small browsers (like mobile browsers) than the default CSS rules that are designed for the wider displays of desktop browsers.</span></span>

## <a name="the-viewport-meta-tag"></a><span data-ttu-id="c7f75-167">뷰포트 메타 태그</span><span class="sxs-lookup"><span data-stu-id="c7f75-167">The Viewport Meta Tag</span></span>

<span data-ttu-id="c7f75-168">대부분의 모바일 브라우저는 모바일 장치의 실제 너비 보다 훨씬 큰 가상 브라우저 창 너비 ( *뷰포트*)를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-168">Most mobile browsers define a virtual browser window width (the *viewport*) that's much larger than the actual width of the mobile device.</span></span> <span data-ttu-id="c7f75-169">이를 통해 모바일 브라우저는 전체 웹 페이지를 가상 디스플레이 안에 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-169">This allows mobile browsers to fit the entire web page inside the virtual display.</span></span> <span data-ttu-id="c7f75-170">그러면 사용자가 관심 있는 콘텐츠를 확대할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-170">Users can then zoom in on interesting content.</span></span> <span data-ttu-id="c7f75-171">그러나 뷰포트 너비를 실제 장치 너비로 설정 하면 콘텐츠가 모바일 브라우저에 맞게 조정 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-171">However, if you set the viewport width to the actual device width, no zooming is required, because the content fits in the mobile browser.</span></span>

<span data-ttu-id="c7f75-172">ASP.NET MVC 4 레이아웃 파일의 뷰포트 `<meta>` 태그는 뷰포트를 장치 너비로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-172">The viewport `<meta>` tag in the ASP.NET MVC 4 layout file sets the viewport to the device width.</span></span> <span data-ttu-id="c7f75-173">다음 줄에서는 ASP.NET MVC 4 레이아웃 파일의 뷰포트 `<meta>` 태그를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-173">The following line shows the viewport `<meta>` tag in the ASP.NET MVC 4 layout file.</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample2.html)]

## <a name="examining-the-effect-of-css-media-queries-and-the-viewport-meta-tag"></a><span data-ttu-id="c7f75-174">CSS 미디어 쿼리 및 뷰포트 메타 태그의 영향 검사</span><span class="sxs-lookup"><span data-stu-id="c7f75-174">Examining the Effect of CSS Media Queries and the Viewport Meta Tag</span></span>

<span data-ttu-id="c7f75-175">편집기에서 *Views\Shared\\_Layout* 파일을 열고 뷰포트 `<meta>` 태그를 주석으로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-175">Open the *Views\Shared\\_Layout.cshtml* file in the editor and comment out the viewport `<meta>` tag.</span></span> <span data-ttu-id="c7f75-176">다음 태그는 주석 처리 된 줄을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-176">The following markup shows the commented-out line.</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample3.cshtml)]

<span data-ttu-id="c7f75-177">편집기에서 *MvcMobile\Content\Site.css* 파일을 열고 미디어 쿼리의 최대 너비를 0 픽셀로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-177">Open the *MvcMobile\Content\Site.css* file in the editor and change the maximum width in the media query to zero pixels.</span></span> <span data-ttu-id="c7f75-178">이렇게 하면 CSS 규칙이 모바일 브라우저에서 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-178">This will prevent the CSS rules from being used in mobile browsers.</span></span> <span data-ttu-id="c7f75-179">다음 줄은 수정 된 미디어 쿼리를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-179">The following line shows the modified media query:</span></span>

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample4.css)]

<span data-ttu-id="c7f75-180">변경 내용을 저장 하 고 모바일 브라우저 에뮬레이터에서 회의 응용 프로그램으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-180">Save your changes and browse to the Conference application in a mobile browser emulator.</span></span> <span data-ttu-id="c7f75-181">다음 이미지에서 가장 작은 텍스트는 뷰포트 `<meta>` 태그를 제거 하는 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-181">The tiny text in the following image is the result of removing the viewport `<meta>` tag.</span></span> <span data-ttu-id="c7f75-182">Viewport `<meta>` 태그를 사용 하지 않으면 브라우저가 대부분의 모바일 브라우저에서 기본 뷰포트 너비 (850 픽셀 이상)로 확대 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-182">With no viewport `<meta>` tag, the browser is zooming out to the default viewport width (850 pixels or wider for most mobile browsers.)</span></span>

<span data-ttu-id="c7f75-183">[![p1_noViewPort](aspnet-mvc-4-mobile-features/_static/image10.png)](aspnet-mvc-4-mobile-features/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="c7f75-183">[![p1_noViewPort](aspnet-mvc-4-mobile-features/_static/image10.png)](aspnet-mvc-4-mobile-features/_static/image9.png)</span></span>

<span data-ttu-id="c7f75-184">변경 내용 실행 취소-레이아웃 파일에서 뷰포트 `<meta>` 태그의 주석 처리를 제거 하 고 *사이트 .css* 파일에서 미디어 쿼리를 850 픽셀로 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-184">Undo your changes — uncomment the viewport `<meta>` tag in the layout file and restore the media query to 850 pixels in the *Site.css* file.</span></span> <span data-ttu-id="c7f75-185">변경 내용을 저장 하 고 모바일 브라우저를 새로 고쳐 모바일 친화적인 디스플레이가 복원 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-185">Save your changes and refresh the mobile browser to verify that the mobile-friendly display has been restored.</span></span>

<span data-ttu-id="c7f75-186">Viewport `<meta>` 태그와 CSS 미디어 쿼리는 ASP.NET MVC 4와 관련이 없으며 모든 웹 응용 프로그램에서 이러한 기능을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-186">The viewport `<meta>` tag and the CSS media query are not specific to ASP.NET MVC 4, and you can take advantage of these features in any web application.</span></span> <span data-ttu-id="c7f75-187">그러나 이제 새 ASP.NET MVC 4 프로젝트를 만들 때 생성 되는 파일에 기본 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-187">But they are now built into the files that are generated when you create a new ASP.NET MVC 4 project.</span></span>

<span data-ttu-id="c7f75-188">Viewport `<meta>` 태그에 대 한 자세한 내용은 두 개의 [뷰포트 (2 부) tale of two](http://www.quirksmode.org/mobile/viewports2.html)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="c7f75-188">For more information about the viewport `<meta>` tag, see [A tale of two viewports — part two](http://www.quirksmode.org/mobile/viewports2.html).</span></span>

<span data-ttu-id="c7f75-189">다음 섹션에서는 모바일 브라우저의 특정 뷰를 제공 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-189">In the next section you'll see how to provide mobile-browser specific views.</span></span>

## <a name="overriding-views-layouts-and-partial-views"></a><span data-ttu-id="c7f75-190">뷰, 레이아웃 및 부분 뷰 재정의</span><span class="sxs-lookup"><span data-stu-id="c7f75-190">Overriding Views, Layouts, and Partial Views</span></span>

<span data-ttu-id="c7f75-191">ASP.NET MVC 4의 중요 한 새로운 기능은 일반적으로, 개별 모바일 브라우저나 특정 브라우저에 대해 모바일 브라우저의 모든 보기 (레이아웃 및 부분 보기 포함)를 재정의할 수 있는 간단한 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-191">A significant new feature in ASP.NET MVC 4 is a simple mechanism that lets you override any view (including layouts and partial views) for mobile browsers in general, for an individual mobile browser, or for any specific browser.</span></span> <span data-ttu-id="c7f75-192">모바일 관련 보기를 제공 하기 위해 보기 파일을 복사 하 고를 추가할 수 있습니다 *.* 파일 이름으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-192">To provide a mobile-specific view, you can copy a view file and add *.Mobile* to the file name.</span></span> <span data-ttu-id="c7f75-193">예를 들어, 모바일 *인덱스* 보기를 만들려면 *Views\Home\Index.cshtml* 을 *Views\Home\Index.Mobile.cshtml*에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-193">For example, to create a mobile *Index* view, copy *Views\Home\Index.cshtml* to *Views\Home\Index.Mobile.cshtml*.</span></span>

<span data-ttu-id="c7f75-194">이 섹션에서는 모바일 전용 레이아웃 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-194">In this section, you'll create a mobile-specific layout file.</span></span>

<span data-ttu-id="c7f75-195">시작 하려면 *Views\Shared\\_Layout* 를 *Views\Shared\\_Layout*로 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-195">To start, copy *Views\Shared\\_Layout.cshtml* to *Views\Shared\\_Layout.Mobile.cshtml*.</span></span> <span data-ttu-id="c7f75-196">*\_Layout* 을 열고 제목을 **MVC4 회의** 에서 **회의 (모바일)** 로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-196">Open *\_Layout.Mobile.cshtml* and change the title from **MVC4 Conference** to **Conference (Mobile)**.</span></span>

<span data-ttu-id="c7f75-197">각 `Html.ActionLink` 호출에서 *각 링크의*"Browse by"를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-197">In each `Html.ActionLink` call, remove "Browse by" in each link *ActionLink*.</span></span> <span data-ttu-id="c7f75-198">다음 코드는 모바일 레이아웃 파일의 완료 된 본문 섹션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-198">The following code shows the completed body section of the mobile layout file.</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample5.cshtml)]

<span data-ttu-id="c7f75-199">*Views\Home\AllTags.cshtml* 파일을 *Views\Home\AllTags.Mobile.cshtml*에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-199">Copy the *Views\Home\AllTags.cshtml* file to *Views\Home\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="c7f75-200">새 파일을 열고 `<h2>` 요소를 "Tags"에서 "Tags (M)"로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-200">Open the new file and change the `<h2>` element from "Tags" to "Tags (M)":</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample6.html)]

<span data-ttu-id="c7f75-201">바탕 화면 브라우저를 사용 하 고 모바일 브라우저 에뮬레이터를 사용 하 여 태그 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-201">Browse to the tags page using a desktop browser and using mobile browser emulator.</span></span> <span data-ttu-id="c7f75-202">모바일 브라우저 에뮬레이터에는 두 가지 변경 내용이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-202">The mobile browser emulator shows the two changes you made.</span></span>

<span data-ttu-id="c7f75-203">[p2m_layoutTags ![](aspnet-mvc-4-mobile-features/_static/image12.png)](aspnet-mvc-4-mobile-features/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="c7f75-203">[![p2m_layoutTags.mobile](aspnet-mvc-4-mobile-features/_static/image12.png)](aspnet-mvc-4-mobile-features/_static/image11.png)</span></span>

<span data-ttu-id="c7f75-204">이와 달리 바탕 화면 표시는 변경 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-204">In contrast, the desktop display has not changed.</span></span>

<span data-ttu-id="c7f75-205">[![p2_layoutTagsDesktop](aspnet-mvc-4-mobile-features/_static/image14.png)](aspnet-mvc-4-mobile-features/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="c7f75-205">[![p2_layoutTagsDesktop](aspnet-mvc-4-mobile-features/_static/image14.png)](aspnet-mvc-4-mobile-features/_static/image13.png)</span></span>

## <a name="browser-specific-views"></a><span data-ttu-id="c7f75-206">브라우저 관련 뷰</span><span class="sxs-lookup"><span data-stu-id="c7f75-206">Browser-Specific Views</span></span>

<span data-ttu-id="c7f75-207">모바일 특정 및 데스크톱 특정 보기 외에 개별 브라우저에 대 한 보기를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-207">In addition to mobile-specific and desktop-specific views, you can create views for an individual browser.</span></span> <span data-ttu-id="c7f75-208">예를 들어 iPhone 브라우저 전용 보기를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-208">For example, you can create views that are specifically for the iPhone browser.</span></span> <span data-ttu-id="c7f75-209">이 섹션에서는 iPhone 브라우저 및 iPhone 버전의 *Alltags* 보기에 대 한 레이아웃을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-209">In this section, you'll create a layout for the iPhone browser and an iPhone version of the *AllTags* view.</span></span>

<span data-ttu-id="c7f75-210">*Global.asax* 파일을 열고 다음 코드를 `Application_Start` 메서드에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-210">Open the *Global.asax* file and add the following code to the `Application_Start` method.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample7.cs)]

<span data-ttu-id="c7f75-211">이 코드는 들어오는 각 요청에 대해 일치 하는 "iPhone" 이라는 새 표시 모드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-211">This code defines a new display mode named "iPhone" that will be matched against each incoming request.</span></span> <span data-ttu-id="c7f75-212">들어오는 요청이 사용자가 정의한 조건과 일치 하는 경우 (즉, 사용자 에이전트가 "iPhone" 문자열을 포함 하는 경우) ASP.NET MVC는 이름에 "iPhone" 접미사가 포함 된 뷰를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-212">If the incoming request matches the condition you defined (that is, if the user agent contains the string "iPhone"), ASP.NET MVC will look for views whose name contains the "iPhone" suffix.</span></span>

<span data-ttu-id="c7f75-213">코드에서 `DefaultDisplayMode`를 마우스 오른쪽 단추로 클릭 하 고 **해결**을 선택한 다음 `using System.Web.WebPages;`을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-213">In the code, right-click `DefaultDisplayMode`, choose **Resolve**, and then choose `using System.Web.WebPages;`.</span></span> <span data-ttu-id="c7f75-214">이렇게 하면 `DisplayModes` 및 `DefaultDisplayMode` 형식이 정의 된 `System.Web.WebPages` 네임 스페이스에 대 한 참조가 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-214">This adds a reference to the `System.Web.WebPages` namespace, which is where the `DisplayModes` and `DefaultDisplayMode` types are defined.</span></span>

<span data-ttu-id="c7f75-215">[![p2_resolve](aspnet-mvc-4-mobile-features/_static/image16.png)](aspnet-mvc-4-mobile-features/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="c7f75-215">[![p2_resolve](aspnet-mvc-4-mobile-features/_static/image16.png)](aspnet-mvc-4-mobile-features/_static/image15.png)</span></span>

<span data-ttu-id="c7f75-216">또는 파일의 `using` 섹션에 다음 줄을 수동으로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-216">Alternatively, you can just manually add the following line to the `using` section of the file.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample8.cs)]

<span data-ttu-id="c7f75-217">*Global.asax* 파일의 전체 내용이 아래에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-217">The complete contents of the *Global.asax* file is shown below.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample9.cs)]

<span data-ttu-id="c7f75-218">변경 사항을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-218">Save the changes.</span></span> <span data-ttu-id="c7f75-219">*MvcMobile\Views\Shared\\_Layout* 파일을 *MvcMobile\Views\Shared\\_Layout*에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-219">Copy the *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* file to *MvcMobile\Views\Shared\\_Layout.iPhone.cshtml*.</span></span> <span data-ttu-id="c7f75-220">새 파일을 열고 `h1` 제목을 `Conference (Mobile)`에서 `Conference (iPhone)`으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-220">Open the new file and then change the `h1` heading from `Conference (Mobile)` to `Conference (iPhone)`.</span></span>

<span data-ttu-id="c7f75-221">*MvcMobile\Views\Home\AllTags.Mobile.cshtml* 파일을 *MvcMobile\Views\Home\AllTags.iPhone.cshtml*에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-221">Copy the *MvcMobile\Views\Home\AllTags.Mobile.cshtml* file to *MvcMobile\Views\Home\AllTags.iPhone.cshtml*.</span></span> <span data-ttu-id="c7f75-222">새 파일에서 `<h2>` 요소를 "Tags (M)"에서 "Tags (iPhone)"로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-222">In the new file, change the `<h2>` element from "Tags (M)" to "Tags (iPhone)".</span></span>

<span data-ttu-id="c7f75-223">응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-223">Run the application.</span></span> <span data-ttu-id="c7f75-224">모바일 브라우저 에뮬레이터를 실행 하 고 해당 사용자 에이전트가 "iPhone"으로 설정 되었는지 확인 한 다음 *Alltags* 보기로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-224">Run a mobile browser emulator, make sure its user agent is set to "iPhone", and browse to the *AllTags* view.</span></span> <span data-ttu-id="c7f75-225">다음 스크린샷은 [Safari](http://www.apple.com/safari/download/) 브라우저에 렌더링 된 *alltags* 뷰를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-225">The following screenshot shows the *AllTags* view rendered in the [Safari](http://www.apple.com/safari/download/) browser.</span></span> <span data-ttu-id="c7f75-226">[여기](https://support.apple.com/kb/DL1531)에서 Windows 용 Safari를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-226">You can download Safari for Windows [here](https://support.apple.com/kb/DL1531).</span></span>

<span data-ttu-id="c7f75-227">[![p2_iphoneView](aspnet-mvc-4-mobile-features/_static/image18.png)](aspnet-mvc-4-mobile-features/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="c7f75-227">[![p2_iphoneView](aspnet-mvc-4-mobile-features/_static/image18.png)](aspnet-mvc-4-mobile-features/_static/image17.png)</span></span>

<span data-ttu-id="c7f75-228">이 섹션에서는 모바일 레이아웃 및 보기를 만드는 방법과 iPhone 등의 특정 장치에 대 한 레이아웃 및 보기를 만드는 방법에 대해 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-228">In this section we've seen how to create mobile layouts and views and how to create layouts and views for specific devices such as the iPhone.</span></span> <span data-ttu-id="c7f75-229">다음 섹션에서는 더 강력한 모바일 보기를 위해 jQuery Mobile을 활용 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-229">In the next section you'll see how to leverage jQuery Mobile for more compelling mobile views.</span></span>

## <a name="using-jquery-mobile"></a><span data-ttu-id="c7f75-230">JQuery Mobile 사용</span><span class="sxs-lookup"><span data-stu-id="c7f75-230">Using jQuery Mobile</span></span>

<span data-ttu-id="c7f75-231">[JQuery mobile](http://jquerymobile.com/demos/1.0b3/#/demos/1.0b3/docs/about/intro.html) library는 모든 주요 모바일 브라우저에서 작동 하는 사용자 인터페이스 프레임 워크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-231">The [jQuery Mobile](http://jquerymobile.com/demos/1.0b3/#/demos/1.0b3/docs/about/intro.html) library provides a user interface framework that works on all the major mobile browsers.</span></span> <span data-ttu-id="c7f75-232">jQuery Mobile은 CSS 및 JavaScript를 지 원하는 모바일 브라우저에 *점진적 향상 기능* 을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-232">jQuery Mobile applies *progressive enhancement* to mobile browsers that support CSS and JavaScript.</span></span> <span data-ttu-id="c7f75-233">점진적 향상 기능을 사용 하면 모든 브라우저에서 웹 페이지의 기본 콘텐츠를 표시할 수 있을 뿐 아니라 더욱 강력한 브라우저와 장치에서 더 다양 한 디스플레이를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-233">Progressive enhancement allows all browsers to display the basic content of a web page, while allowing more powerful browsers and devices to have a richer display.</span></span> <span data-ttu-id="c7f75-234">JQuery Mobile 스타일에 포함 된 JavaScript 및 CSS 파일은 태그를 변경 하지 않고 모바일 브라우저에 맞는 많은 요소를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-234">The JavaScript and CSS files that are included with jQuery Mobile style many elements to fit mobile browsers without making any markup changes.</span></span>

<span data-ttu-id="c7f75-235">이 섹션에서는 jquery Mobile 및 뷰 전환기 위젯을 설치 하는 *jquery. mobile.* i n a. n a n 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-235">In this section you'll install the *jQuery.Mobile.MVC* NuGet package, which installs jQuery Mobile and a view-switcher widget.</span></span>

<span data-ttu-id="c7f75-236">시작 하려면 이전에 만든 *\\_Layout 공유* 된 *\\_Layout* 파일을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-236">To start, delete the *Shared\\_Layout.Mobile.cshtml* and *Shared\\_Layout.iPhone.cshtml* files that you created earlier.</span></span>

<span data-ttu-id="c7f75-237">*Views\Home\AllTags.Mobile.cshtml* 및 *Views\Home\AllTags.iPhone.cshtml* 파일의 이름을 *Views\Home\AllTags.iPhone.cshtml.hide* 및 *Views\Home\AllTags.Mobile.cshtml.hide*로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-237">Rename *Views\Home\AllTags.Mobile.cshtml* and *Views\Home\AllTags.iPhone.cshtml* files to *Views\Home\AllTags.iPhone.cshtml.hide* and *Views\Home\AllTags.Mobile.cshtml.hide*.</span></span> <span data-ttu-id="c7f75-238">파일은 더 이상 확장명이 없습니다 *.* ASP.NET MVC 런타임에서 *alltags* 뷰를 렌더링 하는 데 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-238">Because the files no longer have a *.cshtml* extension, they won't be used by the ASP.NET MVC runtime to render the *AllTags* view.</span></span>

<span data-ttu-id="c7f75-239">다음을 수행 하 여 *jQuery. Mobile.* x NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-239">Install the *jQuery.Mobile.MVC* NuGet package by doing this:</span></span>

1. <span data-ttu-id="c7f75-240">**도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-240">From the **Tools** menu, select **NuGet Package Manager**, and then select **Package Manager Console**.</span></span>

    <span data-ttu-id="c7f75-241">[![p3_packageMgr](aspnet-mvc-4-mobile-features/_static/image20.png)](aspnet-mvc-4-mobile-features/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="c7f75-241">[![p3_packageMgr](aspnet-mvc-4-mobile-features/_static/image20.png)](aspnet-mvc-4-mobile-features/_static/image19.png)</span></span>
2. <span data-ttu-id="c7f75-242">**패키지 관리자 콘솔**에서 `Install-Package jQuery.Mobile.MVC -version 1.0.0`를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-242">In the **Package Manager Console**, enter `Install-Package jQuery.Mobile.MVC -version 1.0.0`</span></span>

<span data-ttu-id="c7f75-243">다음 이미지는 NuGet jQuery. Mobile. x 패키지를 통해 MvcMobile 프로젝트에 추가 되 고 변경 된 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-243">The following image shows the files added and changed to the MvcMobile project by the NuGet jQuery.Mobile.MVC package.</span></span> <span data-ttu-id="c7f75-244">추가 된 파일에는 파일 이름 뒤에 [추가]가 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-244">Files which are added have [add] appended after the file name.</span></span> <span data-ttu-id="c7f75-245">이미지에는 *Content\images* 폴더에 추가 된 GIF 및 PNG 파일이 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-245">The image does not show the GIF and PNG files added to the *Content\images* folder.</span></span>

![](aspnet-mvc-4-mobile-features/_static/image21.png)

<span data-ttu-id="c7f75-246">JQuery. Mobile. n a n.</span><span class="sxs-lookup"><span data-stu-id="c7f75-246">The jQuery.Mobile.MVC NuGet package installs the following:</span></span>

- <span data-ttu-id="c7f75-247">*응용 프로그램\_Start\BundleMobileConfig.cs* 파일은 jQuery JavaScript 및 추가 된 CSS 파일을 참조 하는 데 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-247">The *App\_Start\BundleMobileConfig.cs* file, which is needed to reference the jQuery JavaScript and CSS files added.</span></span> <span data-ttu-id="c7f75-248">아래 지침을 따르고이 파일에 정의 된 모바일 번들을 참조 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-248">You must follow the instructions below and reference the mobile bundle defined in this file.</span></span>
- <span data-ttu-id="c7f75-249">jQuery 모바일 CSS 파일.</span><span class="sxs-lookup"><span data-stu-id="c7f75-249">jQuery Mobile CSS files.</span></span>
- <span data-ttu-id="c7f75-250">`ViewSwitcher` 컨트롤러 위젯 (*Controllers\viewswitchercontroller.cs*).</span><span class="sxs-lookup"><span data-stu-id="c7f75-250">A `ViewSwitcher` controller widget (*Controllers\ViewSwitcherController.cs*).</span></span>
- <span data-ttu-id="c7f75-251">jQuery Mobile JavaScript 파일.</span><span class="sxs-lookup"><span data-stu-id="c7f75-251">jQuery Mobile JavaScript files.</span></span>
- <span data-ttu-id="c7f75-252">JQuery 모바일 스타일의 레이아웃 파일 (*Views\Shared\\_Layout*).</span><span class="sxs-lookup"><span data-stu-id="c7f75-252">A jQuery Mobile-styled layout file (*Views\Shared\\_Layout.Mobile.cshtml*).</span></span>
- <span data-ttu-id="c7f75-253">각 페이지 맨 위에 있는 링크를 제공 하 여 데스크톱 보기에서 모바일 보기로 전환 하거나 그 반대로 전환 하는 MvcMobile\Views\Shared () 뷰-전환기 부분 보기 *(\\_ViewSwitcher*)입니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-253">A view-switcher partial view *(MvcMobile\Views\Shared\\_ViewSwitcher.cshtml*) that provides a link at the top of each page to switch from desktop view to mobile view and vice versa.</span></span>
- <span data-ttu-id="c7f75-254"><em>Content\images</em> 폴더의 여러<em>.png</em> 및 <em>.gif</em> 이미지 파일</span><span class="sxs-lookup"><span data-stu-id="c7f75-254">Several<em>.png</em> and <em>.gif</em> image files in the <em>Content\images</em> folder.</span></span>

<span data-ttu-id="c7f75-255">*Global.asax* 파일을 열고 다음 코드를 `Application_Start` 메서드의 마지막 줄로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-255">Open the *Global.asax* file and add the following code as the last line of the `Application_Start` method.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample10.cs)]

<span data-ttu-id="c7f75-256">다음 코드 *에서는 전체 global.asax 파일을* 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-256">The following code shows the complete *Global.asax* file.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample11.cs?highlight=26)]

> [!NOTE]
> <span data-ttu-id="c7f75-257">Internet Explorer 9를 사용 하는 경우 위의 `BundleMobileConfig` 줄이 노란색 강조 표시 되지 않으면 IE의 호환성 보기 단추![(꺼짐)](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "호환성 보기 단추 (꺼짐)의 그림") 에 [있는 호환성 보기](https://windows.microsoft.com/windows7/How-to-use-Compatibility-View-in-Internet-Explorer-9)단추 그림을 클릭 하 여 호환성 보기 ![단추 (꺼짐)의 개요 그림](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "호환성 보기 단추 (꺼짐)의 그림") 에서 ![호환성 보기 단추 (설정)의 단색 그림](https://res1.windows.microsoft.com/resbox/en/Windows 7/main/156805ff-3130-481b-a12d-4d3a96470f36_14.jpg "호환성 보기 단추 (설정)의 그림")으로 아이콘을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-257">If you are using Internet Explorer 9 and you don't see the `BundleMobileConfig` line above in yellow highlight, click the [Compatibility View button](https://windows.microsoft.com/windows7/How-to-use-Compatibility-View-in-Internet-Explorer-9)![Picture of the Compatibility View button (off)](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "Picture of the Compatibility View button (off)") in IE to make the icon change from an outline ![Picture of the Compatibility View button (off)](https://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "Picture of the Compatibility View button (off)") to a solid color ![Picture of the Compatibility View button (on)](https://res1.windows.microsoft.com/resbox/en/Windows 7/main/156805ff-3130-481b-a12d-4d3a96470f36_14.jpg "Picture of the Compatibility View button (on)").</span></span> <span data-ttu-id="c7f75-258">또는 FireFox 또는 Chrome에서이 자습서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-258">Alternatively you can view this tutorial in FireFox or Chrome.</span></span>

<span data-ttu-id="c7f75-259">*MvcMobile\Views\Shared\\_Layout* 파일을 열고 `Html.Partial` 호출한 후에 다음 태그를 직접 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-259">Open the *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* file and add the following markup directly after the `Html.Partial` call:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample12.cshtml)]

<span data-ttu-id="c7f75-260">전체 *MvcMobile\Views\Shared\\_Layout* 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-260">The complete *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* file is shown below:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample13.cshtml)]

<span data-ttu-id="c7f75-261">응용 프로그램을 빌드하고 모바일 브라우저 에뮬레이터에서 *Alltags* 뷰로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-261">Build the application, and in your mobile browser emulator browse to the *AllTags* view.</span></span> <span data-ttu-id="c7f75-262">다음이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-262">You see the following:</span></span>

<span data-ttu-id="c7f75-263">[![p3_afterNuGet](aspnet-mvc-4-mobile-features/_static/image23.png)](aspnet-mvc-4-mobile-features/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="c7f75-263">[![p3_afterNuGet](aspnet-mvc-4-mobile-features/_static/image23.png)](aspnet-mvc-4-mobile-features/_static/image22.png)</span></span>

> [!NOTE]
> <span data-ttu-id="c7f75-264">IE 또는 Chrome에 대 한 [사용자 에이전트 문자열을](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) iPhone으로 설정 하 고 F-12 개발자 도구를 사용 하 여 모바일 관련 코드를 디버그할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-264">You can debug the mobile specific code by [setting the user agent string](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) for IE or Chrome to iPhone and then using the F-12 developer tools.</span></span> <span data-ttu-id="c7f75-265">모바일 브라우저에서 **홈**, **스피커**, **태그**및 **날짜** 링크를 단추로 표시 하지 않는 경우 jQuery mobile 스크립트와 CSS 파일에 대 한 참조가 잘못 된 것일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-265">If your mobile browser doesn't display the **Home**, **Speaker**, **Tag**, and **Date** links as buttons, the references to jQuery Mobile scripts and CSS files are probably not correct.</span></span>

<span data-ttu-id="c7f75-266">스타일을 변경 하는 것 외에도 모바일 보기와 모바일 보기에서 바탕 화면 보기로 전환할 수 있는 링크가 **표시** 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-266">In addition to the style changes, you see **Displaying mobile view** and a link that lets you switch from mobile view to desktop view.</span></span> <span data-ttu-id="c7f75-267">**바탕 화면 보기** 링크를 선택 하면 바탕 화면 뷰가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-267">Choose the **Desktop view** link, and the desktop view is displayed.</span></span>

<span data-ttu-id="c7f75-268">[![p3_desktopView](aspnet-mvc-4-mobile-features/_static/image25.png)](aspnet-mvc-4-mobile-features/_static/image24.png)</span><span class="sxs-lookup"><span data-stu-id="c7f75-268">[![p3_desktopView](aspnet-mvc-4-mobile-features/_static/image25.png)](aspnet-mvc-4-mobile-features/_static/image24.png)</span></span>

<span data-ttu-id="c7f75-269">바탕 화면 보기는 모바일 보기로 직접 다시 이동 하는 방법을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-269">The desktop view doesn't provide a way to directly navigate back to the mobile view.</span></span> <span data-ttu-id="c7f75-270">이제이 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-270">You'll fix that now.</span></span> <span data-ttu-id="c7f75-271">*Views\Shared\\_Layout* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-271">Open the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="c7f75-272">페이지 `body` 요소 바로 아래에 다음 코드를 추가 합니다 .이 코드는 뷰 전환기 위젯을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-272">Just under the page `body` element, add the following code, which renders the view-switcher widget:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample14.cshtml)]

<span data-ttu-id="c7f75-273">모바일 브라우저에서 *Alltags* 보기를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-273">Refresh the *AllTags* view in the mobile browser.</span></span> <span data-ttu-id="c7f75-274">이제 데스크톱과 모바일 보기 사이를 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-274">You can now navigate between desktop and mobile views.</span></span>

<span data-ttu-id="c7f75-275">[![p3_desktopViewWithMobileLink](aspnet-mvc-4-mobile-features/_static/image27.png)](aspnet-mvc-4-mobile-features/_static/image26.png)</span><span class="sxs-lookup"><span data-stu-id="c7f75-275">[![p3_desktopViewWithMobileLink](aspnet-mvc-4-mobile-features/_static/image27.png)](aspnet-mvc-4-mobile-features/_static/image26.png)</span></span>

> [!NOTE]
> <span data-ttu-id="c7f75-276">디버그 참고: Views\Shared _ViewSwitcher\\의 끝에 다음 코드를 추가 하 여 브라우저를 사용 하는 경우 모바일 장치에 설정 된 사용자 에이전트 문자열을 사용 하 여 뷰를 디버그할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-276">Debug note: You can add the following code to the end of the Views\Shared\\_ViewSwitcher.cshtml to help debug views when using a browser the user agent string set to a mobile device.</span></span>
>
> [!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample15.cs)]
>
> <span data-ttu-id="c7f75-277">*Views\Shared\\_Layout* 파일에 다음 제목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-277">and adding the following heading to the *Views\Shared\\_Layout.cshtml* file.</span></span>
>
> [!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample16.html)]

<span data-ttu-id="c7f75-278">데스크톱 브라우저에서 *Alltags* 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-278">Browse to the *AllTags* page in a desktop browser.</span></span> <span data-ttu-id="c7f75-279">뷰 전환기 위젯은 모바일 레이아웃 페이지에만 추가 되었으므로 데스크톱 브라우저에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-279">The view-switcher widget is not displayed in a desktop browser because it's added only to the mobile layout page.</span></span> <span data-ttu-id="c7f75-280">자습서의 뒷부분에서 보기-전환기 위젯을 바탕 화면 보기에 추가 하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-280">Later in the tutorial you'll see how you can add the view-switcher widget to the desktop view.</span></span>

<span data-ttu-id="c7f75-281">[![p3_desktopBrowser](aspnet-mvc-4-mobile-features/_static/image29.png)](aspnet-mvc-4-mobile-features/_static/image28.png)</span><span class="sxs-lookup"><span data-stu-id="c7f75-281">[![p3_desktopBrowser](aspnet-mvc-4-mobile-features/_static/image29.png)](aspnet-mvc-4-mobile-features/_static/image28.png)</span></span>

## <a name="improving-the-speakers-list"></a><span data-ttu-id="c7f75-282">발표자 목록 개선</span><span class="sxs-lookup"><span data-stu-id="c7f75-282">Improving the Speakers List</span></span>

<span data-ttu-id="c7f75-283">모바일 브라우저에서 **스피커** 링크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-283">In the mobile browser, select the **Speakers** link.</span></span> <span data-ttu-id="c7f75-284">모바일 보기 (*Allspeakers*)가 없으므로 기본 발표자 표시 (*allspeakers*)는 모바일 레이아웃 보기 ( *\_layout.* cshtml)를 사용 하 여 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-284">Because there's no mobile view(*AllSpeakers.Mobile.cshtml*), the default speakers display (*AllSpeakers.cshtml*) is rendered using the mobile layout view (*\_Layout.Mobile.cshtml*).</span></span>

<span data-ttu-id="c7f75-285">[![p3_speakersDeskTop](aspnet-mvc-4-mobile-features/_static/image31.png)](aspnet-mvc-4-mobile-features/_static/image30.png)</span><span class="sxs-lookup"><span data-stu-id="c7f75-285">[![p3_speakersDeskTop](aspnet-mvc-4-mobile-features/_static/image31.png)](aspnet-mvc-4-mobile-features/_static/image30.png)</span></span>

<span data-ttu-id="c7f75-286">다음과 같이 *뷰\\_ViewStart* 의 `true`에 `RequireConsistentDisplayMode`를 설정 하 여 모바일 레이아웃 내에서 기본 (비모바일) 뷰를 전체적으로 렌더링 하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-286">You can globally disable a default (non-mobile) view from rendering inside a mobile layout by setting `RequireConsistentDisplayMode` to `true` in the *Views\\_ViewStart.cshtml* file, like this:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample17.cshtml)]

<span data-ttu-id="c7f75-287">`RequireConsistentDisplayMode`을 `true`로 설정 하면 모바일 레이아웃 (<em>\_layout</em>)은 모바일 뷰에서만 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-287">When `RequireConsistentDisplayMode` is set to `true`, the mobile layout (<em>\_Layout.Mobile.cshtml</em>) is used only for mobile views.</span></span> <span data-ttu-id="c7f75-288">즉, 뷰 파일은 <em>\* \* ViewName</em>형식입니다<em>. 휴대폰과.)</em>모바일 레이아웃이 비모바일 보기에서 제대로 작동 하지 않는 경우 `RequireConsistentDisplayMode`를 `true` 설정 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-288">(That is, the view file is of the form <em>\*\*ViewName</em><em>.Mobile.cshtml</em>.) You might want to set `RequireConsistentDisplayMode` to `true` if your mobile layout doesn't work well with your non-mobile views.</span></span> <span data-ttu-id="c7f75-289">아래 스크린샷은 `RequireConsistentDisplayMode`이 `true`으로 설정 된 경우 <em>스피커</em> 페이지가 어떻게 렌더링 되는지 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-289">The screenshot below shows how the <em>Speakers</em> page renders when `RequireConsistentDisplayMode` is set to `true`.</span></span>

<span data-ttu-id="c7f75-290">[![p3_speakersConsistent](aspnet-mvc-4-mobile-features/_static/image33.png)](aspnet-mvc-4-mobile-features/_static/image32.png)</span><span class="sxs-lookup"><span data-stu-id="c7f75-290">[![p3_speakersConsistent](aspnet-mvc-4-mobile-features/_static/image33.png)](aspnet-mvc-4-mobile-features/_static/image32.png)</span></span>

<span data-ttu-id="c7f75-291">보기 파일의 `false` `RequireConsistentDisplayMode`을 설정 하 여 뷰에서 일관 된 표시 모드를 사용 하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-291">You can disable consistent display mode in a view by setting `RequireConsistentDisplayMode` to `false` in the view file.</span></span> <span data-ttu-id="c7f75-292">*Views\Home\AllSpeakers.cshtml* 파일의 다음 태그는 `false``RequireConsistentDisplayMode` 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-292">The following markup in the *Views\Home\AllSpeakers.cshtml* file sets `RequireConsistentDisplayMode` to `false`:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample18.cshtml)]

## <a name="creating-a-mobile-speakers-view"></a><span data-ttu-id="c7f75-293">모바일 발표자 보기 만들기</span><span class="sxs-lookup"><span data-stu-id="c7f75-293">Creating a Mobile Speakers View</span></span>

<span data-ttu-id="c7f75-294">앞서 살펴본 것 처럼 *발표자* 보기는 읽을 수 있지만 링크는 작지만 모바일 장치에서 탭 하기 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-294">As you just saw, the *Speakers* view is readable, but the links are small and are difficult to tap on a mobile device.</span></span> <span data-ttu-id="c7f75-295">이 섹션에서는 최신 모바일 응용 프로그램 처럼 보이는 모바일 특정 *발표자* 보기를 만듭니다. 여기에는 크고 간편한 링크를 표시 하 고, 스피커를 빠르게 찾을 수 있는 검색 상자가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-295">In this section, you'll create a mobile-specific *Speakers* view that looks like a modern mobile application — it displays large, easy-to-tap links and contains a search box to quickly find speakers.</span></span>

<span data-ttu-id="c7f75-296">Allspeakers를 *allspeakers* *로 복사* 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-296">Copy *AllSpeakers.cshtml* to *AllSpeakers.Mobile.cshtml*.</span></span> <span data-ttu-id="c7f75-297">*Allspeakers* 파일을 열고 `<h2>` 제목 요소를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-297">Open the *AllSpeakers.Mobile.cshtml* file and remove the `<h2>` heading element.</span></span>

<span data-ttu-id="c7f75-298">`<ul>` 태그에서 `data-role` 특성을 추가 하 고 해당 값을 `listview`로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-298">In the `<ul>` tag, add the `data-role` attribute and set its value to `listview`.</span></span> <span data-ttu-id="c7f75-299">다른 [`data-*` 특성과](http://html5doctor.com/html5-custom-data-attributes/)마찬가지로 `data-role="listview"`를 사용 하면 많은 목록 항목을 쉽게 탭 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-299">Like other [`data-*` attributes](http://html5doctor.com/html5-custom-data-attributes/), `data-role="listview"` makes the large list items easier to tap.</span></span> <span data-ttu-id="c7f75-300">완성 된 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-300">This is what the completed markup looks like:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample19.cshtml)]

<span data-ttu-id="c7f75-301">모바일 브라우저를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-301">Refresh the mobile browser.</span></span> <span data-ttu-id="c7f75-302">업데이트 된 보기는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-302">The updated view looks like this:</span></span>

<span data-ttu-id="c7f75-303">[![p3_updatedSpeakerView1](aspnet-mvc-4-mobile-features/_static/image35.png)](aspnet-mvc-4-mobile-features/_static/image34.png)</span><span class="sxs-lookup"><span data-stu-id="c7f75-303">[![p3_updatedSpeakerView1](aspnet-mvc-4-mobile-features/_static/image35.png)](aspnet-mvc-4-mobile-features/_static/image34.png)</span></span>

<span data-ttu-id="c7f75-304">모바일 보기가 개선 되었지만 긴 스피커 목록을 탐색 하기가 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-304">Although the mobile view has improved, it's difficult to navigate the long list of speakers.</span></span> <span data-ttu-id="c7f75-305">이 문제를 해결 하려면 `<ul>` 태그에서 `data-filter` 특성을 추가 하 고 `true`로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-305">To fix this, in the `<ul>` tag, add the `data-filter` attribute and set it to `true`.</span></span> <span data-ttu-id="c7f75-306">아래 코드는 `ul` 태그를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-306">The code below shows the `ul` markup.</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample20.html)]

<span data-ttu-id="c7f75-307">다음 그림은 페이지 맨 위에 `data-filter` 특성의 결과로 나타나는 검색 필터 상자를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-307">The following image shows the search filter box at the top of the page that results from the `data-filter` attribute.</span></span>

<span data-ttu-id="c7f75-308">[![ps_Data_Filter](aspnet-mvc-4-mobile-features/_static/image37.png)](aspnet-mvc-4-mobile-features/_static/image36.png)</span><span class="sxs-lookup"><span data-stu-id="c7f75-308">[![ps_Data_Filter](aspnet-mvc-4-mobile-features/_static/image37.png)](aspnet-mvc-4-mobile-features/_static/image36.png)</span></span>

<span data-ttu-id="c7f75-309">검색 상자에 각 문자를 입력 하면 jQuery Mobile에서 아래 이미지에 표시 된 것 처럼 표시 된 목록을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-309">As you type each letter in the search box, jQuery Mobile filters the displayed list as shown in the image below.</span></span>

<span data-ttu-id="c7f75-310">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image39.png)](aspnet-mvc-4-mobile-features/_static/image38.png)</span><span class="sxs-lookup"><span data-stu-id="c7f75-310">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image39.png)](aspnet-mvc-4-mobile-features/_static/image38.png)</span></span>

## <a name="improving-the-tags-list"></a><span data-ttu-id="c7f75-311">태그 목록 개선</span><span class="sxs-lookup"><span data-stu-id="c7f75-311">Improving the Tags List</span></span>

<span data-ttu-id="c7f75-312">기본 *발표자* 보기와 마찬가지로 *태그* 보기는 읽을 수 있지만 링크는 작고 모바일 장치에서 탭 하기 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-312">Like the default *Speakers* view, the *Tags* view is readable, but the links are small and difficult to tap on a mobile device.</span></span> <span data-ttu-id="c7f75-313">이 섹션에서는 *발표자* 보기를 수정 하는 것과 동일한 방식으로 *태그* 보기를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-313">In this section, you'll fix the *Tags* view the same way you fixed the *Speakers* view.</span></span>

<span data-ttu-id="c7f75-314">*Views\Home\AllTags.Mobile.cshtml.hide* 파일에 대 한 &quot;&quot; 접미사를 제거 하 여 이름을 *Views\Home\AllTags.Mobile.cshtml*로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-314">Remove the &quot;hide&quot; suffix to the *Views\Home\AllTags.Mobile.cshtml.hide* file so the name is *Views\Home\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="c7f75-315">이름을 바꾼 파일을 열고 `<h2>` 요소를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-315">Open the renamed file and remove the `<h2>` element.</span></span>

<span data-ttu-id="c7f75-316">다음과 같이 `data-role` 및 `data-filter` 특성을 `<ul>` 태그에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-316">Add the `data-role` and `data-filter` attributes to the `<ul>` tag, as shown here:</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample21.html)]

<span data-ttu-id="c7f75-317">아래 이미지는 `J`문자에 대 한 태그 페이지 필터링을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-317">The image below shows the tags page filtering on the letter `J`.</span></span>

<span data-ttu-id="c7f75-318">[![p3_tags_J](aspnet-mvc-4-mobile-features/_static/image41.png)](aspnet-mvc-4-mobile-features/_static/image40.png)</span><span class="sxs-lookup"><span data-stu-id="c7f75-318">[![p3_tags_J](aspnet-mvc-4-mobile-features/_static/image41.png)](aspnet-mvc-4-mobile-features/_static/image40.png)</span></span>

## <a name="improving-the-dates-list"></a><span data-ttu-id="c7f75-319">날짜 목록 개선</span><span class="sxs-lookup"><span data-stu-id="c7f75-319">Improving the Dates List</span></span>

<span data-ttu-id="c7f75-320">*발표자* 및 *태그* 보기를 개선 한 것 처럼 *날짜* 뷰를 개선 하 여 모바일 장치에서 더 쉽게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-320">You can improve the *Dates* view like you improved the *Speakers* and *Tags* views, so that it's easier to use on a mobile device.</span></span>

<span data-ttu-id="c7f75-321">*Views\Home\AllDates.cshtml* 파일을 *Views\Home\AllDates.Mobile.cshtml*에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-321">Copy the *Views\Home\AllDates.cshtml* file to *Views\Home\AllDates.Mobile.cshtml*.</span></span> <span data-ttu-id="c7f75-322">새 파일을 열고 `<h2>` 요소를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-322">Open the new file and remove the `<h2>` element.</span></span>

<span data-ttu-id="c7f75-323">다음과 같이 `<ul>` 태그에 `data-role="listview"`를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-323">Add `data-role="listview"` to the `<ul>` tag, like this:</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample22.html)]

<span data-ttu-id="c7f75-324">아래 이미지는 `data-role` 특성을 사용 하 여 **날짜** 페이지의 모양을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-324">The image below shows what the **Date** page looks like with the `data-role` attribute in place.</span></span>

<span data-ttu-id="c7f75-325">[![p3_dates1](aspnet-mvc-4-mobile-features/_static/image43.png)](aspnet-mvc-4-mobile-features/_static/image42.png) *Views\Home\AllDates.Mobile.cshtml* 파일의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-325">[![p3_dates1](aspnet-mvc-4-mobile-features/_static/image43.png)](aspnet-mvc-4-mobile-features/_static/image42.png) Replace the contents of the *Views\Home\AllDates.Mobile.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample23.cshtml)]

<span data-ttu-id="c7f75-326">이 코드는 모든 세션을 일별로 그룹화 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-326">This code groups all sessions by days.</span></span> <span data-ttu-id="c7f75-327">새 날짜에 대 한 목록 구분선을 만들고 각 날짜에 대 한 모든 세션을 구분선 아래에 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-327">It creates a list divider for each new day, and it lists all the sessions for each day under a divider.</span></span> <span data-ttu-id="c7f75-328">이 코드가 실행 될 때 표시 되는 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-328">Here's what it looks like when this code runs:</span></span>

<span data-ttu-id="c7f75-329">[![p3_dates2](aspnet-mvc-4-mobile-features/_static/image45.png)](aspnet-mvc-4-mobile-features/_static/image44.png)</span><span class="sxs-lookup"><span data-stu-id="c7f75-329">[![p3_dates2](aspnet-mvc-4-mobile-features/_static/image45.png)](aspnet-mvc-4-mobile-features/_static/image44.png)</span></span>

## <a name="improving-the-sessionstable-view"></a><span data-ttu-id="c7f75-330">SessionsTable 된 뷰 개선</span><span class="sxs-lookup"><span data-stu-id="c7f75-330">Improving the SessionsTable View</span></span>

<span data-ttu-id="c7f75-331">이 섹션에서는 세션의 모바일 관련 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-331">In this section, you'll create a mobile-specific view of sessions.</span></span> <span data-ttu-id="c7f75-332">변경 내용은 만든 다른 보기 보다 더 광범위 하 게 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-332">The changes we make will be more extensive than in other views we have created.</span></span>

<span data-ttu-id="c7f75-333">모바일 브라우저에서 **스피커** 단추를 탭 한 다음 검색 상자에 `Sc`을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-333">In the mobile browser, tap the **Speaker** button, then enter `Sc` in the search box.</span></span>

<span data-ttu-id="c7f75-334">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image47.png)](aspnet-mvc-4-mobile-features/_static/image46.png)</span><span class="sxs-lookup"><span data-stu-id="c7f75-334">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image47.png)](aspnet-mvc-4-mobile-features/_static/image46.png)</span></span>

<span data-ttu-id="c7f75-335">**Scott Hanselman** 링크를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-335">Tap the **Scott Hanselman** link.</span></span>

<span data-ttu-id="c7f75-336">[![p3_scottHa](aspnet-mvc-4-mobile-features/_static/image49.png)](aspnet-mvc-4-mobile-features/_static/image48.png)</span><span class="sxs-lookup"><span data-stu-id="c7f75-336">[![p3_scottHa](aspnet-mvc-4-mobile-features/_static/image49.png)](aspnet-mvc-4-mobile-features/_static/image48.png)</span></span>

<span data-ttu-id="c7f75-337">여기에서 볼 수 있듯이 모바일 브라우저에서는 표시를 읽기가 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-337">As you can see, the display is difficult to read on a mobile browser.</span></span> <span data-ttu-id="c7f75-338">날짜 열을 읽기 어려울 때 태그 열이 보기를 벗어났습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-338">The date column is hard to read and the tags column is out of the view.</span></span> <span data-ttu-id="c7f75-339">이 문제를 해결 하려면 *Views\Home\SessionsTable.cshtml* 를 *Views\Home\SessionsTable.Mobile.cshtml*에 복사 하 고 파일의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-339">To fix this, copy *Views\Home\SessionsTable.cshtml* to *Views\Home\SessionsTable.Mobile.cshtml*, and then replace the contents of the file with the following code:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample24.cshtml)]

<span data-ttu-id="c7f75-340">이 코드는 대화방 및 태그 열을 제거 하 고 제목, 스피커 및 날짜를 세로로 서식 지정 하 여 모든 정보를 모바일 브라우저에서 읽을 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-340">The code removes the room and tags columns, and formats the title, speaker, and date vertically, so that all this information is readable on a mobile browser.</span></span> <span data-ttu-id="c7f75-341">다음 이미지는 코드 변경 내용을 반영 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-341">The image below reflects the code changes.</span></span>

<span data-ttu-id="c7f75-342">[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image51.png)](aspnet-mvc-4-mobile-features/_static/image50.png)</span><span class="sxs-lookup"><span data-stu-id="c7f75-342">[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image51.png)](aspnet-mvc-4-mobile-features/_static/image50.png)</span></span>

## <a name="improving-the-sessionbycode-view"></a><span data-ttu-id="c7f75-343">SessionByCode 뷰 개선</span><span class="sxs-lookup"><span data-stu-id="c7f75-343">Improving the SessionByCode View</span></span>

<span data-ttu-id="c7f75-344">마지막으로 *Sessionbycode* 뷰의 모바일 관련 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-344">Finally, you'll create a mobile-specific view of the *SessionByCode* view.</span></span> <span data-ttu-id="c7f75-345">모바일 브라우저에서 **스피커** 단추를 탭 한 다음 검색 상자에 `Sc`을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-345">In the mobile browser, tap the **Speaker** button, then enter `Sc` in the search box.</span></span>

<span data-ttu-id="c7f75-346">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image53.png)](aspnet-mvc-4-mobile-features/_static/image52.png)</span><span class="sxs-lookup"><span data-stu-id="c7f75-346">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image53.png)](aspnet-mvc-4-mobile-features/_static/image52.png)</span></span>

<span data-ttu-id="c7f75-347">**Scott Hanselman** 링크를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-347">Tap the **Scott Hanselman** link.</span></span> <span data-ttu-id="c7f75-348">Scott Hanselman의 세션이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-348">Scott Hanselman's sessions are displayed.</span></span>

<span data-ttu-id="c7f75-349">[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image55.png)](aspnet-mvc-4-mobile-features/_static/image54.png)</span><span class="sxs-lookup"><span data-stu-id="c7f75-349">[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image55.png)](aspnet-mvc-4-mobile-features/_static/image54.png)</span></span>

<span data-ttu-id="c7f75-350">웹 링크 **의 MS 웹 스택에 대 한 개요** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-350">Choose the **An Overview of the MS Web Stack of Love** link.</span></span>

<span data-ttu-id="c7f75-351">[![ps_love](aspnet-mvc-4-mobile-features/_static/image57.png)](aspnet-mvc-4-mobile-features/_static/image56.png)</span><span class="sxs-lookup"><span data-stu-id="c7f75-351">[![ps_love](aspnet-mvc-4-mobile-features/_static/image57.png)](aspnet-mvc-4-mobile-features/_static/image56.png)</span></span>

<span data-ttu-id="c7f75-352">기본 바탕 화면 보기는 문제가 없지만 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-352">The default desktop view is fine, but you can improve it.</span></span>

<span data-ttu-id="c7f75-353">*Views\Home\SessionByCode.cshtml* 을 *Views\Home\SessionByCode.Mobile.cshtml* 에 복사 하 고 *Views\Home\SessionByCode.Mobile.cshtml* 파일의 내용을 다음 태그로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-353">Copy the *Views\Home\SessionByCode.cshtml* to *Views\Home\SessionByCode.Mobile.cshtml* and replace the contents of the *Views\Home\SessionByCode.Mobile.cshtml* file with the following markup:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample25.cshtml)]

<span data-ttu-id="c7f75-354">새 태그는 `data-role` 특성을 사용 하 여 뷰의 레이아웃을 향상 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-354">The new markup uses the `data-role` attribute to improve the layout of the view.</span></span>

<span data-ttu-id="c7f75-355">모바일 브라우저를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-355">Refresh the mobile browser.</span></span> <span data-ttu-id="c7f75-356">다음 이미지는 방금 만든 코드 변경 내용을 반영 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-356">The following image reflects the code changes that you just made:</span></span>

<span data-ttu-id="c7f75-357">[![p3_love2](aspnet-mvc-4-mobile-features/_static/image59.png)](aspnet-mvc-4-mobile-features/_static/image58.png)</span><span class="sxs-lookup"><span data-stu-id="c7f75-357">[![p3_love2](aspnet-mvc-4-mobile-features/_static/image59.png)](aspnet-mvc-4-mobile-features/_static/image58.png)</span></span>

## <a name="wrapup-and-review"></a><span data-ttu-id="c7f75-358">Wrapup 및 검토</span><span class="sxs-lookup"><span data-stu-id="c7f75-358">Wrapup and Review</span></span>

<span data-ttu-id="c7f75-359">이 자습서에서는 ASP.NET MVC 4 Developer Preview의 새로운 모바일 기능을 소개 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-359">This tutorial has introduced the new mobile features of ASP.NET MVC 4 Developer Preview.</span></span> <span data-ttu-id="c7f75-360">모바일 기능에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-360">The mobile features include:</span></span>

- <span data-ttu-id="c7f75-361">전역 및 개별 뷰에 대해 레이아웃, 뷰 및 부분 뷰를 재정의 하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-361">The ability to override layout, views, and partial views, both globally and for an individual view.</span></span>
- <span data-ttu-id="c7f75-362">`RequireConsistentDisplayMode` 속성을 사용 하 여 레이아웃 및 부분 재정의 적용을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-362">Control over layout and partial override enforcement using the `RequireConsistentDisplayMode` property.</span></span>
- <span data-ttu-id="c7f75-363">모바일 보기에 대 한 뷰 전환기 위젯을 바탕 화면 보기에 표시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f75-363">A view-switcher widget for mobile views than can also be displayed in desktop views.</span></span>
- <span data-ttu-id="c7f75-364">IPhone 브라우저와 같은 특정 브라우저 지원 지원</span><span class="sxs-lookup"><span data-stu-id="c7f75-364">Support for supporting specific browsers, such as the iPhone browser.</span></span>

## <a name="see-also"></a><span data-ttu-id="c7f75-365">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c7f75-365">See Also</span></span>

- <span data-ttu-id="c7f75-366">[JQuery 모바일](http://jquerymobile.com) 사이트.</span><span class="sxs-lookup"><span data-stu-id="c7f75-366">[jQuery Mobile](http://jquerymobile.com) site.</span></span>
- [<span data-ttu-id="c7f75-367">jQuery 모바일 개요</span><span class="sxs-lookup"><span data-stu-id="c7f75-367">jQuery Mobile Overview</span></span>](http://jquerymobile.com/demos/1.0b3/docs/about/intro.html)
- [<span data-ttu-id="c7f75-368">W3C 권장 사항 모바일 웹 응용 프로그램 모범 사례</span><span class="sxs-lookup"><span data-stu-id="c7f75-368">W3C Recommendation Mobile Web Application Best Practices</span></span>](http://www.w3.org/TR/mwabp/)
- [<span data-ttu-id="c7f75-369">미디어 쿼리에 대 한 W3C 후보 권장 사항</span><span class="sxs-lookup"><span data-stu-id="c7f75-369">W3C Candidate Recommendation for media queries</span></span>](http://www.w3.org/TR/css3-mediaqueries/)
