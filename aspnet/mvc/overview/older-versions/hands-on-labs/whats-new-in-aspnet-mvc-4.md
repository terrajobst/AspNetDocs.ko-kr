---
uid: mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
title: ASP.NET MVC 4의 새로운 기능 | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4는 잘 구성 된 디자인 패턴과 ASP.NET의 기능을 사용 하 여 확장성 있는 표준 기반 웹 응용 프로그램을 빌드하기 위한 프레임 워크입니다.
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 48f7feb3-872f-485d-b96f-e30011ff8c4a
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 4235f4fe666cdeb7d0821127a2b349f2ff30cd6e
ms.sourcegitcommit: 295cf898a4c87e264b0c35c7254b0fa4169f2278
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2019
ms.locfileid: "74057038"
---
# <a name="whats-new-in-aspnet-mvc-4"></a><span data-ttu-id="b4414-103">ASP.NET MVC 4 的新增功能</span><span class="sxs-lookup"><span data-stu-id="b4414-103">What's New in ASP.NET MVC 4</span></span>

<span data-ttu-id="b4414-104">[웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="b4414-104">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="b4414-105">웹 캠프 교육 키트 다운로드</span><span class="sxs-lookup"><span data-stu-id="b4414-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="b4414-106">ASP.NET MVC 4는 잘 구성 된 디자인 패턴과 ASP.NET 및 .NET framework의 기능을 사용 하 여 확장성 있는 표준 기반 웹 응용 프로그램을 빌드하기 위한 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-106">ASP.NET MVC 4 is a framework for building scalable, standards-based web applications using well-established design patterns and the power of the ASP.NET and the .NET framework.</span></span> <span data-ttu-id="b4414-107">이 새로운 4 번째 버전의 프레임 워크는 모바일 웹 응용 프로그램 개발을 더 쉽게 만드는 데 중점을 둔 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-107">This new, fourth version of the framework focuses on making mobile web application development easier.</span></span>

<span data-ttu-id="b4414-108">먼저 새 ASP.NET MVC 4 프로젝트를 만들 때 모바일 장치에 대해 특별히 독립 실행형 앱을 빌드하는 데 사용할 수 있는 모바일 응용 프로그램 프로젝트 템플릿이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-108">To begin with, when you create a new ASP.NET MVC 4 project there is now a mobile application project template you can use to build a standalone app specifically for mobile devices.</span></span> <span data-ttu-id="b4414-109">또한 ASP.NET MVC 4는 jQuery 및 NuGet 패키지를 통해 jQuery Mobile과 통합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-109">Additionally, ASP.NET MVC 4 integrates with jQuery Mobile through a jQuery.Mobile.MVC NuGet package.</span></span> <span data-ttu-id="b4414-110">jQuery Mobile은 Windows Phone, iPhone, Android 등을 비롯 한 널리 사용 되는 모든 모바일 장치 플랫폼과 호환 되는 웹 앱을 개발 하기 위한 HTML5 기반 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-110">jQuery Mobile is an HTML5-based framework for developing web apps that are compatible with all popular mobile device platforms, including Windows Phone, iPhone, Android and so on.</span></span> <span data-ttu-id="b4414-111">그러나 특수화가 필요한 경우에는 ASP.NET MVC 4를 사용 하 여 여러 장치에 대 한 다양 한 보기를 제공 하 고 장치별 최적화를 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-111">However, if you need specialization, ASP.NET MVC 4 also enables you to serve different views for different devices and provide device-specific optimizations.</span></span>

<span data-ttu-id="b4414-112">이 실습 랩에서는 ASP.NET MVC 4 &quot;인터넷 응용 프로그램&quot; 프로젝트 템플릿으로 시작 하 여 사진 갤러리 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-112">In this hands-on lab, you will start with the ASP.NET MVC 4 &quot;Internet Application&quot; project template to create a Photo Gallery application.</span></span> <span data-ttu-id="b4414-113">JQuery Mobile 및 ASP.NET MVC 4의 새로운 기능을 사용 하 여 앱을 점진적으로 개선 하 여 다양 한 모바일 장치 및 데스크톱 웹 브라우저와 호환 되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-113">You will progressively enhance the app using jQuery Mobile and ASP.NET MVC 4's new features to make it compatible with different mobile devices and desktop web browsers.</span></span> <span data-ttu-id="b4414-114">또한 코드 생성을 위한 새 코드 조리법 및 ASP.NET MVC 4를 사용 하 여 작업&lt;ActionResult&gt; 반환 형식을 지원 함으로써 비동기 작업 메서드를 보다 쉽게 작성할 수 있는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-114">You will also learn about new code recipes for code generation and how ASP.NET MVC 4 makes it easier for you to write asynchronous action methods by supporting Task&lt;ActionResult&gt; return types.</span></span>

> [!NOTE]
> <span data-ttu-id="b4414-115">모든 샘플 코드와 코드 조각은 [Microsoft 웹/WebCampTrainingKit 릴리스에서](https://aka.ms/webcamps-training-kit)제공 되는 웹 캠프 교육 키트에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-115">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="b4414-116">이 랩에서 관련 된 프로젝트는 [ASP.NET 4.5의 Web Forms 새로운 기능](https://github.com/Microsoft-Web/HOL-ASPNETWebForms)에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-116">The project specific to this lab is available at [What's New in Web Forms in ASP.NET 4.5](https://github.com/Microsoft-Web/HOL-ASPNETWebForms).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="b4414-117">目标</span><span class="sxs-lookup"><span data-stu-id="b4414-117">Objectives</span></span>

<span data-ttu-id="b4414-118">이 실습 랩에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-118">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="b4414-119">새 모바일 응용 프로그램 프로젝트 템플릿을 포함 하 여 ASP.NET MVC 프로젝트 템플릿에 대 한 향상 된 기능 활용</span><span class="sxs-lookup"><span data-stu-id="b4414-119">Take advantage of the enhancements to the ASP.NET MVC project templates-including the new mobile application project template</span></span>
- <span data-ttu-id="b4414-120">HTML5 뷰포트 특성 및 CSS 미디어 쿼리를 사용 하 여 모바일 장치에 대 한 디스플레이 개선</span><span class="sxs-lookup"><span data-stu-id="b4414-120">Use the HTML5 viewport attribute and CSS media queries to improve the display on mobile devices</span></span>
- <span data-ttu-id="b4414-121">프로그레시브 기능 향상을 위해 jQuery Mobile 사용 및 터치 최적화 웹 UI 빌드</span><span class="sxs-lookup"><span data-stu-id="b4414-121">Use jQuery Mobile for progressive enhancements and for building touch-optimized web UI</span></span>
- <span data-ttu-id="b4414-122">모바일 관련 보기 만들기</span><span class="sxs-lookup"><span data-stu-id="b4414-122">Create mobile-specific views</span></span>
- <span data-ttu-id="b4414-123">뷰-전환기 구성 요소를 사용 하 여 응용 프로그램에서 모바일 및 데스크톱 보기 사이를 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-123">Use the view-switcher component to toggle between mobile and desktop views in the application</span></span>
- <span data-ttu-id="b4414-124">작업 지원을 사용 하 여 비동기 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="b4414-124">Create asynchronous controllers using task support</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="b4414-125">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b4414-125">Prerequisites</span></span>

<span data-ttu-id="b4414-126">이 랩을 완료 하려면 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-126">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="b4414-127">[웹 또는 고급의 경우 2012 Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (설치 방법에 대 한 지침은 [부록 B](#AppendixB) 를 참조 하세요.)</span><span class="sxs-lookup"><span data-stu-id="b4414-127">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix B](#AppendixB) for instructions on how to install it).</span></span>
- <span data-ttu-id="b4414-128">[ASP.NET MVC 4](../../../mvc4.md) (Microsoft Visual Studio 2012 설치에 포함 됨)</span><span class="sxs-lookup"><span data-stu-id="b4414-128">[ASP.NET MVC 4](../../../mvc4.md) (included in the Microsoft Visual Studio 2012 installation)</span></span>
- <span data-ttu-id="b4414-129">Windows Phone 에뮬레이터 ( [Windows Phone 7.1.1 SDK](https://www.microsoft.com/download/details.aspx?id=29233)에 포함 됨)</span><span class="sxs-lookup"><span data-stu-id="b4414-129">Windows Phone Emulator (included in the [Windows Phone 7.1.1 SDK](https://www.microsoft.com/download/details.aspx?id=29233))</span></span>
- <span data-ttu-id="b4414-130">선택 사항- [WebMatrix 2](https://www.microsoft.com/web/webmatrix/) ( **전기 Plum iphone 시뮬레이터** 확장 포함) (iphone 시뮬레이터를 사용 하 여 웹 응용 프로그램을 검색 하는 데 사용 되는 연습 3에만 해당)</span><span class="sxs-lookup"><span data-stu-id="b4414-130">Optional - [WebMatrix 2](https://www.microsoft.com/web/webmatrix/) with **Electric Plum iPhone Simulator** extension (only for Exercise 3 used to browse the web application with an iPhone simulator)</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="b4414-131">安装</span><span class="sxs-lookup"><span data-stu-id="b4414-131">Setup</span></span>

<span data-ttu-id="b4414-132">랩 문서 전체에서 코드 블록을 삽입 하 라는 지침이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-132">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="b4414-133">사용자 편의를 위해 대부분의 코드는 Visual Studio 내에서 사용 하 여 수동으로 추가할 필요가 없도록 하는 Visual Studio Code 코드 조각으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-133">For your convenience, most of that code is provided as Visual Studio Code Snippets, which you can use from within Visual Studio to avoid having to add it manually.</span></span>

<span data-ttu-id="b4414-134">코드 조각을 설치 하려면:</span><span class="sxs-lookup"><span data-stu-id="b4414-134">To install the code snippets:</span></span>

1. <span data-ttu-id="b4414-135">Windows 탐색기 창을 열고 랩의 **Source\Setup** 폴더로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-135">Open a Windows Explorer window and browse to the lab's **Source\Setup** folder.</span></span>
2. <span data-ttu-id="b4414-136">이 폴더에 있는 **setup.exe** 파일을 두 번 클릭 하 여 Visual Studio 코드 조각을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-136">Double-click the **Setup.cmd** file in this folder to install the Visual Studio code snippets.</span></span>

<span data-ttu-id="b4414-137">Visual Studio Code 코드 조각에 익숙하지 않은 경우이를 사용 하는 방법을 알아보려면 [부록 A: &quot;코드 조각&quot;사용](#AppendixA) 문서에서 부록을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-137">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix A: Using Code Snippets](#AppendixA)&quot;.</span></span>

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="b4414-138">실습</span><span class="sxs-lookup"><span data-stu-id="b4414-138">Exercises</span></span>

<span data-ttu-id="b4414-139">이 실습 랩에는 다음 연습이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-139">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="b4414-140">새 ASP.NET MVC 4 프로젝트 템플릿</span><span class="sxs-lookup"><span data-stu-id="b4414-140">New ASP.NET MVC 4 Project Templates</span></span>](#Exercise1)
2. [<span data-ttu-id="b4414-141">사진 갤러리 웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="b4414-141">Creating the Photo Gallery Web Application</span></span>](#Exercise2)
3. [<span data-ttu-id="b4414-142">모바일 장치에 대 한 지원 추가</span><span class="sxs-lookup"><span data-stu-id="b4414-142">Adding Support for Mobile Devices</span></span>](#Exercise3)
4. [<span data-ttu-id="b4414-143">비동기 컨트롤러 사용</span><span class="sxs-lookup"><span data-stu-id="b4414-143">Using Asynchronous Controllers</span></span>](#Exercise4)

> [!NOTE]
> <span data-ttu-id="b4414-144">각 연습에는 연습을 완료 한 후 얻게 되는 결과 솔루션을 포함 하는 **끝** 폴더가 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-144">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="b4414-145">연습을 진행 하는 데 도움이 필요한 경우이 솔루션을 지침으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-145">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="b4414-146">이 랩을 완료 하는 데 소요 되는 예상 시간: **60 분**</span><span class="sxs-lookup"><span data-stu-id="b4414-146">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_New_ASPNET_MVC_4_Project_Templates"></a>
### <a name="exercise-1-new-aspnet-mvc-4-project-templates"></a><span data-ttu-id="b4414-147">연습 1: New ASP.NET MVC 4 프로젝트 템플릿</span><span class="sxs-lookup"><span data-stu-id="b4414-147">Exercise 1: New ASP.NET MVC 4 Project Templates</span></span>

<span data-ttu-id="b4414-148">이 연습에서는 ASP.NET MVC 4 프로젝트 템플릿의 향상 된 기능을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-148">In this exercise, you will explore the enhancements in the ASP.NET MVC 4 Project templates.</span></span> <span data-ttu-id="b4414-149">이제 MVC 3에 이미 있는 인터넷 응용 프로그램 템플릿 외에도이 버전에는 모바일 응용 프로그램에 대 한 별도의 템플릿이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-149">In addition to the Internet Application template, already present in MVC 3, this version now includes a separate template for Mobile applications.</span></span> <span data-ttu-id="b4414-150">먼저 각 템플릿의 관련 기능 중 일부를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-150">First, you will look at some relevant features of each of the templates.</span></span> <span data-ttu-id="b4414-151">그런 다음 적절 한 방법을 사용 하 여 여러 플랫폼에서 페이지를 올바르게 렌더링 하는 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-151">Then, you will work on rendering your page properly on the different platforms by using the right approach.</span></span>

<a id="Task_1_-_Exploring_the_Internet_Application_Template"></a>
#### <a name="task-1---exploring-the-internet-application-template"></a><span data-ttu-id="b4414-152">작업 1-인터넷 응용 프로그램 템플릿 탐색</span><span class="sxs-lookup"><span data-stu-id="b4414-152">Task 1 - Exploring the Internet Application Template</span></span>

1. <span data-ttu-id="b4414-153">**Visual Studio**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-153">Open **Visual Studio**.</span></span>
2. <span data-ttu-id="b4414-154">파일을 선택 합니다. **| 새로 만들기 | 프로젝트** 메뉴 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-154">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="b4414-155">**새 프로젝트** 대화 상자에서 **시각적 개체 C# | 웹** 템플릿 왼쪽 창에서 **ASP.NET MVC 4 웹 응용 프로그램을 선택 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b4414-155">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="b4414-156">프로젝트 이름을 **사진**으로 지정 하 고 위치를 선택 하거나 기본값을 그대로 두고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-156">Name the project **PhotoGallery**, select a location (or leave the default) and click **OK**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b4414-157">나중에 현재 만들고 있는 사진 갤러리 ASP.NET MVC 4 솔루션을 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-157">You will later customize the PhotoGallery ASP.NET MVC 4 solution you are now creating.</span></span>

    <span data-ttu-id="b4414-158">![새 프로젝트 만들기](whats-new-in-aspnet-mvc-4/_static/image1.png "새 프로젝트 만들기")</span><span class="sxs-lookup"><span data-stu-id="b4414-158">![Creating a new project](whats-new-in-aspnet-mvc-4/_static/image1.png "Creating a new project")</span></span>

    <span data-ttu-id="b4414-159">*새 프로젝트 만들기*</span><span class="sxs-lookup"><span data-stu-id="b4414-159">*Creating a new project*</span></span>
3. <span data-ttu-id="b4414-160">**새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **인터넷 응용 프로그램** 프로젝트 템플릿을 선택 하 고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-160">In the **New ASP.NET MVC 4 Project** dialog, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="b4414-161">Razor를 뷰 엔진으로 선택 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-161">Make sure you have selected Razor as the view engine.</span></span>

    <span data-ttu-id="b4414-162">![새 ASP.NET MVC 4 인터넷 응용 프로그램 만들기](whats-new-in-aspnet-mvc-4/_static/image2.png "새 ASP.NET MVC 4 인터넷 응용 프로그램 만들기")</span><span class="sxs-lookup"><span data-stu-id="b4414-162">![Creating a new ASP.NET MVC 4 Internet Application](whats-new-in-aspnet-mvc-4/_static/image2.png "Creating a new ASP.NET MVC 4 Internet Application")</span></span>

    <span data-ttu-id="b4414-163">*새 ASP.NET MVC 4 인터넷 응용 프로그램 만들기*</span><span class="sxs-lookup"><span data-stu-id="b4414-163">*Creating a new ASP.NET MVC 4 Internet Application*</span></span>

    > [!NOTE]
    > <span data-ttu-id="b4414-164">Razor 구문는 ASP.NET MVC 3에서 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-164">Razor syntax has been introduced in ASP.NET MVC 3.</span></span> <span data-ttu-id="b4414-165">이는 파일에 필요한 문자 및 키 입력 수를 최소화 하 여 빠르고 유체 코딩 워크플로를 사용 하도록 설정 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-165">Its goal is to minimize the number of characters and keystrokes required in a file, enabling a fast and fluid coding workflow.</span></span> <span data-ttu-id="b4414-166">Razor는 기존 C# /VB (또는 기타) 언어 기술을 활용 하 고 멋진 HTML 생성 워크플로를 활성화 하는 템플릿 태그 구문을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-166">Razor leverages existing C# / VB (or other) language skills and delivers a template markup syntax that enables an awesome HTML construction workflow.</span></span>
4. <span data-ttu-id="b4414-167">**F5** 키를 눌러 솔루션을 실행 하 고 갱신 된 템플릿을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-167">Press **F5** to run the solution and see the renewed templates.</span></span> <span data-ttu-id="b4414-168">다음 기능을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-168">You can check out the following features:</span></span>

    <span data-ttu-id="b4414-169">**최신 스타일 템플릿**</span><span class="sxs-lookup"><span data-stu-id="b4414-169">**Modern-style templates**</span></span>

    <span data-ttu-id="b4414-170">템플릿이 갱신 되어 최신 스타일을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-170">The templates have been renewed, providing more modern-looking styles.</span></span>

    <span data-ttu-id="b4414-171">![ASP.NET MVC 4 스타일 지정 템플릿](whats-new-in-aspnet-mvc-4/_static/image3.png "MVC 4 스타일 지정 템플릿")</span><span class="sxs-lookup"><span data-stu-id="b4414-171">![ASP.NET MVC 4 restyled templates](whats-new-in-aspnet-mvc-4/_static/image3.png "MVC 4 restyled templates")</span></span>

    <span data-ttu-id="b4414-172">*ASP.NET MVC 4 스타일 지정 템플릿*</span><span class="sxs-lookup"><span data-stu-id="b4414-172">*ASP.NET MVC 4 restyled templates*</span></span>

    <span data-ttu-id="b4414-173">![새 연락처 페이지](whats-new-in-aspnet-mvc-4/_static/image4.png "새 연락처 페이지")</span><span class="sxs-lookup"><span data-stu-id="b4414-173">![New Contact page](whats-new-in-aspnet-mvc-4/_static/image4.png "New Contact page")</span></span>

    <span data-ttu-id="b4414-174">*새 연락처 페이지*</span><span class="sxs-lookup"><span data-stu-id="b4414-174">*New Contact page*</span></span>

    <span data-ttu-id="b4414-175">**적응 렌더링**</span><span class="sxs-lookup"><span data-stu-id="b4414-175">**Adaptive Rendering**</span></span>

    <span data-ttu-id="b4414-176">브라우저 창의 크기를 조정 하 고 페이지 레이아웃이 새 창 크기에 동적으로 적응 하는 방식을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-176">Check out resizing the browser window and notice how the page layout dynamically adapts to the new window size.</span></span> <span data-ttu-id="b4414-177">이러한 템플릿은 적응 렌더링 기술을 사용 하 여 사용자 지정 없이 데스크톱과 모바일 플랫폼 모두에서 적절히 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-177">These templates use the adaptive rendering technique to render properly in both desktop and mobile platforms without any customization.</span></span>

    <span data-ttu-id="b4414-178">![다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿](whats-new-in-aspnet-mvc-4/_static/image5.png "다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿")</span><span class="sxs-lookup"><span data-stu-id="b4414-178">![ASP.NET MVC 4 project template in different browser sizes](whats-new-in-aspnet-mvc-4/_static/image5.png "ASP.NET MVC 4 project template in different browser sizes")</span></span>

    <span data-ttu-id="b4414-179">*다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿*</span><span class="sxs-lookup"><span data-stu-id="b4414-179">*ASP.NET MVC 4 project template in different browser sizes*</span></span>

    <span data-ttu-id="b4414-180">**JavaScript를 사용 하는 풍부한 UI**</span><span class="sxs-lookup"><span data-stu-id="b4414-180">**Richer UI with JavaScript**</span></span>

    <span data-ttu-id="b4414-181">기본 프로젝트 템플릿에 대 한 또 다른 향상 된 기능은 JavaScript를 사용 하 여 더 대화형 JavaScript를 제공 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-181">Another enhancement to default project templates is the use of JavaScript to provide a more interactive JavaScript.</span></span> <span data-ttu-id="b4414-182">템플릿에 사용 되는 로그인 및 등록 링크는 jQuery 유효성 검사를 사용 하 여 클라이언트 쪽에서 입력 필드의 유효성을 검사 하는 방법을 exemplify 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-182">The Login and Register links used in the template exemplify how to use the jQuery Validations to validate the input fields from client-side.</span></span>

    ![jQuery 유효성 검사](whats-new-in-aspnet-mvc-4/_static/image6.png)

    <span data-ttu-id="b4414-184">*jQuery 유효성 검사*</span><span class="sxs-lookup"><span data-stu-id="b4414-184">*jQuery Validation*</span></span>

    > [!NOTE]
    > <span data-ttu-id="b4414-185">두 개의 로그인 섹션, 첫 번째 섹션에서는 사이트에서 등록 된 계정을 사용 하 여 로그인 할 수 있으며, 두 번째 섹션에서는 google (기본적으로 사용 하지 않도록 설정 됨)과 같은 다른 인증 서비스를 사용 하 여 로그인 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-185">Notice the two log in sections, in the first section you can log in using a registered account from the site and in the second section you can alternatively log in using another authentication service like google (disabled by default).</span></span>
5. <span data-ttu-id="b4414-186">디버거를 중지 하 고 Visual Studio로 돌아가려면 브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-186">Close the browser to stop the debugger and return to Visual Studio.</span></span>
6. <span data-ttu-id="b4414-187">**앱\_시작** 폴더 아래에 있는 **AuthConfig.cs** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-187">Open the file **AuthConfig.cs** located under the **App\_Start** folder.</span></span>
7. <span data-ttu-id="b4414-188">마지막 줄에서 의견을 제거 하 여 *OAuth* 인증에 Google 클라이언트를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-188">Remove the comment from the last line to register Google client for *OAuth* authentication.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample1.cs)]

    > [!NOTE]
    > <span data-ttu-id="b4414-189">Openid connect 또는 OAuth 서비스 (예: Facebook, Twitter, Microsoft 등)를 사용 하 여 인증을 쉽게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-189">Notice you can easily enable authentication using any OpenID or OAuth service like Facebook, Twitter, Microsoft, etc.</span></span>
8. <span data-ttu-id="b4414-190">**F5** 키를 눌러 솔루션을 실행 하 고 로그인 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-190">Press **F5** to run the solution and navigate to the login page.</span></span>
9. <span data-ttu-id="b4414-191">로그인 하려면 **Google** service를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-191">Select **Google** service to log in.</span></span>

    ![로그인 서비스 선택](whats-new-in-aspnet-mvc-4/_static/image7.png)

    <span data-ttu-id="b4414-193">*로그인 서비스 선택*</span><span class="sxs-lookup"><span data-stu-id="b4414-193">*Selecting the log in service*</span></span>
10. <span data-ttu-id="b4414-194">Google 계정을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-194">Log in using your Google account.</span></span>
11. <span data-ttu-id="b4414-195">사이트 (localhost)가 Google 계정에서 정보를 검색할 수 있도록 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-195">Allow the site (localhost) to retrieve information from Google account.</span></span>
12. <span data-ttu-id="b4414-196">마지막으로 Google 계정을 연결 하려면 사이트에 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-196">Finally, you will have to register in the site to associate the Google account.</span></span>

   ![Google 계정 연결](whats-new-in-aspnet-mvc-4/_static/image8.png)

   <span data-ttu-id="b4414-198">*Google 계정 연결*</span><span class="sxs-lookup"><span data-stu-id="b4414-198">*Associating your Google account*</span></span>
13. <span data-ttu-id="b4414-199">디버거를 중지 하 고 Visual Studio로 돌아가려면 브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-199">Close the browser to stop the debugger and return to Visual Studio.</span></span>
14. <span data-ttu-id="b4414-200">이제 솔루션을 탐색 하 여 프로젝트 템플릿에서 ASP.NET MVC 4에서 도입 된 몇 가지 다른 새로운 기능을 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="b4414-200">Now explore the solution to check out some other new features introduced by ASP.NET MVC 4 in the project template.</span></span>

   <span data-ttu-id="b4414-201">![ASP.NET MVC 4 인터넷 응용 프로그램 프로젝트 템플릿](whats-new-in-aspnet-mvc-4/_static/image9.png "ASP.NET MVC 4 인터넷 응용 프로그램 프로젝트 템플릿")</span><span class="sxs-lookup"><span data-stu-id="b4414-201">![The ASP.NET MVC 4 Internet Application Project Template](whats-new-in-aspnet-mvc-4/_static/image9.png "The ASP.NET MVC 4 Internet Application Project Template")</span></span>

   <span data-ttu-id="b4414-202">*ASP.NET MVC 4 인터넷 응용 프로그램 프로젝트 템플릿*</span><span class="sxs-lookup"><span data-stu-id="b4414-202">*The ASP.NET MVC 4 Internet Application Project Template*</span></span>

    - <span data-ttu-id="b4414-203">**HTML 5 태그**</span><span class="sxs-lookup"><span data-stu-id="b4414-203">**HTML 5 Markup**</span></span>

       <span data-ttu-id="b4414-204">템플릿 뷰를 탐색 하 여 새 테마 태그를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-204">Browse template views to find out the new theme markup.</span></span>

       <span data-ttu-id="b4414-205">![새 템플릿으로, Razor 및 HTML5 태그를 사용 합니다.](whats-new-in-aspnet-mvc-4/_static/image10.png "새 템플릿으로, Razor 및 HTML5 태그를 사용 합니다.")</span><span class="sxs-lookup"><span data-stu-id="b4414-205">![New template, using Razor and HTML5 markup About.cshtml.](whats-new-in-aspnet-mvc-4/_static/image10.png "New template, using Razor and HTML5 markup About.cshtml.")</span></span>

       <span data-ttu-id="b4414-206">*Razor 및 HTML5 태그를 사용 하는 새 템플릿 (정보 cshtml)*</span><span class="sxs-lookup"><span data-stu-id="b4414-206">*New template, using Razor and HTML5 markup (About.cshtml).*</span></span>
    - <span data-ttu-id="b4414-207">**업데이트 된 JavaScript 라이브러리**</span><span class="sxs-lookup"><span data-stu-id="b4414-207">**Updated JavaScript libraries**</span></span>

       <span data-ttu-id="b4414-208">ASP.NET MVC 4 기본 템플릿에는 JavaScript 및 HTML을 사용 하 여 풍부 하 고 응답성이 뛰어난 웹 응용 프로그램을 만들 수 있는 JavaScript MVVM 프레임 워크인 KnockoutJS가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-208">The ASP.NET MVC 4 default template now includes KnockoutJS, a JavaScript MVVM framework that lets you create rich and highly responsive web applications using JavaScript and HTML.</span></span> <span data-ttu-id="b4414-209">MVC3에서와 마찬가지로 jQuery 및 jQuery UI 라이브러리도 ASP.NET MVC 4에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-209">Like in MVC3, jQuery and jQuery UI libraries are also included in ASP.NET MVC 4.</span></span>

     > [!NOTE]
     > <span data-ttu-id="b4414-210">이 링크에서 KnockOutJS library에 대 한 자세한 내용은 [[http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)](http://learn.knockoutjs.com/)를 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="b4414-210">You can get more information about KnockOutJS library in this link: [[http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)](http://learn.knockoutjs.com/).</span></span> <span data-ttu-id="b4414-211">또한 [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/)에서 jQuery 및 jquery UI에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-211">Additionally, you can learn about jQuery and jQuery UI in [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/).</span></span>

<a id="Task_2_-_Exploring_the_Mobile_Application_Template"></a>
#### <a name="task-2---exploring-the-mobile-application-template"></a><span data-ttu-id="b4414-212">작업 2-모바일 응용 프로그램 템플릿 탐색</span><span class="sxs-lookup"><span data-stu-id="b4414-212">Task 2 - Exploring the Mobile Application Template</span></span>

<span data-ttu-id="b4414-213">ASP.NET MVC 4는 모바일 및 태블릿 브라우저용 웹 사이트 개발을 용이 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-213">ASP.NET MVC 4 facilitates the development of websites for mobile and tablet browsers.</span></span> <span data-ttu-id="b4414-214">이 템플릿의 응용 프로그램 구조는 인터넷 응용 프로그램 템플릿과 동일 하지만 (컨트롤러 코드는 거의 동일 함) 터치 기반 모바일 장치에서 제대로 렌더링 되도록 스타일이 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-214">This template has the same application structure as the Internet Application template (notice that the controller code is practically identical), but its style was modified to render properly in touch-based mobile devices.</span></span>

1. <span data-ttu-id="b4414-215">파일을 선택 합니다. **| 새로 만들기 | 프로젝트** 메뉴 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-215">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="b4414-216">**새 프로젝트** 대화 상자에서 **시각적 개체 C# | 웹** 템플릿을 선택 하 고 **ASP.NET MVC 4 웹 응용 프로그램을 선택 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b4414-216">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose the **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="b4414-217">프로젝트 이름을 **사진 갤러리**로 지정 하 고, 위치를 선택 하 고, 위치를 선택 하거나, &quot;솔루션&quot;에 추가를 선택 하 고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-217">Name the project **PhotoGallery.Mobile**, select a location (or leave the default), select &quot;Add to solution&quot; and click **OK**.</span></span>
2. <span data-ttu-id="b4414-218">**새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **모바일 응용 프로그램** 프로젝트 템플릿을 선택 하 고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-218">In the **New ASP.NET MVC 4 Project** dialog, select the **Mobile Application** project template and click **OK**.</span></span> <span data-ttu-id="b4414-219">Razor를 뷰 엔진으로 선택 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-219">Make sure you have selected Razor as the view engine.</span></span>

    <span data-ttu-id="b4414-220">![새 ASP.NET MVC 4 모바일 응용 프로그램 만들기](whats-new-in-aspnet-mvc-4/_static/image11.png "새 ASP.NET MVC 4 모바일 응용 프로그램 만들기")</span><span class="sxs-lookup"><span data-stu-id="b4414-220">![Creating a new ASP.NET MVC 4 Mobile Application](whats-new-in-aspnet-mvc-4/_static/image11.png "Creating a new ASP.NET MVC 4 Mobile Application")</span></span>

    <span data-ttu-id="b4414-221">*새 ASP.NET MVC 4 모바일 응용 프로그램 만들기*</span><span class="sxs-lookup"><span data-stu-id="b4414-221">*Creating a new ASP.NET MVC 4 Mobile Application*</span></span>
3. <span data-ttu-id="b4414-222">이제 솔루션을 탐색 하 고 mobile 용 ASP.NET MVC 4 솔루션 템플릿에서 도입 된 새로운 기능 중 일부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-222">Now you are able to explore the solution and check out some of the new features introduced by the ASP.NET MVC 4 solution template for mobile:</span></span>

    - <span data-ttu-id="b4414-223">**jQuery 모바일 라이브러리**</span><span class="sxs-lookup"><span data-stu-id="b4414-223">**jQuery Mobile Library**</span></span>

        <span data-ttu-id="b4414-224">모바일 응용 프로그램 프로젝트 템플릿에는 모바일 브라우저 호환성을 위한 오픈 소스 라이브러리인 jQuery 모바일 라이브러리가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-224">The Mobile Application project template includes the jQuery Mobile library, which is an open source library for mobile browser compatibility.</span></span> <span data-ttu-id="b4414-225">jQuery Mobile은 CSS 및 JavaScript를 지 원하는 모바일 브라우저에 점진적 향상 기능을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-225">jQuery Mobile applies progressive enhancement to mobile browsers that support CSS and JavaScript.</span></span> <span data-ttu-id="b4414-226">점진적 향상 기능을 통해 모든 브라우저는 웹 페이지의 기본 콘텐츠를 표시할 수 있으며, 가장 강력한 브라우저 에서만 풍부한 콘텐츠를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-226">Progressive enhancement enables all browsers to display the basic content of a web page, while it only enables the most powerful browsers to display the rich content.</span></span> <span data-ttu-id="b4414-227">JQuery 모바일 스타일에 포함 된 JavaScript 및 CSS 파일은 페이지 태그를 변경 하지 않고 화면에 콘텐츠를 맞추는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-227">The JavaScript and CSS files, included in the jQuery Mobile style, help mobile browsers to fit the content in the screen without making any change in the page markup.</span></span>

        ![jQuery-mobile library-포함 된 템플릿](whats-new-in-aspnet-mvc-4/_static/image12.png)

        <span data-ttu-id="b4414-229">*템플릿에 포함 된 jQuery mobile library*</span><span class="sxs-lookup"><span data-stu-id="b4414-229">*jQuery mobile library included in the template*</span></span>
    - <span data-ttu-id="b4414-230">**HTML5 기반 태그**</span><span class="sxs-lookup"><span data-stu-id="b4414-230">**HTML5 based markup**</span></span>

        ![모바일-응용 프로그램-템플릿 사용-HTML5-태그](whats-new-in-aspnet-mvc-4/_static/image13.png)

        <span data-ttu-id="b4414-232">*HTML5 태그를 사용 하는 모바일 응용 프로그램 템플릿 (Login/cshtml)*</span><span class="sxs-lookup"><span data-stu-id="b4414-232">*Mobile application template using HTML5 markup, (Login.cshtml and index.cshtml)*</span></span>
4. <span data-ttu-id="b4414-233">**F5** 키를 눌러 솔루션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-233">Press **F5** to run the solution.</span></span>
5. <span data-ttu-id="b4414-234">**Windows Phone 7 에뮬레이터**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-234">Open the **Windows Phone 7 Emulator**.</span></span>
6. <span data-ttu-id="b4414-235">휴대폰 시작 화면에서 Internet Explorer를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-235">In the phone start screen, open Internet Explorer.</span></span> <span data-ttu-id="b4414-236">데스크톱 응용 프로그램이 시작 된 URL을 확인 하 고 휴대폰에서 해당 URL로 이동 합니다 (예: `http://localhost:[PortNumber]/`).</span><span class="sxs-lookup"><span data-stu-id="b4414-236">Check out the URL where the desktop application started and browse to that URL from the phone (e.g. `http://localhost:[PortNumber]/`).</span></span>
7. <span data-ttu-id="b4414-237">이제 로그인 페이지를 입력 하거나 정보 페이지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-237">Now you are able to enter the login page or check out the about page.</span></span> <span data-ttu-id="b4414-238">웹 사이트의 스타일은 모바일 용 새 Metro 앱을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-238">Notice that the style of the website is based on the new Metro app for mobile.</span></span> <span data-ttu-id="b4414-239">ASP.NET MVC 4 프로젝트 템플릿이 모바일 장치에 올바르게 표시 되므로 페이지의 모든 요소가 표시 되 고 사용 하도록 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-239">The ASP.NET MVC 4 project template is correctly displayed on mobile devices, making sure all the elements of the page are visible and enabled.</span></span> <span data-ttu-id="b4414-240">헤더에 대 한 링크는 클릭 하거나 탭 할 만큼 충분히 큽니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-240">Notice that the links on the header are big enough to be clicked or tapped.</span></span>

    <span data-ttu-id="b4414-241">![모바일 장치의 프로젝트 템플릿 페이지](whats-new-in-aspnet-mvc-4/_static/image14.png "모바일 장치의 프로젝트 템플릿 페이지")</span><span class="sxs-lookup"><span data-stu-id="b4414-241">![Project template pages in a mobile device](whats-new-in-aspnet-mvc-4/_static/image14.png "Project template pages in a mobile device")</span></span>

    <span data-ttu-id="b4414-242">*모바일 장치의 프로젝트 템플릿 페이지*</span><span class="sxs-lookup"><span data-stu-id="b4414-242">*Project template pages in a mobile device*</span></span>
8. <span data-ttu-id="b4414-243">새 템플릿은 **뷰포트 메타 태그**도 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-243">The new template also uses the **Viewport meta tag**.</span></span> <span data-ttu-id="b4414-244">대부분의 모바일 브라우저는 모바일 장치의 실제 너비 보다 큰 가상 브라우저 창 또는 &quot;뷰포트&quot;의 너비를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-244">Most mobile browsers define a width for a virtual browser window or &quot;viewport&quot;, which is larger than the actual width of the mobile device.</span></span> <span data-ttu-id="b4414-245">이렇게 하면 모바일 브라우저에서 전체 웹 페이지를 가상 표시 안에 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-245">This enables mobile browsers to display the entire web page inside the virtual display.</span></span> <span data-ttu-id="b4414-246">웹 개발자는 **뷰포트 메타 태그** 를 사용 하 여 모바일 장치에서 브라우저 영역의 너비, 높이 및 크기를 설정할 수 있습니다 **.**</span><span class="sxs-lookup"><span data-stu-id="b4414-246">The **Viewport meta tag** allows web developers to set the width, height and scale of the browser area on mobile devices **.**</span></span> <span data-ttu-id="b4414-247">모바일 응용 프로그램에 대 한 ASP.NET MVC 4 템플릿에서는 레이아웃 템플릿 (*Views\Shared\_layout. cshtml*)의 장치 너비 (&quot;width = 장치 너비&quot;)로 뷰포트를 설정 하 여 모든 페이지의 뷰포트가 장치 화면 너비로 설정 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-247">The ASP.NET MVC 4 template for Mobile Applications sets the viewport to the device width (&quot;width=device-width&quot;) in the layout template (*Views\Shared\_Layout.cshtml*), so that all the pages will have their viewport set to the device screen width.</span></span> <span data-ttu-id="b4414-248">뷰포트 메타 태그는 기본 브라우저 보기를 변경 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-248">Notice that the Viewport meta tag will not change the default browser view.</span></span>
9. <span data-ttu-id="b4414-249">뷰에 있는 **\_Layout. cshtml**를 엽니다.  **공유** 폴더, 뷰포트 메타 태그 설명</span><span class="sxs-lookup"><span data-stu-id="b4414-249">Open **\_Layout.cshtml**, located in the **Views | Shared** folder, and comment the Viewport meta tag.</span></span> <span data-ttu-id="b4414-250">응용 프로그램을 아직 열지 않은 경우 실행 하 고 차이점을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-250">Run the application, if not already opened, and check out the differences.</span></span>

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample2.cshtml)]

<span data-ttu-id="b4414-251">![뷰포트 메타 태그를 주석으로 처리 한 후의 사이트입니다.](whats-new-in-aspnet-mvc-4/_static/image15.png "뷰포트 메타 태그를 주석으로 처리 한 후의 사이트입니다.")</span><span class="sxs-lookup"><span data-stu-id="b4414-251">![The site after commenting the viewport meta tag](whats-new-in-aspnet-mvc-4/_static/image15.png "The site after commenting the viewport meta tag")</span></span>

<span data-ttu-id="b4414-252">*뷰포트 메타 태그를 주석으로 처리 한 후의 사이트입니다.*</span><span class="sxs-lookup"><span data-stu-id="b4414-252">*The site after commenting the viewport meta tag*</span></span>
10. <span data-ttu-id="b4414-253">Visual Studio에서 **SHIFT** + **f5** 키를 눌러 응용 프로그램 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-253">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
11. <span data-ttu-id="b4414-254">뷰포트 메타 태그의 주석 처리를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-254">Uncomment the viewport meta tag.</span></span>

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample3.cshtml)]

<a id="Task_3_-_Using_Adaptive_Rendering"></a>
#### <a name="task-3---using-adaptive-rendering"></a><span data-ttu-id="b4414-255">작업 3-적응 렌더링 사용</span><span class="sxs-lookup"><span data-stu-id="b4414-255">Task 3 - Using Adaptive Rendering</span></span>

<span data-ttu-id="b4414-256">이 작업에서는 사용자 지정 없이 모바일 장치 및 웹 브라우저에서 웹 페이지를 올바르게 렌더링 하는 다른 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-256">In this task, you will learn another method to render a Web page correctly on mobile devices and Web browsers at the same time without any customization.</span></span> <span data-ttu-id="b4414-257">이미 유사한 용도로 뷰포트 메타 태그를 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-257">You have already used Viewport meta tag with a similar purpose.</span></span> <span data-ttu-id="b4414-258">이제 다른 강력한 방법 ( *적응 렌더링*)을 충족 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-258">Now you will meet another powerful method: *adaptive rendering*.</span></span>

<span data-ttu-id="b4414-259">적응 렌더링은 **CSS3 미디어 쿼리** 를 사용 하 여 페이지에 적용 되는 스타일을 사용자 지정 하는 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-259">Adaptive rendering is a technique that uses **CSS3 media queries** to customize the style applied to a page.</span></span> <span data-ttu-id="b4414-260">미디어 쿼리는 특정 조건에서 CSS 스타일을 그룹화 하 여 스타일 시트 내에서 조건을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-260">Media queries define conditions inside a style sheet, grouping CSS styles under a certain condition.</span></span> <span data-ttu-id="b4414-261">조건이 true 인 경우에만 스타일이 선언 된 개체에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-261">Only when the condition is true, the style is applied to the declared objects.</span></span>

<span data-ttu-id="b4414-262">적응 렌더링 기술에서 제공 하는 유연성을 통해 다른 장치에 사이트를 표시 하는 사용자 지정을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-262">The flexibility provided by the adaptive rendering technique enables any customization for displaying the site on different devices.</span></span> <span data-ttu-id="b4414-263">스타일을 선택 하는 논리 코드를 작성 하지 않고 단일 스타일 시트에서 원하는 만큼 스타일을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-263">You can define as many styles as you want on a single style sheet without writing logic code to choose the style.</span></span> <span data-ttu-id="b4414-264">따라서 렌더링 용도로 중복 된 코드와 논리의 양이 줄어들기 때문에 페이지 스타일을 적용 하는 것이 매우 편리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-264">Therefore, it is a very neat way of adapting page styles, as it reduces the amount of duplicated code and logic for rendering purposes.</span></span> <span data-ttu-id="b4414-265">반면, CSS 파일의 크기는 매우 커질 수 있으므로 대역폭 소비가 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-265">On the other hand, bandwidth consumption would increase, as the size of your CSS files could grow marginally.</span></span>

<span data-ttu-id="b4414-266">적응 렌더링 기술을 사용 하 여 **브라우저에 관계 없이 사이트가 제대로 표시 됩니다.**</span><span class="sxs-lookup"><span data-stu-id="b4414-266">By using the adaptive rendering technique, your site will be **displayed properly, regardless of the browser.**</span></span> <span data-ttu-id="b4414-267">그러나 대역폭 추가 로드가 중요 한 경우를 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-267">However, you should consider if the bandwidth extra load is a concern.</span></span>

> [!NOTE]
> <span data-ttu-id="b4414-268">미디어 쿼리의 기본 형식은 @media \[범위: 모두 | 핸드헬드 | 인쇄 | 프로젝션 | 화면\] ([속성: 값] 및 ... [속성: 값])</span><span class="sxs-lookup"><span data-stu-id="b4414-268">The basic format of a media query is: @media \[Scope: all | handheld | print | projection | screen\] ([property:value] and ... [property:value])</span></span>

<span data-ttu-id="b4414-269">미디어 쿼리 예: &gt; **@media 모든 및 (최대 너비: 1000px) 및 (최소 너비: 700px) {}:** 00px와 1000px 사이의 모든 해상도</span><span class="sxs-lookup"><span data-stu-id="b4414-269">Examples of media queries: &gt;**@media all and (max-width: 1000px) and (min-width: 700px) {}:** For all the resolutions between 700px and 1000px.</span></span>

> <span data-ttu-id="b4414-270">**@media 화면 및 (최소 너비: 400px) 및 (최대 너비: 700px) {...}:** 화면에만 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-270">**@media screen and (min-width: 400px) and (max-width: 700px) { ... }:** Only for screens.</span></span> <span data-ttu-id="b4414-271">해상도는 400에서 700px 사이 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-271">The resolution must be between 400 and 700px.</span></span>
> 
> <span data-ttu-id="b4414-272">**@media 핸드헬드 및 (최소 너비: 20em), 화면 및 (최소 너비: 20em) {...}:** -핸드헬드 (모바일 및 장치) 및 화면</span><span class="sxs-lookup"><span data-stu-id="b4414-272">**@media handheld and (min-width: 20em), screen and (min-width: 20em) { ... }:** For handhelds(mobile and devices) and screens.</span></span> <span data-ttu-id="b4414-273">최소 너비는 20em 보다 커야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-273">The minimum width must be greater than 20em.</span></span>
> 
> <span data-ttu-id="b4414-274">[W3C 사이트](http://www.w3.org/TR/css3-mediaqueries/)에서이에 대 한 자세한 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-274">You can find more information about this on the [W3C site](http://www.w3.org/TR/css3-mediaqueries/).</span></span>

<span data-ttu-id="b4414-275">이제 적응 렌더링의 작동 방식을 탐색 하 여 ASP.NET MVC 4 기본 웹 사이트 템플릿의 가독성을 향상 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-275">You will now explore how the adaptive rendering works, improving the readability of the ASP.NET MVC 4 default website template.</span></span>

1. <span data-ttu-id="b4414-276">작업 1에서 만든 **사진 갤러리 .sln** 솔루션을 열고 **사진 갤러리** 프로젝트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-276">Open the **PhotoGallery.sln** solution you have created at Task 1 and select the **PhotoGallery** project.</span></span> <span data-ttu-id="b4414-277">**F5** 키를 눌러 솔루션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-277">Press **F5** to run the solution.</span></span>
2. <span data-ttu-id="b4414-278">브라우저의 너비 크기를 조정 하 여 windows를 원래 크기의 절반 또는 1/4 미만으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-278">Resize the browser's width, setting the windows to half or to less than a quarter of its original size.</span></span> <span data-ttu-id="b4414-279">헤더의 항목에 대 한 결과, 일부 요소는 머리글의 표시 영역에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-279">Notice what happens with the items in the header: Some elements will not appear in the visible area of the header.</span></span>
3. <span data-ttu-id="b4414-280">**콘텐츠** 프로젝트 폴더에 있는 Visual Studio 솔루션 탐색기에서 **사이트 .css** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-280">Open **Site.css** file from the Visual Studio Solution explorer, located in **Content** project folder.</span></span> <span data-ttu-id="b4414-281">**Ctrl + F** 를 눌러 Visual Studio 통합 검색을 열고 **CSS 미디어 쿼리**를 찾을 `@media`을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-281">Press **CTRL + F** to open Visual Studio integrated search, and write `@media` to locate the **CSS media query**.</span></span>

    <span data-ttu-id="b4414-282">이 템플릿에 정의 된 미디어 쿼리 조건은 다음과 같은 방식으로 작동 합니다. 브라우저의 창 크기가 **850 px**미만이 면 적용 되는 CSS 규칙이이 미디어 블록 내에서 정의 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-282">The media query condition defined in this template works in this way: When the browser's window size is below **850 px**, the CSS rules applied are the ones defined inside this media block.</span></span>

    <span data-ttu-id="b4414-283">![미디어 쿼리 찾기](whats-new-in-aspnet-mvc-4/_static/image16.png "미디어 쿼리 찾기")</span><span class="sxs-lookup"><span data-stu-id="b4414-283">![Locating the media query](whats-new-in-aspnet-mvc-4/_static/image16.png "Locating the media query")</span></span>

    <span data-ttu-id="b4414-284">*미디어 쿼리 찾기*</span><span class="sxs-lookup"><span data-stu-id="b4414-284">*Locating the media query*</span></span>
4. <span data-ttu-id="b4414-285">적응 렌더링을 사용 하지 않도록 설정 하기 위해 850 px에 설정 된 최대 너비 특성 값을 **10px**로 바꾸고 **CTRL + S** 를 눌러 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-285">Replace the max-width attribute value set in 850 px with **10px**, in order to disable the adaptive rendering, and press **CTRL + S** to save the changes.</span></span> <span data-ttu-id="b4414-286">브라우저로 돌아가서 **CTRL + F5** 키를 눌러 변경한 내용으로 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-286">Return to the browser and press **CTRL + F5** to refresh the page with the changes you have made.</span></span> <span data-ttu-id="b4414-287">창의 너비를 조정할 때 두 페이지의 차이점을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-287">Notice the differences in both pages when adjusting the width of the window.</span></span>

    <span data-ttu-id="b4414-288">![왼쪽의 페이지에 @media 스타일이 적용 됩니다. 오른쪽에는 스타일이 생략 됩니다.](whats-new-in-aspnet-mvc-4/_static/image17.png "왼쪽의 페이지에 @media 스타일이 적용 됩니다. 오른쪽에는 스타일이 생략 됩니다.")</span><span class="sxs-lookup"><span data-stu-id="b4414-288">![In the left, the page is applying the @media style, in the right, the style is omitted](whats-new-in-aspnet-mvc-4/_static/image17.png "In the left, the page is applying the @media style, in the right, the style is omitted")</span></span>

    <span data-ttu-id="b4414-289">*왼쪽의 페이지에 @media 스타일이 적용 됩니다. 오른쪽에는 스타일이 생략 됩니다.*</span><span class="sxs-lookup"><span data-stu-id="b4414-289">*In the left, the page is applying the @media style, in the right, the style is omitted*</span></span>

    <span data-ttu-id="b4414-290">이제 모바일 장치에서 발생 하는 상황을 확인해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-290">Now, let's check out what happens on mobile devices:</span></span>

    <span data-ttu-id="b4414-291">![왼쪽의 페이지에 @media 스타일이 적용 됩니다. 오른쪽에는 스타일이 생략 됩니다.](whats-new-in-aspnet-mvc-4/_static/image18.png "왼쪽의 페이지에 @media 스타일이 적용 됩니다. 오른쪽에는 스타일이 생략 됩니다.")</span><span class="sxs-lookup"><span data-stu-id="b4414-291">![In the left, the page is applying the @media style, in the right, the style is omitted](whats-new-in-aspnet-mvc-4/_static/image18.png "In the left, the page is applying the @media style, in the right, the style is omitted")</span></span>

    <span data-ttu-id="b4414-292">*왼쪽의 페이지에 @media 스타일이 적용 됩니다. 오른쪽에는 스타일이 생략 됩니다.*</span><span class="sxs-lookup"><span data-stu-id="b4414-292">*In the left, the page is applying the @media style, in the right, the style is omitted*</span></span>

    <span data-ttu-id="b4414-293">웹 브라우저에서 페이지가 렌더링 되는 경우 변경 내용이 그다지 중요 하지 않지만 모바일 장치를 사용 하는 경우 차이가 더 분명해 집니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-293">Although you will notice that the changes when the page is rendered in a Web browser are not very significant, when using a mobile device the differences become more obvious.</span></span> <span data-ttu-id="b4414-294">이미지의 왼쪽에서 사용자 지정 스타일의 가독성을 향상 시키는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-294">On the left side of the image, we can see that the custom style improved the readability.</span></span>

    <span data-ttu-id="b4414-295">적응 렌더링은 다양 한 시나리오에서 사용 될 수 있으므로, 웹 사이트에 조건부 스타일을 보다 쉽게 적용 하 고 다양 한 방식으로 일반적인 스타일 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-295">Adaptive rendering can be used in many more scenarios, making it easier to apply conditional styling to a Web site and solving common style issues with a neat approach.</span></span>

    <span data-ttu-id="b4414-296">뷰포트 메타 태그 및 CSS 미디어 쿼리는 ASP.NET MVC 4에 한정 되지 않으므로 모든 웹 응용 프로그램에서 이러한 기능을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-296">The Viewport meta tag and CSS media queries are not specific to ASP.NET MVC 4, so you can take advantage of these features in any web application.</span></span>
5. <span data-ttu-id="b4414-297">Visual Studio에서 **SHIFT** + **f5** 키를 눌러 응용 프로그램 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-297">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_the_Photo_Gallery_Web_Application"></a>
### <a name="exercise-2-creating-the-photo-gallery-web-application"></a><span data-ttu-id="b4414-298">연습 2: 사진 갤러리 웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="b4414-298">Exercise 2: Creating the Photo Gallery Web Application</span></span>

<span data-ttu-id="b4414-299">이 연습에서는 사진 갤러리 응용 프로그램에 대 한 작업을 수행 하 여 사진을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-299">In this exercise, you will work on a Photo Gallery application to display photos.</span></span> <span data-ttu-id="b4414-300">ASP.NET MVC 4 프로젝트 템플릿으로 시작 하 고 서비스에서 사진을 검색 하 고 홈 페이지에 표시 하는 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-300">You will start with the ASP.NET MVC 4 project template, and then you will add a feature to retrieve photos from a service and display them in the home page.</span></span>

<span data-ttu-id="b4414-301">다음 연습에서는이 솔루션을 업데이트 하 여 모바일 장치에 표시 되는 방법을 개선 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-301">In the following exercise, you will update this solution to enhance the way it is displayed on mobile devices.</span></span>

<a id="Task_1_-_Creating_a_Mock_Photo_Service"></a>
#### <a name="task-1---creating-a-mock-photo-service"></a><span data-ttu-id="b4414-302">작업 1-모의 사진 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="b4414-302">Task 1 - Creating a Mock Photo Service</span></span>

<span data-ttu-id="b4414-303">이 작업에서는 갤러리에 표시 되는 콘텐츠를 검색 하는 사진 서비스의 모의를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-303">In this task, you will create a mock of the photo service to retrieve the content that will be displayed in the gallery.</span></span> <span data-ttu-id="b4414-304">이렇게 하려면 각 사진의 데이터를 사용 하 여 JSON 파일을 단순히 반환 하는 새 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-304">To do this, you will add a new controller that will simply return a JSON file with the data of each photo.</span></span>

1. <span data-ttu-id="b4414-305">아직 열려 있지 않은 경우 **Visual Studio** 를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-305">Open **Visual Studio** if not already opened.</span></span>
2. <span data-ttu-id="b4414-306">파일을 선택 합니다. **| 새로 만들기 | 프로젝트** 메뉴 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-306">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="b4414-307">**새 프로젝트** 대화 상자에서 **시각적 개체 C# | 웹** 템플릿 왼쪽 창에서 **ASP.NET MVC 4 웹 응용 프로그램을 선택 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b4414-307">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="b4414-308">프로젝트 이름을 **사진**으로 지정 하 고 위치를 선택 하거나 기본값을 그대로 두고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-308">Name the project **PhotoGallery**, select a location (or leave the default) and click **OK**.</span></span> <span data-ttu-id="b4414-309">또는 **실습 1** 에서 기존 ASP.NET MVC 4 **인터넷 응용 프로그램** 솔루션의 작업을 계속 진행 하 고 다음 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-309">Alternatively, you can continue working from your existing ASP.NET MVC 4 **Internet Application** solution from **Exercise 1** and skip the next step.</span></span>
3. <span data-ttu-id="b4414-310">**새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **인터넷 응용 프로그램** 프로젝트 템플릿을 선택 하 고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-310">In the **New ASP.NET MVC 4 Project** dialog box, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="b4414-311">뷰 엔진으로 Razor가 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-311">Make sure you have Razor selected as the View Engine.</span></span>
4. <span data-ttu-id="b4414-312">**솔루션 탐색기**에서 프로젝트의 **App\_Data** 폴더를 마우스 오른쪽 단추로 클릭 하 고 추가 |를 선택 합니다.  **기존 항목**입니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-312">In the **Solution Explorer**, right-click the **App\_Data** folder of your project, and select **Add | Existing Item**.</span></span> <span data-ttu-id="b4414-313">이 랩의 **Source\assets\app\_Data** 폴더로 이동 하 여 **사진의 json** 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-313">Browse to the **Source\Assets\App\_Data** folder of this lab and add the **Photos.json** file.</span></span>
5. <span data-ttu-id="b4414-314">이름으로 **사진 컨트롤러**를 사용 하 여 새 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-314">Create a new controller with the name **PhotoController**.</span></span> <span data-ttu-id="b4414-315">이렇게 하려면 **Controllers** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** 로 이동한 후 컨트롤러를 선택 **합니다.**</span><span class="sxs-lookup"><span data-stu-id="b4414-315">To do this, right-click on the **Controllers** folder, go to **Add** and select **Controller.**</span></span> <span data-ttu-id="b4414-316">컨트롤러 이름을 완료 하 고 **빈 MVC 컨트롤러** 템플릿을 그대로 두고 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-316">Complete the controller name, leave the **Empty MVC controller** template and click **Add**.</span></span>

    <span data-ttu-id="b4414-317">![사진 컨트롤러 추가](whats-new-in-aspnet-mvc-4/_static/image19.png "사진 컨트롤러 추가")</span><span class="sxs-lookup"><span data-stu-id="b4414-317">![Adding the PhotoController](whats-new-in-aspnet-mvc-4/_static/image19.png "Adding the PhotoController")</span></span>

    <span data-ttu-id="b4414-318">*사진 컨트롤러 추가*</span><span class="sxs-lookup"><span data-stu-id="b4414-318">*Adding the PhotoController*</span></span>
6. <span data-ttu-id="b4414-319">**Index** 메서드를 다음 **갤러리** 작업으로 바꾸고 최근에 프로젝트에 추가한 JSON 파일의 콘텐츠를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-319">Replace the **Index** method with the following **Gallery** action, and return the content from the JSON file you have recently added to the project.</span></span>

    <span data-ttu-id="b4414-320">(코드 조각- *ASP.NET MVC 4 Lab-Ex02-갤러리 동작*)</span><span class="sxs-lookup"><span data-stu-id="b4414-320">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Gallery Action*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample4.cs)]
7. <span data-ttu-id="b4414-321">**F5** 키를 눌러 솔루션을 실행 하 고 모의 photo 서비스를 테스트 하기 위해 다음 URL로 이동 합니다. `http://localhost:[port]/photo/gallery` ([port] 값은 응용 프로그램이 시작 된 현재 포트에 따라 달라 짐)</span><span class="sxs-lookup"><span data-stu-id="b4414-321">Press **F5** to run the solution, and then browse to the following URL in order to test the mocked photo service: `http://localhost:[port]/photo/gallery` (the [port] value depends on the current port where the application was launched).</span></span> <span data-ttu-id="b4414-322">이 URL에 대 한 요청은 **사진. json** 파일의 콘텐츠를 검색 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-322">The request to this URL should retrieve the content of the **Photos.json** file.</span></span>

    <span data-ttu-id="b4414-323">![모의 photo 서비스 테스트](whats-new-in-aspnet-mvc-4/_static/image20.png "모의 photo 서비스 테스트")</span><span class="sxs-lookup"><span data-stu-id="b4414-323">![Testing the mocked photo service](whats-new-in-aspnet-mvc-4/_static/image20.png "Testing the mocked photo service")</span></span>

    <span data-ttu-id="b4414-324">*모의 photo 서비스 테스트*</span><span class="sxs-lookup"><span data-stu-id="b4414-324">*Testing the mocked photo service*</span></span>

<span data-ttu-id="b4414-325">실제 구현에서는 [ASP.NET Web API](../../../../web-api/index.md) 를 사용 하 여 사진 갤러리 서비스를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-325">In a real implementation you could use [ASP.NET Web API](../../../../web-api/index.md) to implement the Photo Gallery service.</span></span> <span data-ttu-id="b4414-326">ASP.NET Web API은 브라우저 및 모바일 장치를 비롯 한 광범위 한 클라이언트에 연결 되는 HTTP 서비스를 쉽게 빌드할 수 있게 해 주는 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-326">ASP.NET Web API is a framework that makes it easy to build HTTP services that reach a broad range of clients, including browsers and mobile devices.</span></span> <span data-ttu-id="b4414-327">ASP.NET Web API 是用于在 .NET Framework 上生成 RESTful 应用程序的理想平台。</span><span class="sxs-lookup"><span data-stu-id="b4414-327">ASP.NET Web API is an ideal platform for building RESTful applications on the .NET Framework.</span></span>

<a id="Task_2_-_Displaying_the_Photo_Gallery"></a>
#### <a name="task-2---displaying-the-photo-gallery"></a><span data-ttu-id="b4414-328">작업 2-사진 갤러리 표시</span><span class="sxs-lookup"><span data-stu-id="b4414-328">Task 2 - Displaying the Photo Gallery</span></span>

<span data-ttu-id="b4414-329">이 작업에서는이 연습의 첫 번째 작업에서 만든 모의 서비스를 사용 하 여 사진 갤러리를 표시 하도록 홈 페이지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-329">In this task, you will update the Home page to show the photo gallery by using the mocked service you created in the first task of this exercise.</span></span> <span data-ttu-id="b4414-330">모델 파일을 추가 하 고 갤러리 뷰를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-330">You will add model files and update the gallery views.</span></span>

1. <span data-ttu-id="b4414-331">Visual Studio에서 **SHIFT** + **f5** 키를 눌러 응용 프로그램 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-331">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
2. <span data-ttu-id="b4414-332">**모델** 폴더에서 **Photo** 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-332">Create the **Photo** class in the **Models** folder.</span></span> <span data-ttu-id="b4414-333">이렇게 하려면 **모델** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** 를 선택한 다음 **클래스**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-333">To do this, right-click on the **Models** folder, select **Add** and click **Class**.</span></span> <span data-ttu-id="b4414-334">그런 다음 이름을 **Photo.cs** 로 설정 하 고 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-334">Then, set the name to **Photo.cs** and click **Add**.</span></span>
3. <span data-ttu-id="b4414-335">**Photo** 클래스에 다음 멤버를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-335">Add the following members to the **Photo** class.</span></span>

    <span data-ttu-id="b4414-336">(코드 조각- *ASP.NET MVC 4 Lab-Ex02-Photo model*)</span><span class="sxs-lookup"><span data-stu-id="b4414-336">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Photo model*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample5.cs)]
4. <span data-ttu-id="b4414-337">从“控制器”文件夹打开 HomeController.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="b4414-337">Open the **HomeController.cs** file from the **Controllers** folder.</span></span>
5. <span data-ttu-id="b4414-338">添加下面的 using 语句。</span><span class="sxs-lookup"><span data-stu-id="b4414-338">Add the following using statements.</span></span>

    <span data-ttu-id="b4414-339">(코드 조각- *ASP.NET MVC 4 Lab-Ex02-HomeController using*)</span><span class="sxs-lookup"><span data-stu-id="b4414-339">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - HomeController Usings*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample6.cs)]
6. <span data-ttu-id="b4414-340">**Httpclient** 를 사용 하 여 갤러리 데이터를 검색 한 다음 **JavaScriptSerializer** 를 사용 하 여 뷰 모델로 deserialize 하는 **인덱스** 작업을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-340">Update the **Index** action to use **HttpClient** to retrieve the gallery data, and then use the **JavaScriptSerializer** to deserialize it to the view model.</span></span>

    <span data-ttu-id="b4414-341">(코드 조각- *ASP.NET MVC 4 Lab-Ex02 동작*)</span><span class="sxs-lookup"><span data-stu-id="b4414-341">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Index Action*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample7.cs)]
7. <span data-ttu-id="b4414-342">**Views\Home** 폴더 **아래에 있는 파일을** 열고 모든 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-342">Open the **Index.cshtml** file located under the **Views\Home** folder and replace all the content with the following code.</span></span>

    <span data-ttu-id="b4414-343">이 코드는 서비스에서 검색 된 모든 사진을 반복 하 여 순서가 지정 되지 않은 목록으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-343">This code loops through all the photos retrieved from the service and displays them into an unordered list.</span></span>

    <span data-ttu-id="b4414-344">(코드 조각- *ASP.NET MVC 4 Lab-Ex02-Photo List*)</span><span class="sxs-lookup"><span data-stu-id="b4414-344">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Photo List*)</span></span>

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample8.cshtml)]
8. <span data-ttu-id="b4414-345">**솔루션 탐색기**에서 프로젝트의 **콘텐츠** 폴더를 마우스 오른쪽 단추로 클릭 하 고 추가 |를 선택 합니다.  **기존 항목**입니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-345">In the **Solution Explorer**, right-click the **Content** folder of your project, and select **Add | Existing Item**.</span></span> <span data-ttu-id="b4414-346">이 랩의 **Source\assets\content** 폴더로 이동 하 여 **사이트 .css** 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-346">Browse to the **Source\Assets\Content** folder of this lab and add the **Site.css** file.</span></span> <span data-ttu-id="b4414-347">교체를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-347">You will have to confirm its replacement.</span></span> <span data-ttu-id="b4414-348">**사이트 .css** 파일이 열려 있는 경우에도 파일을 다시 로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-348">If you have the **Site.css** file open, you will have to confirm to reload the file also.</span></span>
9. <span data-ttu-id="b4414-349">파일 탐색기를 열고이 랩의 **Source\assets** 폴더 아래에 있는 전체 **사진** 폴더를 솔루션 탐색기 프로젝트의 루트 폴더에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-349">Open File Explorer and copy the entire **Photos** folder located under the **Source\Assets** folder of this lab to the root folder of your project in Solution Explorer.</span></span>
10. <span data-ttu-id="b4414-350">运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="b4414-350">Run the application.</span></span> <span data-ttu-id="b4414-351">이제 갤러리에 사진을 표시 하는 홈 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-351">You should now see the home page displaying the photos in the gallery.</span></span>

    <span data-ttu-id="b4414-352">![사진 갤러리](whats-new-in-aspnet-mvc-4/_static/image21.png "사진 갤러리")</span><span class="sxs-lookup"><span data-stu-id="b4414-352">![Photo Gallery](whats-new-in-aspnet-mvc-4/_static/image21.png "Photo Gallery")</span></span>

    <span data-ttu-id="b4414-353">*사진 갤러리*</span><span class="sxs-lookup"><span data-stu-id="b4414-353">*Photo Gallery*</span></span>
11. <span data-ttu-id="b4414-354">Visual Studio에서 **SHIFT** + **f5** 키를 눌러 응용 프로그램 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-354">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Adding_support_for_mobile_devices"></a>
### <a name="exercise-3-adding-support-for-mobile-devices"></a><span data-ttu-id="b4414-355">연습 3: 모바일 장치에 대 한 지원 추가</span><span class="sxs-lookup"><span data-stu-id="b4414-355">Exercise 3: Adding support for mobile devices</span></span>

<span data-ttu-id="b4414-356">ASP.NET MVC 4의 주요 업데이트 중 하나는 모바일 개발에 대 한 지원입니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-356">One of the key updates in ASP.NET MVC 4 is the support for mobile development.</span></span> <span data-ttu-id="b4414-357">이 연습에서는 이전 연습에서 만든 사진 갤러리 솔루션을 확장 하 여 모바일 응용 프로그램에 대 한 ASP.NET MVC 4 new 기능을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-357">In this exercise, you will explore ASP.NET MVC 4 new features for mobile applications by extending the PhotoGallery solution you have created in the previous exercise.</span></span>

<a id="Task_1_-_Installing_jQuery_Mobile_in_an_ASPNET_MVC_4_Application"></a>
#### <a name="task-1---installing-jquery-mobile-in-an-aspnet-mvc-4-application"></a><span data-ttu-id="b4414-358">작업 1-ASP.NET MVC 4 응용 프로그램에 jQuery Mobile 설치</span><span class="sxs-lookup"><span data-stu-id="b4414-358">Task 1 - Installing jQuery Mobile in an ASP.NET MVC 4 Application</span></span>

1. <span data-ttu-id="b4414-359">**Source/Ex3-MobileSupport/begin/** 폴더에 있는 **시작** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-359">Open the **Begin** solution located at **Source/Ex3-MobileSupport/Begin/** folder.</span></span> <span data-ttu-id="b4414-360">그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-360">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="b4414-361">제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-361">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="b4414-362">이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-362">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="b4414-363">**NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-363">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="b4414-364">마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-364">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="b4414-365">NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-365">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="b4414-366">NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-366">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="b4414-367">이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-367">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="b4414-368">**NuGet 패키지 관리자** > **패키지 관리자 콘솔** 메뉴 옵션 > **도구** 를 클릭 하 여 **패키지 관리자 콘솔** 을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-368">Open the **Package Manager Console** by clicking the **Tools** > **NuGet Package Manager** > **Package Manager Console** menu option.</span></span>

    <span data-ttu-id="b4414-369">![NuGet 패키지 관리자 콘솔 열기](whats-new-in-aspnet-mvc-4/_static/image22.png "NuGet 패키지 관리자 콘솔 열기")</span><span class="sxs-lookup"><span data-stu-id="b4414-369">![Opening the NuGet Package Manager Console](whats-new-in-aspnet-mvc-4/_static/image22.png "Opening the NuGet Package Manager Console")</span></span>

    <span data-ttu-id="b4414-370">*NuGet 패키지 관리자 콘솔 열기*</span><span class="sxs-lookup"><span data-stu-id="b4414-370">*Opening the NuGet Package Manager Console*</span></span>
3. <span data-ttu-id="b4414-371">패키지 관리자 콘솔에서 다음 명령을 실행 하 여 **jQuery** 를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-371">In the Package Manager Console run the following command to install the **jQuery.Mobile.MVC** package.</span></span>

    <span data-ttu-id="b4414-372">jQuery Mobile은 터치에 최적화 된 웹 UI를 빌드하기 위한 오픈 소스 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-372">jQuery Mobile is an open source library for building touch-optimized web UI.</span></span> <span data-ttu-id="b4414-373">ASP.NET MVC 4 응용 프로그램과 함께 jQuery Mobile을 사용 하는 도우미가 jQuery의 NuGet 패키지에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-373">The jQuery.Mobile.MVC NuGet package includes helpers to use jQuery Mobile with an ASP.NET MVC 4 application.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b4414-374">다음 명령을 실행 하 여 Nuget에서 jQuery. MVC 라이브러리를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-374">By running the following command, you will be downloading the jQuery.Mobile.MVC library from Nuget.</span></span>

    <span data-ttu-id="b4414-375">PM</span><span class="sxs-lookup"><span data-stu-id="b4414-375">PM</span></span>

    [!code-powershell[Main](whats-new-in-aspnet-mvc-4/samples/sample9.ps1)]

    <span data-ttu-id="b4414-376">이 명령은 다음을 포함 하 여 jQuery Mobile 및 일부 도우미 파일을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-376">This command installs jQuery Mobile and some helper files, including the following:</span></span>

    - <span data-ttu-id="b4414-377">**Views/Shared/\_layout. cshtml**: 더 작은 화면에 최적화 된 jQuery 모바일 기반 레이아웃입니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-377">**Views/Shared/\_Layout.Mobile.cshtml**: is a jQuery Mobile-based layout optimized for a smaller screen.</span></span> <span data-ttu-id="b4414-378">웹 사이트는 모바일 브라우저에서 요청을 받으면 원래 레이아웃 (\_레이아웃. cshtml)을이 항목으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-378">When the website receives a request from a mobile browser, it will replace the original layout (\_Layout.cshtml) with this one.</span></span>
    - <span data-ttu-id="b4414-379">뷰 전환기 구성 요소: **Views/Shared/\_ViewSwitcher** 로 구성 됩니다. cshtml 부분 뷰와 **ViewSwitcherController.cs** controller</span><span class="sxs-lookup"><span data-stu-id="b4414-379">A view-switcher component: consists of the **Views/Shared/\_ViewSwitcher.cshtml** partial view and the **ViewSwitcherController.cs** controller.</span></span> <span data-ttu-id="b4414-380">이 구성 요소는 사용자가 페이지의 데스크톱 버전으로 전환 하는 데 사용할 수 있는 모바일 브라우저의 링크를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-380">This component will show a link on mobile browsers to enable users to switch to the desktop version of the page.</span></span>  
        <span data-ttu-id="b4414-381">![모바일 지원이 있는 사진 갤러리 프로젝트](whats-new-in-aspnet-mvc-4/_static/image23.png "Ph모바일 지원이 있는 o Gallery 프로젝트 ")</span><span class="sxs-lookup"><span data-stu-id="b4414-381">![Photo Gallery project with mobile support](whats-new-in-aspnet-mvc-4/_static/image23.png "Photo Gallery project with mobile support")</span></span>

        <span data-ttu-id="b4414-382">*모바일 지원이 있는 사진 갤러리 프로젝트*</span><span class="sxs-lookup"><span data-stu-id="b4414-382">*Photo Gallery project with mobile support*</span></span>
4. <span data-ttu-id="b4414-383">모바일 번들을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-383">Register the Mobile bundles.</span></span> <span data-ttu-id="b4414-384">이렇게 하려면 **Global.asax.cs** 파일을 열고 다음 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-384">To do this, open the **Global.asax.cs** file and add the following line.</span></span>

    <span data-ttu-id="b4414-385">(코드 조각- *ASP.NET MVC 4 Lab-Ex03-Register Mobile 번들*)</span><span class="sxs-lookup"><span data-stu-id="b4414-385">(Code Snippet - *ASP.NET MVC 4 Lab - Ex03 - Register Mobile Bundles*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample10.cs)]
5. <span data-ttu-id="b4414-386">데스크톱 웹 브라우저를 사용 하 여 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-386">Run the application using a desktop web browser.</span></span>
6. <span data-ttu-id="b4414-387">시작 메뉴에 있는 **Windows Phone 7 에뮬레이터를** 엽니다. **| 모든 프로그램 | Windows Phone SDK 7.1 | 에뮬레이터를 Windows Phone 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b4414-387">Open the **Windows Phone 7 Emulator,** located in **Start Menu | All Programs | Windows Phone SDK 7.1 | Windows Phone Emulator.**</span></span>
7. <span data-ttu-id="b4414-388">휴대폰 시작 화면에서 Internet Explorer를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-388">In the phone start screen, open Internet Explorer.</span></span> <span data-ttu-id="b4414-389">응용 프로그램이 시작 된 URL을 확인 하 고 휴대폰 브라우저 (예: `http://localhost:[PortNumber]/`)를 사용 하 여 해당 URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-389">Check out the URL where the application started and browse to that URL with the phone browser (e.g. `http://localhost:[PortNumber]/`).</span></span>

    <span data-ttu-id="b4414-390">응용 프로그램이 Windows Phone 에뮬레이터에서 다르게 표시 되는 것을 확인할 수 있습니다 .이는 응용 프로그램이 모바일 장치에 대해 최적화 된 보기를 표시 하는 프로젝트에서 새 자산을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-390">You will notice that your application will look different in the Windows Phone emulator, as the jQuery.Mobile.MVC has created new assets in your project that show views optimized for mobile devices.</span></span>

    <span data-ttu-id="b4414-391">휴대폰의 위쪽에 있는 메시지를 확인 하 고 바탕 화면 보기로 전환 되는 링크를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-391">Notice the message at the top of the phone, showing the link that switches to the Desktop view.</span></span> <span data-ttu-id="b4414-392">또한 사용자가 설치한 패키지에서 만든 **\_레이아웃** 은 응용 프로그램에 다른 레이아웃을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-392">Additionally, the **\_Layout.Mobile.cshtml** layout that was created by the package you have installed is including a different layout in the application.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b4414-393">지금까지 모바일 보기로 돌아갈 수 있는 링크가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-393">So far, there is no link to get back to mobile view.</span></span> <span data-ttu-id="b4414-394">이후 버전에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-394">It will be included in later versions.</span></span>

    <span data-ttu-id="b4414-395">![사진 갤러리 홈 페이지의 모바일 보기](whats-new-in-aspnet-mvc-4/_static/image24.png "사진 갤러리 홈 페이지의 모바일 보기")</span><span class="sxs-lookup"><span data-stu-id="b4414-395">![Mobile view of the Photo Gallery Home page](whats-new-in-aspnet-mvc-4/_static/image24.png "Mobile view of the Photo Gallery Home page")</span></span>

    <span data-ttu-id="b4414-396">*사진 갤러리 홈 페이지의 모바일 보기*</span><span class="sxs-lookup"><span data-stu-id="b4414-396">*Mobile view of the Photo Gallery Home page*</span></span>
8. <span data-ttu-id="b4414-397">Visual Studio에서 **SHIFT** + **f5** 키를 눌러 응용 프로그램 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-397">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Task_2_-_Creating_Mobile_Views"></a>
#### <a name="task-2---creating-mobile-views"></a><span data-ttu-id="b4414-398">작업 2-모바일 보기 만들기</span><span class="sxs-lookup"><span data-stu-id="b4414-398">Task 2 - Creating Mobile Views</span></span>

<span data-ttu-id="b4414-399">이 작업에서는 모바일 장치에서 더 나은 모양을 위해 콘텐츠를 조정 하 여 인덱스 보기의 모바일 버전을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-399">In this task, you will create a mobile version of the index view with content adapted for better appearance in mobile devices.</span></span>

1. <span data-ttu-id="b4414-400">**Views\Home\Index.cshtml** view를 복사 하 여 붙여넣어 복사본을 만들고 새 파일의 이름을 **Index. Mobile. cshtml**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-400">Copy the **Views\Home\Index.cshtml** view and paste it to create a copy, rename the new file to **Index.Mobile.cshtml**.</span></span>
2. <span data-ttu-id="b4414-401">새로 만든 **Index. Mobile. cshtml** 뷰를 열고 기존 &lt;ul&gt; 태그를이 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-401">Open the new created **Index.Mobile.cshtml** view and replace the existing &lt;ul&gt; tag with this code.</span></span> <span data-ttu-id="b4414-402">이 작업을 수행 하 여 jQuery의 모바일 테마를 사용 하도록 jQuery Mobile 데이터 주석과 &lt;ul&gt; 태그를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-402">By doing this, you will be updating the &lt;ul&gt; tag with jQuery Mobile data annotations to use the mobile themes from jQuery.</span></span>

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample11.html)]

    > [!NOTE] 
    > 
    > <span data-ttu-id="b4414-403">请注意：</span><span class="sxs-lookup"><span data-stu-id="b4414-403">Notice that:</span></span>
    > 
    > - <span data-ttu-id="b4414-404">**Listview** 로 설정 된 **데이터 역할** 특성은 listview 스타일을 사용 하 여 목록을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-404">The **data-role** attribute set to **listview** will render the list using the listview styles.</span></span>
    > 
    > - <span data-ttu-id="b4414-405">**데이터 인세트** 특성을 true로 설정 하면 모퉁이가 둥근 테두리와 여백이 있는 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-405">The **data-inset** attribute set to true will show the list with rounded border and margin.</span></span>
    > 
    > - <span data-ttu-id="b4414-406">**데이터 필터** 특성을 **true** 로 설정 하면 검색 상자가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-406">The **data-filter** attribute set to **true** will generate a search box.</span></span>
    > 
    > <span data-ttu-id="b4414-407">프로젝트 설명서에서 jQuery 모바일 규칙에 대해 자세히 알아볼 수 있습니다. [ [http://jquerymobile.com/demos/1.1.1/](http://jquerymobile.com/demos/1.1.1/)](http://jquerymobile.com/demos/1.1.1/)</span><span class="sxs-lookup"><span data-stu-id="b4414-407">You can learn more about jQuery Mobile conventions in the project documentation: [[http://jquerymobile.com/demos/1.1.1/](http://jquerymobile.com/demos/1.1.1/)](http://jquerymobile.com/demos/1.1.1/)</span></span>
3. <span data-ttu-id="b4414-408">**Ctrl + S** 를 눌러 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-408">Press **CTRL + S** to save the changes.</span></span>
4. <span data-ttu-id="b4414-409">**Windows Phone Emulator** 로 전환 하 고 사이트를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-409">Switch to the **Windows Phone Emulator** and refresh the site.</span></span> <span data-ttu-id="b4414-410">갤러리 목록의 새로운 모양과 느낌 뿐만 아니라 맨 위에 있는 새 검색 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-410">Notice the new look and feel of the gallery list, as well as the new search box located on the top.</span></span> <span data-ttu-id="b4414-411">그런 다음 검색 상자 (예 **Tulips**)에 단어를 입력 하 여 사진 갤러리에서 검색을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-411">Then, type a word in the search box (for instance, **Tulips**) to start a search in the photo gallery.</span></span>

    <span data-ttu-id="b4414-412">![필터링과 함께 listview 스타일을 사용 하는 갤러리](whats-new-in-aspnet-mvc-4/_static/image25.png "필터링과 함께 listview 스타일을 사용 하는 갤러리")</span><span class="sxs-lookup"><span data-stu-id="b4414-412">![Gallery using listview style with filtering](whats-new-in-aspnet-mvc-4/_static/image25.png "Gallery using listview style with filtering")</span></span>

    <span data-ttu-id="b4414-413">*필터링과 함께 listview 스타일을 사용 하는 갤러리*</span><span class="sxs-lookup"><span data-stu-id="b4414-413">*Gallery using listview style with filtering*</span></span>

    <span data-ttu-id="b4414-414">요약 하면 View Mobilizer 조리법을 사용 하 여 &quot;mobile&quot; 접미사로 인덱스 보기의 복사본을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-414">To summarize, you have used the View Mobilizer recipe to create a copy of the Index view with the &quot;mobile&quot; suffix.</span></span> <span data-ttu-id="b4414-415">이 접미사는 ASP.NET MVC 4를 나타냅니다. 모바일 장치에서 생성 된 모든 요청은이 인덱스 복사본을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-415">This suffix indicates to ASP.NET MVC 4 that every request generated from a mobile device will use this copy of the index.</span></span> <span data-ttu-id="b4414-416">또한 모바일 장치의 사이트 모양과 느낌을 향상 시키기 위해 jQuery Mobile을 사용 하도록 인덱스 뷰의 모바일 버전을 업데이트 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-416">Additionally, you have updated the mobile version of the Index view to use jQuery Mobile for enhancing the site look and feel in mobile devices.</span></span>
5. <span data-ttu-id="b4414-417">Visual Studio로 돌아가서 **Content** 폴더 아래에 있는 **사이트별** 를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-417">Go back to Visual Studio and open **Site.Mobile.css** located under the **Content** folder.</span></span>
6. <span data-ttu-id="b4414-418">사진 제목의 위치를 수정 하 여 이미지의 오른쪽에 표시 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-418">Fix the positioning of the photo title to make it show at the right side of the image.</span></span> <span data-ttu-id="b4414-419">이렇게 하려면 다음 코드를 **사이트. Mobile .css** 파일에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-419">To do this, add the following code to the **Site.Mobile.css** file.</span></span>

    <span data-ttu-id="b4414-420">CSS</span><span class="sxs-lookup"><span data-stu-id="b4414-420">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-mvc-4/samples/sample12.css)]
7. <span data-ttu-id="b4414-421">**Ctrl + S** 를 눌러 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-421">Press **CTRL + S** to save the changes.</span></span>
8. <span data-ttu-id="b4414-422">**Windows Phone 에뮬레이터** 로 다시 전환 하 고 사이트를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-422">Switch back to the **Windows Phone Emulator** and refresh the site.</span></span> <span data-ttu-id="b4414-423">이제 사진 제목을 올바른 위치에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-423">Notice the photo title is properly positioned now.</span></span>

    <span data-ttu-id="b4414-424">![이미지 오른쪽에 배치 된 제목](whats-new-in-aspnet-mvc-4/_static/image26.png "이미지 오른쪽에 배치 된 제목")</span><span class="sxs-lookup"><span data-stu-id="b4414-424">![Title positioned on the right side of the image](whats-new-in-aspnet-mvc-4/_static/image26.png "Title positioned on the right side of the image")</span></span>

    <span data-ttu-id="b4414-425">*이미지 오른쪽에 배치 된 제목*</span><span class="sxs-lookup"><span data-stu-id="b4414-425">*Title positioned on the right side of the image*</span></span>

<a id="Task_3_-_jQuery_Mobile_Themes"></a>
#### <a name="task-3---jquery-mobile-themes"></a><span data-ttu-id="b4414-426">작업 3-jQuery 모바일 테마</span><span class="sxs-lookup"><span data-stu-id="b4414-426">Task 3 - jQuery Mobile Themes</span></span>

<span data-ttu-id="b4414-427">JQuery Mobile의 모든 레이아웃 및 위젯은 새로운 개체 지향 CSS 프레임 워크를 중심으로 디자인 되어 사이트 및 응용 프로그램에 완전 한 통합 시각적 디자인 테마를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-427">Every layout and widget in jQuery Mobile is designed around a new object-oriented CSS framework that makes it possible to apply a complete unified visual design theme to sites and applications.</span></span>

<span data-ttu-id="b4414-428">jQuery Mobile의 기본 테마는 빠른 참조를 위해 문자 (a, b, c, d, e)가 지정 된 5 개의 견본을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-428">jQuery Mobile's default Theme includes 5 swatches that are given letters (a, b, c, d, e) for quick reference.</span></span>

<span data-ttu-id="b4414-429">이 작업에서는 기본값과 다른 테마를 사용 하도록 모바일 레이아웃을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-429">In this task, you will update the mobile layout to use a different theme than the default.</span></span>

1. <span data-ttu-id="b4414-430">Visual Studio로 다시 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-430">Switch back to Visual Studio.</span></span>
2. <span data-ttu-id="b4414-431">Views\Shared에 있는 **\_Layout.** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-431">Open the **\_Layout.Mobile.cshtml** file located in **Views\Shared**.</span></span>
3. <span data-ttu-id="b4414-432">&quot;페이지&quot;으로 설정 된 데이터 역할의 div 요소를 찾고 **데이터 테마** 를 &quot;**e**&quot;로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-432">Find the div element with the data-role set to &quot;page&quot; and update the **data-theme** to &quot;**e**&quot;.</span></span>

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample13.html)]
4. <span data-ttu-id="b4414-433">**Ctrl + S** 를 눌러 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-433">Press **CTRL + S** to save the changes.</span></span>
5. <span data-ttu-id="b4414-434">**Windows Phone 에뮬레이터** 에서 사이트를 새로 고치고 새 색 구성표를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-434">Refresh the site in the **Windows Phone Emulator** and notice the new colors scheme.</span></span>

    <span data-ttu-id="b4414-435">![다른 색 구성표를 사용 하는 모바일 레이아웃](whats-new-in-aspnet-mvc-4/_static/image27.png "다른 색 구성표를 사용 하는 모바일 레이아웃")</span><span class="sxs-lookup"><span data-stu-id="b4414-435">![Mobile layout with a different color scheme](whats-new-in-aspnet-mvc-4/_static/image27.png "Mobile layout with a different color scheme")</span></span>

    <span data-ttu-id="b4414-436">*다른 색 구성표를 사용 하는 모바일 레이아웃*</span><span class="sxs-lookup"><span data-stu-id="b4414-436">*Mobile layout with a different color scheme*</span></span>

<a id="Task_4_-_Using_the_View-Switcher_Component_and_the_Browser_Overriding_Features"></a>
#### <a name="task-4---using-the-view-switcher-component-and-the-browser-overriding-features"></a><span data-ttu-id="b4414-437">작업 4-뷰 전환기 구성 요소 및 브라우저 재정의 기능 사용</span><span class="sxs-lookup"><span data-stu-id="b4414-437">Task 4 - Using the View-Switcher Component and the Browser Overriding Features</span></span>

<span data-ttu-id="b4414-438">모바일 최적화 웹 페이지의 규칙은 사용자가 페이지의 데스크톱 버전으로 전환할 수 있는 바탕 화면 보기 또는 전체 사이트 모드와 같은 텍스트를 포함 하는 링크를 추가 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-438">A convention for mobile-optimized web pages is to add a link whose text is something like Desktop view or Full site mode that lets users switch to a desktop version of the page.</span></span> <span data-ttu-id="b4414-439">JQuery. Mobile. i n a. i n a. i n. i n **\_** a.</span><span class="sxs-lookup"><span data-stu-id="b4414-439">The jQuery.Mobile.MVC package includes a sample **view-switcher** component for this purpose used in the **\_Layout.Mobile.cshtml** view.</span></span>

<span data-ttu-id="b4414-440">![바탕 화면 뷰로 전환 하기 위한 링크](whats-new-in-aspnet-mvc-4/_static/image28.png "바탕 화면 뷰로 전환 하기 위한 링크")</span><span class="sxs-lookup"><span data-stu-id="b4414-440">![Link to switch to Desktop View](whats-new-in-aspnet-mvc-4/_static/image28.png "Link to switch to Desktop View")</span></span>

<span data-ttu-id="b4414-441">*바탕 화면 뷰로 전환 하기 위한 링크*</span><span class="sxs-lookup"><span data-stu-id="b4414-441">*Link to switch to Desktop View*</span></span>

<span data-ttu-id="b4414-442">뷰 전환기는 **브라우저 재정의**라는 새로운 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-442">The view switcher uses a new feature called **Browser Overriding**.</span></span> <span data-ttu-id="b4414-443">이 기능을 사용 하면 응용 프로그램이 실제로 제공 되는 것과 다른 브라우저 (사용자 에이전트)에서 오는 것 처럼 요청을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-443">This feature lets your application treat requests as if they were coming from a different browser (user agent) than the one they are actually coming from.</span></span>

<span data-ttu-id="b4414-444">이 작업에서는 ASP.NET MVC 4의 기능을 재정의 하는 새 브라우저 및 jQuery에서 추가 된 뷰 전환기의 샘플 구현을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-444">In this task, you will explore the sample implementation of a view-switcher added by jQuery.Mobile.MVC and the new browser overriding features in ASP.NET MVC 4.</span></span>

1. <span data-ttu-id="b4414-445">Visual Studio로 다시 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-445">Switch back to Visual Studio.</span></span>
2. <span data-ttu-id="b4414-446">**Views\Shared** 폴더 아래에 있는 **\_Layout** 을 열고 뷰-전환기 구성 요소가 부분 뷰로 참조 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-446">Open the **\_Layout.Mobile.cshtml** view located under the **Views\Shared** folder and notice the view-switcher component being referenced as a partial view.</span></span>

    <span data-ttu-id="b4414-447">![뷰 전환기 구성 요소를 사용 하는 모바일 레이아웃](whats-new-in-aspnet-mvc-4/_static/image29.png "뷰 전환기 구성 요소를 사용 하는 모바일 레이아웃")</span><span class="sxs-lookup"><span data-stu-id="b4414-447">![Mobile layout using View-Switcher component](whats-new-in-aspnet-mvc-4/_static/image29.png "Mobile layout using View-Switcher component")</span></span>

    <span data-ttu-id="b4414-448">*뷰 전환기 구성 요소를 사용 하는 모바일 레이아웃*</span><span class="sxs-lookup"><span data-stu-id="b4414-448">*Mobile layout using View-Switcher component*</span></span>
3. <span data-ttu-id="b4414-449">**\_ViewSwitcher. cshtml** 부분 뷰를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-449">Open the **\_ViewSwitcher.cshtml** partial view.</span></span>

    <span data-ttu-id="b4414-450">부분 뷰는 새로운 메서드인 **ViewContext ()** 를 사용 하 여 웹 요청의 원본을 확인 하 고 해당 링크를 표시 하 여 데스크톱 또는 모바일 보기로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-450">The partial view uses the new method **ViewContext.HttpContext.GetOverriddenBrowser()** to determine the origin of the web request and show the corresponding link to switch either to the Desktop or Mobile views.</span></span>

    <span data-ttu-id="b4414-451">**GetOverriddenBrowser** 메서드는 요청에 대해 현재 설정 된 (실제 또는 재정의) 사용자 에이전트에 해당 하는 **HttpBrowserCapabilitiesBase** 인스턴스를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-451">The **GetOverriddenBrowser** method returns an **HttpBrowserCapabilitiesBase** instance that corresponds to the user agent currently set for the request (actual or overridden).</span></span> <span data-ttu-id="b4414-452">이 값을 사용 하 여 **IsMobileDevice**등의 속성을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-452">You can use this value to get properties such as **IsMobileDevice**.</span></span>

    <span data-ttu-id="b4414-453">![ViewSwitcher 부분 뷰](whats-new-in-aspnet-mvc-4/_static/image30.png "ViewSwitcher 부분 뷰")</span><span class="sxs-lookup"><span data-stu-id="b4414-453">![ViewSwitcher partial view](whats-new-in-aspnet-mvc-4/_static/image30.png "ViewSwitcher partial view")</span></span>

    <span data-ttu-id="b4414-454">*ViewSwitcher 부분 뷰*</span><span class="sxs-lookup"><span data-stu-id="b4414-454">*ViewSwitcher partial view*</span></span>
4. <span data-ttu-id="b4414-455">**Controllers** 폴더에 있는 **ViewSwitcherController.cs** 클래스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-455">Open the **ViewSwitcherController.cs** class located in the **Controllers** folder.</span></span> <span data-ttu-id="b4414-456">ViewSwitcher 구성 요소의 링크에 의해 SwitchView 작업이 호출 되는지 확인 하 고 새 HttpContext 메서드를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-456">Check out that SwitchView action is called by the link in the ViewSwitcher component, and notice the new HttpContext methods.</span></span>

    - <span data-ttu-id="b4414-457">**ClearOverriddenBrowser ()** 메서드는 현재 요청에 대해 재정의 된 사용자 에이전트를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-457">The **HttpContext.ClearOverriddenBrowser()** method removes any overridden user agent for the current request.</span></span>
    - <span data-ttu-id="b4414-458">**SetOverriddenBrowser ()** 메서드는 지정 된 사용자 에이전트를 사용 하 여 요청의 실제 사용자 에이전트 값을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-458">The **HttpContext.SetOverriddenBrowser()** method overrides the request's actual user agent value using the specified user agent.</span></span>  
        <span data-ttu-id="b4414-459">![ViewSwitcher 컨트롤러](whats-new-in-aspnet-mvc-4/_static/image31.png "ViewSwitcher 컨트롤러 ")</span><span class="sxs-lookup"><span data-stu-id="b4414-459">![ViewSwitcher Controller](whats-new-in-aspnet-mvc-4/_static/image31.png "ViewSwitcher Controller")</span></span>  
<span data-ttu-id="b4414-460">*ViewSwitcher 컨트롤러*</span><span class="sxs-lookup"><span data-stu-id="b4414-460">*ViewSwitcher Controller*</span></span>

        <span data-ttu-id="b4414-461">브라우저 재정의는 ASP.NET MVC 4의 핵심 기능이 며, jQuery 패키지를 설치 하지 않은 경우에도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-461">Browser Overriding is a core feature of ASP.NET MVC 4, which is also available even if you do not install the jQuery.Mobile.MVC package.</span></span> <span data-ttu-id="b4414-462">그러나이 기능은 뷰, 레이아웃 및 부분 뷰에만 영향을 주며, Browser 개체에 종속 된 기능에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-462">However, this feature affects only view, layout, and partial-view, and it does not affect any of the features that depend on the Request.Browser object.</span></span>

<a id="Task_5_-_Adding_the_View-Switcher_in_the_Desktop_View"></a>
#### <a name="task-5---adding-the-view-switcher-in-the-desktop-view"></a><span data-ttu-id="b4414-463">작업 5-바탕 화면 보기에서 뷰-전환기 추가</span><span class="sxs-lookup"><span data-stu-id="b4414-463">Task 5 - Adding the View-Switcher in the Desktop View</span></span>

<span data-ttu-id="b4414-464">이 작업에서는 뷰 전환기를 포함 하도록 바탕 화면 레이아웃을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-464">In this task, you will update the desktop layout to include the view-switcher.</span></span> <span data-ttu-id="b4414-465">이렇게 하면 모바일 사용자가 바탕 화면 보기를 탐색할 때 모바일 보기로 돌아갈 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-465">This will allow mobile users to go back to the mobile view when browsing the desktop view.</span></span>

1. <span data-ttu-id="b4414-466">**Windows Phone 에뮬레이터**에서 사이트를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-466">Refresh the site in the **Windows Phone Emulator**.</span></span>
2. <span data-ttu-id="b4414-467">갤러리 위쪽에서 **바탕 화면 보기** 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-467">Click on the **Desktop view** link at the top of the gallery.</span></span> <span data-ttu-id="b4414-468">바탕 화면 보기에는 모바일 보기로 돌아갈 수 있는 뷰 전환기가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-468">Notice there is no view-switcher in the desktop view to allow you return to the mobile view.</span></span>
3. <span data-ttu-id="b4414-469">Visual Studio로 돌아가서 **\_Layout. cshtml** 뷰를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-469">Go back to Visual Studio and open the **\_Layout.cshtml** view.</span></span>
4. <span data-ttu-id="b4414-470">로그인 섹션을 찾은 후 호출을 삽입 하 여 **\_logonpartial** 부분 보기 아래에 **\_viewswitcher** 부분 뷰를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-470">Find the login section and insert a call to render the **\_ViewSwitcher** partial view below the **\_LogOnPartial** partial view.</span></span> <span data-ttu-id="b4414-471">그런 다음 **ctrl + S** 를 눌러 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-471">Then, press **CTRL + S** to save the changes.</span></span>

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample14.cshtml)]
5. <span data-ttu-id="b4414-472">**Ctrl + S** 를 눌러 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-472">Press **CTRL + S** to save the changes.</span></span>
6. <span data-ttu-id="b4414-473">Windows Phone 에뮬레이터에서 페이지를 새로 고치고 화면을 두 번 클릭 하 여 확대 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-473">Refresh the page in the Windows Phone Emulator and double-click the screen to zoom in.</span></span> <span data-ttu-id="b4414-474">이제 홈 페이지에 모바일에서 바탕 화면 보기로 전환 하는 **모바일 보기** 링크가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-474">Notice that the home page now shows the **Mobile view** link that switches from mobile to desktop view.</span></span>

    <span data-ttu-id="b4414-475">![데스크톱 보기에서 렌더링 된 뷰 전환기](whats-new-in-aspnet-mvc-4/_static/image32.png "데스크톱 보기에서 렌더링 된 뷰 전환기")</span><span class="sxs-lookup"><span data-stu-id="b4414-475">![View Switcher rendered in desktop view](whats-new-in-aspnet-mvc-4/_static/image32.png "View Switcher rendered in desktop view")</span></span>

    <span data-ttu-id="b4414-476">*데스크톱 보기에서 렌더링 된 뷰 전환기*</span><span class="sxs-lookup"><span data-stu-id="b4414-476">*View Switcher rendered in desktop view*</span></span>
7. <span data-ttu-id="b4414-477">모바일 보기로 다시 전환 하 고 **정보** 페이지 (http://localhost [port]/Home/About)로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-477">Switch to the Mobile view again and browse to **About** page (http://localhost[port]/Home/About).</span></span> <span data-ttu-id="b4414-478">About. Mobile. cshtml 뷰를 만들지 않은 경우에도 모바일 레이아웃을 사용 하 여 About 페이지가 표시 됩니다 (\_Layout. cshtml).</span><span class="sxs-lookup"><span data-stu-id="b4414-478">Notice that, even if you haven't created an About.Mobile.cshtml view, the About page is displayed using the mobile layout (\_Layout.Mobile.cshtml).</span></span>

    <span data-ttu-id="b4414-479">![정보 페이지](whats-new-in-aspnet-mvc-4/_static/image33.png "“关于”页面")</span><span class="sxs-lookup"><span data-stu-id="b4414-479">![About page](whats-new-in-aspnet-mvc-4/_static/image33.png "About page")</span></span>

    <span data-ttu-id="b4414-480">*정보 페이지*</span><span class="sxs-lookup"><span data-stu-id="b4414-480">*About page*</span></span>
8. <span data-ttu-id="b4414-481">마지막으로 데스크톱 웹 브라우저에서 사이트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-481">Finally, open the site in a desktop Web browser.</span></span> <span data-ttu-id="b4414-482">이전 업데이트가 바탕 화면 보기에 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-482">Notice that none of the previous updates has affected the desktop view.</span></span>

    <span data-ttu-id="b4414-483">![사진 갤러리 바탕 화면 보기](whats-new-in-aspnet-mvc-4/_static/image34.png "사진 갤러리 바탕 화면 보기")</span><span class="sxs-lookup"><span data-stu-id="b4414-483">![PhotoGallery desktop view](whats-new-in-aspnet-mvc-4/_static/image34.png "PhotoGallery desktop view")</span></span>

    <span data-ttu-id="b4414-484">*사진 갤러리 바탕 화면 보기*</span><span class="sxs-lookup"><span data-stu-id="b4414-484">*PhotoGallery desktop view*</span></span>

<a id="Task_6_-_Creating_New_Display_Modes"></a>
#### <a name="task-6---creating-new-display-modes"></a><span data-ttu-id="b4414-485">작업 6-새 디스플레이 모드 만들기</span><span class="sxs-lookup"><span data-stu-id="b4414-485">Task 6 - Creating New Display Modes</span></span>

<span data-ttu-id="b4414-486">새 디스플레이 모드 기능을 사용 하면 응용 프로그램에서 요청을 생성 하는 브라우저에 따라 보기를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-486">The new display modes feature lets an application select views depending on the browser that is generating the request.</span></span> <span data-ttu-id="b4414-487">예를 들어 데스크톱 브라우저에서 홈 페이지를 요청 하는 경우 응용 프로그램은 **Views\Home\Index.cshtml** 템플릿을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-487">For example, if a desktop browser requests the Home page, the application will return the **Views\Home\Index.cshtml** template.</span></span> <span data-ttu-id="b4414-488">그런 다음 모바일 브라우저에서 홈 페이지를 요청 하면 응용 프로그램은 **Views\Home\Index.mobile.cshtml** 템플릿을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-488">Then, if a mobile browser requests the Home page, the application will return the **Views\Home\Index.mobile.cshtml** template.</span></span>

<span data-ttu-id="b4414-489">이 작업에서는 iPhone 장치에 대 한 사용자 지정 레이아웃을 만들고 iPhone 장치에서 요청을 시뮬레이션 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-489">In this task, you will create a customized layout for iPhone devices, and you will have to simulate requests from iPhone devices.</span></span> <span data-ttu-id="b4414-490">이렇게 하려면 iPhone 에뮬레이터/시뮬레이터 (예: [전기 모바일 시뮬레이터](http://www.electricplum.com/)) 또는 사용자 에이전트를 수정 하는 추가 기능을 사용 하는 브라우저를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-490">To do this, you can use either an iPhone emulator/simulator (like [Electric Mobile Simulator](http://www.electricplum.com/)) or a browser with add-ons that modify the user agent.</span></span> <span data-ttu-id="b4414-491">Safari 브라우저에서 iPhone을 에뮬레이트하는 사용자 에이전트 문자열을 설정 하는 방법에 대 한 지침은 Alison의 블로그에서 [safari를 사용](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) 하는 방법에 대 한 자세한 내용을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b4414-491">For instructions on how to set the user agent string in an Safari browser to emulate an iPhone, see [How to let Safari pretend it's IE](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) in David Alison's blog.</span></span>

<span data-ttu-id="b4414-492">**이 태스크는 선택 사항이 며 랩에서 실행 하지 않고 계속 진행할 수 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="b4414-492">**Notice that this task is optional and you can continue throughout the lab without executing it.**</span></span>

1. <span data-ttu-id="b4414-493">Visual Studio에서 **SHIFT** + **f5** 키를 눌러 응용 프로그램 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-493">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
2. <span data-ttu-id="b4414-494">**Global.asax.cs** 를 열고 다음 using 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-494">Open **Global.asax.cs** and add the following using statement.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample15.cs)]
3. <span data-ttu-id="b4414-495">응용 프로그램\_Start 메서드에 다음 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-495">Add the following highlighted code into the Application\_Start method.</span></span>

    <span data-ttu-id="b4414-496">(코드 조각- *ASP.NET MVC 4 Lab-Ex03-IPhone DisplayMode*)</span><span class="sxs-lookup"><span data-stu-id="b4414-496">(Code Snippet - *ASP.NET MVC 4 Lab - Ex03 - iPhone DisplayMode*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample16.cs)]

<span data-ttu-id="b4414-497">들어오는 각 요청에 대해 일치 하는 정적 **Displaymodeprovider. Instance.** mode 정적 목록 내에 **&quot;iPhone&quot;라는 새 DefaultDisplayMode** 를 등록 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-497">You have registered a new **DefaultDisplayMode named &quot;iPhone&quot;**, within the static **DisplayModeProvider.Instance.Modes** static list, that will be matched against each incoming request.</span></span> <span data-ttu-id="b4414-498">들어오는 요청에 &quot;iPhone&quot;문자열이 포함 된 경우 ASP.NET MVC는 이름에 &quot;iPhone&quot; 접미사가 포함 된 뷰를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-498">If the incoming request contains the string &quot;iPhone&quot;, ASP.NET MVC will find the views whose name contain the &quot;iPhone&quot; suffix.</span></span> <span data-ttu-id="b4414-499">0 매개 변수는 특정가 새 모드 인지 여부를 나타냅니다. 예를 들어이 보기는 모바일 장치의 요청과 일치 하는 일반 &quot;모바일&quot; 규칙 보다 더 구체적입니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-499">The 0 parameter indicates how specific is the new mode; for instance, this view is more specific than the general &quot;.mobile&quot; rule that matches requests from mobile devices.</span></span>

<span data-ttu-id="b4414-500">이 코드를 실행 한 후 iPhone 브라우저가 요청을 생성할 때 응용 프로그램은 다음 단계에서 만들 **Views\Shared\\_Layout** 를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-500">After this code runs, when an iPhone browser generates a request, your application will use the **Views\Shared\\_Layout.iPhone.cshtml** layout you will create in the next steps.</span></span>

> [!NOTE]
> <span data-ttu-id="b4414-501">IPhone에 대 한 요청을 테스트 하는이 방법은 데모용으로 간소화 되었으며 모든 iPhone 사용자 에이전트 문자열에 대해 예상 대로 작동 하지 않을 수 있습니다 (예: 테스트는 대/소문자를 구분 함).</span><span class="sxs-lookup"><span data-stu-id="b4414-501">This way of testing the request for iPhone has been simplified for demo purposes and might not work as expected for every iPhone user agent string (for example test is case sensitive).</span></span>

4. <span data-ttu-id="b4414-502">**Views\Shared** 폴더에 **\_layout** 파일의 복사본을 만들고 복사본의 이름을 &quot; **\_layout. cshtml**&quot;로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-502">Create a copy of the **\_Layout.Mobile.cshtml** file in the **Views\Shared** folder and rename the copy to &quot;**\_Layout.iPhone.cshtml**&quot;.</span></span>
5. <span data-ttu-id="b4414-503">이전 단계에서 만든 **\_Layout. cshtml** 를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-503">Open **\_Layout.iPhone.cshtml** you created in the previous step.</span></span>
6. <span data-ttu-id="b4414-504">데이터 역할 특성이 **페이지** 로 설정 된 div 요소를 **찾고&quot;&quot;** **데이터 테마** 특성을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-504">Find the div element with the data-role attribute set to **page** and change the **data-theme** attribute to &quot;**a**&quot;.</span></span>

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample17.cshtml)]

<span data-ttu-id="b4414-505">이제 ASP.NET MVC 4 응용 프로그램에는 세 가지 레이아웃이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-505">Now you have 3 layouts in your ASP.NET MVC 4 application:</span></span>

1. <span data-ttu-id="b4414-506">**\_레이아웃. cshtml**: 데스크톱 브라우저에 사용 되는 기본 레이아웃입니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-506">**\_Layout.cshtml**: default layout used for desktop browsers.</span></span>
2. <span data-ttu-id="b4414-507">**\_레이아웃. mobile. cshtml**: 모바일 장치에 사용 되는 기본 레이아웃입니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-507">**\_Layout.mobile.cshtml**: default layout used for mobile devices.</span></span>
3. <span data-ttu-id="b4414-508">**\_레이아웃. iphone. cshtml**: 다른 색 구성표를 사용 하 여 \_레이아웃과 구별 하는 iphone 장치에 대 한 특정 레이아웃.</span><span class="sxs-lookup"><span data-stu-id="b4414-508">**\_Layout.iPhone.cshtml**: specific layout for iPhone devices, using a different color scheme to differentiate from \_Layout.mobile.cshtml.</span></span>
7. <span data-ttu-id="b4414-509">**F5** 키를 눌러 응용 프로그램을 실행 하 고 **Windows Phone 에뮬레이터**에서 사이트를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-509">Press **F5** to run the application and browse the site in the **Windows Phone Emulator**.</span></span>
8. <span data-ttu-id="b4414-510">**Iphone 시뮬레이터** 를 열고 (iphone 시뮬레이터를 설치 및 구성 하는 방법에 대 한 지침은 [부록 C](#AppendixC) 참조) 사이트를 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-510">Open an **iPhone simulator** (see [Appendix C](#AppendixC) for instructions on how to install and configure an iPhone simulator), and browse to the site too.</span></span> <span data-ttu-id="b4414-511">각 휴대폰은 특정 템플릿을 사용 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-511">Notice that each phone is using the specific template.</span></span>

    ![-For each-장치 2에 대 한 보기 사용](whats-new-in-aspnet-mvc-4/_static/image35.png)

    <span data-ttu-id="b4414-513">*각 모바일 장치에 대해 서로 다른 보기 사용*</span><span class="sxs-lookup"><span data-stu-id="b4414-513">*Using different views for each mobile device*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Using_Asynchronous_Controllers"></a>
### <a name="exercise-4-using-asynchronous-controllers"></a><span data-ttu-id="b4414-514">연습 4: 비동기 컨트롤러 사용</span><span class="sxs-lookup"><span data-stu-id="b4414-514">Exercise 4: Using Asynchronous Controllers</span></span>

<span data-ttu-id="b4414-515">Microsoft .NET Framework 4.5에서는 및의 C# 새로운 언어 기능을 도입 하 여 .net 프로그래밍에 비동기에 대 한 새로운 토대를 제공 Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="b4414-515">Microsoft .NET Framework 4.5 introduces new language features in C# and Visual Basic to provide a new foundation for asynchrony in .NET programming.</span></span> <span data-ttu-id="b4414-516">이 새로운 토대를 통해 비동기 프로그래밍은 및와 유사 하 게 동기 프로그래밍으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-516">This new foundation makes asynchronous programming similar to - and about as straightforward as - synchronous programming.</span></span> <span data-ttu-id="b4414-517">이제 **Asynccontroller** 클래스를 사용 하 여 ASP.NET MVC 4에서 비동기 작업 메서드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-517">You are now able to write asynchronous action methods in ASP.NET MVC 4 by using the **AsyncController** class.</span></span> <span data-ttu-id="b4414-518">장기 실행 CPU 바운드 요청에 비동기 작업 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-518">You can use asynchronous action methods for long-running, non-CPU bound requests.</span></span> <span data-ttu-id="b4414-519">이렇게 하면 요청이 처리 되는 동안 웹 서버에서 작업을 수행 하지 못하도록 차단 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-519">This avoids blocking the Web server from performing work while the request is being processed.</span></span> <span data-ttu-id="b4414-520">AsyncController 클래스는 일반적으로 장기 실행 웹 서비스 호출에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-520">The AsyncController class is typically used for long-running Web service calls.</span></span>

<span data-ttu-id="b4414-521">이 연습에서는 ASP.NET MVC 4의 비동기 작업에 대 한 기본 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-521">This exercise explains the basics of asynchronous operation in ASP.NET MVC 4.</span></span> <span data-ttu-id="b4414-522">자세히 알아보려면 다음 문서를 참조 하세요. [ [https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="b4414-522">If you want a deeper dive, you can check out the following article: [[https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)</span></span>

<a id="Task_1_-_Implementing_an_Asynchronous_Controller"></a>
#### <a name="task-1---implementing-an-asynchronous-controller"></a><span data-ttu-id="b4414-523">작업 1-비동기 컨트롤러 구현</span><span class="sxs-lookup"><span data-stu-id="b4414-523">Task 1 - Implementing an Asynchronous Controller</span></span>

1. <span data-ttu-id="b4414-524">**원본/Ex4-Async/begin/** 폴더에 있는 **시작** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-524">Open the **Begin** solution located at **Source/Ex4-Async/Begin/** folder.</span></span> <span data-ttu-id="b4414-525">그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-525">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="b4414-526">제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-526">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="b4414-527">이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-527">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="b4414-528">**NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-528">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="b4414-529">마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-529">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="b4414-530">NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-530">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="b4414-531">NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-531">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="b4414-532">이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-532">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="b4414-533">**Controllers** 폴더에서 **HomeController.cs** 클래스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-533">Open the **HomeController.cs** class from the **Controllers** folder.</span></span>
3. <span data-ttu-id="b4414-534">다음 using 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-534">Add the following using statement.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample18.cs)]
4. <span data-ttu-id="b4414-535">**Asynccontroller**에서 상속 하도록 **HomeController** 클래스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-535">Update the **HomeController** class to inherit from **AsyncController**.</span></span> <span data-ttu-id="b4414-536">AsyncController에서 파생 되는 컨트롤러는 ASP.NET을 사용 하 여 비동기 요청을 처리 하 고 동기 작업 메서드를 여전히 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-536">Controllers that derive from AsyncController enable ASP.NET to process asynchronous requests, and they can still service synchronous action methods.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample19.cs)]
5. <span data-ttu-id="b4414-537">**Index** 메서드에 **async** 키워드를 추가 하 고 **작업 형식&lt;actionresult&gt;** 반환 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-537">Add the **async** keyword to the **Index** method and make it return the type **Task&lt;ActionResult&gt;**.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample20.cs)]

    > [!NOTE]
    > <span data-ttu-id="b4414-538">**Async** 키워드는 .NET Framework 4.5에서 제공 하는 새 키워드 중 하나입니다. 이 메서드에는 비동기 코드가 포함 되어 있음을 컴파일러에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-538">The **async** keyword is one of the new keywords the .NET Framework 4.5 provides; it tells the compiler that this method contains asynchronous code.</span></span> <span data-ttu-id="b4414-539">**작업** 개체는 나중에 완료 될 수 있는 비동기 작업을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-539">A **Task** object represents an asynchronous operation that may complete at some point in the future.</span></span>
6. <span data-ttu-id="b4414-540">클라이언트를 바꿉니다 **.** 아래 표시 된 것 처럼 wait 키워드를 사용 하는 전체 비동기 버전의 getasync () 호출입니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-540">Replace the **client.GetAsync()** call with the full async version using await keyword as shown below.</span></span>

    <span data-ttu-id="b4414-541">(코드 조각- *ASP.NET MVC 4 Lab-Ex04-GetAsync*)</span><span class="sxs-lookup"><span data-stu-id="b4414-541">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - GetAsync*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample21.cs)]

    > [!NOTE]
    > <span data-ttu-id="b4414-542">이전 버전에서는 결과가 반환 될 때까지 (동기화 버전) **작업** 개체의 **result** 속성을 사용 하 여 스레드를 차단 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-542">In the previous version, you were using the **Result** property from the **Task** object to block the thread until the result is returned (sync version).</span></span>
    > 
    > <span data-ttu-id="b4414-543">**Wait** 키워드를 추가 하면 컴파일러는 메서드 호출에서 반환 된 작업을 비동기적으로 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-543">Adding the **await** keyword tells the compiler to asynchronously wait for the task returned from the method call.</span></span> <span data-ttu-id="b4414-544">즉, 코드의 나머지 부분은 대기 메서드가 완료 된 후에만 콜백으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-544">This means that the rest of the code will be executed as a callback only after the awaited method completes.</span></span> <span data-ttu-id="b4414-545">이 작업을 수행 하기 위해 try-catch 블록을 변경할 필요는 없습니다. 즉, 백그라운드에서 발생 하는 예외 나 전경에서 발생 하는 예외는 프레임 워크에서 제공 하는 처리기를 사용 하 여 추가 작업 없이 계속 catch 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-545">Another thing to notice is that you do not need to change your try-catch block in order to make this work: the exceptions that happen in background or in foreground will still be caught without any extra work using a handler provided by the framework.</span></span>
7. <span data-ttu-id="b4414-546">아래와 같이 줄을 새 코드로 바꿔서 비동기 구현을 계속 하려면 코드를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-546">Change the code to continue with the asynchronous implementation by replacing the lines with the new code as shown below</span></span>

    <span data-ttu-id="b4414-547">(코드 조각- *ASP.NET MVC 4 Lab-Ex04-ReadAsStringAsync*)</span><span class="sxs-lookup"><span data-stu-id="b4414-547">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - ReadAsStringAsync*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample22.cs)]
8. <span data-ttu-id="b4414-548">运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="b4414-548">Run the application.</span></span> <span data-ttu-id="b4414-549">중요 한 변경 사항은 없지만 코드는 스레드 풀의 스레드를 차단 하 여 서버 리소스를 더 효율적으로 사용 하 고 성능을 개선 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-549">You will notice no major changes, but your code will not block a thread from the thread pool making a better usage of the server resources and improving performance.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b4414-550">Lab &quot;의 새로운 비동기 프로그래밍 기능에 대 한 자세한 내용은 Visual Studio 학습 키트에 포함 된 **.net C# 4.5의 .net 및 Visual Basic의 비동기 프로그래밍** 을&quot;.</span><span class="sxs-lookup"><span data-stu-id="b4414-550">You can learn more about the new asynchronous programming features in the lab &quot;**Asynchronous Programming in .NET 4.5 with C# and Visual Basic**&quot; included in the Visual Studio Training Kit.</span></span>

<a id="Task_2_-_Handling_Time-Outs_with_Cancellation_Tokens"></a>
#### <a name="task-2---handling-time-outs-with-cancellation-tokens"></a><span data-ttu-id="b4414-551">작업 2-취소 토큰으로 시간 제한 처리</span><span class="sxs-lookup"><span data-stu-id="b4414-551">Task 2 - Handling Time-Outs with Cancellation Tokens</span></span>

<span data-ttu-id="b4414-552">작업 인스턴스를 반환 하는 비동기 작업 메서드는 제한 시간을 지원할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-552">Asynchronous action methods that return Task instances can also support time-outs.</span></span> <span data-ttu-id="b4414-553">이 작업에서는 취소 토큰을 사용 하 여 시간 제한 시나리오를 처리 하도록 인덱스 메서드 코드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-553">In this task, you will update the Index method code to handle a time-out scenario using a cancellation token.</span></span>

1. <span data-ttu-id="b4414-554">Visual Studio로 돌아가서 **SHIFT + f5** 키를 눌러 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-554">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>
2. <span data-ttu-id="b4414-555">**HomeController.cs** 파일에 다음 using 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-555">Add the following using statement to the **HomeController.cs** file.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample23.cs)]
3. <span data-ttu-id="b4414-556">**CancellationToken** 인수를 수신 하도록 인덱스 작업을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-556">Update the Index action to receive a **CancellationToken** argument.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample24.cs)]
4. <span data-ttu-id="b4414-557">**Getasync** 호출을 업데이트 하 여 취소 토큰을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-557">Update the **GetAsync** call to pass the cancellation token.</span></span>

    <span data-ttu-id="b4414-558">(코드 조각- *ASP.NET MVC 4 Lab-Ex04-SendAsync With CancellationToken*)</span><span class="sxs-lookup"><span data-stu-id="b4414-558">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - SendAsync with CancellationToken*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample25.cs)]
5. <span data-ttu-id="b4414-559">**Asynctimeout** 특성을 500 밀리초로 설정 하 고 **TaskCanceledException** 를 처리 하도록 구성 된 **handleerror** 특성을 **TimedOut** 뷰로 리디렉션하여 *인덱스* 메서드를 장식 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-559">Decorate the *Index* method with an **AsyncTimeout** attribute set to 500 milliseconds and a **HandleError** attribute configured to handle **TaskCanceledException** by redirecting to a **TimedOut** view.</span></span>

    <span data-ttu-id="b4414-560">(코드 조각- *ASP.NET MVC 4 Lab-Ex04*)</span><span class="sxs-lookup"><span data-stu-id="b4414-560">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - Attributes*)</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample26.cs)]
6. <span data-ttu-id="b4414-561">**사진 컨트롤러** 클래스를 열고 **갤러리** 메서드를 업데이트 하 여 장기 실행 작업을 시뮬레이션 하기 위해 1000 밀리초 (1 초)의 실행을 지연 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-561">Open the **PhotoController** class and update the **Gallery** method to delay the execution 1000 milliseconds (1 second) to simulate a long running task.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample27.cs)]
7. <span data-ttu-id="b4414-562">**Web.config** 파일을 열고 다음 요소를 추가 하 여 사용자 지정 오류를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-562">Open the **Web.config** file and enable custom errors by adding the following element.</span></span>

    [!code-xml[Main](whats-new-in-aspnet-mvc-4/samples/sample28.xml)]
8. <span data-ttu-id="b4414-563">**Views\Shared** 에 **TimedOut** 라는 새 뷰를 만들고 기본 레이아웃을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-563">Create a new view in **Views\Shared** named **TimedOut** and use the default layout.</span></span> <span data-ttu-id="b4414-564">솔루션 탐색기에서 **Views\Shared** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 보기**.</span><span class="sxs-lookup"><span data-stu-id="b4414-564">In the Solution Explorer, right-click the **Views\Shared** folder and select **Add | View**.</span></span>

    <span data-ttu-id="b4414-565">![각 모바일 장치에 대해 서로 다른 보기 사용](whats-new-in-aspnet-mvc-4/_static/image36.png "각 모바일 장치에 대해 서로 다른 보기 사용")</span><span class="sxs-lookup"><span data-stu-id="b4414-565">![Using different views for each mobile device](whats-new-in-aspnet-mvc-4/_static/image36.png "Using different views for each mobile device")</span></span>

    <span data-ttu-id="b4414-566">*각 모바일 장치에 대해 서로 다른 보기 사용*</span><span class="sxs-lookup"><span data-stu-id="b4414-566">*Using different views for each mobile device*</span></span>
9. <span data-ttu-id="b4414-567">아래와 같이 **TimedOut** view 콘텐츠를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-567">Update the **TimedOut** view content as shown below.</span></span>

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample29.cshtml)]
10. <span data-ttu-id="b4414-568">응용 프로그램을 실행 하 고 루트 URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-568">Run the application and navigate to the root URL.</span></span> <span data-ttu-id="b4414-569">스레드를 추가 했으므로 1000 밀리초의 절전 모드를 사용할 경우 **Asynctimeout** 특성에 의해 생성 되 고 **handleerror** 특성에 의해 catch 되는 시간 제한 오류가 발생 **합니다.**</span><span class="sxs-lookup"><span data-stu-id="b4414-569">As you have added a **Thread.Sleep** of 1000 milliseconds, you will get a time-out error, generated by the **AsyncTimeout** attribute and catch by the **HandleError** attribute.</span></span>

    <span data-ttu-id="b4414-570">![처리 시간 제한 예외](whats-new-in-aspnet-mvc-4/_static/image37.png "처리 시간 제한 예외")</span><span class="sxs-lookup"><span data-stu-id="b4414-570">![Time-out exception handled](whats-new-in-aspnet-mvc-4/_static/image37.png "Time-out exception handled")</span></span>

    <span data-ttu-id="b4414-571">*처리 시간 제한 예외*</span><span class="sxs-lookup"><span data-stu-id="b4414-571">*Time-out exception handled*</span></span>

> [!NOTE]
> <span data-ttu-id="b4414-572">또한 [부록 D: 웹 배포을 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시](#AppendixD)를 따라 Microsoft Azure 웹 사이트에이 응용 프로그램을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-572">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix D: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixD).</span></span>

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="b4414-573">总结</span><span class="sxs-lookup"><span data-stu-id="b4414-573">Summary</span></span>

<span data-ttu-id="b4414-574">이 실습 실습에서는 ASP.NET MVC 4의 새로운 기능 중 일부를 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-574">In this hands-on-lab, you've observed some of the new features resident in ASP.NET MVC 4.</span></span> <span data-ttu-id="b4414-575">다음 개념에 대해 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-575">The following concepts have been discussed:</span></span>

- <span data-ttu-id="b4414-576">새 모바일 응용 프로그램 프로젝트 템플릿을 포함 하 여 ASP.NET MVC 프로젝트 템플릿에 대 한 향상 된 기능 활용</span><span class="sxs-lookup"><span data-stu-id="b4414-576">Take advantage of the enhancements to the ASP.NET MVC project templates-including the new mobile application project template</span></span>
- <span data-ttu-id="b4414-577">HTML5 뷰포트 특성 및 CSS 미디어 쿼리를 사용 하 여 모바일 장치에 대 한 디스플레이 개선</span><span class="sxs-lookup"><span data-stu-id="b4414-577">Use the HTML5 viewport attribute and CSS media queries to improve the display on mobile devices</span></span>
- <span data-ttu-id="b4414-578">프로그레시브 기능 향상을 위해 jQuery Mobile 사용 및 터치 최적화 웹 UI 빌드</span><span class="sxs-lookup"><span data-stu-id="b4414-578">Use jQuery Mobile for progressive enhancements and for building touch-optimized web UI</span></span>
- <span data-ttu-id="b4414-579">모바일 관련 보기 만들기</span><span class="sxs-lookup"><span data-stu-id="b4414-579">Create mobile-specific views</span></span>
- <span data-ttu-id="b4414-580">뷰-전환기 구성 요소를 사용 하 여 응용 프로그램에서 모바일 및 데스크톱 보기 사이를 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-580">Use the view-switcher component to toggle between mobile and desktop views in the application</span></span>
- <span data-ttu-id="b4414-581">작업 지원을 사용 하 여 비동기 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="b4414-581">Create asynchronous controllers using task support</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a><span data-ttu-id="b4414-582">부록 A: 코드 조각 사용</span><span class="sxs-lookup"><span data-stu-id="b4414-582">Appendix A: Using Code Snippets</span></span>

<span data-ttu-id="b4414-583">코드 조각을 사용 하면 필요한 모든 코드를 편리 하 게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-583">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="b4414-584">랩 문서는 다음 그림에 표시 된 것 처럼 사용자가 사용할 수 있는 경우를 정확 하 게 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-584">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="b4414-585">![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입](whats-new-in-aspnet-mvc-4/_static/image38.png "Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입")</span><span class="sxs-lookup"><span data-stu-id="b4414-585">![Using Visual Studio code snippets to insert code into your project](whats-new-in-aspnet-mvc-4/_static/image38.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="b4414-586">*Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입*</span><span class="sxs-lookup"><span data-stu-id="b4414-586">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="b4414-587">***키보드를 사용 하 여 코드 조각을 추가 하려면C# (만 해당)***</span><span class="sxs-lookup"><span data-stu-id="b4414-587">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="b4414-588">코드를 삽입할 위치에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-588">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="b4414-589">조각 이름 (공백 또는 하이픈 제외)을 입력 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-589">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="b4414-590">IntelliSense는 일치 하는 코드 조각의 이름을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-590">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="b4414-591">올바른 코드 조각을 선택 하거나 전체 코드 조각 이름이 선택 될 때까지 계속 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-591">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="b4414-592">Tab 키를 두 번 눌러 커서 위치에 코드 조각을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-592">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="b4414-593">![코드 조각 이름 입력 시작](whats-new-in-aspnet-mvc-4/_static/image39.png "코드 조각 이름 입력 시작")</span><span class="sxs-lookup"><span data-stu-id="b4414-593">![Start typing the snippet name](whats-new-in-aspnet-mvc-4/_static/image39.png "Start typing the snippet name")</span></span>

<span data-ttu-id="b4414-594">*코드 조각 이름 입력 시작*</span><span class="sxs-lookup"><span data-stu-id="b4414-594">*Start typing the snippet name*</span></span>

<span data-ttu-id="b4414-595">![Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.](whats-new-in-aspnet-mvc-4/_static/image40.png "Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="b4414-595">![Press Tab to select the highlighted snippet](whats-new-in-aspnet-mvc-4/_static/image40.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="b4414-596">*Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="b4414-596">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="b4414-597">![Tab 키를 다시 누르면 코드 조각이 확장 됩니다.](whats-new-in-aspnet-mvc-4/_static/image41.png "Tab 키를 다시 누르면 코드 조각이 확장 됩니다.")</span><span class="sxs-lookup"><span data-stu-id="b4414-597">![Press Tab again and the snippet will expand](whats-new-in-aspnet-mvc-4/_static/image41.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="b4414-598">*Tab 키를 다시 누르면 코드 조각이 확장 됩니다.*</span><span class="sxs-lookup"><span data-stu-id="b4414-598">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="b4414-599">***마우스 (C#, VISUAL BASIC 및 XML)를 사용 하 여 코드 조각을 추가 하려면***</span><span class="sxs-lookup"><span data-stu-id="b4414-599">***To add a code snippet using the mouse (C#, Visual Basic and XML)***</span></span>

1. <span data-ttu-id="b4414-600">코드 조각을 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-600">Right-click where you want to insert the code snippet.</span></span>
2. <span data-ttu-id="b4414-601">코드 **조각 삽입** 을 선택한 다음 **내 코드 조각을**선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-601">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
3. <span data-ttu-id="b4414-602">목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-602">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="b4414-603">![코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.](whats-new-in-aspnet-mvc-4/_static/image42.png "코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="b4414-603">![Right-click where you want to insert the code snippet and select Insert Snippet](whats-new-in-aspnet-mvc-4/_static/image42.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="b4414-604">*코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="b4414-604">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="b4414-605">![목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.](whats-new-in-aspnet-mvc-4/_static/image43.png "목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="b4414-605">![Pick the relevant snippet from the list, by clicking on it](whats-new-in-aspnet-mvc-4/_static/image43.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="b4414-606">*목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="b4414-606">*Pick the relevant snippet from the list, by clicking on it*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="b4414-607">부록 B: 웹에 대 한 Visual Studio Express 2012 설치</span><span class="sxs-lookup"><span data-stu-id="b4414-607">Appendix B: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="b4414-608">**[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)** 를 사용 하 여 웹 또는 다른 &quot;Express&quot; 버전 **에 대해 Microsoft Visual Studio Express 2012** 를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-608">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="b4414-609">다음 지침에서는 *Microsoft 웹 플랫폼 설치 관리자*를 사용 하 여 *Visual studio Express 2012 for Web* 을 설치 하는 데 필요한 단계를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-609">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="b4414-610">[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-610">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="b4414-611">또는 웹 플랫폼 설치 관리자를 이미 설치한 경우에는 웹 플랫폼 설치 관리자를 열고 *Microsoft AZURE SDK&quot;를 사용 하 여 웹 용 2012 Visual Studio Express* &quot;제품을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-611">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;*Visual Studio Express 2012 for Web with Windows Azure SDK*&quot;.</span></span>
2. <span data-ttu-id="b4414-612">**지금 설치**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-612">Click on **Install Now**.</span></span> <span data-ttu-id="b4414-613">**웹 플랫폼 설치 관리자** 가 없으면 먼저이를 다운로드 하 여 설치 하도록 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-613">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="b4414-614">**웹 플랫폼 설치 관리자** 가 열리면 **설치** 를 클릭 하 여 설치를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-614">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="b4414-615">![Visual Studio Express 설치](whats-new-in-aspnet-mvc-4/_static/image44.png "Visual Studio Express 설치")</span><span class="sxs-lookup"><span data-stu-id="b4414-615">![Install Visual Studio Express](whats-new-in-aspnet-mvc-4/_static/image44.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="b4414-616">*Visual Studio Express 설치*</span><span class="sxs-lookup"><span data-stu-id="b4414-616">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="b4414-617">모든 제품의 라이선스 및 사용 조건을 읽고 **동의** 함을 클릭 하 여 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-617">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![사용 조건 동의](whats-new-in-aspnet-mvc-4/_static/image45.png)

    <span data-ttu-id="b4414-619">*사용 조건 동의*</span><span class="sxs-lookup"><span data-stu-id="b4414-619">*Accepting the license terms*</span></span>
5. <span data-ttu-id="b4414-620">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-620">Wait until the downloading and installation process completes.</span></span>

    ![安装进度](whats-new-in-aspnet-mvc-4/_static/image46.png)

    <span data-ttu-id="b4414-622">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="b4414-622">*Installation progress*</span></span>
6. <span data-ttu-id="b4414-623">설치가 완료 되 면 **마침**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-623">When the installation completes, click **Finish**.</span></span>

    ![설치 완료](whats-new-in-aspnet-mvc-4/_static/image47.png)

    <span data-ttu-id="b4414-625">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="b4414-625">*Installation completed*</span></span>
7. <span data-ttu-id="b4414-626">**끝내기** 를 클릭 하 여 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-626">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="b4414-627">웹에 대 한 Visual Studio Express를 열려면 **시작** 화면으로 이동 하 &quot;**VS Express**&quot;작성을 시작한 후 **VS Express for Web** 타일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-627">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 타일](whats-new-in-aspnet-mvc-4/_static/image48.png)

    <span data-ttu-id="b4414-629">*VS Express for Web 타일*</span><span class="sxs-lookup"><span data-stu-id="b4414-629">*VS Express for Web tile*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Installing_WebMatrix_2_and_iPhone_Simulator"></a>
## <a name="appendix-c-installing-webmatrix-2-and-iphone-simulator"></a><span data-ttu-id="b4414-630">부록 C: WebMatrix 2 및 iPhone 시뮬레이터 설치</span><span class="sxs-lookup"><span data-stu-id="b4414-630">Appendix C: Installing WebMatrix 2 and iPhone Simulator</span></span>

<span data-ttu-id="b4414-631">시뮬레이션 된 iPhone 장치에서 사이트를 실행 하려면 iPhone&quot;에 대해 &quot;전자 Mobile 시뮬레이터를 사용 하 여 WebMatrix 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-631">To run your site in a simulated iPhone device you can use the WebMatrix extension &quot;Electric Mobile Simulator for the iPhone&quot;.</span></span> <span data-ttu-id="b4414-632">또한 Visual Studio 2012에서 시뮬레이터를 실행 하도록 동일한 확장을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-632">Also, you can configure the same extension to run the simulator from Visual Studio 2012.</span></span>

<a id="ApxCTask1"></a>

<a id="Task_1_-_Installing_WebMatrix_2"></a>
#### <a name="task-1---installing-webmatrix-2"></a><span data-ttu-id="b4414-633">작업 1-WebMatrix 2 설치</span><span class="sxs-lookup"><span data-stu-id="b4414-633">Task 1 - Installing WebMatrix 2</span></span>

1. <span data-ttu-id="b4414-634">[[https://go.microsoft.com/?linkid=9809776](https://go.microsoft.com/?linkid=9809776)](https://go.microsoft.com/?linkid=9810169)로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-634">Go to [[https://go.microsoft.com/?linkid=9809776](https://go.microsoft.com/?linkid=9809776)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="b4414-635">또는 웹 플랫폼 설치 관리자를 이미 설치한 경우이를 열고 &quot;*WebMatrix 2*&quot;제품을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-635">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;*WebMatrix 2*&quot;.</span></span>
2. <span data-ttu-id="b4414-636">**지금 설치**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-636">Click on **Install Now**.</span></span> <span data-ttu-id="b4414-637">**웹 플랫폼 설치 관리자** 가 없으면 먼저이를 다운로드 하 여 설치 하도록 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-637">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="b4414-638">**웹 플랫폼 설치 관리자** 가 열리면 **설치** 를 클릭 하 여 설치를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-638">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="b4414-639">![WebMatrix 설치 2](whats-new-in-aspnet-mvc-4/_static/image49.png "WebMatrix 설치 2")</span><span class="sxs-lookup"><span data-stu-id="b4414-639">![Install WebMatrix 2](whats-new-in-aspnet-mvc-4/_static/image49.png "Install WebMatrix 2")</span></span>

    <span data-ttu-id="b4414-640">*WebMatrix 설치 2*</span><span class="sxs-lookup"><span data-stu-id="b4414-640">*Install WebMatrix 2*</span></span>
4. <span data-ttu-id="b4414-641">모든 제품의 라이선스 및 사용 조건을 읽고 **동의** 함을 클릭 하 여 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-641">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    <span data-ttu-id="b4414-642">![사용 조건 동의](whats-new-in-aspnet-mvc-4/_static/image50.png "사용 조건 동의")</span><span class="sxs-lookup"><span data-stu-id="b4414-642">![Accepting the license terms](whats-new-in-aspnet-mvc-4/_static/image50.png "Accepting the license terms")</span></span>

    <span data-ttu-id="b4414-643">*사용 조건 동의*</span><span class="sxs-lookup"><span data-stu-id="b4414-643">*Accepting the license terms*</span></span>
5. <span data-ttu-id="b4414-644">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-644">Wait until the downloading and installation process completes.</span></span>

    <span data-ttu-id="b4414-645">![설치 진행률](whats-new-in-aspnet-mvc-4/_static/image51.png "安装进度")</span><span class="sxs-lookup"><span data-stu-id="b4414-645">![Installation progress](whats-new-in-aspnet-mvc-4/_static/image51.png "Installation progress")</span></span>

    <span data-ttu-id="b4414-646">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="b4414-646">*Installation progress*</span></span>
6. <span data-ttu-id="b4414-647">설치가 완료 되 면 **마침**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-647">When the installation completes, click **Finish**.</span></span>

    <span data-ttu-id="b4414-648">![설치 완료](whats-new-in-aspnet-mvc-4/_static/image52.png "설치 완료")</span><span class="sxs-lookup"><span data-stu-id="b4414-648">![Installation completed](whats-new-in-aspnet-mvc-4/_static/image52.png "Installation completed")</span></span>

    <span data-ttu-id="b4414-649">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="b4414-649">*Installation completed*</span></span>
7. <span data-ttu-id="b4414-650">**끝내기** 를 클릭 하 여 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-650">Click **Exit** to close Web Platform Installer.</span></span>

<a id="ApxCTask2"></a>

<a id="Task_2_-_Installing_the_iPhone_Simulator_Extension"></a>
#### <a name="task-2---installing-the-iphone-simulator-extension"></a><span data-ttu-id="b4414-651">작업 2-iPhone 시뮬레이터 확장 설치</span><span class="sxs-lookup"><span data-stu-id="b4414-651">Task 2 - Installing the iPhone Simulator Extension</span></span>

1. <span data-ttu-id="b4414-652">**WebMatrix** 를 실행 하 여 기존 웹 사이트를 열거나 새 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-652">Run **WebMatrix** and open any existing Web site or create a new one.</span></span>
2. <span data-ttu-id="b4414-653">**홈** 리본 메뉴에서 **실행** 단추를 클릭 하 고 **새로 추가**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-653">Click the **Run** button from the **Home** ribbon and select **Add new**.</span></span>

    <span data-ttu-id="b4414-654">![새 WebMatrix 확장 추가](whats-new-in-aspnet-mvc-4/_static/image53.png "새 WebMatrix 확장 추가")</span><span class="sxs-lookup"><span data-stu-id="b4414-654">![Adding new WebMatrix extension](whats-new-in-aspnet-mvc-4/_static/image53.png "Adding new WebMatrix extension")</span></span>

    <span data-ttu-id="b4414-655">*새 WebMatrix 확장 추가*</span><span class="sxs-lookup"><span data-stu-id="b4414-655">*Adding new WebMatrix extension*</span></span>
3. <span data-ttu-id="b4414-656">**IPhone 시뮬레이터** 를 선택 하 고 **설치**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-656">Select **iPhone Simulator** and click **Install**.</span></span>

    <span data-ttu-id="b4414-657">![WebMatrix 확장 검색](whats-new-in-aspnet-mvc-4/_static/image54.png "WebMatrix 확장 검색")</span><span class="sxs-lookup"><span data-stu-id="b4414-657">![Browsing WebMatrix extensions](whats-new-in-aspnet-mvc-4/_static/image54.png "Browsing WebMatrix extensions")</span></span>

    <span data-ttu-id="b4414-658">*WebMatrix 확장 검색*</span><span class="sxs-lookup"><span data-stu-id="b4414-658">*Browsing WebMatrix extensions*</span></span>
4. <span data-ttu-id="b4414-659">패키지 세부 정보에서 **설치** 를 클릭 하 여 확장 설치를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-659">In the package details, click **Install** to continue with the extension installation.</span></span>

    <span data-ttu-id="b4414-660">![iPhone 시뮬레이터 확장](whats-new-in-aspnet-mvc-4/_static/image55.png "iPhone 시뮬레이터 확장")</span><span class="sxs-lookup"><span data-stu-id="b4414-660">![iPhone Simulator extension](whats-new-in-aspnet-mvc-4/_static/image55.png "iPhone Simulator extension")</span></span>

    <span data-ttu-id="b4414-661">*iPhone 시뮬레이터 확장*</span><span class="sxs-lookup"><span data-stu-id="b4414-661">*iPhone Simulator extension*</span></span>
5. <span data-ttu-id="b4414-662">확장 EULA를 읽고 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-662">Read and accept the extension EULA.</span></span>

    <span data-ttu-id="b4414-663">![WebMatrix 확장 EULA](whats-new-in-aspnet-mvc-4/_static/image56.png "WebMatrix 확장 EULA")</span><span class="sxs-lookup"><span data-stu-id="b4414-663">![WebMatrix extension EULA](whats-new-in-aspnet-mvc-4/_static/image56.png "WebMatrix extension EULA")</span></span>

    <span data-ttu-id="b4414-664">*WebMatrix 확장 EULA*</span><span class="sxs-lookup"><span data-stu-id="b4414-664">*WebMatrix extension EULA*</span></span>
6. <span data-ttu-id="b4414-665">이제 iPhone 시뮬레이터 옵션을 사용 하 여 WebMatrix에서 웹 사이트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-665">Now, you can run your Web site from WebMatrix using the iPhone Simulator option.</span></span>

    <span data-ttu-id="b4414-666">![IPhone을 사용 하 여 실행](whats-new-in-aspnet-mvc-4/_static/image57.png "IPhone을 사용 하 여 실행")</span><span class="sxs-lookup"><span data-stu-id="b4414-666">![Run using iPhone](whats-new-in-aspnet-mvc-4/_static/image57.png "Run using iPhone")</span></span>

    <span data-ttu-id="b4414-667">*IPhone을 사용 하 여 실행*</span><span class="sxs-lookup"><span data-stu-id="b4414-667">*Run using iPhone*</span></span>

<a id="ApxCTask3"></a>

<a id="Task_3_-_Configuring_Visual_Studio_2012_to_run_iPhone_Simulator"></a>
#### <a name="task-3---configuring-visual-studio-2012-to-run-iphone-simulator"></a><span data-ttu-id="b4414-668">작업 3-iPhone 시뮬레이터를 실행 하는 Visual Studio 2012 구성</span><span class="sxs-lookup"><span data-stu-id="b4414-668">Task 3 - Configuring Visual Studio 2012 to run iPhone Simulator</span></span>

1. <span data-ttu-id="b4414-669">**Visual Studio 2012** 을 열고 웹 사이트를 열거나 새 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-669">Open **Visual Studio 2012** and open any Web site or create a new project.</span></span>
2. <span data-ttu-id="b4414-670">실행 단추에서 아래쪽 화살표를 클릭 하 고 **찾아보기를**선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-670">Click the down arrow from the Run button and select **Browse with**.</span></span>

    <span data-ttu-id="b4414-671">![찾아보기](whats-new-in-aspnet-mvc-4/_static/image58.png "찾아보기")</span><span class="sxs-lookup"><span data-stu-id="b4414-671">![Browse with](whats-new-in-aspnet-mvc-4/_static/image58.png "Browse with")</span></span>

    <span data-ttu-id="b4414-672">*찾아보기*</span><span class="sxs-lookup"><span data-stu-id="b4414-672">*Browse with*</span></span>
3. <span data-ttu-id="b4414-673">&quot;&quot;로 찾아보기 대화 상자에서 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-673">In the &quot;Browse With&quot; dialog, click **Add**.</span></span>
4. <span data-ttu-id="b4414-674">&quot;프로그램 추가&quot; 대화 상자에서 다음 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-674">In the &quot;Add Program&quot; dialog, use the following values:</span></span>

   - <span data-ttu-id="b4414-675">**프로그램**: C:\Users\*{CurrentUser} \* \AppData\Local\Microsoft\WebMatrix\Extensions\20\iPhoneSimulator\ElectricMobileSim\ElectricMobileSim.exe *(그에 따라 경로 업데이트)*</span><span class="sxs-lookup"><span data-stu-id="b4414-675">**Program**: C:\Users\*{CurrentUser}\*\AppData\Local\Microsoft\WebMatrix\Extensions\20\iPhoneSimulator\ElectricMobileSim\ElectricMobileSim.exe *(update the path accordingly)*</span></span>
   - <span data-ttu-id="b4414-676">**인수**: &quot;1&quot;</span><span class="sxs-lookup"><span data-stu-id="b4414-676">**Arguments**: &quot;1&quot;</span></span>
   - <span data-ttu-id="b4414-677">**이름**: iPhone 시뮬레이터</span><span class="sxs-lookup"><span data-stu-id="b4414-677">**Friendly name**: iPhone Simulator</span></span>

     <span data-ttu-id="b4414-678">![프로그램 추가](whats-new-in-aspnet-mvc-4/_static/image59.png "프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="b4414-678">![Add program](whats-new-in-aspnet-mvc-4/_static/image59.png "Add program")</span></span>

     <span data-ttu-id="b4414-679">*탐색할 프로그램 추가*</span><span class="sxs-lookup"><span data-stu-id="b4414-679">*Add program to browse with*</span></span>
5. <span data-ttu-id="b4414-680">**확인** 을 클릭 하 고 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-680">Click **OK** and close the dialogs.</span></span>
6. <span data-ttu-id="b4414-681">이제 Visual Studio 2012의 iPhone 시뮬레이터에서 웹 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-681">Now you are able to run your Web applications in the iPhone simulator from Visual Studio 2012.</span></span>

    <span data-ttu-id="b4414-682">![IPhone 시뮬레이터를 사용 하 여 찾아보기](whats-new-in-aspnet-mvc-4/_static/image60.png "IPhone 시뮬레이터를 사용 하 여 찾아보기")</span><span class="sxs-lookup"><span data-stu-id="b4414-682">![Browse with iPhone Simulator](whats-new-in-aspnet-mvc-4/_static/image60.png "Browse with iPhone Simulator")</span></span>

    <span data-ttu-id="b4414-683">*IPhone 시뮬레이터를 사용 하 여 찾아보기*</span><span class="sxs-lookup"><span data-stu-id="b4414-683">*Browse with iPhone Simulator*</span></span>

<a id="AppendixD"></a>

<a id="Appendix_D_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-d-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="b4414-684">부록 D: 웹 배포을 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="b4414-684">Appendix D: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="b4414-685">이 부록에서는 windows azure 관리 포털에서 새 웹 사이트를 만들고 랩에 따라 가져온 응용 프로그램을 게시 하 여 Windows Azure에서 제공 하는 웹 배포 게시 기능을 활용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-685">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxDTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="b4414-686">작업 1-Windows Azure 포털에서 새 웹 사이트 만들기</span><span class="sxs-lookup"><span data-stu-id="b4414-686">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="b4414-687">[Windows Azure 관리 포털](https://manage.windowsazure.com/) 로 이동 하 고 구독과 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-687">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b4414-688">Windows Azure를 사용 하면 10 개의 ASP.NET 웹 사이트를 무료로 호스팅한 후 트래픽 증가에 따라 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-688">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="b4414-689">[여기](https://aka.ms/aspnet-hol-azure)에서 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-689">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="b4414-690">![Windows Azure Portal에 로그온 합니다.](whats-new-in-aspnet-mvc-4/_static/image61.png "Windows Azure Portal에 로그온 합니다.")</span><span class="sxs-lookup"><span data-stu-id="b4414-690">![Log on to Windows Azure portal](whats-new-in-aspnet-mvc-4/_static/image61.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="b4414-691">*Windows Azure 관리 포털에 로그온 합니다.*</span><span class="sxs-lookup"><span data-stu-id="b4414-691">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="b4414-692">명령 모음에서 **새로 만들기** 를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-692">Click **New** on the command bar.</span></span>

    <span data-ttu-id="b4414-693">![새 웹 사이트 만들기](whats-new-in-aspnet-mvc-4/_static/image62.png "새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="b4414-693">![Creating a new Web Site](whats-new-in-aspnet-mvc-4/_static/image62.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="b4414-694">*새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="b4414-694">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="b4414-695">**Compute** | **웹 사이트**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-695">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="b4414-696">그런 다음 **빠른 생성** 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-696">Then select **Quick Create** option.</span></span> <span data-ttu-id="b4414-697">새 웹 사이트에 사용할 수 있는 URL을 제공 하 고 **웹 사이트 만들기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-697">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b4414-698">Microsoft Azure 웹 사이트는 사용자가 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램에 대 한 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-698">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="b4414-699">빠른 생성 옵션을 사용 하면 포털 외부에서 Windows Azure 웹 사이트에 완료 된 웹 응용 프로그램을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-699">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="b4414-700">데이터베이스를 설정 하는 단계는 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-700">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="b4414-701">![빠른 생성을 사용 하 여 새 웹 사이트 만들기](whats-new-in-aspnet-mvc-4/_static/image63.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="b4414-701">![Creating a new Web Site using Quick Create](whats-new-in-aspnet-mvc-4/_static/image63.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="b4414-702">*빠른 생성을 사용 하 여 새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="b4414-702">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="b4414-703">새 **웹 사이트가** 만들어질 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-703">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="b4414-704">웹 사이트를 만든 후 **URL** 열 아래의 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-704">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="b4414-705">새 웹 사이트가 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-705">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="b4414-706">![새 웹 사이트로 이동](whats-new-in-aspnet-mvc-4/_static/image64.png "새 웹 사이트로 이동")</span><span class="sxs-lookup"><span data-stu-id="b4414-706">![Browsing to the new web site](whats-new-in-aspnet-mvc-4/_static/image64.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="b4414-707">*새 웹 사이트로 이동*</span><span class="sxs-lookup"><span data-stu-id="b4414-707">*Browsing to the new web site*</span></span>

    <span data-ttu-id="b4414-708">![웹 사이트 실행 중](whats-new-in-aspnet-mvc-4/_static/image65.png "웹 사이트 실행 중")</span><span class="sxs-lookup"><span data-stu-id="b4414-708">![Web site running](whats-new-in-aspnet-mvc-4/_static/image65.png "Web site running")</span></span>

    <span data-ttu-id="b4414-709">*웹 사이트 실행 중*</span><span class="sxs-lookup"><span data-stu-id="b4414-709">*Web site running*</span></span>
6. <span data-ttu-id="b4414-710">포털로 돌아가서 **이름** 열 아래에 있는 웹 사이트의 이름을 클릭 하 여 관리 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-710">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="b4414-711">![웹 사이트 관리 페이지 열기](whats-new-in-aspnet-mvc-4/_static/image66.png "웹 사이트 관리 페이지 열기")</span><span class="sxs-lookup"><span data-stu-id="b4414-711">![Opening the web site management pages](whats-new-in-aspnet-mvc-4/_static/image66.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="b4414-712">*웹 사이트 관리 페이지 열기*</span><span class="sxs-lookup"><span data-stu-id="b4414-712">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="b4414-713">**대시보드** 페이지의 **빠른** 보기 섹션에서 **게시 프로필 다운로드** 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-713">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b4414-714">*게시 프로필* 에는 사용 하도록 설정 된 각 게시 방법에 대해 웹 응용 프로그램을 Windows Azure 웹 사이트에 게시 하는 데 필요한 모든 정보가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-714">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="b4414-715">게시 프로필에는 게시 방법이 활성화 된 각 끝점에 대 한 연결 및 인증에 필요한 Url, 사용자 자격 증명 및 데이터베이스 문자열이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-715">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="b4414-716">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** 및 **Microsoft Visual Studio 2012** 는 게시 프로필 읽기를 지원 하 여 웹 응용 프로그램을 Windows Azure 웹 사이트에 게시 하기 위해 이러한 프로그램의 구성을 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-716">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="b4414-717">![웹 사이트 게시 프로필을 다운로드 하는 중](whats-new-in-aspnet-mvc-4/_static/image67.png "웹 사이트 게시 프로필을 다운로드 하는 중")</span><span class="sxs-lookup"><span data-stu-id="b4414-717">![Downloading the web site publish profile](whats-new-in-aspnet-mvc-4/_static/image67.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="b4414-718">*웹 사이트 게시 프로필을 다운로드 하는 중*</span><span class="sxs-lookup"><span data-stu-id="b4414-718">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="b4414-719">알려진 위치에 게시 프로필 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-719">Download the publish profile file to a known location.</span></span> <span data-ttu-id="b4414-720">이 연습을 통해이 파일을 사용 하 여 Visual Studio에서 Windows Azure 웹 사이트에 웹 응용 프로그램을 게시 하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-720">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="b4414-721">![게시 프로필 파일을 저장 하는 중](whats-new-in-aspnet-mvc-4/_static/image68.png "게시 프로필을 저장 하는 중")</span><span class="sxs-lookup"><span data-stu-id="b4414-721">![Saving the publish profile file](whats-new-in-aspnet-mvc-4/_static/image68.png "Saving the publish profile")</span></span>

    <span data-ttu-id="b4414-722">*게시 프로필 파일을 저장 하는 중*</span><span class="sxs-lookup"><span data-stu-id="b4414-722">*Saving the publish profile file*</span></span>

<a id="ApxDTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="b4414-723">작업 2-데이터베이스 서버 구성</span><span class="sxs-lookup"><span data-stu-id="b4414-723">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="b4414-724">응용 프로그램에서 SQL Server 데이터베이스를 사용 하는 경우 SQL Database 서버를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-724">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="b4414-725">SQL Server 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 작업을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-725">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="b4414-726">응용 프로그램 데이터베이스를 저장 하기 위한 SQL Database 서버가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-726">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="b4414-727">Microsoft Azure 관리 포털의 구독에서 SQL Database 서버를 볼 수는 **SQL 데이터베이스** | **서버** | **서버의 대시보드**.</span><span class="sxs-lookup"><span data-stu-id="b4414-727">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="b4414-728">만든 서버가 없는 경우 명령 모음에서 **추가** 단추를 사용 하 여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-728">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="b4414-729">다음 작업에서 사용할 **서버 이름과 URL, 관리자 로그인 이름 및 암호**를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-729">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="b4414-730">이후 단계에서 생성 되므로 아직 데이터베이스를 만들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="b4414-730">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="b4414-731">![SQL Database 서버 대시보드](whats-new-in-aspnet-mvc-4/_static/image69.png "SQL Database 서버 대시보드")</span><span class="sxs-lookup"><span data-stu-id="b4414-731">![SQL Database Server Dashboard](whats-new-in-aspnet-mvc-4/_static/image69.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="b4414-732">*SQL Database 서버 대시보드*</span><span class="sxs-lookup"><span data-stu-id="b4414-732">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="b4414-733">다음 작업에서는 Visual Studio에서 데이터베이스 연결을 테스트 합니다. 따라서 서버에서 **허용 되는 Ip 주소**목록에 로컬 IP 주소를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-733">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="b4414-734">이렇게 하려면 **구성**을 클릭 하 고, **현재 클라이언트 IP 주소** 에서 ip 주소를 선택 하 고, **시작 Ip 주소** 및 **끝 ip 주소** 텍스트 상자에 붙여 넣고, ![추가-클라이언트-ip 주소-확인 단추](whats-new-in-aspnet-mvc-4/_static/image70.png) 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-734">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](whats-new-in-aspnet-mvc-4/_static/image70.png) button.</span></span>

    ![클라이언트 IP 주소를 추가 하는 중](whats-new-in-aspnet-mvc-4/_static/image71.png)

    <span data-ttu-id="b4414-736">*클라이언트 IP 주소를 추가 하는 중*</span><span class="sxs-lookup"><span data-stu-id="b4414-736">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="b4414-737">**클라이언트 Ip 주소가** 허용 된 ip 주소 목록에 추가 되 면 **저장** 을 클릭 하 여 변경 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-737">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![변경 내용 확인](whats-new-in-aspnet-mvc-4/_static/image72.png)

    <span data-ttu-id="b4414-739">*변경 내용 확인*</span><span class="sxs-lookup"><span data-stu-id="b4414-739">*Confirm Changes*</span></span>

<a id="ApxDTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="b4414-740">작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="b4414-740">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="b4414-741">ASP.NET MVC 4 솔루션으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-741">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="b4414-742">**솔루션 탐색기**에서 웹 사이트 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-742">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="b4414-743">![응용 프로그램 게시](whats-new-in-aspnet-mvc-4/_static/image73.png "发布应用程序")</span><span class="sxs-lookup"><span data-stu-id="b4414-743">![Publishing the Application](whats-new-in-aspnet-mvc-4/_static/image73.png "Publishing the Application")</span></span>

    <span data-ttu-id="b4414-744">*웹 사이트 게시*</span><span class="sxs-lookup"><span data-stu-id="b4414-744">*Publishing the web site*</span></span>
2. <span data-ttu-id="b4414-745">첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-745">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="b4414-746">![게시 프로필을 가져오는 중](whats-new-in-aspnet-mvc-4/_static/image74.png "게시 프로필을 가져오는 중")</span><span class="sxs-lookup"><span data-stu-id="b4414-746">![Importing the publish profile](whats-new-in-aspnet-mvc-4/_static/image74.png "Importing the publish profile")</span></span>

    <span data-ttu-id="b4414-747">*게시 프로필을 가져오는 중*</span><span class="sxs-lookup"><span data-stu-id="b4414-747">*Importing publish profile*</span></span>
3. <span data-ttu-id="b4414-748">**연결 유효성 검사**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-748">Click **Validate Connection**.</span></span> <span data-ttu-id="b4414-749">유효성 검사가 완료 되 면 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-749">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b4414-750">유효성 검사는 연결 유효성 검사 단추 옆에 녹색 확인 표시가 표시 되 면 완료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-750">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="b4414-751">![연결 유효성 검사](whats-new-in-aspnet-mvc-4/_static/image75.png "연결 유효성 검사")</span><span class="sxs-lookup"><span data-stu-id="b4414-751">![Validating connection](whats-new-in-aspnet-mvc-4/_static/image75.png "Validating connection")</span></span>

    <span data-ttu-id="b4414-752">*연결 유효성 검사*</span><span class="sxs-lookup"><span data-stu-id="b4414-752">*Validating connection*</span></span>
4. <span data-ttu-id="b4414-753">**설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆에 있는 단추 (즉, **defaultconnection**)를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-753">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="b4414-754">![웹 배포 구성](whats-new-in-aspnet-mvc-4/_static/image76.png "웹 배포 구성")</span><span class="sxs-lookup"><span data-stu-id="b4414-754">![Web deploy configuration](whats-new-in-aspnet-mvc-4/_static/image76.png "Web deploy configuration")</span></span>

    <span data-ttu-id="b4414-755">*웹 배포 구성*</span><span class="sxs-lookup"><span data-stu-id="b4414-755">*Web deploy configuration*</span></span>
5. <span data-ttu-id="b4414-756">데이터베이스 연결을 다음과 같이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-756">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="b4414-757">**서버 이름** 에 *tcp:* 접두사를 사용 하 여 SQL Database 서버 URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-757">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="b4414-758">**사용자 이름** 에 서버 관리자 로그인 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-758">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="b4414-759">**암호** 에 서버 관리자 로그인 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-759">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="b4414-760">새 데이터베이스 이름 (예: *MVC4SampleDB*)을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-760">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="b4414-761">![대상 연결 문자열 구성](whats-new-in-aspnet-mvc-4/_static/image77.png "대상 연결 문자열 구성")</span><span class="sxs-lookup"><span data-stu-id="b4414-761">![Configuring destination connection string](whats-new-in-aspnet-mvc-4/_static/image77.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="b4414-762">*대상 연결 문자열 구성*</span><span class="sxs-lookup"><span data-stu-id="b4414-762">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="b4414-763">然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="b4414-763">Then click **OK**.</span></span> <span data-ttu-id="b4414-764">데이터베이스를 만들 것인지 묻는 메시지가 표시 되 면 **예**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-764">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="b4414-765">![데이터베이스 만들기](whats-new-in-aspnet-mvc-4/_static/image78.png "데이터베이스 문자열 만들기")</span><span class="sxs-lookup"><span data-stu-id="b4414-765">![Creating the database](whats-new-in-aspnet-mvc-4/_static/image78.png "Creating the database string")</span></span>

    <span data-ttu-id="b4414-766">*데이터베이스 만들기*</span><span class="sxs-lookup"><span data-stu-id="b4414-766">*Creating the database*</span></span>
7. <span data-ttu-id="b4414-767">Windows Azure에서 SQL Database에 연결 하는 데 사용할 연결 문자열은 기본 연결 텍스트 상자 내에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-767">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="b4414-768">然后单击 **“下一步”** 。</span><span class="sxs-lookup"><span data-stu-id="b4414-768">Then click **Next**.</span></span>

    <span data-ttu-id="b4414-769">![SQL Database를 가리키는 연결 문자열](whats-new-in-aspnet-mvc-4/_static/image79.png "SQL Database를 가리키는 연결 문자열")</span><span class="sxs-lookup"><span data-stu-id="b4414-769">![Connection string pointing to SQL Database](whats-new-in-aspnet-mvc-4/_static/image79.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="b4414-770">*SQL Database를 가리키는 연결 문자열*</span><span class="sxs-lookup"><span data-stu-id="b4414-770">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="b4414-771">**미리 보기** 페이지에서 **게시**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-771">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="b4414-772">![웹 응용 프로그램 게시](whats-new-in-aspnet-mvc-4/_static/image80.png "웹 응용 프로그램 게시")</span><span class="sxs-lookup"><span data-stu-id="b4414-772">![Publishing the web application](whats-new-in-aspnet-mvc-4/_static/image80.png "Publishing the web application")</span></span>

    <span data-ttu-id="b4414-773">*웹 응용 프로그램 게시*</span><span class="sxs-lookup"><span data-stu-id="b4414-773">*Publishing the web application*</span></span>
9. <span data-ttu-id="b4414-774">게시 프로세스가 완료 되 면 기본 브라우저가 게시 된 웹 사이트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b4414-774">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="b4414-775">![Windows Azure에 게시 된 응용 프로그램](whats-new-in-aspnet-mvc-4/_static/image81.png "Windows Azure에 게시 된 응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="b4414-775">![Application published to Windows Azure](whats-new-in-aspnet-mvc-4/_static/image81.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="b4414-776">*Windows Azure에 게시 된 응용 프로그램*</span><span class="sxs-lookup"><span data-stu-id="b4414-776">*Application published to Windows Azure*</span></span>
