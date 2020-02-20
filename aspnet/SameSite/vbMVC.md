---
title: ASP.NET 4.7.2 VB MVC에 대 한 SameSite cookie 샘플
author: blowdart
description: ASP.NET 4.7.2 VB MVC에 대 한 SameSite cookie 샘플
ms.author: riande
ms.date: 2/15/2019
uid: samesite/vbMVC
ms.openlocfilehash: f6effce6075f94fb58ce10ec08bf010fab8b4b56
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77458410"
---
# <a name="samesite-cookie-sample-for-aspnet-472-vb-mvc"></a><span data-ttu-id="8b8fd-103">ASP.NET 4.7.2 VB MVC에 대 한 SameSite cookie 샘플</span><span class="sxs-lookup"><span data-stu-id="8b8fd-103">SameSite cookie sample for ASP.NET 4.7.2 VB MVC</span></span>

<span data-ttu-id="8b8fd-104">.NET Framework 4.7는 [SameSite](https://www.owasp.org/index.php/SameSite) 특성에 대 한 기본 제공 지원을 제공 하지만 원래 표준을 준수 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b8fd-104">.NET Framework 4.7 has built-in support for the [SameSite](https://www.owasp.org/index.php/SameSite) attribute, but it adheres to the original standard.</span></span>
<span data-ttu-id="8b8fd-105">패치 된 동작이 `SameSite.None`의 의미를 변경 하 여 값을 전혀 내보내지 않고 `None`값으로 특성을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8b8fd-105">The patched behavior changed the meaning of `SameSite.None` to emit the attribute with a value of `None`, rather than not emit the value at all.</span></span> <span data-ttu-id="8b8fd-106">값을 내보내지 않으려면 쿠키의 `SameSite` 속성을-1로 설정 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b8fd-106">If you want to not emit the value you can set the `SameSite` property on a cookie to -1.</span></span>

## <a name="sampleCode"></a><span data-ttu-id="8b8fd-107">SameSite 특성 작성</span><span class="sxs-lookup"><span data-stu-id="8b8fd-107">Writing the SameSite attribute</span></span>

<span data-ttu-id="8b8fd-108">다음은 쿠키에 SameSite 특성을 작성 하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="8b8fd-108">Following is an example of how to write a SameSite attribute on a cookie;</span></span>

```vb
' Create the cookie
Dim sameSiteCookie As New HttpCookie("sameSiteSample")

' Set a value for the cookie
sameSiteCookie.Value = "sample"

' Set the secure flag, which Chrome's changes will require for SameSite none.
' Note this will also require you to be running on HTTPS
sameSiteCookie.Secure = True

' Set the cookie to HTTP only which is good practice unless you really do need
' to access it client side in scripts.
sameSiteCookie.HttpOnly = True

' Expire the cookie in 1 minute
sameSiteCookie.Expires = Date.Now.AddMinutes(1)

' Add the SameSite attribute, this will emit the attribute with a value of none.
' To Not emit the attribute at all set the SameSite property to -1.
sameSiteCookie.SameSite = SameSiteMode.None

' Add the cookie to the response cookie collection
Response.Cookies.Add(sameSiteCookie)
```

[!INCLUDE[](~/includes/MTcomments.md)]

<span data-ttu-id="8b8fd-109">세션 상태에 대 한 기본 sameSite 특성은 세션 설정의 ' cookieSameSite ' 매개 변수에 설정 됩니다 `web.config`</span><span class="sxs-lookup"><span data-stu-id="8b8fd-109">The default sameSite attribute for session state is set in the 'cookieSameSite' parameter of the session settings in `web.config`</span></span>

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

## <a name="mvc-authentication"></a><span data-ttu-id="8b8fd-110">MVC 인증</span><span class="sxs-lookup"><span data-stu-id="8b8fd-110">MVC Authentication</span></span>

<span data-ttu-id="8b8fd-111">OWIN MVC 쿠키 기반 인증에서는 쿠키 관리자를 사용 하 여 쿠키 특성을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b8fd-111">OWIN MVC cookie based authentication uses a cookie manager to enable the changing of cookie attributes.</span></span> <span data-ttu-id="8b8fd-112">[SameSiteCookieManager](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/SameSiteCookieManager.vb) 는 고유한 프로젝트로 복사할 수 있는 이러한 클래스의 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="8b8fd-112">The [SameSiteCookieManager.vb](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/SameSiteCookieManager.vb) is an implementation of such a class which you can copy into your own projects.</span></span> 

<span data-ttu-id="8b8fd-113">Owin 구성 요소가 모두 버전 4.1.0 이상으로 업그레이드 되었는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b8fd-113">You must ensure your Microsoft.Owin components are all upgraded to version 4.1.0 or greater.</span></span> <span data-ttu-id="8b8fd-114">`packages.config` 파일에서 모든 버전 번호가 일치 하는지 확인 합니다 (예:).</span><span class="sxs-lookup"><span data-stu-id="8b8fd-114">Check your `packages.config` file to ensure all the version numbers match, for example.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <!-- other packages -->
  <package id="Microsoft.Owin.Host.SystemWeb" version="4.1.0" targetFramework="net472" />
  <package id="Microsoft.Owin.Security" version="4.1.0" targetFramework="net472" />
  <package id="Microsoft.Owin.Security.Cookies" version="4.1.0" targetFramework="net472" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net472" />
  <package id="Owin" version="1.0" targetFramework="net472" />
</packages>
```

<span data-ttu-id="8b8fd-115">시작 클래스에서 CookieManager를 사용 하도록 인증 구성 요소를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b8fd-115">The authentication components must be configured to use the CookieManager in your startup class;</span></span>

```vb
Public Sub Configuration(app As IAppBuilder)
    app.UseCookieAuthentication(New CookieAuthenticationOptions() With {
        .CookieSameSite = SameSiteMode.None,
        .CookieHttpOnly = True,
        .CookieSecure = CookieSecureOption.Always,
        .CookieManager = New SameSiteCookieManager(New SystemWebCookieManager())
    })
End Sub
```

<span data-ttu-id="8b8fd-116">쿠키 관리자는이를 지 원하는 *각* 구성 요소에서 설정 해야 합니다. 여기에는 CookieAuthentication 및 OpenIdConnectAuthentication이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b8fd-116">A cookie manager must be set on *each* component that supports it, this includes CookieAuthentication and OpenIdConnectAuthentication.</span></span>

<span data-ttu-id="8b8fd-117">SystemWebCookieManager는 응답 쿠키 통합과 관련 하 여 [알려진 문제](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues) 를 방지 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b8fd-117">The SystemWebCookieManager is used to avoid [known issues](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues) with response cookie integration.</span></span>

### <a name="running-the-sample"></a><span data-ttu-id="8b8fd-118">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="8b8fd-118">Running the sample</span></span>

<span data-ttu-id="8b8fd-119">샘플 프로젝트를 실행 하는 경우 초기 페이지에서 브라우저 디버거를 로드 하 고이를 사용 하 여 사이트에 대 한 쿠키 컬렉션을 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="8b8fd-119">If you run the sample project please load your browser debugger on the initial page and use it to view the cookie collection for the site.</span></span>
<span data-ttu-id="8b8fd-120">Edge 및 Chrome에서이 작업을 수행 하려면 `F12`를 클릭 한 다음 `Application` 탭을 선택 하 고 `Storage` 섹션의 `Cookies` 옵션 아래에서 사이트 URL을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b8fd-120">To do so in Edge and Chrome press `F12` then select the `Application` tab and click the site URL under the `Cookies` option in the `Storage` section.</span></span>

![브라우저 디버거 쿠키 목록](sample/img/BrowserDebugger.png)

<span data-ttu-id="8b8fd-122">"SameSite 쿠키 만들기" 단추를 클릭 하면 샘플 [코드](#sampleCode)에 설정 된 값과 일치 하는 `Lax`SameSite 특성 값이 있는 위의 이미지에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b8fd-122">You can see from the image above that the cookie created by the sample when you click the "Create SameSite Cookie" button has a SameSite attribute value of `Lax`, matching the value set in the [sample code](#sampleCode).</span></span>

## <a name="interception"></a><span data-ttu-id="8b8fd-123">제어 하지 않는 쿠키 가로채기</span><span class="sxs-lookup"><span data-stu-id="8b8fd-123">Intercepting cookies you do not control</span></span>

<span data-ttu-id="8b8fd-124">.NET 4.5.2는 `Response.AddOnSendingHeaders`헤더 쓰기를 가로채기 위한 새 이벤트를 도입 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8b8fd-124">.NET 4.5.2 introduced a new event for intercepting the writing of headers, `Response.AddOnSendingHeaders`.</span></span> <span data-ttu-id="8b8fd-125">이는 쿠키를 클라이언트 컴퓨터에 반환 하기 전에 가로채는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b8fd-125">This can be used to intercept cookies before they are returned to the client machine.</span></span> <span data-ttu-id="8b8fd-126">이 샘플에서는 브라우저가 새로운 sameSite 변경 내용을 지원 하는지 여부를 확인 하는 정적 메서드에 이벤트를 연결 하 고, 그렇지 않은 경우 새 `None` 값이 설정 된 경우에서 특성을 내보내지 않도록 쿠키를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b8fd-126">In the sample we wire up the event to a static method which checks whether the browser supports the new sameSite changes, and if not, changes the cookies to not emit the attribute if the new `None` value has been set.</span></span>

<span data-ttu-id="8b8fd-127">이벤트를 처리 하 고 사용자의 코드에 복사할 수 있는 쿠키 `sameSite` 특성을 조정 하는 [예제를 보려면](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/SameSiteCookieRewriter.vb) [global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/Global.asax.vb) 를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="8b8fd-127">See [global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/Global.asax.vb) for an example of hooking up the event and [SameSiteCookieRewriter.vb](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/SameSiteCookieRewriter.vb) for an example of handling the event and adjusting the cookie `sameSite` attribute which you can copy into your own code.</span></span>

```vb
Sub FilterSameSiteNoneForIncompatibleUserAgents(ByVal sender As Object)
    Dim application As HttpApplication = TryCast(sender, HttpApplication)

    If application IsNot Nothing Then
        Dim userAgent = application.Context.Request.UserAgent

        If SameSite.DisallowsSameSiteNone(userAgent) Then
            application.Response.AddOnSendingHeaders(
                Function(context)
                    Dim cookies = context.Response.Cookies

                    For i = 0 To cookies.Count - 1
                        Dim cookie = cookies(i)

                        If cookie.SameSite = SameSiteMode.None Then
                            cookie.SameSite = CType((-1), SameSiteMode)
                        End If
                    Next
                End Function)
        End If
    End If
End Sub
```

<span data-ttu-id="8b8fd-128">동일한 방식으로 명명 된 쿠키의 특정 동작을 변경할 수 있습니다. 아래 샘플은 `Lax`에서 `None` 값을 지 원하는 브라우저에 `None` 기본 인증 쿠키를 조정 하거나 `None`를 지원 하지 않는 브라우저에서 sameSite 특성을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b8fd-128">You can change specific named cookie behavior in much the same way; the sample below adjust the default authentication cookie from `Lax` to `None` on browsers which support the `None` value, or removes the sameSite attribute on browsers which do not support `None`.</span></span>

```vb
Public Shared Sub AdjustSpecificCookieSettings()
    HttpContext.Current.Response.AddOnSendingHeaders(Function(context)
            Dim cookies = context.Response.Cookies

            For i = 0 To cookies.Count - 1
            Dim cookie = cookies(i)

            If String.Equals(".ASPXAUTH", cookie.Name, StringComparison.Ordinal) Then

                If SameSite.BrowserDetection.DisallowsSameSiteNone(userAgent) Then
                    cookie.SameSite = -1
                Else
                    cookie.SameSite = SameSiteMode.None
                End If

                cookie.Secure = True
            End If
            Next
        End Function)
End Sub
```

## <a name="more-information"></a><span data-ttu-id="8b8fd-129">추가 정보</span><span class="sxs-lookup"><span data-stu-id="8b8fd-129">More Information</span></span>
 
[<span data-ttu-id="8b8fd-130">Chrome 업데이트</span><span class="sxs-lookup"><span data-stu-id="8b8fd-130">Chrome Updates</span></span>](https://www.chromium.org/updates/same-site)

[<span data-ttu-id="8b8fd-131">OWIN SameSite 설명서</span><span class="sxs-lookup"><span data-stu-id="8b8fd-131">OWIN SameSite Documentation</span></span>](/aspnet/samesite/owin-samesite)

[<span data-ttu-id="8b8fd-132">ASP.NET 설명서</span><span class="sxs-lookup"><span data-stu-id="8b8fd-132">ASP.NET Documentation</span></span>](/aspnet/samesite/system-web-samesite)

[<span data-ttu-id="8b8fd-133">.NET SameSite 패치</span><span class="sxs-lookup"><span data-stu-id="8b8fd-133">.NET SameSite Patches</span></span>](/aspnet/samesite/kbs-samesite)