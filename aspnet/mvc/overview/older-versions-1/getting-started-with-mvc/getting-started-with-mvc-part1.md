---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
title: ASP.NET MVC 소개 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 데이터베이스에서 읽고 쓰는 간단한 웹 응용 프로그램을 만듭니다.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: bf4a1c19-0a94-4208-b268-a96ddcf26946
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
msc.type: authoredcontent
ms.openlocfilehash: f8f0014776ba1313119e8c39c63a216b0fc864e7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469799"
---
# <a name="intro-to-aspnet-mvc"></a><span data-ttu-id="67a9d-104">ASP.NET MVC 소개</span><span class="sxs-lookup"><span data-stu-id="67a9d-104">Intro to ASP.NET MVC</span></span>

<span data-ttu-id="67a9d-105">[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="67a9d-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> > [!NOTE]
> > <span data-ttu-id="67a9d-106">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)를 [사용 하 여](../../getting-started/introduction/getting-started.md) 이 자습서를 사용할 수 있는 경우 업데이트 된 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-106">An updated version if this tutorial is available [here](../../getting-started/introduction/getting-started.md) using [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013).</span></span> <span data-ttu-id="67a9d-107">새 자습서에서는이 자습서를 통해 많은 향상 된 기능을 제공 하는 ASP.NET MVC 5를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-107">The new tutorial uses ASP.NET MVC 5, which provides many improvements over this tutorial.</span></span>
>
>
> <span data-ttu-id="67a9d-108">ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-108">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="67a9d-109">데이터베이스에서 읽고 쓰는 간단한 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-109">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="67a9d-110">[ASP.NET mvc 학습 센터](../../../index.md) 를 방문 하 여 다른 ASP.NET mvc 자습서 및 샘플을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-110">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="67a9d-111">[Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/)를 사용 하 여 첫 번째 ASP.NET MVC 웹 응용 프로그램을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-111">Let's make our first ASP.NET MVC Web Application using [Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/).</span></span> <span data-ttu-id="67a9d-112">영화를 만들고 나열 하는 데 도움이 되는 약간의 영화 목록 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-112">We'll make a little Movie list application that will let us create and list movies.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="67a9d-113">만들 내용</span><span class="sxs-lookup"><span data-stu-id="67a9d-113">What You'll Build</span></span>

<span data-ttu-id="67a9d-114">빌드할 응용 프로그램의 두 스크린샷은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-114">Here are two screenshots of the application you'll build.</span></span> <span data-ttu-id="67a9d-115">다양 한 열이 포함 된 간단한 영화 테이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-115">You will have a simple table of movies with various columns.</span></span>

<span data-ttu-id="67a9d-116">[![동영상 목록-Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="67a9d-116">[![Movie List - Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)</span></span>

<span data-ttu-id="67a9d-117">그리고 목록에 영화를 추가할 수 있도록 만들기 양식이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-117">And you'll have a Create Form so we can add movies to the list.</span></span>

<span data-ttu-id="67a9d-118">[동영상 ![만들기-Windows Internet Explorer (2)](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="67a9d-118">[![Create a Movie - Windows Internet Explorer (2)](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)</span></span>

## <a name="skills-youll-learn"></a><span data-ttu-id="67a9d-119">학습할 기술</span><span class="sxs-lookup"><span data-stu-id="67a9d-119">Skills You'll Learn</span></span>

<span data-ttu-id="67a9d-120">이 자습서에서는 Visual Studio를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-120">This tutorial will teach you the basics of building an ASP.NET MVC Web Application using Visual Studio.</span></span> <span data-ttu-id="67a9d-121">다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-121">You'll learn:</span></span>

- <span data-ttu-id="67a9d-122">새 ASP.NET MVC 프로젝트를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="67a9d-122">How to create a new ASP.NET MVC Project</span></span>
- <span data-ttu-id="67a9d-123">SQL Server를 사용 하 여 새 데이터베이스를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="67a9d-123">How to create a new Database with SQL Server</span></span>
- <span data-ttu-id="67a9d-124">ASP.NET MVC 컨트롤러 및 뷰를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="67a9d-124">How to create ASP.NET MVC Controllers and Views</span></span>
- <span data-ttu-id="67a9d-125">데이터를 검색 하 고 표시 하는 방법</span><span class="sxs-lookup"><span data-stu-id="67a9d-125">How to retrieve and display data</span></span>
- <span data-ttu-id="67a9d-126">데이터를 편집 하 고 데이터 유효성 검사를 사용 하도록 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="67a9d-126">How to edit data and enable data validation</span></span>
- <span data-ttu-id="67a9d-127">데이터베이스 스키마를 업데이트 하는 방법</span><span class="sxs-lookup"><span data-stu-id="67a9d-127">How to update the database schema</span></span>

## <a name="get-started"></a><span data-ttu-id="67a9d-128">시작</span><span class="sxs-lookup"><span data-stu-id="67a9d-128">Get Started</span></span>

<span data-ttu-id="67a9d-129">Visual Web Developer 2010 Express를 실행 하 여 시작 합니다 (지금부터 "VWD" 이라고 함). 그런 다음 시작 화면에서 새 프로젝트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-129">Start by running Visual Web Developer 2010 Express (I'll call it "VWD" from now on) and select New Project from the Start Screen.</span></span>

<span data-ttu-id="67a9d-130">Visual Web Developer는 IDE 또는 통합 된 개발자 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-130">Visual Web Developer is an IDE, or Integrated Developer Environment.</span></span> <span data-ttu-id="67a9d-131">Microsoft Word를 사용 하 여 문서를 작성 하는 것 처럼 IDE를 사용 하 여 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-131">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="67a9d-132">사용자에 게 제공 되는 다양 한 옵션 및 파일을 선택 하는 데 사용 하는 메뉴를 보여 주는 도구 모음이 있습니다. 새 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-132">There's a toolbar along the top showing various options available to you, as well as the menu you could also have used to Select File | New project.</span></span>

<span data-ttu-id="67a9d-133">[Microsoft Visual Web Developer 2010 Express ![](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="67a9d-133">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)</span></span>

## <a name="creating-your-first-application"></a><span data-ttu-id="67a9d-134">첫 번째 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="67a9d-134">Creating Your First Application</span></span>

<span data-ttu-id="67a9d-135">Visual Basic 또는 시각적 개체 C#를 사용 하 여 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-135">You can create applications using Visual Basic or Visual C#.</span></span> <span data-ttu-id="67a9d-136">지금은 왼쪽에서 시각적 개체 C# 를 선택 하 고 "ASP.NET MVC 2 웹 응용 프로그램"을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-136">For now, Select Visual C# on the left, then pick "ASP.NET MVC 2 Web Application."</span></span> <span data-ttu-id="67a9d-137">프로젝트 이름을 "영화"로, 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-137">Name your project "Movies" and click OK.</span></span>

<span data-ttu-id="67a9d-138">[새 프로젝트 ![](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="67a9d-138">[![New Project](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)</span></span>

<span data-ttu-id="67a9d-139">오른쪽에는 응용 프로그램의 모든 파일 및 폴더를 표시 하는 솔루션 탐색기 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-139">On the right-hand side is the Solution Explorer showing all the files and folders in your application.</span></span> <span data-ttu-id="67a9d-140">가운데에 있는 큰 창에서는 코드를 편집 하 여 대부분의 시간을 소비 합니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-140">The big window in the middle is where you edit your code and spend most of your time.</span></span> <span data-ttu-id="67a9d-141">Visual Studio는 방금 만든 ASP.NET MVC 프로젝트에 대 한 기본 템플릿을 사용 하 여 작업을 수행 하는 응용 프로그램을 지금 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-141">Visual Studio used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="67a9d-142">이는 간단한 "Hello World!</span><span class="sxs-lookup"><span data-stu-id="67a9d-142">This is a simple "Hello World!</span></span> <span data-ttu-id="67a9d-143">프로젝트를 시작 하 고 응용 프로그램을 시작 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-143">project, and it is a good place to start for our application.</span></span>

<span data-ttu-id="67a9d-144">[Microsoft Visual Web Developer 2010 Express ![](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="67a9d-144">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)</span></span>

<span data-ttu-id="67a9d-145">도구 모음에 대 한 "재생" 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-145">Select the "play" button to the toolbar.</span></span>

![디버그](getting-started-with-mvc-part1/_static/image11.png)

<span data-ttu-id="67a9d-147">프로그램을 컴파일하고 웹 브라우저에서 응용 프로그램을 시작 하는 오른쪽을 가리키는 녹색 화살표입니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-147">It's a green arrow pointing to the right that will compile your program and start your application in a web browser.</span></span>

<span data-ttu-id="67a9d-148">*참고: 대신 키보드에서 F5 키를 누르거나 디버그-&gt;"디버그" 메뉴에서 디버깅 시작을 선택할 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="67a9d-148">*NOTE: You can instead press F5 on your keyboard, or select Debug-&gt;Start Debugging from the "Debug" menu.*</span></span>

<span data-ttu-id="67a9d-149">이렇게 하면 Visual Web Developer에서 개발 웹 서버를 시작 하 고 웹 응용 프로그램을 실행 합니다 .이를 사용 하도록 설정 하는 데 필요한 구성 또는 수동 단계가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-149">This will cause Visual Web Developer to start a development web-server and run our web application (there are no configuration or manual steps required to enable this).</span></span> <span data-ttu-id="67a9d-150">그런 다음 브라우저를 시작 하 고 응용 프로그램의 홈 페이지를 검색 하도록 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-150">It will then launch a browser and configure it to browse the application's home-page.</span></span> <span data-ttu-id="67a9d-151">아래에서 브라우저의 주소 표시줄에는 "localhost"가 표시 되 고 example.com와 같은 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-151">Notice below that the address bar of the browser says "localhost", and not something like example.com.</span></span> <span data-ttu-id="67a9d-152">Localhost는 항상 자신의 로컬 컴퓨터를 가리키지만 (이 경우 방금 빌드한 응용 프로그램을 실행 하는 경우).</span><span class="sxs-lookup"><span data-stu-id="67a9d-152">That's because localhost always points to your own local computer - which in this case is running the application we just built.</span></span>

<span data-ttu-id="67a9d-153">[![홈페이지](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="67a9d-153">[![Home Page](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)</span></span>

<span data-ttu-id="67a9d-154">기본적으로이 기본 템플릿은 방문할 두 페이지와 기본 로그인 페이지를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-154">Out of the box this default template gives you two pages to visit and a basic login page.</span></span> <span data-ttu-id="67a9d-155">이 응용 프로그램의 작동 방식을 변경 하 고 프로세스에서 ASP.NET MVC에 대해 약간의 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-155">Let's change how this application works and learn a little bit about ASP.NET MVC in the process.</span></span> <span data-ttu-id="67a9d-156">브라우저를 닫고 일부 코드를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67a9d-156">Close your browser and lets change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="67a9d-157">다음</span><span class="sxs-lookup"><span data-stu-id="67a9d-157">Next</span></span>](getting-started-with-mvc-part2.md)
