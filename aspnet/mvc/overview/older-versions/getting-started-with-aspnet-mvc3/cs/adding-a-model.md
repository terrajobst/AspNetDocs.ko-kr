---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model
title: 모델 추가 (C#) | Microsoft Docs
author: Rick-Anderson
description: 참고:이 자습서의 업데이트 된 버전은 ASP.NET MVC 5 및 Visual Studio 2013를 사용 하는 여기에서 사용할 수 있습니다. 보다 안전 하 고, 보다 간단 하 고 데모를 수행 하는 것이 더 간단 합니다.
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 42355b95-5f1f-413e-8d16-14cdfaaefcd8
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: a5f494eaa05bcfcd9d49873db728d71c1fd332c8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434897"
---
# <a name="adding-a-model-c"></a><span data-ttu-id="aeb23-104">모델 추가(C#)</span><span class="sxs-lookup"><span data-stu-id="aeb23-104">Adding a Model (C#)</span></span>

<span data-ttu-id="aeb23-105">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="aeb23-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="aeb23-106">이 자습서에서는 Microsoft Visual Studio의 무료 버전인 Microsoft Visual Web Developer 2010 Express 서비스 팩 1을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-106">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="aeb23-107">시작 하기 전에 아래 나열 된 필수 구성 요소를 설치 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-107">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="aeb23-108">[웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)링크를 클릭 하 여 모든 항목을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-108">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="aeb23-109">또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-109">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="aeb23-110">Visual Studio Web Developer Express SP1 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="aeb23-110">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="aeb23-111">ASP.NET MVC 3 도구 업데이트</span><span class="sxs-lookup"><span data-stu-id="aeb23-111">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="aeb23-112">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)</span><span class="sxs-lookup"><span data-stu-id="aeb23-112">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="aeb23-113">Visual Web Developer 2010 대신 Visual Studio 2010을 사용 하는 경우 [Visual studio 2010 필수 조건](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)링크를 클릭 하 여 필수 구성 요소를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-113">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="aeb23-114">이 항목과 함께 사용할 수 있는 C# 소스 코드가 포함 된 Visual Web Developer 프로젝트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-114">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="aeb23-115">[버전을 C# 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-115">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="aeb23-116">Visual Basic 선호 하는 경우이 자습서의 [Visual Basic 버전](../vb/adding-a-model.md) 으로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-116">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/adding-a-model.md) of this tutorial.</span></span>

## <a name="adding-a-model"></a><span data-ttu-id="aeb23-117">모델 추가</span><span class="sxs-lookup"><span data-stu-id="aeb23-117">Adding a Model</span></span>

<span data-ttu-id="aeb23-118">이 섹션에서는 데이터베이스에서 동영상을 관리 하기 위한 몇 가지 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-118">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="aeb23-119">이러한 클래스는 ASP.NET MVC 응용 프로그램의 "모델" 부분이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-119">These classes will be the "model" part of the ASP.NET MVC application.</span></span>

<span data-ttu-id="aeb23-120">이러한 모델 클래스를 정의 하 고 사용 하려면 Entity Framework 라는 .NET Framework 데이터 액세스 기술을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-120">You'll use a .NET Framework data-access technology known as the Entity Framework to define and work with these model classes.</span></span> <span data-ttu-id="aeb23-121">Entity Framework (EF 라고도 함)는 *Code First*라는 개발 패러다임을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-121">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="aeb23-122">Code First를 사용 하면 간단한 클래스를 작성 하 여 모델 개체를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-122">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="aeb23-123">이러한 항목은 "일반-이전 CLR 개체"에서 POCO 클래스 라고도 합니다. 그런 다음 클래스에서 즉석에서 데이터베이스를 만들 수 있습니다. 이렇게 하면 매우 깔끔하고 빠른 개발 워크플로를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-123">(These are also known as POCO classes, from "plain-old CLR objects.") You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="aeb23-124">모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="aeb23-124">Adding Model Classes</span></span>

<span data-ttu-id="aeb23-125">**솔루션 탐색기**에서 *모델* 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 선택한 다음 **클래스**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-125">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="aeb23-126">*클래스* 이름을 "Movie"로 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-126">Name the *class* "Movie".</span></span>

<span data-ttu-id="aeb23-127">[![CreateMovieClass](adding-a-model/_static/image3.png)](adding-a-model/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="aeb23-127">[![CreateMovieClass](adding-a-model/_static/image3.png)](adding-a-model/_static/image2.png)</span></span>

<span data-ttu-id="aeb23-128">`Movie` 클래스에 다음 5 가지 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-128">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="aeb23-129">`Movie` 클래스를 사용 하 여 데이터베이스의 영화를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-129">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="aeb23-130">`Movie` 개체의 각 인스턴스는 데이터베이스 테이블의 행에 해당 하며 `Movie` 클래스의 각 속성은 테이블의 열에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-130">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="aeb23-131">동일한 파일에서 다음 `MovieDBContext` 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-131">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

<span data-ttu-id="aeb23-132">`MovieDBContext` 클래스는 데이터베이스의 `Movie` 클래스 인스턴스 가져오기, 저장 및 업데이트를 처리 하는 Entity Framework movie 데이터베이스 컨텍스트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-132">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="aeb23-133">`MovieDBContext` Entity Framework에서 제공 하는 `DbContext` 기본 클래스에서 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-133">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span> <span data-ttu-id="aeb23-134">`DbContext` 및 `DbSet`에 대 한 자세한 내용은 [Entity Framework의 생산성 향상](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="aeb23-134">For more information about `DbContext` and `DbSet`, see [Productivity Improvements for the Entity Framework](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0).</span></span>

<span data-ttu-id="aeb23-135">`DbContext` 및 `DbSet`를 참조할 수 있도록 하려면 파일 맨 위에 다음 `using` 문을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-135">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="aeb23-136">전체 *Movie.cs* 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-136">The complete *Movie.cs* file is shown below.</span></span>

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-compact"></a><span data-ttu-id="aeb23-137">연결 문자열 만들기 및 SQL Server Compact 작업</span><span class="sxs-lookup"><span data-stu-id="aeb23-137">Creating a Connection String and Working with SQL Server Compact</span></span>

<span data-ttu-id="aeb23-138">만든 `MovieDBContext` 클래스는 데이터베이스에 연결 하 고 데이터베이스 레코드에 `Movie` 개체를 매핑하는 태스크를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-138">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="aeb23-139">한 가지 질문은 연결할 데이터베이스를 지정 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-139">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="aeb23-140">응용 프로그램의 *web.config* 파일에 연결 정보를 추가 하 여이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-140">You'll do that by adding connection information in the *Web.config* file of the application.</span></span>

<span data-ttu-id="aeb23-141">응용 프로그램 루트 *web.config* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-141">Open the application root *Web.config* file.</span></span> <span data-ttu-id="aeb23-142">*Views* 폴더에 있는 *web.config* 파일이 아닙니다. 아래 이미지에는 *web.config* 파일이 모두 표시 됩니다. red로 *원 된 web.config* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-142">(Not the *Web.config* file in the *Views* folder.) The image below show both *Web.config* files; open the *Web.config* file circled in red.</span></span>

![](adding-a-model/_static/image4.png)

<span data-ttu-id="aeb23-143">*Web.config 파일의* `<connectionStrings>` 요소에 다음 연결 문자열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-143">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

<span data-ttu-id="aeb23-144">다음 예제에서는 새 연결 문자열이 추가 된 *web.config 파일의* 일부를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-144">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](adding-a-model/samples/sample6.xml)]

<span data-ttu-id="aeb23-145">이러한 소량의 코드와 XML은 동영상 데이터를 표시 하 고 데이터베이스에 저장 하기 위해 작성 해야 하는 모든 것입니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-145">This small amount of code and XML is everything you need to write in order to represent and store the movie data in a database.</span></span>

<span data-ttu-id="aeb23-146">다음으로, 영화 데이터를 표시 하 고 사용자가 새 영화 목록을 만들 수 있도록 하는 새 `MoviesController` 클래스를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb23-146">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="aeb23-147">[이전](adding-a-view.md)
> [다음](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="aeb23-147">[Previous](adding-a-view.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
