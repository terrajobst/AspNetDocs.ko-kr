---
uid: signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
title: '자습서: SignalR 2를 사용 하 여 빈도가 높은 실시간 앱 만들기 | Microsoft Docs'
author: bradygaster
description: 이 자습서에서는 ASP.NET SignalR를 사용 하 여 높은 빈도의 메시징 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다.
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: 9f969dda-78ea-4329-b1e3-e51c02210a2b
msc.legacyurl: /signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: 2503e90735d6cfa445ee08c9e43f8443aa106096
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600450"
---
# <a name="tutorial-create-high-frequency-real-time-app-with-signalr-2"></a><span data-ttu-id="6bb8e-103">자습서: SignalR 2를 사용 하 여 빈도가 높은 실시간 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="6bb8e-103">Tutorial: Create high-frequency real-time app with SignalR 2</span></span>

<span data-ttu-id="6bb8e-104">이 자습서에서는 ASP.NET SignalR 2를 사용 하 여 빈도가 높은 메시징 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-104">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide high-frequency messaging functionality.</span></span> <span data-ttu-id="6bb8e-105">이 경우 "빈도가 높은 메시징"은 서버가 고정 속도로 업데이트를 보내는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-105">In this case, "high-frequency messaging" means the server sends updates at a fixed rate.</span></span> <span data-ttu-id="6bb8e-106">초당 최대 10 개의 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-106">You send up to 10 messages a second.</span></span>

<span data-ttu-id="6bb8e-107">사용자가 만드는 응용 프로그램은 사용자가 끌 수 있는 셰이프를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-107">The application you create displays a shape that users can drag.</span></span> <span data-ttu-id="6bb8e-108">서버는 모든 연결 된 브라우저에서 셰이프의 위치를 업데이트 하 여 시간 업데이트를 사용 하는 끌어 온 모양의 위치와 일치 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-108">The server updates the position of the shape in all connected browsers to match the position of the dragged shape using timed updates.</span></span>

<span data-ttu-id="6bb8e-109">이 자습서에 소개 된 개념에는 실시간 게임과 기타 시뮬레이션 응용 프로그램의 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-109">Concepts introduced in this tutorial have applications in real-time gaming and other simulation applications.</span></span>

<span data-ttu-id="6bb8e-110">이 자습서에서는 다음과 같은 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-110">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6bb8e-111">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="6bb8e-111">Set up the project</span></span>
> * <span data-ttu-id="6bb8e-112">기본 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="6bb8e-112">Create the base application</span></span>
> * <span data-ttu-id="6bb8e-113">앱이 시작 되 면 허브에 매핑</span><span class="sxs-lookup"><span data-stu-id="6bb8e-113">Map to the hub when app starts</span></span>
> * <span data-ttu-id="6bb8e-114">클라이언트 추가</span><span class="sxs-lookup"><span data-stu-id="6bb8e-114">Add the client</span></span>
> * <span data-ttu-id="6bb8e-115">앱 실행</span><span class="sxs-lookup"><span data-stu-id="6bb8e-115">Run the app</span></span>
> * <span data-ttu-id="6bb8e-116">클라이언트 루프 추가</span><span class="sxs-lookup"><span data-stu-id="6bb8e-116">Add the client loop</span></span>
> * <span data-ttu-id="6bb8e-117">서버 루프 추가</span><span class="sxs-lookup"><span data-stu-id="6bb8e-117">Add the server loop</span></span>
> * <span data-ttu-id="6bb8e-118">부드러운 애니메이션 추가</span><span class="sxs-lookup"><span data-stu-id="6bb8e-118">Add smooth animation</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a><span data-ttu-id="6bb8e-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6bb8e-119">Prerequisites</span></span>

* <span data-ttu-id="6bb8e-120">**ASP.NET 및 웹 개발** 워크 로드가 포함 된 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) .</span><span class="sxs-lookup"><span data-stu-id="6bb8e-120">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="set-up-the-project"></a><span data-ttu-id="6bb8e-121">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="6bb8e-121">Set up the project</span></span>

<span data-ttu-id="6bb8e-122">이 섹션에서는 Visual Studio 2017에서 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-122">In this section, you create the project in Visual Studio 2017.</span></span>

<span data-ttu-id="6bb8e-123">이 섹션에서는 Visual Studio 2017을 사용 하 여 빈 ASP.NET 웹 응용 프로그램을 만들고 SignalR 및 jQuery. u s 라이브러리를 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-123">This section shows how to use Visual Studio 2017 to create an empty ASP.NET Web Application and add the SignalR and jQuery.UI libraries.</span></span>

1. <span data-ttu-id="6bb8e-124">Visual Studio에서 ASP.NET 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-124">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![웹 만들기](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

1. <span data-ttu-id="6bb8e-126">**New ASP.NET 웹 응용 프로그램-MoveShapeDemo** 창에서 **비어 있음** 을 선택 된 상태로 두고 **확인**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-126">In the **New ASP.NET Web Application - MoveShapeDemo** window, leave **Empty** selected and select **OK**.</span></span>

1. <span data-ttu-id="6bb8e-127">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가** > **새 항목**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-127">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="6bb8e-128">**새 항목 추가-MoveShapeDemo**에서 **설치** > **Visual C#**  > **Web** > **SignalR** 을 선택한 다음 **SignalR Hub 클래스 (v2)** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-128">In **Add New Item - MoveShapeDemo**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="6bb8e-129">클래스 이름을 *MoveShapeHub* 로 추가 하 고 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-129">Name the class *MoveShapeHub* and add it to the project.</span></span>

    <span data-ttu-id="6bb8e-130">이 단계에서는 *MoveShapeHub.cs* 클래스 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-130">This step creates the *MoveShapeHub.cs* class file.</span></span> <span data-ttu-id="6bb8e-131">동시에 SignalR를 지 원하는 스크립트 파일 및 어셈블리 참조 집합을 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-131">Simultaneously, it adds  a set of script files and assembly references that support SignalR to the project.</span></span>

1. <span data-ttu-id="6bb8e-132">**도구** > **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-132">Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

1. <span data-ttu-id="6bb8e-133">**패키지 관리자 콘솔**에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-133">In **Package Manager Console**, run this command:</span></span>

    ```console
    Install-Package jQuery.UI.Combined
    ```

    <span data-ttu-id="6bb8e-134">명령은 jQuery UI 라이브러리를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-134">The command installs the jQuery UI library.</span></span> <span data-ttu-id="6bb8e-135">이를 사용 하 여 도형에 애니메이션 효과를 주는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-135">You use it to animate the shape.</span></span>

1. <span data-ttu-id="6bb8e-136">**솔루션 탐색기**에서 스크립트 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-136">In **Solution Explorer**, expand the Scripts node.</span></span>

    ![스크립트 라이브러리 참조](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)

    <span data-ttu-id="6bb8e-138">JQuery, jQueryUI 및 SignalR에 대 한 스크립트 라이브러리는 프로젝트에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-138">Script libraries for jQuery, jQueryUI, and SignalR are visible in the project.</span></span>

## <a name="create-the-base-application"></a><span data-ttu-id="6bb8e-139">기본 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="6bb8e-139">Create the base application</span></span>

<span data-ttu-id="6bb8e-140">이 섹션에서는 브라우저 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-140">In this section, you create a browser application.</span></span> <span data-ttu-id="6bb8e-141">앱은 각 마우스 이동 이벤트 동안 셰이프의 위치를 서버에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-141">The app sends the location of the shape to the server during each mouse move event.</span></span> <span data-ttu-id="6bb8e-142">서버는 연결 된 다른 모든 클라이언트에 실시간으로이 정보를 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-142">The server broadcasts this information to all other connected clients in real time.</span></span> <span data-ttu-id="6bb8e-143">이 응용 프로그램에 대 한 자세한 내용은 이후 섹션에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-143">You learn more about this application in later sections.</span></span>

1. <span data-ttu-id="6bb8e-144">*MoveShapeHub.cs* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-144">Open the *MoveShapeHub.cs* file.</span></span>

1. <span data-ttu-id="6bb8e-145">*MoveShapeHub.cs* 파일의 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-145">Replace the code in the *MoveShapeHub.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.cs)]

1. <span data-ttu-id="6bb8e-146">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-146">Save the file.</span></span>

<span data-ttu-id="6bb8e-147">`MoveShapeHub` 클래스는 SignalR hub의 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-147">The `MoveShapeHub` class is an implementation of a SignalR hub.</span></span> <span data-ttu-id="6bb8e-148">[SignalR 시작](tutorial-getting-started-with-signalr.md) 자습서에서와 같이 허브에는 클라이언트가 직접 호출 하는 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-148">As in the [Getting Started with SignalR](tutorial-getting-started-with-signalr.md) tutorial, the hub has a method that the clients call directly.</span></span> <span data-ttu-id="6bb8e-149">이 경우 클라이언트는 셰이프의 새 X 및 Y 좌표가 포함 된 개체를 서버에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-149">In this case, the client sends an object with the new X and Y coordinates of the shape to the server.</span></span> <span data-ttu-id="6bb8e-150">이러한 좌표는 연결 된 다른 모든 클라이언트에 브로드캐스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-150">Those coordinates get broadcasted to all other connected clients.</span></span> <span data-ttu-id="6bb8e-151">SignalR는 JSON을 사용 하 여이 개체를 자동으로 직렬화 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-151">SignalR automatically serializes this object using JSON.</span></span>

<span data-ttu-id="6bb8e-152">앱은 `ShapeModel` 개체를 클라이언트에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-152">The app sends the `ShapeModel` object to the client.</span></span> <span data-ttu-id="6bb8e-153">이 클래스에는 셰이프의 위치를 저장할 멤버가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-153">It has members to store the position of the shape.</span></span> <span data-ttu-id="6bb8e-154">서버에 있는 개체의 버전에는 저장 되는 클라이언트 데이터를 추적 하는 멤버도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-154">The version of the object on the server also has a member to track which client's data is being stored.</span></span> <span data-ttu-id="6bb8e-155">이 개체는 서버에서 클라이언트의 데이터를 다시 전송 하는 것을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-155">This object prevents the server from sending a client's data back to itself.</span></span> <span data-ttu-id="6bb8e-156">이 멤버는 `JsonIgnore` 특성을 사용 하 여 응용 프로그램이 데이터를 직렬화 하 고 클라이언트로 다시 전송 하는 것을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-156">This member uses the `JsonIgnore` attribute to keep the application from serializing the data and sending it back to the client.</span></span>

## <a name="map-to-the-hub-when-app-starts"></a><span data-ttu-id="6bb8e-157">앱이 시작 되 면 허브에 매핑</span><span class="sxs-lookup"><span data-stu-id="6bb8e-157">Map to the hub when app starts</span></span>

<span data-ttu-id="6bb8e-158">다음에는 응용 프로그램이 시작 될 때 허브에 대 한 매핑을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-158">Next, you set up mapping to the hub when the application starts.</span></span> <span data-ttu-id="6bb8e-159">SignalR 2에서는 OWIN startup 클래스를 추가 하 여 매핑을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-159">In SignalR 2, adding an OWIN startup class creates the mapping.</span></span>

1. <span data-ttu-id="6bb8e-160">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가** > **새 항목**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-160">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="6bb8e-161">**새 항목 추가-MoveShapeDemo** **Visual C#**  > **웹** > **설치** 를 선택한 다음 **OWIN 시작 클래스**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-161">In **Add New Item - MoveShapeDemo** select **Installed** > **Visual C#** > **Web** and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="6bb8e-162">클래스 이름을 *시작* 으로 하 고 **확인**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-162">Name the class *Startup* and select **OK**.</span></span>

1. <span data-ttu-id="6bb8e-163">*Startup.cs* 파일의 기본 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-163">Replace the default code in the *Startup.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.cs)]

<span data-ttu-id="6bb8e-164">OWIN startup 클래스는 앱이 `Configuration` 메서드를 실행할 때 `MapSignalR`를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-164">The OWIN startup class calls `MapSignalR` when the app executes the `Configuration` method.</span></span> <span data-ttu-id="6bb8e-165">앱은 `OwinStartup` 어셈블리 특성을 사용 하 여 OWIN의 시작 프로세스에 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-165">The app adds the class to OWIN's startup process using the `OwinStartup` assembly attribute.</span></span>

## <a name="add-the-client"></a><span data-ttu-id="6bb8e-166">클라이언트 추가</span><span class="sxs-lookup"><span data-stu-id="6bb8e-166">Add the client</span></span>

<span data-ttu-id="6bb8e-167">클라이언트에 대 한 HTML 페이지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-167">Add the HTML page for the client.</span></span>

1. <span data-ttu-id="6bb8e-168">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 > **HTML 페이지** **추가** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-168">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="6bb8e-169">페이지의 이름을 **Default** 로 하 고 **확인을**선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-169">Name the page **Default** and select **OK**.</span></span>

1. <span data-ttu-id="6bb8e-170">**솔루션 탐색기**에서 *default.aspx* 를 마우스 오른쪽 단추로 클릭 하 고 **시작 페이지로 설정**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-170">In **Solution Explorer**, right-click *Default.html* and select **Set as Start Page**.</span></span>

1. <span data-ttu-id="6bb8e-171">*기본 .html* 파일의 기본 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-171">Replace the default code in the *Default.html* file with this code:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.html?highlight=14-16)]

1. <span data-ttu-id="6bb8e-172">**솔루션 탐색기**에서 **스크립트**를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-172">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="6bb8e-173">JQuery 및 SignalR에 대 한 스크립트 라이브러리는 프로젝트에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-173">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="6bb8e-174">패키지 관리자는 SignalR 스크립트의 최신 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-174">The package manager installs a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="6bb8e-175">프로젝트의 스크립트 파일 버전에 해당 하는 코드 블록의 스크립트 참조를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-175">Update the script references in the code block to correspond to the versions of the script files in the project.</span></span>

<span data-ttu-id="6bb8e-176">이 HTML 및 JavaScript 코드는 `shape`라는 빨간색 `div`를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-176">This HTML and JavaScript code creates a red `div` called `shape`.</span></span> <span data-ttu-id="6bb8e-177">JQuery 라이브러리를 사용 하 여 셰이프의 끌기 동작을 사용 하도록 설정 하 고 `drag` 이벤트를 사용 하 여 셰이프의 위치를 서버에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-177">It enables the shape's dragging behavior using the jQuery library and uses the `drag` event to send the shape's position to the server.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="6bb8e-178">앱 실행</span><span class="sxs-lookup"><span data-stu-id="6bb8e-178">Run the app</span></span>

<span data-ttu-id="6bb8e-179">앱을 실행 하 여 it 업무를 se'e 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-179">You can run the app to se\`e it work.</span></span> <span data-ttu-id="6bb8e-180">셰이프를 브라우저 창 주위로 끌면 셰이프는 다른 브라우저 에서도 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-180">When you drag the shape around a browser window, the shape moves in the other browsers too.</span></span>

1. <span data-ttu-id="6bb8e-181">도구 모음에서 **스크립트 디버깅** 을 사용 하도록 설정 하 고 재생 단추를 선택 하 여 디버그 모드에서 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-181">In the toolbar, turn on **Script Debugging** and then select the play button to run the application in Debug mode.</span></span>

    ![디버깅 모드를 켜고 재생을 선택 하는 사용자의 스크린샷](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)

    <span data-ttu-id="6bb8e-183">오른쪽 위 모서리에 빨간색 모양의 브라우저 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-183">A browser window opens with the red shape in the upper-right corner.</span></span>

1. <span data-ttu-id="6bb8e-184">페이지의 URL을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-184">Copy the page's URL.</span></span>

1. <span data-ttu-id="6bb8e-185">다른 브라우저를 열고 URL을 주소 표시줄에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-185">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="6bb8e-186">셰이프를 브라우저 창 중 하나로 끌어 옵니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-186">Drag the shape in one of the browser windows.</span></span> <span data-ttu-id="6bb8e-187">다른 브라우저 창의 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-187">The shape in the other browser window follows.</span></span>

<span data-ttu-id="6bb8e-188">응용 프로그램에서이 메서드를 사용 하는 동안에는 권장 되는 프로그래밍 모델이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-188">While the application functions using this method, it's not a recommended programming model.</span></span> <span data-ttu-id="6bb8e-189">전송 되는 메시지 수에 대 한 상한 값은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-189">There's no upper limit to the number of messages getting sent.</span></span> <span data-ttu-id="6bb8e-190">결과적으로, 클라이언트와 서버는 메시지와 성능이 저하 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-190">As a result, the clients and server get overwhelmed with messages and performance degrades.</span></span> <span data-ttu-id="6bb8e-191">또한 응용 프로그램은 클라이언트에서 연결이 끊긴 애니메이션을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-191">Also, the app displays a disjointed animation on the client.</span></span> <span data-ttu-id="6bb8e-192">이 jerky 애니메이션은 각 메서드에서 셰이프를 즉시 이동 하기 때문에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-192">This jerky animation happens because the shape moves instantly by each method.</span></span> <span data-ttu-id="6bb8e-193">셰이프를 각 새 위치로 부드럽게 이동 하는 것이 더 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-193">It's better if the shape moves smoothly to each new location.</span></span> <span data-ttu-id="6bb8e-194">다음으로 이러한 문제를 해결 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-194">Next, you learn how to fix those issues.</span></span>

## <a name="add-the-client-loop"></a><span data-ttu-id="6bb8e-195">클라이언트 루프 추가</span><span class="sxs-lookup"><span data-stu-id="6bb8e-195">Add the client loop</span></span>

<span data-ttu-id="6bb8e-196">모든 마우스 이동 이벤트에서 셰이프의 위치를 보내면 불필요 한 양의 네트워크 트래픽이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-196">Sending the location of the shape on every mouse move event creates an unnecessary amount of network traffic.</span></span> <span data-ttu-id="6bb8e-197">응용 프로그램은 클라이언트에서 메시지를 제한 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-197">The app needs to throttle the messages from the client.</span></span>

<span data-ttu-id="6bb8e-198">Javascript `setInterval` 함수를 사용 하 여 고정 속도로 서버에 새 위치 정보를 보내는 루프를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-198">Use the javascript `setInterval` function to set up a loop that sends new position information to the server at a fixed rate.</span></span> <span data-ttu-id="6bb8e-199">이 루프는 "게임 루프"의 기본 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-199">This loop is a basic representation of a "game loop."</span></span> <span data-ttu-id="6bb8e-200">게임의 모든 기능을 구동 하는 반복적으로 호출 되는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-200">It's a repeatedly called function that drives all the functionality of a game.</span></span>

1. <span data-ttu-id="6bb8e-201">*기본 .html* 파일의 클라이언트 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-201">Replace the client code in the *Default.html* file with this code:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.html?highlight=14-16)]

    > [!IMPORTANT]
    > <span data-ttu-id="6bb8e-202">스크립트 참조를 다시 바꾸어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-202">You have to replace the script references again.</span></span> <span data-ttu-id="6bb8e-203">프로젝트의 스크립트 버전과 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-203">They must match the versions of the scripts in the project.</span></span>

    <span data-ttu-id="6bb8e-204">이 새 코드는 `updateServerModel` 함수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-204">This new code adds the `updateServerModel` function.</span></span> <span data-ttu-id="6bb8e-205">고정 된 빈도로 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-205">It gets called on a fixed frequency.</span></span> <span data-ttu-id="6bb8e-206">함수는 `moved` 플래그가 보낼 새 위치 데이터가 있음을 나타내는 경우 항상 서버에 위치 데이터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-206">The function sends the position data to the server whenever the `moved` flag indicates that there's new position data to send.</span></span>

1. <span data-ttu-id="6bb8e-207">응용 프로그램을 시작 하려면 재생 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-207">Select the play button to start the application</span></span>

1. <span data-ttu-id="6bb8e-208">페이지의 URL을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-208">Copy the page's URL.</span></span>

1. <span data-ttu-id="6bb8e-209">다른 브라우저를 열고 URL을 주소 표시줄에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-209">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="6bb8e-210">셰이프를 브라우저 창 중 하나로 끌어 옵니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-210">Drag the shape in one of the browser windows.</span></span> <span data-ttu-id="6bb8e-211">다른 브라우저 창의 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-211">The shape in the other browser window follows.</span></span>

<span data-ttu-id="6bb8e-212">앱은 서버로 전송 되는 메시지 수를 제한 처음에는 애니메이션이 부드러운 것으로 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-212">Since the app throttles the number of messages that get sent to the server, the animation won't appear as smooth did at first.</span></span>

## <a name="add-the-server-loop"></a><span data-ttu-id="6bb8e-213">서버 루프 추가</span><span class="sxs-lookup"><span data-stu-id="6bb8e-213">Add the server loop</span></span>

<span data-ttu-id="6bb8e-214">현재 응용 프로그램에서는 서버에서 클라이언트로 전송 된 메시지가 수신 되는 횟수 만큼 계속 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-214">In the current application, messages sent from the server to the client go out as often as they're received.</span></span> <span data-ttu-id="6bb8e-215">이 네트워크 트래픽은 클라이언트에 표시 되는 것과 비슷한 문제를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-215">This network traffic presents a similar problem as we see on the client.</span></span>

<span data-ttu-id="6bb8e-216">앱은 필요한 것 보다 더 자주 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-216">The app can send messages more often than they're needed.</span></span> <span data-ttu-id="6bb8e-217">결과적으로 연결에 대 한 연결이 초과 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-217">The connection can become flooded as a result.</span></span> <span data-ttu-id="6bb8e-218">이 섹션에서는 보내는 메시지의 요금을 제한 타이머를 추가 하도록 서버를 업데이트 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-218">This section describes how to update the server to add a timer that throttles the rate of the outgoing messages.</span></span>

1. <span data-ttu-id="6bb8e-219">`MoveShapeHub.cs` 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-219">Replace the contents of `MoveShapeHub.cs` with this code:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

1. <span data-ttu-id="6bb8e-220">재생 단추를 선택 하 여 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-220">Select the play button to start the application.</span></span>

1. <span data-ttu-id="6bb8e-221">페이지의 URL을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-221">Copy the page's URL.</span></span>

1. <span data-ttu-id="6bb8e-222">다른 브라우저를 열고 URL을 주소 표시줄에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-222">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="6bb8e-223">셰이프를 브라우저 창 중 하나로 끌어 옵니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-223">Drag the shape in one of the browser windows.</span></span>

<span data-ttu-id="6bb8e-224">이 코드는 클라이언트를 확장 하 여 `Broadcaster` 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-224">This code expands the client to add the `Broadcaster` class.</span></span> <span data-ttu-id="6bb8e-225">새 클래스는 .NET framework의 `Timer` 클래스를 사용 하 여 나가는 메시지를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-225">The new class throttles the outgoing messages using the `Timer` class from the .NET framework.</span></span>

<span data-ttu-id="6bb8e-226">허브 자체가 일시적 이라고 이해 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-226">It's good to learn that the hub itself is transitory.</span></span> <span data-ttu-id="6bb8e-227">필요할 때마다 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-227">It's created every time it's needed.</span></span> <span data-ttu-id="6bb8e-228">따라서 앱은 단일 항목으로 `Broadcaster`를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-228">So the app creates the `Broadcaster` as a singleton.</span></span> <span data-ttu-id="6bb8e-229">지연 초기화를 사용 하 여 필요할 때까지 `Broadcaster`생성을 지연 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-229">It uses lazy initialization to defer the `Broadcaster`'s creation until it's needed.</span></span> <span data-ttu-id="6bb8e-230">이렇게 하면 앱이 타이머를 시작 하기 전에 첫 번째 허브 인스턴스를 완전히 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-230">That guarantees that the app creates the first hub instance completely before starting the timer.</span></span>

<span data-ttu-id="6bb8e-231">그런 다음 클라이언트의 `UpdateShape` 함수에 대 한 호출이 허브의 `UpdateModel` 메서드에서 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-231">The call to the clients' `UpdateShape` function is then moved out of the hub's `UpdateModel` method.</span></span> <span data-ttu-id="6bb8e-232">앱이 들어오는 메시지를 받을 때마다 즉시 더 이상 호출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-232">It's no longer called immediately whenever the app receives incoming messages.</span></span> <span data-ttu-id="6bb8e-233">대신, 앱에서 초당 25 번의 호출 속도로 클라이언트에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-233">Instead, the app sends the messages to the clients at a rate of 25 calls per second.</span></span> <span data-ttu-id="6bb8e-234">프로세스는 `Broadcaster` 클래스 내에서 `_broadcastLoop` 타이머를 통해 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-234">The process is  managed by the `_broadcastLoop` timer from within the `Broadcaster` class.</span></span>

<span data-ttu-id="6bb8e-235">마지막으로, 허브에서 직접 클라이언트 메서드를 호출 하는 대신 `Broadcaster` 클래스가 현재 작동 하는 `_hubContext` 허브에 대 한 참조를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-235">Lastly, instead of calling the client method from the hub directly, the `Broadcaster` class needs to get a reference to the currently operating `_hubContext` hub.</span></span> <span data-ttu-id="6bb8e-236">`GlobalHost`를 사용 하 여 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-236">It gets the reference with the `GlobalHost`.</span></span>

## <a name="add-smooth-animation"></a><span data-ttu-id="6bb8e-237">부드러운 애니메이션 추가</span><span class="sxs-lookup"><span data-stu-id="6bb8e-237">Add smooth animation</span></span>

<span data-ttu-id="6bb8e-238">응용 프로그램이 거의 완료 되었지만 한 가지 향상 된 기능을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-238">The application is almost finished, but we could make one more improvement.</span></span> <span data-ttu-id="6bb8e-239">앱은 서버 메시지에 대 한 응답으로 클라이언트에서 셰이프를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-239">The app moves the shape on the client in response to server messages.</span></span> <span data-ttu-id="6bb8e-240">서버에서 제공 하는 새 위치로 셰이프의 위치를 설정 하는 대신 JQuery UI 라이브러리의 `animate` 함수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-240">Instead of setting the position of the shape to the new location given by the server, use the JQuery UI library's `animate` function.</span></span> <span data-ttu-id="6bb8e-241">현재 위치와 새 위치 간에 셰이프를 매끄럽게 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-241">It can move the shape smoothly between its current and new position.</span></span>

1. <span data-ttu-id="6bb8e-242">*기본 .html* 파일의 클라이언트 `updateShape` 메서드를 강조 표시 된 코드와 같이 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-242">Update the client's `updateShape` method in the *Default.html* file to look like the highlighted code:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.html?highlight=33-40)]

1. <span data-ttu-id="6bb8e-243">재생 단추를 선택 하 여 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-243">Select the play button to start the application.</span></span>

1. <span data-ttu-id="6bb8e-244">페이지의 URL을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-244">Copy the page's URL.</span></span>

1. <span data-ttu-id="6bb8e-245">다른 브라우저를 열고 URL을 주소 표시줄에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-245">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="6bb8e-246">셰이프를 브라우저 창 중 하나로 끌어 옵니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-246">Drag the shape in one of the browser windows.</span></span>

<span data-ttu-id="6bb8e-247">다른 창에서 셰이프의 이동이 jerky 작은 것으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-247">The movement of the shape in the other window appears less jerky.</span></span> <span data-ttu-id="6bb8e-248">앱은 들어오는 메시지 마다 한 번만 설정 되는 것이 아니라 시간에 따라 이동 하는 동작을 보간합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-248">The app interpolates its movement over time rather than being set once per incoming message.</span></span>

<span data-ttu-id="6bb8e-249">이 코드는 셰이프를 이전 위치에서 새 위치로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-249">This code moves the shape from the old location to the new one.</span></span> <span data-ttu-id="6bb8e-250">서버는 애니메이션 간격 과정에서 셰이프의 위치를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-250">The server gives the position of the shape over the course of the animation interval.</span></span> <span data-ttu-id="6bb8e-251">이 경우 100 밀리초입니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-251">In this case, that's 100 milliseconds.</span></span> <span data-ttu-id="6bb8e-252">앱은 새 애니메이션을 시작 하기 전에 셰이프에서 실행 중인 이전 애니메이션을 모두 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-252">The app clears any previous animation running on the shape before the new animation starts.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="6bb8e-253">코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="6bb8e-253">Get the code</span></span>

[<span data-ttu-id="6bb8e-254">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="6bb8e-254">Download Completed Project</span></span>](https://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a)

## <a name="additional-resources"></a><span data-ttu-id="6bb8e-255">추가 자료</span><span class="sxs-lookup"><span data-stu-id="6bb8e-255">Additional resources</span></span>

<span data-ttu-id="6bb8e-256">위에서 배운 통신 패러다임은 [SignalR를 사용 하 여 만든 ShootR 게임과](https://shootr.azurewebsites.net/)같이 온라인 게임 및 기타 시뮬레이션을 개발 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-256">The communication paradigm you just learned about is useful for developing online games and other simulations, like [the ShootR game created with SignalR](https://shootr.azurewebsites.net/).</span></span>

<span data-ttu-id="6bb8e-257">SignalR에 대 한 자세한 내용은 다음 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-257">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="6bb8e-258">SignalR 프로젝트</span><span class="sxs-lookup"><span data-stu-id="6bb8e-258">SignalR Project</span></span>](http://signalr.net)

* [<span data-ttu-id="6bb8e-259">SignalR GitHub 및 샘플</span><span class="sxs-lookup"><span data-stu-id="6bb8e-259">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)

* [<span data-ttu-id="6bb8e-260">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="6bb8e-260">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="6bb8e-261">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6bb8e-261">Next steps</span></span>

<span data-ttu-id="6bb8e-262">이 자습서에서는 다음과 같은 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-262">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6bb8e-263">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="6bb8e-263">Set up the project</span></span>
> * <span data-ttu-id="6bb8e-264">기본 응용 프로그램을 만듦</span><span class="sxs-lookup"><span data-stu-id="6bb8e-264">Created the base application</span></span>
> * <span data-ttu-id="6bb8e-265">앱이 시작 될 때 허브에 매핑됨</span><span class="sxs-lookup"><span data-stu-id="6bb8e-265">Mapped to the hub when app starts</span></span>
> * <span data-ttu-id="6bb8e-266">클라이언트 추가</span><span class="sxs-lookup"><span data-stu-id="6bb8e-266">Added the client</span></span>
> * <span data-ttu-id="6bb8e-267">앱 실행</span><span class="sxs-lookup"><span data-stu-id="6bb8e-267">Ran the app</span></span>
> * <span data-ttu-id="6bb8e-268">클라이언트 루프가 추가 됨</span><span class="sxs-lookup"><span data-stu-id="6bb8e-268">Added the client loop</span></span>
> * <span data-ttu-id="6bb8e-269">서버 루프가 추가 됨</span><span class="sxs-lookup"><span data-stu-id="6bb8e-269">Added the server loop</span></span>
> * <span data-ttu-id="6bb8e-270">부드러운 애니메이션 추가</span><span class="sxs-lookup"><span data-stu-id="6bb8e-270">Added smooth animation</span></span>

<span data-ttu-id="6bb8e-271">ASP.NET SignalR 2를 사용 하 여 서버 브로드캐스트 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 알아보려면 다음 문서로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb8e-271">Advance to the next article to learn how to create a web application that uses ASP.NET SignalR 2 to provide server broadcast functionality.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="6bb8e-272">SignalR 2 및 서버 브로드캐스팅</span><span class="sxs-lookup"><span data-stu-id="6bb8e-272">SignalR 2 and server broadcasting</span></span>](tutorial-server-broadcast-with-signalr.md)