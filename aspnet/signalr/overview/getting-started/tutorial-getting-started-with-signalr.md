---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr
title: '자습서: SignalR 2를 사용한 실시간 채팅 | Microsoft Docs'
author: bradygaster
description: 이 자습서에는 SignalR을 사용하여 실시간 채팅 애플리케이션을 만드는 방법을 보여 줍니다. 빈 ASP.NET 웹 응용 프로그램에 SignalR를 추가 합니다.
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: a8b3b778-f009-4369-85c7-e90f9878d8b4
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: bc4ef190b6e36812b6fe7ca4e16eb763431e0e82
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600466"
---
# <a name="tutorial-real-time-chat-with-signalr-2"></a><span data-ttu-id="302be-104">자습서: SignalR 2를 사용 하 여 실시간 채팅</span><span class="sxs-lookup"><span data-stu-id="302be-104">Tutorial: Real-time chat with SignalR 2</span></span>

<span data-ttu-id="302be-105">이 자습서에서는 SignalR를 사용 하 여 실시간 채팅 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="302be-105">This tutorial shows you how to use SignalR to create a real-time chat application.</span></span> <span data-ttu-id="302be-106">빈 ASP.NET 웹 응용 프로그램에 SignalR를 추가 하 고 메시지를 보내고 표시 하는 HTML 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="302be-106">You add SignalR to an empty ASP.NET web application and create an HTML page to send and display messages.</span></span>

<span data-ttu-id="302be-107">이 자습서에서는 다음과 같은 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-107">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="302be-108">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="302be-108">Set up the project</span></span>
> * <span data-ttu-id="302be-109">예제 실행</span><span class="sxs-lookup"><span data-stu-id="302be-109">Run the sample</span></span>
> * <span data-ttu-id="302be-110">코드 검사</span><span class="sxs-lookup"><span data-stu-id="302be-110">Examine the code</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a><span data-ttu-id="302be-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="302be-111">Prerequisites</span></span>

* <span data-ttu-id="302be-112">**ASP.NET 및 웹 개발** 워크 로드가 포함 된 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) .</span><span class="sxs-lookup"><span data-stu-id="302be-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="set-up-the-project"></a><span data-ttu-id="302be-113">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="302be-113">Set up the Project</span></span>

<span data-ttu-id="302be-114">이 섹션에서는 Visual Studio 2017 및 SignalR 2를 사용 하 여 빈 ASP.NET 웹 응용 프로그램을 만들고 SignalR를 추가 하 고 채팅 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="302be-114">This section shows how to use Visual Studio 2017 and SignalR 2 to create an empty ASP.NET web application, add SignalR, and create the chat application.</span></span>

1. <span data-ttu-id="302be-115">Visual Studio에서 ASP.NET 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="302be-115">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![웹 만들기](tutorial-getting-started-with-signalr/_static/image2.png)

1. <span data-ttu-id="302be-117">**New ASP.NET SignalRChat** 창에서 선택 된 상태로 두고 확인 **을 선택 합니다** .</span><span class="sxs-lookup"><span data-stu-id="302be-117">In the **New ASP.NET Project - SignalRChat** window, leave **Empty** selected and select **OK**.</span></span>

1. <span data-ttu-id="302be-118">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가** > **새 항목**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-118">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="302be-119">**새 항목 추가-SignalRChat**에서 **설치** > **Visual C#**  > **Web** > **SignalR** 을 선택한 다음 **SignalR Hub 클래스 (v2)** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-119">In **Add New Item - SignalRChat**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="302be-120">클래스 이름을 *ChatHub* 로 추가 하 고 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-120">Name the class *ChatHub* and add it to the project.</span></span>

    <span data-ttu-id="302be-121">이 단계에서는 *ChatHub.cs* 클래스 파일을 만들고 SignalR을 지 원하는 스크립트 파일 및 어셈블리 참조 집합을 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-121">This step creates the *ChatHub.cs* class file and adds a set of script files and assembly references that support SignalR to the project.</span></span>

1. <span data-ttu-id="302be-122">새 *ChatHub.cs* 클래스 파일의 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="302be-122">Replace the code in the new *ChatHub.cs* class file with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]

1. <span data-ttu-id="302be-123">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가** > **새 항목**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-123">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="302be-124">**새 항목 추가-SignalRChat** **Visual C#**  > **웹** > **설치** 를 선택한 다음 **OWIN 시작 클래스**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-124">In **Add New Item - SignalRChat** select **Installed** > **Visual C#** > **Web**  and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="302be-125">클래스 이름을 *시작* 으로 하 고 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-125">Name the class *Startup* and add it to the project.</span></span>

1. <span data-ttu-id="302be-126">*Startup* 클래스의 기본 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="302be-126">Replace the default code in *Startup* class with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]

1. <span data-ttu-id="302be-127">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 > **HTML 페이지** **추가** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-127">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="302be-128">새 페이지 *인덱스* 의 이름을로 하 고 **확인을**선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-128">Name the new page *index* and select **OK**.</span></span>

1. <span data-ttu-id="302be-129">**솔루션 탐색기**에서 사용자가 만든 HTML 페이지를 마우스 오른쪽 단추로 클릭 하 고 **시작 페이지로 설정**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-129">In **Solution Explorer**, right-click the HTML page you created and select **Set as Start Page**.</span></span>

1. <span data-ttu-id="302be-130">HTML 페이지의 기본 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="302be-130">Replace the default code in the HTML page with this code:</span></span>

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample3.html)]

1. <span data-ttu-id="302be-131">**솔루션 탐색기**에서 **스크립트**를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-131">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="302be-132">JQuery 및 SignalR에 대 한 스크립트 라이브러리는 프로젝트에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="302be-132">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="302be-133">패키지 관리자가 SignalR 스크립트의 최신 버전을 설치 했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="302be-133">The package manager may have installed a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="302be-134">코드 블록의 스크립트 참조가 프로젝트의 스크립트 파일 버전에 해당 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-134">Check that the script references in the code block correspond to the versions of the script files in the project.</span></span>

    <span data-ttu-id="302be-135">원본 코드 블록의 스크립트 참조:</span><span class="sxs-lookup"><span data-stu-id="302be-135">Script references from the original code block:</span></span>

    ```html
    <!--Script references. -->
    <!--Reference the jQuery library. -->
    <script src="Scripts/jquery-3.1.1.min.js" ></script>
    <!--Reference the SignalR library. -->
    <script src="Scripts/jquery.signalR-2.2.1.min.js"></script>
    ```

1. <span data-ttu-id="302be-136">일치 하지 않는 경우 *.html* 파일을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-136">If they don't match, update the *.html* file.</span></span>

1. <span data-ttu-id="302be-137">메뉴 모음에서 **파일** > **모두 저장**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-137">From the menu bar, select **File** > **Save All**.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="302be-138">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="302be-138">Run the Sample</span></span>

1. <span data-ttu-id="302be-139">도구 모음에서 **스크립트 디버깅** 을 사용 하도록 설정 하 고 재생 단추를 선택 하 여 디버그 모드에서 샘플을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-139">In the toolbar, turn on **Script Debugging** and then select the play button to run the sample in Debug mode.</span></span>

    ![사용자 이름 입력](tutorial-getting-started-with-signalr/_static/image3.png)

1. <span data-ttu-id="302be-141">브라우저가 열리면 채팅 id의 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-141">When the browser opens, enter a name for your chat identity.</span></span>

1. <span data-ttu-id="302be-142">브라우저에서 URL을 복사 하 여 다른 두 브라우저를 열고 Url을 주소 표시줄에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="302be-142">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="302be-143">각 브라우저에서 고유한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-143">In each browser, enter a unique name.</span></span>

1. <span data-ttu-id="302be-144">이제 주석을 추가 하 고 **보내기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-144">Now, add a comment and select **Send**.</span></span> <span data-ttu-id="302be-145">다른 브라우저에서 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-145">Repeat that in the other browsers.</span></span> <span data-ttu-id="302be-146">주석은 실시간으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="302be-146">The comments appear in real-time.</span></span>

    > [!NOTE]
    > <span data-ttu-id="302be-147">이 간단한 채팅 응용 프로그램은 서버에 대 한 토론 컨텍스트를 유지 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="302be-147">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="302be-148">허브는 모든 현재 사용자에 게 주석을 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-148">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="302be-149">나중에 채팅에 참여 하는 사용자는 연결 된 시간부터 추가 된 메시지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="302be-149">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="302be-150">채팅 응용 프로그램이 세 가지 브라우저에서 어떻게 실행 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-150">See how the chat application runs in three different browsers.</span></span> <span data-ttu-id="302be-151">Tom, Anand 및 김소미로 메시지를 보내면 모든 브라우저가 실시간으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="302be-151">When Tom, Anand, and Susan send messages, all browsers update in real time:</span></span>

    ![세 브라우저 모두 동일한 채팅 기록을 표시 합니다.](tutorial-getting-started-with-signalr/_static/image4.png)

1. <span data-ttu-id="302be-153">**솔루션 탐색기**에서 실행 중인 응용 프로그램에 대 한 **스크립트 문서** 노드를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-153">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="302be-154">SignalR 라이브러리가 런타임에 생성 하는 *허브* 라는 스크립트 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="302be-154">There's a script file named *hubs* that the SignalR library generates at runtime.</span></span> <span data-ttu-id="302be-155">이 파일은 jQuery 스크립트와 서버측 코드 간의 통신을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-155">This file manages the communication between jQuery script and server-side code.</span></span>

    ![스크립트 문서 노드의 자동 생성 된 허브 스크립트](tutorial-getting-started-with-signalr/_static/image5.png)

## <a name="examine-the-code"></a><span data-ttu-id="302be-157">코드 검사</span><span class="sxs-lookup"><span data-stu-id="302be-157">Examine the Code</span></span>

<span data-ttu-id="302be-158">SignalRChat 응용 프로그램은 두 가지 기본 SignalR 개발 작업을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="302be-158">The SignalRChat application demonstrates two basic SignalR development tasks.</span></span> <span data-ttu-id="302be-159">허브를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="302be-159">It shows you how to create a hub.</span></span> <span data-ttu-id="302be-160">서버는 주 조정 개체로 해당 허브를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-160">The server uses that hub as the main coordination object.</span></span> <span data-ttu-id="302be-161">허브는 SignalR jQuery 라이브러리를 사용 하 여 메시지를 보내고 받습니다.</span><span class="sxs-lookup"><span data-stu-id="302be-161">The hub uses the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs-in-the-chathubcs"></a><span data-ttu-id="302be-162">ChatHub.cs의 SignalR Hubs</span><span class="sxs-lookup"><span data-stu-id="302be-162">SignalR Hubs in the ChatHub.cs</span></span>

<span data-ttu-id="302be-163">위의 코드 샘플에서 `ChatHub` 클래스는 `Microsoft.AspNet.SignalR.Hub` 클래스에서 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="302be-163">In the code sample above, the `ChatHub` class derives from the `Microsoft.AspNet.SignalR.Hub` class.</span></span> <span data-ttu-id="302be-164">`Hub` 클래스에서 파생 하는 것은 SignalR 응용 프로그램을 빌드하는 데 유용한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="302be-164">Deriving from the `Hub` class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="302be-165">허브 클래스에서 공용 메서드를 만든 다음 웹 페이지의 스크립트에서 호출 하 여 해당 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="302be-165">You can create public methods on your hub class and then use those methods by calling them from scripts in a web page.</span></span>

<span data-ttu-id="302be-166">채팅 코드에서 클라이언트는 `ChatHub.Send` 메서드를 호출 하 여 새 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="302be-166">In the chat code, clients call the `ChatHub.Send` method to send a new message.</span></span> <span data-ttu-id="302be-167">그런 다음 허브는 `Clients.All.broadcastMessage`를 호출 하 여 모든 클라이언트에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="302be-167">The hub then sends the message to all clients by calling `Clients.All.broadcastMessage`.</span></span>

<span data-ttu-id="302be-168">`Send` 메서드는 다음과 같은 몇 가지 허브 개념을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="302be-168">The `Send` method demonstrates several hub concepts:</span></span>

* <span data-ttu-id="302be-169">클라이언트에서 호출할 수 있도록 허브에 공용 메서드를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-169">Declare public methods on a hub so that clients can call them.</span></span>

* <span data-ttu-id="302be-170">`Microsoft.AspNet.SignalR.Hub.Clients` 동적 속성을 사용 하 여이 허브에 연결 된 모든 클라이언트와 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-170">Use the `Microsoft.AspNet.SignalR.Hub.Clients` dynamic property to communicate with all clients connected to this hub.</span></span>

* <span data-ttu-id="302be-171">클라이언트에서 함수 (예: `broadcastMessage` 함수)를 호출 하 여 클라이언트를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-171">Call a function on the client (like the `broadcastMessage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample4.cs)]

### <a name="signalr-and-jquery-in-the-indexhtml"></a><span data-ttu-id="302be-172">SignalR 및 jQuery의 인덱스. html</span><span class="sxs-lookup"><span data-stu-id="302be-172">SignalR and jQuery in the index.html</span></span>

<span data-ttu-id="302be-173">코드 샘플의 *SignalR 페이지는* SignalR 허브와 통신 하는 데 jQuery 라이브러리를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="302be-173">The *index.html* page in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="302be-174">이 코드는 여러 중요 한 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-174">The code carries out many important tasks.</span></span> <span data-ttu-id="302be-175">허브를 참조 하는 프록시를 선언 하 고, 서버에서 클라이언트에 콘텐츠를 푸시하는 데 호출할 수 있는 함수를 선언 하 고, 허브에 메시지를 보내기 위한 연결을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-175">It declares a proxy to reference the hub, declares a function that the server can call to push content to clients, and it starts a connection to send messages to the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample5.js)]

> [!NOTE]
> <span data-ttu-id="302be-176">JavaScript에서 서버 클래스 및 해당 멤버에 대 한 참조는 camelCase 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-176">In JavaScript the reference to the server class and its members has to be camelCase.</span></span> <span data-ttu-id="302be-177">코드 샘플은 `chatHub`로 C# JavaScript의 *ChatHub* 클래스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-177">The code sample references the C# *ChatHub* class in JavaScript as `chatHub`.</span></span>

<span data-ttu-id="302be-178">이 코드 블록에서는 스크립트에서 콜백 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="302be-178">In this code block, you create a callback function in the script.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample6.html)]

<span data-ttu-id="302be-179">서버의 허브 클래스는이 함수를 호출 하 여 각 클라이언트에 콘텐츠 업데이트를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-179">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="302be-180">콘텐츠를 표시 하기 전에 콘텐츠를 HTML로 인코딩하는 두 줄은 선택 사항이 며 스크립트 삽입을 방지 하는 좋은 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="302be-180">The two lines that HTML-encode the content before displaying it are optional and show a good way to prevent script injection.</span></span>

<span data-ttu-id="302be-181">이 코드는 허브와의 연결을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="302be-181">This code opens a connection with the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample7.js)]

> [!NOTE]
> <span data-ttu-id="302be-182">이 방법을 사용 하면 이벤트 처리기가 실행 되기 전에 코드에서 연결을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-182">This approach ensures that the code establishes a connection before the event handler executes.</span></span>

<span data-ttu-id="302be-183">이 코드는 연결을 시작한 다음 HTML 페이지의 **보내기** 단추에서 클릭 이벤트를 처리 하는 함수를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-183">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the HTML page.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="302be-184">코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="302be-184">Get the code</span></span>

[<span data-ttu-id="302be-185">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="302be-185">Download Completed Project</span></span>](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)

## <a name="additional-resources"></a><span data-ttu-id="302be-186">추가 자료</span><span class="sxs-lookup"><span data-stu-id="302be-186">Additional resources</span></span>

<span data-ttu-id="302be-187">SignalR에 대 한 자세한 내용은 다음 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="302be-187">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="302be-188">SignalR 프로젝트</span><span class="sxs-lookup"><span data-stu-id="302be-188">SignalR Project</span></span>](http://signalr.net)

* [<span data-ttu-id="302be-189">SignalR Github 및 샘플</span><span class="sxs-lookup"><span data-stu-id="302be-189">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)

* [<span data-ttu-id="302be-190">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="302be-190">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="302be-191">다음 단계</span><span class="sxs-lookup"><span data-stu-id="302be-191">Next steps</span></span>

<span data-ttu-id="302be-192">이 자습서에서는 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-192">In this tutorial you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="302be-193">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="302be-193">Set up the project</span></span>
> * <span data-ttu-id="302be-194">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="302be-194">Ran the sample</span></span>
> * <span data-ttu-id="302be-195">코드 검사</span><span class="sxs-lookup"><span data-stu-id="302be-195">Examined the code</span></span>

<span data-ttu-id="302be-196">SignalR 및 MVC 5를 사용 하는 방법을 알아보려면 다음 문서로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="302be-196">Advance to the next article to learn how to use SignalR and MVC 5.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="302be-197">SignalR 2 및 MVC 5</span><span class="sxs-lookup"><span data-stu-id="302be-197">SignalR 2 and MVC 5</span></span>](tutorial-getting-started-with-signalr-and-mvc.md)