---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
title: 데이터베이스 데이터의 테이블 표시 (VB) | Microsoft Docs
author: microsoft
description: 이 자습서에서는 데이터베이스 레코드 집합을 표시 하는 두 가지 방법을 보여 줍니다. HTML ta에서 데이터베이스 레코드 집합의 형식을 지정 하는 두 가지 방법을 보여 줍니다.
ms.author: riande
ms.date: 10/07/2008
ms.assetid: 5bb4587f-5bcd-44f5-b368-3c1709162b35
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
msc.type: authoredcontent
ms.openlocfilehash: f2e2489ac8455913f55c746dbe05b9fe8272285b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78436739"
---
# <a name="displaying-a-table-of-database-data-vb"></a><span data-ttu-id="d3655-104">데이터베이스 데이터의 테이블 표시(VB)</span><span class="sxs-lookup"><span data-stu-id="d3655-104">Displaying a Table of Database Data (VB)</span></span>

<span data-ttu-id="d3655-105">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="d3655-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="d3655-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="d3655-106">Download PDF</span></span>](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_VB.pdf)

> <span data-ttu-id="d3655-107">이 자습서에서는 데이터베이스 레코드 집합을 표시 하는 두 가지 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-107">In this tutorial, I demonstrate two methods of displaying a set of database records.</span></span> <span data-ttu-id="d3655-108">HTML 테이블에서 데이터베이스 레코드 집합의 서식을 지정 하는 두 가지 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-108">I show two methods of formatting a set of database records in an HTML table.</span></span> <span data-ttu-id="d3655-109">먼저 뷰 내에서 직접 데이터베이스 레코드의 형식을 지정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-109">First, I show how you can format the database records directly within a view.</span></span> <span data-ttu-id="d3655-110">다음으로 데이터베이스 레코드를 포맷할 때 부분를 활용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-110">Next, I demonstrate how you can take advantage of partials when formatting database records.</span></span>

<span data-ttu-id="d3655-111">이 자습서의 목표는 ASP.NET MVC 응용 프로그램에서 데이터베이스 데이터의 HTML 테이블을 표시 하는 방법을 설명 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-111">The goal of this tutorial is to explain how you can display an HTML table of database data in an ASP.NET MVC application.</span></span> <span data-ttu-id="d3655-112">먼저 Visual Studio에 포함 된 스 캐 폴딩 도구를 사용 하 여 레코드 집합을 자동으로 표시 하는 뷰를 생성 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-112">First, you learn how to use the scaffolding tools included in Visual Studio to generate a view that displays a set of records automatically.</span></span> <span data-ttu-id="d3655-113">다음으로 데이터베이스 레코드를 포맷할 때 부분을 템플릿으로 사용 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-113">Next, you learn how to use a partial as a template when formatting database records.</span></span>

## <a name="create-the-model-classes"></a><span data-ttu-id="d3655-114">모델 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="d3655-114">Create the Model Classes</span></span>

<span data-ttu-id="d3655-115">영화 데이터베이스 테이블의 레코드 집합을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-115">We are going to display the set of records from the Movies database table.</span></span> <span data-ttu-id="d3655-116">동영상 데이터베이스 테이블에는 다음 열이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-116">The Movies database table contains the following columns:</span></span>

<a id="0.4_table01"></a>

| <span data-ttu-id="d3655-117">**열 이름**</span><span class="sxs-lookup"><span data-stu-id="d3655-117">**Column Name**</span></span> | <span data-ttu-id="d3655-118">**데이터 형식**</span><span class="sxs-lookup"><span data-stu-id="d3655-118">**Data Type**</span></span> | <span data-ttu-id="d3655-119">**Null 허용**</span><span class="sxs-lookup"><span data-stu-id="d3655-119">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d3655-120">Id</span><span class="sxs-lookup"><span data-stu-id="d3655-120">Id</span></span> | <span data-ttu-id="d3655-121">Int</span><span class="sxs-lookup"><span data-stu-id="d3655-121">Int</span></span> | <span data-ttu-id="d3655-122">False</span><span class="sxs-lookup"><span data-stu-id="d3655-122">False</span></span> |
| <span data-ttu-id="d3655-123">제목</span><span class="sxs-lookup"><span data-stu-id="d3655-123">Title</span></span> | <span data-ttu-id="d3655-124">Nvarchar(200)</span><span class="sxs-lookup"><span data-stu-id="d3655-124">Nvarchar(200)</span></span> | <span data-ttu-id="d3655-125">False</span><span class="sxs-lookup"><span data-stu-id="d3655-125">False</span></span> |
| <span data-ttu-id="d3655-126">감독</span><span class="sxs-lookup"><span data-stu-id="d3655-126">Director</span></span> | <span data-ttu-id="d3655-127">NVarchar(50)</span><span class="sxs-lookup"><span data-stu-id="d3655-127">NVarchar(50)</span></span> | <span data-ttu-id="d3655-128">False</span><span class="sxs-lookup"><span data-stu-id="d3655-128">False</span></span> |
| <span data-ttu-id="d3655-129">DateReleased</span><span class="sxs-lookup"><span data-stu-id="d3655-129">DateReleased</span></span> | <span data-ttu-id="d3655-130">DateTime</span><span class="sxs-lookup"><span data-stu-id="d3655-130">DateTime</span></span> | <span data-ttu-id="d3655-131">False</span><span class="sxs-lookup"><span data-stu-id="d3655-131">False</span></span> |

<span data-ttu-id="d3655-132">ASP.NET MVC 응용 프로그램에서 영화 테이블을 나타내려면 모델 클래스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-132">In order to represent the Movies table in our ASP.NET MVC application, we need to create a model class.</span></span> <span data-ttu-id="d3655-133">이 자습서에서는 Microsoft Entity Framework를 사용 하 여 모델 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-133">In this tutorial, we use the Microsoft Entity Framework to create our model classes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="d3655-134">이 자습서에서는 Microsoft Entity Framework를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-134">In this tutorial, we use the Microsoft Entity Framework.</span></span> <span data-ttu-id="d3655-135">그러나 LINQ to SQL, NHibernate 절전 모드 또는 ADO.NET를 포함 하 여 ASP.NET MVC 응용 프로그램에서 데이터베이스와 상호 작용 하는 다양 한 기술을 사용할 수 있음을 이해 하는 것이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-135">However, it is important to understand that you can use a variety of different technologies to interact with a database from an ASP.NET MVC application including LINQ to SQL, NHibernate, or ADO.NET.</span></span>

<span data-ttu-id="d3655-136">엔터티 데이터 모델 마법사를 시작 하려면 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-136">Follow these steps to launch the Entity Data Model Wizard:</span></span>

1. <span data-ttu-id="d3655-137">솔루션 탐색기 창에서 모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **추가, 새 항목을**차례로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-137">Right-click the Models folder in the Solution Explorer window and the select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="d3655-138">**데이터** 범주를 선택 하 고 **ADO.NET 엔터티 데이터 모델** 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-138">Select the **Data** category and select the **ADO.NET Entity Data Model** template.</span></span>
3. <span data-ttu-id="d3655-139">데이터 모델에 *MoviesDBModel* 의 이름을 지정 하 고 **추가** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-139">Give your data model the name *MoviesDBModel.edmx* and click the **Add** button.</span></span>

<span data-ttu-id="d3655-140">추가 단추를 클릭 하면 엔터티 데이터 모델 마법사가 나타납니다 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="d3655-140">After you click the Add button, the Entity Data Model Wizard appears (see Figure 1).</span></span> <span data-ttu-id="d3655-141">마법사를 완료 하려면 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-141">Follow these steps to complete the wizard:</span></span>

1. <span data-ttu-id="d3655-142">**모델 콘텐츠 선택** 단계에서 **데이터베이스에서 생성** 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-142">In the **Choose Model Contents** step, select the **Generate from database** option.</span></span>
2. <span data-ttu-id="d3655-143">**데이터 연결 선택** 단계에서 연결 설정에 대해 *MoviesDB* 데이터 연결 및 이름 *MoviesDBEntities* 을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-143">In the **Choose Your Data Connection** step, use the *MoviesDB.mdf* data connection and the name *MoviesDBEntities* for the connection settings.</span></span> <span data-ttu-id="d3655-144">**다음** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-144">Click the **Next** button.</span></span>
3. <span data-ttu-id="d3655-145">**데이터베이스 개체 선택** 단계에서 테이블 노드를 확장 하 고 동영상 테이블을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-145">In the **Choose Your Database Objects** step, expand the Tables node, select the Movies table.</span></span> <span data-ttu-id="d3655-146">네임 스페이스 *모델* 을 입력 하 고 **마침** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-146">Enter the namespace *Models* and click the **Finish** button.</span></span>

<span data-ttu-id="d3655-147">[LINQ to SQL 클래스 ![만들기](displaying-a-table-of-database-data-vb/_static/image1.jpg)](displaying-a-table-of-database-data-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d3655-147">[![Creating LINQ to SQL classes](displaying-a-table-of-database-data-vb/_static/image1.jpg)](displaying-a-table-of-database-data-vb/_static/image1.png)</span></span>

<span data-ttu-id="d3655-148">**그림 01**: LINQ to SQL 클래스 만들기 ([전체 크기 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="d3655-148">**Figure 01**: Creating LINQ to SQL classes ([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image2.png))</span></span>

<span data-ttu-id="d3655-149">엔터티 데이터 모델 마법사를 완료 하면 엔터티 데이터 모델 디자이너가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-149">After you complete the Entity Data Model Wizard, the Entity Data Model Designer opens.</span></span> <span data-ttu-id="d3655-150">디자이너에서 영화 엔터티를 표시 합니다 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="d3655-150">The Designer should display the Movies entity (see Figure 2).</span></span>

<span data-ttu-id="d3655-151">[엔터티 데이터 모델 디자이너 ![](displaying-a-table-of-database-data-vb/_static/image2.jpg)](displaying-a-table-of-database-data-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="d3655-151">[![The Entity Data Model Designer](displaying-a-table-of-database-data-vb/_static/image2.jpg)](displaying-a-table-of-database-data-vb/_static/image3.png)</span></span>

<span data-ttu-id="d3655-152">**그림 02**: 엔터티 데이터 모델 디자이너 ([전체 크기 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="d3655-152">**Figure 02**: The Entity Data Model Designer ([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image4.png))</span></span>

<span data-ttu-id="d3655-153">계속 하기 전에 한 가지 변경 작업을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-153">We need to make one change before we continue.</span></span> <span data-ttu-id="d3655-154">엔터티 데이터 마법사는 동영상 데이터베이스 테이블을 나타내는 *영화* 라는 모델 클래스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-154">The Entity Data Wizard generates a model class named *Movies* that represents the Movies database table.</span></span> <span data-ttu-id="d3655-155">영화 클래스를 사용 하 여 특정 영화를 나타내므로 클래스의 *이름을 동영상이* *아닌 영화 (* 복수형이 아닌 단일 영화)로 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-155">Because we'll use the Movies class to represent a particular movie, we need to modify the name of the class to be *Movie* instead of *Movies* (singular rather than plural).</span></span>

<span data-ttu-id="d3655-156">디자이너 화면에서 클래스의 이름을 두 번 클릭 하 고 클래스의 이름을 동영상에서 동영상으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-156">Double-click the name of the class on the designer surface and change the name of the class from Movies to Movie.</span></span> <span data-ttu-id="d3655-157">이렇게 변경한 후에는 **저장** 단추 (플로피 디스크의 아이콘)를 클릭 하 여 Movie 클래스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-157">After making this change, click the **Save** button (the icon of the floppy disk) to generate the Movie class.</span></span>

## <a name="create-the-movies-controller"></a><span data-ttu-id="d3655-158">동영상 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="d3655-158">Create the Movies Controller</span></span>

<span data-ttu-id="d3655-159">이제 데이터베이스 레코드를 표시 하는 방법을 만들었으므로 영화 컬렉션을 반환 하는 컨트롤러를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-159">Now that we have a way to represent our database records, we can create a controller that returns the collection of movies.</span></span> <span data-ttu-id="d3655-160">Visual Studio 솔루션 탐색기 창에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **추가, 컨트롤러** (그림 3 참조)를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-160">Within the Visual Studio Solution Explorer window, right-click the Controllers folder and select the menu option **Add, Controller** (see Figure 3).</span></span>

<span data-ttu-id="d3655-161">[컨트롤러 추가 메뉴 ![](displaying-a-table-of-database-data-vb/_static/image3.jpg)](displaying-a-table-of-database-data-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="d3655-161">[![The Add Controller Menu](displaying-a-table-of-database-data-vb/_static/image3.jpg)](displaying-a-table-of-database-data-vb/_static/image5.png)</span></span>

<span data-ttu-id="d3655-162">**그림 03**: 컨트롤러 추가 메뉴 ([전체 크기 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="d3655-162">**Figure 03**: The Add Controller Menu ([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image6.png))</span></span>

<span data-ttu-id="d3655-163">**컨트롤러 추가** 대화 상자가 나타나면 컨트롤러 이름 MovieController을 입력 합니다 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="d3655-163">When the **Add Controller** dialog appears, enter the controller name MovieController (see Figure 4).</span></span> <span data-ttu-id="d3655-164">**추가** 단추를 클릭 하 여 새 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-164">Click the **Add** button to add the new controller.</span></span>

<span data-ttu-id="d3655-165">[컨트롤러 추가 대화 상자 ![](displaying-a-table-of-database-data-vb/_static/image4.jpg)](displaying-a-table-of-database-data-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="d3655-165">[![The Add Controller dialog](displaying-a-table-of-database-data-vb/_static/image4.jpg)](displaying-a-table-of-database-data-vb/_static/image7.png)</span></span>

<span data-ttu-id="d3655-166">**그림 04**: 컨트롤러 추가 대화 상자 ([전체 크기 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="d3655-166">**Figure 04**: The Add Controller dialog([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image8.png))</span></span>

<span data-ttu-id="d3655-167">데이터베이스 레코드 집합을 반환 하도록 동영상 컨트롤러에서 노출 하는 Index () 동작을 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-167">We need to modify the Index() action exposed by the Movie controller so that it returns the set of database records.</span></span> <span data-ttu-id="d3655-168">컨트롤러를 목록 1의 컨트롤러와 같이 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-168">Modify the controller so that it looks like the controller in Listing 1.</span></span>

<span data-ttu-id="d3655-169">**목록 1 – Controllers\MovieController.vb**</span><span class="sxs-lookup"><span data-stu-id="d3655-169">**Listing 1 – Controllers\MovieController.vb**</span></span>

[!code-vb[Main](displaying-a-table-of-database-data-vb/samples/sample1.vb)]

<span data-ttu-id="d3655-170">목록 1에서 MoviesDBEntities 클래스는 MoviesDB 데이터베이스를 나타내는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-170">In Listing 1, the MoviesDBEntities class is used to represent the MoviesDB database.</span></span> <span data-ttu-id="d3655-171">식 *엔터티입니다. MovieSet ()* 는 동영상 데이터베이스 테이블에서 모든 동영상의 집합을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-171">The expression *entities.MovieSet.ToList()* returns the set of all movies from the Movies database table.</span></span>

## <a name="create-the-view"></a><span data-ttu-id="d3655-172">보기 만들기</span><span class="sxs-lookup"><span data-stu-id="d3655-172">Create the View</span></span>

<span data-ttu-id="d3655-173">HTML 테이블에 데이터베이스 레코드 집합을 표시 하는 가장 쉬운 방법은 Visual Studio에서 제공 하는 스 캐 폴딩을 활용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-173">The easiest way to display a set of database records in an HTML table is to take advantage of the scaffolding provided by Visual Studio.</span></span>

<span data-ttu-id="d3655-174">**빌드, 솔루션 빌드**메뉴 옵션을 선택 하 여 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-174">Build your application by selecting the menu option **Build, Build Solution**.</span></span> <span data-ttu-id="d3655-175">**뷰 추가** 대화 상자를 열기 전에 응용 프로그램을 빌드해야 합니다. 그렇지 않으면 데이터 클래스가 대화 상자에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-175">You must build your application before opening the **Add View** dialog or your data classes won't appear in the dialog.</span></span>

<span data-ttu-id="d3655-176">Index () 작업을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **뷰 추가** 를 선택 합니다 (그림 5 참조).</span><span class="sxs-lookup"><span data-stu-id="d3655-176">Right-click the Index() action and select the menu option **Add View** (see Figure 5).</span></span>

<span data-ttu-id="d3655-177">[뷰를 추가 ![](displaying-a-table-of-database-data-vb/_static/image5.jpg)](displaying-a-table-of-database-data-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="d3655-177">[![Adding a view](displaying-a-table-of-database-data-vb/_static/image5.jpg)](displaying-a-table-of-database-data-vb/_static/image9.png)</span></span>

<span data-ttu-id="d3655-178">**그림 05**: 보기 추가 ([전체 크기 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="d3655-178">**Figure 05**: Adding a view ([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image10.png))</span></span>

<span data-ttu-id="d3655-179">**보기 추가** 대화 상자에서 **강력한 형식의 뷰 만들기**확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-179">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="d3655-180">Movie 클래스를 **뷰 데이터 클래스로**선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-180">Select the Movie class as the **view data class**.</span></span> <span data-ttu-id="d3655-181">**보기 내용** 으로 *목록* 을 선택 합니다 (그림 6 참조).</span><span class="sxs-lookup"><span data-stu-id="d3655-181">Select *List* as the **view content** (see Figure 6).</span></span> <span data-ttu-id="d3655-182">이러한 옵션을 선택 하면 동영상 목록이 표시 되는 강력한 형식의 보기가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-182">Selecting these options will generate a strongly-typed view that displays a list of movies.</span></span>

<span data-ttu-id="d3655-183">[뷰 추가 대화 상자 ![](displaying-a-table-of-database-data-vb/_static/image6.jpg)](displaying-a-table-of-database-data-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="d3655-183">[![The Add View dialog](displaying-a-table-of-database-data-vb/_static/image6.jpg)](displaying-a-table-of-database-data-vb/_static/image11.png)</span></span>

<span data-ttu-id="d3655-184">**그림 06**: 보기 추가 대화 상자 ([전체 크기 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="d3655-184">**Figure 06**: The Add View dialog([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image12.png))</span></span>

<span data-ttu-id="d3655-185">**추가** 단추를 클릭 하면 목록 2의 뷰가 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-185">After you click the **Add** button, the view in Listing 2 is generated automatically.</span></span> <span data-ttu-id="d3655-186">이 보기에는 동영상의 컬렉션을 반복 하 고 동영상의 각 속성을 표시 하는 데 필요한 코드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-186">This view contains the code required to iterate through the collection of movies and display each of the properties of a movie.</span></span>

<span data-ttu-id="d3655-187">**목록 2 – Views\Movie\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="d3655-187">**Listing 2 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample2.aspx)]

<span data-ttu-id="d3655-188">**디버그, 디버깅 시작** 을 선택 하거나 F5 키를 눌러 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-188">You can run the application by selecting the menu option **Debug, Start Debugging** (or hitting the F5 key).</span></span> <span data-ttu-id="d3655-189">응용 프로그램을 실행 하면 Internet Explorer가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-189">Running the application launches Internet Explorer.</span></span> <span data-ttu-id="d3655-190">/Dlurl로 이동 하면 그림 7에 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-190">If you navigate to the /Movie URL then you'll see the page in Figure 7.</span></span>

<span data-ttu-id="d3655-191">[영화 테이블 ![](displaying-a-table-of-database-data-vb/_static/image7.jpg)](displaying-a-table-of-database-data-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="d3655-191">[![A table of movies](displaying-a-table-of-database-data-vb/_static/image7.jpg)](displaying-a-table-of-database-data-vb/_static/image13.png)</span></span>

<span data-ttu-id="d3655-192">**그림 07**: 동영상 표 ([전체 크기 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="d3655-192">**Figure 07**: A table of movies([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image14.png))</span></span>

<span data-ttu-id="d3655-193">그림 7에서 데이터베이스 레코드 표의 모양에 대 한 정보를 원하지 않는 경우 인덱스 뷰를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-193">If you don't like anything about the appearance of the grid of database records in Figure 7 then you can simply modify the Index view.</span></span> <span data-ttu-id="d3655-194">예를 들어 인덱스 뷰를 수정 하 여 *DateReleased* 헤더를 *릴리스 날짜로* 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-194">For example, you can change the *DateReleased* header to *Date Released* by modifying the Index view.</span></span>

## <a name="create-a-template-with-a-partial"></a><span data-ttu-id="d3655-195">부분을 사용 하 여 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="d3655-195">Create a Template with a Partial</span></span>

<span data-ttu-id="d3655-196">뷰가 너무 복잡 한 경우 뷰를 부분로 나누는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-196">When a view gets too complicated, it is a good idea to start breaking the view into partials.</span></span> <span data-ttu-id="d3655-197">부분를 사용 하면 보기를 더 쉽게 이해 하 고 유지 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-197">Using partials makes your views easier to understand and maintain.</span></span> <span data-ttu-id="d3655-198">각 영화 데이터베이스 레코드에 서식을 지정 하는 템플릿으로 사용할 수 있는 부분을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-198">We'll create a partial that we can use as a template to format each of the movie database records.</span></span>

<span data-ttu-id="d3655-199">부분을 만들려면 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-199">Follow these steps to create the partial:</span></span>

1. <span data-ttu-id="d3655-200">Views\Movie 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **뷰 추가**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-200">Right-click the Views\Movie folder and select the menu option **Add View**.</span></span>
2. <span data-ttu-id="d3655-201">*부분 뷰 (.ascx) 만들기*라는 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-201">Check the checkbox labeled *Create a partial view (.ascx)*.</span></span>
3. <span data-ttu-id="d3655-202">부분 *MovieTemplate*의 이름을로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-202">Name the partial *MovieTemplate*.</span></span>
4. <span data-ttu-id="d3655-203">**강력한 형식의 뷰 만들기**확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-203">Check the checkbox labeled **Create a strongly-typed view**.</span></span>
5. <span data-ttu-id="d3655-204">*데이터 보기 클래스로*영화를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-204">Select Movie as the *view data class*.</span></span>
6. <span data-ttu-id="d3655-205">*보기 콘텐츠로 빈 항목*을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-205">Select Empty as the *view content*.</span></span>
7. <span data-ttu-id="d3655-206">**추가** 단추를 클릭 하 여 프로젝트에 부분을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-206">Click the **Add** button to add the partial to your project.</span></span>

<span data-ttu-id="d3655-207">이러한 단계를 완료 한 후 MovieTemplate 부분을 수정 하 여 목록 3 처럼 보이게 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-207">After you complete these steps, modify the MovieTemplate partial to look like Listing 3.</span></span>

<span data-ttu-id="d3655-208">**목록 3 – Views\Movie\MovieTemplate.ascx**</span><span class="sxs-lookup"><span data-stu-id="d3655-208">**Listing 3 – Views\Movie\MovieTemplate.ascx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample3.aspx)]

<span data-ttu-id="d3655-209">목록 3의 부분에는 레코드의 단일 행에 대 한 템플릿이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-209">The partial in Listing 3 contains a template for a single row of records.</span></span>

<span data-ttu-id="d3655-210">목록 4의 수정 된 인덱스 뷰는 MovieTemplate 부분을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-210">The modified Index view in Listing 4 uses the MovieTemplate partial.</span></span>

<span data-ttu-id="d3655-211">**목록 4 – Views\Movie\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="d3655-211">**Listing 4 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample4.aspx)]

<span data-ttu-id="d3655-212">목록 4의 뷰에는 모든 영화를 반복 하는 For Each 루프가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-212">The view in Listing 4 contains a For Each loop that iterates through all of the movies.</span></span> <span data-ttu-id="d3655-213">각 영화에 대해 MovieTemplate 부분을 사용 하 여 동영상의 서식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-213">For each movie, the MovieTemplate partial is used to format the movie.</span></span> <span data-ttu-id="d3655-214">MovieTemplate는 RenderPartial () 도우미 메서드를 호출 하 여 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-214">The MovieTemplate is rendered by calling the RenderPartial() helper method.</span></span>

<span data-ttu-id="d3655-215">수정 된 인덱스 뷰는 데이터베이스 레코드의 동일한 HTML 테이블을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-215">The modified Index view renders the very same HTML table of database records.</span></span> <span data-ttu-id="d3655-216">그러나 뷰가 크게 간소화 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-216">However, the view has been greatly simplified.</span></span>

<span data-ttu-id="d3655-217">RenderPartial () 메서드는 문자열을 반환 하지 않기 때문에 대부분의 다른 도우미 메서드와는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-217">The RenderPartial() method is different than most of the other helper methods because it does not return a string.</span></span> <span data-ttu-id="d3655-218">따라서 &lt;% = Html RenderPartial ()%&gt;대신 &lt;% Html RenderPartial ()%&gt;를 사용 하 여 RenderPartial () 메서드를 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-218">Therefore, you must call the RenderPartial() method using &lt;% Html.RenderPartial() %&gt; instead of &lt;%= Html.RenderPartial() %&gt;.</span></span>

## <a name="summary"></a><span data-ttu-id="d3655-219">요약</span><span class="sxs-lookup"><span data-stu-id="d3655-219">Summary</span></span>

<span data-ttu-id="d3655-220">이 자습서의 목표는 HTML 테이블에 데이터베이스 레코드 집합을 표시 하는 방법을 설명 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-220">The goal of this tutorial was to explain how you can display a set of database records in an HTML table.</span></span> <span data-ttu-id="d3655-221">먼저 Microsoft Entity Framework를 활용 하 여 컨트롤러 작업에서 데이터베이스 레코드 집합을 반환 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-221">First, you learned how to return a set of database records from a controller action by taking advantage of the Microsoft Entity Framework.</span></span> <span data-ttu-id="d3655-222">다음으로, Visual Studio 스 캐 폴딩을 사용 하 여 항목 컬렉션을 자동으로 표시 하는 뷰를 생성 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-222">Next, you learned how to use Visual Studio scaffolding to generate a view that displays a collection of items automatically.</span></span> <span data-ttu-id="d3655-223">마지막으로, 부분을 활용 하 여 뷰를 간소화 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-223">Finally, you learned how to simplify the view by taking advantage of a partial.</span></span> <span data-ttu-id="d3655-224">각 데이터베이스 레코드에 서식을 지정할 수 있도록 부분을 템플릿으로 사용 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="d3655-224">You learned how to use a partial as a template so that you can format each database record.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d3655-225">[이전](creating-model-classes-with-linq-to-sql-vb.md)
> [다음](performing-simple-validation-vb.md)</span><span class="sxs-lookup"><span data-stu-id="d3655-225">[Previous](creating-model-classes-with-linq-to-sql-vb.md)
[Next](performing-simple-validation-vb.md)</span></span>
