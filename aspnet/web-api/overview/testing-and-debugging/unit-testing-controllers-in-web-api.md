---
uid: web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
title: ASP.NET Web API 2의 유닛 테스트 컨트롤러 | Microsoft Docs
author: MikeWasson
description: 이 항목에서는 Web API 2의 유닛 테스트 컨트롤러에 대 한 몇 가지 특정 기술에 대해 설명 합니다. 이 항목을 읽기 전에 자습서 단위를 읽을 수 있습니다.
ms.author: riande
ms.date: 06/11/2014
ms.assetid: 43a6cce7-a3ef-42aa-ad06-90d36d49f098
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: cdb1700537021e276669de1a9e0330a62659746c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447005"
---
# <a name="unit-testing-controllers-in-aspnet-web-api-2"></a><span data-ttu-id="1d935-104">ASP.NET Web API 2의 유닛 테스트 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="1d935-104">Unit Testing Controllers in ASP.NET Web API 2</span></span>

<span data-ttu-id="1d935-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="1d935-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="1d935-106">이 항목에서는 Web API 2의 유닛 테스트 컨트롤러에 대 한 몇 가지 특정 기술에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-106">This topic describes some specific techniques for unit testing controllers in Web API 2.</span></span> <span data-ttu-id="1d935-107">이 항목을 읽기 전에 솔루션에 단위 테스트 프로젝트를 추가 하는 방법을 보여 주는 자습서 [단위 테스트 ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md)를 읽어 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-107">Before reading this topic, you might want to read the tutorial [Unit Testing ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md), which shows how to add a unit-test project to your solution.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="1d935-108">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="1d935-108">Software versions used in the tutorial</span></span>
>
> - [<span data-ttu-id="1d935-109">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="1d935-109">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="1d935-110">Web API 2</span><span class="sxs-lookup"><span data-stu-id="1d935-110">Web API 2</span></span>
> - <span data-ttu-id="1d935-111">[Moq](https://github.com/Moq) 4.5.30</span><span class="sxs-lookup"><span data-stu-id="1d935-111">[Moq](https://github.com/Moq) 4.5.30</span></span>

> [!NOTE]
> <span data-ttu-id="1d935-112">Moq를 사용 했지만 모든 모의 프레임 워크에 동일한 아이디어가 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-112">I used Moq, but the same idea applies to any mocking framework.</span></span> <span data-ttu-id="1d935-113">Moq 4.5.30 이상 버전은 Visual Studio 2017, Roslyn 및 .NET 4.5 이상 버전을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-113">Moq 4.5.30 (and later) supports Visual Studio 2017, Roslyn and .NET 4.5 and later versions.</span></span>

<span data-ttu-id="1d935-114">단위 테스트의 일반적인 패턴은 &quot;정렬&quot;입니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-114">A common pattern in unit tests is &quot;arrange-act-assert&quot;:</span></span>

- <span data-ttu-id="1d935-115">정렬: 테스트를 실행 하기 위한 모든 필수 구성 요소를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-115">Arrange: Set up any prerequisites for the test to run.</span></span>
- <span data-ttu-id="1d935-116">Act: 테스트를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-116">Act: Perform the test.</span></span>
- <span data-ttu-id="1d935-117">Assert: 테스트에 성공 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-117">Assert: Verify that the test succeeded.</span></span>

<span data-ttu-id="1d935-118">정렬 단계에서 모의 개체 또는 스텁 개체를 사용 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-118">In the arrange step, you will often use mock or stub objects.</span></span> <span data-ttu-id="1d935-119">이렇게 하면 종속성 수가 최소화 되므로 테스트는 한 가지 테스트를 중심으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-119">That minimizes the number of dependencies, so the test is focused on testing one thing.</span></span>

<span data-ttu-id="1d935-120">웹 API 컨트롤러에서 단위 테스트를 수행 해야 하는 몇 가지 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-120">Here are some things that you should unit test in your Web API controllers:</span></span>

- <span data-ttu-id="1d935-121">작업은 올바른 응답 유형을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-121">The action returns the correct type of response.</span></span>
- <span data-ttu-id="1d935-122">잘못 된 매개 변수는 올바른 오류 응답을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-122">Invalid parameters return the correct error response.</span></span>
- <span data-ttu-id="1d935-123">작업은 리포지토리 또는 서비스 계층에서 올바른 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-123">The action calls the correct method on the repository or service layer.</span></span>
- <span data-ttu-id="1d935-124">응답이 도메인 모델을 포함 하는 경우 모델 유형을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-124">If the response includes a domain model, verify the model type.</span></span>

<span data-ttu-id="1d935-125">이러한 항목은 몇 가지 일반적인 테스트 이지만 컨트롤러 구현에 따라 구체적입니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-125">These are some of the general things to test, but the specifics depend on your controller implementation.</span></span> <span data-ttu-id="1d935-126">특히 컨트롤러 작업에서 **HttpResponseMessage** 또는 **IHttpActionResult**를 반환 하는지 여부에 따라 큰 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-126">In particular, it makes a big difference whether your controller actions return **HttpResponseMessage** or **IHttpActionResult**.</span></span> <span data-ttu-id="1d935-127">이러한 결과 형식에 대 한 자세한 내용은 [Web Api 2의 작업 결과](../getting-started-with-aspnet-web-api/action-results.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="1d935-127">For more information about these result types, see [Action Results in Web Api 2](../getting-started-with-aspnet-web-api/action-results.md).</span></span>

## <a name="testing-actions-that-return-httpresponsemessage"></a><span data-ttu-id="1d935-128">HttpResponseMessage를 반환 하는 테스트 작업</span><span class="sxs-lookup"><span data-stu-id="1d935-128">Testing Actions that Return HttpResponseMessage</span></span>

<span data-ttu-id="1d935-129">다음은 작업에서 **HttpResponseMessage**를 반환 하는 컨트롤러의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-129">Here is an example of a controller whose actions return **HttpResponseMessage**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample1.cs)]

<span data-ttu-id="1d935-130">컨트롤러는 종속성 주입을 사용 하 여 `IProductRepository`를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-130">Notice the controller uses dependency injection to inject an `IProductRepository`.</span></span> <span data-ttu-id="1d935-131">이렇게 하면 모의 리포지토리를 주입할 수 있으므로 컨트롤러를 더 쉽게 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-131">That makes the controller more testable, because you can inject a mock repository.</span></span> <span data-ttu-id="1d935-132">다음 단위 테스트는 `Get` 메서드가 응답 본문에 `Product`를 기록 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-132">The following unit test verifies that the `Get` method writes a `Product` to the response body.</span></span> <span data-ttu-id="1d935-133">`repository` 모의 `IProductRepository`이라고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-133">Assume that `repository` is a mock `IProductRepository`.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample2.cs)]

<span data-ttu-id="1d935-134">컨트롤러에서 **요청** 및 **구성을** 설정 하는 것이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-134">It's important to set **Request** and **Configuration** on the controller.</span></span> <span data-ttu-id="1d935-135">그렇지 않으면 **Argumentnullexception** 또는 **InvalidOperationException**를 사용 하 여 테스트가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-135">Otherwise, the test will fail with an **ArgumentNullException** or **InvalidOperationException**.</span></span>

## <a name="testing-link-generation"></a><span data-ttu-id="1d935-136">테스트 링크 생성</span><span class="sxs-lookup"><span data-stu-id="1d935-136">Testing Link Generation</span></span>

<span data-ttu-id="1d935-137">`Post` 메서드는 **Urlhelper 링크** 를 호출 하 여 응답에 링크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-137">The `Post` method calls **UrlHelper.Link** to create links in the response.</span></span> <span data-ttu-id="1d935-138">이렇게 하려면 단위 테스트에서 약간의 설정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-138">This requires a little more setup in the unit test:</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample3.cs)]

<span data-ttu-id="1d935-139">**Urlhelper** 클래스는 요청 URL 및 경로 데이터를 요구 하므로 테스트에서 이러한 값을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-139">The **UrlHelper** class needs the request URL and route data, so the test has to set values for these.</span></span> <span data-ttu-id="1d935-140">또 다른 옵션은 모의 또는 스텁 **Urlhelper**입니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-140">Another option is mock or stub **UrlHelper**.</span></span> <span data-ttu-id="1d935-141">이 방법을 사용 하면 [ApiController](https://msdn.microsoft.com/library/system.web.http.apicontroller.url.aspx) 의 기본값을 고정 값을 반환 하는 모의 또는 스텁 버전으로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-141">With this approach, you replace the default value of [ApiController.Url](https://msdn.microsoft.com/library/system.web.http.apicontroller.url.aspx) with a mock or stub version that returns a fixed value.</span></span>

<span data-ttu-id="1d935-142">[Moq](https://github.com/Moq) 프레임 워크를 사용 하 여 테스트를 다시 작성해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-142">Let's rewrite the test using the [Moq](https://github.com/Moq) framework.</span></span> <span data-ttu-id="1d935-143">테스트 프로젝트에 `Moq` NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-143">Install the `Moq` NuGet package in the test project.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample4.cs)]

<span data-ttu-id="1d935-144">이 버전에서는 모의 **Urlhelper** 가 상수 문자열을 반환 하므로 경로 데이터를 설정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-144">In this version, you don't need to set up any route data, because the mock **UrlHelper** returns a constant string.</span></span>

## <a name="testing-actions-that-return-ihttpactionresult"></a><span data-ttu-id="1d935-145">IHttpActionResult를 반환 하는 테스트 작업</span><span class="sxs-lookup"><span data-stu-id="1d935-145">Testing Actions that Return IHttpActionResult</span></span>

<span data-ttu-id="1d935-146">Web API 2에서 컨트롤러 동작은 ASP.NET MVC의 **Actionresult** 와 유사한 **IHttpActionResult**를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-146">In Web API 2, a controller action can return **IHttpActionResult**, which is analogous to **ActionResult** in ASP.NET MVC.</span></span> <span data-ttu-id="1d935-147">**IHttpActionResult** 인터페이스는 HTTP 응답을 만들기 위한 명령 패턴을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-147">The **IHttpActionResult** interface defines a command pattern for creating HTTP responses.</span></span> <span data-ttu-id="1d935-148">컨트롤러는 직접 응답을 만드는 대신 **IHttpActionResult**를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-148">Instead of creating the response directly, the controller returns an **IHttpActionResult**.</span></span> <span data-ttu-id="1d935-149">나중에 파이프라인은 **IHttpActionResult** 를 호출 하 여 응답을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-149">Later, the pipeline invokes the **IHttpActionResult** to create the response.</span></span> <span data-ttu-id="1d935-150">**HttpResponseMessage**에 필요한 많은 설치를 건너뛸 수 있으므로이 방법을 사용 하면 단위 테스트를 보다 쉽게 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-150">This approach makes it easier to write unit tests, because you can skip a lot of the setup that is needed for **HttpResponseMessage**.</span></span>

<span data-ttu-id="1d935-151">작업에서 **IHttpActionResult**를 반환 하는 예제 컨트롤러는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-151">Here is an example controller whose actions return **IHttpActionResult**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample5.cs)]

<span data-ttu-id="1d935-152">이 예제에서는 **IHttpActionResult**를 사용 하는 몇 가지 일반적인 패턴을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-152">This example shows some common patterns using **IHttpActionResult**.</span></span> <span data-ttu-id="1d935-153">테스트를 단위 테스트 하는 방법을 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-153">Let's see how to unit test them.</span></span>

### <a name="action-returns-200-ok-with-a-response-body"></a><span data-ttu-id="1d935-154">작업은 응답 본문으로 200 (OK)를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-154">Action returns 200 (OK) with a response body</span></span>

<span data-ttu-id="1d935-155">`Get` 메서드는 제품이 있는 경우 `Ok(product)`를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-155">The `Get` method calls `Ok(product)` if the product is found.</span></span> <span data-ttu-id="1d935-156">단위 테스트에서 반환 형식이 **Oknegotiatedcontentresult** 이 고 반환 된 제품에 올바른 ID가 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-156">In the unit test, make sure the return type is **OkNegotiatedContentResult** and the returned product has the right ID.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample6.cs)]

<span data-ttu-id="1d935-157">단위 테스트는 작업 결과를 실행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-157">Notice that the unit test doesn't execute the action result.</span></span> <span data-ttu-id="1d935-158">작업 결과에서 HTTP 응답을 올바르게 생성 하는 것으로 간주할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-158">You can assume the action result creates the HTTP response correctly.</span></span> <span data-ttu-id="1d935-159">Web API 프레임 워크에는 고유한 단위 테스트가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-159">(That's why the Web API framework has its own unit tests!)</span></span>

### <a name="action-returns-404-not-found"></a><span data-ttu-id="1d935-160">작업에서 404 (찾을 수 없음)을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-160">Action returns 404 (Not Found)</span></span>

<span data-ttu-id="1d935-161">`Get` 메서드는 제품이 없는 경우 `NotFound()`를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-161">The `Get` method calls `NotFound()` if the product is not found.</span></span> <span data-ttu-id="1d935-162">이 경우 단위 테스트는 반환 형식이 **NotFoundResult**인지만 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-162">For this case, the unit test just checks if the return type is **NotFoundResult**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample7.cs)]

### <a name="action-returns-200-ok-with-no-response-body"></a><span data-ttu-id="1d935-163">작업은 응답 본문이 없는 200 (OK)를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-163">Action returns 200 (OK) with no response body</span></span>

<span data-ttu-id="1d935-164">`Delete` 메서드는 `Ok()`를 호출 하 여 빈 HTTP 200 응답을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-164">The `Delete` method calls `Ok()` to return an empty HTTP 200 response.</span></span> <span data-ttu-id="1d935-165">이전 예제와 마찬가지로 단위 테스트는 반환 형식 (이 경우 **Okresult**)을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-165">Like the previous example, the unit test checks the return type, in this case **OkResult**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample8.cs)]

### <a name="action-returns-201-created-with-a-location-header"></a><span data-ttu-id="1d935-166">작업은 Location 헤더를 사용 하 여 201 (Created)을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-166">Action returns 201 (Created) with a Location header</span></span>

<span data-ttu-id="1d935-167">`Post` 메서드는 `CreatedAtRoute`를 호출 하 여 Location 헤더에 URI가 있는 HTTP 201 응답을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-167">The `Post` method calls `CreatedAtRoute` to return an HTTP 201 response with a URI in the Location header.</span></span> <span data-ttu-id="1d935-168">단위 테스트에서 작업이 올바른 라우팅 값을 설정 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-168">In the unit test, verify that the action sets the correct routing values.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample9.cs)]

### <a name="action-returns-another-2xx-with-a-response-body"></a><span data-ttu-id="1d935-169">작업은 응답 본문이 있는 다른 2xx를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-169">Action returns another 2xx with a response body</span></span>

<span data-ttu-id="1d935-170">`Put` 메서드는 `Content`를 호출 하 여 응답 본문이 포함 된 HTTP 202 (수락) 응답을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-170">The `Put` method calls `Content` to return an HTTP 202 (Accepted) response with a response body.</span></span> <span data-ttu-id="1d935-171">이 경우 200 (OK)을 반환 하는 것과 유사 하지만 단위 테스트 에서도 상태 코드를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d935-171">This case is similar to returning 200 (OK), but the unit test should also check the status code.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample10.cs)]

## <a name="additional-resources"></a><span data-ttu-id="1d935-172">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1d935-172">Additional Resources</span></span>

- [<span data-ttu-id="1d935-173">유닛 테스트 ASP.NET Web API 2 Entity Framework 모의</span><span class="sxs-lookup"><span data-stu-id="1d935-173">Mocking Entity Framework when Unit Testing ASP.NET Web API 2</span></span>](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)
- <span data-ttu-id="1d935-174">[ASP.NET Web API 서비스에 대 한 테스트 작성](https://blogs.msdn.com/b/youssefm/archive/2013/01/28/writing-tests-for-an-asp-net-webapi-service.aspx) (Youssef Moussaoui의 블로그 게시물).</span><span class="sxs-lookup"><span data-stu-id="1d935-174">[Writing tests for an ASP.NET Web API service](https://blogs.msdn.com/b/youssefm/archive/2013/01/28/writing-tests-for-an-asp-net-webapi-service.aspx) (blog post by Youssef Moussaoui).</span></span>
- [<span data-ttu-id="1d935-175">경로 디버거를 사용 하 여 ASP.NET Web API 디버깅</span><span class="sxs-lookup"><span data-stu-id="1d935-175">Debugging ASP.NET Web API with Route Debugger</span></span>](https://blogs.msdn.com/b/webdev/archive/2013/04/04/debugging-asp-net-web-api-with-route-debugger.aspx)
