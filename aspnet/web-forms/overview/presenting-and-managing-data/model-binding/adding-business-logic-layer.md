---
uid: web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
title: 모델 바인딩 및 web forms를 사용 하는 프로젝트에 비즈니스 논리 계층 추가 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서 시리즈에서는 ASP.NET Web Forms 프로젝트를 사용 하 여 모델 바인딩을 사용 하는 기본적인 측면을 보여 줍니다. 모델 바인딩을 사용 하면 데이터 상호 작용이 더 간편 하 게-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 7ef664b3-1cc8-4cbf-bb18-9f0f3a3ada2b
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
msc.type: authoredcontent
ms.openlocfilehash: a824d06d3781e11706f2a48d44ea3ad89bdb7c8b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515429"
---
# <a name="adding-business-logic-layer-to-a-project-that-uses-model-binding-and-web-forms"></a><span data-ttu-id="d6e47-104">모델 바인딩 및 web forms를 사용 하는 프로젝트에 비즈니스 논리 계층 추가</span><span class="sxs-lookup"><span data-stu-id="d6e47-104">Adding business logic layer to a project that uses model binding and web forms</span></span>

<span data-ttu-id="d6e47-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="d6e47-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="d6e47-106">이 자습서 시리즈에서는 ASP.NET Web Forms 프로젝트를 사용 하 여 모델 바인딩을 사용 하는 기본적인 측면을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="d6e47-107">모델 바인딩을 사용 하면 데이터 원본 개체 (예: ObjectDataSource 또는 SqlDataSource)를 처리 하는 것 보다 데이터 상호 작용이 보다 간단 하 게 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="d6e47-108">이 시리즈는 소개 자료로 시작 하 고 이후 자습서에서 보다 고급 개념으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="d6e47-109">이 자습서에서는 비즈니스 논리 계층에서 모델 바인딩을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-109">This tutorial shows how to use model binding with a business logic layer.</span></span> <span data-ttu-id="d6e47-110">OnCallingDataMethods 멤버를 설정 하 여 현재 페이지 이외의 개체를 사용 하 여 데이터 메서드를 호출 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-110">You will set the OnCallingDataMethods member to specify that an object other than the current page is used to call the data methods.</span></span>
> 
> <span data-ttu-id="d6e47-111">이 자습서는 시리즈의 [이전](retrieving-data.md) 부분에서 만든 프로젝트를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-111">This tutorial builds on the project created in the [earlier](retrieving-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="d6e47-112">또는 VB [download](https://go.microsoft.com/fwlink/?LinkId=286116) 에서 C# 전체 프로젝트를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-112">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="d6e47-113">다운로드 가능한 코드는 Visual Studio 2012 또는 Visual Studio 2013와 함께 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-113">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="d6e47-114">이 자습서에서는이 자습서에 표시 된 Visual Studio 2013 템플릿과 약간 다른 Visual Studio 2012 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-114">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="d6e47-115">빌드할 내용</span><span class="sxs-lookup"><span data-stu-id="d6e47-115">What you'll build</span></span>

<span data-ttu-id="d6e47-116">모델 바인딩을 사용 하면 웹 페이지 또는 별도의 비즈니스 논리 클래스에 대 한 코드 파일에 데이터 상호 작용 코드를 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-116">Model binding enables you to put your data interaction code in either the code-behind file for a web page or in a separate business logic class.</span></span> <span data-ttu-id="d6e47-117">이전 자습서에서는 데이터 상호 작용 코드에 코드 숨김이 포함 된 파일을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-117">The previous tutorials have shown how to use the code-behind files for data interaction code.</span></span> <span data-ttu-id="d6e47-118">이 접근 방식은 작은 사이트에는 적용 되지만 큰 사이트를 유지 관리 하는 경우 코드를 반복 하 고 더 어려움을 일으킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-118">This approach works for small sites but it can lead to code repetition and greater difficulty when maintaining a large site.</span></span> <span data-ttu-id="d6e47-119">또한 추상 계층이 없기 때문에 코드 뒤에 있는 코드를 프로그래밍 방식으로 테스트 하는 것이 매우 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-119">It can also be very difficult to programmatically test code that resides in code behind files because there is no abstraction layer.</span></span>

<span data-ttu-id="d6e47-120">데이터 상호 작용 코드를 중앙 집중화 하기 위해 데이터와 상호 작용 하는 모든 논리를 포함 하는 비즈니스 논리 계층을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-120">To centralize the data interaction code, you can create a business logic layer that contains all of the logic for interacting with data.</span></span> <span data-ttu-id="d6e47-121">그런 다음 웹 페이지에서 비즈니스 논리 계층을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-121">You then call the business logic layer from your web pages.</span></span> <span data-ttu-id="d6e47-122">이 자습서에서는 이전 자습서에서 작성 한 모든 코드를 비즈니스 논리 계층으로 이동한 다음 페이지에서 해당 코드를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-122">This tutorial shows how to move all of the code you have written in the previous tutorials into a business logic layer, and then use that code from the pages.</span></span>

<span data-ttu-id="d6e47-123">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-123">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="d6e47-124">코드를 코드 숨김이 아닌 파일에서 비즈니스 논리 계층으로 이동</span><span class="sxs-lookup"><span data-stu-id="d6e47-124">Move the code from code-behind files to a business logic layer</span></span>
2. <span data-ttu-id="d6e47-125">비즈니스 논리 계층에서 메서드를 호출 하도록 데이터 바인딩된 컨트롤 변경</span><span class="sxs-lookup"><span data-stu-id="d6e47-125">Change your data bound controls to call the methods in the business logic layer</span></span>

## <a name="create-business-logic-layer"></a><span data-ttu-id="d6e47-126">비즈니스 논리 계층 만들기</span><span class="sxs-lookup"><span data-stu-id="d6e47-126">Create business logic layer</span></span>

<span data-ttu-id="d6e47-127">이제 웹 페이지에서 호출 되는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-127">Now, you will create the class that is called from the web pages.</span></span> <span data-ttu-id="d6e47-128">이 클래스의 메서드는 이전 자습서에서 사용한 메서드와 비슷하며 값 공급자 특성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-128">The methods in this class look similar to the methods you used in the previous tutorials and include the value provider attributes.</span></span>

<span data-ttu-id="d6e47-129">먼저 **BLL**이라는 새 폴더를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-129">First, add a new folder called **BLL**.</span></span>

![폴더 추가](adding-business-logic-layer/_static/image1.png)

<span data-ttu-id="d6e47-131">BLL 폴더에서 **SchoolBL.cs**이라는 새 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-131">In the BLL folder, create a new class named **SchoolBL.cs**.</span></span> <span data-ttu-id="d6e47-132">여기에는 원래 코드 파일에 있는 모든 데이터 작업이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-132">It will contain all of the data operations that originally resided in code-behind files.</span></span> <span data-ttu-id="d6e47-133">메서드는 코드 숨김이 파일의 메서드와 거의 동일 하지만 몇 가지 변경 내용이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-133">The methods are almost the same as the methods in the code-behind file, but will include some changes.</span></span>

<span data-ttu-id="d6e47-134">가장 중요 한 변경 사항은 **Page** 클래스의 인스턴스 내에서 코드를 더 이상 실행 하지 않는다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-134">The most important change to note is that you are no longer executing the code from within an instance of **Page** class.</span></span> <span data-ttu-id="d6e47-135">Page 클래스에는 **TryUpdateModel** 메서드와 **modelstate** 속성이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-135">The Page class contains the **TryUpdateModel** method and the **ModelState** property.</span></span> <span data-ttu-id="d6e47-136">이 코드를 비즈니스 논리 계층으로 이동 하면 더 이상 이러한 멤버를 호출할 수 있는 페이지 클래스 인스턴스가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-136">When this code is moved to a business logic layer, you no longer have an instance of the Page class to call these members.</span></span> <span data-ttu-id="d6e47-137">이 문제를 해결 하려면 TryUpdateModel 또는 ModelState에 액세스 하는 메서드에 **Modelmethodcontext** 매개 변수를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-137">To get around this issue, you must add a **ModelMethodContext** parameter to any method that accesses TryUpdateModel or ModelState.</span></span> <span data-ttu-id="d6e47-138">이 ModelMethodContext 매개 변수를 사용 하 여 TryUpdateModel를 호출 하거나 ModelState를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-138">You use this ModelMethodContext parameter to call TryUpdateModel or retrieve ModelState.</span></span> <span data-ttu-id="d6e47-139">이 새 매개 변수를 고려 하 여 웹 페이지의 모든 항목을 변경할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-139">You do not need to change anything in the web page to account for this new parameter.</span></span>

<span data-ttu-id="d6e47-140">SchoolBL.cs의 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-140">Replace the code in SchoolBL.cs with the following code.</span></span>

[!code-csharp[Main](adding-business-logic-layer/samples/sample1.cs)]

## <a name="revise-existing-pages-to-retrieve-data-from-business-logic-layer"></a><span data-ttu-id="d6e47-141">기존 페이지를 수정 하 여 비즈니스 논리 계층에서 데이터 검색</span><span class="sxs-lookup"><span data-stu-id="d6e47-141">Revise existing pages to retrieve data from business logic layer</span></span>

<span data-ttu-id="d6e47-142">마지막으로, 비즈니스 논리 계층을 사용 하 여 코드 숨김이 파일의 쿼리를 사용 하지 못하도록 학생 .aspx, AddStudent .aspx 및 강의 페이지를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-142">Finally, you will convert the pages Students.aspx, AddStudent.aspx, and Courses.aspx from using queries in the code-behind file to using the business logic layer.</span></span>

<span data-ttu-id="d6e47-143">학생, AddStudent 및 과정에 대 한 코드 숨겨진 파일에서 다음 쿼리 메서드를 삭제 하거나 주석 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-143">In the code-behind files for Students, AddStudent, and Courses, delete or comment out the following query methods:</span></span>

- <span data-ttu-id="d6e47-144">studentsGrid\_GetData</span><span class="sxs-lookup"><span data-stu-id="d6e47-144">studentsGrid\_GetData</span></span>
- <span data-ttu-id="d6e47-145">studentsGrid\_UpdateItem</span><span class="sxs-lookup"><span data-stu-id="d6e47-145">studentsGrid\_UpdateItem</span></span>
- <span data-ttu-id="d6e47-146">studentsGrid\_DeleteItem</span><span class="sxs-lookup"><span data-stu-id="d6e47-146">studentsGrid\_DeleteItem</span></span>
- <span data-ttu-id="d6e47-147">addStudentForm\_InsertItem</span><span class="sxs-lookup"><span data-stu-id="d6e47-147">addStudentForm\_InsertItem</span></span>
- <span data-ttu-id="d6e47-148">coursesGrid\_GetData</span><span class="sxs-lookup"><span data-stu-id="d6e47-148">coursesGrid\_GetData</span></span>

<span data-ttu-id="d6e47-149">이제 데이터 작업과 관련 된 코드 파일에 코드가 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-149">You now should have no code in the code-behind file that pertains to data operations.</span></span>

<span data-ttu-id="d6e47-150">**OnCallingDataMethods** 이벤트 처리기를 사용 하 여 데이터 메서드에 사용할 개체를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-150">The **OnCallingDataMethods** event handler enables you to specify an object to use for the data methods.</span></span> <span data-ttu-id="d6e47-151">학생과 .aspx에서 해당 이벤트 처리기에 대 한 값을 추가 하 고 비즈니스 논리 클래스의 메서드 이름으로 데이터 메서드의 이름을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-151">In Students.aspx, add a value for that event handler and change the names of the data methods to the names of the methods in the business logic class.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample2.aspx?highlight=3-4,8)]

<span data-ttu-id="d6e47-152">CallingDataMethods에 대 한 코드 숨김이 파일에서 이벤트 처리기를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-152">In the code-behind file for Students.aspx, define the event handler for the CallingDataMethods event.</span></span> <span data-ttu-id="d6e47-153">이 이벤트 처리기에서 데이터 작업에 대 한 비즈니스 논리 클래스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-153">In this event handler, you specify the business logic class for data operations.</span></span>

[!code-csharp[Main](adding-business-logic-layer/samples/sample3.cs)]

<span data-ttu-id="d6e47-154">AddStudent .aspx에서 비슷한 변경을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-154">In AddStudent.aspx, make similar changes.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample4.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample5.cs)]

<span data-ttu-id="d6e47-155">Default.aspx에서 비슷한 변경을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-155">In Courses.aspx, make similar changes.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample6.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample7.cs)]

<span data-ttu-id="d6e47-156">응용 프로그램을 실행 하 고 모든 페이지가 이전 처럼 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-156">Run the application and notice that all of the pages function as they had previously.</span></span> <span data-ttu-id="d6e47-157">유효성 검사 논리도 제대로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-157">The validation logic also works correctly.</span></span>

## <a name="conclusion"></a><span data-ttu-id="d6e47-158">결론</span><span class="sxs-lookup"><span data-stu-id="d6e47-158">Conclusion</span></span>

<span data-ttu-id="d6e47-159">이 자습서에서는 데이터 액세스 계층 및 비즈니스 논리 계층을 사용 하도록 응용 프로그램을 다시 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-159">In this tutorial, you re-structured your application to use a data access layer and business logic layer.</span></span> <span data-ttu-id="d6e47-160">데이터 컨트롤에서 데이터 작업을 위해 현재 페이지가 아닌 개체를 사용 하도록 지정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d6e47-160">You specified that the data controls use an object that is not the current page for data operations.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="d6e47-161">이전</span><span class="sxs-lookup"><span data-stu-id="d6e47-161">Previous</span></span>](using-query-string-values-to-retrieve-data.md)
