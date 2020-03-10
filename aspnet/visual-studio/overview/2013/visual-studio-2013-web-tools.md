---
uid: visual-studio/overview/2013/visual-studio-2013-web-tools
title: '실습: 웹 도구 Visual Studio 2013 | Microsoft Docs'
author: rick-anderson
description: Visual Studio는의 뛰어난 개발 환경입니다. NET 기반 Windows 및 웹 프로젝트. 여기에는 쉽게 사용할 수 있는 강력한 텍스트 편집기가 포함 되어 있습니다.
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 09e82351-816b-402d-acd1-0f9ac6901d16
msc.legacyurl: /visual-studio/overview/2013/visual-studio-2013-web-tools
msc.type: authoredcontent
ms.openlocfilehash: 2fb987dd9b26ad9f0e8a88fd881bde4505ec4148
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505007"
---
# <a name="hands-on-lab-visual-studio-2013-web-tools"></a><span data-ttu-id="98c5b-104">실습: 웹 도구 Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="98c5b-104">Hands On Lab: Visual Studio 2013 Web Tools</span></span>

<span data-ttu-id="98c5b-105">[웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="98c5b-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="98c5b-106">웹 캠프 교육 키트 다운로드</span><span class="sxs-lookup"><span data-stu-id="98c5b-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

> <span data-ttu-id="98c5b-107">Visual Studio는의 뛰어난 개발 환경입니다. NET 기반 Windows 및 웹 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="98c5b-107">Visual Studio is an excellent development environment for .NET-based Windows and web projects.</span></span> <span data-ttu-id="98c5b-108">여기에는 프로젝트 없이 독립 실행형 파일을 쉽게 편집할 수 있는 강력한 텍스트 편집기가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-108">It includes a powerful text editor that can easily be used to edit standalone files without a project.</span></span>
> 
> <span data-ttu-id="98c5b-109">Visual Studio는 각 파일을 편집할 때 전체 기능을 갖춘 구문 분석 트리를 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-109">Visual Studio maintains a full-featured parse tree as you edit each file.</span></span> <span data-ttu-id="98c5b-110">이를 통해 Visual Studio에서 뛰어난 자동 완성 및 문서 기반 작업을 제공 하 고 개발 환경을 훨씬 빠르고 즐겁게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-110">This allows Visual Studio to provide unparalleled auto-completion and document-based actions while making the development experience much faster and more pleasant.</span></span> <span data-ttu-id="98c5b-111">이러한 기능은 HTML 및 CSS 문서에서 특히 강력한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-111">These features are especially powerful in HTML and CSS documents.</span></span>
> 
> <span data-ttu-id="98c5b-112">이러한 모든 기능을 확장에 사용할 수 있으므로 요구 사항에 맞게 강력한 새 기능으로 편집기를 쉽게 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-112">All of this power is also available for extensions, making it simple to extend the editors with powerful new features to suit your needs.</span></span> <span data-ttu-id="98c5b-113">Web Essentials는 Visual Studio에 대 한 대부분의 웹 관련 향상 된 기능 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-113">Web Essentials is a collection of (mostly) web-related enhancements to Visual Studio.</span></span> <span data-ttu-id="98c5b-114">여기에는 많은 새 IntelliSense 완성 (특히 CSS의 경우), 새로운 브라우저 링크 기능, JavaScript 파일용 자동 JSHint, HTML 및 CSS에 대 한 새로운 경고, 최신 웹 개발에 필수적인 기타 많은 기능이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-114">It includes lots of new IntelliSense completions (especially for CSS), new Browser Link features, automatic JSHint for JavaScript files, new warnings for HTML and CSS, and many other features that are essential to modern web development.</span></span>
> 
> <span data-ttu-id="98c5b-115">모든 샘플 코드와 코드 조각은 [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)에서 사용할 수 있는 웹 캠프 교육 키트에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-115">All sample code and snippets are included in the Web Camps Training Kit, available at [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).</span></span>

<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="98c5b-116">개요</span><span class="sxs-lookup"><span data-stu-id="98c5b-116">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="98c5b-117">목표</span><span class="sxs-lookup"><span data-stu-id="98c5b-117">Objectives</span></span>

<span data-ttu-id="98c5b-118">이 실습 랩에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-118">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="98c5b-119">풍부한 HTML5 코드 조각 및 Zen 코딩 등 Web Essentials에 포함 된 새 HTML 편집기 기능 사용</span><span class="sxs-lookup"><span data-stu-id="98c5b-119">Use new HTML editor features included in Web Essentials such as rich HTML5 code snippets and Zen coding</span></span>
- <span data-ttu-id="98c5b-120">색 선택 및 브라우저 매트릭스 도구 설명과 같은 웹 Essentials에 포함 된 새 CSS 편집기 기능 사용</span><span class="sxs-lookup"><span data-stu-id="98c5b-120">Use new CSS editor features included in Web Essentials such as the Color picker and Browser matrix tooltip</span></span>
- <span data-ttu-id="98c5b-121">모든 HTML 요소에 대 한 파일 및 IntelliSense에 압축 풀기와 같은 웹 Essentials에 포함 된 새 JavaScript 편집기 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-121">Use new JavaScript editor features included in Web Essentials such as Extract to File and IntelliSense for all HTML elements</span></span>
- <span data-ttu-id="98c5b-122">브라우저 링크를 사용 하 여 브라우저와 Visual Studio 간 데이터 교환</span><span class="sxs-lookup"><span data-stu-id="98c5b-122">Exchange data between your browser and Visual Studio using Browser Link</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="98c5b-123">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="98c5b-123">Prerequisites</span></span>

<span data-ttu-id="98c5b-124">이 실습 실습을 완료 하려면 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-124">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="98c5b-125">[Microsoft Visual Studio Professional 2013](https://www.microsoft.com/visualstudio/) 이상</span><span class="sxs-lookup"><span data-stu-id="98c5b-125">[Microsoft Visual Studio Professional 2013](https://www.microsoft.com/visualstudio/) or greater</span></span>
- [<span data-ttu-id="98c5b-126">웹 Essentials 2013</span><span class="sxs-lookup"><span data-stu-id="98c5b-126">Web Essentials 2013</span></span>](http://vswebessentials.com/)
- [<span data-ttu-id="98c5b-127">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="98c5b-127">Google Chrome</span></span>](https://www.google.com/chrome/)

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="98c5b-128">설치 프로그램</span><span class="sxs-lookup"><span data-stu-id="98c5b-128">Setup</span></span>

<span data-ttu-id="98c5b-129">이 실습 랩에서 연습을 실행 하려면 먼저 환경을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-129">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="98c5b-130">Windows 탐색기 창을 열고 랩의 **원본** 폴더로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-130">Open a Windows Explorer window and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="98c5b-131">**Setup.exe** 를 마우스 오른쪽 단추로 클릭 하 고 **관리자 권한으로 실행** 을 선택 하 여 환경을 구성 하는 설치 프로세스를 시작 하 고이 랩에 대 한 Visual Studio 코드 조각을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-131">Right-click **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="98c5b-132">사용자 계정 컨트롤 대화 상자가 표시 되 면 계속 하려면 작업을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-132">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="98c5b-133">설치 프로그램을 실행 하기 전에이 랩에 대 한 모든 종속성을 확인 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-133">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="98c5b-134">코드 조각 사용</span><span class="sxs-lookup"><span data-stu-id="98c5b-134">Using the Code Snippets</span></span>

<span data-ttu-id="98c5b-135">랩 문서 전체에서 코드 블록을 삽입 하 라는 지침이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-135">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="98c5b-136">사용자 편의를 위해이 코드의 대부분은 Visual Studio 2013 내에서 액세스할 수 있는 Visual Studio Code 코드 조각으로 제공 되며,이를 수동으로 추가 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-136">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="98c5b-137">각 연습에는 각 연습을 서로 독립적으로 수행할 수 있는 연습 **시작** 폴더에 있는 시작 솔루션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-137">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="98c5b-138">연습 중에 추가 된 코드 조각은 이러한 시작 솔루션에서 누락 되었으며, 연습을 완료할 때까지 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-138">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="98c5b-139">연습에 대 한 소스 코드 내에서 해당 연습의 단계를 완료 하 여 생성 된 코드를 포함 하는 Visual Studio 솔루션을 포함 하는 **끝** 폴더를 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-139">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="98c5b-140">이 실습 랩을 통해 작업할 때 추가 도움이 필요한 경우 이러한 솔루션을 지침으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-140">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="98c5b-141">실습</span><span class="sxs-lookup"><span data-stu-id="98c5b-141">Exercises</span></span>

<span data-ttu-id="98c5b-142">이 실습 랩에는 다음 연습이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-142">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="98c5b-143">브라우저 링크 및 Web Essentials 작업</span><span class="sxs-lookup"><span data-stu-id="98c5b-143">Working with Browser Link and Web Essentials</span></span>](#Exercise1)
2. [<span data-ttu-id="98c5b-144">코드 조각 및 IntelliSense를 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-144">Taking Advantage of Code Snippets and IntelliSense</span></span>](#Exercise2)

> [!NOTE]
> <span data-ttu-id="98c5b-145">Visual Studio를 처음 시작 하는 경우 미리 정의 된 설정 컬렉션 중 하나를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-145">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="98c5b-146">미리 정의 된 각 컬렉션은 특정 개발 스타일에 맞게 디자인 되 고 창 레이아웃, 편집기 동작, IntelliSense 코드 조각 및 대화 상자 옵션을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-146">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="98c5b-147">이 실습의 절차에서는 **일반 개발 설정** 컬렉션을 사용 하는 경우 Visual Studio에서 지정 된 작업을 수행 하는 데 필요한 작업을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-147">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="98c5b-148">개발 환경에 대해 다른 설정 컬렉션을 선택 하는 경우 고려해 야 하는 단계에 차이가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-148">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>

<a id="Exercise1"></a>
### <a name="exercise-1-working-with-browser-link-and-web-essentials"></a><span data-ttu-id="98c5b-149">연습 1: 브라우저 링크 및 Web Essentials 작업</span><span class="sxs-lookup"><span data-stu-id="98c5b-149">Exercise 1: Working with Browser Link and Web Essentials</span></span>

<span data-ttu-id="98c5b-150">**Web Essentials** 는 최신 웹 개발을 위한 다양 한 유용한 기능을 추가 하는 Visual Studio 확장으로, 대부분 웹 개발 환경을 훨씬 빠르고 편리 하 게 만드는 데 주력 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-150">**Web Essentials** is a Visual Studio extension that adds a variety of useful features for modern web development, mostly focused on making the web development experience much faster and more pleasant.</span></span> <span data-ttu-id="98c5b-151">Visual Studio의 확장 갤러리에서 Web Essentials를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-151">You can install Web Essentials from the Extension Gallery in Visual Studio.</span></span>

<span data-ttu-id="98c5b-152">**브라우저 링크** 는 VISUAL studio IDE와 웹 응용 프로그램 및 visual studio 간에 데이터를 교환 하기 위해 열려 있는 모든 브라우저 사이에 채널을 제공 하는 Visual Studio 2013에 포함 된 새로운 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-152">**Browser Link** is a new feature included in Visual Studio 2013 that provides a channel between the Visual Studio IDE and any open browser to exchange data between your web application and Visual Studio.</span></span> <span data-ttu-id="98c5b-153">웹 Essentials는 브라우저 링크를 도구로 확장 하 여 브라우저에서 직접 웹 페이지의 CSS 스타일과 DOM 개체 모델을 조작 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-153">Web Essentials extends Browser Link with tools to manipulate the DOM object model and the CSS styles of your web pages directly from the browser.</span></span>

<span data-ttu-id="98c5b-154">이 연습에서는 간단한 퀴즈 페이지를 개선 하기 위해 **Web Essentials** 및 **브라우저 링크** 에서 지 원하는 기능 중 일부를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-154">In this exercise, you will explore some of the features supported by **Web Essentials** and **Browser Link** to enhance a simple quiz page.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1---running-the-project-in-multiple-browsers"></a><span data-ttu-id="98c5b-155">작업 1-여러 브라우저에서 프로젝트 실행</span><span class="sxs-lookup"><span data-stu-id="98c5b-155">Task 1 - Running the Project in Multiple Browsers</span></span>

<span data-ttu-id="98c5b-156">이 태스크에서는 여러 브라우저에서 한 번에 실행 되도록 웹 응용 프로그램을 구성 하며,이는 브라우저 간 테스트에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-156">In this task, you will configure your web application to run in multiple browsers at once, which is useful for cross-browser testing.</span></span>

1. <span data-ttu-id="98c5b-157">**Microsoft Visual Studio**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-157">Open **Microsoft Visual Studio**.</span></span>
2. <span data-ttu-id="98c5b-158">**파일** 메뉴에서 열기를 선택 합니다.  **프로젝트/솔루션** ... 랩의 **원본** 폴더 (C:\WebCampsTK\HOL\VSWebTooling\Source)에서 **Ex1-WorkingwithBrowserLinkandWebEssentials\Begin** 로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-158">In the **File** menu, select **Open | Project/Solution...** and browse to **Ex1-WorkingwithBrowserLinkandWebEssentials\Begin** in the **Source** folder of the lab (C:\WebCampsTK\HOL\VSWebTooling\Source).</span></span> <span data-ttu-id="98c5b-159">**시작 .sln** 을 선택 하 고 **열기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-159">Select **Begin.sln** and click **Open**.</span></span>
3. <span data-ttu-id="98c5b-160">Visual Studio 도구 모음에서 브라우저 메뉴를 확장 하 고 **찾아보기**...를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-160">In the Visual Studio toolbar, expand the browser menu and select **Browse With...**.</span></span>

    <span data-ttu-id="98c5b-161">![메뉴 옵션으로 찾아보기](visual-studio-2013-web-tools/_static/image1.png "찾아보기 ... 브라우저 메뉴")</span><span class="sxs-lookup"><span data-stu-id="98c5b-161">![Browse With menu option](visual-studio-2013-web-tools/_static/image1.png "Browse with... in browser menu")</span></span>

    <span data-ttu-id="98c5b-162">*메뉴 옵션으로 찾아보기*</span><span class="sxs-lookup"><span data-stu-id="98c5b-162">*Browse With menu option*</span></span>
4. <span data-ttu-id="98c5b-163">**브라우저** 선택 대화 상자에서 **CTRL** 키를 누른 상태에서 **Google Chrome** 및 **Internet Explorer** 를 모두 선택 하 고 **기본값으로 설정**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-163">In the **Browse With** dialog box, select both **Google Chrome** and **Internet Explorer** by holding down the **CTRL** key and click **Set as Default**.</span></span>

    <span data-ttu-id="98c5b-164">![찾아보기 대화 상자](visual-studio-2013-web-tools/_static/image2.png "찾아보기 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="98c5b-164">![Browse with dialog box](visual-studio-2013-web-tools/_static/image2.png "Browse with dialog box")</span></span>

    <span data-ttu-id="98c5b-165">*여러 기본 브라우저 선택*</span><span class="sxs-lookup"><span data-stu-id="98c5b-165">*Selecting multiple default browsers*</span></span>
5. <span data-ttu-id="98c5b-166">이제 Google Chrome과 Internet Explorer가 모두 기본 브라우저로 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-166">Both Google Chrome and Internet Explorer should now appear as the default browsers.</span></span> <span data-ttu-id="98c5b-167">**취소**를 클릭하여 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-167">Click **Cancel** to close the dialog box.</span></span>

    <span data-ttu-id="98c5b-168">![Google Chrome 및 Internet Explorer를 기본 브라우저로](visual-studio-2013-web-tools/_static/image3.png "Google Chrome 및 Internet Explorer 기본 브라우저")</span><span class="sxs-lookup"><span data-stu-id="98c5b-168">![Google Chrome and Internet Explorer as default browsers](visual-studio-2013-web-tools/_static/image3.png "Google Chrome and Internet Explorer default browsers")</span></span>

    <span data-ttu-id="98c5b-169">*Google Chrome 및 Internet Explorer를 기본 브라우저로*</span><span class="sxs-lookup"><span data-stu-id="98c5b-169">*Google Chrome and Internet Explorer as default browsers*</span></span>

    > [!NOTE]
    > <span data-ttu-id="98c5b-170">기본 브라우저를 구성한 후 브라우저 메뉴에서 **다중 브라우저** 옵션이 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-170">After configuring the default browsers, the **Multiple Browsers** option is selected in the browser menu.</span></span>
    > 
    > <span data-ttu-id="98c5b-171">![여러 브라우저](visual-studio-2013-web-tools/_static/image4.png "여러 브라우저")</span><span class="sxs-lookup"><span data-stu-id="98c5b-171">![Multiple browsers](visual-studio-2013-web-tools/_static/image4.png "Multiple browsers")</span></span>
6. <span data-ttu-id="98c5b-172">**Ctrl** + **f5** 키를 눌러 디버깅 하지 않고 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-172">Press **CTRL** + **F5** to run the application without debugging.</span></span>
7. <span data-ttu-id="98c5b-173">두 브라우저 창이 모두 열려 있는 경우 두 브라우저의 업데이트를 동시에 표시 하기 위해 둘 중 하나를 다른 창 위에 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-173">When both browser windows open, place one of them above the other in order to see the updates on both browsers simultaneously.</span></span> <span data-ttu-id="98c5b-174">브라우저는 밝은 파란색 사각형이 있는 웹 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-174">The browsers should display a web page with a light-blue rectangle.</span></span>

    <span data-ttu-id="98c5b-175">![브라우저 하나에 다른 브라우저 배치](visual-studio-2013-web-tools/_static/image5.png "브라우저 하나에 다른 브라우저 배치")</span><span class="sxs-lookup"><span data-stu-id="98c5b-175">![Placing one browser above the other](visual-studio-2013-web-tools/_static/image5.png "Placing one browser above the other")</span></span>

    <span data-ttu-id="98c5b-176">*브라우저 하나에 다른 브라우저 배치*</span><span class="sxs-lookup"><span data-stu-id="98c5b-176">*Placing one browser above the other*</span></span>
8. <span data-ttu-id="98c5b-177">브라우저를 닫지 마세요.</span><span class="sxs-lookup"><span data-stu-id="98c5b-177">Do not close the browsers.</span></span> <span data-ttu-id="98c5b-178">이러한 작업은 다음 작업에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-178">You will use them in the next task.</span></span>

<a id="Ex1Task2"></a>
#### <a name="task-2---using-zen-coding-to-create-html-elements"></a><span data-ttu-id="98c5b-179">작업 2-Zen 코딩을 사용 하 여 HTML 요소 만들기</span><span class="sxs-lookup"><span data-stu-id="98c5b-179">Task 2 - Using Zen Coding to Create HTML Elements</span></span>

<span data-ttu-id="98c5b-180">**Zen 코딩** 은 고속 HTML, XML, XSL (또는 기타 구조화 된 코드 형식) 코딩 및 편집을 위한 편집기 플러그 인입니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-180">**Zen Coding** is an editor plugin for high-speed HTML, XML, XSL (or any other structured code format) coding and editing.</span></span> <span data-ttu-id="98c5b-181">이 플러그 인의 핵심은 CSS 선택기와 유사한 식 (HTML 코드)을 확장 하는 데 사용할 수 있는 강력한 약어 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-181">The core of this plugin is a powerful abbreviation engine which allows you to expand expressions -similar to CSS selectors- into HTML code.</span></span> <span data-ttu-id="98c5b-182">Zen 코딩은 CSS 스타일 선택기 구문을 사용 하 여 HTML을 신속 하 게 작성 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-182">Zen Coding is a fast way to write HTML using a CSS style selector syntax.</span></span>

<span data-ttu-id="98c5b-183">이 연습에서는 Web Essentials에서 제공 하는 Zen 코딩 기능을 사용 하 여 질문의 옵션을 나타내는 HTML 단추를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-183">In this exercise, you will use the Zen Coding feature provided by Web Essentials to generate the HTML buttons that represent the options of the question.</span></span>

1. <span data-ttu-id="98c5b-184">Visual Studio로 다시 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-184">Switch back to Visual Studio.</span></span>
2. <span data-ttu-id="98c5b-185">**보기** | **홈** 폴더에 있는 **인덱스 cshtml** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-185">Open the **Index.cshtml** file located in the **Views** | **Home** folder.</span></span>
3. <span data-ttu-id="98c5b-186">**&lt;!--TODO:** 다음 코드를 사용 하 여 주석&gt;하 고 **tab**키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-186">Replace the **&lt;!-- TODO: add options here--&gt;** comment with the following code, and press **TAB**.</span></span>

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample1.css)]
4. <span data-ttu-id="98c5b-187">HTML로 코드를 확장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-187">The code should be expanded to HTML.</span></span>

    <span data-ttu-id="98c5b-188">![확장 된 HTML](visual-studio-2013-web-tools/_static/image6.png "확장 된 HTML")</span><span class="sxs-lookup"><span data-stu-id="98c5b-188">![Expanded HTML](visual-studio-2013-web-tools/_static/image6.png "Expanded HTML")</span></span>

    <span data-ttu-id="98c5b-189">*확장 된 HTML*</span><span class="sxs-lookup"><span data-stu-id="98c5b-189">*Expanded HTML*</span></span>

    > [!NOTE]
    > <span data-ttu-id="98c5b-190">Zen 코딩 구문에 대해 자세히 알아보려면 다음 [문서](http://www.johnpapa.net/zen-coding-in-visual-studio-2012/)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="98c5b-190">To learn more about Zen Coding syntax, see the following [article](http://www.johnpapa.net/zen-coding-in-visual-studio-2012/).</span></span>
5. <span data-ttu-id="98c5b-191">두 브라우저를 모두 업데이트 하려면 **연결 된 브라우저 새로 고침** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-191">Click the **Refresh linked browsers** button to update both browsers.</span></span>

    <span data-ttu-id="98c5b-192">![연결 된 브라우저 새로 고침](visual-studio-2013-web-tools/_static/image7.png "연결 된 브라우저 새로 고침")</span><span class="sxs-lookup"><span data-stu-id="98c5b-192">![Refresh linked browsers](visual-studio-2013-web-tools/_static/image7.png "Refresh linked browsers")</span></span>

    <span data-ttu-id="98c5b-193">*연결 된 브라우저 새로 고침*</span><span class="sxs-lookup"><span data-stu-id="98c5b-193">*Refresh linked browsers*</span></span>

    <span data-ttu-id="98c5b-194">![Internet Explorer-4 개의 단추로 업데이트 된 페이지](visual-studio-2013-web-tools/_static/image8.png "Internet Explorer-4 개의 단추로 업데이트 된 페이지")</span><span class="sxs-lookup"><span data-stu-id="98c5b-194">![Internet Explorer - Page updated with four buttons](visual-studio-2013-web-tools/_static/image8.png "Internet Explorer - Page updated with four buttons")</span></span>

    <span data-ttu-id="98c5b-195">*Internet Explorer-4 개의 단추로 업데이트 된 페이지*</span><span class="sxs-lookup"><span data-stu-id="98c5b-195">*Internet Explorer - Page updated with four buttons*</span></span>

    <span data-ttu-id="98c5b-196">![Google Chrome-4 개의 단추로 업데이트 된 페이지](visual-studio-2013-web-tools/_static/image9.png "Google Chrome-4 개의 단추로 업데이트 된 페이지")</span><span class="sxs-lookup"><span data-stu-id="98c5b-196">![Google Chrome - Page updated with four buttons](visual-studio-2013-web-tools/_static/image9.png "Google Chrome - Page updated with four buttons")</span></span>

    <span data-ttu-id="98c5b-197">*Google Chrome-4 개의 단추로 업데이트 된 페이지*</span><span class="sxs-lookup"><span data-stu-id="98c5b-197">*Google Chrome - Page updated with four buttons*</span></span>
6. <span data-ttu-id="98c5b-198">Visual Studio로 다시 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-198">Switch back to Visual Studio.</span></span>
7. <span data-ttu-id="98c5b-199">페이지에 단추를 추가 했지만 여전히 템플릿 질문을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-199">You have added the buttons to the page, but you still need to add a template question.</span></span> <span data-ttu-id="98c5b-200">이렇게 하려면 **Lorem Ipsum generator**라는 웹 Essentials의 새로운 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-200">To do so, you will use a new feature in Web Essentials called **Lorem Ipsum generator**.</span></span> <span data-ttu-id="98c5b-201">**클래스** 특성이 **front**인 **div** 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-201">Locate the **div** element with the **class** attribute **front**.</span></span>
8. <span data-ttu-id="98c5b-202">다음 코드를 **div**의 첫 번째 자식 요소로 추가 하 고 **tab**키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-202">Add the following code as the first child element of the **div**, and press **TAB**.</span></span>

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample2.css)]
9. <span data-ttu-id="98c5b-203">HTML로 코드를 확장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-203">The code should be expanded to HTML.</span></span>

    <span data-ttu-id="98c5b-204">![Lorem Ipsum 자동 생성](visual-studio-2013-web-tools/_static/image10.png "Lorem Ipsum 자동 생성")</span><span class="sxs-lookup"><span data-stu-id="98c5b-204">![Lorem Ipsum autogenerated](visual-studio-2013-web-tools/_static/image10.png "Lorem Ipsum autogenerated")</span></span>

    <span data-ttu-id="98c5b-205">*Lorem Ipsum 자동 생성*</span><span class="sxs-lookup"><span data-stu-id="98c5b-205">*Lorem Ipsum autogenerated*</span></span>

    > [!NOTE]
    > <span data-ttu-id="98c5b-206">Zen 코딩의 일부로 이제 HTML 편집기에서 직접 Lorem Ipsum 코드를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-206">As part of Zen Coding, you can now generate Lorem Ipsum code directly in the HTML editor.</span></span> <span data-ttu-id="98c5b-207">**Lorem** 를 입력 하 고 **TAB** 키를 누르면 30 단어 lorem Ipsum 텍스트가 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-207">Simply type **lorem** and hit **TAB** and a 30 word Lorem Ipsum text will be inserted.</span></span> <span data-ttu-id="98c5b-208">예를 들어</span><span class="sxs-lookup"><span data-stu-id="98c5b-208">E.g.</span></span> <span data-ttu-id="98c5b-209">*lorem10* 는 10 개의 Lorem Ipsum 단어를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-209">*lorem10* inserts 10 Lorem Ipsum words.</span></span>
10. <span data-ttu-id="98c5b-210">**Lorem Pixel generator**라는 웹 Essentials의 또 다른 새로운 기능을 사용 하 여 질문의 맨 위에 로고를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-210">You will add a logo at the top of the question by using another new feature in Web Essentials called **Lorem Pixel generator**.</span></span> <span data-ttu-id="98c5b-211">**컨테이너** 를 **클래스** 값으로 사용 하 여 다음 코드를 **div** 요소의 첫 번째 자식 요소로 추가 하 고 **tab**키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-211">Add the following code as the first child element of the **div** element with **container** as **class** value, and press **TAB**.</span></span>

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample3.css)]
11. <span data-ttu-id="98c5b-212">코드가 HTML로 확장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-212">The code should expand to HTML.</span></span>

    <span data-ttu-id="98c5b-213">![자동 생성 되는 Lorem 픽셀](visual-studio-2013-web-tools/_static/image11.png "자동 생성 되는 Lorem 픽셀")</span><span class="sxs-lookup"><span data-stu-id="98c5b-213">![Lorem Pixel autogenerated](visual-studio-2013-web-tools/_static/image11.png "Lorem Pixel autogenerated")</span></span>

    <span data-ttu-id="98c5b-214">*자동 생성 되는 Lorem 픽셀*</span><span class="sxs-lookup"><span data-stu-id="98c5b-214">*Lorem Pixel autogenerated*</span></span>

    > [!NOTE]
    > <span data-ttu-id="98c5b-215">Zen 코딩의 일부로 HTML 편집기에서 직접 Lorem 픽셀 코드를 생성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-215">As part of Zen Coding, you can also generate Lorem Pixel code directly in the HTML editor.</span></span> <span data-ttu-id="98c5b-216">**200 x 200-동물** 및 적중 **탭** 을 입력 하면 동물의 200 x 200 이미지가 포함 된 **img** 태그가 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-216">Simply type **pix-200x200-animals** and hit **TAB** and an **img** tag with a 200x200 image of an animal will be inserted.</span></span> <span data-ttu-id="98c5b-217">자세한 내용은 [Lorem 픽셀](http://www.lorempixel.com)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="98c5b-217">For more information, refer to [Lorem Pixel](http://www.lorempixel.com).</span></span>
12. <span data-ttu-id="98c5b-218">두 브라우저를 모두 업데이트 하려면 **연결 된 브라우저 새로 고침** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-218">Click the **Refresh linked browsers** button to update both browsers.</span></span>

    <span data-ttu-id="98c5b-219">![Internet Explorer-자동으로 생성 되는 이미지 및 텍스트](visual-studio-2013-web-tools/_static/image12.png "Internet Explorer-자동으로 생성 되는 이미지 및 텍스트")</span><span class="sxs-lookup"><span data-stu-id="98c5b-219">![Internet Explorer - Autogenerated image and text](visual-studio-2013-web-tools/_static/image12.png "Internet Explorer - Autogenerated image and text")</span></span>

    <span data-ttu-id="98c5b-220">*Internet Explorer-자동으로 생성 되는 이미지 및 텍스트*</span><span class="sxs-lookup"><span data-stu-id="98c5b-220">*Internet Explorer - Autogenerated image and text*</span></span>

    <span data-ttu-id="98c5b-221">![Google Chrome-자동으로 생성 되는 이미지 및 텍스트](visual-studio-2013-web-tools/_static/image13.png "Google Chrome-자동으로 생성 되는 이미지 및 텍스트")</span><span class="sxs-lookup"><span data-stu-id="98c5b-221">![Google Chrome - Autogenerated image and text](visual-studio-2013-web-tools/_static/image13.png "Google Chrome - Autogenerated image and text")</span></span>

    <span data-ttu-id="98c5b-222">*Google Chrome-자동으로 생성 되는 이미지 및 텍스트*</span><span class="sxs-lookup"><span data-stu-id="98c5b-222">*Google Chrome - Autogenerated image and text*</span></span>

    > [!NOTE]
    > <span data-ttu-id="98c5b-223">코드 조각을 추가할 때 이미지를 임의로 선택 하므로 브라우저에 표시 되는 이미지는 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-223">Because the image is selected randomly when adding the code snippet, the image shown in the browsers may differ.</span></span>
13. <span data-ttu-id="98c5b-224">브라우저를 닫지 마세요.</span><span class="sxs-lookup"><span data-stu-id="98c5b-224">Do not close the browsers.</span></span> <span data-ttu-id="98c5b-225">이러한 작업은 다음 작업에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-225">You will use them in the next task.</span></span>

<a id="Ex1Task3"></a>
#### <a name="task-3---updating-a-style-property"></a><span data-ttu-id="98c5b-226">작업 3-스타일 속성 업데이트</span><span class="sxs-lookup"><span data-stu-id="98c5b-226">Task 3 - Updating a Style Property</span></span>

<span data-ttu-id="98c5b-227">이 작업에서는 브라우저 링크의 **검사 모드** 기능을 사용 하 여 특정 DOM 요소가 생성 되는 정확한 위치를 검색 한 다음 Web Essentials에서 제공 하는 색 선택기를 사용 하 여 해당 요소의 color 속성을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-227">In this task, you will use the Browser Link's **Inspect Mode** feature to detect the exact location where the specific DOM element is generated and then update the color property of that element using a color picker provided by Web Essentials.</span></span>

1. <span data-ttu-id="98c5b-228">Internet Explorer 브라우저에서 Alt **키를 눌러 검사** 모드를 **사용 하도록 설정 하려면** **ALT** +  + 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-228">In the Internet Explorer browser, press **CTRL** + **ALT** + **I** to enable Inspect Mode.</span></span>
2. <span data-ttu-id="98c5b-229">연한 파란색 테두리 위로 포인터를 이동 하 고를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-229">Move the pointer over the light blue border and click.</span></span>

    <span data-ttu-id="98c5b-230">![연한 파란색 테두리 위로 포인터 이동](visual-studio-2013-web-tools/_static/image14.png "연한 파란색 테두리 위로 포인터 이동")</span><span class="sxs-lookup"><span data-stu-id="98c5b-230">![Moving the pointer over the light blue border](visual-studio-2013-web-tools/_static/image14.png "Moving the pointer over the light blue border")</span></span>

    <span data-ttu-id="98c5b-231">*연한 파란색 테두리 위로 포인터 이동*</span><span class="sxs-lookup"><span data-stu-id="98c5b-231">*Moving the pointer over the light blue border*</span></span>
3. <span data-ttu-id="98c5b-232">Visual Studio로 다시 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-232">Switch back to Visual Studio.</span></span> <span data-ttu-id="98c5b-233">브라우저에서 선택한 HTML 요소가 Visual Studio HTML 편집기 에서도 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-233">Notice how the HTML element that you selected in the browser is also selected in the Visual Studio HTML editor.</span></span>

    <span data-ttu-id="98c5b-234">![Visual Studio HTML 편집기에서 선택 된 HTML 요소](visual-studio-2013-web-tools/_static/image15.png "Visual Studio HTML 편집기에서 선택 된 HTML 요소")</span><span class="sxs-lookup"><span data-stu-id="98c5b-234">![HTML element selected in the Visual Studio HTML editor](visual-studio-2013-web-tools/_static/image15.png "HTML element selected in the Visual Studio HTML editor")</span></span>

    <span data-ttu-id="98c5b-235">*Visual Studio HTML 편집기에서 선택 된 HTML 요소*</span><span class="sxs-lookup"><span data-stu-id="98c5b-235">*HTML element selected in the Visual Studio HTML editor*</span></span>
4. <span data-ttu-id="98c5b-236">이제 선택한 요소의 스타일을 변경 하기 위해 **front** CSS 클래스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-236">You will now update the **front** CSS class in order to change the styling of the selected element.</span></span> <span data-ttu-id="98c5b-237">이렇게 하려면 **CTRL** + **를** 눌러 검색 **탐색** 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-237">To do so, press **CTRL** + **,** to open the **Navigate To** search box.</span></span> <span data-ttu-id="98c5b-238">**Site .css** 를 입력 하 고 **enter** 키를 눌러 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-238">Type **site.css** and press **ENTER** to open the file.</span></span>

    <span data-ttu-id="98c5b-239">![파일 사이트 .css를 여는 경우](visual-studio-2013-web-tools/_static/image16.png "파일 사이트 .css를 여는 경우")</span><span class="sxs-lookup"><span data-stu-id="98c5b-239">![Opening file Site.css](visual-studio-2013-web-tools/_static/image16.png "Opening file Site.css")</span></span>

    <span data-ttu-id="98c5b-240">*파일 사이트 .css를 여는 경우*</span><span class="sxs-lookup"><span data-stu-id="98c5b-240">*Opening file Site.css*</span></span>
5. <span data-ttu-id="98c5b-241">**Ctrl** + **F** 를 누르고 **. 대칭 이동-container.** 를 입력 하 여 CSS 선택기를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-241">Press **CTRL** + **F** and type **.flip-container .front** to find the CSS selector.</span></span>
6. <span data-ttu-id="98c5b-242">클래스의 border 속성에서 연한 파란색 사각형을 클릭 하 여 색 선택기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-242">Click the light blue square in the border property of the class to open the Color Picker.</span></span>

    <span data-ttu-id="98c5b-243">![색 선택 열기](visual-studio-2013-web-tools/_static/image17.png "색 선택 열기")</span><span class="sxs-lookup"><span data-stu-id="98c5b-243">![Opening the Color Picker](visual-studio-2013-web-tools/_static/image17.png "Opening the Color Picker")</span></span>

    <span data-ttu-id="98c5b-244">*색 선택 열기*</span><span class="sxs-lookup"><span data-stu-id="98c5b-244">*Opening the Color Picker*</span></span>
7. <span data-ttu-id="98c5b-245">펼침 단추를 클릭 하 여 색 선택기를 확장 하 고 새 색을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-245">Expand the Color Picker by clicking the chevron button and select a new color.</span></span>

    <span data-ttu-id="98c5b-246">![색 선택 확장](visual-studio-2013-web-tools/_static/image18.png "색 선택 확장")</span><span class="sxs-lookup"><span data-stu-id="98c5b-246">![Expanding the Color Picker](visual-studio-2013-web-tools/_static/image18.png "Expanding the Color Picker")</span></span>

    <span data-ttu-id="98c5b-247">*색 선택 확장*</span><span class="sxs-lookup"><span data-stu-id="98c5b-247">*Expanding the Color Picker*</span></span>
8. <span data-ttu-id="98c5b-248">**Ctrl** + **alt** \*\* + 를\*\* 눌러 연결 된 브라우저를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-248">Press **CTRL** + **ALT** + **ENTER** to refresh linked browsers.</span></span>
9. <span data-ttu-id="98c5b-249">Internet Explorer로 전환 하 고 테두리 색이 변경 된 방식을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-249">Switch to Internet Explorer and notice how the color of the border has changed.</span></span>

    <span data-ttu-id="98c5b-250">![Internet Explorer-테두리 색이 업데이트 됨](visual-studio-2013-web-tools/_static/image19.png "Internet Explorer-테두리 색이 업데이트 됨")</span><span class="sxs-lookup"><span data-stu-id="98c5b-250">![Internet Explorer - Border color updated](visual-studio-2013-web-tools/_static/image19.png "Internet Explorer - Border color updated")</span></span>

    <span data-ttu-id="98c5b-251">*Internet Explorer-테두리 색이 업데이트 됨*</span><span class="sxs-lookup"><span data-stu-id="98c5b-251">*Internet Explorer - Border color updated*</span></span>
10. <span data-ttu-id="98c5b-252">Google Chrome으로 전환 하 고 테두리 색이 변경 된 방식을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-252">Switch to Google Chrome and notice how the color of the border has changed.</span></span>

    <span data-ttu-id="98c5b-253">![Google Chrome-테두리 색이 업데이트 됨](visual-studio-2013-web-tools/_static/image20.png "Google Chrome-테두리 색이 업데이트 됨")</span><span class="sxs-lookup"><span data-stu-id="98c5b-253">![Google Chrome - Border color updated](visual-studio-2013-web-tools/_static/image20.png "Google Chrome - Border color updated")</span></span>

    <span data-ttu-id="98c5b-254">*Google Chrome-테두리 색이 업데이트 됨*</span><span class="sxs-lookup"><span data-stu-id="98c5b-254">*Google Chrome - Border color updated*</span></span>
11. <span data-ttu-id="98c5b-255">Visual Studio로 다시 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-255">Switch back to Visual Studio.</span></span>
12. <span data-ttu-id="98c5b-256">**Btn** 선택기를 찾으려면 **Site .css** 파일의 끝으로 이동 하 고 **CTRL** + **F** 를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-256">Go to the end of the **Site.css** file and press **CTRL** + **F** to locate the **.btn** selector.</span></span>
13. <span data-ttu-id="98c5b-257">**-Webkit** 속성은 녹색으로 밑줄이 그어집니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-257">Notice that the **-webkit-border-radius** property is underlined in green.</span></span>

    <span data-ttu-id="98c5b-258">![-webkit-btn selector의 radius 속성](visual-studio-2013-web-tools/_static/image21.png "-webkit-btn selector의 radius 속성")</span><span class="sxs-lookup"><span data-stu-id="98c5b-258">![-webkit-border-radius property of the btn selector](visual-studio-2013-web-tools/_static/image21.png "-webkit-border-radius property of the btn selector")</span></span>

    <span data-ttu-id="98c5b-259">*-webkit-btn selector의 radius 속성*</span><span class="sxs-lookup"><span data-stu-id="98c5b-259">*-webkit-border-radius property of the btn selector*</span></span>
14. <span data-ttu-id="98c5b-260">**-Webkit** 속성에 캐럿을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-260">Place the caret in the **-webkit-border-radius** property.</span></span> <span data-ttu-id="98c5b-261">속성의 첫 번째 단어의 첫 문자 아래에 파란색 선이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-261">A blue line should appear under the first letter of the first word of the property.</span></span> <span data-ttu-id="98c5b-262">**스마트 태그**입니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-262">This is the **smart tag**.</span></span>
15. <span data-ttu-id="98c5b-263">**Ctrl** + 를 누릅니다 **.**</span><span class="sxs-lookup"><span data-stu-id="98c5b-263">Press **CTRL** + **.**</span></span> <span data-ttu-id="98c5b-264">제안 메뉴를 열고 **누락 된 표준 속성 추가 (테두리-반경)** 를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-264">to open the suggestions menu and click **Add missing standard property (border-radius)**.</span></span>

    <span data-ttu-id="98c5b-265">![누락 된 표준 속성 제안 추가](visual-studio-2013-web-tools/_static/image22.png "누락 된 표준 속성 제안 추가")</span><span class="sxs-lookup"><span data-stu-id="98c5b-265">![Add missing standard property suggestion](visual-studio-2013-web-tools/_static/image22.png "Add missing standard property suggestion")</span></span>

    <span data-ttu-id="98c5b-266">*누락 된 표준 속성 제안 추가*</span><span class="sxs-lookup"><span data-stu-id="98c5b-266">*Add missing standard property suggestion*</span></span>
16. <span data-ttu-id="98c5b-267">**테두리-반경** 속성은 CSS 규칙에 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-267">The **border-radius** property is automatically added to the CSS rule.</span></span>

    <span data-ttu-id="98c5b-268">![누락 된 표준 속성 추가 됨](visual-studio-2013-web-tools/_static/image23.png "누락 된 표준 속성 추가 됨")</span><span class="sxs-lookup"><span data-stu-id="98c5b-268">![Missing standard property added](visual-studio-2013-web-tools/_static/image23.png "Missing standard property added")</span></span>

    <span data-ttu-id="98c5b-269">*누락 된 표준 속성 추가 됨*</span><span class="sxs-lookup"><span data-stu-id="98c5b-269">*Missing standard property added*</span></span>
17. <span data-ttu-id="98c5b-270">포인터를 **테두리-radius** 속성 위로 이동 하 여 **브라우저 매트릭스 도구 설명을**표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-270">Move the pointer over the **border-radius** property to display the **Browser matrix tooltip**.</span></span> <span data-ttu-id="98c5b-271">**브라우저 매트릭스 도구 설명** 에는 각 브라우저에서 속성의 가용성이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-271">The **Browser matrix tooltip** shows the availability of the property in each browser.</span></span>

    <span data-ttu-id="98c5b-272">![브라우저 매트릭스 도구 설명](visual-studio-2013-web-tools/_static/image24.png "브라우저 매트릭스 도구 설명")</span><span class="sxs-lookup"><span data-stu-id="98c5b-272">![Browser matrix tooltip](visual-studio-2013-web-tools/_static/image24.png "Browser matrix tooltip")</span></span>

    <span data-ttu-id="98c5b-273">*브라우저 매트릭스 도구 설명*</span><span class="sxs-lookup"><span data-stu-id="98c5b-273">*Browser matrix tooltip*</span></span>
18. <span data-ttu-id="98c5b-274">**테두리-반경** 속성의 값은 여전히 밑줄이 그어집니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-274">Notice that the value of the **border-radius** property is still underlined.</span></span> <span data-ttu-id="98c5b-275">포인터를 값 위로 이동 하 여 경고 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-275">Move the pointer over the value to see the warning message.</span></span>

    <span data-ttu-id="98c5b-276">![테두리-반지름 속성 값 경고](visual-studio-2013-web-tools/_static/image25.png "테두리-반지름 속성 값 경고")</span><span class="sxs-lookup"><span data-stu-id="98c5b-276">![Border-radius property value warning](visual-studio-2013-web-tools/_static/image25.png "Border-radius property value warning")</span></span>

    <span data-ttu-id="98c5b-277">*테두리-반지름 속성 값 경고*</span><span class="sxs-lookup"><span data-stu-id="98c5b-277">*Border-radius property value warning*</span></span>
19. <span data-ttu-id="98c5b-278">도구 설명에서 제안 하는 대로 **테두리-반지름** 속성 값의 단위를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-278">Remove the unit of the **border-radius** property value as suggested by the tooltip.</span></span>
20. <span data-ttu-id="98c5b-279">**테두리 반경** 은 테두리 모퉁이가 둥근 정도를 정의 하는 표준 속성입니다. CSS 규칙에서 **-webkit** 속성 및 값을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-279">As **border-radius** is the standard property for defining how rounded border corners are, you can remove the **-webkit-border-radius** property and value from the CSS rule.</span></span>
21. <span data-ttu-id="98c5b-280">**단어 줄 바꿈** 속성에 캐럿을 배치 하 고 스마트 태그가 아래에도 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-280">Place the caret in the **word-wrap** property and notice that the smart tag also appears below.</span></span>
22. <span data-ttu-id="98c5b-281">메뉴를 열고 누락 된 **공급 업체 특성 추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-281">Open the menu and click **Add missing vendor specifics**.</span></span>

    <span data-ttu-id="98c5b-282">![누락 된 공급 업체 세부 제안 추가](visual-studio-2013-web-tools/_static/image26.png "누락 된 공급 업체 세부 제안 추가")</span><span class="sxs-lookup"><span data-stu-id="98c5b-282">![Add missing vendor specifics suggestion](visual-studio-2013-web-tools/_static/image26.png "Add missing vendor specifics suggestion")</span></span>

    <span data-ttu-id="98c5b-283">*누락 된 공급 업체 세부 제안 추가*</span><span class="sxs-lookup"><span data-stu-id="98c5b-283">*Add missing vendor specifics suggestion*</span></span>
23. <span data-ttu-id="98c5b-284">**---단어 래핑** 속성은 CSS 규칙에 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-284">The **-ms-word-wrap** property is automatically added to the CSS rule.</span></span>

    <span data-ttu-id="98c5b-285">![공급 업체별 속성 추가 됨](visual-studio-2013-web-tools/_static/image27.png "공급 업체별 속성 추가 됨")</span><span class="sxs-lookup"><span data-stu-id="98c5b-285">![Vendor specific property added](visual-studio-2013-web-tools/_static/image27.png "Vendor specific property added")</span></span>

    <span data-ttu-id="98c5b-286">*공급 업체별 속성 추가 됨*</span><span class="sxs-lookup"><span data-stu-id="98c5b-286">*Vendor specific property added*</span></span>

<a id="Ex1Task4"></a>
#### <a name="task-4---updating-the-html-code-from-the-browser"></a><span data-ttu-id="98c5b-287">작업 4-브라우저에서 HTML 코드 업데이트</span><span class="sxs-lookup"><span data-stu-id="98c5b-287">Task 4 - Updating the HTML Code from the Browser</span></span>

<span data-ttu-id="98c5b-288">이 작업에서는 브라우저 링크의 **디자인 모드** 기능을 사용 하 여 브라우저에서 DOM 개체를 편집 하 고 Visual STUDIO의 HTML 소스 파일에 변경 내용을 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-288">In this task, you will use the Browser Link's **Design Mode** feature to edit the DOM object from the browser and transfer the changes to the HTML source file in Visual Studio.</span></span>

1. <span data-ttu-id="98c5b-289">Google Chrome에서 **ctrl** + **alt** + **D** 를 눌러 디자인 모드를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-289">In Google Chrome, press **CTRL** + **ALT** + **D** to enable Design Mode.</span></span>
2. <span data-ttu-id="98c5b-290">포인터를 **Lorem Ipsum dolor sit amet** 레이블 위로 이동 하 고를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-290">Move the pointer over the **Lorem Ipsum dolor sit amet** label and click.</span></span>

    <span data-ttu-id="98c5b-291">![질문 편집](visual-studio-2013-web-tools/_static/image28.png "질문 편집")</span><span class="sxs-lookup"><span data-stu-id="98c5b-291">![Editing the question](visual-studio-2013-web-tools/_static/image28.png "Editing the question")</span></span>

    <span data-ttu-id="98c5b-292">*질문 편집*</span><span class="sxs-lookup"><span data-stu-id="98c5b-292">*Editing the question*</span></span>
3. <span data-ttu-id="98c5b-293">커서가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-293">A cursor should appear.</span></span> <span data-ttu-id="98c5b-294">*더 긴 질문을 작성할 때*원래 텍스트를 어떻게 표시 되는지 바꾸고 **ESC** 키를 눌러 디자인 모드를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-294">Replace the original text with *What does it look like when I write a longer question?*, and then press **ESC** to exit Design Mode.</span></span>

    <span data-ttu-id="98c5b-295">![수정한 질문](visual-studio-2013-web-tools/_static/image29.png "수정한 질문")</span><span class="sxs-lookup"><span data-stu-id="98c5b-295">![Question edited](visual-studio-2013-web-tools/_static/image29.png "Question edited")</span></span>

    <span data-ttu-id="98c5b-296">*수정한 질문*</span><span class="sxs-lookup"><span data-stu-id="98c5b-296">*Question edited*</span></span>
4. <span data-ttu-id="98c5b-297">아직 열지 않은 경우 Visual Studio로 다시 전환 하 고, **Index. cshtml**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-297">Switch back to Visual Studio and open **Index.cshtml**, if not already opened.</span></span> <span data-ttu-id="98c5b-298">**&lt;p&gt;** 요소의 내부 텍스트가 업데이트 된 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-298">Notice that the inner text of the **&lt;p&gt;** element has been updated.</span></span>

    <span data-ttu-id="98c5b-299">![HTML 페이지의 업데이트 된 질문](visual-studio-2013-web-tools/_static/image30.png "HTML 페이지의 업데이트 된 질문")</span><span class="sxs-lookup"><span data-stu-id="98c5b-299">![Updated question in the HTML page](visual-studio-2013-web-tools/_static/image30.png "Updated question in the HTML page")</span></span>

    <span data-ttu-id="98c5b-300">*HTML 페이지의 업데이트 된 질문*</span><span class="sxs-lookup"><span data-stu-id="98c5b-300">*Updated question in the HTML page*</span></span>

<a id="Ex1Task5"></a>
#### <a name="task-5---reviewing-seo-related-warnings"></a><span data-ttu-id="98c5b-301">작업 5-SEO 관련 경고 검토</span><span class="sxs-lookup"><span data-stu-id="98c5b-301">Task 5 - Reviewing SEO Related Warnings</span></span>

<span data-ttu-id="98c5b-302">SEO ( **검색 엔진 최적화** )는 검색 엔진의 결과 목록에서 웹 사이트 순위를 높게 만드는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-302">**Search Engine Optimization** (SEO) is the process of making a website rank higher on a search engine's list of results.</span></span> <span data-ttu-id="98c5b-303">사이트 순위가 높을수록 더 일관 되 게 표시 되는 사이트의 방문자가 검색 엔진에서 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-303">The higher the site ranks and the more consistently it is listed, the more visitors the site will get from that search engine.</span></span> <span data-ttu-id="98c5b-304">Web Essentials는 HTML을 검사 하 고 발견 된 문제를 보고 하 고 문제를 해결 하기 위한 지원을 제공 하는 분석 도구를 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-304">Web Essentials incorporates an analytical tool that examines HTML, reports the issues found and provides assistance to fix them.</span></span>

1. <span data-ttu-id="98c5b-305">**보기** 메뉴로 이동 하 고 **오류 목록** 를 클릭 하 여 **오류 목록** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-305">Go to the **View** menu and click **Error List** to open the **Error List** window.</span></span>

    <span data-ttu-id="98c5b-306">![보기 메뉴의 오류 목록](visual-studio-2013-web-tools/_static/image31.png "보기 메뉴의 오류 목록")</span><span class="sxs-lookup"><span data-stu-id="98c5b-306">![Error List in View menu](visual-studio-2013-web-tools/_static/image31.png "Error List in View menu")</span></span>

    <span data-ttu-id="98c5b-307">*보기 메뉴의 오류 목록*</span><span class="sxs-lookup"><span data-stu-id="98c5b-307">*Error List in View menu*</span></span>
2. <span data-ttu-id="98c5b-308">페이지 설명에 대 한 **&lt;meta&gt;** 태그가 없음을 알리는 SEO 경고가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-308">Notice that there is an SEO warning notifying that a **&lt;meta&gt;** tag for the page description is missing.</span></span> <span data-ttu-id="98c5b-309">SEO 경고 항목을 두 번 클릭 하 여 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-309">Double-click the SEO warning entry to fix it.</span></span>

    <span data-ttu-id="98c5b-310">![오류 목록 창](visual-studio-2013-web-tools/_static/image32.png "오류 목록 창")</span><span class="sxs-lookup"><span data-stu-id="98c5b-310">![Error List window](visual-studio-2013-web-tools/_static/image32.png "Error List window")</span></span>

    <span data-ttu-id="98c5b-311">*오류 목록 창*</span><span class="sxs-lookup"><span data-stu-id="98c5b-311">*Error List window*</span></span>
3. <span data-ttu-id="98c5b-312">**Web Essentials** 대화 상자에서 **예** 를 클릭 하 여 메타&gt; 태그 &lt;설명을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-312">In the **Web Essentials** dialog box, click **Yes** to insert a description &lt;meta&gt; tag.</span></span>

    <span data-ttu-id="98c5b-313">![Web Essentials 대화 상자](visual-studio-2013-web-tools/_static/image33.png "Web Essentials 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="98c5b-313">![Web Essentials dialog box](visual-studio-2013-web-tools/_static/image33.png "Web Essentials dialog box")</span></span>

    <span data-ttu-id="98c5b-314">*Web Essentials 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="98c5b-314">*Web Essentials dialog box*</span></span>
4. <span data-ttu-id="98c5b-315">**\_레이아웃** 에 대 한 편집기가 열리고 **&lt;META&gt;** 태그가 HTML 파일의 **head** 섹션에 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-315">The editor for **\_Layout.cshtml** opens and the **&lt;meta&gt;** tag is automatically added to the **head** section of the HTML file.</span></span>

    <span data-ttu-id="98c5b-316">![_Layout 페이지에 자동으로 추가 되는 메타 태그](visual-studio-2013-web-tools/_static/image34.png "_Layout 페이지에 자동으로 추가 되는 메타 태그")</span><span class="sxs-lookup"><span data-stu-id="98c5b-316">![Meta tag automatically added in _Layout page](visual-studio-2013-web-tools/_static/image34.png "Meta tag automatically added in _Layout page")</span></span>

    <span data-ttu-id="98c5b-317">*\_레이아웃 페이지에 메타 태그가 자동으로 추가 됨*</span><span class="sxs-lookup"><span data-stu-id="98c5b-317">*Meta tag automatically added to \_Layout page*</span></span>
5. <span data-ttu-id="98c5b-318">**Content** 특성의 값을 *GeekQuiz* 로 변경 하 고 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-318">Change the value of the **content** attribute to *GeekQuiz* and save the file.</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-taking-advantage-of-code-snippets-and-intellisense"></a><span data-ttu-id="98c5b-319">연습 2: 코드 조각 및 IntelliSense 활용</span><span class="sxs-lookup"><span data-stu-id="98c5b-319">Exercise 2: Taking Advantage of Code Snippets and IntelliSense</span></span>

<span data-ttu-id="98c5b-320">Web Essentials를 사용 하 여 HTML 편집기는 추가 기능으로 확장 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-320">With Web Essentials, the HTML editor has been extended with extra functionality.</span></span> <span data-ttu-id="98c5b-321">이 연습에서는 웹 응용 프로그램을 개발할 때 도움이 되는 몇 가지 새로운 기능을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-321">In this exercise, you will see some new features that are helpful when developing web applications.</span></span>

<a id="Ex2Task1"></a>
#### <a name="task-1---using-intellisense-in-html-documents"></a><span data-ttu-id="98c5b-322">작업 1-HTML 문서에서 IntelliSense 사용</span><span class="sxs-lookup"><span data-stu-id="98c5b-322">Task 1 - Using IntelliSense in HTML Documents</span></span>

<span data-ttu-id="98c5b-323">이 작업에 표시 되는 첫 번째 새 기능은 **동적 IntelliSense**라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-323">The first new feature you will see in this task is called **Dynamic IntelliSense**.</span></span> <span data-ttu-id="98c5b-324">동적 IntelliSense는 다른 태그 및 특성을 읽어 사용할 수 있는 id를 유추 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-324">Dynamic IntelliSense reads other tags and attributes to infer the possible ids you will use.</span></span>

<span data-ttu-id="98c5b-325">이 작업에서는 레이블과 입력 필드를 포함 하는 새 HTML 폼 요소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-325">In this task, you will create a new HTML form element which contains a label and an input field.</span></span> <span data-ttu-id="98c5b-326">그런 다음 레이블에 **대 한** 특성을 추가 하 여 입력에 바인딩합니다. 범위에 있는 입력의 id를 기반으로 IntelliSense 제안이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-326">Then you will add a **for** attribute to the label to bind it to the input, and you will see IntelliSense suggestions based on the ids of the inputs in scope.</span></span>

1. <span data-ttu-id="98c5b-327">**웹에 대해 Visual Studio Express 2013** 을 열고 **Source/Ex2-TakingAdvantageofCodeSnippetsandIntelliSense/begin** 폴더에 있는 **시작 .sln** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-327">Open **Visual Studio Express 2013 for Web** and the **Begin.sln** solution located in the **Source/Ex2-TakingAdvantageofCodeSnippetsandIntelliSense/Begin** folder.</span></span> <span data-ttu-id="98c5b-328">또는 이전 연습에서 얻은 솔루션을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-328">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>
2. <span data-ttu-id="98c5b-329">**솔루션 탐색기**에서 **보기** | **홈** 폴더에 있는 **인덱스 cshtml** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-329">In **Solution Explorer**, open the **Index.cshtml** file located in the **Views** | **Home** folder.</span></span>
3. <span data-ttu-id="98c5b-330">**&lt;section&gt;** 요소 안에 다음 폼을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-330">Add the following form inside the **&lt;section&gt;** element.</span></span>

    <span data-ttu-id="98c5b-331">(코드 조각- *VisualStudio2013WebTooling* - *Ex2* - *양식*)</span><span class="sxs-lookup"><span data-stu-id="98c5b-331">(Code Snippet - *VisualStudio2013WebTooling* - *Ex2* - *Form*)</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample4.html)]
4. <span data-ttu-id="98c5b-332">입력 태그 앞에는 필드에 대 한 설명이 포함 된 레이블 앞에와 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-332">The input tag should be preceded by a label with some description of the field.</span></span> <span data-ttu-id="98c5b-333">입력 태그 앞에 다음 레이블을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-333">Add the following label before the input tag.</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample5.html)]
5. <span data-ttu-id="98c5b-334">**&lt;레이블의** **for** 특성&gt;레이블이 바인딩되는 폼 요소를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-334">The **for** attribute of a **&lt;label&gt;** specifies which form element a label is bound to.</span></span> <span data-ttu-id="98c5b-335">특성의 값은 관련 된 요소의 id와 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-335">The attribute's value should be equal to the id of the related element.</span></span> <span data-ttu-id="98c5b-336">**For** 특성을 **&lt;label&gt;** 요소에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-336">Add the **for** attribute to the **&lt;label&gt;** element.</span></span> <span data-ttu-id="98c5b-337">다음 그림에 표시 된 것 처럼 &quot;이름&quot; 값은 동일한 범위 (바깥쪽 **&lt;폼&gt;** ) 내의 요소 id를 기준으로 IntelliSense 상자에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-337">As shown in the following figure, the &quot;name&quot; value pops up in the IntelliSense box, based on the id of the elements within the same scope (the enclosing **&lt;form&gt;**).</span></span>

    <span data-ttu-id="98c5b-338">![IntelliSense에서 id 표시](visual-studio-2013-web-tools/_static/image35.png "IntelliSense에서 id 표시")</span><span class="sxs-lookup"><span data-stu-id="98c5b-338">![Showing the id in IntelliSense](visual-studio-2013-web-tools/_static/image35.png "Showing the id in IntelliSense")</span></span>

    <span data-ttu-id="98c5b-339">*IntelliSense에서 id 표시*</span><span class="sxs-lookup"><span data-stu-id="98c5b-339">*Showing the id in IntelliSense*</span></span>
6. <span data-ttu-id="98c5b-340">최근 추가 된 **&lt;폼&gt;** 요소 및 해당 콘텐츠를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-340">Delete the recently added **&lt;form&gt;** element and its content.</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2---using-html-code-snippets"></a><span data-ttu-id="98c5b-341">작업 2-HTML 코드 조각 사용</span><span class="sxs-lookup"><span data-stu-id="98c5b-341">Task 2 - Using HTML Code Snippets</span></span>

<span data-ttu-id="98c5b-342">HTML5에는 25 개가 넘는 새 의미 태그가 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-342">HTML5 introduced more than 25 new semantic tags.</span></span> <span data-ttu-id="98c5b-343">Visual Studio에는 이러한 태그에 대 한 IntelliSense 지원이 이미 있지만 Visual Studio 2013 새 코드 조각을 추가 하 여 더 빠르고 쉽게 태그를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-343">Visual Studio already had IntelliSense support for these tags, but Visual Studio 2013 makes it faster and easier to write markup by adding new code snippets.</span></span> <span data-ttu-id="98c5b-344">이러한 태그는 복잡 하지 않지만 *오디오* 태그에 대 한 올바른 코덱 대체를 추가 하는 것과 같이 몇 가지 사소한 미묘한와 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-344">Though these tags are not complicated, they come with a few small subtleties, such as adding the correct codec fallbacks for the *audio* tag.</span></span> <span data-ttu-id="98c5b-345">이 작업에서는 audio 태그에 대 한 HTML 코드 조각이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-345">In this task, you will see the HTML code snippets for the audio tag.</span></span>

1. <span data-ttu-id="98c5b-346">Aud 파일에서 다음 그림에 표시 된 것 처럼 **&lt;섹션&gt;** 요소 내부에 **&lt;** 을 **입력 합니다.**</span><span class="sxs-lookup"><span data-stu-id="98c5b-346">In the **Index.cshtml** file, type **&lt;aud** inside the **&lt;section&gt;** element as shown in the following figure.</span></span>

    <span data-ttu-id="98c5b-347">![Audio 요소 삽입](visual-studio-2013-web-tools/_static/image36.png "Audio 요소 삽입")</span><span class="sxs-lookup"><span data-stu-id="98c5b-347">![Inserting an audio element](visual-studio-2013-web-tools/_static/image36.png "Inserting an audio element")</span></span>

    <span data-ttu-id="98c5b-348">*Audio 요소 삽입*</span><span class="sxs-lookup"><span data-stu-id="98c5b-348">*Inserting an audio element*</span></span>
2. <span data-ttu-id="98c5b-349">**Tab** 키를 두 번 눌러 다음 코드가 페이지에 추가 되 고 커서가 첫 번째 소스의 **src** 특성에 배치 되는 방식을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-349">Press **TAB** twice and notice how the following code is added on the page and the cursor is placed on the **src** attribute of the first source.</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample6.html)]

    > [!NOTE]
    > <span data-ttu-id="98c5b-350">**TAB** 키를 두 번 누르면 코드 조각이 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-350">By pressing the **TAB** key twice, the code snippet is inserted.</span></span> <span data-ttu-id="98c5b-351">오디오 조각은 지원 향상을 위한 두 개의 소스 파일과 함께 *오디오* 태그의 표준 사용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-351">The audio snippet shows the standard usage of the *audio* tag, with two source files for improved support.</span></span>
3. <span data-ttu-id="98c5b-352">WebCampsTV Katana show: [http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3](http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3)에 대 한 다음 링크를 사용 하 여 두 번째 줄을 삭제 하 고 첫 번째 줄의 소스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-352">Delete the second line and update the source of the first line with the following link to the WebCampsTV Katana show: [http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3](http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3).</span></span> <span data-ttu-id="98c5b-353">결과 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-353">The resulting code is shown below.</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample7.html)]

    > [!NOTE]
    > <span data-ttu-id="98c5b-354">원본 파일 *KatanaProject. mp3* 를 예로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-354">The source file *KatanaProject.mp3* is used as an example.</span></span> <span data-ttu-id="98c5b-355">원하는 경우 다른 원본을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-355">You can use another source if you prefer.</span></span>
4. <span data-ttu-id="98c5b-356">**Ctrl** + **S** 를 눌러 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-356">Press **CTRL** + **S** to save the file.</span></span>
5. <span data-ttu-id="98c5b-357">**Ctrl** + **f5** 키를 눌러 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-357">Press **CTRL** + **F5** to start the application.</span></span>
6. <span data-ttu-id="98c5b-358">오디오 플레이어가 응용 프로그램에 추가 되었음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-358">Notice that an audio player was added to the application.</span></span>

    <span data-ttu-id="98c5b-359">![Internet Explorer의 오디오 플레이어](visual-studio-2013-web-tools/_static/image37.png "Internet Explorer의 오디오 플레이어")</span><span class="sxs-lookup"><span data-stu-id="98c5b-359">![Audio player in Internet Explorer](visual-studio-2013-web-tools/_static/image37.png "Audio player in Internet Explorer")</span></span>

    <span data-ttu-id="98c5b-360">*Internet Explorer의 오디오 플레이어*</span><span class="sxs-lookup"><span data-stu-id="98c5b-360">*Audio player in Internet Explorer*</span></span>

    <span data-ttu-id="98c5b-361">![Google Chrome의 오디오 플레이어](visual-studio-2013-web-tools/_static/image38.png "Google Chrome의 오디오 플레이어")</span><span class="sxs-lookup"><span data-stu-id="98c5b-361">![Audio player in Google Chrome](visual-studio-2013-web-tools/_static/image38.png "Audio player in Google Chrome")</span></span>

    <span data-ttu-id="98c5b-362">*Google Chrome의 오디오 플레이어*</span><span class="sxs-lookup"><span data-stu-id="98c5b-362">*Audio player in Google Chrome*</span></span>
7. <span data-ttu-id="98c5b-363">브라우저를 닫지 마세요.</span><span class="sxs-lookup"><span data-stu-id="98c5b-363">Do not close the browsers.</span></span> <span data-ttu-id="98c5b-364">이러한 작업은 다음 작업에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-364">You will use them in the next task.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3---using-intellisense-in-javascript-documents"></a><span data-ttu-id="98c5b-365">작업 3-JavaScript 문서에서 IntelliSense 사용</span><span class="sxs-lookup"><span data-stu-id="98c5b-365">Task 3 - Using IntelliSense in JavaScript Documents</span></span>

<span data-ttu-id="98c5b-366">Web Essentials 2013를 사용 하는 경우 스타일 시트와 HTML 페이지는 Id 및 클래스 이름 목록을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-366">With Web Essentials 2013, style sheets and HTML pages produce a list of IDs and class names.</span></span> <span data-ttu-id="98c5b-367">이 작업에서는 이러한 목록이 Web Essentials 2013에서 JavaScript IntelliSense 지원을 개선 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-367">In this task, you will learn how those lists improve JavaScript IntelliSense support in Web Essentials 2013.</span></span>

1. <span data-ttu-id="98c5b-368">**Index cshtml** 파일에서 다음 코드를 추가 하 여 JavaScript 코드에 대 한 **스크립트** 태그를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-368">In the **Index.cshtml** file, add the following code to define a **script** tag for JavaScript code.</span></span>

    [!code-cshtml[Main](visual-studio-2013-web-tools/samples/sample8.cshtml)]
2. <span data-ttu-id="98c5b-369">**스크립트** 태그 내에 다음 코드를 추가 하 여 준비 된 콜백 함수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-369">Add the following code inside the **script** tag to define the ready callback function.</span></span>

    <span data-ttu-id="98c5b-370">(코드 조각- *VisualStudio2013WebTooling* - *Ex2* - *ReadyFunction*)</span><span class="sxs-lookup"><span data-stu-id="98c5b-370">(Code Snippet - *VisualStudio2013WebTooling* - *Ex2* - *ReadyFunction*)</span></span>

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample9.js)]
3. <span data-ttu-id="98c5b-371">**스크립트** 태그에 캐럿을 추가 하 고 **ctrl** + 를 누릅니다 **.**</span><span class="sxs-lookup"><span data-stu-id="98c5b-371">Place the caret in the **script** tag and press **CTRL** + **.**</span></span> <span data-ttu-id="98c5b-372">제안 메뉴를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-372">to open the suggestion menu.</span></span>
4. <span data-ttu-id="98c5b-373">**파일 추출을**클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-373">Click **Extract To File**.</span></span>

    <span data-ttu-id="98c5b-374">![JavaScript 파일에 대 한 추출 제안](visual-studio-2013-web-tools/_static/image39.png "JavaScript 파일에 대 한 추출 제안")</span><span class="sxs-lookup"><span data-stu-id="98c5b-374">![JavaScript extract to file suggestion](visual-studio-2013-web-tools/_static/image39.png "JavaScript extract to file suggestion")</span></span>

    <span data-ttu-id="98c5b-375">*JavaScript 파일에 대 한 추출 제안*</span><span class="sxs-lookup"><span data-stu-id="98c5b-375">*JavaScript extract to file suggestion*</span></span>
5. <span data-ttu-id="98c5b-376">다른 이름 **으로 저장** 창에서 **Scripts** 폴더를 선택 하 고 파일 이름을 **init** 로 하 고 **저장**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-376">In the **Save As** window, select the **Scripts** folder, name the file **init.js** and click **Save**.</span></span>

    <span data-ttu-id="98c5b-377">![창으로 저장](visual-studio-2013-web-tools/_static/image40.png "창으로 저장")</span><span class="sxs-lookup"><span data-stu-id="98c5b-377">![Save As window](visual-studio-2013-web-tools/_static/image40.png "Save As window")</span></span>

    <span data-ttu-id="98c5b-378">*창으로 저장*</span><span class="sxs-lookup"><span data-stu-id="98c5b-378">*Save As window*</span></span>

    > [!NOTE]
    > <span data-ttu-id="98c5b-379">**Init .js** 파일이 만들어지고 스크립트의 내용이 파일로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-379">The **init.js** file is created and the content of the script is moved to the file.</span></span>
    > 
    > <span data-ttu-id="98c5b-380">![포함 된 콘텐츠를 사용 하 여 생성 된 초기화 .js 파일](visual-studio-2013-web-tools/_static/image41.png "포함 된 콘텐츠를 사용 하 여 생성 된 초기화 .js 파일")</span><span class="sxs-lookup"><span data-stu-id="98c5b-380">![Init.js file created with the content included](visual-studio-2013-web-tools/_static/image41.png "Init.js file created with the content included")</span></span>
    > 
    > <span data-ttu-id="98c5b-381">*포함 된 콘텐츠를 사용 하 여 생성 된 초기화 .js 파일*</span><span class="sxs-lookup"><span data-stu-id="98c5b-381">*Init.js file created with the content included*</span></span>
6. <span data-ttu-id="98c5b-382">**인덱스 cshtml** 파일을 열고 스크립트 태그가 **init .js** 파일에 대 한 참조로 대체 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-382">Open the **Index.cshtml** file and check that the script tag was replaced with a reference to the **init.js** file.</span></span>

    <span data-ttu-id="98c5b-383">![Init .js html 참조](visual-studio-2013-web-tools/_static/image42.png "Init .js html 참조")</span><span class="sxs-lookup"><span data-stu-id="98c5b-383">![Init.js html reference](visual-studio-2013-web-tools/_static/image42.png "Init.js html reference")</span></span>

    <span data-ttu-id="98c5b-384">*Init .js html 참조*</span><span class="sxs-lookup"><span data-stu-id="98c5b-384">*Init.js html reference*</span></span>
7. <span data-ttu-id="98c5b-385">**솔루션 탐색기** 로 이동 하 여 **init .js** 파일이 솔루션에 자동으로 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-385">Go to the **Solution Explorer** and notice that the **init.js** file was included automatically in the solution.</span></span>

    <span data-ttu-id="98c5b-386">![솔루션에 포함 된 초기화 .js 파일](visual-studio-2013-web-tools/_static/image43.png "솔루션에 포함 된 초기화 .js 파일")</span><span class="sxs-lookup"><span data-stu-id="98c5b-386">![Init.js file included in solution](visual-studio-2013-web-tools/_static/image43.png "Init.js file included in solution")</span></span>

    <span data-ttu-id="98c5b-387">*솔루션에 포함 된 초기화 .js 파일*</span><span class="sxs-lookup"><span data-stu-id="98c5b-387">*Init.js file included in solution*</span></span>
8. <span data-ttu-id="98c5b-388">**Init .js** 파일로 다시 전환 하 여 **준비** 함수 콜백을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-388">Switch back to the **init.js** file to update the **ready** function callback.</span></span>
9. <span data-ttu-id="98c5b-389">*준비*에 전달 된 함수 콜백 정의 내에서 다음 코드를 추가 하 여 특정 클래스 특성에 따라 모든 요소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-389">Inside the function callback definition that is passed to *ready*, add the following code to get all the elements by a specific class attribute.</span></span>

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample10.js)]
10. <span data-ttu-id="98c5b-390">**GetElementsByClassName** 함수 호출 내의 따옴표 사이에 있는 **ctrl** + **공백을** 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-390">Press **CTRL** + **Space** between the quotes inside the **getElementsByClassName** function call.</span></span>

    <span data-ttu-id="98c5b-391">![GetElementsByClassName 함수에 대 한 IntelliSense 표시](visual-studio-2013-web-tools/_static/image44.png "GetElementsByClassName 함수에 대 한 IntelliSense 표시")</span><span class="sxs-lookup"><span data-stu-id="98c5b-391">![Showing IntelliSense for the getElementsByClassName function](visual-studio-2013-web-tools/_static/image44.png "Showing IntelliSense for the getElementsByClassName function")</span></span>

    <span data-ttu-id="98c5b-392">*GetElementsByClassName 함수에 대 한 IntelliSense 표시*</span><span class="sxs-lookup"><span data-stu-id="98c5b-392">*Showing IntelliSense for the getElementsByClassName function*</span></span>

    > [!NOTE]
    > <span data-ttu-id="98c5b-393">IntelliSense가 프로젝트 스타일 시트에 정의 된 클래스를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-393">Notice that IntelliSense shows the classes defined in the project style sheets.</span></span>
11. <span data-ttu-id="98c5b-394">만든 줄을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-394">Replace the line that you have created with the following code.</span></span>

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample11.js)]
12. <span data-ttu-id="98c5b-395">**GetElementsByTagName** 함수의 따옴표 안에 있는 **au** 뒤에 커서를 놓고 **CTRL** + **Space**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-395">Position the cursor after **au** inside the quotes in the **getElementsByTagName** function and press **CTRL** + **Space**.</span></span>

    <span data-ttu-id="98c5b-396">![GetElementByTagName 메서드에 대 한 IntelliSense 표시](visual-studio-2013-web-tools/_static/image45.png "GetElementByTagName 메서드에 대 한 IntelliSense 표시")</span><span class="sxs-lookup"><span data-stu-id="98c5b-396">![Showing IntelliSense for the getElementByTagName method](visual-studio-2013-web-tools/_static/image45.png "Showing IntelliSense for the getElementByTagName method")</span></span>

    <span data-ttu-id="98c5b-397">*GetElementsByTagName 메서드에 대 한 IntelliSense 표시*</span><span class="sxs-lookup"><span data-stu-id="98c5b-397">*Showing IntelliSense for the getElementsByTagName method*</span></span>
13. <span data-ttu-id="98c5b-398">목록에서 **&quot;오디오&quot;** 를 선택 하 고 **enter**키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-398">Select **&quot;audio&quot;** from the list and press **ENTER**.</span></span> <span data-ttu-id="98c5b-399">결과는 다음 그림에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-399">The result is shown in the following figure.</span></span>

    <span data-ttu-id="98c5b-400">![오디오 요소 검색](visual-studio-2013-web-tools/_static/image46.png "오디오 요소 검색")</span><span class="sxs-lookup"><span data-stu-id="98c5b-400">![Retrieving Audio Elements](visual-studio-2013-web-tools/_static/image46.png "Retrieving Audio Elements")</span></span>

    <span data-ttu-id="98c5b-401">*오디오 요소 검색*</span><span class="sxs-lookup"><span data-stu-id="98c5b-401">*Retrieving Audio Elements*</span></span>
14. <span data-ttu-id="98c5b-402">**솔루션 탐색기**에서 **Scripts** 폴더의 **init .js** 파일을 마우스 오른쪽 단추로 클릭 하 고 **Web Essentials** 메뉴에서 파일을 선택 하지 않은 **JavaScript 파일** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-402">In **Solution Explorer**, right-click the **init.js** file in the **Scripts** folder and select **Minify JavaScript file(s)** from the **Web Essentials** menu.</span></span>

    <span data-ttu-id="98c5b-403">![JavaScript 파일 (s)](visual-studio-2013-web-tools/_static/image47.png "JavaScript 파일")</span><span class="sxs-lookup"><span data-stu-id="98c5b-403">![Minify JavaScript file(s)](visual-studio-2013-web-tools/_static/image47.png "Minify JavaScript files")</span></span>

    <span data-ttu-id="98c5b-404">*JavaScript 파일 (s)*</span><span class="sxs-lookup"><span data-stu-id="98c5b-404">*Minify JavaScript file(s)*</span></span>
15. <span data-ttu-id="98c5b-405">원본 파일이 변경 될 때 자동 축소를 사용 하도록 설정 하 라는 메시지가 표시 되 면 **예**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-405">When prompted to enable automatic minification when the source file changes click **Yes**.</span></span>

    <span data-ttu-id="98c5b-406">![자동 축소 경고 사용](visual-studio-2013-web-tools/_static/image48.png "자동 축소 경고 사용")</span><span class="sxs-lookup"><span data-stu-id="98c5b-406">![Enabling automatic minification warning](visual-studio-2013-web-tools/_static/image48.png "Enabling automatic minification warning")</span></span>

    <span data-ttu-id="98c5b-407">*자동 축소 경고 사용*</span><span class="sxs-lookup"><span data-stu-id="98c5b-407">*Enabling automatic minification warning*</span></span>

    > [!NOTE]
    > <span data-ttu-id="98c5b-408">**Init.** m a m. m a. m **a.**</span><span class="sxs-lookup"><span data-stu-id="98c5b-408">The **init.min.js** is created and is added as a dependency of the **init.js** file.</span></span>
    > 
    > <span data-ttu-id="98c5b-409">![초기화 되는 최소 .js 파일](visual-studio-2013-web-tools/_static/image49.png "초기화 되는 최소 .js 파일")</span><span class="sxs-lookup"><span data-stu-id="98c5b-409">![Init.min.js file created](visual-studio-2013-web-tools/_static/image49.png "Init.min.js file created")</span></span>
    > 
    > <span data-ttu-id="98c5b-410">*초기화 되는 최소 .js 파일*</span><span class="sxs-lookup"><span data-stu-id="98c5b-410">*Init.min.js file created*</span></span>
16. <span data-ttu-id="98c5b-411">**Init. 최소 .js** 파일을 열고 파일의 표시를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-411">Open the **init.min.js** file and notice that the file is minified.</span></span>

    <span data-ttu-id="98c5b-412">![Init. 최소 .js 파일 콘텐츠](visual-studio-2013-web-tools/_static/image50.png "Init. 최소 .js 파일 콘텐츠")</span><span class="sxs-lookup"><span data-stu-id="98c5b-412">![Init.min.js file content](visual-studio-2013-web-tools/_static/image50.png "Init.min.js file content")</span></span>

    <span data-ttu-id="98c5b-413">*Init. 최소 .js 파일 콘텐츠*</span><span class="sxs-lookup"><span data-stu-id="98c5b-413">*Init.min.js file content*</span></span>
17. <span data-ttu-id="98c5b-414">**Init .js** 파일에서 **getElementsByTagName** 함수 호출 아래에 다음 코드를 추가 하 여 모든 오디오 요소를 재생 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-414">In the **init.js** file, add the following code below the **getElementsByTagName** function call to play all the audio elements.</span></span>

    <span data-ttu-id="98c5b-415">(코드 조각- *VisualStudio2013WebTooling* - *Ex2* - *play오디오 요소*)</span><span class="sxs-lookup"><span data-stu-id="98c5b-415">(Code Snippet - *VisualStudio2013WebTooling* - *Ex2* - *PlayAudioElements*)</span></span>

    [!code-csharp[Main](visual-studio-2013-web-tools/samples/sample12.cs)]
18. <span data-ttu-id="98c5b-416">**CTRL** + **S** 를 클릭 하 여 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-416">Click **CTRL** + **S** to save the file.</span></span> <span data-ttu-id="98c5b-417">파일이 이미 열려 있으므로 파일이 소스 편집기 외부에서 수정 되었다는 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-417">Since the minified file is already opened, you will see a dialog box saying that the file was modified outside of the source editor.</span></span> <span data-ttu-id="98c5b-418">**예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-418">Click **Yes**.</span></span>

    <span data-ttu-id="98c5b-419">![Microsoft Visual Studio 경고](visual-studio-2013-web-tools/_static/image51.png "Microsoft Visual Studio 경고")</span><span class="sxs-lookup"><span data-stu-id="98c5b-419">![Microsoft Visual Studio warning](visual-studio-2013-web-tools/_static/image51.png "Microsoft Visual Studio warning")</span></span>

    <span data-ttu-id="98c5b-420">*Microsoft Visual Studio 경고*</span><span class="sxs-lookup"><span data-stu-id="98c5b-420">*Microsoft Visual Studio warning*</span></span>
19. <span data-ttu-id="98c5b-421">**Init.** m a m 파일로 다시 전환 하 여 파일이 새 코드로 업데이트 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-421">Switch back to the **init.min.js** file to verify that the file was updated with the new code.</span></span>

    <span data-ttu-id="98c5b-422">![초기화 된 최소 .js 파일](visual-studio-2013-web-tools/_static/image52.png "초기화 된 최소 .js 파일")</span><span class="sxs-lookup"><span data-stu-id="98c5b-422">![Init.min.js file updated](visual-studio-2013-web-tools/_static/image52.png "Init.min.js file updated")</span></span>

    <span data-ttu-id="98c5b-423">*초기화 된 최소 .js 파일*</span><span class="sxs-lookup"><span data-stu-id="98c5b-423">*Init.min.js file updated*</span></span>
20. <span data-ttu-id="98c5b-424">**브라우저 링크 새로 고침** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-424">Click the **Browser Link Refresh** button.</span></span>
21. <span data-ttu-id="98c5b-425">두 브라우저를 새로 고치면 이전 작업에서 본 오디오 플레이어가 자동으로 재생 되기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-425">Once both browsers are refreshed the audio players you saw in the previous task will start playing automatically.</span></span>

    <span data-ttu-id="98c5b-426">![보기에 포함 된 오디오 플레이어](visual-studio-2013-web-tools/_static/image53.png "보기에 포함 된 오디오 플레이어")</span><span class="sxs-lookup"><span data-stu-id="98c5b-426">![Audio player included in view](visual-studio-2013-web-tools/_static/image53.png "Audio player included in view")</span></span>

    <span data-ttu-id="98c5b-427">*보기에 포함 된 오디오 플레이어*</span><span class="sxs-lookup"><span data-stu-id="98c5b-427">*Audio player included in view*</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="98c5b-428">요약</span><span class="sxs-lookup"><span data-stu-id="98c5b-428">Summary</span></span>

<span data-ttu-id="98c5b-429">이 실습 실습을 완료 하면 다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-429">By completing this hands-on lab you have learned how to:</span></span>

- <span data-ttu-id="98c5b-430">풍부한 HTML5 코드 조각 및 Zen 코딩 등 Web Essentials에 포함 된 새 HTML 편집기 기능 사용</span><span class="sxs-lookup"><span data-stu-id="98c5b-430">Use new HTML editor features included in Web Essentials such as rich HTML5 code snippets and Zen coding</span></span>
- <span data-ttu-id="98c5b-431">색 선택 및 브라우저 매트릭스 도구 설명과 같은 웹 Essentials에 포함 된 새 CSS 편집기 기능 사용</span><span class="sxs-lookup"><span data-stu-id="98c5b-431">Use new CSS editor features included in Web Essentials such as the Color picker and Browser matrix tooltip</span></span>
- <span data-ttu-id="98c5b-432">모든 HTML 요소에 대 한 파일 및 IntelliSense에 압축 풀기와 같은 웹 Essentials에 포함 된 새 JavaScript 편집기 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98c5b-432">Use new JavaScript editor features included in Web Essentials such as Extract to File and IntelliSense for all HTML elements</span></span>
- <span data-ttu-id="98c5b-433">브라우저 링크를 사용 하 여 브라우저와 Visual Studio 간 데이터 교환</span><span class="sxs-lookup"><span data-stu-id="98c5b-433">Exchange data between your browser and Visual Studio using Browser Link</span></span>
