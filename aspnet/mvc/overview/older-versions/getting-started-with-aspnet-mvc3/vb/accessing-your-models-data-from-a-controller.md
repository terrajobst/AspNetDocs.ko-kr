---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/accessing-your-models-data-from-a-controller
title: 컨트롤러에서 모델의 데이터에 액세스 (VB) | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1 (...)을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 학습 합니다.
ms.author: riande
ms.date: 01/12/2011
ms.assetid: cad00de1-3c68-4ff4-a436-54236d449459
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 37f45d8f12e3ab5c485718bcf2c59934ad272118
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457991"
---
# <a name="accessing-your-models-data-from-a-controller-vb"></a><span data-ttu-id="35eec-103">컨트롤러에서 모델의 데이터에 액세스(VB)</span><span class="sxs-lookup"><span data-stu-id="35eec-103">Accessing your Model's Data from a Controller (VB)</span></span>

<span data-ttu-id="35eec-104">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="35eec-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="35eec-105">이 자습서에서는 Microsoft Visual Studio의 무료 버전인 Microsoft Visual Web Developer 2010 Express 서비스 팩 1을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="35eec-106">시작 하기 전에 아래 나열 된 필수 구성 요소를 설치 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="35eec-107">[웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)링크를 클릭 하 여 모든 항목을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="35eec-108">또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="35eec-109">Visual Studio Web Developer Express SP1 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="35eec-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="35eec-110">ASP.NET MVC 3 도구 업데이트</span><span class="sxs-lookup"><span data-stu-id="35eec-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="35eec-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)</span><span class="sxs-lookup"><span data-stu-id="35eec-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="35eec-112">Visual Web Developer 2010 대신 Visual Studio 2010을 사용 하는 경우 [Visual studio 2010 필수 조건](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)링크를 클릭 하 여 필수 구성 요소를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="35eec-113">VB.NET 소스 코드를 사용 하는 Visual Web Developer 프로젝트를이 항목과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="35eec-114">[VB.NET 버전을 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="35eec-115">선호 C#하는 경우이 자습서의 [ C# 버전](../cs/accessing-your-models-data-from-a-controller.md) 으로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-115">If you prefer C#, switch to the [C# version](../cs/accessing-your-models-data-from-a-controller.md) of this tutorial.</span></span>

<span data-ttu-id="35eec-116">이 섹션에서는 새 `MoviesController` 클래스를 만들고 영화 데이터를 검색 하 고 보기 템플릿을 사용 하 여 브라우저에 표시 하는 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-116">In this section, you'll create a new `MoviesController` class and write code that retrieves the movie data and displays it in the browser using a view template.</span></span> <span data-ttu-id="35eec-117">계속 하기 전에 응용 프로그램을 빌드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-117">Be sure to build your application before proceeding.</span></span>

<span data-ttu-id="35eec-118">*Controllers* 폴더를 마우스 오른쪽 단추로 클릭 하 고 새 `MoviesController` 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-118">Right-click the *Controllers* folder and create a new `MoviesController` controller.</span></span> <span data-ttu-id="35eec-119">다음 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-119">Select the following options:</span></span>

- <span data-ttu-id="35eec-120">컨트롤러 이름: **moviescontroller.cs**.</span><span class="sxs-lookup"><span data-stu-id="35eec-120">Controller name: **MoviesController**.</span></span> <span data-ttu-id="35eec-121">이것이 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-121">(This is the default.)</span></span>
- <span data-ttu-id="35eec-122">Template: **Entity Framework을 사용 하 여 읽기/쓰기 동작 및 뷰가 포함 된 컨트롤러**입니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-122">Template: **Controller with read/write actions and views, using Entity Framework**.</span></span>
- <span data-ttu-id="35eec-123">모델 클래스: **movie (MvcMovie. 모델)** .</span><span class="sxs-lookup"><span data-stu-id="35eec-123">Model class: **Movie (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="35eec-124">데이터 컨텍스트 클래스: **MovieDBContext (MvcMovie. 모델)** .</span><span class="sxs-lookup"><span data-stu-id="35eec-124">Data context class: **MovieDBContext (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="35eec-125">뷰: **Razor (CSHTML)** .</span><span class="sxs-lookup"><span data-stu-id="35eec-125">Views: **Razor (CSHTML)**.</span></span> <span data-ttu-id="35eec-126">기본값은입니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-126">(The default.)</span></span>

<span data-ttu-id="35eec-127">[![5addMovieController](accessing-your-models-data-from-a-controller/_static/image2.png)](accessing-your-models-data-from-a-controller/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="35eec-127">[![5addMovieController](accessing-your-models-data-from-a-controller/_static/image2.png)](accessing-your-models-data-from-a-controller/_static/image1.png)</span></span>

<span data-ttu-id="35eec-128">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-128">Click **Add**.</span></span> <span data-ttu-id="35eec-129">Visual Web Developer는 다음과 같은 파일 및 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-129">Visual Web Developer creates the following files and folders:</span></span>

- <span data-ttu-id="35eec-130">프로젝트의 *Controllers* 폴더에 있는 *moviescontroller.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-130">*A MoviesController.vb* file in the project's *Controllers* folder.</span></span>
- <span data-ttu-id="35eec-131">프로젝트의 *Views* 폴더에 있는 *동영상* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-131">A *Movies* folder in the project's *Views* folder.</span></span>
- <span data-ttu-id="35eec-132">새 Views\Movies 폴더에서 *. vbhtml, Delete*. Vbhtml, Details, 및 *인덱스* 를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-132">*Create.vbhtml, Delete.vbhtml, Details.vbhtml, Edit.vbhtml*, and *Index.vbhtml* in the new *Views\Movies* folder.</span></span>

<span data-ttu-id="35eec-133">[![5_ScaffoldMovie](accessing-your-models-data-from-a-controller/_static/image4.png)](accessing-your-models-data-from-a-controller/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="35eec-133">[![5_ScaffoldMovie](accessing-your-models-data-from-a-controller/_static/image4.png)](accessing-your-models-data-from-a-controller/_static/image3.png)</span></span>

<span data-ttu-id="35eec-134">ASP.NET MVC 3 스 캐 폴딩 메커니즘은 자동으로 CRUD (만들기, 읽기, 업데이트 및 삭제) 작업 메서드와 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-134">The ASP.NET MVC 3 scaffolding mechanism automatically created the CRUD (create, read, update, and delete) action methods and views for you.</span></span> <span data-ttu-id="35eec-135">이제 동영상 항목을 만들고, 나열 하 고, 편집 하 고, 삭제할 수 있는 완전히 작동 하는 웹 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-135">You now have a fully functional web application that lets you create, list, edit, and delete movie entries.</span></span>

<span data-ttu-id="35eec-136">응용 프로그램을 실행 하 고 브라우저의 주소 표시줄에 있는 URL에 */sourcea* 를 추가 하 여 `Movies` 컨트롤러를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-136">Run the application and browse to the `Movies` controller by appending */Movies* to the URL in the address bar of your browser.</span></span> <span data-ttu-id="35eec-137">응용 프로그램이 *global.asax* 파일에 정의 된 기본 라우팅에 의존 하기 때문에 브라우저 요청 `http://localhost:xxxxx/Movies`는 `Movies` 컨트롤러의 기본 `Index` 작업 메서드로 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-137">Because the application is relying on the default routing (defined in the *Global.asax* file), the browser request `http://localhost:xxxxx/Movies` is routed to the default `Index` action method of the `Movies` controller.</span></span> <span data-ttu-id="35eec-138">즉, 브라우저 요청 `http://localhost:xxxxx/Movies`는 실제로 브라우저 요청 `http://localhost:xxxxx/Movies/Index`와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-138">In other words, the browser request `http://localhost:xxxxx/Movies` is effectively the same as the browser request `http://localhost:xxxxx/Movies/Index`.</span></span> <span data-ttu-id="35eec-139">아직 추가 하지 않았기 때문에 빈 영화 목록이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-139">The result is an empty list of movies, because you haven't added any yet.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image5.png)

## <a name="creating-a-movie"></a><span data-ttu-id="35eec-140">동영상 만들기</span><span class="sxs-lookup"><span data-stu-id="35eec-140">Creating a Movie</span></span>

<span data-ttu-id="35eec-141">**새로 만들기** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-141">Select the **Create New** link.</span></span> <span data-ttu-id="35eec-142">동영상에 대 한 세부 정보를 입력 한 다음 **만들기** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-142">Enter some details about a movie and then click the **Create** button.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image6.png)

<span data-ttu-id="35eec-143">[ **만들기** ] 단추를 클릭 하면 양식이 서버에 게시 되 고,이 경우 동영상 정보가 데이터베이스에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-143">Clicking the **Create** button causes the form to be posted to the server, where the movie information is saved in the database.</span></span> <span data-ttu-id="35eec-144">그런 다음 목록에서 새로 만든 동영상을 볼 수 있는 */Clurl* 로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-144">You're then redirected to the */Movies* URL, where you can see the newly created movie in the listing.</span></span>

<span data-ttu-id="35eec-145">[![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image8.png)](accessing-your-models-data-from-a-controller/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="35eec-145">[![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image8.png)](accessing-your-models-data-from-a-controller/_static/image7.png)</span></span>

<span data-ttu-id="35eec-146">나머지 몇 개의 동영상 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-146">Create a couple more movie entries.</span></span> <span data-ttu-id="35eec-147">모두 작동하는 **편집**, **세부 정보** 및 **삭제** 링크를 사용해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-147">Try the **Edit**, **Details**, and **Delete** links, which are all functional.</span></span>

## <a name="examining-the-generated-code"></a><span data-ttu-id="35eec-148">생성 된 코드 검사</span><span class="sxs-lookup"><span data-stu-id="35eec-148">Examining the Generated Code</span></span>

<span data-ttu-id="35eec-149">*Controllers\MoviesController.vb* 파일을 열고 생성 된 `Index` 메서드를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-149">Open the *Controllers\MoviesController.vb* file and examine the generated `Index` method.</span></span> <span data-ttu-id="35eec-150">`Index` 메서드를 사용 하는 동영상 컨트롤러의 일부는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-150">A portion of the movie controller with the `Index` method is shown below.</span></span>

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample1.vb)]

<span data-ttu-id="35eec-151">`MoviesController` 클래스의 다음 줄은 앞에서 설명한 대로 영화 데이터베이스 컨텍스트를 인스턴스화합니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-151">The following line from the `MoviesController` class instantiates a movie database context, as described previously.</span></span> <span data-ttu-id="35eec-152">동영상 데이터베이스 컨텍스트를 사용 하 여 영화를 쿼리, 편집 및 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-152">You can use the movie database context to query, edit, and delete movies.</span></span>

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample2.vb)]

<span data-ttu-id="35eec-153">`Movies` 컨트롤러에 대 한 요청은 movie 데이터베이스의 `Movies` 테이블에 있는 모든 항목을 반환한 다음 결과를 `Index` 보기에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-153">A request to the `Movies` controller returns all the entries in the `Movies` table of the movie database and then passes the results to the `Index` view.</span></span>

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="35eec-154">강력한 형식의 모델 및 @model 키워드</span><span class="sxs-lookup"><span data-stu-id="35eec-154">Strongly Typed Models and the @model Keyword</span></span>

<span data-ttu-id="35eec-155">이 자습서의 앞부분에서 컨트롤러가 `ViewBag` 개체를 사용 하 여 데이터 또는 개체를 뷰 템플릿에 전달 하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-155">Earlier in this tutorial, you saw how a controller can pass data or objects to a view template using the `ViewBag` object.</span></span> <span data-ttu-id="35eec-156">`ViewBag`은 뷰에 정보를 전달 하는 데 편리한 런타임에 바인딩되는 방법을 제공 하는 동적 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-156">The `ViewBag` is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="35eec-157">ASP.NET MVC는 또한 강력한 형식의 데이터 또는 개체를 뷰 템플릿에 전달 하는 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-157">ASP.NET MVC also provides the ability to pass strongly typed data or objects to a view template.</span></span> <span data-ttu-id="35eec-158">강력 하 게 형식화 된이 접근 방식을 사용 하면 Visual Web Developer 편집기에서 코드 및 더 다양 한 IntelliSense의 컴파일 시간 검사를 더 효율적으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-158">This strongly typed approach enables better compile-time checking of your code and richer IntelliSense in the Visual Web Developer editor.</span></span> <span data-ttu-id="35eec-159">`MoviesController` 클래스 및 인덱스를 사용 하 여이 방법을 사용 하 고 있습니다 *.*</span><span class="sxs-lookup"><span data-stu-id="35eec-159">We're using this approach with the `MoviesController` class and *Index.vbhtml* view template.</span></span>

<span data-ttu-id="35eec-160">코드는 `Index` 동작 메서드에서 `View` 도우미 메서드를 호출할 때 [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) 개체를 만드는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-160">Notice how the code creates a [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) object when it calls the `View` helper method in the `Index` action method.</span></span> <span data-ttu-id="35eec-161">그런 다음 코드는 컨트롤러에서 뷰로이 `Movies` 목록을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-161">The code then passes this `Movies` list from the controller to the view:</span></span>

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample3.vb)]

<span data-ttu-id="35eec-162">뷰 템플릿 파일의 맨 위에 `@ModelType` 문을 포함 하 여 뷰에 필요한 개체 유형을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-162">By including a `@ModelType` statement at the top of the view template file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="35eec-163">동영상 컨트롤러를 만들 때 Visual Web Developer는 인덱스의 맨 위에 다음 `@model` 문을 자동으로 포함 합니다 *. vbhtml* 파일:</span><span class="sxs-lookup"><span data-stu-id="35eec-163">When you created the movie controller, Visual Web Developer automatically included the following `@model` statement at the top of the *Index.vbhtml* file:</span></span>

[!code-vbhtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.vbhtml)]

<span data-ttu-id="35eec-164">이 `@ModelType` 지시어를 사용 하면 강력한 형식의 `Model` 개체를 사용 하 여 컨트롤러에서 뷰에 전달 된 동영상 목록에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-164">This `@ModelType` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="35eec-165">예를 들어, *Index. vbhtml* 템플릿에서 코드는 강력한 형식의 `Model` 개체에 대해 `foreach` 문을 수행 하 여 동영상을 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-165">For example, in the *Index.vbhtml* template, the code loops through the movies by doing a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-vbhtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.vbhtml)]

<span data-ttu-id="35eec-166">`Model` 개체는 강력 하 게 형식화 되어 있기 때문에 (`IEnumerable<Movie>` 개체로) 루프의 각 `item` 개체는 `Movie`로 형식화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-166">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each `item` object in the loop is typed as `Movie`.</span></span> <span data-ttu-id="35eec-167">다른 이점 중 하나는 코드 편집기에서 코드 및 전체 IntelliSense 지원에 대 한 컴파일 시간 검사를 가져오는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-167">Among other benefits, this means that you get compile-time checking of the code and full IntelliSense support in the code editor:</span></span>

<span data-ttu-id="35eec-168">[![5_Intellisense](accessing-your-models-data-from-a-controller/_static/image10.png)](accessing-your-models-data-from-a-controller/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="35eec-168">[![5_Intellisense](accessing-your-models-data-from-a-controller/_static/image10.png)](accessing-your-models-data-from-a-controller/_static/image9.png)</span></span>

## <a name="working-with-sql-server-compact"></a><span data-ttu-id="35eec-169">SQL Server Compact 사용</span><span class="sxs-lookup"><span data-stu-id="35eec-169">Working with SQL Server Compact</span></span>

<span data-ttu-id="35eec-170">Entity Framework Code First 제공 된 데이터베이스 연결 문자열이 아직 존재 하지 않은 `Movies` 데이터베이스를 가리키고 있으므로 데이터베이스를 자동으로 만들 Code First.</span><span class="sxs-lookup"><span data-stu-id="35eec-170">Entity Framework Code First detected that the database connection string that was provided pointed to a `Movies` database that didn't exist yet, so Code First created the database automatically.</span></span> <span data-ttu-id="35eec-171">*앱\_데이터* 폴더를 확인 하 여 만들어졌는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-171">You can verify that it's been created by looking in the *App\_Data* folder.</span></span> <span data-ttu-id="35eec-172">*영화 .sdf* 파일이 표시 되지 않으면 **솔루션 탐색기** 도구 모음에서 **모든 파일 표시** 단추를 클릭 하 고 **새로 고침** 단추를 클릭 한 다음 *응용 프로그램\_데이터* 폴더를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-172">If you don't see the *Movies.sdf* file, click the **Show All Files** button in the **Solution Explorer** toolbar, click the **Refresh** button, and then expand the *App\_Data* folder.</span></span>

<span data-ttu-id="35eec-173">[![SDF_in_SolnExp](accessing-your-models-data-from-a-controller/_static/image12.png)](accessing-your-models-data-from-a-controller/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="35eec-173">[![SDF_in_SolnExp](accessing-your-models-data-from-a-controller/_static/image12.png)](accessing-your-models-data-from-a-controller/_static/image11.png)</span></span>

<span data-ttu-id="35eec-174">*영화 .sdf* 를 두 번 클릭 하 여 **서버 탐색기**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-174">Double-click *Movies.sdf* to open **Server Explorer**.</span></span> <span data-ttu-id="35eec-175">그런 다음 **테이블** 폴더를 확장 하 여 데이터베이스에서 만든 테이블을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-175">Then expand the **Tables** folder to see the tables that have been created in the database.</span></span>

> [!NOTE]
> <span data-ttu-id="35eec-176">*영화 .sdf*를 두 번 클릭할 때 오류가 발생 하면 **SQL Server Compact 4.0 용 VISUAL Studio 2010 SP1 도구**를 설치 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-176">If you get an error when you double-click *Movies.sdf*, make sure you've installed **Visual Studio 2010 SP1 Tools for SQL Server Compact 4.0**.</span></span> <span data-ttu-id="35eec-177">소프트웨어에 대 한 링크는이 자습서 시리즈의 1 부에서 전제 조건 목록을 참조 하세요. 지금 릴리스를 설치 하는 경우에는 Visual Web Developer를 닫았다가 다시 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-177">(For links to the software, see the list of prerequisites in part 1 of this tutorial series.) If you install the release now, you'll have to close and re-open Visual Web Developer.</span></span>

<span data-ttu-id="35eec-178">[![DB_explorer](accessing-your-models-data-from-a-controller/_static/image14.png)](accessing-your-models-data-from-a-controller/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="35eec-178">[![DB_explorer](accessing-your-models-data-from-a-controller/_static/image14.png)](accessing-your-models-data-from-a-controller/_static/image13.png)</span></span>

<span data-ttu-id="35eec-179">두 테이블은 `Movie` 엔터티 집합에 대 한 테이블과 `EdmMetadata` 테이블에 하나씩 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-179">There are two tables, one for the `Movie` entity set and then the `EdmMetadata` table.</span></span> <span data-ttu-id="35eec-180">`EdmMetadata` 테이블은 Entity Framework에서 모델과 데이터베이스가 동기화 되지 않은 시기를 확인 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-180">The `EdmMetadata` table is used by the Entity Framework to determine when the model and the database are out of sync.</span></span>

<span data-ttu-id="35eec-181">`Movies` 테이블을 마우스 오른쪽 단추로 클릭 하 고 **테이블 데이터 표시** 를 선택 하 여 만든 데이터를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-181">Right-click the `Movies` table and select **Show Table Data** to see the data you created.</span></span>

<span data-ttu-id="35eec-182">[![MoviesTable](accessing-your-models-data-from-a-controller/_static/image16.png)](accessing-your-models-data-from-a-controller/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="35eec-182">[![MoviesTable](accessing-your-models-data-from-a-controller/_static/image16.png)](accessing-your-models-data-from-a-controller/_static/image15.png)</span></span>

<span data-ttu-id="35eec-183">`Movies` 테이블을 마우스 오른쪽 단추로 클릭 하 고 **테이블 스키마 편집**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-183">Right-click the `Movies` table and select **Edit Table Schema**.</span></span>

<span data-ttu-id="35eec-184">[![EditTableSchema](accessing-your-models-data-from-a-controller/_static/image18.png)](accessing-your-models-data-from-a-controller/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="35eec-184">[![EditTableSchema](accessing-your-models-data-from-a-controller/_static/image18.png)](accessing-your-models-data-from-a-controller/_static/image17.png)</span></span>

![TableSchemaSM](accessing-your-models-data-from-a-controller/_static/image19.png)

<span data-ttu-id="35eec-186">`Movies` 테이블의 스키마가 이전에 만든 `Movie` 클래스에 매핑되는 방식을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-186">Notice how the schema of the `Movies` table maps to the `Movie` class you created earlier.</span></span> <span data-ttu-id="35eec-187">Entity Framework Code First `Movie` 클래스에 따라이 스키마를 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-187">Entity Framework Code First automatically created this schema for you based on your `Movie` class.</span></span>

<span data-ttu-id="35eec-188">완료 되 면 연결을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-188">When you're finished, close the connection.</span></span> <span data-ttu-id="35eec-189">연결을 닫지 않은 경우 다음에 프로젝트를 실행할 때 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-189">(If you don't close the connection, you might get an error the next time you run the project).</span></span>

<span data-ttu-id="35eec-190">[![CloseConnection](accessing-your-models-data-from-a-controller/_static/image21.png)](accessing-your-models-data-from-a-controller/_static/image20.png)</span><span class="sxs-lookup"><span data-stu-id="35eec-190">[![CloseConnection](accessing-your-models-data-from-a-controller/_static/image21.png)](accessing-your-models-data-from-a-controller/_static/image20.png)</span></span>

<span data-ttu-id="35eec-191">이제 데이터베이스 및 간단한 목록 페이지에서 콘텐츠를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-191">You now have the database and a simple listing page to display content from it.</span></span> <span data-ttu-id="35eec-192">다음 자습서에서는 스 캐 폴드 코드의 나머지 부분을 검토 하 고이 데이터베이스에서 영화를 검색할 수 있도록 하는 `SearchIndex` 메서드 및 `SearchIndex` 뷰를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="35eec-192">In the next tutorial, we'll examine the rest of the scaffolded code and add a `SearchIndex` method and a `SearchIndex` view that lets you search for movies in this database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="35eec-193">[이전](adding-a-model.md)
> [다음](examining-the-edit-methods-and-edit-view.md)</span><span class="sxs-lookup"><span data-stu-id="35eec-193">[Previous](adding-a-model.md)
[Next](examining-the-edit-methods-and-edit-view.md)</span></span>
