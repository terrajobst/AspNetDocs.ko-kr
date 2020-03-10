---
uid: web-api/overview/formats-and-model-binding/content-negotiation
title: ASP.NET Web API의 콘텐츠 협상-ASP.NET 4.x
author: MikeWasson
description: ASP.NET Web API에서 ASP.NET 4.x에 대 한 HTTP 콘텐츠 협상을 구현 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 05/20/2012
ms.custom: seoapril2019
ms.assetid: 0dd51b30-bf5a-419f-a1b7-2817ccca3c7d
msc.legacyurl: /web-api/overview/formats-and-model-binding/content-negotiation
msc.type: authoredcontent
ms.openlocfilehash: cb6668ff6de276d3778ce11f27ce597d8bf1f9c7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504659"
---
# <a name="content-negotiation-in-aspnet-web-api"></a><span data-ttu-id="cd39c-103">ASP.NET Web API의 콘텐츠 협상</span><span class="sxs-lookup"><span data-stu-id="cd39c-103">Content Negotiation in ASP.NET Web API</span></span>

<span data-ttu-id="cd39c-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="cd39c-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="cd39c-105">이 문서에서는 ASP.NET Web API ASP.NET 4.x에 대해 콘텐츠 협상을 구현 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-105">This article describes how ASP.NET Web API implements content negotiation for ASP.NET 4.x.</span></span>

<span data-ttu-id="cd39c-106">HTTP 사양 (RFC 2616)은 "여러 표현을 사용할 수 있는 경우 지정 된 응답에 대 한 최상의 표현을 선택 하는 프로세스"로 콘텐츠 협상을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-106">The HTTP specification (RFC 2616) defines content negotiation as "the process of selecting the best representation for a given response when there are multiple representations available."</span></span> <span data-ttu-id="cd39c-107">HTTP의 콘텐츠 협상에 대 한 기본 메커니즘은 다음 요청 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-107">The primary mechanism for content negotiation in HTTP are these request headers:</span></span>

- <span data-ttu-id="cd39c-108">**수락:** 응답에 허용 되는 미디어 유형 (예: "application/json" "application/xml") 또는 &quot;application/vnd와 같은 사용자 지정 미디어 유형입니다. 예 + xml&quot;</span><span class="sxs-lookup"><span data-stu-id="cd39c-108">**Accept:** Which media types are acceptable for the response, such as "application/json," "application/xml," or a custom media type such as &quot;application/vnd.example+xml&quot;</span></span>
- <span data-ttu-id="cd39c-109">**허용 문자 집합:** UTF-8 또는 ISO 8859-1 같은 문자 집합을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-109">**Accept-Charset:** Which character sets are acceptable, such as UTF-8 or ISO 8859-1.</span></span>
- <span data-ttu-id="cd39c-110">**수락-인코딩:** Gzip과 같은 허용 되는 콘텐츠 인코딩</span><span class="sxs-lookup"><span data-stu-id="cd39c-110">**Accept-Encoding:** Which content encodings are acceptable, such as gzip.</span></span>
- <span data-ttu-id="cd39c-111">**수락 언어:** "En-us"와 같은 기본 자연 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-111">**Accept-Language:** The preferred natural language, such as "en-us".</span></span>

<span data-ttu-id="cd39c-112">서버는 HTTP 요청의 다른 부분을 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-112">The server can also look at other portions of the HTTP request.</span></span> <span data-ttu-id="cd39c-113">예를 들어 요청에 X로 요청 된 헤더 (AJAX 요청을 나타냄)가 포함 된 경우 Accept 헤더가 없으면 서버는 기본적으로 JSON으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-113">For example, if the request contains an X-Requested-With header, indicating an AJAX request, the server might default to JSON if there is no Accept header.</span></span>

<span data-ttu-id="cd39c-114">이 문서에서는 Web API가 허용 및 허용 문자 집합 헤더를 사용 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-114">In this article, we'll look at how Web API uses the Accept and Accept-Charset headers.</span></span> <span data-ttu-id="cd39c-115">(현재는 허용 인코딩 또는 수락 언어를 기본적으로 지원 하지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="cd39c-115">(At this time, there is no built-in support for Accept-Encoding or Accept-Language.)</span></span>

## <a name="serialization"></a><span data-ttu-id="cd39c-116">직렬화</span><span class="sxs-lookup"><span data-stu-id="cd39c-116">Serialization</span></span>

<span data-ttu-id="cd39c-117">Web API 컨트롤러에서 CLR 형식으로 리소스를 반환 하는 경우 파이프라인은 반환 값을 직렬화 하 고 HTTP 응답 본문에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-117">If a Web API controller returns a resource as CLR type, the pipeline serializes the return value and writes it into the HTTP response body.</span></span>

<span data-ttu-id="cd39c-118">예를 들어 다음 컨트롤러 작업을 고려 하십시오.</span><span class="sxs-lookup"><span data-stu-id="cd39c-118">For example, consider the following controller action:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample1.cs)]

<span data-ttu-id="cd39c-119">클라이언트에서이 HTTP 요청을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-119">A client might send this HTTP request:</span></span>

[!code-console[Main](content-negotiation/samples/sample2.cmd)]

<span data-ttu-id="cd39c-120">응답으로 서버에서 다음을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-120">In response, the server might send:</span></span>

[!code-console[Main](content-negotiation/samples/sample3.cmd)]

<span data-ttu-id="cd39c-121">이 예에서 클라이언트는 JSON, Javascript 또는 "모든 항목" (\*/\*)을 요청 했습니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-121">In this example, the client requested either JSON, Javascript, or "anything" (\*/\*).</span></span> <span data-ttu-id="cd39c-122">서버가 `Product` 개체의 JSON 표현으로 응답 했습니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-122">The server responded with a JSON representation of the `Product` object.</span></span> <span data-ttu-id="cd39c-123">응답의 Content-type 헤더는 &quot;application/json&quot;로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-123">Notice that the Content-Type header in the response is set to &quot;application/json&quot;.</span></span>

<span data-ttu-id="cd39c-124">컨트롤러는 **HttpResponseMessage** 개체를 반환할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-124">A controller can also return an **HttpResponseMessage** object.</span></span> <span data-ttu-id="cd39c-125">응답 본문에 대 한 CLR 개체를 지정 하려면 **CreateResponse** 확장 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-125">To specify a CLR object for the response body, call the **CreateResponse** extension method:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample4.cs)]

<span data-ttu-id="cd39c-126">이 옵션을 사용 하면 응답의 세부 정보를 더 세밀 하 게 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-126">This option gives you more control over the details of the response.</span></span> <span data-ttu-id="cd39c-127">상태 코드를 설정 하 고 HTTP 헤더를 추가 하는 등의 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-127">You can set the status code, add HTTP headers, and so forth.</span></span>

<span data-ttu-id="cd39c-128">리소스를 serialize 하는 개체를 *미디어 포맷터*라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-128">The object that serializes the resource is called a *media formatter*.</span></span> <span data-ttu-id="cd39c-129">미디어 포맷터는 **MediaTypeFormatter** 클래스에서 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-129">Media formatters derive from the **MediaTypeFormatter** class.</span></span> <span data-ttu-id="cd39c-130">Web API는 XML 및 JSON에 대 한 미디어 포맷터를 제공 하며, 다른 미디어 유형을 지원 하기 위해 사용자 지정 포맷터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-130">Web API provides media formatters for XML and JSON, and you can create custom formatters to support other media types.</span></span> <span data-ttu-id="cd39c-131">사용자 지정 포맷터를 작성 하는 방법에 대 한 자세한 내용은 [미디어 포맷터](media-formatters.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="cd39c-131">For information about writing a custom formatter, see [Media Formatters](media-formatters.md).</span></span>

## <a name="how-content-negotiation-works"></a><span data-ttu-id="cd39c-132">콘텐츠 협상의 작동 방식</span><span class="sxs-lookup"><span data-stu-id="cd39c-132">How Content Negotiation Works</span></span>

<span data-ttu-id="cd39c-133">먼저 파이프라인은 **Httpconfiguration** 개체에서 **IContentNegotiator** 서비스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-133">First, the pipeline gets the **IContentNegotiator** service from the **HttpConfiguration** object.</span></span> <span data-ttu-id="cd39c-134">또한 **Httpconfiguration. 포맷터** 컬렉션에서 미디어 포맷터 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-134">It also gets the list of media formatters from the **HttpConfiguration.Formatters** collection.</span></span>

<span data-ttu-id="cd39c-135">다음으로 파이프라인은 **IContentNegotiator**를 호출 하 고 다음을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-135">Next, the pipeline calls **IContentNegotiator.Negotiate**, passing in:</span></span>

- <span data-ttu-id="cd39c-136">Serialize 할 개체의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-136">The type of object to serialize</span></span>
- <span data-ttu-id="cd39c-137">미디어 포맷터의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-137">The collection of media formatters</span></span>
- <span data-ttu-id="cd39c-138">HTTP 요청</span><span class="sxs-lookup"><span data-stu-id="cd39c-138">The HTTP request</span></span>

<span data-ttu-id="cd39c-139">**Negotiate** 메서드는 다음 두 가지 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-139">The **Negotiate** method returns two pieces of information:</span></span>

- <span data-ttu-id="cd39c-140">사용할 포맷터</span><span class="sxs-lookup"><span data-stu-id="cd39c-140">Which formatter to use</span></span>
- <span data-ttu-id="cd39c-141">응답의 미디어 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-141">The media type for the response</span></span>

<span data-ttu-id="cd39c-142">포맷터를 찾을 수 없는 경우 **Negotiate** 메서드는 **null**을 반환 하 고 클라이언트는 HTTP 오류 406 (허용 되지 않음)을 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-142">If no formatter is found, the **Negotiate** method returns **null**, and the client receives HTTP error 406 (Not Acceptable).</span></span>

<span data-ttu-id="cd39c-143">다음 코드는 컨트롤러에서 직접 콘텐츠 협상을 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-143">The following code shows how a controller can directly invoke content negotiation:</span></span>

[!code-csharp[Main](content-negotiation/samples/sample5.cs)]

<span data-ttu-id="cd39c-144">이 코드는 파이프라인이 자동으로 수행 하는 작업에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-144">This code is equivalent to the what the pipeline does automatically.</span></span>

## <a name="default-content-negotiator"></a><span data-ttu-id="cd39c-145">기본 콘텐츠 Negotiator</span><span class="sxs-lookup"><span data-stu-id="cd39c-145">Default Content Negotiator</span></span>

<span data-ttu-id="cd39c-146">**Defaultcontentnegotiator** 클래스는 기본 구현을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-146">The **DefaultContentNegotiator** class provides the default implementation of **IContentNegotiator**.</span></span> <span data-ttu-id="cd39c-147">여러 가지 조건을 사용 하 여 포맷터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-147">It uses several criteria to select a formatter.</span></span>

<span data-ttu-id="cd39c-148">먼저 포맷터가 형식을 직렬화 할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-148">First, the formatter must be able to serialize the type.</span></span> <span data-ttu-id="cd39c-149">이는 **MediaTypeFormatter**를 호출 하 여 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-149">This is verified by calling **MediaTypeFormatter.CanWriteType**.</span></span>

<span data-ttu-id="cd39c-150">그런 다음, 콘텐츠 negotiator 각 포맷터를 살펴보고 HTTP 요청과 얼마나 잘 일치 하는지 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-150">Next, the content negotiator looks at each formatter and evaluates how well it matches the HTTP request.</span></span> <span data-ttu-id="cd39c-151">일치를 평가 하기 위해 콘텐츠 negotiator 포맷터에서 다음 두 가지를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-151">To evaluate the match, the content negotiator looks at two things on the formatter:</span></span>

- <span data-ttu-id="cd39c-152">**SupportedMediaTypes** 컬렉션에는 지원 되는 미디어 형식 목록이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-152">The **SupportedMediaTypes** collection, which contains a list of supported media types.</span></span> <span data-ttu-id="cd39c-153">콘텐츠 negotiator이 목록을 요청 수락 헤더와 일치 시 키 려 고 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-153">The content negotiator tries to match this list against the request Accept header.</span></span> <span data-ttu-id="cd39c-154">Accept 헤더는 범위를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-154">Note that the Accept header can include ranges.</span></span> <span data-ttu-id="cd39c-155">예를 들어 "텍스트/일반"은 텍스트/\* 또는 \*/\*일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-155">For example, "text/plain" is a match for text/\* or \*/\*.</span></span>
- <span data-ttu-id="cd39c-156">**MediaTypeMapping** 개체의 목록을 포함 하는 **MediaTypeMappings** 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-156">The **MediaTypeMappings** collection, which contains a list of **MediaTypeMapping** objects.</span></span> <span data-ttu-id="cd39c-157">**MediaTypeMapping** 클래스는 HTTP 요청을 미디어 유형과 일치 시키는 일반적인 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-157">The **MediaTypeMapping** class provides a generic way to match HTTP requests with media types.</span></span> <span data-ttu-id="cd39c-158">예를 들어 사용자 지정 HTTP 헤더를 특정 미디어 형식에 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-158">For example, it could map a custom HTTP header to a particular media type.</span></span>

<span data-ttu-id="cd39c-159">일치 하는 항목이 여러 개인 경우 가장 높은 품질의 일치 항목이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-159">If there are multiple matches, the match with the highest quality factor wins.</span></span> <span data-ttu-id="cd39c-160">다음은 그 예입니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-160">For example:</span></span>

[!code-console[Main](content-negotiation/samples/sample6.cmd)]

<span data-ttu-id="cd39c-161">이 예제에서 application/json은 1.0의 암시 된 품질을 가지 므로 application/xml 보다 우선적으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-161">In this example, application/json has an implied quality factor of 1.0, so it is preferred over application/xml.</span></span>

<span data-ttu-id="cd39c-162">일치 하는 항목이 없는 경우 콘텐츠 negotiator 요청 본문의 미디어 형식 (있는 경우)을 찾으려고 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-162">If no matches are found, the content negotiator tries to match on the media type of the request body, if any.</span></span> <span data-ttu-id="cd39c-163">예를 들어 요청에 JSON 데이터가 포함 된 경우 콘텐츠 negotiator JSON 포맷터를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-163">For example, if the request contains JSON data, the content negotiator looks for a JSON formatter.</span></span>

<span data-ttu-id="cd39c-164">여전히 일치 하는 항목이 없으면 콘텐츠를 serialize 할 수 있는 첫 번째 포맷터만 선택 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-164">If there are still no matches, the content negotiator simply picks the first formatter that can serialize the type.</span></span>

## <a name="selecting-a-character-encoding"></a><span data-ttu-id="cd39c-165">문자 인코딩 선택</span><span class="sxs-lookup"><span data-stu-id="cd39c-165">Selecting a Character Encoding</span></span>

<span data-ttu-id="cd39c-166">포맷터를 선택 하 고 나면 content negotiator는 포맷터의 **supportedencodings** 속성을 확인 하 고 요청 (있는 경우)의 허용 되는 문자 집합 헤더와 일치 하 여 가장 적합 한 문자 인코딩을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd39c-166">After a formatter is selected, the content negotiator chooses the best character encoding by looking at the **SupportedEncodings** property on the formatter, and matching it against the Accept-Charset header in the request (if any).</span></span>
