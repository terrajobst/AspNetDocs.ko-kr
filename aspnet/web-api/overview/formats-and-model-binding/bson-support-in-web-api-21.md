---
uid: web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
title: ASP.NET Web API 2.1에서 BSON 지원-ASP.NET 4.x
author: MikeWasson
description: ASP.NET 4.x 용 .NET 클라이언트 앱과 Web API 컨트롤러 (서버 쪽)에서 BSON을 사용 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: ce11b017-0ca6-4376-aa9d-a7f3288101de
msc.legacyurl: /web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
msc.type: authoredcontent
ms.openlocfilehash: ccbc0372120301b1cd8d4cdc86bd9fba9404d8ae
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519334"
---
# <a name="bson-support-in-aspnet-web-api-21"></a>ASP.NET Web API 2.1에서 BSON 지원

[Mike Wasson](https://github.com/MikeWasson)

이 항목에서는 Web API 컨트롤러 (서버 쪽) 및 .NET 클라이언트 앱에서 BSON을 사용 하는 방법을 보여 줍니다. Web API 2.1는 BSON을 지원 합니다. 

## <a name="what-is-bson"></a>BSON 이란?

[Bson](http://bsonspec.org/) 은 이진 serialization 형식입니다. "BSON"은 "이진 JSON"을 나타내지만 BSON 및 JSON은 매우 다르게 직렬화 됩니다. BSON은 JSON과 유사 하 게 이름-값 쌍으로 표현 되기 때문에 "JSON과 유사 합니다."입니다. JSON과 달리 숫자 데이터 형식은 문자열이 아닌 바이트로 저장 됩니다.

BSON은 간단 하 고 쉽게 검색할 수 있도록 설계 되었으며 인코드/디코드 속도가 빠릅니다.

- BSON은 JSON의 크기와 비교할 수 있습니다. 데이터에 따라, BSON 페이로드는 JSON 페이로드보다 작거나 클 수 있습니다. 이미지 파일 등의 이진 데이터를 serialize 하는 경우에는 이진 데이터가 b a s e 64로 인코딩되지 않으므로 BSON은 JSON 보다 작습니다.
- 요소에 길이 필드가 접두사로 사용 되므로 BSON 문서를 쉽게 검색할 수 있으므로 파서는 요소를 디코딩하지 않고 건너뛸 수 있습니다.
- 숫자 데이터 형식은 문자열이 아닌 숫자로 저장 되기 때문에 인코딩과 디코딩을 효율적입니다.

.NET 클라이언트 앱과 같은 네이티브 클라이언트는 JSON 또는 XML과 같은 텍스트 기반 형식 대신 BSON을 사용 하 여 이점을 누릴 수 있습니다. JavaScript가 JSON 페이로드를 직접 변환할 수 있으므로 browser 클라이언트의 경우 JSON을 사용 하는 것이 좋습니다.

다행히 웹 API는 [콘텐츠 협상](content-negotiation.md)을 사용 하므로 api에서 두 형식을 모두 지원 하 고 클라이언트에서 선택 하도록 할 수 있습니다.

## <a name="enabling-bson-on-the-server"></a>서버에서 BSON 사용

Web API 구성에서 포맷터 컬렉션에 **BsonMediaTypeFormatter** 를 추가 합니다.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample1.cs)]

이제 클라이언트가 "application/bson"을 요청 하면 Web API는 BSON 포맷터를 사용 합니다.

BSON을 다른 미디어 유형과 연결 하려면 SupportedMediaTypes 컬렉션에 추가 합니다. 다음 코드에서는 지원 되는 미디어 형식에 "application/vnd. contoso"를 추가 합니다.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample2.cs)]

## <a name="example-http-session"></a>예제 HTTP 세션

이 예제에서는 다음 모델 클래스와 간단한 Web API 컨트롤러를 사용 합니다.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample3.cs)]

클라이언트는 다음 HTTP 요청을 보낼 수 있습니다.

[!code-console[Main](bson-support-in-web-api-21/samples/sample4.cmd)]

응답은 다음과 같습니다.

[!code-console[Main](bson-support-in-web-api-21/samples/sample5.cmd)]

여기서는 이진 데이터를 &quot;로 바꿨습니다.&quot; 문자. Fiddler의 다음 스크린샷은 원시 16 진수 값을 보여 줍니다.

[![](bson-support-in-web-api-21/_static/image2.png)](bson-support-in-web-api-21/_static/image1.png)

## <a name="using-bson-with-httpclient"></a>HttpClient에서 BSON 사용

.NET 클라이언트 앱은 **Httpclient**에서 bson 포맷터를 사용할 수 있습니다. **Httpclient**에 대 한 자세한 내용은 [.Net 클라이언트에서 Web API 호출](../advanced/calling-a-web-api-from-a-net-client.md)을 참조 하십시오.

다음 코드는 BSON을 수락 하는 GET 요청을 보낸 다음 응답에서 BSON 페이로드를 deserialize 합니다.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample6.cs)]

서버에서 BSON을 요청 하려면 Accept 헤더를 "application/bson"으로 설정 합니다.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample7.cs)]

응답 본문을 deserialize 하려면 **BsonMediaTypeFormatter**을 사용 합니다. 이 포맷터는 기본 포맷터 컬렉션에 없으므로 응답 본문을 읽을 때 해당 포맷터를 지정 해야 합니다.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample8.cs)]

다음 예제에서는 BSON이 포함 된 POST 요청을 보내는 방법을 보여 줍니다.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample9.cs)]

이 코드의 대부분은 이전 예제와 동일 합니다. 그러나 **Postasync** 메서드에서 **BsonMediaTypeFormatter** 을 포맷터로 지정 합니다.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample10.cs)]

## <a name="serializing-top-level-primitive-types"></a>최상위 기본 형식 직렬화

모든 BSON 문서는 키/값 쌍의 목록입니다. BSON 사양은 정수 또는 문자열과 같은 단일 원시 값을 serialize 하는 구문을 정의 하지 않습니다.

이 제한을 해결 하기 위해 **BsonMediaTypeFormatter** 는 기본 형식을 특수 한 경우로 처리 합니다. Serialize 하기 전에 값을 키/값 쌍으로 변환 하 고 키를 "Value"로 변환 합니다. 예를 들어 API 컨트롤러가 정수를 반환 한다고 가정 합니다.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample11.cs)]

직렬화 하기 전에 BSON 포맷터는이를 다음 키/값 쌍으로 변환 합니다.

[!code-json[Main](bson-support-in-web-api-21/samples/sample12.json)]

Deserialize 할 때 포맷터는 데이터를 원래 값으로 다시 변환 합니다. 그러나 웹 API에서 원시 값을 반환 하는 경우 다른 BSON 파서를 사용 하는 클라이언트는이 경우를 처리 해야 합니다. 일반적으로 원시 값이 아닌 구조화 된 데이터를 반환 하는 것을 고려해 야 합니다.

## <a name="additional-resources"></a>추가 리소스

[Web API BSON 샘플](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BSONSample/)

[미디어 포맷터](media-formatters.md)
