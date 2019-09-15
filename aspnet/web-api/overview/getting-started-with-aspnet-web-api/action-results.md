---
uid: web-api/overview/getting-started-with-aspnet-web-api/action-results
title: Web API 2-ASP.NET 4.x의 작업 결과
author: MikeWasson
description: ASP.NET Web API 컨트롤러 작업의 반환 값을 ASP.NET 4.x의 HTTP 응답 메시지로 변환 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: 2fc4797c-38ef-4cc7-926c-ca431c4739e8
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/action-results
msc.type: authoredcontent
ms.openlocfilehash: f00ac0db453053e53d6d6942dd1557b409f4167b
ms.sourcegitcommit: 4b324a11131e38f920126066b94ff478aa9927f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70985844"
---
# <a name="action-results-in-web-api-2"></a>Web API 2의 작업 결과

[!INCLUDE[](~/includes/coreWebAPI.md)]

이 항목에서는 ASP.NET Web API 컨트롤러 작업의 반환 값을 HTTP 응답 메시지로 변환 하는 방법에 대해 설명 합니다.

Web API 컨트롤러 작업은 다음 중 하나를 반환할 수 있습니다.

1. void
2. **HttpResponseMessage**
3. **IHttpActionResult**
4. 다른 형식

웹 API는 반환 되는 방법에 따라 다른 메커니즘을 사용 하 여 HTTP 응답을 만듭니다.

| 반환 형식 | Web API에서 응답을 만드는 방법 |
| --- | --- |
| void | 빈 204 반환 (내용 없음) |
| **HttpResponseMessage** | HTTP 응답 메시지로 직접 변환 합니다. |
| **IHttpActionResult** | **ExecuteAsync** 를 호출 하 여 **HttpResponseMessage**를 만든 다음 HTTP 응답 메시지로 변환 합니다. |
| 기타 형식 | Serialize 된 반환 값을 응답 본문에 씁니다. 200 (OK)을 반환 합니다. |

이 항목의 나머지 부분에서는 각 옵션에 대해 자세히 설명 합니다.

## <a name="void"></a>void

반환 형식이 `void`이면 웹 API는 상태 코드 204 (콘텐츠 없음)가 포함 된 빈 HTTP 응답을 반환 합니다.

컨트롤러 예:

[!code-csharp[Main](action-results/samples/sample1.cs)]

HTTP 응답:

[!code-console[Main](action-results/samples/sample2.cmd)]

## <a name="httpresponsemessage"></a>HttpResponseMessage

작업에서 [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx)를 반환 하는 경우 Web API는 **HttpResponseMessage** 개체의 속성을 사용 하 여 응답을 채우도록 반환 값을 HTTP 응답 메시지로 직접 변환 합니다.

이 옵션을 사용 하면 응답 메시지를 매우 효과적으로 제어할 수 있습니다. 예를 들어 다음 컨트롤러 작업은 Cache-control 헤더를 설정 합니다.

[!code-csharp[Main](action-results/samples/sample3.cs)]

응답:

[!code-console[Main](action-results/samples/sample4.cmd?highlight=2)]

도메인 모델을 **CreateResponse** 메서드에 전달 하는 경우 Web API는 [미디어 포맷터](../formats-and-model-binding/media-formatters.md) 를 사용 하 여 serialize 된 모델을 응답 본문에 씁니다.

[!code-csharp[Main](action-results/samples/sample5.cs)]

Web API는 요청에 Accept 헤더를 사용 하 여 포맷터를 선택 합니다. 자세한 내용은 [콘텐츠 협상](../formats-and-model-binding/content-negotiation.md)을 참조 하세요.

## <a name="ihttpactionresult"></a>IHttpActionResult

**IHttpActionResult** 인터페이스는 Web API 2에서 도입 되었습니다. 기본적으로 **HttpResponseMessage** 팩터리를 정의 합니다. **IHttpActionResult** 인터페이스를 사용할 경우의 몇 가지 이점은 다음과 같습니다.

- 컨트롤러의 [유닛 테스트](../testing-and-debugging/unit-testing-controllers-in-web-api.md) 를 간소화 합니다.
- HTTP 응답을 만들기 위한 공통 논리를 개별 클래스로 이동 합니다.
- 응답 생성에 대 한 하위 수준 세부 정보를 숨겨 컨트롤러 작업의 의도를 명확 하 게 합니다.

**IHttpActionResult** 에는 **HttpResponseMessage** 인스턴스를 비동기식으로 만드는 단일 메서드인 **ExecuteAsync**이 포함 되어 있습니다.

[!code-csharp[Main](action-results/samples/sample6.cs)]

컨트롤러 작업에서 **IHttpActionResult**를 반환 하는 경우 Web API는 **ExecuteAsync** 메서드를 호출 하 여 **HttpResponseMessage**를 만듭니다. 그런 다음 **HttpResponseMessage** 를 HTTP 응답 메시지로 변환 합니다.

다음은 일반 텍스트 응답을 만드는 간단한 **IHttpActionResult** 구현입니다.

[!code-csharp[Main](action-results/samples/sample7.cs)]

컨트롤러 작업 예:

[!code-csharp[Main](action-results/samples/sample8.cs)]

응답:

[!code-console[Main](action-results/samples/sample9.cmd)]

일반적으로 IHttpActionResult 네임 스페이스에 정의 된 구현을 사용 **[합니다.](https://msdn.microsoft.com/library/system.web.http.results.aspx)** **ApiController** 클래스는 이러한 기본 제공 작업 결과를 반환 하는 도우미 메서드를 정의 합니다.

다음 예에서는 요청이 기존 제품 ID와 일치 하지 않는 경우 컨트롤러가 [ApiController](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx) 를 호출 하 여 404 (찾을 수 없음) 응답을 만듭니다. 그렇지 않으면 컨트롤러가 ApiController를 호출 하 여 제품을 포함 하는 200 (OK) 응답을 만듭니다 [.](https://msdn.microsoft.com/library/dn314591.aspx)

[!code-csharp[Main](action-results/samples/sample10.cs)]

## <a name="other-return-types"></a>기타 반환 형식

다른 모든 반환 형식에 대해 Web API는 [미디어 포맷터](../formats-and-model-binding/media-formatters.md) 를 사용 하 여 반환 값을 직렬화 합니다. Web API는 serialize 된 값을 응답 본문에 씁니다. 응답 상태 코드는 200 (정상)입니다.

[!code-csharp[Main](action-results/samples/sample11.cs)]

이 방법의 단점은 404와 같은 오류 코드를 직접 반환할 수 없다는 것입니다. 그러나 오류 코드에 대해 **HttpResponseException** 을 throw 할 수 있습니다. 자세한 내용은 [ASP.NET Web API의 예외 처리](../error-handling/exception-handling.md)를 참조 하세요.

Web API는 요청에 Accept 헤더를 사용 하 여 포맷터를 선택 합니다. 자세한 내용은 [콘텐츠 협상](../formats-and-model-binding/content-negotiation.md)을 참조 하세요.

요청 예

[!code-console[Main](action-results/samples/sample12.cmd)]

예제 응답

[!code-console[Main](action-results/samples/sample13.cmd)]
