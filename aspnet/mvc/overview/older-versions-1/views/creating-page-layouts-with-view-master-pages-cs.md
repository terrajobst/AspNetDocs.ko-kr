---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
title: 보기 마스터 페이지를 사용 하 여 페이지C#레이아웃 만들기 () | Microsoft Docs
author: microsoft
description: 이 자습서에서는 보기 마스터 페이지를 활용 하 여 응용 프로그램에서 여러 페이지에 대 한 공통 페이지 레이아웃을 만드는 방법에 대해 알아봅니다. ...를 사용 하 여
ms.author: riande
ms.date: 10/16/2008
ms.assetid: dff54fcb-68b1-4488-89a2-ca97532d6a4c
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 026e3efb4ebf84016aa0f6a5fda4af549fdadfcb
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74594107"
---
# <a name="creating-page-layouts-with-view-master-pages-c"></a><span data-ttu-id="8acdd-104">보기 마스터 페이지를 사용하여 페이지 레이아웃 만들기(C#)</span><span class="sxs-lookup"><span data-stu-id="8acdd-104">Creating Page Layouts with View Master Pages (C#)</span></span>

<span data-ttu-id="8acdd-105">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="8acdd-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="8acdd-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="8acdd-106">Download PDF</span></span>](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_CS.pdf)

> <span data-ttu-id="8acdd-107">이 자습서에서는 보기 마스터 페이지를 활용 하 여 응용 프로그램에서 여러 페이지에 대 한 공통 페이지 레이아웃을 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-107">In this tutorial, you learn how to create a common page layout for multiple pages in your application by taking advantage of view master pages.</span></span> <span data-ttu-id="8acdd-108">예를 들어, 뷰 마스터 페이지를 사용 하 여 2 열 페이지 레이아웃을 정의 하 고 웹 응용 프로그램의 모든 페이지에 대해 2 열 레이아웃을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-108">You can use a view master page, for example, to define a two-column page layout and use the two-column layout for all of the pages in your web application.</span></span>

## <a name="creating-page-layouts-with-view-master-pages"></a><span data-ttu-id="8acdd-109">보기 마스터 페이지를 사용 하 여 페이지 레이아웃 만들기</span><span class="sxs-lookup"><span data-stu-id="8acdd-109">Creating Page Layouts with View Master Pages</span></span>

<span data-ttu-id="8acdd-110">이 자습서에서는 보기 마스터 페이지를 활용 하 여 응용 프로그램에서 여러 페이지에 대 한 공통 페이지 레이아웃을 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-110">In this tutorial, you learn how to create a common page layout for multiple pages in your application by taking advantage of view master pages.</span></span> <span data-ttu-id="8acdd-111">예를 들어, 뷰 마스터 페이지를 사용 하 여 2 열 페이지 레이아웃을 정의 하 고 웹 응용 프로그램의 모든 페이지에 대해 2 열 레이아웃을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-111">You can use a view master page, for example, to define a two-column page layout and use the two-column layout for all of the pages in your web application.</span></span>

<span data-ttu-id="8acdd-112">또한 보기 마스터 페이지를 활용 하 여 응용 프로그램의 여러 페이지에서 공통 콘텐츠를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-112">You also can take advantage of view master pages to share common content across multiple pages in your application.</span></span> <span data-ttu-id="8acdd-113">예를 들어 보기 마스터 페이지에서 웹 사이트 로고, 탐색 링크 및 배너 광고를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-113">For example, you can place your website logo, navigation links, and banner advertisements in a view master page.</span></span> <span data-ttu-id="8acdd-114">이렇게 하면 응용 프로그램의 모든 페이지가이 콘텐츠를 자동으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-114">That way, every page in your application would display this content automatically.</span></span>

<span data-ttu-id="8acdd-115">이 자습서에서는 새 보기 마스터 페이지를 만들고 마스터 페이지를 기준으로 새 콘텐츠 보기 페이지를 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-115">In this tutorial, you learn how to create a new view master page and create a new view content page based on the master page.</span></span>

### <a name="creating-a-view-master-page"></a><span data-ttu-id="8acdd-116">보기 마스터 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="8acdd-116">Creating a View Master Page</span></span>

<span data-ttu-id="8acdd-117">2 열 레이아웃을 정의 하는 보기 마스터 페이지를 만들어 시작 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-117">Let's start by creating a view master page that defines a two-column layout.</span></span> <span data-ttu-id="8acdd-118">Views\Shared 폴더를 마우스 오른쪽 단추로 클릭 하 고, 메뉴 옵션 **추가, 새 항목**을 차례로 선택 하 고, **Mvc 뷰 마스터 페이지** 템플릿을 선택 하 여 mvc 프로젝트에 새 뷰 마스터 페이지를 추가 합니다 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="8acdd-118">You add a new view master page to an MVC project by right-clicking the Views\Shared folder, selecting the menu option **Add, New Item**, and selecting the **MVC View Master Page** template (see Figure 1).</span></span>

<span data-ttu-id="8acdd-119">[보기 마스터 페이지를 추가 ![](creating-page-layouts-with-view-master-pages-cs/_static/image2.png)](creating-page-layouts-with-view-master-pages-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8acdd-119">[![Adding a view master page](creating-page-layouts-with-view-master-pages-cs/_static/image2.png)](creating-page-layouts-with-view-master-pages-cs/_static/image1.png)</span></span>

<span data-ttu-id="8acdd-120">**그림 01**: 보기 마스터 페이지 추가 ([전체 크기 이미지를 보려면 클릭](creating-page-layouts-with-view-master-pages-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="8acdd-120">**Figure 01**: Adding a view master page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image3.png))</span></span>

<span data-ttu-id="8acdd-121">응용 프로그램에서 둘 이상의 뷰 마스터 페이지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-121">You can create more than one view master page in an application.</span></span> <span data-ttu-id="8acdd-122">각 보기 마스터 페이지는 다른 페이지 레이아웃을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-122">Each view master page can define a different page layout.</span></span> <span data-ttu-id="8acdd-123">예를 들어, 특정 페이지에 2 열 레이아웃 및 다른 페이지를 포함 하 여 3 열 레이아웃을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-123">For example, you might want certain pages to have a two-column layout and other pages to have a three-column layout.</span></span>

<span data-ttu-id="8acdd-124">보기 마스터 페이지는 표준 ASP.NET MVC 뷰와 매우 유사 하 게 보입니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-124">A view master page looks very much like a standard ASP.NET MVC view.</span></span> <span data-ttu-id="8acdd-125">그러나 기본 보기와 달리 보기 마스터 페이지에는 하나 이상의 `<asp:ContentPlaceHolder>` 태그가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-125">However, unlike a normal view, a view master page contains one or more `<asp:ContentPlaceHolder>` tags.</span></span> <span data-ttu-id="8acdd-126">`<contentplaceholder>` 태그는 개별 콘텐츠 페이지에서 재정의할 수 있는 마스터 페이지 영역을 표시 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-126">The `<contentplaceholder>` tags are used to mark the areas of the master page that can be overridden in an individual content page.</span></span>

<span data-ttu-id="8acdd-127">예를 들어 1을 나열 하는 보기 마스터 페이지는 2 열 레이아웃을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-127">For example, the view master page in Listing 1 defines a two-column layout.</span></span> <span data-ttu-id="8acdd-128">두 개의 `<contentplaceholder>` 태그를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-128">It contains two `<contentplaceholder>` tags.</span></span> <span data-ttu-id="8acdd-129">각 열에 대해 하나의 `<ContentPlaceHolder>` 합니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-129">One `<ContentPlaceHolder>` for each column.</span></span>

<span data-ttu-id="8acdd-130">**목록 1 – `Views\Shared\Site.master`**</span><span class="sxs-lookup"><span data-stu-id="8acdd-130">**Listing 1 – `Views\Shared\Site.master`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample1.aspx)]

<span data-ttu-id="8acdd-131">목록 1에 있는 보기 마스터 페이지의 본문에는 두 열에 해당 하는 두 개의 `<div>` 태그가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-131">The body of the view master page in Listing 1 contains two `<div>` tags that correspond to the two columns.</span></span> <span data-ttu-id="8acdd-132">Css 스타일 시트 열 클래스는 두 `<div>` 태그에 모두 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-132">The Cascading Style Sheet column class is applied to both `<div>` tags.</span></span> <span data-ttu-id="8acdd-133">이 클래스는 마스터 페이지의 맨 위에 선언 된 스타일 시트에 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-133">This class is defined in the style sheet declared at the top of the master page.</span></span> <span data-ttu-id="8acdd-134">디자인 뷰로 전환 하 여 보기 마스터 페이지가 렌더링 되는 방식을 미리 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-134">You can preview how the view master page will be rendered by switching to Design view.</span></span> <span data-ttu-id="8acdd-135">소스 코드 편집기의 왼쪽 아래에 있는 디자인 탭을 클릭 합니다 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="8acdd-135">Click the Design tab at the bottom-left of the source code editor (see Figure 2).</span></span>

<span data-ttu-id="8acdd-136">[디자이너에서 마스터 페이지 미리 보기 ![](creating-page-layouts-with-view-master-pages-cs/_static/image5.png)](creating-page-layouts-with-view-master-pages-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="8acdd-136">[![Previewing a master page in the designer](creating-page-layouts-with-view-master-pages-cs/_static/image5.png)](creating-page-layouts-with-view-master-pages-cs/_static/image4.png)</span></span>

<span data-ttu-id="8acdd-137">**그림 02**: 디자이너에서 마스터 페이지 미리 보기 ([전체 크기 이미지를 보려면 클릭](creating-page-layouts-with-view-master-pages-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="8acdd-137">**Figure 02**: Previewing a master page in the designer ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image6.png))</span></span>

### <a name="creating-a-view-content-page"></a><span data-ttu-id="8acdd-138">콘텐츠 보기 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="8acdd-138">Creating a View Content Page</span></span>

<span data-ttu-id="8acdd-139">보기 마스터 페이지를 만든 후에는 보기 마스터 페이지를 기준으로 하나 이상의 콘텐츠 페이지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-139">After you create a view master page, you can create one or more view content pages based on the view master page.</span></span> <span data-ttu-id="8acdd-140">예를 들어 Views\Home 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가, 새 항목**, **MVC 뷰 콘텐츠 페이지** 템플릿을 차례로 선택 하 고 이름으로 .aspx를 입력 한 다음 **추가** 단추를 클릭 하 여 홈 컨트롤러에 대 한 인덱스 보기 콘텐츠 페이지를 만들 수 있습니다 (그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="8acdd-140">For example, you can create an Index view content page for the Home controller by right-clicking the Views\Home folder, selecting **Add, New Item**, selecting the **MVC View Content Page** template, entering the name Index.aspx, and clicking the **Add** button (see Figure 3).</span></span>

<span data-ttu-id="8acdd-141">[콘텐츠 보기 페이지를 추가 ![](creating-page-layouts-with-view-master-pages-cs/_static/image8.png)](creating-page-layouts-with-view-master-pages-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="8acdd-141">[![Adding a view content page](creating-page-layouts-with-view-master-pages-cs/_static/image8.png)](creating-page-layouts-with-view-master-pages-cs/_static/image7.png)</span></span>

<span data-ttu-id="8acdd-142">**그림 03**: 콘텐츠 보기 페이지 추가 ([전체 크기 이미지를 보려면 클릭](creating-page-layouts-with-view-master-pages-cs/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="8acdd-142">**Figure 03**: Adding a view content page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image9.png))</span></span>

<span data-ttu-id="8acdd-143">추가 단추를 클릭 하면 보기 마스터 페이지를 선택 하 여 콘텐츠 보기 페이지와 연결할 수 있는 새 대화 상자가 나타납니다 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="8acdd-143">After you click the Add button, a new dialog appears that enables you to select a view master page to associate with the view content page (see Figure 4).</span></span> <span data-ttu-id="8acdd-144">이전 섹션에서 만든 Site. 마스터 뷰 마스터 페이지로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-144">You can navigate to the Site.master view master page that we created in the previous section.</span></span>

<span data-ttu-id="8acdd-145">[마스터 페이지를 선택 ![](creating-page-layouts-with-view-master-pages-cs/_static/image11.png)](creating-page-layouts-with-view-master-pages-cs/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="8acdd-145">[![Selecting a master page](creating-page-layouts-with-view-master-pages-cs/_static/image11.png)](creating-page-layouts-with-view-master-pages-cs/_static/image10.png)</span></span>

<span data-ttu-id="8acdd-146">**그림 04**: 마스터 페이지 선택 ([전체 크기 이미지를 보려면 클릭](creating-page-layouts-with-view-master-pages-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="8acdd-146">**Figure 04**: Selecting a master page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image12.png))</span></span>

<span data-ttu-id="8acdd-147">사이트. 마스터 마스터 페이지를 기준으로 새 콘텐츠 보기 페이지를 만든 후에는 목록 2에 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-147">After you create a new view content page based on the Site.master master page, you get the file in Listing 2.</span></span>

<span data-ttu-id="8acdd-148">**목록 2 – `Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="8acdd-148">**Listing 2 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample2.aspx)]

<span data-ttu-id="8acdd-149">이 뷰에는 보기 마스터 페이지의 각 `<asp:ContentPlaceHolder>` 태그에 해당 하는 `<asp:Content>` 태그가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-149">Notice that this view contains a `<asp:Content>` tag that corresponds to each of the `<asp:ContentPlaceHolder>` tags in the view master page.</span></span> <span data-ttu-id="8acdd-150">각 `<asp:Content>` 태그는 재정의 하는 특정 `<asp:ContentPlaceHolder>`를 가리키는 ContentPlaceHolderID 특성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-150">Each `<asp:Content>` tag includes a ContentPlaceHolderID attribute that points to the particular `<asp:ContentPlaceHolder>` that it overrides.</span></span>

<span data-ttu-id="8acdd-151">또한 목록 2의 콘텐츠 보기 페이지에는 일반 여는 태그와 닫는 HTML 태그가 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-151">Notice, furthermore, that the content view page in Listing 2 does not contain any of the normal opening and closing HTML tags.</span></span> <span data-ttu-id="8acdd-152">예를 들어 열기 및 닫기 `<html>` 또는 `<head>` 태그가 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-152">For example, it does not contain the opening and closing `<html>` or `<head>` tags.</span></span> <span data-ttu-id="8acdd-153">모든 일반 여는 태그와 닫는 태그는 보기 마스터 페이지에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-153">All of the normal opening and closing tags are contained in the view master page.</span></span>

<span data-ttu-id="8acdd-154">콘텐츠 보기 페이지에 표시 하려는 콘텐츠는 `<asp:Content>` 태그 안에 배치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-154">Any content that you want to display in a view content page must be placed within a `<asp:Content>` tag.</span></span> <span data-ttu-id="8acdd-155">HTML 또는 기타 콘텐츠를 이러한 태그 외부에 두면 페이지를 보려고 할 때 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-155">If you place any HTML or other content outside of these tags, then you will get an error when you attempt to view the page.</span></span>

<span data-ttu-id="8acdd-156">콘텐츠 뷰 페이지에서 마스터 페이지의 모든 `<asp:ContentPlaceHolder>` 태그를 재정의할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-156">You don't need to override every `<asp:ContentPlaceHolder>` tag from a master page in a content view page.</span></span> <span data-ttu-id="8acdd-157">태그를 특정 콘텐츠로 바꾸려는 경우에만 `<asp:ContentPlaceHolder>` 태그를 재정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-157">You only need to override a `<asp:ContentPlaceHolder>` tag when you want to replace the tag with particular content.</span></span>

<span data-ttu-id="8acdd-158">예를 들어 목록 3의 수정 된 인덱스 뷰에는 두 개의 `<asp:Content>` 태그만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-158">For example, the modified Index view in Listing 3 contains only two `<asp:Content>` tags.</span></span> <span data-ttu-id="8acdd-159">각 `<asp:Content>` 태그에는 일부 텍스트가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-159">Each of the `<asp:Content>` tags includes some text.</span></span>

<span data-ttu-id="8acdd-160">**목록 3 – `Views\Home\Index.aspx (modified)`**</span><span class="sxs-lookup"><span data-stu-id="8acdd-160">**Listing 3 – `Views\Home\Index.aspx (modified)`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample3.aspx)]

<span data-ttu-id="8acdd-161">목록 3의 보기가 요청 되 면 그림 5에서 페이지가 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-161">When the view in Listing 3 is requested, it renders the page in Figure 5.</span></span> <span data-ttu-id="8acdd-162">뷰는 두 개의 열이 있는 페이지를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-162">Notice that the view renders a page with two columns.</span></span> <span data-ttu-id="8acdd-163">또한 콘텐츠 보기 페이지의 콘텐츠가 보기 마스터 페이지의 내용과 병합 됨을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-163">Notice, furthermore, that the content from the view content page is merged with the content from the view master page</span></span>

<span data-ttu-id="8acdd-164">[인덱스 보기 콘텐츠 페이지 ![](creating-page-layouts-with-view-master-pages-cs/_static/image14.png)](creating-page-layouts-with-view-master-pages-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="8acdd-164">[![The Index view content page](creating-page-layouts-with-view-master-pages-cs/_static/image14.png)](creating-page-layouts-with-view-master-pages-cs/_static/image13.png)</span></span>

<span data-ttu-id="8acdd-165">**그림 05**: 인덱스 뷰 콘텐츠 페이지 ([전체 크기 이미지를 보려면 클릭](creating-page-layouts-with-view-master-pages-cs/_static/image15.png))</span><span class="sxs-lookup"><span data-stu-id="8acdd-165">**Figure 05**: The Index view content page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image15.png))</span></span>

### <a name="modifying-view-master-page-content"></a><span data-ttu-id="8acdd-166">보기 마스터 페이지 내용 수정</span><span class="sxs-lookup"><span data-stu-id="8acdd-166">Modifying View Master Page Content</span></span>

<span data-ttu-id="8acdd-167">보기 마스터 페이지를 사용할 때 발생 하는 문제 중 하나는 다른 보기 콘텐츠 페이지가 요청 될 때 보기 마스터 페이지 내용을 수정 하는 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-167">One issue that you encounter almost immediately when working with view master pages is the problem of modifying view master page content when different view content pages are requested.</span></span> <span data-ttu-id="8acdd-168">예를 들어 웹 응용 프로그램의 각 페이지에 고유한 제목을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-168">For example, you want each page in your web application to have a unique title.</span></span> <span data-ttu-id="8acdd-169">그러나 제목은 뷰 마스터 페이지에서 선언 되 고 콘텐츠 보기 페이지에는 선언 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-169">However, the title is declared in the view master page and not in the view content page.</span></span> <span data-ttu-id="8acdd-170">따라서 각 콘텐츠 보기 페이지에 대 한 페이지 제목을 사용자 지정 하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="8acdd-170">So, how do you customize the page title for each view content page?</span></span>

<span data-ttu-id="8acdd-171">콘텐츠 보기 페이지에 표시 되는 제목을 수정할 수 있는 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-171">There are two ways that you can modify the title displayed by a view content page.</span></span> <span data-ttu-id="8acdd-172">먼저 콘텐츠 보기 페이지의 맨 위에 선언 된 `<%@ page %>` 지시문의 title 특성에 페이지 제목을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-172">First, you can assign a page title to the title attribute of the `<%@ page %>` directive declared at the top of a view content page.</span></span> <span data-ttu-id="8acdd-173">예를 들어 인덱스 뷰에 페이지 제목 "Super 유용한 웹 사이트"를 할당 하려는 경우 인덱스 뷰의 맨 위에 다음 지시문을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-173">For example, if you want to assign the page title "Super Great Website" to the Index view, then you can include the following directive at the top of the Index view:</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample4.aspx)]

<span data-ttu-id="8acdd-174">인덱스 뷰가 브라우저에 렌더링 되 면 원하는 제목이 브라우저 제목 표시줄에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-174">When the Index view is rendered to the browser, the desired title appears in the browser title bar:</span></span>

<span data-ttu-id="8acdd-175">[![브라우저 제목 표시줄](creating-page-layouts-with-view-master-pages-cs/_static/image17.png)](creating-page-layouts-with-view-master-pages-cs/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="8acdd-175">[![Browser title bar](creating-page-layouts-with-view-master-pages-cs/_static/image17.png)](creating-page-layouts-with-view-master-pages-cs/_static/image16.png)</span></span>

<span data-ttu-id="8acdd-176">마스터 뷰 페이지는 제목 특성이 작동 하기 위해 충족 해야 하는 한 가지 중요 한 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-176">There is one important requirement that a master view page must satisfy in order for the title attribute to work.</span></span> <span data-ttu-id="8acdd-177">보기 마스터 페이지에는 헤더에 대 한 일반 `<head>` 태그가 아닌 `<head runat="server">` 태그가 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-177">The view master page must contain a `<head runat="server">` tag instead of a normal `<head>` tag for its header.</span></span> <span data-ttu-id="8acdd-178">`<head>` 태그에 runat = "server" 특성이 포함 되지 않은 경우 제목이 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-178">If the `<head>` tag does not include the runat="server" attribute then the title won't appear.</span></span> <span data-ttu-id="8acdd-179">기본 보기 마스터 페이지는 필수 `<head runat="server">` 태그를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-179">The default view master page includes the required `<head runat="server">` tag.</span></span>

<span data-ttu-id="8acdd-180">개별 콘텐츠 보기 페이지에서 마스터 페이지 콘텐츠를 수정 하는 다른 방법은 `<asp:ContentPlaceHolder>` 태그에서 수정 하려는 영역을 래핑하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-180">An alternative approach to modifying master page content from an individual view content page is to wrap the region that you want to modify in a `<asp:ContentPlaceHolder>` tag.</span></span> <span data-ttu-id="8acdd-181">예를 들어 마스터 뷰 페이지에서 렌더링 되는 제목 뿐만 아니라 meta 태그도 변경 하려고 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-181">For example, imagine that you want to change not only the title, but also the meta tags, rendered by a master view page.</span></span> <span data-ttu-id="8acdd-182">목록 4의 마스터 뷰 페이지에는 `<head>` 태그 안에 `<asp:ContentPlaceHolder>` 태그가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-182">The master view page in Listing 4 contains a `<asp:ContentPlaceHolder>` tag within its `<head>` tag.</span></span>

<span data-ttu-id="8acdd-183">**목록 4 – `Views\Shared\Site2.master`**</span><span class="sxs-lookup"><span data-stu-id="8acdd-183">**Listing 4 – `Views\Shared\Site2.master`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample5.aspx)]

<span data-ttu-id="8acdd-184">목록 4의 `<asp:ContentPlaceHolder>` 태그에는 기본 내용 (기본 제목 및 기본 메타 태그)이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-184">Notice that the `<asp:ContentPlaceHolder>` tag in Listing 4 includes default content: a default title and default meta tags.</span></span> <span data-ttu-id="8acdd-185">개별 콘텐츠 보기 페이지에서이 `<asp:ContentPlaceHolder>` 태그를 재정의 하지 않으면 기본 콘텐츠가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-185">If you don't override this `<asp:ContentPlaceHolder>` tag in an individual view content page, then the default content will be displayed.</span></span>

<span data-ttu-id="8acdd-186">목록 5의 콘텐츠 뷰 페이지는 사용자 지정 제목 및 사용자 지정 메타 태그를 표시 하기 위해 `<asp:ContentPlaceHolder>` 태그를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-186">The content view page in Listing 5 overrides the `<asp:ContentPlaceHolder>` tag in order to display a custom title and custom meta tags.</span></span>

<span data-ttu-id="8acdd-187">**목록 5 – `Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="8acdd-187">**Listing 5 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample6.aspx)]

### <a name="summary"></a><span data-ttu-id="8acdd-188">요약</span><span class="sxs-lookup"><span data-stu-id="8acdd-188">Summary</span></span>

<span data-ttu-id="8acdd-189">이 자습서에서는 마스터 페이지 보기 및 콘텐츠 페이지 보기에 대 한 기본 소개를 제공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-189">This tutorial provided you with a basic introduction to view master pages and view content pages.</span></span> <span data-ttu-id="8acdd-190">새 보기 마스터 페이지를 만들고 이러한 페이지를 기반으로 보기 콘텐츠 페이지를 만드는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-190">You learned how to create new view master pages and create view content pages based on them.</span></span> <span data-ttu-id="8acdd-191">또한 특정 콘텐츠 보기 페이지에서 보기 마스터 페이지의 내용을 수정 하는 방법도 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="8acdd-191">We also examined how you can modify the content of a view master page from a particular view content page.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8acdd-192">[이전](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
> [다음](passing-data-to-view-master-pages-cs.md)</span><span class="sxs-lookup"><span data-stu-id="8acdd-192">[Previous](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
[Next](passing-data-to-view-master-pages-cs.md)</span></span>
