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
# <a name="samesite-cookies-and-the-open-web-interface-for-net-owin"></a><span data-ttu-id="1d8e6-103">SameSite 쿠키 및 OWIN (Open Web Interface for .NET)</span><span class="sxs-lookup"><span data-stu-id="1d8e6-103">SameSite cookies and the Open Web Interface for .NET (OWIN)</span></span>

<span data-ttu-id="1d8e6-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="1d8e6-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="1d8e6-105">`SameSite`은 CSRF (교차 사이트 요청 위조) 공격에 대 한 보호를 제공 하도록 설계 된 [IETF](https://ietf.org/about/) 초안입니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-105">`SameSite` is an [IETF](https://ietf.org/about/) draft designed to provide some protection against cross-site request forgery (CSRF) attacks.</span></span> <span data-ttu-id="1d8e6-106">[SameSite 2019 초안](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00):</span><span class="sxs-lookup"><span data-stu-id="1d8e6-106">The [SameSite 2019 draft](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00):</span></span>

* <span data-ttu-id="1d8e6-107">에서는 기본적으로 쿠키를 `SameSite=Lax`로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-107">Treats cookies as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="1d8e6-108">사이트 간 배달을 가능 하 게 하기 위해 `SameSite=None`를 명시적으로 어설션하는 쿠키는 `Secure`으로 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-108">States cookies that explicitly assert `SameSite=None` in order to enable cross-site delivery should be marked as `Secure`.</span></span>

<span data-ttu-id="1d8e6-109">`Lax` 대부분의 앱 쿠키에 대해 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-109">`Lax` works for most app cookies.</span></span> <span data-ttu-id="1d8e6-110">Oidc ( [Openid connect Connect](https://openid.net/connect/) )와 같은 일부 형태의 인증 및 [ws-federation](https://auth0.com/docs/protocols/ws-fed) 은 게시 기반 리디렉션에 대해 기본적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-110">Some forms of authentication like [OpenID Connect](https://openid.net/connect/) (OIDC) and [WS-Federation](https://auth0.com/docs/protocols/ws-fed) default to POST based redirects.</span></span> <span data-ttu-id="1d8e6-111">사후 기반 리디렉션은 이러한 구성 요소에 대해 `SameSite`를 사용할 수 없도록 `SameSite` 브라우저 보호를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-111">The POST based redirects trigger the `SameSite` browser protections, so `SameSite` is disabled for these components.</span></span> <span data-ttu-id="1d8e6-112">대부분의 [OAuth](https://oauth.net/) 로그인은 요청 흐름의 차이로 인해 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-112">Most [OAuth](https://oauth.net/) logins aren't affected due to differences in how the request flows.</span></span> <span data-ttu-id="1d8e6-113">다른 모든 구성 요소는 기본적으로 `SameSite` 설정 **되지** 않으며 클라이언트 기본 동작 (이전 또는 새)을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-113">All other components do **not** set `SameSite` by default and use the clients default behavior (old or new).</span></span>

<span data-ttu-id="1d8e6-114">`None` 매개 변수를 사용 하면 이전 [2016 초안 표준](https://tools.ietf.org/html/draft-west-first-party-cookies-07) (예: iOS 12)을 구현한 클라이언트에서 호환성 문제가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-114">The `None` parameter causes compatibility problems with clients that implemented the prior [2016 draft standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07) (for example, iOS 12).</span></span> <span data-ttu-id="1d8e6-115">이 문서의 [이전 브라우저 지원](#sob) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-115">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="1d8e6-116">쿠키를 내보내는 각 OWIN 구성 요소는 `SameSite` 적절 한지 결정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-116">Each OWIN component that emits cookies needs to decide if `SameSite` is appropriate.</span></span>

<span data-ttu-id="1d8e6-117">이 문서의 ASP.NET 4.x 버전은 <xref:samesite/system-web-samesite>를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-117">For the ASP.NET 4.x version of this article, see <xref:samesite/system-web-samesite>.</span></span>

## <a name="api-usage-with-samesite"></a><span data-ttu-id="1d8e6-118">SameSite를 사용 하는 API 사용</span><span class="sxs-lookup"><span data-stu-id="1d8e6-118">API usage with SameSite</span></span>

<span data-ttu-id="1d8e6-119">`Microsoft.Owin`에는 고유한 `SameSite` 구현이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-119">`Microsoft.Owin` has its own `SameSite` implementation:</span></span>

* <span data-ttu-id="1d8e6-120">이는 `System.Web`의 항목에 직접적으로 종속 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-120">That is not directly dependent on the one in `System.Web`.</span></span>
* <span data-ttu-id="1d8e6-121">`SameSite`는 `Microsoft.Owin` 패키지, .NET 4.5 이상에 의해 가능 모든 버전에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-121">`SameSite` works on all versions targetable by the `Microsoft.Owin` packages, .NET 4.5 and later.</span></span>
* <span data-ttu-id="1d8e6-122">[SystemWebCookieManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebCookieManager.cs) 구성 요소만 `System.Web` `HttpCookie` 클래스와 직접적으로 상호 작용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-122">Only the [SystemWebCookieManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebCookieManager.cs) component directly interacts with the `System.Web` `HttpCookie` class.</span></span>

<span data-ttu-id="1d8e6-123">`SystemWebCookieManager`는 .NET 4.7.2 `System.Web` Api에 따라 `SameSite` 지원을 사용 하도록 설정 하 고 패치를 사용 하 여 동작을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-123">`SystemWebCookieManager` depends on the .NET 4.7.2 `System.Web` APIs to enable `SameSite` support, and the patches to change the behavior.</span></span>

<span data-ttu-id="1d8e6-124">`SystemWebCookieManager`를 사용 하는 이유는 [OWIN 및 system.web response 쿠키 통합 문제](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues)에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-124">The reasons to use `SystemWebCookieManager` are outlined in [OWIN and System.Web response cookie integration issues](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues).</span></span> <span data-ttu-id="1d8e6-125">`System.Web`에서 실행 하는 경우 `SystemWebCookieManager` 권장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-125">`SystemWebCookieManager` is recommended when running on `System.Web`.</span></span>

<span data-ttu-id="1d8e6-126">다음 코드는 `Lax``SameSite`를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-126">The following code sets `SameSite` to `Lax`:</span></span>

```csharp
owinContext.Response.Cookies.Append("My Key", "My Value", new CookieOptions()
{
    SameSite = SameSiteMode.Lax
});
```

<span data-ttu-id="1d8e6-127">다음 Api는 `SameSite`을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-127">The following APIs use `SameSite`:</span></span>

* [<span data-ttu-id="1d8e6-128">Owin. SameSiteMode</span><span class="sxs-lookup"><span data-stu-id="1d8e6-128">Microsoft.Owin.SameSiteMode</span></span>](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin/SameSiteMode.cs)
* [<span data-ttu-id="1d8e6-129">CookieOptions. SameSite</span><span class="sxs-lookup"><span data-stu-id="1d8e6-129">CookieOptions.SameSite</span></span>](xref:Microsoft.AspNetCore.Http.CookieOptions.SameSite)
* <span data-ttu-id="1d8e6-130">[은 cookieauthenticationoptions.authenticationtype 클래스](/previous-versions/aspnet/dn385599(v%3Dvs.113))</span><span class="sxs-lookup"><span data-stu-id="1d8e6-130">[CookieAuthenticationOptions Class](/previous-versions/aspnet/dn385599(v%3Dvs.113))</span></span> <!-- CookieAuthenticationOptions.CookieSameSite not published -->
* [<span data-ttu-id="1d8e6-131">은 cookieauthenticationoptions.authenticationtype. CookieSameSite</span><span class="sxs-lookup"><span data-stu-id="1d8e6-131">CookieAuthenticationOptions.CookieSameSite</span></span>](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.Cookies/CookieAuthenticationOptions.cs#L68-#L72)
* <span data-ttu-id="1d8e6-132">[ICookieManager](/previous-versions/aspnet/dn800238(v%3Dvs.113))</span><span class="sxs-lookup"><span data-stu-id="1d8e6-132">[ICookieManager](/previous-versions/aspnet/dn800238(v%3Dvs.113))</span></span>
* [<span data-ttu-id="1d8e6-133">SystemWebCookieManager</span><span class="sxs-lookup"><span data-stu-id="1d8e6-133">SystemWebCookieManager</span></span>](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebCookieManager.cs)
* [<span data-ttu-id="1d8e6-134">SystemWebChunkingCookieManager</span><span class="sxs-lookup"><span data-stu-id="1d8e6-134">SystemWebChunkingCookieManager</span></span>](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebChunkingCookieManager.cs)
* [<span data-ttu-id="1d8e6-135">은 cookieauthenticationoptions.authenticationtype. CookieManager</span><span class="sxs-lookup"><span data-stu-id="1d8e6-135">CookieAuthenticationOptions.CookieManager</span></span>](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.Cookies/CookieAuthenticationOptions.cs#L143-#AL148)
* [<span data-ttu-id="1d8e6-136">OpenIdConnectAuthenticationOptions. CookieManager</span><span class="sxs-lookup"><span data-stu-id="1d8e6-136">OpenIdConnectAuthenticationOptions.CookieManager</span></span>](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.OpenIdConnect/OpenIdConnectAuthenticationOptions.cs#L315-#L318)

## <a name="history-and-changes"></a><span data-ttu-id="1d8e6-137">기록 및 변경 내용</span><span class="sxs-lookup"><span data-stu-id="1d8e6-137">History and changes</span></span>

<span data-ttu-id="1d8e6-138">[Owin](https://www.nuget.org/packages/Microsoft.Owin/) 는 [`SameSite` 2016 초안 표준을](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-138">[Microsoft.Owin](https://www.nuget.org/packages/Microsoft.Owin/) never supported the [`SameSite` 2016 draft standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1).</span></span>

<span data-ttu-id="1d8e6-139">[SameSite 2019 초안](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) 에 대 한 지원은 `Microsoft.Owin` 4.1.0 이상 에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-139">Support for the [SameSite 2019 draft](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) is only available in `Microsoft.Owin` 4.1.0 and later.</span></span> <span data-ttu-id="1d8e6-140">이전 버전에 대 한 패치는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-140">There are no patches for prior versions.</span></span>

<span data-ttu-id="1d8e6-141">`SameSite` 사양의 2019 초안:</span><span class="sxs-lookup"><span data-stu-id="1d8e6-141">The 2019 draft of the `SameSite` specification:</span></span>

* <span data-ttu-id="1d8e6-142">는 이전 버전과 호환 **되지 않습니다** . 2016 초안.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-142">Is **not** backwards compatible with the 2016 draft.</span></span> <span data-ttu-id="1d8e6-143">자세한 내용은이 문서의 [이전 브라우저 지원](#sob) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-143">For more information, see [Supporting older browsers](#sob) in this document.</span></span>
* <span data-ttu-id="1d8e6-144">기본적으로 `SameSite=Lax`로 처리 되는 쿠키를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-144">Specifies cookies are treated as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="1d8e6-145">교차 사이트 배달을 사용 하도록 설정 하기 위해 `SameSite=None`를 명시적으로 어설션하는 쿠키를 `Secure`으로 표시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-145">Specifies cookies that explicitly assert `SameSite=None` in order to enable cross-site delivery should be marked as `Secure`.</span></span> <span data-ttu-id="1d8e6-146">`None`은 옵트아웃 (opt out) 할 새 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-146">`None` is a new entry to opt out.</span></span>
* <span data-ttu-id="1d8e6-147">는 기본적으로 [2 월 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)에 [Chrome](https://chromestatus.com/feature/5088147346030592) 에서 사용 하도록 예약 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-147">Is scheduled to be enabled by [Chrome](https://chromestatus.com/feature/5088147346030592) by default in [Feb 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html).</span></span> <span data-ttu-id="1d8e6-148">브라우저에서 2019의이 표준으로 이동 하기 시작 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-148">Browsers started moving to this standard in 2019.</span></span>
* <span data-ttu-id="1d8e6-149">는 KB 문서에 설명 된 대로 발급 된 패치에 의해 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-149">Is supported by patches issued as described in KB articles.</span></span> <span data-ttu-id="1d8e6-150">자세한 내용은 <xref:samesite/kbs-samesite>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-150">For more information, see <xref:samesite/kbs-samesite>.</span></span>

<a name="sob"></a>

## <a name="supporting-older-browsers"></a><span data-ttu-id="1d8e6-151">이전 브라우저 지원</span><span class="sxs-lookup"><span data-stu-id="1d8e6-151">Supporting older browsers</span></span>

<span data-ttu-id="1d8e6-152">2016 `SameSite` 표준에서는 알 수 없는 값을 `SameSite=Strict` 값으로 처리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-152">The 2016 `SameSite` standard mandated that unknown values must be treated as `SameSite=Strict` values.</span></span> <span data-ttu-id="1d8e6-153">2016 `SameSite` 표준을 지 원하는 이전 브라우저에서 액세스 한 앱은 `None`값을 가진 `SameSite` 속성을 가져오면 중단 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-153">Apps accessed from older browsers which support the 2016 `SameSite` standard may break when they get a `SameSite` property with a value of `None`.</span></span> <span data-ttu-id="1d8e6-154">웹 앱은 이전 브라우저를 지원 하려는 경우 브라우저 검색을 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-154">Web apps must implement browser detection if they intend to support older browsers.</span></span> <span data-ttu-id="1d8e6-155">사용자 에이전트 값이 매우 휘발성 이며 자주 변경 되기 때문에 ASP.NET는 브라우저 검색을 구현 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-155">ASP.NET doesn't implement browser detection because User-Agents values are highly volatile and change frequently.</span></span> <span data-ttu-id="1d8e6-156">[ICookieManager](/previous-versions/aspnet/dn800238(v%3Dvs.113)) 의 확장 지점은 사용자 에이전트 특정 논리를 연결 하는 것을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-156">An extension point in [ICookieManager](/previous-versions/aspnet/dn800238(v%3Dvs.113)) allows plugging in User-Agent specific logic.</span></span>
<!-- https://docs.microsoft.com/previous-versions/aspnet/dn800238(v%3Dvs.113) -->

<span data-ttu-id="1d8e6-157">`Startup.Configuration`에서 다음과 유사한 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-157">In `Startup.Configuration`, add code similar to the following:</span></span>

[!code-csharp[](sample/Startup1.cs?name=snippet)]

<span data-ttu-id="1d8e6-158">위의 코드에는 .NET 4.7.2 이상 `SameSite` 패치가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-158">The preceding code requires the .NET 4.7.2 or later `SameSite` patch.</span></span>

<span data-ttu-id="1d8e6-159">다음 코드는 `SameSiteCookieManager`의 구현 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-159">The following code shows an example implementation of `SameSiteCookieManager`:</span></span>

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet)]

<span data-ttu-id="1d8e6-160">위의 샘플에서 `DisallowsSameSiteNone`은 `CheckSameSite` 메서드에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-160">In the preceding sample, `DisallowsSameSiteNone` is called in the `CheckSameSite` method.</span></span> <span data-ttu-id="1d8e6-161">`DisallowsSameSiteNone`은 사용자 에이전트가 `SameSite` `None`를 지원 하지 않는지 여부를 검색 하는 사용자 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-161">`DisallowsSameSiteNone` is a user method that detects if the user agent doesn't support `SameSite` `None`:</span></span>

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet3&highlight=4)]

<span data-ttu-id="1d8e6-162">다음 코드는 샘플 `DisallowsSameSiteNone` 메서드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-162">The following code shows a sample `DisallowsSameSiteNone` method:</span></span>

> [!WARNING]
> <span data-ttu-id="1d8e6-163">다음 코드는 데모용 으로만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-163">The following code is for demonstration only:</span></span>
> * <span data-ttu-id="1d8e6-164">완료 되지 않은 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-164">It should not be considered complete.</span></span>
> * <span data-ttu-id="1d8e6-165">유지 관리 되거나 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-165">It is not maintained or supported.</span></span>

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet2)]

## <a name="test-apps-for-samesite-problems"></a><span data-ttu-id="1d8e6-166">SameSite 문제에 대 한 앱 테스트</span><span class="sxs-lookup"><span data-stu-id="1d8e6-166">Test apps for SameSite problems</span></span>

<span data-ttu-id="1d8e6-167">타사 로그인을 통해와 같은 원격 사이트와 상호 작용 하는 앱은 다음 작업을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-167">Apps that interact with remote sites such as through third-party login need to:</span></span>

* <span data-ttu-id="1d8e6-168">여러 브라우저에서 상호 작용을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-168">Test the interaction on multiple browsers.</span></span>
* <span data-ttu-id="1d8e6-169">이 문서에서 설명 [하는 브라우저 검색 및 완화](#sob) 를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-169">Apply the [browser detection and mitigation](#sob) discussed in this document.</span></span>

<span data-ttu-id="1d8e6-170">새 `SameSite` 동작을 옵트인 (opt in) 할 수 있는 클라이언트 버전을 사용 하 여 웹 앱을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-170">Test web apps using a client version that can opt-in to the new `SameSite` behavior.</span></span> <span data-ttu-id="1d8e6-171">Chrome, Firefox 및 Chromium Edge 모두에는 테스트에 사용할 수 있는 새로운 옵트인 기능 플래그가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-171">Chrome, Firefox, and Chromium Edge all have new opt-in feature flags that can be used for testing.</span></span> <span data-ttu-id="1d8e6-172">앱이 `SameSite` 패치를 적용 한 후 이전 클라이언트 버전, 특히 Safari를 사용 하 여 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-172">After your app applies the `SameSite` patches, test it with older client versions, especially Safari.</span></span> <span data-ttu-id="1d8e6-173">자세한 내용은이 문서의 [이전 브라우저 지원](#sob) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-173">For more information, see [Supporting older browsers](#sob) in this document.</span></span>

### <a name="test-with-chrome"></a><span data-ttu-id="1d8e6-174">Chrome으로 테스트</span><span class="sxs-lookup"><span data-stu-id="1d8e6-174">Test with Chrome</span></span>

<span data-ttu-id="1d8e6-175">Chrome 78 +는 일시적인 완화를 제공 하기 때문에 잘못 된 결과를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-175">Chrome 78+ gives misleading results because it has a temporary mitigation in place.</span></span> <span data-ttu-id="1d8e6-176">Chrome 78 + 임시 완화를 사용 하면 쿠키가 2 분 이내에 이전 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-176">The Chrome 78+ temporary mitigation allows cookies less than two minutes old.</span></span> <span data-ttu-id="1d8e6-177">적절 한 테스트 플래그가 설정 된 Chrome 76 또는 77은 보다 정확한 결과를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-177">Chrome 76 or 77 with the appropriate test flags enabled provides more accurate results.</span></span> <span data-ttu-id="1d8e6-178">새 `SameSite` 동작을 테스트 하려면 `chrome://flags/#same-site-by-default-cookies`를 **사용**으로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-178">To test the new `SameSite` behavior toggle `chrome://flags/#same-site-by-default-cookies` to **Enabled**.</span></span> <span data-ttu-id="1d8e6-179">이전 버전의 Chrome (75 및 아래)은 새 `None` 설정으로 인해 실패 하는 것으로 보고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-179">Older versions of Chrome (75 and below) are reported to fail with the new `None` setting.</span></span> <span data-ttu-id="1d8e6-180">이 문서의 [이전 브라우저 지원](#sob) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-180">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="1d8e6-181">Google은 이전 chrome 버전을 사용할 수 없도록 설정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-181">Google does not make older chrome versions available.</span></span> <span data-ttu-id="1d8e6-182">[Chromium 다운로드](https://www.chromium.org/getting-involved/download-chromium) 의 지침에 따라 이전 버전의 Chrome을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-182">Follow the instructions at [Download Chromium](https://www.chromium.org/getting-involved/download-chromium) to test older versions of Chrome.</span></span> <span data-ttu-id="1d8e6-183">이전 버전의 chrome을 검색 하 여 제공 된 링크에서 Chrome을 다운로드 **하지** 마세요.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-183">Do **not** download Chrome from links provided by searching for older versions of chrome.</span></span>

* [<span data-ttu-id="1d8e6-184">Chromium 76 Win64</span><span class="sxs-lookup"><span data-stu-id="1d8e6-184">Chromium 76 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [<span data-ttu-id="1d8e6-185">Chromium 74 Win64</span><span class="sxs-lookup"><span data-stu-id="1d8e6-185">Chromium 74 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)

### <a name="test-with-safari"></a><span data-ttu-id="1d8e6-186">Safari를 사용 하 여 테스트</span><span class="sxs-lookup"><span data-stu-id="1d8e6-186">Test with Safari</span></span>

<span data-ttu-id="1d8e6-187">Safari 12는 이전 초안을 엄격 하 게 구현 했으며 새 `None` 값이 쿠키에 있는 경우 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-187">Safari 12 strictly implemented the prior draft and fails when the new `None` value is in a cookie.</span></span> <span data-ttu-id="1d8e6-188">이 문서에서 [이전 브라우저를 지 원하는](#sob) 브라우저 검색 코드를 통해 `None`를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-188">`None` is avoided via the browser detection code [Supporting older browsers](#sob) in this document.</span></span> <span data-ttu-id="1d8e6-189">MSAL, ADAL 또는 사용 중인 라이브러리를 사용 하 여 Safari 12, Safari 13 및 WebKit 기반 OS 스타일 로그인을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-189">Test Safari 12, Safari 13, and WebKit based OS style logins using MSAL, ADAL or whatever library you are using.</span></span> <span data-ttu-id="1d8e6-190">문제는 기본 OS 버전에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-190">The problem is dependent on the underlying OS version.</span></span> <span data-ttu-id="1d8e6-191">OSX Mojave (10.14) 및 iOS 12는 새로운 `SameSite` 동작의 호환성 문제를 해결 하는 것으로 알려져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-191">OSX Mojave (10.14) and iOS 12 are known to have compatibility problems with the new `SameSite` behavior.</span></span> <span data-ttu-id="1d8e6-192">OS를 OSX Catalina.properties (10.15) 또는 iOS 13로 업그레이드 하면 문제가 해결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-192">Upgrading the OS to OSX Catalina (10.15) or iOS 13 fixes the problem.</span></span> <span data-ttu-id="1d8e6-193">Safari에는 현재 새 사양 동작 테스트를 위한 옵트인 플래그가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-193">Safari does not currently have an opt-in flag for testing the new spec behavior.</span></span>

### <a name="test-with-firefox"></a><span data-ttu-id="1d8e6-194">Firefox로 테스트</span><span class="sxs-lookup"><span data-stu-id="1d8e6-194">Test with Firefox</span></span>

<span data-ttu-id="1d8e6-195">새 표준에 대 한 Firefox 지원은 `network.cookie.sameSite.laxByDefault`기능 플래그를 사용 하 여 `about:config` 페이지에서 옵트인 하 여 버전 68 이상에서 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-195">Firefox support for the new standard can be tested on version 68+ by opting in on the `about:config` page with the feature flag `network.cookie.sameSite.laxByDefault`.</span></span> <span data-ttu-id="1d8e6-196">이전 버전의 Firefox와의 호환성 문제에 대 한 보고서가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-196">There haven't been reports of compatibility issues with older versions of Firefox.</span></span>

### <a name="test-with-edge-browser"></a><span data-ttu-id="1d8e6-197">Edge 브라우저를 사용 하 여 테스트</span><span class="sxs-lookup"><span data-stu-id="1d8e6-197">Test with Edge browser</span></span>

<span data-ttu-id="1d8e6-198">Edge는 이전 `SameSite` 표준을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-198">Edge supports the old `SameSite` standard.</span></span> <span data-ttu-id="1d8e6-199">Edge 버전 44에는 새로운 표준과의 알려진 호환성 문제가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-199">Edge version 44 doesn't have any known compatibility problems with the new standard.</span></span>

### <a name="test-with-edge-chromium"></a><span data-ttu-id="1d8e6-200">Edge를 사용 하 여 테스트 (Chromium)</span><span class="sxs-lookup"><span data-stu-id="1d8e6-200">Test with Edge (Chromium)</span></span>

<span data-ttu-id="1d8e6-201">`edge://flags/#same-site-by-default-cookies` 페이지에 `SameSite` 플래그가 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-201">`SameSite` flags are set on the `edge://flags/#same-site-by-default-cookies` page.</span></span> <span data-ttu-id="1d8e6-202">Edge Chromium에서 호환성 문제가 검색 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-202">No compatibility issues were discovered with Edge Chromium.</span></span>

### <a name="test-with-electron"></a><span data-ttu-id="1d8e6-203">전자로 테스트</span><span class="sxs-lookup"><span data-stu-id="1d8e6-203">Test with Electron</span></span>

<span data-ttu-id="1d8e6-204">Electron 버전에는 이전 버전의 Chromium이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-204">Versions of Electron include older versions of Chromium.</span></span> <span data-ttu-id="1d8e6-205">예를 들어 팀에서 사용 하는 전자의 버전은 Chromium 66 이며,이는 이전 동작을 보여 주는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-205">For example, the version of Electron used by Teams is Chromium 66, which exhibits the older behavior.</span></span> <span data-ttu-id="1d8e6-206">제품에서 사용 하는 전자 제품 버전으로 고유한 호환성 테스트를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-206">You must perform your own compatibility testing with the version of Electron your product uses.</span></span> <span data-ttu-id="1d8e6-207">다음 섹션에서 [이전 브라우저 지원](#sob) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="1d8e6-207">See [Supporting older browsers](#sob) in the following section.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1d8e6-208">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1d8e6-208">Additional resources</span></span>

* [<span data-ttu-id="1d8e6-209">Chromium 블로그: 개발자: 새 SameSite를 사용할 준비가 되었습니다. 보안 쿠키 설정</span><span class="sxs-lookup"><span data-stu-id="1d8e6-209">Chromium Blog:Developers: Get Ready for New SameSite=None; Secure Cookie Settings</span></span>](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [<span data-ttu-id="1d8e6-210">SameSite 쿠키 설명</span><span class="sxs-lookup"><span data-stu-id="1d8e6-210">SameSite cookies explained</span></span>](https://web.dev/samesite-cookies-explained/)
* [<span data-ttu-id="1d8e6-211">OWIN 및 System.web 응답 쿠키 통합 문제</span><span class="sxs-lookup"><span data-stu-id="1d8e6-211">OWIN and System.Web response cookie integration issues</span></span>](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues)
