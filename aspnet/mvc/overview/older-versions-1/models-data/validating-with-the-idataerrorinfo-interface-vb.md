---
uid: mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-vb
title: IDataErrorInfo 인터페이스를 사용 하 여 유효성 검사 (VB) | Microsoft Docs
author: StephenWalther
description: Stephen Walther는 모델 클래스에서 IDataErrorInfo 인터페이스를 구현 하 여 사용자 지정 유효성 검사 오류 메시지를 표시 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 3a8a9d9f-82dd-4959-b7c6-960e9ce95df1
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: 8ff3adc5db8114dcca2c66d937e1706f0bac0d30
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78436301"
---
# <a name="validating-with-the-idataerrorinfo-interface-vb"></a><span data-ttu-id="94ec1-103">IDataErrorInfo 인터페이스를 사용한 유효성 검사(VB)</span><span class="sxs-lookup"><span data-stu-id="94ec1-103">Validating with the IDataErrorInfo Interface (VB)</span></span>

<span data-ttu-id="94ec1-104">[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="94ec1-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="94ec1-105">Stephen Walther는 모델 클래스에서 IDataErrorInfo 인터페이스를 구현 하 여 사용자 지정 유효성 검사 오류 메시지를 표시 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-105">Stephen Walther shows you how to display custom validation error messages by implementing the IDataErrorInfo interface in a model class.</span></span>

<span data-ttu-id="94ec1-106">이 자습서의 목표는 ASP.NET MVC 응용 프로그램에서 유효성 검사를 수행 하는 한 가지 방법을 설명 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-106">The goal of this tutorial is to explain one approach to performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="94ec1-107">사용자가 필요한 양식 필드에 값을 제공 하지 않고 HTML 양식을 전송 하지 못하도록 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-107">You learn how to prevent someone from submitting an HTML form without providing values for required form fields.</span></span> <span data-ttu-id="94ec1-108">이 자습서에서는 IErrorDataInfo 인터페이스를 사용 하 여 유효성 검사를 수행 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-108">In this tutorial, you learn how to perform validation by using the IErrorDataInfo interface.</span></span>

## <a name="assumptions"></a><span data-ttu-id="94ec1-109">가정</span><span class="sxs-lookup"><span data-stu-id="94ec1-109">Assumptions</span></span>

<span data-ttu-id="94ec1-110">이 자습서에서는 MoviesDB 데이터베이스와 영화 데이터베이스 테이블을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-110">In this tutorial, I'll use the MoviesDB database and the Movies database table.</span></span> <span data-ttu-id="94ec1-111">이 테이블에는 다음 열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-111">This table has the following columns:</span></span>

<a id="0.6_table01"></a>

| <span data-ttu-id="94ec1-112">**열 이름**</span><span class="sxs-lookup"><span data-stu-id="94ec1-112">**Column Name**</span></span> | <span data-ttu-id="94ec1-113">**데이터 형식**</span><span class="sxs-lookup"><span data-stu-id="94ec1-113">**Data Type**</span></span> | <span data-ttu-id="94ec1-114">**Null 허용**</span><span class="sxs-lookup"><span data-stu-id="94ec1-114">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="94ec1-115">Id</span><span class="sxs-lookup"><span data-stu-id="94ec1-115">Id</span></span> | <span data-ttu-id="94ec1-116">Int</span><span class="sxs-lookup"><span data-stu-id="94ec1-116">Int</span></span> | <span data-ttu-id="94ec1-117">False</span><span class="sxs-lookup"><span data-stu-id="94ec1-117">False</span></span> |
| <span data-ttu-id="94ec1-118">제목</span><span class="sxs-lookup"><span data-stu-id="94ec1-118">Title</span></span> | <span data-ttu-id="94ec1-119">Nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="94ec1-119">Nvarchar(100)</span></span> | <span data-ttu-id="94ec1-120">False</span><span class="sxs-lookup"><span data-stu-id="94ec1-120">False</span></span> |
| <span data-ttu-id="94ec1-121">감독</span><span class="sxs-lookup"><span data-stu-id="94ec1-121">Director</span></span> | <span data-ttu-id="94ec1-122">Nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="94ec1-122">Nvarchar(100)</span></span> | <span data-ttu-id="94ec1-123">False</span><span class="sxs-lookup"><span data-stu-id="94ec1-123">False</span></span> |
| <span data-ttu-id="94ec1-124">DateReleased</span><span class="sxs-lookup"><span data-stu-id="94ec1-124">DateReleased</span></span> | <span data-ttu-id="94ec1-125">DateTime</span><span class="sxs-lookup"><span data-stu-id="94ec1-125">DateTime</span></span> | <span data-ttu-id="94ec1-126">False</span><span class="sxs-lookup"><span data-stu-id="94ec1-126">False</span></span> |

<span data-ttu-id="94ec1-127">이 자습서에서는 Microsoft Entity Framework를 사용 하 여 내 데이터베이스 모델 클래스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-127">In this tutorial, I use the Microsoft Entity Framework to generate my database model classes.</span></span> <span data-ttu-id="94ec1-128">Entity Framework에서 생성 된 Movie 클래스는 그림 1에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-128">The Movie class generated by the Entity Framework is displayed in Figure 1.</span></span>

<span data-ttu-id="94ec1-129">[Movie 엔터티 ![](validating-with-the-idataerrorinfo-interface-vb/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="94ec1-129">[![The Movie entity](validating-with-the-idataerrorinfo-interface-vb/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image1.png)</span></span>

<span data-ttu-id="94ec1-130">**그림 01**: 동영상 엔터티 ([전체 크기 이미지를 보려면 클릭](validating-with-the-idataerrorinfo-interface-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="94ec1-130">**Figure 01**: The Movie entity([Click to view full-size image](validating-with-the-idataerrorinfo-interface-vb/_static/image2.png))</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="94ec1-131">Entity Framework를 사용 하 여 데이터베이스 모델 클래스를 생성 하는 방법에 대 한 자세한 내용은 Entity Framework를 사용 하 여 모델 클래스 만들기의 자습서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="94ec1-131">To learn more about using the Entity Framework to generate your database model classes, see my tutorial entitled Creating Model Classes with the Entity Framework.</span></span>

## <a name="the-controller-class"></a><span data-ttu-id="94ec1-132">Controller 클래스</span><span class="sxs-lookup"><span data-stu-id="94ec1-132">The Controller Class</span></span>

<span data-ttu-id="94ec1-133">Home 컨트롤러를 사용 하 여 영화를 나열 하 고 새 영화를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-133">We use the Home controller to list movies and create new movies.</span></span> <span data-ttu-id="94ec1-134">이 클래스의 코드는 목록 1에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-134">The code for this class is contained in Listing 1.</span></span>

<span data-ttu-id="94ec1-135">**목록 1-Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="94ec1-135">**Listing 1 - Controllers\HomeController.vb**</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample1.vb)]

<span data-ttu-id="94ec1-136">목록 1의 홈 컨트롤러 클래스는 두 개의 Create () 작업을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-136">The Home controller class in Listing 1 contains two Create() actions.</span></span> <span data-ttu-id="94ec1-137">첫 번째 작업은 새 동영상을 만들기 위한 HTML 양식을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-137">The first action displays the HTML form for creating a new movie.</span></span> <span data-ttu-id="94ec1-138">두 번째 Create () 작업은 데이터베이스에 새 동영상을 실제로 삽입 하는 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-138">The second Create() action performs the actual insert of the new movie into the database.</span></span> <span data-ttu-id="94ec1-139">두 번째 Create () 작업은 첫 번째 Create () 작업에 의해 표시 되는 양식이 서버에 전송 될 때 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-139">The second Create() action is invoked when the form displayed by the first Create() action is submitted to the server.</span></span>

<span data-ttu-id="94ec1-140">두 번째 Create () 작업에는 다음 코드 줄이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-140">Notice that the second Create() action contains the following lines of code:</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample2.vb)]

<span data-ttu-id="94ec1-141">유효성 검사 오류가 있는 경우 IsValid 속성은 false를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-141">The IsValid property returns false when there is a validation error.</span></span> <span data-ttu-id="94ec1-142">이 경우 동영상을 만들기 위한 HTML 양식이 포함 된 Create 뷰가 다시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-142">In that case, the Create view that contains the HTML form for creating a movie is redisplayed.</span></span>

## <a name="creating-a-partial-class"></a><span data-ttu-id="94ec1-143">Partial 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="94ec1-143">Creating a Partial Class</span></span>

<span data-ttu-id="94ec1-144">Movie 클래스는 Entity Framework에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-144">The Movie class is generated by the Entity Framework.</span></span> <span data-ttu-id="94ec1-145">솔루션 탐색기 창에서 MoviesDBModel 파일을 확장 하 고 코드 편집기에서 MoviesDBModel 파일을 여는 경우 Movie 클래스에 대 한 코드를 볼 수 있습니다 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="94ec1-145">You can see the code for the Movie class if you expand the MoviesDBModel.edmx file in the Solution Explorer window and open the MoviesDBModel.Designer.vb file in the Code Editor (see Figure 2).</span></span>

<span data-ttu-id="94ec1-146">[Movie 엔터티에 대 한 코드 ![](validating-with-the-idataerrorinfo-interface-vb/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="94ec1-146">[![The code for the Movie entity](validating-with-the-idataerrorinfo-interface-vb/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image3.png)</span></span>

<span data-ttu-id="94ec1-147">**그림 02**: 동영상 엔터티에 대 한 코드 ([전체 크기 이미지를 보려면 클릭](validating-with-the-idataerrorinfo-interface-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="94ec1-147">**Figure 02**: The code for the Movie entity([Click to view full-size image](validating-with-the-idataerrorinfo-interface-vb/_static/image4.png))</span></span>

<span data-ttu-id="94ec1-148">Movie 클래스는 partial 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-148">The Movie class is a partial class.</span></span> <span data-ttu-id="94ec1-149">즉, 동일한 이름으로 다른 partial 클래스를 추가 하 여 Movie 클래스의 기능을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-149">That means that we can add another partial class with the same name to extend the functionality of the Movie class.</span></span> <span data-ttu-id="94ec1-150">새 partial 클래스에 유효성 검사 논리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-150">We'll add our validation logic to the new partial class.</span></span>

<span data-ttu-id="94ec1-151">목록 2의 클래스를 모델 폴더에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-151">Add the class in Listing 2 to the Models folder.</span></span>

<span data-ttu-id="94ec1-152">**목록 2-Models\Movie.vb**</span><span class="sxs-lookup"><span data-stu-id="94ec1-152">**Listing 2 - Models\Movie.vb**</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample3.vb)]

<span data-ttu-id="94ec1-153">목록 2의 클래스에는 *partial* 한정자가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-153">Notice that the class in Listing 2 includes the *partial* modifier.</span></span> <span data-ttu-id="94ec1-154">이 클래스에 추가 하는 메서드나 속성은 Entity Framework에서 생성 된 Movie 클래스의 일부가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-154">Any methods or properties that you add to this class become part of the Movie class generated by the Entity Framework.</span></span>

## <a name="adding-onchanging-and-onchanged-partial-methods"></a><span data-ttu-id="94ec1-155">OnChanging 및 Onchanging 부분 메서드 추가</span><span class="sxs-lookup"><span data-stu-id="94ec1-155">Adding OnChanging and OnChanged Partial Methods</span></span>

<span data-ttu-id="94ec1-156">Entity Framework에서 엔터티 클래스를 생성 하는 경우 Entity Framework는 부분 메서드를 클래스에 자동으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-156">When the Entity Framework generates an entity class, the Entity Framework adds partial methods to the class automatically.</span></span> <span data-ttu-id="94ec1-157">Entity Framework는 클래스의 각 속성에 해당 하는 OnChanging 및 Onchanging 부분 메서드를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-157">The Entity Framework generates OnChanging and OnChanged partial methods that correspond to each property of the class.</span></span>

<span data-ttu-id="94ec1-158">Movie 클래스의 경우 Entity Framework은 다음 메서드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-158">In the case of the Movie class, the Entity Framework creates the following methods:</span></span>

- <span data-ttu-id="94ec1-159">OnIdChanging</span><span class="sxs-lookup"><span data-stu-id="94ec1-159">OnIdChanging</span></span>
- <span data-ttu-id="94ec1-160">OnIdChanged</span><span class="sxs-lookup"><span data-stu-id="94ec1-160">OnIdChanged</span></span>
- <span data-ttu-id="94ec1-161">OnTitleChanging</span><span class="sxs-lookup"><span data-stu-id="94ec1-161">OnTitleChanging</span></span>
- <span data-ttu-id="94ec1-162">OnTitleChanged</span><span class="sxs-lookup"><span data-stu-id="94ec1-162">OnTitleChanged</span></span>
- <span data-ttu-id="94ec1-163">OnDirectorChanging</span><span class="sxs-lookup"><span data-stu-id="94ec1-163">OnDirectorChanging</span></span>
- <span data-ttu-id="94ec1-164">OnDirectorChanged</span><span class="sxs-lookup"><span data-stu-id="94ec1-164">OnDirectorChanged</span></span>
- <span data-ttu-id="94ec1-165">OnDateReleasedChanging</span><span class="sxs-lookup"><span data-stu-id="94ec1-165">OnDateReleasedChanging</span></span>
- <span data-ttu-id="94ec1-166">OnDateReleasedChanged</span><span class="sxs-lookup"><span data-stu-id="94ec1-166">OnDateReleasedChanged</span></span>

<span data-ttu-id="94ec1-167">OnChanging 메서드는 해당 속성이 변경 되기 직전에 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-167">The OnChanging method is called right before the corresponding property is changed.</span></span> <span data-ttu-id="94ec1-168">OnChanged 메서드는 속성이 변경 된 직후에 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-168">The OnChanged method is called right after the property is changed.</span></span>

<span data-ttu-id="94ec1-169">이러한 부분 메서드를 활용 하 여 영화 클래스에 유효성 검사 논리를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-169">You can take advantage of these partial methods to add validation logic to the Movie class.</span></span> <span data-ttu-id="94ec1-170">목록 3의 업데이트 동영상 클래스는 제목 및 감독 속성에 비어 있지 않은 값이 할당 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-170">The update Movie class in Listing 3 verifies that the Title and Director properties are assigned nonempty values.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="94ec1-171">부분 메서드 (partial method)는 구현 하지 않아도 되는 클래스에 정의 된 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-171">A partial method is a method defined in a class that you are not required to implement.</span></span> <span data-ttu-id="94ec1-172">부분 메서드를 구현 하지 않는 경우 컴파일러는 메서드 시그니처와 해당 메서드에 대 한 모든 호출을 제거 하 여 부분 메서드와 관련 된 런타임 비용이 발생 하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-172">If you don't implement a partial method then the compiler removes the method signature and all calls to the method so there are no run-time costs associated with the partial method.</span></span> <span data-ttu-id="94ec1-173">Visual Studio Code 편집기에서 *partial 키워드 뒤에 공백을* 입력 하 여 부분 메서드를 추가 하 여 구현할 부분 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-173">In the Visual Studio Code Editor, you can add a partial method by typing the keyword *partial* followed by a space to view a list of partials to implement.</span></span>

<span data-ttu-id="94ec1-174">**목록 3-Models\Movie.vb**</span><span class="sxs-lookup"><span data-stu-id="94ec1-174">**Listing 3 - Models\Movie.vb**</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample4.vb)]

<span data-ttu-id="94ec1-175">예를 들어 Title 속성에 빈 문자열을 할당 하려고 하면 \_오류 라는 사전에 오류 메시지가 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-175">For example, if you attempt to assign an empty string to the Title property, then an error message is assigned to a Dictionary named \_errors.</span></span>

<span data-ttu-id="94ec1-176">이 시점에서 Title 속성에 빈 문자열을 할당 하면 실제로는 발생 하지 않으며 전용 \_오류 필드에 오류가 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-176">At this point, nothing actually happens when you assign an empty string to the Title property and an error is added to the private \_errors field.</span></span> <span data-ttu-id="94ec1-177">ASP.NET MVC 프레임 워크에 이러한 유효성 검사 오류를 노출 하려면 IDataErrorInfo 인터페이스를 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-177">We need to implement the IDataErrorInfo interface to expose these validation errors to the ASP.NET MVC framework.</span></span>

## <a name="implementing-the-idataerrorinfo-interface"></a><span data-ttu-id="94ec1-178">IDataErrorInfo 인터페이스 구현</span><span class="sxs-lookup"><span data-stu-id="94ec1-178">Implementing the IDataErrorInfo Interface</span></span>

<span data-ttu-id="94ec1-179">IDataErrorInfo 인터페이스는 첫 번째 버전 이후 .NET framework의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-179">The IDataErrorInfo interface has been part of the .NET framework since the first version.</span></span> <span data-ttu-id="94ec1-180">이 인터페이스는 매우 간단한 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-180">This interface is a very simple interface:</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample5.vb)]

<span data-ttu-id="94ec1-181">클래스가 IDataErrorInfo 인터페이스를 구현 하는 경우 ASP.NET MVC 프레임 워크는 클래스의 인스턴스를 만들 때이 인터페이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-181">If a class implements the IDataErrorInfo interface, the ASP.NET MVC framework will use this interface when creating an instance of the class.</span></span> <span data-ttu-id="94ec1-182">예를 들어 Home controller Create () 작업은 Movie 클래스의 인스턴스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-182">For example, the Home controller Create() action accepts an instance of the Movie class:</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample6.vb)]

<span data-ttu-id="94ec1-183">ASP.NET MVC 프레임 워크는 모델 바인더 (DefaultModelBinder)를 사용 하 여 Create () 작업에 전달 되는 동영상의 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-183">The ASP.NET MVC framework creates the instance of the Movie passed to the Create() action by using a model binder (the DefaultModelBinder).</span></span> <span data-ttu-id="94ec1-184">모델 바인더는 HTML 양식 필드를 Movie 개체의 인스턴스에 바인딩하여 Movie 개체의 인스턴스를 만드는 역할을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-184">The model binder is responsible for creating an instance of the Movie object by binding the HTML form fields to an instance of the Movie object.</span></span>

<span data-ttu-id="94ec1-185">DefaultModelBinder는 클래스가 IDataErrorInfo 인터페이스를 구현 하는지 여부를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-185">The DefaultModelBinder detects whether or not a class implements the IDataErrorInfo interface.</span></span> <span data-ttu-id="94ec1-186">클래스가이 인터페이스를 구현 하는 경우 모델 바인더는 클래스의 각 속성에 대해 IDataErrorInfo를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-186">If a class implements this interface then the model binder invokes the IDataErrorInfo.this indexer for each property of the class.</span></span> <span data-ttu-id="94ec1-187">인덱서가 오류 메시지를 반환 하는 경우 모델 바인더는이 오류 메시지를 자동으로 모델 상태에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-187">If the indexer returns an error message then the model binder adds this error message to model state automatically.</span></span>

<span data-ttu-id="94ec1-188">DefaultModelBinder도 IDataErrorInfo 속성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-188">The DefaultModelBinder also checks the IDataErrorInfo.Error property.</span></span> <span data-ttu-id="94ec1-189">이 속성은 클래스와 연결 된 속성이 아닌 특정 유효성 검사 오류를 나타내기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-189">This property is intended to represent non-property specific validation errors associated with the class.</span></span> <span data-ttu-id="94ec1-190">예를 들어 Movie 클래스의 여러 속성 값에 따라 달라 지는 유효성 검사 규칙을 적용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-190">For example, you might want to enforce a validation rule that depends on the values of multiple properties of the Movie class.</span></span> <span data-ttu-id="94ec1-191">이 경우 오류 속성에서 유효성 검사 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-191">In that case, you would return a validation error from the Error property.</span></span>

<span data-ttu-id="94ec1-192">목록 4의 업데이트 된 동영상 클래스는 IDataErrorInfo 인터페이스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-192">The updated Movie class in Listing 4 implements the IDataErrorInfo interface.</span></span>

<span data-ttu-id="94ec1-193">**목록 4-Models\Movie.vb (구현 IDataErrorInfo)**</span><span class="sxs-lookup"><span data-stu-id="94ec1-193">**Listing 4 - Models\Movie.vb (implements IDataErrorInfo)**</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample7.vb)]

<span data-ttu-id="94ec1-194">목록 4에서 인덱서 속성은 \_errors 컬렉션에서 인덱서에 전달 된 속성 이름에 해당 하는 키가 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-194">In Listing 4, the indexer property checks the \_errors collection to see if it contains a key that corresponds to the property name passed to the indexer.</span></span> <span data-ttu-id="94ec1-195">속성과 연결 된 유효성 검사 오류가 없으면 빈 문자열이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-195">If there is no validation error associated with the property then an empty string is returned.</span></span>

<span data-ttu-id="94ec1-196">수정 된 Movie 클래스를 사용 하는 방식으로 홈 컨트롤러를 수정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-196">You don't need to modify the Home controller in any way to use the modified Movie class.</span></span> <span data-ttu-id="94ec1-197">그림 3에 표시 된 페이지는 제목 또는 감독 양식 필드에 값을 입력 하지 않은 경우 발생 하는 상황을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-197">The page displayed in Figure 3 illustrates what happens when no value is entered for the Title or Director form fields.</span></span>

<span data-ttu-id="94ec1-198">[작업 메서드 자동 생성 ![](validating-with-the-idataerrorinfo-interface-vb/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="94ec1-198">[![Creating action methods automatically](validating-with-the-idataerrorinfo-interface-vb/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image5.png)</span></span>

<span data-ttu-id="94ec1-199">**그림 03**: 누락 된 값이 있는 폼 ([전체 크기 이미지를 보려면 클릭](validating-with-the-idataerrorinfo-interface-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="94ec1-199">**Figure 03**: A form with missing values ([Click to view full-size image](validating-with-the-idataerrorinfo-interface-vb/_static/image6.png))</span></span>

<span data-ttu-id="94ec1-200">DateReleased 값의 유효성이 자동으로 검사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-200">Notice that the DateReleased value is validated automatically.</span></span> <span data-ttu-id="94ec1-201">DateReleased 속성은 NULL 값을 허용 하지 않으므로 DefaultModelBinder는 값이 없는 경우이 속성에 대 한 유효성 검사 오류를 자동으로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-201">Because the DateReleased property does not accept NULL values, the DefaultModelBinder generates a validation error for this property automatically when it does not have a value.</span></span> <span data-ttu-id="94ec1-202">DateReleased 속성에 대 한 오류 메시지를 수정 하려면 사용자 지정 모델 바인더를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-202">If you want to modify the error message for the DateReleased property then you need to create a custom model binder.</span></span>

## <a name="summary"></a><span data-ttu-id="94ec1-203">요약</span><span class="sxs-lookup"><span data-stu-id="94ec1-203">Summary</span></span>

<span data-ttu-id="94ec1-204">이 자습서에서는 IDataErrorInfo 인터페이스를 사용 하 여 유효성 검사 오류 메시지를 생성 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-204">In this tutorial, you learned how to use the IDataErrorInfo interface to generate validation error messages.</span></span> <span data-ttu-id="94ec1-205">먼저 Entity Framework에서 생성 된 부분 동영상 클래스의 기능을 확장 하는 부분 동영상 클래스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-205">First, we created a partial Movie class that extends the functionality of the partial Movie class generated by the Entity Framework.</span></span> <span data-ttu-id="94ec1-206">다음으로, 영화 클래스 OnTitleChanging () 및 OnDirectorChanging () 부분 메서드에 유효성 검사 논리를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-206">Next, we added validation logic to the Movie class OnTitleChanging() and OnDirectorChanging() partial methods.</span></span> <span data-ttu-id="94ec1-207">마지막으로 ASP.NET MVC 프레임 워크에 이러한 유효성 검사 메시지를 노출 하기 위해 IDataErrorInfo 인터페이스를 구현 했습니다.</span><span class="sxs-lookup"><span data-stu-id="94ec1-207">Finally, we implemented the IDataErrorInfo interface in order to expose these validation messages to the ASP.NET MVC framework.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="94ec1-208">[이전](performing-simple-validation-vb.md)
> [다음](validating-with-a-service-layer-vb.md)</span><span class="sxs-lookup"><span data-stu-id="94ec1-208">[Previous](performing-simple-validation-vb.md)
[Next](validating-with-a-service-layer-vb.md)</span></span>
