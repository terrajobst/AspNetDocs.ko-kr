---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-routing-conventions
title: ASP.NET Web API 2 Odata-ASP.NET 4.x의 라우팅 규칙
author: MikeWasson
description: ASP.NET 4.x의 Web API 2에서 OData 끝점에 사용 하는 라우팅 규칙을 설명 합니다.
ms.author: riande
ms.date: 07/31/2013
ms.custom: seoapril2019
ms.assetid: adbc175a-14eb-4ab2-a441-d056ffa8266f
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-routing-conventions
msc.type: authoredcontent
ms.openlocfilehash: 63df4a82cd8df92631485b2544117844cfd0ca56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498197"
---
# <a name="routing-conventions-in-aspnet-web-api-2-odata"></a>ASP.NET Web API 2 Odata의 라우팅 규칙

[Mike Wasson](https://github.com/MikeWasson)

> 이 문서에서는 ASP.NET 4.x의 Web API 2에서 OData 끝점에 대해 사용 하는 라우팅 규칙을 설명 합니다.

Web API는 OData 요청을 가져오는 경우 요청을 컨트롤러 이름 및 작업 이름에 매핑합니다. 매핑은 HTTP 메서드와 URI를 기반으로 합니다. 예를 들어 `GET /odata/Products(1)`는 `ProductsController.GetProduct`에 매핑됩니다.

이 문서의 1 부에서는 기본 제공 OData 라우팅 규칙에 대해 설명 합니다. 이러한 규칙은 OData 끝점을 위해 특별히 설계 되었으며 기본 Web API 라우팅 시스템을 대체 합니다. **MapODataRoute**를 호출할 때 대체가 발생 합니다.

2 부에서는 사용자 지정 라우팅 규칙을 추가 하는 방법을 보여 줍니다. 현재 기본 제공 규칙은 전체 범위의 OData Uri를 포함 하지 않지만 추가 사례를 처리 하도록 확장할 수 있습니다.

- [기본 제공 라우팅 규칙](#conventions)
- [사용자 지정 라우팅 규칙](#custom)

<a id="conventions"></a>
## <a name="built-in-routing-conventions"></a>기본 제공 라우팅 규칙

Web API의 OData 라우팅 규칙을 설명 하기 전에 OData Uri를 이해 하는 것이 좋습니다. [ODATA URI](http://www.odata.org/documentation/odata-v3-documentation/url-conventions/) 는 다음으로 구성 됩니다.

- 서비스 루트
- 리소스 경로
- 쿼리 옵션

![](odata-routing-conventions/_static/image1.png)

라우팅의 경우 중요 한 부분은 리소스 경로입니다. 리소스 경로는 세그먼트로 나뉩니다. 예를 들어 `/Products(1)/Supplier`에는 세 개의 세그먼트가 있습니다.

- `Products`는 "Products" 라는 엔터티 집합을 참조 합니다.
- `1`은 엔터티 키 이며 집합에서 단일 엔터티를 선택 합니다.
- `Supplier`는 관련 엔터티를 선택 하는 탐색 속성입니다.

따라서이 경로는 제품 1의 공급자를 선택 합니다.

> [!NOTE]
> OData 경로 세그먼트는 항상 URI 세그먼트와 일치 하지 않습니다. 예를 들어 "1"은 경로 세그먼트로 간주 됩니다.

**컨트롤러 이름입니다.** 컨트롤러 이름은 항상 리소스 경로의 루트에 있는 엔터티 집합에서 파생 됩니다. 예를 들어 리소스 경로가 `/Products(1)/Supplier`되는 경우 Web API는 `ProductsController`라는 컨트롤러를 찾습니다.

**작업 이름입니다.** 작업 이름은 다음 표에 나열 된 것과 같이 경로 세그먼트와 EDM (엔터티 데이터 모델)에서 파생 됩니다. 경우에 따라 작업 이름에 대 한 두 가지 옵션을 선택할 수 있습니다. 예를 들어, "Get" 또는 &quot;GetProducts&quot;합니다.

**엔터티 쿼리**

| 요청 | 예제 URI | 동작 이름 | 예제 작업 |
| --- | --- | --- | --- |
| GET/entityset | /Products | GetEntitySet 또는 Get | GetProducts |
| GET/entityset (키) | /제품 (1) | GetEntityType 또는 Get | GetProduct |
| /Entityset (key)/캐스트 가져오기 | /Products(1)/Models.Book | GetEntityType 또는 Get | GetBook |

자세한 내용은 [읽기 전용 OData 끝점 만들기](odata-v3/creating-an-odata-endpoint.md)를 참조 하세요.

**엔터티 만들기, 업데이트 및 삭제**

| 요청 | 예제 URI | 동작 이름 | 예제 작업 |
| --- | --- | --- | --- |
| POST/entityset | /Products | PostEntityType 또는 Post | PostProduct |
| PUT/entityset (key) | /제품 (1) | PutEntityType 또는 Put | PutProduct |
| /Entityset (key)/캐스트를 입력 합니다. | /Products(1)/Models.Book | PutEntityType 또는 Put | PutBook |
| PATCH/entityset (키) | /제품 (1) | PatchEntityType 또는 Patch | PatchProduct |
| PATCH/entityset (key)/캐스트 | /Products(1)/Models.Book | PatchEntityType 또는 Patch | PatchBook |
| DELETE/entityset (key) | /제품 (1) | DeleteEntityType 또는 Delete | DeleteProduct |
| /Entityset (key)/캐스트 삭제 | /Products(1)/Models.Book | DeleteEntityType 또는 Delete | DeleteBook |

**탐색 속성 쿼리**

| 요청 | 예제 URI | 동작 이름 | 예제 작업 |
| --- | --- | --- | --- |
| /Entityset (key)/탐색을 가져옵니다. | /제품 (1)/공급자 | GetNavigationFromEntityType 또는 Get탐색 | GetSupplierFromProduct |
| /Entityset (key)/cast/navigation 가져오기 | /Products(1)/Models.Book/Author | GetNavigationFromEntityType 또는 Get탐색 | GetAuthorFromBook |

자세한 내용은 [엔터티 관계 작업](odata-v3/working-with-entity-relations.md)을 참조 하세요.

**링크 만들기 및 삭제**

| 요청 | 예제 URI | 동작 이름 |
| --- | --- | --- |
| POST/entityset (key)/$links/탐색 | /Products(1)/$links/Supplier | CreateLink |
| PUT /entityset(key)/$links/navigation | /Products(1)/$links/Supplier | CreateLink |
| /Entityset (key)/$links/탐색을 삭제 합니다. | /Products(1)/$links/Supplier | DeleteLink |
| DELETE /entityset(key)/$links/navigation(relatedKey) | /Products/(1)/$links/Suppliers(1) | DeleteLink |

자세한 내용은 [엔터티 관계 작업](odata-v3/working-with-entity-relations.md)을 참조 하세요.

**속성**

*Web API 2 필요*

| 요청 | 예제 URI | 동작 이름 | 예제 작업 |
| --- | --- | --- | --- |
| /Entityset (key)/property 가져오기 | /Products(1)/Name | GetPropertyFromEntityType 또는 GetProperty | GetNameFromProduct |
| /Entityset (key)/cast/property 가져오기 | /Products(1)/Models.Book/Author | GetPropertyFromEntityType 또는 GetProperty | GetTitleFromBook |

**actions**

| 요청 | 예제 URI | 동작 이름 | 예제 작업 |
| --- | --- | --- | --- |
| POST/entityset (key)/action | /Products(1)/Rate | ActionNameOnEntityType 또는 ActionName | RateOnProduct |
| POST/entityset (key)/cast/action | /Products(1)/Models.Book/CheckOut | ActionNameOnEntityType 또는 ActionName | CheckOutOnBook |

자세한 내용은 [OData 작업](odata-v3/odata-actions.md)을 참조 하세요.

**메서드 시그니처**

다음은 메서드 시그니처에 대 한 몇 가지 규칙입니다.

- 경로에 키가 포함 된 경우 작업에는 *key*라는 매개 변수가 있어야 합니다.
- 경로에 탐색 속성에 대 한 키가 포함 된 경우 작업에는 *relatedKey*라는 매개 변수가 있어야 합니다.
- **[RelatedKey Modatauri]** 매개 변수를 사용 하 여 *키* 및 매개 변수를 장식 합니다.
- POST 및 PUT 요청은 엔터티 형식의 매개 변수를 사용 합니다.
- PATCH 요청은 **델타&lt;t&gt;** 형식의 매개 변수를 사용 합니다. 여기서 *t* 는 엔터티 형식입니다.

참조용으로, 모든 기본 제공 OData 라우팅 규칙에 대 한 메서드 시그니처를 보여 주는 예제는 다음과 같습니다.

[!code-csharp[Main](odata-routing-conventions/samples/sample1.cs)]

<a id="custom"></a>
## <a name="custom-routing-conventions"></a>사용자 지정 라우팅 규칙

현재 기본 제공 규칙은 가능한 모든 OData Uri를 포함 하지 않습니다. **IODataRoutingConvention** 인터페이스를 구현 하 여 새 규칙을 추가할 수 있습니다. 이 인터페이스에는 두 가지 방법이 있습니다.

[!code-csharp[Main](odata-routing-conventions/samples/sample2.cs)]

- **Selectcontroller** 는 컨트롤러의 이름을 반환 합니다.
- **Selectaction** 은 동작의 이름을 반환 합니다.

두 방법 모두 해당 요청에 규칙이 적용 되지 않는 경우이 메서드는 null을 반환 해야 합니다.

**ODataPath** 매개 변수는 구문 분석 된 OData 리소스 경로를 나타냅니다. 여기에는 리소스 경로의 각 세그먼트에 대해 하나씩 **[된 odatapathsegment](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatapathsegment.aspx)** 인스턴스 목록이 포함 됩니다. **된 odatapathsegment** 는 추상 클래스입니다. 각 세그먼트 형식은 **된 odatapathsegment**에서 파생 되는 클래스로 표현 됩니다.

**ODataPath epath** 속성은 모든 경로 세그먼트의 연결을 나타내는 문자열입니다. 예를 들어 URI가 `/Products(1)/Supplier`되는 경우 경로 템플릿은 &quot;~/entityset/key/탐색&quot;됩니다. 세그먼트가 URI 세그먼트와 직접 일치 하지 않습니다. 예를 들어 엔터티 키 (1)는 고유한 **된 odatapathsegment**로 표시 됩니다.

일반적으로 **IODataRoutingConvention** 구현에서는 다음을 수행 합니다.

1. 경로 템플릿을 비교 하 여이 규칙이 현재 요청에 적용 되는지 확인 합니다. 적용 되지 않으면 null을 반환 합니다.
2. 규칙이 적용 되는 경우 **된 odatapathsegment** 인스턴스의 속성을 사용 하 여 컨트롤러 및 작업 이름을 파생 합니다.
3. 작업의 경우 작업 매개 변수 (일반적으로 엔터티 키)에 바인딩할 경로 사전에 값을 추가 합니다.

특정 예제를 살펴보겠습니다. 기본 제공 라우팅 규칙은 탐색 컬렉션에 대 한 인덱싱을 지원 하지 않습니다. 즉, Uri에 대 한 규칙은 다음과 같습니다.

[!code-javascript[Main](odata-routing-conventions/samples/sample3.js)]

이 쿼리 유형을 처리 하는 사용자 지정 라우팅 규칙은 다음과 같습니다.

[!code-csharp[Main](odata-routing-conventions/samples/sample4.cs)]

참고:

1. 이 새로운 라우팅 규칙에 적절 한 클래스의 **Selectcontroller** 메서드가 있으므로 **EntitySetRoutingConvention**에서 파생 됩니다. 즉, **Selectcontroller**를 다시 구현할 필요가 없습니다.
2. 규칙은 GET 요청에만 적용 되 고 경로 템플릿이 &quot;~/entityset/hv/pv/key&quot;인 경우에만 적용 됩니다.
3. 작업 이름은 &quot;Get {EntityType}&quot;입니다. 여기서 *{entitytype}* 은 탐색 컬렉션의 유형입니다. 예를 들어 GetSupplier&quot;를 &quot;합니다. 컨트롤러 작업이 일치 하는지 확인 하는 것 처럼 &#8212; 모든 명명 규칙을 사용할 수 있습니다.
4. 작업은 *key* 및 *relatedKey*라는 두 개의 매개 변수를 사용 합니다. 미리 정의 된 매개 변수 이름 목록은 [ODataRouteConstants](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatarouteconstants.aspx)를 참조 하세요.

다음 단계는 라우팅 규칙의 목록에 새 규칙을 추가 하는 것입니다. 이는 다음 코드와 같이 구성 중에 발생 합니다.

[!code-csharp[Main](odata-routing-conventions/samples/sample5.cs)]

다음은 연구에 유용한 몇 가지 다른 샘플 라우팅 규칙입니다.

- [CompositeKeyRoutingConvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataCompositeKeySample/ODataCompositeKeySample/Extensions/CompositeKeyRoutingConvention.cs)
- [CustomNavigationRoutingConvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataServiceSample/ODataService/Extensions/CustomNavigationRoutingConvention.cs)
- [NonBindableActionRoutingConvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataActionsSample/ODataActionsSample/NonBindableActionRoutingConvention.cs)
- [ODataVersionRouteConstraint](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataVersioningSample/ODataVersioningSample/Extensions/ODataVersionRouteConstraint.cs)

물론 Web API 자체는 오픈 소스 이므로 기본 제공 라우팅 규칙에 대 한 [소스 코드](http://aspnetwebstack.codeplex.com/) 를 볼 수 있습니다. 이러한 **규칙은 system.web** . m a.
