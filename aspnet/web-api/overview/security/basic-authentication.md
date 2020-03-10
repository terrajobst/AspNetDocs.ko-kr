---
uid: web-api/overview/security/basic-authentication
title: ASP.NET Web API의 기본 인증 | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API에서 기본 인증을 사용 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 10/02/2014
ms.assetid: 41423767-0021-47c3-9e53-0021b457c39f
msc.legacyurl: /web-api/overview/security/basic-authentication
msc.type: authoredcontent
ms.openlocfilehash: 1470bd4b5abd5199b9a5105973b053812d643351
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447635"
---
# <a name="basic-authentication-in-aspnet-web-api"></a><span data-ttu-id="85b67-103">ASP.NET Web API의 기본 인증</span><span class="sxs-lookup"><span data-stu-id="85b67-103">Basic Authentication in ASP.NET Web API</span></span>

<span data-ttu-id="85b67-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="85b67-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="85b67-105">기본 인증은 [RFC 2617, HTTP 인증: 기본 및 다이제스트 액세스 인증](http://www.ietf.org/rfc/rfc2617.txt)에 정의 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-105">Basic authentication is defined in [RFC 2617, HTTP Authentication: Basic and Digest Access Authentication](http://www.ietf.org/rfc/rfc2617.txt).</span></span>

<span data-ttu-id="85b67-106">단점</span><span class="sxs-lookup"><span data-stu-id="85b67-106">Disadvantages</span></span>

- <span data-ttu-id="85b67-107">사용자 자격 증명은 요청에서 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-107">User credentials are sent in the request.</span></span>
- <span data-ttu-id="85b67-108">자격 증명은 일반 텍스트로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-108">Credentials are sent as plaintext.</span></span>
- <span data-ttu-id="85b67-109">자격 증명은 모든 요청과 함께 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-109">Credentials are sent with every request.</span></span>
- <span data-ttu-id="85b67-110">브라우저 세션을 종료 하는 경우를 제외 하 고는 로그 아웃 하는 방법이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-110">No way to log out, except by ending the browser session.</span></span>
- <span data-ttu-id="85b67-111">CSRF (교차 사이트 요청 위조)에 취약 합니다. CSRF 측정값이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-111">Vulnerable to cross-site request forgery (CSRF); requires anti-CSRF measures.</span></span>

<span data-ttu-id="85b67-112">장점</span><span class="sxs-lookup"><span data-stu-id="85b67-112">Advantages</span></span>

- <span data-ttu-id="85b67-113">인터넷 표준.</span><span class="sxs-lookup"><span data-stu-id="85b67-113">Internet standard.</span></span>
- <span data-ttu-id="85b67-114">모든 주요 브라우저에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-114">Supported by all major browsers.</span></span>
- <span data-ttu-id="85b67-115">비교적 간단한 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-115">Relatively simple protocol.</span></span>

<span data-ttu-id="85b67-116">기본 인증은 다음과 같이 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-116">Basic authentication works as follows:</span></span>

1. <span data-ttu-id="85b67-117">요청에 인증이 필요한 경우 서버는 401 (권한 없음)을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-117">If a request requires authentication, the server returns 401 (Unauthorized).</span></span> <span data-ttu-id="85b67-118">응답에는 서버가 기본 인증을 지원함을 나타내는 WWW 인증 헤더가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-118">The response includes a WWW-Authenticate header, indicating the server supports Basic authentication.</span></span>
2. <span data-ttu-id="85b67-119">클라이언트는 인증 헤더의 클라이언트 자격 증명을 사용 하 여 다른 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-119">The client sends another request, with the client credentials in the Authorization header.</span></span> <span data-ttu-id="85b67-120">자격 증명은 문자열 "이름: 암호", base64 인코딩 형식으로 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-120">The credentials are formatted as the string "name:password", base64-encoded.</span></span> <span data-ttu-id="85b67-121">자격 증명은 암호화 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-121">The credentials are not encrypted.</span></span>

<span data-ttu-id="85b67-122">기본 인증은 "영역"의 컨텍스트 내에서 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-122">Basic authentication is performed within the context of a "realm."</span></span> <span data-ttu-id="85b67-123">서버에는 WWW-인증 헤더에 영역 이름이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-123">The server includes the name of the realm in the WWW-Authenticate header.</span></span> <span data-ttu-id="85b67-124">사용자의 자격 증명은 해당 영역 내에서 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-124">The user's credentials are valid within that realm.</span></span> <span data-ttu-id="85b67-125">영역의 정확한 범위는 서버에 의해 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-125">The exact scope of a realm is defined by the server.</span></span> <span data-ttu-id="85b67-126">예를 들어 리소스를 분할 하기 위해 여러 영역을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-126">For example, you might define several realms in order to partition resources.</span></span>

![](basic-authentication/_static/image1.png)

<span data-ttu-id="85b67-127">자격 증명이 암호화 되지 않은 상태로 전송 되기 때문에 기본 인증은 HTTPS를 통해서만 안전 합니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-127">Because the credentials are sent unencrypted, Basic authentication is only secure over HTTPS.</span></span> <span data-ttu-id="85b67-128">[WEB API에서 SSL](working-with-ssl-in-web-api.md)사용을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="85b67-128">See [Working with SSL in Web API](working-with-ssl-in-web-api.md).</span></span>

<span data-ttu-id="85b67-129">기본 인증도 CSRF 공격에 취약 합니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-129">Basic authentication is also vulnerable to CSRF attacks.</span></span> <span data-ttu-id="85b67-130">사용자가 자격 증명을 입력 한 후에는 세션 기간 동안 브라우저가 동일한 도메인에 대 한 후속 요청을 자동으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-130">After the user enters credentials, the browser automatically sends them on subsequent requests to the same domain, for the duration of the session.</span></span> <span data-ttu-id="85b67-131">여기에는 AJAX 요청이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-131">This includes AJAX requests.</span></span> <span data-ttu-id="85b67-132">[CSRF (교차 사이트 요청 위조) 공격 방지를](preventing-cross-site-request-forgery-csrf-attacks.md)참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="85b67-132">See [Preventing Cross-Site Request Forgery (CSRF) Attacks](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>

## <a name="basic-authentication-with-iis"></a><span data-ttu-id="85b67-133">IIS를 사용 하 여 기본 인증</span><span class="sxs-lookup"><span data-stu-id="85b67-133">Basic Authentication with IIS</span></span>

<span data-ttu-id="85b67-134">IIS는 기본 인증을 지원 하지만, 사용자가 Windows 자격 증명에 대해 인증 되는 주의 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-134">IIS supports Basic authentication, but there is a caveat: The user is authenticated against their Windows credentials.</span></span> <span data-ttu-id="85b67-135">즉, 사용자가 서버 도메인에 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-135">That means the user must have an account on the server's domain.</span></span> <span data-ttu-id="85b67-136">공용 웹 사이트의 경우 일반적으로 ASP.NET 멤버 자격 공급자에 대해 인증을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-136">For a public-facing web site, you typically want to authenticate against an ASP.NET membership provider.</span></span>

<span data-ttu-id="85b67-137">IIS를 사용 하 여 기본 인증을 사용 하도록 설정 하려면 ASP.NET 프로젝트의 Web.config에서 인증 모드를 "Windows"로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-137">To enable Basic authentication using IIS, set the authentication mode to "Windows" in the Web.config of your ASP.NET project:</span></span>

[!code-xml[Main](basic-authentication/samples/sample1.xml)]

<span data-ttu-id="85b67-138">이 모드에서 IIS는 Windows 자격 증명을 사용 하 여 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-138">In this mode, IIS uses Windows credentials to authenticate.</span></span> <span data-ttu-id="85b67-139">또한 IIS에서 기본 인증을 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-139">In addition, you must enable Basic authentication in IIS.</span></span> <span data-ttu-id="85b67-140">IIS 관리자에서 기능 보기로 이동 하 고, 인증을 선택 하 고, 기본 인증을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-140">In IIS Manager, go to Features View, select Authentication, and enable Basic authentication.</span></span>

![](basic-authentication/_static/image2.png)

<span data-ttu-id="85b67-141">웹 API 프로젝트에서 인증이 필요한 컨트롤러 작업에 대 한 `[Authorize]` 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-141">In your Web API project, add the `[Authorize]` attribute for any controller actions that need authentication.</span></span>

<span data-ttu-id="85b67-142">클라이언트는 요청에 권한 부여 헤더를 설정 하 여 자신을 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-142">A client authenticates itself by setting the Authorization header in the request.</span></span> <span data-ttu-id="85b67-143">Browser 클라이언트는이 단계를 자동으로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-143">Browser clients perform this step automatically.</span></span> <span data-ttu-id="85b67-144">비 브라우저 클라이언트는 헤더를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-144">Nonbrowser clients will need to set the header.</span></span>

## <a name="basic-authentication-with-custom-membership"></a><span data-ttu-id="85b67-145">사용자 지정 멤버 자격으로 기본 인증</span><span class="sxs-lookup"><span data-stu-id="85b67-145">Basic Authentication with Custom Membership</span></span>

<span data-ttu-id="85b67-146">앞서 언급 했 듯이 IIS에 기본 제공 되는 인증은 Windows 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-146">As mentioned, the Basic Authentication built into IIS uses Windows credentials.</span></span> <span data-ttu-id="85b67-147">즉, 호스팅 서버에서 사용자에 대 한 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-147">That means you need to create accounts for your users on the hosting server.</span></span> <span data-ttu-id="85b67-148">그러나 인터넷 응용 프로그램의 경우 사용자 계정은 일반적으로 외부 데이터베이스에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-148">But for an internet application, user accounts are typically stored in an external database.</span></span>

<span data-ttu-id="85b67-149">다음 코드에서는 기본 인증을 수행 하는 HTTP 모듈을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-149">The following code how an HTTP module that performs Basic Authentication.</span></span> <span data-ttu-id="85b67-150">이 예제의 더미 메서드인 `CheckPassword` 메서드를 대체 하 여 ASP.NET 멤버 자격 공급자를 쉽게 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-150">You can easily plug in an ASP.NET membership provider by replacing the `CheckPassword` method, which is a dummy method in this example.</span></span>

<span data-ttu-id="85b67-151">Web API 2에서는 HTTP 모듈 대신 [인증 필터](authentication-filters.md) 또는 [OWIN 미들웨어](../../../aspnet/overview/owin-and-katana/index.md)를 작성 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-151">In Web API 2, you should consider writing an [authentication filter](authentication-filters.md) or [OWIN middleware](../../../aspnet/overview/owin-and-katana/index.md), instead of an HTTP module.</span></span>

[!code-csharp[Main](basic-authentication/samples/sample2.cs)]

<span data-ttu-id="85b67-152">HTTP 모듈을 사용 하도록 설정 하려면 **system.webserver** 섹션의 web.config 파일에 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-152">To enable the HTTP module, add the following to your web.config file in the **system.webServer** section:</span></span>

[!code-xml[Main](basic-authentication/samples/sample3.xml?highlight=4)]

<span data-ttu-id="85b67-153">"해당 Assemblyname"을 어셈블리 이름으로 바꿉니다 ("dll" 확장명 포함 안 함).</span><span class="sxs-lookup"><span data-stu-id="85b67-153">Replace "YourAssemblyName" with the name of the assembly (not including the "dll" extension).</span></span>

<span data-ttu-id="85b67-154">양식 또는 Windows 인증 등의 다른 인증 체계를 사용 하지 않도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85b67-154">You should disable other authentication schemes, such as Forms or Windows auth.</span></span>
