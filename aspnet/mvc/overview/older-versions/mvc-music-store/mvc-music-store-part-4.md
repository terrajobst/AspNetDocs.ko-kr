---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
title: '4 부: 모델 및 데이터 액세스 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 4 부에서는 모델 및 데이터 액세스를 다룹니다.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: ab55ca81-ab9b-44a0-8700-dc6da2599335
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
msc.type: authoredcontent
ms.openlocfilehash: 402be340f1ea3344675e7b859cea8c5130cfc8ee
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451019"
---
# <a name="part-4-models-and-data-access"></a><span data-ttu-id="a145c-104">4 부: 모델 및 데이터 액세스</span><span class="sxs-lookup"><span data-stu-id="a145c-104">Part 4: Models and Data Access</span></span>

<span data-ttu-id="a145c-105">받은 사람 ( [Jon Galloway](https://github.com/jongalloway) )</span><span class="sxs-lookup"><span data-stu-id="a145c-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="a145c-106">MVC Music Store는 웹 개발용 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 소개 하 고 설명 하는 자습서 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="a145c-107">MVC Music Store는 온라인으로 음악 앨범을 판매 하 고 기본적인 사이트 관리, 사용자 로그인 및 쇼핑 카트 기능을 구현 하는 간단한 샘플 저장소 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>
> 
> <span data-ttu-id="a145c-108">이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="a145c-109">4 부에서는 모델 및 데이터 액세스를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-109">Part 4 covers Models and Data Access.</span></span>

<span data-ttu-id="a145c-110">지금까지 컨트롤러에서 보기 템플릿으로 "더미 데이터"를 전달 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-110">So far, we've just been passing "dummy data" from our Controllers to our View templates.</span></span> <span data-ttu-id="a145c-111">이제 실제 데이터베이스를 연결할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-111">Now we're ready to hook up a real database.</span></span> <span data-ttu-id="a145c-112">이 자습서에서는 데이터베이스 엔진으로 SQL Server Compact 버전 (SQL CE 라고도 함)을 사용 하는 방법을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-112">In this tutorial we'll be covering how to use SQL Server Compact Edition (often called SQL CE) as our database engine.</span></span> <span data-ttu-id="a145c-113">SQL CE는 설치 또는 구성이 필요 하지 않은, 포함 된 무료 파일 기반 데이터베이스 이며,이를 통해 로컬 개발에 매우 편리 하 게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-113">SQL CE is a free, embedded, file based database that doesn't require any installation or configuration, which makes it really convenient for local development.</span></span>

## <a name="database-access-with-entity-framework-code-first"></a><span data-ttu-id="a145c-114">Entity Framework 코드-First를 사용 하 여 데이터베이스 액세스</span><span class="sxs-lookup"><span data-stu-id="a145c-114">Database access with Entity Framework Code-First</span></span>

<span data-ttu-id="a145c-115">ASP.NET MVC 3 프로젝트에 포함 된 EF (Entity Framework) 지원을 사용 하 여 데이터베이스를 쿼리하고 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-115">We'll use the Entity Framework (EF) support that is included in ASP.NET MVC 3 projects to query and update the database.</span></span> <span data-ttu-id="a145c-116">EF는 개발자가 데이터베이스에 저장 된 데이터를 개체 지향 방식으로 쿼리 및 업데이트할 수 있도록 하는 유연한 ORM (개체 관계형 매핑) 데이터 API입니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-116">EF is a flexible object relational mapping (ORM) data API that enables developers to query and update data stored in a database in an object-oriented way.</span></span>

<span data-ttu-id="a145c-117">Entity Framework 버전 4는 code first 라는 개발 패러다임을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-117">Entity Framework version 4 supports a development paradigm called code-first.</span></span> <span data-ttu-id="a145c-118">코드 우선을 사용 하면 간단한 클래스 ("일반-이전" CLR 개체에서 POCO 라고도 함)를 작성 하 여 모델 개체를 만들고 클래스에서 즉석에서 데이터베이스를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-118">Code-first allows you to create model object by writing simple classes (also known as POCO from "plain-old" CLR objects), and can even create the database on the fly from your classes.</span></span>

### <a name="changes-to-our-model-classes"></a><span data-ttu-id="a145c-119">모델 클래스의 변경 내용</span><span class="sxs-lookup"><span data-stu-id="a145c-119">Changes to our Model Classes</span></span>

<span data-ttu-id="a145c-120">이 자습서에서는 Entity Framework의 데이터베이스 만들기 기능을 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-120">We will be leveraging the database creation feature in Entity Framework in this tutorial.</span></span> <span data-ttu-id="a145c-121">그러나이 작업을 수행 하기 전에 나중에 사용 하 게 될 몇 가지 작업을 위해 모델 클래스에 몇 가지 사소한 변경을 수행 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-121">Before we do that, though, let's make a few minor changes to our model classes to add in some things we'll be using later on.</span></span>

#### <a name="adding-the-artist-model-classes"></a><span data-ttu-id="a145c-122">음악가 모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="a145c-122">Adding the Artist Model Classes</span></span>

<span data-ttu-id="a145c-123">Microsoft의 앨범이 아티스트와 연결 되므로 음악가를 설명 하는 간단한 모델 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-123">Our Albums will be associated with Artists, so we'll add a simple model class to describe an Artist.</span></span> <span data-ttu-id="a145c-124">아래에 표시 된 코드를 사용 하 여 Artist.cs 라는 모델 폴더에 새 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-124">Add a new class to the Models folder named Artist.cs using the code shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample1.cs)]

#### <a name="updating-our-model-classes"></a><span data-ttu-id="a145c-125">모델 클래스 업데이트</span><span class="sxs-lookup"><span data-stu-id="a145c-125">Updating our Model Classes</span></span>

<span data-ttu-id="a145c-126">아래와 같이 앨범 클래스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-126">Update the Album class as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample2.cs)]

<span data-ttu-id="a145c-127">다음으로, 장르 클래스를 다음과 같이 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-127">Next, make the following updates to the Genre class.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample3.cs)]

### <a name="adding-the-app_data-folder"></a><span data-ttu-id="a145c-128">앱\_데이터 폴더 추가</span><span class="sxs-lookup"><span data-stu-id="a145c-128">Adding the App\_Data folder</span></span>

<span data-ttu-id="a145c-129">응용 프로그램\_데이터 디렉터리를 프로젝트에 추가 하 여 SQL Server Express 데이터베이스 파일을 보관 합니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-129">We'll add an App\_Data directory to our project to hold our SQL Server Express database files.</span></span> <span data-ttu-id="a145c-130">앱\_데이터는 이미 데이터베이스 액세스에 대 한 올바른 보안 액세스 권한이 있는 ASP.NET의 특수 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-130">App\_Data is a special directory in ASP.NET which already has the correct security access permissions for database access.</span></span> <span data-ttu-id="a145c-131">프로젝트 메뉴에서 ASP.NET 폴더 추가, 앱\_데이터를 차례로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-131">From the Project menu, select Add ASP.NET Folder, then App\_Data.</span></span>

![](mvc-music-store-part-4/_static/image1.png)

### <a name="creating-a-connection-string-in-the-webconfig-file"></a><span data-ttu-id="a145c-132">Web.config 파일에 연결 문자열 만들기</span><span class="sxs-lookup"><span data-stu-id="a145c-132">Creating a Connection String in the web.config file</span></span>

<span data-ttu-id="a145c-133">Entity Framework에서 데이터베이스에 연결 하는 방법을 알 수 있도록 웹 사이트의 구성 파일에 몇 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-133">We will add a few lines to the website's configuration file so that Entity Framework knows how to connect to our database.</span></span> <span data-ttu-id="a145c-134">프로젝트의 루트에 있는 web.config 파일을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-134">Double-click on the Web.config file located in the root of the project.</span></span>

![](mvc-music-store-part-4/_static/image2.png)

<span data-ttu-id="a145c-135">아래와 같이이 파일의 아래쪽으로 스크롤하고 마지막 줄 바로 위에 &lt;connectionStrings&gt; 섹션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-135">Scroll to the bottom of this file and add a &lt;connectionStrings&gt; section directly above the last line, as shown below.</span></span>

[!code-xml[Main](mvc-music-store-part-4/samples/sample4.xml)]

### <a name="adding-a-context-class"></a><span data-ttu-id="a145c-136">컨텍스트 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="a145c-136">Adding a Context Class</span></span>

<span data-ttu-id="a145c-137">모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 MusicStoreEntities.cs 이라는 새 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-137">Right-click the Models folder and add a new class named MusicStoreEntities.cs.</span></span>

![](mvc-music-store-part-4/_static/image3.png)

<span data-ttu-id="a145c-138">이 클래스는 Entity Framework 데이터베이스 컨텍스트를 나타내며 us에 대 한 만들기, 읽기, 업데이트 및 삭제 작업을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-138">This class will represent the Entity Framework database context, and will handle our create, read, update, and delete operations for us.</span></span> <span data-ttu-id="a145c-139">이 클래스의 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-139">The code for this class is shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample5.cs)]

<span data-ttu-id="a145c-140">그 이유는 다른 구성, 특수 인터페이스 등이 없다는 것입니다. MusicStoreEntities 클래스는 DbContext 기본 클래스를 확장 하 여 microsoft의 데이터베이스 작업을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-140">That's it - there's no other configuration, special interfaces, etc. By extending the DbContext base class, our MusicStoreEntities class is able to handle our database operations for us.</span></span> <span data-ttu-id="a145c-141">이제 후크 되었으므로 모델 클래스에 몇 가지 속성을 추가 하 여 데이터베이스의 일부 추가 정보를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-141">Now that we've got that hooked up, let's add a few more properties to our model classes to take advantage of some of the additional information in our database.</span></span>

### <a name="adding-our-store-catalog-data"></a><span data-ttu-id="a145c-142">저장소 카탈로그 데이터 추가</span><span class="sxs-lookup"><span data-stu-id="a145c-142">Adding our store catalog data</span></span>

<span data-ttu-id="a145c-143">새로 만든 데이터베이스에 "초기값" 데이터를 추가 하는 Entity Framework 기능을 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-143">We will take advantage of a feature in Entity Framework which adds "seed" data to a newly created database.</span></span> <span data-ttu-id="a145c-144">그러면 스토어 카탈로그를 장르, 음악가 및 앨범 목록으로 미리 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-144">This will pre-populate our store catalog with a list of Genres, Artists, and Albums.</span></span> <span data-ttu-id="a145c-145">이 자습서의 앞부분에서 사용 된 사이트 디자인 파일을 포함 하는 MvcMusicStore-Assets 다운로드-코드 라는 폴더에 있는이 초기값 데이터를 포함 하는 클래스 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-145">The MvcMusicStore-Assets.zip download - which included our site design files used earlier in this tutorial - has a class file with this seed data, located in a folder named Code.</span></span>

<span data-ttu-id="a145c-146">아래와 같이 코드/모델 폴더에서 SampleData.cs 파일을 찾아 프로젝트의 모델 폴더에 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-146">Within the Code / Models folder, locate the SampleData.cs file and drop it into the Models folder in our project, as shown below.</span></span>

![](mvc-music-store-part-4/_static/image4.png)

<span data-ttu-id="a145c-147">이제 해당 Sampledata.xml 클래스에 대 한 Entity Framework를 알려 주는 코드 한 줄을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-147">Now we need to add one line of code to tell Entity Framework about that SampleData class.</span></span> <span data-ttu-id="a145c-148">프로젝트의 루트에서 Global.asax 파일을 두 번 클릭 하 여 열고 응용 프로그램\_시작 메서드 맨 위에 다음 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-148">Double-click on the Global.asax file in the root of the project to open it and add the following line to the top the Application\_Start method.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample6.cs)]

<span data-ttu-id="a145c-149">이 시점에서 프로젝트에 대 한 Entity Framework를 구성 하는 데 필요한 작업을 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-149">At this point, we've completed the work necessary to configure Entity Framework for our project.</span></span>

## <a name="querying-the-database"></a><span data-ttu-id="a145c-150">데이터베이스 쿼리</span><span class="sxs-lookup"><span data-stu-id="a145c-150">Querying the Database</span></span>

<span data-ttu-id="a145c-151">이제 "더미 데이터"를 사용 하는 대신 데이터베이스를 호출 하 여 모든 정보를 쿼리 하도록 StoreController을 업데이트 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-151">Now let's update our StoreController so that instead of using "dummy data" it instead calls into our database to query all of its information.</span></span> <span data-ttu-id="a145c-152">먼저 **StoreController** 에서 필드를 선언 하 고 storedb: 라는 MusicStoreEntities 클래스의 인스턴스를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-152">We'll start by declaring a field on the **StoreController** to hold an instance of the MusicStoreEntities class, named storeDB:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample7.cs)]

### <a name="updating-the-store-index-to-query-the-database"></a><span data-ttu-id="a145c-153">데이터베이스를 쿼리 하기 위해 저장소 인덱스 업데이트</span><span class="sxs-lookup"><span data-stu-id="a145c-153">Updating the Store Index to query the database</span></span>

<span data-ttu-id="a145c-154">MusicStoreEntities 클래스는 Entity Framework에서 유지 관리 되며 데이터베이스의 각 테이블에 대 한 컬렉션 속성을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-154">The MusicStoreEntities class is maintained by the Entity Framework and exposes a collection property for each table in our database.</span></span> <span data-ttu-id="a145c-155">StoreController의 인덱스 작업을 업데이트 하 여 데이터베이스의 모든 장르를 검색 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-155">Let's update our StoreController's Index action to retrieve all Genres in our database.</span></span> <span data-ttu-id="a145c-156">이전에는 문자열 데이터를 하드 코딩 하 여이를 수행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-156">Previously we did this by hard-coding string data.</span></span> <span data-ttu-id="a145c-157">대신 Entity Framework 컨텍스트 Generes 컬렉션을 사용 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-157">Now we can instead just use the Entity Framework context Generes collection:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample8.cs)]

<span data-ttu-id="a145c-158">이전에 반환한 동일한 파일 인덱스 Viewmodel을 반환 하기 때문에 보기 템플릿에서 변경 하지 않아도 됩니다. 지금 데이터베이스에서 라이브 데이터를 반환 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-158">No changes need to happen to our View template since we're still returning the same StoreIndexViewModel we returned before - we're just returning live data from our database now.</span></span>

<span data-ttu-id="a145c-159">프로젝트를 다시 실행 하 고 "/Store" URL을 방문할 때 데이터베이스의 모든 장르 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-159">When we run the project again and visit the "/Store" URL, we'll now see a list of all Genres in our database:</span></span>

![](mvc-music-store-part-4/_static/image1.jpg)

### <a name="updating-store-browse-and-details-to-use-live-data"></a><span data-ttu-id="a145c-160">라이브 데이터를 사용 하도록 저장소 찾아보기 및 세부 정보 업데이트</span><span class="sxs-lookup"><span data-stu-id="a145c-160">Updating Store Browse and Details to use live data</span></span>

<span data-ttu-id="a145c-161">/Sv/shhhhhhs? 장르 = *[일부 장르]* 작업 메서드를 사용 하 여 이름을 기준으로 장르를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-161">With the /Store/Browse?genre=*[some-genre]* action method, we're searching for a Genre by name.</span></span> <span data-ttu-id="a145c-162">동일한 장르 이름에 대해 두 개의 항목을 포함 하는 것이 아니므로를 사용할 수 있기 때문에 결과는 한 가지 뿐입니다. 다음과 같이 적절 한 장르 개체를 쿼리 하기 위한 LINQ의 단일 () 확장 (아직 입력 하지 않음):</span><span class="sxs-lookup"><span data-stu-id="a145c-162">We only expect one result, since we shouldn't ever have two entries for the same Genre name, and so we can use the .Single() extension in LINQ to query for the appropriate Genre object like this (don't type this yet):</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample9.cs)]

<span data-ttu-id="a145c-163">단일 메서드는 람다 식을 매개 변수로 사용 하며,이는 이름이 정의한 값과 일치 하도록 단일 장르 개체를 사용 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-163">The Single method takes a Lambda expression as a parameter, which specifies that we want a single Genre object such that its name matches the value we've defined.</span></span> <span data-ttu-id="a145c-164">위의 경우 이름 값이 Disco 인 단일 장르 개체를 로드 하는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-164">In the case above, we are loading a single Genre object with a Name value matching Disco.</span></span>

<span data-ttu-id="a145c-165">장르 개체가 검색 될 때 로드 하려는 다른 관련 엔터티를 나타낼 수 있도록 하는 Entity Framework 기능을 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-165">We'll take advantage of an Entity Framework feature that allows us to indicate other related entities we want loaded as well when the Genre object is retrieved.</span></span> <span data-ttu-id="a145c-166">이 기능을 쿼리 결과 셰이핑 이라고 하며, 필요한 모든 정보를 검색 하기 위해 데이터베이스에 액세스 해야 하는 횟수를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-166">This feature is called Query Result Shaping, and enables us to reduce the number of times we need to access the database to retrieve all of the information we need.</span></span> <span data-ttu-id="a145c-167">검색 하는 장르에 대 한 앨범을 미리 인출 하려고 하므로, 관련 앨범이 있음을 나타내기 위해 장르 ("앨범")를 포함 하도록 쿼리를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-167">We want to pre-fetch the Albums for Genre we retrieve, so we'll update our query to include from Genres.Include("Albums") to indicate that we want related albums as well.</span></span> <span data-ttu-id="a145c-168">이는 단일 데이터베이스 요청에서 장르 및 앨범 데이터를 모두 검색 하기 때문에 더 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-168">This is more efficient, since it will retrieve both our Genre and Album data in a single database request.</span></span>

<span data-ttu-id="a145c-169">설명에 따르면 업데이트 된 검색 컨트롤러 작업의 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-169">With the explanations out of the way, here's how our updated Browse controller action looks:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample10.cs)]

<span data-ttu-id="a145c-170">이제 스토어 찾아보기 보기를 업데이트 하 여 각 장르에서 사용할 수 있는 앨범을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-170">We can now update the Store Browse View to display the albums which are available in each Genre.</span></span> <span data-ttu-id="a145c-171">보기 템플릿 (/Views/Store/Browse.cshtml에 있음)을 열고 아래와 같이 앨범의 글머리 기호 목록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-171">Open the view template (found in /Views/Store/Browse.cshtml) and add a bulleted list of Albums as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample11.cshtml)]

<span data-ttu-id="a145c-172">응용 프로그램을 실행 하 고/Sv/svhhhhd? 장르 = 재즈로 이동 하면 현재 데이터베이스에서 결과를 끌어온 다음 선택한 장르에 있는 모든 앨범이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-172">Running our application and browsing to /Store/Browse?genre=Jazz shows that our results are now being pulled from the database, displaying all albums in our selected Genre.</span></span>

![](mvc-music-store-part-4/_static/image2.jpg)

<span data-ttu-id="a145c-173">/Store/Details/[id] URL을 동일 하 게 변경 하 고 더미 데이터를 해당 ID가 매개 변수 값과 일치 하는 앨범을 로드 하는 데이터베이스 쿼리로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-173">We'll make the same change to our /Store/Details/[id] URL, and replace our dummy data with a database query which loads an Album whose ID matches the parameter value.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample12.cs)]

<span data-ttu-id="a145c-174">응용 프로그램을 실행 하 고/Store/Details/1를 검색 하면 결과를 데이터베이스에서 끌어올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-174">Running our application and browsing to /Store/Details/1 shows that our results are now being pulled from the database.</span></span>

![](mvc-music-store-part-4/_static/image5.png)

<span data-ttu-id="a145c-175">이제 앨범 ID로 앨범을 표시 하도록 저장소 정보 페이지를 설정 했으므로 자세히 보기에 링크 하기 위해 **찾아보기** 보기를 업데이트 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-175">Now that our Store Details page is set up to display an album by the Album ID, let's update the **Browse** view to link to the Details view.</span></span> <span data-ttu-id="a145c-176">이전 섹션의 끝 부분에서 상점 인덱스에서 저장소 검색에 연결 하는 것과 똑같이 html.actionlink를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-176">We will use Html.ActionLink, exactly as we did to link from Store Index to Store Browse at the end of the previous section.</span></span> <span data-ttu-id="a145c-177">찾아보기 보기의 전체 소스는 아래에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-177">The complete source for the Browse view appears below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample13.cshtml)]

<span data-ttu-id="a145c-178">이제 스토어 페이지에서 장르 페이지로 이동 하 여 사용 가능한 앨범을 나열 하 고 앨범을 클릭 하 여 앨범에 대 한 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a145c-178">We're now able to browse from our Store page to a Genre page, which lists the available albums, and by clicking on an album we can view details for that album.</span></span>

![](mvc-music-store-part-4/_static/image6.png)

> [!div class="step-by-step"]
> <span data-ttu-id="a145c-179">[이전](mvc-music-store-part-3.md)
> [다음](mvc-music-store-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="a145c-179">[Previous](mvc-music-store-part-3.md)
[Next](mvc-music-store-part-5.md)</span></span>
