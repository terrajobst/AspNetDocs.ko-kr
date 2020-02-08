---
uid: web-api/overview/security/authentication-filters
title: ASP.NET Web API 2의 인증 필터 | Microsoft Docs
author: MikeWasson
description: 인증 필터는 HTTP 요청을 인증 하는 구성 요소입니다. Web API 2 및 MVC 5는 모두 인증 필터를 지원 하지만 약간 다릅니다.
ms.author: riande
ms.date: 09/25/2014
ms.assetid: b9882e53-b3ca-4def-89b0-322846973ccb
msc.legacyurl: /web-api/overview/security/authentication-filters
msc.type: authoredcontent
ms.openlocfilehash: 2ef9e62a6c634237e920b6d7aba2127b835f959d
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/07/2020
ms.locfileid: "77075075"
---
# <a name="authentication-filters-in-aspnet-web-api-2"></a><span data-ttu-id="bd493-104">ASP.NET Web API 2의 인증 필터</span><span class="sxs-lookup"><span data-stu-id="bd493-104">Authentication Filters in ASP.NET Web API 2</span></span>

<span data-ttu-id="bd493-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="bd493-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="bd493-106">인증 필터는 HTTP 요청을 인증 하는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-106">An authentication filter is a component that authenticates an HTTP request.</span></span> <span data-ttu-id="bd493-107">Web API 2 및 MVC 5는 모두 인증 필터를 지원 하지만 대부분 필터 인터페이스에 대 한 명명 규칙에 따라 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-107">Web API 2 and MVC 5 both support authentication filters, but they differ slightly, mostly in the naming conventions for the filter interface.</span></span> <span data-ttu-id="bd493-108">이 항목에서는 Web API 인증 필터에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-108">This topic describes Web API authentication filters.</span></span>

<span data-ttu-id="bd493-109">인증 필터를 사용 하면 개별 컨트롤러 또는 작업에 대 한 인증 체계를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-109">Authentication filters let you set an authentication scheme for individual controllers or actions.</span></span> <span data-ttu-id="bd493-110">이런 방식으로 앱은 다양 한 HTTP 리소스에 대해 서로 다른 인증 메커니즘을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-110">That way, your app can support different authentication mechanisms for different HTTP resources.</span></span>

<span data-ttu-id="bd493-111">이 문서에서는 [https://github.com/aspnet/samples](https://github.com/aspnet/samples)에 대 한 [기본 인증](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BasicAuthentication) 샘플의 코드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-111">In this article, I'll show code from the [Basic Authentication](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BasicAuthentication) sample on [https://github.com/aspnet/samples](https://github.com/aspnet/samples).</span></span> <span data-ttu-id="bd493-112">이 샘플에서는 HTTP 기본 액세스 인증 체계 (RFC 2617)를 구현 하는 인증 필터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-112">The sample shows an authentication filter that implements the HTTP Basic Access Authentication scheme (RFC 2617).</span></span> <span data-ttu-id="bd493-113">필터는 `IdentityBasicAuthenticationAttribute`이라는 클래스에서 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-113">The filter is implemented in a class named `IdentityBasicAuthenticationAttribute`.</span></span> <span data-ttu-id="bd493-114">예제에서 코드를 모두 표시 하지는 않습니다. 인증 필터를 작성 하는 방법을 보여 주는 부분만 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-114">I won't show all of the code from the sample, just the parts that illustrate how to write an authentication filter.</span></span>

## <a name="setting-an-authentication-filter"></a><span data-ttu-id="bd493-115">인증 필터 설정</span><span class="sxs-lookup"><span data-stu-id="bd493-115">Setting an Authentication Filter</span></span>

<span data-ttu-id="bd493-116">다른 필터와 마찬가지로 인증 필터는 포트당, 작업별 또는 모든 웹 API 컨트롤러에 전역적으로 적용 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-116">Like other filters, authentication filters can be applied per-controller, per-action, or globally to all Web API controllers.</span></span>

<span data-ttu-id="bd493-117">컨트롤러에 인증 필터를 적용 하려면 컨트롤러 클래스를 필터 특성으로 데코 레이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-117">To apply an authentication filter to a controller, decorate the controller class with the filter attribute.</span></span> <span data-ttu-id="bd493-118">다음 코드는 컨트롤러 클래스에 대 한 `[IdentityBasicAuthentication]` 필터를 설정 하 여 컨트롤러의 모든 작업에 대해 기본 인증을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-118">The following code sets the `[IdentityBasicAuthentication]` filter on a controller class, which enables Basic Authentication for all of the controller's actions.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample1.cs)]

<span data-ttu-id="bd493-119">하나의 작업에 필터를 적용 하려면 필터를 사용 하 여 작업을 데코 레이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-119">To apply the filter to one action, decorate the action with the filter.</span></span> <span data-ttu-id="bd493-120">다음 코드는 컨트롤러의 `Post` 메서드에 `[IdentityBasicAuthentication]` 필터를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-120">The following code sets the `[IdentityBasicAuthentication]` filter on the controller's `Post` method.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample2.cs)]

<span data-ttu-id="bd493-121">모든 Web API 컨트롤러에 필터를 적용 하려면이를 **Globalconfiguration. 필터**에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-121">To apply the filter to all Web API controllers, add it to **GlobalConfiguration.Filters**.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample3.cs)]

## <a name="implementing-a-web-api-authentication-filter"></a><span data-ttu-id="bd493-122">Web API 인증 필터 구현</span><span class="sxs-lookup"><span data-stu-id="bd493-122">Implementing a Web API Authentication Filter</span></span>

<span data-ttu-id="bd493-123">Web API에서 인증 필터는 System.web. p. [i](https://msdn.microsoft.com/library/system.web.http.filters.iauthenticationfilter.aspx) o p.</span><span class="sxs-lookup"><span data-stu-id="bd493-123">In Web API, authentication filters implement the [System.Web.Http.Filters.IAuthenticationFilter](https://msdn.microsoft.com/library/system.web.http.filters.iauthenticationfilter.aspx) interface.</span></span> <span data-ttu-id="bd493-124">또한 특성으로 적용 하기 위해 **system.object**에서 상속 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-124">They should also inherit from **System.Attribute**, in order to be applied as attributes.</span></span>

<span data-ttu-id="bd493-125">**Iauthenticationfilter** 인터페이스에는 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-125">The **IAuthenticationFilter** interface has two methods:</span></span>

- <span data-ttu-id="bd493-126">**AuthenticateAsync** 는 요청에서 자격 증명의 유효성을 검사 하 여 요청을 인증 합니다 (있는 경우).</span><span class="sxs-lookup"><span data-stu-id="bd493-126">**AuthenticateAsync** authenticates the request by validating credentials in the request, if present.</span></span>
- <span data-ttu-id="bd493-127">**ChallengeAsync** 은 필요한 경우 HTTP 응답에 인증 챌린지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-127">**ChallengeAsync** adds an authentication challenge to the HTTP response, if needed.</span></span>

<span data-ttu-id="bd493-128">이러한 메서드는 [rfc 2612](http://tools.ietf.org/html/rfc2616) 및 [rfc 2617](http://tools.ietf.org/html/rfc2617)에 정의 된 인증 흐름에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-128">These methods correspond to the authentication flow defined in [RFC 2612](http://tools.ietf.org/html/rfc2616) and [RFC 2617](http://tools.ietf.org/html/rfc2617):</span></span>

1. <span data-ttu-id="bd493-129">클라이언트는 인증 헤더에 자격 증명을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-129">The client sends credentials in the Authorization header.</span></span> <span data-ttu-id="bd493-130">이는 일반적으로 클라이언트가 서버 로부터 401 (권한 없음) 응답을 받은 후에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-130">This typically happens after the client receives a 401 (Unauthorized) response from the server.</span></span> <span data-ttu-id="bd493-131">그러나 클라이언트는 401을 받은 후 뿐만 아니라 모든 요청과 함께 자격 증명을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-131">However, a client can send credentials with any request, not just after getting a 401.</span></span>
2. <span data-ttu-id="bd493-132">서버에서 자격 증명을 허용 하지 않는 경우 401 (권한 없음) 응답을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-132">If the server does not accept the credentials, it returns a 401 (Unauthorized) response.</span></span> <span data-ttu-id="bd493-133">응답에는 하나 이상의 과제가 포함 된 Www 인증 헤더가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-133">The response includes a Www-Authenticate header that contains one or more challenges.</span></span> <span data-ttu-id="bd493-134">각 챌린지는 서버에서 인식 하는 인증 체계를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-134">Each challenge specifies an authentication scheme recognized by the server.</span></span>

<span data-ttu-id="bd493-135">서버는 익명 요청에서 401을 반환할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-135">The server can also return 401 from an anonymous request.</span></span> <span data-ttu-id="bd493-136">실제로 인증 프로세스를 시작 하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-136">In fact, that's typically how the authentication process is initiated:</span></span>

1. <span data-ttu-id="bd493-137">클라이언트는 익명 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-137">The client sends an anonymous request.</span></span>
2. <span data-ttu-id="bd493-138">서버는 401을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-138">The server returns 401.</span></span>
3. <span data-ttu-id="bd493-139">클라이언트는 자격 증명을 사용 하 여 요청을 다시 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-139">The clients resends the request with credentials.</span></span>

<span data-ttu-id="bd493-140">이 흐름에는 *인증* 및 *권한 부여* 단계가 모두 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-140">This flow includes both *authentication* and *authorization* steps.</span></span>

- <span data-ttu-id="bd493-141">인증에서 클라이언트의 id를 증명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-141">Authentication proves the identity of the client.</span></span>
- <span data-ttu-id="bd493-142">권한 부여는 클라이언트가 특정 리소스에 액세스할 수 있는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-142">Authorization determines whether the client can access a particular resource.</span></span>

<span data-ttu-id="bd493-143">Web API에서 인증 필터는 인증을 처리 하지만 권한 부여는 처리 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-143">In Web API, authentication filters handle authentication, but not authorization.</span></span> <span data-ttu-id="bd493-144">권한 부여 필터 또는 컨트롤러 작업 내에서 권한 부여를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-144">Authorization should be done by an authorization filter or inside the controller action.</span></span>

<span data-ttu-id="bd493-145">웹 API 2 파이프라인의 흐름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-145">Here is the flow in the Web API 2 pipeline:</span></span>

1. <span data-ttu-id="bd493-146">웹 API는 동작을 호출 하기 전에 해당 작업에 대 한 인증 필터 목록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-146">Before invoking an action, Web API creates a list of the authentication filters for that action.</span></span> <span data-ttu-id="bd493-147">여기에는 작업 범위, 컨트롤러 범위 및 전역 범위를 포함 하는 필터가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-147">This includes filters with action scope, controller scope, and global scope.</span></span>
2. <span data-ttu-id="bd493-148">웹 API는 목록의 모든 필터에 대해 **AuthenticateAsync** 를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-148">Web API calls **AuthenticateAsync** on every filter in the list.</span></span> <span data-ttu-id="bd493-149">각 필터는 요청에서 자격 증명의 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-149">Each filter can validate credentials in the request.</span></span> <span data-ttu-id="bd493-150">자격 증명의 유효성을 검사 하는 필터가 있으면이 필터는 **IPrincipal** 을 만들어 요청에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-150">If any filter successfully validates credentials, the filter creates an **IPrincipal** and attaches it to the request.</span></span> <span data-ttu-id="bd493-151">이 시점에서 필터는 오류를 트리거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-151">A filter can also trigger an error at this point.</span></span> <span data-ttu-id="bd493-152">이 경우 나머지 파이프라인은 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-152">If so, the rest of the pipeline does not run.</span></span>
3. <span data-ttu-id="bd493-153">오류가 없는 것으로 가정 하 여 요청은 파이프라인의 나머지 부분을 통해 흐릅니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-153">Assuming there is no error, the request flows through the rest of the pipeline.</span></span>
4. <span data-ttu-id="bd493-154">마지막으로 Web API는 모든 인증 필터의 **ChallengeAsync** 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-154">Finally, Web API calls every authentication filter's **ChallengeAsync** method.</span></span> <span data-ttu-id="bd493-155">필터는 필요한 경우이 메서드를 사용 하 여 응답에 챌린지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-155">Filters use this method to add a challenge to the response, if needed.</span></span> <span data-ttu-id="bd493-156">401 오류에 대 한 응답으로 발생 하는 일반적으로는 항상 그렇지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-156">Typically (but not always) that would happen in response to a 401 error.</span></span>

<span data-ttu-id="bd493-157">다음 다이어그램에서는 두 가지 가능한 사례를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-157">The following diagrams show two possible cases.</span></span> <span data-ttu-id="bd493-158">첫 번째는 인증 필터에서 요청을 성공적으로 인증 하 고, 권한 부여 필터에서 요청을 승인 하 고, 컨트롤러 작업에서 200 (OK)를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-158">In the first, the authentication filter successfully authenticates the request, an authorization filter authorizes the request, and the controller action returns 200 (OK).</span></span>

![](authentication-filters/_static/image1.png)

<span data-ttu-id="bd493-159">두 번째 예제에서는 인증 필터에서 요청을 인증 하지만 권한 부여 필터는 401 (권한 없음)을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-159">In the second example, the authentication filter authenticates the request, but the authorization filter returns 401 (Unauthorized).</span></span> <span data-ttu-id="bd493-160">이 경우 컨트롤러 작업은 호출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-160">In this case, the controller action is not invoked.</span></span> <span data-ttu-id="bd493-161">인증 필터는 Www-인증 헤더를 응답에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-161">The authentication filter adds a Www-Authenticate header to the response.</span></span>

![](authentication-filters/_static/image2.png)

<span data-ttu-id="bd493-162">예를 들어, 컨트롤러 작업에서 익명 요청을 허용 하는 경우 다른 조합을&mdash;사용할 수 있습니다. 인증 필터는 있지만 권한 부여는 없을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-162">Other combinations are possible&mdash;for example, if the controller action allows anonymous requests, you might have an authentication filter but no authorization.</span></span>

## <a name="implementing-the-authenticateasync-method"></a><span data-ttu-id="bd493-163">AuthenticateAsync 메서드 구현</span><span class="sxs-lookup"><span data-stu-id="bd493-163">Implementing the AuthenticateAsync Method</span></span>

<span data-ttu-id="bd493-164">**AuthenticateAsync** 메서드는 요청을 인증 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-164">The **AuthenticateAsync** method tries to authenticate the request.</span></span> <span data-ttu-id="bd493-165">메서드 서명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-165">Here is the method signature:</span></span>

[!code-csharp[Main](authentication-filters/samples/sample4.cs)]

<span data-ttu-id="bd493-166">**AuthenticateAsync** 메서드는 다음 중 하나를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-166">The **AuthenticateAsync** method must do one of the following:</span></span>

1. <span data-ttu-id="bd493-167">Nothing (no op).</span><span class="sxs-lookup"><span data-stu-id="bd493-167">Nothing (no-op).</span></span>
2. <span data-ttu-id="bd493-168">**IPrincipal** 을 만들고 요청에 대해 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-168">Create an **IPrincipal** and set it on the request.</span></span>
3. <span data-ttu-id="bd493-169">오류 결과를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-169">Set an error result.</span></span>

<span data-ttu-id="bd493-170">옵션 (1)은 필터에서 인식 하는 자격 증명이 요청에 없음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-170">Option (1) means the request did not have any credentials that the filter understands.</span></span> <span data-ttu-id="bd493-171">옵션 (2)은 필터가 요청을 성공적으로 인증 했음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-171">Option (2) means the filter successfully authenticated the request.</span></span> <span data-ttu-id="bd493-172">옵션 (3)은 요청에 잘못 된 자격 증명 (예: 잘못 된 암호)이 있어 오류 응답을 트리거하는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-172">Option (3) means the request had invalid credentials (like the wrong password), which triggers an error response.</span></span>

<span data-ttu-id="bd493-173">**AuthenticateAsync**구현에 대 한 일반적인 개요는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-173">Here is a general outline for implementing **AuthenticateAsync**.</span></span>

1. <span data-ttu-id="bd493-174">요청에서 자격 증명을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-174">Look for credentials in the request.</span></span>
2. <span data-ttu-id="bd493-175">자격 증명이 없는 경우 아무 작업도 수행 하지 않고 반환 (op 없음)을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-175">If there are no credentials, do nothing and return (no-op).</span></span>
3. <span data-ttu-id="bd493-176">자격 증명이 있지만 필터에서 인증 체계를 인식 하지 못하는 경우 아무 작업도 수행 하지 않고 반환 (op 없음)을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-176">If there are credentials but the filter does not recognize the authentication scheme, do nothing and return (no-op).</span></span> <span data-ttu-id="bd493-177">파이프라인의 다른 필터에서 스키마를 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-177">Another filter in the pipeline might understand the scheme.</span></span>
4. <span data-ttu-id="bd493-178">필터가 이해 하는 자격 증명이 있으면 인증을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-178">If there are credentials that the filter understands, try to authenticate them.</span></span>
5. <span data-ttu-id="bd493-179">자격 증명이 잘못 된 경우 `context.ErrorResult`설정 하 여 401을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-179">If the credentials are bad, return 401 by setting `context.ErrorResult`.</span></span>
6. <span data-ttu-id="bd493-180">자격 증명이 유효 하면 **IPrincipal** 을 만들고 `context.Principal`를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-180">If the credentials are valid, create an **IPrincipal** and set `context.Principal`.</span></span>

<span data-ttu-id="bd493-181">다음 코드는 [기본 인증](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BasicAuthentication) 샘플의 **AuthenticateAsync** 메서드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-181">The follow code shows the **AuthenticateAsync** method from the [Basic Authentication](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BasicAuthentication) sample.</span></span> <span data-ttu-id="bd493-182">주석은 각 단계를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-182">The comments indicate each step.</span></span> <span data-ttu-id="bd493-183">이 코드는 자격 증명이 없는 인증 헤더, 잘못 된 자격 증명, 잘못 된 사용자 이름/암호 등의 여러 가지 오류 유형을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-183">The code shows several types of error: An Authorization header with no credentials, malformed credentials, and bad username/password.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample5.cs)]

## <a name="setting-an-error-result"></a><span data-ttu-id="bd493-184">오류 결과 설정</span><span class="sxs-lookup"><span data-stu-id="bd493-184">Setting an Error Result</span></span>

<span data-ttu-id="bd493-185">자격 증명이 유효 하지 않은 경우 필터는 오류 응답을 생성 하는 **IHttpActionResult** 로 `context.ErrorResult` 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-185">If the credentials are invalid, the filter must set `context.ErrorResult` to an **IHttpActionResult** that creates an error response.</span></span> <span data-ttu-id="bd493-186">**IHttpActionResult**에 대 한 자세한 내용은 [Web API 2의 작업 결과](../getting-started-with-aspnet-web-api/action-results.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="bd493-186">For more information about **IHttpActionResult**, see [Action Results in Web API 2](../getting-started-with-aspnet-web-api/action-results.md).</span></span>

<span data-ttu-id="bd493-187">기본 인증 샘플에는이 용도에 적합 한 `AuthenticationFailureResult` 클래스가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-187">The Basic Authentication sample includes an `AuthenticationFailureResult` class that is suitable for this purpose.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample6.cs)]

## <a name="implementing-challengeasync"></a><span data-ttu-id="bd493-188">ChallengeAsync 구현</span><span class="sxs-lookup"><span data-stu-id="bd493-188">Implementing ChallengeAsync</span></span>

<span data-ttu-id="bd493-189">**ChallengeAsync** 메서드의 목적은 필요한 경우 응답에 인증 과제를 추가 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-189">The purpose of the **ChallengeAsync** method is to add authentication challenges to the response, if needed.</span></span> <span data-ttu-id="bd493-190">메서드 서명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-190">Here is the method signature:</span></span>

[!code-csharp[Main](authentication-filters/samples/sample7.cs)]

<span data-ttu-id="bd493-191">메서드는 요청 파이프라인의 모든 인증 필터에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-191">The method is called on every authentication filter in the request pipeline.</span></span>

<span data-ttu-id="bd493-192">**ChallengeAsync** 는 HTTP 응답을 만들기 *전에* 호출 되 고, 컨트롤러 작업이 실행 되기 전에도 호출 된다는 것을 이해 하는 것이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-192">It's important to understand that **ChallengeAsync** is called *before* the HTTP response is created, and possibly even before the controller action runs.</span></span> <span data-ttu-id="bd493-193">**ChallengeAsync** 가 호출 되 면 나중에 HTTP 응답을 만드는 데 사용 되는 **IHttpActionResult**가 `context.Result`에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-193">When **ChallengeAsync** is called, `context.Result` contains an **IHttpActionResult**, which is used later to create the HTTP response.</span></span> <span data-ttu-id="bd493-194">따라서 **ChallengeAsync** 를 호출 하면 HTTP 응답에 대 한 어떠한 정보도 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-194">So when **ChallengeAsync** is called, you don't know anything about the HTTP response yet.</span></span> <span data-ttu-id="bd493-195">**ChallengeAsync** 메서드는 `context.Result`의 원래 값을 새 **IHttpActionResult**바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-195">The **ChallengeAsync** method should replace the original value of `context.Result` with a new **IHttpActionResult**.</span></span> <span data-ttu-id="bd493-196">이 **IHttpActionResult** 는 원래 `context.Result`을 래핑해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-196">This **IHttpActionResult** must wrap the original `context.Result`.</span></span>

![](authentication-filters/_static/image3.png)

<span data-ttu-id="bd493-197">원래 **IHttpActionResult** *내부 결과*를 호출 하 고 새 **IHttpActionResult** *외부 결과*를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-197">I'll call the original **IHttpActionResult** the *inner result*, and the new **IHttpActionResult** the *outer result*.</span></span> <span data-ttu-id="bd493-198">외부 결과는 다음을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-198">The outer result must do the following:</span></span>

1. <span data-ttu-id="bd493-199">내부 결과를 호출 하 여 HTTP 응답을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-199">Invoke the inner result to create the HTTP response.</span></span>
2. <span data-ttu-id="bd493-200">응답을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-200">Examine the response.</span></span>
3. <span data-ttu-id="bd493-201">필요한 경우 응답에 인증 챌린지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-201">Add an authentication challenge to the response, if needed.</span></span>

<span data-ttu-id="bd493-202">다음 예제는 기본 인증 샘플에서 가져온 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-202">The following example is taken from the Basic Authentication sample.</span></span> <span data-ttu-id="bd493-203">외부 결과에 대 한 **IHttpActionResult** 를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-203">It defines an **IHttpActionResult** for the outer result.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample8.cs)]

<span data-ttu-id="bd493-204">`InnerResult` 속성은 내부 **IHttpActionResult**를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-204">The `InnerResult` property holds the inner **IHttpActionResult**.</span></span> <span data-ttu-id="bd493-205">`Challenge` 속성은 Www 인증 헤더를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-205">The `Challenge` property represents a Www-Authentication header.</span></span> <span data-ttu-id="bd493-206">**ExecuteAsync** 는 먼저 `InnerResult.ExecuteAsync`를 호출 하 여 HTTP 응답을 만든 다음 필요한 경우 챌린지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-206">Notice that **ExecuteAsync** first calls `InnerResult.ExecuteAsync` to create the HTTP response, and then adds the challenge if needed.</span></span>

<span data-ttu-id="bd493-207">챌린지를 추가 하기 전에 응답 코드를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-207">Check the response code before adding the challenge.</span></span> <span data-ttu-id="bd493-208">대부분의 인증 체계는 다음과 같이 응답이 401 인 경우에만 챌린지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-208">Most authentication schemes only add a challenge if the response is 401, as shown here.</span></span> <span data-ttu-id="bd493-209">그러나 일부 인증 스키마는 성공 응답에 챌린지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-209">However, some authentication schemes do add a challenge to a success response.</span></span> <span data-ttu-id="bd493-210">예를 들어 [Negotiate](http://tools.ietf.org/html/rfc4559#section-5) (RFC 4559)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="bd493-210">For example, see [Negotiate](http://tools.ietf.org/html/rfc4559#section-5) (RFC 4559).</span></span>

<span data-ttu-id="bd493-211">`AddChallengeOnUnauthorizedResult` 클래스가 지정 된 경우 **ChallengeAsync** 의 실제 코드는 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-211">Given the `AddChallengeOnUnauthorizedResult` class, the actual code in **ChallengeAsync** is simple.</span></span> <span data-ttu-id="bd493-212">결과를 만들어 `context.Result`에 연결 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-212">You just create the result and attach it to `context.Result`.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample9.cs)]

<span data-ttu-id="bd493-213">참고: 기본 인증 샘플은 확장 메서드에 배치 하 여이 논리를 비트로 추상화 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-213">Note: The Basic Authentication sample abstracts this logic a bit, by placing it in an extension method.</span></span>

## <a name="combining-authentication-filters-with-host-level-authentication"></a><span data-ttu-id="bd493-214">호스트 수준 인증과 인증 필터 조합</span><span class="sxs-lookup"><span data-stu-id="bd493-214">Combining Authentication Filters with Host-Level Authentication</span></span>

<span data-ttu-id="bd493-215">"호스트 수준 인증"은 요청이 웹 API 프레임 워크에 도달 하기 전에 호스트 (예: IIS)에서 수행 하는 인증입니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-215">"Host-level authentication" is authentication performed by the host (such as IIS), before the request reaches the Web API framework.</span></span>

<span data-ttu-id="bd493-216">응용 프로그램의 나머지 부분에 대해 호스트 수준 인증을 사용 하도록 설정 하 고 Web API 컨트롤러에 대해 사용 하지 않도록 설정 하는 경우가 종종 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-216">Often, you may want to enable host-level authentication for the rest of your application, but disable it for your Web API controllers.</span></span> <span data-ttu-id="bd493-217">예를 들어 일반적인 시나리오는 호스트 수준에서 폼 인증을 사용 하도록 설정 하 고 Web API에는 토큰 기반 인증을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-217">For example, a typical scenario is to enable Forms Authentication at the host level, but use token-based authentication for Web API.</span></span>

<span data-ttu-id="bd493-218">웹 API 파이프라인 내에서 호스트 수준 인증을 사용 하지 않도록 설정 하려면 구성에서 `config.SuppressHostPrincipal()`를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-218">To disable host-level authentication inside the Web API pipeline, call `config.SuppressHostPrincipal()` in your configuration.</span></span> <span data-ttu-id="bd493-219">이렇게 하면 web API는 Web api 파이프라인으로 들어가는 모든 요청에서 **IPrincipal** 을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd493-219">This causes Web API to remove the **IPrincipal** from any request that enters the Web API pipeline.</span></span> <span data-ttu-id="bd493-220">효과적으로 요청&quot; 인증을 취소할 &quot;.</span><span class="sxs-lookup"><span data-stu-id="bd493-220">Effectively, it &quot;un-authenticates&quot; the request.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample10.cs)]

## <a name="additional-resources"></a><span data-ttu-id="bd493-221">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="bd493-221">Additional Resources</span></span>

<span data-ttu-id="bd493-222">[보안 필터 ASP.NET Web API](https://msdn.microsoft.com/magazine/dn781361.aspx) (MSDN Magazine)</span><span class="sxs-lookup"><span data-stu-id="bd493-222">[ASP.NET Web API Security Filters](https://msdn.microsoft.com/magazine/dn781361.aspx) (MSDN Magazine)</span></span>
