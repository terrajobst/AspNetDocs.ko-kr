---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
title: ASP.NET AJAX 인증 및 프로필 애플리케이션 서비스 이해 | Microsoft Docs
author: scottcate
description: 인증 서비스를 통해 사용자는 인증 쿠키를 수신 하기 위해 자격 증명을 제공할 수 있으며, 사용자 지정 사용자를 허용 하는 게이트웨이 서비스 ...
ms.author: riande
ms.date: 03/14/2008
ms.assetid: 6ab4efb6-aab6-45ac-ad2c-bdec5848ef9e
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
msc.type: authoredcontent
ms.openlocfilehash: cab9acb1ffd75cca87f6c575a6abdd000235828e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74635685"
---
# <a name="understanding-aspnet-ajax-authentication-and-profile-application-services"></a><span data-ttu-id="67c24-103">ASP.NET AJAX 인증 및 프로필 애플리케이션 서비스 이해</span><span class="sxs-lookup"><span data-stu-id="67c24-103">Understanding ASP.NET AJAX Authentication and Profile Application Services</span></span>

<span data-ttu-id="67c24-104">[Scott cate cda (](https://github.com/scottcate)</span><span class="sxs-lookup"><span data-stu-id="67c24-104">by [Scott Cate](https://github.com/scottcate)</span></span>

[<span data-ttu-id="67c24-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="67c24-105">Download PDF</span></span>](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial03_MSAjax_ASP.NET_Services_cs.pdf)

> <span data-ttu-id="67c24-106">인증 서비스를 통해 사용자는 인증 쿠키를 수신 하기 위해 자격 증명을 제공할 수 있으며, ASP.NET에서 제공 하는 사용자 지정 사용자 프로필을 허용 하는 게이트웨이 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-106">The Authentication service allows users to provide credentials in order to receive an authentication cookie, and is the gateway service to allow custom user profiles provided by ASP.NET.</span></span> <span data-ttu-id="67c24-107">ASP.NET AJAX 인증 서비스의 사용은 표준 ASP.NET Forms 인증과 호환 되므로 현재 폼 인증을 사용 하는 응용 프로그램 (예: 로그인 제어)은 AJAX 인증 서비스로 업그레이드 하 여 중단 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-107">Use of the ASP.NET AJAX authentication service is compatible with standard ASP.NET Forms authentication, so applications currently using Forms authentication (such as with the Login control) will not be broken by upgrading to the AJAX authentication service.</span></span>

## <a name="introduction"></a><span data-ttu-id="67c24-108">소개</span><span class="sxs-lookup"><span data-stu-id="67c24-108">Introduction</span></span>

<span data-ttu-id="67c24-109">.NET Framework 3.5의 일부로 Microsoft에서 자동으로 환경 업그레이드를 제공 합니다. 새 개발 환경을 사용할 수 있을 뿐 아니라 새로운 LINQ (통합 언어 쿼리) 기능 및 기타 언어 향상 기능을 곧 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-109">As part of the .NET Framework 3.5, Microsoft is delivering a sizable environment upgrade; not only is a new development environment available, but the new Language-Integrated Query (LINQ) features and other language enhancements are forthcoming.</span></span> <span data-ttu-id="67c24-110">또한 다른 도구 집합의 일부 익숙한 기능 (특히 ASP.NET AJAX 확장)은 .NET Framework 기본 클래스 라이브러리의 최고 수준의 멤버로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-110">In addition, some familiar features of other toolsets, notably the ASP.NET AJAX Extensions, are being included as first-class members of the .NET Framework Base Class Library.</span></span> <span data-ttu-id="67c24-111">이러한 확장을 통해 전체 페이지를 새로 고치지 않고도 페이지의 부분 렌더링, 클라이언트 스크립트를 통해 웹 서비스에 액세스 하는 기능 (ASP.NET 프로 파일링 API 포함) 및 광범위 한 클라이언트 쪽 API를 비롯 한 다양 한 새 리치 클라이언트 기능을 사용할 수 있습니다. ASP.NET 서버 쪽 컨트롤 집합에 표시 되는 많은 컨트롤 스키마를 미러링 하도록 디자인 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-111">These extensions enable many new rich client features, including partial rendering of pages without requiring a full page refresh, the ability to access Web Services via client script (including the ASP.NET profiling API), and an extensive client-side API designed to mirror many of the control schemes seen in the ASP.NET server-side control set.</span></span>

<span data-ttu-id="67c24-112">이 백서에서는 ASP.NET 프로 파일링 및 폼 인증 서비스를 구현 하 고 사용 하는 방법을 살펴봅니다. AJAX 확장 Microsoft ASP.NET AJAX 확장을 사용 하면 폼 인증을 쉽게 지원 하 고 프로 파일링 서비스는 웹 서비스 프록시 스크립트를 통해 노출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-112">This whitepaper looks at the implementation and use of the ASP.NET Profiling and Forms Authentication services as they are exposed by the Microsoft ASP.NET AJAX ExtensionsThe AJAX Extensions make Forms authentication incredibly easy to support, as it (as well as the Profiling Service) is exposed through a Web Service proxy script.</span></span> <span data-ttu-id="67c24-113">AJAX 확장은 AuthenticationServiceManager 클래스를 통한 사용자 지정 인증도 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-113">The AJAX Extensions also support custom authentication through the AuthenticationServiceManager class.</span></span>

<span data-ttu-id="67c24-114">이 백서는 Visual Studio 2008의 베타 2 릴리스와 .NET Framework 3.5을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-114">This whitepaper is based on the Beta 2 release of the Visual Studio 2008 and the .NET Framework 3.5.</span></span> <span data-ttu-id="67c24-115">또한이 백서에서는 visual Web Developer Express가 아닌 Visual Studio 2008 Beta 2를 사용 하 고 visual Studio의 사용자 인터페이스에 따라 연습을 제공 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-115">This whitepaper also assumes that you will be working with Visual Studio 2008 Beta 2, not Visual Web Developer Express, and will provide walkthroughs according to the user interface of Visual Studio.</span></span> <span data-ttu-id="67c24-116">일부 코드 샘플은 Visual Web Developer Express에서 사용할 수 없는 프로젝트 템플릿을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-116">Some code samples may utilize project templates unavailable in Visual Web Developer Express.</span></span>

## <a name="profiles-and-authentication"></a><span data-ttu-id="67c24-117">*프로필 및 인증*</span><span class="sxs-lookup"><span data-stu-id="67c24-117">*Profiles and Authentication*</span></span>

<span data-ttu-id="67c24-118">Microsoft ASP.NET 프로필 및 인증 서비스는 ASP.NET Forms 인증 시스템에서 제공 되며 ASP.NET의 표준 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-118">The Microsoft ASP.NET Profiles and Authentication services are provided by the ASP.NET Forms Authentication system, and are standard components of ASP.NET.</span></span> <span data-ttu-id="67c24-119">ASP.NET AJAX 확장은 클라이언트 AJAX 라이브러리의 Sys. Services 네임 스페이스 아래에서 매우 간단한 모델을 통해 스크립트 프록시를 통해 이러한 서비스에 대 한 스크립트 액세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-119">The ASP.NET AJAX Extensions provide script access to these services via script proxies, through a fairly straightforward model under the Sys.Services namespace of the client AJAX library.</span></span>

<span data-ttu-id="67c24-120">인증 서비스를 통해 사용자는 인증 쿠키를 수신 하기 위해 자격 증명을 제공할 수 있으며, ASP.NET에서 제공 하는 사용자 지정 사용자 프로필을 허용 하는 게이트웨이 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-120">The Authentication service allows users to provide credentials in order to receive an authentication cookie, and is the gateway service to allow custom user profiles provided by ASP.NET.</span></span> <span data-ttu-id="67c24-121">ASP.NET AJAX 인증 서비스의 사용은 표준 ASP.NET Forms 인증과 호환 되므로 현재 폼 인증을 사용 하는 응용 프로그램 (예: 로그인 제어)은 AJAX 인증 서비스로 업그레이드 하 여 중단 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-121">Use of the ASP.NET AJAX authentication service is compatible with standard ASP.NET Forms authentication, so applications currently using Forms authentication (such as with the Login control) will not be broken by upgrading to the AJAX authentication service.</span></span>

<span data-ttu-id="67c24-122">프로필 서비스를 사용 하면 인증 서비스에서 제공 하는 멤버 자격에 따라 사용자 데이터를 자동으로 통합 하 고 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-122">The Profile service allows the automatic integration and storage of user data based on membership as provided by the Authentication service.</span></span> <span data-ttu-id="67c24-123">저장 된 데이터는 web.config 파일에 의해 지정 되 고 다양 한 프로 파일링 서비스 공급자가 데이터 관리를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-123">The stored data is specified by the web.config file, and the various profiling service providers handle the data management.</span></span> <span data-ttu-id="67c24-124">인증 서비스와 마찬가지로 AJAX 프로필 서비스는 표준 ASP.NET profile 서비스와 호환 되므로 ASP.NET Profile 서비스의 기능을 통합 하는 페이지는 AJAX 지원을 포함 하 여 중단 되어서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-124">As with the Authentication service, the AJAX Profile service is compatible with the standard ASP.NET profile service, so that pages currently incorporating features of the ASP.NET Profile service should not be broken by including AJAX support.</span></span>

<span data-ttu-id="67c24-125">ASP.NET 인증 및 프로 파일링 서비스를 응용 프로그램에 통합 하는 것은이 백서에서 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-125">Incorporating the ASP.NET Authentication and Profiling services themselves into an application is outside of the scope of this whitepaper.</span></span> <span data-ttu-id="67c24-126">항목에 대 한 자세한 내용은 MSDN Library 참조 문서 [https://msdn.microsoft.com/library/tw292whz.aspx](https://msdn.microsoft.com/library/tw292whz.aspx)에서 멤버 자격을 사용 하 여 사용자 관리를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="67c24-126">For more information on the topic, see the MSDN Library reference article Managing Users by Using Membership at [https://msdn.microsoft.com/library/tw292whz.aspx](https://msdn.microsoft.com/library/tw292whz.aspx).</span></span> <span data-ttu-id="67c24-127">ASP.NET에는 ASP.NET 멤버 자격에 대 한 기본 인증 서비스 공급자 인 SQL Server를 사용 하 여 멤버 자격을 자동으로 설정 하는 유틸리티도 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-127">ASP.NET also includes a utility to automatically set up Membership with a SQL Server, which is the default authentication service provider for ASP.NET Membership.</span></span> <span data-ttu-id="67c24-128">자세한 내용은 [https://msdn.microsoft.com/library/ms229862(vs.80).aspx](https://msdn.microsoft.com/library/ms229862(vs.80).aspx)에서 ASP.NET SQL Server 등록 도구 (Aspnet\_ regsql .exe) 문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="67c24-128">For more information, see the article ASP.NET SQL Server Registration Tool (Aspnet\_regsql.exe) at [https://msdn.microsoft.com/library/ms229862(vs.80).aspx](https://msdn.microsoft.com/library/ms229862(vs.80).aspx).</span></span>

## <a name="using-the-aspnet-ajax-authentication-service"></a><span data-ttu-id="67c24-129">*ASP.NET AJAX 인증 서비스 사용*</span><span class="sxs-lookup"><span data-stu-id="67c24-129">*Using the ASP.NET AJAX Authentication Service*</span></span>

<span data-ttu-id="67c24-130">ASP.NET AJAX 인증 서비스를 web.config 파일에서 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-130">The ASP.NET AJAX Authentication service must be enabled in the web.config file:</span></span>

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample1.xml)]

<span data-ttu-id="67c24-131">인증 서비스를 사용 하려면 ASP.NET Forms 인증을 사용 하도록 설정 해야 하며 클라이언트 브라우저에서 쿠키를 사용 하도록 설정 해야 합니다. 쿠키가 없는 세션에는 URL 매개 변수가 필요 하므로 스크립트는 쿠키 없는 세션을 활성화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-131">The Authentication service requires ASP.NET Forms authentication to be enabled and requires cookies to be enabled on the client browser (a script cannot enable a cookieless session since cookieless sessions require URL parameters).</span></span>

<span data-ttu-id="67c24-132">AJAX 인증 서비스를 사용 하도록 설정 하 고 구성 하면 클라이언트 스크립트에서 해당 개체를 즉시 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-132">Once the AJAX authentication service is enabled and configured, client script can immediately take advantage of the Sys.Services.AuthenticationService object.</span></span> <span data-ttu-id="67c24-133">기본적으로 클라이언트 스크립트는 `login` 메서드와 `isLoggedIn` 속성을 활용 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-133">Primarily, client script will want to take advantage of the `login` method and `isLoggedIn` property.</span></span> <span data-ttu-id="67c24-134">다 수의 매개 변수를 받아들일 수 있는 login 메서드의 기본값을 제공 하는 몇 가지 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-134">Several properties exist to provide defaults for the login method, which can accept a large number of parameters.</span></span>

<span data-ttu-id="67c24-135">*Sys.debug 서비스 멤버*</span><span class="sxs-lookup"><span data-stu-id="67c24-135">*Sys.Services.AuthenticationService members*</span></span>

<span data-ttu-id="67c24-136">*로그인 방법:*</span><span class="sxs-lookup"><span data-stu-id="67c24-136">*login method:*</span></span>

<span data-ttu-id="67c24-137">Login () 메서드는 사용자의 자격 증명을 인증 하는 요청을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-137">The login() method begins a request to authenticate the user's credentials.</span></span> <span data-ttu-id="67c24-138">이 메서드는 비동기적 이며 실행을 차단 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-138">This method is asynchronous and does not block execution.</span></span>

<span data-ttu-id="67c24-139">*변수의*</span><span class="sxs-lookup"><span data-stu-id="67c24-139">*Parameters:*</span></span>

| <span data-ttu-id="67c24-140">**매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="67c24-140">**Parameter Name**</span></span> | <span data-ttu-id="67c24-141">**임을**</span><span class="sxs-lookup"><span data-stu-id="67c24-141">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="67c24-142">userName</span><span class="sxs-lookup"><span data-stu-id="67c24-142">userName</span></span> | <span data-ttu-id="67c24-143">필수</span><span class="sxs-lookup"><span data-stu-id="67c24-143">Required.</span></span> <span data-ttu-id="67c24-144">인증할 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-144">The username to authenticate.</span></span> |
| <span data-ttu-id="67c24-145">암호</span><span class="sxs-lookup"><span data-stu-id="67c24-145">password</span></span> | <span data-ttu-id="67c24-146">선택 사항입니다. 기본값은 null입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-146">Optional (defaults to null).</span></span> <span data-ttu-id="67c24-147">사용자의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-147">The user's password.</span></span> |
| <span data-ttu-id="67c24-148">isPersistent</span><span class="sxs-lookup"><span data-stu-id="67c24-148">isPersistent</span></span> | <span data-ttu-id="67c24-149">선택 사항입니다 (기본값은 false).</span><span class="sxs-lookup"><span data-stu-id="67c24-149">Optional (defaults to false).</span></span> <span data-ttu-id="67c24-150">사용자의 인증 쿠키를 세션 간에 유지할지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-150">Whether the user's authentication cookie should persist across sessions.</span></span> <span data-ttu-id="67c24-151">False 이면 브라우저가 닫히거나 세션이 만료 되 면 사용자가 로그 아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-151">If false, the user will log out when the browser is closed or the session expires.</span></span> |
| <span data-ttu-id="67c24-152">redirectUrl</span><span class="sxs-lookup"><span data-stu-id="67c24-152">redirectUrl</span></span> | <span data-ttu-id="67c24-153">선택 사항입니다. 기본값은 null입니다. 인증에 성공 하면 브라우저를 리디렉션할 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-153">Optional (defaults to null).The URL to redirect the browser to upon successful authentication.</span></span> <span data-ttu-id="67c24-154">이 매개 변수가 null 또는 빈 문자열인 경우 리디렉션이 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-154">If this parameter is null or an empty string, no redirection occurs.</span></span> |
| <span data-ttu-id="67c24-155">customInfo</span><span class="sxs-lookup"><span data-stu-id="67c24-155">customInfo</span></span> | <span data-ttu-id="67c24-156">선택 사항입니다. 기본값은 null입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-156">Optional (defaults to null).</span></span> <span data-ttu-id="67c24-157">이 매개 변수는 현재 사용 되지 않으며 나중에 사용 하도록 예약 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-157">This parameter is currently unused and is reserved for future use.</span></span> |
| <span data-ttu-id="67c24-158">loginCompletedCallback</span><span class="sxs-lookup"><span data-stu-id="67c24-158">loginCompletedCallback</span></span> | <span data-ttu-id="67c24-159">선택 사항입니다. 기본값은 null입니다. 로그인이 성공적으로 완료 되었을 때 호출할 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-159">Optional (defaults to null).The function to call when the login has successfully completed.</span></span> <span data-ttu-id="67c24-160">지정 된 경우이 매개 변수는 defaultLoginCompleted 속성을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-160">If specified, this parameter overrides the defaultLoginCompleted property.</span></span> |
| <span data-ttu-id="67c24-161">failedCallback</span><span class="sxs-lookup"><span data-stu-id="67c24-161">failedCallback</span></span> | <span data-ttu-id="67c24-162">선택 사항입니다. 기본값은 null입니다. 로그인이 실패 했을 때 호출할 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-162">Optional (defaults to null).The function to call when the login has failed.</span></span> <span data-ttu-id="67c24-163">지정 된 경우이 매개 변수는 defaultFailedCallback 속성을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-163">If specified, this parameter overrides the defaultFailedCallback property.</span></span> |
| <span data-ttu-id="67c24-164">userContext</span><span class="sxs-lookup"><span data-stu-id="67c24-164">userContext</span></span> | <span data-ttu-id="67c24-165">선택 사항입니다. 기본값은 null입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-165">Optional (defaults to null).</span></span> <span data-ttu-id="67c24-166">콜백 함수에 전달 되어야 하는 사용자 지정 사용자 컨텍스트 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-166">Custom user context data that should be passed to the callback functions.</span></span> |

<span data-ttu-id="67c24-167">*반환 값:*</span><span class="sxs-lookup"><span data-stu-id="67c24-167">*Return Value:*</span></span>

<span data-ttu-id="67c24-168">이 함수에는 반환 값이 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-168">This function does not include a return value.</span></span> <span data-ttu-id="67c24-169">그러나이 함수에 대 한 호출이 완료 되 면 많은 동작이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-169">However, a number of behaviors are included upon completion of a call to this function:</span></span>

- <span data-ttu-id="67c24-170">`redirectUrl` 매개 변수가 null 또는 빈 문자열이 아닌 경우 현재 페이지가 새로 고쳐지고 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-170">The current page will either be refreshed or be changed if the `redirectUrl` parameter was neither null nor an empty string.</span></span>
- <span data-ttu-id="67c24-171">그러나 매개 변수가 null 이거나 빈 문자열인 경우에는 `loginCompletedCallback` 매개 변수 또는 `defaultLoginCompletedCallback` 속성이 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-171">However, if the parameter was null or an empty string, the `loginCompletedCallback` parameter, or `defaultLoginCompletedCallback` property is called.</span></span>
- <span data-ttu-id="67c24-172">웹 서비스에 대 한 호출이 실패 하면 `defaultFailedCallback` 속성의 `failedCallback` 매개 변수가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-172">If the call to the web service fails, the `failedCallback` parameter of `defaultFailedCallback` property is called.</span></span>

<span data-ttu-id="67c24-173">*로그 아웃 방법:*</span><span class="sxs-lookup"><span data-stu-id="67c24-173">*logout method:*</span></span>

<span data-ttu-id="67c24-174">Logout () 메서드는 자격 증명 쿠키를 제거 하 고 웹 응용 프로그램에서 현재 사용자를 로그 아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-174">The logout() method removes the credentials cookie and logs out the current user from the web application.</span></span>

<span data-ttu-id="67c24-175">*변수의*</span><span class="sxs-lookup"><span data-stu-id="67c24-175">*Parameters:*</span></span>

| <span data-ttu-id="67c24-176">**매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="67c24-176">**Parameter Name**</span></span> | <span data-ttu-id="67c24-177">**임을**</span><span class="sxs-lookup"><span data-stu-id="67c24-177">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="67c24-178">redirectUrl</span><span class="sxs-lookup"><span data-stu-id="67c24-178">redirectUrl</span></span> | <span data-ttu-id="67c24-179">선택 사항입니다. 기본값은 null입니다. 인증에 성공 하면 브라우저를 리디렉션할 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-179">Optional (defaults to null).The URL to redirect the browser to upon successful authentication.</span></span> <span data-ttu-id="67c24-180">이 매개 변수가 null 또는 빈 문자열인 경우 리디렉션이 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-180">If this parameter is null or an empty string, no redirection occurs.</span></span> |
| <span data-ttu-id="67c24-181">logoutCompletedCallback</span><span class="sxs-lookup"><span data-stu-id="67c24-181">logoutCompletedCallback</span></span> | <span data-ttu-id="67c24-182">선택 사항입니다. 기본값은 null입니다. 로그 아웃이 성공적으로 완료 되었을 때 호출할 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-182">Optional (defaults to null).The function to call when the logout has successfully completed.</span></span> <span data-ttu-id="67c24-183">지정 된 경우이 매개 변수는 defaultLogoutCompleted 속성을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-183">If specified, this parameter overrides the defaultLogoutCompleted property.</span></span> |
| <span data-ttu-id="67c24-184">failedCallback</span><span class="sxs-lookup"><span data-stu-id="67c24-184">failedCallback</span></span> | <span data-ttu-id="67c24-185">선택 사항입니다. 기본값은 null입니다. 로그인이 실패 했을 때 호출할 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-185">Optional (defaults to null).The function to call when the login has failed.</span></span> <span data-ttu-id="67c24-186">지정 된 경우이 매개 변수는 defaultFailedCallback 속성을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-186">If specified, this parameter overrides the defaultFailedCallback property.</span></span> |
| <span data-ttu-id="67c24-187">userContext</span><span class="sxs-lookup"><span data-stu-id="67c24-187">userContext</span></span> | <span data-ttu-id="67c24-188">선택 사항입니다. 기본값은 null입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-188">Optional (defaults to null).</span></span> <span data-ttu-id="67c24-189">콜백 함수에 전달 되어야 하는 사용자 지정 사용자 컨텍스트 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-189">Custom user context data that should be passed to the callback functions.</span></span> |

<span data-ttu-id="67c24-190">*반환 값:*</span><span class="sxs-lookup"><span data-stu-id="67c24-190">*Return Value:*</span></span>

<span data-ttu-id="67c24-191">이 함수에는 반환 값이 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-191">This function does not include a return value.</span></span> <span data-ttu-id="67c24-192">그러나이 함수에 대 한 호출이 완료 되 면 많은 동작이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-192">However, a number of behaviors are included upon completion of a call to this function:</span></span>

- <span data-ttu-id="67c24-193">`redirectUrl` 매개 변수가 null 또는 빈 문자열이 아닌 경우 현재 페이지가 새로 고쳐지고 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-193">The current page will either be refreshed or be changed if the `redirectUrl` parameter was neither null nor an empty string.</span></span>
- <span data-ttu-id="67c24-194">그러나 매개 변수가 null 이거나 빈 문자열인 경우에는 `logoutCompletedCallback` 매개 변수 또는 `defaultLogoutCompletedCallback` 속성이 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-194">However, if the parameter was null or an empty string, the `logoutCompletedCallback` parameter, or `defaultLogoutCompletedCallback` property is called.</span></span>
- <span data-ttu-id="67c24-195">웹 서비스에 대 한 호출이 실패 하면 `defaultFailedCallback` 속성의 `failedCallback` 매개 변수가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-195">If the call to the web service fails, the `failedCallback` parameter of `defaultFailedCallback` property is called.</span></span>

<span data-ttu-id="67c24-196">*defaultFailedCallback 속성 (get, set):*</span><span class="sxs-lookup"><span data-stu-id="67c24-196">*defaultFailedCallback property (get, set):*</span></span>

<span data-ttu-id="67c24-197">이 속성은 웹 서비스와의 통신에 실패 한 경우 호출 해야 하는 함수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-197">This property specifies a function that should be called if a failure to communicate with the web service occurs.</span></span> <span data-ttu-id="67c24-198">대리자 (또는 함수 참조)를 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-198">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="67c24-199">이 속성에 지정 된 함수 참조에는 다음 서명이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-199">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample2.js)]

<span data-ttu-id="67c24-200">*변수의*</span><span class="sxs-lookup"><span data-stu-id="67c24-200">*Parameters:*</span></span>

| <span data-ttu-id="67c24-201">**매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="67c24-201">**Parameter Name**</span></span> | <span data-ttu-id="67c24-202">**임을**</span><span class="sxs-lookup"><span data-stu-id="67c24-202">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="67c24-203">오류</span><span class="sxs-lookup"><span data-stu-id="67c24-203">error</span></span> | <span data-ttu-id="67c24-204">오류 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-204">Specifies the error information.</span></span> |
| <span data-ttu-id="67c24-205">userContext</span><span class="sxs-lookup"><span data-stu-id="67c24-205">userContext</span></span> | <span data-ttu-id="67c24-206">Login 또는 logout 함수를 호출할 때 제공 되는 사용자 컨텍스트 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-206">Specifies the user context information provided when the login or logout function was called.</span></span> |
| <span data-ttu-id="67c24-207">methodName</span><span class="sxs-lookup"><span data-stu-id="67c24-207">methodName</span></span> | <span data-ttu-id="67c24-208">호출 메서드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-208">The name of the calling method.</span></span> |

<span data-ttu-id="67c24-209">*defaultLoginCompletedCallback 속성 (get, set):*</span><span class="sxs-lookup"><span data-stu-id="67c24-209">*defaultLoginCompletedCallback property (get, set):*</span></span>

<span data-ttu-id="67c24-210">이 속성은 로그인 웹 서비스 호출이 완료 될 때 호출 되어야 하는 함수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-210">This property specifies a function that should be called when the login web service call has completed.</span></span> <span data-ttu-id="67c24-211">대리자 (또는 함수 참조)를 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-211">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="67c24-212">이 속성에 지정 된 함수 참조에는 다음 서명이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-212">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample3.js)]

<span data-ttu-id="67c24-213">*변수의*</span><span class="sxs-lookup"><span data-stu-id="67c24-213">*Parameters:*</span></span>

| <span data-ttu-id="67c24-214">**매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="67c24-214">**Parameter Name**</span></span> | <span data-ttu-id="67c24-215">**임을**</span><span class="sxs-lookup"><span data-stu-id="67c24-215">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="67c24-216">유효한 자격 증명</span><span class="sxs-lookup"><span data-stu-id="67c24-216">validCredentials</span></span> | <span data-ttu-id="67c24-217">사용자가 유효한 자격 증명을 제공 했는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-217">Specifies whether the user provided valid credentials.</span></span> <span data-ttu-id="67c24-218">사용자가 성공적으로 로그인 한 경우 `true` 합니다. 그렇지 않으면 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-218">`true` if the user successfully logged in; otherwise `false`.</span></span> |
| <span data-ttu-id="67c24-219">userContext</span><span class="sxs-lookup"><span data-stu-id="67c24-219">userContext</span></span> | <span data-ttu-id="67c24-220">로그인 함수가 호출 될 때 제공 되는 사용자 컨텍스트 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-220">Specifies the user context information provided when the login function was called.</span></span> |
| <span data-ttu-id="67c24-221">methodName</span><span class="sxs-lookup"><span data-stu-id="67c24-221">methodName</span></span> | <span data-ttu-id="67c24-222">호출 메서드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-222">The name of the calling method.</span></span> |

<span data-ttu-id="67c24-223">*defaultLogoutCompletedCallback 속성 (get, set):*</span><span class="sxs-lookup"><span data-stu-id="67c24-223">*defaultLogoutCompletedCallback property (get, set):*</span></span>

<span data-ttu-id="67c24-224">이 속성은 로그 아웃 웹 서비스 호출이 완료 될 때 호출 되어야 하는 함수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-224">This property specifies a function that should be called when the logout web service call has completed.</span></span> <span data-ttu-id="67c24-225">대리자 (또는 함수 참조)를 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-225">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="67c24-226">이 속성에 지정 된 함수 참조에는 다음 서명이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-226">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample4.js)]

<span data-ttu-id="67c24-227">*변수의*</span><span class="sxs-lookup"><span data-stu-id="67c24-227">*Parameters:*</span></span>

| <span data-ttu-id="67c24-228">**매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="67c24-228">**Parameter Name**</span></span> | <span data-ttu-id="67c24-229">**임을**</span><span class="sxs-lookup"><span data-stu-id="67c24-229">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="67c24-230">result</span><span class="sxs-lookup"><span data-stu-id="67c24-230">result</span></span> | <span data-ttu-id="67c24-231">이 매개 변수는 항상 `null`됩니다. 나중에 사용 하도록 예약 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-231">This parameter will always be `null`; it is reserved for future use.</span></span> |
| <span data-ttu-id="67c24-232">userContext</span><span class="sxs-lookup"><span data-stu-id="67c24-232">userContext</span></span> | <span data-ttu-id="67c24-233">로그인 함수가 호출 될 때 제공 되는 사용자 컨텍스트 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-233">Specifies the user context information provided when the login function was called.</span></span> |
| <span data-ttu-id="67c24-234">methodName</span><span class="sxs-lookup"><span data-stu-id="67c24-234">methodName</span></span> | <span data-ttu-id="67c24-235">호출 메서드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-235">The name of the calling method.</span></span> |

<span data-ttu-id="67c24-236">*isLoggedIn 속성 (get):*</span><span class="sxs-lookup"><span data-stu-id="67c24-236">*isLoggedIn property (get):*</span></span>

<span data-ttu-id="67c24-237">이 속성은 사용자의 현재 인증 상태를 가져옵니다. 페이지 요청 중에 ScriptManager 개체에 의해 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-237">This property gets the current authentication state of the user; it is set by the ScriptManager object during a page request.</span></span>

<span data-ttu-id="67c24-238">이 속성은 사용자가 현재 로그인 한 경우 `true`를 반환 합니다. 그렇지 않으면 `false`을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-238">This property returns `true` if the user is currently logged in; otherwise, it returns `false`.</span></span>

<span data-ttu-id="67c24-239">*path 속성 (get, set):*</span><span class="sxs-lookup"><span data-stu-id="67c24-239">*path property (get, set):*</span></span>

<span data-ttu-id="67c24-240">이 속성은 인증 웹 서비스의 위치를 프로그래밍 방식으로 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-240">This property programmatically determines the location of the authentication web service.</span></span> <span data-ttu-id="67c24-241">이를 사용 하 여 기본 인증 공급자를 재정의 하 고 하나는 ScriptManager 컨트롤의 AuthenticationService 자식 노드의 Path 속성에서 선언적으로 설정할 수 있습니다. 자세한 내용은 사용자 지정 인증 서비스 공급자 사용을 참조 하세요. 항목을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="67c24-241">It can be used to override the default authentication provider, as well as one set declaratively in the Path property of the ScriptManager control's AuthenticationService child node (for more information, see the Using a Custom Authentication Service Provider topic below).</span></span>

<span data-ttu-id="67c24-242">기본 인증 서비스의 위치는 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-242">Note that the location of the default authentication service does not change.</span></span> <span data-ttu-id="67c24-243">그러나 ASP.NET AJAX를 사용 하면 ASP.NET AJAX 인증 서비스 프록시와 동일한 클래스 인터페이스를 제공 하는 웹 서비스의 위치를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-243">However, ASP.NET AJAX allows you to specify the location of a web service that provides the same class interface as the ASP.NET AJAX authentication service proxy.</span></span>

<span data-ttu-id="67c24-244">또한이 속성을 현재 사이트에서 스크립트 요청을 보내는 값으로 설정 하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-244">Note also that this property should not be set to a value that directs the script request off of the current site.</span></span> <span data-ttu-id="67c24-245">현재 응용 프로그램은 인증 자격 증명을 받지 않으므로 쓸모가 없습니다. 또한 기본 AJAX 기술은 교차 사이트 요청을 게시 해서는 안 되며 클라이언트 브라우저에서 보안 예외를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-245">Because the current application would not receive the authentication credentials, it would be useless; also, the technology underlying AJAX should not post cross-site requests, and may generate a security exception in the client browser.</span></span>

<span data-ttu-id="67c24-246">이 속성은 인증 웹 서비스에 대 한 경로를 나타내는 `String` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-246">This property is a `String` object representing the path to the authentication web service.</span></span>

<span data-ttu-id="67c24-247">*timeout 속성 (get, set):*</span><span class="sxs-lookup"><span data-stu-id="67c24-247">*timeout property (get, set):*</span></span>

<span data-ttu-id="67c24-248">이 속성은 로그인 요청이 실패 했다고 가정 하기 전에 인증 서비스를 대기 하는 시간을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-248">This property determines the length of time to wait for the authentication service before assuming the login request has failed.</span></span> <span data-ttu-id="67c24-249">호출이 완료 될 때까지 대기 하는 동안 제한 시간이 만료 되 면 요청-실패 콜백이 호출 되 고 호출이 완료 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-249">If the timeout expires while waiting for a call to complete, the request-failed callback will be called, and the call will not complete.</span></span>

<span data-ttu-id="67c24-250">이 속성은 인증 서비스의 결과를 대기 하는 시간 (밀리초)을 나타내는 `Number` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-250">This property is a `Number` object representing the number of milliseconds to wait for results from the authentication service.</span></span>

<span data-ttu-id="67c24-251">*코드 샘플: 인증 서비스에 로그인*</span><span class="sxs-lookup"><span data-stu-id="67c24-251">*Code Sample: Logging into the Authentication Service*</span></span>

<span data-ttu-id="67c24-252">다음 태그는 AuthenticationService 클래스의 login 및 logout 메서드에 대 한 간단한 스크립트 호출을 포함 하는 예제 ASP.NET 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-252">The following markup is an example ASP.NET page with a simple script call to the login and logout methods of the AuthenticationService class.</span></span>

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample5.aspx)]

## <a name="accessing-aspnet-profiling-data-via-ajax"></a><span data-ttu-id="67c24-253">AJAX를 통해 ASP.NET 프로 파일링 데이터 액세스</span><span class="sxs-lookup"><span data-stu-id="67c24-253">Accessing ASP.NET Profiling Data via AJAX</span></span>

<span data-ttu-id="67c24-254">또한 ASP.NET 프로 파일링 서비스는 ASP.NET AJAX 확장을 통해 노출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-254">The ASP.NET profiling service is also exposed through the ASP.NET AJAX Extensions.</span></span> <span data-ttu-id="67c24-255">ASP.NET 프로 파일링 서비스는 사용자 데이터를 저장 하 고 검색할 수 있는 풍부 하 고 세부적인 API를 제공 하므로이는 뛰어난 생산성 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-255">Since the ASP.NET profiling service provides a rich, granular API by which to store and retrieve user data, this can be an excellent productivity tool.</span></span>

<span data-ttu-id="67c24-256">프로필 서비스를 web.config에서 사용 하도록 설정 해야 합니다. 기본적으로는 그렇지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-256">The profile service must be enabled in web.config; it is not by default.</span></span> <span data-ttu-id="67c24-257">이렇게 하려면 web.config에서 `profileService` 자식 요소가 enabled = true로 지정 되었는지 확인 하 고 다음과 같이 읽거나 쓸 수 있는 속성을 지정 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-257">To do so, ensure that the `profileService` child element has enabled= true specified in web.config, and that you have specified which properties can be read or written as follows:</span></span>

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample6.xml)]

<span data-ttu-id="67c24-258">또한 프로필 서비스를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-258">The profile service must also be configured.</span></span> <span data-ttu-id="67c24-259">프로 파일링 서비스의 구성은이 백서에서 다루지 않지만 프로필 구성 설정에 정의 된 그룹은 그룹 이름의 하위 속성으로 액세스할 수 있다는 점에 유의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-259">Although configuration of the profiling service is outside of the scope of this whitepaper, it is worthwhile to note that groups as defined in profile configuration settings will be accessible as sub-properties of the group name.</span></span> <span data-ttu-id="67c24-260">예를 들어, 다음 프로필 섹션을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-260">For example, with the following profile section specified:</span></span>

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample7.xml)]

<span data-ttu-id="67c24-261">클라이언트 스크립트는 ProfileService 클래스의 속성 필드의 속성으로 Name, Address. 줄 1, Line2, address. City 및 BackgroundColor에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-261">Client script would be able to access Name, Address.Line1, Address.Line2, Address.City, Address.State, Address.Zip, and BackgroundColor as properties of the properties field of the ProfileService class.</span></span>

<span data-ttu-id="67c24-262">AJAX 프로 파일링 서비스가 구성 되 면 페이지에서 즉시 사용할 수 있게 됩니다. 하지만 사용 하기 전에 한 번 로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-262">Once the AJAX Profiling Service is configured, it will be immediately available in pages; however, it will have to be loaded once before use.</span></span>

<span data-ttu-id="67c24-263">*ProfileService 멤버*</span><span class="sxs-lookup"><span data-stu-id="67c24-263">*Sys.Services.ProfileService members*</span></span>

<span data-ttu-id="67c24-264">*속성 필드:*</span><span class="sxs-lookup"><span data-stu-id="67c24-264">*properties field:*</span></span>

<span data-ttu-id="67c24-265">속성 필드는 모든 구성 된 프로필 데이터를 점-연산자 이름 규칙에서 참조할 수 있는 자식 속성으로 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-265">The properties field exposes all configured profile data as child properties that can be referenced by the dot-operator-name convention.</span></span> <span data-ttu-id="67c24-266">속성 그룹의 자식인 속성을 GroupName. PropertyName 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-266">Properties that are children of property groups are referred to as GroupName.PropertyName.</span></span> <span data-ttu-id="67c24-267">위에서 제공한 예제 프로필 구성에서 사용자의 상태를 가져오려면 다음 식별자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-267">In the example profile configuration presented above, to get the state of the user, you could use the following identifier:</span></span>

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample8.cs)]

<span data-ttu-id="67c24-268">*로드 방법:*</span><span class="sxs-lookup"><span data-stu-id="67c24-268">*load method:*</span></span>

<span data-ttu-id="67c24-269">서버에서 선택한 목록 또는 모든 속성을 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-269">Loads a selected list or all properties from the server.</span></span>

<span data-ttu-id="67c24-270">*변수의*</span><span class="sxs-lookup"><span data-stu-id="67c24-270">*Parameters:*</span></span>

| <span data-ttu-id="67c24-271">**매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="67c24-271">**Parameter Name**</span></span> | <span data-ttu-id="67c24-272">**임을**</span><span class="sxs-lookup"><span data-stu-id="67c24-272">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="67c24-273">propertyNames</span><span class="sxs-lookup"><span data-stu-id="67c24-273">propertyNames</span></span> | <span data-ttu-id="67c24-274">선택 사항입니다. 기본값은 null입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-274">Optional (defaults to null).</span></span> <span data-ttu-id="67c24-275">서버에서 로드 되는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-275">The properties to be loaded from the server.</span></span> |
| <span data-ttu-id="67c24-276">loadCompletedCallback</span><span class="sxs-lookup"><span data-stu-id="67c24-276">loadCompletedCallback</span></span> | <span data-ttu-id="67c24-277">선택 사항입니다. 기본값은 null입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-277">Optional (defaults to null).</span></span> <span data-ttu-id="67c24-278">로드가 완료 될 때 호출할 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-278">The function to call when loading has completed.</span></span> |
| <span data-ttu-id="67c24-279">failedCallback</span><span class="sxs-lookup"><span data-stu-id="67c24-279">failedCallback</span></span> | <span data-ttu-id="67c24-280">선택 사항입니다. 기본값은 null입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-280">Optional (defaults to null).</span></span> <span data-ttu-id="67c24-281">오류가 발생 하는 경우 호출할 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-281">The function to call if an error occurs.</span></span> |
| <span data-ttu-id="67c24-282">userContext</span><span class="sxs-lookup"><span data-stu-id="67c24-282">userContext</span></span> | <span data-ttu-id="67c24-283">선택 사항입니다. 기본값은 null입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-283">Optional (defaults to null).</span></span> <span data-ttu-id="67c24-284">콜백 함수에 전달할 컨텍스트 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-284">Context information to be passed to the callback function.</span></span> |

<span data-ttu-id="67c24-285">Load 함수에는 반환 값이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-285">The load function does not have a return value.</span></span> <span data-ttu-id="67c24-286">호출이 성공적으로 완료 되 면 `loadCompletedCallback` 매개 변수 또는 `defaultLoadCompletedCallback` 속성 중 하나를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-286">If the call completed successfully, it will call either the `loadCompletedCallback` parameter or `defaultLoadCompletedCallback` property.</span></span> <span data-ttu-id="67c24-287">호출이 실패 했거나 제한 시간이 만료 되 면 `failedCallback` 매개 변수 또는 `defaultFailedCallback` 속성이 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-287">If the call failed, or the timeout expired, either the `failedCallback` parameter or `defaultFailedCallback` property will be called.</span></span>

<span data-ttu-id="67c24-288">`propertyNames` 매개 변수를 지정 하지 않으면 모든 읽기 구성 속성이 서버에서 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-288">If the `propertyNames` parameter is not supplied, all read-configured properties are retrieved from the server.</span></span>

<span data-ttu-id="67c24-289">*저장 방법:*</span><span class="sxs-lookup"><span data-stu-id="67c24-289">*save method:*</span></span>

<span data-ttu-id="67c24-290">Save () 메서드는 지정 된 속성 목록 (또는 모든 속성)을 사용자의 ASP.NET 프로필에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-290">The save() method saves the specified property list (or all properties) to the user's ASP.NET profile.</span></span>

<span data-ttu-id="67c24-291">*변수의*</span><span class="sxs-lookup"><span data-stu-id="67c24-291">*Parameters:*</span></span>

| <span data-ttu-id="67c24-292">**매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="67c24-292">**Parameter Name**</span></span> | <span data-ttu-id="67c24-293">**임을**</span><span class="sxs-lookup"><span data-stu-id="67c24-293">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="67c24-294">propertyNames</span><span class="sxs-lookup"><span data-stu-id="67c24-294">propertyNames</span></span> | <span data-ttu-id="67c24-295">선택 사항입니다. 기본값은 null입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-295">Optional (defaults to null).</span></span> <span data-ttu-id="67c24-296">서버에 저장 되는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-296">The properties to be saved to the server.</span></span> |
| <span data-ttu-id="67c24-297">saveCompletedCallback</span><span class="sxs-lookup"><span data-stu-id="67c24-297">saveCompletedCallback</span></span> | <span data-ttu-id="67c24-298">선택 사항입니다. 기본값은 null입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-298">Optional (defaults to null).</span></span> <span data-ttu-id="67c24-299">저장이 완료 될 때 호출할 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-299">The function to call when saving has completed.</span></span> |
| <span data-ttu-id="67c24-300">failedCallback</span><span class="sxs-lookup"><span data-stu-id="67c24-300">failedCallback</span></span> | <span data-ttu-id="67c24-301">선택 사항입니다. 기본값은 null입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-301">Optional (defaults to null).</span></span> <span data-ttu-id="67c24-302">오류가 발생 하는 경우 호출할 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-302">The function to call if an error occurs.</span></span> |
| <span data-ttu-id="67c24-303">userContext</span><span class="sxs-lookup"><span data-stu-id="67c24-303">userContext</span></span> | <span data-ttu-id="67c24-304">선택 사항입니다. 기본값은 null입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-304">Optional (defaults to null).</span></span> <span data-ttu-id="67c24-305">콜백 함수에 전달할 컨텍스트 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-305">Context information to be passed to the callback function.</span></span> |

<span data-ttu-id="67c24-306">저장 함수에 반환 값이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-306">The save function does not have a return value.</span></span> <span data-ttu-id="67c24-307">호출이 성공적으로 완료 되 면 `saveCompletedCallback` 매개 변수 또는 `defaultSaveCompletedCallback` 속성 중 하나를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-307">If the call completes successfully, it will call either the `saveCompletedCallback` parameter or `defaultSaveCompletedCallback` property.</span></span> <span data-ttu-id="67c24-308">호출이 실패 했거나 제한 시간이 만료 된 경우 `failedCallback` 또는 `defaultFailedCallback` 속성이 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-308">If the call failed, or the timeout expired, either the `failedCallback` or `defaultFailedCallback` property will be called.</span></span>

<span data-ttu-id="67c24-309">`propertyNames` 매개 변수가 null 이면 모든 프로필 속성이 서버에 전송 되 고 서버는 저장할 수 있는 속성과 수행할 수 없는 속성을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-309">If the `propertyNames` parameter is null, all profile properties will be sent to the server, and the server will decide which properties can be saved and which cannot.</span></span>

<span data-ttu-id="67c24-310">*defaultFailedCallback 속성 (get, set):*</span><span class="sxs-lookup"><span data-stu-id="67c24-310">*defaultFailedCallback property (get, set):*</span></span>

<span data-ttu-id="67c24-311">이 속성은 웹 서비스와의 통신에 실패 한 경우 호출 해야 하는 함수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-311">This property specifies a function that should be called if a failure to communicate with the web service occurs.</span></span> <span data-ttu-id="67c24-312">대리자 (또는 함수 참조)를 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-312">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="67c24-313">이 속성에 지정 된 함수 참조에는 다음 서명이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-313">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample9.js)]

<span data-ttu-id="67c24-314">*변수의*</span><span class="sxs-lookup"><span data-stu-id="67c24-314">*Parameters:*</span></span>

| <span data-ttu-id="67c24-315">**매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="67c24-315">**Parameter Name**</span></span> | <span data-ttu-id="67c24-316">**임을**</span><span class="sxs-lookup"><span data-stu-id="67c24-316">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="67c24-317">오류</span><span class="sxs-lookup"><span data-stu-id="67c24-317">Error</span></span> | <span data-ttu-id="67c24-318">오류 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-318">Specifies the error information.</span></span> |
| <span data-ttu-id="67c24-319">userContext</span><span class="sxs-lookup"><span data-stu-id="67c24-319">userContext</span></span> | <span data-ttu-id="67c24-320">Load 또는 save 함수를 호출할 때 제공 되는 사용자 컨텍스트 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-320">Specifies the user context information provided when the load or save function was called.</span></span> |
| <span data-ttu-id="67c24-321">methodName</span><span class="sxs-lookup"><span data-stu-id="67c24-321">methodName</span></span> | <span data-ttu-id="67c24-322">호출 메서드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-322">The name of the calling method.</span></span> |

<span data-ttu-id="67c24-323">*defaultSaveCompleted 속성 (get, set):*</span><span class="sxs-lookup"><span data-stu-id="67c24-323">*defaultSaveCompleted property (get, set):*</span></span>

<span data-ttu-id="67c24-324">이 속성은 사용자의 프로필 데이터 저장이 완료 될 때 호출 되어야 하는 함수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-324">This property specifies a function that should be called upon the completion of saving the user's profile data.</span></span> <span data-ttu-id="67c24-325">대리자 (또는 함수 참조)를 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-325">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="67c24-326">이 속성에 지정 된 함수 참조에는 다음 서명이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-326">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample10.js)]

<span data-ttu-id="67c24-327">*변수의*</span><span class="sxs-lookup"><span data-stu-id="67c24-327">*Parameters:*</span></span>

| <span data-ttu-id="67c24-328">**매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="67c24-328">**Parameter Name**</span></span> | <span data-ttu-id="67c24-329">**임을**</span><span class="sxs-lookup"><span data-stu-id="67c24-329">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="67c24-330">numPropsSaved</span><span class="sxs-lookup"><span data-stu-id="67c24-330">numPropsSaved</span></span> | <span data-ttu-id="67c24-331">저장 된 속성의 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-331">Specifies the number of properties that were saved.</span></span> |
| <span data-ttu-id="67c24-332">userContext</span><span class="sxs-lookup"><span data-stu-id="67c24-332">userContext</span></span> | <span data-ttu-id="67c24-333">Load 또는 save 함수를 호출할 때 제공 되는 사용자 컨텍스트 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-333">Specifies the user context information provided when the load or save function was called.</span></span> |
| <span data-ttu-id="67c24-334">methodName</span><span class="sxs-lookup"><span data-stu-id="67c24-334">methodName</span></span> | <span data-ttu-id="67c24-335">호출 메서드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-335">The name of the calling method.</span></span> |

<span data-ttu-id="67c24-336">*defaultLoadCompleted 속성 (get, set):*</span><span class="sxs-lookup"><span data-stu-id="67c24-336">*defaultLoadCompleted property (get, set):*</span></span>

<span data-ttu-id="67c24-337">이 속성은 사용자의 프로필 데이터 로드가 완료 될 때 호출 되어야 하는 함수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-337">This property specifies a function that should be called upon the completion of loading of the user's profile data.</span></span> <span data-ttu-id="67c24-338">대리자 (또는 함수 참조)를 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-338">It should receive a delegate (or function reference).</span></span>

<span data-ttu-id="67c24-339">이 속성에 지정 된 함수 참조에는 다음 서명이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-339">The function reference specified by this property should have the following signature:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample11.js)]

<span data-ttu-id="67c24-340">*변수의*</span><span class="sxs-lookup"><span data-stu-id="67c24-340">*Parameters:*</span></span>

| <span data-ttu-id="67c24-341">**매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="67c24-341">**Parameter Name**</span></span> | <span data-ttu-id="67c24-342">**임을**</span><span class="sxs-lookup"><span data-stu-id="67c24-342">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="67c24-343">numPropsLoaded</span><span class="sxs-lookup"><span data-stu-id="67c24-343">numPropsLoaded</span></span> | <span data-ttu-id="67c24-344">로드 되는 속성 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-344">Specifies the number of properties loaded.</span></span> |
| <span data-ttu-id="67c24-345">userContext</span><span class="sxs-lookup"><span data-stu-id="67c24-345">userContext</span></span> | <span data-ttu-id="67c24-346">Load 또는 save 함수를 호출할 때 제공 되는 사용자 컨텍스트 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-346">Specifies the user context information provided when the load or save function was called.</span></span> |
| <span data-ttu-id="67c24-347">methodName</span><span class="sxs-lookup"><span data-stu-id="67c24-347">methodName</span></span> | <span data-ttu-id="67c24-348">호출 메서드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-348">The name of the calling method.</span></span> |

<span data-ttu-id="67c24-349">*path 속성 (get, set):*</span><span class="sxs-lookup"><span data-stu-id="67c24-349">*path property (get, set):*</span></span>

<span data-ttu-id="67c24-350">이 속성은 프로필 웹 서비스의 위치를 프로그래밍 방식으로 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-350">This property programmatically determines the location of the profile web service.</span></span> <span data-ttu-id="67c24-351">이를 사용 하 여 기본 프로필 서비스 공급자를 재정의 하 고 ScriptManager 컨트롤의 ProfileService 자식 노드의 Path 속성에서 set을 선언적으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-351">It can be used to override the default profile service provider, as well as one set declaratively in the Path property of the ScriptManager control's ProfileService child node.</span></span>

<span data-ttu-id="67c24-352">기본 프로필 서비스의 위치는 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-352">Note that the location of the default profile service does not change.</span></span> <span data-ttu-id="67c24-353">그러나 ASP.NET AJAX를 사용 하면 ASP.NET AJAX 인증 서비스 프록시와 동일한 클래스 인터페이스를 제공 하는 웹 서비스의 위치를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-353">However, ASP.NET AJAX allows you to specify the location of a web service that provides the same class interface as the ASP.NET AJAX authentication service proxy.</span></span>

<span data-ttu-id="67c24-354">또한이 속성을 현재 사이트에서 스크립트 요청을 보내는 값으로 설정 하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-354">Note also that this property should not be set to a value that directs the script request off of the current site.</span></span> <span data-ttu-id="67c24-355">기술 기본 AJAX는 교차 사이트 요청을 게시 해서는 안 되며 클라이언트 브라우저에서 보안 예외를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-355">The technology underlying AJAX should not post cross-site requests, and may generate a security exception in the client browser.</span></span>

<span data-ttu-id="67c24-356">이 속성은 프로필 웹 서비스에 대 한 경로를 나타내는 `String` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-356">This property is a `String` object representing the path to the profile web service.</span></span>

<span data-ttu-id="67c24-357">*timeout 속성 (get, set):*</span><span class="sxs-lookup"><span data-stu-id="67c24-357">*timeout property (get, set):*</span></span>

<span data-ttu-id="67c24-358">이 속성은 로드 또는 저장 요청이 실패 했다고 가정 하기 전에 프로필 서비스를 대기 하는 시간을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-358">This property determines the length of time to wait for the profile service before assuming the load or save request has failed.</span></span> <span data-ttu-id="67c24-359">호출이 완료 될 때까지 대기 하는 동안 제한 시간이 만료 되 면 요청-실패 콜백이 호출 되 고 호출이 완료 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-359">If the timeout expires while waiting for a call to complete, the request-failed callback will be called, and the call will not complete.</span></span>

<span data-ttu-id="67c24-360">이 속성은 프로필 서비스의 결과를 대기 하는 시간 (밀리초)을 나타내는 `Number` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-360">This property is a `Number` object representing the number of milliseconds to wait for results from the profile service.</span></span>

<span data-ttu-id="67c24-361">*코드 샘플: 페이지 로드 시 프로필 데이터 로드*</span><span class="sxs-lookup"><span data-stu-id="67c24-361">*Code sample: Loading profile data at page load*</span></span>

<span data-ttu-id="67c24-362">다음 코드에서는 사용자가 인증 되었는지 여부를 확인 하 고,이 경우 사용자의 기본 배경색을 페이지의 기본 배경색으로 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-362">The following code will check to see whether a user is authenticated, and if so, will load the user's preferred background color as the page's.</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample12.js)]

## <a name="using-a-custom-authentication-service-provider"></a><span data-ttu-id="67c24-363">*사용자 지정 인증 서비스 공급자 사용*</span><span class="sxs-lookup"><span data-stu-id="67c24-363">*Using a Custom Authentication Service Provider*</span></span>

<span data-ttu-id="67c24-364">ASP.NET AJAX 확장을 사용 하면 사용자 지정 웹 서비스를 통해 기능을 노출 하 여 사용자 지정 스크립트 인증 서비스 공급자를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-364">The ASP.NET AJAX Extensions allow you to create a custom script authentication service provider by exposing your functionality through a custom web service.</span></span> <span data-ttu-id="67c24-365">웹 서비스는 사용 하기 위해 `Login` 및 `Logout`의 두 메서드를 노출 해야 합니다. 및 이러한 메서드는 기본 ASP.NET AJAX 인증 웹 서비스와 동일한 메서드 서명으로 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-365">In order to be used, your web service must expose two methods, `Login` and `Logout`; and these methods must be specified with the same method signatures as the default ASP.NET AJAX Authentication web service.</span></span>

<span data-ttu-id="67c24-366">사용자 지정 웹 서비스를 만든 후에는 페이지에서 선언적으로 또는 코드에서 프로그래밍 방식으로 또는 클라이언트 스크립트를 통해 경로를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-366">Once you have created the custom web service, you will need to specify the path to it, either declaratively on your page, programmatically in code, or via the client script.</span></span>

<span data-ttu-id="67c24-367">*경로를 선언적으로 설정 하려면 다음을 수행 합니다.*</span><span class="sxs-lookup"><span data-stu-id="67c24-367">*To set the path declaratively:*</span></span>

<span data-ttu-id="67c24-368">경로를 선언적으로 설정 하려면 ASP.NET 페이지에 ScriptManager 개체의 AuthenticationService 자식을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-368">To set the path declaratively, include the AuthenticationService child of the ScriptManager object on your ASP.NET page:</span></span>

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample13.aspx)]

<span data-ttu-id="67c24-369">*코드에서 경로를 설정 하려면:*</span><span class="sxs-lookup"><span data-stu-id="67c24-369">*To set the path in code:*</span></span>

<span data-ttu-id="67c24-370">경로를 프로그래밍 방식으로 설정 하려면 스크립트 관리자의 인스턴스를 통해 경로를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-370">To set the path programmatically, specify the path via the instance of your script manager:</span></span>

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample14.cs)]

<span data-ttu-id="67c24-371">*스크립트에서 경로를 설정 하려면:*</span><span class="sxs-lookup"><span data-stu-id="67c24-371">*To set the path in script:*</span></span>

<span data-ttu-id="67c24-372">스크립트에서 프로그래밍 방식으로 경로를 설정 하려면 AuthenticationService 클래스의 `path` 속성을 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-372">To set the path programmatically in script, utilize the `path` property of the AuthenticationService class:</span></span>

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample15.js)]

<span data-ttu-id="67c24-373">*사용자 지정 인증용 샘플 웹 서비스*</span><span class="sxs-lookup"><span data-stu-id="67c24-373">*Sample Web Service for Custom Authentication*</span></span>

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample16.aspx)]

## <a name="summary"></a><span data-ttu-id="67c24-374">요약</span><span class="sxs-lookup"><span data-stu-id="67c24-374">Summary</span></span>

<span data-ttu-id="67c24-375">ASP.NET services-특히 프로 파일링, 멤버 자격 및 인증 서비스는 클라이언트 브라우저에서 JavaScript에 쉽게 노출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-375">ASP.NET services - specifically the profiling, membership, and authentication services - are easily exposed to JavaScript on the client browser.</span></span> <span data-ttu-id="67c24-376">이를 통해 개발자는 UpdatePanels와 같은 컨트롤에 의존 하지 않고 클라이언트 쪽 코드를 인증 메커니즘과 원활 하 게 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-376">This allows developers to integrate their client-side code with the authentication mechanism seamlessly, without depending on controls such as UpdatePanels to do the heavy lifting.</span></span> <span data-ttu-id="67c24-377">웹 구성 설정을 활용 하 여 클라이언트 에서도 프로필 데이터를 보호할 수 있습니다. 기본적으로 사용할 수 있는 데이터가 없으며 개발자는 프로필 속성을 옵트인 (opt in) 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-377">Profile data can be protected from the client as well, by utilizing web configuration settings; no data is available by default, and developers must opt-in to profile properties.</span></span>

<span data-ttu-id="67c24-378">또한 개발자는 동일한 메서드 서명을 사용 하 여 간단한 웹 서비스 구현을 만들어 이러한 내장 ASP.NET 서비스에 대 한 사용자 지정 스크립트 공급자를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-378">Furthermore, by creating simplified web service implementations with equivalent method signatures, developers can create custom script providers for these intrinsic ASP.NET services.</span></span> <span data-ttu-id="67c24-379">이러한 기술을 지원 하면 풍부한 클라이언트 응용 프로그램의 개발을 간소화 하는 동시에 개발자에 게 특정 요구를 충족 하는 다양 한 유연성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-379">Support for these techniques simplifies the development of rich client applications, while providing developers with a wide range of flexibility to meet specific needs.</span></span>

## <a name="bio"></a><span data-ttu-id="67c24-380">*약력*</span><span class="sxs-lookup"><span data-stu-id="67c24-380">*Bio*</span></span>

<span data-ttu-id="67c24-381">Scott Cate cda (는 1997부터 Microsoft 웹 기술을 사용 하 고 있으며 기술 자료 소프트웨어 솔루션에 초점을 맞춘 ASP.NET 기반 응용 프로그램을 전문적으로 작성 하는[www.myKB.com](http://www.myKB.com)(myKB.com)의 부사장입니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-381">Scott Cate has been working with Microsoft Web technologies since 1997 and is the President of myKB.com ([www.myKB.com](http://www.myKB.com)) where he specializes in writing ASP.NET based applications focused on Knowledge Base Software solutions.</span></span> <span data-ttu-id="67c24-382">Scott은 [scott.cate@myKB.com](mailto:scott.cate@myKB.com) 또는 [ScottCate.com](http://ScottCate.com) 의 블로그의 전자 메일을 통해 연락할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67c24-382">Scott can be contacted via email at [scott.cate@myKB.com](mailto:scott.cate@myKB.com) or his blog at [ScottCate.com](http://ScottCate.com)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="67c24-383">[이전](understanding-asp-net-ajax-updatepanel-triggers.md)
> [다음](understanding-asp-net-ajax-localization.md)</span><span class="sxs-lookup"><span data-stu-id="67c24-383">[Previous](understanding-asp-net-ajax-updatepanel-triggers.md)
[Next](understanding-asp-net-ajax-localization.md)</span></span>
