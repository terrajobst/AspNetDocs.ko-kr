---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
title: '3 부: 관리 컨트롤러 만들기 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 6b9ae3c4-0274-4170-a1bb-9df9c546b2a9
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
msc.type: authoredcontent
ms.openlocfilehash: f39be7a84e85db93487d246e9f8cb59c401fe5ce
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447911"
---
# <a name="part-3-creating-an-admin-controller"></a><span data-ttu-id="1e97b-102">3 부: 관리 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="1e97b-102">Part 3: Creating an Admin Controller</span></span>

<span data-ttu-id="1e97b-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="1e97b-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="1e97b-104">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="1e97b-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-controller"></a><span data-ttu-id="1e97b-105">관리 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="1e97b-105">Add an Admin Controller</span></span>

<span data-ttu-id="1e97b-106">이 섹션에서는 제품에 대 한 CRUD (만들기, 읽기, 업데이트 및 삭제) 작업을 지 원하는 Web API 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-106">In this section, we'll add a Web API controller that supports CRUD (create, read, update, and delete) operations on products.</span></span> <span data-ttu-id="1e97b-107">컨트롤러는 Entity Framework을 사용 하 여 데이터베이스 계층과 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-107">The controller will use Entity Framework to communicate with the database layer.</span></span> <span data-ttu-id="1e97b-108">관리자만이 컨트롤러를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-108">Only administrators will be able to use this controller.</span></span> <span data-ttu-id="1e97b-109">고객은 다른 컨트롤러를 통해 제품에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-109">Customers will access the products through another controller.</span></span>

<span data-ttu-id="1e97b-110">솔루션 탐색기에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-110">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="1e97b-111">**추가** 를 선택 하 고 **컨트롤러**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-111">Select **Add** and then **Controller**.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image1.png)

<span data-ttu-id="1e97b-112">**컨트롤러 추가** 대화 상자에서 컨트롤러 이름을 `AdminController`로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-112">In the **Add Controller** dialog, name the controller `AdminController`.</span></span> <span data-ttu-id="1e97b-113">**템플릿**에서 Entity Framework&quot;를 사용 하 여 읽기/쓰기 동작이 포함 된 &quot;API 컨트롤러를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-113">Under **Template**, select &quot;API controller with read/write actions, using Entity Framework&quot;.</span></span> <span data-ttu-id="1e97b-114">**모델 클래스**에서 "Product (제품명)"를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-114">Under **Model class**, select "Product (ProductStore.Models)".</span></span> <span data-ttu-id="1e97b-115">**데이터 컨텍스트**아래에서 "&lt;새 데이터 컨텍스트&gt;"를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-115">Under **Data Context**, select "&lt;New Data Context&gt;".</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="1e97b-116">**모델 클래스** 드롭다운이 모델 클래스를 표시 하지 않는 경우 프로젝트를 컴파일 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-116">If the **Model class** drop-down does not show any model classes, make sure you compiled the project.</span></span> <span data-ttu-id="1e97b-117">Entity Framework는 리플렉션을 사용 하므로 컴파일된 어셈블리가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-117">Entity Framework uses reflection, so it needs the compiled assembly.</span></span>

<span data-ttu-id="1e97b-118">"&lt;새 데이터 컨텍스트&gt;"를 선택 하면 **새 데이터 컨텍스트** 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-118">Selecting "&lt;New Data Context&gt;" will open the **New Data Context** dialog.</span></span> <span data-ttu-id="1e97b-119">데이터 컨텍스트 이름을 `ProductStore.Models.OrdersContext`로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-119">Name the data context `ProductStore.Models.OrdersContext`.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image3.png)

<span data-ttu-id="1e97b-120">**확인** 을 클릭 하 여 **새 데이터 컨텍스트** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-120">Click **OK** to dismiss the **New Data Context** dialog.</span></span> <span data-ttu-id="1e97b-121">**컨트롤러 추가** 대화 상자에서 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-121">In the **Add Controller** dialog, click **Add**.</span></span>

<span data-ttu-id="1e97b-122">프로젝트에 추가 된 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-122">Here's what got added to the project:</span></span>

- <span data-ttu-id="1e97b-123">**DbContext**에서 파생 되는 `OrdersContext` 라는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-123">A class named `OrdersContext` that derives from **DbContext**.</span></span> <span data-ttu-id="1e97b-124">이 클래스는 POCO 모델과 데이터베이스 간의 붙이기를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-124">This class provides the glue between the POCO models and the database.</span></span>
- <span data-ttu-id="1e97b-125">`AdminController`이라는 웹 API 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="1e97b-125">A Web API controller named `AdminController`.</span></span> <span data-ttu-id="1e97b-126">이 컨트롤러는 `Product` 인스턴스에 대 한 CRUD 작업을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-126">This controller supports CRUD operations on `Product` instances.</span></span> <span data-ttu-id="1e97b-127">`OrdersContext` 클래스를 사용 하 여 Entity Framework와 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-127">It uses the `OrdersContext` class to communicate with Entity Framework.</span></span>
- <span data-ttu-id="1e97b-128">Web.config 파일의 새 데이터베이스 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-128">A new database connection string in the Web.config file.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image4.png)

<span data-ttu-id="1e97b-129">OrdersContext.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-129">Open the OrdersContext.cs file.</span></span> <span data-ttu-id="1e97b-130">생성자는 데이터베이스 연결 문자열의 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-130">Notice that the constructor specifies the name of the database connection string.</span></span> <span data-ttu-id="1e97b-131">이 이름은 Web.config에 추가 된 연결 문자열을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-131">This name refers to the connection string that was added to Web.config.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample1.cs)]

<span data-ttu-id="1e97b-132">`OrdersContext` 클래스에 다음 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-132">Add the following properties to the `OrdersContext` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample2.cs)]

<span data-ttu-id="1e97b-133">**Dbset** 은 쿼리할 수 있는 엔터티 집합을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-133">A **DbSet** represents a set of entities that can be queried.</span></span> <span data-ttu-id="1e97b-134">다음은 `OrdersContext` 클래스에 대 한 전체 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-134">Here is the complete listing for the `OrdersContext` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample3.cs)]

<span data-ttu-id="1e97b-135">`AdminController` 클래스는 기본 CRUD 기능을 구현 하는 5 개의 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-135">The `AdminController` class defines five methods that implement basic CRUD functionality.</span></span> <span data-ttu-id="1e97b-136">각 메서드는 클라이언트에서 호출할 수 있는 URI에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-136">Each method corresponds to a URI that the client can invoke:</span></span>

| <span data-ttu-id="1e97b-137">Controller 메서드</span><span class="sxs-lookup"><span data-stu-id="1e97b-137">Controller Method</span></span> | <span data-ttu-id="1e97b-138">Description</span><span class="sxs-lookup"><span data-stu-id="1e97b-138">Description</span></span> | <span data-ttu-id="1e97b-139">URI</span><span class="sxs-lookup"><span data-stu-id="1e97b-139">URI</span></span> | <span data-ttu-id="1e97b-140">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="1e97b-140">HTTP Method</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1e97b-141">GetProducts</span><span class="sxs-lookup"><span data-stu-id="1e97b-141">GetProducts</span></span> | <span data-ttu-id="1e97b-142">모든 제품을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-142">Gets all products.</span></span> | <span data-ttu-id="1e97b-143">a p i/제품</span><span class="sxs-lookup"><span data-stu-id="1e97b-143">api/products</span></span> | <span data-ttu-id="1e97b-144">GET</span><span class="sxs-lookup"><span data-stu-id="1e97b-144">GET</span></span> |
| <span data-ttu-id="1e97b-145">GetProduct</span><span class="sxs-lookup"><span data-stu-id="1e97b-145">GetProduct</span></span> | <span data-ttu-id="1e97b-146">ID로 제품을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-146">Finds a product by ID.</span></span> | <span data-ttu-id="1e97b-147">a p i/제품/*i d*</span><span class="sxs-lookup"><span data-stu-id="1e97b-147">api/products/*id*</span></span> | <span data-ttu-id="1e97b-148">GET</span><span class="sxs-lookup"><span data-stu-id="1e97b-148">GET</span></span> |
| <span data-ttu-id="1e97b-149">PutProduct</span><span class="sxs-lookup"><span data-stu-id="1e97b-149">PutProduct</span></span> | <span data-ttu-id="1e97b-150">제품을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-150">Updates a product.</span></span> | <span data-ttu-id="1e97b-151">a p i/제품/*i d*</span><span class="sxs-lookup"><span data-stu-id="1e97b-151">api/products/*id*</span></span> | <span data-ttu-id="1e97b-152">PUT</span><span class="sxs-lookup"><span data-stu-id="1e97b-152">PUT</span></span> |
| <span data-ttu-id="1e97b-153">PostProduct</span><span class="sxs-lookup"><span data-stu-id="1e97b-153">PostProduct</span></span> | <span data-ttu-id="1e97b-154">새 제품을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-154">Creates a new product.</span></span> | <span data-ttu-id="1e97b-155">a p i/제품</span><span class="sxs-lookup"><span data-stu-id="1e97b-155">api/products</span></span> | <span data-ttu-id="1e97b-156">POST</span><span class="sxs-lookup"><span data-stu-id="1e97b-156">POST</span></span> |
| <span data-ttu-id="1e97b-157">DeleteProduct</span><span class="sxs-lookup"><span data-stu-id="1e97b-157">DeleteProduct</span></span> | <span data-ttu-id="1e97b-158">제품을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-158">Deletes a product.</span></span> | <span data-ttu-id="1e97b-159">a p i/제품/*i d*</span><span class="sxs-lookup"><span data-stu-id="1e97b-159">api/products/*id*</span></span> | <span data-ttu-id="1e97b-160">Delete</span><span class="sxs-lookup"><span data-stu-id="1e97b-160">DELETE</span></span> |

<span data-ttu-id="1e97b-161">각 메서드는 `OrdersContext`를 호출 하 여 데이터베이스를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-161">Each method calls into `OrdersContext` to query the database.</span></span> <span data-ttu-id="1e97b-162">컬렉션 (PUT, POST 및 DELETE) 호출을 수정 하는 메서드는 데이터베이스에 대 한 변경 내용을 유지 하는 `db.SaveChanges` 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-162">The methods that modify the collection (PUT, POST, and DELETE) call `db.SaveChanges` to persist the changes to the database.</span></span> <span data-ttu-id="1e97b-163">컨트롤러는 HTTP 요청당 생성 된 다음 삭제 되므로 메서드가 반환 되기 전에 변경 내용을 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-163">Controllers are created per HTTP request and then disposed, so it is necessary to persist changes before a method returns.</span></span>

## <a name="add-a-database-initializer"></a><span data-ttu-id="1e97b-164">데이터베이스 이니셜라이저 추가</span><span class="sxs-lookup"><span data-stu-id="1e97b-164">Add a Database Initializer</span></span>

<span data-ttu-id="1e97b-165">Entity Framework에는 시작 시 데이터베이스를 채우고 모델이 변경 될 때마다 자동으로 데이터베이스를 다시 만들 수 있는 유용한 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-165">Entity Framework has a nice feature that lets you populate the database on startup, and automatically recreate the database whenever the models change.</span></span> <span data-ttu-id="1e97b-166">이 기능은 모델을 변경 하는 경우에도 항상 일부 테스트 데이터가 있으므로 개발 하는 동안 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-166">This feature is useful during development, because you always have some test data, even if you change the models.</span></span>

<span data-ttu-id="1e97b-167">솔루션 탐색기에서 모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 `OrdersContextInitializer`라는 새 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-167">In Solution Explorer, right-click the Models folder and create a new class named `OrdersContextInitializer`.</span></span> <span data-ttu-id="1e97b-168">다음 구현에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-168">Paste in the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample4.cs)]

<span data-ttu-id="1e97b-169">**Dropcreatedatabaseifmodelchanges** 클래스에서 상속 하 여 모델 클래스를 수정할 때마다 데이터베이스를 삭제 Entity Framework 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-169">By inheriting from the **DropCreateDatabaseIfModelChanges** class, we are telling Entity Framework to drop the database whenever we modify the model classes.</span></span> <span data-ttu-id="1e97b-170">Entity Framework 데이터베이스를 만들거나 다시 만들 때 **시드** 메서드를 호출 하 여 테이블을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-170">When Entity Framework creates (or recreates) the database, it calls the **Seed** method to populate the tables.</span></span> <span data-ttu-id="1e97b-171">**Seed** 메서드를 사용 하 여 몇 가지 예제 제품과 예제 순서를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-171">We use the **Seed** method to add some example products plus an example order.</span></span>

<span data-ttu-id="1e97b-172">이 기능은 테스트에 유용 하지만, 누군가가 모델 클래스를 변경 하는 경우 데이터가 손실 될 수 있으므로 프로덕션 환경에서는 **Dropcreatedatabaseifmodelchanges** 클래스를 사용 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="1e97b-172">This feature is great for testing, but don't use the **DropCreateDatabaseIfModelChanges** class in production,, because you could lose your data if someone changes a model class.</span></span>

<span data-ttu-id="1e97b-173">그런 다음 Global.asax를 열고 **응용 프로그램\_Start** 메서드에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-173">Next, open Global.asax and add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample5.cs)]

## <a name="send-a-request-to-the-controller"></a><span data-ttu-id="1e97b-174">컨트롤러에 요청 보내기</span><span class="sxs-lookup"><span data-stu-id="1e97b-174">Send a Request to the Controller</span></span>

<span data-ttu-id="1e97b-175">이 시점에서 클라이언트 코드를 작성 하지 않았지만 웹 브라우저나 [Fiddler](http://www.fiddler2.com/fiddler2/)와 같은 HTTP 디버깅 도구를 사용 하 여 웹 API를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-175">At this point, we haven't written any client code, but you can invoke the web API using a web browser or an HTTP debugging tool such as [Fiddler](http://www.fiddler2.com/fiddler2/).</span></span> <span data-ttu-id="1e97b-176">Visual Studio에서 F5 키를 눌러 디버깅을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-176">In Visual Studio, press F5 to start debugging.</span></span> <span data-ttu-id="1e97b-177">웹 브라우저가 `http://localhost:*portnum*/`으로 열립니다. 여기서 *portnum* 은 일부 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-177">Your web browser will open to `http://localhost:*portnum*/`, where *portnum* is some port number.</span></span>

<span data-ttu-id="1e97b-178">"`http://localhost:*portnum*/api/admin`에 HTTP 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-178">Send an HTTP request to "`http://localhost:*portnum*/api/admin`.</span></span> <span data-ttu-id="1e97b-179">Entity Framework는 데이터베이스를 만들고 초기값을 설정할 수 있기 때문에 첫 번째 요청은 완료 하는 데 속도가 느릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-179">The first request may be slow to complete, because Entity Framework needs to create and seed the database.</span></span> <span data-ttu-id="1e97b-180">응답은 다음과 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e97b-180">The response should something similar to the following:</span></span>

[!code-console[Main](using-web-api-with-entity-framework-part-3/samples/sample6.cmd)]

> [!div class="step-by-step"]
> <span data-ttu-id="1e97b-181">[이전](using-web-api-with-entity-framework-part-2.md)
> [다음](using-web-api-with-entity-framework-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="1e97b-181">[Previous](using-web-api-with-entity-framework-part-2.md)
[Next](using-web-api-with-entity-framework-part-4.md)</span></span>
