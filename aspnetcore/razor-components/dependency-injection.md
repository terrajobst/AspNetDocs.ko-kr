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
# <a name="razor-components-dependency-injection"></a>Razor 구성 요소 종속성 주입

[Rainer Stropek](https://www.timecockpit.com)

[종속성 주입 (DI)](/aspnet/core/fundamentals/dependency-injection) 기본 제공 됩니다. 앱 구성 요소를 삽입 하 여 기본 제공 서비스를 사용할 수 있습니다. 또한 앱 사용자 지정 서비스를 정의 하 고 DI를 통해 사용할 수 있도록 수 있습니다.

## <a name="dependency-injection"></a>종속성 주입

DI는 중앙 위치에 구성 된 서비스에 액세스 하기 위한 기술입니다. 이에 유용할 수 있습니다.

* 여러 구성 요소 간에 서비스 클래스의 단일 인스턴스를 공유 (라고는 *singleton* 서비스).
* 특정 구체적인 서비스 클래스에서 구성 요소를 분리 하 고만 추상화를 참조 합니다. 예를 들어 인터페이스 `IDataAccess` 구체적인 클래스로 구현 됩니다 `DataAccess`합니다. 구성 요소를 수신 하는 데 DI를 사용 하는 경우는 `IDataAccess` 구현, 구성 요소는 구체적인 형식 결합 되지 않습니다. 아마도 단위 테스트에서 모의 구현을 구현을 교환할 수 있습니다.

DI 시스템은 구성 요소에는 서비스의 인스턴스를 제공 하는 일을 담당 합니다. DI는 종속성을 재귀적으로 해결 하 여 서비스 자체는 다른 서비스에 따라 달라질 수 있습니다. DI는 앱을 시작 하는 동안 구성 됩니다. 이 항목 뒷부분의 예가 나와 있습니다.

## <a name="add-services-to-di"></a>DI에 서비스 추가

새 앱을 만든 후 검사를 `Startup.ConfigureServices` 메서드:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Add custom services here
}
```

`ConfigureServices` 메서드에 전달 되는 [IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection), 서비스 설명자 개체의 목록입니다 ([ServiceDescriptor](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor)). 서비스는 서비스 컬렉션에 대 한 서비스 설명자를 제공 하 여 추가 됩니다. 다음 코드 예제에서는 개념을 보여 줍니다.

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddSingleton<IDataAccess, DataAccess>();
}
```

서비스는 다음 수명을 사용 하 여 구성할 수 있습니다.

| 메서드      | 설명 |
| ----------- | ----------- |
| [Singleton](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.singleton#Microsoft_Extensions_DependencyInjection_ServiceDescriptor_Singleton__1_System_Func_System_IServiceProvider___0__) | DI 만듭니다는 *단일 인스턴스* 서비스입니다. 이 서비스를 요구 하는 모든 구성 요소는이 인스턴스에 대 한 참조를 받습니다. |
| [Transient](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.transient) | 받을 때마다이 서비스를 실행 해야 하는 구성 요소에는 *새 인스턴스* 서비스입니다. |
| [Scoped](/dotnet/api/microsoft.extensions.dependencyinjection.servicedescriptor.scoped) | 현재 클라이언트 쪽 Blazor DI 범위 개념이 필요는 없습니다. `Scoped` 처럼 `Singleton`합니다. 그러나 ASP.NET Core Razor 구성 요소를 지원 합니다 `Scoped` 수명입니다. Razor 구성 요소를 연결으로 범위가 지정 된 서비스를 등록 하는 범위가 지정 됩니다. 이러한 이유로 범위가 지정 된 서비스를 사용 하는 것이 좋습니다 서비스의 현재 사용자에 게 범위가 지정 되어야 합니다 (현재는 클라이언트 쪽에서 실행 하는 경우에 브라우저에서). |

DI 시스템은 ASP.NET Core에서 DI 시스템을 기반으로 합니다. 자세한 내용은 [ASP.NET Core에서 종속성 주입](/aspnet/core/fundamentals/dependency-injection)합니다.

## <a name="default-services"></a>기본 서비스

기본 서비스는 자동으로 앱의 서비스 컬렉션에 추가 됩니다. 다음 표에서 제공 하는 유용한 기본 서비스 중 일부를 보여 줍니다.

| 메서드       | 설명 |
| ------------ | ----------- |
| [HttpClient](/dotnet/api/system.net.http.httpclient) | HTTP 요청 송수신 (singleton) URI로 식별 되는 리소스에서 HTTP 응답에 대 한 메서드를 제공 합니다. 이 인스턴스의 `HttpClient` 브라우저를 사용 하 여 백그라운드에서 HTTP 트래픽을 처리 합니다. [HttpClient.BaseAddress](/dotnet/api/system.net.http.httpclient.baseaddress) 앱의 기본 URI 접두사를 자동으로 설정 됩니다. `HttpClient` 클라이언트 쪽 Blazor 앱에만 제공 됩니다. |
| `IJSRuntime` | 호출 될 수 있습니다 디스패치해야 하는 JavaScript 런타임 인스턴스를 나타냅니다. 자세한 내용은 <xref:razor-components/javascript-interop>을 참조하세요. |
| `IUriHelper` | Uri 및 탐색 상태 (단일 항목)를 사용 하 여 작업 하기 위한 도우미입니다. `IUriHelper` 클라이언트 쪽 Blazor 및 ASP.NET Core Razor 구성 요소 앱을 모두 제공 됩니다. |

기본 템플릿에 의해 추가 되는 기본 서비스 공급자 대신 사용자 지정 서비스 공급자를 사용할 수 있는 참고 합니다. 사용자 지정 서비스 공급자 표에 나열 된 기본 서비스를 자동으로 제공 하지 않습니다. 이러한 서비스를 새 서비스 공급자에 명시적으로 추가 합니다.

## <a name="request-a-service-in-a-component"></a>구성 요소에서 서비스 요청

서비스는 서비스 컬렉션에 추가 되 면 이러한 주입할 수 있습니다 사용 하 여 구성 요소 Razor 템플릿은 `@inject` Razor 지시문입니다. `@inject` 두 매개 변수가 있습니다.

* 유형 이름: 삽입할 서비스의 형식입니다.
* 속성 이름: 삽입 된 app service를 수신 하는 속성의 이름입니다. 참고 속성 수동으로 만들기를 필요 하지 않습니다. 컴파일러는 속성을 만듭니다.

여러 `@inject` 문은 다양 한 서비스 삽입을 사용할 수 있습니다.

다음 예제에서는 `@inject`을 사용하는 방법을 보여 줍니다. 서비스 구현 `Services.IDataAccess` 구성 요소의 속성에 주입 됩니다 `DataRepository`합니다. 만 코드를 사용 하는 방식을 참고 합니다 `IDataAccess` 추상화 합니다.

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

내부적으로 생성 된 속성 (`DataRepository`)으로 데코 레이트 된는 `InjectAttribute` 특성입니다. 일반적으로이 특성을 직접 사용 되지 않습니다. 기본 클래스는 구성 요소에 필요한 경우 삽입 된 속성은 또한 필수 기본 클래스에 대 한 `InjectAttribute` 수동으로 추가할 수 있습니다.

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

기본 클래스에서 파생 된 구성 요소에는 `@inject` 지시문은 필요 하지 않습니다. `InjectAttribute` 기본 클래스는 충분 합니다.

```csharp
@page "/demo"
@inherits ComponentBase

<h1>...</h1>
...
```

## <a name="dependency-injection-in-services"></a>서비스에서 종속성 주입

복잡 한 서비스에는 추가 서비스 필요할 수 있습니다. 이전 예에서 `DataAccess` 필요할 수 있습니다는 `HttpClient` 기본 서비스입니다. `@inject` 또는 `InjectAttribute` 서비스에서 사용할 수 없습니다. *생성자 주입* 대신 사용 해야 합니다. 필요한 서비스는 서비스의 생성자에 매개 변수를 추가 하 여 추가 됩니다. 종속성 주입 된 서비스를 만들 때이 생성자에 필요 하며, 적절 하 게 제공 서비스 인식 합니다.

다음 코드 예제에서는 개념을 보여 줍니다.

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

생성자 주입을 위한 다음 필수 조건을 note:

* 인수 모두 수행할 수 있습니다 종속성 주입으로 생성자가 하나 있어야 합니다. DI에서 포함 하지 않는 추가 매개 변수는 기본 값에 지정 된 경우 허용 되는 참고 합니다.
* 해당 생성자 없어야 *공용*합니다.
* 해당 생성자가 하나 여야 합니다. 모호성을 발생 시 DI에 예외가 throw 됩니다.

## <a name="additional-resources"></a>추가 자료

* [ASP.NET Core에서 종속성 주입](/aspnet/core/fundamentals/dependency-injection)
