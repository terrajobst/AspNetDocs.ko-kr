---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
title: ASP.NET MVC에서 HTML5 및 jQuery UI Datepicker 팝업 일정 사용-2 부 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 편집기 템플릿, 표시 템플릿 및 jQuery UI datepicker popup을 사용 하 여 작업 하는 방법에 대 한 기본 사항을 학습 합니다. ASP.NET m ...
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 21a178de-4c5a-4211-8a9c-74ec576c0f30
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
msc.type: authoredcontent
ms.openlocfilehash: 325cc90eb6e717c47863eda6253e0d48d796386b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455895"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-2"></a><span data-ttu-id="1bbe9-103">ASP.NET MVC에서 HTML5 및 jQuery UI Datepicker 팝업 일정 사용-2 부</span><span class="sxs-lookup"><span data-stu-id="1bbe9-103">Using the HTML5 and jQuery UI Datepicker Popup Calendar with ASP.NET MVC - Part 2</span></span>

<span data-ttu-id="1bbe9-104">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="1bbe9-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="1bbe9-105">이 자습서에서는 ASP.NET MVC 웹 응용 프로그램에서 편집기 템플릿, 표시 템플릿 및 jQuery UI datepicker popup 일정을 사용 하는 방법에 대 한 기본 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-105">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery UI datepicker popup calendar in an ASP.NET MVC Web application.</span></span>

## <a name="adding-an-automatic-datetime-template"></a><span data-ttu-id="1bbe9-106">자동 DateTime 템플릿 추가</span><span class="sxs-lookup"><span data-stu-id="1bbe9-106">Adding an Automatic DateTime Template</span></span>

<span data-ttu-id="1bbe9-107">이 자습서의 첫 번째 부분에서는 모델에 특성을 추가 하 여 서식 지정을 명시적으로 지정 하는 방법과 모델을 렌더링 하는 데 사용 되는 템플릿을 명시적으로 지정 하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-107">In the first part of this tutorial, you saw how you can add attributes to the model to explicitly specify formatting, and how you can explicitly specify the template that's used to render the model.</span></span> <span data-ttu-id="1bbe9-108">예를 들어 다음 코드의 [Displayformat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 특성은 `ReleaseDate` 속성의 형식을 명시적으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-108">For example, the [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute in the following code explicitly specifies the formatting for the `ReleaseDate` property.</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample1.cs)]

<span data-ttu-id="1bbe9-109">다음 예에서는 `Date` 열거를 사용 하는 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 특성은 날짜 템플릿을 사용 하 여 모델을 렌더링 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-109">In the following example, the [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attribute, using the `Date` enumeration, specifies that the date template should be used to render the model.</span></span> <span data-ttu-id="1bbe9-110">프로젝트에 날짜 템플릿이 없으면 기본 제공 날짜 템플릿이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-110">If there's no date template in your project, the built-in date template is used.</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample2.cs)]

<span data-ttu-id="1bbe9-111">그러나 ASP. MVC는 형식 이름과 일치 하는 템플릿을 찾아 구성 규칙을 사용 하 여 형식 일치를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-111">However, ASP.MVC can perform type matching using convention-over-configuration, by looking for a template that matches the name of a type.</span></span> <span data-ttu-id="1bbe9-112">이렇게 하면 모든 특성 또는 코드를 사용 하지 않고 데이터를 자동으로 서식 지정 하는 템플릿을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-112">This lets you create a template that automatically formats data without using any attributes or code at all.</span></span> <span data-ttu-id="1bbe9-113">자습서의이 부분에서는 [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)형식의 모델 속성에 자동으로 적용 되는 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-113">For this part of the tutorial, you'll create a template that's automatically applied to model properties of type [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx).</span></span> <span data-ttu-id="1bbe9-114">[DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)형식의 모든 모델 속성을 렌더링 하는 데 템플릿을 사용 하도록 지정 하기 위해 특성 또는 기타 구성을 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-114">You won't need to use an attribute or other configuration to specify that the template should be used to render all model properties of type [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx).</span></span>

<span data-ttu-id="1bbe9-115">개별 속성 또는 개별 필드의 표시를 사용자 지정 하는 방법에 대해서도 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-115">You'll also learn a way to customize the display of individual properties or even individual fields.</span></span>

<span data-ttu-id="1bbe9-116">시작 하려면 기존 서식 지정 정보를 제거 하 고 응용 프로그램에 전체 날짜를 표시 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-116">To begin, let's remove existing formatting information and display full dates in the application.</span></span>

<span data-ttu-id="1bbe9-117">*Movie.cs* 파일을 열고 `ReleaseDate` 속성의 `DataType` 특성을 주석으로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-117">Open the *Movie.cs* file and comment out the `DataType` attribute on the `ReleaseDate` property:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample3.cs)]

<span data-ttu-id="1bbe9-118">Ctrl+F5를 눌러 애플리케이션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-118">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="1bbe9-119">서식 정보가 제공 되지 않을 때의 기본값 이기 때문에 `ReleaseDate` 속성이 이제 날짜와 시간을 모두 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-119">Notice that the `ReleaseDate` property now displays both the date and time, because that's the default when no formatting information is provided.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image1.png)

### <a name="adding-css-styles-for-testing-new-templates"></a><span data-ttu-id="1bbe9-120">새 템플릿 테스트를 위한 CSS 스타일 추가</span><span class="sxs-lookup"><span data-stu-id="1bbe9-120">Adding CSS Styles for Testing New Templates</span></span>

<span data-ttu-id="1bbe9-121">날짜 서식 지정을 위한 템플릿을 만들기 전에 새 템플릿에 적용할 수 있는 몇 가지 CSS 스타일 규칙을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-121">Before you create a template for formatting dates, you'll add a few CSS style rules that you can apply to the new templates.</span></span> <span data-ttu-id="1bbe9-122">렌더링 된 페이지가 새 템플릿을 사용 하 고 있는지 확인 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-122">These will help you verify that the rendered page is using the new template.</span></span>

<span data-ttu-id="1bbe9-123">*Content\site.cs*파일을 열고 파일의 아래쪽에 다음 CSS 규칙을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-123">Open the *Content\Site.cs*s file and add the following CSS rules to the bottom of the file:</span></span>

[!code-css[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample4.css)]

### <a name="adding-datetime-display-templates"></a><span data-ttu-id="1bbe9-124">DateTime 표시 템플릿 추가</span><span class="sxs-lookup"><span data-stu-id="1bbe9-124">Adding DateTime Display Templates</span></span>

<span data-ttu-id="1bbe9-125">이제 새 템플릿을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-125">Now you can create the new template.</span></span> <span data-ttu-id="1bbe9-126">*Views\Movies* 폴더에서 *displaytemplates* 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-126">In the *Views\Movies* folder, create a *DisplayTemplates* folder.</span></span>

<span data-ttu-id="1bbe9-127">*Views\Shared* 폴더에서 *displaytemplates* 폴더와 *editortemplates* 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-127">In the *Views\Shared* folder, create a *DisplayTemplates* folder and an *EditorTemplates* folder.</span></span>

<span data-ttu-id="1bbe9-128">*Views\Shared\DisplayTemplates* 폴더의 표시 템플릿은 모든 컨트롤러에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-128">The display templates in the *Views\Shared\DisplayTemplates* folder will be used by all controllers.</span></span> <span data-ttu-id="1bbe9-129">*Views\Movie\DisplayTemplates* 폴더의 표시 템플릿은 `Movie` 컨트롤러 에서만 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-129">The display templates in the *Views\Movie\DisplayTemplates* folder will be used only by the `Movie` controller.</span></span> <span data-ttu-id="1bbe9-130">(이름이 같은 템플릿이 두 폴더에 모두 표시 되는 경우 *Views\Movie\DisplayTemplates* 폴더의 템플릿 즉, 보다 구체적인 템플릿)이 `Movie` 컨트롤러에서 반환 된 보기에 우선 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-130">(If a template with the same name appears in both folders, the template in the *Views\Movie\DisplayTemplates* folder — that is, the more specific template — takes precedence for views returned by the `Movie` controller.)</span></span>

<span data-ttu-id="1bbe9-131">**솔루션 탐색기**에서 *Views* 폴더를 확장 하 고 *공유* 폴더를 확장 한 다음 *Views\Shared\DisplayTemplates* 폴더를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-131">In **Solution Explorer**, expand the *Views* folder, expand the *Shared* folder, and then right-click the *Views\Shared\DisplayTemplates* folder.</span></span>

<span data-ttu-id="1bbe9-132">**추가** 를 클릭 한 다음 **보기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-132">Click **Add** and then click **View**.</span></span> <span data-ttu-id="1bbe9-133">**보기 추가** 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-133">The **Add View** dialog box is displayed.</span></span>

<span data-ttu-id="1bbe9-134">**보기 이름** 상자에 `DateTime`을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-134">In the **View name** box, type `DateTime`.</span></span> <span data-ttu-id="1bbe9-135">(형식의 이름과 일치 시키려면이 이름을 사용 해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="1bbe9-135">(You must use this name in order to match the name of the type.)</span></span>

<span data-ttu-id="1bbe9-136">**부분 뷰로 만들기** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-136">Select the **Create as a partial view** check box.</span></span> <span data-ttu-id="1bbe9-137">**레이아웃 또는 마스터 페이지를 사용** 하 고 **강력한 형식의 뷰 만들기** 확인란을 선택 하지 않았는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-137">Make sure that the **Use a layout or master page** and **Create a strongly-typed view** check boxes are not selected.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image2.png)

<span data-ttu-id="1bbe9-138">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-138">Click **Add**.</span></span> <span data-ttu-id="1bbe9-139">*Views\Shared\DisplayTemplates*에서 *날짜/시간 cshtml* 템플릿이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-139">A *DateTime.cshtml* template is created in the *Views\Shared\DisplayTemplates*.</span></span>

<span data-ttu-id="1bbe9-140">다음 이미지는 `DateTime` 디스플레이 및 편집기 템플릿을 만든 후 **솔루션 탐색기** 의 *Views* 폴더를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-140">The following image shows the *Views* folder in **Solution Explorer** after the `DateTime` display and editor templates are created.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image3.png)

<span data-ttu-id="1bbe9-141">*Views\Shared\DisplayTemplates\DateTime.cshtml* 파일을 열고 다음 태그를 추가 합니다 .이 태그는 [system.string](https://msdn.microsoft.com/library/system.string.format.aspx) 메서드를 사용 하 여 속성을 시간 없이 날짜로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-141">Open the *Views\Shared\DisplayTemplates\DateTime.cshtml* file and add the following markup, which uses the [String.Format](https://msdn.microsoft.com/library/system.string.format.aspx) method to format the property as a date without the time.</span></span> <span data-ttu-id="1bbe9-142">`{0:d}` 형식은 간단한 날짜 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-142">(The `{0:d}` format specifies short date format.)</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample5.cs)]

<span data-ttu-id="1bbe9-143">*Views\Movie\DisplayTemplates* 폴더에 `DateTime` 템플릿을 만들려면이 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-143">Repeat this step to create a `DateTime` template in the *Views\Movie\DisplayTemplates* folder.</span></span> <span data-ttu-id="1bbe9-144">*Views\Movie\DisplayTemplates\DateTime.cshtml* 파일에서 다음 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-144">Use the following code in the *Views\Movie\DisplayTemplates\DateTime.cshtml* file.</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample6.cs)]

<span data-ttu-id="1bbe9-145">`loud-1` CSS 클래스를 통해 날짜가 굵은 빨간색 텍스트로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-145">The `loud-1` CSS class causes the date to be display in bold red text.</span></span> <span data-ttu-id="1bbe9-146">이 특정 템플릿이 사용 되는 시기를 쉽게 확인할 수 있도록 임시 측정값과 마찬가지로 `loud-1` CSS 클래스를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-146">You added the `loud-1` CSS class just as a temporary measure so you can easily see when this particular template is being used.</span></span>

<span data-ttu-id="1bbe9-147">수행한 작업은 ASP.NET에서 날짜를 표시 하는 데 사용 하는 사용자 지정 된 템플릿을 만들고 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-147">What you've done is created and customized templates that ASP.NET will use to display dates.</span></span> <span data-ttu-id="1bbe9-148">*Views\Shared\DisplayTemplates* 폴더에 있는 보다 일반적인 템플릿은 간단한 간단한 날짜를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-148">The more general template (in the *Views\Shared\DisplayTemplates* folder) displays a simple short date.</span></span> <span data-ttu-id="1bbe9-149">*Views\Movies\DisplayTemplates* 폴더에 있는 `Movie` 컨트롤러에 대해 특별히 지정 된 템플릿에는 굵은 빨간색 텍스트로 서식이 지정 된 간단한 날짜도 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-149">The template that's specifically for the `Movie` controller (in the *Views\Movies\DisplayTemplates* folder) displays a short date that's also formatted as bold red text.</span></span>

<span data-ttu-id="1bbe9-150">Ctrl+F5를 눌러 애플리케이션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-150">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="1bbe9-151">브라우저는 응용 프로그램의 인덱스 뷰를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-151">The browser renders the Index view for the application.</span></span>

<span data-ttu-id="1bbe9-152">이제 `ReleaseDate` 속성은 날짜를 시간 없이 굵은 빨간색 글꼴로 표시 합니다. 이를 통해 *Views\Movies\DisplayTemplates* 폴더의 `DateTime` 템플릿 기반 도우미가 공유 폴더의 `DateTime` 템플릿 도우미 (*Views\Shared\DisplayTemplates*)에 대해 선택 되어 있는지 확인 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-152">The `ReleaseDate` property now displays the date in a bold red font without the time.This helps you confirm that the `DateTime` templated helper in the *Views\Movies\DisplayTemplates* folder is selected over the `DateTime` templated helper in the shared folder (*Views\Shared\DisplayTemplates*).</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image4.png)

<span data-ttu-id="1bbe9-153">이제 *Views\Movies\DisplayTemplates\DateTime.cshtml* 파일의 이름을 *Views\Movies\DisplayTemplates\LoudDateTime.cshtml*로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-153">Now rename the *Views\Movies\DisplayTemplates\DateTime.cshtml* file to *Views\Movies\DisplayTemplates\LoudDateTime.cshtml*.</span></span>

<span data-ttu-id="1bbe9-154">Ctrl+F5를 눌러 애플리케이션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-154">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="1bbe9-155">이번에는 `ReleaseDate` 속성에 시간이 없고 굵은 빨강 글꼴이 없는 날짜가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-155">This time the `ReleaseDate` property displays a date without the time and without the bold red font.</span></span> <span data-ttu-id="1bbe9-156">이는 해당 형식의 모든 모델 속성을 표시 하는 데 데이터 형식 (이 경우 `DateTime`)의 이름을 가진 템플릿이 자동으로 사용 됨을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-156">This illustrates that a template that has the name of the data type (in this case `DateTime`) is automatically used to display all model properties of that type.</span></span> <span data-ttu-id="1bbe9-157">*LoudDateTime* *파일의* 이름을 ASP.NET로 바꾼 후에는 *Views\Movies\DisplayTemplates* 폴더에서 더 이상 템플릿을 찾을 수 없으므로 \* Views\Movies\Shared\* 폴더의 *템플릿을 사용 했습니다.*</span><span class="sxs-lookup"><span data-stu-id="1bbe9-157">After you renamed the *DateTime.cshtml* file to *LoudDateTime.cshtml*, ASP.NET no longer found a template in the *Views\Movies\DisplayTemplates* folder, so it used the *DateTime.cshtml* template from the \*Views\Movies\Shared\* folder.</span></span>

<span data-ttu-id="1bbe9-158">템플릿 일치는 대/소문자를 구분 하지 않으므로 모든 대/소문자를 사용 하 여 템플릿 파일 이름을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-158">(The template matching is case insensitive, so you could have created the template file name with any casing.</span></span> <span data-ttu-id="1bbe9-159">예를 들어, 날짜/시간, *날짜*/ *시간 및 날짜/시간 cshtml* 는 모두 `DateTime` 유형과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-159">For example, *DATETIME.cshtml, datetime.cshtml*, and *DaTeTiMe.cshtml* would all match the `DateTime` type.)</span></span>

<span data-ttu-id="1bbe9-160">검토 하려면이 시점에서 `ReleaseDate` 필드는 간단한 날짜 형식을 사용 하 여 데이터를 표시 하는 *Views\Movies\DisplayTemplates\DateTime.cshtml* 템플릿을 사용 하 여 표시 되지만 그렇지 않은 경우에는 특별 한 형식을 추가 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-160">To review: at this point, the `ReleaseDate` field is being displayed using the *Views\Movies\DisplayTemplates\DateTime.cshtml* template, which displays the data using a short date format, but otherwise adds no special format.</span></span>

### <a name="using-uihint-to-specify-a-display-template"></a><span data-ttu-id="1bbe9-161">UIHint를 사용 하 여 표시 템플릿 지정</span><span class="sxs-lookup"><span data-stu-id="1bbe9-161">Using UIHint to Specify a Display Template</span></span>

<span data-ttu-id="1bbe9-162">웹 응용 프로그램에 많은 `DateTime` 필드가 있고 기본적으로이 필드의 대부분 또는 대부분을 날짜 전용 형식으로 표시 하려는 경우에는 *DateTime* 을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-162">If your web application has many `DateTime` fields and by default you want to display all or most of them in date-only format, the *DateTime.cshtml* template is a good approach.</span></span> <span data-ttu-id="1bbe9-163">그러나 전체 날짜와 시간을 표시 하는 데 몇 가지 날짜가 있으면 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="1bbe9-163">But what if you have a few dates where you want to display the full date and time?</span></span> <span data-ttu-id="1bbe9-164">걱정하실 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-164">No problem.</span></span> <span data-ttu-id="1bbe9-165">추가 템플릿을 만들고 [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) 특성을 사용 하 여 전체 날짜 및 시간에 대 한 서식을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-165">You can create an additional template and use the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute to specify formatting for the full date and time.</span></span> <span data-ttu-id="1bbe9-166">그런 다음 해당 템플릿을 선택적으로 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-166">You can then selectively apply that template.</span></span> <span data-ttu-id="1bbe9-167">모델 수준에서 [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) 특성을 사용 하거나 뷰 내에서 템플릿을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-167">You can use the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute at the model level or you can specify the template inside a view.</span></span> <span data-ttu-id="1bbe9-168">이 섹션에서는 `UIHint` 특성을 사용 하 여 날짜-시간 필드의 일부 인스턴스에 대 한 서식을 선택적으로 변경 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-168">In this section, you'll see how to use the `UIHint` attribute to selectively change the formatting for some instances of date-time fields.</span></span>

<span data-ttu-id="1bbe9-169">*Views\Movies\DisplayTemplates\LoudDateTime.cshtml* 파일을 열고 기존 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-169">Open the *Views\Movies\DisplayTemplates\LoudDateTime.cshtml* file and replace the existing code with the following:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample7.cshtml)]

<span data-ttu-id="1bbe9-170">이렇게 하면 전체 날짜와 시간이 표시 되 고 텍스트를 녹색 및 크게 만드는 CSS 클래스가 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-170">This causes the full date and time to be displayed and adds the CSS class that makes the text green and large.</span></span>

<span data-ttu-id="1bbe9-171">다음 예제와 같이 *Movie.cs* 파일을 열고 [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) 특성을 `ReleaseDate` 속성에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-171">Open the *Movie.cs* file and add the [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) attribute to the `ReleaseDate` property, as shown in the following example:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample8.cs)]

<span data-ttu-id="1bbe9-172">이렇게 하면 ASP.NET MVC에 `ReleaseDate` 속성이 표시 될 때 (`DateTime` 개체 뿐만 아니라) *LoudDateTime* 템플릿을 사용 해야 한다는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-172">This tells ASP.NET MVC that when it displays the `ReleaseDate` property (specifically, and not just any `DateTime` object), it should use the *LoudDateTime.cshtml* template.</span></span>

<span data-ttu-id="1bbe9-173">Ctrl+F5를 눌러 애플리케이션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-173">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="1bbe9-174">이제 `ReleaseDate` 속성은 날짜와 시간을 긴 녹색 글꼴로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-174">Notice that the `ReleaseDate` property now displays the date and time in a large green font.</span></span>

<span data-ttu-id="1bbe9-175">*Movie.cs* 파일의 `UIHint` 특성으로 돌아가서 *LoudDateTime* 템플릿을 사용 하지 않도록 주석 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-175">Return to the `UIHint` attribute in the *Movie.cs* file and comment it out so the *LoudDateTime.cshtml* template won't be used.</span></span> <span data-ttu-id="1bbe9-176">애플리케이션을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-176">Run the application again.</span></span> <span data-ttu-id="1bbe9-177">릴리스 날짜는 크고 녹색으로 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-177">The release date is not displayed large and green.</span></span> <span data-ttu-id="1bbe9-178">이렇게 하면 *Views\Shared\DisplayTemplates\DateTime.cshtml* 템플릿이 인덱스 및 세부 정보 뷰에서 사용 되는지 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-178">This verifies that the *Views\Shared\DisplayTemplates\DateTime.cshtml* template is used in the Index and Details views.</span></span>

<span data-ttu-id="1bbe9-179">앞에서 설명한 것 처럼 보기에서 템플릿을 적용 하면 특정 데이터의 개별 인스턴스에 템플릿을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-179">As mentioned earlier, you can also apply a template in a view, which lets you apply the template to an individual instance of some data.</span></span> <span data-ttu-id="1bbe9-180">*Views\Movies\Details.cshtml* 뷰를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-180">Open the *Views\Movies\Details.cshtml* view.</span></span> <span data-ttu-id="1bbe9-181">`ReleaseDate` 필드에 대 한 호출 [에 대](https://msdn.microsoft.com/library/ee407420.aspx) 한 두 번째 매개 변수로 `"LoudDateTime"`를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-181">Add `"LoudDateTime"` as the second parameter of the [Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) call for the `ReleaseDate` field.</span></span> <span data-ttu-id="1bbe9-182">완성된 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-182">The completed code looks like this:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample9.cshtml)]

<span data-ttu-id="1bbe9-183">이는 모델에 적용 되는 특성에 관계 없이 모델 속성을 표시 하는 데 `LoudDateTime` 템플릿을 사용 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-183">This specifies that the `LoudDateTime` template should be used to display the model property, regardless of what attributes are applied to the model.</span></span>

<span data-ttu-id="1bbe9-184">Ctrl+F5를 눌러 애플리케이션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-184">Press CTRL+F5 to run the application.</span></span>

<span data-ttu-id="1bbe9-185">동영상 인덱스 페이지가 *Views\Shared\DisplayTemplates\DateTime.cshtml* 템플릿 (빨강 굵게)을 사용 하 고 *Movie\Details* 페이지에서 *Views\Movies\DisplayTemplates\LoudDateTime.cshtml* 템플릿 (크거나 녹색)을 사용 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-185">Verify that the movie index page is using the *Views\Shared\DisplayTemplates\DateTime.cshtml* template (red bold) and the *Movie\Details* page is using the *Views\Movies\DisplayTemplates\LoudDateTime.cshtml* template (large and green).</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image5.png)

<span data-ttu-id="1bbe9-186">다음 섹션에서는 복합 형식에 대 한 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1bbe9-186">In the next section, you'll create a template for a complex type.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1bbe9-187">[이전](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1.md)
> [다음](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="1bbe9-187">[Previous](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1.md)
[Next](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)</span></span>
