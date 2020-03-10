---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
title: '1 부: 개요 및 파일 > 새 프로젝트 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 1 부에서는 개요와 파일 > 새 프로젝트를 다룹니다.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: bd356ca3-5bdb-4067-9dac-c9e9923a86e8
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
msc.type: authoredcontent
ms.openlocfilehash: 48428ff4ab5888253ed93ac41e79006eec823ad2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451283"
---
# <a name="part-1-overview-and-file-new-project"></a><span data-ttu-id="4cbbb-104">1 부: 개요 및 파일 > 새 프로젝트</span><span class="sxs-lookup"><span data-stu-id="4cbbb-104">Part 1: Overview and File->New Project</span></span>

<span data-ttu-id="4cbbb-105">받은 사람 ( [Jon Galloway](https://github.com/jongalloway) )</span><span class="sxs-lookup"><span data-stu-id="4cbbb-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="4cbbb-106">MVC Music Store는 웹 개발용 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 소개 하 고 설명 하는 자습서 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="4cbbb-107">MVC Music Store는 온라인으로 음악 앨범을 판매 하 고 기본적인 사이트 관리, 사용자 로그인 및 쇼핑 카트 기능을 구현 하는 간단한 샘플 저장소 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="4cbbb-108">이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="4cbbb-109">1 부에서는 개요와 파일&gt;새 프로젝트를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-109">Part 1 covers Overview and File-&gt;New Project.</span></span>

## <a name="overview"></a><span data-ttu-id="4cbbb-110">개요</span><span class="sxs-lookup"><span data-stu-id="4cbbb-110">Overview</span></span>

<span data-ttu-id="4cbbb-111">MVC Music Store는 웹 개발을 위해 ASP.NET MVC 및 Visual Web Developer를 사용 하는 방법을 단계별로 소개 하 고 설명 하는 자습서 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-111">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Web Developer for web development.</span></span> <span data-ttu-id="4cbbb-112">Microsoft는 느리게 시작 될 예정 이므로, 초급 수준의 웹 개발 환경을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-112">We'll be starting slowly, so beginner level web development experience is okay.</span></span>

<span data-ttu-id="4cbbb-113">빌드할 응용 프로그램은 간단한 음악 상점입니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-113">The application we'll be building is a simple music store.</span></span> <span data-ttu-id="4cbbb-114">응용 프로그램에는 쇼핑, 체크 아웃 및 관리의 세 가지 주요 부분이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-114">There are three main parts to the application: shopping, checkout, and administration.</span></span>

![](mvc-music-store-part-1/_static/image1.jpg)

<span data-ttu-id="4cbbb-115">방문자는 장르별로 앨범을 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-115">Visitors can browse Albums by Genre:</span></span>

![](mvc-music-store-part-1/_static/image2.jpg)

<span data-ttu-id="4cbbb-116">단일 앨범을 보고 해당 바구니에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-116">They can view a single album and add it to their cart:</span></span>

![](mvc-music-store-part-1/_static/image3.jpg)

<span data-ttu-id="4cbbb-117">해당 카트를 검토 하 여 더 이상 원하지 않는 항목을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-117">They can review their cart, removing any items they no longer want:</span></span>

![](mvc-music-store-part-1/_static/image4.jpg)

<span data-ttu-id="4cbbb-118">체크 아웃을 계속 하면 로그인 하거나 사용자 계정에 등록 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-118">Proceeding to Checkout will prompt them to login or register for a user account.</span></span>

![](mvc-music-store-part-1/_static/image1.png)

![](mvc-music-store-part-1/_static/image2.png)

<span data-ttu-id="4cbbb-119">계정을 만든 후에는 배송 및 지불 정보를 입력 하 여 주문을 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-119">After creating an account, they can complete the order by filling out shipping and payment information.</span></span> <span data-ttu-id="4cbbb-120">간단 하 게 유지 하기 위해 microsoft는 놀라운 프로 모션을 실행 하 고 있습니다. 프로 모션 코드를 "무료"로 입력 하면 모든 기능을 무료로 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-120">To keep things simple, we're running an amazing promotion: everything's free if they enter promotion code "FREE"!</span></span>

![](mvc-music-store-part-1/_static/image5.jpg)

<span data-ttu-id="4cbbb-121">주문 후에는 간단한 확인 화면이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-121">After ordering, they see a simple confirmation screen:</span></span>

![](mvc-music-store-part-1/_static/image6.jpg)

<span data-ttu-id="4cbbb-122">고객 관련 페이지 외에도 관리자가 앨범을 만들고, 편집 하 고, 삭제할 수 있는 앨범 목록을 보여 주는 관리자 섹션을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-122">In addition to customer-facing pages, we'll also build an administrator section that shows a list of albums from which Administrators can Create, Edit, and Delete albums:</span></span>

![](mvc-music-store-part-1/_static/image7.jpg)

## <a name="1-file--gt-new-project"></a><span data-ttu-id="4cbbb-123">1. 파일&gt; 새 프로젝트</span><span class="sxs-lookup"><span data-stu-id="4cbbb-123">1. File -&gt; New Project</span></span>

### <a name="installing-the-software"></a><span data-ttu-id="4cbbb-124">소프트웨어 설치</span><span class="sxs-lookup"><span data-stu-id="4cbbb-124">Installing the software</span></span>

<span data-ttu-id="4cbbb-125">이 자습서는 무료 Visual Web Developer 2010 Express (무료)를 사용 하 여 새 ASP.NET MVC 3 프로젝트를 만든 다음, 완벽 하 게 작동 하는 응용 프로그램을 만들기 위해 기능을 증분 방식으로 추가 하는 것으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-125">This tutorial will begin by creating a new ASP.NET MVC 3 project using the free Visual Web Developer 2010 Express (which is free), and then we'll incrementally add features to create a complete functioning application.</span></span> <span data-ttu-id="4cbbb-126">이 과정에서 데이터베이스 액세스, 폼 게시 시나리오, 데이터 유효성 검사, 페이지를 일관 되 게 유지 하기 위해 마스터 페이지 사용, 페이지 업데이트 및 유효성 검사, 사용자 로그인 등에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-126">Along the way, we'll cover database access, form posting scenarios, data validation, using master pages for consistent page layout, using AJAX for page updates and validation, user login, and more.</span></span>

<span data-ttu-id="4cbbb-127">단계별 지침을 따르거나 전체 응용 프로그램을 [MVC-음악 저장소](https://github.com/evilDave/MVC-Music-Store)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-127">You can follow along step by step, or you can download the completed application from [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>

<span data-ttu-id="4cbbb-128">Visual Studio 2010 SP1 또는 Visual Web Developer 2010 Express SP1 (Visual Studio 2010의 무료 버전) 중 하나를 사용 하 여 응용 프로그램을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-128">You can use either Visual Studio 2010 SP1 or Visual Web Developer 2010 Express SP1 (a free version of Visual Studio 2010) to build the application.</span></span> <span data-ttu-id="4cbbb-129">SQL Server Compact (무료)를 사용 하 여 데이터베이스를 호스팅합니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-129">We'll be using the SQL Server Compact (also free) to host the database.</span></span> <span data-ttu-id="4cbbb-130">시작 하기 전에 아래 나열 된 필수 구성 요소를 설치 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-130">Before you start, make sure you've installed the prerequisites listed below.</span></span>

- <span data-ttu-id="4cbbb-131">[Visual Studio Web Developer Express SP1 필수 구성 요소]</span><span class="sxs-lookup"><span data-stu-id="4cbbb-131">[Visual Studio Web Developer Express SP1 prerequisites]</span></span>
- <span data-ttu-id="4cbbb-132">[ASP.NET MVC 3 도구 업데이트]</span><span class="sxs-lookup"><span data-stu-id="4cbbb-132">[ASP.NET MVC 3 Tools Update]</span></span>
- <span data-ttu-id="4cbbb-133">[SQL Server Compact 4.0]-런타임 및 도구 지원을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-133">[SQL Server Compact 4.0] - including both runtime and tools support</span></span>

### <a name="creating-a-new-aspnet-mvc-3-project"></a><span data-ttu-id="4cbbb-134">새 ASP.NET MVC 3 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="4cbbb-134">Creating a new ASP.NET MVC 3 project</span></span>

<span data-ttu-id="4cbbb-135">먼저 Visual Web Developer의 파일 메뉴에서 "새 프로젝트"를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-135">We'll start by selecting "New Project" from the File menu in Visual Web Developer.</span></span> <span data-ttu-id="4cbbb-136">그러면 새 프로젝트 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-136">This brings up the New Project dialog.</span></span>

![](mvc-music-store-part-1/_static/image5.png)

<span data-ttu-id="4cbbb-137">왼쪽의 시각적 C#&gt; 웹 템플릿 그룹을 선택 하 고 가운데 열에서 "ASP.NET MVC 3 웹 응용 프로그램" 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-137">We'll select the Visual C# -&gt; Web Templates group on the left, then choose the "ASP.NET MVC 3 Web Application" template in the center column.</span></span> <span data-ttu-id="4cbbb-138">프로젝트 이름을 MvcMusicStore로 하 고 확인 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-138">Name your project MvcMusicStore and press the OK button.</span></span>

![](mvc-music-store-part-1/_static/image8.jpg)

<span data-ttu-id="4cbbb-139">그러면 프로젝트에 대 한 MVC 특정 설정을 만들 수 있는 보조 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-139">This will display a secondary dialog which allows us to make some MVC specific settings for our project.</span></span> <span data-ttu-id="4cbbb-140">다음을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-140">Select the following:</span></span>

<span data-ttu-id="4cbbb-141">프로젝트 템플릿-빈 선택</span><span class="sxs-lookup"><span data-stu-id="4cbbb-141">Project Template - select Empty</span></span>

<span data-ttu-id="4cbbb-142">뷰 엔진-Razor 선택</span><span class="sxs-lookup"><span data-stu-id="4cbbb-142">View Engine - select Razor</span></span>

<span data-ttu-id="4cbbb-143">HTML5 의미 체계 태그 사용-선택 됨</span><span class="sxs-lookup"><span data-stu-id="4cbbb-143">Use HTML5 semantic markup - checked</span></span>

<span data-ttu-id="4cbbb-144">설정이 아래에 표시 되었는지 확인 한 다음 확인 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-144">Verify that your settings are as shown below, then press the OK button.</span></span>

![](mvc-music-store-part-1/_static/image9.jpg)

<span data-ttu-id="4cbbb-145">그러면 프로젝트가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-145">This will create our project.</span></span> <span data-ttu-id="4cbbb-146">오른쪽의 솔루션 탐색기에 응용 프로그램에 추가 된 폴더를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-146">Let's take a look at the folders that have been added to our application in the Solution Explorer on the right side.</span></span>

![](mvc-music-store-part-1/_static/image10.jpg)

<span data-ttu-id="4cbbb-147">빈 MVC 3 템플릿은 완전히 비어 있지 않으며 기본 폴더 구조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-147">The Empty MVC 3 template isn't completely empty – it adds a basic folder structure:</span></span>

![](mvc-music-store-part-1/_static/image6.png)

<span data-ttu-id="4cbbb-148">ASP.NET MVC는 폴더 이름에 대해 다음과 같은 몇 가지 기본 명명 규칙을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-148">ASP.NET MVC makes use of some basic naming conventions for folder names:</span></span>

| <span data-ttu-id="4cbbb-149">**폴더**</span><span class="sxs-lookup"><span data-stu-id="4cbbb-149">**Folder**</span></span> | <span data-ttu-id="4cbbb-150">**용도**</span><span class="sxs-lookup"><span data-stu-id="4cbbb-150">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="4cbbb-151">**/컨트롤러**</span><span class="sxs-lookup"><span data-stu-id="4cbbb-151">**/Controllers**</span></span> | <span data-ttu-id="4cbbb-152">컨트롤러는 브라우저에서 입력에 응답 하 여 수행할 작업을 결정 하 고 사용자에 게 응답을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-152">Controllers respond to input from the browser, decide what to do with it, and return response to the user.</span></span> |
| <span data-ttu-id="4cbbb-153">**/Views**</span><span class="sxs-lookup"><span data-stu-id="4cbbb-153">**/Views**</span></span> | <span data-ttu-id="4cbbb-154">보기에 UI 템플릿 포함</span><span class="sxs-lookup"><span data-stu-id="4cbbb-154">Views hold our UI templates</span></span> |
| <span data-ttu-id="4cbbb-155">**/모델**</span><span class="sxs-lookup"><span data-stu-id="4cbbb-155">**/Models**</span></span> | <span data-ttu-id="4cbbb-156">모델 데이터 저장 및 조작</span><span class="sxs-lookup"><span data-stu-id="4cbbb-156">Models hold and manipulate data</span></span> |
| <span data-ttu-id="4cbbb-157">**/콘텐츠**</span><span class="sxs-lookup"><span data-stu-id="4cbbb-157">**/Content**</span></span> | <span data-ttu-id="4cbbb-158">이 폴더에는 이미지, CSS 및 기타 정적 콘텐츠가 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-158">This folder holds our images, CSS, and any other static content</span></span> |
| <span data-ttu-id="4cbbb-159">**/Scripts**</span><span class="sxs-lookup"><span data-stu-id="4cbbb-159">**/Scripts**</span></span> | <span data-ttu-id="4cbbb-160">이 폴더에는 JavaScript 파일이 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-160">This folder holds our JavaScript files</span></span> |

<span data-ttu-id="4cbbb-161">ASP.NET MVC 프레임 워크는 기본적으로 "구성에 대 한 규칙" 방식을 사용 하 고 폴더 명명 규칙에 따라 몇 가지 기본 가정을 수행 하기 때문에 이러한 폴더는 빈 ASP.NET MVC 응용 프로그램에도 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-161">These folders are included even in an Empty ASP.NET MVC application because the ASP.NET MVC framework by default uses a "convention over configuration" approach and makes some default assumptions based on folder naming conventions.</span></span> <span data-ttu-id="4cbbb-162">예를 들어, 컨트롤러는 코드에서 명시적으로이를 지정 하지 않고 Views 폴더에서 뷰를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-162">For instance, controllers look for views in the Views folder by default without you having to explicitly specify this in your code.</span></span> <span data-ttu-id="4cbbb-163">기본 규칙을 사용 하면 작성 해야 하는 코드의 양이 줄어들고 다른 개발자가 프로젝트를 보다 쉽게 이해할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-163">Sticking with the default conventions reduces the amount of code you need to write, and can also make it easier for other developers to understand your project.</span></span> <span data-ttu-id="4cbbb-164">응용 프로그램을 빌드할 때 이러한 규칙을 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cbbb-164">We'll explain these conventions more as we build our application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="4cbbb-165">다음</span><span class="sxs-lookup"><span data-stu-id="4cbbb-165">Next</span></span>](mvc-music-store-part-2.md)
