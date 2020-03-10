---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
title: 컨트롤러 추가 | Microsoft Docs
author: shanselman
description: Visual Studio 2013를 사용 하 여이 자습서를 사용할 수 있는 경우 업데이트 된 버전입니다. 새 자습서에서는 ASP.NET MVC 5를 사용 하 여 여러 가지 향상 된 기능을 제공 합니다.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: ff03dcc0-da97-458d-838f-0823e7482642
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
msc.type: authoredcontent
ms.openlocfilehash: e2a298584473f57c2b14edf507f0f6886d906ea3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437567"
---
# <a name="adding-a-controller"></a><span data-ttu-id="1ee2a-104">컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="1ee2a-104">Adding a Controller</span></span>

<span data-ttu-id="1ee2a-105">[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="1ee2a-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> > [!NOTE]
> > <span data-ttu-id="1ee2a-106">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)를 [사용 하 여](../../getting-started/introduction/getting-started.md) 이 자습서를 사용할 수 있는 경우 업데이트 된 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-106">An updated version if this tutorial is available [here](../../getting-started/introduction/getting-started.md) using [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013).</span></span> <span data-ttu-id="1ee2a-107">새 자습서에서는이 자습서를 통해 많은 향상 된 기능을 제공 하는 ASP.NET MVC 5를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-107">The new tutorial uses ASP.NET MVC 5, which provides many improvements over this tutorial.</span></span>
>
>
> <span data-ttu-id="1ee2a-108">ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-108">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="1ee2a-109">데이터베이스에서 읽고 쓰는 간단한 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-109">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="1ee2a-110">[ASP.NET mvc 학습 센터](../../../index.md) 를 방문 하 여 다른 ASP.NET mvc 자습서 및 샘플을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-110">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="1ee2a-111">MVC는 모델, 뷰, 컨트롤러를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-111">MVC stands for Model, View, Controller.</span></span> <span data-ttu-id="1ee2a-112">MVC는 응용 프로그램을 개발 하는 패턴으로, 각 파트에는 다른 책임이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-112">MVC is a pattern for developing applications such that each part has a responsibility that is different from another.</span></span>

- <span data-ttu-id="1ee2a-113">Model: 응용 프로그램의 데이터</span><span class="sxs-lookup"><span data-stu-id="1ee2a-113">Model: The data of your application</span></span>
- <span data-ttu-id="1ee2a-114">보기: 응용 프로그램에서 HTML 응답을 동적으로 생성 하는 데 사용 하는 템플릿 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-114">Views: The template files your application will use to dynamically generate HTML responses.</span></span>
- <span data-ttu-id="1ee2a-115">컨트롤러: 응용 프로그램에 대 한 들어오는 URL 요청을 처리 하 고, 모델 데이터를 검색 한 후 클라이언트에 응답을 다시 렌더링 하는 뷰 템플릿을 지정 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-115">Controllers: Classes that handle incoming URL requests to the application, retrieve model data, and then specify view templates that render a response back to the client</span></span>

<span data-ttu-id="1ee2a-116">이 자습서에서는 이러한 모든 개념을 설명 하 고 응용 프로그램을 빌드하는 데 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-116">We'll be covering all these concepts in this tutorial and show you how to use them to build an application.</span></span>

<span data-ttu-id="1ee2a-117">솔루션 탐색기에서 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 하 고 컨트롤러 추가를 선택 하 여 새 컨트롤러를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-117">Let's create a new controller by right-clicking the controllers folder in the solution Explorer and selecting Add Controller.</span></span>

<span data-ttu-id="1ee2a-118">[![AddControllerRightClick](getting-started-with-mvc-part2/_static/image2.png)](getting-started-with-mvc-part2/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1ee2a-118">[![AddControllerRightClick](getting-started-with-mvc-part2/_static/image2.png)](getting-started-with-mvc-part2/_static/image1.png)</span></span>

<span data-ttu-id="1ee2a-119">새 컨트롤러의 이름을 "HelloWorldController"로 하 고 추가를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-119">Name your new controller "HelloWorldController" and click Add.</span></span>

<span data-ttu-id="1ee2a-120">[![컨트롤러 추가 대화 상자](getting-started-with-mvc-part2/_static/image4.png)](getting-started-with-mvc-part2/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="1ee2a-120">[![Add Controller Dialog](getting-started-with-mvc-part2/_static/image4.png)](getting-started-with-mvc-part2/_static/image3.png)</span></span>

<span data-ttu-id="1ee2a-121">솔루션 탐색기에서 HelloWorldController.cs 라는 새 파일이 생성 되었으며 해당 파일이 이제 **IDE**에서 열려 있음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-121">Notice in the Solution Explorer on the right that a new file has been created for you called HelloWorldController.cs and that file is now opened in the **IDE**.</span></span>

<span data-ttu-id="1ee2a-122">[![HelloWorldControllerCode](getting-started-with-mvc-part2/_static/image6.png)](getting-started-with-mvc-part2/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="1ee2a-122">[![HelloWorldControllerCode](getting-started-with-mvc-part2/_static/image6.png)](getting-started-with-mvc-part2/_static/image5.png)</span></span>

<span data-ttu-id="1ee2a-123">새 public 클래스 HelloWorldController 내에서 다음과 같은 두 개의 새로운 메서드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-123">Create two new methods that look like this inside of your new public class HelloWorldController.</span></span> <span data-ttu-id="1ee2a-124">예를 들어 컨트롤러에서 직접 HTML 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-124">We'll return a string of HTML directly from our controller as an example.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample1.cs)]

<span data-ttu-id="1ee2a-125">컨트롤러 이름이 HelloWorldController이 고 새 메서드를 Index 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-125">Your Controller is named HelloWorldController and your new Method is called Index.</span></span> <span data-ttu-id="1ee2a-126">이전과 마찬가지로 응용 프로그램을 다시 실행 합니다. 재생 단추를 클릭 하거나 F5 키를 눌러이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-126">Run your application again, just as before (click the play button or press F5 to do this).</span></span> <span data-ttu-id="1ee2a-127">브라우저가 시작 되 면 주소 표시줄의 경로를 `http://localhost:xx/HelloWorld`로 변경 합니다. 여기서 xx는 컴퓨터에서 선택한 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-127">Once your browser has started up, change the path in the address bar to `http://localhost:xx/HelloWorld` where xx is whatever number your computer has chosen.</span></span> <span data-ttu-id="1ee2a-128">이제 브라우저가 아래 스크린샷 처럼 보입니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-128">Now your browser should look like the screenshot below.</span></span> <span data-ttu-id="1ee2a-129">위의 메서드에서는 "Content" 라는 메서드에 전달 된 문자열을 반환 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-129">In our method above we returned a string passed into a method called "Content."</span></span> <span data-ttu-id="1ee2a-130">시스템이 몇 가지 HTML을 반환 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-130">We told the system just returns some HTML, and it did!</span></span>

<span data-ttu-id="1ee2a-131">ASP.NET MVC는 들어오는 URL에 따라 서로 다른 컨트롤러 클래스 (및 그 안의 다른 작업 메서드)를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-131">ASP.NET MVC invokes different Controller classes (and different Action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="1ee2a-132">ASP.NET MVC에서 사용 하는 기본 매핑 논리는 다음과 같은 형식을 사용 하 여 실행 되는 코드를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-132">The default mapping logic used by ASP.NET MVC uses a format like this to control what code is run:</span></span>

<span data-ttu-id="1ee2a-133">/[Controller]/[ActionName]/[Parameters]</span><span class="sxs-lookup"><span data-stu-id="1ee2a-133">/[Controller]/[ActionName]/[Parameters]</span></span>

<span data-ttu-id="1ee2a-134">URL의 첫 번째 부분은 실행할 컨트롤러 클래스를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-134">The first part of the URL determines the Controller class to execute.</span></span> <span data-ttu-id="1ee2a-135">그러면/HelloWorld가 HelloWorldController 클래스에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-135">So /HelloWorld maps to the HelloWorldController class.</span></span> <span data-ttu-id="1ee2a-136">URL의 두 번째 부분은 실행할 클래스에 대 한 작업 메서드를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-136">The second part of the URL determines the Action method on the class to execute.</span></span> <span data-ttu-id="1ee2a-137">따라서/HelloWorld/Index는 HelloWorldController 클래스의 Index () 메서드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-137">So /HelloWorld/Index would cause the Index() method of the HelloWorldController class to execute.</span></span> <span data-ttu-id="1ee2a-138">위의/HelloWorld를 방문 하기만 하면 메서드 인덱스가 암시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-138">Notice that we only had to visit /HelloWorld above and the method Index was implied.</span></span> <span data-ttu-id="1ee2a-139">이는 "Index" 라는 메서드가 명시적으로 지정 되지 않은 경우 컨트롤러에서 호출 되는 기본 메서드 이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-139">This is because a method named "Index" is the default method that will be called on a controller if one is not explicitly specified.</span></span>

<span data-ttu-id="1ee2a-140">[기본 작업 ![](getting-started-with-mvc-part2/_static/image8.png)](getting-started-with-mvc-part2/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="1ee2a-140">[![This is my default action](getting-started-with-mvc-part2/_static/image8.png)](getting-started-with-mvc-part2/_static/image7.png)</span></span>

<span data-ttu-id="1ee2a-141">이제 환영 메서드가 실행 되어 해당 HTML 문자열을 반환 하는 `http://localhost:xx/HelloWorld/Welcome.`를 방문해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-141">Now, let's visit `http://localhost:xx/HelloWorld/Welcome.` Now our Welcome Method has executed and returned its HTML string.</span></span>

<span data-ttu-id="1ee2a-142">다시,/[Controller]/[ActionName]/[Parameters]를 다시 한 번, 컨트롤러는 HelloWorld 이며이 경우에는 환영입니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-142">Again, /[Controller]/[ActionName]/[Parameters] so Controller is HelloWorld and Welcome is the Method in this case.</span></span> <span data-ttu-id="1ee2a-143">매개 변수를 아직 수행 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-143">We haven't done Parameters yet.</span></span>

<span data-ttu-id="1ee2a-144">[시작 작업 방법 ![](getting-started-with-mvc-part2/_static/image10.png)](getting-started-with-mvc-part2/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="1ee2a-144">[![This is the Welcome action method](getting-started-with-mvc-part2/_static/image10.png)](getting-started-with-mvc-part2/_static/image9.png)</span></span>

<span data-ttu-id="1ee2a-145">URL에서 컨트롤러로 일부 정보를 전달할 수 있도록 샘플을 약간 수정 하겠습니다. 예를 들어/HelloWorld/Welcome? name = Scott&amp;numtimes = 4와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-145">Let's modify our sample slightly so that we can pass some information in from the URL to our controller, for example like this: /HelloWorld/Welcome?name=Scott&amp;numtimes=4.</span></span> <span data-ttu-id="1ee2a-146">두 개의 매개 변수를 포함 하도록 환영 메서드를 변경 하 고 아래와 같이 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-146">Change your Welcome method to include two parameters and update it like below.</span></span> <span data-ttu-id="1ee2a-147">C# 선택적 매개 변수 기능을 사용 하 여 numtimes 매개 변수가 전달 되지 않은 경우 기본값을 1로 지정 해야 함을 지정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-147">Note that we've used the C# optional parameter feature to indicate that the parameter numTimes should default to 1 if it's not passed in.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample2.cs)]

<span data-ttu-id="1ee2a-148">응용 프로그램을 실행 하 고 이름 및 numtimes 값을 원하는 대로 변경 `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`를 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-148">Run your application and visit `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` changing the value of name and numtimes as you like.</span></span> <span data-ttu-id="1ee2a-149">시스템은 주소 표시줄의 쿼리 문자열에서 메서드의 매개 변수로 명명 된 매개 변수를 자동으로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-149">The system automatically mapped the named parameters from your query string in the address bar to parameters in your method.</span></span>

<span data-ttu-id="1ee2a-150">두 예제 모두에서 컨트롤러는 모든 작업을 수행 하 고 HTML을 직접 반환 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-150">In both these examples the controller has been doing all the work, and has been returning HTML directly.</span></span> <span data-ttu-id="1ee2a-151">일반적으로 컨트롤러에서 HTML을 직접 반환 하는 것을 원하지 않습니다 .이는 코드를 매우 복잡 하 게 종료 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-151">Ordinarily we don't want our Controllers returning HTML directly - since that ends up being very cumbersome to code.</span></span> <span data-ttu-id="1ee2a-152">대신 일반적으로 별도의 뷰 템플릿 파일을 사용 하 여 HTML 응답을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-152">Instead we'll typically use a separate View template file to help generate the HTML response.</span></span> <span data-ttu-id="1ee2a-153">이 작업을 수행 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-153">Let's look at how we can do this.</span></span> <span data-ttu-id="1ee2a-154">브라우저를 닫고 IDE로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="1ee2a-154">Close your browser and return to the IDE.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1ee2a-155">[이전](getting-started-with-mvc-part1.md)
> [다음](getting-started-with-mvc-part3.md)</span><span class="sxs-lookup"><span data-stu-id="1ee2a-155">[Previous](getting-started-with-mvc-part1.md)
[Next](getting-started-with-mvc-part3.md)</span></span>
