---
uid: web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
title: ASP.NET MVC에서 CSRF (교차 사이트 요청 위조) 공격 방지
author: MikeWasson
description: CSRF (교차 사이트 요청 위조) 공격과 ASP.NET 웹 MVC에서 CSRF 측정값을 구현 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 12/12/2012
ms.assetid: 81d46f14-8f48-4d8c-830d-cc8d594dc11b
msc.legacyurl: /web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
msc.type: authoredcontent
ms.openlocfilehash: 5fb0f8bcc9e587ba4fbbf2b857d3bf7adcaafb94
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447113"
---
# <a name="preventing-cross-site-request-forgery-csrf-attacks-in-aspnet-mvc-application"></a><span data-ttu-id="bf6f2-103">ASP.NET MVC 응용 프로그램에서 CSRF (교차 사이트 요청 위조) 공격 방지</span><span class="sxs-lookup"><span data-stu-id="bf6f2-103">Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET MVC Application</span></span>

<span data-ttu-id="bf6f2-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="bf6f2-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="bf6f2-105">CSRF (교차 사이트 요청 위조)는 악의적인 사이트에서 사용자가 현재 로그인 한 취약 한 사이트로 요청을 보내는 공격입니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-105">Cross-Site Request Forgery (CSRF) is an attack where a malicious site sends a request to a vulnerable site where the user is currently logged in</span></span>

<span data-ttu-id="bf6f2-106">CSRF 공격의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-106">Here is an example of a CSRF attack:</span></span>

1. <span data-ttu-id="bf6f2-107">사용자가 폼 인증을 사용 하 여 `www.example.com`에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-107">A user logs into `www.example.com` using forms authentication.</span></span>
2. <span data-ttu-id="bf6f2-108">서버에서 사용자를 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-108">The server authenticates the user.</span></span> <span data-ttu-id="bf6f2-109">서버 응답에는 인증 쿠키가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-109">The response from the server includes an authentication cookie.</span></span>
3. <span data-ttu-id="bf6f2-110">로그 아웃 하지 않으면 사용자가 악성 웹 사이트를 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-110">Without logging out, the user visits a malicious web site.</span></span> <span data-ttu-id="bf6f2-111">이 악의적인 사이트는 다음과 같은 HTML 양식을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-111">This malicious site contains the following HTML form:</span></span> 

    [!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample1.html)]

    <span data-ttu-id="bf6f2-112">양식 작업은 악의적인 사이트가 아닌 취약 한 사이트로 게시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-112">Notice that the form action posts to the vulnerable site, not to the malicious site.</span></span> <span data-ttu-id="bf6f2-113">CSRF의 "교차 사이트" 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-113">This is the "cross-site" part of CSRF.</span></span>
4. <span data-ttu-id="bf6f2-114">사용자가 제출 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-114">The user clicks the submit button.</span></span> <span data-ttu-id="bf6f2-115">브라우저에는 요청과 함께 인증 쿠키가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-115">The browser includes the authentication cookie with the request.</span></span>
5. <span data-ttu-id="bf6f2-116">요청은 사용자의 인증 컨텍스트를 사용 하 여 서버에서 실행 되 고 인증 된 사용자가 수행할 수 있는 모든 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-116">The request runs on the server with the user's authentication context, and can do anything that an authenticated user is allowed to do.</span></span>

<span data-ttu-id="bf6f2-117">이 예에서는 사용자가 양식 단추를 클릭 해야 하지만 악성 페이지는 양식을 자동으로 전송 하는 스크립트를 쉽게 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-117">Although this example requires the user to click the form button, the malicious page could just as easily run a script that submits the form automatically.</span></span> <span data-ttu-id="bf6f2-118">또한 SSL을 사용 하더라도 악의적인 사이트에서 "https://" 요청을 보낼 수 있으므로 CSRF 공격을 방지 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-118">Moreover, using SSL does not prevent a CSRF attack, because the malicious site can send an "https://" request.</span></span>

<span data-ttu-id="bf6f2-119">일반적으로 브라우저는 대상 웹 사이트에 관련 된 모든 쿠키를 보내기 때문에 인증에 쿠키를 사용 하는 웹 사이트에 대해 CSRF 공격을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-119">Typically, CSRF attacks are possible against web sites that use cookies for authentication, because browsers send all relevant cookies to the destination web site.</span></span> <span data-ttu-id="bf6f2-120">그러나 CSRF 공격은 쿠키를 악용 하는 것으로 제한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-120">However, CSRF attacks are not limited to exploiting cookies.</span></span> <span data-ttu-id="bf6f2-121">예를 들어, 기본 및 다이제스트 인증에도 취약 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-121">For example, Basic and Digest authentication are also vulnerable.</span></span> <span data-ttu-id="bf6f2-122">사용자가 기본 또는 다이제스트 인증을 사용 하 여 로그인 한 후</span><span class="sxs-lookup"><span data-stu-id="bf6f2-122">After a user logs in with Basic or Digest authentication.</span></span> <span data-ttu-id="bf6f2-123">브라우저는 세션이 종료 될 때까지 자격 증명을 자동으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-123">the browser automatically sends the credentials until the session ends.</span></span>

## <a name="anti-forgery-tokens"></a><span data-ttu-id="bf6f2-124">위조 방지 토큰</span><span class="sxs-lookup"><span data-stu-id="bf6f2-124">Anti-Forgery Tokens</span></span>

<span data-ttu-id="bf6f2-125">CSRF 공격을 방지 하기 위해 ASP.NET MVC는 *요청 확인 토큰이*라고도 하는 위조 방지 토큰을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-125">To help prevent CSRF attacks, ASP.NET MVC uses anti-forgery tokens, also called *request verification tokens*.</span></span>

1. <span data-ttu-id="bf6f2-126">클라이언트는 폼이 포함 된 HTML 페이지를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-126">The client requests an HTML page that contains a form.</span></span>
2. <span data-ttu-id="bf6f2-127">서버에는 응답에 두 개의 토큰이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-127">The server includes two tokens in the response.</span></span> <span data-ttu-id="bf6f2-128">하나의 토큰이 쿠키로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-128">One token is sent as a cookie.</span></span> <span data-ttu-id="bf6f2-129">다른는 숨겨진 양식 필드에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-129">The other is placed in a hidden form field.</span></span> <span data-ttu-id="bf6f2-130">토큰은 악의적 사용자가 값을 추측할 수 없도록 임의로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-130">The tokens are generated randomly so that an adversary cannot guess the values.</span></span>
3. <span data-ttu-id="bf6f2-131">클라이언트는 양식을 전송할 때 두 토큰을 모두 서버로 다시 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-131">When the client submits the form, it must send both tokens back to the server.</span></span> <span data-ttu-id="bf6f2-132">클라이언트는 쿠키 토큰을 쿠키로 보내고 양식 토큰을 양식 데이터 내부에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-132">The client sends the cookie token as a cookie, and it sends the form token inside the form data.</span></span> <span data-ttu-id="bf6f2-133">사용자가 양식을 전송할 때 브라우저 클라이언트에서 자동으로이를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-133">(A browser client automatically does this when the user submits the form.)</span></span>
4. <span data-ttu-id="bf6f2-134">요청에 두 토큰이 모두 포함 되어 있지 않으면 서버에서 요청을 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-134">If a request does not include both tokens, the server disallows the request.</span></span>

<span data-ttu-id="bf6f2-135">다음은 숨겨진 폼 토큰을 사용 하는 HTML 폼의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-135">Here is an example of an HTML form with a hidden form token:</span></span>

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample2.html)]

<span data-ttu-id="bf6f2-136">위조 방지 토큰은 동일한 원본 정책으로 인해 악의적인 페이지가 사용자의 토큰을 읽을 수 없기 때문에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-136">Anti-forgery tokens work because the malicious page cannot read the user's tokens, due to same-origin policies.</span></span> <span data-ttu-id="bf6f2-137">[동일한 원본 정책을](http://www.w3.org/Security/wiki/Same_Origin_Policy) 통해 서로 다른 두 사이트에서 호스팅되는 문서는 서로의 내용에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-137">([Same-origin policies](http://www.w3.org/Security/wiki/Same_Origin_Policy) prevent documents hosted on two different sites from accessing each other's content.</span></span> <span data-ttu-id="bf6f2-138">따라서 이전 예제에서 악의적인 페이지는 example.com에 요청을 보낼 수 있지만 응답을 읽을 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-138">So in the earlier example, the malicious page can send requests to example.com, but it cannot read the response.)</span></span>

<span data-ttu-id="bf6f2-139">CSRF 공격을 방지 하려면 브라우저에서 사용자가 로그인 한 후 자격 증명을 자동으로 보내는 인증 프로토콜을 사용 하 여 위조 방지 토큰을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-139">To prevent CSRF attacks, use anti-forgery tokens with any authentication protocol where the browser silently sends credentials after the user logs in.</span></span> <span data-ttu-id="bf6f2-140">여기에는 기본 및 다이제스트 인증과 같은 프로토콜 뿐만 아니라 폼 인증과 같은 쿠키 기반 인증 프로토콜도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-140">This includes cookie-based authentication protocols, such as forms authentication, as well as protocols such as Basic and Digest authentication.</span></span>

<span data-ttu-id="bf6f2-141">안전 하지 않은 메서드 (POST, PUT, DELETE)에 대해 위조 방지 토큰이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-141">You should require anti-forgery tokens for any nonsafe methods (POST, PUT, DELETE).</span></span> <span data-ttu-id="bf6f2-142">또한 safe 메서드 (GET, HEAD)에 부작용이 없는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-142">Also, make sure that safe methods (GET, HEAD) do not have any side effects.</span></span> <span data-ttu-id="bf6f2-143">또한 CORS 또는 JSONP 같은 도메인 간 지원을 사용 하도록 설정 하는 경우 GET과 같은 안전한 방법도 CSRF 공격에 취약할 수 있으므로 공격자가 잠재적으로 중요 한 데이터를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-143">Moreover, if you enable cross-domain support, such as CORS or JSONP, then even safe methods like GET are potentially vulnerable to CSRF attacks, allowing the attacker to read potentially sensitive data.</span></span>

## <a name="anti-forgery-tokens-in-aspnet-mvc"></a><span data-ttu-id="bf6f2-144">ASP.NET MVC의 위조 방지 토큰</span><span class="sxs-lookup"><span data-stu-id="bf6f2-144">Anti-Forgery Tokens in ASP.NET MVC</span></span>

<span data-ttu-id="bf6f2-145">위조 방지 토큰을 Razor 페이지에 추가 하려면 **AntiForgeryToken** 도우미 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-145">To add the anti-forgery tokens to a Razor page, use the **HtmlHelper.AntiForgeryToken** helper method:</span></span>

[!code-cshtml[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample3.cshtml)]

<span data-ttu-id="bf6f2-146">이 메서드는 숨겨진 양식 필드를 추가 하 고 쿠키 토큰도 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-146">This method adds the hidden form field and also sets the cookie token.</span></span>

## <a name="anti-csrf-and-ajax"></a><span data-ttu-id="bf6f2-147">CSRF 및 AJAX 방지</span><span class="sxs-lookup"><span data-stu-id="bf6f2-147">Anti-CSRF and AJAX</span></span>

<span data-ttu-id="bf6f2-148">Ajax 요청은 HTML 양식 데이터가 아닌 JSON 데이터를 보낼 수 있기 때문에 폼 토큰은 AJAX 요청에 문제가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-148">The form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="bf6f2-149">한 가지 솔루션은 사용자 지정 HTTP 헤더에 토큰을 보내는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-149">One solution is to send the tokens in a custom HTTP header.</span></span> <span data-ttu-id="bf6f2-150">다음 코드는 Razor 구문을 사용하여 토큰을 생성한 다음 AJAX 요청에 토큰을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-150">The following code uses Razor syntax to generate the tokens, and then adds the tokens to an AJAX request.</span></span> <span data-ttu-id="bf6f2-151">토큰은 **위조 방지. GetTokens**를 호출 하 여 서버에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-151">The tokens are generated at the server by calling **AntiForgery.GetTokens**.</span></span>

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample4.html)]

<span data-ttu-id="bf6f2-152">요청을 처리하는 경우 요청 헤더에서 토큰을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-152">When you process the request, extract the tokens from the request header.</span></span> <span data-ttu-id="bf6f2-153">그런 다음, **위조 방지. validate** 메서드를 호출 하 여 토큰의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-153">Then call the **AntiForgery.Validate** method to validate the tokens.</span></span> <span data-ttu-id="bf6f2-154">**Validate** 메서드는 토큰이 유효 하지 않을 경우 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf6f2-154">The **Validate** method throws an exception if the tokens are not valid.</span></span>

[!code-csharp[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample5.cs)]
