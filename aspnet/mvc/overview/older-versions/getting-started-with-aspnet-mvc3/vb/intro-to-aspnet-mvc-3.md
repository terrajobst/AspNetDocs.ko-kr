---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
title: ASP.NET MVC 3 소개 (VB) | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1 (...)을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 학습 합니다.
ms.author: riande
ms.date: 01/12/2011
ms.assetid: a1b3d789-93b4-487f-b90d-80c9c9b4f8fa
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: 24f7de303ef7f5a457bd509ecc6bd0e3be7e3d9d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485495"
---
# <a name="intro-to-aspnet-mvc-3-vb"></a><span data-ttu-id="c2d45-103">ASP.NET MVC 3 소개(VB)</span><span class="sxs-lookup"><span data-stu-id="c2d45-103">Intro to ASP.NET MVC 3 (VB)</span></span>

<span data-ttu-id="c2d45-104">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="c2d45-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="c2d45-105">이 자습서에서는 Microsoft Visual Studio의 무료 버전인 Microsoft Visual Web Developer 2010 Express 서비스 팩 1을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="c2d45-106">시작 하기 전에 아래 나열 된 필수 구성 요소를 설치 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="c2d45-107">[웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)링크를 클릭 하 여 모든 항목을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="c2d45-108">또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="c2d45-109">Visual Studio Web Developer Express SP1 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="c2d45-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="c2d45-110">ASP.NET MVC 3 도구 업데이트</span><span class="sxs-lookup"><span data-stu-id="c2d45-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="c2d45-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)</span><span class="sxs-lookup"><span data-stu-id="c2d45-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="c2d45-112">Visual Web Developer 2010 대신 Visual Studio 2010을 사용 하는 경우 [Visual studio 2010 필수 조건](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)링크를 클릭 하 여 필수 구성 요소를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="c2d45-113">VB.NET 소스 코드를 사용 하는 Visual Web Developer 프로젝트를이 항목과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="c2d45-114">[VB.NET 버전을 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="c2d45-115">선호 C#하는 경우이 자습서의 [ C# 버전](../cs/intro-to-aspnet-mvc-3.md) 으로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-115">If you prefer C#, switch to the [C# version](../cs/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

<span data-ttu-id="c2d45-116">이 자습서에서는 Microsoft Visual Studio의 무료 버전인 Microsoft Visual Web Developer 2010 Express 서비스 팩 1을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-116">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="c2d45-117">시작 하기 전에 아래 나열 된 필수 구성 요소를 설치 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-117">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="c2d45-118">[웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)링크를 클릭 하 여 모든 항목을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-118">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="c2d45-119">또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-119">Alternatively, you can individually install the prerequisites using the following links:</span></span>

- [<span data-ttu-id="c2d45-120">Visual Studio Web Developer Express SP1 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="c2d45-120">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
- [<span data-ttu-id="c2d45-121">ASP.NET MVC 3 도구 업데이트</span><span class="sxs-lookup"><span data-stu-id="c2d45-121">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- <span data-ttu-id="c2d45-122">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)</span><span class="sxs-lookup"><span data-stu-id="c2d45-122">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>

<span data-ttu-id="c2d45-123">Visual Web Developer 2010 대신 Visual Studio 2010을 사용 하는 경우 [Visual studio 2010 필수 조건](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)링크를 클릭 하 여 필수 구성 요소를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-123">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>

<span data-ttu-id="c2d45-124">이 항목과 함께 사용할 수 있는 VB 소스 코드가 포함 된 Visual Web Developer 프로젝트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-124">A Visual Web Developer project with VB source code is available to accompany this topic.</span></span> <span data-ttu-id="c2d45-125">[여기에서 VB 버전을 다운로드](https://code.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=14824)합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-125">[Download the VB version here](https://code.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=14824).</span></span> <span data-ttu-id="c2d45-126">CSharp를 선호 하는 경우이 자습서의 [csharp 버전](../cs/intro-to-aspnet-mvc-3.md) 으로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-126">If you prefer CSharp, switch to the [CSharp version](../cs/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="c2d45-127">만들 내용</span><span class="sxs-lookup"><span data-stu-id="c2d45-127">What You'll Build</span></span>

<span data-ttu-id="c2d45-128">데이터베이스에서 동영상 만들기, 편집 및 나열을 지 원하는 간단한 동영상 목록 응용 프로그램을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-128">You'll implement a simple movie-listing application that supports creating, editing, and listing movies from a database.</span></span> <span data-ttu-id="c2d45-129">다음은 빌드할 응용 프로그램의 두 가지 스크린샷입니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-129">Below are two screenshots of the application you'll build.</span></span> <span data-ttu-id="c2d45-130">여기에는 데이터베이스의 영화 목록을 표시 하는 페이지가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-130">It includes a page that displays a list of movies from a database:</span></span>

<span data-ttu-id="c2d45-131">[![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image2.png)](intro-to-aspnet-mvc-3/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c2d45-131">[![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image2.png)](intro-to-aspnet-mvc-3/_static/image1.png)</span></span>

<span data-ttu-id="c2d45-132">응용 프로그램을 사용 하 여 영화를 추가, 편집 및 삭제할 수 있을 뿐 아니라 개별 항목에 대 한 세부 정보를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-132">The application also lets you add, edit, and delete movies, as well as see details about individual ones.</span></span> <span data-ttu-id="c2d45-133">모든 데이터 입력 시나리오에는 데이터베이스에 저장 된 데이터가 올바른지 확인 하기 위한 유효성 검사가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-133">All data-entry scenarios include validation to ensure that the data stored in the database is correct.</span></span>

<span data-ttu-id="c2d45-134">[CreateFormSo](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)![</span><span class="sxs-lookup"><span data-stu-id="c2d45-134">[![CreateFormSo](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)</span></span>

## <a name="skills-youll-learn"></a><span data-ttu-id="c2d45-135">학습할 기술</span><span class="sxs-lookup"><span data-stu-id="c2d45-135">Skills You'll Learn</span></span>

<span data-ttu-id="c2d45-136">다음 내용을 학습하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-136">Here's what you'll learn:</span></span>

- <span data-ttu-id="c2d45-137">새 ASP.NET MVC 프로젝트를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="c2d45-137">How to create a new ASP.NET MVC project</span></span>
- <span data-ttu-id="c2d45-138">Entity Framework 코드를 사용 하 여 새 데이터베이스를 만드는 방법-우선</span><span class="sxs-lookup"><span data-stu-id="c2d45-138">How to create a new database using Entity Framework code-first</span></span>
- <span data-ttu-id="c2d45-139">ASP.NET MVC 컨트롤러 및 뷰를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="c2d45-139">How to create ASP.NET MVC controllers and views</span></span>
- <span data-ttu-id="c2d45-140">데이터를 검색 하 고 표시 하는 방법</span><span class="sxs-lookup"><span data-stu-id="c2d45-140">How to retrieve and display data</span></span>
- <span data-ttu-id="c2d45-141">데이터를 편집 하 고 데이터 유효성 검사를 사용 하도록 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="c2d45-141">How to edit data and enable data validation</span></span>

## <a name="getting-started"></a><span data-ttu-id="c2d45-142">시작하기</span><span class="sxs-lookup"><span data-stu-id="c2d45-142">Getting Started</span></span>

<span data-ttu-id="c2d45-143">먼저 Visual Web Developer 2010 Express (short의 경우 "VWD")를 실행 하 고 **시작** 페이지에서 **새 프로젝트** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-143">Start by running Visual Web Developer 2010 Express ("VWD" for short) and select **New Project** from the **Start** page.</span></span>

<span data-ttu-id="c2d45-144">Visual Web Developer는 IDE (통합 개발 환경)입니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-144">Visual Web Developer is an IDE, or integrated development environment.</span></span> <span data-ttu-id="c2d45-145">Microsoft Word를 사용 하 여 문서를 작성 하는 것 처럼 IDE를 사용 하 여 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-145">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="c2d45-146">Visual Web Developer에는 제공 되는 다양 한 옵션을 보여 주는 도구 모음이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-146">In Visual Web Developer there's a toolbar along the top showing various options available to you.</span></span> <span data-ttu-id="c2d45-147">IDE에서 작업을 수행 하는 다른 방법을 제공 하는 메뉴도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-147">There's also a menu that provides another way to perform tasks in the IDE.</span></span> <span data-ttu-id="c2d45-148">예를 들어 **시작** 페이지에서 **새 프로젝트** 를 선택 하는 대신 메뉴를 사용 하 여 **파일** &gt; **새 프로젝트**를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-148">(For example, instead of selecting **New Project** from the **Start** page, you can use the menu and select **File** &gt; **New Project**.)</span></span>

[![](intro-to-aspnet-mvc-3/_static/image6.png)](intro-to-aspnet-mvc-3/_static/image5.png)

## <a name="creating-your-first-application"></a><span data-ttu-id="c2d45-149">첫 번째 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="c2d45-149">Creating Your First Application</span></span>

<span data-ttu-id="c2d45-150">Visual Basic 또는 시각적 개체 C# 중 하나를 프로그래밍 언어로 사용 하 여 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-150">You can create applications using your choice of either Visual Basic or Visual C# as the programming language.</span></span> <span data-ttu-id="c2d45-151">이 자습서에서는 왼쪽에서 Visual Basic를 선택한 다음 **ASP.NET MVC 3 웹 응용 프로그램**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-151">For this tutorial, select Visual Basic on the left, then select **ASP.NET MVC 3 Web Application**.</span></span> <span data-ttu-id="c2d45-152">프로젝트 이름을 "MvcMovie"로 지정한 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-152">Name your project "MvcMovie" and then click **OK**.</span></span>

![1NewMVCproj_sm](intro-to-aspnet-mvc-3/_static/image7.png)

<span data-ttu-id="c2d45-154">**새 ASP.NET MVC 3 프로젝트** 대화 상자에서 **인터넷 응용 프로그램**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-154">In the **New ASP.NET MVC 3 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="c2d45-155">기본 뷰 엔진으로 **Razor** 를 남겨 둡니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-155">Leave **Razor** as the default view engine.</span></span>

![1InternetAppRazor_SM](intro-to-aspnet-mvc-3/_static/image8.png)

<span data-ttu-id="c2d45-157">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-157">Click **OK**.</span></span> <span data-ttu-id="c2d45-158">Visual Web Developer는 방금 만든 ASP.NET MVC 프로젝트에 대 한 기본 템플릿을 사용 했으므로 이제는 작업을 수행 하지 않고 작업 중인 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-158">Visual Web Developer used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="c2d45-159">이는 간단한 "Hello World!"입니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-159">This is a simple "Hello World!"</span></span> <span data-ttu-id="c2d45-160">프로젝트를 시작 하 고 응용 프로그램을 시작 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-160">project, and it's a good place to start your application.</span></span>

[![](intro-to-aspnet-mvc-3/_static/image10.png)](intro-to-aspnet-mvc-3/_static/image9.png)

<span data-ttu-id="c2d45-161">**디버그** 메뉴에서 **디버깅 시작**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-161">From the **Debug** menu, select **Start Debugging**.</span></span>

![](intro-to-aspnet-mvc-3/_static/image11.png)

<span data-ttu-id="c2d45-162">디버깅을 시작 하는 바로 가기 키는 F5입니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-162">Notice that the keyboard shortcut to start debugging is F5.</span></span>

<span data-ttu-id="c2d45-163">F5 키를 누르면 Visual Web Developer에서 개발 웹 서버를 시작 하 고 웹 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-163">F5 causes Visual Web Developer to start a development web server and run your web application.</span></span> <span data-ttu-id="c2d45-164">그러면 VWD에서 브라우저를 시작 하 고 응용 프로그램의 홈 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-164">VWD then launches a browser and opens the application's home page.</span></span> <span data-ttu-id="c2d45-165">브라우저의 주소 표시줄에 `localhost` 표시 되 고 `example.com`와 같은 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-165">Notice that the address bar of the browser says `localhost` and not something like `example.com`.</span></span> <span data-ttu-id="c2d45-166">`localhost`은 항상 자신의 로컬 컴퓨터를 가리키지만이 경우에는 방금 빌드한 응용 프로그램을 실행 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-166">That's because `localhost` always points to your own local computer, which in this case is running the application you just built.</span></span> <span data-ttu-id="c2d45-167">VWD에서 웹 프로젝트를 실행 하면 프로젝트에 대해 임의의 포트가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-167">When VWD runs a web project, a random port is used for the project.</span></span> <span data-ttu-id="c2d45-168">아래 이미지에서 임의의 포트 번호는 43246입니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-168">In the image below, the random port number is 43246.</span></span> <span data-ttu-id="c2d45-169">프로젝트에서 다른 포트 번호를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-169">Your project will probably use a different port number.</span></span>

![](intro-to-aspnet-mvc-3/_static/image12.png)

<span data-ttu-id="c2d45-170">기본적으로이 기본 템플릿은 방문할 두 페이지와 기본 로그인 페이지를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-170">Out of the box this default template gives you two pages to visit and a basic login page.</span></span> <span data-ttu-id="c2d45-171">이 응용 프로그램의 작동 방식을 변경 하 고 프로세스에서 ASP.NET MVC에 대해 약간의 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-171">Let's change how this application works and learn a little bit about ASP.NET MVC in the process.</span></span> <span data-ttu-id="c2d45-172">브라우저를 닫고 일부 코드를 변경 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d45-172">Close your browser and let's change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="c2d45-173">다음</span><span class="sxs-lookup"><span data-stu-id="c2d45-173">Next</span></span>](adding-a-controller.md)
