---
title: ASP.NET에서 SameSite 쿠키 사용
author: rick-anderson
description: 를 사용 하 여 ASP.NET에서 쿠키를 SameSite 하는 방법을 알아봅니다.
ms.author: riande
ms.date: 1/22/2019
uid: samesite/system-web-samesite
ms.openlocfilehash: c262e300361f33621e8bd126a34b251c23f56e1a
ms.sourcegitcommit: 6bd0d7581ec36dc32cb85d0d5fc0e51068dd4423
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/14/2020
ms.locfileid: "77234764"
---
# <a name="work-with-samesite-cookies-in-aspnet"></a>ASP.NET에서 SameSite 쿠키 사용

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

SameSite은 CSRF (교차 사이트 요청 위조) 공격에 대 한 보호를 제공 하도록 설계 된 [IETF](https://ietf.org/about/) 초안 표준입니다. 원래 [2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07)에서는 초안 표준이 [2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)에서 업데이트 되었습니다. 업데이트 된 표준은 이전 표준과 호환 되지 않으며 다음과 같은 가장 눈에 띄는 차이점이 있습니다.

* SameSite 헤더가 없는 쿠키는 기본적으로 `SameSite=Lax`으로 처리 됩니다.
* 사이트 간 쿠키 사용을 허용 하려면 `SameSite=None`를 사용 해야 합니다.
* `SameSite=None` 어설션 하는 쿠키도 `Secure`로 표시 되어야 합니다.
* SameSite = None 값은 [2016 표준](https://tools.ietf.org/html/draft-west-first-party-cookies-07) 에서 허용 되지 않으며 일부 구현에서는 이러한 쿠키를 SameSite = Strict로 처리 합니다. 이 문서의 [이전 브라우저 지원](#sob) 을 참조 하세요.

`SameSite=Lax` 설정은 대부분의 응용 프로그램 쿠키에 대해 작동 합니다. Oidc ( [Openid connect Connect](https://openid.net/connect/) )와 같은 일부 형태의 인증 및 [ws-federation](https://auth0.com/docs/protocols/ws-fed) 은 게시 기반 리디렉션에 대해 기본적으로 사용 됩니다. 사후 기반 리디렉션은 SameSite 브라우저 보호를 트리거하고 이러한 구성 요소에 대해 SameSite을 사용할 수 없습니다. 대부분의 [OAuth](https://oauth.net/) 로그인은 요청 흐름의 차이로 인해 영향을 받지 않습니다.

`iframe`를 사용 하는 응용 프로그램은 `SameSite=Lax` 또는 `SameSite=Strict` 쿠키와 관련 된 문제가 발생할 수 있습니다. iframe은 사이트 간 시나리오로 처리 되기 때문입니다.

쿠키를 내보내는 각 ASP.NET 구성 요소는 SameSite가 적절 한지 결정 해야 합니다.

2019 .Net SameSite 업데이트를 설치한 후 응용 프로그램 문제에 대 한 [알려진 문제](#known) 를 참조 하세요.

## <a name="using-samesite-in-aspnet-472-and-48"></a>ASP.NET 4.7.2 및 4.8에서 SameSite 사용

.Net 4.7.2 및 4.8는 12 월 2019의 업데이트 출시 이후 SameSite에 대 한 [2019 초안 표준을](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) 지원 합니다. 개발자는 [SameSite 속성](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite)을 사용 하 여 SameSite 헤더의 값을 프로그래밍 방식으로 제어할 수 있습니다. `SameSite` 속성을 `Strict`, `Lax`또는 `None`로 설정 하면 해당 값이 쿠키를 사용 하 여 네트워크에 기록 됩니다. `(SameSiteMode)(-1)`와 동일 하 게 설정 하면 쿠키를 사용 하 여 네트워크에 SameSite 헤더를 포함 하지 않아야 함을 나타냅니다. 구성 파일의 [되어 속성](/dotnet/api/system.web.httpcookie.secure)또는 ' requireSSL '은 쿠키를 `Secure` 표시 하는 데 사용할 수 있습니다.

새 `HttpCookie` 인스턴스는 기본적으로 `SameSite=(SameSiteMode)(-1)` 및 `Secure=false`됩니다. 이러한 기본값은 `system.web/httpCookies` 구성 섹션에서 재정의할 수 있습니다. 여기서 문자열 `"Unspecified"` `(SameSiteMode)(-1)`에 대 한 간단한 구성 전용 구문입니다.

```xml
<configuration>
 <system.web>
  <httpCookies sameSite="[Strict|Lax|None|Unspecified]" requireSSL="[true|false]" />
 <system.web>
<configuration>
```

또한 ASP.Net는 이러한 기능에 대해 익명 인증, 폼 인증, 세션 상태 및 역할 관리와 같은 4 가지 특정 쿠키를 발급 합니다. 런타임에 가져온 이러한 쿠키의 인스턴스는 다른 되어 인스턴스와 마찬가지로 `SameSite` 및 `Secure` 속성을 사용 하 여 조작할 수 있습니다. 그러나 SameSite 표준의 패치워크 등장 때문에 이러한 4 가지 기능 쿠키에 대 한 구성 옵션은 일관 되지 않습니다. 다음은 관련 구성 섹션 및 특성입니다. 기본값은 다음과 같습니다. 기능에 대 한 `SameSite` 또는 `Secure` 관련 특성이 없으면이 기능은 위에 설명 된 `system.web/httpCookies` 섹션에 구성 된 기본값으로 대체 됩니다.

```xml
<configuration>
 <system.web>
  <anonymousIdentification cookieRequireSSL="false" /> <!-- No config attribute for SameSite -->
  <authentication>
   <forms cookieSameSite="Lax" requireSSL="false" />
  </authentication>
  <sessionState cookieSameSite="Lax" /> <!-- No config attribute for Secure -->
  <roleManager cookieRequireSSL="false" /> <!-- No config attribute for SameSite -->
 <system.web>
<configuration>
```  

**참고**: ' 지정 되지 않음 '은 현재 `system.web/httpCookies@sameSite`에만 사용할 수 있습니다. 이후 업데이트에서 이전에 표시 된 cookieSameSite 특성에 비슷한 구문을 추가 하려고 합니다. 코드의 `(SameSiteMode)(-1)` 설정은 여전히 이러한 쿠키의 인스턴스에서 작동 합니다. *

## <a name="history-and-changes"></a>기록 및 변경 내용

SameSite 지원은 [2016 초안 표준을](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)사용 하 여 .net 4.7.2에서 처음 구현 되었습니다.

2019 년 11 월 19 일 업데이트는 2016 표준에서 2019 standard로 업데이트 된 .NET 4.7.2 +입니다. 다른 버전의 Windows에 대 한 추가 업데이트가 곧 출시 됩니다. 자세한 내용은 <xref:samesite/kbs-samesite>을 참조하세요.

 SameSite 사양의 2019 초안:

* 는 이전 버전과 호환 **되지 않습니다** . 2016 초안. 자세한 내용은이 문서의 [이전 브라우저 지원](#sob) 을 참조 하세요.
* 기본적으로 `SameSite=Lax`로 처리 되는 쿠키를 지정 합니다.
* 교차 사이트 배달을 사용 하도록 설정 하기 위해 `SameSite=None`를 명시적으로 어설션하는 쿠키를 `Secure`으로 표시 해야 합니다.
* 는 위에 나열 된 KB에 설명 된 대로 발급 된 패치에 의해 지원 됩니다.
* 는 기본적으로 [2 월 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)에 [Chrome](https://chromestatus.com/feature/5088147346030592) 에서 사용 하도록 예약 됩니다. 브라우저에서 2019의이 표준으로 이동 하기 시작 했습니다.

<a name="known"><a/>

## <a name="known-issues"></a>알려진 문제

2016 및 2019 draft 사양이 호환 되지 않기 때문에 11 월 2019 .Net Framework 업데이트에서 일부 변경 내용이 적용 될 수 있습니다.

* 이제 세션 상태 및 폼 인증 쿠키가 지정 되지 않고 `Lax`으로 네트워크에 기록 됩니다.
  * 대부분의 앱은 `SameSite=Lax` 쿠키를 사용 하지만 `iframe`를 사용 하는 응용 프로그램 또는 응용 프로그램 전체에서 게시 되는 앱은 세션 상태나 폼 권한 부여 쿠키가 예상 대로 사용 되지 않는 것을 확인할 수 있습니다. 이를 해결 하려면 앞에서 설명한 대로 적절 한 구성 섹션에서 `cookieSameSite` 값을 변경 합니다.
* 코드 또는 구성에서 명시적으로 `SameSite=None`를 설정 하는 HttpCookies는 이전에 생략 된 것과 같은 값을 쿠키를 사용 하 여 작성 했습니다. 이로 인해 2016 초안 표준만 지 원하는 이전 브라우저에서 문제가 발생할 수 있습니다.
  * `SameSite=None` 쿠키를 사용 하 여 2019 draft standard를 지 원하는 브라우저를 대상으로 지정 하는 경우 `Secure` 표시 하거나 인식 하지 못할 수도 있습니다.
  * `SameSite=None`쓰지 않는 2016 동작으로 되돌리려면 앱 설정 `aspnet:SupressSameSiteNone=true`를 사용 합니다. 이는 앱의 모든 HttpCookies에 적용 됩니다.

### <a name="azure-app-servicesamesite-cookie-handling"></a>Azure App Service-SameSite 쿠키 처리

Azure App Service .Net 4.7.2 앱에서 SameSite 동작을 구성 하는 방법에 대 한 자세한 내용은 [Azure App Service-SameSite 쿠키 처리 및 .NET Framework 4.7.2 patch](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/) 를 참조 하세요.

<a name="sob"></a>

## <a name="supporting-older-browsers"></a>이전 브라우저 지원

2016 SameSite 표준에서는 알 수 없는 값을 `SameSite=Strict` 값으로 처리 해야 합니다. 2016 SameSite 표준을 지 원하는 이전 브라우저에서 액세스 한 앱은 `None`값으로 SameSite 속성을 가져오면 중단 될 수 있습니다. 웹 앱은 이전 브라우저를 지원 하려는 경우 브라우저 검색을 구현 해야 합니다. 사용자 에이전트 값이 매우 휘발성 이며 자주 변경 되기 때문에 ASP.NET는 브라우저 검색을 구현 하지 않습니다. <xref:HTTP.HttpCookie> 호출 사이트에서 다음 코드를 호출할 수 있습니다.

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet)]

위의 샘플에서 `MyUserAgentDetectionLib.DisallowsSameSiteNone` 사용자 에이전트가 SameSite `None`를 지원 하지 않는지 검색 하는 사용자 제공 라이브러리입니다. 다음 코드는 샘플 `DisallowsSameSiteNone` 메서드를 보여 줍니다.

> [!WARNING]
> 다음 코드는 데모용 으로만 사용할 수 있습니다.
> * 완료 되지 않은 것으로 간주 됩니다.
> * 유지 관리 되거나 지원 되지 않습니다.

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet2)]

## <a name="test-apps-for-samesite-problems"></a>SameSite 문제에 대 한 앱 테스트

타사 로그인을 통해와 같은 원격 사이트와 상호 작용 하는 앱은 다음 작업을 수행 해야 합니다.

* 여러 브라우저에서 상호 작용을 테스트 합니다.
* 이 문서에서 설명 [하는 브라우저 검색 및 완화](#sob) 를 적용 합니다.

새 SameSite 동작을 옵트인 (opt in) 할 수 있는 클라이언트 버전을 사용 하 여 웹 앱을 테스트 합니다. Chrome, Firefox 및 Chromium Edge 모두에는 테스트에 사용할 수 있는 새로운 옵트인 기능 플래그가 있습니다. 앱이 SameSite 패치를 적용 한 후 이전 클라이언트 버전, 특히 Safari를 사용 하 여 테스트 합니다. 자세한 내용은이 문서의 [이전 브라우저 지원](#sob) 을 참조 하세요.

### <a name="test-with-chrome"></a>Chrome으로 테스트

Chrome 78 +는 일시적인 완화를 제공 하기 때문에 잘못 된 결과를 제공 합니다. Chrome 78 + 임시 완화를 사용 하면 쿠키가 2 분 이내에 이전 될 수 있습니다. 적절 한 테스트 플래그가 설정 된 Chrome 76 또는 77은 보다 정확한 결과를 제공 합니다. 새 SameSite 동작을 테스트 하려면 `chrome://flags/#same-site-by-default-cookies` **설정**으로 전환 합니다. 이전 버전의 Chrome (75 및 아래)은 새 `None` 설정으로 인해 실패 하는 것으로 보고 됩니다. 이 문서의 [이전 브라우저 지원](#sob) 을 참조 하세요.

Google은 이전 chrome 버전을 사용할 수 없도록 설정 하지 않습니다. [Chromium 다운로드](https://www.chromium.org/getting-involved/download-chromium) 의 지침에 따라 이전 버전의 Chrome을 테스트 합니다. 이전 버전의 chrome을 검색 하 여 제공 된 링크에서 Chrome을 다운로드 **하지** 마세요.

* [Chromium 76 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [Chromium 74 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)

### <a name="test-with-safari"></a>Safari를 사용 하 여 테스트

Safari 12는 이전 초안을 엄격 하 게 구현 했으며 새 `None` 값이 쿠키에 있는 경우 실패 합니다. 이 문서에서 [이전 브라우저를 지 원하는](#sob) 브라우저 검색 코드를 통해 `None`를 방지할 수 있습니다. MSAL, ADAL 또는 사용 중인 라이브러리를 사용 하 여 Safari 12, Safari 13 및 WebKit 기반 OS 스타일 로그인을 테스트 합니다. 문제는 기본 OS 버전에 따라 달라집니다. OSX Mojave (10.14) 및 iOS 12는 새로운 SameSite 동작의 호환성 문제를 해결 하는 것으로 알려져 있습니다. OS를 OSX Catalina.properties (10.15) 또는 iOS 13로 업그레이드 하면 문제가 해결 됩니다. Safari에는 현재 새 사양 동작 테스트를 위한 옵트인 플래그가 없습니다.

### <a name="test-with-firefox"></a>Firefox로 테스트

새 표준에 대 한 Firefox 지원은 `network.cookie.sameSite.laxByDefault`기능 플래그를 사용 하 여 `about:config` 페이지에서 옵트인 하 여 버전 68 이상에서 테스트할 수 있습니다. 이전 버전의 Firefox와의 호환성 문제에 대 한 보고서가 없습니다.

### <a name="test-with-edge-browser"></a>Edge 브라우저를 사용 하 여 테스트

Edge는 이전 SameSite 표준을 지원 합니다. Edge 버전 44에는 새로운 표준과의 알려진 호환성 문제가 없습니다.

### <a name="test-with-edge-chromium"></a>Edge를 사용 하 여 테스트 (Chromium)

SameSite 플래그는 `edge://flags/#same-site-by-default-cookies` 페이지에 설정 되어 있습니다. Edge Chromium에서 호환성 문제가 검색 되지 않았습니다.

### <a name="test-with-electron"></a>전자로 테스트

Electron 버전에는 이전 버전의 Chromium이 포함되어 있습니다. 예를 들어 팀에서 사용 하는 전자의 버전은 Chromium 66 이며,이는 이전 동작을 보여 주는 것입니다. 제품에서 사용 하는 전자 제품 버전으로 고유한 호환성 테스트를 수행 해야 합니다. 다음 섹션에서 [이전 브라우저 지원](#sob) 을 참조 하세요.

## <a name="additional-resources"></a>추가 리소스

* [ASP.NET 및 ASP.NET Core의 예정 된 SameSite 쿠키 변경 내용](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [Chromium 블로그: 개발자: 새 SameSite를 사용할 준비가 되었습니다. 보안 쿠키 설정](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [SameSite 쿠키 설명](https://web.dev/samesite-cookies-explained/)
