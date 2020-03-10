---
uid: web-api/overview/advanced/calling-a-web-api-from-a-net-client
title: .NET 클라이언트에서 Web API 호출 (C#)-ASP.NET 4.x
author: MikeWasson
description: 이 자습서에서는 .NET 4.x 응용 프로그램에서 web API를 호출 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 11/24/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/advanced/calling-a-web-api-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: ab3ba71839123e848dffaa59871f9dac8c1a88d0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504959"
---
# <a name="call-a-web-api-from-a-net-client-c"></a><span data-ttu-id="b1e3f-103">.NET 클라이언트에서 Web API 호출 (C#)</span><span class="sxs-lookup"><span data-stu-id="b1e3f-103">Call a Web API From a .NET Client (C#)</span></span>

<span data-ttu-id="b1e3f-104">만든 사람 [Mike Wasson](https://github.com/MikeWasson) And [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="b1e3f-104">by [Mike Wasson](https://github.com/MikeWasson) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="b1e3f-105">[완료 된 프로젝트를 다운로드](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample)합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-105">[Download Completed Project](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample).</span></span> <span data-ttu-id="b1e3f-106">[지침을 다운로드하세요](/aspnet/core/tutorials/#how-to-download-a-sample).</span><span class="sxs-lookup"><span data-stu-id="b1e3f-106">[Download instructions](/aspnet/core/tutorials/#how-to-download-a-sample).</span></span> 

<span data-ttu-id="b1e3f-107">이 자습서에서는 .NET 응용 프로그램에서 웹 API를 호출 하는 방법을 보여 [줍니다.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="b1e3f-107">This tutorial shows how to call a web API from a .NET application, using [System.Net.Http.HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span></span>

<span data-ttu-id="b1e3f-108">이 자습서에서는 다음 web API를 사용 하는 클라이언트 앱이 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-108">In this tutorial, a client app is written that consumes the following web API:</span></span>

| <span data-ttu-id="b1e3f-109">작업</span><span class="sxs-lookup"><span data-stu-id="b1e3f-109">Action</span></span> | <span data-ttu-id="b1e3f-110">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="b1e3f-110">HTTP method</span></span> | <span data-ttu-id="b1e3f-111">상대 URI</span><span class="sxs-lookup"><span data-stu-id="b1e3f-111">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b1e3f-112">ID로 제품 가져오기</span><span class="sxs-lookup"><span data-stu-id="b1e3f-112">Get a product by ID</span></span> | <span data-ttu-id="b1e3f-113">GET</span><span class="sxs-lookup"><span data-stu-id="b1e3f-113">GET</span></span> | <span data-ttu-id="b1e3f-114">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="b1e3f-114">/api/products/*id*</span></span> |
| <span data-ttu-id="b1e3f-115">새 제품 만들기</span><span class="sxs-lookup"><span data-stu-id="b1e3f-115">Create a new product</span></span> | <span data-ttu-id="b1e3f-116">POST</span><span class="sxs-lookup"><span data-stu-id="b1e3f-116">POST</span></span> | <span data-ttu-id="b1e3f-117">/api/제품</span><span class="sxs-lookup"><span data-stu-id="b1e3f-117">/api/products</span></span> |
| <span data-ttu-id="b1e3f-118">제품 업데이트</span><span class="sxs-lookup"><span data-stu-id="b1e3f-118">Update a product</span></span> | <span data-ttu-id="b1e3f-119">PUT</span><span class="sxs-lookup"><span data-stu-id="b1e3f-119">PUT</span></span> | <span data-ttu-id="b1e3f-120">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="b1e3f-120">/api/products/*id*</span></span> |
| <span data-ttu-id="b1e3f-121">제품 삭제</span><span class="sxs-lookup"><span data-stu-id="b1e3f-121">Delete a product</span></span> | <span data-ttu-id="b1e3f-122">Delete</span><span class="sxs-lookup"><span data-stu-id="b1e3f-122">DELETE</span></span> | <span data-ttu-id="b1e3f-123">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="b1e3f-123">/api/products/*id*</span></span> |

<span data-ttu-id="b1e3f-124">ASP.NET Web API를 사용 하 여이 API를 구현 하는 방법을 알아보려면 [CRUD 작업을 지 원하는 WEB API 만들기](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-124">To learn how to implement this API with ASP.NET Web API, see [Creating a Web API that Supports CRUD Operations](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span></span>

<span data-ttu-id="b1e3f-125">간단히 하기 위해이 자습서의 클라이언트 응용 프로그램은 Windows 콘솔 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-125">For simplicity, the client application in this tutorial is a Windows console application.</span></span> <span data-ttu-id="b1e3f-126">**Httpclient** 는 Windows Phone 및 Windows 스토어 앱 에서도 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-126">**HttpClient** is also supported for Windows Phone and Windows Store apps.</span></span> <span data-ttu-id="b1e3f-127">자세한 내용은 [이식 가능한 라이브러리를 사용 하 여 여러 플랫폼에 대 한 WEB API 클라이언트 코드 작성](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-127">For more information, see [Writing Web API Client Code for Multiple Platforms Using Portable Libraries](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span></span>

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a><span data-ttu-id="b1e3f-128">콘솔 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="b1e3f-128">Create the Console Application</span></span>

<span data-ttu-id="b1e3f-129">Visual Studio에서 **Httpclientsample** 이라는 새 Windows 콘솔 앱을 만들고 다음 코드를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-129">In Visual Studio, create a new Windows console app named **HttpClientSample** and paste in the following code:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

<span data-ttu-id="b1e3f-130">위의 코드는 전체 클라이언트 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-130">The preceding code is the complete client app.</span></span>

<span data-ttu-id="b1e3f-131">`RunAsync` 실행 되 고 작업이 완료 될 때까지 차단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-131">`RunAsync` runs and blocks until it completes.</span></span> <span data-ttu-id="b1e3f-132">대부분의 **Httpclient** 메서드는 네트워크 i/o를 수행 하기 때문에 비동기입니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-132">Most **HttpClient** methods are async, because they perform network I/O.</span></span> <span data-ttu-id="b1e3f-133">모든 비동기 작업은 `RunAsync`내에서 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-133">All of the async tasks are done inside `RunAsync`.</span></span> <span data-ttu-id="b1e3f-134">일반적으로 앱은 주 스레드를 차단 하지 않지만이 앱은 모든 상호 작용을 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-134">Normally an app doesn't block the main thread, but this app doesn't allow any interaction.</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a><span data-ttu-id="b1e3f-135">Web API 클라이언트 라이브러리를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-135">Install the Web API Client Libraries</span></span>

<span data-ttu-id="b1e3f-136">NuGet 패키지 관리자를 사용 하 여 Web API 클라이언트 라이브러리 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-136">Use NuGet Package Manager to install the Web API Client Libraries package.</span></span>

<span data-ttu-id="b1e3f-137">**도구** 메뉴에서 **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-137">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="b1e3f-138">패키지 관리자 콘솔 (PMC)에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-138">In the Package Manager Console (PMC), type the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.Client`

<span data-ttu-id="b1e3f-139">이전 명령은 다음 NuGet 패키지를 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-139">The preceding command adds the following NuGet packages to the project:</span></span>

* <span data-ttu-id="b1e3f-140">Microsoft.AspNet.WebApi.Client</span><span class="sxs-lookup"><span data-stu-id="b1e3f-140">Microsoft.AspNet.WebApi.Client</span></span>
* <span data-ttu-id="b1e3f-141">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="b1e3f-141">Newtonsoft.Json</span></span>

<span data-ttu-id="b1e3f-142">Netwonsoft (Json.NET 라고도 함)는 .NET 용으로 널리 사용 되는 고성능 JSON 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-142">Netwonsoft.Json (also known as Json.NET) is a popular high-performance JSON framework for .NET.</span></span>

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a><span data-ttu-id="b1e3f-143">모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="b1e3f-143">Add a Model Class</span></span>

<span data-ttu-id="b1e3f-144">`Product` 클래스를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-144">Examine the `Product` class:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

<span data-ttu-id="b1e3f-145">이 클래스는 web API에서 사용 하는 데이터 모델과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-145">This class matches the data model used by the web API.</span></span> <span data-ttu-id="b1e3f-146">앱은 **Httpclient** 를 사용 하 여 HTTP 응답에서 `Product` 인스턴스를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-146">An app can use **HttpClient** to read a `Product` instance from an HTTP response.</span></span> <span data-ttu-id="b1e3f-147">앱은 deserialization 코드를 작성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-147">The app doesn't have to write any deserialization code.</span></span>

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a><span data-ttu-id="b1e3f-148">HttpClient 만들기 및 초기화</span><span class="sxs-lookup"><span data-stu-id="b1e3f-148">Create and Initialize HttpClient</span></span>

<span data-ttu-id="b1e3f-149">정적 **Httpclient** 속성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-149">Examine the static **HttpClient** property:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

<span data-ttu-id="b1e3f-150">**Httpclient** 는 한 번 인스턴스화되어 응용 프로그램의 수명 내내 다시 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-150">**HttpClient** is intended to be instantiated once and reused throughout the life of an application.</span></span> <span data-ttu-id="b1e3f-151">다음 조건에 따라 **Socketexception** 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-151">The following conditions can result in **SocketException** errors:</span></span>

* <span data-ttu-id="b1e3f-152">요청당 새 **Httpclient** 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-152">Creating a new **HttpClient** instance per request.</span></span>
* <span data-ttu-id="b1e3f-153">부하가 높은 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-153">Server under heavy load.</span></span>

<span data-ttu-id="b1e3f-154">요청당 새 **Httpclient** 인스턴스를 만들면 사용 가능한 소켓이 고갈 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-154">Creating a new **HttpClient** instance per request can exhaust the available sockets.</span></span>

<span data-ttu-id="b1e3f-155">다음 코드는 **Httpclient** 인스턴스를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-155">The following code initializes the **HttpClient** instance:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

<span data-ttu-id="b1e3f-156">위의 코드는:</span><span class="sxs-lookup"><span data-stu-id="b1e3f-156">The preceding code:</span></span>

* <span data-ttu-id="b1e3f-157">HTTP 요청에 대 한 기본 URI를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-157">Sets the base URI for HTTP requests.</span></span> <span data-ttu-id="b1e3f-158">서버 앱에서 사용 되는 포트로 포트 번호를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-158">Change the port number to the port used in the server app.</span></span> <span data-ttu-id="b1e3f-159">서버 앱에 대 한 포트를 사용 하지 않으면 앱이 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-159">The app won't work unless port for the server app is used.</span></span>
* <span data-ttu-id="b1e3f-160">Accept 헤더를 "application/json"으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-160">Sets the Accept header to "application/json".</span></span> <span data-ttu-id="b1e3f-161">이 헤더를 설정 하면 서버에서 JSON 형식으로 데이터를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-161">Setting this header tells the server to send data in JSON format.</span></span>

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a><span data-ttu-id="b1e3f-162">리소스를 검색 하기 위해 GET 요청 보내기</span><span class="sxs-lookup"><span data-stu-id="b1e3f-162">Send a GET request to retrieve a resource</span></span>

<span data-ttu-id="b1e3f-163">다음 코드는 제품에 대 한 GET 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-163">The following code sends a GET request for a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

<span data-ttu-id="b1e3f-164">**Getasync** 메서드는 HTTP GET 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-164">The **GetAsync** method sends the HTTP GET request.</span></span> <span data-ttu-id="b1e3f-165">메서드가 완료 되 면 HTTP 응답을 포함 하는 **HttpResponseMessage** 를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-165">When the method completes, it returns an **HttpResponseMessage** that contains the HTTP response.</span></span> <span data-ttu-id="b1e3f-166">응답의 상태 코드가 성공 코드 이면 응답 본문은 제품의 JSON 표현을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-166">If the status code in the response is a success code, the response body contains the JSON representation of a product.</span></span> <span data-ttu-id="b1e3f-167">**Readasasync** 를 호출 하 여 JSON 페이로드를 `Product` 인스턴스로 deserialize 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-167">Call **ReadAsAsync** to deserialize the JSON payload to a `Product` instance.</span></span> <span data-ttu-id="b1e3f-168">응답 본문은 임의로 클 수 있으므로 **Readasasync** 메서드는 비동기입니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-168">The **ReadAsAsync** method is asynchronous because the response body can be arbitrarily large.</span></span>

<span data-ttu-id="b1e3f-169">HTTP 응답에 오류 코드가 포함 되어 있으면 **Httpclient** 는 예외를 throw 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-169">**HttpClient** does not throw an exception when the HTTP response contains an error code.</span></span> <span data-ttu-id="b1e3f-170">대신 **.issuccessstatuscode** 속성은 상태가 오류 코드 이면 **false** 입니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-170">Instead, the **IsSuccessStatusCode** property is **false** if the status is an error code.</span></span> <span data-ttu-id="b1e3f-171">HTTP 오류 코드를 예외로 처리 하는 것을 선호 하는 경우 응답 개체에서 [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) 를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-171">If you prefer to treat HTTP error codes as exceptions, call [HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) on the response object.</span></span> <span data-ttu-id="b1e3f-172">상태 코드가 200 299&ndash;`EnsureSuccessStatusCode` 범위를 벗어나면 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-172">`EnsureSuccessStatusCode` throws an exception if the status code falls outside the range 200&ndash;299.</span></span> <span data-ttu-id="b1e3f-173">요청 시간이 초과 되는 경우와 같이 **Httpclient** 는 다른 이유로 인해 예외를 throw 할 수 있습니다 &mdash;.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-173">Note that **HttpClient** can throw exceptions for other reasons &mdash; for example, if the request times out.</span></span>

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a><span data-ttu-id="b1e3f-174">Deserialize 할 미디어 형식 포맷터</span><span class="sxs-lookup"><span data-stu-id="b1e3f-174">Media-Type Formatters to Deserialize</span></span>

<span data-ttu-id="b1e3f-175">**Readasasync** 가 매개 변수 없이 호출 되는 경우 기본 *미디어 포맷터* 집합을 사용 하 여 응답 본문을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-175">When **ReadAsAsync** is called with no parameters, it uses a default set of *media formatters* to read the response body.</span></span> <span data-ttu-id="b1e3f-176">기본 포맷터는 JSON, XML 및 폼 url로 인코딩된 데이터를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-176">The default formatters support JSON, XML, and Form-url-encoded data.</span></span>

<span data-ttu-id="b1e3f-177">기본 포맷터를 사용 하는 대신, **Readasasync** 메서드에 포맷터 목록을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-177">Instead of using the default formatters, you can provide a list of formatters to the **ReadAsAsync** method.</span></span>  <span data-ttu-id="b1e3f-178">포맷터 목록을 사용 하면 사용자 지정 미디어 형식 포맷터가 있는 경우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-178">Using a list of formatters is useful if you have a custom media-type formatter:</span></span>

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

<span data-ttu-id="b1e3f-179">자세한 내용은 [ASP.NET Web API 2의 미디어 포맷터](../formats-and-model-binding/media-formatters.md) (영문)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-179">For more information, see [Media Formatters in ASP.NET Web API 2](../formats-and-model-binding/media-formatters.md)</span></span>

## <a name="sending-a-post-request-to-create-a-resource"></a><span data-ttu-id="b1e3f-180">리소스를 만들기 위한 POST 요청 보내기</span><span class="sxs-lookup"><span data-stu-id="b1e3f-180">Sending a POST Request to Create a Resource</span></span>

<span data-ttu-id="b1e3f-181">다음 코드는 `Product` 인스턴스를 포함 하는 POST 요청을 JSON 형식으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-181">The following code sends a POST request that contains a `Product` instance in JSON format:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

<span data-ttu-id="b1e3f-182">**PostAsJsonAsync** 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-182">The **PostAsJsonAsync** method:</span></span>

* <span data-ttu-id="b1e3f-183">개체를 JSON으로 serialize 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-183">Serializes an object to JSON.</span></span>
* <span data-ttu-id="b1e3f-184">POST 요청에서 JSON 페이로드를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-184">Sends the JSON payload in a POST request.</span></span>

<span data-ttu-id="b1e3f-185">요청이 성공 하면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-185">If the request succeeds:</span></span>

* <span data-ttu-id="b1e3f-186">201 (Created) 응답을 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-186">It should return a 201 (Created) response.</span></span>
* <span data-ttu-id="b1e3f-187">응답에는 Location 헤더에 생성 된 리소스의 URL이 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-187">The response should include the URL of the created resources in the Location header.</span></span>

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a><span data-ttu-id="b1e3f-188">리소스를 업데이트 하는 PUT 요청 보내기</span><span class="sxs-lookup"><span data-stu-id="b1e3f-188">Sending a PUT Request to Update a Resource</span></span>

<span data-ttu-id="b1e3f-189">다음 코드는 제품을 업데이트 하는 PUT 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-189">The following code sends a PUT request to update a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

<span data-ttu-id="b1e3f-190">**PutAsJsonAsync** 메서드는 POST 대신 PUT 요청을 전송 한다는 점을 제외 하 고는 **PostAsJsonAsync**와 유사 하 게 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-190">The **PutAsJsonAsync** method works like **PostAsJsonAsync**, except that it sends a PUT request instead of POST.</span></span>

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a><span data-ttu-id="b1e3f-191">리소스를 삭제 하는 삭제 요청 보내기</span><span class="sxs-lookup"><span data-stu-id="b1e3f-191">Sending a DELETE Request to Delete a Resource</span></span>

<span data-ttu-id="b1e3f-192">다음 코드는 제품을 삭제 하는 삭제 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-192">The following code sends a DELETE request to delete a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

<span data-ttu-id="b1e3f-193">GET과 마찬가지로 DELETE 요청에는 요청 본문이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-193">Like GET, a DELETE request does not have a request body.</span></span> <span data-ttu-id="b1e3f-194">DELETE를 사용 하 여 JSON 또는 XML 형식을 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-194">You don't need to specify JSON or XML format with DELETE.</span></span>

## <a name="test-the-sample"></a><span data-ttu-id="b1e3f-195">샘플 테스트</span><span class="sxs-lookup"><span data-stu-id="b1e3f-195">Test the sample</span></span>

<span data-ttu-id="b1e3f-196">클라이언트 앱을 테스트 하려면:</span><span class="sxs-lookup"><span data-stu-id="b1e3f-196">To test the client app:</span></span>

1. <span data-ttu-id="b1e3f-197">서버 앱을 [다운로드](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) 하 고 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-197">[Download](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) and run the server app.</span></span> <span data-ttu-id="b1e3f-198">[지침을 다운로드하세요](/aspnet/core/#how-to-download-a-sample).</span><span class="sxs-lookup"><span data-stu-id="b1e3f-198">[Download instructions](/aspnet/core/#how-to-download-a-sample).</span></span> <span data-ttu-id="b1e3f-199">서버 앱이 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-199">Verify the server app is working.</span></span> <span data-ttu-id="b1e3f-200">예를 들어 `http://localhost:64195/api/products`는 제품 목록을 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-200">For example, `http://localhost:64195/api/products` should return a list of products.</span></span>
2. <span data-ttu-id="b1e3f-201">HTTP 요청에 대 한 기본 URI를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-201">Set the base URI for HTTP requests.</span></span> <span data-ttu-id="b1e3f-202">서버 앱에서 사용 되는 포트로 포트 번호를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-202">Change the port number to the port used in the server app.</span></span>
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. <span data-ttu-id="b1e3f-203">클라이언트 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-203">Run the client app.</span></span> <span data-ttu-id="b1e3f-204">다음 출력이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1e3f-204">The following output is produced:</span></span>

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```
