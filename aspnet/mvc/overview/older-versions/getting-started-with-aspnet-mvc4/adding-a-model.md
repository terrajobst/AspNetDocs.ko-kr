---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
title: 모델 추가 | Microsoft Docs
author: Rick-Anderson
description: 참고:이 자습서의 업데이트 된 버전은 ASP.NET MVC 5 및 Visual Studio 2013를 사용 하는 여기에서 사용할 수 있습니다. 보다 안전 하 고, 보다 간단 하 고 데모를 수행 하는 것이 더 간단 합니다.
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 53db72da-e0b9-44d9-b60b-6e6988c00b28
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: a9851d93dde495814f67fa0c807d3534f5f0d8ef
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457806"
---
# <a name="adding-a-model"></a><span data-ttu-id="476ac-104">모델 추가</span><span class="sxs-lookup"><span data-stu-id="476ac-104">Adding a Model</span></span>

<span data-ttu-id="476ac-105">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="476ac-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="476ac-106">ASP.NET MVC 5와 Visual Studio 2013를 사용 하는이 자습서의 업데이트 된 버전 [을 사용할 수 있습니다.](../../getting-started/introduction/getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="476ac-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="476ac-107">더 안전 하 고 더 간단 하 고 더 많은 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="476ac-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="476ac-108">이 섹션에서는 데이터베이스에서 동영상을 관리 하기 위한 몇 가지 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="476ac-108">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="476ac-109">이러한 클래스는 ASP.NET MVC 응용 프로그램의 일부&quot; &quot;모델입니다.</span><span class="sxs-lookup"><span data-stu-id="476ac-109">These classes will be the &quot;model&quot; part of the ASP.NET MVC application.</span></span>

<span data-ttu-id="476ac-110">이러한 모델 클래스를 정의 하 고 사용 하려면 [Entity Framework](https://msdn.microsoft.com/library/bb399572(VS.110).aspx) 라는 .NET Framework 데이터 액세스 기술을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="476ac-110">You'll use a .NET Framework data-access technology known as the [Entity Framework](https://msdn.microsoft.com/library/bb399572(VS.110).aspx) to define and work with these model classes.</span></span> <span data-ttu-id="476ac-111">Entity Framework (EF 라고도 함)는 *Code First*라는 개발 패러다임을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="476ac-111">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="476ac-112">Code First를 사용 하면 간단한 클래스를 작성 하 여 모델 개체를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="476ac-112">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="476ac-113">이러한 항목은 &quot;일반-이전 CLR 개체에서 POCO 클래스 라고도 합니다.&quot;) 그런 다음 클래스에서 즉석에서 데이터베이스를 만들 수 있습니다. 이렇게 하면 매우 깔끔하고 빠른 개발 워크플로를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="476ac-113">(These are also known as POCO classes, from &quot;plain-old CLR objects.&quot;) You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="476ac-114">모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="476ac-114">Adding Model Classes</span></span>

<span data-ttu-id="476ac-115">**솔루션 탐색기**에서 *모델* 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 선택한 다음 **클래스**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="476ac-115">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="476ac-116">동영상&quot;&quot;*클래스* 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="476ac-116">Enter the *class* name &quot;Movie&quot;.</span></span>

<span data-ttu-id="476ac-117">`Movie` 클래스에 다음 5 가지 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="476ac-117">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="476ac-118">`Movie` 클래스를 사용 하 여 데이터베이스의 영화를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="476ac-118">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="476ac-119">`Movie` 개체의 각 인스턴스는 데이터베이스 테이블의 행에 해당 하며 `Movie` 클래스의 각 속성은 테이블의 열에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="476ac-119">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="476ac-120">동일한 파일에서 다음 `MovieDBContext` 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="476ac-120">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

<span data-ttu-id="476ac-121">`MovieDBContext` 클래스는 데이터베이스의 `Movie` 클래스 인스턴스 가져오기, 저장 및 업데이트를 처리 하는 Entity Framework movie 데이터베이스 컨텍스트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="476ac-121">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="476ac-122">`MovieDBContext` Entity Framework에서 제공 하는 `DbContext` 기본 클래스에서 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="476ac-122">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span>

<span data-ttu-id="476ac-123">`DbContext` 및 `DbSet`를 참조할 수 있도록 하려면 파일 맨 위에 다음 `using` 문을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="476ac-123">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="476ac-124">전체 *Movie.cs* 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="476ac-124">The complete *Movie.cs* file is shown below.</span></span> <span data-ttu-id="476ac-125">필요 하지 않은 여러 using 문이 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="476ac-125">(Several using statements that are not needed have been removed.)</span></span>

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="476ac-126">연결 문자열 만들기 및 SQL Server LocalDB 사용</span><span class="sxs-lookup"><span data-stu-id="476ac-126">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="476ac-127">만든 `MovieDBContext` 클래스는 데이터베이스에 연결 하 고 데이터베이스 레코드에 `Movie` 개체를 매핑하는 태스크를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="476ac-127">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="476ac-128">한 가지 질문은 연결할 데이터베이스를 지정 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="476ac-128">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="476ac-129">응용 프로그램의 *web.config* 파일에 연결 정보를 추가 하 여이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="476ac-129">You'll do that by adding connection information in the *Web.config* file of the application.</span></span>

<span data-ttu-id="476ac-130">응용 프로그램 루트 *web.config* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="476ac-130">Open the application root *Web.config* file.</span></span> <span data-ttu-id="476ac-131">*Views* 폴더에 있는 *web.config* 파일이 아닙니다. Red에 설명 된 *web.config* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="476ac-131">(Not the *Web.config* file in the *Views* folder.) Open the *Web.config* file outlined in red.</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="476ac-132">*Web.config 파일의* `<connectionStrings>` 요소에 다음 연결 문자열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="476ac-132">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

<span data-ttu-id="476ac-133">다음 예제에서는 새 연결 문자열이 추가 된 *web.config 파일의* 일부를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="476ac-133">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](adding-a-model/samples/sample6.xml?highlight=6-9)]

<span data-ttu-id="476ac-134">이러한 소량의 코드와 XML은 동영상 데이터를 표시 하 고 데이터베이스에 저장 하기 위해 작성 해야 하는 모든 것입니다.</span><span class="sxs-lookup"><span data-stu-id="476ac-134">This small amount of code and XML is everything you need to write in order to represent and store the movie data in a database.</span></span>

<span data-ttu-id="476ac-135">다음으로, 영화 데이터를 표시 하 고 사용자가 새 영화 목록을 만들 수 있도록 하는 새 `MoviesController` 클래스를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="476ac-135">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="476ac-136">[이전](adding-a-view.md)
> [다음](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="476ac-136">[Previous](adding-a-view.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
