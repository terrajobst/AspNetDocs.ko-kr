---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
title: '3 부: 뷰 및 ViewModels | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 3 부에서는 뷰 및 ViewModels을 다룹니다.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 94297aa0-1f2d-4d72-bbcb-63f64653e0c0
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
msc.type: authoredcontent
ms.openlocfilehash: 3fcfc816cde22c697a78bab2c9ea7ace1bf68501
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451133"
---
# <a name="part-3-views-and-viewmodels"></a><span data-ttu-id="b1b68-104">3 부: 뷰 및 ViewModels</span><span class="sxs-lookup"><span data-stu-id="b1b68-104">Part 3: Views and ViewModels</span></span>

<span data-ttu-id="b1b68-105">받은 사람 ( [Jon Galloway](https://github.com/jongalloway) )</span><span class="sxs-lookup"><span data-stu-id="b1b68-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="b1b68-106">MVC Music Store는 웹 개발용 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 소개 하 고 설명 하는 자습서 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="b1b68-107">MVC Music Store는 온라인으로 음악 앨범을 판매 하 고 기본적인 사이트 관리, 사용자 로그인 및 쇼핑 카트 기능을 구현 하는 간단한 샘플 저장소 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="b1b68-108">이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="b1b68-109">3 부에서는 뷰 및 ViewModels을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-109">Part 3 covers Views and ViewModels.</span></span>

<span data-ttu-id="b1b68-110">지금까지 컨트롤러 작업에서 문자열을 반환 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-110">So far we've just been returning strings from controller actions.</span></span> <span data-ttu-id="b1b68-111">이 방법은 컨트롤러의 작동 방식을 파악 하는 좋은 방법 이지만 실제 웹 응용 프로그램을 빌드하는 방법은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-111">That's a nice way to get an idea of how controllers work, but it's not how you'd want to build a real web application.</span></span> <span data-ttu-id="b1b68-112">사이트를 방문 하는 브라우저에 다시 HTML을 생성 하는 더 나은 방법을 원할 것입니다. 즉, 템플릿 파일을 사용 하 여 HTML 콘텐츠를 더 쉽게 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-112">We are going to want a better way to generate HTML back to browsers visiting our site – one where we can use template files to more easily customize the HTML content send back.</span></span> <span data-ttu-id="b1b68-113">이는 보기에서 수행 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-113">That's exactly what Views do.</span></span>

## <a name="adding-a-view-template"></a><span data-ttu-id="b1b68-114">보기 템플릿 추가</span><span class="sxs-lookup"><span data-stu-id="b1b68-114">Adding a View template</span></span>

<span data-ttu-id="b1b68-115">뷰 템플릿을 사용 하려면 HomeController Index 메서드를 변경 하 여 ActionResult를 반환 하 고 아래와 같이 View ()를 반환 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-115">To use a view-template, we'll change the HomeController Index method to return an ActionResult, and have it return View(), like below:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample1.cs)]

<span data-ttu-id="b1b68-116">위의 변경 내용은 대신 문자열을 반환 하는 대신 "뷰"를 사용 하 여 결과를 다시 생성 하는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-116">The above change indicates that instead of returned a string, we instead want to use a "View" to generate a result back.</span></span>

<span data-ttu-id="b1b68-117">이제 프로젝트에 적절 한 뷰 템플릿을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-117">We'll now add an appropriate View template to our project.</span></span> <span data-ttu-id="b1b68-118">이렇게 하려면 인덱스 작업 메서드 내에 텍스트 커서를 놓고 마우스 오른쪽 단추를 클릭 한 다음 "뷰 추가"를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-118">To do this we'll position the text cursor within the Index action method, then right-click and select "Add View".</span></span> <span data-ttu-id="b1b68-119">그러면 보기 추가 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-119">This will bring up the Add View dialog:</span></span>

<span data-ttu-id="b1b68-120">![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b1b68-120">![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)</span></span>

<span data-ttu-id="b1b68-121">"뷰 추가" 대화 상자를 사용 하 여 보기 템플릿 파일을 빠르고 쉽게 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-121">The "Add View" dialog allows us to quickly and easily generate View template files.</span></span> <span data-ttu-id="b1b68-122">기본적으로 "뷰 추가" 대화 상자는 만들 뷰 템플릿의 이름을 미리 채우고,이를 사용 하는 동작 메서드와 일치 하도록 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-122">By default the "Add View" dialog pre-populates the name of the View template to create so that it matches the action method that will use it.</span></span> <span data-ttu-id="b1b68-123">HomeController의 Index () 동작 메서드 내에서 "뷰 추가" 상황에 맞는 메뉴를 사용 했으므로 위의 "뷰 추가" 대화 상자에는 기본적으로 미리 채워진 뷰 이름으로 "인덱스"가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-123">Because we used the "Add View" context menu within the Index() action method of our HomeController, the "Add View" dialog above has "Index" as the view name pre-populated by default.</span></span> <span data-ttu-id="b1b68-124">이 대화 상자의 옵션을 변경할 필요 없이 추가 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-124">We don't need to change any of the options on this dialog, so click the Add button.</span></span>

<span data-ttu-id="b1b68-125">추가 단추를 클릭 하면 Visual Web Developer에서 \Views\Home 디렉터리에 새 인덱스를 만듭니다 .이 폴더는 아직 존재 하지 않는 경우 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-125">When we click the Add button, Visual Web Developer will create a new Index.cshtml view template for us in the \Views\Home directory, creating the folder if doesn't already exist.</span></span>

![](mvc-music-store-part-3/_static/image2.png)

<span data-ttu-id="b1b68-126">"Index. cshtml" 파일의 이름 및 폴더 위치는 중요 하며 기본 ASP.NET MVC 명명 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-126">The name and folder location of the "Index.cshtml" file is important, and follows the default ASP.NET MVC naming conventions.</span></span> <span data-ttu-id="b1b68-127">디렉터리 이름 \Views\Home는 HomeController 라는 컨트롤러와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-127">The directory name, \Views\Home, matches the controller - which is named HomeController.</span></span> <span data-ttu-id="b1b68-128">뷰 템플릿 이름 Index는 뷰를 표시 하는 컨트롤러 작업 메서드와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-128">The view template name, Index, matches the controller action method which will be displaying the view.</span></span>

<span data-ttu-id="b1b68-129">ASP.NET MVC를 사용 하면이 명명 규칙을 사용 하 여 뷰를 반환할 때 뷰 템플릿의 이름이 나 위치를 명시적으로 지정 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-129">ASP.NET MVC allows us to avoid having to explicitly specify the name or location of a view template when we use this naming convention to return a view.</span></span> <span data-ttu-id="b1b68-130">HomeController 내에서 아래와 같이 코드를 작성할 때 기본적으로 \Views\Home\Index.cshtml view 템플릿이 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-130">It will by default render the \Views\Home\Index.cshtml view template when we write code like below within our HomeController:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample2.cs)]

<span data-ttu-id="b1b68-131">"뷰 추가" 대화 상자에서 "추가" 단추를 클릭 한 후에 Visual Web Developer에서 "Index. cshtml" 뷰 템플릿을 만들고 열었습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-131">Visual Web Developer created and opened the "Index.cshtml" view template after we clicked the "Add" button within the "Add View" dialog.</span></span> <span data-ttu-id="b1b68-132">Index. cshtml의 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-132">The contents of Index.cshtml are shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample3.cshtml)]

<span data-ttu-id="b1b68-133">이 보기는 ASP.NET Web Forms 및 이전 버전의 ASP.NET MVC에서 사용 되는 Web Forms 뷰 엔진 보다 간결한 Razor 구문를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-133">This view is using the Razor syntax, which is more concise than the Web Forms view engine used in ASP.NET Web Forms and previous versions of ASP.NET MVC.</span></span> <span data-ttu-id="b1b68-134">Web Forms 뷰 엔진은 ASP.NET MVC 3에서 계속 사용할 수 있지만 대부분의 개발자는 Razor 뷰 엔진이 ASP.NET MVC 개발을 잘 충족 한다는 것을 알게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-134">The Web Forms view engine is still available in ASP.NET MVC 3, but many developers find that the Razor view engine fits ASP.NET MVC development really well.</span></span>

<span data-ttu-id="b1b68-135">처음 세 줄에서는 ViewBag를 사용 하 여 페이지 제목을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-135">The first three lines set the page title using ViewBag.Title.</span></span> <span data-ttu-id="b1b68-136">이 방법이 곧 어떻게 작동 하는지 살펴보겠습니다. 먼저 텍스트 제목 텍스트를 업데이트 하 고 페이지를 확인 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-136">We'll look at how this works in more detail soon, but first let's update the text heading text and view the page.</span></span> <span data-ttu-id="b1b68-137">아래와 같이 &lt;h2&gt; 태그를 "이것이 홈 페이지입니다."로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-137">Update the &lt;h2&gt; tag to say "This is the Home Page" as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample4.cshtml)]

<span data-ttu-id="b1b68-138">응용 프로그램을 실행 하면 새 텍스트가 홈 페이지에 표시 되는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-138">Running the application shows that our new text is visible on the home page.</span></span>

![](mvc-music-store-part-3/_static/image3.png)

## <a name="using-a-layout-for-common-site-elements"></a><span data-ttu-id="b1b68-139">공통 사이트 요소에 레이아웃 사용</span><span class="sxs-lookup"><span data-stu-id="b1b68-139">Using a Layout for common site elements</span></span>

<span data-ttu-id="b1b68-140">대부분의 웹 사이트에는 탐색, 바닥글, 로고 이미지, 스타일 시트 참조 등 여러 페이지 간에 공유 되는 콘텐츠가 있습니다. Razor 뷰 엔진을 사용 하면/Views/Shared 폴더 내에 자동으로 생성 된 레이아웃. cshtml \_이라는 페이지를 사용 하 여이를 쉽게 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-140">Most websites have content which is shared between many pages: navigation, footers, logo images, stylesheet references, etc. The Razor view engine makes this easy to manage using a page called \_Layout.cshtml which has automatically been created for us inside the /Views/Shared folder.</span></span>

![](mvc-music-store-part-3/_static/image4.png)

<span data-ttu-id="b1b68-141">이 폴더를 두 번 클릭 하면 아래와 같은 내용이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-141">Double-click on this folder to view the contents, which are shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample5.cshtml)]

<span data-ttu-id="b1b68-142">개별 보기의 콘텐츠는 @RenderBody() 명령에 의해 표시 되 고 외부에 표시 하려는 모든 공통 콘텐츠는 \_레이아웃에 추가할 수 있습니다. cshtml 태그.</span><span class="sxs-lookup"><span data-stu-id="b1b68-142">The content from our individual views will be displayed by the @RenderBody() command, and any common content that we want to appear outside of that can be added to the \_Layout.cshtml markup.</span></span> <span data-ttu-id="b1b68-143">MVC Music Store에는 홈 페이지에 대 한 링크가 포함 된 공통 헤더와 사이트의 모든 페이지에 대 한 저장 영역이 있으므로 해당 @RenderBody() 문 바로 위의 템플릿에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-143">We'll want our MVC Music Store to have a common header with links to our Home page and Store area on all pages in the site, so we'll add that to the template directly above that @RenderBody() statement.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample6.cshtml)]

## <a name="updating-the-stylesheet"></a><span data-ttu-id="b1b68-144">스타일 시트 업데이트</span><span class="sxs-lookup"><span data-stu-id="b1b68-144">Updating the StyleSheet</span></span>

<span data-ttu-id="b1b68-145">빈 프로젝트 템플릿에는 유효성 검사 메시지를 표시 하는 데 사용 되는 스타일을 포함 하는 매우 간소화 된 CSS 파일이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-145">The empty project template includes a very streamlined CSS file which just includes styles used to display validation messages.</span></span> <span data-ttu-id="b1b68-146">Microsoft의 디자이너는 사이트의 모양과 느낌을 정의 하기 위해 몇 가지 CSS 및 이미지를 제공 했으므로 지금은이를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-146">Our designer has provided some additional CSS and images to define the look and feel for our site, so we'll add those in now.</span></span>

<span data-ttu-id="b1b68-147">업데이트 된 CSS 파일 및 이미지는 MvcMusicStore-Assets의 콘텐츠 디렉터리에 포함 되며,이는 [MVC-음악 스토어](https://github.com/evilDave/MVC-Music-Store)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-147">The updated CSS file and Images are included in the Content directory of MvcMusicStore-Assets.zip which is available at [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span> <span data-ttu-id="b1b68-148">Windows 탐색기에서 두 가지를 모두 선택 하 고 아래와 같이 Visual Web Developer의 솔루션 콘텐츠 폴더에 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-148">We'll select both of them in Windows Explorer and drop them into our Solution's Content folder in Visual Web Developer, as shown below:</span></span>

![](mvc-music-store-part-3/_static/image5.png)

<span data-ttu-id="b1b68-149">기존 사이트 .css 파일을 덮어쓸지 여부를 확인 하는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-149">You'll be asked to confirm if you want to overwrite the existing Site.css file.</span></span> <span data-ttu-id="b1b68-150">예를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-150">Click Yes.</span></span>

![](mvc-music-store-part-3/_static/image6.png)

<span data-ttu-id="b1b68-151">이제 응용 프로그램의 콘텐츠 폴더가 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-151">The Content folder of your application will now appear as follows:</span></span>

![](mvc-music-store-part-3/_static/image7.png)

<span data-ttu-id="b1b68-152">이제 응용 프로그램을 실행 하 여 홈 페이지에 변경 내용이 어떻게 표시 되는지 확인해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-152">Now let's run the application and see how our changes look on the Home page.</span></span>

![](mvc-music-store-part-3/_static/image8.png)

- <span data-ttu-id="b1b68-153">변경 된 내용 검토: 뷰 템플릿이 표준 명명 규칙을 준수 하기 때문에 HomeController의 인덱스 작업 메서드는 \Views\Home\Index.cshtmlView 템플릿을 찾아 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-153">Let's review what's changed: The HomeController's Index action method found and displayed the \Views\Home\Index.cshtmlView template, even though our code called "return View()", because our View template followed the standard naming convention.</span></span>
- <span data-ttu-id="b1b68-154">홈 페이지에 \Views\Home\Index.cshtml view 템플릿 내에 정의 된 간단한 환영 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-154">The Home Page is displaying a simple welcome message that is defined within the \Views\Home\Index.cshtml view template.</span></span>
- <span data-ttu-id="b1b68-155">홈 페이지는 \_레이아웃을 사용 하 고 있으므로 시작 메시지는 표준 사이트 HTML 레이아웃에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-155">The Home Page is using our \_Layout.cshtml template, and so the welcome message is contained within the standard site HTML layout.</span></span>

## <a name="using-a-model-to-pass-information-to-our-view"></a><span data-ttu-id="b1b68-156">모델을 사용 하 여 보기에 정보 전달</span><span class="sxs-lookup"><span data-stu-id="b1b68-156">Using a Model to pass information to our View</span></span>

<span data-ttu-id="b1b68-157">하드 코딩 된 HTML을 표시 하는 보기 템플릿은 매우 흥미로운 웹 사이트를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-157">A View template that just displays hardcoded HTML isn't going to make a very interesting web site.</span></span> <span data-ttu-id="b1b68-158">동적 웹 사이트를 만들려면 컨트롤러 작업에서 보기 템플릿으로 정보를 전달 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-158">To create a dynamic web site, we'll instead want to pass information from our controller actions to our view templates.</span></span>

<span data-ttu-id="b1b68-159">모델-뷰-컨트롤러 패턴에서 모델 이라는 용어는 응용 프로그램의 데이터를 나타내는 개체를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-159">In the Model-View-Controller pattern, the term Model refers to objects which represent the data in the application.</span></span> <span data-ttu-id="b1b68-160">종종 model 개체는 데이터베이스의 테이블에 해당 하지만 반드시 그런 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-160">Often, model objects correspond to tables in your database, but they don't have to.</span></span>

<span data-ttu-id="b1b68-161">ActionResult를 반환 하는 컨트롤러 동작 메서드는 모델 개체를 뷰에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-161">Controller action methods which return an ActionResult can pass a model object to the view.</span></span> <span data-ttu-id="b1b68-162">이렇게 하면 컨트롤러에서 응답을 생성 하는 데 필요한 모든 정보를 완전히 패키지할 수 있으며,이 정보를 사용 하 여 적절 한 HTML 응답을 생성 하는 데 사용 하는 보기 템플릿에이 정보를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-162">This allows a Controller to cleanly package up all the information needed to generate a response, and then pass this information off to a View template to use to generate the appropriate HTML response.</span></span> <span data-ttu-id="b1b68-163">이 작업을 수행 하는 것을 이해 하는 것이 가장 쉬운 방법 이므로 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-163">This is easiest to understand by seeing it in action, so let's get started.</span></span>

<span data-ttu-id="b1b68-164">먼저 저장소 내에서 장르 및 앨범을 나타내는 일부 모델 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-164">First we'll create some Model classes to represent Genres and Albums within our store.</span></span> <span data-ttu-id="b1b68-165">먼저 장르 클래스를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-165">Let's start by creating a Genre class.</span></span> <span data-ttu-id="b1b68-166">프로젝트 내에서 "모델" 폴더를 마우스 오른쪽 단추로 클릭 하 고 "클래스 추가" 옵션을 선택한 다음 파일 이름을 "Genre.cs"로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-166">Right-click the "Models" folder within your project, choose the "Add Class" option, and name the file "Genre.cs".</span></span>

![](mvc-music-store-part-3/_static/image2.jpg)

![](mvc-music-store-part-3/_static/image9.png)

<span data-ttu-id="b1b68-167">그런 다음 생성 된 클래스에 공용 문자열 이름 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-167">Then add a public string Name property to the class that was created:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample7.cs)]

<span data-ttu-id="b1b68-168">*참고: 해당 하는 경우 {get; set;} 표기법은 C#의 자동 구현 속성 기능을 사용 합니다. 이를 통해 지원 필드를 선언 하지 않고도 속성의 이점을 얻을 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="b1b68-168">*Note: In case you're wondering, the { get; set; } notation is making use of C#'s auto-implemented properties feature. This gives us the benefits of a property without requiring us to declare a backing field.*</span></span>

<span data-ttu-id="b1b68-169">그런 다음, 동일한 단계를 수행 하 여 제목과 장르 속성이 있는 앨범 클래스 (이름이 Album.cs)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-169">Next, follow the same steps to create an Album class (named Album.cs) that has a Title and a Genre property:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample8.cs)]

<span data-ttu-id="b1b68-170">이제 모델의 동적 정보를 표시 하는 보기를 사용 하도록 StoreController를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-170">Now we can modify the StoreController to use Views which display dynamic information from our Model.</span></span> <span data-ttu-id="b1b68-171">현재 데모 목적으로 사용 하는 경우, 요청 ID를 기준으로 앨범의 이름을 지정 하면 아래 보기와 같이 해당 정보를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-171">If - for demonstration purposes right now - we named our Albums based on the request ID, we could display that information as in the view below.</span></span>

![](mvc-music-store-part-3/_static/image10.png)

<span data-ttu-id="b1b68-172">먼저 저장소 정보 작업을 변경 하 여 단일 앨범에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-172">We'll start by changing the Store Details action so it shows the information for a single album.</span></span> <span data-ttu-id="b1b68-173">**StoreControllers** 클래스의 맨 위에 "using" 문을 추가 하 여 MvcMusicStore 네임 스페이스를 포함 합니다. 따라서 앨범 클래스를 사용 하려고 할 때마다 MvcMusicStore를 입력할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-173">Add a "using" statement to the top of the **StoreControllers** class to include the MvcMusicStore.Models namespace, so we don't need to type MvcMusicStore.Models.Album every time we want to use the album class.</span></span> <span data-ttu-id="b1b68-174">이제 해당 클래스의 "using" 섹션이 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-174">The "usings" section of that class should now appear as below.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample9.cs)]

<span data-ttu-id="b1b68-175">다음으로 HomeController의 Index 메서드와 같이 문자열이 아니라 ActionResult를 반환 하도록 세부 정보 컨트롤러 작업을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-175">Next, we'll update the Details controller action so that it returns an ActionResult rather than a string, as we did with the HomeController's Index method.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample10.cs)]

<span data-ttu-id="b1b68-176">이제 앨범 개체를 뷰에 반환 하도록 논리를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-176">Now we can modify the logic to return an Album object to the view.</span></span> <span data-ttu-id="b1b68-177">이 자습서의 뒷부분에서는 데이터베이스에서 데이터를 검색할 예정 이지만, 지금은 "더미 데이터"를 사용 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-177">Later in this tutorial we will be retrieving the data from a database – but for right now we will use "dummy data" to get started.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample11.cs)]

<span data-ttu-id="b1b68-178">*참고:에 C#익숙하지 않은 경우 var을 사용 한다고 해 서 현재 앨범 변수가 런타임에 바인딩되어 있다고 가정할 수 있습니다. 올바르지 않습니다. 컴파일러는 C# 이 변수에 할당 하는 내용에 따라 형식 유추를 사용 하 여 앨범이 앨범 형식이 고 로컬 앨범 변수를 앨범 형식으로 컴파일 했기 때문에 컴파일 시간 검사 및 Visual Studio code-편집기를 지원 합니다.*</span><span class="sxs-lookup"><span data-stu-id="b1b68-178">*Note: If you're unfamiliar with C#, you may assume that using var means that our album variable is late-bound. That's not correct – the C# compiler is using type-inference based on what we're assigning to the variable to determine that album is of type Album and compiling the local album variable as an Album type, so we get compile-time checking and Visual Studio code-editor support.*</span></span>

<span data-ttu-id="b1b68-179">이제 앨범을 사용 하 여 HTML 응답을 생성 하는 보기 템플릿을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-179">Let's now create a View template that uses our Album to generate an HTML response.</span></span> <span data-ttu-id="b1b68-180">이렇게 하려면 먼저 새로 만든 앨범 클래스에 대해 보기 추가 대화 상자에서 알 수 있도록 프로젝트를 빌드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-180">Before we do that we need to build the project so that the Add View dialog knows about our newly created Album class.</span></span> <span data-ttu-id="b1b68-181">⇨ Build MvcMusicStore 디버그 메뉴 항목을 선택 하 여 프로젝트를 빌드할 수 있습니다. 추가 크레딧을 위해 Ctrl + Shift + B 바로 가기를 사용 하 여 프로젝트를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-181">You can build the project by selecting the Debug⇨Build MvcMusicStore menu item (for extra credit, you can use the Ctrl-Shift-B shortcut to build the project).</span></span>

![](mvc-music-store-part-3/_static/image11.png)

<span data-ttu-id="b1b68-182">이제 지원 클래스를 설정 했으므로 보기 템플릿을 빌드할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-182">Now that we've set up our supporting classes, we're ready to build our View template.</span></span> <span data-ttu-id="b1b68-183">Details 메서드 내에서 마우스 오른쪽 단추를 클릭 하 고 "보기 추가 ..."를 선택 합니다. 상황에 맞는 메뉴에서.</span><span class="sxs-lookup"><span data-stu-id="b1b68-183">Right-click within the Details method and select "Add View…" from the context menu.</span></span>

![](mvc-music-store-part-3/_static/image12.png)

<span data-ttu-id="b1b68-184">HomeController 이전에 했던 것 처럼 새 보기 템플릿을 만들 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-184">We are going to create a new View template like we did before with the HomeController.</span></span> <span data-ttu-id="b1b68-185">StoreController에서 생성 하기 때문에 기본적으로 \Views\Store\Index.cshtml 파일에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-185">Because we are creating it from the StoreController it will by default be generated in a \Views\Store\Index.cshtml file.</span></span>

<span data-ttu-id="b1b68-186">이전과는 달리 "강력한 형식의" 보기 만들기 "확인란을 선택 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-186">Unlike before, we are going to check the "Create a strongly-typed" view checkbox.</span></span> <span data-ttu-id="b1b68-187">그런 다음 "데이터 클래스 보기" 드롭다운 목록에서 "앨범" 클래스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-187">We are then going to select our "Album" class within the "View data-class" drop-downlist.</span></span> <span data-ttu-id="b1b68-188">이렇게 하면 "뷰 추가" 대화 상자에서 앨범 개체를 사용 하기 위해 전달 될 것으로 예상 되는 보기 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-188">This will cause the "Add View" dialog to create a View template that expects that an Album object will be passed to it to use.</span></span>

![](mvc-music-store-part-3/_static/image13.png)

<span data-ttu-id="b1b68-189">"추가" 단추를 클릭 하면 다음 코드가 포함 된 \Views\Store\Details.cshtml View 템플릿이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-189">When we click the "Add" button our \Views\Store\Details.cshtml View template will be created, containing the following code.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample12.cshtml)]

<span data-ttu-id="b1b68-190">첫 번째 줄은이 뷰가 앨범 클래스에 강력한 형식 임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-190">Notice the first line, which indicates that this view is strongly-typed to our Album class.</span></span> <span data-ttu-id="b1b68-191">Razor 뷰 엔진은 앨범 개체가 전달 되었음을 인식 하므로 모델 속성에 쉽게 액세스할 수 있으며 Visual Web Developer 편집기에서 IntelliSense의 이점을 누릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-191">The Razor view engine understands that it has been passed an Album object, so we can easily access model properties and even have the benefit of IntelliSense in the Visual Web Developer editor.</span></span>

<span data-ttu-id="b1b68-192">&lt;h2&gt; 태그를 업데이트 하 여 다음과 같이 표시 되도록 해당 줄을 수정 하 여 앨범의 Title 속성을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-192">Update the &lt;h2&gt; tag so it displays the Album's Title property by modifying that line to appear as follows.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample13.cshtml)]

<span data-ttu-id="b1b68-193">@Model 키워드 뒤에 마침표를 입력 하면 해당 사용자가 앨범 클래스에서 지 원하는 속성 및 메서드를 표시 하는 IntelliSense가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-193">Notice that IntelliSense is triggered when you enter the period after the @Model keyword, showing the properties and methods that the Album class supports.</span></span>

<span data-ttu-id="b1b68-194">이제 프로젝트를 다시 실행 하 고/Store/Details/5 URL을 방문 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-194">Let's now re-run our project and visit the /Store/Details/5 URL.</span></span> <span data-ttu-id="b1b68-195">아래와 같은 앨범의 세부 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-195">We'll see details of an Album like below.</span></span>

![](mvc-music-store-part-3/_static/image14.png)

<span data-ttu-id="b1b68-196">이제 Store Browse 동작 메서드에 대해 비슷한 업데이트를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-196">Now we'll make a similar update for the Store Browse action method.</span></span> <span data-ttu-id="b1b68-197">ActionResult를 반환 하도록 메서드를 업데이트 하 고 새 장르 개체를 만들어 뷰로 반환 하도록 메서드 논리를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-197">Update the method so it returns an ActionResult, and modify the method logic so it creates a new Genre object and returns it to the View.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample14.cs)]

<span data-ttu-id="b1b68-198">찾아보기 메서드를 마우스 오른쪽 단추로 클릭 하 고 "보기 추가 ..."를 선택 합니다. 상황에 맞는 메뉴에서 강력한 형식의 뷰를 추가 하 여 장르 클래스에 강력한 형식의를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-198">Right-click in the Browse method and select "Add View…" from the context menu, then add a View that is strongly-typed add a strongly typed to the Genre class.</span></span>

![](mvc-music-store-part-3/_static/image15.png)

<span data-ttu-id="b1b68-199">/Views/Store/Browse.cshtml에서 뷰 코드의 &lt;h2&gt; 요소를 업데이트 하 여 장르 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-199">Update the &lt;h2&gt; element in the view code (in /Views/Store/Browse.cshtml) to display the Genre information.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample15.cshtml)]

<span data-ttu-id="b1b68-200">이제 프로젝트를 다시 실행 하 고/sv/dhers로 이동 하겠습니다. 장르 = Disco URL.</span><span class="sxs-lookup"><span data-stu-id="b1b68-200">Now let's re-run our project and browse to the /Store/Browse?Genre=Disco URL.</span></span> <span data-ttu-id="b1b68-201">아래와 같이 표시 되는 찾아보기 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-201">We'll see the Browse page displayed like below.</span></span>

![](mvc-music-store-part-3/_static/image16.png)

<span data-ttu-id="b1b68-202">마지막으로 저장소 **인덱스** 작업 메서드 및 보기에 대해 약간 더 복잡 한 업데이트를 수행 하 여 스토어의 모든 장르 목록을 표시 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-202">Finally, let's make a slightly more complex update to the **Store Index** action method and view to display a list of all the Genres in our store.</span></span> <span data-ttu-id="b1b68-203">이 작업을 수행 하려면 단일 장르 대신 모델 개체로 장르 목록을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-203">We'll do that by using a List of Genres as our model object, rather than just a single Genre.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample16.cs)]

<span data-ttu-id="b1b68-204">저장소 인덱스 작업 메서드를 마우스 오른쪽 단추로 클릭 하 고, 이전과 같이 뷰 추가를 선택 하 고, 모델 클래스로 장르를 선택 하 고, 추가 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-204">Right-click in the Store Index action method and select Add View as before, select Genre as the Model class, and press the Add button.</span></span>

![](mvc-music-store-part-3/_static/image17.png)

<span data-ttu-id="b1b68-205">먼저 @model 선언을 변경 하 여 뷰가 하나만 아닌 여러 장르 개체가 필요한 것을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-205">First we'll change the @model declaration to indicate that the view will be expecting several Genre objects rather than just one.</span></span> <span data-ttu-id="b1b68-206">다음과 같이/Hfile/p\index.s의 첫 번째 줄을 다음과 같이 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-206">Change the first line of /Store/Index.cshtml to read as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample17.cshtml)]

<span data-ttu-id="b1b68-207">이렇게 하면 여러 장르 개체를 보유할 수 있는 모델 개체를 사용 하 여 Razor 뷰 엔진에 지시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-207">This tells the Razor view engine that it will be working with a model object that can hold several Genre objects.</span></span> <span data-ttu-id="b1b68-208">이는 보다 일반적인 모델 형식을 IEnumerable 인터페이스를 지 원하는 개체 형식으로 변경할 수 있도록 하는 것이 더 일반적 이므로 목록&lt;장르&gt; 아닌 IEnumerable&lt;장르&gt;를 사용 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-208">We're using an IEnumerable&lt;Genre&gt; rather than a List&lt;Genre&gt; since it's more generic, allowing us to change our model type later to any object type that supports the IEnumerable interface.</span></span>

<span data-ttu-id="b1b68-209">다음으로, 아래 완성 된 뷰 코드에 표시 된 대로 모델의 장르 개체를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-209">Next, we'll loop through the Genre objects in the model as shown in the completed view code below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample18.cshtml)]

<span data-ttu-id="b1b68-210">이 코드를 입력할 때 전체 IntelliSense를 지원 하므로 "@Model"을 입력 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-210">Notice that we have full IntelliSense support as we enter this code, so that when we type "@Model."</span></span> <span data-ttu-id="b1b68-211">장르 형식의 IEnumerable에서 지 원하는 모든 메서드 및 속성이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-211">we see all methods and properties supported by an IEnumerable of type Genre.</span></span>

![](mvc-music-store-part-3/_static/image18.png)

<span data-ttu-id="b1b68-212">"Foreach" 루프 내에서 Visual Web Developer는 각 항목이 장르 형식 이라는 것을 인식 하므로 각 장르 형식에 대해 IntelliSense를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-212">Within our "foreach" loop, Visual Web Developer knows that each item is of type Genre, so we see IntelliSense for each the Genre type.</span></span>

![](mvc-music-store-part-3/_static/image19.png)

<span data-ttu-id="b1b68-213">다음으로 스 캐 폴딩 기능은 장르 개체를 검사 하 고 각각에 Name 속성이 있음을 확인 했으므로이를 반복 하 고 작성 합니다. 또한 각 개별 항목에 대 한 편집, 세부 정보 및 삭제 링크를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-213">Next, the scaffolding feature examined the Genre object and determined that each will have a Name property, so it loops through and writes them out. It also generates Edit, Details, and Delete links to each individual item.</span></span> <span data-ttu-id="b1b68-214">저장소 관리자에서 나중에이 기능을 활용할 수 있지만 지금은 간단한 목록을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-214">We'll take advantage of that later in our store manager, but for now we'd like to have a simple list instead.</span></span>

<span data-ttu-id="b1b68-215">응용 프로그램을 실행 하 고/Store로 이동 하면 장르 수와 장르 목록이 모두 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-215">When we run the application and browse to /Store, we see that both the count and list of Genres is displayed.</span></span>

![](mvc-music-store-part-3/_static/image20.png)

## <a name="adding-links-between-pages"></a><span data-ttu-id="b1b68-216">페이지 간 링크 추가</span><span class="sxs-lookup"><span data-stu-id="b1b68-216">Adding Links between pages</span></span>

<span data-ttu-id="b1b68-217">장르를 나열 하는/Store URL은 현재 장르 이름을 일반 텍스트로 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-217">Our /Store URL that lists Genres currently lists the Genre names simply as plain text.</span></span> <span data-ttu-id="b1b68-218">이를 변경해 보겠습니다. 대신 "Disco"와 같은 음악 장르를 클릭 하면 "Disco"와 같은 음악 장르를 클릭 하 여 "Disco"로 이동 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-218">Let's change this so that instead of plain text we instead have the Genre names link to the appropriate /Store/Browse URL, so that clicking on a music genre like "Disco" will navigate to the /Store/Browse?genre=Disco URL.</span></span> <span data-ttu-id="b1b68-219">아래와 같은 코드를 사용 하 여 이러한 링크를 출력 하도록 \Views\Store\Index.cshtml View 템플릿을 업데이트할 수 있습니다 **(이에 대 한 내용을 입력 하지 않음)** .</span><span class="sxs-lookup"><span data-stu-id="b1b68-219">We could update our \Views\Store\Index.cshtml View template to output these links using code like below **(don't type this in - we're going to improve on it)**:</span></span>

[!code-html[Main](mvc-music-store-part-3/samples/sample19.html)]

<span data-ttu-id="b1b68-220">이는 작동 하지만, 나중에 하드 코드 된 문자열을 사용 하기 때문에 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-220">That works, but it could lead to trouble later since it relies on a hardcoded string.</span></span> <span data-ttu-id="b1b68-221">예를 들어 컨트롤러의 이름을 바꾸려는 경우 업데이트 해야 하는 링크를 찾는 코드를 검색 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-221">For instance, if we wanted to rename the Controller, we'd need to search through our code looking for links that need to be updated.</span></span>

<span data-ttu-id="b1b68-222">사용할 수 있는 다른 방법은 HTML 도우미 메서드를 활용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-222">An alternative approach we can use is to take advantage of an HTML Helper method.</span></span> <span data-ttu-id="b1b68-223">ASP.NET MVC에는 다음과 같은 다양 한 일반적인 작업을 수행 하기 위해 뷰 템플릿 코드에서 사용할 수 있는 HTML 도우미 메서드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-223">ASP.NET MVC includes HTML Helper methods which are available from our View template code to perform a variety of common tasks just like this.</span></span> <span data-ttu-id="b1b68-224">Html.actionlink () 도우미 메서드는 특히 유용 하며,&gt; 링크를 &lt;HTML을 쉽게 빌드할 수 있도록 하 고 URL 경로가 적절 하 게 URL로 인코딩 되었는지 확인 하는 것과 같은 성가신 정보를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-224">The Html.ActionLink() helper method is a particularly useful one, and makes it easy to build HTML &lt;a&gt; links and takes care of annoying details like making sure URL paths are properly URL encoded.</span></span>

<span data-ttu-id="b1b68-225">Html.actionlink ()에는 링크에 필요한 만큼의 정보를 지정할 수 있는 여러 오버 로드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-225">Html.ActionLink() has several different overloads to allow specifying as much information as you need for your links.</span></span> <span data-ttu-id="b1b68-226">가장 간단한 경우에는 클라이언트에서 하이퍼링크를 클릭 했을 때 이동할 링크 텍스트 및 동작 메서드만 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-226">In the simplest case, you'll supply just the link text and the Action method to go to when the hyperlink is clicked on the client.</span></span> <span data-ttu-id="b1b68-227">예를 들어 다음 호출을 사용 하 여 "저장소 인덱스로 이동" 링크 텍스트가 포함 된 저장소 세부 정보 페이지에서 "/Bv/" Index () 메서드에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-227">For example, we can link to "/Store/" Index() method on the Store Details page with the link text "Go to the Store Index" using the following call:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample20.cshtml)]

<span data-ttu-id="b1b68-228">*참고:이 경우 현재 뷰를 렌더링 하는 것과 동일한 컨트롤러 내의 다른 작업에 연결 하 고 있으므로 컨트롤러 이름을 지정할 필요가 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="b1b68-228">*Note: In this case, we didn't need to specify the controller name because we're just linking to another action within the same controller that's rendering the current view.*</span></span>

<span data-ttu-id="b1b68-229">찾아보기 페이지에 대 한 링크는 매개 변수를 전달 해야 합니다. 따라서 세 개의 매개 변수를 사용 하는 Html.</span><span class="sxs-lookup"><span data-stu-id="b1b68-229">Our links to the Browse page will need to pass a parameter, though, so we'll use another overload of the Html.ActionLink method that takes three parameters:</span></span>

- 1. <span data-ttu-id="b1b68-230">장르 이름을 표시 하는 링크 텍스트</span><span class="sxs-lookup"><span data-stu-id="b1b68-230">Link text, which will display the Genre name</span></span>
- 2. <span data-ttu-id="b1b68-231">컨트롤러 작업 이름 (찾아보기)</span><span class="sxs-lookup"><span data-stu-id="b1b68-231">Controller action name (Browse)</span></span>
- 3. <span data-ttu-id="b1b68-232">이름 (장르) 및 값 (장르 이름)을 모두 지정 하는 경로 매개 변수 값</span><span class="sxs-lookup"><span data-stu-id="b1b68-232">Route parameter values, specifying both the name (Genre) and the value (Genre name)</span></span>

<span data-ttu-id="b1b68-233">이를 모두 함께 저장 하면 다음은 저장소 인덱스 보기에 이러한 링크를 작성 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-233">Putting that all together, here's how we'll write those links to the Store Index view:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample21.cshtml)]

<span data-ttu-id="b1b68-234">이제 프로젝트를 다시 실행 하 고/Svv/URL에 액세스할 때 장르 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-234">Now when we run our project again and access the /Store/ URL we will see a list of genres.</span></span> <span data-ttu-id="b1b68-235">각 장르는 하이퍼링크입니다. 클릭 하면/Dl/whhhhs? 장르 = *[장르]* URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-235">Each genre is a hyperlink – when clicked it will take us to our /Store/Browse?genre=*[genre]* URL.</span></span>

![](mvc-music-store-part-3/_static/image3.jpg)

<span data-ttu-id="b1b68-236">장르 목록의 HTML은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b68-236">The HTML for the genre list looks like this:</span></span>

[!code-html[Main](mvc-music-store-part-3/samples/sample22.html)]

> [!div class="step-by-step"]
> <span data-ttu-id="b1b68-237">[이전](mvc-music-store-part-2.md)
> [다음](mvc-music-store-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="b1b68-237">[Previous](mvc-music-store-part-2.md)
[Next](mvc-music-store-part-4.md)</span></span>
