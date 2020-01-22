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
ms.openlocfilehash: 032368f94ce32cf6231458649e8fdd42bee685e9
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519260"
---
# <a name="parameter-binding-in-aspnet-web-api"></a>ASP.NET Web API의 매개 변수 바인딩

[Mike Wasson](https://github.com/MikeWasson)

[!INCLUDE[](~/includes/coreWebAPI.md)]

이 문서에서는 Web API가 매개 변수를 바인딩하는 방법과 바인딩 프로세스를 사용자 지정 하는 방법을 설명 합니다. 웹 API는 컨트롤러에서 메서드를 호출할 때 *바인딩*이라는 프로세스 인 매개 변수에 대 한 값을 설정 해야 합니다.

기본적으로 웹 API는 다음 규칙을 사용 하 여 매개 변수를 바인딩합니다.

- 매개 변수가 "simple" 형식이 면 Web API는 URI에서 값을 가져오려고 시도 합니다. 단순 형식에는 .NET [기본 형식](https://msdn.microsoft.com/library/system.type.isprimitive.aspx) (**int**, **bool**, **double**등)과 **TimeSpan**, **DateTime**, **Guid**, **decimal**및 **string**과 문자열에서 변환할 수 있는 형식 변환기가 *있는 모든 형식이* 포함 됩니다. 형식 변환기에 대 한 자세한 내용은 뒷부분에 있습니다.
- 복합 형식의 경우 Web API는 [미디어 형식 포맷터](media-formatters.md)를 사용 하 여 메시지 본문에서 값을 읽으려고 시도 합니다.

예를 들어 다음은 일반적인 Web API controller 메서드입니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample1.cs)]

*Id* 매개 변수는 &quot;단순&quot; 유형 이므로 Web API는 요청 URI에서 값을 가져오려고 시도 합니다. *항목* 매개 변수는 복합 유형 이므로 Web API는 미디어 유형 포맷터를 사용 하 여 요청 본문에서 값을 읽습니다.

URI에서 값을 가져오기 위해 Web API는 경로 데이터 및 URI 쿼리 문자열을 찾습니다. 경로 데이터는 라우팅 시스템이 URI를 구문 분석 하 여 경로와 일치 하는 경우에 채워집니다. 자세한 내용은 [라우팅 및 작업 선택](../web-api-routing-and-actions/routing-and-action-selection.md)을 참조 하세요.

이 문서의 나머지 부분에서는 모델 바인딩 프로세스를 사용자 지정할 수 있는 방법을 보여 드리겠습니다. 그러나 복합 형식의 경우 가능한 경우 미디어 형식 포맷터를 사용 하는 것이 좋습니다. HTTP의 주요 원칙은 리소스의 표현을 지정 하는 콘텐츠 협상을 사용 하 여 메시지 본문에서 리소스를 보내는 것입니다. 미디어 유형 포맷터는 정확히 이러한 용도로 설계 되었습니다.

## <a name="using-fromuri"></a>Using [FromUri]

Web API가 URI에서 복합 형식을 읽도록 하려면 **[Fromuri]** 특성을 매개 변수에 추가 합니다. 다음 예제에서는 URI에서 `GeoPoint`를 가져오는 컨트롤러 메서드와 함께 `GeoPoint` 형식을 정의 합니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample2.cs)]

클라이언트는 쿼리 문자열에 위도 및 경도 값을 입력할 수 있으며 Web API는이 값을 사용 하 여 `GeoPoint`를 생성 합니다. 예를 들면 다음과 같습니다.:

`http://localhost/api/values/?Latitude=47.678558&Longitude=-122.130989`

## <a name="using-frombody"></a>[FromBody] 사용

Web API가 요청 본문에서 단순 유형을 읽도록 하려면 **[Frombody]** 특성을 매개 변수에 추가 합니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample3.cs)]

이 예제에서 Web API는 미디어 유형 포맷터를 사용 하 여 요청 본문에서 *이름* 값을 읽습니다. 클라이언트 요청 예제는 다음과 같습니다.

[!code-console[Main](parameter-binding-in-aspnet-web-api/samples/sample4.cmd)]

매개 변수에 [FromBody]가 있는 경우 Web API는 Content-type 헤더를 사용 하 여 포맷터를 선택 합니다. 이 예제에서 콘텐츠 형식은 &quot;application/json&quot; 이며, 요청 본문은 JSON 개체가 아닌 원시 JSON 문자열입니다.

메시지 본문에서 최대 하나의 매개 변수만 읽을 수 있습니다. 따라서이 작업은 작동 하지 않습니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample5.cs)]

이 규칙의 이유는 요청 본문이 한 번만 읽을 수 있는 버퍼링 되지 않은 스트림에 저장 될 수 있기 때문입니다.

## <a name="type-converters"></a>형식 변환기

웹 api에서 **TypeConverter** 를 만들고 문자열 변환을 제공 하 여 클래스를 단순 형식으로 처리 하도록 할 수 있습니다. 즉, web API가 URI에서 해당 클래스를 바인딩하려는 것을 시도 합니다.

다음 코드에서는 지리적 지점을 나타내는 `GeoPoint` 클래스와 문자열에서 `GeoPoint` 인스턴스로 변환 하는 **TypeConverter** 를 보여 줍니다. `GeoPoint` 클래스는 **[TypeConverter]** 특성으로 데코레이팅 되어 형식 변환기를 지정 합니다. (이 예제는 Mike 정지의 블로그 게시물 [MVC/WebAPI에서 작업 서명의 사용자 지정 개체에 바인딩하는 방법](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)에 대해 설명 했습니다.)

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample6.cs)]

이제 Web API는 `GeoPoint`를 단순 형식으로 처리 합니다. 즉, URI에서 `GeoPoint` 매개 변수를 바인딩하려고 시도 합니다. 매개 변수에 **[Fromuri]** 를 포함할 필요가 없습니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample7.cs)]

클라이언트는 다음과 같은 URI를 사용 하 여 메서드를 호출할 수 있습니다.

`http://localhost/api/values/?location=47.678558,-122.130989`

## <a name="model-binders"></a>모델 바인더

형식 변환기 보다 더 유연한 옵션은 사용자 지정 모델 바인더를 만드는 것입니다. 모델 바인더를 사용 하 여 HTTP 요청, 작업 설명 및 경로 데이터의 원시 값과 같은 항목에 액세스할 수 있습니다.

모델 바인더를 만들려면 **Imodelbinder** 인터페이스를 구현 합니다. 이 인터페이스는 단일 메서드인 **Bindmodel**을 정의 합니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample8.cs)]

`GeoPoint` 개체에 대 한 모델 바인더는 다음과 같습니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample9.cs)]

모델 바인더는 *값 공급자*에서 원시 입력 값을 가져옵니다. 이 디자인은 두 가지 고유한 함수를 구분 합니다.

- 값 공급자는 HTTP 요청을 사용 하 여 키-값 쌍의 사전을 채웁니다.
- 모델 바인더는이 사전을 사용 하 여 모델을 채웁니다.

Web API의 기본 값 공급자는 경로 데이터 및 쿼리 문자열에서 값을 가져옵니다. 예를 들어 URI가 `http://localhost/api/values/1?location=48,-122`경우 값 공급자는 다음 키-값 쌍을 만듭니다.

- id = &quot;1&quot;
- location = &quot;48,122&quot;

(&quot;api/{controller}/{id}&quot;기본 경로 템플릿을 가정 합니다.)

바인딩할 매개 변수의 이름은 **ModelBindingContext** 속성에 저장 됩니다. 모델 바인더는 사전에서이 값을 사용 하 여 키를 찾습니다. 값이 존재 하 고 `GeoPoint`변환할 수 있으면 모델 바인더는 바인딩된 값을 **ModelBindingContext** 속성에 할당 합니다.

모델 바인더는 단순 형식 변환으로 제한 되지 않습니다. 이 예에서 모델 바인더는 먼저 알려진 위치 테이블을 확인 하 고, 실패 하면 형식 변환을 사용 합니다.

**모델 바인더 설정**

모델 바인더를 설정 하는 방법에는 여러 가지가 있습니다. 먼저 **[Modelbinder]** 특성을 매개 변수에 추가할 수 있습니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample10.cs)]

**[Modelbinder]** 특성을 형식에 추가할 수도 있습니다. Web API는 해당 형식의 모든 매개 변수에 대해 지정 된 모델 바인더를 사용 합니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample11.cs)]

마지막으로 **Httpconfiguration**에 모델 바인더 공급자를 추가할 수 있습니다. 모델 바인더 공급자는 단순히 모델 바인더를 만드는 팩터리 클래스입니다. [Modelbinderprovider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx) 클래스에서 파생 시켜 공급자를 만들 수 있습니다. 그러나 모델 바인더에서 단일 형식을 처리 하는 경우이 용도로 설계 된 기본 제공 **Simplemodelbinderprovider**를 사용 하는 것이 더 쉽습니다. 다음 코드에서는 이 작업을 수행하는 방법을 보여 줍니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample12.cs)]

모델 바인딩 공급자를 사용 하는 경우에도 **[modelbinder]** 특성을 매개 변수에 추가 하 여 미디어 형식 포맷터가 아니라 모델 바인더를 사용 해야 한다는 것을 Web API에 알려야 합니다. 하지만 이제는 특성에 모델 바인더의 형식을 지정할 필요가 없습니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample13.cs)]

## <a name="value-providers"></a>값 공급자

모델 바인더가 값 공급자에서 값을 가져오는 것을 언급 했습니다. 사용자 지정 값 공급자를 쓰려면 **Ivalueprovider** 인터페이스를 구현 합니다. 요청에서 쿠키의 값을 가져오는 예제는 다음과 같습니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample14.cs)]

**ValueProviderFactory** 클래스에서 파생 시켜 값 공급자 팩터리를 만들어야 하는 경우도 있습니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample15.cs)]

다음과 같이 **Httpconfiguration** 에 값 공급자 팩터리를 추가 합니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample16.cs)]

Web API는 모든 값 공급자를 작성 하므로 모델 바인더가 **Valueprovider. GetValue**를 호출 하면 모델 바인더는이를 생성할 수 있는 첫 번째 값 공급자에서 값을 받습니다.

또는 다음과 같이 **valueprovider** 특성을 사용 하 여 매개 변수 수준에서 값 공급자 팩터리를 설정할 수 있습니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample17.cs)]

이렇게 하면 웹 API는 지정 된 값 공급자 팩터리를 사용 하 여 모델 바인딩을 사용 하 고 다른 등록 된 값 공급자는 사용 하지 않도록 합니다.

## <a name="httpparameterbinding"></a>HttpParameterBinding

모델 바인더는 보다 일반적인 메커니즘의 특정 인스턴스입니다. **[Modelbinder]** 특성을 살펴보면 추상 **parameterbindingattribute** 클래스에서 파생 되는 것을 볼 수 있습니다. 이 클래스는 **Httpparameterbinding** 개체를 반환 하는 단일 메서드인 **GetBinding**를 정의 합니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample18.cs)]

**Httpparameterbinding** 은 값에 매개 변수를 바인딩하는 역할을 합니다. **[Modelbinder]** 의 경우 특성은 **imodelbinder** 를 사용 하 여 실제 바인딩을 수행 하는 **httpparameterbinding** 구현을 반환 합니다. 사용자 고유의 **Httpparameterbinding**을 구현할 수도 있습니다.

예를 들어 `if-match`에서 Etag를 가져오고 요청에서 헤더를 `if-none-match` 하려고 한다고 가정 합니다. 먼저 Etag를 나타내는 클래스를 정의 합니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample19.cs)]

또한 `if-match` 헤더 또는 `if-none-match` 헤더에서 ETag를 가져올 것인지 여부를 나타내는 열거형을 정의 합니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample20.cs)]

다음은 원하는 헤더에서 ETag를 가져와 ETag 형식의 매개 변수에 바인딩하는 **Httpparameterbinding** 입니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample21.cs)]

**Executebindingasync** 메서드는 바인딩을 수행 합니다. 이 메서드 내에서 **Httpactioncontext**의 **actionargument** 사전에 바인딩된 매개 변수 값을 추가 합니다.

> [!NOTE]
> **Executebindingasync** 메서드가 요청 메시지의 본문을 읽는 경우 **WillReadBody** 속성을 재정의 하 여 true를 반환 합니다. 요청 본문은 한 번만 읽을 수 있는 버퍼링 되지 않은 스트림이 될 수 있으므로 Web API는 하나 이상의 바인딩이 메시지 본문을 읽을 수 있는 규칙을 적용 합니다.

사용자 지정 **Httpparameterbinding**을 적용 하려면 **parameterbindingattribute**에서 파생 되는 특성을 정의할 수 있습니다. `ETagParameterBinding`은 `if-match` 헤더와 `if-none-match` 헤더에 대 한 두 개의 특성을 정의 합니다. 둘 다 추상 기본 클래스에서 파생 됩니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample22.cs)]

`[IfNoneMatch]` 특성을 사용 하는 컨트롤러 메서드는 다음과 같습니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample23.cs)]

**Parameterbindingattribute**외에도 사용자 지정 **httpparameterbinding**을 추가 하는 또 다른 후크가 있습니다. **Httpconfiguration** 개체에서 **ParameterBindingRules** 속성은 (**Httpparameterdescriptor** -&gt; **httpparameterbinding**) 형식의 익명 함수 컬렉션입니다. 예를 들어 GET 메서드의 ETag 매개 변수가 `if-none-match`와 `ETagParameterBinding`를 사용 하는 규칙을 추가할 수 있습니다.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample24.cs)]

함수는 바인딩이 적용 되지 않는 매개 변수에 대 한 `null`를 반환 해야 합니다.

## <a name="iactionvaluebinder"></a>IActionValueBinder

전체 매개 변수 바인딩 프로세스는 플러그형 서비스인 **Iactionvaluebinder**에 의해 제어 됩니다. **Iactionvaluebinder** 의 기본 구현에서는 다음을 수행 합니다.

1. 매개 변수에서 **Parameterbindingattribute** 를 찾습니다. 여기에는 **[Frombody]** , **[frombody]** , **[modelbinder]** 또는 사용자 지정 특성이 포함 됩니다.
2. 그렇지 않으면 null이 아닌 **Httpparameterbinding**을 반환 하는 함수에 대 한 ParameterBindingRules를 확인 합니다 **.**
3. 그렇지 않으면 앞에서 설명한 기본 규칙을 사용 합니다. 

    - 매개 변수 형식이 "simple" 이거나 형식 변환기를 포함 하는 경우 URI에서 바인딩합니다. 이는 **[Fromuri]** 특성을 매개 변수에 넣는 것과 같습니다.
    - 그렇지 않으면 메시지 본문에서 매개 변수를 읽으려고 시도 합니다. 이것은 매개 변수에 **[Frombody]** 를 배치 하는 것과 같습니다.

원하는 경우 전체 **Iactionvaluebinder** 서비스를 사용자 지정 구현으로 바꿀 수 있습니다.

## <a name="additional-resources"></a>추가 리소스

[사용자 지정 매개 변수 바인딩 샘플](http://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/CustomParameterBinding)

Mike 정지는 Web API 매개 변수 바인딩에 대 한 좋은 일련의 블로그 게시물을 작성 했습니다.

- [Web API에서 매개 변수 바인딩을 수행 하는 방법](https://blogs.msdn.com/b/jmstall/archive/2012/04/16/how-webapi-does-parameter-binding.aspx)
- [Web API에 대 한 MVC 스타일 매개 변수 바인딩](https://blogs.msdn.com/b/jmstall/archive/2012/04/18/mvc-style-parameter-binding-for-webapi.aspx)
- [MVC/Web API에서 작업 서명의 사용자 지정 개체에 바인딩하는 방법](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)
- [Web API에서 사용자 지정 값 공급자를 만드는 방법](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)
- [웹 API 매개 변수를 내부적으로 바인딩](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)
