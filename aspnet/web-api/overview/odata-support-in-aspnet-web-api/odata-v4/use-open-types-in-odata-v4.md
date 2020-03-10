---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: ASP.NET Web API를 사용 하 여 OData v4에서 Open Types Microsoft Docs
author: microsoft
description: OData v4에서 개방형 형식은 형식 정의에 선언 된 속성 외에도 동적 속성을 포함 하는 구조화 된 형식입니다. 열기...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 950442c071bf50d2c8c1588971f13f85c4891436
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504581"
---
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="efdeb-104">ASP.NET Web API를 사용 하 여 OData v4에서 형식 열기</span><span class="sxs-lookup"><span data-stu-id="efdeb-104">Open Types in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="efdeb-105">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="efdeb-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="efdeb-106">OData v4에서 *개방형 형식은* 형식 정의에 선언 된 속성 외에도 동적 속성을 포함 하는 구조화 된 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-106">In OData v4, an *open type* is a structured type that contains dynamic properties, in addition to any properties that are declared in the type definition.</span></span> <span data-ttu-id="efdeb-107">Open types를 사용 하면 데이터 모델에 유연성을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-107">Open types let you add flexibility to your data models.</span></span> <span data-ttu-id="efdeb-108">이 자습서에서는 ASP.NET Web API OData에서 open types를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-108">This tutorial shows how to use open types in ASP.NET Web API OData.</span></span>
> 
> <span data-ttu-id="efdeb-109">이 자습서에서는 ASP.NET Web API에서 OData 끝점을 만드는 방법을 이미 알고 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-109">This tutorial assumes that you already know how to create an OData endpoint in ASP.NET Web API.</span></span> <span data-ttu-id="efdeb-110">그렇지 않은 경우 먼저 [OData V4 끝점 만들기](create-an-odata-v4-endpoint.md) 를 읽어 보십시오.</span><span class="sxs-lookup"><span data-stu-id="efdeb-110">If not, start by reading [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md) first.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="efdeb-111">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="efdeb-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="efdeb-112">Web API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="efdeb-112">Web API OData 5.3</span></span>
> - <span data-ttu-id="efdeb-113">OData v4</span><span class="sxs-lookup"><span data-stu-id="efdeb-113">OData v4</span></span>

<span data-ttu-id="efdeb-114">첫째, 일부 OData 용어는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-114">First, some OData terminology:</span></span>

- <span data-ttu-id="efdeb-115">엔터티 형식: 키를 포함 하는 구조화 된 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-115">Entity type: A structured type with a key.</span></span>
- <span data-ttu-id="efdeb-116">복합 형식: 키가 없는 구조화 된 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-116">Complex type: A structured type without a key.</span></span>
- <span data-ttu-id="efdeb-117">Open type: 동적 속성을 포함 하는 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-117">Open type: A type with dynamic properties.</span></span> <span data-ttu-id="efdeb-118">엔터티 형식과 복합 형식이 모두 열릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-118">Both entity types and complex types can be open.</span></span>

<span data-ttu-id="efdeb-119">동적 속성의 값은 기본 형식, 복합 형식 또는 열거형 형식일 수 있습니다. 또는 이러한 형식의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-119">The value of a dynamic property can be a primitive type, complex type, or enumeration type; or a collection of any of those types.</span></span> <span data-ttu-id="efdeb-120">개방형 형식에 대 한 자세한 내용은 [OData v4 사양을](http://www.odata.org/documentation/odata-version-4-0/)참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="efdeb-120">For more information about open types, see the [OData v4 specification](http://www.odata.org/documentation/odata-version-4-0/).</span></span>

## <a name="install-the-web-odata-libraries"></a><span data-ttu-id="efdeb-121">웹 OData 라이브러리를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-121">Install the Web OData Libraries</span></span>

<span data-ttu-id="efdeb-122">NuGet 패키지 관리자를 사용 하 여 최신 Web API OData 라이브러리를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-122">Use NuGet Package Manager to install the latest Web API OData libraries.</span></span> <span data-ttu-id="efdeb-123">패키지 관리자 콘솔 창에서 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-123">From the Package Manager Console window:</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a><span data-ttu-id="efdeb-124">CLR 형식 정의</span><span class="sxs-lookup"><span data-stu-id="efdeb-124">Define the CLR Types</span></span>

<span data-ttu-id="efdeb-125">먼저 EDM 모델을 CLR 형식으로 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-125">Start by defining the EDM models as CLR types.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="efdeb-126">EDM (엔터티 데이터 모델)을 만든 경우</span><span class="sxs-lookup"><span data-stu-id="efdeb-126">When the Entity Data Model (EDM) is created,</span></span>

- <span data-ttu-id="efdeb-127">`Category`은 열거형 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-127">`Category` is an enumeration type.</span></span>
- <span data-ttu-id="efdeb-128">`Address`은 복합 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-128">`Address` is a complex type.</span></span> <span data-ttu-id="efdeb-129">(키가 없으므로 엔터티 형식이 아닙니다.)</span><span class="sxs-lookup"><span data-stu-id="efdeb-129">(It does not have a key, so it is not an entity type.)</span></span>
- <span data-ttu-id="efdeb-130">`Customer`은 엔터티 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-130">`Customer` is an entity type.</span></span> <span data-ttu-id="efdeb-131">(키가 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="efdeb-131">(It has a key.)</span></span>
- <span data-ttu-id="efdeb-132">`Press`는 개방형 복합 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-132">`Press` is an open complex type.</span></span>
- <span data-ttu-id="efdeb-133">`Book`는 개방형 엔터티 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-133">`Book` is an open entity type.</span></span>

<span data-ttu-id="efdeb-134">개방형 형식을 만들려면 CLR 형식에 동적 속성을 포함 하는 `IDictionary<string, object>`형식의 속성이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-134">To create an open type, the CLR type must have a property of type `IDictionary<string, object>`, which holds the dynamic properties.</span></span>

## <a name="build-the-edm-model"></a><span data-ttu-id="efdeb-135">EDM 모델 빌드</span><span class="sxs-lookup"><span data-stu-id="efdeb-135">Build the EDM Model</span></span>

<span data-ttu-id="efdeb-136">**ODataConventionModelBuilder** 를 사용 하 여 EDM을 만드는 경우 `Press` 및 `Book` `IDictionary<string, object>` 속성이 있는지 여부에 따라 자동으로 개방형 형식으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-136">If you use **ODataConventionModelBuilder** to create the EDM, `Press` and `Book` are automatically added as open types, based on the presence of a `IDictionary<string, object>` property.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="efdeb-137">**만드는**를 사용 하 여 EDM을 명시적으로 빌드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-137">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a><span data-ttu-id="efdeb-138">OData 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="efdeb-138">Add an OData Controller</span></span>

<span data-ttu-id="efdeb-139">그런 다음 OData 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-139">Next, add an OData controller.</span></span> <span data-ttu-id="efdeb-140">이 자습서에서는 GET 및 POST 요청만 지원 하 고 메모리 내 목록을 사용 하 여 엔터티를 저장 하는 간단한 컨트롤러를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-140">For this tutorial, we'll use a simplified controller that just supports GET and POST requests, and uses an in-memory list to store entities.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="efdeb-141">첫 번째 `Book` 인스턴스에는 동적 속성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-141">Notice that the first `Book` instance has no dynamic properties.</span></span> <span data-ttu-id="efdeb-142">두 번째 `Book` 인스턴스에는 다음과 같은 동적 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-142">The second `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="efdeb-143">"게시 됨": 기본 형식</span><span class="sxs-lookup"><span data-stu-id="efdeb-143">"Published": Primitive type</span></span>
- <span data-ttu-id="efdeb-144">"Authors": 기본 형식의 컬렉션</span><span class="sxs-lookup"><span data-stu-id="efdeb-144">"Authors": Collection of primitive types</span></span>
- <span data-ttu-id="efdeb-145">"OtherCategories": 열거형 형식의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-145">"OtherCategories": Collection of enumeration types.</span></span>

<span data-ttu-id="efdeb-146">또한 해당 `Book` 인스턴스의 `Press` 속성에는 다음과 같은 동적 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-146">Also, the `Press` property of that `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="efdeb-147">"블로그": 기본 형식</span><span class="sxs-lookup"><span data-stu-id="efdeb-147">"Blog": Primitive type</span></span>
- <span data-ttu-id="efdeb-148">"Address": 복합 형식</span><span class="sxs-lookup"><span data-stu-id="efdeb-148">"Address": Complex type</span></span>

## <a name="query-the-metadata"></a><span data-ttu-id="efdeb-149">메타 데이터 쿼리</span><span class="sxs-lookup"><span data-stu-id="efdeb-149">Query the Metadata</span></span>

<span data-ttu-id="efdeb-150">OData 메타 데이터 문서를 가져오려면 GET 요청을 `~/$metadata`으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-150">To get the OData metadata document, send a GET request to `~/$metadata`.</span></span> <span data-ttu-id="efdeb-151">응답 본문은 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-151">The response body should look similar to this:</span></span>

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

<span data-ttu-id="efdeb-152">메타 데이터 문서에서 다음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-152">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="efdeb-153">`Book` 및 `Press` 형식의 경우 `OpenType` 특성의 값은 true입니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-153">For the `Book` and `Press` types, the value of the `OpenType` attribute is true.</span></span> <span data-ttu-id="efdeb-154">`Customer` 및 `Address` 형식에는이 특성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-154">The `Customer` and `Address` types don't have this attribute.</span></span>
- <span data-ttu-id="efdeb-155">`Book` 엔터티 형식에는 네 개의 선언 된 속성, 즉 ISBN, Title 및 Press가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-155">The `Book` entity type has three declared properties: ISBN, Title, and Press.</span></span> <span data-ttu-id="efdeb-156">OData 메타 데이터는 CLR 클래스의 `Book.Properties` 속성을 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-156">The OData metadata does not include the `Book.Properties` property from the CLR class.</span></span>
- <span data-ttu-id="efdeb-157">마찬가지로 `Press` 복합 형식에는 이름 및 범주 라는 두 개의 선언 된 속성만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-157">Similarly, the `Press` complex type has only two declared properties: Name and Category.</span></span> <span data-ttu-id="efdeb-158">메타 데이터는 CLR 클래스의 `Press.DynamicProperties` 속성을 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-158">The metadata does not include the `Press.DynamicProperties` property from the CLR class.</span></span>

## <a name="query-an-entity"></a><span data-ttu-id="efdeb-159">엔터티 쿼리</span><span class="sxs-lookup"><span data-stu-id="efdeb-159">Query an Entity</span></span>

<span data-ttu-id="efdeb-160">ISBN이 "978-0-7356-7942-9"와 같은 책을 가져오려면 GET 요청을 `~/Books('978-0-7356-7942-9')`으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-160">To get the book with ISBN equal to "978-0-7356-7942-9", send a GET request to `~/Books('978-0-7356-7942-9')`.</span></span> <span data-ttu-id="efdeb-161">응답 본문은 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-161">The response body should look similar to the following.</span></span> <span data-ttu-id="efdeb-162">(보다 쉽게 읽을 수 있도록 들여쓰기)</span><span class="sxs-lookup"><span data-stu-id="efdeb-162">(Indented to make it more readable.)</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

<span data-ttu-id="efdeb-163">동적 속성은 선언 된 속성을 사용 하 여 인라인으로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-163">Notice that the dynamic properties are included inline with the declared properties.</span></span>

## <a name="post-an-entity"></a><span data-ttu-id="efdeb-164">엔터티 게시</span><span class="sxs-lookup"><span data-stu-id="efdeb-164">POST an Entity</span></span>

<span data-ttu-id="efdeb-165">책 엔터티를 추가 하려면 `~/Books`에 POST 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-165">To add a Book entity, send a POST request to `~/Books`.</span></span> <span data-ttu-id="efdeb-166">클라이언트는 요청 페이로드에서 동적 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-166">The client can set dynamic properties in the request payload.</span></span>

<span data-ttu-id="efdeb-167">예제 요청은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-167">Here is an example request.</span></span> <span data-ttu-id="efdeb-168">"Price" 및 "게시 된" 속성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-168">Note the "Price" and "Published" properties.</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

<span data-ttu-id="efdeb-169">컨트롤러 메서드에서 중단점을 설정 하는 경우 Web API가 `Properties` 사전에 이러한 속성을 추가 하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efdeb-169">If you set a breakpoint in the controller method, you can see that Web API added these properties to the `Properties` dictionary.</span></span>

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a><span data-ttu-id="efdeb-170">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="efdeb-170">Additional Resources</span></span>

[<span data-ttu-id="efdeb-171">OData 형식 샘플 열기</span><span class="sxs-lookup"><span data-stu-id="efdeb-171">OData Open Type Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
