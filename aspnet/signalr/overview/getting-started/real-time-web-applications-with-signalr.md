---
uid: signalr/overview/getting-started/real-time-web-applications-with-signalr
title: '실습: SignalR를 사용 하는 실시간 웹 응용 프로그램 | Microsoft Docs'
author: bradygaster
description: 실시간 웹 응용 프로그램은 실시간으로 연결 된 클라이언트에 서버 쪽 콘텐츠를 푸시하는 기능을 제공 합니다. ASP.NET 개발자의 경우 ASP ....
ms.author: bradyg
ms.date: 07/16/2014
ms.assetid: ba07958c-42e1-4da0-81db-ba6925ed6db0
msc.legacyurl: /signalr/overview/getting-started/real-time-web-applications-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 9e39fd3f2fc9d4e791002450085215096c222fcd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431669"
---
# <a name="hands-on-lab-real-time-web-applications-with-signalr"></a><span data-ttu-id="cb067-104">실습: SignalR를 사용 하는 실시간 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="cb067-104">Hands On Lab: Real-Time Web Applications with SignalR</span></span>

<span data-ttu-id="cb067-105">[웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="cb067-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

[<span data-ttu-id="cb067-106">웹 캠프 교육 키트, 2015 년 10 월 릴리스 다운로드</span><span class="sxs-lookup"><span data-stu-id="cb067-106">Download Web Camps Training Kit, October 2015 Release</span></span>](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b)

> <span data-ttu-id="cb067-107">실시간 웹 응용 프로그램은 실시간으로 연결 된 클라이언트에 서버 쪽 콘텐츠를 푸시하는 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-107">Real-time Web applications feature the ability to push server-side content to the connected clients as it happens, in real-time.</span></span> <span data-ttu-id="cb067-108">ASP.NET 개발자의 경우 **ASP.NET SignalR** 는 응용 프로그램에 실시간 웹 기능을 추가 하는 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-108">For ASP.NET developers, **ASP.NET SignalR** is a library to add real-time web functionality to their applications.</span></span> <span data-ttu-id="cb067-109">클라이언트와 서버에서 사용할 수 있는 가장 적합 한 전송에 대해 자동으로 가장 적합 한 전송을 선택 하는 여러 전송을 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-109">It takes advantage of several transports, automatically selecting the best available transport given the client and server's best available transport.</span></span> <span data-ttu-id="cb067-110">이는 브라우저와 서버 간의 양방향 통신을 가능 하 게 하는 HTML5 API 인 **WebSocket**을 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-110">It takes advantage of **WebSocket**, an HTML5 API that enables bi-directional communication between the browser and server.</span></span>
> 
> <span data-ttu-id="cb067-111">또한 **SignalR** 는 ASP.NET 응용 프로그램에서 서버와 클라이언트 간 RPC를 수행 하 고, 클라이언트 브라우저에서 서버 쪽 .net 코드에서 JavaScript 함수를 호출 하 고, 연결/연결 끊기 이벤트, 그룹 연결, 권한 부여 등의 연결 관리에 대 한 유용한 후크를 추가 하는 간단한 고급 API를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-111">**SignalR** also provides a simple, high-level API for doing server to client RPC (call JavaScript functions in your clients' browsers from server-side .NET code) in your ASP.NET application, as well as adding useful hooks for connection management, such as connect/disconnect events, grouping connections, and authorization.</span></span>
> 
> <span data-ttu-id="cb067-112">**SignalR** 는 클라이언트와 서버 간의 실시간 작업을 수행 하는 데 필요한 일부 전송에 대 한 추상화입니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-112">**SignalR** is an abstraction over some of the transports that are required to do real-time work between client and server.</span></span> <span data-ttu-id="cb067-113">**SignalR** 연결은 HTTP로 시작 되 고 사용 가능한 경우 **WebSocket** 연결로 승격 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-113">A **SignalR** connection starts as HTTP, and is then promoted to a **WebSocket** connection if available.</span></span> <span data-ttu-id="cb067-114">**Websocket** 은 서버 메모리를 가장 효율적으로 사용 하 고, 대기 시간을 최소화 하며, 가장 엄격한 요구 사항이 있습니다 (예: 클라이언트와 서버 간의 전이중 통신). 또한 **websocket** 은 서버에서 **windows server 2012** 또는 **windows 8**을 사용 하 여 서버를 **.NET Framework 4.5**과 함께 사용 해야 하기 때문에 **SignalR**에 이상적인 전송입니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-114">**WebSocket** is the ideal transport for **SignalR**, since it makes the most efficient use of server memory, has the lowest latency, and has the most underlying features (such as full duplex communication between client and server), but it also has the most stringent requirements: **WebSocket** requires the server to be using **Windows Server 2012** or **Windows 8**, along with **.NET Framework 4.5**.</span></span> <span data-ttu-id="cb067-115">이러한 요구 사항이 충족 되지 않는 경우 **SignalR** 는 다른 전송을 사용 하 여 연결을 설정 하려고 합니다 (예: *Ajax 긴 폴링*).</span><span class="sxs-lookup"><span data-stu-id="cb067-115">If these requirements are not met, **SignalR** will attempt to use other transports to make its connections (like *Ajax long polling*).</span></span>
> 
> <span data-ttu-id="cb067-116">**SignalR** API에는 클라이언트와 서버 간 통신을 위한 두 가지 모델 ( **영구 연결** 및 **허브**)이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-116">The **SignalR** API contains two models for communicating between clients and servers: **Persistent Connections** and **Hubs**.</span></span> <span data-ttu-id="cb067-117">**연결은** 단일 받는 사람, 그룹화 또는 브로드캐스트 메시지를 보내기 위한 간단한 끝점을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-117">A **Connection** represents a simple endpoint for sending single-recipient, grouped, or broadcast messages.</span></span> <span data-ttu-id="cb067-118">**허브** 는 클라이언트와 서버에서 직접 메서드를 호출할 수 있도록 하는 연결 API를 기반으로 하는 더 높은 수준의 파이프라인입니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-118">A **Hub** is a more high-level pipeline built upon the Connection API that allows your client and server to call methods on each other directly.</span></span>
> 
> ![SignalR 아키텍처](real-time-web-applications-with-signalr/_static/image1.png)
> 
> <span data-ttu-id="cb067-120">모든 샘플 코드와 코드 조각은 [https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b)에서 사용할 수 있는 웹 캠프 교육 키트, 10 월 2015 릴리스에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-120">All sample code and snippets are included in the Web Camps Training Kit, October 2015 Release, available at [https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b).</span></span>  <span data-ttu-id="cb067-121">해당 페이지의 설치 관리자 링크는 더 이상 작동 하지 않습니다. 대신 자산 섹션 아래에 있는 링크 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-121">Please note that the Installer link on that page no longer works; use one of the links under the Assets section instead.</span></span>

<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="cb067-122">개요</span><span class="sxs-lookup"><span data-stu-id="cb067-122">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="cb067-123">목표</span><span class="sxs-lookup"><span data-stu-id="cb067-123">Objectives</span></span>

<span data-ttu-id="cb067-124">이 실습 랩에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-124">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="cb067-125">SignalR를 사용 하 여 서버에서 클라이언트로 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-125">Send notifications from server to client using SignalR.</span></span>
- <span data-ttu-id="cb067-126">**SQL Server**를 사용 하 여 SignalR 응용 프로그램을 Scale Out 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-126">Scale Out your SignalR application using **SQL Server**.</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="cb067-127">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="cb067-127">Prerequisites</span></span>

<span data-ttu-id="cb067-128">이 실습 실습을 완료 하려면 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-128">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="cb067-129">[웹 이상의 Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)</span><span class="sxs-lookup"><span data-stu-id="cb067-129">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="cb067-130">설치 프로그램</span><span class="sxs-lookup"><span data-stu-id="cb067-130">Setup</span></span>

<span data-ttu-id="cb067-131">이 실습 랩에서 연습을 실행 하려면 먼저 환경을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-131">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="cb067-132">Windows 탐색기 창을 열고 랩의 **원본** 폴더로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-132">Open a Windows Explorer window and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="cb067-133">**Setup.exe** 를 마우스 오른쪽 단추로 클릭 하 고 **관리자 권한으로 실행** 을 선택 하 여 환경을 구성 하는 설치 프로세스를 시작 하 고이 랩에 대 한 Visual Studio 코드 조각을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-133">Right-click **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="cb067-134">사용자 계정 컨트롤 대화 상자가 표시 되 면 계속 하려면 작업을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-134">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="cb067-135">설치 프로그램을 실행 하기 전에이 랩에 대 한 모든 종속성을 확인 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-135">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="cb067-136">코드 조각 사용</span><span class="sxs-lookup"><span data-stu-id="cb067-136">Using the Code Snippets</span></span>

<span data-ttu-id="cb067-137">랩 문서 전체에서 코드 블록을 삽입 하 라는 지침이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-137">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="cb067-138">사용자 편의를 위해이 코드의 대부분은 Visual Studio 2013 내에서 액세스할 수 있는 Visual Studio Code 코드 조각으로 제공 되며,이를 수동으로 추가 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-138">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="cb067-139">각 연습에는 각 연습을 서로 독립적으로 수행할 수 있는 연습 **시작** 폴더에 있는 시작 솔루션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-139">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="cb067-140">연습 중에 추가 된 코드 조각은 이러한 시작 솔루션에서 누락 되었으며, 연습을 완료할 때까지 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-140">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="cb067-141">연습에 대 한 소스 코드 내에서 해당 연습의 단계를 완료 하 여 생성 된 코드를 포함 하는 Visual Studio 솔루션을 포함 하는 **끝** 폴더를 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-141">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="cb067-142">이 실습 랩을 통해 작업할 때 추가 도움이 필요한 경우 이러한 솔루션을 지침으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-142">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="cb067-143">실습</span><span class="sxs-lookup"><span data-stu-id="cb067-143">Exercises</span></span>

<span data-ttu-id="cb067-144">이 실습 랩에는 다음 연습이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-144">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="cb067-145">SignalR를 사용 하 여 실시간 데이터 작업</span><span class="sxs-lookup"><span data-stu-id="cb067-145">Working with Real-Time Data Using SignalR</span></span>](#Exercise1)
2. [<span data-ttu-id="cb067-146">SQL Server를 사용 하 여 확장</span><span class="sxs-lookup"><span data-stu-id="cb067-146">Scaling Out Using SQL Server</span></span>](#Exercise2)

<span data-ttu-id="cb067-147">이 랩을 완료 하는 데 소요 되는 예상 시간: **60 분**</span><span class="sxs-lookup"><span data-stu-id="cb067-147">Estimated time to complete this lab: **60 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="cb067-148">Visual Studio를 처음 시작 하는 경우 미리 정의 된 설정 컬렉션 중 하나를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-148">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="cb067-149">미리 정의 된 각 컬렉션은 특정 개발 스타일에 맞게 디자인 되 고 창 레이아웃, 편집기 동작, IntelliSense 코드 조각 및 대화 상자 옵션을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-149">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="cb067-150">이 실습의 절차에서는 **일반 개발 설정** 컬렉션을 사용 하는 경우 Visual Studio에서 지정 된 작업을 수행 하는 데 필요한 작업을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-150">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="cb067-151">개발 환경에 대해 다른 설정 컬렉션을 선택 하는 경우 고려해 야 하는 단계에 차이가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-151">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>

<a id="Exercise1"></a>
### <a name="exercise-1-working-with-real-time-data-using-signalr"></a><span data-ttu-id="cb067-152">연습 1: SignalR를 사용 하 여 실시간 데이터 작업</span><span class="sxs-lookup"><span data-stu-id="cb067-152">Exercise 1: Working with Real-Time Data Using SignalR</span></span>

<span data-ttu-id="cb067-153">채팅은 종종 예로 사용 되지만 실시간 웹 기능을 사용 하면 훨씬 더 많은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-153">While chat is often used as an example, you can do a whole lot more with real-time Web functionality.</span></span> <span data-ttu-id="cb067-154">사용자가 새 데이터를 볼 수 있도록 웹 페이지를 새로 고치거 나 페이지가 Ajax 긴 폴링을 구현 하 여 새 데이터를 검색 하는 경우에는 SignalR을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-154">Any time a user refreshes a web page to see new data or the page implements Ajax long polling to retrieve new data, you can use SignalR.</span></span>

<span data-ttu-id="cb067-155">SignalR는 **서버 푸시** 또는 **브로드캐스팅** 기능을 지원 합니다. 연결 관리를 자동으로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-155">SignalR supports **server push** or **broadcasting** functionality; it handles connection management automatically.</span></span> <span data-ttu-id="cb067-156">클라이언트-서버 통신을 위한 클래식 HTTP 연결에서 각 요청에 대 한 연결이 다시 설정 되지만 SignalR는 클라이언트와 서버 간에 영구 연결을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-156">In classic HTTP connections for client-server communication, connection is re-established for each request, but SignalR provides persistent connection between the client and server.</span></span> <span data-ttu-id="cb067-157">SignalR에서 서버 코드는 현재 알고 있는 요청-응답 모델이 아니라 RPC (원격 프로시저 호출)를 사용 하 여 브라우저에서 클라이언트 코드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-157">In SignalR the server code calls out to a client code in the browser using Remote Procedure Calls (RPC), rather than the request-response model we know today.</span></span>

<span data-ttu-id="cb067-158">이 연습에서는 **Geek of 퀴즈** 응용 프로그램이 SignalR를 사용 하 여 전체 페이지를 새로 고치지 않고도 업데이트 된 메트릭을 사용 하 여 통계 대시보드를 표시 하도록 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-158">In this exercise, you will configure the **Geek Quiz** application to use SignalR to display the Statistics dashboard with the updated metrics without the need to refresh the entire page.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--exploring-the-geek-quiz-statistics-page"></a><span data-ttu-id="cb067-159">작업 1 – Geek of 퀴즈 통계 페이지 탐색</span><span class="sxs-lookup"><span data-stu-id="cb067-159">Task 1 – Exploring the Geek Quiz Statistics Page</span></span>

<span data-ttu-id="cb067-160">이 작업에서는 응용 프로그램을 살펴보고 통계 페이지가 표시 되는 방식과 정보가 업데이트 되는 방식을 개선 하는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-160">In this task, you will go through the application and verify how the statistics page is shown and how you can improve the way the information is updated.</span></span>

1. <span data-ttu-id="cb067-161">**웹에 대해 Visual Studio Express 2013** 을 열고 **Source\Ex1-WorkingWithRealTimeData\Begin** 폴더에 있는 **GeekQuiz** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-161">Open **Visual Studio Express 2013 for Web** and open the **GeekQuiz.sln** solution located in the **Source\Ex1-WorkingWithRealTimeData\Begin** folder.</span></span>
2. <span data-ttu-id="cb067-162">**F5** 키를 눌러 솔루션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-162">Press **F5** to run the solution.</span></span> <span data-ttu-id="cb067-163">**로그인** 페이지가 브라우저에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-163">The **Log in** page should appear in the browser.</span></span>

    <span data-ttu-id="cb067-164">![솔루션 실행](real-time-web-applications-with-signalr/_static/image2.png "솔루션 실행")</span><span class="sxs-lookup"><span data-stu-id="cb067-164">![Running the solution](real-time-web-applications-with-signalr/_static/image2.png "Running the solution")</span></span>

    <span data-ttu-id="cb067-165">*솔루션 실행*</span><span class="sxs-lookup"><span data-stu-id="cb067-165">*Running the solution*</span></span>
3. <span data-ttu-id="cb067-166">페이지의 오른쪽 위 모퉁이에 있는 **등록** 을 클릭 하 여 응용 프로그램에서 새 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-166">Click **Register** in the upper-right corner of the page to create a new user in the application.</span></span>

    <span data-ttu-id="cb067-167">![링크 등록](real-time-web-applications-with-signalr/_static/image3.png "링크 등록")</span><span class="sxs-lookup"><span data-stu-id="cb067-167">![Register link](real-time-web-applications-with-signalr/_static/image3.png "Register link")</span></span>

    <span data-ttu-id="cb067-168">*링크 등록*</span><span class="sxs-lookup"><span data-stu-id="cb067-168">*Register link*</span></span>
4. <span data-ttu-id="cb067-169">**등록** 페이지에서 **사용자 이름** 및 **암호**를 입력 한 다음 **등록**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-169">In the **Register** page, enter a **User name** and **Password**, and then click **Register**.</span></span>

    <span data-ttu-id="cb067-170">![사용자 등록](real-time-web-applications-with-signalr/_static/image4.png "사용자 등록")</span><span class="sxs-lookup"><span data-stu-id="cb067-170">![Registering a user](real-time-web-applications-with-signalr/_static/image4.png "Registering a user")</span></span>

    <span data-ttu-id="cb067-171">*사용자 등록*</span><span class="sxs-lookup"><span data-stu-id="cb067-171">*Registering a user*</span></span>
5. <span data-ttu-id="cb067-172">응용 프로그램이 새 계정을 등록 하 고 사용자가 인증 되 고 첫 번째 퀴즈 질문을 표시 하는 홈 페이지로 다시 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-172">The application registers the new account and the user is authenticated and redirected back to the home page showing the first quiz question.</span></span>
6. <span data-ttu-id="cb067-173">새 창에서 **통계** 페이지를 열고 **홈** 페이지와 **통계** 페이지를 나란히 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-173">Open the **Statistics** page in a new window and put the **Home** page and **Statistics** page side-by-side.</span></span>

    <span data-ttu-id="cb067-174">![Side-by-side 창](real-time-web-applications-with-signalr/_static/image5.png "Side-by-side 창")</span><span class="sxs-lookup"><span data-stu-id="cb067-174">![Side-by-side windows](real-time-web-applications-with-signalr/_static/image5.png "Side by side windows")</span></span>

    <span data-ttu-id="cb067-175">*Side-by-side 창*</span><span class="sxs-lookup"><span data-stu-id="cb067-175">*Side-by-side windows*</span></span>
7. <span data-ttu-id="cb067-176">**홈** 페이지에서 옵션 중 하나를 클릭 하 여 질문에 대답 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-176">In the **Home** page, answer the question by clicking one of the options.</span></span>

    <span data-ttu-id="cb067-177">![질문에 답변](real-time-web-applications-with-signalr/_static/image6.png "질문에 답변")</span><span class="sxs-lookup"><span data-stu-id="cb067-177">![Answering a question](real-time-web-applications-with-signalr/_static/image6.png "Answering a question")</span></span>

    <span data-ttu-id="cb067-178">*질문에 답변*</span><span class="sxs-lookup"><span data-stu-id="cb067-178">*Answering a question*</span></span>
8. <span data-ttu-id="cb067-179">단추 중 하나를 클릭 하면 대답이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-179">After clicking one of the buttons, the answer should appear.</span></span>

    <span data-ttu-id="cb067-180">![질문에 대 한 답변이 올바릅니다.](real-time-web-applications-with-signalr/_static/image7.png "질문에 대 한 답변이 올바릅니다.")</span><span class="sxs-lookup"><span data-stu-id="cb067-180">![Question answered correct](real-time-web-applications-with-signalr/_static/image7.png "Question answered correct")</span></span>

    <span data-ttu-id="cb067-181">*질문에 대 한 대답이 올바르게*</span><span class="sxs-lookup"><span data-stu-id="cb067-181">*Question answered correctly*</span></span>
9. <span data-ttu-id="cb067-182">통계 페이지에 제공 된 정보는 오래 된 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-182">Notice that the information provided in the Statistics page is outdated.</span></span> <span data-ttu-id="cb067-183">업데이트 된 결과를 보려면 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-183">Refresh the page in order to see the updated results.</span></span>

    <span data-ttu-id="cb067-184">![통계 페이지](real-time-web-applications-with-signalr/_static/image8.png "통계 페이지")</span><span class="sxs-lookup"><span data-stu-id="cb067-184">![Statistics page](real-time-web-applications-with-signalr/_static/image8.png "Statistics page")</span></span>

    <span data-ttu-id="cb067-185">*통계 페이지*</span><span class="sxs-lookup"><span data-stu-id="cb067-185">*Statistics page*</span></span>
10. <span data-ttu-id="cb067-186">Visual Studio로 돌아가서 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-186">Go back to Visual Studio and stop debugging.</span></span>

<a id="Ex1Task2"></a>
#### <a name="task-2--adding-signalr-to-geek-quiz-to-show-online-charts"></a><span data-ttu-id="cb067-187">작업 2 – Geek of 퀴즈에 SignalR를 추가 하 여 온라인 차트 표시</span><span class="sxs-lookup"><span data-stu-id="cb067-187">Task 2 – Adding SignalR to Geek Quiz to Show Online Charts</span></span>

<span data-ttu-id="cb067-188">이 작업에서는 SignalR를 솔루션에 추가 하 고 새 대답이 서버에 전송 될 때 자동으로 클라이언트에 업데이트를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-188">In this task, you will add SignalR to the solution and send updates to the clients automatically when a new answer is sent to the server.</span></span>

1. <span data-ttu-id="cb067-189">Visual Studio의 **도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-189">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="cb067-190">**패키지 관리자 콘솔** 창에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-190">In the **Package Manager Console** window, execute the following command:</span></span>

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample1.ps1)]

    <span data-ttu-id="cb067-191">![SignalR 패키지 설치](real-time-web-applications-with-signalr/_static/image9.png "SignalR 패키지 설치")</span><span class="sxs-lookup"><span data-stu-id="cb067-191">![SignalR package installation](real-time-web-applications-with-signalr/_static/image9.png "SignalR package installation")</span></span>

    <span data-ttu-id="cb067-192">*SignalR 패키지 설치*</span><span class="sxs-lookup"><span data-stu-id="cb067-192">*SignalR package installation*</span></span>

   > [!NOTE]
   > <span data-ttu-id="cb067-193">새 MVC 5 응용 프로그램에서 **SignalR** NuGet 패키지 버전 2.0.2을 설치 하는 경우 SignalR를 설치 하기 전에 **OWIN** 패키지를 버전 2.0.1 이상으로 수동으로 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-193">When installing **SignalR** NuGet packages version 2.0.2 from a brand new MVC 5 application, you will need to manually update **OWIN** packages to version 2.0.1 (or higher) before installing SignalR.</span></span> <span data-ttu-id="cb067-194">이렇게 하려면 **패키지 관리자 콘솔**에서 다음 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-194">To do this, you can execute the following script in the **Package Manager Console**:</span></span>
   > 
   > [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample2.ps1)]
   > 
   > <span data-ttu-id="cb067-195">SignalR의 이후 릴리스에서는 OWIN 종속성이 자동으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-195">In a future release of SignalR, OWIN dependencies will be automatically updated.</span></span>
3. <span data-ttu-id="cb067-196">**솔루션 탐색기**에서 **Scripts** 폴더를 확장 하 고 SignalR *js* 파일이 솔루션에 추가 되었음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-196">In **Solution Explorer**, expand the **Scripts** folder and notice that the SignalR *js* files were added to the solution.</span></span>

    <span data-ttu-id="cb067-197">![SignalR JavaScript 참조](real-time-web-applications-with-signalr/_static/image10.png "SignalR JavaScript 참조")</span><span class="sxs-lookup"><span data-stu-id="cb067-197">![SignalR JavaScript references](real-time-web-applications-with-signalr/_static/image10.png "SignalR JavaScript references")</span></span>

    <span data-ttu-id="cb067-198">*SignalR JavaScript 참조*</span><span class="sxs-lookup"><span data-stu-id="cb067-198">*SignalR JavaScript references*</span></span>
4. <span data-ttu-id="cb067-199">**솔루션 탐색기**에서 GeekQuiz 프로젝트를 마우스 오른쪽 단추로 클릭 하 | **새 폴더** **추가** 를 선택 하 고 이름을 **Hubs**로 .</span><span class="sxs-lookup"><span data-stu-id="cb067-199">In **Solution Explorer**, right-click the **GeekQuiz** project, select **Add** | **New Folder**, and name it **Hubs**.</span></span>
5. <span data-ttu-id="cb067-200">**허브** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 새 항목**입니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-200">Right-click the **Hubs** folder and select **Add | New Item**.</span></span>

    <span data-ttu-id="cb067-201">![새 항목 추가](real-time-web-applications-with-signalr/_static/image11.png "새 항목 추가")</span><span class="sxs-lookup"><span data-stu-id="cb067-201">![Add new item](real-time-web-applications-with-signalr/_static/image11.png "Add new item")</span></span>

    <span data-ttu-id="cb067-202">*새 항목 추가*</span><span class="sxs-lookup"><span data-stu-id="cb067-202">*Add new item*</span></span>
6. <span data-ttu-id="cb067-203">**새 항목 추가** 대화 상자에서 **C# 시각적 개체 | 웹 |** 왼쪽 창의 SignalR 노드 가운데 창에서 **SignalR Hub 클래스 (v2)** 를 선택 하 고 파일 이름을 **StatisticsHub.cs** 로 선택한 후에 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-203">In the **Add New Item** dialog box, select the **Visual C# | Web | SignalR** node in the left pane, select **SignalR Hub Class (v2)** from the center pane, name the file **StatisticsHub.cs** and click **Add**.</span></span>

    <span data-ttu-id="cb067-204">![새 항목 추가 대화 상자](real-time-web-applications-with-signalr/_static/image12.png "새 항목 추가 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="cb067-204">![Add new item dialog box](real-time-web-applications-with-signalr/_static/image12.png "Add new item dialog box")</span></span>

    <span data-ttu-id="cb067-205">*새 항목 추가 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="cb067-205">*Add new item dialog box*</span></span>
7. <span data-ttu-id="cb067-206">**StatisticsHub** 클래스의 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-206">Replace the code in the **StatisticsHub** class with the following code.</span></span>

    <span data-ttu-id="cb067-207">(코드 조각- *RealTimeSignalR-Ex1-StatisticsHubClass*)</span><span class="sxs-lookup"><span data-stu-id="cb067-207">(Code Snippet - *RealTimeSignalR - Ex1 - StatisticsHubClass*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample3.cs)]
8. <span data-ttu-id="cb067-208">**Startup.cs** 를 열고 **구성** 방법의 끝에 다음 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-208">Open **Startup.cs** and add the following line at the end of the **Configuration** method.</span></span>

    <span data-ttu-id="cb067-209">(코드 조각- *RealTimeSignalR-Ex1-MapSignalR*)</span><span class="sxs-lookup"><span data-stu-id="cb067-209">(Code Snippet - *RealTimeSignalR - Ex1 - MapSignalR*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample4.cs)]
9. <span data-ttu-id="cb067-210">**Services** 폴더 내에서 **StatisticsService.cs** 페이지를 열고 다음 using 지시문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-210">Open the **StatisticsService.cs** page inside the **Services** folder and add the following using directives.</span></span>

    <span data-ttu-id="cb067-211">(코드 조각- *RealTimeSignalR-Ex1-UsingDirectives*)</span><span class="sxs-lookup"><span data-stu-id="cb067-211">(Code Snippet - *RealTimeSignalR - Ex1 - UsingDirectives*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample5.cs)]
10. <span data-ttu-id="cb067-212">연결 된 클라이언트에 업데이트를 알리려면 먼저 현재 연결에 대 한 **컨텍스트** 개체를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-212">To notify connected clients of updates, you first retrieve a **Context** object for the current connection.</span></span> <span data-ttu-id="cb067-213">**허브** 개체는 단일 클라이언트에 메시지를 보내거나 연결 된 모든 클라이언트에 브로드캐스트하는 메서드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-213">The **Hub** object contains methods to send messages to a single client or broadcast to all connected clients.</span></span> <span data-ttu-id="cb067-214">**StatisticsService** 클래스에 다음 메서드를 추가 하 여 통계 데이터를 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-214">Add the following method to the **StatisticsService** class to broadcast the statistics data.</span></span>

    <span data-ttu-id="cb067-215">(코드 조각- *RealTimeSignalR-Ex1-NotifyUpdatesMethod*)</span><span class="sxs-lookup"><span data-stu-id="cb067-215">(Code Snippet - *RealTimeSignalR - Ex1 - NotifyUpdatesMethod*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample6.cs)]

    > [!NOTE]
    > <span data-ttu-id="cb067-216">위의 코드에서는 임의의 메서드 이름을 사용 하 여 클라이언트 (예: *updateStatistics*)에서 함수를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-216">In the code above, you are using an arbitrary method name to call a function on the client (i.e.: *updateStatistics*).</span></span> <span data-ttu-id="cb067-217">지정 하는 메서드 이름은 동적 개체로 해석 됩니다. 즉, IntelliSense 또는 컴파일 타임 유효성 검사를 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-217">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="cb067-218">식은 런타임에 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-218">The expression is evaluated at run time.</span></span> <span data-ttu-id="cb067-219">메서드 호출이 실행 되 면 SignalR는 메서드 이름 및 매개 변수 값을 클라이언트에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-219">When the method call executes, SignalR sends the method name and the parameter values to the client.</span></span> <span data-ttu-id="cb067-220">클라이언트에 이름과 일치 하는 메서드가 있으면 해당 메서드가 호출 되 고 매개 변수 값이이 메서드에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-220">If the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="cb067-221">클라이언트에서 일치 하는 메서드를 찾을 수 없는 경우 오류가 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-221">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="cb067-222">자세한 내용은 [ASP.NET SignalR HUBS API 가이드](../guide-to-the-api/hubs-api-guide-server.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="cb067-222">For more information, refer to [ASP.NET SignalR Hubs API Guide](../guide-to-the-api/hubs-api-guide-server.md).</span></span>
11. <span data-ttu-id="cb067-223">**Controllers** 폴더 내에서 **TriviaController.cs** 페이지를 열고 다음 using 지시문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-223">Open the **TriviaController.cs** page inside the **Controllers** folder and add the following using directives.</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample7.cs)]
12. <span data-ttu-id="cb067-224">**사후** 작업 메서드에 다음 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-224">Add the following highlighted code to the **Post** action method.</span></span>

    <span data-ttu-id="cb067-225">(코드 조각- *RealTimeSignalR-Ex1-NotifyUpdatesCall*)</span><span class="sxs-lookup"><span data-stu-id="cb067-225">(Code Snippet - *RealTimeSignalR - Ex1 - NotifyUpdatesCall*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample8.cs)]
13. <span data-ttu-id="cb067-226">뷰 내에서 **통계. cshtml** 페이지를 엽니다. **| 홈** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-226">Open the **Statistics.cshtml** page inside the **Views | Home** folder.</span></span> <span data-ttu-id="cb067-227">**스크립트** 섹션을 찾고 섹션의 시작 부분에 다음 스크립트 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-227">Locate the **Scripts** section and add the following script references at the beginning of the section.</span></span>

    <span data-ttu-id="cb067-228">(코드 조각- *RealTimeSignalR-Ex1-SignalRScriptReferences*)</span><span class="sxs-lookup"><span data-stu-id="cb067-228">(Code Snippet - *RealTimeSignalR - Ex1 - SignalRScriptReferences*)</span></span>

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample9.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="cb067-229">SignalR 및 기타 스크립트 라이브러리를 Visual Studio 프로젝트에 추가 하면 패키지 관리자가이 항목에 표시 된 버전 보다 최신 버전인 SignalR 스크립트 파일을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-229">When you add SignalR and other script libraries to your Visual Studio project, the Package Manager might install a version of the SignalR script file that is more recent than the version shown in this topic.</span></span> <span data-ttu-id="cb067-230">코드의 스크립트 참조가 프로젝트에 설치 된 스크립트 라이브러리 버전과 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-230">Make sure that the script reference in your code matches the version of the script library installed in your project.</span></span>
14. <span data-ttu-id="cb067-231">다음 강조 표시 된 코드를 추가 하 여 클라이언트를 SignalR hub에 연결 하 고 허브에서 새 메시지가 수신 되 면 통계 데이터를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-231">Add the following highlighted code to connect the client to the SignalR hub and update the statistics data when a new message is received from the hub.</span></span>

    <span data-ttu-id="cb067-232">(코드 조각- *RealTimeSignalR-Ex1-SignalRClientCode*)</span><span class="sxs-lookup"><span data-stu-id="cb067-232">(Code Snippet - *RealTimeSignalR - Ex1 - SignalRClientCode*)</span></span>

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample10.cshtml)]

    <span data-ttu-id="cb067-233">이 코드에서는 허브 프록시를 만들고 서버에서 보낸 메시지를 수신 하기 위해 이벤트 처리기를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-233">In this code, you are creating a Hub Proxy and registering an event handler to listen for messages sent by the server.</span></span> <span data-ttu-id="cb067-234">이 경우 *updateStatistics* 메서드를 통해 전송 되는 메시지를 수신 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-234">In this case, you listen for messages sent through the *updateStatistics* method.</span></span>

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a><span data-ttu-id="cb067-235">작업 3 – 솔루션 실행</span><span class="sxs-lookup"><span data-stu-id="cb067-235">Task 3 – Running the Solution</span></span>

<span data-ttu-id="cb067-236">이 태스크에서는 솔루션을 실행 하 여 새 질문에 답변 한 후 SignalR를 사용 하 여 통계 보기가 자동으로 업데이트 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-236">In this task, you will run the solution to verify that the statistics view is updated automatically using SignalR after answering a new question.</span></span>

1. <span data-ttu-id="cb067-237">**F5** 키를 눌러 솔루션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-237">Press **F5** to run the solution.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cb067-238">응용 프로그램에 아직 로그인 하지 않은 경우 작업 1에서 만든 사용자로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-238">If not already logged in to the application, log in with the user you created in Task 1.</span></span>
2. <span data-ttu-id="cb067-239">새 창에서 **통계** 페이지를 열고 작업 1에서와 같이 **홈** 페이지와 **통계** 페이지를 나란히 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-239">Open the **Statistics** page in a new window and put the **Home** page and **Statistics** page side-by-side as you did in Task 1.</span></span>
3. <span data-ttu-id="cb067-240">**홈** 페이지에서 옵션 중 하나를 클릭 하 여 질문에 대답 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-240">In the **Home** page, answer the question by clicking one of the options.</span></span>

    <span data-ttu-id="cb067-241">![다른 질문에 답변](real-time-web-applications-with-signalr/_static/image13.png "다른 질문에 답변")</span><span class="sxs-lookup"><span data-stu-id="cb067-241">![Answering another question](real-time-web-applications-with-signalr/_static/image13.png "Answering another question")</span></span>

    <span data-ttu-id="cb067-242">*다른 질문에 답변*</span><span class="sxs-lookup"><span data-stu-id="cb067-242">*Answering another question*</span></span>
4. <span data-ttu-id="cb067-243">단추 중 하나를 클릭 하면 대답이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-243">After clicking one of the buttons, the answer should appear.</span></span> <span data-ttu-id="cb067-244">페이지의 통계 정보는 전체 페이지를 새로 고칠 필요 없이 업데이트 된 정보를 사용 하 여 질문에 대답 한 후 자동으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-244">Notice that the Statistics information on the page is updated automatically after answering the question with the updated information without the need to refresh the entire page.</span></span>

    <span data-ttu-id="cb067-245">![응답 후 새로 고쳐진 통계 페이지](real-time-web-applications-with-signalr/_static/image14.png "응답 후 새로 고쳐진 통계 페이지")</span><span class="sxs-lookup"><span data-stu-id="cb067-245">![Statistics page refreshed after answer](real-time-web-applications-with-signalr/_static/image14.png "Statistics page refreshed after answer")</span></span>

    <span data-ttu-id="cb067-246">*응답 후 새로 고쳐진 통계 페이지*</span><span class="sxs-lookup"><span data-stu-id="cb067-246">*Statistics page refreshed after answer*</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-scaling-out-using-sql-server"></a><span data-ttu-id="cb067-247">연습 2: SQL Server을 사용 하 여 확장</span><span class="sxs-lookup"><span data-stu-id="cb067-247">Exercise 2: Scaling Out Using SQL Server</span></span>

<span data-ttu-id="cb067-248">웹 응용 프로그램의 크기를 조정 하는 경우 일반적으로 *수직 확장* 및 *수평 확장* 옵션 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-248">When scaling a web application, you can generally choose between *scaling up* and *scaling out* options.</span></span> <span data-ttu-id="cb067-249">수직 *확장* 은 더 많은 리소스 (CPU, RAM 등)가 있는 대규모 서버를 사용 하는 것을 의미 합니다 .이는 부하를 처리할 서버를 더 추가 하 *는 것입니다* .</span><span class="sxs-lookup"><span data-stu-id="cb067-249">*Scale up* means using a larger server, with more resources (CPU, RAM, etc.) while *scale out* means adding more servers to handle the load.</span></span> <span data-ttu-id="cb067-250">후자와 관련 하 여 발생 하는 문제는 클라이언트를 다른 서버로 라우팅할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-250">The problem with the latter is that the clients can get routed to different servers.</span></span> <span data-ttu-id="cb067-251">한 서버에 연결 된 클라이언트는 다른 서버에서 보낸 메시지를 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-251">A client that is connected to one server will not receive messages sent from another server.</span></span>

<span data-ttu-id="cb067-252">서버 간에 메시지를 전달 하기 위해 *후면판*이라는 구성 요소를 사용 하 여 이러한 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-252">You can solve these issues by using a component called *backplane*, to forward messages between servers.</span></span> <span data-ttu-id="cb067-253">후면판을 사용 하는 경우 각 응용 프로그램 인스턴스는 후면판으로 메시지를 보내고, 후면판은이를 다른 응용 프로그램 인스턴스로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-253">With a backplane enabled, each application instance sends messages to the backplane, and the backplane forwards them to the other application instances.</span></span>

<span data-ttu-id="cb067-254">SignalR에 대 한 백플레인을에는 현재 다음과 같은 세 가지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-254">There are currently three types of backplanes for SignalR:</span></span>

- <span data-ttu-id="cb067-255">**Windows Azure Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="cb067-255">**Windows Azure Service Bus**.</span></span> <span data-ttu-id="cb067-256">Service Bus는 구성 요소가 느슨하게 결합 된 메시지를 보낼 수 있도록 하는 메시징 인프라입니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-256">Service Bus is a messaging infrastructure that allows components to send loosely coupled messages.</span></span>
- <span data-ttu-id="cb067-257">**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="cb067-257">**SQL Server**.</span></span> <span data-ttu-id="cb067-258">SQL Server 후면판은 메시지를 SQL 테이블에 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-258">The SQL Server backplane writes messages to SQL tables.</span></span> <span data-ttu-id="cb067-259">후면판은 효율적인 메시징의 Service Broker를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-259">The backplane uses Service Broker for efficient messaging.</span></span> <span data-ttu-id="cb067-260">그러나 Service Broker를 사용 하도록 설정 하지 않은 경우에도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-260">However, it also works if Service Broker is not enabled.</span></span>
- <span data-ttu-id="cb067-261">**Redis**.</span><span class="sxs-lookup"><span data-stu-id="cb067-261">**Redis**.</span></span> <span data-ttu-id="cb067-262">Redis는 메모리 내 키-값 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-262">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="cb067-263">Redis는 메시지를 보내기 위한 게시/구독 ("pub/sub") 패턴을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-263">Redis supports a publish/subscribe ("pub/sub") pattern for sending messages.</span></span>

<span data-ttu-id="cb067-264">모든 메시지는 메시지 버스를 통해 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-264">Every message is sent through a message bus.</span></span> <span data-ttu-id="cb067-265">메시지 버스는 게시/구독 추상화를 제공 하는 [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) 인터페이스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-265">A message bus implements the [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) interface, which provides a publish/subscribe abstraction.</span></span> <span data-ttu-id="cb067-266">백플레인을는 기본 **IMessageBus** 를 해당 후면판 용으로 설계 된 버스로 바꿔 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-266">The backplanes work by replacing the default **IMessageBus** with a bus designed for that backplane.</span></span>

<span data-ttu-id="cb067-267">각 서버 인스턴스는 버스를 통해 후면판에 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-267">Each server instance connects to the backplane through the bus.</span></span> <span data-ttu-id="cb067-268">메시지가 전송 되 면 후면판으로 이동 하 여 후면판에서 모든 서버에 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-268">When a message is sent, it goes to the backplane, and the backplane sends it to every server.</span></span> <span data-ttu-id="cb067-269">서버는 후면판에서 메시지를 받으면 해당 메시지를 로컬 캐시에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-269">When a server receives a message from the backplane, it stores the message in its local cache.</span></span> <span data-ttu-id="cb067-270">그런 다음 서버는 로컬 캐시에서 클라이언트로 메시지를 배달 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-270">The server then delivers messages to clients from its local cache.</span></span>

<span data-ttu-id="cb067-271">SignalR 후면판의 작동 방식에 대 한 자세한 내용은이 [문서](../performance/scaleout-in-signalr.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="cb067-271">For more information about how the SignalR backplane works, read this [article](../performance/scaleout-in-signalr.md).</span></span>

> [!NOTE]
> <span data-ttu-id="cb067-272">후면판이 병목 상태가 될 수 있는 몇 가지 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-272">There are some scenarios where a backplane can become a bottleneck.</span></span> <span data-ttu-id="cb067-273">몇 가지 일반적인 SignalR 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-273">Here are some typical SignalR scenarios:</span></span>
> 
> - <span data-ttu-id="cb067-274">[서버 브로드캐스트](tutorial-server-broadcast-with-signalr.md) (예: 주식 종목): 백플레인을 서버에서 메시지를 보내는 속도를 제어 하므로이 시나리오에 대해 잘 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-274">[Server broadcast](tutorial-server-broadcast-with-signalr.md) (e.g., stock ticker): Backplanes work well for this scenario, because the server controls the rate at which messages are sent.</span></span>
> - <span data-ttu-id="cb067-275">[클라이언트-클라이언트](tutorial-getting-started-with-signalr.md) (예: 채팅):이 시나리오에서는 메시지 수가 클라이언트 수로 확장 되 면 후면판에서 병목 현상이 발생할 수 있습니다. 즉, 더 많은 클라이언트에 연결 될 때 메시지의 비율이 비례적으로 증가 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-275">[Client-to-client](tutorial-getting-started-with-signalr.md) (e.g., chat): In this scenario, the backplane might be a bottleneck if the number of messages scales with the number of clients; that is, if the rate of messages grows proportionally as more clients join.</span></span>
> - <span data-ttu-id="cb067-276">[높은 빈도 실시간](tutorial-high-frequency-realtime-with-signalr.md) (예: 실시간 게임):이 시나리오에는 후면판을 권장 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-276">[High-frequency realtime](tutorial-high-frequency-realtime-with-signalr.md) (e.g., real-time games): A backplane is not recommended for this scenario.</span></span>

<span data-ttu-id="cb067-277">이 연습에서는 **SQL Server** 를 사용 하 여 **geek of 퀴즈** 응용 프로그램에서 메시지를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-277">In this exercise, you will use **SQL Server** to distribute messages across the **Geek Quiz** application.</span></span> <span data-ttu-id="cb067-278">이러한 작업을 단일 테스트 컴퓨터에서 실행 하 여 구성을 설정 하는 방법을 배울 수 있습니다. 그러나 전체 효과를 얻으려면 SignalR 응용 프로그램을 둘 이상의 서버에 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-278">You will run these tasks on a single test machine to learn how to set up the configuration, but in order to get the full effect, you will need to deploy the SignalR application to two or more servers.</span></span> <span data-ttu-id="cb067-279">또한 서버 중 하나 또는 별도의 전용 서버에 SQL Server를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-279">You must also install SQL Server on one of the servers, or on a separate dedicated server.</span></span>

![SQL Server 다이어그램을 사용 하 여 Scale Out](real-time-web-applications-with-signalr/_static/image15.png)

<a id="Ex2Task1"></a>
#### <a name="task-1---understanding-the-scenario"></a><span data-ttu-id="cb067-281">작업 1-시나리오 이해</span><span class="sxs-lookup"><span data-stu-id="cb067-281">Task 1 - Understanding the Scenario</span></span>

<span data-ttu-id="cb067-282">이 작업에서는 로컬 컴퓨터에서 여러 IIS 인스턴스를 시뮬레이션 하는 **Geek of 퀴즈** 의 두 인스턴스를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-282">In this task, you will run 2 instances of **Geek Quiz** simulating multiple IIS instances on your local machine.</span></span> <span data-ttu-id="cb067-283">이 시나리오에서 한 응용 프로그램에 대 한 기타 정보 질문에 응답 하는 경우 두 번째 인스턴스의 통계 페이지에서 업데이트에 대 한 알림이 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-283">In this scenario, when answering trivia questions on one application, update won't be notified on the statistics page of the second instance.</span></span> <span data-ttu-id="cb067-284">이 시뮬레이션은 응용 프로그램이 여러 인스턴스에 배포 되 고 부하 분산 장치를 사용 하 여 통신 하는 환경과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-284">This simulation resembles an environment where your application is deployed on multiple instances and using a load balancer to communicate with them.</span></span>

1. <span data-ttu-id="cb067-285">**Source/Ex2-ScalingOutWithSQLServer/begin** 폴더에 있는 **begin .sln** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-285">Open the **Begin.sln** solution located in the **Source/Ex2-ScalingOutWithSQLServer/Begin** folder.</span></span> <span data-ttu-id="cb067-286">로드 된 후에는 솔루션에 동일한 구조를 가진 두 개의 프로젝트가 있지만 이름이 다른 두 프로젝트가 **서버 탐색기** 에 대 한 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-286">Once loaded, you will notice on the **Server Explorer** that the solution has two projects with identical structures but different names.</span></span> <span data-ttu-id="cb067-287">이렇게 하면 로컬 컴퓨터에서 동일한 응용 프로그램의 두 인스턴스를 실행 하는 것이 시뮬레이션 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-287">This will simulate running two instances of the same application on your local machine.</span></span>

    <span data-ttu-id="cb067-288">![Geek of 퀴즈의 2 개 인스턴스를 시뮬레이션 하는 솔루션 시작](real-time-web-applications-with-signalr/_static/image16.png "Geek of 퀴즈의 2 개 인스턴스를 시뮬레이션 하는 솔루션 시작")</span><span class="sxs-lookup"><span data-stu-id="cb067-288">![Begin Solution Simulating 2 Instances of Geek Quiz](real-time-web-applications-with-signalr/_static/image16.png "Begin Solution Simulating 2 Instances of Geek Quiz")</span></span>

    <span data-ttu-id="cb067-289">*Geek of 퀴즈의 2 개 인스턴스를 시뮬레이션 하는 솔루션 시작*</span><span class="sxs-lookup"><span data-stu-id="cb067-289">*Begin Solution Simulating 2 Instances of Geek Quiz*</span></span>
2. <span data-ttu-id="cb067-290">솔루션 노드를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 하 여 솔루션의 속성 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-290">Open the properties page of the solution by right-clicking the solution node and selecting **Properties**.</span></span> <span data-ttu-id="cb067-291">시작 **프로젝트**에서 **여러 개의 시작 프로젝트** 를 선택 하 고 두 프로젝트의 **동작** 값을 *시작*으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-291">Under **Startup Project**, select **Multiple startup projects** and change the **Action** value for both projects to *Start*.</span></span>

    <span data-ttu-id="cb067-292">![여러 프로젝트 시작](real-time-web-applications-with-signalr/_static/image17.png "여러 프로젝트 시작")</span><span class="sxs-lookup"><span data-stu-id="cb067-292">![Starting Multiple Projects](real-time-web-applications-with-signalr/_static/image17.png "Starting Multiple Projects")</span></span>

    <span data-ttu-id="cb067-293">*여러 프로젝트 시작*</span><span class="sxs-lookup"><span data-stu-id="cb067-293">*Starting Multiple Projects*</span></span>
3. <span data-ttu-id="cb067-294">**F5** 키를 눌러 솔루션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-294">Press **F5** to run the solution.</span></span> <span data-ttu-id="cb067-295">응용 프로그램은 동일한 응용 프로그램의 여러 인스턴스를 시뮬레이션 하는 서로 다른 포트에서 **Geek of 퀴즈** 의 두 인스턴스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-295">The application will launch two instances of **Geek Quiz** in different ports, simulating multiple instances of the same application.</span></span> <span data-ttu-id="cb067-296">왼쪽에 있는 브라우저 중 하나를 화면 오른쪽에 고정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-296">Pin one of the browsers on left and the other on the right of your screen.</span></span> <span data-ttu-id="cb067-297">자격 증명을 사용 하 여 로그인 하거나 새 사용자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-297">Log in with your credentials or register a new user.</span></span> <span data-ttu-id="cb067-298">로그인 되 면 왼쪽에 있는 기타 정보 페이지를 유지 하 고 오른쪽 브라우저의 **통계** 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-298">Once logged in, keep the Trivia page on the left and go to the **Statistics** page in the browser on the right.</span></span>

    ![Geek of 퀴즈를 나란히](real-time-web-applications-with-signalr/_static/image18.png)

    <span data-ttu-id="cb067-300">*Geek of 퀴즈를 나란히*</span><span class="sxs-lookup"><span data-stu-id="cb067-300">*Geek Quiz Side by Side*</span></span>

    ![다른 포트의 geek of 퀴즈](real-time-web-applications-with-signalr/_static/image19.png)

    <span data-ttu-id="cb067-302">*다른 포트의 geek of 퀴즈*</span><span class="sxs-lookup"><span data-stu-id="cb067-302">*Geek Quiz in Different Ports*</span></span>
4. <span data-ttu-id="cb067-303">왼쪽 브라우저에서 질문에 대 한 대답을 시작 하면 오른쪽 브라우저의 **통계** 페이지가 업데이트 되지 않는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-303">Start answering questions in the left browser and you will notice that the **Statistics** page in the right browser is not being updated.</span></span> <span data-ttu-id="cb067-304">**SignalR** 는 로컬 캐시를 사용 하 여 클라이언트 전체에 메시지를 분산 하 고이 시나리오는 여러 인스턴스를 시뮬레이션 하기 때문에 캐시는 서로 공유 되지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-304">This is because **SignalR** uses a local cache to distribute messages across their clients and this scenario is simulating multiple instances, therefore the cache is not shared between them.</span></span> <span data-ttu-id="cb067-305">동일한 단계를 테스트 하 고 단일 앱을 사용 하 여 **SignalR** 작동 하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-305">You can verify that **SignalR** is working by testing the same steps but using a single app.</span></span> <span data-ttu-id="cb067-306">다음 작업에서는 인스턴스 간에 메시지를 복제 하도록 후면판을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-306">In the following tasks you will configure a backplane to replicate the messages across instances.</span></span>
5. <span data-ttu-id="cb067-307">Visual Studio로 돌아가서 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-307">Go back to Visual Studio and stop debugging.</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-sql-server-backplane"></a><span data-ttu-id="cb067-308">작업 2-SQL Server 백플레인 만들기</span><span class="sxs-lookup"><span data-stu-id="cb067-308">Task 2 – Creating the SQL Server Backplane</span></span>

<span data-ttu-id="cb067-309">이 작업에서는 **Geek of 퀴즈** 응용 프로그램의 후면판 역할을 할 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-309">In this task, you will create a database that will serve as a backplane for the **Geek Quiz** application.</span></span> <span data-ttu-id="cb067-310">**SQL Server 개체 탐색기** 를 사용 하 여 서버를 검색 하 고 데이터베이스를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-310">You will use **SQL Server Object Explorer** to browse your server and initialize the database.</span></span> <span data-ttu-id="cb067-311">또한 **Service Broker**를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-311">Additionally, you will enable the **Service Broker**.</span></span>

1. <span data-ttu-id="cb067-312">**Visual Studio**에서 메뉴 **보기** 를 열고 **SQL Server 개체 탐색기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-312">In **Visual Studio**, open menu **View** and select **SQL Server Object Explorer**.</span></span>
2. <span data-ttu-id="cb067-313">**SQL Server** 노드를 마우스 오른쪽 단추로 클릭 하 고 **SQL Server 추가** ... 옵션을 선택 하 여 LocalDB 인스턴스에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-313">Connect to your LocalDB instance by right-clicking the **SQL Server** node and selecting **Add SQL Server...** option.</span></span>

    <span data-ttu-id="cb067-314">![SQL Server 인스턴스 추가](real-time-web-applications-with-signalr/_static/image20.png "SQL Server 인스턴스 추가")</span><span class="sxs-lookup"><span data-stu-id="cb067-314">![Adding a SQL Server Instance](real-time-web-applications-with-signalr/_static/image20.png "Adding a SQL Server Instance")</span></span>

    <span data-ttu-id="cb067-315">*SQL Server 개체 탐색기에 SQL Server 인스턴스 추가*</span><span class="sxs-lookup"><span data-stu-id="cb067-315">*Adding a SQL Server instance to SQL Server Object Explorer*</span></span>
3. <span data-ttu-id="cb067-316">**서버 이름** 을 *(localdb) \v11.0* 으로 설정 하 고 **Windows 인증** 을 인증 모드로 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-316">Set the **server name** to *(localdb)\v11.0* and leave **Windows Authentication** as your authentication mode.</span></span> <span data-ttu-id="cb067-317">**연결**을 클릭하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-317">Click **Connect** to continue.</span></span>

    <span data-ttu-id="cb067-318">![LocalDB에 연결](real-time-web-applications-with-signalr/_static/image21.png "LocalDB에 연결")</span><span class="sxs-lookup"><span data-stu-id="cb067-318">![Connecting to LocalDB](real-time-web-applications-with-signalr/_static/image21.png "Connecting to LocalDB")</span></span>

    <span data-ttu-id="cb067-319">*LocalDB에 연결*</span><span class="sxs-lookup"><span data-stu-id="cb067-319">*Connecting to LocalDB*</span></span>
4. <span data-ttu-id="cb067-320">이제 LocalDB 인스턴스에 연결 되었으므로 SignalR에 대 한 SQL Server 후면판을 나타내는 데이터베이스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-320">Now that you are connected to your LocalDB instance, you will need to create a database that will represent the SQL Server backplane for SignalR.</span></span> <span data-ttu-id="cb067-321">이렇게 하려면 **데이터베이스** 노드를 마우스 오른쪽 단추로 클릭 하 고 **새 데이터베이스 추가**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-321">To do this, right-click the **Databases** node and select **Add New Database**.</span></span>

    <span data-ttu-id="cb067-322">![새 데이터베이스 추가](real-time-web-applications-with-signalr/_static/image22.png "새 데이터베이스 추가")</span><span class="sxs-lookup"><span data-stu-id="cb067-322">![Adding a new database](real-time-web-applications-with-signalr/_static/image22.png "Adding a new database")</span></span>

    <span data-ttu-id="cb067-323">*새 데이터베이스 추가*</span><span class="sxs-lookup"><span data-stu-id="cb067-323">*Adding a new database*</span></span>
5. <span data-ttu-id="cb067-324">데이터베이스 이름을 *SignalR* 로 설정 하 고 **확인** 을 클릭 하 여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-324">Set the database name to *SignalR* and click **OK** to create it.</span></span>

    <span data-ttu-id="cb067-325">![SignalR 데이터베이스 만들기](real-time-web-applications-with-signalr/_static/image23.png "SignalR 데이터베이스 만들기")</span><span class="sxs-lookup"><span data-stu-id="cb067-325">![Creating the SignalR database](real-time-web-applications-with-signalr/_static/image23.png "Creating the SignalR database")</span></span>

    <span data-ttu-id="cb067-326">*SignalR 데이터베이스 만들기*</span><span class="sxs-lookup"><span data-stu-id="cb067-326">*Creating the SignalR database*</span></span>

    > [!NOTE]
    > <span data-ttu-id="cb067-327">데이터베이스의 이름을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-327">You can choose any name for the database.</span></span>
6. <span data-ttu-id="cb067-328">후면판에서 업데이트를 보다 효율적으로 수신 하려면 데이터베이스에 대해 Service Broker를 사용 하도록 설정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-328">To receive updates more efficiently from the backplane, it is recommended to enable Service Broker for the database.</span></span> <span data-ttu-id="cb067-329">Service Broker은 SQL Server의 메시징 및 큐에 대 한 기본 지원을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-329">Service Broker provides native support for messaging and queuing in SQL Server.</span></span> <span data-ttu-id="cb067-330">후면판은 Service Broker 없이도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-330">The backplane also works without Service Broker.</span></span> <span data-ttu-id="cb067-331">데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 **새 쿼리**를 선택 하 여 새 쿼리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-331">Open a new query by right-clicking the database and select **New Query**.</span></span>

    <span data-ttu-id="cb067-332">![새 쿼리 열기](real-time-web-applications-with-signalr/_static/image24.png "새 쿼리 열기")</span><span class="sxs-lookup"><span data-stu-id="cb067-332">![Opening a New Query](real-time-web-applications-with-signalr/_static/image24.png "Opening a New Query")</span></span>

    <span data-ttu-id="cb067-333">*새 쿼리 열기*</span><span class="sxs-lookup"><span data-stu-id="cb067-333">*Opening a New Query*</span></span>
7. <span data-ttu-id="cb067-334">Service Broker 사용 하도록 설정 되어 있는지 여부를 확인 하려면를 사용 **하 여** **\_Broker\_사용** 열을 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-334">To check whether Service Broker is enabled, query the **is\_broker\_enabled** column in the **sys.databases** catalog view.</span></span> <span data-ttu-id="cb067-335">최근에 열었던 쿼리 창에서 다음 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-335">Execute the following script in the recently opened query window.</span></span>

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample11.sql)]

    <span data-ttu-id="cb067-336">![Service Broker 상태 쿼리](real-time-web-applications-with-signalr/_static/image25.png "Service Broker 상태 쿼리")</span><span class="sxs-lookup"><span data-stu-id="cb067-336">![Querying the Service Broker Status](real-time-web-applications-with-signalr/_static/image25.png "Querying the Service Broker Status")</span></span>

    <span data-ttu-id="cb067-337">*Service Broker 상태 쿼리*</span><span class="sxs-lookup"><span data-stu-id="cb067-337">*Querying the Service Broker Status*</span></span>
8. <span data-ttu-id="cb067-338">의 값 **이\_broker\_사용 하도록 설정** 된 경우 데이터베이스에서 사용 하도록 설정 된 열이 0&quot;&quot;다음 명령을 사용 하 여 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-338">If the value of the **is\_broker\_enabled** column in your database is &quot;0&quot;, use the following command to enable it.</span></span> <span data-ttu-id="cb067-339">**&lt;데이터베이스&gt;** 을 만들 때 설정한 이름으로 바꿉니다 (예: SignalR).</span><span class="sxs-lookup"><span data-stu-id="cb067-339">Replace **&lt;YOUR-DATABASE&gt;** with the name you set when creating the database (e.g.: SignalR).</span></span>

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample12.sql)]

    <span data-ttu-id="cb067-340">![Service Broker 사용](real-time-web-applications-with-signalr/_static/image26.png "Service Broker 사용")</span><span class="sxs-lookup"><span data-stu-id="cb067-340">![Enabling Service Broker](real-time-web-applications-with-signalr/_static/image26.png "Enabling Service Broker")</span></span>

    <span data-ttu-id="cb067-341">*Service Broker 사용*</span><span class="sxs-lookup"><span data-stu-id="cb067-341">*Enabling Service Broker*</span></span>

    > [!NOTE]
    > <span data-ttu-id="cb067-342">이 쿼리가 교착 상태로 표시 되는 경우 DB에 연결 된 응용 프로그램이 없는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-342">If this query appears to deadlock, make sure there are no applications connected to the DB.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--configuring-the-signalr-application"></a><span data-ttu-id="cb067-343">작업 3-SignalR 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="cb067-343">Task 3 – Configuring the SignalR Application</span></span>

<span data-ttu-id="cb067-344">이 작업에서는 SQL Server 후면판에 연결 하도록 **Geek of 퀴즈** 를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-344">In this task, you will configure **Geek Quiz** to connect to the SQL Server backplane.</span></span> <span data-ttu-id="cb067-345">먼저 **SignalR** NuGet 패키지를 추가 하 고 연결 문자열을 후면판 데이터베이스로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-345">You will first add the **SignalR.SqlServer** NuGet package and set the connection string to your backplane database.</span></span>

1. <span data-ttu-id="cb067-346">**도구** > **NuGet 패키지 관리자**에서 **패키지 관리자 콘솔** 을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-346">Open the **Package Manager Console** from **Tools** > **NuGet Package Manager**.</span></span> <span data-ttu-id="cb067-347">**기본 프로젝트** 드롭다운 목록에서 **GeekQuiz** 프로젝트가 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-347">Make sure that **GeekQuiz** project is selected in the **Default project** drop-down list.</span></span> <span data-ttu-id="cb067-348">다음 명령을 입력 하 여 **SignalR** NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-348">Type the following command to install the **Microsoft.AspNet.SignalR.SqlServer** NuGet package.</span></span>

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample13.ps1)]
2. <span data-ttu-id="cb067-349">이전 단계를 반복 하지만 이번에는 project **GeekQuiz2**에 대해이 시간을 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-349">Repeat the previous step but this time for project **GeekQuiz2**.</span></span>
3. <span data-ttu-id="cb067-350">SQL Server 백플레인를 구성 하려면 **GeekQuiz** 프로젝트의 **Startup.cs** 파일을 열고 **configure** 메서드에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-350">To configure the SQL Server backplane, open the **Startup.cs** file of the **GeekQuiz** project and add the following code to the **Configure** method.</span></span> <span data-ttu-id="cb067-351">**&lt;-데이터베이스&gt;** 을 SQL Server 백플레인를 만들 때 사용한 데이터베이스 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-351">Replace **&lt;YOUR-DATABASE&gt;** with your database name you used when creating the SQL Server backplane.</span></span> <span data-ttu-id="cb067-352">**GeekQuiz2** 프로젝트에 대해이 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-352">Repeat this step for the **GeekQuiz2** project.</span></span>

    <span data-ttu-id="cb067-353">(코드 조각- *RealTimeSignalR-Ex2-StartupConfiguration*)</span><span class="sxs-lookup"><span data-stu-id="cb067-353">(Code Snippet - *RealTimeSignalR - Ex2 - StartupConfiguration*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample14.cs)]
4. <span data-ttu-id="cb067-354">이제 두 프로젝트가 모두 SQL Server 후면판을 사용 하도록 구성 되었으므로 **F5** 키를 눌러 동시에 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-354">Now that both projects are configured to use the SQL Server backplane, press **F5** to run them simultaneously.</span></span>
5. <span data-ttu-id="cb067-355">다시 **Visual Studio** 는 서로 다른 포트에서 두 개의 **geek of 퀴즈** 인스턴스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-355">Again, **Visual Studio** will launch two instances of **Geek Quiz** in different ports.</span></span> <span data-ttu-id="cb067-356">왼쪽에 있는 브라우저 중 하나를 화면 오른쪽에 고정 하 고 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-356">Pin one of the browsers on the left and the other on the right of your screen and log in with your credentials.</span></span> <span data-ttu-id="cb067-357">왼쪽에 있는 기타 정보 페이지를 유지 하 고 오른쪽 브라우저에서 **통계** pagein 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-357">Keep the Trivia page on the left and go to **Statistics** pagein the right browser.</span></span>
6. <span data-ttu-id="cb067-358">왼쪽 브라우저에서 질문에 답변 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-358">Start answering questions in the left browser.</span></span> <span data-ttu-id="cb067-359">이번에는 후면판 덕분에 **통계** 페이지가 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-359">This time, the **Statistics** page is updated thanks to the backplane.</span></span> <span data-ttu-id="cb067-360">응용 프로그램 사이를 전환 하 고 (이제**통계** 는 왼쪽에 있고, **기타 정보** 는 오른쪽에 있습니다.) 테스트를 반복 하 여 두 인스턴스에 대해 모두 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-360">Switch between applications (**Statistics** is now on the left, and **Trivia** is on the right) and repeat the test to validate that it is working for both instances.</span></span> <span data-ttu-id="cb067-361">후면판은 연결 된 각 서버에 대 한 메시지의 *공유 캐시로* 사용 되며, 각 서버는 연결 된 클라이언트에 배포할 메시지를 자체 로컬 캐시에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-361">The backplane serves as a *shared cache* of messages for each connected server, and each server will store the messages in their own local cache to distribute to connected clients.</span></span>
7. <span data-ttu-id="cb067-362">Visual Studio로 돌아가서 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-362">Go back to Visual Studio and stop debugging.</span></span>
8. <span data-ttu-id="cb067-363">SQL Server 백플레인 구성 요소는 지정 된 데이터베이스에 필요한 테이블을 자동으로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-363">The SQL Server backplane component automatically generates the necessary tables on the specified database.</span></span> <span data-ttu-id="cb067-364">**SQL Server 개체 탐색기** 패널에서 후면판에 대해 만든 데이터베이스 (예: SignalR)를 열고 해당 테이블을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-364">In the **SQL Server Object Explorer** panel, open the database you created for the backplane (e.g.: SignalR) and expand its tables.</span></span> <span data-ttu-id="cb067-365">다음 테이블이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-365">You should see the following tables:</span></span>

    ![후면판 생성 테이블](real-time-web-applications-with-signalr/_static/image27.png)

    <span data-ttu-id="cb067-367">*후면판 생성 테이블*</span><span class="sxs-lookup"><span data-stu-id="cb067-367">*Backplane Generated Tables*</span></span>
9. <span data-ttu-id="cb067-368">**SignalR\_0** 테이블을 마우스 오른쪽 단추로 클릭 하 고 **데이터 보기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-368">Right-click the **SignalR.Messages\_0** table and select **View Data**.</span></span>

    ![SignalR 후면판 메시지 보기 테이블](real-time-web-applications-with-signalr/_static/image28.png)

    <span data-ttu-id="cb067-370">*SignalR 후면판 메시지 보기 테이블*</span><span class="sxs-lookup"><span data-stu-id="cb067-370">*View SignalR Backplane Messages Table*</span></span>
10. <span data-ttu-id="cb067-371">기타 정보 질문에 대답할 때 **허브** 로 전송 되는 다른 메시지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-371">You can see the different messages sent to the **Hub** when answering the trivia questions.</span></span> <span data-ttu-id="cb067-372">후면판은 이러한 메시지를 연결 된 인스턴스에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-372">The backplane distributes these messages to any connected instance.</span></span>

    ![후면판 메시지 테이블](real-time-web-applications-with-signalr/_static/image29.png)

    <span data-ttu-id="cb067-374">*후면판 메시지 테이블*</span><span class="sxs-lookup"><span data-stu-id="cb067-374">*Backplane Messages Table*</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="cb067-375">요약</span><span class="sxs-lookup"><span data-stu-id="cb067-375">Summary</span></span>

<span data-ttu-id="cb067-376">이 실습 랩에서는 응용 프로그램에 **SignalR** 를 추가 하 고 **허브**를 사용 하 여 서버에서 연결 된 클라이언트로 알림을 보내는 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-376">In this hands-on lab, you have learned how to add **SignalR** to your application and send notifications from the server to your connected clients using **Hubs**.</span></span> <span data-ttu-id="cb067-377">또한 응용 프로그램을 여러 IIS 인스턴스에 배포할 때 *후면판* 구성 요소를 사용 하 여 응용 프로그램을 확장 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="cb067-377">Additionally, you learned how to scale out your application by using a *backplane* component when your application is deployed in multiple IIS instances.</span></span>
