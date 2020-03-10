---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
title: ASP.NET Web API 2에서 OData 작업 지원 | Microsoft Docs
author: MikeWasson
description: OData에서 작업은 엔터티에 대 한 CRUD 작업으로 쉽게 정의 되지 않는 서버 쪽 동작을 추가 하는 방법입니다. 작업에는 다음이 포함 됩니다. 구현 ...
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 2d7b3aa2-aa47-4e6e-b0ce-3d65a1c6fe02
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
msc.type: authoredcontent
ms.openlocfilehash: ae8b23f0868f992cb2bbbf14ee3f7ac848501515
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448175"
---
# <a name="supporting-odata-actions-in-aspnet-web-api-2"></a>ASP.NET Web API 2에서 OData 작업 지원

[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> OData에서 *작업* 은 엔터티에 대 한 CRUD 작업으로 쉽게 정의 되지 않는 서버 쪽 동작을 추가 하는 방법입니다. 작업에는 다음이 포함 됩니다.
> 
> - 복잡 한 트랜잭션 구현
> - 여러 엔터티를 한 번에 조작 합니다.
> - 엔터티의 특정 속성만 업데이트할 수 있습니다.
> - 엔터티에 정의 되지 않은 서버로 정보를 보내는 중입니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - Web API 2
> - OData 버전 3
> - Entity Framework 6

## <a name="example-rating-a-product"></a>예: 제품 등급 매기기

이 예에서는 사용자가 제품의 등급을 지정 하 고 각 제품의 평균 등급을 표시 하려고 합니다. 데이터베이스에서 제품에 키가 지정 된 등급의 목록을 저장 합니다.

다음은 Entity Framework의 등급을 나타내는 데 사용할 수 있는 모델입니다.

[!code-csharp[Main](odata-actions/samples/sample1.cs)]

그러나 클라이언트가 `ProductRating` 개체를 "등급" 컬렉션에 게시 하지 않도록 합니다. 기본적으로 등급은 Products 컬렉션과 연결 되며 클라이언트는 등급 값을 게시 하기만 하면 됩니다.

따라서 정상적인 CRUD 작업을 사용 하는 대신 클라이언트에서 제품에 대해 호출할 수 있는 작업을 정의 합니다. OData 용어에서 작업은 제품 엔터티에 *바인딩됩니다* .

>작업은 서버에 부작용이 있습니다. 이러한 이유로 HTTP POST 요청을 사용 하 여 호출 됩니다. 작업에는 서비스 메타 데이터에 설명 되어 있는 매개 변수 및 반환 형식이 있을 수 있습니다. 클라이언트는 요청 본문에 매개 변수를 보내고 서버는 응답 본문에 반환 값을 보냅니다. "등급 제품" 작업을 호출 하기 위해 클라이언트는 다음과 같은 URI에 게시물을 보냅니다.

[!code-console[Main](odata-actions/samples/sample2.cmd)]

POST 요청의 데이터는 단순히 제품 등급입니다.

[!code-console[Main](odata-actions/samples/sample3.cmd)]

## <a name="declare-the-action-in-the-entity-data-model"></a>엔터티 데이터 모델에서 작업을 선언 합니다.

Web API 구성에서 EDM (엔터티 데이터 모델)에 작업을 추가 합니다.

[!code-csharp[Main](odata-actions/samples/sample4.cs)]

이 코드는 제품 엔터티에서 수행할 수 있는 작업으로 "RateProduct"를 정의 합니다. 또한 동작이 "등급" 이라는 **int** 매개 변수를 사용 하 고 **정수** 값을 반환 한다는 것을 선언 합니다.

## <a name="add-the-action-to-the-controller"></a>컨트롤러에 작업 추가

"RateProduct" 작업은 제품 엔터티에 바인딩됩니다. 작업을 구현 하려면 `RateProduct` 라는 메서드를 Products 컨트롤러에 추가 합니다.

[!code-csharp[Main](odata-actions/samples/sample5.cs)]

메서드 이름이 EDM의 작업 이름과 일치 하는지 확인 합니다. 메서드에는 두 개의 매개 변수가 있습니다.

- *키*: 평가할 제품의 키입니다.
- *parameters*: 작업 매개 변수 값의 사전입니다.

기본 라우팅 규칙을 사용 하는 경우 키 매개 변수의 이름을 "key"로 지정 해야 합니다. 표시 된 것 처럼 **[Fromodatauri]** 특성도 포함 하는 것도 중요 합니다. 이 특성은 요청 URI에서 키를 구문 분석할 때 OData 구문 규칙을 사용 하도록 Web API에 지시 합니다.

*매개 변수* 사전을 사용 하 여 작업 매개 변수를 가져옵니다.

[!code-csharp[Main](odata-actions/samples/sample6.cs)]

클라이언트에서 동작 매개 변수를 올바른 형식으로 보내는 경우 **Modelstate. IsValid** 값이 true입니다. 이 경우 **ODataActionParameters** 사전을 사용 하 여 매개 변수 값을 가져올 수 있습니다. 이 예제에서 `RateProduct` 작업은 "등급" 이라는 단일 매개 변수를 사용 합니다.

## <a name="action-metadata"></a>작업 메타 데이터

서비스 메타 데이터를 보려면/odata/$metadata에 GET 요청을 보냅니다. 다음은 `RateProduct` 작업을 선언 하는 메타 데이터의 일부입니다.

[!code-xml[Main](odata-actions/samples/sample7.xml)]

**FunctionImport** 요소는 작업을 선언 합니다. 대부분의 필드는 별도의 설명이 필요 하지만 두 가지는 주의를 기울여야 합니다.

- **Isbindable** 가능은 최소한 시간 동안 대상 엔터티에서 작업을 호출할 수 있음을 의미 합니다.
- **IsAlwaysBindable** 은 대상 엔터티에서 항상 동작을 호출할 수 있음을 의미 합니다.

차이점은 일부 동작은 클라이언트에서 항상 사용할 수 있지만 다른 작업은 엔터티의 상태에 따라 달라질 수 있습니다. 예를 들어 "구매" 작업을 정의 한다고 가정 합니다. 재고에 있는 항목만 구매할 수 있습니다. 항목이 재고가 없으면 클라이언트에서 해당 작업을 호출할 수 없습니다.

EDM을 정의 하는 경우 **동작** 메서드는 항상 바인딩할 수 있는 작업을 만듭니다.

[!code-csharp[Main](odata-actions/samples/sample8.cs?highlight=1)]

이 항목의 뒷부분에서는 항상 바인딩할 수 있는 작업 ( *임시* 작업이 라고도 함)에 대해 설명 합니다.

## <a name="invoking-the-action"></a>작업 호출

이제 클라이언트가이 작업을 호출 하는 방법을 알아보겠습니다. 클라이언트에서 ID가 4 인 제품에 등급 2를 제공 하려고 한다고 가정 합니다. 요청 본문에 JSON 형식을 사용 하는 예제 요청 메시지는 다음과 같습니다.

[!code-console[Main](odata-actions/samples/sample9.cmd)]

응답 메시지는 다음과 같습니다.

[!code-console[Main](odata-actions/samples/sample10.cmd)]

## <a name="binding-an-action-to-an-entity-set"></a>작업을 엔터티 집합에 바인딩

이전 예제에서 작업은 단일 엔터티에 바인딩됩니다. 클라이언트는 단일 제품을 평가 합니다. 엔터티 컬렉션에 작업을 바인딩할 수도 있습니다. 다음과 같이 변경 합니다.

EDM에서 엔터티의 **컬렉션** 속성에 작업을 추가 합니다.

[!code-csharp[Main](odata-actions/samples/sample11.cs?highlight=1)]

Controller 메서드에서 *키* 매개 변수를 생략 합니다.

[!code-csharp[Main](odata-actions/samples/sample12.cs)]

이제 클라이언트가 Products 엔터티 집합에 대 한 작업을 호출 합니다.

[!code-console[Main](odata-actions/samples/sample13.cmd)]

## <a name="actions-with-collection-parameters"></a>컬렉션 매개 변수를 사용한 작업

작업에는 값 컬렉션을 사용 하는 매개 변수가 있을 수 있습니다. EDM에서 **collectionparameter&lt;t&gt;** 를 사용 하 여 매개 변수를 선언 합니다.

[!code-csharp[Main](odata-actions/samples/sample14.cs)]

이 매개 변수는 **int** 값의 컬렉션을 사용 하는 "등급" 이라는 매개 변수를 선언 합니다. Controller 메서드에서 **ODataActionParameters** 개체의 매개 변수 값을 가져오지만 이제 값은 **ICollection&lt;int&gt;** 값입니다.

[!code-csharp[Main](odata-actions/samples/sample15.cs)]

## <a name="transient-actions"></a>임시 작업

"RateProduct" 예제에서 사용자는 항상 제품의 등급을 지정할 수 있으므로 작업을 항상 사용할 수 있습니다. 하지만 일부 작업은 엔터티의 상태에 따라 달라 집니다. 예를 들어 비디오 임대 서비스에서는 "체크 아웃" 작업을 항상 사용할 수 있는 것은 아닙니다. 이는 해당 비디오의 복사본을 사용할 수 있는지 여부에 따라 달라 집니다. 이 동작 유형을 *일시적* 동작 이라고 합니다.

서비스 메타 데이터에서 일시적인 작업에는 **IsAlwaysBindable** 가 false와 같습니다. 이것은 실제로 기본값 이므로 메타 데이터는 다음과 같습니다.

[!code-xml[Main](odata-actions/samples/sample16.xml)]

이 문제가 발생 하는 이유는 다음과 같습니다. 동작이 일시적인 경우 서버에서 작업을 사용할 수 있을 때 클라이언트에 게 알려야 합니다. 엔터티의 작업에 대 한 링크를 포함 하 여이 작업을 수행 합니다. 동영상 엔터티에 대 한 예제는 다음과 같습니다.

[!code-console[Main](odata-actions/samples/sample17.cmd)]

"#CheckOut" 속성에는 체크 아웃 작업에 대 한 링크가 포함 되어 있습니다. 동작을 사용할 수 없는 경우 서버에서 해당 링크를 생략 합니다.

EDM에서 임시 작업을 선언 하려면 **TransientAction** 메서드를 호출 합니다.

[!code-csharp[Main](odata-actions/samples/sample18.cs)]

또한 지정 된 엔터티에 대 한 작업 링크를 반환 하는 함수를 제공 해야 합니다. **Hasactionlink**를 호출 하 여이 함수를 설정 합니다. 함수를 람다 식으로 작성할 수 있습니다.

[!code-csharp[Main](odata-actions/samples/sample19.cs)]

동작을 사용할 수 있는 경우 람다 식에서 작업에 대 한 링크를 반환 합니다. OData serializer는 엔터티를 직렬화 할 때이 링크를 포함 합니다. 동작을 사용할 수 없는 경우 함수는 `null`반환 합니다.

## <a name="additional-resources"></a>추가 리소스

[OData 작업 샘플](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v3/ODataActionsSample/)
