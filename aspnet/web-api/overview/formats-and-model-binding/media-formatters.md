---
uid: web-api/overview/formats-and-model-binding/media-formatters
title: ASP.NET Web API 2-ASP.NET 4. x의 미디어 포맷터
author: MikeWasson
description: ASP.NET 4.x의 ASP.NET Web API에서 추가 미디어 형식을 지 원하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: 4c56f64a-086a-44ce-99c2-4c69604cd7fd
msc.legacyurl: /web-api/overview/formats-and-model-binding/media-formatters
msc.type: authoredcontent
ms.openlocfilehash: da0c566dad302054d7d0a6435e4c6df178c64772
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448943"
---
# <a name="media-formatters-in-aspnet-web-api-2"></a><span data-ttu-id="fd8d1-103">ASP.NET Web API 2의 미디어 포맷터</span><span class="sxs-lookup"><span data-stu-id="fd8d1-103">Media Formatters in ASP.NET Web API 2</span></span>

<span data-ttu-id="fd8d1-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="fd8d1-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="fd8d1-105">이 자습서에서는 ASP.NET Web API에서 추가 미디어 형식을 지 원하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-105">This tutorial shows how to support additional media formats in ASP.NET Web API.</span></span>

## <a name="internet-media-types"></a><span data-ttu-id="fd8d1-106">인터넷 미디어 유형</span><span class="sxs-lookup"><span data-stu-id="fd8d1-106">Internet Media Types</span></span>

<span data-ttu-id="fd8d1-107">MIME 형식이 라고도 하는 미디어 유형은 데이터의 형식을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-107">A media type, also called a MIME type, identifies the format of a piece of data.</span></span> <span data-ttu-id="fd8d1-108">HTTP에서 미디어 유형은 메시지 본문의 형식을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-108">In HTTP, media types describe the format of the message body.</span></span> <span data-ttu-id="fd8d1-109">미디어 유형은 형식 및 하위 형식 이라는 두 개의 문자열로 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-109">A media type consists of two strings, a type and a subtype.</span></span> <span data-ttu-id="fd8d1-110">예를 들어 다음과 같은 가치를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-110">For example:</span></span>

- <span data-ttu-id="fd8d1-111">text/html</span><span class="sxs-lookup"><span data-stu-id="fd8d1-111">text/html</span></span>
- <span data-ttu-id="fd8d1-112">image/png</span><span class="sxs-lookup"><span data-stu-id="fd8d1-112">image/png</span></span>
- <span data-ttu-id="fd8d1-113">application/json</span><span class="sxs-lookup"><span data-stu-id="fd8d1-113">application/json</span></span>

<span data-ttu-id="fd8d1-114">HTTP 메시지에 엔터티 본문이 포함 되어 있는 경우 Content-type 헤더는 메시지 본문의 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-114">When an HTTP message contains an entity-body, the Content-Type header specifies the format of the message body.</span></span> <span data-ttu-id="fd8d1-115">메시지 본문의 내용을 구문 분석 하는 방법을 수신자에 게 알립니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-115">This tells the receiver how to parse the contents of the message body.</span></span>

<span data-ttu-id="fd8d1-116">예를 들어 HTTP 응답이 PNG 이미지를 포함 하는 경우 응답에는 다음과 같은 헤더가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-116">For example, if an HTTP response contains a PNG image, the response might have the following headers.</span></span>

[!code-console[Main](media-formatters/samples/sample1.cmd)]

<span data-ttu-id="fd8d1-117">클라이언트는 요청 메시지를 보낼 때 Accept 헤더를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-117">When the client sends a request message, it can include an Accept header.</span></span> <span data-ttu-id="fd8d1-118">Accept 헤더는 클라이언트가 서버에서 원하는 미디어 유형을 서버에 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-118">The Accept header tells the server which media type(s) the client wants from the server.</span></span> <span data-ttu-id="fd8d1-119">예를 들어 다음과 같은 가치를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-119">For example:</span></span>

[!code-console[Main](media-formatters/samples/sample2.cmd)]

<span data-ttu-id="fd8d1-120">이 헤더는 클라이언트가 HTML, XHTML 또는 XML 중 하나를 원하는 지를 서버에 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-120">This header tells the server that the client wants either HTML, XHTML, or XML.</span></span>

<span data-ttu-id="fd8d1-121">미디어 유형은 웹 API에서 HTTP 메시지 본문을 직렬화 및 deserialize 하는 방법을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-121">The media type determines how Web API serializes and deserializes the HTTP message body.</span></span> <span data-ttu-id="fd8d1-122">Web API는 XML, JSON, BSON 및 양식 x-www-form-urlencoded 데이터를 기본적으로 지원 하며 *미디어 포맷터*를 작성 하 여 추가 미디어 유형을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-122">Web API has built-in support for XML, JSON, BSON, and form-urlencoded data, and you can support additional media types by writing a *media formatter*.</span></span>

<span data-ttu-id="fd8d1-123">미디어 포맷터를 만들려면 다음 클래스 중 하나에서 파생 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-123">To create a media formatter, derive from one of these classes:</span></span>

- <span data-ttu-id="fd8d1-124">[MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx).</span><span class="sxs-lookup"><span data-stu-id="fd8d1-124">[MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx).</span></span> <span data-ttu-id="fd8d1-125">이 클래스는 비동기 읽기 및 쓰기 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-125">This class uses asynchronous read and write methods.</span></span>
- <span data-ttu-id="fd8d1-126">[BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx).</span><span class="sxs-lookup"><span data-stu-id="fd8d1-126">[BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx).</span></span> <span data-ttu-id="fd8d1-127">이 클래스는 **MediaTypeFormatter** 에서 파생 되지만 동기 읽기/쓰기 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-127">This class derives from **MediaTypeFormatter** but uses synchronous read/write methods.</span></span>

<span data-ttu-id="fd8d1-128">비동기 코드가 없기 때문에 **BufferedMediaTypeFormatter** 에서 파생 하는 것이 더 간단 하지만 i/o 중에 호출 스레드가 차단 될 수 있음을 의미 하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-128">Deriving from **BufferedMediaTypeFormatter** is simpler, because there is no asynchronous code, but it also means the calling thread can block during I/O.</span></span>

## <a name="example-creating-a-csv-media-formatter"></a><span data-ttu-id="fd8d1-129">예: CSV 미디어 포맷터 만들기</span><span class="sxs-lookup"><span data-stu-id="fd8d1-129">Example: Creating a CSV Media Formatter</span></span>

<span data-ttu-id="fd8d1-130">다음 예에서는 Product 개체를 CSV (쉼표로 구분 된 값) 형식으로 serialize 할 수 있는 미디어 유형 포맷터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-130">The following example shows a media type formatter that can serialize a Product object to a comma-separated values (CSV) format.</span></span> <span data-ttu-id="fd8d1-131">이 예에서는 [CRUD 작업을 지 원하는 WEB API 만들기](../older-versions/creating-a-web-api-that-supports-crud-operations.md)자습서에 정의 된 제품 유형을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-131">This example uses the Product type defined in the tutorial [Creating a Web API that Supports CRUD Operations](../older-versions/creating-a-web-api-that-supports-crud-operations.md).</span></span> <span data-ttu-id="fd8d1-132">Product 개체의 정의는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-132">Here is the definition of the Product object:</span></span>

[!code-csharp[Main](media-formatters/samples/sample3.cs)]

<span data-ttu-id="fd8d1-133">CSV 포맷터를 구현 하려면 **BufferedMediaTypeFormatter**에서 파생 되는 클래스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-133">To implement a CSV formatter, define a class that derives from **BufferedMediaTypeFormatter**:</span></span>

[!code-csharp[Main](media-formatters/samples/sample4.cs)]

<span data-ttu-id="fd8d1-134">생성자에서 포맷터가 지 원하는 미디어 형식을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-134">In the constructor, add the media types that the formatter supports.</span></span> <span data-ttu-id="fd8d1-135">이 예제에서 포맷터는 단일 미디어 유형인 &quot;text/csv&quot;를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-135">In this example, the formatter supports a single media type, &quot;text/csv&quot;:</span></span>

[!code-csharp[Main](media-formatters/samples/sample5.cs)]

<span data-ttu-id="fd8d1-136">다음과 같이 **Canwritetype** 메서드를 재정의 하 여 포맷터가 serialize 할 수 있는 형식을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-136">Override the **CanWriteType** method to indicate which types the formatter can serialize:</span></span>

[!code-csharp[Main](media-formatters/samples/sample6.cs)]

<span data-ttu-id="fd8d1-137">이 예제에서 포맷터는 단일 `Product` 개체 뿐만 아니라 `Product` 개체의 컬렉션을 serialize 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-137">In this example, the formatter can serialize single `Product` objects as well as collections of `Product` objects.</span></span>

<span data-ttu-id="fd8d1-138">마찬가지로 **CanReadType** 메서드를 재정의 하 여 포맷터가 deserialize 할 수 있는 형식을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-138">Similarly, override the **CanReadType** method to indicate which types the formatter can deserialize.</span></span> <span data-ttu-id="fd8d1-139">이 예제에서 포맷터는 deserialization을 지원 하지 않으므로 메서드는 단순히 **false**를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-139">In this example, the formatter does not support deserialization, so the method simply returns **false**.</span></span>

[!code-csharp[Main](media-formatters/samples/sample7.cs)]

<span data-ttu-id="fd8d1-140">마지막으로 **WriteToStream** 메서드를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-140">Finally, override the **WriteToStream** method.</span></span> <span data-ttu-id="fd8d1-141">이 메서드는 스트림에 작성 하 여 형식을 serialize 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-141">This method serializes a type by writing it to a stream.</span></span> <span data-ttu-id="fd8d1-142">포맷터가 deserialization을 지 원하는 경우 **Readfromstream** 메서드를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-142">If your formatter supports deserialization, also override the **ReadFromStream** method.</span></span>

[!code-csharp[Main](media-formatters/samples/sample8.cs)]

## <a name="adding-a-media-formatter-to-the-web-api-pipeline"></a><span data-ttu-id="fd8d1-143">웹 API 파이프라인에 미디어 포맷터 추가</span><span class="sxs-lookup"><span data-stu-id="fd8d1-143">Adding a Media Formatter to the Web API Pipeline</span></span>

<span data-ttu-id="fd8d1-144">웹 API 파이프라인에 미디어 유형 포맷터를 추가 하려면 **Httpconfiguration** 개체에서 **포맷터** 속성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-144">To add a media type formatter to the Web API pipeline, use the **Formatters** property on the **HttpConfiguration** object.</span></span>

[!code-csharp[Main](media-formatters/samples/sample9.cs)]

## <a name="character-encodings"></a><span data-ttu-id="fd8d1-145">문자 인코딩</span><span class="sxs-lookup"><span data-stu-id="fd8d1-145">Character Encodings</span></span>

<span data-ttu-id="fd8d1-146">필요에 따라 미디어 포맷터는 UTF-8 또는 ISO 8859-1 같은 여러 문자 인코딩을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-146">Optionally, a media formatter can support multiple character encodings, such as UTF-8 or ISO 8859-1.</span></span>

<span data-ttu-id="fd8d1-147">생성자에서 **Supportedencodings** 컬렉션에 하나 이상의 [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) system.string 형식을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-147">In the constructor, add one or more [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) types to the **SupportedEncodings** collection.</span></span> <span data-ttu-id="fd8d1-148">기본 인코딩을 먼저 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-148">Put the default encoding first.</span></span>

[!code-csharp[Main](media-formatters/samples/sample10.cs?highlight=6-7)]

<span data-ttu-id="fd8d1-149">**WriteToStream** 및 **readfromstream** 메서드에서 [MediaTypeFormatter](https://msdn.microsoft.com/library/hh969054.aspx) 를 호출 하 여 기본 문자 인코딩을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-149">In the **WriteToStream** and **ReadFromStream** methods, call [MediaTypeFormatter.SelectCharacterEncoding](https://msdn.microsoft.com/library/hh969054.aspx) to select the preferred character encoding.</span></span> <span data-ttu-id="fd8d1-150">이 메서드는 지원 되는 인코딩 목록과 요청 헤더를 일치 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-150">This method matches the request headers against the list of supported encodings.</span></span> <span data-ttu-id="fd8d1-151">스트림에서 읽거나 쓸 때 반환 된 **인코딩을** 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8d1-151">Use the returned **Encoding** when you read or write from the stream:</span></span>

[!code-csharp[Main](media-formatters/samples/sample11.cs?highlight=3,5)]
