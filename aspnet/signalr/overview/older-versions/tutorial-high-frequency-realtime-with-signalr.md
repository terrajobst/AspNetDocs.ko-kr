---
uid: signalr/overview/older-versions/tutorial-high-frequency-realtime-with-signalr
title: SignalR 1.x를 사용 하는 높은 빈도 실시간 Microsoft Docs
author: bradygaster
description: 이 자습서에서는 ASP.NET SignalR를 사용 하 여 높은 빈도의 메시징 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다. 빈도가 높은 메시징 ...
ms.author: bradyg
ms.date: 04/16/2013
ms.assetid: ad2a5da5-2e79-40ea-bc84-028d327f5982
msc.legacyurl: /signalr/overview/older-versions/tutorial-high-frequency-realtime-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: e37e63a410952ec170cbbaadeeb54eae7e82b3b5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505715"
---
# <a name="high-frequency-realtime-with-signalr-1x"></a><span data-ttu-id="9ae99-104">SignalR 1.x를 사용하는 고주파수 실시간</span><span class="sxs-lookup"><span data-stu-id="9ae99-104">High-Frequency Realtime with SignalR 1.x</span></span>

<span data-ttu-id="9ae99-105">[Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="9ae99-105">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="9ae99-106">이 자습서에서는 ASP.NET SignalR를 사용 하 여 높은 빈도의 메시징 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-106">This tutorial shows how to create a web application that uses ASP.NET SignalR to provide high-frequency messaging functionality.</span></span> <span data-ttu-id="9ae99-107">이 경우 빈도가 높은 메시징은 고정 속도로 전송 되는 업데이트를 의미 합니다. 이 응용 프로그램의 경우 최대 10 개의 메시지가 1 초입니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-107">High-frequency messaging in this case means updates that are sent at a fixed rate; in the case of this application, up to 10 messages a second.</span></span>
> 
> <span data-ttu-id="9ae99-108">이 자습서에서 만들 응용 프로그램은 사용자가 끌 수 있는 셰이프를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-108">The application you'll create in this tutorial displays a shape that users can drag.</span></span> <span data-ttu-id="9ae99-109">그러면 연결 된 다른 모든 브라우저의 셰이프 위치가 시간 업데이트를 사용 하 여 끌어 온 모양의 위치와 일치 하도록 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-109">The position of the shape in all other connected browsers will then be updated to match the position of the dragged shape using timed updates.</span></span>
> 
> <span data-ttu-id="9ae99-110">이 자습서에 소개 된 개념에는 실시간 게임과 기타 시뮬레이션 응용 프로그램의 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-110">Concepts introduced in this tutorial have applications in real-time gaming and other simulation applications.</span></span>
> 
> <span data-ttu-id="9ae99-111">자습서에 대 한 의견을 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-111">Comments on the tutorial are welcome.</span></span> <span data-ttu-id="9ae99-112">자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com)에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-112">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com).</span></span>

## <a name="overview"></a><span data-ttu-id="9ae99-113">개요</span><span class="sxs-lookup"><span data-stu-id="9ae99-113">Overview</span></span>

<span data-ttu-id="9ae99-114">이 자습서에서는 다른 브라우저와 개체의 상태를 실시간으로 공유 하는 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-114">This tutorial demonstrates how to create an application that shares the state of an object with other browsers in real time.</span></span> <span data-ttu-id="9ae99-115">만들 응용 프로그램을 MoveShape 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-115">The application we'll create is called MoveShape.</span></span> <span data-ttu-id="9ae99-116">MoveShape 페이지에는 사용자가 끌 수 있는 HTML Div 요소가 표시 됩니다. 사용자가 Div를 끌면 새 위치가 서버에 전송 되 고, 그 다음에는 연결 된 다른 모든 클라이언트가 일치 하도록 셰이프 위치를 업데이트 하는 것을 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-116">The MoveShape page will display an HTML Div element that the user can drag; when the user drags the Div, its new position will be sent to the server, which will then tell all other connected clients to update the shape's position to match.</span></span>

![응용 프로그램 창](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

<span data-ttu-id="9ae99-118">이 자습서에서 만든 응용 프로그램은 Damian Edwards 데모를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-118">The application created in this tutorial is based on a demo by Damian Edwards.</span></span> <span data-ttu-id="9ae99-119">이 데모를 포함 하는 비디오는 [여기](https://channel9.msdn.com/Series/Building-Web-Apps-with-ASP-NET-Jump-Start/Building-Web-Apps-with-ASPNET-Jump-Start-08-Real-time-Communication-with-SignalR)에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-119">A video containing this demo can be seen [here](https://channel9.msdn.com/Series/Building-Web-Apps-with-ASP-NET-Jump-Start/Building-Web-Apps-with-ASPNET-Jump-Start-08-Real-time-Communication-with-SignalR).</span></span>

<span data-ttu-id="9ae99-120">이 자습서에서는 셰이프를 끌 때 발생 하는 각 이벤트에서 SignalR 메시지를 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-120">The tutorial will start by demonstrating how to send SignalR messages from each event that fires as the shape is dragged.</span></span> <span data-ttu-id="9ae99-121">그러면 연결 된 각 클라이언트는 메시지를 받을 때마다 셰이프의 로컬 버전 위치를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-121">Each connected client will then update the position of the local version of the shape each time a message is received.</span></span>

<span data-ttu-id="9ae99-122">응용 프로그램은이 메서드를 사용 하 여 작동 하는 동안에는 전송 되는 메시지 수에 대 한 상한 제한이 없기 때문에 권장 되는 프로그래밍 모델이 아닙니다. 따라서 클라이언트와 서버에서 메시지와 성능이 저하 될 수 있습니다. .</span><span class="sxs-lookup"><span data-stu-id="9ae99-122">While the application will function using this method, this is not a recommended programming model, since there would be no upper limit to the number of messages getting sent, so the clients and server could get overwhelmed with messages and performance would degrade.</span></span> <span data-ttu-id="9ae99-123">셰이프를 각 메서드에서 즉시 이동 하는 것이 아니라 각 새 위치로 이동 하는 것이 아니라 클라이언트에서 표시 되는 애니메이션도 연결 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-123">The displayed animation on the client would also be disjointed, as the shape would be moved instantly by each method, rather than moving smoothly to each new location.</span></span> <span data-ttu-id="9ae99-124">자습서의 뒷부분에 나오는 섹션에서는 클라이언트 또는 서버에서 메시지를 전송 하는 최대 속도를 제한 하는 타이머 함수를 만드는 방법과 위치 간에 셰이프를 부드럽게 이동 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-124">Later sections of the tutorial will demonstrate how to create a timer function that restricts the maximum rate at which messages are sent by either the client or server, and how to move the shape smoothly between locations.</span></span> <span data-ttu-id="9ae99-125">이 자습서에서 만든 응용 프로그램의 최종 버전은 [코드 갤러리](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-125">The final version of the application created in this tutorial can be downloaded from [Code Gallery](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6).</span></span>

<span data-ttu-id="9ae99-126">이 자습서에는 다음과 같은 섹션이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-126">This tutorial contains the following sections:</span></span>

- [<span data-ttu-id="9ae99-127">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="9ae99-127">Prerequisites</span></span>](#prerequisites)
- [<span data-ttu-id="9ae99-128">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="9ae99-128">Create the project</span></span>](#createtheproject)
- [<span data-ttu-id="9ae99-129">ASP.NET SignalR 및 JQuery NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-129">Add the ASP.NET SignalR and JQuery.UI NuGet packages</span></span>](#nugetpackages)
- [<span data-ttu-id="9ae99-130">기본 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="9ae99-130">Create the base application</span></span>](#baseapp)
- [<span data-ttu-id="9ae99-131">클라이언트 루프 추가</span><span class="sxs-lookup"><span data-stu-id="9ae99-131">Add the client loop</span></span>](#clientloop)
- [<span data-ttu-id="9ae99-132">서버 루프 추가</span><span class="sxs-lookup"><span data-stu-id="9ae99-132">Add the server loop</span></span>](#serverloop)
- [<span data-ttu-id="9ae99-133">클라이언트에서 부드러운 애니메이션 추가</span><span class="sxs-lookup"><span data-stu-id="9ae99-133">Add smooth animation on the client</span></span>](#animation)
- [<span data-ttu-id="9ae99-134">추가 단계</span><span class="sxs-lookup"><span data-stu-id="9ae99-134">Further Steps</span></span>](#furthersteps)

<a id="prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="9ae99-135">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="9ae99-135">Prerequisites</span></span>

<span data-ttu-id="9ae99-136">이 자습서에는 Visual Studio 2012 또는 Visual Studio 2010이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-136">This tutorial requires Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="9ae99-137">Visual Studio 2010을 사용 하는 경우 프로젝트는 .NET Framework 4.5이 아닌 .NET Framework 4를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-137">If Visual Studio 2010 is used, the project will use .NET Framework 4 rather than .NET Framework 4.5.</span></span>

<span data-ttu-id="9ae99-138">Visual Studio 2012을 사용 하는 경우 [ASP.NET 및 Web Tools 2012.2 업데이트](https://go.microsoft.com/fwlink/?LinkId=282650)를 설치 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-138">If you are using Visual Studio 2012, it's recommended that you install the [ASP.NET and Web Tools 2012.2 update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="9ae99-139">이 업데이트에는 게시, 새 기능 및 새 템플릿과 같은 새로운 기능이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-139">This update contains new features such as enhancements to publishing, new functionality, and new templates.</span></span>

<span data-ttu-id="9ae99-140">Visual Studio 2010을 사용 하는 경우 [NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) 이 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-140">If you have Visual Studio 2010, make sure that [NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) is installed.</span></span>

<a id="createtheproject"></a>

## <a name="create-the-project"></a><span data-ttu-id="9ae99-141">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="9ae99-141">Create the project</span></span>

<span data-ttu-id="9ae99-142">이 섹션에서는 Visual Studio에서 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-142">In this section, we'll create the project in Visual Studio.</span></span>

1. <span data-ttu-id="9ae99-143">**파일** 메뉴에서 **새 프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-143">From the **File** menu click **New Project**.</span></span>
2. <span data-ttu-id="9ae99-144">**새 프로젝트** 대화 상자에서 **템플릿** 을 확장 **C#** 하 고 **웹**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-144">In the **New Project** dialog box, expand **C#** under **Templates** and select **Web**.</span></span>
3. <span data-ttu-id="9ae99-145">**ASP.NET Empty 웹 응용 프로그램** 템플릿을 선택 하 고 프로젝트 이름을 *MoveShapeDemo*로 선택한 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-145">Select the **ASP.NET Empty Web Application** template, name the project *MoveShapeDemo*, and click **OK**.</span></span>

    ![새 프로젝트 만들기](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)

<a id="nugetpackages"></a>

## <a name="add-the-signalr-and-jqueryui-nuget-packages"></a><span data-ttu-id="9ae99-147">SignalR 및 JQuery NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-147">Add the SignalR and JQuery.UI NuGet Packages</span></span>

<span data-ttu-id="9ae99-148">NuGet 패키지를 설치 하 여 프로젝트에 SignalR 기능을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-148">You can add SignalR functionality to a project by installing a NuGet package.</span></span> <span data-ttu-id="9ae99-149">이 자습서에서는 또한 셰이프를 끌어서 애니메이션 효과를 주는 데 사용할 수 있도록 JQuery 패키지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-149">This tutorial will also use the JQuery.UI package for allowing the shape to be dragged and animated.</span></span>

1. <span data-ttu-id="9ae99-150">도구 |를 클릭 합니다.  **NuGet 패키지 관리자 | 패키지 관리자 콘솔**.</span><span class="sxs-lookup"><span data-stu-id="9ae99-150">Click **Tools | NuGet Package Manager | Package Manager Console**.</span></span>
2. <span data-ttu-id="9ae99-151">패키지 관리자에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-151">Enter the following command in the package manager.</span></span>

    [!code-powershell[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.ps1)]

    <span data-ttu-id="9ae99-152">SignalR 패키지는 다양 한 NuGet 패키지를 종속성으로 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-152">The SignalR package installs a number of other NuGet packages as dependencies.</span></span> <span data-ttu-id="9ae99-153">설치가 완료 되 면 ASP.NET 응용 프로그램에서 SignalR를 사용 하는 데 필요한 모든 서버 및 클라이언트 구성 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-153">When the installation is finished you have all of the server and client components required to use SignalR in an ASP.NET application.</span></span>
3. <span data-ttu-id="9ae99-154">패키지 관리자 콘솔에 다음 명령을 입력 하 여 JQuery 및 JQuery. n u l l 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-154">Enter the following command into the package manager console to install the JQuery and JQuery.UI packages.</span></span>

    [!code-powershell[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.ps1)]

<a id="baseapp"></a>

## <a name="create-the-base-application"></a><span data-ttu-id="9ae99-155">기본 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="9ae99-155">Create the base application</span></span>

<span data-ttu-id="9ae99-156">이 섹션에서는 각 마우스 이동 이벤트 동안 셰이프의 위치를 서버로 보내는 브라우저 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-156">In this section, we'll create a browser application that sends the location of the shape to the server during each mouse move event.</span></span> <span data-ttu-id="9ae99-157">그런 다음 서버는 수신 될 때 연결 된 다른 모든 클라이언트에이 정보를 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-157">The server then broadcasts this information to all other connected clients as it is received.</span></span> <span data-ttu-id="9ae99-158">이후 섹션에서이 응용 프로그램을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-158">We'll expand on this application in later sections.</span></span>

1. <span data-ttu-id="9ae99-159">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**, **클래스 ...** 를 차례로 선택 합니다. 클래스 이름을 **MoveShapeHub** 로 하 고 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-159">In **Solution Explorer**, right-click on the project and select **Add**, **Class...**. Name the class **MoveShapeHub** and click **Add**.</span></span>
2. <span data-ttu-id="9ae99-160">새 **MoveShapeHub** 클래스의 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-160">Replace the code in the new **MoveShapeHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.cs)]

    <span data-ttu-id="9ae99-161">위의 `MoveShapeHub` 클래스는 SignalR hub의 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-161">The `MoveShapeHub` class above is an implementation of a SignalR hub.</span></span> <span data-ttu-id="9ae99-162">[SignalR 시작](index.md) 자습서에서와 같이 허브에는 클라이언트가 직접 호출 하는 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-162">As in the [Getting Started with SignalR](index.md) tutorial, the hub has a method that the clients will call directly.</span></span> <span data-ttu-id="9ae99-163">이 경우 클라이언트는 셰이프의 새 X 및 Y 좌표를 포함 하는 개체를 서버에 전송 합니다. 그러면 연결 된 다른 모든 클라이언트에 브로드캐스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-163">In this case, the client will send an object containing the new X and Y coordinates of the shape to the server, which then gets broadcasted to all other connected clients.</span></span> <span data-ttu-id="9ae99-164">SignalR는 JSON을 사용 하 여이 개체를 자동으로 직렬화 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-164">SignalR will automatically serialize this object using JSON.</span></span>

    <span data-ttu-id="9ae99-165">클라이언트에 전송 되는 개체 (`ShapeModel`)에는 셰이프의 위치를 저장 하는 멤버가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-165">The object that will be sent to the client (`ShapeModel`) contains members to store the position of the shape.</span></span> <span data-ttu-id="9ae99-166">서버에 있는 개체의 버전에는 저장 되는 클라이언트 데이터를 추적 하는 멤버도 포함 되어 있으므로 지정 된 클라이언트는 자신의 데이터를 전송 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-166">The version of the object on the server also contains a member to track which client's data is being stored, so that a given client won't be sent their own data.</span></span> <span data-ttu-id="9ae99-167">이 멤버는 `JsonIgnore` 특성을 사용 하 여 serialize 되어 클라이언트에 전송 되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-167">This member uses the `JsonIgnore` attribute to keep it from being serialized and sent to the client.</span></span>
3. <span data-ttu-id="9ae99-168">다음으로, 응용 프로그램이 시작 될 때 허브를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-168">Next, we'll set up the hub when the application starts.</span></span> <span data-ttu-id="9ae99-169">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 **추가 |를 클릭 합니다. 전역 응용 프로그램 클래스**입니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-169">In **Solution Explorer**, right-click the project, then click **Add | Global Application Class**.</span></span> <span data-ttu-id="9ae99-170">*Global* 의 기본 이름을 그대로 적용 하 고 **확인을**클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-170">Accept the default name of *Global* and click **OK**.</span></span>

    ![전역 응용 프로그램 클래스 추가](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)
4. <span data-ttu-id="9ae99-172">Global.asax.cs 클래스에서 제공 된 **using** 문 뒤에 다음 `using` 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-172">Add the following `using` statement after the provided **using** statements in the Global.asax.cs class.</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.cs)]
5. <span data-ttu-id="9ae99-173">SignalR에 대 한 기본 경로를 등록 하려면 전역 클래스의 `Application_Start` 메서드에 다음 코드 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-173">Add the following line of code in the `Application_Start` method of the Global class to register the default route for SignalR.</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

    <span data-ttu-id="9ae99-174">Global.asax 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-174">Your global.asax file should look like the following:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.cs)]
6. <span data-ttu-id="9ae99-175">다음으로 클라이언트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-175">Next, we'll add the client.</span></span> <span data-ttu-id="9ae99-176">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 **추가 |를 클릭 합니다. 새 항목**입니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-176">In **Solution Explorer**, right-click the project, then click **Add | New Item**.</span></span> <span data-ttu-id="9ae99-177">**새 항목 추가** 대화 상자에서 **Html 페이지**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-177">In the **Add New Item** dialog, select **Html Page**.</span></span> <span data-ttu-id="9ae99-178">페이지에 적절 한 이름 (예: **.html**)을 지정 하 고 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-178">Give the page an appropriate name (like **Default.html**) and click **Add**.</span></span>
7. <span data-ttu-id="9ae99-179">**솔루션 탐색기**에서 방금 만든 페이지를 마우스 오른쪽 단추로 클릭 하 고 **시작 페이지로 설정**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-179">In **Solution Explorer**, right-click the page you just created and click **Set as Start Page**.</span></span>
8. <span data-ttu-id="9ae99-180">HTML 페이지의 기본 코드를 다음 코드 조각으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-180">Replace the default code in the HTML page with the following code snippet.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9ae99-181">아래의 스크립트 참조가 Scripts 폴더의 프로젝트에 추가 된 패키지와 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-181">Verify that the script references below match the packages added to your project in the Scripts folder.</span></span> <span data-ttu-id="9ae99-182">Visual Studio 2010에서는 프로젝트에 추가 된 JQuery 및 SignalR 버전이 아래 버전 번호와 일치 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-182">In Visual Studio 2010, the version of JQuery and SignalR added to the project may not match the version numbers below.</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample7.html)]

    <span data-ttu-id="9ae99-183">위의 HTML 및 JavaScript 코드는 Shape 라는 빨간 Div를 만들고, jQuery 라이브러리를 사용 하 여 셰이프의 끌기 동작을 사용 하도록 설정 하 고, 셰이프의 `drag` 이벤트를 사용 하 여 셰이프의 위치를 서버로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-183">The above HTML and JavaScript code creates a red Div called Shape, enables the shape's dragging behavior using the jQuery library, and uses the shape's `drag` event to send the shape's position to the server.</span></span>
9. <span data-ttu-id="9ae99-184">F5 키를 눌러 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-184">Start the application by pressing F5.</span></span> <span data-ttu-id="9ae99-185">페이지의 URL을 복사 하 여 두 번째 브라우저 창에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-185">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="9ae99-186">셰이프를 브라우저 창 중 하나로 끌어 옵니다. 다른 브라우저 창의 셰이프는 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-186">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span>

    ![응용 프로그램 창](tutorial-high-frequency-realtime-with-signalr/_static/image4.png)

<a id="clientloop"></a>

## <a name="add-the-client-loop"></a><span data-ttu-id="9ae99-188">클라이언트 루프 추가</span><span class="sxs-lookup"><span data-stu-id="9ae99-188">Add the client loop</span></span>

<span data-ttu-id="9ae99-189">모든 마우스 이동 이벤트에서 셰이프의 위치를 전송 하면 불필요 한 양의 네트워크 트래픽이 생성 되므로 클라이언트의 메시지를 제한 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-189">Since sending the location of the shape on every mouse move event will create an unnecessary amount of network traffic, the messages from the client need to be throttled.</span></span> <span data-ttu-id="9ae99-190">Javascript `setInterval` 함수를 사용 하 여 고정 속도로 서버에 새 위치 정보를 보내는 루프를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-190">We'll use the javascript `setInterval` function to set up a loop that sends new position information to the server at a fixed rate.</span></span> <span data-ttu-id="9ae99-191">이 루프는 게임 또는 기타 시뮬레이션의 모든 기능을 구동 하는 반복적인 호출 함수 인 "게임 루프"를 매우 기본적으로 표현한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-191">This loop is a very basic representation of a "game loop", a repeatedly called function that drives all of the functionality of a game or other simulation.</span></span>

1. <span data-ttu-id="9ae99-192">HTML 페이지의 클라이언트 코드를 다음 코드 조각과 일치 하도록 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-192">Update the client code in the HTML page to match the following code snippet.</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample8.html)]

    <span data-ttu-id="9ae99-193">위의 업데이트는 고정 된 빈도로 호출 되는 `updateServerModel` 함수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-193">The above update adds the `updateServerModel` function, which gets called on a fixed frequency.</span></span> <span data-ttu-id="9ae99-194">이 함수는 `moved` 플래그가 보낼 새 위치 데이터가 있음을 나타내는 경우 항상 서버에 위치 데이터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-194">This function sends the position data to the server whenever the `moved` flag indicates that there is new position data to send.</span></span>
2. <span data-ttu-id="9ae99-195">F5 키를 눌러 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-195">Start the application by pressing F5.</span></span> <span data-ttu-id="9ae99-196">페이지의 URL을 복사 하 여 두 번째 브라우저 창에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-196">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="9ae99-197">셰이프를 브라우저 창 중 하나로 끌어 옵니다. 다른 브라우저 창의 셰이프는 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-197">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span> <span data-ttu-id="9ae99-198">서버로 전송 되는 메시지 수가 제한 되기 때문에 이전 섹션에서 애니메이션은 부드러운 모양으로 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-198">Since the number of messages that get sent to the server will be throttled, the animation will not appear as smooth as in the previous section.</span></span>

    ![응용 프로그램 창](tutorial-high-frequency-realtime-with-signalr/_static/image5.png)

<a id="serverloop"></a>

## <a name="add-the-server-loop"></a><span data-ttu-id="9ae99-200">서버 루프 추가</span><span class="sxs-lookup"><span data-stu-id="9ae99-200">Add the server loop</span></span>

<span data-ttu-id="9ae99-201">현재 응용 프로그램에서는 서버에서 클라이언트로 전송 되는 메시지가 수신 되는 횟수 만큼 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-201">In the current application, messages sent from the server to the client go out as often as they are received.</span></span> <span data-ttu-id="9ae99-202">이는 클라이언트에 표시 된 것과 비슷한 문제를 표시 합니다. 메시지는 필요한 것 보다 더 자주 전송 될 수 있으며, 그에 따라 연결이 유발 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-202">This presents a similar problem as was seen on the client; messages can be sent more often than they are needed, and the connection could become flooded as a result.</span></span> <span data-ttu-id="9ae99-203">이 섹션에서는 보내는 메시지의 요금을 제한 하는 타이머를 구현 하도록 서버를 업데이트 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-203">This section describes how to update the server to implement a timer that throttles the rate of the outgoing messages.</span></span>

1. <span data-ttu-id="9ae99-204">`MoveShapeHub.cs` 내용을 다음 코드 조각으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-204">Replace the contents of `MoveShapeHub.cs` with the following code snippet.</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample9.cs)]

    <span data-ttu-id="9ae99-205">위의 코드는 클라이언트를 확장 하 여 `Broadcaster` 클래스를 추가 합니다 .이 클래스는 .NET framework에서 `Timer` 클래스를 사용 하 여 나가는 메시지를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-205">The above code expands the client to add the `Broadcaster` class, which throttles the outgoing messages using the `Timer` class from the .NET framework.</span></span>

    <span data-ttu-id="9ae99-206">허브 자체는 일시적 이므로 (필요할 때마다 만들어짐) `Broadcaster` 단일 항목으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-206">Since the hub itself is transitory (it is created every time it is needed), the `Broadcaster` will be created as a singleton.</span></span> <span data-ttu-id="9ae99-207">초기화 지연 (.NET 4에 도입 됨)은 필요할 때까지 생성을 지연 하 여 타이머를 시작 하기 전에 첫 번째 허브 인스턴스가 완전히 만들어졌는지 확인 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-207">Lazy initialization (introduced in .NET 4) is used to defer its creation until it is needed, ensuring that the first hub instance is completely created before the timer is started.</span></span>

    <span data-ttu-id="9ae99-208">클라이언트의 `UpdateShape` 함수에 대 한 호출은 허브의 `UpdateModel` 메서드에서 이동 하 여 들어오는 메시지가 수신 될 때마다 즉시 호출 되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-208">The call to the clients' `UpdateShape` function is then moved out of the hub's `UpdateModel` method, so that it is no longer called immediately whenever incoming messages are received.</span></span> <span data-ttu-id="9ae99-209">대신 클라이언트에 대 한 메시지는 `Broadcaster` 클래스 내에서 `_broadcastLoop` 타이머에 의해 관리 되는 초당 25 개의 호출 속도로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-209">Instead, the messages to the clients will be sent at a rate of 25 calls per second, managed by the `_broadcastLoop` timer from within the `Broadcaster` class.</span></span>

    <span data-ttu-id="9ae99-210">마지막으로, 허브에서 직접 클라이언트 메서드를 호출 하는 대신 `Broadcaster` 클래스가 `GlobalHost`를 사용 하 여 현재 운영 허브 (`_hubContext`)에 대 한 참조를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-210">Lastly, instead of calling the client method from the hub directly, the `Broadcaster` class needs to obtain a reference to the currently operating hub (`_hubContext`) using the `GlobalHost`.</span></span>
2. <span data-ttu-id="9ae99-211">F5 키를 눌러 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-211">Start the application by pressing F5.</span></span> <span data-ttu-id="9ae99-212">페이지의 URL을 복사 하 여 두 번째 브라우저 창에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-212">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="9ae99-213">셰이프를 브라우저 창 중 하나로 끌어 옵니다. 다른 브라우저 창의 셰이프는 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-213">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span> <span data-ttu-id="9ae99-214">브라우저에는 이전 섹션의 차이점이 표시 되지 않지만 클라이언트에 전송 되는 메시지 수가 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-214">There will not be a visible difference in the browser from the previous section, but the number of messages that get sent to the client will be throttled.</span></span>

    ![응용 프로그램 창](tutorial-high-frequency-realtime-with-signalr/_static/image6.png)

<a id="animation"></a>

## <a name="add-smooth-animation-on-the-client"></a><span data-ttu-id="9ae99-216">클라이언트에서 부드러운 애니메이션 추가</span><span class="sxs-lookup"><span data-stu-id="9ae99-216">Add smooth animation on the client</span></span>

<span data-ttu-id="9ae99-217">응용 프로그램은 거의 완전 하지만 서버 메시지에 대 한 응답으로 이동 하는 클라이언트의 셰이프 동작에서 더 많은 개선을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-217">The application is almost complete, but we could make one more improvement, in the motion of the shape on the client as it is moved in response to server messages.</span></span> <span data-ttu-id="9ae99-218">셰이프 위치를 서버에서 제공 하는 새 위치로 설정 하는 대신 JQuery UI 라이브러리의 `animate` 함수를 사용 하 여 현재 위치와 새 위치 간에 셰이프를 부드럽게 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-218">Rather than setting the position of the shape to the new location given by the server, we'll use the JQuery UI library's `animate` function to move the shape smoothly between its current and new position.</span></span>

1. <span data-ttu-id="9ae99-219">아래 강조 표시 된 코드 처럼 보이도록 클라이언트의 `updateShape` 메서드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-219">Update the client's `updateShape` method to look like the highlighted code below:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample10.html?highlight=35-42)]

    <span data-ttu-id="9ae99-220">위의 코드는 애니메이션 간격 (이 경우 100 밀리초) 동안 서버에서 제공 하는 새 위치에서 이전 위치까지 셰이프를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-220">The above code moves the shape from the old location to the new one given by the server over the course of the animation interval (in this case, 100 milliseconds).</span></span> <span data-ttu-id="9ae99-221">셰이프를 실행 하는 모든 이전 애니메이션은 새 애니메이션이 시작 되기 전에 지워집니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-221">Any previous animation running on the shape is cleared before the new animation starts.</span></span>
2. <span data-ttu-id="9ae99-222">F5 키를 눌러 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-222">Start the application by pressing F5.</span></span> <span data-ttu-id="9ae99-223">페이지의 URL을 복사 하 여 두 번째 브라우저 창에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-223">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="9ae99-224">셰이프를 브라우저 창 중 하나로 끌어 옵니다. 다른 브라우저 창의 셰이프는 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-224">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span> <span data-ttu-id="9ae99-225">들어오는 메시지 마다 한 번만 설정 하는 것이 아니라 시간이 지남에 따라 이동이 보간된 경우 다른 창에서 셰이프의 이동이 jerky 더 작은 수준으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-225">The movement of the shape in the other window should appear less jerky as its movement is interpolated over time rather than being set once per incoming message.</span></span>

    ![응용 프로그램 창](tutorial-high-frequency-realtime-with-signalr/_static/image7.png)

<a id="furthersteps"></a>

## <a name="further-steps"></a><span data-ttu-id="9ae99-227">추가 단계</span><span class="sxs-lookup"><span data-stu-id="9ae99-227">Further Steps</span></span>

<span data-ttu-id="9ae99-228">이 자습서에서는 클라이언트와 서버 간에 높은 빈도의 메시지를 전송 하는 SignalR 응용 프로그램을 프로그래밍 하는 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-228">In this tutorial, you've learned how to program a SignalR application that sends high-frequency messages between clients and servers.</span></span> <span data-ttu-id="9ae99-229">이 통신 패러다임은 [SignalR를 사용 하 여 만든 ShootR 게임과](http://shootr.signalr.net)같이 온라인 게임 및 기타 시뮬레이션을 개발 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-229">This communication paradigm is useful for developing online games and other simulations, such as [the ShootR game created with SignalR](http://shootr.signalr.net).</span></span>

<span data-ttu-id="9ae99-230">이 자습서에서 만든 전체 응용 프로그램은 [코드 갤러리](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae99-230">The complete application created in this tutorial can be downloaded from [Code Gallery](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6).</span></span>

<span data-ttu-id="9ae99-231">SignalR 개발 개념에 대해 자세히 알아보려면 SignalR 원본 코드 및 리소스에 대 한 다음 사이트를 방문 하세요.</span><span class="sxs-lookup"><span data-stu-id="9ae99-231">To learn more about SignalR development concepts, visit the following sites for SignalR source code and resources:</span></span>

- [<span data-ttu-id="9ae99-232">SignalR 프로젝트</span><span class="sxs-lookup"><span data-stu-id="9ae99-232">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="9ae99-233">SignalR Github 및 샘플</span><span class="sxs-lookup"><span data-stu-id="9ae99-233">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="9ae99-234">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="9ae99-234">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
