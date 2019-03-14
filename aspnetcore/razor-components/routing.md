---
title: 라우팅 razor 구성 요소
author: guardrex
description: 앱에 NavLink 구성 요소에 대 한 요청을 라우팅하는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/01/2019
uid: razor-components/routing
ms.openlocfilehash: 5c648ba1bb3846f5baa515e808a98a3b33f81438
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57031610"
---
# <a name="razor-components-routing"></a>라우팅 razor 구성 요소

[Luke Latham](https://github.com/guardrex)으로

앱에 NavLink 구성 요소에 대 한 요청을 라우팅하는 방법에 알아봅니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) ([다운로드 방법](xref:index#how-to-download-a-sample)) 필수 구성 요소는 [시작](xref:razor-components/get-started) 항목을 참조하세요.

## <a name="route-templates"></a>경로 템플릿

`<Router>` 구성 요소를 사용 하면 라우팅 및 경로 템플릿에 액세스할 수 있는 각 구성 요소에 제공 됩니다. 합니다 `<Router>` 구성 요소에 표시 되는 *App.cshtml* 파일:

```cshtml
<Router AppAssembly=typeof(Program).Assembly />
```

때를  *\*.cshtml* 파일을 `@page` 지시문 컴파일됩니다, 생성된 된 클래스는 지정 된을 [RouteAttribute](/dotnet/api/microsoft.aspnetcore.mvc.routeattribute) 경로 템플릿을 지정 합니다. 런타임 시 사용 하 여 구성 요소 클래스에 대 한 라우터 찾습니다는 `RouteAttribute` 하 고 어떤 구성 요소는 요청 된 URL과 일치 하는 경로 템플릿을 렌더링 합니다.

여러 경로 템플릿 구성 요소에 적용할 수 있습니다. 에 [샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/), 다음 구성 요소에 대 한 요청에 응답할 `/BlazorRoute` 및 `/DifferentBlazorRoute`합니다.

*Pages/BlazorRoute.cshtml*:

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/BlazorRoute.cshtml?start=1&end=4)]

`<Router>` 확인할 때 요청 된 경로 렌더링에 대 한 대체 (fallback) 구성 요소를 설정 하는 지원 되지 않습니다. 설정 하 여이 옵트인 시나리오를 사용 하도록 설정 된 `FallbackComponent` 대체 (fallback) 구성 요소 클래스의 형식 매개 변수입니다.

다음 예제에서는 설정에 정의 된 구성 요소 *Pages/MyFallbackRazorComponent.cshtml* 에 대 한 대체 (fallback) 구성 요소로 `<Router>`:

```cshtml
<Router ... FallbackComponent="typeof(Pages.MyFallbackRazorComponent)" />
```

> [!IMPORTANT]
> 경로 올바르게 생성 하려면 앱을 포함 해야 합니다는 `<base>` 태그 해당 *wwwroot/index.html* 에 지정 된 앱 기본 경로 사용 하 여 파일을 `href` 특성 (`<base href="/" />`). 자세한 내용은 참조 하세요. [호스트 및 배포 합니다. 앱 기본 경로](xref:host-and-deploy/razor-components/index#app-base-path)합니다.

## <a name="route-parameters"></a>경로 매개 변수

라우터 경로 매개 변수를 사용 하 여 동일한 이름 (대/소문자 구분)를 사용 하 여 해당 구성 요소 매개 변수를 채웁니다.

*Pages/RouteParameter.cshtml*:

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/RouteParameter.cshtml?start=1&end=8)]

선택적 매개 변수는 아직 지원 되지 않습니다 하므로 두 `@page` 지시문 위의 예제에 적용 됩니다. 첫 번째 매개 변수 없이 구성 요소에 대 한 탐색을 허용합니다. 두 번째 `@page` 지시문은 합니다 `{text}` 경로 매개 변수 및 값을 할당 합니다 `Text` 속성입니다.

## <a name="route-constraints"></a>경로 제약 조건

경로 제약 조건 형식 구성 요소에 경로 세그먼트에서 일치를 적용 합니다.

다음 예에서 경로 사용자 구성 요소를 경우에 일치 합니다.

* `Id` 경로 세그먼트는 요청 URL에 존재 합니다.
* 합니다 `Id` 세그먼트는 정수 (`int`).

```cshtml
@page "/Users/{Id:int}"

<h1>The user Id is @Id!</h1>

@functions {
    [Parameter]
    private int Id { get; set; }
}
```

다음 표에 표시 된 경로 제약 조건을 사용할 수 있습니다. 고정 문화권을 사용 하 여 일치 하는 경로 제약 조건에 대 한이 경고 테이블에 대 한 자세한 내용은 아래를 참조 하세요.

| 제약 조건 | 예제           | 일치하는 예제                                                                  | 고정<br>culture<br>일치 |
| ---------- | ----------------- | -------------------------------------------------------------------------------- | :------------------------------: |
| `bool`     | `{active:bool}`   | `true`, `FALSE`                                                                  | 아니요                               |
| `datetime` | `{dob:datetime}`  | `2016-12-31`, `2016-12-31 7:32pm`                                                | 예                              |
| `decimal`  | `{price:decimal}` | `49.99`, `-1,000.01`                                                             | 예                              |
| `double`   | `{weight:double}` | `1.234`, `-1,001.01e8`                                                           | 예                              |
| `float`    | `{weight:float}`  | `1.234`, `-1,001.01e8`                                                           | 예                              |
| `guid`     | `{id:guid}`       | `CD2C1638-1638-72D5-1638-DEADBEEF1638`, `{CD2C1638-1638-72D5-1638-DEADBEEF1638}` | 아니요                               |
| `int`      | `{id:int}`        | `123456789`, `-123456789`                                                        | 예                              |
| `long`     | `{ticks:long}`    | `123456789`, `-123456789`                                                        | 예                              |

> [!WARNING]
> CLR 형식(예: `int` 또는 `DateTime`)으로 변환되는 URL을 확인하는 경로 제약 조건은 항상 고정 문화권을 사용합니다. 이러한 제약 조건은 URL은 지역화될 수 없다고 가정합니다.

## <a name="navlink-component"></a>NavLink 구성 요소

HTML 대신 NavLink 구성 요소를 사용  **\<는 >** 탐색 링크를 만들 때 요소입니다. NavLink 구성 요소 처럼를  **\<는 >** 요소를 설정/해제 하는 점을 제외 하 고는 `active` CSS 클래스에 따라 해당 `href` 현재 URL과 일치 합니다. `active` 클래스는 사용자는 페이지는 표시 된 탐색 링크 간에 활성 페이지를 이해 합니다.

NavMenu 구성 요소를 [샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) 만듭니다는 [부트스트랩](https://getbootstrap.com/docs/) NavLink 구성 요소를 사용 하는 방법에 설명 하는 탐색 모음입니다. 다음 태그에서 처음 두 NavLinks를 표시 합니다 *Shared/NavMenu.cshtml* 파일입니다.

[!code-cshtml[](common/samples/3.x/BlazorSample/Shared/NavMenu.cshtml?start=13&end=24&highlight=4-6,9-11)]

두 개의 `NavLinkMatch` 옵션:

* `NavLinkMatch.All` &ndash; 전체 현재 URL 일치 하는 경우는 NavLink 해야 활성 수를 지정 합니다.
* `NavLinkMatch.Prefix` &ndash; NavLink 함을 active 현재 URL의 접두사를 벗어난 일치할 경우를 지정 합니다.

위의 예에서 홈 NavLink (`href=""`) 모든 Url과 일치 하 고 항상 수신 된 `active` CSS 클래스입니다. 두 번째 NavLink 데이터만 수신 합니다 `active` BlazorRoute 구성 요소를 방문 하는 사용자 클래스 (`href="BlazorRoute"`).
