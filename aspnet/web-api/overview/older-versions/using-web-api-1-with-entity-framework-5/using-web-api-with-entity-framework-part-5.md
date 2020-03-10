---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
title: '5 부: 녹아웃을 사용 하 여 동적 UI 만들기 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 9d9cb3b0-f4a7-434e-a508-9fc0ad0eb813
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
msc.type: authoredcontent
ms.openlocfilehash: bbdeba756de7986cfeb92aa10a57f4f101382f99
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447863"
---
# <a name="part-5-creating-a-dynamic-ui-with-knockoutjs"></a><span data-ttu-id="66748-102">5 부: 녹아웃을 사용 하 여 동적 UI 만들기</span><span class="sxs-lookup"><span data-stu-id="66748-102">Part 5: Creating a Dynamic UI with Knockout.js</span></span>

<span data-ttu-id="66748-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="66748-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="66748-104">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="66748-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-a-dynamic-ui-with-knockoutjs"></a><span data-ttu-id="66748-105">Knockout.js를 사용하여 동적 UI 만들기</span><span class="sxs-lookup"><span data-stu-id="66748-105">Creating a Dynamic UI with Knockout.js</span></span>

<span data-ttu-id="66748-106">이 섹션에서는 node.js를 사용 하 여 관리 보기에 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="66748-106">In this section, we'll use Knockout.js to add functionality to the Admin view.</span></span>

<span data-ttu-id="66748-107">[녹아웃](http://knockoutjs.com/) 은 HTML 컨트롤을 데이터에 쉽게 바인딩할 수 있도록 하는 Javascript 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="66748-107">[Knockout.js](http://knockoutjs.com/) is a Javascript library that makes it easy to bind HTML controls to data.</span></span> <span data-ttu-id="66748-108">녹아웃은 MVVM (모델-뷰-ViewModel) 패턴을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="66748-108">Knockout.js uses the Model-View-ViewModel (MVVM) pattern.</span></span>

- <span data-ttu-id="66748-109">*모델* 은 비즈니스 도메인 (이 경우에는 제품 및 주문)의 데이터를 서버 쪽으로 표현한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="66748-109">The *model* is the server-side representation of the data in the business domain (in our case, products and orders).</span></span>
- <span data-ttu-id="66748-110">*뷰* 는 프레젠테이션 계층 (HTML)입니다.</span><span class="sxs-lookup"><span data-stu-id="66748-110">The *view* is the presentation layer (HTML).</span></span>
- <span data-ttu-id="66748-111">*뷰 모델* 은 모델 데이터를 포함 하는 Javascript 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="66748-111">The *view-model* is a Javascript object that holds the model data.</span></span> <span data-ttu-id="66748-112">뷰 모델은 UI의 코드 추상화입니다.</span><span class="sxs-lookup"><span data-stu-id="66748-112">The view-model is a code abstraction of the UI.</span></span> <span data-ttu-id="66748-113">HTML 표현에 대해 알지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="66748-113">It has no knowledge of the HTML representation.</span></span> <span data-ttu-id="66748-114">대신, 뷰의 추상 기능 (예: "항목 목록")을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="66748-114">Instead, it represents abstract features of the view, such as "a list of items".</span></span>

<span data-ttu-id="66748-115">뷰가 뷰 모델에 대 한 데이터 바인딩된 뷰입니다.</span><span class="sxs-lookup"><span data-stu-id="66748-115">The view is data-bound to the view-model.</span></span> <span data-ttu-id="66748-116">뷰 모델에 대 한 업데이트는 뷰에 자동으로 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66748-116">Updates to the view-model are automatically reflected in the view.</span></span> <span data-ttu-id="66748-117">뷰 모델은 또한 보기에서 단추 클릭과 같은 이벤트를 가져와서 주문 생성과 같은 모델에 대 한 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="66748-117">The view-model also gets events from the view, such as button clicks, and performs operations on the model, such as creating an order.</span></span>

![](using-web-api-with-entity-framework-part-5/_static/image1.png)

<span data-ttu-id="66748-118">먼저 뷰 모델을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="66748-118">First we'll define the view-model.</span></span> <span data-ttu-id="66748-119">그러면 HTML 태그를 뷰 모델에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="66748-119">After that, we will bind the HTML markup to the view-model.</span></span>

<span data-ttu-id="66748-120">다음 Razor 섹션을 관리자에 추가 합니다. cshtml:</span><span class="sxs-lookup"><span data-stu-id="66748-120">Add the following Razor section to Admin.cshtml:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample1.cshtml)]

<span data-ttu-id="66748-121">이 섹션은 파일의 아무 곳에 나 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66748-121">You can add this section anywhere in the file.</span></span> <span data-ttu-id="66748-122">뷰가 렌더링 되 면 HTML 페이지 맨 아래에 닫는 &lt;/본문&gt; 태그 바로 앞에 섹션이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66748-122">When the view is rendered, the section appears at the bottom of the HTML page, right before the closing &lt;/body&gt; tag.</span></span>

<span data-ttu-id="66748-123">이 페이지에 대 한 모든 스크립트는 주석으로 표시 된 스크립트 태그 안에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66748-123">All of the script for this page will go inside the script tag indicated by the comment:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample2.html)]

<span data-ttu-id="66748-124">먼저 뷰 모델 클래스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="66748-124">First, define a view-model class:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample3.js)]

<span data-ttu-id="66748-125">**observableArray** 는 *관찰*가능 이라고 하는 녹아웃의 특수 한 종류의 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="66748-125">**ko.observableArray** is a special kind of object in Knockout, called an *observable*.</span></span> <span data-ttu-id="66748-126">[Default.js 설명서](http://knockoutjs.com/documentation/observables.html)에서: 관찰 가능은 "구독자에 게 변경 내용을 알릴 수 있는 JavaScript 개체"입니다.</span><span class="sxs-lookup"><span data-stu-id="66748-126">From the [Knockout.js documentation](http://knockoutjs.com/documentation/observables.html): An observable is a "JavaScript object that can notify subscribers about changes."</span></span> <span data-ttu-id="66748-127">관찰 가능의 내용이 변경 되 면 뷰가 일치 하도록 자동으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66748-127">When the contents of an observable change, the view is automatically updated to match.</span></span>

<span data-ttu-id="66748-128">`products` 배열을 채우려면 웹 API에 대 한 AJAX 요청을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="66748-128">To populate the `products` array, make an AJAX request to the web API.</span></span> <span data-ttu-id="66748-129">API에 대 한 기본 URI를 보기 모음에 저장 했습니다 (자습서의 [4 부](using-web-api-with-entity-framework-part-4.md) 참조).</span><span class="sxs-lookup"><span data-stu-id="66748-129">Recall that we stored the base URI for the API in the view bag (see [Part 4](using-web-api-with-entity-framework-part-4.md) of the tutorial).</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample4.js?highlight=5)]

<span data-ttu-id="66748-130">그런 다음 뷰-모델에 함수를 추가 하 여 제품을 만들고, 업데이트 하 고, 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="66748-130">Next, add functions to the view-model to create, update, and delete products.</span></span> <span data-ttu-id="66748-131">이러한 함수는 AJAX 호출을 web API에 전송 하 고 결과를 사용 하 여 뷰 모델을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="66748-131">These functions submit AJAX calls to the web API and use the results to update the view-model.</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample5.js?highlight=7)]

<span data-ttu-id="66748-132">이제 가장 중요 한 부분은 다음과 같습니다. DOM이 fulled 로드 되 면 **ko. applyBindings** 함수를 호출 하 고 `ProductsViewModel`의 새 인스턴스를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="66748-132">Now the most important part: When the DOM is fulled loaded, call the **ko.applyBindings** function and pass in a new instance of the `ProductsViewModel`:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample6.js)]

<span data-ttu-id="66748-133">**Ko-kr bindings** 메서드는 녹아웃을 활성화 하 고 뷰에 뷰 모델을 배선 합니다.</span><span class="sxs-lookup"><span data-stu-id="66748-133">The **ko.applyBindings** method activates Knockout and wires up the view-model to the view.</span></span>

<span data-ttu-id="66748-134">이제 뷰 모델이 있으므로 바인딩을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66748-134">Now that we have a view-model, we can create the bindings.</span></span> <span data-ttu-id="66748-135">`data-bind` 특성을 HTML 요소에 추가 하 여이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="66748-135">In Knockout.js, you do this by adding `data-bind` attributes to HTML elements.</span></span> <span data-ttu-id="66748-136">예를 들어, HTML 목록을 배열에 바인딩하려면 `foreach` 바인딩을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="66748-136">For example, to bind an HTML list to an array, use the `foreach` binding:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample7.html?highlight=1)]

<span data-ttu-id="66748-137">`foreach` 바인딩은 배열을 반복 하 고 배열의 각 개체에 대해 자식 요소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="66748-137">The `foreach` binding iterates through the array and creates child elements for each object in the array.</span></span> <span data-ttu-id="66748-138">자식 요소의 바인딩은 배열 개체의 속성을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66748-138">Bindings on the child elements can refer to properties on the array objects.</span></span>

<span data-ttu-id="66748-139">"업데이트-제품" 목록에 다음 바인딩을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="66748-139">Add the following bindings to the "update-products" list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample8.html)]

<span data-ttu-id="66748-140">`<li>` 요소는 **foreach** 바인딩의 범위 내에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="66748-140">The `<li>` element occurs within the scope of the **foreach** binding.</span></span> <span data-ttu-id="66748-141">즉, 녹아웃은 `products` 배열의 각 제품에 대해 요소를 한 번씩 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="66748-141">That means Knockout will render the element once for each product in the `products` array.</span></span> <span data-ttu-id="66748-142">`<li>` 요소 내의 모든 바인딩은 해당 제품 인스턴스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="66748-142">All of the bindings within the `<li>` element refer to that product instance.</span></span> <span data-ttu-id="66748-143">예를 들어 `$data.Name`은 제품의 `Name` 속성을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="66748-143">For example, `$data.Name` refers to the `Name` property on the product.</span></span>

<span data-ttu-id="66748-144">텍스트 입력의 값을 설정 하려면 `value` 바인딩을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="66748-144">To set the values of the text inputs, use the `value` binding.</span></span> <span data-ttu-id="66748-145">단추는 `click` 바인딩을 사용 하 여 모델 뷰의 함수에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="66748-145">The buttons are bound to functions on the model-view, using the `click` binding.</span></span> <span data-ttu-id="66748-146">Product 인스턴스는 각 함수에 매개 변수로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66748-146">The product instance is passed as a parameter to each function.</span></span> <span data-ttu-id="66748-147">자세한 내용은 [default.js 설명서](http://knockoutjs.com/documentation/observables.html) 에서 다양 한 바인딩에 대해 잘 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="66748-147">For more information, the [Knockout.js documentation](http://knockoutjs.com/documentation/observables.html) has good descriptions of the various bindings.</span></span>

<span data-ttu-id="66748-148">다음으로, 제품 추가 양식에서 **전송** 이벤트에 대 한 바인딩을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="66748-148">Next, add a binding for the **submit** event on the Add Product form:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample9.html)]

<span data-ttu-id="66748-149">이 바인딩은 뷰 모델에서 `create` 함수를 호출 하 여 새 제품을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="66748-149">This binding calls the `create` function on the view-model to create a new product.</span></span>

<span data-ttu-id="66748-150">관리 보기에 대 한 전체 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="66748-150">Here is the complete code for the Admin view:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample10.cshtml)]

<span data-ttu-id="66748-151">응용 프로그램을 실행 하 고 관리자 계정으로 로그인 한 다음 "관리" 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="66748-151">Run the application, log in with the Administrator account, and click the "Admin" link.</span></span> <span data-ttu-id="66748-152">제품 목록이 표시 되 고 제품을 생성, 업데이트 또는 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66748-152">You should see the list of products, and be able to create, update, or delete products.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="66748-153">[이전](using-web-api-with-entity-framework-part-4.md)
> [다음](using-web-api-with-entity-framework-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="66748-153">[Previous](using-web-api-with-entity-framework-part-4.md)
[Next](using-web-api-with-entity-framework-part-6.md)</span></span>
