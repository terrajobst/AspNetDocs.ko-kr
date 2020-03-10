---
uid: web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
title: ASP.NET 웹 페이지 (Razor) 사이트에서 도우미 만들기 및 사용 | Microsoft Docs
author: Rick-Anderson
description: 이 문서에서는 Razor (ASP.NET 웹 페이지) 웹 사이트에서 도우미를 만드는 방법을 설명 합니다. 도우미는 성능에 코드 및 태그를 포함 하는 다시 사용할 수 있는 구성 요소입니다.
ms.author: riande
ms.date: 02/17/2014
ms.assetid: 46bff772-01e0-40f0-9ae6-9e18c5442ee6
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 380663951094c9fc7d5f0601e30995fa073a204b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454307"
---
# <a name="creating-and-using-a-helper-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="d928a-104">ASP.NET 웹 페이지 (Razor) 사이트에서 도우미 만들기 및 사용</span><span class="sxs-lookup"><span data-stu-id="d928a-104">Creating and Using a Helper in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="d928a-105">만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="d928a-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="d928a-106">이 문서에서는 Razor (ASP.NET 웹 페이지) 웹 사이트에서 도우미를 만드는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-106">This article describes how to create a helper in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="d928a-107">*도우미* 는 지루한 또는 복잡할 수 있는 작업을 수행 하기 위한 코드와 태그를 포함 하는 재사용 가능한 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-107">A *helper* is a reusable component that includes code and markup to perform a task that might be tedious or complex.</span></span>
> 
> <span data-ttu-id="d928a-108">**학습 내용:**</span><span class="sxs-lookup"><span data-stu-id="d928a-108">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="d928a-109">간단한 도우미를 만들고 사용 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-109">How to create and use a simple helper.</span></span>
> 
> <span data-ttu-id="d928a-110">다음은이 문서에 도입 된 ASP.NET 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-110">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="d928a-111">`@helper` 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-111">The `@helper` syntax.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="d928a-112">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="d928a-112">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="d928a-113">ASP.NET 웹 페이지 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="d928a-113">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="d928a-114">이 자습서는 ASP.NET 웹 페이지 2 에서도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-114">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="overview-of-helpers"></a><span data-ttu-id="d928a-115">도우미 개요</span><span class="sxs-lookup"><span data-stu-id="d928a-115">Overview of Helpers</span></span>

<span data-ttu-id="d928a-116">사이트의 서로 다른 페이지에서 동일한 작업을 수행 해야 하는 경우 도우미를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-116">If you need to perform the same tasks on different pages in your site, you can use a helper.</span></span> <span data-ttu-id="d928a-117">ASP.NET 웹 페이지에는 많은 도우미가 포함 되어 있으며 다운로드 하 고 설치할 수 있는 많은 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-117">ASP.NET Web Pages includes a number of helpers, and there are many more that you can download and install.</span></span> <span data-ttu-id="d928a-118">ASP.NET 웹 페이지의 기본 제공 도우미 목록은 [ASP.NET API 빠른 참조](https://go.microsoft.com/fwlink/?LinkId=202907)에 나열 되어 있습니다. 사용자의 요구를 충족 하는 기존 도우미가 없는 경우 사용자 고유의 도우미를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-118">(A list of the built-in helpers in ASP.NET Web Pages is listed in the [ASP.NET API Quick Reference](https://go.microsoft.com/fwlink/?LinkId=202907).) If none of the existing helpers meet your needs, you can create your own helper.</span></span>

<span data-ttu-id="d928a-119">도우미를 사용 하면 여러 페이지에서 공통 코드 블록을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-119">A helper lets you use a common block of code across multiple pages.</span></span> <span data-ttu-id="d928a-120">페이지에서 일반적으로 일반 단락과 별도로 설정 된 메모 항목을 만들려고 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-120">Suppose that in your page you often want to create a note item that's set apart from normal paragraphs.</span></span> <span data-ttu-id="d928a-121">노트는 테두리가 있는 상자로 스타일을 지정 하는 `<div>` 요소로 생성 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-121">Perhaps the note is created as a `<div>` element that's styled as a box with a border.</span></span> <span data-ttu-id="d928a-122">메모를 표시 하려고 할 때마다 동일한 태그를 페이지에 추가 하는 대신 태그를 도우미로 패키지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-122">Rather than add this same markup to a page every time you want to display a note, you can package the markup as a helper.</span></span> <span data-ttu-id="d928a-123">그런 다음 필요에 맞게 한 줄의 코드를 사용 하 여 메모를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-123">You can then insert the note with a single line of code anywhere you need it.</span></span>

<span data-ttu-id="d928a-124">이와 같은 도우미를 사용 하면 각 페이지의 코드를 보다 간단 하 고 쉽게 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-124">Using a helper like this makes the code in each of your pages simpler and easier to read.</span></span> <span data-ttu-id="d928a-125">또한 노트의 모양을 변경 해야 하는 경우에는 한 곳에서 태그를 변경할 수 있기 때문에 사이트를 더 쉽게 유지 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-125">It also makes it easier to maintain your site, because if you need to change how the notes look, you can change the markup in one place.</span></span>

## <a name="creating-a-helper"></a><span data-ttu-id="d928a-126">도우미 만들기</span><span class="sxs-lookup"><span data-stu-id="d928a-126">Creating a Helper</span></span>

<span data-ttu-id="d928a-127">이 절차에서는 설명 된 대로 메모를 만드는 도우미를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-127">This procedure shows you how to create the helper that creates the note, as just described.</span></span> <span data-ttu-id="d928a-128">이는 간단한 예제 이지만 사용자 지정 도우미에는 필요한 모든 태그 및 ASP.NET 코드가 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-128">This is a simple example, but the custom helper can include any markup and ASP.NET code that you need.</span></span>

1. <span data-ttu-id="d928a-129">웹 사이트의 루트 폴더에서 *App\_Code*라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-129">In the root folder of the website, create a folder named *App\_Code*.</span></span> <span data-ttu-id="d928a-130">ASP.NET에서 도우미와 같은 구성 요소에 대 한 코드를 넣을 수 있는 예약 된 폴더 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-130">This is a reserved folder name in ASP.NET where you can put code for components like helpers.</span></span>
2. <span data-ttu-id="d928a-131">*앱\_코드* 폴더에서 새 *cshtml* 파일을 만들고 이름을 myororors로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-131">In the *App\_Code* folder create a new *.cshtml* file and name it *MyHelpers.cshtml*.</span></span>
3. <span data-ttu-id="d928a-132">기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-132">Replace the existing content with the following:</span></span>

    [!code-cshtml[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    <span data-ttu-id="d928a-133">이 코드는 `@helper` 구문을 사용 하 여 `MakeNote`라는 새 도우미를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-133">The code uses the `@helper` syntax to declare a new helper named `MakeNote`.</span></span> <span data-ttu-id="d928a-134">이 특정 도우미를 사용 하면 텍스트와 태그의 조합을 포함할 수 있는 `content` 매개 변수를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-134">This particular helper lets you pass a parameter named `content` that can contain a combination of text and markup.</span></span> <span data-ttu-id="d928a-135">도우미는 `@content` 변수를 사용 하 여 메모 본문에 문자열을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-135">The helper inserts the string into the note body using the `@content` variable.</span></span>

    <span data-ttu-id="d928a-136">파일 이름은 *myhelpers. cshtml*이지만 도우미의 이름은 `MakeNote`입니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-136">Notice that the file is named *MyHelpers.cshtml*, but the helper is named `MakeNote`.</span></span> <span data-ttu-id="d928a-137">단일 파일에 여러 사용자 지정 도우미를 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-137">You can put multiple custom helpers into a single file.</span></span>
4. <span data-ttu-id="d928a-138">파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-138">Save and close the file.</span></span>

## <a name="using-the-helper-in-a-page"></a><span data-ttu-id="d928a-139">페이지에서 도우미 사용</span><span class="sxs-lookup"><span data-stu-id="d928a-139">Using the Helper in a Page</span></span>

1. <span data-ttu-id="d928a-140">루트 폴더에서 *TestHelper*라는 비어 있는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-140">In the root folder, create a new blank file called *TestHelper.cshtml*.</span></span>
2. <span data-ttu-id="d928a-141">파일에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-141">Add the following code to the file:</span></span>

    [!code-html[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample2.html)]

    <span data-ttu-id="d928a-142">만든 도우미를 호출 하려면 `@`와 도우미가 있는 파일 이름, 점, 도우미 이름을 차례로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-142">To call the helper you created, use `@` followed by the file name where the helper is, a dot, and then the helper name.</span></span> <span data-ttu-id="d928a-143">*앱\_코드* 폴더에 여러 폴더가 있는 경우 `@FolderName.FileName.HelperName` 구문을 사용 하 여 모든 중첩 된 폴더 수준 내에서 도우미를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-143">(If you had multiple folders in the *App\_Code* folder, you could use the syntax `@FolderName.FileName.HelperName` to call your helper within any nested folder level).</span></span> <span data-ttu-id="d928a-144">괄호 안에 인용 부호로 추가 하는 텍스트는 도우미가 웹 페이지에 있는 메모의 일부로 표시 하는 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-144">The text that you add in quotation marks within the parentheses is the text that the helper will display as part of the note in the web page.</span></span>
3. <span data-ttu-id="d928a-145">페이지를 저장 하 고 브라우저에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-145">Save the page and run it in a browser.</span></span> <span data-ttu-id="d928a-146">도우미는 도우미를 호출한 경우 두 단락 사이에 메모 항목을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-146">The helper generates the note item right where you called the helper: between the two paragraphs.</span></span>

    ![브라우저의 페이지와 도우미가 지정 된 텍스트 주위에 상자를 넣는 태그를 생성 하는 방법을 보여 주는 스크린샷](creating-and-using-a-helper-in-an-aspnet-web-pages-site/_static/image1.png)

## <a name="additional-resources"></a><span data-ttu-id="d928a-148">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="d928a-148">Additional Resources</span></span>

<span data-ttu-id="d928a-149">[Razor 도우미로 서의 가로 메뉴](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2341)입니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-149">[Horizontal menu as a Razor helper](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2341).</span></span> <span data-ttu-id="d928a-150">Mike Pope이 블로그 항목은 태그, CSS 및 코드를 사용 하 여 도우미로 가로 메뉴를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-150">This blog entry by Mike Pope shows how to create a horizontal menu as a helper using markup, CSS, and code.</span></span>

<span data-ttu-id="d928a-151">[WebMatrix 및 ASP.NET MVC3에 대 한 ASP.NET 웹 페이지 도우미에서 HTML5 활용](http://geekswithblogs.net/wildturtle/archive/2010/11/08/html5-in-asp.net-web-pages-helpers-for-webmatrix-and_aspnet_mvc3.aspx)</span><span class="sxs-lookup"><span data-stu-id="d928a-151">[Leveraging HTML5 in ASP.NET Web Pages Helpers for WebMatrix and ASP.NET MVC3](http://geekswithblogs.net/wildturtle/archive/2010/11/08/html5-in-asp.net-web-pages-helpers-for-webmatrix-and_aspnet_mvc3.aspx).</span></span> <span data-ttu-id="d928a-152">Sam Abraham이 블로그 항목에는 HTML5 `Canvas` 요소를 렌더링 하는 도우미가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-152">This blog entry by Sam Abraham shows a helper that renders an HTML5 `Canvas` element.</span></span>

<span data-ttu-id="d928a-153">[WebMatrix의 @Helpers와 @Functions 간의 차이점](http://www.mikesdotnetting.com/Article/173/The-Difference-Between-@Helpers-and-@Functions-In-WebMatrix)입니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-153">[The Difference Between @Helpers and @Functions in WebMatrix](http://www.mikesdotnetting.com/Article/173/The-Difference-Between-@Helpers-and-@Functions-In-WebMatrix).</span></span> <span data-ttu-id="d928a-154">Mike Brind의이 블로그 항목에서는 구문 및 `@function` 구문과 각 구문을 사용 하는 경우 `@helper` 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d928a-154">This blog entry by Mike Brind describes `@helper` syntax and `@function` syntax and when to use each.</span></span>
