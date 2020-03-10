---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-view
title: 뷰 추가 | Microsoft Docs
author: Rick-Anderson
description: 참고:이 자습서의 업데이트 된 버전은 ASP.NET MVC 5 및 Visual Studio 2013를 사용 하는 여기에서 사용할 수 있습니다. 보다 안전 하 고, 보다 간단 하 고 데모를 수행 하는 것이 더 간단 합니다.
ms.author: riande
ms.date: 08/28/2012
ms.assetid: dde851d7-882e-4d99-9b96-cf96daed81cc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: 81c2e1f46b08cbc9b5aa5d6c1b36d9d8dc2ba581
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485369"
---
# <a name="adding-a-view"></a><span data-ttu-id="46e16-104">보기 추가</span><span class="sxs-lookup"><span data-stu-id="46e16-104">Adding a View</span></span>

<span data-ttu-id="46e16-105">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="46e16-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="46e16-106">ASP.NET MVC 5와 Visual Studio 2013를 사용 하는이 자습서의 업데이트 된 버전 [을 사용할 수 있습니다.](../../getting-started/introduction/getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="46e16-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="46e16-107">더 안전 하 고 더 간단 하 고 더 많은 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="46e16-108">이 섹션에서는 뷰 템플릿 파일을 사용 하 여 클라이언트에 HTML 응답을 생성 하는 프로세스를 명확 하 게 캡슐화 하는 `HelloWorldController` 클래스를 수정 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-108">In this section you're going to modify the `HelloWorldController` class to use view template files to cleanly encapsulate the process of generating HTML responses to a client.</span></span>

<span data-ttu-id="46e16-109">ASP.NET MVC 3에 도입 된 [Razor 뷰 엔진](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx) 을 사용 하 여 뷰 템플릿 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-109">You'll create a view template file using the [Razor view engine](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx) introduced with ASP.NET MVC 3.</span></span> <span data-ttu-id="46e16-110">Razor 기반 뷰 템플릿에는 *. cshtml* 파일 확장명이 있으며을 사용 하 여 C#HTML 출력을 만드는 세련 된 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-110">Razor-based view templates have a *.cshtml* file extension, and provide an elegant way to create HTML output using C#.</span></span> <span data-ttu-id="46e16-111">Razor는 보기 템플릿을 작성할 때 필요한 문자 및 키 입력 수를 최소화 하 고 신속 하 고 유체 코딩 워크플로를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-111">Razor minimizes the number of characters and keystrokes required when writing a view template, and enables a fast, fluid coding workflow.</span></span>

<span data-ttu-id="46e16-112">현재 `Index` 메서드는 컨트롤러 클래스에서 하드 코딩된 메시지 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-112">Currently the `Index` method returns a string with a message that is hard-coded in the controller class.</span></span> <span data-ttu-id="46e16-113">다음 코드와 같이 `View` 개체를 반환 하도록 `Index` 메서드를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-113">Change the `Index` method to return a `View` object, as shown in the following code:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample1.cs)]

<span data-ttu-id="46e16-114">위의 `Index` 메서드는 뷰 템플릿을 사용 하 여 브라우저에 HTML 응답을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-114">The `Index` method above uses a view template to generate an HTML response to the browser.</span></span> <span data-ttu-id="46e16-115">위의 `Index` 메서드와 같은 컨트롤러 메서드 ( [동작 메서드](http://rachelappel.com/asp.net-mvc-actionresults-explained)라고도 함)는 일반적으로 문자열과 같은 기본 형식이 아닌 [actionresult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (또는 [actionresult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)에서 파생 된 클래스)를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-115">Controller methods (also known as [action methods](http://rachelappel.com/asp.net-mvc-actionresults-explained)), such as the `Index` method above, generally return an [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (or a class derived from [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)), not primitive types like string.</span></span>

<span data-ttu-id="46e16-116">프로젝트에서 `Index` 메서드와 함께 사용할 수 있는 뷰 템플릿을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-116">In the project, add a view template that you can use with the `Index` method.</span></span> <span data-ttu-id="46e16-117">이렇게 하려면 `Index` 메서드 내부를 마우스 오른쪽 단추로 클릭 하 고 **뷰 추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-117">To do this, right-click inside the `Index` method and click **Add View**.</span></span>

![](adding-a-view/_static/image1.png)

<span data-ttu-id="46e16-118">**뷰 추가** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-118">The **Add View** dialog box appears.</span></span> <span data-ttu-id="46e16-119">기본값을 그대로 두고 **추가** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-119">Leave the defaults the way they are and click the **Add** button:</span></span>

![](adding-a-view/_static/image2.png)

<span data-ttu-id="46e16-120">*MvcMovie\Views\HelloWorld* 폴더와 *MvcMovie\Views\HelloWorld\Index.cshtml* 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-120">The *MvcMovie\Views\HelloWorld* folder and the *MvcMovie\Views\HelloWorld\Index.cshtml* file are created.</span></span> <span data-ttu-id="46e16-121">**솔루션 탐색기**에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-121">You can see them in **Solution Explorer**:</span></span>

![](adding-a-view/_static/image3.png)

<span data-ttu-id="46e16-122">다음은 생성 된 *인덱스 cshtml* 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-122">The following shows the *Index.cshtml* file that was created:</span></span>

![HelloWorldIndex](adding-a-view/_static/image4.png)

<span data-ttu-id="46e16-124">`<h2>` 태그 아래에 다음 HTML을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-124">Add the following HTML under the `<h2>` tag.</span></span>

[!code-html[Main](adding-a-view/samples/sample2.html)]

<span data-ttu-id="46e16-125">전체 *MvcMovie\Views\HelloWorld\Index.cshtml* 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-125">The complete *MvcMovie\Views\HelloWorld\Index.cshtml* file is shown below.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml?highlight=7-8)]

<span data-ttu-id="46e16-126">Visual Studio 2012을 사용 하는 경우 솔루션 탐색기에서 *Index. cshtml* 파일을 마우스 오른쪽 단추로 클릭 하 고 **페이지 검사기에서 보기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-126">If you are using Visual Studio 2012, in solution explorer, right click the *Index.cshtml* file and select **View in Page Inspector**.</span></span>

![PI](adding-a-view/_static/image5.png)

<span data-ttu-id="46e16-128">[페이지 검사기 자습서](../../views/using-page-inspector-in-aspnet-mvc.md) 에는이 새 도구에 대 한 자세한 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-128">The [Page Inspector tutorial](../../views/using-page-inspector-in-aspnet-mvc.md) has more information about this new tool.</span></span>

<span data-ttu-id="46e16-129">또는 응용 프로그램을 실행 하 고 `HelloWorld` 컨트롤러 (`http://localhost:xxxx/HelloWorld`)로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-129">Alternatively, run the application and browse to the `HelloWorld` controller (`http://localhost:xxxx/HelloWorld`).</span></span> <span data-ttu-id="46e16-130">컨트롤러의 `Index` 메서드가 많은 작업을 수행 하지 않았습니다. 메서드는 뷰 템플릿 파일을 사용 하 여 브라우저에 응답을 렌더링 하도록 지정 하는 `return View()`문을 실행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-130">The `Index` method in your controller didn't do much work; it simply ran the statement `return View()`, which specified that the method should use a view template file to render a response to the browser.</span></span> <span data-ttu-id="46e16-131">사용할 뷰 템플릿 파일의 이름을 명시적으로 지정 하지 않았기 때문에 ASP.NET *MVC는* \Views\HelloWorld 폴더에 있는 폴더에서 기본적으로 폴더를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-131">Because you didn't explicitly specify the name of the view template file to use, ASP.NET MVC defaulted to using the *Index.cshtml* view file in the *\Views\HelloWorld* folder.</span></span> <span data-ttu-id="46e16-132">아래 이미지는 보기 템플릿의 문자열 &quot;Hello를 보여 줍니다. 뷰에 하드 코드 된&quot; 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-132">The image below shows the string &quot;Hello from our View Template!&quot; hard-coded in the view.</span></span>

![](adding-a-view/_static/image6.png)

<span data-ttu-id="46e16-133">매우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-133">Looks pretty good.</span></span> <span data-ttu-id="46e16-134">그러나 브라우저의 제목 표시줄에 ASP.NET A&quot; 인덱스 &quot;표시 되 고 페이지 맨 위에 있는 빅 링크에는 여기에 로고 &quot;표시 됩니다. 여기에서 로고 &quot;아래&quot; 합니다.&quot; 링크는 등록 및 로그인 링크 이며, 홈, 정보 및 연락처 페이지에 대 한 링크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-134">However, notice that the browser's title bar shows &quot;Index My ASP.NET A&quot; and the big link on the top of the page says &quot;your logo here.&quot; Below the &quot;your logo here.&quot; link are registration and log in links, and below that links to Home, About and Contact pages.</span></span> <span data-ttu-id="46e16-135">이러한 중 일부를 변경해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-135">Let's change some of these.</span></span>

## <a name="changing-views-and-layout-pages"></a><span data-ttu-id="46e16-136">보기 및 레이아웃 페이지 변경</span><span class="sxs-lookup"><span data-stu-id="46e16-136">Changing Views and Layout Pages</span></span>

<span data-ttu-id="46e16-137">먼저 여기에서 로고 &quot;를 변경 하려고 합니다. 페이지 맨 위에 제목을&quot; 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-137">First, you want to change the &quot;your logo here.&quot; title at the top of the page.</span></span> <span data-ttu-id="46e16-138">해당 텍스트는 모든 페이지에 공통적입니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-138">That text is common to every page.</span></span> <span data-ttu-id="46e16-139">응용 프로그램의 모든 페이지에 표시 되더라도 실제로는 프로젝트의 한 곳 에서만 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-139">It's actually implemented in only one place in the project, even though it appears on every page in the application.</span></span> <span data-ttu-id="46e16-140">**솔루션 탐색기** 의 */Views/Shared* 폴더로 이동 하 *\_Layout. cshtml* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-140">Go to the */Views/Shared* folder in **Solution Explorer** and open the *\_Layout.cshtml* file.</span></span> <span data-ttu-id="46e16-141">이 파일을 *레이아웃 페이지* 라고 하며 다른 모든 페이지에서 사용 하&quot; 공유 &quot;shell입니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-141">This file is called a *layout page* and it's the shared &quot;shell&quot; that all other pages use.</span></span>

![_LayoutCshtml](adding-a-view/_static/image7.png)

<span data-ttu-id="46e16-143">레이아웃 템플릿을 사용 하면 사이트의 HTML 컨테이너 레이아웃을 한 곳에서 지정한 다음 사이트의 여러 페이지에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-143">Layout templates allow you to specify the HTML container layout of your site in one place and then apply it across multiple pages in your site.</span></span> <span data-ttu-id="46e16-144">`@RenderBody()` 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-144">Find the `@RenderBody()` line.</span></span> <span data-ttu-id="46e16-145">`RenderBody`는 개발자가 만든 모든 보기 전용 페이지가 표시되는 자리 표시자이며 레이아웃 페이지으로 &quot;래핑됩니다&quot;.</span><span class="sxs-lookup"><span data-stu-id="46e16-145">`RenderBody` is a placeholder where all the view-specific pages you create show up, &quot;wrapped&quot; in the layout page.</span></span> <span data-ttu-id="46e16-146">예를 들어 About 링크를 선택 하는 경우 `RenderBody` 메서드 내에 *Views\Home\About.cshtml* 뷰가 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-146">For example, if you select the About link, the *Views\Home\About.cshtml* view is rendered inside the `RenderBody` method.</span></span>

<span data-ttu-id="46e16-147">레이아웃 템플릿의 사이트 제목 머리글을 &quot;&quot; 로고에서 &quot;MVC Movie&quot;로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-147">Change the site-title heading in the layout template from &quot;your logo here&quot; to &quot;MVC Movie&quot;.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

<span data-ttu-id="46e16-148">Title 요소의 내용을 다음 태그로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-148">Replace the contents of the title element with the following markup:</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml)]

<span data-ttu-id="46e16-149">응용 프로그램을 실행 하 고 &quot;MVC Movie &quot;를 표시 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-149">Run the application and notice that it now says &quot;MVC Movie &quot;.</span></span> <span data-ttu-id="46e16-150">**About** 링크를 클릭 하면 해당 페이지에 MVC Movie&quot;&quot;표시 되는 방식이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-150">Click the **About** link, and you see how that page shows &quot;MVC Movie&quot;, too.</span></span> <span data-ttu-id="46e16-151">레이아웃 템플릿을 한 번 변경 하 고 사이트의 모든 페이지에 새 제목을 반영할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-151">We were able to make the change once in the layout template and have all pages on the site reflect the new title.</span></span>

![](adding-a-view/_static/image8.png)

<span data-ttu-id="46e16-152">이제 인덱스 뷰의 제목을 변경 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-152">Now, let's change the title of the Index view.</span></span>

<span data-ttu-id="46e16-153">*MvcMovie\Views\HelloWorld\Index.cshtml*를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-153">Open *MvcMovie\Views\HelloWorld\Index.cshtml*.</span></span> <span data-ttu-id="46e16-154">변경 하는 데는 두 가지 위치가 있습니다. 첫 번째는 브라우저의 제목에 표시 되는 텍스트이 고, 그 다음에는 보조 헤더 (`<h2>` 요소)에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-154">There are two places to make a change: first, the text that appears in the title of the browser, and then in the secondary header (the `<h2>` element).</span></span> <span data-ttu-id="46e16-155">어떤 코드에서 어떤 앱의 부분을 변경하는지 볼 수 있도록 약간 다르게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-155">You'll make them slightly different so you can see which bit of code changes which part of the app.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample6.cshtml)]

<span data-ttu-id="46e16-156">표시할 HTML 제목을 나타내려면 위의 코드는 `ViewBag` 개체의 `Title` 속성을 설정 합니다 ( *인덱스. cshtml* 뷰 템플릿).</span><span class="sxs-lookup"><span data-stu-id="46e16-156">To indicate the HTML title to display, the code above sets a `Title` property of the `ViewBag` object (which is in the *Index.cshtml* view template).</span></span> <span data-ttu-id="46e16-157">레이아웃 템플릿의 소스 코드를 다시 살펴보면 템플릿에서 `<title>` 요소의이 값을 이전에 수정한 HTML의 `<head>` 섹션의 일부로 사용 하는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-157">If you look back at the source code of the layout template, you'll notice that the template uses this value in the `<title>` element as part of the `<head>` section of the HTML that we modified previously.</span></span> <span data-ttu-id="46e16-158">이 `ViewBag` 방법을 사용 하면 보기 템플릿과 레이아웃 파일 사이에 다른 매개 변수를 쉽게 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-158">Using this `ViewBag` approach, you can easily pass other parameters between your view template and your layout file.</span></span>

<span data-ttu-id="46e16-159">응용 프로그램을 실행 하 고 `http://localhost:xx/HelloWorld`로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-159">Run the application and browse to `http://localhost:xx/HelloWorld`.</span></span> <span data-ttu-id="46e16-160">브라우저 제목, 기본 제목 및 작은 제목이 변경된 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-160">Notice that the browser title, the primary heading, and the secondary headings have changed.</span></span> <span data-ttu-id="46e16-161">(브라우저에서 변경 내용을 확인할 수 없는 경우 캐시된 콘텐츠를 보고 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-161">(If you don't see changes in the browser, you might be viewing cached content.</span></span> <span data-ttu-id="46e16-162">브라우저에서 Ctrl + F5 키를 눌러 서버의 응답을 강제로 로드 합니다. 브라우저 제목은 인덱스에 설정 된 `ViewBag.Title`를 사용 하 여 만들어지며, 레이아웃 파일에 추가 &quot;동영상 앱&quot; 추가 됩니다 *.*</span><span class="sxs-lookup"><span data-stu-id="46e16-162">Press Ctrl+F5 in your browser to force the response from the server to be loaded.) The browser title is created with the `ViewBag.Title` we set in the *Index.cshtml* view template and the additional &quot;- Movie App&quot; added in the layout file.</span></span>

<span data-ttu-id="46e16-163">또한 *Index. cshtml* 뷰 템플릿의 콘텐츠가\_레이아웃과 병합 되었는지 확인 *합니다. cshtml* 뷰 템플릿과 단일 HTML 응답이 브라우저에 전송 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-163">Also notice how the content in the *Index.cshtml* view template was merged with the *\_Layout.cshtml* view template and a single HTML response was sent to the browser.</span></span> <span data-ttu-id="46e16-164">레이아웃 템플릿을 사용하면 애플리케이션의 모든 페이지에 걸쳐 적용되는 변경 내용을 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-164">Layout templates make it really easy to make changes that apply across all of the pages in your application.</span></span>

![](adding-a-view/_static/image9.png)

<span data-ttu-id="46e16-165">약간의 &quot;데이터&quot; (이 경우 보기 템플릿!&quot; 메시지의 Hello &quot;)는 하드 코드 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-165">Our little bit of &quot;data&quot; (in this case the &quot;Hello from our View Template!&quot; message) is hard-coded, though.</span></span> <span data-ttu-id="46e16-166">MVC 응용 프로그램에는 &quot;V&quot; (보기)가 있으며 &quot;C&quot; (컨트롤러)가 있지만 &quot;M&quot; (모델)은 아직 없습니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-166">The MVC application has a &quot;V&quot; (view) and you've got a &quot;C&quot; (controller), but no &quot;M&quot; (model) yet.</span></span> <span data-ttu-id="46e16-167">잠시 후 데이터베이스를 만들고 해당 데이터베이스에서 모델 데이터를 검색 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-167">Shortly, we'll walk through how create a database and retrieve model data from it.</span></span>

## <a name="passing-data-from-the-controller-to-the-view"></a><span data-ttu-id="46e16-168">컨트롤러에서 보기로 데이터 전달</span><span class="sxs-lookup"><span data-stu-id="46e16-168">Passing Data from the Controller to the View</span></span>

<span data-ttu-id="46e16-169">데이터베이스로 이동 하 여 모델에 대해 이야기 하기 전에 먼저 컨트롤러에서 뷰로 정보를 전달 하는 방법에 대해 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-169">Before we go to a database and talk about models, though, let's first talk about passing information from the controller to a view.</span></span> <span data-ttu-id="46e16-170">컨트롤러 클래스는 들어오는 URL 요청에 대 한 응답으로 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-170">Controller classes are invoked in response to an incoming URL request.</span></span> <span data-ttu-id="46e16-171">컨트롤러 클래스는 들어오는 브라우저 요청을 처리 하는 코드를 작성 하 고, 데이터베이스에서 데이터를 검색 하 고, 궁극적으로 브라우저에 다시 보낼 응답 유형을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-171">A controller class is where you write the code that handles the incoming browser requests, retrieves data from a database, and ultimately decides what type of response to send back to the browser.</span></span> <span data-ttu-id="46e16-172">그러면 컨트롤러에서 뷰 템플릿을 사용 하 여 브라우저에 HTML 응답을 생성 하 고 서식을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-172">View templates can then be used from a controller to generate and format an HTML response to the browser.</span></span>

<span data-ttu-id="46e16-173">컨트롤러는 뷰 템플릿이 브라우저에 응답을 렌더링 하는 데 필요한 모든 데이터 또는 개체를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-173">Controllers are responsible for providing whatever data or objects are required in order for a view template to render a response to the browser.</span></span> <span data-ttu-id="46e16-174">모범 사례: **뷰 템플릿은 비즈니스 논리를 수행 하거나 데이터베이스와 직접 상호 작용 하지 않아야**합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-174">A best practice: **A view template should never perform business logic or interact with a database directly**.</span></span> <span data-ttu-id="46e16-175">대신, 뷰 템플릿은 컨트롤러에서 제공 하는 데이터에 대해서만 작동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-175">Instead, a view template should work only with the data that's provided to it by the controller.</span></span> <span data-ttu-id="46e16-176">이러한 &quot;&quot; 문제를 분리 하면 코드를 정리 하 고, 테스트 가능 하 고, 유지 관리 하기 쉽게 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-176">Maintaining this &quot;separation of concerns&quot; helps keep your code clean, testable and more maintainable.</span></span>

<span data-ttu-id="46e16-177">현재 `HelloWorldController` 클래스의 `Welcome` 작업 메서드는 `name` 및 `numTimes` 매개 변수를 사용 하 여 브라우저에 직접 값을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-177">Currently, the `Welcome` action method in the `HelloWorldController` class takes a `name` and a `numTimes` parameter and then outputs the values directly to the browser.</span></span> <span data-ttu-id="46e16-178">컨트롤러에서이 응답을 문자열로 렌더링 하 게 하는 대신 뷰 템플릿을 사용 하도록 컨트롤러를 변경 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-178">Rather than have the controller render this response as a string, let's change the controller to use a view template instead.</span></span> <span data-ttu-id="46e16-179">보기 템플릿은 동적 응답을 생성합니다. 즉, 응답을 생성하기 위해 컨트롤러에서 보기로 일부 적절한 데이터를 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-179">The view template will generate a dynamic response, which means that you need to pass appropriate bits of data from the controller to the view in order to generate the response.</span></span> <span data-ttu-id="46e16-180">이렇게 하려면 컨트롤러에서 뷰 템플릿이 액세스할 수 있는 `ViewBag` 개체에 필요한 동적 데이터 (매개 변수)를 배치 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-180">You can do this by having the controller put the dynamic data (parameters) that the view template needs in a `ViewBag` object that the view template can then access.</span></span>

<span data-ttu-id="46e16-181">*HelloWorldController.cs* 파일로 돌아가서 `Welcome` 메서드를 변경 하 여 `Message` 및 `NumTimes` 값을 `ViewBag` 개체에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-181">Return to the *HelloWorldController.cs* file and change the `Welcome` method to add a `Message` and `NumTimes` value to the `ViewBag` object.</span></span> <span data-ttu-id="46e16-182">`ViewBag`는 동적 개체입니다. 즉, 원하는 모든 항목을 배치할 수 있습니다. `ViewBag` 개체 안에 항목을 넣을 때까지 정의 된 속성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-182">`ViewBag` is a dynamic object, which means you can put whatever you want in to it; the `ViewBag` object has no defined properties until you put something inside it.</span></span> <span data-ttu-id="46e16-183">[ASP.NET MVC 모델 바인딩 시스템](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) 은 주소 표시줄의 쿼리 문자열에서 메서드의 매개 변수로 명명 된 매개 변수 (`name` 및 `numTimes`)를 자동으로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-183">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters (`name` and `numTimes`) from the query string in the address bar to parameters in your method.</span></span> <span data-ttu-id="46e16-184">전체 *HelloWorldController.cs* 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-184">The complete *HelloWorldController.cs* file looks like this:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample7.cs)]

<span data-ttu-id="46e16-185">이제 `ViewBag` 개체는 뷰에 자동으로 전달 되는 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-185">Now the `ViewBag` object contains data that will be passed to the view automatically.</span></span>

<span data-ttu-id="46e16-186">다음으로 시작 보기 템플릿이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-186">Next, you need a Welcome view template!</span></span> <span data-ttu-id="46e16-187">**빌드** 메뉴에서 **mvcmovie 빌드** 를 선택 하 여 프로젝트가 컴파일되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-187">In the **Build** menu, select **Build MvcMovie** to make sure the project is compiled.</span></span>

<span data-ttu-id="46e16-188">그런 다음 `Welcome` 메서드 내부를 마우스 오른쪽 단추로 클릭 하 고 **뷰 추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-188">Then right-click inside the `Welcome` method and click **Add View**.</span></span>

![](adding-a-view/_static/image10.png)

<span data-ttu-id="46e16-189">**보기 추가** 대화 상자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-189">Here's what the **Add View** dialog box looks like:</span></span>

![](adding-a-view/_static/image11.png)

<span data-ttu-id="46e16-190">**추가**를 클릭 한 후 새 *시작 cshtml* 파일의 `<h2>` 요소 아래에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-190">Click **Add**, and then add the following code under the `<h2>` element in the new *Welcome.cshtml* file.</span></span> <span data-ttu-id="46e16-191">사용자에 게 표시 되는 횟수 만큼 Hello&quot; &quot;표시 하는 루프를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-191">You'll create a loop that says &quot;Hello&quot; as many times as the user says it should.</span></span> <span data-ttu-id="46e16-192">전체 *시작. cshtml* 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-192">The complete *Welcome.cshtml* file is shown below.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample8.cshtml)]

<span data-ttu-id="46e16-193">응용 프로그램을 실행 하 고 다음 URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-193">Run the application and browse to the following URL:</span></span>

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

<span data-ttu-id="46e16-194">이제 데이터가 URL에서 가져온 후 [모델 바인더](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)를 사용 하 여 컨트롤러에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-194">Now data is taken from the URL and passed to the controller using the [model binder](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx).</span></span> <span data-ttu-id="46e16-195">컨트롤러는 데이터를 `ViewBag` 개체에 패키지 하 고 해당 개체를 뷰에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-195">The controller packages the data into a `ViewBag` object and passes that object to the view.</span></span> <span data-ttu-id="46e16-196">그런 다음 보기는 사용자에 게 데이터를 HTML로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-196">The view then displays the data as HTML to the user.</span></span>

![](adding-a-view/_static/image12.png)

<span data-ttu-id="46e16-197">위의 샘플에서는 `ViewBag` 개체를 사용 하 여 컨트롤러에서 뷰로 데이터를 전달 했습니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-197">In the sample above, we used a `ViewBag` object to pass data from the controller to a view.</span></span> <span data-ttu-id="46e16-198">자습서의 뒷부분에서는 뷰 모델을 사용 하 여 컨트롤러에서 뷰로 데이터를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-198">Latter in the tutorial, we will use a view model to pass data from a controller to a view.</span></span> <span data-ttu-id="46e16-199">데이터 전달에 대 한 뷰 모델 접근 방식은 일반적으로 보기 모음 접근 방법 보다 훨씬 선호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-199">The view model approach to passing data is generally much preferred over the view bag approach.</span></span> <span data-ttu-id="46e16-200">자세한 내용은 블로그 항목 [동적 V 강력한 형식의 뷰](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="46e16-200">See the blog entry [Dynamic V Strongly Typed Views](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) for more information.</span></span>

<span data-ttu-id="46e16-201">모델에 대 한 &quot;M&quot;의 일종 이지만 데이터베이스 종류는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-201">Well, that was a kind of an &quot;M&quot; for model, but not the database kind.</span></span> <span data-ttu-id="46e16-202">지금까지 학습한 것을 살펴보고 동영상의 데이터베이스를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="46e16-202">Let's take what we've learned and create a database of movies.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="46e16-203">[이전](adding-a-controller.md)
> [다음](adding-a-model.md)</span><span class="sxs-lookup"><span data-stu-id="46e16-203">[Previous](adding-a-controller.md)
[Next](adding-a-model.md)</span></span>
