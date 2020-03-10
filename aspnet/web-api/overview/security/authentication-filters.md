---
uid: web-api/overview/security/authentication-filters
title: ASP.NET Web API 2의 인증 필터 | Microsoft Docs
author: MikeWasson
description: 인증 필터는 HTTP 요청을 인증 하는 구성 요소입니다. Web API 2 및 MVC 5는 모두 인증 필터를 지원 하지만 약간 다릅니다.
ms.author: riande
ms.date: 09/25/2014
ms.assetid: b9882e53-b3ca-4def-89b0-322846973ccb
msc.legacyurl: /web-api/overview/security/authentication-filters
msc.type: authoredcontent
ms.openlocfilehash: 2ef9e62a6c634237e920b6d7aba2127b835f959d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447773"
---
# <a name="authentication-filters-in-aspnet-web-api-2"></a>ASP.NET Web API 2의 인증 필터

[Mike Wasson](https://github.com/MikeWasson)

> 인증 필터는 HTTP 요청을 인증 하는 구성 요소입니다. Web API 2 및 MVC 5는 모두 인증 필터를 지원 하지만 대부분 필터 인터페이스에 대 한 명명 규칙에 따라 약간 다릅니다. 이 항목에서는 Web API 인증 필터에 대해 설명 합니다.

인증 필터를 사용 하면 개별 컨트롤러 또는 작업에 대 한 인증 체계를 설정할 수 있습니다. 이런 방식으로 앱은 다양 한 HTTP 리소스에 대해 서로 다른 인증 메커니즘을 지원할 수 있습니다.

이 문서에서는 [https://github.com/aspnet/samples](https://github.com/aspnet/samples)에 대 한 [기본 인증](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BasicAuthentication) 샘플의 코드를 표시 합니다. 이 샘플에서는 HTTP 기본 액세스 인증 체계 (RFC 2617)를 구현 하는 인증 필터를 보여 줍니다. 필터는 `IdentityBasicAuthenticationAttribute`이라는 클래스에서 구현 됩니다. 예제에서 코드를 모두 표시 하지는 않습니다. 인증 필터를 작성 하는 방법을 보여 주는 부분만 있으면 됩니다.

## <a name="setting-an-authentication-filter"></a>인증 필터 설정

다른 필터와 마찬가지로 인증 필터는 포트당, 작업별 또는 모든 웹 API 컨트롤러에 전역적으로 적용 될 수 있습니다.

컨트롤러에 인증 필터를 적용 하려면 컨트롤러 클래스를 필터 특성으로 데코 레이트 합니다. 다음 코드는 컨트롤러 클래스에 대 한 `[IdentityBasicAuthentication]` 필터를 설정 하 여 컨트롤러의 모든 작업에 대해 기본 인증을 사용 하도록 설정 합니다.

[!code-csharp[Main](authentication-filters/samples/sample1.cs)]

하나의 작업에 필터를 적용 하려면 필터를 사용 하 여 작업을 데코 레이트 합니다. 다음 코드는 컨트롤러의 `Post` 메서드에 `[IdentityBasicAuthentication]` 필터를 설정 합니다.

[!code-csharp[Main](authentication-filters/samples/sample2.cs)]

모든 Web API 컨트롤러에 필터를 적용 하려면이를 **Globalconfiguration. 필터**에 추가 합니다.

[!code-csharp[Main](authentication-filters/samples/sample3.cs)]

## <a name="implementing-a-web-api-authentication-filter"></a>Web API 인증 필터 구현

Web API에서 인증 필터는 System.web. p. [i](https://msdn.microsoft.com/library/system.web.http.filters.iauthenticationfilter.aspx) o p. 또한 특성으로 적용 하기 위해 **system.object**에서 상속 해야 합니다.

**Iauthenticationfilter** 인터페이스에는 두 가지 방법이 있습니다.

- **AuthenticateAsync** 는 요청에서 자격 증명의 유효성을 검사 하 여 요청을 인증 합니다 (있는 경우).
- **ChallengeAsync** 은 필요한 경우 HTTP 응답에 인증 챌린지를 추가 합니다.

이러한 메서드는 [rfc 2612](http://tools.ietf.org/html/rfc2616) 및 [rfc 2617](http://tools.ietf.org/html/rfc2617)에 정의 된 인증 흐름에 해당 합니다.

1. 클라이언트는 인증 헤더에 자격 증명을 보냅니다. 이는 일반적으로 클라이언트가 서버 로부터 401 (권한 없음) 응답을 받은 후에 발생 합니다. 그러나 클라이언트는 401을 받은 후 뿐만 아니라 모든 요청과 함께 자격 증명을 보낼 수 있습니다.
2. 서버에서 자격 증명을 허용 하지 않는 경우 401 (권한 없음) 응답을 반환 합니다. 응답에는 하나 이상의 과제가 포함 된 Www 인증 헤더가 포함 되어 있습니다. 각 챌린지는 서버에서 인식 하는 인증 체계를 지정 합니다.

서버는 익명 요청에서 401을 반환할 수도 있습니다. 실제로 인증 프로세스를 시작 하는 방법은 다음과 같습니다.

1. 클라이언트는 익명 요청을 보냅니다.
2. 서버는 401을 반환 합니다.
3. 클라이언트는 자격 증명을 사용 하 여 요청을 다시 보냅니다.

이 흐름에는 *인증* 및 *권한 부여* 단계가 모두 포함 됩니다.

- 인증에서 클라이언트의 id를 증명 합니다.
- 권한 부여는 클라이언트가 특정 리소스에 액세스할 수 있는지 여부를 확인 합니다.

Web API에서 인증 필터는 인증을 처리 하지만 권한 부여는 처리 하지 않습니다. 권한 부여 필터 또는 컨트롤러 작업 내에서 권한 부여를 수행 해야 합니다.

웹 API 2 파이프라인의 흐름은 다음과 같습니다.

1. 웹 API는 동작을 호출 하기 전에 해당 작업에 대 한 인증 필터 목록을 만듭니다. 여기에는 작업 범위, 컨트롤러 범위 및 전역 범위를 포함 하는 필터가 포함 됩니다.
2. 웹 API는 목록의 모든 필터에 대해 **AuthenticateAsync** 를 호출 합니다. 각 필터는 요청에서 자격 증명의 유효성을 검사할 수 있습니다. 자격 증명의 유효성을 검사 하는 필터가 있으면이 필터는 **IPrincipal** 을 만들어 요청에 연결 합니다. 이 시점에서 필터는 오류를 트리거할 수도 있습니다. 이 경우 나머지 파이프라인은 실행 되지 않습니다.
3. 오류가 없는 것으로 가정 하 여 요청은 파이프라인의 나머지 부분을 통해 흐릅니다.
4. 마지막으로 Web API는 모든 인증 필터의 **ChallengeAsync** 메서드를 호출 합니다. 필터는 필요한 경우이 메서드를 사용 하 여 응답에 챌린지를 추가 합니다. 401 오류에 대 한 응답으로 발생 하는 일반적으로는 항상 그렇지는 않습니다.

다음 다이어그램에서는 두 가지 가능한 사례를 보여 줍니다. 첫 번째는 인증 필터에서 요청을 성공적으로 인증 하 고, 권한 부여 필터에서 요청을 승인 하 고, 컨트롤러 작업에서 200 (OK)를 반환 합니다.

![](authentication-filters/_static/image1.png)

두 번째 예제에서는 인증 필터에서 요청을 인증 하지만 권한 부여 필터는 401 (권한 없음)을 반환 합니다. 이 경우 컨트롤러 작업은 호출 되지 않습니다. 인증 필터는 Www-인증 헤더를 응답에 추가 합니다.

![](authentication-filters/_static/image2.png)

예를 들어, 컨트롤러 작업에서 익명 요청을 허용 하는 경우 다른 조합을&mdash;사용할 수 있습니다. 인증 필터는 있지만 권한 부여는 없을 수 있습니다.

## <a name="implementing-the-authenticateasync-method"></a>AuthenticateAsync 메서드 구현

**AuthenticateAsync** 메서드는 요청을 인증 하려고 합니다. 메서드 서명은 다음과 같습니다.

[!code-csharp[Main](authentication-filters/samples/sample4.cs)]

**AuthenticateAsync** 메서드는 다음 중 하나를 수행 해야 합니다.

1. Nothing (no op).
2. **IPrincipal** 을 만들고 요청에 대해 설정 합니다.
3. 오류 결과를 설정 합니다.

옵션 (1)은 필터에서 인식 하는 자격 증명이 요청에 없음을 의미 합니다. 옵션 (2)은 필터가 요청을 성공적으로 인증 했음을 의미 합니다. 옵션 (3)은 요청에 잘못 된 자격 증명 (예: 잘못 된 암호)이 있어 오류 응답을 트리거하는 것을 의미 합니다.

**AuthenticateAsync**구현에 대 한 일반적인 개요는 다음과 같습니다.

1. 요청에서 자격 증명을 찾습니다.
2. 자격 증명이 없는 경우 아무 작업도 수행 하지 않고 반환 (op 없음)을 반환 합니다.
3. 자격 증명이 있지만 필터에서 인증 체계를 인식 하지 못하는 경우 아무 작업도 수행 하지 않고 반환 (op 없음)을 반환 합니다. 파이프라인의 다른 필터에서 스키마를 이해할 수 있습니다.
4. 필터가 이해 하는 자격 증명이 있으면 인증을 시도 합니다.
5. 자격 증명이 잘못 된 경우 `context.ErrorResult`설정 하 여 401을 반환 합니다.
6. 자격 증명이 유효 하면 **IPrincipal** 을 만들고 `context.Principal`를 설정 합니다.

다음 코드는 [기본 인증](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BasicAuthentication) 샘플의 **AuthenticateAsync** 메서드를 보여 줍니다. 주석은 각 단계를 표시 합니다. 이 코드는 자격 증명이 없는 인증 헤더, 잘못 된 자격 증명, 잘못 된 사용자 이름/암호 등의 여러 가지 오류 유형을 보여 줍니다.

[!code-csharp[Main](authentication-filters/samples/sample5.cs)]

## <a name="setting-an-error-result"></a>오류 결과 설정

자격 증명이 유효 하지 않은 경우 필터는 오류 응답을 생성 하는 **IHttpActionResult** 로 `context.ErrorResult` 설정 해야 합니다. **IHttpActionResult**에 대 한 자세한 내용은 [Web API 2의 작업 결과](../getting-started-with-aspnet-web-api/action-results.md)를 참조 하세요.

기본 인증 샘플에는이 용도에 적합 한 `AuthenticationFailureResult` 클래스가 포함 되어 있습니다.

[!code-csharp[Main](authentication-filters/samples/sample6.cs)]

## <a name="implementing-challengeasync"></a>ChallengeAsync 구현

**ChallengeAsync** 메서드의 목적은 필요한 경우 응답에 인증 과제를 추가 하는 것입니다. 메서드 서명은 다음과 같습니다.

[!code-csharp[Main](authentication-filters/samples/sample7.cs)]

메서드는 요청 파이프라인의 모든 인증 필터에서 호출 됩니다.

**ChallengeAsync** 는 HTTP 응답을 만들기 *전에* 호출 되 고, 컨트롤러 작업이 실행 되기 전에도 호출 된다는 것을 이해 하는 것이 중요 합니다. **ChallengeAsync** 가 호출 되 면 나중에 HTTP 응답을 만드는 데 사용 되는 **IHttpActionResult**가 `context.Result`에 포함 됩니다. 따라서 **ChallengeAsync** 를 호출 하면 HTTP 응답에 대 한 어떠한 정보도 알 수 없습니다. **ChallengeAsync** 메서드는 `context.Result`의 원래 값을 새 **IHttpActionResult**바꿉니다. 이 **IHttpActionResult** 는 원래 `context.Result`을 래핑해야 합니다.

![](authentication-filters/_static/image3.png)

원래 **IHttpActionResult** *내부 결과*를 호출 하 고 새 **IHttpActionResult** *외부 결과*를 호출 합니다. 외부 결과는 다음을 수행 해야 합니다.

1. 내부 결과를 호출 하 여 HTTP 응답을 만듭니다.
2. 응답을 검사 합니다.
3. 필요한 경우 응답에 인증 챌린지를 추가 합니다.

다음 예제는 기본 인증 샘플에서 가져온 것입니다. 외부 결과에 대 한 **IHttpActionResult** 를 정의 합니다.

[!code-csharp[Main](authentication-filters/samples/sample8.cs)]

`InnerResult` 속성은 내부 **IHttpActionResult**를 포함 합니다. `Challenge` 속성은 Www 인증 헤더를 나타냅니다. **ExecuteAsync** 는 먼저 `InnerResult.ExecuteAsync`를 호출 하 여 HTTP 응답을 만든 다음 필요한 경우 챌린지를 추가 합니다.

챌린지를 추가 하기 전에 응답 코드를 확인 합니다. 대부분의 인증 체계는 다음과 같이 응답이 401 인 경우에만 챌린지를 추가 합니다. 그러나 일부 인증 스키마는 성공 응답에 챌린지를 추가 합니다. 예를 들어 [Negotiate](http://tools.ietf.org/html/rfc4559#section-5) (RFC 4559)을 참조 하세요.

`AddChallengeOnUnauthorizedResult` 클래스가 지정 된 경우 **ChallengeAsync** 의 실제 코드는 간단 합니다. 결과를 만들어 `context.Result`에 연결 하기만 하면 됩니다.

[!code-csharp[Main](authentication-filters/samples/sample9.cs)]

참고: 기본 인증 샘플은 확장 메서드에 배치 하 여이 논리를 비트로 추상화 합니다.

## <a name="combining-authentication-filters-with-host-level-authentication"></a>호스트 수준 인증과 인증 필터 조합

"호스트 수준 인증"은 요청이 웹 API 프레임 워크에 도달 하기 전에 호스트 (예: IIS)에서 수행 하는 인증입니다.

응용 프로그램의 나머지 부분에 대해 호스트 수준 인증을 사용 하도록 설정 하 고 Web API 컨트롤러에 대해 사용 하지 않도록 설정 하는 경우가 종종 있습니다. 예를 들어 일반적인 시나리오는 호스트 수준에서 폼 인증을 사용 하도록 설정 하 고 Web API에는 토큰 기반 인증을 사용 하는 것입니다.

웹 API 파이프라인 내에서 호스트 수준 인증을 사용 하지 않도록 설정 하려면 구성에서 `config.SuppressHostPrincipal()`를 호출 합니다. 이렇게 하면 web API는 Web api 파이프라인으로 들어가는 모든 요청에서 **IPrincipal** 을 제거 합니다. 효과적으로 요청&quot; 인증을 취소할 &quot;.

[!code-csharp[Main](authentication-filters/samples/sample10.cs)]

## <a name="additional-resources"></a>추가 리소스

[보안 필터 ASP.NET Web API](https://msdn.microsoft.com/magazine/dn781361.aspx) (MSDN Magazine)
