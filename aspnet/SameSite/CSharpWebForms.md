---
title: ASP.NET 4.7.2 C# WebForms에 대 한 SameSite cookie 샘플
author: blowdart
description: ASP.NET 4.7.2 C# WebForms에 대 한 SameSite cookie 샘플
ms.author: riande
ms.date: 2/15/2019
uid: samesite/CSharpWebForms
ms.openlocfilehash: 50d4745eca5954275abaa59dab726e7cf7ea193f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422255"
---
# <a name="samesite-cookie-sample-for-aspnet-472-c-webforms"></a>ASP.NET 4.7.2 C# WebForms에 대 한 SameSite cookie 샘플

.NET Framework 4.7는 [SameSite](https://www.owasp.org/index.php/SameSite) 특성에 대 한 기본 제공 지원을 제공 하지만 원래 표준을 준수 합니다.
패치 된 동작이 `SameSite.None`의 의미를 변경 하 여 값을 전혀 내보내지 않고 `None`값으로 특성을 내보냅니다. 값을 내보내지 않으려면 쿠키의 `SameSite` 속성을-1로 설정 하면 됩니다.

## <a name="sampleCode"></a>SameSite 특성 작성

다음은 쿠키에 SameSite 특성을 작성 하는 방법의 예입니다.

```c#
// Create the cookie
HttpCookie sameSiteCookie = new HttpCookie("SameSiteSample");

// Set a value for the cookie
sameSiteCookie.Value = "sample";

// Set the secure flag, which Chrome's changes will require for SameSite none.
// Note this will also require you to be running on HTTPS
sameSiteCookie.Secure = true;

// Set the cookie to HTTP only which is good practice unless you really do need
// to access it client side in scripts.
sameSiteCookie.HttpOnly = true;

// Add the SameSite attribute, this will emit the attribute with a value of none.
// To not emit the attribute at all set the SameSite property to -1.
sameSiteCookie.SameSite = SameSiteMode.None;

// Add the cookie to the response cookie collection
Response.Cookies.Add(sameSiteCookie);
```

[!INCLUDE[](~/includes/MTcomments.md)]

폼 인증 쿠키의 기본 sameSite 특성은의 폼 인증 설정의 `cookieSameSite` 매개 변수에 설정 됩니다 `web.config` 

```xml
<system.web>
  <authentication mode="Forms">
    <forms name=".ASPXAUTH" loginUrl="~/" cookieSameSite="None" requireSSL="true">
    </forms>
  </authentication>
</system.web>
```

세션 상태에 대 한 기본 sameSite 특성도 `web.config`에서 세션 설정의 ' cookieSameSite ' 매개 변수에 설정 됩니다.

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

.NET에 대 한 11 월 2019 업데이트는 가장 호환성이 높은 설정 `lax` 폼 인증 및 세션에 대 한 기본 설정을 변경 했습니다. 그러나 iframe에 페이지를 포함 하는 경우이 설정을 없음으로 되돌린 다음 아래 표시 된 [가로채기](#interception) 코드를 추가 하 여 브라우저 기능에 따라 `none` 동작을 조정 해야 할 수 있습니다.

### <a name="running-the-sample"></a>샘플 실행

샘플 프로젝트를 실행 하는 경우 초기 페이지에서 브라우저 디버거를 로드 하 고이를 사용 하 여 사이트에 대 한 쿠키 컬렉션을 봅니다.
Edge 및 Chrome에서이 작업을 수행 하려면 `F12`를 클릭 한 다음 `Application` 탭을 선택 하 고 `Storage` 섹션의 `Cookies` 옵션 아래에서 사이트 URL을 클릭 합니다.

![브라우저 디버거 쿠키 목록](sample/img/BrowserDebugger.png)

위의 이미지에서 볼 수 있습니다. 예를 들어 "쿠키 만들기" 단추를 클릭 하면 샘플 [코드](#sampleCode)에 설정 된 값과 일치 하는 `Lax`SameSite 특성 값이 있습니다.

## <a name="interception"></a>제어 하지 않는 쿠키 가로채기

.NET 4.5.2는 `Response.AddOnSendingHeaders`헤더 쓰기를 가로채기 위한 새 이벤트를 도입 했습니다. 이는 쿠키를 클라이언트 컴퓨터에 반환 하기 전에 가로채는 데 사용할 수 있습니다. 이 샘플에서는 브라우저가 새로운 sameSite 변경 내용을 지원 하는지 여부를 확인 하는 정적 메서드에 이벤트를 연결 하 고, 그렇지 않은 경우 새 `None` 값이 설정 된 경우에서 특성을 내보내지 않도록 쿠키를 변경 합니다.

이벤트를 처리 하 고 쿠키 `sameSite` 특성을 조정 하는 예제는 이벤트를 [연결 하는](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpWebForms/SameSiteCookieRewriter.cs) 예제는 [global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpWebForms/Global.asax.cs) 를 참조 하세요.

```c#
public static void FilterSameSiteNoneForIncompatibleUserAgents(object sender)
{
    HttpApplication application = sender as HttpApplication;
    if (application != null)
    {
        var userAgent = application.Context.Request.UserAgent;
        if (SameSite.BrowserDetection.DisallowsSameSiteNone(userAgent))
        {
            HttpContext.Current.Response.AddOnSendingHeaders(context =>
            {
                var cookies = context.Response.Cookies;
                for (var i = 0; i < cookies.Count; i++)
                {
                    var cookie = cookies[i];
                    if (cookie.SameSite == SameSiteMode.None)
                    {
                        cookie.SameSite = (SameSiteMode)(-1); // Unspecified
                    }
                }
            });
        }
    }
}
```

동일한 방식으로 명명 된 쿠키의 특정 동작을 변경할 수 있습니다. 아래 샘플은 `Lax`에서 `None` 값을 지 원하는 브라우저에 `None` 기본 인증 쿠키를 조정 하거나 `None`를 지원 하지 않는 브라우저에서 sameSite 특성을 제거 합니다.

```c#
public static void AdjustSpecificCookieSettings()
{
    HttpContext.Current.Response.AddOnSendingHeaders(context =>
    {
        var cookies = context.Response.Cookies;
        for (var i = 0; i < cookies.Count; i++)
        {
            var cookie = cookies[i]; 
            // Forms auth: ".ASPXAUTH"
            // Session: "ASP.NET_SessionId"
            if (string.Equals(".ASPXAUTH", cookie.Name, StringComparison.Ordinal))
            { 
                if (SameSite.BrowserDetection.DisallowsSameSiteNone(userAgent))
                {
                    cookie.SameSite = -1;
                }
                else
                {
                    cookie.SameSite = SameSiteMode.None;
                }
                cookie.Secure = true;
            }
        }
    });
}
```

## <a name="more-information"></a>추가 정보

[Chrome 업데이트](https://www.chromium.org/updates/same-site)

[ASP.NET 설명서](/aspnet/samesite/system-web-samesite)

[.NET SameSite 패치](/aspnet/samesite/kbs-samesite)