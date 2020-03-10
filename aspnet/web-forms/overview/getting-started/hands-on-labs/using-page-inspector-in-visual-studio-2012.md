---
uid: web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
title: Visual Studio 2012에서 페이지 검사기 사용 | Microsoft Docs
author: rick-anderson
description: 이 실습 랩에서는 Visual Studio에서 웹 페이지 문제를 검색 하 고 수정 하는 새 도구인 페이지 검사기를 검색 합니다. 페이지 검사기는 새로운 도구인
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 73232292-a5fe-4720-82a1-8f6553effd1f
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: f42b1be2697ba7d1145b3e334fe8f4ebf019cd12
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78473801"
---
# <a name="using-page-inspector-in-visual-studio-2012"></a><span data-ttu-id="72eb5-104">Visual Studio 2012에서 페이지 검사기 사용</span><span class="sxs-lookup"><span data-stu-id="72eb5-104">Using Page Inspector in Visual Studio 2012</span></span>

<span data-ttu-id="72eb5-105">[웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="72eb5-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="72eb5-106">이 실습 랩에서는 Visual Studio에서 웹 페이지 문제를 검색 하 고 수정 하는 새 도구인 페이지 검사기를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-106">In this Hands-on Lab, you will discover a new tool to find and fix web page issues in Visual Studio - the Page Inspector.</span></span>
> 
> <span data-ttu-id="72eb5-107">페이지 검사기는 브라우저 진단 도구를 Visual Studio에 제공 하 고 브라우저, ASP.NET 및 소스 코드 간에 통합 된 환경을 제공 하는 새로운 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-107">Page Inspector is a new tool that brings browser diagnostics tools to Visual Studio and provides an integrated experience among the browser, ASP.NET, and source code.</span></span> <span data-ttu-id="72eb5-108">Visual Studio IDE 내에서 직접 웹 페이지 (HTML, Web Forms, ASP.NET MVC 또는 웹 페이지)를 렌더링 하 고 소스 코드와 결과 출력을 모두 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-108">It renders a web page (HTML, Web Forms, ASP.NET MVC, or Web Pages) directly within the Visual Studio IDE and lets you examine both the source code and the resulting output.</span></span> <span data-ttu-id="72eb5-109">페이지 검사기를 사용 하면 웹 사이트를 쉽게 분해 하 고, 처음부터 빠르게 페이지를 작성 하 고, 문제를 신속 하 게 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-109">Page Inspector enables you to easily decompose a website, rapidly build pages from the ground up, and quickly diagnose issues.</span></span>
> 
> <span data-ttu-id="72eb5-110">오늘날 ASP.NET MVC 및 WebForms와 같이 적시에 유연 하 고 확장 가능한 웹 사이트를 만드는 다양 한 웹 프레임 워크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-110">Nowadays we have a number of Web frameworks that create flexible and scalable websites in a timely manner, such as ASP.NET MVC and WebForms.</span></span> <span data-ttu-id="72eb5-111">반면에 IDE는 템플릿 기반 페이지와 동적 콘텐츠에서 디자이너 뷰를 지원 하지 않기 때문에 페이지에서 발생 하는 문제를 찾는 것이 더 어려워집니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-111">On the other hand, it gets harder to find issues on the pages because the IDE does not support the designer view in template-based pages and dynamic content.</span></span> <span data-ttu-id="72eb5-112">따라서 이러한 웹 사이트를 브라우저에서 열어 사용자에 게 표시 되는 방식을 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-112">Therefore, these websites have to be opened in a browser to see how they appear to a user.</span></span>
> 
> <span data-ttu-id="72eb5-113">웹 개발자는 외부 도구를 사용 하 여 브라우저에서 정기적으로 실행 되는 문제를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-113">Web developers use external tools to find issues that regularly run in the browser.</span></span> <span data-ttu-id="72eb5-114">그런 다음 IDE로 돌아가서 수정을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-114">Then, they return to the IDE and start fixing.</span></span> <span data-ttu-id="72eb5-115">IDE, 브라우저 및 프로 파일링 도구 사이에서 이와 같은 작업을 수행 하는 것은 비효율적일 수 있으며, 경우에 따라 문제를 재현할 때마다 새로 배포 하 고 캐시를 정리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-115">This back and forth activity among the IDE, the browser and the profiling tools can be inefficient, and sometimes requires a fresh deployment and cache cleaning each time you want to reproduce an issue.</span></span>
> 
> <span data-ttu-id="72eb5-116">페이지 검사기는 결합 된 기능 집합을 사용 하 여 두 분야의 장점을 모두 제공 함으로써 클라이언트 (브라우저 도구)와 서버 (ASP.NET 및 소스 코드) 사이에서 웹 개발의 격차를 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-116">Page Inspector bridges a gap in Web development between the client (browser tools) and the server (ASP.NET and source code) by bringing together the best of both worlds using a combined set of features.</span></span>
> 
> <span data-ttu-id="72eb5-117">페이지 검사기를 사용 하 여 브라우저에서 렌더링 될 HTML 태그를 생성 한 소스 파일 (서버 쪽 코드 포함)의 요소를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-117">Using Page Inspector, you can see which elements in the source files (including server-side code) have produced the HTML markup to be rendered in the browser.</span></span> <span data-ttu-id="72eb5-118">또한 페이지 검사기를 사용 하면 CSS 속성 및 DOM 요소 특성을 수정 하 여 브라우저에 즉시 반영 된 변경 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-118">Page Inspector also lets you modify CSS properties and DOM element attributes to see the changes reflected immediately in the browser.</span></span>
> 
> <span data-ttu-id="72eb5-119">이 실습 랩에서는 페이지 검사기 기능을 안내 하 고 이러한 기능을 사용 하 여 웹 응용 프로그램의 문제를 해결 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-119">This hands-on lab will walk you through the Page Inspector features and show you how you can use them to fix issues in Web applications.</span></span> <span data-ttu-id="72eb5-120">**이 랩에서는 비슷한 흐름을 사용 하지만 다른 기술을 대상으로 하는 두 개의 연습이 포함 되어 있습니다. ASP.NET MVC 개발자 인 경우 연습 1을 따르세요. WebForms 개발자 인 경우 연습 2를 따릅니다**.</span><span class="sxs-lookup"><span data-stu-id="72eb5-120">**This lab contains two exercises using similar flows but targeting different technologies. If you are an ASP.NET MVC Developer, follow exercise one; if you are a WebForms developer follow exercise two**.</span></span>
> 
> <span data-ttu-id="72eb5-121">이 랩에서는 원본 폴더에 제공 된 샘플 웹 응용 프로그램에 사소한 변경 사항을 적용 하 여 앞에서 설명한 향상 된 기능 및 새로운 기능을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-121">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>
> 
> <span data-ttu-id="72eb5-122">모든 샘플 코드와 코드 조각은 [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)에서 사용할 수 있는 웹 캠프 교육 키트에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-122">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="72eb5-123">목표</span><span class="sxs-lookup"><span data-stu-id="72eb5-123">Objectives</span></span>

<span data-ttu-id="72eb5-124">이 실습 랩에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-124">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="72eb5-125">페이지 검사기를 사용 하 여 웹 사이트 분해</span><span class="sxs-lookup"><span data-stu-id="72eb5-125">Decompose a Web Site using Page Inspector</span></span>
- <span data-ttu-id="72eb5-126">페이지 검사기를 사용 하 여 CSS 스타일 변경 검사 및 미리 보기</span><span class="sxs-lookup"><span data-stu-id="72eb5-126">Inspect and preview CSS styles changes with Page Inspector</span></span>
- <span data-ttu-id="72eb5-127">페이지 검사기를 사용 하 여 웹 페이지의 문제 검색 및 해결</span><span class="sxs-lookup"><span data-stu-id="72eb5-127">Detect and fix issues in your web pages using Page Inspector</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="72eb5-128">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="72eb5-128">Prerequisites</span></span>

<span data-ttu-id="72eb5-129">이 랩을 완료 하려면 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-129">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="72eb5-130">[웹 또는 고급의 경우 2012 Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (설치 방법에 대 한 지침은 [부록 a를](#AppendixA) 참조 하세요.)</span><span class="sxs-lookup"><span data-stu-id="72eb5-130">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>
- <span data-ttu-id="72eb5-131">Internet Explorer 9 이상</span><span class="sxs-lookup"><span data-stu-id="72eb5-131">Internet Explorer 9 or higher</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="72eb5-132">실습</span><span class="sxs-lookup"><span data-stu-id="72eb5-132">Exercises</span></span>

<span data-ttu-id="72eb5-133">이 실습 랩에는 다음 연습이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-133">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="72eb5-134">연습 1: ASP.NET MVC 프로젝트에서 페이지 검사기 사용</span><span class="sxs-lookup"><span data-stu-id="72eb5-134">Exercise 1: Using Page Inspector in ASP.NET MVC Projects</span></span>](#Exercise1)
2. [<span data-ttu-id="72eb5-135">연습 2: WebForms 프로젝트에서 페이지 검사기 사용</span><span class="sxs-lookup"><span data-stu-id="72eb5-135">Exercise 2: Using Page Inspector in WebForms Projects</span></span>](#Exercise2)

> [!NOTE]
> <span data-ttu-id="72eb5-136">각 연습은 연습 시작 폴더에 있는 시작 솔루션과 함께 사용 하 여 각 연습을 서로 독립적으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-136">Each exercise is accompanied by a starting solution, located in the Begin folder of the exercise, that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="72eb5-137">연습에 대 한 소스 코드 내에서 해당 연습의 단계를 완료 하 여 생성 된 코드를 포함 하는 Visual Studio 솔루션을 포함 하는 끝 폴더를 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-137">Inside the source code for an exercise, you will also find an End folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="72eb5-138">이 실습 랩을 통해 작업할 때 추가 도움이 필요한 경우 이러한 솔루션을 지침으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-138">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

<span data-ttu-id="72eb5-139">이 랩을 완료 하는 데 소요 되는 예상 시간: **30 분**</span><span class="sxs-lookup"><span data-stu-id="72eb5-139">Estimated time to complete this lab: **30 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Using_Page_Inspector_in_ASPNET_MVC_Projects"></a>
### <a name="exercise-1-using-page-inspector-in-aspnet-mvc-projects"></a><span data-ttu-id="72eb5-140">연습 1: ASP.NET MVC 프로젝트에서 페이지 검사기 사용</span><span class="sxs-lookup"><span data-stu-id="72eb5-140">Exercise 1: Using Page Inspector in ASP.NET MVC Projects</span></span>

<span data-ttu-id="72eb5-141">이 연습에서는 **페이지 검사기**를 사용 하 여 **ASP.NET MVC 4** 솔루션을 미리 보고 디버그 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-141">In this exercise, you will learn how to preview and debug an **ASP.NET MVC 4** solution using **Page Inspector**.</span></span> <span data-ttu-id="72eb5-142">먼저, 웹 디버깅 프로세스를 용이 하 게 하는 기능을 배울 수 있도록 도구를 간략히 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-142">First, you will perform a brief lap around the tool to learn the features that facilitate the Web debugging process.</span></span> <span data-ttu-id="72eb5-143">그런 다음 스타일 문제가 있는 웹 페이지에서 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-143">Then, you will work in a web page that contains styling issues.</span></span> <span data-ttu-id="72eb5-144">페이지 검사기를 사용 하 여 문제를 생성 하는 소스 코드를 찾고 수정 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-144">You will learn how to use Page Inspector to find the source code that generates the issue and fix it.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a><span data-ttu-id="72eb5-145">작업 1-페이지 검사기 탐색</span><span class="sxs-lookup"><span data-stu-id="72eb5-145">Task 1 - Exploring Page Inspector</span></span>

<span data-ttu-id="72eb5-146">이 작업에서는 사진 갤러리를 표시 하는 ASP.NET MVC 4 프로젝트의 컨텍스트에서 페이지 검사기를 사용 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-146">In this task, you will learn how to use the Page Inspector in the context of an ASP.NET MVC 4 project that shows a photo gallery.</span></span>

1. <span data-ttu-id="72eb5-147">**Source/Ex1-MVC4/begin/** 폴더에 있는 **시작** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-147">Open the **Begin** solution located at **Source/Ex1-MVC4/Begin/** folder.</span></span>

   1. <span data-ttu-id="72eb5-148">계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-148">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="72eb5-149">이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-149">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="72eb5-150">**NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-150">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="72eb5-151">마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-151">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="72eb5-152">NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-152">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="72eb5-153">NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-153">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="72eb5-154">이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-154">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="72eb5-155">솔루션 탐색기 **/Views/Home** 프로젝트 폴더 아래에서 **Index. cshtml** 뷰를 찾아 마우스 오른쪽 단추로 클릭 한 다음 **페이지 검사기에서 보기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-155">In the Solution Explorer, locate **Index.cshtml** view under the **/Views/Home** project folder, right-click it and select **View in Page Inspector**.</span></span>

    <span data-ttu-id="72eb5-156">![페이지 검사기 미리 볼 파일 선택](using-page-inspector-in-visual-studio-2012/_static/image1.png "페이지 검사기 미리 볼 파일 선택")</span><span class="sxs-lookup"><span data-stu-id="72eb5-156">![Selecting a file to preview in Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image1.png "Selecting a file to preview in Page Inspector")</span></span>

    <span data-ttu-id="72eb5-157">*페이지 검사기 미리 볼 파일 선택*</span><span class="sxs-lookup"><span data-stu-id="72eb5-157">*Selecting a file to preview in Page Inspector*</span></span>
3. <span data-ttu-id="72eb5-158">페이지 검사기 창에는 선택한 원본 뷰에 매핑된 */Home/Index* URL이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-158">The Page Inspector window will show the */Home/Index* URL mapped to the source View you selected.</span></span>

    ![PageInspector의 첫 번째 연락처](using-page-inspector-in-visual-studio-2012/_static/image2.png)

    <span data-ttu-id="72eb5-160">*페이지 검사기에 대 한 첫 번째 연락처*</span><span class="sxs-lookup"><span data-stu-id="72eb5-160">*The first contact with Page Inspector*</span></span>

    <span data-ttu-id="72eb5-161">페이지 검사기 도구는 Visual Studio 환경에 통합 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-161">The Page Inspector tool is integrated in your Visual Studio environment.</span></span> <span data-ttu-id="72eb5-162">검사기에는 강력한 HTML 프로파일러와 함께 포함 된 브라우저가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-162">The inspector contains an embedded browser, together with a powerful HTML profiler.</span></span> <span data-ttu-id="72eb5-163">페이지의 모양을 확인 하기 위해 솔루션을 실행할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-163">Notice that you do not have to run the solution to see how your pages look.</span></span>

    > [!NOTE]
    > <span data-ttu-id="72eb5-164">페이지 검사기 브라우저의 너비가 열린 페이지의 너비 보다 적으면 페이지가 제대로 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-164">When the width of Page Inspector browser is less than the width of the opened page, you will not see the page properly.</span></span> <span data-ttu-id="72eb5-165">이 경우 페이지 검사기의 너비를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-165">If that happens, adjust the width of the Page Inspector.</span></span>
4. <span data-ttu-id="72eb5-166">페이지 검사기에서 **파일** 탭을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-166">Click the **Files** tab in Page Inspector.</span></span>

    <span data-ttu-id="72eb5-167">인덱스 페이지를 작성 하는 모든 원본 파일이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-167">You will see all the source files that are composing the Index page.</span></span> <span data-ttu-id="72eb5-168">이 기능을 사용 하면 특히 부분 뷰 및 템플릿으로 작업 하는 경우 모든 요소를 한눈에 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-168">This feature helps to identify all the elements at a glance, especially when you are working with partial views and templates.</span></span> <span data-ttu-id="72eb5-169">링크를 클릭 하면 각 파일을 열 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-169">Notice that you can also open each of the files if you click the links.</span></span>

    ![-파일-탭](using-page-inspector-in-visual-studio-2012/_static/image3.png)

    <span data-ttu-id="72eb5-171">*파일 탭*</span><span class="sxs-lookup"><span data-stu-id="72eb5-171">*The Files tab*</span></span>
5. <span data-ttu-id="72eb5-172">탭의 왼쪽에 있는 **토글 검사 모드** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-172">Click the **Toggle Inspection Mode** button, located at the left of the tabs.</span></span>

    <span data-ttu-id="72eb5-173">이 도구를 사용 하 여 페이지의 요소를 선택 하 고 HTML 및 Razor 코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-173">This tool will let you select any element of the page and see its HTML and Razor code.</span></span>

    ![전환-검사 모드-단추](using-page-inspector-in-visual-studio-2012/_static/image4.png)

    <span data-ttu-id="72eb5-175">*검사 모드 토글 단추*</span><span class="sxs-lookup"><span data-stu-id="72eb5-175">*Toggle Inspection Mode button*</span></span>
6. <span data-ttu-id="72eb5-176">페이지 검사기 브라우저에서 마우스 포인터를 페이지 요소 위로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-176">In the Page Inspector browser, move the mouse pointer over the page elements.</span></span> <span data-ttu-id="72eb5-177">마우스 포인터를 렌더링 된 페이지의 특정 부분으로 이동 하는 동안 요소 형식이 표시 되 고 Visual Studio 편집기에서 해당 소스 태그나 코드가 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-177">While you move the mouse pointer over any part of the rendered page, the element type is displayed and the corresponding source markup or code is highlighted in the Visual Studio editor.</span></span>

    ![검사 모드 실행](using-page-inspector-in-visual-studio-2012/_static/image5.png)

    <span data-ttu-id="72eb5-179">*검사 모드 실행*</span><span class="sxs-lookup"><span data-stu-id="72eb5-179">*Inspection mode in action*</span></span>

    > [!NOTE]
    > <span data-ttu-id="72eb5-180">페이지 검사기 창을 최대화 하지 마십시오. 그렇지 않으면 소스 코드를 표시 하는 미리 보기 탭을 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-180">Do not maximize the Page Inspector window or you will not be able to see the preview tab showing the source code.</span></span> <span data-ttu-id="72eb5-181">최대화 된 페이지 검사기의 요소를 클릭 하면 선택의 소스 코드가 표시 되지만 페이지 검사기 창이 숨겨집니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-181">If you click the element in Page Inspector when it is maximized, the source code of the selection will appear but it will hide the Page Inspector window.</span></span>

    <span data-ttu-id="72eb5-182">**인덱스 cshtml** 파일에 주의를 기울여야 하는 경우 선택한 요소를 생성 하는 소스 코드의 일부가 강조 표시 된 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-182">If you pay attention to the **Index.cshtml** file, you will notice that the portion of source code that generates the selected element is highlighted.</span></span> <span data-ttu-id="72eb5-183">이 기능을 사용 하면 긴 소스 파일을 쉽게 편집할 수 있으므로 코드에 직접 액세스 하는 방법과 빠른 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-183">This feature facilitates the editing of long source files, providing a direct and fast way to access the code.</span></span>

    ![요소 검사](using-page-inspector-in-visual-studio-2012/_static/image6.png)

    <span data-ttu-id="72eb5-185">*요소 검사*</span><span class="sxs-lookup"><span data-stu-id="72eb5-185">*Inspecting elements*</span></span>
7. <span data-ttu-id="72eb5-186">**검사 모드 설정/해제** 단추를 클릭 합니다 (![Html 탭을 선택 하 여 페이지 검사기 브라우저에 렌더링 된 html 코드를 표시 합니다.](using-page-inspector-in-visual-studio-2012/_static/image7.png "HTML 탭을 선택 하 여 페이지 검사기 브라우저에서 렌더링 된 HTML 코드를 표시 합니다.")</span><span class="sxs-lookup"><span data-stu-id="72eb5-186">Click the **Toggle Inspection Mode** button (![Select the HTML tab to display the HTML code rendered in the Page Inspector browser.](using-page-inspector-in-visual-studio-2012/_static/image7.png "Select the HTML tab to display the HTML code rendered in the Page Inspector browser.")</span></span> <span data-ttu-id="72eb5-187">)를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-187">) to disable the cursor.</span></span>
8. <span data-ttu-id="72eb5-188">**Html** 탭을 선택 하 여 페이지 검사기 브라우저에서 렌더링 된 html 코드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-188">Select the **HTML** tab to display the HTML code rendered in the Page Inspector browser.</span></span>
9. <span data-ttu-id="72eb5-189">HTML 태그에서 Koala 링크를 사용 하 여 목록 항목을 찾아 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-189">In the HTML markup, locate the list item with the Koala link and select it.</span></span>

    <span data-ttu-id="72eb5-190">코드를 선택 하면 브라우저에서 해당 출력이 자동으로 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-190">Notice that when you select the code, the corresponding output is automatically highlighted in the browser.</span></span> <span data-ttu-id="72eb5-191">이 기능은 HTML 블록이 페이지에서 렌더링 되는 방법을 확인 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-191">This feature is useful to see how an HTML block is rendered on the page.</span></span>

    <span data-ttu-id="72eb5-192">![페이지에서 HTML 요소 선택](using-page-inspector-in-visual-studio-2012/_static/image8.png "페이지에서 HTML 요소 선택")</span><span class="sxs-lookup"><span data-stu-id="72eb5-192">![Selecting HTML element in the page](using-page-inspector-in-visual-studio-2012/_static/image8.png "Selecting HTML element in the page")</span></span>

    <span data-ttu-id="72eb5-193">*페이지에서 HTML 요소 선택*</span><span class="sxs-lookup"><span data-stu-id="72eb5-193">*Selecting HTML element in the page*</span></span>
10. <span data-ttu-id="72eb5-194">검사 모드 설정 **/해제** 단추를 클릭 하 여 *검사 모드* 를 사용 하도록 설정 하 고 탐색 모음을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-194">Click the **Toggle Inspection Mode** button to enable *Inspection Mode* and click the navigation bar.</span></span> <span data-ttu-id="72eb5-195">HTML 코드의 오른쪽에 있는 스타일 창에 선택한 요소에 CSS 스타일이 적용 된 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-195">On the right of the HTML code, in the Styles pane, you will see a list with the CSS styles applied to the selected element.</span></span>

    > [!NOTE]
    > <span data-ttu-id="72eb5-196">헤더가 사이트 레이아웃의 일부 이기 때문에 페이지 검사기 \_Layout 파일이 열리고 영향을 받는 코드의 세그먼트가 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-196">Since the header is a part of the site layout, Page Inspector will also open \_Layout.cshtml file and highlight the segment of code affected.</span></span>

    ![스타일 검색](using-page-inspector-in-visual-studio-2012/_static/image9.png)

    <span data-ttu-id="72eb5-198">*선택한 요소의 스타일 및 소스 파일 검색*</span><span class="sxs-lookup"><span data-stu-id="72eb5-198">*Discovering styles and source files of a selected element*</span></span>
11. <span data-ttu-id="72eb5-199">검사 설정/해제 포인터가 활성화 된 상태에서 마우스 포인터를 파란색 추천 막대 아래로 이동 하 고 절반 원을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-199">With the toggle inspection pointer enabled, move the mouse pointer below the blue featured bar and click the half circle.</span></span>

    <span data-ttu-id="72eb5-200">![요소 선택](using-page-inspector-in-visual-studio-2012/_static/image10.png "요소 선택")</span><span class="sxs-lookup"><span data-stu-id="72eb5-200">![Selecting an element](using-page-inspector-in-visual-studio-2012/_static/image10.png "Selecting an element")</span></span>

    <span data-ttu-id="72eb5-201">*요소 선택*</span><span class="sxs-lookup"><span data-stu-id="72eb5-201">*Selecting an element*</span></span>
12. <span data-ttu-id="72eb5-202">스타일 창의 **. 주-콘텐츠** 그룹에서 **배경 이미지** 항목을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-202">In the Styles pane, locate the **background-image** item under the **.main-content** group.</span></span> <span data-ttu-id="72eb5-203">**배경 이미지** 를 **선택 취소** 하 고 어떻게 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-203">**Uncheck** the **background-image** and see what happens.</span></span> <span data-ttu-id="72eb5-204">그러면 브라우저에 변경 내용이 즉시 반영 되 고 원이 숨겨집니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-204">You will notice that the browser will reflect the changes immediately and the circle is hidden.</span></span>

    > [!NOTE]
    > <span data-ttu-id="72eb5-205">페이지 검사기 스타일 탭에서 적용 하는 변경 내용은 원래 스타일 시트에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-205">The changes you apply on the Page Inspector Styles tab do not affect the original stylesheet.</span></span> <span data-ttu-id="72eb5-206">스타일을 선택 취소 하거나 값을 원하는 횟수 만큼 변경할 수 있지만 페이지를 새로 고치면 복원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-206">You can uncheck styles or change their values as many times as you want, but they will be restored after refreshing the page.</span></span>

    <span data-ttu-id="72eb5-207">![CSS 스타일 사용 및 사용 안 함](using-page-inspector-in-visual-studio-2012/_static/image11.png "CSS 스타일 사용 및 사용 안 함")</span><span class="sxs-lookup"><span data-stu-id="72eb5-207">![Enabling and disabling CSS styles](using-page-inspector-in-visual-studio-2012/_static/image11.png "Enabling and disabling CSS styles")</span></span>

    <span data-ttu-id="72eb5-208">*CSS 스타일 사용 및 사용 안 함*</span><span class="sxs-lookup"><span data-stu-id="72eb5-208">*Enabling and disabling CSS styles*</span></span>
13. <span data-ttu-id="72eb5-209">이제 검사 모드를 사용 하 여 헤더의 '**여기에서 로고**' 텍스트를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-209">Now, click the '**your logo here**' text on the header using the inspection mode.</span></span>
14. <span data-ttu-id="72eb5-210">**스타일** 탭의 **. 사이트 제목** 그룹에서 **font-size** CSS 특성을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-210">In the **Styles** tab, locate the **font-size** CSS attribute under the **.site-title** group.</span></span> <span data-ttu-id="72eb5-211">특성 값을 두 번 클릭 하 고 2.3 em 값을 **3 em**으로 바꾼 다음 **enter**키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-211">Double-click the attribute value and replace the 2.3 em value with **3 em**, and then press **ENTER**.</span></span> <span data-ttu-id="72eb5-212">제목이 클수록 보입니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-212">Notice that the title looks bigger.</span></span>

    <span data-ttu-id="72eb5-213">![페이지 검사기에서 CSS 값 변경](using-page-inspector-in-visual-studio-2012/_static/image12.png "페이지 검사기에서 CSS 값 변경")</span><span class="sxs-lookup"><span data-stu-id="72eb5-213">![Changing CSS values in the Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image12.png "Changing CSS values in the Page Inspector")</span></span>

    <span data-ttu-id="72eb5-214">*페이지 검사기에서 CSS 값 변경*</span><span class="sxs-lookup"><span data-stu-id="72eb5-214">*Changing CSS values in the Page Inspector*</span></span>
15. <span data-ttu-id="72eb5-215">페이지 검사기의 오른쪽 창에 있는 **추적 스타일** 탭을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-215">Click the **Trace Styles** tab, located in the right pane of Page Inspector.</span></span> <span data-ttu-id="72eb5-216">이 방법은 선택 항목에 적용 된 모든 스타일을 특성 이름별로 정렬 하 여 표시 하는 대체 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-216">This is an alternative way to see all the styles applied to the selection, ordered by attribute name.</span></span>

    ![CSS 스타일 추적](using-page-inspector-in-visual-studio-2012/_static/image13.png)

    <span data-ttu-id="72eb5-218">*선택한 요소의 CSS 스타일 추적*</span><span class="sxs-lookup"><span data-stu-id="72eb5-218">*CSS styles tracing of the selected element*</span></span>
16. <span data-ttu-id="72eb5-219">페이지 검사기의 또 다른 기능은 레이아웃 창입니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-219">Another feature of Page Inspector is the Layout pane.</span></span> <span data-ttu-id="72eb5-220">검사 모드를 사용 하 여 탐색 모음을 선택 하 고 오른쪽 창에서 **레이아웃** 탭을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-220">Using the inspection mode, select the navigation bar and then click the **Layout** tab on the right pane.</span></span> <span data-ttu-id="72eb5-221">선택한 요소의 정확한 크기와 해당 오프셋, 여백, 안쪽 여백 및 테두리 크기가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-221">You will see the exact size of the selected element, as well as its offset, margin, padding and border size.</span></span> <span data-ttu-id="72eb5-222">이 보기에서 값을 수정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-222">Notice that you can also modify the values from this view.</span></span>

    <span data-ttu-id="72eb5-223">![페이지 검사기의 요소 레이아웃](using-page-inspector-in-visual-studio-2012/_static/image14.png "페이지 검사기의 요소 레이아웃")</span><span class="sxs-lookup"><span data-stu-id="72eb5-223">![Element layout in Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image14.png "Element layout in Page Inspector")</span></span>

    <span data-ttu-id="72eb5-224">*페이지 검사기의 요소 레이아웃*</span><span class="sxs-lookup"><span data-stu-id="72eb5-224">*Element layout in Page Inspector*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a><span data-ttu-id="72eb5-225">작업 2-사진 갤러리에서 스타일 문제 찾기 및 수정</span><span class="sxs-lookup"><span data-stu-id="72eb5-225">Task 2 - Finding and Fixing Style Issues in the Photo Gallery</span></span>

<span data-ttu-id="72eb5-226">이전 버전의 Visual Studio에서 웹 페이지 문제를 진단 하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="72eb5-226">How would you diagnose Web pages issues with previous versions of Visual Studio?</span></span> <span data-ttu-id="72eb5-227">Internet Explorer 개발자 도구 또는 Firebug와 같이 Visual Studio IDE 외부에서 실행 되는 웹 디버깅 도구에 대해 잘 알고 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-227">You are likely familiar with web debugging tools that run outside the Visual Studio IDE, like Internet Explorer Developer Tools or Firebug.</span></span> <span data-ttu-id="72eb5-228">브라우저는 HTML, 스크립팅 및 스타일만 이해 하는 반면 기본 프레임 워크는 렌더링 될 HTML을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-228">Browsers only understand HTML, scripting and styles, while an underlying framework generates the HTML that will be rendered.</span></span> <span data-ttu-id="72eb5-229">따라서 웹 페이지의 모양을 확인 하려면 전체 사이트를 배포 해야 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-229">For that reason, you often need to deploy the whole site to see how web pages look like.</span></span>

<span data-ttu-id="72eb5-230">웹 사이트에서 문제를 검색 하 고 수정 하려는 경우 다음 단계를 수행 했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-230">You had probably followed these steps when you wanted to detect and fix an issue in your web site:</span></span>

1. <span data-ttu-id="72eb5-231">Visual Studio에서 솔루션을 실행 하거나 웹 서버에 페이지를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-231">Run the Solution from Visual Studio, or deploy the page on the web server.</span></span>
2. <span data-ttu-id="72eb5-232">브라우저에서 사용 하는 개발자 도구를 열거나 소스 코드와 스타일을 열고 문제를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-232">In the browser, open the developer tools you use, or simply open the source code and the styles and try to match the issue.</span></span> <span data-ttu-id="72eb5-233">관련 파일을 찾으려면 스타일 클래스의 이름을 사용 하 여 &quot;검색&quot; 또는 파일에서 검색&quot; 기능을 &quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-233">To find the files involved, you would have used the &quot;Search&quot; or &quot;Search in files&quot; features with the name of the style classes.</span></span>
3. <span data-ttu-id="72eb5-234">오류가 검색 되 면 웹 브라우저 및 서버를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-234">Once the error is detected, stop the Web browser and the server.</span></span>
4. <span data-ttu-id="72eb5-235">브라우저 캐시를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-235">Clear the browser cache.</span></span>
5. <span data-ttu-id="72eb5-236">수정 사항을 적용 하려면 Visual Studio로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-236">Return to Visual Studio to apply a fix.</span></span> <span data-ttu-id="72eb5-237">테스트 하는 모든 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-237">Repeat all the steps to test.</span></span>

<span data-ttu-id="72eb5-238">ASP.NET MVC 4에는 실제 WYSIWYG가 없으므로 이후 단계에서 웹 응용 프로그램을 실행 하거나 배포한 후에 대부분의 스타일 문제가 감지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-238">As there is no real WYSIWYG in ASP.NET MVC 4, most of the style issues are detected on a later stage, after running or deploying the web application.</span></span> <span data-ttu-id="72eb5-239">이제 페이지 검사기를 사용 하 여 솔루션을 실행 하지 않고 모든 페이지를 미리 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-239">Now, with Page Inspector, it is possible to preview any page without running the solution.</span></span>

<span data-ttu-id="72eb5-240">이 작업에서는 페이지 검사기를 사용 하 여 사진 갤러리 응용 프로그램의 일부 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-240">In this task, you will use the Page inspector and fix some issues the Photo Gallery application.</span></span>

1. <span data-ttu-id="72eb5-241">페이지 검사기를 사용 하 여 헤더의 왼쪽에 있는 **레지스터** 와 **로그인** 링크를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-241">Using Page Inspector, locate the **Register** and the **Log in** links at the left side of the header.</span></span>

    <span data-ttu-id="72eb5-242">링크는 오른쪽의 예상 위치에 표시 되지 않으며 글머리 기호 목록과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-242">Notice that the links are not displayed at the expected place on the right, and they are shown like a bulleted list.</span></span> <span data-ttu-id="72eb5-243">이제 링크를 오른쪽에 맞추고 그에 따라 스타일을 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-243">You will now align the links to the right and restyle them accordingly.</span></span>

    <span data-ttu-id="72eb5-244">![등록 및 로그인 링크 찾기](using-page-inspector-in-visual-studio-2012/_static/image15.png "등록 및 로그인 링크 찾기")</span><span class="sxs-lookup"><span data-stu-id="72eb5-244">![Locating the Register and Log in links](using-page-inspector-in-visual-studio-2012/_static/image15.png "Locating the Register and Log in links")</span></span>

    <span data-ttu-id="72eb5-245">*등록 및 로그인 링크 찾기*</span><span class="sxs-lookup"><span data-stu-id="72eb5-245">*Locating the Register and Log in links*</span></span>
2. <span data-ttu-id="72eb5-246">토글 검사 모드 선택 된 상태에서 등록 링크를 클릭 하 여 해당 코드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-246">With Toggle Inspection Mode selected, click close to, but not on, the Register link to open its code.</span></span>

    <span data-ttu-id="72eb5-247">링크의 소스 코드는 **loginpartial.cshtml 파일\_** 에 있으며, 첫 번째 위치에서 찾을 수 있는 위치에 해당 하는 및 \_레이아웃이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-247">Notice that the source code of the links is located in the **\_LoginPartial.cshtml** file, not the Index.cshtml nor the \_Layout.cshtml, which are the places you might look in first place.</span></span> <span data-ttu-id="72eb5-248">올바른 소스 파일에 직접 배치 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-248">You have been placed directly in the correct source file.</span></span>
3. <span data-ttu-id="72eb5-249">**스타일** 탭에서 이러한 링크의 HTML 컨테이너인 **\<섹션 > #login** 항목을 찾아 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-249">In the **Styles** tab, locate and click the **\<section> #login** item, which is the HTML container for these links.</span></span>

    <span data-ttu-id="72eb5-250">**#Login** 스타일은를 클릭 한 후에 자동으로 **사이트 .css** 에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-250">Notice that the **#login** style is automatically located in **Site.css** after you click.</span></span> <span data-ttu-id="72eb5-251">코드도 이제 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-251">Moreover, the code is now highlighted.</span></span>

    <span data-ttu-id="72eb5-252">![CSS 스타일 선택](using-page-inspector-in-visual-studio-2012/_static/image16.png "CSS 스타일 선택")</span><span class="sxs-lookup"><span data-stu-id="72eb5-252">![Selecting the CSS styles](using-page-inspector-in-visual-studio-2012/_static/image16.png "Selecting the CSS styles")</span></span>

    <span data-ttu-id="72eb5-253">*CSS 스타일 선택*</span><span class="sxs-lookup"><span data-stu-id="72eb5-253">*Selecting the CSS styles*</span></span>
4. <span data-ttu-id="72eb5-254">열기 및 닫기 문자를 제거 하 여 강조 표시 된 코드에서 **텍스트 맞춤** 특성의 주석 처리를 제거 하 고 **사이트 .css** 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-254">Uncomment the **text-align** attribute in the highlighted code by removing the opening and closing characters and save the **Site.css** file.</span></span>

    <span data-ttu-id="72eb5-255">페이지 검사기는 현재 페이지를 구성 하는 다른 모든 파일을 인식 하 고 이러한 파일이 변경 되 면이를 감지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-255">Page Inspector is aware of all the different files that compose the current page, and it can detect when any of these files change.</span></span> <span data-ttu-id="72eb5-256">브라우저의 현재 페이지가 원본 파일과 동기화 되지 않을 때마다 경고를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-256">It alerts you whenever the current page in browser is not in sync with the source files.</span></span>
5. <span data-ttu-id="72eb5-257">페이지 검사기 브라우저에서 주소 표시줄 아래에 있는 막대를 클릭 하 여 페이지를 다시 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-257">In the Page Inspector browser, click the bar located below the address bar to reload the page.</span></span>

    ![페이지 다시 로드](using-page-inspector-in-visual-studio-2012/_static/image17.png)

    <span data-ttu-id="72eb5-259">*페이지 다시 로드*</span><span class="sxs-lookup"><span data-stu-id="72eb5-259">*Reloading the page*</span></span>

    <span data-ttu-id="72eb5-260">링크는 이제 오른쪽에 있지만 여전히 글머리 기호 목록과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-260">The links are now at the right, but they still look like a bulleted list.</span></span> <span data-ttu-id="72eb5-261">이제 글머리 기호를 제거 하 고 링크를 가로로 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-261">Now, you will remove the bullets and align the links horizontally.</span></span>

    ![업데이트 된 페이지](using-page-inspector-in-visual-studio-2012/_static/image18.png)

    <span data-ttu-id="72eb5-263">*업데이트 된 페이지*</span><span class="sxs-lookup"><span data-stu-id="72eb5-263">*Updated page*</span></span>
6. <span data-ttu-id="72eb5-264">검사 모드를 사용 하 여 &quot;등록&quot;를 포함 하는 **&lt;li&gt;** 항목을 선택 하 고 &quot;링크를&quot; 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-264">Using the inspection mode, select any of the **&lt;li&gt;** items that contain the &quot;Register&quot; and &quot;Log in&quot; links.</span></span> <span data-ttu-id="72eb5-265">그런 다음 **&lt;섹션&gt; #login** 항목을 클릭 하 여 **스타일 css** 코드에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-265">Then, click the **&lt;section&gt; #login** item to access **Styles.css** code.</span></span>

    <span data-ttu-id="72eb5-266">![스타일 찾기](using-page-inspector-in-visual-studio-2012/_static/image19.png "스타일 찾기")</span><span class="sxs-lookup"><span data-stu-id="72eb5-266">![Finding the style](using-page-inspector-in-visual-studio-2012/_static/image19.png "Finding the style")</span></span>

    <span data-ttu-id="72eb5-267">*스타일 찾기*</span><span class="sxs-lookup"><span data-stu-id="72eb5-267">*Finding the style*</span></span>
7. <span data-ttu-id="72eb5-268">**스타일 .css**에서 **#login li** 항목에 대 한 코드의 주석 처리를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-268">In **Style.css**, uncomment the code for **#login li** items.</span></span> <span data-ttu-id="72eb5-269">추가 하는 스타일은 글머리 기호를 숨기고 항목이 가로로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-269">The style you are adding will hide the bullet and display the items horizontally.</span></span>

    <span data-ttu-id="72eb5-270">![로그인 링크의 스타일 다시 지정](using-page-inspector-in-visual-studio-2012/_static/image20.png "로그인 링크의 스타일 다시 지정")</span><span class="sxs-lookup"><span data-stu-id="72eb5-270">![Restyling the login links](using-page-inspector-in-visual-studio-2012/_static/image20.png "Restyling the login links")</span></span>

    <span data-ttu-id="72eb5-271">*로그인 링크의 스타일 다시 지정*</span><span class="sxs-lookup"><span data-stu-id="72eb5-271">*Restyling the login links*</span></span>
8. <span data-ttu-id="72eb5-272">**스타일 .css** 파일을 저장 하 고 주소 아래에 있는 막대에서 한 번을 클릭 하 여 페이지를 다시 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-272">Save **Style.css** file and click once on the bar located below the address to reload the page.</span></span> <span data-ttu-id="72eb5-273">링크가 올바르게 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-273">Notice that the links appear correctly.</span></span>

    <span data-ttu-id="72eb5-274">![오른쪽에 정렬 된 링크](using-page-inspector-in-visual-studio-2012/_static/image21.png "오른쪽에 정렬 된 링크")</span><span class="sxs-lookup"><span data-stu-id="72eb5-274">![Links aligned to the right side](using-page-inspector-in-visual-studio-2012/_static/image21.png "Links aligned to the right side")</span></span>

    <span data-ttu-id="72eb5-275">*오른쪽에 정렬 된 링크*</span><span class="sxs-lookup"><span data-stu-id="72eb5-275">*Links aligned to the right side*</span></span>
9. <span data-ttu-id="72eb5-276">마지막으로 헤더 제목을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-276">Finally, you will change the header title.</span></span> <span data-ttu-id="72eb5-277">검사 모드를 사용 하 여 **여기에서 로고** 를 클릭 하 고 해당 텍스트를 생성 하는 소스 코드를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-277">Use the inspection mode to click **your logo here** text and get to the source code that generates it.</span></span>
10. <span data-ttu-id="72eb5-278">이제 **\_레이아웃**을 사용 하 고 있습니다. cshtml에서 '**로고를 여기**로 ' 텍스트를 '**사진 갤러리**'로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-278">Now you are in **\_Layout.cshtml**, replace '**your logo here**' text with '**Photo Gallery**'.</span></span> <span data-ttu-id="72eb5-279">페이지 검사기 브라우저를 저장 하 고 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-279">Save and update the Page Inspector browser.</span></span>

    <span data-ttu-id="72eb5-280">![새 제목 할당](using-page-inspector-in-visual-studio-2012/_static/image22.png "새 제목 할당")</span><span class="sxs-lookup"><span data-stu-id="72eb5-280">![Assigning a new title](using-page-inspector-in-visual-studio-2012/_static/image22.png "Assigning a new title")</span></span>

    <span data-ttu-id="72eb5-281">*새 제목 할당*</span><span class="sxs-lookup"><span data-stu-id="72eb5-281">*Assigning a new title*</span></span>

    ![사진 갤러리 페이지](using-page-inspector-in-visual-studio-2012/_static/image23.png)

    <span data-ttu-id="72eb5-283">*사진 갤러리 페이지가 업데이트 됨*</span><span class="sxs-lookup"><span data-stu-id="72eb5-283">*Photo Gallery page updated*</span></span>
11. <span data-ttu-id="72eb5-284">마지막으로, **사진 갤러리** 프로젝트를 선택 하 고 **f5** 키를 눌러 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-284">Finally, select the **PhotoGallery** project and press **F5** to run the app.</span></span> <span data-ttu-id="72eb5-285">모든 변경 내용이 예상 대로 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-285">Check out all the changes work as expected.</span></span>

---

<a id="Exercise2"></a>

<a id="Exercise_2_Using_Page_Inspector_in_WebForms_Projects"></a>
### <a name="exercise-2-using-page-inspector-in-webforms-projects"></a><span data-ttu-id="72eb5-286">연습 2: WebForms 프로젝트에서 페이지 검사기 사용</span><span class="sxs-lookup"><span data-stu-id="72eb5-286">Exercise 2: Using Page Inspector in WebForms Projects</span></span>

<span data-ttu-id="72eb5-287">이 연습에서는 페이지 검사기를 사용 하 여 WebForms 솔루션을 미리 보고 디버그 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-287">In this exercise, you will learn how to preview and debug a WebForms solution using Page Inspector.</span></span> <span data-ttu-id="72eb5-288">웹 디버깅 프로세스를 용이 하 게 하는 페이지 검사기 기능에 대 한 자세한 내용은 도구에 대 한 간략 한 랩을 먼저 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-288">You will first perform a brief lap around the tool to learn the Page Inspector features that facilitate the Web debugging process.</span></span> <span data-ttu-id="72eb5-289">그런 다음 스타일 문제가 있는 웹 페이지에서 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-289">Then, you will work in a web page that contains styling issues.</span></span> <span data-ttu-id="72eb5-290">페이지 검사기를 사용 하 여 문제를 생성 하는 소스 코드를 찾고 수정 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-290">You will learn how to use Page Inspector to find the source code that generates the issue and fix it.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a><span data-ttu-id="72eb5-291">작업 1-페이지 검사기 탐색</span><span class="sxs-lookup"><span data-stu-id="72eb5-291">Task 1 - Exploring Page Inspector</span></span>

<span data-ttu-id="72eb5-292">이 작업에서는 사진 갤러리를 표시 하는 WebForms 프로젝트의 컨텍스트에서 페이지 검사기 기능을 사용 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-292">In this task, you will learn how to use the Page Inspector features in the context of a WebForms project that shows a photo gallery.</span></span>

1. <span data-ttu-id="72eb5-293">**Source/Ex2-WebForms/begin/** 폴더에 있는 **시작** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-293">Open the **Begin** solution located at **Source/Ex2-WebForms/Begin/** folder.</span></span>

   1. <span data-ttu-id="72eb5-294">계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-294">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="72eb5-295">이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-295">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="72eb5-296">**NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-296">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="72eb5-297">마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-297">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="72eb5-298">NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-298">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="72eb5-299">NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-299">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="72eb5-300">이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-300">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="72eb5-301">솔루션 탐색기 **default.aspx 페이지를** 찾아 마우스 오른쪽 단추로 클릭 하 고 **페이지 검사기에서 보기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-301">In the Solution Explorer, locate **Default.aspx** page, right-click it and select **View in Page Inspector**.</span></span>

    <span data-ttu-id="72eb5-302">![페이지 검사기를 사용 하 여 default.aspx 열기](using-page-inspector-in-visual-studio-2012/_static/image24.png "페이지 검사기를 사용 하 여 default.aspx 열기")</span><span class="sxs-lookup"><span data-stu-id="72eb5-302">![Opening Default.aspx with Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image24.png "Opening Default.aspx with Page Inspector")</span></span>

    <span data-ttu-id="72eb5-303">*페이지 검사기를 사용 하 여 default.aspx 열기*</span><span class="sxs-lookup"><span data-stu-id="72eb5-303">*Opening Default.aspx with Page Inspector*</span></span>
3. <span data-ttu-id="72eb5-304">페이지 검사기 창은 Default.aspx를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-304">The Page Inspector window will show Default.aspx.</span></span>

    <span data-ttu-id="72eb5-305">![페이지 검사기에서 default.aspx 보기](using-page-inspector-in-visual-studio-2012/_static/image25.png "페이지 검사기에서 default.aspx 보기")</span><span class="sxs-lookup"><span data-stu-id="72eb5-305">![Viewing Default.aspx in Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image25.png "Viewing Default.aspx in Page Inspector")</span></span>

    <span data-ttu-id="72eb5-306">*페이지 검사기에서 default.aspx 보기*</span><span class="sxs-lookup"><span data-stu-id="72eb5-306">*Viewing Default.aspx in Page Inspector*</span></span>

    <span data-ttu-id="72eb5-307">페이지 검사기 도구는 Visual Studio 환경에 통합 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-307">The Page Inspector tool is integrated in your Visual Studio environment.</span></span> <span data-ttu-id="72eb5-308">검사기에는 선택한 코드를 표시 하는 강력한 HTML 프로파일러와 함께 포함 된 브라우저가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-308">The inspector contains an embedded browser, together with a powerful HTML profiler that will show the selected code.</span></span> <span data-ttu-id="72eb5-309">페이지의 모양을 확인 하기 위해 솔루션을 실행할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-309">Notice that you do not have to run the solution to see how your pages look.</span></span>

    > [!NOTE]
    > <span data-ttu-id="72eb5-310">페이지 검사기 브라우저의 너비가 열린 페이지의 너비 보다 적으면 페이지가 제대로 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-310">When the width of Page Inspector browser is less than the width of the opened page, you will not see the page properly.</span></span> <span data-ttu-id="72eb5-311">이 경우 페이지 검사기의 너비를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-311">If that happens, adjust the width of the Page Inspector.</span></span>
4. <span data-ttu-id="72eb5-312">페이지 검사기에서 **파일** 탭을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-312">Click the **Files** tab in Page Inspector.</span></span>

    <span data-ttu-id="72eb5-313">렌더링 된 기본 페이지를 작성 하는 모든 원본 파일이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-313">You will see all the source files that are composing the rendered Default page.</span></span> <span data-ttu-id="72eb5-314">이 기능은 특히 사용자 컨트롤 및 마스터 페이지를 사용 하 여 작업 하는 경우 모든 요소를 한눈에 식별 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-314">This is a useful feature to identify all the elements at a glance, especially when you are working with User Controls and Master Pages.</span></span> <span data-ttu-id="72eb5-315">각 파일을 탐색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-315">Notice that you can also navigate to each of the files.</span></span>

    <span data-ttu-id="72eb5-316">![파일 탭](using-page-inspector-in-visual-studio-2012/_static/image26.png "파일 탭")</span><span class="sxs-lookup"><span data-stu-id="72eb5-316">![The Files tab](using-page-inspector-in-visual-studio-2012/_static/image26.png "The Files tab")</span></span>

    <span data-ttu-id="72eb5-317">*파일 탭*</span><span class="sxs-lookup"><span data-stu-id="72eb5-317">*The Files tab*</span></span>
5. <span data-ttu-id="72eb5-318">탭의 왼쪽에 있는 **토글 검사 모드** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-318">Click the **Toggle Inspection Mode** button, located at the left of the tabs.</span></span>

    <span data-ttu-id="72eb5-319">이 도구를 사용 하 여 페이지의 요소를 선택 하 고 HTML 코드 및 .aspx 소스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-319">This tool will let you select any element of the page and see its HTML code and .aspx source.</span></span>

    <span data-ttu-id="72eb5-320">![검사 모드 토글 단추](using-page-inspector-in-visual-studio-2012/_static/image27.png "검사 모드 토글 단추")</span><span class="sxs-lookup"><span data-stu-id="72eb5-320">![Toggle Inspection Mode button](using-page-inspector-in-visual-studio-2012/_static/image27.png "Toggle Inspection Mode button")</span></span>

    <span data-ttu-id="72eb5-321">*검사 모드 토글 단추*</span><span class="sxs-lookup"><span data-stu-id="72eb5-321">*Toggle Inspection Mode button*</span></span>
6. <span data-ttu-id="72eb5-322">페이지 검사기 브라우저에서 페이지 요소 위로 마우스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-322">In the Page Inspector browser, move the mouse over the page elements.</span></span> <span data-ttu-id="72eb5-323">마우스 포인터를 렌더링 된 페이지의 특정 부분으로 이동 하는 동안 요소 형식이 표시 되 고 Visual Studio 편집기에서 해당 소스 태그나 코드가 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-323">While you move the mouse pointer over any part of the rendered page, the element type is displayed and the corresponding source markup or code is highlighted in the Visual Studio editor.</span></span>

    <span data-ttu-id="72eb5-324">![검사 모드 실행](using-page-inspector-in-visual-studio-2012/_static/image28.png "검사 모드 실행")</span><span class="sxs-lookup"><span data-stu-id="72eb5-324">![Inspection mode in action](using-page-inspector-in-visual-studio-2012/_static/image28.png "Inspection mode in action")</span></span>

    <span data-ttu-id="72eb5-325">*검사 모드 실행*</span><span class="sxs-lookup"><span data-stu-id="72eb5-325">*Inspection mode in action*</span></span>

    > [!NOTE]
    > <span data-ttu-id="72eb5-326">페이지 검사기 창을 최대화 하지 마십시오. 그렇지 않으면 소스 코드를 표시 하는 미리 보기 탭을 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-326">Do not maximize the Page Inspector window or you will not be able to see the preview tab showing the source code.</span></span> <span data-ttu-id="72eb5-327">최대화 된 페이지 검사기의 요소를 클릭 하면 선택의 소스 코드가 표시 되지만 페이지 검사기 창이 숨겨집니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-327">If you click the element in Page Inspector when it is maximized, the source code of the selection will appear but it will hide the Page Inspector window.</span></span>

    <span data-ttu-id="72eb5-328">**Default.aspx 파일에** 주의를 기울여야 하는 경우 선택한 요소를 생성 하는 소스 코드 부분이 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-328">If you pay attention to **Default.aspx** file, you will notice that the portion of source code that generates the selected element is highlighted.</span></span> <span data-ttu-id="72eb5-329">이 기능은 긴 소스 파일의 버전을 용이 하 게 하 여 코드에 직접적이 고 빠르게 액세스할 수 있는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-329">This feature facilitates the edition of long source files, providing a direct and fast way to access the code.</span></span>

    <span data-ttu-id="72eb5-330">![요소 검사](using-page-inspector-in-visual-studio-2012/_static/image29.png "요소 검사")</span><span class="sxs-lookup"><span data-stu-id="72eb5-330">![Inspecting elements](using-page-inspector-in-visual-studio-2012/_static/image29.png "Inspecting elements")</span></span>

    <span data-ttu-id="72eb5-331">*요소 검사*</span><span class="sxs-lookup"><span data-stu-id="72eb5-331">*Inspecting elements*</span></span>
7. <span data-ttu-id="72eb5-332">**설정/해제** 단추를 클릭 합니다 (html-html-검사 모드-html-![코드에서 렌더링-탐색기-브라우저-탐색기-브라우저에서).](using-page-inspector-in-visual-studio-2012/_static/image30.png "-Html-html-코드-렌더링-페이지-탐색-탐색기-브라우저를 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="72eb5-332">Click the **Toggle Inspection Mode** button (![Select-the-HTML-tab-to-display-the-HTML-code-rendered-in-the-Page-Inspector-browser.](using-page-inspector-in-visual-studio-2012/_static/image30.png "Select-the-HTML-tab-to-display-the-HTML-code-rendered-in-the-Page-Inspector-browser.")</span></span> <span data-ttu-id="72eb5-333">)를 사용 하 여 커서를 사용 하지 않도록 설정 페이지 검사기.</span><span class="sxs-lookup"><span data-stu-id="72eb5-333">), located in Page Inspector tabs, to disable the cursor.</span></span>
8. <span data-ttu-id="72eb5-334">**Html** 탭을 선택 하 여 페이지 검사기 브라우저에서 렌더링 된 html 코드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-334">Select the **HTML** tab to display the HTML code rendered in the Page Inspector browser.</span></span>
9. <span data-ttu-id="72eb5-335">HTML 코드에서 Koala 링크를 사용 하 여 목록 항목을 찾아 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-335">In the HTML code, locate the list item with the Koala link and select it.</span></span>

    <span data-ttu-id="72eb5-336">코드를 선택 하면 해당 출력이 자동으로 브라우저에 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-336">Notice that when you select the code, the corresponding output is automatically highlighted browser.</span></span> <span data-ttu-id="72eb5-337">이 기능은 HTML 블록이 페이지에서 렌더링 되는 방법을 확인 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-337">This feature is useful to see how an HTML block is rendered on the page.</span></span>

    <span data-ttu-id="72eb5-338">![페이지에서 HTML 요소 선택](using-page-inspector-in-visual-studio-2012/_static/image31.png "페이지에서 HTML 요소 선택")</span><span class="sxs-lookup"><span data-stu-id="72eb5-338">![Selecting an HTML element in the page](using-page-inspector-in-visual-studio-2012/_static/image31.png "Selecting an HTML element in the page")</span></span>

    <span data-ttu-id="72eb5-339">*페이지에서 HTML 요소 선택*</span><span class="sxs-lookup"><span data-stu-id="72eb5-339">*Selecting an HTML element in the page*</span></span>
10. <span data-ttu-id="72eb5-340">검사 모드 설정 **/해제** 단추를 클릭 하 여 *검사 모드* 를 사용 하도록 설정 하 고 탐색 모음을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-340">Click the **Toggle Inspection Mode** button to enable *Inspection Mode* and click the navigation bar.</span></span> <span data-ttu-id="72eb5-341">HTML 코드의 오른쪽에 있는 스타일 창에 선택한 요소에 CSS 스타일이 적용 된 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-341">On the right of the HTML code, in the Styles pane, you will see a list with the CSS styles applied to the selected element.</span></span>

    > [!NOTE]
    > <span data-ttu-id="72eb5-342">헤더가 사이트 레이아웃의 일부 이기 때문에 페이지 검사기는 사이트 .Master 파일도 열고 영향을 받는 코드의 세그먼트를 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-342">since the header is a part of the site layout, Page Inspector will also open Site.Master file and highlight the segment of code affected.</span></span>

    <span data-ttu-id="72eb5-343">![스타일 검색 WebForms](using-page-inspector-in-visual-studio-2012/_static/image32.png "선택한 요소의 스타일 및 소스 파일 검색")</span><span class="sxs-lookup"><span data-stu-id="72eb5-343">![Discovering styles WebForms](using-page-inspector-in-visual-studio-2012/_static/image32.png "Discovering styles and source files of a selected element")</span></span>

    <span data-ttu-id="72eb5-344">*선택한 요소의 스타일 및 소스 파일 검색*</span><span class="sxs-lookup"><span data-stu-id="72eb5-344">*Discovering styles and source files of a selected element*</span></span>
11. <span data-ttu-id="72eb5-345">검사 설정/해제 포인터가 활성화 된 상태에서 마우스 포인터를 메뉴 모음 아래로 이동 하 고 빈 절반 원을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-345">With the toggle inspection pointer enabled, move the mouse pointer below the menu bar and click the blank half circle.</span></span>

    <span data-ttu-id="72eb5-346">![요소 선택](using-page-inspector-in-visual-studio-2012/_static/image33.png "요소 선택")</span><span class="sxs-lookup"><span data-stu-id="72eb5-346">![Selecting an element](using-page-inspector-in-visual-studio-2012/_static/image33.png "Selecting an element")</span></span>

    <span data-ttu-id="72eb5-347">*요소 선택*</span><span class="sxs-lookup"><span data-stu-id="72eb5-347">*Selecting an element*</span></span>
12. <span data-ttu-id="72eb5-348">스타일 창의 **. 주-콘텐츠** 그룹에서 **배경 이미지** 항목을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-348">In the Styles pane, locate the **background-image** item under the **.main-content** group.</span></span> <span data-ttu-id="72eb5-349">**배경 이미지** 를 **선택 취소** 하 고 어떻게 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-349">**Uncheck** the **background-image** and see what happens.</span></span> <span data-ttu-id="72eb5-350">그러면 브라우저에 변경 내용이 즉시 반영 되 고 원이 숨겨집니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-350">You will notice that the browser will reflect the changes immediately and the circle is hidden.</span></span>

    > [!NOTE]
    > <span data-ttu-id="72eb5-351">페이지 검사기 스타일 탭에서 적용 하는 변경 내용은 원래 스타일 시트에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-351">The changes you apply on the Page Inspector Styles tab do not affect the original stylesheet.</span></span> <span data-ttu-id="72eb5-352">스타일을 선택 취소 하거나 값을 원하는 횟수 만큼 변경할 수 있지만 페이지를 새로 고치면 복원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-352">You can uncheck styles or change their values as many times as you want, but they will be restored after refreshing the page.</span></span>

    <span data-ttu-id="72eb5-353">![CSS styles2 사용 및 사용 안 함](using-page-inspector-in-visual-studio-2012/_static/image34.png "CSS 스타일 사용 및 사용 안 함")</span><span class="sxs-lookup"><span data-stu-id="72eb5-353">![Enabling and disabling CSS styles2](using-page-inspector-in-visual-studio-2012/_static/image34.png "Enabling and disabling CSS styles")</span></span>

    <span data-ttu-id="72eb5-354">*CSS 스타일 사용 및 사용 안 함*</span><span class="sxs-lookup"><span data-stu-id="72eb5-354">*Enabling and disabling CSS styles*</span></span>
13. <span data-ttu-id="72eb5-355">이제 검사 모드를 사용 하 여 헤더**의 '** **여기에서 로고** ' 텍스트를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-355">Now, click the '**your** **logo here'** text on the header using the inspection mode.</span></span>
14. <span data-ttu-id="72eb5-356">**스타일** 탭의 **. 사이트 제목** 그룹에서 **font-size** CSS 특성을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-356">In the **Styles** tab, locate the **font-size** CSS attribute under the **.site-title** group.</span></span> <span data-ttu-id="72eb5-357">특성을 두 번 클릭 하 여 해당 값을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-357">Double-click the attribute once to edit its value.</span></span> <span data-ttu-id="72eb5-358">2\.3 em 값을 **3em**으로 바꾸고 enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-358">Replace the 2.3em value with **3em**, and then press ENTER.</span></span> <span data-ttu-id="72eb5-359">제목이 클수록 보입니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-359">Notice that the title looks bigger.</span></span>

    <span data-ttu-id="72eb5-360">![Inspector2 페이지에서 CSS 값 변경](using-page-inspector-in-visual-studio-2012/_static/image35.png "페이지 검사기에서 CSS 값 변경")</span><span class="sxs-lookup"><span data-stu-id="72eb5-360">![Changing CSS values in the Page Inspector2](using-page-inspector-in-visual-studio-2012/_static/image35.png "Changing CSS values in the Page Inspector")</span></span>

    <span data-ttu-id="72eb5-361">*페이지 검사기에서 CSS 값 변경*</span><span class="sxs-lookup"><span data-stu-id="72eb5-361">*Changing CSS values in the Page Inspector*</span></span>
15. <span data-ttu-id="72eb5-362">페이지 검사기의 오른쪽 창에 있는 **추적 스타일** 탭을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-362">Click the **Trace Styles** tab, located in the right pane of Page Inspector.</span></span> <span data-ttu-id="72eb5-363">이 방법은 선택 항목에 적용 된 모든 스타일을 특성 이름별로 정렬 하 여 표시 하는 대체 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-363">This is an alternative way to see all the styles applied to the selection, ordered by attribute name.</span></span>

    <span data-ttu-id="72eb5-364">![선택한 요소의 CSS 스타일 추적](using-page-inspector-in-visual-studio-2012/_static/image36.png "선택한 요소의 CSS 스타일 추적")</span><span class="sxs-lookup"><span data-stu-id="72eb5-364">![CSS styles tracing of the selected element](using-page-inspector-in-visual-studio-2012/_static/image36.png "CSS styles tracing of the selected element")</span></span>

    <span data-ttu-id="72eb5-365">*선택한 요소의 CSS 스타일 추적*</span><span class="sxs-lookup"><span data-stu-id="72eb5-365">*CSS styles tracing of the selected element*</span></span>
16. <span data-ttu-id="72eb5-366">페이지 검사기의 또 다른 기능은 레이아웃 창입니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-366">Another feature of Page Inspector is the Layout pane.</span></span> <span data-ttu-id="72eb5-367">검사 모드를 사용 하 여 탐색 모음을 선택 하 고 오른쪽 창에서 **레이아웃** 탭을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-367">Using the inspection mode, select the navigation bar and then click the **Layout** tab on the right pane.</span></span> <span data-ttu-id="72eb5-368">선택한 요소의 정확한 크기와 해당 오프셋, 여백, 안쪽 여백 및 테두리 크기가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-368">You will see the exact size of the selected element, as well as its offset, margin, padding and border size.</span></span> <span data-ttu-id="72eb5-369">이 보기에서 값을 수정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-369">Notice that you can also modify the values from this view.</span></span>

    <span data-ttu-id="72eb5-370">![페이지 검사기의 요소 레이아웃](using-page-inspector-in-visual-studio-2012/_static/image37.png "페이지 검사기의 요소 레이아웃")</span><span class="sxs-lookup"><span data-stu-id="72eb5-370">![Element layout in Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image37.png "Element layout in Page Inspector")</span></span>

    <span data-ttu-id="72eb5-371">*페이지 검사기의 요소 레이아웃*</span><span class="sxs-lookup"><span data-stu-id="72eb5-371">*Element layout in Page Inspector*</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a><span data-ttu-id="72eb5-372">작업 2-사진 갤러리에서 스타일 문제 찾기 및 수정</span><span class="sxs-lookup"><span data-stu-id="72eb5-372">Task 2 - Finding and Fixing Style Issues in the Photo Gallery</span></span>

<span data-ttu-id="72eb5-373">이전 버전의 Visual Studio에서 웹 페이지 문제를 진단 하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="72eb5-373">How would you diagnose Web pages issues with previous versions of Visual Studio?</span></span> <span data-ttu-id="72eb5-374">Internet Explorer 개발자 도구 또는 Firebug와 같이 Visual Studio IDE 외부에서 실행 되는 웹 디버깅 도구에 대해 잘 알고 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-374">You are likely familiar with web debugging tools that run outside the Visual Studio IDE, like Internet Explorer Developer Tools or Firebug.</span></span> <span data-ttu-id="72eb5-375">브라우저는 HTML, 스크립팅 및 스타일만 이해 하는 반면 기본 프레임 워크는 렌더링 될 HTML을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-375">Browsers only understand HTML, scripting and styles, while an underlying framework generates the HTML that will be rendered.</span></span> <span data-ttu-id="72eb5-376">따라서 웹 페이지의 모양을 확인 하려면 전체 사이트를 배포 해야 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-376">For that reason, you often need to deploy the whole site to see how web pages look like.</span></span>

<span data-ttu-id="72eb5-377">웹 사이트에서 문제를 검색 하 고 수정 하려는 경우 다음 단계를 수행 했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-377">You had probably followed these steps when you wanted to detect and fix an issue in your web site:</span></span>

1. <span data-ttu-id="72eb5-378">Visual Studio에서 솔루션을 실행 하거나 웹 서버에 페이지를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-378">Run the Solution from Visual Studio, or deploy the page on the web server.</span></span>
2. <span data-ttu-id="72eb5-379">브라우저에서 사용 하는 개발자 도구를 열거나 소스 코드와 스타일을 열고 문제를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-379">In the browser, open the developer tools you use, or simply open the source code and the styles and try to match the issue.</span></span> <span data-ttu-id="72eb5-380">관련 파일을 찾으려면 스타일 클래스의 이름을 사용 하 여 &quot;검색&quot; 또는 파일에서 검색&quot; 기능을 &quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-380">To find the files involved, you'd have used the &quot;Search&quot; or &quot;Search in files&quot; features with the name of the style classes.</span></span>
3. <span data-ttu-id="72eb5-381">오류가 검색 되 면 웹 브라우저 및 서버를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-381">Once the error is detected, stop the Web browser and the server.</span></span>
4. <span data-ttu-id="72eb5-382">브라우저 캐시를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-382">Clear the browser cache.</span></span>
5. <span data-ttu-id="72eb5-383">수정 사항을 적용 하려면 Visual Studio로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-383">Return to Visual Studio to apply a fix.</span></span> <span data-ttu-id="72eb5-384">테스트 하는 모든 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-384">Repeat all the steps to test.</span></span>

<span data-ttu-id="72eb5-385">ASP.NET WebForms에는 실제 WYSIWYG가 없으므로 이후 단계에서 (실행 또는 배포 후) 일부 스타일 문제가 감지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-385">As there is no real WYSIWYG in ASP.NET WebForms, some style issues are detected on a later stage, after running or deploying.</span></span> <span data-ttu-id="72eb5-386">이제 페이지 검사기를 사용 하 여 솔루션을 실행 하지 않고 모든 페이지를 미리 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-386">Now, with Page Inspector, it is possible to preview any page without running the solution.</span></span>

<span data-ttu-id="72eb5-387">이 작업에서는 사진 갤러리 응용 프로그램의 일부 문제를 해결 하는 데 페이지 검사기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-387">In this task, you will use the Page inspector for fixing some issues of the Photo Gallery application.</span></span> <span data-ttu-id="72eb5-388">다음 단계에서는 헤더에서 몇 가지 간단한 스타일 지정 문제를 검색 하 고 신속 하 게 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-388">In the following steps, you will detect and quickly fix some simple styling issue in the header.</span></span>

1. <span data-ttu-id="72eb5-389">페이지 검사를 사용 하 여 헤더의 왼쪽에 있는 **레지스터** 및 **로그인** 링크를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-389">Using Page Inspection, locate the **Register** and the **Log In** links at the left side of the header.</span></span>

    <span data-ttu-id="72eb5-390">오른쪽의 예상 위치에는 링크가 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-390">Notice that the link is not displayed at the expected place on the right.</span></span> <span data-ttu-id="72eb5-391">이제 링크를 오른쪽에 맞추고 그에 맞게 스타일을 다시 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-391">You will now align the link to the right and restyle it accordingly.</span></span>

    <span data-ttu-id="72eb5-392">![왼쪽에 위치 하는 로그인 링크](using-page-inspector-in-visual-studio-2012/_static/image38.png "왼쪽에 위치 하는 로그인 링크")</span><span class="sxs-lookup"><span data-stu-id="72eb5-392">![Log in link positioned on the left](using-page-inspector-in-visual-studio-2012/_static/image38.png "Log in link positioned on the left")</span></span>

    <span data-ttu-id="72eb5-393">*왼쪽에 위치 하는 로그인 링크*</span><span class="sxs-lookup"><span data-stu-id="72eb5-393">*Log In link positioned on the left*</span></span>
2. <span data-ttu-id="72eb5-394">토글 검사 모드 선택 하 고 로그인 링크를 선택 하 여 해당 코드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-394">With Toggle Inspection Mode selected, select the Log In link to open its code.</span></span>

    <span data-ttu-id="72eb5-395">링크 소스 코드는 첫 번째 위치에 있는 default.aspx 페이지가 아닌 **site.master** 파일에 위치 하는 것을 볼 수 있습니다. 올바른 소스 파일에 직접 배치 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-395">Notice that the link source code is located in the **Site.Master** file, not in the Default.aspx page which is the place you might look in first place; you have been placed directly in the correct source file.</span></span>
3. <span data-ttu-id="72eb5-396">**스타일** 탭에서 이러한 링크의 HTML 컨테이너인 **&lt;섹션&gt; #login** 항목을 찾아 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-396">In the **Styles** tab, locate and click the **&lt;section&gt; #login** item, which is the HTML container for these links.</span></span>

    <span data-ttu-id="72eb5-397">**#Login** 스타일은를 클릭 한 후에 자동으로 **사이트 .css** 에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-397">Notice that the **#login** style is automatically located in **Site.css** after you click.</span></span> <span data-ttu-id="72eb5-398">코드도 이제 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-398">Moreover, the code is now highlighted.</span></span>

    <span data-ttu-id="72eb5-399">![CSS 스타일 선택](using-page-inspector-in-visual-studio-2012/_static/image39.png "CSS 스타일 선택")</span><span class="sxs-lookup"><span data-stu-id="72eb5-399">![Selecting the CSS styles](using-page-inspector-in-visual-studio-2012/_static/image39.png "Selecting the CSS styles")</span></span>

    <span data-ttu-id="72eb5-400">*CSS 스타일 선택*</span><span class="sxs-lookup"><span data-stu-id="72eb5-400">*Selecting the CSS styles*</span></span>
4. <span data-ttu-id="72eb5-401">열기 및 닫기 문자를 제거 하 여 강조 표시 된 코드에서 **텍스트 맞춤** 특성의 주석 처리를 제거 하 고 **사이트 .css** 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-401">Uncomment the **text-align** attribute in the highlighted code by removing the opening and closing characters and save the **Site.css** file.</span></span>

    <span data-ttu-id="72eb5-402">페이지 검사기는 현재 페이지를 구성 하는 다른 모든 파일을 인식 하 고 이러한 파일이 변경 되 면이를 감지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-402">Page Inspector is aware of all the different files that compose the current page, and it can detect when any of these files change.</span></span> <span data-ttu-id="72eb5-403">브라우저의 현재 페이지가 원본 파일과 동기화 되지 않을 때마다 경고를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-403">It alerts you whenever the current page in browser is not in sync with the source files.</span></span>
5. <span data-ttu-id="72eb5-404">페이지 검사기 브라우저에서 주소 표시줄 아래에 있는 막대를 클릭 하 여 변경 내용을 저장 하 고 페이지를 다시 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-404">In the Page Inspector browser, click the bar located below the address bar to save the changes and reload the page.</span></span>

    ![페이지 다시 로드](using-page-inspector-in-visual-studio-2012/_static/image40.png)

    <span data-ttu-id="72eb5-406">*페이지 다시 로드*</span><span class="sxs-lookup"><span data-stu-id="72eb5-406">*Reloading the page*</span></span>

    <span data-ttu-id="72eb5-407">링크는 이제 오른쪽에 있지만 여전히 글머리 기호 목록과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-407">The links are now at the right, but they still look like a bulleted list.</span></span> <span data-ttu-id="72eb5-408">이제 글머리 기호를 제거 하 고 링크를 가로로 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-408">Now, you will remove the bullets and align the links horizontally.</span></span>

    ![업데이트 된 페이지](using-page-inspector-in-visual-studio-2012/_static/image41.png)

    <span data-ttu-id="72eb5-410">*업데이트 된 페이지*</span><span class="sxs-lookup"><span data-stu-id="72eb5-410">*Updated page*</span></span>
6. <span data-ttu-id="72eb5-411">검사 모드를 사용 하 여 &quot;등록&quot;를 포함 하는 **&lt;li&gt;** 항목을 선택 하 고 &quot;링크를&quot; 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-411">Using the inspection mode, select any of the **&lt;li&gt;** items that contain the &quot;Register&quot; and &quot;Log in&quot; links.</span></span> <span data-ttu-id="72eb5-412">그런 다음 **&lt;섹션&gt; #login** 항목을 클릭 하 여 **스타일 css** 코드에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-412">Then, click the **&lt;section&gt; #login** item to access **Styles.css** code.</span></span>

    <span data-ttu-id="72eb5-413">![스타일 찾기](using-page-inspector-in-visual-studio-2012/_static/image42.png "스타일 찾기")</span><span class="sxs-lookup"><span data-stu-id="72eb5-413">![Finding the style](using-page-inspector-in-visual-studio-2012/_static/image42.png "Finding the style")</span></span>

    <span data-ttu-id="72eb5-414">*스타일 찾기*</span><span class="sxs-lookup"><span data-stu-id="72eb5-414">*Finding the style*</span></span>
7. <span data-ttu-id="72eb5-415">**스타일 .css**에서 **#login li** 항목에 대 한 코드의 주석 처리를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-415">In **Style.css**, uncomment the code for **#login li** items.</span></span> <span data-ttu-id="72eb5-416">추가 하는 스타일은 글머리 기호를 숨기고 항목이 가로로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-416">The style you are adding will hide the bullet and display the items horizontally.</span></span>

    <span data-ttu-id="72eb5-417">![로그인 링크의 스타일 다시 지정](using-page-inspector-in-visual-studio-2012/_static/image43.png "로그인 링크의 스타일 다시 지정")</span><span class="sxs-lookup"><span data-stu-id="72eb5-417">![Restyling the login links](using-page-inspector-in-visual-studio-2012/_static/image43.png "Restyling the login links")</span></span>

    <span data-ttu-id="72eb5-418">*로그인 링크의 스타일 다시 지정*</span><span class="sxs-lookup"><span data-stu-id="72eb5-418">*Restyling the login links*</span></span>
8. <span data-ttu-id="72eb5-419">**스타일 .css** 파일을 저장 하 고 주소 아래에 있는 막대에서 한 번을 클릭 하 여 페이지를 다시 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-419">Save **Style.css** file and click once on the bar located below the address to reload the page.</span></span> <span data-ttu-id="72eb5-420">링크가 올바르게 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-420">Notice that the links appear correctly.</span></span>

    <span data-ttu-id="72eb5-421">![오른쪽에 정렬 된 링크](using-page-inspector-in-visual-studio-2012/_static/image44.png "오른쪽에 정렬 된 링크")</span><span class="sxs-lookup"><span data-stu-id="72eb5-421">![Links aligned to the right side](using-page-inspector-in-visual-studio-2012/_static/image44.png "Links aligned to the right side")</span></span>

    <span data-ttu-id="72eb5-422">*오른쪽에 정렬 된 링크*</span><span class="sxs-lookup"><span data-stu-id="72eb5-422">*Links aligned to the right side*</span></span>
9. <span data-ttu-id="72eb5-423">마지막으로 헤더 제목을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-423">Finally, you will change the header title.</span></span> <span data-ttu-id="72eb5-424">모든 파일에서 '**로고 위치 '** 텍스트를 검색 하는 대신 검사 모드를 사용 하 여 텍스트를 클릭 하 고이를 생성 하는 소스 코드를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-424">Instead of searching for the '**your logo here'** text in all the files, use the inspection mode to click the text and get to source code that generates it.</span></span>

    <span data-ttu-id="72eb5-425">![사이트 제목 찾기](using-page-inspector-in-visual-studio-2012/_static/image45.png "사이트 제목 찾기")</span><span class="sxs-lookup"><span data-stu-id="72eb5-425">![Finding the site title](using-page-inspector-in-visual-studio-2012/_static/image45.png "Finding the site title")</span></span>

    <span data-ttu-id="72eb5-426">*사이트 제목 찾기*</span><span class="sxs-lookup"><span data-stu-id="72eb5-426">*Finding the site title*</span></span>
10. <span data-ttu-id="72eb5-427">이제 **site.master**에서 '**로고를 여기**' 텍스트를 '**사진 갤러리**'로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-427">Now you are in **Site.Master**, replace the '**your logo here**' text with '**Photo Gallery**'.</span></span> <span data-ttu-id="72eb5-428">페이지 검사기 브라우저를 저장 하 고 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-428">Save and update the Page Inspector browser.</span></span>

    <span data-ttu-id="72eb5-429">![사진 갤러리 페이지가 업데이트 됨](using-page-inspector-in-visual-studio-2012/_static/image46.png "사진 갤러리 페이지가 업데이트 됨")</span><span class="sxs-lookup"><span data-stu-id="72eb5-429">![Photo Gallery page updated](using-page-inspector-in-visual-studio-2012/_static/image46.png "Photo Gallery page updated")</span></span>

    <span data-ttu-id="72eb5-430">*사진 갤러리 페이지가 업데이트 됨*</span><span class="sxs-lookup"><span data-stu-id="72eb5-430">*Photo Gallery page updated*</span></span>
11. <span data-ttu-id="72eb5-431">마지막으로 **f5** 키를 눌러 앱을 실행 합니다. 모든 변경 내용이 예상 대로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-431">Finally press **F5** to run the app the check out all the changes work as expected.</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="72eb5-432">요약</span><span class="sxs-lookup"><span data-stu-id="72eb5-432">Summary</span></span>

<span data-ttu-id="72eb5-433">이 실습 실습을 완료 하면 브라우저에서 웹 사이트를 다시 빌드하고 실행할 필요 없이 페이지 검사기를 사용 하 여 웹 응용 프로그램을 미리 보는 방법을 학습 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-433">By completing this Hands-On Lab, you have learnt how to use Page Inspector to preview your Web application without having to rebuild and run the Web site in a browser.</span></span> <span data-ttu-id="72eb5-434">또한 렌더링 된 출력에서 소스 코드에 직접 액세스 하 여 버그를 신속 하 게 찾아 수정 하는 방법을 학습 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-434">In addition, you have learnt how to quickly find and fix bugs by accessing directly from the rendered output to the source code.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="72eb5-435">부록 A: 웹에 대 한 Visual Studio Express 2012 설치</span><span class="sxs-lookup"><span data-stu-id="72eb5-435">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="72eb5-436">**[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)** 를 사용 하 여 웹 또는 다른 &quot;Express&quot; 버전 **에 대해 Microsoft Visual Studio Express 2012** 를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-436">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="72eb5-437">다음 지침에서는 *Microsoft 웹 플랫폼 설치 관리자*를 사용 하 여 *Visual studio Express 2012 for Web* 을 설치 하는 데 필요한 단계를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-437">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="72eb5-438">[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-438">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="72eb5-439">또는 웹 플랫폼 설치 관리자를 이미 설치한 경우에는 웹 플랫폼 설치 관리자를 열고 <em>Microsoft AZURE SDK&quot;를 사용 하 여 웹 용 2012 Visual Studio Express</em> &quot;제품을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-439">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="72eb5-440">**지금 설치**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-440">Click on **Install Now**.</span></span> <span data-ttu-id="72eb5-441">**웹 플랫폼 설치 관리자** 가 없으면 먼저이를 다운로드 하 여 설치 하도록 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-441">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="72eb5-442">**웹 플랫폼 설치 관리자** 가 열리면 **설치** 를 클릭 하 여 설치를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-442">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="72eb5-443">![Visual Studio Express 설치](using-page-inspector-in-visual-studio-2012/_static/image47.png "Visual Studio Express 설치")</span><span class="sxs-lookup"><span data-stu-id="72eb5-443">![Install Visual Studio Express](using-page-inspector-in-visual-studio-2012/_static/image47.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="72eb5-444">*Visual Studio Express 설치*</span><span class="sxs-lookup"><span data-stu-id="72eb5-444">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="72eb5-445">모든 제품의 라이선스 및 사용 조건을 읽고 **동의** 함을 클릭 하 여 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-445">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![사용 조건 동의](using-page-inspector-in-visual-studio-2012/_static/image48.png)

    <span data-ttu-id="72eb5-447">*사용 조건 동의*</span><span class="sxs-lookup"><span data-stu-id="72eb5-447">*Accepting the license terms*</span></span>
5. <span data-ttu-id="72eb5-448">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-448">Wait until the downloading and installation process completes.</span></span>

    ![설치 진행률](using-page-inspector-in-visual-studio-2012/_static/image49.png)

    <span data-ttu-id="72eb5-450">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="72eb5-450">*Installation progress*</span></span>
6. <span data-ttu-id="72eb5-451">설치가 완료 되 면 **마침**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-451">When the installation completes, click **Finish**.</span></span>

    ![설치 완료](using-page-inspector-in-visual-studio-2012/_static/image50.png)

    <span data-ttu-id="72eb5-453">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="72eb5-453">*Installation completed*</span></span>
7. <span data-ttu-id="72eb5-454">**끝내기** 를 클릭 하 여 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-454">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="72eb5-455">웹에 대 한 Visual Studio Express를 열려면 **시작** 화면으로 이동 하 &quot;**VS Express**&quot;작성을 시작한 후 **VS Express for Web** 타일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="72eb5-455">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 타일](using-page-inspector-in-visual-studio-2012/_static/image51.png)

    <span data-ttu-id="72eb5-457">*VS Express for Web 타일*</span><span class="sxs-lookup"><span data-stu-id="72eb5-457">*VS Express for Web tile*</span></span>
