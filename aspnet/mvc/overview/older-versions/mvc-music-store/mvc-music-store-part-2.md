---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
title: '2 부: 컨트롤러 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 2 부에서는 컨트롤러를 다룹니다.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 998ce4e1-9d72-435b-8f1c-399a10ae4360
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
msc.type: authoredcontent
ms.openlocfilehash: 9dc2226f4951d4bed122df37d35bbb94730a00ad
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451193"
---
# <a name="part-2-controllers"></a><span data-ttu-id="9ba69-104">2 부: 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="9ba69-104">Part 2: Controllers</span></span>

<span data-ttu-id="9ba69-105">받은 사람 ( [Jon Galloway](https://github.com/jongalloway) )</span><span class="sxs-lookup"><span data-stu-id="9ba69-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="9ba69-106">MVC Music Store는 웹 개발용 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 소개 하 고 설명 하는 자습서 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="9ba69-107">MVC Music Store는 온라인으로 음악 앨범을 판매 하 고 기본적인 사이트 관리, 사용자 로그인 및 쇼핑 카트 기능을 구현 하는 간단한 샘플 저장소 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="9ba69-108">이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="9ba69-109">2 부에서는 컨트롤러를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-109">Part 2 covers Controllers.</span></span>

<span data-ttu-id="9ba69-110">기존 웹 프레임 워크를 사용 하는 경우 들어오는 Url은 일반적으로 디스크의 파일에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-110">With traditional web frameworks, incoming URLs are typically mapped to files on disk.</span></span> <span data-ttu-id="9ba69-111">예: "/Products.aspx" 또는 "/Products.php"와 같은 URL에 대 한 요청은 "" 또는 "" 파일에 의해 처리 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-111">For example: a request for a URL like "/Products.aspx" or "/Products.php" might be processed by a "Products.aspx" or "Products.php" file.</span></span>

<span data-ttu-id="9ba69-112">웹 기반 MVC 프레임 워크는 Url을 서버 코드에 약간 다른 방식으로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-112">Web-based MVC frameworks map URLs to server code in a slightly different way.</span></span> <span data-ttu-id="9ba69-113">들어오는 Url을 파일에 매핑하는 대신, 해당 url을 클래스의 메서드에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-113">Instead of mapping incoming URLs to files, they instead map URLs to methods on classes.</span></span> <span data-ttu-id="9ba69-114">이러한 클래스를 "컨트롤러" 라고 하며, 들어오는 HTTP 요청을 처리 하 고, 사용자 입력을 처리 하 고, 데이터를 검색 및 저장 하 고, 클라이언트로 다시 보낼 응답을 결정 합니다 (HTML 표시, 파일 다운로드, 다른 위치로 리디렉션). URL 등).</span><span class="sxs-lookup"><span data-stu-id="9ba69-114">These classes are called "Controllers" and they are responsible for processing incoming HTTP requests, handling user input, retrieving and saving data, and determining the response to send back to the client (display HTML, download a file, redirect to a different URL, etc.).</span></span>

## <a name="adding-a-homecontroller"></a><span data-ttu-id="9ba69-115">HomeController 추가</span><span class="sxs-lookup"><span data-stu-id="9ba69-115">Adding a HomeController</span></span>

<span data-ttu-id="9ba69-116">사이트의 홈 페이지에 대 한 Url을 처리 하는 컨트롤러 클래스를 추가 하 여 MVC Music Store 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-116">We'll begin our MVC Music Store application by adding a Controller class that will handle URLs to the Home page of our site.</span></span> <span data-ttu-id="9ba69-117">ASP.NET MVC의 기본 명명 규칙을 따르고 HomeController를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-117">We'll follow the default naming conventions of ASP.NET MVC and call it HomeController.</span></span>

<span data-ttu-id="9ba69-118">솔루션 탐색기 내의 "컨트롤러" 폴더를 마우스 오른쪽 단추로 클릭 하 고 "추가"를 선택 하 고 "컨트롤러 ..."를 선택 합니다. 명령</span><span class="sxs-lookup"><span data-stu-id="9ba69-118">Right-click the "Controllers" folder within the Solution Explorer and select "Add", and then the "Controller…" command:</span></span>

![](mvc-music-store-part-2/_static/image1.jpg)

<span data-ttu-id="9ba69-119">그러면 "컨트롤러 추가" 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-119">This will bring up the "Add Controller" dialog.</span></span> <span data-ttu-id="9ba69-120">컨트롤러 이름을 "HomeController"로 하 고 추가 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-120">Name the controller "HomeController" and press the Add button.</span></span>

![](mvc-music-store-part-2/_static/image1.png)

<span data-ttu-id="9ba69-121">그러면 다음 코드를 사용 하 여 새 파일인 HomeController.cs가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-121">This will create a new file, HomeController.cs, with the following code:</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample1.cs)]

<span data-ttu-id="9ba69-122">가능한 한 간단 하 게 시작 하려면 Index 메서드를 단순히 문자열만 반환 하는 간단한 메서드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-122">To start as simply as possible, let's replace the Index method with a simple method that just returns a string.</span></span> <span data-ttu-id="9ba69-123">다음 두 가지 변경 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-123">We'll make two changes:</span></span>

- <span data-ttu-id="9ba69-124">메서드를 변경 하 여 ActionResult 대신 문자열 반환</span><span class="sxs-lookup"><span data-stu-id="9ba69-124">Change the method to return a string instead of an ActionResult</span></span>
- <span data-ttu-id="9ba69-125">Return 문을 변경 하 여 "Hello from Home"을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-125">Change the return statement to return "Hello from Home"</span></span>

<span data-ttu-id="9ba69-126">이제 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-126">The method should now look like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample2.cs)]

## <a name="running-the-application"></a><span data-ttu-id="9ba69-127">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="9ba69-127">Running the Application</span></span>

<span data-ttu-id="9ba69-128">이제 사이트를 실행 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-128">Now let's run the site.</span></span> <span data-ttu-id="9ba69-129">웹 서버를 시작 하 고 다음 중 하나를 사용 하 여 사이트를 사용해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-129">We can start our web-server and try out the site using any of the following::</span></span>

- <span data-ttu-id="9ba69-130">디버그 ⇨ 디버깅 시작 메뉴 항목을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-130">Choose the Debug ⇨ Start Debugging menu item</span></span>
- <span data-ttu-id="9ba69-131">도구 모음에서 녹색 화살표 단추를 클릭 ![](mvc-music-store-part-2/_static/image2.jpg)</span><span class="sxs-lookup"><span data-stu-id="9ba69-131">Click the Green arrow button in the toolbar ![](mvc-music-store-part-2/_static/image2.jpg)</span></span>
- <span data-ttu-id="9ba69-132">키보드 바로 가기 인 F5 키를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-132">Use the keyboard shortcut, F5.</span></span>

<span data-ttu-id="9ba69-133">위의 단계를 사용 하 여 프로젝트를 컴파일한 다음 Visual Web Developer에 기본 제공 되는 ASP.NET 개발 서버를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-133">Using any of the above steps will compile our project, and then cause the ASP.NET Development Server that is built-into Visual Web Developer to start.</span></span> <span data-ttu-id="9ba69-134">화면 하단에 ASP.NET 개발 서버 시작 됨을 나타내는 알림이 표시 되 고 실행 중인 포트 번호가 표시 됩니다 ().</span><span class="sxs-lookup"><span data-stu-id="9ba69-134">A notification will appear in the bottom corner of the screen to indicate that the ASP.NET Development Server has started up, and will show the port number that it is running under.</span></span>

![](mvc-music-store-part-2/_static/image2.png)

<span data-ttu-id="9ba69-135">그러면 Visual Web Developer에서 웹 서버를 가리키는 URL이 있는 브라우저 창을 자동으로 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-135">Visual Web Developer will then automatically open a browser window whose URL points to our web-server.</span></span> <span data-ttu-id="9ba69-136">이렇게 하면 웹 응용 프로그램을 빠르게 사용해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-136">This will allow us to quickly try out our web application:</span></span>

![](mvc-music-store-part-2/_static/image3.png)

<span data-ttu-id="9ba69-137">괜찮습니다 .이는 새로운 웹 사이트를 만들고, 세 개의 선 함수를 추가 했으며, 브라우저에서 텍스트를 얻었습니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-137">Okay, that was pretty quick – we created a new website, added a three line function, and we've got text in a browser.</span></span> <span data-ttu-id="9ba69-138">로켓 과학은 아니지만 시작입니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-138">Not rocket science, but it's a start.</span></span>

<span data-ttu-id="9ba69-139">*참고: Visual Web Developer에는 웹 사이트를 실행 하는 ASP.NET 개발 서버 포함 되어 있습니다. 위의 스크린샷에는 사이트가 `http://localhost:26641/`에서 실행 되므로 포트 26641를 사용 합니다. 포트 번호는 다를 수 있습니다. 이 자습서에서 URL과 같은 URL의 예를 보면 포트 번호 다음에 표시 됩니다. 포트 번호가 26641 인 것으로 가정 하 고/Sv/svto 찾아보기로 이동 하면 `http://localhost:26641/Store/Browse`검색을 의미 합니다.*</span><span class="sxs-lookup"><span data-stu-id="9ba69-139">*Note: Visual Web Developer includes the ASP.NET Development Server, which will run your website on a random free "port" number. In the screenshot above, the site is running at `http://localhost:26641/`, so it's using port 26641. Your port number will be different. When we talk about URL's like /Store/Browse in this tutorial, that will go after the port number. Assuming a port number of 26641, browsing to /Store/Browse will mean browsing to `http://localhost:26641/Store/Browse`.*</span></span>

## <a name="adding-a-storecontroller"></a><span data-ttu-id="9ba69-140">StoreController 추가</span><span class="sxs-lookup"><span data-stu-id="9ba69-140">Adding a StoreController</span></span>

<span data-ttu-id="9ba69-141">사이트의 홈 페이지를 구현 하는 간단한 HomeController를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-141">We added a simple HomeController that implements the Home Page of our site.</span></span> <span data-ttu-id="9ba69-142">이제 music store의 검색 기능을 구현 하는 데 사용할 다른 컨트롤러를 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-142">Let's now add another controller that we'll use to implement the browsing functionality of our music store.</span></span> <span data-ttu-id="9ba69-143">저장소 컨트롤러는 세 가지 시나리오를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-143">Our store controller will support three scenarios:</span></span>

- <span data-ttu-id="9ba69-144">Music store의 음악 장르 목록 페이지</span><span class="sxs-lookup"><span data-stu-id="9ba69-144">A listing page of the music genres in our music store</span></span>
- <span data-ttu-id="9ba69-145">특정 장르의 모든 음악 앨범을 나열 하는 찾아보기 페이지</span><span class="sxs-lookup"><span data-stu-id="9ba69-145">A browse page that lists all of the music albums in a particular genre</span></span>
- <span data-ttu-id="9ba69-146">특정 음악 앨범에 대 한 정보를 표시 하는 세부 정보 페이지</span><span class="sxs-lookup"><span data-stu-id="9ba69-146">A details page that shows information about a specific music album</span></span>

<span data-ttu-id="9ba69-147">새 StoreController 클래스를 추가 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-147">We'll start by adding a new StoreController class..</span></span> <span data-ttu-id="9ba69-148">아직 실행 하지 않은 경우 브라우저를 닫거나 디버그 ⇨ 디버깅 중지 메뉴 항목을 선택 하 여 응용 프로그램 실행을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-148">If you haven't already, stop running the application either by closing the browser or selecting the Debug ⇨ Stop Debugging menu item.</span></span>

<span data-ttu-id="9ba69-149">이제 새 StoreController를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-149">Now add a new StoreController.</span></span> <span data-ttu-id="9ba69-150">HomeController를 사용 하는 것 처럼 솔루션 탐색기 내에서 "컨트롤러" 폴더를 마우스 오른쪽 단추로 클릭 하 고 추가&gt;컨트롤러 메뉴 항목을 선택 하 여이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-150">Just like we did with HomeController, we'll do this by right-clicking on the "Controllers" folder within the Solution Explorer and choosing the Add-&gt;Controller menu item</span></span>

![](mvc-music-store-part-2/_static/image4.png)

<span data-ttu-id="9ba69-151">새 StoreController에는 이미 "Index" 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-151">Our new StoreController already has an "Index" method.</span></span> <span data-ttu-id="9ba69-152">이 "인덱스" 메서드를 사용 하 여 음악 스토어의 모든 장르를 나열 하는 목록 페이지를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-152">We'll use this "Index" method to implement our listing page that lists all genres in our music store.</span></span> <span data-ttu-id="9ba69-153">또한 StoreController에서 처리할 두 가지 다른 시나리오를 구현 하는 두 가지 메서드를 더 추가 하 여 찾아보기 및 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-153">We'll also add two additional methods to implement the two other scenarios we want our StoreController to handle: Browse and Details.</span></span>

<span data-ttu-id="9ba69-154">컨트롤러 내에서 이러한 메서드 (인덱스, 찾아보기 및 세부 정보)를 "컨트롤러 작업" 이라고 하며, 이미 HomeController () 작업 메서드를 사용 하는 경우 URL 요청에 응답 하 고 (일반적으로) 콘텐츠를 결정 하는 작업입니다. URL을 호출한 브라우저 또는 사용자에 게 다시 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-154">These methods (Index, Browse and Details) within our Controller are called "Controller Actions", and as you've already seen with the HomeController.Index()action method, their job is to respond to URL requests and (generally speaking) determine what content should be sent back to the browser or user that invoked the URL.</span></span>

<span data-ttu-id="9ba69-155">Index () 메서드를 변경 하 여 "Hello from StoreController ()" 라는 문자열을 반환 하 고 Browse () 및 Details ()에 대해 비슷한 메서드를 추가 하 여 구현을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-155">We'll start our StoreController implementation by changing theIndex() method to return the string "Hello from Store.Index()" and we'll add similar methods for Browse() and Details():</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample3.cs)]

<span data-ttu-id="9ba69-156">프로젝트를 다시 실행 하 고 다음 Url을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-156">Run the project again and browse the following URLs:</span></span>

- <span data-ttu-id="9ba69-157">/Store</span><span class="sxs-lookup"><span data-stu-id="9ba69-157">/Store</span></span>
- <span data-ttu-id="9ba69-158">/Sver/찾아보기</span><span class="sxs-lookup"><span data-stu-id="9ba69-158">/Store/Browse</span></span>
- <span data-ttu-id="9ba69-159">/Sv/ds/세부 정보</span><span class="sxs-lookup"><span data-stu-id="9ba69-159">/Store/Details</span></span>

<span data-ttu-id="9ba69-160">이러한 Url에 액세스 하면 컨트롤러 내에서 작업 메서드를 호출 하 고 문자열 응답을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-160">Accessing these URLs will invoke the action methods within our Controller and return string responses:</span></span>

![](mvc-music-store-part-2/_static/image5.png)

<span data-ttu-id="9ba69-161">매우 유용 하지만 상수 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-161">That's great, but these are just constant strings.</span></span> <span data-ttu-id="9ba69-162">동적으로 만들어 URL에서 정보를 가져와 페이지 출력에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-162">Let's make them dynamic, so they take information from the URL and display it in the page output.</span></span>

<span data-ttu-id="9ba69-163">먼저 찾아보기 동작 메서드를 변경 하 여 URL에서 querystring 값을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-163">First we'll change the Browse action method to retrieve a querystring value from the URL.</span></span> <span data-ttu-id="9ba69-164">작업 메서드에 "장르" 매개 변수를 추가 하 여이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-164">We can do this by adding a "genre" parameter to our action method.</span></span> <span data-ttu-id="9ba69-165">이 작업을 수행 하면 ASP.NET MVC가 호출 될 때 작업 메서드에 "장르" 라는 쿼리 문자열 또는 폼 게시 매개 변수를 자동으로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-165">When we do this ASP.NET MVC will automatically pass any querystring or form post parameters named "genre" to our action method when it is invoked.</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample4.cs)]

<span data-ttu-id="9ba69-166">*참고: HtmlEncode 유틸리티 메서드를 사용 하 여 사용자 입력을 삭제 합니다. 이를 통해 사용자는/Vv/dher>와 같은 링크를 사용 하 여 Javascript를 뷰에 삽입할 수 없습니다. 장르 =&lt;스크립트&gt;창. location = 'http://hackersite.com'&lt;/script&gt;.*</span><span class="sxs-lookup"><span data-stu-id="9ba69-166">*Note: We're using the HttpUtility.HtmlEncode utility method to sanitize the user input. This prevents users from injecting Javascript into our View with a link like /Store/Browse?Genre=&lt;script&gt;window.location='http://hackersite.com'&lt;/script&gt;.*</span></span>

<span data-ttu-id="9ba69-167">이제/Dv>로 이동 하겠습니다. 장르 = Disco</span><span class="sxs-lookup"><span data-stu-id="9ba69-167">Now let's browse to /Store/Browse?Genre=Disco</span></span>

![](mvc-music-store-part-2/_static/image6.png)

<span data-ttu-id="9ba69-168">다음으로 자세히 작업을 변경 하 여 ID 라는 입력 매개 변수를 읽고 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-168">Let's next change the Details action to read and display an input parameter named ID.</span></span> <span data-ttu-id="9ba69-169">이전 메서드와 달리 ID 값을 querystring 매개 변수로 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-169">Unlike our previous method, we won't be embedding the ID value as a querystring parameter.</span></span> <span data-ttu-id="9ba69-170">대신 URL 자체에 직접 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-170">Instead we'll embed it directly within the URL itself.</span></span> <span data-ttu-id="9ba69-171">예:/Store/Details/5.</span><span class="sxs-lookup"><span data-stu-id="9ba69-171">For example: /Store/Details/5.</span></span>

<span data-ttu-id="9ba69-172">ASP.NET MVC를 사용 하면 아무것도 구성 하지 않고도이 작업을 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-172">ASP.NET MVC lets us easily do this without having to configure anything.</span></span> <span data-ttu-id="9ba69-173">ASP.NET MVC의 기본 라우팅 규칙은 작업 메서드 이름 뒤에 있는 URL의 세그먼트를 "ID" 라는 매개 변수로 처리 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-173">ASP.NET MVC's default routing convention is to treat the segment of a URL after the action method name as a parameter named "ID".</span></span> <span data-ttu-id="9ba69-174">작업 메서드에 ID 라는 매개 변수가 있는 경우 ASP.NET MVC는 자동으로 URL 세그먼트를 매개 변수로 사용자에 게 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-174">If your action method has a parameter named ID then ASP.NET MVC will automatically pass the URL segment to you as a parameter.</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample5.cs)]

<span data-ttu-id="9ba69-175">응용 프로그램을 실행 하 고/Store/Details/5로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-175">Run the application and browse to /Store/Details/5:</span></span>

![](mvc-music-store-part-2/_static/image7.png)

<span data-ttu-id="9ba69-176">지금까지 수행한 작업을 간략하게 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-176">Let's recap what we've done so far:</span></span>

- <span data-ttu-id="9ba69-177">Visual Web Developer에서 새로운 ASP.NET MVC 프로젝트를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-177">We've created a new ASP.NET MVC project in Visual Web Developer</span></span>
- <span data-ttu-id="9ba69-178">ASP.NET MVC 응용 프로그램의 기본 폴더 구조에 대해 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-178">We've discussed the basic folder structure of an ASP.NET MVC application</span></span>
- <span data-ttu-id="9ba69-179">ASP.NET 개발 서버를 사용 하 여 웹 사이트를 실행 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-179">We've learned how to run our website using the ASP.NET Development Server</span></span>
- <span data-ttu-id="9ba69-180">HomeController 및 StoreController 라는 두 개의 컨트롤러 클래스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-180">We've created two Controller classes: a HomeController and a StoreController</span></span>
- <span data-ttu-id="9ba69-181">URL 요청에 응답 하 고 브라우저에 텍스트를 반환 하는 작업 메서드를 컨트롤러에 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="9ba69-181">We've added Action Methods to our controllers which respond to URL requests and return text to the browser</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9ba69-182">[이전](mvc-music-store-part-1.md)
> [다음](mvc-music-store-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="9ba69-182">[Previous](mvc-music-store-part-1.md)
[Next](mvc-music-store-part-3.md)</span></span>
