---
uid: mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
title: 마스터 페이지 및 부분를 사용 하 여 UI 다시 사용 | Microsoft Docs
author: microsoft
description: 7 단계에서는 부분 보기 템플릿 및 마스터 페이지를 사용 하 여 코드 중복을 제거 하기 위해 보기 템플릿 내에서 ' 마른 원칙 '을 적용할 수 있는 방법을 살펴봅니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: d4243a4a-e91c-4116-9ae0-5c08e5285677
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
msc.type: authoredcontent
ms.openlocfilehash: 0b17cb6ac14b7f187bf1f175097a37907689d46e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468725"
---
# <a name="re-use-ui-using-master-pages-and-partials"></a><span data-ttu-id="7e83b-103">마스터 페이지 및 부분을 사용하여 UI 재사용</span><span class="sxs-lookup"><span data-stu-id="7e83b-103">Re-use UI Using Master Pages and Partials</span></span>

<span data-ttu-id="7e83b-104">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="7e83b-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="7e83b-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="7e83b-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="7e83b-106">ASP.NET MVC 1을 사용 하 여 작고 완전 한 웹 응용 프로그램을 빌드하는 방법을 안내 하는 무료 ["Nerddinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 의 7 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-106">This is step 7 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="7e83b-107">7 단계에서는 부분 보기 템플릿 및 마스터 페이지를 사용 하 여 코드 중복을 제거 하기 위해 보기 템플릿 내에서 "건조 원칙"을 적용할 수 있는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-107">Step 7 looks at ways we can apply the "DRY Principle" within our view templates to eliminate code duplication, using partial view templates and master pages.</span></span>
> 
> <span data-ttu-id="7e83b-108">ASP.NET MVC 3을 사용 하는 경우 [mvc 3 시작](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [mvc Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-7-partials-and-master-pages"></a><span data-ttu-id="7e83b-109">NerdDinner Step 7: 부분 및 마스터 페이지</span><span class="sxs-lookup"><span data-stu-id="7e83b-109">NerdDinner Step 7: Partials and Master Pages</span></span>

<span data-ttu-id="7e83b-110">ASP.NET MVC의 디자인 철학 중 하나는 "직접 반복 안 함" 원칙 (일반적으로 "원음" 이라고 함)입니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-110">One of the design philosophies ASP.NET MVC embraces is the "Do Not Repeat Yourself" principle (commonly referred to as "DRY").</span></span> <span data-ttu-id="7e83b-111">마른 디자인은 코드 및 논리의 중복을 제거 하 여 궁극적으로 응용 프로그램을 더 빠르게 빌드하고 유지 관리할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-111">A DRY design helps eliminate the duplication of code and logic, which ultimately makes applications faster to build and easier to maintain.</span></span>

<span data-ttu-id="7e83b-112">몇 가지 부분으로 이루어진 Ddinner 시나리오에 적용 된 마른 원칙이 이미 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-112">We've already seen the DRY principle applied in several of our NerdDinner scenarios.</span></span> <span data-ttu-id="7e83b-113">몇 가지 예: 유효성 검사 논리는 모델 계층 내에서 구현 되므로 컨트롤러의 편집 및 만들기 시나리오 모두에서 적용 될 수 있습니다. 편집, 세부 정보 및 삭제 동작 메서드에서 "NotFound" 뷰 템플릿을 다시 사용 하 고 있습니다. 뷰 () 도우미 메서드를 호출할 때 이름을 명시적으로 지정할 필요가 없도록 하는 뷰 템플릿에서 규칙 명명 패턴을 사용 합니다. 그리고 편집 및 만들기 작업 시나리오 모두에 대해 d Innerformviewmodel 클래스를 다시 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-113">A few examples: our validation logic is implemented within our model layer, which enables it to be enforced across both edit and create scenarios in our controller; we are re-using the "NotFound" view template across the Edit, Details and Delete action methods; we are using a convention- naming pattern with our view templates, which eliminates the need to explicitly specify the name when we call the View() helper method; and we are re-using the DinnerFormViewModel class for both Edit and Create action scenarios.</span></span>

<span data-ttu-id="7e83b-114">이제 보기 템플릿 내에서 "마른 원칙"을 적용 하 여 코드 중복을 제거할 수 있는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-114">Let's now look at ways we can apply the "DRY Principle" within our view templates to eliminate code duplication there as well.</span></span>

### <a name="re-visiting-our-edit-and-create-view-templates"></a><span data-ttu-id="7e83b-115">편집 및 만들기 보기 템플릿 다시 방문</span><span class="sxs-lookup"><span data-stu-id="7e83b-115">Re-visiting our Edit and Create View Templates</span></span>

<span data-ttu-id="7e83b-116">현재는 두 가지 보기 템플릿 "Edit .aspx" 및 ".aspx 만들기"를 사용 하 여 Dinner form UI를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-116">Currently we are using two different view templates – "Edit.aspx" and "Create.aspx" – to display our Dinner form UI.</span></span> <span data-ttu-id="7e83b-117">시각적 개체를 시각적으로 비교 하면 어떻게 유사한 지 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-117">A quick visual comparison of them highlights how similar they are.</span></span> <span data-ttu-id="7e83b-118">생성 형태는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-118">Below is what the create form looks like:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image1.png)

<span data-ttu-id="7e83b-119">"편집" 형태는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-119">And here is what our "Edit" form looks like:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image2.png)

<span data-ttu-id="7e83b-120">차이가 많지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-120">Not much of a difference is there?</span></span> <span data-ttu-id="7e83b-121">제목 및 머리글 텍스트 외에도 양식 레이아웃과 입력 컨트롤은 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-121">Other than the title and header text, the form layout and input controls are identical.</span></span>

<span data-ttu-id="7e83b-122">"Edit .aspx" 및 ".aspx 만들기" 보기 템플릿을 열면 동일한 양식 레이아웃 및 입력 제어 코드가 포함 된 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-122">If we open up the "Edit.aspx" and "Create.aspx" view templates we'll find that they contain identical form layout and input control code.</span></span> <span data-ttu-id="7e83b-123">이 중복은 새 Dinner property를 도입 하거나 변경할 때 언제 든 지 변경 내용을 두 번 수행 하는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-123">This duplication means we end up having to make changes twice anytime we introduce or change a new Dinner property - which is not good.</span></span>

### <a name="using-partial-view-templates"></a><span data-ttu-id="7e83b-124">부분 뷰 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="7e83b-124">Using Partial View Templates</span></span>

<span data-ttu-id="7e83b-125">ASP.NET MVC는 페이지의 하위 부분에 대 한 뷰 렌더링 논리를 캡슐화 하는 데 사용할 수 있는 "부분 뷰" 템플릿을 정의 하는 기능을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-125">ASP.NET MVC supports the ability to define "partial view" templates that can be used to encapsulate view rendering logic for a sub-portion of a page.</span></span> <span data-ttu-id="7e83b-126">"부분"는 뷰 렌더링 논리를 한 번 정의한 다음 응용 프로그램의 여러 위치에서 다시 사용 하는 유용한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-126">"Partials" provide a useful way to define view rendering logic once, and then re-use it in multiple places across an application.</span></span>

<span data-ttu-id="7e83b-127">편집 .aspx의 "건조" 및 .aspx 보기 템플릿 복제를 지원 하기 위해 두 가지 모두에 공통 된 양식 레이아웃 및 입력 요소를 캡슐화 하는 "' d a t e. n a m e. n a m e" 이라는 부분 뷰 템플릿을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-127">To help "DRY-up" our Edit.aspx and Create.aspx view template duplication, we can create a partial view template named "DinnerForm.ascx" that encapsulates the form layout and input elements common to both.</span></span> <span data-ttu-id="7e83b-128">/Views/Dinners 디렉터리를 마우스 오른쪽 단추로 클릭 하 고 "추가&gt;뷰" 메뉴 명령을 선택 하 여이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-128">We'll do this by right-clicking on our /Views/Dinners directory and choosing the "Add-&gt;View" menu command:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image3.png)

<span data-ttu-id="7e83b-129">그러면 "보기 추가" 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-129">This will display the "Add View" dialog.</span></span> <span data-ttu-id="7e83b-130">"' D i n 폼"을 만들 새 뷰의 이름을 지정 하 고, 대화 상자 내에서 "부분 보기 만들기" 확인란을 선택 하 고,이를 d Innerformviewmodel 클래스로 전달 한다는 것을</span><span class="sxs-lookup"><span data-stu-id="7e83b-130">We'll name the new view we want to create "DinnerForm", select the "Create a partial view" checkbox within the dialog, and indicate that we will pass it a DinnerFormViewModel class:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image4.png)

<span data-ttu-id="7e83b-131">"추가" 단추를 클릭 하면 Visual Studio에서 "\Views\Dinners" 디렉터리 내에 새 "" 보기 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-131">When we click the "Add" button, Visual Studio will create a new "DinnerForm.ascx" view template for us within the "\Views\Dinners" directory.</span></span>

<span data-ttu-id="7e83b-132">그런 다음, Edit .aspx/Create .aspx 보기 템플릿에서 중복 양식 레이아웃/입력 컨트롤 코드를 복사 하 여 새 "' i n a m e. n a m e.</span><span class="sxs-lookup"><span data-stu-id="7e83b-132">We can then copy/paste the duplicate form layout / input control code from our Edit.aspx/ Create.aspx view templates into our new "DinnerForm.ascx" partial view template:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample1.aspx)]

<span data-ttu-id="7e83b-133">그런 다음, 편집 및 만들기 보기 템플릿을 업데이트 하 여이 템플릿 부분 템플릿을 호출 하 고, 형식 중복을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-133">We can then update our Edit and Create view templates to call the DinnerForm partial template and eliminate the form duplication.</span></span> <span data-ttu-id="7e83b-134">이 작업을 수행 하려면 보기 템플릿 내에서 Html RenderPartial ("DinnerForm")를 호출 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-134">We can do this by calling Html.RenderPartial("DinnerForm") within our view templates:</span></span>

##### <a name="createaspx"></a><span data-ttu-id="7e83b-135">.Aspx 만들기</span><span class="sxs-lookup"><span data-stu-id="7e83b-135">Create.aspx</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample2.aspx)]

##### <a name="editaspx"></a><span data-ttu-id="7e83b-136">Edit.aspx</span><span class="sxs-lookup"><span data-stu-id="7e83b-136">Edit.aspx</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample3.aspx)]

<span data-ttu-id="7e83b-137">Html RenderPartial을 호출할 때 원하는 부분 템플릿의 경로를 명시적으로 한정할 수 있습니다. 예를 들어 ~ Views/Dinners/DinnerForm.</span><span class="sxs-lookup"><span data-stu-id="7e83b-137">You can explicitly qualify the path of the partial template you want when calling Html.RenderPartial (for example: ~Views/Dinners/DinnerForm.ascx").</span></span> <span data-ttu-id="7e83b-138">위의 코드에서는 ASP.NET MVC 내에서 규칙 기반 명명 패턴을 활용 하 고, 렌더링할 부분 이름으로 ""을 지정 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-138">In our code above, though, we are taking advantage of the convention-based naming pattern within ASP.NET MVC, and just specifying "DinnerForm" as the name of the partial to render.</span></span> <span data-ttu-id="7e83b-139">이 작업을 수행 하면 ASP.NET MVC가 규칙 기반 뷰 디렉터리에서 먼저 표시 됩니다 (이는/Views/Dinners이 됨).</span><span class="sxs-lookup"><span data-stu-id="7e83b-139">When we do this ASP.NET MVC will look first in the convention-based views directory (for DinnersController this would be /Views/Dinners).</span></span> <span data-ttu-id="7e83b-140">부분 템플릿이 없으면/Views/Shared 디렉터리에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-140">If it doesn't find the partial template there it will then look for it in the /Views/Shared directory.</span></span>

<span data-ttu-id="7e83b-141">부분 뷰의 이름만 사용 하 여 Html RenderPartial ()를 호출 하면 ASP.NET MVC는 호출 하는 뷰 템플릿에서 사용 하는 동일한 모델 및 ViewData dictionary 개체를 부분 뷰로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-141">When Html.RenderPartial() is called with just the name of the partial view, ASP.NET MVC will pass to the partial view the same Model and ViewData dictionary objects used by the calling view template.</span></span> <span data-ttu-id="7e83b-142">또는 사용할 부분 뷰에 대해 대체 모델 개체 및/또는 ViewData 사전을 전달할 수 있도록 하는 Html RenderPartial ()의 오버 로드 된 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-142">Alternatively, there are overloaded versions of Html.RenderPartial() that enable you to pass an alternate Model object and/or ViewData dictionary for the partial view to use.</span></span> <span data-ttu-id="7e83b-143">이는 전체 모델/ViewModel의 하위 집합만 전달 하려는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-143">This is useful for scenarios where you only want to pass a subset of the full Model/ViewModel.</span></span>

| <span data-ttu-id="7e83b-144">**사이드 토픽: &lt;% =%&gt;대신%%&gt;을 (를) &lt;하는 이유는 무엇입니까?**</span><span class="sxs-lookup"><span data-stu-id="7e83b-144">**Side Topic: Why &lt;% %&gt; instead of &lt;%= %&gt;?**</span></span> |
| --- |
| <span data-ttu-id="7e83b-145">위의 코드에서 발견할 수 있는 사소한 작업 중 하나는 Html을 호출할 때 &lt;% =%&gt; 블록 대신 &lt;%%&gt; 블록을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-145">One of the subtle things you might have noticed with the code above is that we are using a &lt;% %&gt; block instead of a &lt;%= %&gt; block when calling Html.RenderPartial().</span></span> <span data-ttu-id="7e83b-146">ASP.NET 의% =%&gt; 블록 &lt;개발자가 지정 된 값 (예: &lt;% = "Hello"%&gt; "Hello"를 렌더링)을 렌더링 하려고 함을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-146">&lt;%= %&gt; blocks in ASP.NET indicate that a developer wants to render a specified value (for example: &lt;%= "Hello" %&gt; would render "Hello").</span></span> <span data-ttu-id="7e83b-147">대신 &lt;%%&gt; 블록은 개발자가 코드를 실행 하 고 있는 모든 렌더링 된 출력을 명시적으로 수행 해야 함을 표시 합니다 (예: &lt;% Response ("Hello")%&gt;).</span><span class="sxs-lookup"><span data-stu-id="7e83b-147">&lt;% %&gt; blocks instead indicate that the developer wants to execute code, and that any rendered output within them must be done explicitly (for example: &lt;% Response.Write("Hello") %&gt;.</span></span> <span data-ttu-id="7e83b-148">Html로 &lt;%%&gt; 블록을 사용 하는 이유는 Html. RenderPartial () 메서드가 문자열을 반환 하지 않고 대신 호출 하는 뷰 템플릿의 출력 스트림으로 콘텐츠를 직접 출력 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-148">The reason we are using a &lt;% %&gt; block with our Html.RenderPartial code above is because the Html.RenderPartial() method doesn't return a string, and instead outputs the content directly to the calling view template's output stream.</span></span> <span data-ttu-id="7e83b-149">성능 효율성을 위해이 작업을 수행 합니다. 이렇게 하면 (잠재적으로 매우 큰) 임시 문자열 개체를 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-149">It does this for performance efficiency reasons, and by doing so it avoids the need to create a (potentially very large) temporary string object.</span></span> <span data-ttu-id="7e83b-150">이렇게 하면 메모리 사용이 줄어들고 전반적인 응용 프로그램 처리량이 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-150">This reduces memory usage and improves overall application throughput.</span></span> <span data-ttu-id="7e83b-151">Html RenderPartial ()를 사용할 때 한 가지 일반적인 실수는 &lt;%%&gt; 블록 내에 있는 경우 호출 끝에 세미콜론을 추가 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-151">One common mistake when using Html.RenderPartial() is to forget to add a semi-colon at the end of the call when it is within a &lt;% %&gt; block.</span></span> <span data-ttu-id="7e83b-152">예를 들어 다음 코드는 컴파일러 오류를 발생 시킵니다. &lt;% Html RenderPartial ("' DinnerForm")%&gt;. 대신 &lt;% Html. RenderPartial ("DinnerForm");을 (를) 작성 해야 합니다. %&gt; &lt;%%&gt; 블록이 자체 포함 된 코드 문 이므로 코드 문을 사용 하 C# 는 경우 세미콜론으로 종료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-152">For example, this code will cause a compiler error: &lt;% Html.RenderPartial("DinnerForm") %&gt; You instead need to write: &lt;% Html.RenderPartial("DinnerForm"); %&gt; This is because &lt;% %&gt; blocks are self-contained code statements, and when using C# code statements need to be terminated with a semi-colon.</span></span> |

### <a name="using-partial-view-templates-to-clarify-code"></a><span data-ttu-id="7e83b-153">코드를 명확 하 게 나타내기 위해 부분 뷰 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="7e83b-153">Using Partial View Templates to Clarify Code</span></span>

<span data-ttu-id="7e83b-154">여러 위치에서 뷰 렌더링 논리가 중복 되는 것을 방지 하기 위해 "' d Innerform" 부분 뷰 템플릿을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-154">We created the "DinnerForm" partial view template to avoid duplicating view rendering logic in multiple places.</span></span> <span data-ttu-id="7e83b-155">이는 부분 뷰 템플릿을 만드는 가장 일반적인 이유입니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-155">This is the most common reason to create partial view templates.</span></span>

<span data-ttu-id="7e83b-156">경우에 따라 단일 위치로만 호출 되는 경우에도 부분 뷰를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-156">Sometimes it still makes sense to create partial views even when they are only being called in a single place.</span></span> <span data-ttu-id="7e83b-157">뷰 렌더링 논리를 추출 하 고 하나 이상의 잘 명명 된 부분 템플릿으로 분할 하는 경우 매우 복잡 한 뷰 템플릿을 더 쉽게 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-157">Very complicated view templates can often become much easier to read when their view rendering logic is extracted and partitioned into one or more well named partial templates.</span></span>

<span data-ttu-id="7e83b-158">예를 들어, 프로젝트의 site.master 파일 (곧 살펴볼 예정)에서 아래 코드 조각을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-158">For example, consider the below code-snippet from the Site.master file in our project (which we will be looking at shortly).</span></span> <span data-ttu-id="7e83b-159">화면 오른쪽 위에 로그인/로그 아웃 링크를 표시 하는 논리가 "LogOnUserControl" 부분 안에 캡슐화 되기 때문에 코드는 비교적 간단 하 게 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-159">The code is relatively straight-forward to read – partly because the logic to display a login/logout link at the top right of the screen is encapsulated within the "LogOnUserControl" partial:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample4.aspx)]

<span data-ttu-id="7e83b-160">보기 템플릿 내에서 html/code 태그를 이해 하는 것을 혼동 하는 경우, 그 중 일부를 추출 하 여 잘 명명 된 부분 뷰로 리팩터링할 때 명확 하지 않을 지 여부를 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-160">Whenever you find yourself getting confused trying to understand the html/code markup within a view-template, consider whether it wouldn't be clearer if some of it was extracted and refactored into well-named partial views.</span></span>

### <a name="master-pages"></a><span data-ttu-id="7e83b-161">마스터 페이지</span><span class="sxs-lookup"><span data-stu-id="7e83b-161">Master Pages</span></span>

<span data-ttu-id="7e83b-162">ASP.NET MVC는 부분 뷰를 지 원하는 것 외에도 사이트의 공통 레이아웃 및 최상위 html을 정의 하는 데 사용할 수 있는 "마스터 페이지" 템플릿을 만드는 기능을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-162">In addition to supporting partial views, ASP.NET MVC also supports the ability to create "master page" templates that can be used to define the common layout and top-level html of a site.</span></span> <span data-ttu-id="7e83b-163">그런 다음 콘텐츠 자리 표시자 컨트롤을 마스터 페이지에 추가 하 여 재정의할 수 있는 대체 가능 영역을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-163">Content placeholder controls can then be added to the master page to identify replaceable regions that can be overridden or "filled in" by views.</span></span> <span data-ttu-id="7e83b-164">이를 통해 응용 프로그램 전체에 공통적인 레이아웃을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-164">This provides a very effective (and DRY) way to apply a common layout across an application.</span></span>

<span data-ttu-id="7e83b-165">기본적으로 new ASP.NET MVC 프로젝트에는 마스터 페이지 템플릿이 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-165">By default, new ASP.NET MVC projects have a master page template automatically added to them.</span></span> <span data-ttu-id="7e83b-166">이 마스터 페이지의 이름은 "\Views\Shared\"이 고,이 폴더는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-166">This master page is named "Site.master" and lives within the \Views\Shared\ folder:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image5.png)

<span data-ttu-id="7e83b-167">기본 site.master 파일은 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-167">The default Site.master file looks like below.</span></span> <span data-ttu-id="7e83b-168">위쪽의 탐색 메뉴와 함께 사이트의 외부 html을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-168">It defines the outer html of the site, along with a menu for navigation at the top.</span></span> <span data-ttu-id="7e83b-169">여기에는 제목에 대 한 두 개의 대체 가능한 콘텐츠 자리 표시자 컨트롤과 페이지의 기본 콘텐츠가 교체 되어야 하는 위치에 대 한 다른 두 개의 콘텐츠 자리 표시자 컨트롤이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-169">It contains two replaceable content placeholder controls – one for the title, and the other for where the primary content of a page should be replaced:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample5.aspx)]

<span data-ttu-id="7e83b-170">팀 간 Ddinner 응용 프로그램에 대해 만든 모든 보기 템플릿 ("목록", "세부 정보", "편집", "만들기", "NotFound" 등)은이 사이트를 기반으로 합니다. 마스터 템플릿.</span><span class="sxs-lookup"><span data-stu-id="7e83b-170">All of the view templates we've created for our NerdDinner application ("List", "Details", "Edit", "Create", "NotFound", etc) have been based on this Site.master template.</span></span> <span data-ttu-id="7e83b-171">이는 "뷰 추가" 대화 상자를 사용 하 여 뷰를 만들 때 기본적으로 위쪽 &lt;% @ Page%&gt; 지시문에 추가 된 "MasterPageFile" 특성을 통해 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-171">This is indicated via the "MasterPageFile" attribute that was added by default to the top &lt;% @ Page %&gt; directive when we created our views using the "Add View" dialog:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample6.aspx)]

<span data-ttu-id="7e83b-172">즉, 사이트의 마스터 콘텐츠를 변경 하 고, 보기 템플릿을 렌더링할 때 변경 내용을 자동으로 적용 하 고 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-172">What this means is that we can change the Site.master content, and have the changes automatically be applied and used when we render any of our view templates.</span></span>

<span data-ttu-id="7e83b-173">응용 프로그램의 헤더가 "내 MVC 응용 프로그램"이 아닌 "NerdDinner"가 되도록 site.master의 헤더 섹션을 업데이트 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-173">Let's update our Site.master's header section so that the header of our application is "NerdDinner" instead of "My MVC Application".</span></span> <span data-ttu-id="7e83b-174">또한 탐색 메뉴를 업데이트 하 여 첫 번째 탭이 "Dinner a Dinner" (HomeController의 Index () 작업 메서드로 처리 됨)이 고, "Host a Dinner" 라는 새 탭을 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-174">Let's also update our navigation menu so that the first tab is "Find a Dinner" (handled by the HomeController's Index() action method), and let's add a new tab called "Host a Dinner" (handled by the DinnersController's Create() action method):</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample7.aspx)]

<span data-ttu-id="7e83b-175">Site.master 파일을 저장 하 고 브라우저를 새로 고치면 응용 프로그램 내의 모든 보기에 머리글 변경이 표시 되는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-175">When we save the Site.master file and refresh our browser we'll see our header changes show up across all views within our application.</span></span> <span data-ttu-id="7e83b-176">다음은 그 예입니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-176">For example:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image6.png)

<span data-ttu-id="7e83b-177">*/Dinners/Edit/[id]* URL:</span><span class="sxs-lookup"><span data-stu-id="7e83b-177">And with the */Dinners/Edit/[id]* URL:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image7.png)

### <a name="next-step"></a><span data-ttu-id="7e83b-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7e83b-178">Next Step</span></span>

<span data-ttu-id="7e83b-179">부분 및 마스터 페이지는 보기를 명확 하 게 구성할 수 있는 매우 유연한 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-179">Partials and master pages provide very flexible options that enable you to cleanly organize views.</span></span> <span data-ttu-id="7e83b-180">보기 내용/코드를 복제 하는 것을 방지 하 고 보기 템플릿을 쉽게 읽고 유지 관리 하는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-180">You'll find that they help you avoid duplicating view content/ code, and make your view templates easier to read and maintain.</span></span>

<span data-ttu-id="7e83b-181">이제 앞에서 빌드한 나열 시나리오를 다시 방문 하 고 확장 가능한 페이징 지원을 사용 하도록 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7e83b-181">Let's now revisit the listing scenario we built earlier and enable scalable paging support.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7e83b-182">[이전](use-viewdata-and-implement-viewmodel-classes.md)
> [다음](implement-efficient-data-paging.md)</span><span class="sxs-lookup"><span data-stu-id="7e83b-182">[Previous](use-viewdata-and-implement-viewmodel-classes.md)
[Next](implement-efficient-data-paging.md)</span></span>
