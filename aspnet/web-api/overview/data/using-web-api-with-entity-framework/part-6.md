---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-6
title: JavaScript 클라이언트 만들기 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 20360326-b123-4b1e-abae-1d350edf4ce4
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-6
msc.type: authoredcontent
ms.openlocfilehash: 74f2cc4e5e401d690042b05b028dfc0c46ae282a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504725"
---
# <a name="create-the-javascript-client"></a><span data-ttu-id="14511-102">JavaScript 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="14511-102">Create the JavaScript Client</span></span>

<span data-ttu-id="14511-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="14511-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="14511-104">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="14511-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="14511-105">이 섹션에서는 HTML, JavaScript 및 [녹아웃 .js](http://knockoutjs.com/) 라이브러리를 사용 하 여 응용 프로그램에 대 한 클라이언트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14511-105">In this section, you will create the client for the application, using HTML, JavaScript, and the [Knockout.js](http://knockoutjs.com/) library.</span></span> <span data-ttu-id="14511-106">다음 단계에서 클라이언트 앱을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="14511-106">We'll build the client app in stages:</span></span>

- <span data-ttu-id="14511-107">책 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="14511-107">Showing a list of books.</span></span>
- <span data-ttu-id="14511-108">책 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="14511-108">Showing a book detail.</span></span>
- <span data-ttu-id="14511-109">새 책을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="14511-109">Adding a new book.</span></span>

<span data-ttu-id="14511-110">녹아웃 라이브러리는 MVVM (모델-뷰-ViewModel) 패턴을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="14511-110">The Knockout library uses the Model-View-ViewModel (MVVM) pattern:</span></span>

- <span data-ttu-id="14511-111">**모델** 은 비즈니스 도메인 (이 경우 책 및 저자)의 데이터를 서버 쪽으로 표현한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="14511-111">The **model** is the server-side representation of the data in the business domain (in our case, books and authors).</span></span>
- <span data-ttu-id="14511-112">**뷰** 는 프레젠테이션 계층 (HTML)입니다.</span><span class="sxs-lookup"><span data-stu-id="14511-112">The **view** is the presentation layer (HTML).</span></span>
- <span data-ttu-id="14511-113">**뷰 모델** 은 모델을 보유 하는 JavaScript 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="14511-113">The **view model** is a JavaScript object that holds the models.</span></span> <span data-ttu-id="14511-114">뷰 모델은 UI의 코드 추상화입니다.</span><span class="sxs-lookup"><span data-stu-id="14511-114">The view model is a code abstraction of the UI.</span></span> <span data-ttu-id="14511-115">HTML 표현에 대해 알지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="14511-115">It has no knowledge of the HTML representation.</span></span> <span data-ttu-id="14511-116">대신, 책&quot;목록 &quot;와 같이 뷰의 추상 기능을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="14511-116">Instead, it represents abstract features of the view, such as &quot;a list of books&quot;.</span></span>

<span data-ttu-id="14511-117">뷰 모델에 대 한 데이터 바인딩된 뷰입니다.</span><span class="sxs-lookup"><span data-stu-id="14511-117">The view is data-bound to the view model.</span></span> <span data-ttu-id="14511-118">뷰 모델에 대 한 업데이트는 뷰에 자동으로 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="14511-118">Updates to the view model are automatically reflected in the view.</span></span> <span data-ttu-id="14511-119">뷰 모델은 단추 클릭과 같은 보기 에서도 이벤트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="14511-119">The view model also gets events from the view, such as button clicks.</span></span>

![](part-6/_static/image1.png)

<span data-ttu-id="14511-120">이 방법을 사용 하면 코드를 다시 작성 하지 않고도 바인딩을 변경할 수 있으므로 앱의 레이아웃 및 UI를 쉽게 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14511-120">This approach makes it easy to change the layout and UI of your app, because you can change the bindings, without rewriting any code.</span></span> <span data-ttu-id="14511-121">예를 들어 `<ul>`항목의 목록을 표시 한 다음 나중에 테이블로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14511-121">For example, you might show a list of items as a `<ul>`, then change it later to a table.</span></span>

## <a name="add-the-knockout-library"></a><span data-ttu-id="14511-122">녹아웃 라이브러리 추가</span><span class="sxs-lookup"><span data-stu-id="14511-122">Add the Knockout Library</span></span>

<span data-ttu-id="14511-123">Visual Studio의 **도구** 메뉴에서 **NuGet 패키지 관리자**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="14511-123">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**.</span></span> <span data-ttu-id="14511-124">그런 후 **패키지 관리자 콘솔**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14511-124">Then select **Package Manager Console**.</span></span> <span data-ttu-id="14511-125">패키지 관리자 콘솔 창에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="14511-125">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](part-6/samples/sample1.cmd)]

<span data-ttu-id="14511-126">이 명령은 녹아웃 파일을 Scripts 폴더에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="14511-126">This command adds the Knockout files to the Scripts folder.</span></span>

## <a name="create-the-view-model"></a><span data-ttu-id="14511-127">뷰 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="14511-127">Create the View Model</span></span>

<span data-ttu-id="14511-128">Scripts 폴더에 node.js 라는 JavaScript 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="14511-128">Add a JavaScript file named app.js to the Scripts folder.</span></span> <span data-ttu-id="14511-129">솔루션 탐색기에서 Scripts 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 선택한 다음 **JavaScript 파일**을 선택 합니다. 다음 코드를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="14511-129">(In Solution Explorer, right-click the Scripts folder, select **Add**, then select **JavaScript File**.) Paste in the following code:</span></span>

[!code-javascript[Main](part-6/samples/sample2.js)]

<span data-ttu-id="14511-130">녹아웃에서 `observable` 클래스는 데이터 바인딩을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="14511-130">In Knockout, the `observable` class enables data-binding.</span></span> <span data-ttu-id="14511-131">관찰 가능의 내용이 변경 되 면 관찰 가능 개체는 모든 데이터 바인딩된 컨트롤에 자동으로 알리고 자체적으로 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14511-131">When the contents of an observable change, the observable notifies all of the data-bound controls, so they can update themselves.</span></span> <span data-ttu-id="14511-132">`observableArray` 클래스는 *관찰*가능의 배열 버전입니다. 먼저 보기 모델에는 두 가지 관찰 가능 개체 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14511-132">(The `observableArray` class is the array version of *observable*.) To start with, our view model has two observables:</span></span>

- <span data-ttu-id="14511-133">`books`은 책 목록을 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="14511-133">`books` holds the list of books.</span></span>
- <span data-ttu-id="14511-134">AJAX 호출이 실패 하면 `error`에 오류 메시지가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="14511-134">`error` contains an error message if an AJAX call fails.</span></span>

<span data-ttu-id="14511-135">`getAllBooks` 메서드는 서적 목록을 가져오는 AJAX 호출을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="14511-135">The `getAllBooks` method makes an AJAX call to get the list of books.</span></span> <span data-ttu-id="14511-136">그런 다음 `books` 배열에 결과를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="14511-136">Then it pushes the result onto the `books` array.</span></span>

<span data-ttu-id="14511-137">`ko.applyBindings` 메서드는 녹아웃 라이브러리의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="14511-137">The `ko.applyBindings` method is part of the Knockout library.</span></span> <span data-ttu-id="14511-138">뷰 모델을 매개 변수로 사용 하 고 데이터 바인딩을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="14511-138">It takes the view model as a parameter and sets up the data binding.</span></span>

## <a name="add-a-script-bundle"></a><span data-ttu-id="14511-139">스크립트 번들 추가</span><span class="sxs-lookup"><span data-stu-id="14511-139">Add a Script Bundle</span></span>

<span data-ttu-id="14511-140">번들은 여러 파일을 단일 파일로 쉽게 결합 하거나 묶을 수 있는 ASP.NET 4.5의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="14511-140">Bundling is a feature in ASP.NET 4.5 that makes it easy to combine or bundle multiple files into a single file.</span></span> <span data-ttu-id="14511-141">묶음은 서버에 대 한 요청 수를 줄여 페이지 로드 시간을 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14511-141">Bundling reduces the number of requests to the server, which can improve page load time.</span></span>

<span data-ttu-id="14511-142">File App\_Start/BundleConfig를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="14511-142">Open the file App\_Start/BundleConfig.cs.</span></span> <span data-ttu-id="14511-143">RegisterBundles 메서드에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="14511-143">Add the following code to the RegisterBundles method.</span></span>

[!code-csharp[Main](part-6/samples/sample3.cs)]

> [!div class="step-by-step"]
> <span data-ttu-id="14511-144">[이전](part-5.md)
> [다음](part-7.md)</span><span class="sxs-lookup"><span data-stu-id="14511-144">[Previous](part-5.md)
[Next](part-7.md)</span></span>
