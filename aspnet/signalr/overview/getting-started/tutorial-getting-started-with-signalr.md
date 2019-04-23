---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr
title: '자습서: SignalR 2를 사용 하 여 실시간 채팅 | Microsoft Docs'
author: bradygaster
description: 이 자습서에는 SignalR을 사용하여 실시간 채팅 애플리케이션을 만드는 방법을 보여 줍니다. 빈 ASP.NET 웹 응용 프로그램에 SignalR을 추가합니다.
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: a8b3b778-f009-4369-85c7-e90f9878d8b4
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: ecc235454d4b95ce660a4373387f44720826b076
ms.sourcegitcommit: 2d53ed9e4c8b19d3526cbc689bfa8394c9449cec
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905646"
---
# <a name="tutorial-real-time-chat-with-signalr-2"></a><span data-ttu-id="fdb31-104">자습서: SignalR 2를 사용하는 실시간 채팅</span><span class="sxs-lookup"><span data-stu-id="fdb31-104">Tutorial: Real-time chat with SignalR 2</span></span>

<span data-ttu-id="fdb31-105">이 자습서에서는 실시간 채팅 응용 프로그램을 만드는 SignalR을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-105">This tutorial shows you how to use SignalR to create a real-time chat application.</span></span> <span data-ttu-id="fdb31-106">SignalR 빈 ASP.NET 웹 응용 프로그램에 추가 하 고이 정보를 보내고 메시지를 표시 하는 HTML 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-106">You add SignalR to an empty ASP.NET web application and create an HTML page to send and display messages.</span></span>

<span data-ttu-id="fdb31-107">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-107">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fdb31-108">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="fdb31-108">Set up the project</span></span>
> * <span data-ttu-id="fdb31-109">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="fdb31-109">Run the sample</span></span>
> * <span data-ttu-id="fdb31-110">코드 검사</span><span class="sxs-lookup"><span data-stu-id="fdb31-110">Examine the code</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a><span data-ttu-id="fdb31-111">전제 조건</span><span class="sxs-lookup"><span data-stu-id="fdb31-111">Prerequisites</span></span>

* <span data-ttu-id="fdb31-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) 사용 하 여 합니다 **ASP.NET 및 웹 개발** 워크 로드.</span><span class="sxs-lookup"><span data-stu-id="fdb31-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="set-up-the-project"></a><span data-ttu-id="fdb31-113">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="fdb31-113">Set up the Project</span></span>

<span data-ttu-id="fdb31-114">이 섹션에서는 Visual Studio 2017 및 SignalR 2를 사용 하 여 빈 ASP.NET 웹 응용 프로그램을 만드는 방법을 보여 줍니다. SignalR에 추가한 채팅 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-114">This section shows how to use Visual Studio 2017 and SignalR 2 to create an empty ASP.NET web application, add SignalR, and create the chat application.</span></span>

1. <span data-ttu-id="fdb31-115">Visual Studio에서 ASP.NET 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-115">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![웹 만들기](tutorial-getting-started-with-signalr/_static/image2.png)

1. <span data-ttu-id="fdb31-117">에 **새 ASP.NET 프로젝트-SignalRChat** 창에서 유지 **빈** 선택 하 고 선택 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-117">In the **New ASP.NET Project - SignalRChat** window, leave **Empty** selected and select **OK**.</span></span>

1. <span data-ttu-id="fdb31-118">**솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **추가** > **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-118">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="fdb31-119">**새 항목 추가-SignalRChat**를 선택 **설치 됨** > **시각적 C#**   >  **Web**  >  **SignalR** 선택한 후 **SignalR 허브 클래스 (v2)** 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-119">In **Add New Item - SignalRChat**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="fdb31-120">클래스의 이름을 *ChatHub* 하 고 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-120">Name the class *ChatHub* and add it to the project.</span></span>

    <span data-ttu-id="fdb31-121">이 단계에서는 합니다 *ChatHub.cs* 클래스 파일 및 스크립트 파일 및 프로젝트에 SignalR을 지 원하는 어셈블리 참조의 집합을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-121">This step creates the *ChatHub.cs* class file and adds a set of script files and assembly references that support SignalR to the project.</span></span>

1. <span data-ttu-id="fdb31-122">새 코드를 바꿉니다 *ChatHub.cs* 이 코드를 사용 하 여 클래스 파일:</span><span class="sxs-lookup"><span data-stu-id="fdb31-122">Replace the code in the new *ChatHub.cs* class file with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]

1. <span data-ttu-id="fdb31-123">**솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **추가** > **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-123">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="fdb31-124">**새 항목 추가-SignalRChat** 선택 **설치 됨** > **시각적 C#**   >  **Web** 차례로 선택 **OWIN Startup 클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-124">In **Add New Item - SignalRChat** select **Installed** > **Visual C#** > **Web**  and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="fdb31-125">클래스의 이름을 *시작* 하 고 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-125">Name the class *Startup* and add it to the project.</span></span>

1. <span data-ttu-id="fdb31-126">기본 코드를 바꿉니다 *시작* 이 코드를 사용 하 여 클래스:</span><span class="sxs-lookup"><span data-stu-id="fdb31-126">Replace the default code in *Startup* class with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]

1. <span data-ttu-id="fdb31-127">**솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **추가** > **HTML 페이지**합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-127">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="fdb31-128">새 페이지의 이름을 *인덱스* 선택한 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-128">Name the new page *index* and select **OK**.</span></span>

1. <span data-ttu-id="fdb31-129">**솔루션 탐색기**, 만든 HTML 페이지를 마우스 오른쪽 단추로 **시작 페이지로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-129">In **Solution Explorer**, right-click the HTML page you created and select **Set as Start Page**.</span></span>

1. <span data-ttu-id="fdb31-130">HTML 페이지의 기본 코드를이 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-130">Replace the default code in the HTML page with this code:</span></span>

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample3.html)]

1. <span data-ttu-id="fdb31-131">**솔루션 탐색기**를 확장 하 고 **스크립트**합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-131">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="fdb31-132">JQuery 및 SignalR에 대 한 스크립트 라이브러리 프로젝트에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-132">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="fdb31-133">패키지 관리자 SignalR 스크립트의 이후 버전이 설치 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-133">The package manager may have installed a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="fdb31-134">프로젝트에서 스크립트 파일의 버전에 해당 하는 코드 블록에 대 한 스크립트 참조는 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-134">Check that the script references in the code block correspond to the versions of the script files in the project.</span></span>

    <span data-ttu-id="fdb31-135">원래 코드 블록에서 스크립트 참조:</span><span class="sxs-lookup"><span data-stu-id="fdb31-135">Script references from the original code block:</span></span>

    ```html
    <!--Script references. -->
    <!--Reference the jQuery library. -->
    <script src="Scripts/jquery-3.1.1.min.js" ></script>
    <!--Reference the SignalR library. -->
    <script src="Scripts/jquery.signalR-2.2.1.min.js"></script>
    ```

1. <span data-ttu-id="fdb31-136">일치 하지 않으면 업데이트 합니다 *.html* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-136">If they don't match, update the *.html* file.</span></span>

1. <span data-ttu-id="fdb31-137">메뉴 모음에서 선택 **파일** > **모두 저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-137">From the menu bar, select **File** > **Save All**.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="fdb31-138">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="fdb31-138">Run the Sample</span></span>

1. <span data-ttu-id="fdb31-139">도구 모음에서 설정 **스크립트 디버깅** 다음 디버그 모드에서 샘플을 실행 하려면 재생 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-139">In the toolbar, turn on **Script Debugging** and then select the play button to run the sample in Debug mode.</span></span>

    ![사용자 이름 입력](tutorial-getting-started-with-signalr/_static/image3.png)

1. <span data-ttu-id="fdb31-141">브라우저가 열리면 채팅 id에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-141">When the browser opens, enter a name for your chat identity.</span></span>

1. <span data-ttu-id="fdb31-142">브라우저에서 URL을 복사 하 고 다른 두 브라우저를 열고 주소 표시줄에 Url을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-142">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="fdb31-143">각 브라우저에서 고유한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-143">In each browser, enter a unique name.</span></span>

1. <span data-ttu-id="fdb31-144">이제 선택한 주석 추가 **보낼**합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-144">Now, add a comment and select **Send**.</span></span> <span data-ttu-id="fdb31-145">다른 브라우저에는 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-145">Repeat that in the other browsers.</span></span> <span data-ttu-id="fdb31-146">실시간 설명이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-146">The comments appear in real-time.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fdb31-147">이 간단한 채팅 응용 프로그램 서버에서 토론 컨텍스트를 유지 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-147">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="fdb31-148">허브는 모든 현재 사용자에 게 의견을 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-148">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="fdb31-149">채팅을 나중에 조인 하는 사용자에 가입할 때부터 추가 된 메시지를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-149">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="fdb31-150">세 가지 다른 브라우저에서 채팅 응용 프로그램을 실행 하는 방법을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="fdb31-150">See how the chat application runs in three different browsers.</span></span> <span data-ttu-id="fdb31-151">Tom, Anand, 및 Susan 메시지를 보낼 때, 모든 브라우저 실시간으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-151">When Tom, Anand, and Susan send messages, all browsers update in real time:</span></span>

    ![모든 세 가지 브라우저 동일한 채팅 기록 표시](tutorial-getting-started-with-signalr/_static/image4.png)

1. <span data-ttu-id="fdb31-153">**솔루션 탐색기**를 검사 합니다 **스크립트 문서** 실행 중인 응용 프로그램에 대 한 노드.</span><span class="sxs-lookup"><span data-stu-id="fdb31-153">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="fdb31-154">명명 된 스크립트 파일이 *hubs* SignalR 라이브러리는 런타임에 생성 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-154">There's a script file named *hubs* that the SignalR library generates at runtime.</span></span> <span data-ttu-id="fdb31-155">이 파일 jQuery 스크립트와 서버 쪽 코드 간의 통신을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-155">This file manages the communication between jQuery script and server-side code.</span></span>

    ![스크립트 문서 노드의 hubs 스크립트 자동 생성](tutorial-getting-started-with-signalr/_static/image5.png)

## <a name="examine-the-code"></a><span data-ttu-id="fdb31-157">코드 검사</span><span class="sxs-lookup"><span data-stu-id="fdb31-157">Examine the Code</span></span>

<span data-ttu-id="fdb31-158">SignalRChat 응용 프로그램에서는 두 가지 기본 SignalR 개발 작업을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-158">The SignalRChat application demonstrates two basic SignalR development tasks.</span></span> <span data-ttu-id="fdb31-159">허브를 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-159">It shows you how to create a hub.</span></span> <span data-ttu-id="fdb31-160">서버는 주 조정 개체와 해당 허브를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-160">The server uses that hub as the main coordination object.</span></span> <span data-ttu-id="fdb31-161">허브는 SignalR jQuery 라이브러리를 사용 하 여 메시지 보내기 및 받기.</span><span class="sxs-lookup"><span data-stu-id="fdb31-161">The hub uses the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs-in-the-chathubcs"></a><span data-ttu-id="fdb31-162">SignalR 허브를 ChatHub.cs에서</span><span class="sxs-lookup"><span data-stu-id="fdb31-162">SignalR Hubs in the ChatHub.cs</span></span>

<span data-ttu-id="fdb31-163">위의 코드 샘플에는 `ChatHub` 클래스에서 파생 되는 `Microsoft.AspNet.SignalR.Hub` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-163">In the code sample above, the `ChatHub` class derives from the `Microsoft.AspNet.SignalR.Hub` class.</span></span> <span data-ttu-id="fdb31-164">파생 된 `Hub` 클래스는 SignalR 응용 프로그램을 빌드하는 유용한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-164">Deriving from the `Hub` class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="fdb31-165">허브 클래스에서 public 메서드를 만들고 해당 메서드를 사용 하 여 웹 페이지의 스크립트에서 호출 하 여 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-165">You can create public methods on your hub class and then use those methods by calling them from scripts in a web page.</span></span>

<span data-ttu-id="fdb31-166">채팅 코드에서 클라이언트 호출을 `ChatHub.Send` 새 메시지를 전송 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-166">In the chat code, clients call the `ChatHub.Send` method to send a new message.</span></span> <span data-ttu-id="fdb31-167">허브는 메시지를 전송 합니다 모든 클라이언트를 호출 하 여 `Clients.All.broadcastMessage`입니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-167">The hub then sends the message to all clients by calling `Clients.All.broadcastMessage`.</span></span>

<span data-ttu-id="fdb31-168">`Send` 메서드 여러 허브 개념을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-168">The `Send` method demonstrates several hub concepts:</span></span>

* <span data-ttu-id="fdb31-169">클라이언트에서 호출할 수 있도록 허브에서 공용 메서드를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-169">Declare public methods on a hub so that clients can call them.</span></span>

* <span data-ttu-id="fdb31-170">사용 된 `Microsoft.AspNet.SignalR.Hub.Clients` 이 허브에 연결 된 모든 클라이언트와 통신 하는 동적 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-170">Use the `Microsoft.AspNet.SignalR.Hub.Clients` dynamic property to communicate with all clients connected to this hub.</span></span>

* <span data-ttu-id="fdb31-171">클라이언트에서 함수를 호출 (같은 `broadcastMessage` 함수) 클라이언트를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-171">Call a function on the client (like the `broadcastMessage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample4.cs)]

### <a name="signalr-and-jquery-in-the-indexhtml"></a><span data-ttu-id="fdb31-172">SignalR 및 index.html에서 jQuery</span><span class="sxs-lookup"><span data-stu-id="fdb31-172">SignalR and jQuery in the index.html</span></span>

<span data-ttu-id="fdb31-173">합니다 *index.html* 코드 샘플에서 페이지에는 SignalR jQuery 라이브러리를 사용 하 여 SignalR 허브와 통신 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-173">The *index.html* page in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="fdb31-174">코드는 여러 중요 한 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-174">The code carries out many important tasks.</span></span> <span data-ttu-id="fdb31-175">허브를 참조 하는 프록시를 선언, 서버는 클라이언트 밀어넣기 콘텐츠를 호출할 수 있습니다 하 고 허브에 메시지를 보내는 연결을 시작 하는 함수를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-175">It declares a proxy to reference the hub, declares a function that the server can call to push content to clients, and it starts a connection to send messages to the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample5.js)]

> [!NOTE]
> <span data-ttu-id="fdb31-176">JavaScript에서 서버 클래스 및 해당 멤버에 대 한 참조는 camelCase 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-176">In JavaScript the reference to the server class and its members has to be camelCase.</span></span> <span data-ttu-id="fdb31-177">코드 샘플 참조는 C# *ChatHub* 으로 JavaScript에서 클래스 `chatHub`합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-177">The code sample references the C# *ChatHub* class in JavaScript as `chatHub`.</span></span>

<span data-ttu-id="fdb31-178">이 코드 블록을 스크립트에 콜백 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-178">In this code block, you create a callback function in the script.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample6.html)]

<span data-ttu-id="fdb31-179">서버의 허브 클래스는 각 클라이언트에 콘텐츠 업데이트를 푸시 하려면이 함수를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-179">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="fdb31-180">두 줄 해당 HTML 인코딩해야 표시 하기 전에 콘텐츠는 선택 사항 및 스크립트 삽입을 방지 하는 좋은 방법은 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-180">The two lines that HTML-encode the content before displaying it are optional and show a good way to prevent script injection.</span></span>

<span data-ttu-id="fdb31-181">이 코드는 허브를 사용 하 여 연결을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-181">This code opens a connection with the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample7.js)]

> [!NOTE]
> <span data-ttu-id="fdb31-182">이 방법을 사용 하면 이벤트 처리기 실행 되기 전에 코드는 연결을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-182">This approach ensures that the code establishes a connection before the event handler executes.</span></span>

<span data-ttu-id="fdb31-183">코드는 연결을 시작 하 고 다음에 클릭 이벤트를 처리 하는 함수 전달 합니다 **보낼** HTML 페이지에 단추.</span><span class="sxs-lookup"><span data-stu-id="fdb31-183">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the HTML page.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="fdb31-184">코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="fdb31-184">Get the code</span></span>

[<span data-ttu-id="fdb31-185">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="fdb31-185">Download Completed Project</span></span>](http://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)

## <a name="additional-resources"></a><span data-ttu-id="fdb31-186">추가 자료</span><span class="sxs-lookup"><span data-stu-id="fdb31-186">Additional resources</span></span>

<span data-ttu-id="fdb31-187">SignalR에 대 한 자세한 내용은 다음 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="fdb31-187">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="fdb31-188">SignalR 프로젝트</span><span class="sxs-lookup"><span data-stu-id="fdb31-188">SignalR Project</span></span>](http://signalr.net)

* [<span data-ttu-id="fdb31-189">SignalR Github 및 샘플</span><span class="sxs-lookup"><span data-stu-id="fdb31-189">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)

* [<span data-ttu-id="fdb31-190">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="fdb31-190">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="fdb31-191">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fdb31-191">Next steps</span></span>

<span data-ttu-id="fdb31-192">이 자습서에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdb31-192">In this tutorial you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fdb31-193">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="fdb31-193">Set up the project</span></span>
> * <span data-ttu-id="fdb31-194">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="fdb31-194">Ran the sample</span></span>
> * <span data-ttu-id="fdb31-195">코드 검사</span><span class="sxs-lookup"><span data-stu-id="fdb31-195">Examined the code</span></span>

<span data-ttu-id="fdb31-196">SignalR 및 MVC 5를 사용 하는 방법을 알아보려면 다음 문서로 계속 진행 하세요.</span><span class="sxs-lookup"><span data-stu-id="fdb31-196">Advance to the next article to learn how to use SignalR and MVC 5.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="fdb31-197">SignalR 2 및 MVC 5</span><span class="sxs-lookup"><span data-stu-id="fdb31-197">SignalR 2 and MVC 5</span></span>](tutorial-getting-started-with-signalr-and-mvc.md)