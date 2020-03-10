---
uid: aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
title: ASP.NET에서 수행할 수 없는 작업 및 수행 하는 작업 Microsoft Docs
author: Rick-Anderson
description: 이 항목에서는 ASP.NET 웹 프로젝트 내에서 사용자가 수행 하는 몇 가지 일반적인 실수에 대해 설명 합니다. 이러한 동작을 방지 하기 위해 수행 해야 할 작업에 대 한 권장 사항을 제공 합니다.
ms.author: riande
ms.date: 01/28/2019
ms.assetid: c39b9965-545c-4b04-8f55-21be7f28a9e5
msc.legacyurl: /aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
msc.type: authoredcontent
ms.openlocfilehash: 980d3544df70643043391e6573803ce21b3a824f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500135"
---
# <a name="what-not-to-do-in-aspnet-and-what-to-do-instead"></a><span data-ttu-id="a4e68-104">ASP.NET에서 하지 말아야 하는 일과 해야 하는 일</span><span class="sxs-lookup"><span data-stu-id="a4e68-104">What not to do in ASP.NET, and what to do instead</span></span>

> <span data-ttu-id="a4e68-105">이 항목에서는 ASP.NET 웹 프로젝트 내에서 사용자가 수행 하는 몇 가지 일반적인 실수에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-105">This topic describes several common mistakes people make within ASP.NET web projects.</span></span> <span data-ttu-id="a4e68-106">이러한 일반적인 실수를 방지 하기 위해 수행 해야 하는 작업에 대 한 권장 사항을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-106">It provides recommendations for what you should do to avoid these common mistakes.</span></span> <span data-ttu-id="a4e68-107">**Damian Edwards** 의 개발자 회의에서 [프레젠테이션을](http://vimeo.com/68390507) 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-107">It is based on a [presentation](http://vimeo.com/68390507) by **Damian Edwards** at Norwegian Developers Conference.</span></span>

## <a name="disclaimer"></a><span data-ttu-id="a4e68-108">고지 사항</span><span class="sxs-lookup"><span data-stu-id="a4e68-108">Disclaimer</span></span>

<span data-ttu-id="a4e68-109">이 항목은 응용 프로그램의 보안 및 효율성을 보장 하기 위한 전체 가이드로 제공 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-109">This topic is not intended as a complete guide to ensure your application is secure and efficient.</span></span> <span data-ttu-id="a4e68-110">이 항목에 설명 되어 있지 않은 보안 및 성능에 대 한 모범 사례를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-110">You still need to follow best practices for security and performance that are not outlined in this topic.</span></span> <span data-ttu-id="a4e68-111">.NET 클래스 및 프로세스와 관련 된 일반적인 실수를 방지 하는 방법만 제안 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-111">It only suggests how to avoid common mistakes related to .NET classes and processes.</span></span>

## <a name="overview"></a><span data-ttu-id="a4e68-112">개요</span><span class="sxs-lookup"><span data-stu-id="a4e68-112">Overview</span></span>

<span data-ttu-id="a4e68-113">이 항목에는 다음과 같은 섹션이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-113">This topic contains the following sections:</span></span>

- [<span data-ttu-id="a4e68-114">표준 준수</span><span class="sxs-lookup"><span data-stu-id="a4e68-114">Standards Compliance</span></span>](#standards)

    - [<span data-ttu-id="a4e68-115">제어 어댑터</span><span class="sxs-lookup"><span data-stu-id="a4e68-115">Control Adapters</span></span>](#adapters)
    - [<span data-ttu-id="a4e68-116">컨트롤의 스타일 속성</span><span class="sxs-lookup"><span data-stu-id="a4e68-116">Style Properties on Controls</span></span>](#styleprop)
    - [<span data-ttu-id="a4e68-117">페이지 및 컨트롤 콜백</span><span class="sxs-lookup"><span data-stu-id="a4e68-117">Page and Control Callbacks</span></span>](#callback)
    - [<span data-ttu-id="a4e68-118">브라우저 기능 검색</span><span class="sxs-lookup"><span data-stu-id="a4e68-118">Browser Capability Detection</span></span>](#browsercap)
- [<span data-ttu-id="a4e68-119">보안</span><span class="sxs-lookup"><span data-stu-id="a4e68-119">Security</span></span>](#security)

    - [<span data-ttu-id="a4e68-120">요청 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="a4e68-120">Request Validation</span></span>](#validation)
    - [<span data-ttu-id="a4e68-121">쿠키 없는 폼 인증 및 세션</span><span class="sxs-lookup"><span data-stu-id="a4e68-121">Cookieless Forms Authentication and Session</span></span>](#cookieless)
    - [<span data-ttu-id="a4e68-122">EnableViewStateMac</span><span class="sxs-lookup"><span data-stu-id="a4e68-122">EnableViewStateMac</span></span>](#viewstatemac)
    - [<span data-ttu-id="a4e68-123">보통 신뢰</span><span class="sxs-lookup"><span data-stu-id="a4e68-123">Medium Trust</span></span>](#medium)
    - [<span data-ttu-id="a4e68-124">&lt;appSettings&gt;</span><span class="sxs-lookup"><span data-stu-id="a4e68-124">&lt;appSettings&gt;</span></span>](#appsettings)
    - [<span data-ttu-id="a4e68-125">UrlPathEncode</span><span class="sxs-lookup"><span data-stu-id="a4e68-125">UrlPathEncode</span></span>](#urlpathencode)
- [<span data-ttu-id="a4e68-126">안정성 및 성능</span><span class="sxs-lookup"><span data-stu-id="a4e68-126">Reliability and Performance</span></span>](#performance)

    - [<span data-ttu-id="a4e68-127">PreSendRequestHeaders 및 보도 Endrequestcontent</span><span class="sxs-lookup"><span data-stu-id="a4e68-127">PreSendRequestHeaders and PreSendRequestContent</span></span>](#presend)
    - [<span data-ttu-id="a4e68-128">Web Forms를 사용 하는 비동기 페이지 이벤트</span><span class="sxs-lookup"><span data-stu-id="a4e68-128">Asynchronous Page Events with Web Forms</span></span>](#asyncevents)
    - [<span data-ttu-id="a4e68-129">시작 및 잊어버린 작업</span><span class="sxs-lookup"><span data-stu-id="a4e68-129">Fire-and-Forget Work</span></span>](#fire)
    - [<span data-ttu-id="a4e68-130">요청 엔터티 본문</span><span class="sxs-lookup"><span data-stu-id="a4e68-130">Request Entity Body</span></span>](#requestentity)
    - [<span data-ttu-id="a4e68-131">응답. 리디렉션 및 응답. 끝</span><span class="sxs-lookup"><span data-stu-id="a4e68-131">Response.Redirect and Response.End</span></span>](#redirect)
    - [<span data-ttu-id="a4e68-132">EnableViewState 및 ViewStateMode</span><span class="sxs-lookup"><span data-stu-id="a4e68-132">EnableViewState and ViewStateMode</span></span>](#viewstatemode)
    - [<span data-ttu-id="a4e68-133">SqlMembershipProvider</span><span class="sxs-lookup"><span data-stu-id="a4e68-133">SqlMembershipProvider</span></span>](#sqlprovider)
    - [<span data-ttu-id="a4e68-134">장기 실행 요청 (> 110 초)</span><span class="sxs-lookup"><span data-stu-id="a4e68-134">Long Running Requests (>110 seconds)</span></span>](#long)

<a id="standards"></a>

## <a name="standards-compliance"></a><span data-ttu-id="a4e68-135">표준 준수</span><span class="sxs-lookup"><span data-stu-id="a4e68-135">Standards Compliance</span></span>

<a id="adapters"></a>

### <a name="control-adapters"></a><span data-ttu-id="a4e68-136">제어 어댑터</span><span class="sxs-lookup"><span data-stu-id="a4e68-136">Control adapters</span></span>

<span data-ttu-id="a4e68-137">권장 사항: 적응 렌더링에 컨트롤 어댑터 사용을 중지 하 고 대신 CSS 미디어 쿼리 및 표준 규격 HTML을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-137">Recommendation: Stop using control adapters for adaptive rendering, and instead use CSS media queries and standards-compliant HTML.</span></span>

<span data-ttu-id="a4e68-138">컨트롤 어댑터는 다른 장치 및 환경에 맞게 사용자 지정 된 프레젠테이션 코드를 렌더링 하기 위해 .NET 2.0에서 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-138">Controls Adapters were introduced in .NET 2.0 to render presentation code that was customized for different devices and environments.</span></span> <span data-ttu-id="a4e68-139">이제 CSS 및 HTML을 사용 하 여이 적응형 렌더링을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-139">Now, this adaptive rendering can be accomplished with CSS and HTML.</span></span> <span data-ttu-id="a4e68-140">컨트롤 어댑터 사용을 중지 하 고 기존 어댑터를 CSS 및 HTML로 변환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-140">You should stop using Control Adapters and convert any existing adapters to CSS and HTML.</span></span>

<span data-ttu-id="a4e68-141">자세한 내용은 [미디어 쿼리](http://www.w3.org/TR/css3-mediaqueries/) 및 [방법: ASP.NET Web Forms/MVC 응용 프로그램에 모바일 페이지 추가](../../../whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a4e68-141">For more information, see [Media Queries](http://www.w3.org/TR/css3-mediaqueries/) and [How To: Add Mobile Pages to Your ASP.NET Web Forms / MVC Application](../../../whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application.md).</span></span>

<a id="styleprop"></a>

### <a name="style-properties-on-controls"></a><span data-ttu-id="a4e68-142">컨트롤의 스타일 속성</span><span class="sxs-lookup"><span data-stu-id="a4e68-142">Style properties on controls</span></span>

<span data-ttu-id="a4e68-143">권장 사항: 컨트롤 태그에서 스타일 값 설정을 중지 하 고 대신 CSS 스타일 시트에서 형식 지정 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-143">Recommendation: Stop setting style values in the control markup, and instead set formatting values in CSS stylesheets.</span></span>

<span data-ttu-id="a4e68-144">웹 서버 컨트롤에는 인라인 스타일 속성을 설정 하는 데 사용할 수 있는 수십 개의 속성이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-144">Web server controls contain dozens of properties which can be used to set in-line style properties.</span></span> <span data-ttu-id="a4e68-145">예를 들어 ForeColor 속성은 컨트롤에 대 한 텍스트의 색을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-145">For example, the ForeColor property sets the color of the text for a control.</span></span> <span data-ttu-id="a4e68-146">CSS 스타일 시트를 통해 이와 동일한 효과를 보다 효율적으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-146">You can accomplish this same effect more efficiently through CSS stylesheets.</span></span> <span data-ttu-id="a4e68-147">스타일 시트를 사용 하면 스타일 값을 중앙 집중화 하 고 응용 프로그램 전체에서 이러한 값을 설정 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-147">Stylesheets enable you to centralize style values and avoid setting these values throughout your application.</span></span>

<span data-ttu-id="a4e68-148">다음 예제에서는 텍스트를 빨강으로 설정 하는 CSS 클래스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-148">The following example shows a CSS class the sets text to red.</span></span>

[!code-css[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample1.css)]

<span data-ttu-id="a4e68-149">다음 예제에서는 CSS 클래스를 동적으로 적용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-149">The next example shows how to dynamically apply the CSS class.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample2.cs)]

<a id="callback"></a>

### <a name="page-and-control-callbacks"></a><span data-ttu-id="a4e68-150">페이지 및 컨트롤 콜백</span><span class="sxs-lookup"><span data-stu-id="a4e68-150">Page and control callbacks</span></span>

<span data-ttu-id="a4e68-151">권장 사항: 페이지 및 컨트롤 콜백 사용을 중지 하 고 대신 AJAX, UpdatePanel, MVC 동작 메서드, Web API 또는 SignalR 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-151">Recommendation: Stop using page and control callbacks, and instead use any of the following: AJAX, UpdatePanel, MVC action methods, Web API, or SignalR.</span></span>

<span data-ttu-id="a4e68-152">이전 버전의 ASP.NET에서는 페이지 및 컨트롤 콜백 메서드를 사용 하 여 전체 페이지를 새로 고치지 않고 웹 페이지의 일부를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-152">In earlier versions of ASP.NET, Page and Control callback methods enabled you to update part of the web page without refreshing an entire page.</span></span> <span data-ttu-id="a4e68-153">이제 [AJAX](../../../ajax/index.md), [UpdatePanel](https://msdn.microsoft.com/library/bb386454.aspx), [MVC](../../../mvc/index.md), [Web API](../../../web-api/index.md) 또는 [SignalR](../../../signalr/index.md)를 통해 부분 페이지 업데이트를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-153">You can now accomplish partial-page updates through [AJAX](../../../ajax/index.md), [UpdatePanel](https://msdn.microsoft.com/library/bb386454.aspx), [MVC](../../../mvc/index.md), [Web API](../../../web-api/index.md) or [SignalR](../../../signalr/index.md).</span></span> <span data-ttu-id="a4e68-154">친숙 한 Url 및 라우팅 문제를 일으킬 수 있으므로 콜백 메서드 사용을 중지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-154">You should stop using callback methods because they can cause issues with friendly URLs and routing.</span></span> <span data-ttu-id="a4e68-155">기본적으로 컨트롤은 콜백 메서드를 사용 하지 않지만 컨트롤에서이 기능을 사용 하도록 설정한 경우에는 사용 하지 않도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-155">By default, controls do not enable callback methods, but if you enabled this feature in a control, you should disable it.</span></span>

<a id="browsercap"></a>

### <a name="browser-capability-detection"></a><span data-ttu-id="a4e68-156">브라우저 기능 검색</span><span class="sxs-lookup"><span data-stu-id="a4e68-156">Browser capability detection</span></span>

<span data-ttu-id="a4e68-157">권장 사항: 정적 브라우저 기능 검색 사용을 중지 하 고 대신 동적 기능 검색을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-157">Recommendation: Stop using static browser capability detection, and instead use dynamic feature detection.</span></span>

<span data-ttu-id="a4e68-158">이전 버전의 ASP.NET에서는 각 브라우저에 대해 지원 되는 기능이 XML 파일에 저장 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-158">In earlier versions of ASP.NET, the supported features for each browser were stored in an XML file.</span></span> <span data-ttu-id="a4e68-159">정적 조회를 통해 기능 지원을 검색 하는 것은 최상의 방법이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-159">Detecting feature support through a static lookup is not the best approach.</span></span> <span data-ttu-id="a4e68-160">이제 [Modernizr](http://modernizr.com/)와 같은 기능 검색 프레임 워크를 사용 하 여 브라우저의 지원 되는 기능을 동적으로 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-160">Now, you can dynamically detect a browser's supported features by using a feature detection framework, such as [Modernizr](http://modernizr.com/).</span></span> <span data-ttu-id="a4e68-161">기능 검색은 메서드 또는 속성을 사용한 다음 브라우저에서 원하는 결과를 생성 한 것인지 확인 하 여 지원을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-161">Feature detection determines support by attempting to use a method or property and then checking to see if the browser produced the desired result.</span></span> <span data-ttu-id="a4e68-162">기본적으로 Modernizr는 웹 응용 프로그램 템플릿에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-162">By default, Modernizr is included in the Web application templates.</span></span>

<a id="security"></a>

## <a name="security"></a><span data-ttu-id="a4e68-163">보안</span><span class="sxs-lookup"><span data-stu-id="a4e68-163">Security</span></span>

<a id="validation"></a>

### <a name="request-validation"></a><span data-ttu-id="a4e68-164">요청 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="a4e68-164">Request validation</span></span>

<span data-ttu-id="a4e68-165">권장 사항: 사용자 입력의 유효성을 검사 하 고 사용자의 출력을 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-165">Recommendation: Validate user input, and encode output from users.</span></span>

<span data-ttu-id="a4e68-166">요청 유효성 검사는 각 요청을 검사 하 고 인식 된 위협이 발견 되는 경우 요청을 중지 하는 ASP.NET의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-166">Request validation is a feature of ASP.NET that inspects each request and stops the request if a perceived threat is found.</span></span> <span data-ttu-id="a4e68-167">사이트 간 스크립팅 공격 으로부터 응용 프로그램을 보호 하기 위한 요청 유효성 검사에 의존 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-167">Do not depend on request validation for securing your application against cross-site scripting attacks.</span></span> <span data-ttu-id="a4e68-168">대신 사용자의 모든 입력에 대 한 유효성을 검사 하 고 출력을 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-168">Instead, validate all input from users and encode the output.</span></span> <span data-ttu-id="a4e68-169">일부 제한 된 경우에는 정규식을 사용 하 여 입력의 유효성을 검사할 수 있지만 더 복잡 한 경우에는 값이 허용 되는 값과 일치 하는지 확인 하는 .NET 클래스를 사용 하 여 사용자 입력의 유효성을 검사 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-169">In some limited cases, you can use regular expressions to validate the input, but in more complicated cases you should validate user input by using .NET classes that determine if the value matches allowed values.</span></span>

<span data-ttu-id="a4e68-170">다음 예제에서는 Uri 클래스에서 정적 메서드를 사용 하 여 사용자가 제공한 Uri가 유효한 지 여부를 확인 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-170">The following example shows how to use a static method in the Uri class to determine whether the Uri provided by a user is valid.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample3.cs)]

<span data-ttu-id="a4e68-171">그러나 Uri를 충분히 확인 하려면 `http` 또는 `https`를 지정 하는지 여부도 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-171">However, to sufficiently verify the Uri, you should also check to make sure it specifies `http` or `https`.</span></span> <span data-ttu-id="a4e68-172">다음 예에서는 인스턴스 메서드를 사용 하 여 Uri가 유효한 지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-172">The following example uses instance methods to verify that the Uri is valid.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample4.cs)]

<span data-ttu-id="a4e68-173">사용자 입력을 HTML로 렌더링 하거나 SQL 쿼리에서 사용자 입력을 포함 하기 전에 값을 인코딩하여 악성 코드가 포함 되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-173">Before rendering user input as HTML or including user input in a SQL query, encode the values to ensure malicious code is not included.</span></span>

<span data-ttu-id="a4e68-174">아래와 같이 &lt;%:%&gt; 구문을 사용 하 여 태그의 값을 HTML로 인코딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-174">You can HTML encode the value in markup with the &lt;%: %&gt; syntax, as shown below.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample5.aspx?highlight=1)]

<span data-ttu-id="a4e68-175">또는 Razor 구문 아래와 같이 @로 HTML을 인코딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-175">Or, in Razor syntax, you can HTML encode with @, as shown below.</span></span>

[!code-cshtml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample6.cshtml?highlight=1)]

<span data-ttu-id="a4e68-176">다음 예제에서는 코드 숨김으로 값을 HTML로 인코딩하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-176">The next example shows how to HTML encode a value in code-behind.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample7.cs)]

<span data-ttu-id="a4e68-177">SQL 명령에 대 한 값을 안전 하 게 인코딩하려면 [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx)와 같은 명령 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-177">To safely encode a value for SQL commands, use command parameters such as the [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx).</span></span> <a id="cookieless"></a>

### <a name="cookieless-forms-authentication-and-session"></a><span data-ttu-id="a4e68-178">쿠키 없는 폼 인증 및 세션</span><span class="sxs-lookup"><span data-stu-id="a4e68-178">Cookieless forms authentication and session</span></span>

<span data-ttu-id="a4e68-179">권장 사항: 쿠키가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-179">Recommendation: Require cookies.</span></span>

<span data-ttu-id="a4e68-180">쿼리 문자열에 인증 정보를 전달 하는 것은 안전 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-180">Passing authentication information in the query string is not secure.</span></span> <span data-ttu-id="a4e68-181">따라서 응용 프로그램에 인증이 포함 되어 있으면 쿠키가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-181">Therefore, require cookies when your application includes authentication.</span></span> <span data-ttu-id="a4e68-182">쿠키가 중요 한 정보를 저장 하는 경우 쿠키에 대해 SSL을 요구 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-182">If your cookie stores sensitive information, consider requiring SSL for the cookie.</span></span>

<span data-ttu-id="a4e68-183">다음 예제에서는 폼 인증에 SSL을 통해 전송 되는 쿠키가 필요한 경우 Web.config 파일에를 지정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-183">The following example shows how to specify in the Web.config file that Forms Authentication requires a cookie that is transmitted over SSL.</span></span>

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample8.xml)]

<a id="viewstatemac"></a>

### <a name="enableviewstatemac"></a><span data-ttu-id="a4e68-184">EnableViewStateMac</span><span class="sxs-lookup"><span data-stu-id="a4e68-184">EnableViewStateMac</span></span>

<span data-ttu-id="a4e68-185">권장 사항: false로 설정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-185">Recommendation: Never set to false.</span></span>

<span data-ttu-id="a4e68-186">기본적으로 EnableViewStateMac는 true로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-186">By default, EnableViewStateMac is set to true.</span></span> <span data-ttu-id="a4e68-187">응용 프로그램에서 뷰 상태를 사용 하지 않는 경우에도 EnableViewStateMac을 false로 설정 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="a4e68-187">Even if your application is not using view state, do not set EnableViewStateMac to false.</span></span> <span data-ttu-id="a4e68-188">이 값을 false로 설정 하면 응용 프로그램이 교차 사이트 스크립팅에 취약 해질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-188">Setting this value to false will make your application vulnerable to cross-site scripting.</span></span>

<span data-ttu-id="a4e68-189">ASP.NET 4.5.2부터 런타임은 **EnableViewStateMac = true**를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-189">Starting with ASP.NET 4.5.2, the runtime enforces **EnableViewStateMac=true**.</span></span> <span data-ttu-id="a4e68-190">False로 설정한 경우에도 런타임은이 값을 무시 하 고 값을 true로 설정 하 여 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-190">Even if you set it to false, the runtime ignores this value and proceeds with the value set to true.</span></span> <span data-ttu-id="a4e68-191">자세한 내용은 [ASP.NET 4.5.2 및 EnableViewStateMac](https://blogs.msdn.com/b/webdev/archive/2014/05/07/asp-net-4-5-2-and-enableviewstatemac.aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a4e68-191">For more information, see [ASP.NET 4.5.2 and EnableViewStateMac](https://blogs.msdn.com/b/webdev/archive/2014/05/07/asp-net-4-5-2-and-enableviewstatemac.aspx).</span></span>

<span data-ttu-id="a4e68-192">다음 예제에서는 EnableViewStateMac를 true로 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-192">The following example shows how to set EnableViewStateMac to true.</span></span> <span data-ttu-id="a4e68-193">이 값은 기본적으로 true 이므로 실제로이 값을 true로 설정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-193">You do not need to actually set this value to true because it is true by default.</span></span> <span data-ttu-id="a4e68-194">그러나 응용 프로그램의 모든 페이지에서이 값을 false로 설정한 경우에는이 값을 즉시 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-194">However, if you have set it to false on any page in your application, you must immediately correct this value.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample9.aspx)]

<a id="medium"></a>

### <a name="medium-trust"></a><span data-ttu-id="a4e68-195">보통 신뢰</span><span class="sxs-lookup"><span data-stu-id="a4e68-195">Medium trust</span></span>

<span data-ttu-id="a4e68-196">권장 사항: 보안 경계로 보통 신뢰 수준 또는 다른 신뢰 수준에 의존 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-196">Recommendation: Do not depend on Medium Trust (or any other trust level) as a security boundary.</span></span>

<span data-ttu-id="a4e68-197">부분 신뢰는 응용 프로그램을 적절 하 게 보호 하지 않으므로 사용 하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-197">Partial trust does not adequately protect your application and should not be used.</span></span> <span data-ttu-id="a4e68-198">대신 완전 신뢰를 사용 하 고 신뢰할 수 없는 응용 프로그램을 별도의 응용 프로그램 풀에서 격리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-198">Instead, use Full Trust, and isolate untrusted applications in separate application pools.</span></span> <span data-ttu-id="a4e68-199">또한 고유한 id로 각 응용 프로그램 풀을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-199">Also, run each application pool under a unique identity.</span></span> <span data-ttu-id="a4e68-200">자세한 내용은 [ASP.NET 부분 신뢰에서 응용 프로그램 격리를 보장 하지 않음](https://support.microsoft.com/kb/2698981)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a4e68-200">For more information, see [ASP.NET Partial Trust does not guarantee application isolation](https://support.microsoft.com/kb/2698981).</span></span>

<a id="appsettings"></a>

### <a name="ltappsettingsgt"></a><span data-ttu-id="a4e68-201">&lt;appSettings&gt;</span><span class="sxs-lookup"><span data-stu-id="a4e68-201">&lt;appSettings&gt;</span></span>

<span data-ttu-id="a4e68-202">권장 사항: &lt;appSettings&gt; 요소에서 보안 설정을 사용 하지 않도록 설정 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="a4e68-202">Recommendation: Do not disable security settings in &lt;appSettings&gt; element.</span></span>

<span data-ttu-id="a4e68-203">AppSettings 요소에는 보안 업데이트에 필요한 여러 값이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-203">The appSettings element contains many values which are required for security updates.</span></span> <span data-ttu-id="a4e68-204">이러한 값은 변경 하거나 사용 하지 않도록 설정 하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-204">You should not change or disable these values.</span></span> <span data-ttu-id="a4e68-205">업데이트를 배포할 때 이러한 값을 사용 하지 않도록 설정 해야 하는 경우 배포를 완료 한 후 즉시 다시 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-205">If you must disable these values when deploying an update, immediately re-enable after completing deployment.</span></span>

<span data-ttu-id="a4e68-206">자세한 내용은 [ASP.NET AppSettings 요소](https://msdn.microsoft.com/library/hh975440.aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a4e68-206">For details, see [ASP.NET appSettings Element](https://msdn.microsoft.com/library/hh975440.aspx).</span></span>

<a id="urlpathencode"></a>

### <a name="urlpathencode"></a><span data-ttu-id="a4e68-207">UrlPathEncode</span><span class="sxs-lookup"><span data-stu-id="a4e68-207">UrlPathEncode</span></span>

<span data-ttu-id="a4e68-208">권장 사항: 대신 [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx) 를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-208">Recommendation: Use [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx) instead.</span></span>

<span data-ttu-id="a4e68-209">UrlPathEncode 메서드가 매우 특정 브라우저 호환성 문제를 해결 하기 위해 .NET Framework에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-209">The UrlPathEncode method was added to the .NET Framework to resolve a very specific browser compatibility problem.</span></span> <span data-ttu-id="a4e68-210">URL을 적절 하 게 인코딩하지 않고 교차 사이트 스크립팅 으로부터 응용 프로그램을 보호 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-210">It does not adequately encode a URL, and does not protect your application from cross-site scripting.</span></span> <span data-ttu-id="a4e68-211">응용 프로그램에서 사용 하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-211">You should never use it in your application.</span></span> <span data-ttu-id="a4e68-212">대신 [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-212">Instead, use [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx).</span></span>

<span data-ttu-id="a4e68-213">다음 예제에서는 인코딩된 URL을 하이퍼링크 컨트롤에 대 한 쿼리 문자열 매개 변수로 전달 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-213">The following example shows how to pass an encoded URL as a query string parameter for a hyperlink control.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample10.cs)]

<a id="performance"></a>

## <a name="reliability-and-performance"></a><span data-ttu-id="a4e68-214">안정성 및 성능</span><span class="sxs-lookup"><span data-stu-id="a4e68-214">Reliability and performance</span></span>

<a id="presend"></a>

### <a name="presendrequestheaders-and-presendrequestcontent"></a><span data-ttu-id="a4e68-215">PreSendRequestHeaders 및 보도 Endrequestcontent</span><span class="sxs-lookup"><span data-stu-id="a4e68-215">PreSendRequestHeaders and PreSendRequestContent</span></span>

<span data-ttu-id="a4e68-216">권장 사항: 관리 되는 모듈에서는 이러한 이벤트를 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="a4e68-216">Recommendation: Do not use these events with managed modules.</span></span> <span data-ttu-id="a4e68-217">대신, 필요한 작업을 수행 하는 네이티브 IIS 모듈을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-217">Instead, write a native IIS module to perform the required task.</span></span> <span data-ttu-id="a4e68-218">[네이티브 코드 HTTP 모듈 만들기](https://msdn.microsoft.com/library/ms693629.aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a4e68-218">See [Creating Native-Code HTTP Modules](https://msdn.microsoft.com/library/ms693629.aspx).</span></span>

<span data-ttu-id="a4e68-219">네이티브 IIS 모듈과 함께 [PreSendRequestHeaders](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestheaders.aspx) 및 [보도 endrequestcontent](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestcontent.aspx) 이벤트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-219">You can use the [PreSendRequestHeaders](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestheaders.aspx) and [PreSendRequestContent](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestcontent.aspx) events with native IIS modules.</span></span>
> [!WARNING]
> <span data-ttu-id="a4e68-220">`IHttpModule`를 구현 하는 관리 되는 모듈에 `PreSendRequestHeaders` 및 `PreSendRequestContent`를 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="a4e68-220">Do not use `PreSendRequestHeaders` and `PreSendRequestContent` with managed modules that implement `IHttpModule`.</span></span> <span data-ttu-id="a4e68-221">이러한 속성을 설정 하면 비동기 요청을 사용 하 여 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-221">Setting these properties can cause issues with asynchronous requests.</span></span> <span data-ttu-id="a4e68-222">애플리케이션 요청 라우팅 (ARR) 및 websocket의 조합을 w3wp 충돌을 일으킬 수 있는 액세스 위반 예외가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-222">The combination of Application Requested Routing (ARR) and websockets might lead to access violation exceptions that can cause w3wp to crash.</span></span> <span data-ttu-id="a4e68-223">예를 들어 iiscore! W3_CONTEXT_BASE::GetIsLastNotification + 68 iiscore.dll에서 액세스 위반 예외 (0xC0000005) 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-223">For example, iiscore!W3_CONTEXT_BASE::GetIsLastNotification+68 in iiscore.dll has caused an access violation exception (0xC0000005).</span></span>

<a id="asyncevents"></a>

### <a name="asynchronous-page-events-with-web-forms"></a><span data-ttu-id="a4e68-224">Web forms를 사용 하는 비동기 페이지 이벤트</span><span class="sxs-lookup"><span data-stu-id="a4e68-224">Asynchronous page events with web forms</span></span>

<span data-ttu-id="a4e68-225">권장 사항: Web Forms에서는 페이지 수명 주기 이벤트에 대해 비동기 void 메서드를 작성 하지 말고 비동기 코드에 [RegisterAsyncTask](https://msdn.microsoft.com/library/system.web.ui.page.registerasynctask.aspx) 를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-225">Recommendation: In Web Forms, avoid writing async void methods for Page lifecycle events, and instead use [Page.RegisterAsyncTask](https://msdn.microsoft.com/library/system.web.ui.page.registerasynctask.aspx) for asynchronous code.</span></span>

<span data-ttu-id="a4e68-226">**비동기 및** **void**로 페이지 이벤트를 표시 하면 비동기 코드가 완료 된 시간을 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-226">When you mark a page event with **async** and **void**, you cannot determine when the asynchronous code has finished.</span></span> <span data-ttu-id="a4e68-227">대신 RegisterAsyncTask를 사용 하 여 비동기 코드를 실행 하 여 완료를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-227">Instead, use Page.RegisterAsyncTask to run the asynchronous code in a way that enables you to track its completion.</span></span>

<span data-ttu-id="a4e68-228">다음 예제에서는 비동기 코드를 포함 하는 단추 클릭 처리기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-228">The following example shows a button click handler that contains asynchronous code.</span></span> <span data-ttu-id="a4e68-229">이 예제에는 비동기 작업의 간단한 예제로만 제공 되 고 권장 되는 방법이 아닌 문자열 값을 비동기적으로 읽는 작업이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-229">This example includes reading a string value asynchronously, which is provided only as a simplified example of an asynchronous task and not as a recommended practice.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample11.cs)]

<span data-ttu-id="a4e68-230">비동기 작업을 사용 하는 경우 Web.config 파일에서 Http 런타임 대상 프레임 워크를 4.5 이상으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-230">If you are using asynchronous Tasks, set the Http runtime target framework to 4.5 (or later) in the Web.config file.</span></span> <span data-ttu-id="a4e68-231">대상 프레임 워크를 4.5로 설정 하면 .NET 4.5에 추가 된 새 동기화 컨텍스트가 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-231">Setting the target framework to 4.5 turns on the new synchronization context that was added in .NET 4.5.</span></span> <span data-ttu-id="a4e68-232">이 값은 Visual Studio의 새 프로젝트에서 기본적으로 설정 되지만 기존 프로젝트로 작업 하는 경우에는 설정 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-232">This value is set by default in new projects in Visual Studio, but is not be set if you are working with an existing project.</span></span>

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample12.xml)]

<a id="fire"></a>

### <a name="fire-and-forget-work"></a><span data-ttu-id="a4e68-233">시작 및 잊어버린 작업</span><span class="sxs-lookup"><span data-stu-id="a4e68-233">Fire-and-forget work</span></span>

<span data-ttu-id="a4e68-234">권장 사항: ASP.NET 내에서 요청을 처리 하는 경우 시작 및 제거 작업을 시작 하지 않습니다 (예: QueueUserWorkItem 메서드 호출 또는 대리자를 반복적으로 호출 하는 타이머 만들기).</span><span class="sxs-lookup"><span data-stu-id="a4e68-234">Recommendation: When handling a request within ASP.NET, avoid launching fire-and-forget work (such calling the ThreadPool.QueueUserWorkItem method or creating a timer that repeatedly calls a delegate).</span></span>

<span data-ttu-id="a4e68-235">응용 프로그램에서 ASP.NET 내에 실행 되는 화재 및 잊은 작업을 수행 하는 경우 응용 프로그램이 동기화 되지 않을 수 있습니다. 언제 든 지 앱 도메인을 제거할 수 있으며,이는 진행 중인 프로세스가 응용 프로그램의 현재 상태와 더 이상 일치 하지 않을 수 있음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-235">If your application has fire-and-forget work that runs within ASP.NET, your application can get out of sync. At any time, the app domain can be destroyed which means your ongoing process may no longer match the current state of the application.</span></span>

<span data-ttu-id="a4e68-236">이러한 유형의 작업은 ASP.NET 외부에서 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-236">You should move this type of work outside of ASP.NET.</span></span> <span data-ttu-id="a4e68-237">Azure에서 웹 작업, Windows 서비스 또는 작업자 역할을 사용 하 여 진행 중인 작업을 수행 하 고 다른 프로세스에서 해당 코드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-237">You can use a Web Jobs, Windows Service or a Worker role in Azure to perform ongoing work, and run that code from another process.</span></span>

<span data-ttu-id="a4e68-238">ASP.NET 내에서이 작업을 수행 해야 하는 경우 [WebBackgrounder](http://www.nuget.org/packages/webbackgrounder) 라는 Nuget 패키지를 추가 하 여 코드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-238">If you must perform this work within ASP.NET, you can add the Nuget package called [WebBackgrounder](http://www.nuget.org/packages/webbackgrounder) to run the code.</span></span>

<a id="requestentity"></a>

### <a name="request-entity-body"></a><span data-ttu-id="a4e68-239">요청 엔터티 본문</span><span class="sxs-lookup"><span data-stu-id="a4e68-239">Request entity body</span></span>

<span data-ttu-id="a4e68-240">권장 사항: 처리기의 실행 이벤트 전에 InputStream 또는 요청을 읽지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="a4e68-240">Recommendation: Avoid reading Request.Form or Request.InputStream before the handler's execute event.</span></span>

<span data-ttu-id="a4e68-241">InputStream에서 읽어야 하는 가장 빠른는 처리기의 실행 이벤트 중입니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-241">The earliest you should read from Request.Form or Request.InputStream is during the handler's execute event.</span></span> <span data-ttu-id="a4e68-242">MVC에서 컨트롤러는 처리기 이며 작업 메서드가 실행 될 때 실행 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-242">In MVC, the Controller is the handler and the execute event is when the action method runs.</span></span> <span data-ttu-id="a4e68-243">Web Forms에서 페이지는 처리기이 고 execute 이벤트는 페이지. Init 이벤트가 발생 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-243">In Web Forms, the Page is the handler and the execute event is when the Page.Init event fires.</span></span> <span data-ttu-id="a4e68-244">실행 이벤트 보다 이전 요청 엔터티 본문을 읽는 경우 요청 처리에 방해가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-244">If you read the request entity body earlier than the execute event, you interfere with the processing of the request.</span></span>

<span data-ttu-id="a4e68-245">실행 이벤트 전에 요청 엔터티 본문을 읽어야 하는 경우 [GetBufferlessInputStream](https://msdn.microsoft.com/library/ff406798.aspx) 또는 [GetBufferedInputStream](https://msdn.microsoft.com/library/system.web.httprequest.getbufferedinputstream.aspx)중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-245">If you need to read the request entity body before the execute event, use either [Request.GetBufferlessInputStream](https://msdn.microsoft.com/library/ff406798.aspx) or [Request.GetBufferedInputStream](https://msdn.microsoft.com/library/system.web.httprequest.getbufferedinputstream.aspx).</span></span> <span data-ttu-id="a4e68-246">GetBufferlessInputStream를 사용 하는 경우 요청에서 원시 스트림을 가져오고 전체 요청을 처리 하는 책임이 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-246">When you use GetBufferlessInputStream, you get the raw stream from the request, and assume responsibility for processing the entire request.</span></span> <span data-ttu-id="a4e68-247">GetBufferlessInputStream를 호출한 후 InputStream 및 ASP.NET를 사용 하 여 채워지지 않았기 때문에를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-247">After calling GetBufferlessInputStream, Request.Form and Request.InputStream are not available because they have not been populated by ASP.NET.</span></span> <span data-ttu-id="a4e68-248">GetBufferedInputStream를 사용 하는 경우 요청에서 스트림의 복사본을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-248">When you use GetBufferedInputStream, you get a copy of the stream from the request.</span></span> <span data-ttu-id="a4e68-249">ASP.NET는 다른 복사본을 채우기 때문에 InputStream 및 요청에서 나중에 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-249">Request.Form and Request.InputStream are still available later in the request because ASP.NET populates the other copy.</span></span>

<a id="redirect"></a>

### <a name="responseredirect-and-responseend"></a><span data-ttu-id="a4e68-250">응답. 리디렉션 및 응답. 끝</span><span class="sxs-lookup"><span data-stu-id="a4e68-250">Response.Redirect and Response.End</span></span>

<span data-ttu-id="a4e68-251">권장 사항: [Response (String)](https://msdn.microsoft.com/library/t9dwyts4.aspx)를 호출한 후 스레드를 처리 하는 방법의 차이를 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-251">Recommendation: Be aware of differences in how thread is handled after calling [Response.Redirect(String)](https://msdn.microsoft.com/library/t9dwyts4.aspx).</span></span>

<span data-ttu-id="a4e68-252">[Response. Redirect (String)](https://msdn.microsoft.com/library/t9dwyts4.aspx) 메서드는 response 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-252">The [Response.Redirect(String)](https://msdn.microsoft.com/library/t9dwyts4.aspx) method calls the Response.End method.</span></span> <span data-ttu-id="a4e68-253">동기 프로세스에서 Request. Redirect를 호출 하면 현재 스레드가 즉시 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-253">In a synchronous process, calling Request.Redirect causes the current thread to immediately abort.</span></span> <span data-ttu-id="a4e68-254">그러나 비동기 프로세스에서 Response를 호출 하면 현재 스레드가 중단 되지 않으므로 코드 실행이 요청에 대해 계속 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-254">However, in an asynchronous process, calling Response.Redirect does not abort the current thread, so code execution continues for the request.</span></span> <span data-ttu-id="a4e68-255">비동기 프로세스에서 코드 실행을 중지 하려면 메서드에서 작업을 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-255">In an asynchronous process, you must return the Task from the method to stop the code execution.</span></span>

<span data-ttu-id="a4e68-256">MVC 프로젝트에서는 Response를 호출 하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-256">In an MVC project, you should not call Response.Redirect.</span></span> <span data-ttu-id="a4e68-257">대신 RedirectResult를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-257">Instead, return a RedirectResult.</span></span>

<a id="viewstatemode"></a>

### <a name="enableviewstate-and-viewstatemode"></a><span data-ttu-id="a4e68-258">EnableViewState 및 ViewStateMode</span><span class="sxs-lookup"><span data-stu-id="a4e68-258">EnableViewState and ViewStateMode</span></span>

<span data-ttu-id="a4e68-259">권장 사항: view 상태를 사용 하는 컨트롤에 대해 세부적인 제어를 제공 하려면 EnableViewState 대신 ViewStateMode를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-259">Recommendation: Use ViewStateMode, instead of EnableViewState, to provide granular control over which controls use view state.</span></span>

<span data-ttu-id="a4e68-260">Page 지시문에서 EnableViewState를 false로 설정 하면 페이지 내의 모든 컨트롤에 대해 뷰 상태가 사용 하지 않도록 설정 되 고 사용 하도록 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-260">When you set EnableViewState to false in the Page directive, view state is disabled for all controls within the page and cannot be enabled.</span></span> <span data-ttu-id="a4e68-261">페이지의 특정 컨트롤에만 뷰 상태를 사용 하려면 페이지에 대해 ViewStateMode를 사용 안 함으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-261">If you want to enable view state for only certain controls in your page, set ViewStateMode to Disabled for the Page.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample13.aspx)]

<span data-ttu-id="a4e68-262">그런 다음 뷰 상태를 실제로 필요로 하는 컨트롤에 대해서만 ViewStateMode를 사용으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-262">Then, set ViewStateMode to Enabled on only the controls that actually need view state.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample14.aspx)]

<span data-ttu-id="a4e68-263">필요한 컨트롤에 대해서만 뷰 상태를 사용 하도록 설정 하면 웹 페이지의 뷰 상태 크기를 축소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-263">By enabling view state for only the controls that need it, you can shrink the size of the view state for your web pages.</span></span>

<a id="sqlprovider"></a>

### <a name="sqlmembershipprovider"></a><span data-ttu-id="a4e68-264">SqlMembershipProvider</span><span class="sxs-lookup"><span data-stu-id="a4e68-264">SqlMembershipProvider</span></span>

<span data-ttu-id="a4e68-265">권장 사항: Universal Providers을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-265">Recommendation: Use Universal Providers.</span></span>

<span data-ttu-id="a4e68-266">현재 프로젝트 템플릿에서 SqlMembershipProvider는 NuGet 패키지로 사용할 수 있는 [ASP.NET Universal Providers](http://www.nuget.org/packages/Microsoft.AspNet.Providers)으로 대체 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-266">In the current project templates, SqlMembershipProvider has been replaced by [ASP.NET Universal Providers](http://www.nuget.org/packages/Microsoft.AspNet.Providers), which is available as a NuGet package.</span></span> <span data-ttu-id="a4e68-267">이전 버전의 템플릿으로 빌드된 프로젝트에서 SqlMembershipProvider를 사용 하는 경우 Universal Providers로 전환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-267">If you are using SqlMembershipProvider in a project that was built with an earlier version of the templates, you should switch to Universal Providers.</span></span> <span data-ttu-id="a4e68-268">Universal Providers은 Entity Framework에서 지원 되는 모든 데이터베이스에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-268">The Universal Providers work with all databases that are supported by Entity Framework.</span></span>

<span data-ttu-id="a4e68-269">자세한 내용은 [ASP.NET Universal Providers 소개](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a4e68-269">For more information, see [Introducing ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx).</span></span>

<a id="long"></a>

### <a name="long-running-requests-110-seconds"></a><span data-ttu-id="a4e68-270">장기 실행 요청 (> 110 초)</span><span class="sxs-lookup"><span data-stu-id="a4e68-270">Long-running requests (>110 seconds)</span></span>

<span data-ttu-id="a4e68-271">권장 사항: 연결 된 클라이언트에 대해 [websocket](https://msdn.microsoft.com/library/system.net.websockets.websocket.aspx) 또는 [SignalR](../../../signalr/index.md) 를 사용 하 고 비동기 i/o 작업을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-271">Recommendation: Use [WebSockets](https://msdn.microsoft.com/library/system.net.websockets.websocket.aspx) or [SignalR](../../../signalr/index.md) for connected clients, and use asynchronous I/O operations.</span></span>

<span data-ttu-id="a4e68-272">장기 실행 요청을 실행 하면 웹 응용 프로그램에서 예기치 않은 결과가 발생 하 고 성능이 저하 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-272">Long-running requests can cause unpredictable results and poor performance in your web application.</span></span> <span data-ttu-id="a4e68-273">요청에 대 한 기본 시간 제한 설정은 110 초입니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-273">The default timeout setting for a request is 110 seconds.</span></span> <span data-ttu-id="a4e68-274">장기 실행 요청에서 세션 상태를 사용 하는 경우 ASP.NET는 110 초 후 세션 개체에 대 한 잠금을 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-274">If you are using session state with a long-running request, ASP.NET will release the lock on the Session object after 110 seconds.</span></span> <span data-ttu-id="a4e68-275">그러나 잠금이 해제 되 고 작업이 성공적으로 완료 되지 않을 수 있는 경우 응용 프로그램은 세션 개체에 대 한 작업 중간에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-275">However, your application might be in the middle of an operation on the Session object when the lock is released, and the operation might not complete successfully.</span></span> <span data-ttu-id="a4e68-276">첫 번째 요청이 실행 되는 동안 사용자의 두 번째 요청이 차단 된 경우 두 번째 요청은 일관 되지 않은 상태에서 세션 개체에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-276">If a second request from the user is blocked while the first request is running, the second request might access the Session object in an inconsistent state.</span></span>

<span data-ttu-id="a4e68-277">응용 프로그램에 차단 (또는 동기) i/o 작업이 포함 된 경우 응용 프로그램이 응답 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-277">If your application includes blocking (or synchronous) I/O operations, the application will be unresponsive.</span></span>

<span data-ttu-id="a4e68-278">성능을 향상 시키려면 .NET Framework에서 비동기 i/o 작업을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-278">To improve performance, use the asynchronous I/O operations in the .NET Framework.</span></span> <span data-ttu-id="a4e68-279">또한 클라이언트를 서버에 연결 하는 데 Websocket 또는 SignalR를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-279">Also, use WebSockets or SignalR for connecting clients to the server.</span></span> <span data-ttu-id="a4e68-280">이러한 기능은 장기 실행 요청을 효율적으로 처리할 수 있도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e68-280">These features are designed to efficiently handle long-running requests.</span></span>
