---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
title: ASP.NET MVC에서 HTML5 및 jQuery UI Datepicker 팝업 일정 사용-3 부 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 편집기 템플릿, 표시 템플릿 및 jQuery UI datepicker popup을 사용 하 여 작업 하는 방법에 대 한 기본 사항을 학습 합니다. ASP.NET m ...
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 8f5f91ae-12d7-4cf3-ac09-4bb53d07ee60
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
msc.type: authoredcontent
ms.openlocfilehash: b3249397e54e64538c4dc78e5fe8b94656e8962b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433217"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-3"></a><span data-ttu-id="58d9b-103">ASP.NET MVC에서 HTML5 및 jQuery UI Datepicker 팝업 일정 사용-3 부</span><span class="sxs-lookup"><span data-stu-id="58d9b-103">Using the HTML5 and jQuery UI Datepicker Popup Calendar with ASP.NET MVC - Part 3</span></span>

<span data-ttu-id="58d9b-104">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="58d9b-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="58d9b-105">이 자습서에서는 ASP.NET MVC 웹 응용 프로그램에서 편집기 템플릿, 표시 템플릿 및 jQuery UI datepicker popup 일정을 사용 하는 방법에 대 한 기본 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-105">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery UI datepicker popup calendar in an ASP.NET MVC Web application.</span></span>

## <a name="working-with-complex-types"></a><span data-ttu-id="58d9b-106">복합 형식 작업</span><span class="sxs-lookup"><span data-stu-id="58d9b-106">Working with Complex Types</span></span>

<span data-ttu-id="58d9b-107">이 섹션에서는 address 클래스를 만들고 템플릿을 만들어 표시 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-107">In this section you'll create an address class and learn how to create a template to display it.</span></span>

<span data-ttu-id="58d9b-108">*모델* 폴더에서 *Person.cs* 이라는 새 클래스 파일을 만듭니다. 여기에는 두 가지 형식, 즉 `Person` 클래스와 `Address` 클래스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-108">In the *Models* folder, create a new class file named *Person.cs* where you'll put two types: a `Person` class and an `Address` class.</span></span> <span data-ttu-id="58d9b-109">`Person` 클래스에는 `Address`으로 형식화 된 속성이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-109">The `Person` class will contain a property that's typed as `Address`.</span></span> <span data-ttu-id="58d9b-110">`Address` 형식은 복합 형식입니다. 즉, `int`, `string`또는 `double`와 같은 기본 제공 형식 중 하나가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-110">The `Address` type is a complex type, meaning it's not one of the built-in types like `int`, `string`, or `double`.</span></span> <span data-ttu-id="58d9b-111">대신 여러 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-111">Instead, it has several properties.</span></span> <span data-ttu-id="58d9b-112">새 클래스에 대 한 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-112">The code for the new classes looks like this:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample1.cs)]

<span data-ttu-id="58d9b-113">`Movie` 컨트롤러에서 다음 `PersonDetail` 작업을 추가 하 여 person 인스턴스를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-113">In the `Movie` controller, add the following `PersonDetail` action to display a person instance:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample2.cs)]

<span data-ttu-id="58d9b-114">그런 다음 `Movie` 컨트롤러에 다음 코드를 추가 하 여 일부 샘플 데이터로 `Person` 모델을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-114">Then add the following code to the `Movie` controller to populate the `Person` model with some sample data:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample3.cs)]

<span data-ttu-id="58d9b-115">*Views\Movies\PersonDetail.cshtml* 파일을 열고 `PersonDetail` 뷰에 대해 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-115">Open the *Views\Movies\PersonDetail.cshtml* file and add the following markup for the `PersonDetail` view.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample4.cshtml)]

<span data-ttu-id="58d9b-116">Ctrl + F5 키를 눌러 응용 프로그램을 실행 하 고 *영화/PersonDetail*로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-116">Press Ctrl+F5 to run the application and navigate to *Movies/PersonDetail*.</span></span>

<span data-ttu-id="58d9b-117">이 스크린샷에서 볼 수 있듯이 `PersonDetail` 보기에는 `Address` 복합 형식이 포함 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-117">The `PersonDetail` view doesn't contain the `Address` complex type, as you can see in this screenshot.</span></span> <span data-ttu-id="58d9b-118">(주소가 표시 되지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="58d9b-118">(No address is shown.)</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image1.png)

<span data-ttu-id="58d9b-119">`Address` 모델 데이터는 복합 유형 이므로 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-119">The `Address` model data is not displayed because it's a complex type.</span></span> <span data-ttu-id="58d9b-120">주소 정보를 표시 하려면 *Views\Movies\PersonDetail.cshtml* 파일을 다시 열고 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-120">To display the address information, open the *Views\Movies\PersonDetail.cshtml* file again and add the following markup.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample5.cshtml)]

<span data-ttu-id="58d9b-121">현재 보기 `PersonDetail`의 전체 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-121">The complete markup for the `PersonDetail` now view looks like this:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample6.cshtml)]

<span data-ttu-id="58d9b-122">응용 프로그램을 다시 실행 하 고 `PersonDetail` 보기를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-122">Run the application again and display the `PersonDetail` view.</span></span> <span data-ttu-id="58d9b-123">이제 주소 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-123">The address information is now displayed:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image2.png)

### <a name="creating-a-template-for-a-complex-type"></a><span data-ttu-id="58d9b-124">복합 형식에 대 한 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="58d9b-124">Creating a Template for a Complex Type</span></span>

<span data-ttu-id="58d9b-125">이 섹션에서는 `Address` 복합 유형을 렌더링 하는 데 사용 되는 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-125">In this section you'll create a template that will be used to render the `Address` complex type.</span></span> <span data-ttu-id="58d9b-126">`Address` 형식에 대 한 템플릿을 만들 때 ASP.NET MVC는 자동으로이를 사용 하 여 응용 프로그램의 모든 위치에서 주소 모델의 형식을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-126">When you create a template for the `Address` type, ASP.NET MVC can automatically use it to format an address model anywhere in the application.</span></span> <span data-ttu-id="58d9b-127">이렇게 하면 응용 프로그램의 한 곳에서 `Address` 형식의 렌더링을 제어 하는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-127">This gives you a way to control the rendering of the `Address` type from just one place in the application.</span></span>

<span data-ttu-id="58d9b-128">*Views\Shared\DisplayTemplates* 폴더에서 **Address**라는 강력한 형식의 부분 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-128">In the *Views\Shared\DisplayTemplates* folder, create a strongly typed partial view named **Address**:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image3.png)

<span data-ttu-id="58d9b-129">**추가**를 클릭 한 다음 새 *Views\Shared\DisplayTemplates\Address.cshtml* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-129">Click **Add**, and then open the new *Views\Shared\DisplayTemplates\Address.cshtml* file.</span></span> <span data-ttu-id="58d9b-130">새 뷰에는 다음과 같은 생성 된 태그가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-130">The new view contains the following generated markup:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample7.cshtml)]

<span data-ttu-id="58d9b-131">응용 프로그램을 실행 하 고 `PersonDetail` 보기를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-131">Run the application and display the `PersonDetail` view.</span></span> <span data-ttu-id="58d9b-132">이번에는 방금 만든 `Address` 템플릿이 `Address` 복합 형식을 표시 하는 데 사용 되므로 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-132">This time, the `Address` template that you just created is used to display the `Address` complex type, so the display looks like the following:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image4.png)

### <a name="summary-ways-to-specify-the-model-display-format-and-template"></a><span data-ttu-id="58d9b-133">요약: 모델 표시 형식 및 템플릿을 지정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="58d9b-133">Summary: Ways to Specify the Model Display Format and Template</span></span>

<span data-ttu-id="58d9b-134">다음 방법을 사용 하 여 모델 속성에 대 한 서식 또는 템플릿을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-134">You've seen that you can specify the format or template for a model property by using the following approaches:</span></span>

- <span data-ttu-id="58d9b-135">모델의 속성에 `DisplayFormat` 특성을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-135">Applying the `DisplayFormat` attribute to a property in the model.</span></span> <span data-ttu-id="58d9b-136">예를 들어 다음 코드는 시간 없이 날짜를 표시 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-136">For example, the following code causes the date to be displayed without the time:</span></span>

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample8.cs)]
- <span data-ttu-id="58d9b-137">모델의 속성에 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 특성을 적용 하 고 데이터 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-137">Applying a [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attribute to a property in the model and specifying the data type.</span></span> <span data-ttu-id="58d9b-138">예를 들어 다음 코드는 시간 없이 날짜를 표시 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-138">For example, the following code causes the date to be displayed without the time.</span></span>

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample9.cs)]

    <span data-ttu-id="58d9b-139">응용 프로그램의 *Views\Shared\DisplayTemplates* 폴더 또는 *Views\Movies\DisplayTemplates* 폴더에 *date. cshtml* 템플릿이 포함 되어 있으면 해당 템플릿이 `DateTime` 속성을 렌더링 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-139">If the application contains a *date.cshtml* template in the *Views\Shared\DisplayTemplates* folder or the *Views\Movies\DisplayTemplates* folder, that template will be used to render the `DateTime` property.</span></span> <span data-ttu-id="58d9b-140">그렇지 않으면 기본 제공 ASP.NET 템플릿 시스템은 속성을 날짜로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-140">Otherwise the built-in ASP.NET templating system displays the property as a date.</span></span>
- <span data-ttu-id="58d9b-141">서식 지정 하려는 데이터 형식과 이름이 일치 하는 *Views\Shared\DisplayTemplates* 폴더 또는 *Views\Movies\DisplayTemplates* 폴더에 표시 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="58d9b-141">Creating a display template in the *Views\Shared\DisplayTemplates* folder or the *Views\Movies\DisplayTemplates* folder whose name matches the data type that you want to format.</span></span> <span data-ttu-id="58d9b-142">예를 들어 모델에 특성을 추가 하 고 뷰에 태그를 추가 하지 않고 모델에서 `DateTime` 속성을 렌더링 하는 데 *Views\Shared\DisplayTemplates\DateTime.cshtml* 를 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-142">For example, you saw that the *Views\Shared\DisplayTemplates\DateTime.cshtml* was used to render `DateTime` properties in a model, without adding an attribute to the model and without adding any markup to views.</span></span>
- <span data-ttu-id="58d9b-143">모델에서 [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) 특성을 사용 하 여 모델 속성을 표시 하는 템플릿을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-143">Using the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute on the model to specify the template to display the model property.</span></span>
- <span data-ttu-id="58d9b-144">보기에서 호출 [에 대 한 표시 템플릿 이름을 Html. displayfor](https://msdn.microsoft.com/library/ee407420.aspx) 명시적으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-144">Explicitly adding the display template name to the [Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) call in a view.</span></span>

<span data-ttu-id="58d9b-145">사용 하는 방법은 응용 프로그램에서 수행 해야 하는 작업에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-145">The approach you use depends on what you need to do in your application.</span></span> <span data-ttu-id="58d9b-146">이러한 접근 방식을 혼합 하 여 필요한 형식 지정을 정확 하 게 수행 하는 것은 일반적이 지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-146">It's not uncommon to mix these approaches to get exactly the kind of formatting that you need.</span></span>

<span data-ttu-id="58d9b-147">다음 섹션에서는 기어를 전환 하 고 데이터를 표시 하는 방법을 사용자 지정 하 여 이동 하는 방법을 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-147">In the next section, you'll switch gears a bit and move from customizing how data is displayed to customizing how it's entered.</span></span> <span data-ttu-id="58d9b-148">날짜를 지정 하는 정면 방법을 제공 하기 위해 응용 프로그램의 편집 뷰에 jQuery datepicker를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="58d9b-148">You'll hook up the jQuery datepicker to the edit views in the application in order to provide a slick way to specify dates.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="58d9b-149">[이전](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
> [다음](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="58d9b-149">[Previous](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
[Next](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)</span></span>
