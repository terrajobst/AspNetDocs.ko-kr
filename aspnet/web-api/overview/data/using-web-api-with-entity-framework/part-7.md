---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-7
title: 보기 (UI) 만들기 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: b2445062-a1fe-4133-8994-f510280f6d9a
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-7
msc.type: authoredcontent
ms.openlocfilehash: 62c4523c2c6fb399cfbc3716309a1379996d601c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448985"
---
# <a name="create-the-view-ui"></a><span data-ttu-id="98bf8-102">보기(UI) 만들기</span><span class="sxs-lookup"><span data-stu-id="98bf8-102">Create the View (UI)</span></span>

<span data-ttu-id="98bf8-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="98bf8-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="98bf8-104">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="98bf8-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="98bf8-105">이 섹션에서는 앱에 대 한 HTML 정의를 시작 하 고 HTML과 뷰 모델 간에 데이터 바인딩을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="98bf8-105">In this section, you will start to define the HTML for the app, and add data binding between the HTML and the view model.</span></span>

<span data-ttu-id="98bf8-106">파일 Views/Home/Index. cshtml를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="98bf8-106">Open the file Views/Home/Index.cshtml.</span></span> <span data-ttu-id="98bf8-107">해당 파일의 전체 내용을 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="98bf8-107">Replace the entire contents of that file with the following.</span></span>

[!code-cshtml[Main](part-7/samples/sample1.cshtml)]

<span data-ttu-id="98bf8-108">대부분의 `div` 요소는 [부트스트랩](http://getbootstrap.com/) 스타일 지정에 대 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="98bf8-108">Most of the `div` elements are there for [Bootstrap](http://getbootstrap.com/) styling.</span></span> <span data-ttu-id="98bf8-109">중요 한 요소는 `data-bind` 특성이 있는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="98bf8-109">The important elements are the ones with `data-bind` attributes.</span></span> <span data-ttu-id="98bf8-110">이 특성은 HTML을 뷰 모델에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="98bf8-110">This attribute links the HTML to the view model.</span></span>

<span data-ttu-id="98bf8-111">다음은 그 예입니다.</span><span class="sxs-lookup"><span data-stu-id="98bf8-111">For example:</span></span>

[!code-html[Main](part-7/samples/sample2.html)]

<span data-ttu-id="98bf8-112">이 예제에서 &quot;&quot; 바인딩을 `text`하면 `<p>` 요소가 뷰 모델에서 `error` 속성의 값을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="98bf8-112">In this example, the &quot;`text`&quot; binding causes the `<p>` element to show the value of the `error` property from the view model.</span></span> <span data-ttu-id="98bf8-113">`error`은 `ko.observable`으로 선언 됨을 기억 하십시오.</span><span class="sxs-lookup"><span data-stu-id="98bf8-113">Recall that `error` was declared as a `ko.observable`:</span></span>

[!code-javascript[Main](part-7/samples/sample3.js)]

<span data-ttu-id="98bf8-114">`error`에 새 값이 할당 될 때마다 녹아웃은 `<p>` 요소의 텍스트를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="98bf8-114">Whenever a new value is assigned to `error`, Knockout updates the text in the `<p>` element.</span></span>

<span data-ttu-id="98bf8-115">`foreach` 바인딩은 `books` 배열의 콘텐츠를 반복 하도록 녹아웃에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="98bf8-115">The `foreach` binding tells Knockout to loop through the contents of the `books` array.</span></span> <span data-ttu-id="98bf8-116">배열에 있는 각 항목에 대해 녹아웃은 새 &lt;li&gt; 요소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98bf8-116">For each item in the array, Knockout creates a new &lt;li&gt; element.</span></span> <span data-ttu-id="98bf8-117">`foreach` 컨텍스트 내의 바인딩은 배열 항목의 속성을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="98bf8-117">Bindings inside the context of the `foreach` refer to properties on the array item.</span></span> <span data-ttu-id="98bf8-118">다음은 그 예입니다.</span><span class="sxs-lookup"><span data-stu-id="98bf8-118">For example:</span></span>

[!code-html[Main](part-7/samples/sample4.html)]

<span data-ttu-id="98bf8-119">여기서 `text` 바인딩은 각 책의 Author 속성을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="98bf8-119">Here the `text` binding reads the Author property of each book.</span></span>

<span data-ttu-id="98bf8-120">지금 응용 프로그램을 실행 하는 경우 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98bf8-120">If you run the application now, it should look like this:</span></span>

![](part-7/_static/image1.png)

<span data-ttu-id="98bf8-121">페이지를 로드 한 후 책 목록이 비동기적으로 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98bf8-121">The list of books loads asynchronously, after the page loads.</span></span> <span data-ttu-id="98bf8-122">현재 &quot;세부 정보&quot; 링크가 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98bf8-122">Right now, the &quot;Details&quot; links are not functional.</span></span> <span data-ttu-id="98bf8-123">다음 섹션에서이 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="98bf8-123">We'll add this functionality in the next section.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="98bf8-124">[이전](part-6.md)
> [다음](part-8.md)</span><span class="sxs-lookup"><span data-stu-id="98bf8-124">[Previous](part-6.md)
[Next](part-8.md)</span></span>
