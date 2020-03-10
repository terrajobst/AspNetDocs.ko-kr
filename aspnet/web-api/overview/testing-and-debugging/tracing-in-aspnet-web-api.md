---
uid: web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
title: ASP.NET Web API 2의 추적 | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API에서 추적을 사용 하도록 설정 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 66a837e9-600b-4b72-97a9-19804231c64a
msc.legacyurl: /web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: a01acb649556d06ab9828ceab0fcbdf363bbc0d1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484343"
---
# <a name="tracing-in-aspnet-web-api-2"></a><span data-ttu-id="2d25d-103">ASP.NET Web API 2에서 추적</span><span class="sxs-lookup"><span data-stu-id="2d25d-103">Tracing in ASP.NET Web API 2</span></span>

<span data-ttu-id="2d25d-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2d25d-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="2d25d-105">웹 기반 응용 프로그램을 디버깅 하려는 경우 올바른 추적 로그 집합을 대체 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-105">When you are trying to debug a web-based application, there is no substitute for a good set of trace logs.</span></span> <span data-ttu-id="2d25d-106">이 자습서에서는 ASP.NET Web API에서 추적을 사용 하도록 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-106">This tutorial shows how to enable tracing in ASP.NET Web API.</span></span> <span data-ttu-id="2d25d-107">이 기능을 사용 하 여 웹 API 프레임 워크가 컨트롤러를 호출 하기 전과 후에 수행 하는 작업을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-107">You can use this feature to trace what the Web API framework does before and after it invokes your controller.</span></span> <span data-ttu-id="2d25d-108">또한 사용자 고유의 코드를 추적 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-108">You can also use it to trace your own code.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="2d25d-109">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="2d25d-109">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="2d25d-110">[Visual studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) (visual studio 2015 에서도 작동)</span><span class="sxs-lookup"><span data-stu-id="2d25d-110">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) (also works with Visual Studio 2015)</span></span>
> - <span data-ttu-id="2d25d-111">Web API 2</span><span class="sxs-lookup"><span data-stu-id="2d25d-111">Web API 2</span></span>
> - [<span data-ttu-id="2d25d-112">WebApi. 추적</span><span class="sxs-lookup"><span data-stu-id="2d25d-112">Microsoft.AspNet.WebApi.Tracing</span></span>](http://www.nuget.org/packages/Microsoft.AspNet.WebApi.Tracing)

## <a name="enable-systemdiagnostics-tracing-in-web-api"></a><span data-ttu-id="2d25d-113">Web API에서 시스템 진단 추적을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="2d25d-113">Enable System.Diagnostics Tracing in Web API</span></span>

<span data-ttu-id="2d25d-114">먼저 새 ASP.NET 웹 응용 프로그램 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-114">First, we'll create a new ASP.NET Web Application project.</span></span> <span data-ttu-id="2d25d-115">Visual Studio의 **파일** 메뉴에서 **새로 만들기** > **프로젝트**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-115">In Visual Studio, from the **File** menu, select **New** > **Project**.</span></span> <span data-ttu-id="2d25d-116">**템플릿**, **웹**에서 **ASP.NET 웹 응용 프로그램**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-116">Under **Templates**, **Web**, select **ASP.NET Web Application**.</span></span>

[![](tracing-in-aspnet-web-api/_static/image2.png)](tracing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="2d25d-117">웹 API 프로젝트 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-117">Choose the Web API project template.</span></span>

[![](tracing-in-aspnet-web-api/_static/image4.png)](tracing-in-aspnet-web-api/_static/image3.png)

<span data-ttu-id="2d25d-118">**도구** 메뉴에서 **NuGet 패키지 관리자**, **패키지 관리 콘솔**을 차례로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-118">From the **Tools** menu, select **NuGet Package Manager**, then **Package Manage Console**.</span></span>

<span data-ttu-id="2d25d-119">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-119">In the Package Manager Console window, type the following commands.</span></span>

[!code-console[Main](tracing-in-aspnet-web-api/samples/sample1.cmd)]

<span data-ttu-id="2d25d-120">첫 번째 명령은 최신 웹 API 추적 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-120">The first command installs the latest Web API tracing package.</span></span> <span data-ttu-id="2d25d-121">또한 핵심 웹 API 패키지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-121">It also updates the core Web API packages.</span></span> <span data-ttu-id="2d25d-122">두 번째 명령은 WebHost 패키지를 최신 버전으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-122">The second command updates the WebApi.WebHost package to the latest version.</span></span>

> [!NOTE]
> <span data-ttu-id="2d25d-123">웹 API의 특정 버전을 대상으로 지정 하려는 경우 추적 패키지를 설치할 때-Version 플래그를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-123">If you want to target a specific version of Web API, use the -Version flag when you install the tracing package.</span></span>

<span data-ttu-id="2d25d-124">앱\_시작 폴더에서 WebApiConfig.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-124">Open the file WebApiConfig.cs in the App\_Start folder.</span></span> <span data-ttu-id="2d25d-125">**Register** 메서드에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-125">Add the following code to the **Register** method.</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample2.cs?highlight=6)]

<span data-ttu-id="2d25d-126">이 코드는 Web API 파이프라인에 [SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx) 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-126">This code adds the [SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx) class to the Web API pipeline.</span></span> <span data-ttu-id="2d25d-127">**SystemDiagnosticsTraceWriter** 클래스는 추적을 [시스템 진단](https://msdn.microsoft.com/library/system.diagnostics.trace)에 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-127">The **SystemDiagnosticsTraceWriter** class writes traces to [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace).</span></span>

<span data-ttu-id="2d25d-128">추적을 보려면 디버거에서 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-128">To see the traces, run the application in the debugger.</span></span> <span data-ttu-id="2d25d-129">브라우저에서 `/api/values`으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-129">In the browser, navigate to `/api/values`.</span></span>

![](tracing-in-aspnet-web-api/_static/image5.png)

<span data-ttu-id="2d25d-130">Trace 문은 Visual Studio의 출력 창에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-130">The trace statements are written to the Output window in Visual Studio.</span></span> <span data-ttu-id="2d25d-131">( **보기** 메뉴에서 **출력**을 선택 합니다.)</span><span class="sxs-lookup"><span data-stu-id="2d25d-131">(From the **View** menu, select **Output**).</span></span>

[![](tracing-in-aspnet-web-api/_static/image7.png)](tracing-in-aspnet-web-api/_static/image6.png)

<span data-ttu-id="2d25d-132">**SystemDiagnosticsTraceWriter** 는 추적을 **시스템 진단**에 쓰도록 하므로 추가 추적 수신기를 등록할 수 있습니다. 예를 들어 로그 파일에 추적을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-132">Because **SystemDiagnosticsTraceWriter** writes traces to **System.Diagnostics.Trace**, you can register additional trace listeners; for example, to write traces to a log file.</span></span> <span data-ttu-id="2d25d-133">추적 작성자에 대 한 자세한 내용은 MSDN의 [추적 수신기](https://msdn.microsoft.com/library/4y5y10s7.aspx) 항목을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2d25d-133">For more information about trace writers, see the [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx) topic on MSDN.</span></span>

### <a name="configuring-systemdiagnosticstracewriter"></a><span data-ttu-id="2d25d-134">SystemDiagnosticsTraceWriter 구성</span><span class="sxs-lookup"><span data-stu-id="2d25d-134">Configuring SystemDiagnosticsTraceWriter</span></span>

<span data-ttu-id="2d25d-135">다음 코드에서는 추적 작성기를 구성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-135">The following code shows how to configure the trace writer.</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="2d25d-136">다음 두 가지 설정을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-136">There are two settings that you can control:</span></span>

- <span data-ttu-id="2d25d-137">IsVerbose: false 인 경우 각 추적에 최소한의 정보가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-137">IsVerbose: If false, each trace contains minimal information.</span></span> <span data-ttu-id="2d25d-138">True 이면 추적에 추가 정보가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-138">If true, traces include more information.</span></span>
- <span data-ttu-id="2d25d-139">이상 수준: 최소 추적 수준을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-139">MinimumLevel: Sets the minimum trace level.</span></span> <span data-ttu-id="2d25d-140">추적 수준이 순서 대로 디버그, 정보, 경고, 오류 및 치명적입니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-140">Trace levels, in order, are Debug, Info, Warn, Error, and Fatal.</span></span>

## <a name="adding-traces-to-your-web-api-application"></a><span data-ttu-id="2d25d-141">웹 API 응용 프로그램에 추적 추가</span><span class="sxs-lookup"><span data-stu-id="2d25d-141">Adding Traces to Your Web API Application</span></span>

<span data-ttu-id="2d25d-142">추적 기록기를 추가 하면 웹 API 파이프라인에서 만든 추적에 즉시 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-142">Adding a trace writer gives you immediate access to the traces created by the Web API pipeline.</span></span> <span data-ttu-id="2d25d-143">또한 추적 작성기를 사용 하 여 사용자 고유의 코드를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-143">You can also use the trace writer to trace your own code:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="2d25d-144">추적 작성기를 가져오려면 **Httpcecetrraraa**를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-144">To get the trace writer, call **HttpConfiguration.Services.GetTraceWriter**.</span></span> <span data-ttu-id="2d25d-145">컨트롤러에서이 메서드는 **ApiController** 속성을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-145">From a controller, this method is accessible through the **ApiController.Configuration** property.</span></span>

<span data-ttu-id="2d25d-146">추적을 작성 하려면 **ITraceWriter** 메서드를 직접 호출할 수 있지만 [ITraceWriterExtensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx) 클래스는 보다 친숙 한 일부 확장 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-146">To write a trace, you can call the **ITraceWriter.Trace** method directly, but the [ITraceWriterExtensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx) class defines some extension methods that are more friendly.</span></span> <span data-ttu-id="2d25d-147">예를 들어 위에 표시 된 **정보** 메서드는 추적 수준 **정보**를 사용 하 여 추적을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-147">For example, the **Info** method shown above creates a trace with trace level **Info**.</span></span>

## <a name="web-api-tracing-infrastructure"></a><span data-ttu-id="2d25d-148">웹 API 추적 인프라</span><span class="sxs-lookup"><span data-stu-id="2d25d-148">Web API Tracing Infrastructure</span></span>

<span data-ttu-id="2d25d-149">이 섹션에서는 Web API에 대 한 사용자 지정 추적 기록기를 작성 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-149">This section describes how to write a custom trace writer for Web API.</span></span>

<span data-ttu-id="2d25d-150">WebApi 패키지는 Web API의 보다 일반적인 추적 인프라 위에 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-150">The Microsoft.AspNet.WebApi.Tracing package is built on top of a more general tracing infrastructure in Web API.</span></span> <span data-ttu-id="2d25d-151">WebApi를 사용 하는 대신 [Nlog](http://nlog-project.org/) 또는 [log4net](http://logging.apache.org/log4net/)와 같은 다른 추적/로깅 라이브러리를 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-151">Instead of using Microsoft.AspNet.WebApi.Tracing, you can also plug in some other tracing/logging library, such as [NLog](http://nlog-project.org/) or [log4net](http://logging.apache.org/log4net/).</span></span>

<span data-ttu-id="2d25d-152">추적을 수집 하려면 **ITraceWriter** 인터페이스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-152">To collect traces, implement the **ITraceWriter** interface.</span></span> <span data-ttu-id="2d25d-153">다음은 간단한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-153">Here is a simple example:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="2d25d-154">**ITraceWriter** 메서드는 추적을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-154">The **ITraceWriter.Trace** method creates a trace.</span></span> <span data-ttu-id="2d25d-155">호출자는 범주 및 추적 수준을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-155">The caller specifies a category and trace level.</span></span> <span data-ttu-id="2d25d-156">범주는 임의의 사용자 정의 문자열일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-156">The category can be any user-defined string.</span></span> <span data-ttu-id="2d25d-157">**추적** 을 구현 하는 경우 다음을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-157">Your implementation of **Trace** should do the following:</span></span>

1. <span data-ttu-id="2d25d-158">새 **TraceRecord**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-158">Create a new **TraceRecord**.</span></span> <span data-ttu-id="2d25d-159">표시 된 것 처럼 요청, 범주 및 추적 수준으로 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-159">Initialize it with the request, category, and trace level, as shown.</span></span> <span data-ttu-id="2d25d-160">이러한 값은 호출자가 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-160">These values are provided by the caller.</span></span>
2. <span data-ttu-id="2d25d-161">*Traceaction* 대리자를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-161">Invoke the *traceAction* delegate.</span></span> <span data-ttu-id="2d25d-162">이 대리자 내에서 호출자는 **TraceRecord**의 나머지 부분을 채워야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-162">Inside this delegate, the caller is expected to fill in the rest of the **TraceRecord**.</span></span>
3. <span data-ttu-id="2d25d-163">원하는 로깅 기술을 사용 하 여 **TraceRecord**를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-163">Write the **TraceRecord**, using any logging technique that you like.</span></span> <span data-ttu-id="2d25d-164">여기에 표시 된 예제는 단순히 **system.object**를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-164">The example shown here simply calls into **System.Diagnostics.Trace**.</span></span>

## <a name="setting-the-trace-writer"></a><span data-ttu-id="2d25d-165">추적 작성기 설정</span><span class="sxs-lookup"><span data-stu-id="2d25d-165">Setting the Trace Writer</span></span>

<span data-ttu-id="2d25d-166">추적을 사용 하도록 설정 하려면 **ITraceWriter** 구현을 사용 하도록 Web API를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-166">To enable tracing, you must configure Web API to use your **ITraceWriter** implementation.</span></span> <span data-ttu-id="2d25d-167">다음 코드와 같이 **Httpconfiguration** 개체를 통해이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-167">You do this through the **HttpConfiguration** object, as shown in the following code:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="2d25d-168">하나의 추적 기록기만 활성화 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-168">Only one trace writer can be active.</span></span> <span data-ttu-id="2d25d-169">기본적으로 Web API는 아무 작업도 수행 하지 않는 &quot;op&quot; 추적 프로그램을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-169">By default, Web API sets a &quot;no-op&quot; tracer that does nothing.</span></span> <span data-ttu-id="2d25d-170">추적 코드가 추적을 작성 하기 전에 추적 기록기가 **null** 인지 여부를 확인할 필요가 없도록 &quot;op&quot; 추적 기능이 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-170">(The &quot;no-op&quot; tracer exists so that tracing code does not have to check whether the trace writer is **null** before writing a trace.)</span></span>

## <a name="how-web-api-tracing-works"></a><span data-ttu-id="2d25d-171">Web API 추적 작동 방법</span><span class="sxs-lookup"><span data-stu-id="2d25d-171">How Web API Tracing Works</span></span>

<span data-ttu-id="2d25d-172">Web API의 추적은 *외관* 패턴을 사용 합니다. 추적을 사용 하는 경우 web API는 추적 호출을 수행 하는 클래스로 요청 파이프라인의 다양 한 부분을 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-172">Tracing in Web API uses a *facade* pattern: When tracing is enabled, Web API wraps various parts of the request pipeline with classes that perform trace calls.</span></span>

<span data-ttu-id="2d25d-173">예를 들어, 컨트롤러를 선택 하는 경우 파이프라인은 **IHttpControllerSelector** 인터페이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-173">For example, when selecting a controller, the pipeline uses the **IHttpControllerSelector** interface.</span></span> <span data-ttu-id="2d25d-174">추적을 사용 하는 경우 파이프라인은 **IHttpControllerSelector** 를 구현 하지만 실제 구현을 통해 호출 하는 클래스를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-174">With tracing enabled, the pipeline inserts a class that implements **IHttpControllerSelector** but calls through to the real implementation:</span></span>

![Web API 추적은 외관 패턴을 사용 합니다.](tracing-in-aspnet-web-api/_static/image8.png)

<span data-ttu-id="2d25d-176">이 디자인의 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-176">The benefits of this design include:</span></span>

- <span data-ttu-id="2d25d-177">추적 기록기를 추가 하지 않으면 추적 구성 요소가 인스턴스화되지 않으며 성능에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-177">If you do not add a trace writer, the tracing components are not instantiated and have no performance impact.</span></span>
- <span data-ttu-id="2d25d-178">**IHttpControllerSelector** 와 같은 기본 서비스를 사용자 지정 구현으로 대체 하는 경우 추적은 래퍼 개체에 의해 수행 되므로 추적에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-178">If you replace default services such as **IHttpControllerSelector** with your own custom implementation, tracing is not affected, because tracing is done by the wrapper object.</span></span>

<span data-ttu-id="2d25d-179">기본 **ITraceManager** 서비스를 대체 하 여 전체 Web API 추적 프레임 워크를 사용자 지정 프레임 워크로 대체할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-179">You can also replace the entire Web API trace framework with your own custom framework, by replacing the default **ITraceManager** service:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="2d25d-180">**ITraceManager** 를 구현 하 여 추적 시스템을 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-180">Implement **ITraceManager.Initialize** to initialize your tracing system.</span></span> <span data-ttu-id="2d25d-181">이는 Web API에 기본 제공 되는 모든 추적 코드를 포함 하 여 *전체* 추적 프레임 워크를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d25d-181">Be aware that this replaces the *entire* trace framework, including all of the tracing code that is built into Web API.</span></span>
