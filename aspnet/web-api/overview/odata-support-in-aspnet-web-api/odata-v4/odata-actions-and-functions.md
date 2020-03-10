---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
title: ASP.NET Web API 2.2를 사용 하 여 OData v4의 동작 및 함수 | Microsoft Docs
author: MikeWasson
description: OData에서 작업 및 함수는 엔터티에 대 한 CRUD 작업으로 쉽게 정의 되지 않는 서버 쪽 동작을 추가 하는 방법입니다. 이 자습서에서는 다음 방법을 보여 줍니다.
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 0e6fb03c-b16d-4bb0-ab0b-552bd2b6ece1
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
msc.type: authoredcontent
ms.openlocfilehash: f5af94e93e5b7f2351d40febbf1a468d635c9db1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448061"
---
# <a name="actions-and-functions-in-odata-v4-using-aspnet-web-api-22"></a>ASP.NET Web API 2.2를 사용 하는 OData v4의 동작 및 함수

[Mike Wasson](https://github.com/MikeWasson)

> OData에서 작업 및 함수는 엔터티에 대 한 CRUD 작업으로 쉽게 정의 되지 않는 서버 쪽 동작을 추가 하는 방법입니다. 이 자습서에서는 Web API 2.2를 사용 하 여 OData v4 끝점에 작업 및 함수를 추가 하는 방법을 보여 줍니다. 자습서는 [ASP.NET Web API 2를 사용 하 여 OData V4 엔드포인트 만들기](create-an-odata-v4-endpoint.md) 자습서를 기반으로 합니다.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
>
> - 웹 API 2.2
> - OData v4
> - Visual Studio 2013 (Visual [Studio 2017 다운로드](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))
> - .NET 4.5
>
> ## <a name="tutorial-versions"></a>자습서 버전
>
> OData 버전 3의 경우 [ASP.NET Web API 2의 Odata 작업](../odata-v3/odata-actions.md)을 참조 하세요.

작업과 *함수의* 차이점 은 작업에 부작용이 있을 수 있다는 것 이며 함수는 그렇지 않습니다. 작업 및 함수는 모두 데이터를 반환할 수 있습니다. 작업에는 다음이 포함 됩니다.

- 복잡 한 트랜잭션.
- 여러 엔터티를 한 번에 조작 합니다.
- 엔터티의 특정 속성만 업데이트할 수 있습니다.
- 엔터티가 아닌 데이터를 보내는 중입니다.

함수는 엔터티 또는 컬렉션과 직접 일치 하지 않는 정보를 반환 하는 데 유용 합니다.

작업 (또는 함수)은 단일 엔터티 또는 컬렉션을 대상으로 할 수 있습니다. OData 용어에서이는 *바인딩입니다*. 서비스에서 정적 작업으로 호출 되는 &quot;바인딩되지 않은&quot; 작업/함수를 사용할 수도 있습니다.

## <a name="example-adding-an-action"></a>예: 작업 추가

제품을 평가 하는 작업을 정의 해 보겠습니다.

> [!NOTE]
> 이 자습서에서는 [ASP.NET Web API 2를 사용 하 여 OData V4 끝점 만들기](create-an-odata-v4-endpoint.md) 자습서를 기반으로 합니다.

먼저 등급을 나타내는 `ProductRating` 모델을 추가 합니다.

[!code-csharp[Main](odata-actions-and-functions/samples/sample1.cs)]

또한 EF가 데이터베이스에 등급 테이블을 만들 수 있도록 **Dbset** 을 `ProductsContext` 클래스에 추가 합니다.

[!code-csharp[Main](odata-actions-and-functions/samples/sample2.cs)]

### <a name="add-the-action-to-the-edm"></a>EDM에 작업 추가

WebApiConfig.cs에서 다음 코드를 추가 합니다.

[!code-csharp[Main](odata-actions-and-functions/samples/sample3.cs)]

**EntityTypeConfiguration** 메서드는 EDM (엔터티 데이터 모델)에 작업을 추가 합니다. **Parameter** 메서드는 동작에 대해 형식화 된 매개 변수를 지정 합니다.

또한이 코드는 EDM에 대 한 네임 스페이스를 설정 합니다. 네임 스페이스는 동작에 대 한 URI에 정규화 된 동작 이름이 포함 되기 때문에 중요 합니다.

[!code-console[Main](odata-actions-and-functions/samples/sample4.cmd)]

> [!NOTE]
> 일반적인 IIS 구성에서이 URL의 점은 IIS에서 404 오류를 반환 하는 원인이 됩니다. Web.config 파일에 다음 섹션을 추가 하 여이 문제를 해결할 수 있습니다.

[!code-xml[Main](odata-actions-and-functions/samples/sample5.xml)]

### <a name="add-a-controller-method-for-the-action"></a>작업에 대 한 컨트롤러 메서드 추가

&quot;Rate&quot; 작업을 사용 하도록 설정 하려면 다음 메서드를 `ProductsController`에 추가 합니다.

[!code-csharp[Main](odata-actions-and-functions/samples/sample6.cs)]

메서드 이름이 작업 이름과 일치 하는지 확인 합니다. **[HttpPost]** 특성은 메서드가 HTTP POST 메서드를 지정 합니다.

동작을 호출 하기 위해 클라이언트는 다음과 같은 HTTP POST 요청을 보냅니다.

[!code-console[Main](odata-actions-and-functions/samples/sample7.cmd)]

작업에 대 한 URI는 엔터티 URI에 추가 된 정규화 된 작업 이름 이므로 작업에 대 한 URI가 제품 인스턴스에 바인딩되어&quot; &quot;합니다. EDM 네임 스페이스를 &quot;제품 서비스&quot;로 설정 했으므로 정규화 된 작업 이름은 제품 서비스 &quot;입니다. Rate&quot;.

요청의 본문은 작업 매개 변수를 JSON 페이로드로 포함 합니다. Web API는 JSON 페이로드를 매개 변수 값의 사전 인 **ODataActionParameters** 개체로 자동으로 변환 합니다. 이 사전을 사용 하 여 컨트롤러 메서드의 매개 변수에 액세스 합니다.

클라이언트에서 동작 매개 변수를 잘못 된 형식으로 보내는 경우 **Modelstate. IsValid** 값은 false입니다. 컨트롤러 메서드에서이 플래그를 확인 하 고 **IsValid** 가 false 인 경우 오류를 반환 합니다.

[!code-csharp[Main](odata-actions-and-functions/samples/sample8.cs)]

## <a name="example-adding-a-function"></a>예: 함수 추가

이제 가장 비용이 많이 드는 제품을 반환 하는 OData 함수를 추가 해 보겠습니다. 이전 처럼 첫 번째 단계는 함수를 EDM에 추가 하는 것입니다. WebApiConfig.cs에서 다음 코드를 추가 합니다.

[!code-csharp[Main](odata-actions-and-functions/samples/sample9.cs)]

이 경우 함수는 개별 제품 인스턴스가 아닌 Products 컬렉션에 바인딩됩니다. 클라이언트는 GET 요청을 보내 함수를 호출 합니다.

[!code-console[Main](odata-actions-and-functions/samples/sample10.cmd)]

이 함수에 대 한 컨트롤러 메서드는 다음과 같습니다.

[!code-csharp[Main](odata-actions-and-functions/samples/sample11.cs)]

메서드 이름이 함수 이름과 일치 하는지 확인 합니다. **[HttpGet]** 특성은 메서드가 HTTP GET 메서드를 지정 합니다.

HTTP 응답은 다음과 같습니다.

[!code-console[Main](odata-actions-and-functions/samples/sample12.cmd)]

## <a name="example-adding-an-unbound-function"></a>예제: 바인딩되지 않은 함수 추가

이전 예제는 컬렉션에 바인딩된 함수 였습니다. 다음 예제에서는 *바인딩되지* 않은 함수를 만듭니다. 바인딩되지 않은 함수는 서비스에서 정적 작업으로 호출 됩니다. 이 예제의 함수는 지정 된 우편 번호에 대 한 판매 세율을 반환 합니다.

WebApiConfig 파일에서 함수를 EDM에 추가 합니다.

[!code-csharp[Main](odata-actions-and-functions/samples/sample13.cs)]

엔터티 형식 또는 컬렉션이 아닌 **만드는**에서 직접 **함수** 를 호출 하 고 있습니다. 이렇게 하면 함수가 바인딩되지 않음을 모델 작성기에 알려 줍니다.

함수를 구현 하는 컨트롤러 메서드는 다음과 같습니다.

[!code-csharp[Main](odata-actions-and-functions/samples/sample14.cs)]

이 메서드를 배치한 웹 API 컨트롤러에는 중요 하지 않습니다. `ProductsController`에 추가 하거나 별도의 컨트롤러를 정의할 수 있습니다. **[ODataRoute]** 특성은 함수에 대 한 URI 템플릿을 정의 합니다.

클라이언트 요청 예제는 다음과 같습니다.

[!code-console[Main](odata-actions-and-functions/samples/sample15.cmd)]

HTTP 응답:

[!code-console[Main](odata-actions-and-functions/samples/sample16.cmd)]
