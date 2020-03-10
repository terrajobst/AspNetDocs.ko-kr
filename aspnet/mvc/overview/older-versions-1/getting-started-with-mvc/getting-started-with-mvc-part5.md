---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
title: 컨트롤러에서 모델의 데이터에 액세스 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 데이터베이스에서 읽고 쓰는 간단한 웹 응용 프로그램을 만듭니다.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 004703cd-e0e9-4ba7-9974-1b0475c71222
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
msc.type: authoredcontent
ms.openlocfilehash: 207ed880977d794d81efdc1ea458d17a68d501d8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437369"
---
# <a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="dfc1c-104">컨트롤러에서 모델의 데이터에 액세스</span><span class="sxs-lookup"><span data-stu-id="dfc1c-104">Accessing your Model's Data from a Controller</span></span>

<span data-ttu-id="dfc1c-105">[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="dfc1c-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="dfc1c-106">ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="dfc1c-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="dfc1c-107">데이터베이스에서 읽고 쓰는 간단한 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dfc1c-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="dfc1c-108">[ASP.NET mvc 학습 센터](../../../index.md) 를 방문 하 여 다른 ASP.NET mvc 자습서 및 샘플을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc1c-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="dfc1c-109">이 섹션에서는 새 Moviescontroller.cs 클래스를 만들고, 영화 데이터를 검색 하는 코드를 작성 하 고, 뷰 템플릿을 사용 하 여 브라우저에 다시 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc1c-109">In this section we are going to create a new MoviesController class, and write some code that retrieves our Movie data and displays it back to the browser using a View template.</span></span>

<span data-ttu-id="dfc1c-110">Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 새 Moviescontroller.cs을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dfc1c-110">Right click on the Controllers folder and make a new MoviesController.</span></span>

<span data-ttu-id="dfc1c-111">[컨트롤러 추가 ![](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="dfc1c-111">[![Add Controller](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)</span></span>

<span data-ttu-id="dfc1c-112">이렇게 하면 프로젝트 내의 \Controllers 폴더 아래에 새 "MoviesController.cs" 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="dfc1c-112">This will create a new "MoviesController.cs" file underneath our \Controllers folder within our project.</span></span> <span data-ttu-id="dfc1c-113">MovieController를 업데이트 하 여 새로 채워진 데이터베이스에서 동영상 목록을 검색 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc1c-113">Let's update the MovieController to retrieve the list of movies from our newly populated database.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part5/samples/sample1.cs)]

<span data-ttu-id="dfc1c-114">1984의 여름 이후에 릴리스된 영화만 검색 하도록 LINQ 쿼리를 수행 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc1c-114">We are performing a LINQ query so that we only retrieve movies released after the summer of 1984.</span></span> <span data-ttu-id="dfc1c-115">이 동영상 목록을 다시 렌더링 하려면 뷰 템플릿이 필요 하므로 메서드를 마우스 오른쪽 단추로 클릭 하 고 보기 추가를 선택 하 여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dfc1c-115">We'll need a View template to render this list of movies back, so right-click in the method and select Add View to create it.</span></span>

<span data-ttu-id="dfc1c-116">보기 추가 대화 상자 내에서 보기 템플릿에&gt;&lt;목록을 전달 하 고 있는지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc1c-116">Within the Add View dialog we'll indicate that we are passing a List&lt;Movies.Models.Movie&gt; to our View template.</span></span> <span data-ttu-id="dfc1c-117">보기 추가 대화 상자를 사용 하 여 "빈" 템플릿을 만들도록 선택한 이전 시간과 달리 이번에는 Visual Studio에서 일부 기본 콘텐츠를 사용 하 여 보기 템플릿을 자동으로 "스 캐 폴드" 하는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc1c-117">Unlike the previous times we used the Add View dialog and chose to create an "Empty" template, this time we'll indicate that we want Visual Studio to automatically "scaffold" a view template for us with some default content.</span></span> <span data-ttu-id="dfc1c-118">"콘텐츠 보기 드롭다운 메뉴에서" 목록 "항목을 선택 하 여이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc1c-118">We'll do this by selecting the "List" item within the "View content dropdown menu.</span></span>

<span data-ttu-id="dfc1c-119">새 클래스를 만든 경우 보기 추가 대화 상자에 표시 되도록 응용 프로그램을 컴파일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc1c-119">Remember, when you have a created a new class you'll need to compile your application for it to show up in the Add View Dialog.</span></span>

![뷰 추가](getting-started-with-mvc-part5/_static/image3.png)

<span data-ttu-id="dfc1c-121">추가를 클릭 하면 시스템에서 영화 목록을 표시 하는 보기에 대 한 코드를 자동으로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc1c-121">Click add and the system will automatically generate the code for a View for us that displays our list of movies.</span></span> <span data-ttu-id="dfc1c-122">이전에 Hello World 보기를 사용 했을 때와 같이 &lt;h2&gt; 제목을 "내 동영상 목록"과 같이 변경 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc1c-122">This is a good time to change the &lt;h2&gt; heading to something like "My Movie List" like we did earlier with the Hello World view.</span></span>

<span data-ttu-id="dfc1c-123">[![영화-Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="dfc1c-123">[![Movies - Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)</span></span>

<span data-ttu-id="dfc1c-124">응용 프로그램을 실행 하 고 주소 표시줄에서/영화를 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc1c-124">Run your application and visit /Movies in the address bar.</span></span> <span data-ttu-id="dfc1c-125">이제 컨트롤러 내부의 기본 쿼리를 사용 하 여 데이터베이스에서 데이터를 검색 하 고 영화에 대해 알고 있는 뷰로 데이터를 반환 했습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc1c-125">Now we've retrieved data from the database using a basic query inside the Controller and returned the data to a View that knows about Movies.</span></span> <span data-ttu-id="dfc1c-126">그런 다음이 뷰는 동영상 목록을 회전 하 고 데이터 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dfc1c-126">That View then spins through the list of Movies and creates a table of data for us.</span></span>

<span data-ttu-id="dfc1c-127">[![동영상 목록-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="dfc1c-127">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)</span></span>

<span data-ttu-id="dfc1c-128">이 응용 프로그램을 사용 하 여 편집, 세부 정보 및 삭제 기능을 구현 하지 않으므로 스 캐 폴드 템플릿이 생성 하는 기본 링크가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc1c-128">We won't be implementing Edit, Details and Delete functionality with this application - so we don't need the default links that the scaffold template created for us.</span></span> <span data-ttu-id="dfc1c-129">/Movies/Index.aspx 파일을 열고 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc1c-129">Open up the /Movies/Index.aspx file and remove them.</span></span>

<span data-ttu-id="dfc1c-130">다음은 이러한 변경을 수행한 후에 업데이트 된 뷰 템플릿이 표시 되는 대상에 대 한 소스 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="dfc1c-130">Here is the source code for what our updated View template should look like once we make these changes:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part5/samples/sample2.aspx)]

<span data-ttu-id="dfc1c-131">필요 하지 않은 링크를 만들기 때문에이 예제에 대 한 링크를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc1c-131">It's creating links that we won't need, so we'll delete them for this example.</span></span> <span data-ttu-id="dfc1c-132">새 링크 만들기는 다음 단계와 같이 계속 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfc1c-132">We will keep our Create New link though, as that's next!</span></span> <span data-ttu-id="dfc1c-133">해당 열이 제거 되 면 앱의 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc1c-133">Here's what our app looks like with that column removed.</span></span>

<span data-ttu-id="dfc1c-134">[![동영상 목록-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="dfc1c-134">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)</span></span>

<span data-ttu-id="dfc1c-135">이제 영화 데이터를 간단히 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc1c-135">We now have a simple listing of our movie data.</span></span> <span data-ttu-id="dfc1c-136">그러나 "새로 만들기" 링크를 클릭 하면 후크 되지 않으므로 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc1c-136">However, if we click the "Create New" link, we'll get an error as it's not hooked up!</span></span> <span data-ttu-id="dfc1c-137">Create Action 메서드를 구현 하 고 사용자가 데이터베이스에 새 영화를 입력할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc1c-137">Let's implement a Create Action method and enable a user to enter new movies in our database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="dfc1c-138">[이전](getting-started-with-mvc-part4.md)
> [다음](getting-started-with-mvc-part6.md)</span><span class="sxs-lookup"><span data-stu-id="dfc1c-138">[Previous](getting-started-with-mvc-part4.md)
[Next](getting-started-with-mvc-part6.md)</span></span>
