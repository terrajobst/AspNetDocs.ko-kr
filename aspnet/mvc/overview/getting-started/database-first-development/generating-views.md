---
uid: mvc/overview/getting-started/database-first-development/generating-views
title: '자습서: ASP.NET MVC 앱을 사용 하 여 EF Database First에 대 한 보기 생성'
description: 이 자습서에서는 ASP.NET 스 캐 폴딩을 사용 하 여 컨트롤러 및 뷰를 생성 하는 방법을 집중적으로 다룹니다.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: 669367cf-8e30-4eb6-821d-10a7d9bb906c
msc.legacyurl: /mvc/overview/getting-started/database-first-development/generating-views
msc.type: authoredcontent
ms.openlocfilehash: e71e13e22d8a72e1699cfc70d4d93af603edba5b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499475"
---
# <a name="tutorial-generate-views-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="983e3-103">자습서: ASP.NET MVC 앱을 사용 하 여 EF Database First에 대 한 보기 생성</span><span class="sxs-lookup"><span data-stu-id="983e3-103">Tutorial: Generate views for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="983e3-104">MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="983e3-105">이 자습서 시리즈에서는 사용자가 데이터베이스 테이블에 있는 데이터를 표시, 편집, 만들기 및 삭제할 수 있도록 하는 코드를 자동으로 생성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="983e3-106">생성 된 코드는 데이터베이스 테이블의 열에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="983e3-107">이 자습서에서는 ASP.NET 스 캐 폴딩을 사용 하 여 컨트롤러 및 뷰를 생성 하는 방법을 집중적으로 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-107">This tutorial focuses on using ASP.NET Scaffolding to generate the controllers and views.</span></span>

<span data-ttu-id="983e3-108">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="983e3-109">스 캐 폴드 추가</span><span class="sxs-lookup"><span data-stu-id="983e3-109">Add scaffold</span></span>
> * <span data-ttu-id="983e3-110">새 뷰에 링크 추가</span><span class="sxs-lookup"><span data-stu-id="983e3-110">Add links to new views</span></span>
> * <span data-ttu-id="983e3-111">학생 보기 표시</span><span class="sxs-lookup"><span data-stu-id="983e3-111">Display student views</span></span>
> * <span data-ttu-id="983e3-112">등록 보기 표시</span><span class="sxs-lookup"><span data-stu-id="983e3-112">Display enrollment views</span></span>

## <a name="prerequisite"></a><span data-ttu-id="983e3-113">필수 요소</span><span class="sxs-lookup"><span data-stu-id="983e3-113">Prerequisite</span></span>

* [<span data-ttu-id="983e3-114">웹 응용 프로그램 및 데이터 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="983e3-114">Create the web application and data models</span></span>](creating-the-web-application.md)

## <a name="add-scaffold"></a><span data-ttu-id="983e3-115">스 캐 폴드 추가</span><span class="sxs-lookup"><span data-stu-id="983e3-115">Add scaffold</span></span>

<span data-ttu-id="983e3-116">모델 클래스에 대 한 표준 데이터 작업을 제공 하는 코드를 생성할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-116">You are ready to generate code that will provide standard data operations for the model classes.</span></span> <span data-ttu-id="983e3-117">스 캐 폴드 항목을 추가 하 여 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-117">You add the code by adding a scaffold item.</span></span> <span data-ttu-id="983e3-118">추가할 수 있는 스 캐 폴딩 유형에 대 한 다양 한 옵션이 있습니다. 이 자습서에서 스 캐 폴드는 이전 섹션에서 만든 학생 및 등록 모델에 해당 하는 컨트롤러 및 보기를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-118">There are many options for the type of scaffolding you can add; in this tutorial, the scaffold will include a controller and views that correspond to the Student and Enrollment models you created in the previous section.</span></span>

<span data-ttu-id="983e3-119">프로젝트에서 일관성을 유지 하기 위해 새 컨트롤러를 기존 **Controllers** 폴더에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-119">To maintain consistency in your project, you will add the new controller to the existing **Controllers** folder.</span></span> <span data-ttu-id="983e3-120">**Controllers** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** > **새 스 캐 폴드 항목**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-120">Right-click the **Controllers** folder, and select **Add** > **New Scaffolded Item**.</span></span>

<span data-ttu-id="983e3-121">Entity Framework 옵션 **을 사용 하 여 뷰가 포함 된 MVC 5 컨트롤러를** 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-121">Select the **MVC 5 Controller with views, using Entity Framework** option.</span></span> <span data-ttu-id="983e3-122">이 옵션은 모델에서 데이터를 업데이트, 삭제, 생성 및 표시 하기 위한 컨트롤러 및 뷰를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-122">This option will generate the controller and views for updating, deleting, creating and displaying the data in your model.</span></span>

![mvc 컨트롤러 추가](generating-views/_static/image2.png)

<span data-ttu-id="983e3-124">모델 클래스에 대해 **Student (ContosoSite)** 를 선택 하 고 컨텍스트 클래스에 대 한 **개체 (ContosoSite)** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-124">Select **Student (ContosoSite.Models)** for the model class and select the **ContosoUniversityDataEntities (ContosoSite.Models)** for the context class.</span></span> <span data-ttu-id="983e3-125">컨트롤러 이름을 **studentscontroller.cs**으로 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-125">Keep the controller name as **StudentsController**.</span></span>

<span data-ttu-id="983e3-126">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-126">Click **Add**.</span></span>

<span data-ttu-id="983e3-127">오류가 표시 되는 경우 이전 섹션에서 프로젝트를 빌드하지 않았기 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-127">If you receive an error, it may be because you did not build the project in the previous section.</span></span> <span data-ttu-id="983e3-128">그렇다면 프로젝트를 빌드한 다음 스 캐 폴드 항목을 다시 추가 하십시오.</span><span class="sxs-lookup"><span data-stu-id="983e3-128">If so, try building the project, and then add the scaffolded item again.</span></span>

<span data-ttu-id="983e3-129">코드 생성 프로세스가 완료 되 면 프로젝트의 **컨트롤러** 및 **뷰** > **학생** 폴더에 새 컨트롤러 및 뷰가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-129">After the code generation process is complete, you will see a new controller and views in your project's **Controllers** and **Views** > **Students** folders.</span></span>

<span data-ttu-id="983e3-130">동일한 단계를 다시 수행 하지만 **등록** 클래스에 대해 스 캐 폴드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-130">Perform the same steps again, but add a scaffold for the **Enrollment** class.</span></span> <span data-ttu-id="983e3-131">완료 되 면 **EnrollmentsController.cs** 파일이 있고 Create, Delete, Details, Edit 및 Index 뷰가 있는 **등록** **라는 이름의 폴더가** 있습니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-131">When finished, you have an **EnrollmentsController.cs** file, and a folder under **Views** named **Enrollments** with the Create, Delete, Details, Edit and Index views.</span></span>

## <a name="add-links-to-new-views"></a><span data-ttu-id="983e3-132">새 뷰에 링크 추가</span><span class="sxs-lookup"><span data-stu-id="983e3-132">Add links to new views</span></span>

<span data-ttu-id="983e3-133">새 보기를 쉽게 탐색할 수 있도록 학생 및 등록의 인덱스 보기에 두 개의 하이퍼링크를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-133">To make it easier for you to navigate to your new views, you can add a couple of hyperlinks to the Index views for students and enrollments.</span></span> <span data-ttu-id="983e3-134">사이트의 홈 페이지인 **보기** > **홈** > *인덱스*에서 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-134">Open the file at **Views** > **Home** > *Index.cshtml*, which is the home page for your site.</span></span> <span data-ttu-id="983e3-135">Jumbotron 아래에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-135">Add the following code below the jumbotron.</span></span>

[!code-cshtml[Main](generating-views/samples/sample1.cshtml)]

<span data-ttu-id="983e3-136">Html.actionlink 메서드의 경우 첫 번째 매개 변수는 링크에 표시 되는 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-136">For the ActionLink method, the first parameter is the text to display in the link.</span></span> <span data-ttu-id="983e3-137">두 번째 매개 변수는 작업이 고 세 번째 매개 변수는 컨트롤러의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-137">The second parameter is the action and the third parameter is the name of the controller.</span></span> <span data-ttu-id="983e3-138">예를 들어 첫 번째 링크는 Studentscontroller.cs의 인덱스 작업을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-138">For example, the first link points to the Index action in StudentsController.</span></span> <span data-ttu-id="983e3-139">실제 하이퍼링크는 이러한 값에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-139">The actual hyperlink is constructed from these values.</span></span> <span data-ttu-id="983e3-140">첫 번째 링크는 궁극적으로 **Views/학생용** 폴더 내의 **인덱스 cshtml** 파일로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-140">The first link ultimately takes users to the **Index.cshtml** file within the **Views/Students** folder.</span></span>

## <a name="display-student-views"></a><span data-ttu-id="983e3-141">학생 보기 표시</span><span class="sxs-lookup"><span data-stu-id="983e3-141">Display student views</span></span>

<span data-ttu-id="983e3-142">프로젝트에 추가 된 코드가 학생 목록을 올바르게 표시 하 고 사용자가 데이터베이스에서 학생 레코드를 편집, 생성 또는 삭제할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-142">You will verify that the code added to your project correctly displays a list of the students, and enables users to edit, create, or delete the student records in the database.</span></span>

<span data-ttu-id="983e3-143">**Home** > *Index* > **뷰** 를 마우스 오른쪽 단추로 클릭 하 고 **브라우저에서 보기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-143">Right-click the **Views** > **Home** > *Index.cshtml* file, and select **View in Browser**.</span></span> <span data-ttu-id="983e3-144">응용 프로그램 홈 페이지에서 **학생 목록**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-144">On the application home page, select **List of students**.</span></span>

![](generating-views/_static/image6.png)

<span data-ttu-id="983e3-145">**인덱스** 페이지에서 학생 목록과이 데이터를 수정할 링크를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-145">On the **Index** page, notice the list of the students and links to modify this data.</span></span> <span data-ttu-id="983e3-146">새 연결 **만들기** 링크를 선택 하 고 새 학생에 대 한 일부 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-146">Select the **Create New** link and provide some values for a new student.</span></span> <span data-ttu-id="983e3-147">**만들기**를 클릭 하면 새 학생이 목록에 추가 된 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-147">Click **Create**, and notice the new student is added to your list.</span></span>

<span data-ttu-id="983e3-148">**인덱스** 페이지로 돌아가서 **편집** 링크를 선택 하 고 학생에 대 한 일부 값을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-148">Back on the **Index** page, select the **Edit** link, and change some of the values for a student.</span></span> <span data-ttu-id="983e3-149">**저장**을 클릭 하면 학생 레코드가 변경 된 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-149">Click **Save**, and notice the student record has been changed.</span></span>

<span data-ttu-id="983e3-150">마지막으로, **삭제** 링크를 선택 하 고 **삭제** 단추를 클릭 하 여 레코드 삭제를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-150">Finally, select the **Delete** link and confirm that you want to delete the record by clicking the **Delete** button.</span></span>

<span data-ttu-id="983e3-151">코드를 작성 하지 않고도 학생 테이블의 데이터에 대 한 일반 작업을 수행 하는 뷰를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-151">Without writing any code, you have added views that perform common operations on the data in the Student table.</span></span>

<span data-ttu-id="983e3-152">필드에 대 한 텍스트 레이블이 데이터베이스 속성 (예: **LastName**)을 기반으로 한다는 것을 알고 있을 수 있습니다 .이는 웹 페이지에 표시할 내용이 반드시 필요한 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-152">You may have noticed that the text label for a field is based on the database property (such as **LastName**) which is not necessarily what you want to display on the web page.</span></span> <span data-ttu-id="983e3-153">예를 들어 레이블을 **성**으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-153">For example, you may prefer the label to be **Last Name**.</span></span> <span data-ttu-id="983e3-154">자습서의 뒷부분에서이 표시 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-154">You will fix this display issue later in the tutorial.</span></span>

## <a name="display-enrollment-views"></a><span data-ttu-id="983e3-155">등록 보기 표시</span><span class="sxs-lookup"><span data-stu-id="983e3-155">Display enrollment views</span></span>

<span data-ttu-id="983e3-156">데이터베이스에는 학생 및 등록 테이블 간에 일 대 다 관계가 포함 되 고 강좌와 등록 테이블 간의 일 대 다 관계가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-156">Your database includes a one-to-many relationship between the Student and Enrollment tables, and a one-to-many relationship between the Course and Enrollment tables.</span></span> <span data-ttu-id="983e3-157">등록에 대 한 뷰는 이러한 관계를 올바르게 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-157">The views for Enrollment correctly handle these relationships.</span></span> <span data-ttu-id="983e3-158">사이트의 홈 페이지로 이동 하 고 **등록 목록** 링크를 선택한 다음 **새로 만들기** 링크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-158">Navigate to the home page for your site and select the **List of enrollments** link and then the **Create New** link.</span></span>

<span data-ttu-id="983e3-159">이 보기에는 새 등록 레코드를 만들기 위한 양식이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-159">The view displays a form for creating a new enrollment record.</span></span> <span data-ttu-id="983e3-160">특히 **CourseID** 드롭다운 목록과 **StudentID** 드롭다운 목록이 폼에 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-160">In particular, notice that the form contains a **CourseID** drop-down list and a **StudentID** drop-down list.</span></span> <span data-ttu-id="983e3-161">둘 다 관련 테이블의 값으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-161">Both are populated with values from the related tables.</span></span>

<span data-ttu-id="983e3-162">또한 제공 된 값의 유효성 검사는 필드의 데이터 형식에 따라 자동으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-162">Furthermore, validation of the provided values is automatically applied based on the data type of the field.</span></span> <span data-ttu-id="983e3-163">**등급** 에는 숫자가 필요 하므로 호환 되지 않는 값을 제공 하려고 하면 오류 메시지가 표시 됩니다. *필드 등급은 숫자* 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-163">**Grade** requires a number, so an error message is displayed if you try to provide an incompatible value: *The field Grade must be a number.*</span></span>

<span data-ttu-id="983e3-164">자동 생성 된 뷰가 사용자가 데이터베이스의 데이터를 사용할 수 있도록 하는 것을 확인 했습니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-164">You have verified that the automatically-generated views enable users to work with the data in the database.</span></span> <span data-ttu-id="983e3-165">이 시리즈의 다음 자습서에서는 데이터베이스를 업데이트 하 고 웹 응용 프로그램에서 해당 변경 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-165">In the next tutorial in this series, you will update the database and make the corresponding changes in the web application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="983e3-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="983e3-166">Next steps</span></span>

<span data-ttu-id="983e3-167">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-167">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="983e3-168">스 캐 폴드 추가 됨</span><span class="sxs-lookup"><span data-stu-id="983e3-168">Added scaffold</span></span>
> * <span data-ttu-id="983e3-169">새 뷰에 링크 추가 됨</span><span class="sxs-lookup"><span data-stu-id="983e3-169">Added links to new views</span></span>
> * <span data-ttu-id="983e3-170">표시 된 학생 보기</span><span class="sxs-lookup"><span data-stu-id="983e3-170">Displayed student views</span></span>
> * <span data-ttu-id="983e3-171">표시 된 등록 보기</span><span class="sxs-lookup"><span data-stu-id="983e3-171">Displayed enrollment views</span></span>

<span data-ttu-id="983e3-172">데이터베이스를 변경 하는 방법을 알아보려면 다음 자습서로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="983e3-172">Advance to the next tutorial to learn how to change the database.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="983e3-173">데이터베이스 변경</span><span class="sxs-lookup"><span data-stu-id="983e3-173">Change the database</span></span>](changing-the-database.md)