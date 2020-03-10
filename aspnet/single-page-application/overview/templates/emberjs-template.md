---
uid: single-page-application/overview/templates/emberjs-template
title: EmberJS 템플릿 | Microsoft Docs
author: xqiu
description: EmberJS 템플릿
ms.author: riande
ms.date: 01/30/2013
ms.assetid: 04d5f142-5f62-494a-b5ea-4f3d068d34cb
msc.legacyurl: /single-page-application/overview/templates/emberjs-template
msc.type: authoredcontent
ms.openlocfilehash: 1aefa46dd0841b1b06675409cc8a09f9a218d7ac
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467159"
---
# <a name="emberjs-template"></a><span data-ttu-id="6ef1f-103">EmberJS 템플릿</span><span class="sxs-lookup"><span data-stu-id="6ef1f-103">EmberJS template</span></span>

<span data-ttu-id="6ef1f-104">[Xinyang Qiu](https://github.com/xqiu)</span><span class="sxs-lookup"><span data-stu-id="6ef1f-104">by [Xinyang Qiu](https://github.com/xqiu)</span></span>

> <span data-ttu-id="6ef1f-105">EmberJS MVC 템플릿은 네 번째 Totten, Thiago Santos 및 Xinyang Qiu에 의해 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-105">The EmberJS MVC Template is written by Nathan Totten, Thiago Santos, and Xinyang Qiu.</span></span>
> 
> [<span data-ttu-id="6ef1f-106">EmberJS MVC 템플릿 다운로드</span><span class="sxs-lookup"><span data-stu-id="6ef1f-106">Download the EmberJS MVC Template</span></span>](https://go.microsoft.com/fwlink/?LinkId=282647)

<span data-ttu-id="6ef1f-107">EmberJS SPA 템플릿은 EmberJS를 사용 하 여 대화형 클라이언트 쪽 웹 앱을 신속 하 게 빌드할 수 있도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-107">The EmberJS SPA template is designed to get you started quickly building interactive client-side web apps using EmberJS.</span></span>

<span data-ttu-id="6ef1f-108">SPA (단일 페이지 응용 프로그램)는 단일 HTML 페이지를 로드 한 다음 새 페이지를 로드 하는 대신 페이지를 동적으로 업데이트 하는 웹 응용 프로그램에 대 한 일반적인 용어입니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-108">"Single-page application" (SPA) is the general term for a web application that loads a single HTML page and then updates the page dynamically, instead of loading new pages.</span></span> <span data-ttu-id="6ef1f-109">초기 페이지를 로드 한 후 SPA는 AJAX 요청을 통해 서버와 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-109">After the initial page load, the SPA talks with the server through AJAX requests.</span></span>

![](emberjs-template/_static/image1.png)

<span data-ttu-id="6ef1f-110">AJAX는 새로운 것은 아니지만 오늘날에는 크고 정교한 SPA 응용 프로그램을 쉽게 빌드하고 유지 관리할 수 있는 JavaScript 프레임 워크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-110">AJAX is nothing new, but today there are JavaScript frameworks that make it easier to build and maintain a large sophisticated SPA application.</span></span> <span data-ttu-id="6ef1f-111">또한 HTML 5와 CSS3을 통해 풍부한 Ui를 보다 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-111">Also, HTML 5 and CSS3 are making it easier to create rich UIs.</span></span>

<span data-ttu-id="6ef1f-112">EmberJS SPA 템플릿에서는 [Ember.js](http://emberjs.com/) JavaScript 라이브러리를 사용 하 여 AJAX 요청에서 페이지 업데이트를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-112">The EmberJS SPA Template uses the [Ember](http://emberjs.com/) JavaScript library to handle page updates from AJAX requests.</span></span> <span data-ttu-id="6ef1f-113">Ember.js는 데이터 바인딩을 사용 하 여 페이지를 최신 데이터와 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-113">Ember.js uses data binding to synchronize the page with the latest data.</span></span> <span data-ttu-id="6ef1f-114">이렇게 하면 JSON 데이터를 안내 하는 코드를 작성 하 여 DOM을 업데이트 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-114">That way, you don't have to write any of the code that walks through the JSON data and updates the DOM.</span></span> <span data-ttu-id="6ef1f-115">대신, Ember.js에 데이터를 제공 하는 방법을 설명 하는 선언적 특성을 HTML에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-115">Instead, you put declarative attributes in the HTML that tell Ember.js how to present the data.</span></span>

<span data-ttu-id="6ef1f-116">서버 쪽에서는 EmberJS 템플릿이 [KNOCKOUTJS SPA 템플릿과](../introduction/knockoutjs-template.md)거의 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-116">On the server side, the EmberJS template is almost identical to the [KnockoutJS SPA template](../introduction/knockoutjs-template.md).</span></span> <span data-ttu-id="6ef1f-117">ASP.NET MVC를 사용 하 여 HTML 문서를 제공 하 고 ASP.NET Web API 하 여 클라이언트에서 AJAX 요청을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-117">It uses ASP.NET MVC to serve HTML documents, and ASP.NET Web API to handle AJAX requests from the client.</span></span> <span data-ttu-id="6ef1f-118">템플릿의 이러한 측면에 대 한 자세한 내용은 [KnockoutJS 템플릿](../introduction/knockoutjs-template.md) 설명서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-118">For more information about those aspects of the template, refer to the [KnockoutJS template](../introduction/knockoutjs-template.md) documentation.</span></span> <span data-ttu-id="6ef1f-119">이 항목에서는 녹아웃 템플릿과 EmberJS 템플릿 간의 차이점에 대해 중점적으로 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-119">This topic focuses on the differences between the Knockout template and the EmberJS template.</span></span>

## <a name="create-an-emberjs-spa-template-project"></a><span data-ttu-id="6ef1f-120">EmberJS SPA 템플릿 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="6ef1f-120">Create an EmberJS SPA Template Project</span></span>

<span data-ttu-id="6ef1f-121">위의 다운로드 단추를 클릭 하 여 템플릿을 다운로드 하 고 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-121">Download and install the template by clicking the Download button above.</span></span> <span data-ttu-id="6ef1f-122">Visual Studio를 다시 시작 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-122">You might need to restart Visual Studio.</span></span>

<span data-ttu-id="6ef1f-123">**템플릿** 창에서 **설치 된 템플릿** 을 선택 하 고  **C# 시각적** 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-123">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="6ef1f-124">**시각적 개체 C#** 에서 **웹**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-124">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="6ef1f-125">프로젝트 템플릿 목록에서 **ASP.NET MVC 4 웹 응용 프로그램**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-125">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="6ef1f-126">프로젝트 이름을 지정하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-126">Name the project and click **OK**.</span></span>

![](emberjs-template/_static/image2.png)

<span data-ttu-id="6ef1f-127">**새 프로젝트** 마법사에서 **ember.js SPA 프로젝트**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-127">In the **New Project** wizard, select **Ember.js SPA Project**.</span></span>

![](emberjs-template/_static/image4.png)

## <a name="emberjs-spa-template-overview"></a><span data-ttu-id="6ef1f-128">EmberJS SPA 템플릿 개요</span><span class="sxs-lookup"><span data-stu-id="6ef1f-128">EmberJS SPA Template Overview</span></span>

<span data-ttu-id="6ef1f-129">EmberJS 템플릿은 jQuery, Ember.js, Handlebars을 조합 하 여 부드러운 대화형 UI를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-129">The EmberJS template uses a combination of jQuery, Ember.js, Handlebars.js to create a smooth, interactive UI.</span></span>

<span data-ttu-id="6ef1f-130">Ember.js는 클라이언트 쪽 MVC 패턴을 사용 하는 JavaScript 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-130">Ember.js is a JavaScript library that uses a client-side MVC pattern.</span></span>

- <span data-ttu-id="6ef1f-131">Handlebars 템플릿 언어로 작성 된 *템플릿은*응용 프로그램 사용자 인터페이스를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-131">A *template*, written in the Handlebars templating language, describes the application user interface.</span></span> <span data-ttu-id="6ef1f-132">릴리스 모드에서 [handlebars 컴파일러](https://github.com/Myslik/csharp-ember-handlebars) 는 handlebars template을 번들로 묶고 컴파일하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-132">In release mode, the [Handlebars compiler](https://github.com/Myslik/csharp-ember-handlebars) is used to bundle and compile the handlebars template.</span></span>
- <span data-ttu-id="6ef1f-133">*모델* 은 서버에서 가져온 응용 프로그램 데이터 (할 일 목록 및 할 일 항목)를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-133">A *model* stores the application data that it gets from the server (ToDo lists and ToDo items).</span></span>
- <span data-ttu-id="6ef1f-134">*컨트롤러* 는 응용 프로그램 상태를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-134">A *controller* stores application state.</span></span> <span data-ttu-id="6ef1f-135">컨트롤러는 종종 해당 템플릿에 모델 데이터를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-135">Controllers often present model data to the corresponding templates.</span></span>
- <span data-ttu-id="6ef1f-136">*뷰* 는 응용 프로그램에서 기본 이벤트를 변환 하 고이를 컨트롤러에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-136">A *view* translates primitive events from the application and passes these to the controller.</span></span>
- <span data-ttu-id="6ef1f-137">*라우터* 는 url과 템플릿을 동기화 된 상태로 유지 하 여 응용 프로그램 상태를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-137">A *router* manages application state, keeping URLs and templates in sync.</span></span>

<span data-ttu-id="6ef1f-138">또한 Ember.js 데이터 라이브러리를 사용 하 여 JSON 개체 (RESTful API를 통해 서버에서 가져옴)와 클라이언트 모델을 동기화 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-138">In addition, the Ember Data library can be used to synchronize JSON objects (obtained from the server through a RESTful API) and the client models.</span></span>

<span data-ttu-id="6ef1f-139">EmberJS SPA 템플릿은 스크립트를 8 개의 계층으로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-139">The EmberJS SPA template organizes the scripts into eight layers:</span></span>

- <span data-ttu-id="6ef1f-140">webapi\_webapi\_. x a x x. x x x: ASP.NET Web API 작업을 수행 하기 위해 Ember.js 데이터 라이브러리를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-140">webapi\_adapter.js, webapi\_serializer.js: Extends the Ember Data library to work with ASP.NET Web API.</span></span>
- <span data-ttu-id="6ef1f-141">Scripts/default.js: 새 Ember.js Handlebars 도우미를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-141">Scripts/helpers.js: Defines new Ember Handlebars helpers.</span></span>
- <span data-ttu-id="6ef1f-142">Scripts/node.js: 앱을 만들고 어댑터와 직렬 변환기를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-142">Scripts/app.js: Creates the app and configures the adapter and serializer.</span></span>
- <span data-ttu-id="6ef1f-143">스크립트/앱/모델/\*: 모델을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-143">Scripts/app/models/\*.js: Defines the models.</span></span>
- <span data-ttu-id="6ef1f-144">Scripts/app/views/\*: 뷰를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-144">Scripts/app/views/\*.js: Defines the views.</span></span>
- <span data-ttu-id="6ef1f-145">Scripts/app/controllers/\*: 컨트롤러를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-145">Scripts/app/controllers/\*.js: Defines the controllers.</span></span>
- <span data-ttu-id="6ef1f-146">스크립트/앱/경로, 스크립트/앱/라우터 .js: 경로를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-146">Scripts/app/routes, Scripts/app/router.js: Defines the routes.</span></span>
- <span data-ttu-id="6ef1f-147">Templates/\*. hbs: handlebars template을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-147">Templates/\*.hbs: Defines the handlebars templates.</span></span>

<span data-ttu-id="6ef1f-148">이러한 스크립트 중 일부를 좀 더 자세히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-148">Let's look at some of these scripts in more detail.</span></span>

## <a name="models"></a><span data-ttu-id="6ef1f-149">모델</span><span class="sxs-lookup"><span data-stu-id="6ef1f-149">Models</span></span>

<span data-ttu-id="6ef1f-150">모델은 스크립트/앱/모델 폴더에 정의 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-150">The models are defined in the Scripts/app/models folder.</span></span> <span data-ttu-id="6ef1f-151">TodoItem 및 todoList의 두 가지 모델 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-151">There are two model files: todoItem.js and todoList.js.</span></span>

<span data-ttu-id="6ef1f-152">**todo. node.js** 목록에 대 한 클라이언트 쪽 (브라우저) 모델을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-152">**todo.model.js** defines the client-side (browser) models for the to-do lists.</span></span> <span data-ttu-id="6ef1f-153">TodoItem 및 todoList의 두 가지 모델 클래스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-153">There are two model classes: todoItem and todoList.</span></span> <span data-ttu-id="6ef1f-154">Ember.js에서 모델은 DS의 서브 클래스입니다. 모델링.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-154">In Ember, models are subclasses of DS.Model.</span></span> <span data-ttu-id="6ef1f-155">모델에는 특성이 포함 된 속성이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-155">A model can have properties with attributes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample1.js)]

<span data-ttu-id="6ef1f-156">모델은 다른 모델에 대 한 관계를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-156">Models can define relationships to other models:</span></span>

[!code-css[Main](emberjs-template/samples/sample2.css)]

<span data-ttu-id="6ef1f-157">모델에는 다른 속성에 바인딩하는 계산 된 속성이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-157">Models can have computed properties that bind to other properties:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample3.js)]

<span data-ttu-id="6ef1f-158">모델에는 관찰 된 속성이 변경 될 때 호출 되는 관찰자 함수가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-158">Models can have observer functions, which are invoked when an observed property changes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample4.js)]

## <a name="views"></a><span data-ttu-id="6ef1f-159">뷰</span><span class="sxs-lookup"><span data-stu-id="6ef1f-159">Views</span></span>

<span data-ttu-id="6ef1f-160">뷰는 Scripts/app/views 폴더에 정의 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-160">The views are defined in the Scripts/app/views folder.</span></span> <span data-ttu-id="6ef1f-161">뷰는 응용 프로그램 UI에서 이벤트를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-161">A view translates events from the application UI.</span></span> <span data-ttu-id="6ef1f-162">이벤트 처리기는 컨트롤러 함수를 다시 호출 하거나 단순히 데이터 컨텍스트를 직접 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-162">An event handler can call back to controller functions, or simply call the data context directly.</span></span>

<span data-ttu-id="6ef1f-163">예를 들어 다음 코드는 views/TodoItemEditView에서 가져온 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-163">For example, the following code is from views/TodoItemEditView.js.</span></span> <span data-ttu-id="6ef1f-164">입력 텍스트 필드에 대 한 이벤트 처리를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-164">It defines the event handling for an input text field.</span></span>

[!code-javascript[Main](emberjs-template/samples/sample5.js)]

## <a name="controller"></a><span data-ttu-id="6ef1f-165">컨트롤러</span><span class="sxs-lookup"><span data-stu-id="6ef1f-165">Controller</span></span>

<span data-ttu-id="6ef1f-166">컨트롤러는 Scripts/app/controllers 폴더에 정의 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-166">The controllers are defined in the Scripts/app/controllers folder.</span></span> <span data-ttu-id="6ef1f-167">단일 모델을 나타내려면 `Ember.ObjectController`를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-167">To represent a single model, extend `Ember.ObjectController`:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample6.js)]

<span data-ttu-id="6ef1f-168">컨트롤러는 `Ember.ArrayController`확장 하 여 모델의 컬렉션을 나타낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-168">A controller can also represent a collection of models by extending `Ember.ArrayController`.</span></span> <span data-ttu-id="6ef1f-169">예를 들어 TodoListController은 `todoList` 개체의 배열을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-169">For example, the TodoListController represents an array of `todoList` objects.</span></span> <span data-ttu-id="6ef1f-170">컨트롤러는 todoList ID를 기준으로 내림차순으로 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-170">The controller sorts by todoList ID, in descending order:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample7.js)]

<span data-ttu-id="6ef1f-171">컨트롤러는 새 todoList를 만들어 배열에 추가 하는 `addTodoList`이라는 함수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-171">The controller defines a function named `addTodoList`, which creates a new todoList and adds it to the array.</span></span> <span data-ttu-id="6ef1f-172">이 함수를 호출 하는 방법을 확인 하려면 Templates 폴더에서 todoListTemplate 이라는 템플릿 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-172">To see how this function gets called, open the template file named todoListTemplate.html, in the Templates folder.</span></span> <span data-ttu-id="6ef1f-173">다음 템플릿 코드는 단추를 `addTodoList` 함수에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-173">The following template code binds a button to the `addTodoList` function:</span></span>

[!code-html[Main](emberjs-template/samples/sample8.html)]

<span data-ttu-id="6ef1f-174">또한 컨트롤러는 오류 메시지를 포함 하는 `error` 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-174">The controller also contains an `error` property, which holds an error message.</span></span> <span data-ttu-id="6ef1f-175">다음은 오류 메시지를 표시 하는 템플릿 코드입니다 (todoListTemplate에도 해당).</span><span class="sxs-lookup"><span data-stu-id="6ef1f-175">Here is the template code to display the error message (also in todoListTemplate.html):</span></span>

[!code-html[Main](emberjs-template/samples/sample9.html)]

## <a name="routes"></a><span data-ttu-id="6ef1f-176">경로</span><span class="sxs-lookup"><span data-stu-id="6ef1f-176">Routes</span></span>

<span data-ttu-id="6ef1f-177">Node.js는 표시 하 고, 응용 프로그램 상태를 설정 하 고, Url을 경로에 일치 시키는 기본 템플릿 및 경로를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-177">Router.js defines the routes and the default template to display, sets up application state, and matches URLs to routes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample10.js)]

<span data-ttu-id="6ef1f-178">TodoListRoute는 setupController 함수를 재정의 하 여 TodoListRoute에 대 한 데이터를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-178">TodoListRoute.js loads data for the TodoListRoute by overriding the setupController function:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample11.js)]

<span data-ttu-id="6ef1f-179">Ember.js는 명명 규칙을 사용 하 여 Url, 경로 이름, 컨트롤러 및 템플릿을 일치 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-179">Ember uses naming conventions to match URLs, route names, controllers, and templates.</span></span> <span data-ttu-id="6ef1f-180">자세한 내용은 EmberJS 설명서에서 [http://emberjs.com/guides/routing/defining-your-routes/](http://emberjs.com/guides/routing/defining-your-routes/) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-180">For more information, see [http://emberjs.com/guides/routing/defining-your-routes/](http://emberjs.com/guides/routing/defining-your-routes/) at the EmberJS documentation.</span></span>

## <a name="templates"></a><span data-ttu-id="6ef1f-181">템플릿</span><span class="sxs-lookup"><span data-stu-id="6ef1f-181">Templates</span></span>

<span data-ttu-id="6ef1f-182">Templates 폴더에는 다음 4 개의 템플릿이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-182">The Templates folder contains four templates:</span></span>

- <span data-ttu-id="6ef1f-183">응용 프로그램. hbs: 응용 프로그램이 시작 될 때 렌더링 되는 기본 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-183">application.hbs: The default template that is rendered when the application is started.</span></span>
- <span data-ttu-id="6ef1f-184">. hbs: "/about" 경로에 대 한 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-184">about.hbs: The template for the "/about" route.</span></span>
- <span data-ttu-id="6ef1f-185">index. hbs: 루트 "/" 경로에 대 한 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-185">index.hbs: The template for the root "/" route.</span></span>
- <span data-ttu-id="6ef1f-186">todoList: "/todo" 경로에 대 한 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-186">todoList.hbs: The template for the "/todo" route.</span></span>
- <span data-ttu-id="6ef1f-187">\_탐색 모음. hbs: 템플릿은 탐색 메뉴를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-187">\_navbar.hbs: The template defines the navigation menu.</span></span>

<span data-ttu-id="6ef1f-188">응용 프로그램 템플릿은 마스터 페이지 처럼 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-188">The application template acts like a master page.</span></span> <span data-ttu-id="6ef1f-189">여기에는 경로에 따라의 다른 템플릿을 삽입 하는 헤더, 바닥글 및 "{{콘센트가}}"가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-189">It contains a header, a footer, and an "{{outlet}}" to insert other templates in depending on the route.</span></span> <span data-ttu-id="6ef1f-190">Ember.js의 응용 프로그램 템플릿에 대 한 자세한 내용은 [http://guides.emberjs.com/v1.10.0/templates/the-application-template//](http://guides.emberjs.com/v1.10.0/templates/the-application-template/)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-190">For more information about application templates in Ember, see [http://guides.emberjs.com/v1.10.0/templates/the-application-template//](http://guides.emberjs.com/v1.10.0/templates/the-application-template/).</span></span>

<span data-ttu-id="6ef1f-191">"/TodoList" 템플릿에는 두 개의 루프 식이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-191">The "/todoList" template contains two loop expressions.</span></span> <span data-ttu-id="6ef1f-192">외부 루프가 `{{#each controller}}`되 고 내부 루프가 `{{#each todos}}`됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-192">The outside loop is `{{#each controller}}`, and the inside loop is `{{#each todos}}`.</span></span> <span data-ttu-id="6ef1f-193">다음 코드는 기본 제공 `Ember.Checkbox` 뷰, 사용자 지정 된 `App.TodoItemEditView`및 `deleteTodo` 작업 링크를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-193">The following code shows a built-in `Ember.Checkbox` view, a customized `App.TodoItemEditView`, and a link with a `deleteTodo` action.</span></span>

[!code-html[Main](emberjs-template/samples/sample12.html)]

<span data-ttu-id="6ef1f-194">Controllers/HtmlHelperExtensions. cs에 정의 된 `HtmlHelperExtensions` 클래스는 Web.config 파일에서 **debug** 가 **true** 로 설정 된 경우 템플릿 파일을 캐시 하 고 삽입 하는 도우미 함수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-194">The `HtmlHelperExtensions` class, defined in Controllers/HtmlHelperExtensions.cs, defines a helper function to cache and insert template files when **debug** is set to **true** in the Web.config file.</span></span> <span data-ttu-id="6ef1f-195">이 함수는 Views/Home/ASP.NET에 정의 된 MVC 뷰 파일에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-195">This function is called from the ASP.NET MVC view file defined in Views/Home/App.cshtml:</span></span>

[!code-cshtml[Main](emberjs-template/samples/sample13.cshtml)]

<span data-ttu-id="6ef1f-196">인수 없이 호출 되는 함수는 템플릿 폴더의 모든 템플릿 파일을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-196">Called with no arguments, the function renders all of the template files in the Templates folder.</span></span> <span data-ttu-id="6ef1f-197">하위 폴더 또는 특정 템플릿 파일을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-197">You can also specify a subfolder or a specific template file.</span></span>

<span data-ttu-id="6ef1f-198">Web.config에서 **debug** 가 **false** 인 경우 응용 프로그램은 번들 항목인 "~/bundles/templates"를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-198">When **debug** is **false** in Web.config, the application includes the bundle item "~/bundles/templates".</span></span> <span data-ttu-id="6ef1f-199">이 번들 항목은 Handlebars 컴파일러 라이브러리를 사용 하 여 BundleConfig.cs에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ef1f-199">This bundle item is added in BundleConfig.cs, using the Handlebars compiler library:</span></span>

[!code-csharp[Main](emberjs-template/samples/sample14.cs)]
