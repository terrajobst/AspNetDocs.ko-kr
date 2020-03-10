---
uid: signalr/overview/older-versions/dependency-injection
title: SignalR 1.x에서 종속성 주입 | Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/15/2013
ms.assetid: eaa206c4-edb3-487e-8fcb-54a3261fed36
msc.legacyurl: /signalr/overview/older-versions/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: de838ab6b3a299eb1e5ebeb9fa3c583478ce3e56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431543"
---
# <a name="dependency-injection-in-signalr-1x"></a><span data-ttu-id="096d2-102">SignalR 1.x에서 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="096d2-102">Dependency Injection in SignalR 1.x</span></span>

<span data-ttu-id="096d2-103">사람, [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="096d2-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="096d2-104">종속성 주입은 개체 간에 하드 코드 된 종속성을 제거 하는 방법으로, 테스트 (모의 개체 사용) 또는 런타임 동작을 변경 하 여 개체의 종속성을 쉽게 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-104">Dependency injection is a way to remove hard-coded dependencies between objects, making it easier to replace an object's dependencies, either for testing (using mock objects) or to change run-time behavior.</span></span> <span data-ttu-id="096d2-105">이 자습서에서는 SignalR hubs에서 종속성 주입을 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-105">This tutorial shows how to perform dependency injection on SignalR hubs.</span></span> <span data-ttu-id="096d2-106">또한 SignalR에서 IoC 컨테이너를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-106">It also shows how to use IoC containers with SignalR.</span></span> <span data-ttu-id="096d2-107">IoC 컨테이너는 종속성 주입을 위한 일반 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-107">An IoC container is a general framework for dependency injection.</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="096d2-108">종속성 주입 이란?</span><span class="sxs-lookup"><span data-stu-id="096d2-108">What is Dependency Injection?</span></span>

<span data-ttu-id="096d2-109">종속성 주입에 이미 익숙한 경우이 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-109">Skip this section if you are already familiar with dependency injection.</span></span>

<span data-ttu-id="096d2-110">DI ( *종속성 주입* )는 개체가 자체 종속성을 만들 책임이 없는 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-110">*Dependency injection* (DI) is a pattern where objects are not responsible for creating their own dependencies.</span></span> <span data-ttu-id="096d2-111">다음은 DI를 동기로 확인 하는 간단한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-111">Here is a simple example to motivate DI.</span></span> <span data-ttu-id="096d2-112">메시지를 기록 해야 하는 개체가 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-112">Suppose you have an object that needs to log messages.</span></span> <span data-ttu-id="096d2-113">로깅 인터페이스를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-113">You might define a logging interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="096d2-114">개체에서 메시지를 기록 하는 `ILogger`를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-114">In your object, you can create an `ILogger` to log messages:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="096d2-115">이렇게 하는 것이 좋지만 최상의 디자인은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-115">This works, but it's not the best design.</span></span> <span data-ttu-id="096d2-116">`FileLogger`을 다른 `ILogger` 구현으로 대체 하려는 경우 `SomeComponent`를 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-116">If you want to replace `FileLogger` with another `ILogger` implementation, you will have to modify `SomeComponent`.</span></span> <span data-ttu-id="096d2-117">많은 다른 개체가 `FileLogger`를 사용 하는 경우 모든 개체를 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-117">Supposing that a lot of other objects use `FileLogger`, you will need to change all of them.</span></span> <span data-ttu-id="096d2-118">또는 단일 항목을 `FileLogger` 하도록 결정 한 경우에는 응용 프로그램 전체에서 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-118">Or if you decide to make `FileLogger` a singleton, you'll also need to make changes throughout the application.</span></span>

<span data-ttu-id="096d2-119">생성자 인수를 사용 하는 등의 방법으로 개체에 `ILogger`을 "주입" 하는 것이 더 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-119">A better approach is to "inject" an `ILogger` into the object—for example, by using a constructor argument:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="096d2-120">이제 개체는 사용할 `ILogger`를 선택 하는 일을 담당 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-120">Now the object is not responsible for selecting which `ILogger` to use.</span></span> <span data-ttu-id="096d2-121">이에 종속 된 개체를 변경 하지 않고 `ILogger` 구현을 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-121">You can switch `ILogger` implementations without changing the objects that depend on it.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="096d2-122">이 패턴을 [생성자 주입](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-122">This pattern is called [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="096d2-123">또 다른 패턴은 setter 삽입으로, setter 메서드 또는 속성을 통해 종속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-123">Another pattern is setter injection, where you set the dependency through a setter method or property.</span></span>

## <a name="simple-dependency-injection-in-signalr"></a><span data-ttu-id="096d2-124">SignalR의 간단한 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="096d2-124">Simple Dependency Injection in SignalR</span></span>

<span data-ttu-id="096d2-125">[SignalR 시작](../getting-started/tutorial-getting-started-with-signalr.md)자습서의 채팅 응용 프로그램을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-125">Consider the Chat application from the tutorial [Getting Started with SignalR](../getting-started/tutorial-getting-started-with-signalr.md).</span></span> <span data-ttu-id="096d2-126">해당 응용 프로그램의 허브 클래스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-126">Here is the hub class from that application:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="096d2-127">메시지를 보내기 전에 서버에 채팅 메시지를 저장 하려는 경우를 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-127">Suppose that you want to store chat messages on the server before sending them.</span></span> <span data-ttu-id="096d2-128">이 기능을 추상화 하는 인터페이스를 정의 하 고 DI를 사용 하 여 `ChatHub` 클래스에 인터페이스를 주입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-128">You might define an interface that abstracts this functionality, and use DI to inject the interface into the `ChatHub` class.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="096d2-129">유일한 문제는 SignalR 응용 프로그램에서 직접 허브를 만들지 않는 것입니다. SignalR 사용자를 위해 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-129">The only problem is that a SignalR application does not directly create hubs; SignalR creates them for you.</span></span> <span data-ttu-id="096d2-130">기본적으로 SignalR에는 매개 변수가 없는 생성자가 있는 허브 클래스가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-130">By default, SignalR expects a hub class to have a parameterless constructor.</span></span> <span data-ttu-id="096d2-131">그러나 함수를 쉽게 등록 하 여 허브 인스턴스를 만들고이 함수를 사용 하 여 DI를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-131">However, you can easily register a function to create hub instances, and use this function to perform DI.</span></span> <span data-ttu-id="096d2-132">**DependencyResolver**를 호출 하 여 함수를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-132">Register the function by calling **GlobalHost.DependencyResolver.Register**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample7.cs)]

<span data-ttu-id="096d2-133">이제 SignalR는 `ChatHub` 인스턴스를 만들어야 할 때마다이 무명 함수를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-133">Now SignalR will invoke this anonymous function whenever it needs to create a `ChatHub` instance.</span></span>

## <a name="ioc-containers"></a><span data-ttu-id="096d2-134">IoC 컨테이너</span><span class="sxs-lookup"><span data-stu-id="096d2-134">IoC Containers</span></span>

<span data-ttu-id="096d2-135">위의 코드는 간단한 경우에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-135">The previous code is fine for simple cases.</span></span> <span data-ttu-id="096d2-136">그러나 여전히이를 작성 해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-136">But you still had to write this:</span></span>

[!code-css[Main](dependency-injection/samples/sample8.css)]

<span data-ttu-id="096d2-137">많은 종속성이 있는 복잡 한 응용 프로그램에서는 많은 "배선" 코드를 작성 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-137">In a complex application with many dependencies, you might need to write a lot of this "wiring" code.</span></span> <span data-ttu-id="096d2-138">특히 종속성이 중첩 된 경우이 코드를 유지 관리 하기 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-138">This code can be hard to maintain, especially if dependencies are nested.</span></span> <span data-ttu-id="096d2-139">단위 테스트도 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-139">It is also hard to unit test.</span></span>

<span data-ttu-id="096d2-140">한 가지 해결 방법은 IoC 컨테이너를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-140">One solution is to use an IoC container.</span></span> <span data-ttu-id="096d2-141">IoC 컨테이너는 종속성 관리를 담당 하는 소프트웨어 구성 요소입니다. 컨테이너를 사용 하 여 형식을 등록 한 다음 컨테이너를 사용 하 여 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-141">An IoC container is a software component that is responsible for managing dependencies.You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="096d2-142">컨테이너는 종속성 관계를 자동으로 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-142">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="096d2-143">많은 IoC 컨테이너를 사용 하 여 개체 수명 및 범위와 같은 항목을 제어할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-143">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="096d2-144">"IoC"는 프레임 워크가 응용 프로그램 코드를 호출 하는 일반적인 패턴 인 "제어 반전"을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-144">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="096d2-145">IoC 컨테이너는 사용자에 대 한 개체를 생성 하 여 일반적인 제어 흐름을 "반전" 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-145">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>

## <a name="using-ioc-containers-in-signalr"></a><span data-ttu-id="096d2-146">SignalR에서 IoC 컨테이너 사용</span><span class="sxs-lookup"><span data-stu-id="096d2-146">Using IoC Containers in SignalR</span></span>

<span data-ttu-id="096d2-147">채팅 응용 프로그램은 매우 간단 하 여 IoC 컨테이너의 이점을 누릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-147">The Chat application is probably too simple to benefit from an IoC container.</span></span> <span data-ttu-id="096d2-148">대신 [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) 샘플을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-148">Instead, let's look at the [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) sample.</span></span>

<span data-ttu-id="096d2-149">StockTicker 샘플은 두 개의 주 클래스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-149">The StockTicker sample defines two main classes:</span></span>

- <span data-ttu-id="096d2-150">`StockTickerHub`: 클라이언트 연결을 관리 하는 허브 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-150">`StockTickerHub`: The hub class, which manages client connections.</span></span>
- <span data-ttu-id="096d2-151">`StockTicker`: 주식 가격을 보유 하 고 정기적으로 업데이트 하는 단일 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-151">`StockTicker`: A singleton that holds stock prices and periodically updates them.</span></span>

<span data-ttu-id="096d2-152">`StockTickerHub`는 `StockTicker` singleton에 대 한 참조를 보유 하 고 `StockTicker`는 `StockTickerHub`에 대 한 **IHubConnectionContext** 에 대 한 참조를 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-152">`StockTickerHub` holds a reference to the `StockTicker` singleton, while `StockTicker` holds a reference to the **IHubConnectionContext** for the `StockTickerHub`.</span></span> <span data-ttu-id="096d2-153">이 인터페이스는이 인터페이스를 사용 하 여 `StockTickerHub` 인스턴스와 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-153">It uses this interface to communicate with `StockTickerHub` instances.</span></span> <span data-ttu-id="096d2-154">자세한 내용은 [ASP.NET SignalR를 사용 하 여 서버 브로드캐스트](index.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="096d2-154">(For more information, see [Server Broadcast with ASP.NET SignalR](index.md).)</span></span>

<span data-ttu-id="096d2-155">IoC 컨테이너를 사용 하 여 이러한 종속성을 약간 untangle 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-155">We can use an IoC container to untangle these dependencies a bit.</span></span> <span data-ttu-id="096d2-156">먼저 `StockTickerHub` 및 `StockTicker` 클래스를 단순화 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-156">First, let's simplify the `StockTickerHub` and `StockTicker` classes.</span></span> <span data-ttu-id="096d2-157">다음 코드에서는 필요 하지 않은 부분을 주석으로 처리 했습니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-157">In the following code, I've commented out the parts that we don't need.</span></span>

<span data-ttu-id="096d2-158">`StockTicker`에서 매개 변수가 없는 생성자를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-158">Remove the parameterless constructor from `StockTicker`.</span></span> <span data-ttu-id="096d2-159">대신 항상 DI를 사용 하 여 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-159">Instead, we will always use DI to create the hub.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

<span data-ttu-id="096d2-160">StockTicker의 경우 singleton 인스턴스를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-160">For StockTicker, remove the singleton instance.</span></span> <span data-ttu-id="096d2-161">나중에 IoC 컨테이너를 사용 하 여 StockTicker 수명을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-161">Later, we'll use the IoC container to control the StockTicker lifetime.</span></span> <span data-ttu-id="096d2-162">또한 생성자를 public으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-162">Also, make the constructor public.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs?highlight=7)]

<span data-ttu-id="096d2-163">그런 다음 `StockTicker`에 대 한 인터페이스를 만들어 코드를 리팩터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-163">Next, we can refactor the code by creating an interface for `StockTicker`.</span></span> <span data-ttu-id="096d2-164">이 인터페이스를 사용 하 여 `StockTicker` 클래스에서 `StockTickerHub`를 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-164">We'll use this interface to decouple the `StockTickerHub` from the `StockTicker` class.</span></span>

<span data-ttu-id="096d2-165">Visual Studio에서는 이러한 종류의 리팩터링을 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-165">Visual Studio makes this kind of refactoring easy.</span></span> <span data-ttu-id="096d2-166">StockTicker.cs 파일을 열고 `StockTicker` 클래스 선언을 마우스 오른쪽 단추로 클릭 한 다음 **리팩터링** ...을 선택 합니다. **인터페이스를 추출**합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-166">Open the file StockTicker.cs, right-click on the `StockTicker` class declaration, and select **Refactor** ... **Extract Interface**.</span></span>

![](dependency-injection/_static/image1.png)

<span data-ttu-id="096d2-167">**인터페이스 추출** 대화 상자에서 **모두 선택**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-167">In the **Extract Interface** dialog, click **Select All**.</span></span> <span data-ttu-id="096d2-168">다른 기본값을 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-168">Leave the other defaults.</span></span> <span data-ttu-id="096d2-169">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-169">Click **OK**.</span></span>

![](dependency-injection/_static/image2.png)

<span data-ttu-id="096d2-170">Visual Studio는 `IStockTicker`이라는 새 인터페이스를 만들고 `IStockTicker`에서 파생 `StockTicker` 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-170">Visual Studio creates a new interface named `IStockTicker`, and also changes `StockTicker` to derive from `IStockTicker`.</span></span>

<span data-ttu-id="096d2-171">IStockTicker.cs 파일을 열고 인터페이스를 **public**으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-171">Open the file IStockTicker.cs and change the interface to **public**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample11.cs?highlight=1)]

<span data-ttu-id="096d2-172">`StockTickerHub` 클래스에서 `StockTicker`의 두 인스턴스를 `IStockTicker`로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-172">In the `StockTickerHub` class, change the two instances of `StockTicker` to `IStockTicker`:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample12.cs?highlight=4,6)]

<span data-ttu-id="096d2-173">`IStockTicker` 인터페이스를 만드는 것은 반드시 필요한 것은 아니지만 DI를 통해 응용 프로그램의 구성 요소 간 결합을 줄이는 방법을 보여 드리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-173">Creating an `IStockTicker` interface isn't strictly necessary, but I wanted to show how DI can help to reduce coupling between components in your application.</span></span>

## <a name="add-the-ninject-library"></a><span data-ttu-id="096d2-174">Ninject 라이브러리 추가</span><span class="sxs-lookup"><span data-stu-id="096d2-174">Add the Ninject Library</span></span>

<span data-ttu-id="096d2-175">.NET 용 오픈 소스 IoC 컨테이너는 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-175">There are many open-source IoC containers for .NET.</span></span> <span data-ttu-id="096d2-176">이 자습서에서는 [Ninject](http://www.ninject.org/)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-176">For this tutorial, I'll use [Ninject](http://www.ninject.org/).</span></span> <span data-ttu-id="096d2-177">(기타 인기 있는 라이브러리에는 [성 Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity)및 [StructureMap](http://docs.structuremap.net)가 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="096d2-177">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity), and [StructureMap](http://docs.structuremap.net).)</span></span>

<span data-ttu-id="096d2-178">NuGet 패키지 관리자를 사용 하 여 [Ninject 라이브러리](https://nuget.org/packages/Ninject/3.0.1.10)를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-178">Use NuGet Package Manager to install the [Ninject library](https://nuget.org/packages/Ninject/3.0.1.10).</span></span> <span data-ttu-id="096d2-179">Visual Studio의 **도구** 메뉴에서 **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-179">In Visual Studio, from the **Tools** menu select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="096d2-180">패키지 관리자 콘솔 창에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-180">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](dependency-injection/samples/sample13.ps1)]

## <a name="replace-the-signalr-dependency-resolver"></a><span data-ttu-id="096d2-181">SignalR 종속성 확인자를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-181">Replace the SignalR Dependency Resolver</span></span>

<span data-ttu-id="096d2-182">SignalR 내에서 Ninject를 사용 하려면 **DefaultDependencyResolver**에서 파생 되는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-182">To use Ninject within SignalR, create a class that derives from **DefaultDependencyResolver**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample14.cs)]

<span data-ttu-id="096d2-183">이 클래스는 **DefaultDependencyResolver**의 **GetService** 및 **getservices** 메서드를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-183">This class overrides the **GetService** and **GetServices** methods of **DefaultDependencyResolver**.</span></span> <span data-ttu-id="096d2-184">SignalR는 이러한 메서드를 호출 하 여 런타임에 SignalR에서 내부적으로 사용 되는 다양 한 서비스 뿐만 아니라 허브 인스턴스를 비롯 한 다양 한 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-184">SignalR calls these methods to create various objects at runtime, including hub instances, as well as various services used internally by SignalR.</span></span>

- <span data-ttu-id="096d2-185">**GetService** 메서드는 형식의 단일 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-185">The **GetService** method creates a single instance of a type.</span></span> <span data-ttu-id="096d2-186">Ninject 커널의 **Trget** 메서드를 호출 하려면이 메서드를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-186">Override this method to call the Ninject kernel's **TryGet** method.</span></span> <span data-ttu-id="096d2-187">해당 메서드가 null을 반환 하는 경우 기본 해결 프로그램으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-187">If that method returns null, fall back to the default resolver.</span></span>
- <span data-ttu-id="096d2-188">**Getservices** 메서드는 지정 된 형식의 개체 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-188">The **GetServices** method creates a collection of objects of a specified type.</span></span> <span data-ttu-id="096d2-189">Ninject의 결과를 기본 해결 프로그램의 결과와 연결 하려면이 메서드를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-189">Override this method to concatenate the results from Ninject with the results from the default resolver.</span></span>

## <a name="configure-ninject-bindings"></a><span data-ttu-id="096d2-190">Ninject 바인딩 구성</span><span class="sxs-lookup"><span data-stu-id="096d2-190">Configure Ninject Bindings</span></span>

<span data-ttu-id="096d2-191">이제 Ninject을 사용 하 여 형식 바인딩을 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-191">Now we'll use Ninject to declare type bindings.</span></span>

<span data-ttu-id="096d2-192">RegisterHubs.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-192">Open the file RegisterHubs.cs.</span></span> <span data-ttu-id="096d2-193">`RegisterHubs.Start` 메서드에서 Ninject가 *커널을*호출 하는 Ninject 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-193">In the `RegisterHubs.Start` method, create the Ninject container, which Ninject calls the *kernel*.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample15.cs)]

<span data-ttu-id="096d2-194">사용자 지정 종속성 해결 프로그램의 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-194">Create an instance of our custom dependency resolver:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample16.cs)]

<span data-ttu-id="096d2-195">다음과 같이 `IStockTicker`에 대 한 바인딩을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-195">Create a binding for `IStockTicker` as follows:</span></span>

[!code-html[Main](dependency-injection/samples/sample17.html)]

<span data-ttu-id="096d2-196">이 코드는 두 가지를 말합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-196">This code is saying two things.</span></span> <span data-ttu-id="096d2-197">먼저 응용 프로그램에 `IStockTicker`필요할 때마다 커널이 `StockTicker`의 인스턴스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-197">First, whenever the application needs an `IStockTicker`, the kernel should create an instance of `StockTicker`.</span></span> <span data-ttu-id="096d2-198">둘째, `StockTicker` 클래스는 단일 개체로 생성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-198">Second, the `StockTicker` class should be a created as a singleton object.</span></span> <span data-ttu-id="096d2-199">Ninject는 개체의 인스턴스 하나를 만들고 각 요청에 대해 동일한 인스턴스를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-199">Ninject will create one instance of the object, and return the same instance for each request.</span></span>

<span data-ttu-id="096d2-200">다음과 같이 **IHubConnectionContext** 에 대 한 바인딩을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-200">Create a binding for **IHubConnectionContext** as follows:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample18.cs)]

<span data-ttu-id="096d2-201">이 코드는 **IHubConnection**를 반환 하는 익명 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-201">This code creates an anonymous function that returns an **IHubConnection**.</span></span> <span data-ttu-id="096d2-202">**WhenInjectedInto** 메서드는 `IStockTicker` 인스턴스를 만들 때만이 함수를 사용 하도록 Ninject에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-202">The **WhenInjectedInto** method tells Ninject to use this function only when creating `IStockTicker` instances.</span></span> <span data-ttu-id="096d2-203">그 이유는 SignalR는 내부적으로 **IHubConnectionContext** 인스턴스를 만들기 때문에 SignalR가 만드는 방법을 재정의 하려고 하지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-203">The reason is that SignalR creates **IHubConnectionContext** instances internally, and we don't want to override how SignalR creates them.</span></span> <span data-ttu-id="096d2-204">이 함수는 `StockTicker` 클래스에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-204">This function only applies to our `StockTicker` class.</span></span>

<span data-ttu-id="096d2-205">종속성 확인자를 **Maphubs** 메서드에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-205">Pass the dependency resolver into the **MapHubs** method:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample19.cs)]

<span data-ttu-id="096d2-206">이제 SignalR는 기본 해결 프로그램 대신 **Maphubs**에 지정 된 해결 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-206">Now SignalR will use the resolver specified in **MapHubs**, instead of the default resolver.</span></span>

<span data-ttu-id="096d2-207">`RegisterHubs.Start`에 대 한 전체 코드 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-207">Here is the complete code listing for `RegisterHubs.Start`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample20.cs)]

<span data-ttu-id="096d2-208">Visual Studio에서 StockTicker 응용 프로그램을 실행 하려면 F5 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-208">To run the StockTicker application in Visual Studio, press F5.</span></span> <span data-ttu-id="096d2-209">브라우저 창에서 `http://localhost:*port*/SignalR.Sample/StockTicker.html`로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-209">In the browser window, navigate to `http://localhost:*port*/SignalR.Sample/StockTicker.html`.</span></span>

![](dependency-injection/_static/image3.png)

<span data-ttu-id="096d2-210">응용 프로그램은 이전과 동일 하 게 동일한 기능을가지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-210">The application has exactly the same functionality as before.</span></span> <span data-ttu-id="096d2-211">자세한 내용은 [ASP.NET SignalR를 사용 하 여 서버 브로드캐스트](index.md)를 참조 하세요. 이 동작은 변경 되지 않았습니다. 코드를 쉽게 테스트 하 고, 유지 관리 하 고, 발전 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="096d2-211">(For a description, see [Server Broadcast with ASP.NET SignalR](index.md).) We haven't changed the behavior; just made the code easier to test, maintain, and evolve.</span></span>
