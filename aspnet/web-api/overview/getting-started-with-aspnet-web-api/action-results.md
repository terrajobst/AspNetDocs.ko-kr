---
uid: web-api/overview/getting-started-with-aspnet-web-api/action-results
title: Web API 2-ASP.NET 4.x의 작업 결과
author: MikeWasson
description: ASP.NET Web API 컨트롤러 작업의 반환 값을 ASP.NET 4.x의 HTTP 응답 메시지로 변환 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: 2fc4797c-38ef-4cc7-926c-ca431c4739e8
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/action-results
msc.type: authoredcontent
ms.openlocfilehash: f00ac0db453053e53d6d6942dd1557b409f4167b
ms.sourcegitcommit: 4b324a11131e38f920126066b94ff478aa9927f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70985844"
---
# <a name="action-results-in-web-api-2"></a><span data-ttu-id="60bb4-103">Web API 2의 작업 결과</span><span class="sxs-lookup"><span data-stu-id="60bb4-103">Action Results in Web API 2</span></span>

[!INCLUDE[](~/includes/coreWebAPI.md)]

<span data-ttu-id="60bb4-104">이 항목에서는 ASP.NET Web API 컨트롤러 작업의 반환 값을 HTTP 응답 메시지로 변환 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-104">This topic describes how ASP.NET Web API converts the return value from a controller action into an HTTP response message.</span></span>

<span data-ttu-id="60bb4-105">Web API 컨트롤러 작업은 다음 중 하나를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-105">A Web API controller action can return any of the following:</span></span>

1. <span data-ttu-id="60bb4-106">void</span><span class="sxs-lookup"><span data-stu-id="60bb4-106">void</span></span>
2. <span data-ttu-id="60bb4-107">**HttpResponseMessage**</span><span class="sxs-lookup"><span data-stu-id="60bb4-107">**HttpResponseMessage**</span></span>
3. <span data-ttu-id="60bb4-108">**IHttpActionResult**</span><span class="sxs-lookup"><span data-stu-id="60bb4-108">**IHttpActionResult**</span></span>
4. <span data-ttu-id="60bb4-109">다른 형식</span><span class="sxs-lookup"><span data-stu-id="60bb4-109">Some other type</span></span>

<span data-ttu-id="60bb4-110">웹 API는 반환 되는 방법에 따라 다른 메커니즘을 사용 하 여 HTTP 응답을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-110">Depending on which of these is returned, Web API uses a different mechanism to create the HTTP response.</span></span>

| <span data-ttu-id="60bb4-111">반환 형식</span><span class="sxs-lookup"><span data-stu-id="60bb4-111">Return type</span></span> | <span data-ttu-id="60bb4-112">Web API에서 응답을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="60bb4-112">How Web API creates the response</span></span> |
| --- | --- |
| <span data-ttu-id="60bb4-113">void</span><span class="sxs-lookup"><span data-stu-id="60bb4-113">void</span></span> | <span data-ttu-id="60bb4-114">빈 204 반환 (내용 없음)</span><span class="sxs-lookup"><span data-stu-id="60bb4-114">Return empty 204 (No Content)</span></span> |
| <span data-ttu-id="60bb4-115">**HttpResponseMessage**</span><span class="sxs-lookup"><span data-stu-id="60bb4-115">**HttpResponseMessage**</span></span> | <span data-ttu-id="60bb4-116">HTTP 응답 메시지로 직접 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-116">Convert directly to an HTTP response message.</span></span> |
| <span data-ttu-id="60bb4-117">**IHttpActionResult**</span><span class="sxs-lookup"><span data-stu-id="60bb4-117">**IHttpActionResult**</span></span> | <span data-ttu-id="60bb4-118">**ExecuteAsync** 를 호출 하 여 **HttpResponseMessage**를 만든 다음 HTTP 응답 메시지로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-118">Call **ExecuteAsync** to create an **HttpResponseMessage**, then convert to an HTTP response message.</span></span> |
| <span data-ttu-id="60bb4-119">기타 형식</span><span class="sxs-lookup"><span data-stu-id="60bb4-119">Other type</span></span> | <span data-ttu-id="60bb4-120">Serialize 된 반환 값을 응답 본문에 씁니다. 200 (OK)을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-120">Write the serialized return value into the response body; return 200 (OK).</span></span> |

<span data-ttu-id="60bb4-121">이 항목의 나머지 부분에서는 각 옵션에 대해 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-121">The rest of this topic describes each option in more detail.</span></span>

## <a name="void"></a><span data-ttu-id="60bb4-122">void</span><span class="sxs-lookup"><span data-stu-id="60bb4-122">void</span></span>

<span data-ttu-id="60bb4-123">반환 형식이 `void`이면 웹 API는 상태 코드 204 (콘텐츠 없음)가 포함 된 빈 HTTP 응답을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-123">If the return type is `void`, Web API simply returns an empty HTTP response with status code 204 (No Content).</span></span>

<span data-ttu-id="60bb4-124">컨트롤러 예:</span><span class="sxs-lookup"><span data-stu-id="60bb4-124">Example controller:</span></span>

[!code-csharp[Main](action-results/samples/sample1.cs)]

<span data-ttu-id="60bb4-125">HTTP 응답:</span><span class="sxs-lookup"><span data-stu-id="60bb4-125">HTTP response:</span></span>

[!code-console[Main](action-results/samples/sample2.cmd)]

## <a name="httpresponsemessage"></a><span data-ttu-id="60bb4-126">HttpResponseMessage</span><span class="sxs-lookup"><span data-stu-id="60bb4-126">HttpResponseMessage</span></span>

<span data-ttu-id="60bb4-127">작업에서 [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx)를 반환 하는 경우 Web API는 **HttpResponseMessage** 개체의 속성을 사용 하 여 응답을 채우도록 반환 값을 HTTP 응답 메시지로 직접 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-127">If the action returns an [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx), Web API converts the return value directly into an HTTP response message, using the properties of the **HttpResponseMessage** object to populate the response.</span></span>

<span data-ttu-id="60bb4-128">이 옵션을 사용 하면 응답 메시지를 매우 효과적으로 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-128">This option gives you a lot of control over the response message.</span></span> <span data-ttu-id="60bb4-129">예를 들어 다음 컨트롤러 작업은 Cache-control 헤더를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-129">For example, the following controller action sets the Cache-Control header.</span></span>

[!code-csharp[Main](action-results/samples/sample3.cs)]

<span data-ttu-id="60bb4-130">응답:</span><span class="sxs-lookup"><span data-stu-id="60bb4-130">Response:</span></span>

[!code-console[Main](action-results/samples/sample4.cmd?highlight=2)]

<span data-ttu-id="60bb4-131">도메인 모델을 **CreateResponse** 메서드에 전달 하는 경우 Web API는 [미디어 포맷터](../formats-and-model-binding/media-formatters.md) 를 사용 하 여 serialize 된 모델을 응답 본문에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-131">If you pass a domain model to the **CreateResponse** method, Web API uses a [media formatter](../formats-and-model-binding/media-formatters.md) to write the serialized model into the response body.</span></span>

[!code-csharp[Main](action-results/samples/sample5.cs)]

<span data-ttu-id="60bb4-132">Web API는 요청에 Accept 헤더를 사용 하 여 포맷터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-132">Web API uses the Accept header in the request to choose the formatter.</span></span> <span data-ttu-id="60bb4-133">자세한 내용은 [콘텐츠 협상](../formats-and-model-binding/content-negotiation.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="60bb4-133">For more information, see [Content Negotiation](../formats-and-model-binding/content-negotiation.md).</span></span>

## <a name="ihttpactionresult"></a><span data-ttu-id="60bb4-134">IHttpActionResult</span><span class="sxs-lookup"><span data-stu-id="60bb4-134">IHttpActionResult</span></span>

<span data-ttu-id="60bb4-135">**IHttpActionResult** 인터페이스는 Web API 2에서 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-135">The **IHttpActionResult** interface was introduced in Web API 2.</span></span> <span data-ttu-id="60bb4-136">기본적으로 **HttpResponseMessage** 팩터리를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-136">Essentially, it defines an **HttpResponseMessage** factory.</span></span> <span data-ttu-id="60bb4-137">**IHttpActionResult** 인터페이스를 사용할 경우의 몇 가지 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-137">Here are some advantages of using the **IHttpActionResult** interface:</span></span>

- <span data-ttu-id="60bb4-138">컨트롤러의 [유닛 테스트](../testing-and-debugging/unit-testing-controllers-in-web-api.md) 를 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-138">Simplifies [unit testing](../testing-and-debugging/unit-testing-controllers-in-web-api.md) your controllers.</span></span>
- <span data-ttu-id="60bb4-139">HTTP 응답을 만들기 위한 공통 논리를 개별 클래스로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-139">Moves common logic for creating HTTP responses into separate classes.</span></span>
- <span data-ttu-id="60bb4-140">응답 생성에 대 한 하위 수준 세부 정보를 숨겨 컨트롤러 작업의 의도를 명확 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-140">Makes the intent of the controller action clearer, by hiding the low-level details of constructing the response.</span></span>

<span data-ttu-id="60bb4-141">**IHttpActionResult** 에는 **HttpResponseMessage** 인스턴스를 비동기식으로 만드는 단일 메서드인 **ExecuteAsync**이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-141">**IHttpActionResult** contains a single method, **ExecuteAsync**, which asynchronously creates an **HttpResponseMessage** instance.</span></span>

[!code-csharp[Main](action-results/samples/sample6.cs)]

<span data-ttu-id="60bb4-142">컨트롤러 작업에서 **IHttpActionResult**를 반환 하는 경우 Web API는 **ExecuteAsync** 메서드를 호출 하 여 **HttpResponseMessage**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-142">If a controller action returns an **IHttpActionResult**, Web API calls the **ExecuteAsync** method to create an **HttpResponseMessage**.</span></span> <span data-ttu-id="60bb4-143">그런 다음 **HttpResponseMessage** 를 HTTP 응답 메시지로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-143">Then it converts the **HttpResponseMessage** into an HTTP response message.</span></span>

<span data-ttu-id="60bb4-144">다음은 일반 텍스트 응답을 만드는 간단한 **IHttpActionResult** 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-144">Here is a simple implementation of **IHttpActionResult** that creates a plain text response:</span></span>

[!code-csharp[Main](action-results/samples/sample7.cs)]

<span data-ttu-id="60bb4-145">컨트롤러 작업 예:</span><span class="sxs-lookup"><span data-stu-id="60bb4-145">Example controller action:</span></span>

[!code-csharp[Main](action-results/samples/sample8.cs)]

<span data-ttu-id="60bb4-146">응답:</span><span class="sxs-lookup"><span data-stu-id="60bb4-146">Response:</span></span>

[!code-console[Main](action-results/samples/sample9.cmd)]

<span data-ttu-id="60bb4-147">일반적으로 IHttpActionResult 네임 스페이스에 정의 된 구현을 사용 **[합니다.](https://msdn.microsoft.com/library/system.web.http.results.aspx)**</span><span class="sxs-lookup"><span data-stu-id="60bb4-147">More often, you use the **IHttpActionResult** implementations defined in the **[System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)** namespace.</span></span> <span data-ttu-id="60bb4-148">**ApiController** 클래스는 이러한 기본 제공 작업 결과를 반환 하는 도우미 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-148">The **ApiController** class defines helper methods that return these built-in action results.</span></span>

<span data-ttu-id="60bb4-149">다음 예에서는 요청이 기존 제품 ID와 일치 하지 않는 경우 컨트롤러가 [ApiController](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx) 를 호출 하 여 404 (찾을 수 없음) 응답을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-149">In the following example, if the request does not match an existing product ID, the controller calls [ApiController.NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx) to create a 404 (Not Found) response.</span></span> <span data-ttu-id="60bb4-150">그렇지 않으면 컨트롤러가 ApiController를 호출 하 여 제품을 포함 하는 200 (OK) 응답을 만듭니다 [.](https://msdn.microsoft.com/library/dn314591.aspx)</span><span class="sxs-lookup"><span data-stu-id="60bb4-150">Otherwise, the controller calls [ApiController.OK](https://msdn.microsoft.com/library/dn314591.aspx), which creates a 200 (OK) response that contains the product.</span></span>

[!code-csharp[Main](action-results/samples/sample10.cs)]

## <a name="other-return-types"></a><span data-ttu-id="60bb4-151">기타 반환 형식</span><span class="sxs-lookup"><span data-stu-id="60bb4-151">Other Return Types</span></span>

<span data-ttu-id="60bb4-152">다른 모든 반환 형식에 대해 Web API는 [미디어 포맷터](../formats-and-model-binding/media-formatters.md) 를 사용 하 여 반환 값을 직렬화 합니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-152">For all other return types, Web API uses a [media formatter](../formats-and-model-binding/media-formatters.md) to serialize the return value.</span></span> <span data-ttu-id="60bb4-153">Web API는 serialize 된 값을 응답 본문에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-153">Web API writes the serialized value into the response body.</span></span> <span data-ttu-id="60bb4-154">응답 상태 코드는 200 (정상)입니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-154">The response status code is 200 (OK).</span></span>

[!code-csharp[Main](action-results/samples/sample11.cs)]

<span data-ttu-id="60bb4-155">이 방법의 단점은 404와 같은 오류 코드를 직접 반환할 수 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-155">A disadvantage of this approach is that you cannot directly return an error code, such as 404.</span></span> <span data-ttu-id="60bb4-156">그러나 오류 코드에 대해 **HttpResponseException** 을 throw 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-156">However, you can throw an **HttpResponseException** for error codes.</span></span> <span data-ttu-id="60bb4-157">자세한 내용은 [ASP.NET Web API의 예외 처리](../error-handling/exception-handling.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="60bb4-157">For more information, see [Exception Handling in ASP.NET Web API](../error-handling/exception-handling.md).</span></span>

<span data-ttu-id="60bb4-158">Web API는 요청에 Accept 헤더를 사용 하 여 포맷터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="60bb4-158">Web API uses the Accept header in the request to choose the formatter.</span></span> <span data-ttu-id="60bb4-159">자세한 내용은 [콘텐츠 협상](../formats-and-model-binding/content-negotiation.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="60bb4-159">For more information, see [Content Negotiation](../formats-and-model-binding/content-negotiation.md).</span></span>

<span data-ttu-id="60bb4-160">요청 예</span><span class="sxs-lookup"><span data-stu-id="60bb4-160">Example request</span></span>

[!code-console[Main](action-results/samples/sample12.cmd)]

<span data-ttu-id="60bb4-161">예제 응답</span><span class="sxs-lookup"><span data-stu-id="60bb4-161">Example response</span></span>

[!code-console[Main](action-results/samples/sample13.cmd)]
