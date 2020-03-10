---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-4
title: 엔터티 관계 처리 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: d2f5710c-23c7-40a5-9cd9-5d0516570cba
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-4
msc.type: authoredcontent
ms.openlocfilehash: be4948e5443a5eb4e1824c63dd0c445a7ee1928e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449123"
---
# <a name="handling-entity-relations"></a><span data-ttu-id="949b7-102">엔터티 관계 처리</span><span class="sxs-lookup"><span data-stu-id="949b7-102">Handling Entity Relations</span></span>

<span data-ttu-id="949b7-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="949b7-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="949b7-104">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="949b7-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="949b7-105">이 섹션에서는 EF가 관련 엔터티를 로드 하는 방법 및 모델 클래스에서 순환 탐색 속성을 처리 하는 방법에 대해 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-105">This section describes some details of how EF loads related entities, and how to handle circular navigation properties in your model classes.</span></span> <span data-ttu-id="949b7-106">이 단원에서는 배경 지식을 제공 하며 자습서를 완료 하는 데 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-106">(This section provides background knowledge, and is not required to complete the tutorial.</span></span> <span data-ttu-id="949b7-107">원한다 면 [5 부.](part-5.md)로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-107">If you prefer, skip to [Part 5.](part-5.md).)</span></span>

## <a name="eager-loading-versus-lazy-loading"></a><span data-ttu-id="949b7-108">즉시 로드 및 지연 로드</span><span class="sxs-lookup"><span data-stu-id="949b7-108">Eager Loading versus Lazy Loading</span></span>

<span data-ttu-id="949b7-109">EF를 관계형 데이터베이스와 함께 사용 하는 경우 EF에서 관련 데이터를 로드 하는 방법을 이해 하는 것이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-109">When using EF with a relational database, it's important to understand how EF loads related data.</span></span>

<span data-ttu-id="949b7-110">EF에서 생성 하는 SQL 쿼리를 확인 하는 것도 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-110">It's also useful to see the SQL queries that EF generates.</span></span> <span data-ttu-id="949b7-111">SQL을 추적 하려면 `BookServiceContext` 생성자에 다음 코드 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-111">To trace the SQL, add the following line of code to the `BookServiceContext` constructor:</span></span>

[!code-csharp[Main](part-4/samples/sample1.cs)]

<span data-ttu-id="949b7-112">/Sh/ws에 GET 요청을 보내면 다음과 같이 JSON이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-112">If you send a GET request to /api/books, it returns JSON like the following:</span></span>

[!code-console[Main](part-4/samples/sample2.cmd)]

<span data-ttu-id="949b7-113">서적에 유효한 AuthorId 포함 되어 있더라도 Author 속성이 null 인 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-113">You can see that the Author property is null, even though the book contains a valid AuthorId.</span></span> <span data-ttu-id="949b7-114">EF가 관련 된 작성자 엔터티를 로드 하지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-114">That's because EF is not loading the related Author entities.</span></span> <span data-ttu-id="949b7-115">SQL 쿼리의 추적 로그는 다음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-115">The trace log of the SQL query confirms this:</span></span>

[!code-console[Main](part-4/samples/sample3.sql)]

<span data-ttu-id="949b7-116">SELECT 문은 Books 테이블에서 사용 되며 Author 테이블을 참조 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-116">The SELECT statement takes from the Books table, and does not reference the Author table.</span></span>

<span data-ttu-id="949b7-117">참조를 위해 책 목록을 반환 하는 `BooksController` 클래스의 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-117">For reference, here is the method in the `BooksController` class that returns the list of books.</span></span>

[!code-csharp[Main](part-4/samples/sample4.cs)]

<span data-ttu-id="949b7-118">JSON 데이터의 일부로 작성자를 반환할 수 있는 방법을 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-118">Let's see how we can return the Author as part of the JSON data.</span></span> <span data-ttu-id="949b7-119">Entity Framework에서 관련 데이터를 로드 하는 방법에는 즉시 로드, 지연 로드 및 명시적 로드의 세 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-119">There are three ways to load related data in Entity Framework: eager loading, lazy loading, and explicit loading.</span></span> <span data-ttu-id="949b7-120">각 기술과 절충 하 여 작동 방식을 이해 하는 것이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-120">There are trade-offs with each technique, so it's important to understand how they work.</span></span>

### <a name="eager-loading"></a><span data-ttu-id="949b7-121">즉시 로드</span><span class="sxs-lookup"><span data-stu-id="949b7-121">Eager Loading</span></span>

<span data-ttu-id="949b7-122">*즉시 로드*를 사용 하면 EF는 초기 데이터베이스 쿼리의 일부로 관련 엔터티를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-122">With *eager loading*, EF loads related entities as part of the initial database query.</span></span> <span data-ttu-id="949b7-123">즉시 로드를 수행 하려면 System.web. **Include** 확장명 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-123">To perform eager loading, use the **System.Data.Entity.Include** extension method.</span></span>

[!code-csharp[Main](part-4/samples/sample5.cs)]

<span data-ttu-id="949b7-124">이렇게 하면 쿼리에 작성자 데이터가 포함 되도록 EF에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-124">This tells EF to include the Author data in the query.</span></span> <span data-ttu-id="949b7-125">이러한 변경을 수행 하 고 앱을 실행 하는 경우 JSON 데이터는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-125">If you make this change and run the app, now the JSON data looks like this:</span></span>

[!code-console[Main](part-4/samples/sample6.cmd)]

<span data-ttu-id="949b7-126">추적 로그는 EF가 책 및 Author 테이블에 대해 조인을 수행 하는 것을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-126">The trace log shows that EF performed a join on the Book and Author tables.</span></span>

[!code-console[Main](part-4/samples/sample7.cmd)]

### <a name="lazy-loading"></a><span data-ttu-id="949b7-127">지연 로드</span><span class="sxs-lookup"><span data-stu-id="949b7-127">Lazy Loading</span></span>

<span data-ttu-id="949b7-128">지연 로드를 사용 하면 해당 엔터티에 대 한 탐색 속성이 역참조 될 때 EF에서 관련 엔터티를 자동으로 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-128">With lazy loading, EF automatically loads a related entity when the navigation property for that entity is dereferenced.</span></span> <span data-ttu-id="949b7-129">지연 로드를 사용 하려면 탐색 속성을 virtual로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-129">To enable lazy loading, make the navigation property virtual.</span></span> <span data-ttu-id="949b7-130">예를 들어 Book 클래스에서 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-130">For example, in the Book class:</span></span>

[!code-csharp[Main](part-4/samples/sample8.cs?highlight=6)]

<span data-ttu-id="949b7-131">이제 다음 코드를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-131">Now consider the following code:</span></span>

[!code-csharp[Main](part-4/samples/sample9.cs)]

<span data-ttu-id="949b7-132">지연 로드를 사용 하는 경우 `books[0]`의 `Author` 속성에 액세스 하면 EF가 데이터베이스에서 작성자를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-132">When lazy loading is enabled, accessing the `Author` property on `books[0]` causes EF to query the database for the author.</span></span>

<span data-ttu-id="949b7-133">런타임에는 관련 엔터티를 검색할 때마다 쿼리가 전송 되기 때문에 지연 로드에는 여러 데이터베이스를 왕복 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-133">Lazy loading requires multiple database trips, because EF sends a query each time it retrieves a related entity.</span></span> <span data-ttu-id="949b7-134">일반적으로 serialize 하는 개체에 대해 지연 로드를 사용 하지 않도록 설정 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-134">Generally, you want lazy loading disabled for objects that you serialize.</span></span> <span data-ttu-id="949b7-135">Serializer는 관련 엔터티 로드를 트리거하는 모델의 모든 속성을 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-135">The serializer has to read all of the properties on the model, which triggers loading the related entities.</span></span> <span data-ttu-id="949b7-136">예를 들어 EF가 지연 로드를 사용 하도록 설정 된 책 목록을 직렬화 할 때 SQL 쿼리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-136">For example, here are the SQL queries when EF serializes the list of books with lazy loading enabled.</span></span> <span data-ttu-id="949b7-137">EF는 세 개의 저자에 대해 3 개의 개별 쿼리를 수행 하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-137">You can see that EF makes three separate queries for the three authors.</span></span>

[!code-console[Main](part-4/samples/sample10.sql)]

<span data-ttu-id="949b7-138">지연 로드를 사용 해야 하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-138">There are still times when you might want to use lazy loading.</span></span> <span data-ttu-id="949b7-139">즉시 로드 하면 EF가 매우 복잡 한 조인을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-139">Eager loading can cause EF to generate a very complex join.</span></span> <span data-ttu-id="949b7-140">또는 작은 데이터 하위 집합에 대 한 관련 엔터티가 필요할 수 있으며 지연 로드가 더 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-140">Or you might need related entities for a small subset of the data, and lazy loading would be more efficient.</span></span>

<span data-ttu-id="949b7-141">Serialization 문제를 방지 하는 한 가지 방법은 엔터티 개체 대신 Dto (데이터 전송 개체)를 serialize 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-141">One way to avoid serialization problems is to serialize data transfer objects (DTOs) instead of entity objects.</span></span> <span data-ttu-id="949b7-142">이 방법은이 문서의 뒷부분에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-142">I'll show this approach later in the article.</span></span>

### <a name="explicit-loading"></a><span data-ttu-id="949b7-143">명시적 로드</span><span class="sxs-lookup"><span data-stu-id="949b7-143">Explicit Loading</span></span>

<span data-ttu-id="949b7-144">명시적 로드는 코드에서 명시적으로 관련 데이터를 가져오는 것을 제외 하 고는 지연 로드와 비슷합니다. 탐색 속성에 액세스 하는 경우 자동으로 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-144">Explicit loading is similar to lazy loading, except that you explicitly get the related data in code; it doesn't happen automatically when you access a navigation property.</span></span> <span data-ttu-id="949b7-145">명시적 로드를 사용 하면 관련 데이터를 로드 하는 시기를 보다 세밀 하 게 제어할 수 있지만 추가 코드가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-145">Explicit loading gives you more control over when to load related data, but requires extra code.</span></span> <span data-ttu-id="949b7-146">명시적 로드에 대 한 자세한 내용은 [관련 엔터티 로드](https://msdn.microsoft.com/data/jj574232#explicit)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="949b7-146">For more information about explicit loading, see [Loading Related Entities](https://msdn.microsoft.com/data/jj574232#explicit).</span></span>

## <a name="navigation-properties-and-circular-references"></a><span data-ttu-id="949b7-147">탐색 속성 및 순환 참조</span><span class="sxs-lookup"><span data-stu-id="949b7-147">Navigation Properties and Circular References</span></span>

<span data-ttu-id="949b7-148">Book 및 Author 모델을 정의한 경우 책 작성자 관계에 대 한 `Book` 클래스에 탐색 속성을 정의 했지만 다른 방향으로 탐색 속성을 정의 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-148">When I defined the Book and Author models, I defined a navigation property on the `Book` class for the Book-Author relationship, but I did not define a navigation property in the other direction.</span></span>

<span data-ttu-id="949b7-149">`Author` 클래스에 해당 탐색 속성을 추가 하면 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="949b7-149">What happens if you add the corresponding navigation property to the `Author` class?</span></span>

[!code-csharp[Main](part-4/samples/sample11.cs?highlight=7)]

<span data-ttu-id="949b7-150">그러나 이렇게 하면 모델을 serialize 할 때 문제가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-150">Unfortunately, this creates a problem when you serialize the models.</span></span> <span data-ttu-id="949b7-151">관련 데이터를 로드 하는 경우 순환 개체 그래프가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-151">If you load the related data, it creates a circular object graph.</span></span>

![](part-4/_static/image1.png)

<span data-ttu-id="949b7-152">JSON 또는 XML 포맷터가 그래프를 serialize 하려고 하면 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-152">When the JSON or XML formatter tries to serialize the graph, it will throw an exception.</span></span> <span data-ttu-id="949b7-153">두 포맷터는 서로 다른 예외 메시지를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-153">The two formatters throw different exception messages.</span></span> <span data-ttu-id="949b7-154">JSON 포맷터의 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-154">Here is an example for the JSON formatter:</span></span>

[!code-console[Main](part-4/samples/sample12.cmd)]

<span data-ttu-id="949b7-155">XML 포맷터는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-155">Here is the XML formatter:</span></span>

[!code-xml[Main](part-4/samples/sample13.xml)]

<span data-ttu-id="949b7-156">한 가지 해결 방법은 다음 섹션에서 설명 하는 Dto을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-156">One solution is to use DTOs, which I describe in the next section.</span></span> <span data-ttu-id="949b7-157">또는 JSON 및 XML 포맷터를 구성 하 여 그래프 순환을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-157">Alternatively, you can configure the JSON and XML formatters to handle graph cycles.</span></span> <span data-ttu-id="949b7-158">자세한 내용은 [순환 개체 참조 처리](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="949b7-158">For more information, see [Handling Circular Object References](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).</span></span>

<span data-ttu-id="949b7-159">이 자습서에서는 `Author.Book` 탐색 속성이 필요 하지 않으므로 그대로 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="949b7-159">For this tutorial, you don't need the `Author.Book` navigation property, so you can leave it out.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="949b7-160">[이전](part-3.md)
> [다음](part-5.md)</span><span class="sxs-lookup"><span data-stu-id="949b7-160">[Previous](part-3.md)
[Next](part-5.md)</span></span>
