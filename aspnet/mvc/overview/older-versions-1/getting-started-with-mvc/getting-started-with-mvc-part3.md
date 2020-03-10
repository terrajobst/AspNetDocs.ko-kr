---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
title: 뷰 추가 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 데이터베이스에서 읽고 쓰는 간단한 웹 응용 프로그램을 만듭니다.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: e8f1515c-c277-47ff-a23e-224118f13f02
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
msc.type: authoredcontent
ms.openlocfilehash: 462b1210c45da67058899193afcea973f3daf122
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469775"
---
# <a name="adding-a-view"></a><span data-ttu-id="d03cf-104">보기 추가</span><span class="sxs-lookup"><span data-stu-id="d03cf-104">Adding a View</span></span>

<span data-ttu-id="d03cf-105">[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="d03cf-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="d03cf-106">ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="d03cf-107">데이터베이스에서 읽고 쓰는 간단한 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="d03cf-108">[ASP.NET mvc 학습 센터](../../../index.md) 를 방문 하 여 다른 ASP.NET mvc 자습서 및 샘플을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="d03cf-109">이 섹션에서는 HelloWorldController 클래스에서 뷰 템플릿 파일을 사용 하 여 클라이언트에 대 한 HTML 응답 생성을 완전히 캡슐화 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-109">In this section we are going to look at how we can have our HelloWorldController class use a View template file to cleanly encapsulate generating HTML responses back to a client.</span></span>

<span data-ttu-id="d03cf-110">인덱스 메서드와 함께 뷰 템플릿을 사용 하 여 시작 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-110">Let's start by using a View template with our Index method.</span></span> <span data-ttu-id="d03cf-111">이 메서드는 인덱스 라고 하 고 HelloWorldController에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-111">Our method is called Index and it's in the HelloWorldController.</span></span> <span data-ttu-id="d03cf-112">현재 Index () 메서드는 Controller 클래스 내에서 하드 코드 된 메시지를 포함 하는 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-112">Currently our Index() method returns a string with a message that is hardcoded within the Controller class.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample1.cs)]

<span data-ttu-id="d03cf-113">이제 다음과 같이 인덱스 메서드를 변경 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-113">Let's now change the Index method to instead look like this:</span></span>

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample2.cs)]

<span data-ttu-id="d03cf-114">이제 Index () 메서드에 사용할 수 있는 뷰 템플릿을 프로젝트에 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-114">Let's now add a View template to our project that we can use for our Index() method.</span></span> <span data-ttu-id="d03cf-115">이렇게 하려면 인덱스 메서드 가운데에 마우스를 놓고 마우스 오른쪽 단추를 클릭 한 다음 보기 추가 ...를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-115">To do this, right-click with your mouse somewhere in the middle of the Index method and click Add View...</span></span>

![이미지](getting-started-with-mvc-part3/_static/image1.png)

<span data-ttu-id="d03cf-117">그러면 인덱스 메서드에서 사용할 수 있는 보기 템플릿을 만드는 방법에 대 한 몇 가지 옵션을 제공 하는 "뷰 추가" 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-117">This will bring up the "Add View" dialog which provides us some options for how we want to create a view template that can be used by our Index method.</span></span> <span data-ttu-id="d03cf-118">지금은 아무것도 변경 하지 말고 추가 단추를 클릭 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-118">For now, don't change anything, and just click the Add button.</span></span>

<span data-ttu-id="d03cf-119">[뷰 추가 ![대화 상자](getting-started-with-mvc-part3/_static/image3.png)](getting-started-with-mvc-part3/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="d03cf-119">[![Add View Dialog](getting-started-with-mvc-part3/_static/image3.png)](getting-started-with-mvc-part3/_static/image2.png)</span></span>

<span data-ttu-id="d03cf-120">추가를 클릭 하면 여기에 표시 된 것 처럼 새 폴더와 새 파일이 솔루션 폴더에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-120">After you click Add, a new folder and a new file will appear in the Solution Folder, as seen here.</span></span> <span data-ttu-id="d03cf-121">이제 보기 아래에 HelloWorld 폴더와 해당 폴더 안에 있는 인덱스 .aspx 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-121">I now have a HelloWorld folder under Views, and an Index.aspx file inside that folder.</span></span>

<span data-ttu-id="d03cf-122">[![solutionexplorerwithindex](getting-started-with-mvc-part3/_static/image5.png)](getting-started-with-mvc-part3/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="d03cf-122">[![solutionexplorerwithindex](getting-started-with-mvc-part3/_static/image5.png)](getting-started-with-mvc-part3/_static/image4.png)</span></span>

<span data-ttu-id="d03cf-123">새 인덱스 파일도 이미 열려 있으며 편집할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-123">The new Index file is also already opened and ready for editing.</span></span> <span data-ttu-id="d03cf-124">"Hello World"와 같이 첫 번째 &lt;h2&gt;인덱스&lt;/h 2&gt;에 일부 텍스트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-124">Add some text under the first &lt;h2&gt;Index&lt;/h2&gt; like "Hello World."</span></span>

[!code-html[Main](getting-started-with-mvc-part3/samples/sample3.html)]

<span data-ttu-id="d03cf-125">응용 프로그램을 실행 하 고 브라우저에서 [`http://localhost:xx/HelloWorld`](http://localhostxx) 를 다시 방문 하세요.</span><span class="sxs-lookup"><span data-stu-id="d03cf-125">Run your application and visit [`http://localhost:xx/HelloWorld`](http://localhostxx) again in your browser.</span></span> <span data-ttu-id="d03cf-126">이 예에서 컨트롤러의 인덱스 메서드는 아무 작업을 수행 하지 않았지만 뷰 템플릿 파일을 사용 하 여 클라이언트에 응답을 다시 렌더링 하도록 지정 하는 "return 뷰 ()"를 호출 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-126">The Index method in our controller in this example didn't do any work, but did call "return View()" which indicated that we wanted to use a view template file to render a response back to the client.</span></span> <span data-ttu-id="d03cf-127">사용할 뷰 템플릿 파일의 이름을 명시적으로 지정 하지 않았기 때문에 ASP.NET MVC는 \Views\HelloWorld 폴더에 있는 파일을 사용 하 여 기본적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-127">Because we did not explicitly specify the name of the view template file to use, ASP.NET MVC defaulted to using the Index.aspx view file within the \Views\HelloWorld folder.</span></span> <span data-ttu-id="d03cf-128">이제 보기에 하드 코딩 된 문자열이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-128">Now we see the string we hard-coded in our View.</span></span>

<span data-ttu-id="d03cf-129">[인덱스 ![-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image7.png)](getting-started-with-mvc-part3/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="d03cf-129">[![Index - Windows Internet Explorer](getting-started-with-mvc-part3/_static/image7.png)](getting-started-with-mvc-part3/_static/image6.png)</span></span>

<span data-ttu-id="d03cf-130">매우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-130">Looks pretty good.</span></span> <span data-ttu-id="d03cf-131">그러나 브라우저의 제목은 "인덱스"로 표시 되 고 페이지의 큰 제목은 "내 MVC 응용 프로그램" 이라고 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-131">However, notice that the Browser's title says "Index" and the big title on the page says "My MVC Application."</span></span> <span data-ttu-id="d03cf-132">이러한 변경 내용을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-132">Let's change those.</span></span>

### <a name="changing-views-and-master-pages"></a><span data-ttu-id="d03cf-133">보기 및 마스터 페이지 변경</span><span class="sxs-lookup"><span data-stu-id="d03cf-133">Changing Views and Master Pages</span></span>

<span data-ttu-id="d03cf-134">먼저 "내 MVC 응용 프로그램" 텍스트를 변경 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-134">First, let's change the text "My MVC Application."</span></span> <span data-ttu-id="d03cf-135">이 텍스트는 공유 되 고 모든 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-135">That text is shared and appears on every page.</span></span> <span data-ttu-id="d03cf-136">실제로는 응용 프로그램의 모든 페이지에 있더라도 코드의 한 곳에만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-136">It actually appears in only one place in our code, even though it's on every page in our app.</span></span> <span data-ttu-id="d03cf-137">솔루션 탐색기의/Views/Shared 폴더로 이동 하 여 사이트 .Master 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-137">Go to the /Views/Shared folder in the Solution Explorer and open the Site.Master file.</span></span> <span data-ttu-id="d03cf-138">이 파일을 마스터 페이지 라고 하며 다른 모든 페이지에서 사용 하는 공유 "셸"입니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-138">This file is called a Master Page and it's the shared "shell" that all our other pages use.</span></span>

<span data-ttu-id="d03cf-139">이 파일에는 ContentPlaceholder "MainContent" 라는 텍스트가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-139">Notice some text that says ContentPlaceholder "MainContent" in this file.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample4.aspx)]

<span data-ttu-id="d03cf-140">이 자리 표시자는 만든 모든 페이지가 마스터 페이지에 표시 되는 "래핑된" 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-140">That placeholder is where all the pages you create will show up, "wrapped" in the master page.</span></span> <span data-ttu-id="d03cf-141">제목을 변경 하 고 앱을 실행 하 고 여러 페이지를 방문 하세요.</span><span class="sxs-lookup"><span data-stu-id="d03cf-141">Try changing the title, then run your app and visit multiple pages.</span></span> <span data-ttu-id="d03cf-142">단일 변경 내용이 여러 페이지에 표시 되는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-142">You'll notice that your one change appears on multiple pages.</span></span>

[!code-html[Main](getting-started-with-mvc-part3/samples/sample5.html)]

<span data-ttu-id="d03cf-143">이제 모든 페이지에 기본 제목이 있습니다. 여기에는 "내 MVC 영화 응용 프로그램"의 H1이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-143">Now every page will have the Primary Heading - that's H1 - of "My MVC Movie Application."</span></span> <span data-ttu-id="d03cf-144">위쪽에 있는 흰색 텍스트를 처리 하 고 모든 페이지에서 공유 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-144">That handles the white text at the top there that's shared across all the pages.</span></span>

<span data-ttu-id="d03cf-145">변경 된 제목이 있는 Site.master는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-145">Here is the Site.Master in its entirety with our changed title:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample6.aspx)]

<span data-ttu-id="d03cf-146">이제 인덱스 페이지의 제목을 변경 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-146">Now, let's change the title of the Index page.</span></span>

<span data-ttu-id="d03cf-147">/HelloWorld/Index.aspx. 열기</span><span class="sxs-lookup"><span data-stu-id="d03cf-147">Open /HelloWorld/Index.aspx.</span></span> <span data-ttu-id="d03cf-148">변경 해야 하는 두 가지 위치가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-148">There's two places to change.</span></span> <span data-ttu-id="d03cf-149">먼저 브라우저 제목에 표시 되는 제목을 표시 한 다음 보조 헤더 (H2)도 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-149">First, the Title that appears in the title of the browser, then the secondary header - that's H2 - as well.</span></span> <span data-ttu-id="d03cf-150">앱의 일부를 변경 하는 코드의 비트를 확인할 수 있도록 각각 약간씩 다르게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-150">I'll make them each slightly different so you can see which bit of code changes which part of the app.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample7.aspx)]

<span data-ttu-id="d03cf-151">앱을 실행 하 고/Movies.를 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-151">Run your app and visit /Movies.</span></span> <span data-ttu-id="d03cf-152">브라우저 제목, 주 머리글 및 보조 머리글이 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-152">Notice that the browser title, the primary heading and the secondary headings have changed.</span></span> <span data-ttu-id="d03cf-153">보기를 약간만 변경 하 여 앱에서 큰 변경 작업을 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-153">It's easy to make big changes in your app with small changes to your view.</span></span>

<span data-ttu-id="d03cf-154">[![동영상 목록-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image9.png)](getting-started-with-mvc-part3/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="d03cf-154">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part3/_static/image9.png)](getting-started-with-mvc-part3/_static/image8.png)</span></span>

<span data-ttu-id="d03cf-155">약간 약간의 "데이터" (이 경우 "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="d03cf-155">Our little bit of "data" (in this case the "Hello World!"</span></span> <span data-ttu-id="d03cf-156">메시지)가 하드 코딩 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-156">message) was hard coded though.</span></span> <span data-ttu-id="d03cf-157">V (뷰)가 있지만 C (컨트롤러)가 있지만 M (모델)은 아직 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-157">We've got V (Views) and we've got C (Controllers), but no M (Model) yet.</span></span> <span data-ttu-id="d03cf-158">데이터베이스를 만들고 모델 데이터를 검색 하는 방법을 곧 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-158">We'll shortly walk through how create a database and retrieve model data from it.</span></span>

## <a name="passing-a-viewmodel"></a><span data-ttu-id="d03cf-159">ViewModel 전달</span><span class="sxs-lookup"><span data-stu-id="d03cf-159">Passing a ViewModel</span></span>

<span data-ttu-id="d03cf-160">데이터베이스로 이동 하 여 모델에 대해 설명 하기 전에 먼저 "ViewModels"에 대해 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-160">Before we go to a database and talk about Models, though, let's first talk about "ViewModels."</span></span> <span data-ttu-id="d03cf-161">이러한 개체는 뷰 템플릿이 클라이언트에 게 다시 HTML 응답을 렌더링 하는 데 필요한 항목을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-161">These are objects that represent what a View template requires to render an HTML response back to a client.</span></span> <span data-ttu-id="d03cf-162">일반적으로이 클래스는 컨트롤러 클래스에 의해 생성 되 고 뷰 템플릿에 전달 되며 뷰 템플릿에 필요한 데이터만 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-162">They are typically created and passed by a Controller class to a View template, and should only contain the data that the View template requires - and no more.</span></span>

<span data-ttu-id="d03cf-163">이전에는 HelloWorld 샘플을 통해 환영 () 동작 메서드는 이름 및 numTimes 매개 변수를 사용 하 여 브라우저에 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-163">Previously with our HelloWorld sample, our Welcome() action method took a name and a numTimes parameter and output it to the browser.</span></span> <span data-ttu-id="d03cf-164">컨트롤러에서이 응답을 계속 직접 렌더링 하는 대신 해당 데이터를 저장 하는 작은 클래스를 만든 다음 뷰 템플릿에 전달 하 여 HTML 응답을 다시 렌더링 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-164">Rather than have the Controller continue to render this response directly,let's instead make a small class to hold that data and then pass it over to a View template to render back the HTML response using it.</span></span> <span data-ttu-id="d03cf-165">이러한 방식으로 컨트롤러는 응용 프로그램 내에서 문제를 명확 하 게 분리 하는 "문제를 해결 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-165">This way the Controller is concerned with one thing and the View template another – enabling us to maintain clean "separation of concerns" within our application.</span></span>

<span data-ttu-id="d03cf-166">HelloWorldController.cs 파일로 돌아가서 새 "WelcomeViewModel" 클래스를 추가 하 고 컨트롤러 내에서 시작 메서드를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-166">Return to the HelloWorldController.cs file and add a new "WelcomeViewModel" class and change the Welcome method inside your controller.</span></span> <span data-ttu-id="d03cf-167">다음은 동일한 파일에 새 클래스를 사용 하는 전체 HelloWorldController.cs입니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-167">Here is the complete HelloWorldController.cs with the new class in the same file.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample8.cs)]

<span data-ttu-id="d03cf-168">여러 줄에 있는 경우에도 환영 메서드는 사실 두 개의 코드 문입니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-168">Even though it's on multiple lines, our Welcome method is really only two code statements.</span></span> <span data-ttu-id="d03cf-169">첫 번째 문은 두 개의 매개 변수를 ViewModel 개체에 패키지 하 고, 두 번째 문은 결과 개체를 뷰에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-169">The first statement packages up our two parameters into a ViewModel object, and the second passes the resulting object onto the View.</span></span>

<span data-ttu-id="d03cf-170">이제 시작 보기 템플릿이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-170">Now we need a Welcome View template!</span></span> <span data-ttu-id="d03cf-171">시작 메서드를 마우스 오른쪽 단추로 클릭 하 고 뷰 추가를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-171">Right click in the Welcome method and select Add View.</span></span> <span data-ttu-id="d03cf-172">이번에는 "강력한 형식의 뷰 만들기"를 선택 하 고 드롭다운 목록에서 WelcomeViewModel 클래스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-172">This time, we'll check "Create a strongly-typed view" and select our WelcomeViewModel class from the drop down list.</span></span> <span data-ttu-id="d03cf-173">이 새 뷰는 WelcomeViewModels 및 다른 유형의 개체는 인식 하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-173">This new view will only know about WelcomeViewModels and no other types of objects.</span></span>

> <span data-ttu-id="d03cf-174">*참고: 드롭다운 목록에 표시 되는 WelcomeViewModel를 추가한 후 한 번 컴파일해야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="d03cf-174">*NOTE: You'll need to have compiled once after adding your WelcomeViewModel for to show up in the drop down list.*</span></span>

<span data-ttu-id="d03cf-175">보기 추가 대화 상자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-175">Here's what your Add View dialog should look like.</span></span> <span data-ttu-id="d03cf-176">추가 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-176">Click the Add button.</span></span> ![원 원으로 표시 되는 추가](getting-started-with-mvc-part3/_static/image10.png)

<span data-ttu-id="d03cf-178">새 시작 .aspx의 &lt;h2&gt;에이 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-178">Add this code under the &lt;h2&gt; in your new Welcome.aspx.</span></span> <span data-ttu-id="d03cf-179">사용자에 게 표시 되는 횟수 만큼 루프와 Hello를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-179">We'll make a loop and say Hello as many times as the user says we should!</span></span>

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample9.aspx)]

<span data-ttu-id="d03cf-180">또한 아래 스크린샷에 표시 된 것 처럼 모델 개체를 참조할 때마다 유용한 Intellisense를 제공 하기 위해 WelcomeViewModel에 대 한 보기를 제공 하기 때문에 입력 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-180">Also, notice while you're typing that because we told this View about the WelcomeViewModel (they are married, remember?) that we get helpful Intellisense each time we reference our Model object as seen in the screenshot below:</span></span>

<span data-ttu-id="d03cf-181">[![NumTime 소스 코드](getting-started-with-mvc-part3/_static/image12.png)](getting-started-with-mvc-part3/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="d03cf-181">[![NumTime Source Code](getting-started-with-mvc-part3/_static/image12.png)](getting-started-with-mvc-part3/_static/image11.png)</span></span>

<span data-ttu-id="d03cf-182">응용 프로그램을 실행 하 고 `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`를 다시 방문 하세요.</span><span class="sxs-lookup"><span data-stu-id="d03cf-182">Run your application and visit `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` again.</span></span> <span data-ttu-id="d03cf-183">이제 URL에서 데이터를 가져오고, 컨트롤러에 자동으로 전달 됩니다. 컨트롤러는 데이터를 ViewModel으로 패키지 하 고 해당 개체를 보기에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-183">Now we're taking data from the URL, it's passed into our Controller automatically, our Controller packages up the data into a ViewModel and passes that object onto our View.</span></span> <span data-ttu-id="d03cf-184">보기는 사용자에 게 데이터를 HTML로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-184">The View than displays the data as HTML to the user.</span></span>

<span data-ttu-id="d03cf-185">[![시작-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image14.png)](getting-started-with-mvc-part3/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="d03cf-185">[![Welcome - Windows Internet Explorer](getting-started-with-mvc-part3/_static/image14.png)](getting-started-with-mvc-part3/_static/image13.png)</span></span>

<span data-ttu-id="d03cf-186">모델에 대 한 일종의 "M" 이지만 데이터베이스 종류는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-186">Well, that was a kind of an "M" for Model, but not the database kind.</span></span> <span data-ttu-id="d03cf-187">학습 한 내용을 살펴보고 영화 데이터베이스를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d03cf-187">Let's take what we've learned and create a database of Movies.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d03cf-188">[이전](getting-started-with-mvc-part2.md)
> [다음](getting-started-with-mvc-part4.md)</span><span class="sxs-lookup"><span data-stu-id="d03cf-188">[Previous](getting-started-with-mvc-part2.md)
[Next](getting-started-with-mvc-part4.md)</span></span>
