---
uid: signalr/overview/advanced/dependency-injection
title: SignalR의 종속성 주입 | Microsoft Docs
author: bradygaster
description: 이전 버전의에 대 한 자세한 내용은이 항목에서 사용 된 소프트웨어 버전 Visual Studio 2013 .NET 4.5 SignalR 버전 2 이전 버전의 항목을 참조 하세요.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: a14121ae-02cf-4024-8af0-9dd0dc810690
msc.legacyurl: /signalr/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 52978b10b6c131ac8eff4535216cc60b43fdf3de
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431867"
---
# <a name="dependency-injection-in-signalr"></a><span data-ttu-id="ebb0d-103">SignalR에서 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="ebb0d-103">Dependency Injection in SignalR</span></span>

<span data-ttu-id="ebb0d-104">사람, [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="ebb0d-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="ebb0d-105">이 항목에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="ebb0d-105">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="ebb0d-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="ebb0d-106">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="ebb0d-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="ebb0d-107">.NET 4.5</span></span>
> - <span data-ttu-id="ebb0d-108">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="ebb0d-108">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="ebb0d-109">이 항목의 이전 버전</span><span class="sxs-lookup"><span data-stu-id="ebb0d-109">Previous versions of this topic</span></span>
>
> <span data-ttu-id="ebb0d-110">이전 버전의 SignalR에 대 한 자세한 내용은 [SignalR 이전 버전](../older-versions/index.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="ebb0d-111">질문 및 설명</span><span class="sxs-lookup"><span data-stu-id="ebb0d-111">Questions and comments</span></span>
>
> <span data-ttu-id="ebb0d-112">이 자습서와 페이지 맨 아래에 있는 의견에서 개선할 수 있는 방법에 대 한 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="ebb0d-113">자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="ebb0d-114">종속성 주입은 개체 간에 하드 코드 된 종속성을 제거 하는 방법으로, 테스트 (모의 개체 사용) 또는 런타임 동작을 변경 하 여 개체의 종속성을 쉽게 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-114">Dependency injection is a way to remove hard-coded dependencies between objects, making it easier to replace an object's dependencies, either for testing (using mock objects) or to change run-time behavior.</span></span> <span data-ttu-id="ebb0d-115">이 자습서에서는 SignalR hubs에서 종속성 주입을 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-115">This tutorial shows how to perform dependency injection on SignalR hubs.</span></span> <span data-ttu-id="ebb0d-116">또한 SignalR에서 IoC 컨테이너를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-116">It also shows how to use IoC containers with SignalR.</span></span> <span data-ttu-id="ebb0d-117">IoC 컨테이너는 종속성 주입을 위한 일반 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-117">An IoC container is a general framework for dependency injection.</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="ebb0d-118">종속성 주입 이란?</span><span class="sxs-lookup"><span data-stu-id="ebb0d-118">What is Dependency Injection?</span></span>

<span data-ttu-id="ebb0d-119">종속성 주입에 이미 익숙한 경우이 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-119">Skip this section if you are already familiar with dependency injection.</span></span>

<span data-ttu-id="ebb0d-120">DI ( *종속성 주입* )는 개체가 자체 종속성을 만들 책임이 없는 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-120">*Dependency injection* (DI) is a pattern where objects are not responsible for creating their own dependencies.</span></span> <span data-ttu-id="ebb0d-121">다음은 DI를 동기로 확인 하는 간단한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-121">Here is a simple example to motivate DI.</span></span> <span data-ttu-id="ebb0d-122">메시지를 기록 해야 하는 개체가 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-122">Suppose you have an object that needs to log messages.</span></span> <span data-ttu-id="ebb0d-123">로깅 인터페이스를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-123">You might define a logging interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="ebb0d-124">개체에서 메시지를 기록 하는 `ILogger`를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-124">In your object, you can create an `ILogger` to log messages:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="ebb0d-125">이렇게 하는 것이 좋지만 최상의 디자인은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-125">This works, but it's not the best design.</span></span> <span data-ttu-id="ebb0d-126">`FileLogger`을 다른 `ILogger` 구현으로 대체 하려는 경우 `SomeComponent`를 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-126">If you want to replace `FileLogger` with another `ILogger` implementation, you will have to modify `SomeComponent`.</span></span> <span data-ttu-id="ebb0d-127">많은 다른 개체가 `FileLogger`를 사용 하는 경우 모든 개체를 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-127">Supposing that a lot of other objects use `FileLogger`, you will need to change all of them.</span></span> <span data-ttu-id="ebb0d-128">또는 단일 항목을 `FileLogger` 하도록 결정 한 경우에는 응용 프로그램 전체에서 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-128">Or if you decide to make `FileLogger` a singleton, you'll also need to make changes throughout the application.</span></span>

<span data-ttu-id="ebb0d-129">생성자 인수를 사용 하는 등의 방법으로 개체에 `ILogger`을 "주입" 하는 것이 더 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-129">A better approach is to "inject" an `ILogger` into the object—for example, by using a constructor argument:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="ebb0d-130">이제 개체는 사용할 `ILogger`를 선택 하는 일을 담당 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-130">Now the object is not responsible for selecting which `ILogger` to use.</span></span> <span data-ttu-id="ebb0d-131">이에 종속 된 개체를 변경 하지 않고 `ILogger` 구현을 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-131">You can switch `ILogger` implementations without changing the objects that depend on it.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="ebb0d-132">이 패턴을 [생성자 주입](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-132">This pattern is called [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="ebb0d-133">또 다른 패턴은 setter 삽입으로, setter 메서드 또는 속성을 통해 종속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-133">Another pattern is setter injection, where you set the dependency through a setter method or property.</span></span>

## <a name="simple-dependency-injection-in-signalr"></a><span data-ttu-id="ebb0d-134">SignalR의 간단한 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="ebb0d-134">Simple Dependency Injection in SignalR</span></span>

<span data-ttu-id="ebb0d-135">[SignalR 시작](../getting-started/tutorial-getting-started-with-signalr.md)자습서의 채팅 응용 프로그램을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-135">Consider the Chat application from the tutorial [Getting Started with SignalR](../getting-started/tutorial-getting-started-with-signalr.md).</span></span> <span data-ttu-id="ebb0d-136">해당 응용 프로그램의 허브 클래스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-136">Here is the hub class from that application:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="ebb0d-137">메시지를 보내기 전에 서버에 채팅 메시지를 저장 하려는 경우를 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-137">Suppose that you want to store chat messages on the server before sending them.</span></span> <span data-ttu-id="ebb0d-138">이 기능을 추상화 하는 인터페이스를 정의 하 고 DI를 사용 하 여 `ChatHub` 클래스에 인터페이스를 주입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-138">You might define an interface that abstracts this functionality, and use DI to inject the interface into the `ChatHub` class.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="ebb0d-139">유일한 문제는 SignalR 응용 프로그램에서 직접 허브를 만들지 않는 것입니다. SignalR 사용자를 위해 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-139">The only problem is that a SignalR application does not directly create hubs; SignalR creates them for you.</span></span> <span data-ttu-id="ebb0d-140">기본적으로 SignalR에는 매개 변수가 없는 생성자가 있는 허브 클래스가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-140">By default, SignalR expects a hub class to have a parameterless constructor.</span></span> <span data-ttu-id="ebb0d-141">그러나 함수를 쉽게 등록 하 여 허브 인스턴스를 만들고이 함수를 사용 하 여 DI를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-141">However, you can easily register a function to create hub instances, and use this function to perform DI.</span></span> <span data-ttu-id="ebb0d-142">**DependencyResolver**를 호출 하 여 함수를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-142">Register the function by calling **GlobalHost.DependencyResolver.Register**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample7.cs)]

<span data-ttu-id="ebb0d-143">이제 SignalR는 `ChatHub` 인스턴스를 만들어야 할 때마다이 무명 함수를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-143">Now SignalR will invoke this anonymous function whenever it needs to create a `ChatHub` instance.</span></span>

## <a name="ioc-containers"></a><span data-ttu-id="ebb0d-144">IoC 컨테이너</span><span class="sxs-lookup"><span data-stu-id="ebb0d-144">IoC Containers</span></span>

<span data-ttu-id="ebb0d-145">위의 코드는 간단한 경우에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-145">The previous code is fine for simple cases.</span></span> <span data-ttu-id="ebb0d-146">그러나 여전히이를 작성 해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-146">But you still had to write this:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

<span data-ttu-id="ebb0d-147">많은 종속성이 있는 복잡 한 응용 프로그램에서는 많은 "배선" 코드를 작성 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-147">In a complex application with many dependencies, you might need to write a lot of this "wiring" code.</span></span> <span data-ttu-id="ebb0d-148">특히 종속성이 중첩 된 경우이 코드를 유지 관리 하기 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-148">This code can be hard to maintain, especially if dependencies are nested.</span></span> <span data-ttu-id="ebb0d-149">단위 테스트도 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-149">It is also hard to unit test.</span></span>

<span data-ttu-id="ebb0d-150">한 가지 해결 방법은 IoC 컨테이너를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-150">One solution is to use an IoC container.</span></span> <span data-ttu-id="ebb0d-151">IoC 컨테이너는 종속성 관리를 담당 하는 소프트웨어 구성 요소입니다. 컨테이너를 사용 하 여 형식을 등록 한 다음 컨테이너를 사용 하 여 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-151">An IoC container is a software component that is responsible for managing dependencies.You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="ebb0d-152">컨테이너는 종속성 관계를 자동으로 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-152">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="ebb0d-153">많은 IoC 컨테이너를 사용 하 여 개체 수명 및 범위와 같은 항목을 제어할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-153">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="ebb0d-154">"IoC"는 프레임 워크가 응용 프로그램 코드를 호출 하는 일반적인 패턴 인 "제어 반전"을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-154">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="ebb0d-155">IoC 컨테이너는 사용자에 대 한 개체를 생성 하 여 일반적인 제어 흐름을 "반전" 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-155">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>

## <a name="using-ioc-containers-in-signalr"></a><span data-ttu-id="ebb0d-156">SignalR에서 IoC 컨테이너 사용</span><span class="sxs-lookup"><span data-stu-id="ebb0d-156">Using IoC Containers in SignalR</span></span>

<span data-ttu-id="ebb0d-157">채팅 응용 프로그램은 매우 간단 하 여 IoC 컨테이너의 이점을 누릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-157">The Chat application is probably too simple to benefit from an IoC container.</span></span> <span data-ttu-id="ebb0d-158">대신 [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) 샘플을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-158">Instead, let's look at the [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) sample.</span></span>

<span data-ttu-id="ebb0d-159">StockTicker 샘플은 두 개의 주 클래스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-159">The StockTicker sample defines two main classes:</span></span>

- <span data-ttu-id="ebb0d-160">`StockTickerHub`: 클라이언트 연결을 관리 하는 허브 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-160">`StockTickerHub`: The hub class, which manages client connections.</span></span>
- <span data-ttu-id="ebb0d-161">`StockTicker`: 주식 가격을 보유 하 고 정기적으로 업데이트 하는 단일 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-161">`StockTicker`: A singleton that holds stock prices and periodically updates them.</span></span>

<span data-ttu-id="ebb0d-162">`StockTickerHub`는 `StockTicker` singleton에 대 한 참조를 보유 하 고 `StockTicker`는 `StockTickerHub`에 대 한 **IHubConnectionContext** 에 대 한 참조를 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-162">`StockTickerHub` holds a reference to the `StockTicker` singleton, while `StockTicker` holds a reference to the **IHubConnectionContext** for the `StockTickerHub`.</span></span> <span data-ttu-id="ebb0d-163">이 인터페이스는이 인터페이스를 사용 하 여 `StockTickerHub` 인스턴스와 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-163">It uses this interface to communicate with `StockTickerHub` instances.</span></span> <span data-ttu-id="ebb0d-164">자세한 내용은 [ASP.NET SignalR를 사용 하 여 서버 브로드캐스트](../getting-started/tutorial-server-broadcast-with-signalr.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-164">(For more information, see [Server Broadcast with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).)</span></span>

<span data-ttu-id="ebb0d-165">IoC 컨테이너를 사용 하 여 이러한 종속성을 약간 untangle 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-165">We can use an IoC container to untangle these dependencies a bit.</span></span> <span data-ttu-id="ebb0d-166">먼저 `StockTickerHub` 및 `StockTicker` 클래스를 단순화 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-166">First, let's simplify the `StockTickerHub` and `StockTicker` classes.</span></span> <span data-ttu-id="ebb0d-167">다음 코드에서는 필요 하지 않은 부분을 주석으로 처리 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-167">In the following code, I've commented out the parts that we don't need.</span></span>

<span data-ttu-id="ebb0d-168">`StockTickerHub`에서 매개 변수가 없는 생성자를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-168">Remove the parameterless constructor from `StockTickerHub`.</span></span> <span data-ttu-id="ebb0d-169">대신 항상 DI를 사용 하 여 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-169">Instead, we will always use DI to create the hub.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

<span data-ttu-id="ebb0d-170">StockTicker의 경우 singleton 인스턴스를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-170">For StockTicker, remove the singleton instance.</span></span> <span data-ttu-id="ebb0d-171">나중에 IoC 컨테이너를 사용 하 여 StockTicker 수명을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-171">Later, we'll use the IoC container to control the StockTicker lifetime.</span></span> <span data-ttu-id="ebb0d-172">또한 생성자를 public으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-172">Also, make the constructor public.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs?highlight=7)]

<span data-ttu-id="ebb0d-173">그런 다음 `StockTicker`에 대 한 인터페이스를 만들어 코드를 리팩터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-173">Next, we can refactor the code by creating an interface for `StockTicker`.</span></span> <span data-ttu-id="ebb0d-174">이 인터페이스를 사용 하 여 `StockTicker` 클래스에서 `StockTickerHub`를 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-174">We'll use this interface to decouple the `StockTickerHub` from the `StockTicker` class.</span></span>

<span data-ttu-id="ebb0d-175">Visual Studio에서는 이러한 종류의 리팩터링을 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-175">Visual Studio makes this kind of refactoring easy.</span></span> <span data-ttu-id="ebb0d-176">StockTicker.cs 파일을 열고 `StockTicker` 클래스 선언을 마우스 오른쪽 단추로 클릭 한 다음 **리팩터링** ...을 선택 합니다. **인터페이스를 추출**합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-176">Open the file StockTicker.cs, right-click on the `StockTicker` class declaration, and select **Refactor** ... **Extract Interface**.</span></span>

![](dependency-injection/_static/image1.png)

<span data-ttu-id="ebb0d-177">**인터페이스 추출** 대화 상자에서 **모두 선택**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-177">In the **Extract Interface** dialog, click **Select All**.</span></span> <span data-ttu-id="ebb0d-178">다른 기본값을 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-178">Leave the other defaults.</span></span> <span data-ttu-id="ebb0d-179">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-179">Click **OK**.</span></span>

![](dependency-injection/_static/image2.png)

<span data-ttu-id="ebb0d-180">Visual Studio는 `IStockTicker`이라는 새 인터페이스를 만들고 `IStockTicker`에서 파생 `StockTicker` 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-180">Visual Studio creates a new interface named `IStockTicker`, and also changes `StockTicker` to derive from `IStockTicker`.</span></span>

<span data-ttu-id="ebb0d-181">IStockTicker.cs 파일을 열고 인터페이스를 **public**으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-181">Open the file IStockTicker.cs and change the interface to **public**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample11.cs?highlight=1)]

<span data-ttu-id="ebb0d-182">`StockTickerHub` 클래스에서 `StockTicker`의 두 인스턴스를 `IStockTicker`로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-182">In the `StockTickerHub` class, change the two instances of `StockTicker` to `IStockTicker`:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample12.cs?highlight=4,6)]

<span data-ttu-id="ebb0d-183">`IStockTicker` 인터페이스를 만드는 것은 반드시 필요한 것은 아니지만 DI를 통해 응용 프로그램의 구성 요소 간 결합을 줄이는 방법을 보여 드리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-183">Creating an `IStockTicker` interface isn't strictly necessary, but I wanted to show how DI can help to reduce coupling between components in your application.</span></span>

## <a name="add-the-ninject-library"></a><span data-ttu-id="ebb0d-184">Ninject 라이브러리 추가</span><span class="sxs-lookup"><span data-stu-id="ebb0d-184">Add the Ninject Library</span></span>

<span data-ttu-id="ebb0d-185">.NET 용 오픈 소스 IoC 컨테이너는 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-185">There are many open-source IoC containers for .NET.</span></span> <span data-ttu-id="ebb0d-186">이 자습서에서는 [Ninject](http://www.ninject.org/)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-186">For this tutorial, I'll use [Ninject](http://www.ninject.org/).</span></span> <span data-ttu-id="ebb0d-187">(기타 인기 있는 라이브러리에는 [성 Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity)및 [StructureMap](http://docs.structuremap.net)가 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="ebb0d-187">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity), and [StructureMap](http://docs.structuremap.net).)</span></span>

<span data-ttu-id="ebb0d-188">NuGet 패키지 관리자를 사용 하 여 [Ninject 라이브러리](https://nuget.org/packages/Ninject/3.0.1.10)를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-188">Use NuGet Package Manager to install the [Ninject library](https://nuget.org/packages/Ninject/3.0.1.10).</span></span> <span data-ttu-id="ebb0d-189">Visual Studio의 **도구** 메뉴에서 **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-189">In Visual Studio, from the **Tools** menu select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="ebb0d-190">패키지 관리자 콘솔 창에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-190">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](dependency-injection/samples/sample13.ps1)]

## <a name="replace-the-signalr-dependency-resolver"></a><span data-ttu-id="ebb0d-191">SignalR 종속성 확인자를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-191">Replace the SignalR Dependency Resolver</span></span>

<span data-ttu-id="ebb0d-192">SignalR 내에서 Ninject를 사용 하려면 **DefaultDependencyResolver**에서 파생 되는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-192">To use Ninject within SignalR, create a class that derives from **DefaultDependencyResolver**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample14.cs)]

<span data-ttu-id="ebb0d-193">이 클래스는 **DefaultDependencyResolver**의 **GetService** 및 **getservices** 메서드를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-193">This class overrides the **GetService** and **GetServices** methods of **DefaultDependencyResolver**.</span></span> <span data-ttu-id="ebb0d-194">SignalR는 이러한 메서드를 호출 하 여 런타임에 SignalR에서 내부적으로 사용 되는 다양 한 서비스 뿐만 아니라 허브 인스턴스를 비롯 한 다양 한 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-194">SignalR calls these methods to create various objects at runtime, including hub instances, as well as various services used internally by SignalR.</span></span>

- <span data-ttu-id="ebb0d-195">**GetService** 메서드는 형식의 단일 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-195">The **GetService** method creates a single instance of a type.</span></span> <span data-ttu-id="ebb0d-196">Ninject 커널의 **Trget** 메서드를 호출 하려면이 메서드를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-196">Override this method to call the Ninject kernel's **TryGet** method.</span></span> <span data-ttu-id="ebb0d-197">해당 메서드가 null을 반환 하는 경우 기본 해결 프로그램으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-197">If that method returns null, fall back to the default resolver.</span></span>
- <span data-ttu-id="ebb0d-198">**Getservices** 메서드는 지정 된 형식의 개체 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-198">The **GetServices** method creates a collection of objects of a specified type.</span></span> <span data-ttu-id="ebb0d-199">Ninject의 결과를 기본 해결 프로그램의 결과와 연결 하려면이 메서드를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-199">Override this method to concatenate the results from Ninject with the results from the default resolver.</span></span>

## <a name="configure-ninject-bindings"></a><span data-ttu-id="ebb0d-200">Ninject 바인딩 구성</span><span class="sxs-lookup"><span data-stu-id="ebb0d-200">Configure Ninject Bindings</span></span>

<span data-ttu-id="ebb0d-201">이제 Ninject을 사용 하 여 형식 바인딩을 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-201">Now we'll use Ninject to declare type bindings.</span></span>

<span data-ttu-id="ebb0d-202">응용 프로그램의 Startup.cs 클래스를 엽니다. `readme.txt`의 패키지 지침에 따라 수동으로 만들었거나 프로젝트에 인증을 추가 하 여 만든 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-202">Open your application's Startup.cs class (that you either created manually as per the package instructions in `readme.txt`, or that was created by adding authentication to your project).</span></span> <span data-ttu-id="ebb0d-203">`Startup.Configuration` 메서드에서 Ninject가 *커널을*호출 하는 Ninject 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-203">In the `Startup.Configuration` method, create the Ninject container, which Ninject calls the *kernel*.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample15.cs)]

<span data-ttu-id="ebb0d-204">사용자 지정 종속성 해결 프로그램의 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-204">Create an instance of our custom dependency resolver:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample16.cs)]

<span data-ttu-id="ebb0d-205">다음과 같이 `IStockTicker`에 대 한 바인딩을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-205">Create a binding for `IStockTicker` as follows:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample17.cs)]

<span data-ttu-id="ebb0d-206">이 코드는 두 가지를 말합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-206">This code is saying two things.</span></span> <span data-ttu-id="ebb0d-207">먼저 응용 프로그램에 `IStockTicker`필요할 때마다 커널이 `StockTicker`의 인스턴스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-207">First, whenever the application needs an `IStockTicker`, the kernel should create an instance of `StockTicker`.</span></span> <span data-ttu-id="ebb0d-208">둘째, `StockTicker` 클래스는 단일 개체로 생성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-208">Second, the `StockTicker` class should be a created as a singleton object.</span></span> <span data-ttu-id="ebb0d-209">Ninject는 개체의 인스턴스 하나를 만들고 각 요청에 대해 동일한 인스턴스를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-209">Ninject will create one instance of the object, and return the same instance for each request.</span></span>

<span data-ttu-id="ebb0d-210">다음과 같이 **IHubConnectionContext** 에 대 한 바인딩을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-210">Create a binding for **IHubConnectionContext** as follows:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample18.cs)]

<span data-ttu-id="ebb0d-211">이 코드는 **IHubConnection**를 반환 하는 익명 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-211">This code creates an anonymous function that returns an **IHubConnection**.</span></span> <span data-ttu-id="ebb0d-212">**WhenInjectedInto** 메서드는 `IStockTicker` 인스턴스를 만들 때만이 함수를 사용 하도록 Ninject에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-212">The **WhenInjectedInto** method tells Ninject to use this function only when creating `IStockTicker` instances.</span></span> <span data-ttu-id="ebb0d-213">그 이유는 SignalR는 내부적으로 **IHubConnectionContext** 인스턴스를 만들기 때문에 SignalR가 만드는 방법을 재정의 하려고 하지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-213">The reason is that SignalR creates **IHubConnectionContext** instances internally, and we don't want to override how SignalR creates them.</span></span> <span data-ttu-id="ebb0d-214">이 함수는 `StockTicker` 클래스에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-214">This function only applies to our `StockTicker` class.</span></span>

<span data-ttu-id="ebb0d-215">허브 구성을 추가 하 여 **MapSignalR** 메서드에 종속성 확인자를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-215">Pass the dependency resolver into the **MapSignalR** method by adding a hub configuration:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample19.cs)]

<span data-ttu-id="ebb0d-216">새 매개 변수를 사용 하 여 샘플의 Startup 클래스에서 ConfigureSignalR 메서드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-216">Update the Startup.ConfigureSignalR method in the sample's Startup class with the new parameter:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample20.cs)]

<span data-ttu-id="ebb0d-217">이제 SignalR는 기본 해결 프로그램 대신 **MapSignalR**에 지정 된 해결 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-217">Now SignalR will use the resolver specified in **MapSignalR**, instead of the default resolver.</span></span>

<span data-ttu-id="ebb0d-218">`Startup.Configuration`에 대 한 전체 코드 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-218">Here is the complete code listing for `Startup.Configuration`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample21.cs)]

<span data-ttu-id="ebb0d-219">Visual Studio에서 StockTicker 응용 프로그램을 실행 하려면 F5 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-219">To run the StockTicker application in Visual Studio, press F5.</span></span> <span data-ttu-id="ebb0d-220">브라우저 창에서 `http://localhost:*port*/SignalR.Sample/StockTicker.html`로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-220">In the browser window, navigate to `http://localhost:*port*/SignalR.Sample/StockTicker.html`.</span></span>

![](dependency-injection/_static/image3.png)

<span data-ttu-id="ebb0d-221">응용 프로그램은 이전과 동일 하 게 동일한 기능을가지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-221">The application has exactly the same functionality as before.</span></span> <span data-ttu-id="ebb0d-222">자세한 내용은 [ASP.NET SignalR를 사용 하 여 서버 브로드캐스트](../getting-started/tutorial-server-broadcast-with-signalr.md)를 참조 하세요. 이 동작은 변경 되지 않았습니다. 코드를 쉽게 테스트 하 고, 유지 관리 하 고, 발전 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebb0d-222">(For a description, see [Server Broadcast with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).) We haven't changed the behavior; just made the code easier to test, maintain, and evolve.</span></span>
