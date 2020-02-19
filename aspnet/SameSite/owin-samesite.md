---
title: SameSite 쿠키 및 OWIN (Open Web Interface for .NET) 사용
author: rick-anderson
description: SameSite 쿠키 및 OWIN (Open Web Interface for .NET) 사용
ms.author: riande
ms.date: 12/6/2019
uid: owin-samesite
ms.openlocfilehash: a3353fd0f0332899aaba26b83aea0ff7c3a6d19b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455739"
---
# <a name="samesite-cookies-and-the-open-web-interface-for-net-owin"></a>SameSite 쿠키 및 OWIN (Open Web Interface for .NET)

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

`SameSite`은 CSRF (교차 사이트 요청 위조) 공격에 대 한 보호를 제공 하도록 설계 된 [IETF](https://ietf.org/about/) 초안입니다. [SameSite 2019 초안](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00):

* 에서는 기본적으로 쿠키를 `SameSite=Lax`로 처리 합니다.
* 사이트 간 배달을 가능 하 게 하기 위해 `SameSite=None`를 명시적으로 어설션하는 쿠키는 `Secure`으로 표시 되어야 합니다.

`Lax` 대부분의 앱 쿠키에 대해 작동 합니다. Oidc ( [Openid connect Connect](https://openid.net/connect/) )와 같은 일부 형태의 인증 및 [ws-federation](https://auth0.com/docs/protocols/ws-fed) 은 게시 기반 리디렉션에 대해 기본적으로 사용 됩니다. 사후 기반 리디렉션은 이러한 구성 요소에 대해 `SameSite`를 사용할 수 없도록 `SameSite` 브라우저 보호를 트리거합니다. 대부분의 [OAuth](https://oauth.net/) 로그인은 요청 흐름의 차이로 인해 영향을 받지 않습니다. 다른 모든 구성 요소는 기본적으로 `SameSite` 설정 **되지** 않으며 클라이언트 기본 동작 (이전 또는 새)을 사용 합니다.

`None` 매개 변수를 사용 하면 이전 [2016 초안 표준](https://tools.ietf.org/html/draft-west-first-party-cookies-07) (예: iOS 12)을 구현한 클라이언트에서 호환성 문제가 발생 합니다. 이 문서의 [이전 브라우저 지원](#sob) 을 참조 하세요.

쿠키를 내보내는 각 OWIN 구성 요소는 `SameSite` 적절 한지 결정 해야 합니다.

이 문서의 ASP.NET 4.x 버전은 <xref:samesite/system-web-samesite>를 참조 하세요.

## <a name="api-usage-with-samesite"></a>SameSite를 사용 하는 API 사용

`Microsoft.Owin`에는 고유한 `SameSite` 구현이 있습니다.

* 이는 `System.Web`의 항목에 직접적으로 종속 되지 않습니다.
* `SameSite`는 `Microsoft.Owin` 패키지, .NET 4.5 이상에 의해 가능 모든 버전에서 작동 합니다.
* [SystemWebCookieManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebCookieManager.cs) 구성 요소만 `System.Web` `HttpCookie` 클래스와 직접적으로 상호 작용 합니다.

`SystemWebCookieManager`는 .NET 4.7.2 `System.Web` Api에 따라 `SameSite` 지원을 사용 하도록 설정 하 고 패치를 사용 하 여 동작을 변경 합니다.

`SystemWebCookieManager`를 사용 하는 이유는 [OWIN 및 system.web response 쿠키 통합 문제](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues)에 설명 되어 있습니다. `System.Web`에서 실행 하는 경우 `SystemWebCookieManager` 권장 됩니다.

다음 코드는 `Lax``SameSite`를 설정 합니다.

```csharp
owinContext.Response.Cookies.Append("My Key", "My Value", new CookieOptions()
{
    SameSite = SameSiteMode.Lax
});
```

다음 Api는 `SameSite`을 사용 합니다.

* [Owin. SameSiteMode](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin/SameSiteMode.cs)
* [CookieOptions. SameSite](xref:Microsoft.AspNetCore.Http.CookieOptions.SameSite)
* [은 cookieauthenticationoptions.authenticationtype 클래스](/previous-versions/aspnet/dn385599(v%3Dvs.113)) <!-- CookieAuthenticationOptions.CookieSameSite not published -->
* [은 cookieauthenticationoptions.authenticationtype. CookieSameSite](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.Cookies/CookieAuthenticationOptions.cs#L68-#L72)
* [ICookieManager](/previous-versions/aspnet/dn800238(v%3Dvs.113))
* [SystemWebCookieManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebCookieManager.cs)
* [SystemWebChunkingCookieManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebChunkingCookieManager.cs)
* [은 cookieauthenticationoptions.authenticationtype. CookieManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.Cookies/CookieAuthenticationOptions.cs#L143-#AL148)
* [OpenIdConnectAuthenticationOptions. CookieManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.OpenIdConnect/OpenIdConnectAuthenticationOptions.cs#L315-#L318)

## <a name="history-and-changes"></a>기록 및 변경 내용

[Owin](https://www.nuget.org/packages/Microsoft.Owin/) 는 [`SameSite` 2016 초안 표준을](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)지원 하지 않습니다.

[SameSite 2019 초안](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) 에 대 한 지원은 `Microsoft.Owin` 4.1.0 이상 에서만 사용할 수 있습니다. 이전 버전에 대 한 패치는 없습니다.

`SameSite` 사양의 2019 초안:

* 는 이전 버전과 호환 **되지 않습니다** . 2016 초안. 자세한 내용은이 문서의 [이전 브라우저 지원](#sob) 을 참조 하세요.
* 기본적으로 `SameSite=Lax`로 처리 되는 쿠키를 지정 합니다.
* 교차 사이트 배달을 사용 하도록 설정 하기 위해 `SameSite=None`를 명시적으로 어설션하는 쿠키를 `Secure`으로 표시 해야 합니다. `None`은 옵트아웃 (opt out) 할 새 항목입니다.
* 는 기본적으로 [2 월 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)에 [Chrome](https://chromestatus.com/feature/5088147346030592) 에서 사용 하도록 예약 됩니다. 브라우저에서 2019의이 표준으로 이동 하기 시작 했습니다.
* 는 KB 문서에 설명 된 대로 발급 된 패치에 의해 지원 됩니다. 자세한 내용은 <xref:samesite/kbs-samesite>을 참조하세요.

<a name="sob"></a>

## <a name="supporting-older-browsers"></a>이전 브라우저 지원

2016 `SameSite` 표준에서는 알 수 없는 값을 `SameSite=Strict` 값으로 처리 해야 합니다. 2016 `SameSite` 표준을 지 원하는 이전 브라우저에서 액세스 한 앱은 `None`값을 가진 `SameSite` 속성을 가져오면 중단 될 수 있습니다. 웹 앱은 이전 브라우저를 지원 하려는 경우 브라우저 검색을 구현 해야 합니다. 사용자 에이전트 값이 매우 휘발성 이며 자주 변경 되기 때문에 ASP.NET는 브라우저 검색을 구현 하지 않습니다. [ICookieManager](/previous-versions/aspnet/dn800238(v%3Dvs.113)) 의 확장 지점은 사용자 에이전트 특정 논리를 연결 하는 것을 허용 합니다.
<!-- https://docs.microsoft.com/previous-versions/aspnet/dn800238(v%3Dvs.113) -->

`Startup.Configuration`에서 다음과 유사한 코드를 추가 합니다.

[!code-csharp[](sample/Startup1.cs?name=snippet)]

위의 코드에는 .NET 4.7.2 이상 `SameSite` 패치가 필요 합니다.

다음 코드는 `SameSiteCookieManager`의 구현 예를 보여 줍니다.

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet)]

위의 샘플에서 `DisallowsSameSiteNone`은 `CheckSameSite` 메서드에서 호출 됩니다. `DisallowsSameSiteNone`은 사용자 에이전트가 `SameSite` `None`를 지원 하지 않는지 여부를 검색 하는 사용자 방법입니다.

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet3&highlight=4)]

다음 코드는 샘플 `DisallowsSameSiteNone` 메서드를 보여 줍니다.

> [!WARNING]
> 다음 코드는 데모용 으로만 사용할 수 있습니다.
> * 완료 되지 않은 것으로 간주 됩니다.
> * 유지 관리 되거나 지원 되지 않습니다.

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet2)]

## <a name="test-apps-for-samesite-problems"></a>SameSite 문제에 대 한 앱 테스트

타사 로그인을 통해와 같은 원격 사이트와 상호 작용 하는 앱은 다음 작업을 수행 해야 합니다.

* 여러 브라우저에서 상호 작용을 테스트 합니다.
* 이 문서에서 설명 [하는 브라우저 검색 및 완화](#sob) 를 적용 합니다.

새 `SameSite` 동작을 옵트인 (opt in) 할 수 있는 클라이언트 버전을 사용 하 여 웹 앱을 테스트 합니다. Chrome, Firefox 및 Chromium Edge 모두에는 테스트에 사용할 수 있는 새로운 옵트인 기능 플래그가 있습니다. 앱이 `SameSite` 패치를 적용 한 후 이전 클라이언트 버전, 특히 Safari를 사용 하 여 테스트 합니다. 자세한 내용은이 문서의 [이전 브라우저 지원](#sob) 을 참조 하세요.

### <a name="test-with-chrome"></a>Chrome으로 테스트

Chrome 78 +는 일시적인 완화를 제공 하기 때문에 잘못 된 결과를 제공 합니다. Chrome 78 + 임시 완화를 사용 하면 쿠키가 2 분 이내에 이전 될 수 있습니다. 적절 한 테스트 플래그가 설정 된 Chrome 76 또는 77은 보다 정확한 결과를 제공 합니다. 새 `SameSite` 동작을 테스트 하려면 `chrome://flags/#same-site-by-default-cookies`를 **사용**으로 전환 합니다. 이전 버전의 Chrome (75 및 아래)은 새 `None` 설정으로 인해 실패 하는 것으로 보고 됩니다. 이 문서의 [이전 브라우저 지원](#sob) 을 참조 하세요.

Google은 이전 chrome 버전을 사용할 수 없도록 설정 하지 않습니다. [Chromium 다운로드](https://www.chromium.org/getting-involved/download-chromium) 의 지침에 따라 이전 버전의 Chrome을 테스트 합니다. 이전 버전의 chrome을 검색 하 여 제공 된 링크에서 Chrome을 다운로드 **하지** 마세요.

* [Chromium 76 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [Chromium 74 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)

### <a name="test-with-safari"></a>Safari를 사용 하 여 테스트

Safari 12는 이전 초안을 엄격 하 게 구현 했으며 새 `None` 값이 쿠키에 있는 경우 실패 합니다. 이 문서에서 [이전 브라우저를 지 원하는](#sob) 브라우저 검색 코드를 통해 `None`를 방지할 수 있습니다. MSAL, ADAL 또는 사용 중인 라이브러리를 사용 하 여 Safari 12, Safari 13 및 WebKit 기반 OS 스타일 로그인을 테스트 합니다. 문제는 기본 OS 버전에 따라 달라집니다. OSX Mojave (10.14) 및 iOS 12는 새로운 `SameSite` 동작의 호환성 문제를 해결 하는 것으로 알려져 있습니다. OS를 OSX Catalina.properties (10.15) 또는 iOS 13로 업그레이드 하면 문제가 해결 됩니다. Safari에는 현재 새 사양 동작 테스트를 위한 옵트인 플래그가 없습니다.

### <a name="test-with-firefox"></a>Firefox로 테스트

새 표준에 대 한 Firefox 지원은 `network.cookie.sameSite.laxByDefault`기능 플래그를 사용 하 여 `about:config` 페이지에서 옵트인 하 여 버전 68 이상에서 테스트할 수 있습니다. 이전 버전의 Firefox와의 호환성 문제에 대 한 보고서가 없습니다.

### <a name="test-with-edge-browser"></a>Edge 브라우저를 사용 하 여 테스트

Edge는 이전 `SameSite` 표준을 지원 합니다. Edge 버전 44에는 새로운 표준과의 알려진 호환성 문제가 없습니다.

### <a name="test-with-edge-chromium"></a>Edge를 사용 하 여 테스트 (Chromium)

`edge://flags/#same-site-by-default-cookies` 페이지에 `SameSite` 플래그가 설정 됩니다. Edge Chromium에서 호환성 문제가 검색 되지 않았습니다.

### <a name="test-with-electron"></a>전자로 테스트

Electron 버전에는 이전 버전의 Chromium이 포함되어 있습니다. 예를 들어 팀에서 사용 하는 전자의 버전은 Chromium 66 이며,이는 이전 동작을 보여 주는 것입니다. 제품에서 사용 하는 전자 제품 버전으로 고유한 호환성 테스트를 수행 해야 합니다. 다음 섹션에서 [이전 브라우저 지원](#sob) 을 참조 하세요.

## <a name="additional-resources"></a>추가 리소스

* [Chromium 블로그: 개발자: 새 SameSite를 사용할 준비가 되었습니다. 보안 쿠키 설정](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [SameSite 쿠키 설명](https://web.dev/samesite-cookies-explained/)
* [OWIN 및 System.web 응답 쿠키 통합 문제](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues)
