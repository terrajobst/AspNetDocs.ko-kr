---
title: ASP.NET에서 SameSite 쿠키 사용
author: rick-anderson
description: 를 사용 하 여 ASP.NET에서 쿠키를 SameSite 하는 방법을 알아봅니다.
ms.author: riande
ms.date: 2/15/2019
uid: samesite/system-web-samesite
ms.openlocfilehash: edb368910b24be2d042afe3c19ffa1fb23245443
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455709"
---
# <a name="work-with-samesite-cookies-in-aspnet"></a>ASP.NET에서 SameSite 쿠키 사용

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

SameSite은 CSRF (교차 사이트 요청 위조) 공격에 대 한 보호를 제공 하도록 설계 된 [IETF](https://ietf.org/about/) 초안 표준입니다. 원래 [2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07)에서는 초안 표준이 [2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)에서 업데이트 되었습니다. 업데이트 된 표준은 이전 표준과 호환 되지 않으며 다음과 같은 가장 눈에 띄는 차이점이 있습니다.

* SameSite 헤더가 없는 쿠키는 기본적으로 `SameSite=Lax`으로 처리 됩니다.
* 사이트 간 쿠키 사용을 허용 하려면 `SameSite=None`를 사용 해야 합니다.
* `SameSite=None` 어설션 하는 쿠키도 `Secure`로 표시 되어야 합니다.
* [`<iframe>`](https://developer.mozilla.org/docs/Web/HTML/Element/iframe) 를 사용 하는 응용 프로그램은 `<iframe>` 사이트 간 시나리오로 처리 되기 때문에 `sameSite=Lax` 또는 `sameSite=Strict` 쿠키와 관련 된 문제가 발생할 수 있습니다.
* `SameSite=None` 값은 [2016 표준](https://tools.ietf.org/html/draft-west-first-party-cookies-07) 에서 허용 되지 않으며 일부 구현에서는 이러한 쿠키를 `SameSite=Strict`로 처리 합니다. 이 문서의 [이전 브라우저 지원](#sob) 을 참조 하세요.

`SameSite=Lax` 설정은 대부분의 응용 프로그램 쿠키에 대해 작동 합니다. Oidc ( [Openid connect Connect](https://openid.net/connect/) )와 같은 일부 형태의 인증 및 [ws-federation](https://auth0.com/docs/protocols/ws-fed) 은 게시 기반 리디렉션에 대해 기본적으로 사용 됩니다. 사후 기반 리디렉션은 SameSite 브라우저 보호를 트리거하고 이러한 구성 요소에 대해 SameSite을 사용할 수 없습니다. 대부분의 [OAuth](https://oauth.net/) 로그인은 요청 흐름의 차이로 인해 영향을 받지 않습니다.

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

[!INCLUDE[](~/includes/MTcomments.md)]

<a name="retargeting"></a>

### <a name="retarget-net-apps"></a>.NET 앱 대상을 변경 합니다.

.NET 4.7.2 이상을 대상으로 하려면:

* *Web.config* 에 다음이 포함 되어 있는지 확인 합니다.  <!-- review, I removed `debug="true"` -->

  ```xml
  <system.web>
    <compilation targetFramework="4.7.2"/>
    <httpRuntime targetFramework="4.7.2"/>
  </system.web>

* Verify the project file contains the correct [TargetFrameworkVersion](/visualstudio/msbuild/msbuild-target-framework-and-target-platform?view=vs-2019):

  ```xml
  <TargetFrameworkVersion>v4.7.2</TargetFrameworkVersion>
  ```

  자세한 내용은 [.Net 마이그레이션 가이드](/dotnet/framework/migration-guide/) 를 참조 하세요.

* 프로젝트의 NuGet 패키지가 올바른 프레임 워크 버전을 대상으로 하는지 확인 합니다. 다음과 같이 *패키지 .config* 파일을 검사 하 여 올바른 프레임 워크 버전을 확인할 수 있습니다.

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <packages>
    <package id="Microsoft.AspNet.Mvc" version="5.2.7" targetFramework="net472" />
    <package id="Microsoft.ApplicationInsights" version="2.4.0" targetFramework="net451" />
  </packages>
  ```

  위의 *패키지 .config* 파일에서 `Microsoft.ApplicationInsights` 패키지는 다음과 같습니다.
    * 는 .NET 4.5.1을 대상으로 합니다.
    * 프레임 워크 대상을 대상으로 하는 업데이트 된 패키지가 있는 경우 `targetFramework` 특성이 `net472` 업데이트 되어야 합니다.

<a name="nope"></a>

### <a name="net-versions-earlier-than-472"></a>4\.7.2 보다 이전 버전의 .NET

Microsoft는 동일한 사이트 쿠키 특성을 4.7.2 하는 .NET 버전을 지원 하지 않습니다. 다음을 수행 하는 신뢰할 수 있는 방법이 없습니다.

* 브라우저 버전에 따라 특성이 올바르게 작성 되었는지 확인 합니다.
* 이전 프레임 워크 버전에서 인증 및 세션 쿠키를 가로채 고 조정 합니다.

### <a name="december-patch-behavior-changes"></a>12 월 패치 동작 변경 내용

.NET Framework의 특정 동작 변경 내용은 `SameSite` 속성이 `None` 값을 해석 하는 방법입니다.

* `None` 패치 이전에는 다음을 의미 합니다.
  * 특성을 전혀 내보내지 않습니다.
* 패치 후:
  * `None`값은 "`None`값을 사용 하 여 특성을 내보냅니다."를 의미 합니다.
  * `(SameSiteMode)(-1)` `SameSite` 값을 설정 하면 특성을 내보내지 않습니다.

폼 인증 및 세션 상태 쿠키의 기본 SameSite 값이 `None`에서 `Lax`로 변경 되었습니다.

### <a name="summary-of-change-impact-on-browsers"></a>브라우저에 대 한 변경 내용 영향 요약

패치를 설치 하 고 `SameSite.None`를 사용 하 여 쿠키를 발급 하는 경우 다음 두 가지 중 하나가 발생 합니다.
* Chrome v80는 새 구현에 따라이 쿠키를 처리 하며 쿠키에 대해 동일한 사이트 제한을 적용 하지 않습니다.
* 새 구현을 지원 하도록 업데이트 되지 않은 브라우저는 이전 구현을 따릅니다. 이전 구현에는 다음이 표시 됩니다.
  * 이해할 수 없는 값이 표시 되 면이를 무시 하 고 엄격한 동일한 사이트 제한으로 전환 합니다.

따라서 앱이 Chrome에서 중단 되거나 다른 많은 위치에서 중단 됩니다.

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

2016 SameSite 표준에서는 알 수 없는 값을 `SameSite=Strict` 값으로 처리 해야 합니다. 2016 SameSite 표준을 지 원하는 이전 브라우저에서 액세스 한 앱은 `None`값으로 SameSite 속성을 가져오면 중단 될 수 있습니다. 웹 앱은 이전 브라우저를 지원 하려는 경우 브라우저 검색을 구현 해야 합니다. 사용자 에이전트 값이 매우 휘발성 이며 자주 변경 되기 때문에 ASP.NET는 브라우저 검색을 구현 하지 않습니다.

문제를 해결 하는 Microsoft의 접근 방식은 브라우저 검색 구성 요소를 구현 하 여 브라우저에서 지원 하지 않는 것으로 알려진 경우 쿠키에서 `sameSite=None` 특성을 제거 하는 것입니다. Google의 충고는 두 쿠키를 발급 하는 것으로, 하나는 새 특성을, 하나는 특성이 없는 쿠키를 사용 하는 것입니다. 하지만 Google의 조언을 제한적으로 고려 합니다. 일부 브라우저, 특히 모바일 브라우저는 한 사이트의 쿠키 수에 대 한 제한이 매우 적거나 도메인 이름이 보낼 수 있습니다. 여러 쿠키를 전송 하는 경우, 특히 인증 쿠키와 같은 큰 쿠키는 모바일 브라우저 제한에 신속 하 게 도달 하 여 진단 하 고 수정 하기 어려운 앱 오류를 일으킬 수 있습니다. 또한 두 번째 쿠키 방식을 사용 하도록 업데이트 되지 않은 타사 코드 및 구성 요소에 대 한 많은 에코 시스템이 있습니다.

[이 GitHub 리포지토리의]() 샘플 프로젝트에 사용 되는 브라우저 검색 코드는 두 개의 파일에 포함 되어 있습니다.

* [C#SameSiteSupport.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.cs)
* [VB SameSiteSupport](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.vb)

이러한 검색은 가장 일반적인 브라우저 에이전트로, 2016 표준을 지원 하 고 특성을 완전히 제거 해야 합니다. 완전 한 구현이 아닙니다.

* 앱에서 테스트 사이트가 아닌 브라우저를 볼 수 있습니다.
* 사용자 환경에 필요한 경우 검색을 추가할 준비를 해야 합니다.

검색을 연결 하는 방법은 사용 중인 .NET 및 웹 프레임 워크의 버전에 따라 다릅니다. <xref:HTTP.HttpCookie> 호출 사이트에서 다음 코드를 호출할 수 있습니다.

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet)]

다음 ASP.NET 4.7.2 SameSite cookie 항목을 참조 하세요.

* [C#MVC](xref:samesite/csMVC)
* [C#WebForms](xref:samesite/CSharpWebForms)
* [VB WebForms](xref:samesite/vbWF)
* [VB MVC](xref:samesite/vbMVC)
<!--
* <xref:samesite/csMVC>
* <xref:samesite/CSharpWebForms>
* <xref:samesite/vbWF>
* <xref:samesite/vbMVC>
-->

### <a name="ensuring-your-site-redirects-to-https"></a>사이트가 HTTPS로 리디렉션 되는지 확인

ASP.NET 4. x, WebForms 및 MVC의 경우 [IIS의 URL 재작성](/iis/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module) 기능을 사용 하 여 모든 요청을 HTTPS로 리디렉션할 수 있습니다. 다음 XML에서는 샘플 규칙을 보여 줍니다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <rule name="Redirect to https" stopProcessing="true">
          <match url="(.*)"/>
          <conditions>
            <add input="{HTTPS}" pattern="Off"/>
            <add input="{REQUEST_METHOD}" pattern="^get$|^head$" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" redirectType="Permanent"/>
        </rule>
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

[IIS URL 재작성](https://www.iis.net/downloads/microsoft/url-rewrite) 의 온-프레미스 설치는 설치 해야 할 수 있는 선택적 기능입니다.

## <a name="test-apps-for-samesite-problems"></a>SameSite 문제에 대 한 앱 테스트

지원 되는 브라우저를 사용 하 여 앱을 테스트 하 고 쿠키를 포함 하는 시나리오를 진행 해야 합니다. 쿠키 시나리오는 일반적으로 다음을 포함 합니다.

* 로그인 양식
* Facebook, Azure AD, OAuth 및 OIDC와 같은 외부 로그인 메커니즘
* 다른 사이트의 요청을 수락 하는 페이지
* Iframe에 포함 되도록 설계 된 앱의 페이지

앱에서 쿠키가 올바르게 생성, 유지 및 삭제 되었는지 확인 해야 합니다.

타사 로그인을 통해와 같은 원격 사이트와 상호 작용 하는 앱은 다음 작업을 수행 해야 합니다.

* 여러 브라우저에서 상호 작용을 테스트 합니다.
* 이 문서에서 설명 [하는 브라우저 검색 및 완화](#sob) 를 적용 합니다.

새 SameSite 동작을 옵트인 (opt in) 할 수 있는 클라이언트 버전을 사용 하 여 웹 앱을 테스트 합니다. Chrome, Firefox 및 Chromium Edge 모두에는 테스트에 사용할 수 있는 새로운 옵트인 기능 플래그가 있습니다. 앱이 SameSite 패치를 적용 한 후 이전 클라이언트 버전, 특히 Safari를 사용 하 여 테스트 합니다. 자세한 내용은이 문서의 [이전 브라우저 지원](#sob) 을 참조 하세요.

### <a name="test-with-chrome"></a>Chrome으로 테스트

Chrome 78 +는 일시적인 완화를 제공 하기 때문에 잘못 된 결과를 제공 합니다. Chrome 78 + 임시 완화를 사용 하면 쿠키가 2 분 이내에 이전 될 수 있습니다. 적절 한 테스트 플래그가 설정 된 Chrome 76 또는 77은 보다 정확한 결과를 제공 합니다. 새 SameSite 동작을 테스트 하려면 `chrome://flags/#same-site-by-default-cookies` **설정**으로 전환 합니다. 이전 버전의 Chrome (75 및 아래)은 새 `None` 설정으로 인해 실패 하는 것으로 보고 됩니다. 이 문서의 [이전 브라우저 지원](#sob) 을 참조 하세요.

Google은 이전 chrome 버전을 사용할 수 없도록 설정 하지 않습니다. [Chromium 다운로드](https://www.chromium.org/getting-involved/download-chromium) 의 지침에 따라 이전 버전의 Chrome을 테스트 합니다. 이전 버전의 chrome을 검색 하 여 제공 된 링크에서 Chrome을 다운로드 **하지** 마세요.

* [Chromium 76 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [Chromium 74 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)
* 64 비트 버전의 Windows를 사용 하지 않는 경우 [OmahaProxy viewer](https://omahaproxy.appspot.com/) 를 사용 하 여 [Chromium에서 제공](https://www.chromium.org/getting-involved/download-chromium)하는 지침을 사용 하 여 Chrome 74 (v 74.0.3729.108)에 해당 하는 Chromium 분기를 조회할 수 있습니다.

#### <a name="test-with-chrome-80"></a>Chrome 80 이상으로 테스트

새 특성을 지 원하는 Chrome 버전을 [다운로드](https://www.google.com/chrome/) 합니다. 작성 시점에 현재 버전은 Chrome 80입니다. Chrome 80에는 새 동작을 사용 하도록 설정 `chrome://flags/#same-site-by-default-cookies` 플래그가 필요 합니다. SameSite 특성을 사용 하지 않는 쿠키의 예정 된 동작을 테스트 하려면 (`chrome://flags/#cookies-without-same-site-must-be-secure`)도 사용 하도록 설정 해야 합니다. Chrome 80는 특정 요청에 대 한 시간 제한 유예 기간을 사용 하는 경우를 제외 하 고는 특성이 없는 쿠키를 `SameSite=Lax`으로 처리 하는 스위치를 대상으로 합니다. 시간이 지정 된 유예 기간을 사용 하지 않도록 설정 하려면 다음 명령줄 인수를 사용 하 여 Chrome 80을 시작할 수 있습니다.

`--enable-features=SameSiteDefaultChecksMethodRigorously`

Chrome 80에는 브라우저 콘솔에 누락 된 sameSite 특성에 대 한 경고 메시지가 있습니다. F12 키를 사용 하 여 브라우저 콘솔을 엽니다.

### <a name="test-with-safari"></a>Safari를 사용 하 여 테스트

Safari 12는 이전 초안을 엄격 하 게 구현 했으며 새 `None` 값이 쿠키에 있는 경우 실패 합니다. 이 문서에서 [이전 브라우저를 지 원하는](#sob) 브라우저 검색 코드를 통해 `None`를 방지할 수 있습니다. MSAL, ADAL 또는 사용 중인 라이브러리를 사용 하 여 Safari 12, Safari 13 및 WebKit 기반 OS 스타일 로그인을 테스트 합니다. 문제는 기본 OS 버전에 따라 달라집니다. OSX Mojave (10.14) 및 iOS 12는 새로운 SameSite 동작의 호환성 문제를 해결 하는 것으로 알려져 있습니다. OS를 OSX Catalina.properties (10.15) 또는 iOS 13로 업그레이드 하면 문제가 해결 됩니다. Safari에는 현재 새 사양 동작 테스트를 위한 옵트인 플래그가 없습니다.

### <a name="test-with-firefox"></a>Firefox로 테스트

새 표준에 대 한 Firefox 지원은 `network.cookie.sameSite.laxByDefault`기능 플래그를 사용 하 여 `about:config` 페이지에서 옵트인 하 여 버전 68 이상에서 테스트할 수 있습니다. 이전 버전의 Firefox와의 호환성 문제에 대 한 보고서가 없습니다.

### <a name="test-with-edge-legacy-browser"></a>Edge (레거시) 브라우저를 사용 하 여 테스트

Edge는 이전 SameSite 표준을 지원 합니다. Edge 버전 44 이상에는 새 표준에 대 한 알려진 호환성 문제가 없습니다.

### <a name="test-with-edge-chromium"></a>Edge를 사용 하 여 테스트 (Chromium)

SameSite 플래그는 `edge://flags/#same-site-by-default-cookies` 페이지에 설정 되어 있습니다. Edge Chromium에서 호환성 문제가 검색 되지 않았습니다.

### <a name="test-with-electron"></a>전자로 테스트

Electron 버전에는 이전 버전의 Chromium이 포함되어 있습니다. 예를 들어 팀에서 사용 하는 전자의 버전은 Chromium 66 이며,이는 이전 동작을 보여 주는 것입니다. 제품에서 사용 하는 전자 제품 버전으로 고유한 호환성 테스트를 수행 해야 합니다. [이전 브라우저 지원](#sob)을 참조 하세요.

## <a name="reverting-samesite-patches"></a>SameSite 패치 되돌리기

.NET Framework 앱의 업데이트 된 sameSite 동작을 `None`값에 대 한 sameSite 특성을 내보내지 않는 이전 동작으로 되돌릴 수 있습니다. 그런 다음 인증 및 세션 쿠키를 되돌려 값을 내보내지 않습니다. 이는 표준에 대 한 변경 내용을 지 원하는 브라우저를 사용 하 여 사용자에 대 한 외부 POST 요청 또는 인증을 중단 하기 때문에 *매우 임시 수정*으로 표시 되어야 합니다.

### <a name="reverting-net-472-behavior"></a>.NET 4.7.2 동작 되돌리기

다음 구성 설정을 포함 하도록 *web.config* 를 업데이트 합니다.

```xml
<configuration> 
  <appSettings>
    <add key="aspnet:SuppressSameSiteNone" value="true" />
  </appSettings>
 
  <system.web> 
    <authentication> 
      <forms cookieSameSite="None" /> 
    </authentication> 
    <sessionState cookieSameSite="None" /> 
  </system.web> 
</configuration>
```

## <a name="additional-resources"></a>추가 리소스

* [ASP.NET 및 ASP.NET Core의 예정 된 SameSite 쿠키 변경 내용](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [Chromium 블로그: 개발자: 새 SameSite를 사용할 준비가 되었습니다. 보안 쿠키 설정](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [SameSite 쿠키 설명](https://web.dev/samesite-cookies-explained/)
* [Chrome 업데이트](https://www.chromium.org/updates/same-site)
* [.NET SameSite 패치](/aspnet/samesite/kbs-samesite)
* [Azure 웹 응용 프로그램 동일한 사이트 정보](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/)
* [Azure ActiveDirectory 동일한 사이트 정보](/azure/active-directory/develop/howto-handle-samesite-cookie-changes-chrome-browser)
