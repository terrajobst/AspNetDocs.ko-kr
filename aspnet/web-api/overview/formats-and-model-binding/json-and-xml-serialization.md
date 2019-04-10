---
uid: web-api/overview/formats-and-model-binding/json-and-xml-serialization
title: JSON 및 XML 직렬화에 ASP.NET Web API-ASP.NET 4.x
author: MikeWasson
description: ASP.NET Web API에서 JSON 및 XML 포맷터를 ASP.NET에 대 한 설명 4.x 합니다.
ms.author: riande
ms.date: 05/30/2012
ms.custom: seoapril2019
ms.assetid: 1cd7525d-de5e-4ab6-94f0-51480d3255d1
msc.legacyurl: /web-api/overview/formats-and-model-binding/json-and-xml-serialization
msc.type: authoredcontent
ms.openlocfilehash: a9e7ed63a55c146976e0221214e722f3a2292fee
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59408279"
---
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a><span data-ttu-id="c22dc-103">JSON 및 XML 직렬화에 ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="c22dc-103">JSON and XML Serialization in ASP.NET Web API</span></span>

<span data-ttu-id="c22dc-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c22dc-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="c22dc-105">이 문서에서는 ASP.NET Web API에서 JSON 및 XML 포맷터를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-105">This article describes the JSON and XML formatters in ASP.NET Web API.</span></span>

<span data-ttu-id="c22dc-106">ASP.NET Web API에는 *미디어 유형 포맷터* 는 개체 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-106">In ASP.NET Web API, a *media-type formatter* is an object that can:</span></span>

- <span data-ttu-id="c22dc-107">HTTP에서 읽기 CLR 개체로 메시지 본문</span><span class="sxs-lookup"><span data-stu-id="c22dc-107">Read CLR objects from an HTTP message body</span></span>
- <span data-ttu-id="c22dc-108">HTTP 메시지 본문에 CLR 개체를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-108">Write CLR objects into an HTTP message body</span></span>

<span data-ttu-id="c22dc-109">웹 API는 JSON 및 XML에 대 한 미디어 유형 포맷터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-109">Web API provides media-type formatters for both JSON and XML.</span></span> <span data-ttu-id="c22dc-110">프레임 워크는 기본적으로 파이프라인에 이러한 포맷터를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-110">The framework inserts these formatters into the pipeline by default.</span></span> <span data-ttu-id="c22dc-111">클라이언트는 HTTP 요청의 Accept 헤더의 JSON 또는 XML 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-111">Clients can request either JSON or XML in the Accept header of the HTTP request.</span></span>

## <a name="contents"></a><span data-ttu-id="c22dc-112">목차</span><span class="sxs-lookup"><span data-stu-id="c22dc-112">Contents</span></span>

- [<span data-ttu-id="c22dc-113">JSON 미디어 유형 포맷터입니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-113">JSON Media-Type Formatter</span></span>](#json_media_type_formatter)

    - [<span data-ttu-id="c22dc-114">읽기 전용 속성</span><span class="sxs-lookup"><span data-stu-id="c22dc-114">Read-Only Properties</span></span>](#json_readonly)
    - [<span data-ttu-id="c22dc-115">날짜</span><span class="sxs-lookup"><span data-stu-id="c22dc-115">Dates</span></span>](#json_dates)
    - [<span data-ttu-id="c22dc-116">들여쓰기</span><span class="sxs-lookup"><span data-stu-id="c22dc-116">Indenting</span></span>](#json_indenting)
    - [<span data-ttu-id="c22dc-117">카멜식 대/소문자</span><span class="sxs-lookup"><span data-stu-id="c22dc-117">Camel Casing</span></span>](#json_camelcasing)
    - [<span data-ttu-id="c22dc-118">익명 및 약한 형 개체</span><span class="sxs-lookup"><span data-stu-id="c22dc-118">Anonymous and Weakly-Typed Objects</span></span>](#json_anon)
- [<span data-ttu-id="c22dc-119">XML 미디어 유형 포맷터입니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-119">XML Media-Type Formatter</span></span>](#xml_media_type_formatter)

    - [<span data-ttu-id="c22dc-120">읽기 전용 속성</span><span class="sxs-lookup"><span data-stu-id="c22dc-120">Read-Only Properties</span></span>](#xml_readonly)
    - [<span data-ttu-id="c22dc-121">날짜</span><span class="sxs-lookup"><span data-stu-id="c22dc-121">Dates</span></span>](#xml_dates)
    - [<span data-ttu-id="c22dc-122">들여쓰기</span><span class="sxs-lookup"><span data-stu-id="c22dc-122">Indenting</span></span>](#xml_indenting)
    - [<span data-ttu-id="c22dc-123">형식당 하나의 XML 직렬 변환기 설정</span><span class="sxs-lookup"><span data-stu-id="c22dc-123">Setting Per-Type XML Serializers</span></span>](#xml_pertype)
- [<span data-ttu-id="c22dc-124">JSON 또는 XML 포맷터를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-124">Removing the JSON or XML Formatter</span></span>](#removing_the_json_or_xml_formatter)
- [<span data-ttu-id="c22dc-125">순환 개체 참조를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-125">Handling Circular Object References</span></span>](#handling_circular_object_references)
- [<span data-ttu-id="c22dc-126">테스트 개체 Serialization</span><span class="sxs-lookup"><span data-stu-id="c22dc-126">Testing Object Serialization</span></span>](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a><span data-ttu-id="c22dc-127">JSON 미디어 유형 포맷터입니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-127">JSON Media-Type Formatter</span></span>

<span data-ttu-id="c22dc-128">제공 하는 JSON 형식 지정 된 **JsonMediaTypeFormatter** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-128">JSON formatting is provided by the **JsonMediaTypeFormatter** class.</span></span> <span data-ttu-id="c22dc-129">기본적으로 **JsonMediaTypeFormatter** 사용 하는 [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serialization을 수행 하는 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-129">By default, **JsonMediaTypeFormatter** uses the [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) library to perform serialization.</span></span> <span data-ttu-id="c22dc-130">Json.NET 타사 오픈 소스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-130">Json.NET is a third-party open source project.</span></span>

<span data-ttu-id="c22dc-131">원하는 경우 구성할 수 있습니다는 **JsonMediaTypeFormatter** 클래스를 사용 합니다 **DataContractJsonSerializer** Json.NET 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-131">If you prefer, you can configure the **JsonMediaTypeFormatter** class to use the **DataContractJsonSerializer** instead of Json.NET.</span></span> <span data-ttu-id="c22dc-132">이렇게 하려면 설정 합니다 **UseDataContractJsonSerializer** 속성을 **true**:</span><span class="sxs-lookup"><span data-stu-id="c22dc-132">To do so, set the **UseDataContractJsonSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a><span data-ttu-id="c22dc-133">JSON serialization</span><span class="sxs-lookup"><span data-stu-id="c22dc-133">JSON Serialization</span></span>

<span data-ttu-id="c22dc-134">이 섹션에서는 기본값을 사용 하 여 JSON 포맷터의 몇 가지 특정 동작을 설명 [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer입니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-134">This section describes some specific behaviors of the JSON formatter, using the default [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer.</span></span> <span data-ttu-id="c22dc-135">Json.NET library;의 포괄적인 설명서를 다루지는지 않습니다. 자세한 내용은 참조는 [Json.NET 설명서](http://james.newtonking.com/projects/json/help/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-135">This is not meant to be comprehensive documentation of the Json.NET library; for more information, see the [Json.NET Documentation](http://james.newtonking.com/projects/json/help/).</span></span>

#### <a name="what-gets-serialized"></a><span data-ttu-id="c22dc-136">Serialize 되는 요소?</span><span class="sxs-lookup"><span data-stu-id="c22dc-136">What Gets Serialized?</span></span>

<span data-ttu-id="c22dc-137">기본적으로 모든 public 속성과 필드가 serialize 된 JSON에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-137">By default, all public properties and fields are included in the serialized JSON.</span></span> <span data-ttu-id="c22dc-138">속성 또는 필드를 생략 하려면 데코 레이트 하는 **JsonIgnore** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-138">To omit a property or field, decorate it with the **JsonIgnore** attribute.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

<span data-ttu-id="c22dc-139">원하는 경우는 &quot;옵트인&quot; 접근을 사용 하 여 클래스를 데코 레이트 합니다 **DataContract** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-139">If you prefer an &quot;opt-in&quot; approach, decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="c22dc-140">이 특성이 있는 경우에 멤버를 무시에 대 한 필요 합니다 **DataMember**합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-140">If this attribute is present, members are ignored unless they have the **DataMember**.</span></span> <span data-ttu-id="c22dc-141">사용할 수도 있습니다 **DataMember** 전용 멤버를 serialize 합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-141">You can also use **DataMember** to serialize private members.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="c22dc-142">읽기 전용 속성</span><span class="sxs-lookup"><span data-stu-id="c22dc-142">Read-Only Properties</span></span>

<span data-ttu-id="c22dc-143">읽기 전용 속성은 기본적으로 serialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-143">Read-only properties are serialized by default.</span></span>

<a id="json_dates"></a>
### <a name="dates"></a><span data-ttu-id="c22dc-144">날짜</span><span class="sxs-lookup"><span data-stu-id="c22dc-144">Dates</span></span>

<span data-ttu-id="c22dc-145">기본적으로 Json.NET 날짜를 씁니다 [ISO 8601](http://www.w3.org/TR/NOTE-datetime) 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-145">By default, Json.NET writes dates in [ISO 8601](http://www.w3.org/TR/NOTE-datetime) format.</span></span> <span data-ttu-id="c22dc-146">Utc (협정 세계시) 날짜는 "Z" 접미사를 사용 하 여 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-146">Dates in UTC (Coordinated Universal Time) are written with a "Z" suffix.</span></span> <span data-ttu-id="c22dc-147">현지 시간에서 날짜-표준 시간대 오프셋을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-147">Dates in local time include a time-zone offset.</span></span> <span data-ttu-id="c22dc-148">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="c22dc-148">For example:</span></span>

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

<span data-ttu-id="c22dc-149">Json.NET 기본적으로 표준 시간대를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-149">By default, Json.NET preserves the time zone.</span></span> <span data-ttu-id="c22dc-150">DateTimeZoneHandling 속성을 설정 하 여이 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-150">You can override this by setting the DateTimeZoneHandling property:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

<span data-ttu-id="c22dc-151">사용 하려는 경우 [Microsoft JSON 날짜 형식을](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) ISO 8601 대신 설정 된 **DateFormatHandling** serializer 설정에 대 한 속성:</span><span class="sxs-lookup"><span data-stu-id="c22dc-151">If you prefer to use [Microsoft JSON date format](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) instead of ISO 8601, set the **DateFormatHandling** property on the serializer settings:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="c22dc-152">들여쓰기</span><span class="sxs-lookup"><span data-stu-id="c22dc-152">Indenting</span></span>

<span data-ttu-id="c22dc-153">들여쓰기 된 JSON을 작성 하려면 설정 합니다 **서식** 설정을 **Formatting.Indented**:</span><span class="sxs-lookup"><span data-stu-id="c22dc-153">To write indented JSON, set the **Formatting** setting to **Formatting.Indented**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a><span data-ttu-id="c22dc-154">카멜식 대/소문자</span><span class="sxs-lookup"><span data-stu-id="c22dc-154">Camel Casing</span></span>

<span data-ttu-id="c22dc-155">JSON 속성 이름을 카멜식 대/소문자를 사용 하 여 데이터 모델을 변경 하지 않고를 작성 하려면 설정 합니다 **CamelCasePropertyNamesContractResolver** serializer에서:</span><span class="sxs-lookup"><span data-stu-id="c22dc-155">To write JSON property names with camel casing, without changing your data model, set the **CamelCasePropertyNamesContractResolver** on the serializer:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a><span data-ttu-id="c22dc-156">익명 및 약한 형 개체</span><span class="sxs-lookup"><span data-stu-id="c22dc-156">Anonymous and Weakly-Typed Objects</span></span>

<span data-ttu-id="c22dc-157">동작 메서드는 익명 개체를 반환 하 고 JSON으로 serialize 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-157">An action method can return an anonymous object and serialize it to JSON.</span></span> <span data-ttu-id="c22dc-158">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="c22dc-158">For example:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

<span data-ttu-id="c22dc-159">응답 메시지 본문은 다음 JSON이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-159">The response message body will contain the following JSON:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

<span data-ttu-id="c22dc-160">웹 API가 받은 느슨하게 구조화 클라이언트에서 JSON 개체, 경우 요청 본문을 deserialize 할 수는 **Newtonsoft.Json.Linq.JObject** 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-160">If your web API receives loosely structured JSON objects from clients, you can deserialize the request body to a **Newtonsoft.Json.Linq.JObject** type.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

<span data-ttu-id="c22dc-161">그러나는 강력한 형식의 데이터 개체를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-161">However, it is usually better to use strongly typed data objects.</span></span> <span data-ttu-id="c22dc-162">그런 다음 사용자가 직접 데이터를 구문 분석 필요가 없습니다 및 모델 유효성 검사의 이점을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-162">Then you don't need to parse the data yourself, and you get the benefits of model validation.</span></span>

<span data-ttu-id="c22dc-163">XML serializer 익명 형식을 지원 하지 않습니다 또는 **JObject** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="c22dc-163">The XML serializer does not support anonymous types or **JObject** instances.</span></span> <span data-ttu-id="c22dc-164">JSON 데이터에 대 한 이러한 기능을 사용 하는 경우이 문서의 뒷부분에 설명 된 대로 XML 포맷터 파이프라인에서 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-164">If you use these features for your JSON data, you should remove the XML formatter from the pipeline, as described later in this article.</span></span>

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a><span data-ttu-id="c22dc-165">XML 미디어 유형 포맷터입니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-165">XML Media-Type Formatter</span></span>

<span data-ttu-id="c22dc-166">제공 하는 XML 서식 지정 된 **XmlMediaTypeFormatter** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-166">XML formatting is provided by the **XmlMediaTypeFormatter** class.</span></span> <span data-ttu-id="c22dc-167">기본적으로 **XmlMediaTypeFormatter** 사용 하는 **DataContractSerializer** serialization을 수행 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-167">By default, **XmlMediaTypeFormatter** uses the **DataContractSerializer** class to perform serialization.</span></span>

<span data-ttu-id="c22dc-168">원하는 경우 구성할 수 있습니다는 **XmlMediaTypeFormatter** 사용 하는 **XmlSerializer** 대신 합니다 **DataContractSerializer**합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-168">If you prefer, you can configure the **XmlMediaTypeFormatter** to use the **XmlSerializer** instead of the **DataContractSerializer**.</span></span> <span data-ttu-id="c22dc-169">이렇게 하려면 설정 합니다 **UseXmlSerializer** 속성을 **true**:</span><span class="sxs-lookup"><span data-stu-id="c22dc-169">To do so, set the **UseXmlSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

<span data-ttu-id="c22dc-170">합니다 **XmlSerializer** 클래스 형식 보다 적은 집합을 지원 **DataContractSerializer**, 하지만 결과 XML 통해 더 많은 제어를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-170">The **XmlSerializer** class supports a narrower set of types than **DataContractSerializer**, but gives more control over the resulting XML.</span></span> <span data-ttu-id="c22dc-171">사용 하는 것이 좋습니다 **XmlSerializer** 기존 XML 스키마와 일치 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="c22dc-171">Consider using **XmlSerializer** if you need to match an existing XML schema.</span></span>

### <a name="xml-serialization"></a><span data-ttu-id="c22dc-172">XML Serialization</span><span class="sxs-lookup"><span data-stu-id="c22dc-172">XML Serialization</span></span>

<span data-ttu-id="c22dc-173">이 섹션에서는 기본값을 사용 하 여 XML 포맷터의 몇 가지 특정 동작을 설명 **DataContractSerializer**합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-173">This section describes some specific behaviors of the XML formatter, using the default **DataContractSerializer**.</span></span>

<span data-ttu-id="c22dc-174">기본적으로 DataContractSerializer는 다음과 같이 동작합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-174">By default, the DataContractSerializer behaves as follows:</span></span>

- <span data-ttu-id="c22dc-175">모든 공용 읽기/쓰기 속성과 필드가 serialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-175">All public read/write properties and fields are serialized.</span></span> <span data-ttu-id="c22dc-176">속성 또는 필드를 생략 하려면 데코 레이트 하는 **IgnoreDataMember** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-176">To omit a property or field, decorate it with the **IgnoreDataMember** attribute.</span></span>
- <span data-ttu-id="c22dc-177">Private 및 protected 멤버는 serialize 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-177">Private and protected members are not serialized.</span></span>
- <span data-ttu-id="c22dc-178">읽기 전용 속성이 serialize 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-178">Read-only properties are not serialized.</span></span> <span data-ttu-id="c22dc-179">그러나 (읽기 전용 컬렉션 속성의 내용은 serialize 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="c22dc-179">(However, the contents of a read-only collection property are serialized.)</span></span>
- <span data-ttu-id="c22dc-180">클래스 선언에 표시 된 대로 클래스 및 멤버 이름의 XML로 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-180">Class and member names are written in the XML exactly as they appear in the class declaration.</span></span>
- <span data-ttu-id="c22dc-181">기본 XML 네임 스페이스 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-181">A default XML namespace is used.</span></span>

<span data-ttu-id="c22dc-182">사용 하 여 클래스를 데코레이팅 할 수 있습니다 더 많이 제어할 serialization에 필요한 경우는 **DataContract** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-182">If you need more control over the serialization, you can decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="c22dc-183">이 특성이 있는 경우 클래스는 다음과 같이 serialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-183">When this attribute is present, the class is serialized as follows:</span></span>

- <span data-ttu-id="c22dc-184">&quot;옵트인&quot; 접근 방식: 기본적으로 속성과 필드가 serialize 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-184">&quot;Opt in&quot; approach: Properties and fields are not serialized by default.</span></span> <span data-ttu-id="c22dc-185">속성 또는 필드를 serialize 하려면 데코 레이트 하는 **DataMember** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-185">To serialize a property or field, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="c22dc-186">Private 또는 protected 멤버를 serialize 하려면 데코 레이트 하는 **DataMember** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-186">To serialize a private or protected member, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="c22dc-187">읽기 전용 속성이 serialize 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-187">Read-only properties are not serialized.</span></span>
- <span data-ttu-id="c22dc-188">클래스 이름을 XML에 표시 되는 방식을 변경 하려면 설정 합니다 *이름* 에 매개 변수를 **DataContract** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-188">To change how the class name appears in the XML, set the *Name* parameter in the **DataContract** attribute.</span></span>
- <span data-ttu-id="c22dc-189">멤버 이름을 XML에 표시 되는 방식을 변경 하려면 설정 합니다 *이름* 에 매개 변수를 **DataMember** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-189">To change how a member name appears in the XML, set the *Name* parameter in the **DataMember** attribute.</span></span>
- <span data-ttu-id="c22dc-190">XML 네임 스페이스를 변경 하려면 설정 합니다 *Namespace* 에 매개 변수를 **DataContract** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-190">To change the XML namespace, set the *Namespace* parameter in the **DataContract** class.</span></span>

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="c22dc-191">읽기 전용 속성</span><span class="sxs-lookup"><span data-stu-id="c22dc-191">Read-Only Properties</span></span>

<span data-ttu-id="c22dc-192">읽기 전용 속성이 serialize 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-192">Read-only properties are not serialized.</span></span> <span data-ttu-id="c22dc-193">읽기 전용 속성을 지 원하는 private 필드에 사용 하 여 개인 필드를 표시할 수 있습니다 합니다 **DataMember** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-193">If a read-only property has a backing private field, you can mark the private field with the **DataMember** attribute.</span></span> <span data-ttu-id="c22dc-194">이 접근 방식에서는 합니다 **DataContract** 클래스의 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-194">This approach requires the **DataContract** attribute on the class.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a><span data-ttu-id="c22dc-195">날짜</span><span class="sxs-lookup"><span data-stu-id="c22dc-195">Dates</span></span>

<span data-ttu-id="c22dc-196">날짜는 ISO 8601 형식으로 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-196">Dates are written in ISO 8601 format.</span></span> <span data-ttu-id="c22dc-197">예를 들어 &quot;2012-05-23T20:21:37.9116538Z&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-197">For example, &quot;2012-05-23T20:21:37.9116538Z&quot;.</span></span>

<a id="xml_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="c22dc-198">들여쓰기</span><span class="sxs-lookup"><span data-stu-id="c22dc-198">Indenting</span></span>

<span data-ttu-id="c22dc-199">들여쓰기 된 XML을 쓸 설정 합니다 **들여쓰기** 속성을 **true**:</span><span class="sxs-lookup"><span data-stu-id="c22dc-199">To write indented XML, set the **Indent** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a><span data-ttu-id="c22dc-200">형식당 하나의 XML 직렬 변환기 설정</span><span class="sxs-lookup"><span data-stu-id="c22dc-200">Setting Per-Type XML Serializers</span></span>

<span data-ttu-id="c22dc-201">다른 CLR 형식에 대 한 다른 XML 직렬 변환기를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-201">You can set different XML serializers for different CLR types.</span></span> <span data-ttu-id="c22dc-202">예를 들어 필요한 특정 데이터 개체를 해야 할 수 있습니다 **XmlSerializer** 이전 버전과 호환성에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-202">For example, you might have a particular data object that requires **XmlSerializer** for backward compatibility.</span></span> <span data-ttu-id="c22dc-203">사용할 수 있습니다 **XmlSerializer** 이 개체를 사용 하 여 계속 **DataContractSerializer** 다른 형식에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-203">You can use **XmlSerializer** for this object and continue to use **DataContractSerializer** for other types.</span></span>

<span data-ttu-id="c22dc-204">특정 형식에 대 한 XML 직렬 변환기를 설정 하려면 호출 **SetSerializer**합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-204">To set an XML serializer for a particular type, call **SetSerializer**.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

<span data-ttu-id="c22dc-205">지정할 수는 **XmlSerializer** 에서 파생 된 모든 개체 또는 **XmlObjectSerializer**합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-205">You can specify an **XmlSerializer** or any object that derives from **XmlObjectSerializer**.</span></span>

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a><span data-ttu-id="c22dc-206">JSON 또는 XML 포맷터를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-206">Removing the JSON or XML Formatter</span></span>

<span data-ttu-id="c22dc-207">JSON 포맷터 또는 XML 포맷터를 사용 하지 않을 경우 포맷터 목록에서 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-207">You can remove the JSON formatter or the XML formatter from the list of formatters, if you do not want to use them.</span></span> <span data-ttu-id="c22dc-208">이 작업을 수행 하는 주요 이유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-208">The main reasons to do this are:</span></span>

- <span data-ttu-id="c22dc-209">특정 미디어 유형의 웹 API 응답 내용을 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-209">To restrict your web API responses to a particular media type.</span></span> <span data-ttu-id="c22dc-210">예를 들어 JSON 응답 에서만 지원 및 XML 포맷터를 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-210">For example, you might decide to support only JSON responses, and remove the XML formatter.</span></span>
- <span data-ttu-id="c22dc-211">기본 포맷터를 사용자 지정 포맷터를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-211">To replace the default formatter with a custom formatter.</span></span> <span data-ttu-id="c22dc-212">예를 들어 JSON 포맷터의 고유한 사용자 지정 구현을 사용 하 여 JSON 포맷터를 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-212">For example, you could replace the JSON formatter with your own custom implementation of a JSON formatter.</span></span>

<span data-ttu-id="c22dc-213">다음 코드는 기본 포맷터를 제거 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-213">The following code shows how to remove the default formatters.</span></span> <span data-ttu-id="c22dc-214">이를 호출 하면 **응용 프로그램\_시작** Global.asax에 정의 된 메서드를 합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-214">Call this from your **Application\_Start** method, defined in Global.asax.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a><span data-ttu-id="c22dc-215">순환 개체 참조를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-215">Handling Circular Object References</span></span>

<span data-ttu-id="c22dc-216">기본적으로 JSON 및 XML 포맷터를 값으로 모든 개체를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-216">By default, the JSON and XML formatters write all objects as values.</span></span> <span data-ttu-id="c22dc-217">두 속성이 같은 개체를 참조 하는 경우, 동일한 개체를 컬렉션에 두 번 표시 하는 경우 포맷터 개체를 두 번 serialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-217">If two properties refer to the same object, or if the same object appears twice in a collection, the formatter will serialize the object twice.</span></span> <span data-ttu-id="c22dc-218">왜냐하면 특정 문제를 개체 그래프에는 주기를 포함 하는 경우 serializer가 그래프에는 루프를 감지 하는 경우 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-218">This is a particular problem if your object graph contains cycles, because the serializer will throw an exception when it detects a loop in the graph.</span></span>

<span data-ttu-id="c22dc-219">다음 개체 모델 및 컨트롤러를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-219">Consider the following object models and controller.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

<span data-ttu-id="c22dc-220">이 작업을 호출 하면 포맷터를 클라이언트에 상태 코드 500 (내부 서버 오류) 응답을 변환 하는 예외가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-220">Invoking this action will cause the formatter to thrown an exception, which translates to a status code 500 (Internal Server Error) response to the client.</span></span>

<span data-ttu-id="c22dc-221">JSON에서 개체 참조를 유지 하려면 다음 코드를 추가 합니다 **응용 프로그램\_시작** Global.asax 파일에는 메서드:</span><span class="sxs-lookup"><span data-stu-id="c22dc-221">To preserve object references in JSON, add the following code to **Application\_Start** method in the Global.asax file:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

<span data-ttu-id="c22dc-222">이제 컨트롤러 작업에서는 다음과 같은 JSON을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-222">Now the controller action will return JSON that looks like this:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

<span data-ttu-id="c22dc-223">직렬 변환기를 추가 하는 &quot;$id&quot; 두 개체에는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-223">Notice that the serializer adds an &quot;$id&quot; property to both objects.</span></span> <span data-ttu-id="c22dc-224">또한 감지한 Employee.Department 속성 개체 참조를 사용 하 여 값을 대체 하도록 루프를 만듭니다. {&quot;$ref&quot;:&quot;1&quot;}.</span><span class="sxs-lookup"><span data-stu-id="c22dc-224">Also, it detects that the Employee.Department property creates a loop, so it replaces the value with an object reference: {&quot;$ref&quot;:&quot;1&quot;}.</span></span>

> [!NOTE]
> <span data-ttu-id="c22dc-225">개체 참조는 json에서 표준 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-225">Object references are not standard in JSON.</span></span> <span data-ttu-id="c22dc-226">이 기능을 사용 하기 전에 클라이언트에 결과 구문 분석할 수 있는지 여부를 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-226">Before using this feature, consider whether your clients will be able to parse the results.</span></span> <span data-ttu-id="c22dc-227">그래프에서 주기를 제거 하려면 단순히 좋을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-227">It might be better simply to remove cycles from the graph.</span></span> <span data-ttu-id="c22dc-228">예를 들어,이 예제에서 직원 부서에 다시 링크를 실제로 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-228">For example, the link from Employee back to Department is not really needed in this example.</span></span>


<span data-ttu-id="c22dc-229">XML에서 개체 참조를 유지 하는 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-229">To preserve object references in XML, you have two options.</span></span> <span data-ttu-id="c22dc-230">간단한 옵션은 추가 `[DataContract(IsReference=true)]` 모델 클래스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-230">The simpler option is to add `[DataContract(IsReference=true)]` to your model class.</span></span> <span data-ttu-id="c22dc-231">합니다 *IsReference* 개체 참조 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-231">The *IsReference* parameter enables object references.</span></span> <span data-ttu-id="c22dc-232">유의 해야 **DataContract** 추가할 해야 하므로 옵트인, 직렬화를 사용 하면 **DataMember** 속성 특성:</span><span class="sxs-lookup"><span data-stu-id="c22dc-232">Remember that **DataContract** makes serialization opt-in, so you will also need to add **DataMember** attributes to the properties:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

<span data-ttu-id="c22dc-233">포맷터와 유사한 XML 생성은 이제 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-233">Now the formatter will produce XML similar to following:</span></span>

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

<span data-ttu-id="c22dc-234">모델 클래스의 특성을 방지 하려는 경우 또 다른 옵션: 만들 새 형식별 **DataContractSerializer** 인스턴스 및 설정 *preserveObjectReferences* 에 **true** 생성자에서.</span><span class="sxs-lookup"><span data-stu-id="c22dc-234">If you want to avoid attributes on your model class, there is another option: Create a new type-specific **DataContractSerializer** instance and set *preserveObjectReferences* to **true** in the constructor.</span></span> <span data-ttu-id="c22dc-235">XML 미디어 유형 포맷터에서 형식당 하나의 serializer로이 인스턴스를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-235">Then set this instance as a per-type serializer on the XML media-type formatter.</span></span> <span data-ttu-id="c22dc-236">다음 코드에는이 작업을 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-236">The following code show how to do this:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a><span data-ttu-id="c22dc-237">테스트 개체 Serialization</span><span class="sxs-lookup"><span data-stu-id="c22dc-237">Testing Object Serialization</span></span>

<span data-ttu-id="c22dc-238">Web API를 디자인할 때 데이터 개체는 직렬화 하는 방법을 테스트 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-238">As you design your web API, it is useful to test how your data objects will be serialized.</span></span> <span data-ttu-id="c22dc-239">컨트롤러 만들기 또는 컨트롤러 작업을 호출 하지 않고이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c22dc-239">You can do this without creating a controller or invoking a controller action.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
