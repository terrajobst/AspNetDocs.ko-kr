---
uid: web-api/overview/advanced/http-cookies
title: ASP.NET Web API의 HTTP 쿠키-ASP.NET 4.x
author: MikeWasson
description: ASP.NET 4.x 용 Web API에서 HTTP 쿠키를 보내고 받는 방법에 대해 설명 합니다.
ms.author: riande
ms.date: 09/17/2012
ms.custom: seoapril2019
ms.assetid: 243db2ec-8f67-4a5e-a382-4ddcec4b4164
msc.legacyurl: /web-api/overview/advanced/http-cookies
msc.type: authoredcontent
ms.openlocfilehash: 8ca26ff6776daa13bc4f8b06c2eba61afcfefba2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449315"
---
# <a name="http-cookies-in-aspnet-web-api"></a>ASP.NET Web API의 HTTP 쿠키

[Mike Wasson](https://github.com/MikeWasson)

이 항목에서는 Web API에서 HTTP 쿠키를 보내고 받는 방법에 대해 설명 합니다.

## <a name="background-on-http-cookies"></a>HTTP 쿠키의 배경

이 섹션에서는 HTTP 수준에서 쿠키를 구현 하는 방법에 대 한 간략 한 개요를 제공 합니다. 자세한 내용은 [RFC 6265](http://tools.ietf.org/html/rfc6265)을 참조 하세요.

쿠키는 서버가 HTTP 응답으로 보내는 데이터의 일부입니다. 클라이언트 (선택 사항)는 쿠키를 저장 하 고 후속 요청에서 반환 합니다. 이렇게 하면 클라이언트와 서버가 상태를 공유할 수 있습니다. 쿠키를 설정 하기 위해 서버는 응답에 설정-쿠키 헤더를 포함 합니다. 쿠키 형식은 선택적 특성이 있는 이름-값 쌍입니다. 다음은 그 예입니다.

[!code-powershell[Main](http-cookies/samples/sample1.ps1)]

특성을 사용 하는 예제는 다음과 같습니다.

[!code-powershell[Main](http-cookies/samples/sample2.ps1)]

서버에 쿠키를 반환 하기 위해 클라이언트는 이후 요청에 쿠키 헤더를 포함 합니다.

[!code-console[Main](http-cookies/samples/sample3.cmd)]

![](http-cookies/_static/image1.png)

HTTP 응답에는 여러 개의 Set 쿠키 헤더가 포함 될 수 있습니다.

[!code-powershell[Main](http-cookies/samples/sample4.ps1)]

클라이언트는 단일 쿠키 헤더를 사용 하 여 여러 쿠키를 반환 합니다.

[!code-console[Main](http-cookies/samples/sample5.cmd)]

쿠키의 범위 및 기간은 Set 쿠키 헤더의 다음 특성에 의해 제어 됩니다.

- **도메인**: 쿠키를 받아야 하는 도메인을 클라이언트에 알립니다. 예를 들어 도메인이 "example.com" 이면 클라이언트는 example.com의 모든 하위 도메인에 쿠키를 반환 합니다. 지정 하지 않으면 도메인은 원본 서버입니다.
- **경로**: 도메인 내의 지정 된 경로로 쿠키를 제한 합니다. 지정 하지 않으면 요청 URI의 경로가 사용 됩니다.
- **Expires**: 쿠키에 대 한 만료 날짜를 설정 합니다. 클라이언트는 만료 되 면 쿠키를 삭제 합니다.
- **최대 사용 기간**: 쿠키에 대 한 최대 기간을 설정 합니다. 최대 사용 기간에 도달 하면 클라이언트에서 쿠키를 삭제 합니다.

`Expires`와 `Max-Age`를 모두 설정 하는 경우 `Max-Age`가 우선적으로 적용 됩니다. 둘 다 설정 하지 않으면 현재 세션이 종료 될 때 클라이언트에서 쿠키를 삭제 합니다. "Session"의 정확한 의미는 사용자 에이전트에 의해 결정 됩니다.

그러나 클라이언트는 쿠키를 무시할 수 있습니다. 예를 들어 사용자는 개인 정보 보호를 위해 쿠키를 사용 하지 않도록 설정할 수 있습니다. 클라이언트는 만료 되기 전에 쿠키를 삭제 하거나 저장 된 쿠키 수를 제한할 수 있습니다. 개인 정보 보호를 위해 클라이언트는 종종 "타사" 쿠키를 거부 합니다. 여기서 도메인은 원본 서버와 일치 하지 않습니다. 간단히 말해서 서버는 설정 된 쿠키를 다시 가져오는 데 의존해 서는 안 됩니다.

## <a name="cookies-in-web-api"></a>Web API의 쿠키

쿠키를 HTTP 응답에 추가 하려면 쿠키를 나타내는 **CookieHeaderValue** 인스턴스를 만듭니다. 그런 다음 시스템 .Net. Http에 정의 된 **Addcookies** 확장 메서드를 호출 합니다 **. HttpResponseHeadersExtensions** 클래스를 추가 하 여 쿠키를 추가 합니다.

예를 들어 다음 코드는 컨트롤러 작업 내에 쿠키를 추가 합니다.

[!code-csharp[Main](http-cookies/samples/sample6.cs)]

**Addcookies** 는 **CookieHeaderValue** 인스턴스의 배열을 사용 합니다.

클라이언트 요청에서 쿠키를 추출 하려면 **Getcookies** 메서드를 호출 합니다.

[!code-csharp[Main](http-cookies/samples/sample7.cs)]

**CookieHeaderValue** 에는 **CookieState** 인스턴스 컬렉션이 포함 되어 있습니다. 각 **CookieState** 는 하나의 쿠키를 나타냅니다. 다음과 같이 인덱서 메서드를 사용 하 여 이름을 기준으로 **CookieState** 를 가져옵니다.

## <a name="structured-cookie-data"></a>구조적 쿠키 데이터

많은 브라우저에서 총 수와 도메인당 수를&#8212;저장할 쿠키 수를 제한 합니다. 따라서 여러 쿠키를 설정 하는 대신 단일 쿠키에 구조화 된 데이터를 저장 하는 것이 유용할 수 있습니다.

> [!NOTE]
> RFC 6265는 쿠키 데이터의 구조를 정의 하지 않습니다.

**CookieHeaderValue** 클래스를 사용 하 여 쿠키 데이터의 이름-값 쌍 목록을 전달할 수 있습니다. 이러한 이름-값 쌍은 집합 쿠키 헤더에 URL로 인코딩된 폼 데이터로 인코딩됩니다.

[!code-csharp[Main](http-cookies/samples/sample8.cs)]

이전 코드는 다음과 같은 설정 쿠키 헤더를 생성 합니다.

[!code-powershell[Main](http-cookies/samples/sample9.ps1)]

**CookieState** 클래스는 요청 메시지의 쿠키에서 하위 값을 읽을 수 있는 인덱서 메서드를 제공 합니다.

[!code-csharp[Main](http-cookies/samples/sample10.cs)]

## <a name="example-set-and-retrieve-cookies-in-a-message-handler"></a>예: 메시지 처리기에서 쿠키 설정 및 검색

이전 예제에서는 Web API 컨트롤러 내에서 쿠키를 사용 하는 방법을 살펴보았습니다. 또 다른 옵션은 [메시지 처리기](http-message-handlers.md)를 사용 하는 것입니다. 메시지 처리기는 컨트롤러 보다 이전에 파이프라인에서 호출 됩니다. 메시지 처리기는 요청이 컨트롤러에 도달 하기 전에 요청에서 쿠키를 읽거나 컨트롤러에서 응답을 생성 한 후 응답에 쿠키를 추가할 수 있습니다.

![](http-cookies/_static/image2.png)

다음 코드에서는 세션 Id를 만들기 위한 메시지 처리기를 보여 줍니다. 세션 ID는 쿠키에 저장 됩니다. 처리기는 세션 쿠키에 대 한 요청을 확인 합니다. 요청에 쿠키가 포함 되지 않은 경우 처리기는 새 세션 ID를 생성 합니다. 두 경우 모두 처리기는 **HttpRequestMessage** 속성 모음에 세션 ID를 저장 합니다. 또한 세션 쿠키를 HTTP 응답에 추가 합니다.

이 구현에서는 클라이언트의 세션 ID가 실제로 서버에서 발급 되었는지 확인 하지 않습니다. 인증 형식으로 사용 하지 마세요. 예제는 HTTP 쿠키 관리를 표시 하는 것입니다.

[!code-csharp[Main](http-cookies/samples/sample11.cs)]

컨트롤러는 **HttpRequestMessage** 속성 모음에서 세션 ID를 가져올 수 있습니다.

[!code-csharp[Main](http-cookies/samples/sample12.cs)]
