---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: '자습서: SignalR 2를 사용 하 여 서버 브로드캐스트 | Microsoft Docs'
author: tdykstra
description: 이 자습서에서는 ASP.NET SignalR 2를 사용 하 여 서버 브로드캐스트 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다.
ms.author: bradyg
ms.date: 01/02/2019
ms.topic: tutorial
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14924109fff8db3e537e6bc08b6dc868792ee660
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431243"
---
# <a name="tutorial-server-broadcast-with-signalr-2"></a><span data-ttu-id="39ab7-103">자습서: SignalR 2를 사용 하 여 서버 브로드캐스트</span><span class="sxs-lookup"><span data-stu-id="39ab7-103">Tutorial: Server broadcast with SignalR 2</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="39ab7-104">이 자습서에서는 ASP.NET SignalR 2를 사용 하 여 서버 브로드캐스트 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-104">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide server broadcast functionality.</span></span> <span data-ttu-id="39ab7-105">서버 브로드캐스트는 서버에서 클라이언트로 전송 되는 통신을 시작 하는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-105">Server broadcast means that the server starts the communications sent to clients.</span></span>

<span data-ttu-id="39ab7-106">이 자습서에서 만들 응용 프로그램은 서버 브로드캐스트 기능을 위한 일반적인 시나리오인 주식 시세 표시기를 시뮬레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-106">The application that you'll create in this tutorial simulates a stock ticker, a typical scenario for server broadcast functionality.</span></span> <span data-ttu-id="39ab7-107">정기적으로 서버는 주식 가격을 임의로 업데이트 하 고 연결 된 모든 클라이언트에 업데이트를 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-107">Periodically, the server randomly updates stock prices and broadcast the updates to all connected clients.</span></span> <span data-ttu-id="39ab7-108">브라우저에서 **변경 내용** 및 **%** 열의 숫자 및 기호는 서버의 알림에 따라 동적으로 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-108">In the browser, the numbers and symbols in the **Change** and **%** columns dynamically change in response to notifications from the server.</span></span> <span data-ttu-id="39ab7-109">동일한 URL에 대 한 추가 브라우저를 열 경우 모두 동일한 데이터 및 동일한 데이터 변경 내용을 동시에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-109">If you open additional browsers to the same URL, they all show the same data and the same changes to the data simultaneously.</span></span>

![웹 만들기](tutorial-server-broadcast-with-signalr/_static/image1.png)

<span data-ttu-id="39ab7-111">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-111">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="39ab7-112">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="39ab7-112">Create the project</span></span>
> * <span data-ttu-id="39ab7-113">서버 코드 설정</span><span class="sxs-lookup"><span data-stu-id="39ab7-113">Set up the server code</span></span>
> * <span data-ttu-id="39ab7-114">서버 코드 검사</span><span class="sxs-lookup"><span data-stu-id="39ab7-114">Examine the server code</span></span>
> * <span data-ttu-id="39ab7-115">클라이언트 코드 설정</span><span class="sxs-lookup"><span data-stu-id="39ab7-115">Set up the client code</span></span>
> * <span data-ttu-id="39ab7-116">클라이언트 코드 검사</span><span class="sxs-lookup"><span data-stu-id="39ab7-116">Examine the client code</span></span>
> * <span data-ttu-id="39ab7-117">애플리케이션 테스트</span><span class="sxs-lookup"><span data-stu-id="39ab7-117">Test the application</span></span>
> * <span data-ttu-id="39ab7-118">로깅 사용</span><span class="sxs-lookup"><span data-stu-id="39ab7-118">Enable logging</span></span>

> [!IMPORTANT]
> <span data-ttu-id="39ab7-119">응용 프로그램을 빌드하는 단계를 수행 하지 않으려면 비어 있는 새 ASP.NET 웹 응용 프로그램 프로젝트에 SignalR 패키지를 설치 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-119">If you don't want to work through the steps of building the application, you can install the SignalR.Sample package in a new Empty ASP.NET Web Application project.</span></span> <span data-ttu-id="39ab7-120">이 자습서의 단계를 수행 하지 않고 NuGet 패키지를 설치 하는 경우 *readme.txt* 파일의 지침을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-120">If you install the NuGet package without performing the steps in this tutorial, you must follow the instructions in the *readme.txt* file.</span></span> <span data-ttu-id="39ab7-121">패키지를 실행 하려면 설치 된 패키지에서 `ConfigureSignalR` 메서드를 호출 하는 OWIN startup 클래스를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-121">To run the package you need to add an OWIN startup class which calls the `ConfigureSignalR` method in the installed package.</span></span> <span data-ttu-id="39ab7-122">OWIN startup 클래스를 추가 하지 않으면 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-122">You will receive an error if you do not add the OWIN startup class.</span></span> <span data-ttu-id="39ab7-123">이 문서의 [StockTicker 샘플 설치](#install-the-stockticker-sample) 섹션을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="39ab7-123">See the [Install the StockTicker sample](#install-the-stockticker-sample) section of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39ab7-124">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="39ab7-124">Prerequisites</span></span>

* <span data-ttu-id="39ab7-125">[ASP.NET 및 웹 개발](https://visualstudio.microsoft.com/downloads/) 워크로드가 있는 **Visual Studio 2017**</span><span class="sxs-lookup"><span data-stu-id="39ab7-125">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="39ab7-126">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="39ab7-126">Create the project</span></span>

<span data-ttu-id="39ab7-127">이 섹션에서는 Visual Studio 2017을 사용 하 여 빈 ASP.NET 웹 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-127">This section shows how to use Visual Studio 2017 to create an empty ASP.NET Web Application.</span></span>

1. <span data-ttu-id="39ab7-128">Visual Studio에서 ASP.NET 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-128">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![웹 만들기](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. <span data-ttu-id="39ab7-130">**새 ASP.NET 웹 응용 프로그램-SignalR. StockTicker** 창에서 선택 된 **상태로 두고** **확인**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-130">In the **New ASP.NET Web Application - SignalR.StockTicker** window, leave **Empty** selected and select **OK**.</span></span>

## <a name="set-up-the-server-code"></a><span data-ttu-id="39ab7-131">서버 코드 설정</span><span class="sxs-lookup"><span data-stu-id="39ab7-131">Set up the server code</span></span>

<span data-ttu-id="39ab7-132">이 섹션에서는 서버에서 실행 되는 코드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-132">In this section, you set up the code that runs on the server.</span></span>

### <a name="create-the-stock-class"></a><span data-ttu-id="39ab7-133">스톡 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="39ab7-133">Create the Stock class</span></span>

<span data-ttu-id="39ab7-134">먼저 주식 정보를 저장 하 고 전송 하는 데 사용할 *스톡* 모델 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-134">You begin by creating the *Stock* model class that you'll use to store and transmit information about a stock.</span></span>

1. <span data-ttu-id="39ab7-135">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 > **클래스** **추가** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-135">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="39ab7-136">클래스 이름을 *스톡* 으로 만들고 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-136">Name the class *Stock* and add it to the project.</span></span>

1. <span data-ttu-id="39ab7-137">*Stock.cs* 파일의 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-137">Replace the code in the *Stock.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    <span data-ttu-id="39ab7-138">주식을 만들 때 설정 하는 두 가지 속성 (예: Microsoft의 MSFT) 및 `Price``Symbol` 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-138">The two properties that you'll set when you create stocks are `Symbol` (for example, MSFT for Microsoft) and `Price`.</span></span> <span data-ttu-id="39ab7-139">다른 속성은 `Price`를 설정 하는 방법과 시기에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-139">The other properties depend on how and when you set `Price`.</span></span> <span data-ttu-id="39ab7-140">`Price`를 처음으로 설정 하는 경우 값이 `DayOpen`으로 전파 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-140">The first time you set `Price`, the value gets propagated to `DayOpen`.</span></span> <span data-ttu-id="39ab7-141">그런 다음 `Price`설정 하면 앱에서 `Price`와 `DayOpen`간의 차이를 기준으로 `Change` 및 `PercentChange` 속성 값을 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-141">After that, when you set `Price`, the app calculates the `Change` and `PercentChange` property values based on the difference between `Price` and `DayOpen`.</span></span>

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a><span data-ttu-id="39ab7-142">StockTickerHub 및 StockTicker 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="39ab7-142">Create the StockTickerHub and StockTicker classes</span></span>

<span data-ttu-id="39ab7-143">SignalR Hub API를 사용 하 여 서버와 클라이언트 간의 상호 작용을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-143">You'll use the SignalR Hub API to handle server-to-client interaction.</span></span> <span data-ttu-id="39ab7-144">SignalR `Hub` 클래스에서 파생 되는 `StockTickerHub` 클래스는 클라이언트의 수신 연결 및 메서드 호출을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-144">A `StockTickerHub` class that derives from the SignalR `Hub` class will handle receiving connections and method calls from clients.</span></span> <span data-ttu-id="39ab7-145">또한 주식 데이터를 유지 관리 하 고 `Timer` 개체를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-145">You also need to maintain stock data and run a `Timer` object.</span></span> <span data-ttu-id="39ab7-146">`Timer` 개체는 클라이언트 연결과 무관 하 게 가격 업데이트를 주기적으로 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-146">The `Timer` object will periodically trigger price updates independent of client connections.</span></span> <span data-ttu-id="39ab7-147">허브가 임시 이기 때문에 `Hub` 클래스에 이러한 함수를 배치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-147">You can't put these functions in a `Hub` class, because Hubs are transient.</span></span> <span data-ttu-id="39ab7-148">앱은 클라이언트에서 서버로의 연결과 같은 허브의 각 태스크에 대 한 `Hub` 클래스 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-148">The app creates a `Hub` class instance for each task on the hub, like connections and calls from the client to the server.</span></span> <span data-ttu-id="39ab7-149">따라서 주식 데이터를 유지 하 고, 가격을 업데이트 하 고, 가격 업데이트를 브로드캐스팅하는 메커니즘이 별도의 클래스에서 실행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-149">So the mechanism that keeps stock data, updates prices, and broadcasts the price updates has to run in a separate class.</span></span> <span data-ttu-id="39ab7-150">클래스의 이름을 `StockTicker`합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-150">You'll name the class `StockTicker`.</span></span>

![StockTicker에서 브로드캐스팅](tutorial-server-broadcast-with-signalr/_static/image3.png)

<span data-ttu-id="39ab7-152">`StockTicker` 클래스의 인스턴스를 서버에서 실행 하려는 경우에만 각 `StockTickerHub` 인스턴스에서 singleton `StockTicker` 인스턴스로 참조를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-152">You only want one instance of the `StockTicker` class to run on the server, so you'll need to set up a reference from each `StockTickerHub` instance to the singleton `StockTicker` instance.</span></span> <span data-ttu-id="39ab7-153">`StockTicker` 클래스는 주식 데이터를 포함 하 고 업데이트를 트리거 하지만 `StockTicker` `Hub` 클래스가 아니기 때문에 클라이언트에 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-153">The `StockTicker` class has to broadcast to clients because it has the stock data and triggers updates, but `StockTicker` isn't a `Hub` class.</span></span> <span data-ttu-id="39ab7-154">`StockTicker` 클래스는 SignalR Hub 연결 컨텍스트 개체에 대 한 참조를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-154">The `StockTicker` class has to get a reference to the SignalR Hub connection context object.</span></span> <span data-ttu-id="39ab7-155">그런 다음 SignalR 연결 컨텍스트 개체를 사용 하 여 클라이언트에 브로드캐스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-155">It can then use the SignalR connection context object to broadcast to clients.</span></span>

#### <a name="create-stocktickerhubcs"></a><span data-ttu-id="39ab7-156">StockTickerHub.cs 만들기</span><span class="sxs-lookup"><span data-stu-id="39ab7-156">Create StockTickerHub.cs</span></span>

1. <span data-ttu-id="39ab7-157">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가** > **새 항목**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-157">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="39ab7-158">**새 항목 추가-SignalR. StockTicker**에서 **설치** > **Visual C#**  > **Web** > **SignalR** 를 선택한 다음 **SignalR Hub 클래스 (v2)** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-158">In **Add New Item - SignalR.StockTicker**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="39ab7-159">클래스 이름을 *StockTickerHub* 로 추가 하 고 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-159">Name the class *StockTickerHub* and add it to the project.</span></span>

    <span data-ttu-id="39ab7-160">이 단계에서는 *StockTickerHub.cs* 클래스 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-160">This step creates the *StockTickerHub.cs* class file.</span></span> <span data-ttu-id="39ab7-161">동시에 SignalR를 지 원하는 스크립트 파일 및 어셈블리 참조 집합을 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-161">Simultaneously, it adds a set of script files and assembly references that supports SignalR to the project.</span></span>

1. <span data-ttu-id="39ab7-162">*StockTickerHub.cs* 파일의 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-162">Replace the code in the *StockTickerHub.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. <span data-ttu-id="39ab7-163">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-163">Save the file.</span></span>

<span data-ttu-id="39ab7-164">앱은 [허브](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) 클래스를 사용 하 여 클라이언트가 서버에서 호출할 수 있는 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-164">The app uses the [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) class to define methods the clients can call on the server.</span></span> <span data-ttu-id="39ab7-165">메서드 하나를 정의 하 고 `GetAllStocks()`합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-165">You're defining one method: `GetAllStocks()`.</span></span> <span data-ttu-id="39ab7-166">클라이언트는 처음 서버에 연결할 때이 메서드를 호출 하 여 현재 가격으로 모든 주식의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-166">When a client initially connects to the server, it will call this method to get a list of all of the stocks with their current prices.</span></span> <span data-ttu-id="39ab7-167">메서드를 동기적으로 실행 하 고 메모리에서 데이터를 반환 하기 때문에 `IEnumerable<Stock>`를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-167">The method can run synchronously and return `IEnumerable<Stock>` because it's returning data from memory.</span></span>

<span data-ttu-id="39ab7-168">데이터베이스 조회 나 웹 서비스 호출과 같이 대기와 관련 된 작업을 수행 하 여 메서드가 데이터를 가져와야 하는 경우 비동기 처리를 사용 하도록 `Task<IEnumerable<Stock>>`를 반환 값으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-168">If the method had to get the data by doing something that would involve waiting, like a database lookup or a web service call, you would specify `Task<IEnumerable<Stock>>` as the return value to enable asynchronous processing.</span></span> <span data-ttu-id="39ab7-169">자세한 내용은 [ASP.NET SignalR HUBS API 가이드-서버-비동기적으로 실행 하는 경우](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="39ab7-169">For more information, see [ASP.NET SignalR Hubs API Guide - Server - When to execute asynchronously](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).</span></span>

<span data-ttu-id="39ab7-170">`HubName` 특성은 앱이 클라이언트의 JavaScript 코드에서 허브를 참조 하는 방법을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-170">The `HubName` attribute specifies how the app will reference the Hub in JavaScript code on the client.</span></span> <span data-ttu-id="39ab7-171">클라이언트의 기본 이름입니다 .이 특성을 사용 하지 않는 경우는 클래스 이름의 camelCase 버전입니다 .이 경우에는 `stockTickerHub`입니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-171">The default name on the client if you don't use this attribute, is a camelCase version of the class name, which in this case would be `stockTickerHub`.</span></span>

<span data-ttu-id="39ab7-172">나중에 `StockTicker` 클래스를 만들 때 앱은 정적 `Instance` 속성에 해당 클래스의 단일 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-172">As you'll see later when you create the `StockTicker` class, the app creates a singleton instance of that class in its static `Instance` property.</span></span> <span data-ttu-id="39ab7-173">`StockTicker`의 단일 인스턴스는 연결 하거나 연결을 끊는 클라이언트 수에 관계 없이 메모리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-173">That singleton instance of `StockTicker` is in memory no matter how many clients connect or disconnect.</span></span> <span data-ttu-id="39ab7-174">이 인스턴스는 `GetAllStocks()` 메서드에서 현재 주식 정보를 반환 하는 데 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-174">That instance is what the `GetAllStocks()` method uses to return current stock information.</span></span>

#### <a name="create-stocktickercs"></a><span data-ttu-id="39ab7-175">StockTicker.cs 만들기</span><span class="sxs-lookup"><span data-stu-id="39ab7-175">Create StockTicker.cs</span></span>

1. <span data-ttu-id="39ab7-176">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 > **클래스** **추가** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-176">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="39ab7-177">클래스 이름을 *StockTicker* 로 추가 하 고 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-177">Name the class *StockTicker* and add it to the project.</span></span>

1. <span data-ttu-id="39ab7-178">*StockTicker.cs* 파일의 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-178">Replace the code in the *StockTicker.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

<span data-ttu-id="39ab7-179">모든 스레드가 동일한 StockTicker 코드 인스턴스를 실행 하므로 StockTicker 클래스는 스레드로부터 안전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-179">Since all threads will be running the same instance of StockTicker code, the StockTicker class has to be thread-safe.</span></span>

### <a name="examine-the-server-code"></a><span data-ttu-id="39ab7-180">서버 코드 검사</span><span class="sxs-lookup"><span data-stu-id="39ab7-180">Examine the server code</span></span>

<span data-ttu-id="39ab7-181">서버 코드를 살펴보면 앱이 작동 하는 방식을 이해 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-181">If you examine the server code, it will help you understand how the app works.</span></span>

#### <a name="storing-the-singleton-instance-in-a-static-field"></a><span data-ttu-id="39ab7-182">단일 인스턴스를 정적 필드에 저장</span><span class="sxs-lookup"><span data-stu-id="39ab7-182">Storing the singleton instance in a static field</span></span>

<span data-ttu-id="39ab7-183">이 코드는 `Instance` 속성을 클래스의 인스턴스로 백업 하는 정적 `_instance` 필드를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-183">The code initializes the static `_instance` field that backs the `Instance` property with an instance of the class.</span></span> <span data-ttu-id="39ab7-184">생성자는 전용 이므로 앱에서 만들 수 있는 클래스의 유일한 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-184">Because the constructor is private, it's the only instance of the class that the app can create.</span></span> <span data-ttu-id="39ab7-185">앱은 `_instance` 필드에 [초기화 지연을](/dotnet/framework/performance/lazy-initialization) 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-185">The app uses [Lazy initialization](/dotnet/framework/performance/lazy-initialization) for the `_instance` field.</span></span> <span data-ttu-id="39ab7-186">성능상의 이유로는 그렇지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-186">It's not for performance reasons.</span></span> <span data-ttu-id="39ab7-187">인스턴스를 만드는 것은 스레드로부터 안전한 지 확인 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-187">It's to make sure the instance creation is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

<span data-ttu-id="39ab7-188">클라이언트가 서버에 연결할 때마다 별도의 스레드에서 실행 되는 StockTickerHub 클래스의 새 인스턴스는 앞에서 `StockTickerHub` 클래스에서 살펴본 것 처럼 `StockTicker.Instance` 정적 속성에서 StockTicker singleton 인스턴스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-188">Each time a client connects to the server, a new instance of the StockTickerHub class running in a separate thread gets the StockTicker singleton instance from the `StockTicker.Instance` static property, as you saw earlier in the `StockTickerHub` class.</span></span>

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a><span data-ttu-id="39ab7-189">ConcurrentDictionary에 주식 데이터 저장</span><span class="sxs-lookup"><span data-stu-id="39ab7-189">Storing stock data in a ConcurrentDictionary</span></span>

<span data-ttu-id="39ab7-190">생성자는 일부 샘플 재고 데이터를 사용 하 여 `_stocks` 컬렉션을 초기화 하 고 `GetAllStocks`는 주식을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-190">The constructor initializes the `_stocks` collection with some sample stock data, and `GetAllStocks` returns the stocks.</span></span> <span data-ttu-id="39ab7-191">앞서 살펴본 것 처럼이 주식 컬렉션은 클라이언트가 호출할 수 있는 `Hub` 클래스의 서버 메서드인 `StockTickerHub.GetAllStocks`에 의해 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-191">As you saw earlier, this collection of stocks is returned by `StockTickerHub.GetAllStocks`, which is a server method in the `Hub` class that clients can call.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

<span data-ttu-id="39ab7-192">스톡 컬렉션은 스레드 보안을 위해 [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) 형식으로 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-192">The stocks collection is defined as a [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) type for thread safety.</span></span> <span data-ttu-id="39ab7-193">또는 [사전](https://msdn.microsoft.com/library/xfhwa508.aspx) 개체를 사용 하 고 변경할 때 사전을 명시적으로 잠글 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-193">As an alternative, you could use a [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) object and explicitly lock the dictionary when you make changes to it.</span></span>

<span data-ttu-id="39ab7-194">이 샘플 응용 프로그램의 경우 응용 프로그램 데이터를 메모리에 저장 하 고 앱이 `StockTicker` 인스턴스를 삭제할 때 데이터가 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-194">For this sample application, it's OK to store application data in memory and to lose the data when the app disposes of the  `StockTicker` instance.</span></span> <span data-ttu-id="39ab7-195">실제 응용 프로그램에서는 데이터베이스와 같은 백 엔드 데이터 저장소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-195">In a real application, you would work with a back-end data store like a database.</span></span>

#### <a name="periodically-updating-stock-prices"></a><span data-ttu-id="39ab7-196">정기적으로 주식 가격 업데이트</span><span class="sxs-lookup"><span data-stu-id="39ab7-196">Periodically updating stock prices</span></span>

<span data-ttu-id="39ab7-197">생성자는 임의 기준으로 주식 가격을 업데이트 하는 메서드를 주기적으로 호출 하는 `Timer` 개체를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-197">The constructor starts up a `Timer` object that periodically calls methods that update stock prices on a random basis.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 <span data-ttu-id="39ab7-198">`Timer`는 상태 매개 변수에 null을 전달 하는 `UpdateStockPrices`를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-198">`Timer` calls `UpdateStockPrices`, which passes in null in the state parameter.</span></span> <span data-ttu-id="39ab7-199">가격을 업데이트 하기 전에 앱은 `_updateStockPricesLock` 개체에 대 한 잠금을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-199">Before updating prices, the app takes a lock on the `_updateStockPricesLock` object.</span></span> <span data-ttu-id="39ab7-200">코드는 다른 스레드가 이미 가격을 업데이트 하 고 있는지 확인 한 다음 목록의 각 주식의 `TryUpdateStockPrice`를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-200">The code checks if another thread is already updating prices, and then it calls `TryUpdateStockPrice` on each stock in the list.</span></span> <span data-ttu-id="39ab7-201">`TryUpdateStockPrice` 메서드는 주식 가격을 변경할 것인지 여부와 변경 정도를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-201">The `TryUpdateStockPrice` method decides whether to change the stock price, and how much to change it.</span></span> <span data-ttu-id="39ab7-202">주가 변경 되 면 앱은 `BroadcastStockPrice`를 호출 하 여 모든 연결 된 클라이언트에 주식 가격 변경을 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-202">If the stock price changes, the app calls `BroadcastStockPrice` to broadcast the stock price change to all connected clients.</span></span>

<span data-ttu-id="39ab7-203">`_updatingStockPrices` 플래그는 [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) 로 지정 되어 스레드로부터 안전 하 게 보호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-203">The `_updatingStockPrices` flag designated [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) to make sure it is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

<span data-ttu-id="39ab7-204">실제 응용 프로그램에서 `TryUpdateStockPrice` 메서드는 웹 서비스를 호출 하 여 가격을 조회 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-204">In a real application, the `TryUpdateStockPrice` method would call a web service to look up the price.</span></span> <span data-ttu-id="39ab7-205">이 코드에서 앱은 난수 생성기를 사용 하 여 임의로 변경을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-205">In this code, the app uses a random number generator to make changes randomly.</span></span>

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a><span data-ttu-id="39ab7-206">StockTicker 클래스가 클라이언트에 브로드캐스트할 수 있도록 SignalR 컨텍스트 가져오기</span><span class="sxs-lookup"><span data-stu-id="39ab7-206">Getting the SignalR context so that the StockTicker class can broadcast to clients</span></span>

<span data-ttu-id="39ab7-207">가격 변경 내용은 `StockTicker` 개체에서 발생 하므로 연결 된 모든 클라이언트에서 `updateStockPrice` 메서드를 호출 해야 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-207">Because the price changes originate here in the `StockTicker` object, it's the object that needs to call an `updateStockPrice` method on all connected clients.</span></span> <span data-ttu-id="39ab7-208">`Hub` 클래스에는 클라이언트 메서드를 호출 하기 위한 API가 있지만 `StockTicker`는 `Hub` 클래스에서 파생 되지 않으며 `Hub` 개체에 대 한 참조가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-208">In a `Hub` class, you have an API for calling client methods, but `StockTicker` doesn't derive from the `Hub` class and doesn't have a reference to any `Hub` object.</span></span> <span data-ttu-id="39ab7-209">연결 된 클라이언트에 브로드캐스트하는 `StockTicker` 클래스는 `StockTickerHub` 클래스에 대 한 SignalR context 인스턴스를 가져온 다음이를 사용 하 여 클라이언트에서 메서드를 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-209">To broadcast to connected clients, the `StockTicker` class has to get the SignalR context instance for the `StockTickerHub` class and use that to call methods on clients.</span></span>

<span data-ttu-id="39ab7-210">이 코드는 singleton 클래스 인스턴스를 만들 때 SignalR 컨텍스트에 대 한 참조를 가져오고 생성자에 대 한 참조를 전달 하며 생성자는이를 `Clients` 속성에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-210">The code gets a reference to the SignalR context when it creates the singleton class instance, passes that reference to the constructor, and the constructor puts it in the `Clients` property.</span></span>

<span data-ttu-id="39ab7-211">컨텍스트를 한 번만 가져오려고 하는 두 가지 이유는 다음과 같습니다. 컨텍스트 가져오기 작업은 비용이 많이 들고, 한 번 가져오면 앱이 클라이언트에 전송 되는 메시지의 순서를 유지 하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-211">There are two reasons why you want to get the context only once: getting the context is an expensive task, and getting it once makes sure the app preserves the intended order of messages sent to the clients.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

<span data-ttu-id="39ab7-212">컨텍스트의 `Clients` 속성을 가져와 `StockTickerClient` 속성에 배치 하면 `Hub` 클래스와 동일한 것으로 보이는 클라이언트 메서드를 호출 하는 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-212">Getting the `Clients` property of the context and putting it in the `StockTickerClient` property lets you write code to call client methods that looks the same as it would in a `Hub` class.</span></span> <span data-ttu-id="39ab7-213">예를 들어 모든 클라이언트에 브로드캐스트하는 `Clients.All.updateStockPrice(stock)`작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-213">For instance, to broadcast to all clients you can write `Clients.All.updateStockPrice(stock)`.</span></span>

<span data-ttu-id="39ab7-214">`BroadcastStockPrice`에서 호출 하는 `updateStockPrice` 메서드가 아직 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-214">The `updateStockPrice` method that you're calling in `BroadcastStockPrice` doesn't exist yet.</span></span> <span data-ttu-id="39ab7-215">나중에 클라이언트에서 실행 되는 코드를 작성할 때 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-215">You'll add it later when you write code that runs on the client.</span></span> <span data-ttu-id="39ab7-216">`Clients.All` 동적 이기 때문에 `updateStockPrice`를 참조할 수 있습니다. 즉, 앱이 런타임에 식을 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-216">You can refer to `updateStockPrice` here because `Clients.All` is dynamic, which means the app will evaluate the expression at runtime.</span></span> <span data-ttu-id="39ab7-217">이 메서드 호출이 실행 되 면 SignalR는 메서드 이름 및 매개 변수 값을 클라이언트에 전송 하 고, 클라이언트에 `updateStockPrice`라는 메서드가 있으면 앱은 해당 메서드를 호출 하 고 매개 변수 값을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-217">When this method call executes, SignalR will send the method name and the parameter value to the client, and if the client has a method named `updateStockPrice`, the app will call that method and pass the parameter value to it.</span></span>

<span data-ttu-id="39ab7-218">`Clients.All`는 모든 클라이언트에 보내기를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-218">`Clients.All` means send to all clients.</span></span> <span data-ttu-id="39ab7-219">SignalR는 보낼 클라이언트 또는 클라이언트 그룹을 지정 하는 다른 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-219">SignalR gives you other options to specify which clients or groups of clients to send to.</span></span> <span data-ttu-id="39ab7-220">자세한 내용은 [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="39ab7-220">For more information, see [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span></span>

### <a name="register-the-signalr-route"></a><span data-ttu-id="39ab7-221">SignalR 경로 등록</span><span class="sxs-lookup"><span data-stu-id="39ab7-221">Register the SignalR route</span></span>

<span data-ttu-id="39ab7-222">서버에서 가로채서 SignalR에 지시할 URL을 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-222">The server needs to know which URL to intercept and direct to SignalR.</span></span> <span data-ttu-id="39ab7-223">이렇게 하려면 OWIN startup 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-223">To do that, add an OWIN startup class:</span></span>

1. <span data-ttu-id="39ab7-224">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가** > **새 항목**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-224">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="39ab7-225">**새 항목 추가-SignalR. StockTicker** **설치** > **Visual C#**  > **Web** 을 선택한 다음 **OWIN 시작 클래스**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-225">In **Add New Item - SignalR.StockTicker** select **Installed** > **Visual C#** > **Web** and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="39ab7-226">클래스 이름을 *시작* 으로 하 고 **확인**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-226">Name the class *Startup* and select **OK**.</span></span>

1. <span data-ttu-id="39ab7-227">*Startup.cs* 파일의 기본 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-227">Replace the default code in the *Startup.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

<span data-ttu-id="39ab7-228">이제 서버 코드를 설정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-228">You have now finished setting up the server code.</span></span> <span data-ttu-id="39ab7-229">다음 섹션에서는 클라이언트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-229">In the next section, you'll set up the client.</span></span>

## <a name="set-up-the-client-code"></a><span data-ttu-id="39ab7-230">클라이언트 코드 설정</span><span class="sxs-lookup"><span data-stu-id="39ab7-230">Set up the client code</span></span>

<span data-ttu-id="39ab7-231">이 섹션에서는 클라이언트에서 실행 되는 코드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-231">In this section, you set up the code that runs on the client.</span></span>

### <a name="create-the-html-page-and-javascript-file"></a><span data-ttu-id="39ab7-232">HTML 페이지 및 JavaScript 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="39ab7-232">Create the HTML page and JavaScript file</span></span>

<span data-ttu-id="39ab7-233">HTML 페이지에 데이터가 표시 되 고 JavaScript 파일이 데이터를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-233">The HTML page will display the data and the JavaScript file will organize the data.</span></span>

#### <a name="create-stocktickerhtml"></a><span data-ttu-id="39ab7-234">StockTicker 만들기</span><span class="sxs-lookup"><span data-stu-id="39ab7-234">Create StockTicker.html</span></span>

<span data-ttu-id="39ab7-235">먼저 HTML 클라이언트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-235">First, you'll add the HTML client.</span></span>

1. <span data-ttu-id="39ab7-236">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 > **HTML 페이지** **추가** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-236">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="39ab7-237">파일 이름을 *StockTicker* 로 선택 하 고 **확인을**선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-237">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="39ab7-238">*StockTicker* 파일의 기본 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-238">Replace the default code in the *StockTicker.html* file with this code:</span></span>

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    <span data-ttu-id="39ab7-239">HTML은 5 개의 열, 머리글 행 및 5 개 열 전체에 걸쳐 있는 단일 셀을 포함 하는 데이터 행을 포함 하는 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-239">The HTML creates a table with five columns, a header row, and a data row with a single cell that spans all five columns.</span></span> <span data-ttu-id="39ab7-240">데이터 행에 "로드 중 ..."이 표시 됩니다. 앱이 시작 되는 일시적입니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-240">The data row shows "loading..." momentarily when the app starts.</span></span> <span data-ttu-id="39ab7-241">JavaScript 코드는 해당 행을 제거 하 고 서버에서 검색 된 주식 데이터를 사용 하 여 해당 행을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-241">JavaScript code will remove that row and add in its place rows with stock data retrieved from the server.</span></span>

    <span data-ttu-id="39ab7-242">스크립트 태그는 다음을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-242">The script tags specify:</span></span>

    * <span data-ttu-id="39ab7-243">JQuery 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-243">The jQuery script file.</span></span>

    * <span data-ttu-id="39ab7-244">SignalR core 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-244">The SignalR core script file.</span></span>

    * <span data-ttu-id="39ab7-245">SignalR 프록시 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-245">The SignalR proxies script file.</span></span>

    * <span data-ttu-id="39ab7-246">나중에 만들 StockTicker 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-246">A StockTicker script file that you'll create later.</span></span>

    <span data-ttu-id="39ab7-247">앱은 SignalR 프록시 스크립트 파일을 동적으로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-247">The app dynamically generates the SignalR proxies script file.</span></span> <span data-ttu-id="39ab7-248">"/Signalr/hubs" URL을 지정 하 고 허브 클래스 (이 경우 `StockTickerHub.GetAllStocks`의 메서드에 대 한 프록시 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-248">It specifies the "/signalr/hubs" URL and defines proxy methods for the methods on the Hub class, in this case, for `StockTickerHub.GetAllStocks`.</span></span> <span data-ttu-id="39ab7-249">원한다 면 [SignalR 유틸리티](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)를 사용 하 여이 JavaScript 파일을 수동으로 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-249">If you prefer, you can generate this JavaScript file manually by using [SignalR Utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/).</span></span> <span data-ttu-id="39ab7-250">`MapHubs` 메서드 호출에서 동적 파일 생성을 사용 하지 않도록 설정 하는 것을 잊지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="39ab7-250">Don't forget to disable dynamic file creation in the `MapHubs` method call.</span></span>

1. <span data-ttu-id="39ab7-251">**솔루션 탐색기**에서 **스크립트**를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-251">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="39ab7-252">JQuery 및 SignalR에 대 한 스크립트 라이브러리는 프로젝트에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-252">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="39ab7-253">패키지 관리자가 SignalR 스크립트의 최신 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-253">The package manager will install a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="39ab7-254">프로젝트의 스크립트 파일 버전에 해당 하는 코드 블록의 스크립트 참조를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-254">Update the script references in the code block to correspond to the versions of the script files in the project.</span></span>

1. <span data-ttu-id="39ab7-255">**솔루션 탐색기**에서 *StockTicker*을 마우스 오른쪽 단추로 클릭 한 다음 **시작 페이지로 설정**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-255">In **Solution Explorer**, right-click *StockTicker.html*, and then select **Set as Start Page**.</span></span>

#### <a name="create-stocktickerjs"></a><span data-ttu-id="39ab7-256">StockTicker 만들기</span><span class="sxs-lookup"><span data-stu-id="39ab7-256">Create StockTicker.js</span></span>

<span data-ttu-id="39ab7-257">이제 JavaScript 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-257">Now create the JavaScript file.</span></span>

1. <span data-ttu-id="39ab7-258">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 > **JavaScript 파일** **추가** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-258">In **Solution Explorer**, right-click the project and select **Add** > **JavaScript File**.</span></span>

1. <span data-ttu-id="39ab7-259">파일 이름을 *StockTicker* 로 선택 하 고 **확인을**선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-259">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="39ab7-260">*StockTicker* 파일에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-260">Add this code to the *StockTicker.js* file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a><span data-ttu-id="39ab7-261">클라이언트 코드 검사</span><span class="sxs-lookup"><span data-stu-id="39ab7-261">Examine the client code</span></span>

<span data-ttu-id="39ab7-262">클라이언트 코드를 살펴보면 클라이언트 코드가 서버 코드와 상호 작용 하 여 앱이 작동 하도록 하는 방법을 배우는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-262">If you examine the client code, it will help you learn how the client code interacts with the server code to make the app work.</span></span>

#### <a name="starting-the-connection"></a><span data-ttu-id="39ab7-263">연결 시작</span><span class="sxs-lookup"><span data-stu-id="39ab7-263">Starting the connection</span></span>

<span data-ttu-id="39ab7-264">`$.connection` SignalR 프록시를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-264">`$.connection` refers to the SignalR proxies.</span></span> <span data-ttu-id="39ab7-265">이 코드는 `StockTickerHub` 클래스에 대 한 프록시에 대 한 참조를 가져와 `ticker` 변수에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-265">The code gets a reference to the proxy for the `StockTickerHub` class and puts it in the `ticker` variable.</span></span> <span data-ttu-id="39ab7-266">프록시 이름은 `HubName` 특성에 의해 설정 된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-266">The proxy name is the name that was set by the `HubName` attribute:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

<span data-ttu-id="39ab7-267">모든 변수와 함수를 정의한 후 파일의 마지막 코드 줄에서는 SignalR `start` 함수를 호출 하 여 SignalR 연결을 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-267">After you define all the variables and functions, the last line of code in the file initializes the SignalR connection by calling the SignalR `start` function.</span></span> <span data-ttu-id="39ab7-268">`start` 함수는 비동기적으로 실행 되 고 [JQuery 지연 된 개체](http://api.jquery.com/category/deferred-object/)를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-268">The `start` function executes asynchronously and returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/).</span></span> <span data-ttu-id="39ab7-269">Done 함수를 호출 하 여 앱이 비동기 작업을 완료할 때 호출할 함수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-269">You can call the done function to specify the function to call when the app finishes the asynchronous action.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a><span data-ttu-id="39ab7-270">모든 주식 가져오기</span><span class="sxs-lookup"><span data-stu-id="39ab7-270">Getting all the stocks</span></span>

<span data-ttu-id="39ab7-271">`init` 함수는 서버에서 `getAllStocks` 함수를 호출 하 고 서버에서 반환 하는 정보를 사용 하 여 스톡 테이블을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-271">The `init` function calls the `getAllStocks` function on the server and uses the information that the server returns to update the stock table.</span></span> <span data-ttu-id="39ab7-272">서버에서 메서드 이름이 파스칼식 대/소문자를 사용 하는 경우에도 기본적으로 클라이언트에서 camelCasing를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-272">Notice that, by default, you have to use camelCasing on the client even though the method name is pascal-cased on the server.</span></span> <span data-ttu-id="39ab7-273">CamelCasing 규칙은 개체가 아닌 메서드에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-273">The camelCasing rule only applies to methods, not objects.</span></span> <span data-ttu-id="39ab7-274">예를 들어 `stock.symbol` 또는 `stock.price`아닌 `stock.Symbol` 및 `stock.Price`을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-274">For example, you refer to `stock.Symbol` and `stock.Price`, not `stock.symbol` or `stock.price`.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

<span data-ttu-id="39ab7-275">`init` 메서드에서 앱은 `formatStock`를 호출 하 여 서버에서 받은 각 스톡 개체에 대 한 HTML을 만든 다음 `stock` 개체의 속성에 대 한 서식을 지정 하 고 `supplant`를 호출 하 여 `rowTemplate` 변수의 자리 표시자를 `stock` 개체 속성 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-275">In the `init` method, the app creates HTML for a table row for each stock object received from the server by calling `formatStock` to format properties of the `stock` object, and then by calling `supplant` to replace placeholders in the `rowTemplate` variable with the `stock` object property values.</span></span> <span data-ttu-id="39ab7-276">그러면 결과 HTML이 스톡 테이블에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-276">The resulting HTML is then appended to the stock table.</span></span>

> [!NOTE]
> <span data-ttu-id="39ab7-277">비동기 `start` 함수가 완료 된 후 실행 되는 `callback` 함수로에 전달 하 여 `init`를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-277">You call `init` by passing it in as a `callback` function that executes after the asynchronous `start` function finishes.</span></span> <span data-ttu-id="39ab7-278">`start`를 호출한 후 별도의 JavaScript 문으로 `init`를 호출한 경우 함수는 시작 함수가 연결 설정을 완료할 때까지 기다리지 않고 즉시 실행 되기 때문에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-278">If you called `init` as a separate JavaScript statement after calling `start`, the function would fail because it would run immediately without waiting for the start function to finish establishing the connection.</span></span> <span data-ttu-id="39ab7-279">이 경우 `init` 함수는 앱이 서버 연결을 설정 하기 전에 `getAllStocks` 함수를 호출 하려고 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-279">In that case, the `init` function would try to call the `getAllStocks` function before the app establishes a server connection.</span></span>

#### <a name="getting-updated-stock-prices"></a><span data-ttu-id="39ab7-280">업데이트 된 주식 가격</span><span class="sxs-lookup"><span data-stu-id="39ab7-280">Getting updated stock prices</span></span>

<span data-ttu-id="39ab7-281">서버에서 주식 시세를 변경 하면 연결 된 클라이언트에서 `updateStockPrice`를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-281">When the server changes a stock's price, it calls the `updateStockPrice` on connected clients.</span></span> <span data-ttu-id="39ab7-282">앱은 `stockTicker` 프록시의 client 속성에 함수를 추가 하 여 서버에서 호출할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-282">The app adds the function to the client property of the `stockTicker` proxy to make it available to calls from the server.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

<span data-ttu-id="39ab7-283">`updateStockPrice` 함수는 `init` 함수와 동일한 방식으로 서버에서 받은 스톡 개체의 형식을 테이블 행으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-283">The `updateStockPrice` function formats a stock object received from the server into a table row the same way as in the `init` function.</span></span> <span data-ttu-id="39ab7-284">테이블에 행을 추가 하는 대신 테이블에서 주식의 현재 행을 찾아 해당 행을 새 행으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-284">Instead of appending the row to the table, it finds the stock's current row in the table and replaces that row with the new one.</span></span>

## <a name="test-the-application"></a><span data-ttu-id="39ab7-285">애플리케이션 테스트</span><span class="sxs-lookup"><span data-stu-id="39ab7-285">Test the application</span></span>

<span data-ttu-id="39ab7-286">앱이 작동 하는지 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-286">You can test the app to make sure it's working.</span></span> <span data-ttu-id="39ab7-287">모든 브라우저 창에서 주식 가격이 변동 인 라이브 재고 테이블이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-287">You'll see all browser windows display the live stock table with stock prices fluctuating.</span></span>

1. <span data-ttu-id="39ab7-288">도구 모음에서 **스크립트 디버깅** 을 사용 하도록 설정 하 고 재생 단추를 선택 하 여 디버그 모드에서 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-288">In the toolbar, turn on **Script Debugging** and then select the play button to run the app in Debug mode.</span></span>

    ![디버깅 모드를 켜고 재생을 선택 하는 사용자의 스크린샷](tutorial-server-broadcast-with-signalr/_static/image4.png)

    <span data-ttu-id="39ab7-290">**라이브 재고 테이블**을 표시 하는 브라우저 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-290">A browser window will open displaying the **Live Stock Table**.</span></span> <span data-ttu-id="39ab7-291">Stock 테이블에는 처음에 "로드 중 ..."이 표시 됩니다. 그런 다음, 짧은 시간 후에 앱은 초기 주식 데이터를 표시 한 다음 주가 변경 되기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-291">The stock table initially shows the "loading..." line, then, after a short time, the app shows the initial stock data, and then the stock prices start to change.</span></span>

1. <span data-ttu-id="39ab7-292">브라우저에서 URL을 복사 하 여 다른 두 브라우저를 열고 Url을 주소 표시줄에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-292">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

    <span data-ttu-id="39ab7-293">초기 주식 표시는 첫 번째 브라우저와 동일 하며 변경 내용이 동시에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-293">The initial stock display is the same as the first browser and changes happen simultaneously.</span></span>

1. <span data-ttu-id="39ab7-294">모든 브라우저를 닫고 새 브라우저를 연 다음 동일한 URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-294">Close all browsers, open a new browser, and go to the same URL.</span></span>

    <span data-ttu-id="39ab7-295">StockTicker singleton 개체가 서버에서 계속 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-295">The StockTicker singleton object continued to run in the server.</span></span> <span data-ttu-id="39ab7-296">**라이브 스톡 테이블** 은 주가 계속 변경 된 것을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-296">The **Live Stock Table** shows that the stocks have continued to change.</span></span> <span data-ttu-id="39ab7-297">변경 수치가 0 인 초기 테이블은 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-297">You don't see the initial table with zero change figures.</span></span>

1. <span data-ttu-id="39ab7-298">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-298">Close the browser.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="39ab7-299">로깅 사용</span><span class="sxs-lookup"><span data-stu-id="39ab7-299">Enable logging</span></span>

<span data-ttu-id="39ab7-300">SignalR에는 문제 해결을 지원 하기 위해 클라이언트에서 사용할 수 있는 기본 제공 로깅 함수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-300">SignalR has a built-in logging function that you can enable on the client to aid in troubleshooting.</span></span> <span data-ttu-id="39ab7-301">이 섹션에서는 로깅을 사용 하도록 설정 하 고 SignalR에서 사용 하는 전송 방법에 대 한 로그를 표시 하는 예제를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-301">In this section, you enable logging and see examples that show how logs tell you which of the following transport methods SignalR is using:</span></span>

* <span data-ttu-id="39ab7-302">[Websocket](http://en.wikipedia.org/wiki/WebSocket)-IIS 8 및 현재 브라우저에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-302">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), supported by IIS 8 and current browsers.</span></span>

* <span data-ttu-id="39ab7-303">Internet Explorer 이외의 브라우저에서 지원 되는 [서버에서 보낸 이벤트](http://en.wikipedia.org/wiki/Server-sent_events)</span><span class="sxs-lookup"><span data-stu-id="39ab7-303">[Server-sent events](http://en.wikipedia.org/wiki/Server-sent_events), supported by browsers other than Internet Explorer.</span></span>

* <span data-ttu-id="39ab7-304">[영구적 프레임](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe)으로, Internet Explorer에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-304">[Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), supported by Internet Explorer.</span></span>

* <span data-ttu-id="39ab7-305">모든 브라우저에서 지원 되는 [Ajax 긴 폴링](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling).</span><span class="sxs-lookup"><span data-stu-id="39ab7-305">[Ajax long polling](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), supported by all browsers.</span></span>

<span data-ttu-id="39ab7-306">SignalR는 지정 된 모든 연결에 대해 서버와 클라이언트가 지 원하는 최상의 전송 방법을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-306">For any given connection, SignalR chooses the best transport method that both the server and the client support.</span></span>

1. <span data-ttu-id="39ab7-307">*StockTicker*를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-307">Open *StockTicker.js*.</span></span>

1. <span data-ttu-id="39ab7-308">이 강조 표시 된 코드 줄을 추가 하 여 파일 끝에서 연결을 초기화 하는 코드 바로 앞에서 로깅을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-308">Add this highlighted line of code to enable logging immediately before the code that initializes the connection at the end of the file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. <span data-ttu-id="39ab7-309">**F5** 키를 눌러 프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-309">Press **F5** to run the project.</span></span>

1. <span data-ttu-id="39ab7-310">브라우저의 개발자 도구 창을 열고 콘솔을 선택 하 여 로그를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-310">Open your browser's developer tools window, and select the Console to see the logs.</span></span> <span data-ttu-id="39ab7-311">새 연결에 대 한 전송 방법을 협상 하는 SignalR의 로그를 확인 하려면 페이지를 새로 고쳐야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-311">You might have to refresh the page to see the logs of SignalR negotiating the transport method for a new connection.</span></span>

    * <span data-ttu-id="39ab7-312">Windows 8 (IIS 8)에서 Internet Explorer 10을 실행 하는 경우 전송 방법은 **websocket**입니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-312">If you're running Internet Explorer 10 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

    * <span data-ttu-id="39ab7-313">Windows 7 (IIS 7.5)에서 Internet Explorer 10을 실행 하는 경우 전송 방법은 **iframe**입니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-313">If you're running Internet Explorer 10 on Windows 7 (IIS 7.5), the transport method is **iframe**.</span></span>

    * <span data-ttu-id="39ab7-314">Windows 8 (IIS 8)에서 Firefox 19를 실행 하는 경우 전송 방법은 **websocket**입니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-314">If you're running Firefox 19 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

        > [!TIP]
        > <span data-ttu-id="39ab7-315">Firefox에서 Firebug 추가 기능을 설치 하 여 콘솔 창을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-315">In Firefox, install the Firebug add-in to get a Console window.</span></span>

    * <span data-ttu-id="39ab7-316">Windows 7 (IIS 7.5)에서 Firefox 19를 실행 하는 경우 전송 방법은 서버에서 **보낸** 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-316">If you're running Firefox 19 on Windows 7 (IIS 7.5), the transport method is **server-sent** events.</span></span>

## <a name="install-the-stockticker-sample"></a><span data-ttu-id="39ab7-317">StockTicker 샘플 설치</span><span class="sxs-lookup"><span data-stu-id="39ab7-317">Install the StockTicker sample</span></span>

<span data-ttu-id="39ab7-318">[SignalR](http://nuget.org/packages/microsoft.aspnet.signalr.sample) 는 StockTicker 응용 프로그램을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-318">The [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) installs the StockTicker application.</span></span> <span data-ttu-id="39ab7-319">NuGet 패키지에는 처음부터 만든 단순화 된 버전 보다 더 많은 기능이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-319">The NuGet package includes more features than the simplified version that you created from scratch.</span></span> <span data-ttu-id="39ab7-320">자습서의이 섹션에서는 NuGet 패키지를 설치 하 고 새 기능 및이를 구현 하는 코드를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-320">In this section of the tutorial, you install the NuGet package and review the new features and the code that implements them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="39ab7-321">이 자습서의 이전 단계를 수행 하지 않고 패키지를 설치 하는 경우 프로젝트에 OWIN startup 클래스를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-321">If you install the package without performing the earlier steps of this tutorial, you must add an OWIN startup class to your project.</span></span> <span data-ttu-id="39ab7-322">NuGet 패키지에 대 한이 readme.txt 파일은이 단계를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-322">This readme.txt file for the NuGet package explains this step.</span></span>

### <a name="install-the-signalrsample-nuget-package"></a><span data-ttu-id="39ab7-323">SignalR NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-323">Install the SignalR.Sample NuGet package</span></span>

1. <span data-ttu-id="39ab7-324">**솔루션 탐색기**에서 프로젝트의 이름을 마우스 오른쪽 단추를 클릭하고 **NuGet 패키지 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-324">In **Solution Explorer**, right-click the project and select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="39ab7-325">**NuGet 패키지 관리자: SignalR. StockTicker**에서 **찾아보기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-325">In **NuGet Package manager: SignalR.StockTicker**, select **Browse**.</span></span>

1. <span data-ttu-id="39ab7-326">**패키지 원본**에서 **nuget.org**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-326">From **Package source**, select **nuget.org**.</span></span>

1. <span data-ttu-id="39ab7-327">검색 상자에 *SignalR* 를 입력 하 고 **SignalR** > **설치**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-327">Enter *SignalR.Sample* in the search box and select **Microsoft.AspNet.SignalR.Sample** > **Install**.</span></span>

1. <span data-ttu-id="39ab7-328">**솔루션 탐색기**에서 *SignalR* 폴더를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-328">In **Solution Explorer**, expand the *SignalR.Sample* folder.</span></span>

    <span data-ttu-id="39ab7-329">SignalR 패키지를 설치 하면 폴더와 해당 내용이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-329">Installing the SignalR.Sample package created the folder and its contents.</span></span>

1. <span data-ttu-id="39ab7-330">*SignalR* 폴더에서 *StockTicker*를 마우스 오른쪽 단추로 클릭 한 다음 **시작 페이지로 설정**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-330">In the *SignalR.Sample* folder, right-click *StockTicker.html*, and then select **Set As Start Page**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="39ab7-331">SignalR NuGet 패키지를 설치 하면 *Scripts* 폴더에 있는 jQuery 버전이 변경 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-331">Installing The SignalR.Sample NuGet package might change the version of jQuery that you have in your *Scripts* folder.</span></span> <span data-ttu-id="39ab7-332">패키지가 *SignalR* 폴더에 설치 하는 새 *StockTicker* 파일은 패키지가 설치 하는 jQuery 버전과 동기화 되지만 원래 *StockTicker* 파일을 다시 실행 하려는 경우에는 먼저 스크립트 태그에서 jquery 참조를 업데이트 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-332">The new *StockTicker.html* file that the package installs in the *SignalR.Sample* folder will be in sync with the jQuery version that the package installs, but if you want to run your original *StockTicker.html* file again, you might have to update the jQuery reference in the script tag first.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="39ab7-333">애플리케이션 실행</span><span class="sxs-lookup"><span data-stu-id="39ab7-333">Run the application</span></span>

 <span data-ttu-id="39ab7-334">첫 번째 앱에서 살펴본 테이블에는 유용한 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-334">The table that you saw in the first app had useful features.</span></span> <span data-ttu-id="39ab7-335">전체 주식 시세 응용 프로그램에는 새 기능이 표시 됩니다. 가로 스크롤 창에서는 주식 데이터 및 주식으로 색을 변경 하는 주가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-335">The full stock ticker application shows new features: a horizontally scrolling window that shows the stock data and stocks that change color as they rise and fall.</span></span>

1. <span data-ttu-id="39ab7-336">**F5** 키를 눌러 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-336">Press **F5** to run the app.</span></span>

     <span data-ttu-id="39ab7-337">앱을 처음으로 실행 하는 경우 "market"은 "닫힘" 이며, 스크롤하지 않는 정적 테이블과 표시기 창이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-337">When you run the app for the first time, the "market" is "closed" and you see a static table and a ticker window that isn't scrolling.</span></span>

1. <span data-ttu-id="39ab7-338">**시장 열기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-338">Select **Open Market**.</span></span>

    ![라이브 표시기의 스크린샷](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * <span data-ttu-id="39ab7-340">**라이브 주식 시세 표시기** 상자를 가로로 스크롤하면 서버에서 정기적으로 주식 시세 변경을 정기적으로 브로드캐스트 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-340">The **Live Stock Ticker** box starts to scroll horizontally, and the server starts to periodically broadcast stock price changes on a random basis.</span></span>

    * <span data-ttu-id="39ab7-341">주가 변경 될 때마다 앱은 **Live Stock 테이블과** **라이브 주식 시세 표시기**를 모두 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-341">Each time a stock price changes, the app updates both the **Live Stock Table** and the **Live Stock Ticker**.</span></span>

    * <span data-ttu-id="39ab7-342">주가 변화 하는 경우 앱은 녹색 배경의 재고를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-342">When a stock's price change is positive, the app shows the stock with a green background.</span></span>

    * <span data-ttu-id="39ab7-343">변경이 음수 이면 앱은 빨간색 배경의 재고를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-343">When the change is negative, the app shows the stock with a red background.</span></span>

1. <span data-ttu-id="39ab7-344">**시장 종결**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-344">Select **Close Market**.</span></span>

    * <span data-ttu-id="39ab7-345">테이블 업데이트가 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-345">The table updates stop.</span></span>

    * <span data-ttu-id="39ab7-346">표시기가 스크롤을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-346">The ticker stops scrolling.</span></span>

1. <span data-ttu-id="39ab7-347">**다시 설정**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-347">Select **Reset**.</span></span>

    * <span data-ttu-id="39ab7-348">모든 재고 데이터를 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-348">All stock data is reset.</span></span>

    * <span data-ttu-id="39ab7-349">앱은 가격 변경이 시작 되기 전에 초기 상태를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-349">The app restores the initial state before price changes started.</span></span>

1. <span data-ttu-id="39ab7-350">브라우저에서 URL을 복사 하 여 다른 두 브라우저를 열고 Url을 주소 표시줄에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-350">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="39ab7-351">각 브라우저에서 동시에 동일한 데이터를 동적으로 업데이트 하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-351">You see the same data dynamically updated at the same time in each browser.</span></span>

1. <span data-ttu-id="39ab7-352">컨트롤 중 하나를 선택 하면 모든 브라우저가 동시에 동일한 방식으로 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-352">When you select any of the controls, all browsers respond the same way at the same time.</span></span>

### <a name="live-stock-ticker-display"></a><span data-ttu-id="39ab7-353">라이브 주식 종목 표시</span><span class="sxs-lookup"><span data-stu-id="39ab7-353">Live Stock Ticker display</span></span>

<span data-ttu-id="39ab7-354">**라이브 주식 시세** 표시는 CSS 스타일을 통해 한 줄로 형식이 지정 된 `<div>` 요소의 순서가 지정 되지 않은 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-354">The **Live Stock Ticker** display is an unordered list in a `<div>` element formatted into a single line by CSS styles.</span></span> <span data-ttu-id="39ab7-355">앱은 `<li>` 템플릿 문자열에서 자리 표시자를 바꾸고 `<li>` 요소를 `<ul>` 요소에 동적으로 추가 하 여 테이블과 동일한 방식으로 종목을 초기화 하 고 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-355">The app initializes and updates the ticker the same way as the table: by replacing placeholders in an `<li>` template string and dynamically adding the `<li>` elements to the `<ul>` element.</span></span> <span data-ttu-id="39ab7-356">앱은 jQuery `animate` 함수를 사용 하 여 스크롤을 포함 하 여 `<div>`내에서 순서가 지정 되지 않은 목록의 왼쪽 여백을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-356">The app includes  scrolling by using the jQuery `animate` function to vary the margin-left of the unordered list within the `<div>`.</span></span>

#### <a name="signalrsample-stocktickerhtml"></a><span data-ttu-id="39ab7-357">SignalR StockTicker</span><span class="sxs-lookup"><span data-stu-id="39ab7-357">SignalR.Sample StockTicker.html</span></span>

<span data-ttu-id="39ab7-358">주식 시세 HTML 코드:</span><span class="sxs-lookup"><span data-stu-id="39ab7-358">The stock ticker HTML code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a><span data-ttu-id="39ab7-359">SignalR StockTicker</span><span class="sxs-lookup"><span data-stu-id="39ab7-359">SignalR.Sample StockTicker.css</span></span>

<span data-ttu-id="39ab7-360">주식 시세 CSS 코드:</span><span class="sxs-lookup"><span data-stu-id="39ab7-360">The stock ticker CSS code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a><span data-ttu-id="39ab7-361">SignalR SignalR. StockTicker</span><span class="sxs-lookup"><span data-stu-id="39ab7-361">SignalR.Sample SignalR.StockTicker.js</span></span>

<span data-ttu-id="39ab7-362">스크롤할 수 있도록 하는 jQuery 코드:</span><span class="sxs-lookup"><span data-stu-id="39ab7-362">The jQuery code that makes it scroll:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a><span data-ttu-id="39ab7-363">클라이언트에서 호출할 수 있는 서버에 대 한 추가 메서드</span><span class="sxs-lookup"><span data-stu-id="39ab7-363">Additional methods on the server that the client can call</span></span>

<span data-ttu-id="39ab7-364">앱에 유연성을 추가 하기 위해 앱에서 호출할 수 있는 추가 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-364">To add flexibility to the app, there are additional methods the app can call.</span></span>

#### <a name="signalrsample-stocktickerhubcs"></a><span data-ttu-id="39ab7-365">SignalR StockTickerHub.cs</span><span class="sxs-lookup"><span data-stu-id="39ab7-365">SignalR.Sample StockTickerHub.cs</span></span>

<span data-ttu-id="39ab7-366">`StockTickerHub` 클래스는 클라이언트에서 호출할 수 있는 다음 네 가지 메서드를 추가로 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-366">The `StockTickerHub` class defines four additional methods that the client can call:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

<span data-ttu-id="39ab7-367">앱은 페이지 맨 위에 있는 단추에 대 한 응답으로 `OpenMarket`, `CloseMarket`및 `Reset`를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-367">The app calls `OpenMarket`, `CloseMarket`, and `Reset` in response to the buttons at the top of the page.</span></span> <span data-ttu-id="39ab7-368">모든 클라이언트에 즉시 전파 되는 상태 변경을 트리거하는 한 클라이언트의 패턴을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-368">They demonstrate the pattern of one client triggering a change in state immediately propagated to all clients.</span></span> <span data-ttu-id="39ab7-369">이러한 각 메서드는 시장 상태를 변경 하 고 새 상태를 브로드캐스팅하는 `StockTicker` 클래스의 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-369">Each of these methods calls a method in the `StockTicker` class that causes the market state change and then broadcasts the new state.</span></span>

#### <a name="signalrsample-stocktickercs"></a><span data-ttu-id="39ab7-370">SignalR StockTicker.cs</span><span class="sxs-lookup"><span data-stu-id="39ab7-370">SignalR.Sample StockTicker.cs</span></span>

<span data-ttu-id="39ab7-371">`StockTicker` 클래스에서 앱은 `MarketState` 열거형 값을 반환 하는 `MarketState` 속성을 사용 하 여 시장의 상태를 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-371">In the `StockTicker` class, the app maintains the state of the market with a `MarketState` property that returns a `MarketState` enum value:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

<span data-ttu-id="39ab7-372">`StockTicker` 클래스는 스레드로부터 안전 해야 하므로 시장 상태를 변경 하는 각 메서드는 잠금 블록 내에서이를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-372">Each of the methods that change the market state do so inside a lock block because the `StockTicker` class has to be thread-safe:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

<span data-ttu-id="39ab7-373">이 코드가 스레드로부터 안전 하 게 보호 되도록 하기 위해 `volatile`지정 된 `MarketState` 속성을 지 원하는 `_marketState` 필드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-373">To make sure this code is thread-safe, the `_marketState` field that backs the `MarketState` property designated `volatile`:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

<span data-ttu-id="39ab7-374">`BroadcastMarketStateChange` 및 `BroadcastMarketReset` 메서드는 클라이언트에 정의 된 다른 메서드를 호출 하는 경우를 제외 하 고 이미 보았던 BroadcastStockPrice 메서드와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-374">The `BroadcastMarketStateChange` and `BroadcastMarketReset` methods are similar to the BroadcastStockPrice method that you already saw, except they call different methods defined at the client:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a><span data-ttu-id="39ab7-375">서버에서 호출할 수 있는 클라이언트의 추가 함수</span><span class="sxs-lookup"><span data-stu-id="39ab7-375">Additional functions on the client that the server can call</span></span>

<span data-ttu-id="39ab7-376">이제 `updateStockPrice` 함수는 테이블 및 표시기 표시를 모두 처리 하 고 `jQuery.Color`를 사용 하 여 빨간색 및 녹색 색을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-376">The `updateStockPrice` function now handles both the table and the ticker display, and it uses `jQuery.Color` to flash red and green colors.</span></span>

<span data-ttu-id="39ab7-377">StockTicker의 새로운 함수는 시장 상태에 따라 단추를 사용 하거나 사용 하지 않도록 설정 하 고 *SignalR* 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-377">New functions in *SignalR.StockTicker.js* enable and disable the buttons based on market state.</span></span> <span data-ttu-id="39ab7-378">또한 **라이브 주식 시세 표시기** 가로 스크롤을 중지 하거나 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-378">They also stop or start the **Live Stock Ticker** horizontal scrolling.</span></span> <span data-ttu-id="39ab7-379">많은 함수가 `ticker.client`에 추가 되기 때문에 앱은 [jQuery extend 함수](http://api.jquery.com/jQuery.extend/) 를 사용 하 여 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-379">Since many functions are being added to `ticker.client`, the app uses the [jQuery extend function](http://api.jquery.com/jQuery.extend/) to add them.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a><span data-ttu-id="39ab7-380">연결을 설정한 후 추가 클라이언트 설정</span><span class="sxs-lookup"><span data-stu-id="39ab7-380">Additional client setup after establishing the connection</span></span>

<span data-ttu-id="39ab7-381">클라이언트에서 연결을 설정한 후에는 다음과 같은 몇 가지 추가 작업을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-381">After the client establishes the connection, it has some additional work to do:</span></span>

* <span data-ttu-id="39ab7-382">적절 한 `marketOpened` 또는 `marketClosed` 함수를 호출 하기 위해 시장이 열려 있는지 종결 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-382">Find out if the market is open or closed to call the appropriate `marketOpened` or `marketClosed` function.</span></span>

* <span data-ttu-id="39ab7-383">서버 메서드 호출을 단추에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-383">Attach the server method calls to the buttons.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

<span data-ttu-id="39ab7-384">서버 메서드는 앱이 연결을 설정할 때까지 단추에 연결 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-384">The server methods aren't wired up to the buttons until after the app establishes the connection.</span></span> <span data-ttu-id="39ab7-385">코드를 사용 하기 전에 서버 메서드를 호출할 수 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-385">It's so the code can't call the server methods before they're available.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="39ab7-386">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="39ab7-386">Additional resources</span></span>

<span data-ttu-id="39ab7-387">이 자습서에서는 서버에서 연결 된 모든 클라이언트로 메시지를 브로드캐스팅하는 SignalR 응용 프로그램을 프로그래밍 하는 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-387">In this tutorial you've learned how to program a SignalR application that broadcasts messages from the server to all connected clients.</span></span> <span data-ttu-id="39ab7-388">이제 모든 클라이언트의 알림에 대 한 응답으로 메시지를 정기적으로 브로드캐스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-388">Now you can broadcast messages on a periodic basis and in response to notifications from any client.</span></span> <span data-ttu-id="39ab7-389">다중 스레드 singleton 인스턴스의 개념을 사용 하 여 다중 플레이어 온라인 게임 시나리오에서 서버 상태를 유지 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-389">You can use the concept of multi-threaded singleton instance to maintain server state in multi-player online game scenarios.</span></span> <span data-ttu-id="39ab7-390">예를 들어 SignalR을 [기반으로 하는 Sho이상 r 게임](https://github.com/NTaylorMullen/ShootR)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="39ab7-390">For an example, see [the ShootR game based on SignalR](https://github.com/NTaylorMullen/ShootR).</span></span>

<span data-ttu-id="39ab7-391">피어 투 피어 통신 시나리오를 보여 주는 자습서는 [SignalR 시작](introduction-to-signalr.md) 하기 및 [SignalR를 사용 하 여 실시간 업데이트](tutorial-high-frequency-realtime-with-signalr.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="39ab7-391">For tutorials that show peer-to-peer communication scenarios, see [Getting Started with SignalR](introduction-to-signalr.md) and [Real-Time Updating with SignalR](tutorial-high-frequency-realtime-with-signalr.md).</span></span>

<span data-ttu-id="39ab7-392">SignalR에 대 한 자세한 내용은 다음 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="39ab7-392">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="39ab7-393">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="39ab7-393">ASP.NET SignalR</span></span>](../../index.md)
* [<span data-ttu-id="39ab7-394">SignalR 프로젝트</span><span class="sxs-lookup"><span data-stu-id="39ab7-394">SignalR Project</span></span>](http://signalr.net/)
* [<span data-ttu-id="39ab7-395">SignalR GitHub 및 샘플</span><span class="sxs-lookup"><span data-stu-id="39ab7-395">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)
* [<span data-ttu-id="39ab7-396">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="39ab7-396">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="39ab7-397">다음 단계</span><span class="sxs-lookup"><span data-stu-id="39ab7-397">Next steps</span></span>

<span data-ttu-id="39ab7-398">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-398">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="39ab7-399">프로젝트를 만듦</span><span class="sxs-lookup"><span data-stu-id="39ab7-399">Created the project</span></span>
> * <span data-ttu-id="39ab7-400">서버 코드 설정</span><span class="sxs-lookup"><span data-stu-id="39ab7-400">Set up the server code</span></span>
> * <span data-ttu-id="39ab7-401">서버 코드를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-401">Examined the server code</span></span>
> * <span data-ttu-id="39ab7-402">클라이언트 코드 설정</span><span class="sxs-lookup"><span data-stu-id="39ab7-402">Set up the client code</span></span>
> * <span data-ttu-id="39ab7-403">클라이언트 코드를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-403">Examined the client code</span></span>
> * <span data-ttu-id="39ab7-404">애플리케이션 테스트</span><span class="sxs-lookup"><span data-stu-id="39ab7-404">Tested the application</span></span>
> * <span data-ttu-id="39ab7-405">로깅 사용</span><span class="sxs-lookup"><span data-stu-id="39ab7-405">Enabled logging</span></span>

<span data-ttu-id="39ab7-406">ASP.NET SignalR 2를 사용 하는 실시간 웹 응용 프로그램을 만드는 방법에 대해 알아보려면 다음 문서로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ab7-406">Advance to the next article to learn how to create a real-time web application that uses ASP.NET SignalR 2.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="39ab7-407">SignalR를 사용 하 여 실시간 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="39ab7-407">Create real-time web app with SignalR</span></span>](real-time-web-applications-with-signalr.md)
