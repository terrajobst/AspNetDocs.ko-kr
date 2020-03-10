---
uid: signalr/overview/older-versions/tutorial-getting-started-with-signalr-and-mvc-4
title: '자습서: SignalR 1.x 및 MVC 4 시작 | Microsoft Docs'
author: bradygaster
description: ASP.NET SignalR 및 ASP.NET MVC 4를 사용 하 여 실시간 채팅 응용 프로그램을 빌드합니다.
ms.author: bradyg
ms.date: 03/29/2013
ms.assetid: eeef9f73-6de3-49f9-b50b-9af22108f2ce
msc.legacyurl: /signalr/overview/older-versions/tutorial-getting-started-with-signalr-and-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 9186915df6d5de6bc20dfc0adabc54056d2f3a8c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468071"
---
# <a name="tutorial-getting-started-with-signalr-1x-and-mvc-4"></a><span data-ttu-id="04bb6-103">자습서: SignalR 1.x 및 MVC 4 시작</span><span class="sxs-lookup"><span data-stu-id="04bb6-103">Tutorial: Getting Started with SignalR 1.x and MVC 4</span></span>

<span data-ttu-id="04bb6-104">[Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span><span class="sxs-lookup"><span data-stu-id="04bb6-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="04bb6-105">이 자습서에서는 ASP.NET SignalR를 사용 하 여 실시간 채팅 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-105">This tutorial shows how to use ASP.NET SignalR to create a real-time chat application.</span></span> <span data-ttu-id="04bb6-106">MVC 4 응용 프로그램에 SignalR를 추가 하 고 메시지를 보내고 표시 하는 채팅 보기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-106">You will add SignalR to an MVC 4 application and create a chat view to send and display messages.</span></span>

## <a name="overview"></a><span data-ttu-id="04bb6-107">개요</span><span class="sxs-lookup"><span data-stu-id="04bb6-107">Overview</span></span>

<span data-ttu-id="04bb6-108">이 자습서에서는 ASP.NET SignalR 및 ASP.NET MVC 4를 사용 하 여 실시간 웹 응용 프로그램을 개발 하는 방법을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-108">This tutorial introduces you to real-time web application development with ASP.NET SignalR and ASP.NET MVC 4.</span></span> <span data-ttu-id="04bb6-109">이 자습서에서는 [SignalR 시작 자습서](tutorial-getting-started-with-signalr.md)와 동일한 채팅 응용 프로그램 코드를 사용 하지만 인터넷 템플릿을 기반으로 하는 MVC 4 응용 프로그램에 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-109">The tutorial uses the same chat application code as the [SignalR Getting Started tutorial](tutorial-getting-started-with-signalr.md), but shows how to add it to an MVC 4 application based on the Internet template.</span></span>

<span data-ttu-id="04bb6-110">이 항목에서는 다음과 같은 SignalR 개발 작업에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-110">In this topic you will learn the following SignalR development tasks:</span></span>

- <span data-ttu-id="04bb6-111">SignalR 라이브러리를 MVC 4 응용 프로그램에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-111">Adding the SignalR library to an MVC 4 application.</span></span>
- <span data-ttu-id="04bb6-112">클라이언트에 콘텐츠를 푸시하는 허브 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="04bb6-112">Creating a hub class to push content to clients.</span></span>
- <span data-ttu-id="04bb6-113">웹 페이지에서 SignalR jQuery 라이브러리를 사용 하 여 메시지를 보내고 허브에서 업데이트를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-113">Using the SignalR jQuery library in a web page to send messages and display updates from the hub.</span></span>

<span data-ttu-id="04bb6-114">다음 스크린샷은 브라우저에서 실행 되는 완료 된 채팅 응용 프로그램을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-114">The following screen shot shows the completed chat application running in a browser.</span></span>

![채팅 인스턴스](tutorial-getting-started-with-signalr-and-mvc-4/_static/image2.png)

<span data-ttu-id="04bb6-116">섹션이</span><span class="sxs-lookup"><span data-stu-id="04bb6-116">Sections:</span></span>

- [<span data-ttu-id="04bb6-117">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="04bb6-117">Set up the Project</span></span>](#setup)
- [<span data-ttu-id="04bb6-118">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="04bb6-118">Run the Sample</span></span>](#run)
- [<span data-ttu-id="04bb6-119">코드 검사</span><span class="sxs-lookup"><span data-stu-id="04bb6-119">Examine the Code</span></span>](#code)
- [<span data-ttu-id="04bb6-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="04bb6-120">Next Steps</span></span>](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a><span data-ttu-id="04bb6-121">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="04bb6-121">Set up the Project</span></span>

<span data-ttu-id="04bb6-122">필수 조건:</span><span class="sxs-lookup"><span data-stu-id="04bb6-122">Prerequisites:</span></span>

- <span data-ttu-id="04bb6-123">Visual Studio 2010 SP1, Visual Studio 2012 또는 Visual Studio 2012 Express</span><span class="sxs-lookup"><span data-stu-id="04bb6-123">Visual Studio 2010 SP1, Visual Studio 2012, or Visual Studio 2012 Express.</span></span> <span data-ttu-id="04bb6-124">Visual Studio가 없는 경우 [ASP.NET 다운로드](https://www.asp.net/downloads) 를 참조 하 여 무료 visual Studio 2012 Express 개발 도구를 다운로드 하세요.</span><span class="sxs-lookup"><span data-stu-id="04bb6-124">If you do not have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2012 Express Development Tool.</span></span>
- <span data-ttu-id="04bb6-125">Visual Studio 2010의 경우 [ASP.NET MVC 4](https://www.microsoft.com/download/details.aspx?id=30683)를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-125">For Visual Studio 2010, install [ASP.NET MVC 4](https://www.microsoft.com/download/details.aspx?id=30683).</span></span>

<span data-ttu-id="04bb6-126">이 섹션에서는 ASP.NET MVC 4 응용 프로그램을 만들고, SignalR 라이브러리를 추가 하 고, 채팅 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-126">This section shows how to create an ASP.NET MVC 4 application, add the SignalR library, and create the chat application.</span></span>

1. 1. <span data-ttu-id="04bb6-127">Visual Studio에서 ASP.NET MVC 4 응용 프로그램을 만들고, 이름을 SignalRChat로, 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-127">In Visual Studio create an ASP.NET MVC 4 application, name it SignalRChat, and click OK.</span></span>

        > [!NOTE]
        > <span data-ttu-id="04bb6-128">VS 2010의 프레임 워크 버전 드롭다운 컨트롤에서 **.NET Framework 4** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-128">In VS 2010, select **.NET Framework 4** in the Framework version dropdown control.</span></span> <span data-ttu-id="04bb6-129">SignalR 코드는 .NET Framework 버전 4 및 4.5에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-129">SignalR code runs on .NET Framework versions 4 and 4.5.</span></span>

        ![Mvc 웹 만들기](tutorial-getting-started-with-signalr-and-mvc-4/_static/image3.png)
      2. <span data-ttu-id="04bb6-131">인터넷 응용 프로그램 템플릿을 선택 하 고 **단위 테스트 프로젝트를 만드는**옵션을 선택 취소 한 다음 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-131">Select the Internet Application template, clear the option to **Create a unit test project**, and click OK.</span></span>

         ![Mvc 인터넷 사이트 만들기](tutorial-getting-started-with-signalr-and-mvc-4/_static/image4.png)
      3. <span data-ttu-id="04bb6-133">**패키지 관리자 콘솔 > NuGet 패키지 관리자 > 도구** 를 열고 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-133">Open the **Tools > NuGet Package Manager > Package Manager Console** and run the following command.</span></span> <span data-ttu-id="04bb6-134">이 단계에서는 SignalR 기능을 사용할 수 있도록 하는 스크립트 파일 및 어셈블리 참조 집합을 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-134">This step adds to the project a set of script files and assembly references that enable SignalR functionality.</span></span>

         `install-package Microsoft.AspNet.SignalR -Version 1.1.3`
      4. <span data-ttu-id="04bb6-135">**솔루션 탐색기** 에서 Scripts 폴더를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-135">In **Solution Explorer** expand the Scripts folder.</span></span> <span data-ttu-id="04bb6-136">SignalR에 대 한 스크립트 라이브러리는 프로젝트에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-136">Note that script libraries for SignalR have been added to the project.</span></span>

         ![라이브러리 참조](tutorial-getting-started-with-signalr-and-mvc-4/_static/image6.png)
      5. <span data-ttu-id="04bb6-138">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 새 폴더**를 추가 하 고 **허브**라는 새 폴더를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-138">In **Solution Explorer**, right-click the project, select **Add | New Folder**, and add a new folder named **Hubs**.</span></span>
      6. <span data-ttu-id="04bb6-139">**허브** 폴더를 마우스 오른쪽 단추로 클릭 하 고 추가를 클릭 합니다.  **클래스**를 만들고 ChatHub.cs 이라는 새 C# 클래스를만듭니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-139">Right-click the **Hubs** folder, click **Add | Class**, and create a new C# class named **ChatHub.cs**.</span></span> <span data-ttu-id="04bb6-140">모든 클라이언트에 메시지를 보내는 SignalR 서버 허브로이 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-140">You will use this class as a SignalR server hub that sends messages to all clients.</span></span>

> [!NOTE]
> <span data-ttu-id="04bb6-141">Visual Studio 2012을 사용 하 고 [ASP.NET 및 Web Tools 2012.2 업데이트](../../../visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw.md#_Installation)를 설치한 경우 새 SignalR 항목 템플릿을 사용 하 여 허브 클래스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-141">If you use Visual Studio 2012 and have installed the [ASP.NET and Web Tools 2012.2 update](../../../visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw.md#_Installation), you can use the new SignalR item template to create the hub class.</span></span> <span data-ttu-id="04bb6-142">이렇게 하려면 **허브** 폴더를 마우스 오른쪽 단추로 클릭 하 고 추가를 클릭 합니다.  **새 항목**에서 **SignalR Hub 클래스 (v1)** 를 선택 하 고 클래스 이름을 **ChatHub.cs**로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-142">To do that, right-click the **Hubs** folder, click **Add | New Item**, select **SignalR Hub Class (v1)**, and name the class **ChatHub.cs**.</span></span>

1. <span data-ttu-id="04bb6-143">**ChatHub** 클래스의 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-143">Replace the code in the **ChatHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample1.cs)]
2. <span data-ttu-id="04bb6-144">프로젝트에 대 한 global.asax 파일을 열고 메서드 `RouteTable.Routes.MapHubs();`에 대 한 호출을 `Application_Start` 메서드의 코드의 첫 번째 줄로 **추가 합니다.**</span><span class="sxs-lookup"><span data-stu-id="04bb6-144">Open the **Global.asax** file for the project, and add a call to the method `RouteTable.Routes.MapHubs();` as the first line of code in the `Application_Start` method.</span></span> <span data-ttu-id="04bb6-145">이 코드는 SignalR hubs의 기본 경로를 등록 하며 다른 경로를 등록 하기 전에 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-145">This code registers the default route for SignalR hubs and must be called before you register any other routes.</span></span> <span data-ttu-id="04bb6-146">완료 된 `Application_Start` 메서드는 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-146">The completed `Application_Start` method looks like the following example.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample2.cs)]
3. <span data-ttu-id="04bb6-147">**Controllers/HomeController** 에 있는 `HomeController` 클래스를 편집 하 고 클래스에 다음 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-147">Edit the `HomeController` class found in **Controllers/HomeController.cs** and add the following method to the class.</span></span> <span data-ttu-id="04bb6-148">이 메서드는 이후 단계에서 만들 **채팅** 보기를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-148">This method returns the **Chat** view that you will create in a later step.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample3.cs)]
4. <span data-ttu-id="04bb6-149">방금 만든 `Chat` 메서드 내에서 마우스 오른쪽 단추를 클릭 하 고 **뷰 추가** 를 클릭 하 여 새 뷰 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-149">Right-click within the `Chat` method you just created, and click **Add View** to create a new view file.</span></span>
5. <span data-ttu-id="04bb6-150">**보기 추가** 대화 상자에서 **레이아웃 또는 마스터 페이지** (다른 확인란의 선택을 취소)를 사용 하도록 확인란을 선택 했는지 확인 한 다음 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-150">In the **Add View** dialog, make sure the check box is selected to **Use a layout or master page** (clear the other check boxes), and then click **Add**.</span></span>

    ![보기 추가](tutorial-getting-started-with-signalr-and-mvc-4/_static/image8.png)
6. <span data-ttu-id="04bb6-152">**Chat. cshtml**이라는 새 뷰 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-152">Edit the new view file named **Chat.cshtml**.</span></span> <span data-ttu-id="04bb6-153">&lt;h2&gt; 태그 뒤에 다음 &lt;div&gt; 섹션 및 `@section scripts` 코드 블록을 페이지에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-153">After the &lt;h2&gt; tag, paste the following &lt;div&gt; section and `@section scripts` code block into the page.</span></span> <span data-ttu-id="04bb6-154">이 스크립트를 사용 하면 페이지에서 채팅 메시지를 보내고 서버에서 메시지를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-154">This script enables the page to send chat messages and display messages from the server.</span></span> <span data-ttu-id="04bb6-155">채팅 보기의 전체 코드는 다음 코드 블록에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-155">The complete code for the chat view appears in the following code block.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="04bb6-156">SignalR 및 기타 스크립트 라이브러리를 Visual Studio 프로젝트에 추가 하는 경우 패키지 관리자는이 항목에 표시 된 버전 보다 최신 버전의 스크립트를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-156">When you add SignalR and other script libraries to your Visual Studio project, the Package Manager might install versions of the scripts that are more recent than the versions shown in this topic.</span></span> <span data-ttu-id="04bb6-157">코드의 스크립트 참조가 프로젝트에 설치 된 스크립트 라이브러리 버전과 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-157">Make sure that the script references in your code match the versions of the script libraries installed in your project.</span></span>

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample4.cshtml)]
7. <span data-ttu-id="04bb6-158">프로젝트에 대 한 **모든를 저장** 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-158">**Save All** for the project.</span></span>

<a id="run"></a>

## <a name="run-the-sample"></a><span data-ttu-id="04bb6-159">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="04bb6-159">Run the Sample</span></span>

1. <span data-ttu-id="04bb6-160">F5 키를 눌러 디버그 모드에서 프로젝트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-160">Press F5 to run the project in debug mode.</span></span>
2. <span data-ttu-id="04bb6-161">브라우저 주소 줄에서 프로젝트에 대 한 기본 페이지의 URL에 **/home/chat** 를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-161">In the browser address line, append **/home/chat** to the URL of the default page for the project.</span></span> <span data-ttu-id="04bb6-162">채팅 페이지가 브라우저 인스턴스에 로드 되 고 사용자 이름을 입력 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-162">The Chat page loads in a browser instance and prompts for a user name.</span></span>

    ![사용자 이름 입력](tutorial-getting-started-with-signalr-and-mvc-4/_static/image9.png)
3. <span data-ttu-id="04bb6-164">사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-164">Enter a user name.</span></span>
4. <span data-ttu-id="04bb6-165">브라우저의 주소 줄에서 URL을 복사 하 고이를 사용 하 여 두 개의 브라우저 인스턴스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-165">Copy the URL from the address line of the browser and use it to open two more browser instances.</span></span> <span data-ttu-id="04bb6-166">각 브라우저 인스턴스에서 고유한 사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-166">In each browser instance, enter a unique user name.</span></span>
5. <span data-ttu-id="04bb6-167">각 브라우저 인스턴스에서 주석을 추가 하 고 **보내기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-167">In each browser instance, add a comment and click **Send**.</span></span> <span data-ttu-id="04bb6-168">주석은 모든 브라우저 인스턴스에 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-168">The comments should display in all browser instances.</span></span>

    > [!NOTE]
    > <span data-ttu-id="04bb6-169">이 간단한 채팅 응용 프로그램은 서버에 대 한 토론 컨텍스트를 유지 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-169">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="04bb6-170">허브는 모든 현재 사용자에 게 주석을 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-170">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="04bb6-171">나중에 채팅에 참여 하는 사용자는 연결 된 시간부터 추가 된 메시지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-171">Users who join the chat later will see messages added from the time they join.</span></span>
6. <span data-ttu-id="04bb6-172">다음 스크린샷은 브라우저에서 실행 중인 채팅 응용 프로그램을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-172">The following screen shot shows the chat application running in a browser.</span></span>

    ![채팅 브라우저](tutorial-getting-started-with-signalr-and-mvc-4/_static/image11.png)
7. <span data-ttu-id="04bb6-174">**솔루션 탐색기**에서 실행 중인 응용 프로그램에 대 한 **스크립트 문서** 노드를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-174">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="04bb6-175">Internet Explorer를 브라우저로 사용 하는 경우이 노드가 디버그 모드에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-175">This node is visible in debug mode if you are using Internet Explorer as your browser.</span></span> <span data-ttu-id="04bb6-176">SignalR 라이브러리가 런타임에 동적으로 생성 하는 **허브** 라는 스크립트 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-176">There is a script file named **hubs** that the SignalR library dynamically generates at runtime.</span></span> <span data-ttu-id="04bb6-177">이 파일은 jQuery 스크립트와 서버측 코드 간의 통신을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-177">This file manages the communication between jQuery script and server-side code.</span></span> <span data-ttu-id="04bb6-178">Internet Explorer 이외의 브라우저를 사용 하는 경우 동적 **허브** 파일을 직접 탐색 하 여 액세스할 수도 있습니다 (예: http://mywebsite/signalr/hubs).</span><span class="sxs-lookup"><span data-stu-id="04bb6-178">If you use a browser other than Internet Explorer, you can also access the dynamic **hubs** file by browsing to it directly, for example http://mywebsite/signalr/hubs.</span></span>

    ![생성 된 허브 스크립트](tutorial-getting-started-with-signalr-and-mvc-4/_static/image13.png)

<a id="code"></a>

## <a name="examine-the-code"></a><span data-ttu-id="04bb6-180">코드 검사</span><span class="sxs-lookup"><span data-stu-id="04bb6-180">Examine the Code</span></span>

<span data-ttu-id="04bb6-181">SignalR chat 응용 프로그램은 서버에서 주 조정 개체로 허브를 만들고 SignalR jQuery 라이브러리를 사용 하 여 메시지를 보내고 받는 두 가지 기본 SignalR 개발 작업을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-181">The SignalR chat application demonstrates two basic SignalR development tasks: creating a hub as the main coordination object on the server, and using the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs"></a><span data-ttu-id="04bb6-182">SignalR 허브</span><span class="sxs-lookup"><span data-stu-id="04bb6-182">SignalR Hubs</span></span>

<span data-ttu-id="04bb6-183">코드 샘플에서 **ChatHub** 클래스는 **SignalR** 클래스에서 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-183">In the code sample the **ChatHub** class derives from the **Microsoft.AspNet.SignalR.Hub** class.</span></span> <span data-ttu-id="04bb6-184">**허브** 클래스에서 파생 하는 것은 SignalR 응용 프로그램을 빌드하는 데 유용한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-184">Deriving from the **Hub** class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="04bb6-185">허브 클래스에서 공용 메서드를 만든 다음 웹 페이지의 jQuery 스크립트에서 해당 메서드를 호출 하 여 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-185">You can create public methods on your hub class and then access those methods by calling them from jQuery scripts in a web page.</span></span>

<span data-ttu-id="04bb6-186">채팅 코드에서 클라이언트는 **ChatHub** 메서드를 호출 하 여 새 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-186">In the chat code, clients call the **ChatHub.Send** method to send a new message.</span></span> <span data-ttu-id="04bb6-187">그러면 허브는 **addNewMessageToPage**를 호출 하 여 모든 클라이언트에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-187">The hub in turn sends the message to all clients by calling **Clients.All.addNewMessageToPage**.</span></span>

<span data-ttu-id="04bb6-188">**Send** 메서드는 다음과 같은 몇 가지 허브 개념을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-188">The **Send** method demonstrates several hub concepts :</span></span>

- <span data-ttu-id="04bb6-189">클라이언트에서 호출할 수 있도록 허브에 공용 메서드를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-189">Declare public methods on a hub so that clients can call them.</span></span>
- <span data-ttu-id="04bb6-190">**SignalR** 속성을 사용 하 여이 허브에 연결 된 모든 클라이언트에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-190">Use the **Microsoft.AspNet.SignalR.Hub.Clients** property to access all clients connected to this hub.</span></span>
- <span data-ttu-id="04bb6-191">클라이언트 (예: `addNewMessageToPage` 함수)에서 jQuery 함수를 호출 하 여 클라이언트를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-191">Call a jQuery function on the client (such as the `addNewMessageToPage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a><span data-ttu-id="04bb6-192">SignalR 및 jQuery</span><span class="sxs-lookup"><span data-stu-id="04bb6-192">SignalR and jQuery</span></span>

<span data-ttu-id="04bb6-193">코드 샘플의 SignalR jQuery 뷰 파일은 SignalR hub와 통신 하는 데 jQuery 라이브러리를 사용 **하는 방법을** 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-193">The **Chat.cshtml** view file in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="04bb6-194">코드의 필수 작업은 허브에 대해 자동 생성 된 프록시에 대 한 참조를 만들고, 서버에서 클라이언트에 콘텐츠를 푸시하는 데 사용할 수 있는 함수를 선언 하 고, 허브로 메시지를 보내기 위한 연결을 시작 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-194">The essential tasks in the code are creating a reference to the auto-generated proxy for the hub, declaring a function that the server can call to push content to clients, and starting a connection to send messages to the hub.</span></span>

<span data-ttu-id="04bb6-195">다음 코드는 허브에 대 한 프록시를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-195">The following code declares a proxy for a hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample6.js)]

> [!NOTE]
> <span data-ttu-id="04bb6-196">JQuery에서 서버 클래스 및 해당 멤버에 대 한 참조는 카멜식 대/소문자로 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-196">In jQuery the reference to the server class and its members is in camel case.</span></span> <span data-ttu-id="04bb6-197">코드 샘플은 jQuery의 C# **ChatHub** 클래스를 **ChatHub**로 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-197">The code sample references the C# **ChatHub** class in jQuery as **chatHub**.</span></span> <span data-ttu-id="04bb6-198">에서 C#와 같이 기존 파스칼식 대/소문자를 사용 하 여 jQuery에서 `ChatHub` 클래스를 참조 하려면 ChatHub.cs 클래스 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-198">If you want to reference the `ChatHub` class in jQuery with conventional Pascal casing as you would in C#, edit the ChatHub.cs class file.</span></span> <span data-ttu-id="04bb6-199">`Microsoft.AspNet.SignalR.Hubs` 네임 스페이스를 참조 하는 `using` 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-199">Add a `using` statement to reference the `Microsoft.AspNet.SignalR.Hubs` namespace.</span></span> <span data-ttu-id="04bb6-200">그런 다음 `ChatHub` 클래스에 `HubName` 특성을 추가 합니다 (예: `[HubName("ChatHub")]`).</span><span class="sxs-lookup"><span data-stu-id="04bb6-200">Then add the `HubName` attribute to the `ChatHub` class, for example `[HubName("ChatHub")]`.</span></span> <span data-ttu-id="04bb6-201">마지막으로 `ChatHub` 클래스에 대 한 jQuery 참조를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-201">Finally, update your jQuery reference to the `ChatHub` class.</span></span>

<span data-ttu-id="04bb6-202">다음 코드에서는 스크립트에서 콜백 함수를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-202">The following code shows how to create a callback function in the script.</span></span> <span data-ttu-id="04bb6-203">서버의 허브 클래스는이 함수를 호출 하 여 각 클라이언트에 콘텐츠 업데이트를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-203">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="04bb6-204">`htmlEncode` 함수에 대 한 선택적 호출에서는 스크립트 삽입을 방지 하는 방법으로 메시지 내용을 페이지에 표시 하기 전에 HTML로 인코딩하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-204">The optional call to the `htmlEncode` function shows a way to HTML encode the message content before displaying it in the page, as a way to prevent script injection.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample7.html)]

<span data-ttu-id="04bb6-205">다음 코드에서는 허브와의 연결을 여는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-205">The following code shows how to open a connection with the hub.</span></span> <span data-ttu-id="04bb6-206">이 코드는 연결을 시작한 다음 채팅 페이지의 **보내기** 단추에서 클릭 이벤트를 처리 하는 함수를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-206">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the Chat page.</span></span>

> [!NOTE]
> <span data-ttu-id="04bb6-207">이 방법을 사용 하면 이벤트 처리기가 실행 되기 전에 연결이 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-207">This approach ensures that the connection is established before the event handler executes.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a><span data-ttu-id="04bb6-208">다음 단계</span><span class="sxs-lookup"><span data-stu-id="04bb6-208">Next Steps</span></span>

<span data-ttu-id="04bb6-209">SignalR는 실시간 웹 응용 프로그램을 빌드하기 위한 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-209">You learned that SignalR is a framework for building real-time web applications.</span></span> <span data-ttu-id="04bb6-210">또한 ASP.NET 응용 프로그램에 SignalR를 추가 하는 방법, 허브 클래스를 만드는 방법 및 허브에서 메시지를 보내고 받는 방법에 대 한 몇 가지 SignalR 개발 작업을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="04bb6-210">You also learned several SignalR development tasks: how to add SignalR to an ASP.NET application, how to create a hub class, and how to send and receive messages from the hub.</span></span>

<span data-ttu-id="04bb6-211">고급 SignalR 개발 개념에 대 한 자세한 내용은 다음 사이트에서 SignalR 소스 코드 및 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="04bb6-211">To learn more advanced SignalR developments concepts, visit the following sites for SignalR source code and resources :</span></span>

- [<span data-ttu-id="04bb6-212">SignalR 프로젝트</span><span class="sxs-lookup"><span data-stu-id="04bb6-212">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="04bb6-213">SignalR Github 및 샘플</span><span class="sxs-lookup"><span data-stu-id="04bb6-213">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="04bb6-214">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="04bb6-214">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
