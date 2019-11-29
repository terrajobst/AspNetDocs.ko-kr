---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
title: 데이터 액세스 계층 만들기 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈에서는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 0bbf7a6e-d7eb-4091-91e4-fff892777f32
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
msc.type: authoredcontent
ms.openlocfilehash: 0fcf050474a57be9ed53ec0783a6d6b7dde2bf4c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575746"
---
# <a name="create-the-data-access-layer"></a><span data-ttu-id="b1545-103">데이터 액세스 레이어 만들기</span><span class="sxs-lookup"><span data-stu-id="b1545-103">Create the Data Access Layer</span></span>

<span data-ttu-id="b1545-104">[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="b1545-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="b1545-105">[정문 장난감 샘플 프로젝트 (C#) 다운로드](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자 서적 다운로드 (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="b1545-105">[Download Wingtip Toys Sample Project (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="b1545-106">이 자습서 시리즈에서는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013 for Web을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="b1545-107">[소스 코드를 포함 C# ](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 하는 Visual Studio 2013 프로젝트는이 자습서 계열과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>

<span data-ttu-id="b1545-108">이 자습서에서는 ASP.NET Web Forms 및 Entity Framework Code First를 사용 하 여 데이터베이스에서 데이터를 만들고 액세스 하 고 검토 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-108">This tutorial describes how to create, access, and review data from a database using ASP.NET Web Forms and Entity Framework Code First.</span></span> <span data-ttu-id="b1545-109">이 자습서는 이전 자습서 "프로젝트 만들기"를 기반으로 하며, 정문 장난감 스토어 자습서 시리즈의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-109">This tutorial builds on the previous tutorial "Create the Project" and is part of the Wingtip Toy Store tutorial series.</span></span> <span data-ttu-id="b1545-110">이 자습서를 완료 하면 프로젝트의 *모델* 폴더에 있는 데이터 액세스 클래스의 그룹을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-110">When you've completed this tutorial, you will have built a group of data-access classes that are in the *Models* folder of the project.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="b1545-111">학습 내용:</span><span class="sxs-lookup"><span data-stu-id="b1545-111">What you'll learn:</span></span>

- <span data-ttu-id="b1545-112">데이터 모델을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="b1545-112">How to create the data models.</span></span>
- <span data-ttu-id="b1545-113">데이터베이스를 초기화 하 고 초기값을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="b1545-113">How to initialize and seed the database.</span></span>
- <span data-ttu-id="b1545-114">데이터베이스를 지원 하도록 응용 프로그램을 업데이트 하 고 구성 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-114">How to update and configure the application to support the database.</span></span>

### <a name="these-are-the-features-introduced-in-the-tutorial"></a><span data-ttu-id="b1545-115">자습서에서 소개 하는 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-115">These are the features introduced in the tutorial:</span></span>

- <span data-ttu-id="b1545-116">Entity Framework Code First</span><span class="sxs-lookup"><span data-stu-id="b1545-116">Entity Framework Code First</span></span>
- <span data-ttu-id="b1545-117">LocalDB</span><span class="sxs-lookup"><span data-stu-id="b1545-117">LocalDB</span></span>
- <span data-ttu-id="b1545-118">데이터 주석</span><span class="sxs-lookup"><span data-stu-id="b1545-118">Data Annotations</span></span>

## <a name="creating-the-data-models"></a><span data-ttu-id="b1545-119">데이터 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="b1545-119">Creating the Data Models</span></span>

<span data-ttu-id="b1545-120">[Entity Framework](https://msdn.microsoft.com/data/aa937723) 은 ORM (개체 관계형 매핑) 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-120">[Entity Framework](https://msdn.microsoft.com/data/aa937723) is an object-relational mapping (ORM) framework.</span></span> <span data-ttu-id="b1545-121">이를 통해 관계형 데이터를 개체로 사용 하 여 일반적으로 작성 해야 하는 대부분의 데이터 액세스 코드를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-121">It lets you work with relational data as objects, eliminating most of the data-access code that you'd usually need to write.</span></span> <span data-ttu-id="b1545-122">Entity Framework를 사용 하 여 [LINQ](https://msdn.microsoft.com/library/bb397926.aspx)를 사용 하 여 쿼리를 실행 한 다음 데이터를 강력한 형식의 개체로 검색 및 조작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-122">Using Entity Framework, you can issue queries using [LINQ](https://msdn.microsoft.com/library/bb397926.aspx), then retrieve and manipulate data as strongly typed objects.</span></span> <span data-ttu-id="b1545-123">LINQ는 데이터 쿼리 및 업데이트를 위한 패턴을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-123">LINQ provides patterns for querying and updating data.</span></span> <span data-ttu-id="b1545-124">Entity Framework를 사용 하면 데이터 액세스 기본 사항에 중점을 두는 대신 응용 프로그램의 나머지 부분을 만드는 데 집중할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-124">Using Entity Framework allows you to focus on creating the rest of your application, rather than focusing on the data access fundamentals.</span></span> <span data-ttu-id="b1545-125">이 자습서 시리즈의 뒷부분에서 데이터를 사용 하 여 탐색 및 제품 쿼리를 채우는 방법을 보여 드리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-125">Later in this tutorial series, we'll show you how to use the data to populate navigation and product queries.</span></span>

<span data-ttu-id="b1545-126">Entity Framework는 *Code First*라는 개발 패러다임을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-126">Entity Framework supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="b1545-127">Code First를 사용 하면 클래스를 사용 하 여 데이터 모델을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-127">Code First lets you define your data models using classes.</span></span> <span data-ttu-id="b1545-128">클래스는 다른 형식, 메서드 및 이벤트의 변수를 함께 그룹화 하 여 사용자 고유의 사용자 지정 형식을 만들 수 있도록 하는 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-128">A class is a construct that enables you to create your own custom types by grouping together variables of other types, methods and events.</span></span> <span data-ttu-id="b1545-129">클래스를 기존 데이터베이스에 매핑하거나이를 사용 하 여 데이터베이스를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-129">You can map classes to an existing database or use them to generate a database.</span></span> <span data-ttu-id="b1545-130">이 자습서에서는 데이터 모델 클래스를 작성 하 여 데이터 모델을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-130">In this tutorial, you'll create the data models by writing data model classes.</span></span> <span data-ttu-id="b1545-131">그런 다음 이러한 새 클래스에서 즉시 데이터베이스를 만들 Entity Framework 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-131">Then, you'll let Entity Framework create the database on the fly from these new classes.</span></span>

<span data-ttu-id="b1545-132">먼저 Web Forms 응용 프로그램에 대 한 데이터 모델을 정의 하는 엔터티 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-132">You will begin by creating the entity classes that define the data models for the Web Forms application.</span></span> <span data-ttu-id="b1545-133">그런 다음 엔터티 클래스를 관리 하 고 데이터베이스에 대 한 데이터 액세스를 제공 하는 컨텍스트 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-133">Then you will create a context class that manages the entity classes and provides data access to the database.</span></span> <span data-ttu-id="b1545-134">또한 데이터베이스를 채우는 데 사용할 이니셜라이저 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-134">You will also create an initializer class that you will use to populate the database.</span></span>

### <a name="entity-framework-and-references"></a><span data-ttu-id="b1545-135">Entity Framework 및 참조</span><span class="sxs-lookup"><span data-stu-id="b1545-135">Entity Framework and References</span></span>

<span data-ttu-id="b1545-136">기본적으로 Entity Framework는 **Web Forms** 템플릿을 사용 하 여 새 **ASP.NET 웹 응용 프로그램** 을 만들 때 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-136">By default, Entity Framework is included when you create a new **ASP.NET Web Application** using the **Web Forms** template.</span></span> <span data-ttu-id="b1545-137">Entity Framework는 NuGet 패키지로 설치, 제거 및 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-137">Entity Framework can be installed, uninstalled, and updated as a NuGet package.</span></span>

<span data-ttu-id="b1545-138">이 NuGet 패키지는 프로젝트에 다음 **런타임** 어셈블리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-138">This NuGet package includes the following **runtime** assemblies within your project:</span></span>

- <span data-ttu-id="b1545-139">EntityFramework .dll – Entity Framework에서 사용 하는 모든 공용 런타임 코드</span><span class="sxs-lookup"><span data-stu-id="b1545-139">EntityFramework.dll – All the common runtime code used by Entity Framework</span></span>
- <span data-ttu-id="b1545-140">EntityFramework. SqlServer – Entity Framework에 대 한 Microsoft SQL Server 공급자</span><span class="sxs-lookup"><span data-stu-id="b1545-140">EntityFramework.SqlServer.dll – The Microsoft SQL Server provider for Entity Framework</span></span>

### <a name="entity-classes"></a><span data-ttu-id="b1545-141">엔터티 클래스</span><span class="sxs-lookup"><span data-stu-id="b1545-141">Entity Classes</span></span>

<span data-ttu-id="b1545-142">데이터의 스키마를 정의 하기 위해 만드는 클래스를 엔터티 클래스 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-142">The classes you create to define the schema of the data are called entity classes.</span></span> <span data-ttu-id="b1545-143">데이터베이스 디자인을 처음 접하는 경우 엔터티 클래스를 데이터베이스의 테이블 정의로 간주 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-143">If you're new to database design, think of the entity classes as table definitions of a database.</span></span> <span data-ttu-id="b1545-144">클래스의 각 속성은 데이터베이스 테이블의 열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-144">Each property in the class specifies a column in the table of the database.</span></span> <span data-ttu-id="b1545-145">이러한 클래스는 개체 지향 코드와 데이터베이스의 관계형 테이블 구조 간에 간단한 개체 관계형 인터페이스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-145">These classes provide a lightweight, object-relational interface between object-oriented code and the relational table structure of the database.</span></span>

<span data-ttu-id="b1545-146">이 자습서에서는 제품 및 범주에 대 한 스키마를 나타내는 간단한 엔터티 클래스를 추가 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-146">In this tutorial, you'll start out by adding simple entity classes representing the schemas for products and categories.</span></span> <span data-ttu-id="b1545-147">Products 클래스에는 각 제품에 대 한 정의가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-147">The products class will contain definitions for each product.</span></span> <span data-ttu-id="b1545-148">Product 클래스의 각 멤버 이름은 `ProductID`, `ProductName`, `Description`, `ImagePath`, `UnitPrice`, `CategoryID`, `Category`입니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-148">The name of each of the members of the product class will be `ProductID`, `ProductName`, `Description`, `ImagePath`, `UnitPrice`, `CategoryID`, and `Category`.</span></span> <span data-ttu-id="b1545-149">Category 클래스에는 제품이 속할 수 있는 각 범주에 대 한 정의 (예: 자동차, 보트 또는 평면)가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-149">The category class will contain definitions for each category that a product can belong to, such as Car, Boat, or Plane.</span></span> <span data-ttu-id="b1545-150">Category 클래스의 각 멤버 이름은 `CategoryID`, `CategoryName`, `Description`및 `Products`됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-150">The name of each of the members of the category class will be `CategoryID`, `CategoryName`, `Description`, and `Products`.</span></span> <span data-ttu-id="b1545-151">각 제품은 범주 중 하나에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-151">Each product will belong to one of the categories.</span></span> <span data-ttu-id="b1545-152">이러한 엔터티 클래스는 프로젝트의 기존 *모델* 폴더에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-152">These entity classes will be added to the project's existing *Models* folder.</span></span>

1. <span data-ttu-id="b1545-153">**솔루션 탐색기**에서 *모델* 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **추가** -&gt; **새 항목**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-153">In **Solution Explorer**, right-click the *Models* folder and then select **Add** -&gt; **New Item**.</span></span> 

    ![데이터 액세스 계층-새 항목 메뉴 만들기](create_the_data_access_layer/_static/image1.png)

   <span data-ttu-id="b1545-155">**새 항목 추가** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-155">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="b1545-156">왼쪽의 **설치 됨** 창에서 **Visual C#**  아래에 있는 **코드**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-156">Under **Visual C#** from the **Installed** pane on the left, select **Code**.</span></span> 

    ![데이터 액세스 계층-새 항목 메뉴 만들기](create_the_data_access_layer/_static/image2.png)
3. <span data-ttu-id="b1545-158">가운데 창에서 **클래스** 를 선택 하 고이 새 클래스의 이름을 *Product.cs*로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-158">Select **Class** from the middle pane and name this new class *Product.cs*.</span></span>
4. <span data-ttu-id="b1545-159">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-159">Click **Add**.</span></span>  
   <span data-ttu-id="b1545-160">새 클래스 파일이 편집기에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-160">The new class file is displayed in the editor.</span></span>
5. <span data-ttu-id="b1545-161">기본 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-161">Replace the default code with the following code:</span></span>   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample1.cs)]
6. <span data-ttu-id="b1545-162">1 ~ 4 단계를 반복 하 여 다른 클래스를 만들고, 새 클래스의 이름을 *Category.cs* 로 변경 하 고, 기본 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-162">Create another class by repeating steps 1 through 4, however, name the new class *Category.cs* and replace the default code with the following code:</span></span>  

    [!code-csharp[Main](create_the_data_access_layer/samples/sample2.cs)]

<span data-ttu-id="b1545-163">앞에서 설명한 것 처럼 `Category` 클래스는 응용 프로그램이 판매 하도록 디자인 된 제품의 유형 (예: <a id="a"></a>&quot;자동차&quot;, &quot;배&quot;, &quot;Rockets&quot;등)을 나타내며, `Product` 클래스는 데이터베이스의 개별 제품 (장난감)을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-163">As previously mentioned, the `Category` class represents the type of product that the application is designed to sell (such as <a id="a"></a>&quot;Cars&quot;, &quot;Boats&quot;, &quot;Rockets&quot;, and so on), and the `Product` class represents the individual products (toys) in the database.</span></span> <span data-ttu-id="b1545-164">`Product` 개체의 각 인스턴스는 관계형 데이터베이스 테이블의 행에 해당 하며 Product 클래스의 각 속성은 관계형 데이터베이스 테이블의 열에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-164">Each instance of a `Product` object will correspond to a row within a relational database table, and each property of the Product class will map to a column in the relational database table.</span></span> <span data-ttu-id="b1545-165">이 자습서의 뒷부분에서는 데이터베이스에 포함 된 제품 데이터를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-165">Later in this tutorial, you'll review the product data contained in the database.</span></span>

### <a name="data-annotations"></a><span data-ttu-id="b1545-166">데이터 주석</span><span class="sxs-lookup"><span data-stu-id="b1545-166">Data Annotations</span></span>

<span data-ttu-id="b1545-167">클래스의 특정 멤버에 `[ScaffoldColumn(false)]`와 같은 멤버에 대 한 세부 정보를 지정 하는 특성이 있다는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-167">You may have noticed that certain members of the classes have attributes specifying details about the member, such as `[ScaffoldColumn(false)]`.</span></span> <span data-ttu-id="b1545-168">이는 *데이터 주석*입니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-168">These are *data annotations*.</span></span> <span data-ttu-id="b1545-169">데이터 주석 특성은 해당 멤버에 대 한 사용자 입력의 유효성을 검사 하 고, 형식을 지정 하 고, 데이터베이스를 만들 때 모델링 하는 방법을 지정 하는 방법을 설명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-169">The data annotation attributes can describe how to validate user input for that member, to specify formatting for it, and to specify how it is modeled when the database is created.</span></span>

### <a name="context-class"></a><span data-ttu-id="b1545-170">Context 클래스</span><span class="sxs-lookup"><span data-stu-id="b1545-170">Context Class</span></span>

<span data-ttu-id="b1545-171">데이터 액세스를 위한 클래스 사용을 시작 하려면 컨텍스트 클래스를 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-171">To start using the classes for data access, you must define a context class.</span></span> <span data-ttu-id="b1545-172">앞에서 설명한 것 처럼 컨텍스트 클래스는 엔터티 클래스 (예: `Product` 클래스 및 `Category` 클래스)를 관리 하 고 데이터베이스에 대 한 데이터 액세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-172">As mentioned previously, the context class manages the entity classes (such as the `Product` class and the `Category` class) and provides data access to the database.</span></span>

<span data-ttu-id="b1545-173">이 프로시저는 새 C# 컨텍스트 클래스를 *모델* 폴더에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-173">This procedure adds a new C# context class to the *Models* folder.</span></span>

1. <span data-ttu-id="b1545-174">*모델* 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **추가** -&gt; **새 항목**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-174">Right-click the *Models* folder and then select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="b1545-175">**새 항목 추가** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-175">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="b1545-176">가운데 창에서 **클래스** 를 선택 하 고 이름을 *ProductContext.cs* 로 선택한 후 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-176">Select **Class** from the middle pane, name it *ProductContext.cs* and click **Add**.</span></span>
3. <span data-ttu-id="b1545-177">클래스에 포함 된 기본 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-177">Replace the default code contained in the class with the following code:</span></span>   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample3.cs)]

<span data-ttu-id="b1545-178">이 코드는 강력한 형식의 개체를 사용 하 여 데이터를 쿼리, 삽입, 업데이트 및 삭제 하는 기능이 포함 된 Entity Framework의 모든 핵심 기능에 액세스할 수 있도록 `System.Data.Entity` 네임 스페이스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-178">This code adds the `System.Data.Entity` namespace so that you have access to all the core functionality of Entity Framework, which includes the capability to query, insert, update, and delete data by working with strongly typed objects.</span></span>

<span data-ttu-id="b1545-179">`ProductContext` 클래스는 데이터베이스에서 `Product` 클래스 인스턴스를 가져오고, 저장 하 고, 업데이트 하는 것을 처리 하는 Entity Framework product 데이터베이스 컨텍스트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-179">The `ProductContext` class represents Entity Framework product database context, which handles fetching, storing, and updating `Product` class instances in the database.</span></span> <span data-ttu-id="b1545-180">`ProductContext` 클래스는 Entity Framework에서 제공 하는 `DbContext` 기본 클래스에서 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-180">The `ProductContext` class derives from the `DbContext` base class provided by Entity Framework.</span></span>

### <a name="initializer-class"></a><span data-ttu-id="b1545-181">이니셜라이저 클래스</span><span class="sxs-lookup"><span data-stu-id="b1545-181">Initializer Class</span></span>

<span data-ttu-id="b1545-182">컨텍스트를 처음 사용할 때 데이터베이스를 초기화 하려면 일부 사용자 지정 논리를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-182">You will need to run some custom logic to initialize the database the first time the context is used.</span></span> <span data-ttu-id="b1545-183">이렇게 하면 제품 및 범주를 즉시 표시할 수 있도록 시드 데이터를 데이터베이스에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-183">This will allow seed data to be added to the database so that you can immediately display products and categories.</span></span>

<span data-ttu-id="b1545-184">이 절차에서는 새 C# 이니셜라이저 클래스를 *모델* 폴더에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-184">This procedure adds a new C# initializer class to the *Models* folder.</span></span>

1. <span data-ttu-id="b1545-185">*모델* 폴더에서 다른 `Class`를 만들고 이름을 *ProductDatabaseInitializer.cs*로 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-185">Create another `Class` in the *Models* folder and name it *ProductDatabaseInitializer.cs*.</span></span>
2. <span data-ttu-id="b1545-186">클래스에 포함 된 기본 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-186">Replace the default code contained in the class with the following code:</span></span>   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample4.cs)]

<span data-ttu-id="b1545-187">위의 코드에서 볼 수 있듯이 데이터베이스를 만들고 초기화할 때 `Seed` 속성이 재정의 되 고가 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-187">As you can see from the above code, when the database is created and initialized, the `Seed` property is overridden and set.</span></span> <span data-ttu-id="b1545-188">`Seed` 속성이 설정 되 면 범주 및 제품의 값을 사용 하 여 데이터베이스를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-188">When the `Seed` property is set, the values from the categories and products are used to populate the database.</span></span> <span data-ttu-id="b1545-189">데이터베이스를 만든 후 위의 코드를 수정 하 여 초기값 데이터를 업데이트 하려고 하면 웹 응용 프로그램을 실행할 때 업데이트가 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-189">If you attempt to update the seed data by modifying the above code after the database has been created, you won't see any updates when you run the Web application.</span></span> <span data-ttu-id="b1545-190">그 이유는 위의 코드에서 `DropCreateDatabaseIfModelChanges` 클래스의 구현을 사용 하 여 시드 데이터를 다시 설정 하기 전에 모델 (스키마)이 변경 되었는지 여부를 인식 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-190">The reason is the above code uses an implementation of the `DropCreateDatabaseIfModelChanges` class to recognize if the model (schema) has changed before resetting the seed data.</span></span> <span data-ttu-id="b1545-191">`Category` 및 `Product` 엔터티 클래스에 대 한 변경 내용이 없는 경우 데이터베이스는 초기값 데이터로 다시 초기화 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-191">If no changes are made to the `Category` and `Product` entity classes, the database will not be reinitialized with the seed data.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="b1545-192">응용 프로그램을 실행할 때마다 데이터베이스를 다시 만들려면 `DropCreateDatabaseIfModelChanges` 클래스 대신 `DropCreateDatabaseAlways` 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-192">If you wanted the database to be recreated every time you ran the application, you could use the `DropCreateDatabaseAlways` class instead of the `DropCreateDatabaseIfModelChanges` class.</span></span> <span data-ttu-id="b1545-193">그러나이 자습서 시리즈의 경우 `DropCreateDatabaseIfModelChanges` 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-193">However for this tutorial series, use the `DropCreateDatabaseIfModelChanges` class.</span></span>

<span data-ttu-id="b1545-194">이 자습서의이 시점에서 4 개의 새 클래스와 하나의 기본 클래스를 포함 하는 *모델* 폴더가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-194">At this point in this tutorial, you will have a *Models* folder with four new classes and one default class:</span></span>

![데이터 액세스 계층-모델 폴더 만들기](create_the_data_access_layer/_static/image3.png)

### <a name="configuring-the-application-to-use-the-data-model"></a><span data-ttu-id="b1545-196">데이터 모델을 사용 하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="b1545-196">Configuring the Application to Use the Data Model</span></span>

<span data-ttu-id="b1545-197">이제 데이터를 나타내는 클래스를 만들었으므로 클래스를 사용 하도록 응용 프로그램을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-197">Now that you've created the classes that represent the data, you must configure the application to use the classes.</span></span> <span data-ttu-id="b1545-198">*Global.asax* 파일에서 모델을 초기화 하는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-198">In the *Global.asax* file, you add code that initializes the model.</span></span> <span data-ttu-id="b1545-199">*Web.config* 파일에서 새 데이터 클래스가 나타내는 데이터를 저장 하는 데 사용할 데이터베이스를 응용 프로그램에 알리는 정보를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-199">In the *Web.config* file you add information that tells the application what database you'll use to store the data that's represented by the new data classes.</span></span> <span data-ttu-id="b1545-200">*Global.asax* 파일을 사용 하 여 응용 프로그램 이벤트 또는 메서드를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-200">The *Global.asax* file can be used to handle application events or methods.</span></span> <span data-ttu-id="b1545-201">Web.config *파일을* 사용 하 여 ASP.NET 웹 응용 프로그램의 구성을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-201">The *Web.config* file allows you to control the configuration of your ASP.NET web application.</span></span>

#### <a name="updating-the-globalasax-file"></a><span data-ttu-id="b1545-202">Global.asax 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="b1545-202">Updating the Global.asax file</span></span>

<span data-ttu-id="b1545-203">응용 프로그램이 시작 될 때 데이터 모델을 초기화 하려면 *Global.asax.cs* 파일에서 `Application_Start` 처리기를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-203">To initialize the data models when the application starts, you will update the `Application_Start` handler in the *Global.asax.cs* file.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="b1545-204">솔루션 탐색기에서 *global.asax* 파일 또는 *Global.asax.cs* 파일 중 하나를 선택 하 여 *Global.asax.cs* 파일을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-204">In Solution Explorer, you can select either the *Global.asax* file or the *Global.asax.cs* file to edit the *Global.asax.cs* file.</span></span>

1. <span data-ttu-id="b1545-205">노란색으로 강조 표시 된 다음 코드를 *Global.asax.cs* 파일의 `Application_Start` 메서드에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-205">Add the following code highlighted in yellow to the `Application_Start` method in the *Global.asax.cs* file.</span></span>   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample5.cs?highlight=9-10,22-23)]

> [!NOTE] 
> 
> <span data-ttu-id="b1545-206">브라우저에서이 자습서 시리즈를 볼 때 노란색으로 강조 표시 된 코드를 보려면 브라우저에서 HTML5를 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-206">Your browser must support HTML5 to view the code highlighted in yellow when viewing this tutorial series in a browser.</span></span>

<span data-ttu-id="b1545-207">위의 코드에 표시 된 것 처럼 응용 프로그램이 시작 되 면 응용 프로그램은 처음에 데이터에 액세스할 때 실행 되는 이니셜라이저를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-207">As shown in the above code, when the application starts, the application specifies the initializer that will run during the first time the data is accessed.</span></span> <span data-ttu-id="b1545-208">`Database` 개체 및 `ProductDatabaseInitializer` 개체에 액세스 하려면 두 개의 추가 네임 스페이스가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-208">The two additional namespaces are required to access the `Database` object and the `ProductDatabaseInitializer` object.</span></span>

 <span data-ttu-id="b1545-209">Web.config 파일 수정</span><span class="sxs-lookup"><span data-stu-id="b1545-209">Modifying the Web.Config File</span></span> 

<span data-ttu-id="b1545-210">데이터베이스가 시드 데이터로 채워질 때 Entity Framework Code First 기본 위치에 데이터베이스를 생성 하므로 응용 프로그램에 사용자 고유의 연결 정보를 추가 하면 데이터베이스 위치를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-210">Although Entity Framework Code First will generate a database for you in a default location when the database is populated with seed data, adding your own connection information to your application gives you control of the database location.</span></span> <span data-ttu-id="b1545-211">프로젝트의 루트에 있는 응용 프로그램의 *web.config* 파일에서 연결 문자열을 사용 하 여이 데이터베이스 연결을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-211">You specify this database connection using a connection string in the application's *Web.config* file at the root of the project.</span></span> <span data-ttu-id="b1545-212">새 연결 문자열을 추가 하 여 데이터베이스 (*wingtiptoys*)의 위치를 기본 위치가 아닌 응용 프로그램의 데이터 디렉터리 (*앱\_데이터*)에서 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-212">By adding a new connection string, you can direct the location of the database (*wingtiptoys.mdf*) to be built in the application's data directory (*App\_Data*), rather than its default location.</span></span> <span data-ttu-id="b1545-213">이렇게 변경 하면이 자습서의 뒷부분에서 데이터베이스 파일을 찾아 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-213">Making this change will allow you to find and inspect the database file later in this tutorial.</span></span>

1. <span data-ttu-id="b1545-214">**솔루션 탐색기**에서 *web.config 파일을 찾아 엽니다.*</span><span class="sxs-lookup"><span data-stu-id="b1545-214">In **Solution Explorer**, find and open the *Web.config* file.</span></span>
2. <span data-ttu-id="b1545-215">노란색으로 강조 표시 된 연결 문자열을 web.config 파일의 `<connectionStrings>` 섹션에 다음과 같이 *추가 합니다.*</span><span class="sxs-lookup"><span data-stu-id="b1545-215">Add the connection string highlighted in yellow to the `<connectionStrings>` section of the *Web.config* file as follows:</span></span>  

    [!code-xml[Main](create_the_data_access_layer/samples/sample6.xml?highlight=4-7)]

<span data-ttu-id="b1545-216">응용 프로그램을 처음 실행 하는 경우 연결 문자열에 지정 된 위치에 데이터베이스를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-216">When the application is run for the first time, it will build the database at the location specified by the connection string.</span></span> <span data-ttu-id="b1545-217">응용 프로그램을 실행 하기 전에 먼저 빌드 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-217">But before running the application, let's build it first.</span></span>

## <a name="building-the-application"></a><span data-ttu-id="b1545-218">응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="b1545-218">Building the Application</span></span>

<span data-ttu-id="b1545-219">웹 응용 프로그램에 대 한 모든 클래스와 변경 내용을 확인 하려면 응용 프로그램을 빌드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-219">To make sure that all the classes and changes to your Web application work, you should build the application.</span></span>

1. <span data-ttu-id="b1545-220">**디버그** 메뉴에서 **WingtipToys 빌드**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-220">From the **Debug** menu, select **Build WingtipToys**.</span></span>  
 <span data-ttu-id="b1545-221">**출력** 창이 표시 되 고 모든 작업이 정상적으로 완료 되 면 *성공* 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-221">The **Output** window is displayed, and if all went well, you see a *succeeded* message.</span></span>  

    ![데이터 액세스 계층-출력 창 만들기](create_the_data_access_layer/_static/image4.png)

<span data-ttu-id="b1545-223">오류가 발생 하는 경우 위의 단계를 다시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-223">If you run into an error, re-check the above steps.</span></span> <span data-ttu-id="b1545-224">**출력** 창의 정보는 문제가 있는 파일 및 파일에서 변경이 필요한 위치를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-224">The information in the **Output** window will indicate which file has a problem and where in the file a change is required.</span></span> <span data-ttu-id="b1545-225">이 정보를 사용 하 여 프로젝트에서 위의 단계를 검토 하 고 수정 해야 하는 부분을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-225">This information will enable you to determine what part of the above steps need to be reviewed and fixed in your project.</span></span>

## <a name="summary"></a><span data-ttu-id="b1545-226">요약</span><span class="sxs-lookup"><span data-stu-id="b1545-226">Summary</span></span>

<span data-ttu-id="b1545-227">데이터 모델을 만든 시리즈의이 자습서에서는 데이터베이스를 초기화 하 고 초기값으로 사용 되는 코드를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-227">In this tutorial of the series you have created the data model, as well as, added the code that will be used to initialize and seed the database.</span></span> <span data-ttu-id="b1545-228">또한 응용 프로그램이 실행 될 때 데이터 모델을 사용 하도록 응용 프로그램을 구성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-228">You have also configured the application to use the data models when the application is run.</span></span>

<span data-ttu-id="b1545-229">다음 자습서에서는 UI를 업데이트 하 고, 탐색을 추가 하 고, 데이터베이스에서 데이터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-229">In the next tutorial, you'll update the UI, add navigation, and retrieve data from the database.</span></span> <span data-ttu-id="b1545-230">그러면이 자습서에서 만든 엔터티 클래스를 기반으로 데이터베이스가 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1545-230">This will result in the database being automatically created based on the entity classes that you created in this tutorial.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b1545-231">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b1545-231">Additional Resources</span></span>

<span data-ttu-id="b1545-232">[Entity Framework 개요](https://msdn.microsoft.com/library/bb399567.aspx) </span><span class="sxs-lookup"><span data-stu-id="b1545-232">[Entity Framework Overview](https://msdn.microsoft.com/library/bb399567.aspx) </span></span>  
<span data-ttu-id="b1545-233">[ADO.NET Entity Framework에 대 한 초보자 가이드](https://msdn.microsoft.com/data/ee712907) </span><span class="sxs-lookup"><span data-stu-id="b1545-233">[Beginner's Guide to the ADO.NET Entity Framework](https://msdn.microsoft.com/data/ee712907) </span></span>  
<span data-ttu-id="b1545-234">[Entity Framework를 사용 하 여 Code First 개발](http://www.msteched.com/2010/Europe/DEV212) (비디오)</span><span class="sxs-lookup"><span data-stu-id="b1545-234">[Code First Development with Entity Framework](http://www.msteched.com/2010/Europe/DEV212) (video)</span></span>   
<span data-ttu-id="b1545-235">[Code First 관계 흐름 API](https://msdn.microsoft.com/data/hh134698) </span><span class="sxs-lookup"><span data-stu-id="b1545-235">[Code First Relationships Fluent API](https://msdn.microsoft.com/data/hh134698) </span></span>  
[<span data-ttu-id="b1545-236">Code First 데이터 주석</span><span class="sxs-lookup"><span data-stu-id="b1545-236">Code First Data Annotations</span></span>](https://msdn.microsoft.com/data/gg193958)  
[<span data-ttu-id="b1545-237">Entity Framework의 생산성 향상</span><span class="sxs-lookup"><span data-stu-id="b1545-237">Productivity Improvements for the Entity Framework</span></span>](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)

> [!div class="step-by-step"]
> <span data-ttu-id="b1545-238">[이전](create-the-project.md)
> [다음](ui_and_navigation.md)</span><span class="sxs-lookup"><span data-stu-id="b1545-238">[Previous](create-the-project.md)
[Next](ui_and_navigation.md)</span></span>
