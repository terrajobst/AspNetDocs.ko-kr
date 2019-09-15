---
uid: web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
title: ASP.NET Web API의 매개 변수 바인딩-ASP.NET 4.x
author: MikeWasson
description: Web API가 매개 변수를 바인딩하는 방법 및 ASP.NET 4.x에서 바인딩 프로세스를 사용자 지정 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 07/11/2013
ms.custom: seoapril2019
ms.assetid: e42c8388-04ed-4341-9fdb-41b1b4c06320
msc.legacyurl: /web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 5386532ab581e023d93d16a5d4107e07f40b986f
ms.sourcegitcommit: 4b324a11131e38f920126066b94ff478aa9927f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70985811"
---
# <a name="parameter-binding-in-aspnet-web-api"></a><span data-ttu-id="0b338-103">ASP.NET Web API의 매개 변수 바인딩</span><span class="sxs-lookup"><span data-stu-id="0b338-103">Parameter Binding in ASP.NET Web API</span></span>

<span data-ttu-id="0b338-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="0b338-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[!INCLUDE[](~/includes/coreWebAPI.md)]

<span data-ttu-id="0b338-105">이 문서에서는 Web API가 매개 변수를 바인딩하는 방법과 바인딩 프로세스를 사용자 지정 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-105">This article describes how Web API binds parameters, and how you can customize the binding process.</span></span> <span data-ttu-id="0b338-106">웹 API는 컨트롤러에서 메서드를 호출할 때 *바인딩*이라는 프로세스 인 매개 변수에 대 한 값을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-106">When Web API calls a method on a controller, it must set values for the parameters, a process called *binding*.</span></span>

<span data-ttu-id="0b338-107">기본적으로 웹 API는 다음 규칙을 사용 하 여 매개 변수를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-107">By default, Web API uses the following rules to bind parameters:</span></span>

- <span data-ttu-id="0b338-108">매개 변수가 "simple" 형식이 면 Web API는 URI에서 값을 가져오려고 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-108">If the parameter is a "simple" type, Web API tries to get the value from the URI.</span></span> <span data-ttu-id="0b338-109">단순 형식에는 .NET [기본 형식](https://msdn.microsoft.com/library/system.type.isprimitive.aspx) (**int**, **bool**, **Double**등)이 *포함 되 고* **TimeSpan**, **DateTime**, **Guid**, **decimal**및 **문자열과**형식의 모든 형식이 포함 됩니다. 문자열에서 변환할 수 있는 변환기입니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-109">Simple types include the .NET [primitive types](https://msdn.microsoft.com/library/system.type.isprimitive.aspx) (**int**, **bool**, **double**, and so forth), plus **TimeSpan**, **DateTime**, **Guid**, **decimal**, and **string**, *plus* any type with a type converter that can convert from a string.</span></span> <span data-ttu-id="0b338-110">형식 변환기에 대 한 자세한 내용은 뒷부분에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-110">(More about type converters later.)</span></span>
- <span data-ttu-id="0b338-111">복합 형식의 경우 Web API는 [미디어 형식 포맷터](media-formatters.md)를 사용 하 여 메시지 본문에서 값을 읽으려고 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-111">For complex types, Web API tries to read the value from the message body, using a [media-type formatter](media-formatters.md).</span></span>

<span data-ttu-id="0b338-112">예를 들어 다음은 일반적인 Web API controller 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-112">For example, here is a typical Web API controller method:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="0b338-113">*Id* 매개 변수 &quot;는 단순&quot; 형식 이므로 Web API는 요청 URI에서 값을 가져오려고 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-113">The *id* parameter is a &quot;simple&quot; type, so Web API tries to get the value from the request URI.</span></span> <span data-ttu-id="0b338-114">*항목* 매개 변수는 복합 유형 이므로 Web API는 미디어 유형 포맷터를 사용 하 여 요청 본문에서 값을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-114">The *item* parameter is a complex type, so Web API uses a media-type formatter to read the value from the request body.</span></span>

<span data-ttu-id="0b338-115">URI에서 값을 가져오기 위해 Web API는 경로 데이터 및 URI 쿼리 문자열을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-115">To get a value from the URI, Web API looks in the route data and the URI query string.</span></span> <span data-ttu-id="0b338-116">경로 데이터는 라우팅 시스템이 URI를 구문 분석 하 여 경로와 일치 하는 경우에 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-116">The route data is populated when the routing system parses the URI and matches it to a route.</span></span> <span data-ttu-id="0b338-117">자세한 내용은 [라우팅 및 작업 선택](../web-api-routing-and-actions/routing-and-action-selection.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0b338-117">For more information, see [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span>

<span data-ttu-id="0b338-118">이 문서의 나머지 부분에서는 모델 바인딩 프로세스를 사용자 지정할 수 있는 방법을 보여 드리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-118">In the rest of this article, I'll show how you can customize the model binding process.</span></span> <span data-ttu-id="0b338-119">그러나 복합 형식의 경우 가능한 경우 미디어 형식 포맷터를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-119">For complex types, however, consider using media-type formatters whenever possible.</span></span> <span data-ttu-id="0b338-120">HTTP의 주요 원칙은 리소스의 표현을 지정 하는 콘텐츠 협상을 사용 하 여 메시지 본문에서 리소스를 보내는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-120">A key principle of HTTP is that resources are sent in the message body, using content negotiation to specify the representation of the resource.</span></span> <span data-ttu-id="0b338-121">미디어 유형 포맷터는 정확히 이러한 용도로 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-121">Media-type formatters were designed for exactly this purpose.</span></span>

## <a name="using-fromuri"></a><span data-ttu-id="0b338-122">Using [FromUri]</span><span class="sxs-lookup"><span data-stu-id="0b338-122">Using [FromUri]</span></span>

<span data-ttu-id="0b338-123">Web API가 URI에서 복합 형식을 읽도록 하려면 **[Fromuri]** 특성을 매개 변수에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-123">To force Web API to read a complex type from the URI, add the **[FromUri]** attribute to the parameter.</span></span> <span data-ttu-id="0b338-124">다음 예제에서는 URI `GeoPoint` `GeoPoint` 에서을 가져오는 컨트롤러 메서드와 함께 형식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-124">The following example defines a `GeoPoint` type, along with a controller method that gets the `GeoPoint` from the URI.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="0b338-125">클라이언트는 쿼리 문자열에 위도 및 경도 값을 입력할 수 있으며 Web API는이 값을 사용 하 여 `GeoPoint`를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-125">The client can put the Latitude and Longitude values in the query string and Web API will use them to construct a `GeoPoint`.</span></span> <span data-ttu-id="0b338-126">예:</span><span class="sxs-lookup"><span data-stu-id="0b338-126">For example:</span></span>

`http://localhost/api/values/?Latitude=47.678558&Longitude=-122.130989`

## <a name="using-frombody"></a><span data-ttu-id="0b338-127">[FromBody] 사용</span><span class="sxs-lookup"><span data-stu-id="0b338-127">Using [FromBody]</span></span>

<span data-ttu-id="0b338-128">Web API가 요청 본문에서 단순 유형을 읽도록 하려면 **[Frombody]** 특성을 매개 변수에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-128">To force Web API to read a simple type from the request body, add the **[FromBody]** attribute to the parameter:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="0b338-129">이 예제에서 Web API는 미디어 유형 포맷터를 사용 하 여 요청 본문에서 *이름* 값을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-129">In this example, Web API will use a media-type formatter to read the value of *name* from the request body.</span></span> <span data-ttu-id="0b338-130">클라이언트 요청 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-130">Here is an example client request.</span></span>

[!code-console[Main](parameter-binding-in-aspnet-web-api/samples/sample4.cmd)]

<span data-ttu-id="0b338-131">매개 변수에 [FromBody]가 있는 경우 Web API는 Content-type 헤더를 사용 하 여 포맷터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-131">When a parameter has [FromBody], Web API uses the Content-Type header to select a formatter.</span></span> <span data-ttu-id="0b338-132">이 예제에서 콘텐츠 형식은 application/json &quot;&quot; 이 고 요청 본문은 json 개체가 아닌 원시 json 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-132">In this example, the content type is &quot;application/json&quot; and the request body is a raw JSON string (not a JSON object).</span></span>

<span data-ttu-id="0b338-133">메시지 본문에서 최대 하나의 매개 변수만 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-133">At most one parameter is allowed to read from the message body.</span></span> <span data-ttu-id="0b338-134">따라서이 작업은 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-134">So this will not work:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="0b338-135">이 규칙의 이유는 요청 본문이 한 번만 읽을 수 있는 버퍼링 되지 않은 스트림에 저장 될 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-135">The reason for this rule is that the request body might be stored in a non-buffered stream that can only be read once.</span></span>

## <a name="type-converters"></a><span data-ttu-id="0b338-136">형식 변환기</span><span class="sxs-lookup"><span data-stu-id="0b338-136">Type Converters</span></span>

<span data-ttu-id="0b338-137">웹 api에서 **TypeConverter** 를 만들고 문자열 변환을 제공 하 여 클래스를 단순 형식으로 처리 하도록 할 수 있습니다. 즉, web API가 URI에서 해당 클래스를 바인딩하려는 것을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-137">You can make Web API treat a class as a simple type (so that Web API will try to bind it from the URI) by creating a **TypeConverter** and providing a string conversion.</span></span>

<span data-ttu-id="0b338-138">다음 코드에서는 지리적 지점을 `GeoPoint` 나타내는 클래스와 문자열에서 `GeoPoint` 인스턴스로 변환 하는 **TypeConverter** 를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-138">The following code shows a `GeoPoint` class that represents a geographical point, plus a **TypeConverter** that converts from strings to `GeoPoint` instances.</span></span> <span data-ttu-id="0b338-139">클래스 `GeoPoint` 는 **[TypeConverter]** 특성으로 데코레이팅 되어 형식 변환기를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-139">The `GeoPoint` class is decorated with a **[TypeConverter]** attribute to specify the type converter.</span></span> <span data-ttu-id="0b338-140">(이 예제는 Mike 정지의 블로그 게시물 [MVC/WebAPI에서 작업 서명의 사용자 지정 개체에 바인딩하는 방법](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)에 대해 설명 했습니다.)</span><span class="sxs-lookup"><span data-stu-id="0b338-140">(This example was inspired by Mike Stall's blog post [How to bind to custom objects in action signatures in MVC/WebAPI](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx).)</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="0b338-141">이제 Web API는 단순 `GeoPoint` 유형으로 처리 합니다. 즉, URI에서 매개 변수 `GeoPoint` 를 바인딩하려 려 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-141">Now Web API will treat `GeoPoint` as a simple type, meaning it will try to bind `GeoPoint` parameters from the URI.</span></span> <span data-ttu-id="0b338-142">매개 변수에 **[Fromuri]** 를 포함할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-142">You don't need to include **[FromUri]** on the parameter.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="0b338-143">클라이언트는 다음과 같은 URI를 사용 하 여 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-143">The client can invoke the method with a URI like this:</span></span>

`http://localhost/api/values/?location=47.678558,-122.130989`

## <a name="model-binders"></a><span data-ttu-id="0b338-144">모델 바인더</span><span class="sxs-lookup"><span data-stu-id="0b338-144">Model Binders</span></span>

<span data-ttu-id="0b338-145">형식 변환기 보다 더 유연한 옵션은 사용자 지정 모델 바인더를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-145">A more flexible option than a type converter is to create a custom model binder.</span></span> <span data-ttu-id="0b338-146">모델 바인더를 사용 하 여 HTTP 요청, 작업 설명 및 경로 데이터의 원시 값과 같은 항목에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-146">With a model binder, you have access to things like the HTTP request, the action description, and the raw values from the route data.</span></span>

<span data-ttu-id="0b338-147">모델 바인더를 만들려면 **Imodelbinder** 인터페이스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-147">To create a model binder, implement the **IModelBinder** interface.</span></span> <span data-ttu-id="0b338-148">이 인터페이스는 단일 메서드인 **Bindmodel**을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-148">This interface defines a single method, **BindModel**:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample8.cs)]

<span data-ttu-id="0b338-149">개체에 대 한 `GeoPoint` 모델 바인더는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-149">Here is a model binder for `GeoPoint` objects.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample9.cs)]

<span data-ttu-id="0b338-150">모델 바인더는 *값 공급자*에서 원시 입력 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-150">A model binder gets raw input values from a *value provider*.</span></span> <span data-ttu-id="0b338-151">이 디자인은 두 가지 고유한 함수를 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-151">This design separates two distinct functions:</span></span>

- <span data-ttu-id="0b338-152">값 공급자는 HTTP 요청을 사용 하 여 키-값 쌍의 사전을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-152">The value provider takes the HTTP request and populates a dictionary of key-value pairs.</span></span>
- <span data-ttu-id="0b338-153">모델 바인더는이 사전을 사용 하 여 모델을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-153">The model binder uses this dictionary to populate the model.</span></span>

<span data-ttu-id="0b338-154">Web API의 기본 값 공급자는 경로 데이터 및 쿼리 문자열에서 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-154">The default value provider in Web API gets values from the route data and the query string.</span></span> <span data-ttu-id="0b338-155">예를 들어 URI가 인 `http://localhost/api/values/1?location=48,-122`경우 값 공급자는 다음 키-값 쌍을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-155">For example, if the URI is `http://localhost/api/values/1?location=48,-122`, the value provider creates the following key-value pairs:</span></span>

- <span data-ttu-id="0b338-156">id = &quot;1&quot;</span><span class="sxs-lookup"><span data-stu-id="0b338-156">id = &quot;1&quot;</span></span>
- <span data-ttu-id="0b338-157">location = &quot;48,122&quot;</span><span class="sxs-lookup"><span data-stu-id="0b338-157">location = &quot;48,122&quot;</span></span>

<span data-ttu-id="0b338-158">(Api/{controller}/{id} &quot;&quot;인 기본 경로 템플릿을 가정 합니다.)</span><span class="sxs-lookup"><span data-stu-id="0b338-158">(I'm assuming the default route template, which is &quot;api/{controller}/{id}&quot;.)</span></span>

<span data-ttu-id="0b338-159">바인딩할 매개 변수의 이름은 **ModelBindingContext** 속성에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-159">The name of the parameter to bind is stored in the **ModelBindingContext.ModelName** property.</span></span> <span data-ttu-id="0b338-160">모델 바인더는 사전에서이 값을 사용 하 여 키를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-160">The model binder looks for a key with this value in the dictionary.</span></span> <span data-ttu-id="0b338-161">값이 존재 하 고로 `GeoPoint`변환할 수 있는 경우 모델 바인더는 **ModelBindingContext** 속성에 바인딩된 값을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-161">If the value exists and can be converted into a `GeoPoint`, the model binder assigns the bound value to the **ModelBindingContext.Model** property.</span></span>

<span data-ttu-id="0b338-162">모델 바인더는 단순 형식 변환으로 제한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-162">Notice that the model binder is not limited to a simple type conversion.</span></span> <span data-ttu-id="0b338-163">이 예에서 모델 바인더는 먼저 알려진 위치 테이블을 확인 하 고, 실패 하면 형식 변환을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-163">In this example, the model binder first looks in a table of known locations, and if that fails, it uses type conversion.</span></span>

<span data-ttu-id="0b338-164">**모델 바인더 설정**</span><span class="sxs-lookup"><span data-stu-id="0b338-164">**Setting the Model Binder**</span></span>

<span data-ttu-id="0b338-165">모델 바인더를 설정 하는 방법에는 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-165">There are several ways to set a model binder.</span></span> <span data-ttu-id="0b338-166">먼저 **[Modelbinder]** 특성을 매개 변수에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-166">First, you can add a **[ModelBinder]** attribute to the parameter.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample10.cs)]

<span data-ttu-id="0b338-167">**[Modelbinder]** 특성을 형식에 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-167">You can also add a **[ModelBinder]** attribute to the type.</span></span> <span data-ttu-id="0b338-168">Web API는 해당 형식의 모든 매개 변수에 대해 지정 된 모델 바인더를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-168">Web API will use the specified model binder for all parameters of that type.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample11.cs)]

<span data-ttu-id="0b338-169">마지막으로 **Httpconfiguration**에 모델 바인더 공급자를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-169">Finally, you can add a model-binder provider to the **HttpConfiguration**.</span></span> <span data-ttu-id="0b338-170">모델 바인더 공급자는 단순히 모델 바인더를 만드는 팩터리 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-170">A model-binder provider is simply a factory class that creates a model binder.</span></span> <span data-ttu-id="0b338-171">[Modelbinderprovider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx) 클래스에서 파생 시켜 공급자를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-171">You can create a provider by deriving from the [ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx) class.</span></span> <span data-ttu-id="0b338-172">그러나 모델 바인더에서 단일 형식을 처리 하는 경우이 용도로 설계 된 기본 제공 **Simplemodelbinderprovider**를 사용 하는 것이 더 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-172">However, if your model binder handles a single type, it's easier to use the built-in **SimpleModelBinderProvider**, which is designed for this purpose.</span></span> <span data-ttu-id="0b338-173">다음 코드에서는 이 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-173">The following code shows how to do this.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample12.cs)]

<span data-ttu-id="0b338-174">모델 바인딩 공급자를 사용 하는 경우에도 **[modelbinder]** 특성을 매개 변수에 추가 하 여 미디어 형식 포맷터가 아니라 모델 바인더를 사용 해야 한다는 것을 Web API에 알려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-174">With a model-binding provider, you still need to add the **[ModelBinder]** attribute to the parameter, to tell Web API that it should use a model binder and not a media-type formatter.</span></span> <span data-ttu-id="0b338-175">하지만 이제는 특성에 모델 바인더의 형식을 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-175">But now you don't need to specify the type of model binder in the attribute:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample13.cs)]

## <a name="value-providers"></a><span data-ttu-id="0b338-176">값 공급자</span><span class="sxs-lookup"><span data-stu-id="0b338-176">Value Providers</span></span>

<span data-ttu-id="0b338-177">모델 바인더가 값 공급자에서 값을 가져오는 것을 언급 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-177">I mentioned that a model binder gets values from a value provider.</span></span> <span data-ttu-id="0b338-178">사용자 지정 값 공급자를 쓰려면 **Ivalueprovider** 인터페이스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-178">To write a custom value provider, implement the **IValueProvider** interface.</span></span> <span data-ttu-id="0b338-179">요청에서 쿠키의 값을 가져오는 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-179">Here is an example that pulls values from the cookies in the request:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample14.cs)]

<span data-ttu-id="0b338-180">**ValueProviderFactory** 클래스에서 파생 시켜 값 공급자 팩터리를 만들어야 하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-180">You also need to create a value provider factory by deriving from the **ValueProviderFactory** class.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample15.cs)]

<span data-ttu-id="0b338-181">다음과 같이 **Httpconfiguration** 에 값 공급자 팩터리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-181">Add the value provider factory to the **HttpConfiguration** as follows.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample16.cs)]

<span data-ttu-id="0b338-182">Web API는 모든 값 공급자를 작성 하므로 모델 바인더가 **Valueprovider. GetValue**를 호출 하면 모델 바인더는이를 생성할 수 있는 첫 번째 값 공급자에서 값을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-182">Web API composes all of the value providers, so when a model binder calls **ValueProvider.GetValue**, the model binder receives the value from the first value provider that is able to produce it.</span></span>

<span data-ttu-id="0b338-183">또는 다음과 같이 **valueprovider** 특성을 사용 하 여 매개 변수 수준에서 값 공급자 팩터리를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-183">Alternatively, you can set the value provider factory at the parameter level by using the **ValueProvider** attribute, as follows:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample17.cs)]

<span data-ttu-id="0b338-184">이렇게 하면 웹 API는 지정 된 값 공급자 팩터리를 사용 하 여 모델 바인딩을 사용 하 고 다른 등록 된 값 공급자는 사용 하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-184">This tells Web API to use model binding with the specified value provider factory, and not to use any of the other registered value providers.</span></span>

## <a name="httpparameterbinding"></a><span data-ttu-id="0b338-185">HttpParameterBinding</span><span class="sxs-lookup"><span data-stu-id="0b338-185">HttpParameterBinding</span></span>

<span data-ttu-id="0b338-186">모델 바인더는 보다 일반적인 메커니즘의 특정 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-186">Model binders are a specific instance of a more general mechanism.</span></span> <span data-ttu-id="0b338-187">**[Modelbinder]** 특성을 살펴보면 추상 **parameterbindingattribute** 클래스에서 파생 되는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-187">If you look at the **[ModelBinder]** attribute, you will see that it derives from the abstract **ParameterBindingAttribute** class.</span></span> <span data-ttu-id="0b338-188">이 클래스는 **Httpparameterbinding** 개체를 반환 하는 단일 메서드인 **GetBinding**를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-188">This class defines a single method, **GetBinding**, which returns an **HttpParameterBinding** object:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample18.cs)]

<span data-ttu-id="0b338-189">**Httpparameterbinding** 은 값에 매개 변수를 바인딩하는 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-189">An **HttpParameterBinding** is responsible for binding a parameter to a value.</span></span> <span data-ttu-id="0b338-190">**[Modelbinder]** 의 경우 특성은 **imodelbinder** 를 사용 하 여 실제 바인딩을 수행 하는 **httpparameterbinding** 구현을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-190">In the case of **[ModelBinder]**, the attribute returns an **HttpParameterBinding** implementation that uses an **IModelBinder** to perform the actual binding.</span></span> <span data-ttu-id="0b338-191">사용자 고유의 **Httpparameterbinding**을 구현할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-191">You can also implement your own **HttpParameterBinding**.</span></span>

<span data-ttu-id="0b338-192">예를 들어 요청에서 etag `if-match` 및 `if-none-match` 헤더를 가져오려고 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-192">For example, suppose you want to get ETags from `if-match` and `if-none-match` headers in the request.</span></span> <span data-ttu-id="0b338-193">먼저 Etag를 나타내는 클래스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-193">We'll start by defining a class to represent ETags.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample19.cs)]

<span data-ttu-id="0b338-194">또한 `if-match` 헤더`if-none-match` 또는 헤더에서 ETag를 가져올 것인지 여부를 나타내는 열거형을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-194">We'll also define an enumeration to indicate whether to get the ETag from the `if-match` header or the `if-none-match` header.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample20.cs)]

<span data-ttu-id="0b338-195">다음은 원하는 헤더에서 ETag를 가져와 ETag 형식의 매개 변수에 바인딩하는 **Httpparameterbinding** 입니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-195">Here is an **HttpParameterBinding** that gets the ETag from the desired header and binds it to a parameter of type ETag:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample21.cs)]

<span data-ttu-id="0b338-196">**Executebindingasync** 메서드는 바인딩을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-196">The **ExecuteBindingAsync** method does the binding.</span></span> <span data-ttu-id="0b338-197">이 메서드 내에서 **Httpactioncontext**의 **actionargument** 사전에 바인딩된 매개 변수 값을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-197">Within this method, add the bound parameter value to the **ActionArgument** dictionary in the **HttpActionContext**.</span></span>

> [!NOTE]
> <span data-ttu-id="0b338-198">**Executebindingasync** 메서드가 요청 메시지의 본문을 읽는 경우 **WillReadBody** 속성을 재정의 하 여 true를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-198">If your **ExecuteBindingAsync** method reads the body of the request message, override the **WillReadBody** property to return true.</span></span> <span data-ttu-id="0b338-199">요청 본문은 한 번만 읽을 수 있는 버퍼링 되지 않은 스트림이 될 수 있으므로 Web API는 하나 이상의 바인딩이 메시지 본문을 읽을 수 있는 규칙을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-199">The request body might be an unbuffered stream that can only be read once, so Web API enforces a rule that at most one binding can read the message body.</span></span>

<span data-ttu-id="0b338-200">사용자 지정 **Httpparameterbinding**을 적용 하려면 **parameterbindingattribute**에서 파생 되는 특성을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-200">To apply a custom **HttpParameterBinding**, you can define an attribute that derives from **ParameterBindingAttribute**.</span></span> <span data-ttu-id="0b338-201">의 `ETagParameterBinding`경우 `if-match` 헤더와 헤더에 `if-none-match` 대해 각각 하나씩 두 개의 특성을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-201">For `ETagParameterBinding`, we'll define two attributes, one for `if-match` headers and one for `if-none-match` headers.</span></span> <span data-ttu-id="0b338-202">둘 다 추상 기본 클래스에서 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-202">Both derive from an abstract base class.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample22.cs)]

<span data-ttu-id="0b338-203">특성을 `[IfNoneMatch]` 사용 하는 컨트롤러 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-203">Here is a controller method that uses the `[IfNoneMatch]` attribute.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample23.cs)]

<span data-ttu-id="0b338-204">**Parameterbindingattribute**외에도 사용자 지정 **httpparameterbinding**을 추가 하는 또 다른 후크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-204">Besides **ParameterBindingAttribute**, there is another hook for adding a custom **HttpParameterBinding**.</span></span> <span data-ttu-id="0b338-205">**Httpconfiguration** 개체에서 **ParameterBindingRules** 속성은 (**httpparameterdescriptor**  - &gt; **httpparameterbinding**) 형식의 익명 함수 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-205">On the **HttpConfiguration** object, the **ParameterBindingRules** property is a collection of anonymous functions of type (**HttpParameterDescriptor** -&gt; **HttpParameterBinding**).</span></span> <span data-ttu-id="0b338-206">예를 들어 GET 메서드의 ETag 매개 변수가에서 사용 `ETagParameterBinding` `if-none-match`하는 규칙을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-206">For example, you could add a rule that any ETag parameter on a GET method uses `ETagParameterBinding` with `if-none-match`:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample24.cs)]

<span data-ttu-id="0b338-207">함수는 바인딩이 적용 `null` 되지 않는 매개 변수에 대 한를 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-207">The function should return `null` for parameters where the binding is not applicable.</span></span>

## <a name="iactionvaluebinder"></a><span data-ttu-id="0b338-208">IActionValueBinder</span><span class="sxs-lookup"><span data-stu-id="0b338-208">IActionValueBinder</span></span>

<span data-ttu-id="0b338-209">전체 매개 변수 바인딩 프로세스는 플러그형 서비스인 **Iactionvaluebinder**에 의해 제어 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-209">The entire parameter-binding process is controlled by a pluggable service, **IActionValueBinder**.</span></span> <span data-ttu-id="0b338-210">**Iactionvaluebinder** 의 기본 구현에서는 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-210">The default implementation of **IActionValueBinder** does the following:</span></span>

1. <span data-ttu-id="0b338-211">매개 변수에서 **Parameterbindingattribute** 를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-211">Look for a **ParameterBindingAttribute** on the parameter.</span></span> <span data-ttu-id="0b338-212">여기에는 **[Frombody]** , **[frombody]** , **[modelbinder]** 또는 사용자 지정 특성이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-212">This includes **[FromBody]**, **[FromUri]**, and **[ModelBinder]**, or custom attributes.</span></span>
2. <span data-ttu-id="0b338-213">그렇지 않으면 null이 아닌 **Httpparameterbinding**을 반환 하는 함수에 대 한 ParameterBindingRules를 확인 합니다 **.**</span><span class="sxs-lookup"><span data-stu-id="0b338-213">Otherwise, look in **HttpConfiguration.ParameterBindingRules** for a function that returns a non-null **HttpParameterBinding**.</span></span>
3. <span data-ttu-id="0b338-214">그렇지 않으면 앞에서 설명한 기본 규칙을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-214">Otherwise, use the default rules that I described previously.</span></span> 

    - <span data-ttu-id="0b338-215">매개 변수 형식이 "simple" 이거나 형식 변환기를 포함 하는 경우 URI에서 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-215">If the parameter type is "simple"or has a type converter, bind from the URI.</span></span> <span data-ttu-id="0b338-216">이는 **[Fromuri]** 특성을 매개 변수에 넣는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-216">This is equivalent to putting the **[FromUri]** attribute on the parameter.</span></span>
    - <span data-ttu-id="0b338-217">그렇지 않으면 메시지 본문에서 매개 변수를 읽으려고 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-217">Otherwise, try to read the parameter from the message body.</span></span> <span data-ttu-id="0b338-218">이것은 매개 변수에 **[Frombody]** 를 배치 하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-218">This is equivalent to putting **[FromBody]** on the parameter.</span></span>

<span data-ttu-id="0b338-219">원하는 경우 전체 **Iactionvaluebinder** 서비스를 사용자 지정 구현으로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-219">If you wanted, you could replace the entire **IActionValueBinder** service with a custom implementation.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0b338-220">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="0b338-220">Additional Resources</span></span>

[<span data-ttu-id="0b338-221">사용자 지정 매개 변수 바인딩 샘플</span><span class="sxs-lookup"><span data-stu-id="0b338-221">Custom Parameter Binding Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/CustomParameterBinding/ReadMe.txt)

<span data-ttu-id="0b338-222">Mike 정지는 Web API 매개 변수 바인딩에 대 한 좋은 일련의 블로그 게시물을 작성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0b338-222">Mike Stall wrote a good series of blog posts about Web API parameter binding:</span></span>

- [<span data-ttu-id="0b338-223">Web API에서 매개 변수 바인딩을 수행 하는 방법</span><span class="sxs-lookup"><span data-stu-id="0b338-223">How Web API does Parameter Binding</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/16/how-webapi-does-parameter-binding.aspx)
- [<span data-ttu-id="0b338-224">Web API에 대 한 MVC 스타일 매개 변수 바인딩</span><span class="sxs-lookup"><span data-stu-id="0b338-224">MVC Style parameter binding for Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/18/mvc-style-parameter-binding-for-webapi.aspx)
- [<span data-ttu-id="0b338-225">MVC/Web API에서 작업 서명의 사용자 지정 개체에 바인딩하는 방법</span><span class="sxs-lookup"><span data-stu-id="0b338-225">How to bind to custom objects in action signatures in MVC/Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)
- [<span data-ttu-id="0b338-226">Web API에서 사용자 지정 값 공급자를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="0b338-226">How to create a custom value provider in Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)
- [<span data-ttu-id="0b338-227">웹 API 매개 변수를 내부적으로 바인딩</span><span class="sxs-lookup"><span data-stu-id="0b338-227">Web API Parameter binding under the hood</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)
