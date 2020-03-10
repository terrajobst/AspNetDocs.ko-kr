---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-3
title: Code First 마이그레이션를 사용 하 여 데이터베이스 초기값 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 76e2013a-65b7-488c-834d-9448ecea378e
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-3
msc.type: authoredcontent
ms.openlocfilehash: 257bd06848adb949330856cc71eeb3d685e9d036
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449117"
---
# <a name="use-code-first-migrations-to-seed-the-database"></a><span data-ttu-id="7eb16-102">Code First 마이그레이션를 사용 하 여 데이터베이스 시드</span><span class="sxs-lookup"><span data-stu-id="7eb16-102">Use Code First Migrations to Seed the Database</span></span>

<span data-ttu-id="7eb16-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="7eb16-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="7eb16-104">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="7eb16-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="7eb16-105">이 섹션에서는 EF에서 [Code First 마이그레이션](https://msdn.microsoft.com/data/jj591621) 를 사용 하 여 테스트 데이터로 데이터베이스를 초기값으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-105">In this section, you will use [Code First Migrations](https://msdn.microsoft.com/data/jj591621) in EF to seed the database with test data.</span></span>

<span data-ttu-id="7eb16-106">**도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-106">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="7eb16-107">패키지 관리자 콘솔 창에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-107">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](part-3/samples/sample1.cmd)]

<span data-ttu-id="7eb16-108">이 명령은 마이그레이션 폴더에 migration 이라는 폴더와 Configuration.cs 이라는 코드 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-108">This command adds a folder named Migrations to your project, plus a code file named Configuration.cs in the Migrations folder.</span></span>

![](part-3/_static/image1.png)

<span data-ttu-id="7eb16-109">Configuration.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-109">Open the Configuration.cs file.</span></span> <span data-ttu-id="7eb16-110">다음 **using** 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-110">Add the following **using** statement.</span></span>

[!code-csharp[Main](part-3/samples/sample2.cs)]

<span data-ttu-id="7eb16-111">그런 다음, 다음 코드를 **구성 초기값** 메서드에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-111">Then add the following code to the **Configuration.Seed** method:</span></span>

[!code-csharp[Main](part-3/samples/sample3.cs)]

<span data-ttu-id="7eb16-112">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-112">In the Package Manager Console window, type the following commands:</span></span>

[!code-console[Main](part-3/samples/sample4.cmd)]

<span data-ttu-id="7eb16-113">첫 번째 명령은 데이터베이스를 만드는 코드를 생성 하 고, 두 번째 명령은 해당 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-113">The first command generates code that creates the database, and the second command executes that code.</span></span> <span data-ttu-id="7eb16-114">데이터베이스는 [LocalDB](https://msdn.microsoft.com/library/hh510202.aspx)를 사용 하 여 로컬로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-114">The database is created locally, using [LocalDB](https://msdn.microsoft.com/library/hh510202.aspx).</span></span>

![](part-3/_static/image2.png)

## <a name="explore-the-api-optional"></a><span data-ttu-id="7eb16-115">API 탐색 (선택 사항)</span><span class="sxs-lookup"><span data-stu-id="7eb16-115">Explore the API (Optional)</span></span>

<span data-ttu-id="7eb16-116">F5 키를 눌러 디버그 모드에서 애플리케이션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-116">Press F5 to run the application in debug mode.</span></span> <span data-ttu-id="7eb16-117">Visual Studio가 IIS Express를 시작 하 고 웹 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-117">Visual Studio starts IIS Express and runs your web app.</span></span> <span data-ttu-id="7eb16-118">그러면 Visual Studio가 브라우저를 시작 하 고 앱의 홈 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-118">Visual Studio then launches a browser and opens the app's home page.</span></span>

<span data-ttu-id="7eb16-119">Visual Studio에서 웹 프로젝트를 실행 하는 경우 포트 번호를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-119">When Visual Studio runs a web project, it assigns a port number.</span></span> <span data-ttu-id="7eb16-120">아래 이미지에서 포트 번호는 50524입니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-120">In the image below, the port number is 50524.</span></span> <span data-ttu-id="7eb16-121">응용 프로그램을 실행 하면 다른 포트 번호가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-121">When you run the application, you'll see a different port number.</span></span>

![](part-3/_static/image3.png)

<span data-ttu-id="7eb16-122">홈 페이지는 ASP.NET MVC를 사용 하 여 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-122">The home page is implemented using ASP.NET MVC.</span></span> <span data-ttu-id="7eb16-123">페이지 위쪽에 "API" 라는 링크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-123">At the top of the page, there is a link that says "API".</span></span> <span data-ttu-id="7eb16-124">이 링크를 통해 web API에 대 한 자동 생성 된 도움말 페이지로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-124">This link brings you to an auto-generated help page for the web API.</span></span> <span data-ttu-id="7eb16-125">이 도움말 페이지가 생성 되는 방법 및 페이지에 사용자 고유의 설명서를 추가 하는 방법에 대 한 자세한 내용은 [ASP.NET Web API에 대 한 도움말 페이지 만들기](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md)를 참조 하세요. 도움말 페이지 링크를 클릭 하면 요청 및 응답 형식을 포함 하 여 API에 대 한 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-125">(To learn how this help page is generated, and how you can add your own documentation to the page, see [Creating Help Pages for ASP.NET Web API](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md).) You can click on the help page links to see details about the API, including the request and response format.</span></span>

![](part-3/_static/image4.png)

<span data-ttu-id="7eb16-126">API를 사용 하면 데이터베이스에서 CRUD 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-126">The API enables CRUD operations on the database.</span></span> <span data-ttu-id="7eb16-127">다음은 API를 요약 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-127">The following summarizes the API.</span></span>

| <span data-ttu-id="7eb16-128">Authors</span><span class="sxs-lookup"><span data-stu-id="7eb16-128">Authors</span></span> |  |
| --- | -- |
| <span data-ttu-id="7eb16-129">GET api/authors</span><span class="sxs-lookup"><span data-stu-id="7eb16-129">GET api/authors</span></span> | <span data-ttu-id="7eb16-130">모든 작성자를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-130">Get all authors.</span></span> |
| <span data-ttu-id="7eb16-131">GET api/authors/{id}</span><span class="sxs-lookup"><span data-stu-id="7eb16-131">GET api/authors/{id}</span></span> | <span data-ttu-id="7eb16-132">ID 별로 작성자를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-132">Get an author by ID.</span></span> |
| <span data-ttu-id="7eb16-133">POST /api/authors</span><span class="sxs-lookup"><span data-stu-id="7eb16-133">POST /api/authors</span></span> | <span data-ttu-id="7eb16-134">새 저자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-134">Create a new author.</span></span> |
| <span data-ttu-id="7eb16-135">PUT /api/authors/{id}</span><span class="sxs-lookup"><span data-stu-id="7eb16-135">PUT /api/authors/{id}</span></span> | <span data-ttu-id="7eb16-136">기존 작성자를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-136">Update an existing author.</span></span> |
| <span data-ttu-id="7eb16-137">DELETE /api/authors/{id}</span><span class="sxs-lookup"><span data-stu-id="7eb16-137">DELETE /api/authors/{id}</span></span> | <span data-ttu-id="7eb16-138">작성자를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-138">Delete an author.</span></span> |

| <span data-ttu-id="7eb16-139">서적</span><span class="sxs-lookup"><span data-stu-id="7eb16-139">Books</span></span> |  |
| --- | -- |
| <span data-ttu-id="7eb16-140">GET /api/books</span><span class="sxs-lookup"><span data-stu-id="7eb16-140">GET /api/books</span></span> | <span data-ttu-id="7eb16-141">모든 책을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-141">Get all books.</span></span> |
| <span data-ttu-id="7eb16-142">GET /api/books/{id}</span><span class="sxs-lookup"><span data-stu-id="7eb16-142">GET /api/books/{id}</span></span> | <span data-ttu-id="7eb16-143">ID 별로 책을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-143">Get a book by ID.</span></span> |
| <span data-ttu-id="7eb16-144">POST /api/books</span><span class="sxs-lookup"><span data-stu-id="7eb16-144">POST /api/books</span></span> | <span data-ttu-id="7eb16-145">새 책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-145">Create a new book.</span></span> |
| <span data-ttu-id="7eb16-146">PUT /api/books/{id}</span><span class="sxs-lookup"><span data-stu-id="7eb16-146">PUT /api/books/{id}</span></span> | <span data-ttu-id="7eb16-147">기존 책을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-147">Update an existing book.</span></span> |
| <span data-ttu-id="7eb16-148">DELETE /api/books/{id}</span><span class="sxs-lookup"><span data-stu-id="7eb16-148">DELETE /api/books/{id}</span></span> | <span data-ttu-id="7eb16-149">책을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-149">Delete a book.</span></span> |

## <a name="view-the-database-optional"></a><span data-ttu-id="7eb16-150">데이터베이스 보기 (옵션)</span><span class="sxs-lookup"><span data-stu-id="7eb16-150">View the Database (Optional)</span></span>

<span data-ttu-id="7eb16-151">데이터베이스 업데이트 명령을 실행 한 경우 EF는 데이터베이스를 만들고 `Seed` 메서드를 호출 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-151">When you ran the Update-Database command, EF created the database and called the `Seed` method.</span></span> <span data-ttu-id="7eb16-152">응용 프로그램을 로컬로 실행 하는 경우 EF는 [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-152">When you run the application locally, EF uses [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx).</span></span> <span data-ttu-id="7eb16-153">Visual Studio에서 데이터베이스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-153">You can view the database in Visual Studio.</span></span> <span data-ttu-id="7eb16-154">**보기** 메뉴에서 **SQL Server 개체 탐색기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-154">From the **View** menu, select **SQL Server Object Explorer**.</span></span>

![](part-3/_static/image5.png)

<span data-ttu-id="7eb16-155">**서버에 연결** 대화 상자의 **서버 이름** 입력란에 "(localdb) \v11.0"을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-155">In the **Connect to Server** dialog, in the **Server Name** edit box, type "(localdb)\v11.0".</span></span> <span data-ttu-id="7eb16-156">**인증** 옵션을 "Windows 인증"으로 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-156">Leave the **Authentication** option as "Windows Authentication".</span></span> <span data-ttu-id="7eb16-157">**연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-157">Click **Connect**.</span></span>

![](part-3/_static/image6.png)

<span data-ttu-id="7eb16-158">Visual Studio는 LocalDB에 연결 하 고 SQL Server 개체 탐색기 창에 기존 데이터베이스를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-158">Visual Studio connects to LocalDB and shows your existing databases in the SQL Server Object Explorer window.</span></span> <span data-ttu-id="7eb16-159">노드를 확장 하 여 EF에서 만든 테이블을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-159">You can expand the nodes to see the tables that EF created.</span></span>

![](part-3/_static/image7.png)

<span data-ttu-id="7eb16-160">데이터를 보려면 테이블을 마우스 오른쪽 단추로 클릭 하 고 **데이터 보기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-160">To view the data, right-click a table and select **View Data**.</span></span>

![](part-3/_static/image8.png)

<span data-ttu-id="7eb16-161">다음 스크린샷에서는 Books 테이블의 결과를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-161">The following screenshot shows the results for the Books table.</span></span> <span data-ttu-id="7eb16-162">EF는 데이터베이스를 초기값 데이터로 채우고 테이블에는 Authors 테이블에 대 한 외래 키가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7eb16-162">Notice that EF populated the database with the seed data, and the table contains the foreign key to the Authors table.</span></span>

![](part-3/_static/image9.png)

> [!div class="step-by-step"]
> <span data-ttu-id="7eb16-163">[이전](part-2.md)
> [다음](part-4.md)</span><span class="sxs-lookup"><span data-stu-id="7eb16-163">[Previous](part-2.md)
[Next](part-4.md)</span></span>
