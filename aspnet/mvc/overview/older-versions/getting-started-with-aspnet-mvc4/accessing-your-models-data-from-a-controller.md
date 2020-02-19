---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
title: 컨트롤러에서 모델의 데이터에 액세스 | Microsoft Docs
author: Rick-Anderson
description: 참고:이 자습서의 업데이트 된 버전은 ASP.NET MVC 5 및 Visual Studio 2013를 사용 하는 여기에서 사용할 수 있습니다. 보다 안전 하 고, 보다 간단 하 고 데모를 수행 하는 것이 더 간단 합니다.
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 61e0206d-7f32-4018-992d-0a51b48b37dc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 7c4aa34567ac4fb31d1ed874cf65986c4e779e66
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456168"
---
# <a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="bb371-104">컨트롤러에서 모델의 데이터에 액세스</span><span class="sxs-lookup"><span data-stu-id="bb371-104">Accessing Your Model's Data from a Controller</span></span>

<span data-ttu-id="bb371-105">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="bb371-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="bb371-106">ASP.NET MVC 5와 Visual Studio 2013를 사용 하는이 자습서의 업데이트 된 버전 [을 사용할 수 있습니다.](../../getting-started/introduction/getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="bb371-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="bb371-107">더 안전 하 고 더 간단 하 고 더 많은 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="bb371-108">이 섹션에서는 새 `MoviesController` 클래스를 만들고 영화 데이터를 검색 하 고 보기 템플릿을 사용 하 여 브라우저에 표시 하는 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-108">In this section, you'll create a new `MoviesController` class and write code that retrieves the movie data and displays it in the browser using a view template.</span></span>

<span data-ttu-id="bb371-109">다음 단계로 이동 하기 전에 **응용 프로그램을 빌드합니다** .</span><span class="sxs-lookup"><span data-stu-id="bb371-109">**Build the application** before going on to the next step.</span></span>

<span data-ttu-id="bb371-110">*Controllers* 폴더를 마우스 오른쪽 단추로 클릭 하 고 새 `MoviesController` 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-110">Right-click the *Controllers* folder and create a new `MoviesController` controller.</span></span> <span data-ttu-id="bb371-111">아래 옵션은 응용 프로그램을 빌드할 때까지 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-111">The options below will not appear until you build your application.</span></span> <span data-ttu-id="bb371-112">다음 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-112">Select the following options:</span></span>

- <span data-ttu-id="bb371-113">컨트롤러 이름: **moviescontroller.cs**.</span><span class="sxs-lookup"><span data-stu-id="bb371-113">Controller name: **MoviesController**.</span></span> <span data-ttu-id="bb371-114">이것이 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-114">(This is the default.</span></span> <span data-ttu-id="bb371-115">)</span><span class="sxs-lookup"><span data-stu-id="bb371-115">)</span></span>
- <span data-ttu-id="bb371-116">Template: **Entity Framework을 사용 하 여 읽기/쓰기 동작 및 뷰가 포함 된 MVC 컨트롤러**입니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-116">Template: **MVC Controller with read/write actions and views, using Entity Framework**.</span></span>
- <span data-ttu-id="bb371-117">모델 클래스: **movie (MvcMovie. 모델)** .</span><span class="sxs-lookup"><span data-stu-id="bb371-117">Model class: **Movie (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="bb371-118">데이터 컨텍스트 클래스: **MovieDBContext (MvcMovie. 모델)** .</span><span class="sxs-lookup"><span data-stu-id="bb371-118">Data context class: **MovieDBContext (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="bb371-119">뷰: **Razor (CSHTML)** .</span><span class="sxs-lookup"><span data-stu-id="bb371-119">Views: **Razor (CSHTML)**.</span></span> <span data-ttu-id="bb371-120">기본값은입니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-120">(The default.)</span></span>

![AddScaffoldedMovieController](accessing-your-models-data-from-a-controller/_static/image1.png)

<span data-ttu-id="bb371-122">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-122">Click **Add**.</span></span> <span data-ttu-id="bb371-123">Visual Studio Express 다음과 같은 파일 및 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-123">Visual Studio Express creates the following files and folders:</span></span>

- <span data-ttu-id="bb371-124">프로젝트의 *Controllers* 폴더에 있는 *MoviesController.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-124">*A MoviesController.cs* file in the project's *Controllers* folder.</span></span>
- <span data-ttu-id="bb371-125">프로젝트의 *Views* 폴더에 있는 *동영상* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-125">A *Movies* folder in the project's *Views* folder.</span></span>
- <span data-ttu-id="bb371-126">새 *Views\Movies* 폴더에서 *. cshtml, Delete cshtml, Details, Edit. cshtml*및 *인덱스* 를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-126">*Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml*, and *Index.cshtml* in the new *Views\Movies* folder.</span></span>

<span data-ttu-id="bb371-127">ASP.NET MVC 4는 자동으로 CRUD (만들기, 읽기, 업데이트 및 삭제) 작업 메서드와 뷰를 만듭니다. CRUD 작업 메서드 및 보기의 자동 생성을 스 캐 폴딩 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-127">ASP.NET MVC 4 automatically created the CRUD (create, read, update, and delete) action methods and views for you (the automatic creation of CRUD action methods and views is known as scaffolding).</span></span> <span data-ttu-id="bb371-128">이제 동영상 항목을 만들고, 나열 하 고, 편집 하 고, 삭제할 수 있는 완전히 작동 하는 웹 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-128">You now have a fully functional web application that lets you create, list, edit, and delete movie entries.</span></span>

<span data-ttu-id="bb371-129">응용 프로그램을 실행 하 고 브라우저의 주소 표시줄에 있는 URL에 */sourcea* 를 추가 하 여 `Movies` 컨트롤러를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-129">Run the application and browse to the `Movies` controller by appending */Movies* to the URL in the address bar of your browser.</span></span> <span data-ttu-id="bb371-130">응용 프로그램이 *global.asax* 파일에 정의 된 기본 라우팅에 의존 하기 때문에 브라우저 요청 `http://localhost:xxxxx/Movies`는 `Movies` 컨트롤러의 기본 `Index` 작업 메서드로 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-130">Because the application is relying on the default routing (defined in the *Global.asax* file), the browser request `http://localhost:xxxxx/Movies` is routed to the default `Index` action method of the `Movies` controller.</span></span> <span data-ttu-id="bb371-131">즉, 브라우저 요청 `http://localhost:xxxxx/Movies`는 실제로 브라우저 요청 `http://localhost:xxxxx/Movies/Index`와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-131">In other words, the browser request `http://localhost:xxxxx/Movies` is effectively the same as the browser request `http://localhost:xxxxx/Movies/Index`.</span></span> <span data-ttu-id="bb371-132">아직 추가 하지 않았기 때문에 빈 영화 목록이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-132">The result is an empty list of movies, because you haven't added any yet.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image2.png)

### <a name="creating-a-movie"></a><span data-ttu-id="bb371-133">동영상 만들기</span><span class="sxs-lookup"><span data-stu-id="bb371-133">Creating a Movie</span></span>

<span data-ttu-id="bb371-134">**새로 만들기** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-134">Select the **Create New** link.</span></span> <span data-ttu-id="bb371-135">동영상에 대 한 세부 정보를 입력 한 다음 **만들기** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-135">Enter some details about a movie and then click the **Create** button.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image3.png)

<span data-ttu-id="bb371-136">[ **만들기** ] 단추를 클릭 하면 양식이 서버에 게시 되 고,이 경우 동영상 정보가 데이터베이스에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-136">Clicking the **Create** button causes the form to be posted to the server, where the movie information is saved in the database.</span></span> <span data-ttu-id="bb371-137">그런 다음 목록에서 새로 만든 동영상을 볼 수 있는 */Clurl* 로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-137">You're then redirected to the */Movies* URL, where you can see the newly created movie in the listing.</span></span>

<span data-ttu-id="bb371-138">![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image4.png "IndexWhenHarryMet")</span><span class="sxs-lookup"><span data-stu-id="bb371-138">![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image4.png "IndexWhenHarryMet")</span></span>

<span data-ttu-id="bb371-139">나머지 몇 개의 동영상 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-139">Create a couple more movie entries.</span></span> <span data-ttu-id="bb371-140">모두 작동하는 **편집**, **세부 정보** 및 **삭제** 링크를 사용해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-140">Try the **Edit**, **Details**, and **Delete** links, which are all functional.</span></span>

## <a name="examining-the-generated-code"></a><span data-ttu-id="bb371-141">생성 된 코드 검사</span><span class="sxs-lookup"><span data-stu-id="bb371-141">Examining the Generated Code</span></span>

<span data-ttu-id="bb371-142">*Controllers\MoviesController.cs* 파일을 열고 생성 된 `Index` 메서드를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-142">Open the *Controllers\MoviesController.cs* file and examine the generated `Index` method.</span></span> <span data-ttu-id="bb371-143">`Index` 메서드를 사용 하는 동영상 컨트롤러의 일부는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-143">A portion of the movie controller with the `Index` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

<span data-ttu-id="bb371-144">`MoviesController` 클래스의 다음 줄은 앞에서 설명한 대로 영화 데이터베이스 컨텍스트를 인스턴스화합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-144">The following line from the `MoviesController` class instantiates a movie database context, as described previously.</span></span> <span data-ttu-id="bb371-145">동영상 데이터베이스 컨텍스트를 사용 하 여 영화를 쿼리, 편집 및 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-145">You can use the movie database context to query, edit, and delete movies.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

<span data-ttu-id="bb371-146">`Movies` 컨트롤러에 대 한 요청은 movie 데이터베이스의 `Movies` 테이블에 있는 모든 항목을 반환한 다음 결과를 `Index` 보기에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-146">A request to the `Movies` controller returns all the entries in the `Movies` table of the movie database and then passes the results to the `Index` view.</span></span>

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="bb371-147">강력한 형식의 모델 및 @model 키워드</span><span class="sxs-lookup"><span data-stu-id="bb371-147">Strongly Typed Models and the @model Keyword</span></span>

<span data-ttu-id="bb371-148">이 자습서의 앞부분에서 컨트롤러가 `ViewBag` 개체를 사용 하 여 데이터 또는 개체를 뷰 템플릿에 전달 하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-148">Earlier in this tutorial, you saw how a controller can pass data or objects to a view template using the `ViewBag` object.</span></span> <span data-ttu-id="bb371-149">`ViewBag`은 뷰에 정보를 전달 하는 데 편리한 런타임에 바인딩되는 방법을 제공 하는 동적 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-149">The `ViewBag` is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="bb371-150">ASP.NET MVC는 또한 강력한 형식의 데이터 또는 개체를 뷰 템플릿에 전달 하는 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-150">ASP.NET MVC also provides the ability to pass strongly typed data or objects to a view template.</span></span> <span data-ttu-id="bb371-151">강력 하 게 형식화 된이 방법은 Visual Studio 편집기에서 코드 및 더 다양 한 IntelliSense의 컴파일 시간 검사를 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-151">This strongly typed approach enables better compile-time checking of your code and richer IntelliSense in the Visual Studio editor.</span></span> <span data-ttu-id="bb371-152">Visual Studio에서 스 캐 폴딩 메커니즘은 메서드 및 뷰를 만들 때 `MoviesController` 클래스 및 뷰 템플릿을 사용 하 여이 방법을 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-152">The scaffolding mechanism in Visual Studio used this approach with the `MoviesController` class and view templates when it created the methods and views.</span></span>

<span data-ttu-id="bb371-153">*Controllers\MoviesController.cs* 파일에서 생성 된 `Details` 메서드를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-153">In the *Controllers\MoviesController.cs* file examine the generated `Details` method.</span></span> <span data-ttu-id="bb371-154">`Details` 메서드를 사용 하는 동영상 컨트롤러의 일부는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-154">A portion of the movie controller with the `Details` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs?highlight=3,8)]

<span data-ttu-id="bb371-155">`Movie` 발견 되 면 `Movie` 모델의 인스턴스가 자세히 보기로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-155">If a `Movie` is found, an instance of the `Movie` model is passed to the Details view.</span></span> <span data-ttu-id="bb371-156">*Views\Movies\Details.cshtml* 파일의 내용을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-156">Examine the contents of the *Views\Movies\Details.cshtml* file.</span></span>

<span data-ttu-id="bb371-157">뷰 템플릿 파일의 맨 위에 `@model` 문을 포함 하 여 뷰에 필요한 개체 유형을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-157">By including a `@model` statement at the top of the view template file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="bb371-158">영화 컨트롤러를 만들 때 Visual Studio에서는 `@model`Details.cshtml*파일의 맨 위에 다음* 문을 자동으로 포함했습니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-158">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.cshtml)]

<span data-ttu-id="bb371-159">이 `@model` 지시문을 사용하면 강력한 형식인 `Model` 개체를 사용하여 컨트롤러가 뷰에 전달된 영화에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-159">This `@model` directive allows you to access the movie that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="bb371-160">예를 들어, *Details* 템플릿에서는 코드는 각 동영상 필드를 `DisplayNameFor`에 전달 하 고 강력한 형식의 `Model` 개체를 사용 하 여 HTML 도우미 [에 대해 displayfor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-160">For example, in the *Details.cshtml* template, the code passes each movie field to the `DisplayNameFor` and [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML Helpers with the strongly typed `Model` object.</span></span> <span data-ttu-id="bb371-161">만들기 및 편집 메서드와 뷰 템플릿은 또한 영화 모델 개체를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-161">The Create and Edit methods and view templates also pass a movie model object.</span></span>

<span data-ttu-id="bb371-162">*MoviesController.cs* 파일에서 *Index. cshtml* 뷰 템플릿 및 `Index` 메서드를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-162">Examine the *Index.cshtml* view template and the `Index` method in the *MoviesController.cs* file.</span></span> <span data-ttu-id="bb371-163">코드는 `Index` 동작 메서드에서 `View` 도우미 메서드를 호출할 때 [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) 개체를 만드는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-163">Notice how the code creates a [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) object when it calls the `View` helper method in the `Index` action method.</span></span> <span data-ttu-id="bb371-164">그런 다음 코드는 컨트롤러에서 뷰로이 `Movies` 목록을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-164">The code then passes this `Movies` list from the controller to the view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample5.cs?highlight=3)]

<span data-ttu-id="bb371-165">동영상 컨트롤러를 만들 때 다음 `@model` 문이 *Index. cshtml* 파일의 맨 위에 자동으로 포함 Visual Studio Express.</span><span class="sxs-lookup"><span data-stu-id="bb371-165">When you created the movie controller, Visual Studio Express automatically included the following `@model` statement at the top of the *Index.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

<span data-ttu-id="bb371-166">이 `@model` 지시어를 사용 하면 강력한 형식의 `Model` 개체를 사용 하 여 컨트롤러에서 뷰에 전달 된 동영상 목록에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-166">This `@model` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="bb371-167">예를 들어, *인덱스인* 템플릿에서 코드는 강력한 형식의 `Model` 개체에 대해 `foreach` 문을 수행 하 여 동영상을 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-167">For example, in the *Index.cshtml* template, the code loops through the movies by doing a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample7.cshtml?highlight=1,4,7,10,13,16,19-21)]

<span data-ttu-id="bb371-168">`Model` 개체는 강력 하 게 형식화 되어 있기 때문에 (`IEnumerable<Movie>` 개체로) 루프의 각 `item` 개체는 `Movie`로 형식화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-168">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each `item` object in the loop is typed as `Movie`.</span></span> <span data-ttu-id="bb371-169">다른 이점 중 하나는 코드 편집기에서 코드 및 전체 IntelliSense 지원에 대 한 컴파일 시간 검사를 가져오는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-169">Among other benefits, this means that you get compile-time checking of the code and full IntelliSense support in the code editor:</span></span>

![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image5.png)

## <a name="working-with-sql-server-localdb"></a><span data-ttu-id="bb371-171">SQL Server LocalDB 사용</span><span class="sxs-lookup"><span data-stu-id="bb371-171">Working with SQL Server LocalDB</span></span>

<span data-ttu-id="bb371-172">Entity Framework Code First 제공 된 데이터베이스 연결 문자열이 아직 존재 하지 않은 `Movies` 데이터베이스를 가리키고 있으므로 데이터베이스를 자동으로 만들 Code First.</span><span class="sxs-lookup"><span data-stu-id="bb371-172">Entity Framework Code First detected that the database connection string that was provided pointed to a `Movies` database that didn't exist yet, so Code First created the database automatically.</span></span> <span data-ttu-id="bb371-173">*앱\_데이터* 폴더를 확인 하 여 만들어졌는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-173">You can verify that it's been created by looking in the *App\_Data* folder.</span></span> <span data-ttu-id="bb371-174">*영화 .mdf* 파일이 표시 되지 않으면 **솔루션 탐색기** 도구 모음에서 **모든 파일 표시** 단추를 클릭 하 고 **새로 고침** 단추를 클릭 한 다음 *앱\_데이터* 폴더를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-174">If you don't see the *Movies.mdf* file, click the **Show All Files** button in the **Solution Explorer** toolbar, click the **Refresh** button, and then expand the *App\_Data* folder.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image6.png)

<span data-ttu-id="bb371-175">*동영상과* 를 두 번 클릭 하 여 **데이터베이스 탐색기**를 열고 **Tables** 폴더를 확장 하 여 동영상 테이블을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-175">Double-click *Movies.mdf* to open **DATABASE EXPLORER**, then expand the **Tables** folder to see the Movies table.</span></span>

<span data-ttu-id="bb371-176">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image7.png "DB_explorer")</span><span class="sxs-lookup"><span data-stu-id="bb371-176">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image7.png "DB_explorer")</span></span>

> [!NOTE]
> <span data-ttu-id="bb371-177">데이터베이스 탐색기가 표시 되지 않으면 **도구** 메뉴에서 **데이터베이스에 연결**을 선택 하 고 **데이터 소스 선택** 대화 상자를 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-177">If the database explorer doesn't appear, from the **TOOLS** menu, select **Connect to Database**, then cancel the **Choose Data Source** dialog.</span></span> <span data-ttu-id="bb371-178">그러면 데이터베이스 탐색기가 강제로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-178">This will force open the database explorer.</span></span>

> [!NOTE]
> <span data-ttu-id="bb371-179">VWD 또는 Visual Studio 2010을 사용 하는 경우 다음 중 하 나와 유사한 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-179">If you are using VWD or Visual Studio 2010 and get an error similar to any of the following following:</span></span>
> 
> - <span data-ttu-id="bb371-180">데이터베이스 ' C:\Webs\MVC4\MVCMOVIE\MVCMOVIE\APP\_DATA\MOVIES. MDF는 버전 706 이므로 열 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-180">The database 'C:\Webs\MVC4\MVCMOVIE\MVCMOVIE\APP\_DATA\MOVIES.MDF' cannot be opened because it is version 706.</span></span> <span data-ttu-id="bb371-181">이 서버는 버전 655 및 이전 버전을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-181">This server supports version 655 and earlier.</span></span> <span data-ttu-id="bb371-182">다운그레이드는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-182">A downgrade path is not supported.</span></span>
> - <span data-ttu-id="bb371-183">제공 된 SqlConnection가 초기 카탈로그를 지정 하지 않고 &quot;InvalidOperation 예외가 사용자&quot; 코드에서 처리 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-183">&quot;InvalidOperation Exception was unhandled by user code&quot; The supplied SqlConnection does not specify an initial catalog.</span></span>
> 
> <span data-ttu-id="bb371-184">[SQL Server Data Tools](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx) 및 [LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0)를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-184">You need to install the [SQL Server Data Tools](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx) and [LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0).</span></span> <span data-ttu-id="bb371-185">이전 페이지에서 지정한 `MovieDBContext` 연결 문자열을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-185">Verify the `MovieDBContext` connection string specified on the previous page.</span></span>

<span data-ttu-id="bb371-186">`Movies` 테이블을 마우스 오른쪽 단추로 클릭 하 고 **테이블 데이터 표시** 를 선택 하 여 만든 데이터를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-186">Right-click the `Movies` table and select **Show Table Data** to see the data you created.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image8.png)

<span data-ttu-id="bb371-187">`Movies` 테이블을 마우스 오른쪽 단추로 클릭 하 고 **테이블 정의 열기** 를 선택 하 Entity Framework Code First 생성 된 테이블 구조를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-187">Right-click the `Movies` table and select **Open Table Definition** to see the table structure that Entity Framework Code First created for you.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image9.png "MoviesTable")

![](accessing-your-models-data-from-a-controller/_static/image10.png)

<span data-ttu-id="bb371-188">`Movies` 테이블의 스키마가 이전에 만든 `Movie` 클래스에 매핑되는 방식을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-188">Notice how the schema of the `Movies` table maps to the `Movie` class you created earlier.</span></span> <span data-ttu-id="bb371-189">Entity Framework Code First `Movie` 클래스에 따라이 스키마를 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-189">Entity Framework Code First automatically created this schema for you based on your `Movie` class.</span></span>

<span data-ttu-id="bb371-190">완료 되 면 *MovieDBContext* 를 마우스 오른쪽 단추로 클릭 하 고 **연결 닫기**를 선택 하 여 연결을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-190">When you're finished, close the connection by right clicking *MovieDBContext* and selecting **Close Connection**.</span></span> <span data-ttu-id="bb371-191">연결을 닫지 않은 경우 다음에 프로젝트를 실행할 때 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-191">(If you don't close the connection, you might get an error the next time you run the project).</span></span>

![](accessing-your-models-data-from-a-controller/_static/image11.png "CloseConnection")

<span data-ttu-id="bb371-192">이제 데이터베이스 및 간단한 목록 페이지에서 콘텐츠를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-192">You now have the database and a simple listing page to display content from it.</span></span> <span data-ttu-id="bb371-193">다음 자습서에서는 스 캐 폴드 코드의 나머지 부분을 검토 하 고이 데이터베이스에서 영화를 검색할 수 있도록 하는 `SearchIndex` 메서드 및 `SearchIndex` 뷰를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb371-193">In the next tutorial, we'll examine the rest of the scaffolded code and add a `SearchIndex` method and a `SearchIndex` view that lets you search for movies in this database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="bb371-194">[이전](adding-a-model.md)
> [다음](examining-the-edit-methods-and-edit-view.md)</span><span class="sxs-lookup"><span data-stu-id="bb371-194">[Previous](adding-a-model.md)
[Next](examining-the-edit-methods-and-edit-view.md)</span></span>
