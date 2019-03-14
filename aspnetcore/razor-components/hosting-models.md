---
title: Razor 구성 요소 호스팅 모델
author: guardrex
description: 클라이언트 쪽 Blazor 및 서버 쪽 ASP.NET Core Razor 구성 요소 호스팅 모델을 이해 합니다.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/hosting-models
ms.openlocfilehash: d1e0c472d7d10eeb4cef0da735cf703c98dd1645
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57042440"
---
# <a name="razor-components-hosting-models"></a><span data-ttu-id="ec568-103">Razor 구성 요소 호스팅 모델</span><span class="sxs-lookup"><span data-stu-id="ec568-103">Razor Components hosting models</span></span>

<span data-ttu-id="ec568-104">[Daniel Roth](https://github.com/danroth27)</span><span class="sxs-lookup"><span data-stu-id="ec568-104">By [Daniel Roth](https://github.com/danroth27)</span></span>

<span data-ttu-id="ec568-105">Razor 구성 요소는 클라이언트 쪽에서 실행 하도록 설계 하는 웹 프레임 워크, WebAssembly 기반.NET 런타임 브라우저에서 (*Blazor*) 또는 ASP.NET Core에서 서버 쪽 (*ASP.NET Core Razor 구성 요소가*).</span><span class="sxs-lookup"><span data-stu-id="ec568-105">Razor Components is a web framework designed to run client-side in the browser on a WebAssembly-based .NET runtime (*Blazor*) or server-side in ASP.NET Core (*ASP.NET Core Razor Components*).</span></span> <span data-ttu-id="ec568-106">호스팅 모델, 앱 및 구성 요소 모델에 관계 없이 *동일 하 게 유지*합니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-106">Regardless of the hosting model, the app and component models *remain the same*.</span></span> <span data-ttu-id="ec568-107">이 문서에서는 사용 가능한 호스팅 모델을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-107">This article discusses the available hosting models.</span></span>

## <a name="client-side-hosting-model"></a><span data-ttu-id="ec568-108">클라이언트 쪽 호스팅 모델</span><span class="sxs-lookup"><span data-stu-id="ec568-108">Client-side hosting model</span></span>

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

<span data-ttu-id="ec568-109">Blazor의 주 호스팅 모델은 브라우저에서 실행 중인 클라이언트 쪽입니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-109">The principal hosting model for Blazor is running client-side in the browser.</span></span> <span data-ttu-id="ec568-110">이 모델에서는 Blazor 앱, 종속성 및.NET 런타임 브라우저 다운로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-110">In this model, the Blazor app, its dependencies, and the .NET runtime are downloaded to the browser.</span></span> <span data-ttu-id="ec568-111">해당 앱은 브라우저 UI 스레드에서 직접 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-111">The app is executed directly on the browser UI thread.</span></span> <span data-ttu-id="ec568-112">모든 UI 업데이트 및 이벤트 처리에는 동일한 프로세스 내에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-112">All UI updates and event handling happens within the same process.</span></span> <span data-ttu-id="ec568-113">정적 파일을 사용 하 여 모든 웹 서버 기본 설정으로 앱 자산을 배포할 수 있습니다 (참조 [호스트 및 배포](xref:host-and-deploy/razor-components/index)).</span><span class="sxs-lookup"><span data-stu-id="ec568-113">The app assets can be deployed as static files using whatever web server is preferred (see [Host and deploy](xref:host-and-deploy/razor-components/index)).</span></span>

![Blazor 클라이언트 측: Blazor 앱 브라우저 내에서 UI 스레드에서 실행 됩니다.](hosting-models/_static/client-side.png)

<span data-ttu-id="ec568-115">클라이언트 쪽 호스팅 모델을 사용 하 여 Blazor 앱을 만들려면 사용 합니다 **Blazor** 또는 **Blazor (ASP.NET Core 호스팅)** 프로젝트 템플릿 (`blazor` 또는 `blazorhosted` 를사용하는경우서식파일[새 dotnet](/dotnet/core/tools/dotnet-new) 명령 프롬프트에서 명령을).</span><span class="sxs-lookup"><span data-stu-id="ec568-115">To create a Blazor app using the client-side hosting model, use the **Blazor** or **Blazor (ASP.NET Core Hosted)** project templates (`blazor` or `blazorhosted` template when using the [dotnet new](/dotnet/core/tools/dotnet-new) command at a command prompt).</span></span> <span data-ttu-id="ec568-116">포함 된 *blazor.webassembly.js* 핸들 스크립트:</span><span class="sxs-lookup"><span data-stu-id="ec568-116">The included *blazor.webassembly.js* script handles:</span></span>

* <span data-ttu-id="ec568-117">.NET 런타임, 앱 및 해당 종속성을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-117">Downloading the .NET runtime, the app, and its dependencies.</span></span>
* <span data-ttu-id="ec568-118">앱을 실행 하려면 런타임 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-118">Initialization of the runtime to run the app.</span></span>

<span data-ttu-id="ec568-119">클라이언트 쪽 호스팅 모델에는 몇 가지 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-119">The client-side hosting model offers several benefits.</span></span> <span data-ttu-id="ec568-120">클라이언트 쪽 Blazor:</span><span class="sxs-lookup"><span data-stu-id="ec568-120">Client-side Blazor:</span></span>

* <span data-ttu-id="ec568-121">.NET 서버 쪽 종속성을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-121">Has no .NET server-side dependency.</span></span>
* <span data-ttu-id="ec568-122">풍부한 대화형 UI에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-122">Has a rich interactive UI.</span></span>
* <span data-ttu-id="ec568-123">클라이언트 리소스 및 기능을 최대한 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-123">Fully leverages client resources and capabilities.</span></span>
* <span data-ttu-id="ec568-124">오프 로드 서버에서 클라이언트로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-124">Offloads work from the server to the client.</span></span>
* <span data-ttu-id="ec568-125">오프 라인 시나리오를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-125">Supports offline scenarios.</span></span>

<span data-ttu-id="ec568-126">클라이언트 쪽 호스팅에 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-126">There are downsides to client-side hosting.</span></span> <span data-ttu-id="ec568-127">클라이언트 쪽 Blazor:</span><span class="sxs-lookup"><span data-stu-id="ec568-127">Client-side Blazor:</span></span>

* <span data-ttu-id="ec568-128">브라우저의 기능으로 앱을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-128">Restricts the app to the capabilities of the browser.</span></span>
* <span data-ttu-id="ec568-129">지원 되는 클라이언트 하드웨어 및 소프트웨어 (예를 들어, WebAssembly 지원)에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-129">Requires capable client hardware and software (for example, WebAssembly support).</span></span>
* <span data-ttu-id="ec568-130">로드 시간 더 오래 앱을 더 큰 다운로드 크기에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-130">Has a larger download size and longer app load time.</span></span>
* <span data-ttu-id="ec568-131">.NET 런타임 및 도구 지원 (예를 들어,.NET Standard 지원과 디버깅의 제한) 성숙 적습니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-131">Has less mature .NET runtime and tooling support (for example, limitations in .NET Standard support and debugging).</span></span>

<span data-ttu-id="ec568-132">Visual Studio에 포함 된 **Blazor (호스팅되는 ASP.NET Core)** WebAssembly에서 실행 되는 ASP.NET Core 서버에서 호스팅되는 Blazor 앱을 만들기 위한 프로젝트 템플릿.</span><span class="sxs-lookup"><span data-stu-id="ec568-132">Visual Studio includes the **Blazor (ASP.NET Core hosted)** project template for creating a Blazor app that runs on WebAssembly and is hosted on an ASP.NET Core server.</span></span> <span data-ttu-id="ec568-133">ASP.NET Core 앱 클라이언트로 Blazor 앱 역할 이지만 그렇지 않은 경우 별도 프로세스.</span><span class="sxs-lookup"><span data-stu-id="ec568-133">The ASP.NET Core app serves the Blazor app to clients but is otherwise a separate process.</span></span> <span data-ttu-id="ec568-134">클라이언트 쪽 Blazor 앱 웹 API 호출 또는 SignalR 연결을 사용 하 여 네트워크를 통해 서버를 조작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-134">The client-side Blazor app can interact with the server over the network using Web API calls or SignalR connections.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ec568-135">클라이언트 쪽 Blazor 앱을 IIS 하위 기능 앱으로 호스팅되는 ASP.NET Core 앱에서 제공 하는 경우 상속된 된 ASP.NET Core 모듈 처리기 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-135">If a client-side Blazor app is served by an ASP.NET Core app hosted as an IIS sub-app, disable the inherited ASP.NET Core Module handler.</span></span> <span data-ttu-id="ec568-136">Blazor 앱의 앱 기본 경로 설정 *index.html* IIS에서 하위 앱을 구성할 때 사용 하는 IIS 별칭에는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-136">Set the app base path in the Blazor app's *index.html* file to the IIS alias used when configuring the sub-app in IIS.</span></span>
>
> <span data-ttu-id="ec568-137">자세한 내용은 [앱 기본 경로](xref:host-and-deploy/razor-components/index#app-base-path)합니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-137">For more information, see [App base path](xref:host-and-deploy/razor-components/index#app-base-path).</span></span>

## <a name="server-side-hosting-model"></a><span data-ttu-id="ec568-138">서버 쪽 호스팅 모델</span><span class="sxs-lookup"><span data-stu-id="ec568-138">Server-side hosting model</span></span>

<span data-ttu-id="ec568-139">ASP.NET Core Razor 구성 요소 서버 쪽 호스팅 모델에서는 응용 프로그램 서버에서 ASP.NET Core 앱 내에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-139">In the ASP.NET Core Razor Components server-side hosting model, the app is executed on the server from within an ASP.NET Core app.</span></span> <span data-ttu-id="ec568-140">UI 업데이트, 이벤트 처리 및 JavaScript 호출은 SignalR 연결상에서 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-140">UI updates, event handling, and JavaScript calls are handled over a SignalR connection.</span></span>

![ASP.NET Core Razor 구성 요소 서버 측: 브라우저와 상호 작용 (ASP.NET Core 앱 내에서 호스팅) 앱 서버에서 SignalR 연결을 통해.](hosting-models/_static/server-side.png)

<span data-ttu-id="ec568-142">서버 쪽 호스팅 모델을 사용 하는 구성 요소 Razor 앱을 만들려면 사용 합니다 **Blazor (서버 쪽 ASP.NET Core에서)** 템플릿 (`blazorserver` 사용 하는 경우 [새 dotnet](/dotnet/core/tools/dotnet-new) 명령 프롬프트에서).</span><span class="sxs-lookup"><span data-stu-id="ec568-142">To create a Razor Components app using the server-side hosting model, use the **Blazor (Server-side in ASP.NET Core)** template (`blazorserver` when using [dotnet new](/dotnet/core/tools/dotnet-new) at a command prompt).</span></span> <span data-ttu-id="ec568-143">ASP.NET Core 앱을 Razor 구성 요소 서버 쪽 앱을 호스트 및 클라이언트가 연결 된 SignalR 끝점을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-143">An ASP.NET Core app hosts the Razor Components server-side app and sets up the SignalR endpoint where clients connect.</span></span> <span data-ttu-id="ec568-144">앱의를 참조 하는 ASP.NET Core 앱 `Startup` 추가할 클래스:</span><span class="sxs-lookup"><span data-stu-id="ec568-144">The ASP.NET Core app references the app's `Startup` class to add:</span></span>

* <span data-ttu-id="ec568-145">서버 쪽 구성 요소 Razor 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-145">Server-side Razor Components services.</span></span>
* <span data-ttu-id="ec568-146">요청 처리 파이프라인에 대 한 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-146">The app to the request handling pipeline.</span></span>

[!code-csharp[](hosting-models/samples_snapshot/Startup.cs?highlight=5,27)]

<span data-ttu-id="ec568-147">합니다 *blazor.server.js* 스크립트&dagger; 클라이언트 연결을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-147">The *blazor.server.js* script&dagger; establishes the client connection.</span></span> <span data-ttu-id="ec568-148">것은 앱의 책임 (예를 들어 네트워크 연결이) 발생할 경우 필요에 따라 앱 상태를 유지 및 복원입니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-148">It's the app's responsibility to persist and restore app state as required (for example, in the event of a lost network connection).</span></span>

<span data-ttu-id="ec568-149">서버 쪽 호스팅 모델에는 몇 가지 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-149">The server-side hosting model offers several benefits:</span></span>

* <span data-ttu-id="ec568-150">.NET을 사용 하 여 전체 응용 프로그램을 작성할 수 있습니다 하 고 C# 구성 요소 모델을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-150">Allows you to write your entire app with .NET and C# using the component model.</span></span>
* <span data-ttu-id="ec568-151">불필요 한 페이지 새로 고침을 방지 및 풍부한 대화형 느낌을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-151">Provides a rich interactive feel and avoids unnecessary page refreshes.</span></span>
* <span data-ttu-id="ec568-152">클라이언트 쪽 Blazor 앱과 앱 크기가 매우 작아 졌습니다 및 훨씬 빠르게 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-152">Has a significantly smaller app size than a client-side Blazor app and loads much faster.</span></span>
* <span data-ttu-id="ec568-153">구성 요소 논리는 모든.NET Core 호환 되는 Api를 사용 하는 등 서버 기능의 활용을 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-153">Component logic can take full advantage of server capabilities, including using any .NET Core compatible APIs.</span></span>
* <span data-ttu-id="ec568-154">도구, 디버깅와 같은 기존.NET 예상 대로 작동 하므로.NET Core에 서버에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-154">Runs on .NET Core on the server, so existing .NET tooling, such as debugging, works as expected.</span></span>
* <span data-ttu-id="ec568-155">씬 클라이언트와 함께 (예: 브라우저 WebAssembly 및 리소스를 지원 하지 않는 제한 된 장치).</span><span class="sxs-lookup"><span data-stu-id="ec568-155">Works with thin clients (for example, browsers that don't support WebAssembly and resource constrained devices).</span></span>

<span data-ttu-id="ec568-156">서버 쪽 호스팅에 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-156">There are downsides to server-side hosting:</span></span>

* <span data-ttu-id="ec568-157">더 높은 대기 시간에 있습니다. 모든 사용자 상호 작용을 네트워크 홉이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-157">Has higher latency: Every user interaction involves a network hop.</span></span>
* <span data-ttu-id="ec568-158">오프 라인 지원 되지 않습니다는 제공합니다. 클라이언트 연결에 실패 하면 앱 작동이 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-158">Offers no offline support: If the client connection fails, the app stops working.</span></span>
* <span data-ttu-id="ec568-159">확장성을 감소 되었습니다. 서버는 여러 클라이언트 연결을 관리 하 고 클라이언트 상태를 처리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-159">Has reduced scalability: The server must manage multiple client connections and handle client state.</span></span>
* <span data-ttu-id="ec568-160">앱을 제공 하는 ASP.NET Core 서버가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-160">Requires an ASP.NET Core server to serve the app.</span></span> <span data-ttu-id="ec568-161">(예: CDN)에서 서버 없이 배포 할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-161">Deployment without a server (for example, from a CDN) isn't possible.</span></span>

<span data-ttu-id="ec568-162">&dagger;합니다 *blazor.server.js* 스크립트는 다음 경로에 게시 됩니다. *bin / {디버그 | 릴리스} / {대상 프레임 워크} /publish/ {응용 프로그램 이름}. 앱/배포/_framework*합니다.</span><span class="sxs-lookup"><span data-stu-id="ec568-162">&dagger;The *blazor.server.js* script is published to the following path: *bin/{Debug|Release}/{TARGET FRAMEWORK}/publish/{APPLICATION NAME}.App/dist/_framework*.</span></span>
