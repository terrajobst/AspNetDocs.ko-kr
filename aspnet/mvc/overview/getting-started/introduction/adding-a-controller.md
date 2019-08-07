---
uid: mvc/overview/getting-started/introduction/adding-a-controller
title: 컨트롤러 추가 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: cc764f3b-6921-486a-8f44-c6ccd1249acd
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 6b38d757d37374b14979f8a079a46158ff64f9c3
ms.sourcegitcommit: f774732a3960fca079438a88a5472c37cf7be08a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2019
ms.locfileid: "68810769"
---
# <a name="adding-a-controller"></a><span data-ttu-id="5d085-102">컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="5d085-102">Adding a Controller</span></span>

<span data-ttu-id="5d085-103">[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="5d085-103">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

[!INCLUDE [Tutorial Note](sample/code-location.md)]

<span data-ttu-id="5d085-104">MVC는 *모델-뷰-컨트롤러*를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-104">MVC stands for *model-view-controller*.</span></span> <span data-ttu-id="5d085-105">MVC는 잘 설계 되 고, 테스트 가능 하 고, 유지 관리 하기 쉬운 응용 프로그램을 개발 하기 위한 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-105">MVC is a pattern for developing applications that are well architected, testable and easy to maintain.</span></span> <span data-ttu-id="5d085-106">MVC 기반 응용 프로그램에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-106">MVC-based applications contain:</span></span>

- <span data-ttu-id="5d085-107">**M** odels: 응용 프로그램의 데이터를 나타내고 유효성 검사 논리를 사용 하 여 해당 데이터에 대 한 비즈니스 규칙을 적용 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-107">**M** odels: Classes that represent the data of the application and that use validation logic to enforce business rules for that data.</span></span>
- <span data-ttu-id="5d085-108">**V** iews: 응용 프로그램에서 HTML 응답을 동적으로 생성 하는 데 사용 하는 템플릿 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-108">**V** iews: Template files that your application uses to dynamically generate HTML responses.</span></span>
- <span data-ttu-id="5d085-109">**C** ontrollers: 들어오는 브라우저 요청을 처리 하 고 모델 데이터를 검색 한 다음 브라우저에 응답을 반환 하는 보기 템플릿을 지정 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-109">**C** ontrollers: Classes that handle incoming browser requests, retrieve model data, and then specify view templates that return a response to the browser.</span></span>

<span data-ttu-id="5d085-110">Microsoft는이 자습서 시리즈의 모든 개념을 다루며 응용 프로그램을 빌드하는 데 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-110">We'll be covering all these concepts in this tutorial series and show you how to use them to build an application.</span></span>

<span data-ttu-id="5d085-111">먼저 컨트롤러 클래스를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-111">Let's begin by creating a controller class.</span></span> <span data-ttu-id="5d085-112">**솔루션 탐색기**에서 *Controllers* 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **추가**, **컨트롤러**를 차례로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-112">In **Solution Explorer**, right-click the *Controllers* folder and then click **Add**, then **Controller**.</span></span>

![](adding-a-controller/_static/image1.png)

<span data-ttu-id="5d085-113">**스 캐 폴드 추가** 대화 상자에서 **MVC 5 컨트롤러-비어 있음**을 클릭 한 다음 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-113">In the **Add Scaffold** dialog box, click **MVC 5 Controller - Empty**, and then click **Add**.</span></span>

![](adding-a-controller/_static/image2.png)  

<span data-ttu-id="5d085-114">새 컨트롤러의 이름을 "HelloWorldController"로 하 고 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-114">Name your new controller "HelloWorldController" and click **Add**.</span></span>

![컨트롤러 추가](adding-a-controller/_static/image3.png)

<span data-ttu-id="5d085-116">*HelloWorldController.cs* 라는 새 파일을 만들고 새 폴더 *Views\HelloWorld*를 **솔루션 탐색기** 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-116">Notice in **Solution Explorer** that a new file has been created named *HelloWorldController.cs* and a new folder *Views\HelloWorld*.</span></span> <span data-ttu-id="5d085-117">컨트롤러가 IDE에 열려 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-117">The controller is open in the IDE.</span></span>

![](adding-a-controller/_static/image4.png)

<span data-ttu-id="5d085-118">파일의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-118">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

<span data-ttu-id="5d085-119">컨트롤러 메서드는 HTML 문자열을 예제로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-119">The controller methods will return a string of HTML as an example.</span></span> <span data-ttu-id="5d085-120">컨트롤러 이름은 `HelloWorldController` 이 고 첫 번째 메서드의 이름은 `Index`입니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-120">The controller is named `HelloWorldController` and the first method is named `Index`.</span></span> <span data-ttu-id="5d085-121">브라우저에서 호출 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-121">Let's invoke it from a browser.</span></span> <span data-ttu-id="5d085-122">F5 키 또는 Ctrl + F5 키를 눌러 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-122">Run the application (press F5 or Ctrl+F5).</span></span> <span data-ttu-id="5d085-123">브라우저에서 주소 표시줄의 &quot;경로&quot; 에 HelloWorld를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-123">In the browser, append &quot;HelloWorld&quot; to the path in the address bar.</span></span> <span data-ttu-id="5d085-124">예를 들어 아래 `http://localhost:1234/HelloWorld.`그림에서 볼 때 브라우저의 페이지는 다음 스크린샷 처럼 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-124">(For example, in the illustration below, it's `http://localhost:1234/HelloWorld.`) The page in the browser will look like the following screenshot.</span></span> <span data-ttu-id="5d085-125">위의 메서드에서 코드는 문자열을 직접 반환 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-125">In the method above, the code returned a string directly.</span></span> <span data-ttu-id="5d085-126">일부 HTML만 반환 하도록 시스템에 지시 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-126">You told the system to just return some HTML, and it did!</span></span>

![](adding-a-controller/_static/image5.png)

<span data-ttu-id="5d085-127">ASP.NET MVC는 들어오는 URL에 따라 서로 다른 컨트롤러 클래스 (및 그 안의 다른 작업 메서드)를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-127">ASP.NET MVC invokes different controller classes (and different action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="5d085-128">ASP.NET MVC에서 사용 하는 기본 URL 라우팅 논리는 다음과 같은 형식을 사용 하 여 호출할 코드를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-128">The default URL routing logic used by ASP.NET MVC uses a format like this to determine what code to invoke:</span></span>

`/[Controller]/[ActionName]/[Parameters]`

<span data-ttu-id="5d085-129">*App\_Start/RouteConfig* 파일에서 라우팅에 대 한 형식을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-129">You set the format for routing in the *App\_Start/RouteConfig.cs* file.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample2.cs?highlight=7-8)]

<span data-ttu-id="5d085-130">응용 프로그램을 실행 하 고 URL 세그먼트를 제공 하지 않으면 기본적으로 "홈" 컨트롤러와 위 코드의 기본값 섹션에 지정 된 "인덱스" 작업 메서드로 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-130">When you run the application and don't supply any URL segments, it defaults to the "Home" controller and the "Index" action method specified in the defaults section of the code above.</span></span>

<span data-ttu-id="5d085-131">URL의 첫 번째 부분은 실행할 컨트롤러 클래스를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-131">The first part of the URL determines the controller class to execute.</span></span> <span data-ttu-id="5d085-132">그러면 */HelloWorld* 가 `HelloWorldController` 클래스에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-132">So */HelloWorld* maps to the `HelloWorldController` class.</span></span> <span data-ttu-id="5d085-133">URL의 두 번째 부분은 실행할 클래스에 대 한 작업 메서드를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-133">The second part of the URL determines the action method on the class to execute.</span></span> <span data-ttu-id="5d085-134">따라서 */HelloWorld/Index* `Index` 는 `HelloWorldController` 클래스의 메서드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-134">So */HelloWorld/Index* would cause the `Index` method of the `HelloWorldController` class to execute.</span></span> <span data-ttu-id="5d085-135">*/Helloworld* `Index` 로 이동 하기만 하면 기본적으로 메서드가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-135">Notice that we only had to browse to */HelloWorld* and the `Index` method was used by default.</span></span> <span data-ttu-id="5d085-136">이는 메서드가 `Index` 명시적으로 지정 되지 않은 경우 컨트롤러에서 호출 되는 기본 메서드 이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-136">This is because a method named `Index` is the default method that will be called on a controller if one is not explicitly specified.</span></span> <span data-ttu-id="5d085-137">URL 세그먼트(`Parameters`)의 세 번째 부분은 경로 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-137">The third part of the URL segment ( `Parameters`) is for route data.</span></span> <span data-ttu-id="5d085-138">이 자습서의 뒷부분에서 경로 데이터를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-138">We'll see route data later on in this tutorial.</span></span>

<span data-ttu-id="5d085-139">`http://localhost:xxxx/HelloWorld/Welcome`으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-139">Browse to `http://localhost:xxxx/HelloWorld/Welcome`.</span></span> <span data-ttu-id="5d085-140">메서드 `Welcome` 는 시작 동작 메서드인 문자열 &quot;을 실행 하 고 반환 합니다. &quot;.</span><span class="sxs-lookup"><span data-stu-id="5d085-140">The `Welcome` method runs and returns the string &quot;This is the Welcome action method...&quot;.</span></span> <span data-ttu-id="5d085-141">기본 MVC 매핑은 `/[Controller]/[ActionName]/[Parameters]`입니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-141">The default MVC mapping is `/[Controller]/[ActionName]/[Parameters]`.</span></span> <span data-ttu-id="5d085-142">이 URL의 경우 컨트롤러는 `HelloWorld`이고 `Welcome`은 작업 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-142">For this URL, the controller is `HelloWorld` and `Welcome` is the action method.</span></span> <span data-ttu-id="5d085-143">아직 URL의 `[Parameters]` 부분을 사용하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-143">You haven't used the `[Parameters]` part of the URL yet.</span></span>

![](adding-a-controller/_static/image6.png)

<span data-ttu-id="5d085-144">URL의 일부 매개 변수 정보를 컨트롤러에 전달할 수 있도록 예제를 약간 수정 하겠습니다 (예: */HelloWorld/Welcome? name = Scott&amp;numtimes = 4*).</span><span class="sxs-lookup"><span data-stu-id="5d085-144">Let's modify the example slightly so that you can pass some parameter information from the URL to the controller (for example, */HelloWorld/Welcome?name=Scott&amp;numtimes=4*).</span></span> <span data-ttu-id="5d085-145">다음과 같이 두 개의 매개 변수를 포함 하도록 메서드를변경합니다.`Welcome`</span><span class="sxs-lookup"><span data-stu-id="5d085-145">Change your `Welcome` method to include two parameters as shown below.</span></span> <span data-ttu-id="5d085-146">이 코드에서는 C# 선택적 매개 변수 기능을 사용 하 여 매개 변수에 대 `numTimes` 한 값이 전달 되지 않는 경우 매개 변수의 기본값을 1로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-146">Note that the code uses the C# optional-parameter feature to indicate that the `numTimes` parameter should default to 1 if no value is passed for that parameter.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample3.cs)]

> [!NOTE]
> <span data-ttu-id="5d085-147">보안 정보: 위의 코드는 [HtmlEncode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx) 을 사용 하 여 악의적인 입력 (즉, JavaScript) 으로부터 응용 프로그램을 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-147">Security Note: The code above uses [HttpUtility.HtmlEncode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx) to protect the application from malicious input (namely JavaScript).</span></span> <span data-ttu-id="5d085-148">자세한 내용은 [방법: 문자열](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx)에 HTML 인코딩을 적용 하 여 웹 응용 프로그램에서 스크립트 악용을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-148">For more information see [How to: Protect Against Script Exploits in a Web Application by Applying HTML Encoding to Strings](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx).</span></span>

 <span data-ttu-id="5d085-149">응용 프로그램을 실행 하 고 예제 URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`)로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-149">Run your application and browse to the example URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`).</span></span> <span data-ttu-id="5d085-150">URL에서 `name` 및 `numtimes`에 다른 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-150">You can try different values for `name` and `numtimes` in the URL.</span></span> <span data-ttu-id="5d085-151">[ASP.NET MVC 모델 바인딩 시스템](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) 은 주소 표시줄의 쿼리 문자열에서 명명 된 매개 변수를 메서드의 매개 변수에 자동으로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-151">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters from the query string in the address bar to parameters in your method.</span></span>

![](adding-a-controller/_static/image7.png)

<span data-ttu-id="5d085-152">위의 샘플 `Parameters`에서 URL 세그먼트 ()는 사용 `name` 되지 않으며 및 `numTimes` 매개 변수는 [쿼리 문자열로](http://en.wikipedia.org/wiki/Query_string)전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-152">In the sample above, the URL segment ( `Parameters`) is not used, the `name` and `numTimes` parameters are passed as [query strings](http://en.wikipedia.org/wiki/Query_string).</span></span> <span data-ttu-id="5d085-153">?</span><span class="sxs-lookup"><span data-stu-id="5d085-153">The ?</span></span> <span data-ttu-id="5d085-154">위의 URL에서 (물음표)는 구분 기호 이며 쿼리 문자열은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-154">(question mark) in the above URL is a separator, and the query strings follow.</span></span> <span data-ttu-id="5d085-155">&amp; 문자는 쿼리 문자열을 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-155">The &amp; character separates query strings.</span></span>

<span data-ttu-id="5d085-156">환영 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-156">Replace the Welcome method with the following code:</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample4.cs)]

<span data-ttu-id="5d085-157">응용 프로그램을 실행 하 고 다음 URL을 입력 합니다.`http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`</span><span class="sxs-lookup"><span data-stu-id="5d085-157">Run the application and enter the following URL: `http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`</span></span>

![](adding-a-controller/_static/image8.png)

<span data-ttu-id="5d085-158">이 때 세 번째 URL 세그먼트가 경로 매개 `ID.` 변수와 일치 하는 경우 작업 메서드에는 `Welcome` `RegisterRoutes` 메서드의`ID`URL 사양과 일치 하는 매개 변수 ()가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-158">This time the third URL segment matched the route parameter `ID.` The `Welcome` action method contains a parameter (`ID`) that matched the URL specification in the `RegisterRoutes` method.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample5.cs?highlight=7)]

<span data-ttu-id="5d085-159">ASP.NET MVC 응용 프로그램에서는 매개 변수를 쿼리 문자열로 전달 하는 것 보다 경로 데이터로 전달 하는 것이 더 일반적입니다 (위의 ID와 같이).</span><span class="sxs-lookup"><span data-stu-id="5d085-159">In ASP.NET MVC applications, it's more typical to pass in parameters as route data (like we did with ID above) than passing them as query strings.</span></span> <span data-ttu-id="5d085-160">경로를 추가 하 여 `name` 및 `numtimes` 의 매개 변수를 URL의 경로 데이터로 전달할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-160">You could also add a route to pass both the `name` and `numtimes` in parameters as route data in the URL.</span></span> <span data-ttu-id="5d085-161">에 \*앱\_start\* 파일을 "Hello" 경로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-161">In the *App\_Start\RouteConfig.cs* file, add the "Hello" route:</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample6.cs?highlight=13-16)]

<span data-ttu-id="5d085-162">응용 프로그램을 실행 하 고 `/localhost:XXX/HelloWorld/Welcome/Scott/3`로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-162">Run the application and browse to `/localhost:XXX/HelloWorld/Welcome/Scott/3`.</span></span>

![](adding-a-controller/_static/image9.png)

<span data-ttu-id="5d085-163">많은 MVC 응용 프로그램의 경우 기본 경로는 정상적으로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-163">For many MVC applications, the default route works fine.</span></span> <span data-ttu-id="5d085-164">모델 바인더를 사용 하 여 데이터를 전달 하는이 자습서의 뒷부분에서 설명 하 고 해당에 대 한 기본 경로를 수정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-164">You'll learn later in this tutorial to pass data using the model binder, and you won't have to modify the default route for that.</span></span>

<span data-ttu-id="5d085-165">이 예에서 컨트롤러는 MVC의 &quot;VC&quot; 부분을 수행 하 고 있습니다. 즉, 뷰 및 컨트롤러가 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-165">In these examples the controller has been doing the &quot;VC&quot; portion of MVC — that is, the view and controller work.</span></span> <span data-ttu-id="5d085-166">컨트롤러는 HTML을 직접 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-166">The controller is returning HTML directly.</span></span> <span data-ttu-id="5d085-167">일반적으로 컨트롤러는 코드를 매우 복잡 하 게 하기 때문에 HTML을 직접 반환 하는 것을 원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-167">Ordinarily you don't want controllers returning HTML directly, since that becomes very cumbersome to code.</span></span> <span data-ttu-id="5d085-168">대신 일반적으로 별도의 뷰 템플릿 파일을 사용 하 여 HTML 응답을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-168">Instead we'll typically use a separate view template file to help generate the HTML response.</span></span> <span data-ttu-id="5d085-169">이 작업을 수행 하는 방법에 대해 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5d085-169">Let's look next at how we can do this.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5d085-170">[이전](getting-started.md)
> [다음](adding-a-view.md)</span><span class="sxs-lookup"><span data-stu-id="5d085-170">[Previous](getting-started.md)
[Next](adding-a-view.md)</span></span>
