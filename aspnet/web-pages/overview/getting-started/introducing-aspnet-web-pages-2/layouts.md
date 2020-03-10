---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
title: ASP.NET 웹 페이지 소개-일관 된 레이아웃 만들기 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 레이아웃을 사용 하 여 ASP.NET 웹 페이지를 사용 하는 사이트의 페이지에 대해 일관 된 모양을 만드는 방법을 보여 줍니다. 다음을 완료 했다고 가정 합니다.
ms.author: riande
ms.date: 05/28/2015
ms.assetid: c85ec591-f8d7-4882-b763-de6ab9f3df7a
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
msc.type: authoredcontent
ms.openlocfilehash: 678eb7089e95e3d221d6b2d82034a62aefa75757
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422747"
---
# <a name="introducing-aspnet-web-pages---creating-a-consistent-layout"></a><span data-ttu-id="f394d-104">ASP.NET 웹 페이지 소개-일관적인 레이아웃 만들기</span><span class="sxs-lookup"><span data-stu-id="f394d-104">Introducing ASP.NET Web Pages - Creating a Consistent Layout</span></span>

<span data-ttu-id="f394d-105">만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="f394d-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="f394d-106">이 자습서에서는 *레이아웃* 을 사용 하 여 ASP.NET 웹 페이지를 사용 하는 사이트의 페이지에 대해 일관 된 모양을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-106">This tutorial shows you how to use *layouts* to create a consistent look for the pages on a site that uses ASP.NET Web Pages.</span></span> <span data-ttu-id="f394d-107">[ASP.NET 웹 페이지에서 데이터베이스 데이터를 삭제](https://go.microsoft.com/fwlink/?LinkId=251584)하 여 계열을 완료 했다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-107">It assumes you have completed the series through [Deleting Database Data in ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251584).</span></span>
> 
> <span data-ttu-id="f394d-108">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="f394d-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="f394d-109">레이아웃 페이지는 무엇 인가요?</span><span class="sxs-lookup"><span data-stu-id="f394d-109">What a layout page is.</span></span>
> - <span data-ttu-id="f394d-110">레이아웃 페이지를 동적 콘텐츠와 결합 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-110">How to combine layout pages with dynamic content.</span></span>
> - <span data-ttu-id="f394d-111">레이아웃 페이지에 값을 전달 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-111">How to pass values to a layout page.</span></span>

## <a name="about-layouts"></a><span data-ttu-id="f394d-112">레이아웃 정보</span><span class="sxs-lookup"><span data-stu-id="f394d-112">About Layouts</span></span>

<span data-ttu-id="f394d-113">지금까지 만든 페이지는 모두 완전 한 독립 실행형 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-113">The pages you've created so far have all been complete, standalone pages.</span></span> <span data-ttu-id="f394d-114">모두 동일한 사이트에 속하지만 공통 요소나 표준 모양을 갖지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-114">They all belong to the same site, but they don't have any common elements or a standard look.</span></span>

<span data-ttu-id="f394d-115">대부분의 사이트에는 일관 된 모양과 레이아웃이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-115">Most sites do have a consistent look and layout.</span></span> <span data-ttu-id="f394d-116">예를 들어 [Microsoft.com/web](https://www.microsoft.com/web/) 사이트로 이동 하 여이를 살펴보면 페이지가 모두 전체 레이아웃 및 시각적 테마를 준수 하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-116">For example, if you go to the [Microsoft.com/web](https://www.microsoft.com/web/) site and look around, you see that the pages all adhere to an overall layout and to a visual theme:</span></span>

![머리글, 탐색 영역, 콘텐츠 영역 및 바닥글의 레이아웃을 표시 하는 Microsoft.com/web 사이트 페이지](layouts/_static/image1.png)

<span data-ttu-id="f394d-118">이 레이아웃을 만드는 *비효율적인* 방법은 각 페이지에 개별적으로 머리글, 탐색 모음 및 바닥글을 정의 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-118">An *inefficient* way to create this layout would be to define a header, navigation bar, and footer separately on each of your pages.</span></span> <span data-ttu-id="f394d-119">매번 동일한 태그를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-119">You'd be duplicating the same markup each time.</span></span> <span data-ttu-id="f394d-120">바닥글 업데이트와 같은 항목을 변경 하려면 각 페이지를 별도로 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-120">If you wanted to change something (for example, update the footer), you'd have to change each page separately.</span></span>

<span data-ttu-id="f394d-121">*레이아웃 페이지가* 제공 되는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-121">That's where *layout pages* come in.</span></span> <span data-ttu-id="f394d-122">ASP.NET 웹 페이지에서 사이트의 페이지에 대 한 전체 컨테이너를 제공 하는 레이아웃 페이지를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-122">In ASP.NET Web Pages, you can define a layout page that provides an overall container for pages on your site.</span></span> <span data-ttu-id="f394d-123">예를 들어 레이아웃 페이지에는 머리글, 탐색 영역 및 바닥글을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-123">For example, the layout page can contain the header, navigation area, and footer.</span></span> <span data-ttu-id="f394d-124">레이아웃 페이지에는 주 콘텐츠가 이동 하는 자리 표시 자가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-124">The layout page includes a placeholder where the main content goes.</span></span>

<span data-ttu-id="f394d-125">그런 다음 해당 페이지에 대 한 코드와 태그를 포함 하는 개별 콘텐츠 페이지를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-125">You can then define individual content pages that contain the markup and the code for only that page.</span></span> <span data-ttu-id="f394d-126">콘텐츠 페이지가 완전 한 HTML 페이지가 될 필요는 없습니다. `<body>` 요소가 없어도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-126">Content pages don't have to be complete HTML pages; they don't even have to have a `<body>` element.</span></span> <span data-ttu-id="f394d-127">또한 콘텐츠를 표시 하려는 레이아웃 페이지를 ASP.NET 알려 주는 코드 줄이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-127">They also have a line of code that tells ASP.NET what layout page you want to display the content in.</span></span> <span data-ttu-id="f394d-128">이 관계가 작동 하는 방식을 대략적으로 보여 주는 그림은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-128">Here's a picture that shows roughly how this relationship works:</span></span>

![두 콘텐츠 페이지와 이러한 페이지에 맞는 레이아웃 페이지가 표시 된 개념적 다이어그램](layouts/_static/image2.png)

<span data-ttu-id="f394d-130">이러한 상호 작용은 동작에서 볼 때 쉽게 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-130">This interaction is easy to understand when you see it in action.</span></span> <span data-ttu-id="f394d-131">이 자습서에서는 레이아웃을 사용 하도록 동영상 페이지를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-131">In this tutorial, you'll change your movies pages to use a layout.</span></span>

## <a name="adding-a-layout-page"></a><span data-ttu-id="f394d-132">레이아웃 페이지 추가</span><span class="sxs-lookup"><span data-stu-id="f394d-132">Adding a Layout Page</span></span>

<span data-ttu-id="f394d-133">먼저 머리글, 바닥글 및 주 콘텐츠에 대 한 영역을 사용 하 여 일반적인 페이지 레이아웃을 정의 하는 레이아웃 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-133">You'll start by creating a layout page that defines a typical page layout with a header, footer, and an area for the main content.</span></span> <span data-ttu-id="f394d-134">*\_* web\ststststststststststststststststststststststststst</span><span class="sxs-lookup"><span data-stu-id="f394d-134">In the WebPagesMovies site, add a CSHTML page named *\_Layout.cshtml*.</span></span>

<span data-ttu-id="f394d-135">선행 밑줄 (`_`) 문자는 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-135">The leading underscore ( `_` ) character is significant.</span></span> <span data-ttu-id="f394d-136">페이지 이름이 밑줄로 시작 하는 경우 ASP.NET는 해당 페이지를 브라우저에 직접 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-136">If a page's name starts with an underscore, ASP.NET won't directly send that page to the browser.</span></span> <span data-ttu-id="f394d-137">이 규칙을 사용 하면 사이트에 필요한 페이지를 정의할 수 있지만 사용자가 직접 요청할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-137">This convention lets you define pages that are required for your site but that users shouldn't be able to request directly.</span></span>

<span data-ttu-id="f394d-138">페이지의 내용을 다음과 같이 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-138">Replace the content in the page with the following:</span></span>

[!code-html[Main](layouts/samples/sample1.html)]

<span data-ttu-id="f394d-139">여기에서 볼 수 있듯이이 태그는 `<div>` 요소를 사용 하 여 페이지에 세 개의 섹션을 정의 하는 HTML 뿐 이며 세 개의 섹션을 저장할 `<div>` 요소가 하나 더 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-139">As you can see, this markup is just HTML that uses `<div>` elements to define three sections in the page plus one more `<div>` element to hold the three sections.</span></span> <span data-ttu-id="f394d-140">바닥글에는 약간의 Razor 코드 (`@DateTime.Now.Year`)가 포함 되어 있습니다 .이 코드는 페이지의 해당 위치에서 현재 연도를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-140">The footer contains a bit of Razor code: `@DateTime.Now.Year`, which will render the current year at that location in the page.</span></span>

<span data-ttu-id="f394d-141">*동영상 .css*이라는 스타일 시트에 대 한 링크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-141">Notice that there's a link to a style sheet named *Movies.css*.</span></span> <span data-ttu-id="f394d-142">스타일 시트는 요소의 물리적 레이아웃에 대 한 세부 정보를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-142">The style sheet is where the details of the physical layout of the elements will be defined.</span></span> <span data-ttu-id="f394d-143">잠시 후에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-143">You'll create that in a moment.</span></span>

<span data-ttu-id="f394d-144">이 *\_레이아웃* 에서 유일 하지 않은 기능은 `@Render.Body()` 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-144">The only unusual feature in this *\_Layout.cshtml* page is the `@Render.Body()` line.</span></span> <span data-ttu-id="f394d-145">이 레이아웃을 다른 페이지와 병합할 때 콘텐츠가 이동 하는 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-145">That's the placeholder where the content will go when this layout is merged with another page.</span></span>

## <a name="adding-a-css-file"></a><span data-ttu-id="f394d-146">.Css 파일 추가</span><span class="sxs-lookup"><span data-stu-id="f394d-146">Adding a .css File</span></span>

<span data-ttu-id="f394d-147">페이지에서 요소의 실제 정렬 (즉, 모양)을 정의 하는 기본 방법은 CSS (css 스타일 시트) 규칙을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-147">The preferred way to define the actual arrangement (that is, appearance) of elements on the page is to use cascading style sheet (CSS) rules.</span></span> <span data-ttu-id="f394d-148">따라서 새 레이아웃에 대 한 규칙이 있는 *.css* 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-148">So you'll create a *.css* file that has the rules for your new layout.</span></span>

<span data-ttu-id="f394d-149">WebMatrix에서 사이트의 루트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-149">In WebMatrix, select the root of your site.</span></span> <span data-ttu-id="f394d-150">그런 다음 리본의 **파일** 탭에서 **새로 만들기** 단추 아래의 화살표를 클릭 한 다음 **새 폴더**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-150">Then in the **Files** tab of the ribbon, click the arrow under the **New** button and then click **New Folder**.</span></span>

![리본 메뉴의 새로 만들기 아래에 있는 ' 새 폴더 ' 옵션입니다.](layouts/_static/image3.png)

<span data-ttu-id="f394d-152">새 폴더의 이름을 *스타일*로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-152">Name the new folder *Styles*.</span></span>

![새 폴더 ' 스타일 ' 이름 지정](layouts/_static/image4.png)

<span data-ttu-id="f394d-154">새 *스타일* 폴더 내에서 *동영상이 .css*인 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-154">Inside the new *Styles* folder, create a file named *Movies.css*.</span></span>

![새 동영상 .css 파일 만들기](layouts/_static/image5.png)

<span data-ttu-id="f394d-156">새 *.css* 파일의 내용을 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-156">Replace the contents of the new *.css* file with the following:</span></span>

[!code-css[Main](layouts/samples/sample2.css)]

<span data-ttu-id="f394d-157">이러한 CSS 규칙에 대해서는 두 가지를 제외 하 고는 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-157">We won't say much about these CSS rules, except to note two things.</span></span> <span data-ttu-id="f394d-158">하나는 글꼴과 크기를 설정 하는 것 외에도 규칙에서 절대 위치를 사용 하 여 머리글, 바닥글 및 주 콘텐츠 영역의 위치를 설정 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-158">One is that in addition to setting fonts and sizes, the rules use absolute positioning to establish the location of the header, footer, and main content area.</span></span> <span data-ttu-id="f394d-159">CSS에 위치를 처음 접하는 경우 W3Schools 사이트에서 [Css 위치 지정](http://www.w3schools.com/css/css_positioning.asp) 자습서를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-159">If you're new to positioning in CSS, you can read the [CSS Positioning](http://www.w3schools.com/css/css_positioning.asp) tutorial at the W3Schools site.</span></span>

<span data-ttu-id="f394d-160">그 밖의 다른 점은 원래 *동영상. cshtml* 파일에 개별적으로 정의 된 스타일 규칙을 복사 했다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-160">The other thing to note is that at the bottom, we've copied the style rules that were originally defined individually in the *Movies.cshtml* file.</span></span> <span data-ttu-id="f394d-161">이러한 규칙은 ASP.NET 웹 페이지 자습서를 [사용 하 여 데이터를 표시 하](https://go.microsoft.com/fwlink/?LinkId=251580) 는 방법을 소개 하 여 테이블에 줄무늬를 추가한 `WebGrid` 도우미 렌더링 태그를 만드는 데 사용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-161">These rules were used in the [Introduction to Displaying Data by Using ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251580) tutorial to make the `WebGrid` helper render markup that added stripes to the table.</span></span> <span data-ttu-id="f394d-162">스타일 정의에 *.css* 파일을 사용 하려는 경우 전체 사이트에 대 한 스타일 규칙을 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-162">(If you're going to use a *.css* file for style definitions, you might as well put the style rules for the whole site in it.)</span></span>

## <a name="updating-the-movies-file-to-use-the-layout"></a><span data-ttu-id="f394d-163">레이아웃을 사용 하도록 동영상 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="f394d-163">Updating the Movies File to Use the Layout</span></span>

<span data-ttu-id="f394d-164">이제 사이트에서 기존 파일을 업데이트 하 여 새 레이아웃을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-164">Now you can update the existing files in your site to use the new layout.</span></span> <span data-ttu-id="f394d-165">*영화 cshtml* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-165">Open the *Movies.cshtml* file.</span></span> <span data-ttu-id="f394d-166">맨 위에 있는 코드의 첫 번째 줄에 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-166">At the top, as the first line of code, add the following:</span></span>

[!code-csharp[Main](layouts/samples/sample3.cs)]

<span data-ttu-id="f394d-167">이제 페이지는 다음과 같은 방식으로 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-167">The page now starts out this way:</span></span>

[!code-cshtml[Main](layouts/samples/sample4.cshtml?highlight=2)]

<span data-ttu-id="f394d-168">이 한 줄의 코드는 *동영상* 페이지가 실행 될 때 *\_Layout. cshtml* 파일과 병합 되어야 한다는 것을 ASP.NET에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-168">This one line of code tells ASP.NET that when the *Movies* page runs, it should be merged with the *\_Layout.cshtml* file.</span></span>

<span data-ttu-id="f394d-169">이제 *동영상과* 파일은 레이아웃 페이지를 사용 하므로 *\_layout* 파일에 의해 처리 되는 *동영상. cshtml* 페이지에서 태그를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-169">Since the *Movies.cshtml* file now uses a layout page, you can remove the markup from the *Movies.cshtml* page that's taken care of by the *\_Layout.cshtml* file.</span></span> <span data-ttu-id="f394d-170">`<!DOCTYPE>`, `<html>`및 `<body>` 여는 태그와 닫는 태그를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-170">Take out the `<!DOCTYPE>`, `<html>`, and `<body>` opening and closing tags.</span></span> <span data-ttu-id="f394d-171">이제 *.css* 파일에 해당 규칙이 있기 때문에 표의 스타일 규칙을 포함 하는 전체 `<head>` 요소 및 해당 내용을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-171">Take out the entire `<head>` element and its contents, which includes the style rules for the grid, since you've now got those rules in a *.css* file.</span></span> <span data-ttu-id="f394d-172">현재 `<h1>` 요소를 `<h2>` 요소로 변경 합니다. 레이아웃 페이지에 `<h1>` 요소가 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-172">While you're at it, change the existing `<h1>` element to an `<h2>` element; you have an `<h1>` element in the layout page already.</span></span> <span data-ttu-id="f394d-173">`<h2>` 텍스트를 "동영상 나열"으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-173">Change the `<h2>` text to "List Movies".</span></span>

<span data-ttu-id="f394d-174">일반적으로 콘텐츠 페이지에서 이러한 종류의 변경 작업을 수행 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-174">Normally you wouldn't have to make these sorts of changes in a content page.</span></span> <span data-ttu-id="f394d-175">레이아웃 페이지를 사용 하 여 사이트를 시작 하는 경우 이러한 모든 요소를 시작 하지 않고 콘텐츠 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-175">When you start your site out with a layout page, you create content pages without all these elements to begin with.</span></span> <span data-ttu-id="f394d-176">그러나이 경우에는 독립 실행형 페이지를 레이아웃을 사용 하는 것으로 변환 하는 것이 좋습니다. 따라서 정리가 약간 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-176">In this case, though, you're converting a standalone page to one that uses a layout, so there's a bit of cleanup.</span></span>

<span data-ttu-id="f394d-177">작업이 완료 되 면 *동영상과* 페이지는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-177">When you're finished, the *Movies.cshtml* page will look like the following:</span></span>

[!code-cshtml[Main](layouts/samples/sample5.cshtml)]

### <a name="testing-the-layout"></a><span data-ttu-id="f394d-178">레이아웃 테스트</span><span class="sxs-lookup"><span data-stu-id="f394d-178">Testing the Layout</span></span>

<span data-ttu-id="f394d-179">이제 레이아웃이 어떻게 표시 되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-179">Now you can see what the layout looks like.</span></span> <span data-ttu-id="f394d-180">WebMatrix에서 *동영상과* 페이지를 마우스 오른쪽 단추로 클릭 하 고 **브라우저에서 시작**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-180">In WebMatrix, right-click the *Movies.cshtml* page and select **Launch in browser**.</span></span> <span data-ttu-id="f394d-181">브라우저에 페이지가 표시 되 면 페이지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-181">When the browser displays the page, it looks like this page:</span></span>

![레이아웃을 사용 하 여 렌더링 된 동영상 페이지](layouts/_static/image6.png)

<span data-ttu-id="f394d-183">ASP.NET가 영화의 콘텐츠를 *\_레이아웃* 에 병합 했습니다 .이 페이지는 `RenderBody` 메서드가 인 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-183">ASP.NET has merged the content of the Movies.cshtml page into the *\_Layout.cshtml* page right where the `RenderBody` method is.</span></span> <span data-ttu-id="f394d-184">물론 *\_레이아웃* 은 페이지의 모양을 정의 하는 *.css* 파일을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-184">And of course the *\_Layout.cshtml* page references a *.css* file that defines the look of the page.</span></span>

## <a name="updating-the-addmovie-page-to-use-the-layout"></a><span data-ttu-id="f394d-185">레이아웃을 사용 하도록 AddMovie 페이지 업데이트</span><span class="sxs-lookup"><span data-stu-id="f394d-185">Updating the AddMovie Page to Use the Layout</span></span>

<span data-ttu-id="f394d-186">레이아웃의 실제 혜택은 사이트의 모든 페이지에 사용할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-186">The real benefit of layouts is that you can use them for all the pages in your site.</span></span> <span data-ttu-id="f394d-187">*Addmovie. cshtml* 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-187">Open the *AddMovie.cshtml* page.</span></span>

<span data-ttu-id="f394d-188">*Addmovie* 페이지에는 유효성 검사 오류 메시지의 모양을 정의 하는 CSS 규칙이 원래 있던 것을 기억할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-188">You might remember that the *AddMovie.cshtml* page originally had some CSS rules in it to define the look of validation error messages.</span></span> <span data-ttu-id="f394d-189">이제 사이트에 대 한 *.css* 파일이 있으므로 해당 규칙을 *.css* 파일로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-189">Since you have a *.css* file for your site now, you can move those rules to the *.css* file.</span></span> <span data-ttu-id="f394d-190">*Addmovie* 파일에서 제거 하 고 *동영상 .css* 파일의 아래쪽에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-190">Remove them from the *AddMovie.cshtml* file and add them to the bottom of the *Movies.css* file.</span></span> <span data-ttu-id="f394d-191">다음 규칙을 이동 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-191">You are moving the following rules:</span></span>

[!code-css[Main](layouts/samples/sample6.css)]

<span data-ttu-id="f394d-192">이제는 *Addmovie* 에서 동일한 종류의 변경 내용을 적용 합니다. cshtml를 사용 하는 *경우, 이제* 는 `Layout="~/_Layout.cshtml;` 추가 하 고 HTML 태그는 불필요 하 게 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-192">Now make the same sorts of changes in *AddMovie.cshtml* that you did for *Movies.cshtml* — add `Layout="~/_Layout.cshtml;` and remove the HTML markup that's now extraneous.</span></span> <span data-ttu-id="f394d-193">`<h1>` 요소를 `<h2>`변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-193">Change the `<h1>` element to `<h2>`.</span></span> <span data-ttu-id="f394d-194">완료 되 면 페이지는 다음 예와 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-194">When you're done, the page will look like this example:</span></span>

[!code-cshtml[Main](layouts/samples/sample7.cshtml)]

<span data-ttu-id="f394d-195">페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-195">Run the page.</span></span> <span data-ttu-id="f394d-196">이제 다음 그림과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-196">Now it looks like this illustration:</span></span>

![레이아웃을 사용 하 여 렌더링 된 ' 동영상 추가 ' 페이지](layouts/_static/image7.png)

<span data-ttu-id="f394d-198">사이트의 페이지 ( *Editmovie. cshtml* 및 *DeleteMovie*)에 대해 비슷한 변경을 수행 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-198">You want to make similar changes to the pages in the site — *EditMovie.cshtml* and *DeleteMovie.cshtml*.</span></span> <span data-ttu-id="f394d-199">그러나 이렇게 하기 전에 레이아웃에 대 한 다른 변경을 수행 하 여 좀 더 유연 하 게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-199">However, before you do, you can make another change to the layout that makes it a little more flexible.</span></span>

## <a name="passing-title-information-to-the-layout-page"></a><span data-ttu-id="f394d-200">레이아웃 페이지에 제목 정보 전달</span><span class="sxs-lookup"><span data-stu-id="f394d-200">Passing Title Information to the Layout Page</span></span>

<span data-ttu-id="f394d-201">사용자가 만든 *\_레이아웃. cshtml* 페이지에는 "My Movie Site"로 설정 된 `<title>` 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-201">The *\_Layout.cshtml* page that you created has a `<title>` element that's set to "My Movie Site".</span></span> <span data-ttu-id="f394d-202">대부분의 브라우저는이 요소의 내용을 탭의 텍스트로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-202">Most browsers display the content of this element as the text on a tab:</span></span>

![브라우저 탭에 표시 되는 페이지의 &lt;제목&gt; 요소](layouts/_static/image8.png)

<span data-ttu-id="f394d-204">이 제목 정보는 일반 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-204">This title information is generic.</span></span> <span data-ttu-id="f394d-205">제목 텍스트를 현재 페이지에 더 구체적으로 지정 하려고 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-205">Suppose that you want the title text to be more specific to the current page.</span></span> <span data-ttu-id="f394d-206">(제목 텍스트는 페이지에 대 한 정보를 확인 하기 위해 검색 엔진 에서도 사용 됩니다.) *동영상과* 같은 콘텐츠 페이지에서 정보를 전달 하 고, 레이아웃 페이지로 이동한 다음 해당 정보를 사용 하 여 레이아웃 페이지에서 렌더링 되는 항목을 사용자 지정할 수 있습니다 *.*</span><span class="sxs-lookup"><span data-stu-id="f394d-206">(The title text is also used by search engines to determine what your page is about.) You can pass information from a content page like *Movies.cshtml* or *AddMovie.cshtml* to the layout page, and then use that information to customize what the layout page renders.</span></span>

<span data-ttu-id="f394d-207">*동영상. cshtml* 페이지를 다시 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-207">Open the *Movies.cshtml* page again.</span></span> <span data-ttu-id="f394d-208">위쪽의 코드에서 다음 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-208">In the code at the top, add the following line:</span></span>

[!code-csharp[Main](layouts/samples/sample8.cs)]

<span data-ttu-id="f394d-209">`Page` 개체는 모든 *cshtml* 페이지에서 사용할 수 있으며,이 목적을 위해 페이지와 레이아웃 간에 정보를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-209">The `Page` object is available on all *.cshtml* pages and is for this purpose, namely to share information between a page and its layout.</span></span>

<span data-ttu-id="f394d-210">*\_레이아웃. cshtml* 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-210">Open the *\_Layout.cshtml* page.</span></span> <span data-ttu-id="f394d-211">이 태그와 같이 `<title>` 요소를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-211">Change the `<title>` element so that it looks like this markup:</span></span>

[!code-html[Main](layouts/samples/sample9.html)]

<span data-ttu-id="f394d-212">이 코드는 `Page.Title` 속성에 있는 모든 항목을 페이지의 해당 위치에서 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-212">This code renders whatever is in the `Page.Title` property right at that location in the page.</span></span>

<span data-ttu-id="f394d-213">*동영상. cshtml* 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-213">Run the *Movies.cshtml* page.</span></span> <span data-ttu-id="f394d-214">이번에는 브라우저 탭에 `Page.Title`값으로 전달 된 내용이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-214">This time the browser tab shows what you passed as the value of `Page.Title`:</span></span>

![동적으로 생성 된 제목을 보여 주는 브라우저 탭](layouts/_static/image9.png)

<span data-ttu-id="f394d-216">원하는 경우 브라우저에서 페이지 소스를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-216">If you want, view the page source in the browser.</span></span> <span data-ttu-id="f394d-217">`<title>` 요소가 `<title>List Movies</title>`으로 렌더링 되는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-217">You can see that the `<title>` element is rendered as `<title>List Movies</title>`.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="f394d-218">**Page 개체입니다.**</span><span class="sxs-lookup"><span data-stu-id="f394d-218">**The Page Object**</span></span>
> 
> <span data-ttu-id="f394d-219">`Page`의 유용한 기능은 동적 개체입니다. 즉, `Title` 속성이 고정 또는 예약 된 이름이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-219">A useful feature of `Page` is that it's a dynamic object — the `Title` property is not a fixed or reserved name.</span></span> <span data-ttu-id="f394d-220">`Page` 개체의 값으로 *임의의* 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-220">You can use *any* name for a value of the `Page` object.</span></span> <span data-ttu-id="f394d-221">예를 들어 `Page.CurrentName` 또는 `Page.MyPage`라는 속성을 사용 하 여 제목을 쉽게 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-221">For example, you could as easily have passed the title by using a property named `Page.CurrentName` or `Page.MyPage`.</span></span> <span data-ttu-id="f394d-222">유일한 제한 사항은 이름을 지정할 수 있는 속성에 대 한 일반 규칙을 따라야 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-222">The only restriction is that the name has to follow the normal rules for what properties can be named.</span></span> <span data-ttu-id="f394d-223">(예를 들어 이름에는 공백이 포함 될 수 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="f394d-223">(For example, the name can't contain a space.)</span></span>
> 
> <span data-ttu-id="f394d-224">`Page` 개체를 사용 하 여 원하는 수의 값을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-224">You can pass any number of values by using the `Page` object.</span></span> <span data-ttu-id="f394d-225">레이아웃 페이지에 영화 정보를 전달 하려는 경우 `Page.MovieTitle`, `Page.Genre` 및 `Page.MovieYear`와 같은 항목을 사용 하 여 값을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-225">If you wanted to pass movie information to the layout page, you could pass values by using something like `Page.MovieTitle` and `Page.Genre` and `Page.MovieYear`.</span></span> <span data-ttu-id="f394d-226">(또는 정보를 저장 하기 위해 만든 다른 모든 이름) 매우 명백한 요구 사항은 콘텐츠 페이지 및 레이아웃 페이지에서 동일한 이름을 사용 해야 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-226">(Or any other names that you invented to store the information.) The only requirement — which is probably obvious — is that you have to use the same names in the content page and the layout page.</span></span>
> 
> <span data-ttu-id="f394d-227">`Page` 개체를 사용 하 여 전달 하는 정보는 레이아웃 페이지에 표시할 텍스트로만 제한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-227">The information you pass by using the `Page` object isn't limited to just text to display on the layout page.</span></span> <span data-ttu-id="f394d-228">레이아웃 페이지에 값을 전달할 수 있습니다. 그러면 레이아웃 페이지의 코드에서 값을 사용 하 여 페이지의 섹션을 표시할지 여부를 결정 하 고 사용할 *.css* 파일 등을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-228">You can pass a value to the layout page, and then code in the layout page can use the value to decide whether to display a section of the page, what *.css* file to use, and so on.</span></span> <span data-ttu-id="f394d-229">`Page` 개체에서 전달 하는 값은 코드에서 사용 하는 다른 값과 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-229">The values you pass in the `Page` object are like any other values that you use in code.</span></span> <span data-ttu-id="f394d-230">콘텐츠 페이지에서 값이 시작 되 고 레이아웃 페이지에 전달 되는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-230">It's just that the values originate in the content page and are passed to the layout page.</span></span>

<span data-ttu-id="f394d-231">*Addmovie* 페이지를 열고 코드 맨 위에 addmovie의 제목을 제공 하는 줄을 추가 합니다 *. cshtml* 페이지:</span><span class="sxs-lookup"><span data-stu-id="f394d-231">Open the *AddMovie.cshtml* page and add a line to the top of the code that provides a title for the *AddMovie.cshtml* page:</span></span>

[!code-csharp[Main](layouts/samples/sample10.cs)]

<span data-ttu-id="f394d-232">*Addmovie. cshtml* 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-232">Run the *AddMovie.cshtml* page.</span></span> <span data-ttu-id="f394d-233">새 제목 표시:</span><span class="sxs-lookup"><span data-stu-id="f394d-233">You see the new title there:</span></span>

![동적으로 만들어진 ' 동영상 추가 ' 제목을 보여 주는 브라우저 탭](layouts/_static/image10.png)

## <a name="updating-the-remaining-pages-to-use-the-layout"></a><span data-ttu-id="f394d-235">나머지 페이지를 업데이트 하 여 레이아웃 사용</span><span class="sxs-lookup"><span data-stu-id="f394d-235">Updating the Remaining Pages to Use the Layout</span></span>

<span data-ttu-id="f394d-236">이제 새 레이아웃을 사용 하도록 사이트의 나머지 페이지를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-236">Now you can finish the remaining pages in your site so that they use the new layout.</span></span> <span data-ttu-id="f394d-237">*Editmovie. cshtml* 및 *DeleteMovie* 를 차례로 열고 각에서 동일한 변경을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-237">Open *EditMovie.cshtml* and *DeleteMovie.cshtml* in turn and make the same changes in each.</span></span>

<span data-ttu-id="f394d-238">레이아웃 페이지에 연결 되는 코드 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-238">Add the line of code that links to the layout page:</span></span>

[!code-csharp[Main](layouts/samples/sample11.cs)]

<span data-ttu-id="f394d-239">페이지 제목을 설정 하는 선을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-239">Add a line to set the title of the page:</span></span>

[!code-csharp[Main](layouts/samples/sample12.cs)]

<span data-ttu-id="f394d-240">또는:</span><span class="sxs-lookup"><span data-stu-id="f394d-240">or:</span></span>

[!code-csharp[Main](layouts/samples/sample13.cs)]

<span data-ttu-id="f394d-241">모든 불필요 한 HTML 태그를 제거 합니다. 기본적으로 `<body>` 요소 내에 있는 비트만 그대로 둡니다 (맨 위에 있는 코드 블록).</span><span class="sxs-lookup"><span data-stu-id="f394d-241">Remove all the extraneous HTML markup — basically, leave only the bits that are inside the `<body>` element (plus the code block at the top).</span></span>

<span data-ttu-id="f394d-242">`<h1>` 요소를 `<h2>` 요소가 되도록 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-242">Change the `<h1>` element to be an `<h2>` element.</span></span>

<span data-ttu-id="f394d-243">이러한 변경을 수행한 후에는 각 테스트를 테스트 하 여 제대로 표시 되 고 제목이 올바른지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-243">When you've made these changes, test each and make sure that it's displaying properly and that the title is correct.</span></span>

## <a name="parting-thoughts-about-layout-pages"></a><span data-ttu-id="f394d-244">레이아웃 페이지에 대 한 파팅 고가</span><span class="sxs-lookup"><span data-stu-id="f394d-244">Parting Thoughts About Layout Pages</span></span>

<span data-ttu-id="f394d-245">이 자습서에서는 *\_레이아웃* 을 만들고 `RenderBody` 메서드를 사용 하 여 다른 페이지에서 콘텐츠를 병합 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-245">In this tutorial you created a *\_Layout.cshtml* page and used the `RenderBody` method to merge content from another page.</span></span> <span data-ttu-id="f394d-246">이 패턴은 웹 페이지에서 레이아웃을 사용 하는 기본 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-246">That's the basic pattern for using layouts in Web Pages.</span></span>

<span data-ttu-id="f394d-247">레이아웃 페이지에는 여기에 포함 되지 않은 추가 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-247">Layout pages have additional features that we didn't cover here.</span></span> <span data-ttu-id="f394d-248">예를 들어 레이아웃 페이지를 중첩할 수 있습니다. 즉, 한 레이아웃 페이지에서 다른 레이아웃 페이지를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-248">For example, you can nest layout pages — one layout page can in turn reference another.</span></span> <span data-ttu-id="f394d-249">중첩 된 레이아웃은 다른 레이아웃이 필요한 사이트의 하위 섹션으로 작업 하는 경우 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-249">Nested layouts can be useful if you're working with subsections of a site that require different layouts.</span></span> <span data-ttu-id="f394d-250">추가 메서드 (예: `RenderSection`)를 사용 하 여 레이아웃 페이지에서 명명 된 섹션을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-250">You can also use additional methods (for example, `RenderSection`) to set up named sections in the layout page.</span></span>

<span data-ttu-id="f394d-251">레이아웃 페이지와 *.css* 파일의 조합은 강력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-251">The combination of layout pages and *.css* files is powerful.</span></span> <span data-ttu-id="f394d-252">다음 자습서 시리즈에서 볼 수 있듯이, WebMatrix에서 *템플릿을*기반으로 사이트를 만들 수 있으며,이를 통해 미리 빌드된 기능이 있는 사이트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-252">As you'll see in the next tutorial series, in WebMatrix you can create a site based on a *template*, which gives you a site that has prebuilt functionality in it.</span></span> <span data-ttu-id="f394d-253">이 템플릿은 레이아웃 페이지와 CSS를 사용 하 여 메뉴와 같은 기능을 제공 하는 사이트를 만드는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-253">The templates make good use of layout pages and CSS to create sites that look great and that have features like menus.</span></span> <span data-ttu-id="f394d-254">다음은 레이아웃 페이지와 CSS를 사용 하는 기능을 보여 주는 템플릿을 기반으로 하는 사이트의 홈 페이지 스크린샷입니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-254">Here's a screenshot of the home page from a site based on a template, showing features that use layout pages and CSS:</span></span>

![헤더, 탐색 영역, 콘텐츠 영역, 옵션 섹션 및 로그인 링크를 표시 하는 WebMatrix 사이트 템플릿에서 만든 레이아웃](layouts/_static/image11.png)

## <a name="complete-listing-for-movie-page-updated-to-use-a-layout-page"></a><span data-ttu-id="f394d-256">동영상에 대 한 목록 완료 페이지 (레이아웃 페이지를 사용 하도록 업데이트 됨)</span><span class="sxs-lookup"><span data-stu-id="f394d-256">Complete Listing for Movie Page (Updated to Use a Layout Page)</span></span>

[!code-cshtml[Main](layouts/samples/sample14.cshtml)]

## <a name="complete-page-listing-for-add-movie-page-updated-for-layout"></a><span data-ttu-id="f394d-257">동영상 추가 페이지의 전체 페이지 목록 (레이아웃으로 업데이트 됨)</span><span class="sxs-lookup"><span data-stu-id="f394d-257">Complete Page Listing for Add Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample15.cshtml)]

## <a name="complete-page-listing-for-delete-movie-page-updated-for-layout"></a><span data-ttu-id="f394d-258">동영상 삭제 페이지에 대 한 전체 페이지 목록 (레이아웃으로 업데이트 됨)</span><span class="sxs-lookup"><span data-stu-id="f394d-258">Complete Page Listing for Delete Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample16.cshtml)]

## <a name="complete-page-listing-for-edit-movie-page-updated-for-layout"></a><span data-ttu-id="f394d-259">동영상 편집 페이지의 전체 페이지 목록 (레이아웃으로 업데이트 됨)</span><span class="sxs-lookup"><span data-stu-id="f394d-259">Complete Page Listing for Edit Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample17.cshtml)]

## <a name="coming-up-next"></a><span data-ttu-id="f394d-260">다음에서 시작</span><span class="sxs-lookup"><span data-stu-id="f394d-260">Coming Up Next</span></span>

<span data-ttu-id="f394d-261">다음 자습서에서는 모든 사용자가 볼 수 있도록 인터넷에 사이트를 게시 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-261">In the next tutorial, you'll learn how to publish your site to the Internet so everyone can see it.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f394d-262">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f394d-262">Additional Resources</span></span>

- <span data-ttu-id="f394d-263">[일관적인 모양 만들기](https://go.microsoft.com/fwlink/?LinkID=202891) -레이아웃 사용에 대 한 자세한 정보를 제공 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-263">[Creating a Consistent Look](https://go.microsoft.com/fwlink/?LinkID=202891) — An article that provides some more detail on working with layouts.</span></span> <span data-ttu-id="f394d-264">또한 일부 콘텐츠를 표시 하거나 숨기는 레이아웃 페이지에 값을 전달 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-264">It also describes how to pass a value to a layout page that shows or hides some of the content.</span></span>
- <span data-ttu-id="f394d-265">[Razor를 사용 하는 중첩 레이아웃 페이지](http://www.mikesdotnetting.com/Article/164/Nested-Layout-Pages-with-Razor) -레이아웃 페이지를 중첩 하는 방법에 대 한 예제는 Mike brind 블로그입니다.</span><span class="sxs-lookup"><span data-stu-id="f394d-265">[Nested Layout Pages with Razor](http://www.mikesdotnetting.com/Article/164/Nested-Layout-Pages-with-Razor) — Mike Brind blogs an example of how to nest layout pages.</span></span> <span data-ttu-id="f394d-266">(페이지 다운로드 포함)</span><span class="sxs-lookup"><span data-stu-id="f394d-266">(Includes a download of the pages.)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f394d-267">[이전](deleting-data.md)
> [다음](publishing.md)</span><span class="sxs-lookup"><span data-stu-id="f394d-267">[Previous](deleting-data.md)
[Next](publishing.md)</span></span>
