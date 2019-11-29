---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
title: '2 부: 도메인 모델 만들기 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: fe3ef85f-bdc6-4e10-9768-25aa565c01d0
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
msc.type: authoredcontent
ms.openlocfilehash: 7c5ed1bdb4b390c94907b14e208231f16ad42d96
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600363"
---
# <a name="part-2-creating-the-domain-models"></a><span data-ttu-id="f0c18-102">2 부: 도메인 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="f0c18-102">Part 2: Creating the Domain Models</span></span>

<span data-ttu-id="f0c18-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="f0c18-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="f0c18-104">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="f0c18-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-models"></a><span data-ttu-id="f0c18-105">모델 추가</span><span class="sxs-lookup"><span data-stu-id="f0c18-105">Add Models</span></span>

<span data-ttu-id="f0c18-106">Entity Framework 접근 하는 방법에는 다음 세 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-106">There are three ways to approach Entity Framework:</span></span>

- <span data-ttu-id="f0c18-107">데이터베이스 우선: 데이터베이스에서 시작 하 Entity Framework 코드를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-107">Database-first: You start with a database, and Entity Framework generates the code.</span></span>
- <span data-ttu-id="f0c18-108">모델 우선: 시각적 모델로 시작 하 고 Entity Framework는 데이터베이스와 코드를 모두 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-108">Model-first: You start with a visual model, and Entity Framework generates both the database and code.</span></span>
- <span data-ttu-id="f0c18-109">코드 우선: 코드로 시작 하 고 Entity Framework는 데이터베이스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-109">Code-first: You start with code, and Entity Framework generates the database.</span></span>

<span data-ttu-id="f0c18-110">코드 우선 방법을 사용 하 고 있으므로 도메인 개체를 POCOs (일반-이전 CLR 개체)로 정의 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-110">We are using the code-first approach, so we start by defining our domain objects as POCOs (plain-old CLR objects).</span></span> <span data-ttu-id="f0c18-111">코드 우선 방법을 사용 하면 도메인 개체는 트랜잭션 또는 지 속성 같은 데이터베이스 계층을 지원 하기 위해 추가 코드가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-111">With the code-first approach, domain objects don't need any extra code to support the database layer, such as transactions or persistence.</span></span> <span data-ttu-id="f0c18-112">특히 [Entityobject](https://msdn.microsoft.com/library/system.data.objects.dataclasses.entityobject.aspx) 클래스에서 상속할 필요가 없습니다. 데이터 주석을 사용 하 여 Entity Framework 데이터베이스 스키마를 만드는 방법을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-112">(Specifically, they do not need to inherit from the [EntityObject](https://msdn.microsoft.com/library/system.data.objects.dataclasses.entityobject.aspx) class.) You can still use data annotations to control how Entity Framework creates the database schema.</span></span>

<span data-ttu-id="f0c18-113">POCOs는 [데이터베이스 상태](https://msdn.microsoft.com/library/system.data.entitystate.aspx)를 설명 하는 추가 속성을 수행 하지 않으므로 JSON 또는 XML로 쉽게 serialize 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-113">Because POCOs do not carry any extra properties that describe [database state](https://msdn.microsoft.com/library/system.data.entitystate.aspx), they can easily be serialized to JSON or XML.</span></span> <span data-ttu-id="f0c18-114">그러나이는 자습서의 뒷부분에서 볼 수 있는 것 처럼 항상 Entity Framework 모델을 클라이언트에 직접 노출 하는 것을 의미 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-114">However, that does not mean you should always expose your Entity Framework models directly to clients, as we'll see later in the tutorial.</span></span>

<span data-ttu-id="f0c18-115">다음 POCOs를 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-115">We will create the following POCOs:</span></span>

- <span data-ttu-id="f0c18-116">제품</span><span class="sxs-lookup"><span data-stu-id="f0c18-116">Product</span></span>
- <span data-ttu-id="f0c18-117">Order</span><span class="sxs-lookup"><span data-stu-id="f0c18-117">Order</span></span>
- <span data-ttu-id="f0c18-118">OrderDetail</span><span class="sxs-lookup"><span data-stu-id="f0c18-118">OrderDetail</span></span>

<span data-ttu-id="f0c18-119">각 클래스를 만들려면 솔루션 탐색기의 모델 폴더를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-119">To create each class, right-click the Models folder in Solution Explorer.</span></span> <span data-ttu-id="f0c18-120">상황에 맞는 메뉴에서 **추가** 를 선택한 다음 클래스를 선택 **합니다.**</span><span class="sxs-lookup"><span data-stu-id="f0c18-120">From the context menu, select **Add** and then select **Class.**</span></span>

![](using-web-api-with-entity-framework-part-2/_static/image1.png)

<span data-ttu-id="f0c18-121">다음 구현을 사용 하 여 `Product` 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-121">Add a `Product` class with the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample1.cs)]

<span data-ttu-id="f0c18-122">규칙에 따라 Entity Framework는 `Id` 속성을 기본 키로 사용 하 여 데이터베이스 테이블의 id 열에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-122">By convention, Entity Framework uses the `Id` property as the primary key and maps it to an identity column in the database table.</span></span> <span data-ttu-id="f0c18-123">새 `Product` 인스턴스를 만들 때 데이터베이스에서 값을 생성 하기 때문에 `Id`에 대 한 값을 설정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-123">When you create a new `Product` instance, you won't set a value for `Id`, because the database generates the value.</span></span>

<span data-ttu-id="f0c18-124">**ScaffoldColumn** 특성은 편집기 폼을 생성할 때 ASP.NET MVC에 게 `Id` 속성을 건너뛰도록 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-124">The **ScaffoldColumn** attribute tells ASP.NET MVC to skip the `Id` property when generating an editor form.</span></span> <span data-ttu-id="f0c18-125">**Required** 특성은 모델의 유효성을 검사 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-125">The **Required** attribute is used to validate the model.</span></span> <span data-ttu-id="f0c18-126">`Name` 속성이 비어 있지 않은 문자열 이어야 함을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-126">It specifies that the `Name` property must be a non-empty string.</span></span>

<span data-ttu-id="f0c18-127">`Order` 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-127">Add the `Order` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample2.cs)]

<span data-ttu-id="f0c18-128">`OrderDetail` 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-128">Add the `OrderDetail` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample3.cs)]

## <a name="foreign-key-relations"></a><span data-ttu-id="f0c18-129">외래 키 관계</span><span class="sxs-lookup"><span data-stu-id="f0c18-129">Foreign Key Relations</span></span>

<span data-ttu-id="f0c18-130">주문에는 여러 주문 정보가 포함 되며, 각 주문 정보는 단일 제품을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-130">An order contains many order details, and each order detail refers to a single product.</span></span> <span data-ttu-id="f0c18-131">이러한 관계를 나타내기 위해 `OrderDetail` 클래스는 `OrderId` 및 `ProductId`라는 속성을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-131">To represent these relations, the `OrderDetail` class defines properties named `OrderId` and `ProductId`.</span></span> <span data-ttu-id="f0c18-132">Entity Framework은 이러한 속성이 외래 키를 나타내는 것으로 유추 하 고 데이터베이스에 외래 키 제약 조건을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-132">Entity Framework will infer that these properties represent foreign keys, and will add foreign-key constraints to the database.</span></span>

![](using-web-api-with-entity-framework-part-2/_static/image2.png)

<span data-ttu-id="f0c18-133">`Order` 및 `OrderDetail` 클래스에는 관련 개체에 대 한 참조를 포함 하는 "탐색" 속성도 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-133">The `Order` and `OrderDetail` classes also include "navigation" properties, which contain references to the related objects.</span></span> <span data-ttu-id="f0c18-134">주문이 제공 되 면 탐색 속성을 따라 주문에서 제품으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-134">Given an order, you can navigate to the products in the order by following the navigation properties.</span></span>

<span data-ttu-id="f0c18-135">이제 프로젝트를 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-135">Compile the project now.</span></span> <span data-ttu-id="f0c18-136">Entity Framework는 리플렉션을 사용 하 여 모델의 속성을 검색 하므로 데이터베이스 스키마를 만들기 위해 컴파일된 어셈블리가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-136">Entity Framework uses reflection to discover the properties of the models, so it requires a compiled assembly to create the database schema.</span></span>

## <a name="configure-the-media-type-formatters"></a><span data-ttu-id="f0c18-137">미디어 유형 포맷터 구성</span><span class="sxs-lookup"><span data-stu-id="f0c18-137">Configure the Media-Type Formatters</span></span>

<span data-ttu-id="f0c18-138">[미디어 형식 포맷터](../../formats-and-model-binding/media-formatters.md) 는 Web API가 HTTP 응답 본문을 쓸 때 데이터를 serialize 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-138">A [media-type formatter](../../formats-and-model-binding/media-formatters.md) is an object that serializes your data when Web API writes the HTTP response body.</span></span> <span data-ttu-id="f0c18-139">기본 제공 포맷터는 JSON 및 XML 출력을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-139">The built-in formatters support JSON and XML output.</span></span> <span data-ttu-id="f0c18-140">기본적으로 이러한 포맷터는 모두 값으로 모든 개체를 직렬화 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-140">By default, both of these formatters serialize all objects by value.</span></span>

<span data-ttu-id="f0c18-141">값으로 직렬화는 개체 그래프에 순환 참조가 포함 된 경우 문제를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-141">Serialization by value creates a problem if an object graph contains circular references.</span></span> <span data-ttu-id="f0c18-142">이는 `Order` 및 `OrderDetail` 클래스에 대 한 참조가 며 각 클래스에 대 한 참조를 포함 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-142">That's exactly the case with the `Order` and `OrderDetail` classes, because each holds a reference to the other.</span></span> <span data-ttu-id="f0c18-143">포맷터는 참조를 따르고 각 개체를 값으로 쓰고 원으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-143">The formatter will follow the references, writing each object by value, and go in circles.</span></span> <span data-ttu-id="f0c18-144">따라서 기본 동작을 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-144">Therefore, we need to change the default behavior.</span></span>

<span data-ttu-id="f0c18-145">솔루션 탐색기에서 앱\_시작 폴더를 확장 하 고 이름이 WebApiConfig.cs 인 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-145">In Solution Explorer, expand the App\_Start folder and open the file named WebApiConfig.cs.</span></span> <span data-ttu-id="f0c18-146">`WebApiConfig` 클래스에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-146">Add the following code to the `WebApiConfig` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample4.cs?highlight=11)]

<span data-ttu-id="f0c18-147">이 코드는 개체 참조를 유지 하도록 JSON 포맷터를 설정 하 고 파이프라인에서 XML 포맷터를 완전히 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-147">This code sets the JSON formatter to preserve object references, and removes the XML formatter from the pipeline entirely.</span></span> <span data-ttu-id="f0c18-148">(개체 참조를 유지 하도록 XML 포맷터를 구성할 수 있지만이 응용 프로그램에 대 한 JSON만 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0c18-148">(You can configure the XML formatter to preserve object references, but it's a little more work, and we only need JSON for this application.</span></span> <span data-ttu-id="f0c18-149">자세한 내용은 [순환 개체 참조 처리](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f0c18-149">For more information, see [Handling Circular Object References](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f0c18-150">[이전](using-web-api-with-entity-framework-part-1.md)
> [다음](using-web-api-with-entity-framework-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="f0c18-150">[Previous](using-web-api-with-entity-framework-part-1.md)
[Next](using-web-api-with-entity-framework-part-3.md)</span></span>
