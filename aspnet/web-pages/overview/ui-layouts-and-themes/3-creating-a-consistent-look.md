---
uid: web-pages/overview/ui-layouts-and-themes/3-creating-a-consistent-look
title: ASP.NET 웹 페이지 (Razor) 사이트에서 일관 된 레이아웃 만들기 | Microsoft Docs
author: Rick-Anderson
description: '사이트에 대 한 웹 페이지를 보다 효율적으로 만들 수 있도록 웹 사이트에 대 한 콘텐츠 (예: 머리글 및 바닥글)의 재사용 가능한 블록을 만들 수 있습니다.'
ms.author: riande
ms.date: 03/10/2014
ms.assetid: d7bd001b-6db2-4422-9b78-f3d08b743b00
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/3-creating-a-consistent-look
msc.type: authoredcontent
ms.openlocfilehash: 3f63ce68ae4c13970ac0df196167ace0b22b592c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509099"
---
# <a name="creating-a-consistent-layout-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="72928-103">ASP.NET 웹 페이지 (Razor) 사이트에서 일관 된 레이아웃 만들기</span><span class="sxs-lookup"><span data-stu-id="72928-103">Creating a Consistent Layout in ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="72928-104">만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="72928-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="72928-105">이 문서에서는 Razor (ASP.NET 웹 페이지) 웹 사이트에서 레이아웃 페이지를 사용 하 여 다시 사용할 수 있는 콘텐츠 블록 (예: 머리글 및 바닥글)을 만들고 사이트의 모든 페이지에 대해 일관 된 모양을 만드는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-105">This article explains how you can use layout pages in an ASP.NET Web Pages (Razor) website to create reusable blocks of content (like headers and footers) and to create a consistent look for all the pages in the site.</span></span>
> 
> <span data-ttu-id="72928-106">**학습 내용:**</span><span class="sxs-lookup"><span data-stu-id="72928-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="72928-107">헤더 및 바닥글과 같은 재사용 가능한 콘텐츠 블록을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="72928-107">How to create reusable blocks of content like headers and footers.</span></span>
> - <span data-ttu-id="72928-108">레이아웃을 사용 하 여 사이트의 모든 페이지에 대해 일관 된 모양을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="72928-108">How to create a consistent look for all the pages in your site using a layout.</span></span>
> - <span data-ttu-id="72928-109">런타임에 데이터를 레이아웃 페이지에 전달 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="72928-109">How to pass data at run time to a layout page.</span></span>
> 
> <span data-ttu-id="72928-110">다음은이 문서에 도입 된 ASP.NET 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="72928-110">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="72928-111">콘텐츠 블록-여러 페이지에 삽입할 HTML 형식 콘텐츠를 포함 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="72928-111">Content blocks, which are files that contain HTML-formatted content to be inserted in multiple pages.</span></span>
> - <span data-ttu-id="72928-112">웹 사이트 페이지에서 공유할 수 있는 HTML 형식 콘텐츠를 포함 하는 페이지인 레이아웃 페이지</span><span class="sxs-lookup"><span data-stu-id="72928-112">Layout pages, which are pages that contain HTML-formatted content that can be shared by pages on the website.</span></span>
> - <span data-ttu-id="72928-113">`RenderPage`, `RenderBody`및 `RenderSection` 메서드로, 페이지 요소를 삽입할 위치를 ASP.NET에 게 알립니다.</span><span class="sxs-lookup"><span data-stu-id="72928-113">The `RenderPage`, `RenderBody`, and `RenderSection` methods, which tell ASP.NET where to insert page elements.</span></span>
> - <span data-ttu-id="72928-114">콘텐츠 블록과 레이아웃 페이지 간에 데이터를 공유할 수 있도록 하는 `PageData` 사전입니다.</span><span class="sxs-lookup"><span data-stu-id="72928-114">The `PageData` dictionary that lets you share data between content blocks and layout pages.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="72928-115">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="72928-115">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="72928-116">ASP.NET 웹 페이지 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="72928-116">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="72928-117">이 자습서는 ASP.NET 웹 페이지 2 에서도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-117">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="about-layout-pages"></a><span data-ttu-id="72928-118">레이아웃 페이지 정보</span><span class="sxs-lookup"><span data-stu-id="72928-118">About Layout Pages</span></span>

<span data-ttu-id="72928-119">대부분의 웹 사이트에는 머리글 및 바닥글과 같이 모든 페이지에 표시 되는 콘텐츠 또는 사용자에 게 로그인 여부를 알려 주는 상자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-119">Many websites have content that's displayed on every page, like a header and footer, or a box that tells users that they're logged in.</span></span> <span data-ttu-id="72928-120">ASP.NET를 사용 하면 일반 웹 페이지와 마찬가지로 텍스트, 마크업 및 코드를 포함할 수 있는 콘텐츠 블록을 사용 하 여 별도의 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-120">ASP.NET lets you create a separate file with a content block that can contain text, markup, and code, just like a regular web page.</span></span> <span data-ttu-id="72928-121">그런 다음 정보를 표시할 사이트의 다른 페이지에 콘텐츠 블록을 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-121">You can then insert the content block in other pages on the site where you want the information to appear.</span></span> <span data-ttu-id="72928-122">이렇게 하면 동일한 콘텐츠를 모든 페이지에 복사 하 여 붙여 넣을 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-122">That way you don't have to copy and paste the same content into every page.</span></span> <span data-ttu-id="72928-123">이와 같은 일반적인 콘텐츠를 만들면 사이트를 더 쉽게 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-123">Creating common content like this also makes it easier to update your site.</span></span> <span data-ttu-id="72928-124">콘텐츠를 변경 해야 하는 경우에는 단일 파일만 업데이트 하면 내용이 삽입 된 모든 위치에 변경 내용이 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72928-124">If you need to change the content, you can just update a single file, and the changes are then reflected everywhere the content has been inserted.</span></span>

<span data-ttu-id="72928-125">다음 다이어그램에서는 콘텐츠 블록의 작동 방식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="72928-125">The following diagram shows how content blocks work.</span></span> <span data-ttu-id="72928-126">브라우저에서 웹 서버의 페이지를 요청 하면 ASP.NET는 기본 페이지에서 `RenderPage` 메서드가 호출 된 지점에 콘텐츠 블록을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-126">When a browser requests a page from the web server, ASP.NET inserts the content blocks at the point where the `RenderPage` method is called in the main page.</span></span> <span data-ttu-id="72928-127">그러면 완료 된 (병합 된) 페이지가 브라우저에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72928-127">The finished (merged) page is then sent to the browser.</span></span>

![RenderPage 메서드가 참조 된 페이지를 현재 페이지에 삽입 하는 방법을 보여 주는 개념적 다이어그램입니다.](3-creating-a-consistent-look/_static/image1.jpg)

<span data-ttu-id="72928-129">이 절차에서는 별도의 파일에 있는 두 개의 콘텐츠 블록 (헤더 및 바닥글)을 참조 하는 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72928-129">In this procedure, you'll create a page that references two content blocks (a header and a footer) that are located in separate files.</span></span> <span data-ttu-id="72928-130">사이트의 모든 페이지에서 동일한 콘텐츠 블록을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-130">You can use these same content blocks in any page in your site.</span></span> <span data-ttu-id="72928-131">완료 되 면 다음과 같은 페이지를 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72928-131">When you're done, you'll get a page like this:</span></span>

![RenderPage 메서드에 대 한 호출을 포함 하는 페이지를 실행 하 여 발생 하는 브라우저의 페이지를 보여 주는 스크린샷](3-creating-a-consistent-look/_static/image2.png)

1. <span data-ttu-id="72928-133">웹 사이트의 루트 폴더에서 *Index. cshtml*라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72928-133">In the root folder of your website, create a file named *Index.cshtml*.</span></span>
2. <span data-ttu-id="72928-134">기존 태그를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="72928-134">Replace the existing markup with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample1.html)]
3. <span data-ttu-id="72928-135">루트 폴더에서 *Shared*라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72928-135">In the root folder, create a folder named *Shared*.</span></span>

    > [!NOTE]
    > <span data-ttu-id="72928-136">*공유*된 폴더의 웹 페이지 간에 공유 되는 파일을 저장 하는 것이 일반적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="72928-136">It's common practice to store files that are shared among web pages in a folder named *Shared*.</span></span>
4. <span data-ttu-id="72928-137">*공유* 폴더에서 *\_헤더. cshtml*라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72928-137">In the *Shared* folder, create a file named *\_Header.cshtml*.</span></span>
5. <span data-ttu-id="72928-138">기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="72928-138">Replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample2.html)]

    <span data-ttu-id="72928-139">파일 이름은 *\_헤더. cshtml*이며, 접두사로 밑줄 (\_)을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-139">Notice that the file name is *\_Header.cshtml*, with an underscore (\_) as a prefix.</span></span> <span data-ttu-id="72928-140">ASP.NET 이름이 밑줄로 시작 하는 경우 브라우저에 페이지를 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-140">ASP.NET won't send a page to the browser if its name starts with an underscore.</span></span> <span data-ttu-id="72928-141">이렇게 하면 사용자가 이러한 페이지를 직접 요청 (실수로 또는 그렇지 않은 경우) 할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-141">This prevents people from requesting (inadvertently or otherwise) these pages directly.</span></span> <span data-ttu-id="72928-142">사용자가 해당 페이지 &#8212; 를 다른 페이지에 삽입 하는 것을 엄격 하 게 요청할 수 없도록 하기 때문에 콘텐츠 블록이 있는 페이지의 이름을 지정할 때 밑줄을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-142">It's a good idea to use an underscore to name pages that have content blocks in them, because you don't really want users to be able to request these pages &#8212; they exist strictly to be inserted into other pages.</span></span>
6. <span data-ttu-id="72928-143">*공유* 폴더에서 *\_Footer* 라는 파일을 만들고 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="72928-143">In the *Shared* folder, create a file named *\_Footer.cshtml* and replace the content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample3.html)]
7. <span data-ttu-id="72928-144">*Index. cshtml* 페이지에서 다음과 같이 `RenderPage` 메서드에 대 한 두 호출을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-144">In the *Index.cshtml* page, add two calls to the `RenderPage` method, as shown here:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample4.html)]

    <span data-ttu-id="72928-145">웹 페이지에 콘텐츠 블록을 삽입 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="72928-145">This shows how to insert a content block into a web page.</span></span> <span data-ttu-id="72928-146">`RenderPage` 메서드를 호출 하 여 해당 위치에 삽입 하려는 내용의 파일 이름을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-146">You call the `RenderPage` method and pass it the name of the file whose contents you want to insert at that point.</span></span> <span data-ttu-id="72928-147">여기에서 *\_헤더* 의 내용을 삽입 합니다. cshtml 및 *\_Footer* 파일에는 *인덱스 cshtml* 파일.</span><span class="sxs-lookup"><span data-stu-id="72928-147">Here, you're inserting the contents of the *\_Header.cshtml* and *\_Footer.cshtml* files into the *Index.cshtml* file.</span></span>
8. <span data-ttu-id="72928-148">브라우저에서 *Index. cshtml* 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-148">Run the *Index.cshtml* page in a browser.</span></span> <span data-ttu-id="72928-149">(WebMatrix의 **파일** 작업 영역에서 파일을 마우스 오른쪽 단추로 클릭 한 다음 **브라우저에서 시작**을 선택 합니다.)</span><span class="sxs-lookup"><span data-stu-id="72928-149">(In WebMatrix, in the **Files** workspace, right-click the file and then select **Launch in browser**.)</span></span>
9. <span data-ttu-id="72928-150">브라우저에서 페이지 소스를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="72928-150">In the browser, view the page source.</span></span> <span data-ttu-id="72928-151">예를 들어 Internet Explorer에서 페이지를 마우스 오른쪽 단추로 클릭 한 다음 **소스 보기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-151">(For example, in Internet Explorer, right-click the page and then click **View Source**.)</span></span>

    <span data-ttu-id="72928-152">이렇게 하면 브라우저에 전송 된 웹 페이지 태그를 볼 수 있습니다 .이 태그는 인덱스 페이지 태그를 콘텐츠 블록과 결합 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-152">This lets you see the web page markup that's sent to the browser, which combines the index page markup with the content blocks.</span></span> <span data-ttu-id="72928-153">다음 예에서는 *Index. cshtml*에 대해 렌더링 되는 페이지 원본을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="72928-153">The following example shows the page source that's rendered for *Index.cshtml*.</span></span> <span data-ttu-id="72928-154">*Index. cshtml* 에 삽입 된 `RenderPage`에 대 한 호출은 머리글 및 바닥글 파일의 실제 콘텐츠로 대체 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-154">The calls to `RenderPage` that you inserted into *Index.cshtml* have been replaced with the actual contents of the header and footer files.</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample5.html)]

## <a name="creating-a-consistent-look-using-layout-pages"></a><span data-ttu-id="72928-155">레이아웃 페이지를 사용 하 여 일관 된 모양 만들기</span><span class="sxs-lookup"><span data-stu-id="72928-155">Creating a Consistent Look Using Layout Pages</span></span>

<span data-ttu-id="72928-156">지금까지 여러 페이지에 동일한 콘텐츠를 포함 하는 것이 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-156">So far you've seen that it's easy to include the same content on multiple pages.</span></span> <span data-ttu-id="72928-157">사이트를 일관 되 게 찾는 방법은 레이아웃 페이지를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="72928-157">A more structured approach to creating a consistent look for a site is to use layout pages.</span></span> <span data-ttu-id="72928-158">레이아웃 페이지는 웹 페이지의 구조를 정의 하지만 실제 콘텐츠는 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-158">A layout page defines the structure of a web page, but doesn't contain any actual content.</span></span> <span data-ttu-id="72928-159">레이아웃 페이지를 만든 후에는 콘텐츠를 포함 하는 웹 페이지를 만든 다음 레이아웃 페이지에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-159">After you've created a layout page, you can create web pages that contain the content and then link them to the layout page.</span></span> <span data-ttu-id="72928-160">이러한 페이지가 표시 되 면 레이아웃 페이지에 따라 형식이 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72928-160">When these pages are displayed, they'll be formatted according to the layout page.</span></span> <span data-ttu-id="72928-161">이 경우 레이아웃 페이지는 다른 페이지에 정의 된 콘텐츠에 대 한 일종의 템플릿 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-161">(In this sense, a layout page acts as a kind of template for content that's defined in other pages.)</span></span>

<span data-ttu-id="72928-162">레이아웃 페이지는 `RenderBody` 메서드에 대 한 호출을 포함 한다는 점을 제외 하 고 HTML 페이지와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-162">The layout page is just like any HTML page, except that it contains a call to the `RenderBody` method.</span></span> <span data-ttu-id="72928-163">레이아웃 페이지에서 `RenderBody` 메서드의 위치에 따라 콘텐츠 페이지의 정보가 포함 될 위치가 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72928-163">The position of the `RenderBody` method in the layout page determines where the information from the content page will be included.</span></span>

<span data-ttu-id="72928-164">다음 다이어그램에서는 런타임에 콘텐츠 페이지 및 레이아웃 페이지를 결합 하 여 완성 된 웹 페이지를 생성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="72928-164">The following diagram shows how content pages and layout pages are combined at run time to produce the finished web page.</span></span> <span data-ttu-id="72928-165">브라우저에서 콘텐츠 페이지를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-165">The browser requests a content page.</span></span> <span data-ttu-id="72928-166">콘텐츠 페이지에는 페이지 구조에 사용할 레이아웃 페이지를 지정 하는 코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-166">The content page has code in it that specifies the layout page to use for the page's structure.</span></span> <span data-ttu-id="72928-167">레이아웃 페이지에서 `RenderBody` 메서드가 호출 되는 지점에 콘텐츠가 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72928-167">In the layout page, the content is inserted at the point where the `RenderBody` method is called.</span></span> <span data-ttu-id="72928-168">이전 섹션에서 수행한 것과 같은 방법으로 `RenderPage` 메서드를 호출 하 여 콘텐츠 블록을 레이아웃 페이지에 삽입할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-168">Content blocks can also be inserted into the layout page by calling the `RenderPage` method, the way you did in the previous section.</span></span> <span data-ttu-id="72928-169">웹 페이지가 완료 되 면 브라우저에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72928-169">When the web page is complete, it's sent to the browser.</span></span>

![RenderBody 메서드 호출을 포함 하는 페이지를 실행 하 여 발생 하는 브라우저의 페이지를 보여 주는 스크린샷](3-creating-a-consistent-look/_static/image3.jpg)

<span data-ttu-id="72928-171">다음 절차에서는 레이아웃 페이지를 만들고 콘텐츠 페이지를 해당 페이지에 연결 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="72928-171">The following procedure shows how to create a layout page and link content pages to it.</span></span>

1. <span data-ttu-id="72928-172">웹 사이트의 *공유* 폴더에서 *Layout1\_* 라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72928-172">In the *Shared* folder of your website, create a file named *\_Layout1.cshtml*.</span></span>
2. <span data-ttu-id="72928-173">기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="72928-173">Replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample6.html)]

    <span data-ttu-id="72928-174">레이아웃 페이지에서 `RenderPage` 메서드를 사용 하 여 콘텐츠 블록을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-174">You use the `RenderPage` method in a layout page to insert content blocks.</span></span> <span data-ttu-id="72928-175">레이아웃 페이지는 `RenderBody` 메서드에 대 한 호출을 하나만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-175">A layout page can contain only one call to the `RenderBody` method.</span></span>
3. <span data-ttu-id="72928-176">*공유* 폴더에서 *.header2\_* 라는 파일을 만들고 기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="72928-176">In the *Shared* folder, create a file named *\_Header2.cshtml* and replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample7.html)]
4. <span data-ttu-id="72928-177">루트 폴더에서 새 폴더를 만들고 이름을 *스타일*로 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-177">In the root folder, create a new folder and name it *Styles*.</span></span>
5. <span data-ttu-id="72928-178">*Styles* 폴더에서 이름이 *.css* 인 파일을 만들고 다음 스타일 정의를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-178">In the *Styles* folder, create a file named *Site.css* and add the following style definitions:</span></span>

    [!code-css[Main](3-creating-a-consistent-look/samples/sample8.css)]

    <span data-ttu-id="72928-179">이러한 스타일 정의는 레이아웃 페이지에서 스타일 시트를 사용 하는 방법을 보여 주기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="72928-179">These style definitions are here only to show how style sheets can be used with layout pages.</span></span> <span data-ttu-id="72928-180">원하는 경우 이러한 요소에 대해 고유한 스타일을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-180">If you want, you can define your own styles for these elements.</span></span>
6. <span data-ttu-id="72928-181">루트 폴더에서 *Content1* 라는 파일을 만들고 기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="72928-181">In the root folder, create a file named *Content1.cshtml* and replace any existing content with the following:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample9.cshtml)]

    <span data-ttu-id="72928-182">레이아웃 페이지를 사용 하는 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="72928-182">This is a page that will use a layout page.</span></span> <span data-ttu-id="72928-183">페이지 맨 위에 있는 코드 블록은이 콘텐츠 형식을 지정 하는 데 사용할 레이아웃 페이지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="72928-183">The code block at the top of the page indicates which layout page to use to format this content.</span></span>
7. <span data-ttu-id="72928-184">브라우저에서 *Content1* 를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-184">Run *Content1.cshtml* in a browser.</span></span> <span data-ttu-id="72928-185">렌더링 된 페이지는 *\_Layout1* 에 정의 된 형식 및 스타일 시트와 *Content1*에 정의 된 텍스트 (내용)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-185">The rendered page uses the format and style sheet defined in *\_Layout1.cshtml* and the text (content) defined in *Content1.cshtml*.</span></span>

    ![[이미지]](3-creating-a-consistent-look/_static/image4.png)

    <span data-ttu-id="72928-187">6 단계를 반복 하 여 동일한 레이아웃 페이지를 공유할 수 있는 추가 콘텐츠 페이지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-187">You can repeat step 6 to create additional content pages that can then share the same layout page.</span></span>

    > [!NOTE]
    > <span data-ttu-id="72928-188">폴더의 모든 콘텐츠 페이지에 대해 동일한 레이아웃 페이지를 자동으로 사용할 수 있도록 사이트를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-188">You can set up your site so that you can automatically use the same layout page for all the content pages in a folder.</span></span> <span data-ttu-id="72928-189">자세한 내용은 [ASP.NET 웹 페이지에 대 한 사이트 전체 동작 사용자 지정](https://go.microsoft.com/fwlink/?LinkId=202906)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="72928-189">For details, see [Customizing Site-Wide Behavior for ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=202906).</span></span>

## <a name="designing-layout-pages-that-have-multiple-content-sections"></a><span data-ttu-id="72928-190">여러 콘텐츠 섹션이 있는 레이아웃 페이지 디자인</span><span class="sxs-lookup"><span data-stu-id="72928-190">Designing Layout Pages That Have Multiple Content Sections</span></span>

<span data-ttu-id="72928-191">콘텐츠 페이지에는 여러 섹션이 있을 수 있습니다 .이는 대체 가능한 콘텐츠가 있는 여러 영역이 있는 레이아웃을 사용 하려는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-191">A content page can have multiple sections, which is useful if you want to use layouts that have multiple areas with replaceable content.</span></span> <span data-ttu-id="72928-192">콘텐츠 페이지에서 각 섹션에 고유한 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-192">In the content page, you give each section a unique name.</span></span> <span data-ttu-id="72928-193">기본 섹션은 명명 되지 않은 상태로 남아 있습니다. 레이아웃 페이지에서 명명 되지 않은 (기본값) 섹션이 표시 되는 위치를 지정 하는 `RenderBody` 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-193">(The default section is left unnamed.) In the layout page, you add a `RenderBody` method to specify where the unnamed (default) section should appear.</span></span> <span data-ttu-id="72928-194">그런 다음 명명 된 섹션을 개별적으로 렌더링 하기 위해 별도의 `RenderSection` 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-194">You then add separate `RenderSection` methods in order to render named sections individually.</span></span>

<span data-ttu-id="72928-195">다음 다이어그램에서는 ASP.NET에서 여러 섹션으로 나뉜 콘텐츠를 처리 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="72928-195">The following diagram shows how ASP.NET handles content that's divided into multiple sections.</span></span> <span data-ttu-id="72928-196">각 명명 된 섹션은 콘텐츠 페이지의 섹션 블록에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-196">Each named section is contained in a section block in the content page.</span></span> <span data-ttu-id="72928-197">(예제에서는 `Header` 이름이 지정 되 고 `List`. 프레임 워크는 `RenderSection` 메서드가 호출 된 지점의 레이아웃 페이지에 콘텐츠 섹션을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-197">(They're named `Header` and `List` in the example.) The framework inserts content section into the layout page at the point where the `RenderSection` method is called.</span></span> <span data-ttu-id="72928-198">명명 되지 않은 (기본) 섹션은 앞에서 살펴본 것 처럼 `RenderBody` 메서드가 호출 된 지점에 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72928-198">The unnamed (default) section is inserted at the point where the `RenderBody` method is called, as you saw earlier.</span></span>

![RenderSection 메서드가 참조 섹션을 현재 페이지에 삽입 하는 방법을 보여 주는 개념적 다이어그램](3-creating-a-consistent-look/_static/image5.jpg)

<span data-ttu-id="72928-200">이 절차에서는 여러 콘텐츠 섹션을 포함 하는 콘텐츠 페이지를 만드는 방법과 여러 콘텐츠 섹션을 지 원하는 레이아웃 페이지를 사용 하 여 렌더링 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="72928-200">This procedure shows how to create a content page that has multiple content sections and how to render it using a layout page that supports multiple content sections.</span></span>

1. <span data-ttu-id="72928-201">*공유* 폴더에서 *Layout2\_* 라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72928-201">In the *Shared* folder, create a file named *\_Layout2.cshtml*.</span></span>
2. <span data-ttu-id="72928-202">기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="72928-202">Replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample10.html)]

    <span data-ttu-id="72928-203">`RenderSection` 메서드를 사용 하 여 헤더 및 목록 섹션을 모두 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-203">You use the `RenderSection` method to render both the header and list sections.</span></span>
3. <span data-ttu-id="72928-204">루트 폴더에서 *Content2* 라는 파일을 만들고 기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="72928-204">In the root folder, create a file named *Content2.cshtml* and replace any existing content with the following:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample11.cshtml)]

    <span data-ttu-id="72928-205">이 콘텐츠 페이지에는 페이지 맨 위에 있는 코드 블록이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-205">This content page contains a code block at the top of the page.</span></span> <span data-ttu-id="72928-206">각 명명 된 섹션은 section 블록에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-206">Each named section is contained in a section block.</span></span> <span data-ttu-id="72928-207">페이지의 나머지 부분에는 기본 (명명 되지 않은) 콘텐츠 섹션이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-207">The rest of the page contains the default (unnamed) content section.</span></span>
4. <span data-ttu-id="72928-208">브라우저에서 *Content2* 를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-208">Run *Content2.cshtml* in a browser.</span></span>

    ![RenderSection 메서드 호출을 포함 하는 페이지를 실행 하 여 발생 하는 브라우저의 페이지를 보여 주는 스크린샷](3-creating-a-consistent-look/_static/image6.png)

## <a name="making-content-sections-optional"></a><span data-ttu-id="72928-210">콘텐츠 섹션 만들기 옵션</span><span class="sxs-lookup"><span data-stu-id="72928-210">Making Content Sections Optional</span></span>

<span data-ttu-id="72928-211">일반적으로 콘텐츠 페이지에서 만드는 섹션은 레이아웃 페이지에 정의 된 섹션과 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-211">Normally, the sections that you create in a content page have to match sections that are defined in the layout page.</span></span> <span data-ttu-id="72928-212">다음 중 하나가 발생 하는 경우 오류를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-212">You can get errors if any of the following occur:</span></span>

- <span data-ttu-id="72928-213">콘텐츠 페이지의 레이아웃 페이지에 해당 섹션이 없는 섹션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-213">The content page contains a section that has no corresponding section in the layout page.</span></span>
- <span data-ttu-id="72928-214">레이아웃 페이지에 콘텐츠가 없는 섹션이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-214">The layout page contains a section for which there's no content.</span></span>
- <span data-ttu-id="72928-215">레이아웃 페이지에 동일한 섹션을 두 번 이상 렌더링 하려고 하는 메서드 호출이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-215">The layout page includes method calls that try to render the same section more than once.</span></span>

<span data-ttu-id="72928-216">그러나 레이아웃 페이지에서 섹션을 선택 사항으로 선언 하 여 명명 된 섹션에 대해이 동작을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-216">However, you can override this behavior for a named section by declaring the section to be optional in the layout page.</span></span> <span data-ttu-id="72928-217">이렇게 하면 레이아웃 페이지를 공유할 수 있지만 특정 섹션에 대 한 콘텐츠가 없을 수도 있는 여러 콘텐츠 페이지를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-217">This lets you define multiple content pages that can share a layout page but that might or might not have content for a specific section.</span></span>

1. <span data-ttu-id="72928-218">Content2를 열고 다음 섹션을 제거 *합니다* .</span><span class="sxs-lookup"><span data-stu-id="72928-218">Open *Content2.cshtml* and remove the following section:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample12.cshtml)]
2. <span data-ttu-id="72928-219">페이지를 저장 하 고 브라우저에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-219">Save the page and then run it in a browser.</span></span> <span data-ttu-id="72928-220">콘텐츠 페이지에서 레이아웃 페이지에 정의 된 섹션에 대 한 콘텐츠 (헤더 섹션)를 제공 하지 않기 때문에 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72928-220">An error message is displayed, because the content page doesn't provide content for a section defined in the layout page, namely the header section.</span></span>

    ![RenderSection 메서드를 호출 하는 페이지를 실행 하지만 해당 섹션이 제공 되지 않는 경우 발생 하는 오류를 보여 주는 스크린샷](3-creating-a-consistent-look/_static/image7.png)
3. <span data-ttu-id="72928-222">*공유* 폴더에서 *\_Layout2* 페이지를 열고 다음 줄을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="72928-222">In the *Shared* folder, open the *\_Layout2.cshtml* page and replace this line:</span></span>

    [!code-javascript[Main](3-creating-a-consistent-look/samples/sample13.js)]

    <span data-ttu-id="72928-223">다음 코드와 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="72928-223">with the following code:</span></span>

    [!code-javascript[Main](3-creating-a-consistent-look/samples/sample14.js)]

    <span data-ttu-id="72928-224">또는 동일한 결과를 생성 하는 다음 코드 블록으로 이전 코드 줄을 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-224">As an alternative, you could replace the previous line of code with the following code block, which produces the same results:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample15.cshtml)]
4. <span data-ttu-id="72928-225">브라우저에서 *Content2* 페이지를 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-225">Run the *Content2.cshtml* page in a browser again.</span></span> <span data-ttu-id="72928-226">브라우저에서이 페이지를 열어 둔 경우 새로 고칠 수 있습니다. 이번에는 헤더가 없더라도 페이지가 오류 없이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72928-226">(If you still have this page open in the browser, you can just refresh it.) This time the page is displayed with no error, even though it has no header.</span></span>

## <a name="passing-data-to-layout-pages"></a><span data-ttu-id="72928-227">레이아웃 페이지에 데이터 전달</span><span class="sxs-lookup"><span data-stu-id="72928-227">Passing Data to Layout Pages</span></span>

<span data-ttu-id="72928-228">콘텐츠 페이지에서 레이아웃 페이지에 참조 해야 하는 데이터를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-228">You might have data defined in the content page that you need to refer to in a layout page.</span></span> <span data-ttu-id="72928-229">그렇다면 콘텐츠 페이지에서 레이아웃 페이지로 데이터를 전달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-229">If so, you need to pass the data from the content page to the layout page.</span></span> <span data-ttu-id="72928-230">예를 들어 사용자의 로그인 상태를 표시 하거나 사용자 입력을 기준으로 콘텐츠 영역을 표시 하거나 숨길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-230">For example, you might want to display the login status of a user, or you might want to show or hide content areas based on user input.</span></span>

<span data-ttu-id="72928-231">콘텐츠 페이지에서 레이아웃 페이지로 데이터를 전달 하려면 콘텐츠 페이지의 `PageData` 속성에 값을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-231">To pass data from a content page to a layout page, you can put values into the `PageData` property of the content page.</span></span> <span data-ttu-id="72928-232">`PageData` 속성은 페이지 간에 전달 하려는 데이터를 포함 하는 이름/값 쌍의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="72928-232">The `PageData` property is a collection of name/value pairs that hold the data that you want to pass between pages.</span></span> <span data-ttu-id="72928-233">그러면 레이아웃 페이지에서 `PageData` 속성의 값을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-233">In the layout page, you can then read values out of the `PageData` property.</span></span>

<span data-ttu-id="72928-234">다른 다이어그램은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-234">Here's another diagram.</span></span> <span data-ttu-id="72928-235">이 항목에서는 ASP.NET가 `PageData` 속성을 사용 하 여 콘텐츠 페이지의 값을 레이아웃 페이지에 전달 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="72928-235">This one shows how ASP.NET can use the `PageData` property to pass values from a content page to the layout page.</span></span> <span data-ttu-id="72928-236">ASP.NET가 웹 페이지 빌드를 시작 하면 `PageData` 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72928-236">When ASP.NET begins building the web page, it creates the `PageData` collection.</span></span> <span data-ttu-id="72928-237">콘텐츠 페이지에서 `PageData` 컬렉션에 데이터를 저장 하는 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-237">In the content page, you write code to put data in the `PageData` collection.</span></span> <span data-ttu-id="72928-238">`PageData` 컬렉션의 값은 콘텐츠 페이지의 다른 섹션 또는 추가 콘텐츠 블록 에서도 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-238">Values in the `PageData` collection can also be accessed by other sections in the content page or by additional content blocks.</span></span>

![콘텐츠 페이지가 PageData 사전을 채우고 해당 정보를 레이아웃 페이지에 전달 하는 방법을 보여 주는 개념적 다이어그램입니다.](3-creating-a-consistent-look/_static/image8.jpg)

<span data-ttu-id="72928-240">다음 절차에서는 콘텐츠 페이지에서 레이아웃 페이지로 데이터를 전달 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="72928-240">The following procedure shows how to pass data from a content page to a layout page.</span></span> <span data-ttu-id="72928-241">페이지가 실행 되 면 사용자가 레이아웃 페이지에 정의 된 목록을 숨기 거 나 표시할 수 있는 단추가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72928-241">When the page runs, it displays a button that lets the user hide or show a list that's defined in the layout page.</span></span> <span data-ttu-id="72928-242">사용자가 단추를 클릭 하면 `PageData` 속성에 true/false (부울) 값이 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72928-242">When users click the button, it sets a true/false (Boolean) value in the `PageData` property.</span></span> <span data-ttu-id="72928-243">레이아웃 페이지에서 해당 값을 읽고, false 인 경우 목록을 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="72928-243">The layout page reads that value, and if it's false, hides the list.</span></span> <span data-ttu-id="72928-244">콘텐츠 페이지에서 **목록 숨기기** 단추 또는 **목록 표시** 단추를 표시할지 여부를 결정 하는 데에도이 값이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72928-244">The value is also used in the content page to determine whether to display the **Hide List** button or the **Show List** button.</span></span>

![[이미지]](3-creating-a-consistent-look/_static/image9.jpg)

1. <span data-ttu-id="72928-246">루트 폴더에서 *Content3* 라는 파일을 만들고 기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="72928-246">In the root folder, create a file named *Content3.cshtml* and replace any existing content with the following:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample16.cshtml)]

    <span data-ttu-id="72928-247">이 코드는 두 개의 데이터를 웹 페이지의 제목 &#8212; `PageData` 속성에 저장 하 고 true 또는 false를 지정 하 여 목록을 표시할지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-247">The code stores two pieces of data in the `PageData` property &#8212; the title of the web page and true or false to specify whether to display a list.</span></span>

    <span data-ttu-id="72928-248">ASP.NET를 사용 하면 코드 블록을 사용 하 여 조건적으로 페이지에 HTML 태그를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-248">Notice that ASP.NET lets you put HTML markup into the page conditionally using a code block.</span></span> <span data-ttu-id="72928-249">예를 들어 페이지 본문의 `if/else` 블록은 `PageData["ShowList"]` true로 설정 되었는지 여부에 따라 표시할 폼을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-249">For example, the `if/else` block in the body of the page determines which form to display depending on whether `PageData["ShowList"]` is set to true.</span></span>
2. <span data-ttu-id="72928-250">*공유* 폴더에서 *Layout3\_* 라는 파일을 만들고 기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="72928-250">In the *Shared* folder, create a file named *\_Layout3.cshtml* and replace any existing content with the following:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample17.cshtml)]

    <span data-ttu-id="72928-251">레이아웃 페이지에는 `PageData` 속성에서 제목 값을 가져오는 `<title>` 요소의 식이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72928-251">The layout page includes an expression in the `<title>` element that gets the title value from the `PageData` property.</span></span> <span data-ttu-id="72928-252">또한 `PageData` 속성의 `ShowList` 값을 사용 하 여 목록 콘텐츠 블록을 표시할지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-252">It also uses the `ShowList` value of the `PageData` property to determine whether to display the list content block.</span></span>
3. <span data-ttu-id="72928-253">*공유* 폴더에서 *\_List. cshtml* 라는 파일을 만들고 기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="72928-253">In the *Shared* folder, create a file named *\_List.cshtml* and replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample18.html)]
4. <span data-ttu-id="72928-254">브라우저에서 *Content3* 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-254">Run the *Content3.cshtml* page in a browser.</span></span> <span data-ttu-id="72928-255">페이지의 왼쪽에 목록이 표시 되 고 맨 아래에 **목록 숨기기** 단추가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72928-255">The page is displayed with the list visible on the left side of the page and a **Hide List** button at the bottom.</span></span>

    ![목록을 포함 하는 페이지와 ' 목록 숨기기 ' 라고 표시 된 단추를 보여 주는 스크린샷](3-creating-a-consistent-look/_static/image10.png)
5. <span data-ttu-id="72928-257">**목록 숨기기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="72928-257">Click **Hide List**.</span></span> <span data-ttu-id="72928-258">목록이 사라지고 단추가 **목록 표시**로 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72928-258">The list disappears and the button changes to **Show List**.</span></span>

    ![목록 및 ' Show List ' 단추를 포함 하지 않는 페이지를 보여 주는 스크린샷](3-creating-a-consistent-look/_static/image11.png)
6. <span data-ttu-id="72928-260">**목록 표시** 단추를 클릭 하면 목록이 다시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72928-260">Click the **Show List** button, and the list is displayed again.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="72928-261">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="72928-261">Additional Resources</span></span>

[<span data-ttu-id="72928-262">ASP.NET 웹 페이지에 대 한 사이트 전체 동작 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="72928-262">Customizing Site-Wide Behavior for ASP.NET Web Pages</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
