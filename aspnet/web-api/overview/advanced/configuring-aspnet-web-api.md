---
uid: web-api/overview/advanced/configuring-aspnet-web-api
title: ASP.NET Web API 2-ASP.NET 4.x 구성
author: MikeWasson
description: 'ASP.NET 4.x에 대해 2 ASP.NET Web API 구성: 설정, ASP.NET 4.x 호스팅, OWIN 셀프 호스팅, 글로벌 서비스 및 이전 컨트롤러 구성을 구성 합니다.'
ms.author: riande
ms.date: 03/31/2014
ms.custom: seoapril2019
ms.assetid: 9e10a700-8d91-4d2e-a31e-b8b569fe867c
msc.legacyurl: /web-api/overview/advanced/configuring-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 4f76728fa5e4602e35e1b7cb2d41b2245093cad8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449345"
---
# <a name="configuring-aspnet-web-api-2"></a><span data-ttu-id="509ec-103">ASP.NET Web API 2 구성</span><span class="sxs-lookup"><span data-stu-id="509ec-103">Configuring ASP.NET Web API 2</span></span>

<span data-ttu-id="509ec-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="509ec-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="509ec-105">이 항목에서는 ASP.NET Web API를 구성 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-105">This topic describes how to configure ASP.NET Web API.</span></span>

- [<span data-ttu-id="509ec-106">구성 설정</span><span class="sxs-lookup"><span data-stu-id="509ec-106">Configuration Settings</span></span>](#settings)
- [<span data-ttu-id="509ec-107">ASP.NET 호스팅을 사용 하 여 Web API 구성</span><span class="sxs-lookup"><span data-stu-id="509ec-107">Configuring Web API with ASP.NET Hosting</span></span>](#webhost)
- [<span data-ttu-id="509ec-108">OWIN 자체 호스팅을 사용 하 여 Web API 구성</span><span class="sxs-lookup"><span data-stu-id="509ec-108">Configuring Web API with OWIN Self-Hosting</span></span>](#selfhost)
- [<span data-ttu-id="509ec-109">전역 웹 API 서비스</span><span class="sxs-lookup"><span data-stu-id="509ec-109">Global Web API Services</span></span>](#services)
- [<span data-ttu-id="509ec-110">컨트롤러 단위 구성</span><span class="sxs-lookup"><span data-stu-id="509ec-110">Per-Controller Configuration</span></span>](#percontrollerconfig)

<a id="settings"></a>
## <a name="configuration-settings"></a><span data-ttu-id="509ec-111">구성 설정</span><span class="sxs-lookup"><span data-stu-id="509ec-111">Configuration Settings</span></span>

<span data-ttu-id="509ec-112">웹 API 구성 설정은 [httpconfiguration](https://msdn.microsoft.com/library/system.web.http.httpconfiguration.aspx) 클래스에서 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-112">Web API configuration settings are defined in the [HttpConfiguration](https://msdn.microsoft.com/library/system.web.http.httpconfiguration.aspx) class.</span></span>

| <span data-ttu-id="509ec-113">멤버</span><span class="sxs-lookup"><span data-stu-id="509ec-113">Member</span></span> | <span data-ttu-id="509ec-114">Description</span><span class="sxs-lookup"><span data-stu-id="509ec-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="509ec-115">**DependencyResolver**</span><span class="sxs-lookup"><span data-stu-id="509ec-115">**DependencyResolver**</span></span> | <span data-ttu-id="509ec-116">컨트롤러에 대 한 종속성 주입을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-116">Enables dependency injection for controllers.</span></span> <span data-ttu-id="509ec-117">[웹 API 종속성 해결 프로그램 사용을](dependency-injection.md)참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="509ec-117">See [Using the Web API Dependency Resolver](dependency-injection.md).</span></span> |
| <span data-ttu-id="509ec-118">**필터**</span><span class="sxs-lookup"><span data-stu-id="509ec-118">**Filters**</span></span> | <span data-ttu-id="509ec-119">작업 필터.</span><span class="sxs-lookup"><span data-stu-id="509ec-119">Action filters.</span></span> |
| <span data-ttu-id="509ec-120">**포맷터**</span><span class="sxs-lookup"><span data-stu-id="509ec-120">**Formatters**</span></span> | <span data-ttu-id="509ec-121">[미디어 유형 포맷터](../formats-and-model-binding/media-formatters.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-121">[Media-type formatters](../formats-and-model-binding/media-formatters.md).</span></span> |
| <span data-ttu-id="509ec-122">**IncludeErrorDetailPolicy**</span><span class="sxs-lookup"><span data-stu-id="509ec-122">**IncludeErrorDetailPolicy**</span></span> | <span data-ttu-id="509ec-123">HTTP 응답 메시지에 예외 메시지 및 스택 추적과 같은 오류 정보를 서버에 포함할지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-123">Specifies whether the server should include error details, such as exception messages and stack traces, in HTTP response messages.</span></span> <span data-ttu-id="509ec-124">[IncludeErrorDetailPolicy](https://msdn.microsoft.com/library/system.web.http.includeerrordetailpolicy(v=vs.108))를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="509ec-124">See [IncludeErrorDetailPolicy](https://msdn.microsoft.com/library/system.web.http.includeerrordetailpolicy(v=vs.108)).</span></span> |
| <span data-ttu-id="509ec-125">**이니셜라이저**</span><span class="sxs-lookup"><span data-stu-id="509ec-125">**Initializer**</span></span> | <span data-ttu-id="509ec-126">**Httpconfiguration**의 최종 초기화를 수행 하는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-126">A function that performs final initialization of the **HttpConfiguration**.</span></span> |
| <span data-ttu-id="509ec-127">**MessageHandlers**</span><span class="sxs-lookup"><span data-stu-id="509ec-127">**MessageHandlers**</span></span> | <span data-ttu-id="509ec-128">[HTTP 메시지 처리기](http-message-handlers.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-128">[HTTP message handlers](http-message-handlers.md).</span></span> |
| <span data-ttu-id="509ec-129">**ParameterBindingRules**</span><span class="sxs-lookup"><span data-stu-id="509ec-129">**ParameterBindingRules**</span></span> | <span data-ttu-id="509ec-130">컨트롤러 작업에 대 한 매개 변수를 바인딩하는 규칙의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-130">A collection of rules for binding parameters on controller actions.</span></span> |
| <span data-ttu-id="509ec-131">**속성**</span><span class="sxs-lookup"><span data-stu-id="509ec-131">**Properties**</span></span> | <span data-ttu-id="509ec-132">일반 속성 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-132">A generic property bag.</span></span> |
| <span data-ttu-id="509ec-133">**경로**</span><span class="sxs-lookup"><span data-stu-id="509ec-133">**Routes**</span></span> | <span data-ttu-id="509ec-134">경로 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-134">The collection of routes.</span></span> <span data-ttu-id="509ec-135">[ASP.NET Web API에서 라우팅을](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="509ec-135">See [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span> |
| <span data-ttu-id="509ec-136">**Services**</span><span class="sxs-lookup"><span data-stu-id="509ec-136">**Services**</span></span> | <span data-ttu-id="509ec-137">서비스의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-137">The collection of services.</span></span> <span data-ttu-id="509ec-138">[서비스](#services)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="509ec-138">See [Services](#services).</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="509ec-139">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="509ec-139">Prerequisites</span></span>

<span data-ttu-id="509ec-140">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional 또는 Enterprise 버전</span><span class="sxs-lookup"><span data-stu-id="509ec-140">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional, or Enterprise edition.</span></span>

<a id="webhost"></a>
## <a name="configuring-web-api-with-aspnet-hosting"></a><span data-ttu-id="509ec-141">ASP.NET 호스팅을 사용 하 여 Web API 구성</span><span class="sxs-lookup"><span data-stu-id="509ec-141">Configuring Web API with ASP.NET Hosting</span></span>

<span data-ttu-id="509ec-142">ASP.NET 응용 프로그램에서 **응용 프로그램\_Start** 메서드에서 [Globalconfiguration. 구성](https://msdn.microsoft.com/library/system.web.http.globalconfiguration.configure.aspx) 을 호출 하 여 Web API를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-142">In an ASP.NET application, configure Web API by calling [GlobalConfiguration.Configure](https://msdn.microsoft.com/library/system.web.http.globalconfiguration.configure.aspx) in the **Application\_Start** method.</span></span> <span data-ttu-id="509ec-143">**Configure** 메서드는 **httpconfiguration**형식의 단일 매개 변수를 사용 하 여 대리자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-143">The **Configure** method takes a delegate with a single parameter of type **HttpConfiguration**.</span></span> <span data-ttu-id="509ec-144">대리자 내의 모든 구성을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-144">Perform all of your configuration inside the delegate.</span></span>

<span data-ttu-id="509ec-145">익명 대리자를 사용 하는 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-145">Here is an example using an anonymous delegate:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="509ec-146">Visual Studio 2017에서는 **새 ASP.NET 프로젝트** 대화 상자에서 "web API"를 선택 하면 "ASP.NET 웹 응용 프로그램" 프로젝트 템플릿이 자동으로 구성 코드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-146">In Visual Studio 2017, the "ASP.NET Web Application" project template automatically sets up the configuration code, if you select "Web API" in the **New ASP.NET Project** dialog.</span></span>

[![](configuring-aspnet-web-api/_static/image2.png)](configuring-aspnet-web-api/_static/image1.png)

<span data-ttu-id="509ec-147">프로젝트 템플릿은 앱\_시작 폴더 내에 WebApiConfig.cs 라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-147">The project template creates a file named WebApiConfig.cs inside the App\_Start folder.</span></span> <span data-ttu-id="509ec-148">이 코드 파일은 웹 API 구성 코드를 저장 해야 하는 대리자를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-148">This code file defines the delegate where you should put your Web API configuration code.</span></span>

![](configuring-aspnet-web-api/_static/image3.png)

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample2.cs?highlight=12)]

<span data-ttu-id="509ec-149">또한 프로젝트 템플릿은 응용 프로그램에서 대리자를 호출 하는 코드를 **시작\_** 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-149">The project template also adds the code that calls the delegate from **Application\_Start**.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample3.cs?highlight=5)]

<a id="selfhost"></a>
## <a name="configuring-web-api-with-owin-self-hosting"></a><span data-ttu-id="509ec-150">OWIN 자체 호스팅을 사용 하 여 Web API 구성</span><span class="sxs-lookup"><span data-stu-id="509ec-150">Configuring Web API with OWIN Self-Hosting</span></span>

<span data-ttu-id="509ec-151">OWIN를 사용 하 여 자체 호스트 하는 경우 새 **Httpconfiguration** 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-151">If you are self-hosting with OWIN, create a new **HttpConfiguration** instance.</span></span> <span data-ttu-id="509ec-152">이 인스턴스에서 구성을 수행 하 고 인스턴스를 **Owin. UseWebApi** 확장 메서드로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-152">Perform any configuration on this instance, and then pass the instance to the **Owin.UseWebApi** extension method.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="509ec-153">[OWIN를 사용 하 여 자체 호스트 ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md) 에서 전체 단계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-153">The tutorial [Use OWIN to Self-Host ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md) shows the complete steps.</span></span>

<a id="services"></a>
## <a name="global-web-api-services"></a><span data-ttu-id="509ec-154">전역 웹 API 서비스</span><span class="sxs-lookup"><span data-stu-id="509ec-154">Global Web API Services</span></span>

<span data-ttu-id="509ec-155">**Httpconfiguration. Services** 컬렉션에는 Web API가 컨트롤러 선택 및 콘텐츠 협상과 같은 다양 한 작업을 수행 하는 데 사용 하는 글로벌 서비스 집합이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-155">The **HttpConfiguration.Services** collection contains a set of global services that Web API uses to perform various tasks, such as controller selection and content negotiation.</span></span>

> [!NOTE]
> <span data-ttu-id="509ec-156">서비스 **컬렉션은** 서비스 검색 또는 종속성 주입에 대 한 일반적인 용도의 메커니즘이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-156">The **Services** collection is not a general-purpose mechanism for service discovery or dependency injection.</span></span> <span data-ttu-id="509ec-157">웹 API 프레임 워크에 알려진 서비스 유형만 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-157">It only stores service types that are known to the Web API framework.</span></span>

<span data-ttu-id="509ec-158">**서비스** 컬렉션은 기본 서비스 집합을 사용 하 여 초기화 되며, 사용자 지정 구현을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-158">The **Services** collection is initialized with a default set of services, and you can provide your own custom implementations.</span></span> <span data-ttu-id="509ec-159">일부 서비스는 여러 인스턴스를 지원 하지만 다른 서비스는 하나의 인스턴스만 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-159">Some services support multiple instances, while others can have only one instance.</span></span> <span data-ttu-id="509ec-160">그러나 컨트롤러 수준에서 서비스를 제공할 수도 있습니다. [컨트롤러 단위 구성](#percontrollerconfig)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="509ec-160">(However, you can also provide services at the controller level; see [Per-Controller Configuration](#percontrollerconfig).</span></span>

<span data-ttu-id="509ec-161">단일 인스턴스 서비스</span><span class="sxs-lookup"><span data-stu-id="509ec-161">Single-Instance Services</span></span>

| <span data-ttu-id="509ec-162">서비스</span><span class="sxs-lookup"><span data-stu-id="509ec-162">Service</span></span> | <span data-ttu-id="509ec-163">Description</span><span class="sxs-lookup"><span data-stu-id="509ec-163">Description</span></span> |
| --- | --- |
| <span data-ttu-id="509ec-164">**IActionValueBinder**</span><span class="sxs-lookup"><span data-stu-id="509ec-164">**IActionValueBinder**</span></span> | <span data-ttu-id="509ec-165">매개 변수에 대 한 바인딩을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-165">Gets a binding for a parameter.</span></span> |
| <span data-ttu-id="509ec-166">**IApiExplorer**</span><span class="sxs-lookup"><span data-stu-id="509ec-166">**IApiExplorer**</span></span> | <span data-ttu-id="509ec-167">응용 프로그램에서 노출 하는 Api에 대 한 설명을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-167">Gets descriptions of the APIs exposed by the application.</span></span> <span data-ttu-id="509ec-168">[웹 API에 대 한 도움말 페이지 만들기](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="509ec-168">See [Creating a Help Page for a Web API](../getting-started-with-aspnet-web-api/creating-api-help-pages.md).</span></span> |
| <span data-ttu-id="509ec-169">**IAssembliesResolver**</span><span class="sxs-lookup"><span data-stu-id="509ec-169">**IAssembliesResolver**</span></span> | <span data-ttu-id="509ec-170">응용 프로그램에 대 한 어셈블리의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-170">Gets a list of the assemblies for the application.</span></span> <span data-ttu-id="509ec-171">[라우팅 및 작업 선택을](../web-api-routing-and-actions/routing-and-action-selection.md)참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="509ec-171">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="509ec-172">**IBodyModelValidator**</span><span class="sxs-lookup"><span data-stu-id="509ec-172">**IBodyModelValidator**</span></span> | <span data-ttu-id="509ec-173">미디어 형식 포맷터에 의해 요청 본문에서 읽은 모델의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-173">Validates a model that is read from the request body by a media-type formatter.</span></span> |
| <span data-ttu-id="509ec-174">**IContentNegotiator**</span><span class="sxs-lookup"><span data-stu-id="509ec-174">**IContentNegotiator**</span></span> | <span data-ttu-id="509ec-175">콘텐츠 협상을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-175">Performs content negotiation.</span></span> |
| <span data-ttu-id="509ec-176">**IDocumentationProvider**</span><span class="sxs-lookup"><span data-stu-id="509ec-176">**IDocumentationProvider**</span></span> | <span data-ttu-id="509ec-177">Api에 대 한 설명서를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-177">Provides documentation for APIs.</span></span> <span data-ttu-id="509ec-178">기본값은 **null**입니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-178">The default is **null**.</span></span> <span data-ttu-id="509ec-179">[웹 API에 대 한 도움말 페이지 만들기](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="509ec-179">See [Creating a Help Page for a Web API](../getting-started-with-aspnet-web-api/creating-api-help-pages.md).</span></span> |
| <span data-ttu-id="509ec-180">**IHostBufferPolicySelector**</span><span class="sxs-lookup"><span data-stu-id="509ec-180">**IHostBufferPolicySelector**</span></span> | <span data-ttu-id="509ec-181">호스트가 HTTP 메시지 엔터티 본문을 버퍼링 해야 하는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-181">Indicates whether the host should buffer HTTP message entity bodies.</span></span> |
| <span data-ttu-id="509ec-182">**IHttpActionInvoker**</span><span class="sxs-lookup"><span data-stu-id="509ec-182">**IHttpActionInvoker**</span></span> | <span data-ttu-id="509ec-183">컨트롤러 동작을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-183">Invokes a controller action.</span></span> <span data-ttu-id="509ec-184">[라우팅 및 작업 선택을](../web-api-routing-and-actions/routing-and-action-selection.md)참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="509ec-184">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="509ec-185">**IHttpActionSelector**</span><span class="sxs-lookup"><span data-stu-id="509ec-185">**IHttpActionSelector**</span></span> | <span data-ttu-id="509ec-186">컨트롤러 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-186">Selects a controller action.</span></span> <span data-ttu-id="509ec-187">[라우팅 및 작업 선택을](../web-api-routing-and-actions/routing-and-action-selection.md)참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="509ec-187">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="509ec-188">**IHttpControllerActivator**</span><span class="sxs-lookup"><span data-stu-id="509ec-188">**IHttpControllerActivator**</span></span> | <span data-ttu-id="509ec-189">컨트롤러를 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-189">Activates a controller.</span></span> <span data-ttu-id="509ec-190">[라우팅 및 작업 선택을](../web-api-routing-and-actions/routing-and-action-selection.md)참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="509ec-190">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="509ec-191">**IHttpControllerSelector**</span><span class="sxs-lookup"><span data-stu-id="509ec-191">**IHttpControllerSelector**</span></span> | <span data-ttu-id="509ec-192">컨트롤러를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-192">Selects a controller.</span></span> <span data-ttu-id="509ec-193">[라우팅 및 작업 선택을](../web-api-routing-and-actions/routing-and-action-selection.md)참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="509ec-193">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="509ec-194">**IHttpControllerTypeResolver**</span><span class="sxs-lookup"><span data-stu-id="509ec-194">**IHttpControllerTypeResolver**</span></span> | <span data-ttu-id="509ec-195">응용 프로그램의 Web API 컨트롤러 형식 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-195">Provides a list of the Web API controller types in the application.</span></span> <span data-ttu-id="509ec-196">[라우팅 및 작업 선택을](../web-api-routing-and-actions/routing-and-action-selection.md)참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="509ec-196">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="509ec-197">**ITraceManager**</span><span class="sxs-lookup"><span data-stu-id="509ec-197">**ITraceManager**</span></span> | <span data-ttu-id="509ec-198">추적 프레임 워크를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-198">Initializes the tracing framework.</span></span> <span data-ttu-id="509ec-199">[ASP.NET Web API 추적을](../testing-and-debugging/tracing-in-aspnet-web-api.md)참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="509ec-199">See [Tracing in ASP.NET Web API](../testing-and-debugging/tracing-in-aspnet-web-api.md).</span></span> |
| <span data-ttu-id="509ec-200">**ITraceWriter**</span><span class="sxs-lookup"><span data-stu-id="509ec-200">**ITraceWriter**</span></span> | <span data-ttu-id="509ec-201">추적 작성기를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-201">Provides a trace writer.</span></span> <span data-ttu-id="509ec-202">기본값은 "no op" 추적 기록기입니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-202">The default is a "no-op" trace writer.</span></span> <span data-ttu-id="509ec-203">[ASP.NET Web API 추적을](../testing-and-debugging/tracing-in-aspnet-web-api.md)참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="509ec-203">See [Tracing in ASP.NET Web API](../testing-and-debugging/tracing-in-aspnet-web-api.md).</span></span> |
| <span data-ttu-id="509ec-204">**IModelValidatorCache**</span><span class="sxs-lookup"><span data-stu-id="509ec-204">**IModelValidatorCache**</span></span> | <span data-ttu-id="509ec-205">모델 유효성 검사기의 캐시를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-205">Provides a cache of model validators.</span></span> |

<span data-ttu-id="509ec-206">여러 인스턴스 서비스</span><span class="sxs-lookup"><span data-stu-id="509ec-206">Multiple-Instance Services</span></span>

|                 <span data-ttu-id="509ec-207">서비스</span><span class="sxs-lookup"><span data-stu-id="509ec-207">Service</span></span>                 |                                                                                                              <span data-ttu-id="509ec-208">Description</span><span class="sxs-lookup"><span data-stu-id="509ec-208">Description</span></span>                                                                                                               |
|-----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <span data-ttu-id="509ec-209"><strong>IFilterProvider</strong></span><span class="sxs-lookup"><span data-stu-id="509ec-209"><strong>IFilterProvider</strong></span></span>     |                                                                                           <span data-ttu-id="509ec-210">컨트롤러 작업에 대 한 필터 목록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-210">Returns a list of filters for a controller action.</span></span>                                                                                           |
|  <span data-ttu-id="509ec-211"><strong>ModelBinderProvider</strong></span><span class="sxs-lookup"><span data-stu-id="509ec-211"><strong>ModelBinderProvider</strong></span></span>   |                                                                                                <span data-ttu-id="509ec-212">지정 된 형식에 대 한 모델 바인더를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-212">Returns a model binder for a given type.</span></span>                                                                                                |
| <span data-ttu-id="509ec-213"><strong>ModelMetadataProvider</strong></span><span class="sxs-lookup"><span data-stu-id="509ec-213"><strong>ModelMetadataProvider</strong></span></span>  |                                                                                                     <span data-ttu-id="509ec-214">모델에 대 한 메타 데이터를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-214">Provides metadata for a model.</span></span>                                                                                                     |
| <span data-ttu-id="509ec-215"><strong>ModelValidatorProvider</strong></span><span class="sxs-lookup"><span data-stu-id="509ec-215"><strong>ModelValidatorProvider</strong></span></span> |                                                                                                   <span data-ttu-id="509ec-216">모델에 대 한 유효성 검사기를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-216">Provides a validator for a model.</span></span>                                                                                                    |
|  <span data-ttu-id="509ec-217"><strong>ValueProviderFactory</strong></span><span class="sxs-lookup"><span data-stu-id="509ec-217"><strong>ValueProviderFactory</strong></span></span>  | <span data-ttu-id="509ec-218">값 공급자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-218">Creates a value provider.</span></span> <span data-ttu-id="509ec-219">자세한 내용은 Mike 정지의 블로그 게시물 [WebAPI에서 사용자 지정 값 공급자를 만드는 방법](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="509ec-219">For more information, see Mike Stall's blog post [How to create a custom value provider in WebAPI](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)</span></span> |

<span data-ttu-id="509ec-220">다중 인스턴스 서비스에 사용자 지정 구현을 추가 하려면 **서비스** 컬렉션에서 **add** 또는 **Insert** 를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-220">To add a custom implementation to a multi-instance service, call **Add** or **Insert** on the **Services** collection:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="509ec-221">단일 인스턴스 서비스를 사용자 지정 구현으로 바꾸려면 **서비스** 컬렉션에서 **replace** 를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-221">To replace a single-instance service with a custom implementation, call **Replace** on the **Services** collection:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample6.cs)]

<a id="percontrollerconfig"></a>
## <a name="per-controller-configuration"></a><span data-ttu-id="509ec-222">컨트롤러 단위 구성</span><span class="sxs-lookup"><span data-stu-id="509ec-222">Per-Controller Configuration</span></span>

<span data-ttu-id="509ec-223">컨트롤러 별로 다음 설정을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-223">You can override the following settings on a per-controller basis:</span></span>

- <span data-ttu-id="509ec-224">미디어 유형 포맷터</span><span class="sxs-lookup"><span data-stu-id="509ec-224">Media-type formatters</span></span>
- <span data-ttu-id="509ec-225">매개 변수 바인딩 규칙</span><span class="sxs-lookup"><span data-stu-id="509ec-225">Parameter binding rules</span></span>
- <span data-ttu-id="509ec-226">Services</span><span class="sxs-lookup"><span data-stu-id="509ec-226">Services</span></span>

<span data-ttu-id="509ec-227">이렇게 하려면 **IControllerConfiguration** 인터페이스를 구현 하는 사용자 지정 특성을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-227">To do so, define a custom attribute that implements the **IControllerConfiguration** interface.</span></span> <span data-ttu-id="509ec-228">그런 다음 컨트롤러에 특성을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-228">Then apply the attribute to the controller.</span></span>

<span data-ttu-id="509ec-229">다음 예에서는 기본 미디어 유형 포맷터를 사용자 지정 포맷터로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-229">The following example replaces the default media-type formatters with a custom formatter.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="509ec-230">**IControllerConfiguration** 메서드는 두 개의 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-230">The **IControllerConfiguration.Initialize** method takes two parameters:</span></span>

- <span data-ttu-id="509ec-231">**Httpcontrollersettings** 개체</span><span class="sxs-lookup"><span data-stu-id="509ec-231">An **HttpControllerSettings** object</span></span>
- <span data-ttu-id="509ec-232">**Httpcontrollerdescriptor** 개체</span><span class="sxs-lookup"><span data-stu-id="509ec-232">An **HttpControllerDescriptor** object</span></span>

<span data-ttu-id="509ec-233">**Httpcontrollerdescriptor** 에는 컨트롤러에 대 한 설명이 포함 되어 있으며,이를 통해 정보를 확인할 수 있습니다 (예를 들어 두 컨트롤러를 구분 하는).</span><span class="sxs-lookup"><span data-stu-id="509ec-233">The **HttpControllerDescriptor** contains a description of the controller, which you can examine for informational purposes (say, to distinguish between two controllers).</span></span>

<span data-ttu-id="509ec-234">**Httpcontrollersettings** 개체를 사용 하 여 컨트롤러를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-234">Use the **HttpControllerSettings** object to configure the controller.</span></span> <span data-ttu-id="509ec-235">이 개체에는 컨트롤러 단위로 재정의할 수 있는 구성 매개 변수의 하위 집합이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-235">This object contains the subset of configuration parameters that you can override on a per-controller basis.</span></span> <span data-ttu-id="509ec-236">변경 하지 않는 설정은 기본적으로 전역 **Httpconfiguration** 개체로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="509ec-236">Any settings that you don't change default to the global **HttpConfiguration** object.</span></span>
