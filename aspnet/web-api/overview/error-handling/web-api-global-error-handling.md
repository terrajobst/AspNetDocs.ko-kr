---
uid: web-api/overview/error-handling/web-api-global-error-handling
title: ASP.NET Web API 2-ASP.NET 4.x의 전역 오류 처리
author: davidmatson
description: ASP.NET 4.x의 ASP.NET Web API 2에 있는 전역 오류 처리에 대 한 개요입니다.
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: bffd7863-f63b-4b23-a13c-372b5492e9fb
msc.legacyurl: /web-api/overview/error-handling/web-api-global-error-handling
msc.type: authoredcontent
ms.openlocfilehash: 94f2d6d31d0b37f9bb0077e6258c70a2dfb1918d
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457741"
---
# <a name="global-error-handling-in-aspnet-web-api-2"></a>ASP.NET Web API 2의 전역 오류 처리

[David Matson](https://github.com/davidmatson), [Rick Anderson](https://twitter.com/RickAndMSFT)

이 항목에서는 ASP.NET 4.x의 ASP.NET Web API 2에서 전역 오류 처리에 대 한 개요를 제공 합니다. 현재는 Web API에서 전체적으로 오류를 기록 하거나 처리 하는 쉬운 방법이 없습니다. 일부 처리 되지 않은 예외는 [예외 필터](exception-handling.md)를 통해 처리할 수 있지만 예외 필터가 처리할 수 없는 여러 가지 경우가 있습니다. 다음은 그 예입니다.

1. 컨트롤러 생성자에서 throw된 예외
2. 메시지 처리기에서 throw된 예외
3. 라우팅 중에 throw된 예외
4. 응답 콘텐츠를 직렬화 하는 동안 throw 된 예외입니다.

이러한 예외를 기록 하 고 처리할 수 있는 간단 하 고 일관 된 방법을 제공 하려고 합니다. 

예외를 처리 하는 두 가지 주요 사례는 오류 응답을 보낼 수 있는 경우이 고, 그렇지 않은 경우에는 예외를 기록 하는 경우입니다. 후자의 경우는 스트리밍 응답 콘텐츠 중간에 예외가 throw 되는 경우를 예로 들 수 있습니다. 이 경우 상태 코드, 헤더 및 부분 콘텐츠가 이미 네트워크에 있으므로 새 응답 메시지를 보내는 것이 너무 늦 었으 므로 단순히 연결을 중단 합니다. 예외를 처리 하 여 새 응답 메시지를 생성할 수는 없지만 예외 로깅은 계속 지원 됩니다. 오류를 검색할 수 있는 경우 다음과 같이 적절 한 오류 응답을 반환할 수 있습니다.

[!code-csharp[Main](web-api-global-error-handling/samples/sample1.cs?highlight=6)]

### <a name="existing-options"></a>기존 옵션

[예외 필터](exception-handling.md)외에도 현재 [메시지 처리기](../advanced/http-message-handlers.md) 를 사용 하 여 모든 500 수준 응답을 관찰할 수 있지만 원래 오류에 대 한 컨텍스트를 제외 하 고 해당 응답에 대해 작동 하는 것은 어렵습니다. 메시지 처리기에는 처리할 수 있는 사례와 관련 된 예외 필터와 동일한 제한 사항이 있습니다. Web API는 오류 상태를 캡처하는 추적 인프라를 포함 하는 반면 추적 인프라는 진단 용 이며 프로덕션 환경에서 실행 하는 데 적합 하지 않습니다. 전역 예외 처리 및 로깅은 프로덕션 중에 실행 되 고 기존 모니터링 솔루션 (예: [ELMAH](https://code.google.com/p/elmah/) )에 연결 될 수 있는 서비스 여야 합니다.

### <a name="solution-overview"></a>솔루션 개요

 처리 되지 않은 예외를 기록 하 고 처리 하기 위해 두 개의 새로운 사용자 교체 서비스 [Iexceptionlogger](../releases/whats-new-in-aspnet-web-api-21.md) 및 Iexceptionlogger를 제공 합니다. 서비스는 매우 유사 하지만 두 가지 주요 차이점이 있습니다.

1. 여러 예외로 거를 등록 하는 것을 지원 하지만 단일 예외 처리기만 등록 합니다.
2. 연결을 중단 하려고 하는 경우에도 예외 로거가 항상 호출 됩니다. 예외 처리기는 보낼 응답 메시지를 계속 선택할 수 있는 경우에만 호출 됩니다.

두 서비스 모두 예외가 검색 된 지점의 관련 정보를 포함 하는 예외 컨텍스트에 대 한 액세스를 제공 합니다. 특히 [HttpRequestMessage](https://msdn.microsoft.com/library/system.net.http.httprequestmessage(v=vs.110).aspx), [httprequestcontext](https://msdn.microsoft.com/library/system.web.http.controllers.httprequestcontext(v=vs.118).aspx), throw 된 예외 및 예외 소스 (아래 세부 정보)를 포함 합니다.

### <a name="design-principles"></a>디자인 원칙

1. **주요 변경 내용 없음** 이 기능은 부 릴리스에 추가 되므로 솔루션에 영향을 주는 중요 한 제약 조건 중 하나는 형식 계약과 동작에 대 한 주요 변경 내용이 없다는 것입니다. 이 제약 조건은 기존 catch 블록을 사용 하 여 예외를 500 응답으로 설정 하는 몇 가지 정리 작업을 수행 합니다. 이러한 추가 정리는 이후 주요 릴리스에 대해 고려할 수 있습니다. 이 사항이 중요 한 경우 [ASP.NET Web API 사용자 음성](http://aspnet.uservoice.com/forums/147201-asp-net-web-api/suggestions/5451321-add-flag-to-enable-iexceptionlogger-and-iexception)에서 투표 하세요.
2. **WEB API 구문을 사용 하 여 일관성 유지** Web API의 필터 파이프라인은 작업별, 컨트롤러 특정 또는 전역 범위에서 논리를 적용 하는 유연성과 함께 교차 영역 문제를 처리 하는 좋은 방법입니다. 예외 필터를 비롯 한 필터에는 전역 범위에 등록 된 경우에도 항상 작업 및 컨트롤러 컨텍스트가 있습니다. 이 계약은 필터에 적합 하지만 전역 범위가 지정 된 예외 필터는 메시지 처리기에서 발생 하는 예외와 같은 일부 예외 처리 사례에 적합 하지 않습니다. 여기서 작업 또는 컨트롤러 컨텍스트는 존재 하지 않습니다. 예외 처리를 위해 필터에서 제공 하는 유연한 범위 지정을 사용 하려면 여전히 예외 필터가 필요 합니다. 그러나 컨트롤러 컨텍스트 외부에서 예외를 처리 해야 하는 경우 전체 전역 오류 처리 (컨트롤러 컨텍스트 및 작업 컨텍스트 제약 조건이 없는 항목)에 대 한 별도의 구성도 필요 합니다.

### <a name="when-to-use"></a>사용 시기

- 예외로 거는 Web API에 의해 catch 되는 처리 되지 않은 모든 예외를 표시 하는 솔루션입니다.
- 예외 처리기는 Web API에서 catch 한 처리 되지 않은 예외에 대 한 모든 가능한 응답을 사용자 지정 하기 위한 솔루션입니다.
- 예외 필터는 특정 작업이 나 컨트롤러와 관련 된 하위 집합의 처리 되지 않은 예외를 처리 하는 가장 쉬운 솔루션입니다.

### <a name="service-details"></a>서비스 정보

 예외로 거 및 처리기 서비스 인터페이스는 해당 컨텍스트를 가져오는 간단한 비동기 메서드입니다. 

[!code-csharp[Main](web-api-global-error-handling/samples/sample2.cs)]

 또한 두 인터페이스에 대 한 기본 클래스를 제공 합니다. 권장 된 시간에 로그 하거나 처리 하려면 핵심 (sync 또는 async) 메서드를 재정의 해야 합니다. 로깅의 경우, `ExceptionLogger` 기본 클래스는 나중에 호출 스택을 추가로 전파 하 고 다시 catch 하는 경우에도 각 예외에 대해 코어 로깅 메서드를 한 번만 호출 하는 것을 보장 합니다. `ExceptionHandler` 기본 클래스는 기존 중첩 된 catch 블록을 무시 하 고 호출 스택의 맨 위에 있는 예외에 대해서만 핵심 처리 메서드를 호출 합니다. 이러한 기본 클래스의 간소화 된 버전은 아래 부록에 있습니다. `IExceptionLogger` 및 `IExceptionHandler`는 모두 `ExceptionContext`를 통해 예외에 대 한 정보를 받습니다.

[!code-csharp[Main](web-api-global-error-handling/samples/sample3.cs)]

프레임 워크에서 예외로 거 또는 예외 처리기를 호출 하는 경우에는 항상 `Exception`와 `Request`를 제공 합니다. 단위 테스트를 제외 하 고는 항상 `RequestContext`제공 합니다. `ControllerContext` 및 `ActionContext`를 제공 하지 않습니다 (예외 필터에 대 한 catch 블록에서 호출 하는 경우에만). 매우 드물게 `Response`제공 됩니다 (응답을 쓰려고 하는 도중에 특정 IIS 사례 에서만). 이러한 속성 중 일부는 `null` 될 수 있으므로 예외 클래스의 멤버에 액세스 하기 전에 `null` 확인 해야 합니다.`CatchBlock` 예외를 확인 하는 catch 블록을 나타내는 문자열입니다. Catch 블록 문자열은 다음과 같습니다.

- HttpServer (SendAsync 메서드)
- HttpControllerDispatcher (SendAsync 메서드)
- HttpBatchHandler (SendAsync 메서드)
- IExceptionFilter (ApiController의 ExecuteAsync에서 예외 필터 파이프라인 처리)
- OWIN 호스트:

    - HttpMessageHandlerAdapter (버퍼링 출력의 경우)
    - HttpMessageHandlerAdapter (스트리밍 출력의 경우)
- 웹 호스트:

    - HttpControllerHandler (버퍼링 출력의 경우)
    - HttpControllerHandler (스트리밍 출력의 경우)
    - HttpControllerHandler (버퍼링 된 출력 모드에서 오류 복구에 실패 하는 경우)

정적 읽기 전용 속성을 통해서도 catch 블록 문자열의 목록을 사용할 수 있습니다. (핵심 catch 블록 문자열은 정적 System.web.http.exceptionhandling.exceptioncatchblocks.httpserver.sendasync의에 있으며 나머지는 OWIN 및 웹 호스트에 대해 각각 하나의 정적 클래스에 표시 됩니다.)`IsTopLevelCatchBlock` 는 호출 스택의 맨 위에 있는 예외 처리의 권장 패턴을 따라 다음과 같이 유용 합니다. 중첩 된 catch 블록이 발생 하는 모든 위치에서 예외를 500 응답으로 전환 하는 대신 예외 처리기가 호스트에서 볼 때까지 예외가 전파 되도록 할 수 있습니다.

`ExceptionContext`외에도 로거가 전체 `ExceptionLoggerContext`를 통해 하나 이상의 정보를 가져옵니다.

[!code-csharp[Main](web-api-global-error-handling/samples/sample4.cs)]

두 번째 속성인 `CanBeHandled`는로 거가 처리할 수 없는 예외를 식별할 수 있도록 합니다. 연결이 중단 되 고 새 응답 메시지를 보낼 수 없는 경우로 거가 호출 되지만 처리기가 호출 ***되지*** 않고 로거가이 속성에서이 시나리오를 식별할 수 있습니다.

`ExceptionContext`에 대 한 추가 처리기는 예외를 처리 하기 위해 전체 `ExceptionHandlerContext`에서 설정할 수 있는 하나 이상의 속성을 가져옵니다.

[!code-csharp[Main](web-api-global-error-handling/samples/sample5.cs)]

예외 처리기는 `Result` 속성을 작업 결과 (예: [Exceptionresult](https://msdn.microsoft.com/library/system.web.http.results.exceptionresult(v=vs.118).aspx), [internalservererrorresult](https://msdn.microsoft.com/library/system.web.http.results.internalservererrorresult(v=vs.118).aspx), [StatusCodeResult](https://msdn.microsoft.com/library/system.web.http.results.statuscoderesult(v=vs.118).aspx)또는 custom result)로 설정 하 여 예외를 처리 했음을 나타냅니다. `Result` 속성이 null 이면 예외가 처리 되지 않으며 원래 예외가 다시 throw 됩니다.

호출 스택의 맨 위에 있는 예외의 경우 응답이 API 호출자에 게 적합 한지 확인 하기 위해 추가 단계를 수행 했습니다. 예외가 호스트에 전파 되는 경우 호출자는 일반적으로 적절 한 API 오류 응답이 아닌 HTML이 고 일반적으로 HTML 인 응답을 제공 하는 노란색 화면을 볼 수 있습니다. 이러한 경우 결과가 null이 아닌 것으로 시작 되며, 사용자 지정 예외 처리기가 명시적으로 다시 `null` (처리 되지 않음)로 설정 된 경우에만 예외가 호스트에 전파 됩니다. 이러한 경우 `null` `Result`을 설정 하는 것은 두 가지 시나리오에 유용할 수 있습니다.

1. 웹 API 이전/외부에 등록 된 사용자 지정 예외 처리 미들웨어를 사용 하는 OWIN 호스팅된 웹 API입니다.
2. 브라우저를 통한 로컬 디버깅-죽음의 노란색 화면이 실제로는 처리 되지 않은 예외에 대 한 유용한 응답입니다.

예외로 거와 예외 처리기 모두에서로 거 또는 처리기 자체가 예외를 throw 하는 경우 복구할 항목을 수행 하지 않습니다. (예외를 전파 하는 것 외에도 더 나은 방법이 있는 경우이 페이지의 맨 아래에 의견을 남겨 두세요.) 예외로 거와 처리기에 대 한 계약은 예외가 호출자에 게 전파 되는 것을 허용 하지 않아야 합니다. 그렇지 않으면 예외는 일반적으로 호스트에 대 한 모든 방식으로 ASP와 같이 HTML 오류를 발생 시킬 수 있습니다. NET의 노란색 화면)이 다시 클라이언트로 전송 됩니다 (일반적으로 JSON 또는 XML을 필요로 하는 API 호출자의 기본 옵션이 아님).

## <a name="examples"></a>예

### <a name="tracing-exception-logger"></a>예외로 거 추적

아래 예외로 거는 구성 된 추적 소스 (Visual Studio의 디버그 출력 창 포함)로 예외 데이터를 보냅니다.

[!code-csharp[Main](web-api-global-error-handling/samples/sample6.cs)]

### <a name="custom-error-message-exception-handler"></a>사용자 지정 오류 메시지 예외 처리기

다음은 지원 담당자를 위한 전자 메일 주소를 포함 하 여 클라이언트에 대 한 사용자 지정 오류 응답을 생성 합니다.

[!code-csharp[Main](web-api-global-error-handling/samples/sample7.cs)]

## <a name="registering-exception-filters"></a>예외 필터 등록

"ASP.NET MVC 4 웹 응용 프로그램" 프로젝트 템플릿을 사용 하 여 프로젝트를 만드는 경우 *App/_Start* 폴더의 `WebApiConfig` 클래스 내부에 웹 API 구성 코드를 저장 합니다.

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

## <a name="appendix-base-class-details"></a>부록: 기본 클래스 세부 정보

[!code-csharp[Main](web-api-global-error-handling/samples/sample8.cs)]
