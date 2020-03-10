---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
title: ASP.NET MVC 4 도우미, 폼 및 유효성 검사 | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4 모델 및 데이터 액세스 실습 랩에서는 데이터베이스의 데이터를 로드 하 고 표시 합니다. 이 실습 랩에서는 다음에를 추가 합니다.
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 187ee9cd-bc70-479b-bfed-f568b8da96eb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
msc.type: authoredcontent
ms.openlocfilehash: 0e2605a4188eaf814f6ab0ebfeaabed4457bcfa3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433793"
---
# <a name="aspnet-mvc-4-helpers-forms-and-validation"></a><span data-ttu-id="abaf8-104">ASP.NET MVC 4 도우미, 폼 및 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="abaf8-104">ASP.NET MVC 4 Helpers, Forms and Validation</span></span>

<span data-ttu-id="abaf8-105">[웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="abaf8-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="abaf8-106">웹 캠프 교육 키트 다운로드</span><span class="sxs-lookup"><span data-stu-id="abaf8-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="abaf8-107">**ASP.NET MVC 4 모델 및 데이터 액세스** 실습 랩에서는 데이터베이스의 데이터를 로드 하 고 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-107">In **ASP.NET MVC 4 Models and Data Access** Hands-on Lab, you have been loading and displaying data from the database.</span></span> <span data-ttu-id="abaf8-108">이 실습 랩에서는 **음악 스토어** 응용 프로그램에 해당 데이터를 편집 하는 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-108">In this Hands-on Lab, you will add to the **Music Store** application the ability to edit that data.</span></span>

<span data-ttu-id="abaf8-109">이러한 목표를 염두에 두면 먼저 앨범의 만들기, 읽기, 업데이트 및 삭제 (CRUD) 작업을 지 원하는 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-109">With that goal in mind, you will first create the controller that will support the Create, Read, Update and Delete (CRUD) actions of albums.</span></span> <span data-ttu-id="abaf8-110">ASP.NET MVC의 스 캐 폴딩 기능을 활용 하 여 HTML 테이블에 앨범 속성을 표시 하는 인덱스 뷰 템플릿을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-110">You will generate an Index View template taking advantage of ASP.NET MVC's scaffolding feature to display the albums' properties in an HTML table.</span></span> <span data-ttu-id="abaf8-111">이 보기를 향상 시키려면 긴 설명을 잘라내는 사용자 지정 HTML 도우미를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-111">To enhance that view, you will add a custom HTML helper that will truncate long descriptions.</span></span>

<span data-ttu-id="abaf8-112">그런 다음 드롭다운과 같은 폼 요소를 사용 하 여 데이터베이스의 앨범을 변경할 수 있는 편집 및 만들기 뷰를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-112">Afterwards, you will add the Edit and Create Views that will let you alter the albums in the database, with the help of form elements like dropdowns.</span></span>

<span data-ttu-id="abaf8-113">마지막으로 사용자가 앨범을 삭제 하 고 입력의 유효성을 검사 하 여 잘못 된 데이터를 입력 하는 것을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-113">Lastly, you will let users delete an album and also you will prevent them from entering wrong data by validating their input.</span></span>

<span data-ttu-id="abaf8-114">이 실습 랩에서는 **ASP.NET MVC**에 대 한 기본 지식이 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-114">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="abaf8-115">이전에 **ASP.NET mvc** 를 사용 하지 않은 경우 **ASP.NET mvc 기본** 실습 실습을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-115">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC Fundamentals** Hands-on Lab.</span></span>

<span data-ttu-id="abaf8-116">이 랩에서는 원본 폴더에 제공 된 샘플 웹 응용 프로그램에 사소한 변경 사항을 적용 하 여 앞에서 설명한 향상 된 기능 및 새로운 기능을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-116">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>

> [!NOTE]
> <span data-ttu-id="abaf8-117">모든 샘플 코드와 코드 조각은 [Microsoft 웹/WebCampTrainingKit 릴리스에서](https://aka.ms/webcamps-training-kit)제공 되는 웹 캠프 교육 키트에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-117">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="abaf8-118">이 랩에서 관련 된 프로젝트는 [ASP.NET MVC 4 도우미, 폼 및 유효성 검사](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-118">The project specific to this lab is available at [ASP.NET MVC 4 Helpers, Forms and Validation](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="abaf8-119">목표</span><span class="sxs-lookup"><span data-stu-id="abaf8-119">Objectives</span></span>

<span data-ttu-id="abaf8-120">이 실습 랩에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-120">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="abaf8-121">CRUD 작업을 지 원하는 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="abaf8-121">Create a controller to support CRUD operations</span></span>
- <span data-ttu-id="abaf8-122">HTML 테이블에 엔터티 속성을 표시 하는 인덱스 뷰 생성</span><span class="sxs-lookup"><span data-stu-id="abaf8-122">Generate an Index View to display entity properties in an HTML table</span></span>
- <span data-ttu-id="abaf8-123">사용자 지정 HTML 도우미 추가</span><span class="sxs-lookup"><span data-stu-id="abaf8-123">Add a custom HTML helper</span></span>
- <span data-ttu-id="abaf8-124">편집 보기 만들기 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="abaf8-124">Create and customize an Edit View</span></span>
- <span data-ttu-id="abaf8-125">HTTP GET 또는 HTTP POST 호출에 반응 하는 동작 메서드를 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-125">Differentiate between action methods that react to either HTTP-GET or HTTP-POST calls</span></span>
- <span data-ttu-id="abaf8-126">만들기 보기 추가 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="abaf8-126">Add and customize a Create View</span></span>
- <span data-ttu-id="abaf8-127">엔터티 삭제를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-127">Handle the deletion of an entity</span></span>
- <span data-ttu-id="abaf8-128">사용자 입력 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="abaf8-128">Validate user input</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="abaf8-129">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="abaf8-129">Prerequisites</span></span>

<span data-ttu-id="abaf8-130">이 랩을 완료 하려면 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-130">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="abaf8-131">[웹 또는 고급의 경우 2012 Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (설치 방법에 대 한 지침은 [부록 a를](#AppendixA) 참조 하세요.)</span><span class="sxs-lookup"><span data-stu-id="abaf8-131">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="abaf8-132">설치 프로그램</span><span class="sxs-lookup"><span data-stu-id="abaf8-132">Setup</span></span>

<span data-ttu-id="abaf8-133">**코드 조각 설치**</span><span class="sxs-lookup"><span data-stu-id="abaf8-133">**Installing Code Snippets**</span></span>

<span data-ttu-id="abaf8-134">편의를 위해이 랩에서 관리 하는 대부분의 코드는 Visual Studio 코드 조각으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-134">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="abaf8-135">코드 조각을 설치 하려면 **.\Source\Setup\CodeSnippets.vsi** 파일을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-135">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="abaf8-136">Visual Studio Code 코드 조각을 잘 모르는 경우이를 사용 하는 방법을 알아보려면이 문서의 부록 [B: 코드 조각&quot;사용](#AppendixB) &quot;부록을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="abaf8-136">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="abaf8-137">실습</span><span class="sxs-lookup"><span data-stu-id="abaf8-137">Exercises</span></span>

<span data-ttu-id="abaf8-138">다음 연습은이 실습 랩을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-138">The following exercises make up this Hands-On Lab:</span></span>

1. [<span data-ttu-id="abaf8-139">저장소 관리자 컨트롤러 및 해당 인덱스 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="abaf8-139">Creating the Store Manager controller and its Index view</span></span>](#Exercise1)
2. [<span data-ttu-id="abaf8-140">HTML 도우미 추가</span><span class="sxs-lookup"><span data-stu-id="abaf8-140">Adding an HTML Helper</span></span>](#Exercise2)
3. [<span data-ttu-id="abaf8-141">편집 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="abaf8-141">Creating the Edit View</span></span>](#Exercise3)
4. [<span data-ttu-id="abaf8-142">Create View 추가</span><span class="sxs-lookup"><span data-stu-id="abaf8-142">Adding a Create View</span></span>](#Exercise4)
5. [<span data-ttu-id="abaf8-143">삭제 처리</span><span class="sxs-lookup"><span data-stu-id="abaf8-143">Handling Deletion</span></span>](#Exercise5)
6. [<span data-ttu-id="abaf8-144">유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="abaf8-144">Adding Validation</span></span>](#Exercise6)
7. [<span data-ttu-id="abaf8-145">클라이언트 쪽에서에이 없는 jQuery 사용</span><span class="sxs-lookup"><span data-stu-id="abaf8-145">Using Unobtrusive jQuery at Client Side</span></span>](#Exercise7)

> [!NOTE]
> <span data-ttu-id="abaf8-146">각 연습에는 연습을 완료 한 후 얻게 되는 결과 솔루션을 포함 하는 **끝** 폴더가 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-146">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="abaf8-147">연습을 진행 하는 데 도움이 필요한 경우이 솔루션을 지침으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-147">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="abaf8-148">이 랩을 완료 하는 데 소요 되는 예상 시간: **60 분**</span><span class="sxs-lookup"><span data-stu-id="abaf8-148">Estimated time to complete this lab: **60 minutes**</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_the_Store_Manager_controller_and_its_Index_view"></a>
### <a name="exercise-1-creating-the-store-manager-controller-and-its-index-view"></a><span data-ttu-id="abaf8-149">연습 1: Store Manager 컨트롤러 및 해당 인덱스 보기 만들기</span><span class="sxs-lookup"><span data-stu-id="abaf8-149">Exercise 1: Creating the Store Manager controller and its Index view</span></span>

<span data-ttu-id="abaf8-150">이 연습에서는 CRUD 작업을 지원 하기 위해 새 컨트롤러를 만드는 방법, 데이터베이스에서 앨범 목록을 반환 하도록 인덱스 작업 메서드를 사용자 지정 하 고, 마지막으로 ASP.NET MVC의 스 캐 폴딩을 활용 하 여 인덱스 뷰 템플릿을 생성 하는 방법에 대해 설명 합니다. HTML 테이블에 앨범 속성을 표시 하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-150">In this exercise, you will learn how to create a new controller to support CRUD operations, customize its Index action method to return a list of albums from the database and finally generating an Index View template taking advantage of ASP.NET MVC's scaffolding feature to display the albums' properties in an HTML table.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_StoreManagerController"></a>
#### <a name="task-1---creating-the-storemanagercontroller"></a><span data-ttu-id="abaf8-151">작업 1-StoreManagerController 만들기</span><span class="sxs-lookup"><span data-stu-id="abaf8-151">Task 1 - Creating the StoreManagerController</span></span>

<span data-ttu-id="abaf8-152">이 작업에서는 CRUD 작업을 지원 하기 위해 **StoreManagerController** 라는 새 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-152">In this task, you will create a new controller called **StoreManagerController** to support CRUD operations.</span></span>

1. <span data-ttu-id="abaf8-153">**Source/Ex1-CreatingTheStoreManagerController/begin/** 폴더에 있는 **시작** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-153">Open the **Begin** solution located at **Source/Ex1-CreatingTheStoreManagerController/Begin/** folder.</span></span>

   1. <span data-ttu-id="abaf8-154">계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-154">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="abaf8-155">이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-155">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="abaf8-156">**NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-156">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="abaf8-157">마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-157">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="abaf8-158">NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-158">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="abaf8-159">NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-159">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="abaf8-160">이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-160">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="abaf8-161">새 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-161">Add a new controller.</span></span> <span data-ttu-id="abaf8-162">이렇게 하려면 솔루션 탐색기 내의 **Controllers** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** 를 선택한 다음 **컨트롤러** 명령을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-162">To do this, right-click the **Controllers** folder within the Solution Explorer, select **Add** and then the **Controller** command.</span></span> <span data-ttu-id="abaf8-163">**컨트롤러** **이름을** **StoreManagerController** 로 변경 하 고 **빈 읽기/쓰기 동작이 포함 된 MVC 컨트롤러** 옵션을 선택 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-163">Change the **Controller** **Name** to **StoreManagerController** and make sure the option **MVC controller with empty read/write actions** is selected.</span></span> <span data-ttu-id="abaf8-164">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-164">Click **Add**.</span></span>

    <span data-ttu-id="abaf8-165">![컨트롤러 추가 대화 상자](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "컨트롤러 추가 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="abaf8-165">![Add controller dialog](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "Add controller dialog")</span></span>

    <span data-ttu-id="abaf8-166">*컨트롤러 추가 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="abaf8-166">*Add Controller Dialog*</span></span>

    <span data-ttu-id="abaf8-167">새 컨트롤러 클래스가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-167">A new Controller class is generated.</span></span> <span data-ttu-id="abaf8-168">읽기/쓰기에 대 한 작업을 추가 하도록 지정 했으므로 이러한 작업에 대해 스텁 메서드를 사용 하 여 일반적인 CRUD 작업을 수행 하 고 응용 프로그램 관련 논리를 포함 하 라는 메시지를 표시 하 여 일반적인 CRUD 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-168">Since you indicated to add actions for read/write, stub methods for those, common CRUD actions are created with TODO comments filled in, prompting to include the application specific logic.</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Customizing_the_StoreManager_Index"></a>
#### <a name="task-2---customizing-the-storemanager-index"></a><span data-ttu-id="abaf8-169">작업 2-StoreManager 인덱스 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="abaf8-169">Task 2 - Customizing the StoreManager Index</span></span>

<span data-ttu-id="abaf8-170">이 태스크에서는 StoreManager Index 동작 메서드를 사용자 지정 하 여 데이터베이스의 앨범 목록과 함께 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-170">In this task, you will customize the StoreManager Index action method to return a View with the list of albums from the database.</span></span>

1. <span data-ttu-id="abaf8-171">StoreManagerController 클래스에서 다음 *using* 지시문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-171">In the StoreManagerController class, add the following *using* directives.</span></span>

    <span data-ttu-id="abaf8-172">(코드 조각- *ASP.NET MVC 4 도우미 및 폼 및 유효성 검사-MvcMusicStore를 사용 하 여 Ex1*)</span><span class="sxs-lookup"><span data-stu-id="abaf8-172">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 using MvcMusicStore*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample1.cs)]
2. <span data-ttu-id="abaf8-173">MusicStoreEntities의 인스턴스를 보유할 필드를 **StoreManagerController** 에 추가 합니다 **.**</span><span class="sxs-lookup"><span data-stu-id="abaf8-173">Add a field to the **StoreManagerController** to hold an instance of **MusicStoreEntities.**</span></span>

    <span data-ttu-id="abaf8-174">(코드 조각- *ASP.NET MVC 4 도우미 및 폼 및 유효성 검사-Ex1 MusicStoreEntities*)</span><span class="sxs-lookup"><span data-stu-id="abaf8-174">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 MusicStoreEntities*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample2.cs)]
3. <span data-ttu-id="abaf8-175">StoreManagerController Index 작업을 구현 하 여 앨범 목록이 포함 된 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-175">Implement the StoreManagerController Index action to return a View with the list of albums.</span></span>

    <span data-ttu-id="abaf8-176">컨트롤러 작업 논리는 앞에서 작성 한 StoreController의 인덱스 작업과 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-176">The Controller action logic will be very similar to the StoreController's Index action written earlier.</span></span> <span data-ttu-id="abaf8-177">LINQ를 사용 하 여 표시할 장르 및 음악가 정보를 비롯 한 모든 앨범을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-177">Use LINQ to retrieve all albums, including Genre and Artist information for display.</span></span>

    <span data-ttu-id="abaf8-178">(코드 조각- *ASP.NET MVC 4 도우미 및 폼 및 유효성 검사-Ex1 StoreManagerController Index*)</span><span class="sxs-lookup"><span data-stu-id="abaf8-178">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 StoreManagerController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample3.cs)]

<a id="Ex1Task3"></a>

<a id="strongTask_3_-_Creating_the_Index_Viewstrong"></a>
#### <a name="task-3---creating-the-index-view"></a><span data-ttu-id="abaf8-179">작업 3-인덱스 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="abaf8-179">Task 3 - Creating the Index View</span></span>

<span data-ttu-id="abaf8-180">이 태스크에서는 **Storemanager** 컨트롤러에서 반환 된 앨범 목록을 표시 하는 인덱스 뷰 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-180">In this task, you will create the Index View template to display the list of albums returned by the **StoreManager** Controller.</span></span>

1. <span data-ttu-id="abaf8-181">새 뷰 템플릿을 만들기 전에 **보기 추가 대화 상자** 에서 사용할 **앨범** 클래스에 대해 알 수 있도록 프로젝트를 빌드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-181">Before creating the new View template, you should build the project so that the **Add View Dialog** knows about the **Album** class to use.</span></span> <span data-ttu-id="abaf8-182">**빌드 선택 | MvcMusicStore를 빌드하여** 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-182">Select **Build | Build MvcMusicStore** to build the project.</span></span>
2. <span data-ttu-id="abaf8-183">**인덱스** 동작 메서드 내부를 마우스 오른쪽 단추로 클릭 하 고 **뷰 추가**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-183">Right-click inside the **Index** action method and select **Add View**.</span></span> <span data-ttu-id="abaf8-184">그러면 **보기 추가** 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-184">This will bring up the **Add View** dialog.</span></span>

    <span data-ttu-id="abaf8-185">![뷰 추가](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "뷰 추가")</span><span class="sxs-lookup"><span data-stu-id="abaf8-185">![Add view](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "Add view")</span></span>

    <span data-ttu-id="abaf8-186">*Index 메서드 내에서 뷰 추가*</span><span class="sxs-lookup"><span data-stu-id="abaf8-186">*Adding a View from within the Index method*</span></span>
3. <span data-ttu-id="abaf8-187">보기 추가 대화 상자에서 뷰 이름이 **Index**인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-187">In the Add View dialog, verify that the View Name is **Index**.</span></span> <span data-ttu-id="abaf8-188">**강력한 형식의 뷰 만들기** 옵션을 선택 하 고 **모델 클래스** 드롭다운에서 **앨범 (MvcMusicStore)** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-188">Select the **Create a strongly-typed view** option, and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down.</span></span> <span data-ttu-id="abaf8-189">**스 캐 폴드 템플릿** 드롭다운에서 **목록** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-189">Select **List** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="abaf8-190">**뷰 엔진** 은 **Razor** 로 두고 다른 필드는 기본값으로 유지 한 다음 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-190">Leave the **View engine** to **Razor** and the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="abaf8-191">![인덱스 뷰 추가](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "인덱스 뷰 추가")</span><span class="sxs-lookup"><span data-stu-id="abaf8-191">![Adding an index view](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "Adding an index view")</span></span>

    <span data-ttu-id="abaf8-192">*인덱스 뷰 추가*</span><span class="sxs-lookup"><span data-stu-id="abaf8-192">*Adding an Index View*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Customizing_the_scaffold_of_the_Index_View"></a>
#### <a name="task-4---customizing-the-scaffold-of-the-index-view"></a><span data-ttu-id="abaf8-193">작업 4-인덱스 뷰의 스 캐 폴드 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="abaf8-193">Task 4 - Customizing the scaffold of the Index View</span></span>

<span data-ttu-id="abaf8-194">이 작업에서는 ASP.NET MVC 스 캐 폴딩 기능을 사용 하 여 만든 단순 보기 템플릿을 조정 하 여 원하는 필드를 표시 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-194">In this task, you will adjust the simple View template created with ASP.NET MVC scaffolding feature to have it display the fields you want.</span></span>

> [!NOTE]
> <span data-ttu-id="abaf8-195">ASP.NET MVC 내에서 **스 캐 폴딩** 지원은 앨범 모델의 모든 필드를 나열 하는 간단한 뷰 템플릿을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-195">The **scaffolding** support within ASP.NET MVC generates a simple View template which lists all fields in the Album model.</span></span> <span data-ttu-id="abaf8-196">**스 캐 폴딩** 은 강력한 형식의 뷰를 시작 하는 빠른 방법을 제공 합니다. 즉, 뷰 템플릿을 수동으로 작성 하지 않고 스 캐 폴딩을 빠르게 기본 템플릿을 생성 한 다음 생성 된 코드를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-196">**Scaffolding** provides a quick way to get started on a strongly typed view: rather than having to write the View template manually, scaffolding quickly generates a default template and then you can modify the generated code.</span></span>

1. <span data-ttu-id="abaf8-197">만든 코드를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-197">Review the code created.</span></span> <span data-ttu-id="abaf8-198">생성 된 필드 목록은 **스 캐 폴딩** 이 표 형식 데이터를 표시 하는 데 사용 하는 다음 HTML 테이블에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-198">The generated list of fields will be part of the following HTML table that **Scaffolding** is using for displaying tabular data.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample4.cshtml)]
2. <span data-ttu-id="abaf8-199">**&lt;테이블&gt;** 코드를 다음 코드로 바꿔 **장르**, **음악가**, **앨범 제목**및 **가격** 필드만 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-199">Replace the **&lt;table&gt;** code with the following code to display only the **Genre**, **Artist**, **Album Title**, and **Price** fields.</span></span> <span data-ttu-id="abaf8-200">그러면 **AlbumId** 및 **앨범 아트 URL** 열이 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-200">This deletes the **AlbumId** and **Album Art URL** columns.</span></span> <span data-ttu-id="abaf8-201">또한 GenreId 및 ArtistId 열을 변경 하 여 **Artist.Name** 및 **Genre.Name**의 연결 된 클래스 속성을 표시 하 고 **세부 정보** 링크를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-201">Also, it changes GenreId and ArtistId columns to display their linked class properties of **Artist.Name** and **Genre.Name**, and removes the **Details** link.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample5.cshtml)]
3. <span data-ttu-id="abaf8-202">다음 설명을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-202">Change the following descriptions.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample6.cshtml)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="abaf8-203">작업 5-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="abaf8-203">Task 5 - Running the Application</span></span>

<span data-ttu-id="abaf8-204">이 태스크에서는 **Storemanager** **인덱스** 뷰 템플릿이 이전 단계의 디자인에 따라 앨범 목록을 표시 하는지 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-204">In this task, you will test that the **StoreManager** **Index** View template displays a list of albums according to the design of the previous steps.</span></span>

1. <span data-ttu-id="abaf8-205">**F5** 키를 눌러 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-205">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="abaf8-206">프로젝트가 홈 페이지에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-206">The project starts in the Home page.</span></span> <span data-ttu-id="abaf8-207">URL을 **/Storemanager** 로 변경 하 여 앨범 목록이 표시 되는지 확인 하 고 **제목**, **음악가** 및 **장르**를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-207">Change the URL to **/StoreManager** to verify that a list of albums is displayed, showing their **Title**, **Artist** and **Genre**.</span></span>

    <span data-ttu-id="abaf8-208">![앨범 목록 찾아보기](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "앨범 목록 찾아보기")</span><span class="sxs-lookup"><span data-stu-id="abaf8-208">![Browsing the list of albums](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "Browsing the list of albums")</span></span>

    <span data-ttu-id="abaf8-209">*앨범 목록 찾아보기*</span><span class="sxs-lookup"><span data-stu-id="abaf8-209">*Browsing the list of albums*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Adding_an_HTML_Helper"></a>
### <a name="exercise-2-adding-an-html-helper"></a><span data-ttu-id="abaf8-210">연습 2: HTML 도우미 추가</span><span class="sxs-lookup"><span data-stu-id="abaf8-210">Exercise 2: Adding an HTML Helper</span></span>

<span data-ttu-id="abaf8-211">StoreManager 인덱스 페이지에는 한 가지 잠재적인 문제가 있습니다. Title 및 음악가 이름 속성은 모두 테이블 서식 지정을 throw 할 수 있을 정도로 길어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-211">The StoreManager Index page has one potential issue: Title and Artist Name properties can both be long enough to throw off the table formatting.</span></span> <span data-ttu-id="abaf8-212">이 연습에서는 해당 텍스트를 잘라내는 사용자 지정 HTML 도우미를 추가 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-212">In this exercise you will learn how to add a custom HTML helper to truncate that text.</span></span>

<span data-ttu-id="abaf8-213">다음 그림에서는 작은 브라우저 크기를 사용할 때 텍스트의 길이 때문에 형식이 수정 되는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-213">In the following figure, you can see how the format is modified because of the length of the text when you use a small browser size.</span></span>

<span data-ttu-id="abaf8-214">![잘리지 않은 텍스트를 사용 하 여 앨범 목록 찾아보기](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "잘리지 않은 텍스트를 사용 하 여 앨범 목록 찾아보기")</span><span class="sxs-lookup"><span data-stu-id="abaf8-214">![Browsing the list of Albums with not truncated text](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "Browsing the list of Albums with not truncated text")</span></span>

<span data-ttu-id="abaf8-215">*잘리지 않은 텍스트를 사용 하 여 앨범 목록 찾아보기*</span><span class="sxs-lookup"><span data-stu-id="abaf8-215">*Browsing the list of Albums with not truncated text*</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Extending_the_HTML_Helper"></a>
#### <a name="task-1---extending-the-html-helper"></a><span data-ttu-id="abaf8-216">작업 1-HTML 도우미 확장</span><span class="sxs-lookup"><span data-stu-id="abaf8-216">Task 1 - Extending the HTML Helper</span></span>

<span data-ttu-id="abaf8-217">이 작업에서는 ASP.NET MVC 뷰 내에서 노출 되는 **HTML** 개체에 새 메서드 **Truncate** 를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-217">In this task, you will add a new method **Truncate** to the **HTML** object exposed within ASP.NET MVC Views.</span></span> <span data-ttu-id="abaf8-218">이렇게 하려면 ASP.NET MVC에서 제공 하는 기본 제공 system.string **도우미** 클래스에 대 한 **확장 메서드** 를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-218">To do this, you will implement an **extension method** to the built-in **System.Web.Mvc.HtmlHelper** class provided by ASP.NET MVC.</span></span>

> [!NOTE]
> <span data-ttu-id="abaf8-219">**확장 메서드에**대 한 자세한 내용은이 msdn 문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="abaf8-219">To read more about **Extension Methods**, please visit this msdn article.</span></span> <span data-ttu-id="abaf8-220">[https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="abaf8-220">[https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx).</span></span>

1. <span data-ttu-id="abaf8-221">**Source/Ex2-AddingAnHTMLHelper/begin/** 폴더에 있는 **시작** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-221">Open the **Begin** solution located at **Source/Ex2-AddingAnHTMLHelper/Begin/** folder.</span></span> <span data-ttu-id="abaf8-222">그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-222">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="abaf8-223">제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-223">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="abaf8-224">이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-224">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="abaf8-225">**NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-225">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="abaf8-226">마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-226">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="abaf8-227">NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-227">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="abaf8-228">NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-228">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="abaf8-229">이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-229">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="abaf8-230">StoreManager의 인덱스 뷰를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-230">Open StoreManager's Index View.</span></span> <span data-ttu-id="abaf8-231">이렇게 하려면 솔루션 탐색기에서 **Views** 폴더를 확장 하 고 **storemanager** 를 확장 한 다음 **Index. cshtml** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-231">To do this, in the Solution Explorer expand the **Views** folder, then the **StoreManager** and open the **Index.cshtml** file.</span></span>
3. <span data-ttu-id="abaf8-232"><strong>자르기</strong> 도우미 메서드를 정의 하려면 <strong>@model</strong> 지시문 아래에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-232">Add the following code below the <strong>@model</strong> directive to define the <strong>Truncate</strong> helper method.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample7.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Truncating_Text_in_the_Page"></a>
#### <a name="task-2---truncating-text-in-the-page"></a><span data-ttu-id="abaf8-233">작업 2-페이지에서 텍스트 잘라내기</span><span class="sxs-lookup"><span data-stu-id="abaf8-233">Task 2 - Truncating Text in the Page</span></span>

<span data-ttu-id="abaf8-234">이 태스크에서는 **truncate** 메서드를 사용 하 여 뷰 템플릿의 텍스트를 자릅니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-234">In this task, you will use the **Truncate** method to truncate the text in the View template.</span></span>

1. <span data-ttu-id="abaf8-235">StoreManager의 인덱스 뷰를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-235">Open StoreManager's Index View.</span></span> <span data-ttu-id="abaf8-236">이렇게 하려면 솔루션 탐색기에서 **Views** 폴더를 확장 하 고 **storemanager** 를 확장 한 다음 **Index. cshtml** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-236">To do this, in the Solution Explorer expand the **Views** folder, then the **StoreManager** and open the **Index.cshtml** file.</span></span>
2. <span data-ttu-id="abaf8-237">**음악가 이름** 및 앨범의 **제목을**표시 하는 줄을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-237">Replace the lines that show the **Artist Name** and Album's **Title**.</span></span> <span data-ttu-id="abaf8-238">이렇게 하려면 다음 줄을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-238">To do this, replace the following lines.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample8.cshtml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="abaf8-239">작업 3-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="abaf8-239">Task 3 - Running the Application</span></span>

<span data-ttu-id="abaf8-240">이 태스크에서는 **Storemanager** **인덱스** 뷰 템플릿이 앨범의 제목 및 음악가 이름을 잘라내는 지 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-240">In this task, you will test that the **StoreManager** **Index** View template truncates the Album's Title and Artist Name.</span></span>

1. <span data-ttu-id="abaf8-241">**F5** 키를 눌러 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-241">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="abaf8-242">프로젝트가 홈 페이지에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-242">The project starts in the Home page.</span></span> <span data-ttu-id="abaf8-243">URL을 **/Storemanager** 로 변경 하 여 **제목** 및 **음악가** 열의 긴 텍스트가 잘리는 지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-243">Change the URL to **/StoreManager** to verify that long texts in the **Title** and **Artist** column are truncated.</span></span>

    <span data-ttu-id="abaf8-244">![잘린 제목 및 음악가 이름](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "잘린 제목 및 음악가 이름")</span><span class="sxs-lookup"><span data-stu-id="abaf8-244">![Truncated titles and artists names](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "Truncated titles and artists names")</span></span>

    <span data-ttu-id="abaf8-245">*잘린 제목 및 음악가 이름*</span><span class="sxs-lookup"><span data-stu-id="abaf8-245">*Truncated Titles and Artist Names*</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Creating_the_Edit_View"></a>
### <a name="exercise-3-creating-the-edit-view"></a><span data-ttu-id="abaf8-246">연습 3: 편집 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="abaf8-246">Exercise 3: Creating the Edit View</span></span>

<span data-ttu-id="abaf8-247">이 연습에서는 상점 관리자가 앨범을 편집할 수 있도록 하는 양식을 만드는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-247">In this exercise, you will learn how to create a form to allow store managers to edit an Album.</span></span> <span data-ttu-id="abaf8-248">**/StoreManager/Edit/id** URL (**id** 를 편집할 앨범의 고유 id)을 탐색 하므로 서버에 대 한 HTTP GET 호출을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-248">They will browse the **/StoreManager/Edit/id** URL (**id** being the unique id of the album to edit), thus making an HTTP-GET call to the server.</span></span>

<span data-ttu-id="abaf8-249">컨트롤러 편집 작업 메서드는 데이터베이스에서 적절 한 앨범을 검색 하 고,이를 캡슐화 하는 **StoreManagerViewModel** 개체를 만든 다음,이를 보기 템플릿에 전달 하 여 HTML 페이지를 사용자에 게 다시 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-249">The Controller Edit action method will retrieve the appropriate Album from the database, create a **StoreManagerViewModel** object to encapsulate it (along with a list of Artists and Genres), and then pass it off to a View template to render the HTML page back to the user.</span></span> <span data-ttu-id="abaf8-250">이 페이지에는 앨범 속성을 편집할 수 있는 텍스트 상자 및 드롭다운이 있는 **&lt;폼&gt;** 요소가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-250">This page will contain a **&lt;form&gt;** element with textboxes and dropdowns for editing the Album properties.</span></span>

<span data-ttu-id="abaf8-251">사용자가 앨범 양식 값을 업데이트 하 고 **저장** 단추를 클릭 하면 HTTP POST 호출을 통해 변경 내용이 **/StoreManager/Edit/id**로 다시 전송 됩니다. URL은 마지막 호출에서와 동일 하 게 유지 되지만, ASP.NET MVC는이 시간을 HTTP POST로 식별 하므로 다른 편집 작업 메서드 ( **[HttpPost]** 를 사용 하 여 데코레이팅된 항목)를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-251">Once the user updates the Album form values and clicks the **Save** button, the changes are submitted via an HTTP-POST call back to **/StoreManager/Edit/id**. Although the URL remains the same as in the last call, ASP.NET MVC identifies that this time it is an HTTP-POST and therefore executes a different Edit action method (one decorated with **[HttpPost]**).</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Edit_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-edit-action-method"></a><span data-ttu-id="abaf8-252">작업 1-HTTP-GET 편집 작업 메서드 구현</span><span class="sxs-lookup"><span data-stu-id="abaf8-252">Task 1 - Implementing the HTTP-GET Edit Action Method</span></span>

<span data-ttu-id="abaf8-253">이 태스크에서는 편집 작업 메서드의 HTTP GET 버전을 구현 하 여 데이터베이스에서 적절 한 앨범을 검색 하 고 모든 장르 및 음악가의 목록도 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-253">In this task, you will implement the HTTP-GET version of the Edit action method to retrieve the appropriate Album from the database, as well as a list of all Genres and Artists.</span></span> <span data-ttu-id="abaf8-254">마지막 단계에서 정의 된 **StoreManagerViewModel** 개체에이 데이터를 패키지 합니다. 그러면 응답을 렌더링 하기 위해 뷰 템플릿에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-254">It will package this data up into the **StoreManagerViewModel** object defined in the last step, which will then be passed to a View template to render the response with.</span></span>

1. <span data-ttu-id="abaf8-255">**원본/Ex3-만들기** 에 있는 **시작** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-255">Open the **Begin** solution located at **Source/Ex3-CreatingTheEditView/Begin/** folder.</span></span> <span data-ttu-id="abaf8-256">그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-256">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="abaf8-257">제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-257">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="abaf8-258">이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-258">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="abaf8-259">**NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-259">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="abaf8-260">마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-260">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="abaf8-261">NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-261">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="abaf8-262">NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-262">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="abaf8-263">이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-263">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="abaf8-264">**StoreManagerController** 클래스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-264">Open the **StoreManagerController** class.</span></span> <span data-ttu-id="abaf8-265">이렇게 하려면 **Controllers** 폴더를 확장 하 고 **StoreManagerController.cs**를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-265">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="abaf8-266">**HTTP-GET Edit** 작업 메서드를 다음 코드로 바꾸어 해당 하는 **앨범** 뿐만 아니라 **장르** 및 **음악가** 목록을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-266">Replace the **HTTP-GET Edit** action method with the following code to retrieve the appropriate **Album** as well as the **Genres** and **Artists** lists.</span></span>

    <span data-ttu-id="abaf8-267">(코드 조각- *ASP.NET MVC 4 도우미 및 폼 및 유효성 검사-Ex3 STOREMANAGERCONTROLLER HTTP-편집 작업 가져오기*)</span><span class="sxs-lookup"><span data-stu-id="abaf8-267">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex3 StoreManagerController HTTP-GET Edit action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample9.cs)]

    > [!NOTE]
    > <span data-ttu-id="abaf8-268">**Collections** 및 장르에 **대해 system.object를 사용 하** 는 대신 **system.web을 사용** 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-268">You are using **System.Web.Mvc** **SelectList** for Artists and Genres instead of the **System.Collections.Generic** List.</span></span>
    > 
    > <span data-ttu-id="abaf8-269">**Selectlist** 는 HTML 드롭다운을 채우고 현재 선택 등의 작업을 관리 하는 클리너 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-269">**SelectList** is a cleaner way to populate HTML dropdowns and manage things like current selection.</span></span> <span data-ttu-id="abaf8-270">컨트롤러 작업에서 이러한 ViewModel 개체를 인스턴스화하고 나중에 설정 하면 편집 양식 시나리오가 더 명확 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-270">Instantiating and later setting up these ViewModel objects in the controller action will make the Edit form scenario cleaner.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Creating_the_Edit_View"></a>
#### <a name="task-2---creating-the-edit-view"></a><span data-ttu-id="abaf8-271">작업 2-편집 보기 만들기</span><span class="sxs-lookup"><span data-stu-id="abaf8-271">Task 2 - Creating the Edit View</span></span>

<span data-ttu-id="abaf8-272">이 태스크에서는 나중에 앨범 속성을 표시 하는 편집 보기 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-272">In this task, you will create an Edit View template that will later display the album properties.</span></span>

1. <span data-ttu-id="abaf8-273">편집 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-273">Create the Edit View.</span></span> <span data-ttu-id="abaf8-274">이렇게 하려면 **편집** 동작 메서드 내부를 마우스 오른쪽 단추로 클릭 하 고 **뷰 추가**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-274">To do this, right-click inside the **Edit** action method and select **Add View**.</span></span>
2. <span data-ttu-id="abaf8-275">보기 추가 대화 상자에서 뷰 이름이 **편집**인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-275">In the Add View dialog, verify that the View Name is **Edit**.</span></span> <span data-ttu-id="abaf8-276">강력한 형식의 **뷰 만들기** 확인란을 선택 하 고 **데이터 클래스 보기** 드롭다운에서 **앨범 (MvcMusicStore)** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-276">Check the **Create a strongly-typed view** checkbox and select **Album (MvcMusicStore.Models)** from the **View data class** drop-down.</span></span> <span data-ttu-id="abaf8-277">**스 캐 폴드 템플릿** 드롭다운에서 **편집** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-277">Select **Edit** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="abaf8-278">다른 필드의 기본값을 그대로 두고 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-278">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="abaf8-279">![편집 뷰 추가](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "편집 뷰 추가")</span><span class="sxs-lookup"><span data-stu-id="abaf8-279">![Adding an Edit view](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "Adding an Edit view")</span></span>

    <span data-ttu-id="abaf8-280">*편집 뷰 추가*</span><span class="sxs-lookup"><span data-stu-id="abaf8-280">*Adding an Edit view*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="abaf8-281">작업 3-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="abaf8-281">Task 3 - Running the Application</span></span>

<span data-ttu-id="abaf8-282">이 태스크에서는 **Storemanager** **편집** 뷰 페이지에 매개 변수로 전달 된 앨범의 속성 값이 표시 되는 것을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-282">In this task, you will test that the **StoreManager** **Edit** View page displays the properties' values for the album passed as parameter.</span></span>

1. <span data-ttu-id="abaf8-283">**F5** 키를 눌러 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-283">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="abaf8-284">프로젝트가 홈 페이지에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-284">The project starts in the Home page.</span></span> <span data-ttu-id="abaf8-285">URL을 **/StoreManager/Edit/1** 로 변경 하 여 전달 된 앨범의 속성 값이 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-285">Change the URL to **/StoreManager/Edit/1** to verify that the properties' values for the album passed are displayed.</span></span>

    <span data-ttu-id="abaf8-286">![탐색 앨범의 편집 보기](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "탐색 앨범의 편집 보기")</span><span class="sxs-lookup"><span data-stu-id="abaf8-286">![Browsing Album's Edit View](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "Browsing Album's Edit View")</span></span>

    <span data-ttu-id="abaf8-287">*탐색 앨범의 편집 보기*</span><span class="sxs-lookup"><span data-stu-id="abaf8-287">*Browsing Album's Edit view*</span></span>

<a id="Ex3Task4"></a>

<a id="Task_4_-_Implementing_drop-downs_on_the_Album_Editor_Template"></a>
#### <a name="task-4---implementing-drop-downs-on-the-album-editor-template"></a><span data-ttu-id="abaf8-288">작업 4-앨범 편집기 템플릿에서 드롭다운 구현</span><span class="sxs-lookup"><span data-stu-id="abaf8-288">Task 4 - Implementing drop-downs on the Album Editor Template</span></span>

<span data-ttu-id="abaf8-289">이 태스크에서는 사용자가 음악가와 장르 목록에서 선택할 수 있도록 마지막 태스크에서 만든 보기 템플릿에 드롭다운을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-289">In this task, you will add drop-downs to the View template created in the last task, so that the user can select from a list of Artists and Genres.</span></span>

1. <span data-ttu-id="abaf8-290">모든 **앨범** 필드 집합 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-290">Replace all the **Album** fieldset code with the following:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample10.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="abaf8-291">아티스트와 장르를 선택 하기 위한 드롭다운을 렌더링 하기 위한 **Html DropDownList** 도우미가 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-291">An **Html.DropDownList** helper has been added to render drop-downs for choosing Artists and Genres.</span></span> <span data-ttu-id="abaf8-292">**Html. DropDownList** 에 전달 된 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-292">The parameters passed to **Html.DropDownList** are:</span></span>
    > 
    > 1. <span data-ttu-id="abaf8-293">폼 필드의 이름 ( **&quot;ArtistId&quot;** )입니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-293">The name of the form field (**&quot;ArtistId&quot;**).</span></span>
    > 2. <span data-ttu-id="abaf8-294">드롭다운의 값 **목록** 입니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-294">The **SelectList** of values for the drop-down.</span></span>

<a id="Ex3Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="abaf8-295">작업 5-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="abaf8-295">Task 5 - Running the Application</span></span>

<span data-ttu-id="abaf8-296">이 태스크에서는 **Storemanager** **편집** 뷰 페이지에서 음악가 및 장르 ID 텍스트 필드 대신 드롭다운을 표시 하는지 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-296">In this task, you will test that the **StoreManager** **Edit** View page displays drop-downs instead of Artist and Genre ID text fields.</span></span>

1. <span data-ttu-id="abaf8-297">**F5** 키를 눌러 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-297">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="abaf8-298">프로젝트가 홈 페이지에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-298">The project starts in the Home page.</span></span> <span data-ttu-id="abaf8-299">URL을 **/StoreManager/Edit/1** 로 변경 하 여 음악가 및 장르 ID 텍스트 필드가 아닌 드롭다운이 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-299">Change the URL to **/StoreManager/Edit/1** to verify that it displays drop-downs instead of Artist and Genre ID text fields.</span></span>

    <span data-ttu-id="abaf8-300">![드롭다운을 사용 하 여 앨범의 편집 뷰 찾아보기](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "드롭다운을 사용 하 여 앨범의 편집 뷰 찾아보기")</span><span class="sxs-lookup"><span data-stu-id="abaf8-300">![Browsing Album's Edit View with drop downs](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "Browsing Album's Edit View with drop downs")</span></span>

    <span data-ttu-id="abaf8-301">*이번에는 드롭다운을 사용 하 여 앨범의 편집 보기를 검색 합니다.*</span><span class="sxs-lookup"><span data-stu-id="abaf8-301">*Browsing Album's Edit view, this time with dropdowns*</span></span>

<a id="Ex3Task6"></a>

<a id="Task_6_-_Implementing_the_HTTP-POST_Edit_action_method"></a>
#### <a name="task-6---implementing-the-http-post-edit-action-method"></a><span data-ttu-id="abaf8-302">작업 6-HTTP-사후 편집 작업 메서드 구현</span><span class="sxs-lookup"><span data-stu-id="abaf8-302">Task 6 - Implementing the HTTP-POST Edit action method</span></span>

<span data-ttu-id="abaf8-303">이제 편집 뷰가 예상 대로 표시 되므로, 앨범에 대 한 변경 내용을 저장 하기 위해 HTTP POST 편집 작업 메서드를 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-303">Now that the Edit View displays as expected, you need to implement the HTTP-POST Edit Action method to save the changes made to the Album.</span></span>

1. <span data-ttu-id="abaf8-304">필요한 경우 브라우저를 닫고 Visual Studio 창으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-304">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="abaf8-305">**Controllers** 폴더에서 **StoreManagerController** 을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-305">Open **StoreManagerController** from the **Controllers** folder.</span></span>
2. <span data-ttu-id="abaf8-306">**HTTP-POST 편집** 작업 메서드 코드를 다음으로 바꿉니다 (교체 해야 하는 메서드는 두 개의 매개 변수를 받는 오버 로드 된 버전).</span><span class="sxs-lookup"><span data-stu-id="abaf8-306">Replace **HTTP-POST Edit** action method code with the following (note that the method that must be replaced is overloaded version that receives two parameters):</span></span>

    <span data-ttu-id="abaf8-307">(코드 조각- *ASP.NET MVC 4 도우미 및 폼 및 유효성 검사-Ex3 STOREMANAGERCONTROLLER HTTP-사후 편집 작업*)</span><span class="sxs-lookup"><span data-stu-id="abaf8-307">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex3 StoreManagerController HTTP-POST Edit action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample11.cs)]

    > [!NOTE]
    > <span data-ttu-id="abaf8-308">이 메서드는 사용자가 뷰의 **저장** 단추를 클릭 하 고 폼 값의 HTTP POST를 서버에 다시 실행 하 여 데이터베이스에 보관 하는 경우 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-308">This method will be executed when the user clicks the **Save** button of the View and performs an HTTP-POST of the form values back to the server to persist them in the database.</span></span> <span data-ttu-id="abaf8-309">데코레이터 **[HttpPost]** 는 메서드를 이러한 HTTP 게시 시나리오에 사용 해야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-309">The decorator **[HttpPost]** indicates that the method should be used for those HTTP-POST scenarios.</span></span> <span data-ttu-id="abaf8-310">메서드는 **앨범** 개체를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-310">The method takes an **Album** object.</span></span> <span data-ttu-id="abaf8-311">ASP.NET MVC는 게시 된 &lt;양식&gt; 값에서 앨범 개체를 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-311">ASP.NET MVC will automatically create the Album object from the posted &lt;form&gt; values.</span></span>
    > 
    > <span data-ttu-id="abaf8-312">이 메서드는 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-312">The method will perform these steps:</span></span>
    > 
    > 1. <span data-ttu-id="abaf8-313">Model이 올바르면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-313">If model is valid:</span></span>
    > 
    >     1. <span data-ttu-id="abaf8-314">컨텍스트에서 앨범 항목을 업데이트 하 여 수정 된 개체로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-314">Update the album entry in the context to mark it as a modified object.</span></span>
    >     2. <span data-ttu-id="abaf8-315">변경 내용을 저장 하 고 인덱스 뷰로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-315">Save the changes and redirect to the index view.</span></span>
    > 2. <span data-ttu-id="abaf8-316">모델이 유효 하지 않으면 ViewBag을 **GenreId** 및 **ArtistId**로 채운 다음 수신 된 앨범 개체가 있는 뷰를 반환 하 여 사용자가 필요한 업데이트를 수행할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-316">If the model is not valid, it will populate the ViewBag with the **GenreId** and **ArtistId**, then it will return the view with the received Album object to allow the user perform any required update.</span></span>

<a id="Ex3Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a><span data-ttu-id="abaf8-317">작업 7-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="abaf8-317">Task 7 - Running the Application</span></span>

<span data-ttu-id="abaf8-318">이 태스크에서는 **Storemanager 편집** 뷰 페이지가 실제로 업데이트 된 앨범 데이터를 데이터베이스에 저장 하는지 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-318">In this task, you will test that the **StoreManager Edit** View page actually saves the updated Album data in the database.</span></span>

1. <span data-ttu-id="abaf8-319">**F5** 키를 눌러 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-319">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="abaf8-320">프로젝트가 홈 페이지에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-320">The project starts in the Home page.</span></span> <span data-ttu-id="abaf8-321">URL을 **/StoreManager/Edit/1**로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-321">Change the URL to **/StoreManager/Edit/1**.</span></span> <span data-ttu-id="abaf8-322">앨범 제목을 **로드** 로 변경 하 고 **저장**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-322">Change the Album title to **Load** and click on **Save**.</span></span> <span data-ttu-id="abaf8-323">앨범의 제목이 실제로 앨범 목록에서 변경 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-323">Verify that album's title actually changed in the list of albums.</span></span>

    <span data-ttu-id="abaf8-324">![앨범 업데이트](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "앨범 업데이트")</span><span class="sxs-lookup"><span data-stu-id="abaf8-324">![Updating an album](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "Updating an album")</span></span>

    <span data-ttu-id="abaf8-325">*앨범 업데이트*</span><span class="sxs-lookup"><span data-stu-id="abaf8-325">*Updating an Album*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Adding_a_Create_View"></a>
### <a name="exercise-4-adding-a-create-view"></a><span data-ttu-id="abaf8-326">연습 4: Create View 추가</span><span class="sxs-lookup"><span data-stu-id="abaf8-326">Exercise 4: Adding a Create View</span></span>

<span data-ttu-id="abaf8-327">이제 **StoreManagerController** **편집** 기능을 지원 하기 때문에이 연습에서는 저장소 관리자가 새 앨범을 응용 프로그램에 추가할 수 있도록 뷰 만들기 템플릿을 추가 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-327">Now that the **StoreManagerController** supports the **Edit** ability, in this exercise you will learn how to add a Create View template to let store managers add new Albums to the application.</span></span>

<span data-ttu-id="abaf8-328">편집 기능을 사용 하는 것 처럼 **StoreManagerController** 클래스 내에서 두 개의 별도 메서드를 사용 하 여 Create 시나리오를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-328">Like you did with the Edit functionality, you will implement the Create scenario using two separate methods within the **StoreManagerController** class:</span></span>

1. <span data-ttu-id="abaf8-329">상점 관리자가 먼저 **/StoreManager/Create** URL을 방문 하는 경우 하나의 작업 메서드가 빈 폼을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-329">One action method will display an empty form when store managers first visit the **/StoreManager/Create** URL.</span></span>
2. <span data-ttu-id="abaf8-330">두 번째 작업 메서드는 저장소 관리자가 양식 내에서 **저장** 단추를 클릭 하 고 값을 다시 **/STOREMANAGER/CREATE** URL에 HTTP POST로 전송 하는 시나리오를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-330">A second action method will handle the scenario where the store manager clicks the **Save** button within the form and submits the values back to the **/StoreManager/Create** URL as an HTTP-POST.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Create_action_method"></a>
#### <a name="task-1---implementing-the-http-get-create-action-method"></a><span data-ttu-id="abaf8-331">작업 1-HTTP-GET 작업 메서드 구현</span><span class="sxs-lookup"><span data-stu-id="abaf8-331">Task 1 - Implementing the HTTP-GET Create action method</span></span>

<span data-ttu-id="abaf8-332">이 작업에서는 Create action 메서드의 HTTP GET 버전을 구현 하 여 모든 장르 및 음악가 목록을 검색 하 고,이 데이터를 **StoreManagerViewModel** 개체에 패키지 하 고,이 데이터를 뷰 템플릿으로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-332">In this task, you will implement the HTTP-GET version of the Create action method to retrieve a list of all Genres and Artists, package this data up into a **StoreManagerViewModel** object, which will then be passed to a View template.</span></span>

1. <span data-ttu-id="abaf8-333">**Source/Ex4-AddingACreateView/begin/** 폴더에 있는 **시작** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-333">Open the **Begin** solution located at **Source/Ex4-AddingACreateView/Begin/** folder.</span></span> <span data-ttu-id="abaf8-334">그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-334">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="abaf8-335">제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-335">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="abaf8-336">이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-336">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="abaf8-337">**NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-337">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="abaf8-338">마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-338">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="abaf8-339">NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-339">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="abaf8-340">NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-340">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="abaf8-341">이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-341">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="abaf8-342">**StoreManagerController** 클래스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-342">Open **StoreManagerController** class.</span></span> <span data-ttu-id="abaf8-343">이렇게 하려면 **Controllers** 폴더를 확장 하 고 **StoreManagerController.cs**를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-343">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="abaf8-344">**만들기** 작업 메서드 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-344">Replace the **Create** action method code with the following:</span></span>

    <span data-ttu-id="abaf8-345">(코드 조각- *ASP.NET MVC 4 도우미 및 폼 및 유효성 검사-Ex4 STOREMANAGERCONTROLLER HTTP-GET 만들기 작업*)</span><span class="sxs-lookup"><span data-stu-id="abaf8-345">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex4 StoreManagerController HTTP-GET Create action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample12.cs)]

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_the_Create_View"></a>
#### <a name="task-2---adding-the-create-view"></a><span data-ttu-id="abaf8-346">작업 2-만들기 뷰 추가</span><span class="sxs-lookup"><span data-stu-id="abaf8-346">Task 2 - Adding the Create View</span></span>

<span data-ttu-id="abaf8-347">이 태스크에서는 새 (비어 있음) 앨범 양식을 표시 하는 뷰 만들기 템플릿을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-347">In this task, you will add the Create View template that will display a new (empty) Album form.</span></span>

1. <span data-ttu-id="abaf8-348">**만들기** 동작 메서드 내부를 마우스 오른쪽 단추로 클릭 하 고 **뷰 추가**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-348">Right-click inside the **Create** action method and select **Add View**.</span></span> <span data-ttu-id="abaf8-349">그러면 보기 추가 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-349">This will bring up the Add View dialog.</span></span>
2. <span data-ttu-id="abaf8-350">보기 추가 대화 상자에서 보기 이름이 **생성**인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-350">In the Add View dialog, verify that the View Name is **Create**.</span></span> <span data-ttu-id="abaf8-351">**강력한 형식의 뷰 만들기** 옵션을 선택 하 고 **모델 클래스** 드롭다운에서 **앨범 (MvcMusicStore)** 을 선택 하 고 **스 캐 폴드 템플릿** 드롭다운에서 **만들기** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-351">Select the **Create a strongly-typed view** option and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down and **Create** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="abaf8-352">다른 필드의 기본값을 그대로 두고 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-352">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="abaf8-353">![Create view 추가](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "adding-a-create-view")</span><span class="sxs-lookup"><span data-stu-id="abaf8-353">![Adding a create view](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "adding-a-create-view.png")</span></span>

    <span data-ttu-id="abaf8-354">*Create View 추가*</span><span class="sxs-lookup"><span data-stu-id="abaf8-354">*Adding the Create View*</span></span>
3. <span data-ttu-id="abaf8-355">아래와 같이 드롭다운 목록을 사용 하도록 **GenreId** 및 **ArtistId** 필드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-355">Update the **GenreId** and **ArtistId** fields to use a drop-down list as shown below:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample13.cshtml)]

<a id="Ex4Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="abaf8-356">작업 3-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="abaf8-356">Task 3 - Running the Application</span></span>

<span data-ttu-id="abaf8-357">이 태스크에서는 **Storemanager** 뷰 **만들기** 페이지에 빈 앨범 양식이 표시 되는 것을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-357">In this task, you will test that the **StoreManager** **Create** View page displays an empty Album form.</span></span>

1. <span data-ttu-id="abaf8-358">**F5** 키를 눌러 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-358">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="abaf8-359">프로젝트가 홈 페이지에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-359">The project starts in the Home page.</span></span> <span data-ttu-id="abaf8-360">URL을 **/StoreManager/Create**로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-360">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="abaf8-361">새 앨범 속성을 채우도록 빈 양식이 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-361">Verify that an empty form is displayed for filling the new Album properties.</span></span>

    <span data-ttu-id="abaf8-362">![빈 폼을 사용 하 여 뷰 만들기](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "빈 폼을 사용 하 여 뷰 만들기")</span><span class="sxs-lookup"><span data-stu-id="abaf8-362">![Create View with an empty form](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "Create View with an empty form")</span></span>

    <span data-ttu-id="abaf8-363">*빈 폼을 사용 하 여 뷰 만들기*</span><span class="sxs-lookup"><span data-stu-id="abaf8-363">*Create View with an empty form*</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_-_Implementing_the_HTTP-POST_Create_Action_Method"></a>
#### <a name="task-4---implementing-the-http-post-create-action-method"></a><span data-ttu-id="abaf8-364">작업 4-HTTP POST 만들기 작업 메서드 구현</span><span class="sxs-lookup"><span data-stu-id="abaf8-364">Task 4 - Implementing the HTTP-POST Create Action Method</span></span>

<span data-ttu-id="abaf8-365">이 작업에서는 사용자가 **저장** 단추를 클릭할 때 호출 되는 Create ACTION 메서드의 HTTP POST 버전을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-365">In this task, you will implement the HTTP-POST version of the Create action method that will be invoked when a user clicks the **Save** button.</span></span> <span data-ttu-id="abaf8-366">메서드는 데이터베이스에 새 앨범을 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-366">The method should save the new album in the database.</span></span>

1. <span data-ttu-id="abaf8-367">필요한 경우 브라우저를 닫고 Visual Studio 창으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-367">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="abaf8-368">**StoreManagerController** 클래스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-368">Open **StoreManagerController** class.</span></span> <span data-ttu-id="abaf8-369">이렇게 하려면 **Controllers** 폴더를 확장 하 고 **StoreManagerController.cs**를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-369">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
2. <span data-ttu-id="abaf8-370">**HTTP-POST 만들기** 작업 메서드 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-370">Replace **HTTP-POST Create** action method code with the following:</span></span>

    <span data-ttu-id="abaf8-371">(코드 조각- *ASP.NET MVC 4 도우미 및 폼 및 유효성 검사-Ex4 STOREMANAGERCONTROLLER HTTP-사후 만들기 작업*)</span><span class="sxs-lookup"><span data-stu-id="abaf8-371">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex4 StoreManagerController HTTP- POST Create action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample14.cs)]

    > [!NOTE]
    > <span data-ttu-id="abaf8-372">만들기 작업은 이전 편집 작업 메서드와 비슷하지만 개체를 수정 된 것으로 설정 하는 대신 컨텍스트에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-372">The Create action is pretty similar to the previous Edit action method but instead of setting the object as modified, it is being added to the context.</span></span>

<a id="Ex4Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="abaf8-373">작업 5-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="abaf8-373">Task 5 - Running the Application</span></span>

<span data-ttu-id="abaf8-374">이 태스크에서는 **storemanager 뷰 만들기** 페이지에서 새 앨범을 만든 다음 Storemanager 인덱스 뷰로 리디렉션하는 테스트를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-374">In this task, you will test that the **StoreManager Create** View page lets you create a new Album and then redirects to the StoreManager Index View.</span></span>

1. <span data-ttu-id="abaf8-375">**F5** 키를 눌러 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-375">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="abaf8-376">프로젝트가 홈 페이지에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-376">The project starts in the Home page.</span></span> <span data-ttu-id="abaf8-377">URL을 **/StoreManager/Create**로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-377">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="abaf8-378">다음 그림에 나와 있는 것 처럼 모든 양식 필드를 새 앨범의 데이터로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-378">Fill all the form fields with data for a new Album, like the one in the following figure:</span></span>

    <span data-ttu-id="abaf8-379">![앨범 만들기](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "앨범 만들기")</span><span class="sxs-lookup"><span data-stu-id="abaf8-379">![Creating an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "Creating an Album")</span></span>

    <span data-ttu-id="abaf8-380">*앨범 만들기*</span><span class="sxs-lookup"><span data-stu-id="abaf8-380">*Creating an Album*</span></span>
3. <span data-ttu-id="abaf8-381">방금 만든 새 앨범이 포함 된 StoreManager 인덱스 뷰로 리디렉션되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-381">Verify that you get redirected to the StoreManager Index View that includes the new Album just created.</span></span>

    <span data-ttu-id="abaf8-382">![새 앨범 만듦](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "새 앨범 만듦")</span><span class="sxs-lookup"><span data-stu-id="abaf8-382">![New Album Created](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "New Album Created")</span></span>

    <span data-ttu-id="abaf8-383">*새 앨범 만듦*</span><span class="sxs-lookup"><span data-stu-id="abaf8-383">*New Album Created*</span></span>

<a id="Exercise5"></a>

<a id="Exercise_5_Handling_Deletion"></a>
### <a name="exercise-5-handling-deletion"></a><span data-ttu-id="abaf8-384">연습 5: 삭제 처리</span><span class="sxs-lookup"><span data-stu-id="abaf8-384">Exercise 5: Handling Deletion</span></span>

<span data-ttu-id="abaf8-385">앨범을 삭제 하는 기능은 아직 구현 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-385">The ability to delete albums is not yet implemented.</span></span> <span data-ttu-id="abaf8-386">이 연습을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-386">This is what this exercise will be about.</span></span> <span data-ttu-id="abaf8-387">이전과 마찬가지로 **StoreManagerController** 클래스 내에서 두 개의 개별 메서드를 사용 하 여 삭제 시나리오를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-387">Like before, you will implement the Delete scenario using two separate methods within the **StoreManagerController** class:</span></span>

1. <span data-ttu-id="abaf8-388">하나의 작업 메서드가 확인 폼을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-388">One action method will display a confirmation form</span></span>
2. <span data-ttu-id="abaf8-389">두 번째 작업 메서드는 폼 제출을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-389">A second action method will handle the form submission</span></span>

<a id="Ex5Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Delete_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-delete-action-method"></a><span data-ttu-id="abaf8-390">작업 1-HTTP-GET 삭제 작업 메서드 구현</span><span class="sxs-lookup"><span data-stu-id="abaf8-390">Task 1 - Implementing the HTTP-GET Delete Action Method</span></span>

<span data-ttu-id="abaf8-391">이 작업에서는 삭제 작업 메서드의 HTTP-GET 버전을 구현 하 여 앨범 정보를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-391">In this task, you will implement the HTTP-GET version of the Delete action method to retrieve the album's information.</span></span>

1. <span data-ttu-id="abaf8-392">**Source/Ex5-HandlingDeletion/begin/** 폴더에 있는 **시작** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-392">Open the **Begin** solution located at **Source/Ex5-HandlingDeletion/Begin/** folder.</span></span> <span data-ttu-id="abaf8-393">그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-393">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="abaf8-394">제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-394">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="abaf8-395">이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-395">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="abaf8-396">**NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-396">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="abaf8-397">마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-397">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="abaf8-398">NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-398">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="abaf8-399">NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-399">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="abaf8-400">이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-400">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="abaf8-401">**StoreManagerController** 클래스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-401">Open **StoreManagerController** class.</span></span> <span data-ttu-id="abaf8-402">이렇게 하려면 **Controllers** 폴더를 확장 하 고 **StoreManagerController.cs**를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-402">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="abaf8-403">컨트롤러 삭제 작업은 이전 저장소 정보 컨트롤러 작업과 동일 합니다. URL에 제공 된 **id** 를 사용 하 여 데이터베이스에서 **앨범** 개체를 쿼리하고 적절 한 **뷰**를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-403">The Delete controller action is exactly the same as the previous Store Details controller action: it queries the **album** object from the database using the **id** provided in the URL and returns the appropriate **View**.</span></span> <span data-ttu-id="abaf8-404">이렇게 하려면 HTTP-GET **Delete** 작업 메서드 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-404">To do this, replace the HTTP-GET **Delete** action method code with the following:</span></span>

    <span data-ttu-id="abaf8-405">(코드 조각- *ASP.NET MVC 4 도우미 및 폼 및 유효성 검사-Ex5 처리 삭제 HTTP-삭제 작업 가져오기*)</span><span class="sxs-lookup"><span data-stu-id="abaf8-405">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex5 Handling Deletion HTTP-GET Delete action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample15.cs)]
4. <span data-ttu-id="abaf8-406">**Delete** 동작 메서드 내부를 마우스 오른쪽 단추로 클릭 하 고 **뷰 추가**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-406">Right-click inside the **Delete** action method and select **Add View**.</span></span> <span data-ttu-id="abaf8-407">그러면 보기 추가 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-407">This will bring up the Add View dialog.</span></span>
5. <span data-ttu-id="abaf8-408">보기 추가 대화 상자에서 뷰 이름이 **삭제**인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-408">In the Add View dialog, verify that the View name is **Delete**.</span></span> <span data-ttu-id="abaf8-409">**강력한 형식의 뷰 만들기** 옵션을 선택 하 고 **모델 클래스** 드롭다운에서 **앨범 (MvcMusicStore)** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-409">Select the **Create a strongly-typed view** option and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down.</span></span> <span data-ttu-id="abaf8-410">**스 캐 폴드 템플릿** 드롭다운에서 **삭제** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-410">Select **Delete** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="abaf8-411">다른 필드의 기본값을 그대로 두고 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-411">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="abaf8-412">![삭제 뷰 추가](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "삭제 뷰 추가")</span><span class="sxs-lookup"><span data-stu-id="abaf8-412">![Adding a Delete View](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "Adding a Delete View")</span></span>

    <span data-ttu-id="abaf8-413">*삭제 뷰 추가*</span><span class="sxs-lookup"><span data-stu-id="abaf8-413">*Adding a Delete View*</span></span>
6. <span data-ttu-id="abaf8-414">삭제 템플릿은 모델의 모든 필드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-414">The Delete template shows all the fields from the model.</span></span> <span data-ttu-id="abaf8-415">앨범의 제목만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-415">You will show only the album's title.</span></span> <span data-ttu-id="abaf8-416">이렇게 하려면 뷰의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-416">To do this, replace the content of the view with the following code:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample16.cshtml)]

<a id="Ex05Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="abaf8-417">작업 2-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="abaf8-417">Task 2 - Running the Application</span></span>

<span data-ttu-id="abaf8-418">이 태스크에서는 **Storemanager** 뷰 **삭제** 페이지에 확인 삭제 양식이 표시 되는 것을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-418">In this task, you will test that the **StoreManager** **Delete** View page displays a confirmation deletion form.</span></span>

1. <span data-ttu-id="abaf8-419">**F5** 키를 눌러 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-419">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="abaf8-420">프로젝트가 홈 페이지에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-420">The project starts in the Home page.</span></span> <span data-ttu-id="abaf8-421">URL을 **/Storemanager**로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-421">Change the URL to **/StoreManager**.</span></span> <span data-ttu-id="abaf8-422">**삭제** 를 클릭 하 여 삭제할 앨범을 하나 선택 하 고 새 보기가 업로드 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-422">Select one album to delete by clicking **Delete** and verify that the new view is uploaded.</span></span>

    <span data-ttu-id="abaf8-423">![앨범 삭제](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "앨범 삭제")</span><span class="sxs-lookup"><span data-stu-id="abaf8-423">![Deleting an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "Deleting an Album")</span></span>

    <span data-ttu-id="abaf8-424">*앨범 삭제*</span><span class="sxs-lookup"><span data-stu-id="abaf8-424">*Deleting an Album*</span></span>

<a id="Ex05Task3"></a>

<a id="Task_3-_Implementing_the_HTTP-POST_Delete_Action_Method"></a>
#### <a name="task-3--implementing-the-http-post-delete-action-method"></a><span data-ttu-id="abaf8-425">작업 3-HTTP-사후 삭제 작업 메서드 구현</span><span class="sxs-lookup"><span data-stu-id="abaf8-425">Task 3- Implementing the HTTP-POST Delete Action Method</span></span>

<span data-ttu-id="abaf8-426">이 작업에서는 사용자가 **삭제** 단추를 클릭할 때 호출 되는 delete 동작 메서드의 HTTP POST 버전을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-426">In this task, you will implement the HTTP-POST version of the Delete action method that will be invoked when a user clicks the **Delete** button.</span></span> <span data-ttu-id="abaf8-427">메서드는 데이터베이스의 앨범을 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-427">The method should delete the album in the database.</span></span>

1. <span data-ttu-id="abaf8-428">필요한 경우 브라우저를 닫고 Visual Studio 창으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-428">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="abaf8-429">**StoreManagerController** 클래스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-429">Open **StoreManagerController** class.</span></span> <span data-ttu-id="abaf8-430">이렇게 하려면 **Controllers** 폴더를 확장 하 고 **StoreManagerController.cs**를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-430">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
2. <span data-ttu-id="abaf8-431">**HTTP-사후 삭제** 작업 메서드 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-431">Replace **HTTP-POST Delete** action method code with the following:</span></span>

    <span data-ttu-id="abaf8-432">(코드 조각- *ASP.NET MVC 4 도우미 및 폼 및 유효성 검사-Ex5 처리 삭제 HTTP-사후 삭제 작업*)</span><span class="sxs-lookup"><span data-stu-id="abaf8-432">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex5 Handling Deletion HTTP-POST Delete action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample17.cs)]

<a id="Ex5Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="abaf8-433">작업 4-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="abaf8-433">Task 4 - Running the Application</span></span>

<span data-ttu-id="abaf8-434">이 태스크에서는 **storemanager 뷰 삭제** 페이지를 사용 하 여 앨범을 삭제 한 다음 Storemanager 인덱스 뷰로 리디렉션하는 것을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-434">In this task, you will test that the **StoreManager Delete** View page lets you delete an Album and then redirects to the StoreManager Index View.</span></span>

1. <span data-ttu-id="abaf8-435">**F5** 키를 눌러 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-435">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="abaf8-436">프로젝트가 홈 페이지에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-436">The project starts in the Home page.</span></span> <span data-ttu-id="abaf8-437">URL을 **/Storemanager**로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-437">Change the URL to **/StoreManager**.</span></span> <span data-ttu-id="abaf8-438">삭제를 클릭 하 여 삭제할 앨범 하나를 선택 **합니다.**</span><span class="sxs-lookup"><span data-stu-id="abaf8-438">Select one album to delete by clicking **Delete.**</span></span> <span data-ttu-id="abaf8-439">**삭제** 단추를 클릭 하 여 삭제를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-439">Confirm the deletion by clicking **Delete** button:</span></span>

    <span data-ttu-id="abaf8-440">![앨범 삭제](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "앨범 삭제")</span><span class="sxs-lookup"><span data-stu-id="abaf8-440">![Deleting an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "Deleting an Album")</span></span>

    <span data-ttu-id="abaf8-441">*앨범 삭제*</span><span class="sxs-lookup"><span data-stu-id="abaf8-441">*Deleting an Album*</span></span>
3. <span data-ttu-id="abaf8-442">앨범이 **인덱스** 페이지에 나타나지 않으므로 삭제 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-442">Verify that the album was deleted since it does not appear in the **Index** page.</span></span>

<a id="Exercise6"></a>

<a id="Exercise_6_Adding_Validation"></a>
### <a name="exercise-6-adding-validation"></a><span data-ttu-id="abaf8-443">연습 6: 유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="abaf8-443">Exercise 6: Adding Validation</span></span>

<span data-ttu-id="abaf8-444">현재 보유 하 고 있는 양식 만들기 및 편집은 어떤 종류의 유효성 검사도 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-444">Currently, the Create and Edit forms you have in place do not perform any kind of validation.</span></span> <span data-ttu-id="abaf8-445">사용자가 필수 필드를 비워 두고 price 필드에 문자를 입력 하는 경우 첫 번째 오류는 데이터베이스에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-445">If the user leaves a required field blank or type letters in the price field, the first error you will get will be from the database.</span></span>

<span data-ttu-id="abaf8-446">모델 클래스에 데이터 주석을 추가 하 여 응용 프로그램에 유효성 검사를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-446">You can add validation to the application by adding Data Annotations to your model class.</span></span> <span data-ttu-id="abaf8-447">데이터 주석을 사용 하면 모델 속성에 적용 하려는 규칙을 설명할 수 있으며, ASP.NET MVC는 사용자에 게 적절 한 메시지를 적용 하 고 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-447">Data Annotations allow describing the rules you want applied to your model properties, and ASP.NET MVC will take care of enforcing and displaying appropriate message to users.</span></span>

<a id="Ex06Task1"></a>

<a id="Task_1_-_Adding_Data_Annotations"></a>
#### <a name="task-1---adding-data-annotations"></a><span data-ttu-id="abaf8-448">작업 1-데이터 주석 추가</span><span class="sxs-lookup"><span data-stu-id="abaf8-448">Task 1 - Adding Data Annotations</span></span>

<span data-ttu-id="abaf8-449">이 태스크에서는 적절 한 경우 만들기 및 편집 페이지 표시 유효성 검사 메시지를 만드는 앨범 모델에 데이터 주석을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-449">In this task, you will add Data Annotations to the Album Model that will make the Create and Edit page display validation messages when appropriate.</span></span>

<span data-ttu-id="abaf8-450">간단한 모델 클래스의 경우에는 **system.componentmodel**에 대 한 **using** 문을 추가 하 고 적절 한 속성에 **[Required]** 특성을 배치 하 여 데이터 주석을 추가 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-450">For a simple Model class, adding a Data Annotation is just handled by adding a **using** statement for **System.ComponentModel.DataAnnotation**, then placing a **[Required]** attribute on the appropriate properties.</span></span> <span data-ttu-id="abaf8-451">다음 예에서는 **이름** 속성을 뷰의 필수 필드로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-451">The following example would make the **Name** property a required field in the View.</span></span>

[!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample18.cs)]

<span data-ttu-id="abaf8-452">이 응용 프로그램이 엔터티 데이터 모델를 생성 하는 경우에는이 응용 프로그램이 좀 더 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-452">This is a little more complex in cases like this application where the Entity Data Model is generated.</span></span> <span data-ttu-id="abaf8-453">모델 클래스에 직접 데이터 주석을 추가한 경우 데이터베이스에서 모델을 업데이트 하면 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-453">If you added Data Annotations directly to the model classes, they would be overwritten if you update the model from the database.</span></span> <span data-ttu-id="abaf8-454">대신 주석을 보유 하기 위해 존재 하 고 **[MetadataType]** 특성을 사용 하 여 모델 클래스와 연결 된 메타 데이터 부분 클래스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-454">Instead, you can make use of metadata partial classes which will exist to hold the annotations and are associated with the model classes using the **[MetadataType]** attribute.</span></span>

1. <span data-ttu-id="abaf8-455">**Source/Ex6-AddingValidation/begin/** 폴더에 있는 **시작** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-455">Open the **Begin** solution located at **Source/Ex6-AddingValidation/Begin/** folder.</span></span> <span data-ttu-id="abaf8-456">그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-456">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="abaf8-457">제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-457">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="abaf8-458">이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-458">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="abaf8-459">**NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-459">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="abaf8-460">마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-460">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="abaf8-461">NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-461">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="abaf8-462">NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-462">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="abaf8-463">이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-463">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="abaf8-464">**모델** 폴더에서 **Album.cs** 을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-464">Open the **Album.cs** from the **Models** folder.</span></span>
3. <span data-ttu-id="abaf8-465">**Album.cs** 콘텐츠를 강조 표시 된 코드로 대체 하 여 다음과 같이 표시 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-465">Replace **Album.cs** content with the highlighted code, so that it looks like the following:</span></span>

    > [!NOTE]
    > <span data-ttu-id="abaf8-466">**[Displayformat (ConvertEmptyStringToNull = false)]** 줄은 데이터 원본에서 데이터 필드가 업데이트 될 때 모델의 빈 문자열이 null로 변환 되지 않음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-466">The line **[DisplayFormat(ConvertEmptyStringToNull=false)]** indicates that empty strings from the model won't be converted to null when the data field is updated in the data source.</span></span> <span data-ttu-id="abaf8-467">이 설정은 데이터 주석이 필드의 유효성을 검사 하기 전에 Entity Framework에서 모델에 null 값을 할당 하는 경우 예외를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-467">This setting will avoid an exception when the Entity Framework assigns null values to the model before Data Annotation validates the fields.</span></span>

    <span data-ttu-id="abaf8-468">(코드 조각- *ASP.NET MVC 4 도우미 및 폼 및 유효성 검사-Ex6 앨범 메타 데이터 partial 클래스*)</span><span class="sxs-lookup"><span data-stu-id="abaf8-468">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex6 Album metadata partial class*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample19.cs)]

    > [!NOTE]
    > <span data-ttu-id="abaf8-469">이 **앨범** 부분 클래스에는 데이터 주석의 **AlbumMetaData** 클래스를 가리키는 **MetadataType** 특성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-469">This **Album** partial class has a **MetadataType** attribute which points to the **AlbumMetaData** class for the Data Annotations.</span></span> <span data-ttu-id="abaf8-470">앨범 모델에 주석을 추가 하는 데 사용 하는 데이터 주석 특성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-470">These are some of the Data Annotation attributes you are using to annotate the Album model:</span></span>
    > 
    > - <span data-ttu-id="abaf8-471">필수-속성이 필수 필드 임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-471">Required - Indicates that the property is a required field</span></span>
    > - <span data-ttu-id="abaf8-472">DisplayName-양식 필드 및 유효성 검사 메시지에 사용할 텍스트를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-472">DisplayName - Defines the text to be used on form fields and validation messages</span></span>
    > - <span data-ttu-id="abaf8-473">DisplayFormat-데이터 필드를 표시 하 고 서식을 지정 하는 방법을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-473">DisplayFormat - Specifies how data fields are displayed and formatted.</span></span>
    > - <span data-ttu-id="abaf8-474">StringLength-문자열 필드의 최대 길이를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-474">StringLength - Defines a maximum length for a string field</span></span>
    > - <span data-ttu-id="abaf8-475">범위-숫자 필드에 대 한 최대값 및 최소값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-475">Range - Gives a maximum and minimum value for a numeric field</span></span>
    > - <span data-ttu-id="abaf8-476">ScaffoldColumn-편집기 양식에서 필드를 숨길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-476">ScaffoldColumn - Allows hiding fields from editor forms</span></span>

<a id="Ex06Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="abaf8-477">작업 2-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="abaf8-477">Task 2 - Running the Application</span></span>

<span data-ttu-id="abaf8-478">이 태스크에서는 마지막 작업에서 선택한 표시 이름을 사용 하 여 페이지 만들기 및 편집 페이지의 유효성을 검사 하는 방법을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-478">In this task, you will test that the Create and Edit pages validate fields, using the display names chosen in the last task.</span></span>

1. <span data-ttu-id="abaf8-479">**F5** 키를 눌러 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-479">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="abaf8-480">프로젝트가 홈 페이지에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-480">The project starts in the Home page.</span></span> <span data-ttu-id="abaf8-481">URL을 **/StoreManager/Create**로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-481">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="abaf8-482">표시 이름이 partial 클래스의 이름과 일치 하는지 확인 합니다 (예: **AlbumArtUrl**대신 **앨범 아트 URL** ).</span><span class="sxs-lookup"><span data-stu-id="abaf8-482">Verify that the display names match the ones in the partial class (like **Album Art URL** instead of **AlbumArtUrl**)</span></span>
3. <span data-ttu-id="abaf8-483">양식을 채우지 않고 **만들기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-483">Click **Create**, without filling the form.</span></span> <span data-ttu-id="abaf8-484">해당 유효성 검사 메시지가 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-484">Verify that you get the corresponding validation messages.</span></span>

    <span data-ttu-id="abaf8-485">![만들기 페이지의 유효성을 검사 한 필드](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "만들기 페이지의 유효성을 검사 한 필드")</span><span class="sxs-lookup"><span data-stu-id="abaf8-485">![Validated fields in the Create page](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "Validated fields in the Create page")</span></span>

    <span data-ttu-id="abaf8-486">*만들기 페이지의 유효성을 검사 한 필드*</span><span class="sxs-lookup"><span data-stu-id="abaf8-486">*Validated fields in the Create page*</span></span>
4. <span data-ttu-id="abaf8-487">**편집** 페이지에서 동일한가 발생 하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-487">You can verify that the same occurs with the **Edit** page.</span></span> <span data-ttu-id="abaf8-488">URL을 **/StoreManager/Edit/1** 로 변경 하 고 표시 이름이 부분 클래스 (예: **AlbumArtUrl**대신 **앨범 아트 URL** )의 이름과 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-488">Change the URL to **/StoreManager/Edit/1** and verify that the display names match the ones in the partial class (like **Album Art URL** instead of **AlbumArtUrl**).</span></span> <span data-ttu-id="abaf8-489">**제목** 및 **가격** 필드를 비운 후 **저장**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-489">Empty the **Title** and **Price** fields and click **Save**.</span></span> <span data-ttu-id="abaf8-490">해당 유효성 검사 메시지가 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-490">Verify that you get the corresponding validation messages.</span></span>

    ![편집 페이지의 유효성을 검사 한 필드](aspnet-mvc-4-helpers-forms-and-validation/_static/image19.png)

    <span data-ttu-id="abaf8-492">*편집 페이지의 유효성을 검사 한 필드*</span><span class="sxs-lookup"><span data-stu-id="abaf8-492">*Validated fields in the Edit page*</span></span>

<a id="Exercise7"></a>

<a id="Exercise_7_Using_Unobtrusive_jQuery_at_Client_Side"></a>
### <a name="exercise-7-using-unobtrusive-jquery-at-client-side"></a><span data-ttu-id="abaf8-493">연습 7: 클라이언트 쪽에서 조심 스럽게 jQuery 사용</span><span class="sxs-lookup"><span data-stu-id="abaf8-493">Exercise 7: Using Unobtrusive jQuery at Client Side</span></span>

<span data-ttu-id="abaf8-494">이 연습에서는 클라이언트 쪽에서 MVC 4를 사용 하지 않는 jQuery 유효성 검사를 사용 하도록 설정 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-494">In this exercise, you will learn how to enable MVC 4 Unobtrusive jQuery validation at client side.</span></span>

> [!NOTE]
> <span data-ttu-id="abaf8-495">조심 스럽게 jQuery는 데이터 ajax 접두사 JavaScript를 사용 하 여 인라인 클라이언트 스크립트를 intrusively 내보내는 대신 서버에서 작업 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-495">The Unobtrusive jQuery uses data-ajax prefix JavaScript to invoke action methods on the server rather than intrusively emitting inline client scripts.</span></span>

<a id="Ex7Task1"></a>

<a id="Task_1_-_Running_the_Application_before_Enabling_Unobtrusive_jQuery"></a>
#### <a name="task-1---running-the-application-before-enabling-unobtrusive-jquery"></a><span data-ttu-id="abaf8-496">작업 1-방해 하지 않는 jQuery를 사용 하도록 설정 하기 전에 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="abaf8-496">Task 1 - Running the Application before Enabling Unobtrusive jQuery</span></span>

<span data-ttu-id="abaf8-497">이 태스크에서는 jQuery를 포함 하기 전에 응용 프로그램을 실행 하 여 두 유효성 검사 모델을 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-497">In this task, you will run the application before including jQuery in order to compare both validation models.</span></span>

1. <span data-ttu-id="abaf8-498">**Source/Ex7-UnobtrusivejQueryValidation/begin/** 폴더에 있는 **시작** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-498">Open the **Begin** solution located at **Source/Ex7-UnobtrusivejQueryValidation/Begin/** folder.</span></span> <span data-ttu-id="abaf8-499">그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-499">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="abaf8-500">제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-500">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="abaf8-501">이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-501">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="abaf8-502">**NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-502">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="abaf8-503">마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-503">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="abaf8-504">NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-504">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="abaf8-505">NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-505">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="abaf8-506">이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-506">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="abaf8-507">**F5** 키를 눌러 애플리케이션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-507">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="abaf8-508">프로젝트가 홈 페이지에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-508">The project starts in the Home page.</span></span> <span data-ttu-id="abaf8-509">**/StoreManager/Create** 를 찾아보고 폼을 채우지 않고 **만들기** 를 클릭 하 여 유효성 검사 메시지를 수신 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-509">Browse **/StoreManager/Create** and click **Create** without filling the form to verify that you get validation messages:</span></span>

    <span data-ttu-id="abaf8-510">![클라이언트 유효성 검사 사용 안 함](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "클라이언트 유효성 검사 사용 안 함")</span><span class="sxs-lookup"><span data-stu-id="abaf8-510">![Client validation disabled](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "Client validation disabled")</span></span>

    <span data-ttu-id="abaf8-511">*클라이언트 유효성 검사 사용 안 함*</span><span class="sxs-lookup"><span data-stu-id="abaf8-511">*Client validation disabled*</span></span>
4. <span data-ttu-id="abaf8-512">브라우저에서 HTML 소스 코드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-512">In the browser, open the HTML source code:</span></span>

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample20.html)]

<a id="Ex7Task2"></a>

<a id="Task_2_-_Enabling_Unobtrusive_Client_Validation"></a>
#### <a name="task-2---enabling-unobtrusive-client-validation"></a><span data-ttu-id="abaf8-513">작업 2-비 클라이언트 유효성 검사 사용</span><span class="sxs-lookup"><span data-stu-id="abaf8-513">Task 2 - Enabling Unobtrusive Client Validation</span></span>

<span data-ttu-id="abaf8-514">이 태스크에서는 **web.config** 파일에서 jQuery를 사용 하지 않는 **클라이언트 유효성 검사** 를 사용 하도록 설정 합니다 .이는 기본적으로 모든 새 ASP.NET MVC 4 프로젝트에서 false로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-514">In this task, you will enable jQuery **unobtrusive client validation** from **Web.config** file, which is by default set to false in all new ASP.NET MVC 4 projects.</span></span> <span data-ttu-id="abaf8-515">또한 jQuery를 사용 하지 않는 클라이언트 유효성 검사 작업을 수행 하는 데 필요한 스크립트 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-515">Additionally, you will add the necessary scripts references to make jQuery Unobtrusive Client Validation work.</span></span>

1. <span data-ttu-id="abaf8-516">프로젝트 루트에서 **web.config** 파일을 열고 **clientvalidationenabled** 및 **UnobtrusiveJavaScriptEnabled** keys 값이 **true**로 설정 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-516">Open **Web.Config** file at project root, and make sure that the **ClientValidationEnabled** and **UnobtrusiveJavaScriptEnabled** keys values are set to **true**.</span></span>

    [!code-xml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample21.xml)]

    > [!NOTE]
    > <span data-ttu-id="abaf8-517">Global.asax.cs에서 코드에의 한 클라이언트 유효성 검사를 사용 하도록 설정 하 여 동일한 결과를 얻을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-517">You can also enable client validation by code at Global.asax.cs to get the same results:</span></span>
    > 
    > <span data-ttu-id="abaf8-518">**HtmlHelper. ClientValidationEnabled = true;**</span><span class="sxs-lookup"><span data-stu-id="abaf8-518">**HtmlHelper.ClientValidationEnabled = true;**</span></span>
    > 
    > <span data-ttu-id="abaf8-519">또한 모든 컨트롤러에 ClientValidationEnabled 특성을 할당 하 여 사용자 지정 동작을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-519">Additionally, you can assign ClientValidationEnabled attribute into any controller to have a custom behavior.</span></span>
2. <span data-ttu-id="abaf8-520">**Views\StoreManager**에서 **Create. cshtml** 를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-520">Open **Create.cshtml** at **Views\StoreManager**.</span></span>
3. <span data-ttu-id="abaf8-521">다음 스크립트 파일 **jquery. validate** 및 **jquery.** **/bundles/jqueryval**&quot; 번들을 &quot;통해 뷰에서 참조 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-521">Make sure the following script files, **jquery.validate** and **jquery.validate.unobtrusive**, are referenced in the view through the &quot;**~/bundles/jqueryval**&quot; bundle.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample22.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="abaf8-522">이러한 모든 jQuery 라이브러리는 MVC 4 새 프로젝트에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-522">All these jQuery libraries are included in MVC 4 new projects.</span></span> <span data-ttu-id="abaf8-523">프로젝트의 **/Scripts** 폴더에서 더 많은 라이브러리를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-523">You can find more libraries in the **/Scripts** folder of you project.</span></span>
    > 
    > <span data-ttu-id="abaf8-524">이 유효성 검사 라이브러리를 작동 시키려면 jQuery 프레임 워크 라이브러리에 대 한 참조를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-524">In order to make this validation libraries work, you need to add a reference to the jQuery framework library.</span></span> <span data-ttu-id="abaf8-525">이 참조는 이미 **\_레이아웃. cshtml** 파일에 추가 되었으므로이 특정 뷰에 추가할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-525">Since this reference is already added in the **\_Layout.cshtml** file, you do not need to add it in this particular view.</span></span>

<a id="Ex7Task3"></a>

<a id="Task_3_-_Running_the_Application_Using_Unobtrusive_jQuery_Validation"></a>
#### <a name="task-3---running-the-application-using-unobtrusive-jquery-validation"></a><span data-ttu-id="abaf8-526">작업 3-방해 되지 않는 jQuery 유효성 검사를 사용 하 여 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="abaf8-526">Task 3 - Running the Application Using Unobtrusive jQuery Validation</span></span>

<span data-ttu-id="abaf8-527">이 태스크에서는 사용자가 새 앨범을 만들 때 **Storemanager** create View 템플릿이 jQuery 라이브러리를 사용 하 여 클라이언트 쪽 유효성 검사를 수행 하는지 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-527">In this task, you will test that the **StoreManager** create view template performs client side validation using jQuery libraries when the user creates a new album.</span></span>

1. <span data-ttu-id="abaf8-528">**F5** 키를 눌러 애플리케이션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-528">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="abaf8-529">프로젝트가 홈 페이지에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-529">The project starts in the Home page.</span></span> <span data-ttu-id="abaf8-530">**/StoreManager/Create** 를 찾아보고 폼을 채우지 않고 **만들기** 를 클릭 하 여 유효성 검사 메시지를 수신 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-530">Browse **/StoreManager/Create** and click **Create** without filling the form to verify that you get validation messages:</span></span>

    <span data-ttu-id="abaf8-531">![JQuery를 사용 하 여 클라이언트 유효성 검사 사용](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "JQuery를 사용 하 여 클라이언트 유효성 검사 사용")</span><span class="sxs-lookup"><span data-stu-id="abaf8-531">![Client validation with jQuery enabled](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "Client validation with jQuery enabled")</span></span>

    <span data-ttu-id="abaf8-532">*JQuery를 사용 하 여 클라이언트 유효성 검사 사용*</span><span class="sxs-lookup"><span data-stu-id="abaf8-532">*Client validation with jQuery enabled*</span></span>
3. <span data-ttu-id="abaf8-533">브라우저에서 뷰 만들기에 대 한 소스 코드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-533">In the browser, open the source code for Create view:</span></span>

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample23.html)]

   > [!NOTE]
   > <span data-ttu-id="abaf8-534">각 클라이언트 유효성 검사 규칙에 대해*rulename*=&quot;*메시지*&quot;특성이 있는 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-534">For each client validation rule, Unobtrusive jQuery adds an attribute with data-val-*rulename*=&quot;*message*&quot;.</span></span> <span data-ttu-id="abaf8-535">다음은 클라이언트 유효성 검사를 수행 하기 위해 html 입력 필드에 삽입 하지 않는 태그의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-535">Below is a list of tags that Unobtrusive jQuery inserts into the html input field to perform client validation:</span></span>
   > 
   > - <span data-ttu-id="abaf8-536">데이터-val</span><span class="sxs-lookup"><span data-stu-id="abaf8-536">Data-val</span></span>
   > - <span data-ttu-id="abaf8-537">Data-val-number</span><span class="sxs-lookup"><span data-stu-id="abaf8-537">Data-val-number</span></span>
   > - <span data-ttu-id="abaf8-538">데이터-val 범위</span><span class="sxs-lookup"><span data-stu-id="abaf8-538">Data-val-range</span></span>
   > - <span data-ttu-id="abaf8-539">데이터-val 범위-min/Data-val-range-max</span><span class="sxs-lookup"><span data-stu-id="abaf8-539">Data-val-range-min / Data-val-range-max</span></span>
   > - <span data-ttu-id="abaf8-540">Data-val-필수</span><span class="sxs-lookup"><span data-stu-id="abaf8-540">Data-val-required</span></span>
   > - <span data-ttu-id="abaf8-541">데이터-val 길이</span><span class="sxs-lookup"><span data-stu-id="abaf8-541">Data-val-length</span></span>
   > - <span data-ttu-id="abaf8-542">Data-val-length-max/Data-val-length-min</span><span class="sxs-lookup"><span data-stu-id="abaf8-542">Data-val-length-max / Data-val-length-min</span></span>
   > 
   > <span data-ttu-id="abaf8-543">모든 데이터 값은 모델 **데이터 주석**으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-543">All the data values are filled with model **Data Annotation**.</span></span> <span data-ttu-id="abaf8-544">그런 다음 서버 쪽에서 작동 하는 모든 논리를 클라이언트 쪽에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-544">Then, all the logic that works at server side can be run at client side.</span></span> <span data-ttu-id="abaf8-545">예를 들어 Price 특성은 모델에 다음과 같은 데이터 주석을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-545">For example, Price attribute has the following data annotation in the model:</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample24.cs)]
   > 
   > <span data-ttu-id="abaf8-546">비-jQuery를 사용한 후 생성 된 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-546">After using Unobtrusive jQuery, the generated code is:</span></span>
   > 
   > [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample25.html)]

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="abaf8-547">요약</span><span class="sxs-lookup"><span data-stu-id="abaf8-547">Summary</span></span>

<span data-ttu-id="abaf8-548">이 실습 실습을 완료 하면 다음을 사용 하 여 사용자가 데이터베이스에 저장 된 데이터를 변경할 수 있도록 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-548">By completing this Hands-On Lab you have learned how to enable users to change the data stored in the database with the use of the following:</span></span>

- <span data-ttu-id="abaf8-549">인덱스, 만들기, 편집, 삭제 등의 컨트롤러 작업</span><span class="sxs-lookup"><span data-stu-id="abaf8-549">Controller actions like Index, Create, Edit, Delete</span></span>
- <span data-ttu-id="abaf8-550">HTML 테이블에 속성을 표시 하기 위한 ASP.NET MVC의 스 캐 폴딩 기능</span><span class="sxs-lookup"><span data-stu-id="abaf8-550">ASP.NET MVC's scaffolding feature for displaying properties in an HTML table</span></span>
- <span data-ttu-id="abaf8-551">사용자 환경을 개선 하기 위한 사용자 지정 HTML 도우미</span><span class="sxs-lookup"><span data-stu-id="abaf8-551">Custom HTML helpers to improve user experience</span></span>
- <span data-ttu-id="abaf8-552">HTTP GET 또는 HTTP POST 호출에 반응 하는 작업 메서드</span><span class="sxs-lookup"><span data-stu-id="abaf8-552">Action methods that react to either HTTP-GET or HTTP-POST calls</span></span>
- <span data-ttu-id="abaf8-553">만들기 및 편집 같은 유사한 보기 템플릿에 대 한 공유 편집기 템플릿</span><span class="sxs-lookup"><span data-stu-id="abaf8-553">A shared editor template for similar View templates like Create and Edit</span></span>
- <span data-ttu-id="abaf8-554">드롭다운 같은 폼 요소</span><span class="sxs-lookup"><span data-stu-id="abaf8-554">Form elements like drop-downs</span></span>
- <span data-ttu-id="abaf8-555">모델 유효성 검사에 대 한 데이터 주석</span><span class="sxs-lookup"><span data-stu-id="abaf8-555">Data annotations for Model validation</span></span>
- <span data-ttu-id="abaf8-556">JQuery를 사용 하지 않는 라이브러리를 사용 하 여 클라이언트 쪽 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="abaf8-556">Client Side Validation using jQuery Unobtrusive library</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="abaf8-557">부록 A: 웹에 대 한 Visual Studio Express 2012 설치</span><span class="sxs-lookup"><span data-stu-id="abaf8-557">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="abaf8-558">**[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)** 를 사용 하 여 웹 또는 다른 &quot;Express&quot; 버전 **에 대해 Microsoft Visual Studio Express 2012** 를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-558">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="abaf8-559">다음 지침에서는 *Microsoft 웹 플랫폼 설치 관리자*를 사용 하 여 *Visual studio Express 2012 for Web* 을 설치 하는 데 필요한 단계를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-559">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="abaf8-560">[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-560">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="abaf8-561">또는 웹 플랫폼 설치 관리자를 이미 설치한 경우에는 웹 플랫폼 설치 관리자를 열고 <em>Microsoft AZURE SDK&quot;를 사용 하 여 웹 용 2012 Visual Studio Express</em> &quot;제품을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-561">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="abaf8-562">**지금 설치**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-562">Click on **Install Now**.</span></span> <span data-ttu-id="abaf8-563">**웹 플랫폼 설치 관리자** 가 없으면 먼저이를 다운로드 하 여 설치 하도록 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-563">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="abaf8-564">**웹 플랫폼 설치 관리자** 가 열리면 **설치** 를 클릭 하 여 설치를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-564">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="abaf8-565">![Visual Studio Express 설치](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "Visual Studio Express 설치")</span><span class="sxs-lookup"><span data-stu-id="abaf8-565">![Install Visual Studio Express](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="abaf8-566">*Visual Studio Express 설치*</span><span class="sxs-lookup"><span data-stu-id="abaf8-566">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="abaf8-567">모든 제품의 라이선스 및 사용 조건을 읽고 **동의** 함을 클릭 하 여 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-567">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![사용 조건 동의](aspnet-mvc-4-helpers-forms-and-validation/_static/image23.png)

    <span data-ttu-id="abaf8-569">*사용 조건 동의*</span><span class="sxs-lookup"><span data-stu-id="abaf8-569">*Accepting the license terms*</span></span>
5. <span data-ttu-id="abaf8-570">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-570">Wait until the downloading and installation process completes.</span></span>

    ![설치 진행률](aspnet-mvc-4-helpers-forms-and-validation/_static/image24.png)

    <span data-ttu-id="abaf8-572">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="abaf8-572">*Installation progress*</span></span>
6. <span data-ttu-id="abaf8-573">설치가 완료 되 면 **마침**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-573">When the installation completes, click **Finish**.</span></span>

    ![설치 완료](aspnet-mvc-4-helpers-forms-and-validation/_static/image25.png)

    <span data-ttu-id="abaf8-575">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="abaf8-575">*Installation completed*</span></span>
7. <span data-ttu-id="abaf8-576">**끝내기** 를 클릭 하 여 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-576">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="abaf8-577">웹에 대 한 Visual Studio Express를 열려면 **시작** 화면으로 이동 하 &quot;**VS Express**&quot;작성을 시작한 후 **VS Express for Web** 타일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-577">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 타일](aspnet-mvc-4-helpers-forms-and-validation/_static/image26.png)

    <span data-ttu-id="abaf8-579">*VS Express for Web 타일*</span><span class="sxs-lookup"><span data-stu-id="abaf8-579">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="abaf8-580">부록 B: 코드 조각 사용</span><span class="sxs-lookup"><span data-stu-id="abaf8-580">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="abaf8-581">코드 조각을 사용 하면 필요한 모든 코드를 편리 하 게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-581">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="abaf8-582">랩 문서는 다음 그림에 표시 된 것 처럼 사용자가 사용할 수 있는 경우를 정확 하 게 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-582">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="abaf8-583">![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입")</span><span class="sxs-lookup"><span data-stu-id="abaf8-583">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="abaf8-584">*Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입*</span><span class="sxs-lookup"><span data-stu-id="abaf8-584">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="abaf8-585">***키보드를 사용 하 여 코드 조각을 추가 하려면C# (만 해당)***</span><span class="sxs-lookup"><span data-stu-id="abaf8-585">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="abaf8-586">코드를 삽입할 위치에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-586">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="abaf8-587">조각 이름 (공백 또는 하이픈 제외)을 입력 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-587">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="abaf8-588">IntelliSense는 일치 하는 코드 조각의 이름을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-588">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="abaf8-589">올바른 코드 조각을 선택 하거나 전체 코드 조각 이름이 선택 될 때까지 계속 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-589">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="abaf8-590">Tab 키를 두 번 눌러 커서 위치에 코드 조각을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-590">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="abaf8-591">![코드 조각 이름 입력 시작](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "코드 조각 이름 입력 시작")</span><span class="sxs-lookup"><span data-stu-id="abaf8-591">![Start typing the snippet name](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "Start typing the snippet name")</span></span>

<span data-ttu-id="abaf8-592">*코드 조각 이름 입력 시작*</span><span class="sxs-lookup"><span data-stu-id="abaf8-592">*Start typing the snippet name*</span></span>

<span data-ttu-id="abaf8-593">![Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="abaf8-593">![Press Tab to select the highlighted snippet](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="abaf8-594">*Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="abaf8-594">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="abaf8-595">![Tab 키를 다시 누르면 코드 조각이 확장 됩니다.](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "Tab 키를 다시 누르면 코드 조각이 확장 됩니다.")</span><span class="sxs-lookup"><span data-stu-id="abaf8-595">![Press Tab again and the snippet will expand](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="abaf8-596">*Tab 키를 다시 누르면 코드 조각이 확장 됩니다.*</span><span class="sxs-lookup"><span data-stu-id="abaf8-596">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="abaf8-597">***마우스C#(, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면*** 1(sp1).</span><span class="sxs-lookup"><span data-stu-id="abaf8-597">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="abaf8-598">코드 조각을 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-598">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="abaf8-599">코드 **조각 삽입** 을 선택한 다음 **내 코드 조각을**선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-599">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="abaf8-600">목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="abaf8-600">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="abaf8-601">![코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="abaf8-601">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="abaf8-602">*코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="abaf8-602">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="abaf8-603">![목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="abaf8-603">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="abaf8-604">*목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="abaf8-604">*Pick the relevant snippet from the list, by clicking on it*</span></span>
