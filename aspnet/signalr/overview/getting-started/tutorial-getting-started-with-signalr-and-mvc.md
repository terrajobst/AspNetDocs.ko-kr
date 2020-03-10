---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
title: '자습서: SignalR 2 및 MVC 5와 실시간 채팅 | Microsoft Docs'
author: bradygaster
description: 이 자습서에서는 ASP.NET SignalR 2를 사용 하 여 실시간 채팅 응용 프로그램을 만드는 방법을 보여 줍니다. MVC 5 응용 프로그램에 SignalR를 추가 합니다.
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: 80bfe5fb-bdfc-41fe-ac43-2132e5d69fac
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: 5671e4f0123ca2b0cb5314336cf4411467feac70
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431621"
---
# <a name="tutorial-real-time-chat-with-signalr-2-and-mvc-5"></a><span data-ttu-id="1b147-104">자습서: SignalR 2 및 MVC 5와 실시간 채팅</span><span class="sxs-lookup"><span data-stu-id="1b147-104">Tutorial: Real-time chat with SignalR 2 and MVC 5</span></span>

<span data-ttu-id="1b147-105">이 자습서에서는 ASP.NET SignalR 2를 사용 하 여 실시간 채팅 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-105">This tutorial shows how to use ASP.NET SignalR 2 to create a real-time chat application.</span></span> <span data-ttu-id="1b147-106">MVC 5 응용 프로그램에 SignalR를 추가 하 고 메시지를 보내고 표시 하는 채팅 보기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-106">You add SignalR to an MVC 5 application and create a chat view to send and display messages.</span></span>

<span data-ttu-id="1b147-107">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-107">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1b147-108">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="1b147-108">Set up the project</span></span>
> * <span data-ttu-id="1b147-109">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="1b147-109">Run the sample</span></span>
> * <span data-ttu-id="1b147-110">코드 검사</span><span class="sxs-lookup"><span data-stu-id="1b147-110">Examine the code</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a><span data-ttu-id="1b147-111">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="1b147-111">Prerequisites</span></span>

* <span data-ttu-id="1b147-112">[ASP.NET 및 웹 개발](https://visualstudio.microsoft.com/downloads/) 워크로드가 있는 **Visual Studio 2017**</span><span class="sxs-lookup"><span data-stu-id="1b147-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="set-up-the-project"></a><span data-ttu-id="1b147-113">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="1b147-113">Set up the Project</span></span>

<span data-ttu-id="1b147-114">이 섹션에서는 Visual Studio 2017 및 SignalR 2를 사용 하 여 빈 ASP.NET MVC 5 응용 프로그램을 만들고 SignalR 라이브러리를 추가 하 고 채팅 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-114">This section shows how to use Visual Studio 2017 and SignalR 2 to create an empty ASP.NET MVC 5 application, add the SignalR library, and create the chat application.</span></span>

1. <span data-ttu-id="1b147-115">Visual Studio에서 .NET Framework 4.5를 C# 대상으로 하는 ASP.NET 응용 프로그램을 만들고 이름을 SignalRChat로 지정 하 고 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-115">In Visual Studio, create a C# ASP.NET application that targets .NET Framework 4.5, name it SignalRChat, and click OK.</span></span>

    ![웹 만들기](tutorial-getting-started-with-signalr-and-mvc/_static/image1.png)

1. <span data-ttu-id="1b147-117">**New ASP.NET 웹 응용 프로그램-SignalRMvcChat**에서 **MVC** 를 선택 하 고 **인증 변경**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-117">In **New ASP.NET Web Application - SignalRMvcChat**, select **MVC** and then select **Change Authentication**.</span></span>

1. <span data-ttu-id="1b147-118">**변경 인증**에서 **인증 안 함** 을 선택 하 고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-118">In **Change Authentication**, select **No Authentication** and click **OK**.</span></span>

    ![인증 안 함 선택](tutorial-getting-started-with-signalr-and-mvc/_static/image2.png)

1. <span data-ttu-id="1b147-120">**New ASP.NET 웹 응용 프로그램-SignalRMvcChat**에서 **확인**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-120">In **New ASP.NET Web Application - SignalRMvcChat**, select **OK**.</span></span>

1. <span data-ttu-id="1b147-121">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가** > **새 항목**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-121">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="1b147-122">**새 항목 추가-SignalRChat**에서 **설치** > **Visual C#**  > **Web** > **SignalR** 을 선택한 다음 **SignalR Hub 클래스 (v2)** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-122">In **Add New Item - SignalRChat**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="1b147-123">클래스 이름을 *ChatHub* 로 추가 하 고 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-123">Name the class *ChatHub* and add it to the project.</span></span>

    <span data-ttu-id="1b147-124">이 단계에서는 *ChatHub.cs* 클래스 파일을 만들고 SignalR을 지 원하는 스크립트 파일 및 어셈블리 참조 집합을 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-124">This step creates the *ChatHub.cs* class file and adds a set of script files and assembly references that support SignalR to the project.</span></span>

1. <span data-ttu-id="1b147-125">새 *ChatHub.cs* 클래스 파일의 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-125">Replace the code in the new *ChatHub.cs* class file with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample1.cs)]

1. <span data-ttu-id="1b147-126">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 > **클래스** **추가** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-126">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="1b147-127">새 클래스의 이름을 *시작* 하 고 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-127">Name the new class *Startup* and add it to the project.</span></span>

1. <span data-ttu-id="1b147-128">*Startup.cs* 클래스 파일의 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-128">Replace the code in the *Startup.cs* class file with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample2.cs)]

1. <span data-ttu-id="1b147-129">**솔루션 탐색기**에서 **컨트롤러** > **HomeController.cs**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-129">In **Solution Explorer**, select **Controllers** > **HomeController.cs**.</span></span>

1. <span data-ttu-id="1b147-130">*HomeController.cs*에이 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-130">Add this method to the *HomeController.cs*.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample3.cs)]

    <span data-ttu-id="1b147-131">이 메서드는 이후 단계에서 만든 **채팅** 보기를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-131">This method returns the **Chat** view that you create in a later step.</span></span>

1. <span data-ttu-id="1b147-132">**솔루션 탐색기**에서 **보기** > **홈**을 마우스 오른쪽 단추로 클릭 하 고 >  **보기** **추가** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-132">In **Solution Explorer**, right-click **Views** > **Home**, and select **Add** >  **View**.</span></span>

1. <span data-ttu-id="1b147-133">**보기 추가**에서 새 보기 **채팅** 의 이름을로 표시 하 고 **추가**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-133">In **Add View**, name the new view **Chat** and select **Add**.</span></span>

1. <span data-ttu-id="1b147-134">**채팅** 의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-134">Replace the contents of **Chat.cshtml** with this code:</span></span>

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample4.cshtml)]

1. <span data-ttu-id="1b147-135">**솔루션 탐색기**에서 **스크립트**를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-135">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="1b147-136">JQuery 및 SignalR에 대 한 스크립트 라이브러리는 프로젝트에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-136">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="1b147-137">패키지 관리자가 SignalR 스크립트의 최신 버전을 설치 했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-137">The package manager may have installed a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="1b147-138">코드 블록의 스크립트 참조가 프로젝트의 스크립트 파일 버전에 해당 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-138">Check that the script references in the code block correspond to the versions of the script files in the project.</span></span>

    <span data-ttu-id="1b147-139">원본 코드 블록의 스크립트 참조:</span><span class="sxs-lookup"><span data-stu-id="1b147-139">Script references from the original code block:</span></span>

    ```cshtml
    <!--Script references. -->
    <!--The jQuery library is required and is referenced by default in _Layout.cshtml. -->
    <!--Reference the SignalR library. -->
    <script src="~/Scripts/jquery.signalR-2.1.0.min.js"></script>
    ```

1. <span data-ttu-id="1b147-140">일치 하지 않는 경우에는 *cshtml* 파일을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-140">If they don't match, update the *.cshtml* file.</span></span>

1. <span data-ttu-id="1b147-141">메뉴 모음에서 **파일** > **모두 저장**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-141">From the menu bar, select **File** > **Save All**.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="1b147-142">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="1b147-142">Run the Sample</span></span>

1. <span data-ttu-id="1b147-143">도구 모음에서 **스크립트 디버깅** 을 사용 하도록 설정 하 고 재생 단추를 선택 하 여 디버그 모드에서 샘플을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-143">In the toolbar, turn on **Script Debugging** and then select the play button to run the sample in Debug mode.</span></span>

    ![사용자 이름 입력](tutorial-getting-started-with-signalr-and-mvc/_static/image3.png)

1. <span data-ttu-id="1b147-145">브라우저가 열리면 채팅 id의 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-145">When the browser opens, enter a name for your chat identity.</span></span>

1. <span data-ttu-id="1b147-146">브라우저에서 URL을 복사 하 여 다른 두 브라우저를 열고 Url을 주소 표시줄에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-146">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="1b147-147">각 브라우저에서 고유한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-147">In each browser, enter a unique name.</span></span>

1. <span data-ttu-id="1b147-148">이제 주석을 추가 하 고 **보내기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-148">Now, add a comment and select **Send**.</span></span> <span data-ttu-id="1b147-149">다른 브라우저에서 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-149">Repeat that in the other browsers.</span></span> <span data-ttu-id="1b147-150">주석은 실시간으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-150">The comments appear in real time.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1b147-151">이 간단한 채팅 응용 프로그램은 서버에 대 한 토론 컨텍스트를 유지 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-151">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="1b147-152">허브는 모든 현재 사용자에 게 주석을 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-152">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="1b147-153">나중에 채팅에 참여 하는 사용자는 연결 된 시간부터 추가 된 메시지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-153">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="1b147-154">채팅 응용 프로그램이 세 가지 브라우저에서 어떻게 실행 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-154">See how the chat application runs in three different browsers.</span></span> <span data-ttu-id="1b147-155">Tom, Anand 및 김소미로 메시지를 보내면 모든 브라우저가 실시간으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-155">When Tom, Anand, and Susan send messages, all browsers update in real time:</span></span>

    ![세 브라우저 모두 동일한 채팅 기록을 표시 합니다.](tutorial-getting-started-with-signalr-and-mvc/_static/image4.png)

1. <span data-ttu-id="1b147-157">**솔루션 탐색기**에서 실행 중인 응용 프로그램에 대 한 **스크립트 문서** 노드를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-157">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="1b147-158">SignalR 라이브러리가 런타임에 생성 하는 *허브* 라는 스크립트 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-158">There's a script file named *hubs* that the SignalR library generates at runtime.</span></span> <span data-ttu-id="1b147-159">이 파일은 jQuery 스크립트와 서버측 코드 간의 통신을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-159">This file manages the communication between jQuery script and server-side code.</span></span>

    ![스크립트 문서 노드의 자동 생성 된 허브 스크립트](tutorial-getting-started-with-signalr-and-mvc/_static/image5.png)

## <a name="examine-the-code"></a><span data-ttu-id="1b147-161">코드 검사</span><span class="sxs-lookup"><span data-stu-id="1b147-161">Examine the Code</span></span>

<span data-ttu-id="1b147-162">SignalR chat 응용 프로그램은 두 가지 기본 SignalR 개발 작업을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-162">The SignalR chat application demonstrates two basic SignalR development tasks.</span></span> <span data-ttu-id="1b147-163">허브를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-163">It shows you how to create a hub.</span></span> <span data-ttu-id="1b147-164">서버는 주 조정 개체로 해당 허브를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-164">The server uses that hub as the main coordination object.</span></span> <span data-ttu-id="1b147-165">허브는 SignalR jQuery 라이브러리를 사용 하 여 메시지를 보내고 받습니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-165">The hub uses the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs-in-the-chathubcs"></a><span data-ttu-id="1b147-166">ChatHub.cs의 SignalR Hubs</span><span class="sxs-lookup"><span data-stu-id="1b147-166">SignalR Hubs in the ChatHub.cs</span></span>

<span data-ttu-id="1b147-167">코드 샘플에서 `ChatHub` 클래스는 `Microsoft.AspNet.SignalR.Hub` 클래스에서 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-167">In the code sample, the `ChatHub` class derives from the `Microsoft.AspNet.SignalR.Hub` class.</span></span> <span data-ttu-id="1b147-168">`Hub` 클래스에서 파생 하는 것은 SignalR 응용 프로그램을 빌드하는 데 유용한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-168">Deriving from the `Hub` class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="1b147-169">허브 클래스에서 공용 메서드를 만든 다음 웹 페이지의 스크립트에서 해당 메서드를 호출 하 여 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-169">You can create public methods on your hub class and then access those methods by calling them from scripts in a web page.</span></span>

<span data-ttu-id="1b147-170">채팅 코드에서 클라이언트는 `ChatHub.Send` 메서드를 호출 하 여 새 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-170">In the chat code, clients call the `ChatHub.Send` method to send a new message.</span></span> <span data-ttu-id="1b147-171">그런 다음 허브는 `Clients.All.addNewMessageToPage`를 호출 하 여 모든 클라이언트에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-171">The hub in turn sends the message to all clients by calling `Clients.All.addNewMessageToPage`.</span></span>

<span data-ttu-id="1b147-172">`Send` 메서드는 다음과 같은 몇 가지 허브 개념을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-172">The `Send` method demonstrates several hub concepts:</span></span>

* <span data-ttu-id="1b147-173">클라이언트에서 호출할 수 있도록 허브에 공용 메서드를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-173">Declare public methods on a hub so that clients can call them.</span></span>

* <span data-ttu-id="1b147-174">`Microsoft.AspNet.SignalR.Hub.Clients` 동적 속성을 사용 하 여이 허브에 연결 된 모든 클라이언트와 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-174">Use the `Microsoft.AspNet.SignalR.Hub.Clients` dynamic property to communicate with all clients connected to this hub.</span></span>

* <span data-ttu-id="1b147-175">클라이언트에서 함수 (예: `addNewMessageToPage` 함수)를 호출 하 여 클라이언트를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-175">Call a function on the client (like the `addNewMessageToPage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample5.cs)]

### <a name="signalr-and-jquery-chatcshtml"></a><span data-ttu-id="1b147-176">SignalR 및 jQuery 채팅. cshtml</span><span class="sxs-lookup"><span data-stu-id="1b147-176">SignalR and jQuery Chat.cshtml</span></span>

<span data-ttu-id="1b147-177">코드 샘플의 SignalR jQuery 뷰 파일은 SignalR hub와 통신 하는 데 jQuery 라이브러리를 사용 *하는 방법을* 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-177">The *Chat.cshtml* view file in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span>  <span data-ttu-id="1b147-178">이 코드는 여러 중요 한 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-178">The code carries out many important tasks.</span></span> <span data-ttu-id="1b147-179">허브에 대해 자동 생성 된 프록시에 대 한 참조를 만들고, 서버에서 클라이언트에 콘텐츠를 푸시하는 데 호출할 수 있는 함수를 선언 하 고, 허브로 메시지를 보내기 위한 연결을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-179">It creates a reference to the autogenerated proxy for the hub, declares a function that the server can call to push content to clients, and it starts a connection to send messages to the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample6.js)]

> [!NOTE]
> <span data-ttu-id="1b147-180">JavaScript에서 서버 클래스 및 해당 멤버에 대 한 참조는 camelCase에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-180">In JavaScript, the reference to the server class and its members is in camelCase.</span></span> <span data-ttu-id="1b147-181">코드 샘플에서는 JavaScript의 C# `ChatHub` 클래스를 `chatHub`으로 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-181">The code sample references the C# `ChatHub` class in JavaScript as `chatHub`.</span></span>

<span data-ttu-id="1b147-182">이 코드 블록에서는 스크립트에서 콜백 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-182">In this code block, you create a callback function in the script.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample7.html)]

<span data-ttu-id="1b147-183">서버의 허브 클래스는이 함수를 호출 하 여 각 클라이언트에 콘텐츠 업데이트를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-183">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="1b147-184">`htmlEncode` 함수에 대 한 선택적 호출에서는 메시지 내용을 페이지에 표시 하기 전에 HTML로 인코딩하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-184">The optional call to the `htmlEncode` function shows a way to HTML encode the message content before displaying it in the page.</span></span> <span data-ttu-id="1b147-185">스크립트 삽입을 방지 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-185">It's a way to prevent script injection.</span></span>

<span data-ttu-id="1b147-186">이 코드는 허브와의 연결을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-186">This code opens a connection with the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample8.js)]

> [!NOTE]
> <span data-ttu-id="1b147-187">이 방법을 사용 하면 이벤트 처리기가 실행 되기 전에 연결을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-187">This approach ensures that you establish a connection before the event handler executes.</span></span>

<span data-ttu-id="1b147-188">이 코드는 연결을 시작한 다음 채팅 페이지의 **보내기** 단추에서 클릭 이벤트를 처리 하는 함수를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-188">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the Chat page.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="1b147-189">코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="1b147-189">Get the code</span></span>

[<span data-ttu-id="1b147-190">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="1b147-190">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Getting-Started-with-c366b2f3)

## <a name="additional-resources"></a><span data-ttu-id="1b147-191">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1b147-191">Additional resources</span></span>

<span data-ttu-id="1b147-192">SignalR에 대 한 자세한 내용은 다음 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="1b147-192">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="1b147-193">SignalR 프로젝트</span><span class="sxs-lookup"><span data-stu-id="1b147-193">SignalR Project</span></span>](http://signalr.net)

* [<span data-ttu-id="1b147-194">SignalR GitHub 및 샘플</span><span class="sxs-lookup"><span data-stu-id="1b147-194">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)

* [<span data-ttu-id="1b147-195">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="1b147-195">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="1b147-196">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1b147-196">Next steps</span></span>

<span data-ttu-id="1b147-197">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-197">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1b147-198">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="1b147-198">Set up the project</span></span>
> * <span data-ttu-id="1b147-199">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="1b147-199">Ran the sample</span></span>
> * <span data-ttu-id="1b147-200">코드 검사</span><span class="sxs-lookup"><span data-stu-id="1b147-200">Examined the code</span></span>

<span data-ttu-id="1b147-201">ASP.NET SignalR 2를 사용 하 여 빈도가 높은 메시징 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 알아보려면 다음 문서로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b147-201">Advance to the next article to learn how to create a web application that uses ASP.NET SignalR 2 to provide high-frequency messaging functionality.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="1b147-202">빈도가 높은 메시징이 있는 웹 앱</span><span class="sxs-lookup"><span data-stu-id="1b147-202">Web app with high-frequency messaging</span></span>](tutorial-high-frequency-realtime-with-signalr.md)