---
uid: mvc/overview/getting-started/database-first-development/creating-the-web-application
title: '자습서: ASP.NET MVC를 사용 하 여 EF Database First 용 웹 응용 프로그램 및 데이터 모델 만들기'
description: 이 자습서에서는 웹 응용 프로그램을 만들고 데이터베이스 테이블을 기반으로 데이터 모델을 생성 하는 방법을 집중적으로 설명 합니다.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: bc8f2bd5-ff57-4dcd-8418-a5bd517d8953
msc.legacyurl: /mvc/overview/getting-started/database-first-development/creating-the-web-application
msc.type: authoredcontent
ms.openlocfilehash: 30fd42be5677df6fa6ee0630914098c30d21385b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499529"
---
# <a name="tutorial-create-the-web-application-and-data-models-for-ef-database-first-with-aspnet-mvc"></a><span data-ttu-id="497bf-103">자습서: ASP.NET MVC를 사용 하 여 EF Database First 용 웹 응용 프로그램 및 데이터 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="497bf-103">Tutorial: Create the Web Application and Data Models for EF Database First with ASP.NET MVC</span></span>

 <span data-ttu-id="497bf-104">MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="497bf-105">이 자습서 시리즈에서는 사용자가 데이터베이스 테이블에 있는 데이터를 표시, 편집, 만들기 및 삭제할 수 있도록 하는 코드를 자동으로 생성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="497bf-106">생성 된 코드는 데이터베이스 테이블의 열에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="497bf-107">이 자습서에서는 웹 응용 프로그램을 만들고 데이터베이스 테이블을 기반으로 데이터 모델을 생성 하는 방법을 집중적으로 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-107">This tutorial focuses on creating the web application, and generating the data models based on your database tables.</span></span>

<span data-ttu-id="497bf-108">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="497bf-109">ASP.NET 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="497bf-109">Create an ASP.NET web app</span></span>
> * <span data-ttu-id="497bf-110">모델 생성</span><span class="sxs-lookup"><span data-stu-id="497bf-110">Generate the models</span></span>

## <a name="prerequisites"></a><span data-ttu-id="497bf-111">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="497bf-111">Prerequisites</span></span>

* [<span data-ttu-id="497bf-112">MVC 5를 사용 하 여 Entity Framework 6 Database First 시작 하기</span><span class="sxs-lookup"><span data-stu-id="497bf-112">Getting started with Entity Framework 6 Database First using MVC 5</span></span>](setting-up-database.md)

## <a name="create-an-aspnet-web-app"></a><span data-ttu-id="497bf-113">ASP.NET 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="497bf-113">Create an ASP.NET web app</span></span>

<span data-ttu-id="497bf-114">새 솔루션이 나 데이터베이스 프로젝트와 동일한 솔루션에서 Visual Studio에서 새 프로젝트를 만들고 **ASP.NET 웹 응용 프로그램** 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-114">In either a new solution or the same solution as the database project, create a new project in Visual Studio and select the **ASP.NET Web Application** template.</span></span> <span data-ttu-id="497bf-115">프로젝트 이름을 **ContosoSite**로 합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-115">Name the project **ContosoSite**.</span></span>

![프로젝트 만들기](creating-the-web-application/_static/image1.png)

<span data-ttu-id="497bf-117">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-117">Click **OK**.</span></span>

<span data-ttu-id="497bf-118">새 ASP.NET 프로젝트 창에서 **MVC** 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-118">In the New ASP.NET Project window, select the **MVC** template.</span></span> <span data-ttu-id="497bf-119">나중에 응용 프로그램을 클라우드에 배포 하기 때문에 지금은 **클라우드 옵션에서 호스트** 를 지울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-119">You can clear the **Host in the cloud** option for now because you will deploy the application to the cloud later.</span></span> <span data-ttu-id="497bf-120">**확인** 을 클릭 하 여 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-120">Click **OK** to create the application.</span></span>

<span data-ttu-id="497bf-121">프로젝트는 기본 파일 및 폴더를 사용 하 여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-121">The project is created with the default files and folders.</span></span>

<span data-ttu-id="497bf-122">이 자습서에서는 Entity Framework 6을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-122">In this tutorial, you will use Entity Framework 6.</span></span> <span data-ttu-id="497bf-123">NuGet 패키지 관리 창을 통해 프로젝트의 Entity Framework 버전을 두 번 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-123">You can double-check the version of Entity Framework in your project through the Manage NuGet Packages window.</span></span> <span data-ttu-id="497bf-124">필요한 경우 Entity Framework 버전을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-124">If necessary, update your version of Entity Framework.</span></span>

![버전 표시](creating-the-web-application/_static/image3.png)

## <a name="generate-the-models"></a><span data-ttu-id="497bf-126">모델 생성</span><span class="sxs-lookup"><span data-stu-id="497bf-126">Generate the models</span></span>

<span data-ttu-id="497bf-127">이제 데이터베이스 테이블에서 Entity Framework 모델을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-127">You will now create Entity Framework models from the database tables.</span></span> <span data-ttu-id="497bf-128">이러한 모델은 데이터 작업에 사용 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-128">These models are classes that you will use to work with the data.</span></span> <span data-ttu-id="497bf-129">각 모델은 데이터베이스의 테이블을 미러링 하 고 테이블의 열에 해당 하는 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-129">Each model mirrors a table in the database and contains properties that correspond to the columns in the table.</span></span>

<span data-ttu-id="497bf-130">**모델** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** 및 **새 항목**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-130">Right-click the **Models** folder, and select **Add** and **New Item**.</span></span>

<span data-ttu-id="497bf-131">새 항목 추가 창의 왼쪽 창에서 **데이터** 를 선택 하 고 가운데 창의 옵션에서 **엔터티 데이터 모델 ADO.NET** 합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-131">In the Add New Item window, select **Data** in the left pane and **ADO.NET Entity Data Model** from the options in the center pane.</span></span> <span data-ttu-id="497bf-132">새 모델 파일의 이름을 **ContosoModel**로 합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-132">Name the new model file **ContosoModel**.</span></span>

<span data-ttu-id="497bf-133">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-133">Click **Add**.</span></span>

<span data-ttu-id="497bf-134">엔터티 데이터 모델 마법사에서 **데이터베이스의 EF Designer**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-134">In the Entity Data Model Wizard, select **EF Designer from database**.</span></span>

<span data-ttu-id="497bf-135">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-135">Click **Next**.</span></span>

<span data-ttu-id="497bf-136">개발 환경 내에서 데이터베이스 연결을 정의한 경우 이러한 연결 중 하나가 미리 선택 된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-136">If you have database connections defined within your development environment, you may see one of these connections pre-selected.</span></span> <span data-ttu-id="497bf-137">그러나이 자습서의 첫 번째 부분에서 만든 데이터베이스에 대 한 새 연결을 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-137">However, you want to create a new connection to the database you created in the first part of this tutorial.</span></span> <span data-ttu-id="497bf-138">**새 연결** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-138">Click the **New Connection** button.</span></span>

<span data-ttu-id="497bf-139">연결 속성 창에서 데이터베이스가 생성 된 로컬 서버의 이름 (이 경우 **localdb) \ProjectsV13**)을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-139">In the Connection Properties window, provide the name of the local server where your database was created (in this case **(localdb)\ProjectsV13**).</span></span> <span data-ttu-id="497bf-140">서버 이름을 제공한 후 사용 가능한 데이터베이스에서 해당 데이터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-140">After providing the server name, select the ContosoUniversityData from the available databases.</span></span>

![연결 속성 설정](creating-the-web-application/_static/image8.png)

<span data-ttu-id="497bf-142">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-142">Click **OK**.</span></span>

<span data-ttu-id="497bf-143">이제 올바른 연결 속성이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-143">The correct connection properties are now displayed.</span></span> <span data-ttu-id="497bf-144">Web.config 파일에서 연결에 기본 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-144">You can use the default name for connection in the Web.Config file.</span></span>

<span data-ttu-id="497bf-145">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-145">Click **Next**.</span></span>

<span data-ttu-id="497bf-146">최신 버전의 Entity Framework을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-146">Select the latest version of Entity Framework.</span></span>

<span data-ttu-id="497bf-147">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-147">Click **Next**.</span></span>

<span data-ttu-id="497bf-148">세 테이블 모두에 대해 모델을 생성 하려면 **테이블** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-148">Select **Tables** to generate models for all three tables.</span></span>

<span data-ttu-id="497bf-149">**Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-149">Click **Finish**.</span></span>

<span data-ttu-id="497bf-150">보안 경고가 표시 되 면 **확인** 을 선택 하 여 템플릿을 계속 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-150">If you receive a security warning, select **OK** to continue running the template.</span></span>

<span data-ttu-id="497bf-151">데이터베이스 테이블에서 모델을 생성 하 고 테이블 간의 속성 및 관계를 보여 주는 다이어그램이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-151">The models are generated from the database tables, and a diagram is displayed that shows the properties and relationships between the tables.</span></span>

![모델 다이어그램](creating-the-web-application/_static/image11.png)

<span data-ttu-id="497bf-153">이제 모델 폴더에는 데이터베이스에서 생성 된 모델과 관련 된 많은 새 파일이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-153">The Models folder now includes many new files related to the models that were generated from the database.</span></span>

<span data-ttu-id="497bf-154">**ContosoModel.Context.cs** 파일은 **DbContext** 클래스에서 파생 되는 클래스를 포함 하며 데이터베이스 테이블에 해당 하는 각 모델 클래스에 대 한 속성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-154">The **ContosoModel.Context.cs** file contains a class that derives from the **DbContext** class, and provides a property for each model class that corresponds to a database table.</span></span> <span data-ttu-id="497bf-155">**Course.cs**, **Enrollment.cs**및 **Student.cs** 파일은 데이터베이스 테이블을 나타내는 모델 클래스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-155">The **Course.cs**, **Enrollment.cs**, and **Student.cs** files contain the model classes that represent the databases tables.</span></span> <span data-ttu-id="497bf-156">스 캐 폴딩으로 작업할 때 컨텍스트 클래스와 모델 클래스를 모두 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-156">You will use both the context class and the model classes when working with scaffolding.</span></span>

<span data-ttu-id="497bf-157">이 자습서를 진행 하기 전에 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-157">Before proceeding with this tutorial, build the project.</span></span> <span data-ttu-id="497bf-158">다음 섹션에서는 데이터 모델을 기반으로 코드를 생성 하지만 프로젝트가 빌드되지 않은 경우 해당 섹션은 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-158">In the next section, you will generate code based on the data models, but that section will not work if the project has not been built.</span></span>

## <a name="next-steps"></a><span data-ttu-id="497bf-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="497bf-159">Next steps</span></span>

<span data-ttu-id="497bf-160">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-160">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="497bf-161">ASP.NET 웹 앱을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-161">Created an ASP.NET web app</span></span>
> * <span data-ttu-id="497bf-162">생성 된 모델</span><span class="sxs-lookup"><span data-stu-id="497bf-162">Generated the models</span></span>

<span data-ttu-id="497bf-163">데이터 모델을 기반으로 코드 생성을 만드는 방법을 알아보려면 다음 자습서로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="497bf-163">Advance to the next tutorial to learn how to create generate code based on the data models.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="497bf-164">뷰 생성</span><span class="sxs-lookup"><span data-stu-id="497bf-164">Generating views</span></span>](generating-views.md)
