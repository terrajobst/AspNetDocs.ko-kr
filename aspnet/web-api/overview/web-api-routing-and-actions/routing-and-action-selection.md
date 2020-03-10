---
uid: web-api/overview/web-api-routing-and-actions/routing-and-action-selection
title: ASP.NET Web API에서 라우팅 및 작업 선택 Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 12/14/2018
ms.assetid: bcf2d223-cb7f-411e-be05-f43e96a14015
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-and-action-selection
msc.type: authoredcontent
ms.openlocfilehash: 62114e56fb29e80c93b82dcb78ce2bc2a123a83b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446915"
---
# <a name="routing-and-action-selection-in-aspnet-web-api"></a>ASP.NET Web API에서 라우팅 및 작업 선택

[Mike Wasson](https://github.com/MikeWasson)

이 문서에서는 ASP.NET Web API는 컨트롤러의 특정 작업에 HTTP 요청을 라우팅하는 방법을 설명 합니다.

> [!NOTE]
> 라우팅에 대 한 개략적인 개요는 [ASP.NET Web API에서 라우팅](routing-in-aspnet-web-api.md)을 참조 하세요.

이 문서에서는 라우팅 프로세스에 대 한 세부 정보를 살펴봅니다. Web API 프로젝트를 만들고 일부 요청이 원하는 방식으로 라우팅되지 않는 경우이 문서를 통해 도움을 받을 수 있습니다.

라우팅에는 세 가지 주요 단계가 있습니다.

1. 경로 템플릿에 대 한 URI 일치
2. 컨트롤러 선택
3. 작업을 선택 합니다.

프로세스의 일부를 사용자 지정 동작으로 바꿀 수 있습니다. 이 문서에서는 기본 동작을 설명 합니다. 마지막으로 동작을 사용자 지정할 수 있는 위치를 확인 합니다.

## <a name="route-templates"></a>경로 템플릿

경로 템플릿은 URI 경로와 비슷하지만 중괄호를 사용 하 여 표시 되는 자리 표시자 값이 있을 수 있습니다.

[!code-csharp[Main](routing-and-action-selection/samples/sample1.ps1)]

경로를 만들 때 일부 또는 모든 자리 표시자에 대 한 기본값을 제공할 수 있습니다.

[!code-csharp[Main](routing-and-action-selection/samples/sample2.cs)]

또한 URI 세그먼트가 자리 표시자와 일치 하는 방법을 제한 하는 제약 조건을 제공할 수 있습니다.

[!code-csharp[Main](routing-and-action-selection/samples/sample3.js)]

프레임 워크는 URI 경로의 세그먼트를 템플릿에 일치 시 키 려 고 시도 합니다. 템플릿의 리터럴은 정확히 일치 해야 합니다. 제약 조건을 지정 하지 않으면 자리 표시자는 모든 값과 일치 합니다. 프레임 워크가 호스트 이름 또는 쿼리 매개 변수와 같은 URI의 다른 부분과 일치 하지 않습니다. 프레임 워크는 경로 테이블에서 URI와 일치 하는 첫 번째 경로를 선택 합니다.

"{Controller}" 및 "{action}" 이라는 두 가지 특수 한 자리 표시 자가 있습니다.

- "{controller}"는 컨트롤러의 이름을 제공 합니다.
- "{action}"은 (는) 동작 이름을 제공 합니다. Web API에서 일반적인 규칙은 "{action}"을 생략 하는 것입니다.

### <a name="defaults"></a>기본값

기본값을 제공 하는 경우 경로는 해당 세그먼트가 없는 URI와 일치 합니다. 다음은 그 예입니다.

[!code-csharp[Main](routing-and-action-selection/samples/sample4.cs)]

Uri `http://localhost/api/products/all` 이전 경로와 일치 `http://localhost/api/products`. 후자 URI에서 누락 된 `{category}` 세그먼트에는 `all`기본값이 할당 됩니다.

### <a name="route-dictionary"></a>경로 사전

프레임 워크가 URI에 대해 일치 하는 항목을 찾으면 각 자리 표시자에 대 한 값을 포함 하는 사전을 만듭니다. 키는 중괄호를 포함 하지 않는 자리 표시자 이름입니다. 값은 URI 경로 또는 기본값에서 가져옵니다. 사전은 **IHttpRouteData** 개체에 저장 됩니다.

이 경로 일치 단계에서 특수 한 "{controller}" 및 "{action}" 자리 표시자는 다른 자리 표시자와 동일 하 게 처리 됩니다. 단지 다른 값을 사용 하 여 사전에 저장 됩니다.

기본값은 RouteParameter 특수 값을 가질 수 있습니다 **.** 자리 표시자에이 값이 할당 되 면 해당 값은 경로 사전에 추가 되지 않습니다. 다음은 그 예입니다.

[!code-csharp[Main](routing-and-action-selection/samples/sample5.cs)]

URI 경로 "api/products"의 경우 경로 사전에는 다음이 포함 됩니다.

- 컨트롤러: "제품"
- 범주: "all"

그러나 "api/products/장난감/123"의 경우 경로 사전에는 다음이 포함 됩니다.

- 컨트롤러: "제품"
- 범주: "장난감"
- id: "123"

기본값에는 경로 템플릿의 아무 곳에도 나타나지 않는 값이 포함 될 수 있습니다. 경로가 일치 하는 경우 해당 값이 사전에 저장 됩니다. 다음은 그 예입니다.

[!code-csharp[Main](routing-and-action-selection/samples/sample6.cs)]

URI 경로가 "api/root/8" 이면 사전에는 다음 두 값이 포함 됩니다.

- 컨트롤러: "고객"
- id: "8"

## <a name="selecting-a-controller"></a>컨트롤러 선택

컨트롤러 선택은 **IHttpControllerSelector 컨트롤러** 메서드에서 처리 됩니다. 이 메서드는 **HttpRequestMessage** 인스턴스를 사용 하 여 **httpcontrollerdescriptor**를 반환 합니다. 기본 구현은 **DefaultHttpControllerSelector** 클래스에서 제공 됩니다. 이 클래스는 간단한 알고리즘을 사용 합니다.

1. "컨트롤러" 키에 대 한 경로 사전을 찾습니다.
2. 이 키의 값을 가져와 "Controller" 문자열을 추가 하 여 컨트롤러 유형 이름을 가져옵니다.
3. 이 형식 이름을 사용 하 여 Web API 컨트롤러를 찾습니다.

예를 들어 경로 사전에 키-값 쌍 "controller" = "products"가 포함 되어 있으면 컨트롤러 유형은 "ProductsController"입니다. 일치 하는 형식 또는 여러 일치 항목이 없는 경우 프레임 워크는 클라이언트에 오류를 반환 합니다.

3 단계에서 **DefaultHttpControllerSelector** 는 **IHttpControllerTypeResolver** 인터페이스를 사용 하 여 Web API 컨트롤러 유형 목록을 가져옵니다. **IHttpControllerTypeResolver** 의 기본 구현에서는 (a) **IHttpController**를 구현 하는 모든 public 클래스 (b)가 abstract가 아니고 (c)에 "Controller"로 끝나는 모든 public 클래스를 반환 합니다.

## <a name="action-selection"></a>작업 선택

컨트롤러를 선택한 후 프레임 워크는 **IHttpActionSelector 작업** 메서드를 호출 하 여 작업을 선택 합니다. 이 메서드는 **Httpcontrollercontext** 를 사용 하 고 **httpcontrollercontext**를 반환 합니다.

기본 구현은 **ApiControllerActionSelector** 클래스에서 제공 됩니다. 작업을 선택 하려면 다음을 확인 합니다.

- 요청의 HTTP 메서드입니다.
- 경로 템플릿의 "{action}" 자리 표시자 (있는 경우)입니다.
- 컨트롤러에 대 한 작업의 매개 변수입니다.

선택 알고리즘을 확인 하기 전에 컨트롤러 작업에 대 한 몇 가지 사항을 이해 해야 합니다.

**"작업"으로 간주 되는 컨트롤러의 메서드는 무엇입니까?** 작업을 선택 하는 경우 프레임 워크는 컨트롤러의 공용 인스턴스 메서드만 찾습니다. 또한 ["특수 이름"](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname) 메서드 (생성자, 이벤트, 연산자 오버 로드 등) 및 **ApiController** 클래스에서 상속 된 메서드를 제외 합니다.

**HTTP 메서드.** 프레임 워크는 요청의 HTTP 메서드와 일치 하는 동작만 선택 하 고 다음과 같이 결정 됩니다.

1. 특성을 사용 하 여 HTTP 메서드 ( **Acceptverbs**, **httpdelete**, **HttpGet**, **httpdelete**, **Httpdelete**, **httpdelete**, **HttpPost**또는 **httpdelete**)를 지정할 수 있습니다.
2. 그렇지 않고 컨트롤러 메서드의 이름이 "Get", "Post", "Put", "Delete", "Head", "Options" 또는 "Patch"로 시작 하는 경우이 작업은 해당 HTTP 메서드를 지원 합니다.
3. 위의 항목이 없으면 메서드는 POST를 지원 합니다.

**매개 변수 바인딩입니다.** 매개 변수 바인딩은 Web API가 매개 변수 값을 만드는 방법입니다. 매개 변수 바인딩에 대 한 기본 규칙은 다음과 같습니다.

- 단순 형식은 URI에서 가져옵니다.
- 복합 형식은 요청 본문에서 가져옵니다.

단순 형식에는 모든 [.NET Framework 기본 형식](https://msdn.microsoft.com/library/system.type.isprimitive)및 **DateTime**, **Decimal**, **Guid**, **String**및 **TimeSpan**이 포함 됩니다. 각 작업에 대해 최대 하나의 매개 변수는 요청 본문을 읽을 수 있습니다.

> [!NOTE]
> 기본 바인딩 규칙을 재정의할 수 있습니다. [WebAPI 매개 변수 바인딩은 내부적으로](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)참조 하세요.

이 배경에서 작업 선택 알고리즘은 다음과 같습니다.

1. 컨트롤러에서 HTTP 요청 메서드와 일치 하는 모든 작업의 목록을 만듭니다.
2. 경로 사전에 "action" 항목이 있는 경우 이름이이 값과 일치 하지 않는 작업을 제거 합니다.
3. 다음과 같이 작업 매개 변수를 URI에 일치 시 키 려 고 합니다. 

    1. 각 작업에 대해 단순 형식인 매개 변수 목록을 가져옵니다. 여기서 바인딩은 URI에서 매개 변수를 가져옵니다. 선택적 매개 변수를 제외 합니다.
    2. 이 목록에서 경로 사전 또는 URI 쿼리 문자열에서 각 매개 변수 이름에 대 한 일치 항목 찾기를 시도 합니다. 일치는 대/소문자를 구분 하지 않으며 매개 변수 순서에 따라 달라 집니다.
    3. 목록의 모든 매개 변수가 URI에서 일치 하는 항목을 포함 하는 작업을 선택 합니다.
    4. 하나 이상의 작업이 이러한 조건을 충족 하는 경우 가장 많은 매개 변수 일치 항목을 사용 하 여 하나를 선택 합니다.
4. **[Nonaction]** 특성이 있는 동작을 무시 합니다.

#3 단계가 가장 혼란 스 러 울 수 있습니다. 기본 개념은 매개 변수가 URI, 요청 본문 또는 사용자 지정 바인딩에서 해당 값을 가져올 수 있다는 것입니다. URI에서 제공 되는 매개 변수의 경우 URI에 실제로 경로 (경로 사전) 또는 쿼리 문자열의 해당 매개 변수에 대 한 값이 포함 되어 있는지 확인 하려고 합니다.

예를 들어 다음 작업을 고려 하십시오.

[!code-csharp[Main](routing-and-action-selection/samples/sample7.cs)]

*Id* 매개 변수는 URI에 바인딩됩니다. 따라서이 작업은 경로 사전 또는 쿼리 문자열에 "id"의 값을 포함 하는 URI만 일치 시킬 수 있습니다.

선택적 매개 변수는 선택 사항 이므로 예외입니다. 선택적 매개 변수의 경우 바인딩이 URI에서 값을 가져올 수 없는 경우 정상입니다.

복합 형식은 다른 이유로 인 한 예외입니다. 복합 형식은 사용자 지정 바인딩을 통해 URI에만 바인딩할 수 있습니다. 그러나이 경우 프레임 워크는 매개 변수가 특정 URI에 바인딩 되었는지 여부를 미리 알 수 없습니다. 이를 확인 하려면 바인딩을 호출 해야 합니다. 선택 알고리즘의 목표는 바인딩을 호출 하기 전에 정적 설명에서 작업을 선택 하는 것입니다. 따라서 복합 형식은 일치 알고리즘에서 제외 됩니다.

동작을 선택 하면 모든 매개 변수 바인딩이 호출 됩니다.

요약:

- 작업은 요청의 HTTP 메서드와 일치 해야 합니다.
- 작업 이름은 경로 사전의 "action" 항목과 일치 해야 합니다 (있는 경우).
- 작업의 모든 매개 변수에 대해 매개 변수를 URI에서 가져온 경우 매개 변수 이름은 경로 사전 또는 URI 쿼리 문자열에서 찾아야 합니다. 복합 형식을 사용 하는 선택적 매개 변수 및 매개 변수는 제외 됩니다.
- 가장 많은 수의 매개 변수를 일치 시 키 려 고 합니다. 가장 일치 하는 항목은 매개 변수가 없는 메서드 일 수 있습니다.

## <a name="extended-example"></a>확장 된 예제

라우트에

[!code-csharp[Main](routing-and-action-selection/samples/sample8.cs)]

컨트롤러:

[!code-csharp[Main](routing-and-action-selection/samples/sample9.cs)]

HTTP 요청:

[!code-console[Main](routing-and-action-selection/samples/sample10.cmd)]

### <a name="route-matching"></a>경로 일치

URI는 이름이 "DefaultApi" 인 경로와 일치 합니다. 경로 사전에는 다음 항목이 포함 됩니다.

- 컨트롤러: "제품"
- id: "1"

경로 사전에 쿼리 문자열 매개 변수 "version" 및 "details"가 포함 되어 있지 않지만 작업을 선택 하는 동안에는이 매개 변수를 계속 고려 합니다.

### <a name="controller-selection"></a>컨트롤러 선택

경로 사전의 "컨트롤러" 항목에서 컨트롤러 유형이 `ProductsController`입니다.

### <a name="action-selection"></a>작업 선택

HTTP 요청은 GET 요청입니다. GET을 지 원하는 컨트롤러 작업은 `GetAll`, `GetById`및 `FindProductsByName`입니다. 경로 사전이 "action"에 대 한 항목을 포함 하지 않으므로 작업 이름과 일치 하지 않아도 됩니다.

다음으로 작업에 대 한 매개 변수 이름을 일치 시키고 GET 동작만 검색 하려고 합니다.

| 작업 | 일치 시킬 매개 변수 |
| --- | --- |
| `GetAll` | none |
| `GetById` | "id" |
| `FindProductsByName` | 이름의 |

`GetById`의 *version* 매개 변수는 선택적 매개 변수 이기 때문에 고려 되지 않습니다.

`GetAll` 메서드는 일반적으로와 일치 합니다. 경로 사전이 "id"를 포함 하기 때문에 `GetById` 메서드도 일치 합니다. `FindProductsByName` 메서드가와 일치 하지 않습니다.

`GetById` 메서드는 `GetAll`에 대 한 매개 변수 및 매개 변수는 일치 하지 않으므로 적용 됩니다. 메서드는 다음 매개 변수 값을 사용 하 여 호출 됩니다.

- *id* = 1
- *버전* = 1.5

선택 알고리즘에서 *버전* 을 사용 하지 않은 경우에도 매개 변수 값은 URI 쿼리 문자열에서 가져옵니다.

## <a name="extension-points"></a>확장점

Web API는 라우팅 프로세스의 일부에 대 한 확장 위치를 제공 합니다.

| 인터페이스 | Description |
| --- | --- |
| **IHttpControllerSelector** | 컨트롤러를 선택 합니다. |
| **IHttpControllerTypeResolver** | 컨트롤러 유형 목록을 가져옵니다. **DefaultHttpControllerSelector** 는이 목록에서 컨트롤러 유형을 선택 합니다. |
| **IAssembliesResolver** | 프로젝트 어셈블리의 목록을 가져옵니다. **IHttpControllerTypeResolver** 인터페이스는이 목록을 사용 하 여 컨트롤러 유형을 찾습니다. |
| **IHttpControllerActivator** | 새 컨트롤러 인스턴스를 만듭니다. |
| **IHttpActionSelector** | 작업을 선택합니다. |
| **IHttpActionInvoker** | 동작을 호출 합니다. |

이러한 인터페이스에 대 한 고유한 구현을 제공 하려면 **Httpconfiguration** 개체에서 **서비스** 컬렉션을 사용 합니다.

[!code-csharp[Main](routing-and-action-selection/samples/sample11.cs)]
