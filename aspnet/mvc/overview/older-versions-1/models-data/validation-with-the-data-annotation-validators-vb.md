---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
title: 데이터 주석 유효성 검사기를 사용한 유효성 검사 (VB) | Microsoft Docs
author: microsoft
description: ASP.NET MVC 응용 프로그램 내에서 유효성 검사를 수행 하려면 데이터 주석 모델 바인더를 활용 하세요. 다른 유형의 유효성 검사기를 사용 하는 방법에 대해 알아봅니다.
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 0d23ff2b-f2ec-434a-be3b-1180beeccba3
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
msc.type: authoredcontent
ms.openlocfilehash: 00150575baabc659f7dd0c07349cde52105f6c8b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435941"
---
# <a name="validation-with-the-data-annotation-validators-vb"></a><span data-ttu-id="5ef36-104">데이터 주석 유효성 검사기를 사용한 유효성 검사(VB)</span><span class="sxs-lookup"><span data-stu-id="5ef36-104">Validation with the Data Annotation Validators (VB)</span></span>

<span data-ttu-id="5ef36-105">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="5ef36-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="5ef36-106">ASP.NET MVC 응용 프로그램 내에서 유효성 검사를 수행 하려면 데이터 주석 모델 바인더를 활용 하세요.</span><span class="sxs-lookup"><span data-stu-id="5ef36-106">Take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="5ef36-107">다양 한 종류의 유효성 검사기 특성을 사용 하 고 Microsoft Entity Framework에서 작업 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-107">Learn how to use the different types of validator attributes and work with them in the Microsoft Entity Framework.</span></span>

<span data-ttu-id="5ef36-108">이 자습서에서는 데이터 주석 유효성 검사기를 사용 하 여 ASP.NET MVC 응용 프로그램에서 유효성 검사를 수행 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-108">In this tutorial, you learn how to use the Data Annotation validators to perform validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="5ef36-109">데이터 주석 유효성 검사기를 사용 하는 경우의 장점은 필수 또는 StringLength 특성과 같은 하나 이상의 특성을 클래스 속성에 추가 하 여 유효성 검사를 수행할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-109">The advantage of using the Data Annotation validators is that they enable you to perform validation simply by adding one or more attributes – such as the Required or StringLength attribute – to a class property.</span></span>

<span data-ttu-id="5ef36-110">데이터 주석 유효성 검사기를 사용 하려면 먼저 데이터 주석 모델 바인더를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-110">Before you can use the Data Annotation validators, you must download the Data Annotations Model Binder.</span></span> <span data-ttu-id="5ef36-111">CodePlex 웹 사이트에서 [여기](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471)를 클릭 하 여 데이터 주석 모델 바인더 샘플을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-111">You can download the Data Annotations Model Binder Sample from the CodePlex website by clicking [here](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471).</span></span>

<span data-ttu-id="5ef36-112">데이터 주석 모델 바인더는 Microsoft ASP.NET MVC 프레임 워크의 공식 부분이 아니라는 것을 이해 하는 것이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-112">It is important to understand that the Data Annotations Model Binder is not an official part of the Microsoft ASP.NET MVC framework.</span></span> <span data-ttu-id="5ef36-113">Microsoft ASP.NET MVC 팀에서 데이터 주석 모델 바인더를 만들었으므로 Microsoft는이 자습서에서 설명 하 고 사용 된 데이터 주석 모델 바인더에 대 한 공식적인 제품 지원을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-113">Although the Data Annotations Model Binder was created by the Microsoft ASP.NET MVC team, Microsoft does not offer official product support for the Data Annotations Model Binder described and used in this tutorial.</span></span>

## <a name="using-the-data-annotation-model-binder"></a><span data-ttu-id="5ef36-114">데이터 주석 모델 바인더 사용</span><span class="sxs-lookup"><span data-stu-id="5ef36-114">Using the Data Annotation Model Binder</span></span>

<span data-ttu-id="5ef36-115">ASP.NET MVC 응용 프로그램에서 데이터 주석 모델 바인더를 사용 하려면 먼저 System.componentmodel 어셈블리와 어셈블리에 대 한 참조를 추가 해야 합니다 .이를 위해 먼저 참조를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-115">In order to use the Data Annotations Model Binder in an ASP.NET MVC application, you first need to add a reference to the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly.</span></span> <span data-ttu-id="5ef36-116">메뉴 옵션 **프로젝트, 참조 추가를**선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-116">Select the menu option **Project, Add Reference**.</span></span> <span data-ttu-id="5ef36-117">그런 다음 **찾아보기** 탭을 클릭 하 여 데이터 주석 모델 바인더 샘플을 다운로드 하 고 압축을 푼 위치를 찾습니다 ( **그림 1**참조).</span><span class="sxs-lookup"><span data-stu-id="5ef36-117">Next click the **Browse** tab and browse to the location where you downloaded (and unzipped) the Data Annotations Model Binder sample (see **Figure 1**).</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image2.png)](validation-with-the-data-annotation-validators-vb/_static/image1.png)

<span data-ttu-id="5ef36-118">**그림 1**: 데이터 주석 모델 바인더에 대 한 참조 추가 ([전체 크기 이미지를 보려면 클릭](validation-with-the-data-annotation-validators-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="5ef36-118">**Figure 1**: Adding a reference to the Data Annotations Model Binder ([Click to view full-size image](validation-with-the-data-annotation-validators-vb/_static/image3.png))</span></span>

<span data-ttu-id="5ef36-119">System.componentmodel 어셈블리와 어셈블리를 둘 다 선택 하 고 확인 단추를 클릭 합니다 ( **확인** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-119">Select both the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly and click the **OK** button.</span></span>

<span data-ttu-id="5ef36-120">데이터 주석 모델 바인더를 사용 하 여 .NET Framework 서비스 팩 1에 포함 된 System.componentmodel 어셈블리를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-120">You cannot use the System.ComponentModel.DataAnnotations.dll assembly included with .NET Framework Service Pack 1 with the Data Annotations Model Binder.</span></span> <span data-ttu-id="5ef36-121">데이터 주석 모델 바인더 샘플 다운로드에 포함 된 System.componentmodel 어셈블리의 버전을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-121">You must use the version of the System.ComponentModel.DataAnnotations.dll assembly included with the Data Annotations Model Binder Sample download.</span></span>

<span data-ttu-id="5ef36-122">마지막으로, Global.asax 파일에 DataAnnotations 모델 바인더를 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-122">Finally, you need to register the DataAnnotations Model Binder in the Global.asax file.</span></span> <span data-ttu-id="5ef36-123">응용 프로그램\_Start () 메서드가 다음과 같이 표시 되도록 Application\_Start () 이벤트 처리기에 다음 코드 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-123">Add the following line of code to the Application\_Start() event handler so that the Application\_Start() method looks like this:</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample1.vb)]

<span data-ttu-id="5ef36-124">이 코드 줄은 DataAnnotationsModelBinder를 전체 ASP.NET MVC 응용 프로그램에 대 한 기본 모델 바인더로 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-124">This line of code registers the DataAnnotationsModelBinder as the default model binder for the entire ASP.NET MVC application.</span></span>

## <a name="using-the-data-annotation-validator-attributes"></a><span data-ttu-id="5ef36-125">데이터 주석 유효성 검사기 특성 사용</span><span class="sxs-lookup"><span data-stu-id="5ef36-125">Using the Data Annotation Validator Attributes</span></span>

<span data-ttu-id="5ef36-126">데이터 주석 모델 바인더를 사용 하는 경우 유효성 검사 특성을 사용 하 여 유효성 검사를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-126">When you use the Data Annotations Model Binder, you use validator attributes to perform validation.</span></span> <span data-ttu-id="5ef36-127">System.componentmodel 네임 스페이스는 다음과 같은 유효성 검사기 특성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-127">The System.ComponentModel.DataAnnotations namespace includes the following validator attributes:</span></span>

- <span data-ttu-id="5ef36-128">범위 – 속성 값이 지정 된 값 범위에 속하는지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-128">Range – Enables you to validate whether the value of a property falls between a specified range of values.</span></span>
- <span data-ttu-id="5ef36-129">RegularExpression – 속성 값이 지정 된 정규식 패턴과 일치 하는지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-129">RegularExpression – Enables you to validate whether the value of a property matches a specified regular expression pattern.</span></span>
- <span data-ttu-id="5ef36-130">필수 – 필요에 따라 속성을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-130">Required – Enables you to mark a property as required.</span></span>
- <span data-ttu-id="5ef36-131">StringLength – 문자열 속성의 최대 길이를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-131">StringLength – Enables you to specify a maximum length for a string property.</span></span>
- <span data-ttu-id="5ef36-132">유효성 검사 – 모든 유효성 검사기 특성에 대 한 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-132">Validation – The base class for all validator attributes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="5ef36-133">유효성 검사 요구가 표준 유효성 검사기에서 충족 되지 않는 경우에는 항상 기본 유효성 검사 특성에서 새 유효성 검사기 특성을 상속 하 여 사용자 지정 유효성 검사기 특성을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-133">If your validation needs are not satisfied by any of the standard validators then you always have the option of creating a custom validator attribute by inheriting a new validator attribute from the base Validation attribute.</span></span>

<span data-ttu-id="5ef36-134">**목록 1** 의 Product 클래스는 이러한 유효성 검사기 특성을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-134">The Product class in **Listing 1** illustrates how to use these validator attributes.</span></span> <span data-ttu-id="5ef36-135">Name, Description 및 UnitPrice 속성은 필수로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-135">The Name, Description, and UnitPrice properties are marked as required.</span></span> <span data-ttu-id="5ef36-136">이름 속성의 문자열 길이는 10 자 미만 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-136">The Name property must have a string length that is less than 10 characters.</span></span> <span data-ttu-id="5ef36-137">마지막으로 단가 속성은 통화 금액을 나타내는 정규식 패턴과 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-137">Finally, the UnitPrice property must match a regular expression pattern that represents a currency amount.</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample2.vb)]

<span data-ttu-id="5ef36-138">**목록 1**: Models\product.vb</span><span class="sxs-lookup"><span data-stu-id="5ef36-138">**Listing 1**: Models\Product.vb</span></span>

<span data-ttu-id="5ef36-139">Product 클래스는 DisplayName 특성과 같은 추가 특성을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-139">The Product class illustrates how to use one additional attribute: the DisplayName attribute.</span></span> <span data-ttu-id="5ef36-140">DisplayName 특성을 사용 하면 오류 메시지에 속성이 표시 될 때 속성의 이름을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-140">The DisplayName attribute enables you to modify the name of the property when the property is displayed in an error message.</span></span> <span data-ttu-id="5ef36-141">"UnitPrice 필드가 필요 합니다." 라는 오류 메시지를 표시 하는 대신 "Price 필드가 필요 합니다." 라는 오류 메시지를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-141">Instead of displaying the error message "The UnitPrice field is required" you can display the error message "The Price field is required".</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="5ef36-142">유효성 검사기에 표시 되는 오류 메시지를 완전히 사용자 지정 하려면 다음과 같이 유효성 검사기의 ErrorMessage 속성에 사용자 지정 오류 메시지를 할당 하면 됩니다. `<Required(ErrorMessage:="This field needs a value!")>`</span><span class="sxs-lookup"><span data-stu-id="5ef36-142">If you want to completely customize the error message displayed by a validator then you can assign a custom error message to the validator's ErrorMessage property like this: `<Required(ErrorMessage:="This field needs a value!")>`</span></span>

<span data-ttu-id="5ef36-143">목록 **2**에서 만들기 () 컨트롤러 작업과 함께 **목록 1** 에서 Product 클래스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-143">You can use the Product class in **Listing 1** with the Create() controller action in **Listing 2**.</span></span> <span data-ttu-id="5ef36-144">이 컨트롤러 작업은 모델 상태에 오류가 있을 때 Create view를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-144">This controller action redisplays the Create view when model state contains any errors.</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample3.vb)]

<span data-ttu-id="5ef36-145">**목록 2**: 제어기</span><span class="sxs-lookup"><span data-stu-id="5ef36-145">**Listing 2**: Controllers\ProductController.vb</span></span>

<span data-ttu-id="5ef36-146">마지막으로 만들기 () 작업을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **보기 추가**를 선택 하 여 **목록 3** 에서 보기를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-146">Finally, you can create the view in **Listing 3** by right-clicking the Create() action and selecting the menu option **Add View**.</span></span> <span data-ttu-id="5ef36-147">Product 클래스를 사용 하 여 모델 클래스로 강력한 형식의 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-147">Create a strongly-typed view with the Product class as the model class.</span></span> <span data-ttu-id="5ef36-148">콘텐츠 보기 드롭다운 목록에서 **만들기** 를 선택 합니다 ( **그림 2**참조).</span><span class="sxs-lookup"><span data-stu-id="5ef36-148">Select **Create** from the view content dropdown list (see **Figure 2**).</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image5.png)](validation-with-the-data-annotation-validators-vb/_static/image4.png)

<span data-ttu-id="5ef36-149">**그림 2**: Create View 추가</span><span class="sxs-lookup"><span data-stu-id="5ef36-149">**Figure 2**: Adding the Create View</span></span>

[!code-aspx[Main](validation-with-the-data-annotation-validators-vb/samples/sample4.aspx)]

<span data-ttu-id="5ef36-150">**목록 3**: Views\Product\Create.aspx</span><span class="sxs-lookup"><span data-stu-id="5ef36-150">**Listing 3**: Views\Product\Create.aspx</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="5ef36-151">**보기 추가** 메뉴 옵션으로 생성 된 만들기 폼에서 Id 필드를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-151">Remove the Id field from the Create form generated by the **Add View** menu option.</span></span> <span data-ttu-id="5ef36-152">Id 필드는 id 열에 해당 하기 때문에 사용자가이 필드에 대 한 값을 입력할 수 없도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-152">Because the Id field corresponds to an Identity column, you don't want to allow users to enter a value for this field.</span></span>

<span data-ttu-id="5ef36-153">제품을 만들기 위한 양식을 제출 하 고 필수 필드에 대 한 값을 입력 하지 않으면 **그림 3** 의 유효성 검사 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-153">If you submit the form for creating a Product and you do not enter values for the required fields, then the validation error messages in **Figure 3** are displayed.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image7.png)](validation-with-the-data-annotation-validators-vb/_static/image6.png)

<span data-ttu-id="5ef36-154">**그림 3**: 필수 필드 누락</span><span class="sxs-lookup"><span data-stu-id="5ef36-154">**Figure 3**: Missing required fields</span></span>

<span data-ttu-id="5ef36-155">잘못 된 통화 금액을 입력 하면 **그림 4** 의 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-155">If you enter an invalid currency amount, then the error message in **Figure 4** is displayed.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image9.png)](validation-with-the-data-annotation-validators-vb/_static/image8.png)

<span data-ttu-id="5ef36-156">**그림 4**: 통화 금액이 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-156">**Figure 4**: Invalid currency amount</span></span>

## <a name="using-data-annotation-validators-with-the-entity-framework"></a><span data-ttu-id="5ef36-157">Entity Framework에서 데이터 주석 유효성 검사기 사용</span><span class="sxs-lookup"><span data-stu-id="5ef36-157">Using Data Annotation Validators with the Entity Framework</span></span>

<span data-ttu-id="5ef36-158">Microsoft Entity Framework를 사용 하 여 데이터 모델 클래스를 생성 하는 경우에는 클래스에 유효성 검사기 특성을 직접 적용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-158">If you are using the Microsoft Entity Framework to generate your data model classes then you cannot apply the validator attributes directly to your classes.</span></span> <span data-ttu-id="5ef36-159">Entity Framework Designer는 모델 클래스를 생성 하므로 다음에 디자이너에서 변경 작업을 수행 하면 모델 클래스의 모든 변경 내용을 덮어쓰게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-159">Because the Entity Framework Designer generates the model classes, any changes you make to the model classes will be overwritten the next time you make any changes in the Designer.</span></span>

<span data-ttu-id="5ef36-160">Entity Framework에서 생성 된 클래스에 유효성 검사기를 사용 하려면 메타 데이터 클래스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-160">If you want to use the validators with the classes generated by the Entity Framework then you need to create meta data classes.</span></span> <span data-ttu-id="5ef36-161">실제 클래스에 유효성 검사기를 적용 하는 대신 메타 데이터 클래스에 유효성 검사기를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-161">You apply the validators to the meta data class instead of applying the validators to the actual class.</span></span>

<span data-ttu-id="5ef36-162">예를 들어 Entity Framework를 사용 하 여 동영상 클래스를 만들었다고 가정 합니다 ( **그림 5**참조).</span><span class="sxs-lookup"><span data-stu-id="5ef36-162">For example, imagine that you have created a Movie class using the Entity Framework (see **Figure 5**).</span></span> <span data-ttu-id="5ef36-163">또한 영화 제목 및 감독 속성에 필수 속성을 만들려고 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-163">Imagine, furthermore, that you want to make the Movie Title and Director properties required properties.</span></span> <span data-ttu-id="5ef36-164">이 경우 **목록 4**에서 partial 클래스 및 메타 데이터 클래스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-164">In that case, you can create the partial class and meta data class in **Listing 4**.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image11.png)](validation-with-the-data-annotation-validators-vb/_static/image10.png)

<span data-ttu-id="5ef36-165">**그림 5**: Entity Framework에서 생성 된 동영상 클래스</span><span class="sxs-lookup"><span data-stu-id="5ef36-165">**Figure 5**: Movie class generated by Entity Framework</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample5.vb)]

<span data-ttu-id="5ef36-166">**목록 4**: Models\Movie.vb</span><span class="sxs-lookup"><span data-stu-id="5ef36-166">**Listing 4**: Models\Movie.vb</span></span>

<span data-ttu-id="5ef36-167">**목록 4** 의 파일에는 Movie 및 MovieMetaData 라는 두 개의 클래스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-167">The file in **Listing 4** contains two classes named Movie and MovieMetaData.</span></span> <span data-ttu-id="5ef36-168">Movie 클래스는 partial 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-168">The Movie class is a partial class.</span></span> <span data-ttu-id="5ef36-169">DataModel 파일에 포함 된 Entity Framework에서 생성 된 partial 클래스에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-169">It corresponds to the partial class generated by the Entity Framework that is contained in the DataModel.Designer.vb file.</span></span>

<span data-ttu-id="5ef36-170">현재 .NET framework는 부분 속성을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-170">Currently, the .NET framework does not support partial properties.</span></span> <span data-ttu-id="5ef36-171">따라서 **목록 4**에서 파일에 정의 된 movie 클래스의 속성에 유효성 검사기 특성을 적용 하 여 DataModel 파일에 정의 된 movie 클래스의 속성에 유효성 검사기 특성을 적용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-171">Therefore, there is no way to apply the validator attributes to the properties of the Movie class defined in the DataModel.Designer.vb file by applying the validator attributes to the properties of the Movie class defined in the file in **Listing 4**.</span></span>

<span data-ttu-id="5ef36-172">Movie partial 클래스는 MovieMetaData 클래스를 가리키는 MetadataType 특성으로 데코 레이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-172">Notice that the Movie partial class is decorated with a MetadataType attribute that points at the MovieMetaData class.</span></span> <span data-ttu-id="5ef36-173">MovieMetaData 클래스는 Movie 클래스의 속성에 대 한 프록시 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-173">The MovieMetaData class contains proxy properties for the properties of the Movie class.</span></span>

<span data-ttu-id="5ef36-174">유효성 검사기 특성은 MovieMetaData 클래스의 속성에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-174">The validator attributes are applied to the properties of the MovieMetaData class.</span></span> <span data-ttu-id="5ef36-175">Title, Director 및 DateReleased 속성은 모두 필수 속성으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-175">The Title, Director, and DateReleased properties are all marked as required properties.</span></span> <span data-ttu-id="5ef36-176">디렉터 속성은 5 자 미만의 문자열을 할당 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-176">The Director property must be assigned a string that contains less than 5 characters.</span></span> <span data-ttu-id="5ef36-177">마지막으로 DisplayName 특성은 DateReleased 속성에 적용 되어 "출시 날짜 필드는 필수입니다."와 같은 오류 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-177">Finally, the DisplayName attribute is applied to the DateReleased property to display an error message like "The Date Released field is required."</span></span> <span data-ttu-id="5ef36-178">"DateReleased 필드가 필요 합니다." 라는 오류는 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-178">instead of the error "The DateReleased field is required."</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="5ef36-179">MovieMetaData 클래스의 프록시 속성은 Movie 클래스의 해당 속성과 동일한 형식을 나타낼 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-179">Notice that the proxy properties in the MovieMetaData class do not need to represent the same types as the corresponding properties in the Movie class.</span></span> <span data-ttu-id="5ef36-180">예를 들어 Director 속성은 Movie 클래스의 문자열 속성 및 MovieMetaData 클래스의 개체 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-180">For example, the Director property is a string property in the Movie class and an object property in the MovieMetaData class.</span></span>

<span data-ttu-id="5ef36-181">**그림 6** 의 페이지에서는 영화 속성에 대해 잘못 된 값을 입력할 때 반환 되는 오류 메시지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-181">The page in **Figure 6** illustrates the error messages returned when you enter invalid values for the Movie properties.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image13.png)](validation-with-the-data-annotation-validators-vb/_static/image12.png)

<span data-ttu-id="5ef36-182">**그림 6**: Entity Framework에 유효성 검사기 사용 ([전체 크기 이미지를 보려면 클릭](validation-with-the-data-annotation-validators-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="5ef36-182">**Figure 6**: Using validators with the Entity Framework ([Click to view full-size image](validation-with-the-data-annotation-validators-vb/_static/image14.png))</span></span>

## <a name="summary"></a><span data-ttu-id="5ef36-183">요약</span><span class="sxs-lookup"><span data-stu-id="5ef36-183">Summary</span></span>

<span data-ttu-id="5ef36-184">이 자습서에서는 데이터 주석 모델 바인더를 활용 하 여 ASP.NET MVC 응용 프로그램 내에서 유효성 검사를 수행 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-184">In this tutorial, you learned how to take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="5ef36-185">필수 및 StringLength 특성과 같은 다양 한 유형의 유효성 검사기 특성을 사용 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-185">You learned how to use the different types of validator attributes such as the Required and StringLength attributes.</span></span> <span data-ttu-id="5ef36-186">Microsoft Entity Framework로 작업할 때 이러한 특성을 사용 하는 방법도 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef36-186">You also learned how to use these attributes when working with the Microsoft Entity Framework.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="5ef36-187">이전</span><span class="sxs-lookup"><span data-stu-id="5ef36-187">Previous</span></span>](validating-with-a-service-layer-vb.md)
