---
uid: aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
title: OWIN 및 Katana 시작 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 09/27/2013
ms.assetid: 6dae249f-5ac6-4f6e-bc49-13bcd5a54a70
msc.legacyurl: /aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
msc.type: authoredcontent
ms.openlocfilehash: 4dfd7b8ebb2bb48d7ef800fd522b79a7b4a045c2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78472445"
---
# <a name="getting-started-with-owin-and-katana"></a><span data-ttu-id="837b6-102">OWIN 및 Katana 시작</span><span class="sxs-lookup"><span data-stu-id="837b6-102">Getting Started with OWIN and Katana</span></span>

<span data-ttu-id="837b6-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="837b6-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="837b6-104">[OWIN (Open Web Interface for .net)](http://owin.org/) 는 .net 웹 서버와 웹 응용 프로그램 간의 추상화를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-104">[Open Web Interface for .NET (OWIN)](http://owin.org/) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="837b6-105">웹 서버를 응용 프로그램에서 분리 하면 OWIN를 사용 하 여 .NET 웹 개발용 미들웨어를 보다 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-105">By decoupling the web server from the application, OWIN makes it easier to create middleware for .NET web development.</span></span> <span data-ttu-id="837b6-106">또한 OWIN를 사용 하면 웹 응용 프로그램을 다른 호스트로&#8212;더 쉽게 이식할 수 있습니다. 예를 들어 Windows 서비스 또는 기타 프로세스에서 자체 호스팅을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-106">Also, OWIN makes it easier to port web applications to other hosts&#8212;for example, self-hosting in a Windows service or other process.</span></span>

<span data-ttu-id="837b6-107">OWIN는 구현이 아니라 커뮤니티 소유 사양입니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-107">OWIN is a community-owned specification, not an implementation.</span></span> <span data-ttu-id="837b6-108">Katana 프로젝트는 Microsoft에서 개발 된 오픈 소스 OWIN 구성 요소 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-108">The Katana project is a set of open-source OWIN components developed by Microsoft.</span></span> <span data-ttu-id="837b6-109">OWIN 및 Katana에 대 한 일반적인 개요는 [Project Katana의 개요](an-overview-of-project-katana.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="837b6-109">For a general overview of both OWIN and Katana, see [An Overview of Project Katana](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="837b6-110">이 문서에서는 시작 하는 코드를 바로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-110">In this article, I will jump right into code to get started.</span></span>

<span data-ttu-id="837b6-111">이 자습서에서는 [Visual Studio 2013 릴리스 후보](https://go.microsoft.com/fwlink/?LinkId=306566)를 사용 하지만 Visual Studio 2012을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-111">This tutorial uses [Visual Studio 2013 Release Candidate](https://go.microsoft.com/fwlink/?LinkId=306566), but you can also use Visual Studio 2012.</span></span> <span data-ttu-id="837b6-112">몇 가지 단계는 Visual Studio 2012에서 다릅니다 .이에 대 한 자세한 내용은 아래를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="837b6-112">A few of the steps are different in Visual Studio 2012, which I note below.</span></span>

## <a name="host-owin-in-iis"></a><span data-ttu-id="837b6-113">IIS의 호스트 OWIN</span><span class="sxs-lookup"><span data-stu-id="837b6-113">Host OWIN in IIS</span></span>

<span data-ttu-id="837b6-114">이 섹션에서는 IIS에서 OWIN를 호스팅합니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-114">In this section, we'll host OWIN in IIS.</span></span> <span data-ttu-id="837b6-115">이 옵션을 사용 하면 OWIN 파이프라인의 유연성과 composability을 IIS의 완성 된 기능 집합과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-115">This option gives you the flexibility and composability of an OWIN pipeline together with the mature feature set of IIS.</span></span> <span data-ttu-id="837b6-116">이 옵션을 사용 하면 OWIN 응용 프로그램이 ASP.NET 요청 파이프라인에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-116">Using this option, the OWIN application runs in the ASP.NET request pipeline.</span></span>

<span data-ttu-id="837b6-117">먼저 새 ASP.NET 웹 응용 프로그램 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-117">First, create a new ASP.NET Web Application project.</span></span> <span data-ttu-id="837b6-118">Visual Studio 2012에서는 ASP.NET 빈 웹 응용 프로그램 프로젝트 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-118">(In Visual Studio 2012, use the ASP.NET Empty Web Application project type.)</span></span>

![](getting-started-with-owin-and-katana/_static/image1.png)

<span data-ttu-id="837b6-119">**새 ASP.NET 프로젝트** 대화 상자에서 **빈** 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-119">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span>

![](getting-started-with-owin-and-katana/_static/image2.png)

### <a name="add-nuget-packages"></a><span data-ttu-id="837b6-120">NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="837b6-120">Add NuGet Packages</span></span>

<span data-ttu-id="837b6-121">다음으로 필요한 NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-121">Next, add the required NuGet packages.</span></span> <span data-ttu-id="837b6-122">**도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-122">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="837b6-123">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-123">In the Package Manager Console window, type the following command:</span></span>

`install-package Microsoft.Owin.Host.SystemWeb –Pre`

![](getting-started-with-owin-and-katana/_static/image3.png)

### <a name="add-a-startup-class"></a><span data-ttu-id="837b6-124">시작 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="837b6-124">Add a Startup Class</span></span>

<span data-ttu-id="837b6-125">다음으로 OWIN startup 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-125">Next, add an OWIN startup class.</span></span> <span data-ttu-id="837b6-126">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 선택한 다음 **새 항목**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-126">In Solution Explorer, right-click the project and select **Add**, then select **New Item**.</span></span> <span data-ttu-id="837b6-127">**새 항목 추가** 대화 상자에서 **Owin 시작 클래스**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-127">In the **Add New Item** dialog, select **Owin Startup class**.</span></span> <span data-ttu-id="837b6-128">Startup 클래스를 구성 하는 방법에 대 한 자세한 내용은 [OWIN Startup 클래스 검색](owin-startup-class-detection.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="837b6-128">For more info on configuring the startup class, see [OWIN Startup Class Detection](owin-startup-class-detection.md).</span></span>

![](getting-started-with-owin-and-katana/_static/image4.png)

<span data-ttu-id="837b6-129">`Startup1.Configuration` 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-129">Add the following code to the `Startup1.Configuration` method:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample1.cs?highlight=3)]

<span data-ttu-id="837b6-130">이 코드는 OWIN 파이프라인에 간단한 미들웨어를 추가 합니다 .이는 **OWIN 컨텍스트** 인스턴스를 수신 하는 함수로 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-130">This code adds a simple piece of middleware to the OWIN pipeline, implemented as a function that receives a **Microsoft.Owin.IOwinContext** instance.</span></span> <span data-ttu-id="837b6-131">서버에서 HTTP 요청을 받으면 OWIN 파이프라인은 미들웨어를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-131">When the server receives an HTTP request, the OWIN pipeline invokes the middleware.</span></span> <span data-ttu-id="837b6-132">미들웨어는 응답의 콘텐츠 형식을 설정 하 고 응답 본문을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-132">The middleware sets the content type for the response and writes the response body.</span></span>

> [!NOTE]
> <span data-ttu-id="837b6-133">OWIN Startup 클래스 템플릿은 Visual Studio 2013에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-133">The OWIN Startup class template is available in Visual Studio 2013.</span></span> <span data-ttu-id="837b6-134">Visual Studio 2012을 사용 하는 경우 `Startup1`라는 비어 있는 새 클래스를 추가 하 고 다음 코드를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-134">If you are using Visual Studio 2012, just add a new empty class named `Startup1`, and paste in the following code:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample2.cs)]

### <a name="run-the-application"></a><span data-ttu-id="837b6-135">애플리케이션 실행</span><span class="sxs-lookup"><span data-stu-id="837b6-135">Run the Application</span></span>

<span data-ttu-id="837b6-136">F5를 눌러 디버깅을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-136">Press F5 to begin debugging.</span></span> <span data-ttu-id="837b6-137">Visual Studio에서 `http://localhost:*port*/`하는 브라우저 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-137">Visual Studio will open a browser window to `http://localhost:*port*/`.</span></span> <span data-ttu-id="837b6-138">페이지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-138">The page should look like the following:</span></span>

![](getting-started-with-owin-and-katana/_static/image5.png)

## <a name="self-host-owin-in-a-console-application"></a><span data-ttu-id="837b6-139">콘솔 응용 프로그램의 자체 호스트 OWIN</span><span class="sxs-lookup"><span data-stu-id="837b6-139">Self-Host OWIN in a Console Application</span></span>

<span data-ttu-id="837b6-140">사용자 지정 프로세스에서이 응용 프로그램을 IIS 호스팅에서 자체 호스팅으로 쉽게 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-140">It's easy to convert this application from IIS hosting to self-hosting in a custom process.</span></span> <span data-ttu-id="837b6-141">Iis를 호스트 하는 경우 IIS는 HTTP 서버와 서비스를 호스팅하는 프로세스 역할을 모두 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-141">With IIS hosting, IIS acts as both the HTTP server and as the process that hosts the service.</span></span> <span data-ttu-id="837b6-142">자체 호스팅을 사용 하 여 응용 프로그램은 프로세스를 만들고 **HttpListener** 클래스를 HTTP 서버로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-142">With self-hosting, your application creates the process and uses the **HttpListener** class as the HTTP server.</span></span>

<span data-ttu-id="837b6-143">Visual Studio에서 새 콘솔 애플리케이션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-143">In Visual Studio, create a new console application.</span></span> <span data-ttu-id="837b6-144">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-144">In the Package Manager Console window, type the following command:</span></span>

`Install-Package Microsoft.Owin.SelfHost -Pre`

<span data-ttu-id="837b6-145">이 자습서의 1 부에서 프로젝트에 `Startup1` 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-145">Add a `Startup1` class from part 1 of this tutorial to the project.</span></span> <span data-ttu-id="837b6-146">이 클래스는 수정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-146">You don't need to modify this class.</span></span>

<span data-ttu-id="837b6-147">응용 프로그램의 `Main` 메서드를 다음과 같이 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-147">Implement the application's `Main` method as follows.</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample3.cs)]

<span data-ttu-id="837b6-148">콘솔 응용 프로그램을 실행 하면 서버가 `http://localhost:9000`수신 대기를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-148">When you run the console application, the server starts listening to `http://localhost:9000`.</span></span> <span data-ttu-id="837b6-149">웹 브라우저에서이 주소로 이동 하면 "Hello 세계" 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-149">If you navigate to this address in a web browser, you will see the "Hello world" page.</span></span>

![](getting-started-with-owin-and-katana/_static/image6.png)

## <a name="add-owin-diagnostics"></a><span data-ttu-id="837b6-150">OWIN 진단 추가</span><span class="sxs-lookup"><span data-stu-id="837b6-150">Add OWIN Diagnostics</span></span>

<span data-ttu-id="837b6-151">Owin 패키지에는 처리 되지 않은 예외를 catch 하 고 오류 세부 정보를 포함 하는 HTML 페이지가 표시 되는 미들웨어가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-151">The Microsoft.Owin.Diagnostics package contains middleware that catches unhandled exceptions and displays an HTML page with error details.</span></span> <span data-ttu-id="837b6-152">이 페이지는 ASP.NET 오류 페이지와 매우 유사 하 게 작동 합니다 .이는 "[주황색 화면 (죽음](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow))"이 라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-152">This page functions much like the ASP.NET error page that is sometimes called the "[yellow screen of death](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)" (YSOD).</span></span> <span data-ttu-id="837b6-153">Katana 오류 페이지는 YSOD 같이 개발 중에 유용 하지만 프로덕션 모드에서 사용 하지 않도록 설정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-153">Like the YSOD, the Katana error page is useful during development, but it's a good practice to disable it in production mode.</span></span>

<span data-ttu-id="837b6-154">프로젝트에 진단 패키지를 설치 하려면 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-154">To install the Diagnostics package in your project, type the following command in the Package Manager Console window:</span></span>

`install-package Microsoft.Owin.Diagnostics –Pre`

<span data-ttu-id="837b6-155">`Startup1.Configuration` 메서드의 코드를 다음과 같이 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-155">Change the code in your `Startup1.Configuration` method as follows:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample4.cs?highlight=4,9-12)]

<span data-ttu-id="837b6-156">이제 CTRL + f 5를 사용 하 여 디버깅 하지 않고 응용 프로그램을 실행 하면 Visual Studio가 예외에서 중단 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-156">Now use CTRL+F5 to run the application without debugging, so that Visual Studio will not break on the exception.</span></span> <span data-ttu-id="837b6-157">응용 프로그램은 `http://localhost/fail`이동할 때까지 응용 프로그램에서 예외를 throw 하는 시점까지 이전과 동일 하 게 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-157">The application behaves the same as before, until you navigate to `http://localhost/fail`, at which point the application throws the exception.</span></span> <span data-ttu-id="837b6-158">오류 페이지 미들웨어는 예외를 catch 하 고 오류에 대 한 정보를 포함 하는 HTML 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-158">The error page middleware will catch the exception and display an HTML page with information about the error.</span></span> <span data-ttu-id="837b6-159">탭을 클릭 하 여 스택, 쿼리 문자열, 쿠키, 요청 헤더 및 OWIN 환경 변수를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="837b6-159">You can click the tabs to see the stack, query string, cookies, request header, and OWIN environment variables.</span></span>

![](getting-started-with-owin-and-katana/_static/image7.png)

## <a name="next-steps"></a><span data-ttu-id="837b6-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="837b6-160">Next Steps</span></span>

- [<span data-ttu-id="837b6-161">OWIN 시작 클래스 검색</span><span class="sxs-lookup"><span data-stu-id="837b6-161">OWIN Startup Class Detection</span></span>](owin-startup-class-detection.md)
- [<span data-ttu-id="837b6-162">OWIN를 사용 하 여 자체 호스트 ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="837b6-162">Use OWIN to Self-Host ASP.NET Web API</span></span>](../../../web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)
- [<span data-ttu-id="837b6-163">OWIN를 사용 하 여 자체 호스트 SignalR</span><span class="sxs-lookup"><span data-stu-id="837b6-163">Use OWIN to Self-Host SignalR</span></span>](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)
