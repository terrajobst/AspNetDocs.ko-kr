---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-2
title: 모델 및 컨트롤러 추가 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 88908ff8-51a9-40eb-931c-a8139128b680
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-2
msc.type: authoredcontent
ms.openlocfilehash: 57dacda421968f341284d89c9a3ad80040c16e25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449189"
---
# <a name="add-models-and-controllers"></a><span data-ttu-id="30397-102">모델 및 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="30397-102">Add Models and Controllers</span></span>

<span data-ttu-id="30397-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="30397-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="30397-104">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="30397-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="30397-105">이 섹션에서는 데이터베이스 엔터티를 정의 하는 모델 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-105">In this section, you will add model classes that define the database entities.</span></span> <span data-ttu-id="30397-106">그런 다음 해당 엔터티에 대 한 CRUD 작업을 수행 하는 Web API 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-106">Then you will add Web API controllers that perform CRUD operations on those entities.</span></span>

## <a name="add-model-classes"></a><span data-ttu-id="30397-107">모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="30397-107">Add Model Classes</span></span>

<span data-ttu-id="30397-108">이 자습서에서는 EF (Entity Framework)에 대 한 "Code First" 접근 방법을 사용 하 여 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30397-108">In this tutorial, we'll create the database by using the "Code First" approach to Entity Framework (EF).</span></span> <span data-ttu-id="30397-109">Code First를 사용 하 여 C# 데이터베이스 테이블에 해당 하는 클래스를 작성 하 고 EF는 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30397-109">With Code First, you write C# classes that correspond to database tables, and EF creates the database.</span></span> <span data-ttu-id="30397-110">자세한 내용은 [Entity Framework 개발 방법](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="30397-110">(For more information, see [Entity Framework Development Approaches](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf).)</span></span>

<span data-ttu-id="30397-111">도메인 개체를 POCOs (일반-이전 CLR 개체)로 정의 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-111">We start by defining our domain objects as POCOs (plain-old CLR objects).</span></span> <span data-ttu-id="30397-112">다음 POCOs를 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30397-112">We will create the following POCOs:</span></span>

- <span data-ttu-id="30397-113">작성자</span><span class="sxs-lookup"><span data-stu-id="30397-113">Author</span></span>
- <span data-ttu-id="30397-114">Book</span><span class="sxs-lookup"><span data-stu-id="30397-114">Book</span></span>

<span data-ttu-id="30397-115">솔루션 탐색기에서 모델 폴더를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-115">In Solution Explorer, right click the Models folder.</span></span> <span data-ttu-id="30397-116">**추가**를 선택한 다음 **클래스**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-116">Select **Add**, then select **Class**.</span></span> <span data-ttu-id="30397-117">클래스 `Author` 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-117">Name the class `Author`.</span></span>

![](part-2/_static/image1.png)

<span data-ttu-id="30397-118">Author.cs의 모든 상용구 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="30397-118">Replace all of the boilerplate code in Author.cs with the following code.</span></span>

[!code-csharp[Main](part-2/samples/sample1.cs)]

<span data-ttu-id="30397-119">다음 코드를 사용 하 여 `Book`라는 다른 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-119">Add another class named `Book`, with the following code.</span></span>

[!code-csharp[Main](part-2/samples/sample2.cs)]

<span data-ttu-id="30397-120">Entity Framework은 이러한 모델을 사용 하 여 데이터베이스 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30397-120">Entity Framework will use these models to create database tables.</span></span> <span data-ttu-id="30397-121">각 모델에 대해 `Id` 속성은 데이터베이스 테이블의 기본 키 열이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30397-121">For each model, the `Id` property will become the primary key column of the database table.</span></span>

<span data-ttu-id="30397-122">Book 클래스에서 `AuthorId`는 `Author` 테이블에 외래 키를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-122">In the Book class, the `AuthorId` defines a foreign key into the `Author` table.</span></span> <span data-ttu-id="30397-123">(간단히 하기 위해 각 책에 단일 저자가 있다고 가정 합니다.) Book 클래스에는 관련 된 `Author`에 대 한 탐색 속성도 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30397-123">(For simplicity, I'm assuming that each book has a single author.) The book class also contains a navigation property to the related `Author`.</span></span> <span data-ttu-id="30397-124">탐색 속성을 사용 하 여 코드에서 관련 `Author`에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30397-124">You can use the navigation property to access the related `Author` in code.</span></span> <span data-ttu-id="30397-125">4 부의 탐색 속성에 대해 자세히 언급 하 고 [엔터티 관계를 처리](part-4.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-125">I say more about navigation properties in part 4, [Handling Entity Relations](part-4.md).</span></span>

## <a name="add-web-api-controllers"></a><span data-ttu-id="30397-126">Web API 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="30397-126">Add Web API Controllers</span></span>

<span data-ttu-id="30397-127">이 섹션에서는 CRUD 작업 (만들기, 읽기, 업데이트 및 삭제)을 지 원하는 Web API 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-127">In this section, we'll add Web API controllers that support CRUD operations (create, read, update, and delete).</span></span> <span data-ttu-id="30397-128">컨트롤러는 Entity Framework을 사용 하 여 데이터베이스 계층과 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-128">The controllers will use Entity Framework to communicate with the database layer.</span></span>

<span data-ttu-id="30397-129">먼저 file controller/Valuecontroller .cs를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30397-129">First, you can delete the file Controllers/ValuesController.cs.</span></span> <span data-ttu-id="30397-130">이 파일에는 웹 API 컨트롤러의 예가 포함 되어 있지만이 자습서에서는 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30397-130">This file contains an example Web API controller, but you don't need it for this tutorial.</span></span>

![](part-2/_static/image2.png)

<span data-ttu-id="30397-131">다음으로 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-131">Next, build the project.</span></span> <span data-ttu-id="30397-132">웹 API 스 캐 폴딩은 리플렉션을 사용 하 여 모델 클래스를 찾습니다. 따라서 컴파일된 어셈블리가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-132">The Web API scaffolding uses reflection to find the model classes, so it needs the compiled assembly.</span></span>

<span data-ttu-id="30397-133">솔루션 탐색기에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-133">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="30397-134">**추가**를 선택한 다음 **컨트롤러**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-134">Select **Add**, then select **Controller**.</span></span>

![](part-2/_static/image3.png)

<span data-ttu-id="30397-135">**스 캐 폴드 추가** 대화 상자에서 "작업을 사용 하는 웹 API 2 컨트롤러, Entity Framework 사용"을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-135">In the **Add Scaffold** dialog, select "Web API 2 Controller with actions, using Entity Framework".</span></span> <span data-ttu-id="30397-136">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-136">Click **Add**.</span></span>

![](part-2/_static/image4.png)

<span data-ttu-id="30397-137">**컨트롤러 추가** 대화 상자에서 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-137">In the **Add Controller** dialog, do the following:</span></span>

1. <span data-ttu-id="30397-138">**모델 클래스** 드롭다운에서 `Author` 클래스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-138">In the **Model class** dropdown, select the `Author` class.</span></span> <span data-ttu-id="30397-139">드롭다운 목록에 표시 되지 않는 경우 프로젝트를 빌드 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-139">(If you don't see it listed in the dropdown, make sure that you built the project.)</span></span>
2. <span data-ttu-id="30397-140">"비동기 컨트롤러 작업 사용"을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-140">Check "Use async controller actions".</span></span>
3. <span data-ttu-id="30397-141">컨트롤러 이름을 &quot;AuthorsController&quot;으로 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="30397-141">Leave the controller name as &quot;AuthorsController&quot;.</span></span>
4. <span data-ttu-id="30397-142">**데이터 컨텍스트 클래스**옆에 있는 더하기 (+) 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-142">Click plus (+) button next to **Data Context Class**.</span></span>

![](part-2/_static/image5.png)

<span data-ttu-id="30397-143">**새 데이터 컨텍스트** 대화 상자에서 기본 이름을 그대로 두고 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-143">In the **New Data Context** dialog, leave the default name and click **Add**.</span></span>

![](part-2/_static/image6.png)

<span data-ttu-id="30397-144">**추가** 를 클릭 하 여 **컨트롤러 추가** 대화 상자를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-144">Click **Add** to complete the **Add Controller** dialog.</span></span> <span data-ttu-id="30397-145">대화 상자에서 프로젝트에 두 개의 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-145">The dialog adds two classes to your project:</span></span>

- <span data-ttu-id="30397-146">`AuthorsController`는 Web API 컨트롤러를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-146">`AuthorsController` defines a Web API controller.</span></span> <span data-ttu-id="30397-147">컨트롤러는 클라이언트가 저자 목록에서 CRUD 작업을 수행 하는 데 사용 하는 REST API를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-147">The controller implements the REST API that clients use to perform CRUD operations on the list of authors.</span></span>
- <span data-ttu-id="30397-148">`BookServiceContext`는 런타임에 데이터베이스의 데이터로 개체 채우기, 변경 내용 추적 및 데이터베이스에 데이터 유지를 포함 하는 엔터티 개체를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-148">`BookServiceContext` manages entity objects during run time, which includes populating objects with data from a database, change tracking, and persisting data to the database.</span></span> <span data-ttu-id="30397-149">`DbContext`에서 상속받습니다.</span><span class="sxs-lookup"><span data-stu-id="30397-149">It inherits from `DbContext`.</span></span>

![](part-2/_static/image7.png)

<span data-ttu-id="30397-150">이제 프로젝트를 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-150">At this point, build the project again.</span></span> <span data-ttu-id="30397-151">이제 동일한 단계를 수행 하 여 `Book` 엔터티에 대 한 API 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-151">Now go through the same steps to add an API controller for `Book` entities.</span></span> <span data-ttu-id="30397-152">이번에는 모델 클래스에 대해 `Book`를 선택 하 고 데이터 컨텍스트 클래스에 대해 기존 `BookServiceContext` 클래스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-152">This time, select `Book` for the model class, and select the existing `BookServiceContext` class for the data context class.</span></span> <span data-ttu-id="30397-153">새 데이터 컨텍스트를 만들지 마세요. **추가** 를 클릭 하 여 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="30397-153">(Don't create a new data context.) Click **Add** to add the controller.</span></span>

![](part-2/_static/image8.png)

> [!div class="step-by-step"]
> <span data-ttu-id="30397-154">[이전](part-1.md)
> [다음](part-3.md)</span><span class="sxs-lookup"><span data-stu-id="30397-154">[Previous](part-1.md)
[Next](part-3.md)</span></span>
