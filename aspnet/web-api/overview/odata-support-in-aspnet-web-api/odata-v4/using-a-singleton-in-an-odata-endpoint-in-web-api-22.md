---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
title: Web API 2.2를 사용 하 여 OData v4에서 단일 항목 만들기 Microsoft Docs
author: rick-anderson
description: 이 항목에서는 Web API 2.2의 OData 끝점에서 단일 항목을 정의 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 4064ab14-26ee-4d5c-ae58-1bdda525ad06
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 218449c18759b306e425c55f8e7b573d837b4658
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504503"
---
# <a name="create-a-singleton-in-odata-v4-using-web-api-22"></a><span data-ttu-id="85913-103">Web API 2.2를 사용 하 여 OData v4에서 단일 항목 만들기</span><span class="sxs-lookup"><span data-stu-id="85913-103">Create a Singleton in OData v4 Using Web API 2.2</span></span>

<span data-ttu-id="85913-104">Zoe 루 오 어</span><span class="sxs-lookup"><span data-stu-id="85913-104">by Zoe Luo</span></span>

> <span data-ttu-id="85913-105">일반적으로 엔터티는 엔터티 집합 내에 캡슐화 된 경우에만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85913-105">Traditionally, an entity could only be accessed if it were encapsulated inside an entity set.</span></span> <span data-ttu-id="85913-106">그러나 OData v4는 두 가지 추가 옵션인 Singleton과 포함을 제공 하며, 둘 다 WebAPI 2.2에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85913-106">But OData v4 provides two additional options, Singleton and Containment, both of which WebAPI 2.2 supports.</span></span>

<span data-ttu-id="85913-107">이 문서에서는 Web API 2.2의 OData 끝점에서 단일 항목을 정의 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="85913-107">This article shows how to define a singleton in an OData endpoint in Web API 2.2.</span></span> <span data-ttu-id="85913-108">Singleton 이란 무엇이 고이를 사용 하 여 이점을 얻는 방법에 대 한 자세한 내용은 단일 항목을 [사용 하 여 특수 엔터티 정의](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="85913-108">For information on what a singleton is and how you can benefit from using it, see [Using a singleton to define your special entity](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx).</span></span> <span data-ttu-id="85913-109">Web API에서 OData V4 끝점을 만들려면 [ASP.NET Web API 2.2를 사용 하 여 odata V4 엔드포인트 만들기](create-an-odata-v4-endpoint.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="85913-109">To create an OData V4 endpoint in Web API, see [Create an OData v4 Endpoint Using ASP.NET Web API 2.2](create-an-odata-v4-endpoint.md).</span></span> 

<span data-ttu-id="85913-110">다음 데이터 모델을 사용 하 여 Web API 프로젝트에서 단일 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85913-110">We'll create a singleton in your Web API project using the following data model:</span></span>

![데이터 모델](using-a-singleton-in-an-odata-endpoint-in-web-api-22/_static/image1.png)

<span data-ttu-id="85913-112">`Umbrella` 이라는 singleton은 형식 `Company`를 기반으로 정의 되며 `Employees` 라는 엔터티 집합은 `Employee`형식에 따라 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85913-112">A singleton named `Umbrella` will be defined based on type `Company`, and an entity set named `Employees` will be defined based on type `Employee`.</span></span>

<span data-ttu-id="85913-113">이 자습서에서 사용 되는 솔루션은 [CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85913-113">The solution used in this tutorial can be downloaded from [CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/).</span></span>

## <a name="define-the-data-model"></a><span data-ttu-id="85913-114">데이터 모델 정의</span><span class="sxs-lookup"><span data-stu-id="85913-114">Define the data model</span></span>

1. <span data-ttu-id="85913-115">CLR 형식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="85913-115">Define the CLR types.</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample1.cs)]
2. <span data-ttu-id="85913-116">CLR 형식에 따라 EDM 모델을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="85913-116">Generate the EDM model based on the CLR types.</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample2.cs)]

    <span data-ttu-id="85913-117">여기서 `builder.Singleton<Company>("Umbrella")`는 모델 작성기에 EDM 모델에 `Umbrella` 라는 singleton을 만들도록 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="85913-117">Here, `builder.Singleton<Company>("Umbrella")` tells the model builder to create a singleton named `Umbrella` in the EDM model.</span></span>

    <span data-ttu-id="85913-118">생성 되는 메타 데이터는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="85913-118">The generated metadata will look like the following:</span></span>

    [!code-xml[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample3.xml)]

    <span data-ttu-id="85913-119">메타 데이터에서 `Employees` 엔터티 집합에 `Company` 탐색 속성이 singleton `Umbrella`에 바인딩되어 있음을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85913-119">From the metadata we can see that the navigation property `Company` in the `Employees` entity set is bound to the singleton `Umbrella`.</span></span> <span data-ttu-id="85913-120">`Umbrella`에 `Company` 형식이 있으므로 `ODataConventionModelBuilder`에 의해 바인딩이 자동으로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85913-120">The binding is done automatically by `ODataConventionModelBuilder`, since only `Umbrella` has the `Company` type.</span></span> <span data-ttu-id="85913-121">모델에 모호성이 있는 경우 `HasSingletonBinding`를 사용 하 여 탐색 속성을 singleton에 명시적으로 바인딩할 수 있습니다. `HasSingletonBinding` CLR 형식 정의에서 `Singleton` 특성을 사용 하는 것과 동일한 효과가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85913-121">If there is any ambiguity in the model, you can use `HasSingletonBinding` to explicitly bind a navigation property to a singleton; `HasSingletonBinding` has the same effect as using the `Singleton` attribute in the CLR type definition:</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample4.cs)]

## <a name="define-the-singleton-controller"></a><span data-ttu-id="85913-122">Singleton 컨트롤러 정의</span><span class="sxs-lookup"><span data-stu-id="85913-122">Define the singleton controller</span></span>

<span data-ttu-id="85913-123">EntitySet 컨트롤러와 마찬가지로 singleton 컨트롤러는 `ODataController`에서 상속 되며 singleton 컨트롤러 이름은 `[singletonName]Controller`해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85913-123">Like the EntitySet controller, the singleton controller inherits from `ODataController`, and the singleton controller name should be `[singletonName]Controller`.</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample5.cs)]

<span data-ttu-id="85913-124">다른 종류의 요청을 처리 하기 위해 작업은 컨트롤러에 미리 정의 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85913-124">In order to handle different kinds of requests, actions are required to be pre-defined in the controller.</span></span> <span data-ttu-id="85913-125">WebApi 2.2에서는 기본적으로 **특성 라우팅이** 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85913-125">**Attribute routing** is enabled by default in WebApi 2.2.</span></span> <span data-ttu-id="85913-126">예를 들어 특성 라우팅을 사용 하 여 `Company`에서 `Revenue` 쿼리를 처리 하는 작업을 정의 하려면 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="85913-126">For example, to define an action to handle querying `Revenue` from `Company` using attribute routing, use the following:</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample6.cs)]

<span data-ttu-id="85913-127">각 동작에 대 한 특성을 정의 하지 않으려는 경우 다음 [OData 라우팅 규칙](../odata-routing-conventions.md)에 따라 작업을 정의 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85913-127">If you are not willing to define attributes for each action, just define your actions following [OData Routing Conventions](../odata-routing-conventions.md).</span></span> <span data-ttu-id="85913-128">Singleton을 쿼리 하는 데는 키가 필요 하지 않으므로 singleton 컨트롤러에 정의 된 작업은 entityset 컨트롤러에 정의 된 동작과 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="85913-128">Since a key is not required for querying a singleton, the actions defined in the singleton controller are slightly different from actions defined in the entityset controller.</span></span>

<span data-ttu-id="85913-129">참조를 위해 singleton 컨트롤러의 모든 작업 정의에 대 한 메서드 시그니처는 아래에 나열 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85913-129">For reference, method signatures for every action definition in the singleton controller are listed below.</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample7.cs)]

<span data-ttu-id="85913-130">기본적으로이 작업은 서비스 쪽에서 수행 해야 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="85913-130">Basically, this is all you need to do on the service side.</span></span> <span data-ttu-id="85913-131">[샘플 프로젝트](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/) 에는 솔루션에 대 한 모든 코드와 단일 항목을 사용 하는 방법을 보여 주는 OData 클라이언트가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85913-131">The [sample project](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/) contains all of the code for the solution and the OData client that shows how to use the singleton.</span></span> <span data-ttu-id="85913-132">클라이언트는 [OData V4 클라이언트 앱 만들기](create-an-odata-v4-client-app.md)의 단계에 따라 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="85913-132">The client is built by following the steps in [Create an OData v4 Client App](create-an-odata-v4-client-app.md).</span></span>

<span data-ttu-id="85913-133">.</span><span class="sxs-lookup"><span data-stu-id="85913-133">.</span></span> 

<span data-ttu-id="85913-134">*이 문서의 원래 내용에 대 한 Leo Hu-hu을 주셔서 감사 합니다.*</span><span class="sxs-lookup"><span data-stu-id="85913-134">*Thanks to Leo Hu for the original content of this article.*</span></span>
