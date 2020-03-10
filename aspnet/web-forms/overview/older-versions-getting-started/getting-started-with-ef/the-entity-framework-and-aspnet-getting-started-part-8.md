---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
title: Entity Framework 4.0 Database First 및 ASP.NET 4 Web Forms 시작-8 부 | Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 응용 프로그램 샘플은 ...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: aaadd9bb-5508-448c-ad57-5497dff90e13
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
msc.type: authoredcontent
ms.openlocfilehash: ff6a808dd501df8056c0fb0784a8e42e094d5db7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78473507"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-8"></a><span data-ttu-id="9627b-104">Entity Framework 4.0 Database First 및 ASP.NET 4 Web Forms 시작-8 부</span><span class="sxs-lookup"><span data-stu-id="9627b-104">Getting Started with Entity Framework 4.0 Database First and ASP.NET 4 Web Forms - Part 8</span></span>

<span data-ttu-id="9627b-105">만든 사람 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="9627b-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="9627b-106">Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 4.0 및 Visual Studio 2010를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-106">The Contoso University sample web application demonstrates how to create ASP.NET Web Forms applications using the Entity Framework 4.0 and Visual Studio 2010.</span></span> <span data-ttu-id="9627b-107">자습서 시리즈에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](the-entity-framework-and-aspnet-getting-started-part-1.md) 를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="9627b-107">For information about the tutorial series, see [the first tutorial in the series](the-entity-framework-and-aspnet-getting-started-part-1.md)</span></span>

## <a name="using-dynamic-data-functionality-to-format-and-validate-data"></a><span data-ttu-id="9627b-108">Dynamic Data 기능을 사용 하 여 데이터 서식 지정 및 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="9627b-108">Using Dynamic Data Functionality to Format and Validate Data</span></span>

<span data-ttu-id="9627b-109">이전 자습서에서 저장 프로시저를 구현 했습니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-109">In the previous tutorial you implemented stored procedures.</span></span> <span data-ttu-id="9627b-110">이 자습서에서는 Dynamic Data 기능을 통해 다음과 같은 이점을 제공 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-110">This tutorial will show you how Dynamic Data functionality can provide the following benefits:</span></span>

- <span data-ttu-id="9627b-111">필드는 데이터 형식에 따라 자동으로 표시 되도록 서식이 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-111">Fields are automatically formatted for display based on their data type.</span></span>
- <span data-ttu-id="9627b-112">필드는 데이터 형식에 따라 자동으로 유효성이 검사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-112">Fields are automatically validated based on their data type.</span></span>
- <span data-ttu-id="9627b-113">데이터 모델에 메타 데이터를 추가 하 여 서식 지정 및 유효성 검사 동작을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-113">You can add metadata to the data model to customize formatting and validation behavior.</span></span> <span data-ttu-id="9627b-114">이 작업을 수행 하는 경우 한 곳에 서식 및 유효성 검사 규칙을 추가할 수 있으며, Dynamic Data 컨트롤을 사용 하 여 필드에 액세스 하는 모든 곳에서 자동으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-114">When you do this, you can add the formatting and validation rules in just one place, and they're automatically applied everywhere you access the fields using Dynamic Data controls.</span></span>

<span data-ttu-id="9627b-115">이 기능이 어떻게 작동 하는지 확인 하려면 기존 *학생* 페이지의 필드를 표시 하 고 편집 하는 데 사용 하는 컨트롤을 변경 하 고 `Student` 엔터티 형식의 이름 및 날짜 필드에 서식 및 유효성 검사 메타 데이터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-115">To see how this works, you'll change the controls you use to display and edit fields in the existing *Students.aspx* page, and you'll add formatting and validation metadata to the name and date fields of the `Student` entity type.</span></span>

<span data-ttu-id="9627b-116">[![Image01](the-entity-framework-and-aspnet-getting-started-part-8/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="9627b-116">[![Image01](the-entity-framework-and-aspnet-getting-started-part-8/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image1.png)</span></span>

## <a name="using-dynamicfield-and-dynamiccontrol-controls"></a><span data-ttu-id="9627b-117">DynamicField 및 DynamicControl 컨트롤 사용</span><span class="sxs-lookup"><span data-stu-id="9627b-117">Using DynamicField and DynamicControl Controls</span></span>

<span data-ttu-id="9627b-118">*학생용 .aspx* 페이지를 열고 `StudentsGridView` 컨트롤에서 **이름** 및 **등록 날짜** `TemplateField` 요소를 다음 태그로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-118">Open the *Students.aspx* page and in the `StudentsGridView` control replace the **Name** and **Enrollment Date** `TemplateField` elements with the following markup:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample1.aspx)]

<span data-ttu-id="9627b-119">이 태그는 학생 이름 템플릿 필드에서 `TextBox` 및 `Label` 컨트롤 대신 `DynamicControl` 컨트롤을 사용 하 고 등록 날짜에 `DynamicField` 컨트롤을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-119">This markup uses `DynamicControl` controls in place of `TextBox` and `Label` controls in the student name template field, and it uses a `DynamicField` control for the enrollment date.</span></span> <span data-ttu-id="9627b-120">서식 문자열을 지정 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-120">No format strings are specified.</span></span>

<span data-ttu-id="9627b-121">`StudentsGridView` 컨트롤 뒤에 `ValidationSummary` 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-121">Add a `ValidationSummary` control after the `StudentsGridView` control.</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample2.aspx)]

<span data-ttu-id="9627b-122">`SearchGridView` 컨트롤에서 `EditItemTemplate` 요소를 생략 하는 것을 제외 하 고 `StudentsGridView` 컨트롤과 같이 **이름** 및 **등록 날짜** 열의 태그를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-122">In the `SearchGridView` control replace the markup for the **Name** and **Enrollment Date** columns as you did in the `StudentsGridView` control, except omit the `EditItemTemplate` element.</span></span> <span data-ttu-id="9627b-123">이제 `SearchGridView` 컨트롤의 `Columns` 요소에 다음 태그가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-123">The `Columns` element of the `SearchGridView` control now contains the following markup:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample3.aspx)]

<span data-ttu-id="9627b-124">*Students.aspx.cs* 를 열고 다음 `using` 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-124">Open *Students.aspx.cs* and add the following `using` statement:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample4.cs)]

<span data-ttu-id="9627b-125">페이지의 `Init` 이벤트에 대 한 처리기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-125">Add a handler for the page's `Init` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample5.cs)]

<span data-ttu-id="9627b-126">이 코드는 Dynamic Data에서 `Student` 엔터티의 필드에 대해 이러한 데이터 바인딩된 컨트롤에 서식 지정 및 유효성 검사를 제공 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-126">This code specifies that Dynamic Data will provide formatting and validation in these data-bound controls for fields of the `Student` entity.</span></span> <span data-ttu-id="9627b-127">페이지를 실행할 때 다음 예제와 같은 오류 메시지가 표시 되 면 일반적으로 `Page_Init`에서 `EnableDynamicData` 메서드를 호출 하는 것을 잊은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-127">If you get an error message like the following example when you run the page, it typically means you've forgotten to call the `EnableDynamicData` method in `Page_Init`:</span></span>

`Could not determine a MetaTable. A MetaTable could not be determined for the data source 'StudentsEntityDataSource' and one could not be inferred from the request URL.`

<span data-ttu-id="9627b-128">페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-128">Run the page.</span></span>

<span data-ttu-id="9627b-129">[![Image03](the-entity-framework-and-aspnet-getting-started-part-8/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="9627b-129">[![Image03](the-entity-framework-and-aspnet-getting-started-part-8/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image3.png)</span></span>

<span data-ttu-id="9627b-130">**등록 날짜** 열에는 속성 형식이 `DateTime`되기 때문에 날짜와 함께 시간이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-130">In the **Enrollment Date** column, the time is displayed along with the date because the property type is `DateTime`.</span></span> <span data-ttu-id="9627b-131">나중에이 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-131">You'll fix that later.</span></span>

<span data-ttu-id="9627b-132">지금은 Dynamic Data에서 기본 데이터 유효성 검사를 자동으로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-132">For now, notice that Dynamic Data automatically provides basic data validation.</span></span> <span data-ttu-id="9627b-133">예를 들어 **편집**을 클릭 하 고 날짜 필드의 선택을 취소 한 다음 **업데이트**를 클릭 하면 값이 데이터 모델에서 null을 허용 하지 않기 때문에 Dynamic Data에서 자동으로 필수 필드로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-133">For example, click **Edit**, clear the date field, click **Update**, and you see that Dynamic Data automatically makes this a required field because the value is not nullable in the data model.</span></span> <span data-ttu-id="9627b-134">이 페이지는 필드 뒤에 별표를 표시 하 고 `ValidationSummary` 컨트롤에 오류 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-134">The page displays an asterisk after the field and an error message in the `ValidationSummary` control:</span></span>

<span data-ttu-id="9627b-135">[![Image05](the-entity-framework-and-aspnet-getting-started-part-8/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="9627b-135">[![Image05](the-entity-framework-and-aspnet-getting-started-part-8/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image5.png)</span></span>

<span data-ttu-id="9627b-136">별표 위에 마우스 포인터를 놓으면 오류 메시지를 볼 수도 있으므로 `ValidationSummary` 컨트롤을 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-136">You could omit the `ValidationSummary` control, because you can also hold the mouse pointer over the asterisk to see the error message:</span></span>

<span data-ttu-id="9627b-137">[![Image06](the-entity-framework-and-aspnet-getting-started-part-8/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="9627b-137">[![Image06](the-entity-framework-and-aspnet-getting-started-part-8/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image7.png)</span></span>

<span data-ttu-id="9627b-138">또한 Dynamic Data **등록 날짜** 필드에 입력 한 데이터가 유효한 날짜 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-138">Dynamic Data will also validate that data entered in the **Enrollment Date** field is a valid date:</span></span>

<span data-ttu-id="9627b-139">[![Image04](the-entity-framework-and-aspnet-getting-started-part-8/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="9627b-139">[![Image04](the-entity-framework-and-aspnet-getting-started-part-8/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image9.png)</span></span>

<span data-ttu-id="9627b-140">여기에서 볼 수 있듯이 일반적인 오류 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-140">As you can see, this is a generic error message.</span></span> <span data-ttu-id="9627b-141">다음 섹션에서는 유효성 검사 및 서식 지정 규칙 뿐만 아니라 메시지를 사용자 지정 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-141">In the next section you'll see how to customize messages as well as validation and formatting rules.</span></span>

## <a name="adding-metadata-to-the-data-model"></a><span data-ttu-id="9627b-142">데이터 모델에 메타 데이터 추가</span><span class="sxs-lookup"><span data-stu-id="9627b-142">Adding Metadata to the Data Model</span></span>

<span data-ttu-id="9627b-143">일반적으로 Dynamic Data에서 제공 하는 기능을 사용자 지정 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-143">Typically, you want to customize the functionality provided by Dynamic Data.</span></span> <span data-ttu-id="9627b-144">예를 들어 데이터가 표시 되는 방법 및 오류 메시지의 내용을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-144">For example, you might change how data is displayed and the content of error messages.</span></span> <span data-ttu-id="9627b-145">일반적으로 데이터 형식에 따라 자동으로 제공 되는 Dynamic Data 보다 많은 기능을 제공 하도록 데이터 유효성 검사 규칙을 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-145">You typically also customize data validation rules to provide more functionality than what Dynamic Data provides automatically based on data types.</span></span> <span data-ttu-id="9627b-146">이렇게 하려면 엔터티 형식에 해당 하는 partial 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-146">To do this, you create partial classes that correspond to entity types.</span></span>

<span data-ttu-id="9627b-147">**솔루션 탐색기**에서 **ContosoUniversity** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **참조 추가**를 선택한 다음 `System.ComponentModel.DataAnnotations`에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-147">In **Solution Explorer**, right-click the **ContosoUniversity** project, select **Add Reference**, and add a reference to `System.ComponentModel.DataAnnotations`.</span></span>

<span data-ttu-id="9627b-148">[![Image11](the-entity-framework-and-aspnet-getting-started-part-8/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="9627b-148">[![Image11](the-entity-framework-and-aspnet-getting-started-part-8/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image11.png)</span></span>

<span data-ttu-id="9627b-149">*DAL* 폴더에서 새 클래스 파일을 만들고 이름을 *Student.cs*로 바꾼 후 해당 파일의 템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-149">In the *DAL* folder, create a new class file, name it *Student.cs*, and replace the template code in it with the following code.</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample6.cs)]

<span data-ttu-id="9627b-150">이 코드는 `Student` 엔터티에 대 한 partial 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-150">This code creates a partial class for the `Student` entity.</span></span> <span data-ttu-id="9627b-151">이 partial 클래스에 적용 되는 `MetadataType` 특성은 메타 데이터를 지정 하는 데 사용 하는 클래스를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-151">The `MetadataType` attribute applied to this partial class identifies the class that you're using to specify metadata.</span></span> <span data-ttu-id="9627b-152">메타 데이터 클래스는 어떤 이름도 가질 수 있지만, 엔터티 이름 및 "메타 데이터"를 사용 하는 것이 일반적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-152">The metadata class can have any name, but using the entity name plus "Metadata" is a common practice.</span></span>

<span data-ttu-id="9627b-153">메타 데이터 클래스의 속성에 적용 되는 특성은 형식 지정, 유효성 검사, 규칙 및 오류 메시지를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-153">The attributes applied to properties in the metadata class specify formatting, validation, rules, and error messages.</span></span> <span data-ttu-id="9627b-154">여기에 표시 된 특성에는 다음과 같은 결과가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-154">The attributes shown here will have the following results:</span></span>

- <span data-ttu-id="9627b-155">`EnrollmentDate`는 시간 없이 날짜로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-155">`EnrollmentDate` will display as a date (without a time).</span></span>
- <span data-ttu-id="9627b-156">두 이름 필드의 길이는 모두 25 자이 하 여야 하 고 사용자 지정 오류 메시지가 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-156">Both name fields must be 25 characters or less in length, and a custom error message is provided.</span></span>
- <span data-ttu-id="9627b-157">두 이름 필드가 모두 필요 하며 사용자 지정 오류 메시지가 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-157">Both name fields are required, and a custom error message is provided.</span></span>

<span data-ttu-id="9627b-158">*학습자* 페이지를 다시 실행 하면 날짜가 시간 없이 표시 되는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-158">Run the *Students.aspx* page again, and you see that the dates are now displayed without times:</span></span>

<span data-ttu-id="9627b-159">[![Image08](the-entity-framework-and-aspnet-getting-started-part-8/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="9627b-159">[![Image08](the-entity-framework-and-aspnet-getting-started-part-8/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image13.png)</span></span>

<span data-ttu-id="9627b-160">행을 편집 하 고 이름 필드의 값을 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-160">Edit a row and try to clear the values in the name fields.</span></span> <span data-ttu-id="9627b-161">필드 오류를 나타내는 별표는 **업데이트**를 클릭 하기 전에 필드를 벗어나면 바로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-161">The asterisks indicating field errors appear as soon as you leave a field, before you click **Update**.</span></span> <span data-ttu-id="9627b-162">**업데이트**를 클릭 하면 지정한 오류 메시지 텍스트가 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-162">When you click **Update**, the page displays the error message text you specified.</span></span>

<span data-ttu-id="9627b-163">[![Image10](the-entity-framework-and-aspnet-getting-started-part-8/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="9627b-163">[![Image10](the-entity-framework-and-aspnet-getting-started-part-8/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image15.png)</span></span>

<span data-ttu-id="9627b-164">25 자 보다 긴 이름을 입력 하 고 **업데이트**를 클릭 하면 지정한 오류 메시지 텍스트가 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-164">Try to enter names that are longer than 25 characters, click **Update**, and the page displays the error message text you specified.</span></span>

<span data-ttu-id="9627b-165">[![Image09](the-entity-framework-and-aspnet-getting-started-part-8/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="9627b-165">[![Image09](the-entity-framework-and-aspnet-getting-started-part-8/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image17.png)</span></span>

<span data-ttu-id="9627b-166">이제 데이터 모델 메타 데이터에서 이러한 형식 지정 및 유효성 검사 규칙을 설정 했으므로 `DynamicControl` 또는 `DynamicField` 컨트롤을 사용 하는 경우 이러한 필드를 표시 하거나 변경할 수 있도록 허용 하는 모든 페이지에 규칙이 자동으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-166">Now that you've set up these formatting and validation rules in the data model metadata, the rules will automatically be applied on every page that displays or allows changes to these fields, so long as you use `DynamicControl` or `DynamicField` controls.</span></span> <span data-ttu-id="9627b-167">이렇게 하면 프로그래밍 및 테스트를 더 쉽게 수행할 수 있도록 작성 해야 하는 중복 코드의 양이 줄어들고,이로 인해 응용 프로그램 전체에서 데이터 형식 지정 및 유효성 검사가 일관 되 게 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-167">This reduces the amount of redundant code you have to write, which makes programming and testing easier, and it ensures that data formatting and validation are consistent throughout an application.</span></span>

## <a name="more-information"></a><span data-ttu-id="9627b-168">추가 정보</span><span class="sxs-lookup"><span data-stu-id="9627b-168">More Information</span></span>

<span data-ttu-id="9627b-169">이 자습서에서는 Entity Framework 시작에 대 한이 일련의 자습서를 마칩니다.</span><span class="sxs-lookup"><span data-stu-id="9627b-169">This concludes this series of tutorials on Getting Started with the Entity Framework.</span></span> <span data-ttu-id="9627b-170">Entity Framework를 사용 하는 방법을 배우는 데 도움이 되는 자세한 내용은 [다음 Entity Framework 자습서 시리즈의 첫 번째 자습서](../continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md) 를 계속 진행 하거나 다음 사이트를 방문 하세요.</span><span class="sxs-lookup"><span data-stu-id="9627b-170">For more resources to help you learn how to use the Entity Framework, continue with [the first tutorial in the next Entity Framework tutorial series](../continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md) or visit the following sites:</span></span>

- [<span data-ttu-id="9627b-171">Entity Framework FAQ</span><span class="sxs-lookup"><span data-stu-id="9627b-171">Entity Framework FAQ</span></span>](http://www.ef-faq.org/introduction.html)
- [<span data-ttu-id="9627b-172">Entity Framework 팀 블로그</span><span class="sxs-lookup"><span data-stu-id="9627b-172">The Entity Framework Team Blog</span></span>](https://blogs.msdn.com/b/adonet/)
- [<span data-ttu-id="9627b-173">MSDN Library의 Entity Framework</span><span class="sxs-lookup"><span data-stu-id="9627b-173">Entity Framework in the MSDN Library</span></span>](https://msdn.microsoft.com/library/bb399572.aspx)
- [<span data-ttu-id="9627b-174">MSDN 데이터 개발자 센터의 Entity Framework</span><span class="sxs-lookup"><span data-stu-id="9627b-174">Entity Framework in the MSDN Data Developer Center</span></span>](https://msdn.microsoft.com/data/ef.aspx)
- [<span data-ttu-id="9627b-175">MSDN Library의 EntityDataSource 웹 서버 컨트롤 개요</span><span class="sxs-lookup"><span data-stu-id="9627b-175">EntityDataSource Web Server Control Overview in the MSDN Library</span></span>](https://msdn.microsoft.com/library/cc488502.aspx)
- [<span data-ttu-id="9627b-176">MSDN Library의 EntityDataSource control API 참조</span><span class="sxs-lookup"><span data-stu-id="9627b-176">EntityDataSource control API reference in the MSDN Library</span></span>](https://msdn.microsoft.com/library/system.web.ui.webcontrols.entitydatasource.aspx)
- [<span data-ttu-id="9627b-177">MSDN의 Entity Framework 포럼</span><span class="sxs-lookup"><span data-stu-id="9627b-177">Entity Framework Forums on MSDN</span></span>](https://social.msdn.microsoft.com/forums/adodotnetentityframework/)
- [<span data-ttu-id="9627b-178">Julie Lerman의 블로그</span><span class="sxs-lookup"><span data-stu-id="9627b-178">Julie Lerman's blog</span></span>](http://thedatafarm.com/blog/)

> [!div class="step-by-step"]
> [<span data-ttu-id="9627b-179">이전</span><span class="sxs-lookup"><span data-stu-id="9627b-179">Previous</span></span>](the-entity-framework-and-aspnet-getting-started-part-7.md)
