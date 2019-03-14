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
# <a name="razor-components-javascript-interop"></a><span data-ttu-id="eaa3b-103">Razor 구성 요소가 JavaScript interop</span><span class="sxs-lookup"><span data-stu-id="eaa3b-103">Razor Components JavaScript interop</span></span>

<span data-ttu-id="eaa3b-104">하 여 [Javier Calvarro 박](https://github.com/javiercn)하십시오 [Daniel Roth](https://github.com/danroth27), 및 [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="eaa3b-104">By [Javier Calvarro Nelson](https://github.com/javiercn), [Daniel Roth](https://github.com/danroth27), and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="eaa3b-105">구성 요소 Razor 앱을.NET 및.NET에서 JavaScript 함수를 호출할 수 JavaScript 코드에서 메서드.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-105">A Razor Components app can invoke JavaScript functions from .NET and .NET methods from JavaScript code.</span></span>

## <a name="invoke-javascript-functions-from-net-methods"></a><span data-ttu-id="eaa3b-106">.NET 메서드에서 JavaScript 함수를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-106">Invoke JavaScript functions from .NET methods</span></span>

<span data-ttu-id="eaa3b-107">.NET 코드를 JavaScript 함수를 호출 해야 하는 경우 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-107">There are times when .NET code is required to call a JavaScript function.</span></span> <span data-ttu-id="eaa3b-108">예를 들어 JavaScript 호출을 브라우저 기능 또는 앱에 JavaScript 라이브러리에서 기능을 노출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-108">For example, a JavaScript call can expose browser capabilities or functionality from a JavaScript library to the app.</span></span>

<span data-ttu-id="eaa3b-109">.NET에서 JavaScript로 호출을 사용 하 여는 `IJSRuntime` 추상화 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-109">To call into JavaScript from .NET, use the `IJSRuntime` abstraction.</span></span> <span data-ttu-id="eaa3b-110">합니다 `InvokeAsync<T>` 메서드를 `IJSRuntime` 와 임의 개수의 JSON 직렬화 가능 인수를 호출 하려면 JavaScript 함수에 대 한 식별자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-110">The `InvokeAsync<T>` method on `IJSRuntime` takes an identifier for the JavaScript function you wish to invoke along with any number of JSON-serializable arguments.</span></span> <span data-ttu-id="eaa3b-111">전역 범위와 관련 된 함수 식별자가 (`window`).</span><span class="sxs-lookup"><span data-stu-id="eaa3b-111">The function identifier is relative to the global scope (`window`).</span></span> <span data-ttu-id="eaa3b-112">호출 하려는 경우 `window.someScope.someFunction`, 식별자가 `someScope.someFunction`합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-112">If you wish to call `window.someScope.someFunction`, the identifier is `someScope.someFunction`.</span></span> <span data-ttu-id="eaa3b-113">가 호출 되기 전에 함수를 등록 하려면 않아도가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-113">There's no need to register the function before it's called.</span></span> <span data-ttu-id="eaa3b-114">반환 형식은 `T` 도 JSON 직렬화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-114">The return type `T` must also be JSON serializable.</span></span>

<span data-ttu-id="eaa3b-115">서버 쪽 ASP.NET Core Razor 구성 요소 앱:</span><span class="sxs-lookup"><span data-stu-id="eaa3b-115">For server-side ASP.NET Core Razor Components apps:</span></span>

* <span data-ttu-id="eaa3b-116">서버 쪽 앱에서 여러 사용자 요청을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-116">Multiple user requests are processed by the server-side app.</span></span> <span data-ttu-id="eaa3b-117">호출 하지 마십시오 `JSRuntime.Current` JavaScript 함수를 호출 하는 구성 요소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-117">Don't call `JSRuntime.Current` in a component to invoke JavaScript functions.</span></span>
* <span data-ttu-id="eaa3b-118">삽입 된 `IJSRuntime` 추상화 및 JavaScript interop 호출에 삽입 된 개체를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-118">Inject the `IJSRuntime` abstraction and use the injected object to issue JavaScript interop calls.</span></span>

<span data-ttu-id="eaa3b-119">다음 예제는 기반 [TextDecoder](https://developer.mozilla.org/docs/Web/API/TextDecoder), 실험적 JavaScript 기반 디코더는 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-119">The following example is based on [TextDecoder](https://developer.mozilla.org/docs/Web/API/TextDecoder), an experimental JavaScript-based decoder.</span></span> <span data-ttu-id="eaa3b-120">JavaScript 함수를 호출 하는 방법을 보여 줍니다는 C# 메서드.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-120">The example demonstrates how to invoke a JavaScript function from a C# method.</span></span> <span data-ttu-id="eaa3b-121">JavaScript 함수에서 바이트 배열을 취하는 C# 메서드를 배열의 디코딩하고 표시에 대 한 구성 요소에 텍스트를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-121">The JavaScript function accepts a byte array from a C# method, decodes the array, and returns the text to the component for display.</span></span>

<span data-ttu-id="eaa3b-122">내 합니다 `<head>` 요소의 *wwwroot/index.html*를 사용 하는 함수를 제공 `TextDecoder` 전달 된 배열을 디코드 하려면:</span><span class="sxs-lookup"><span data-stu-id="eaa3b-122">Inside the `<head>` element of *wwwroot/index.html*, provide a function that uses `TextDecoder` to decode a passed array:</span></span>

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

<span data-ttu-id="eaa3b-123">앞의 예제에 표시 된 코드와 같은 JavaScript 코드를 스크립트 파일에 대 한 참조를 사용 하 여 JavaScript 파일에서 로드할 수도 있습니다는 *wwwroot/index.html* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-123">JavaScript code, such as the code shown in the preceding example, can also be loaded by a JavaScript file with a reference to the script file in the *wwwroot/index.html* file.</span></span>

<span data-ttu-id="eaa3b-124">다음 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="eaa3b-124">The following component:</span></span>

* <span data-ttu-id="eaa3b-125">호출 하는 `ConvertArray` JavaScript 함수를 사용 하 여 `JsRuntime` 구성 단추 (**변환 배열**) 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-125">Invokes the `ConvertArray` JavaScript function using `JsRuntime` when a component button (**Convert Array**) is selected.</span></span>
* <span data-ttu-id="eaa3b-126">JavaScript 함수를 호출한 다음 전달된 된 배열은 문자열로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-126">After the JavaScript function is called, the passed array is converted into a string.</span></span> <span data-ttu-id="eaa3b-127">표시에 대 한 구성 요소에는 문자열이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-127">The string is returned to the component for display.</span></span>

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

<span data-ttu-id="eaa3b-128">클라이언트 쪽 Blazor 앱에 대 한는 `IJSRuntime` 추상화에서 액세스할 수 `JSRuntime.Current`,이 현재 사용자의 요청을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-128">For client-side Blazor apps, the `IJSRuntime` abstraction is accessible from `JSRuntime.Current`, which refers to the current user's request.</span></span> <span data-ttu-id="eaa3b-129">클라이언트 쪽 Blazor 앱의 사용자만 이기 때문에 사용 하 여 `JSRuntime.Current` 호출할 JavaScript 함수 정상적으로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-129">Because there's only a single user of a client-side Blazor app, using `JSRuntime.Current` to invoke a JavaScript function works normally.</span></span> <span data-ttu-id="eaa3b-130">만 사용 하 여 `JSRuntime.Current` 클라이언트 쪽 Blazor 앱에서.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-130">Only use `JSRuntime.Current` in client-side Blazor apps.</span></span>

<span data-ttu-id="eaa3b-131">이 항목과 관련 된 클라이언트 쪽 샘플 앱에서 두 JavaScript 함수는 사용자 입력을 받는 환영 메시지를 표시 하는 DOM과 상호 작용 하는 클라이언트 쪽 앱에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-131">In the client-side sample app that accompanies this topic, two JavaScript functions are available to the client-side app that interact with the DOM to receive user input and display a welcome message:</span></span>

* <span data-ttu-id="eaa3b-132">`showPrompt` &ndash; 사용자 입력 (사용자 이름)를 수락할 프롬프트를 생성 하 고 호출자에 게 이름을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-132">`showPrompt` &ndash; Produces a prompt to accept user input (the user's name) and returns the name to the caller.</span></span>
* <span data-ttu-id="eaa3b-133">`displayWelcome` &ndash; 환영 메시지를 호출자에서 사용 하 여 DOM 개체를 할당 한 `id` 의 `welcome`합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-133">`displayWelcome` &ndash; Assigns a welcome message from the caller to a DOM object with an `id` of `welcome`.</span></span>

<span data-ttu-id="eaa3b-134">*wwwroot/exampleJsInterop.js*:</span><span class="sxs-lookup"><span data-stu-id="eaa3b-134">*wwwroot/exampleJsInterop.js*:</span></span>

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=2-7)]

<span data-ttu-id="eaa3b-135">위치는 `<script>` JavaScript 파일에서 참조 하는 태그를 *wwwroot/index.html* 파일:</span><span class="sxs-lookup"><span data-stu-id="eaa3b-135">Place the `<script>` tag that references the JavaScript file in the *wwwroot/index.html* file:</span></span>

[!code-html[](./common/samples/3.x/BlazorSample/wwwroot/index.html?highlight=16)]

<span data-ttu-id="eaa3b-136">스크립트 태그를 동적으로 업데이트할 수 없으므로 구성 요소 파일에 스크립트 태그를 놓지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-136">Don't place a script tag in a component file because the script tag can't be updated dynamically.</span></span>

<span data-ttu-id="eaa3b-137">호출 하 여 JavaScript 함수를 사용 하 여.NET 메서드 interop `InvokeAsync<T>` 메서드를 `IJSRuntime`입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-137">.NET methods interop with the JavaScript functions by calling `InvokeAsync<T>` method on `IJSRuntime`.</span></span>

<span data-ttu-id="eaa3b-138">샘플 앱에서는 한 쌍의 C# 메서드를 `Prompt` 하 고 `Display`를 호출 하는 `showPrompt` 및 `displayWelcome` JavaScript 함수:</span><span class="sxs-lookup"><span data-stu-id="eaa3b-138">The sample app uses a pair of C# methods, `Prompt` and `Display`, to invoke the `showPrompt` and `displayWelcome` JavaScript functions:</span></span>

<span data-ttu-id="eaa3b-139">*JsInteropClasses/ExampleJsInterop.cs*:</span><span class="sxs-lookup"><span data-stu-id="eaa3b-139">*JsInteropClasses/ExampleJsInterop.cs*:</span></span>

[!code-csharp[](./common/samples/3.x/BlazorSample/JsInteropClasses/ExampleJsInterop.cs?name=snippet1&highlight=6-8,14-16)]

<span data-ttu-id="eaa3b-140">`IJSRuntime` 추상화는 비동기 서버 쪽 시나리오에 대 한 허용 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-140">The `IJSRuntime` abstraction is asynchronous to allow for server-side scenarios.</span></span> <span data-ttu-id="eaa3b-141">클라이언트 쪽 앱이 실행 되는 JavaScript 함수를 동기적으로 호출 하려는 경우에 다운 `IJSInProcessRuntime` 호출 `Invoke<T>` 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-141">If the app runs client-side and you want to invoke a JavaScript function synchronously, downcast to `IJSInProcessRuntime` and call `Invoke<T>` instead.</span></span> <span data-ttu-id="eaa3b-142">대부분의 JavaScript 라이브러리를 interop 사용 하 여 비동기 Api 라이브러리를 확인 하는 모든 시나리오에서 클라이언트 쪽 또는 서버 쪽에서 사용할 수 있는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-142">We recommend that most JavaScript interop libraries use the async APIs to ensure the libraries are available in all scenarios, client-side or server-side.</span></span>

<span data-ttu-id="eaa3b-143">JS interop을 보여 주기 위해 구성 요소를 포함 하는 샘플 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-143">The sample app includes a component to demonstrate JS interop.</span></span> <span data-ttu-id="eaa3b-144">구성 요소:</span><span class="sxs-lookup"><span data-stu-id="eaa3b-144">The component:</span></span>

* <span data-ttu-id="eaa3b-145">JS 프롬프트를 통해 사용자 입력을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-145">Receives user input via a JS prompt.</span></span>
* <span data-ttu-id="eaa3b-146">처리에 대 한 구성 요소에 텍스트를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-146">Returns the text to the component for processing.</span></span>
* <span data-ttu-id="eaa3b-147">시작 메시지를 표시 하려면 DOM과 상호 작용 하는 두 번째 JS 함수를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-147">Calls a second JS function that interacts with the DOM to display a welcome message.</span></span>

<span data-ttu-id="eaa3b-148">*Pages/JSInterop.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="eaa3b-148">*Pages/JSInterop.cshtml*:</span></span>

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?start=1&end=21&highlight=2-3,9-11,13,16-20)]

1. <span data-ttu-id="eaa3b-149">때 `TriggerJsPrompt` 구성 요소를 선택 하 여 실행 됩니다 **트리거 JavaScript 프롬프트** 단추를 `ExampleJsInterop.Prompt` 에서 메서드 C# 코드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-149">When `TriggerJsPrompt` is executed by selecting the component's **Trigger JavaScript Prompt** button, the `ExampleJsInterop.Prompt` method in C# code is called.</span></span>
1. <span data-ttu-id="eaa3b-150">`Prompt` 메서드가 실행 된 JavaScript `showPrompt` 함수는 *wwwroot/exampleJsInterop.js* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-150">The `Prompt` method executes the JavaScript `showPrompt` function provided in the *wwwroot/exampleJsInterop.js* file.</span></span>
1. <span data-ttu-id="eaa3b-151">합니다 `showPrompt` HTML 인코딩 및 반환 되는 사용자 입력 (사용자 이름)을 허용 하는 함수는 `Prompt` 메서드 궁극적으로 구성 요소 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-151">The `showPrompt` function accepts user input (the user's name), which is HTML-encoded and returned to the `Prompt` method and ultimately back to the component.</span></span> <span data-ttu-id="eaa3b-152">구성 요소를 로컬 변수에 사용자 이름을 저장 `name`합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-152">The component stores the user's name in a local variable, `name`.</span></span>
1. <span data-ttu-id="eaa3b-153">문자열에 저장 `name` 초에 전달 되는 환영 메시지는 통합 C# 메서드를 `ExampleJsInterop.Display`합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-153">The string stored in `name` is incorporated into a welcome message, which is passed to a second C# method, `ExampleJsInterop.Display`.</span></span>
1. <span data-ttu-id="eaa3b-154">`Display` JavaScript 함수를 호출 `displayWelcome`를 환영 메시지 머리글 태그로 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-154">`Display` calls a JavaScript function, `displayWelcome`, which renders the welcome message into a heading tag.</span></span>

## <a name="capture-references-to-elements"></a><span data-ttu-id="eaa3b-155">요소에 대 한 참조를 캡처</span><span class="sxs-lookup"><span data-stu-id="eaa3b-155">Capture references to elements</span></span>

<span data-ttu-id="eaa3b-156">일부 [JavaScript interop](xref:razor-components/javascript-interop) 시나리오에는 HTML 요소에 대 한 참조가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-156">Some [JavaScript interop](xref:razor-components/javascript-interop) scenarios require references to HTML elements.</span></span> <span data-ttu-id="eaa3b-157">예를 들어, UI 라이브러리 요소 참조를 초기화 해야 할 수 있습니다 또는 같은 요소에 대해 비슷한 Api를 호출 해야 할 수 있습니다 `focus` 또는 `play`합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-157">For example, a UI library may require an element reference for initialization, or you might need to call command-like APIs on an element, such as `focus` or `play`.</span></span>

<span data-ttu-id="eaa3b-158">구성 요소에서 HTML 요소에 대 한 참조를 추가 하 여 캡처할 수 있습니다는 `ref` HTML 요소에 특성 및 다음 형식의 필드를 정의할 `ElementRef` 이름이 값과 일치는 `ref` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-158">You can capture references to HTML elements in a component by adding a `ref` attribute to the HTML element and then defining a field of type `ElementRef` whose name matches the value of the `ref` attribute.</span></span>

<span data-ttu-id="eaa3b-159">다음 예제에서는 사용자 입력된 요소에 대 한 참조를 캡처를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-159">The following example shows capturing a reference to the username input element:</span></span>

```csharp
<input ref="username" ... />

@functions {
    ElementRef username;
}
```

> [!NOTE]
> <span data-ttu-id="eaa3b-160">수행할 **되지** DOM을 채우는 방법으로 캡처된 요소 참조를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-160">Do **not** use captured element references as a way of populating the DOM.</span></span> <span data-ttu-id="eaa3b-161">이렇게 선언적 렌더링 모델을 방해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-161">Doing so may interfere with the declarative rendering model.</span></span>

<span data-ttu-id="eaa3b-162">.NET 코드와 관련 된 관련해 서는 `ElementRef` 불투명 핸들입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-162">As far as .NET code is concerned, an `ElementRef` is an opaque handle.</span></span> <span data-ttu-id="eaa3b-163">합니다 *만* 것으로 할 수 있는 점은 JavaScript interop을 통해 JavaScript 코드를 통해 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-163">The *only* thing you can do with it is pass it through to JavaScript code via JavaScript interop.</span></span> <span data-ttu-id="eaa3b-164">이렇게 하면 JavaScript 쪽 코드를 받는 `HTMLElement` 인스턴스 일반 DOM Api를 사용 하 여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-164">When you do so, the JavaScript-side code receives an `HTMLElement` instance, which it can use with normal DOM APIs.</span></span>

<span data-ttu-id="eaa3b-165">예를 들어, 다음 코드 요소에 포커스를 설정 하는 수 있게 해 주는.NET 확장 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-165">For example, the following code defines a .NET extension method that enables setting the focus on an element:</span></span>

<span data-ttu-id="eaa3b-166">*mylib.js*:</span><span class="sxs-lookup"><span data-stu-id="eaa3b-166">*mylib.js*:</span></span>

```javascript
window.myLib = {
  focusElement : function (element) {
    element.focus();
  }
}
```

<span data-ttu-id="eaa3b-167">*ElementRefExtensions.cs*:</span><span class="sxs-lookup"><span data-stu-id="eaa3b-167">*ElementRefExtensions.cs*:</span></span>

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

<span data-ttu-id="eaa3b-168">이제 구성 요소에서 입력을 집중할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-168">Now you can focus inputs in any of your components:</span></span>

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
> <span data-ttu-id="eaa3b-169">합니다 `username` 변수는 구성 요소를 렌더링 하 고 해당 출력을 포함 한 후에 채워집니다는 `<input>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-169">The `username` variable is only populated after the component renders and its output includes the `<input>` element.</span></span> <span data-ttu-id="eaa3b-170">채워지지를 전달 하려고 하면 `ElementRef` JavaScript 코드에 JavaScript 코드를 받는 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-170">If you try to pass an unpopulated `ElementRef` to JavaScript code, the JavaScript code receives `null`.</span></span> <span data-ttu-id="eaa3b-171">구성 요소 사용 (초기 포커스 요소에 설정)로 렌더링을 마친 후 요소 참조를 조작 하는 `OnAfterRenderAsync` 나 `OnAfterRender` [구성 요소 수명 주기 메서드](xref:razor-components/components#lifecycle-methods)합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-171">To manipulate element references after the component has finished rendering (to set the initial focus on an element) use the `OnAfterRenderAsync` or `OnAfterRender` [component lifecycle methods](xref:razor-components/components#lifecycle-methods).</span></span>

## <a name="invoke-net-methods-from-javascript-functions"></a><span data-ttu-id="eaa3b-172">JavaScript 함수에서.NET 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-172">Invoke .NET methods from JavaScript functions</span></span>

### <a name="static-net-method-call"></a><span data-ttu-id="eaa3b-173">정적.NET 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="eaa3b-173">Static .NET method call</span></span>

<span data-ttu-id="eaa3b-174">JavaScript에서 정적.NET 메서드를 호출 하려면 사용 합니다 `DotNet.invokeMethod` 또는 `DotNet.invokeMethodAsync` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-174">To invoke a static .NET method from JavaScript, use the `DotNet.invokeMethod` or `DotNet.invokeMethodAsync` functions.</span></span> <span data-ttu-id="eaa3b-175">정적 메서드를 호출 하 고 함수 및 인수를 포함 하는 어셈블리의 이름을 하려는의 식별자를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-175">Pass in the identifier of the static method you wish to call, the name of the assembly containing the function, and any arguments.</span></span> <span data-ttu-id="eaa3b-176">마찬가지로 비동기 버전은 서버 쪽 시나리오를 지원 하도록 기본 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-176">Again, the async version is preferred to support server-side scenarios.</span></span> <span data-ttu-id="eaa3b-177">JavaScript에서 호출 되도록.NET 메서드는 이어야 합니다 public, 정적 및 사용 하 여 데코 레이트 된 `[JSInvokable]`합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-177">To be invokable from JavaScript, the .NET method must be public, static, and decorated with `[JSInvokable]`.</span></span> <span data-ttu-id="eaa3b-178">기본적으로 메서드 식별자 메서드 이름 이지만 사용 하 여 다른 식별자를 지정할 수 있습니다는 `JSInvokableAttribute` 생성자입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-178">By default, the method identifier is the method name, but you can specify a different identifier using the `JSInvokableAttribute` constructor.</span></span> <span data-ttu-id="eaa3b-179">개방형 제네릭 메서드를 호출 합니다. 현재 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-179">Calling open generic methods isn't currently supported.</span></span>

<span data-ttu-id="eaa3b-180">샘플 앱에 포함 되어는 C# 배열을 반환 하는 방법 `int`s입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-180">The sample app includes a C# method to return an array of `int`s.</span></span> <span data-ttu-id="eaa3b-181">로 데코레이팅된 메서드는 `JSInvokable` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-181">The method is decorated with the `JSInvokable` attribute.</span></span>

<span data-ttu-id="eaa3b-182">*Pages/JsInterop.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="eaa3b-182">*Pages/JsInterop.cshtml*:</span></span>

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?start=47&end=58&highlight=7-11)]

<span data-ttu-id="eaa3b-183">클라이언트에 제공 하는 JavaScript를 호출 하는 C# .NET 메서드.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-183">JavaScript served to the client invokes the C# .NET method.</span></span>

<span data-ttu-id="eaa3b-184">*wwwroot/exampleJsInterop.js*:</span><span class="sxs-lookup"><span data-stu-id="eaa3b-184">*wwwroot/exampleJsInterop.js*:</span></span>

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=8-12)]

<span data-ttu-id="eaa3b-185">경우는 **트리거.NET 정적 메서드에 ReturnArrayAsync** 단추를 선택한 경우 브라우저의 웹 개발자 도구에서 콘솔 출력을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-185">When the **Trigger .NET static method ReturnArrayAsync** button is selected, examine the console output in the browser's web developer tools:</span></span>

```console
Array(4) [ 1, 2, 3, 4 ]
```

<span data-ttu-id="eaa3b-186">네 번째 배열 값을 배열에 푸시됩니다. (`data.push(4);`)에서 반환 된 `ReturnArrayAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-186">The fourth array value is pushed to the array (`data.push(4);`) returned by `ReturnArrayAsync`.</span></span>

### <a name="instance-method-call"></a><span data-ttu-id="eaa3b-187">인스턴스 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="eaa3b-187">Instance method call</span></span>

<span data-ttu-id="eaa3b-188">또한 JavaScript에서.NET 인스턴스 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-188">You can also call .NET instance methods from JavaScript.</span></span> <span data-ttu-id="eaa3b-189">JavaScript에서.NET 인스턴스 메서드를 호출 하려면 먼저 전달할.NET 인스턴스 JavaScript에 래핑하여는 `DotNetObjectRef` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-189">To invoke a .NET instance method from JavaScript, first pass the .NET instance to JavaScript by wrapping it in a `DotNetObjectRef` instance.</span></span> <span data-ttu-id="eaa3b-190">.NET 인스턴스 JavaScript로 참조로 전달 되 고 사용 하 여 인스턴스에 대 한.NET 인스턴스 메서드를 호출할 수 있습니다 합니다 `invokeMethod` 또는 `invokeMethodAsync` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-190">The .NET instance is passed by reference to JavaScript, and you can invoke .NET instance methods on the instance using the `invokeMethod` or `invokeMethodAsync` functions.</span></span> <span data-ttu-id="eaa3b-191">JavaScript에서 다른.NET 메서드를 호출 하는 경우.NET 인스턴스를 인수로 전달할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-191">The .NET instance can also be passed as an argument when invoking other .NET methods from JavaScript.</span></span>

> [!NOTE]
> <span data-ttu-id="eaa3b-192">샘플 앱은 클라이언트 콘솔에 메시지를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-192">The sample app logs messages to the client-side console.</span></span> <span data-ttu-id="eaa3b-193">샘플 앱에서 보여 주는 다음 예제에 대 한 브라우저의 개발자 도구에서 브라우저의 콘솔 출력을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-193">For the following examples demonstrated by the sample app, examine the browser's console output in the browser's developer tools.</span></span>

<span data-ttu-id="eaa3b-194">경우는 **HelloHelper.SayHello 트리거.NET 인스턴스 메서드** 단추를 선택 하면 `ExampleJsInterop.CallHelloHelperSayHello` 라고 하 고 이름을 전달 `Blazor`, 메서드.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-194">When the **Trigger .NET instance method HelloHelper.SayHello** button is selected, `ExampleJsInterop.CallHelloHelperSayHello` is called and passes a name, `Blazor`, to the method.</span></span>

<span data-ttu-id="eaa3b-195">*Pages/JsInterop.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="eaa3b-195">*Pages/JsInterop.cshtml*:</span></span>

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?start=60&end=69&highlight=8)]

<span data-ttu-id="eaa3b-196">`CallHelloHelperSayHello` JavaScript 함수를 호출 `sayHello` 의 새 인스턴스를 사용 하 여 `HelloHelper`입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-196">`CallHelloHelperSayHello` invokes the JavaScript function `sayHello` with a new instance of `HelloHelper`.</span></span>

<span data-ttu-id="eaa3b-197">*JsInteropClasses/ExampleJsInterop.cs*:</span><span class="sxs-lookup"><span data-stu-id="eaa3b-197">*JsInteropClasses/ExampleJsInterop.cs*:</span></span>

[!code-csharp[](./common/samples/3.x/BlazorSample/JsInteropClasses/ExampleJsInterop.cs?name=snippet1&highlight=19-25)]

<span data-ttu-id="eaa3b-198">*wwwroot/exampleJsInterop.js*:</span><span class="sxs-lookup"><span data-stu-id="eaa3b-198">*wwwroot/exampleJsInterop.js*:</span></span>

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=15-17)]

<span data-ttu-id="eaa3b-199">이름에 전달 됩니다 `HelloHelper`의 설정 하는 생성자를 `HelloHelper.Name` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-199">The name is passed to `HelloHelper`'s constructor, which sets the `HelloHelper.Name` property.</span></span> <span data-ttu-id="eaa3b-200">때 JavaScript 함수 `sayHello` 실행 됩니다 `HelloHelper.SayHello` 반환을 `Hello, {Name}!` JavaScript 함수에 의해 콘솔에 기록 되는 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-200">When the JavaScript function `sayHello` is executed, `HelloHelper.SayHello` returns the `Hello, {Name}!` message, which is written to the console by the JavaScript function.</span></span>

<span data-ttu-id="eaa3b-201">*JsInteropClasses/HelloHelper.cs*:</span><span class="sxs-lookup"><span data-stu-id="eaa3b-201">*JsInteropClasses/HelloHelper.cs*:</span></span>

[!code-csharp[](./common/samples/3.x/BlazorSample/JsInteropClasses/HelloHelper.cs?name=snippet1&highlight=5,10-11)]

<span data-ttu-id="eaa3b-202">브라우저의 웹 개발자 도구에서 출력을 콘솔:</span><span class="sxs-lookup"><span data-stu-id="eaa3b-202">Console output in the browser's web developer tools:</span></span>

```console
Hello, Blazor!
```

## <a name="share-interop-code-in-a-razor-component-class-library"></a><span data-ttu-id="eaa3b-203">구성 요소 Razor 클래스 라이브러리에서 interop 코드 공유</span><span class="sxs-lookup"><span data-stu-id="eaa3b-203">Share interop code in a Razor Component class library</span></span>

<span data-ttu-id="eaa3b-204">구성 요소 Razor 클래스 라이브러리에 JavaScript interop 코드를 포함할 수 있습니다 (`dotnet new blazorlib`), NuGet 패키지의 코드를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-204">JavaScript interop code can be included in a Razor Component class library (`dotnet new blazorlib`), which allows you to share the code in a NuGet package.</span></span>

<span data-ttu-id="eaa3b-205">구성 요소 Razor 클래스 라이브러리는 빌드된 어셈블리에 포함 JavaScript 리소스를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-205">The Razor Component class library handles embedding JavaScript resources in the built assembly.</span></span> <span data-ttu-id="eaa3b-206">JavaScript 파일에 배치 되는 *wwwroot* 폴더 및 도구 담당 라이브러리를 빌드할 때 리소스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-206">The JavaScript files are placed in the *wwwroot* folder, and the tooling takes care of embedding the resources when the library is built.</span></span>

<span data-ttu-id="eaa3b-207">기본 제공된 NuGet 패키지를 기본 NuGet 패키지 참조 하는 것 처럼 앱의 프로젝트 파일에서 참조 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-207">The built NuGet package is referenced in the project file of the app just as any normal NuGet package is referenced.</span></span> <span data-ttu-id="eaa3b-208">앱을 복원한 후 앱 코드 것 처럼 JavaScript에 호출할 수 있습니다 C#입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa3b-208">After the app has been restored, app code can call into JavaScript as if it were C#.</span></span>
