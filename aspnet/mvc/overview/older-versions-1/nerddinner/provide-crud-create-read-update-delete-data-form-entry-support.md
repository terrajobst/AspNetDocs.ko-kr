---
uid: mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
title: CRUD (만들기, 읽기, 업데이트, 삭제) 데이터 양식 항목 지원 |을 제공 합니다. Microsoft Docs
author: microsoft
description: 5 단계에서는 Dinners 편집, 만들기 및 삭제에 대 한 지원을 사용 하도록 설정 하 여 DinnersController 클래스를 추가로 수행 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: bbb976e5-6150-4283-a374-c22fbafe29f5
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
msc.type: authoredcontent
ms.openlocfilehash: b3123af9a1477bc496a0d229d628510fc202b6d2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468917"
---
# <a name="provide-crud-create-read-update-delete-data-form-entry-support"></a><span data-ttu-id="032ce-103">CRUD(만들기, 읽기, 업데이트, 삭제) 데이터 양식 항목 지원 제공</span><span class="sxs-lookup"><span data-stu-id="032ce-103">Provide CRUD (Create, Read, Update, Delete) Data Form Entry Support</span></span>

<span data-ttu-id="032ce-104">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="032ce-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="032ce-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="032ce-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="032ce-106">ASP.NET MVC 1을 사용 하 여 작고 완전 한 웹 응용 프로그램을 빌드하는 방법을 안내 하는 무료 ["Nerddinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 의 5 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-106">This is step 5 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="032ce-107">5 단계에서는 Dinners 편집, 만들기 및 삭제에 대 한 지원을 사용 하도록 설정 하 여 DinnersController 클래스를 추가로 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-107">Step 5 shows how to take our DinnersController class further by enable support for editing, creating and deleting Dinners with it as well.</span></span>
> 
> <span data-ttu-id="032ce-108">ASP.NET MVC 3을 사용 하는 경우 [mvc 3 시작](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [mvc Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-5-create-update-delete-form-scenarios"></a><span data-ttu-id="032ce-109">NerdDinner 5 단계: 양식 만들기, 업데이트, 삭제 시나리오</span><span class="sxs-lookup"><span data-stu-id="032ce-109">NerdDinner Step 5: Create, Update, Delete Form Scenarios</span></span>

<span data-ttu-id="032ce-110">컨트롤러 및 보기를 소개 하 고이를 사용 하 여 Dinners on 사이트에 대 한 목록/세부 정보 환경을 구현 하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-110">We've introduced controllers and views, and covered how to use them to implement a listing/details experience for Dinners on site.</span></span> <span data-ttu-id="032ce-111">다음 단계에서는 Dinners를 사용 하 여이 클래스를 추가 하 고 편집, 만들기 및 삭제를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-111">Our next step will be to take our DinnersController class further and enable support for editing, creating and deleting Dinners with it as well.</span></span>

### <a name="urls-handled-by-dinnerscontroller"></a><span data-ttu-id="032ce-112">DinnersController에서 처리 하는 Url</span><span class="sxs-lookup"><span data-stu-id="032ce-112">URLs handled by DinnersController</span></span>

<span data-ttu-id="032ce-113">이전에는 두 가지 Url ( */Dinners* 및 */Dinners/Details/[id])* 에 대 한 지원을 구현 하는 작업 메서드를 dinnerscontroller에 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-113">We previously added action methods to DinnersController that implemented support for two URLs: */Dinners* and */Dinners/Details/[id]*.</span></span>

| <span data-ttu-id="032ce-114">**URL**</span><span class="sxs-lookup"><span data-stu-id="032ce-114">**URL**</span></span> | <span data-ttu-id="032ce-115">**동사**</span><span class="sxs-lookup"><span data-stu-id="032ce-115">**VERB**</span></span> | <span data-ttu-id="032ce-116">**용도**</span><span class="sxs-lookup"><span data-stu-id="032ce-116">**Purpose**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="032ce-117">*/Dinners/*</span><span class="sxs-lookup"><span data-stu-id="032ce-117">*/Dinners/*</span></span> | <span data-ttu-id="032ce-118">GET</span><span class="sxs-lookup"><span data-stu-id="032ce-118">GET</span></span> | <span data-ttu-id="032ce-119">예정 된 dinners의 HTML 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-119">Display an HTML list of upcoming dinners.</span></span> |
| <span data-ttu-id="032ce-120">*/Dinners/Details/[id]*</span><span class="sxs-lookup"><span data-stu-id="032ce-120">*/Dinners/Details/[id]*</span></span> | <span data-ttu-id="032ce-121">GET</span><span class="sxs-lookup"><span data-stu-id="032ce-121">GET</span></span> | <span data-ttu-id="032ce-122">특정 dinner a에 대 한 세부 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-122">Display details about a specific dinner.</span></span> |

<span data-ttu-id="032ce-123">이제 */Dinners/Edit/[id]* , */Dinners/Create*및 */Dinners/Delete/[id]* 의 세 가지 추가 url을 구현 하는 작업 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-123">We will now add action methods to implement three additional URLs: */Dinners/Edit/[id]*, */Dinners/Create*, and */Dinners/Delete/[id]*.</span></span> <span data-ttu-id="032ce-124">이러한 Url을 사용 하면 기존 Dinners 편집, 새 Dinners 만들기, Dinners 삭제를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-124">These URLs will enable support for editing existing Dinners, creating new Dinners, and deleting Dinners.</span></span>

<span data-ttu-id="032ce-125">이러한 새 Url을 사용 하 여 HTTP GET 및 HTTP POST 동사 상호 작용을 모두 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-125">We will support both HTTP GET and HTTP POST verb interactions with these new URLs.</span></span> <span data-ttu-id="032ce-126">이러한 Url에 대 한 HTTP GET 요청은 데이터의 초기 HTML 보기 ("편집"의 경우 Dinner data로 채워진 폼, "만들기"의 경우 빈 폼, "delete"의 경우 삭제 확인 화면)를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-126">HTTP GET requests to these URLs will display the initial HTML view of the data (a form populated with the Dinner data in the case of "edit", a blank form in the case of "create", and a delete confirmation screen in the case of "delete").</span></span> <span data-ttu-id="032ce-127">이러한 Url에 대 한 HTTP POST 요청은 microsoft의 데이터베이스에서 데이터를 저장/업데이트/삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-127">HTTP POST requests to these URLs will save/update/delete the Dinner data in our DinnerRepository (and from there to the database).</span></span>

| <span data-ttu-id="032ce-128">**URL**</span><span class="sxs-lookup"><span data-stu-id="032ce-128">**URL**</span></span> | <span data-ttu-id="032ce-129">**동사**</span><span class="sxs-lookup"><span data-stu-id="032ce-129">**VERB**</span></span> | <span data-ttu-id="032ce-130">**용도**</span><span class="sxs-lookup"><span data-stu-id="032ce-130">**Purpose**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="032ce-131">*/Dinners/Edit/[id]*</span><span class="sxs-lookup"><span data-stu-id="032ce-131">*/Dinners/Edit/[id]*</span></span> | <span data-ttu-id="032ce-132">GET</span><span class="sxs-lookup"><span data-stu-id="032ce-132">GET</span></span> | <span data-ttu-id="032ce-133">Dinner data로 채워진 편집 가능한 HTML 폼을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-133">Display an editable HTML form populated with Dinner data.</span></span> |
| <span data-ttu-id="032ce-134">POST</span><span class="sxs-lookup"><span data-stu-id="032ce-134">POST</span></span> | <span data-ttu-id="032ce-135">특정 Dinner a의 폼 변경 내용을 데이터베이스에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-135">Save the form changes for a particular Dinner to the database.</span></span> |
| <span data-ttu-id="032ce-136">*/Dinners/Create*</span><span class="sxs-lookup"><span data-stu-id="032ce-136">*/Dinners/Create*</span></span> | <span data-ttu-id="032ce-137">GET</span><span class="sxs-lookup"><span data-stu-id="032ce-137">GET</span></span> | <span data-ttu-id="032ce-138">사용자가 새 Dinners를 정의할 수 있도록 하는 빈 HTML 양식을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-138">Display an empty HTML form that allows users to define new Dinners.</span></span> |
| <span data-ttu-id="032ce-139">POST</span><span class="sxs-lookup"><span data-stu-id="032ce-139">POST</span></span> | <span data-ttu-id="032ce-140">새 Dinner를 만들고 데이터베이스에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-140">Create a new Dinner and save it in the database.</span></span> |
| <span data-ttu-id="032ce-141">*/Dinners/Delete/[id]*</span><span class="sxs-lookup"><span data-stu-id="032ce-141">*/Dinners/Delete/[id]*</span></span> | <span data-ttu-id="032ce-142">GET</span><span class="sxs-lookup"><span data-stu-id="032ce-142">GET</span></span> | <span data-ttu-id="032ce-143">삭제 확인 화면을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-143">Display delete confirmation screen.</span></span> |
| <span data-ttu-id="032ce-144">POST</span><span class="sxs-lookup"><span data-stu-id="032ce-144">POST</span></span> | <span data-ttu-id="032ce-145">데이터베이스에서 지정 된 dinner a를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-145">Deletes the specified dinner from the database.</span></span> |

### <a name="edit-support"></a><span data-ttu-id="032ce-146">지원 편집</span><span class="sxs-lookup"><span data-stu-id="032ce-146">Edit Support</span></span>

<span data-ttu-id="032ce-147">"편집" 시나리오를 구현 하는 것부터 시작 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-147">Let's begin by implementing the "edit" scenario.</span></span>

#### <a name="the-http-get-edit-action-method"></a><span data-ttu-id="032ce-148">HTTP-GET 편집 동작 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-148">The HTTP-GET Edit Action Method</span></span>

<span data-ttu-id="032ce-149">먼저 편집 작업 메서드의 HTTP "GET" 동작을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-149">We'll start by implementing the HTTP "GET" behavior of our edit action method.</span></span> <span data-ttu-id="032ce-150">이 메서드는 */Dinners/Edit/[id]* URL이 요청 될 때 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-150">This method will be invoked when the */Dinners/Edit/[id]* URL is requested.</span></span> <span data-ttu-id="032ce-151">구현은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-151">Our implementation will look like:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample1.cs)]

<span data-ttu-id="032ce-152">위의 코드에서는 d Innerrepository를 사용 하 여 Dinner object를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-152">The code above uses the DinnerRepository to retrieve a Dinner object.</span></span> <span data-ttu-id="032ce-153">그런 다음 Dinner object를 사용 하 여 뷰 템플릿을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-153">It then renders a View template using the Dinner object.</span></span> <span data-ttu-id="032ce-154">명시적으로 템플릿 이름을 *view ()* 도우미 메서드에 전달 하지 않았으므로 규칙 기반 기본 경로를 사용 하 여 뷰 템플릿을 확인 합니다./Views/Dinners/Edit.aspx.</span><span class="sxs-lookup"><span data-stu-id="032ce-154">Because we haven't explicitly passed a template name to the *View()* helper method, it will use the convention based default path to resolve the view template: /Views/Dinners/Edit.aspx.</span></span>

<span data-ttu-id="032ce-155">이제이 뷰 템플릿을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-155">Let's now create this view template.</span></span> <span data-ttu-id="032ce-156">편집 메서드를 마우스 오른쪽 단추로 클릭 하 고 "뷰 추가" 상황에 맞는 메뉴 명령을 선택 하 여이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-156">We will do this by right-clicking within the Edit method and selecting the "Add View" context menu command:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image1.png)

<span data-ttu-id="032ce-157">"뷰 추가" 대화 상자 내에서 Dinner object를 뷰 템플릿에 모델로 전달 하 고 "Edit" 템플릿을 자동으로 스 캐 폴드 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-157">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to our view template as its model, and choose to auto-scaffold an "Edit" template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image2.png)

<span data-ttu-id="032ce-158">"추가" 단추를 클릭 하면 Visual Studio는 "\Views\Dinners" 디렉터리 내에 새 ".aspx" 파일 보기 템플릿 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-158">When we click the "Add" button, Visual Studio will add a new "Edit.aspx" view template file for us within the "\Views\Dinners" directory.</span></span> <span data-ttu-id="032ce-159">또한 아래와 같이 초기 "Edit" 스 캐 폴드 구현으로 채워진 코드 편집기 내에서 새로운 "Edit .aspx" 보기 템플릿을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-159">It will also open up the new "Edit.aspx" view template within the code-editor – populated with an initial "Edit" scaffold implementation like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image3.png)

<span data-ttu-id="032ce-160">생성 된 기본 "edit" 스 캐 폴드를 몇 가지 변경 하 고 편집 뷰 템플릿을 업데이트 하 여 아래 콘텐츠를 포함 하도록 합니다 (노출 하지 않으려는 일부 속성을 제거 함).</span><span class="sxs-lookup"><span data-stu-id="032ce-160">Let's make a few changes to the default "edit" scaffold generated, and update the edit view template to have the content below (which removes a few of the properties we don't want to expose):</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample2.aspx)]

<span data-ttu-id="032ce-161">응용 프로그램을 실행 하 고 *"/Dinners/Edit/1"* URL을 요청 하면 다음 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-161">When we run the application and request the *"/Dinners/Edit/1"* URL we will see the following page:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image4.png)

<span data-ttu-id="032ce-162">뷰에서 생성 된 HTML 태그는 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-162">The HTML markup generated by our view looks like below.</span></span> <span data-ttu-id="032ce-163">표준 HTML 이며, "저장" &lt;입력 형식 = "제출"/&gt; 단추가 푸시되 면 */Dinners/Edit/1* URL에 HTTP POST를 수행 하는 &lt;form&gt; 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-163">It is standard HTML – with a &lt;form&gt; element that performs an HTTP POST to the */Dinners/Edit/1* URL when the "Save" &lt;input type="submit"/&gt; button is pushed.</span></span> <span data-ttu-id="032ce-164">HTML &lt;입력 형식 = "text"/&gt; 요소가 편집 가능한 각 속성에 대해 출력 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-164">A HTML &lt;input type="text"/&gt; element has been output for each editable property:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image5.png)

#### <a name="htmlbeginform-and-htmltextbox-html-helper-methods"></a><span data-ttu-id="032ce-165">Html.beginform () 및 Html. TextBox () Html 도우미 메서드</span><span class="sxs-lookup"><span data-stu-id="032ce-165">Html.BeginForm() and Html.TextBox() Html Helper Methods</span></span>

<span data-ttu-id="032ce-166">"ValidationSummary (), Html.beginform (), Html. 텍스트 상자 () 및 Html. ValidationMessage ()를 사용 하 여" .aspx 편집 "보기 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-166">Our "Edit.aspx" view template is using several "Html Helper" methods: Html.ValidationSummary(), Html.BeginForm(), Html.TextBox(), and Html.ValidationMessage().</span></span> <span data-ttu-id="032ce-167">이러한 도우미 메서드는 미국의 HTML 태그를 생성 하는 것 외에도 기본 제공 오류 처리 및 유효성 검사를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-167">In addition to generating HTML markup for us, these helper methods provide built-in error handling and validation support.</span></span>

##### <a name="htmlbeginform-helper-method"></a><span data-ttu-id="032ce-168">Html.beginform () 도우미 메서드</span><span class="sxs-lookup"><span data-stu-id="032ce-168">Html.BeginForm() helper method</span></span>

<span data-ttu-id="032ce-169">Html.beginform () 도우미 메서드는 태그에서 HTML &lt;form&gt; 요소를 출력 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-169">The Html.BeginForm() helper method is what output the HTML &lt;form&gt; element in our markup.</span></span> <span data-ttu-id="032ce-170">이 메서드를 사용 하는 경우 편집 .aspx 보기 템플릿에서 C# "using" 문을 적용 하 고 있음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-170">In our Edit.aspx view template you'll notice that we are applying a C# "using" statement when using this method.</span></span> <span data-ttu-id="032ce-171">여는 중괄호는 콘텐츠&gt; &lt;폼의 시작을 나타내고, 닫는 중괄호는 &lt;&gt; 요소의 끝을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-171">The open curly brace indicates the beginning of the &lt;form&gt; content, and the closing curly brace is what indicates the end of the &lt;/form&gt; element:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample3.cs)]

<span data-ttu-id="032ce-172">또는 이와 같은 시나리오에서 "using" 문을 사용 하지 않는 경우 동일한 작업을 수행 하는 Html.beginform () 및 .Html () 조합을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-172">Alternatively, if you find the "using" statement approach unnatural for a scenario like this, you can use a Html.BeginForm() and Html.EndForm() combination (which does the same thing):</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample4.aspx)]

<span data-ttu-id="032ce-173">매개 변수 없이 Html.beginform ()를 호출 하면이 메서드는 현재 요청의 URL에 대해 HTTP POST를 수행 하는 form 요소를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-173">Calling Html.BeginForm() without any parameters will cause it to output a form element that does an HTTP-POST to the current request's URL.</span></span> <span data-ttu-id="032ce-174">이렇게 하면 편집 뷰에서 *&lt;form action = "/Dinners/Edit/1" method = "post"&gt;* 요소가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-174">That is why our Edit view generates a *&lt;form action="/Dinners/Edit/1" method="post"&gt;* element.</span></span> <span data-ttu-id="032ce-175">다른 URL에 게시 하려는 경우 Html.beginform ()에 명시적 매개 변수를 전달할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-175">We could have alternatively passed explicit parameters to Html.BeginForm() if we wanted to post to a different URL.</span></span>

##### <a name="htmltextbox-helper-method"></a><span data-ttu-id="032ce-176">Html. TextBox () 도우미 메서드</span><span class="sxs-lookup"><span data-stu-id="032ce-176">Html.TextBox() helper method</span></span>

<span data-ttu-id="032ce-177">편집 .aspx 뷰에서는 Html. TextBox () 도우미 메서드를 사용 하 &lt;입력 형식 = "text"/&gt; 요소를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-177">Our Edit.aspx view uses the Html.TextBox() helper method to output &lt;input type="text"/&gt; elements:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample5.aspx)]

<span data-ttu-id="032ce-178">위의 Html. TextBox () 메서드는 단일 매개 변수를 사용 합니다 .이 매개 변수는 &lt;입력 형식 = "text"/&gt; 요소의 id/name 특성을 모두 지정 하 고 텍스트 상자 값을 채울 모델 속성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-178">The Html.TextBox() method above takes a single parameter – which is being used to specify both the id/name attributes of the &lt;input type="text"/&gt; element to output, as well as the model property to populate the textbox value from.</span></span> <span data-ttu-id="032ce-179">예를 들어 편집 뷰에 전달 된 Dinner object에는 "Title" 속성 값 ".NET 퓨처"가 있으며 Html. TextBox ("Title") 메서드 호출 출력: *&lt;입력 id = "title" name = "title" type = "text" value = ".Net 퓨처"/&gt;* .</span><span class="sxs-lookup"><span data-stu-id="032ce-179">For example, the Dinner object we passed to the Edit view had a "Title" property value of ".NET Futures", and so our Html.TextBox("Title") method call output: *&lt;input id="Title" name="Title" type="text" value=".NET Futures" /&gt;*.</span></span>

<span data-ttu-id="032ce-180">또는 첫 번째 Html. TextBox () 매개 변수를 사용 하 여 요소의 id/이름을 지정한 다음 두 번째 매개 변수로 사용할 값을 명시적으로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-180">Alternatively, we can use the first Html.TextBox() parameter to specify the id/name of the element, and then explicitly pass in the value to use as a second parameter:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample6.aspx)]

<span data-ttu-id="032ce-181">일반적으로 출력 되는 값에 대 한 사용자 지정 서식 지정을 수행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-181">Often we'll want to perform custom formatting on the value that is output.</span></span> <span data-ttu-id="032ce-182">String.format () 정적 메서드 기본 제공 .NET은 이러한 시나리오에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-182">The String.Format() static method built-into .NET is useful for these scenarios.</span></span> <span data-ttu-id="032ce-183">편집 .aspx 뷰 템플릿에서는이를 사용 하 여 시간에 대 한 초를 표시 하지 않도록 EventDate 값 (DateTime 형식)의 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-183">Our Edit.aspx view template is using this to format the EventDate value (which is of type DateTime) so that it doesn't show seconds for the time:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample7.aspx)]

<span data-ttu-id="032ce-184">Html. TextBox ()의 세 번째 매개 변수는 선택적으로 추가 HTML 특성을 출력 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-184">A third parameter to Html.TextBox() can optionally be used to output additional HTML attributes.</span></span> <span data-ttu-id="032ce-185">아래 코드 조각은 추가 크기 = "30" 특성과 class = "mycssclass" 특성을 &lt;입력 형식 = "text"/&gt; 요소에 렌더링 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-185">The code-snippet below demonstrates how to render an additional size="30" attribute and a class="mycssclass" attribute on the &lt;input type="text"/&gt; element.</span></span> <span data-ttu-id="032ce-186">"@" character because "클래스"를 사용 하 여 클래스 특성의 이름을 이스케이프 하는 방법은의 C#예약 된 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-186">Note how we are escaping the name of the class attribute using a "@" character because "class" is a reserved keyword in C#:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample8.aspx)]

#### <a name="implementing-the-http-post-edit-action-method"></a><span data-ttu-id="032ce-187">HTTP POST 편집 작업 메서드 구현</span><span class="sxs-lookup"><span data-stu-id="032ce-187">Implementing the HTTP-POST Edit Action Method</span></span>

<span data-ttu-id="032ce-188">이제 HTTP-GET 버전의 편집 작업 메서드가 구현 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-188">We now have the HTTP-GET version of our Edit action method implemented.</span></span> <span data-ttu-id="032ce-189">사용자가 */Dinners/Edit/1* URL을 요청 하면 다음과 같은 HTML 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-189">When a user requests the */Dinners/Edit/1* URL they receive an HTML page like the following:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image6.png)

<span data-ttu-id="032ce-190">"저장" 단추를 누르면 */Dinners/Edit/1* URL에 양식이 게시 되 고 HTTP post 동사를 사용 하 여 HTML &lt;입력&gt; 폼 값이 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-190">Pressing the "Save" button causes a form post to the */Dinners/Edit/1* URL, and submits the HTML &lt;input&gt; form values using the HTTP POST verb.</span></span> <span data-ttu-id="032ce-191">이제 Dinner를 저장 하는 작업을 처리 하는 edit 작업 메서드의 HTTP POST 동작을 구현 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-191">Let's now implement the HTTP POST behavior of our edit action method – which will handle saving the Dinner.</span></span>

<span data-ttu-id="032ce-192">먼저 오버 로드 된 "Edit" 작업 메서드를 ' AcceptVerbs ' 특성이 있는 "AcceptVerbs" 특성을 포함 하는이를 시작 합니다 .이 메서드는 HTTP POST 시나리오를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-192">We'll begin by adding an overloaded "Edit" action method to our DinnersController that has an "AcceptVerbs" attribute on it that indicates it handles HTTP POST scenarios:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample9.cs)]

<span data-ttu-id="032ce-193">[AcceptVerbs] 특성이 오버 로드 된 작업 메서드에 적용 되는 경우 ASP.NET MVC는 들어오는 HTTP 동사에 따라 적절 한 작업 메서드에 대 한 디스패치 요청을 자동으로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-193">When the [AcceptVerbs] attribute is applied to overloaded action methods, ASP.NET MVC automatically handles dispatching requests to the appropriate action method depending on the incoming HTTP verb.</span></span> <span data-ttu-id="032ce-194">*/Dinners/Edit/[id]* url에 대 한 http POST 요청은 위의 edit 메서드로 이동 하 고, */Dinners/Edit/[id]* url에 대 한 다른 모든 http 동사 요청은 구현 된 첫 번째 편집 메서드로 이동 합니다 (`[AcceptVerbs]` 특성이 없음).</span><span class="sxs-lookup"><span data-stu-id="032ce-194">HTTP POST requests to */Dinners/Edit/[id]* URLs will go to the above Edit method, while all other HTTP verb requests to */Dinners/Edit/[id]* URLs will go to the first Edit method we implemented (which did not have an `[AcceptVerbs]` attribute).</span></span>

| <span data-ttu-id="032ce-195">**측면 토픽: HTTP 동사를 통해 구분 하는 이유**</span><span class="sxs-lookup"><span data-stu-id="032ce-195">**Side Topic: Why differentiate via HTTP verbs?**</span></span> |
| --- |
| <span data-ttu-id="032ce-196">요청은 HTTP 동사를 통해 단일 URL을 사용 하 고 해당 동작을 차별화 하는 이유를 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-196">You might ask – why are we using a single URL and differentiating its behavior via the HTTP verb?</span></span> <span data-ttu-id="032ce-197">편집 변경 내용을 로드 하 고 저장 하는 두 개의 별도 Url을 포함 하지 않는 이유는 무엇 인가요?</span><span class="sxs-lookup"><span data-stu-id="032ce-197">Why not just have two separate URLs to handle loading and saving edit changes?</span></span> <span data-ttu-id="032ce-198">예:/Dinners/Edit/[id]를 표시 하 여 초기 양식과/Dinners/Save/[id]를 표시 하 여 저장 하려면 폼 게시를 처리 하 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="032ce-198">For example: /Dinners/Edit/[id] to display the initial form and /Dinners/Save/[id] to handle the form post to save it?</span></span> <span data-ttu-id="032ce-199">두 개의 개별 Url을 게시 하는 경우의 단점은/Dinners/Save/2에 게시 한 다음 입력 오류로 인해 HTML 양식을 다시 표시 해야 하는 경우 최종 사용자가 브라우저의 주소 표시줄에/Dinners/Save/2 URL을 포함 하는 것입니다 (폼이 게시 된 URL 이기 때문).</span><span class="sxs-lookup"><span data-stu-id="032ce-199">The downside with publishing two separate URLs is that in cases where we post to /Dinners/Save/2, and then need to redisplay the HTML form because of an input error, the end-user will end up having the /Dinners/Save/2 URL in their browser's address bar (since that was the URL the form posted to).</span></span> <span data-ttu-id="032ce-200">최종 사용자가이 다시 표시 페이지에 브라우저 즐겨찾기 목록에 책갈피를 추가 하거나 URL을 복사/붙여넣기 하 여 친구에 게 전자 메일을 보내면 해당 URL이 post 값에 의존 하기 때문에 나중에 작동 하지 않는 URL이 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-200">If the end-user bookmarks this redisplayed page to their browser favorites list, or copy/pastes the URL and emails it to a friend, they will end up saving a URL that won't work in the future (since that URL depends on post values).</span></span> <span data-ttu-id="032ce-201">단일 URL (예:/Dinners/Edit/[id])을 노출 하 고 HTTP 동사로 처리 하는 것을 구분 하 여 최종 사용자가 편집 페이지에 책갈피를 제공 하거나 URL을 다른 사용자에 게 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-201">By exposing a single URL (like: /Dinners/Edit/[id]) and differentiating the processing of it by HTTP verb, it is safe for end-users to bookmark the edit page and/or send the URL to others.</span></span> |

#### <a name="retrieving-form-post-values"></a><span data-ttu-id="032ce-202">폼 게시 값 검색</span><span class="sxs-lookup"><span data-stu-id="032ce-202">Retrieving Form Post Values</span></span>

<span data-ttu-id="032ce-203">HTTP POST "Edit" 메서드 내에서 게시 된 양식 매개 변수에 액세스할 수 있는 여러 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-203">There are a variety of ways we can access posted form parameters within our HTTP POST "Edit" method.</span></span> <span data-ttu-id="032ce-204">간단한 방법 중 하나는 컨트롤러 기본 클래스에서 Request 속성을 사용 하 여 양식 컬렉션에 액세스 하 고 게시 된 값을 직접 검색 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-204">One simple approach is to just use the Request property on the Controller base class to access the form collection and retrieve the posted values directly:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample10.cs)]

<span data-ttu-id="032ce-205">특히 오류 처리 논리를 추가한 후에는 위의 접근 방법이 약간 자세한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-205">The above approach is a little verbose, though, especially once we add error handling logic.</span></span>

<span data-ttu-id="032ce-206">이 시나리오에 대 한 더 나은 방법은 컨트롤러 기본 클래스에서 기본 제공 *UpdateModel ()* 도우미 메서드를 활용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-206">A better approach for this scenario is to leverage the built-in *UpdateModel()* helper method on the Controller base class.</span></span> <span data-ttu-id="032ce-207">들어오는 폼 매개 변수를 사용 하 여 전달 하는 개체의 속성을 업데이트 하는 것을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-207">It supports updating the properties of an object we pass it using the incoming form parameters.</span></span> <span data-ttu-id="032ce-208">리플렉션을 사용 하 여 개체의 속성 이름을 확인 한 다음 클라이언트에서 제출한 입력 값을 기반으로 값을 자동으로 변환 하 고 값을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-208">It uses reflection to determine the property names on the object, and then automatically converts and assigns values to them based on the input values submitted by the client.</span></span>

<span data-ttu-id="032ce-209">UpdateModel () 메서드를 사용 하 여 다음 코드를 사용 하 여 HTTP-사후 편집 작업을 단순화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-209">We could use the UpdateModel() method to simplify our HTTP-POST Edit Action using this code:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample11.cs)]

<span data-ttu-id="032ce-210">이제 */Dinners/Edit/1* URL을 방문 하 여 저녁의 제목을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-210">We can now visit the */Dinners/Edit/1* URL, and change the title of our Dinner:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image7.png)

<span data-ttu-id="032ce-211">"저장" 단추를 클릭 하면 편집 작업에 폼 게시를 수행 하 고 업데이트 된 값이 데이터베이스에 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-211">When we click the "Save" button, we'll perform a form post to our Edit action, and the updated values will be persisted in the database.</span></span> <span data-ttu-id="032ce-212">그러면 Dinner (새로 저장 된 값이 표시 됨)에 대 한 세부 정보 URL로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-212">We will then be redirected to the Details URL for the Dinner (which will display the newly saved values):</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image8.png)

#### <a name="handling-edit-errors"></a><span data-ttu-id="032ce-213">편집 오류 처리</span><span class="sxs-lookup"><span data-stu-id="032ce-213">Handling Edit Errors</span></span>

<span data-ttu-id="032ce-214">현재 HTTP POST 구현은 오류가 발생 한 경우를 제외 하 고는 정상적으로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-214">Our current HTTP-POST implementation works fine – except when there are errors.</span></span>

<span data-ttu-id="032ce-215">사용자가 양식을 편집 하는 실수를 하는 경우 양식이 수정 하도록 안내 하는 정보 오류 메시지와 함께 다시 표시 되는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-215">When a user makes a mistake editing a form, we need to make sure that the form is redisplayed with an informative error message that guides them to fix it.</span></span> <span data-ttu-id="032ce-216">여기에는 최종 사용자가 잘못 된 입력을 게시 하는 경우 (예: 잘못 된 날짜 문자열)와 입력 형식이 올바르지만 비즈니스 규칙 위반이 발생 하는 경우가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-216">This includes cases where an end-user posts incorrect input (for example: a malformed date string), as well as cases where the input format is valid but there is a business rule violation.</span></span> <span data-ttu-id="032ce-217">오류가 발생 하면 폼은 사용자가 원래 입력 한 입력 데이터를 그대로 유지 하 여 변경 내용을 수동으로 다시 채워야 하지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-217">When errors occur the form should preserve the input data the user originally entered so that they don't have to refill their changes manually.</span></span> <span data-ttu-id="032ce-218">이 프로세스는 양식이 성공적으로 완료 될 때까지 필요한 횟수 만큼 반복 됩니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-218">This process should repeat as many times as necessary until the form successfully completes.</span></span>

<span data-ttu-id="032ce-219">ASP.NET MVC에는 오류 처리 및 양식 다시 표시를 용이 하 게 하는 몇 가지 유용한 기본 제공 기능이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-219">ASP.NET MVC includes some nice built-in features that make error handling and form redisplay easy.</span></span> <span data-ttu-id="032ce-220">이러한 기능을 작동 하는 것을 확인 하려면 다음 코드를 사용 하 여 편집 작업 메서드를 업데이트 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-220">To see these features in action let's update our Edit action method with the following code:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample12.cs)]

<span data-ttu-id="032ce-221">위의 코드는 이제 작업에 대 한 try/catch 오류 처리 블록을 래핑하는 점을 제외 하 고 이전 구현과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-221">The above code is similar to our previous implementation – except that we are now wrapping a try/catch error handling block around our work.</span></span> <span data-ttu-id="032ce-222">UpdateModel ()를 호출할 때 예외가 발생 하거나, (모델 내에서 규칙 위반으로 인해 저장 하려는 Dinner object가 잘못 된 경우 예외를 발생 시키는 경우 예외를 발생 시키는), 오류 처리 블록이 catch 됩니다. 실행할.</span><span class="sxs-lookup"><span data-stu-id="032ce-222">If an exception occurs either when calling UpdateModel(), or when we try and save the DinnerRepository (which will raise an exception if the Dinner object we are trying to save is invalid because of a rule violation within our model), our catch error handling block will execute.</span></span> <span data-ttu-id="032ce-223">이 내에서 저녁 개체에 존재 하는 모든 규칙 위반을 반복 하 여 해당 개체를 ModelState 개체에 추가 합니다. (곧 논의 될 예정입니다.)</span><span class="sxs-lookup"><span data-stu-id="032ce-223">Within it we loop over any rule violations that exist in the Dinner object and add them to a ModelState object (which we'll discuss shortly).</span></span> <span data-ttu-id="032ce-224">그런 다음 뷰를 다시 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-224">We then redisplay the view.</span></span>

<span data-ttu-id="032ce-225">이 작업을 확인 하려면 응용 프로그램을 다시 실행 하 고 Dinner a를 편집한 다음 빈 제목, EventDate "위조"로 변경 하 고 country 값이 USA 인 영국 전화 번호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-225">To see this working let's re-run the application, edit a Dinner, and change it to have an empty Title, an EventDate of "BOGUS", and use a UK phone number with a country value of USA.</span></span> <span data-ttu-id="032ce-226">"저장" 단추를 누르면 HTTP POST Edit 메서드는 Dinner (오류가 있으므로)를 저장할 수 없으며 다음 양식을 다시 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-226">When we press the "Save" button our HTTP POST Edit method will not be able to save the Dinner (because there are errors) and will redisplay the form:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image9.png)

<span data-ttu-id="032ce-227">응용 프로그램에는 훌륭한 오류 환경이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-227">Our application has a decent error experience.</span></span> <span data-ttu-id="032ce-228">잘못 된 입력을 포함 하는 텍스트 요소는 빨간색으로 강조 표시 되 고 유효성 검사 오류 메시지는 최종 사용자에 게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-228">The text elements with the invalid input are highlighted in red, and validation error messages are displayed to the end user about them.</span></span> <span data-ttu-id="032ce-229">또한 폼은 사용자가 원래 입력 한 입력 데이터를 유지 하므로 모든 항목을 다시 쓸 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-229">The form is also preserving the input data the user originally entered – so that they don't have to refill anything.</span></span>

<span data-ttu-id="032ce-230">그렇다면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="032ce-230">How, you might ask, did this occur?</span></span> <span data-ttu-id="032ce-231">제목, EventDate 및 연락처 전화 텍스트 상자를 빨간색으로 강조 표시 하 고 원래 입력 된 사용자 값을 출력 하는 방법은 무엇 인가요?</span><span class="sxs-lookup"><span data-stu-id="032ce-231">How did the Title, EventDate, and ContactPhone textboxes highlight themselves in red and know to output the originally entered user values?</span></span> <span data-ttu-id="032ce-232">그리고 오류 메시지가 위쪽의 목록에 어떻게 표시 되나요?</span><span class="sxs-lookup"><span data-stu-id="032ce-232">And how did error messages get displayed in the list at the top?</span></span> <span data-ttu-id="032ce-233">좋은 소식은 입력 유효성 검사 및 오류 처리 시나리오를 쉽게 해 주는 기본 제공 ASP.NET MVC 기능 중 일부를 사용 했기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-233">The good news is that this didn't occur by magic - rather it was because we used some of the built-in ASP.NET MVC features that make input validation and error handling scenarios easy.</span></span>

#### <a name="understanding-modelstate-and-the-validation-html-helper-methods"></a><span data-ttu-id="032ce-234">ModelState 및 유효성 검사 HTML 도우미 메서드 이해</span><span class="sxs-lookup"><span data-stu-id="032ce-234">Understanding ModelState and the Validation HTML Helper Methods</span></span>

<span data-ttu-id="032ce-235">컨트롤러 클래스에는 뷰에 전달 되는 모델 개체에 오류가 있음을 나타내는 방법을 제공 하는 "ModelState" 속성 컬렉션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-235">Controller classes have a "ModelState" property collection which provides a way to indicate that errors exist with a model object being passed to a View.</span></span> <span data-ttu-id="032ce-236">ModelState 컬렉션 내의 오류 항목은 문제가 있는 모델 속성의 이름 (예: "제목", "EventDate" 또는 "연락처 전화")을 식별 하 고 사용자에 게 친숙 한 오류 메시지를 지정할 수 있도록 허용 합니다 (예: "제목 필요").</span><span class="sxs-lookup"><span data-stu-id="032ce-236">Error entries within the ModelState collection identify the name of the model property with the issue (for example: "Title", "EventDate", or "ContactPhone"), and allow a human-friendly error message to be specified (for example: "Title is required").</span></span>

<span data-ttu-id="032ce-237">*UpdateModel ()* 도우미 메서드는 모델 개체의 속성에 양식 값을 할당 하는 동안 오류가 발생할 때 modelstate 컬렉션을 자동으로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-237">The *UpdateModel()* helper method automatically populates the ModelState collection when it encounters errors while trying to assign form values to properties on the model object.</span></span> <span data-ttu-id="032ce-238">예를 들어 Dinner object의 EventDate 속성은 DateTime 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-238">For example, our Dinner object's EventDate property is of type DateTime.</span></span> <span data-ttu-id="032ce-239">UpdateModel () 메서드가 위의 시나리오에서 문자열 값 "위조"를 할당할 수 없는 경우 UpdateModel () 메서드는 해당 속성에서 할당 오류가 발생 했음을 나타내는 항목을 ModelState 컬렉션에 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-239">When the UpdateModel() method was unable to assign the string value "BOGUS" to it in the scenario above, the UpdateModel() method added an entry to the ModelState collection indicating an assignment error had occurred with that property.</span></span>

<span data-ttu-id="032ce-240">또한 개발자는 "catch" 오류 처리 블록 내에서 수행 하는 것과 같은 방식으로 ModelState 컬렉션에 오류 항목을 명시적으로 추가 하는 코드를 작성할 수 있습니다 .이 블록의 활성 규칙 위반을 기반으로 하는 항목이 있는 저녁 개체:</span><span class="sxs-lookup"><span data-stu-id="032ce-240">Developers can also write code to explicitly add error entries into the ModelState collection like we are doing below within our "catch" error handling block, which is populating the ModelState collection with entries based on the active Rule Violations in the Dinner object:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample13.cs)]

#### <a name="html-helper-integration-with-modelstate"></a><span data-ttu-id="032ce-241">ModelState와 Html 도우미 통합</span><span class="sxs-lookup"><span data-stu-id="032ce-241">Html Helper Integration with ModelState</span></span>

<span data-ttu-id="032ce-242">Html 도우미 메서드 Html. TextBox ()-출력을 렌더링할 때 ModelState 컬렉션을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-242">HTML helper methods - like Html.TextBox() - check the ModelState collection when rendering output.</span></span> <span data-ttu-id="032ce-243">항목에 대 한 오류가 있으면 사용자가 입력 한 값과 CSS 오류 클래스를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-243">If an error for the item exists, they render the user-entered value and a CSS error class.</span></span>

<span data-ttu-id="032ce-244">예를 들어, "편집" 뷰에서는 Html. TextBox () 도우미 메서드를 사용 하 여 Dinner object의 EventDate를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-244">For example, in our "Edit" view we are using the Html.TextBox() helper method to render the EventDate of our Dinner object:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample14.aspx)]

<span data-ttu-id="032ce-245">오류가 발생 한 시나리오에서 뷰가 렌더링 되 면 Html. TextBox () 메서드는 ModelState 컬렉션을 확인 하 여 Dinner object의 "EventDate" 속성과 관련 된 오류가 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-245">When the view was rendered in the error scenario, the Html.TextBox() method checked the ModelState collection to see if there were any errors associated with the "EventDate" property of our Dinner object.</span></span> <span data-ttu-id="032ce-246">전송 된 사용자 입력 ("위조")을 값으로 렌더링 한 오류가 발생 한 것을 확인 하 고, 생성 된 &lt;입력 형식 = "textbox"/&gt; 태그에 css 오류 클래스를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-246">When it determined that there was an error it rendered the submitted user input ("BOGUS") as the value, and added a css error class to the &lt;input type="textbox"/&gt; markup it generated:</span></span>

[!code-html[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample15.html)]

<span data-ttu-id="032ce-247">Css 오류 클래스의 모양을 사용자 지정 하 여 원하는 대로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-247">You can customize the appearance of the css error class to look however you want.</span></span> <span data-ttu-id="032ce-248">기본 CSS 오류 클래스 – "입력-유효성 검사-오류"는 *\content\site.xml* 스타일 시트에 정의 되어 있으며 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-248">The default CSS error class – "input-validation-error" – is defined in the *\content\site.css* stylesheet and looks like below:</span></span>

[!code-css[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample16.css)]

<span data-ttu-id="032ce-249">이 CSS 규칙은 다음과 같이 잘못 된 입력 요소를 강조 표시 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-249">This CSS rule is what caused our invalid input elements to be highlighted like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image10.png)

##### <a name="htmlvalidationmessage-helper-method"></a><span data-ttu-id="032ce-250">Html.ValidationMessage() Helper Method</span><span class="sxs-lookup"><span data-stu-id="032ce-250">Html.ValidationMessage() Helper Method</span></span>

<span data-ttu-id="032ce-251">Html. ValidationMessage () 도우미 메서드를 사용 하 여 특정 모델 속성과 연결 된 ModelState 오류 메시지를 출력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-251">The Html.ValidationMessage() helper method can be used to output the ModelState error message associated with a particular model property:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample17.aspx)]

<span data-ttu-id="032ce-252">위의 코드 출력: *&lt;span class = "필드-유효성 검사-오류"&gt; 값 ' o n s '가 잘못 된&lt;/span&gt;*</span><span class="sxs-lookup"><span data-stu-id="032ce-252">The above code outputs: *&lt;span class="field-validation-error"&gt; The value ‘BOGUS' is invalid&lt;/span&gt;*</span></span>

<span data-ttu-id="032ce-253">또한 Html. ValidationMessage () 도우미 메서드는 개발자가 표시 되는 오류 텍스트 메시지를 재정의할 수 있도록 하는 두 번째 매개 변수를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-253">The Html.ValidationMessage() helper method also supports a second parameter that allows developers to override the error text message that is displayed:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample18.aspx)]

<span data-ttu-id="032ce-254">위의 코드 출력: *&lt;span class = "필드-유효성 검사-오류"&gt;\*&lt;/span&gt;* 는 eventdate 속성에 오류가 있을 때 기본 오류 텍스트 대신.</span><span class="sxs-lookup"><span data-stu-id="032ce-254">The above code outputs: *&lt;span class="field-validation-error"&gt;\*&lt;/span&gt;* instead of the default error text when an error is present for the EventDate property.</span></span>

##### <a name="htmlvalidationsummary-helper-method"></a><span data-ttu-id="032ce-255">Html.ValidationSummary() Helper Method</span><span class="sxs-lookup"><span data-stu-id="032ce-255">Html.ValidationSummary() Helper Method</span></span>

<span data-ttu-id="032ce-256">ValidationSummary () 도우미 메서드를 사용 하 여 ModelState 컬렉션에 있는 모든 자세한 오류 메시지의 &lt;l/&gt;&lt;/ul&gt; 목록과 함께 &lt;ul&gt;요약 오류 메시지를 렌더링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-256">The Html.ValidationSummary() helper method can be used to render a summary error message, accompanied by a &lt;ul&gt;&lt;li/&gt;&lt;/ul&gt; list of all detailed error messages in the ModelState collection:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image11.png)

<span data-ttu-id="032ce-257">ValidationSummary () 도우미 메서드는 선택적 문자열 매개 변수를 사용 합니다 .이 매개 변수는 자세한 오류 목록 위에 표시할 요약 오류 메시지를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-257">The Html.ValidationSummary() helper method takes an optional string parameter – which defines a summary error message to display above the list of detailed errors:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample19.aspx)]

<span data-ttu-id="032ce-258">필요에 따라 CSS를 사용 하 여 오류 목록 모양을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-258">You can optionally use CSS to override what the error list looks like.</span></span>

#### <a name="using-a-addruleviolations-helper-method"></a><span data-ttu-id="032ce-259">AddRuleViolations 도우미 메서드 사용</span><span class="sxs-lookup"><span data-stu-id="032ce-259">Using a AddRuleViolations Helper Method</span></span>

<span data-ttu-id="032ce-260">초기 HTTP POST 편집 구현은 해당 catch 블록 내에서 foreach 문을 사용 하 여 Dinner object의 규칙 위반을 반복 하 고 컨트롤러의 ModelState 컬렉션에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-260">Our initial HTTP-POST Edit implementation used a foreach statement within its catch block to loop over the Dinner object's Rule Violations and add them to the controller's ModelState collection:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample20.cs)]

<span data-ttu-id="032ce-261">ASP.NET MVC ModelStateDictionary 클래스에 도우미 메서드를 추가 하는 "ControllerHelpers" 클래스를 해당 프로젝트 내에 추가 하 여이 코드를 조금 더 깔끔하고 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-261">We can make this code a little cleaner by adding a "ControllerHelpers" class to the NerdDinner project, and implement an "AddRuleViolations" extension method within it that adds a helper method to the ASP.NET MVC ModelStateDictionary class.</span></span> <span data-ttu-id="032ce-262">이 확장 메서드는 RuleViolation 오류 목록으로 ModelStateDictionary을 채우는 데 필요한 논리를 캡슐화 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-262">This extension method can encapsulate the logic necessary to populate the ModelStateDictionary with a list of RuleViolation errors:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample21.cs)]

<span data-ttu-id="032ce-263">그런 다음이 확장 메서드를 사용 하 여이 확장 메서드를 사용 하 여 Dinner Rule 위반으로 ModelState 컬렉션을 채우는 HTTP POST 편집 작업 메서드를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-263">We can then update our HTTP-POST Edit action method to use this extension method to populate the ModelState collection with our Dinner Rule Violations.</span></span>

#### <a name="complete-edit-action-method-implementations"></a><span data-ttu-id="032ce-264">작업 메서드 구현 편집 완료</span><span class="sxs-lookup"><span data-stu-id="032ce-264">Complete Edit Action Method Implementations</span></span>

<span data-ttu-id="032ce-265">아래 코드는 편집 시나리오에 필요한 모든 컨트롤러 논리를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-265">The code below implements all of the controller logic necessary for our Edit scenario:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample22.cs)]

<span data-ttu-id="032ce-266">편집 구현에 대 한 좋은 점은, 컨트롤러 클래스와 뷰 템플릿이 모두 Dinner model에서 적용 되는 특정 유효성 검사 또는 비즈니스 규칙에 대해 알고 있어야 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-266">The nice thing about our Edit implementation is that neither our Controller class nor our View template has to know anything about the specific validation or business rules being enforced by our Dinner model.</span></span> <span data-ttu-id="032ce-267">나중에 모델에 추가 규칙을 추가할 수 있으며 컨트롤러 또는 뷰에서 코드를 변경 하 여 지원 하기 위해 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-267">We can add additional rules to our model in the future and do not have to make any code changes to our controller or view in order for them to be supported.</span></span> <span data-ttu-id="032ce-268">코드를 최소한으로 변경 하 여 나중에 응용 프로그램 요구 사항을 쉽게 향상 시킬 수 있는 유연성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-268">This provides us with the flexibility to easily evolve our application requirements in the future with a minimum of code changes.</span></span>

### <a name="create-support"></a><span data-ttu-id="032ce-269">지원 만들기</span><span class="sxs-lookup"><span data-stu-id="032ce-269">Create Support</span></span>

<span data-ttu-id="032ce-270">Microsoft는이 DinnersController 클래스의 "편집" 동작을 구현 했습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-270">We've finished implementing the "Edit" behavior of our DinnersController class.</span></span> <span data-ttu-id="032ce-271">이제에서 "만들기" 지원을 구현 하 여 사용자가 새 Dinners를 추가할 수 있도록 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-271">Let's now move on to implement the "Create" support on it – which will enable users to add new Dinners.</span></span>

#### <a name="the-http-get-create-action-method"></a><span data-ttu-id="032ce-272">HTTP-GET 작업 메서드</span><span class="sxs-lookup"><span data-stu-id="032ce-272">The HTTP-GET Create Action Method</span></span>

<span data-ttu-id="032ce-273">먼저 create action 메서드의 HTTP "GET" 동작을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-273">We'll begin by implementing the HTTP "GET" behavior of our create action method.</span></span> <span data-ttu-id="032ce-274">이 메서드는 누군가가 */Dinners/Create* URL을 방문할 때 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-274">This method will be called when someone visits the */Dinners/Create* URL.</span></span> <span data-ttu-id="032ce-275">구현은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-275">Our implementation looks like:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample23.cs)]

<span data-ttu-id="032ce-276">위의 코드는 새 Dinner object를 만들고 나중에 1 주일 후에 EventDate 속성을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-276">The code above creates a new Dinner object, and assigns its EventDate property to be one week in the future.</span></span> <span data-ttu-id="032ce-277">그런 다음 새 Dinner object를 기반으로 하는 뷰를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-277">It then renders a View that is based on the new Dinner object.</span></span> <span data-ttu-id="032ce-278">*View ()* 도우미 메서드에 이름을 명시적으로 전달 하지 않았으므로 규칙 기반 기본 경로를 사용 하 여 뷰 템플릿을 확인 합니다./Views/Dinners/Create.aspx.</span><span class="sxs-lookup"><span data-stu-id="032ce-278">Because we haven't explicitly passed a name to the *View()* helper method, it will use the convention based default path to resolve the view template: /Views/Dinners/Create.aspx.</span></span>

<span data-ttu-id="032ce-279">이제이 뷰 템플릿을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-279">Let's now create this view template.</span></span> <span data-ttu-id="032ce-280">이렇게 하려면 만들기 작업 메서드 내에서 마우스 오른쪽 단추를 클릭 하 고 "뷰 추가" 상황에 맞는 메뉴 명령을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-280">We can do this by right-clicking within the Create action method and selecting the "Add View" context menu command.</span></span> <span data-ttu-id="032ce-281">"뷰 추가" 대화 상자 내에서 저녁 개체를 보기 템플릿에 전달 하 고 "만들기" 템플릿을 자동으로 스 캐 폴드 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-281">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to the view template, and choose to auto-scaffold a "Create" template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image12.png)

<span data-ttu-id="032ce-282">"추가" 단추를 클릭 하면 Visual Studio가 "\Views\Dinners" 디렉터리에 새 스 캐 폴드 기반 "Create .aspx" 보기를 저장 하 고 IDE 내에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-282">When we click the "Add" button, Visual Studio will save a new scaffold-based "Create.aspx" view to the "\Views\Dinners" directory, and open it up within the IDE:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image13.png)

<span data-ttu-id="032ce-283">Microsoft에서 생성 된 기본 "create" 스 캐 폴드 파일을 몇 가지 변경 하 고 아래와 같이 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-283">Let's make a few changes to the default "create" scaffold file that was generated for us, and modify it up to look like below:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample24.aspx)]

<span data-ttu-id="032ce-284">이제 응용 프로그램을 실행 하 고 브라우저 내에서 *"/Dinners/Create"* URL에 액세스할 때 만들기 작업 구현에서 아래와 같은 UI를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-284">And now when we run our application and access the *"/Dinners/Create"* URL within the browser it will render UI like below from our Create action implementation:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image14.png)

#### <a name="implementing-the-http-post-create-action-method"></a><span data-ttu-id="032ce-285">HTTP POST 만들기 작업 메서드 구현</span><span class="sxs-lookup"><span data-stu-id="032ce-285">Implementing the HTTP-POST Create Action Method</span></span>

<span data-ttu-id="032ce-286">만들기 작업 메서드의 HTTP GET 버전이 구현 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-286">We have the HTTP-GET version of our Create action method implemented.</span></span> <span data-ttu-id="032ce-287">사용자가 [저장] 단추를 클릭 하면 */Dinners/Create* URL에 폼 게시를 수행 하 고 HTTP post 동사를 사용 하 여 HTML &lt;입력&gt; 양식 값을 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-287">When a user clicks the "Save" button it performs a form post to the */Dinners/Create* URL, and submits the HTML &lt;input&gt; form values using the HTTP POST verb.</span></span>

<span data-ttu-id="032ce-288">이제 create action 메서드의 HTTP POST 동작을 구현 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-288">Let's now implement the HTTP POST behavior of our create action method.</span></span> <span data-ttu-id="032ce-289">먼저 오버 로드 된 "Create" 작업 메서드를 ' AcceptVerbs ' 특성이 있는 "AcceptVerbs" 특성을 포함 하는 ' Create ' 작업 메서드를 추가 하 여 HTTP POST 시나리오를 처리 하는 것으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-289">We'll begin by adding an overloaded "Create" action method to our DinnersController that has an "AcceptVerbs" attribute on it that indicates it handles HTTP POST scenarios:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample25.cs)]

<span data-ttu-id="032ce-290">HTTP POST 사용 "만들기" 메서드 내에서 게시 된 양식 매개 변수에 액세스할 수 있는 여러 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-290">There are a variety of ways we can access the posted form parameters within our HTTP-POST enabled "Create" method.</span></span>

<span data-ttu-id="032ce-291">한 가지 방법은 새 Dinner object를 만든 후 *UpdateModel ()* 도우미 메서드 (예: 편집 작업)를 사용 하 여 게시 된 폼 값으로 채우는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-291">One approach is to create a new Dinner object and then use the *UpdateModel()* helper method (like we did with the Edit action) to populate it with the posted form values.</span></span> <span data-ttu-id="032ce-292">그런 다음,이를 데이터베이스에 추가 하 고 데이터베이스에 저장 한 다음 사용자를 세부 정보 작업으로 리디렉션하여 아래 코드를 사용 하 여 새로 만든 Dinner a를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-292">We can then add it to our DinnerRepository, persist it to the database, and redirect the user to our Details action to show the newly created Dinner using the code below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample26.cs)]

<span data-ttu-id="032ce-293">또는 Create () 작업 메서드가 Dinner object를 메서드 매개 변수로 사용 하는 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-293">Alternatively, we can use an approach where we have our Create() action method take a Dinner object as a method parameter.</span></span> <span data-ttu-id="032ce-294">그런 다음 ASP.NET MVC는 자동으로 새 Dinner object를 인스턴스화하고, 양식 입력을 사용 하 여 속성을 채우고, 작업 메서드에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-294">ASP.NET MVC will then automatically instantiate a new Dinner object for us, populate its properties using the form inputs, and pass it to our action method:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample27.cs)]

<span data-ttu-id="032ce-295">위의 작업 메서드는 ModelState. IsValid 속성을 확인 하 여 Dinner object가 폼 게시 값으로 채워져 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-295">Our action method above verifies that the Dinner object has been successfully populated with the form post values by checking the ModelState.IsValid property.</span></span> <span data-ttu-id="032ce-296">입력 변환 문제가 있는 경우 false를 반환 하 고 (예: EventDate 속성의 "가짜" 문자열), 동작 메서드에서 폼을 다시 설정 하는 데 문제가 있는 경우 false를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-296">This will return false if there are input conversion issues (for example: a string of "BOGUS" for the EventDate property), and if there are any issues our action method redisplays the form.</span></span>

<span data-ttu-id="032ce-297">입력 값이 유효 하면 작업 메서드는 새 Dinner를 추가 하 고이를 새 Dinner in을 d에 게 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-297">If the input values are valid, then the action method attempts to add and save the new Dinner to the DinnerRepository.</span></span> <span data-ttu-id="032ce-298">이 작업은 try/catch 블록 내에서 래핑하고 비즈니스 규칙 위반이 발생할 경우 폼을 다시 시작 합니다 .이 경우에는 예외가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-298">It wraps this work within a try/catch block and redisplays the form if there are any business rule violations (which would cause the dinnerRepository.Save() method to raise an exception).</span></span>

<span data-ttu-id="032ce-299">동작에서이 오류 처리 동작을 확인 하기 위해 */Dinners/Create* URL을 요청 하 고 새 Dinner a에 대 한 세부 정보를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-299">To see this error handling behavior in action, we can request the */Dinners/Create* URL and fill out details about a new Dinner.</span></span> <span data-ttu-id="032ce-300">입력 또는 값이 잘못 되 면 아래와 같이 강조 표시 된 오류와 함께 만들기 양식이 다시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-300">Incorrect input or values will cause the create form to be redisplayed with the errors highlighted like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image15.png)

<span data-ttu-id="032ce-301">만들기 양식이 편집 양식과 정확히 동일한 유효성 검사 및 비즈니스 규칙을 어떻게 인식 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-301">Notice how our Create form is honoring the exact same validation and business rules as our Edit form.</span></span> <span data-ttu-id="032ce-302">이는 유효성 검사 및 비즈니스 규칙이 모델에서 정의 되었고 응용 프로그램의 UI 나 컨트롤러에 포함 되지 않았기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-302">This is because our validation and business rules were defined in the model, and were not embedded within the UI or controller of the application.</span></span> <span data-ttu-id="032ce-303">즉, 나중에 유효성 검사 또는 비즈니스 규칙을 한 곳에서 변경/진화 하 고 응용 프로그램 전체에 적용 되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-303">This means we can later change/evolve our validation or business rules in a single place and have them apply throughout our application.</span></span> <span data-ttu-id="032ce-304">새 규칙을 자동으로 적용 하거나 기존 규칙에 대 한 수정 사항을 자동으로 적용 하도록 편집 또는 만들기 작업 메서드 내의 코드를 변경 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-304">We will not have to change any code within either our Edit or Create action methods to automatically honor any new rules or modifications to existing ones.</span></span>

<span data-ttu-id="032ce-305">입력 값을 수정 하 고 "저장" 단추를 다시 클릭 하면, 해당 하는 경우에는 추가 작업이 성공 하 고 새 Dinner가 데이터베이스에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-305">When we fix the input values and click the "Save" button again, our addition to the DinnerRepository will succeed, and a new Dinner will be added to the database.</span></span> <span data-ttu-id="032ce-306">그런 다음 */Dinners/Details/[id]* URL로 리디렉션됩니다. 여기에서 새로 만든 Dinner a에 대 한 세부 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-306">We will then be redirected to the */Dinners/Details/[id]* URL – where we will be presented with details about the newly created Dinner:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image16.png)

### <a name="delete-support"></a><span data-ttu-id="032ce-307">삭제 지원</span><span class="sxs-lookup"><span data-stu-id="032ce-307">Delete Support</span></span>

<span data-ttu-id="032ce-308">이제 microsoft의 ' 삭제 ' 지원을 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-308">Let's now add "Delete" support to our DinnersController.</span></span>

#### <a name="the-http-get-delete-action-method"></a><span data-ttu-id="032ce-309">HTTP-GET Delete 동작 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-309">The HTTP-GET Delete Action Method</span></span>

<span data-ttu-id="032ce-310">먼저 delete 동작 메서드의 HTTP GET 동작을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-310">We'll begin by implementing the HTTP GET behavior of our delete action method.</span></span> <span data-ttu-id="032ce-311">이 메서드는 누군가가 */Dinners/Delete/[id]* URL을 방문할 때 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-311">This method will get called when someone visits the */Dinners/Delete/[id]* URL.</span></span> <span data-ttu-id="032ce-312">다음은 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-312">Below is the implementation:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample28.cs)]

<span data-ttu-id="032ce-313">작업 메서드는 삭제할 Dinner a를 검색 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-313">The action method attempts to retrieve the Dinner to be deleted.</span></span> <span data-ttu-id="032ce-314">Dinner exists가 있는 경우 Dinner object를 기준으로 뷰를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-314">If the Dinner exists it renders a View based on the Dinner object.</span></span> <span data-ttu-id="032ce-315">개체가 존재 하지 않거나 이미 삭제 된 경우 "Details" 작업 메서드에 대해 앞에서 만든 "NotFound" 뷰 템플릿을 렌더링 하는 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-315">If the object doesn't exist (or has already been deleted) it returns a View that renders the "NotFound" view template we created earlier for our "Details" action method.</span></span>

<span data-ttu-id="032ce-316">삭제 작업 메서드 내에서 마우스 오른쪽 단추를 클릭 하 고 "뷰 추가" 상황에 맞는 메뉴 명령을 선택 하 여 "삭제" 뷰 템플릿을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-316">We can create the "Delete" view template by right-clicking within the Delete action method and selecting the "Add View" context menu command.</span></span> <span data-ttu-id="032ce-317">"뷰 추가" 대화 상자 내에서 Dinner object를 뷰 템플릿에 모델로 전달 하 고 빈 템플릿을 만들도록 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-317">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to our view template as its model, and choose to create an empty template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image17.png)

<span data-ttu-id="032ce-318">"추가" 단추를 클릭 하면 Visual Studio에서 "\Views\Dinners" 디렉터리 내에 새 ".aspx" 보기 템플릿 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-318">When we click the "Add" button, Visual Studio will add a new "Delete.aspx" view template file for us within our "\Views\Dinners" directory.</span></span> <span data-ttu-id="032ce-319">템플릿에 HTML 및 코드를 추가 하 여 아래와 같은 삭제 확인 화면을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-319">We'll add some HTML and code to the template to implement a delete confirmation screen like below:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample29.aspx)]

<span data-ttu-id="032ce-320">위의 코드는 삭제할 Dinner of의 제목을 표시 하 고, 최종 사용자가 해당 내에서 "삭제" 단추를 클릭 하면/Dinners/Delete/[id] URL에 게시물을 수행 하는 &lt;form&gt; 요소를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-320">The code above displays the title of the Dinner to be deleted, and outputs a &lt;form&gt; element that does a POST to the /Dinners/Delete/[id] URL if the end-user clicks the "Delete" button within it.</span></span>

<span data-ttu-id="032ce-321">응용 프로그램을 실행 하 고 유효한 Dinner object에 대 한 *"/Dinners/Delete/[id]"* URL에 액세스 하는 경우 아래와 같은 UI를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-321">When we run our application and access the *"/Dinners/Delete/[id]"* URL for a valid Dinner object it renders UI like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image18.png)

| <span data-ttu-id="032ce-322">**사이드 토픽: POST를 수행 하는 이유는 무엇 인가요?**</span><span class="sxs-lookup"><span data-stu-id="032ce-322">**Side Topic: Why are we doing a POST?**</span></span> |
| --- |
| <span data-ttu-id="032ce-323">사용자에 게 요청할 수 있습니다. 삭제 확인 화면 내에서&gt; &lt;양식을 만드는 데 필요한 이유는 무엇 인가요?</span><span class="sxs-lookup"><span data-stu-id="032ce-323">You might ask – why did we go through the effort of creating a &lt;form&gt; within our Delete confirmation screen?</span></span> <span data-ttu-id="032ce-324">단순히 표준 하이퍼링크를 사용 하 여 실제 삭제 작업을 수행 하는 동작 메서드에 연결 하지 않는 이유는 무엇 인가요?</span><span class="sxs-lookup"><span data-stu-id="032ce-324">Why not just use a standard hyperlink to link to an action method that does the actual delete operation?</span></span> <span data-ttu-id="032ce-325">그 이유는 Url을 검색 하는 웹 크롤러 및 검색 엔진 으로부터 보호 하 고 링크를 팔 로우 할 때 실수로 데이터를 삭제 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-325">The reason is because we want to be careful to guard against web-crawlers and search engines discovering our URLs and inadvertently causing data to be deleted when they follow the links.</span></span> <span data-ttu-id="032ce-326">HTTP-GET 기반 Url은 액세스/탐색에 "안전한" 것으로 간주 되며 HTTP POST를 따르지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-326">HTTP-GET based URLs are considered "safe" for them to access/crawl, and they are supposed to not follow HTTP-POST ones.</span></span> <span data-ttu-id="032ce-327">좋은 규칙은 항상 소거식 또는 데이터 수정 작업을 HTTP POST 요청 뒤에 배치 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-327">A good rule is to make sure you always put destructive or data modifying operations behind HTTP-POST requests.</span></span> |

#### <a name="implementing-the-http-post-delete-action-method"></a><span data-ttu-id="032ce-328">HTTP-사후 삭제 작업 메서드 구현</span><span class="sxs-lookup"><span data-stu-id="032ce-328">Implementing the HTTP-POST Delete Action Method</span></span>

<span data-ttu-id="032ce-329">이제 삭제 확인 화면을 표시 하는 ' 삭제 작업 ' 메서드의 HTTP 가져오기 버전을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-329">We now have the HTTP-GET version of our Delete action method implemented which displays a delete confirmation screen.</span></span> <span data-ttu-id="032ce-330">최종 사용자가 "삭제" 단추를 클릭 하면 */Dinners/Dinner/[id]* URL에 폼 게시가 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-330">When an end user clicks the "Delete" button it will perform a form post to the */Dinners/Dinner/[id]* URL.</span></span>

<span data-ttu-id="032ce-331">이제 다음 코드를 사용 하 여 delete 동작 메서드의 HTTP "POST" 동작을 구현 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-331">Let's now implement the HTTP "POST" behavior of the delete action method using the code below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample30.cs)]

<span data-ttu-id="032ce-332">삭제 작업 메서드의 HTTP POST 버전은 삭제할 dinner object를 검색 하려고 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-332">The HTTP-POST version of our Delete action method attempts to retrieve the dinner object to delete.</span></span> <span data-ttu-id="032ce-333">이를 찾을 수 없는 경우 (이미 삭제 되었기 때문에) "NotFound" 템플릿을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-333">If it can't find it (because it has already been deleted) it renders our "NotFound" template.</span></span> <span data-ttu-id="032ce-334">저녁을 찾은 경우에는이를 d a d i 저장소에서 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-334">If it finds the Dinner, it deletes it from the DinnerRepository.</span></span> <span data-ttu-id="032ce-335">그런 다음 "삭제 된" 템플릿을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-335">It then renders a "Deleted" template.</span></span>

<span data-ttu-id="032ce-336">"삭제 된" 템플릿을 구현 하려면 작업 메서드를 마우스 오른쪽 단추로 클릭 하 고 "뷰 추가" 상황에 맞는 메뉴를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-336">To implement the "Deleted" template we'll right-click in the action method and choose the "Add View" context menu.</span></span> <span data-ttu-id="032ce-337">보기의 이름을 "Deleted"로 지정 하 고 빈 템플릿 (강력한 형식의 모델 개체를 사용 하지 않음)으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-337">We'll name our view "Deleted" and have it be an empty template (and not take a strongly-typed model object).</span></span> <span data-ttu-id="032ce-338">그런 다음 몇 가지 HTML 콘텐츠를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-338">We'll then add some HTML content to it:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample31.aspx)]

<span data-ttu-id="032ce-339">이제 응용 프로그램을 실행 하 고 유효한 Dinner object에 대 한 *"/Dinners/Delete/[id]"* URL에 액세스할 때 아래와 같이 Dinner Delete 확인 화면이 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-339">And now when we run our application and access the *"/Dinners/Delete/[id]"* URL for a valid Dinner object it will render our Dinner delete confirmation screen like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image19.png)

<span data-ttu-id="032ce-340">"삭제" 단추를 클릭 하면 */Dinners/Delete/[id]* URL에 대 한 HTTP POST를 수행 하 여 데이터베이스에서 Dinner a를 삭제 하 고 "Deleted" 보기 템플릿을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-340">When we click the "Delete" button it will perform an HTTP-POST to the */Dinners/Delete/[id]* URL, which will delete the Dinner from our database, and display our "Deleted" view template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image20.png)

### <a name="model-binding-security"></a><span data-ttu-id="032ce-341">모델 바인딩 보안</span><span class="sxs-lookup"><span data-stu-id="032ce-341">Model Binding Security</span></span>

<span data-ttu-id="032ce-342">ASP.NET MVC의 기본 제공 모델 바인딩 기능을 사용 하는 두 가지 다른 방법에 대해 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-342">We've discussed two different ways to use the built-in model-binding features of ASP.NET MVC.</span></span> <span data-ttu-id="032ce-343">첫 번째는 UpdateModel () 메서드를 사용 하 여 기존 모델 개체의 속성을 업데이트 하 고, 두 번째는 ASP.NET MVC를 사용 하 여의 모델 개체를 동작 메서드 매개 변수로 전달 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-343">The first using the UpdateModel() method to update properties on an existing model object, and the second using ASP.NET MVC's support for passing model objects in as action method parameters.</span></span> <span data-ttu-id="032ce-344">두 기술 모두 매우 강력 하 고 매우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-344">Both of these techniques are very powerful and extremely useful.</span></span>

<span data-ttu-id="032ce-345">또한이 기능을 사용 하면 it 책임이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-345">This power also brings with it responsibility.</span></span> <span data-ttu-id="032ce-346">사용자 입력을 허용 하는 경우 항상 보안에 대해 paranoid 하는 것이 중요 하며,이는 개체를 폼 입력에 바인딩할 때에도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-346">It is important to always be paranoid about security when accepting any user input, and this is also true when binding objects to form input.</span></span> <span data-ttu-id="032ce-347">HTML 및 JavaScript 주입 공격을 방지 하기 위해 사용자가 입력 한 값을 항상 HTML로 인코딩하고 SQL 삽입 공격에 주의 해야 합니다 (참고:이를 방지 하기 위해 매개 변수를 자동으로 인코딩하는 응용 프로그램에 대 한 LINQ to SQL를 사용 중입니다. 공격 유형).</span><span class="sxs-lookup"><span data-stu-id="032ce-347">You should be careful to always HTML encode any user-entered values to avoid HTML and JavaScript injection attacks, and be careful of SQL injection attacks (note: we are using LINQ to SQL for our application, which automatically encodes parameters to prevent these types of attacks).</span></span> <span data-ttu-id="032ce-348">클라이언트 쪽 유효성 검사에만 의존해 서는 안 되며 항상 서버 쪽 유효성 검사를 사용 하 여 가짜 값을 보내려고 시도 하는 해커 로부터 보호 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-348">You should never rely on client-side validation alone, and always employ server-side validation to guard against hackers attempting to send you bogus values.</span></span>

<span data-ttu-id="032ce-349">ASP.NET MVC의 바인딩 기능을 사용할 때 고려해 야 할 추가 보안 항목 중 하나는 사용자가 바인딩하는 개체의 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-349">One additional security item to make sure you think about when using the binding features of ASP.NET MVC is the scope of the objects you are binding.</span></span> <span data-ttu-id="032ce-350">특히, 바인딩할 수 있는 속성의 보안 의미를 이해 하 고 최종 사용자가 업데이트 하기 위해 정말로 업데이트할 수 있는 속성만 허용 하는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-350">Specifically, you want to make sure you understand the security implications of the properties you are allowing to be bound, and make sure you only allow those properties that really should be updatable by an end-user to be updated.</span></span>

<span data-ttu-id="032ce-351">기본적으로 UpdateModel () 메서드는 들어오는 폼 매개 변수 값과 일치 하는 모델 개체의 모든 속성을 업데이트 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-351">By default, the UpdateModel() method will attempt to update all properties on the model object that match incoming form parameter values.</span></span> <span data-ttu-id="032ce-352">마찬가지로 기본적으로 동작 메서드 매개 변수로 전달 되는 개체는 폼 매개 변수를 통해 설정 된 모든 속성을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-352">Likewise, objects passed as action method parameters also by default can have all of their properties set via form parameters.</span></span>

#### <a name="locking-down-binding-on-a-per-usage-basis"></a><span data-ttu-id="032ce-353">사용률에 대 한 바인딩 잠금</span><span class="sxs-lookup"><span data-stu-id="032ce-353">Locking down binding on a per-usage basis</span></span>

<span data-ttu-id="032ce-354">업데이트할 수 있는 속성의 명시적 "포함 목록"을 제공 하 여 사용 별로 바인딩 정책을 잠글 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-354">You can lock down the binding policy on a per-usage basis by providing an explicit "include list" of properties that can be updated.</span></span> <span data-ttu-id="032ce-355">이 작업은 다음과 같이 UpdateModel () 메서드에 추가 문자열 배열 매개 변수를 전달 하 여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-355">This can be done by passing an extra string array parameter to the UpdateModel() method like below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample32.cs)]

<span data-ttu-id="032ce-356">동작 메서드 매개 변수로 전달 되는 개체는 다음과 같이 허용 되는 속성의 "포함 목록"을 지정할 수 있는 [Bind] 특성도 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-356">Objects passed as action method parameters also support a [Bind] attribute that enables an "include list" of allowed properties to be specified like below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample33.cs)]

#### <a name="locking-down-binding-on-a-type-basis"></a><span data-ttu-id="032ce-357">형식에 대 한 바인딩 잠금</span><span class="sxs-lookup"><span data-stu-id="032ce-357">Locking down binding on a type basis</span></span>

<span data-ttu-id="032ce-358">유형별 기준으로 바인딩 규칙을 잠글 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-358">You can also lock down the binding rules on a per-type basis.</span></span> <span data-ttu-id="032ce-359">이렇게 하면 바인딩 규칙을 한 번 지정한 다음 모든 컨트롤러 및 작업 메서드에서 모든 시나리오 (UpdateModel 및 동작 메서드 매개 변수 시나리오 모두 포함)에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-359">This allows you to specify the binding rules once, and then have them apply in all scenarios (including both UpdateModel and action method parameter scenarios) across all controllers and action methods.</span></span>

<span data-ttu-id="032ce-360">[Bind] 특성을 형식에 추가 하거나 응용 프로그램의 Global.asax 파일에 등록 하 여 형식당 하나의 형식 바인딩 규칙을 사용자 지정할 수 있습니다 (형식을 소유 하지 않는 시나리오에 유용).</span><span class="sxs-lookup"><span data-stu-id="032ce-360">You can customize the per-type binding rules by adding a [Bind] attribute onto a type, or by registering it within the Global.asax file of the application (useful for scenarios where you don't own the type).</span></span> <span data-ttu-id="032ce-361">그런 다음 Bind 특성의 Include 및 Exclude 속성을 사용 하 여 특정 클래스 또는 인터페이스에 대해 바인딩할 수 있는 속성을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-361">You can then use the Bind attribute's Include and Exclude properties to control which properties are bindable for the particular class or interface.</span></span>

<span data-ttu-id="032ce-362">여기서는 팀 간 Ddinner 응용 프로그램에서 Dinner class에 대해이 기술을 사용 하 고 바인딩 가능한 속성의 목록을 다음으로 제한 하는 [Bind] 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-362">We'll use this technique for the Dinner class in our NerdDinner application, and add a [Bind] attribute to it that restricts the list of bindable properties to the following:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample34.cs)]

<span data-ttu-id="032ce-363">바인딩을 통해 RSVPs 컬렉션을 조작 하는 것을 허용 하지 않으며, 바인딩을 통해 DinnerID 또는 HostedBy 속성을 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-363">Notice we are not allowing the RSVPs collection to be manipulated via binding, nor are we allowing the DinnerID or HostedBy properties to be set via binding.</span></span> <span data-ttu-id="032ce-364">보안상의 이유로 작업 메서드 내에서 명시적 코드를 사용 하 여 이러한 특정 속성을 조작 합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-364">For security reasons we'll instead only manipulate these particular properties using explicit code within our action methods.</span></span>

### <a name="crud-wrap-up"></a><span data-ttu-id="032ce-365">CRUD 래핑</span><span class="sxs-lookup"><span data-stu-id="032ce-365">CRUD Wrap-Up</span></span>

<span data-ttu-id="032ce-366">ASP.NET MVC에는 양식 게시 시나리오를 구현 하는 데 도움이 되는 다양 한 기본 제공 기능이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-366">ASP.NET MVC includes a number of built-in features that help with implementing form posting scenarios.</span></span> <span data-ttu-id="032ce-367">Microsoft는 이러한 다양 한 기능을 사용 하 여 microsoft의 다양 한 기능을 통해 microsoft의</span><span class="sxs-lookup"><span data-stu-id="032ce-367">We used a variety of these features to provide CRUD UI support on top of our DinnerRepository.</span></span>

<span data-ttu-id="032ce-368">응용 프로그램을 구현 하는 모델 중심 접근 방법을 사용 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-368">We are using a model-focused approach to implement our application.</span></span> <span data-ttu-id="032ce-369">즉, 모든 유효성 검사 및 비즈니스 규칙 논리가 모델 계층 내에서 정의 되 고 컨트롤러 또는 뷰 내에서 정의 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-369">This means that all our validation and business rule logic is defined within our model layer – and not within our controllers or views.</span></span> <span data-ttu-id="032ce-370">컨트롤러 클래스와 뷰 템플릿은 Dinner model 클래스에서 적용 하는 특정 비즈니스 규칙에 대 한 정보를 알지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-370">Neither our Controller class nor our View templates know anything about the specific business rules being enforced by our Dinner model class.</span></span>

<span data-ttu-id="032ce-371">이렇게 하면 응용 프로그램 아키텍처가 깨끗 하 게 유지 되 고 테스트 하기가 더 쉬워집니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-371">This will keep our application architecture clean and make it easier to test.</span></span> <span data-ttu-id="032ce-372">향후 모델 계층에 비즈니스 규칙을 더 추가할 수 있으며, 컨트롤러 또는 뷰에서 *코드를 변경 하* 여 지원 하기 위해 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-372">We can add additional business rules to our model layer in the future and *not have to make any code changes* to our Controller or View in order for them to be supported.</span></span> <span data-ttu-id="032ce-373">이를 통해 향후 응용 프로그램을 개선 하 고 변경 하는 데 많은 민첩성을 제공할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-373">This is going to provide us with a great deal of agility to evolve and change our application in the future.</span></span>

<span data-ttu-id="032ce-374">이제 microsoft의 DinnersController에서 Dinner 목록/세부 정보 뿐만 아니라 만들기, 편집 및 삭제 지원을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-374">Our DinnersController now enables Dinner listings/details, as well as create, edit and delete support.</span></span> <span data-ttu-id="032ce-375">클래스에 대 한 전체 코드는 아래에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-375">The complete code for the class can be found below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample35.cs)]

### <a name="next-step"></a><span data-ttu-id="032ce-376">다음 단계</span><span class="sxs-lookup"><span data-stu-id="032ce-376">Next Step</span></span>

<span data-ttu-id="032ce-377">이제 microsoft의 기본 CRUD (만들기, 읽기, 업데이트 및 삭제) 지원이 microsoft의 DinnersController 클래스 내에서 구현 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-377">We now have basic CRUD (Create, Read, Update and Delete) support implement within our DinnersController class.</span></span>

<span data-ttu-id="032ce-378">이제 ViewData 및 ViewModel 클래스를 사용 하 여 폼에서 훨씬 더 풍부한 UI를 사용 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="032ce-378">Let's now look at how we can use ViewData and ViewModel classes to enable even richer UI on our forms.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="032ce-379">[이전](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
> [다음](use-viewdata-and-implement-viewmodel-classes.md)</span><span class="sxs-lookup"><span data-stu-id="032ce-379">[Previous](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
[Next](use-viewdata-and-implement-viewmodel-classes.md)</span></span>
