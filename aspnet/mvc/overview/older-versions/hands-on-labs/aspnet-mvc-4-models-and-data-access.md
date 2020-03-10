---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
title: ASP.NET MVC 4 모델 및 데이터 액세스 | Microsoft Docs
author: rick-anderson
description: 참고:이 실습 랩에서는 ASP.NET MVC에 대 한 기본 지식이 있다고 가정 합니다. 이전에 ASP.NET MVC를 사용 하지 않은 경우 ASP.NET MVC 4를 대신 사용 하는 것이 좋습니다.
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 634ea84b-f904-4afe-b71b-49cccef4d9cc
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
msc.type: authoredcontent
ms.openlocfilehash: 90635b617930d0a9c126795f4c8790d542e33dc9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451469"
---
# <a name="aspnet-mvc-4-models-and-data-access"></a><span data-ttu-id="bdaf7-104">ASP.NET MVC 4 모델 및 데이터 액세스</span><span class="sxs-lookup"><span data-stu-id="bdaf7-104">ASP.NET MVC 4 Models and Data Access</span></span>

<span data-ttu-id="bdaf7-105">[웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="bdaf7-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="bdaf7-106">웹 캠프 교육 키트 다운로드</span><span class="sxs-lookup"><span data-stu-id="bdaf7-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="bdaf7-107">이 실습 랩에서는 **ASP.NET MVC**에 대 한 기본 지식이 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-107">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="bdaf7-108">이전에 **ASP.NET mvc** 를 사용 하지 않은 경우 **ASP.NET mvc 4 기본** 실습 실습을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-108">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC 4 Fundamentals** Hands-on Lab.</span></span>

<span data-ttu-id="bdaf7-109">이 랩에서는 원본 폴더에 제공 된 샘플 웹 응용 프로그램에 사소한 변경 사항을 적용 하 여 앞에서 설명한 향상 된 기능 및 새로운 기능을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-109">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>

> [!NOTE]
> <span data-ttu-id="bdaf7-110">모든 샘플 코드와 코드 조각은 [Microsoft 웹/WebCampTrainingKit 릴리스에서](https://aka.ms/webcamps-training-kit)제공 되는 웹 캠프 교육 키트에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-110">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="bdaf7-111">이 랩에서 관련 된 프로젝트는 [ASP.NET MVC 4 모델 및 데이터 액세스](https://github.com/Microsoft-Web/HOL-MVC4ModelsAndDataAccess)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-111">The project specific to this lab is available at [ASP.NET MVC 4 Models and Data Access](https://github.com/Microsoft-Web/HOL-MVC4ModelsAndDataAccess).</span></span>

<span data-ttu-id="bdaf7-112">**ASP.NET MVC 기본** 실습 랩에서는 하드 코드 된 데이터를 컨트롤러에서 보기 템플릿으로 전달 했습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-112">In **ASP.NET MVC Fundamentals** Hands-on Lab, you have been passing hard-coded data from the Controllers to the View templates.</span></span> <span data-ttu-id="bdaf7-113">그러나 실제 웹 응용 프로그램을 빌드하기 위해 실제 데이터베이스를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-113">But, in order to build a real Web application, you might want to use a real database.</span></span>

<span data-ttu-id="bdaf7-114">이 실습 랩에서는 Music Store 응용 프로그램에 필요한 데이터를 저장 하 고 검색 하기 위해 데이터베이스 엔진을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-114">This Hands-on Lab will show you how to use a database engine in order to store and retrieve the data needed for the Music Store application.</span></span> <span data-ttu-id="bdaf7-115">이렇게 하려면 기존 데이터베이스로 시작 하 고이 데이터베이스에서 엔터티 데이터 모델를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-115">To accomplish that, you will start with an existing database and create the Entity Data Model from it.</span></span> <span data-ttu-id="bdaf7-116">이 랩에서는 **Database First** 접근 방식 뿐만 아니라 **Code First** 방법도 충족 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-116">Throughout this lab, you will meet the **Database First** approach as well as the **Code First** approach.</span></span>

<span data-ttu-id="bdaf7-117">그러나 **Model First** 방법을 사용 하 고 도구를 사용 하 여 동일한 모델을 만든 다음 여기에서 데이터베이스를 생성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-117">However, you can also use the **Model First** approach, create the same model using the tools, and then generate the database from it.</span></span>

<span data-ttu-id="bdaf7-118">![Database First와 Model First 비교](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First와 Model First 비교")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-118">![Database First vs. Model First](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First vs. Model First")</span></span>

<span data-ttu-id="bdaf7-119">*Database First와 Model First 비교*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-119">*Database First vs. Model First*</span></span>

<span data-ttu-id="bdaf7-120">모델을 생성 한 후에는 하드 코드 된 데이터를 사용 하는 대신 StoreController에서 적절 하 게 조정 하 여 데이터베이스에서 가져온 데이터와 저장소 뷰를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-120">After generating the Model, you will make the proper adjustments in the StoreController to provide the Store Views with the data taken from the database, instead of using hard-coded data.</span></span> <span data-ttu-id="bdaf7-121">이번에는 데이터가 데이터베이스에서 제공 되는 경우를 비롯 하 여 StoreController가 뷰 템플릿에 대해 동일한 ViewModels를 반환 하기 때문에 뷰 템플릿을 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-121">You will not need to make any change to the View templates because the StoreController will be returning the same ViewModels to the View templates, although this time the data will come from the database.</span></span>

<span data-ttu-id="bdaf7-122">**Code First 방법**</span><span class="sxs-lookup"><span data-stu-id="bdaf7-122">**The Code First Approach**</span></span>

<span data-ttu-id="bdaf7-123">Code First 방법을 사용 하면 일반적으로 프레임 워크와 결합 된 클래스를 생성 하지 않고 코드에서 모델을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-123">The Code First approach allows us to define the model from the code without generating classes that are generally coupled with the framework.</span></span>

<span data-ttu-id="bdaf7-124">Code first에서 모델 개체는 POCOs, &quot;일반 이전 CLR 개체&quot;를 사용 하 여 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-124">In code first, model objects are defined with POCOs, &quot;Plain Old CLR Objects&quot;.</span></span> <span data-ttu-id="bdaf7-125">POCOs는 상속이 없고 인터페이스를 구현 하지 않는 간단한 일반 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-125">POCOs are simple plain classes that have no inheritance and do not implement interfaces.</span></span> <span data-ttu-id="bdaf7-126">데이터베이스를 자동으로 생성 하거나 기존 데이터베이스를 사용 하 고 코드에서 클래스 매핑을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-126">We can automatically generate the database from them, or we can use an existing database and generate the class mapping from the code.</span></span>

<span data-ttu-id="bdaf7-127">이 방법을 사용할 경우의 이점은 POCOs 클래스가 매핑 프레임 워크와 결합 되지 않으므로 모델은 지 속성 프레임 워크 (이 경우 Entity Framework)와 독립적으로 유지 된다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-127">The benefits of using this approach is that the Model remains independent from the persistence framework (in this case, Entity Framework), as the POCOs classes are not coupled with the mapping framework.</span></span>

> [!NOTE]
> <span data-ttu-id="bdaf7-128">이 랩은이 실습 랩에 표시 된 기능에 맞게 사용자 지정 및 최소화 된 ASP.NET MVC 4 및 버전의 Music Store 샘플 응용 프로그램을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-128">This Lab is based on ASP.NET MVC 4 and a version of the Music Store sample application customized and minimized to fit only the features shown in this Hands-On Lab.</span></span>
> 
> <span data-ttu-id="bdaf7-129">전체 **음악 스토어** 자습서 응용 프로그램을 탐색 하려는 경우 [MVC-음악 스토어](https://github.com/evilDave/MVC-Music-Store)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-129">If you wish to explore the whole **Music Store** tutorial application you can find it in [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="bdaf7-130">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="bdaf7-130">Prerequisites</span></span>

<span data-ttu-id="bdaf7-131">이 랩을 완료 하려면 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-131">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="bdaf7-132">[웹 또는 고급의 경우 2012 Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (설치 방법에 대 한 지침은 [부록 a를](#AppendixA) 참조 하세요.)</span><span class="sxs-lookup"><span data-stu-id="bdaf7-132">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="bdaf7-133">설치 프로그램</span><span class="sxs-lookup"><span data-stu-id="bdaf7-133">Setup</span></span>

<span data-ttu-id="bdaf7-134">**코드 조각 설치**</span><span class="sxs-lookup"><span data-stu-id="bdaf7-134">**Installing Code Snippets**</span></span>

<span data-ttu-id="bdaf7-135">편의를 위해이 랩에서 관리 하는 대부분의 코드는 Visual Studio 코드 조각으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-135">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="bdaf7-136">코드 조각을 설치 하려면 **.\Source\Setup\CodeSnippets.vsi** 파일을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-136">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="bdaf7-137">Visual Studio Code 코드 조각에 대해 잘 모르는 경우이를 사용 하는 방법을 알아보려면이 문서의 부록 [C: 코드 조각&quot;사용](#AppendixC) &quot;부록을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-137">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="bdaf7-138">실습</span><span class="sxs-lookup"><span data-stu-id="bdaf7-138">Exercises</span></span>

<span data-ttu-id="bdaf7-139">이 실습 랩은 다음 연습으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-139">This Hands-on Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="bdaf7-140">연습 1: 데이터베이스 추가</span><span class="sxs-lookup"><span data-stu-id="bdaf7-140">Exercise 1: Adding a Database</span></span>](#Exercise1)
2. [<span data-ttu-id="bdaf7-141">연습 2: Code First을 사용 하 여 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="bdaf7-141">Exercise 2: Creating a Database using Code First</span></span>](#Exercise2)
3. [<span data-ttu-id="bdaf7-142">연습 3: 매개 변수를 사용 하 여 데이터베이스 쿼리</span><span class="sxs-lookup"><span data-stu-id="bdaf7-142">Exercise 3: Querying the Database with Parameters</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="bdaf7-143">각 연습에는 연습을 완료 한 후 얻게 되는 결과 솔루션을 포함 하는 **끝** 폴더가 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-143">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="bdaf7-144">연습을 진행 하는 데 도움이 필요한 경우이 솔루션을 지침으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-144">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="bdaf7-145">이 랩을 완료 하는 데 소요 되는 예상 시간: **35 분**</span><span class="sxs-lookup"><span data-stu-id="bdaf7-145">Estimated time to complete this lab: **35 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Adding_a_Database"></a>
### <a name="exercise-1-adding-a-database"></a><span data-ttu-id="bdaf7-146">연습 1: 데이터베이스 추가</span><span class="sxs-lookup"><span data-stu-id="bdaf7-146">Exercise 1: Adding a Database</span></span>

<span data-ttu-id="bdaf7-147">이 연습에서는 데이터를 사용 하기 위해 MusicStore 응용 프로그램의 테이블이 포함 된 데이터베이스를 솔루션에 추가 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-147">In this exercise, you will learn how to add a database with the tables of the MusicStore application to the solution in order to consume its data.</span></span> <span data-ttu-id="bdaf7-148">데이터베이스가 모델을 사용 하 여 생성 되 고 솔루션에 추가 된 후에는 하드 코드 된 값을 사용 하는 대신 데이터베이스에서 가져온 데이터를 뷰 템플릿에 제공 하도록 StoreController 클래스를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-148">Once the database is generated with the model, and added to the solution, you will modify the StoreController class to provide the View template with the data taken from the database, instead of using hard-coded values.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Adding_a_Database"></a>
#### <a name="task-1---adding-a-database"></a><span data-ttu-id="bdaf7-149">작업 1-데이터베이스 추가</span><span class="sxs-lookup"><span data-stu-id="bdaf7-149">Task 1 - Adding a Database</span></span>

<span data-ttu-id="bdaf7-150">이 태스크에서는 MusicStore 응용 프로그램의 주 테이블이 포함 된 이미 생성 된 데이터베이스를 솔루션에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-150">In this task, you will add an already created database with the main tables of the MusicStore application to the solution.</span></span>

1. <span data-ttu-id="bdaf7-151">**Source/Ex1-AddingADatabaseDBFirst/begin/** 폴더에 있는 **시작** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-151">Open the **Begin** solution located at **Source/Ex1-AddingADatabaseDBFirst/Begin/** folder.</span></span>

   1. <span data-ttu-id="bdaf7-152">계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-152">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="bdaf7-153">이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-153">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="bdaf7-154">**NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-154">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="bdaf7-155">마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-155">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="bdaf7-156">NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-156">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="bdaf7-157">NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-157">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="bdaf7-158">이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-158">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="bdaf7-159">**MvcMusicStore** 데이터베이스 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-159">Add **MvcMusicStore** database file.</span></span> <span data-ttu-id="bdaf7-160">이 실습 랩에서는 이미 생성 된 **MvcMusicStore**라는 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-160">In this Hands-on Lab, you will use an already created database called **MvcMusicStore.mdf**.</span></span> <span data-ttu-id="bdaf7-161">이렇게 하려면 **앱\_데이터** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** 를 가리킨 다음 **기존 항목**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-161">To do that, right-click **App\_Data** folder, point to **Add** and then click **Existing Item**.</span></span> <span data-ttu-id="bdaf7-162">**\Source\sts\source\asset** 로 이동 하 여 **MvcMusicStore** 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-162">Browse to **\Source\Assets** and select the **MvcMusicStore.mdf** file.</span></span>

    <span data-ttu-id="bdaf7-163">![기존 항목 추가](aspnet-mvc-4-models-and-data-access/_static/image2.png "기존 항목 추가")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-163">![Adding an Existing Item](aspnet-mvc-4-models-and-data-access/_static/image2.png "Adding an Existing Item")</span></span>

    <span data-ttu-id="bdaf7-164">*기존 항목 추가*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-164">*Adding an Existing Item*</span></span>

    <span data-ttu-id="bdaf7-165">![MvcMusicStore 데이터베이스 파일](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore 데이터베이스 파일")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-165">![MvcMusicStore.mdf database file](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore.mdf database file")</span></span>

    <span data-ttu-id="bdaf7-166">*MvcMusicStore 데이터베이스 파일*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-166">*MvcMusicStore.mdf database file*</span></span>

    <span data-ttu-id="bdaf7-167">데이터베이스가 프로젝트에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-167">The database has been added to the project.</span></span> <span data-ttu-id="bdaf7-168">데이터베이스가 솔루션 내에 있는 경우에도 다른 데이터베이스 서버에서 호스팅되는 것으로 쿼리 및 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-168">Even when the database is located inside the solution, you can query and update it as it was hosted in a different database server.</span></span>

    <span data-ttu-id="bdaf7-169">![솔루션 탐색기의 MvcMusicStore 데이터베이스](aspnet-mvc-4-models-and-data-access/_static/image4.png "솔루션 탐색기의 MvcMusicStore 데이터베이스")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-169">![MvcMusicStore database in Solution Explorer](aspnet-mvc-4-models-and-data-access/_static/image4.png "MvcMusicStore database in Solution Explorer")</span></span>

    <span data-ttu-id="bdaf7-170">*솔루션 탐색기의 MvcMusicStore 데이터베이스*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-170">*MvcMusicStore database in Solution Explorer*</span></span>
3. <span data-ttu-id="bdaf7-171">데이터베이스에 대 한 연결을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-171">Verify the connection to the database.</span></span> <span data-ttu-id="bdaf7-172">이렇게 하려면 **MvcMusicStore** 를 두 번 클릭 하 여 연결을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-172">To do this, double-click **MvcMusicStore.mdf** to establish a connection.</span></span>

    <span data-ttu-id="bdaf7-173">![MvcMusicStore에 연결](aspnet-mvc-4-models-and-data-access/_static/image5.png "MvcMusicStore에 연결")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-173">![Connecting to MvcMusicStore.mdf](aspnet-mvc-4-models-and-data-access/_static/image5.png "Connecting to MvcMusicStore.mdf")</span></span>

    <span data-ttu-id="bdaf7-174">*MvcMusicStore에 연결*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-174">*Connecting to MvcMusicStore.mdf*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_a_Data_Model"></a>
#### <a name="task-2---creating-a-data-model"></a><span data-ttu-id="bdaf7-175">작업 2-데이터 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="bdaf7-175">Task 2 - Creating a Data Model</span></span>

<span data-ttu-id="bdaf7-176">이 태스크에서는 이전 태스크에 추가 된 데이터베이스와 상호 작용 하는 데이터 모델을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-176">In this task, you will create a data model to interact with the database added in the previous task.</span></span>

1. <span data-ttu-id="bdaf7-177">데이터베이스를 나타내는 데이터 모델을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-177">Create a data model that will represent the database.</span></span> <span data-ttu-id="bdaf7-178">이렇게 하려면 솔루션 탐색기에서 **모델** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** 를 가리킨 다음 **새 항목**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-178">To do this, in Solution Explorer right-click the **Models** folder, point to **Add** and then click **New Item**.</span></span> <span data-ttu-id="bdaf7-179">**새 항목 추가** 대화 상자에서 **데이터** 템플릿을 선택 하 고 **ADO.NET 엔터티 데이터 모델** 항목을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-179">In the **Add New Item** dialog, select the **Data** template and then the **ADO.NET Entity Data Model** item.</span></span> <span data-ttu-id="bdaf7-180">데이터 모델 이름을 **Storedb .edmx** 로 변경 하 고 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-180">Change the data model name to **StoreDB.edmx** and click **Add**.</span></span>

    <span data-ttu-id="bdaf7-181">![StoreDB ADO.NET 엔터티 데이터 모델 추가](aspnet-mvc-4-models-and-data-access/_static/image6.png "StoreDB ADO.NET 엔터티 데이터 모델 추가")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-181">![Adding the StoreDB ADO.NET Entity Data Model](aspnet-mvc-4-models-and-data-access/_static/image6.png "Adding the StoreDB ADO.NET Entity Data Model")</span></span>

    <span data-ttu-id="bdaf7-182">*StoreDB ADO.NET 엔터티 데이터 모델 추가*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-182">*Adding the StoreDB ADO.NET Entity Data Model*</span></span>
2. <span data-ttu-id="bdaf7-183">**엔터티 데이터 모델 마법사** 가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-183">The **Entity Data Model Wizard** will appear.</span></span> <span data-ttu-id="bdaf7-184">이 마법사는 모델 계층을 만드는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-184">This wizard will guide you through the creation of the model layer.</span></span> <span data-ttu-id="bdaf7-185">최근에 추가 된 기존 데이터베이스를 기반으로 모델을 만들어야 하므로 **데이터베이스에서 생성** 을 선택 하 고 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-185">Since the model should be created based on the existing database recently added, select **Generate from database** and click **Next**.</span></span>

    <span data-ttu-id="bdaf7-186">![모델 콘텐츠 선택](aspnet-mvc-4-models-and-data-access/_static/image7.png "모델 콘텐츠 선택")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-186">![Choosing the model content](aspnet-mvc-4-models-and-data-access/_static/image7.png "Choosing the model content")</span></span>

    <span data-ttu-id="bdaf7-187">*모델 콘텐츠 선택*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-187">*Choosing the model content*</span></span>
3. <span data-ttu-id="bdaf7-188">데이터베이스에서 모델을 생성 하기 때문에 사용할 연결을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-188">Since you are generating a model from a database, you will need to specify the connection to use.</span></span> <span data-ttu-id="bdaf7-189">**새 연결**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-189">Click **New Connection**.</span></span>
4. <span data-ttu-id="bdaf7-190">**데이터베이스 파일 Microsoft SQL Server** 선택 하 고 **계속**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-190">Select **Microsoft SQL Server Database File** and click **Continue**.</span></span>

    <span data-ttu-id="bdaf7-191">![데이터 원본 선택](aspnet-mvc-4-models-and-data-access/_static/image8.png "데이터 원본 선택")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-191">![Choose data source](aspnet-mvc-4-models-and-data-access/_static/image8.png "Choose data source")</span></span>

    <span data-ttu-id="bdaf7-192">*데이터 소스 선택 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-192">*Choose data source dialog*</span></span>
5. <span data-ttu-id="bdaf7-193">**찾아보기** 를 클릭 하 고 **App\_Data** 폴더에 있는 데이터베이스 **MvcMusicStore** 를 선택 하 고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-193">Click **Browse** and select the database **MvcMusicStore.mdf** you located in the **App\_Data** folder and click **OK**.</span></span>

    <span data-ttu-id="bdaf7-194">![연결 속성](aspnet-mvc-4-models-and-data-access/_static/image9.png "연결 속성")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-194">![Connection properties](aspnet-mvc-4-models-and-data-access/_static/image9.png "Connection properties")</span></span>

    <span data-ttu-id="bdaf7-195">*연결 속성*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-195">*Connection properties*</span></span>
6. <span data-ttu-id="bdaf7-196">생성 된 클래스의 이름은 엔터티 연결 문자열과 동일 해야 하므로 이름을 **MusicStoreEntities** 로 변경 하 고 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-196">The generated class should have the same name as the entity connection string, so change its name to **MusicStoreEntities** and click **Next**.</span></span>

    <span data-ttu-id="bdaf7-197">![데이터 연결 선택](aspnet-mvc-4-models-and-data-access/_static/image10.png "데이터 연결 선택")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-197">![Choosing the data connection](aspnet-mvc-4-models-and-data-access/_static/image10.png "Choosing the data connection")</span></span>

    <span data-ttu-id="bdaf7-198">*데이터 연결 선택*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-198">*Choosing the data connection*</span></span>
7. <span data-ttu-id="bdaf7-199">사용할 데이터베이스 개체를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-199">Choose the database objects to use.</span></span> <span data-ttu-id="bdaf7-200">엔터티 모델은 데이터베이스의 테이블만 사용 하 고, **테이블** 옵션을 선택 하 고, **모델에 외래 키 열 포함** 및 **복수화 또는 단 수 생성 된 개체 이름** 옵션도 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-200">As the Entity Model will use just the database's tables, select the **Tables** option, and make sure that the **Include foreign key columns in the model** and **Pluralize or singularize generated object names** options are also selected.</span></span> <span data-ttu-id="bdaf7-201">모델 네임 스페이스를 **MvcMusicStore** 로 변경 하 고 **마침**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-201">Change the Model Namespace to **MvcMusicStore.Model** and click **Finish**.</span></span>

    <span data-ttu-id="bdaf7-202">![데이터베이스 개체 선택](aspnet-mvc-4-models-and-data-access/_static/image11.png "데이터베이스 개체 선택")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-202">![Choosing the database objects](aspnet-mvc-4-models-and-data-access/_static/image11.png "Choosing the database objects")</span></span>

    <span data-ttu-id="bdaf7-203">*데이터베이스 개체 선택*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-203">*Choosing the database objects*</span></span>

    > [!NOTE]
    > <span data-ttu-id="bdaf7-204">보안 경고 대화 상자가 표시 되 면 **확인** 을 클릭 하 여 템플릿을 실행 하 고 모델 엔터티에 대 한 클래스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-204">If a Security Warning dialog is shown, click **OK** to run the template and generate the classes for the model entities.</span></span>
8. <span data-ttu-id="bdaf7-205">데이터베이스에 대 한 엔터티 다이어그램이 표시 되는 반면, 각 테이블을 데이터베이스에 매핑하는 별도의 클래스가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-205">An entity diagram for the database will appear, while a separate class that maps each table to the database will be created.</span></span> <span data-ttu-id="bdaf7-206">예를 들어 앨범 **테이블은** **앨범** 클래스로 표현 되며, 여기서 테이블의 각 열은 클래스 속성에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-206">For example, the **Albums** table will be represented by an **Album** class, where each column in the table will map to a class property.</span></span> <span data-ttu-id="bdaf7-207">이렇게 하면 데이터베이스의 행을 나타내는 개체를 쿼리하고 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-207">This will allow you to query and work with objects that represent rows in the database.</span></span>

    <span data-ttu-id="bdaf7-208">![엔터티 다이어그램](aspnet-mvc-4-models-and-data-access/_static/image12.png "엔터티 다이어그램")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-208">![Entity diagram](aspnet-mvc-4-models-and-data-access/_static/image12.png "Entity diagram")</span></span>

    <span data-ttu-id="bdaf7-209">*엔터티 다이어그램*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-209">*Entity diagram*</span></span>

    > [!NOTE]
    > <span data-ttu-id="bdaf7-210">T4 템플릿 (.tt)은 엔터티 클래스를 생성 하는 코드를 실행 하 고 같은 이름의 기존 클래스를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-210">The T4 templates (.tt) run code to generate the entities classes and will overwrite the existing classes with the same name.</span></span> <span data-ttu-id="bdaf7-211">이 예제에서는 &quot;앨범&quot;, &quot;장르&quot; 및 &quot;음악가&quot; 생성 된 코드로 덮어쓴 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-211">In this example, the classes &quot;Album&quot;, &quot;Genre&quot; and &quot;Artist&quot; were overwritten with the generated code.</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Building_the_Application"></a>
#### <a name="task-3---building-the-application"></a><span data-ttu-id="bdaf7-212">작업 3-응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="bdaf7-212">Task 3 - Building the Application</span></span>

<span data-ttu-id="bdaf7-213">이 태스크에서는 모델 생성이 **앨범**, **장르** 및 **음악가** 모델 클래스를 제거 했지만 새 데이터 모델 클래스를 사용 하 여 프로젝트가 성공적으로 빌드 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-213">In this task, you will check that, although the model generation have removed the **Album**, **Genre** and **Artist** model classes, the project builds successfully by using the new data model classes.</span></span>

1. <span data-ttu-id="bdaf7-214">**빌드** 메뉴 항목을 선택한 다음 **MvcMusicStore 빌드**를 선택 하 여 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-214">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>

    <span data-ttu-id="bdaf7-215">![프로젝트 빌드](aspnet-mvc-4-models-and-data-access/_static/image13.png "프로젝트 빌드")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-215">![Building the project](aspnet-mvc-4-models-and-data-access/_static/image13.png "Building the project")</span></span>

    <span data-ttu-id="bdaf7-216">*프로젝트 빌드*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-216">*Building the project*</span></span>
2. <span data-ttu-id="bdaf7-217">프로젝트가 성공적으로 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-217">The project builds successfully.</span></span> <span data-ttu-id="bdaf7-218">그래도 작동 하는 이유는 무엇 인가요?</span><span class="sxs-lookup"><span data-stu-id="bdaf7-218">Why does it still work?</span></span> <span data-ttu-id="bdaf7-219">데이터베이스 테이블에는 제거 된 클래스의 **앨범** 및 **장르**에서 사용 하는 속성을 포함 하는 필드가 있기 때문에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-219">It works because the database tables have fields that include the properties that you were using in the removed classes **Album** and **Genre**.</span></span>

    <span data-ttu-id="bdaf7-220">![빌드 성공](aspnet-mvc-4-models-and-data-access/_static/image14.png "빌드 성공")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-220">![Builds succeeded](aspnet-mvc-4-models-and-data-access/_static/image14.png "Builds succeeded")</span></span>

    <span data-ttu-id="bdaf7-221">*빌드 성공*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-221">*Builds succeeded*</span></span>
3. <span data-ttu-id="bdaf7-222">디자이너에서 엔터티를 다이어그램 형식으로 표시 하는 동안 해당 엔터티는 C# 정말 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-222">While the designer displays the entities in a diagram format, they are really C# classes.</span></span> <span data-ttu-id="bdaf7-223">솔루션 탐색기에서 **Storedb .edmx** 노드를 확장 한 다음 **StoreDB.tt**를 확장 하면 새로 생성 된 엔터티가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-223">Expand the **StoreDB.edmx** node in the Solution Explorer and then **StoreDB.tt**, you will see the new generated entities.</span></span>

    <span data-ttu-id="bdaf7-224">![생성된 파일](aspnet-mvc-4-models-and-data-access/_static/image15.png "생성 된 파일")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-224">![Generated files](aspnet-mvc-4-models-and-data-access/_static/image15.png "Generated files")</span></span>

    <span data-ttu-id="bdaf7-225">*생성된 파일*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-225">*Generated files*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a><span data-ttu-id="bdaf7-226">작업 4-데이터베이스 쿼리</span><span class="sxs-lookup"><span data-stu-id="bdaf7-226">Task 4 - Querying the Database</span></span>

<span data-ttu-id="bdaf7-227">이 작업에서는 하드 코드 된 데이터를 사용 하는 대신 데이터베이스를 쿼리하여 정보를 검색 하도록 StoreController 클래스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-227">In this task, you will update the StoreController class so that, instead of using hardcoded data, it will query the database to retrieve the information.</span></span>

1. <span data-ttu-id="bdaf7-228">**Controllers\StoreController.cs** 을 열고 클래스에 다음 필드를 추가 하 여 **Storedb**라는 **MusicStoreEntities** 클래스의 인스턴스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-228">Open **Controllers\StoreController.cs** and add the following field to the class to hold an instance of the **MusicStoreEntities** class, named **storeDB**:</span></span>

    <span data-ttu-id="bdaf7-229">(코드 조각- *모델 및 데이터 액세스-Ex1 storeDB*)</span><span class="sxs-lookup"><span data-stu-id="bdaf7-229">(Code Snippet - *Models And Data Access - Ex1 storeDB*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample1.cs)]
2. <span data-ttu-id="bdaf7-230">**MusicStoreEntities** 클래스는 데이터베이스의 각 테이블에 대 한 컬렉션 속성을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-230">The **MusicStoreEntities** class exposes a collection property for each table in the database.</span></span> <span data-ttu-id="bdaf7-231">모든 **앨범이**포함 된 장르를 검색 하도록 **찾아보기** 작업 메서드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-231">Update **Browse** action method to retrieve a Genre with all of the **Albums**.</span></span>

    <span data-ttu-id="bdaf7-232">(코드 조각- *모델 및 데이터 액세스-Ex1 저장소 찾아보기*)</span><span class="sxs-lookup"><span data-stu-id="bdaf7-232">(Code Snippet - *Models And Data Access - Ex1 Store Browse*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample2.cs)]

    > [!NOTE]
    > <span data-ttu-id="bdaf7-233">**LINQ** (언어 통합 쿼리) 라는 .net 기능을 사용 하 여 이러한 컬렉션에 대해 강력한 형식의 쿼리 식을 작성 합니다 .이 기능을 사용 하면 데이터베이스에 대해 코드를 실행 하 고 프로그래밍할 수 있는 개체를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-233">You are using a capability of .NET called **LINQ** (language-integrated query) to write strongly-typed query expressions against these collections - which will execute code against the database and return objects that you can program against.</span></span>
    > 
    > <span data-ttu-id="bdaf7-234">LINQ에 대 한 자세한 내용은 [msdn 사이트](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx)를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-234">For more information about LINQ, please visit the [msdn site](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx).</span></span>
3. <span data-ttu-id="bdaf7-235">**인덱스** 작업 메서드를 업데이트 하 여 모든 장르를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-235">Update **Index** action method to retrieve all the genres.</span></span>

    <span data-ttu-id="bdaf7-236">(코드 조각- *모델 및 데이터 액세스-Ex1 저장소 인덱스*)</span><span class="sxs-lookup"><span data-stu-id="bdaf7-236">(Code Snippet - *Models And Data Access - Ex1 Store Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample3.cs)]
4. <span data-ttu-id="bdaf7-237">**인덱스** 작업 메서드를 업데이트 하 여 모든 장르를 검색 하 고 컬렉션을 목록으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-237">Update **Index** action method to retrieve all the genres and transform the collection to a list.</span></span>

    <span data-ttu-id="bdaf7-238">(코드 조각- *모델 및 데이터 액세스-Ex1 저장소 GenreMenu*)</span><span class="sxs-lookup"><span data-stu-id="bdaf7-238">(Code Snippet - *Models And Data Access - Ex1 Store GenreMenu*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample4.cs)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="bdaf7-239">작업 5-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="bdaf7-239">Task 5 - Running the Application</span></span>

<span data-ttu-id="bdaf7-240">이 태스크에서는 저장소 인덱스 페이지에 하드 코드 된 항목이 아니라 데이터베이스에 저장 된 장르가 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-240">In this task, you will check that the Store Index page will now display the Genres stored in the database instead of the hardcoded ones.</span></span> <span data-ttu-id="bdaf7-241">**StoreController** 는 이전과 동일한 엔터티를 반환 하기 때문에 뷰 템플릿을 변경할 필요가 없습니다. 하지만 이번에는 데이터가 데이터베이스에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-241">There is no need to change the View template because the **StoreController** is returning the same entities as before, although this time the data will come from the database.</span></span>

1. <span data-ttu-id="bdaf7-242">솔루션을 다시 빌드하고 **F5** 키를 눌러 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-242">Rebuild the solution and press **F5** to run the Application.</span></span>
2. <span data-ttu-id="bdaf7-243">프로젝트가 홈 페이지에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-243">The project starts in the Home page.</span></span> <span data-ttu-id="bdaf7-244">**장르** 메뉴가 더 이상 하드 코드 된 목록이 아닌지 확인 하 고 데이터가 데이터베이스에서 직접 검색 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-244">Verify that the menu of **Genres** is no longer a hardcoded list, and the data is directly retrieved from the database.</span></span>

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image16.png)

    <span data-ttu-id="bdaf7-246">*데이터베이스에서 장르 검색*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-246">*Browsing Genres from the database*</span></span>
3. <span data-ttu-id="bdaf7-247">이제 장르로 이동 하 여 데이터베이스에서 앨범이 채워지는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-247">Now browse to any genre and verify the albums are populated from database.</span></span>

    <span data-ttu-id="bdaf7-248">![데이터베이스에서 앨범 찾아보기](aspnet-mvc-4-models-and-data-access/_static/image17.png "데이터베이스에서 앨범 찾아보기")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-248">![Browsing Albums from the database](aspnet-mvc-4-models-and-data-access/_static/image17.png "Browsing Albums from the database")</span></span>

    <span data-ttu-id="bdaf7-249">*데이터베이스에서 앨범 찾아보기*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-249">*Browsing Albums from the database*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Database_Using_Code_First"></a>
### <a name="exercise-2-creating-a-database-using-code-first"></a><span data-ttu-id="bdaf7-250">연습 2: Code First을 사용 하 여 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="bdaf7-250">Exercise 2: Creating a Database Using Code First</span></span>

<span data-ttu-id="bdaf7-251">이 연습에서는 MusicStore 응용 프로그램의 테이블을 사용 하 여 데이터베이스를 만드는 방법 및 해당 데이터에 액세스 하는 방법을 설명 Code First 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-251">In this exercise, you will learn how to use the Code First approach to create a database with the tables of the MusicStore application, and how to access its data.</span></span>

<span data-ttu-id="bdaf7-252">모델을 생성 한 후에는 하드 코드 된 값을 사용 하는 대신 데이터베이스에서 가져온 데이터를 사용 하 여 뷰 템플릿을 제공 하도록 StoreController를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-252">Once the model is generated, you will modify the StoreController to provide the View template with the data taken from the database, instead of using hardcoded values.</span></span>

> [!NOTE]
> <span data-ttu-id="bdaf7-253">연습 1을 완료 하 고 이미 Database First 방식으로 작업 한 경우 다른 프로세스를 사용 하 여 동일한 결과를 얻는 방법을 배우게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-253">If you have completed Exercise 1 and have already worked with the Database First approach, you will now learn how to get the same results with a different process.</span></span> <span data-ttu-id="bdaf7-254">실습 1과 관련 된 작업은 더 쉽게 읽을 수 있도록 표시 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-254">The tasks that are in common with Exercise 1 have been marked to make your reading easier.</span></span> <span data-ttu-id="bdaf7-255">연습 1을 완료 하지 않았지만 Code First 방법을 배우는 경우이 연습에서 시작 하 여 토픽의 전체 검사를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-255">If you have not completed Exercise 1 but would like to learn the Code First approach, you can start from this exercise and get a full coverage of the topic.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Populating_Sample_Data"></a>
#### <a name="task-1---populating-sample-data"></a><span data-ttu-id="bdaf7-256">작업 1-샘플 데이터 채우기</span><span class="sxs-lookup"><span data-stu-id="bdaf7-256">Task 1 - Populating Sample Data</span></span>

<span data-ttu-id="bdaf7-257">이 태스크에서는 처음 코드를 사용 하 여 만들 때 샘플 데이터를 사용 하 여 데이터베이스를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-257">In this task, you will populate the database with sample data when it is initially created using Code-First.</span></span>

1. <span data-ttu-id="bdaf7-258">**Source/Ex2-CreatingADatabaseCodeFirst/begin/** 폴더에 있는 **시작** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-258">Open the **Begin** solution located at **Source/Ex2-CreatingADatabaseCodeFirst/Begin/** folder.</span></span> <span data-ttu-id="bdaf7-259">그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-259">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="bdaf7-260">제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-260">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="bdaf7-261">이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-261">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="bdaf7-262">**NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-262">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="bdaf7-263">마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-263">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="bdaf7-264">NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-264">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="bdaf7-265">NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-265">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="bdaf7-266">이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-266">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="bdaf7-267">**모델** 폴더에 **SampleData.cs** 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-267">Add the **SampleData.cs** file to the **Models** folder.</span></span> <span data-ttu-id="bdaf7-268">이렇게 하려면 **모델** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** 를 가리킨 다음 **기존 항목**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-268">To do that, right-click **Models** folder, point to **Add** and then click **Existing Item**.</span></span> <span data-ttu-id="bdaf7-269">**\Source\sts\source\stl** 을 찾아 **SampleData.cs** 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-269">Browse to **\Source\Assets** and select the **SampleData.cs** file.</span></span>

    <span data-ttu-id="bdaf7-270">![샘플 데이터 채우기 코드](aspnet-mvc-4-models-and-data-access/_static/image18.png "샘플 데이터 채우기 코드")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-270">![Sample data populate code](aspnet-mvc-4-models-and-data-access/_static/image18.png "Sample data populate code")</span></span>

    <span data-ttu-id="bdaf7-271">*샘플 데이터 채우기 코드*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-271">*Sample data populate code*</span></span>
3. <span data-ttu-id="bdaf7-272">**Global.asax.cs** 파일을 열고 다음 *using* 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-272">Open the **Global.asax.cs** file and add the following *using* statements.</span></span>

    <span data-ttu-id="bdaf7-273">(코드 조각- *모델 및 데이터 액세스-Ex2 Global Global.asax using*)</span><span class="sxs-lookup"><span data-stu-id="bdaf7-273">(Code Snippet - *Models And Data Access - Ex2 Global Asax Usings*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample5.cs)]
4. <span data-ttu-id="bdaf7-274">**응용 프로그램\_Start ()** 메서드에서 다음 줄을 추가 하 여 데이터베이스 이니셜라이저를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-274">In the **Application\_Start()** method add the following line to set the database initializer.</span></span>

    <span data-ttu-id="bdaf7-275">(코드 조각- *모델 및 데이터 액세스-Ex2 Global Global.asax SetInitializer*)</span><span class="sxs-lookup"><span data-stu-id="bdaf7-275">(Code Snippet - *Models And Data Access - Ex2 Global Asax SetInitializer*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample6.cs)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Configuring_the_connection_to_the_Database"></a>
#### <a name="task-2---configuring-the-connection-to-the-database"></a><span data-ttu-id="bdaf7-276">작업 2-데이터베이스에 대 한 연결 구성</span><span class="sxs-lookup"><span data-stu-id="bdaf7-276">Task 2 - Configuring the connection to the Database</span></span>

<span data-ttu-id="bdaf7-277">프로젝트에 데이터베이스를 이미 추가 했으므로 이제는 web.config 파일에 연결 문자열을 **작성 합니다.**</span><span class="sxs-lookup"><span data-stu-id="bdaf7-277">Now that you have already added a database to our project, you will write in the **Web.config** file the connection string.</span></span>

1. <span data-ttu-id="bdaf7-278">**Web.config에 연결**문자열을 추가 합니다. 이렇게 하려면 프로젝트 루트에서 **web.config를 열고** defaultconnection 이라는 연결 문자열을 **&lt;connectionStrings&gt;** 섹션에서 다음 줄로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-278">Add a connection string at **Web.config**. To do that, open **Web.config** at project root and replace the connection string named DefaultConnection with this line in the **&lt;connectionStrings&gt;** section:</span></span>

    <span data-ttu-id="bdaf7-279">![Web.config 파일 위치](aspnet-mvc-4-models-and-data-access/_static/image19.png "Web.config 파일 위치")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-279">![Web.config file location](aspnet-mvc-4-models-and-data-access/_static/image19.png "Web.config file location")</span></span>

    <span data-ttu-id="bdaf7-280">*Web.config 파일 위치*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-280">*Web.config file location*</span></span>

    [!code-xml[Main](aspnet-mvc-4-models-and-data-access/samples/sample7.xml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Working_with_the_Model"></a>
#### <a name="task-3---working-with-the-model"></a><span data-ttu-id="bdaf7-281">작업 3-모델 작업</span><span class="sxs-lookup"><span data-stu-id="bdaf7-281">Task 3 - Working with the Model</span></span>

<span data-ttu-id="bdaf7-282">데이터베이스에 대 한 연결을 이미 구성 했으므로 모델을 데이터베이스 테이블과 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-282">Now that you have already configured the connection to the database, you will link the model with the database tables.</span></span> <span data-ttu-id="bdaf7-283">이 태스크에서는 Code First를 사용 하 여 데이터베이스에 연결 되는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-283">In this task, you will create a class that will be linked to the database with Code First.</span></span> <span data-ttu-id="bdaf7-284">수정 해야 하는 POCO 모델 클래스가 존재 한다는 점에 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-284">Remember that there is an existent POCO model class that should be modified.</span></span>

> [!NOTE]
> <span data-ttu-id="bdaf7-285">연습 1을 완료 한 경우 마법사에서이 단계를 수행 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-285">If you completed Exercise 1, you will note that this step was performed by a wizard.</span></span> <span data-ttu-id="bdaf7-286">Code First를 수행 하 여 데이터 엔터티에 연결 되는 클래스를 수동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-286">By doing Code First, you will manually create classes that will be linked to data entities.</span></span>

1. <span data-ttu-id="bdaf7-287">**모델** 프로젝트 폴더에서 POCO 모델 클래스 **장르** 를 열고 ID를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-287">Open the POCO model class **Genre** from **Models** project folder and include an ID.</span></span> <span data-ttu-id="bdaf7-288">이름이 **GenreId**인 int 속성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-288">Use an int property with the name **GenreId**.</span></span>

    <span data-ttu-id="bdaf7-289">(코드 조각- *모델 및 데이터 액세스-Ex2 Code First 장르*)</span><span class="sxs-lookup"><span data-stu-id="bdaf7-289">(Code Snippet - *Models And Data Access - Ex2 Code First Genre*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample8.cs)]

    > [!NOTE]
    > <span data-ttu-id="bdaf7-290">Code First 규칙을 사용 하려면 클래스 장르에 자동으로 검색 되는 기본 키 속성이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-290">To work with Code First conventions, the class Genre must have a primary key property that will be automatically detected.</span></span>
    > 
    > <span data-ttu-id="bdaf7-291">이 [msdn 문서](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx)에서 Code First 규칙에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-291">You can read more about Code First Conventions in this [msdn article](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx).</span></span>
2. <span data-ttu-id="bdaf7-292">이제 **모델** 프로젝트 폴더에서 POCO 모델 클래스 **앨범** 을 열고 외래 키를 포함 하 고 이름이 **GenreId** 및 **ArtistId**인 속성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-292">Now, open the POCO model class **Album** from **Models** project folder and include the foreign keys, create properties with the names **GenreId** and **ArtistId**.</span></span> <span data-ttu-id="bdaf7-293">이 클래스에는 기본 키에 대 한 **GenreId** 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-293">This class already have the **GenreId** for the primary key.</span></span>

    <span data-ttu-id="bdaf7-294">(코드 조각- *모델 및 데이터 액세스-Ex2 Code First 앨범*)</span><span class="sxs-lookup"><span data-stu-id="bdaf7-294">(Code Snippet - *Models And Data Access - Ex2 Code First Album*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample9.cs)]
3. <span data-ttu-id="bdaf7-295">POCO 모델 클래스 **음악가** 를 열고 **ArtistId** 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-295">Open the POCO model class **Artist** and include the **ArtistId** property.</span></span>

    <span data-ttu-id="bdaf7-296">(코드 조각- *모델 및 데이터 액세스-Ex2 Code First 음악가*)</span><span class="sxs-lookup"><span data-stu-id="bdaf7-296">(Code Snippet - *Models And Data Access - Ex2 Code First Artist*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample10.cs)]
4. <span data-ttu-id="bdaf7-297">**모델** 프로젝트 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 클래스**.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-297">Right-click the **Models** project folder and select **Add | Class**.</span></span> <span data-ttu-id="bdaf7-298">파일 이름을 **MusicStoreEntities.cs**로 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-298">Name the file **MusicStoreEntities.cs**.</span></span> <span data-ttu-id="bdaf7-299">그런 다음 추가를 클릭 **합니다.**</span><span class="sxs-lookup"><span data-stu-id="bdaf7-299">Then, click **Add.**</span></span>

    <span data-ttu-id="bdaf7-300">![클래스 추가](aspnet-mvc-4-models-and-data-access/_static/image20.png "클래스 추가")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-300">![Adding a class](aspnet-mvc-4-models-and-data-access/_static/image20.png "Adding a class")</span></span>

    <span data-ttu-id="bdaf7-301">*새 항목 추가*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-301">*Adding a new item*</span></span>

    <span data-ttu-id="bdaf7-302">![Class2 추가](aspnet-mvc-4-models-and-data-access/_static/image21.png "Class2 추가")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-302">![Adding a class2](aspnet-mvc-4-models-and-data-access/_static/image21.png "Adding a class2")</span></span>

    <span data-ttu-id="bdaf7-303">*클래스 추가*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-303">*Adding a class*</span></span>
5. <span data-ttu-id="bdaf7-304">방금 만든 클래스를 **MusicStoreEntities.cs** **하 고 네임 스페이스** 를 포함 하 여 네임 스페이스를 **엽니다.**</span><span class="sxs-lookup"><span data-stu-id="bdaf7-304">Open the class you have just created, **MusicStoreEntities.cs**, and include the namespaces **System.Data.Entity** and **System.Data.Entity.Infrastructure**.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample11.cs)]
6. <span data-ttu-id="bdaf7-305">**DbContext** 클래스를 확장 하도록 클래스 선언을 바꿉니다. Public **dbset** 을 선언 하 고 **onmodelcreating** 메서드를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-305">Replace the class declaration to extend the **DbContext** class: declare a public **DBSet** and override **OnModelCreating** method.</span></span> <span data-ttu-id="bdaf7-306">이 단계를 수행한 후에는 모델을 Entity Framework와 연결 하는 도메인 클래스를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-306">After this step you will get a domain class that will link your model with the Entity Framework.</span></span> <span data-ttu-id="bdaf7-307">이렇게 하려면 클래스 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-307">In order to do that, replace the class code with the following:</span></span>

    <span data-ttu-id="bdaf7-308">(코드 조각- *모델 및 데이터 액세스-Ex2 Code First MusicStoreEntities*)</span><span class="sxs-lookup"><span data-stu-id="bdaf7-308">(Code Snippet - *Models And Data Access - Ex2 Code First MusicStoreEntities*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample12.cs)]

> [!NOTE]
> <span data-ttu-id="bdaf7-309">Entity Framework **DbContext** 및 **dbset** 를 사용 하면 POCO 클래스 장르를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-309">With Entity Framework **DbContext** and **DBSet** you will be able to query the POCO class Genre.</span></span> <span data-ttu-id="bdaf7-310">**Onmodelcreating** 메서드를 확장 하 여 **코드** 에서 장르를 데이터베이스 테이블에 매핑하는 방법을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-310">By extending **OnModelCreating** method, you are specifying in the **code** how Genre will be mapped to a database table.</span></span> <span data-ttu-id="bdaf7-311">DBContext 및 DBSet에 대 한 자세한 내용은 msdn 문서 [링크](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) 에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-311">You can find more information about DBContext and DBSet in this msdn article: [link](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a><span data-ttu-id="bdaf7-312">작업 4-데이터베이스 쿼리</span><span class="sxs-lookup"><span data-stu-id="bdaf7-312">Task 4 - Querying the Database</span></span>

<span data-ttu-id="bdaf7-313">이 작업에서는 하드 코드 된 데이터를 사용 하는 대신 데이터베이스에서 StoreController 클래스를 검색 하도록 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-313">In this task, you will update the StoreController class so that, instead of using hardcoded data, it will retrieve it from the database.</span></span>

> [!NOTE]
> <span data-ttu-id="bdaf7-314">이 작업은 연습 1에서 일반적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-314">This task is in common with Exercise 1.</span></span>
> 
> <span data-ttu-id="bdaf7-315">연습 1을 완료 한 경우 이러한 단계는 두 방법 (데이터베이스 first 또는 Code first)에서 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-315">If you completed Exercise 1 you will note these steps are the same in both approaches (Database first or Code first).</span></span> <span data-ttu-id="bdaf7-316">모델에 데이터를 연결 하는 방법은 다르지만 데이터 엔터티에 대 한 액세스는 컨트롤러에서 아직 투명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-316">They are different in how the data is linked with the model, but the access to data entities is yet transparent from the controller.</span></span>

1. <span data-ttu-id="bdaf7-317">**Controllers\StoreController.cs** 을 열고 클래스에 다음 필드를 추가 하 여 **Storedb**라는 **MusicStoreEntities** 클래스의 인스턴스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-317">Open **Controllers\StoreController.cs** and add the following field to the class to hold an instance of the **MusicStoreEntities** class, named **storeDB**:</span></span>

    <span data-ttu-id="bdaf7-318">(코드 조각- *모델 및 데이터 액세스-Ex1 storeDB*)</span><span class="sxs-lookup"><span data-stu-id="bdaf7-318">(Code Snippet - *Models And Data Access - Ex1 storeDB*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample13.cs)]
2. <span data-ttu-id="bdaf7-319">**MusicStoreEntities** 클래스는 데이터베이스의 각 테이블에 대 한 컬렉션 속성을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-319">The **MusicStoreEntities** class exposes a collection property for each table in the database.</span></span> <span data-ttu-id="bdaf7-320">모든 **앨범이**포함 된 장르를 검색 하도록 **찾아보기** 작업 메서드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-320">Update **Browse** action method to retrieve a Genre with all of the **Albums**.</span></span>

    <span data-ttu-id="bdaf7-321">(코드 조각- *모델 및 데이터 액세스-Ex2 저장소 찾아보기*)</span><span class="sxs-lookup"><span data-stu-id="bdaf7-321">(Code Snippet - *Models And Data Access - Ex2 Store Browse*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample14.cs)]

    > [!NOTE]
    > <span data-ttu-id="bdaf7-322">**LINQ** (언어 통합 쿼리) 라는 .net 기능을 사용 하 여 이러한 컬렉션에 대해 강력한 형식의 쿼리 식을 작성 합니다 .이 기능을 사용 하면 데이터베이스에 대해 코드를 실행 하 고 프로그래밍할 수 있는 개체를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-322">You are using a capability of .NET called **LINQ** (language-integrated query) to write strongly-typed query expressions against these collections - which will execute code against the database and return objects that you can program against.</span></span>
    > 
    > <span data-ttu-id="bdaf7-323">LINQ에 대 한 자세한 내용은 [msdn 사이트](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx)를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-323">For more information about LINQ, please visit the [msdn site](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx).</span></span>
3. <span data-ttu-id="bdaf7-324">**인덱스** 작업 메서드를 업데이트 하 여 모든 장르를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-324">Update **Index** action method to retrieve all the genres.</span></span>

    <span data-ttu-id="bdaf7-325">(코드 조각- *모델 및 데이터 액세스-Ex2 저장소 인덱스*)</span><span class="sxs-lookup"><span data-stu-id="bdaf7-325">(Code Snippet - *Models And Data Access - Ex2 Store Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample15.cs)]
4. <span data-ttu-id="bdaf7-326">**인덱스** 작업 메서드를 업데이트 하 여 모든 장르를 검색 하 고 컬렉션을 목록으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-326">Update **Index** action method to retrieve all the genres and transform the collection to a list.</span></span>

    <span data-ttu-id="bdaf7-327">(코드 조각- *모델 및 데이터 액세스-Ex2 저장소 GenreMenu*)</span><span class="sxs-lookup"><span data-stu-id="bdaf7-327">(Code Snippet - *Models And Data Access - Ex2 Store GenreMenu*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample16.cs)]

<a id="Ex2Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="bdaf7-328">작업 5-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="bdaf7-328">Task 5 - Running the Application</span></span>

<span data-ttu-id="bdaf7-329">이 태스크에서는 저장소 인덱스 페이지에 하드 코드 된 항목이 아니라 데이터베이스에 저장 된 장르가 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-329">In this task, you will check that the Store Index page will now display the Genres stored in the database instead of the hardcoded ones.</span></span> <span data-ttu-id="bdaf7-330">**StoreController** 가 이전 처럼 동일한 파일 **인덱스 viewmodel** 을 반환 하지만 이번에는 데이터를 데이터베이스에서 가져올 수 있으므로 뷰 템플릿을 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-330">There is no need to change the View template because the **StoreController** is returning the same **StoreIndexViewModel** as before, but this time the data will come from the database.</span></span>

1. <span data-ttu-id="bdaf7-331">솔루션을 다시 빌드하고 **F5** 키를 눌러 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-331">Rebuild the solution and press **F5** to run the Application.</span></span>
2. <span data-ttu-id="bdaf7-332">프로젝트가 홈 페이지에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-332">The project starts in the Home page.</span></span> <span data-ttu-id="bdaf7-333">**장르** 메뉴가 더 이상 하드 코드 된 목록이 아닌지 확인 하 고 데이터가 데이터베이스에서 직접 검색 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-333">Verify that the menu of **Genres** is no longer a hardcoded list, and the data is directly retrieved from the database.</span></span>

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image22.png)

    <span data-ttu-id="bdaf7-335">*데이터베이스에서 장르 검색*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-335">*Browsing Genres from the database*</span></span>
3. <span data-ttu-id="bdaf7-336">이제 장르로 이동 하 여 데이터베이스에서 앨범이 채워지는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-336">Now browse to any genre and verify the albums are populated from database.</span></span>

    <span data-ttu-id="bdaf7-337">![데이터베이스에서 앨범 찾아보기](aspnet-mvc-4-models-and-data-access/_static/image23.png "데이터베이스에서 앨범 찾아보기")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-337">![Browsing Albums from the database](aspnet-mvc-4-models-and-data-access/_static/image23.png "Browsing Albums from the database")</span></span>

    <span data-ttu-id="bdaf7-338">*데이터베이스에서 앨범 찾아보기*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-338">*Browsing Albums from the database*</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Querying_the_Database_with_Parameters"></a>
### <a name="exercise-3-querying-the-database-with-parameters"></a><span data-ttu-id="bdaf7-339">연습 3: 매개 변수를 사용 하 여 데이터베이스 쿼리</span><span class="sxs-lookup"><span data-stu-id="bdaf7-339">Exercise 3: Querying the Database with Parameters</span></span>

<span data-ttu-id="bdaf7-340">이 연습에서는 매개 변수를 사용 하 여 데이터베이스를 쿼리 하는 방법 및 쿼리 결과 셰이핑을 사용 하는 방법에 대해 설명 합니다 .이 기능을 사용 하 여 데이터를 보다 효율적으로 검색 하는 데이터베이스 액세스를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-340">In this exercise, you will learn how to query the database using parameters, and how to use Query Result Shaping, a feature that reduces the number database accesses retrieving data in a more efficient way.</span></span>

> [!NOTE]
> <span data-ttu-id="bdaf7-341">쿼리 결과 셰이핑에 대 한 자세한 내용은 다음 [msdn 문서](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-341">For further information on Query Result Shaping, visit the following [msdn article](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx).</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_StoreController_to_Retrieve_Albums_from_Database"></a>
#### <a name="task-1---modifying-storecontroller-to-retrieve-albums-from-database"></a><span data-ttu-id="bdaf7-342">작업 1-StoreController를 수정 하 여 데이터베이스에서 앨범 검색</span><span class="sxs-lookup"><span data-stu-id="bdaf7-342">Task 1 - Modifying StoreController to Retrieve Albums from Database</span></span>

<span data-ttu-id="bdaf7-343">이 작업에서는 데이터베이스에 액세스 하 여 특정 장르에서 앨범을 검색 하도록 **StoreController** 클래스를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-343">In this task, you will change the **StoreController** class to access the database to retrieve albums from a specific genre.</span></span>

1. <span data-ttu-id="bdaf7-344">데이터베이스 우선 방법을 사용 하려는 경우에는 **Source\Ex3-QueryingTheDatabaseWithParametersCodeFirst\Begin** 폴더에 있는 **Begin** solution를 엽니다. 여기서는 코드를 처음 사용 하거나 **Source\Ex3-QueryingTheDatabaseWithParametersDBFirst\Begin** 폴더를 사용 하려는 경우에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-344">Open the **Begin** solution located at the **Source\Ex3-QueryingTheDatabaseWithParametersCodeFirst\Begin** folder if you want to use Code-First approach or **Source\Ex3-QueryingTheDatabaseWithParametersDBFirst\Begin** folder if you want to use Database-First approach.</span></span> <span data-ttu-id="bdaf7-345">그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-345">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="bdaf7-346">제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-346">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="bdaf7-347">이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-347">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="bdaf7-348">**NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-348">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="bdaf7-349">마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-349">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="bdaf7-350">NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-350">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="bdaf7-351">NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-351">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="bdaf7-352">이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-352">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="bdaf7-353">**StoreController** 클래스를 열어 **찾아보기** 동작 메서드를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-353">Open the **StoreController** class to change the **Browse** action method.</span></span> <span data-ttu-id="bdaf7-354">이렇게 하려면 **솔루션 탐색기**에서 **Controllers** 폴더를 확장 하 고 **StoreController.cs**를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-354">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
3. <span data-ttu-id="bdaf7-355">**찾아보기** 동작 메서드를 변경 하 여 특정 장르의 앨범을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-355">Change the **Browse** action method to retrieve albums for a specific genre.</span></span> <span data-ttu-id="bdaf7-356">이렇게 하려면 다음 코드를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-356">To do this, replace the following code:</span></span>

    <span data-ttu-id="bdaf7-357">(코드 조각- *모델 및 데이터 액세스-Ex3 StoreController BrowseMethod*)</span><span class="sxs-lookup"><span data-stu-id="bdaf7-357">(Code Snippet - *Models And Data Access - Ex3 StoreController BrowseMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample17.cs)]

> [!NOTE]
> <span data-ttu-id="bdaf7-358">엔터티 컬렉션을 채우려면 **Include** 메서드를 사용 하 여 앨범을 검색 하도록 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-358">To populate a collection of the entity, you need to use the **Include** method to specify you want to retrieve the albums too.</span></span> <span data-ttu-id="bdaf7-359">을 사용할 수 있습니다. **단일 () 확장 (** 이 경우에는 하나의 장르만 앨범에 필요 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-359">You can use the .**Single()** extension in LINQ because in this case only one genre is expected for an album.</span></span> <span data-ttu-id="bdaf7-360">**Single ()** 메서드는 람다 식을 매개 변수로 사용 합니다 .이 경우에는 이름이 정의 된 값과 일치 하도록 단일 장르 개체를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-360">The **Single()** method takes a Lambda expression as a parameter, which in this case specifies a single Genre object such that its name matches the value defined.</span></span>
> 
> <span data-ttu-id="bdaf7-361">장르 개체가 검색 될 때 로드 하려는 다른 관련 엔터티를 나타낼 수 있도록 하는 기능을 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-361">You will take advantage of a feature that allows you to indicate other related entities you want loaded as well when the Genre object is retrieved.</span></span> <span data-ttu-id="bdaf7-362">이 기능을 **쿼리 결과 셰이핑**이라고 하며,이를 통해 데이터베이스에 액세스 하 여 정보를 검색 하는 데 필요한 횟수를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-362">This feature is called **Query Result Shaping**, and enables you to reduce the number of times needed to access the database to retrieve information.</span></span> <span data-ttu-id="bdaf7-363">이 시나리오에서는 검색 하는 장르에 대 한 앨범을 미리 인출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-363">In this scenario, you will want to pre-fetch the Albums for the Genre you retrieve.</span></span>
> 
> <span data-ttu-id="bdaf7-364">이 쿼리에는 관련 앨범이 필요 함을 나타내는 **장르 (&quot;앨범&quot;)** 가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-364">The query includes **Genres.Include(&quot;Albums&quot;)** to indicate that you want related albums as well.</span></span> <span data-ttu-id="bdaf7-365">이렇게 하면 단일 데이터베이스 요청에서 장르 및 앨범 데이터를 모두 검색 하므로 더 효율적인 응용 프로그램이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-365">This will result in a more efficient application, since it will retrieve both Genre and Album data in a single database request.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="bdaf7-366">작업 2-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="bdaf7-366">Task 2 - Running the Application</span></span>

<span data-ttu-id="bdaf7-367">이 태스크에서는 응용 프로그램을 실행 하 고 데이터베이스에서 특정 장르의 앨범을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-367">In this task, you will run the application and retrieve albums of a specific genre from the database.</span></span>

1. <span data-ttu-id="bdaf7-368">**F5** 키를 눌러 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-368">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="bdaf7-369">프로젝트가 홈 페이지에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-369">The project starts in the Home page.</span></span> <span data-ttu-id="bdaf7-370">URL을/Svs\uhhhhhhhhhhhhhi로 변경 하 여 데이터베이스에서 결과가 검색 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-370">Change the URL to **/Store/Browse?genre=Pop** to verify that the results are being retrieved from the database.</span></span>

    <span data-ttu-id="bdaf7-371">![장르로 찾아보기](aspnet-mvc-4-models-and-data-access/_static/image24.png "장르로 찾아보기")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-371">![Browsing by genre](aspnet-mvc-4-models-and-data-access/_static/image24.png "Browsing by genre")</span></span>

    <span data-ttu-id="bdaf7-372">*탐색/창/찾아보기? 장르 = Pop*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-372">*Browsing /Store/Browse?genre=Pop*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Accessing_Albums_by_Id"></a>
#### <a name="task-3---accessing-albums-by-id"></a><span data-ttu-id="bdaf7-373">작업 3-Id로 앨범 액세스</span><span class="sxs-lookup"><span data-stu-id="bdaf7-373">Task 3 - Accessing Albums by Id</span></span>

<span data-ttu-id="bdaf7-374">이 작업에서는 이전 절차를 반복 하 여 해당 Id로 앨범을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-374">In this task, you will repeat the previous procedure to get albums by their Id.</span></span>

1. <span data-ttu-id="bdaf7-375">필요한 경우 브라우저를 닫고 Visual Studio로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-375">Close the browser if needed, to return to Visual Studio.</span></span> <span data-ttu-id="bdaf7-376">**StoreController** 클래스를 열어 **Details** 작업 메서드를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-376">Open the **StoreController** class to change the **Details** action method.</span></span> <span data-ttu-id="bdaf7-377">이렇게 하려면 **솔루션 탐색기**에서 **Controllers** 폴더를 확장 하 고 **StoreController.cs**를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-377">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
2. <span data-ttu-id="bdaf7-378">**세부 정보** 작업 메서드를 변경 하 여 해당 **Id**를 기반으로 하는 앨범 세부 정보를 검색 합니다. 이렇게 하려면 다음 코드를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-378">Change the **Details** action method to retrieve albums details based on their **Id**. To do this, replace the following code:</span></span>

    <span data-ttu-id="bdaf7-379">(코드 조각- *모델 및 데이터 액세스-Ex3 StoreController DetailsMethod*)</span><span class="sxs-lookup"><span data-stu-id="bdaf7-379">(Code Snippet - *Models And Data Access - Ex3 StoreController DetailsMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample18.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="bdaf7-380">작업 4-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="bdaf7-380">Task 4 - Running the Application</span></span>

<span data-ttu-id="bdaf7-381">이 작업에서는 웹 브라우저에서 응용 프로그램을 실행 하 고 Id를 기준으로 앨범 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-381">In this task, you will run the Application in a web browser and obtain album details by their Id.</span></span>

1. <span data-ttu-id="bdaf7-382">**F5** 키를 눌러 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-382">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="bdaf7-383">프로젝트가 홈 페이지에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-383">The project starts in the Home page.</span></span> <span data-ttu-id="bdaf7-384">URL을 **/Store/Details/51** 로 변경 하거나 장르를 검색 하 고 앨범을 선택 하 여 데이터베이스에서 결과가 검색 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-384">Change the URL to **/Store/Details/51** or browse the genres and select an album to verify that the results are being retrieved from the database.</span></span>

    <span data-ttu-id="bdaf7-385">![검색 세부 정보](aspnet-mvc-4-models-and-data-access/_static/image25.png "검색 세부 정보")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-385">![Browsing Details](aspnet-mvc-4-models-and-data-access/_static/image25.png "Browsing Details")</span></span>

    <span data-ttu-id="bdaf7-386">*/Store/Details/51 찾아보기*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-386">*Browsing /Store/Details/51*</span></span>

> [!NOTE]
> <span data-ttu-id="bdaf7-387">또한 [부록 B: 웹 배포을 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시](#AppendixB)를 수행 하는 Windows Azure 웹 사이트에이 응용 프로그램을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-387">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="bdaf7-388">요약</span><span class="sxs-lookup"><span data-stu-id="bdaf7-388">Summary</span></span>

<span data-ttu-id="bdaf7-389">이 실습 실습을 완료 하면 **Database First** 방법과 **Code First** 방법을 사용 하 여 ASP.NET MVC 모델 및 데이터 액세스의 기본 사항을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-389">By completing this Hands-on Lab you have learned the fundamentals of ASP.NET MVC Models and Data Access, using the **Database First** approach as well as the **Code First** Approach:</span></span>

- <span data-ttu-id="bdaf7-390">데이터를 사용 하기 위해 솔루션에 데이터베이스를 추가 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bdaf7-390">How to add a database to the solution in order to consume its data</span></span>
- <span data-ttu-id="bdaf7-391">하드 코드 된 데이터 대신 데이터베이스에서 가져온 데이터를 사용 하 여 뷰 템플릿을 제공 하도록 컨트롤러를 업데이트 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bdaf7-391">How to update Controllers to provide View templates with the data taken from the database instead of hard-coded one</span></span>
- <span data-ttu-id="bdaf7-392">매개 변수를 사용 하 여 데이터베이스를 쿼리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bdaf7-392">How to query the database using parameters</span></span>
- <span data-ttu-id="bdaf7-393">데이터베이스 액세스의 수를 줄이고 보다 효율적인 방식으로 데이터를 검색 하는 기능인 쿼리 결과 셰이핑을 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bdaf7-393">How to use the Query Result Shaping, a feature that reduces the number of database accesses, retrieving data in a more efficient way</span></span>
- <span data-ttu-id="bdaf7-394">Microsoft Entity Framework에서 Database First 및 Code First 접근 방법을 사용 하 여 데이터베이스를 모델과 연결 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bdaf7-394">How to use both Database First and Code First approaches in Microsoft Entity Framework to link the database with the model</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="bdaf7-395">부록 A: 웹에 대 한 Visual Studio Express 2012 설치</span><span class="sxs-lookup"><span data-stu-id="bdaf7-395">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="bdaf7-396">**[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)** 를 사용 하 여 웹 또는 다른 &quot;Express&quot; 버전 **에 대해 Microsoft Visual Studio Express 2012** 를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-396">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="bdaf7-397">다음 지침에서는 *Microsoft 웹 플랫폼 설치 관리자*를 사용 하 여 *Visual studio Express 2012 for Web* 을 설치 하는 데 필요한 단계를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-397">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="bdaf7-398">[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-398">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="bdaf7-399">또는 웹 플랫폼 설치 관리자를 이미 설치한 경우에는 웹 플랫폼 설치 관리자를 열고 <em>Microsoft AZURE SDK&quot;를 사용 하 여 웹 용 2012 Visual Studio Express</em> &quot;제품을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-399">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="bdaf7-400">**지금 설치**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-400">Click on **Install Now**.</span></span> <span data-ttu-id="bdaf7-401">**웹 플랫폼 설치 관리자** 가 없으면 먼저이를 다운로드 하 여 설치 하도록 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-401">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="bdaf7-402">**웹 플랫폼 설치 관리자** 가 열리면 **설치** 를 클릭 하 여 설치를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-402">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="bdaf7-403">![Visual Studio Express 설치](aspnet-mvc-4-models-and-data-access/_static/image26.png "Visual Studio Express 설치")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-403">![Install Visual Studio Express](aspnet-mvc-4-models-and-data-access/_static/image26.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="bdaf7-404">*Visual Studio Express 설치*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-404">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="bdaf7-405">모든 제품의 라이선스 및 사용 조건을 읽고 **동의** 함을 클릭 하 여 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-405">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![사용 조건 동의](aspnet-mvc-4-models-and-data-access/_static/image27.png)

    <span data-ttu-id="bdaf7-407">*사용 조건 동의*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-407">*Accepting the license terms*</span></span>
5. <span data-ttu-id="bdaf7-408">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-408">Wait until the downloading and installation process completes.</span></span>

    ![설치 진행률](aspnet-mvc-4-models-and-data-access/_static/image28.png)

    <span data-ttu-id="bdaf7-410">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-410">*Installation progress*</span></span>
6. <span data-ttu-id="bdaf7-411">설치가 완료 되 면 **마침**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-411">When the installation completes, click **Finish**.</span></span>

    ![설치 완료](aspnet-mvc-4-models-and-data-access/_static/image29.png)

    <span data-ttu-id="bdaf7-413">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-413">*Installation completed*</span></span>
7. <span data-ttu-id="bdaf7-414">**끝내기** 를 클릭 하 여 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-414">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="bdaf7-415">웹에 대 한 Visual Studio Express를 열려면 **시작** 화면으로 이동 하 &quot;**VS Express**&quot;작성을 시작한 후 **VS Express for Web** 타일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-415">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 타일](aspnet-mvc-4-models-and-data-access/_static/image30.png)

    <span data-ttu-id="bdaf7-417">*VS Express for Web 타일*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-417">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="bdaf7-418">부록 B: 웹 배포을 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="bdaf7-418">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="bdaf7-419">이 부록에서는 windows azure 관리 포털에서 새 웹 사이트를 만들고 랩에 따라 가져온 응용 프로그램을 게시 하 여 Windows Azure에서 제공 하는 웹 배포 게시 기능을 활용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-419">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="bdaf7-420">작업 1-Windows Azure 포털에서 새 웹 사이트 만들기</span><span class="sxs-lookup"><span data-stu-id="bdaf7-420">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="bdaf7-421">[Windows Azure 관리 포털](https://manage.windowsazure.com/) 로 이동 하 고 구독과 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-421">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bdaf7-422">Windows Azure를 사용 하면 10 개의 ASP.NET 웹 사이트를 무료로 호스팅한 후 트래픽 증가에 따라 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-422">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="bdaf7-423">[여기](https://aka.ms/aspnet-hol-azure)에서 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-423">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="bdaf7-424">![Windows Azure Portal에 로그온 합니다.](aspnet-mvc-4-models-and-data-access/_static/image31.png "Windows Azure Portal에 로그온 합니다.")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-424">![Log on to Windows Azure portal](aspnet-mvc-4-models-and-data-access/_static/image31.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="bdaf7-425">*Windows Azure 관리 포털에 로그온 합니다.*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-425">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="bdaf7-426">명령 모음에서 **새로 만들기** 를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-426">Click **New** on the command bar.</span></span>

    <span data-ttu-id="bdaf7-427">![새 웹 사이트 만들기](aspnet-mvc-4-models-and-data-access/_static/image32.png "새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-427">![Creating a new Web Site](aspnet-mvc-4-models-and-data-access/_static/image32.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="bdaf7-428">*새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-428">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="bdaf7-429">**Compute** | **웹 사이트**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-429">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="bdaf7-430">그런 다음 **빠른 생성** 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-430">Then select **Quick Create** option.</span></span> <span data-ttu-id="bdaf7-431">새 웹 사이트에 사용할 수 있는 URL을 제공 하 고 **웹 사이트 만들기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-431">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bdaf7-432">Microsoft Azure 웹 사이트는 사용자가 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램에 대 한 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-432">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="bdaf7-433">빠른 생성 옵션을 사용 하면 포털 외부에서 Windows Azure 웹 사이트에 완료 된 웹 응용 프로그램을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-433">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="bdaf7-434">데이터베이스를 설정 하는 단계는 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-434">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="bdaf7-435">![빠른 생성을 사용 하 여 새 웹 사이트 만들기](aspnet-mvc-4-models-and-data-access/_static/image33.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-435">![Creating a new Web Site using Quick Create](aspnet-mvc-4-models-and-data-access/_static/image33.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="bdaf7-436">*빠른 생성을 사용 하 여 새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-436">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="bdaf7-437">새 **웹 사이트가** 만들어질 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-437">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="bdaf7-438">웹 사이트를 만든 후 **URL** 열 아래의 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-438">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="bdaf7-439">새 웹 사이트가 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-439">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="bdaf7-440">![새 웹 사이트로 이동](aspnet-mvc-4-models-and-data-access/_static/image34.png "새 웹 사이트로 이동")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-440">![Browsing to the new web site](aspnet-mvc-4-models-and-data-access/_static/image34.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="bdaf7-441">*새 웹 사이트로 이동*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-441">*Browsing to the new web site*</span></span>

    <span data-ttu-id="bdaf7-442">![웹 사이트 실행 중](aspnet-mvc-4-models-and-data-access/_static/image35.png "웹 사이트 실행 중")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-442">![Web site running](aspnet-mvc-4-models-and-data-access/_static/image35.png "Web site running")</span></span>

    <span data-ttu-id="bdaf7-443">*웹 사이트 실행 중*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-443">*Web site running*</span></span>
6. <span data-ttu-id="bdaf7-444">포털로 돌아가서 **이름** 열 아래에 있는 웹 사이트의 이름을 클릭 하 여 관리 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-444">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="bdaf7-445">![웹 사이트 관리 페이지 열기](aspnet-mvc-4-models-and-data-access/_static/image36.png "웹 사이트 관리 페이지 열기")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-445">![Opening the web site management pages](aspnet-mvc-4-models-and-data-access/_static/image36.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="bdaf7-446">*웹 사이트 관리 페이지 열기*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-446">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="bdaf7-447">**대시보드** 페이지의 **빠른** 보기 섹션에서 **게시 프로필 다운로드** 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-447">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bdaf7-448">*게시 프로필* 에는 사용 하도록 설정 된 각 게시 방법에 대해 웹 응용 프로그램을 Windows Azure 웹 사이트에 게시 하는 데 필요한 모든 정보가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-448">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="bdaf7-449">게시 프로필에는 게시 방법이 사용 설정된 각 엔드포인트에 연결하고 이에 대해 인증하는 데 필요한 URL, 사용자 자격 증명 및 데이터베이스 문자열이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-449">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="bdaf7-450">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** 및 **Microsoft Visual Studio 2012** 는 게시 프로필 읽기를 지원 하 여 웹 응용 프로그램을 Windows Azure 웹 사이트에 게시 하기 위해 이러한 프로그램의 구성을 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-450">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="bdaf7-451">![웹 사이트 게시 프로필을 다운로드 하는 중](aspnet-mvc-4-models-and-data-access/_static/image37.png "웹 사이트 게시 프로필을 다운로드 하는 중")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-451">![Downloading the web site publish profile](aspnet-mvc-4-models-and-data-access/_static/image37.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="bdaf7-452">*웹 사이트 게시 프로필을 다운로드 하는 중*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-452">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="bdaf7-453">알려진 위치에 게시 프로필 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-453">Download the publish profile file to a known location.</span></span> <span data-ttu-id="bdaf7-454">이 연습을 통해이 파일을 사용 하 여 Visual Studio에서 Windows Azure 웹 사이트에 웹 응용 프로그램을 게시 하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-454">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="bdaf7-455">![게시 프로필 파일을 저장 하는 중](aspnet-mvc-4-models-and-data-access/_static/image38.png "게시 프로필을 저장 하는 중")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-455">![Saving the publish profile file](aspnet-mvc-4-models-and-data-access/_static/image38.png "Saving the publish profile")</span></span>

    <span data-ttu-id="bdaf7-456">*게시 프로필 파일을 저장 하는 중*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-456">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="bdaf7-457">작업 2-데이터베이스 서버 구성</span><span class="sxs-lookup"><span data-stu-id="bdaf7-457">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="bdaf7-458">응용 프로그램에서 SQL Server 데이터베이스를 사용 하는 경우 SQL Database 서버를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-458">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="bdaf7-459">SQL Server 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 작업을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-459">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="bdaf7-460">응용 프로그램 데이터베이스를 저장 하기 위한 SQL Database 서버가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-460">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="bdaf7-461">Microsoft Azure 관리 포털의 구독에서 SQL Database 서버를 볼 수는 **SQL 데이터베이스** | **서버** | **서버의 대시보드**.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-461">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="bdaf7-462">만든 서버가 없는 경우 명령 모음에서 **추가** 단추를 사용 하 여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-462">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="bdaf7-463">다음 작업에서 사용할 **서버 이름과 URL, 관리자 로그인 이름 및 암호**를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-463">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="bdaf7-464">이후 단계에서 생성 되므로 아직 데이터베이스를 만들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-464">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="bdaf7-465">![SQL Database 서버 대시보드](aspnet-mvc-4-models-and-data-access/_static/image39.png "SQL Database 서버 대시보드")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-465">![SQL Database Server Dashboard](aspnet-mvc-4-models-and-data-access/_static/image39.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="bdaf7-466">*SQL Database 서버 대시보드*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-466">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="bdaf7-467">다음 작업에서는 Visual Studio에서 데이터베이스 연결을 테스트 합니다. 따라서 서버에서 **허용 되는 Ip 주소**목록에 로컬 IP 주소를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-467">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="bdaf7-468">이렇게 하려면 **구성**을 클릭 하 고, **현재 클라이언트 IP 주소** 에서 ip 주소를 선택 하 고, **시작 Ip 주소** 및 **끝 ip 주소** 텍스트 상자에 붙여 넣고, ![추가-클라이언트-ip 주소-확인 단추](aspnet-mvc-4-models-and-data-access/_static/image40.png) 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-468">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-models-and-data-access/_static/image40.png) button.</span></span>

    ![클라이언트 IP 주소를 추가 하는 중](aspnet-mvc-4-models-and-data-access/_static/image41.png)

    <span data-ttu-id="bdaf7-470">*클라이언트 IP 주소를 추가 하는 중*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-470">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="bdaf7-471">**클라이언트 Ip 주소가** 허용 된 ip 주소 목록에 추가 되 면 **저장** 을 클릭 하 여 변경 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-471">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![변경 내용 확인](aspnet-mvc-4-models-and-data-access/_static/image42.png)

    <span data-ttu-id="bdaf7-473">*변경 내용 확인*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-473">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="bdaf7-474">작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="bdaf7-474">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="bdaf7-475">ASP.NET MVC 4 솔루션으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-475">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="bdaf7-476">**솔루션 탐색기**에서 웹 사이트 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-476">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="bdaf7-477">![응용 프로그램 게시](aspnet-mvc-4-models-and-data-access/_static/image43.png "응용 프로그램 게시")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-477">![Publishing the Application](aspnet-mvc-4-models-and-data-access/_static/image43.png "Publishing the Application")</span></span>

    <span data-ttu-id="bdaf7-478">*웹 사이트 게시*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-478">*Publishing the web site*</span></span>
2. <span data-ttu-id="bdaf7-479">첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-479">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="bdaf7-480">![게시 프로필을 가져오는 중](aspnet-mvc-4-models-and-data-access/_static/image44.png "게시 프로필을 가져오는 중")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-480">![Importing the publish profile](aspnet-mvc-4-models-and-data-access/_static/image44.png "Importing the publish profile")</span></span>

    <span data-ttu-id="bdaf7-481">*게시 프로필을 가져오는 중*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-481">*Importing publish profile*</span></span>
3. <span data-ttu-id="bdaf7-482">**연결 유효성 검사**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-482">Click **Validate Connection**.</span></span> <span data-ttu-id="bdaf7-483">유효성 검사가 완료 되 면 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-483">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bdaf7-484">유효성 검사는 연결 유효성 검사 단추 옆에 녹색 확인 표시가 표시 되 면 완료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-484">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="bdaf7-485">![연결 유효성 검사](aspnet-mvc-4-models-and-data-access/_static/image45.png "연결 유효성 검사")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-485">![Validating connection](aspnet-mvc-4-models-and-data-access/_static/image45.png "Validating connection")</span></span>

    <span data-ttu-id="bdaf7-486">*연결 유효성 검사*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-486">*Validating connection*</span></span>
4. <span data-ttu-id="bdaf7-487">**설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆에 있는 단추 (즉, **defaultconnection**)를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-487">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="bdaf7-488">![웹 배포 구성](aspnet-mvc-4-models-and-data-access/_static/image46.png "웹 배포 구성")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-488">![Web deploy configuration](aspnet-mvc-4-models-and-data-access/_static/image46.png "Web deploy configuration")</span></span>

    <span data-ttu-id="bdaf7-489">*웹 배포 구성*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-489">*Web deploy configuration*</span></span>
5. <span data-ttu-id="bdaf7-490">데이터베이스 연결을 다음과 같이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-490">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="bdaf7-491">**서버 이름** 에 *tcp:* 접두사를 사용 하 여 SQL Database 서버 URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-491">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="bdaf7-492">**사용자 이름** 에 서버 관리자 로그인 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-492">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="bdaf7-493">**암호** 에 서버 관리자 로그인 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-493">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="bdaf7-494">새 데이터베이스 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-494">Type a new database name.</span></span>

     <span data-ttu-id="bdaf7-495">![대상 연결 문자열 구성](aspnet-mvc-4-models-and-data-access/_static/image47.png "대상 연결 문자열 구성")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-495">![Configuring destination connection string](aspnet-mvc-4-models-and-data-access/_static/image47.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="bdaf7-496">*대상 연결 문자열 구성*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-496">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="bdaf7-497">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-497">Then click **OK**.</span></span> <span data-ttu-id="bdaf7-498">데이터베이스를 만들 것인지 묻는 메시지가 표시 되 면 **예**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-498">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="bdaf7-499">![데이터베이스 만들기](aspnet-mvc-4-models-and-data-access/_static/image48.png "데이터베이스 문자열 만들기")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-499">![Creating the database](aspnet-mvc-4-models-and-data-access/_static/image48.png "Creating the database string")</span></span>

    <span data-ttu-id="bdaf7-500">*데이터베이스 만들기*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-500">*Creating the database*</span></span>
7. <span data-ttu-id="bdaf7-501">Windows Azure에서 SQL Database에 연결 하는 데 사용할 연결 문자열은 기본 연결 텍스트 상자 내에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-501">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="bdaf7-502">그런 후 **Next** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-502">Then click **Next**.</span></span>

    <span data-ttu-id="bdaf7-503">![SQL Database를 가리키는 연결 문자열](aspnet-mvc-4-models-and-data-access/_static/image49.png "SQL Database를 가리키는 연결 문자열")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-503">![Connection string pointing to SQL Database](aspnet-mvc-4-models-and-data-access/_static/image49.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="bdaf7-504">*SQL Database를 가리키는 연결 문자열*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-504">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="bdaf7-505">**미리 보기** 페이지에서 **게시**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-505">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="bdaf7-506">![웹 응용 프로그램 게시](aspnet-mvc-4-models-and-data-access/_static/image50.png "웹 응용 프로그램 게시")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-506">![Publishing the web application](aspnet-mvc-4-models-and-data-access/_static/image50.png "Publishing the web application")</span></span>

    <span data-ttu-id="bdaf7-507">*웹 응용 프로그램 게시*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-507">*Publishing the web application*</span></span>
9. <span data-ttu-id="bdaf7-508">게시 프로세스가 완료 되 면 기본 브라우저가 게시 된 웹 사이트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-508">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="bdaf7-509">부록 C: 코드 조각 사용</span><span class="sxs-lookup"><span data-stu-id="bdaf7-509">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="bdaf7-510">코드 조각을 사용 하면 필요한 모든 코드를 편리 하 게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-510">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="bdaf7-511">랩 문서는 다음 그림에 표시 된 것 처럼 사용자가 사용할 수 있는 경우를 정확 하 게 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-511">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="bdaf7-512">![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입](aspnet-mvc-4-models-and-data-access/_static/image51.png "Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-512">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-models-and-data-access/_static/image51.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="bdaf7-513">*Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-513">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="bdaf7-514">***키보드를 사용 하 여 코드 조각을 추가 하려면C# (만 해당)***</span><span class="sxs-lookup"><span data-stu-id="bdaf7-514">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="bdaf7-515">코드를 삽입할 위치에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-515">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="bdaf7-516">조각 이름 (공백 또는 하이픈 제외)을 입력 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-516">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="bdaf7-517">IntelliSense는 일치 하는 코드 조각의 이름을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-517">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="bdaf7-518">올바른 코드 조각을 선택 하거나 전체 코드 조각 이름이 선택 될 때까지 계속 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-518">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="bdaf7-519">Tab 키를 두 번 눌러 커서 위치에 코드 조각을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-519">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="bdaf7-520">![코드 조각 이름 입력 시작](aspnet-mvc-4-models-and-data-access/_static/image52.png "코드 조각 이름 입력 시작")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-520">![Start typing the snippet name](aspnet-mvc-4-models-and-data-access/_static/image52.png "Start typing the snippet name")</span></span>

<span data-ttu-id="bdaf7-521">*코드 조각 이름 입력 시작*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-521">*Start typing the snippet name*</span></span>

<span data-ttu-id="bdaf7-522">![Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.](aspnet-mvc-4-models-and-data-access/_static/image53.png "Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-522">![Press Tab to select the highlighted snippet](aspnet-mvc-4-models-and-data-access/_static/image53.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="bdaf7-523">*Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-523">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="bdaf7-524">![Tab 키를 다시 누르면 코드 조각이 확장 됩니다.](aspnet-mvc-4-models-and-data-access/_static/image54.png "Tab 키를 다시 누르면 코드 조각이 확장 됩니다.")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-524">![Press Tab again and the snippet will expand](aspnet-mvc-4-models-and-data-access/_static/image54.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="bdaf7-525">*Tab 키를 다시 누르면 코드 조각이 확장 됩니다.*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-525">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="bdaf7-526">***마우스C#(, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면*** 1(sp1).</span><span class="sxs-lookup"><span data-stu-id="bdaf7-526">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="bdaf7-527">코드 조각을 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-527">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="bdaf7-528">코드 **조각 삽입** 을 선택한 다음 **내 코드 조각을**선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-528">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="bdaf7-529">목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaf7-529">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="bdaf7-530">![코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.](aspnet-mvc-4-models-and-data-access/_static/image55.png "코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-530">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-models-and-data-access/_static/image55.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="bdaf7-531">*코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-531">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="bdaf7-532">![목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.](aspnet-mvc-4-models-and-data-access/_static/image56.png "목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="bdaf7-532">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-models-and-data-access/_static/image56.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="bdaf7-533">*목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="bdaf7-533">*Pick the relevant snippet from the list, by clicking on it*</span></span>
