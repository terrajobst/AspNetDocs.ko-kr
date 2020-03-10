---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
title: Create 메서드 추가 및 뷰 만들기 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 데이터베이스에서 읽고 쓰는 간단한 웹 응용 프로그램을 만듭니다.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: a3a90963-0286-4fa0-9b3d-c230cc18b0a3
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
msc.type: authoredcontent
ms.openlocfilehash: 05a281720f76b107fe8d902ef60d5d2e72af3ef5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437291"
---
# <a name="adding-a-create-method-and-create-view"></a><span data-ttu-id="a97b2-104">메서드 만들기 및 보기 만들기 추가</span><span class="sxs-lookup"><span data-stu-id="a97b2-104">Adding a Create Method and Create View</span></span>

<span data-ttu-id="a97b2-105">[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="a97b2-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="a97b2-106">ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="a97b2-107">데이터베이스에서 읽고 쓰는 간단한 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="a97b2-108">[ASP.NET mvc 학습 센터](../../../index.md) 를 방문 하 여 다른 ASP.NET mvc 자습서 및 샘플을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="a97b2-109">이 섹션에서는 사용자가 데이터베이스에 새 동영상을 만들 수 있도록 하는 데 필요한 지원을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-109">In this section we are going to implement the support necessary to enable users to create new movies in our database.</span></span> <span data-ttu-id="a97b2-110">/Movies/Create URL 작업을 구현 하 여이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-110">We'll do this by implementing the /Movies/Create URL action.</span></span>

<span data-ttu-id="a97b2-111">/Movies/Create URL을 구현 하는 과정은 두 단계로 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-111">Implementing the /Movies/Create URL is a two step process.</span></span> <span data-ttu-id="a97b2-112">사용자가 처음으로/Movies/Create URL을 방문 하면 새 영화를 입력 하기 위해 채울 수 있는 HTML 양식으로 표시 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-112">When a user first visits the /Movies/Create URL we want to show them an HTML form that they can fill out to enter a new movie.</span></span> <span data-ttu-id="a97b2-113">그런 다음 사용자가 폼을 제출 하 고 데이터를 서버에 다시 게시할 때 게시 된 내용을 검색 하 여 데이터베이스에 저장 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-113">Then, when the user submits the form and posts the data back to the server, we want to retrieve the posted contents and save it into our database.</span></span>

<span data-ttu-id="a97b2-114">Moviescontroller.cs 클래스 내에서 두 개의 Create () 메서드 내에서 이러한 두 단계를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-114">We'll implement these two steps within two Create() methods within our MoviesController class.</span></span> <span data-ttu-id="a97b2-115">한 가지 방법은 사용자가 새 동영상을 만들기 위해 채워야 하&gt; &lt;폼을 표시 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-115">One method will show the &lt;form&gt; that the user should fill out to create a new movie.</span></span> <span data-ttu-id="a97b2-116">두 번째 방법은 사용자가 서버에 다시&gt; &lt;폼을 전송 하 고 데이터베이스 내에 새 동영상을 저장할 때 게시 된 데이터의 처리를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-116">The second method will handle processing the posted data when the user submits the &lt;form&gt; back to the server, and save a new Movie within our database.</span></span>

<span data-ttu-id="a97b2-117">이를 구현 하기 위해 Moviescontroller.cs 클래스에 추가 하는 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-117">Below is the code we'll add to our MoviesController class to implement this:</span></span>

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample1.cs)]

<span data-ttu-id="a97b2-118">위의 코드에는 컨트롤러 내에서 필요한 모든 코드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-118">The above code contains all of the code that we'll need within our Controller.</span></span>

<span data-ttu-id="a97b2-119">이제 사용자에 게 폼을 표시 하는 데 사용할 만들기 뷰 템플릿을 구현 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-119">Let's now implement the Create View template that we'll use to display a form to the user.</span></span> <span data-ttu-id="a97b2-120">첫 번째 Create 메서드를 마우스 오른쪽 단추로 클릭 하 고 "뷰 추가"를 선택 하 여 동영상 양식에 대 한 보기 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-120">We'll right click in the first Create method and select "Add View" to create the view template for our Movie form.</span></span>

<span data-ttu-id="a97b2-121">보기 템플릿을 해당 뷰 데이터 클래스로 전달 하 고 "스 캐 폴드" 템플릿을 "생성" 하도록 지정 하는 것을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-121">We'll select that we are going to pass the view template a "Movie" as its view data class, and indicate that we want to "scaffold" a "Create" template.</span></span>

<span data-ttu-id="a97b2-122">[뷰 추가 ![](getting-started-with-mvc-part6/_static/image2.png)](getting-started-with-mvc-part6/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a97b2-122">[![Add View](getting-started-with-mvc-part6/_static/image2.png)](getting-started-with-mvc-part6/_static/image1.png)</span></span>

<span data-ttu-id="a97b2-123">추가 단추를 클릭 하면 \Movies\Create.aspx View 템플릿이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-123">After you click the Add button, \Movies\Create.aspx View template will be created for you.</span></span> <span data-ttu-id="a97b2-124">"콘텐츠 보기" 드롭다운에서 "만들기"를 선택 했으므로 보기 추가 대화 상자에서 일부 기본 콘텐츠를 자동으로 "스 캐 폴드" 합니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-124">Because we selected "Create" from the "view content" dropdown, the Add View dialog automatically "scaffolded" some default content for us.</span></span> <span data-ttu-id="a97b2-125">스 캐 폴딩은 HTML &lt;폼&gt;, 유효성 검사 오류 메시지를 이동할 위치 및 스 캐 폴딩이 동영상에 대해 알고 있으므로 클래스의 각 속성에 대 한 레이블 및 필드를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-125">The scaffolding created an HTML &lt;form&gt;, a place for validation error messages to go, and since scaffolding knows about Movies, it created Label and Fields for each property of our class.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part6/samples/sample2.aspx)]

<span data-ttu-id="a97b2-126">데이터베이스는 영화 ID를 자동으로 제공 하므로 모델을 참조 하는 필드를 제거 하겠습니다. 만들기 뷰의 Id입니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-126">Since our database automatically gives a Movie an ID, let's remove those fields that reference model.Id from our Create View.</span></span> <span data-ttu-id="a97b2-127">범례&gt;필드 &lt;후 7 줄을 제거 합니다 .이 필드는 원하지 않는 ID 필드를 표시&gt;&lt;.</span><span class="sxs-lookup"><span data-stu-id="a97b2-127">Remove the 7 lines after &lt;legend&gt;Fields&lt;/legend&gt; as they show the ID field that we don't want.</span></span>

<span data-ttu-id="a97b2-128">이제 새 영화를 만들어 데이터베이스에 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-128">Let's now create a new movie and add it to the database.</span></span> <span data-ttu-id="a97b2-129">이 작업을 수행 하려면 응용 프로그램을 다시 실행 하 고 "/Dlurl" URL을 방문 하 여 "만들기" 링크를 클릭 하 여 새 영화를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-129">We'll do this by running the application again and visit the "/Movies" URL and click the "Create" link to add a new Movie.</span></span>

<span data-ttu-id="a97b2-130">[![만들기-Windows Internet Explorer](getting-started-with-mvc-part6/_static/image4.png)](getting-started-with-mvc-part6/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="a97b2-130">[![Create - Windows Internet Explorer](getting-started-with-mvc-part6/_static/image4.png)](getting-started-with-mvc-part6/_static/image3.png)</span></span>

<span data-ttu-id="a97b2-131">만들기 단추를 클릭 하면이 폼의 데이터를 방금 만든/Movies/Create 메서드에 다시 게시 합니다 (HTTP POST를 통해).</span><span class="sxs-lookup"><span data-stu-id="a97b2-131">When we click the Create button, we'll be posting back (via HTTP POST) the data on this form to the /Movies/Create method that we just created.</span></span> <span data-ttu-id="a97b2-132">시스템에서 URL의 "numTimes" 및 "name" 매개 변수를 자동으로 가져와 이전 메서드의 매개 변수에 매핑한 경우와 마찬가지로 시스템에서 자동으로 양식 필드를 POST에서 자동으로 가져와 개체에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-132">Just like when the system automatically took the "numTimes" and "name " parameter out of the URL and mapped them to parameters on a method earlier, the system will automatically take the Form Fields from a POST and map them to an object.</span></span> <span data-ttu-id="a97b2-133">이 경우 "ReleaseDate" 및 "Title"과 같은 HTML 필드의 값은 자동으로 동영상의 새 인스턴스에 대 한 올바른 속성에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-133">In this case, values from fields in HTML like "ReleaseDate" and "Title" will automatically be put into the correct properties of a new instance of a Movie.</span></span>

<span data-ttu-id="a97b2-134">Moviescontroller.cs에서 두 번째 Create 메서드를 다시 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-134">Let's look at the second Create method from our MoviesController again.</span></span> <span data-ttu-id="a97b2-135">"영화" 개체를 인수로 사용 하는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-135">Notice how it takes a "Movie" object as an argument:</span></span>

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample3.cs)]

<span data-ttu-id="a97b2-136">그런 다음이 Movie 개체는 Create action 메서드의 [HttpPost] 버전으로 전달 된 후 데이터베이스에 저장 된 다음 사용자를 Index () 작업 메서드로 다시 리디렉션하여 저장 된 결과를 동영상 목록에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-136">This Movie object was then passed to the [HttpPost] version of our Create action method, and we saved it in the database and then redirected the user back to the Index() action method which will show the saved result in the movie list:</span></span>

<span data-ttu-id="a97b2-137">[![동영상 목록-Windows Internet Explorer](getting-started-with-mvc-part6/_static/image6.png)](getting-started-with-mvc-part6/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="a97b2-137">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part6/_static/image6.png)](getting-started-with-mvc-part6/_static/image5.png)</span></span>

<span data-ttu-id="a97b2-138">그러나 동영상이 정확한 지 여부를 확인 하지 않으며, 데이터베이스에서 제목이 없는 영화를 저장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-138">We aren't checking if our movies are correct, though, and the database won't allow us to save a movie with no Title.</span></span> <span data-ttu-id="a97b2-139">데이터베이스에 오류가 발생 하기 전에 사용자에 게 알릴 수 있는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-139">It'd be nice if we could tell the user that before the database threw an error.</span></span> <span data-ttu-id="a97b2-140">응용 프로그램에 유효성 검사 지원을 추가 하 여 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a97b2-140">We'll do this next by adding validation support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a97b2-141">[이전](getting-started-with-mvc-part5.md)
> [다음](getting-started-with-mvc-part7.md)</span><span class="sxs-lookup"><span data-stu-id="a97b2-141">[Previous](getting-started-with-mvc-part5.md)
[Next](getting-started-with-mvc-part7.md)</span></span>
