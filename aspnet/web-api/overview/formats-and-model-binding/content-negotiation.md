---
uid: web-api/overview/formats-and-model-binding/content-negotiation
title: ASP.NET Web API의 콘텐츠 협상-ASP.NET 4.x
author: MikeWasson
description: ASP.NET Web API에서 ASP.NET 4.x에 대 한 HTTP 콘텐츠 협상을 구현 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 05/20/2012
ms.custom: seoapril2019
ms.assetid: 0dd51b30-bf5a-419f-a1b7-2817ccca3c7d
msc.legacyurl: /web-api/overview/formats-and-model-binding/content-negotiation
msc.type: authoredcontent
ms.openlocfilehash: cb6668ff6de276d3778ce11f27ce597d8bf1f9c7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504659"
---
# <a name="content-negotiation-in-aspnet-web-api"></a>ASP.NET Web API의 콘텐츠 협상

[Mike Wasson](https://github.com/MikeWasson)

이 문서에서는 ASP.NET Web API ASP.NET 4.x에 대해 콘텐츠 협상을 구현 하는 방법을 설명 합니다.

HTTP 사양 (RFC 2616)은 "여러 표현을 사용할 수 있는 경우 지정 된 응답에 대 한 최상의 표현을 선택 하는 프로세스"로 콘텐츠 협상을 정의 합니다. HTTP의 콘텐츠 협상에 대 한 기본 메커니즘은 다음 요청 헤더입니다.

- **수락:** 응답에 허용 되는 미디어 유형 (예: "application/json" "application/xml") 또는 &quot;application/vnd와 같은 사용자 지정 미디어 유형입니다. 예 + xml&quot;
- **허용 문자 집합:** UTF-8 또는 ISO 8859-1 같은 문자 집합을 사용할 수 있습니다.
- **수락-인코딩:** Gzip과 같은 허용 되는 콘텐츠 인코딩
- **수락 언어:** "En-us"와 같은 기본 자연 언어입니다.

서버는 HTTP 요청의 다른 부분을 볼 수도 있습니다. 예를 들어 요청에 X로 요청 된 헤더 (AJAX 요청을 나타냄)가 포함 된 경우 Accept 헤더가 없으면 서버는 기본적으로 JSON으로 지정할 수 있습니다.

이 문서에서는 Web API가 허용 및 허용 문자 집합 헤더를 사용 하는 방법을 살펴보겠습니다. (현재는 허용 인코딩 또는 수락 언어를 기본적으로 지원 하지 않습니다.)

## <a name="serialization"></a>직렬화

Web API 컨트롤러에서 CLR 형식으로 리소스를 반환 하는 경우 파이프라인은 반환 값을 직렬화 하 고 HTTP 응답 본문에 씁니다.

예를 들어 다음 컨트롤러 작업을 고려 하십시오.

[!code-csharp[Main](content-negotiation/samples/sample1.cs)]

클라이언트에서이 HTTP 요청을 보낼 수 있습니다.

[!code-console[Main](content-negotiation/samples/sample2.cmd)]

응답으로 서버에서 다음을 보낼 수 있습니다.

[!code-console[Main](content-negotiation/samples/sample3.cmd)]

이 예에서 클라이언트는 JSON, Javascript 또는 "모든 항목" (\*/\*)을 요청 했습니다. 서버가 `Product` 개체의 JSON 표현으로 응답 했습니다. 응답의 Content-type 헤더는 &quot;application/json&quot;로 설정 됩니다.

컨트롤러는 **HttpResponseMessage** 개체를 반환할 수도 있습니다. 응답 본문에 대 한 CLR 개체를 지정 하려면 **CreateResponse** 확장 메서드를 호출 합니다.

[!code-csharp[Main](content-negotiation/samples/sample4.cs)]

이 옵션을 사용 하면 응답의 세부 정보를 더 세밀 하 게 제어할 수 있습니다. 상태 코드를 설정 하 고 HTTP 헤더를 추가 하는 등의 방법을 사용할 수 있습니다.

리소스를 serialize 하는 개체를 *미디어 포맷터*라고 합니다. 미디어 포맷터는 **MediaTypeFormatter** 클래스에서 파생 됩니다. Web API는 XML 및 JSON에 대 한 미디어 포맷터를 제공 하며, 다른 미디어 유형을 지원 하기 위해 사용자 지정 포맷터를 만들 수 있습니다. 사용자 지정 포맷터를 작성 하는 방법에 대 한 자세한 내용은 [미디어 포맷터](media-formatters.md)를 참조 하세요.

## <a name="how-content-negotiation-works"></a>콘텐츠 협상의 작동 방식

먼저 파이프라인은 **Httpconfiguration** 개체에서 **IContentNegotiator** 서비스를 가져옵니다. 또한 **Httpconfiguration. 포맷터** 컬렉션에서 미디어 포맷터 목록을 가져옵니다.

다음으로 파이프라인은 **IContentNegotiator**를 호출 하 고 다음을 전달 합니다.

- Serialize 할 개체의 형식입니다.
- 미디어 포맷터의 컬렉션입니다.
- HTTP 요청

**Negotiate** 메서드는 다음 두 가지 정보를 반환 합니다.

- 사용할 포맷터
- 응답의 미디어 유형입니다.

포맷터를 찾을 수 없는 경우 **Negotiate** 메서드는 **null**을 반환 하 고 클라이언트는 HTTP 오류 406 (허용 되지 않음)을 수신 합니다.

다음 코드는 컨트롤러에서 직접 콘텐츠 협상을 호출 하는 방법을 보여 줍니다.

[!code-csharp[Main](content-negotiation/samples/sample5.cs)]

이 코드는 파이프라인이 자동으로 수행 하는 작업에 해당 합니다.

## <a name="default-content-negotiator"></a>기본 콘텐츠 Negotiator

**Defaultcontentnegotiator** 클래스는 기본 구현을 제공 합니다. 여러 가지 조건을 사용 하 여 포맷터를 선택 합니다.

먼저 포맷터가 형식을 직렬화 할 수 있어야 합니다. 이는 **MediaTypeFormatter**를 호출 하 여 확인 됩니다.

그런 다음, 콘텐츠 negotiator 각 포맷터를 살펴보고 HTTP 요청과 얼마나 잘 일치 하는지 평가 합니다. 일치를 평가 하기 위해 콘텐츠 negotiator 포맷터에서 다음 두 가지를 살펴봅니다.

- **SupportedMediaTypes** 컬렉션에는 지원 되는 미디어 형식 목록이 포함 되어 있습니다. 콘텐츠 negotiator이 목록을 요청 수락 헤더와 일치 시 키 려 고 합니다. Accept 헤더는 범위를 포함할 수 있습니다. 예를 들어 "텍스트/일반"은 텍스트/\* 또는 \*/\*일치 합니다.
- **MediaTypeMapping** 개체의 목록을 포함 하는 **MediaTypeMappings** 컬렉션입니다. **MediaTypeMapping** 클래스는 HTTP 요청을 미디어 유형과 일치 시키는 일반적인 방법을 제공 합니다. 예를 들어 사용자 지정 HTTP 헤더를 특정 미디어 형식에 매핑할 수 있습니다.

일치 하는 항목이 여러 개인 경우 가장 높은 품질의 일치 항목이 적용 됩니다. 다음은 그 예입니다.

[!code-console[Main](content-negotiation/samples/sample6.cmd)]

이 예제에서 application/json은 1.0의 암시 된 품질을 가지 므로 application/xml 보다 우선적으로 적용 됩니다.

일치 하는 항목이 없는 경우 콘텐츠 negotiator 요청 본문의 미디어 형식 (있는 경우)을 찾으려고 시도 합니다. 예를 들어 요청에 JSON 데이터가 포함 된 경우 콘텐츠 negotiator JSON 포맷터를 찾습니다.

여전히 일치 하는 항목이 없으면 콘텐츠를 serialize 할 수 있는 첫 번째 포맷터만 선택 하면 됩니다.

## <a name="selecting-a-character-encoding"></a>문자 인코딩 선택

포맷터를 선택 하 고 나면 content negotiator는 포맷터의 **supportedencodings** 속성을 확인 하 고 요청 (있는 경우)의 허용 되는 문자 집합 헤더와 일치 하 여 가장 적합 한 문자 인코딩을 선택 합니다.
