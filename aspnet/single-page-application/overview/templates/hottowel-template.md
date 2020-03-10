---
uid: single-page-application/overview/templates/hottowel-template
title: Hot 수건 템플릿 | Microsoft Docs
author: madskristensen
description: HotTowel 템플릿
ms.author: riande
ms.date: 02/09/2013
ms.assetid: 75af2e17-6ed3-4d24-8ea1-bc340027c318
msc.legacyurl: /single-page-application/overview/templates/hottowel-template
msc.type: authoredcontent
ms.openlocfilehash: eeab69e75546791978bb09d7823d95caf9dca1a0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467141"
---
# <a name="hot-towel-template"></a><span data-ttu-id="e621b-103">Hot Towel 템플릿</span><span class="sxs-lookup"><span data-stu-id="e621b-103">Hot Towel template</span></span>

<span data-ttu-id="e621b-104">[Mads Kristensen](https://github.com/madskristensen)</span><span class="sxs-lookup"><span data-stu-id="e621b-104">by [Mads Kristensen](https://github.com/madskristensen)</span></span>

> <span data-ttu-id="e621b-105">수건 MVC 템플릿은 John Papa에 의해 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-105">The Hot Towel MVC Template is written by John Papa</span></span>
> 
> <span data-ttu-id="e621b-106">다운로드할 버전 선택:</span><span class="sxs-lookup"><span data-stu-id="e621b-106">Choose which version to download:</span></span>
> 
> [<span data-ttu-id="e621b-107">Visual Studio 2012 용 핫 수건 MVC 템플릿</span><span class="sxs-lookup"><span data-stu-id="e621b-107">Hot Towel MVC Template for Visual Studio 2012</span></span>](https://visualstudiogallery.msdn.microsoft.com/1f68fbe8-b4e9-4968-9fd3-ddc7cbc52dca)
> 
> [<span data-ttu-id="e621b-108">Visual Studio 2013에 대 한 Hot 수건 MVC 템플릿</span><span class="sxs-lookup"><span data-stu-id="e621b-108">Hot Towel MVC Template for Visual Studio 2013</span></span>](https://visualstudiogallery.msdn.microsoft.com/1eb8780d-d522-4dcf-bf56-56f0eab305c2)
> 
> 
> <span data-ttu-id="e621b-109">Hot 수건: SPA로 이동 하지 않으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-109">Hot Towel: Because you don't want to go to the SPA without one!</span></span>

<span data-ttu-id="e621b-110">SPA를 빌드하려고 하지만 시작할 위치를 결정할 수 없나요?</span><span class="sxs-lookup"><span data-stu-id="e621b-110">Want to build a SPA but can't decide where to start?</span></span> <span data-ttu-id="e621b-111">상시 수건를 사용 하 고 몇 초 안에 SPA 및 모든 도구를 구축 해야 합니다!</span><span class="sxs-lookup"><span data-stu-id="e621b-111">Use Hot Towel and in seconds you'll have a SPA and all the tools you need to build on it!</span></span>

<span data-ttu-id="e621b-112">Hot 수건는 ASP.NET를 사용 하 여 SPA (단일 페이지 응용 프로그램)를 빌드하기 위한 좋은 시작점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-112">Hot Towel creates a great starting point for building a Single Page Application (SPA) with ASP.NET.</span></span> <span data-ttu-id="e621b-113">기본적으로 코드에 대 한 모듈식 구조, 보기 탐색, 데이터 바인딩, 다양 한 데이터 관리 및 간단 하지만 세련 된 스타일을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-113">Out of the box you it provides a modular structure for your code, view navigation, data binding, rich data management and simple but elegant styling.</span></span> <span data-ttu-id="e621b-114">핫 수건는 SPA를 구축 하는 데 필요한 모든 것을 제공 하므로, 앱에 집중할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-114">Hot Towel provides everything you need to build a SPA, so you can focus on your app, not the plumbing.</span></span>

> <span data-ttu-id="e621b-115">[John Papa의 비디오, 자습서 및 Pluralsight 과정](http://johnpapa.net/spa?vsix)에서 SPA를 구축 하는 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="e621b-115">Learn more about building a SPA from [John Papa's videos, tutorials and Pluralsight courses](http://johnpapa.net/spa?vsix).</span></span>

## <a name="application-structure"></a><span data-ttu-id="e621b-116">응용 프로그램 구조</span><span class="sxs-lookup"><span data-stu-id="e621b-116">Application Structure</span></span>

<span data-ttu-id="e621b-117">Hot 수건 SPA는 응용 프로그램을 정의 하는 JavaScript 및 HTML 파일이 포함 된 앱 폴더를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-117">Hot Towel SPA provides an App folder which contains the JavaScript and HTML files that define your application.</span></span>

<span data-ttu-id="e621b-118">앱 폴더 내:</span><span class="sxs-lookup"><span data-stu-id="e621b-118">Inside the App folder:</span></span>

- <span data-ttu-id="e621b-119">durandal</span><span class="sxs-lookup"><span data-stu-id="e621b-119">durandal</span></span>
- <span data-ttu-id="e621b-120">services</span><span class="sxs-lookup"><span data-stu-id="e621b-120">services</span></span>
- <span data-ttu-id="e621b-121">viewmodel</span><span class="sxs-lookup"><span data-stu-id="e621b-121">viewmodels</span></span>
- <span data-ttu-id="e621b-122">뷰</span><span class="sxs-lookup"><span data-stu-id="e621b-122">views</span></span>

<span data-ttu-id="e621b-123">앱 폴더에는 모듈의 컬렉션이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-123">The App folder contains a collection of modules.</span></span> <span data-ttu-id="e621b-124">이러한 모듈은 기능을 캡슐화 하 고 다른 모듈에 대 한 종속성을 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-124">These modules encapsulate functionality and declare dependencies on other modules.</span></span> <span data-ttu-id="e621b-125">Views 폴더에는 응용 프로그램에 대 한 HTML이 포함 되며 viewmodel 폴더에는 보기에 대 한 프레젠테이션 논리 (일반적인 MVVM 패턴)가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-125">The views folder contains the HTML for your application and the viewmodels folder contains the presentation logic for the views (a common MVVM pattern).</span></span> <span data-ttu-id="e621b-126">서비스 폴더는 HTTP 데이터 검색 또는 로컬 저장소 상호 작용과 같이 응용 프로그램에 필요할 수 있는 모든 공통 서비스를 보관 하는 데 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-126">The services folder is ideal for housing any common services that your application may need such as HTTP data retrieval or local storage interaction.</span></span> <span data-ttu-id="e621b-127">여러 viewmodel에서 서비스 모듈의 코드를 다시 사용 하는 것이 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-127">It is common for multiple viewmodels to re-use code from the service modules.</span></span>

## <a name="aspnet-mvc-server-side-application-structure"></a><span data-ttu-id="e621b-128">ASP.NET MVC 서버 쪽 응용 프로그램 구조</span><span class="sxs-lookup"><span data-stu-id="e621b-128">ASP.NET MVC Server Side Application Structure</span></span>

<span data-ttu-id="e621b-129">핫 수건는 친숙 하 고 강력한 ASP.NET MVC 구조를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-129">Hot Towel builds on the familiar and powerful ASP.NET MVC structure.</span></span>

- <span data-ttu-id="e621b-130">앱\_시작</span><span class="sxs-lookup"><span data-stu-id="e621b-130">App\_Start</span></span>
- <span data-ttu-id="e621b-131">콘텐츠</span><span class="sxs-lookup"><span data-stu-id="e621b-131">Content</span></span>
- <span data-ttu-id="e621b-132">Controllers</span><span class="sxs-lookup"><span data-stu-id="e621b-132">Controllers</span></span>
- <span data-ttu-id="e621b-133">모델</span><span class="sxs-lookup"><span data-stu-id="e621b-133">Models</span></span>
- <span data-ttu-id="e621b-134">스크립트</span><span class="sxs-lookup"><span data-stu-id="e621b-134">Scripts</span></span>
- <span data-ttu-id="e621b-135">뷰</span><span class="sxs-lookup"><span data-stu-id="e621b-135">Views</span></span>

## <a name="featured-libraries"></a><span data-ttu-id="e621b-136">주요 라이브러리</span><span class="sxs-lookup"><span data-stu-id="e621b-136">Featured Libraries</span></span>

- <span data-ttu-id="e621b-137">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="e621b-137">ASP.NET MVC</span></span>
- <span data-ttu-id="e621b-138">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="e621b-138">ASP.NET Web API</span></span>
- <span data-ttu-id="e621b-139">ASP.NET 웹 최적화-묶음 및 축소</span><span class="sxs-lookup"><span data-stu-id="e621b-139">ASP.NET Web Optimization - bundling and minification</span></span>
- <span data-ttu-id="e621b-140">[간편](http://Breezejs.com) 하 게 .js-풍부한 데이터 관리</span><span class="sxs-lookup"><span data-stu-id="e621b-140">[Breeze.js](http://Breezejs.com) - rich data management</span></span>
- <span data-ttu-id="e621b-141">[Durandal](http://Durandaljs.com) -탐색 및 뷰 컴퍼지션</span><span class="sxs-lookup"><span data-stu-id="e621b-141">[Durandal.js](http://Durandaljs.com) - navigation and View composition</span></span>
- <span data-ttu-id="e621b-142">[.Js](http://Knockoutjs.com) -데이터 바인딩</span><span class="sxs-lookup"><span data-stu-id="e621b-142">[Knockout.js](http://Knockoutjs.com) - data bindings</span></span>
- <span data-ttu-id="e621b-143">[Node.js 필요](http://requirejs.org) -AMD 및 최적화를 사용한 모듈화</span><span class="sxs-lookup"><span data-stu-id="e621b-143">[Require.js](http://requirejs.org) - Modularity with AMD and optimization</span></span>
- <span data-ttu-id="e621b-144">[To a](http://jpapa.me/c7toastr) 팝업 메시지</span><span class="sxs-lookup"><span data-stu-id="e621b-144">[Toastr.js](http://jpapa.me/c7toastr) - pop-up messages</span></span>
- <span data-ttu-id="e621b-145">[Twitter 부트스트랩](https://twitter.github.com/bootstrap/) -강력한 CSS 스타일 지정</span><span class="sxs-lookup"><span data-stu-id="e621b-145">[Twitter Bootstrap](https://twitter.github.com/bootstrap/) - robust CSS styling</span></span>

## <a name="installing-via-the-visual-studio-2012-hot-towel-spa-template"></a><span data-ttu-id="e621b-146">Visual Studio 2012 핫 수건 SPA 템플릿을 통해 설치</span><span class="sxs-lookup"><span data-stu-id="e621b-146">Installing via the Visual Studio 2012 Hot Towel SPA Template</span></span>

<span data-ttu-id="e621b-147">Hot 수건은 Visual Studio 2012 템플릿으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-147">Hot Towel can be installed as a Visual Studio 2012 template.</span></span> <span data-ttu-id="e621b-148">`File` | `New Project` 클릭 하 고 `ASP.NET MVC 4 Web Application`를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-148">Just click `File` | `New Project` and choose `ASP.NET MVC 4 Web Application`.</span></span> <span data-ttu-id="e621b-149">그런 다음 ' Hot 수건 단일 페이지 응용 프로그램 "템플릿을 선택 하 고 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-149">Then select the 'Hot Towel Single Page Application" template and run!</span></span>

## <a name="installing-via-the-nuget-package"></a><span data-ttu-id="e621b-150">NuGet 패키지를 통해 설치</span><span class="sxs-lookup"><span data-stu-id="e621b-150">Installing via the NuGet Package</span></span>

<span data-ttu-id="e621b-151">Hot 수건는 기존의 빈 ASP.NET MVC 프로젝트를 보강 하는 NuGet 패키지 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-151">Hot Towel is also a NuGet package that augments an existing empty ASP.NET MVC project.</span></span> <span data-ttu-id="e621b-152">Nuget을 사용 하 여 설치 하 고 실행 하세요.</span><span class="sxs-lookup"><span data-stu-id="e621b-152">Just install using Nuget and then run!</span></span>

[!code-powershell[Main](hottowel-template/samples/sample1.ps1)]

## <a name="how-do-i-build-on-hot-towel"></a><span data-ttu-id="e621b-153">핫 수건에서 빌드하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="e621b-153">How Do I Build On Hot Towel?</span></span>

<span data-ttu-id="e621b-154">단순히 코드 추가를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-154">Simply start adding code!</span></span>

1. <span data-ttu-id="e621b-155">사용자 고유의 서버 쪽 코드, 특히 Entity Framework 및 WebAPI를 추가 합니다 (이는 간단한 .js를 사용 하 여).</span><span class="sxs-lookup"><span data-stu-id="e621b-155">Add your own server-side code, preferably Entity Framework and WebAPI (which really shine with Breeze.js)</span></span>
2. <span data-ttu-id="e621b-156">`App/views` 폴더에 보기 추가</span><span class="sxs-lookup"><span data-stu-id="e621b-156">Add views to the `App/views` folder</span></span>
3. <span data-ttu-id="e621b-157">`App/viewmodels` 폴더에 viewmodel 추가</span><span class="sxs-lookup"><span data-stu-id="e621b-157">Add viewmodels to the `App/viewmodels` folder</span></span>
4. <span data-ttu-id="e621b-158">HTML 추가 및 새 뷰에 데이터 바인딩 녹아웃</span><span class="sxs-lookup"><span data-stu-id="e621b-158">Add HTML and Knockout data bindings to your new views</span></span>
5. <span data-ttu-id="e621b-159">`shell.js`의 탐색 경로를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-159">Update the navigation routes in `shell.js`</span></span>

## <a name="walkthrough-of-the-htmljavascript"></a><span data-ttu-id="e621b-160">HTML/JavaScript 연습</span><span class="sxs-lookup"><span data-stu-id="e621b-160">Walkthrough of the HTML/JavaScript</span></span>

### <a name="viewshottowelindexcshtml"></a><span data-ttu-id="e621b-161">Views/HotTowel/index.cshtml</span><span class="sxs-lookup"><span data-stu-id="e621b-161">Views/HotTowel/index.cshtml</span></span>

<span data-ttu-id="e621b-162">index. cshtml는 MVC 응용 프로그램의 시작 경로 및 뷰입니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-162">index.cshtml is the starting route and view for the MVC application.</span></span> <span data-ttu-id="e621b-163">여기에는 모든 표준 meta 태그, css 링크 및 원하는 JavaScript 참조가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-163">It contains all the standard meta tags, css links, and JavaScript references you would expect.</span></span> <span data-ttu-id="e621b-164">본문에는 모든 콘텐츠 (보기)가 요청 될 때 배치 되는 단일 `<div>` 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-164">The body contains a single `<div>` which is where all of the content (your views) will be placed when they are requested.</span></span> <span data-ttu-id="e621b-165">`@Scripts.Render`를 사용 하 여 `main.js` 파일에 포함 된 응용 프로그램 코드에 대 한 입구 지점을 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-165">The `@Scripts.Render` uses Require.js to run the entrance point for the application's code, which is contained in the `main.js` file.</span></span> <span data-ttu-id="e621b-166">앱이 로드 되는 동안 시작 화면을 만드는 방법을 보여 주기 위해 시작 화면이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-166">A splash screen is provided to demonstrate how to create a splash screen while your app loads.</span></span>

[!code-cshtml[Main](hottowel-template/samples/sample2.cshtml)]

### <a name="appmainjs"></a><span data-ttu-id="e621b-167">앱/기본 .js</span><span class="sxs-lookup"><span data-stu-id="e621b-167">App/main.js</span></span>

<span data-ttu-id="e621b-168">`main.js` 파일에는 앱이 로드 되는 즉시 실행 되는 코드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-168">The `main.js` file contains the code that will run as soon as your app is loaded.</span></span> <span data-ttu-id="e621b-169">탐색 경로를 정의 하 고, 시작 뷰를 설정 하 고, 응용 프로그램의 데이터를 준비 하는 등의 설정/부트스트래핑을 수행 하려는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-169">This is where you want to define your navigation routes, set your start up views, and perform any setup/bootstrapping such as priming your application's data.</span></span>

<span data-ttu-id="e621b-170">`main.js` 파일은 응용 프로그램 시작에 도움이 되는 몇 가지 durandal 모듈을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-170">The `main.js` file defines several of durandal's modules to help the application kick start.</span></span> <span data-ttu-id="e621b-171">Define 문은 모듈 종속성을 확인 하는 데 도움이 되며 함수에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-171">The define statement helps resolve the modules dependencies so they are available for the function.</span></span> <span data-ttu-id="e621b-172">먼저 디버깅 메시지를 사용할 수 있으며,이는 응용 프로그램이 콘솔 창에 수행 중인 이벤트에 대 한 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-172">First the debugging messages are enabled, which send messages about what events the application is performing to the console window.</span></span> <span data-ttu-id="e621b-173">응용 프로그램 시작 코드는 응용 프로그램을 시작 하도록 durandal framework에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-173">The app.start code tells durandal framework to start the application.</span></span> <span data-ttu-id="e621b-174">규칙은 durandal가 모든 뷰와 viewmodel 동일한 명명 된 폴더에 포함 되어 있음을 알 수 있도록 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-174">The conventions are set so that durandal knows all views and viewmodels are contained in the same named folders, respectively.</span></span> <span data-ttu-id="e621b-175">마지막으로 `app.setRoot`는 미리 정의 된 `entrance` 애니메이션을 사용 하 여 `shell`을 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-175">Finally, the `app.setRoot` kicks loads the `shell` using a predefined `entrance` animation.</span></span>

[!code-javascript[Main](hottowel-template/samples/sample3.js)]

## <a name="views"></a><span data-ttu-id="e621b-176">뷰</span><span class="sxs-lookup"><span data-stu-id="e621b-176">Views</span></span>

<span data-ttu-id="e621b-177">보기는 `App/views` 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-177">Views are found in the `App/views` folder.</span></span>

### <a name="shellhtml"></a><span data-ttu-id="e621b-178">shell.html</span><span class="sxs-lookup"><span data-stu-id="e621b-178">shell.html</span></span>

<span data-ttu-id="e621b-179">`shell.html`는 HTML에 대 한 마스터 레이아웃을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-179">The `shell.html` contains the master layout for your HTML.</span></span> <span data-ttu-id="e621b-180">다른 모든 보기는 `shell` 보기의 한쪽에 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-180">All of your other views will be composed somewhere in side of your `shell` view.</span></span> <span data-ttu-id="e621b-181">Hot 수건는 머리글, 콘텐츠 영역 및 바닥글의 세 가지 영역을 포함 하는 `shell`를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-181">Hot Towel provides a `shell` with three such regions: a header, a content area, and a footer.</span></span> <span data-ttu-id="e621b-182">이러한 각 지역은 요청 시 내용 폼과 함께 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-182">Each of these regions is loaded with contents form other views when requested.</span></span>

<span data-ttu-id="e621b-183">머리글 및 바닥글에 대 한 `compose` 바인딩은 각각 `nav` 및 `footer` 뷰를 가리키도록 핫 수건 하드 코딩 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-183">The `compose` bindings for the header and footer are hard coded in Hot Towel to point to the `nav` and `footer` views, respectively.</span></span> <span data-ttu-id="e621b-184">`#content` 섹션의 작성 바인딩은 `router` 모듈의 활성 항목에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-184">The compose binding for the section `#content` is bound to the `router` module's active item.</span></span> <span data-ttu-id="e621b-185">즉, 탐색 링크를 클릭 하면 해당 뷰가이 영역에 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-185">In other words, when you click a navigation link it's corresponding view is loaded in this area.</span></span>

[!code-html[Main](hottowel-template/samples/sample4.html)]

### <a name="navhtml"></a><span data-ttu-id="e621b-186">nav.html</span><span class="sxs-lookup"><span data-stu-id="e621b-186">nav.html</span></span>

<span data-ttu-id="e621b-187">`nav.html`은 SPA에 대 한 탐색 링크를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-187">The `nav.html` contains the navigation links for the SPA.</span></span> <span data-ttu-id="e621b-188">예를 들어 메뉴 구조를 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-188">This is where the menu structure can be placed, for example.</span></span> <span data-ttu-id="e621b-189">이는 `shell.js`에서 정의한 탐색을 표시 하는 데 사용 되는 데이터 바인딩 (녹아웃 사용)이 `router` 모듈에 자주 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-189">Often this is data bound (using Knockout) to the `router` module to display the navigation you defined in the `shell.js`.</span></span> <span data-ttu-id="e621b-190">녹아웃은 데이터 바인딩 특성을 검색 하 여 탐색 경로를 표시 하 고 `router` 모듈이 한 뷰에서 다른 뷰로 이동 하는 중에는 (Twitter 부트스트랩 사용) progressbar를 표시 하는 `shell` viewmodel에 바인딩합니다 (`router.isNavigating`참조).</span><span class="sxs-lookup"><span data-stu-id="e621b-190">Knockout looks for the data-bind attributes and binds those to the `shell` viewmodel to display the navigation routes and to show a progressbar (using Twitter Bootstrap) if the `router` module is in the middle of navigating from one view to another (see `router.isNavigating`).</span></span>

[!code-html[Main](hottowel-template/samples/sample5.html)]

### <a name="homehtml-and-detailshtml"></a><span data-ttu-id="e621b-191">.html 및 details</span><span class="sxs-lookup"><span data-stu-id="e621b-191">home.html and details.html</span></span>

<span data-ttu-id="e621b-192">이러한 보기에는 사용자 지정 보기에 대 한 HTML이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-192">These views contain HTML for custom views.</span></span> <span data-ttu-id="e621b-193">`nav` 보기 메뉴의 `home` 링크를 클릭 하면 `home` 뷰가 `shell` 뷰의 콘텐츠 영역에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-193">When the `home` link in the `nav` view's menu is clicked, the `home` view will be placed in the content area of the `shell` view.</span></span> <span data-ttu-id="e621b-194">이러한 보기를 사용자 지정 보기로 확대 하거나 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-194">These views can be augmented or replaced with your own custom views.</span></span>

### <a name="footerhtml"></a><span data-ttu-id="e621b-195">footer.html</span><span class="sxs-lookup"><span data-stu-id="e621b-195">footer.html</span></span>

<span data-ttu-id="e621b-196">`footer.html`는 바닥글에 `shell` 보기의 맨 아래에 나타나는 HTML을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-196">The `footer.html` contains HTML that appears in the footer, at the bottom of the `shell` view.</span></span>

## <a name="viewmodels"></a><span data-ttu-id="e621b-197">ViewModels</span><span class="sxs-lookup"><span data-stu-id="e621b-197">ViewModels</span></span>

<span data-ttu-id="e621b-198">ViewModels은 `App/viewmodels` 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-198">ViewModels are found in the `App/viewmodels` folder.</span></span>

### <a name="shelljs"></a><span data-ttu-id="e621b-199">shell .js</span><span class="sxs-lookup"><span data-stu-id="e621b-199">shell.js</span></span>

<span data-ttu-id="e621b-200">`shell` viewmodel에는 `shell` 뷰에 바인딩된 속성 및 함수가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-200">The `shell` viewmodel contains properties and functions that are bound to the `shell` view.</span></span> <span data-ttu-id="e621b-201">메뉴 탐색 바인딩이 발견 되는 경우가 종종 있습니다 (`router.mapNav` 논리 참조).</span><span class="sxs-lookup"><span data-stu-id="e621b-201">Often this is where the menu navigation bindings are found (see the `router.mapNav` logic).</span></span>

[!code-javascript[Main](hottowel-template/samples/sample6.js)]

### <a name="homejs-and-detailsjs"></a><span data-ttu-id="e621b-202">default.js 및 세부 정보 .js</span><span class="sxs-lookup"><span data-stu-id="e621b-202">home.js and details.js</span></span>

<span data-ttu-id="e621b-203">이러한 viewmodel `home` 뷰에 바인딩되는 속성 및 함수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-203">These viewmodels contain the properties and functions that are bound to the `home` view.</span></span> <span data-ttu-id="e621b-204">또한 보기의 프레젠테이션 논리를 포함 하며 데이터와 뷰 간의 붙이기가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-204">it also contains the presentation logic for the view, and is the glue between the data and the view.</span></span>

[!code-javascript[Main](hottowel-template/samples/sample7.js)]

## <a name="services"></a><span data-ttu-id="e621b-205">Services</span><span class="sxs-lookup"><span data-stu-id="e621b-205">Services</span></span>

<span data-ttu-id="e621b-206">서비스는 App/services 폴더에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-206">Services are found in the App/services folder.</span></span> <span data-ttu-id="e621b-207">원격 데이터 가져오기 및 게시를 담당 하는 dataservice 모듈과 같은 향후 서비스를 배치할 수 있는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-207">Ideally your future services such as a dataservice module, that is responsible for getting and posting remote data, could be placed.</span></span>

### <a name="loggerjs"></a><span data-ttu-id="e621b-208">logger.js</span><span class="sxs-lookup"><span data-stu-id="e621b-208">logger.js</span></span>

<span data-ttu-id="e621b-209">Hot 수건는 services 폴더에 `logger` 모듈을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-209">Hot Towel provides a `logger` module in the services folder.</span></span> <span data-ttu-id="e621b-210">`logger` 모듈은 pop up 알림을에서 콘솔 및 사용자에 게 메시지를 로깅하는 데 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="e621b-210">The `logger` module is ideal for logging messages to the console and to the user in pop up toasts.</span></span>
