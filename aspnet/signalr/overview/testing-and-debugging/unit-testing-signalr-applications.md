---
uid: signalr/overview/testing-and-debugging/unit-testing-signalr-applications
title: SignalR 응용 프로그램 단위 테스트 | Microsoft Docs
author: bradygaster
description: 이 문서에서는 SignalR 2.0의 유닛 테스트 기능을 사용 하는 방법을 설명 합니다.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: d1983524-e0d5-4ee6-9d87-1f552f7cb964
msc.legacyurl: /signalr/overview/testing-and-debugging/unit-testing-signalr-applications
msc.type: authoredcontent
ms.openlocfilehash: 2cf2e88f141d89971439dc1fc4979849f8dded47
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467303"
---
# <a name="unit-testing-signalr-applications"></a><span data-ttu-id="333ae-103">SignalR 애플리케이션 유닛 테스트</span><span class="sxs-lookup"><span data-stu-id="333ae-103">Unit Testing SignalR Applications</span></span>

<span data-ttu-id="333ae-104">[Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="333ae-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="333ae-105">이 문서에서는 SignalR 2의 유닛 테스트 기능을 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-105">This article describes using the Unit Testing features of SignalR 2.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="333ae-106">이 항목에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="333ae-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="333ae-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="333ae-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="333ae-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="333ae-108">.NET 4.5</span></span>
> - <span data-ttu-id="333ae-109">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="333ae-109">SignalR version 2</span></span>
>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="333ae-110">질문 및 설명</span><span class="sxs-lookup"><span data-stu-id="333ae-110">Questions and comments</span></span>
>
> <span data-ttu-id="333ae-111">이 자습서와 페이지 맨 아래에 있는 의견에서 개선할 수 있는 방법에 대 한 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="333ae-111">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="333ae-112">자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-112">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<a id="unit"></a>
## <a name="unit-testing-signalr-applications"></a><span data-ttu-id="333ae-113">SignalR 응용 프로그램 단위 테스트</span><span class="sxs-lookup"><span data-stu-id="333ae-113">Unit testing SignalR applications</span></span>

<span data-ttu-id="333ae-114">SignalR 2의 단위 테스트 기능을 사용 하 여 SignalR 응용 프로그램에 대 한 단위 테스트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-114">You can use the unit test features in SignalR 2 to create unit tests for your SignalR application.</span></span> <span data-ttu-id="333ae-115">SignalR 2에는 테스트를 위한 허브 메서드를 시뮬레이션 하기 위해 모의 개체를 만드는 데 사용할 수 있는 [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) 인터페이스가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-115">SignalR 2 includes the [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) interface, which can be used to create a mock object to simulate your hub methods for testing.</span></span>

<span data-ttu-id="333ae-116">이 섹션에서는 [XUnit.net](https://github.com/xunit/xunit) 및 [moq](https://github.com/Moq/moq4)를 사용 하 여 초보자를 위한 [자습서](../getting-started/tutorial-getting-started-with-signalr.md) 에서 만든 응용 프로그램에 대 한 단위 테스트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-116">In this section, you'll add unit tests for the application created in the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md) using [XUnit.net](https://github.com/xunit/xunit) and [Moq](https://github.com/Moq/moq4).</span></span>

<span data-ttu-id="333ae-117">XUnit.net는 테스트를 제어 하는 데 사용 됩니다. Moq는 테스트를 위한 [모의](http://en.wikipedia.org/wiki/Mock_object) 개체를 만드는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-117">XUnit.net will be used to control the test; Moq will be used to create a [mock](http://en.wikipedia.org/wiki/Mock_object) object for testing.</span></span> <span data-ttu-id="333ae-118">원하는 경우 다른 모의 프레임 워크를 사용할 수 있습니다. [Nsubstitute](http://nsubstitute.github.io/) 좋은 선택 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-118">Other mocking frameworks can be used if desired; [NSubstitute](http://nsubstitute.github.io/) is also a good choice.</span></span> <span data-ttu-id="333ae-119">이 자습서에서는 다음 두 가지 방법으로 모의 개체를 설정 하는 방법을 보여 줍니다. 첫 번째는 `dynamic` 개체 (.NET Framework 4에서 도입 됨)와 두 번째 인터페이스를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-119">This tutorial demonstrates how to set up the mock object in two ways: First, using a `dynamic` object (introduced in .NET Framework 4), and second, using an interface.</span></span>

### <a name="contents"></a><span data-ttu-id="333ae-120">콘텐츠</span><span class="sxs-lookup"><span data-stu-id="333ae-120">Contents</span></span>

<span data-ttu-id="333ae-121">이 자습서에는 다음과 같은 섹션이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-121">This tutorial contains the following sections.</span></span>

- [<span data-ttu-id="333ae-122">동적으로 단위 테스트</span><span class="sxs-lookup"><span data-stu-id="333ae-122">Unit testing with Dynamic</span></span>](#dynamic)
- [<span data-ttu-id="333ae-123">유형별 단위 테스트</span><span class="sxs-lookup"><span data-stu-id="333ae-123">Unit testing by type</span></span>](#type)

<a id="dynamic"></a>
### <a name="unit-testing-with-dynamic"></a><span data-ttu-id="333ae-124">동적으로 단위 테스트</span><span class="sxs-lookup"><span data-stu-id="333ae-124">Unit testing with Dynamic</span></span>

<span data-ttu-id="333ae-125">이 섹션에서는 동적 개체를 사용 하 여 초보자를 위한 [자습서](../getting-started/tutorial-getting-started-with-signalr.md) 에서 만든 응용 프로그램에 대 한 단위 테스트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-125">In this section, you'll add a unit test for the application created in the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md) using a dynamic object.</span></span>

1. <span data-ttu-id="333ae-126">Visual Studio 2013에 대 한 [Xunit Runner 확장](https://visualstudiogallery.msdn.microsoft.com/463c5987-f82b-46c8-a97e-b1cde42b9099) 을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-126">Install the [XUnit Runner extension](https://visualstudiogallery.msdn.microsoft.com/463c5987-f82b-46c8-a97e-b1cde42b9099) for Visual Studio 2013.</span></span>
2. <span data-ttu-id="333ae-127">초보자를 위한 [자습서](../getting-started/tutorial-getting-started-with-signalr.md)를 완료 하거나 [MSDN 코드 갤러리](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)에서 완성 된 응용 프로그램을 다운로드 하세요.</span><span class="sxs-lookup"><span data-stu-id="333ae-127">Either complete the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md), or download the completed application from [MSDN Code Gallery](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9).</span></span>
3. <span data-ttu-id="333ae-128">다운로드 버전의 시작 응용 프로그램을 사용 하는 경우 **패키지 관리자 콘솔** 을 열고 **복원** 을 클릭 하 여 SignalR 패키지를 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-128">If you are using the download version of the Getting Started application, open **Package Manager Console** and click **Restore** to add the SignalR package to the project.</span></span>

    ![패키지 복원](unit-testing-signalr-applications/_static/image1.png)
4. <span data-ttu-id="333ae-130">단위 테스트에 대 한 프로젝트를 솔루션에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-130">Add a project to the solution for the unit test.</span></span> <span data-ttu-id="333ae-131">**솔루션 탐색기** 에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **추가**, **새 프로젝트**...를 차례로 선택 합니다. **C#** 노드 아래에서 **Windows** 노드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-131">Right-click your solution in **Solution Explorer** and select **Add**, **New Project...**. Under the **C#** node, select the **Windows** node.</span></span> <span data-ttu-id="333ae-132">**클래스 라이브러리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-132">Select **Class Library**.</span></span> <span data-ttu-id="333ae-133">새 프로젝트의 이름을 **Testlibrary** 로 하 고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-133">Name the new project **TestLibrary** and click **OK**.</span></span>

    ![테스트 라이브러리 만들기](unit-testing-signalr-applications/_static/image2.png)
5. <span data-ttu-id="333ae-135">SignalRChat 프로젝트에 테스트 라이브러리 프로젝트에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-135">Add a reference in the test library project to the SignalRChat project.</span></span> <span data-ttu-id="333ae-136">**Testlibrary** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**, **참조 ...** 를 차례로 선택 합니다. **솔루션** 노드 아래에서 **프로젝트** 노드를 선택 하 고 **SignalRChat**를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-136">Right-click the **TestLibrary** project and select **Add**, **Reference...**. Select the **Projects** node under the **Solution** node, and check **SignalRChat**.</span></span> <span data-ttu-id="333ae-137">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-137">Click **OK**.</span></span>

    ![프로젝트 참조 추가](unit-testing-signalr-applications/_static/image3.png)
6. <span data-ttu-id="333ae-139">**Testlibrary** 프로젝트에 SignalR, Moq 및 xunit 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-139">Add the SignalR, Moq, and XUnit packages to the **TestLibrary** project.</span></span> <span data-ttu-id="333ae-140">**패키지 관리자 콘솔**에서 **기본 프로젝트** 드롭다운을 **testlibrary**로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-140">In the **Package Manager Console**, set the **Default Project** dropdown to **TestLibrary**.</span></span> <span data-ttu-id="333ae-141">콘솔 창에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-141">Run the following commands in the console window:</span></span>

   - `Install-Package Microsoft.AspNet.SignalR`
   - `Install-Package Moq`
   - `Install-Package XUnit`

     ![패키지 설치](unit-testing-signalr-applications/_static/image4.png)
7. <span data-ttu-id="333ae-143">테스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-143">Create the test file.</span></span> <span data-ttu-id="333ae-144">**Testlibrary** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가 ...** , **클래스**를 차례로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-144">Right-click the **TestLibrary** project and click **Add...**, **Class**.</span></span> <span data-ttu-id="333ae-145">새 클래스의 이름을 **Tests.cs**로 합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-145">Name the new class **Tests.cs**.</span></span>
8. <span data-ttu-id="333ae-146">Tests.cs의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-146">Replace the contents of Tests.cs with the following code.</span></span>

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample1.cs)]

    <span data-ttu-id="333ae-147">위의 코드에서 테스트 클라이언트는 [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) 형식의 [moq](https://github.com/Moq/moq4) 라이브러리의 `Mock` 개체를 사용 하 여 만듭니다 (SignalR 2.1에서 형식 매개 변수에 대 한 `dynamic` 할당). `IHubCallerConnectionContext` 인터페이스는 클라이언트에서 메서드를 호출 하는 데 사용 되는 프록시 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-147">In the code above, a test client is created using the `Mock` object from the [Moq](https://github.com/Moq/moq4) library, of type [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (in SignalR 2.1, assign `dynamic` for the type parameter.) The `IHubCallerConnectionContext` interface is the proxy object with which you invoke methods on the client.</span></span> <span data-ttu-id="333ae-148">그러면 `ChatHub` 클래스에서 호출할 수 있도록 `broadcastMessage` 함수가 모의 클라이언트에 대해 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-148">The `broadcastMessage` function is then defined for the mock client so that it can be called by the `ChatHub` class.</span></span> <span data-ttu-id="333ae-149">그런 다음 테스트 엔진은 `ChatHub` 클래스의 `Send` 메서드를 호출 합니다. 그러면이 메서드는 모의 `broadcastMessage` 함수를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-149">The test engine then calls the `Send` method of the `ChatHub` class, which in turn calls the mocked `broadcastMessage` function.</span></span>
9. <span data-ttu-id="333ae-150">**F6**키를 눌러 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-150">Build the solution by pressing **F6**.</span></span>
10. <span data-ttu-id="333ae-151">단위 테스트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-151">Run the unit test.</span></span> <span data-ttu-id="333ae-152">Visual Studio에서 **테스트**, **Windows**, **테스트 탐색기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-152">In Visual Studio, select **Test**, **Windows**, **Test Explorer**.</span></span> <span data-ttu-id="333ae-153">테스트 탐색기 창에서 **HubsAreMockableViaDynamic** 를 마우스 오른쪽 단추로 클릭 하 고 **선택한 테스트 실행**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-153">In the Test Explorer window, right-click **HubsAreMockableViaDynamic** and select **Run Selected Tests**.</span></span>

    ![테스트 탐색기](unit-testing-signalr-applications/_static/image5.png)
11. <span data-ttu-id="333ae-155">테스트 탐색기 창에서 아래쪽 창을 확인 하 여 테스트가 통과 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-155">Verify that the test passed by checking the lower pane in the Test Explorer window.</span></span> <span data-ttu-id="333ae-156">이 창에는 테스트 성공이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-156">The window will show that the test passed.</span></span>

    ![테스트 통과](unit-testing-signalr-applications/_static/image6.png)

<a id="type"></a>
### <a name="unit-testing-by-type"></a><span data-ttu-id="333ae-158">유형별 단위 테스트</span><span class="sxs-lookup"><span data-stu-id="333ae-158">Unit testing by type</span></span>

<span data-ttu-id="333ae-159">이 섹션에서는 테스트할 메서드가 포함 된 인터페이스를 사용 하 여 [시작 자습서](../getting-started/tutorial-getting-started-with-signalr.md) 에서 만든 응용 프로그램에 대 한 테스트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-159">In this section, you'll add a test for the application created in the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md) using an interface that contains the method to be tested.</span></span>

1. <span data-ttu-id="333ae-160">위의 [동적 자습서를 사용 하 여 단위 테스트](#dynamic) 에서 1-7 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-160">Complete steps 1-7 in the [Unit testing with Dynamic](#dynamic) tutorial above.</span></span>
2. <span data-ttu-id="333ae-161">Tests.cs의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-161">Replace the contents of Tests.cs with the following code.</span></span>

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample2.cs)]

    <span data-ttu-id="333ae-162">위의 코드에서는 테스트 엔진에서 모의 클라이언트를 만들 `broadcastMessage` 메서드의 시그니처를 정의 하는 인터페이스가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-162">In the code above, an interface is created defining the signature of the `broadcastMessage` method for which the test engine will create a mock client.</span></span> <span data-ttu-id="333ae-163">그런 다음 [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) 형식의 `Mock` 개체 (SignalR 2.1, 형식 매개 변수에 대 한 `dynamic` 할당)를 사용 하 여 모의 클라이언트를 만듭니다. `IHubCallerConnectionContext` 인터페이스는 클라이언트에서 메서드를 호출 하는 데 사용 되는 프록시 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-163">A mock client is then created using the `Mock` object, of type [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (in SignalR 2.1, assign `dynamic` for the type parameter.) The `IHubCallerConnectionContext` interface is the proxy object with which you invoke methods on the client.</span></span>

    <span data-ttu-id="333ae-164">그런 다음 테스트는 `ChatHub`의 인스턴스를 만든 다음 `broadcastMessage` 메서드의 모의 버전을 만듭니다 .이 버전은 허브에서 `Send` 메서드를 호출 하 여 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-164">The test then creates an instance of `ChatHub`, and then creates a mock version of the `broadcastMessage` method, which in turn is invoked by calling the `Send` method on the hub.</span></span>
3. <span data-ttu-id="333ae-165">**F6**키를 눌러 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-165">Build the solution by pressing **F6**.</span></span>
4. <span data-ttu-id="333ae-166">단위 테스트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-166">Run the unit test.</span></span> <span data-ttu-id="333ae-167">Visual Studio에서 **테스트**, **Windows**, **테스트 탐색기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-167">In Visual Studio, select **Test**, **Windows**, **Test Explorer**.</span></span> <span data-ttu-id="333ae-168">테스트 탐색기 창에서 **HubsAreMockableViaDynamic** 를 마우스 오른쪽 단추로 클릭 하 고 **선택한 테스트 실행**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-168">In the Test Explorer window, right-click **HubsAreMockableViaDynamic** and select **Run Selected Tests**.</span></span>

    ![테스트 탐색기](unit-testing-signalr-applications/_static/image7.png)
5. <span data-ttu-id="333ae-170">테스트 탐색기 창에서 아래쪽 창을 확인 하 여 테스트가 통과 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-170">Verify that the test passed by checking the lower pane in the Test Explorer window.</span></span> <span data-ttu-id="333ae-171">이 창에는 테스트 성공이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="333ae-171">The window will show that the test passed.</span></span>

    ![테스트 통과](unit-testing-signalr-applications/_static/image8.png)
