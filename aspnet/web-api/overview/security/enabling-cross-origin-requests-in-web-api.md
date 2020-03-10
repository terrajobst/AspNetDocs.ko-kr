---
uid: web-api/overview/security/enabling-cross-origin-requests-in-web-api
title: ASP.NET Web API 2에서 크로스-원본 요청을 사용 하도록 설정 Microsoft Docs
author: MikeWasson
description: ASP.NET Web API에서 CORS (원본 간 리소스 공유)를 지 원하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 01/29/2019
ms.assetid: 9b265a5a-6a70-4a82-adce-2d7c56ae8bdd
msc.legacyurl: /web-api/overview/security/enabling-cross-origin-requests-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 9d3016d98fa6c3a55359c6dab0737407b29925f1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447617"
---
# <a name="enable-cross-origin-requests-in-aspnet-web-api-2"></a><span data-ttu-id="76cff-103">ASP.NET Web API 2에서 크로스-원본 요청을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="76cff-103">Enable cross-origin requests in ASP.NET Web API 2</span></span>

<span data-ttu-id="76cff-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="76cff-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="76cff-105">브라우저 보안은 웹 페이지에서 다른 도메인으로 AJAX 요청을 수행하지 못하도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-105">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="76cff-106">이러한 제한을 *동일한 원본 정책*이라고 하며 악의적인 사이트에서 다른 사이트의 중요 한 데이터를 읽지 못하도록 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-106">This restriction is called the *same-origin policy*, and prevents a malicious site from reading sensitive data from another site.</span></span> <span data-ttu-id="76cff-107">그러나 경우에 따라 다른 사이트에서 web API를 호출 하도록 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-107">However, sometimes you might want to let other sites call your web API.</span></span>
>
> <span data-ttu-id="76cff-108">CORS ( [원본 간 리소스 공유](http://www.w3.org/TR/cors/) )는 서버에서 동일한 원본 정책을 완화할 수 있게 해 주는 W3C 표준입니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-108">[Cross Origin Resource Sharing](http://www.w3.org/TR/cors/) (CORS) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="76cff-109">CORS를 사용하면 서버에서 명시적으로 일부 원본 간 요청을 허용하는 한편 다른 요청은 거부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-109">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span> <span data-ttu-id="76cff-110">CORS는 [JSONP](http://en.wikipedia.org/wiki/JSONP)와 같은 이전 기술 보다 더 안전 하 고 유연 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-110">CORS is safer and more flexible than earlier techniques such as [JSONP](http://en.wikipedia.org/wiki/JSONP).</span></span> <span data-ttu-id="76cff-111">이 자습서에서는 Web API 응용 프로그램에서 CORS를 사용 하도록 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-111">This tutorial shows how to enable CORS in your Web API application.</span></span>
>
> ## <a name="software-used-in-the-tutorial"></a><span data-ttu-id="76cff-112">자습서에서 사용 되는 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="76cff-112">Software used in the tutorial</span></span>
>
> - [<span data-ttu-id="76cff-113">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="76cff-113">Visual Studio</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="76cff-114">웹 API 2.2</span><span class="sxs-lookup"><span data-stu-id="76cff-114">Web API 2.2</span></span>

## <a name="introduction"></a><span data-ttu-id="76cff-115">소개</span><span class="sxs-lookup"><span data-stu-id="76cff-115">Introduction</span></span>

<span data-ttu-id="76cff-116">이 자습서에서는 ASP.NET Web API의 CORS 지원에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-116">This tutorial demonstrates CORS support in ASP.NET Web API.</span></span> <span data-ttu-id="76cff-117">웹 API 컨트롤러를 호스트 하는 두 개의 ASP.NET 프로젝트와 WebService를 호출 하는 "WebClient" 라는 두 개의 프로젝트를 만들어 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-117">We'll start by creating two ASP.NET projects – one called "WebService", which hosts a Web API controller, and the other called "WebClient", which calls WebService.</span></span> <span data-ttu-id="76cff-118">두 응용 프로그램이 서로 다른 도메인에서 호스트 되기 때문에 WebClient에서 WebService로의 AJAX 요청은 크로스-원본 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-118">Because the two applications are hosted at different domains, an AJAX request from WebClient to WebService is a cross-origin request.</span></span>

![](enabling-cross-origin-requests-in-web-api/_static/image1.png)

### <a name="what-is-same-origin"></a><span data-ttu-id="76cff-119">"동일 원본"이란?</span><span class="sxs-lookup"><span data-stu-id="76cff-119">What is "same origin"?</span></span>

<span data-ttu-id="76cff-120">두 URL의 스키마, 호스트 및 포트가 모두 동일한 경우, 두 URL의 원본이 동일하다고 말합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-120">Two URLs have the same origin if they have identical schemes, hosts, and ports.</span></span> <span data-ttu-id="76cff-121">([RFC 6454](http://tools.ietf.org/html/rfc6454))</span><span class="sxs-lookup"><span data-stu-id="76cff-121">([RFC 6454](http://tools.ietf.org/html/rfc6454))</span></span>

<span data-ttu-id="76cff-122">다음 두 URL은 동일한 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-122">These two URLs have the same origin:</span></span>

- `http://example.com/foo.html`
- `http://example.com/bar.html`

<span data-ttu-id="76cff-123">반면, 다음 URL들은 위의 두 URL과는 다른 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-123">These URLs have different origins than the previous two:</span></span>

- <span data-ttu-id="76cff-124">`http://example.net`-다른 도메인</span><span class="sxs-lookup"><span data-stu-id="76cff-124">`http://example.net` - Different domain</span></span>
- <span data-ttu-id="76cff-125">`http://example.com:9000/foo.html`-다른 포트</span><span class="sxs-lookup"><span data-stu-id="76cff-125">`http://example.com:9000/foo.html` - Different port</span></span>
- <span data-ttu-id="76cff-126">`https://example.com/foo.html`-다른 체계</span><span class="sxs-lookup"><span data-stu-id="76cff-126">`https://example.com/foo.html` - Different scheme</span></span>
- <span data-ttu-id="76cff-127">`http://www.example.com/foo.html`-다른 하위 도메인</span><span class="sxs-lookup"><span data-stu-id="76cff-127">`http://www.example.com/foo.html` - Different subdomain</span></span>

> [!NOTE]
> <span data-ttu-id="76cff-128">Internet Explorer는 원본을 비교할 때 포트를 고려 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-128">Internet Explorer does not consider the port when comparing origins.</span></span>

## <a name="create-the-webservice-project"></a><span data-ttu-id="76cff-129">웹 서비스 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="76cff-129">Create the WebService project</span></span>

> [!NOTE]
> <span data-ttu-id="76cff-130">이 섹션에서는 Web API 프로젝트를 만드는 방법을 이미 알고 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-130">This section assumes you already know how to create Web API projects.</span></span> <span data-ttu-id="76cff-131">그렇지 않은 경우 [ASP.NET Web API 시작](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="76cff-131">If not, see [Getting Started with ASP.NET Web API](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>

1. <span data-ttu-id="76cff-132">Visual Studio를 시작 하 고 새 **.NET Framework (ASP.NET Web Application)** 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-132">Start Visual Studio and create a new **ASP.NET Web Application (.NET Framework)** project.</span></span>
2. <span data-ttu-id="76cff-133">**새 ASP.NET 웹 응용 프로그램** 대화 상자에서 **빈** 프로젝트 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-133">In the **New ASP.NET Web Application** dialog box, select the **Empty** project template.</span></span> <span data-ttu-id="76cff-134">**에 대 한 폴더 및 핵심 참조 추가**에서 **Web API** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-134">Under **Add folders and core references for**, select the **Web API** checkbox.</span></span>

   ![Visual Studio의 새 ASP.NET 프로젝트 대화 상자](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog.png)

3. <span data-ttu-id="76cff-136">다음 코드를 사용 하 여 `TestController` 이라는 웹 API 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-136">Add a Web API controller named `TestController` with the following code:</span></span>

   [!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample1.cs)]

4. <span data-ttu-id="76cff-137">응용 프로그램을 로컬로 실행 하거나 Azure에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-137">You can run the application locally or deploy to Azure.</span></span> <span data-ttu-id="76cff-138">(이 자습서의 스크린샷에서 앱은 Azure App Service Web Apps에 배포 됩니다.) Web API가 작동 하는지 확인 하려면 `http://hostname/api/test/`으로 이동 합니다. 여기서 *hostname* 은 응용 프로그램을 배포한 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-138">(For the screenshots in this tutorial, the app deploys to Azure App Service Web Apps.) To verify that the web API is working, navigate to `http://hostname/api/test/`, where *hostname* is the domain where you deployed the application.</span></span> <span data-ttu-id="76cff-139">응답 텍스트 &quot;GET: 테스트 메시지&quot;표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-139">You should see the response text, &quot;GET: Test Message&quot;.</span></span>

   ![테스트 메시지를 표시 하는 웹 브라우저](enabling-cross-origin-requests-in-web-api/_static/image4.png)

## <a name="create-the-webclient-project"></a><span data-ttu-id="76cff-141">WebClient 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="76cff-141">Create the WebClient project</span></span>

1. <span data-ttu-id="76cff-142">다른 **.NET Framework (ASP.NET Web Application)** 프로젝트를 만들고 **MVC** 프로젝트 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-142">Create another **ASP.NET Web Application (.NET Framework)** project and select the **MVC** project template.</span></span> <span data-ttu-id="76cff-143">필요에 따라 \*\*인증 > \*\* **인증 안 함**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-143">Optionally, select **Change Authentication** > **No Authentication**.</span></span> <span data-ttu-id="76cff-144">이 자습서에 대 한 인증이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-144">You don't need authentication for this tutorial.</span></span>

   ![Visual Studio의 새 ASP.NET 프로젝트 대화 상자에서 MVC 템플릿](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog-mvc.png)

2. <span data-ttu-id="76cff-146">**솔루션 탐색기**에서 파일 *Views/Home/Index. cshtml*를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-146">In **Solution Explorer**, open the file *Views/Home/Index.cshtml*.</span></span> <span data-ttu-id="76cff-147">이 파일의 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-147">Replace the code in this file with the following:</span></span>

   [!code-cshtml[Main](enabling-cross-origin-requests-in-web-api/samples/sample2.cshtml?highlight=13)]

   <span data-ttu-id="76cff-148">*Serviceurl* 변수에서 WebService 앱의 URI를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-148">For the *serviceUrl* variable, use the URI of the WebService app.</span></span>

3. <span data-ttu-id="76cff-149">로컬에서 WebClient 앱을 실행 하거나 다른 웹 사이트에 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-149">Run the WebClient app locally or publish it to another website.</span></span>

<span data-ttu-id="76cff-150">"사용해 보세요." 단추를 클릭 하면 드롭다운 상자 (GET, POST 또는 PUT)에 나열 된 HTTP 메서드를 사용 하 여 AJAX 요청이 WebService 앱에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-150">When you click the "Try It" button, an AJAX request is submitted to the WebService app using the HTTP method listed in the dropdown box (GET, POST, or PUT).</span></span> <span data-ttu-id="76cff-151">이렇게 하면 서로 다른 크로스-원본 요청을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-151">This lets you examine different cross-origin requests.</span></span> <span data-ttu-id="76cff-152">현재 WebService 앱은 CORS를 지원 하지 않으므로 단추를 클릭 하면 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-152">Currently, the WebService app does not support CORS, so if you click the button you'll get an error.</span></span>

![브라우저에서 ' 사용해 보세요 ' 오류](enabling-cross-origin-requests-in-web-api/_static/image7.png)

> [!NOTE]
> <span data-ttu-id="76cff-154">[Fiddler](https://www.telerik.com/fiddler)와 같은 도구에서 HTTP 트래픽을 볼 경우 브라우저가 GET 요청을 보내고 요청이 성공 하지만 AJAX 호출에서 오류를 반환 하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-154">If you watch the HTTP traffic in a tool like [Fiddler](https://www.telerik.com/fiddler), you'll see that the browser does send the GET request, and the request succeeds, but the AJAX call returns an error.</span></span> <span data-ttu-id="76cff-155">동일한 원본 정책이 브라우저에서 요청을 *보내지* 못하도록 하는 것을 이해 하는 것이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-155">It's important to understand that same-origin policy does not prevent the browser from *sending* the request.</span></span> <span data-ttu-id="76cff-156">대신 응용 프로그램에서 *응답*을 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-156">Instead, it prevents the application from seeing the *response*.</span></span>

![웹 요청을 표시 하는 Fiddler 웹 디버거](enabling-cross-origin-requests-in-web-api/_static/image8.png)

## <a name="enable-cors"></a><span data-ttu-id="76cff-158">CORS를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="76cff-158">Enable CORS</span></span>

<span data-ttu-id="76cff-159">이제 WebService 앱에서 CORS를 사용 하도록 설정 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-159">Now let's enable CORS in the WebService app.</span></span> <span data-ttu-id="76cff-160">먼저 CORS NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-160">First, add the CORS NuGet package.</span></span> <span data-ttu-id="76cff-161">Visual Studio의 **도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-161">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="76cff-162">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-162">In the Package Manager Console window, type the following command:</span></span>

[!code-powershell[Main](enabling-cross-origin-requests-in-web-api/samples/sample3.ps1)]

<span data-ttu-id="76cff-163">이 명령은 최신 패키지를 설치 하 고 핵심 웹 API 라이브러리를 비롯 한 모든 종속성을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-163">This command installs the latest package and updates all dependencies, including the core Web API libraries.</span></span> <span data-ttu-id="76cff-164">`-Version` 플래그를 사용 하 여 특정 버전을 대상으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-164">Use the `-Version` flag to target a specific version.</span></span> <span data-ttu-id="76cff-165">CORS 패키지에는 Web API 2.0 이상이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-165">The CORS package requires Web API 2.0 or later.</span></span>

<span data-ttu-id="76cff-166">File *App\_Start/WebApiConfig .cs*를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-166">Open the file *App\_Start/WebApiConfig.cs*.</span></span> <span data-ttu-id="76cff-167">**Webapiconfig. Register** 메서드에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-167">Add the following code to the **WebApiConfig.Register** method:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample4.cs?highlight=9)]

<span data-ttu-id="76cff-168">그런 다음 `TestController` 클래스에 **[EnableCors]** 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-168">Next, add the **[EnableCors]** attribute to the `TestController` class:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample5.cs?highlight=3,7)]

<span data-ttu-id="76cff-169">*원본* 매개 변수의 경우 WebClient 응용 프로그램을 배포한 URI를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-169">For the *origins* parameter, use the URI where you deployed the WebClient application.</span></span> <span data-ttu-id="76cff-170">이렇게 하면 다른 모든 도메인 간 요청을 허용 하지 않고, WebClient의 크로스-원본 요청을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-170">This allows cross-origin requests from WebClient, while still disallowing all other cross-domain requests.</span></span> <span data-ttu-id="76cff-171">나중에 **[EnableCors]** 에 대 한 매개 변수를 자세히 설명 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-171">Later, I'll describe the parameters for **[EnableCors]** in more detail.</span></span>

<span data-ttu-id="76cff-172">*원본* URL의 끝에 슬래시를 포함 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="76cff-172">Do not include a forward slash at the end of the *origins* URL.</span></span>

<span data-ttu-id="76cff-173">업데이트 된 웹 서비스 응용 프로그램을 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-173">Redeploy the updated WebService application.</span></span> <span data-ttu-id="76cff-174">WebClient를 업데이트할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-174">You don't need to update WebClient.</span></span> <span data-ttu-id="76cff-175">이제 WebClient의 AJAX 요청이 성공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-175">Now the AJAX request from WebClient should succeed.</span></span> <span data-ttu-id="76cff-176">GET, PUT 및 POST 메서드를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-176">The GET, PUT, and POST methods are all allowed.</span></span>

![성공적인 테스트 메시지를 표시 하는 웹 브라우저](enabling-cross-origin-requests-in-web-api/_static/image9.png)

## <a name="how-cors-works"></a><span data-ttu-id="76cff-178">CORS 작동 방법</span><span class="sxs-lookup"><span data-stu-id="76cff-178">How CORS Works</span></span>

<span data-ttu-id="76cff-179">이 섹션에서는 HTTP 메시지 수준에서 CORS 요청에 발생 하는 작업에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-179">This section describes what happens in a CORS request, at the level of the HTTP messages.</span></span> <span data-ttu-id="76cff-180">**[EnableCors]** 특성을 올바르게 구성 하 고 원하는 대로 작동 하지 않는 경우 문제를 해결할 수 있도록 CORS가 작동 하는 방식을 이해 하는 것이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-180">It's important to understand how CORS works, so that you can configure the **[EnableCors]** attribute correctly and troubleshoot if things don't work as you expect.</span></span>

<span data-ttu-id="76cff-181">CORS 명세에서는 교차 원본 요청을 활성화시키기 위한 용도로 몇 가지 새로운 HTTP 헤더들이 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-181">The CORS specification introduces several new HTTP headers that enable cross-origin requests.</span></span> <span data-ttu-id="76cff-182">브라우저에서 CORS를 지 원하는 경우 원본 간 요청에 대해 이러한 헤더를 자동으로 설정 합니다. JavaScript 코드에서 특별 한 작업을 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-182">If a browser supports CORS, it sets these headers automatically for cross-origin requests; you don't need to do anything special in your JavaScript code.</span></span>

<span data-ttu-id="76cff-183">원본 간 요청의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-183">Here is an example of a cross-origin request.</span></span> <span data-ttu-id="76cff-184">"원본" 헤더는 요청을 수행 하는 사이트의 도메인을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-184">The "Origin" header gives the domain of the site that is making the request.</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample6.cmd?highlight=5)]

<span data-ttu-id="76cff-185">서버에서 요청을 허용 하는 경우 액세스 제어 허용 원본 헤더를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-185">If the server allows the request, it sets the Access-Control-Allow-Origin header.</span></span> <span data-ttu-id="76cff-186">이 헤더의 값이 원본 헤더와 일치 하거나 와일드 카드 값 "\*" 이며,이는 모든 원본이 허용 됨을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-186">The value of this header either matches the Origin header, or is the wildcard value "\*", meaning that any origin is allowed.</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample7.cmd?highlight=5)]

<span data-ttu-id="76cff-187">응답에 액세스 제어 허용-원본 헤더가 포함 되어 있지 않으면 AJAX 요청이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-187">If the response does not include the Access-Control-Allow-Origin header, the AJAX request fails.</span></span> <span data-ttu-id="76cff-188">특히 브라우저에서 요청을 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-188">Specifically, the browser disallows the request.</span></span> <span data-ttu-id="76cff-189">서버에서 응답을 반환 하는 경우에도 브라우저는 클라이언트 응용 프로그램에서 응답을 사용할 수 있도록 설정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-189">Even if the server returns a successful response, the browser does not make the response available to the client application.</span></span>

<span data-ttu-id="76cff-190">**실행 전 요청**</span><span class="sxs-lookup"><span data-stu-id="76cff-190">**Preflight Requests**</span></span>

<span data-ttu-id="76cff-191">일부 CORS 요청에 대해서는 브라우저에서 리소스에 대 한 실제 요청을 보내기 전에 "실행 전 요청" 이라는 추가 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-191">For some CORS requests, the browser sends an additional request, called a "preflight request", before it sends the actual request for the resource.</span></span>

<span data-ttu-id="76cff-192">다음 조건에 해당 하는 경우 브라우저에서 실행 전 요청을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-192">The browser can skip the preflight request if the following conditions are true:</span></span>

- <span data-ttu-id="76cff-193">요청 메서드는 *GET, HEAD* 또는 POST입니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-193">The request method is GET, HEAD, or POST, *and*</span></span>
- <span data-ttu-id="76cff-194">응용 프로그램은 허용, 허용 언어, 콘텐츠 언어, 콘텐츠 형식 또는 마지막 이벤트 ID 이외의 요청 *헤더를 설정* 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-194">The application does not set any request headers other than Accept, Accept-Language, Content-Language, Content-Type, or Last-Event-ID, *and*</span></span>
- <span data-ttu-id="76cff-195">Content-type 헤더 (설정 된 경우)는 다음 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-195">The Content-Type header (if set) is one of the following:</span></span>

    - <span data-ttu-id="76cff-196">application/x-www-form-urlencoded</span><span class="sxs-lookup"><span data-stu-id="76cff-196">application/x-www-form-urlencoded</span></span>
    - <span data-ttu-id="76cff-197">다중 파트/폼 데이터</span><span class="sxs-lookup"><span data-stu-id="76cff-197">multipart/form-data</span></span>
    - <span data-ttu-id="76cff-198">텍스트/일반</span><span class="sxs-lookup"><span data-stu-id="76cff-198">text/plain</span></span>

<span data-ttu-id="76cff-199">요청 헤더에 대 한 규칙은 응용 프로그램이 **XMLHttpRequest** 개체에 대해 **setRequestHeader** 를 호출 하 여 설정 하는 헤더에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-199">The rule about request headers applies to headers that the application sets by calling **setRequestHeader** on the **XMLHttpRequest** object.</span></span> <span data-ttu-id="76cff-200">CORS 사양은 이러한 "author 요청 헤더"를 호출 합니다. 이 규칙은 *브라우저* 에서 설정할 수 있는 헤더 (예: 사용자 에이전트, 호스트 또는 콘텐츠 길이)에는 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-200">(The CORS specification calls these "author request headers".) The rule does not apply to headers the *browser* can set, such as User-Agent, Host, or Content-Length.</span></span>

<span data-ttu-id="76cff-201">다음은 실행 전 요청의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-201">Here is an example of a preflight request:</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample8.cmd?highlight=4-5)]

<span data-ttu-id="76cff-202">사전 비행 요청은 HTTP OPTIONS 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-202">The pre-flight request uses the HTTP OPTIONS method.</span></span> <span data-ttu-id="76cff-203">여기에는 두 가지 특수 헤더가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-203">It includes two special headers:</span></span>

- <span data-ttu-id="76cff-204">액세스 제어-요청 메서드: 실제 요청에 사용 되는 HTTP 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-204">Access-Control-Request-Method: The HTTP method that will be used for the actual request.</span></span>
- <span data-ttu-id="76cff-205">액세스 제어-요청 헤더: *응용 프로그램이* 실제 요청에 대해 설정한 요청 헤더의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-205">Access-Control-Request-Headers: A list of request headers that the *application* set on the actual request.</span></span> <span data-ttu-id="76cff-206">이 경우 브라우저에서 설정 하는 헤더는 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-206">(Again, this does not include headers that the browser sets.)</span></span>

<span data-ttu-id="76cff-207">서버에서 요청을 허용 한다고 가정 하는 예제 응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-207">Here is an example response, assuming that the server allows the request:</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample9.cmd?highlight=6-7)]

<span data-ttu-id="76cff-208">응답에는 허용 되는 메서드를 나열 하는 액세스 제어-허용 메서드 헤더와 허용 되는 헤더를 나열 하는 액세스 제어-헤더 헤더가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-208">The response includes an Access-Control-Allow-Methods header that lists the allowed methods, and optionally an Access-Control-Allow-Headers header, which lists the allowed headers.</span></span> <span data-ttu-id="76cff-209">실행 전 요청이 성공 하는 경우 브라우저는 앞에서 설명한 대로 실제 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-209">If the preflight request succeeds, the browser sends the actual request, as described earlier.</span></span>

<span data-ttu-id="76cff-210">실행 전 옵션 요청 (예: [Fiddler](https://www.telerik.com/fiddler) 및 [postman](https://www.getpostman.com/))을 사용 하 여 끝점을 테스트 하는 데 일반적으로 사용 되는 도구는 기본적으로 필수 옵션 헤더를 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-210">Tools commonly used to test endpoints with preflight OPTIONS requests (for example, [Fiddler](https://www.telerik.com/fiddler) and [Postman](https://www.getpostman.com/)) don't send the required OPTIONS headers by default.</span></span> <span data-ttu-id="76cff-211">`Access-Control-Request-Method` 및 `Access-Control-Request-Headers` 헤더가 요청과 함께 전송 되 고 옵션 헤더가 IIS를 통해 앱에 도달 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-211">Confirm that the `Access-Control-Request-Method` and `Access-Control-Request-Headers` headers are sent with the request and that OPTIONS headers reach the app through IIS.</span></span>

<span data-ttu-id="76cff-212">ASP.NET 앱이 옵션 요청을 수신 하 고 처리할 수 있도록 IIS를 구성 하려면 `<system.webServer><handlers>` 섹션에서 앱의 *web.config* 파일에 다음 구성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-212">To configure IIS to allow an ASP.NET app to receive and handle OPTION requests, add the following configuration to the app's *web.config* file in the `<system.webServer><handlers>` section:</span></span>

```xml
<system.webServer>
  <handlers>
    <remove name="ExtensionlessUrlHandler-Integrated-4.0" />
    <remove name="OPTIONSVerbHandler" />
    <add name="ExtensionlessUrlHandler-Integrated-4.0" path="*." verb="*" type="System.Web.Handlers.TransferRequestHandler" preCondition="integratedMode,runtimeVersionv4.0" />
  </handlers>
</system.webServer>
```

<span data-ttu-id="76cff-213">`OPTIONSVerbHandler`를 제거 하면 IIS에서 옵션 요청을 처리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-213">The removal of `OPTIONSVerbHandler` prevents IIS from handling OPTIONS requests.</span></span> <span data-ttu-id="76cff-214">기본 모듈 등록에서는 확장명 없는 Url을 사용 하 여 GET, HEAD, POST 및 DEBUG 요청만 허용 하기 때문에 `ExtensionlessUrlHandler-Integrated-4.0`를 대체 하 여 옵션 요청이 앱에 도달 하도록 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-214">The replacement of `ExtensionlessUrlHandler-Integrated-4.0` allows OPTIONS requests to reach the app because the default module registration only allows GET, HEAD, POST, and DEBUG requests with extensionless URLs.</span></span>

## <a name="scope-rules-for-enablecors"></a><span data-ttu-id="76cff-215">[EnableCors]에 대 한 범위 규칙</span><span class="sxs-lookup"><span data-stu-id="76cff-215">Scope Rules for [EnableCors]</span></span>

<span data-ttu-id="76cff-216">응용 프로그램의 모든 웹 API 컨트롤러에 대해 작업당 CORS를 사용 하도록 설정 하거나, 컨트롤러 당 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-216">You can enable CORS per action, per controller, or globally for all Web API controllers in your application.</span></span>

<span data-ttu-id="76cff-217">**작업 당**</span><span class="sxs-lookup"><span data-stu-id="76cff-217">**Per Action**</span></span>

<span data-ttu-id="76cff-218">단일 작업에 대해 CORS를 사용 하도록 설정 하려면 동작 메서드에서 **[EnableCors]** 특성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-218">To enable CORS for a single action, set the **[EnableCors]** attribute on the action method.</span></span> <span data-ttu-id="76cff-219">다음 예제에서는 `GetItem` 메서드에 대해서만 CORS를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-219">The following example enables CORS for the `GetItem` method only.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample10.cs)]

<span data-ttu-id="76cff-220">**컨트롤러 당**</span><span class="sxs-lookup"><span data-stu-id="76cff-220">**Per Controller**</span></span>

<span data-ttu-id="76cff-221">컨트롤러 클래스에서 **[EnableCors]** 를 설정 하면 컨트롤러의 모든 작업에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-221">If you set **[EnableCors]** on the controller class, it applies to all the actions on the controller.</span></span> <span data-ttu-id="76cff-222">작업에 대해 CORS를 사용 하지 않도록 설정 하려면 **[DisableCors]** 특성을 작업에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-222">To disable CORS for an action, add the **[DisableCors]** attribute to the action.</span></span> <span data-ttu-id="76cff-223">다음 예에서는 `PutItem`를 제외 하 고 모든 메서드에 대해 CORS를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-223">The following example enables CORS for every method except `PutItem`.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample11.cs)]

<span data-ttu-id="76cff-224">**전역적으로**</span><span class="sxs-lookup"><span data-stu-id="76cff-224">**Globally**</span></span>

<span data-ttu-id="76cff-225">응용 프로그램의 모든 Web API 컨트롤러에 대해 CORS를 사용 하도록 설정 하려면 **EnableCorsAttribute** 인스턴스를 **EnableCors** 메서드에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-225">To enable CORS for all Web API controllers in your application, pass an **EnableCorsAttribute** instance to the **EnableCors** method:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample12.cs)]

<span data-ttu-id="76cff-226">특성을 두 개 이상의 범위에서 설정 하는 경우 우선 순위는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-226">If you set the attribute at more than one scope, the order of precedence is:</span></span>

1. <span data-ttu-id="76cff-227">작업</span><span class="sxs-lookup"><span data-stu-id="76cff-227">Action</span></span>
2. <span data-ttu-id="76cff-228">컨트롤러</span><span class="sxs-lookup"><span data-stu-id="76cff-228">Controller</span></span>
3. <span data-ttu-id="76cff-229">Global</span><span class="sxs-lookup"><span data-stu-id="76cff-229">Global</span></span>

## <a name="set-the-allowed-origins"></a><span data-ttu-id="76cff-230">허용되는 원본 설정하기</span><span class="sxs-lookup"><span data-stu-id="76cff-230">Set the allowed origins</span></span>

<span data-ttu-id="76cff-231">**[EnableCors]** 특성의 *원본* 매개 변수는 리소스에 액세스할 수 있는 원본을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-231">The *origins* parameter of the **[EnableCors]** attribute specifies which origins are allowed to access the resource.</span></span> <span data-ttu-id="76cff-232">값은 허용 된 원본에 대 한 쉼표로 구분 된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-232">The value is a comma-separated list of the allowed origins.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample13.cs)]

<span data-ttu-id="76cff-233">와일드 카드 값 "\*"을 사용 하 여 모든 원본에서 요청을 허용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-233">You can also use the wildcard value "\*" to allow requests from any origins.</span></span>

<span data-ttu-id="76cff-234">모든 원본의 요청을 허용하기 전에 신중히 고민하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-234">Consider carefully before allowing requests from any origin.</span></span> <span data-ttu-id="76cff-235">즉, 웹 사이트를 그대로 사용 하 여 웹 API에 대 한 AJAX 호출을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-235">It means that literally any website can make AJAX calls to your web API.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample14.cs)]

## <a name="set-the-allowed-http-methods"></a><span data-ttu-id="76cff-236">허용되는 HTTP 메서드 설정하기</span><span class="sxs-lookup"><span data-stu-id="76cff-236">Set the allowed HTTP methods</span></span>

<span data-ttu-id="76cff-237">**[EnableCors]** 특성의 *메서드* 매개 변수는 리소스에 액세스할 수 있는 HTTP 메서드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-237">The *methods* parameter of the **[EnableCors]** attribute specifies which HTTP methods are allowed to access the resource.</span></span> <span data-ttu-id="76cff-238">모든 메서드를 허용 하려면 "\*" 와일드 카드 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-238">To allow all methods, use the wildcard value "\*".</span></span> <span data-ttu-id="76cff-239">다음 예제에서는 GET 및 POST 요청만 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-239">The following example allows only GET and POST requests.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample15.cs)]

## <a name="set-the-allowed-request-headers"></a><span data-ttu-id="76cff-240">허용되는 요청 헤더 설정하기</span><span class="sxs-lookup"><span data-stu-id="76cff-240">Set the allowed request headers</span></span>

<span data-ttu-id="76cff-241">이 문서에서는 이전에 실행 전 요청에 액세스 제어 요청 헤더 헤더를 포함 하 여 응용 프로그램에 의해 설정 된 HTTP 헤더를 나열 하는 방법에 대해 설명 했습니다 ("작성자 요청 헤더").</span><span class="sxs-lookup"><span data-stu-id="76cff-241">This article described earlier how a preflight request might include an Access-Control-Request-Headers header, listing the HTTP headers set by the application (the so-called "author request headers").</span></span> <span data-ttu-id="76cff-242">**[EnableCors]** 특성의 *headers* 매개 변수는 허용 되는 저자 요청 헤더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-242">The *headers* parameter of the **[EnableCors]** attribute specifies which author request headers are allowed.</span></span> <span data-ttu-id="76cff-243">모든 헤더를 허용 하려면 *헤더* 를 "\*"로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-243">To allow any headers, set *headers* to "\*".</span></span> <span data-ttu-id="76cff-244">특정 헤더를 허용 목록 하려면 *헤더* 를 허용 된 헤더의 쉼표로 구분 된 목록으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-244">To whitelist specific headers, set *headers* to a comma-separated list of the allowed headers:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample16.cs)]

<span data-ttu-id="76cff-245">그러나 브라우저는 액세스 제어 요청 헤더를 설정 하는 방법과 완전히 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-245">However, browsers are not entirely consistent in how they set Access-Control-Request-Headers.</span></span> <span data-ttu-id="76cff-246">예를 들어 Chrome에는 현재 "원본"이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-246">For example, Chrome currently includes "origin".</span></span> <span data-ttu-id="76cff-247">FireFox에는 응용 프로그램에서 스크립트를 설정 하는 경우에도 "Accept"와 같은 표준 헤더가 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-247">FireFox does not include standard headers such as "Accept", even when the application sets them in script.</span></span>

<span data-ttu-id="76cff-248">*헤더* 를 "\*" 이외의 값으로 설정 하는 경우 "accept", "content-type" 및 "원본"을 포함 하 고 지원 하려는 사용자 지정 헤더를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-248">If you set *headers* to anything other than "\*", you should include at least "accept", "content-type", and "origin", plus any custom headers that you want to support.</span></span>

## <a name="set-the-allowed-response-headers"></a><span data-ttu-id="76cff-249">허용 되는 응답 헤더 설정</span><span class="sxs-lookup"><span data-stu-id="76cff-249">Set the allowed response headers</span></span>

<span data-ttu-id="76cff-250">기본적으로 브라우저는 응용 프로그램에 대 한 모든 응답 헤더를 노출 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-250">By default, the browser does not expose all of the response headers to the application.</span></span> <span data-ttu-id="76cff-251">기본적으로 사용 가능한 응답 헤더들은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-251">The response headers that are available by default are:</span></span>

- <span data-ttu-id="76cff-252">Cache-Control</span><span class="sxs-lookup"><span data-stu-id="76cff-252">Cache-Control</span></span>
- <span data-ttu-id="76cff-253">Content-Language</span><span class="sxs-lookup"><span data-stu-id="76cff-253">Content-Language</span></span>
- <span data-ttu-id="76cff-254">콘텐츠 형식</span><span class="sxs-lookup"><span data-stu-id="76cff-254">Content-Type</span></span>
- <span data-ttu-id="76cff-255">만료</span><span class="sxs-lookup"><span data-stu-id="76cff-255">Expires</span></span>
- <span data-ttu-id="76cff-256">Last-Modified</span><span class="sxs-lookup"><span data-stu-id="76cff-256">Last-Modified</span></span>
- <span data-ttu-id="76cff-257">Pragma</span><span class="sxs-lookup"><span data-stu-id="76cff-257">Pragma</span></span>

<span data-ttu-id="76cff-258">CORS spec은 이러한 [간단한 응답 헤더](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header)를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-258">The CORS spec calls these [simple response headers](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header).</span></span> <span data-ttu-id="76cff-259">응용 프로그램에서 다른 헤더를 사용할 수 있도록 하려면 **[EnableCors]** 의 *exposedHeaders* 매개 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-259">To make other headers available to the application, set the *exposedHeaders* parameter of **[EnableCors]**.</span></span>

<span data-ttu-id="76cff-260">다음 예제에서 컨트롤러의 `Get` 메서드는 ' X-사용자 지정 헤더 ' 라는 사용자 지정 헤더를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-260">In the following example, the controller's `Get` method sets a custom header named ‘X-Custom-Header'.</span></span> <span data-ttu-id="76cff-261">기본적으로 브라우저는 크로스-원본 요청에서이 헤더를 노출 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-261">By default, the browser will not expose this header in a cross-origin request.</span></span> <span data-ttu-id="76cff-262">헤더를 사용할 수 있도록 설정 하려면 *exposedHeaders*에 ' X X X-u r l '을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-262">To make the header available, include ‘X-Custom-Header' in *exposedHeaders*.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample17.cs)]

## <a name="pass-credentials-in-cross-origin-requests"></a><span data-ttu-id="76cff-263">크로스-원본 요청에서 자격 증명 전달</span><span class="sxs-lookup"><span data-stu-id="76cff-263">Pass credentials in cross-origin requests</span></span>

<span data-ttu-id="76cff-264">CORS 요청에서 자격 증명(Credentials)은 특별한 처리를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-264">Credentials require special handling in a CORS request.</span></span> <span data-ttu-id="76cff-265">기본적으로 브라우저는 원본 간 요청과 함께 자격 증명을 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-265">By default, the browser does not send any credentials with a cross-origin request.</span></span> <span data-ttu-id="76cff-266">여기에서 말하는 자격 증명에는 쿠키뿐만 아니라 HTTP 인증 스킴도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-266">Credentials include cookies as well as HTTP authentication schemes.</span></span> <span data-ttu-id="76cff-267">크로스-원본 요청을 사용 하 여 자격 증명을 보내려면 클라이언트에서 **XMLHttpRequest** 를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-267">To send credentials with a cross-origin request, the client must set **XMLHttpRequest.withCredentials** to true.</span></span>

<span data-ttu-id="76cff-268">**XMLHttpRequest** 직접 사용:</span><span class="sxs-lookup"><span data-stu-id="76cff-268">Using **XMLHttpRequest** directly:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample18.cs)]

<span data-ttu-id="76cff-269">jQuery를 사용할 경우:</span><span class="sxs-lookup"><span data-stu-id="76cff-269">In jQuery:</span></span>

[!code-javascript[Main](enabling-cross-origin-requests-in-web-api/samples/sample19.js)]

<span data-ttu-id="76cff-270">또한 서버에서도 자격 증명을 허용해야만 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-270">In addition, the server must allow the credentials.</span></span> <span data-ttu-id="76cff-271">Web API에서 원본 간 자격 증명을 허용 하려면 **[EnableCors]** 특성에서 **SupportsCredentials** 속성을 true로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-271">To allow cross-origin credentials in Web API, set the **SupportsCredentials** property to true on the **[EnableCors]** attribute:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample20.cs)]

<span data-ttu-id="76cff-272">이 속성이 true 이면 HTTP 응답에 액세스 제어-허용-자격 증명 헤더가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-272">If this property is true, the HTTP response will include an Access-Control-Allow-Credentials header.</span></span> <span data-ttu-id="76cff-273">이 헤더는 서버에서 원본 간 요청에 대 한 자격 증명을 허용 하도록 브라우저에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-273">This header tells the browser that the server allows credentials for a cross-origin request.</span></span>

<span data-ttu-id="76cff-274">브라우저에서 자격 증명을 전송 하지만 응답에 유효한 액세스 제어-허용-자격 증명 헤더가 포함 되어 있지 않은 경우 브라우저는 응용 프로그램에 응답을 노출 하지 않으며 AJAX 요청이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-274">If the browser sends credentials, but the response does not include a valid Access-Control-Allow-Credentials header, the browser will not expose the response to the application, and the AJAX request fails.</span></span>

<span data-ttu-id="76cff-275">**SupportsCredentials** 를 true로 설정 하는 경우에는 다른 도메인의 웹 사이트에서 사용자를 대신 하 여 사용자를 대신 하 여 사용자의 웹 API에 로그인 한 사용자의 자격 증명을 보낼 수 있다는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-275">Be careful about setting **SupportsCredentials** to true, because it means a website at another domain can send a logged-in user's credentials to your Web API on the user's behalf, without the user being aware.</span></span> <span data-ttu-id="76cff-276">CORS 사양은 **SupportsCredentials** 가 true 인 경우 \*&quot;에 대 &quot;한 *원본* 설정이 잘못 되었음을 알려 주는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-276">The CORS spec also states that setting *origins* to &quot;\*&quot; is invalid if **SupportsCredentials** is true.</span></span>

## <a name="custom-cors-policy-providers"></a><span data-ttu-id="76cff-277">사용자 지정 CORS 정책 공급자</span><span class="sxs-lookup"><span data-stu-id="76cff-277">Custom CORS policy providers</span></span>

<span data-ttu-id="76cff-278">**[EnableCors]** 특성은 **ICorsPolicyProvider** 인터페이스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-278">The **[EnableCors]** attribute implements the **ICorsPolicyProvider** interface.</span></span> <span data-ttu-id="76cff-279">**특성** 에서 파생 되는 클래스를 만들고 **ICorsPolicyProvider**을 구현 하 여 사용자 고유의 구현을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-279">You can provide your own implementation by creating a class that derives from **Attribute** and implements **ICorsPolicyProvider**.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample21.cs)]

<span data-ttu-id="76cff-280">이제 입력 하는 모든 위치 **[EnableCors]** 에 특성을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-280">Now you can apply the attribute any place that you would put **[EnableCors]**.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample22.cs)]

<span data-ttu-id="76cff-281">예를 들어 사용자 지정 CORS 정책 공급자가 구성 파일에서 설정을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-281">For example, a custom CORS policy provider could read the settings from a configuration file.</span></span>

<span data-ttu-id="76cff-282">특성을 사용 하는 대신 **ICorsPolicyProvider** 개체를 만드는 **ICorsPolicyProviderFactory** 개체를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-282">As an alternative to using attributes, you can register an **ICorsPolicyProviderFactory** object that creates **ICorsPolicyProvider** objects.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample23.cs)]

<span data-ttu-id="76cff-283">**ICorsPolicyProviderFactory**를 설정 하려면 시작 시 다음과 같이 **SetCorsPolicyProviderFactory** 확장 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-283">To set the **ICorsPolicyProviderFactory**, call the **SetCorsPolicyProviderFactory** extension method at startup, as follows:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample24.cs)]

## <a name="browser-support"></a><span data-ttu-id="76cff-284">브라우저 지원</span><span class="sxs-lookup"><span data-stu-id="76cff-284">Browser support</span></span>

<span data-ttu-id="76cff-285">Web API CORS 패키지는 서버 쪽 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-285">The Web API CORS package is a server-side technology.</span></span> <span data-ttu-id="76cff-286">사용자의 브라우저 에서도 CORS를 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-286">The user's browser also needs to support CORS.</span></span> <span data-ttu-id="76cff-287">다행히 모든 주요 브라우저의 현재 버전에는 [CORS에 대 한 지원이](http://caniuse.com/cors)포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76cff-287">Fortunately, the current versions of all major browsers include [support for CORS](http://caniuse.com/cors).</span></span>
