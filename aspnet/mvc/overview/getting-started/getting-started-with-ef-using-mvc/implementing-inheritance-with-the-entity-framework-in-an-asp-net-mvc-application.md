---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: '자습서: ASP.NET MVC 5 앱에서 EF로 상속 구현'
description: 이 자습서에서는 데이터 모델에서 상속을 구현하는 방법을 보여 줍니다.
author: tdykstra
ms.author: riande
ms.date: 01/21/2019
ms.topic: tutorial
ms.assetid: 08834147-77ec-454a-bb7a-d931d2a40dab
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 73a01ed47b0935a1a9734c197377470defb1fe36
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471065"
---
# <a name="tutorial-implement-inheritance-with-ef-in-an-aspnet-mvc-5-app"></a><span data-ttu-id="1ec25-103">자습서: ASP.NET MVC 5 앱에서 EF로 상속 구현</span><span class="sxs-lookup"><span data-stu-id="1ec25-103">Tutorial: Implement Inheritance with EF in an ASP.NET MVC 5 app</span></span>

<span data-ttu-id="1ec25-104">이전 자습서에서는 동시성 예외를 처리 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-104">In the previous tutorial you handled concurrency exceptions.</span></span> <span data-ttu-id="1ec25-105">이 자습서에서는 데이터 모델에서 상속을 구현하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-105">This tutorial will show you how to implement inheritance in the data model.</span></span>

<span data-ttu-id="1ec25-106">개체 지향 프로그래밍에서는 [상속](http://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming)) 을 사용 하 여 코드를 쉽게 [재사용할](http://en.wikipedia.org/wiki/Code_reuse)수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-106">In object-oriented programming, you can use [inheritance](http://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming)) to facilitate [code reuse](http://en.wikipedia.org/wiki/Code_reuse).</span></span> <span data-ttu-id="1ec25-107">이 자습서에서는 강사와 학생 모두에게 공통적인 속성(예: `Instructor`)이 포함된 `Student` 기본 클래스에서 클래스가 파생되도록 `Person` 및 `LastName` 클래스를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-107">In this tutorial, you'll change the `Instructor` and `Student` classes so that they derive from a `Person` base class which contains properties such as `LastName` that are common to both instructors and students.</span></span> <span data-ttu-id="1ec25-108">웹 페이지를 추가하거나 변경하지는 않지만 일부 코드를 변경하고 이러한 변경 내용이 데이터베이스에 자동으로 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-108">You won't add or change any web pages, but you'll change some of the code and those changes will be automatically reflected in the database.</span></span>

<span data-ttu-id="1ec25-109">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-109">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1ec25-110">데이터베이스에 상속 매핑 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="1ec25-110">Learn to map inheritance to database</span></span>
> * <span data-ttu-id="1ec25-111">Person 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="1ec25-111">Create the Person class</span></span>
> * <span data-ttu-id="1ec25-112">강사 및 학생 업데이트</span><span class="sxs-lookup"><span data-stu-id="1ec25-112">Update Instructor and Student</span></span>
> * <span data-ttu-id="1ec25-113">모델에 사람 추가</span><span class="sxs-lookup"><span data-stu-id="1ec25-113">Add Person to the Model</span></span>
> * <span data-ttu-id="1ec25-114">마이그레이션 만들기 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="1ec25-114">Create and Update Migrations</span></span>
> * <span data-ttu-id="1ec25-115">구현 테스트</span><span class="sxs-lookup"><span data-stu-id="1ec25-115">Test the implementation</span></span>
> * <span data-ttu-id="1ec25-116">Deploy to Azure</span><span class="sxs-lookup"><span data-stu-id="1ec25-116">Deploy to Azure</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ec25-117">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="1ec25-117">Prerequisites</span></span>

* [<span data-ttu-id="1ec25-118">동시성 처리</span><span class="sxs-lookup"><span data-stu-id="1ec25-118">Handling Concurrency</span></span>](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="map-inheritance-to-database"></a><span data-ttu-id="1ec25-119">데이터베이스에 상속 매핑</span><span class="sxs-lookup"><span data-stu-id="1ec25-119">Map inheritance to database</span></span>

<span data-ttu-id="1ec25-120">`School` 데이터 모델의 `Instructor` 및 `Student` 클래스에는 동일한 여러 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-120">The `Instructor` and `Student` classes in the `School` data model have several properties that are identical:</span></span>

![Student_and_Instructor_classes](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

<span data-ttu-id="1ec25-122">`Instructor` 및 `Student` 엔터티에서 공유하는 속성에 대해 중복 코드를 제거하려고 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-122">Suppose you want to eliminate the redundant code for the properties that are shared by the `Instructor` and `Student` entities.</span></span> <span data-ttu-id="1ec25-123">또는 강사 또는 학생의 이름인지 여부를 신경쓰지 않고 이름의 형식을 지정할 수 있는 서비스를 작성하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-123">Or you want to write a service that can format names without caring whether the name came from an instructor or a student.</span></span> <span data-ttu-id="1ec25-124">다음 그림과 같이 해당 공유 속성만 포함 하는 `Person` 기본 클래스를 만든 다음 `Instructor` 및 `Student` 엔터티가 해당 기본 클래스에서 상속 하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-124">You could create a `Person` base class which contains only those shared properties, then make the `Instructor` and `Student` entities inherit from that base class, as shown in the following illustration:</span></span>

![Student_and_Instructor_classes_deriving_from_Person_class](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

<span data-ttu-id="1ec25-126">데이터베이스에 이 상속 구조를 여러 가지 방법으로 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-126">There are several ways this inheritance structure could be represented in the database.</span></span> <span data-ttu-id="1ec25-127">학생 및 강사 모두에 대 한 정보를 단일 테이블에 포함 하는 `Person` 테이블이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-127">You could have a `Person` table that includes information about both students and instructors in a single table.</span></span> <span data-ttu-id="1ec25-128">일부 열은 강사 (`HireDate`) 에게만 적용 되 고 일부는 학생 (`EnrollmentDate`)에만 적용 되 고 일부는 둘 다 (`LastName`, `FirstName`)에만 적용 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-128">Some of the columns could apply only to instructors (`HireDate`), some only to students (`EnrollmentDate`), some to both (`LastName`, `FirstName`).</span></span> <span data-ttu-id="1ec25-129">일반적으로 각 행이 나타내는 형식을 나타내는 *판별자* 열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-129">Typically, you'd have a *discriminator* column to indicate which type each row represents.</span></span> <span data-ttu-id="1ec25-130">예를 들어, 판별자 열은 강사에 대해 "Instructor"를, 학생에 대해 "Student"를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-130">For example, the discriminator column might have "Instructor" for instructors and "Student" for students.</span></span>

![테이블당 테이블 수 hierarchy_example](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

<span data-ttu-id="1ec25-132">단일 데이터베이스 테이블에서 엔터티 상속 구조를 생성 하는이 패턴은 TPH ( *계층당 하나의 테이블* ) 상속 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-132">This pattern of generating an entity inheritance structure from a single database table is called *table-per-hierarchy* (TPH) inheritance.</span></span>

<span data-ttu-id="1ec25-133">다른 방법은 데이터베이스를 상속 구조와 유사하게 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-133">An alternative is to make the database look more like the inheritance structure.</span></span> <span data-ttu-id="1ec25-134">예를 들어 `Person` 테이블에 이름 필드만 포함 하 고 날짜 필드를 사용 하 여 별도의 `Instructor` 및 `Student` 테이블을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-134">For example, you could have only the name fields in the `Person` table and have separate `Instructor` and `Student` tables with the date fields.</span></span>

![Table-per-type_inheritance](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="1ec25-136">각 엔터티 클래스에 대 한 데이터베이스 테이블을 만드는이 패턴을 TPT (형식당 *하나의 테이블* ) 상속 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-136">This pattern of making a database table for each entity class is called *table per type* (TPT) inheritance.</span></span>

<span data-ttu-id="1ec25-137">또 다른 옵션은 모든 비추상 형식을 개별 테이블에 매핑하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-137">Yet another option is to map all non-abstract types to individual tables.</span></span> <span data-ttu-id="1ec25-138">상속된 속성을 포함한 모든 클래스 속성을 해당 테이블의 열에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-138">All properties of a class, including inherited properties, map to columns of the corresponding table.</span></span> <span data-ttu-id="1ec25-139">이 패턴을 TPC(구체적 클래스당 하나의 테이블) 상속이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-139">This pattern is called Table-per-Concrete Class (TPC) inheritance.</span></span> <span data-ttu-id="1ec25-140">앞에서 설명한 것 처럼 `Person`, `Student`및 `Instructor` 클래스에 대해 TPC 상속을 구현 하는 경우 `Student` 및 `Instructor` 테이블은 이전에 수행한 것 보다 상속을 구현한 후에는 다르게 보입니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-140">If you implemented TPC inheritance for the `Person`, `Student`, and `Instructor` classes as shown earlier, the `Student` and `Instructor` tables would look no different after implementing inheritance than they did before.</span></span>

<span data-ttu-id="1ec25-141">일반적으로 TPT 패턴은 복잡 한 조인 쿼리를 발생 시킬 수 있기 때문에 TPC 및 TPH 상속 패턴 Entity Framework은 TPT 상속 패턴 보다 더 나은 성능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-141">TPC and TPH inheritance patterns generally deliver better performance in the Entity Framework than TPT inheritance patterns, because TPT patterns can result in complex join queries.</span></span>

<span data-ttu-id="1ec25-142">이 자습서에서는 TPH 상속을 구현하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-142">This tutorial demonstrates how to implement TPH inheritance.</span></span> <span data-ttu-id="1ec25-143">TPH는 Entity Framework의 기본 상속 패턴 이므로 `Person` 클래스를 만들고, `Instructor` 및 `Student` 클래스를 `Person`에서 파생 되도록 변경 하 고, 새 클래스를 `DbContext`에 추가 하 고, 마이그레이션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-143">TPH is the default inheritance pattern in the Entity Framework, so all you have to do is create a `Person` class, change the `Instructor` and `Student` classes to derive from `Person`, add the new class to the `DbContext`, and create a migration.</span></span> <span data-ttu-id="1ec25-144">다른 상속 패턴을 구현 하는 방법에 대 한 자세한 내용은 MSDN Entity Framework 설명서에서 형식당 [하나의 테이블 상속 매핑](https://msdn.microsoft.com/data/jj591617#2.5) 및 TPC ( [비추상 클래스) 상속 매핑](https://msdn.microsoft.com/data/jj591617#2.6) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="1ec25-144">(For information about how to implement the other inheritance patterns, see [Mapping the Table-Per-Type (TPT) Inheritance](https://msdn.microsoft.com/data/jj591617#2.5) and [Mapping the Table-Per-Concrete Class (TPC) Inheritance](https://msdn.microsoft.com/data/jj591617#2.6) in the MSDN Entity Framework documentation.)</span></span>

## <a name="create-the-person-class"></a><span data-ttu-id="1ec25-145">Person 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="1ec25-145">Create the Person class</span></span>

<span data-ttu-id="1ec25-146">*모델* 폴더에서 *Person.cs* 을 만들고 템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-146">In the *Models* folder, create *Person.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

## <a name="update-instructor-and-student"></a><span data-ttu-id="1ec25-147">강사 및 학생 업데이트</span><span class="sxs-lookup"><span data-stu-id="1ec25-147">Update Instructor and Student</span></span>

<span data-ttu-id="1ec25-148">이제 *Instructor.cs* 및 *Student.cs* 를 업데이트 하 여 *Person.sc*에서 값을 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-148">Now update the *Instructor.cs* and *Student.cs* to inherit values from the *Person.sc*.</span></span>

<span data-ttu-id="1ec25-149">*Instructor.cs*에서 `Person` 클래스의 `Instructor` 클래스를 파생 하 고 키 및 이름 필드를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-149">In *Instructor.cs*, derive the `Instructor` class from the `Person` class and remove the key and name fields.</span></span> <span data-ttu-id="1ec25-150">해당 코드는 다음 예제와 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-150">The code will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="1ec25-151">*Student.cs*에 대 한 비슷한 변경을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-151">Make similar changes to *Student.cs*.</span></span> <span data-ttu-id="1ec25-152">`Student` 클래스는 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-152">The `Student` class will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="add-person-to-the-model"></a><span data-ttu-id="1ec25-153">모델에 사람 추가</span><span class="sxs-lookup"><span data-stu-id="1ec25-153">Add Person to the Model</span></span>

<span data-ttu-id="1ec25-154">*SchoolContext.cs*에서 `Person` 엔터티 형식에 대 한 `DbSet` 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-154">In *SchoolContext.cs*, add a `DbSet` property for the `Person` entity type:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="1ec25-155">계층당 하나의 테이블 상속을 구성하기 위해 Entity Framework에 필요한 모든 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-155">This is all that the Entity Framework needs in order to configure table-per-hierarchy inheritance.</span></span> <span data-ttu-id="1ec25-156">여기서 볼 수 있듯이 데이터베이스를 업데이트 하면 `Student` 및 `Instructor` 테이블 대신 `Person` 테이블이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-156">As you'll see, when the database is updated, it will have a `Person` table in place of the `Student` and `Instructor` tables.</span></span>

## <a name="create-and-update-migrations"></a><span data-ttu-id="1ec25-157">마이그레이션 만들기 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="1ec25-157">Create and Update Migrations</span></span>

<span data-ttu-id="1ec25-158">패키지 관리자 콘솔 (PMC)에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-158">In the Package Manager Console (PMC), enter the following command:</span></span>

`Add-Migration Inheritance`

<span data-ttu-id="1ec25-159">PMC에서 `Update-Database` 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-159">Run the `Update-Database` command in the PMC.</span></span> <span data-ttu-id="1ec25-160">마이그레이션에서 처리 방법을 알지 못하는 기존 데이터가 있으므로이 시점에서 명령이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-160">The command will fail at this point because we have existing data that migrations doesn't know how to handle.</span></span> <span data-ttu-id="1ec25-161">다음과 같은 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-161">You get an error message like the following one:</span></span>

> <span data-ttu-id="1ec25-162">*개체 ' dbo '를 삭제할 수 없습니다. 강사 '는 FOREIGN KEY 제약 조건에 의해 참조 되므로*</span><span class="sxs-lookup"><span data-stu-id="1ec25-162">*Could not drop object 'dbo.Instructor' because it is referenced by a FOREIGN KEY constraint.*</span></span>

<span data-ttu-id="1ec25-163">*마이그레이션\&l t; 타임 스탬프&gt;\_Inheritance.cs* 을 열고 `Up` 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-163">Open *Migrations\&lt;timestamp&gt;\_Inheritance.cs* and replace the `Up` method with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

<span data-ttu-id="1ec25-164">이 코드는 다음과 같은 데이터베이스 업데이트 작업을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-164">This code takes care of the following database update tasks:</span></span>

- <span data-ttu-id="1ec25-165">Student 테이블을 가리키는 외래 키 제약 조건 및 인덱스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-165">Removes foreign key constraints and indexes that point to the Student table.</span></span>
- <span data-ttu-id="1ec25-166">Instructor 테이블 이름을 Person으로 바꾸고 Student 데이터를 저장하기 위해 필요한 변경을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-166">Renames the Instructor table as Person and makes changes needed for it to store Student data:</span></span>

    - <span data-ttu-id="1ec25-167">학생에 대한 Nullable EnrollmentDate를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-167">Adds nullable EnrollmentDate for students.</span></span>
    - <span data-ttu-id="1ec25-168">행이 학생용인지, 강사용인지 나타내는 판별자 열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-168">Adds Discriminator column to indicate whether a row is for a student or an instructor.</span></span>
    - <span data-ttu-id="1ec25-169">학생 행은 고용 날짜를 포함하지 않으므로 HireDate를 Nullable로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-169">Makes HireDate nullable since student rows won't have hire dates.</span></span>
    - <span data-ttu-id="1ec25-170">학생을 가리키는 외래 키를 업데이트하는 데 사용할 임시 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-170">Adds a temporary field that will be used to update foreign keys that point to students.</span></span> <span data-ttu-id="1ec25-171">Person 테이블에 학생을 복사 하면 새 기본 키 값이 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-171">When you copy students into the Person table they'll get new primary key values.</span></span>
- <span data-ttu-id="1ec25-172">Student 테이블에서 Person 테이블로 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-172">Copies data from the Student table into the Person table.</span></span> <span data-ttu-id="1ec25-173">그러면 학생에게 새 기본 키 값이 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-173">This causes students to get assigned new primary key values.</span></span>
- <span data-ttu-id="1ec25-174">학생을 가리키는 외래 키 값을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-174">Fixes foreign key values that point to students.</span></span>
- <span data-ttu-id="1ec25-175">이제 Person 테이블을 가리키도록 외래 키 제약 조건 및 인덱스를 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-175">Re-creates foreign key constraints and indexes, now pointing them to the Person table.</span></span>

<span data-ttu-id="1ec25-176">(기본 키 형식으로 정수 대신 GUID를 사용한 경우, 학생 기본 키 값을 변경할 필요가 없으며 이 단계 중 일부가 생략되었을 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="1ec25-176">(If you had used GUID instead of integer as the primary key type, the student primary key values wouldn't have to change, and several of these steps could have been omitted.)</span></span>

<span data-ttu-id="1ec25-177">`update-database` 명령을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-177">Run the `update-database` command again.</span></span>

<span data-ttu-id="1ec25-178">프로덕션 시스템에서는 이전 데이터베이스 버전으로 다시 이동 하는 데 사용 해야 하는 경우에는 Down 메서드를 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-178">(In a production system you would make corresponding changes to the Down method in case you ever had to use that to go back to the previous database version.</span></span> <span data-ttu-id="1ec25-179">이 자습서에서는 Down 메서드를 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-179">For this tutorial you won't be using the Down method.)</span></span>

> [!NOTE]
> <span data-ttu-id="1ec25-180">데이터를 마이그레이션하고 스키마를 변경 하는 경우 다른 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-180">It's possible to get other errors when migrating data and making schema changes.</span></span> <span data-ttu-id="1ec25-181">해결할 수 없는 마이그레이션 오류가 발생 하면 *web.config 파일에서* 연결 문자열을 변경 하거나 데이터베이스를 삭제 하 여 자습서를 계속 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-181">If you get migration errors you can't resolve, you can continue with the tutorial by changing the connection string in the *Web.config* file or by deleting the database.</span></span> <span data-ttu-id="1ec25-182">가장 간단한 방법은 web.config 파일에서 데이터베이스 이름을 바꾸는 것 *입니다.*</span><span class="sxs-lookup"><span data-stu-id="1ec25-182">The simplest approach is to rename the database in the *Web.config* file.</span></span> <span data-ttu-id="1ec25-183">예를 들어 다음 예제와 같이 데이터베이스 이름을 ContosoUniversity2로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-183">For example, change the database name to ContosoUniversity2 as shown in the following example:</span></span>
>
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.xml?highlight=2)]
>
> <span data-ttu-id="1ec25-184">새 데이터베이스를 사용 하면 마이그레이션할 데이터가 없으며 `update-database` 명령이 오류 없이 완료 될 가능성이 훨씬 높습니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-184">With a new database, there is no data to migrate, and the `update-database` command is much more likely to complete without errors.</span></span> <span data-ttu-id="1ec25-185">데이터베이스를 삭제 하는 방법에 대 한 지침은 [Visual Studio 2012에서 데이터베이스](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)를 삭제 하는 방법을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="1ec25-185">For instructions on how to delete the database, see [How to Drop a Database from Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).</span></span> <span data-ttu-id="1ec25-186">자습서를 계속 진행 하기 위해이 방법을 사용 하는 경우이 자습서의 끝에 있는 배포 단계를 건너뛰거나 새 사이트 및 데이터베이스에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-186">If you take this approach in order to continue with the tutorial, skip the deployment step at the end of this tutorial or deploy to a new site and database.</span></span> <span data-ttu-id="1ec25-187">이미 배포 하는 동일한 사이트에 업데이트를 배포 하는 경우, 자동으로 마이그레이션을 실행 하면 EF가 동일한 오류를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-187">If you deploy an update to the same site you've been deploying to already, EF will get the same error there when it runs migrations automatically.</span></span> <span data-ttu-id="1ec25-188">마이그레이션 오류를 해결 하려면 가장 적합 한 리소스는 Entity Framework 포럼 또는 StackOverflow.com 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-188">If you want to troubleshoot a migrations error, the best resource is one of the Entity Framework forums or StackOverflow.com.</span></span>

## <a name="test-the-implementation"></a><span data-ttu-id="1ec25-189">구현 테스트</span><span class="sxs-lookup"><span data-stu-id="1ec25-189">Test the implementation</span></span>

<span data-ttu-id="1ec25-190">사이트를 실행 하 고 다양 한 페이지를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-190">Run the site and try various pages.</span></span> <span data-ttu-id="1ec25-191">모든 항목이 이전과 같이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-191">Everything works the same as it did before.</span></span>

<span data-ttu-id="1ec25-192">**서버 탐색기** 에서 **Data Connections\SchoolContext** 및 **Tables**를 확장 하면 **Student** 및 **강사** 테이블이 **Person** 테이블로 대체 된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-192">In **Server Explorer,** expand **Data Connections\SchoolContext** and then **Tables**, and you see that the **Student** and **Instructor** tables have been replaced by a **Person** table.</span></span> <span data-ttu-id="1ec25-193">**Person** 테이블을 확장 하면 **Student** 및 **강사** 테이블에 사용 되는 모든 열이 포함 되어 있는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-193">Expand the **Person** table and you see that it has all of the columns that used to be in the **Student** and **Instructor** tables.</span></span>

<span data-ttu-id="1ec25-194">Person 테이블을 마우스 오른쪽 단추로 클릭한 후 **테이블 데이터 표시**를 클릭하여 판별자 열을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-194">Right-click the Person table, and then click **Show Table Data** to see the discriminator column.</span></span>

<span data-ttu-id="1ec25-195">다음 다이어그램에서는 새 School 데이터베이스의 구조를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-195">The following diagram illustrates the structure of the new School database:</span></span>

![School_database_diagram](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

## <a name="deploy-to-azure"></a><span data-ttu-id="1ec25-197">Deploy to Azure</span><span class="sxs-lookup"><span data-stu-id="1ec25-197">Deploy to Azure</span></span>

<span data-ttu-id="1ec25-198">이 섹션에서는이 자습서 시리즈의 [3 부, 정렬, 필터링 및 페이징](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md) 에서 선택적으로 **Azure에 앱 배포** 섹션을 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-198">This section requires you to have completed the optional **Deploying the app to Azure** section in [Part 3, Sorting, Filtering, and Paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md) of this tutorial series.</span></span> <span data-ttu-id="1ec25-199">로컬 프로젝트에서 데이터베이스를 삭제 하 여 마이그레이션 오류가 해결 된 경우에는이 단계를 건너뜁니다. 또는 새 사이트 및 데이터베이스를 만들고 새 환경에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-199">If you had migrations errors that you resolved by deleting the database in your local project, skip this step; or create a new site and database, and deploy to the new environment.</span></span>

1. <span data-ttu-id="1ec25-200">Visual Studio의 **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-200">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>

2. <span data-ttu-id="1ec25-201">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-201">Click **Publish**.</span></span>

    <span data-ttu-id="1ec25-202">웹 앱이 기본 브라우저에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-202">The Web app opens in your default browser.</span></span>

3. <span data-ttu-id="1ec25-203">응용 프로그램을 테스트 하 여 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-203">Test the application to verify it's working.</span></span>

    <span data-ttu-id="1ec25-204">데이터베이스에 액세스 하는 페이지를 처음 실행 하는 경우 Entity Framework는 현재 데이터 모델을 사용 하 여 데이터베이스를 최신 상태로 만드는 데 필요한 모든 마이그레이션 `Up` 메서드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-204">The first time you run a page that accesses the database, the Entity Framework runs all of the migrations `Up` methods required to bring the database up to date with the current data model.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="1ec25-205">코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="1ec25-205">Get the code</span></span>

[<span data-ttu-id="1ec25-206">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="1ec25-206">Download Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="1ec25-207">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1ec25-207">Additional resources</span></span>

<span data-ttu-id="1ec25-208">[ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)에서 다른 Entity Framework 리소스에 대 한 링크를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-208">Links to other Entity Framework resources can be found in the [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

<span data-ttu-id="1ec25-209">이 및 다른 상속 구조에 대 한 자세한 내용은 MSDN의 [TPT 상속 패턴](https://msdn.microsoft.com/data/jj618293) 및 [TPH 상속 패턴](https://msdn.microsoft.com/data/jj618292) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="1ec25-209">For more information about this and other inheritance structures, see [TPT Inheritance Pattern](https://msdn.microsoft.com/data/jj618293) and [TPH Inheritance Pattern](https://msdn.microsoft.com/data/jj618292) on MSDN.</span></span> <span data-ttu-id="1ec25-210">다음 자습서에서는 다양한 고급 Entity Framework 시나리오를 처리하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-210">In the next tutorial you'll see how to handle a variety of relatively advanced Entity Framework scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ec25-211">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1ec25-211">Next steps</span></span>

<span data-ttu-id="1ec25-212">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-212">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1ec25-213">상속을 데이터베이스로 매핑하기 위해 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-213">Learned to map inheritance to database</span></span>
> * <span data-ttu-id="1ec25-214">Person 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="1ec25-214">Created the Person class</span></span>
> * <span data-ttu-id="1ec25-215">강사 및 학생 업데이트</span><span class="sxs-lookup"><span data-stu-id="1ec25-215">Updated Instructor and Student</span></span>
> * <span data-ttu-id="1ec25-216">모델에 개인 추가</span><span class="sxs-lookup"><span data-stu-id="1ec25-216">Added Person to the Model</span></span>
> * <span data-ttu-id="1ec25-217">마이그레이션 생성 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="1ec25-217">Created and Update Migrations</span></span>
> * <span data-ttu-id="1ec25-218">구현 테스트</span><span class="sxs-lookup"><span data-stu-id="1ec25-218">Tested the implementation</span></span>
> * <span data-ttu-id="1ec25-219">Azure에 배포</span><span class="sxs-lookup"><span data-stu-id="1ec25-219">Deployed to Azure</span></span>

<span data-ttu-id="1ec25-220">Entity Framework Code First를 사용 하는 ASP.NET 웹 응용 프로그램을 개발 하는 기본 사항을 벗어날 때 알아두어야 하는 유용한 항목에 대해 알아보려면 다음 문서로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ec25-220">Advance to the next article to learn about topics that are useful to be aware of when you go beyond the basics of developing ASP.NET web applications that use Entity Framework Code First.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="1ec25-221">고급 Entity Framework 시나리오</span><span class="sxs-lookup"><span data-stu-id="1ec25-221">Advanced Entity Framework Scenarios</span></span>](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
