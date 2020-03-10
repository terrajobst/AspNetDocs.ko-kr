---
title: ASP.NET 4.7.2 VB WebForms에 대 한 SameSite cookie 샘플
author: blowdart
description: ASP.NET 4.7.2 VB WebForms에 대 한 SameSite cookie 샘플
ms.author: riande
ms.date: 2/15/2019
uid: samesite/vbWF
ms.openlocfilehash: 8979edecc5acf7dac81b9f53d31af00389f4727c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78438437"
---
# <a name="samesite-cookie-sample-for-aspnet-472-vb-webforms"></a><span data-ttu-id="465bc-103">ASP.NET 4.7.2 VB WebForms에 대 한 SameSite cookie 샘플</span><span class="sxs-lookup"><span data-stu-id="465bc-103">SameSite cookie sample for ASP.NET 4.7.2 VB WebForms</span></span>
<span data-ttu-id="465bc-104">.NET Framework 4.7는 [SameSite](https://www.owasp.org/index.php/SameSite) 특성에 대 한 기본 제공 지원을 제공 하지만 원래 표준을 준수 합니다.</span><span class="sxs-lookup"><span data-stu-id="465bc-104">.NET Framework 4.7 has built-in support for the [SameSite](https://www.owasp.org/index.php/SameSite) attribute, but it adheres to the original standard.</span></span>
<span data-ttu-id="465bc-105">패치 된 동작이 `SameSite.None`의 의미를 변경 하 여 값을 전혀 내보내지 않고 `None`값으로 특성을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="465bc-105">The patched behavior changed the meaning of `SameSite.None` to emit the attribute with a value of `None`, rather than not emit the value at all.</span></span> <span data-ttu-id="465bc-106">값을 내보내지 않으려면 쿠키의 `SameSite` 속성을-1로 설정 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="465bc-106">If you want to not emit the value you can set the `SameSite` property on a cookie to -1.</span></span>

## <a name="sampleCode"></a><span data-ttu-id="465bc-107">SameSite 특성 작성</span><span class="sxs-lookup"><span data-stu-id="465bc-107">Writing the SameSite attribute</span></span>

<span data-ttu-id="465bc-108">다음은 쿠키에 SameSite 특성을 작성 하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="465bc-108">Following is an example of how to write a SameSite attribute on a cookie;</span></span>

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

<span data-ttu-id="465bc-109">폼 인증 쿠키의 기본 sameSite 특성은의 폼 인증 설정의 `cookieSameSite` 매개 변수에 설정 됩니다 `web.config`</span><span class="sxs-lookup"><span data-stu-id="465bc-109">The default sameSite attribute for a forms authentication cookie is set in the `cookieSameSite` parameter of the forms authentication settings in `web.config`</span></span> 

```xml
<system.web>
  <authentication mode="Forms">
    <forms name=".ASPXAUTH" loginUrl="~/" cookieSameSite="None" requireSSL="true">
    </forms>
  </authentication>
</system.web>
```

<span data-ttu-id="465bc-110">세션 상태에 대 한 기본 sameSite 특성도 `web.config`에서 세션 설정의 ' cookieSameSite ' 매개 변수에 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="465bc-110">The default sameSite attribute for session state is also set in the 'cookieSameSite' parameter of the session settings in `web.config`</span></span>

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

<span data-ttu-id="465bc-111">.NET에 대 한 11 월 2019 업데이트는 가장 호환성이 높은 설정 `lax` 폼 인증 및 세션에 대 한 기본 설정을 변경 했습니다. 그러나 iframe에 페이지를 포함 하는 경우이 설정을 없음으로 되돌린 다음 아래 표시 된 [가로채기](#interception) 코드를 추가 하 여 브라우저 기능에 따라 `none` 동작을 조정 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="465bc-111">The November 2019 update to .NET changed the default settings for Forms Authentication and Session to `lax` as is the most compatible setting, however if you embed pages into iframes you may need to revert this setting to None, and then add the [interception](#interception) code shown below to adjust the `none` behavior depending on browser capability.</span></span>

### <a name="running-the-sample"></a><span data-ttu-id="465bc-112">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="465bc-112">Running the sample</span></span>

<span data-ttu-id="465bc-113">샘플 프로젝트를 실행 하는 경우 초기 페이지에서 브라우저 디버거를 로드 하 고이를 사용 하 여 사이트에 대 한 쿠키 컬렉션을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="465bc-113">If you run the sample project  load your browser debugger on the initial page and use it to view the cookie collection for the site.</span></span>
<span data-ttu-id="465bc-114">Edge 및 Chrome에서이 작업을 수행 하려면 `F12`를 클릭 한 다음 `Application` 탭을 선택 하 고 `Storage` 섹션의 `Cookies` 옵션 아래에서 사이트 URL을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="465bc-114">To do so in Edge and Chrome press `F12` then select the `Application` tab and click the site URL under the `Cookies` option in the `Storage` section.</span></span>

![브라우저 디버거 쿠키 목록](sample/img/BrowserDebugger.png)

<span data-ttu-id="465bc-116">위의 이미지에서 볼 수 있습니다. 예를 들어 "쿠키 만들기" 단추를 클릭 하면 샘플 [코드](#sampleCode)에 설정 된 값과 일치 하는 `Lax`SameSite 특성 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="465bc-116">You can see from the image above that the cookie created by the sample when you click the "Create Cookies" button has a SameSite attribute value of `Lax`, matching the value set in the [sample code](#sampleCode).</span></span>

## <a name="interception"></a><span data-ttu-id="465bc-117">제어 하지 않는 쿠키 가로채기</span><span class="sxs-lookup"><span data-stu-id="465bc-117">Intercepting cookies you do not control</span></span>

<span data-ttu-id="465bc-118">.NET 4.5.2는 `Response.AddOnSendingHeaders`헤더 쓰기를 가로채기 위한 새 이벤트를 도입 했습니다.</span><span class="sxs-lookup"><span data-stu-id="465bc-118">.NET 4.5.2 introduced a new event for intercepting the writing of headers, `Response.AddOnSendingHeaders`.</span></span> <span data-ttu-id="465bc-119">이는 쿠키를 클라이언트 컴퓨터에 반환 하기 전에 가로채는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="465bc-119">This can be used to intercept cookies before they are returned to the client machine.</span></span> <span data-ttu-id="465bc-120">이 샘플에서는 브라우저가 새로운 sameSite 변경 내용을 지원 하는지 여부를 확인 하는 정적 메서드에 이벤트를 연결 하 고, 그렇지 않은 경우 새 `None` 값이 설정 된 경우에서 특성을 내보내지 않도록 쿠키를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="465bc-120">In the sample we wire up the event to a static method which checks whether the browser supports the new sameSite changes, and if not, changes the cookies to not emit the attribute if the new `None` value has been set.</span></span>

<span data-ttu-id="465bc-121">이벤트를 처리 하 고 쿠키 `sameSite` 특성을 조정 하는 예제는 이벤트를 [연결 하는](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicWebForms/SameSiteCookieRewriter.vb) 예제는 [global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicWebForms/Global.asax.vb) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="465bc-121">See [global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicWebForms/Global.asax.vb) for an example of hooking up the event and [SameSiteCookieRewriter.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicWebForms/SameSiteCookieRewriter.vb) for an example of handling the event and adjusting the cookie `sameSite` attribute.</span></span>


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

<span data-ttu-id="465bc-122">동일한 방식으로 명명 된 쿠키의 특정 동작을 변경할 수 있습니다. 아래 샘플은 `Lax`에서 `None` 값을 지 원하는 브라우저에 `None` 기본 인증 쿠키를 조정 하거나 `None`를 지원 하지 않는 브라우저에서 sameSite 특성을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="465bc-122">You can change specific named cookie behavior in much the same way; the sample below adjust the default authentication cookie from `Lax` to `None` on browsers which support the `None` value, or removes the sameSite attribute on browsers which do not support `None`.</span></span>

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

## <a name="more-information"></a><span data-ttu-id="465bc-123">추가 정보</span><span class="sxs-lookup"><span data-stu-id="465bc-123">More Information</span></span>

[<span data-ttu-id="465bc-124">Chrome 업데이트</span><span class="sxs-lookup"><span data-stu-id="465bc-124">Chrome Updates</span></span>](https://www.chromium.org/updates/same-site)

[<span data-ttu-id="465bc-125">ASP.NET 설명서</span><span class="sxs-lookup"><span data-stu-id="465bc-125">ASP.NET Documentation</span></span>](/aspnet/samesite/system-web-samesite)

[<span data-ttu-id="465bc-126">.NET SameSite 패치</span><span class="sxs-lookup"><span data-stu-id="465bc-126">.NET SameSite Patches</span></span>](/aspnet/samesite/kbs-samesite)