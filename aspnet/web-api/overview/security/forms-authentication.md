---
uid: web-api/overview/security/forms-authentication
title: ASP.NET Web API의 폼 인증 | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API에서 폼 인증을 사용 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 12/12/2012
ms.assetid: 9f06c1f2-ffaa-4831-94a0-2e4a3befdf07
msc.legacyurl: /web-api/overview/security/forms-authentication
msc.type: authoredcontent
ms.openlocfilehash: 147bfab76e48497f35a72b28cd935f40ec4193bf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484379"
---
# <a name="forms-authentication-in-aspnet-web-api"></a><span data-ttu-id="f206b-103">ASP.NET Web API의 폼 인증</span><span class="sxs-lookup"><span data-stu-id="f206b-103">Forms Authentication in ASP.NET Web API</span></span>

<span data-ttu-id="f206b-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="f206b-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="f206b-105">폼 인증은 HTML 폼을 사용 하 여 사용자의 자격 증명을 서버에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f206b-105">Forms authentication uses an HTML form to send the user's credentials to the server.</span></span> <span data-ttu-id="f206b-106">인터넷 표준이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f206b-106">It is not an Internet standard.</span></span> <span data-ttu-id="f206b-107">폼 인증은 사용자가 HTML 양식과 상호 작용할 수 있도록 웹 응용 프로그램에서 호출 되는 웹 Api에만 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="f206b-107">Forms authentication is only appropriate for web APIs that are called from a web application, so that the user can interact with the HTML form.</span></span>

| <span data-ttu-id="f206b-108">장점</span><span class="sxs-lookup"><span data-stu-id="f206b-108">Advantages</span></span> | <span data-ttu-id="f206b-109">단점</span><span class="sxs-lookup"><span data-stu-id="f206b-109">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="f206b-110">-간편한 구현: ASP.NET에 기본 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f206b-110">- Easy to implement: Built into ASP.NET.</span></span> <span data-ttu-id="f206b-111">-ASP.NET 멤버 자격 공급자를 사용 하 여 사용자 계정을 쉽게 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f206b-111">- Uses ASP.NET membership provider, which makes it easy to manage user accounts.</span></span> | <span data-ttu-id="f206b-112">-표준 HTTP 인증 메커니즘이 아닙니다. 표준 권한 부여 헤더 대신 HTTP 쿠키를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f206b-112">- Not a standard HTTP authentication mechanism; uses HTTP cookies instead of the standard Authorization header.</span></span> <span data-ttu-id="f206b-113">-브라우저 클라이언트가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f206b-113">- Requires a browser client.</span></span> <span data-ttu-id="f206b-114">-자격 증명이 일반 텍스트로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f206b-114">- Credentials are sent as plaintext.</span></span> <span data-ttu-id="f206b-115">-CSRF (교차 사이트 요청 위조)에 취약 합니다. CSRF 측정값이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f206b-115">- Vulnerable to cross-site request forgery (CSRF); requires anti-CSRF measures.</span></span> <span data-ttu-id="f206b-116">-비 브라우저 클라이언트에서 사용 하기 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="f206b-116">- Difficult to use from nonbrowser clients.</span></span> <span data-ttu-id="f206b-117">로그인 하려면 브라우저가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f206b-117">Login requires a browser.</span></span> <span data-ttu-id="f206b-118">-사용자 자격 증명이 요청에서 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f206b-118">- User credentials are sent in the request.</span></span> <span data-ttu-id="f206b-119">-일부 사용자가 쿠키를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f206b-119">- Some users disable cookies.</span></span> |

<span data-ttu-id="f206b-120">간단히 말해서 ASP.NET의 폼 인증은 다음과 같이 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f206b-120">Briefly, forms authentication in ASP.NET works like this:</span></span>

1. <span data-ttu-id="f206b-121">클라이언트가 인증을 요구 하는 리소스를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="f206b-121">The client requests a resource that requires authentication.</span></span>
2. <span data-ttu-id="f206b-122">사용자가 인증 되지 않은 경우 서버는 HTTP 302 (찾음)을 반환 하 고 로그인 페이지로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="f206b-122">If the user is not authenticated, the server returns HTTP 302 (Found) and redirects to a login page.</span></span>
3. <span data-ttu-id="f206b-123">사용자가 자격 증명을 입력 하 고 양식을 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="f206b-123">The user enters credentials and submits the form.</span></span>
4. <span data-ttu-id="f206b-124">서버는 다시 원래 URI로 리디렉션하는 다른 HTTP 302을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f206b-124">The server returns another HTTP 302 that redirects back to the original URI.</span></span> <span data-ttu-id="f206b-125">이 응답에는 인증 쿠키가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f206b-125">This response includes an authentication cookie.</span></span>
5. <span data-ttu-id="f206b-126">클라이언트에서 리소스를 다시 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="f206b-126">The client requests the resource again.</span></span> <span data-ttu-id="f206b-127">요청은 인증 쿠키를 포함 하므로 서버에서 요청을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="f206b-127">The request includes the authentication cookie, so the server grants the request.</span></span>

![](forms-authentication/_static/image1.png)

<span data-ttu-id="f206b-128">자세한 내용은 [폼 인증 개요](../../../web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs.md) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f206b-128">For more information, see [An Overview of Forms Authentication.](../../../web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs.md)</span></span>

## <a name="using-forms-authentication-with-web-api"></a><span data-ttu-id="f206b-129">Web API에서 폼 인증 사용</span><span class="sxs-lookup"><span data-stu-id="f206b-129">Using Forms Authentication with Web API</span></span>

<span data-ttu-id="f206b-130">폼 인증을 사용 하는 응용 프로그램을 만들려면 MVC 4 프로젝트 마법사에서 "인터넷 응용 프로그램" 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f206b-130">To create an application that uses forms authentication, select the "Internet Application" template in the MVC 4 project wizard.</span></span> <span data-ttu-id="f206b-131">이 템플릿은 계정 관리를 위한 MVC 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f206b-131">This template creates MVC controllers for account management.</span></span> <span data-ttu-id="f206b-132">ASP.NET-2012 업데이트에서 사용할 수 있는 "단일 페이지 응용 프로그램" 템플릿을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f206b-132">You can also use the "Single Page Application" template, available in the ASP.NET Fall 2012 Update.</span></span>

<span data-ttu-id="f206b-133">Web API 컨트롤러에서 [[권한 부여] 특성 사용](authentication-and-authorization-in-aspnet-web-api.md#auth3)에 설명 된 대로 `[Authorize]` 특성을 사용 하 여 액세스를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f206b-133">In your web API controllers, you can restrict access by using the `[Authorize]` attribute, as described in [Using the [Authorize] Attribute](authentication-and-authorization-in-aspnet-web-api.md#auth3).</span></span>

<span data-ttu-id="f206b-134">폼 인증은 세션 쿠키를 사용 하 여 요청을 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="f206b-134">Forms-authentication uses a session cookie to authenticate requests.</span></span> <span data-ttu-id="f206b-135">브라우저는 모든 관련 쿠키를 대상 웹 사이트로 자동으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f206b-135">Browsers automatically send all relevant cookies to the destination web site.</span></span> <span data-ttu-id="f206b-136">이 기능을 통해 폼 인증은 CSRF (교차 사이트 요청 위조) 공격에 취약할 수 있습니다. [CSRF (교차 사이트 요청 위조) 공격 방지](preventing-cross-site-request-forgery-csrf-attacks.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f206b-136">This feature makes forms authentication potentially vulnerable to cross-site request forgery (CSRF) attacks See [Preventing Cross-Site Request Forgery (CSRF) Attacks](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>

<span data-ttu-id="f206b-137">폼 인증에서는 사용자의 자격 증명을 암호화 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f206b-137">Forms authentication does not encrypt the user's credentials.</span></span> <span data-ttu-id="f206b-138">따라서 폼 인증은 SSL과 함께 사용 하지 않는 한 안전 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f206b-138">Therefore, forms authentication is not secure unless used with SSL.</span></span> <span data-ttu-id="f206b-139">[WEB API에서 SSL](working-with-ssl-in-web-api.md)사용을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f206b-139">See [Working with SSL in Web API](working-with-ssl-in-web-api.md).</span></span>
