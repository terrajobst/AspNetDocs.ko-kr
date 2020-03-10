---
uid: mvc/overview/getting-started/database-first-development/enhancing-data-validation
title: '자습서: ASP.NET MVC 앱을 사용 하 여 EF Database First에 대 한 데이터 유효성 검사 강화'
description: 이 자습서에서는 데이터 모델에 데이터 주석을 추가 하 여 유효성 검사 요구 사항을 지정 하 고 서식을 표시 하는 방법을 집중적으로 설명 합니다.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: 0ed5e67a-34c0-4b57-84a6-802b0fb3cd00
msc.legacyurl: /mvc/overview/getting-started/database-first-development/enhancing-data-validation
msc.type: authoredcontent
ms.openlocfilehash: 897cd7c6a40445e2a4abede50d81e101372d3233
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499535"
---
# <a name="tutorial-enhance-data-validation-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="7a376-103">자습서: ASP.NET MVC 앱을 사용 하 여 EF Database First에 대 한 데이터 유효성 검사 강화</span><span class="sxs-lookup"><span data-stu-id="7a376-103">Tutorial: Enhance data validation for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="7a376-104">MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="7a376-105">이 자습서 시리즈에서는 사용자가 데이터베이스 테이블에 있는 데이터를 표시, 편집, 만들기 및 삭제할 수 있도록 하는 코드를 자동으로 생성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="7a376-106">생성 된 코드는 데이터베이스 테이블의 열에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="7a376-107">이 자습서에서는 데이터 모델에 데이터 주석을 추가 하 여 유효성 검사 요구 사항을 지정 하 고 서식을 표시 하는 방법을 집중적으로 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-107">This tutorial focuses on adding data annotations to the data model to specify validation requirements and display formatting.</span></span> <span data-ttu-id="7a376-108">의견 섹션에서 사용자의 의견에 따라 개선 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-108">It was improved based on feedback from users in the comments section.</span></span>

<span data-ttu-id="7a376-109">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-109">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7a376-110">데이터 주석 추가</span><span class="sxs-lookup"><span data-stu-id="7a376-110">Add data annotations</span></span>
> * <span data-ttu-id="7a376-111">메타 데이터 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="7a376-111">Add metadata classes</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a376-112">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="7a376-112">Prerequisites</span></span>

* [<span data-ttu-id="7a376-113">보기 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="7a376-113">Customize a view</span></span>](customizing-a-view.md)

## <a name="add-data-annotations"></a><span data-ttu-id="7a376-114">데이터 주석 추가</span><span class="sxs-lookup"><span data-stu-id="7a376-114">Add data annotations</span></span>

<span data-ttu-id="7a376-115">이전 항목에서 살펴본 것 처럼 일부 데이터 유효성 검사 규칙은 사용자 입력에 자동으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-115">As you saw in an earlier topic, some data validation rules are automatically applied to the user input.</span></span> <span data-ttu-id="7a376-116">예를 들어 Grade 속성에는 숫자만 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-116">For example, you can only provide a number for the Grade property.</span></span> <span data-ttu-id="7a376-117">더 많은 데이터 유효성 검사 규칙을 지정 하기 위해 모델 클래스에 데이터 주석을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-117">To specify more data validation rules, you can add data annotations to your model class.</span></span> <span data-ttu-id="7a376-118">이러한 주석은 지정 된 속성에 대 한 웹 응용 프로그램 전체에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-118">These annotations are applied throughout your web application for the specified property.</span></span> <span data-ttu-id="7a376-119">속성이 표시 되는 방식을 변경 하는 서식 특성을 적용할 수도 있습니다. 와 같이 텍스트 레이블에 사용 되는 값을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-119">You can also apply formatting attributes that change how the properties are displayed; such as, changing the value used for text labels.</span></span>

<span data-ttu-id="7a376-120">이 자습서에서는 FirstName, LastName 및 MiddleName 속성에 대해 제공 되는 값의 길이를 제한 하는 데이터 주석을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-120">In this tutorial, you will add data annotations to restrict the length of the values provided for the FirstName, LastName, and MiddleName properties.</span></span> <span data-ttu-id="7a376-121">데이터베이스에서 이러한 값은 50 자로 제한 됩니다. 그러나 웹 응용 프로그램에서는 현재 문자 제한이 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-121">In the database, these values are limited to 50 characters; however, in your web application that character limit is currently not enforced.</span></span> <span data-ttu-id="7a376-122">사용자가 이러한 값 중 하나에 대해 50 자를 초과 하 여 제공 하는 경우에는 해당 값을 데이터베이스에 저장 하려고 할 때 페이지의 작동이 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-122">If a user provides more than 50 characters for one of those values, the page will crash when attempting to save the value to the database.</span></span> <span data-ttu-id="7a376-123">또한 점수는 0과 4 사이의 값으로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-123">You will also restrict Grade to values between 0 and 4.</span></span>

<span data-ttu-id="7a376-124">**모델** > **ContosoModel** > **ContosoModel.tt** 를 선택 하 고 *Student.cs* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-124">Select **Models** > **ContosoModel.edmx** > **ContosoModel.tt** and open the *Student.cs* file.</span></span> <span data-ttu-id="7a376-125">클래스에 다음 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-125">Add the following highlighted code to the class.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample1.cs?highlight=5,15,17,20)]

<span data-ttu-id="7a376-126">*Enrollment.cs* 를 열고 다음 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-126">Open *Enrollment.cs* and add the following highlighted code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample2.cs?highlight=5,10)]

<span data-ttu-id="7a376-127">솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-127">Build the solution.</span></span>

<span data-ttu-id="7a376-128">**학생 목록** 을 클릭 하 고 **편집**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-128">Click **List of students** and select **Edit**.</span></span> <span data-ttu-id="7a376-129">50 자를 초과 하는 문자를 입력 하려고 하면 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-129">If you attempt to enter more than 50 characters, an error message is displayed.</span></span>

![오류 메시지 표시](enhancing-data-validation/_static/image1.png)

<span data-ttu-id="7a376-131">홈 페이지로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-131">Go back to the home page.</span></span> <span data-ttu-id="7a376-132">**등록 목록** 을 클릭 하 고 **편집**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-132">Click **List of enrollments** and select **Edit**.</span></span> <span data-ttu-id="7a376-133">4 보다 높은 등급을 제공 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-133">Attempt to provide a grade above 4.</span></span> <span data-ttu-id="7a376-134">이 오류가 표시 됩니다. *필드 등급은 0에서 4 사이* 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-134">You will receive this error: *The field Grade must be between 0 and 4.*</span></span>

## <a name="add-metadata-classes"></a><span data-ttu-id="7a376-135">메타 데이터 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="7a376-135">Add metadata classes</span></span>

<span data-ttu-id="7a376-136">모델 클래스에 직접 유효성 검사 특성을 추가 하는 것은 데이터베이스를 변경 하지 않을 때 작동 합니다. 그러나 데이터베이스를 변경 하 고 모델 클래스를 다시 생성 해야 하는 경우에는 모델 클래스에 적용 한 모든 특성을 잃게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-136">Adding the validation attributes directly to the model class works when you do not expect the database to change; however, if your database changes and you need to regenerate the model class, you will lose all of the attributes you had applied to the model class.</span></span> <span data-ttu-id="7a376-137">이 접근 방식은 매우 비효율적 이며 중요 한 유효성 검사 규칙을 손실 하는 경향이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-137">This approach can be very inefficient and prone to losing important validation rules.</span></span>

<span data-ttu-id="7a376-138">이 문제를 방지 하기 위해 특성을 포함 하는 메타 데이터 클래스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-138">To avoid this problem, you can add a metadata class that contains the attributes.</span></span> <span data-ttu-id="7a376-139">모델 클래스를 메타 데이터 클래스에 연결 하면 해당 특성이 모델에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-139">When you associate the model class to the metadata class, those attributes are applied to the model.</span></span> <span data-ttu-id="7a376-140">이 방법에서는 메타 데이터 클래스에 적용 된 모든 특성을 잃지 않고 모델 클래스를 다시 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-140">In this approach, the model class can be regenerated without losing all of the attributes that have been applied to the metadata class.</span></span>

<span data-ttu-id="7a376-141">**모델** 폴더에서 이름이 *Metadata.cs*인 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-141">In the **Models** folder, add a class named *Metadata.cs*.</span></span>

<span data-ttu-id="7a376-142">*Metadata.cs* 의 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-142">Replace the code in *Metadata.cs* with the following code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample3.cs)]

<span data-ttu-id="7a376-143">이러한 메타 데이터 클래스는 이전에 모델 클래스에 적용 한 모든 유효성 검사 특성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-143">These metadata classes contain all of the validation attributes that you had previously applied to the model classes.</span></span> <span data-ttu-id="7a376-144">**표시** 특성은 텍스트 레이블에 사용 되는 값을 변경 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-144">The **Display** attribute is used to change the value used for text labels.</span></span>

<span data-ttu-id="7a376-145">이제 모델 클래스를 메타 데이터 클래스와 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-145">Now, you must associate the model classes with the metadata classes.</span></span>

<span data-ttu-id="7a376-146">**모델** 폴더에서 이름이 *PartialClasses.cs*인 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-146">In the **Models** folder, add a class named *PartialClasses.cs*.</span></span>

<span data-ttu-id="7a376-147">파일 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-147">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample4.cs)]

<span data-ttu-id="7a376-148">각 클래스는 `partial` 클래스로 표시 되 고 각각은 이름과 네임 스페이스를 자동으로 생성 되는 클래스로 일치 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-148">Notice that each class is marked as a `partial` class, and each matches the name and namespace as the class that is automatically generated.</span></span> <span data-ttu-id="7a376-149">메타 데이터 특성을 partial 클래스에 적용 하 여 데이터 유효성 검사 특성이 자동으로 생성 된 클래스에 적용 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-149">By applying the metadata attribute to the partial class, you ensure that the data validation attributes will be applied to the automatically-generated class.</span></span> <span data-ttu-id="7a376-150">메타 데이터 특성은 다시 생성 되지 않는 부분 클래스에서 적용 되므로 모델 클래스를 다시 생성할 때 이러한 특성은 손실 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-150">These attributes will not be lost when you regenerate the model classes because the metadata attribute is applied in partial classes that are not regenerated.</span></span>

<span data-ttu-id="7a376-151">자동으로 생성 된 클래스를 다시 생성 하려면 *ContosoModel* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-151">To regenerate the automatically-generated classes, open the *ContosoModel.edmx* file.</span></span> <span data-ttu-id="7a376-152">다시 한 번 디자인 화면을 마우스 오른쪽 단추로 클릭 하 고 **데이터베이스에서 모델 업데이트**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-152">Once again, right-click on the design surface and select **Update Model from Database**.</span></span> <span data-ttu-id="7a376-153">데이터베이스를 변경 하지 않은 경우에도이 프로세스는 클래스를 다시 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-153">Even though you have not changed the database, this process will regenerate the classes.</span></span> <span data-ttu-id="7a376-154">**새로 고침** 탭에서 **테이블** 을 선택 하 고 **마침**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-154">In the **Refresh** tab, select **Tables** and **Finish**.</span></span>

<span data-ttu-id="7a376-155">*ContosoModel* 파일을 저장 하 여 변경 내용을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-155">Save the *ContosoModel.edmx* file to apply the changes.</span></span>

<span data-ttu-id="7a376-156">*Student.cs* 파일 또는 *Enrollment.cs* 파일을 열고 이전에 적용 한 데이터 유효성 검사 특성이 파일에 더 이상 표시 되지 않는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-156">Open the *Student.cs* file or the *Enrollment.cs* file, and notice that the data validation attributes you applied earlier are no longer in the file.</span></span> <span data-ttu-id="7a376-157">그러나 응용 프로그램을 실행 하 고 데이터를 입력할 때 유효성 검사 규칙이 계속 적용 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-157">However, run the application, and notice that the validation rules are still applied when you enter data.</span></span>

## <a name="conclusion"></a><span data-ttu-id="7a376-158">결론</span><span class="sxs-lookup"><span data-stu-id="7a376-158">Conclusion</span></span>

<span data-ttu-id="7a376-159">이 시리즈에서는 사용자가 데이터를 편집, 업데이트, 만들기 및 삭제할 수 있도록 하는 기존 데이터베이스에서 코드를 생성 하는 방법에 대 한 간단한 예를 제공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-159">This series provided a simple example of how to generate code from an existing database that enables users to edit, update, create and delete data.</span></span> <span data-ttu-id="7a376-160">ASP.NET MVC 5, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-160">It used ASP.NET MVC 5, Entity Framework and ASP.NET Scaffolding to create the project.</span></span> 

<span data-ttu-id="7a376-161">Code First 개발의 소개 예제는 [ASP.NET MVC 5 시작](../introduction/getting-started.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="7a376-161">For an introductory example of Code First development, see [Getting Started with ASP.NET MVC 5](../introduction/getting-started.md).</span></span> 

<span data-ttu-id="7a376-162">고급 예제를 보려면 [ASP.NET MVC 4 앱에 대 한 Entity Framework 데이터 모델 만들기](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="7a376-162">For a more advanced example, see [Creating an Entity Framework Data Model for an ASP.NET MVC 4 App](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="7a376-163">Database First의 데이터로 작업 하는 데 사용 하는 DbContext API는 Code First의 데이터로 작업 하는 데 사용 하는 API와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-163">Note that the DbContext API that you use for working with data in Database First is the same as the API you use for working with data in Code First.</span></span> <span data-ttu-id="7a376-164">Database First를 사용 하려는 경우에도 Code First 자습서에서 관련 데이터 읽기 및 업데이트, 동시성 충돌 처리 등과 같은 보다 복잡 한 시나리오를 처리 하는 방법을 배울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-164">Even if you intend to use Database First, you can learn how to handle more complex scenarios such as reading and updating related data, handling concurrency conflicts, and so forth from a Code First tutorial.</span></span> <span data-ttu-id="7a376-165">유일한 차이점은 데이터베이스, 컨텍스트 클래스 및 엔터티 클래스를 만드는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-165">The only difference is in how the database, context class, and entity classes are created.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7a376-166">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="7a376-166">Additional resources</span></span>

<span data-ttu-id="7a376-167">속성 및 클래스에 적용할 수 있는 데이터 유효성 검사 주석의 전체 목록은 [System.componentmodel 주석을](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="7a376-167">For a full list of data validation annotations you can apply to properties and classes, see [System.ComponentModel.DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a376-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7a376-168">Next steps</span></span>

<span data-ttu-id="7a376-169">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7a376-169">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7a376-170">추가 된 데이터 주석</span><span class="sxs-lookup"><span data-stu-id="7a376-170">Added data annotations</span></span>
> * <span data-ttu-id="7a376-171">메타 데이터 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="7a376-171">Added metadata classes</span></span>

<span data-ttu-id="7a376-172">Azure App Service에 웹 앱과 SQL 데이터베이스를 배포 하는 방법을 알아보려면 다음 자습서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="7a376-172">To learn how to deploy a web app and SQL database to Azure App Service, see this tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="7a376-173">Azure App Service에 .NET 앱 배포</span><span class="sxs-lookup"><span data-stu-id="7a376-173">Deploy a .NET app to Azure App Service</span></span>](/azure/app-service/app-service-web-tutorial-dotnet-sqldatabase/)
