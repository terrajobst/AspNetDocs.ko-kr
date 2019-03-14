---
title: Razor 구성 요소 종속성 주입
author: guardrex
description: Blazor 및 Razor 구성 요소 응용 프로그램 구성 요소를 삽입 하 여 기본 제공 서비스를 사용할 수 하는 방법을 참조 하세요.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/dependency-injection
ms.openlocfilehash: 6ce8fa74f20145f48797d267c20ef2593368b941
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57042430"
---
# <a name="razor-components-dependency-injection"></a><span data-ttu-id="865b2-103">Razor 구성 요소 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="865b2-103">Razor Components dependency injection</span></span>

<span data-ttu-id="865b2-104">[Rainer Stropek](https://www.timecockpit.com)</span><span class="sxs-lookup"><span data-stu-id="865b2-104">By [Rainer Stropek](https://www.timecockpit.com)</span></span>

<span data-ttu-id="865b2-105">[종속성 주입 (DI)](/aspnet/core/fundamentals/dependency-injection) 기본 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-105">[Dependency injection (DI)](/aspnet/core/fundamentals/dependency-injection) is built-in.</span></span> <span data-ttu-id="865b2-106">앱 구성 요소를 삽입 하 여 기본 제공 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-106">Apps can use built-in services by having them injected into components.</span></span> <span data-ttu-id="865b2-107">또한 앱 사용자 지정 서비스를 정의 하 고 DI를 통해 사용할 수 있도록 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-107">Apps can also define custom services and make them available via DI.</span></span>

## <a name="dependency-injection"></a><span data-ttu-id="865b2-108">종속성 주입</span><span class="sxs-lookup"><span data-stu-id="865b2-108">Dependency injection</span></span>

<span data-ttu-id="865b2-109">DI는 중앙 위치에 구성 된 서비스에 액세스 하기 위한 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-109">DI is a technique for accessing services configured in a central location.</span></span> <span data-ttu-id="865b2-110">이에 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-110">This can be useful to:</span></span>

* <span data-ttu-id="865b2-111">여러 구성 요소 간에 서비스 클래스의 단일 인스턴스를 공유 (라고는 *singleton* 서비스).</span><span class="sxs-lookup"><span data-stu-id="865b2-111">Share a single instance of a service class across many components (known as a *singleton* service).</span></span>
* <span data-ttu-id="865b2-112">특정 구체적인 서비스 클래스에서 구성 요소를 분리 하 고만 추상화를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-112">Decouple components from particular concrete service classes and only reference abstractions.</span></span> <span data-ttu-id="865b2-113">예를 들어 인터페이스 `IDataAccess` 구체적인 클래스로 구현 됩니다 `DataAccess`합니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-113">For example, an interface `IDataAccess` is implemented by a concrete class `DataAccess`.</span></span> <span data-ttu-id="865b2-114">구성 요소를 수신 하는 데 DI를 사용 하는 경우는 `IDataAccess` 구현, 구성 요소는 구체적인 형식 결합 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-114">When a component uses DI to receive an `IDataAccess` implementation, the component isn't coupled to the concrete type.</span></span> <span data-ttu-id="865b2-115">아마도 단위 테스트에서 모의 구현을 구현을 교환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-115">The implementation can be swapped, perhaps to a mock implementation in unit tests.</span></span>

<span data-ttu-id="865b2-116">DI 시스템은 구성 요소에는 서비스의 인스턴스를 제공 하는 일을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-116">The DI system is responsible for supplying instances of services to components.</span></span> <span data-ttu-id="865b2-117">DI는 종속성을 재귀적으로 해결 하 여 서비스 자체는 다른 서비스에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-117">DI also resolves dependencies recursively so that services themselves can depend on further services.</span></span> <span data-ttu-id="865b2-118">DI는 앱을 시작 하는 동안 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-118">DI is configured during startup of the app.</span></span> <span data-ttu-id="865b2-119">이 항목 뒷부분의 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-119">An example is shown later in this topic.</span></span>

## <a name="add-services-to-di"></a><span data-ttu-id="865b2-120">DI에 서비스 추가</span><span class="sxs-lookup"><span data-stu-id="865b2-120">Add services to DI</span></span>

<span data-ttu-id="865b2-121">새 앱을 만든 후 검사를 `Startup.ConfigureServices` 메서드:</span><span class="sxs-lookup"><span data-stu-id="865b2-121">After creating a new app, examine the `Startup.ConfigureServices` method:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Add custom services here
}
```

<span data-ttu-id="865b2-122">`ConfigureServices` 메서드에 전달 되는 [IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection), 서비스 설명자 개체의 목록입니다 ([ServiceDescriptor](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor)).</span><span class="sxs-lookup"><span data-stu-id="865b2-122">The `ConfigureServices` method is passed an [IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection), which is a list of service descriptor objects ([ServiceDescriptor](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor)).</span></span> <span data-ttu-id="865b2-123">서비스는 서비스 컬렉션에 대 한 서비스 설명자를 제공 하 여 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-123">Services are added by providing service descriptors to the service collection.</span></span> <span data-ttu-id="865b2-124">다음 코드 예제에서는 개념을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-124">The following code sample demonstrates the concept:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddSingleton<IDataAccess, DataAccess>();
}
```

<span data-ttu-id="865b2-125">서비스는 다음 수명을 사용 하 여 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-125">Services can be configured with the following lifetimes:</span></span>

| <span data-ttu-id="865b2-126">메서드</span><span class="sxs-lookup"><span data-stu-id="865b2-126">Method</span></span>      | <span data-ttu-id="865b2-127">설명</span><span class="sxs-lookup"><span data-stu-id="865b2-127">Description</span></span> |
| ----------- | ----------- |
| [<span data-ttu-id="865b2-128">Singleton</span><span class="sxs-lookup"><span data-stu-id="865b2-128">Singleton</span></span>](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.singleton#Microsoft_Extensions_DependencyInjection_ServiceDescriptor_Singleton__1_System_Func_System_IServiceProvider___0__) | <span data-ttu-id="865b2-129">DI 만듭니다는 *단일 인스턴스* 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-129">DI creates a *single instance* of the service.</span></span> <span data-ttu-id="865b2-130">이 서비스를 요구 하는 모든 구성 요소는이 인스턴스에 대 한 참조를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-130">All components requiring this service receive a reference to this instance.</span></span> |
| [<span data-ttu-id="865b2-131">Transient</span><span class="sxs-lookup"><span data-stu-id="865b2-131">Transient</span></span>](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.transient) | <span data-ttu-id="865b2-132">받을 때마다이 서비스를 실행 해야 하는 구성 요소에는 *새 인스턴스* 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-132">Whenever a component requires this service, it receives a *new instance* of the service.</span></span> |
| [<span data-ttu-id="865b2-133">Scoped</span><span class="sxs-lookup"><span data-stu-id="865b2-133">Scoped</span></span>](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.scoped) | <span data-ttu-id="865b2-134">현재 클라이언트 쪽 Blazor DI 범위 개념이 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-134">Client-side Blazor doesn't currently have the concept of DI scopes.</span></span> <span data-ttu-id="865b2-135">`Scoped` 처럼 `Singleton`합니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-135">`Scoped` behaves like `Singleton`.</span></span> <span data-ttu-id="865b2-136">그러나 ASP.NET Core Razor 구성 요소를 지원 합니다 `Scoped` 수명입니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-136">However, ASP.NET Core Razor Components support the `Scoped` lifetime.</span></span> <span data-ttu-id="865b2-137">Razor 구성 요소를 연결으로 범위가 지정 된 서비스를 등록 하는 범위가 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-137">In a Razor Component, a scoped service registration is scoped to the connection.</span></span> <span data-ttu-id="865b2-138">이러한 이유로 범위가 지정 된 서비스를 사용 하는 것이 좋습니다 서비스의 현재 사용자에 게 범위가 지정 되어야 합니다 (현재는 클라이언트 쪽에서 실행 하는 경우에 브라우저에서).</span><span class="sxs-lookup"><span data-stu-id="865b2-138">For this reason, using scoped services is preferred for services that should be scoped to the current user (even if the current intent is to run client-side in the browser).</span></span> |

<span data-ttu-id="865b2-139">DI 시스템은 ASP.NET Core에서 DI 시스템을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-139">The DI system is based on the DI system in ASP.NET Core.</span></span> <span data-ttu-id="865b2-140">자세한 내용은 [ASP.NET Core에서 종속성 주입](/aspnet/core/fundamentals/dependency-injection)합니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-140">For more information, see [Dependency injection in ASP.NET Core](/aspnet/core/fundamentals/dependency-injection).</span></span>

## <a name="default-services"></a><span data-ttu-id="865b2-141">기본 서비스</span><span class="sxs-lookup"><span data-stu-id="865b2-141">Default services</span></span>

<span data-ttu-id="865b2-142">기본 서비스는 자동으로 앱의 서비스 컬렉션에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-142">Default services are automatically added to the service collection of an app.</span></span> <span data-ttu-id="865b2-143">다음 표에서 제공 하는 유용한 기본 서비스 중 일부를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-143">The following table shows some of the useful default services provided.</span></span>

| <span data-ttu-id="865b2-144">메서드</span><span class="sxs-lookup"><span data-stu-id="865b2-144">Method</span></span>       | <span data-ttu-id="865b2-145">설명</span><span class="sxs-lookup"><span data-stu-id="865b2-145">Description</span></span> |
| ------------ | ----------- |
| [<span data-ttu-id="865b2-146">HttpClient</span><span class="sxs-lookup"><span data-stu-id="865b2-146">HttpClient</span></span>](/dotnet/api/system.net.http.httpclient) | <span data-ttu-id="865b2-147">HTTP 요청 송수신 (singleton) URI로 식별 되는 리소스에서 HTTP 응답에 대 한 메서드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-147">Provides methods for sending HTTP requests and receiving HTTP responses from a resource identified by a URI (singleton).</span></span> <span data-ttu-id="865b2-148">이 인스턴스의 `HttpClient` 브라우저를 사용 하 여 백그라운드에서 HTTP 트래픽을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-148">Note that this instance of `HttpClient` uses the browser for handling the HTTP traffic in the background.</span></span> <span data-ttu-id="865b2-149">[HttpClient.BaseAddress](/dotnet/api/system.net.http.httpclient.baseaddress) 앱의 기본 URI 접두사를 자동으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-149">[HttpClient.BaseAddress](/dotnet/api/system.net.http.httpclient.baseaddress) is automatically set to the base URI prefix of the app.</span></span> <span data-ttu-id="865b2-150">`HttpClient` 클라이언트 쪽 Blazor 앱에만 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-150">`HttpClient` is only provided to client-side Blazor apps.</span></span> |
| `IJSRuntime` | <span data-ttu-id="865b2-151">호출 될 수 있습니다 디스패치해야 하는 JavaScript 런타임 인스턴스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-151">Represents an instance of a JavaScript runtime to which calls may be dispatched.</span></span> <span data-ttu-id="865b2-152">자세한 내용은 <xref:razor-components/javascript-interop>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="865b2-152">For more information, see <xref:razor-components/javascript-interop>.</span></span> |
| `IUriHelper` | <span data-ttu-id="865b2-153">Uri 및 탐색 상태 (단일 항목)를 사용 하 여 작업 하기 위한 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-153">Helpers for working with URIs and navigation state (singleton).</span></span> <span data-ttu-id="865b2-154">`IUriHelper` 클라이언트 쪽 Blazor 및 ASP.NET Core Razor 구성 요소 앱을 모두 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-154">`IUriHelper` is provided to both client-side Blazor and ASP.NET Core Razor Components apps.</span></span> |

<span data-ttu-id="865b2-155">기본 템플릿에 의해 추가 되는 기본 서비스 공급자 대신 사용자 지정 서비스 공급자를 사용할 수 있는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-155">Note that it is possible to use a custom services provider instead of the default service provider that's added by the default template.</span></span> <span data-ttu-id="865b2-156">사용자 지정 서비스 공급자 표에 나열 된 기본 서비스를 자동으로 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-156">A custom service provider doesn't automatically provide the default services listed in the table.</span></span> <span data-ttu-id="865b2-157">이러한 서비스를 새 서비스 공급자에 명시적으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-157">Those services must be added to the new service provider explicitly.</span></span>

## <a name="request-a-service-in-a-component"></a><span data-ttu-id="865b2-158">구성 요소에서 서비스 요청</span><span class="sxs-lookup"><span data-stu-id="865b2-158">Request a service in a component</span></span>

<span data-ttu-id="865b2-159">서비스는 서비스 컬렉션에 추가 되 면 이러한 주입할 수 있습니다 사용 하 여 구성 요소 Razor 템플릿은 `@inject` Razor 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-159">Once services are added to the service collection, they can be injected into the components' Razor templates using the `@inject` Razor directive.</span></span> <span data-ttu-id="865b2-160">`@inject` 두 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-160">`@inject` has two parameters:</span></span>

* <span data-ttu-id="865b2-161">유형 이름: 삽입할 서비스의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-161">Type name: The type of the service to inject.</span></span>
* <span data-ttu-id="865b2-162">속성 이름: 삽입 된 app service를 수신 하는 속성의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-162">Property name: The name of the property receiving the injected app service.</span></span> <span data-ttu-id="865b2-163">참고 속성 수동으로 만들기를 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-163">Note that the property doesn't require manual creation.</span></span> <span data-ttu-id="865b2-164">컴파일러는 속성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-164">The compiler creates the property.</span></span>

<span data-ttu-id="865b2-165">여러 `@inject` 문은 다양 한 서비스 삽입을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-165">Multiple `@inject` statements can be used to inject different services.</span></span>

<span data-ttu-id="865b2-166">다음 예제에서는 `@inject`을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-166">The following example shows how to use `@inject`.</span></span> <span data-ttu-id="865b2-167">서비스 구현 `Services.IDataAccess` 구성 요소의 속성에 주입 됩니다 `DataRepository`합니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-167">The service implementing `Services.IDataAccess` is injected into the component's property `DataRepository`.</span></span> <span data-ttu-id="865b2-168">만 코드를 사용 하는 방식을 참고 합니다 `IDataAccess` 추상화 합니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-168">Note how the code is only using the `IDataAccess` abstraction:</span></span>

```csharp
@page "/customer-list"
@using Services
@inject IDataAccess DataRepository

<ul>
    @if (Customers != null)
    {
        @foreach (var customer in Customers)
        {
            <li>@customer.FirstName @customer.LastName</li>
        }
    }
</ul>

@functions {
    private IReadOnlyList<Customer> Customers;

    protected override async Task OnInitAsync()
    {
        // The property DataRepository received an implementation
        // of IDataAccess through dependency injection. Use 
        // DataRepository to obtain data from the server.
        Customers = await DataRepository.GetAllCustomersAsync();
    }
}
```

<span data-ttu-id="865b2-169">내부적으로 생성 된 속성 (`DataRepository`)으로 데코 레이트 된는 `InjectAttribute` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-169">Internally, the generated property (`DataRepository`) is decorated with the `InjectAttribute` attribute.</span></span> <span data-ttu-id="865b2-170">일반적으로이 특성을 직접 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-170">Typically, this attribute isn't used directly.</span></span> <span data-ttu-id="865b2-171">기본 클래스는 구성 요소에 필요한 경우 삽입 된 속성은 또한 필수 기본 클래스에 대 한 `InjectAttribute` 수동으로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-171">If a base class is required for components and injected properties are also required for the base class, `InjectAttribute` can be manually added:</span></span>

```csharp
public class ComponentBase : BlazorComponent
{
    // Dependency injection works even if using the
    // InjectAttribute in a component's base class.
    [Inject]
    protected IDataAccess DataRepository { get; set; }
    ...
}
```

<span data-ttu-id="865b2-172">기본 클래스에서 파생 된 구성 요소에는 `@inject` 지시문은 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-172">In components derived from the base class, the `@inject` directive isn't required.</span></span> <span data-ttu-id="865b2-173">`InjectAttribute` 기본 클래스는 충분 합니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-173">The `InjectAttribute` of the base class is sufficient:</span></span>

```csharp
@page "/demo"
@inherits ComponentBase

<h1>...</h1>
...
```

## <a name="dependency-injection-in-services"></a><span data-ttu-id="865b2-174">서비스에서 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="865b2-174">Dependency injection in services</span></span>

<span data-ttu-id="865b2-175">복잡 한 서비스에는 추가 서비스 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-175">Complex services might require additional services.</span></span> <span data-ttu-id="865b2-176">이전 예에서 `DataAccess` 필요할 수 있습니다는 `HttpClient` 기본 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-176">In the prior example, `DataAccess` might require the `HttpClient` default service.</span></span> <span data-ttu-id="865b2-177">`@inject` 또는 `InjectAttribute` 서비스에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-177">`@inject` or the `InjectAttribute` can't be used in services.</span></span> <span data-ttu-id="865b2-178">*생성자 주입* 대신 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-178">*Constructor injection* must be used instead.</span></span> <span data-ttu-id="865b2-179">필요한 서비스는 서비스의 생성자에 매개 변수를 추가 하 여 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-179">Required services are added by adding parameters to the service's constructor.</span></span> <span data-ttu-id="865b2-180">종속성 주입 된 서비스를 만들 때이 생성자에 필요 하며, 적절 하 게 제공 서비스 인식 합니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-180">When dependency injection creates the service, it recognizes the services it requires in the constructor and provides them accordingly.</span></span>

<span data-ttu-id="865b2-181">다음 코드 예제에서는 개념을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-181">The following code sample demonstrates the concept:</span></span>

```csharp
public class DataAccess : IDataAccess
{
    // The constructor receives an HttpClient via dependency
    // injection. HttpClient is a default service.
    public DataAccess(HttpClient client)
    {
        ...
    }
    ...
}
```

<span data-ttu-id="865b2-182">생성자 주입을 위한 다음 필수 조건을 note:</span><span class="sxs-lookup"><span data-stu-id="865b2-182">Note the following prerequisites for constructor injection:</span></span>

* <span data-ttu-id="865b2-183">인수 모두 수행할 수 있습니다 종속성 주입으로 생성자가 하나 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-183">There must be one constructor whose arguments can all be fulfilled by dependency injection.</span></span> <span data-ttu-id="865b2-184">DI에서 포함 하지 않는 추가 매개 변수는 기본 값에 지정 된 경우 허용 되는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-184">Note that additional parameters not covered by DI are allowed if default values are specified for them.</span></span>
* <span data-ttu-id="865b2-185">해당 생성자 없어야 *공용*합니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-185">The applicable constructor must be *public*.</span></span>
* <span data-ttu-id="865b2-186">해당 생성자가 하나 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-186">There must only be one applicable constructor.</span></span> <span data-ttu-id="865b2-187">모호성을 발생 시 DI에 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="865b2-187">In case of an ambiguity, DI throws an exception.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="865b2-188">추가 자료</span><span class="sxs-lookup"><span data-stu-id="865b2-188">Additional resources</span></span>

* [<span data-ttu-id="865b2-189">ASP.NET Core에서 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="865b2-189">Dependency injection in ASP.NET Core</span></span>](/aspnet/core/fundamentals/dependency-injection)
