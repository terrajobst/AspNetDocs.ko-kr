---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: ASP.NET Web API 2에서 특성 라우팅 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 7da1805d8a7066e82743dc9bd7e024cc9813ee89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446999"
---
# <a name="attribute-routing-in-aspnet-web-api-2"></a>ASP.NET Web API 2에서 특성 라우팅

[Mike Wasson](https://github.com/MikeWasson)

*라우팅은* 웹 API가 작업에 대 한 URI와 일치 하는 방법입니다. Web API 2는 *특성 라우팅*이라는 새로운 유형의 라우팅을 지원 합니다. 이름에서 알 수 있듯이 특성 라우팅은 경로를 정의 하는 특성을 사용 합니다. 특성 라우팅은 웹 API에서 Uri를 보다 강력 하 게 제어할 수 있도록 합니다. 예를 들어 리소스 계층 구조를 설명 하는 Uri를 쉽게 만들 수 있습니다.

규칙 기반 라우팅 이라고 하는 이전 라우팅 스타일은 여전히 완전 하 게 지원 됩니다. 실제로 동일한 프로젝트에서 두 기법을 결합할 수 있습니다.

이 항목에서는 특성 라우팅을 사용 하도록 설정 하 고 특성 라우팅에 대 한 다양 한 옵션을 설명 합니다. 특성 라우팅을 사용 하는 종단 간 자습서는 [WEB API 2에서 특성 라우팅을 사용 하 여 REST API 만들기](create-a-rest-api-with-attribute-routing.md)를 참조 하세요.

## <a name="prerequisites"></a>사전 요구 사항

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional 또는 Enterprise edition

또는 NuGet 패키지 관리자를 사용 하 여 필요한 패키지를 설치 합니다. Visual Studio의 **도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a>특성을 라우팅하는 이유

Web API의 첫 번째 릴리스는 *규칙 기반* 라우팅을 사용 했습니다. 해당 라우팅 형식에서 기본적으로 매개 변수가 있는 문자열인 경로 템플릿을 하나 이상 정의 합니다. 프레임 워크는 요청을 받으면 경로 템플릿과 URI를 일치 시킵니다. 규칙 기반 라우팅에 대 한 자세한 내용은 [ASP.NET Web API 라우팅](routing-in-aspnet-web-api.md)을 참조 하세요.

규칙 기반 라우팅의 이점 중 하나는 템플릿이 단일 장소에서 정의 되 고 라우팅 규칙이 모든 컨트롤러에서 일관 되 게 적용 된다는 것입니다. 불행 하 게도 규칙 기반 라우팅은 RESTful Api에서 공통적으로 사용 되는 특정 URI 패턴을 지원 하기 어렵습니다. 예를 들어, 리소스에는 고객에 게 주문이 있고, 영화에는 행위자가 있으며, 책은 저자와 같은 하위 리소스가 포함 되어 있습니다. 이러한 관계를 반영 하는 Uri를 만드는 것은 자연스럽 게 수행 됩니다.

`/customers/1/orders`

이러한 유형의 URI는 규칙 기반 라우팅을 사용 하 여 만드는 것이 어렵습니다. 이 작업을 수행할 수 있지만 컨트롤러 또는 리소스 종류가 많은 경우 결과가 제대로 확장 되지 않습니다.

특성 라우팅을 사용 하 여이 URI에 대 한 경로를 정의 하는 것은 간단 합니다. 단순히 컨트롤러 작업에 특성을 추가 합니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

특성 라우팅이 용이 하 게 하는 몇 가지 다른 패턴은 다음과 같습니다.

**API 버전 관리**

이 예제에서 "/api/v1/products"는 "/api/v2/products"가 아닌 다른 컨트롤러로 라우팅됩니다.

`/api/v1/products`
`/api/v2/products`

**오버 로드 된 URI 세그먼트**

이 예제에서 "1"은 주문 번호 이지만 "보류 중"은 컬렉션에 매핑됩니다.

`/orders/1`
`/orders/pending`

**여러 매개 변수 형식**

이 예에서 "1"은 주문 번호 이지만 "2013/06/16"은 날짜를 지정 합니다.

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a>특성 라우팅 사용

특성 라우팅을 사용 하도록 설정 하려면 구성 하는 동안 **Maphttpattributeroutes** 를 호출 합니다. 이 확장 메서드는 **system.web. HttpConfigurationExtensions** 클래스에서 정의 됩니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

특성 라우팅은 [규칙 기반](routing-in-aspnet-web-api.md) 라우팅과 함께 사용할 수 있습니다. 규칙 기반 경로를 정의 하려면 **MapHttpRoute** 메서드를 호출 합니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

Web API를 구성 하는 방법에 대 한 자세한 내용은 [ASP.NET Web API 2 구성](../advanced/configuring-aspnet-web-api.md)을 참조 하세요.

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a>참고: Web API 1에서 마이그레이션

Web API 2 이전에 웹 API 프로젝트 템플릿은 다음과 같은 코드를 생성 했습니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

특성 라우팅이 사용 되는 경우이 코드는 예외를 throw 합니다. 특성 라우팅을 사용 하도록 기존 Web API 프로젝트를 업그레이드 하는 경우이 구성 코드를 다음으로 업데이트 해야 합니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> 자세한 내용은 [ASP.NET 호스팅을 사용 하 여 WEB API 구성](../advanced/configuring-aspnet-web-api.md#webhost)을 참조 하세요.

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a>경로 특성 추가

특성을 사용 하 여 정의 된 경로의 예는 다음과 같습니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

&quot;customers/{customerId}/orders&quot; 문자열은 경로에 대 한 URI 템플릿입니다. Web API는 요청 URI를 템플릿에 일치 시 키 려 고 합니다. 이 예에서 "customers" 및 "orders"는 리터럴 세그먼트 이며 "{customerId}"는 변수 매개 변수입니다. 다음 Uri는이 템플릿과 일치 합니다.

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

이 항목의 뒷부분에서 설명 하는 [제약 조건을](#constraints)사용 하 여 일치를 제한할 수 있습니다.

경로 템플릿의 &quot;{customerId}&quot; 매개 변수가 메서드의 *customerId* 매개 변수 이름과 일치 하는지 확인 합니다. Web API는 컨트롤러 작업을 호출할 때 경로 매개 변수를 바인딩하려 려 합니다. 예를 들어 URI가 `http://example.com/customers/1/orders`되는 경우 Web API는 동작의 *customerId* 매개 변수에 "1" 값을 바인딩하려고 합니다.

URI 템플릿에는 여러 매개 변수를 사용할 수 있습니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

경로 특성이 없는 컨트롤러 메서드는 규칙 기반 라우팅을 사용 합니다. 이런 방식으로 동일한 프로젝트에서 두 가지 유형의 라우팅을 결합할 수 있습니다.

## <a name="http-methods"></a>HTTP 메서드

웹 API는 또한 요청의 HTTP 메서드 (GET, POST 등)를 기반으로 작업을 선택 합니다. 기본적으로 웹 API는 컨트롤러 메서드 이름의 시작과 함께 대/소문자를 구분 하지 않는 일치 항목을 찾습니다. 예를 들어 `PutCustomers` 라는 컨트롤러 메서드는 HTTP PUT 요청과 일치 합니다.

메서드를 다음 특성으로 데코레이팅 하 여이 규칙을 재정의할 수 있습니다.

- **HttpDelete**
- **[HttpGet]**
- **[HttpHead]**
- **[HttpOptions]**
- **[HttpPatch]**
- **HttpPost**
- **HttpPut**

다음 예제에서는 CreateBook 메서드를 HTTP POST 요청에 매핑합니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

비표준 메서드를 비롯 한 다른 모든 HTTP 메서드의 경우 HTTP 메서드 목록을 사용 하는 **Acceptverbs** 특성을 사용 합니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a>경로 접두사

컨트롤러의 경로는 모두 동일한 접두사로 시작 하는 경우가 많습니다. 다음은 그 예입니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

**[RoutePrefix]** 특성을 사용 하 여 전체 컨트롤러에 대 한 공통 접두사를 설정할 수 있습니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

메서드 특성에 물결표 (~)를 사용 하 여 경로 접두사를 재정의 합니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

경로 접두사는 매개 변수를 포함할 수 있습니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a>경로 제약 조건

경로 제약 조건을 사용 하면 경로 템플릿의 매개 변수가 일치 하는 방식을 제한할 수 있습니다. 일반적인 구문은 &quot;{parameter: constraint}&quot;입니다. 다음은 그 예입니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

여기서 첫 번째 경로는 URI의 &quot;id&quot; 세그먼트가 정수인 경우에만 선택 됩니다. 그렇지 않으면 두 번째 경로가 선택 됩니다.

다음 표에서는 지원 되는 제약 조건을 보여 줍니다.

| 제약 조건 | Description | 예제 |
| --- | --- | --- |
| 알파 | 대문자 또는 소문자 라틴 알파벳 문자 (a-z, a-z)를 찾습니다. | {x:alpha} |
| bool | 부울 값을 찾습니다. | {x:bool} |
| Datetime | **DateTime** 값과 일치 합니다. | {x:datetime} |
| decimal | 10 진수 값을 찾습니다. | {x:decimal} |
| double | 64 비트 부동 소수점 값을 찾습니다. | {x:double} |
| float | 32 비트 부동 소수점 값을 찾습니다. | {x:float} |
| guid | GUID 값과 일치 합니다. | {x:guid} |
| int | 32 비트 정수 값을 검색 합니다. | {x:int} |
| length | 지정 된 길이 또는 지정 된 길이 범위 내에서 문자열을 찾습니다. | {x:length(6)} {x:length(1,20)} |
| long | 64 비트 정수 값을 검색 합니다. | {x:long} |
| max | 최대값과 정수를 일치 시킵니다. | {x:max(10)} |
| maxlength | 최대 길이가 인 문자열을 찾습니다. | {x:maxlength(10)} |
| min | 최소값을 가진 정수를 찾습니다. | {x:min(10)} |
| minlength | 최소 길이가 인 문자열을 찾습니다. | {x:minlength(10)} |
| range | 값 범위 내에서 정수를 찾습니다. | {x:range(10,50)} |
| regex | 정규식과 일치 합니다. | {x:regex (^ \d{3}-\d{3}-\d{4}$)} |

&quot;min&quot;와 같은 일부 제약 조건은 괄호 안에 인수를 사용 합니다. 콜론으로 구분 된 매개 변수에 여러 제약 조건을 적용할 수 있습니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a>사용자 지정 경로 제약 조건

**IHttpRouteConstraint** 인터페이스를 구현 하 여 사용자 지정 경로 제약 조건을 만들 수 있습니다. 예를 들어 다음 제약 조건은 매개 변수를 0이 아닌 정수 값으로 제한 합니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

다음 코드에서는 제약 조건을 등록 하는 방법을 보여 줍니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

이제 경로에 제약 조건을 적용할 수 있습니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

**IInlineConstraintResolver** 인터페이스를 구현 하 여 전체 **DefaultInlineConstraintResolver** 클래스를 대체할 수도 있습니다. 이렇게 하면 **IInlineConstraintResolver** 구현에서 특별히 추가 하지 않는 한 기본 제공 제약 조건이 모두 바뀝니다.

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a>선택적 URI 매개 변수 및 기본값

경로 매개 변수에 물음표를 추가 하 여 URI 매개 변수를 선택적으로 만들 수 있습니다. 경로 매개 변수가 선택 사항인 경우에는 메서드 매개 변수의 기본값을 정의 해야 합니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

이 예제에서 `/api/books/locale/1033` 및 `/api/books/locale`는 동일한 리소스를 반환 합니다.

또는 다음과 같이 경로 템플릿 내에 기본값을 지정할 수 있습니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

이는 이전 예제와 거의 동일 하지만 기본값이 적용 될 때 동작의 약간 차이가 있습니다.

- 첫 번째 예제 ("{lcid: int?}")에서 1033의 기본값은 메서드 매개 변수에 직접 할당 되므로 매개 변수의 값이 정확 하 게 지정 됩니다.
- 두 번째 예 ("{lcid: int = 1033}")에서 "1033"의 기본값은 모델 바인딩 프로세스를 거칩니다. 기본 모델 바인더는 "1033"을 숫자 값 1033로 변환 합니다. 그러나 다른 작업을 수행 하는 사용자 지정 모델 바인더를 연결할 수도 있습니다.

파이프라인에 사용자 지정 모델 바인더를 포함 하지 않는 한 대부분의 경우 두 가지 형태는 동일 합니다.

<a id="route-names"></a>
## <a name="route-names"></a>경로 이름

Web API에서 모든 경로에는 이름이 있습니다. 경로 이름은 링크를 생성 하는 데 유용 하므로 HTTP 응답에 링크를 포함할 수 있습니다.

경로 이름을 지정 하려면 특성의 **이름** 속성을 설정 합니다. 다음 예에서는 경로 이름을 설정 하는 방법과 링크를 생성할 때 경로 이름을 사용 하는 방법을 보여 줍니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a>경로 순서

프레임 워크는 URI를 경로와 일치 시 키 려 고 할 때 특정 순서로 경로를 평가 합니다. 순서를 지정 하려면 경로 특성에서 **order** 속성을 설정 합니다. 낮은 값이 먼저 계산 됩니다. 기본 순서 값은 0입니다.

다음은 전체 순서가 결정 되는 방법입니다.

1. 경로 특성의 **Order** 속성을 비교 합니다.
2. 경로 템플릿에서 각 URI 세그먼트를 확인 합니다. 각 세그먼트에 대해 다음과 같이 정렬 합니다.

    1. 리터럴 세그먼트.
    2. 제약 조건이 포함 된 경로 매개 변수입니다.
    3. 제약 조건이 없는 경로 매개 변수입니다.
    4. 제약 조건이 있는 와일드 카드 매개 변수 세그먼트입니다.
    5. 제약 조건이 없는 와일드 카드 매개 변수 세그먼트입니다.
3. 연결의 경우 경로는 대/소문자를 구분 하지 않는 경로 템플릿의[stringcomparison.ordinalignorecase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)(서 수 문자열 비교)를 기준으로 정렬 됩니다.

다음 예를 참조하세요. 다음 컨트롤러를 정의 한다고 가정 합니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

이러한 경로는 다음과 같이 정렬 됩니다.

1. 주문/세부 정보
2. orders/{id}
3. orders/{customerName}
4. orders/{\*date}
5. orders/pending

"Details"는 리터럴 세그먼트 이며 "{id}" 앞에 나타나지만 **Order** 속성은 1 이기 때문에 "보류 중"으로 표시 됩니다. 이 예에서는 "details" 또는 "pending" 이라는 고객이 없는 것으로 가정 합니다. 일반적으로 모호한 경로를 방지 하십시오. 이 예제에서 `GetByCustomer`에 대 한 더 나은 경로 템플릿은 "customers/{customerName}"입니다.
