---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: ASP.NET MVC 응용 프로그램에서 Entity Framework로 상속 구현 (8/10) | Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다.
ms.author: riande
ms.date: 07/30/2013
ms.assetid: a5c3feff-5335-4cdd-a97d-f7a8785c2494
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9507cba71b976825257cc9948d54f2651355959d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595315"
---
# <a name="implementing-inheritance-with-the-entity-framework-in-an-aspnet-mvc-application-8-of-10"></a><span data-ttu-id="21bb6-103">ASP.NET MVC 응용 프로그램에서 Entity Framework로 상속 구현 (8/10)</span><span class="sxs-lookup"><span data-stu-id="21bb6-103">Implementing Inheritance with the Entity Framework in an ASP.NET MVC Application (8 of 10)</span></span>

<span data-ttu-id="21bb6-104">만든 사람 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="21bb6-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="21bb6-105">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="21bb6-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="21bb6-106">Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 5 Code First 및 Visual Studio 2012을 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="21bb6-107">자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21bb6-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="21bb6-108">[이 챕터의](building-the-ef5-mvc4-chapter-downloads.md) 시작 또는 시작 프로젝트 다운로드에서 자습서 시리즈를 시작 하 고 여기에서 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="21bb6-109">해결할 수 없는 문제가 발생 하는 경우 [완료 된 챕터를 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 하 여 문제를 재현해 보세요.</span><span class="sxs-lookup"><span data-stu-id="21bb6-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="21bb6-110">일반적으로 코드를 완성 된 코드와 비교 하 여 문제에 대 한 솔루션을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="21bb6-111">몇 가지 일반적인 오류 및 해결 방법에 대 한 자세한 내용은 [오류 및 해결](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors) 방법을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="21bb6-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>

<span data-ttu-id="21bb6-112">이전 자습서에서는 동시성 예외를 처리 했습니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-112">In the previous tutorial you handled concurrency exceptions.</span></span> <span data-ttu-id="21bb6-113">이 자습서에서는 데이터 모델에서 상속을 구현하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-113">This tutorial will show you how to implement inheritance in the data model.</span></span>

<span data-ttu-id="21bb6-114">개체 지향 프로그래밍에서는 상속을 사용 하 여 중복 코드를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-114">In object-oriented programming, you can use inheritance to eliminate redundant code.</span></span> <span data-ttu-id="21bb6-115">이 자습서에서는 강사와 학생 모두에게 공통적인 속성(예: `LastName`)이 포함된 `Person` 기본 클래스에서 클래스가 파생되도록 `Instructor` 및 `Student` 클래스를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-115">In this tutorial, you'll change the `Instructor` and `Student` classes so that they derive from a `Person` base class which contains properties such as `LastName` that are common to both instructors and students.</span></span> <span data-ttu-id="21bb6-116">웹 페이지를 추가하거나 변경하지는 않지만 일부 코드를 변경하고 이러한 변경 내용이 데이터베이스에 자동으로 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-116">You won't add or change any web pages, but you'll change some of the code and those changes will be automatically reflected in the database.</span></span>

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a><span data-ttu-id="21bb6-117">계층당 하나의 테이블 및 형식당 하나의 테이블 상속</span><span class="sxs-lookup"><span data-stu-id="21bb6-117">Table-per-Hierarchy versus Table-per-Type Inheritance</span></span>

<span data-ttu-id="21bb6-118">개체 지향 프로그래밍에서는 상속을 사용 하 여 관련 클래스 작업을 보다 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-118">In object-oriented programming, you can use inheritance to make it easier to work with related classes.</span></span> <span data-ttu-id="21bb6-119">예를 들어 `School` 데이터 모델의 `Instructor` 및 `Student` 클래스는 중복 된 코드를 생성 하는 여러 속성을 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-119">For example, the `Instructor` and `Student` classes in the `School` data model share several properties, which results in redundant code:</span></span>

![Student_and_Instructor_classes](https://asp.net/media/2578113/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_e7a32f99-8bc4-48ce-aeaf-216a18071a8b.png)

<span data-ttu-id="21bb6-121">`Instructor` 및 `Student` 엔터티에서 공유하는 속성에 대해 중복 코드를 제거하려고 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-121">Suppose you want to eliminate the redundant code for the properties that are shared by the `Instructor` and `Student` entities.</span></span> <span data-ttu-id="21bb6-122">다음 그림과 같이 해당 공유 속성만 포함 하는 `Person` 기본 클래스를 만든 다음 `Instructor` 및 `Student` 엔터티가 해당 기본 클래스에서 상속 하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-122">You could create a `Person` base class which contains only those shared properties, then make the `Instructor` and `Student` entities inherit from that base class, as shown in the following illustration:</span></span>

![Student_and_Instructor_classes_deriving_from_Person_class](https://asp.net/media/2578119/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_deriving_from_Person_class_671d708c-cbb8-454a-a8f8-c2d99439acd9.png)

<span data-ttu-id="21bb6-124">데이터베이스에 이 상속 구조를 여러 가지 방법으로 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-124">There are several ways this inheritance structure could be represented in the database.</span></span> <span data-ttu-id="21bb6-125">학생 및 강사 모두에 대 한 정보를 단일 테이블에 포함 하는 `Person` 테이블이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-125">You could have a `Person` table that includes information about both students and instructors in a single table.</span></span> <span data-ttu-id="21bb6-126">일부 열은 강사 (`HireDate`) 에게만 적용 되 고 일부는 학생 (`EnrollmentDate`)에만 적용 되 고 일부는 둘 다 (`LastName`, `FirstName`)에만 적용 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-126">Some of the columns could apply only to instructors (`HireDate`), some only to students (`EnrollmentDate`), some to both (`LastName`, `FirstName`).</span></span> <span data-ttu-id="21bb6-127">일반적으로 각 행이 나타내는 형식을 나타내는 *판별자* 열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-127">Typically, you'd have a *discriminator* column to indicate which type each row represents.</span></span> <span data-ttu-id="21bb6-128">예를 들어, 판별자 열은 강사에 대해 "Instructor"를, 학생에 대해 "Student"를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-128">For example, the discriminator column might have "Instructor" for instructors and "Student" for students.</span></span>

![테이블당 테이블 수 hierarchy_example](https://asp.net/media/2578125/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-hierarchy_example_244067cd-b451-4e9b-9595-793b9afca505.png)

<span data-ttu-id="21bb6-130">단일 데이터베이스 테이블에서 엔터티 상속 구조를 생성 하는이 패턴은 TPH ( *계층당 하나의 테이블* ) 상속 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-130">This pattern of generating an entity inheritance structure from a single database table is called *table-per-hierarchy* (TPH) inheritance.</span></span>

<span data-ttu-id="21bb6-131">다른 방법은 데이터베이스를 상속 구조와 유사하게 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-131">An alternative is to make the database look more like the inheritance structure.</span></span> <span data-ttu-id="21bb6-132">예를 들어 `Person` 테이블에 이름 필드만 포함 하 고 날짜 필드를 사용 하 여 별도의 `Instructor` 및 `Student` 테이블을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-132">For example, you could have only the name fields in the `Person` table and have separate `Instructor` and `Student` tables with the date fields.</span></span>

![테이블당 테이블 수 type_inheritance](https://asp.net/media/2578131/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-type_inheritance.png)

<span data-ttu-id="21bb6-134">각 엔터티 클래스에 대 한 데이터베이스 테이블을 만드는이 패턴을 TPT (형식당 *하나의 테이블* ) 상속 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-134">This pattern of making a database table for each entity class is called *table per type* (TPT) inheritance.</span></span>

<span data-ttu-id="21bb6-135">TPH 상속 패턴 Entity Framework은 일반적으로 TPT 상속 패턴 보다 더 나은 성능을 제공 합니다. TPT 패턴은 복잡 한 조인 쿼리를 발생 시킬 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-135">TPH inheritance patterns generally deliver better performance in the Entity Framework than TPT inheritance patterns, because TPT patterns can result in complex join queries.</span></span> <span data-ttu-id="21bb6-136">이 자습서에서는 TPH 상속을 구현하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-136">This tutorial demonstrates how to implement TPH inheritance.</span></span> <span data-ttu-id="21bb6-137">이렇게 하려면 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-137">You'll do that by performing the following steps:</span></span>

- <span data-ttu-id="21bb6-138">`Person` 클래스를 만들고 `Person`에서 파생 되도록 `Instructor` 및 `Student` 클래스를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-138">Create a `Person` class and change the `Instructor` and `Student` classes to derive from `Person`.</span></span>
- <span data-ttu-id="21bb6-139">데이터베이스 컨텍스트 클래스에 모델-데이터베이스 매핑 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-139">Add model-to-database mapping code to the database context class.</span></span>
- <span data-ttu-id="21bb6-140">프로젝트 전체에서 `InstructorID` 및 `StudentID` 참조를 `PersonID`로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-140">Change `InstructorID` and `StudentID` references throughout the project to `PersonID`.</span></span>

## <a name="creating-the-person-class"></a><span data-ttu-id="21bb6-141">Person 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="21bb6-141">Creating the Person Class</span></span>

 <span data-ttu-id="21bb6-142">참고: 이러한 클래스를 사용 하는 컨트롤러를 업데이트할 때까지 아래 클래스를 만든 후에는 프로젝트를 컴파일할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-142">Note: You won't be able to compile the project after creating the classes below until you update the controllers that uses these classes.</span></span> 

<span data-ttu-id="21bb6-143">*모델* 폴더에서 *Person.cs* 을 만들고 템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-143">In the *Models* folder, create *Person.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="21bb6-144">*Instructor.cs*에서 `Person` 클래스의 `Instructor` 클래스를 파생 하 고 키 및 이름 필드를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-144">In *Instructor.cs*, derive the `Instructor` class from the `Person` class and remove the key and name fields.</span></span> <span data-ttu-id="21bb6-145">해당 코드는 다음 예제와 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-145">The code will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="21bb6-146">*Student.cs*에 대 한 비슷한 변경을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-146">Make similar changes to *Student.cs*.</span></span> <span data-ttu-id="21bb6-147">`Student` 클래스는 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-147">The `Student` class will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="adding-the-person-entity-type-to-the-model"></a><span data-ttu-id="21bb6-148">모델에 Person 엔터티 형식 추가</span><span class="sxs-lookup"><span data-stu-id="21bb6-148">Adding the Person Entity Type to the Model</span></span>

<span data-ttu-id="21bb6-149">*SchoolContext.cs*에서 `Person` 엔터티 형식에 대 한 `DbSet` 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-149">In *SchoolContext.cs*, add a `DbSet` property for the `Person` entity type:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="21bb6-150">계층당 하나의 테이블 상속을 구성하기 위해 Entity Framework에 필요한 모든 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-150">This is all that the Entity Framework needs in order to configure table-per-hierarchy inheritance.</span></span> <span data-ttu-id="21bb6-151">여기서 볼 수 있듯이 데이터베이스를 다시 만들 때 `Student` 및 `Instructor` 테이블 대신 `Person` 테이블이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-151">As you'll see, when the database is re-created, it will have a `Person` table in place of the `Student` and `Instructor` tables.</span></span>

## <a name="changing-instructorid-and-studentid-to-personid"></a><span data-ttu-id="21bb6-152">InstructorID 및 StudentID를 PersonID로 변경</span><span class="sxs-lookup"><span data-stu-id="21bb6-152">Changing InstructorID and StudentID to PersonID</span></span>

<span data-ttu-id="21bb6-153">*SchoolContext.cs*의 강사-강좌 매핑 문에서 `MapRightKey("InstructorID")`을 `MapRightKey("PersonID")`변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-153">In *SchoolContext.cs*, in the Instructor-Course mapping statement, change `MapRightKey("InstructorID")` to `MapRightKey("PersonID")`:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=4)]

<span data-ttu-id="21bb6-154">이러한 변경은 필요 하지 않습니다. 다대다 조인 테이블의 InstructorID 열 이름만 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-154">This change isn't required; it just changes the name of the InstructorID column in the many-to-many join table.</span></span> <span data-ttu-id="21bb6-155">이름을 InstructorID로 남겨 둔 경우에도 응용 프로그램이 제대로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-155">If you left the name as InstructorID, the application would still work correctly.</span></span> <span data-ttu-id="21bb6-156">다음은 완료 된 *SchoolContext.cs*입니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-156">Here is the completed *SchoolContext.cs*:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=15,24)]

<span data-ttu-id="21bb6-157">다음으로 `InstructorID`를 `PersonID`으로 변경 하 고 *마이그레이션* 폴더의 타임 스탬프 마이그레이션 파일을 ***제외*** 하 고 프로젝트 전체에서 `PersonID` `StudentID` 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-157">Next you need to change `InstructorID` to `PersonID` and `StudentID` to `PersonID` throughout the project ***except*** in the time-stamped migrations files in the *Migrations* folder.</span></span> <span data-ttu-id="21bb6-158">이렇게 하려면 변경 해야 하는 파일만 찾고 연 다음 열린 파일에 대 한 전체 변경을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-158">To do that you'll find and open only the files that need to be changed, then perform a global change on the opened files.</span></span> <span data-ttu-id="21bb6-159">변경 해야 하는 *마이그레이션* 폴더의 유일한 파일은 *Migrations\Configuration.cs.* 입니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-159">The only file in the *Migrations* folder you should change is *Migrations\Configuration.cs.*</span></span>

1. > [!IMPORTANT]
   > <span data-ttu-id="21bb6-160">먼저 Visual Studio에서 열려 있는 모든 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-160">Begin by closing all the open files in Visual Studio.</span></span>
2. <span data-ttu-id="21bb6-161">**편집** 메뉴에서 **찾기 및 바꾸기--모든 파일 찾기** 를 클릭 한 다음 프로젝트에서 `InstructorID`포함 된 모든 파일을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-161">Click **Find and Replace -- Find all Files** in the **Edit** menu, and then search for all files in the project that contain `InstructorID`.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. <span data-ttu-id="21bb6-162">각 파일에 대해 한 줄을 두 번 클릭 하 여 *마이그레이션 폴더에* &lt;타임 스탬프&gt; *\_.cs* 마이그레이션 파일을 ***제외 하*** 고 각 파일을 **찾기 결과** 창에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-162">Open each file in the **Find Results** window ***except*** the &lt;time-stamp&gt;*\_.cs* migration files in the *Migrations* folder, by double-clicking one line for each file.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)
4. <span data-ttu-id="21bb6-163">**파일에서 바꾸기** 대화 상자를 열고 열려 **있는** **모든 문서**를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-163">Open the **Replace in Files** dialog and change **Look in** to **All Open Documents**.</span></span>
5. <span data-ttu-id="21bb6-164">**파일에서 바꾸기** 대화 상자를 사용 하 여 모든 `InstructorID`을 `PersonID.` 변경</span><span class="sxs-lookup"><span data-stu-id="21bb6-164">Use the **Replace in Files** dialog to change all `InstructorID` to `PersonID.`</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)
6. <span data-ttu-id="21bb6-165">프로젝트에서 `StudentID`를 포함 하는 모든 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-165">Find all the files in the project that contain `StudentID`.</span></span>
7. <span data-ttu-id="21bb6-166">각 파일에 대해 한 줄을 두 번 클릭 하 여 &lt;타임 스탬프&gt;를 제외 하 고 *마이그레이션 폴더에* *\_\*.cs* 마이그레이션 파일을 ***제외 하*** 고 각 파일을 **찾기 결과** 창에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-166">Open each file in the **Find Results** window ***except*** the &lt;time-stamp&gt;*\_\*.cs* migration files in the *Migrations* folder, by double-clicking one line for each file.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
8. <span data-ttu-id="21bb6-167">**파일에서 바꾸기** 대화 상자를 열고 열려 **있는** **모든 문서**를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-167">Open the **Replace in Files** dialog and change **Look in** to **All Open Documents**.</span></span>
9. <span data-ttu-id="21bb6-168">**파일에서 바꾸기** 대화 상자를 사용 하 여 모든 `StudentID`을 `PersonID`변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-168">Use the **Replace in Files** dialog to change all `StudentID` to `PersonID`.</span></span>   
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)
10. <span data-ttu-id="21bb6-169">프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-169">Build the project.</span></span>

<span data-ttu-id="21bb6-170">이는 기본 키의 이름을 지정 하는 `classnameID` 패턴의 *단점* 을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-170">(Note that this demonstrates a *disadvantage* of the `classnameID` pattern for naming primary keys.</span></span> <span data-ttu-id="21bb6-171">클래스 이름 앞에 접두사를 지정 하지 않고 기본 키 ID의 이름을 지정한 경우에는 이름을 바꿀 필요가 *없습니다* .</span><span class="sxs-lookup"><span data-stu-id="21bb6-171">If you had named primary keys ID without prefixing the class name, *no* renaming would be necessary now.)</span></span>

## <a name="create-and-update-a-migrations-file"></a><span data-ttu-id="21bb6-172">마이그레이션 파일 만들기 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="21bb6-172">Create and Update a Migrations File</span></span>

<span data-ttu-id="21bb6-173">패키지 관리자 콘솔 (PMC)에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-173">In the Package Manager Console (PMC), enter the following command:</span></span>

`Add-Migration Inheritance`

<span data-ttu-id="21bb6-174">PMC에서 `Update-Database` 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-174">Run the `Update-Database` command in the PMC.</span></span> <span data-ttu-id="21bb6-175">마이그레이션에서 처리 방법을 알지 못하는 기존 데이터가 있으므로이 시점에서 명령이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-175">The command will fail at this point because we have existing data that migrations doesn't know how to handle.</span></span> <span data-ttu-id="21bb6-176">다음 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-176">You get the following error:</span></span>

<span data-ttu-id="21bb6-177">*ALTER TABLE 문이 FOREIGN KEY 제약 조건 "FK\_dbo와 충돌 했습니다. 부서\_dbo. Person\_PersonID ". 데이터베이스 "ContosoUniversity", 테이블 "dbo .에서 충돌이 발생 했습니다. Person ", ' PersonID ' 열*</span><span class="sxs-lookup"><span data-stu-id="21bb6-177">*The ALTER TABLE statement conflicted with the FOREIGN KEY constraint "FK\_dbo.Department\_dbo.Person\_PersonID". The conflict occurred in database "ContosoUniversity", table "dbo.Person", column 'PersonID'.*</span></span>

<span data-ttu-id="21bb6-178">*마이그레이션\&l t; 타임 스탬프&gt;\_Inheritance.cs* 을 열고 `Up` 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-178">Open *Migrations\&lt;timestamp&gt;\_Inheritance.cs* and replace the `Up` method with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=25,29-40)]

<span data-ttu-id="21bb6-179">`update-database` 명령을 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-179">Run the `update-database` command again.</span></span>

> [!NOTE]
> <span data-ttu-id="21bb6-180">데이터를 마이그레이션하고 스키마를 변경 하는 경우 다른 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-180">It's possible to get other errors when migrating data and making schema changes.</span></span> <span data-ttu-id="21bb6-181">해결할 수 없는 마이그레이션 오류가 발생 하면 *web.config 파일에서* 연결 문자열을 변경 하거나 데이터베이스를 삭제 하 여 자습서를 계속 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-181">If you get migration errors you can't resolve, you can continue with the tutorial by changing the connection string in the *Web.config* file or deleting the database.</span></span> <span data-ttu-id="21bb6-182">가장 간단한 방법은 web.config 파일에서 데이터베이스 이름을 바꾸는 것 *입니다.*</span><span class="sxs-lookup"><span data-stu-id="21bb6-182">The simplest approach is to rename the database in the *Web.config* file.</span></span> <span data-ttu-id="21bb6-183">예를 들어 다음 예제와 같이 데이터베이스 이름을 CU\_test로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-183">For example, change the database name to CU\_test as shown in the following example:</span></span>
> 
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.xml?highlight=1-2)]
> 
> <span data-ttu-id="21bb6-184">새 데이터베이스를 사용 하면 마이그레이션할 데이터가 없으며 `update-database` 명령이 오류 없이 완료 될 가능성이 훨씬 높습니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-184">With a new database, there is no data to migrate, and the `update-database` command is much more likely to complete without errors.</span></span> <span data-ttu-id="21bb6-185">데이터베이스를 삭제 하는 방법에 대 한 지침은 [Visual Studio 2012에서 데이터베이스](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)를 삭제 하는 방법을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="21bb6-185">For instructions on how to delete the database, see [How to Drop a Database from Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).</span></span> <span data-ttu-id="21bb6-186">자습서를 계속 진행 하기 위해이 방법을 사용 하는 경우, 배포 된 사이트는 마이그레이션을 자동으로 실행 하는 경우 동일한 오류가 발생 하므로이 자습서의 끝에 있는 배포 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-186">If you take this approach in order to continue with the tutorial, skip the deployment step at the end of this tutorial, since the deployed site would get the same error when it runs migrations automatically.</span></span> <span data-ttu-id="21bb6-187">마이그레이션 오류를 해결 하려면 가장 적합 한 리소스는 Entity Framework 포럼 또는 StackOverflow.com 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-187">If you want to troubleshoot a migrations error, the best resource is one of the Entity Framework forums or StackOverflow.com.</span></span>

## <a name="testing"></a><span data-ttu-id="21bb6-188">테스트</span><span class="sxs-lookup"><span data-stu-id="21bb6-188">Testing</span></span>

<span data-ttu-id="21bb6-189">사이트를 실행 하 고 다양 한 페이지를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-189">Run the site and try various pages.</span></span> <span data-ttu-id="21bb6-190">모든 항목이 이전과 같이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-190">Everything works the same as it did before.</span></span>

<span data-ttu-id="21bb6-191">**서버 탐색기** 에서 **schoolcontext.cs** 및 **Tables**를 확장 하 고 **Student** 및 **강사** 테이블이 **Person** 테이블로 대체 된 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-191">In **Server Explorer,** expand **SchoolContext** and then **Tables**, and you see that the **Student** and **Instructor** tables have been replaced by a **Person** table.</span></span> <span data-ttu-id="21bb6-192">**Person** 테이블을 확장 하면 **Student** 및 **강사** 테이블에 사용 되는 모든 열이 포함 되어 있는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-192">Expand the **Person** table and you see that it has all of the columns that used to be in the **Student** and **Instructor** tables.</span></span>

![Server_Explorer_showing_Person_table](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="21bb6-194">Person 테이블을 마우스 오른쪽 단추로 클릭한 후 **테이블 데이터 표시**를 클릭하여 판별자 열을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-194">Right-click the Person table, and then click **Show Table Data** to see the discriminator column.</span></span>

![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="21bb6-195">다음 다이어그램에서는 새 School 데이터베이스의 구조를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-195">The following diagram illustrates the structure of the new School database:</span></span>

![School_database_diagram](https://asp.net/media/2578143/Windows-Live-Writer_58f5a93579b2_CC7B_School_database_diagram_6350a801-7199-413f-bbac-4a2009ed19d7.png)

## <a name="summary"></a><span data-ttu-id="21bb6-197">요약</span><span class="sxs-lookup"><span data-stu-id="21bb6-197">Summary</span></span>

<span data-ttu-id="21bb6-198">이제 `Person`, `Student`및 `Instructor` 클래스에 대해 계층당 하나의 테이블 상속이 구현 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-198">Table-per-hierarchy inheritance has now been implemented for the `Person`, `Student`, and `Instructor` classes.</span></span> <span data-ttu-id="21bb6-199">이 및 다른 상속 구조에 대 한 자세한 내용은 계승 Teza의 Avi의 블로그에서 [상속 매핑 전략](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="21bb6-199">For more information about this and other inheritance structures, see [Inheritance Mapping Strategies](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx) on Morteza Manavi's blog.</span></span> <span data-ttu-id="21bb6-200">다음 자습서에서는 리포지토리 및 작업 단위 패턴을 구현 하는 몇 가지 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-200">In the next tutorial you'll see some ways to implement the repository and unit of work patterns.</span></span>

<span data-ttu-id="21bb6-201">[ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md)에서 다른 Entity Framework 리소스에 대 한 링크를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21bb6-201">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="21bb6-202">[이전](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [다음](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="21bb6-202">[Previous](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)</span></span>
