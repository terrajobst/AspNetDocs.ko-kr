---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
title: '5 부: 양식 및 템플릿 편집 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 5 부에서는 편집 양식 및 템플릿을 다룹니다.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 6b09413a-6d6a-425a-87c9-629f91b91b28
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
msc.type: authoredcontent
ms.openlocfilehash: 20b99cbe57b5dfa623205838a5929733a6c2d70d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450911"
---
# <a name="part-5-edit-forms-and-templating"></a><span data-ttu-id="fef90-104">5 부: 양식 및 템플릿 편집</span><span class="sxs-lookup"><span data-stu-id="fef90-104">Part 5: Edit Forms and Templating</span></span>

<span data-ttu-id="fef90-105">받은 사람 ( [Jon Galloway](https://github.com/jongalloway) )</span><span class="sxs-lookup"><span data-stu-id="fef90-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="fef90-106">MVC Music Store는 웹 개발용 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 소개 하 고 설명 하는 자습서 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="fef90-107">MVC Music Store는 온라인으로 음악 앨범을 판매 하 고 기본적인 사이트 관리, 사용자 로그인 및 쇼핑 카트 기능을 구현 하는 간단한 샘플 저장소 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>
> 
> <span data-ttu-id="fef90-108">이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="fef90-109">5 부에서는 편집 양식 및 템플릿을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-109">Part 5 covers Edit Forms and Templating.</span></span>

<span data-ttu-id="fef90-110">이전 장에서는 데이터베이스에서 데이터를 로드 하 고 표시 했습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-110">In the past chapter, we were loading data from our database and displaying it.</span></span> <span data-ttu-id="fef90-111">이 장에서는 데이터 편집도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-111">In this chapter, we'll also enable editing the data.</span></span>

## <a name="creating-the-storemanagercontroller"></a><span data-ttu-id="fef90-112">StoreManagerController 만들기</span><span class="sxs-lookup"><span data-stu-id="fef90-112">Creating the StoreManagerController</span></span>

<span data-ttu-id="fef90-113">먼저 **StoreManagerController**이라는 새 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-113">We'll begin by creating a new controller called **StoreManagerController**.</span></span> <span data-ttu-id="fef90-114">이 컨트롤러의 경우 ASP.NET MVC 3 도구 업데이트에서 사용할 수 있는 스 캐 폴딩 기능을 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-114">For this controller, we will be taking advantage of the Scaffolding features available in the ASP.NET MVC 3 Tools Update.</span></span> <span data-ttu-id="fef90-115">아래와 같이 컨트롤러 추가 대화 상자에 대 한 옵션을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-115">Set the options for the Add Controller dialog as shown below.</span></span>

![](mvc-music-store-part-5/_static/image1.png)

<span data-ttu-id="fef90-116">추가 단추를 클릭 하면 ASP.NET MVC 3 스 캐 폴딩 메커니즘이 적절 한 작업을 수행 하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-116">When you click the Add button, you'll see that the ASP.NET MVC 3 scaffolding mechanism does a good amount of work for you:</span></span>

- <span data-ttu-id="fef90-117">로컬 Entity Framework 변수를 사용 하 여 새 StoreManagerController를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-117">It creates the new StoreManagerController with a local Entity Framework variable</span></span>
- <span data-ttu-id="fef90-118">프로젝트의 Views 폴더에 StoreManager 폴더를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-118">It adds a StoreManager folder to the project's Views folder</span></span>
- <span data-ttu-id="fef90-119">Create. cshtml, Delete. cshtml, Details, Edit. cshtml 및 Index. cshtml 뷰를 추가 합니다 .이는 앨범 클래스에 강력한 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-119">It adds Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml, and Index.cshtml view, strongly typed to the Album class</span></span>

![](mvc-music-store-part-5/_static/image2.png)

<span data-ttu-id="fef90-120">새 StoreManager controller 클래스에는 앨범 모델 클래스로 작업 하 고 데이터베이스 액세스에 Entity Framework 컨텍스트를 사용 하는 방법을 알고 있는 CRUD (만들기, 읽기, 업데이트, 삭제) 컨트롤러 작업이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-120">The new StoreManager controller class includes CRUD (create, read, update, delete) controller actions which know how to work with the Album model class and use our Entity Framework context for database access.</span></span>

## <a name="modifying-a-scaffolded-view"></a><span data-ttu-id="fef90-121">스 캐 폴드 뷰 수정</span><span class="sxs-lookup"><span data-stu-id="fef90-121">Modifying a Scaffolded View</span></span>

<span data-ttu-id="fef90-122">이 코드는이 코드를 생성 하는 동안이 자습서 전체에서 작성 한 것 처럼 표준 ASP.NET MVC 코드 임을 기억해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-122">It's important to remember that, while this code was generated for us, it's standard ASP.NET MVC code, just like we've been writing throughout this tutorial.</span></span> <span data-ttu-id="fef90-123">이 도구는 상용구 컨트롤러 코드를 작성 하 고 강력한 형식의 뷰를 수동으로 만드는 데 소비 하는 시간을 절약 하기 위해 작성 되었습니다 .이는 생성 된 코드의 종류 이며, 되어서는 안됩니다 변경 하는 방법에 대 한 주석에서 디렉터리 경고 앞에서 볼 수 있습니다. code.</span><span class="sxs-lookup"><span data-stu-id="fef90-123">It's intended to save you the time you'd spend on writing boilerplate controller code and creating the strongly typed views manually, but this isn't the kind of generated code you may have seen prefaced with dire warnings in comments about how you mustn't change the code.</span></span> <span data-ttu-id="fef90-124">코드를 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-124">This is your code, and you're expected to change it.</span></span>

<span data-ttu-id="fef90-125">이제 StoreManager 인덱스 보기 (/Views/StoreManager/Index.cshtml)에 대 한 빠른 편집부터 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-125">So, let's start with a quick edit to the StoreManager Index view (/Views/StoreManager/Index.cshtml).</span></span> <span data-ttu-id="fef90-126">이 보기에는 편집/세부 정보/삭제 링크를 사용 하 여 스토어의 앨범을 나열 하 고 앨범의 공용 속성을 포함 하는 표가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-126">This view will display a table which lists the Albums in our store with Edit / Details / Delete links, and includes the Album's public properties.</span></span> <span data-ttu-id="fef90-127">AlbumArtUrl 필드는이 표시에서 그다지 유용 하지 않으므로 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-127">We'll remove the AlbumArtUrl field, as it's not very useful in this display.</span></span> <span data-ttu-id="fef90-128">보기 코드의 &lt;테이블&gt; 섹션에서 아래 강조 표시 된 줄에 표시 된 것 처럼 AlbumArtUrl references 주위의 &lt;번째&gt; 및 &lt;td&gt; 요소를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-128">In &lt;table&gt; section of the view code, remove the &lt;th&gt; and &lt;td&gt; elements surrounding AlbumArtUrl references, as indicated by the highlighted lines below:</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample1.cshtml)]

<span data-ttu-id="fef90-129">수정 된 뷰 코드는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-129">The modified view code will appear as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample2.cshtml)]

## <a name="a-first-look-at-the-store-manager"></a><span data-ttu-id="fef90-130">저장소 관리자에 대 한 첫 번째 보기</span><span class="sxs-lookup"><span data-stu-id="fef90-130">A first look at the Store Manager</span></span>

<span data-ttu-id="fef90-131">이제 응용 프로그램을 실행 하 고/StoreManager/.로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-131">Now run the application and browse to /StoreManager/.</span></span> <span data-ttu-id="fef90-132">그러면 방금 수정한 저장소 관리자 인덱스가 표시 되 고 편집, 세부 정보 및 삭제 링크를 포함 하는 스토어의 앨범 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-132">This displays the Store Manager Index we just modified, showing a list of the albums in the store with links to Edit, Details, and Delete.</span></span>

![](mvc-music-store-part-5/_static/image3.png)

<span data-ttu-id="fef90-133">편집 링크를 클릭 하면 장르 및 음악가 드롭다운을 비롯 하 여 앨범에 대 한 필드가 포함 된 편집 양식이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-133">Clicking the Edit link displays an edit form with fields for the Album, including dropdowns for Genre and Artist.</span></span>

![](mvc-music-store-part-5/_static/image4.png)

<span data-ttu-id="fef90-134">아래쪽의 "목록으로 돌아가기" 링크를 클릭 한 다음 앨범에 대 한 세부 정보 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-134">Click the "Back to List" link at the bottom, then click on the Details link for an Album.</span></span> <span data-ttu-id="fef90-135">그러면 개별 앨범에 대 한 세부 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-135">This displays the detail information for an individual Album.</span></span>

![](mvc-music-store-part-5/_static/image5.png)

<span data-ttu-id="fef90-136">다시 목록으로 돌아가기 링크를 클릭 한 다음 삭제 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-136">Again, click the Back to List link, then click on a Delete link.</span></span> <span data-ttu-id="fef90-137">그러면 앨범 세부 정보를 표시 하 고 삭제 여부를 묻는 확인 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-137">This displays a confirmation dialog, showing the album details and asking if we're sure we want to delete it.</span></span>

![](mvc-music-store-part-5/_static/image6.png)

<span data-ttu-id="fef90-138">맨 아래에 있는 삭제 단추를 클릭 하면 앨범이 삭제 되 고 삭제 된 앨범이 표시 되는 인덱스 페이지로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-138">Clicking the Delete button at the bottom will delete the album and return you to the Index page, which shows the album deleted.</span></span>

<span data-ttu-id="fef90-139">저장소 관리자를 사용 하 여 작업을 수행 하는 것은 아니지만, CRUD 작업을 시작 하는 데 사용할 수 있는 컨트롤러와 코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-139">We're not done with the Store Manager, but we have working controller and view code for the CRUD operations to start from.</span></span>

## <a name="looking-at-the-store-manager-controller-code"></a><span data-ttu-id="fef90-140">Store Manager 컨트롤러 코드 보기</span><span class="sxs-lookup"><span data-stu-id="fef90-140">Looking at the Store Manager Controller code</span></span>

<span data-ttu-id="fef90-141">저장소 관리자 컨트롤러에는 적절 한 양의 코드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-141">The Store Manager Controller contains a good amount of code.</span></span> <span data-ttu-id="fef90-142">위에서 아래로 이동 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-142">Let's go through this from top to bottom.</span></span> <span data-ttu-id="fef90-143">컨트롤러에는 MVC 컨트롤러에 대 한 몇 가지 표준 네임 스페이스와 모델 네임 스페이스에 대 한 참조가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-143">The controller includes some standard namespaces for an MVC controller, as well as a reference to our Models namespace.</span></span> <span data-ttu-id="fef90-144">컨트롤러에는 데이터 액세스에 대 한 각 컨트롤러 작업에서 사용 되는 MusicStoreEntities의 전용 인스턴스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-144">The controller has a private instance of MusicStoreEntities, used by each of the controller actions for data access.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample3.cs)]

### <a name="store-manager-index-and-details-actions"></a><span data-ttu-id="fef90-145">저장소 관리자 인덱스 및 세부 정보 작업</span><span class="sxs-lookup"><span data-stu-id="fef90-145">Store Manager Index and Details actions</span></span>

<span data-ttu-id="fef90-146">인덱스 뷰는 저장소 찾아보기 방법으로 작업할 때 이전에 확인 한 각 앨범의 참조 된 장르 및 음악가 정보를 포함 하 여 앨범 목록을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-146">The index view retrieves a list of Albums, including each album's referenced Genre and Artist information, as we previously saw when working on the Store Browse method.</span></span> <span data-ttu-id="fef90-147">인덱스 뷰는 연결 된 개체에 대 한 참조를 따라 각 앨범의 장르 이름과 음악가 이름을 표시 하 여 컨트롤러를 효율적으로 만들고 원래 요청에서이 정보를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-147">The Index view is following the references to the linked objects so that it can display each album's Genre name and Artist name, so the controller is being efficient and querying for this information in the original request.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample4.cs)]

<span data-ttu-id="fef90-148">StoreManager 컨트롤러의 세부 정보 컨트롤러 작업은 이전에 만든 저장소 컨트롤러 세부 정보 작업과 동일 하 게 작동 합니다. 여기서는 Find () 메서드를 사용 하 여 ID로 앨범을 쿼리 한 다음이를 뷰로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-148">The StoreManager Controller's Details controller action works exactly the same as the Store Controller Details action we wrote previously - it queries for the Album by ID using the Find() method, then returns it to the view.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample5.cs)]

### <a name="the-create-action-methods"></a><span data-ttu-id="fef90-149">작업 메서드 만들기</span><span class="sxs-lookup"><span data-stu-id="fef90-149">The Create Action Methods</span></span>

<span data-ttu-id="fef90-150">만들기 작업 메서드는 폼 입력을 처리 하기 때문에 지금까지 살펴본 것과 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-150">The Create action methods are a little different from ones we've seen so far, because they handle form input.</span></span> <span data-ttu-id="fef90-151">사용자가/StoreManager/Create/를 처음 방문 하면 빈 양식이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-151">When a user first visits /StoreManager/Create/ they will be shown an empty form.</span></span> <span data-ttu-id="fef90-152">이 HTML 페이지에는 사용자가 앨범 세부 정보를 입력할 수 있는 드롭다운 및 텍스트 상자 입력 요소를 포함 하는 &lt;form&gt; 요소가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-152">This HTML page will contain a &lt;form&gt; element that contains dropdown and textbox input elements where they can enter the album's details.</span></span>

<span data-ttu-id="fef90-153">사용자가 앨범 양식 값을 채운 후 "저장" 단추를 눌러 이러한 변경 내용을 응용 프로그램에 다시 제출 하 여 데이터베이스 내에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-153">After the user fills in the Album form values, they can press the "Save" button to submit these changes back to our application to save within the database.</span></span> <span data-ttu-id="fef90-154">사용자가 "저장" 단추를 누르면 &lt;양식&gt;에서 HTTP post를 다시 실행 하 여/StoreManager/Create/URL에 다시 게시 하 고 &lt;형식&gt; 값을 HTTP POST의 일부로 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-154">When the user presses the "save" button the &lt;form&gt; will perform an HTTP-POST back to the /StoreManager/Create/ URL and submit the &lt;form&gt; values as part of the HTTP-POST.</span></span>

<span data-ttu-id="fef90-155">ASP.NET MVC를 사용 하면 StoreManagerController 클래스 내에서 두 개의 별도 "Create" 작업 메서드를 구현 하 여 (/StoreManager/Create/URL에 대 한 초기 HTTP-GET 찾아보기를 처리 하는 경우), 전송 된 변경 내용에 대 한 HTTP POST를 처리 하는 두 가지 URL 호출 시나리오의 논리를 쉽게 분할할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-155">ASP.NET MVC allows us to easily split up the logic of these two URL invocation scenarios by enabling us to implement two separate "Create" action methods within our StoreManagerController class – one to handle the initial HTTP-GET browse to the /StoreManager/Create/ URL, and the other to handle the HTTP-POST of the submitted changes.</span></span>

### <a name="passing-information-to-a-view-using-viewbag"></a><span data-ttu-id="fef90-156">ViewBag를 사용 하 여 뷰에 정보 전달</span><span class="sxs-lookup"><span data-stu-id="fef90-156">Passing information to a View using ViewBag</span></span>

<span data-ttu-id="fef90-157">이 자습서의 앞부분에서 ViewBag를 사용 했지만 많은 이야기를 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-157">We've used the ViewBag earlier in this tutorial, but haven't talked much about it.</span></span> <span data-ttu-id="fef90-158">ViewBag 강력한 형식의 모델 개체를 사용 하지 않고 뷰에 정보를 전달할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-158">The ViewBag allows us to pass information to the view without using a strongly typed model object.</span></span> <span data-ttu-id="fef90-159">이 경우 편집 HTTP-컨트롤러 가져오기 작업은 드롭다운을 채우기 위해 장르 및 음악가 목록을 폼에 전달 해야 하며,이 작업을 수행 하는 가장 간단한 방법은 ViewBag 항목으로 반환 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-159">In this case, our Edit HTTP-GET controller action needs to pass both a list of Genres and Artists to the form to populate the dropdowns, and the simplest way to do that is to return them as ViewBag items.</span></span>

<span data-ttu-id="fef90-160">ViewBag는 동적 개체입니다. 즉, 이러한 속성을 정의 하는 코드를 작성 하지 않고도 여기에 ViewBag 또는 ViewBag을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-160">The ViewBag is a dynamic object, meaning that you can type ViewBag.Foo or ViewBag.YourNameHere without writing code to define those properties.</span></span> <span data-ttu-id="fef90-161">이 경우 컨트롤러 코드는 GenreId 및 Viewbag를 사용 하 여 폼으로 전송 된 드롭다운 값이 GenreId 및 ArtistId (설정 되는 앨범 속성)가 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-161">In this case, the controller code uses ViewBag.GenreId and ViewBag.ArtistId so that the dropdown values submitted with the form will be GenreId and ArtistId, which are the Album properties they will be setting.</span></span>

<span data-ttu-id="fef90-162">이러한 드롭다운 값은 해당 목적 으로만 빌드되는 SelectList 개체를 사용 하 여 폼으로 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-162">These dropdown values are returned to the form using the SelectList object, which is built just for that purpose.</span></span> <span data-ttu-id="fef90-163">다음과 같은 코드를 사용 하 여이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-163">This is done using code like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample6.cs)]

<span data-ttu-id="fef90-164">작업 메서드 코드에서 볼 수 있듯이 다음 세 개의 매개 변수를 사용 하 여이 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-164">As you can see from the action method code, three parameters are being used to create this object:</span></span>

- <span data-ttu-id="fef90-165">드롭다운이 표시 되는 항목 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-165">The list of items the dropdown will be displaying.</span></span> <span data-ttu-id="fef90-166">이것은 단지 단지 문자열만이 아니라 장르 목록을 전달 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-166">Note that this isn't just a string - we're passing a list of Genres.</span></span>
- <span data-ttu-id="fef90-167">SelectList에 전달 되는 다음 매개 변수는 선택 된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-167">The next parameter being passed to the SelectList is the Selected Value.</span></span> <span data-ttu-id="fef90-168">이 방법으로 목록에서 항목을 미리 선택 하는 방법을 선택 하는 방법을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-168">This how the SelectList knows how to pre-select an item in the list.</span></span> <span data-ttu-id="fef90-169">편집 양식을 살펴보면 매우 유사 하 게 이해 하는 것이 더 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-169">This will be easier to understand when we look at the Edit form, which is pretty similar.</span></span>
- <span data-ttu-id="fef90-170">마지막 매개 변수는 표시 되는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-170">The final parameter is the property to be displayed.</span></span> <span data-ttu-id="fef90-171">이 경우 Genre.Name 속성은 사용자에 게 표시 되는 속성 임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-171">In this case, this is indicating that the Genre.Name property is what will be shown to the user.</span></span>

<span data-ttu-id="fef90-172">이 점을 염두에 두면 HTTP-GET 만들기 작업은 매우 간단 합니다. 두 개의 SelectLists가 ViewBag에 추가 되 고 모델 개체가 폼에 전달 되지 않습니다 (아직 생성 되지 않았기 때문).</span><span class="sxs-lookup"><span data-stu-id="fef90-172">With that in mind, then, the HTTP-GET Create action is pretty simple - two SelectLists are added to the ViewBag, and no model object is passed to the form (since it hasn't been created yet).</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample7.cs)]

### <a name="html-helpers-to-display-the-drop-downs-in-the-create-view"></a><span data-ttu-id="fef90-173">만들기 뷰에서 드롭다운을 표시 하는 HTML 도우미</span><span class="sxs-lookup"><span data-stu-id="fef90-173">HTML Helpers to display the Drop Downs in the Create View</span></span>

<span data-ttu-id="fef90-174">드롭다운 값을 보기에 전달 하는 방법에 대해 알아보았습니다. 뷰를 빠르게 확인 하 여 해당 값이 표시 되는 방식을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-174">Since we've talked about how the drop down values are passed to the view, let's take a quick look at the view to see how those values are displayed.</span></span> <span data-ttu-id="fef90-175">코드 보기 (/Views/StoreManager/Create.cshtml)에서 다음 호출이 장르 드롭다운을 표시 하도록 설정 된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-175">In the view code (/Views/StoreManager/Create.cshtml), you'll see the following call is made to display the Genre drop down.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample8.cshtml)]

<span data-ttu-id="fef90-176">이를 HTML 도우미 라고 하며이는 일반적인 뷰 작업을 수행 하는 유틸리티 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-176">This is known as an HTML Helper - a utility method which performs a common view task.</span></span> <span data-ttu-id="fef90-177">HTML 도우미는 보기 코드를 간결 하 고 읽기 쉽게 유지 하는 데 매우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-177">HTML Helpers are very useful in keeping our view code concise and readable.</span></span> <span data-ttu-id="fef90-178">ASP.NET MVC는 Html DropDownList 도우미를 제공 하지만 나중에 볼 수 있듯이 응용 프로그램에서 다시 사용할 수 있는 보기 코드에 대 한 자체 도우미를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-178">The Html.DropDownList helper is provided by ASP.NET MVC, but as we'll see later it's possible to create our own helpers for view code we'll reuse in our application.</span></span>

<span data-ttu-id="fef90-179">Html DropDownList 호출은 표시할 목록을 가져올 위치와 미리 선택 해야 하는 값 (있는 경우)을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-179">The Html.DropDownList call just needs to be told two things - where to get the list to display, and what value (if any) should be pre-selected.</span></span> <span data-ttu-id="fef90-180">첫 번째 매개 변수인 GenreId은 모델 또는 ViewBag에서 GenreId 라는 값을 검색 하도록 DropDownList에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-180">The first parameter, GenreId, tells the DropDownList to look for a value named GenreId in either the model or ViewBag.</span></span> <span data-ttu-id="fef90-181">두 번째 매개 변수는 드롭다운 목록에서 처음에 선택 된 대로 표시할 값을 나타내는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-181">The second parameter is used to indicate the value to show as initially selected in the drop down list.</span></span> <span data-ttu-id="fef90-182">이 폼은 만들기 양식 이므로 미리 선택 하 고 문자열을 비워 둘 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-182">Since this form is a Create form, there's no value to be preselected and String.Empty is passed.</span></span>

### <a name="handling-the-posted-form-values"></a><span data-ttu-id="fef90-183">게시 된 폼 값 처리</span><span class="sxs-lookup"><span data-stu-id="fef90-183">Handling the Posted Form values</span></span>

<span data-ttu-id="fef90-184">앞서 설명한 것 처럼 각 폼과 연결 된 두 가지 작업 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-184">As we discussed before, there are two action methods associated with each form.</span></span> <span data-ttu-id="fef90-185">첫 번째는 HTTP GET 요청을 처리 하 고 폼을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-185">The first handles the HTTP-GET request and displays the form.</span></span> <span data-ttu-id="fef90-186">두 번째는 전송 된 폼 값을 포함 하는 HTTP POST 요청을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-186">The second handles the HTTP-POST request, which contains the submitted form values.</span></span> <span data-ttu-id="fef90-187">컨트롤러 작업에는 HTTP POST 요청에만 응답 해야 한다는 사실을 ASP.NET MVC에 알리는 [HttpPost] 특성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-187">Notice that controller action has an [HttpPost] attribute, which tells ASP.NET MVC that it should only respond to HTTP-POST requests.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample9.cs)]

<span data-ttu-id="fef90-188">이 작업에는 네 가지 책임이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-188">This action has four responsibilities:</span></span>

- 1. <span data-ttu-id="fef90-189">양식 값 읽기</span><span class="sxs-lookup"><span data-stu-id="fef90-189">Read the form values</span></span>
- 2. <span data-ttu-id="fef90-190">양식 값이 모든 유효성 검사 규칙을 통과 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-190">Check if the form values pass any validation rules</span></span>
- 3. <span data-ttu-id="fef90-191">양식 제출이 유효한 경우 데이터를 저장 하 고 업데이트 된 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-191">If the form submission is valid, save the data and display the updated list</span></span>
- 4. <span data-ttu-id="fef90-192">양식 제출이 유효 하지 않은 경우 유효성 검사 오류로 폼을 다시 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-192">If the form submission is not valid, redisplay the form with validation errors</span></span>

#### <a name="reading-form-values-with-model-binding"></a><span data-ttu-id="fef90-193">모델 바인딩을 사용 하 여 폼 값 읽기</span><span class="sxs-lookup"><span data-stu-id="fef90-193">Reading Form Values with Model Binding</span></span>

<span data-ttu-id="fef90-194">컨트롤러 작업은 GenreId 및 ArtistId에 대 한 값을 포함 하는 양식 전송 (드롭다운 목록에서) 및 제목, 가격 및 AlbumArtUrl의 텍스트 상자 값을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-194">The controller action is processing a form submission that includes values for GenreId and ArtistId (from the drop down list) and textbox values for Title, Price, and AlbumArtUrl.</span></span> <span data-ttu-id="fef90-195">폼 값에 직접 액세스 하는 것이 가능 하지만 ASP.NET MVC에 기본 제공 되는 모델 바인딩 기능을 사용 하는 것이 더 나은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-195">While it's possible to directly access form values, a better approach is to use the Model Binding capabilities built into ASP.NET MVC.</span></span> <span data-ttu-id="fef90-196">컨트롤러 작업에서 모델 형식을 매개 변수로 사용 하는 경우 ASP.NET MVC는 경로 및 querystring 값 뿐만 아니라 양식 입력을 사용 하 여 해당 형식의 개체를 채우려고 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-196">When a controller action takes a model type as a parameter, ASP.NET MVC will attempt to populate an object of that type using form inputs (as well as route and querystring values).</span></span> <span data-ttu-id="fef90-197">이를 위해 이름이 model 개체의 속성과 일치 하는 값을 검색 합니다. 예를 들어 새 앨범 개체의 GenreId 값을 설정 하는 경우 이름이 GenreId 인 입력을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-197">It does this by looking for values whose names match properties of the model object, e.g. when setting the new Album object's GenreId value, it looks for an input with the name GenreId.</span></span> <span data-ttu-id="fef90-198">ASP.NET MVC의 표준 메서드를 사용 하 여 뷰를 만들 때 폼은 항상 속성 이름을 입력 필드 이름으로 사용 하 여 렌더링 되므로 필드 이름이 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-198">When you create views using the standard methods in ASP.NET MVC, the forms will always be rendered using property names as input field names, so this the field names will just match up.</span></span>

#### <a name="validating-the-model"></a><span data-ttu-id="fef90-199">모델 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="fef90-199">Validating the Model</span></span>

<span data-ttu-id="fef90-200">모델의 유효성을 검사 하려면 모델의 유효성을 검사 합니다. IsValid.</span><span class="sxs-lookup"><span data-stu-id="fef90-200">The model is validated with a simple call to ModelState.IsValid.</span></span> <span data-ttu-id="fef90-201">아직 모든 유효성 검사 규칙을 앨범 클래스에 추가 하지 않았습니다. 지금은 약간의 작업을 수행 합니다. 이제이 검사가 그다지 많지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-201">We haven't added any validation rules to our Album class yet - we'll do that in a bit - so right now this check doesn't have much to do.</span></span> <span data-ttu-id="fef90-202">중요 한 점은이 ModelStat 검사가 모델에 적용 되는 유효성 검사 규칙에 맞게 조정 되기 때문에 유효성 검사 규칙을 나중에 변경 하려면 컨트롤러 작업 코드를 업데이트할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-202">What's important is that this ModelStat.IsValid check will adapt to the validation rules we put on our model, so future changes to validation rules won't require any updates to the controller action code.</span></span>

#### <a name="saving-the-submitted-values"></a><span data-ttu-id="fef90-203">전송 된 값 저장</span><span class="sxs-lookup"><span data-stu-id="fef90-203">Saving the submitted values</span></span>

<span data-ttu-id="fef90-204">양식 전송에서 유효성 검사를 통과 하는 경우에는 값을 데이터베이스에 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-204">If the form submission passes validation, it's time to save the values to the database.</span></span> <span data-ttu-id="fef90-205">Entity Framework를 사용 하는 경우에는 모델을 앨범 컬렉션에 추가 하 고 SaveChanges를 호출 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-205">With Entity Framework, that just requires adding the model to the Albums collection and calling SaveChanges.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample10.cs)]

<span data-ttu-id="fef90-206">Entity Framework은 적절 한 SQL 명령을 생성 하 여 값을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-206">Entity Framework generates the appropriate SQL commands to persist the value.</span></span> <span data-ttu-id="fef90-207">데이터를 저장 한 후에는 업데이트를 볼 수 있도록 앨범 목록으로 다시 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-207">After saving the data, we redirect back to the list of Albums so we can see our update.</span></span> <span data-ttu-id="fef90-208">이 작업은 표시 하려는 컨트롤러 작업의 이름으로 RedirectToAction을 반환 하 여 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-208">This is done by returning RedirectToAction with the name of the controller action we want displayed.</span></span> <span data-ttu-id="fef90-209">이 경우 인덱스 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-209">In this case, that's the Index method.</span></span>

#### <a name="displaying-invalid-form-submissions-with-validation-errors"></a><span data-ttu-id="fef90-210">유효성 검사 오류가 있는 잘못 된 양식 전송 표시</span><span class="sxs-lookup"><span data-stu-id="fef90-210">Displaying invalid form submissions with Validation Errors</span></span>

<span data-ttu-id="fef90-211">잘못 된 폼 입력의 경우 드롭다운 값이 ViewBag에 추가 되 고 (HTTP GET 사례에서와 같이) 바인딩된 모델 값이 표시를 위해 뷰로 다시 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-211">In the case of invalid form input, the dropdown values are added to the ViewBag (as in the HTTP-GET case) and the bound model values are passed back to the view for display.</span></span> <span data-ttu-id="fef90-212">유효성 검사 오류는 @Html.ValidationMessageFor HTML 도우미를 사용 하 여 자동으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-212">Validation errors are automatically displayed using the @Html.ValidationMessageFor HTML Helper.</span></span>

#### <a name="testing-the-create-form"></a><span data-ttu-id="fef90-213">만들기 폼 테스트</span><span class="sxs-lookup"><span data-stu-id="fef90-213">Testing the Create Form</span></span>

<span data-ttu-id="fef90-214">이를 테스트 하려면 응용 프로그램을 실행 하 고/StoreManager/Create/로 이동 합니다. 그러면 StoreController Create HTTP-GET 메서드에서 반환 된 빈 양식이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-214">To test this out, run the application and browse to /StoreManager/Create/ - this will show you the blank form which was returned by the StoreController Create HTTP-GET method.</span></span>

<span data-ttu-id="fef90-215">일부 값을 입력 하 고 만들기 단추를 클릭 하 여 양식을 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-215">Fill in some values and click the Create button to submit the form.</span></span>

![](mvc-music-store-part-5/_static/image7.png)

![](mvc-music-store-part-5/_static/image8.png)

### <a name="handling-edits"></a><span data-ttu-id="fef90-216">편집 내용 처리</span><span class="sxs-lookup"><span data-stu-id="fef90-216">Handling Edits</span></span>

<span data-ttu-id="fef90-217">편집 작업 쌍 (HTTP-GET 및 HTTP POST)은 방금 살펴본 만들기 작업 메서드와 매우 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-217">The Edit action pair (HTTP-GET and HTTP-POST) are very similar to the Create action methods we just looked at.</span></span> <span data-ttu-id="fef90-218">편집 시나리오에서는 기존 앨범으로 작업 하는 작업이 포함 되므로 Edit HTTP-GET 메서드는 경로를 통해 전달 되는 "id" 매개 변수를 기반으로 하 여 앨범을 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-218">Since the edit scenario involves working with an existing album, the Edit HTTP-GET method loads the Album based on the "id" parameter, passed in via the route.</span></span> <span data-ttu-id="fef90-219">AlbumId에서 앨범을 검색 하는이 코드는 이전에 자세히 컨트롤러 작업에서 살펴본 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-219">This code for retrieving an album by AlbumId is the same as we've previously looked at in the Details controller action.</span></span> <span data-ttu-id="fef90-220">Create/HTTP GET 메서드와 마찬가지로 드롭다운 값이 ViewBag를 통해 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-220">As with the Create / HTTP-GET method, the drop down values are returned via the ViewBag.</span></span> <span data-ttu-id="fef90-221">그러면 ViewBag를 통해 추가 데이터 (예: 장르 목록)를 전달 하는 동안 모델 개체로 앨범을 모델 개체로 반환 하 여 앨범 클래스에 강력한 형식으로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-221">This allows us to return an Album as our model object to the view (which is strongly typed to the Album class) while passing additional data (e.g. a list of Genres) via the ViewBag.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample11.cs)]

<span data-ttu-id="fef90-222">HTTP-사후 편집 작업은 HTTP-사후 작업 만들기와 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-222">The Edit HTTP-POST action is very similar to the Create HTTP-POST action.</span></span> <span data-ttu-id="fef90-223">유일한 차이점은 db에 새 앨범을 추가 하는 대신입니다. 앨범 컬렉션은 db를 사용 하 여 앨범의 현재 인스턴스를 찾는 중입니다. 항목 (앨범)을 입력 하 고 해당 상태를 수정 됨으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-223">The only difference is that instead of adding a new album to the db.Albums collection, we're finding the current instance of the Album using db.Entry(album) and setting its state to Modified.</span></span> <span data-ttu-id="fef90-224">이렇게 하면 새 앨범을 만드는 것과는 달리 기존 앨범을 수정 하는 Entity Framework에 게 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-224">This tells Entity Framework that we are modifying an existing album as opposed to creating a new one.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample12.cs)]

<span data-ttu-id="fef90-225">응용 프로그램을 실행 하 고/StoreManger/로 이동한 다음 앨범의 편집 링크를 클릭 하 여이를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-225">We can test this out by running the application and browsing to /StoreManger/, then clicking the Edit link for an album.</span></span>

![](mvc-music-store-part-5/_static/image9.png)

<span data-ttu-id="fef90-226">그러면 편집 HTTP-GET 메서드에 표시 되는 편집 양식이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-226">This displays the Edit form shown by the Edit HTTP-GET method.</span></span> <span data-ttu-id="fef90-227">일부 값을 입력 하 고 저장 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-227">Fill in some values and click the Save button.</span></span>

![](mvc-music-store-part-5/_static/image10.png)

<span data-ttu-id="fef90-228">그러면 양식이 게시 되 고, 값이 저장 되며, 값이 업데이트 되었음을 보여 주는 앨범 목록으로 돌아옵니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-228">This posts the form, saves the values, and returns us to the Album list, showing that the values were updated.</span></span>

![](mvc-music-store-part-5/_static/image11.png)

### <a name="handling-deletion"></a><span data-ttu-id="fef90-229">삭제 처리</span><span class="sxs-lookup"><span data-stu-id="fef90-229">Handling Deletion</span></span>

<span data-ttu-id="fef90-230">삭제는 편집 및 만들기와 동일한 패턴을 따르며, 한 컨트롤러 작업을 사용 하 여 확인 양식을 표시 하 고, 다른 컨트롤러 작업을 사용 하 여 양식 전송을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-230">Deletion follows the same pattern as Edit and Create, using one controller action to display the confirmation form, and another controller action to handle the form submission.</span></span>

<span data-ttu-id="fef90-231">HTTP-삭제 컨트롤러 가져오기 작업은 이전 저장소 관리자 정보 컨트롤러 작업과 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-231">The HTTP-GET Delete controller action is exactly the same as our previous Store Manager Details controller action.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample13.cs)]

<span data-ttu-id="fef90-232">보기 콘텐츠 삭제 템플릿을 사용 하 여 앨범 형식에 강력한 형식의 양식을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-232">We display a form that's strongly typed to an Album type, using the Delete view content template.</span></span>

![](mvc-music-store-part-5/_static/image12.png)

<span data-ttu-id="fef90-233">Delete 템플릿은 모델에 대 한 모든 필드를 표시 하지만이를 상당히 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-233">The Delete template shows all the fields for the model, but we can simplify that down quite a bit.</span></span> <span data-ttu-id="fef90-234">/Views/StoreManager/Delete.cshtml의 보기 코드를 다음과 같이 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-234">Change the view code in /Views/StoreManager/Delete.cshtml to the following.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample14.cshtml)]

<span data-ttu-id="fef90-235">이렇게 하면 간단한 삭제 확인이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-235">This displays a simplified Delete confirmation.</span></span>

![](mvc-music-store-part-5/_static/image13.png)

<span data-ttu-id="fef90-236">삭제 단추를 클릭 하면 양식이 서버에 다시 게시 되어 DeleteConfirmed 작업이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-236">Clicking the Delete button causes the form to be posted back to the server, which executes the DeleteConfirmed action.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample15.cs)]

<span data-ttu-id="fef90-237">HTTP-사후 삭제 컨트롤러 작업은 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-237">Our HTTP-POST Delete Controller Action takes the following actions:</span></span>

- 1. <span data-ttu-id="fef90-238">ID 별로 앨범을 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-238">Loads the Album by ID</span></span>
- 2. <span data-ttu-id="fef90-239">앨범을 삭제 하 고 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-239">Deletes it the album and save changes</span></span>
- 3. <span data-ttu-id="fef90-240">목록에서 앨범이 제거 되었음을 보여 주는 인덱스로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-240">Redirects to the Index, showing that the Album was removed from the list</span></span>

<span data-ttu-id="fef90-241">이를 테스트 하려면 응용 프로그램을 실행 하 고/StoreManager.로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-241">To test this, run the application and browse to /StoreManager.</span></span> <span data-ttu-id="fef90-242">목록에서 앨범을 선택 하 고 삭제 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-242">Select an album from the list and click the Delete link.</span></span>

![](mvc-music-store-part-5/_static/image14.png)

<span data-ttu-id="fef90-243">그러면 삭제 확인 화면이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-243">This displays our Delete confirmation screen.</span></span>

![](mvc-music-store-part-5/_static/image15.png)

<span data-ttu-id="fef90-244">삭제 단추를 클릭 하면 앨범이 제거 되 고 저장 관리자 인덱스 페이지로 반환 됩니다. 그러면 앨범이 삭제 된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-244">Clicking the Delete button removes the album and returns us to the Store Manager Index page, which shows that the album has been deleted.</span></span>

![](mvc-music-store-part-5/_static/image16.png)

### <a name="using-a-custom-html-helper-to-truncate-text"></a><span data-ttu-id="fef90-245">사용자 지정 HTML 도우미를 사용 하 여 텍스트 자르기</span><span class="sxs-lookup"><span data-stu-id="fef90-245">Using a custom HTML Helper to truncate text</span></span>

<span data-ttu-id="fef90-246">Store Manager 인덱스 페이지에는 잠재적인 문제가 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-246">We've got one potential issue with our Store Manager Index page.</span></span> <span data-ttu-id="fef90-247">앨범 제목 및 음악가 이름 속성은 모두 테이블 서식 지정을 해제할 수 있을 정도로 길어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-247">Our Album Title and Artist Name properties can both be long enough that they could throw off our table formatting.</span></span> <span data-ttu-id="fef90-248">보기에서 이러한 속성과 다른 속성을 쉽게 잘라낼 수 있도록 사용자 지정 HTML 도우미를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-248">We'll create a custom HTML Helper to allow us to easily truncate these and other properties in our Views.</span></span>

![](mvc-music-store-part-5/_static/image17.png)

<span data-ttu-id="fef90-249">Razor의 @helper 구문을 사용 하면 보기에 사용할 자체 도우미 함수를 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-249">Razor's @helper syntax has made it pretty easy to create your own helper functions for use in your views.</span></span> <span data-ttu-id="fef90-250">/Views/StoreManager/Index.cshtml view를 열고 @model 줄 바로 뒤에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-250">Open the /Views/StoreManager/Index.cshtml view and add the following code directly after the @model line.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample16.cshtml)]

<span data-ttu-id="fef90-251">이 도우미 메서드는 허용 되는 문자열 및 최대 길이를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-251">This helper method takes a string and a maximum length to allow.</span></span> <span data-ttu-id="fef90-252">제공 된 텍스트가 지정 된 길이 보다 짧으면 도우미는이를 있는 그대로 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-252">If the text supplied is shorter than the length specified, the helper outputs it as-is.</span></span> <span data-ttu-id="fef90-253">더 긴 경우 텍스트를 자르고 "..."를 렌더링 합니다. 나머지입니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-253">If it is longer, then it truncates the text and renders "…" for the remainder.</span></span>

<span data-ttu-id="fef90-254">이제 자르기 도우미를 사용 하 여 앨범 제목과 음악가 이름 속성이 모두 25 자 미만인 지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-254">Now we can use our Truncate helper to ensure that both the Album Title and Artist Name properties are less than 25 characters.</span></span> <span data-ttu-id="fef90-255">새 자르기 도우미를 사용 하는 전체 뷰 코드는 아래에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-255">The complete view code using our new Truncate helper appears below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample17.cshtml)]

<span data-ttu-id="fef90-256">이제/StoreManager/URL을 찾아볼 때 앨범 및 제목은 최대 길이 미만으로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-256">Now when we browse the /StoreManager/ URL, the albums and titles are kept below our maximum lengths.</span></span>

![](mvc-music-store-part-5/_static/image18.png)

<span data-ttu-id="fef90-257">참고: 단일 뷰에서 도우미를 만들고 사용 하는 간단한 사례를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fef90-257">Note: This shows the simple case of creating and using a helper in one view.</span></span> <span data-ttu-id="fef90-258">사이트 전체에서 사용할 수 있는 도우미를 만드는 방법에 대 한 자세한 내용은 블로그 게시물: [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)</span><span class="sxs-lookup"><span data-stu-id="fef90-258">To learn more about creating helpers that you can use throughout your site, see my blog post: [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="fef90-259">[이전](mvc-music-store-part-4.md)
> [다음](mvc-music-store-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="fef90-259">[Previous](mvc-music-store-part-4.md)
[Next](mvc-music-store-part-6.md)</span></span>
