---
title: Razor 구성 요소가 JavaScript interop
author: guardrex
description: .NET 및.NET에서 JavaScript 함수를 호출 하는 방법을 알아봅니다 Blazor 및 Razor 구성 요소 앱에서 JavaScript에서 메서드.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/javascript-interop
ms.openlocfilehash: 9f822fee8990b03ff15ffa9857a2ddd95328a6ce
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57050370"
---
# <a name="razor-components-javascript-interop"></a>Razor 구성 요소가 JavaScript interop

하 여 [Javier Calvarro 박](https://github.com/javiercn)하십시오 [Daniel Roth](https://github.com/danroth27), 및 [Luke Latham](https://github.com/guardrex)

구성 요소 Razor 앱을.NET 및.NET에서 JavaScript 함수를 호출할 수 JavaScript 코드에서 메서드.

## <a name="invoke-javascript-functions-from-net-methods"></a>.NET 메서드에서 JavaScript 함수를 호출 합니다.

.NET 코드를 JavaScript 함수를 호출 해야 하는 경우 경우가 있습니다. 예를 들어 JavaScript 호출을 브라우저 기능 또는 앱에 JavaScript 라이브러리에서 기능을 노출할 수 있습니다.

.NET에서 JavaScript로 호출을 사용 하 여는 `IJSRuntime` 추상화 합니다. 합니다 `InvokeAsync<T>` 메서드를 `IJSRuntime` 와 임의 개수의 JSON 직렬화 가능 인수를 호출 하려면 JavaScript 함수에 대 한 식별자를 사용 합니다. 전역 범위와 관련 된 함수 식별자가 (`window`). 호출 하려는 경우 `window.someScope.someFunction`, 식별자가 `someScope.someFunction`합니다. 가 호출 되기 전에 함수를 등록 하려면 않아도가 됩니다. 반환 형식은 `T` 도 JSON 직렬화 해야 합니다.

서버 쪽 ASP.NET Core Razor 구성 요소 앱:

* 서버 쪽 앱에서 여러 사용자 요청을 처리 합니다. 호출 하지 마십시오 `JSRuntime.Current` JavaScript 함수를 호출 하는 구성 요소에 있습니다.
* 삽입 된 `IJSRuntime` 추상화 및 JavaScript interop 호출에 삽입 된 개체를 사용 하 여 합니다.

다음 예제는 기반 [TextDecoder](https://developer.mozilla.org/docs/Web/API/TextDecoder), 실험적 JavaScript 기반 디코더는 합니다. JavaScript 함수를 호출 하는 방법을 보여 줍니다는 C# 메서드. JavaScript 함수에서 바이트 배열을 취하는 C# 메서드를 배열의 디코딩하고 표시에 대 한 구성 요소에 텍스트를 반환 합니다.

내 합니다 `<head>` 요소의 *wwwroot/index.html*를 사용 하는 함수를 제공 `TextDecoder` 전달 된 배열을 디코드 하려면:

```html
<script>
  window.ConvertArray = (win1251Array) => {
    var win1251decoder = new TextDecoder('windows-1251');
    var bytes = new Uint8Array(win1251Array);
    var decodedArray = win1251decoder.decode(bytes);
    console.log(decodedArray);
    return decodedArray;
  };
</script>
```

앞의 예제에 표시 된 코드와 같은 JavaScript 코드를 스크립트 파일에 대 한 참조를 사용 하 여 JavaScript 파일에서 로드할 수도 있습니다는 *wwwroot/index.html* 파일입니다.

다음 구성 요소:

* 호출 하는 `ConvertArray` JavaScript 함수를 사용 하 여 `JsRuntime` 구성 단추 (**변환 배열**) 선택 합니다.
* JavaScript 함수를 호출한 다음 전달된 된 배열은 문자열로 변환 됩니다. 표시에 대 한 구성 요소에는 문자열이 반환 됩니다.

```cshtml
@page "/"
@using Microsoft.JSInterop;
@inject IJSRuntime JsRuntime;

<h1>Call JavaScript Function Example</h1>

<button type="button" class="btn btn-primary" onclick="@ConvertArray">
    Convert Array
</button>

<p class="mt-2" style="font-size:1.6em">
    <span class="badge badge-success">
        @ConvertedText
    </span>
</p>

@functions {
    // Quote (c)2005 Universal Pictures: Serenity
    // https://www.uphe.com/movies/serenity
    // David Krumholtz on IMDB: https://www.imdb.com/name/nm0472710/

    private MarkupString ConvertedText =
        new MarkupString("Select the <b>Convert Array</b> button.");

    private uint[] QuoteArray = new uint[]
        {
            60, 101, 109, 62, 67, 97, 110, 39, 116, 32, 115, 116, 111, 112, 32,
            116, 104, 101, 32, 115, 105, 103, 110, 97, 108, 44, 32, 77, 97,
            108, 46, 60, 47, 101, 109, 62, 32, 45, 32, 77, 114, 46, 32, 85, 110,
            105, 118, 101, 114, 115, 101, 10, 10,
        };

    async void ConvertArray()
    {
        var text =
            await JsRuntime.InvokeAsync<string>("ConvertArray", QuoteArray);

        ConvertedText = new MarkupString(text);

        StateHasChanged();
    }
}
```

클라이언트 쪽 Blazor 앱에 대 한는 `IJSRuntime` 추상화에서 액세스할 수 `JSRuntime.Current`,이 현재 사용자의 요청을 가리킵니다. 클라이언트 쪽 Blazor 앱의 사용자만 이기 때문에 사용 하 여 `JSRuntime.Current` 호출할 JavaScript 함수 정상적으로 작동 합니다. 만 사용 하 여 `JSRuntime.Current` 클라이언트 쪽 Blazor 앱에서.

이 항목과 관련 된 클라이언트 쪽 샘플 앱에서 두 JavaScript 함수는 사용자 입력을 받는 환영 메시지를 표시 하는 DOM과 상호 작용 하는 클라이언트 쪽 앱에 사용할 수 있습니다.

* `showPrompt` &ndash; 사용자 입력 (사용자 이름)를 수락할 프롬프트를 생성 하 고 호출자에 게 이름을 반환 합니다.
* `displayWelcome` &ndash; 환영 메시지를 호출자에서 사용 하 여 DOM 개체를 할당 한 `id` 의 `welcome`합니다.

*wwwroot/exampleJsInterop.js*:

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=2-7)]

위치는 `<script>` JavaScript 파일에서 참조 하는 태그를 *wwwroot/index.html* 파일:

[!code-html[](./common/samples/3.x/BlazorSample/wwwroot/index.html?highlight=16)]

스크립트 태그를 동적으로 업데이트할 수 없으므로 구성 요소 파일에 스크립트 태그를 놓지 마십시오.

호출 하 여 JavaScript 함수를 사용 하 여.NET 메서드 interop `InvokeAsync<T>` 메서드를 `IJSRuntime`입니다.

샘플 앱에서는 한 쌍의 C# 메서드를 `Prompt` 하 고 `Display`를 호출 하는 `showPrompt` 및 `displayWelcome` JavaScript 함수:

*JsInteropClasses/ExampleJsInterop.cs*:

[!code-csharp[](./common/samples/3.x/BlazorSample/JsInteropClasses/ExampleJsInterop.cs?name=snippet1&highlight=6-8,14-16)]

`IJSRuntime` 추상화는 비동기 서버 쪽 시나리오에 대 한 허용 하도록 합니다. 클라이언트 쪽 앱이 실행 되는 JavaScript 함수를 동기적으로 호출 하려는 경우에 다운 `IJSInProcessRuntime` 호출 `Invoke<T>` 대신 합니다. 대부분의 JavaScript 라이브러리를 interop 사용 하 여 비동기 Api 라이브러리를 확인 하는 모든 시나리오에서 클라이언트 쪽 또는 서버 쪽에서 사용할 수 있는 것이 좋습니다.

JS interop을 보여 주기 위해 구성 요소를 포함 하는 샘플 앱입니다. 구성 요소:

* JS 프롬프트를 통해 사용자 입력을 받습니다.
* 처리에 대 한 구성 요소에 텍스트를 반환합니다.
* 시작 메시지를 표시 하려면 DOM과 상호 작용 하는 두 번째 JS 함수를 호출 합니다.

*Pages/JSInterop.cshtml*:

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?start=1&end=21&highlight=2-3,9-11,13,16-20)]

1. 때 `TriggerJsPrompt` 구성 요소를 선택 하 여 실행 됩니다 **트리거 JavaScript 프롬프트** 단추를 `ExampleJsInterop.Prompt` 에서 메서드 C# 코드를 호출 합니다.
1. `Prompt` 메서드가 실행 된 JavaScript `showPrompt` 함수는 *wwwroot/exampleJsInterop.js* 파일입니다.
1. 합니다 `showPrompt` HTML 인코딩 및 반환 되는 사용자 입력 (사용자 이름)을 허용 하는 함수는 `Prompt` 메서드 궁극적으로 구성 요소 다시 합니다. 구성 요소를 로컬 변수에 사용자 이름을 저장 `name`합니다.
1. 문자열에 저장 `name` 초에 전달 되는 환영 메시지는 통합 C# 메서드를 `ExampleJsInterop.Display`합니다.
1. `Display` JavaScript 함수를 호출 `displayWelcome`를 환영 메시지 머리글 태그로 렌더링 합니다.

## <a name="capture-references-to-elements"></a>요소에 대 한 참조를 캡처

일부 [JavaScript interop](xref:razor-components/javascript-interop) 시나리오에는 HTML 요소에 대 한 참조가 필요 합니다. 예를 들어, UI 라이브러리 요소 참조를 초기화 해야 할 수 있습니다 또는 같은 요소에 대해 비슷한 Api를 호출 해야 할 수 있습니다 `focus` 또는 `play`합니다.

구성 요소에서 HTML 요소에 대 한 참조를 추가 하 여 캡처할 수 있습니다는 `ref` HTML 요소에 특성 및 다음 형식의 필드를 정의할 `ElementRef` 이름이 값과 일치는 `ref` 특성입니다.

다음 예제에서는 사용자 입력된 요소에 대 한 참조를 캡처를 보여 줍니다.

```csharp
<input ref="username" ... />

@functions {
    ElementRef username;
}
```

> [!NOTE]
> 수행할 **되지** DOM을 채우는 방법으로 캡처된 요소 참조를 사용 합니다. 이렇게 선언적 렌더링 모델을 방해할 수 있습니다.

.NET 코드와 관련 된 관련해 서는 `ElementRef` 불투명 핸들입니다. 합니다 *만* 것으로 할 수 있는 점은 JavaScript interop을 통해 JavaScript 코드를 통해 전달 합니다. 이렇게 하면 JavaScript 쪽 코드를 받는 `HTMLElement` 인스턴스 일반 DOM Api를 사용 하 여 사용할 수 있습니다.

예를 들어, 다음 코드 요소에 포커스를 설정 하는 수 있게 해 주는.NET 확장 메서드를 정의 합니다.

*mylib.js*:

```javascript
window.myLib = {
  focusElement : function (element) {
    element.focus();
  }
}
```

*ElementRefExtensions.cs*:

```csharp
using Microsoft.AspNetCore.Blazor;
using Microsoft.JSInterop;
using System.Threading.Tasks;

namespace MyLib
{
    public static class MyLibElementRefExtensions
    {
        public static Task Focus(this ElementRef elementRef)
        {
            return JSRuntime.Current.InvokeAsync<object>("myLib.focusElement", elementRef);
        }
    }
}
```

이제 구성 요소에서 입력을 집중할 수 있습니다.

```cshtml
@using MyLib

<input ref="username" />
<button onclick="@SetFocus">Set focus</button>

@functions {
    ElementRef username;

    void SetFocus()
    {
        username.Focus();
    }
}
```

> [!IMPORTANT]
> 합니다 `username` 변수는 구성 요소를 렌더링 하 고 해당 출력을 포함 한 후에 채워집니다는 `<input>` 요소입니다. 채워지지를 전달 하려고 하면 `ElementRef` JavaScript 코드에 JavaScript 코드를 받는 `null`합니다. 구성 요소 사용 (초기 포커스 요소에 설정)로 렌더링을 마친 후 요소 참조를 조작 하는 `OnAfterRenderAsync` 나 `OnAfterRender` [구성 요소 수명 주기 메서드](xref:razor-components/components#lifecycle-methods)합니다.

## <a name="invoke-net-methods-from-javascript-functions"></a>JavaScript 함수에서.NET 메서드를 호출 합니다.

### <a name="static-net-method-call"></a>정적.NET 메서드 호출

JavaScript에서 정적.NET 메서드를 호출 하려면 사용 합니다 `DotNet.invokeMethod` 또는 `DotNet.invokeMethodAsync` 함수입니다. 정적 메서드를 호출 하 고 함수 및 인수를 포함 하는 어셈블리의 이름을 하려는의 식별자를 전달 합니다. 마찬가지로 비동기 버전은 서버 쪽 시나리오를 지원 하도록 기본 설정입니다. JavaScript에서 호출 되도록.NET 메서드는 이어야 합니다 public, 정적 및 사용 하 여 데코 레이트 된 `[JSInvokable]`합니다. 기본적으로 메서드 식별자 메서드 이름 이지만 사용 하 여 다른 식별자를 지정할 수 있습니다는 `JSInvokableAttribute` 생성자입니다. 개방형 제네릭 메서드를 호출 합니다. 현재 지원 되지 않습니다.

샘플 앱에 포함 되어는 C# 배열을 반환 하는 방법 `int`s입니다. 로 데코레이팅된 메서드는 `JSInvokable` 특성입니다.

*Pages/JsInterop.cshtml*:

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?start=47&end=58&highlight=7-11)]

클라이언트에 제공 하는 JavaScript를 호출 하는 C# .NET 메서드.

*wwwroot/exampleJsInterop.js*:

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=8-12)]

경우는 **트리거.NET 정적 메서드에 ReturnArrayAsync** 단추를 선택한 경우 브라우저의 웹 개발자 도구에서 콘솔 출력을 검토 합니다.

```console
Array(4) [ 1, 2, 3, 4 ]
```

네 번째 배열 값을 배열에 푸시됩니다. (`data.push(4);`)에서 반환 된 `ReturnArrayAsync`합니다.

### <a name="instance-method-call"></a>인스턴스 메서드 호출

또한 JavaScript에서.NET 인스턴스 메서드를 호출할 수 있습니다. JavaScript에서.NET 인스턴스 메서드를 호출 하려면 먼저 전달할.NET 인스턴스 JavaScript에 래핑하여는 `DotNetObjectRef` 인스턴스. .NET 인스턴스 JavaScript로 참조로 전달 되 고 사용 하 여 인스턴스에 대 한.NET 인스턴스 메서드를 호출할 수 있습니다 합니다 `invokeMethod` 또는 `invokeMethodAsync` 함수입니다. JavaScript에서 다른.NET 메서드를 호출 하는 경우.NET 인스턴스를 인수로 전달할 수도 있습니다.

> [!NOTE]
> 샘플 앱은 클라이언트 콘솔에 메시지를 기록합니다. 샘플 앱에서 보여 주는 다음 예제에 대 한 브라우저의 개발자 도구에서 브라우저의 콘솔 출력을 검사 합니다.

경우는 **HelloHelper.SayHello 트리거.NET 인스턴스 메서드** 단추를 선택 하면 `ExampleJsInterop.CallHelloHelperSayHello` 라고 하 고 이름을 전달 `Blazor`, 메서드.

*Pages/JsInterop.cshtml*:

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?start=60&end=69&highlight=8)]

`CallHelloHelperSayHello` JavaScript 함수를 호출 `sayHello` 의 새 인스턴스를 사용 하 여 `HelloHelper`입니다.

*JsInteropClasses/ExampleJsInterop.cs*:

[!code-csharp[](./common/samples/3.x/BlazorSample/JsInteropClasses/ExampleJsInterop.cs?name=snippet1&highlight=19-25)]

*wwwroot/exampleJsInterop.js*:

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=15-17)]

이름에 전달 됩니다 `HelloHelper`의 설정 하는 생성자를 `HelloHelper.Name` 속성입니다. 때 JavaScript 함수 `sayHello` 실행 됩니다 `HelloHelper.SayHello` 반환을 `Hello, {Name}!` JavaScript 함수에 의해 콘솔에 기록 되는 메시지입니다.

*JsInteropClasses/HelloHelper.cs*:

[!code-csharp[](./common/samples/3.x/BlazorSample/JsInteropClasses/HelloHelper.cs?name=snippet1&highlight=5,10-11)]

브라우저의 웹 개발자 도구에서 출력을 콘솔:

```console
Hello, Blazor!
```

## <a name="share-interop-code-in-a-razor-component-class-library"></a>구성 요소 Razor 클래스 라이브러리에서 interop 코드 공유

구성 요소 Razor 클래스 라이브러리에 JavaScript interop 코드를 포함할 수 있습니다 (`dotnet new blazorlib`), NuGet 패키지의 코드를 공유할 수 있습니다.

구성 요소 Razor 클래스 라이브러리는 빌드된 어셈블리에 포함 JavaScript 리소스를 처리합니다. JavaScript 파일에 배치 되는 *wwwroot* 폴더 및 도구 담당 라이브러리를 빌드할 때 리소스를 포함 합니다.

기본 제공된 NuGet 패키지를 기본 NuGet 패키지 참조 하는 것 처럼 앱의 프로젝트 파일에서 참조 됩니다. 앱을 복원한 후 앱 코드 것 처럼 JavaScript에 호출할 수 있습니다 C#입니다.
