---
uid: web-api/overview/advanced/calling-a-web-api-from-a-net-client
title: .NET 클라이언트에서 Web API 호출 (C#)-ASP.NET 4.x
author: MikeWasson
description: 이 자습서에서는.NET 4.x 응용 프로그램에서 web API를 호출 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 11/24/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/advanced/calling-a-web-api-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 113600ca1e77ae9667465464da505478fc948c9b
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59421110"
---
# <a name="call-a-web-api-from-a-net-client-c"></a><span data-ttu-id="2f60c-103">.NET 클라이언트 (C#)에서 Web API 호출</span><span class="sxs-lookup"><span data-stu-id="2f60c-103">Call a Web API From a .NET Client (C#)</span></span>

<span data-ttu-id="2f60c-104">하 여 [Mike Wasson](https://github.com/MikeWasson) 고 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="2f60c-104">by [Mike Wasson](https://github.com/MikeWasson) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="2f60c-105">[완료 된 프로젝트 다운로드](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-105">[Download Completed Project](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample).</span></span> <span data-ttu-id="2f60c-106">[지침을 다운로드하세요](/aspnet/core/tutorials/#how-to-download-a-sample).</span><span class="sxs-lookup"><span data-stu-id="2f60c-106">[Download instructions](/aspnet/core/tutorials/#how-to-download-a-sample).</span></span> 

<span data-ttu-id="2f60c-107">이 자습서에서는.NET 응용 프로그램, web API를 호출 하는 방법을 보여 줍니다.를 사용 하 여 [System.Net.Http.HttpClient 합니다.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="2f60c-107">This tutorial shows how to call a web API from a .NET application, using [System.Net.Http.HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span></span>

<span data-ttu-id="2f60c-108">이 자습서에서는 다음 웹 API를 사용 하는 클라이언트 앱을 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-108">In this tutorial, a client app is written that consumes the following web API:</span></span>

| <span data-ttu-id="2f60c-109">작업</span><span class="sxs-lookup"><span data-stu-id="2f60c-109">Action</span></span> | <span data-ttu-id="2f60c-110">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="2f60c-110">HTTP method</span></span> | <span data-ttu-id="2f60c-111">상대 URI</span><span class="sxs-lookup"><span data-stu-id="2f60c-111">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2f60c-112">제품 ID 별로 가져오기</span><span class="sxs-lookup"><span data-stu-id="2f60c-112">Get a product by ID</span></span> | <span data-ttu-id="2f60c-113">가져오기</span><span class="sxs-lookup"><span data-stu-id="2f60c-113">GET</span></span> | <span data-ttu-id="2f60c-114">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="2f60c-114">/api/products/*id*</span></span> |
| <span data-ttu-id="2f60c-115">새 제품 만들기</span><span class="sxs-lookup"><span data-stu-id="2f60c-115">Create a new product</span></span> | <span data-ttu-id="2f60c-116">올리기</span><span class="sxs-lookup"><span data-stu-id="2f60c-116">POST</span></span> | <span data-ttu-id="2f60c-117">api 제품</span><span class="sxs-lookup"><span data-stu-id="2f60c-117">/api/products</span></span> |
| <span data-ttu-id="2f60c-118">제품 업데이트</span><span class="sxs-lookup"><span data-stu-id="2f60c-118">Update a product</span></span> | <span data-ttu-id="2f60c-119">PUT</span><span class="sxs-lookup"><span data-stu-id="2f60c-119">PUT</span></span> | <span data-ttu-id="2f60c-120">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="2f60c-120">/api/products/*id*</span></span> |
| <span data-ttu-id="2f60c-121">제품 삭제</span><span class="sxs-lookup"><span data-stu-id="2f60c-121">Delete a product</span></span> | <span data-ttu-id="2f60c-122">Delete</span><span class="sxs-lookup"><span data-stu-id="2f60c-122">DELETE</span></span> | <span data-ttu-id="2f60c-123">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="2f60c-123">/api/products/*id*</span></span> |

<span data-ttu-id="2f60c-124">참조를 ASP.NET Web API를 사용 하 여이 API를 구현 하는 방법을 알아보려면 [Web API에서는 CRUD 작업을 만드는](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-124">To learn how to implement this API with ASP.NET Web API, see [Creating a Web API that Supports CRUD Operations](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span></span>

<span data-ttu-id="2f60c-125">간단히 하기 위해이 자습서에서는 클라이언트 응용 프로그램은 Windows 콘솔 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-125">For simplicity, the client application in this tutorial is a Windows console application.</span></span> <span data-ttu-id="2f60c-126">**HttpClient** Windows Phone 및 Windows 스토어 앱도 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-126">**HttpClient** is also supported for Windows Phone and Windows Store apps.</span></span> <span data-ttu-id="2f60c-127">자세한 내용은 참조 하세요. [여러 플랫폼 이식 가능한 라이브러리 사용에 대 한 웹 API 클라이언트 코드 작성](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span><span class="sxs-lookup"><span data-stu-id="2f60c-127">For more information, see [Writing Web API Client Code for Multiple Platforms Using Portable Libraries](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span></span>

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a><span data-ttu-id="2f60c-128">콘솔 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="2f60c-128">Create the Console Application</span></span>

<span data-ttu-id="2f60c-129">Visual Studio에서 명명 된 새 Windows 콘솔 앱을 만듭니다 **HttpClientSample** 다음 코드에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-129">In Visual Studio, create a new Windows console app named **HttpClientSample** and paste in the following code:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

<span data-ttu-id="2f60c-130">위의 코드는 전체 클라이언트 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-130">The preceding code is the complete client app.</span></span>

`RunAsync` <span data-ttu-id="2f60c-131">실행 및 완료 될 때까지 차단 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-131">runs and blocks until it completes.</span></span> <span data-ttu-id="2f60c-132">대부분 **HttpClient** 메서드는 비동기, 네트워크 I/O를 수행 하는 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-132">Most **HttpClient** methods are async, because they perform network I/O.</span></span> <span data-ttu-id="2f60c-133">내부에서 수행 하는 비동기 작업을 모두 `RunAsync`입니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-133">All of the async tasks are done inside `RunAsync`.</span></span> <span data-ttu-id="2f60c-134">일반적으로 앱 주 스레드를 차단 하지 않습니다 하지만이 앱이 모든 상호 작용을 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-134">Normally an app doesn't block the main thread, but this app doesn't allow any interaction.</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a><span data-ttu-id="2f60c-135">웹 API 클라이언트 라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="2f60c-135">Install the Web API Client Libraries</span></span>

<span data-ttu-id="2f60c-136">NuGet 패키지 관리자를 사용 하 여 웹 API 클라이언트 라이브러리 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-136">Use NuGet Package Manager to install the Web API Client Libraries package.</span></span>

<span data-ttu-id="2f60c-137">**도구** 메뉴에서 **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-137">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="2f60c-138">에 콘솔 PMC (패키지 관리자), 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-138">In the Package Manager Console (PMC), type the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.Client`

<span data-ttu-id="2f60c-139">위의 명령은 프로젝트에 다음 NuGet 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-139">The preceding command adds the following NuGet packages to the project:</span></span>

* <span data-ttu-id="2f60c-140">Microsoft.AspNet.WebApi.Client</span><span class="sxs-lookup"><span data-stu-id="2f60c-140">Microsoft.AspNet.WebApi.Client</span></span>
* <span data-ttu-id="2f60c-141">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="2f60c-141">Newtonsoft.Json</span></span>

<span data-ttu-id="2f60c-142">Json.NET은.NET에 대 한 인기 있는 고성능 JSON 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-142">Json.NET is a popular high-performance JSON framework for .NET.</span></span>

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a><span data-ttu-id="2f60c-143">모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="2f60c-143">Add a Model Class</span></span>

<span data-ttu-id="2f60c-144">`Product` 클래스를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-144">Examine the `Product` class:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

<span data-ttu-id="2f60c-145">이 클래스는 웹 API에 의해 사용 되는 데이터 모델을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-145">This class matches the data model used by the web API.</span></span> <span data-ttu-id="2f60c-146">앱에서 사용할 수 있습니다 **HttpClient** 읽을 수는 `Product` HTTP 응답 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-146">An app can use **HttpClient** to read a `Product` instance from an HTTP response.</span></span> <span data-ttu-id="2f60c-147">앱은 deserialization 코드를 작성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-147">The app doesn't have to write any deserialization code.</span></span>

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a><span data-ttu-id="2f60c-148">만들기 및 HttpClient를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-148">Create and Initialize HttpClient</span></span>

<span data-ttu-id="2f60c-149">정적 검사 **HttpClient** 속성:</span><span class="sxs-lookup"><span data-stu-id="2f60c-149">Examine the static **HttpClient** property:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

<span data-ttu-id="2f60c-150">**HttpClient** 한 번 인스턴스화되면 되 고 응용 프로그램의 수명 내내 다시 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-150">**HttpClient** is intended to be instantiated once and reused throughout the life of an application.</span></span> <span data-ttu-id="2f60c-151">다음 조건이 발생할 수 있습니다 **SocketException** 오류:</span><span class="sxs-lookup"><span data-stu-id="2f60c-151">The following conditions can result in **SocketException** errors:</span></span>

* <span data-ttu-id="2f60c-152">새로 만들 **HttpClient** 요청당 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="2f60c-152">Creating a new **HttpClient** instance per request.</span></span>
* <span data-ttu-id="2f60c-153">부하가 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-153">Server under heavy load.</span></span>

<span data-ttu-id="2f60c-154">새로 만들 **HttpClient** 요청당 인스턴스는 사용 가능한 소켓 소모 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-154">Creating a new **HttpClient** instance per request can exhaust the available sockets.</span></span>

<span data-ttu-id="2f60c-155">다음 코드는 초기화 된 **HttpClient** 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="2f60c-155">The following code initializes the **HttpClient** instance:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

<span data-ttu-id="2f60c-156">위의 코드는:</span><span class="sxs-lookup"><span data-stu-id="2f60c-156">The preceding code:</span></span>

* <span data-ttu-id="2f60c-157">HTTP 요청에 대 한 기본 URI를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-157">Sets the base URI for HTTP requests.</span></span> <span data-ttu-id="2f60c-158">서버 앱에서 사용 되는 포트를 포트 번호를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-158">Change the port number to the port used in the server app.</span></span> <span data-ttu-id="2f60c-159">앱 서버 앱에 대 한 포트를 사용 하지 않으면 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-159">The app won't work unless port for the server app is used.</span></span>
* <span data-ttu-id="2f60c-160">Accept 헤더가 "application/json"으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-160">Sets the Accept header to "application/json".</span></span> <span data-ttu-id="2f60c-161">이 헤더를 설정 합니다. JSON 형식으로 데이터를 보내도록 서버에 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-161">Setting this header tells the server to send data in JSON format.</span></span>

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a><span data-ttu-id="2f60c-162">리소스를 검색에 GET 요청을 보냄</span><span class="sxs-lookup"><span data-stu-id="2f60c-162">Send a GET request to retrieve a resource</span></span>

<span data-ttu-id="2f60c-163">다음 코드는 제품에 대 한 GET 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-163">The following code sends a GET request for a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

<span data-ttu-id="2f60c-164">합니다 **GetAsync** 메서드는 HTTP GET 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-164">The **GetAsync** method sends the HTTP GET request.</span></span> <span data-ttu-id="2f60c-165">메서드가 완료 되 면 반환 된 **HttpResponseMessage** HTTP 응답을 포함 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-165">When the method completes, it returns an **HttpResponseMessage** that contains the HTTP response.</span></span> <span data-ttu-id="2f60c-166">응답에 상태 코드가 성공 코드 인 경우 응답 본문에는 제품의 JSON 표현을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-166">If the status code in the response is a success code, the response body contains the JSON representation of a product.</span></span> <span data-ttu-id="2f60c-167">호출 **ReadAsAsync** JSON 페이로드를 deserialize 하는 데는 `Product` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="2f60c-167">Call **ReadAsAsync** to deserialize the JSON payload to a `Product` instance.</span></span> <span data-ttu-id="2f60c-168">합니다 **ReadAsAsync** 메서드는 응답 본문은 임의로 큰 수 있기 때문에 비동기입니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-168">The **ReadAsAsync** method is asynchronous because the response body can be arbitrarily large.</span></span>

<span data-ttu-id="2f60c-169">**HttpClient** HTTP 응답 오류 코드를 포함 하는 경우 예외를 throw 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-169">**HttpClient** does not throw an exception when the HTTP response contains an error code.</span></span> <span data-ttu-id="2f60c-170">대신 합니다 **IsSuccessStatusCode** 속성은 **false** 상태가 오류 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-170">Instead, the **IsSuccessStatusCode** property is **false** if the status is an error code.</span></span> <span data-ttu-id="2f60c-171">HTTP 오류 코드를 예외로 처리 하는 것을 선호 하는 경우 호출 [HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) 응답 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-171">If you prefer to treat HTTP error codes as exceptions, call [HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) on the response object.</span></span> `EnsureSuccessStatusCode` <span data-ttu-id="2f60c-172">상태 코드 200 범위를 벗어나는 경우 예외를 throw&ndash;299 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-172">throws an exception if the status code falls outside the range 200&ndash;299.</span></span> <span data-ttu-id="2f60c-173">사실은 **HttpClient** 다른 이유로 예외를 throw 할 수 있습니다 &mdash; 예를 들어 요청 시간이 초과 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-173">Note that **HttpClient** can throw exceptions for other reasons &mdash; for example, if the request times out.</span></span>

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a><span data-ttu-id="2f60c-174">Deserialize 하는 미디어 유형 포맷터</span><span class="sxs-lookup"><span data-stu-id="2f60c-174">Media-Type Formatters to Deserialize</span></span>

<span data-ttu-id="2f60c-175">때 **ReadAsAsync** 라고 일련의 기본 매개 변수 없이 사용 *미디어 포맷터* 응답 본문을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-175">When **ReadAsAsync** is called with no parameters, it uses a default set of *media formatters* to read the response body.</span></span> <span data-ttu-id="2f60c-176">기본 포맷터는 JSON, XML 및 양식 url로 인코딩된 데이터를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-176">The default formatters support JSON, XML, and Form-url-encoded data.</span></span>

<span data-ttu-id="2f60c-177">기본 포맷터를 사용 하는 대신 하는 포맷터의 목록을 제공할 수 있습니다 합니다 **ReadAsAsync** 메서드.</span><span class="sxs-lookup"><span data-stu-id="2f60c-177">Instead of using the default formatters, you can provide a list of formatters to the **ReadAsAsync** method.</span></span>  <span data-ttu-id="2f60c-178">포맷터 목록을 사용 하 여는 사용자 지정 미디어 유형 포맷터를 해야 하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-178">Using a list of formatters is useful if you have a custom media-type formatter:</span></span>

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

<span data-ttu-id="2f60c-179">자세한 내용은 참조 하세요. [ASP.NET Web API 2의 미디어 포맷터](../formats-and-model-binding/media-formatters.md)</span><span class="sxs-lookup"><span data-stu-id="2f60c-179">For more information, see [Media Formatters in ASP.NET Web API 2](../formats-and-model-binding/media-formatters.md)</span></span>

## <a name="sending-a-post-request-to-create-a-resource"></a><span data-ttu-id="2f60c-180">리소스를 만드는 POST 요청</span><span class="sxs-lookup"><span data-stu-id="2f60c-180">Sending a POST Request to Create a Resource</span></span>

<span data-ttu-id="2f60c-181">다음 코드를 포함 하는 POST 요청이 전송 된 `Product` JSON 형식으로 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="2f60c-181">The following code sends a POST request that contains a `Product` instance in JSON format:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

<span data-ttu-id="2f60c-182">합니다 **PostAsJsonAsync** 메서드:</span><span class="sxs-lookup"><span data-stu-id="2f60c-182">The **PostAsJsonAsync** method:</span></span>

* <span data-ttu-id="2f60c-183">Json 개체를 serialize합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-183">Serializes an object to JSON.</span></span>
* <span data-ttu-id="2f60c-184">POST 요청에 JSON 페이로드를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-184">Sends the JSON payload in a POST request.</span></span>

<span data-ttu-id="2f60c-185">요청이 성공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-185">If the request succeeds:</span></span>

* <span data-ttu-id="2f60c-186">201 (만들어짐) 응답을 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-186">It should return a 201 (Created) response.</span></span>
* <span data-ttu-id="2f60c-187">응답의 Location 헤더의 생성된 된 리소스의 URL을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-187">The response should include the URL of the created resources in the Location header.</span></span>

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a><span data-ttu-id="2f60c-188">리소스를 업데이트 하는 PUT 요청을 보내기</span><span class="sxs-lookup"><span data-stu-id="2f60c-188">Sending a PUT Request to Update a Resource</span></span>

<span data-ttu-id="2f60c-189">다음 코드는 제품을 업데이트 하는 PUT 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-189">The following code sends a PUT request to update a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

<span data-ttu-id="2f60c-190">합니다 **PutAsJsonAsync** 메서드처럼 작동 **PostAsJsonAsync**POST 대신 PUT 요청을 전송 하는 점을 제외 하 고, 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-190">The **PutAsJsonAsync** method works like **PostAsJsonAsync**, except that it sends a PUT request instead of POST.</span></span>

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a><span data-ttu-id="2f60c-191">리소스를 삭제 하는 DELETE 요청을 보내기</span><span class="sxs-lookup"><span data-stu-id="2f60c-191">Sending a DELETE Request to Delete a Resource</span></span>

<span data-ttu-id="2f60c-192">다음 코드는 제품을 삭제 하는 DELETE 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-192">The following code sends a DELETE request to delete a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

<span data-ttu-id="2f60c-193">GET, 같은 삭제 요청 되지 않은 요청 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-193">Like GET, a DELETE request does not have a request body.</span></span> <span data-ttu-id="2f60c-194">삭제를 사용 하 여 JSON 또는 XML 형식으로 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-194">You don't need to specify JSON or XML format with DELETE.</span></span>

## <a name="test-the-sample"></a><span data-ttu-id="2f60c-195">샘플 테스트</span><span class="sxs-lookup"><span data-stu-id="2f60c-195">Test the sample</span></span>

<span data-ttu-id="2f60c-196">클라이언트 앱을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-196">To test the client app:</span></span>

1. <span data-ttu-id="2f60c-197">[다운로드](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) 및 서버 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-197">[Download](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) and run the server app.</span></span> <span data-ttu-id="2f60c-198">[지침을 다운로드하세요](/aspnet/core/tutorials/#how-to-download-a-sample).</span><span class="sxs-lookup"><span data-stu-id="2f60c-198">[Download instructions](/aspnet/core/tutorials/#how-to-download-a-sample).</span></span> <span data-ttu-id="2f60c-199">서버 앱이 작동을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-199">Verify the server app is working.</span></span> <span data-ttu-id="2f60c-200">예를 들어 `http://localhost:64195/api/products` 제품 목록을 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-200">For example, `http://localhost:64195/api/products` should return a list of products.</span></span>
2. <span data-ttu-id="2f60c-201">HTTP 요청에 대 한 기본 URI를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-201">Set the base URI for HTTP requests.</span></span> <span data-ttu-id="2f60c-202">서버 앱에서 사용 되는 포트를 포트 번호를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-202">Change the port number to the port used in the server app.</span></span>
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. <span data-ttu-id="2f60c-203">클라이언트 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-203">Run the client app.</span></span> <span data-ttu-id="2f60c-204">다음 출력이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f60c-204">The following output is produced:</span></span>

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```
