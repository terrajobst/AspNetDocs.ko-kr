---
uid: mvc/overview/getting-started/database-first-development/changing-the-database
title: '자습서: ASP.NET MVC 앱을 사용 하 여 EF Database First에 대 한 데이터베이스 변경'
description: 이 자습서에서는 데이터베이스 구조에 대 한 업데이트를 수행 하 고 웹 응용 프로그램 전체에서 해당 변경 내용을 전파 하는 방법을 집중적으로 설명 합니다.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: cfd5c083-a319-482e-8f25-5b38caa93954
msc.legacyurl: /mvc/overview/getting-started/database-first-development/changing-the-database
msc.type: authoredcontent
ms.openlocfilehash: 52cad1120908cf0d4f85770f8e2690f9415c5f56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499523"
---
# <a name="tutorial-change-the-database-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="3f291-103">자습서: ASP.NET MVC 앱을 사용 하 여 EF Database First에 대 한 데이터베이스 변경</span><span class="sxs-lookup"><span data-stu-id="3f291-103">Tutorial: Change the database for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="3f291-104">MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="3f291-105">이 자습서 시리즈에서는 사용자가 데이터베이스 테이블에 있는 데이터를 표시, 편집, 만들기 및 삭제할 수 있도록 하는 코드를 자동으로 생성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="3f291-106">생성 된 코드는 데이터베이스 테이블의 열에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="3f291-107">이 자습서에서는 데이터베이스 구조에 대 한 업데이트를 수행 하 고 웹 응용 프로그램 전체에서 해당 변경 내용을 전파 하는 방법을 집중적으로 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-107">This tutorial focuses on making an update to the database structure and propagating that change throughout the web application.</span></span>

<span data-ttu-id="3f291-108">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3f291-109">열 추가</span><span class="sxs-lookup"><span data-stu-id="3f291-109">Add a column</span></span>
> * <span data-ttu-id="3f291-110">뷰에 속성 추가</span><span class="sxs-lookup"><span data-stu-id="3f291-110">Add the property to the views</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f291-111">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="3f291-111">Prerequisites</span></span>

* [<span data-ttu-id="3f291-112">뷰 생성</span><span class="sxs-lookup"><span data-stu-id="3f291-112">Generating views</span></span>](generating-views.md)

## <a name="add-a-column"></a><span data-ttu-id="3f291-113">열 추가</span><span class="sxs-lookup"><span data-stu-id="3f291-113">Add a column</span></span>

<span data-ttu-id="3f291-114">데이터베이스의 테이블 구조를 업데이트 하는 경우 변경 내용이 데이터 모델, 뷰 및 컨트롤러에 전파 되는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-114">If you update the structure of a table in your database, you need to ensure that your change is propagated to the data model, views, and controller.</span></span>

<span data-ttu-id="3f291-115">이 자습서에서는 학생 테이블에 새 열을 추가 하 여 학생의 중간 이름을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-115">For this tutorial, you will add a new column to the Student table to record the middle name of the student.</span></span> <span data-ttu-id="3f291-116">이 열을 추가 하려면 데이터베이스 프로젝트를 열고 Student .sql 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-116">To add this column, open the database project, and open the Student.sql file.</span></span> <span data-ttu-id="3f291-117">디자이너나 T-sql 코드를 통해 NVARCHAR (50) 인 **MiddleName** 라는 열을 추가 하 고 NULL 값을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-117">Through either the designer or the T-SQL code, add a column named **MiddleName** that is an NVARCHAR(50) and allows NULL values.</span></span>

<span data-ttu-id="3f291-118">데이터베이스 프로젝트 (또는 F5)를 시작 하 여이 변경 내용을 로컬 데이터베이스에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-118">Deploy this change to your local database by starting your database project (or F5).</span></span> <span data-ttu-id="3f291-119">새 필드가 테이블에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-119">The new field is added to the table.</span></span> <span data-ttu-id="3f291-120">SQL Server 개체 탐색기에 표시 되지 않으면 창에서 새로 고침 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-120">If you do not see it in the SQL Server Object Explorer, click the Refresh button in the pane.</span></span>

![새 열 표시](changing-the-database/_static/image2.png)

<span data-ttu-id="3f291-122">데이터베이스 테이블에 새 열이 있지만 현재 데이터 모델 클래스에 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-122">The new column exists in the database table, but it does not currently exist in the data model class.</span></span> <span data-ttu-id="3f291-123">새 열을 포함 하도록 모델을 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-123">You must update the model to include your new column.</span></span> <span data-ttu-id="3f291-124">**모델 폴더에서** **ContosoModel** 파일을 열어 모델 다이어그램을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-124">In the **Models** folder, open the **ContosoModel.edmx** file to display the model diagram.</span></span> <span data-ttu-id="3f291-125">학생 모델에는 MiddleName 속성이 포함 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-125">Notice that the Student model does not contain the MiddleName property.</span></span> <span data-ttu-id="3f291-126">디자인 화면에서 아무 곳 이나 마우스 오른쪽 단추로 클릭 하 고 **데이터베이스에서 모델 업데이트**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-126">Right-click anywhere on the design surface, and select **Update Model from Database**.</span></span>

<span data-ttu-id="3f291-127">업데이트 마법사에서 **새로 고침** 탭을 선택한 다음 **테이블** > **dbo** > **Student**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-127">In the Update Wizard, select the **Refresh** tab and then select **Tables** > **dbo** > **Student**.</span></span> <span data-ttu-id="3f291-128">**Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-128">Click **Finish**.</span></span>

<span data-ttu-id="3f291-129">업데이트 프로세스가 완료 되 면 데이터베이스 다이어그램에 새 **MiddleName** 속성이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-129">After the update process is finished, the database diagram includes the new **MiddleName** property.</span></span> <span data-ttu-id="3f291-130">**ContosoModel** 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-130">Save the **ContosoModel.edmx** file.</span></span> <span data-ttu-id="3f291-131">**Student.cs** 클래스로 전파 될 새 속성에 대해이 파일을 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-131">You must save this file for the new property to be propagated to the **Student.cs** class.</span></span> <span data-ttu-id="3f291-132">이제 데이터베이스 및 모델이 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-132">You have now updated the database and the model.</span></span>

<span data-ttu-id="3f291-133">솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-133">Build the solution.</span></span>

## <a name="add-the-property-to-the-views"></a><span data-ttu-id="3f291-134">뷰에 속성 추가</span><span class="sxs-lookup"><span data-stu-id="3f291-134">Add the property to the views</span></span>

<span data-ttu-id="3f291-135">불행 하 게도 보기에는 새 속성이 포함 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-135">Unfortunately, the views still do not contain the new property.</span></span> <span data-ttu-id="3f291-136">뷰를 업데이트 하려면 두 가지 옵션이 있습니다. 학생 클래스의 스 캐 폴딩을 다시 추가 하 여 뷰를 다시 생성 하거나 기존 보기에 새 속성을 수동으로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-136">To update the views you have two options - you can either re-generate the views by once again adding scaffolding for the Student class, or you can manually add the new property to your existing views.</span></span> <span data-ttu-id="3f291-137">이 자습서에서는 자동으로 생성 된 뷰에 대해 사용자 지정 된 변경을 수행 하지 않았으므로 스 캐 폴딩을 다시 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-137">In this tutorial, you will add the scaffolding again because you have not made any customized changes to the automatically-generated views.</span></span> <span data-ttu-id="3f291-138">뷰를 변경 하 고 해당 변경 내용을 잃지 않으려는 경우 속성을 수동으로 추가 하는 것을 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-138">You might consider manually adding the property when you have made changes to the views and do not want to lose those changes.</span></span>

<span data-ttu-id="3f291-139">뷰가 다시 생성 되도록 하려면 **보기**아래에서 **학생** 폴더를 삭제 하 고 **studentscontroller.cs**를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-139">To ensure the views are re-created, delete the **Students** folder under **Views**, and delete the **StudentsController**.</span></span> <span data-ttu-id="3f291-140">그런 다음 **Controllers** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **학생** 모델에 스 캐 폴딩을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-140">Then, right-click the **Controllers** folder and add scaffolding for the **Student** model.</span></span> <span data-ttu-id="3f291-141">다시 컨트롤러 이름을 **studentscontroller.cs**로 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-141">Again, name the controller **StudentsController**.</span></span> <span data-ttu-id="3f291-142">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-142">Select **Add**.</span></span>

<span data-ttu-id="3f291-143">솔루션을 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-143">Build the solution again.</span></span> <span data-ttu-id="3f291-144">뷰에 MiddleName 속성이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-144">The views now contain the MiddleName property.</span></span>

![중간 이름 표시](changing-the-database/_static/image5.png)

## <a name="next-steps"></a><span data-ttu-id="3f291-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3f291-146">Next steps</span></span>

<span data-ttu-id="3f291-147">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-147">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3f291-148">열 추가</span><span class="sxs-lookup"><span data-stu-id="3f291-148">Added a column</span></span>
> * <span data-ttu-id="3f291-149">뷰에 속성을 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-149">Added the property to the views</span></span>

<span data-ttu-id="3f291-150">학생 레코드에 대 한 세부 정보를 표시 하기 위해 보기를 사용자 지정 하는 방법을 알아보려면 다음 자습서로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f291-150">Advance to the next tutorial to learn how to customize the view for showing details about a student record.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="3f291-151">보기 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="3f291-151">Customize a view</span></span>](customizing-a-view.md)